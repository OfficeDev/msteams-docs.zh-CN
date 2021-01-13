---
title: 什么是对话机器人？
author: clearab
description: Microsoft Teams 中的对话机器人概述。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 0304ae436b54db0d111eaed507beb350f1ca4632
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797867"
---
# <a name="what-are-conversational-bots-in-microsoft-teams"></a>什么是 Microsoft Teams 中的对话机器人？

对话机器人允许用户通过文本、交互式卡片和任务模块与 Web 服务进行交互。 它们非常灵活 — 对话机器人的范围可以包括处理一些简单命令或复杂、人工智能和自然语言处理虚拟助理。 它们可以是较大应用程序的一个方面，也可以完全独立。

下面的 GIF 显示用户同时使用文本和交互式卡片在一对一聊天中与机器人交互。 找到卡片、文本和任务模块的合适组合是创建有用的自动程序的关键。 不要忘记，机器人不仅仅是文本！

![FAQ Plus gif](~/assets/images/FAQPlusEndUser.gif)

## <a name="build--a-bot-for-teams-with-the-microsoft-bot-framework"></a>使用 Microsoft Bot Framework 生成适用于 Teams 的自动程序

[Microsoft Bot Framework](https://dev.botframework.com/)是一个丰富的 SDK，用于使用 C#、Java、Python 和 JavaScript 生成机器人。 如果你已有一个基于 Bot Framework 的自动程序，你可以轻松调整它以在 Microsoft Teams 中工作。 我们建议你使用 C# 或 Node.js来利用[SDK。](/microsoftteams/platform/#pivot=sdk-tools) 这些包扩展基本 Bot Builder SDK 类和方法，如下所示：

* 使用专用卡类型，如 Office 365 连接器卡。
* 使用和设置有关活动的特定于 Teams 的频道数据。
* 处理邮件扩展请求。

Teams 自动程序由三个元素组成：

* 您托管的可公开访问的 Web 服务。
* 使用 Bot Framework 注册机器人。
* 包含应用清单的 Teams 应用包。 用户将安装 Teams 客户端，并通过自动程序服务将其连接到 Web 服务。

> [!IMPORTANT]
> 你可以以任何 Web 编程技术开发 Teams 应用并直接调用 [Bot Framework REST API，](/bot-framework/rest-api/bot-framework-rest-overview) 但你必须自己执行所有令牌处理。

> [!TIP]
> Teams App Studio* 可帮助你创建和配置应用清单，还可以在 Bot Framework 上将 Web 服务注册为自动程序。 它还包含 React 控件库和交互式卡片生成器。 *请参阅* [Teams App Studio 入门](~/concepts/build-and-test/app-studio-overview.md)。

## <a name="create-a-chatbot-for-teams-with-microsoft-power-virtual-agents"></a>使用 Microsoft Power Virtual Agents 为 Teams 创建聊天机器人

[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) 是一项基于 Microsoft Power 平台和 Bot Framework 构建的聊天机器人服务。  Power Virtual Agent 开发过程使用引导式无代码图形界面方法，使团队中的每个成员能够轻松创建和维护智能虚拟代理。  在 Power [Virtual Agents](https://powervirtualagents.microsoft.com)门户中完成聊天机器人的创建后，你可以轻松地将 Power Virtual [Agents 聊天机器人](how-to/add-power-virtual-agents-bot-to-teams.md)与 Teams 集成。 若要开始创建 Power Virtual Agents 聊天机器人， *请参阅* [Power Virtual Agents 文档](https://docs.microsoft.com/power-virtual-agents/)。

## <a name="webhooks-and-connectors"></a>Webhook 和连接器

Webhook 和连接器允许你创建用于基本交互的简单自动程序，如启动工作流或其他简单命令。 它们仅在您创建的团队中工作，并且适用于特定于公司工作流的简单流程。 *有关详细信息*[，请参阅什么是 Webhook 和连接器？](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)

## <a name="where-bots-work-best"></a>自动程序最工作的地方

Microsoft Teams 中的机器人可以是一对一对话、群聊或团队中的频道的一部分。 每个范围都将为对话机器人提供独特的机会和挑战。

### <a name="in-a-channel"></a>在频道中

频道包含多个人之间的线程对话-可能 (，最多两千) 。 这可能会为机器人带来巨大影响，但个人交互需要简洁明了。 传统的多向交互可能不起作用。 相反，请查找使用交互式卡片或任务模块，或者如果需要收集大量信息，则可能会将对话移动到一对一对话。 尽管可以使用 Microsoft Graph 和提升的组织级别权限从对话中检索其他邮件，但自动程序也仅有权访问直接接收的邮件 `@mentioned` 。

机器人在频道中 excel 的一些应用场景包括：

* **通知**，尤其是提供交互式卡片以便用户获取其他信息时。
* **反馈方案，** 如投票和调查。
* 可以在单个请求 **/** 响应周期中解析的交互，其中结果对对话的多个成员很有用。
* **社交/有趣的机器人** — 获取出色的 cat 图像、随机选取获胜者等。

### <a name="in-a-group-chat"></a>在群聊中

群聊是三个或多个人员之间的非线程对话。 它们的成员数通常少于频道的成员数，并且具有更多的瞬态成员。 与频道类似，机器人将仅有权访问直接位于其中 `@mentioned` 的消息。

在频道中良好工作的方案通常与群聊中一样。

### <a name="in-a-one-to-one-chat"></a>在一对一聊天中

这是对话机器人与用户交互的传统方式。 它们可以启用非常不同的工作负载。 问&聊天机器人、在其他系统中启动工作流的机器人、告诉机器人和做笔记的机器人只是几个示例。 请记住，基于对话的界面是否是显示功能的最佳方法。

## <a name="bot-fails"></a>自动程序失败

### <a name="having-multi-turn-experiences-in-chat"></a>在聊天中拥有多轮体验

自动程序与用户之间的广泛对话是完成任务的一种缓慢且过于复杂的方式，它还需要开发人员保持状态。 若要退出此状态，用户必须退出或键入"*取消*"。 最重要的是，此过程不必要的繁琐：

用户：安排与 Megan 的会议。

BOT：我找到 200 个结果，请包含名字和姓氏。

用户：安排与 Megan Bowen 的会议。

BOT：确定，你要在什么时间与 Megan Bowen 会面？

用户：下午 1：00。

BOT：哪一天？

### <a name="supporting-too-many-commands"></a>支持过多命令

支持过多命令（尤其是广泛的命令）的自动程序将不会成功，或者用户不会积极查看。 由于当前自动程序菜单中只有 6 个可见命令，因此其他任何命令都不可能以任何频率使用。 深入到特定领域的机器人（而不是尝试成为广泛助手）将更好地工作并更好地进行开发。

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a>使用未应答的响应维护大型检索知识库

自动程序最适合于短而快速交互，而不是通过长列表查找答案。

## <a name="get-started"></a>入门

* [C#/dotnet 中的 Teams 对话机器人](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [JavaScript 中的 Teams 对话机器人](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a>了解详细信息

> [!div class="nextstepaction"]
> [Teams 中的机器人基础知识](~/bots/bot-basics.md)

> [!div class="nextstepaction"]
> [创建适合 Teams 的机器人](~/bots/how-to/create-a-bot-for-teams.md)
