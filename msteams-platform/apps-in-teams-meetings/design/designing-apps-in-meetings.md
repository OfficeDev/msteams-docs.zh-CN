---
title: 设计会议扩展
author: heath-hamilton
description: 了解如何在会议Teams设计应用并获取 Microsoft Teams UI 工具包。
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: a08e5a850a62b0cf73661d00e07e55e46abce32f
ms.sourcegitcommit: 3560ee1619e3ab6483a250f1d7f2ceb69353b2dc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2021
ms.locfileid: "53335408"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="4e312-103">设计会议Microsoft Teams扩展</span><span class="sxs-lookup"><span data-stu-id="4e312-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="4e312-104">你可以创建应用来使会议更加高效。</span><span class="sxs-lookup"><span data-stu-id="4e312-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="4e312-105">例如，要求用户在呼叫过程中完成调查或发送不会中断会议流的快速提醒。</span><span class="sxs-lookup"><span data-stu-id="4e312-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="4e312-106">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="4e312-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="4e312-107">你可以找到更全面的设计指南，包括你可以根据需要获取和修改的元素，Microsoft Teams UI 工具包。</span><span class="sxs-lookup"><span data-stu-id="4e312-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4e312-108">获取 Microsoft Teams UI Kit（用户）</span><span class="sxs-lookup"><span data-stu-id="4e312-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="4e312-109">添加会议扩展</span><span class="sxs-lookup"><span data-stu-id="4e312-109">Add a meeting extension</span></span>

<span data-ttu-id="4e312-110">用户可以在会议之前和会议期间添加会议扩展名。</span><span class="sxs-lookup"><span data-stu-id="4e312-110">Users can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="4e312-111">他们还可以直接从应用商店添加特定会议Teams应用。</span><span class="sxs-lookup"><span data-stu-id="4e312-111">They also can add an app for a specific meeting directly from the Teams store.</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="4e312-112">在会议前添加</span><span class="sxs-lookup"><span data-stu-id="4e312-112">Add before a meeting</span></span>

<span data-ttu-id="4e312-113">在会议详细信息中，用户可以选择"添加选项卡 **+"** 以打开应用飞出控件并查找针对会议优化的应用。</span><span class="sxs-lookup"><span data-stu-id="4e312-113">In the meeting details, users can select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="示例演示如何在会议之前添加会议扩展名。" border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="4e312-115">会议期间添加</span><span class="sxs-lookup"><span data-stu-id="4e312-115">Add during a meeting</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4e312-116">桌面设备</span><span class="sxs-lookup"><span data-stu-id="4e312-116">Desktop</span></span>](#tab/desktop)

在会议中，**用户可以选择"** 更多 :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **添加应用**"，然后选择他们需要的应用。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="示例演示如何在会议期间添加会议扩展名。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="4e312-119">移动设备</span><span class="sxs-lookup"><span data-stu-id="4e312-119">Mobile</span></span>](#tab/mobile)

在桌面上添加应用后，可以选择该应用，并且可以通过选择"更多"在会议使用 **该应用** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: 。

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="示例演示如何在移动会议期间添加会议扩展。" border="false":::

---

## <a name="before-a-meeting"></a><span data-ttu-id="4e312-122">会议前</span><span class="sxs-lookup"><span data-stu-id="4e312-122">Before a meeting</span></span>

<span data-ttu-id="4e312-123">在会议之前，用户可以在选项卡中添加内容。以下示例显示了一个草稿调查问题，人员将在呼叫过程中回答该问题。</span><span class="sxs-lookup"><span data-stu-id="4e312-123">Prior to a meeting, users can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="示例演示如何在呼叫之前应用会议详细信息中的内容。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="4e312-125">结构：会议 (会议之前和之后) </span><span class="sxs-lookup"><span data-stu-id="4e312-125">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="示例显示会议之前和之后的会议选项卡的结构结构分析。" border="false":::

|<span data-ttu-id="4e312-127">计数器</span><span class="sxs-lookup"><span data-stu-id="4e312-127">Counter</span></span>|<span data-ttu-id="4e312-128">说明</span><span class="sxs-lookup"><span data-stu-id="4e312-128">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4e312-129">1</span><span class="sxs-lookup"><span data-stu-id="4e312-129">1</span></span>|<span data-ttu-id="4e312-130">**选项卡名称**：选项卡的导航标签。</span><span class="sxs-lookup"><span data-stu-id="4e312-130">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="4e312-131">2</span><span class="sxs-lookup"><span data-stu-id="4e312-131">2</span></span>|<span data-ttu-id="4e312-132">**Tab 溢出**：打开选项卡操作，如重命名和删除。</span><span class="sxs-lookup"><span data-stu-id="4e312-132">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="4e312-133">3</span><span class="sxs-lookup"><span data-stu-id="4e312-133">3</span></span>|<span data-ttu-id="4e312-134">**iframe：** 显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="4e312-134">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="4e312-135">使用 UI 模板进行设计</span><span class="sxs-lookup"><span data-stu-id="4e312-135">Designing with UI templates</span></span>

