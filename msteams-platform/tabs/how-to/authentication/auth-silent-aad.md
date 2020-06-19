---
title: 无提示的身份验证
description: 描述无提示身份验证
keywords: 团队身份验证 SSO 无提示 AAD
ms.openlocfilehash: b8a5b8cb9328635f5730ca089da29140d0a17ac4
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801011"
---
# <a name="silent-authentication"></a>无提示的身份验证

> [!NOTE]
> 若要对移动客户端上的选项卡进行身份验证，您需要确保您至少使用的是1.4.1 版本的团队 JavaScript SDK。

在 Azure Active Directory （Azure AD）中进行无提示身份验证，可通过无提示刷新身份验证令牌，最大限度地减少用户输入其登录凭据的次数。 （有关真正的单一登录支持，请查看我们的[SSO 文档](~/tabs/how-to/authentication/auth-aad-sso.md)）

如果要将代码完全保持在客户端，可以使用适用于 JavaScript 的[Azure Active Directory 身份验证库](/azure/active-directory/develop/active-directory-authentication-libraries)尝试以无提示方式获取 azure AD 访问令牌。 这意味着用户可能永远不会看到弹出对话框（如果他们最近已登录）。

尽管 ADAL.js 库针对 AngularJS 应用程序进行了优化，但它也适用于纯 JavaScript 单页应用程序。

> [!NOTE]
> 目前，无提示身份验证仅适用于选项卡。 它在从 bot 登录时仍不起作用。

## <a name="how-silent-authentication-works"></a>无提示身份验证的工作方式

ADAL.js 库为 OAuth 2.0 隐式授予流创建了一个隐藏的 iframe，但它指定了 `prompt=none` AZURE AD 从不显示登录页。 如果需要用户交互，因为用户需要登录或授予对应用程序的访问权限，则 Azure AD 将立即返回一个错误，ADAL.js 然后向您的应用程序报告。 此时，您的应用程序可以根据需要显示 "登录" 按钮。

## <a name="how-to-do-silent-authentication"></a>如何执行无提示身份验证

本文中的代码来自团队示例应用程序[Microsoft 团队身份验证示例（节点）](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)。

### <a name="include-and-configure-adal"></a>包含和配置 ADAL

在选项卡页中包含 ADAL.js 库，并使用客户端 ID 和重定向 URL 配置 ADAL：

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

在该选项卡的内容页中，调用 `microsoftTeams.getContext()` 获取当前用户的登录提示。 这将用作对 Azure AD 的调用中的 login_hint。

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

如果 ADAL 为用户缓存了未到期的令牌，请使用该令牌。 否则，尝试通过调用以无提示方式获取令牌 `acquireToken(resource, callback)` 。 ADAL.js 将使用请求的令牌调用回调函数，如果身份验证失败，则调用错误。

如果在回调函数中遇到错误，则显示 "登录" 按钮并回退到显式登录。

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

通过 `AuthenticationContext.handleWindowCallback(hash)` 在登录回调页中调用，让 ADAL.js 负责从 AZURE AD 中分析结果。

检查我们是否有有效的用户和呼叫， `microsoftTeams.authentication.notifySuccess()` 或 `microsoftTeams.authentication.notifyFailure()` 将状态报告回您的主选项卡内容页面。

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
