---
title: 自适应卡片的通用操作概述
description: 自适应卡片的通用操作快速概述。
ms.topic: overview
ms.localizationpriority: medium
ms.openlocfilehash: ba957456e2926e11b021f6a2577706cef7fb5ad7
ms.sourcegitcommit: 8feddafb51b2a1a85d04e37568b2861287f982d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2021
ms.locfileid: "59475711"
---
# <a name="universal-actions-for-adaptive-cards"></a>自适应卡的通用操作

自适应卡片的通用操作从开发人员反馈中发展，尽管自适应卡片的布局和呈现是通用的，但操作处理不是。 即使开发人员希望将同一张卡片发送到不同位置，他们必须处理不同的操作。

自适应卡片的通用操作将机器人作为处理操作的通用后端引入，并引入了新的操作类型，它适用于应用，如Teams `Action.Execute` 和Outlook。

本文档可帮助你了解如何使用通用操作模型增强跨平台和应用程序与自适应卡片交互的用户体验。

> [!NOTE]
> 仅对自动程序发送的自适应卡片 v1.4 的通用操作的支持可用。 即将推出对通过撰写框和链接取消点击卡片发送的卡片的支持。

## <a name="enhance-user-experiences-with-universal-actions-for-adaptive-cards"></a>使用自适应卡片的通用操作增强用户体验

自适应卡片的通用操作通过启用以下方案来增强用户体验：

* [通用操作](#universal-actions)
* [用户特定视图](#user-specific-views)
* [顺序工作流支持](#sequential-workflow-support)
* [最新视图](#up-to-date-views)

### <a name="universal-actions"></a>通用操作

在自适应卡片的通用操作之前，不同的主机提供不同的操作模型，如下所示：

* Teams或自动程序 `Action.Submit` 使用 ，这是一种将实际通信模型延迟到基础通道的方法。
* Outlook与自适应卡片有效负载中显式指定的后端 `Action.Http` 服务通信。

下图显示了当前不一致的操作模型：

:::image type="content" source="~/assets/images/adaptive-cards/current-teams-outlook-action-model.png" alt-text="不一致的操作模型":::

借助自适应卡片的通用操作，可用于 `Action.Execute` 跨不同平台的操作处理。 `Action.Execute`适用于中心，包括Teams Outlook。 此外，自适应卡片还可以作为触发的调用 `Action.Execute` 请求的响应返回。

下图显示了新的通用操作模型：

:::image type="content" source="~/assets/images/adaptive-cards/universal-action-model.png" alt-text="自适应卡片的新通用操作":::

现在，你可以向用户和用户发送Teams Outlook，然后使用基础自动程序保持彼此同步。 在此内部版本下，在任一平台上执行的任何操作都反映给另一个平台， (自适应卡片的通用操作) 模型。

下图描述了适用于用户和用户的通用自适应卡片Teams Outlook：

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-teams-outlook.jpg" alt-text="移动同一卡片Teams和Outlook":::

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-teams-outlook.png" alt-text="与 Teams 和 Outlook":::

* * *

### <a name="user-specific-views"></a>用户特定视图

现在，聊天Teams频道中的每个用户都会在自适应卡片上看到完全相同的视图和按钮操作。 但是，在某些情况下，要求某些用户采取不同的行动，并有权访问同一聊天或频道中的不同信息。

例如，如果您在聊天或频道中发送事件报告卡，则只有分配了事件的用户才能看到"解决 **"** 按钮。 另一方面，事件创建者必须看到"编辑"按钮，并且所有其他用户只能查看事件的详细信息。 这是由 属性启用的用户特定视图 `refresh` 所实现。

下图显示了一个票证消息传递扩展 (ME) ，其中聊天中的不同用户根据要求显示了不同的操作：

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="移动用户特定视图":::

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="用户特定视图":::

* * *

有关详细信息，请参阅用户 [特定视图的示例](User-Specific-Views.md)。

### <a name="sequential-workflow-support"></a>顺序工作流支持

借助顺序工作流支持，用户可以执行一系列工作流，而无需单独发送不同的卡片。 这是通过返回自适应卡片以响应操作 `Action.Execute` 而实现。 此外，聊天或频道中的任意用户都可以通过其工作流进行，而无需修改聊天中其他用户的卡片。

下图演示了一个食物订购机器人示例： <br/>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

下图显示了聊天或频道中不同用户的不同状态：

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="适应机器人状态":::

有关详细信息，请参阅顺序 [工作流的示例](Sequential-Workflows.md)。

### <a name="up-to-date-views"></a>最新视图

你可以创建自动更新的自适应卡片。 例如，它可以是由用户发送的审批请求。 审批后，该卡片必须自动显示有关请求审批时间和批准请求者的详细信息。 刷新模型使您能够提供此类最新视图。 下图显示了多步骤审批流以及如何显示不同用户的视图。

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views.png" alt-text="最新用户特定视图":::

有关详细信息，请参阅 [最新视图的示例](Up-To-Date-Views.md)。

现在，你可以了解如何使用新的通用操作模型转换自适应卡片，以提供独特且增强的用户体验。

## <a name="adaptive-cards-and-the-new-universal-actions-model"></a>自适应卡片和新的通用操作模型

自适应卡片是内容（如文本和图形）以及用户可以执行的操作的组合。 有关详细信息，请参阅自适应 [卡片](http://adaptivecards.io/)。 自适应卡片的新通用操作支持跨平台和应用程序常见处理自适应卡片操作。 有关详细信息，请参阅通用 [操作模型](/adaptive-cards/authoring-cards/universal-action-model)。

可以通过使用快速入门指南更新方案 [并利用通用](Work-with-universal-actions-for-adaptive-cards.md) 操作开始。

## <a name="see-also"></a>另请参阅

* [什么是自动程序](~/bots/what-are-bots.md)
* [自适应卡概述](~/task-modules-and-cards/what-are-cards.md)
* [自适应卡片 @ Microsoft Build 2020](https://youtu.be/hEBhwB72Qn4?t=1393)
* [Adaptive Cards @ Ignite 2020](https://techcommunity.microsoft.com/t5/video-hub/elevate-user-experiences-with-teams-and-adaptive-cards/m-p/1689460)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [使用自适应卡的通用操作](Work-with-universal-actions-for-adaptive-cards.md)
