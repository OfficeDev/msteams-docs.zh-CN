---
title: 了解应用功能
author: heath-hamilton
description: 说明的 Teams 应用功能
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 6d08d06c55aed4b531fba4bb533c896c13073cfc
ms.sourcegitcommit: 9404c2e3a30887b9e17e0c89b12dd26fd9b8033e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/09/2021
ms.locfileid: "51654431"
---
# <a name="understand-microsoft-teams-app-capabilities"></a>了解 Microsoft Teams 应用功能

扩展性或入口点是应用向用户自我清单的不同方式。 例如，用户可以与画布选项卡上的应用交互以执行活动，或者可能会选择使用对话机器人执行相同的操作。 用于生成 Teams 应用的各种功能允许你增加其使用范围。

有多种方法可以扩展 Teams，因此每个应用都是唯一的。 有些仅具有一个功能，如 webhook，而其他功能则具有多个功能来为用户提供各种选项。 例如，你的应用可以在中心位置（即选项卡）中显示数据，并通过对话界面（即自动程序）显示相同的 **信息**。

## <a name="app-capabilities"></a>应用功能

Teams 应用具有以下一项或全部核心功能：

* [选项卡](../tabs/what-are-tabs.md)
* [消息扩展](../messaging-extensions/what-are-messaging-extensions.md)
* [机器人](../bots/what-are-bots.md)
* [Webhook 和连接器](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

你的应用还可以利用高级功能，例如适用于 Teams 的[Microsoft Graph API。](https://docs.microsoft.com/graph/teams-concept-overview)

下图展示了哪些功能将为你提供应用中想要的功能。

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="说明什么是 Teams 应用功能的&quot;心图&quot;。":::

## <a name="always-consider-your-user"></a>始终考虑你的用户

在熟悉 Teams 应用开发时，你将了解它的核心基础。 您了解到存在多个生成特定功能的方法。 在这种情况下，请考虑如何为用户提供更本机的体验。
例如，可以在作为应用程序中的选项卡构建的表单中收集用户输入。 您还可以使用任务模块完成此操作，而无需切换视图和中断用户的工作流程。 选择与用户常规工作流程的偏差最小的扩展点很重要。

## <a name="see-also"></a>另请参阅

> [!div class="nextstepaction"]
> [生成 Teams 应用](../overview.md)
## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [团队应用程序入口点](../concepts/extensibility-points.md)
