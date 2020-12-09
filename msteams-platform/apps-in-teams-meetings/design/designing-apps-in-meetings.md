---
title: 正在设计会议分机
author: heath-hamilton
description: 了解如何在团队会议中设计应用并获取 Microsoft 团队 UI 工具包。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 3d18895626d5f2846d10e7145a622834d82b2e98
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605941"
---
# <a name="designing-your-microsoft-teams-meeting-extension"></a><span data-ttu-id="1577d-103">正在设计 Microsoft 团队会议扩展</span><span class="sxs-lookup"><span data-stu-id="1577d-103">Designing your Microsoft Teams meeting extension</span></span>

<span data-ttu-id="1577d-104">您可以创建应用程序以提高会议的生产率。</span><span class="sxs-lookup"><span data-stu-id="1577d-104">You can create apps to make meetings more productive.</span></span> <span data-ttu-id="1577d-105">例如，要求人员在呼叫过程中完成调查或发送不会中断会议流的快速提醒。</span><span class="sxs-lookup"><span data-stu-id="1577d-105">For example, ask people to complete a survey during a call or send a quick reminder that doesn’t interrupt the flow of the meeting.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="1577d-106">Microsoft 团队 UI 工具包</span><span class="sxs-lookup"><span data-stu-id="1577d-106">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="1577d-107">您可以在 Microsoft 团队 UI 工具包中找到更全面的设计准则，包括可在需要时获取和修改的元素。</span><span class="sxs-lookup"><span data-stu-id="1577d-107">You can find more comprehensive design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1577d-108"> (Figma) 获取 Microsoft 团队 UI 工具包 </span><span class="sxs-lookup"><span data-stu-id="1577d-108">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-meeting-extension"></a><span data-ttu-id="1577d-109">添加会议分机</span><span class="sxs-lookup"><span data-stu-id="1577d-109">Add a meeting extension</span></span>

<span data-ttu-id="1577d-110">您可以在会议前后添加会议分机号。</span><span class="sxs-lookup"><span data-stu-id="1577d-110">You can add a meeting extension before and during meetings.</span></span> <span data-ttu-id="1577d-111">您还可以直接从团队存储 (AppSource) 中的特定会议的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1577d-111">You also can an app for a specific meeting directly from the Teams store (AppSource).</span></span>

### <a name="add-before-a-meeting"></a><span data-ttu-id="1577d-112">在会议之前添加</span><span class="sxs-lookup"><span data-stu-id="1577d-112">Add before a meeting</span></span>

<span data-ttu-id="1577d-113">在会议之前，会议详细信息选择 " **添加选项卡 +** " 以打开 "应用程序" 飞出并查找针对会议优化的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1577d-113">Before a meeting, the meeting details select **Add a tab +** to open the app flyout and find apps optimized for meetings.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/add-before-meeting.png" alt-text="示例演示如何在会议之前添加会议分机号。" border="false":::

### <a name="add-during-a-meeting"></a><span data-ttu-id="1577d-115">在会议过程中添加</span><span class="sxs-lookup"><span data-stu-id="1577d-115">Add during a meeting</span></span>

在会议中，选择 "**更多** :::image type="icon" source="../../assets/icons/teams-client-more.png":::  >  **添加应用程序**"，然后选择所需的应用程序。

:::image type="content" source="../../assets/images/apps-in-meetings/add-during-meeting.png" alt-text="示例演示如何在会议过程中添加会议分机号。" border="false":::

## <a name="before-a-meeting"></a><span data-ttu-id="1577d-118">会议前</span><span class="sxs-lookup"><span data-stu-id="1577d-118">Before a meeting</span></span>

<span data-ttu-id="1577d-119">在会议之前，您可以在选项卡中添加内容。下面的示例展示了用户在呼叫过程中将应答的草案调查问题。</span><span class="sxs-lookup"><span data-stu-id="1577d-119">Prior to your meeting, you can add content in the tab. The following example shows a draft survey question that people will answer during the call.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/before-meeting-tab.png" alt-text="示例演示如何在呼叫之前在会议详细信息中应用内容。" border="false":::

