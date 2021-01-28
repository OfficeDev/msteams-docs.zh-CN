---
title: 使用 Azure Active Directory 对选项卡进行身份验证
description: 介绍 Teams 中的身份验证以及如何在选项卡中使用它
ms.topic: how-to
keywords: teams 身份验证选项卡 AAD
ms.openlocfilehash: 1502d2634b39230e0428863383bf97ada0be0359
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014563"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>在 Microsoft Teams 选项卡中对用户进行身份验证

> [!Note]
> 若要在移动客户端上对选项卡进行身份验证，需要确保使用的是 Teams JavaScript SDK 版本 1.4.1 或更高版本。

你可能希望在 Teams 应用内使用许多服务，其中大多数服务都需要身份验证和授权才能访问该服务。 服务包括 Facebook、Twitter，当然还包括 Teams。 Teams 用户具有使用 Microsoft Graph 存储在 Azure Active Directory (Azure AD) 中的用户配置文件信息，本文将重点介绍使用 Azure AD 进行身份验证，以访问此信息。

OAuth 2.0 是 Azure AD 和许多其他服务提供商使用的身份验证的开放标准。 了解 OAuth 2.0 是在 Teams 和 Azure AD 中处理身份验证的先决条件。 以下示例使用 OAuth 2.0 隐式授予流，目的是最终从 Azure AD 和 Microsoft Graph 中读取用户配置文件信息。

本文中的代码来自 Teams 示例应用 Microsoft Teams 选项卡身份验证示例 ([节点) 。 ](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) 它包含一个静态选项卡，该选项卡请求获取 Microsoft Graph 的访问令牌，并显示 Azure AD 中当前用户的基本个人资料信息。

有关选项卡的身份验证流的一般概述，请参阅选项卡[中的主题"身份验证流"。](~/tabs/how-to/authentication/auth-flow-tab.md)

选项卡中的身份验证流与自动程序中的身份验证流略有不同。

## <a name="configuring-identity-providers"></a>配置标识提供程序

