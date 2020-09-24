---
title: 设计 Microsoft 团队会议选项卡
author: heath-hamilton
description: 为 Microsoft 团队设计 "会议" 选项卡的指南和最佳实践。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 4f75591468de41b5d4d3ac62a25b93412b3fccaa
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "48243331"
---
# <a name="design-an-in-meeting-tab"></a><span data-ttu-id="62eba-103">设计会议内的选项卡</span><span class="sxs-lookup"><span data-stu-id="62eba-103">Design an in-meeting tab</span></span>

<span data-ttu-id="62eba-104">"会议" 选项卡是在会议过程中充实协作的画布。</span><span class="sxs-lookup"><span data-stu-id="62eba-104">The in-meeting tab is a canvas for augmenting collaboration during meetings.</span></span> <span data-ttu-id="62eba-105">根据 "团队" 选项卡功能，与会者可以通过共享或基于角色的视图在会议阶段外的专用空间中查看应用程序内容并与之交互。</span><span class="sxs-lookup"><span data-stu-id="62eba-105">Based on the Teams tab capability, attendees can see and interact with app content in a dedicated space outside the meeting stage through shared or role-based views.</span></span>

## <a name="use-cases"></a><span data-ttu-id="62eba-106">用例</span><span class="sxs-lookup"><span data-stu-id="62eba-106">Use cases</span></span>

<span data-ttu-id="62eba-107">用户可能会使用 "会议" 选项卡执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="62eba-107">People might use the in-meeting tab to:</span></span>

* <span data-ttu-id="62eba-108">提供详细反馈 (例如，评估求职候选人) </span><span class="sxs-lookup"><span data-stu-id="62eba-108">Provide detailed feedback (for example, evaluate a job candidate)</span></span>
* <span data-ttu-id="62eba-109">为会议参与者快速创建轮询、调查或任务项</span><span class="sxs-lookup"><span data-stu-id="62eba-109">Quickly create a poll, survey, or task item for the meeting participants</span></span>
* <span data-ttu-id="62eba-110">显示与会议相关的注释 (例如，有关销售线索的信息) </span><span class="sxs-lookup"><span data-stu-id="62eba-110">Display notes relevant to the meeting (for example, information about a sales lead)</span></span>

## <a name="example"></a><span data-ttu-id="62eba-111">示例</span><span class="sxs-lookup"><span data-stu-id="62eba-111">Example</span></span>

<span data-ttu-id="62eba-112">以下示例显示了显示调查应用程序内容的 "会议" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="62eba-112">The following example shows the in-meeting tab displaying survey app content.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-organizer-view.png" alt-text="示例显示会议组织者的视角中会议 "会议" 选项卡的外观。":::

<span data-ttu-id="62eba-114"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">请参阅完整的方案 (Figma) </a></span><span class="sxs-lookup"><span data-stu-id="62eba-114"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See the full scenario (Figma)</a></span></span>

<span data-ttu-id="62eba-115"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">请参阅其他示例用例 (Figma) </a></span><span class="sxs-lookup"><span data-stu-id="62eba-115"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See other example use cases (Figma)</a></span></span>

## <a name="anatomy"></a><span data-ttu-id="62eba-116">解析</span><span class="sxs-lookup"><span data-stu-id="62eba-116">Anatomy</span></span>

<span data-ttu-id="62eba-117">"会议" 选项卡将使用以下维度显示您的应用程序内容：</span><span class="sxs-lookup"><span data-stu-id="62eba-117">The in-meeting tab displays your app content using the following dimensions:</span></span>

* <span data-ttu-id="62eba-118">**宽度**：280像素用于 web 视图区域。</span><span class="sxs-lookup"><span data-stu-id="62eba-118">**Width**: 280 pixels for the webview area.</span></span> <span data-ttu-id="62eba-119">在 web 视图的左侧和右侧有20像素的填充。</span><span class="sxs-lookup"><span data-stu-id="62eba-119">There are 20 pixels of padding on the left and right sides of the webview.</span></span>
* <span data-ttu-id="62eba-120">**高度**：完全出血到选项卡的底部。在 web 视图区域和选项卡头之间有20像素的填充。</span><span class="sxs-lookup"><span data-stu-id="62eba-120">**Height**: Full bleed to the bottom of the tab. There are 20 pixels of padding between the webview area and tab header.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-anatomy.png" alt-text="显示会议扩展 "会议" 选项卡的 UI 剖析的插图。" border="false":::

