---
title: 规划 Teams 移动版
author: surbhigupta
description: 规划在 Teams 移动版上创建应用的指南
ms.topic: conceptual
ms.localizationpriority: high
ms.author: v-abirade
ms.openlocfilehash: 16eada349d2a6adc5b45e89f075107838594eeeb
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111722"
---
# <a name="plan-responsive-tabs-for-teams-mobile"></a>规划 Teams 移动版的响应式选项卡

 Teams 平台提供了在移动设备和桌面上构建应用的机会。 应用用户可以首选桌面或移动设备，也可以同时使用两者。 用户可以在桌面上准备数据，但可以通过移动设备使用和共享更多数据。 构建任何应用的关键是了解并满足用户的需求。 有一些功能（如机器人、消息扩展和连接器）可在桌面和移动设备上无缝工作。 但是，构建选项卡和任务模块需要规划在 Teams 移动设备上托管 Web 体验。 本文介绍如何在 Teams 移动版上规划响应式网页。

## <a name="identify-apps-scope"></a>确定应用范围

以下列表提供了计划为 Teams 移动版构建应用的关键信息：

* 考虑 Teams 应用的跨设备功能。 例如，如果在桌面上拥有一个性能良好的应用，则可以探索如何在移动设备上构建类似应用。 最初，在移动设备上转移整个桌面体验可能很困难。 可以从基本但常见的方案开始。 收集更多见解和用户反馈后，请添加功能。

* 确保以移动设备上的相应用户角色为目标。 例如，如果要构建一个为最终用户提供服务的应用，并且还向开发人员和高级经理提供数据访问权限，则当开始在 Teams 移动版上构建应用时，最终用户可以更多地使用该应用。 但是，你可以满足桌面应用上所有角色的需求，但建议从群体数目更大的角色和可能的早期采用者入手，以获得更小的屏幕体验。 根据示例，最终用户是适当的用户角色。 可以逐渐添加功能来支持 Teams 移动版上的其他用户角色。

## <a name="understand-different-stages-to-build-apps"></a>了解构建应用的不同阶段

确定应用范围后，可以了解以下三个阶段，在 Teams 移动版上规划任何应用并增强用户体验：

1. **使用**

   在移动设备上查看应用。 若要在移动设备上构建应用，可以从使用体验开始。 由于移动世界已将内容滚动作为常见做法，因此可以显示相关信息。 使用参与机制（例如通知）来通知更新。

2. **快速操作**

   在移动设备上使用应用。 当用户开始在移动设备上使用内容后，可以通过从桌面应用迁移一些操作来将应用扩展到下一级。 可以针对移动设备优化和构建新操作。

3. **支持**

   提供完整的应用体验以在移动设备上进行互动。 当用户与应用进行互动时，请在移动设备上提供与桌面体验相当或更出色的完全沉浸式体验。 若要为用户提供良好的体验，请让所有用例都在移动设备上响应。

> [!TIP]
> 若要获取有关设计准则的信息，请参阅 [Teams 应用的设计过程](design-teams-app-process.md)。

## <a name="use-cases"></a>用例

让我们通过以下用例来了解如何为 Teams 移动版规划不同类型的应用：

<br>

<details>

<summary><b>仪表板和数据可视化应用</b></summary>

可以了解如何在 Teams 移动平台上规划仪表板和数据可视化应用的响应式选项卡。

使用：

在第一阶段，可以实现最基本的使用体验来查看数据。 域中任何应用的目的都是以可视化效果形式显示数据。 在应用中，可以在桌面上显示最近查看的可视化效果，或显示用户所有授权图表的列表。 在桌面上创建仪表板后，用户可以使用移动设备访问信息。 可以将用户选择的任何图表的详细视图显示为选项卡中的扩展视图，也可以使用任务模块显示。

可以显示以下信息：

* 仪表板和摘要
* 数据视觉对象、地图和信息图
* 图表、图形和表

![仪表板和数据可视化应用使用情况](../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-consumption.png)

快速操作：

在第二阶段，用户可以使用桌面体验中的现有图表和视觉对象。 可以引入以下操作：

* 搜索内容
* 筛选数据
* 创建书签

![仪表板和数据可视化应用快速操作](../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-quick-actions.png)

启用：

在第三阶段，用户可以从头开始创建内容，例如图表和图形。 确保为移动设备引入应用中的所有功能。 例如，可以使用任务模块帮助访问特定数据项以及详细视图。

可以向用户提供以下访问权限：

* 修改标题和说明
* 插入数据项以创建可视化效果
* 在频道或群组聊天中共享可视化效果

![仪表板和数据可视化应用启用](../../assets/images/app-fundamentals/dashboarding-and-data-visualization-apps-enablement.png)

<br>

</details>

<br>

<details>

<summary><b>任务版块应用</b></summary>

可以了解如何在 Teams 移动平台上为任务版块应用规划响应式选项卡。

使用：

在第一阶段中，应用可以在垂直堆栈中向用户显示任务列表。 如果有多个类别的任务，例如“**建议**”、“**活动**”和“**已关闭**”，则提供筛选器安来显示分组任务或作为标头来查看分组任务。

![任务版块应用使用](../../assets/images/app-fundamentals/taskboarding-apps-consumption.png)

快速操作：

在第二个阶段，可以向用户提供以下应用访问权限：

* 创建具有必填字段的任务或项目以减少用户的认知负担
* 更改版块类型或视图
* 展开视图以查看任务
* 使用任务模块查看详细视图
* 将任务移动到不同的类别
* 通过电子邮件和活动源在聊天和频道中共享相关任务

![任务版块应用快速操作](../../assets/images/app-fundamentals/taskboarding-apps-quick-actions.png)

启用：

在第三阶段，可以让用户体验以下活动：

* 添加新项目和版块
* 添加和修改不同的类别，例如“**建议**”、“**活动**”和“**已关闭**”
* 为任务配置评论、附件和其他复杂的功能

![任务板块应用启用](../../assets/images/app-fundamentals/taskboarding-apps-enablement.png)
<br>

</details>

<br>

<details>

<summary><b>合著和白板应用</b></summary>

可以了解如何在 Teams 移动平台上为合著和白板应用规划响应式选项卡。

使用：

在第一阶段，可以考虑使用桌面体验来显示应用中的内容和资产。  可以显示以下功能：

* 评论或反馈
* 放大或缩小
* 挂起文档的当前阶段或进度

![合著和白板应用使用](../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-consumption.png)

快速操作:

在第二个阶段，可以引入以下操作：

* 创建用于协作的新版块或用于签名的新文档
* 在内部以及与来宾共享版块
* 配置管理员权限

> [!TIP]
> 可以公开操作，这些操作可以在小屏幕上轻松显示。

![合著和白板应用快速操作](../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-quick-actions.png)

启用：

在第三阶段，为用户提供完整的体验。 可以让用户体验以下活动：

* 添加文本、形状和快速笔记
* 浏览内容
* 添加层和筛选器
* 删除、撤消和重做操作
* 使用 JS SDK API 访问相机和麦克风。 有关设备功能的详细信息，请参阅[设备功能概述](../device-capabilities/device-capabilities-overview.md)。

![合著和白板应用启用](../../assets/images/app-fundamentals/coauthoring-and-whiteboarding-apps-enablement.png)

<br>

</details>

## <a name="see-also"></a>另请参阅

以下设计和验证指南可根据应用的范围提供帮助：

* [设计选项卡](../../tabs/design/tabs.md)
* [设计机器人](../../bots/design/bots.md)
* [设计任务模块](../..//task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [应用商店验证指南](../deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)
