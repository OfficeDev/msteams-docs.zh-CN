---
title: 了解团队应用程序功能
author: heath-hamilton
description: ''
ms.topic: overview
ms.author: heath-hamilton
ms.openlocfilehash: 580d75b648bde1caf0e85647c89635804c91fb70
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651909"
---
# <a name="understanding-teams-app-capabilities"></a>了解团队应用程序功能

*功能*是在 Microsoft 团队平台上构建应用程序的扩展点。

有多种方法可以扩展团队客户端，因此每个应用程序都是唯一的：某些应用程序具有一项功能 (如 webhook) ，而另一些则可以提供用户选项。 例如，您的应用程序可以在中心位置 ("选项卡中显示数据) 并通过会话界面 (bot) 提供相同的信息。

你的团队应用可以具有以下核心功能中的一个或所有：

* [选项卡](../tabs/what-are-tabs.md)
* [消息扩展](../messaging-extensions/what-are-messaging-extensions.md)
* [Webhook 和连接器](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)
* [机器人](../bots/what-are-bots.md)

您的应用程序还可以利用高级功能，例如[Microsoft GRAPH REST API](../graph-api/rsc/resource-specific-consent.md)。

请参阅下图，了解哪些功能将在您的应用程序中提供所需的功能。

![说明团队应用程序功能是什么的构思图](doc-links/images/capabilities-overview.png)

## <a name="doing-whats-best-for-your-users"></a>执行最适合您的用户的操作

在熟悉团队应用程序开发的过程中，您将开始了解其 subtleties。 有多种方法可以生成某些功能 (如收集用户输入) 。 例如，可以使用将基于 web 的窗体嵌入在选项卡中 `<iframe>` 。 此外，您还可以使用任务模块（团队 UI 约定）在选项卡中执行此操作，以获得用户可能喜欢的更真实的体验。

选择功能和 UI 约定、控件和元素的正确组合，可以先[了解受众的用例](../concepts/design/understand-use-cases.md)。

## <a name="learn-more"></a>了解详细信息

* [开始规划您的应用程序](../concepts/extensibility-points.md)
