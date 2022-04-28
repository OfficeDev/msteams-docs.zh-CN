---
title: 将机器人添加到Microsoft Teams应用
description: 介绍如何开始在 Microsoft Teams 中开发机器人
ms.topic: conceptual
keywords: 团队机器人开发
ms.localizationpriority: medium
ms.date: 05/20/2018
ms.openlocfilehash: 164c8e518e38d506bbaf80f59edebfb18c07acec
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103423"
---
# <a name="add-bots-to-microsoft-teams-apps"></a>将机器人添加到Microsoft Teams应用

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

构建和连接智能机器人，通过聊天自然地与Microsoft Teams用户交互。 或者提供一个简单的基于命令的机器人，用作更广泛的Teams应用体验的“命令行”接口。 可以创建仅限通知的机器人，该机器人可直接在频道或直接消息中将与用户相关的信息推送到用户。 甚至可以引入现有的基于 Bot Framework 的机器人，并添加特定于Teams的支持，使体验更加丰富。

> [!IMPORTANT]
> 目前，机器人在政府社区云 (GCC) 中可用，但在GCC-High和国防部 (DOD) 中不可用。

![帮助用户的机器人示例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a>需要了解的内容：机器人

机器人与你在对话中交互的任何其他团队成员一样出现，只不过它具有六边形头像图标，并且始终处于联机状态。

机器人的行为不同，具体取决于它所涉及的聊天类型。 Teams中的机器人支持[应用清单](~/resources/schema/manifest-schema.md)中称为范围的几种类型的对话。

* `teams` 也称为频道对话。
* `personal` 机器人与单个用户之间的对话。
* `groupChat` 机器人与 2 个或更多用户之间的对话。

有关详细信息，请参阅[与Microsoft Teams机器人的对话](~/resources/bot-v3/bot-conversations/bots-conversations.md)。

使用Microsoft Teams应用，可以使机器人成为你体验的明星，或者只是帮助程序。 机器人作为更广泛的应用包的一部分进行分发，其中可以包括其他功能，如 [选项卡](~/tabs/what-are-tabs.md) 或 [消息扩展](~/messaging-extensions/what-are-messaging-extensions.md)。

## <a name="bot-apis"></a>机器人 API

Microsoft Teams支持大部分[Microsoft Bot Framework](https://dev.botframework.com/)。  (如果已有一个基于 Bot Framework 的机器人，则可以轻松地将其适应Microsoft Teams.) 建议使用 C# 或Node.js来利用我们的 [SDK](/microsoftteams/platform/#pivot=sdk-tools)。 这些工具包拓展了基本机器人生成器 SDK 的类和方法：

* 使用专用卡片类型，例如Office 365连接器卡。
* 在活动上使用和设置特定Teams通道数据。
* 处理消息扩展请求。

SDK 扩展安装依赖项，包括 Bot Builder SDK。

* **.NET** 若要使用 Bot Builder SDK for .NET 的Microsoft Teams扩展，[请在Visual Studio项目中安装 Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet 包。 为了Node.js开发，BotBuilder for Microsoft Teams 功能已合并到 [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) 中，截至 v4.6。

> [!IMPORTANT]
> 可以在任何其他 Web 编程技术中开发Teams应用，并直接调用 [Bot Framework REST API](/bot-framework/rest-api/bot-framework-rest-overview)，但必须自行执行所有令牌处理。

*Teams App Studio* 可帮助你创建和配置应用清单，并可为你创建 Bot Framework 机器人。 它还包含React控件库和交互式卡片生成器。

## <a name="outgoing-webhooks"></a>传出 webhook

通过传出 Webhook，可以创建用于基本交互的简单机器人，例如启动工作流或可能需要的其他简单命令。 传出 Webhook 仅存在于你创建它们的团队中，适用于特定于公司工作流的简单流程。 有关详细信息，请参阅 [传出 Webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)。

## <a name="build-a-great-teams-bot"></a>生成出色的Teams机器人

以下主题将指导你完成创建适用于Teams的出色机器人的过程：

* [创建机器人](~/resources/bot-v3/bots-create.md)：利用 Bot Framework 团队提供的出色工具、文档和社区。
* [与机器人交谈](~/resources/bot-v3/bot-conversations/bots-conversations.md)：添加基本对话流并利用特定于通道的功能。 如果在 .NET 或 Node.js 中进行开发，请使用 Bot Builder SDK 的扩展来简化工作。
* [在机器人中使用卡](~/resources/bot-v3/bots-cards.md)片：设计卡来通信和接受用户响应。
* [响应机器人事件](~/resources/bot-v3/bots-notifications.md)
* [仅通知机器人](~/resources/bot-v3/bots-notification-only.md)：使用机器人为应用发送通知。
* [获取上下文](~/resources/bot-v3/bots-context.md)：获取有关用户的信息。
* [机器人菜单](~/resources/bot-v3/bots-menus.md)：在机器人中使用菜单。
* [机器人和文件](~/resources/bot-v3/bots-files.md)：从机器人发送和接收文件。
* [将选项卡与机器人配合使用](~/resources/bot-v3/bots-with-tabs.md)：使选项卡和机器人协同工作。
* [测试机器人](~/resources/bot-v3/bots-test.md)：添加机器人以进行个人或团队对话，以查看其运行情况。

## <a name="see-also"></a>另请参阅

[Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
