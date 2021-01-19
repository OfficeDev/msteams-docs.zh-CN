---
title: 设计会议扩展
author: heath-hamilton
description: 了解如何在 Teams 会议中设计应用并获取 Microsoft Teams UI 工具包。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: c6e76356b698da4e32e279b0842ab2cc35254e99
ms.sourcegitcommit: 84f408aa2854aa7a5cefaa66ce9a373b19e0864a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/18/2021
ms.locfileid: "49886756"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="b182e-103">设计 Microsoft Teams 会议扩展</span><span class="sxs-lookup"><span data-stu-id="b182e-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="b182e-104">你可以创建应用，使会议更高效。</span><span class="sxs-lookup"><span data-stu-id="b182e-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="b182e-105">例如，要求用户在呼叫期间完成调查或发送不会中断会议流程的快速提醒。</span><span class="sxs-lookup"><span data-stu-id="b182e-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="b182e-106">Microsoft Teams UI 工具包</span><span class="sxs-lookup"><span data-stu-id="b182e-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="b182e-107">可以在 Microsoft Teams UI 工具包中查找更全面的设计准则，包括可根据需要获取和修改的元素。</span><span class="sxs-lookup"><span data-stu-id="b182e-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b182e-108">获取 Microsoft Teams UI 工具包 (图) </span><span class="sxs-lookup"><span data-stu-id="b182e-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="b182e-109">添加会议扩展</span><span class="sxs-lookup"><span data-stu-id="b182e-109">Add a meeting extension</span></span>

<span data-ttu-id="b182e-110">您可以在会议之前和会议期间添加会议扩展名。</span><span class="sxs-lookup"><span data-stu-id="b182e-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="b182e-111">还可以直接从 AppSource 应用商店或 AppSource 应用商店为特定会议 () 。</span><span class="sxs-lookup"><span data-stu-id="b182e-111">You also can add an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="b182e-112">在会议前添加</span><span class="sxs-lookup"><span data-stu-id="b182e-112">Add before a meeting</span></span>

<span data-ttu-id="b182e-113">在会议详细信息中，选择 **"添加选项卡 +"** 以打开应用飞出并查找已针对会议优化的应用。</span><span class="sxs-lookup"><span data-stu-id="b182e-113">In the meeting details, select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="示例演示如何在会议之前添加会议扩展名。" border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="b182e-115">在会议期间添加</span><span class="sxs-lookup"><span data-stu-id="b182e-115">Add during a meeting</span></span>

在会议中选择 **"更多** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **添加应用"，** 然后选择你需要的应用。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="示例演示如何在会议期间添加会议扩展名。" border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="b182e-118">会议之前</span><span class="sxs-lookup"><span data-stu-id="b182e-118">Before a meeting</span></span>

<span data-ttu-id="b182e-119">在会议之前，可以在选项卡中添加内容。以下示例显示了呼叫过程中人员将回答的草稿调查问题。</span><span class="sxs-lookup"><span data-stu-id="b182e-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="示例演示如何在呼叫之前在会议详细信息中应用内容。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="b182e-121">分析：会议 (会议之前和之后) </span><span class="sxs-lookup"><span data-stu-id="b182e-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="示例显示会议之前和之后会议选项卡的结构分析。" border="false":::

|<span data-ttu-id="b182e-123">计数器</span><span class="sxs-lookup"><span data-stu-id="b182e-123">Counter</span></span>|<span data-ttu-id="b182e-124">说明</span><span class="sxs-lookup"><span data-stu-id="b182e-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b182e-125">1</span><span class="sxs-lookup"><span data-stu-id="b182e-125">1</span></span>|<span data-ttu-id="b182e-126">**选项卡名称**：选项卡的导航标签。</span><span class="sxs-lookup"><span data-stu-id="b182e-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="b182e-127">2 </span><span class="sxs-lookup"><span data-stu-id="b182e-127">2</span></span>|<span data-ttu-id="b182e-128">**Tab 溢出**：打开选项卡操作，如重命名和删除。</span><span class="sxs-lookup"><span data-stu-id="b182e-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="b182e-129">3</span><span class="sxs-lookup"><span data-stu-id="b182e-129">3</span></span>|<span data-ttu-id="b182e-130">**iframe：** 显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="b182e-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="b182e-131">使用 UI 模板进行设计</span><span class="sxs-lookup"><span data-stu-id="b182e-131">Designing with UI templates</span></span>

