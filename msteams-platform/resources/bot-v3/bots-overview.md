---
title: 将机器人添加到 Microsoft Teams 应用
description: 介绍如何开始在 Microsoft Teams 中开发机器人
ms.topic: conceptual
keywords: teams 机器人开发
localization_priority: Normal
ms.date: 05/20/2018
ms.openlocfilehash: c7b719aae3a8d1b09ed8a1be7f54028fe7f2481e
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019753"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>将机器人添加到 Microsoft Teams 应用

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

构建并连接智能机器人，以便通过聊天自然地与 Microsoft Teams 用户进行交互。 或者提供一个简单的基于命令的机器人，以用作你的"命令行"界面，以便获得更广泛的 Teams 应用体验。 你可以制作一个仅通知自动程序，它可以将与用户有关的信息直接推送到频道或直接消息中。 你甚至可以引入现有的基于 Bot Framework 的机器人，并添加特定于 Teams 的支持，以让你的体验更加突出。

![机器人协助用户的示例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>您需要了解哪些信息：Bots

机器人的显示方式与你在对话中交互的其他任何团队成员一样，只是它具有一个六边形的头像图标，并且始终联机。

自动程序的行为方式有所不同，具体取决于它涉及的对话类型。 Teams 中的聊天机器人支持多种类型的 (在应用清单或 [应用中称为](~/resources/schema/manifest-schema.md)) 。

* `teams` 也称为频道对话
* `personal` 机器人和单个用户之间的对话
* `groupChat` 机器人与 2 个或多个用户之间的对话

有关详细信息 [，请参阅](~/resources/bot-v3/bot-conversations/bots-conversations.md) 与 Microsoft Teams 机器人对话。

使用 Microsoft Teams 应用，你可以使机器人成为你体验的星形，或者只是一个帮助程序。 自动程序作为更广泛的应用包的一部分进行分发，其中可以包含选项卡或消息传递[扩展等其他功能](~/messaging-extensions/what-are-messaging-extensions.md)。 [](~/tabs/what-are-tabs.md)

## <a name="bot-apis"></a>自动程序 API

Microsoft Teams 支持大多数 [Microsoft Bot Framework](https://dev.botframework.com/)。  (如果你已有一个基于 Bot Framework 的自动程序，你可以轻松调整它以在 Microsoft Teams 中工作。) 我们建议你使用 C# 或 Node.js 来利用我们的[SDK。](/microsoftteams/platform/#pivot=sdk-tools) 这些工具包拓展了基本机器人生成器 SDK 的类和方法：

* 使用专用卡片类型，如 Office 365 连接器卡
* 在活动中使用和设置特定于 Teams 的频道数据
* 处理邮件扩展请求

SDK 扩展将安装依赖项，包括 Bot Builder SDK。

* **.NET** 若要使用适用于 .NET 的自动程序生成器 SDK 的 Microsoft Teams 扩展，请在你的自动程序项目中安装 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet Visual Studio包。 对于Node.js，自 v4.6 起，BotBuilder for Microsoft Teams 功能已合并到 [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) 中。

*另请参阅* [Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

> [!IMPORTANT]
> 可以使用任何其他 Web 编程技术开发 Teams 应用并直接调用 [Bot Framework REST](/bot-framework/rest-api/bot-framework-rest-overview) API，但你必须自己执行所有令牌处理。

*Teams App Studio* 可帮助你创建和配置应用清单，并可以创建自动程序框架自动程序。 它还包含 React 控件库和交互式卡片生成器。

## <a name="outgoing-webhooks"></a>传出 webhook

传出 Webhook 允许你创建用于基本交互的简单自动程序，例如启动工作流或其他您可能需要的简单命令。 传出 Webhook 仅在你创建它们的团队中活动，并且适用于特定于公司工作流的简单流程。 有关详细信息[，请参阅传出 Webhook。](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

## <a name="build-a-great-teams-bot"></a>构建出色的 Teams 机器人

以下主题将指导你完成为 Teams 创建出色的机器人的过程。

* [创建自动程序](~/resources/bot-v3/bots-create.md)：利用 Bot Framework 团队提供的出色的工具、文档和社区。
* [与机器人交谈](~/resources/bot-v3/bot-conversations/bots-conversations.md)：添加基本对话流并利用特定于频道的功能。 如果使用 .NET 或 Node.js 开发，请使用自动程序生成器 SDK 的扩展来简化你的工作。
* [在机器人中使用卡片](~/resources/bot-v3/bots-cards.md) 设计卡片以进行通信并接受用户响应。
* [响应机器人事件](~/resources/bot-v3/bots-notifications.md)。
* [仅通知机器人](~/resources/bot-v3/bots-notification-only.md) 使用机器人为应用发送通知。
* [获取上下文](~/resources/bot-v3/bots-context.md) 获取有关用户的信息。
* [自动程序菜单](~/resources/bot-v3/bots-menus.md) 使用机器人中的菜单。
* [机器人和文件](~/resources/bot-v3/bots-files.md) 从机器人发送和接收文件。
* [将选项卡与机器人一同使用](~/resources/bot-v3/bots-with-tabs.md) 使选项卡和机器人协同工作。
* [测试机器人](~/resources/bot-v3/bots-test.md)：添加用于个人或团队对话的自动程序以查看其运行。
