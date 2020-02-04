---
title: 对团队中的用户进行身份验证
description: 描述团队中的身份验证以及如何在应用程序中使用
keywords: 团队身份验证 OAuth SSO AAD
ms.openlocfilehash: d3ae57d9937c6794fb743b44ca8210a5afd181bf
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673114"
---
# <a name="authentication-in-teams"></a>团队中的身份验证

> [!Note]
> 在移动客户端上基于 Web 的身份验证需要团队 JavaScript SDK 的1.4.1 或更高版本。

为了让您的应用程序能够访问受 Azure Active Directory 保护的用户信息，以及从其他服务（如 Facebook 和 Twitter）访问数据，您的应用程序必须与这些提供程序建立受信任的连接。 如果您的应用程序需要在用户作用域中使用 Microsoft Graph Api，您还需要对用户进行身份验证以检索相应的身份验证令牌。

在 Microsoft 团队中，有两个不同的身份验证流可供您的应用程序利用。 您可以在嵌入在选项卡、配置页或任务模块中的[内容页](~/tabs/how-to/create-tab-pages/content-page.md)中执行传统的基于 web 的身份验证流。 如果您的应用程序包含对话的 bot，则可以使用 OAuthPrompt 流（也可以选择使用 Azure Bot 框架的令牌服务）在对话过程中对用户进行身份验证。

## <a name="web-based-authentication-flow"></a>基于 Web 的身份验证流

您需要对[选项卡](~/tabs/what-are-tabs.md)使用基于 web 的身份验证流，并且可以选择将其与[对话 bot](~/bots/what-are-bots.md)或[邮件扩展](~/messaging-extensions/what-are-messaging-extensions.md)一起使用。 您将使用 web 内容页中的[Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)启用身份验证，然后将该内容页嵌入到选项卡、配置页或任务模块中。 如果要将基于 web 的身份验证流与对话机器人配合使用，则需要将[任务模块与 bot 结合使用](~/task-modules-and-cards/task-modules/task-modules-bots.md)。

* [选项卡中的身份验证流](~/tabs/how-to/authentication/auth-flow-tab.md)介绍了 tab 身份验证在团队中的工作方式。 这显示了用于选项卡的典型的基于 web 的身份验证流。
* [选项卡中的 AZURE AD 身份验证](~/tabs/how-to/authentication/auth-tab-AAD.md)介绍了如何从团队中应用程序的选项卡中连接到 Azure Active Directory。
* [无提示身份验证（AZURE AD）](~/tabs/how-to/authentication/auth-silent-AAD.md)介绍如何使用 Azure Active Directory 减少应用中的登录/同意提示。
* [Dotnet/c #](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp)或[JavaScript/node.js](https://github.com/OfficeDev/microsoft-teams-sample-complete-node)中的基于 Web 的身份验证

## <a name="the-oauthprompt-flow-for-conversational-bots"></a>对话 bot 的 OAuthPrompt 流

Azure Bot 框架的 OAuthPrompt 使使用会话 bot 的应用程序更易于进行身份验证。 你也可以利用 Azure Bot 框架的令牌服务来协助令牌缓存。

有关使用 OAuthPrompt 的详细信息，请参阅：

* [Bot 身份验证流程概述](~/bots/how-to/authentication/auth-flow-bot.md)介绍了如何在团队中的应用程序中的 Bot 中处理身份验证。 这显示了一个非基于 web 的身份验证流，用于所有版本的团队（web、桌面应用程序和移动应用）上的 bot
* [机器人身份验证](~/bots/how-to/authentication/add-authentication.md)
* [Dotnet/c #](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)或[JavaScript/node.js](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth)中的 Bot 身份验证（v3 SDK）示例

## <a name="configure-your-identity-provider"></a>配置您的标识提供程序

无论您的应用程序使用的是哪种身份验证流（甚至您可能同时使用这两种），您都需要将标识提供程序配置为与您的团队应用程序进行通信。 你将在此处找到的大部分示例和演练主要是使用 Azure Active Directory 作为你的标识提供程序。 但是，无论您使用哪种标识提供程序，都将应用这些概念。

有关详细信息，请参阅[配置标识提供程序](~/concepts/authentication/configure-identity-provider.md)
