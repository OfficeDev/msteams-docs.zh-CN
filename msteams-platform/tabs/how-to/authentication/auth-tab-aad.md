---
title: 使用 Azure Active Directory 的选项卡的身份验证
description: 介绍 Teams 中的身份验证以及如何在选项卡中使用它
ms.topic: how-to
keywords: teams 身份验证选项卡 AAD
ms.openlocfilehash: f2429653fe875406870ba82e27fce3d643ff69f6
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2021
ms.locfileid: "51995902"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a><span data-ttu-id="0c20c-104">在 Microsoft Teams 选项卡中对用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="0c20c-104">Authenticate a user in a Microsoft Teams tab</span></span>

> [!Note]
> <span data-ttu-id="0c20c-105">若要在移动客户端上对选项卡进行身份验证，需要确保使用的是 Teams JavaScript SDK 版本 1.4.1 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="0c20c-105">For authentication to work for your tab on mobile clients, you need to ensure you're using version 1.4.1 or later of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="0c20c-106">你可能希望在 Teams 应用内使用许多服务，这些服务中的大多数都需要进行身份验证和授权才能访问该服务。</span><span class="sxs-lookup"><span data-stu-id="0c20c-106">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="0c20c-107">服务包括 Facebook、Twitter，当然还包括 Teams。</span><span class="sxs-lookup"><span data-stu-id="0c20c-107">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="0c20c-108">Teams 用户具有使用 Microsoft Graph 存储在 Azure Active Directory (Azure AD) 中的用户配置文件信息，本文将重点介绍使用 Azure AD 进行身份验证，以便访问此信息。</span><span class="sxs-lookup"><span data-stu-id="0c20c-108">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph and this article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="0c20c-109">OAuth 2.0 是 Azure AD 和许多其他服务提供商使用的身份验证的开放式标准。</span><span class="sxs-lookup"><span data-stu-id="0c20c-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="0c20c-110">了解 OAuth 2.0 是在 Teams 和 Azure AD 中处理身份验证的先决条件。</span><span class="sxs-lookup"><span data-stu-id="0c20c-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="0c20c-111">以下示例使用 OAuth 2.0 隐式授予流，目的是最终从 Azure AD 和 Microsoft Graph 中读取用户配置文件信息。</span><span class="sxs-lookup"><span data-stu-id="0c20c-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="0c20c-112">本文中的代码来自 Node (中的 Teams 示例应用[Microsoft Teams 选项卡) 。 ](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)</span><span class="sxs-lookup"><span data-stu-id="0c20c-112">The code in this article comes from the Teams sample app [Microsoft Teams tab authentication sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span> <span data-ttu-id="0c20c-113">它包含一个静态选项卡，用于请求 Microsoft Graph 的访问令牌，并显示 Azure AD 中当前用户的基本个人资料信息。</span><span class="sxs-lookup"><span data-stu-id="0c20c-113">It contains a static tab that requests an access token for Microsoft Graph and shows the current user's basic profile information from Azure AD.</span></span>

