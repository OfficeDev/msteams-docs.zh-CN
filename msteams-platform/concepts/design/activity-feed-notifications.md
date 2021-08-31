---
title: 设计活动源通知
author: heath-hamilton
description: 了解如何为应用设计活动源Teams并获取 Microsoft Teams UI 工具包。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 7bc5527a4ac849ab6a46692da85b051f86606f92
ms.sourcegitcommit: 306b6e8cb3aac8bfda10ef3999467a797d64539d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2021
ms.locfileid: "58408550"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a>为应用设计活动源Microsoft Teams通知

活动源是一个图面，用户可在活动源中Microsoft Teams。 源将保留过去四周的通知。

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="示例显示一个应用通知，Teams移动活动源中。" border="false":::

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="示例显示显示在活动源中的Teams通知。" border="false":::

---

## <a name="anatomy"></a>解剖

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="活动源Teams的设计结构。" border="false":::

|计数器|说明|
|----------|-----------|
|1|**头** 像：显示发起活动的人。|
|2|**活动类型/应用图标**：描述活动的类型。 对于应用通知，行图标将替换为应用图标。|
|3|**标题 (一) ：Actor + reason**： *Actor*：发起活动的用户或应用的名称。 *Reason*：描述活动。|
|4 |**时间戳：** 显示活动发生的时间。|
|5 |**Location (second line)**： Shows where the activity happened in Teams.|
|6 |**第三 (第三行) ：** 可选。 显示预览文本或其他信息。|

## <a name="types-of-activity-feed-notification-cards"></a>活动源通知卡的类型

以下变体显示你可以显示的活动源通知卡类型。 应用徽标替换应用生成的通知的用户头像。

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="活动源Teams的变体。" border="false":::

## <a name="manage-activity-feed-notifications"></a>管理活动源通知

用户可以在"设置"页中管理从Teams发送的通知。

## <a name="related-system-notifications"></a>相关系统通知

每个活动都会生成一个系统通知。 显示内容取决于用户在通知设置中配置哪些内容。 用户还可以基于其操作系统选择通知样式。

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Android 和 iOS Teams活动源卡的变体。" border="false":::

|计数器|说明|
|----------|-----------|
|1|Android|
|2|iOS|

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="不同操作系统Teams活动卡的变体。" border="false":::

|计数器|说明|
|----------|-----------|
|1|Teams自定义|
|2|Windows|
|3|Mac|

---

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [实现活动源通知](/graph/teams-send-activityfeednotifications)
