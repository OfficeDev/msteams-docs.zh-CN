---
title: 什么是邮件扩展？
author: clearab
description: Microsoft 团队平台上的邮件扩展概述
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 01a038d57368826345a55358b1d628447b21f772
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673304"
---
# <a name="what-are-messaging-extensions"></a>什么是邮件扩展？

邮件扩展允许用户通过 Microsoft 团队客户端中的按钮和表单与 web 服务进行交互。 他们可以通过撰写邮件区域、命令框或直接从邮件中搜索或启动外部系统中的操作。 然后，您可以将该交互的结果发送回 Microsoft 团队客户端（通常采用格式丰富的卡片的形式）。

下面的屏幕截图显示可以从中调用邮件扩展的位置。

![消息扩展调用位置](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="what-kinds-of-tasks-are-they-good-for"></a>哪些类型的任务适合？

**方案：** 我需要一些外部系统执行某些操作，并希望将操作的结果发送回我的对话。
**示例：** 预订资源并让频道知道您为其预留的日期/时间。

**方案：** 我需要在外部系统中查找内容，我想要与我的对话共享结果。
**示例：** 在 Azure DevOps 中搜索工作项，并将其与组共享为自适应卡片。

**方案：** 我需要在外部系统中完成涉及多个步骤（或多个信息）的复杂任务，并且应与会话共享结果。
**示例：** 在跟踪系统中创建基于团队消息的 bug，将该 bug 分配给 Bob，然后将卡片发送给会话线程，并提供 bug 的详细信息。

## <a name="how-do-messaging-extensions-work"></a>邮件扩展功能扩展的工作原理是什么？

邮件扩展由您承载的 web 服务和应用程序清单组成，该服务定义在 Microsoft 团队客户端中可从何处调用 web 服务。 他们利用 Bot 框架的邮件架构和安全通信协议，因此您还需要将 web 服务注册为 Bot 框架中的 bot。 尽管您可以手动创建 web 服务，但我们建议您充分利用[Bot 框架 SDK](https://github.com/microsoft/botframework)来更简单地使用协议。

在 Microsoft 团队应用程序的应用程序清单中，你将定义最大为十个不同命令的单一消息扩展。 每个命令定义一种类型（操作或搜索），并且可以从该客户端（撰写邮件区域、命令栏和/或邮件）中调用该客户端中的位置。 调用后，web 服务将收到具有 JSON 有效负载的 HTTPS 消息，其中包括所有相关信息。 你将使用 JSON 有效负载进行响应，让团队客户端了解下一步要启用的交互。

## <a name="types-of-messaging-extension-commands"></a>邮件扩展命令的类型

消息扩展命令的类型定义了可用于 web 服务的 UI 元素和交互流。 某些交互（如身份验证和配置）可用于这两种类型的命令。

### <a name="action-commands"></a>操作命令

操作命令允许你向用户呈现模式弹出窗口，以收集或显示信息。 当用户提交表单时，您的 web 服务可以通过直接在对话中插入邮件，或在撰写邮件区域中插入邮件并允许用户提交邮件来做出响应。 甚至可以将多个表单链接在一起，以获取更复杂的工作流。

它们可以通过撰写邮件区域、命令框或邮件触发。 从邮件中调用时，发送到你的 bot 的初始 JSON 有效负载将包含从中调用的整个邮件。

![邮件扩展操作命令任务模块](~/assets/images/task-module.png)

### <a name="search-commands"></a>搜索命令

搜索命令允许用户搜索外部系统中的信息（通过搜索框手动操作，或将指向被监视域的链接粘贴到撰写邮件区域中），然后将搜索结果插入到邮件中。 在最基本的搜索命令流中，初始调用邮件将包含用户提交的搜索字符串。 你将使用卡片和卡片预览的列表进行响应。 团队客户端将在列表中呈现卡片预览，以便最终用户可以从中进行选择。 当用户选择卡片时，完整大小的卡片将插入到撰写邮件区域中。

它们可以通过撰写消息区域或命令框触发。 与 action 命令不同，它们不能从邮件中触发。

![邮件扩展搜索命令](~/assets/images/search-extension.png)

### <a name="link-unfurling"></a>链接 unfurling

将 URL 粘贴到撰写邮件区域中时，还必须选择调用您的服务。 此功能称为**链接 unfurling**，使您可以在将包含特定域的 url 粘贴到撰写邮件区域时订阅接收调用。 您的 web 服务可以将 URL "unfurl" 到详细卡片中，提供的信息比标准网站预览卡更多。 您甚至可以添加按钮以允许用户立即执行操作，而无需离开 Microsoft 团队客户端。

## <a name="get-started"></a>入门

准备好开始构建了吗？ 尝试一下我们的快速入门：

* 适用于 C 的快速入门#
  * [带有基于操作的命令的消息扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [包含基于搜索的命令的邮件扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* 适用于 JavaScript 的快速入门
  * [带有基于操作的命令的消息扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [包含基于搜索的命令的邮件扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

## <a name="learn-more"></a>了解更多

构建消息扩展：

* [创建邮件扩展](~/messaging-extensions/how-to/create-messaging-extension.md)
* [定义操作消息扩展命令](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [定义搜索邮件扩展命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)
