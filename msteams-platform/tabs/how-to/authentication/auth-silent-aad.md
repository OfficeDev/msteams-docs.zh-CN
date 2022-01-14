---
title: 无提示的身份验证
description: 介绍选项卡的无提示身份验证、单一Azure Active Directory登录和登录
ms.topic: conceptual
ms.localizationpriority: medium
keywords: teams 身份验证 SSO 无提示Azure AD选项卡
ms.openlocfilehash: bf50f1840996371292b94ef6d3b2f16d5377a3f9
ms.sourcegitcommit: 25a33b31cc56c05169fc52c65d44c65c601aefef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2022
ms.locfileid: "62043215"
---
# <a name="silent-authentication"></a>无提示的身份验证

> [!IMPORTANT]
> Microsoft 对 Active Directory Authentication Library (ADAL) 的支持和开发（包括安全修补程序）将于 **2022 年 6 月 30 日结束**。 更新应用程序以使用 MICROSOFT 身份验证库 (MSAL) 继续获得支持。 请参阅 [将应用程序迁移到 MSAL ](/azure/active-directory/develop/msal-migration) (Microsoft 身份验证) 。

> [!NOTE]
> 若要在移动客户端上对选项卡进行身份验证，请确保Teams JavaScript SDK 版本 1.4.1 或更高版本。

自动Azure Active Directory中的无提示身份验证通过静默刷新身份验证令牌来最大程度地减少用户输入凭据次数。 有关真正的单一登录支持，请参阅 [SSO 文档](~/tabs/how-to/authentication/auth-aad-sso.md)。

若要使代码客户端保持运行，请使用 JavaScript Azure AD身份验证库以静默方式Azure AD访问令牌。 [](/azure/active-directory/develop/active-directory-authentication-libraries) 如果用户最近登录过，则他们不会看到弹出对话框。

虽然 Active Directory 身份验证库针对 AngularJS 应用程序进行了优化，但它也可与 SPA (JavaScript 单页) 。

> [!NOTE]
> 目前，无提示身份验证仅适用于选项卡。 从自动程序登录时，它不起作用。

## <a name="how-silent-authentication-works"></a>无提示身份验证的工作原理

Active Directory 身份验证库为 OAuth 2.0 隐式授权流创建隐藏的 iframe。 但库指定 `prompt=none` ，Azure AD不显示登录页。 如果用户需要登录或授予对应用程序的访问权限，可能需要用户交互。 如果需要用户交互，Azure AD库向应用报告的错误。 如有必要，你的应用现在可以显示登录选项。

## <a name="how-to-do-silent-authentication"></a>如何执行无提示身份验证

本文中的代码来自Teams身份验证示例节点的 Teams[示例应用](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)。

[使用 Azure AD](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp)启动无提示且简单的身份验证可配置选项卡，然后按照说明在本地计算机上运行示例。

### <a name="include-and-configure-active-directory-authentication-library"></a>包括和配置 Active Directory 身份验证库

在选项卡页中包括 Active Directory 身份验证库，然后使用客户端 ID 和重定向 URL 配置库：

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

### <a name="get-the-user-context"></a>获取用户上下文

在选项卡的内容页中，调用 `microsoftTeams.getContext()` 获取当前用户的登录提示。 该提示在调用应用 `loginHint` 时用作 Azure AD。

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

如果 Active Directory 身份验证库具有为用户缓存的未用令牌，请使用令牌。 或者，调用 `acquireToken(resource, callback)` 以静默方式接收令牌。 库使用请求的令牌调用回调函数，如果身份验证失败，则生成错误。

如果您在回调函数中收到错误，则显示并使用显式登录选项。

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

Active Directory 身份验证库通过Azure AD回调页调用来分析用户 `AuthenticationContext.handleWindowCallback(hash)` 的结果。

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

### <a name="handle-the-sign-out-flow"></a>处理注销流程

使用以下代码处理身份验证中的注销Azure AD流：

> [!NOTE]
> 从选项卡或自动Teams注销时，将清除当前会话。

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```

## <a name="see-also"></a>另请参阅

* [配置标识提供程序以使用Azure AD](../../../concepts/authentication/configure-identity-provider.md)
* [了解 MSAL (Microsoft 身份验证库) ](/azure/active-directory/develop/msal-overview)
