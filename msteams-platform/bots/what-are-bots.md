---
title: 什么是对话 bot？
author: clearab
description: Microsoft 团队中的会话 bot 概述。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 132b71a4da7462c426468c7fc2f79b26b6fbb03b
ms.sourcegitcommit: 058b7bbd817af5f513e0e018f2ef562dc3086a84
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2020
ms.locfileid: "43120288"
---
# <a name="what-are-conversational-bots"></a>什么是对话 bot？

会话 bot 使用户能够通过文本、交互式卡片和任务模块与 web 服务进行交互。 它们的灵活性非常灵活—会话间的 bot 可用于处理几个简单的命令或复杂、人工智能化的工作和自然语言处理的虚拟助手。 它们可以是大型应用程序的一个方面，也可以完全独立。

下面的 GIF 显示了用户使用文本和交互式卡片同时在一对一聊天中与 bot 聊天。 查找卡片、文本和任务模块的正确组合是创建有用的 bot 的关键所在。 别忘了，机器人要远不止是文本！

![FAQ 加 gif](~/assets/images/FAQPlusEndUser.gif)

## <a name="how-bots-work"></a>Bot 的工作原理

你的团队 bot 由三个元素组成：

* 您承载的可公开访问的 web 服务。
* 使用 Bot 框架的 bot 注册。
* 您的团队应用程序包与您的应用程序清单。 这是用户将安装的内容，并将团队客户端连接到 web 服务，并通过 Bot 服务进行路由。

Microsoft 团队的 bot 基于[Microsoft Bot 框架](https://dev.botframework.com/)构建。 如果您已经有一个基于 Bot 框架的 bot，您可以轻松地对其进行调整以在 Microsoft 团队中工作。 我们建议您使用 c # 或 node.js 来利用我们的[sdk](/microsoftteams/platform/#pivot=sdk-tools)。 这些包扩展了基本的 Bot 生成器 SDK 类和方法，如下所示：

* 使用专用的卡片类型，如 Office 365 连接器卡。
* 使用和设置活动的团队特定频道数据。
* 处理邮件扩展请求。

> [!IMPORTANT]
> 您可以在任何 web 编程技术中开发团队应用程序，并直接调用[Bot 框架 REST api](/bot-framework/rest-api/bot-framework-rest-overview) ，但您必须自己执行所有令牌处理。

> [!TIP]
> 团队应用程序 Studio * 可帮助您创建和配置应用程序清单，并可将 web 服务注册为 Bot 框架上的 bot。 它还包含响应控制库和交互式卡片生成器。 *请参阅*[开始使用团队应用 Studio](~/concepts/build-and-test/app-studio-overview.md)。

## <a name="webhooks-and-connectors"></a>Webhook 和连接器

Webhook 和连接器允许您创建简单的 bot 来实现基本交互，例如启动脱离工作流或其他简单命令。 它们仅在您创建它们的团队中运行，适用于特定于贵公司的工作流的简单流程。 *请参阅*[什么是 webhook 和连接器？](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)有关详细信息，请参阅。

## <a name="where-bots-work-best"></a>在何处最适合使用 bot

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

## <a name="bot-fails"></a>机器人失败

### <a name="having-multi-turn-experiences-in-chat"></a>在聊天中拥有多轮体验

您的 bot 和用户之间的一个广泛的对话框是一种缓慢且过于复杂的方法来使任务完成，还需要开发人员维护状态。 若要退出此状态，用户必须是超时时间或键入 "*取消*"。 在所有情况下，此过程是不必要的单调操作：

用户：使用 Megan 安排会议。

BOT：我发现了200结果，请包含姓和名。

用户：使用 Megan Bowen 安排会议。

机器人：好了，您想要使用 Megan Bowen 来满足什么时间？

用户： 1:00 pm。

机器人：在哪天？

### <a name="supporting-too-many-commands"></a>支持的命令过多

用户不能成功或查看不支持过多命令的 bot （尤其是一系列命令）。 由于当前机器人菜单中只有6个可见的命令，因此任何频率都不大可能使用。 深入了解特定区域的 bot，而不是尝试成为一家广泛的助理将会更好地发挥作用并 fare。

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a>使用 unranked 响应维护大型检索知识库

Bot 最适用于简短的快速交互，而不是 sifting 通过长列表查找答案。

## <a name="get-started"></a>入门

* [C # 中的团队对话机器人/dotnet](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [JavaScript 中的团队对话机器人](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a>了解详细信息

> [!div class="nextstepaction"]
> [团队中的 bot 的基础知识](~/bots/bot-basics.md)

> [!div class="nextstepaction"]
> [为团队创建机器人](~/bots/how-to/create-a-bot-for-teams.md)