### <a name="anatomy-meeting-tab-before-and-after-meetings"></a><span data-ttu-id="1577d-121">剖析：会议选项卡 (之前和之后的会议) </span><span class="sxs-lookup"><span data-stu-id="1577d-121">Anatomy: Meeting tab (before and after meetings)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/meeting-details-tab-anatomy.png" alt-text="示例显示会议前后会议选项卡的结构解析。" border="false":::

|<span data-ttu-id="1577d-123">计数器</span><span class="sxs-lookup"><span data-stu-id="1577d-123">Counter</span></span>|<span data-ttu-id="1577d-124">说明</span><span class="sxs-lookup"><span data-stu-id="1577d-124">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1577d-125">1</span><span class="sxs-lookup"><span data-stu-id="1577d-125">1</span></span>|<span data-ttu-id="1577d-126">**选项卡名称**：选项卡的导航标签。</span><span class="sxs-lookup"><span data-stu-id="1577d-126">**Tab name**: Navigation label for your tab.</span></span>|
|<span data-ttu-id="1577d-127">2 </span><span class="sxs-lookup"><span data-stu-id="1577d-127">2</span></span>|<span data-ttu-id="1577d-128">**选项卡溢出**：打开选项卡操作，例如 "重命名" 和 "删除"。</span><span class="sxs-lookup"><span data-stu-id="1577d-128">**Tab overflow**: Opens tab actions, such as rename and remove.</span></span>|
|<span data-ttu-id="1577d-129">3 </span><span class="sxs-lookup"><span data-stu-id="1577d-129">3</span></span>|<span data-ttu-id="1577d-130">**iframe**：显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="1577d-130">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="1577d-131">使用 UI 模板进行设计</span><span class="sxs-lookup"><span data-stu-id="1577d-131">Designing with UI templates</span></span>

<span data-ttu-id="1577d-132">使用以下团队 UI 模板之一来帮助设计 "会议" 选项卡：</span><span class="sxs-lookup"><span data-stu-id="1577d-132">Use one of the following Teams UI templates to help design your meeting tab:</span></span>

