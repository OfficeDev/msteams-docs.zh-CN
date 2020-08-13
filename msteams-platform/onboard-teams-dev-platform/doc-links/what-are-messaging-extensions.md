---
title: 什么是邮件扩展？
author: clearab
description: Microsoft 团队平台上的邮件扩展概述
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 3e80c965fb8cb2c4da2af6f6bf0709e7c8bd1d88
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651878"
---
# <a name="what-are-messaging-extensions"></a>什么是邮件扩展？

邮件扩展允许用户通过 Microsoft 团队客户端中的按钮和表单与 web 服务进行交互。 他们可以从撰写邮件区域、命令框或直接从邮件中搜索或启动外部系统中的操作。 然后，您可以将该交互的结果发送回 Microsoft 团队客户端（通常采用格式丰富的卡片的形式）。

下面的屏幕截图显示可以从中调用邮件扩展的位置。

![消息扩展调用位置](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="user-scenarios"></a>用户方案

**方案：** 我需要一些外部系统执行某些操作，并希望将操作的结果发送回我的对话。
**示例：** 预订资源并让频道知道您为其预留的日期/时间。

**方案：** 我需要在外部系统中查找内容，我想要与我的对话共享结果。
**示例：** 在 Azure DevOps 中搜索工作项，并将其与组共享为自适应卡片。

**方案：** 我需要在外部系统中完成涉及多个步骤 (或大量信息) 的复杂任务，并且应与会话共享结果。
**示例：** 在跟踪系统中创建基于团队消息的 bug，将该 bug 分配给 Bob，然后将卡片发送给会话线程，并提供 bug 的详细信息。

## <a name="how-do-messaging-extensions-work"></a>邮件扩展功能扩展的工作原理是什么？

邮件扩展由您承载的 web 服务和应用程序清单组成，该服务定义在 Microsoft 团队客户端中可从何处调用 web 服务。 他们利用 Bot 框架的邮件架构和安全通信协议，因此您还需要将 web 服务注册为 Bot 框架中的 bot。 尽管您可以手动创建 web 服务，但我们建议您充分利用[Bot 框架 SDK](https://github.com/microsoft/botframework)来更简单地使用协议。

在 Microsoft 团队应用程序的应用程序清单中，你将定义最大为十个不同命令的单一消息扩展。 每个命令定义一种类型 (操作或搜索) ，并且客户端中的位置可以从 (撰写邮件区域、命令栏和/或邮件) 中调用。 调用后，web 服务将收到具有 JSON 有效负载的 HTTPS 消息，其中包括所有相关信息。 你将使用 JSON 有效负载进行响应，让团队客户端了解下一步要启用的交互。

## <a name="types-of-messaging-extensions"></a>邮件扩展类型

消息扩展命令的类型定义了可用于 web 服务的 UI 元素和交互流。 某些交互（如身份验证和配置）可用于这两种类型的命令。

### <a name="action-commands"></a>操作命令

操作命令使您可以向用户呈现模式弹出窗口，以收集或显示信息。 当用户提交表单时，您的 web 服务可以通过直接在对话中插入邮件，或在撰写邮件区域中插入邮件并允许用户提交邮件来做出响应。 甚至可以将多个表单链接在一起，以获取更复杂的工作流。

它们可以通过撰写邮件区域、命令框或邮件触发。 从邮件中调用时，发送到你的 bot 的初始 JSON 有效负载将包含从中调用的整个邮件。

![邮件扩展操作命令任务模块](~/assets/images/task-module.png)

### <a name="search-commands"></a>搜索命令

搜索命令允许用户在搜索框中手动搜索外部系统，或者通过将指向受监视域的链接粘贴到 "撰写" 邮件区域中来 (的信息) ，然后将搜索结果插入到邮件中。 在最基本的搜索命令流中，初始调用邮件将包含用户提交的搜索字符串。 你将使用卡片和卡片预览的列表进行响应。 团队客户端将在列表中呈现卡片预览，以便最终用户可以从中进行选择。 当用户选择卡片时，完整大小的卡片将插入到撰写邮件区域中。

它们可以通过撰写消息区域或命令框触发。 与 action 命令不同，它们不能从邮件中触发。

![邮件扩展搜索命令](~/assets/images/search-extension.png)

### <a name="link-unfurling"></a>链接展开

您还可以在将 URL 粘贴到撰写邮件区域中时调用您的服务。 此功能称为**链接 unfurling**，使您可以在将包含特定域的 url 粘贴到撰写邮件区域时订阅接收调用。 您的 web 服务可以将 URL "unfurl" 到详细卡片中，提供的信息比标准网站预览卡更多。 您甚至可以添加按钮，这样用户无需离开团队即可执行操作。

## <a name="get-started"></a>入门

准备好开始构建了吗？ 尝试一下我们的快速入门：

### <a name="c"></a>C#
* [带有基于操作的命令的消息扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
* [包含基于搜索的命令的邮件扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)

### <a name="javascript"></a>JavaScript
* [带有基于操作的命令的消息扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
* [包含基于搜索的命令的邮件扩展](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

## <a name="learn-more"></a>了解详细信息

* [创建邮件扩展](~/messaging-extensions/how-to/create-messaging-extension.md)
* [定义操作消息扩展命令](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [定义搜索邮件扩展命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)
* [规划应用程序](../../concepts/extensibility-points.md)
* [生成应用程序](../../concepts/building-an-app.md)
* [发布应用程序](../../concepts/deploy-and-publish/overview.md)