<span data-ttu-id="0c20c-114">有关选项卡的身份验证流的一般概述，请参阅选项卡 [中的身份验证流主题](~/tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="0c20c-114">For a general overview of authentication flow for tabs see the topic [Authentication flow in tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="0c20c-115">选项卡中的身份验证流与自动程序中的身份验证流略有不同。</span><span class="sxs-lookup"><span data-stu-id="0c20c-115">Authentication flow in tabs differs slightly from authentication flow in bots.</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="0c20c-116">配置标识提供程序</span><span class="sxs-lookup"><span data-stu-id="0c20c-116">Configuring identity providers</span></span>

<span data-ttu-id="0c20c-117">有关 [将](~/concepts/authentication/configure-identity-provider.md) Azure Active Directory 用作标识提供程序时配置 OAuth 2.0 回调重定向 URL () 请参阅主题配置标识提供程序。</span><span class="sxs-lookup"><span data-stu-id="0c20c-117">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="0c20c-118">启动身份验证流</span><span class="sxs-lookup"><span data-stu-id="0c20c-118">Initiate authentication flow</span></span>

<span data-ttu-id="0c20c-119">身份验证流应该由用户操作触发。</span><span class="sxs-lookup"><span data-stu-id="0c20c-119">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="0c20c-120">不应自动打开身份验证弹出窗口，因为这可能会触发浏览器的弹出窗口阻止程序，并让用户混淆。</span><span class="sxs-lookup"><span data-stu-id="0c20c-120">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

<span data-ttu-id="0c20c-121">将按钮添加到配置或内容页面，以便用户能够根据需要登录。</span><span class="sxs-lookup"><span data-stu-id="0c20c-121">Add a button to your configuration or content page to enable the user to sign in when needed.</span></span> <span data-ttu-id="0c20c-122">可以在选项卡配置页或任何[内容页](~/tabs/how-to/create-tab-pages/configuration-page.md)[中完成](~/tabs/how-to/create-tab-pages/content-page.md)此操作。</span><span class="sxs-lookup"><span data-stu-id="0c20c-122">This can be done in the tab [configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) page or any [content](~/tabs/how-to/create-tab-pages/content-page.md) page.</span></span>

<span data-ttu-id="0c20c-123">与大多数标识提供程序一样，Azure AD 不允许将其内容放置在 iframe 中。</span><span class="sxs-lookup"><span data-stu-id="0c20c-123">Azure AD, like most identity providers, does not allow its content to be placed in an iframe.</span></span> <span data-ttu-id="0c20c-124">这意味着您需要添加一个弹出窗口来承载标识提供程序。</span><span class="sxs-lookup"><span data-stu-id="0c20c-124">This means that you will need to add a pop-up page to host the identity provider.</span></span> <span data-ttu-id="0c20c-125">在下面的示例中，此页面为 `/tab-auth/simple-start` 。</span><span class="sxs-lookup"><span data-stu-id="0c20c-125">In the following example this page is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="0c20c-126">选择按钮后，使用 Microsoft Teams 客户端 SDK 的 函数 `microsoftTeams.authenticate()` 启动此页面。</span><span class="sxs-lookup"><span data-stu-id="0c20c-126">Use the `microsoftTeams.authenticate()` function of the Microsoft Teams client SDK to launch this page when your button is selected.</span></span>

```javascript
microsoftTeams.authentication.authenticate({
    url: window.location.origin + "/tab-auth/simple-start",
    width: 600,
    height: 535,
    successCallback: function (result) {
        getUserProfile(result.accessToken);
    },
    failureCallback: function (reason) {
        handleAuthError(reason);
    }
});
```

### <a name="notes"></a><span data-ttu-id="0c20c-127">注释</span><span class="sxs-lookup"><span data-stu-id="0c20c-127">Notes</span></span>

* <span data-ttu-id="0c20c-128">您传递到的 URL `microsoftTeams.authentication.authenticate()` 是身份验证流的起始页。</span><span class="sxs-lookup"><span data-stu-id="0c20c-128">The URL you pass to `microsoftTeams.authentication.authenticate()` is the start page of the authentication flow.</span></span> <span data-ttu-id="0c20c-129">此示例中为 `/tab-auth/simple-start` 。</span><span class="sxs-lookup"><span data-stu-id="0c20c-129">In this example that is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="0c20c-130">这应该匹配你在 Azure AD 应用程序注册 [门户中注册的内容](https://apps.dev.microsoft.com)。</span><span class="sxs-lookup"><span data-stu-id="0c20c-130">This should match what you registered in the [Azure AD Application Registration Portal](https://apps.dev.microsoft.com).</span></span>

* <span data-ttu-id="0c20c-131">身份验证流必须在域上的页面上启动。</span><span class="sxs-lookup"><span data-stu-id="0c20c-131">Authentication flow must start on a page that's on your domain.</span></span> <span data-ttu-id="0c20c-132">此域还应在清单 [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) 的 部分列出。</span><span class="sxs-lookup"><span data-stu-id="0c20c-132">This domain should also be listed in the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="0c20c-133">否则将导致空弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="0c20c-133">Failure to do so will result in an empty pop-up.</span></span>

* <span data-ttu-id="0c20c-134">如果不使用 `microsoftTeams.authentication.authenticate()` ，则会导致弹出窗口在登录过程结束时无法关闭。</span><span class="sxs-lookup"><span data-stu-id="0c20c-134">Failing to use `microsoftTeams.authentication.authenticate()` will cause a problem with the popup not closing at the end of the sign in process.</span></span>

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a><span data-ttu-id="0c20c-135">从弹出窗口导航到授权页面</span><span class="sxs-lookup"><span data-stu-id="0c20c-135">Navigate to the authorization page from your popup page</span></span>

<span data-ttu-id="0c20c-136">显示弹出窗口 `/tab-auth/simple-start` () 运行以下代码。</span><span class="sxs-lookup"><span data-stu-id="0c20c-136">When your popup page (`/tab-auth/simple-start`) is displayed the following code is run.</span></span> <span data-ttu-id="0c20c-137">此页面的主要目标是重定向到标识提供程序，以便用户可以登录。</span><span class="sxs-lookup"><span data-stu-id="0c20c-137">The main goal of this page is to redirect to your identity provider so the user can sign in.</span></span> <span data-ttu-id="0c20c-138">此重定向可以在服务器端使用 HTTP 302 进行，但在这种情况下，使用 调用 在客户端上完成 `window.location.assign()` 。</span><span class="sxs-lookup"><span data-stu-id="0c20c-138">This redirection could be done on the server side using HTTP 302, but in this case it is done on the client side using with a call to `window.location.assign()`.</span></span> <span data-ttu-id="0c20c-139">这还 `microsoftTeams.getContext()` 可用于检索可传递到 Azure AD 的提示信息。</span><span class="sxs-lookup"><span data-stu-id="0c20c-139">This also allows `microsoftTeams.getContext()` to be used to retrieve hinting information which can be passed to Azure AD.</span></span>

```javascript
microsoftTeams.getContext(function (context) {
    // Generate random state string and store it, so we can verify it in the callback
    let state = _guid(); // _guid() is a helper function in the sample
    localStorage.setItem("simple.state", state);
    localStorage.removeItem("simple.error");
    // Go to the Azure AD authorization endpoint
    let queryParams = {
        client_id: "YOUR_APP_ID_HERE",
        response_type: "id_token token",
        response_mode: "fragment",
        scope: "https://graph.microsoft.com/User.Read openid",
        redirect_uri: window.location.origin + "/tab-auth/simple-end",
        nonce: _guid(),
        state: state,
        // The context object is populated by Teams; the loginHint attribute
         // is used as hinting information
        login_hint: context.loginHint,
    };

    let authorizeEndpoint = "https://login.microsoftonline.com/" + context.tid + "/oauth2/v2.0/authorize?" + toQueryString(queryParams);
    window.location.assign(authorizeEndpoint);
});
```

<span data-ttu-id="0c20c-140">用户完成授权后，用户将被重定向到你在 上为你的应用指定的回调页面 `/tab-auth/simple-end` 。</span><span class="sxs-lookup"><span data-stu-id="0c20c-140">After the user completes authorization, the user is redirected to the callback page you specified for your app at `/tab-auth/simple-end`.</span></span>

### <a name="notes"></a><span data-ttu-id="0c20c-141">注释</span><span class="sxs-lookup"><span data-stu-id="0c20c-141">Notes</span></span>

* <span data-ttu-id="0c20c-142">请参阅 [获取用户上下文信息](~/tabs/how-to/access-teams-context.md) ，帮助构建身份验证请求和 URL。</span><span class="sxs-lookup"><span data-stu-id="0c20c-142">See [get user context information](~/tabs/how-to/access-teams-context.md) for help building authentication requests and URLs.</span></span> <span data-ttu-id="0c20c-143">例如，可以使用用户的登录名作为 Azure AD 登录的值，这意味着用户 `login_hint` 可能需要键入更少的内容。</span><span class="sxs-lookup"><span data-stu-id="0c20c-143">For example, you can use the user's login name as the `login_hint` value for Azure AD sign-in, which means the user might need to type less.</span></span> <span data-ttu-id="0c20c-144">请记住，不应直接使用此上下文作为标识证明，因为攻击者可能会在恶意浏览器中加载你的页面，并为用户提供其需要的任何信息。</span><span class="sxs-lookup"><span data-stu-id="0c20c-144">Remember that you should not use this context directly as proof of identity since an attacker could load your page in a malicious browser and provide it with any information they want.</span></span>
* <span data-ttu-id="0c20c-145">尽管选项卡上下文提供了有关用户的有用信息，但请勿使用此信息对用户进行身份验证，无论是作为选项卡内容 URL 的 URL 参数获取还是通过调用 Microsoft Teams 客户端 SDK 中的 函数。 `microsoftTeams.getContext()`</span><span class="sxs-lookup"><span data-stu-id="0c20c-145">Although the tab context provides useful information regarding the user, don't use this information to authenticate the user whether you get it as URL parameters to your tab content URL or by calling the `microsoftTeams.getContext()` function in the Microsoft Teams client SDK.</span></span> <span data-ttu-id="0c20c-146">恶意参与者可能会使用自己的参数调用您的选项卡内容 URL，模拟 Microsoft Teams 的网页可以在 iframe 中加载您的选项卡内容 URL，并自行将数据返回到 `getContext()` 函数。</span><span class="sxs-lookup"><span data-stu-id="0c20c-146">A malicious actor could invoke your tab content URL with its own parameters, and a web page impersonating Microsoft Teams could load your tab content URL in an iframe and return its own data to the `getContext()` function.</span></span> <span data-ttu-id="0c20c-147">你应该将选项卡上下文中的标识相关信息视为提示，并验证这些信息，然后再使用。</span><span class="sxs-lookup"><span data-stu-id="0c20c-147">You should treat the identity-related information in the tab context simply as hints and validate them before use.</span></span>
* <span data-ttu-id="0c20c-148">`state`参数用于确认调用回调 URI 的服务是调用的服务。</span><span class="sxs-lookup"><span data-stu-id="0c20c-148">The `state` parameter is used to confirm that the service calling the callback URI is the service you called.</span></span> <span data-ttu-id="0c20c-149">如果回调中的参数与在调用期间发送的参数不匹配，则返回调用不会得到验证，应该 `state` 终止。</span><span class="sxs-lookup"><span data-stu-id="0c20c-149">If the `state` parameter in the callback does not match the parameter you sent during the call the return call is not verified and should be terminated.</span></span>
* <span data-ttu-id="0c20c-150">不需要将标识提供程序的域包括在列表上的 `validDomains` 应用manifest.js文件中。</span><span class="sxs-lookup"><span data-stu-id="0c20c-150">It is not necessary to include the identity provider's domain in the `validDomains` list in the app's manifest.json file.</span></span>

## <a name="the-callback-page"></a><span data-ttu-id="0c20c-151">回调页面</span><span class="sxs-lookup"><span data-stu-id="0c20c-151">The callback page</span></span>

<span data-ttu-id="0c20c-152">在上一部分中，你调用了 Azure AD 授权服务，并传入了用户和应用信息，以便 Azure AD 可以给用户提供其自己的单一授权体验。</span><span class="sxs-lookup"><span data-stu-id="0c20c-152">In the last section you called the Azure AD authorization service and passed in user and app information so that Azure AD could present the user with its own monolithic authorization experience.</span></span> <span data-ttu-id="0c20c-153">你的应用无法控制此体验中发生的情况。</span><span class="sxs-lookup"><span data-stu-id="0c20c-153">Your app has no control over what happens in this experience.</span></span> <span data-ttu-id="0c20c-154">它只知道当 Azure AD 调用你 `/tab-auth/simple-end` () 。</span><span class="sxs-lookup"><span data-stu-id="0c20c-154">All it knows is what is returned when Azure AD calls the  callback page that you provided (`/tab-auth/simple-end`).</span></span>

<span data-ttu-id="0c20c-155">在此页面中，你需要根据 Azure AD 返回的信息并调用 或 来确定是成功还是 `microsoftTeams.authentication.notifySuccess()` 失败 `microsoftTeams.authentication.notifyFailure()` 。</span><span class="sxs-lookup"><span data-stu-id="0c20c-155">In this page you need to determine success or failure based on the information returned by Azure AD and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()`.</span></span> <span data-ttu-id="0c20c-156">如果登录成功，你将有权访问服务资源。</span><span class="sxs-lookup"><span data-stu-id="0c20c-156">If the login was successful you will have access to service resources.</span></span>

````javascript
// Split the key-value pairs passed from Azure AD
// getHashParameters is a helper function that parses the arguments sent
// to the callback URL by Azure AD after the authorization call
let hashParams = getHashParameters();
if (hashParams["error"]) {
    // Authentication/authorization failed
    microsoftTeams.authentication.notifyFailure(hashParams["error"]);
} else if (hashParams["access_token"]) {
    // Get the stored state parameter and compare with incoming state
    // This validates that the data is coming from Azure AD
    let expectedState = localStorage.getItem("simple.state");
    if (expectedState !== hashParams["state"]) {
        // State does not match, report error
        microsoftTeams.authentication.notifyFailure("StateDoesNotMatch");
    } else {
        // Success: return token information to the tab
        microsoftTeams.authentication.notifySuccess({
            idToken: hashParams["id_token"],
            accessToken: hashParams["access_token"],
            tokenType: hashParams["token_type"],
            expiresIn: hashParams["expires_in"]
        })
    }
} else {
    // Unexpected condition: hash does not contain error or access_token parameter
    microsoftTeams.authentication.notifyFailure("UnexpectedFailure");
}
````

<span data-ttu-id="0c20c-157">此代码使用帮助程序函数分析从 Azure AD 收到的 `window.location.hash` 键值 `getHashParameters()` 对。</span><span class="sxs-lookup"><span data-stu-id="0c20c-157">This code parses the key-value pairs received from Azure AD in `window.location.hash` using the `getHashParameters()` helper function.</span></span> <span data-ttu-id="0c20c-158">如果找到 ， 且 值与在身份验证流开始时提供的 相同，它将通过调用 将访问令牌返回到选项卡;否则，它将报告 `access_token` `state` `notifySuccess()` 错误 `notifyFailure()` 。</span><span class="sxs-lookup"><span data-stu-id="0c20c-158">If it finds an `access_token`, and the `state` value is the same as the one provided at the start of the authentication flow, it returns the access token to the tab by calling `notifySuccess()`; otherwise it reports an error with `notifyFailure()`.</span></span>

### <a name="notes"></a><span data-ttu-id="0c20c-159">注释</span><span class="sxs-lookup"><span data-stu-id="0c20c-159">Notes</span></span>

<span data-ttu-id="0c20c-160">`NotifyFailure()` 具有以下预定义失败原因：</span><span class="sxs-lookup"><span data-stu-id="0c20c-160">`NotifyFailure()` has the following predefined failure reasons:</span></span>

* <span data-ttu-id="0c20c-161">`CancelledByUser` 用户在完成身份验证流之前关闭了弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="0c20c-161">`CancelledByUser` the user closed the popup window before completing the authentication flow.</span></span>
* <span data-ttu-id="0c20c-162">`FailedToOpenWindow` 无法打开弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="0c20c-162">`FailedToOpenWindow` the popup window could not be opened.</span></span> <span data-ttu-id="0c20c-163">在浏览器中运行 Microsoft Teams 时，这通常意味着弹出窗口阻止程序阻止了该窗口。</span><span class="sxs-lookup"><span data-stu-id="0c20c-163">When running Microsoft Teams in a browser, this typically means that the window was blocked by a popup blocker.</span></span>

<span data-ttu-id="0c20c-164">如果成功，可以刷新或重新加载页面，并显示与现在经过身份验证的用户相关的内容。</span><span class="sxs-lookup"><span data-stu-id="0c20c-164">If successful, you can refresh or reload the page and show content relevant to the now-authenticated user.</span></span> <span data-ttu-id="0c20c-165">如果身份验证失败，则显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="0c20c-165">If authentication fails, display an error message.</span></span>

<span data-ttu-id="0c20c-166">你的应用可以设置自己的会话 Cookie，以便用户无需在当前设备上返回到你的选项卡时再次登录。</span><span class="sxs-lookup"><span data-stu-id="0c20c-166">Your app can set its own session cookie so that the user need not sign in again when they return to your tab on the current device.</span></span>

> [!NOTE]
> <span data-ttu-id="0c20c-167">Chrome 80 计划于 2020 年初发布，引入了新的 Cookie 值，并默认实施 Cookie 策略。</span><span class="sxs-lookup"><span data-stu-id="0c20c-167">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="0c20c-168">建议设置 Cookie 的预定用途，而不是依赖默认浏览器行为。</span><span class="sxs-lookup"><span data-stu-id="0c20c-168">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="0c20c-169">*请参阅* [SameSite cookie attribute (2020 update)](../../../resources/samesite-cookie-update.md)。</span><span class="sxs-lookup"><span data-stu-id="0c20c-169">*See* [SameSite cookie attribute (2020 update)](../../../resources/samesite-cookie-update.md).</span></span>

>[!NOTE]
><span data-ttu-id="0c20c-170">若要为 Microsoft Teams 免费和来宾用户获取正确的令牌，应用使用特定于租户的 https://login.microsoftonline.com/ **终结点 {tenantId} 非常重要**。</span><span class="sxs-lookup"><span data-stu-id="0c20c-170">To get the correct token for Microsoft Teams Free and guest users, it is important that the apps use tenant specific endpoint https://login.microsoftonline.com/**{tenantId}**.</span></span> <span data-ttu-id="0c20c-171">你可以从自动程序消息或选项卡上下文获取 tenantId。</span><span class="sxs-lookup"><span data-stu-id="0c20c-171">You can get tenantId from the bot message or tab context.</span></span> <span data-ttu-id="0c20c-172">如果应用使用 ，用户将获取不正确的令牌，并登录到"主页"租户，而不是当前 https://login.microsoftonline.com/common 已登录的租户。</span><span class="sxs-lookup"><span data-stu-id="0c20c-172">If the apps use https://login.microsoftonline.com/common, the users will get incorrect tokens and will log on to the "home" tenant instead of the tenant that they are currently signed into.</span></span>

<span data-ttu-id="0c20c-173">有关 Single Sign-On (SSO) 请参阅文章 [Silent authentication](~/tabs/how-to/authentication/auth-silent-AAD.md)。</span><span class="sxs-lookup"><span data-stu-id="0c20c-173">For more information on Single Sign-On (SSO) see the article [Silent authentication](~/tabs/how-to/authentication/auth-silent-AAD.md).</span></span>

## <a name="code-sample"></a><span data-ttu-id="0c20c-174">代码示例</span><span class="sxs-lookup"><span data-stu-id="0c20c-174">Code sample</span></span>

<span data-ttu-id="0c20c-175">显示使用 Azure AD 的选项卡身份验证过程的示例代码：</span><span class="sxs-lookup"><span data-stu-id="0c20c-175">Sample code showing the tab authentication process using Azure AD:</span></span>

| <span data-ttu-id="0c20c-176">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="0c20c-176">**Sample name**</span></span> | <span data-ttu-id="0c20c-177">**说明**</span><span class="sxs-lookup"><span data-stu-id="0c20c-177">**description**</span></span> | <span data-ttu-id="0c20c-178">**.NET**</span><span class="sxs-lookup"><span data-stu-id="0c20c-178">**.NET**</span></span> | <span data-ttu-id="0c20c-179">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="0c20c-179">**Node.js**</span></span> |
|-----------------|-----------------|-------------|
| <span data-ttu-id="0c20c-180">Microsoft Teams 选项卡身份验证</span><span class="sxs-lookup"><span data-stu-id="0c20c-180">Microsoft Teams tab authentication</span></span> | <span data-ttu-id="0c20c-181">使用 Azure AD 的选项卡身份验证过程。</span><span class="sxs-lookup"><span data-stu-id="0c20c-181">Tab authentication process using Azure AD.</span></span> | [<span data-ttu-id="0c20c-182">View</span><span class="sxs-lookup"><span data-stu-id="0c20c-182">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) | [<span data-ttu-id="0c20c-183">View</span><span class="sxs-lookup"><span data-stu-id="0c20c-183">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) |
