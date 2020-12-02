---
title: 对选项卡的单一登录支持
description: 描述 (SSO) 的单一登录
keywords: 团队身份验证 SSO AAD 单一登录 api
ms.openlocfilehash: 08ad1ab55a06ccb887755322fbd572f745952d8e
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552449"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>单一登录 (SSO) 支持选项卡

用户通过其工作、学校或 Microsoft 帐户登录 Microsoft 团队 (Office 365、Outlook 等) 。 通过允许单一登录对桌面或移动客户端上的 Microsoft "团队" 选项卡 (或任务模块) 进行授权，可以利用这一点。 因此，如果用户同意使用您的应用程序，则无需再次在其他设备上同意，它们将自动登录。 此外，我们还会预提取访问令牌，以提高性能和加载时间。

>[!NOTE]
> **团队移动客户端版本支持 SSO**  
>
> 适用于 Android 的✔团队 (1416/1.0.0.2020073101 及更高版本) 
>
> 适用于 iOS 的✔团队 (版本：2.0.18 和更高 _版本_)   
>
> 若要获取团队的最佳体验，请使用最新版本的 iOS 和 Android。

>[!NOTE]
> **快速入门**  
>
> 开始使用 tab SSO 的最简单途径是使用 Microsoft 团队工具包获取 Visual Studio Code。 [了解更多](../../../toolkit/visual-studio-code-tab-sso.md)


## <a name="how-sso-works-at-runtime"></a>运行时 SSO 的工作方式

下图显示 SSO 进程的工作原理：

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. 在 "" 选项卡中，对进行了 JavaScript 调用 `getAuthToken()` 。 这将告知团队获取选项卡应用程序的身份验证令牌。
2. 如果这是当前用户第一次使用您的选项卡应用程序，则在需要同意时，将会发出请求提示 () 或处理步骤验证 (如双重身份验证) ）。
3. 团队从当前用户的 Azure AD 终结点请求选项卡应用程序令牌。
4. Azure AD 将选项卡应用程序令牌发送给团队应用程序。
5. 团队将选项卡应用程序令牌作为调用返回的 result 对象的一部分发送到选项卡 `getAuthToken()` 。
6. 将通过 JavaScript 在选项卡应用程序中分析令牌，以提取所需的信息，如用户的电子邮件地址。

