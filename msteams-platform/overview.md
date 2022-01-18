---
title: 为 Microsoft Teams 平台生成应用
author: heath-hamilton
description: 大致了解开发人员如何使用自定义应用扩展 Microsoft Teams 功能。
ms.topic: overview
ms.localizationpriority: high
ms.author: lajanuar
ms.date: 05/24/2021
ms.openlocfilehash: 1a7957c8ea6d889ffe5ab7e40c8a5bb1377b6ca5
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059621"
---
# <a name="build-apps-for-microsoft-teams"></a>构建 Microsoft Teams 应用

Microsoft Teams 应用将关键信息、常用工具和受信任的流程引入人们不断收集、学习和工作的地方。

应用是扩展 Teams 以满足需求的一种方法。 为 Teams 创建全新的内容，或集成现有应用。

> [!div class="nextstepaction"]
> [从这里开始](get-started/get-started-overview.md)

## <a name="what-are-teams-apps"></a>什么是 Teams 应用？

Teams 应用是[功能](concepts/capabilities-overview.md)的组合。 某些应用很简单（发送通知），而另一些应用则很复杂（管理患者记录）。 规划应用时，请记住 Teams 是一个协作中心。 最佳 Teams 应用可帮助人们表达自己，更好地协同工作。

### <a name="personal-apps"></a>个人应用

:::row:::
   :::column span="1":::

**帮助人们关注**：[个人应用](concepts/design/personal-apps.md)是一个专用空间或机器人，可帮助用户专注于自己的任务或查看对他们很重要的活动。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-personal-apps-2021.png" alt-text="Teams 客户端中个人应用的外观的概念表示形式。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="tabs"></a>选项卡

:::row:::
   :::column span="1":::

**更方便地进行排序**：在 [tab](tabs/what-are-tabs.md)中显示基于 Web 的内容，用户可以在其中一起讨论和处理它。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-channel-chat-apps-2021.png" alt-text="Teams 客户端中选项卡外观的概念表示形式。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="bots"></a>机器人

:::row:::
   :::column span="1":::

**将字词转换为操作**： 对话通常会导致需要执行某些操作（生成订单、查看我的代码、检查票证状态等）。 [机器人](bots/what-are-bots.md)可以直接在 Teams 中启动这些类型的工作流。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-bots-2021.png" alt-text="在 Teams 客户端中机器人外观的概念表示形式。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="messaging-extensions"></a>消息传递扩展

:::row:::

   :::column span="1":::

**可更轻松地进行多任务**：使用 [分页扩展](messaging-extensions/what-are-messaging-extensions.md)，可以在对话中快速共享外部信息。 还可以对消息执行操作，例如基于频道帖子的内容创建帮助票证。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-messaging-extensions-2021.png" alt-text="消息传递扩展在 Teams 客户端中的外观的概念表示形式。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="meeting-extensions"></a>会议扩展

:::row:::

   :::column span="1":::

**为会议创建应用**： [将应用纳入 Teams 通话体验](apps-in-teams-meetings/design/designing-apps-in-meetings.md)有一些选项。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-meeting-extensions-2021.png" alt-text="Teams 客户端中会议扩展的外观的概念表示形式。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="webhooks-and-connectors"></a>Webhook 和连接器

:::row:::

   :::column span="":::

**与外部应用通信**： [传入 Webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) 是一种将通知从其他应用自动发送到 Teams 频道的简单方法。 使用 [传出 webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)，向 Web 服务发送@mention消息。

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-connectors.png" alt-text="连接器在 Teams 客户端中的外观的概念表示形式。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph for Teams

:::row:::

   :::column span="":::

**利用 Teams 数据**：[Microsoft Graph API for Teams](/graph/teams-concept-overview) 提供有关团队、频道、用户和消息的信息的访问权限，这些信息可帮助你为应用创建或增强功能（如丰富通知）。

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-graph.png" alt-text="适用于 Teams 的 Microsoft Graph API 的概念表示形式。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>开始生成

通过设置环境并创建简单的应用，快速熟悉 Teams 的构建。

> [!div class="nextstepaction"]
> [构建首个应用](get-started/get-started-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>与Teams整合

将用户喜欢的现有 Web 应用、服务或系统的功能与 Teams 的协作功能混合在一起。

> [!div class="nextstepaction"]
> [创建现有应用](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>一些代码会大有用处

无需成为专家程序员即可构建出色的 Teams 应用。 试用几个低代码解决方案之一。

> [!div class="nextstepaction"]
> [创建低代码应用](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a>获取应用的创意

正在寻找应用开发灵感？ 通过高保真概念模拟浏览我们的实际方案和行业解决方案列表，了解 Teams 应用可帮助用户的各种方式。

> [!div class="nextstepaction"]
> [查看应用方案](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="test-your-app-running-across-microsoft-365"></a>测试跨Microsoft 365运行的应用

可以使用 Microsoft Teams JavaScript 客户端 SDK v2 预览版预览以其他高使用率Microsoft 365体验运行的 Teams 应用。

> [!div class="nextstepaction"]
> [扩展应用](m365-apps/overview.md)

## <a name="see-also"></a>另请参阅

* [应用程序基础知识](~/concepts/app-fundamentals-overview.md)
* [指定 Teams 应用](~/concepts/design/design-teams-app-process.md)
* [将用例映射到 Teams 应用功能](~/concepts/design/map-use-cases.md)
