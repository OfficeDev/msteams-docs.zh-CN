---
title: 为 Microsoft Teams 平台生成应用
author: heath-hamilton
description: 大致了解开发人员如何使用自定义应用扩展 Microsoft Teams 功能。
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 9f043fd5bab441ce88b0e04b4254b925aff25aad
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911882"
---
# <a name="build-apps-for-microsoft-teams"></a>构建 Microsoft Teams 应用

Microsoft Teams 应用将关键信息、常用工具和受信任流程引入人们越来越多的收集、学习和工作的地方。

应用是如何扩展 Teams 以满足你的需求的。 为 Teams 创建新内容或集成现有应用。

> [!div class="nextstepaction"]
> [从这里开始](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a>什么是 Teams 应用？

Teams 应用是功能和[入口点](concepts/capabilities-overview.md)[的组合](concepts/extensibility-points.md)。 例如，用户可以在频道和入口点 (聊天) 自动 (聊天) 。 

某些应用使用简单的 (发送) ，而其他应用在管理患者 (记录时) 。 规划应用时，请记住 Teams 是协作中心。 最佳的 Teams 应用可帮助用户表达自我并更好地协同工作。

:::row:::
   :::column span="":::

### <a name="tabs"></a>选项卡

**更方便地获取信息**：有时你只需使内容更易于查找。 在选项卡中显示重要网页 [，为](tabs/what-are-tabs.md)Teams 中的静态和动态内容提供全屏 Web 体验。

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Teams 客户端中选项卡外观的概念表示形式。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a>机器人

**将字词转换为操作**：对话通常导致需要执行某些操作 (生成订单、查看代码、检查票证状态等) 。 机器人 [可以在](bots/what-are-bots.md) Teams 内启动这些类型的工作流。

:::image type="content" source="assets/images/overview-bots.png" alt-text="自动程序在 Teams 客户端中的外观的概念表示形式。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>消息扩展

**简化多任务**[：使用消息传递](messaging-extensions/what-are-messaging-extensions.md)扩展，可以在对话中快速共享外部信息。 还可以对消息采取行动，例如根据频道帖子的内容创建帮助票证。

:::image type="content" source="assets\images\overview-messaging.png" alt-text="在 Teams 客户端中邮件扩展外观的概念表示形式。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a>Webhook

**与外部应用通信**： [传入 Webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) 是一种将通知从另一个应用自动发送到 Teams 频道的简单方法。 使用 [传出 Webhook，](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)向 Web 服务发送@mention。

:::image type="content" source="assets/images/overview-connectors.png" alt-text="在 Teams 客户端中连接器外观的概念表示形式。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a>适用于 Teams 的 Microsoft Graph

**利用 Teams 数据**：适用于 Teams 的 [Microsoft Graph API](https://docs.microsoft.com/graph/teams-concept-overview) 提供对团队、频道、用户和消息的访问权限，这些信息可帮助你创建或增强应用的功能。

:::image type="content" source="assets/images/overview-graph.png" alt-text="适用于 Teams 的 Microsoft Graph API 的概念表示形式。" border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a>开始构建

   通过创建一个简单的应用并添加一些常用的功能，快速熟悉 Teams 的生成。

   > [!div class="nextstepaction"]
   > [现在生成你的第一个应用](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>与Teams整合

   将用户喜欢的现有 Web 应用、服务或系统的功能与 Teams 的协作功能混合在一起。

   > [!div class="nextstepaction"]
   > [集成现有应用](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>一些代码会大有作为

   你无需是专家程序员来构建出色的 Teams 应用。 请尝试多种低代码解决方案之一。

   > [!div class="nextstepaction"]
   > [创建低代码应用](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a>资源

* [将"共享到 Teams"按钮添加到网站](concepts/build-and-test/share-to-teams.md)
* [设计 Teams 应用](concepts/design/design-teams-app-overview.md)
* [Microsoft Teams JavaScript 客户端 SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* 适用于[JavaScript](https://github.com/Microsoft/botbuilder-js)和[.NET](https://github.com/Microsoft/botbuilder-dotnet/)的 Bot Framework SDK
* [发布 Teams 应用](concepts/deploy-and-publish/overview.md)