> [!NOTE]
> `getAuthToken()`仅适用于同意一组有限的用户级 api （电子邮件、配置文件、offline_access 和 OpenId），而不是对更多 Microsoft Graph 范围（例如或）有效 `User.Read` `Mail.Read` 。 如果你需要 [其他 Graph 作用域](#apps-that-require-additional-microsoft-graph-scopes)，请参阅本文档末尾的部分，了解建议的解决方法。

SSO API 也可在嵌入 web 内容的 [任务模块](../../../task-modules-and-cards/what-are-task-modules.md) 中运行。

## <a name="develop-an-sso-microsoft-teams-tab"></a>开发 SSO Microsoft 团队选项卡

本节介绍创建使用 SSO 的 "团队" 选项卡所涉及的任务。 此处介绍了这些任务是语言和框架不可知的。

### <a name="1-create-your-azure-active-directory-azure-ad-application"></a>1. 在 Azure AD) 应用程序中创建 Azure Active Directory (

#### <a name="registering-your-application-in-theazure-ad-portal-overview"></a>在[AZURE AD 门户](https://azure.microsoft.com/features/azure-portal/) 中注册应用程序概述：

1. 获取 [AZURE AD 应用程序 ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)。
2. 指定应用程序需要的 Azure AD 终结点和 Microsoft Graph （可选）的权限。
3. [授予](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) 对团队桌面、web 和移动应用程序的权限。
4. 预授权团队通过选择 " **添加范围** " 按钮，并在打开的面板中，输入 `access_as_user` 作为 **作用域名称**。

> [!NOTE]
> 您应注意一些重要限制：
>
> * 仅支持用户级别的 Microsoft Graph API 权限，即电子邮件、配置文件、offline_access、OpenId。 如果需要访问其他 Microsoft Graph 作用域 (例如 `User.Read` 或 `Mail.Read`) ，请参阅本文档末尾的 [建议解决方法](#apps-that-require-additional-microsoft-graph-scopes) 。
> * 您的应用程序的域名与您为 Azure AD 应用程序注册的域名称相同，这一点很重要。
> * 目前，我们不支持每个应用的多个域。
> * 我们不支持使用域的应用程序， `azurewebsites.net` 因为它太常见，可能存在安全风险。 但是，我们正在努力删除此限制。

#### <a name="registering-your-app-through-the-azure-active-directory-portal-in-depth"></a>通过 Azure Active Directory 门户注册你的应用程序深入：

1. 在 [Azure Active Directory –应用程序注册](https://go.microsoft.com/fwlink/?linkid=2083908) 门户中注册新的应用程序。
2. 选择 " **新建注册** "，并在 " *注册应用程序" 页* 上，设置以下值：
    * 将 **名称** 设置为您的应用程序名称。
    * 选择 **受支持的帐户类型** (任何帐户类型的工作) ¹
    * 保留“重定向 URI”为空。
    * 选择“注册”。
3. 在 "概述" 页上，将应用程序复制并保存 **(客户端) ID**。 稍后在更新团队应用程序清单时，将需要它。
4. 在“**管理**”下，选择“**公开 API**”。 
5. 选择 " **设置** " 链接，以以的形式生成应用程序 ID URI `api://{AppID}` 。 插入完全限定的域名 (，并追加一个正斜杠 "/"，并追加到双正斜杠和 GUID 之间的结束) 。 整个 ID 的形式应为： `api://fully-qualified-domain-name.com/{AppID}` ²
    * 例如： `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 。
    
    完全限定的域名是用户可读的域名，您的应用程序将从该域名提供服务。 如果您使用的是隧道服务（如 ngrok），则每当 ngrok 子域更改时，您都需要更新此值。 
6. 选择“添加一个作用域”按钮。 在打开的面板中，输入 `access_as_user` 作为“作用域名称”。
7. 设置 **谁可以同意？** 若要 `Admins and users`
8. 填写用于配置管理员和用户同意提示的字段，其中包含适用于该范围的值 `access_as_user` ：
    * **管理员同意职务：** 团队可以访问用户的配置文件。
    * **管理员同意说明**：允许团队以当前用户的身份调用应用程序的 web api。
    * **用户同意标题**：团队可以访问用户配置文件，并代表用户发出请求。
    * **用户同意说明：** 使团队可以使用与用户相同的权限调用此应用的 Api。
9. 确保将 "**状态**" 设置为 "**已启用**"
10. 选择 " **添加范围** " 按钮以保存 
    * 显示在文本字段正下方的 **范围名称** 的域部分应自动匹配上一步中设置的 **应用程序 ID** URI，并 `/access_as_user` 追加到末尾：
        * `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`
11. 在 " **授权客户端应用程序** " 部分中，确定要为您的应用程序的 web 应用程序授权的应用程序。 选择 " *添加客户端应用程序*"。 输入以下每个客户端 Id，然后选择您在上一步中创建的授权范围：
    * `1fec8e78-bce4-4aaf-ab1b-5451cc387264` (团队移动/桌面应用程序) 
    * `5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (团队 web 应用程序) 
12. 导航到 " **API 权限**"。 选择 "*添加权限*  >  " "*microsoft graph*  >  *委派权限*"，然后从 Microsoft graph API 添加以下权限：
    * 默认情况下， (启用 Read) 
    * email
    * offline_access
    * OpenId
    * 个人资料

13. 导航到 "**身份验证**"

    如果尚未向应用授予 IT 管理员同意，则用户在首次使用应用程序时必须提供许可。

    设置重定向 URI：
    * 选择 " **添加平台**"。
    * 选择 " **web**"。
    * 输入您的应用程序的 **重定向 URI** 。 这将是成功的隐式授予流将重定向到用户的页面。 这将是您在步骤5中输入的完全限定的域名，后跟应发送身份验证响应的 API 路由。 如果您正在关注任何团队示例，则将执行以下操作： `https://subdomain.example.com/auth-end`

    接下来，通过选中以下框来启用隐式授予：  
    ✔ ID 令牌  
    ✔访问令牌  
    
恭喜你！ 您已完成应用注册先决条件，以继续使用您的选项卡 SSO 应用。     

> [!NOTE]
>
> * ¹如果您的 Azure AD 应用注册到在团队中进行身份验证请求的 _同一个_ 租户中，则不会要求用户同意并将立即被授予访问令牌。 如果 Azure AD 应用在其他租户中注册，则用户只需同意这些权限。
> * ²如果你收到一条错误，指出域已拥有且你是所有者，请按照 [以下过程操作：将自定义域名添加到 Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) 以注册域，然后重复上面的步骤5。  (如果您未使用 Office 365 租赁) 中的管理员凭据登录，也会发生此错误。
> * 如果未在返回的访问令牌中接收 UPN (用户主体名称) ，则可以将其作为 Azure AD 中的 [可选声明](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) 进行添加。

### <a name="2-update-your-microsoft-teams-application-manifest"></a>2. 更新 Microsoft 团队应用程序清单

将新属性添加到 Microsoft 团队清单：

* **WebApplicationInfo** -以下元素的父元素：

> [!div class="checklist"]
> * **id** -应用程序的客户端 id。 这是您在向 Azure AD 注册应用程序的过程中获得的应用程序 ID。
>* **resource** -应用程序的域和子域。 此 URI (包括 `api://` 您在 `scope` 上面的步骤6中创建时注册的协议) 。 您不应 `access_as_user` 在资源中包含该路径。 此 URI 的域部分应与在团队应用程序清单的 Url 中使用的域（包括任何子域）相匹配。

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

> [!NOTE]
>
>* AAD 应用的资源通常是其网站 URL 和 appID (（例如) ）的根 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 。 我们还使用此值来确保你的请求来自同一个域。 因此，请确保 `contentURL` 选项卡使用与资源属性相同的域。
>* 您需要使用清单版本1.5 或更高版本来实现 `webApplicationInfo` 字段。

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a>3. 从客户端代码中获取身份验证令牌

身份验证 API 如下所示：

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

当您 `getAuthToken` 需要拨打和额外的用户同意时 (对用户级权限) -我们将向用户显示一个对话框，让他们鼓励他们授予额外的同意。 

收到成功回调中的访问令牌后，可以对访问令牌进行解码，以查看与该令牌关联的声明。  (可以选择将访问令牌手动复制/粘贴到工具（如 [JWT.io](https://jwt.io/) ），以检查其内容) 。 如果未在返回的访问令牌中接收 UPN (用户主体名称) ，则可以将其作为 Azure AD 中的 [可选声明](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) 进行添加。

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="sample-code"></a>示例代码

请访问我们的示例应用程序： [MSTeams 选项卡 SSO 示例-Nodejs](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs)

该自述文件介绍如何设置开发环境以及如何在 Azure AD 中配置应用程序。 您还可以进一步了解如何在 [应用程序结构部分](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs#app-structure) 中对示例进行构造，以帮助熟悉基本代码。

## <a name="known-limitations"></a>已知限制

### <a name="apps-that-require-additional-microsoft-graph-scopes"></a>需要其他 Microsoft Graph 作用域的应用程序

我们目前的 SSO 实施仅授予用户级权限（电子邮件、配置文件、offline_access、OpenId）的同意，而不是对其他 Api (（如 User. read) ）。 如果您的应用程序需要更多 Microsoft Graph 作用域，下面是一些启用解决方法：

#### <a name="tenant-admin-consent"></a>租户管理员同意

最简单的方法是让租户管理员代表组织进行预先同意。 这意味着用户无需同意这些作用域，您就可以使用 Azure AD 的 [代表流](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)来交换令牌服务器端。 这种解决方法对于内部业务线应用程序是可接受的，但对于可能无法依赖租户管理员批准的第三方开发人员来说可能不够。

同意代表组织 (作为租户管理员) 的简单方法是访问：

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a>使用 Auth API 请求其他许可

获取其他 Microsoft Graph 作用域的另一种方法是，使用现有的 [基于 web 的 AZURE ad 身份验证方法](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) 呈现许可对话，这涉及弹出 Azure ad 同意对话框。 有一些显著的添加：

1. `getAuthToken()`需要使用 AZURE AD[代表流](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)交换服务器端检索的令牌，以获取对这些额外 Microsoft Graph api 的访问权限。
    * 请务必将 v2 Microsoft Graph 终结点用于此 exchange
2. 如果 exchange 发生故障，Azure AD 将返回无效的授予异常。 通常有以下两种错误消息 `invalid_grant` 之一： `interaction_required`
3. 当 exchange 发生故障时，您需要请求其他许可。 建议显示一些 UI，要求用户授予更多许可。 此 UI 应包括使用我们的 [AZURE ad 身份验证 API](~/concepts/authentication/auth-silent-aad.md)触发 azure ad 许可对话的按钮。
4. 当询问 Azure AD 的其他许可时，您需要将 `prompt=consent` [查询字符串参数](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) 包括在 azure ad 中，否则 azure ad 将不会要求提供其他作用域。
    * 而不是： `?scope={scopes}`
    * 使用以下命令： `?prompt=consent&scope={scopes}`
    * 请确保 `{scopes}` 包含要提示用户的所有作用域 (例如： Mail. read) 。
5. 一旦用户授予了其他权限，则重试代表流，以获取对这些附加 Api 的访问权限。

### <a name="non-azure-ad-authentication"></a>非 Azure AD 身份验证

以上所述的身份验证解决方案仅适用于支持 Azure AD 作为标识提供程序的应用程序和服务。 要使用基于非 Azure AD 的服务进行身份验证的应用程序需要继续使用基于弹出窗口的 [web 身份验证流](~/concepts/authentication.md)。