1. <span data-ttu-id="62eba-122">**应用图标**： "会议中" 选项卡的入口点。</span><span class="sxs-lookup"><span data-stu-id="62eba-122">**App icon**: The entry point to the in-meeting tab.</span></span>
1. <span data-ttu-id="62eba-123">**标头**：包含选项卡名称。</span><span class="sxs-lookup"><span data-stu-id="62eba-123">**Header**: Includes the tab name.</span></span>
1. <span data-ttu-id="62eba-124">**名称**：选项卡实例的名称。</span><span class="sxs-lookup"><span data-stu-id="62eba-124">**Name**: The name of the tab instance.</span></span>
1. <span data-ttu-id="62eba-125">**消除**：关闭选项卡。始终使用右上关闭图标而不是页脚中的操作。</span><span class="sxs-lookup"><span data-stu-id="62eba-125">**Dismiss**: Dismisses the tab. Always use the upper-right close icon instead of an action in the footer.</span></span>
1. <span data-ttu-id="62eba-126">**Web 视图**：显示所有第三方应用程序内容。</span><span class="sxs-lookup"><span data-stu-id="62eba-126">**Webview**: Displays all third-party app content.</span></span>

## <a name="behavior"></a><span data-ttu-id="62eba-127">行为</span><span class="sxs-lookup"><span data-stu-id="62eba-127">Behavior</span></span>

### <a name="scale"></a><span data-ttu-id="62eba-128">Scale</span><span class="sxs-lookup"><span data-stu-id="62eba-128">Scale</span></span>

<span data-ttu-id="62eba-129">目前，"会议中" 选项卡的宽度是固定的。</span><span class="sxs-lookup"><span data-stu-id="62eba-129">Currently, the width of the in-meeting tab is fixed.</span></span>

### <a name="scrolling"></a><span data-ttu-id="62eba-130">上下</span><span class="sxs-lookup"><span data-stu-id="62eba-130">Scrolling</span></span>

<span data-ttu-id="62eba-131">以下是有关在 "会议" 选项卡中滚动的内容：</span><span class="sxs-lookup"><span data-stu-id="62eba-131">Here's what to know about scrolling in the in-meeting tab:</span></span>

* <span data-ttu-id="62eba-132">应仅能够垂直滚动。</span><span class="sxs-lookup"><span data-stu-id="62eba-132">You should only be able to scroll vertically.</span></span>
* <span data-ttu-id="62eba-133">您只能看到您已滚动的内容 (不在) 以上或之下的任何内容。</span><span class="sxs-lookup"><span data-stu-id="62eba-133">You can only see the content you've scrolled to (nothing above or below).</span></span>
* <span data-ttu-id="62eba-134">滚动条是 web 视图内容的一部分。</span><span class="sxs-lookup"><span data-stu-id="62eba-134">The scrollbar is part of the webview content.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll.png" alt-text="显示如何在 "会议" 选项卡中滚动 web 视图内容的工作方式的图示。" border="false":::

### <a name="navigation"></a><span data-ttu-id="62eba-136">导航</span><span class="sxs-lookup"><span data-stu-id="62eba-136">Navigation</span></span>

<span data-ttu-id="62eba-137">对于具有导航层或较大内容的方案，建议允许用户导航到辅助层。</span><span class="sxs-lookup"><span data-stu-id="62eba-137">For scenarios with navigation layers or heavy content, we recommend allowing users to navigate to a secondary layer.</span></span> <span data-ttu-id="62eba-138">用户必须能够返回到上一层。</span><span class="sxs-lookup"><span data-stu-id="62eba-138">Users must be able to go back to the previous layer.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav.png" alt-text="显示如何在 "会议" 选项卡中导航到辅助图层的图示工作方式。" border="false":::

