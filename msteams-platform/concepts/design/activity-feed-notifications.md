---
title: 设计活动源通知
author: heath-hamilton
description: 了解如何为应用设计活动源Teams并获取 Microsoft Teams UI 工具包。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: reference
ms.openlocfilehash: 61a2a6da2a5ed0cb3126b9798094b06c575c9b6c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631251"
---
# <a name="designing-activity-feed-notifications-for-your-microsoft-teams-app"></a><span data-ttu-id="b9cc0-103">为应用设计活动源Microsoft Teams通知</span><span class="sxs-lookup"><span data-stu-id="b9cc0-103">Designing activity feed notifications for your Microsoft Teams app</span></span>

<span data-ttu-id="b9cc0-104">活动源是一个图面，用户可在活动源中访问Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-104">The activity feed is a surface for users to access their notifications in Microsoft Teams.</span></span> <span data-ttu-id="b9cc0-105">源将保留过去四周的通知。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-105">The feed retains notifications from the past four weeks.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="b9cc0-106">桌面</span><span class="sxs-lookup"><span data-stu-id="b9cc0-106">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/desktop-overview.png" alt-text="示例显示显示在活动源中的Teams通知。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="b9cc0-108">移动</span><span class="sxs-lookup"><span data-stu-id="b9cc0-108">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-overview.png" alt-text="示例显示显示在移动活动源Teams应用程序通知。" border="false":::

---

## <a name="anatomy"></a><span data-ttu-id="b9cc0-110">解剖</span><span class="sxs-lookup"><span data-stu-id="b9cc0-110">Anatomy</span></span>

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-anatomy.png" alt-text="活动源Teams设计结构。" border="false":::

|<span data-ttu-id="b9cc0-112">计数器</span><span class="sxs-lookup"><span data-stu-id="b9cc0-112">Counter</span></span>|<span data-ttu-id="b9cc0-113">说明</span><span class="sxs-lookup"><span data-stu-id="b9cc0-113">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b9cc0-114">1</span><span class="sxs-lookup"><span data-stu-id="b9cc0-114">1</span></span>|<span data-ttu-id="b9cc0-115">**头** 像：显示发起活动的人。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-115">**Avatar**: Shows who initiated the activity.</span></span>|
|<span data-ttu-id="b9cc0-116">2</span><span class="sxs-lookup"><span data-stu-id="b9cc0-116">2</span></span>|<span data-ttu-id="b9cc0-117">**活动类型/应用图标**：描述活动的类型。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-117">**Activity type/app icon**: Depicts the type of activity.</span></span> <span data-ttu-id="b9cc0-118">对于应用通知，行图标将替换为应用图标。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-118">For app notifications, the line icon is replaced with an app icon.</span></span>|
|<span data-ttu-id="b9cc0-119">3</span><span class="sxs-lookup"><span data-stu-id="b9cc0-119">3</span></span>|<span data-ttu-id="b9cc0-120">**标题 (一行) ：Actor + reason**： *Actor*：发起活动的用户或应用的名称。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-120">**Title (first line): Actor + reason**: *Actor*: Name of the user or app that initiated the activity.</span></span> <span data-ttu-id="b9cc0-121">*Reason*：描述活动。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-121">*Reason*: Describes the activity.</span></span>|
|<span data-ttu-id="b9cc0-122">4 </span><span class="sxs-lookup"><span data-stu-id="b9cc0-122">4</span></span>|<span data-ttu-id="b9cc0-123">**时间戳：** 显示活动发生的时间。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-123">**Timestamp**: Shows when the activity happened.</span></span>|
|<span data-ttu-id="b9cc0-124">5 </span><span class="sxs-lookup"><span data-stu-id="b9cc0-124">5</span></span>|<span data-ttu-id="b9cc0-125">**Location (second line)**： Shows where the activity happened in Teams.</span><span class="sxs-lookup"><span data-stu-id="b9cc0-125">**Location (second line)**: Shows where the activity happened in Teams.</span></span>|
|<span data-ttu-id="b9cc0-126">6 </span><span class="sxs-lookup"><span data-stu-id="b9cc0-126">6</span></span>|<span data-ttu-id="b9cc0-127">**第三 (第三行) ：** 可选。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-127">**Tertiary information (third line)**: Optional.</span></span> <span data-ttu-id="b9cc0-128">显示预览文本或其他信息。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-128">Shows preview text or additional information.</span></span>|

## <a name="types-of-activity-feed-notification-cards"></a><span data-ttu-id="b9cc0-129">活动源通知卡的类型</span><span class="sxs-lookup"><span data-stu-id="b9cc0-129">Types of activity feed notification cards</span></span>

