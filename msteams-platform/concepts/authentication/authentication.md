---
title: 验证应用用户
description: 介绍Teams中的身份验证以及如何在应用中使用它
ms.topic: conceptual
ms.localizationpriority: medium
keywords: teams 身份验证 OAuth SSO AAD
ms.openlocfilehash: 1705e85843fbe8d75af978da8baff081b58c6ca1
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720306"
---
# <a name="authenticate-users-in-microsoft-teams"></a>对用户进行身份验证Microsoft Teams

> [!Note]
> 移动客户端上基于 Web 的身份验证需要 JavaScript 客户端 SDK 的 1.4.1 Teams更高版本。

为了访问受 Azure Active Directory (AAD) 保护的用户信息以及访问 Facebook 和 Twitter 等服务的数据，该应用与这些提供商建立了受信任的连接。 如果应用使用 Microsoft Graph用户作用域中的 API，请对用户进行身份验证以检索相应的身份验证令牌。

在Teams中，应用有两个不同的身份验证流。 在嵌入选项卡、配置页或任务模块的内容[](~/tabs/how-to/create-tab-pages/content-page.md)页中执行传统的基于 Web 的身份验证流。 如果应用包含对话机器人，请使用 OAuthPrompt 流和 Azure Bot Framework 的令牌服务（可选），在对话中对用户进行身份验证。

## <a name="web-based-authentication-flow"></a>基于 Web 的身份验证流程

对选项卡使用基于 Web 的[](~/tabs/what-are-tabs.md)身份验证流，并选择与对话机器人[](~/bots/what-are-bots.md)或消息[扩展一起使用它](~/messaging-extensions/what-are-messaging-extensions.md)。 使用 web Microsoft Teams页面中的[JavaScript](/javascript/api/overview/msteams-client)客户端 SDK 启用身份验证。 启用身份验证后，将内容页面嵌入到选项卡、配置页面或任务模块中。 有关基于 Web 的身份验证流详细信息，请参阅：

* [Add authentication to the Teams bot](~/bots/how-to/authentication/add-authentication.md)介绍如何将基于 Web 的身份验证流与对话机器人一同使用。
* [选项卡中的身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)介绍了选项卡身份验证在Teams。 这将显示用于选项卡的典型基于 Web 的身份验证流。
* [AAD中的身份验证](~/tabs/how-to/authentication/auth-tab-AAD.md)介绍如何从 AAD 应用中的选项卡内连接到Teams。
* [无提示AAD](~/tabs/how-to/authentication/auth-silent-AAD.md)描述如何使用无提示身份验证减少应用中的登录或AAD。
* [.Net 或 C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) [JavaScript 或 Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) 提供了基于 Web 的身份验证的示例。

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>用于对话机器人的 OAuthPrompt 流

Azure Bot Framework OAuth Prompt 使你可以更轻松地对使用对话机器人的应用程序进行身份验证。 使用 Azure Bot Framework 的令牌服务来协助进行令牌缓存。

有关使用 OAuthPrompt 的信息，请参阅：

* [自动程序身份验证流概述](~/bots/how-to/authentication/auth-flow-bot.md)介绍了身份验证在 Teams 应用中的自动程序Teams。 这显示了用于在 Web、桌面应用和移动应用Teams聊天机器人的非基于 Web 的身份验证流。
* [自动程序](~/bots/how-to/authentication/add-authentication.md)身份验证介绍如何向自动程序添加 OAuth Teams身份验证。

## <a name="code-sample"></a>代码示例

提供 Bot 身份验证 v3 SDK 示例。

| **示例名称** | **说明** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| 自动程序身份验证 | 此示例演示如何在自动程序 for Microsoft Teams 中开始使用身份验证。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| 选项卡、聊天机器人和消息传递扩展 (ME) SSO | 此示例演示 Tab、Bot 和 ME 的 SSO - 搜索、操作、linkunfurl。 |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | 不可用 |


## <a name="configure-the-identity-provider"></a>配置标识提供程序

无论应用的身份验证流如何，配置标识提供程序以与Teams通信。 大多数示例和演练主要处理将 AAD用作标识提供程序。 但是，无论标识提供程序如何，概念均适用。 

有关详细信息，请参阅 [配置标识提供程序](~/concepts/authentication/configure-identity-provider.md)。

## <a name="third-party-cookies-on-ios"></a>iOS 上的第三方 Cookie

iOS 14 更新后，Apple 默认阻止[](https://webkit.org/blog/10218/full-third-party-cookie-blocking-and-more/)了所有应用的第三方 Cookie 访问。 因此，利用第三方 Cookie 在频道或聊天选项卡和个人应用中进行身份验证的应用将无法在 iOS 客户端上完成Teams工作流。 若要符合隐私和安全要求，必须移动到基于令牌的系统或使用第一方 Cookie 进行用户身份验证工作流。