## <a name="components"></a><span data-ttu-id="62eba-140">组件</span><span class="sxs-lookup"><span data-stu-id="62eba-140">Components</span></span>

<span data-ttu-id="62eba-141">"在会议中" 选项卡主要是基于以下 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI 组件（ (Figma) </a>）生成的，这是基于 " <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">流畅设计" 系统</a>的。</span><span class="sxs-lookup"><span data-stu-id="62eba-141">In-meeting tabs are built primarily with the following <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI components (Figma)</a>, which are based on the <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent Design System</a>.</span></span>

<span data-ttu-id="62eba-142">组件</span><span class="sxs-lookup"><span data-stu-id="62eba-142">Component</span></span> | <span data-ttu-id="62eba-143">准则</span><span class="sxs-lookup"><span data-stu-id="62eba-143">Guidelines</span></span> | <span data-ttu-id="62eba-144">示例</span><span class="sxs-lookup"><span data-stu-id="62eba-144">Example</span></span>
 - | - | -
<span data-ttu-id="62eba-145">按钮</span><span class="sxs-lookup"><span data-stu-id="62eba-145">Button</span></span> | <span data-ttu-id="62eba-146">主要和次要按钮可以是中型或小型</span><span class="sxs-lookup"><span data-stu-id="62eba-146">Primary and secondary buttons can be medium or small</span></span> | <span data-ttu-id="62eba-147">发送响应</span><span class="sxs-lookup"><span data-stu-id="62eba-147">Send a response</span></span>
<span data-ttu-id="62eba-148">Input</span><span class="sxs-lookup"><span data-stu-id="62eba-148">Input</span></span> | <span data-ttu-id="62eba-149">用于简短用户输入的字段。</span><span class="sxs-lookup"><span data-stu-id="62eba-149">Field for brief user input.</span></span> <span data-ttu-id="62eba-150">标签文本可以包含图标</span><span class="sxs-lookup"><span data-stu-id="62eba-150">Label text can include an icon</span></span>  | <span data-ttu-id="62eba-151">输入反馈</span><span class="sxs-lookup"><span data-stu-id="62eba-151">Enter feedback</span></span>
<span data-ttu-id="62eba-152">下拉列表</span><span class="sxs-lookup"><span data-stu-id="62eba-152">Dropdown</span></span> | <span data-ttu-id="62eba-153">从列表中选择一个或多个选项。</span><span class="sxs-lookup"><span data-stu-id="62eba-153">Select one or more options from a list.</span></span> <span data-ttu-id="62eba-154">可以包括搜索和多选功能</span><span class="sxs-lookup"><span data-stu-id="62eba-154">Can include search and multi-selection features</span></span> | <span data-ttu-id="62eba-155">选择语言</span><span class="sxs-lookup"><span data-stu-id="62eba-155">Choose a language</span></span>
<span data-ttu-id="62eba-156">选择控件</span><span class="sxs-lookup"><span data-stu-id="62eba-156">Selection controls</span></span> | <span data-ttu-id="62eba-157">将 checkbox 用于多个选项或单选按钮，然后切换选择单个选项。</span><span class="sxs-lookup"><span data-stu-id="62eba-157">Use checkboxes for multiple choices or radio buttons and toggles for single choices.</span></span> <span data-ttu-id="62eba-158">有关更详细的选择，请使用滑块</span><span class="sxs-lookup"><span data-stu-id="62eba-158">For more detailed selections, use a slider</span></span> | <span data-ttu-id="62eba-159">投票中的投票</span><span class="sxs-lookup"><span data-stu-id="62eba-159">Vote in a poll</span></span>
<span data-ttu-id="62eba-160">警报</span><span class="sxs-lookup"><span data-stu-id="62eba-160">Alerts</span></span> | <span data-ttu-id="62eba-161">无论是显示紧急邮件、错误状态还是警告，邮件都应短，并且不会中断用户的当前任务</span><span class="sxs-lookup"><span data-stu-id="62eba-161">Whether displaying an urgent message, error state, or warning, the message should be short and won't interrupt the user's current task</span></span> | <span data-ttu-id="62eba-162">提交响应时显示问题</span><span class="sxs-lookup"><span data-stu-id="62eba-162">Display issue when submitting a response</span></span>

