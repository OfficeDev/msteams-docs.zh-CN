---
title: 为选项卡提供单一登录支持
description: 描述单一登录 (SSO)
ms.topic: how-to
ms.localizationpriority: high
keywords: Teams 身份验证 SSO Microsoft Azure Active Directory (Azure AD) 单一登录 API
ms.openlocfilehash: d9391489c8bafafa24ba52528f5d0b8440319a55
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104418"
---
# <a name="single-sign-on-sso-support-for-tabs"></a>对选项卡的单一登录 (SSO) 支持

用户通过其工作、学校或 Microsoft 帐户（即 Office 365、Outlook）登录到 Microsoft Teams，你可以通过允许单一登录在桌面或移动客户端上授权 Teams 选项卡或任务模块来使用此功能。 如果用户登录过一次，则不必在另一台设备上重新登录，因为他们会自动登录。 此外，你的访问令牌会被预取以提高性能和加载时间。

> [!NOTE]
> **支持 SSO 的 Teams 移动客户端版本**  
>
> ✔适用于 Android 的 Teams（1416/1.0.0.2020073101 及更高版本）
>
> ✔适用于 iOS 团队（_版本_: 2.0.18 及更高版本）  
>
> ✔Teams JavaScript SDK（_版本_: 1.11 及更高版本）使 SSO 在会议侧面板中得以使用。
>
> 为获得 Teams 的最佳体验，请使用最新版本的 iOS 和 Android。[!NOTE]
> **快速入门**  
>
> 选项卡 SSO 入门的最简单路径是使用用于 Microsoft Visual Studio Code 的 Teams 工具包。 有关详细信息，请参阅 [SSO 配合 Teams 工具包和适用于选项卡的 Visual Studio Code](../../../toolkit/visual-studio-code-tab-sso.md)

<!--- TBD: Edit this article.
* Admonitions/alerts seem to be overused.
* Don't add note for a list of items.
* Don't add numbers to headings.
* Don't copy-paste superscript characters as is. Use HTML entities. See https://sitefarm.ucdavis.edu/training/all/using-wysiwyg/special-characters for the values.
* Same for the check marks added in the content in the note above. The content should not be in a note anyway.
--->

## <a name="how-sso-works-at-runtime"></a>运行时 SSO 的工作方式

下图显示了 SSO 流程的工作方式：

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. 在选项卡中，对 `getAuthToken()` 进行 JavaScript 调用。 `getAuthToken()` 让 Teams 获取选项卡应用程序的访问令牌。
2. 如果当前用户是第一次使用选项卡应用程序，则在需要同意时会提示你同意。 或者，有一个请求提示来处理升级身份验证，例如双因素身份验证。
3. Teams 从当前用户的 Azure AD 终结点请求选项卡访问令牌。
4. Azure AD 将选项卡访问令牌发送到 Teams 应用程序。
5. Teams 将选项卡访问令牌作为 `getAuthToken()` 调用返回的结果对象的一部分发送到选项卡。
6. 使用 JavaScript 在选项卡应用程序中分析令牌，以提取所需的信息，例如用户的电子邮件地址。