<span data-ttu-id="4e312-136">使用以下 UI 模板Teams之一来帮助设计会议选项卡：</span><span class="sxs-lookup"><span data-stu-id="4e312-136">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="4e312-137">[列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目采取操作。</span><span class="sxs-lookup"><span data-stu-id="4e312-137">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="4e312-138">[任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为看板或街道）是一组卡片，通常用于跟踪工作项或票证的状态。</span><span class="sxs-lookup"><span data-stu-id="4e312-138">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="4e312-139">[仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是包含多个卡片的画布，可提供数据或内容的概述。</span><span class="sxs-lookup"><span data-stu-id="4e312-139">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="4e312-140">[表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单用于以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="4e312-140">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="4e312-141">[空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="4e312-141">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="4e312-142">[左侧导航](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav)：如果你的选项卡需要一些导航，左侧导航组件会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="4e312-142">[Left nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your tab requires some navigation.</span></span> <span data-ttu-id="4e312-143">通常，应该将导航保持在最低程度。</span><span class="sxs-lookup"><span data-stu-id="4e312-143">In general, you should keep navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="4e312-144">使用会议内选项卡</span><span class="sxs-lookup"><span data-stu-id="4e312-144">Use an in-meeting tab</span></span>

<span data-ttu-id="4e312-145">"会议内"选项卡是一块画布，用于增强会议期间的协作。</span><span class="sxs-lookup"><span data-stu-id="4e312-145">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="4e312-146">与会者可以通过共享视图或基于角色的视图在会议阶段外的专用空间中查看应用内容并与之交互。</span><span class="sxs-lookup"><span data-stu-id="4e312-146">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="4e312-147">用例</span><span class="sxs-lookup"><span data-stu-id="4e312-147">Use cases</span></span>

<span data-ttu-id="4e312-148">人们可能会使用"会议内"选项卡：</span><span class="sxs-lookup"><span data-stu-id="4e312-148">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="4e312-149">提供详细反馈。</span><span class="sxs-lookup"><span data-stu-id="4e312-149">Provide detailed feedback.</span></span> <span data-ttu-id="4e312-150">例如，评估一个职位候选人。</span><span class="sxs-lookup"><span data-stu-id="4e312-150">For example, evaluate a job candidate.</span></span>
* <span data-ttu-id="4e312-151">为会议参与者创建投票、调查或任务项。</span><span class="sxs-lookup"><span data-stu-id="4e312-151">Create a poll, survey, or task item for the meeting participants.</span></span>
* <span data-ttu-id="4e312-152">显示与会议相关的备注。</span><span class="sxs-lookup"><span data-stu-id="4e312-152">Display notes relevant to the meeting.</span></span> <span data-ttu-id="4e312-153">例如，有关销售线索的信息。</span><span class="sxs-lookup"><span data-stu-id="4e312-153">For example, information about a sales lead.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4e312-154">桌面设备</span><span class="sxs-lookup"><span data-stu-id="4e312-154">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="示例演示如何在会议中的选项卡中显示投票内容。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="4e312-156">移动设备</span><span class="sxs-lookup"><span data-stu-id="4e312-156">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="示例演示如何在移动设备上的&quot;会议&quot;选项卡中显示投票内容。" border="false":::

---

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="4e312-158">结构：会议内选项卡</span><span class="sxs-lookup"><span data-stu-id="4e312-158">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="示例显示会议内选项卡的结构结构分析。" border="false":::

|<span data-ttu-id="4e312-160">计数器</span><span class="sxs-lookup"><span data-stu-id="4e312-160">Counter</span></span>|<span data-ttu-id="4e312-161">说明</span><span class="sxs-lookup"><span data-stu-id="4e312-161">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4e312-162">1</span><span class="sxs-lookup"><span data-stu-id="4e312-162">1</span></span>|<span data-ttu-id="4e312-163">**应用图标 (选择**) ：16 像素透明应用徽标。</span><span class="sxs-lookup"><span data-stu-id="4e312-163">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="4e312-164">2</span><span class="sxs-lookup"><span data-stu-id="4e312-164">2</span></span>|<span data-ttu-id="4e312-165">**应用名称**</span><span class="sxs-lookup"><span data-stu-id="4e312-165">**App name**</span></span>|
|<span data-ttu-id="4e312-166">3</span><span class="sxs-lookup"><span data-stu-id="4e312-166">3</span></span>|<span data-ttu-id="4e312-167">**标头**：包括你的应用名称。</span><span class="sxs-lookup"><span data-stu-id="4e312-167">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="4e312-168">4 </span><span class="sxs-lookup"><span data-stu-id="4e312-168">4</span></span>|<span data-ttu-id="4e312-169">**关闭按钮**：关闭选项卡。始终使用右上方的关闭图标，而不是页脚中的操作。</span><span class="sxs-lookup"><span data-stu-id="4e312-169">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="4e312-170">5 </span><span class="sxs-lookup"><span data-stu-id="4e312-170">5</span></span>|<span data-ttu-id="4e312-171">**通知栏**：错误警报显示在标题正下方，将 iframe 内容向下推送 20 像素。</span><span class="sxs-lookup"><span data-stu-id="4e312-171">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="4e312-172">6 </span><span class="sxs-lookup"><span data-stu-id="4e312-172">6</span></span>|<span data-ttu-id="4e312-173">**iframe：** 显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="4e312-173">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="4e312-174">Spacing</span><span class="sxs-lookup"><span data-stu-id="4e312-174">Spacing</span></span>

<span data-ttu-id="4e312-175">优化会议选项卡以适合 280 像素宽的 iframe 区域中的边缘到边缘。</span><span class="sxs-lookup"><span data-stu-id="4e312-175">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="4e312-176">在 iframe 的左侧和右侧以及选项卡标题之间有 20 个像素的填充。</span><span class="sxs-lookup"><span data-stu-id="4e312-176">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="4e312-177">iframe 完全出血到选项卡底部。</span><span class="sxs-lookup"><span data-stu-id="4e312-177">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="示例显示会议中的选项卡间距尺寸。" border="false":::

### <a name="scrolling"></a><span data-ttu-id="4e312-179">滚动</span><span class="sxs-lookup"><span data-stu-id="4e312-179">Scrolling</span></span>

<span data-ttu-id="4e312-180">如果允许滚动，请记住以下几点：</span><span class="sxs-lookup"><span data-stu-id="4e312-180">Remember the following if you allow scrolling:</span></span>

* <span data-ttu-id="4e312-181">iframe 内容中的内容只应垂直滚动。</span><span class="sxs-lookup"><span data-stu-id="4e312-181">Content in the iframe contents should only scroll vertically.</span></span>
* <span data-ttu-id="4e312-182">用户只能看到他们滚动到的内容， (上方或) 。</span><span class="sxs-lookup"><span data-stu-id="4e312-182">Users should only see the content they've scrolled to (nothing above or below).</span></span> 
* <span data-ttu-id="4e312-183">滚动条是 iframe 内容的一部分。</span><span class="sxs-lookup"><span data-stu-id="4e312-183">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="示例显示如何滚动会议中的选项卡。" border="false":::

### <a name="navigation"></a><span data-ttu-id="4e312-185">导航</span><span class="sxs-lookup"><span data-stu-id="4e312-185">Navigation</span></span>

<span data-ttu-id="4e312-186">对于具有导航层或大量内容的方案，我们建议允许用户导航到辅助层。</span><span class="sxs-lookup"><span data-stu-id="4e312-186">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="4e312-187">用户必须能够返回到上一层。</span><span class="sxs-lookup"><span data-stu-id="4e312-187">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="示例显示会议内导航。" border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="4e312-189">使用会议内对话框</span><span class="sxs-lookup"><span data-stu-id="4e312-189">Use an in-meeting dialog</span></span>

<span data-ttu-id="4e312-190">会议中的对话框显示在会议Teams上。</span><span class="sxs-lookup"><span data-stu-id="4e312-190">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="4e312-191">它们需要用户的注意、确认或交互，但很细微，不会中断会议。</span><span class="sxs-lookup"><span data-stu-id="4e312-191">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="4e312-192">应谨慎使用这些模式，并针对轻型和面向任务的场景。</span><span class="sxs-lookup"><span data-stu-id="4e312-192">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="4e312-193">用例</span><span class="sxs-lookup"><span data-stu-id="4e312-193">Use cases</span></span>

<span data-ttu-id="4e312-194">会议内对话框由以下用户触发 (例如会议组织者) 可能希望参与者：</span><span class="sxs-lookup"><span data-stu-id="4e312-194">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="4e312-195">提供简短反馈</span><span class="sxs-lookup"><span data-stu-id="4e312-195">Provide brief feedback</span></span>
* <span data-ttu-id="4e312-196">参加简短调查或投票</span><span class="sxs-lookup"><span data-stu-id="4e312-196">Take a short survey or poll</span></span>
* <span data-ttu-id="4e312-197">提交审批</span><span class="sxs-lookup"><span data-stu-id="4e312-197">Submit approvals</span></span>
* <span data-ttu-id="4e312-198">获取提醒</span><span class="sxs-lookup"><span data-stu-id="4e312-198">Get reminders</span></span>

# <a name="desktop"></a>[<span data-ttu-id="4e312-199">桌面设备</span><span class="sxs-lookup"><span data-stu-id="4e312-199">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="示例演示如何使用会议内对话框。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="4e312-201">移动设备</span><span class="sxs-lookup"><span data-stu-id="4e312-201">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="示例演示如何在移动设备上使用会议内对话框。" border="false":::

---

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="4e312-203">结构：会议内对话框</span><span class="sxs-lookup"><span data-stu-id="4e312-203">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="示例显示会议对话的结构结构分析。" border="false":::

|<span data-ttu-id="4e312-205">计数器</span><span class="sxs-lookup"><span data-stu-id="4e312-205">Counter</span></span>|<span data-ttu-id="4e312-206">说明</span><span class="sxs-lookup"><span data-stu-id="4e312-206">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4e312-207">1</span><span class="sxs-lookup"><span data-stu-id="4e312-207">1</span></span>|<span data-ttu-id="4e312-208">**标头**：包括应用图标、名称、操作字符串和关闭图标。</span><span class="sxs-lookup"><span data-stu-id="4e312-208">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="4e312-209">2</span><span class="sxs-lookup"><span data-stu-id="4e312-209">2</span></span>|<span data-ttu-id="4e312-210">**iframe：** 显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="4e312-210">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="4e312-211">结构：会议内对话框标头</span><span class="sxs-lookup"><span data-stu-id="4e312-211">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="示例显示会议内对话框标题的结构结构分析。" border="false":::

<span data-ttu-id="4e312-213">有两个标头变量。</span><span class="sxs-lookup"><span data-stu-id="4e312-213">There are two header variants.</span></span> <span data-ttu-id="4e312-214">如果可能，将变体与头像一同使用，以强调对话框来自某人。</span><span class="sxs-lookup"><span data-stu-id="4e312-214">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="4e312-215">计数器</span><span class="sxs-lookup"><span data-stu-id="4e312-215">Counter</span></span>|<span data-ttu-id="4e312-216">说明</span><span class="sxs-lookup"><span data-stu-id="4e312-216">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4e312-217">1</span><span class="sxs-lookup"><span data-stu-id="4e312-217">1</span></span>|<span data-ttu-id="4e312-218">**头** 像：启动会议对话的人。</span><span class="sxs-lookup"><span data-stu-id="4e312-218">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="4e312-219">2</span><span class="sxs-lookup"><span data-stu-id="4e312-219">2</span></span>|<span data-ttu-id="4e312-220">**应用程序图标**</span><span class="sxs-lookup"><span data-stu-id="4e312-220">**App icon**</span></span>|
|<span data-ttu-id="4e312-221">3</span><span class="sxs-lookup"><span data-stu-id="4e312-221">3</span></span>|<span data-ttu-id="4e312-222">**应用名称**</span><span class="sxs-lookup"><span data-stu-id="4e312-222">**App name**</span></span>|
|<span data-ttu-id="4e312-223">4 </span><span class="sxs-lookup"><span data-stu-id="4e312-223">4</span></span>|<span data-ttu-id="4e312-224">**关闭按钮**：关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="4e312-224">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="4e312-225">5 </span><span class="sxs-lookup"><span data-stu-id="4e312-225">5</span></span>|<span data-ttu-id="4e312-226">**操作字符串**：通常描述启动对话框的人。</span><span class="sxs-lookup"><span data-stu-id="4e312-226">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior-in-meeting-dialogs"></a><span data-ttu-id="4e312-227">响应行为：会议内对话框</span><span class="sxs-lookup"><span data-stu-id="4e312-227">Responsive behavior: In-meeting dialogs</span></span>

<span data-ttu-id="4e312-228">根据不同的方案，会议内对话框的大小可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="4e312-228">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="4e312-229">确保保持填充和组件大小。</span><span class="sxs-lookup"><span data-stu-id="4e312-229">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="4e312-230">**Width：** 可以指定对话框的 iframe 的宽度（在支持的大小范围内的任何位置）。</span><span class="sxs-lookup"><span data-stu-id="4e312-230">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="4e312-231">**高度**：可以在支持的大小范围内的任何位置指定对话框的 iframe 的高度。</span><span class="sxs-lookup"><span data-stu-id="4e312-231">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="4e312-232">如果应用内容超出最大高度，还可以允许用户垂直滚动。</span><span class="sxs-lookup"><span data-stu-id="4e312-232">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="4e312-233">若要实现，使用 键指定宽度和 [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) 高度。</span><span class="sxs-lookup"><span data-stu-id="4e312-233">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="示例显示会议内对话框。宽度：最小为 280 像素 (248 像素的 iframe) 。最大为 460 像素 (428 像素的 iframe) 。高度：300 像素 (iframe) 。" border="false":::

## <a name="use-the-shared-meeting-stage"></a><span data-ttu-id="4e312-235">使用共享会议阶段</span><span class="sxs-lookup"><span data-stu-id="4e312-235">Use the shared meeting stage</span></span>

<span data-ttu-id="4e312-236">共享会议阶段可帮助会议参与者实时地与应用内容进行交互和协作。</span><span class="sxs-lookup"><span data-stu-id="4e312-236">Shared meeting stage helps meeting participants interact with and collaborate on app content in real-time.</span></span> <span data-ttu-id="4e312-237">例如，用户可以专注于编辑文档、使用白板进行集体讨论或查看仪表板。</span><span class="sxs-lookup"><span data-stu-id="4e312-237">For example, users can focus their call on editing a document, brainstorming with a whiteboard, or reviewing a dashboard.</span></span>

<span data-ttu-id="4e312-238">共享到会议阶段的应用占用的空间与共享屏幕相同。</span><span class="sxs-lookup"><span data-stu-id="4e312-238">Apps shared to the meeting stage occupy the same space as a shared screen.</span></span> <span data-ttu-id="4e312-239">该阶段将针对所有会议参与者进行重定向。</span><span class="sxs-lookup"><span data-stu-id="4e312-239">The stage reorients for all meeting participants.</span></span>

### <a name="use-cases"></a><span data-ttu-id="4e312-240">用例</span><span class="sxs-lookup"><span data-stu-id="4e312-240">Use cases</span></span>

<span data-ttu-id="4e312-241">共享会议阶段与协作和参与有关。</span><span class="sxs-lookup"><span data-stu-id="4e312-241">The shared meeting stage is all about collaboration and participation.</span></span> <span data-ttu-id="4e312-242">下面是帮助您入门的一些示例方案。</span><span class="sxs-lookup"><span data-stu-id="4e312-242">Here are some example scenarios to help you get started.</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="4e312-243">**编辑和查看**：深入了解仪表板，与通话中的每个人一起规划。</span><span class="sxs-lookup"><span data-stu-id="4e312-243">**Edit and review**: Dive into dashboards and planning with everyone on the call.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-edit-review.png" alt-text="示例显示共享会议阶段正在审阅的仪表板。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

<span data-ttu-id="4e312-245">**白板：** 在共享画布上一起绘制和创意。</span><span class="sxs-lookup"><span data-stu-id="4e312-245">**Whiteboard**: Draw and ideate together on a shared canvas.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-whiteboard.png" alt-text="示例显示共享会议阶段上的白板。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="1":::

<span data-ttu-id="4e312-247">**测验**：使用交互式材料测试知识和获取见解。</span><span class="sxs-lookup"><span data-stu-id="4e312-247">**Quiz**: Test knowledge and gain insights with interactive materials.</span></span>

   :::column-end:::
   :::column span="3":::

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-quiz.png" alt-text="示例在共享会议阶段显示测验。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="anatomy-shared-meeting-stage"></a><span data-ttu-id="4e312-249">结构：共享会议阶段</span><span class="sxs-lookup"><span data-stu-id="4e312-249">Anatomy: Shared meeting stage</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/shared-meeting-stage-anatomy.png" alt-text="图像显示共享会议阶段的设计结构。" border="false":::

|<span data-ttu-id="4e312-251">计数器</span><span class="sxs-lookup"><span data-stu-id="4e312-251">Counter</span></span>|<span data-ttu-id="4e312-252">说明</span><span class="sxs-lookup"><span data-stu-id="4e312-252">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4e312-253">1</span><span class="sxs-lookup"><span data-stu-id="4e312-253">1</span></span>|<span data-ttu-id="4e312-254">**应用图标**：突出显示的图标表示应用的"会议中"选项卡已打开。</span><span class="sxs-lookup"><span data-stu-id="4e312-254">**App icon**: The highlighted icon indicates the app's in-meeting tab is open.</span></span>|
|<span data-ttu-id="4e312-255">2</span><span class="sxs-lookup"><span data-stu-id="4e312-255">2</span></span>|<span data-ttu-id="4e312-256">**共享到会议阶段按钮**：将应用共享到会议阶段的入口点。</span><span class="sxs-lookup"><span data-stu-id="4e312-256">**Share to meeting stage button**: The entry point to share the app to the meeting stage.</span></span> <span data-ttu-id="4e312-257">显示是否将应用配置为使用共享会议阶段。</span><span class="sxs-lookup"><span data-stu-id="4e312-257">Displays if you configure your app to use the shared meeting stage.</span></span>|
|<span data-ttu-id="4e312-258">3</span><span class="sxs-lookup"><span data-stu-id="4e312-258">3</span></span>|<span data-ttu-id="4e312-259">**iframe：** 显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="4e312-259">**iframe**: Displays your app content.</span></span>|
|<span data-ttu-id="4e312-260">4 </span><span class="sxs-lookup"><span data-stu-id="4e312-260">4</span></span>|<span data-ttu-id="4e312-261">**"停止共享"** 按钮：停止将应用共享到会议阶段。</span><span class="sxs-lookup"><span data-stu-id="4e312-261">**Stop sharing button**: Stops sharing the app to the meeting stage.</span></span> <span data-ttu-id="4e312-262">仅显示启动共享的参与者。</span><span class="sxs-lookup"><span data-stu-id="4e312-262">Displays only for the participant who started the share.</span></span>|
|<span data-ttu-id="4e312-263">5 </span><span class="sxs-lookup"><span data-stu-id="4e312-263">5</span></span>|<span data-ttu-id="4e312-264">**演示者属性**：显示共享应用的参与者的姓名。</span><span class="sxs-lookup"><span data-stu-id="4e312-264">**Presenter attribution**: Displays the name of the participant who shared the app.</span></span>|

### <a name="responsive-behavior-shared-meeting-stage"></a><span data-ttu-id="4e312-265">响应行为：共享会议阶段</span><span class="sxs-lookup"><span data-stu-id="4e312-265">Responsive behavior: Shared meeting stage</span></span>

<span data-ttu-id="4e312-266">共享到会议阶段的应用的大小因会议状态和用户调整窗口大小而异。</span><span class="sxs-lookup"><span data-stu-id="4e312-266">Apps shared to the meeting stage vary in size based on the state of the meeting and how the user resizes the window.</span></span> <span data-ttu-id="4e312-267">保持填充和导航和控件的响应式布局，就像在浏览器中一样。</span><span class="sxs-lookup"><span data-stu-id="4e312-267">Maintain padding and the responsive layout of navigation and controls just as you would in a browser.</span></span>

* <span data-ttu-id="4e312-268">侧 **面板**：会议期间，用户随时都可以打开侧面板，以聊天、查看名单或使用应用 (即会议中的选项卡) 。</span><span class="sxs-lookup"><span data-stu-id="4e312-268">**Side panel**: A user can have the side panel open at any time during a meeting to chat, view the roster, or use an app (i.e., in-meeting tab).</span></span> <span data-ttu-id="4e312-269">面板打开时，阶段动态重新排列。</span><span class="sxs-lookup"><span data-stu-id="4e312-269">The stage dynamically rearranges when the panel is open.</span></span>
* <span data-ttu-id="4e312-270">**视频和音频网格**：视频和音频网格始终可见，以显示会议参与者。</span><span class="sxs-lookup"><span data-stu-id="4e312-270">**Video and audio grid**: The video and audio grid is always visible to show meeting participants.</span></span> <span data-ttu-id="4e312-271">当用户聚焦或固定会议中的某人时，这将增加参与者网格的高度或宽度，具体取决于方向。</span><span class="sxs-lookup"><span data-stu-id="4e312-271">When a user spotlights or pins someone in the meeting, this increases the height or width of the participant grid depending on the orientation.</span></span>

#### <a name="meeting-stage-without-side-panel"></a><span data-ttu-id="4e312-272">没有侧 (面板的) </span><span class="sxs-lookup"><span data-stu-id="4e312-272">Meeting stage (without side panel)</span></span>

<span data-ttu-id="4e312-273">当侧面板未打开时，默认情况下，会议阶段为 994x678 像素，并且至少为 792x382 像素。</span><span class="sxs-lookup"><span data-stu-id="4e312-273">When the side panel isn't open, the meeting stage is 994x678 pixels by default and can be a minimum 792x382 pixels.</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-no-side-panel.png" alt-text="显示关闭侧面板时共享会议阶段响应的图像。" border="false":::

#### <a name="meeting-stage-with-side-panel"></a><span data-ttu-id="4e312-275">带侧 (面板的) </span><span class="sxs-lookup"><span data-stu-id="4e312-275">Meeting stage (with side panel)</span></span>

<span data-ttu-id="4e312-276">侧面板打开时，默认情况下，会议阶段为 918x540 像素，并且至少为 472x382 像素。</span><span class="sxs-lookup"><span data-stu-id="4e312-276">When the side panel is open, the meeting stage is 918x540 pixels by default and can be a minimum 472x382 pixels.</span></span>

:::image type="content" source="~/assets/images/apps-in-meetings/meeting-stage-with-side-panel.png" alt-text="显示侧面板打开时共享会议阶段响应的图像。" border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="4e312-278">会议后</span><span class="sxs-lookup"><span data-stu-id="4e312-278">After a meeting</span></span>

<span data-ttu-id="4e312-279">可以在会议结束后返回到会议并查看应用内容。</span><span class="sxs-lookup"><span data-stu-id="4e312-279">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="4e312-280">本示例中，会议组织者可以在 **Contoso** 选项卡中查看投票结果。 (注意：从设计的角度来看，会议前和会议后选项卡体验之间没有区别。) </span><span class="sxs-lookup"><span data-stu-id="4e312-280">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="示例插图显示会议后选项卡。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="4e312-282">最佳实践</span><span class="sxs-lookup"><span data-stu-id="4e312-282">Best practices</span></span>

<span data-ttu-id="4e312-283">使用上述建议打造优质应用体验。</span><span class="sxs-lookup"><span data-stu-id="4e312-283">Use these recommendations to create a quality app experience.</span></span>

### <a name="interactions"></a><span data-ttu-id="4e312-284">交互</span><span class="sxs-lookup"><span data-stu-id="4e312-284">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="显示如何限制交互数的示例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="4e312-286">操作：限制交互数</span><span class="sxs-lookup"><span data-stu-id="4e312-286">Do: Limit the number of interactions</span></span>

<span data-ttu-id="4e312-287">对于会议内对话框，删除不帮助用户快速完成某些内容的不必要内容。</span><span class="sxs-lookup"><span data-stu-id="4e312-287">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="显示如何不引入不必要的元素的示例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="4e312-289">请勿：引入不必要的元素</span><span class="sxs-lookup"><span data-stu-id="4e312-289">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="4e312-290">具有多个交互的单个会议对话可能会干扰呼叫。</span><span class="sxs-lookup"><span data-stu-id="4e312-290">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-do.png" alt-text="显示如何创建聚焦环境的示例。" border="false":::

#### <a name="do-create-a-focused-environment"></a><span data-ttu-id="4e312-292">要执行：创建重点环境</span><span class="sxs-lookup"><span data-stu-id="4e312-292">Do: Create a focused environment</span></span>

<span data-ttu-id="4e312-293">我们建议将应用体验的范围仅保留为会议阶段。</span><span class="sxs-lookup"><span data-stu-id="4e312-293">We recommend keeping your app’s experience scoped to just the meeting stage.</span></span> <span data-ttu-id="4e312-294">你可以将侧面板中的"会议内"选项卡用作某些方案的辅助专用视图。</span><span class="sxs-lookup"><span data-stu-id="4e312-294">You can use an in-meeting tab in the side panel as a secondary, private view for certain scenarios.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-shared-stage-dont.png" alt-text="显示会议期间如何不包括竞争图面的示例。" border="false":::

#### <a name="dont-include-competing-surfaces"></a><span data-ttu-id="4e312-296">不要：包括竞争面</span><span class="sxs-lookup"><span data-stu-id="4e312-296">Don't: Include competing surfaces</span></span>

<span data-ttu-id="4e312-297">你的应用应仅要求用户一次专注于一个图面，无论它是在阶段进行协作还是响应会议内对话框。</span><span class="sxs-lookup"><span data-stu-id="4e312-297">Your app should only ask users to focus on a single surface a time, whether it's collaborating on the stage or responding to an in-meeting dialog.</span></span> <span data-ttu-id="4e312-298"> (注意：当你的应用处于阶段时，你无法保留由其他应用触发的) </span><span class="sxs-lookup"><span data-stu-id="4e312-298">(Note: You can’t keep dialogs being triggered by other apps while your app is on the stage.)</span></span> 

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="4e312-299">布局</span><span class="sxs-lookup"><span data-stu-id="4e312-299">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="显示如何使用单列对话框布局的示例。" border="false":::

#### <a name="do-use-a-one-column-dialog"></a><span data-ttu-id="4e312-301">操作：使用单列对话框</span><span class="sxs-lookup"><span data-stu-id="4e312-301">Do: Use a one-column dialog</span></span>

<span data-ttu-id="4e312-302">由于对话框位于会议阶段的中心，任务完成应快速而简单，以避免用户感到沮丧。</span><span class="sxs-lookup"><span data-stu-id="4e312-302">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="显示不应使会议扩展空间混乱的示例。" border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="4e312-304">Don't： Clutter the space</span><span class="sxs-lookup"><span data-stu-id="4e312-304">Don't: Clutter the space</span></span>

<span data-ttu-id="4e312-305">密集或结构过度的内容可能会让人分心和不知所措，尤其是在会议期间。</span><span class="sxs-lookup"><span data-stu-id="4e312-305">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="显示单列选项卡布局的示例。" border="false":::

#### <a name="do-use-a-one-column-tab"></a><span data-ttu-id="4e312-307">操作：使用单列选项卡</span><span class="sxs-lookup"><span data-stu-id="4e312-307">Do: Use a one-column tab</span></span>

<span data-ttu-id="4e312-308">鉴于"会议"选项卡的窄性质，我们强烈建议在单个列中显示内容。</span><span class="sxs-lookup"><span data-stu-id="4e312-308">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="显示具有多个列的选项卡的示例。" border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="4e312-310">请勿：使用多个列</span><span class="sxs-lookup"><span data-stu-id="4e312-310">Don't: Use multiple columns</span></span>

<span data-ttu-id="4e312-311">由于"会议内"选项卡的空间有限，因此不建议使用具有多个列的布局。</span><span class="sxs-lookup"><span data-stu-id="4e312-311">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="4e312-312">控件</span><span class="sxs-lookup"><span data-stu-id="4e312-312">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="显示如何右对齐主要控件的示例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="4e312-314">应做：右对齐主要操作</span><span class="sxs-lookup"><span data-stu-id="4e312-314">Do: Right align the primary action</span></span>

<span data-ttu-id="4e312-315">我们建议将视觉最重的操作定位到最右边的位置。</span><span class="sxs-lookup"><span data-stu-id="4e312-315">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="显示不应左对齐主要控件的示例。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="4e312-317">不：左对齐或居中对齐操作</span><span class="sxs-lookup"><span data-stu-id="4e312-317">Don't: Left or center align actions</span></span>

<span data-ttu-id="4e312-318">这偏离了用于Teams控件放置的标准模式，并且可能会与顶部对话框后面的对话框冲突。</span><span class="sxs-lookup"><span data-stu-id="4e312-318">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a><span data-ttu-id="4e312-319">滚动</span><span class="sxs-lookup"><span data-stu-id="4e312-319">Scrolling</span></span>

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="在会议中的选项卡中显示垂直滚动的示例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-do.png" alt-text="显示共享会议阶段中的垂直滚动的示例。" border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="4e312-322">操作：垂直滚动</span><span class="sxs-lookup"><span data-stu-id="4e312-322">Do: Scroll vertically</span></span>

<span data-ttu-id="4e312-323">用户预期垂直滚动Teams (和任何其他位置) 。</span><span class="sxs-lookup"><span data-stu-id="4e312-323">Users expect vertical scrolling in Teams (and elsewhere).</span></span> <span data-ttu-id="4e312-324">如果你具有创意画布（如白板，用户可以在 x 和 y 轴上平移）。这可能不适用。</span><span class="sxs-lookup"><span data-stu-id="4e312-324">This may not apply if you have a creative canvas, such as a whiteboard, which users can pan across the x and y axis.</span></span>

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="显示会议内选项卡中水平滚动的示例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-scroll-dont.png" alt-text="显示共享会议阶段中的水平滚动的示例。" border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="4e312-327">不：水平滚动</span><span class="sxs-lookup"><span data-stu-id="4e312-327">Don't: Scroll horizontally</span></span>

<span data-ttu-id="4e312-328">在包括会议环境或会议Teams (，水平滚动不是预期) 。</span><span class="sxs-lookup"><span data-stu-id="4e312-328">Horizontal scrolling isn’t an expected behavior in Teams (including the meeting environment).</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="4e312-329">工作流</span><span class="sxs-lookup"><span data-stu-id="4e312-329">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="在会议选项卡中显示复杂方案的示例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="4e312-331">Do： Surface complex scenarios in the in-meeting tab</span><span class="sxs-lookup"><span data-stu-id="4e312-331">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="4e312-332">如果你的应用包含多个任务，我们强烈建议将会议中的选项卡与单列布局一同使用。</span><span class="sxs-lookup"><span data-stu-id="4e312-332">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="在会议对话中显示复杂方案的示例。" border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="4e312-334">请勿：使会议对话变得复杂</span><span class="sxs-lookup"><span data-stu-id="4e312-334">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="4e312-335">会议内对话框用于简短交互。</span><span class="sxs-lookup"><span data-stu-id="4e312-335">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="4e312-336">主题</span><span class="sxs-lookup"><span data-stu-id="4e312-336">Theming</span></span>

:::row:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="显示具有深色主题的会议扩展名的示例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-do.png" alt-text="另一个示例显示具有深色主题的会议扩展。" border="false":::

#### <a name="do-focus-on-dark-theme"></a><span data-ttu-id="4e312-339">应做：专注于深色主题</span><span class="sxs-lookup"><span data-stu-id="4e312-339">Do: Focus on dark theme</span></span>

<span data-ttu-id="4e312-340">Teams会议针对深色主题进行了优化，以帮助减少视觉和认知噪音，以便用户可以专注于讨论和共享内容。</span><span class="sxs-lookup"><span data-stu-id="4e312-340">Teams meetings are optimized for dark theme to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="4e312-341">请记住特定类型的应用 (如白板和文档编辑) 不需要深色画布。</span><span class="sxs-lookup"><span data-stu-id="4e312-341">Keep in mind certain types of apps (such as whiteboarding and document editing) don't need a dark canvas.</span></span>

   :::column-end:::
   :::column span="":::

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="显示颜色与会议主题不匹配的会议扩展的示例。" border="false":::

:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-theming-dont.png" alt-text="另一个示例显示具有与会议主题不匹配的颜色的会议扩展。" border="false":::

#### <a name="dont-use-unfamiliar-colors"></a><span data-ttu-id="4e312-344">请勿：使用不熟悉的颜色</span><span class="sxs-lookup"><span data-stu-id="4e312-344">Don't: Use unfamiliar colors</span></span>

<span data-ttu-id="4e312-345">与会议环境发生冲突的颜色可能会分散注意力，对会议环境Teams。</span><span class="sxs-lookup"><span data-stu-id="4e312-345">Colors that clash with the meeting environment may be distracting and appear less native to Teams.</span></span> <span data-ttu-id="4e312-346">了解颜色渐变[Teams，](https://developer.microsoft.com/fluentui#/styles/web/colors/products)包括调用主题中性色。</span><span class="sxs-lookup"><span data-stu-id="4e312-346">Learn about the Teams [color ramp](https://developer.microsoft.com/fluentui#/styles/web/colors/products), including call theme neutrals.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="4e312-347">导航</span><span class="sxs-lookup"><span data-stu-id="4e312-347">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="显示具有后退按钮的会议扩展名的示例。" border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="4e312-349">操作：具有"后退"按钮</span><span class="sxs-lookup"><span data-stu-id="4e312-349">Do: Have a back button</span></span>

<span data-ttu-id="4e312-350">如果在会议选项卡中具有多个导航层，用户必须能够返回到其以前的视图。</span><span class="sxs-lookup"><span data-stu-id="4e312-350">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="显示具有两个消除按钮的会议扩展的示例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="4e312-352">请勿：包含其他消除按钮</span><span class="sxs-lookup"><span data-stu-id="4e312-352">Don't: Include another dismiss button</span></span>

<span data-ttu-id="4e312-353">提供关闭会议内选项卡内容的选项可能会导致问题，因为标题中已有一个按钮可以关闭会议中的选项卡本身。</span><span class="sxs-lookup"><span data-stu-id="4e312-353">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="显示会议选项卡 (模式或) 模块的示例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="4e312-355">警告：避免会议内选项卡中的模式</span><span class="sxs-lookup"><span data-stu-id="4e312-355">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="4e312-356">模式 (也称为任务模块) 在已经较窄的会议内选项卡中可能会封装和遮盖内容。</span><span class="sxs-lookup"><span data-stu-id="4e312-356">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive-behavior"></a><span data-ttu-id="4e312-357">响应行为</span><span class="sxs-lookup"><span data-stu-id="4e312-357">Responsive behavior</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-do.png" alt-text="显示如何正确调整会议扩展大小的示例。" border="false":::

#### <a name="do-resize-and-scale-your-app-responsively"></a><span data-ttu-id="4e312-359">应做：响应式调整应用大小和缩放应用</span><span class="sxs-lookup"><span data-stu-id="4e312-359">Do: Resize and scale your app responsively</span></span>

<span data-ttu-id="4e312-360">应用内容应在较小的窗口中动态调整大小和缩小。</span><span class="sxs-lookup"><span data-stu-id="4e312-360">App content should dynamically resize and condense in smaller windows.</span></span> <span data-ttu-id="4e312-361">使应用的主导航和任何浮动控件可见。</span><span class="sxs-lookup"><span data-stu-id="4e312-361">Keep your app’s main navigation and any floating controls visible.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/shared-meeting-stage-responsiveness-dont.png" alt-text="显示如何正确调整会议扩展大小的示例。" border="false":::

#### <a name="dont-crop-or-clip-primary-ui-components"></a><span data-ttu-id="4e312-363">不：裁剪或剪裁主要 UI 组件</span><span class="sxs-lookup"><span data-stu-id="4e312-363">Don't: Crop or clip primary UI components</span></span>

<span data-ttu-id="4e312-364">浮动导航和屏幕外控件和需要滚动查找可能会让用户感到困惑。</span><span class="sxs-lookup"><span data-stu-id="4e312-364">Floating navigation and controls off screen and requiring a scroll to find can be confusing for users.</span></span> <span data-ttu-id="4e312-365">当应用内容无法容纳在 iframe 中时，不应水平滚动。</span><span class="sxs-lookup"><span data-stu-id="4e312-365">Your app content shouldn’t scroll horizontally when it can't fit in the iframe.</span></span>

   :::column-end:::
:::row-end:::

## <a name="next-step"></a><span data-ttu-id="4e312-366">后续步骤</span><span class="sxs-lookup"><span data-stu-id="4e312-366">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4e312-367">为会议配置应用</span><span class="sxs-lookup"><span data-stu-id="4e312-367">Configure your app for meetings</span></span>](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
