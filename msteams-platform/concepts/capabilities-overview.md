---
title: 了解 Teams 应用功能
author: heath-hamilton
description: 说明的 Teams 应用功能
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 5336b36b52cf81be414f18ccaaf9e235c079e626
ms.sourcegitcommit: 49d1ecda14042bf3f368b14c1971618fe979b914
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/23/2021
ms.locfileid: "51034703"
---
# <a name="understanding-teams-app-capabilities"></a>了解 Teams 应用功能

*功能* 是构建 Microsoft Teams 平台上应用的扩展点。

有多种方法可以扩展 Teams，因此每个应用都是独一无二的：一些应用只有一个 (如 webhook) ，而另一些则有一些可以为用户提供选项。 例如，你的应用可以在中心位置显示数据 (选项卡) ，并通过对话界面 (自动程序) 。

Teams 应用具有以下一项或全部核心功能：

* [选项卡](../tabs/what-are-tabs.md)
* [消息扩展](../messaging-extensions/what-are-messaging-extensions.md)
* [机器人](../bots/what-are-bots.md)
* [Webhook 和连接器](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

你的应用还可以利用高级功能，例如适用于 Teams 的[Microsoft Graph API。](https://docs.microsoft.com/graph/teams-concept-overview)

请参阅下图，了解哪些功能将提供你需要的应用功能。

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="说明什么是 Teams 应用功能的&quot;心图&quot;。":::

## <a name="doing-whats-best-for-your-users"></a>执行最适合用户的事情

当你熟悉 Teams 应用开发时，你将开始了解它的细微之处。 生成某些功能的方法 (例如收集用户输入) 。 例如，可以使用 在选项卡中嵌入基于 Web 的表单 `<iframe>` 。 您还可以使用任务模块（Teams UI 约定）在选项卡中完成此操作，以便获得用户可能喜欢的更本机体验。

选择正确的功能和设计需要首先 [了解受众的用例](../concepts/design/understand-use-cases.md)。
