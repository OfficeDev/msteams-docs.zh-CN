---
title: 无提示的身份验证
description: 描述无提示身份验证
ms.topic: conceptual
keywords: teams 身份验证 SSO 无提示 AAD
ms.openlocfilehash: e55e415aba08fdedf4409abf39115838c3a5faf0
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014094"
---
# <a name="silent-authentication"></a><span data-ttu-id="aea77-104">无提示的身份验证</span><span class="sxs-lookup"><span data-stu-id="aea77-104">Silent authentication</span></span>

> [!NOTE]
> <span data-ttu-id="aea77-105">若要在移动客户端上对选项卡进行身份验证，你需要确保你至少使用的是 1.4.1 版本的 Teams JavaScript SDK。</span><span class="sxs-lookup"><span data-stu-id="aea77-105">For authentication to work for your tab on mobile clients, you need to ensure you're using at least the 1.4.1 version of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="aea77-106">Azure Active Directory (Azure AD) 中的无提示身份验证通过静默刷新身份验证令牌来最大程度地减少用户输入其登录凭据所需的次数。</span><span class="sxs-lookup"><span data-stu-id="aea77-106">Silent authentication in Azure Active Directory (Azure AD) minimizes the number of times a user needs to enter their login credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="aea77-107"> (要获得真正的单一登录支持，请参阅我们的 [SSO 文档](~/tabs/how-to/authentication/auth-aad-sso.md)) </span><span class="sxs-lookup"><span data-stu-id="aea77-107">(For true single sign-on support, view our [SSO Documentation](~/tabs/how-to/authentication/auth-aad-sso.md))</span></span>

<span data-ttu-id="aea77-108">如果你想要使代码完全在客户端运行，可以使用适用于 JavaScript 的 [Azure Active Directory](/azure/active-directory/develop/active-directory-authentication-libraries) 身份验证库以静默方式尝试获取 Azure AD 访问令牌。</span><span class="sxs-lookup"><span data-stu-id="aea77-108">If you want to keep your code completely client-side, you can use the [Azure Active Directory Authentication Library](/azure/active-directory/develop/active-directory-authentication-libraries) for JavaScript to attempt to acquire an Azure AD access token silently.</span></span> <span data-ttu-id="aea77-109">这意味着，如果用户最近登录过，可能永远不会看到弹出对话框。</span><span class="sxs-lookup"><span data-stu-id="aea77-109">This means that the user may never see a popup dialog if they have signed in recently.</span></span>

<span data-ttu-id="aea77-110">尽管 ADAL.js库已针对 AngularJS 应用程序进行了优化，但它也适用于纯 JavaScript 单页应用程序。</span><span class="sxs-lookup"><span data-stu-id="aea77-110">Even though the ADAL.js library is optimized for AngularJS applications, it also works with pure JavaScript single-page applications.</span></span>

> [!NOTE]
> <span data-ttu-id="aea77-111">目前，无提示身份验证仅适用于选项卡。</span><span class="sxs-lookup"><span data-stu-id="aea77-111">Currently, silent authentication only works for tabs.</span></span> <span data-ttu-id="aea77-112">从自动程序登录时，它尚不起作用。</span><span class="sxs-lookup"><span data-stu-id="aea77-112">It does not yet work when signing in from a bot.</span></span>

## <a name="how-silent-authentication-works"></a><span data-ttu-id="aea77-113">无提示身份验证的工作原理</span><span class="sxs-lookup"><span data-stu-id="aea77-113">How silent authentication works</span></span>

<span data-ttu-id="aea77-114">该ADAL.js库为 OAuth 2.0 隐式授予流创建隐藏的 iframe，但它指定 Azure AD 从不显示 `prompt=none` 登录页。</span><span class="sxs-lookup"><span data-stu-id="aea77-114">The ADAL.js library creates a hidden iframe for OAuth 2.0 implicit grant flow, but it specifies `prompt=none` so that Azure AD never shows the login page.</span></span> <span data-ttu-id="aea77-115">如果由于用户需要登录或授予对应用程序的访问权限而需要用户交互，Azure AD 将立即返回错误，ADAL.js报告给应用。</span><span class="sxs-lookup"><span data-stu-id="aea77-115">If user interaction is required because the user needs to log in or grant access to the application, Azure AD will immediately return an error that ADAL.js then reports to your app.</span></span> <span data-ttu-id="aea77-116">此时，你的应用可以显示登录按钮（如果需要）。</span><span class="sxs-lookup"><span data-stu-id="aea77-116">At this point your app can show a login button if needed.</span></span>

