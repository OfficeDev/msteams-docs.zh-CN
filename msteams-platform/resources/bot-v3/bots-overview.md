---
title: 将机器人添加到 Microsoft Teams 应用
description: 介绍如何开始在 Microsoft Teams 中开发机器人
ms.topic: conceptual
keywords: teams 机器人开发
ms.date: 05/20/2018
ms.openlocfilehash: 226340500f59754d603f21b7868eecab38f942af
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014402"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>将机器人添加到 Microsoft Teams 应用

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

构建并连接智能机器人，以便通过聊天自然地与 Microsoft Teams 用户进行交互。 或者提供一个简单的基于命令的自动程序，以用作更广泛的 Teams 应用体验的"命令行"界面。 你可以创建一个仅通知自动程序，它可以将与用户有关的信息直接推送到频道或直接消息中。 你甚至可以引入现有的基于 Bot Framework 的机器人并添加特定于 Teams 的支持，以让你的体验大放异彩。

![帮助用户的机器人示例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>你需要了解的：聊天机器人

机器人的显示方式与你在对话中交互的其他任何团队成员一样，只是有一个六边形的头像图标，并且始终联机。

自动程序的行为有所不同，具体取决于它涉及的对话类型。 Teams 中的机器人支持多种对话 (在应用[清单中称为) 。](~/resources/schema/manifest-schema.md)

* `teams` 也称为频道对话
* `personal` 自动程序与单个用户之间的对话
* `groupChat` 机器人与 2 个或多个用户的对话

有关详细信息 [，请参阅与 Microsoft Teams 自动程序](~/resources/bot-v3/bot-conversations/bots-conversations.md) 对话。

借助 Microsoft Teams 应用，你可以使机器人成为你体验的星形，或只是一个帮助程序。 机器人作为更广泛的应用包的一部分进行分发，其中可以包含其他功能，如[选项卡或](~/tabs/what-are-tabs.md)[消息传递扩展](~/messaging-extensions/what-are-messaging-extensions.md)。

## <a name="bot-apis"></a>自动程序 API

Microsoft Teams 支持大多数[Microsoft Bot Framework。](https://dev.botframework.com/)  (如果你已经有一个基于 Bot Framework 的机器人，你可以轻松调整它以在 Microsoft Teams 中工作。) 我们建议你使用 C# 或 Node.js 来利用[SDK。](/microsoftteams/platform/#pivot=sdk-tools) 这些包扩展了基本 Bot Builder SDK 类和方法：

* 使用专用卡类型，如 Office 365 连接器卡
* 在活动中使用和设置特定于 Teams 的频道数据
* 处理邮件扩展请求

SDK 扩展将安装依赖项，包括 Bot Builder SDK。

* **.NET** 若要将 Microsoft Teams 扩展用于适用于 .NET 的 Bot Builder SDK，请在您的项目安装 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet Visual Studio包。 对于Node.js，自 v4.6 起，适用于 Microsoft Teams 的 BotBuilder 功能已合并到 [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) 中。

*另请参阅* [Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

> [!IMPORTANT]
> 可以使用任何其他 Web 编程技术开发 Teams 应用并直接调用 [Bot Framework REST API，](/bot-framework/rest-api/bot-framework-rest-overview) 但你必须自己执行所有令牌处理。

*Teams App Studio* 可帮助你创建和配置应用清单，并可以创建自动程序框架自动程序。 它还包含 React 控件库和交互式卡片生成器。

## <a name="outgoing-webhooks"></a>传出 Webhook

传出 Webhook 允许你创建用于基本交互的简单自动程序，例如启动工作流或其他您可能需要的简单命令。 传出 Webhook 仅在您创建的团队中活动，用于特定于公司工作流的简单流程。 有关详细信息[，请参阅传出 Webhook。](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

## <a name="build-a-great-teams-bot"></a>构建出色的 Teams 机器人

以下主题将指导你完成为 Teams 创建出色的自动程序的过程。

* [创建自动程序](~/resources/bot-v3/bots-create.md)：利用 Bot Framework 团队提供的出色的工具、文档和社区。
* [与机器人交谈](~/resources/bot-v3/bot-conversations/bots-conversations.md)：添加基本对话流并利用特定于频道的功能。 如果使用 .NET 或 Node.js进行开发，请使用自动程序生成器 SDK 的扩展来简化工作。
* [在机器人中使用卡片](~/resources/bot-v3/bots-cards.md) 设计卡片以传达并接受用户响应。
* [响应机器人事件](~/resources/bot-v3/bots-notifications.md)。
* [仅通知机器人](~/resources/bot-v3/bots-notification-only.md) 使用机器人为应用发送通知。
* [获取上下文](~/resources/bot-v3/bots-context.md) 获取有关用户的信息。
* [自动程序菜单](~/resources/bot-v3/bots-menus.md) 使用机器人中的菜单。
* [机器人和文件](~/resources/bot-v3/bots-files.md) 从机器人发送和接收文件。
* [将选项卡与机器人一同使用](~/resources/bot-v3/bots-with-tabs.md) 使选项卡和机器人协同工作。
* [测试机器人](~/resources/bot-v3/bots-test.md)：为个人对话或团队对话添加自动程序以查看其运行。
