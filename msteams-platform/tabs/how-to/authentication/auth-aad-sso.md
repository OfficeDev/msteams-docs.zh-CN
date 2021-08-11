---
title: 选项卡的单一登录支持
description: '介绍 SSO (单一) '
ms.topic: how-to
localization_priority: Normal
keywords: teams 身份验证 SSO AAD 单一登录 api
ms.openlocfilehash: f51f34f103682207551d1b53d47a763f7c3b464085b6806c1241c1e14636bc06
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2021
ms.locfileid: "57701892"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>单一登录 (SSO) 选项卡支持

用户通过Microsoft Teams、学校或 Microsoft 帐户（Office 365、Outlook等）登录登录。 通过允许单一登录在桌面或移动客户端上授权Teams选项卡或任务模块，可以充分利用这一点。 如果用户同意使用你的应用，则当他们自动登录时，他们不需要在另一台设备上再次同意。 此外，会预取访问令牌，以改进性能和加载时间。

> [!NOTE]
> **Teams SSO 的移动客户端版本**  
>
> ✔Teams Android (1416/1.0.0.2020073101 及更高版本) 
>
> ✔Teams iOS (_版本_：2.0.18 及更高版本)   
>
> 为了获得最佳体验Teams，请使用最新版本的 iOS 和 Android。

> [!NOTE]
> **快速入门**  
>
> 开始使用选项卡 SSO 的最简单路径是使用适用于 Teams 的 Visual Studio Code。 有关详细信息，请参阅[SSO with Teams toolkit 和 Visual Studio Code for tabs](../../../toolkit/visual-studio-code-tab-sso.md)

## <a name="how-sso-works-at-runtime"></a>运行时 SSO 的工作方式

下图显示了 SSO 进程的工作原理：

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. 在选项卡中，对 `getAuthToken()` 进行 JavaScript 调用。 这将Teams获取选项卡应用程序的身份验证令牌。
2. 如果这是当前用户第一次使用你的选项卡应用程序，则当需要同意或处理双重身份验证等逐步身份验证时，会提示你同意。
3. Teams从当前用户的 AAD Azure Active Directory (终结点) 选项卡应用程序令牌。
4. AAD 将选项卡应用程序令牌发送到Teams应用程序。
5. Teams将选项卡应用程序令牌作为调用返回的结果对象的一部分发送到 `getAuthToken()` 选项卡。
6. 令牌使用 JavaScript 在选项卡应用程序中进行分析，以提取所需信息，如用户的电子邮件地址。

