---
title: 用于为选项卡启用 SSO 的代码配置
description: 介绍为选项卡启用 SSO 的代码配置
ms.topic: how-to
ms.localizationpriority: high
keywords: Teams 身份验证选项卡 Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: 466da3cbd879ed2546adcad87f6f55620d54256d
ms.sourcegitcommit: 07f41abbeb1572a306a789485953c5588d65051e
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/06/2022
ms.locfileid: "66658934"
---
# <a name="add-code-to-enable-sso"></a>添加代码以启用 SSO

在添加代码以启用 SSO 之前，请确保已将应用注册到 Azure AD。

> [!div class="nextstepaction"]
> [注册Azure AD](tab-sso-register-aad.md)

需要配置选项卡应用的客户端代码，以从 Azure AD 获取访问令牌。 访问令牌是由选项卡应用颁发。 如果选项卡应用需要其他 Microsoft Graph 权限，则需要将访问令牌传递给服务器端，并将其交换为 Microsoft Graph 令牌。

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/sso-config-code.png" alt-text="配置用于处理访问令牌的代码":::

本节介绍：

- [添加客户端代码](#add-client-side-code)
- [将访问令牌传递到服务器端代码](#pass-the-access-token-to-server-side-code)
- [验证访问令牌](#validate-the-access-token)

## <a name="add-client-side-code"></a>添加客户端代码

若要获取当前应用用户的应用访问权限，客户端代码必须调用 Teams 以获取访问令牌。 需要更新客户端代码，以便使用 `getAuthToken()` 启动验证过程。

<br>
<details>
<summary>详细了解 getAuthToken（）</summary>
<br>
`getAuthToken()` 是 Microsoft Teams JavaScript SDK 中的一种方法。 它请求代表应用颁发 Azure AD 访问令牌。 如果令牌尚未过期，则可以从缓存中获取该令牌。 否则，将向 Azure AD 发送请求以获取新令牌。

 有关详细信息，请参阅 [getAuthToken](/javascript/api/@microsoft/teams-js/microsoftteams.authentication?view=msteams-client-js-latest#@microsoft-teams-js-microsoftteams-authentication-getauthtoken&preserve-view=true)。
</details>

### <a name="when-to-call-getauthtoken"></a>何时调用 getAccessToken

在需要当前应用用户的访问令牌时使用 `getAuthToken()` ：

| 如果需要访问令牌... | 调用 getAuthToken () ... |
| --- | --- |
| 当应用用户访问应用时 | 从内部 `microsoftTeams.initialize()`。 |
| 使用应用的特定功能 | 当应用用户执行需要登录的操作时。 |

### <a name="add-code-for-getauthtoken"></a>添加 getAuthToken 的代码

将 JavaScript 代码片段添加到选项卡应用，以执行以下操作：

- 调用 `getAuthToken()`。
- 分析访问令牌或将其传递给服务器端代码。

下面的代码段演示了调用 `getAuthToken()` 的示例。

```javascript
microsoftTeams.initialize();
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Error getting token: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

因此，可以将 `getAuthToken()` 调用添加到所有在需要令牌时启动操作的函数和处理程序。

<br>
<details>
<summary>下面是客户端代码的示例：</summary>

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/config-client-code.png" alt-text="配置客户端代码" lightbox="../../../assets/images/authentication/teams-sso-tabs/config-client-code.png":::

</details>

当 Teams 收到访问令牌时，会根据需要对其进行缓存和重复使用。 每当调用 `getAuthToken()` ，直到它过期时，都可以使用此令牌，而无需再次调用Azure AD。

> [!IMPORTANT]
> 作为访问令牌安全性的最佳做法：
>
> - 需要访问令牌时，始终调用 `getAuthToken()`。
> - Teams 将为你缓存访问令牌。 请勿缓存或将其存储在应用的代码中。

### <a name="consent-dialog-for-getting-access-token"></a>获取访问令牌的许可对话框

当你调用 `getAuthToken()` 并且需要应用用户同意才能获得用户级权限时，会向当前登录的应用用户显示一个 Azure AD 对话框。

:::image type="content" source="../../../assets/images/authentication/teams-sso-tabs/tabs-sso-prompt.png" alt-text="选项卡单一登录对话提示":::

显示的同意对话框适用于Azure AD中定义的 open-id 范围。 应用用户必须只提供一次同意。 同意后，应用用户可以访问和使用选项卡应用来获取授予的权限和范围。

> [!IMPORTANT]
> 不需要同意对话的方案：
>
> - 如果租户管理员已代表租户授予同意，则无需提示应用用户同意。 这意味着应用用户看不到同意对话框，并且可以无缝访问应用。
> - 如果 Azure AD 应用在 Teams 中发出身份验证请求的同一租户中注册，则无法要求应用用户同意，并且会立即获得访问令牌。 仅当 Azure AD 应用在其他租户中注册时，应用用户才同意这些权限。

如果遇到任何错误，请参阅 [Teams 中的 SSO 身份验证疑难解答](tab-sso-troubleshooting.md)。

### <a name="use-the-access-token-as-an-identity-token"></a>使用访问令牌作为身份令牌

返回到选项卡应用的令牌既是访问令牌，也是 ID 令牌。 或者，选项卡应用可以使用令牌作为访问令牌，以向服务器端上的 API 发出经过身份验证的 HTTPS 请求。

从 `getAuthToken()` 中返回的访问令牌可用于使用令牌中的以下声明来建立应用用户的标识：

- `name`：应用用户的显示名称。
- `preferred_username`：应用用户的电子邮件地址。
- `oid`：表示应用用户 ID 的 GUID。
- `tid`：表示应用用户登录到的租户的 GUID。

Teams 可以缓存与应用用户标识相关联的信息，例如用户的首选项。

> [!NOTE]
> 如果需要构建唯一 ID 来表示系统中的应用用户，请参阅“[使用声明可靠地识别用户](/azure/active-directory/develop/id-tokens#using-claims-to-reliably-identify-a-user-subject-and-object-id)”以获取详细信息。

## <a name="pass-the-access-token-to-server-side-code"></a>将访问令牌传递到服务器端代码

如果需要访问服务器上的 Web API，则需要将访问令牌传递给服务器端代码。 Web API 必须解码访问令牌才能查看该令牌的声明。

> [!NOTE]
> 如果未在返回的访问令牌中收到 UPN，请将其添加为 Azure AD 中的[可选声明](/azure/active-directory/develop/active-directory-optional-claims)。
> 有关详细信息，请参阅[访问令牌](/azure/active-directory/develop/access-tokens)。

成功回调 `getAuthToken()` 中的访问令牌（为经过身份验证的用户）提供对 Web API 的访问权限。 如果需要，服务器端代码也可以分析令牌以获取[身份信息](#use-the-access-token-as-an-identity-token)。

如果需要传递访问令牌来获取 Microsoft Graph 数据，请参阅 [具有 Microsoft Graph 权限的扩展选项卡应用](tab-sso-graph-api.md)。

### <a name="code-for-passing-access-token-to-server-side"></a>用于将访问令牌传递到服务器端的代码

以下代码显示了将访问令牌传递到服务器端的示例。 向服务器端 Web API 发送请求时，令牌在 `Authorization` 标头中传递。 此示例发送 JSON 数据，因此它使用该 `POST` 方法。 如果未写入服务器，则 `GET` 足以发送访问令牌。

```javascript
$.ajax({
    type: "POST",
    url: "/api/DoSomething",
    headers: {
        "Authorization": "Bearer " + accessToken
    },
    data: { /* some JSON payload */ },
    contentType: "application/json; charset=utf-8"
}).done(function (data) {
    // Handle success
}).fail(function (error) {
    // Handle error
}).always(function () {
    // Cleanup
});
```

### <a name="validate-the-access-token"></a>验证访问令牌

服务器上的 Web API 必须解码访问令牌，并验证它是否已从客户端发送。 该令牌是 JSON Web 令牌 (JWT)，这意味着验证方式与大多数标准 OAuth 流中的令牌验证方式类似。 Web API 必须解码访问令牌。 （可选）手动将访问令牌复制并粘贴到工具中，例如 jwt.ms。

有许多库可用于处理 JWT 验证。 基本验证包括：

- 检查令牌的格式是否正确
- 检查令牌是否由预期的颁发机构颁发
- 检查令牌是否是针对 Web API

验证令牌时，请牢记以下准则：

- 有效的 SSO 令牌由 Azure AD 颁发。 令牌中的 `iss` 声明应以此值开头。
- 令牌的 `aud1` 参数将设置为 Azure AD 应用注册期间生成的应用 ID。
- 令牌的 `scp` 参数将被设置为 `access_as_user`。

#### <a name="example-access-token"></a>示例访问令牌

以下是访问令牌的典型解码有效负载。

```javascript
{
    aud: "2c3caa80-93f9-425e-8b85-0745f50c0d24",
    iss: "https://login.microsoftonline.com/fec4f964-8bc9-4fac-b972-1c1da35adbcd/v2.0",
    iat: 1521143967,
    nbf: 1521143967,
    exp: 1521147867,
    aio: "ATQAy/8GAAAA0agfnU4DTJUlEqGLisMtBk5q6z+6DB+sgiRjB/Ni73q83y0B86yBHU/WFJnlMQJ8",
    azp: "e4590ed6-62b3-5102-beff-bad2292ab01c",
    azpacr: "0",
    e_exp: 262800,
    name: "Mila Nikolova",
    oid: "6467882c-fdfd-4354-a1ed-4e13f064be25",
    preferred_username: "milan@contoso.com",
    scp: "access_as_user",
    sub: "XkjgWjdmaZ-_xDmhgN1BMP2vL2YOfeVxfPT_o8GRWaw",
    tid: "fec4f964-8bc9-4fac-b972-1c1da35adbcd",
    uti: "MICAQyhrH02ov54bCtIDAA",
    ver: "2.0"
}
```

## <a name="code-samples"></a>代码示例

| 示例名称 | Description | C#/.NET| Node.js |
|---------------|---------------|------|--------------|
| 选项卡 SSO |适用于选项卡 Azure AD SSO 的 Microsoft Teams 示例应用| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs)， </br>[Teams 工具包](../../../toolkit/visual-studio-code-tab-sso.md)|
| 选项卡、机器人和消息扩展 (ME) SSO | 此示例演示用于选项卡、机器人和 ME 的 SSO - 搜索、操作、linkunfurl。 |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [更新 Teams 应用清单并预览应用](tab-sso-manifest.md)

## <a name="see-also"></a>另请参阅

- [jwt.ms](https://jwt.ms/)
- [Active Directory 可选声明](/azure/active-directory/develop/active-directory-optional-claims)
- [访问令牌](/azure/active-directory/develop/access-tokens)
- [Microsoft 身份验证库 (MSAL) 概述](/azure/active-directory/develop/msal-overview)
- [Microsoft 标识平台访问令牌](/azure/active-directory/develop/id-tokens)
- [Microsoft 标识平台访问令牌](/azure/active-directory/develop/access-tokens#validating-tokens)
