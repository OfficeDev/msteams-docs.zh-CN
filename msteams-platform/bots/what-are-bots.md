---
title: 什么是对话 bot？
author: clearab
description: Microsoft 团队中的会话 bot 概述。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 7bde886b67788a355181c83287d999a3bfb9727a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673117"
---
# <a name="what-are-conversational-bots"></a>什么是对话 bot？

会话 bot 使用户能够通过文本、交互式卡片和任务模块与 web 服务进行交互。 它们的灵活性非常灵活—会话间的 bot 可用于处理几个简单的命令或复杂、人工智能的智能化和自然语言处理虚拟助理。 它们可以是大型应用程序的一个方面，也可以完全独立。

下面的 GIF 显示了用户使用文本和交互式卡片同时在一对一聊天中与 bot 聊天。 查找卡片、文本和任务模块的正确组合是创建有用的 bot 的关键所在。 别忘了，机器人要远不止是文本！

![FAQ 加 gif](~/assets/images/FAQPlusEndUser.gif)

## <a name="what-tasks-are-best-handled-by-bots"></a>哪些任务最适合通过 bot 处理？

Microsoft 团队中的 bot 可以是一对一对话、组聊天或团队中的频道的一部分。 每个范围都将为您的会话 bot 提供独特的机会和挑战。

### <a name="in-a-channel"></a>通道中

频道包含多个用户之间的线程对话—可能有很多人（目前最多为2000）。 这可能会为你的 bot 提供大规模的访问，但各个交互需要简明。 传统的多项交互操作可能不会很好。 相反，如果需要收集大量信息，请查看使用互动卡片或任务模块，或者可能将对话移动到一对一对话中。 你的 bot 也只能访问直接访问邮件的`@mentioned`邮件，无法使用 Microsoft Graph 和提升的组织级别权限从对话中检索其他邮件。

在频道中 excel 的一些应用场景包括：

* **通知**，尤其是为用户提供用于获取其他信息的互动卡片时。
* **反馈方案**，如投票和调查。
* 可在**单个请求/响应周期**中解决的交互，其中的结果对对话的多个成员很有用。
* **社交/趣味 bot** —获取非常棒的 cat 图像，随机挑选获奖者等。

### <a name="in-a-group-chat"></a>在群聊中

组聊天是三个或更多人之间的非线程对话。 它们的成员数往往少于通道，并且更具暂时性。 与频道类似，你的`@mentioned` bot 仅可直接访问邮件。

在频道中正常工作的方案通常在组聊天中也会起作用。

### <a name="in-a-one-to-one-chat"></a>以一对一聊天

这是对话机器人与用户进行交互的传统方法。 他们可以实现多元化不同的工作负载。 问：&bot、在其他系统中启动工作流的 bot、通知笑话的 bot 以及记录笔记的 bot 只是几个示例。 只需记住，应考虑基于会话的界面是否是展示功能的最佳方式。

## <a name="how-do-bots-work"></a>Bot 的工作原理是什么？

你的 bot 由三部分组成：

* 您承载的可公开访问的 web 服务。
* 您的 bot 注册，用于向 Bot 框架注册你的 bot。
* 您的团队应用程序包，其中包含您的应用程序清单。 这是您的用户安装并将团队客户端连接到 web 服务（通过 Bot 服务路由）的内容。

Microsoft 团队的 bot 基于[Microsoft Bot 框架](https://dev.botframework.com/)构建。 （如果已经有一个基于 Bot 框架的 bot，可以轻松地将其调整为在 Microsoft 团队中工作。）我们建议您使用 c # 或 node.js 来利用我们的[sdk](/microsoftteams/platform/#pivot=sdk-tools)。 这些包扩展了基本的 Bot 生成器 SDK 类和方法：

* 使用专用的卡片类型，如 Office 365 连接器卡。
* 使用和设置针对活动的特定于团队的频道数据。
* 处理消息扩展请求。

> [!IMPORTANT]
> 您可以在任何 web 编程技术中开发团队应用程序，并直接调用[Bot 框架 REST api](/bot-framework/rest-api/bot-framework-rest-overview) ，但您必须自己执行所有令牌处理。

*团队应用程序 Studio*可帮助您创建和配置应用程序清单，并可将 web 服务注册为 bot 框架上的 bot。 它还包含响应控制库和交互式卡片生成器。 *请参阅*[开始使用团队应用 Studio](~/concepts/build-and-test/app-studio-overview.md)。

## <a name="webhooks-and-connectors"></a>Webhook 和连接器

Webhook 和连接器允许您创建简单的 bot 来实现基本交互，例如启动脱离工作流或其他简单命令。 它们仅在您创建它们的团队中运行，适用于特定于贵公司的工作流的简单流程。 *请参阅*[什么是 webhook 和连接器？](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)有关详细信息，请参阅。

## <a name="get-started"></a>入门

* [C # 中的团队对话机器人/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [JavaScript 中的团队对话机器人](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a>了解更多

* [团队中的 bot 的基础知识](~/bots/bot-basics.md)
* [为团队创建机器人](~/bots/how-to/create-a-bot-for-teams.md)
