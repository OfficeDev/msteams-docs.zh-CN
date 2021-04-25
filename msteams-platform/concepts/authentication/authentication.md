---
title: 验证应用用户
description: 介绍 Teams 中的身份验证以及如何在应用中使用它
ms.topic: conceptual
keywords: teams 身份验证 OAuth SSO AAD
ms.openlocfilehash: 33ef0c55842c495ca44495bc0653a47b147ebbfc
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2021
ms.locfileid: "51995993"
---
# <a name="authenticate-users-in-microsoft-teams"></a>在 Microsoft Teams 中对用户进行身份验证

> [!NOTE]
> 移动客户端上基于 Web 的身份验证需要 Microsoft Teams JavaScript SDK 版本 1.4.1 或更高版本。

若要访问受 Azure Active Directory (AAD) 保护的用户信息，以及访问 Facebook 和 Twitter 等服务的数据，应用需要与这些提供商建立受信任的连接。 如果应用在用户范围内使用 Microsoft Graph API，请对用户进行身份验证以检索相应的身份验证令牌。

在 Teams 中，应用有两个不同的身份验证流。 在嵌入选项卡、配置页或任务模块的内容[](~/tabs/how-to/create-tab-pages/content-page.md)页中执行传统的基于 Web 的身份验证流。 如果应用包含对话机器人，请使用 OAuthPrompt 流和 Azure Bot Framework 的令牌服务（可选）将用户作为对话的一部分进行身份验证。

## <a name="web-based-authentication-flow"></a>基于 Web 的身份验证流

对选项卡使用基于 Web 的[](~/tabs/what-are-tabs.md)身份验证流，并选择与对话机器人[](~/bots/what-are-bots.md)或消息扩展[一起使用它](~/messaging-extensions/what-are-messaging-extensions.md)。 使用 [Web 内容页中的 Microsoft Teams JavaScript](/javascript/api/overview/msteams-client) 客户端 SDK 启用身份验证。 启用身份验证后，在选项卡、配置页或任务模块中嵌入内容页。 有关基于 Web 的身份验证流详细信息，请参阅：

* [向 Teams 机器人添加身份验证](~/bots/how-to/authentication/add-authentication.md) 介绍如何将基于 Web 的身份验证流与对话机器人一同使用。
* [选项卡中的身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md) 介绍了选项卡身份验证在 Teams 中的工作方式。 这将显示用于选项卡的典型基于 Web 的身份验证流。
* [选项卡中的 AAD](~/tabs/how-to/authentication/auth-tab-AAD.md) 身份验证介绍如何从 Teams 应用中的选项卡内连接到 AAD。
* [无提示身份验证 AAD](~/tabs/how-to/authentication/auth-silent-AAD.md) 介绍如何使用 AAD 减少应用中的登录或同意提示。
* [.Net、C#、JavaScript](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp) [或 Node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node) 提供了基于 Web 的身份验证的示例。

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>用于对话机器人的 OAuthPrompt 流

Azure Bot Framework 的 OAuthPrompt 使使用对话机器人的应用更容易进行身份验证。 使用 Azure Bot Framework 的令牌服务来帮助进行令牌缓存。

有关使用 OAuthPrompt 的信息，请参阅：

* [自动程序身份验证流概述](~/bots/how-to/authentication/auth-flow-bot.md) 介绍了身份验证在 Teams 应用中自动程序内的工作方式。 这显示了用于 Teams Web、桌面应用和移动应用上的自动程序的非基于 Web 的身份验证流。
* [自动程序](~/bots/how-to/authentication/add-authentication.md) 身份验证介绍如何将 OAuth 身份验证添加到 Teams 自动程序。

## <a name="code-sample"></a>代码示例

提供 Bot 身份验证 v3 SDK 示例。

| **示例名称** | **说明** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| 自动程序身份验证 | 此示例演示如何开始使用 Microsoft Teams 自动程序中的身份验证。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |

## <a name="configure-the-identity-provider"></a>配置标识提供程序

无论应用的身份验证流如何，配置标识提供程序以与 Teams 应用通信。 大多数示例和演练主要涉及将 AAD 用作标识提供程序。 但是，无论标识提供程序如何，概念都适用。

有关详细信息，请参阅 [配置标识提供程序](~/concepts/authentication/configure-identity-provider.md)。
