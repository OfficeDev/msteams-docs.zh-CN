---
title: 选项卡的单一登录支持
description: '介绍 SSO (单一) '
ms.topic: how-to
keywords: teams 身份验证 SSO AAD 单一登录 api
ms.openlocfilehash: 72fbafe49e021b0cc23dcdaeee7eb5fe82ee23de
ms.sourcegitcommit: b99ed616db734371e4af4594b7e895c5b05737c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/09/2021
ms.locfileid: "50162885"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>单一登录 (SSO) 选项卡支持

用户通过工作、学校或 Microsoft 帐户登录 Microsoft Teams (Office 365、Outlook 等) 。 你可以利用这一点，允许单一登录来授权 Microsoft Teams 选项卡 (或任务模块) 桌面或移动客户端上。 因此，如果用户同意使用你的应用，则他们不需要在另一台设备上再次同意，他们将自动登录。 此外，我们会预取访问令牌，以改进性能和加载时间。

> [!NOTE]
> **支持 SSO 的 Teams 移动客户端版本**  
>
> ✔适用于 Android (1416/1.0.0.2020073101 及更高版本) 
>
> ✔ iOS (_版本_：2.0.18 及更高版本)   
>
> 为了获得最佳 Teams 体验，请使用最新版本的 iOS 和 Android。

> [!NOTE]
> **快速入门**  
>
> 开始使用选项卡 SSO 的最简单路径是 Microsoft Teams Toolkit for Visual Studio Code。 [了解更多](../../../toolkit/visual-studio-code-tab-sso.md)

## <a name="how-sso-works-at-runtime"></a>运行时 SSO 的工作方式

