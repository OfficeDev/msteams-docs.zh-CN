---
title: 无提示的身份验证
description: 在本模块中，了解如何对选项卡执行无提示身份验证、单一登录和 Azure AD，以及它的工作原理
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: 7df394bf43bd004e0a430b011ad5aad9c23d6983
ms.sourcegitcommit: 1cda2fd3498a76c09e31ed7fd88175414ad428f7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/27/2022
ms.locfileid: "67035308"
---
# <a name="use-silent-authentication-in-azure-ad"></a>在 Azure AD 中使用无提示身份验证

> [!IMPORTANT]
> Microsoft 对 Active Directory 身份验证库 (ADAL) 的支持和开发，包括安全修补程序，将于 **2022 年 6 月 30日** 结束。 若要继续接收支持，请将应用程序更新为使用 Microsoft 身份验证库 (MSAL) 。请参阅 [将应用程序迁移到 Microsoft 身份验证库 (MSAL) ](/azure/active-directory/develop/msal-migration)。

> [!NOTE]
> 要使身份验证适用于移动客户端上的选项卡，请确保使用的是 Teams JavaScript SDK 版本 1.4.1 或更高版本。

Azure AD 中的无提示身份验证通过无提示刷新身份验证令牌，最大限度地减少了用户需要输入凭据的次数。 有关真正的单一登录支持，请参阅 [SSO 文档](~/tabs/how-to/authentication/tab-sso-overview.md)。

若要保留代码客户端，请使用适用于 JavaScript 的 [Azure AD 身份验证库](/azure/active-directory/develop/active-directory-authentication-libraries)以无提示方式获取 Microsoft Azure Active Directory (Azure AD) 访问令牌。 如果用户最近已登录，则看不到弹出对话框。

虽然 Active Directory 身份验证库针对 AngularJS 应用程序进行了优化，它也适用于 JavaScript 单页应用程序 (SPA)。

> [!NOTE]
> 目前，无提示身份验证仅适用于选项卡。 从机器人登录时，它不起作用。

## <a name="how-silent-authentication-works"></a>无提示身份验证的工作原理

Active Directory 身份验证库为 OAuth 2.0 隐式授权流程创建隐藏的 iframe。 但库会指定 `prompt=none`，因此 Azure AD 不会显示登录页面。 如果用户需要登录或授予对应用程序的访问权限，则可能需要用户交互。 如果需要用户交互，Azure AD 会返回一个错误，由库报告给应用程序。 如有必要，应用现在可以显示登录选项。

## <a name="how-to-do-silent-authentication"></a>如何执行无提示身份验证

本文中的代码来自 Teams 示例应用，即 [Teams 身份验证示例节点](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)。

[使用 Azure AD 启动无提示和简单身份验证可配置选项卡](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp)，并按照说明在本地计算机上运行示例。

### <a name="include-and-configure-active-directory-authentication-library"></a>添加和配置 Active Directory 身份验证库

在选项卡页中添加 Active Directory 身份验证库，并使用客户端 ID 和重定向 URL 配置库：

```html
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/1.0.15/js/adal.min.js" integrity="sha384-lIk8T3uMxKqXQVVfFbiw0K/Nq+kt1P3NtGt/pNexiDby2rKU6xnDY8p16gIwKqgI" crossorigin="anonymous"></script>
<script type="text/javascript">
    // Active Directory Authentication Library configuration
    let config = {
        clientId: "YOUR_APP_ID_HERE",
        // redirectUri must be in the list of redirect URLs for the Azure AD app
        redirectUri: window.location.origin + "/tab-auth/silent-end",
        cacheLocation: "localStorage",
        navigateToLoginRequestUrl: false,
    };
</script>
```

### <a name="get-the-user-context"></a>获取当前上下文的用户

在选项卡的内容页中，调用 `microsoftTeams.getContext()` 以获取当前用户的登录提示。 该提示在调用 Azure AD 时用作 `loginHint`。

```javascript
// Set up extra query parameters for Active Directory Authentication Library
// - openid and profile scope adds profile information to the id_token
// - login_hint provides the expected user name
if (loginHint) {
    config.extraQueryParameter = "scope=openid+profile&login_hint=" + encodeURIComponent(loginHint);
} else {
    config.extraQueryParameter = "scope=openid+profile";
}
```

### <a name="authenticate"></a>身份验证

如果 Active Directory 身份验证库为用户缓存了未过期的令牌，请使用该令牌。 或者，调用 `acquireToken(resource, callback)` 以无提示方式接收令牌。 库使用请求的令牌调用回调函数，或者在身份验证失败时生成错误。

如果回调函数中出现错误，请显示并使用显式登录选项。

```javascript
let authContext = new AuthenticationContext(config); // from Active Directory Authentication Library
// See if there is a cached user and it matches the expected user
let user = authContext.getCachedUser();
if (user) {
    if (user.profile.oid !== userObjectId) {
        // User doesn't match, clear the cache
        authContext.clearCache();
    }
}

// In this example we are getting an id token (which Active Directory Authentication Library returns if we ask for resource = clientId)
authContext.acquireToken(config.clientId, function (errDesc, token, err, tokenType) {
    if (token) {
        // Make sure Active Directory Authentication Library gave us an ID token
        if (tokenType !== authContext.CONSTANTS.ID_TOKEN) {
            token = authContext.getCachedToken(config.clientId);
        }
        showProfileInformation(idToken);
    } else {
        console.log("Renewal failed: " + err);
        // Failed to get the token silently; show the login button
        showLoginButton();
        // You could attempt to launch the login popup here, but in browsers this could be blocked by
        // a popup blocker, in which case the login attempt will fail with the reason FailedToOpenWindow.
    }
});
```

### <a name="process-the-return-value"></a>处理返回值

Active Directory 身份验证库通过在登录回调页中调用 `AuthenticationContext.handleWindowCallback(hash)` 来分析 Azure AD 的结果。

检查是否有有效的用户，并调用 `microsoftTeams.authentication.notifySuccess()` 或 `microsoftTeams.authentication.notifyFailure()` 向主选项卡内容页面报告状态。

```javascript
if (authContext.isCallback(window.location.hash)) {
    authContext.handleWindowCallback(window.location.hash);
    if (window.parent === window) {
        if (authContext.getCachedUser()) {
            microsoftTeams.authentication.notifySuccess();
        } else {
            microsoftTeams.authentication.notifyFailure(authContext.getLoginError());
        }
    }
}
```

### <a name="handle-the-sign-out-flow"></a>处理注销流程

使用以下代码处理 Azure AD 身份验证中的注销流程：

> [!NOTE]
> 从 Teams 选项卡或机器人注销时，将清除当前会话。

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```

## <a name="see-also"></a>另请参阅

* [配置标识提供程序使用 Azure AD](../../../concepts/authentication/configure-identity-provider.md)
* [了解 Microsoft 身份验证库 (MSAL)](/azure/active-directory/develop/msal-overview)
