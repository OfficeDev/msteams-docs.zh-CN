---
title: 将用例映射到Teams功能
author: surbhigupta
description: 确定你的应用用例在应用体验Teams工作。
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 82b7c4cf29eb6b5d31c55dbc420a3c2c6c3038dfa710ba6257fc5486a97713bf
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2021
ms.locfileid: "57709550"
---
# <a name="map-your-use-cases-to-teams-app-capabilities"></a>将用例映射到Teams功能

确定用户 *是谁* 以及要解决的问题后，可以决定 *如何* 解决问题了。 The *who，* *what*， and *how* completes the process of understanding and mapping your use cases to Teams app capabilities. 你需要根据从用户收到的查询响应来定义应用的范围，然后确定最适合生成应用的功能。

> [!NOTE]
> 你必须深入了解可用于应用的 [入口点和 UI](../../concepts/extensibility-points.md) 元素。 此外，还必须确保仔细考虑 [用例](../../concepts/design/understand-use-cases.md) 。

## <a name="choose-the-correct-scope-for-your-app"></a>为应用选择正确的作用域

选择应用范围时，请考虑以下事项：

* 应用可以跨范围存在。
* 应用功能（如邮件扩展）可跨范围关注用户。
* 用户通常对将应用添加到频道或Teams很不一样。
* 来宾可以访问在频道或Teams公开的内容。

你可以根据以下条件在个人范围和团队或频道范围之间选择：

* 对于个人范围，请提出以下问题：
  * 出于隐私或其他原因，是否要求与应用进行一对一交互？ 例如，检查休假余额或其他私人信息。
  * 用户之间是否可能没有任何共同协作Teams？ 例如，在公司中查找即将推出的组织范围事件。
  * 在应用体验中，是否需要向用户发送任何Teams消息？ 例如，审批或注册提醒。
* 对于共享范围 (团队、频道或聊天) ，请提出以下问题：
  * 应用在选项卡或机器人中呈现的信息是否与团队中的大多数成员相关且有用？ 例如，Scrum 应用。
  * 应用上下文是否可能随应用添加到的团队而更改？ 例如，Planner 的任务在不同团队中有所不同。 
  * 需要协作的人物中的所有成员是否可能是单个团队的一部分？ 例如，处理票证的代理。

以下方案将指导你了解与应用功能良好协作的入口点和 UI Teams选择：

> [!NOTE]
> 这不是一个详尽的列表，但有助于你思考一些可用的可能性。

## <a name="create-share-and-collaborate-on-items-in-an-external-system"></a>在外部系统中创建、共享和协作处理项目

Microsoft Teams应用是一种与数据交互的不错方法，并且有多种集成点可供选择。

* **使用搜索命令的邮件扩展**：搜索外部系统，并作为交互式卡片共享结果。

* **使用操作命令的消息** 扩展：收集信息以插入数据存储或执行高级搜索。

* **选项卡**：创建用于查看、处理和共享数据的嵌入式 Web 体验。

* **连接器和 webhook：** 一种将数据推送和发送出客户端的简单Teams方法。

* **任务模块**：需要它们收集或显示信息的交互式模式表单。

## <a name="initiate-workflows-and-processes"></a>启动工作流和流程

有时，只需一种在外部系统中快速启动流程或工作流的方法。

* **邮件扩展操作命令**：从邮件触发，允许用户将邮件内容快速发送到 Web 服务。

* **任务模块**：在启动工作流之前，从选项卡、自动程序或消息传递扩展中打开它们以收集信息。

* **对话机器人**：通过文本和富卡片与用户交互。

* **传出 Webhook：** 当你不需要生成整个对话机器人时，进行简单的来回交互是一个不错的选择。

## <a name="send-notifications-and-alerts"></a>发送通知和警报

向用户发送异步通知和通知，Teams。 使用交互式卡片可以快速访问常用操作和指向其他信息的链接。

* **对话机器人**：向组、频道或单个用户发送主动消息。

* **连接器和传入 Webhook：** 允许订阅频道以接收邮件。 连接器允许用户使用配置页面定制订阅。

## <a name="ask-questions-and-get-answers"></a>提问并获取答案

人们有疑问，你可能会得到存储在某处的很多答案。 遗憾的是，连接这两者通常非常困难。

* **对话机器人**：自然语言处理、AI、机器学习以及所有话题。 使用由智能云支持自动程序将用户连接到他们需要的答案。

* **选项卡**：将现有 Web 门户嵌入Teams或为添加Teams创建特定于 Web 门户的版本。

## <a name="get-social"></a>获取社交

协作平台本质上是一个社交平台。 让创造力的一面是免费的，为工作场所添加一些有趣的内容。 所有用户都必须能够发送彩信、提供 kudos、获取一些 meme、删除一些表情符号或其他任何能够影响你奇特感的符号。

## <a name="think-in-terms-of-a-single-page-app"></a>从单页应用考虑

选项卡是嵌入式网页。 您可以在 SPA 中执行几乎任何操作，您可以在 Teams 中的选项卡中Teams。 只需注意作用域。 组和频道选项卡用于共享体验，个人选项卡用于个人体验。 团队的资料列表位于频道选项卡上，而资料列表在个人选项卡中。

## <a name="start-small"></a>小型启动

不确定从何处开始？ 觉得使用各种可用选项有点不知所措？ 你必须选择应用的核心功能，然后开始操作。 在了解信息通过环境中的各个上下文Teams后，可以更加简单地了解更复杂的交互。

## <a name="put-it-all-together"></a>全部放在一起

也就是说，最佳应用通常组合多个功能，从而创建在正确的上下文中使用正确功能吸引用户的应用。 不得将任何功能强制放入不属于它的位置。 仅仅因为有一对一对话机器人，并不意味着将其添加到任何团队。 不同的扩展点适用于不同的内容，可以发挥它们创建成功应用的优势。

## <a name="see-also"></a>另请参阅

[生成首个 Microsoft Teams 应用](~/get-started/code-samples.md#build-your-first-microsoft-teams-app-overview)