## <a name="theming"></a><span data-ttu-id="62eba-163">主题</span><span class="sxs-lookup"><span data-stu-id="62eba-163">Theming</span></span>

### <a name="colors"></a><span data-ttu-id="62eba-164">颜色</span><span class="sxs-lookup"><span data-stu-id="62eba-164">Colors</span></span>

<span data-ttu-id="62eba-165">将 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">推荐的配色方案 (Figma) </a> 用于背景、foregrounds 和传达状态。</span><span class="sxs-lookup"><span data-stu-id="62eba-165">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended color scheme (Figma)</a> for backgrounds, foregrounds, and conveying states.</span></span>

### <a name="typography"></a><span data-ttu-id="62eba-166">版式</span><span class="sxs-lookup"><span data-stu-id="62eba-166">Typography</span></span>

<span data-ttu-id="62eba-167">对标题、正文文本和元数据文本使用 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">建议的字体大小和权重 (Figma) </a> 。</span><span class="sxs-lookup"><span data-stu-id="62eba-167">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended font sizes and weights (Figma)</a> for titles, body text, and metadata text.</span></span>

## <a name="best-practices"></a><span data-ttu-id="62eba-168">最佳做法</span><span class="sxs-lookup"><span data-stu-id="62eba-168">Best practices</span></span>

### <a name="responsiveness"></a><span data-ttu-id="62eba-169">性</span><span class="sxs-lookup"><span data-stu-id="62eba-169">Responsiveness</span></span>

<span data-ttu-id="62eba-170">会议选项卡布局应能够扩展到各种大小。</span><span class="sxs-lookup"><span data-stu-id="62eba-170">In-meeting tab layouts should be able to scale to various sizes.</span></span> <span data-ttu-id="62eba-171">考虑选项卡在会议前后的缩放方式并拍摄形状。</span><span class="sxs-lookup"><span data-stu-id="62eba-171">Consider how the tab will scale and take shape before, during, and after the meeting.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-before-meeting.png" alt-text="插图显示会议中的选项卡内容看起来像是会议前后的全屏选项卡。" border="false":::

#### <a name="before-the-meeting"></a><span data-ttu-id="62eba-173">会议之前</span><span class="sxs-lookup"><span data-stu-id="62eba-173">Before the meeting</span></span>

<span data-ttu-id="62eba-174">确保您的选项卡布局可以适应不同语言的右侧或左侧布局，并且该控件将移动到正确的位置。</span><span class="sxs-lookup"><span data-stu-id="62eba-174">Make sure your tab layout can adapt to a right or left layout for different languages and that controls move to the correct locations.</span></span> <span data-ttu-id="62eba-175"> (会议前版式也可应用于会议后的版式。 ) </span><span class="sxs-lookup"><span data-stu-id="62eba-175">(Pre-meeting layouts can also apply to post-meeting layouts.)</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-during-meeting.png" alt-text="显示会议期间如何将会议前选项卡内容压缩到 "会议" 选项卡的插图。" border="false":::

#### <a name="during-the-meeting"></a><span data-ttu-id="62eba-177">会议期间</span><span class="sxs-lookup"><span data-stu-id="62eba-177">During the meeting</span></span>

<span data-ttu-id="62eba-178">将选项卡内容调整到会议选项卡布局和位置。</span><span class="sxs-lookup"><span data-stu-id="62eba-178">Tab content adjusts to the in-meeting tab layout and location.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="62eba-179">主题</span><span class="sxs-lookup"><span data-stu-id="62eba-179">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-theming-do.png" alt-text="演示如何为团队会议中使用的深色主题设计 "会议" 选项卡。" border="false":::

