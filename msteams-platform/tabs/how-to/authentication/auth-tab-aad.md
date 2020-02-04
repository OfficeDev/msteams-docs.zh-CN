---
title: 使用 Azure Active Directory 的选项卡的身份验证
description: 描述团队中的身份验证以及如何在选项卡中使用
keywords: 团队身份验证选项卡 AAD
ms.openlocfilehash: 760fce99a51dc722905035bade6db008072ee0b4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673249"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a><span data-ttu-id="0ba53-104">在 Microsoft 团队选项卡中对用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="0ba53-104">Authenticate a user in a Microsoft Teams tab</span></span>

> [!Note]
> <span data-ttu-id="0ba53-105">若要对移动客户端上的选项卡进行身份验证，您需要确保使用的是版本1.4.1 或团队 JavaScript SDK 的更高版本。</span><span class="sxs-lookup"><span data-stu-id="0ba53-105">For authentication to work for your tab on mobile clients, you need to ensure you're using version 1.4.1 or later of the Teams JavaScript SDK.</span></span>

<span data-ttu-id="0ba53-106">您可能需要在团队应用程序中使用许多服务，这些服务中的大多数都需要身份验证和授权才能获取对服务的访问权限。</span><span class="sxs-lookup"><span data-stu-id="0ba53-106">There are many services that you may wish to consume inside your Teams app, and most of those services require authentication and authorization to get access to the service.</span></span> <span data-ttu-id="0ba53-107">服务包括 Facebook、Twitter 和课程团队。</span><span class="sxs-lookup"><span data-stu-id="0ba53-107">Services include Facebook, Twitter, and of course Teams.</span></span> <span data-ttu-id="0ba53-108">工作组用户在 Azure Active Directory （Azure AD）中使用 Microsoft Graph 存储了用户配置文件信息，本文将重点介绍如何使用 Azure AD 获取此信息的访问权限。</span><span class="sxs-lookup"><span data-stu-id="0ba53-108">Users of Teams have user profile information stored in Azure Active Directory (Azure AD) using Microsoft Graph and this article will focus on authentication using Azure AD to get access to this information.</span></span>

<span data-ttu-id="0ba53-109">OAuth 2.0 是一种开放的标准，用于 Azure AD 和许多其他服务提供商使用的身份验证。</span><span class="sxs-lookup"><span data-stu-id="0ba53-109">OAuth 2.0 is an open standard for authentication used by Azure AD and many other service providers.</span></span> <span data-ttu-id="0ba53-110">了解 OAuth 2.0 是在团队和 Azure AD 中使用身份验证的先决条件。</span><span class="sxs-lookup"><span data-stu-id="0ba53-110">Understanding OAuth 2.0 is a prerequisite for working with authentication in Teams and Azure AD.</span></span> <span data-ttu-id="0ba53-111">下面的示例使用 OAuth 2.0 隐式授予流，其目标是最终从 Azure AD 和 Microsoft Graph 读取用户的配置文件信息。</span><span class="sxs-lookup"><span data-stu-id="0ba53-111">The examples below use the OAuth 2.0 Implicit Grant flow with the goal of eventually reading the user's profile information from Azure AD and Microsoft Graph.</span></span>