有关 [将](~/concepts/authentication/configure-identity-provider.md) Azure Active Directory 用作标识提供程序) 配置 OAuth 2.0 回调重定向 (URL 的详细步骤，请参阅主题。

## <a name="initiate-authentication-flow"></a>启动身份验证流

用户操作应触发身份验证流。 不应自动打开身份验证弹出窗口，因为这可能会触发浏览器的弹出窗口阻止程序，并让用户混淆。

向配置或内容页面添加按钮，以便用户能够根据需要登录。 可以在选项卡配置页或任何内容页[](~/tabs/how-to/create-tab-pages/configuration-page.md)[中完成](~/tabs/how-to/create-tab-pages/content-page.md)此操作。

与大多数标识提供程序一样，Azure AD 不允许将其内容放置在 iframe 中。 这意味着你需要添加一个弹出窗口来承载标识提供程序。 在下面的示例中，此页面为 `/tab-auth/simple-start` 。 选择按钮后，使用 Microsoft Teams 客户端 SDK 的功能 `microsoftTeams.authenticate()` 启动此页面。

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

### <a name="notes"></a>注释

* 您传递到的 URL `microsoftTeams.authentication.authenticate()` 是身份验证流的起始页。 本示例中为 `/tab-auth/simple-start` 。 这应该匹配你在 Azure AD 应用程序注册 [门户中注册的内容](https://apps.dev.microsoft.com)。

* 身份验证流必须在域上的页面上启动。 此域还应在清单 [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) 的一节中列出。 否则将导致出现空弹出窗口。

* 如果不使用 `microsoftTeams.authentication.authenticate()` ，将导致在登录过程结束时弹出窗口未关闭的问题。

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a>从弹出窗口导航到授权页面

显示弹出窗口 `/tab-auth/simple-start` () 运行以下代码。 此页面的主要目标是重定向到标识提供程序，以便用户可以登录。 此重定向可以在服务器端使用 HTTP 302 完成，但在这种情况下，它通过调用在客户端上完成 `window.location.assign()` 。 这还 `microsoftTeams.getContext()` 可用于检索可传递到 Azure AD 的提示信息。

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

用户完成授权后，用户将被重定向到你为应用指定的回调页面 `/tab-auth/simple-end` 。

### <a name="notes"></a>注释

* 请参阅 [获取用户上下文信息](~/tabs/how-to/access-teams-context.md) ，以帮助生成身份验证请求和 URL。 例如，可以使用用户的登录名作为 Azure AD 登录的值，这意味着用户可能需要键入 `login_hint` 更少的内容。 请记住，不应直接使用此上下文作为标识证明，因为攻击者可能会在恶意浏览器中加载你的页面，并为用户提供他们需要的任何信息。
* 尽管选项卡上下文提供了有关用户的有用信息，但请勿使用此信息对用户进行身份验证，无论是作为选项卡内容 URL 的 URL 参数获取，还是通过调用 Microsoft Teams 客户端 SDK 中的函数。 `microsoftTeams.getContext()` 恶意参与者可能会使用自己的参数调用您的选项卡内容 URL，模拟 Microsoft Teams 的网页可能会加载 iframe 中的选项卡内容 URL，并自行将数据返回到 `getContext()` 函数。 你应该将选项卡上下文中的标识相关信息视为提示，并验证这些信息，然后再使用。
* 此 `state` 参数用于确认调用回调 URI 的服务是您调用的服务。 如果回调中的参数与在调用期间发送的参数不匹配，则不验证回拨，应 `state` 终止回拨。
* 不需要将标识提供程序的域包括在应用文件上的manifest.js`validDomains` 列表中。

## <a name="the-callback-page"></a>回调页面

在上一部分中，你调用了 Azure AD 授权服务，并传入了用户和应用信息，以便 Azure AD 可以给用户提供自己的单一授权体验。 你的应用无法控制此体验中发生的情况。 它只知道当 Azure AD 调用你 `/tab-auth/simple-end` () 。

在此页面中，你需要根据 Azure AD 返回的信息和调用或确定成功或 `microsoftTeams.authentication.notifySuccess()` 失败 `microsoftTeams.authentication.notifyFailure()` 。 如果登录成功，你将有权访问服务资源。

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

此代码分析在使用帮助程序函数时从 Azure AD 收到的键值 `window.location.hash` `getHashParameters()` 对。 如果找到一个 ，并且值与身份验证流开始时提供的令牌相同，它将通过调用返回对选项卡的访问令牌;否则它将报告 `access_token` `state` 一个错误 `notifySuccess()` `notifyFailure()` 。

### <a name="notes"></a>注释

`NotifyFailure()` 具有以下预定义失败原因：

* `CancelledByUser` 用户在完成身份验证流之前关闭了弹出窗口。
* `FailedToOpenWindow` 无法打开弹出窗口。 在浏览器中运行 Microsoft Teams 时，这通常意味着弹出窗口阻止程序阻止该窗口。

如果成功，可以刷新或重新加载页面，并显示与现在经过身份验证的用户相关的内容。 如果身份验证失败，则显示错误消息。

你的应用可以设置自己的会话 Cookie，以便用户无需在当前设备上返回到你的选项卡时重新登录。

> [!NOTE]
> 计划于 2020 年初发布的 Chrome 80 引入了新的 Cookie 值，并默认实施 Cookie 策略。 建议您设置 Cookie 的预定用途，而不是依赖默认浏览器行为。 *请参阅* [SameSite cookie 属性 (2020 update) 。](../../../resources/samesite-cookie-update.md)

>[!NOTE]
>若要获取适用于 Microsoft Teams 免费用户和来宾用户的正确令牌，应用使用特定于租户的终结点 https://login.microsoftonline.com/ **{tenantId} 非常重要**。 你可以从自动程序消息或选项卡上下文获取 tenantId。 如果应用使用，用户将获取不正确的令牌，并登录到"主页"租户，而不是当前 https://login.microsoftonline.com/common 登录的租户。

有关 Single Sign-On (SSO) 请参阅无提示 [身份验证一文](~/tabs/how-to/authentication/auth-silent-AAD.md)。

## <a name="samples"></a>示例

有关显示使用 Azure AD 的选项卡身份验证过程的示例代码，请参阅：

* [Microsoft Teams 选项卡身份验证示例 (节点) ](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