#### <a name="do-design-for-a-dark-theme"></a><span data-ttu-id="62eba-181">Do：深色主题的设计</span><span class="sxs-lookup"><span data-stu-id="62eba-181">Do: Design for a dark theme</span></span>

<span data-ttu-id="62eba-182">团队会议针对深色模式进行了优化，以帮助减少视觉和认知干扰，以便用户可以将注意力集中在讨论和共享内容上。</span><span class="sxs-lookup"><span data-stu-id="62eba-182">Teams meetings are optimized for dark mode to help reduce visual and cognitive noise so users can focus on the discussion and shared content.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-theming-dont.png" alt-text="插图显示您不应使用未 conducive 到 "团队深色" 主题的颜色。" border="false":::

#### <a name="dont-use-unfamiliar-colors"></a><span data-ttu-id="62eba-184">不：使用不熟悉的颜色</span><span class="sxs-lookup"><span data-stu-id="62eba-184">Don't: Use unfamiliar colors</span></span>

<span data-ttu-id="62eba-185">与会议环境冲突的颜色可能会分散注意力，并使其在工作组中的显示较少。</span><span class="sxs-lookup"><span data-stu-id="62eba-185">Colors that clash with the meeting environment may be distracting and appear less native to Teams.</span></span>

   :::column-end:::
:::row-end:::

### <a name="scrolling"></a><span data-ttu-id="62eba-186">上下</span><span class="sxs-lookup"><span data-stu-id="62eba-186">Scrolling</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll-do.png" alt-text="图中显示只允许在 "会议" 选项卡中进行垂直滚动。" border="false":::

#### <a name="do-scroll-vertically"></a><span data-ttu-id="62eba-188">Do：垂直滚动</span><span class="sxs-lookup"><span data-stu-id="62eba-188">Do: Scroll vertically</span></span>

<span data-ttu-id="62eba-189">用户在团队中预测垂直滚动 (和其他) 。</span><span class="sxs-lookup"><span data-stu-id="62eba-189">Users anticipate vertical scrolling in Teams (and elsewhere).</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-scroll-dont.png" alt-text="显示显示不应允许在 "会议" 选项卡中水平滚动的图示。" border="false":::

#### <a name="dont-scroll-horizontally"></a><span data-ttu-id="62eba-191">不：水平滚动</span><span class="sxs-lookup"><span data-stu-id="62eba-191">Don't: Scroll horizontally</span></span>

<span data-ttu-id="62eba-192">水平滚动不是团队中的预期行为。</span><span class="sxs-lookup"><span data-stu-id="62eba-192">Horizontal scrolling isn’t an expected behavior in Teams.</span></span> <span data-ttu-id="62eba-193">会议环境中的其他画布将垂直滚动。</span><span class="sxs-lookup"><span data-stu-id="62eba-193">Other canvases in the meeting environment scroll vertically.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="62eba-194">布局</span><span class="sxs-lookup"><span data-stu-id="62eba-194">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-layout-do.png" alt-text="图示在 "会议" 选项卡中显示建议的单列版式。" border="false":::

#### <a name="do-single-columns"></a><span data-ttu-id="62eba-196">操作：单个列</span><span class="sxs-lookup"><span data-stu-id="62eba-196">Do: Single columns</span></span>

<span data-ttu-id="62eba-197">在给定会议的选项卡的范围内，强烈建议在一列中显示内容。</span><span class="sxs-lookup"><span data-stu-id="62eba-197">Given the in-meeting tab’s narrow nature, we strongly recommend displaying the contents in a single column.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-layout-dont.png" alt-text="显示 "会议" 选项卡中的两列布局不理想的图示。" border="false":::

#### <a name="dont-multiple-columns"></a><span data-ttu-id="62eba-199">不：多个列</span><span class="sxs-lookup"><span data-stu-id="62eba-199">Don't: Multiple columns</span></span>

<span data-ttu-id="62eba-200">由于 "会议" 选项卡的空间有限，不建议使用多列布局。</span><span class="sxs-lookup"><span data-stu-id="62eba-200">Due to the limited space of the in-meeting tab, layouts with more than one column aren’t recommended.</span></span>

   :::column-end:::
