---
title: 了解应用功能
author: heath-hamilton
description: Teams说明的应用功能
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: a10c991c374392afca0ce793c0c34ea3fc0ca611
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155360"
---
# <a name="understand-microsoft-teams-app-capabilities"></a>了解Microsoft Teams应用功能

扩展性或入口点是应用向用户自我清单的不同方式。 例如，用户可以与画布选项卡上的应用交互以执行活动，或者可能会选择使用对话机器人执行相同的操作。 用于构建应用应用的各种Teams允许你增加其使用范围。

有多种方法可以扩展Teams，因此每个应用都是唯一的。 有些仅具有一个功能，如 webhook，而其他功能则具有多个功能来为用户提供各种选项。 例如，你的应用可以在中心位置（即选项卡）中显示数据，并通过对话界面（即自动程序）显示相同的 **信息**。

## <a name="app-capabilities"></a>应用功能

你的Teams应用具有以下一项或全部核心功能：

* [选项卡](../tabs/what-are-tabs.md)
* [消息扩展](../messaging-extensions/what-are-messaging-extensions.md)
* [机器人](../bots/what-are-bots.md)
* [Webhook 和连接器](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

你的应用还可以利用高级功能，例如适用于 Teams 的[Microsoft Graph API。](/graph/teams-concept-overview)

下图展示了哪些功能将为你提供你需要的应用功能：

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="&quot;心图&quot;说明了Teams功能是什么。":::

## <a name="always-consider-your-user"></a>始终考虑你的用户

当你熟悉应用Teams时，你已了解它的核心基础。 您了解到存在多个生成特定功能的方法。 在这种情况下，请考虑如何为用户提供更本机的体验。
例如，可以在作为应用程序中的选项卡构建的表单中收集用户输入。 您还可以使用任务模块完成此操作，而无需切换视图和中断用户的工作流程。 选择与用户常规工作流程的偏差最小的扩展点很重要。

## <a name="government-community-cloud-gcc"></a>政府社区云 (GCC)

政府社区云是一个以政府为中心的商业环境副本。 国防部 (DOD) 和联邦承包商必须满足严格的网络安全和合规性要求。 为此，GCC-High满足 DOD 和联邦承包商的需求。 GCC-High是 DOD 云的副本，但存在于其自己的自主环境中。 DOD 云仅为国防部生成。

下表包含 Teams、GCC-High 和 DOD GCC和可用性：

| 功能   | GCC | GCC-High | DOD |
|-------------|---------|
| Teams开发的应用一样，拥有的应用 | ✔️应用是否已启用GCC。 | ✔️应用是否已启用，GCC-高。 | ✔️应用是否已启用 DOD。 |
| Microsoft 应用 | ✔️ Microsoft 应用符合GCC | ✔️ Microsoft 应用符合GCC-High | ✔️符合 DOD 的 Microsoft 应用 |
| 3p 或第三方应用 | ✔️第三方应用可用。 默认情况下禁用，租户管理员自行决定是否启用它。 | ❌ | ❌ |
| 机器人 | ✔️ | ❌ | ❌ |
| 自定义或 Lob 选项卡应用 |  ✔️ | ✔️ | ✔️ |
| 旁加载应用 | ✔️ | ❌ | ❌ |
| 自定义或 Lob 机器人 | ✔️ | ❌ | ❌ |
| 自定义消息传递扩展 | ❌ | ❌ | ❌ |
| 自定义连接器 | ❌ | ❌ | ❌ |

以下列表可帮助标识这些功能GCC、GCC-High 和 DOD 的可用性：

* 有关第三方应用，请参阅 [Web 应用](../samples/integrating-web-apps.md) 和 [会议应用程序扩展性](../apps-in-teams-meetings/meeting-app-extensibility.md)。
* 对于机器人，请参阅生成适用于[Teams](../get-started/first-app-bot.md)的第一个对话机器人、设计[Teams](../bots/design/bots.md)机器人、将机器人添加到[Microsoft Teams 应用](../resources/bot-v3/bots-overview.md)和 Teams。 [](../bots/what-are-bots.md)
* 有关旁加载应用，请参阅启用[Teams自定义](../concepts/design/enable-app-customization.md)应用、分配[Microsoft Teams 应用](../concepts/deploy-and-publish/apps-publish-overview.md)，Upload[应用Teams。](../concepts/deploy-and-publish/apps-upload.md)
* 有关自定义连接器，请参阅[create Office 365 connectors for Teams](../webhooks-and-connectors/how-to/connectors-creating.md)。

## <a name="see-also"></a>另请参阅

[生成适用于Teams](../overview.md) 
[生成首个Microsoft Teams应用](../build-your-first-app/build-first-app-overview.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [团队应用程序入口点](../concepts/extensibility-points.md)
