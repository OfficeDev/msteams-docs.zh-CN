---
title: 使用 Azure Active Directory 的选项卡的身份验证
description: 描述团队中的身份验证以及如何在选项卡中使用
keywords: 团队身份验证选项卡 AAD
ms.openlocfilehash: a1d3a96e23706012b643b5827701b49e2306d847
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237781"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>在 Microsoft 团队选项卡中对用户进行身份验证

> [!Note]
> 若要对移动客户端上的选项卡进行身份验证，您需要确保使用的是版本1.4.1 或团队 JavaScript SDK 的更高版本。

您可能需要在团队应用程序中使用许多服务，这些服务中的大多数都需要身份验证和授权才能获取对服务的访问权限。 服务包括 Facebook、Twitter 和课程团队。 工作组用户在 Azure Active Directory 中存储了用户配置文件信息 (Azure AD) 使用 Microsoft Graph，本文将重点介绍如何使用 Azure AD 获取对此信息的访问权限。

OAuth 2.0 是一种开放的标准，用于 Azure AD 和许多其他服务提供商使用的身份验证。 了解 OAuth 2.0 是在团队和 Azure AD 中使用身份验证的先决条件。 下面的示例使用 OAuth 2.0 隐式授予流，其目标是最终从 Azure AD 和 Microsoft Graph 读取用户的配置文件信息。

本文中的代码来自 (Node) 的团队示例应用程序 " [Microsoft 团队" 选项卡身份验证示例 ](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)。 它包含一个静态选项卡，该选项卡请求 Microsoft Graph 的访问令牌，并显示来自 Azure AD 的当前用户的基本配置文件信息。

有关选项卡的身份验证流的一般概述，请参阅 [选项卡中的主题身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)。

选项卡中的身份验证流与 bot 中的身份验证流略有不同。

## <a name="configuring-identity-providers"></a>配置标识提供程序

有关在将 Azure Active Directory 用作标识提供程序时，请参阅 [配置标识提供程序](~/concepts/authentication/configure-identity-provider.md) ，了解有关配置 OAuth 2.0 回调重定向 URL (s 的详细步骤) 主题。

## <a name="initiate-authentication-flow"></a>启动身份验证流

应由用户操作触发身份验证流。 您不应自动打开身份验证弹出窗口，因为这可能会触发浏览器的弹出窗口阻止器，并将用户搞糊涂。

向您的配置或内容页添加一个按钮，以使用户能够在需要时登录。 可以在 "选项卡 [配置](~/tabs/how-to/create-tab-pages/configuration-page.md) " 页或任何 [内容](~/tabs/how-to/create-tab-pages/content-page.md) 页中执行此操作。

与大多数标识提供程序一样，Azure AD 不允许将其内容放置在 iframe 中。 这意味着，您需要添加一个弹出页面来承载标识提供程序。 在下面的示例中，此页为 `/tab-auth/simple-start` 。 使用 `microsoftTeams.authenticate()` Microsoft team CLIENT SDK 的功能在选择按钮时启动此页。

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