下图显示了 SSO 过程的工作原理：

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. 在选项卡中，对进行 JavaScript 调用 `getAuthToken()` 。 这将指示 Teams 获取选项卡应用程序的身份验证令牌。
2. 如果这是当前用户第一次使用选项卡应用程序，当需要同意) 或处理双重身份验证 (例如双重身份验证) 时，系统将会提示你同意 (。
3. Teams 从 Azure AD 终结点为当前用户请求选项卡应用程序令牌。
4. Azure AD 将选项卡应用程序令牌发送到 Teams 应用程序。
5. Teams 将选项卡应用程序令牌作为调用返回的结果对象的一部分发送到 `getAuthToken()` 选项卡。
6. 令牌将在选项卡应用程序中通过 JavaScript 进行分析，以提取所需信息，如用户的电子邮件地址。

> [!NOTE]
> 仅对同意一组有限的用户级 API（电子邮件、配置文件、offline_access 和 OpenId）有效，对进一步 Microsoft Graph 作用域（如 `getAuthToken()` `User.Read` 或）无效 `Mail.Read` 。 如果需要其他 Graph 范围，请参阅本文档末尾的部分，了解建议的 [解决方法](#apps-that-require-additional-microsoft-graph-scopes)。

SSO API 还将 [在嵌入](../../../task-modules-and-cards/what-are-task-modules.md) Web 内容的任务模块中工作。

## <a name="develop-an-sso-microsoft-teams-tab"></a>开发 SSO Microsoft Teams 选项卡

本节介绍创建使用 SSO 的 Teams 选项卡所涉及的任务。 此处介绍的这些任务与语言和框架无关。

### <a name="1-create-your-azure-active-directory-azure-ad-application"></a>1. 创建 Azure Active Directory (Azure AD) 应用程序

#### <a name="registering-your-application-in-theazure-ad-portal-overview"></a>在[Azure AD](https://azure.microsoft.com/features/azure-portal/) 门户中注册应用程序概述：

1. 获取[Azure AD 应用程序 ID。](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)
2. 指定应用程序对 Azure AD 终结点和（可选）Microsoft Graph 所需的权限。
3. [授予 Teams](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) 桌面、Web 和移动应用程序的权限。
4. 通过选择"添加范围 **"** 按钮来预授权 Teams，在打开的面板中输入 `access_as_user` 为范围 **名称**。

> [!NOTE]
> 应了解一些重要限制：
>
> * 我们仅支持用户级别的 Microsoft Graph API 权限，即电子邮件、配置文件、offline_access、OpenId。 如果你需要访问其他 Microsoft Graph 作用域， (或) ，请参阅本文档 `User.Read` 末尾 `Mail.Read` 的推荐解决方法。 [](#apps-that-require-additional-microsoft-graph-scopes)
> * 应用程序的域名与为 Azure AD 应用程序注册的域名相同，这一点很重要。
> * 目前，我们不支持每个应用多个域。
> * 我们不支持使用该域的应用程序，因为它太常见， `azurewebsites.net` 并且可能是一种安全风险。 但是，我们正在积极寻求删除此限制。

#### <a name="registering-your-app-through-the-azure-active-directory-portal-in-depth"></a>通过 Azure Active Directory 门户进行深入注册应用：

1. 在 Azure Active [Directory - 应用注册门户中注册新](https://go.microsoft.com/fwlink/?linkid=2083908) 应用程序。
2. 选择 **"新建** 注册"， *在"注册应用程序"页上*，设置以下值：
    * 将 **名称** 设置为应用名称。
    * 选择 **支持的帐户类型 (** 任何帐户类型都) ¹
    * 保留“重定向 URI”为空。
    * 选择“注册”。
3. 在概述页上，复制并保存应用程序 (**客户端) ID。** 稍后在更新 Teams 应用程序清单时将需要它。
4. 在“**管理**”下，选择“**公开 API**”。 
5. 选择 **"设置** "链接以生成应用程序 ID URI，格式为 `api://{AppID}` 。 插入您的完全限定域名 (双正斜杠和 GUID 之间追加一个) 斜杠"/"。 整个 ID 的形式 `api://fully-qualified-domain-name.com/{AppID}` 应为：
    * ex： `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` .
    
    完全限定的域名是提供应用服务的人工可读域名。 如果使用的是隧道服务（如 ngrok），则需要在 ngrok 子域更改时更新此值。 
6. 选择“添加一个作用域”按钮。 在打开的面板中，输入 `access_as_user` 作为“作用域名称”。
7. 设置 **谁可以同意？**`Admins and users`
8. 使用适用于作用域的值填写用于配置管理员和用户同意提示的 `access_as_user` 字段：
    * **管理员同意标题：** Teams 可以访问用户配置文件。
    * **管理员同意说明**：允许 Teams 以当前用户模式调用应用的 Web API。
    * **用户同意标题**：Teams 可以访问用户配置文件并代表用户提出请求。
    * **用户同意说明：** 允许 Teams 使用与用户相同的权限调用此应用的 API。
9. 确保 **状态** 设置为 **"已启用"**
10. 选择要 **保存的"添加** 范围"按钮 
    * 显示在文本字段正下方的范围名称的域部分应自动匹配上一步中设置的应用程序 **ID** URI，并追加 `/access_as_user` 到末尾：
        * `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`
11. 在 **"授权客户端应用程序** "部分，确定要针对应用的 Web 应用程序授权的应用程序。 选择 *"添加客户端应用程序"。* 输入以下每个客户端 ID，然后选择在上一步中创建的授权范围：
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Teams 移动/桌面应用程序) 
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Teams Web 应用程序) 
12. 导航到 **API 权限**。 选择 *"添加* Microsoft Graph 委派权限"权限，然后从 Microsoft Graph API 添加  >    >  以下权限：
    * User.Read (默认启用) 
    * email
    * offline_access
    * OpenId
    * 个人资料

13. 导航到 **身份验证**

    如果应用尚未获得 IT 管理员同意，则用户第一次使用应用时必须同意。

    设置重定向 URI：
    * 选择 **"添加平台"。**
    * 选择 **Web**。
    * 输入 **应用的重定向 URI。** 这将是一个页面，其中成功的隐式授予流将重定向用户。 这将是在步骤 5 中输入的完全限定域名，后跟应发送身份验证响应的 API 路由。 如果你正在遵循任何 Teams 示例，这将： `https://subdomain.example.com/auth-end`

    接下来，通过选中以下框启用隐式授予：  
    ✔ ID 令牌  
    ✔访问令牌  
    
恭喜！ 已完成应用注册先决条件，可以继续选项卡 SSO 应用。     

> [!NOTE]
>
> * ¹ 如果你的 Azure AD 应用在 Teams 中提出身份验证请求的同一租户中注册，将不会要求用户同意，并且将被授予访问令牌。 如果用户在不同的租户中注册 Azure AD 应用，则只需同意这些权限。
> * 1 如果出现错误，指出域已拥有并且你是所有者，请按照快速入门中的过程操作：将自定义域名添加到 [Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) 以注册域，然后重复上述步骤 5。  (如果不使用 Office 365 租赁服务中的管理员凭据登录，也会) 。
> * 如果未在返回的访问令牌 (UPN) 主体名称，可以在 Azure AD 中将其添加为可选声明。 [](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims)

### <a name="2-update-your-microsoft-teams-application-manifest"></a>2. 更新 Microsoft Teams 应用程序清单

将新属性添加到 Microsoft Teams 清单：

* **WebApplicationInfo** - 以下元素的父元素：

> [!div class="checklist"]
> * **id** - 应用程序的客户端 ID。 这是在向 Azure AD 注册应用程序时获取的应用程序 ID。
>* **resource** - 应用程序的域和子域。 这是相同的 URI (，包括) 步骤 6 中创建时注册 `api://` `scope` 的协议。 不应在资源 `access_as_user` 中包括路径。 此 URI 的域部分应匹配 Teams 应用程序清单的 URL 中使用的域，包括任何子域。

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

> [!NOTE]
>
>* AAD 应用的资源通常是其站点 URL 和 appID 的根 (例如 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`) 。 我们还使用此值来确保你的请求来自同一个域。 因此，请确保选项卡使用的域与资源属性 `contentURL` 相同。
>* 您需要使用清单版本 1.5 或更高版本来实现 `webApplicationInfo` 该字段。

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. 从客户端代码获取身份验证令牌

下面是身份验证 API 的外观：

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

当你呼叫时（对于用户级别 (需要其他用户同意) -我们将向用户显示一个对话框，鼓励他们授予 `getAuthToken` 其他同意。 

在成功回调中收到访问令牌后，你可以解码访问令牌以查看与该令牌关联的声明。  (，也可以手动将访问令牌复制/粘贴到工具（如 JWT.io）中，以检查[](https://jwt.io/)访问令牌) 。 如果未在返回的访问令牌 (UPN) 主体名称，可以在 Azure AD 中将其添加为可选声明。 [](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims)

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-sample"></a>代码示例

|**示例名称**|**说明**|**C#**|**TypeScript**|
|---------------|---------------|------|--------------|
| Tab SSO |用于选项卡 Azure AD SSO 的 Microsoft Teams 示例应用| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[视图](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs)， </br>[Teams Toolkit](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>已知限制

### <a name="apps-that-require-additional-microsoft-graph-scopes"></a>需要其他 Microsoft Graph 作用域的应用

我们当前针对 SSO 的实现仅授予用户级别权限（电子邮件、配置文件、offline_access、OpenId）的许可，而不是针对其他 API (如 User.Read 或 Mail.Read) 。 如果你的应用需要进一步使用 Microsoft Graph 范围，下面是一些启用的解决方法：

#### <a name="tenant-admin-consent"></a>租户管理员同意

最简单的方法是让租户管理员代表组织预先同意。 这意味着用户不需要同意这些作用域，然后可以使用 Azure AD 的代表流自由交换令牌 [服务器端](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)。 此解决方法对于内部业务线应用程序是可接受的，但可能不足以供可能无法依赖租户管理员审批的第三方开发人员使用。

代表组织以租户管理员 (的一种) 方式是访问：

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a>使用身份验证 API 请求其他同意

获取其他 Microsoft Graph 作用域的另一个方法是使用我们现有的基于 Web 的 [Azure AD](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) 身份验证方法呈现同意对话框，该方法涉及弹出 Azure AD 同意对话框。 有一些值得注意的新增功能：

1. 使用检索到的令牌需要使用 Azure AD 代表流在服务器端进行交换，才能访问这些额外的 `getAuthToken()` Microsoft Graph API。 [](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)
    * 请务必将 v2 Microsoft Graph 终结点用于此交换
2. 如果交换失败，Azure AD 将返回无效的授予例外。 通常有两条错误消息之一： `invalid_grant` 或 `interaction_required`
3. 当交换失败时，需要请求其他同意。 我们建议显示一些要求用户授予其他同意的 UI。 此 UI 应包括使用 Azure AD 身份验证 API 触发 [Azure AD 同意对话框的按钮](~/concepts/authentication/auth-silent-aad.md)。
4. 当请求 Azure AD 的其他同意时，你需要将查询 `prompt=consent` [字符串参数](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) 包括在 Azure AD 中，否则 Azure AD 不会请求其他作用域。
    * 而不是： `?scope={scopes}`
    * 使用以下方法： `?prompt=consent&scope={scopes}`
    * 请确保包括提示用户输入内容的所有作用域，例如 (`{scopes}` Mail.Read 或 User.Read) 。
5. 在用户授予其他权限后，重试代表流获取这些附加 API 的访问权限。

### <a name="non-azure-ad-authentication"></a>非 Azure AD 身份验证

上述身份验证解决方案仅适用于支持 Azure AD 作为标识提供程序的应用和服务。 想要使用基于非 Azure AD 的服务进行身份验证的应用需要继续使用基于弹出窗口的 [Web 身份验证流](~/concepts/authentication.md)。

> [!NOTE] 
> Azure AD B2C 租户内的客户拥有的应用支持 SSO。
