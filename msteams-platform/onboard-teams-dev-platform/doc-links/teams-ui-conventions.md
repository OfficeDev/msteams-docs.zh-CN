---
title: 确定团队应用程序上下文
author: heath-hamilton
description: 在规划团队应用程序时，您必须确定是否将在协作空间、个人空间或两者中使用应用程序。
ms.openlocfilehash: 05c92aa8b199cbdb58e477fb4a64467c150edbfd
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651892"
---
# <a name="getting-to-know-teams-ui-conventions"></a>获取已知团队 UI 约定

应用程序通常表现出一个或多个标准团队 UI 约定。 使用这些约定构建应用程序的功能会导致丰富的体验，让团队用户的本地体验感到不上。

## <a name="cards"></a>卡

[卡片](~/task-modules-and-cards/what-are-cards.md) 是由架构化 JSON 定义的 UI 容器，可包含多个属性和附件。 它们可以包含带格式的文本、媒体、控件 (如下拉框和单选按钮) 和用于触发卡片操作的按钮。

卡片操作可向应用程序的 API 发送有效负载、打开链接、启动身份验证流或向对话发送邮件。 团队平台支持多种类型的卡片，包括自适应卡片、英雄卡片、缩略图卡片等。 您可以组合卡片集合并显示在列表或轮播中。

## <a name="task-modules"></a>任务模块

[任务模块](~/task-modules-and-cards/what-are-task-modules.md) 提供了团队中的模式弹出窗口体验。 它们对于启动工作流、收集用户输入或显示丰富的信息（如视频或 Power BI 仪表板）尤其有用。 在任务模块中，可以运行自定义前端代码、显示 `<iframe>` 小部件或显示自适应卡片。

考虑您想要如何构建应用程序时，请记住，模式是用户输入信息或完成任务（与选项卡或基于对话的 bot 体验相比）的自然。

## <a name="deep-links"></a>深度链接

您的应用程序可以创建 [URL 深层链接](~/concepts/build-and-test/deep-links.md) ，以帮助您通过您的应用程序和团队客户端导航您的用户。 您可以为团队中的大多数实体创建 deeplink，有些 (如新的会议请求) 允许您使用 URL 中的查询字符串预填充信息。 

例如，您的会话自动程序可以向任务模块发送一封邮件，其中包含一个 deeplink，以将一个卡片作为一对一的邮件发送给一个用户，而这又包含一个 deeplink，以便在特定的日期/时间使用特定用户新建会议。 使用深层链接可在应用程序可用的各种扩展点之间进行连接，始终保持用户在正确的上下文中的持续时间。

## <a name="web-based-content"></a>基于 Web 的内容

[基于 Web 的内容](~/tabs/how-to/create-tab-pages/content-page.md) 是您承载的可嵌入到选项卡或任务模块中的网页。 若要在团队客户端中嵌入您的网页，必须执行以下操作：

* 包含 `HTTPS` 在 URL 中。
* 嵌入在中 `<iframe>` 。
* 包括 Microsoft 团队 JavaScript 客户端 SDK，并 `initialize()` 在页面加载时调用 SDK 的方法。

## <a name="next-steps"></a>后续步骤

* [设计应用程序](../../tabs/design/tabs.md)
