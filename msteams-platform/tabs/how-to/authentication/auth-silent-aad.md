---
title: 无提示的身份验证
description: 描述无提示身份验证
ms.topic: conceptual
keywords: teams 身份验证 SSO 无提示 AAD
ms.openlocfilehash: 7facaef0941ff7602b3e23444653ef41415c3396
ms.sourcegitcommit: 3727fc58e84b6f1752612884c2e0b25e207fb56e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/26/2021
ms.locfileid: "51382343"
---
# <a name="silent-authentication"></a><span data-ttu-id="fcfd7-104">无提示的身份验证</span><span class="sxs-lookup"><span data-stu-id="fcfd7-104">Silent authentication</span></span>

> [!NOTE]
> <span data-ttu-id="fcfd7-105">若要在移动客户端上对选项卡进行身份验证，请确保你使用的是至少 1.4.1 版本的 Teams JavaScript SDK。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-105">For authentication to work for your tab on mobile clients, ensure you are using at least 1.4.1 version of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="fcfd7-106">Azure Active Directory (AAD) 中的无提示身份验证通过静默刷新身份验证令牌来最大程度地减少用户输入登录凭据次数。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-106">Silent authentication in Azure Active Directory (AAD) minimizes the number of times a user enters their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="fcfd7-107">有关真正的单一登录支持，请参阅 [SSO 文档](~/tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-107">For true single sign-on support, see [SSO documentation](~/tabs/how-to/authentication/auth-aad-sso.md).</span></span>

<span data-ttu-id="fcfd7-108">如果希望代码完全在客户端运行，可以使用适用于 JavaScript 的 [AAD](/azure/active-directory/develop/active-directory-authentication-libraries) 身份验证库以静默方式获取 AAD 访问令牌。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-108">If you want to keep your code completely client-side, you can use the [AAD authentication library](/azure/active-directory/develop/active-directory-authentication-libraries) for JavaScript to get an AAD access token silently.</span></span> <span data-ttu-id="fcfd7-109">如果用户最近登录过，他们绝不会看到弹出对话框。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-109">If the user has signed in recently, they never see a popup dialog box.</span></span>

<span data-ttu-id="fcfd7-110">尽管 ADAL.js库已针对 AngularJS 应用程序进行了优化，但它也适用于纯 JavaScript 单页应用程序。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-110">Even though the ADAL.js library is optimized for AngularJS applications, it also works with pure JavaScript single-page applications.</span></span>

> [!NOTE]
> <span data-ttu-id="fcfd7-111">目前，无提示身份验证仅适用于选项卡。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-111">Currently, silent authentication only works for tabs.</span></span> <span data-ttu-id="fcfd7-112">从自动程序登录时，它不起作用。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-112">It does not work when signing in from a bot.</span></span>

## <a name="how-silent-authentication-works"></a><span data-ttu-id="fcfd7-113">无提示身份验证的工作原理</span><span class="sxs-lookup"><span data-stu-id="fcfd7-113">How silent authentication works</span></span>

<span data-ttu-id="fcfd7-114">该ADAL.js库为 OAuth 2.0 隐式授权流创建隐藏的 iframe。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-114">The ADAL.js library creates a hidden iframe for OAuth 2.0 implicit grant flow.</span></span> <span data-ttu-id="fcfd7-115">但库指定 `prompt=none` ，因此 Azure AD 永远不会显示登录页面。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-115">But the library specifies `prompt=none`, so Azure AD never shows the sign in page.</span></span> <span data-ttu-id="fcfd7-116">如果由于用户需要登录或授予对应用程序的访问权限而需要用户交互，AAD 会立即返回一个错误，ADAL.js报告给应用。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-116">If user interaction is required because the user needs to sign in or grant access to the application, AAD immediately returns an error that ADAL.js reports to your app.</span></span> <span data-ttu-id="fcfd7-117">此时，你的应用可以显示登录按钮（如果需要）。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-117">At this point your app can show a sign in button if required.</span></span>

## <a name="how-to-do-silent-authentication"></a><span data-ttu-id="fcfd7-118">如何执行无提示身份验证</span><span class="sxs-lookup"><span data-stu-id="fcfd7-118">How to do silent authentication</span></span>

<span data-ttu-id="fcfd7-119">本文中的代码来自 Teams 示例应用，该应用是 [Teams 身份验证示例节点](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs)。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-119">The code in this article comes from the Teams sample app that is [Teams authentication sample node](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/app-auth/nodejs/src/views/tab/silent/silent.hbs).</span></span>

### <a name="include-and-configure-adal"></a><span data-ttu-id="fcfd7-120">包括和配置 ADAL</span><span class="sxs-lookup"><span data-stu-id="fcfd7-120">include and configure ADAL</span></span>

<span data-ttu-id="fcfd7-121">将 ADAL.js 库包括在选项卡页中，然后使用客户端 ID 和重定向 URL 配置 ADAL：</span><span class="sxs-lookup"><span data-stu-id="fcfd7-121">Include the ADAL.js library in your tab pages and configure ADAL with your client ID and redirect URL:</span></span>

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

### <a name="get-the-user-context"></a><span data-ttu-id="fcfd7-122">获取用户上下文</span><span class="sxs-lookup"><span data-stu-id="fcfd7-122">Get the user context</span></span>

<span data-ttu-id="fcfd7-123">在选项卡的内容页中，调用 `microsoftTeams.getContext()` 获取当前用户的登录提示。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-123">In the tab's content page, call `microsoftTeams.getContext()` to get a sign in hint for the current user.</span></span> <span data-ttu-id="fcfd7-124">在调用 AAD 时，这用作 loginHint。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-124">This is used as a loginHint in the call to AAD.</span></span>

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

### <a name="authenticate"></a><span data-ttu-id="fcfd7-125">身份验证</span><span class="sxs-lookup"><span data-stu-id="fcfd7-125">Authenticate</span></span>

<span data-ttu-id="fcfd7-126">如果 ADAL 为尚未过期的用户缓存了一个令牌，请使用该令牌。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-126">If ADAL has a token cached for the user that has not expired, use that token.</span></span> <span data-ttu-id="fcfd7-127">或者，尝试通过调用 以静默方式获取令牌 `acquireToken(resource, callback)` 。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-127">Alternately, attempt to get a token silently by calling `acquireToken(resource, callback)`.</span></span> <span data-ttu-id="fcfd7-128">ADAL.js请求的令牌调用回调函数，或在身份验证失败时提供错误。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-128">ADAL.js calls the callback function with the requested token, or gives an error if authentication fails.</span></span>

<span data-ttu-id="fcfd7-129">如果您在回调函数中收到错误，则显示登录按钮并回退到显式登录。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-129">If you get an error in the callback function, show a sign in button and fall back to an explicit sign in.</span></span>

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

### <a name="process-the-return-value"></a><span data-ttu-id="fcfd7-130">处理返回值</span><span class="sxs-lookup"><span data-stu-id="fcfd7-130">Process the return value</span></span>

<span data-ttu-id="fcfd7-131">ADAL.js登录回调页中调用来分析 AAD `AuthenticationContext.handleWindowCallback(hash)` 的结果。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-131">ADAL.js parses the result from AAD by calling `AuthenticationContext.handleWindowCallback(hash)` in the sign in callback page.</span></span>

<span data-ttu-id="fcfd7-132">检查用户是否有效，并调用 `microsoftTeams.authentication.notifySuccess()` 或 `microsoftTeams.authentication.notifyFailure()` 将状态报告给主选项卡内容页。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-132">Check that you have a valid user and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()` to report the status to your main tab content page.</span></span>

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

### <a name="handle-sign-out-flow"></a><span data-ttu-id="fcfd7-133">处理注销流</span><span class="sxs-lookup"><span data-stu-id="fcfd7-133">Handle sign out flow</span></span>

<span data-ttu-id="fcfd7-134">使用以下代码处理 AAD 身份验证中的注销流：</span><span class="sxs-lookup"><span data-stu-id="fcfd7-134">Use the following code to handle sign out flow in AAD Auth:</span></span>

> [!NOTE]
> <span data-ttu-id="fcfd7-135">当 Teams 选项卡或自动程序注销完成时，当前会话也将清除。</span><span class="sxs-lookup"><span data-stu-id="fcfd7-135">While logout for Teams tab or bot is done, the current session is also cleared.</span></span>

```javascript
function logout() {
localStorage.clear();
window.location.href = "@Url.Action("<<Action Name>>", "<<Controller Name>>")";
}
```