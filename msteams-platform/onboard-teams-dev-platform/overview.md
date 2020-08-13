---
title: 团队开发人员平台
author: clearab
description: 概述开发人员如何使用团队平台扩展和自定义 Microsoft 团队功能。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: d127acb33212f23dff9cf0dd83a1936044c10d5e
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651875"
---
# <a name="building-for-microsoft-teams"></a>为 Microsoft 团队构建

Microsoft 团队应用程序可提供关键信息、常见工具和受信任的过程，以便人们越来越多地收集、学习和工作。

应用程序是您扩展团队以满足您的需求的方式。 您可以为团队创建全新的品牌，或者只是在收藏的应用和服务中集成功能。

## <a name="what-can-teams-apps-do"></a>团队应用程序可以做什么？

人员通过一组平台[功能](capabilities-overview.md)发现和使用团队应用。

有些应用程序很简单 (发送通知) ，其他应用程序 (查看患者记录) 的复杂。 在规划您的应用程序时，请记住，团队是协作中心。 最佳团队应用可帮助人们自己表达自己并更好地协同工作。

### <a name="get-information-more-conveniently"></a>更方便地获取信息

有时，您只需更轻松地查找内容。 在[选项卡](doc-links/what-are-tabs.md)中显示一个重要的网页，该网页为工作组中的静态和动态内容提供了全屏 web 体验。

![选项卡在团队客户端中的外观的概念性表示。](doc-links/images/overview-tabs.png)

### <a name="share-links-without-switching-context"></a>在不切换上下文的情况下共享链接

将信息提取到对话中，永远不会离开团队。 例如，通过邮件[扩展](doc-links/what-are-messaging-extensions.md)，您可以使用邮件撰写框，通过外部系统共享丰富的、易于 digestible 的内容。

![邮件扩展在团队客户端中的显示方式的概念性表示](doc-links\images\overview-messaging.png)

### <a name="turn-words-into-actions"></a>将词语转换为操作

对话通常会导致需要执行某些操作 (创建订单、查看我的代码等 ) 。 [机器人](doc-links/what-are-bots.md)可以直接在团队内部启动这些类型的工作流。

![团队客户端中的 bot 外观的概念性表示](doc-links/images/overview-bots.png)

### <a name="communicate-with-external-apps-and-services"></a>与外部应用程序和服务进行通信

[传入 webhook](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks)是一种将来自其他应用程序的通知自动发送到团队频道或聊天的简单方法。 通过[传出的 webhook](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks)，您可以使用 @mention 向 web 服务发送邮件。

![团队客户端中的连接器外观的概念性表示。](doc-links/images/overview-connectors.png)

### <a name="utilize-teams-data"></a>利用团队数据

[适用于团队的 Microsoft GRAPH REST API](https://docs.microsoft.com/graph/teams-concept-overview)提供了有关可帮助您创建或增强应用程序功能的团队、频道、用户和消息的信息的访问权限。

!["适用于团队的 Microsoft Graph REST API 的概念性表示](doc-links/images/overview-graph.png)
  
## <a name="start-building"></a>开始构建

   通过创建一个简单的应用程序并添加一些常用功能，快速熟悉为团队构建。

   > [!div class="nextstepaction"]
   > [立即构建您的第一个应用程序](build-your-first-app/build-real-world-app.md)

### <a name="bring-it-all-together"></a>将所有组合在一起

   通过将组织最喜爱的 web 应用程序、服务和系统与团队协作功能混合在一起，简化用户的流程和工作流。

   > [!div class="nextstepaction"]
   > [集成现有应用程序](doc-links/integrating-web-apps.md)

### <a name="trust-the-process"></a>信任流程

   了解整个团队平台开发过程，以便有效地为您的组织或任何人规划、设计、构建和发布应用程序。

   > [!div class="nextstepaction"]
   > [开始规划您的应用程序](doc-links/extensibility-points.md)

### <a name="no-code-no-worries"></a>无代码，无照管

   您无需成为程序员即可构建出色的应用程序。 使用 Microsoft Power Platform 创建一个几乎不包含任何代码的团队应用程序。

   > [!div class="nextstepaction"]
   > [导入 Power Platform 应用](doc-links/importing-custom-microsoft-apps.md)

## <a name="resources"></a>资源

* [向您的网站添加 "共享到团队" 按钮](doc-links/share-to-teams.md)
* [使用推荐指南设计你的应用](doc-links/designing-overview.md)
* [熟知的 UI 设计系统](https://fluentsite.z22.web.core.windows.net/)
* [Microsoft 团队 JavaScript 客户端 SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest)
* 用于 .NET 的 JavaScript 和[Bot 框架 sdk](https://github.com/Microsoft/botbuilder-dotnet/)的[bot 框架 sdk](https://github.com/Microsoft/botbuilder-js)
