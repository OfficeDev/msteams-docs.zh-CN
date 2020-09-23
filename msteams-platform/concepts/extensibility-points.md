---
title: 团队应用程序的入口点
author: heath-hamilton
description: 介绍用户在团队中使用应用程序的方式和位置。
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 1c68467177fc440993f059133f049f18785374b7
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209779"
---
# <a name="entry-points-for-teams-apps"></a>团队应用程序的入口点

团队平台提供了一组灵活的入口点，用户可在其中发现和使用您的应用程序。 您的应用程序可以像将现有网站嵌入个人选项卡或多面应用程序（用户在多个入口点之间进行交互）一样简单。

最成功的应用程序会让团队成为本地用户，因此务必仔细规划应用程序的入口点。

## <a name="teams-channels-and-group-chats"></a>团队、频道和组聊天

团队、频道和组聊天是协作空间。 使用这些入口点的应用程序可供所有成员使用，并且通常侧重于其他工作流或解除新的社会交互。

下面介绍了团队应用程序功能在协作上下文中的常见使用方法：

* [**选项卡**](~/tabs/what-are-tabs.md) 提供为团队、频道或组聊天配置的全屏嵌入式 web 体验。 所有成员都与基于 web 的内容进行交互，因此无状态的单页面应用体验是典型的。

* [**邮件扩展**](~/messaging-extensions/what-are-messaging-extensions.md) 是将外部内容插入到对话中或对邮件执行操作而不离开团队的快捷方式。 链接 unfurling 在共享公共 URL 中的内容时提供丰富的内容。

* [**Bot**](~/bots/what-are-bots.md) 通过聊天与对话的成员进行交互，并响应事件 (如添加新成员或重命名频道) 。 与这些上下文中的 bot 的对话对团队、频道或组的所有成员都可见，因此应与所有人相关的 bot 对话。

* [**Webhook 和连接器**](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) 允许外部服务将邮件发布到对话中，并允许用户向服务发送邮件。

* [**Microsoft GRAPH REST API**](https://docs.microsoft.com/graph/teams-concept-overview) ，用于获取有关团队、频道和组聊天的数据，以帮助自动化和管理团队流程。

## <a name="personal-apps"></a>个人应用

[个人应用](~/concepts/design/personal-apps.md) 重点关注与单个用户的交互。 此上下文中的体验对每个用户都是唯一的。 用户可以将个人应用程序固定到左侧导航轨，以便快速访问。

下面介绍了团队功能在个人环境中的常用功能：

* [**Bot**](~/bots/what-are-bots.md) 具有与用户的一对一对话。 需要多转对话或提供仅与特定用户相关的通知的 bot 最适用于个人上下文。

* [**选项卡**](~/tabs/what-are-tabs.md) 提供了对单个用户有意义的全屏嵌入式 web 体验。

## <a name="ui-components"></a>UI 组件

应用程序通常表现出一个或多个标准团队 UI 组件。 使用这些组件构建应用程序会导致丰富的体验，让团队用户的本地体验感到不在。

### <a name="cards"></a>卡

[卡片](~/task-modules-and-cards/what-are-cards.md) 是由 JSON 定义的 UI 容器，可包含带格式的文本、媒体、控件 (如下拉列表和单选按钮) 和触发操作的按钮。

卡片操作可向应用程序的 API 发送有效负载、打开链接、启动身份验证流或向对话发送邮件。 团队平台支持多张卡片，包括自适应卡片、英雄卡片、缩略图卡片等。 您可以组合卡片集合并显示在列表或轮播中。

### <a name="task-modules"></a>任务模块

[任务模块](~/task-modules-and-cards/what-are-task-modules.md) 在团队中提供了模式体验。 它们对于启动工作流、收集用户输入或显示丰富的信息（如视频或 Power BI 仪表板）尤其有用。 在任务模块中，可以运行自定义前端代码、显示 `<iframe>` 小部件或显示自适应卡片。

考虑您想要如何构建应用程序时，请记住，模式是用户输入信息或完成任务（与选项卡或基于对话的 bot 体验相比）的自然。

### <a name="deep-links"></a>深度链接

您的应用程序可以创建 [URL 深层链接](~/concepts/build-and-test/deep-links.md) ，以帮助您通过您的应用程序和团队客户端导航您的用户。 您可以为团队中的大多数实体创建深层链接，有些 (像新的会议请求) 允许您使用 URL 中的查询字符串预填充信息。

例如，您的会话自动程序可以向通道发送一封邮件，其中包含指向任务模块的深层链接，从而将一个卡片作为一对一的邮件发送给用户，这又包含一个深层链接，以便在特定日期/时间使用特定用户新建会议。 使用深层链接可在应用程序可用的各种扩展点之间进行连接，始终保持用户在正确的上下文中的持续时间。

### <a name="web-based-content"></a>基于 Web 的内容

[基于 Web 的内容](~/tabs/how-to/create-tab-pages/content-page.md) 是您承载的可嵌入到选项卡或任务模块中的网页。