:::row-end:::

### <a name="navigation"></a><span data-ttu-id="62eba-201">导航</span><span class="sxs-lookup"><span data-stu-id="62eba-201">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-do.png" alt-text="图显示如果您的会议选项卡应用程序有多个导航层，则应始终提供 "后退" 按钮。" border="false":::

#### <a name="do-have-a-back-button"></a><span data-ttu-id="62eba-203">操作：有一个 "后退" 按钮</span><span class="sxs-lookup"><span data-stu-id="62eba-203">Do: Have a back button</span></span>

<span data-ttu-id="62eba-204">如果您有多个导航层，则用户必须能够回退到其以前的视图。</span><span class="sxs-lookup"><span data-stu-id="62eba-204">If you have more than one layer of navigation, users must be able to go back to their previous view.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-dont.png" alt-text="图中显示在导航的 "会议" 选项卡中添加另一个 "关闭" 按钮是多余的，可能会导致问题。" border="false":::

#### <a name="dont-include-another-close-button"></a><span data-ttu-id="62eba-206">不：包含另一个 "关闭" 按钮</span><span class="sxs-lookup"><span data-stu-id="62eba-206">Don't: Include another close button</span></span>

<span data-ttu-id="62eba-207">提供用于关闭 "会议" 选项卡内容的选项可能会导致出现问题，因为标头中已有 "关闭" 按钮来消除会议中的选项卡本身。</span><span class="sxs-lookup"><span data-stu-id="62eba-207">Providing an option to close in-meeting tab content may cause issues since there’s already a close button in the header to dismiss the in-meeting tab itself.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-tab-nav-caution.png" alt-text="图示在使用模式时需要谨慎 (例如，任务模块在 "会议" 选项卡中) 在给定有限的空间。" border="false":::

#### <a name="caution-using-dialogs-in-a-narrow-space"></a><span data-ttu-id="62eba-209">警告：在窄间距中使用对话</span><span class="sxs-lookup"><span data-stu-id="62eba-209">Caution: Using dialogs in a narrow space</span></span>

<span data-ttu-id="62eba-210">在 "已缩小的会议" 选项卡中的对话框（如任务模块）可能会自动换行并掩盖内容。</span><span class="sxs-lookup"><span data-stu-id="62eba-210">Dialogs, such as task modules, in the already narrow in-meeting tab might wrap and obscure the content.</span></span>

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a><span data-ttu-id="62eba-211">辅助功能</span><span class="sxs-lookup"><span data-stu-id="62eba-211">Accessibility</span></span>

<span data-ttu-id="62eba-212">有关辅助功能的信息，请参阅 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>。</span><span class="sxs-lookup"><span data-stu-id="62eba-212">For information on accessibility, see <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

## <a name="resources"></a><span data-ttu-id="62eba-213">资源</span><span class="sxs-lookup"><span data-stu-id="62eba-213">Resources</span></span>

* <span data-ttu-id="62eba-214"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft 团队会议扩展 Figma 文件</a></span><span class="sxs-lookup"><span data-stu-id="62eba-214"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft Teams meeting extensions Figma file</a></span></span>
* [<span data-ttu-id="62eba-215">选项卡设计指南</span><span class="sxs-lookup"><span data-stu-id="62eba-215">Tabs design guidelines</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="62eba-216">移动设备的选项卡设计指南</span><span class="sxs-lookup"><span data-stu-id="62eba-216">Tabs design guidelines for mobile</span></span>](../../tabs/design/tabs-mobile.md)

## <a name="validate-your-design"></a><span data-ttu-id="62eba-217">验证设计</span><span class="sxs-lookup"><span data-stu-id="62eba-217">Validate your design</span></span>

<span data-ttu-id="62eba-218">如果计划将应用程序发布到 AppSource，则应了解通常会在提交期间导致应用程序失败的设计问题。</span><span class="sxs-lookup"><span data-stu-id="62eba-218">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="62eba-219">检查设计验证准则</span><span class="sxs-lookup"><span data-stu-id="62eba-219">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines)
