---
title: 规划应用概述
author: heath-hamilton
description: 介绍规划应用、了解用例、应用功能和其他 Teams 功能的元素。
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.openlocfilehash: bb72b099c82e12190cbdb955d68362dda731a939
ms.sourcegitcommit: 9d318eda5589ea8f5519d05cb83e0acf3e13e2f4
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66150685"
---
# <a name="plan-your-app-with-teams-features"></a>使用 Teams 功能规划应用

构建出色的 Teams 应用就是寻找满足用户需求的正确功能组合的过程。 应用的设计、特性、功能源于此目的。

从本质上看，Teams 是一个协作平台。它也是一个社交平台，是跨平台的本机平台和 Office 365 的核心，并为你提供个人画布来创建应用。

在本部分中，了解如何：

* 确定用例并将其映射到 Teams 功能。
* 使用计划清单。
* 应用部署以外的计划。

## <a name="plan-with-teams"></a>使用 Teams 进行规划

Teams 即平台在应用开发的每个阶段为你提供工具包、库、应用。 让我们分解一下应用生成的生命周期：

:::image type="content" source="../assets/images/app-fundamentals/plan-app.png" alt-text="图示应用规划的过程" border="true":::

* [生成之前](#before-you-build)
* [生成时](#during-build)
* [生成后](#post-build)
* [计划清单](../concepts/design/planning-checklist.md)

### <a name="before-you-build"></a>生成之前

了解用户及其关注点是 Teams 应用提供帮助的第一个指标。 围绕问题构建用例，确定应用如何解决该问题，并绘制解决方案。

* **了解你的用例和 Teams 应用功能**：了解用户的要求，并识别正确的功能。

* **映射用例**：根据需求将常见用例映射到 Teams 功能，如共享、协作、工作流、相关社交平台等。

* **为 Teams 移动版计划响应式选项卡**：它涵盖了常见的方案，有助于规划 Teams 移动应用。

### <a name="during-build"></a>在生成期间

* **创建和生成应用项目**：通过 Teams 可以选择最适合应用要求的生成环境。 使用 Teams 工具包或其他 SDK（如 C#、Blazor、Node.js 等）开始使用。

* **设计应用 UI**：使用 Teams UI 工具包和 UI 库设计应用布局。

* **将 Teams 用作平台**：Teams 平台可帮助你构建单功能或多功能应用。 Teams 应用由增强应用体验的集成产品和服务提供支持。

    :::image type="content" source="../assets/images/overview/teams-solution.png" alt-text="Teams 解决方案的感知表示形式。" border="true":::

    应用在 Teams 上显示为选项卡、自动程序、消息扩展、连接器、Webhook 或多功能应用。 这些功能在后端由 Azure、Microsoft Graph、SharePoint、Power 应用提供支持，可帮助自动执行任务和流程。

    这些功能的组合帮助你将应用解决方案变为现实。

* **集成设备功能**：可以在应用中集成本机设备功能，例如相机、QR 或条形码扫描仪、照片库、麦克风、位置。

### <a name="post-build"></a>生成后

* 将应用与 Teams 和其他应用（如 Microsoft 365、Microsoft Graph 等）集成。
* 使用开发人员门户配置、管理、部署应用。

#### <a name="government-community-cloud"></a>政府社区云

政府社区云 (GCC) 是以政府为中心的商业环境副本。 美国国防部 (DOD) 和联邦承包商必须满足严格的网络安全和合规性要求。 为此，已创建 GCC-High 以满足 DOD 和联邦承包商的需求。 GCC-High 是 DOD 云的副本，但存在于其自己的主权环境中。 DOD 云仅针对国防部构建。

政府云的终结点为：

| 租户 | GCC | GCC-High | DOD |
|-------------|---------|---|---|
|Teams 客户端|`https://teams.microsoft.com`|`https://gov.teams.microsoft.us/`|`https://dod.teams.microsoft.us/` |
|Teams 管理员 |`https://admin.teams.microsoft.com/`|`https://admin.gov.teams.microsoft.us/`|`https://admin.dod.teams.microsoft.us`|
|Microsoft Graph |`https://graph.microsoft.com`|`https://graph.microsoft.us`|`https://dod-graph.microsoft.us`|

下表包括 GCC、GCC-High、DOD 的 Teams 功能和可用性：

| 功能   | GCC | GCC-High | DOD |
|-------------|---------|---|---|
| Teams 拥有的应用（与在内部开发的应用中一样） | ✔️ 如果应用具有 GCC，则会启用该应用。 | ✔️ 如果应用具有 GCC-High，则会启用该应用。 | ✔️ 如果应用具有 DOD，则会启用该应用。 |
| Microsoft 应用 | ✔️ 符合 GCC 的 Microsoft 应用 | ✔️ 符合 GCC-High 的 Microsoft 应用 | ✔️ 符合 DOD 的 Microsoft 应用 |
| 3P 或第三方应用 | ✔️ 第三方应用可用。默认情况下禁用，租户管理员自行决定是否启用它。 | ❌ | ❌ |
| 自定义或 Lob 选项卡应用 |  ✔️ | ✔️(****Compliance UI**_) | ✔️(_ ***Compliance UI***) |
| 自定义或 Lob 机器人 | ✔️ | ✔️(****Compliance UI***) | ❌ |
| 自定义消息扩展 | ✔️ | ✔️ | ❌ |
| 旁加载应用 | ✔️ | ❌ | ❌ |
| 自定义连接器 | ❌ | ❌ | ❌ |

****合规性 UI***：通过启用第三方通信，客户接受通过第三方而不是 Microsoft 处理此类通信。 客户全权负责降低与第三方机器人在其服务中连接的风险。 Microsoft 不认可客户允许与其服务连接的第三方的安全性，也不提供任何担保、明示或暗示。 启用机器人将基于你选择利用的机器人将系统边界扩展到此租户之外。 你有责任确保这符合你的合规性要求，包括 FedRAMP、DFARS、ITAR 等。你有责任评估连接到的任何终结点和 URL 的风险和符合性。

以下列表有助于确定对于不同功能的 GCC、GCC-High、DOD 的可用性：

* 对于第三方应用，请参阅 [web 应用](../samples/integrating-web-apps.md)和[会议应用拓展性](../apps-in-teams-meetings/meeting-app-extensibility.md)。
* 对于机器人，请参阅[为 Teams 构建第一个对话机器人](../get-started/first-app-bot.md)、[设计 Teams 机器人](../bots/design/bots.md)、[将机器人添加到 Microsoft Teams 应用](../resources/bot-v3/bots-overview.md)、[Teams 中的机器人](../bots/what-are-bots.md)。
* 有关旁加载应用的信息，请参阅[允许自定义 Teams 应用](../concepts/design/enable-app-customization.md)、[分发你的 Microsoft Teams 应用](../concepts/deploy-and-publish/apps-publish-overview.md)、[在 Teams 中上传你的应用](../concepts/deploy-and-publish/apps-upload.md)。
* 有关自定义连接器的信息，请参阅[创建适用于 Teams 的 Office 365 连接器](../webhooks-and-connectors/how-to/connectors-creating.md)。

</details>

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [用例和 Teams 功能](design/understand-use-cases.md)

## <a name="see-also"></a>另请参阅

* [计划清单](../concepts/design/planning-checklist.md)
* [Teams 集成注意事项](../samples/integrating-web-apps.md)
* [构建你的第一个 Microsoft Teams 应用](../build-your-first-app/build-first-app-overview.md)
