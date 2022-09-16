---
title: 自适应卡的通用操作概述
description: 了解适用于自适应卡片的通用操作，例如特定于用户的视图、顺序工作流支持，以及桌面和移动环境的更多功能
ms.topic: overview
ms.localizationpriority: medium
ms.openlocfilehash: 9c04ed4726840bd3d1637555d1bb021f31bf2e25
ms.sourcegitcommit: 19f3e4e9088d0a07c9b567e76640d498b9d1981f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/16/2022
ms.locfileid: "67786974"
---
# <a name="universal-actions-for-adaptive-cards"></a>自适应卡的通用操作

自适应卡片的通用操作是从开发人员反馈演变而来的，尽管自适应卡片的布局和呈现是通用的，但操作处理并非如此。 即使开发人员想要将同一张卡片发送到不同的地方，他们也必须以不同的方式处理操作。

自适应卡的通用操作将机器人作为处理操作的常见后端，并引入了一种新的操作类型， `Action.Execute`它适用于 Teams 和 Outlook 等应用。

本文档可帮助你了解如何使用通用操作模型来增强用户跨平台和应用程序与自适应卡片交互的体验。

> [!NOTE]
> 支持自适应卡 v1.4 的通用操作仅适用于机器人发送的卡。 即将推出对通过撰写框发送的卡片和链接展开卡片的支持。

## <a name="enhance-user-experiences-with-universal-actions-for-adaptive-cards"></a>使用适用于自适应卡片的通用操作增强用户体验

自适应卡的通用操作通过启用以下方案来增强用户体验：

* [通用操作](#universal-actions)
* [用户特定视图](#user-specific-views)
* [顺序工作流支持](#sequential-workflow-support)
* [最新视图](#up-to-date-views)

### <a name="universal-actions"></a>通用操作

在自适应卡的通用操作之前，不同的主机提供了不同的操作模型，如下所示：

* 使用的 `Action.Submit`Teams 或机器人是一种将实际通信模型延迟到基础通道的方法。
* Outlook 用于 `Action.Http` 与自适应卡有效负载中显式指定的后端服务通信。

下图显示了当前不一致的操作模型：

:::image type="content" source="~/assets/images/adaptive-cards/current-teams-outlook-action-model.png" alt-text="不一致的操作模型":::

使用适用于自适应卡片的通用操作，可以用于 `Action.Execute` 跨不同平台的操作处理。 `Action.Execute` 适用于包括 Teams 和 Outlook 在内的各个中心。 此外，自适应卡片可以作为触发的调用请求的 `Action.Execute` 响应返回。

下图显示了新的通用操作模型：

:::image type="content" source="~/assets/images/adaptive-cards/universal-action-model.png" alt-text="自适应卡的新通用操作":::

现在，可以将相同的卡片发送到 Teams 和 Outlook，并使用基础机器人使它们彼此保持同步。 在任一平台上执行的任何操作都会通过此生成反映到另一个平台，部署 (自适应卡片通用操作) 模型 *的任何位置* 。

下图描绘了 Teams 和 Outlook 的自适应卡的通用操作：

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="~/assets/images/mobile-universal-bots-teams-outlook.png" alt-text="移动到 Teams 和 Outlook 的同一张卡片":::

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-teams-outlook.png" alt-text="Teams 和 Outlook 的同一张卡片" lightbox="../../../assets/images/adaptive-cards/universal-bots-teams-outlook.png":::

* * *

### <a name="user-specific-views"></a>用户特定视图

今天，Teams 聊天或频道中的每个用户都会在自适应卡片上看到完全相同的视图和按钮操作。 但是，在某些情况下，某些用户需要以不同的方式行事，并有权访问同一聊天或频道中的不同信息。

例如，如果在聊天或频道中发送事件报告卡，则只有分配了事件的用户才能看到“ **解决** ”按钮。 另一方面，事件创建者必须看到 **“编辑”** 按钮，所有其他用户必须只能查看事件的详细信息。 属性启用 `refresh` 的用户特定视图可以实现此操作。

下图显示了一个票证消息扩展 (ME) 的示例，其中聊天中的不同用户根据要求显示不同的操作：

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="~/assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg" alt-text="移动用户特定视图" lightbox="../../../assets/images/adaptive-cards/mobile-universal-bots-incident-management.jpg":::

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="用户特定视图" lightbox="../../../assets/images/adaptive-cards/universal-bots-incident-management.png":::

* * *

有关详细信息，请参阅 [用户特定视图的示例](User-Specific-Views.md)。

### <a name="sequential-workflow-support"></a>顺序工作流支持

使用顺序工作流支持，用户可以通过一系列工作流进行进度，而无需单独发送不同的卡片。 这可以通过 `Action.Execute` 返回自适应卡片来响应操作来实现。 此外，聊天或频道中的任何用户都可以通过其工作流进行进度，而无需修改聊天中其他用户的卡片。

下图演示了食品订购机器人示例： <br/>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

下图显示了聊天或频道中不同用户的各种状态：

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="餐饮机器人状态" lightbox="../../../assets/images/adaptive-cards/universal-bots-catering-bot.png":::

有关详细信息，请参阅 [顺序工作流示例](Sequential-Workflows.md)。

### <a name="up-to-date-views"></a>最新视图

可以创建自动更新的自适应卡片。 例如，它可以是用户发送的审批请求。 批准后，该卡必须自动显示有关请求审批时间和批准请求的人员的详细信息。 刷新模型使你能够提供此类最新视图。 下图显示了多步骤审批流以及如何显示不同用户的视图。

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views.png" alt-text="最新的用户特定视图" lightbox="../../../assets/images/adaptive-cards/universal-bots-up-to-date-views.png":::

有关详细信息，请参阅 [最新视图的示例](Up-To-Date-Views.md)。

现在，你可以了解如何使用新的通用操作模型转换自适应卡片，以提供独特且增强的用户体验。

## <a name="adaptive-cards-and-the-new-universal-actions-model"></a>自适应卡片和新的通用操作模型

自适应卡片是内容（如文本和图形）以及用户可以执行的操作的组合。 有关详细信息，请参阅 [自适应卡片](http://adaptivecards.io/)。 新的自适应卡通用操作可跨平台和应用程序常见处理自适应卡片操作。 有关详细信息，请参阅 [通用操作模型](/adaptive-cards/authoring-cards/universal-action-model)。

可以使用[快速入门指南]. (Work-with-universal-actions-for-adaptive-cards.md) 更新方案并利用通用操作入门。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [使用自适应卡的通用操作](Work-with-universal-actions-for-adaptive-cards.md)

## <a name="see-also"></a>另请参阅

* [什么是机器人](~/bots/what-are-bots.md)
* [自适应卡概述](~/task-modules-and-cards/what-are-cards.md)
* [自适应卡片 @ Microsoft Build 2020](https://youtu.be/hEBhwB72Qn4?t=1393)
* [自适应卡 @ Ignite 2020](https://techcommunity.microsoft.com/t5/video-hub/elevate-user-experiences-with-teams-and-adaptive-cards/m-p/1689460)。
* [基于搜索的消息传递扩展的通用操作](../../../messaging-extensions/how-to/search-commands/universal-actions-for-search-based-message-extensions.md)
