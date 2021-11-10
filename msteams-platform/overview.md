---
title: 生成适用于 Microsoft Teams 平台的应用
author: heath-hamilton
description: 获取开发人员如何使用自定义应用扩展Microsoft Teams功能的概述。
ms.topic: overview
ms.localizationpriority: medium
ms.author: lajanuar
ms.date: 05/24/2021
ms.openlocfilehash: 878b6fd22373edb8f9cbbf28c15c8d5dd10ee3e0
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888032"
---
# <a name="build-apps-for-microsoft-teams"></a>构建 Microsoft Teams 应用

Microsoft Teams应用将关键信息、常用工具和受信任流程引入人们越来越集中、学习和工作的地方。

应用是扩展Teams以满足你的需求。 为现有应用创建全新的Teams或集成现有应用。

> [!div class="nextstepaction"]
> [从这里开始](get-started/get-started-overview.md)

## <a name="what-are-teams-apps"></a>什么是Teams应用？

Teams应用是功能[的组合](concepts/capabilities-overview.md)。 某些应用使用简单的 (发送) ，而其他应用则复杂 (患者记录) 。 规划应用时，请记住Teams协作中心。 最佳应用Teams帮助用户表达自己，并更好地协同工作。

### <a name="personal-apps"></a>个人应用

:::row:::
   :::column span="1":::

**帮助用户关注**： [个人](concepts/design/personal-apps.md) 应用是一个专用空间或自动程序，可帮助用户专注于自己的任务或查看重要的活动。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-personal-apps-2021.png" alt-text="个人应用在客户端中的外观的概念Teams表示。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="tabs"></a>选项卡

:::row:::
   :::column span="1":::

**协作更方便：** 在选项卡中显示基于 Web 的内容，[](tabs/what-are-tabs.md)用户可以在选项卡中一起讨论和处理内容。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-channel-chat-apps-2021.png" alt-text="选项卡在客户端中的外观的概念Teams表示。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="bots"></a>机器人

:::row:::
   :::column span="1":::

**将字词转换为操作**：对话通常导致需要执行某些操作 (生成订单、查看代码、检查票证状态等) 。 机器人[可以在](bots/what-are-bots.md)内部启动这些类型的Teams。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-bots-2021.png" alt-text="自动程序在客户端中的外观的概念Teams表示。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="messaging-extensions"></a>消息扩展

:::row:::

   :::column span="1":::

**使多任务更容易**[：使用消息传递](messaging-extensions/what-are-messaging-extensions.md)扩展，可以在对话中快速共享外部信息。 还可以对消息采取行动，例如根据频道帖子的内容创建帮助票证。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-messaging-extensions-2021.png" alt-text="在概念上表示邮件扩展在 Teams 中的外观。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="meeting-extensions"></a>会议扩展

:::row:::

   :::column span="1":::

**为会议创建应用**：有一些选项用于将你的应用合并到Teams [体验](apps-in-teams-meetings/design/designing-apps-in-meetings.md)。

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-meeting-extensions-2021.png" alt-text="在概念上表示会议扩展在 Teams 中的外观。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="webhooks-and-connectors"></a>Webhook 和连接器

:::row:::

   :::column span="":::

**与外部应用通信**[：传入 Webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks)是一种将通知从另一个应用自动发送到 Teams 通道的简单方法。 使用 [传出 webhook，](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)使用 @mention 发送 web 服务。

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-connectors.png" alt-text="连接器在客户端中的外观的概念Teams表示。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a>Microsoft Graph for Teams

:::row:::

   :::column span="":::

**利用 Teams** 数据：适用于 [Teams](/graph/teams-concept-overview)的 Microsoft Graph API 提供对团队、频道、用户和消息的访问权限，这些信息可帮助你创建或增强应用功能 (如丰富的通知) 。

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-graph.png" alt-text="Microsoft Graph API Teams。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>开始构建

通过设置环境和创建一个简单的Teams快速熟悉构建环境。

> [!div class="nextstepaction"]
> [构建首个应用](get-started/get-started-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>与Teams整合

将用户喜欢的现有 Web 应用、服务或系统的功能与 web 应用的协作功能Teams。

> [!div class="nextstepaction"]
> [集成现有应用](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>一个小代码会大有作为

你无需成为专家程序员来构建出色的Teams应用。 请尝试多个低代码解决方案之一。

> [!div class="nextstepaction"]
> [创建低代码应用](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a>获取应用灵感

寻找应用开发灵感？ 浏览我们具有高保真概念的实际方案和行业解决方案列表，了解应用Teams用户的各种方法。

> [!div class="nextstepaction"]
> [请参阅应用方案](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a>另请参阅

* [应用程序基础知识](~/concepts/app-fundamentals-overview.md)
* [设计Teams应用](~/concepts/design/design-teams-app-process.md)
* [将用例映射到Teams功能](~/concepts/design/map-use-cases.md)