<span data-ttu-id="b182e-132">使用以下 Teams UI 模板之一来帮助设计会议选项卡：</span><span class="sxs-lookup"><span data-stu-id="b182e-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="b182e-133">[列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可扫描的格式显示相关项目，并允许用户对整个列表或单个项目采取操作。</span><span class="sxs-lookup"><span data-stu-id="b182e-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="b182e-134">[任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为看板或街道）是一组卡片，通常用于跟踪工作项或票证的状态。</span><span class="sxs-lookup"><span data-stu-id="b182e-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="b182e-135">[仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是包含多个卡片的画布，可提供数据或内容的概述。</span><span class="sxs-lookup"><span data-stu-id="b182e-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="b182e-136">[表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单用于以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="b182e-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="b182e-137">[空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于许多方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="b182e-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="b182e-138">[左侧导航](../../concepts/design/design-teams-app-ui-templates.md#left-nav)：如果你的选项卡需要一些导航，左侧导航模板可以提供帮助。</span><span class="sxs-lookup"><span data-stu-id="b182e-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="b182e-139">通常，应使 Tab 键导航保持在最低程度。</span><span class="sxs-lookup"><span data-stu-id="b182e-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="b182e-140">使用"会议内"选项卡</span><span class="sxs-lookup"><span data-stu-id="b182e-140">Use an in-meeting tab</span></span>

<span data-ttu-id="b182e-141">"会议内"选项卡是一块画布，用于增强会议期间的协作。</span><span class="sxs-lookup"><span data-stu-id="b182e-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="b182e-142">与会者可以通过共享视图或基于角色的视图在会议阶段外的专用空间中查看应用内容并与之交互。</span><span class="sxs-lookup"><span data-stu-id="b182e-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="b182e-143">用例</span><span class="sxs-lookup"><span data-stu-id="b182e-143">Use cases</span></span>

<span data-ttu-id="b182e-144">用户可能会使用"会议内"选项卡：</span><span class="sxs-lookup"><span data-stu-id="b182e-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="b182e-145">提供详细的 (例如，评估候选人) </span><span class="sxs-lookup"><span data-stu-id="b182e-145">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="b182e-146">为会议参与者快速创建投票、调查或任务项</span><span class="sxs-lookup"><span data-stu-id="b182e-146">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="b182e-147">显示与会议记录相关的 (，例如，有关销售线索) </span><span class="sxs-lookup"><span data-stu-id="b182e-147">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="示例演示如何在会议中的选项卡中显示轮询内容。" border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="b182e-149">"分析：会议内"选项卡</span><span class="sxs-lookup"><span data-stu-id="b182e-149">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="示例显示会议内选项卡的结构分析。" border="false":::

|<span data-ttu-id="b182e-151">计数器</span><span class="sxs-lookup"><span data-stu-id="b182e-151">Counter</span></span>|<span data-ttu-id="b182e-152">说明</span><span class="sxs-lookup"><span data-stu-id="b182e-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b182e-153">1</span><span class="sxs-lookup"><span data-stu-id="b182e-153">1</span></span>|<span data-ttu-id="b182e-154">**所选 (图标**) ：16 像素透明应用徽标。</span><span class="sxs-lookup"><span data-stu-id="b182e-154">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="b182e-155">2 </span><span class="sxs-lookup"><span data-stu-id="b182e-155">2</span></span>|<span data-ttu-id="b182e-156">**应用名称**</span><span class="sxs-lookup"><span data-stu-id="b182e-156">**App name**</span></span>|
|<span data-ttu-id="b182e-157">3</span><span class="sxs-lookup"><span data-stu-id="b182e-157">3</span></span>|<span data-ttu-id="b182e-158">**标头**：包括你的应用名称。</span><span class="sxs-lookup"><span data-stu-id="b182e-158">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="b182e-159">4 </span><span class="sxs-lookup"><span data-stu-id="b182e-159">4</span></span>|<span data-ttu-id="b182e-160">**关闭按钮**：关闭选项卡。始终使用右上方的关闭图标，而不是页脚中的操作。</span><span class="sxs-lookup"><span data-stu-id="b182e-160">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="b182e-161">5 </span><span class="sxs-lookup"><span data-stu-id="b182e-161">5</span></span>|<span data-ttu-id="b182e-162">**通知栏**：错误警报显示在标题正下方，将 iframe 内容向下推送 20 像素。</span><span class="sxs-lookup"><span data-stu-id="b182e-162">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="b182e-163">6 </span><span class="sxs-lookup"><span data-stu-id="b182e-163">6</span></span>|<span data-ttu-id="b182e-164">**iframe：** 显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="b182e-164">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="b182e-165">Spacing</span><span class="sxs-lookup"><span data-stu-id="b182e-165">Spacing</span></span>

<span data-ttu-id="b182e-166">优化会议内选项卡以适合 280 像素范围 iframe 区域中的边缘到边缘。</span><span class="sxs-lookup"><span data-stu-id="b182e-166">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="b182e-167">iframe 的左右两侧以及选项卡标题之间有 20 像素的填充。</span><span class="sxs-lookup"><span data-stu-id="b182e-167">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="b182e-168">iframe 完全出血到选项卡底部。</span><span class="sxs-lookup"><span data-stu-id="b182e-168">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="示例显示会议中的选项卡间距尺寸。" border="false":::

### <a name="scrolling"></a><span data-ttu-id="b182e-170">滚动</span><span class="sxs-lookup"><span data-stu-id="b182e-170">Scrolling</span></span>

<span data-ttu-id="b182e-171">Iframe 内容应垂直滚动。</span><span class="sxs-lookup"><span data-stu-id="b182e-171">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="b182e-172">只能看到滚动到的内容， (上或下方) 。</span><span class="sxs-lookup"><span data-stu-id="b182e-172">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="b182e-173">滚动条是 iframe 内容的一部分。</span><span class="sxs-lookup"><span data-stu-id="b182e-173">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="示例显示如何滚动会议中的选项卡。" border="false":::

### <a name="navigation"></a><span data-ttu-id="b182e-175">导航</span><span class="sxs-lookup"><span data-stu-id="b182e-175">Navigation</span></span>

<span data-ttu-id="b182e-176">对于具有导航层或大量内容的方案，我们建议允许用户导航到辅助层。</span><span class="sxs-lookup"><span data-stu-id="b182e-176">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="b182e-177">用户必须能够返回到上一层。</span><span class="sxs-lookup"><span data-stu-id="b182e-177">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="示例显示会议内导航。" border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="b182e-179">使用会议内对话框</span><span class="sxs-lookup"><span data-stu-id="b182e-179">Use an in-meeting dialog</span></span>

<span data-ttu-id="b182e-180">会议中的对话框显示在 Teams 会议阶段。</span><span class="sxs-lookup"><span data-stu-id="b182e-180">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="b182e-181">它们需要用户的注意、确认或交互，但非常细微，不会中断会议。</span><span class="sxs-lookup"><span data-stu-id="b182e-181">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="b182e-182">应谨慎使用这些资源，并针对轻型和面向任务的方案。</span><span class="sxs-lookup"><span data-stu-id="b182e-182">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="b182e-183">用例</span><span class="sxs-lookup"><span data-stu-id="b182e-183">Use cases</span></span>

<span data-ttu-id="b182e-184">会议内对话框由可能希望参与者 (会议组织者) 等用户触发：</span><span class="sxs-lookup"><span data-stu-id="b182e-184">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="b182e-185">提供简短反馈</span><span class="sxs-lookup"><span data-stu-id="b182e-185">Provide brief feedback</span></span>
* <span data-ttu-id="b182e-186">参加简短调查或投票</span><span class="sxs-lookup"><span data-stu-id="b182e-186">Take a short survey or poll</span></span>
* <span data-ttu-id="b182e-187">提交审批</span><span class="sxs-lookup"><span data-stu-id="b182e-187">Submit approvals</span></span>
* <span data-ttu-id="b182e-188">获取提醒</span><span class="sxs-lookup"><span data-stu-id="b182e-188">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="示例演示如何使用会议内对话框。" border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="b182e-190">分析：会议内对话框</span><span class="sxs-lookup"><span data-stu-id="b182e-190">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="示例显示会议内对话框的结构分析。" border="false":::

|<span data-ttu-id="b182e-192">计数器</span><span class="sxs-lookup"><span data-stu-id="b182e-192">Counter</span></span>|<span data-ttu-id="b182e-193">说明</span><span class="sxs-lookup"><span data-stu-id="b182e-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b182e-194">1</span><span class="sxs-lookup"><span data-stu-id="b182e-194">1</span></span>|<span data-ttu-id="b182e-195">**标头**：包括应用图标、名称、操作字符串和关闭图标。</span><span class="sxs-lookup"><span data-stu-id="b182e-195">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="b182e-196">2 </span><span class="sxs-lookup"><span data-stu-id="b182e-196">2</span></span>|<span data-ttu-id="b182e-197">**iframe：** 显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="b182e-197">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="b182e-198">分析：会议内对话框标题</span><span class="sxs-lookup"><span data-stu-id="b182e-198">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="示例显示会议内对话框标题的结构分析。" border="false":::

<span data-ttu-id="b182e-200">有两个标头变量。</span><span class="sxs-lookup"><span data-stu-id="b182e-200">There are two header variants.</span></span> <span data-ttu-id="b182e-201">如果可能，将变量与头像一同使用，以强调对话框来自个人。</span><span class="sxs-lookup"><span data-stu-id="b182e-201">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="b182e-202">计数器</span><span class="sxs-lookup"><span data-stu-id="b182e-202">Counter</span></span>|<span data-ttu-id="b182e-203">说明</span><span class="sxs-lookup"><span data-stu-id="b182e-203">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="b182e-204">1</span><span class="sxs-lookup"><span data-stu-id="b182e-204">1</span></span>|<span data-ttu-id="b182e-205">**头** 像：启动会议内对话框的人。</span><span class="sxs-lookup"><span data-stu-id="b182e-205">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="b182e-206">2 </span><span class="sxs-lookup"><span data-stu-id="b182e-206">2</span></span>|<span data-ttu-id="b182e-207">**应用程序图标**</span><span class="sxs-lookup"><span data-stu-id="b182e-207">**App icon**</span></span>|
|<span data-ttu-id="b182e-208">3</span><span class="sxs-lookup"><span data-stu-id="b182e-208">3</span></span>|<span data-ttu-id="b182e-209">**应用名称**</span><span class="sxs-lookup"><span data-stu-id="b182e-209">**App name**</span></span>|
|<span data-ttu-id="b182e-210">4 </span><span class="sxs-lookup"><span data-stu-id="b182e-210">4</span></span>|<span data-ttu-id="b182e-211">**关闭按钮**：关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="b182e-211">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="b182e-212">5 </span><span class="sxs-lookup"><span data-stu-id="b182e-212">5</span></span>|<span data-ttu-id="b182e-213">**操作字符串**：通常描述启动对话框的人。</span><span class="sxs-lookup"><span data-stu-id="b182e-213">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="b182e-214">响应行为</span><span class="sxs-lookup"><span data-stu-id="b182e-214">Responsive behavior</span></span>

<span data-ttu-id="b182e-215">会议内对话框的大小可能会有所不同，以考虑不同的方案。</span><span class="sxs-lookup"><span data-stu-id="b182e-215">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="b182e-216">确保保持填充和组件大小。</span><span class="sxs-lookup"><span data-stu-id="b182e-216">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="b182e-217">**宽度**：iframe 宽度是指定范围内的绝对值。</span><span class="sxs-lookup"><span data-stu-id="b182e-217">**Width**: The iframe width is an absolute value within the range you specify.</span></span>
* <span data-ttu-id="b182e-218">**高度**：对话框的高度由 iframe 中的内容决定。</span><span class="sxs-lookup"><span data-stu-id="b182e-218">**Height**: The height of the dialog is determined by the content in the iframe.</span></span> <span data-ttu-id="b182e-219">垂直滚动将接管超过最大高度的内容。</span><span class="sxs-lookup"><span data-stu-id="b182e-219">Vertical scroll takes over for content that exceeds the maximum height.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="示例显示会议内对话框。宽度：最小-280 像素 (248 像素的 iframe) 。最大像素为 460 (428 像素的 iframe) 。高度：iframe (300) 。" border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="b182e-221">会议后</span><span class="sxs-lookup"><span data-stu-id="b182e-221">After a meeting</span></span>

<span data-ttu-id="b182e-222">会议结束后，你可以返回到会议并查看应用内容。</span><span class="sxs-lookup"><span data-stu-id="b182e-222">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="b182e-223">本示例中，会议组织者可以在 **Contoso** 选项卡中查看投票结果。 (注意：从设计的角度来看，会议前和会议后选项卡体验之间没有任何区别。) </span><span class="sxs-lookup"><span data-stu-id="b182e-223">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="示例显示会议后选项卡。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="b182e-225">最佳做法</span><span class="sxs-lookup"><span data-stu-id="b182e-225">Best practices</span></span>

### <a name="interactions"></a><span data-ttu-id="b182e-226">交互</span><span class="sxs-lookup"><span data-stu-id="b182e-226">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="显示如何限制交互数的示例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="b182e-228">Do： Limit the number of interactions</span><span class="sxs-lookup"><span data-stu-id="b182e-228">Do: Limit the number of interactions</span></span>

<span data-ttu-id="b182e-229">对于会议内对话框，删除不帮助用户快速完成某些内容的不必要内容。</span><span class="sxs-lookup"><span data-stu-id="b182e-229">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="显示如何不引入不必要的元素的示例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="b182e-231">请勿：引入不必要的元素</span><span class="sxs-lookup"><span data-stu-id="b182e-231">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="b182e-232">具有多个交互的单个会议内对话框可能会分散呼叫的干扰。</span><span class="sxs-lookup"><span data-stu-id="b182e-232">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="b182e-233">布局</span><span class="sxs-lookup"><span data-stu-id="b182e-233">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="显示如何使用单列对话框布局的示例。" border="false":::

#### <a name="do-use-a-single-column-dialog-layout"></a><span data-ttu-id="b182e-235">操作：使用单列对话框布局</span><span class="sxs-lookup"><span data-stu-id="b182e-235">Do: Use a single-column dialog layout</span></span>

<span data-ttu-id="b182e-236">由于对话框位于会议阶段的中心，因此任务完成应快速且简单，以避免用户感到沮丧。</span><span class="sxs-lookup"><span data-stu-id="b182e-236">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="显示不应使会议扩展空间混乱的示例。" border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="b182e-238">请勿：使空格变得杂乱</span><span class="sxs-lookup"><span data-stu-id="b182e-238">Don't: Clutter the space</span></span>

<span data-ttu-id="b182e-239">内容密集或结构过度可能会让人分心和不知所措，尤其是在会议期间。</span><span class="sxs-lookup"><span data-stu-id="b182e-239">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="显示单列选项卡布局的示例。" border="false":::

#### <a name="do-use-a-single-column-tab-layout"></a><span data-ttu-id="b182e-241">操作：使用单列选项卡布局</span><span class="sxs-lookup"><span data-stu-id="b182e-241">Do: Use a single-column tab layout</span></span>

<span data-ttu-id="b182e-242">鉴于会议内选项卡的窄性质，我们强烈建议在单个列中显示内容。</span><span class="sxs-lookup"><span data-stu-id="b182e-242">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="显示具有多个列的选项卡的示例。" border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="b182e-244">请勿：使用多个列</span><span class="sxs-lookup"><span data-stu-id="b182e-244">Don't: Use multiple columns</span></span>

<span data-ttu-id="b182e-245">由于会议中选项卡的空间有限，因此不建议使用具有多个列的布局。</span><span class="sxs-lookup"><span data-stu-id="b182e-245">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="b182e-246">控件</span><span class="sxs-lookup"><span data-stu-id="b182e-246">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="显示如何右对齐主要控件的示例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="b182e-248">操作：右对齐主要操作</span><span class="sxs-lookup"><span data-stu-id="b182e-248">Do: Right align the primary action</span></span>

<span data-ttu-id="b182e-249">我们建议将视觉最重的操作定位到最右边的位置。</span><span class="sxs-lookup"><span data-stu-id="b182e-249">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="显示不应使主控件左对齐的示例。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="b182e-251">请勿：左对齐或居中对齐操作</span><span class="sxs-lookup"><span data-stu-id="b182e-251">Don't: Left or center align actions</span></span>

<span data-ttu-id="b182e-252">这偏离了用于控件在对话框中放置的标准 Teams 模式，并且可能会与顶部对话框后面的对话框冲突。</span><span class="sxs-lookup"><span data-stu-id="b182e-252">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="b182e-253">Scroll</span><span class="sxs-lookup"><span data-stu-id="b182e-253">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="显示会议内选项卡中的垂直滚动的示例。" border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="b182e-255">操作：垂直滚动</span><span class="sxs-lookup"><span data-stu-id="b182e-255">Do: Scroll vertically</span></span>

<span data-ttu-id="b182e-256">用户期望在 Teams 中和 (其他位置进行垂直) 。</span><span class="sxs-lookup"><span data-stu-id="b182e-256">Users expect vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="显示会议内选项卡中水平滚动的示例。" border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="b182e-258">不要：水平滚动</span><span class="sxs-lookup"><span data-stu-id="b182e-258">Don't: Scroll horizontally</span></span>

<span data-ttu-id="b182e-259">水平滚动在 Teams 中不是预期行为。</span><span class="sxs-lookup"><span data-stu-id="b182e-259">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="b182e-260">会议环境中的其他画布垂直滚动。</span><span class="sxs-lookup"><span data-stu-id="b182e-260">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="b182e-261">工作流</span><span class="sxs-lookup"><span data-stu-id="b182e-261">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="在&quot;会议内&quot;选项卡中显示复杂方案的示例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="b182e-263">Do： Surface complex scenarios in the in-meeting tab</span><span class="sxs-lookup"><span data-stu-id="b182e-263">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="b182e-264">如果你的应用包含多个任务，我们强烈建议将会议内选项卡与单列布局一同使用。</span><span class="sxs-lookup"><span data-stu-id="b182e-264">If your app includes multiple tasks, we strongly recommend using an in-meeting tab with a single-column layout.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="在会议内对话框中显示复杂方案的示例。" border="false":::

#### <a name="dont-make-in-meeting-dialogs-complex"></a><span data-ttu-id="b182e-266">请勿：使会议内对话框变得复杂</span><span class="sxs-lookup"><span data-stu-id="b182e-266">Don't: Make in-meeting dialogs complex</span></span>

<span data-ttu-id="b182e-267">会议内对话框用于简短交互。</span><span class="sxs-lookup"><span data-stu-id="b182e-267">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="b182e-268">主题</span><span class="sxs-lookup"><span data-stu-id="b182e-268">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="显示具有深色主题的会议扩展的示例。" border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="b182e-270">使用 Teams 颜色令牌</span><span class="sxs-lookup"><span data-stu-id="b182e-270">Do: Use Teams color tokens</span></span>

<span data-ttu-id="b182e-271">Teams 会议针对深色模式进行了优化，以帮助减少视觉和认知干扰，以便用户可以专注于讨论和共享内容。</span><span class="sxs-lookup"><span data-stu-id="b182e-271">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="b182e-272">了解如何使用<a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">Fluent UI (颜色) 。 </a></span><span class="sxs-lookup"><span data-stu-id="b182e-272">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="显示默认为浅色 (会议) 的示例。" border="false":::

#### <a name="dont-hard-code-hex-values"></a><span data-ttu-id="b182e-274">请勿：硬编码十六进制值</span><span class="sxs-lookup"><span data-stu-id="b182e-274">Don't: Hard code hex values</span></span>

<span data-ttu-id="b182e-275">如果不使用 Teams 颜色令牌，你的设计将不太可扩展，并且需要更多时间来管理。</span><span class="sxs-lookup"><span data-stu-id="b182e-275">If you don’t use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="b182e-276">导航</span><span class="sxs-lookup"><span data-stu-id="b182e-276">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="显示具有后退按钮的会议扩展的示例。" border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="b182e-278">Do： Have a back button</span><span class="sxs-lookup"><span data-stu-id="b182e-278">Do: Have a back button</span></span>

<span data-ttu-id="b182e-279">如果在会议内选项卡中具有多个导航层，用户必须能够返回其以前的视图。</span><span class="sxs-lookup"><span data-stu-id="b182e-279">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="显示具有两个消除按钮的会议扩展的示例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="b182e-281">请勿：包括另一个消除按钮</span><span class="sxs-lookup"><span data-stu-id="b182e-281">Don't: Include another dismiss button</span></span>

<span data-ttu-id="b182e-282">提供关闭会议内选项卡内容的选项可能会导致问题，因为标题中已有一个按钮可消除会议内选项卡本身。</span><span class="sxs-lookup"><span data-stu-id="b182e-282">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="显示模式模块 (或任务) 在会议选项卡中显示的示例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="b182e-284">警告：避免会议内选项卡中的模式</span><span class="sxs-lookup"><span data-stu-id="b182e-284">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="b182e-285">模式 (在) 较窄的"会议"选项卡中运行的任务模块可能会封装和遮盖内容。</span><span class="sxs-lookup"><span data-stu-id="b182e-285">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="b182e-286">验证设计</span><span class="sxs-lookup"><span data-stu-id="b182e-286">Validate your design</span></span>

<span data-ttu-id="b182e-287">如果你计划将应用发布到 AppSource，你应了解在提交期间通常导致应用失败的设计问题。</span><span class="sxs-lookup"><span data-stu-id="b182e-287">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b182e-288">检查设计验证指南</span><span class="sxs-lookup"><span data-stu-id="b182e-288">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
