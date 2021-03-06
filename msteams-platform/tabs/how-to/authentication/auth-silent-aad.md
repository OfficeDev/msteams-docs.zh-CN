---
title: 无提示的身份验证
description: 描述无提示身份验证
ms.topic: conceptual
localization_priority: Normal
keywords: teams 身份验证 SSO 无提示 AAD
ms.openlocfilehash: 0c75c6d50fd1191b6ea8548d65c9df4ce8453898
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019599"
---
# <a name="silent-authentication"></a>无提示的身份验证

> [!NOTE]
> 若要在移动客户端上对选项卡进行身份验证，请确保使用的是至少 1.4.1 版本的 Teams JavaScript SDK。

AAD Azure Active Directory (中的无提示身份验证) 静默刷新身份验证令牌，从而最大程度地减少用户输入登录凭据次数。 有关真正的单一登录支持，请参阅 [SSO 文档](~/tabs/how-to/authentication/auth-aad-sso.md)。

如果希望代码完全在客户端运行，可以使用适用于 JavaScript 的 [AAD](/azure/active-directory/develop/active-directory-authentication-libraries) 身份验证库以静默方式获取 AAD 访问令牌。 如果用户最近登录过，他们绝不会看到弹出对话框。

尽管 ADAL.js库已针对 AngularJS 应用程序进行了优化，但它也适用于纯 JavaScript 单页应用程序。

> [!NOTE]
> 目前，无提示身份验证仅适用于选项卡。 从自动程序登录时，它不起作用。

## <a name="how-silent-authentication-works"></a>无提示身份验证的工作原理

该ADAL.js库为 OAuth 2.0 隐式授权流创建隐藏的 iframe。 但库指定 `prompt=none` ，因此 Azure AD 永远不会显示登录页面。 如果由于用户需要登录或授予对应用程序的访问权限而需要用户交互，AAD 会立即返回一个错误，ADAL.js报告给应用。 此时，你的应用可以显示登录按钮（如果需要）。

## <a name="how-to-do-silent-authentication"></a>如何执行无提示身份验证

本文中的代码来自Teams身份验证示例节点的 Teams[示例应用](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)。

[使用 AAD 启动](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) 无提示且简单的身份验证可配置选项卡，并按照说明在本地计算机上运行示例。

### <a name="include-and-configure-adal"></a>包括和配置 ADAL

将 ADAL.js 库包括在选项卡页中，然后使用客户端 ID 和重定向 URL 配置 ADAL：

```html
<script src="https://secure.aadcdn.microsoftonline-p.com/lib/1.0.15/js/adal.min.js" integrity="sha384-lIk8T3uMxKqXQVVfFbiw0K/Nq+kt1P3NtGt/pNexiDby2rKU6xnDY8p16gIwKqgI" crossorigin="anonymous"></script>
<script type="text/javascript">
    // ADAL.js configuration
    let config = {
        clientId: "YOUR_APP_ID_HERE",
        // redirectUri must be in the list of redirect URLs for the Azure AD app
        redirectUri: window.location.origin + "/tab-auth/silent-end",
        cacheLocation: "localStorage",
        navigateToLoginRequestUrl: false,
    };
</script>
```

### <a name="get-the-user-context"></a>获取用户上下文

在选项卡的内容页中，调用 `microsoftTeams.getContext()` 获取当前用户的登录提示。 在调用 AAD 时，这用作 loginHint。

```javascript
// Set up extra query parameters for ADAL
// - openid and profile scope adds profile information to the id_token
// - login_hint provides the expected user name
if (loginHint) {
    config.extraQueryParameter = "scope=openid+profile&login_hint=" + encodeURIComponent(loginHint);
} else {
    config.extraQueryParameter = "scope=openid+profile";
}
```

### <a name="authenticate"></a>身份验证

如果 ADAL 为尚未过期的用户缓存了一个令牌，请使用该令牌。 或者，尝试通过调用 以静默方式获取令牌 `acquireToken(resource, callback)` 。 ADAL.js请求的令牌调用回调函数，或在身份验证失败时提供错误。

如果您在回调函数中收到错误，则显示登录按钮并回退到显式登录。

```javascript
let authContext = new AuthenticationContext(config); // from the ADAL.js library
// See if there's a cached user and it matches the expected user
let user = authContext.getCachedUser();
if (user) {
    if (user.profile.oid !== userObjectId) {
        // User doesn't match, clear the cache
        authContext.clearCache();
    }
}

// In this example we are getting an id token (which ADAL.js returns if we ask for resource = clientId)
authContext.acquireToken(config.clientId, function (errDesc, token, err, tokenType) {
    if (token) {
        // Make sure ADAL gave us an id token
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

ADAL.js登录回调页中调用来分析 AAD `AuthenticationContext.handleWindowCallback(hash)` 的结果。

检查用户是否有效，并调用 `microsoftTeams.authentication.notifySuccess()` 或 `microsoftTeams.authentication.notifyFailure()` 将状态报告给主选项卡内容页。

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

### <a name="handle-sign-out-flow"></a>处理注销流

使用以下代码处理 AAD 身份验证中的注销流：

> [!NOTE]
> 当用户Teams或自动程序注销时，当前会话也将清除。

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```
