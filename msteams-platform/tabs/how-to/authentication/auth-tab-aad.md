---
title: 使用 Azure Active Directory 对选项卡进行身份验证
description: 介绍 Teams 中的身份验证以及如何在选项卡中使用它
ms.topic: how-to
ms.localizationpriority: medium
keywords: Teams 身份验证选项卡, Microsoft Azure Active Directory (Azure AD)
ms.openlocfilehash: aa60f3908a13b55add525a561fe3f60afaad6c87
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65757316"
---
# <a name="authenticate-a-user-in-a-microsoft-teams-tab"></a>在 Microsoft Teams 选项卡中对用户进行身份验证

> [!Note]
> 若要在移动客户端上对选项卡进行身份验证，你需要确保使用的是 Teams JavaScript SDK 1.4.1 或更高版本。

你可能希望在 Teams 应用中使用许多服务，其中大多数服务都需要身份验证和授权才能访问该服务。 服务包括 Facebook、Twitter 和Teams。 Teams 用户配置文件信息存储在使用 Microsoft Graph 的 Azure AD 中，本文将重点介绍如何使用 Azure AD 进行身份验证以获取对此信息的访问权限。

OAuth 2.0 是 Azure AD 和许多其他服务提供商使用的身份验证开放标准。 了解 OAuth 2.0 是在 Teams 和 Azure AD 中使用身份验证的先决条件。 以下示例使用 OAuth 2.0 隐式授予流，目标是最终从 Azure AD 和 Microsoft Graph 中读取用户的个人资料信息。

本文中的代码来自Teams示例应用[Microsoft Teams选项卡身份验证示例 (节点) ](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)。 它包含一个静态选项卡，用于请求 Microsoft Graph 的访问令牌并显示来自 Azure AD 的当前用户的基本个人资料信息。

有关选项卡的身份验证流的一般概述，请参阅[选项卡中的身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)。

选项卡中的身份验证流与机器人中的身份验证流略有不同。

## <a name="configuring-identity-providers"></a>配置身份提供程序

有关在将 Azure AD 用作身份提供程序时配置 OAuth 2.0 回调重定向 URL 的详细步骤，请参阅主题[配置身份提供程序](~/concepts/authentication/configure-identity-provider.md)。

## <a name="initiate-authentication-flow"></a>启动身份验证流

身份验证流应由用户操作触发。 不应自动打开身份验证弹出窗口，因为这可能会触发浏览器的弹出窗口阻止程序并混淆用户。

将按钮添加到配置或内容页，使用户能够在需要时登录。 可在选项卡的[配置](~/tabs/how-to/create-tab-pages/configuration-page.md)页或任何[内容](~/tabs/how-to/create-tab-pages/content-page.md)页上完成此操作。

与大多数标识提供者一样，Azure AD 不允许将其内容放置在 iframe 中。 这意味着需要添加一个弹出页来托管标识提供者。 在以下示例中，此页为 `/tab-auth/simple-start`. 选择按钮时，可使用 Microsoft Teams 客户端 SDK 的 `microsoftTeams.authenticate()` 函数启动此页面。

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

