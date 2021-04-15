---
title: 消息扩展
author: clearab
description: Microsoft Teams 平台上的消息扩展概述
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2d82202c72584927fc705813151d91510a7f12c9
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696735"
---
# <a name="messaging-extensions"></a>消息扩展

消息传递扩展允许用户通过 Microsoft Teams 客户端中的按钮和表单与 Web 服务交互。 他们可以从撰写邮件区域、命令框或直接从邮件搜索或启动外部系统中的操作。 你可以以格式丰富的卡片的形式将交互结果发送回 Microsoft Teams 客户端。 本文档概述了邮件扩展、在不同方案中执行的任务、邮件扩展的工作、操作和搜索命令以及链接取消点击。

下图显示了调用邮件扩展的位置：

![消息扩展调用位置](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="scenarios-where-messaging-extensions-are-used"></a>使用邮件扩展的方案

| 方案 | 示例 |
|:-----------------|:-----------------|
|您希望某些外部系统执行一个操作，并且此操作的结果将发送回您的对话。|预留资源并允许频道知道预留的时间段。|
|您希望在外部系统中查找内容，并与对话共享结果。|在 Azure DevOps 中搜索工作项，并作为自适应卡片与组共享。|
|您希望完成涉及外部系统中多个步骤或大量信息的复杂任务，并与对话共享结果。|根据 Teams 消息在跟踪系统中创建 Bug，将 Bug 分配给 Bob，然后向对话线程发送包含 Bug 详细信息的卡片。|

## <a name="understand-how-messaging-extensions-work"></a>了解邮件扩展如何工作

消息传递扩展包含您托管的 Web 服务和应用程序清单，它定义从 Microsoft Teams 客户端调用 Web 服务的地方。 Web 服务利用 Bot Framework 的消息架构和安全通信协议，因此你必须在 Bot Framework 中将 Web 服务注册为自动程序。 

> [!NOTE]
> 虽然可以手动创建 Web 服务，但使用 [Bot Framework SDK](https://github.com/microsoft/botframework) 处理协议。

在 Microsoft Teams 应用的应用清单中，使用最多十个不同的命令定义单个消息传递扩展。 每个命令都定义一种类型，如操作或搜索以及客户端中调用它的位置。 调用位置包括撰写邮件区域、命令栏和邮件。 在调用时，Web 服务会收到一条包含 JSON 有效负载的 HTTPS 消息，其中包括所有相关信息。 使用 JSON 有效负载进行响应，让 Teams 客户端知道要启用的下一次交互。 

## <a name="types-of-messaging-extension-commands"></a>邮件扩展命令的类型

邮件扩展命令有两种类型：操作命令和搜索命令。 消息扩展命令类型定义可用于 Web 服务的 UI 元素和交互流。 某些交互（如身份验证和配置）可用于两种类型的命令。

### <a name="action-commands"></a>操作命令

操作命令用于向用户显示用于收集或显示信息的模式弹出窗口。 当用户提交表单时，Web 服务会通过直接将邮件插入对话或将邮件插入撰写邮件区域来做出响应。 之后，用户可以提交邮件。 可以将多个表单链接在一起，以使用更复杂的工作流。

操作命令从撰写邮件区域、命令框或邮件中触发。 从邮件调用命令时，发送到机器人的初始 JSON 有效负载包括从其中调用它的整个消息。 下图显示了邮件扩展操作命令任务模块 ![ ：邮件扩展操作命令任务模块](~/assets/images/task-module.png)

### <a name="search-commands"></a>搜索命令

搜索命令允许用户通过搜索框手动搜索外部系统的信息，或者将受监视域的链接粘贴到撰写邮件区域，然后将搜索结果插入邮件中。 在最基本的搜索命令流中，初始调用消息包括用户提交的搜索字符串。 使用卡片和卡片预览列表进行响应。 Teams 客户端为用户呈现卡片预览列表。 当用户从列表中选择卡片时，全尺寸卡片将插入到撰写邮件区域中。

卡片从撰写邮件区域或命令框触发，不会从邮件中触发。 无法从邮件中触发它们。
下图显示了邮件扩展搜索命令任务模块：

![邮件扩展搜索命令](~/assets/images/search-extension.png)

> [!NOTE]
> 有关卡片详细信息，请参阅 [什么是卡片](../task-modules-and-cards/what-are-cards.md)。

## <a name="link-unfurling"></a>链接展开

在撰写邮件区域中粘贴 URL 时，将调用 Web 服务。 此功能称为链接取消点击。 当包含特定域的 URL 粘贴到撰写邮件区域中时，可以订阅接收调用。 Web 服务可以将 URL"取消展开"为详细卡片，提供比标准网站预览卡更多的信息。 你可以添加按钮以允许用户立即采取措施，而无需离开 Microsoft Teams 客户端。
在邮件扩展中粘贴链接时，以下图像显示链接展开功能：
 
![取消链接](../assets/images/messaging-extension/unfurl-link.png)

![链接取消点击](../assets/images/messaging-extension/link-unfurl.gif)


## <a name="see-also"></a>另请参阅

> [!div class="nextstepaction"]
> [创建邮件扩展](../build-your-first-app/build-messaging-extension.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [定义操作消息传递扩展命令](~/messaging-extensions/how-to/action-commands/define-action-command.md)

> [!div class="nextstepaction"]
> [定义搜索邮件扩展命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)