> [!NOTE]
> `getAuthToken()` 仅对一组有限的用户级 API（即电子邮件、配置文件、offline_access、OpenId）的许可有效。 它不用于其他 Graph 范围，如 `User.Read` 或 `Mail.Read`。 有关建议的解决方法，请参阅[使用 Graph 权限获取访问令牌](#get-an-access-token-with-graph-permissions)。

SSO API 还适用于嵌入 Web 内容的[任务模块](../../../task-modules-and-cards/what-are-task-modules.md)。

## <a name="develop-an-sso-microsoft-teams-tab"></a>开发 SSO Microsoft Teams 选项卡

本部分介绍创建使用 SSO 的 Teams 选项卡所涉及的任务。这些任务与语言和框架无关。

### <a name="1-create-your-azure-ad-application"></a>1. 创建 Azure AD 应用程序

> [!NOTE]
> 必须知道一些重要的限制：
>
> * 仅支持用户级图形 API 权限，即电子邮件、配置文件、offline_access、OpenId。 如果必须有权访问其他 Graph 范围，例如 `User.Read` 或 `Mail.Read`，请参阅[使用 Graph 权限获取访问令牌](#get-an-access-token-with-graph-permissions)。
> * 应用程序的域名与为 Azure AD 应用程序注册的域名相同，这一点很重要。
> * 目前不支持每个应用有多个域。
> * 对于新应用程序，用户必须将 `accessTokenAcceptedVersion` 设置为 `2`。

若要通过 Azure AD 门户注册应用，请执行以下步骤：

1. 在 [Azure AD 应用注册](https://go.microsoft.com/fwlink/?linkid=2083908)门户中注册新应用程序。
1. 选择“**新注册**”。 将显示 **注册应用程序** 页。
1. 在“**注册应用**”页面中，指定以下值：
    1. 输入应用的 **名称**。
    2. 选择 **支持的帐户类型**，选择单租户或多租户帐户类型。¹
    * 保留“重定向 URI”为空。
    3. 选择“注册”。
1. 在概述页上，复制并保存 **应用程序（客户端）ID**。 之后在更新 Teams 应用程序清单时，必须知道它。
1. 在“**管理**”下，选择“**公开 API**”。

    > [!NOTE]
    >
    > * 如果要使用机器人和选项卡生成应用，请输入应用程序 ID URI 作为 `api://fully-qualified-domain-name.com/botid-{YourBotId}`。
    >
    > * 域名请使用小写字母，不要使用大写字母。 例如，若要创建应用服务或 Web 应用，请输入基本资源名称作为 `demoapplication`，然后 URL 将为 `https://demoapplication.azurewebsites.net`。 但是，如果使用基本资源名称作为 `DemoApplication`，则 URL 将为 `https://DemoApplication.azurewebsites.net`，这支持桌面、Web 和 iOS，但在 android 中不受支持。

1. 选择“**设置**”链接以生成应用 ID URI，格式为 `api://{AppID}`。 插入具有正斜杠的完全限定的域名 "/" 追加到末尾，介于双正斜杠和 GUID 之间。 整个 ID 的格式必须为 `api://fully-qualified-domain-name.com/{AppID}`。 ² 例如 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`。 完全限定的域名是在其中提供应用的人类可读域名。 如果使用的是隧道服务（如 ngrok），则必须在 ngrok 子域发生更改时更新此值。
1. 选择“**添加作用域**”。在打开的面板中，输入 **access_as_user** 作为“**作用域名称**”。
1. 在 **谁可以同意？** 框中，输入 **管理员和用户**。
1. 在框中输入详细信息，以便使用适用于 `access_as_user` 作用域的值来配置管理员和用户同意提示：
    * **管理员同意标题:** Teams 可以访问用户的配置文件。
    * **管理员同意说明**：Teams 可以作为当前用户调用应用程序的 web API。
    * **用户同意标题**：Teams 可以访问你的个人资料并代表你发出请求。
    * **用户同意说明**：Teams 可以使用与用户相同的权限调用此应用的 API。
1. 确保将“状态”设置为“已启用”。
1. 选择“**添加作用域**”以保存详细信息。显示在文本字段正下方的“**作用域名称**”的域部分应自动与上一步骤中设置的“**应用 ID URI**”匹配，并将 `/access_as_user` 附加到末尾 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`。
1. 在“**授权客户端应用程序**”部分中，确定要授权给应用的 Web 应用程序的应用程序。 选择 **添加客户端应用程序**。 输入以下每个客户端 ID，然后选择在上一步中创建的授权范围：
    * 对于 Teams 移动或桌面应用程序，`1fec8e78-bce4-4aaf-ab1b-5451cc387264`。
    * 对于 Teams Web 应用程序，`5e3ce6c0-2b1f-4285-8d4b-75ee78787346`。
1. 导航到 **API 权限**。 选择 **添加权限** > **Microsoft Graph** > **委派权限**，然后从图形 API 添加以下权限：
    * 默认情况下已启用 User.Read
    * 电子邮件
    * offline_access
    * OpenId
    * 个人资料

1. 导航到 **身份验证**。

    > [!IMPORTANT]
    > 如果尚未向应用授予 IT 管理员同意，则用户必须在首次使用应用时提供同意。

    若要输入重定向 URI：
    * 选择 **添加平台**。
    * 选择“**Web**”。
    * 输入应用的 **重定向 URI**。 此 URI 与在步骤 5 中输入的完全限定的域名相同。 它后跟发送身份验证响应的 API 路由。 如果正在关注任何 Teams 示例，则 URI 为 `https://subdomain.example.com/auth-end`。 有关详细信息，请参阅 [OAuth 2.0 授权代码流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

    > [!NOTE]
    > 选项卡 SSO 不需要隐式授权。

恭喜！你已完成应用注册先决条件，可以继续使用 Tab SSO 应用。

> [!NOTE]
>
> * ¹如果 Azure AD 应用在你在 Teams 中发出身份验证请求的同一租户中注册，则无法要求用户同意，并且会立即获得访问令牌。 仅当 Azure AD 应用在其他租户中注册时，用户才同意这些权限。
> * ²如果未将自定义域添加到 Azure AD，则会收到一个错误，指出主机名不能基于已拥有的域。 若要将自定义域添加到 Azure AD 并注册它，请按照[将自定义域名添加到 Azure AD](/azure/active-directory/fundamentals/add-custom-domain) 的过程，然后重复步骤 5。 如果未在 Office 365 租赁中使用管理员凭据登录，也可能会收到此错误。
> * 如果未在返回的访问令牌中收到用户主体名称 (UPN)，则可以在 Azure AD 中将其添加为[可选声明](/azure/active-directory/develop/active-directory-optional-claims)。

### <a name="2-update-your-teams-application-manifest"></a>2. 更新 Teams 应用程序清单

使用以下代码将新属性添加到 Teams 清单：

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

* **WebApplicationInfo** 是下列元素的父元素：

> [!div class="checklist"]
>
> * **id** - 应用程序的客户端 ID。 它是在向 Azure AD 注册应用程序时获取的应用程序 ID。
>* **resource** - 应用程序的域和子域。 这是在步骤 6 中创建 `scope` 时注册的相同 URI（包括 `api://` 协议）。 不得在资源中包含 `access_as_user` 路径。 此 URI 的域部分必须与 Teams 应用程序清单的 URL 中使用的域（包括任何子域）匹配。
> [!NOTE]
>
>* Azure AD 应用的资源通常是其站点 URL 和 appID 的根（例如 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`）。 此值还用于确保请求来自同一域。 确保选项卡上的 `contentURL` 使用与资源属性相同的域。
>* 必须使用清单版本 1.5 或更高版本来实现 `webApplicationInfo` 字段。

### <a name="3-get-an-access-token-from-your-client-side-code"></a>3. 从客户端代码获取访问令牌

> [!NOTE]
> 若要避免 `Teams SDK Error: resourceDisabled` 等错误，请确保在 Azure AD 应用注册和 Teams 应用中正确配置应用程序 ID URI。

使用以下身份验证 API：

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

调用 `getAuthToken` 并且用户级权限需要用户同意时，会向用户显示一个对话框以授予同意。

在成功回调中收到访问令牌后，解码访问令牌以查看该令牌的声明。 （可选）手动将访问令牌复制并粘贴到工具中，例如 [jwt.ms](https://jwt.ms/)。 如果未在返回的访问令牌中收到 UPN，请将其添加为 Azure AD 中的[可选声明](/azure/active-directory/develop/active-directory-optional-claims)。 有关详细信息，请参阅[访问令牌](/azure/active-directory/develop/access-tokens)。

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-snippets"></a>代码段

以下代码提供了使用 MSAL 库提取访问令牌的代理流示例：

### <a name="c"></a>[C#](#tab/dotnet)

```csharp

IConfidentialClientApplication app = ConfidentialClientApplicationBuilder.Create(<"Client id">)
                                                .WithClientSecret(<"Client secret">)
                                                .WithAuthority($"https://login.microsoftonline.com/<"Tenant id">")
                                                .Build();
 
            try
            {
                var idToken = <"Client side token">;
                UserAssertion assert = new UserAssertion(idToken);
                List<string> scopes = new List<string>();
                scopes.Add("https://graph.microsoft.com/User.Read");
                var responseToken = await app.AcquireTokenOnBehalfOf(scopes, assert).ExecuteAsync();
                return responseToken.AccessToken.ToString();
            }
            catch (Exception ex)
            {
                return ex.Message;
            }
        }
```

### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```javascript

// Exchange cliend side token with server token
  app.post('/getProfileOnBehalfOf', function(req, res) {
        var tid = < "Tenand id" >
    var token = < "Client side token" >
    var scopes = ["https://graph.microsoft.com/User.Read"];

        // Creating MSAL client
        const msalClient = new msal.ConfidentialClientApplication({
            auth: {
                clientId: < "Client ID" >,
                clientSecret: < "Client Secret" >
      }
        });

        var oboPromise = new Promise((resolve, reject) => {
            msalClient.acquireTokenOnBehalfOf({
                authority: `https://login.microsoftonline.com/${tid}`,
                oboAssertion: token,
                scopes: scopes,
                skipCache: true
            }).then(result => {
                console.log("Token is: " + result.accessToken);
            }).catch(error => {
                reject({ "error": error.errorCode });
            });
        });
```

---

## <a name="code-sample"></a>代码示例

|**示例名称**|**说明**|**C#**|**Node.js**|
|---------------|---------------|------|--------------|
| 选项卡 SSO |适用于选项卡 Azure AD SSO 的 Microsoft Teams 示例应用| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs)， </br>[Teams 工具包](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a>已知限制

### <a name="get-an-access-token-with-graph-permissions"></a>获取具有 Graph 权限的访问令牌

我们当前的 SSO 实现仅授予用户级权限的许可，这些权限不可用于进行 Graph 调用。 若要获取进行 Graph 调用所需的权限（范围），SSO 解决方案必须实现自定义 Web 服务，以交换从 Teams JavaScript SDK 收到的令牌，以获取包含所需作用域的令牌。 这是使用 Azure AD [on-behalf-of flow](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow) 实现的。

### <a name="tenant-admin-consent"></a>租户管理员同意

以租户管理员身份代表组织同意的一种简单方法是引用 `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`。

#### <a name="ask-for-consent-using-the-auth-api"></a>使用身份验证 API 请求同意

获取 Graph 范围的另一种方法是使用现有的[基于 web 的 Azure AD 身份验证方法](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-pop-up-page)呈现同意对话框。 此方法涉及弹出 Azure AD 同意对话框。

若要使用身份验证 API 请求其他同意，请执行以下步骤：

1. 使用 `getAuthToken()` 取回的令牌必须通过 Azure AD [on-behalf-of flow](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) 在服务器端交换，以获取对其他图形 API 的访问权限。 请确保为此交换使用 v2 Graph 终结点。
2. 如果交换失败，Azure AD 将返回无效的授权异常。 通常有两条错误消息之一，`invalid_grant` 或 `interaction_required`。
3. 交换失败时，必须请求同意。 显示要求用户授予其他同意的一些用户界面 (UI)。 此 UI 必须包含一个按钮，该按钮使用我们的 [Azure AD 身份验证 API](~/concepts/authentication/auth-silent-aad.md) 触发 Azure AD 同意对话框。
4. 请求 Azure AD 的更多同意时，必须在给 Azure AD 发送的 [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) 中包含 `prompt=consent`，否则 Azure AD 不会要求其他范围。
    * 而不用 `?scope={scopes}`
    * 使用此 `?prompt=consent&scope={scopes}`
    * 确保 `{scopes}` 包括你提示用户的所有范围，例如 Mail.Read 或 User.Read。
5. 用户授予更多权限后，请重试 on-behalf-of-flow 以获取对这些其他 API 的访问权限。

### <a name="non-azure-ad-authentication"></a>非 Azure AD 身份验证

上述身份验证解决方案仅适用于支持 Azure AD 作为标识提供者的应用和服务。 想要使用基于非 Azure AD 的服务进行身份验证的应用必须继续使用基于弹出窗口的 [web 身份验证流](~/concepts/authentication.md)。

> [!NOTE]
> Azure AD B2C 租户中的客户拥有的应用支持 SSO。

## <a name="step-by-step-guides"></a>分步指南

* 按照[分步指南](../../../sbs-tabs-and-messaging-extensions-with-sso.yml)对选项卡和邮件扩展进行身份验证。
* 按照[分步指南](../../../sbs-tab-with-adaptive-cards.yml)创建具有自适应卡的选项卡。

## <a name="see-also"></a>另请参阅

[Teams Bot 与单一登录](../../../sbs-bots-with-sso.yml)