<span data-ttu-id="b9cc0-130">以下变体显示你可以显示的活动源通知卡类型。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-130">The following variants show the kinds of activity feed notification cards you can display.</span></span> <span data-ttu-id="b9cc0-131">应用徽标替换应用生成的通知的用户头像。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-131">The app logo replaces the user avatar for app-generated notifications.</span></span>

:::image type="content" source="../../assets/images/activity-feed/activity-feed-card-types.png" alt-text="活动Teams卡的变体。" border="false":::

## <a name="manage-activity-feed-notifications"></a><span data-ttu-id="b9cc0-133">管理活动源通知</span><span class="sxs-lookup"><span data-stu-id="b9cc0-133">Manage activity feed notifications</span></span>

<span data-ttu-id="b9cc0-134">用户可以在"设置"页中管理从Teams发送的通知。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-134">Users can manage notifications sent from your app in the Teams settings page.</span></span>

## <a name="related-system-notifications"></a><span data-ttu-id="b9cc0-135">相关系统通知</span><span class="sxs-lookup"><span data-stu-id="b9cc0-135">Related system notifications</span></span>

<span data-ttu-id="b9cc0-136">每个活动都会生成一个系统通知。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-136">Each activity generates a system notification.</span></span> <span data-ttu-id="b9cc0-137">显示内容取决于用户在通知设置中配置哪些内容。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-137">What displays depends on what the user configures in their notification settings.</span></span> <span data-ttu-id="b9cc0-138">用户还可以基于其操作系统选择通知样式。</span><span class="sxs-lookup"><span data-stu-id="b9cc0-138">Users can also choose a notification style based on their operating system.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="b9cc0-139">桌面</span><span class="sxs-lookup"><span data-stu-id="b9cc0-139">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/activity-feed/related-system-notifications.png" alt-text="不同操作系统Teams活动卡的变体。" border="false":::

|<span data-ttu-id="b9cc0-141">计数器</span><span class="sxs-lookup"><span data-stu-id="b9cc0-141">Counter</span></span>|<span data-ttu-id="b9cc0-142">说明</span><span class="sxs-lookup"><span data-stu-id="b9cc0-142">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b9cc0-143">1</span><span class="sxs-lookup"><span data-stu-id="b9cc0-143">1</span></span>|<span data-ttu-id="b9cc0-144">Teams自定义</span><span class="sxs-lookup"><span data-stu-id="b9cc0-144">Teams custom</span></span>|
|<span data-ttu-id="b9cc0-145">2</span><span class="sxs-lookup"><span data-stu-id="b9cc0-145">2</span></span>|<span data-ttu-id="b9cc0-146">Windows</span><span class="sxs-lookup"><span data-stu-id="b9cc0-146">Windows</span></span>|
|<span data-ttu-id="b9cc0-147">3</span><span class="sxs-lookup"><span data-stu-id="b9cc0-147">3</span></span>|<span data-ttu-id="b9cc0-148">Mac</span><span class="sxs-lookup"><span data-stu-id="b9cc0-148">Mac</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="b9cc0-149">移动</span><span class="sxs-lookup"><span data-stu-id="b9cc0-149">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/activity-feed/mobile-related-system-notifications.png" alt-text="Android 和 iOS Teams活动源卡的变体。" border="false":::

|<span data-ttu-id="b9cc0-151">计数器</span><span class="sxs-lookup"><span data-stu-id="b9cc0-151">Counter</span></span>|<span data-ttu-id="b9cc0-152">说明</span><span class="sxs-lookup"><span data-stu-id="b9cc0-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b9cc0-153">1</span><span class="sxs-lookup"><span data-stu-id="b9cc0-153">1</span></span>|<span data-ttu-id="b9cc0-154">Android</span><span class="sxs-lookup"><span data-stu-id="b9cc0-154">Android</span></span>|
|<span data-ttu-id="b9cc0-155">2</span><span class="sxs-lookup"><span data-stu-id="b9cc0-155">2</span></span>|<span data-ttu-id="b9cc0-156">iOS</span><span class="sxs-lookup"><span data-stu-id="b9cc0-156">iOS</span></span>|

---

## <a name="next-step"></a><span data-ttu-id="b9cc0-157">后续步骤</span><span class="sxs-lookup"><span data-stu-id="b9cc0-157">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b9cc0-158">实现活动源通知</span><span class="sxs-lookup"><span data-stu-id="b9cc0-158">Implement activity feed notifications</span></span>](/graph/teams-send-activityfeednotifications)