> [!NOTE]
> 仅在同意一组有限的用户级 API（即电子邮件、配置文件、offline_access `getAuthToken()` OpenId）时有效。 它不能用于进一步Graph范围，如 `User.Read` 或 `Mail.Read` 。 有关建议的解决方法，请参阅使用[权限获取Graph令牌](#get-an-access-token-with-graph-permissions)。


SSO API 还适用于 [嵌入](../../../task-modules-and-cards/what-are-task-modules.md) Web 内容的任务模块。

## <a name="develop-an-sso-microsoft-teams-tab"></a>"开发 SSO Microsoft Teams"选项卡

本节介绍创建使用 SSO 的 Teams 选项卡所涉及的任务。 这些任务与语言和框架无关。

### <a name="1-create-your-aad-application"></a>1. 创建 AAD 应用程序

**在 AAD 门户概述 [中注册](https://azure.microsoft.com/features/azure-portal/) 应用程序**

1. 获取[AAD 应用程序 ID。](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in) 
1. 指定应用程序所需的 AAD 终结点和（可选）Graph。
1. [授予对](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources)桌面Teams Web 和移动应用程序的权限。
1. 通过选择Teams"范围"按钮预授权用户，在打开的面板中，输入"access_as_user"作为 **"范围名称"。**

> [!NOTE]
> 您必须了解一些重要的限制：
>
> * 仅支持用户Graph API 权限，即电子邮件、配置文件、offline_access、OpenId。 如果必须有权访问诸如 或 Graph 等作用域，请参阅获取具有 Graph `User.Read` `Mail.Read` [权限的访问令牌](#get-an-access-token-with-graph-permissions)。
> * 应用程序的域名与为 AAD 应用程序注册的域名相同，这一点很重要。
> * 目前不支持每个应用多个域。

**通过 AAD 门户注册应用**

1. 在 AAD 应用注册门户 [中注册新](https://go.microsoft.com/fwlink/?linkid=2083908) 应用程序。
1. 选择 **"新建注册"。** 将显示 **"注册应用程序"** 页。
1. 在 **"注册应用程序"** 页中，输入以下值：
    1. 为 **应用输入** 名称。
    2. 选择" **支持的帐户类型"，** 选择"单个租户"或"多租户帐户类型"。 ¹
    * 保留“重定向 URI”为空。
    3. 选择“注册”。
1. 在概述页上，复制并保存应用程序 (**客户端) ID**。 更新应用程序清单时，稍后必须Teams该清单。
1. 在“**管理**”下，选择“**公开 API**”。

    > [!NOTE]
    > 如果要使用自动程序和选项卡生成应用，请输入"应用程序 ID URI"作为 `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。

1. 选择 **"设置**"链接以生成格式为 的应用程序 ID URI。 `api://{AppID}` 在双正斜杠和 GUID 之间插入完全限定域名，末尾附加一个正斜杠"/"。 整个 ID 的形式必须为 `api://fully-qualified-domain-name.com/{AppID}` 。 1。例如 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` ， 。 完全限定的域名是提供应用时可读的域名。 如果使用的是隧道服务（如 ngrok），则必须在 ngrok 子域发生更改时更新此值。
1. 选择“**添加作用域**”。 在打开的面板中，输入 **access_as_user** 作为范围 **名称**。
1. 在 **"Who同意？"** 框中，输入 **"管理员和用户"。**
1. 在框中输入详细信息，以使用适用于作用域的值配置管理员和用户同意 `access_as_user` 提示：
    * **管理员同意标题:** Teams 可以访问用户的配置文件。
    * **管理员同意** 说明：Teams当前用户调用应用的 Web API。
    * **用户同意标题**：Teams可以访问你的个人资料并代表你提出请求。
    * **用户同意Teams：** 用户可以使用你拥有的相同权限调用此应用的 API。
1. 确保将“状态”设置为“已启用”。
1. 选择 **"添加范围** "以保存详细信息。 文本字段下方显示的 **作用域** 名称的域部分必须自动匹配上一步中设置的应用程序 **ID** URI，并 `/access_as_user` 追加到末尾 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user` 。
1. 在 **"授权客户端应用程序** "部分，确定要针对应用程序的 Web 应用程序授权的应用程序。 选择 **"添加客户端应用程序"。** 输入以下每个客户端 ID，然后选择在上一步中创建的授权作用域：
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264`用于Teams或桌面应用程序。
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346`Teams Web 应用程序。
1. 导航到 **"API 权限"。** 选择 **"添加**  >  **Microsoft Graph** 委派权限"，然后从 API 添加以下  >  Graph权限：
    * 默认情况下启用 User.Read
    * 电子邮件
    * offline_access
    * OpenId
    * 个人资料

1. 导航到 **身份验证**。

    如果应用尚未获得 IT 管理员同意，用户第一次使用应用时必须同意。

    若要输入重定向 URI：
    * 选择 **"添加平台"。**
    * 选择 **"Web"。**
    * 输入 **应用的重定向 URI。** 这是一个页面，其中成功的隐式授予流将重定向用户。 这是在步骤 5 中输入的完全限定域名，后跟发送身份验证响应的 API 路由。 如果您遵循任何示例Teams，则此为 `https://subdomain.example.com/auth-end` 。

    通过选中以下框启用隐式授予：✔ ID 令牌✔访问令牌

恭喜！ 已完成应用注册先决条件，可以继续选项卡 SSO 应用。

> [!NOTE]
>
> * ¹ 如果你的 AAD 应用在 Teams 中进行身份验证请求的同一租户中注册，则不能要求用户同意并获取访问令牌。 只有在 AAD 应用注册到其他租户时，用户才同意这些权限。
> * 你已经收到一个错误，指出主机名不得基于已拥有域。 若要将自定义域添加到 AAD 并注册它，请按照向 [AAD](/azure/active-directory/fundamentals/add-custom-domain) 添加自定义域名过程操作，然后重复步骤 5。 如果未使用租户租户中的管理员凭据登录，Office 365此错误。
> * 如果未在返回的访问令牌 (UPN) 用户主体名称，可以在 AAD 中将其添加为可选声明。 [](/azure/active-directory/develop/active-directory-optional-claims)

### <a name="2-update-your-teams-application-manifest"></a>2. 更新Teams应用程序清单

使用以下代码将新属性添加到Teams清单：

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

* **WebApplicationInfo** 是以下元素的父元素：

> [!div class="checklist"]
> * **id** - 应用程序的客户端 ID。 这是在向 Azure AD 注册应用程序时获取的应用程序 ID。
>* **resource** - 应用程序的域和子域。 这是相同的 URI (包括你在步骤 `api://` 6) 注册的协议 `scope` 和协议。 不得在资源 `access_as_user` 中包括路径。 此 URI 的域部分必须与在应用程序清单的 URL 中使用的域（包括任何子Teams匹配。

> [!NOTE]
>
>* AAD 应用的资源通常是其网站 URL 和 appID (根，例如 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`) 。 此值还用于确保你的请求来自同一个域。 确保选项卡 `contentURL` 的 使用与资源属性相同的域。
>* 必须使用清单版本 1.5 或更高版本来实现 `webApplicationInfo` 字段。

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. 从客户端代码获取身份验证令牌

使用以下身份验证 API：

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

调用 时，用户级别权限需要其他用户同意，将显示一个对话框，以向用户授予 `getAuthToken` 其他同意。

在成功回调中收到访问令牌后，可以解码访问令牌以查看与该令牌关联的声明。 （可选）你可以手动将访问令牌复制并粘贴到工具中，jwt.ms 检查其内容[](https://jwt.ms/)。 如果未在返回的访问令牌中接收 UPN，可以在 AAD 中将其添加为[](/azure/active-directory/develop/active-directory-optional-claims)可选声明。

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-sample"></a>代码示例

|**示例名称**|**说明**|**C#**|**Node.js**|
|---------------|---------------|------|--------------|
| 选项卡 SSO |Microsoft Teams Azure AD SSO 的选项卡示例应用| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[查看](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs)、 </br>[Teams Toolkit](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>已知限制

### <a name="get-an-access-token-with-graph-permissions"></a>获取具有权限Graph令牌

我们的 SSO 当前实现仅授予用户级别权限的许可，这些权限不能用于进行Graph调用。 若要获取执行 Graph 调用 (所需的) 作用域的权限，SSO 解决方案必须实现自定义 Web 服务，以交换从 Teams JavaScript SDK 获取的令牌，以交换包含所需范围的令牌。 这是使用 AAD 的代表 [流完成的](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)。

#### <a name="tenant-admin-consent"></a>租户管理员同意

代表组织作为租户管理员同意的一种简单方法就是引用 `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>` 。

#### <a name="ask-for-additional-consent-using-the-auth-api"></a>使用身份验证 API 请求其他同意

获取其他Graph范围的另一个方法是使用我们现有的基于 Web 的[Azure AD](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)身份验证方法显示同意对话框，该方法涉及弹出 Azure AD 同意对话框。 

**使用身份验证 API 请求其他同意**

1. 使用 检索到的令牌需要使用 AAD 代表流在服务器端进行交换，才能访问这些附加 Graph `getAuthToken()` API。 [](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) 确保对此 exchange 使用 v2 Graph终结点。
2. 如果交换失败，AAD 将返回无效的授予异常。 通常有两条错误消息中的一条或 `invalid_grant` `interaction_required` 。
3. 当交换失败时，必须请求其他同意。 在 UI (显示) 要求用户授予其他同意。 此 UI 必须包含使用 AAD 身份验证 API 触发 [AAD 同意对话框的按钮](~/concepts/authentication/auth-silent-aad.md)。
4. 请求 AAD 的其他同意时，必须在 `prompt=consent` 查询 [字符串参数](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) 中包括 AAD，否则 AAD 不要求其他范围。
    * 而不是 `?scope={scopes}`
    * 使用此 `?prompt=consent&scope={scopes}`
    * 确保 `{scopes}` 包括提示用户的所有范围，例如 Mail.Read 或 User.Read。
5. 在用户授予其他权限后，重试代表流获取这些附加 API 的访问权限。

### <a name="non-aad-authentication"></a>非 AAD 身份验证

上述身份验证解决方案仅适用于支持 AAD 作为标识提供程序的应用和服务。 想要使用基于非 AAD 的服务进行身份验证的应用必须继续使用基于弹出窗口的 [Web 身份验证流](~/concepts/authentication.md)。

> [!NOTE]
> AAD B2C 租户内的客户拥有的应用支持 SSO。