<span data-ttu-id="0ba53-112">本文中的代码来自团队示例应用程序[Microsoft 团队选项卡身份验证示例（节点）](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)。</span><span class="sxs-lookup"><span data-stu-id="0ba53-112">The code in this article comes from the Teams sample app [Microsoft Teams tab authentication sample (Node)](https://github.com/OfficeDev/microsoft-teams-sample-complete-node).</span></span> <span data-ttu-id="0ba53-113">它包含一个静态选项卡，该选项卡请求 Microsoft Graph 的访问令牌，并显示来自 Azure AD 的当前用户的基本配置文件信息。</span><span class="sxs-lookup"><span data-stu-id="0ba53-113">It contains a static tab that requests an access token for Microsoft Graph and shows the current user's basic profile information from Azure AD.</span></span>

<span data-ttu-id="0ba53-114">有关选项卡的身份验证流的一般概述，请参阅[选项卡中的主题身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)。</span><span class="sxs-lookup"><span data-stu-id="0ba53-114">For a general overview of authentication flow for tabs see the topic [Authentication flow in tabs](~/tabs/how-to/authentication/auth-flow-tab.md).</span></span>

<span data-ttu-id="0ba53-115">选项卡中的身份验证流与 bot 中的身份验证流略有不同。</span><span class="sxs-lookup"><span data-stu-id="0ba53-115">Authentication flow in tabs differs slightly from authentication flow in bots.</span></span>

## <a name="configuring-identity-providers"></a><span data-ttu-id="0ba53-116">配置标识提供程序</span><span class="sxs-lookup"><span data-stu-id="0ba53-116">Configuring identity providers</span></span>

<span data-ttu-id="0ba53-117">有关在使用 Azure Active Directory 作为标识提供程序时配置 OAuth 2.0 回调重定向 URL 的详细步骤，请参阅主题[配置标识提供程序](~/concepts/authentication/configure-identity-provider.md)。</span><span class="sxs-lookup"><span data-stu-id="0ba53-117">See the topic [Configure identity providers](~/concepts/authentication/configure-identity-provider.md) for detailed steps on configuring OAuth 2.0 callback redirect URL(s) when using Azure Active Directory as an identity provider.</span></span>

## <a name="initiate-authentication-flow"></a><span data-ttu-id="0ba53-118">启动身份验证流</span><span class="sxs-lookup"><span data-stu-id="0ba53-118">Initiate authentication flow</span></span>

<span data-ttu-id="0ba53-119">应由用户操作触发身份验证流。</span><span class="sxs-lookup"><span data-stu-id="0ba53-119">Authentication flow should be triggered by a user action.</span></span> <span data-ttu-id="0ba53-120">您不应自动打开身份验证弹出窗口，因为这可能会触发浏览器的弹出窗口阻止器，并将用户搞糊涂。</span><span class="sxs-lookup"><span data-stu-id="0ba53-120">You should not open the authentication pop-up automatically because this is likely to trigger the browser's pop-up blocker as well as confuse the user.</span></span>

<span data-ttu-id="0ba53-121">向您的配置或内容页添加一个按钮，以使用户能够在需要时登录。</span><span class="sxs-lookup"><span data-stu-id="0ba53-121">Add a button to your configuration or content page to enable the user to sign in when needed.</span></span> <span data-ttu-id="0ba53-122">可以在 "选项卡[配置](~/tabs/how-to/create-tab-pages/configuration-page.md)" 页或任何[内容](~/tabs/how-to/create-tab-pages/content-page.md)页中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="0ba53-122">This can be done in the tab [configuration](~/tabs/how-to/create-tab-pages/configuration-page.md) page or any [content](~/tabs/how-to/create-tab-pages/content-page.md) page.</span></span>

<span data-ttu-id="0ba53-123">与大多数标识提供程序一样，Azure AD 不允许将其内容放置在 iframe 中。</span><span class="sxs-lookup"><span data-stu-id="0ba53-123">Azure AD, like most identity providers, does not allow its content to be placed in an iframe.</span></span> <span data-ttu-id="0ba53-124">这意味着，您需要添加一个弹出页面来承载标识提供程序。</span><span class="sxs-lookup"><span data-stu-id="0ba53-124">This means that you will need to add a pop-up page to host the identity provider.</span></span> <span data-ttu-id="0ba53-125">在下面的示例中，此`/tab-auth/simple-start`页为。</span><span class="sxs-lookup"><span data-stu-id="0ba53-125">In the following example this page is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="0ba53-126">使用 Microsoft `microsoftTeams.authenticate()` TEAM client SDK 的功能在选择按钮时启动此页。</span><span class="sxs-lookup"><span data-stu-id="0ba53-126">Use the `microsoftTeams.authenticate()` function of the Microsoft Teams client SDK to launch this page when your button is selected.</span></span>

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

### <a name="notes"></a><span data-ttu-id="0ba53-127">注释</span><span class="sxs-lookup"><span data-stu-id="0ba53-127">Notes</span></span>

* <span data-ttu-id="0ba53-128">您传递到`microsoftTeams.authentication.authenticate()`的 URL 是身份验证流的起始页。</span><span class="sxs-lookup"><span data-stu-id="0ba53-128">The URL you pass to `microsoftTeams.authentication.authenticate()` is the start page of the authentication flow.</span></span> <span data-ttu-id="0ba53-129">在此示例中为`/tab-auth/simple-start`。</span><span class="sxs-lookup"><span data-stu-id="0ba53-129">In this example that is `/tab-auth/simple-start`.</span></span> <span data-ttu-id="0ba53-130">这应与您在[AZURE AD 应用程序注册门户](https://apps.dev.microsoft.com)中注册的内容相匹配。</span><span class="sxs-lookup"><span data-stu-id="0ba53-130">This should match what you registered in the [Azure AD Application Registration Portal](https://apps.dev.microsoft.com).</span></span>

* <span data-ttu-id="0ba53-131">身份验证流必须在您的域中的页面上启动。</span><span class="sxs-lookup"><span data-stu-id="0ba53-131">Authentication flow must start on a page that's on your domain.</span></span> <span data-ttu-id="0ba53-132">此外，还应在清单[`validDomains`](~/resources/schema/manifest-schema.md#validdomains)部分列出此域。</span><span class="sxs-lookup"><span data-stu-id="0ba53-132">This domain should also be listed in the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) section of the manifest.</span></span> <span data-ttu-id="0ba53-133">如果不这样做，则会导致空弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="0ba53-133">Failure to do so will result in an empty pop-up.</span></span>

* <span data-ttu-id="0ba53-134">如果无法使用`microsoftTeams.authentication.authenticate()` ，将导致在登录过程结束时未关闭弹出窗口的问题。</span><span class="sxs-lookup"><span data-stu-id="0ba53-134">Failing to use `microsoftTeams.authentication.authenticate()` will cause a problem with the popup not closing at the end of the sign in process.</span></span>

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a><span data-ttu-id="0ba53-135">从弹出页导航到 "授权" 页</span><span class="sxs-lookup"><span data-stu-id="0ba53-135">Navigate to the authorization page from your popup page</span></span>

<span data-ttu-id="0ba53-136">当弹出页面（`/tab-auth/simple-start`）显示时，将运行以下代码。</span><span class="sxs-lookup"><span data-stu-id="0ba53-136">When your popup page (`/tab-auth/simple-start`) is displayed the following code is run.</span></span> <span data-ttu-id="0ba53-137">此页面的主要目标是重定向到你的身份提供商，以便用户可以登录。</span><span class="sxs-lookup"><span data-stu-id="0ba53-137">The main goal of this page is to redirect to your identity provider so the user can sign in.</span></span> <span data-ttu-id="0ba53-138">此重定向可在服务器端使用 HTTP 302 进行，但在这种情况下，会在使用调用的客户端上完成此`window.location.assign()`重定向。</span><span class="sxs-lookup"><span data-stu-id="0ba53-138">This redirection could be done on the server side using HTTP 302, but in this case it is done on the client side using with a call to `window.location.assign()`.</span></span> <span data-ttu-id="0ba53-139">这也允许`microsoftTeams.getContext()`用于检索可传递给 Azure AD 的提示信息。</span><span class="sxs-lookup"><span data-stu-id="0ba53-139">This also allows `microsoftTeams.getContext()` to be used to retrieve hinting information which can be passed to Azure AD.</span></span>

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
        resource: "https://graph.microsoft.com/User.Read openid",
        redirect_uri: window.location.origin + "/tab-auth/simple-end",
        nonce: _guid(),
        state: state,
        // The context object is populated by Teams; the loginHint attribute
         // is used as hinting information
        login_hint: context.loginHint,
    };

    let authorizeEndpoint = "https://login.microsoftonline.com/" + context.tid + "/oauth2/authorize?" + toQueryString(queryParams);
    window.location.assign(authorizeEndpoint);
});
```

<span data-ttu-id="0ba53-140">用户完成授权后，会将用户重定向到您在上`/tab-auth/simple-end`为您的应用程序指定的回拨页面。</span><span class="sxs-lookup"><span data-stu-id="0ba53-140">After the user completes authorization, the user is redirected to the callback page you specified for your app at `/tab-auth/simple-end`.</span></span>

### <a name="notes"></a><span data-ttu-id="0ba53-141">注释</span><span class="sxs-lookup"><span data-stu-id="0ba53-141">Notes</span></span>

* <span data-ttu-id="0ba53-142">有关生成身份验证请求和 Url 的帮助，请参阅[获取用户上下文信息](~/tabs/how-to/access-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="0ba53-142">See [get user context information](~/tabs/how-to/access-teams-context.md) for help building authentication requests and URLs.</span></span> <span data-ttu-id="0ba53-143">例如，可以使用用户的登录名作为 Azure AD 登录的`login_hint`值，这意味着用户可能需要键入更少的值。</span><span class="sxs-lookup"><span data-stu-id="0ba53-143">For example, you can use the user's login name as the `login_hint` value for Azure AD sign-in, which means the user might need to type less.</span></span> <span data-ttu-id="0ba53-144">请注意，您不应直接将此上下文用作身份证明，因为攻击者可以在恶意浏览器中加载页面并为其提供所需的任何信息。</span><span class="sxs-lookup"><span data-stu-id="0ba53-144">Remember that you should not use this context directly as proof of identity since an attacker could load your page in a malicious browser and provide it with any information they want.</span></span>
* <span data-ttu-id="0ba53-145">尽管选项卡上下文提供了有关用户的有用信息，但请勿使用此信息对用户进行身份验证，无论您是将其作为 URL 参数获取到您的`microsoftTeams.getContext()`选项卡内容 URL，还是通过在 Microsoft 团队客户端 SDK 中调用该函数。</span><span class="sxs-lookup"><span data-stu-id="0ba53-145">Although the tab context provides useful information regarding the user, don't use this information to authenticate the user whether you get it as URL parameters to your tab content URL or by calling the `microsoftTeams.getContext()` function in the Microsoft Teams client SDK.</span></span> <span data-ttu-id="0ba53-146">恶意参与者可以使用其自己的参数调用您的选项卡内容 URL，并且模拟 Microsoft 团队的网页可以在 iframe 中加载您的选项卡内容 URL 并将其自己`getContext()`的数据返回到函数中。</span><span class="sxs-lookup"><span data-stu-id="0ba53-146">A malicious actor could invoke your tab content URL with its own parameters, and a web page impersonating Microsoft Teams could load your tab content URL in an iframe and return its own data to the `getContext()` function.</span></span> <span data-ttu-id="0ba53-147">应在选项卡上下文中将与标识相关的信息简单地视为提示，并在使用之前对其进行验证。</span><span class="sxs-lookup"><span data-stu-id="0ba53-147">You should treat the identity-related information in the tab context simply as hints and validate them before use.</span></span>
* <span data-ttu-id="0ba53-148">此`state`参数用于确认调用回调 URI 的服务是否为您调用的服务。</span><span class="sxs-lookup"><span data-stu-id="0ba53-148">The `state` parameter is used to confirm that the service calling the callback URI is the service you called.</span></span> <span data-ttu-id="0ba53-149">如果回调`state`中的参数与您在呼叫过程中发送的参数不匹配，则不会验证返回调用，应终止。</span><span class="sxs-lookup"><span data-stu-id="0ba53-149">If the `state` parameter in the callback does not match the parameter you sent during the call the return call is not verified and should be terminated.</span></span>
* <span data-ttu-id="0ba53-150">无需在应用程序的清单 json 文件中的`validDomains`列表中包含标识提供程序的域。</span><span class="sxs-lookup"><span data-stu-id="0ba53-150">It is not necessary to include the identity provider's domain in the `validDomains` list in the app's manifest.json file.</span></span>

## <a name="the-callback-page"></a><span data-ttu-id="0ba53-151">回调页</span><span class="sxs-lookup"><span data-stu-id="0ba53-151">The callback page</span></span>

<span data-ttu-id="0ba53-152">在上一节中，您调用了 Azure AD 授权服务并传入了用户和应用程序信息，以便 Azure AD 可以向用户提供自己的单一授权体验。</span><span class="sxs-lookup"><span data-stu-id="0ba53-152">In the last section you called the Azure AD authorization service and passed in user and app information so that Azure AD could present the user with its own monolithic authorization experience.</span></span> <span data-ttu-id="0ba53-153">您的应用程序无法控制此体验中发生的操作。</span><span class="sxs-lookup"><span data-stu-id="0ba53-153">Your app has no control over what happens in this experience.</span></span> <span data-ttu-id="0ba53-154">在 Azure AD 调用所提供的回调页面（`/tab-auth/simple-end`）时，所有 it 都知道返回的是返回的。</span><span class="sxs-lookup"><span data-stu-id="0ba53-154">All it knows is what is returned when Azure AD calls the  callback page that you provided (`/tab-auth/simple-end`).</span></span>

<span data-ttu-id="0ba53-155">在此页面中，您需要根据 Azure AD 返回的信息以及调用`microsoftTeams.authentication.notifySuccess()`或`microsoftTeams.authentication.notifyFailure()`来确定是否成功或失败。</span><span class="sxs-lookup"><span data-stu-id="0ba53-155">In this page you need to determine success or failure based on the information returned by Azure AD and call `microsoftTeams.authentication.notifySuccess()` or `microsoftTeams.authentication.notifyFailure()`.</span></span> <span data-ttu-id="0ba53-156">如果登录成功，您将有权访问服务资源。</span><span class="sxs-lookup"><span data-stu-id="0ba53-156">If the login was successful you will have access to service resources.</span></span>

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

<span data-ttu-id="0ba53-157">此代码分析了使用`window.location.hash` `getHashParameters()` HELPER 函数在 Azure AD 中接收到的键/值对。</span><span class="sxs-lookup"><span data-stu-id="0ba53-157">This code parses the key-value pairs received from Azure AD in `window.location.hash` using the `getHashParameters()` helper function.</span></span> <span data-ttu-id="0ba53-158">如果找到了`access_token`，并且`state`值与身份验证流开始时提供的值相同，则通过调用`notifySuccess()`返回选项卡的访问令牌;否则，它会报告错误`notifyFailure()`。</span><span class="sxs-lookup"><span data-stu-id="0ba53-158">If it finds an `access_token`, and the `state` value is the same as the one provided at the start of the authentication flow, it returns the access token to the tab by calling `notifySuccess()`; otherwise it reports an error with `notifyFailure()`.</span></span>

### <a name="notes"></a><span data-ttu-id="0ba53-159">注释</span><span class="sxs-lookup"><span data-stu-id="0ba53-159">Notes</span></span>

<span data-ttu-id="0ba53-160">`NotifyFailure()`具有以下预定义的失败原因：</span><span class="sxs-lookup"><span data-stu-id="0ba53-160">`NotifyFailure()` has the following predefined failure reasons:</span></span>

* <span data-ttu-id="0ba53-161">`CancelledByUser`用户在完成身份验证流之前关闭了弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="0ba53-161">`CancelledByUser` the user closed the popup window before completing the authentication flow.</span></span>
* <span data-ttu-id="0ba53-162">`FailedToOpenWindow`无法打开弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="0ba53-162">`FailedToOpenWindow` the popup window could not be opened.</span></span> <span data-ttu-id="0ba53-163">在浏览器中运行 Microsoft 团队时，这通常意味着弹出窗口阻止程序阻止了该窗口。</span><span class="sxs-lookup"><span data-stu-id="0ba53-163">When running Microsoft Teams in a browser, this typically means that the window was blocked by a popup blocker.</span></span>

<span data-ttu-id="0ba53-164">如果成功，您可以刷新或重新加载页面，并显示与现已通过身份验证的用户相关的内容。</span><span class="sxs-lookup"><span data-stu-id="0ba53-164">If successful, you can refresh or reload the page and show content relevant to the now-authenticated user.</span></span> <span data-ttu-id="0ba53-165">如果身份验证失败，则显示一条错误消息。</span><span class="sxs-lookup"><span data-stu-id="0ba53-165">If authentication fails, display an error message.</span></span>

<span data-ttu-id="0ba53-166">您的应用程序可以设置自己的会话 cookie，以便用户在返回到当前设备上的选项卡时无需再次登录。</span><span class="sxs-lookup"><span data-stu-id="0ba53-166">Your app can set its own session cookie so that the user need not sign in again when they return to your tab on the current device.</span></span>

> [!NOTE]
> <span data-ttu-id="0ba53-167">Chrome 80，安排在早期2020中发布，默认引入新的 cookie 值并强加 cookie 策略。</span><span class="sxs-lookup"><span data-stu-id="0ba53-167">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="0ba53-168">建议您为 cookie 设置预期用途，而不是依赖于默认浏览器行为。</span><span class="sxs-lookup"><span data-stu-id="0ba53-168">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="0ba53-169">*请参阅* [SameSite cookie 属性（2020更新）](../../../resources/samesite-cookie-update.md)。</span><span class="sxs-lookup"><span data-stu-id="0ba53-169">*See* [SameSite cookie attribute (2020 update)](../../../resources/samesite-cookie-update.md).</span></span>

<span data-ttu-id="0ba53-170">有关单一登录（SSO）的详细信息，请参阅 "[无提示身份验证](~/tabs/how-to/authentication/auth-silent-AAD.md)" 一文。</span><span class="sxs-lookup"><span data-stu-id="0ba53-170">For more information on Single Sign-On (SSO) see the article [Silent authentication](~/tabs/how-to/authentication/auth-silent-AAD.md).</span></span>

## <a name="samples"></a><span data-ttu-id="0ba53-171">示例</span><span class="sxs-lookup"><span data-stu-id="0ba53-171">Samples</span></span>

<span data-ttu-id="0ba53-172">有关使用 Azure AD 显示 tab 键身份验证过程的示例代码，请参阅：</span><span class="sxs-lookup"><span data-stu-id="0ba53-172">For sample code showing the tab authentication process using Azure AD see:</span></span>

* [<span data-ttu-id="0ba53-173">Microsoft 团队选项卡身份验证示例（节点）</span><span class="sxs-lookup"><span data-stu-id="0ba53-173">Microsoft Teams tab authentication sample (Node)</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