* 您传递到的 URL `microsoftTeams.authentication.authenticate()` 是身份验证流的起始页。 在此示例中为 `/tab-auth/simple-start` 。 这应与您在 [AZURE AD 应用程序注册门户](https://apps.dev.microsoft.com)中注册的内容相匹配。

* 身份验证流必须在您的域中的页面上启动。 此外，还应在清单部分列出此域 [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) 。 如果不这样做，则会导致空弹出窗口。

* 如果无法使用， `microsoftTeams.authentication.authenticate()` 将导致在登录过程结束时未关闭弹出窗口的问题。

## <a name="navigate-to-the-authorization-page-from-your-popup-page"></a>从弹出页导航到 "授权" 页

当显示弹出页面 () 时，将 `/tab-auth/simple-start` 运行以下代码。 此页面的主要目标是重定向到你的身份提供商，以便用户可以登录。 此重定向可在服务器端使用 HTTP 302 进行，但在这种情况下，会在使用调用的客户端上完成此重定向 `window.location.assign()` 。 这也允许 `microsoftTeams.getContext()` 用于检索可传递给 AZURE AD 的提示信息。

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

    let authorizeEndpoint = "https://login.microsoftonline.com/" + context.tid + "/oauth2/v2.0/authorize?" + toQueryString(queryParams);
    window.location.assign(authorizeEndpoint);
});
```

用户完成授权后，会将用户重定向到您在上为您的应用程序指定的回拨页面 `/tab-auth/simple-end` 。

### <a name="notes"></a>注释

* 有关生成身份验证请求和 Url 的帮助，请参阅 [获取用户上下文信息](~/tabs/how-to/access-teams-context.md) 。 例如，可以使用用户的登录名作为 `login_hint` AZURE AD 登录的值，这意味着用户可能需要键入更少的值。 请注意，您不应直接将此上下文用作身份证明，因为攻击者可以在恶意浏览器中加载页面并为其提供所需的任何信息。
* 尽管选项卡上下文提供了有关用户的有用信息，但请勿使用此信息对用户进行身份验证，无论您是将其作为 URL 参数获取到您的选项卡内容 URL，还是通过在 `microsoftTeams.getContext()` Microsoft 团队客户端 SDK 中调用该函数。 恶意参与者可以使用其自己的参数调用您的选项卡内容 URL，并且模拟 Microsoft 团队的网页可以在 iframe 中加载您的选项卡内容 URL 并将其自己的数据返回到 `getContext()` 函数中。 应在选项卡上下文中将与标识相关的信息简单地视为提示，并在使用之前对其进行验证。
* 此 `state` 参数用于确认调用回调 URI 的服务是否为您调用的服务。 如果 `state` 回调中的参数与您在呼叫过程中发送的参数不匹配，则不会验证返回调用，应终止。
* 不需要将标识提供程序的域包含在 `validDomains` 文件中应用程序的 manifest.js的列表中。

## <a name="the-callback-page"></a>回调页

在上一节中，您调用了 Azure AD 授权服务并传入了用户和应用程序信息，以便 Azure AD 可以向用户提供自己的单一授权体验。 您的应用程序无法控制此体验中发生的操作。 在 Azure AD 调用 () 提供的回调页面时，将会返回所有 it 知道的内容 `/tab-auth/simple-end` 。

在此页面中，您需要根据 Azure AD 返回的信息以及调用或来确定是否成功或失败 `microsoftTeams.authentication.notifySuccess()` `microsoftTeams.authentication.notifyFailure()` 。 如果登录成功，您将有权访问服务资源。

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

此代码分析了 `window.location.hash` 使用 helper 函数在 AZURE AD 中接收到的键/值对 `getHashParameters()` 。 如果找到了 `access_token` ，并且值与 `state` 身份验证流开始时提供的值相同，则通过调用将访问令牌返回到选项卡 `notifySuccess()` ; 否则，它将报告错误 `notifyFailure()` 。

### <a name="notes"></a>注释

`NotifyFailure()` 具有以下预定义的失败原因：

* `CancelledByUser` 用户在完成身份验证流之前关闭了弹出窗口。
* `FailedToOpenWindow` 无法打开弹出窗口。 在浏览器中运行 Microsoft 团队时，这通常意味着弹出窗口阻止程序阻止了该窗口。

如果成功，您可以刷新或重新加载页面，并显示与现已通过身份验证的用户相关的内容。 如果身份验证失败，则显示一条错误消息。

您的应用程序可以设置自己的会话 cookie，以便用户在返回到当前设备上的选项卡时无需再次登录。

> [!NOTE]
> Chrome 80，安排在早期2020中发布，默认引入新的 cookie 值并强加 cookie 策略。 建议您为 cookie 设置预期用途，而不是依赖于默认浏览器行为。 *请参阅* [SameSite cookie 属性 (2020 update) ](../../../resources/samesite-cookie-update.md)。

>[!NOTE]
>若要为 Microsoft 团队免费和来宾用户获取正确的令牌，请务必使用租户特定终结点 https://login.microsoftonline.com/ **{tenantId}**。 您可以从 bot 邮件或选项卡上下文获取 tenantId。 如果应用程序使用 https://login.microsoftonline.com/common ，则用户将收到不正确的令牌，并将登录到 "home" 租户，而不是他们当前登录到的租户。

有关单一登录 (SSO 的详细信息) 参阅 " [无提示身份验证](~/tabs/how-to/authentication/auth-silent-AAD.md)" 一文。

## <a name="samples"></a>示例

有关使用 Azure AD 显示 tab 键身份验证过程的示例代码，请参阅：

* [Microsoft 团队选项卡身份验证示例 (节点) ](https://github.com/OfficeDev/microsoft-teams-sample-auth-node)
