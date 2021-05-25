---
title: 设计会议扩展
author: heath-hamilton
description: 了解如何在会议Teams设计应用并获取 Microsoft Teams UI 工具包。
ms.author: lajanuar
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 33b11a6dfc759fabd54ca2fe2c68978a5d5d1475
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644615"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="b59c1-103">设计会议Microsoft Teams扩展</span><span class="sxs-lookup"><span data-stu-id="b59c1-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="b59c1-104">你可以创建应用来使会议更加高效。</span><span class="sxs-lookup"><span data-stu-id="b59c1-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="b59c1-105">例如，要求用户在呼叫过程中完成调查或发送不会中断会议流的快速提醒。</span><span class="sxs-lookup"><span data-stu-id="b59c1-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="b59c1-106">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="b59c1-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="b59c1-107">你可以找到更全面的设计指南，包括你可以根据需要获取和修改的元素，Microsoft Teams UI 工具包。</span><span class="sxs-lookup"><span data-stu-id="b59c1-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b59c1-108">获取 Microsoft Teams UI Kit （用户）</span><span class="sxs-lookup"><span data-stu-id="b59c1-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="b59c1-109">添加会议扩展</span><span class="sxs-lookup"><span data-stu-id="b59c1-109">Add a meeting extension</span></span>

<span data-ttu-id="b59c1-110">用户可以在会议之前和会议期间添加会议扩展名。</span><span class="sxs-lookup"><span data-stu-id="b59c1-110">Users can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="b59c1-111">他们还可以直接从应用商店添加特定会议Teams应用。</span><span class="sxs-lookup"><span data-stu-id="b59c1-111">They also can add an app for a specific meeting directly from the Teams store.</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="b59c1-112">在会议前添加</span><span class="sxs-lookup"><span data-stu-id="b59c1-112">Add before a meeting</span></span>

<span data-ttu-id="b59c1-113">在会议详细信息中，用户可以选择"添加选项卡 **+"** 以打开应用飞出控件并查找针对会议优化的应用。</span><span class="sxs-lookup"><span data-stu-id="b59c1-113">In the meeting details, users can select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="示例演示如何在会议之前添加会议扩展名。" border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="b59c1-115">会议期间添加</span><span class="sxs-lookup"><span data-stu-id="b59c1-115">Add during a meeting</span></span>

# <a name="desktop"></a>[<span data-ttu-id="b59c1-116">桌面</span><span class="sxs-lookup"><span data-stu-id="b59c1-116">Desktop</span></span>](#tab/desktop)

在会议中，**用户可以选择"** 更多 :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **添加应用**"，然后选择他们需要的应用。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="示例演示如何在会议期间添加会议扩展名。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="b59c1-119">移动</span><span class="sxs-lookup"><span data-stu-id="b59c1-119">Mobile</span></span>](#tab/mobile)

在会议中， **用户可以选择"** 更多 :::image type="icon" source="../../assets/icons/teams-client-more.png"::: "并选择他们需要的应用。

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-add-during-meeting.png" alt-text="示例演示如何在移动会议期间添加会议扩展。" border="false":::

---

## <a name="before-a-meeting"></a><span data-ttu-id="b59c1-122">会议前</span><span class="sxs-lookup"><span data-stu-id="b59c1-122">Before a meeting</span></span>

<span data-ttu-id="b59c1-123">在会议之前，用户可以在选项卡中添加内容。以下示例显示了一个草稿调查问题，人员将在呼叫过程中回答该问题。</span><span class="sxs-lookup"><span data-stu-id="b59c1-123">Prior to a meeting, users can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="示例演示如何在呼叫之前应用会议详细信息中的内容。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="b59c1-125">结构：会议 (会议之前和之后) </span><span class="sxs-lookup"><span data-stu-id="b59c1-125">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="示例显示会议之前和之后的会议选项卡的结构结构分析。" border="false":::

