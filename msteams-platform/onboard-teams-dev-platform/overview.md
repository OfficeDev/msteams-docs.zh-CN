---
title: Microsoft 团队开发人员平台
author: clearab
description: 概述开发人员如何使用团队平台扩展和自定义 Microsoft 团队功能。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 73cbd4f68d8878872147bd412972495de1b5de6e
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964569"
---
# <a name="building-for-microsoft-teams"></a>为 Microsoft 团队构建

Microsoft 团队应用程序可提供关键信息、常见工具和受信任的过程，以便人们越来越多地收集、学习和工作。

应用程序是您扩展团队以满足您的需求的方式。 创建适用于团队的全新功能或集成现有应用程序。

## <a name="what-are-teams-apps"></a>什么是团队应用？

人员通过一组平台 [功能](capabilities-overview.md)发现和使用团队应用。

有些应用程序很简单 (发送通知) ，其他应用程序 (查看患者记录) 的复杂。 在规划您的应用程序时，请记住，团队是协作中心。 最佳团队应用可帮助人们自己表达自己并更好地协同工作。

:::row:::
   :::column span="":::

### <a name="tabs"></a>选项卡

**更方便地获取信息**：有时只需更轻松地找到一些内容。 在 [选项卡](../tabs/what-are-tabs.md)中显示一个重要的网页，该网页为工作组中的静态和动态内容提供了全屏 web 体验。

:::image type="content" source="doc-links/images/overview-tabs.png" alt-text="选项卡在团队客户端中的外观的概念性表示。" border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a>消息传递扩展

**更轻松**地执行多项工作：使用 [邮件扩展](../messaging-extensions/what-are-messaging-extensions.md)，可以在对话中快速共享外部信息。 您还可以对邮件执行操作，例如根据频道帖子的内容创建帮助票证。

:::image type="content" source="doc-links/images/overview-messaging.png" alt-text="邮件扩展在团队客户端中的显示方式的概念性表示。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a>机器人

将**单词转换为操作**：对话通常会导致需要执行某些操作， (生成订单、查看我的代码、检查票证状态等 ) 。 [机器人](../bots/what-are-bots.md)可以直接在团队内部启动这些类型的工作流。

:::image type="content" source="doc-links/images/overview-bots.png" alt-text="团队客户端中的 bot 外观的概念性表示。" border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a>Webhook

**与外部应用程序通信**： [传入 webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) 是一种将通知从另一个应用程序自动发送到团队频道的简单方法。 使用 [传出的 webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)，将 @mention 的 web 服务进行消息处理。

:::image type="content" source="doc-links/images/overview-connectors.png" alt-text="团队客户端中的连接器外观的概念性表示。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>适用于团队的 Microsoft Graph

**利用团队数据**： [适用于团队的 MICROSOFT Graph REST API](https://docs.microsoft.com/graph/teams-concept-overview) 提供了有关可帮助您创建或增强应用程序功能的团队、频道、用户和消息的信息的访问权限。

:::image type="content" source="doc-links/images/overview-graph.png" alt-text="适用于团队的 Microsoft Graph REST API 的概念性表示。" border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a>入门

使用我们的第一个应用教程快速跳转，了解如何集成和导入现有应用程序，或花一些时间了解团队应用程序开发生命周期。

:::row:::
   :::column span="2":::

### <a name="start-building"></a>开始构建

   通过创建一个简单的应用程序并添加一些常用功能，快速熟悉为团队构建。

   > [!div class="nextstepaction"]
   > [立即构建您的第一个应用程序](build-your-first-app/building-real-world-app.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a>与团队集成

   将用户喜爱的功能与团队协作功能的现有 web 应用、服务或系统融合。

   > [!div class="nextstepaction"]
   > [集成现有应用程序](migrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a>较小的代码是一段较长的方法

   您无需成为专家级程序员即可构建出色的团队应用程序。 尝试几个低代码解决方案中的一个。

   > [!div class="nextstepaction"]
   > [创建低代码应用程序](low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="trust-the-process"></a>信任流程

   了解整个团队平台开发过程，以便有效地为您的组织或任何人规划、设计、构建和发布应用程序。

   > [!div class="nextstepaction"]
   > [开始规划您的应用程序](../concepts/extensibility-points.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a>资源

* [向您的网站添加 "共享到团队" 按钮](../concepts/build-and-test/share-to-teams.md)
* [熟知设计系统](https://fluentsite.z22.web.core.windows.net/)
* [Microsoft 团队 JavaScript SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* 用于 .NET 的 JavaScript 和[Bot 框架 sdk](https://github.com/Microsoft/botbuilder-dotnet/)的[bot 框架 sdk](https://github.com/Microsoft/botbuilder-js)
* [将应用发布到组织或 AppSource](../concepts/deploy-and-publish/overview.md)