## <a name="how-to-do-silent-authentication"></a><span data-ttu-id="aea77-117">如何执行无提示身份验证</span><span class="sxs-lookup"><span data-stu-id="aea77-117">How to do silent authentication</span></span>

<span data-ttu-id="aea77-118">本文中的代码来自 Teams 示例应用 Microsoft Teams 身份验证示例 ([Node) 。 ](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)</span><span class="sxs-lookup"><span data-stu-id="aea77-118">The code in this article comes from the Teams sample app [Microsoft Teams Authentication Sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span>

### <a name="include-and-configure-adal"></a><span data-ttu-id="aea77-119">包括和配置 ADAL</span><span class="sxs-lookup"><span data-stu-id="aea77-119">include and configure ADAL</span></span>

<span data-ttu-id="aea77-120">将ADAL.js库包括在选项卡页中，然后使用客户端 ID 和重定向 URL 配置 ADAL：</span><span class="sxs-lookup"><span data-stu-id="aea77-120">Include the ADAL.js library in your tab pages and configure ADAL with your client ID and redirect URL:</span></span>

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

### <a name="get-the-user-context"></a><span data-ttu-id="aea77-121">获取用户上下文</span><span class="sxs-lookup"><span data-stu-id="aea77-121">Get the user context</span></span>

<span data-ttu-id="aea77-122">在选项卡的内容页中，调用 `microsoftTeams.getContext()` 以获取当前用户的登录提示。</span><span class="sxs-lookup"><span data-stu-id="aea77-122">In the tab's content page, call `microsoftTeams.getContext()` to get a login hint for the current user.</span></span> <span data-ttu-id="aea77-123">这将在调用 Azure AD login_hint用作一个方法。</span><span class="sxs-lookup"><span data-stu-id="aea77-123">This will be used as a login_hint in the call to Azure AD.</span></span>

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

### <a name="authenticate"></a><span data-ttu-id="aea77-124">身份验证</span><span class="sxs-lookup"><span data-stu-id="aea77-124">Authenticate</span></span>

<span data-ttu-id="aea77-125">如果 ADAL 具有为用户缓存的未用令牌，请使用该令牌。</span><span class="sxs-lookup"><span data-stu-id="aea77-125">If ADAL has an unexpired token cached for the user, use that.</span></span> <span data-ttu-id="aea77-126">否则，尝试通过调用以静默方式获取令牌 `acquireToken(resource, callback)` 。</span><span class="sxs-lookup"><span data-stu-id="aea77-126">Otherwise, attempt to get a token silently by calling `acquireToken(resource, callback)`.</span></span> <span data-ttu-id="aea77-127">ADAL.js请求的令牌调用回调函数，或者身份验证失败时出现错误。</span><span class="sxs-lookup"><span data-stu-id="aea77-127">ADAL.js will call your callback function with the requested token, or an error if authentication fails.</span></span>

<span data-ttu-id="aea77-128">如果在回调函数中收到错误，则显示登录按钮并回退到显式登录。</span><span class="sxs-lookup"><span data-stu-id="aea77-128">If you get an error in the callback function, show a login button and fall back to an explicit login.</span></span>

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

### <a name="process-the-return-value"></a><span data-ttu-id="aea77-129">处理返回值</span><span class="sxs-lookup"><span data-stu-id="aea77-129">Process the return value</span></span>

<span data-ttu-id="aea77-130">让我们ADAL.js登录回调页中调用来分析 Azure AD `AuthenticationContext.handleWindowCallback(hash)` 中的结果。</span><span class="sxs-lookup"><span data-stu-id="aea77-130">Let ADAL.js take care of parsing the result from Azure AD by calling `AuthenticationContext.handleWindowCallback(hash)` in the login callback page.</span></span>

<span data-ttu-id="aea77-131">检查我们是否具有有效的用户并呼叫 `microsoftTeams.authentication.notifySuccess()` 或将状态报告 `microsoftTeams.authentication.notifyFailure()` 回主选项卡内容页。</span><span class="sxs-lookup"><span data-stu-id="aea77-131">Check that we have a valid user and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()` to report status back to your main tab content page.</span></span>

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