|<span data-ttu-id="b59c1-127">计数器</span><span class="sxs-lookup"><span data-stu-id="b59c1-127">Counter</span></span>|<span data-ttu-id="b59c1-128">说明</span><span class="sxs-lookup"><span data-stu-id="b59c1-128">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b59c1-129">1</span><span class="sxs-lookup"><span data-stu-id="b59c1-129">1</span></span>|<span data-ttu-id="b59c1-130">**选项卡名称**：选项卡的导航标签。</span><span class="sxs-lookup"><span data-stu-id="b59c1-130">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="b59c1-131">2</span><span class="sxs-lookup"><span data-stu-id="b59c1-131">2</span></span>|<span data-ttu-id="b59c1-132">**Tab 溢出**：打开选项卡操作，如重命名和删除。</span><span class="sxs-lookup"><span data-stu-id="b59c1-132">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="b59c1-133">3</span><span class="sxs-lookup"><span data-stu-id="b59c1-133">3</span></span>|<span data-ttu-id="b59c1-134">**iframe：** 显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="b59c1-134">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="b59c1-135">使用 UI 模板进行设计</span><span class="sxs-lookup"><span data-stu-id="b59c1-135">Designing with UI templates</span></span>

<span data-ttu-id="b59c1-136">使用以下 UI 模板Teams之一来帮助设计会议选项卡：</span><span class="sxs-lookup"><span data-stu-id="b59c1-136">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="b59c1-137">[列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目采取操作。</span><span class="sxs-lookup"><span data-stu-id="b59c1-137">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="b59c1-138">[任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为看板或街道）是一组卡片，通常用于跟踪工作项或票证的状态。</span><span class="sxs-lookup"><span data-stu-id="b59c1-138">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="b59c1-139">[仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是包含多个卡片的画布，可提供数据或内容的概述。</span><span class="sxs-lookup"><span data-stu-id="b59c1-139">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="b59c1-140">[表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单用于以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="b59c1-140">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="b59c1-141">[空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="b59c1-141">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="b59c1-142">[左侧导航](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav)：如果你的选项卡需要一些导航，左侧导航组件会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="b59c1-142">[Left nav](../../concepts/design/design-teams-app-advanced-ui-components.md#left-nav): The left nav component can help if your tab requires some navigation.</span></span> <span data-ttu-id="b59c1-143">通常，应该将导航保持在最低程度。</span><span class="sxs-lookup"><span data-stu-id="b59c1-143">In general, you should keep navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="b59c1-144">使用会议内选项卡</span><span class="sxs-lookup"><span data-stu-id="b59c1-144">Use an in-meeting tab</span></span>

<span data-ttu-id="b59c1-145">"会议内"选项卡是一块画布，用于增强会议期间的协作。</span><span class="sxs-lookup"><span data-stu-id="b59c1-145">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="b59c1-146">与会者可以通过共享视图或基于角色的视图在会议阶段外的专用空间中查看应用内容并与之交互。</span><span class="sxs-lookup"><span data-stu-id="b59c1-146">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="b59c1-147">用例</span><span class="sxs-lookup"><span data-stu-id="b59c1-147">Use cases</span></span>

<span data-ttu-id="b59c1-148">人们可能会使用"会议内"选项卡：</span><span class="sxs-lookup"><span data-stu-id="b59c1-148">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="b59c1-149">提供详细反馈。</span><span class="sxs-lookup"><span data-stu-id="b59c1-149">Provide detailed feedback.</span></span> <span data-ttu-id="b59c1-150">例如，评估一个职位候选人。</span><span class="sxs-lookup"><span data-stu-id="b59c1-150">For example, evaluate a job candidate.</span></span>
* <span data-ttu-id="b59c1-151">为会议参与者创建投票、调查或任务项。</span><span class="sxs-lookup"><span data-stu-id="b59c1-151">Create a poll, survey, or task item for the meeting participants.</span></span>
* <span data-ttu-id="b59c1-152">显示与会议相关的备注。</span><span class="sxs-lookup"><span data-stu-id="b59c1-152">Display notes relevant to the meeting.</span></span> <span data-ttu-id="b59c1-153">例如，有关销售线索的信息。</span><span class="sxs-lookup"><span data-stu-id="b59c1-153">For example, information about a sales lead.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="b59c1-154">桌面</span><span class="sxs-lookup"><span data-stu-id="b59c1-154">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="示例演示如何在会议中的选项卡中显示投票内容。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="b59c1-156">移动</span><span class="sxs-lookup"><span data-stu-id="b59c1-156">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-tab.png" alt-text="示例演示如何在移动设备上的&quot;会议&quot;选项卡中显示投票内容。" border="false":::

---

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="b59c1-158">结构：会议内选项卡</span><span class="sxs-lookup"><span data-stu-id="b59c1-158">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="示例显示会议内选项卡的结构结构分析。" border="false":::

|<span data-ttu-id="b59c1-160">计数器</span><span class="sxs-lookup"><span data-stu-id="b59c1-160">Counter</span></span>|<span data-ttu-id="b59c1-161">说明</span><span class="sxs-lookup"><span data-stu-id="b59c1-161">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b59c1-162">1</span><span class="sxs-lookup"><span data-stu-id="b59c1-162">1</span></span>|<span data-ttu-id="b59c1-163">**应用图标 (选择**) ：16 像素透明应用徽标。</span><span class="sxs-lookup"><span data-stu-id="b59c1-163">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="b59c1-164">2</span><span class="sxs-lookup"><span data-stu-id="b59c1-164">2</span></span>|<span data-ttu-id="b59c1-165">**应用名称**</span><span class="sxs-lookup"><span data-stu-id="b59c1-165">**App name**</span></span>|
|<span data-ttu-id="b59c1-166">3</span><span class="sxs-lookup"><span data-stu-id="b59c1-166">3</span></span>|<span data-ttu-id="b59c1-167">**标头**：包括你的应用名称。</span><span class="sxs-lookup"><span data-stu-id="b59c1-167">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="b59c1-168">4 </span><span class="sxs-lookup"><span data-stu-id="b59c1-168">4</span></span>|<span data-ttu-id="b59c1-169">**关闭按钮**：关闭选项卡。始终使用右上方的关闭图标，而不是页脚中的操作。</span><span class="sxs-lookup"><span data-stu-id="b59c1-169">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="b59c1-170">5 </span><span class="sxs-lookup"><span data-stu-id="b59c1-170">5</span></span>|<span data-ttu-id="b59c1-171">**通知栏**：错误警报显示在标题正下方，将 iframe 内容向下推送 20 像素。</span><span class="sxs-lookup"><span data-stu-id="b59c1-171">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="b59c1-172">6 </span><span class="sxs-lookup"><span data-stu-id="b59c1-172">6</span></span>|<span data-ttu-id="b59c1-173">**iframe：** 显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="b59c1-173">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="b59c1-174">Spacing</span><span class="sxs-lookup"><span data-stu-id="b59c1-174">Spacing</span></span>

<span data-ttu-id="b59c1-175">优化会议选项卡以适合 280 像素宽的 iframe 区域中的边缘到边缘。</span><span class="sxs-lookup"><span data-stu-id="b59c1-175">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="b59c1-176">在 iframe 的左侧和右侧以及选项卡标题之间有 20 个像素的填充。</span><span class="sxs-lookup"><span data-stu-id="b59c1-176">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="b59c1-177">iframe 完全出血到选项卡底部。</span><span class="sxs-lookup"><span data-stu-id="b59c1-177">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="示例显示会议中的选项卡间距尺寸。" border="false":::

### <a name="scrolling"></a><span data-ttu-id="b59c1-179">滚动</span><span class="sxs-lookup"><span data-stu-id="b59c1-179">Scrolling</span></span>

<span data-ttu-id="b59c1-180">Iframe 内容应垂直滚动。</span><span class="sxs-lookup"><span data-stu-id="b59c1-180">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="b59c1-181">只能查看滚动到的内容， (上方或) 。</span><span class="sxs-lookup"><span data-stu-id="b59c1-181">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="b59c1-182">滚动条是 iframe 内容的一部分。</span><span class="sxs-lookup"><span data-stu-id="b59c1-182">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="示例显示如何滚动会议中的选项卡。" border="false":::

### <a name="navigation"></a><span data-ttu-id="b59c1-184">导航</span><span class="sxs-lookup"><span data-stu-id="b59c1-184">Navigation</span></span>

<span data-ttu-id="b59c1-185">对于具有导航层或大量内容的方案，我们建议允许用户导航到辅助层。</span><span class="sxs-lookup"><span data-stu-id="b59c1-185">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="b59c1-186">用户必须能够返回到上一层。</span><span class="sxs-lookup"><span data-stu-id="b59c1-186">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="示例显示会议内导航。" border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="b59c1-188">使用会议内对话框</span><span class="sxs-lookup"><span data-stu-id="b59c1-188">Use an in-meeting dialog</span></span>

<span data-ttu-id="b59c1-189">会议中的对话框显示在会议Teams上。</span><span class="sxs-lookup"><span data-stu-id="b59c1-189">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="b59c1-190">它们需要用户的注意、确认或交互，但很细微，不会中断会议。</span><span class="sxs-lookup"><span data-stu-id="b59c1-190">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="b59c1-191">应谨慎使用这些模式，并针对轻型和面向任务的场景。</span><span class="sxs-lookup"><span data-stu-id="b59c1-191">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="b59c1-192">用例</span><span class="sxs-lookup"><span data-stu-id="b59c1-192">Use cases</span></span>

<span data-ttu-id="b59c1-193">会议内对话框由以下用户触发 (例如会议组织者) 可能希望参与者：</span><span class="sxs-lookup"><span data-stu-id="b59c1-193">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="b59c1-194">提供简短反馈</span><span class="sxs-lookup"><span data-stu-id="b59c1-194">Provide brief feedback</span></span>
* <span data-ttu-id="b59c1-195">参加简短调查或投票</span><span class="sxs-lookup"><span data-stu-id="b59c1-195">Take a short survey or poll</span></span>
* <span data-ttu-id="b59c1-196">提交审批</span><span class="sxs-lookup"><span data-stu-id="b59c1-196">Submit approvals</span></span>
* <span data-ttu-id="b59c1-197">获取提醒</span><span class="sxs-lookup"><span data-stu-id="b59c1-197">Get reminders</span></span>

# <a name="desktop"></a>[<span data-ttu-id="b59c1-198">桌面</span><span class="sxs-lookup"><span data-stu-id="b59c1-198">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="示例演示如何使用会议内对话框。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="b59c1-200">移动</span><span class="sxs-lookup"><span data-stu-id="b59c1-200">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/apps-in-meetings/mobile-use-in-meeting-dialog.png" alt-text="示例演示如何在移动设备上使用会议内对话框。" border="false":::

---

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="b59c1-202">结构：会议内对话框</span><span class="sxs-lookup"><span data-stu-id="b59c1-202">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="示例显示会议对话的结构结构分析。" border="false":::

|<span data-ttu-id="b59c1-204">计数器</span><span class="sxs-lookup"><span data-stu-id="b59c1-204">Counter</span></span>|<span data-ttu-id="b59c1-205">说明</span><span class="sxs-lookup"><span data-stu-id="b59c1-205">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b59c1-206">1</span><span class="sxs-lookup"><span data-stu-id="b59c1-206">1</span></span>|<span data-ttu-id="b59c1-207">**标头**：包括应用图标、名称、操作字符串和关闭图标。</span><span class="sxs-lookup"><span data-stu-id="b59c1-207">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="b59c1-208">2</span><span class="sxs-lookup"><span data-stu-id="b59c1-208">2</span></span>|<span data-ttu-id="b59c1-209">**iframe：** 显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="b59c1-209">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="b59c1-210">结构：会议内对话框标头</span><span class="sxs-lookup"><span data-stu-id="b59c1-210">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="示例显示会议内对话框标题的结构结构分析。" border="false":::

<span data-ttu-id="b59c1-212">有两个标头变量。</span><span class="sxs-lookup"><span data-stu-id="b59c1-212">There are two header variants.</span></span> <span data-ttu-id="b59c1-213">如果可能，将变体与头像一同使用，以强调对话框来自某人。</span><span class="sxs-lookup"><span data-stu-id="b59c1-213">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="b59c1-214">计数器</span><span class="sxs-lookup"><span data-stu-id="b59c1-214">Counter</span></span>|<span data-ttu-id="b59c1-215">说明</span><span class="sxs-lookup"><span data-stu-id="b59c1-215">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b59c1-216">1</span><span class="sxs-lookup"><span data-stu-id="b59c1-216">1</span></span>|<span data-ttu-id="b59c1-217">**头** 像：启动会议对话的人。</span><span class="sxs-lookup"><span data-stu-id="b59c1-217">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="b59c1-218">2</span><span class="sxs-lookup"><span data-stu-id="b59c1-218">2</span></span>|<span data-ttu-id="b59c1-219">**应用程序图标**</span><span class="sxs-lookup"><span data-stu-id="b59c1-219">**App icon**</span></span>|
|<span data-ttu-id="b59c1-220">3</span><span class="sxs-lookup"><span data-stu-id="b59c1-220">3</span></span>|<span data-ttu-id="b59c1-221">**应用名称**</span><span class="sxs-lookup"><span data-stu-id="b59c1-221">**App name**</span></span>|
|<span data-ttu-id="b59c1-222">4 </span><span class="sxs-lookup"><span data-stu-id="b59c1-222">4</span></span>|<span data-ttu-id="b59c1-223">**关闭按钮**：关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="b59c1-223">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="b59c1-224">5 </span><span class="sxs-lookup"><span data-stu-id="b59c1-224">5</span></span>|<span data-ttu-id="b59c1-225">**操作字符串**：通常描述启动对话框的人。</span><span class="sxs-lookup"><span data-stu-id="b59c1-225">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="b59c1-226">响应行为</span><span class="sxs-lookup"><span data-stu-id="b59c1-226">Responsive behavior</span></span>

<span data-ttu-id="b59c1-227">根据不同的方案，会议内对话框的大小可能会有所不同。</span><span class="sxs-lookup"><span data-stu-id="b59c1-227">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="b59c1-228">确保保持填充和组件大小。</span><span class="sxs-lookup"><span data-stu-id="b59c1-228">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="b59c1-229">**Width：** 可以指定对话框的 iframe 的宽度（在支持的大小范围内的任何位置）。</span><span class="sxs-lookup"><span data-stu-id="b59c1-229">**Width**: You can specify the width of the dialog's iframe anywhere within the supported size range.</span></span>
* <span data-ttu-id="b59c1-230">**高度**：可以在支持的大小范围内的任何位置指定对话框的 iframe 的高度。</span><span class="sxs-lookup"><span data-stu-id="b59c1-230">**Height**: You can specify the height of the dialog's iframe anywhere within the supported size range.</span></span> <span data-ttu-id="b59c1-231">如果应用内容超出最大高度，还可以允许用户垂直滚动。</span><span class="sxs-lookup"><span data-stu-id="b59c1-231">You also can allow users to scroll vertically if your app content exceeds the maximum height.</span></span>

<span data-ttu-id="b59c1-232">若要实现，使用 键指定宽度和 [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) 高度。</span><span class="sxs-lookup"><span data-stu-id="b59c1-232">To implement, specify the width and height using the [`externalResourceUrl`](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md#notificationsignal-api) key.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="示例显示会议内对话框。宽度：最小为 280 像素 (248 像素的 iframe) 。最大为 460 像素 (428 像素的 iframe) 。高度：300 像素 (iframe) 。" border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="b59c1-234">会议后</span><span class="sxs-lookup"><span data-stu-id="b59c1-234">After a meeting</span></span>

<span data-ttu-id="b59c1-235">可以在会议结束后返回到会议并查看应用内容。</span><span class="sxs-lookup"><span data-stu-id="b59c1-235">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="b59c1-236">本示例中，会议组织者可以在 **Contoso** 选项卡中查看投票结果。 (注意：从设计的角度来看，会议前和会议后选项卡体验之间没有区别。) </span><span class="sxs-lookup"><span data-stu-id="b59c1-236">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="示例插图显示会议后选项卡。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="b59c1-238">最佳做法</span><span class="sxs-lookup"><span data-stu-id="b59c1-238">Best practices</span></span>

<span data-ttu-id="b59c1-239">使用这些建议创建高质量的应用体验。</span><span class="sxs-lookup"><span data-stu-id="b59c1-239">Use these recommendations to create a quality app experience.</span></span>

### <a name="interactions"></a><span data-ttu-id="b59c1-240">交互</span><span class="sxs-lookup"><span data-stu-id="b59c1-240">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="显示如何限制交互数的示例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="b59c1-242">操作：限制交互数</span><span class="sxs-lookup"><span data-stu-id="b59c1-242">Do: Limit the number of interactions</span></span>

<span data-ttu-id="b59c1-243">对于会议内对话框，删除不帮助用户快速完成某些内容的不必要内容。</span><span class="sxs-lookup"><span data-stu-id="b59c1-243">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="显示如何不引入不必要的元素的示例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="b59c1-245">请勿：引入不必要的元素</span><span class="sxs-lookup"><span data-stu-id="b59c1-245">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="b59c1-246">具有多个交互的单个会议对话可能会干扰呼叫。</span><span class="sxs-lookup"><span data-stu-id="b59c1-246">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="b59c1-247">布局</span><span class="sxs-lookup"><span data-stu-id="b59c1-247">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="显示如何使用单列对话框布局的示例。" border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="b59c1-249">操作：使用单列对话框布局</span><span class="sxs-lookup"><span data-stu-id="b59c1-249">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="b59c1-250">由于对话框位于会议阶段的中心，任务完成应快速而简单，以避免用户感到沮丧。</span><span class="sxs-lookup"><span data-stu-id="b59c1-250">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="显示不应使会议扩展空间混乱的示例。" border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="b59c1-252">Don't： Clutter the space</span><span class="sxs-lookup"><span data-stu-id="b59c1-252">Don't: Clutter the space</span></span>

<span data-ttu-id="b59c1-253">密集或结构过度的内容可能会让人分心和不知所措，尤其是在会议期间。</span><span class="sxs-lookup"><span data-stu-id="b59c1-253">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="显示单列选项卡布局的示例。" border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="b59c1-255">操作：使用单列选项卡布局</span><span class="sxs-lookup"><span data-stu-id="b59c1-255">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="b59c1-256">鉴于"会议"选项卡的窄性质，我们强烈建议在单个列中显示内容。</span><span class="sxs-lookup"><span data-stu-id="b59c1-256">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="显示具有多个列的选项卡的示例。" border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="b59c1-258">请勿：使用多个列</span><span class="sxs-lookup"><span data-stu-id="b59c1-258">Don't: Use multiple columns</span></span>

<span data-ttu-id="b59c1-259">由于"会议内"选项卡的空间有限，因此不建议使用具有多个列的布局。</span><span class="sxs-lookup"><span data-stu-id="b59c1-259">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="b59c1-260">控件</span><span class="sxs-lookup"><span data-stu-id="b59c1-260">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="显示如何右对齐主要控件的示例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="b59c1-262">应做：右对齐主要操作</span><span class="sxs-lookup"><span data-stu-id="b59c1-262">Do: Right align the primary action</span></span>

<span data-ttu-id="b59c1-263">我们建议将视觉最重的操作定位到最右边的位置。</span><span class="sxs-lookup"><span data-stu-id="b59c1-263">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="显示不应左对齐主要控件的示例。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="b59c1-265">不：左对齐或居中对齐操作</span><span class="sxs-lookup"><span data-stu-id="b59c1-265">Don't: Left or center align actions</span></span>

<span data-ttu-id="b59c1-266">这偏离了用于Teams控件放置的标准模式，并且可能会与顶部对话框后面的对话框冲突。</span><span class="sxs-lookup"><span data-stu-id="b59c1-266">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="b59c1-267">Scroll</span><span class="sxs-lookup"><span data-stu-id="b59c1-267">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="在会议中的选项卡中显示垂直滚动的示例。" border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="b59c1-269">操作：垂直滚动</span><span class="sxs-lookup"><span data-stu-id="b59c1-269">Do: Scroll vertically</span></span>

<span data-ttu-id="b59c1-270">用户预期垂直滚动Teams (和任何其他位置) 。</span><span class="sxs-lookup"><span data-stu-id="b59c1-270">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="显示会议内选项卡中水平滚动的示例。" border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="b59c1-272">不：水平滚动</span><span class="sxs-lookup"><span data-stu-id="b59c1-272">Don't: Scroll horizontally</span></span>

<span data-ttu-id="b59c1-273">水平滚动并不是预期的行为Teams。</span><span class="sxs-lookup"><span data-stu-id="b59c1-273">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="b59c1-274">会议环境中的其他画布垂直滚动。</span><span class="sxs-lookup"><span data-stu-id="b59c1-274">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="b59c1-275">工作流</span><span class="sxs-lookup"><span data-stu-id="b59c1-275">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="在会议选项卡中显示复杂方案的示例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="b59c1-277">Do： Surface complex scenarios in the in-meeting tab</span><span class="sxs-lookup"><span data-stu-id="b59c1-277">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="b59c1-278">如果你的应用包含多个任务，我们强烈建议将会议中的选项卡与单列布局一同使用。</span><span class="sxs-lookup"><span data-stu-id="b59c1-278">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="在会议对话中显示复杂方案的示例。" border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="b59c1-280">请勿：使会议对话变得复杂</span><span class="sxs-lookup"><span data-stu-id="b59c1-280">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="b59c1-281">会议内对话框用于简短交互。</span><span class="sxs-lookup"><span data-stu-id="b59c1-281">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="b59c1-282">主题</span><span class="sxs-lookup"><span data-stu-id="b59c1-282">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="显示具有深色主题的会议扩展名的示例。" border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="b59c1-284">Do：使用Teams颜色令牌</span><span class="sxs-lookup"><span data-stu-id="b59c1-284">Do: Use Teams color tokens</span></span>

<span data-ttu-id="b59c1-285">Teams会议针对深色模式进行了优化，以帮助减少视觉和认知噪音，以便用户可以专注于讨论和共享内容。</span><span class="sxs-lookup"><span data-stu-id="b59c1-285">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="b59c1-286">了解如何使用<a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">Fluent UI (颜色) 。 </a></span><span class="sxs-lookup"><span data-stu-id="b59c1-286">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="显示默认使用浅色 (会议扩展) 示例。" border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="b59c1-288">请勿：硬编码十六进制值</span><span class="sxs-lookup"><span data-stu-id="b59c1-288">Don't: Hard code hex values</span></span>

<span data-ttu-id="b59c1-289">如果不使用颜色令牌Teams，你的设计将不太可扩展，并且需要更多的时间进行管理。</span><span class="sxs-lookup"><span data-stu-id="b59c1-289">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="b59c1-290">导航</span><span class="sxs-lookup"><span data-stu-id="b59c1-290">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="显示具有后退按钮的会议扩展名的示例。" border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="b59c1-292">操作：具有"后退"按钮</span><span class="sxs-lookup"><span data-stu-id="b59c1-292">Do: Have a back button</span></span>

<span data-ttu-id="b59c1-293">如果在会议选项卡中具有多个导航层，用户必须能够返回到其以前的视图。</span><span class="sxs-lookup"><span data-stu-id="b59c1-293">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="显示具有两个消除按钮的会议扩展的示例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="b59c1-295">请勿：包含其他消除按钮</span><span class="sxs-lookup"><span data-stu-id="b59c1-295">Don't: Include another dismiss button</span></span>

<span data-ttu-id="b59c1-296">提供关闭会议内选项卡内容的选项可能会导致问题，因为标题中已有一个按钮可以关闭会议中的选项卡本身。</span><span class="sxs-lookup"><span data-stu-id="b59c1-296">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="显示会议选项卡 (模式或) 模块的示例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="b59c1-298">警告：避免会议内选项卡中的模式</span><span class="sxs-lookup"><span data-stu-id="b59c1-298">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="b59c1-299">模式 (也称为任务模块) 在已经较窄的会议内选项卡中可能会封装和遮盖内容。</span><span class="sxs-lookup"><span data-stu-id="b59c1-299">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::
