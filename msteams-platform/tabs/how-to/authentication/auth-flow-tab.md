---
title: 选项卡的身份验证流
description: 描述选项卡中的身份验证流
keywords: 团队身份验证流选项卡
ms.openlocfilehash: 5ecd4d7d3a2658d17a8c6dea5d73cbd98eb2dfde
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552540"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>Microsoft 团队身份验证流（针对选项卡）

> [!Note]
> 若要对移动客户端上的选项卡进行身份验证，您需要确保您至少使用的是1.4.1 版本的团队 JavaScript SDK。
> 团队 SDK 为身份验证流启动单独的窗口，因此 samesite 属性可以设置为 "不严格"。 目前，SameSite = None 不受团队桌面客户端或 Chrome 或 Safari 早期版本的支持。

OAuth 2.0 是一种开放的标准，用于 Azure AD 和许多其他标识提供程序使用的身份验证和授权。 对 OAuth 2.0 的基本了解是在团队中使用身份验证的先决条件; [下面是一个很好的概述](https://aaronparecki.com/oauth-2-simplified/) ，比 [正式规范](https://oauth.net/2/)更易于遵循。 选项卡和 bot 的身份验证流略有不同，因为选项卡非常类似于网站，因此可以直接使用 OAuth 2.0;bot 不是，并且必须以不同的方式执行几项操作，但核心概念是相同的。

有关使用 Node 和 [OAuth 2.0 隐式授予类型](https://oauth.net/2/grant-types/implicit/)的选项卡和 bot 的身份验证流示例，*请参阅*[启动身份验证流。](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow)

![选项卡身份验证序列图](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. 用户与选项卡配置或内容页上的内容进行交互，通常是一个标记为 "登录" 或 "登录" 的按钮。
2. 该选项卡构造其授权起始页的 URL，可以选择使用 URL 占位符中的信息，也可以通过调用 `microsoftTeams.getContext()` 团队客户端 SDK 方法来简化用户的身份验证体验。 例如，在使用 Azure AD 进行身份验证时，如果 `login_hint` 将参数设置为用户的电子邮件地址，则用户甚至可能无法登录（如果可能最近这样做），因为如果可能，AZURE AD 将使用用户缓存的凭据：弹出窗口将短暂闪烁，然后消失。
3. 然后，该选项卡调用 `microsoftTeams.authentication.authenticate()` 方法并注册 `successCallback` 和 `failureCallback` 函数。
4. 团队在弹出窗口的 iframe 中打开起始页。 起始页生成随机 `state` 数据，并将其保存以供将来验证，并重定向到标识提供程序的 `/authorize` 终结点（如 `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` Azure AD）。 `<tenant id>`将替换为你自己的租户 id (context.subname) 。
    * 与团队中的其他应用程序身份验证流一样，起始页必须位于其列表中的域中 `validDomains` 和登录后重定向页面所在的同一个域中。
    * **重要说明**：对身份验证请求中的参数的 OAuth 2.0 隐式授予流调用， `state` 其中包含唯一的会话数据，以防止 [跨站点请求伪造攻击](https://en.wikipedia.org/wiki/Cross-site_request_forgery)。 下面的示例对数据使用随机生成的 GUID `state` 。
5. 在提供程序的网站上，用户登录并授予对该选项卡的访问权限。
6. 提供程序将用户带访问令牌的选项卡的 OAuth 2.0 重定向页面。
7. 该选项卡将检查返回的 `state` 值是否与先前保存的值匹配，以及调用 `microsoftTeams.authentication.notifySuccess()` ，后者又会调用 `successCallback` 在步骤3中注册的函数。
8. 团队将关闭弹出窗口。
9. 该选项卡显示配置 UI 或刷新或重新加载选项卡内容，具体取决于用户的启动位置。

## <a name="treat-tab-context-as-hints"></a>将选项卡上下文视为提示

尽管选项卡上下文提供了有关用户的有用信息，但请勿使用此信息对用户进行身份验证，无论您是将其作为 URL 参数获取到您的选项卡内容 URL，还是通过在 `microsoftTeams.getContext()` Microsoft 团队客户端 SDK 中调用该函数。 恶意参与者可以使用其自己的参数调用您的选项卡内容 URL，并且模拟 Microsoft 团队的网页可以在 iframe 中加载您的选项卡内容 URL 并将其自己的数据返回到 `getContext()` 函数中。 应在选项卡上下文中将与标识相关的信息简单地视为提示，并在使用之前对其进行验证。 请参阅 [从弹出页面导航到 "授权" 页面](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)中的注释。

## <a name="samples"></a>示例

有关显示 tab 验证过程的示例代码，请参阅：

* [Microsoft 团队选项卡身份验证示例 (节点) ](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Microsoft (c # ) 的 "团队" 选项卡身份验证示例 ](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

## <a name="more-details"></a>更多详细信息

有关针对 Azure Active Directory 进行选项卡身份验证的详细实施演练，请参阅：

* [在 Microsoft 团队选项卡中对用户进行身份验证](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [无提示的身份验证](~/tabs/how-to/authentication/auth-silent-AAD.md)
