---
title: 向应用添加Microsoft Teams程序
description: 介绍如何开始在 Microsoft Teams
ms.topic: conceptual
keywords: teams 机器人开发
ms.localizationpriority: medium
ms.date: 05/20/2018
ms.openlocfilehash: afa83478ee478d74dbdedb5cd805719fc8434070
ms.sourcegitcommit: 6573881f7e69d8e5ec8861f54df84e7d519f0511
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/04/2021
ms.locfileid: "60096547"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>向应用添加Microsoft Teams程序

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

构建并连接智能机器人，以便Microsoft Teams用户自然地交互。 或者提供一个简单的基于命令的自动程序，以用作你的"命令行"界面，以便Teams应用体验。 你可以创建一个仅通知自动程序，它可以将与用户有关的信息直接推送到频道或直接消息中。 你甚至可以引入现有的基于 Bot Framework 的机器人，并添加Teams特定支持，以让你的体验大放异彩。

> [!IMPORTANT]
> 目前，自动程序在 政府社区云 (GCC) 中可用，但在 doD GCC-High 和国防部 (中) 。

![机器人协助用户的示例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>您需要了解哪些信息：Bots

机器人的显示方式与你在对话中交互的其他任何团队成员一样，只是它具有一个六边形的头像图标，并且始终联机。

自动程序的行为方式有所不同，具体取决于它涉及的对话类型。 聊天机器人Teams应用程序清单中称为作用域的多种[对话](~/resources/schema/manifest-schema.md)。

* `teams` 也称为频道对话。
* `personal` 机器人和单个用户之间的对话。
* `groupChat` 机器人与 2 个或多个用户之间的对话。

有关详细信息，请参阅与自动程序[Microsoft Teams对话](~/resources/bot-v3/bot-conversations/bots-conversations.md)。

通过Microsoft Teams应用，你可以使机器人成为你体验的星形，或者只是一个帮助程序。 自动程序作为更广泛的应用包的一部分进行分发，其中可以包含选项卡或消息传递扩展[等其他功能](~/messaging-extensions/what-are-messaging-extensions.md)。 [](~/tabs/what-are-tabs.md)

## <a name="bot-apis"></a>自动程序 API

Microsoft Teams支持[大多数Microsoft Bot Framework。](https://dev.botframework.com/)  (如果你已有一个基于 Bot Framework 的机器人，你可以轻松调整它以在 Microsoft Teams.) 我们建议你使用 C# 或 Node.js 来利用我们的[SDK。](/microsoftteams/platform/#pivot=sdk-tools) 这些工具包拓展了基本机器人生成器 SDK 的类和方法：

* 使用专用卡类型，如 Office 365 连接器卡。
* 使用和设置Teams特定频道数据。
* 处理邮件扩展请求。

SDK 扩展将安装依赖项，包括 Bot Builder SDK。

* **.NET** 若要使用适用于 .NET Microsoft Teams聊天机器人生成器 SDK 的 Microsoft Teams 扩展，请在你的 Visual Studio 项目中安装 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet程序包。 对于Node.js，botBuilder for Microsoft Teams 功能自 v4.6 起已合并到[Bot Framework SDK](https://github.com/microsoft/botframework-sdk)中。

> [!IMPORTANT]
> 可以使用任何其他Teams技术开发应用程序并直接调用[Bot Framework REST](/bot-framework/rest-api/bot-framework-rest-overview) API，但你必须自己执行所有令牌处理。

*Teams App Studio* 可帮助你创建和配置应用清单，并可以创建自动程序框架自动程序。 它还包含一个React库和交互式卡片生成器。 

## <a name="outgoing-webhooks"></a>传出 webhook

传出 Webhook 允许你创建用于基本交互的简单自动程序，例如启动工作流或其他您可能需要的简单命令。 传出 Webhook 仅在你创建它们的团队中活动，并且适用于特定于公司工作流的简单流程。 有关详细信息，请参阅传出[Webhook。](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

## <a name="build-a-great-teams-bot"></a>构建出色的自动Teams程序

以下主题将指导你完成为用户创建出色的自动程序Teams：

* [创建自动程序](~/resources/bot-v3/bots-create.md)：利用 Bot Framework 团队提供的出色的工具、文档和社区。
* [与机器人交谈](~/resources/bot-v3/bot-conversations/bots-conversations.md)：添加基本对话流并利用特定于频道的功能。 如果使用 .NET 或 Node.js 开发，请使用 Bot Builder SDK 的扩展来简化你的工作。
* [在机器人中使用卡片](~/resources/bot-v3/bots-cards.md)：设计卡片以传达并接受用户响应。
* [响应机器人事件](~/resources/bot-v3/bots-notifications.md)
* [仅通知机器人](~/resources/bot-v3/bots-notification-only.md)：使用机器人为应用发送通知。
* [获取上下文](~/resources/bot-v3/bots-context.md)：获取有关用户的信息。
* [自动程序](~/resources/bot-v3/bots-menus.md)菜单：使用机器人中的菜单。
* [机器人和文件](~/resources/bot-v3/bots-files.md)：从机器人发送和接收文件。
* [将选项卡与机器人一同使用](~/resources/bot-v3/bots-with-tabs.md)：使选项卡和机器人协同工作。
* [测试机器人](~/resources/bot-v3/bots-test.md)：添加用于个人或团队对话的自动程序，以查看其是否运行。

## <a name="see-also"></a>另请参阅

[Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。