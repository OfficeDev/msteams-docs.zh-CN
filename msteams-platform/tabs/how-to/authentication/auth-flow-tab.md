---
title: 选项卡的身份验证流
description: 描述选项卡中的身份验证流
ms.topic: conceptual
keywords: teams 身份验证流选项卡
ms.openlocfilehash: 9505419a6594529bcf8d19a90d029705e573c67b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014584"
---
# <a name="microsoft-teams-authentication-flow-for-tabs"></a>选项卡的 Microsoft Teams 身份验证流

> [!Note]
> 若要在移动客户端上对选项卡进行身份验证，你需要确保你至少使用的是 1.4.1 版本的 Teams JavaScript SDK。
> Teams SDK 为身份验证流启动单独的窗口，因此 samesite 属性可以设置为"Lax"。 目前，Teams 桌面客户端或较旧版本的 Chrome 或 Safari 不支持 SameSite=None。

OAuth 2.0 是 Azure AD 和许多其他标识提供程序使用的身份验证和授权的开放标准。 基本了解 OAuth 2.0 是在 Teams 中处理身份验证的先决条件; [下面是比](https://aaronparecki.com/oauth-2-simplified/) 正式规范更易于遵循的一个很好的 [概述](https://oauth.net/2/)。 选项卡和自动程序身份验证流有点不同，因为选项卡与网站非常相似，因此可以直接使用 OAuth 2.0;机器人不是并且必须以不同方式执行一些操作，但核心概念是相同的。

*有关*[使用 Node 和](~/tabs/how-to/authentication/auth-tab-aad.md#initiate-authentication-flow) [OAuth 2.0](https://oauth.net/2/grant-types/implicit/)隐式授予类型的选项卡和聊天机器人的身份验证流示例，请参阅"为选项卡启动身份验证流"。

![Tab 键身份验证序列图](~/assets/images/authentication/tab_auth_sequence_diagram.png)

1. 用户与选项卡配置或内容页面上的内容进行交互，通常标有"登录"或"登录"的按钮。
2. 该选项卡构造其身份验证起始页的 URL，可以选择使用 URL 占位符中的信息，或者通过调用 Teams 客户端 SDK 方法来简化用户的身份验证 `microsoftTeams.getContext()` 体验。 例如，使用 Azure AD 进行身份验证时，如果参数设置为用户的电子邮件地址，则用户可能甚至不需要登录（如果他们最近已登录的话）。因为 Azure AD 将尽可能使用用户的缓存凭据：弹出窗口将短暂闪烁，然后消失。 `login_hint`
3. 然后，该选项卡 `microsoftTeams.authentication.authenticate()` 将调用该方法并注册 `successCallback` and `failureCallback` 函数。
4. Teams 在弹出窗口的 iframe 中打开起始页。 起始页将生成随机数据、保存该数据供将来验证，并重定向到标识提供程序的终结点，如 `state` `/authorize` Azure `https://login.microsoftonline.com/<tenant ID>/oauth2/authorize` AD。 将 `<tenant id>` 你自己的租户 ID (context.tid) 。
    * 与 Teams 中的另一个应用程序身份验证流一样，起始页必须位于其列表中的域中，并且必须与登录后重定向页位于 `validDomains` 同一域中。
    * **重要** 提示：OAuth 2.0 隐式授予流调用身份验证请求中的参数，其中包含唯一的会话数据，以防止跨站点请求 `state` [伪造攻击](https://en.wikipedia.org/wiki/Cross-site_request_forgery)。 以下示例使用随机生成的数据 `state` GUID。
5. 在提供程序的网站上，用户登录并授予对选项卡的访问权限。
6. 提供程序使用访问令牌将用户定向到选项卡的 OAuth 2.0 重定向页面。
7. 该选项卡检查返回的值是否与之前保存的值匹配，并调用，这反过来调用步骤 `state` `microsoftTeams.authentication.notifySuccess()` `successCallback` 3 中注册的函数。
8. Teams 关闭弹出窗口。
9. 选项卡显示配置 UI 或刷新或重新加载选项卡内容，具体取决于用户从何处开始。

## <a name="treat-tab-context-as-hints"></a>将选项卡上下文视为提示

尽管选项卡上下文提供了有关用户的有用信息，但请勿使用此信息对用户进行身份验证，无论是作为选项卡内容 URL 的 URL 参数获取，还是通过调用 Microsoft Teams 客户端 SDK 中的函数。 `microsoftTeams.getContext()` 恶意参与者可能会使用自己的参数调用您的选项卡内容 URL，模拟 Microsoft Teams 的网页可能会加载 iframe 中的选项卡内容 URL，并自行将数据返回到 `getContext()` 函数。 你应该将选项卡上下文中的标识相关信息视为提示，并验证这些信息，然后再使用。 请参阅从弹出窗口 [导航到授权页中的注释](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)。

## <a name="samples"></a>示例

有关显示选项卡身份验证过程的示例代码，请参阅：

* [Microsoft Teams 选项卡身份验证示例 (节点) ](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)
* [Microsoft Teams 选项卡身份验证示例 (C#) ](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)

## <a name="more-details"></a>更多详细信息

有关面向 Azure Active Directory 的选项卡身份验证的详细实现演练，请参阅：

* [在 Microsoft Teams 选项卡中对用户进行身份验证](~/tabs/how-to/authentication/auth-tab-AAD.md)
* [无提示的身份验证](~/tabs/how-to/authentication/auth-silent-AAD.md)
