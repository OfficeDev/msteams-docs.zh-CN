---
title: 向 Microsoft 团队应用程序添加 bot
description: 介绍如何开始在 Microsoft 团队中开发 bot
keywords: 团队 bot 开发
ms.date: 05/20/2018
ms.openlocfilehash: 58221e94520ef6e748bbd6c17fa7933813874c56
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "42228050"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>向 Microsoft 团队应用程序添加 bot

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

构建和连接智能机器人，以便通过聊天自然与 Microsoft 团队用户交互。 或者提供一个简单的基于命令的 bot，用作您更广泛的团队应用体验的 "命令行" 界面。 您可以创建仅通知 bot，这可以在频道或直接消息中直接将与用户相关的信息推送到他们。 您甚至可以引入现有的基于 Bot 框架的 bot 并添加团队特定的支持，以实现您的体验的亮点。

![帮助用户的机器人示例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>您需要了解的内容： Bot

与在对话中交互的任何其他团队成员类似，不同之处在于它具有一个六角头像图标，并且始终处于联机状态。

Bot 的行为有所不同，具体取决于所涉及的对话类型。 团队中的 bot 支持几种对话（在[应用程序清单](~/resources/schema/manifest-schema.md)中称为 "作用域"）。

* `teams`也称为频道对话
* `personal`Bot 和单个用户之间的对话
* `groupChat`机器人和2个或更多用户之间的对话

有关详细信息，请参阅[与 Microsoft 团队 bot 进行对话](~/resources/bot-v3/bot-conversations/bots-conversations.md)。

在 Microsoft 团队应用程序中，你可以将 bot 设置为你的体验的明星或仅提供帮助者。 将 bot 作为更广泛的应用程序包的一部分进行分发，其中可能包括[选项卡](~/tabs/what-are-tabs.md)或[邮件扩展](~/messaging-extensions/what-are-messaging-extensions.md)等其他功能。

## <a name="bot-apis"></a>Bot Api

Microsoft 团队支持大多数[Microsoft Bot 框架](https://dev.botframework.com/)。 （如果已经有一个基于 Bot 框架的 bot，可以轻松地将其调整为在 Microsoft 团队中工作。）我们建议您使用 c # 或 node.js 来利用我们的[sdk](/microsoftteams/platform/#pivot=sdk-tools)。 这些包扩展了基本的 Bot 生成器 SDK 类和方法：

* 使用专用的卡片类型，如 Office 365 连接器卡
* 使用和设置针对活动的特定于团队的频道数据
* 处理邮件扩展请求

SDK 扩展安装了依赖项，包括机器人生成器 SDK。

* **.Net**若要使用适用于 .NET 的机器人生成器 SDK 的 Microsoft 团队扩展，请在 Visual Studio 项目中安装 ".[团队](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)" NuGet 包。 对于 node.js 开发，BotBuilder for Microsoft 团队功能已并入到来自 v4.0 的[Bot 框架 SDK](https://github.com/microsoft/botframework-sdk)中。

*另请参阅* [Bot 框架示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

> [!IMPORTANT]
> 您可以在任何其他 web 编程技术中开发团队应用程序，并直接调用[Bot 框架 REST api](/bot-framework/rest-api/bot-framework-rest-overview) ，但您必须自己执行所有令牌处理。

*团队应用程序 Studio*可帮助您创建和配置应用程序清单，并可为您创建您的 Bot 框架 Bot。 它还包含响应控制库和交互式卡片生成器。

## <a name="outgoing-webhooks"></a>传出 webhook

通过传出 webhook，您可以创建简单的 bot 来实现基本交互，例如启动关闭工作流或您可能需要的其他简单命令。 传出 webhook 仅在您创建它们的团队中实时发布，适用于特定于贵公司的工作流的简单流程。 有关详细信息，请参阅[出局 webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md) 。

## <a name="build-a-great-teams-bot"></a>构建一个出色的团队 bot

以下主题将指导您完成为团队创建出色的 bot 的过程。

* [创建机器人](~/resources/bot-v3/bots-create.md)：充分利用由 bot 框架团队提供的强大工具、文档和社区。
* [与你的 Bot 对话](~/resources/bot-v3/bot-conversations/bots-conversations.md)：添加基本对话流和利用特定于频道的功能。 如果是在 .NET 或 node.js 中进行开发，请使用机器人生成器 SDK 的扩展来简化您的工作。
* [在你的 bot 中使用卡片](~/resources/bot-v3/bots-cards.md)设计卡片以传达和接受用户响应。
* [响应 bot 事件](~/resources/bot-v3/bots-notifications.md)。
* [仅通知 bot](~/resources/bot-v3/bots-notification-only.md)使用 bot 向您的应用程序发送通知。
* [获取上下文](~/resources/bot-v3/bots-context.md)获取有关用户的信息。
* [Bot 菜单](~/resources/bot-v3/bots-menus.md)在 bot 中使用菜单。
* [Bot 和文件](~/resources/bot-v3/bots-files.md)从 bot 发送和接收文件。
* [使用带 bot 的选项卡](~/resources/bot-v3/bots-with-tabs.md)使选项卡和 bot 协同工作。
* [测试你的 bot](~/resources/bot-v3/bots-test.md)：添加你的个人或团队对话的 bot 以查看其操作。