* <span data-ttu-id="1577d-133">[列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可浏览的格式显示相关项目，并允许用户对整个列表或单个项目执行操作。</span><span class="sxs-lookup"><span data-stu-id="1577d-133">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="1577d-134">[任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为 "看板母板" 或 "泳道"）是用于跟踪工作项或票证状态的卡片的集合。</span><span class="sxs-lookup"><span data-stu-id="1577d-134">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="1577d-135">[仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是一个包含多个卡片的画布，可提供数据或内容的概述。</span><span class="sxs-lookup"><span data-stu-id="1577d-135">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="1577d-136">[表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="1577d-136">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="1577d-137">[空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="1577d-137">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="1577d-138">[左侧](../../concepts/design/design-teams-app-ui-templates.md#left-nav)导航：如果您的选项卡需要一些导航，则左侧导航模板可有所帮助。</span><span class="sxs-lookup"><span data-stu-id="1577d-138">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="1577d-139">通常情况下，应保持最小的选项卡导航。</span><span class="sxs-lookup"><span data-stu-id="1577d-139">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-an-in-meeting-tab"></a><span data-ttu-id="1577d-140">使用会议中的选项卡</span><span class="sxs-lookup"><span data-stu-id="1577d-140">Use an in-meeting tab</span></span>

<span data-ttu-id="1577d-141">"会议" 选项卡是在会议过程中充实协作的画布。</span><span class="sxs-lookup"><span data-stu-id="1577d-141">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="1577d-142">与会者可以通过共享或基于角色的视图在会议阶段外的专用空间中查看应用程序内容并与之交互。</span><span class="sxs-lookup"><span data-stu-id="1577d-142">Attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

### <a name="use-cases"></a><span data-ttu-id="1577d-143">用例</span><span class="sxs-lookup"><span data-stu-id="1577d-143">Use cases</span></span>

<span data-ttu-id="1577d-144">用户可能会使用 "会议" 选项卡执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="1577d-144">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="1577d-145">提供详细反馈 (例如，评估求职候选人) </span><span class="sxs-lookup"><span data-stu-id="1577d-145">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="1577d-146">为会议参与者快速创建轮询、调查或任务项</span><span class="sxs-lookup"><span data-stu-id="1577d-146">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="1577d-147">显示与会议相关的注释 (例如，有关销售线索的信息) </span><span class="sxs-lookup"><span data-stu-id="1577d-147">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-tab.png" alt-text="示例演示如何在 &quot;会议&quot; 选项卡中显示轮询内容。" border="false":::

### <a name="anatomy-in-meeting-tab"></a><span data-ttu-id="1577d-149">剖析：会议中的选项卡</span><span class="sxs-lookup"><span data-stu-id="1577d-149">Anatomy: In-meeting tab</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-anatomy.png" alt-text="示例显示了 &quot;会议&quot; 选项卡的结构解析。" border="false":::

|<span data-ttu-id="1577d-151">计数器</span><span class="sxs-lookup"><span data-stu-id="1577d-151">Counter</span></span>|<span data-ttu-id="1577d-152">说明</span><span class="sxs-lookup"><span data-stu-id="1577d-152">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1577d-153">1</span><span class="sxs-lookup"><span data-stu-id="1577d-153">1</span></span>|<span data-ttu-id="1577d-154">**选定)  (的应用程序图标**：16像素透明应用程序徽标。</span><span class="sxs-lookup"><span data-stu-id="1577d-154">**App icon (selected)**: 16-pixel transparent app logo.</span></span>|
|<span data-ttu-id="1577d-155">2 </span><span class="sxs-lookup"><span data-stu-id="1577d-155">2</span></span>|<span data-ttu-id="1577d-156">**应用名称**</span><span class="sxs-lookup"><span data-stu-id="1577d-156">**App name**</span></span>|
|<span data-ttu-id="1577d-157">3 </span><span class="sxs-lookup"><span data-stu-id="1577d-157">3</span></span>|<span data-ttu-id="1577d-158">**标头**：包括您的应用程序名称。</span><span class="sxs-lookup"><span data-stu-id="1577d-158">**Header**: Includes your app name.</span></span>|
|<span data-ttu-id="1577d-159">4 </span><span class="sxs-lookup"><span data-stu-id="1577d-159">4</span></span>|<span data-ttu-id="1577d-160">"**关闭" 按钮**：关闭选项卡。始终使用右上关闭图标而不是页脚中的操作。</span><span class="sxs-lookup"><span data-stu-id="1577d-160">**Close button**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>|
|<span data-ttu-id="1577d-161">5 </span><span class="sxs-lookup"><span data-stu-id="1577d-161">5</span></span>|<span data-ttu-id="1577d-162">**通知栏**：错误警报显示在标头正下方，并将 iframe 内容向下推送20个像素。</span><span class="sxs-lookup"><span data-stu-id="1577d-162">**Notification bar**: Error alerts display directly below the header and push the iframe content down by 20 pixels.</span></span>|
|<span data-ttu-id="1577d-163">6 </span><span class="sxs-lookup"><span data-stu-id="1577d-163">6</span></span>|<span data-ttu-id="1577d-164">**iframe**：显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="1577d-164">**iframe**: Displays your app content.</span></span>|

### <a name="spacing"></a><span data-ttu-id="1577d-165">Spacing</span><span class="sxs-lookup"><span data-stu-id="1577d-165">Spacing</span></span>

<span data-ttu-id="1577d-166">优化 "会议" 选项卡，使其适合在280像素宽 iframe 区域中的边缘到边缘。</span><span class="sxs-lookup"><span data-stu-id="1577d-166">Optimize your in-meeting tab to fit edge-to-edge within the 280 pixel-wide iframe area.</span></span> <span data-ttu-id="1577d-167">Iframe 左侧和右侧的填充量为20像素，在选项卡标题之间。</span><span class="sxs-lookup"><span data-stu-id="1577d-167">There are 20 pixels of padding on the left and right sides of the iframe and between the tab header.</span></span> <span data-ttu-id="1577d-168">Iframe 是选项卡底部的完全出血。</span><span class="sxs-lookup"><span data-stu-id="1577d-168">The iframe is full bleed to the bottom of the tab.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-spacing.png" alt-text="示例显示了会议制表符间距尺寸。" border="false":::

### <a name="scrolling"></a><span data-ttu-id="1577d-170">上下</span><span class="sxs-lookup"><span data-stu-id="1577d-170">Scrolling</span></span>

<span data-ttu-id="1577d-171">Iframe 内容应垂直滚动。</span><span class="sxs-lookup"><span data-stu-id="1577d-171">Iframe contents should scroll vertically.</span></span> <span data-ttu-id="1577d-172">您只能看到您已滚动的内容 (不在) 以上或之下的任何内容。</span><span class="sxs-lookup"><span data-stu-id="1577d-172">You can only see the content you've scrolled to (nothing above or below).</span></span> <span data-ttu-id="1577d-173">滚动条是 iframe 内容的一部分。</span><span class="sxs-lookup"><span data-stu-id="1577d-173">The scrollbar is part of the iframe content.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-scrolling.png" alt-text="示例显示 &quot;会议&quot; 选项卡如何滚动。" border="false":::

### <a name="navigation"></a><span data-ttu-id="1577d-175">导航</span><span class="sxs-lookup"><span data-stu-id="1577d-175">Navigation</span></span>

<span data-ttu-id="1577d-176">对于具有导航层或较大内容的方案，建议允许用户导航到辅助层。</span><span class="sxs-lookup"><span data-stu-id="1577d-176">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="1577d-177">用户必须能够返回到上一层。</span><span class="sxs-lookup"><span data-stu-id="1577d-177">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav.png" alt-text="示例显示了会议内导航。" border="false":::

## <a name="use-an-in-meeting-dialog"></a><span data-ttu-id="1577d-179">使用会议中的对话框</span><span class="sxs-lookup"><span data-stu-id="1577d-179">Use an in-meeting dialog</span></span>

<span data-ttu-id="1577d-180">会议中的对话框显示在团队会议阶段。</span><span class="sxs-lookup"><span data-stu-id="1577d-180">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="1577d-181">他们需要用户注意、确认或交互，但这并不会中断会议。</span><span class="sxs-lookup"><span data-stu-id="1577d-181">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span> <span data-ttu-id="1577d-182">您应谨慎使用这些方案，并针对较亮和面向任务的方案。</span><span class="sxs-lookup"><span data-stu-id="1577d-182">You should use these sparingly and for scenarios that are light and task oriented.</span></span>

### <a name="use-cases"></a><span data-ttu-id="1577d-183">用例</span><span class="sxs-lookup"><span data-stu-id="1577d-183">Use cases</span></span>

<span data-ttu-id="1577d-184">会议组织者 (（如会议组织者) 可能希望参与者执行以下操作触发会议组织者：</span><span class="sxs-lookup"><span data-stu-id="1577d-184">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="1577d-185">提供简短反馈</span><span class="sxs-lookup"><span data-stu-id="1577d-185">Provide brief feedback</span></span>
* <span data-ttu-id="1577d-186">进行简短调查或轮询</span><span class="sxs-lookup"><span data-stu-id="1577d-186">Take a short survey or poll</span></span>
* <span data-ttu-id="1577d-187">提交批准</span><span class="sxs-lookup"><span data-stu-id="1577d-187">Submit approvals</span></span>
* <span data-ttu-id="1577d-188">获取提醒</span><span class="sxs-lookup"><span data-stu-id="1577d-188">Get reminders</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/use-in-meeting-dialog.png" alt-text="示例演示如何使用会议内对话框。" border="false":::

### <a name="anatomy-in-meeting-dialog"></a><span data-ttu-id="1577d-190">剖析：会议对话</span><span class="sxs-lookup"><span data-stu-id="1577d-190">Anatomy: In-meeting dialog</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-anatomy.png" alt-text="示例显示了会议对话框的结构解析。" border="false":::

|<span data-ttu-id="1577d-192">计数器</span><span class="sxs-lookup"><span data-stu-id="1577d-192">Counter</span></span>|<span data-ttu-id="1577d-193">说明</span><span class="sxs-lookup"><span data-stu-id="1577d-193">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1577d-194">1</span><span class="sxs-lookup"><span data-stu-id="1577d-194">1</span></span>|<span data-ttu-id="1577d-195">**标头**：包括应用程序图标、名称、操作字符串和关闭图标。</span><span class="sxs-lookup"><span data-stu-id="1577d-195">**Header**: Includes app icon, name, action string, and close icon.</span></span>|
|<span data-ttu-id="1577d-196">2 </span><span class="sxs-lookup"><span data-stu-id="1577d-196">2</span></span>|<span data-ttu-id="1577d-197">**iframe**：显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="1577d-197">**iframe**: Displays your app content.</span></span>|

### <a name="anatomy-in-meeting-dialog-header"></a><span data-ttu-id="1577d-198">剖析：会议对话头</span><span class="sxs-lookup"><span data-stu-id="1577d-198">Anatomy: In-meeting dialog header</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-header-anatomy.png" alt-text="示例显示了会议对话标题的结构解析。" border="false":::

<span data-ttu-id="1577d-200">有两个标头变量。</span><span class="sxs-lookup"><span data-stu-id="1577d-200">There are two header variants.</span></span> <span data-ttu-id="1577d-201">如果可能，请使用头像和头像，以强调对话框是否来自某个人。</span><span class="sxs-lookup"><span data-stu-id="1577d-201">When possible, use the variant with the avatar to reinforce that the dialog is coming from a person.</span></span>

|<span data-ttu-id="1577d-202">计数器</span><span class="sxs-lookup"><span data-stu-id="1577d-202">Counter</span></span>|<span data-ttu-id="1577d-203">说明</span><span class="sxs-lookup"><span data-stu-id="1577d-203">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1577d-204">1</span><span class="sxs-lookup"><span data-stu-id="1577d-204">1</span></span>|<span data-ttu-id="1577d-205">**虚拟形象**：启动 "会议" 对话框的人员。</span><span class="sxs-lookup"><span data-stu-id="1577d-205">**Avatar**: Person who initiates the in-meeting dialog.</span></span>|
|<span data-ttu-id="1577d-206">2 </span><span class="sxs-lookup"><span data-stu-id="1577d-206">2</span></span>|<span data-ttu-id="1577d-207">**应用程序图标**</span><span class="sxs-lookup"><span data-stu-id="1577d-207">**App icon**</span></span>|
|<span data-ttu-id="1577d-208">3 </span><span class="sxs-lookup"><span data-stu-id="1577d-208">3</span></span>|<span data-ttu-id="1577d-209">**应用名称**</span><span class="sxs-lookup"><span data-stu-id="1577d-209">**App name**</span></span>|
|<span data-ttu-id="1577d-210">4 </span><span class="sxs-lookup"><span data-stu-id="1577d-210">4</span></span>|<span data-ttu-id="1577d-211">"**关闭" 按钮**：关闭对话框。</span><span class="sxs-lookup"><span data-stu-id="1577d-211">**Close button**: Dismisses the dialog.</span></span>|
|<span data-ttu-id="1577d-212">5 </span><span class="sxs-lookup"><span data-stu-id="1577d-212">5</span></span>|<span data-ttu-id="1577d-213">**操作字符串**：通常说明启动对话框的是谁。</span><span class="sxs-lookup"><span data-stu-id="1577d-213">**Action string**: Typically describes who initiated the dialog.</span></span>|

### <a name="responsive-behavior"></a><span data-ttu-id="1577d-214">响应行为</span><span class="sxs-lookup"><span data-stu-id="1577d-214">Responsive behavior</span></span>

<span data-ttu-id="1577d-215">会议中的对话框的大小可能因不同的方案而异。</span><span class="sxs-lookup"><span data-stu-id="1577d-215">In-meeting dialogs can vary in size to account for different scenarios.</span></span> <span data-ttu-id="1577d-216">请务必保持填充和组件大小。</span><span class="sxs-lookup"><span data-stu-id="1577d-216">Make sure to maintain padding and component sizes.</span></span>

* <span data-ttu-id="1577d-217">**Width**： iframe 宽度是指定范围内的绝对值。</span><span class="sxs-lookup"><span data-stu-id="1577d-217">**Width**: The iframe width is an absolute value within the range you specify.</span></span>
* <span data-ttu-id="1577d-218">**Height**：对话框的高度由 iframe 中的内容决定。</span><span class="sxs-lookup"><span data-stu-id="1577d-218">**Height**: The height of the dialog is determined by the content in the iframe.</span></span> <span data-ttu-id="1577d-219">垂直滚动将接管超出最大高度的内容。</span><span class="sxs-lookup"><span data-stu-id="1577d-219">Vertical scroll takes over for content that exceeds the maximum height.</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-responsive.png" alt-text="示例显示 &quot;会议中&quot; 对话框。宽： Min--280 像素 (248 像素 iframe) 。最大值为460像素 (428 像素 iframe) 。高度：300像素 (iframe) 。" border="false":::

## <a name="after-a-meeting"></a><span data-ttu-id="1577d-221">会议后</span><span class="sxs-lookup"><span data-stu-id="1577d-221">After a meeting</span></span>

<span data-ttu-id="1577d-222">你可以在会议结束后返回到会议并查看应用内容。</span><span class="sxs-lookup"><span data-stu-id="1577d-222">You can go back to a meeting after it ends and view app content.</span></span> <span data-ttu-id="1577d-223">在此示例中，会议组织者可以在 " **Contoso** " 选项卡中查看轮询结果。 (注意：从设计的角度看，会议前后选项卡体验之间没有任何区别。 ) </span><span class="sxs-lookup"><span data-stu-id="1577d-223">In this example, the meeting organizer can look at poll results in the **Contoso** tab. (Note: From a design standpoint, there's no difference between a the pre- and post-meeting tab experience.)</span></span>

:::image type="content" source="../../assets/images/apps-in-meetings/post-meeting-experience.png" alt-text="示例显示 &quot;会议后&quot; 选项卡。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="1577d-225">最佳做法</span><span class="sxs-lookup"><span data-stu-id="1577d-225">Best practices</span></span>

### <a name="interactions"></a><span data-ttu-id="1577d-226">相互作用</span><span class="sxs-lookup"><span data-stu-id="1577d-226">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-limit-the-number-of-interactions"></a><span data-ttu-id="1577d-228">操作：限制交互的数量</span><span class="sxs-lookup"><span data-stu-id="1577d-228">Do: Limit the number of interactions</span></span>

<span data-ttu-id="1577d-229">对于 "会议中" 对话框，删除不会帮助用户快速完成某些不必要的内容。</span><span class="sxs-lookup"><span data-stu-id="1577d-229">For in-meeting dialogs, remove unnecessary content that doesn't help users accomplish something quickly.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/interaction-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="1577d-231">请勿：引入不必要的元素</span><span class="sxs-lookup"><span data-stu-id="1577d-231">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="1577d-232">具有多个交互组件的单个会议对话可以分散呼叫。</span><span class="sxs-lookup"><span data-stu-id="1577d-232">A single in-meeting dialog with multiple interactions can distract from the call.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="1577d-233">布局</span><span class="sxs-lookup"><span data-stu-id="1577d-233">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-use-single-column-layouts"></a><span data-ttu-id="1577d-235">Do： Use 单列版式</span><span class="sxs-lookup"><span data-stu-id="1577d-235">Do: Use single-column layouts</span></span>

<span data-ttu-id="1577d-236">由于对话位于会议阶段的中心，因此任务完成应快速而简单，以避免用户不满。</span><span class="sxs-lookup"><span data-stu-id="1577d-236">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-layout-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="1577d-238">不：打乱空间</span><span class="sxs-lookup"><span data-stu-id="1577d-238">Don't: Clutter the space</span></span>

<span data-ttu-id="1577d-239">密集或过于复杂的内容可能会分散注意力，尤其是在会议过程中。</span><span class="sxs-lookup"><span data-stu-id="1577d-239">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-use-single-columns"></a><span data-ttu-id="1577d-241">操作：使用单个列</span><span class="sxs-lookup"><span data-stu-id="1577d-241">Do: Use single columns</span></span>

<span data-ttu-id="1577d-242">在给定会议的选项卡的范围内，强烈建议在一列中显示内容。</span><span class="sxs-lookup"><span data-stu-id="1577d-242">Given the in-meeting tab's narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-layout-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-use-multiple-columns"></a><span data-ttu-id="1577d-244">请勿：使用多个列</span><span class="sxs-lookup"><span data-stu-id="1577d-244">Don't: Use multiple columns</span></span>

<span data-ttu-id="1577d-245">由于 "会议" 选项卡的空间有限，不建议使用多列布局。</span><span class="sxs-lookup"><span data-stu-id="1577d-245">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="1577d-246">控件</span><span class="sxs-lookup"><span data-stu-id="1577d-246">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="1577d-248">操作：将主要操作右对齐</span><span class="sxs-lookup"><span data-stu-id="1577d-248">Do: Right align the primary action</span></span>

<span data-ttu-id="1577d-249">我们建议 positioining 对最右侧位置的最大视觉上的操作。</span><span class="sxs-lookup"><span data-stu-id="1577d-249">We recommend positioining the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-controls-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="1577d-251">不：左对齐或居中对齐操作</span><span class="sxs-lookup"><span data-stu-id="1577d-251">Don't: Left or center align actions</span></span>

<span data-ttu-id="1577d-252">这与对话框中的控件放置的标准团队模式不同，可能与顶部的对话框冲突。</span><span class="sxs-lookup"><span data-stu-id="1577d-252">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scroll"></a><span data-ttu-id="1577d-253">Scroll</span><span class="sxs-lookup"><span data-stu-id="1577d-253">Scroll</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="1577d-255">Do：垂直滚动</span><span class="sxs-lookup"><span data-stu-id="1577d-255">Do: Scroll vertically</span></span>

<span data-ttu-id="1577d-256">建议将最具视觉的繁重操作定位到最右侧的位置。</span><span class="sxs-lookup"><span data-stu-id="1577d-256">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-scroll-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="1577d-258">不：水平滚动</span><span class="sxs-lookup"><span data-stu-id="1577d-258">Don't: Scroll horizontally</span></span>

<span data-ttu-id="1577d-259">水平滚动不是团队中的预期行为。</span><span class="sxs-lookup"><span data-stu-id="1577d-259">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="1577d-260">会议环境中的其他画布将垂直滚动。</span><span class="sxs-lookup"><span data-stu-id="1577d-260">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="workflows"></a><span data-ttu-id="1577d-261">工作流</span><span class="sxs-lookup"><span data-stu-id="1577d-261">Workflows</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-workflow-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-surface-complex-scenarios-in-the-in-meeting-tab"></a><span data-ttu-id="1577d-263">操作：会议中选项卡中的表面复杂方案</span><span class="sxs-lookup"><span data-stu-id="1577d-263">Do: Surface complex scenarios in the in-meeting tab</span></span>

<span data-ttu-id="1577d-264">如果您的应用程序包含多个任务，强烈建议在 "会议" 选项卡中使用单列版式。</span><span class="sxs-lookup"><span data-stu-id="1577d-264">If your app includes multiple tasks, we strongly recommend a single-column layout in an in-meeting tab.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-dialog-workflow-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-package-complex-scenarios-in-the-in-meeting-dialog"></a><span data-ttu-id="1577d-266">不：在会议对话中打包复杂方案</span><span class="sxs-lookup"><span data-stu-id="1577d-266">Don't: Package complex scenarios in the in-meeting dialog</span></span>

<span data-ttu-id="1577d-267">会议中的对话框用于进行简要交互。</span><span class="sxs-lookup"><span data-stu-id="1577d-267">In-meeting dialogs are intended for brief interactions.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="1577d-268">主题</span><span class="sxs-lookup"><span data-stu-id="1577d-268">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-use-teams-color-tokens"></a><span data-ttu-id="1577d-270">任务：使用团队颜色标记</span><span class="sxs-lookup"><span data-stu-id="1577d-270">Do: Use Teams color tokens</span></span>

<span data-ttu-id="1577d-271">团队会议针对深色模式进行了优化，以帮助减少视觉和认知干扰，以便用户可以将注意力集中在讨论和共享内容上。</span><span class="sxs-lookup"><span data-stu-id="1577d-271">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span> <span data-ttu-id="1577d-272">了解如何使用 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">颜色令牌 (熟知的 UI) </a>。</span><span class="sxs-lookup"><span data-stu-id="1577d-272">Learn about using <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a>.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-theming-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="1577d-274">请勿：包含另一个消除按钮</span><span class="sxs-lookup"><span data-stu-id="1577d-274">Don't: Include another dismiss button</span></span>

<span data-ttu-id="1577d-275">提供用于关闭 "会议" 选项卡内容的选项可能会导致出现问题，因为标头中已有一个按钮可消除 "会议" 选项卡本身。</span><span class="sxs-lookup"><span data-stu-id="1577d-275">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="1577d-276">导航</span><span class="sxs-lookup"><span data-stu-id="1577d-276">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-do.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="1577d-278">操作：有一个 "后退" 按钮</span><span class="sxs-lookup"><span data-stu-id="1577d-278">Do: Have a back button</span></span>

<span data-ttu-id="1577d-279">如果在 "会议" 选项卡中有多个导航层，则用户必须能够返回到其以前的视图。</span><span class="sxs-lookup"><span data-stu-id="1577d-279">If you have more than one layer of navigation in an in-meeting tab, users must be able to go back to their previous views.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-dont.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="dont-include-another-dismiss-button"></a><span data-ttu-id="1577d-281">请勿：包含另一个消除按钮</span><span class="sxs-lookup"><span data-stu-id="1577d-281">Don't: Include another dismiss button</span></span>

<span data-ttu-id="1577d-282">提供用于关闭 "会议" 选项卡内容的选项可能会导致出现问题，因为标头中已有一个按钮可消除 "会议" 选项卡本身。</span><span class="sxs-lookup"><span data-stu-id="1577d-282">Providing an option to close in-meeting tab content may cause issues since there’s already a button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/apps-in-meetings/in-meeting-tab-nav-caution.png" alt-text="显示会议扩展最佳实践的示例。" border="false":::

#### <a name="caution-avoid-modals-within-the-in-meeting-tab"></a><span data-ttu-id="1577d-284">警告：避免在会议中选项卡中模式</span><span class="sxs-lookup"><span data-stu-id="1577d-284">Caution: Avoid modals within the in-meeting tab</span></span>

<span data-ttu-id="1577d-285">在 "已过窄的会议" 选项卡中) 的模式 (也称为 "任务模块" 可能会自动换行并掩盖内容。</span><span class="sxs-lookup"><span data-stu-id="1577d-285">Modals (also known as task modules) in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="validate-your-design"></a><span data-ttu-id="1577d-286">验证设计</span><span class="sxs-lookup"><span data-stu-id="1577d-286">Validate your design</span></span>

<span data-ttu-id="1577d-287">如果计划将应用程序发布到 AppSource，则应了解通常会在提交期间导致应用程序失败的设计问题。</span><span class="sxs-lookup"><span data-stu-id="1577d-287">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1577d-288">检查设计验证准则</span><span class="sxs-lookup"><span data-stu-id="1577d-288">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
