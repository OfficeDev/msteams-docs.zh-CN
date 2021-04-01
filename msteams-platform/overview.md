---
title: 构建适用于 Microsoft Teams 平台的应用
author: heath-hamilton
description: 大致了解开发人员如何使用自定义应用扩展 Microsoft Teams 功能。
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: e40d2b0d8b0d12e6275b97f79d103310d22f9720
ms.sourcegitcommit: 3bd2627b7a334568f61ccc606395e3d89aa521d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "51475926"
---
# <a name="build-apps-for-microsoft-teams"></a>构建 Microsoft Teams 应用

Microsoft Teams 应用将关键信息、常用工具和受信任流程引入人们越来越集中、学习和工作的地方。

应用是扩展 Teams 以满足你的需求。 为 Teams 创建新内容或集成现有应用。

> [!div class="nextstepaction"]
> [从这里开始](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a>什么是 Teams 应用？

Teams 应用是功能和[入口点](concepts/capabilities-overview.md)[的组合](concepts/extensibility-points.md)。 例如，用户可以与你的应用的聊天机器人功能 (在) 入口点 (聊天) 。 

某些应用使用简单的 (发送) ，而其他应用则复杂 (患者记录) 。 规划应用时，请记住 Teams 是协作中心。 最佳的 Teams 应用可帮助用户表达自己，并更好地协同工作。

:::row:::
   :::column span="":::

### <a name="tabs"></a>选项卡

**更方便地获取信息**：有时你只需使内容更易于查找。 在选项卡中 [显示重要网页](tabs/what-are-tabs.md)，为 Teams 中的静态和动态内容提供全屏 Web 体验。

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Teams 客户端中选项卡外观的概念表示形式。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a>机器人

**将字词转换为操作**：对话通常导致需要执行某些操作 (生成订单、查看代码、检查票证状态等) 。 机器人 [可以在](bots/what-are-bots.md) Teams 内启动这些类型的工作流。

:::image type="content" source="assets/images/overview-bots.png" alt-text="Teams 客户端中机器人外观的概念表示形式。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a>消息扩展

**使多任务更容易**[：使用消息传递](messaging-extensions/what-are-messaging-extensions.md)扩展，可以在对话中快速共享外部信息。 还可以对消息采取行动，例如根据频道帖子的内容创建帮助票证。

:::image type="content" source="assets\images\overview-messaging.png" alt-text="概念性表示在 Teams 客户端中邮件扩展的外观。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a>Webhook

**与外部应用通信**[：传入 Webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks)是一种将通知从另一个应用自动发送到 Teams 频道的简单方法。 使用 [传出 webhook，](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)使用 @mention 发送 web 服务。

:::image type="content" source="assets/images/overview-connectors.png" alt-text="在概念上表示 Teams 客户端中的连接器外观。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a>适用于 Teams 的 Microsoft Graph

**利用 Teams 数据**：适用于 Teams 的 [Microsoft Graph API](https://docs.microsoft.com/graph/teams-concept-overview) 提供对团队、频道、用户和消息的访问权限，这些信息可帮助你创建或增强应用的功能。

:::image type="content" source="assets/images/overview-graph.png" alt-text="适用于 Teams 的 Microsoft Graph API 的概念表示形式。" border="false":::

   :::column-end:::
   :::column span="":::

:::row:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

## <a name="build-solutions-for-microsoft-teams-apps"></a>为 Microsoft Teams 应用生成解决方案
 
Microsoft 提供了一本可扩展性外观书籍，这是一个按行业组织的 Teams 应用的方案库。 本书帮助你在 Teams 平台上生成应用，并了解使用各种 Teams 平台功能的不同可能方案。 通讯簿方案从业务问题、所涉及的角色及其挑战开始，以满足业务需求的 Teams 应用解决方案结束。

此库的每个方案都附带一组高保真设计概念模型，这些模型可作为设计应用和增强用户体验的灵感。 此外，该书重点介绍了构建每个应用时遵循的设计和体系结构最佳做法。 有关详细信息，请参阅可扩展性外观书籍。 有关详细信息，请参阅 [扩展性外观书籍](https://adoption.microsoft.com/extensibility-look-book/scenarios/)。 

## <a name="start-building"></a>开始构建

通过创建简单的应用并添加一些常用功能，快速熟悉 Teams 构建。

> [!div class="nextstepaction"]
> [现在生成你的第一个应用](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a>与Teams整合

将用户喜欢的现有 Web 应用、服务或系统的功能与 Teams 的协作功能融合在一起。

> [!div class="nextstepaction"]
> [集成现有应用](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a>一个小代码会大有作为

你无需成为专家程序员来构建出色的 Teams 应用。 请尝试多个低代码解决方案之一。

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
