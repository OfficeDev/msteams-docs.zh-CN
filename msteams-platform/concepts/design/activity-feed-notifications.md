---
title: " 设计活动源通知 "
author: heath-hamilton
description: 了解如何为 Teams 应用设计活动源通知并获取 Teams UI 工具包。 在 Visual Studio C 中从 Teams 通道开发通知#
ms.localizationpriority: medium
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 9a17027f7dd68993a118f24bb23cfff0a56651e1
ms.sourcegitcommit: 4ba6392eced76ba6baeb6d6dd9ba426ebf4ab24f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/21/2022
ms.locfileid: "66919765"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a>为 Microsoft Teams 应用设计活动源通知

活动源是用户在 Microsoft Teams 中访问其通知的图面。 源保留过去四周的通知。

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="示例显示在移动版 Teams 活动源中显示的应用通知。":::

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="示例显示 Teams 活动源中显示的应用通知。":::

---

## <a name="anatomy"></a>解剖

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="设计 Teams 活动源通知的解剖。":::

|计数器|说明|
|----------|-----------|
|1|**头像**：显示发起活动的人员。|
|2|**活动类型/应用图标**：描述活动的类型。 对于应用通知，行图标将替换为应用图标。|
|3|**标题 (第一行) ：执行组件 + 原因**： *执行组件*：发起活动的用户或应用的名称。 *原因*：描述活动。|
|4|**时间戳**：显示活动发生的时间。|
|5|**第二行 (位置)**：显示 Teams 中的活动发生位置。|
|6|**文本预览 (第三行)**：显示从通知开始截断的行。|

## <a name="types-of-activity-feed-notification-cards"></a>活动源通知卡的类型

以下变体显示可以显示的活动源通知卡的类型。 应用徽标将替换应用生成的通知的用户头像。

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="Teams 活动源卡的变体。":::

## <a name="manage-activity-feed-notifications"></a>管理活动源通知

用户可以在 Teams 设置页中管理从应用发送的通知。

## <a name="related-system-notifications"></a>相关系统通知

每个活动都会生成系统通知。 显示的内容取决于用户在其通知设置中配置的内容。 用户还可以根据其操作系统选择通知样式。

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Android 和 iOS 上 Teams 活动源卡的变体。":::

|计数器|说明|
|----------|-----------|
|1|Android|
|2|iOS|

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="不同操作系统上 Teams 活动卡的变体。":::

|计数器|说明|
|----------|-----------|
|1|Teams 自定义|
|2|Windows|
|3|Mac|

---

## <a name="step-by-step-guide"></a>分步指南

按照 [分步指南](../../sbs-graphactivity-feedbroadcast.yml) 在 Teams 中发送活动源通知。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [实现活动源通知](/graph/teams-send-activityfeednotifications)
