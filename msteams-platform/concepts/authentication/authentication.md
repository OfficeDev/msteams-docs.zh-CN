---
title: 验证应用用户
description: 介绍 Teams 中的身份验证以及如何在应用中使用它
ms.topic: conceptual
keywords: teams 身份验证 OAuth SSO AAD
ms.openlocfilehash: 6ddcd8a9e847d9216b7e2dcc12733a6cd413b48e
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014290"
---
# <a name="authenticating-users-in-microsoft-teams"></a>在 Microsoft Teams 中验证用户

> [!Note]
> 移动客户端上基于 Web 的身份验证需要 Teams JavaScript SDK 版本 1.4.1 或更高版本。

为了让你的应用访问受 Azure Active Directory 保护的用户信息，以及访问来自其他服务（如 Facebook 和 Twitter）的数据，你的应用必须建立与这些提供商的信任连接。 如果你的应用需要在用户范围内使用 Microsoft Graph API，你还需要对用户进行身份验证以检索相应的身份验证令牌。

在 Microsoft Teams 中，你的应用有两个不同的身份验证流程可以利用。 您可以在嵌入选项卡、配置页或任务模块的内容页中[](~/tabs/how-to/create-tab-pages/content-page.md)执行传统的基于 Web 的身份验证流。 如果你的应用包含对话机器人，可以使用 OAuthPrompt 流 (（可选）和 Azure Bot Framework 的令牌服务) 在对话中对用户进行身份验证。

## <a name="web-based-authentication-flow"></a>基于 Web 的身份验证流

你需要对选项卡使用基于 Web 的身份验证流，并且[](~/tabs/what-are-tabs.md)可以选择与对话机器人或消息扩展一起[](~/bots/what-are-bots.md)[使用它](~/messaging-extensions/what-are-messaging-extensions.md)。 你将使用 Web 内容页中的 [Microsoft Teams JavaScript](/javascript/api/overview/msteams-client) 客户端 SDK 启用身份验证，然后将该内容页嵌入选项卡、配置页或任务模块中。 如果要将基于 Web 的身份验证流与对话机器人一同使用，则需要将任务模块与自动程序 [一同使用](~/task-modules-and-cards/task-modules/task-modules-bots.md)。

* [选项卡中的身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md) 介绍了选项卡身份验证在 Teams 中的工作方式。 这显示了用于选项卡的典型基于 Web 的身份验证流。
* [选项卡中的 Azure AD](~/tabs/how-to/authentication/auth-tab-AAD.md) 身份验证描述如何从 Teams 应用中的选项卡内连接到 Azure Active Directory。
* [Azure AD (无 ](~/tabs/how-to/authentication/auth-silent-AAD.md) 提示) 介绍了如何使用 Azure Active Directory 减少应用中的登录/同意提示。
* [dotnet/C# 或](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) [JavaScript/Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>用于对话机器人的 OAuthPrompt 流

Azure Bot Framework 的 OAuthPrompt 使使用对话机器人的应用更容易进行身份验证。 您还可以利用 Azure Bot Framework 的令牌服务来帮助进行令牌缓存。

有关使用 OAuthPrompt 的信息，请参阅：

* [自动程序身份验证流概述](~/bots/how-to/authentication/auth-flow-bot.md) 介绍了身份验证在 Teams 应用中自动程序内的工作方式。 这显示了一个非基于 Web 的身份验证流，用于所有版本的 Teams (Web、桌面应用和移动应用上的) 
* [自动程序身份验证](~/bots/how-to/authentication/add-authentication.md)
* 在[dotnet (C#](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)或[JavaScript/) ](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) v3 SDK Node.js

## <a name="configure-your-identity-provider"></a>配置标识提供程序

无论你的应用使用哪种身份验证流 (你甚至可能同时使用这两) ，你都需要配置标识提供程序以与 Teams 应用通信。 你将在此处找到的大多数示例和演练主要涉及将 Azure Active Directory 用作标识提供程序。 但是，无论使用哪个标识提供程序，概念都适用。

有关详细信息，请参阅 [配置标识提供程序](~/concepts/authentication/configure-identity-provider.md)