* 传递给 `microsoftTeams.authentication.authenticate()` 的 URL 是身份验证流的起始页。 在此示例中，它是 `/tab-auth/simple-start`。 这应与在 [Azure AD 应用程序注册门户](https://apps.dev.microsoft.com)中注册的内容相一致。

* 身份验证流必须从域上的页面开始。 此域还应在清单的 [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) 部分中列出。 如果不这样做，则会导致出现空弹出窗口。

* 如果无法使用 `microsoftTeams.authentication.authenticate()`，则会导致弹出窗口在登录过程结束时无法关闭。

## <a name="navigate-to-the-authorization-page-from-your-pop-up-page"></a>从弹出页导航到授权页

显示弹出页 (`/tab-auth/simple-start`) 时，将运行以下代码。 此页面的主要目标是重定向到身份提供程序，以便用户可以登录。 可以使用 HTTP 302 在服务器端执行此重定向，但在本例中，此重定向是在客户端使用调用来 `window.location.assign()`完成的。 这还允许使用 `microsoftTeams.getContext()` 来检索提示信息，这些提示信息可以传递给 Azure AD。

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

完成授权后，用户将重定向到在 `/tab-auth/simple-end` 上为应用指定的回调页。

### <a name="notes"></a>注释

* 有关生成身份验证请求和 URL 的帮助，请参阅[获取用户上下文信息](~/tabs/how-to/access-teams-context.md)。 例如，可以将用户的登录名用作 Azure AD登录的 `login_hint` 值，这意味着用户只需输入更少的内容。 请记住，不应直接使用此上下文作为身份证明，因为攻击者可能会在恶意浏览器中加载页面，并向其提供所需的任何信息。
* 尽管选项卡上下文提供了有关用户的有用信息，但无论是将其用作选项卡内容 URL 的 URL 参数还是通过调用 Microsoft Teams 客户端 SDK 中的 `microsoftTeams.getContext()` 函数，都不要使用此信息对用户进行身份验证。 恶意行动者可以使用自己的参数来调用选项卡内容 URL，而模拟 Microsoft Teams 的网页可能会在 iframe 中加载选项卡内容 URL，并将其自己的数据返回给 `getContext()` 函数。 应将选项卡上下文中与身份相关的信息视为提示，并在使用前对其进行验证。
* `state` 参数用于确认调用回调 URI 的服务就是你调用的服务。 `state`如果回调中的参数与在调用期间发送的参数不匹配，则返回调用不会进行验证，应终止。
* 无需在应用的 manifest.json 文件的列表中 `validDomains` 包含标识提供者的域。

## <a name="the-callback-page"></a>回调页

在上一部分中，你调用了 Azure AD 授权服务，并传入了用户和应用信息，以便 Azure AD 可以向用户提供自己的整体授权体验。 你的应用无法控制此体验中发生的情况。 它只知道当 Azure AD 调用你提供的回调页时返回的内容 (`/tab-auth/simple-end`)。

在此页中，需要根据 Azure AD 返回的信息和调用或确定 `microsoftTeams.authentication.notifySuccess()` 成功或 `microsoftTeams.authentication.notifyFailure()`失败。 如果登录成功，你将有权访问服务资源。

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

此代码使用 `getHashParameters()` 帮助程序函数来解析从 `window.location.hash` 中的 Azure AD 接收到的键值对。 如果它找到 `access_token`，并且 `state` 值与身份验证流开始时提供的值相同，则它会通过调用 `notifySuccess()` 将访问令牌返回给选项卡，否则会报告错误并显示 `notifyFailure()`。

### <a name="notes"></a>注释

`NotifyFailure()` 具有以下预定义的失败原因：

* `CancelledByUser`：用户在完成身份验证流之前关闭了弹出窗口。
* `FailedToOpenWindow` 无法打开弹出窗口。 当 Microsoft Teams 在浏览器中运行时，这通常意味着窗口被弹出窗口阻止程序阻止。

如果成功，则可以刷新或重新加载页面，并显示与现在经过身份验证的用户相关的内容。 如果身份验证失败，则会显示一条错误消息。

你的应用可以设置自己的会话 Cookie，以便用户在返回到当前设备上的选项卡时无需再次登录。

> [!NOTE]
>
> * 计划于 2020 年初发布的 Chrome 80 引入了新的 Cookie 值并默认实施 Cookie 策略。 建议为 Cookie 设置预期用途，而不是依赖默认浏览器行为。 *请参阅* [SameSite Cookie 属性（2020 年更新）](../../../resources/samesite-cookie-update.md)。
> * 若要为 Microsoft Teams 免费版和来宾用户获取正确的令牌，应用必须使用特定于租户的终结点 `https://login.microsoftonline.com/**{tenantId}**`，这一点很重要。 可以从机器人消息或选项卡上下文中获取 tenantId。 如果应用使用 `https://login.microsoftonline.com/common`，则用户将收到不正确的令牌，并且将登录到“主页”租户，而不是当前登录到的租户。

有关单Sign-On (SSO) 的详细信息，请参阅 [“无提示身份验证](~/tabs/how-to/authentication/auth-silent-AAD.md)”一文。

## <a name="code-sample"></a>代码示例

显示使用 Azure AD 的选项卡身份验证流程的示例代码：

| **示例名称** | **说明** | **.NET** | **Node.js** |
|-----------------|-----------------|-------------|
| Microsoft Teams 选项卡身份验证 | 使用 Azure AD 的选项卡身份验证流程。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-channel-group-config-page-auth/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-auth/nodejs) |

## <a name="see-also"></a>另请参阅

* [规划用户身份验证](../../../concepts/design/understand-use-cases.md)
* [为 Microsoft Teams 设计选项卡](~/tabs/design/tabs.md)
* [无提示的身份验证](~/tabs/how-to/authentication/auth-silent-aad.md)
* [为消息扩展添加身份验证](~/messaging-extensions/how-to/add-authentication.md)
* [机器人的单一登录 (SSO) 支持](~/bots/how-to/authentication/auth-aad-sso-bots.md)
