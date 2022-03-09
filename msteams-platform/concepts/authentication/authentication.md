---
title: 验证应用用户
description: 介绍Teams中的身份验证以及如何在应用中使用它
ms.topic: conceptual
ms.localizationpriority: medium
keywords: 'teams 身份验证 OAuth SSO Microsoft Azure Active Directory (Azure AD) '
ms.openlocfilehash: efc065f317d0877b3e5f158566cba6d5d095505f
ms.sourcegitcommit: 830fdc80556a5fde642850dd6b4d1b7efda3609d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/09/2022
ms.locfileid: "63399343"
---
# <a name="authenticate-users-in-microsoft-teams"></a>对用户进行身份验证Microsoft Teams

> [!Note]
> 移动客户端上基于 Web 的身份验证需要 JavaScript 客户端 SDK 的 1.4.1 Teams更高版本。

为了访问受 Azure AD 保护的用户信息，以及访问 Facebook 和 Twitter 等服务的数据，该应用与这些提供商建立了受信任的连接。 如果应用使用 Microsoft Graph用户作用域中的 API，请对用户进行身份验证以检索相应的身份验证令牌。

在Teams中，应用有两个不同的身份验证流。 在嵌入选项卡、配置页或任务模块的内容[](~/tabs/how-to/create-tab-pages/content-page.md)页中执行传统的基于 Web 的身份验证流。 如果应用包含对话机器人，请使用 OAuthPrompt 流和 Azure Bot Framework 的令牌服务（可选），在对话中对用户进行身份验证。

## <a name="web-based-authentication-flow"></a>基于 Web 的身份验证流程

对选项卡使用基于 Web 的[身份验证流，](~/tabs/what-are-tabs.md)并选择与对话机器人或消息[](~/bots/what-are-bots.md)扩展[一起使用它](~/messaging-extensions/what-are-messaging-extensions.md)。 使用 [web Microsoft Teams页面中的 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 启用身份验证。 启用身份验证后，将内容页面嵌入到选项卡、配置页面或任务模块中。 有关基于 Web 的身份验证流详细信息，请参阅：

* [Add authentication to the Teams bot](~/bots/how-to/authentication/add-authentication.md) 介绍如何将基于 Web 的身份验证流与对话机器人一同使用。
* [选项卡中的身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)介绍了选项卡身份验证在Teams。 这将显示用于选项卡的典型基于 Web 的身份验证流。
* [Azure AD中的身份验证](~/tabs/how-to/authentication/auth-tab-AAD.md)介绍如何从 Azure AD 应用中的选项卡内连接到Teams。
* [无提示Azure AD](~/tabs/how-to/authentication/auth-silent-AAD.md)描述如何使用无提示身份验证减少应用中的登录或Azure AD。
* [.Net、C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) 、 [JavaScript 或 Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) 提供了基于 Web 的身份验证的示例。

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>用于对话机器人的 OAuthPrompt 流

Azure Bot Framework OAuth Prompt 使你可以更轻松地对使用对话机器人的应用程序进行身份验证。 使用 Azure Bot Framework 的令牌服务来协助进行令牌缓存。

有关使用 OAuthPrompt 的信息，请参阅：

* [Bot authentication flow overview](~/bots/how-to/authentication/auth-flow-bot.md) describes how authentication works within a bot in the app in Teams. 这将显示一个非基于 Web 的身份验证流，用于 Teams Web、桌面应用和移动应用上的聊天机器人。
* [自动程序](~/bots/how-to/authentication/add-authentication.md)身份验证介绍如何向自动程序添加 OAuth Teams身份验证。

## <a name="code-sample"></a>代码示例

提供 Bot 身份验证 v3 SDK 示例。

| **示例名称** | **说明** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| 自动程序身份验证 | 此示例演示如何开始使用自动程序 for Microsoft Teams。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| 使用 SSO 的选项卡、聊天 (消息) 扩展 | 此示例演示 Tab、Bot 和 ME 的 SSO - 搜索、操作、linkunfurl。 |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | 不可用 |

## <a name="configure-the-identity-provider"></a>配置标识提供程序

无论应用的身份验证流如何，配置标识提供程序以与Teams通信。 大多数示例和演练主要涉及将 Azure AD用作标识提供程序。 但是，无论标识提供程序如何，概念均适用。

有关详细信息，请参阅 [配置标识提供程序](~/concepts/authentication/configure-identity-provider.md)。

## <a name="third-party-cookies-on-ios"></a>iOS 上的第三方 Cookie

iOS 14 更新后，Apple 默认阻止了所有应用的第[](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/)三方 Cookie 访问。 因此，利用第三方 Cookie 在频道或聊天选项卡和个人应用中进行身份验证的应用将无法在 iOS 客户端上完成Teams工作流。 若要符合隐私和安全要求，必须移动到基于令牌的系统或使用第一方 Cookie 进行用户身份验证工作流。

## <a name="see-also"></a>另请参阅

* [选项卡的 Microsoft Teams 身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)
* [为机器人提供单一登录支持](~/bots/how-to/authentication/auth-aad-sso-bots.md)
* [向邮件扩展添加身份验证](~/messaging-extensions/how-to/add-authentication.md)
