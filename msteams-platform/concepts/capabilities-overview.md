---
title: 了解团队应用程序功能
author: heath-hamilton
description: 团队应用程序功能说明
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: e7a6fe61fa5c74547ce20cc895afdd044f35e512
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210161"
---
# <a name="understanding-teams-app-capabilities"></a>了解团队应用程序功能

*功能* 是在 Microsoft 团队平台上构建应用程序的扩展点。

有多种方法可以扩展团队，因此每个应用程序都是唯一的：某些应用程序具有一项功能 (如 webhook) ，而另一些则提供用户选项。 例如，您的应用程序可以在中心位置 ("选项卡中显示数据) 并通过会话界面 (bot) 提供相同的信息。

你的团队应用可以具有以下核心功能中的一个或所有：

* [选项卡](../tabs/what-are-tabs.md)
* [消息扩展](../messaging-extensions/what-are-messaging-extensions.md)
* [机器人](../bots/what-are-bots.md)
* [Webhook 和连接器](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

您的应用程序还可以利用高级功能，例如 [Microsoft GRAPH API For 团队](https://docs.microsoft.com/graph/teams-concept-overview)。

请参阅下图，了解哪些功能将在您的应用程序中提供所需的功能。

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="阐明了团队应用功能的构思图。":::

## <a name="doing-whats-best-for-your-users"></a>执行最适合您的用户的操作

在熟悉团队应用程序开发的过程中，您将开始了解其 subtleties。 有多种方法可以生成某些功能 (如收集用户输入) 。 例如，可以使用将基于 web 的窗体嵌入在选项卡中 `<iframe>` 。 此外，您还可以使用任务模块（团队 UI 约定）在选项卡中执行此操作，以获得用户可能喜欢的更真实的体验。

选择适当的功能和设计可先 [了解观众的用例](../concepts/design/understand-use-cases.md)。
