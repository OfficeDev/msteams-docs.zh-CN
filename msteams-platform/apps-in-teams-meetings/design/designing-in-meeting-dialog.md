---
title: 设计 Microsoft 团队会议对话
author: heath-hamilton
description: 为 Microsoft 团队设计会议内对话的指南和最佳实践。
ms.author: lajanuar
ms.topic: conceptual
ms.openlocfilehash: 89e532e6dbd83e54269606f6e051fa377de68f62
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "48243322"
---
# <a name="design-an-in-meeting-dialog"></a><span data-ttu-id="03db5-103">设计会议内对话</span><span class="sxs-lookup"><span data-stu-id="03db5-103">Design an in-meeting dialog</span></span>

<span data-ttu-id="03db5-104">会议中的对话框显示在团队会议阶段。</span><span class="sxs-lookup"><span data-stu-id="03db5-104">In-meeting dialogs display on the Teams meeting stage.</span></span> <span data-ttu-id="03db5-105">他们需要用户注意、确认或交互，但这并不会中断会议。</span><span class="sxs-lookup"><span data-stu-id="03db5-105">They require a user's attention, confirmation, or interaction but are subtle and don't interrupt the meeting.</span></span>

## <a name="use-cases"></a><span data-ttu-id="03db5-106">用例</span><span class="sxs-lookup"><span data-stu-id="03db5-106">Use cases</span></span>

<span data-ttu-id="03db5-107">会议组织者 (（如会议组织者) 可能希望参与者执行以下操作触发会议组织者：</span><span class="sxs-lookup"><span data-stu-id="03db5-107">In-meeting dialogs are triggered by a user (such as the meeting organizer) who might want participants to:</span></span>

* <span data-ttu-id="03db5-108">提供简短反馈</span><span class="sxs-lookup"><span data-stu-id="03db5-108">Provide brief feedback</span></span>
* <span data-ttu-id="03db5-109">进行简短调查或轮询</span><span class="sxs-lookup"><span data-stu-id="03db5-109">Take a short survey or poll</span></span>
* <span data-ttu-id="03db5-110">提交批准</span><span class="sxs-lookup"><span data-stu-id="03db5-110">Submit approvals</span></span>
* <span data-ttu-id="03db5-111">获取提醒</span><span class="sxs-lookup"><span data-stu-id="03db5-111">Get reminders</span></span>

## <a name="example"></a><span data-ttu-id="03db5-112">示例</span><span class="sxs-lookup"><span data-stu-id="03db5-112">Example</span></span>

<span data-ttu-id="03db5-113">下面的示例显示会议参与者的角度看，会议中的对话框可能是什么样子的。</span><span class="sxs-lookup"><span data-stu-id="03db5-113">The following example shows what the in-meeting dialog might look like from a meeting participant's perspective.</span></span> <span data-ttu-id="03db5-114">正如您所看到的，内容和任务是轻型的。</span><span class="sxs-lookup"><span data-stu-id="03db5-114">As you can see, the content and task are lightweight.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-participant-view.png" alt-text="示例显示会议参与者的视角中会议对话框的外观。":::

<span data-ttu-id="03db5-116"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">请参阅完整的方案 (Figma) </a></span><span class="sxs-lookup"><span data-stu-id="03db5-116"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See the full scenario (Figma)</a></span></span>

<span data-ttu-id="03db5-117"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">请参阅其他示例用例 (Figma) </a></span><span class="sxs-lookup"><span data-stu-id="03db5-117"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See other example use cases (Figma)</a></span></span>

## <a name="anatomy"></a><span data-ttu-id="03db5-118">解析</span><span class="sxs-lookup"><span data-stu-id="03db5-118">Anatomy</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-anatomy.png" alt-text="会议中的对话框视图的 UI 剖析。" border="false":::

1. <span data-ttu-id="03db5-120">**应用程序图标**</span><span class="sxs-lookup"><span data-stu-id="03db5-120">**App icon**</span></span>
1. <span data-ttu-id="03db5-121">**应用名称**</span><span class="sxs-lookup"><span data-stu-id="03db5-121">**App name**</span></span>
1. <span data-ttu-id="03db5-122">**操作字符串**</span><span class="sxs-lookup"><span data-stu-id="03db5-122">**Action string**</span></span>
1. <span data-ttu-id="03db5-123">**消除图标：** 关闭单个对话框。</span><span class="sxs-lookup"><span data-stu-id="03db5-123">**Dismiss icon:** Closes a single dialog.</span></span> <span data-ttu-id="03db5-124">始终使用右上关闭图标而不是页脚中的操作。</span><span class="sxs-lookup"><span data-stu-id="03db5-124">Always use the upper-right close icon instead of an action in the footer.</span></span>
1. <span data-ttu-id="03db5-125">**Web 视图**：显示所有第三方应用程序内容和按钮 (标准团队按钮的建议) 。</span><span class="sxs-lookup"><span data-stu-id="03db5-125">**Webview**: Displays all third-party app content and buttons (standard Teams buttons recommended).</span></span>

### <a name="sizing"></a><span data-ttu-id="03db5-126">调整</span><span class="sxs-lookup"><span data-stu-id="03db5-126">Sizing</span></span>

<span data-ttu-id="03db5-127">会议中的对话框的大小可能因不同的用例而异，但您必须始终保留填充和组件大小。</span><span class="sxs-lookup"><span data-stu-id="03db5-127">In-meeting dialogs can vary in size to account for different use cases, but you must always maintain padding and component sizes.</span></span>

* <span data-ttu-id="03db5-128">**高度**：对话框的高度由 web 视图中的内容决定。</span><span class="sxs-lookup"><span data-stu-id="03db5-128">**Height**: The height of the dialog is determined by the content in the webview.</span></span> <span data-ttu-id="03db5-129">垂直滚动将接管超出您指定的最大高度的内容。</span><span class="sxs-lookup"><span data-stu-id="03db5-129">Vertical scroll takes over for content that exceeds the maximum height you specify.</span></span>
* <span data-ttu-id="03db5-130">**宽度**： web 视图的宽度是指定范围内的绝对值。</span><span class="sxs-lookup"><span data-stu-id="03db5-130">**Width**: The width of the webview is an absolute value within the range you specify.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-sizing.png" alt-text="显示会议对话的可能尺寸的图示。高度：对话框的高度由 web 视图中的内容决定。垂直滚动将接管超出) 所定义的最大高度 (的内容。最小值：无。最大值：400像素 (320 像素 web 视图) 。宽度： web 视图的宽度是指定范围内的绝对值。最小值：288像素 (256 像素 web 视图) 。最大值：468像素 (436 像素 web 视图) 。" border="false":::

## <a name="behavior"></a><span data-ttu-id="03db5-132">行为</span><span class="sxs-lookup"><span data-stu-id="03db5-132">Behavior</span></span>

<span data-ttu-id="03db5-133">请参阅 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>中的常规会议对话行为，如 rest、加载等。</span><span class="sxs-lookup"><span data-stu-id="03db5-133">See general in-meeting dialog behavior, such as rest, loading, and more, in <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

### <a name="position"></a><span data-ttu-id="03db5-134">Position</span><span class="sxs-lookup"><span data-stu-id="03db5-134">Position</span></span>

<span data-ttu-id="03db5-135">会议中的对话在会议阶段居中对齐。</span><span class="sxs-lookup"><span data-stu-id="03db5-135">In-meeting dialogs are aligned in the center of the meeting stage.</span></span> <span data-ttu-id="03db5-136">无法在团队系统级通知框架中拖动和工作它们。</span><span class="sxs-lookup"><span data-stu-id="03db5-136">They can’t be dragged and work within the framework of Teams system-level notifications.</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-position.png" alt-text="显示会议对话的 UI 剖析的插图。" border="false":::

### <a name="aggregation"></a><span data-ttu-id="03db5-138">聚合</span><span class="sxs-lookup"><span data-stu-id="03db5-138">Aggregation</span></span>

<span data-ttu-id="03db5-139">一次仅显示一个对话框，从最后一次向下发送到最新的堆栈排名。</span><span class="sxs-lookup"><span data-stu-id="03db5-139">Only one dialog displays at a time, stack ranking from last to most recent sent to the bottom.</span></span> <span data-ttu-id="03db5-140">一旦对话框得以解决或消除，下一个对话框便会发生。</span><span class="sxs-lookup"><span data-stu-id="03db5-140">Once a dialog is resolved or dismissed, the next one take its place.</span></span>

<span data-ttu-id="03db5-141"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">请参阅 (Figma 的示例) </a></span><span class="sxs-lookup"><span data-stu-id="03db5-141"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">See an example (Figma)</a></span></span>

### <a name="scrolling"></a><span data-ttu-id="03db5-142">上下</span><span class="sxs-lookup"><span data-stu-id="03db5-142">Scrolling</span></span>

<span data-ttu-id="03db5-143">在会议对话中的 "web 视图" 部分发生滚动。</span><span class="sxs-lookup"><span data-stu-id="03db5-143">Scrolling occurs in the webview portion of an in-meeting dialog.</span></span> <span data-ttu-id="03db5-144">请记住以下有关滚动的信息：</span><span class="sxs-lookup"><span data-stu-id="03db5-144">Remember the following about scrolling:</span></span>

* <span data-ttu-id="03db5-145">应仅能够垂直滚动。</span><span class="sxs-lookup"><span data-stu-id="03db5-145">You should only be able to scroll vertically.</span></span>
* <span data-ttu-id="03db5-146">您只能看到您已滚动的内容 (不在) 以上或之下的任何内容。</span><span class="sxs-lookup"><span data-stu-id="03db5-146">You can only see the content you've scrolled to (nothing above or below).</span></span>

:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-scroll.png" alt-text="显示在 "会议" 对话框中滚动 web 视图内容的方式的图示。" border="false":::

### <a name="buttons"></a><span data-ttu-id="03db5-148">按钮</span><span class="sxs-lookup"><span data-stu-id="03db5-148">Buttons</span></span>

<span data-ttu-id="03db5-149">"会议中" 对话框按钮是 web 视图的一部分 ([请参阅一些示例](#best-practices)) 。</span><span class="sxs-lookup"><span data-stu-id="03db5-149">In-meeting dialog buttons are part of the webview ([see some examples](#best-practices)).</span></span>

<span data-ttu-id="03db5-150">与类似组件不同，在用户选择按钮后将消除会议中的对话框。</span><span class="sxs-lookup"><span data-stu-id="03db5-150">Unlike similar components, in-meeting dialogs are dismissed once a user selects a button.</span></span>

## <a name="components"></a><span data-ttu-id="03db5-151">组件</span><span class="sxs-lookup"><span data-stu-id="03db5-151">Components</span></span>

<span data-ttu-id="03db5-152">会议中的对话框主要是基于以下 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI 组件（ (Figma) </a>）生成的，这些组件基于的是 <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">熟知的设计系统</a>。</span><span class="sxs-lookup"><span data-stu-id="03db5-152">In-meeting dialogs are built primarily with the following <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">UI components (Figma)</a>, which are based on the <a href="https://fluentsite.z22.web.core.windows.net/" target="_blank">Fluent Design System</a>.</span></span>

<span data-ttu-id="03db5-153">组件</span><span class="sxs-lookup"><span data-stu-id="03db5-153">Component</span></span> | <span data-ttu-id="03db5-154">准则</span><span class="sxs-lookup"><span data-stu-id="03db5-154">Guidelines</span></span> | <span data-ttu-id="03db5-155">示例</span><span class="sxs-lookup"><span data-stu-id="03db5-155">Example</span></span>
 - | - | -
<span data-ttu-id="03db5-156">按钮</span><span class="sxs-lookup"><span data-stu-id="03db5-156">Button</span></span> | <span data-ttu-id="03db5-157">主要和次要按钮可以是中型或小型</span><span class="sxs-lookup"><span data-stu-id="03db5-157">Primary and secondary buttons can be medium or small</span></span> | <span data-ttu-id="03db5-158">发送响应</span><span class="sxs-lookup"><span data-stu-id="03db5-158">Send a response</span></span>
<span data-ttu-id="03db5-159">Input</span><span class="sxs-lookup"><span data-stu-id="03db5-159">Input</span></span> | <span data-ttu-id="03db5-160">用于简短用户输入的字段。</span><span class="sxs-lookup"><span data-stu-id="03db5-160">Field for brief user input.</span></span> <span data-ttu-id="03db5-161">标签文本可以包含图标</span><span class="sxs-lookup"><span data-stu-id="03db5-161">Label text can include an icon</span></span>  | <span data-ttu-id="03db5-162">输入反馈</span><span class="sxs-lookup"><span data-stu-id="03db5-162">Enter feedback</span></span>
<span data-ttu-id="03db5-163">下拉列表</span><span class="sxs-lookup"><span data-stu-id="03db5-163">Dropdown</span></span> | <span data-ttu-id="03db5-164">从列表中选择一个或多个选项。</span><span class="sxs-lookup"><span data-stu-id="03db5-164">Select one or more options from a list.</span></span> <span data-ttu-id="03db5-165">可以包括搜索和多选功能</span><span class="sxs-lookup"><span data-stu-id="03db5-165">Can include search and multi-selection features</span></span> | <span data-ttu-id="03db5-166">选择语言</span><span class="sxs-lookup"><span data-stu-id="03db5-166">Choose a language</span></span>
<span data-ttu-id="03db5-167">选择控件</span><span class="sxs-lookup"><span data-stu-id="03db5-167">Selection controls</span></span> | <span data-ttu-id="03db5-168">将 checkbox 用于多个选项或单选按钮，然后切换选择单个选项。</span><span class="sxs-lookup"><span data-stu-id="03db5-168">Use checkboxes for multiple choices or radio buttons and toggles for single choices.</span></span> <span data-ttu-id="03db5-169">有关更详细的选择，请使用滑块</span><span class="sxs-lookup"><span data-stu-id="03db5-169">For more detailed selections, use a slider</span></span> | <span data-ttu-id="03db5-170">投票中的投票</span><span class="sxs-lookup"><span data-stu-id="03db5-170">Vote in a poll</span></span>
<span data-ttu-id="03db5-171">警报</span><span class="sxs-lookup"><span data-stu-id="03db5-171">Alerts</span></span> | <span data-ttu-id="03db5-172">无论是显示紧急邮件、错误状态还是警告，邮件都应短，并且不会中断用户的当前任务</span><span class="sxs-lookup"><span data-stu-id="03db5-172">Whether displaying an urgent message, error state, or warning, the message should be short and won't interrupt the user's current task</span></span> | <span data-ttu-id="03db5-173">提交响应时显示问题</span><span class="sxs-lookup"><span data-stu-id="03db5-173">Display issue when submitting a response</span></span>

## <a name="theming"></a><span data-ttu-id="03db5-174">主题</span><span class="sxs-lookup"><span data-stu-id="03db5-174">Theming</span></span>

### <a name="colors"></a><span data-ttu-id="03db5-175">颜色</span><span class="sxs-lookup"><span data-stu-id="03db5-175">Colors</span></span>

<span data-ttu-id="03db5-176">将 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">推荐的配色方案 (Figma) </a> 用于背景、foregrounds 和传达状态。</span><span class="sxs-lookup"><span data-stu-id="03db5-176">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended color scheme (Figma)</a> for backgrounds, foregrounds, and conveying states.</span></span>

### <a name="typography"></a><span data-ttu-id="03db5-177">版式</span><span class="sxs-lookup"><span data-stu-id="03db5-177">Typography</span></span>

<span data-ttu-id="03db5-178">对标题、正文文本和元数据文本使用 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">建议的字体大小和权重 (Figma) </a> 。</span><span class="sxs-lookup"><span data-stu-id="03db5-178">Use the <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">recommended font sizes and weights (Figma)</a> for titles, body text, and metadata text.</span></span>

## <a name="best-practices"></a><span data-ttu-id="03db5-179">最佳做法</span><span class="sxs-lookup"><span data-stu-id="03db5-179">Best practices</span></span>

<span data-ttu-id="03db5-180">虽然会议中的对话可以使呼叫更有效，但如果 obtrusive，也可以 derail 呼叫。</span><span class="sxs-lookup"><span data-stu-id="03db5-180">While in-meeting dialogs can make calls more effective, they also can derail calls if too obtrusive.</span></span> <span data-ttu-id="03db5-181">通常情况下，请尽量少使用对话框，并遵循这些最佳实践。</span><span class="sxs-lookup"><span data-stu-id="03db5-181">In general, use the dialogs sparingly and follow these best practices.</span></span>

### <a name="navigation"></a><span data-ttu-id="03db5-182">导航</span><span class="sxs-lookup"><span data-stu-id="03db5-182">Navigation</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-steps-do.png" alt-text="演示如何将会议中的对话框内容限制为单个屏幕，以便用户可以将注意力集中在会议上。" border="false":::

#### <a name="do-keep-it-contained"></a><span data-ttu-id="03db5-184">Do：将其包含</span><span class="sxs-lookup"><span data-stu-id="03db5-184">Do: Keep it contained</span></span>

<span data-ttu-id="03db5-185">将会议中的对话框内容限制为单个屏幕，以便用户可以将注意力集中在会议上。</span><span class="sxs-lookup"><span data-stu-id="03db5-185">Limit in-meeting dialog content to a single screen so users can focus on the meeting.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-steps-dont.png" alt-text="图示：会议对话框不应要求用户在内容中导航。" border="false":::

#### <a name="dont-include-multiple-steps"></a><span data-ttu-id="03db5-187">请勿：包含多个步骤</span><span class="sxs-lookup"><span data-stu-id="03db5-187">Don't: Include multiple steps</span></span>

<span data-ttu-id="03db5-188">会议中的对话框不应要求用户在内容中导航。</span><span class="sxs-lookup"><span data-stu-id="03db5-188">In-meeting dialogs shouldn't require users to navigate through content.</span></span>

   :::column-end:::
:::row-end:::

### <a name="interactions"></a><span data-ttu-id="03db5-189">相互作用</span><span class="sxs-lookup"><span data-stu-id="03db5-189">Interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-interactions-do.png" alt-text="图中显示为什么应删除不会帮助用户快速完成某些不必要的内容的原因。" border="false":::

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-interactions-dont.png" alt-text="另一种说明为何应删除不能帮助用户快速完成某些不必要的内容的说明。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-tab-do.png" alt-text="插图显示，如果需要复杂的交互，建议您改为在会议上使用一栏。" border="false":::

#### <a name="do-limit-number-of-interactions"></a><span data-ttu-id="03db5-193">操作：限制交互次数</span><span class="sxs-lookup"><span data-stu-id="03db5-193">Do: Limit number of interactions</span></span>

<span data-ttu-id="03db5-194">删除不会帮助用户快速完成某项不必要的内容。</span><span class="sxs-lookup"><span data-stu-id="03db5-194">Remove unnecessary content that doesn't help users accomplish something quickly.</span></span> <span data-ttu-id="03db5-195">如果需要复杂的交互，强烈建议您改为使用 "会议" 选项卡上的单个栏显示内容。</span><span class="sxs-lookup"><span data-stu-id="03db5-195">If you need complex interactions, we strongly recommend displaying your content using a single column on the in-meeting tab instead.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-tab-dont.png" alt-text="图中显示会议中的对话 distracts 中的交互过多。" border="false":::

#### <a name="dont-introduce-unnecessary-elements"></a><span data-ttu-id="03db5-197">请勿：引入不必要的元素</span><span class="sxs-lookup"><span data-stu-id="03db5-197">Don't: Introduce unnecessary elements</span></span>

<span data-ttu-id="03db5-198">您可以设计具有多个交互的单个会议内对话，但如果过多，可能会分散会议。</span><span class="sxs-lookup"><span data-stu-id="03db5-198">You may be able to design a single in-meeting dialog with multiple interactions, but too many can distract from the meeting.</span></span>

   :::column-end:::
:::row-end:::

### <a name="layout"></a><span data-ttu-id="03db5-199">布局</span><span class="sxs-lookup"><span data-stu-id="03db5-199">Layout</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-layout-do.png" alt-text="显示会议中对话框的理想布局的插图。" border="false":::

#### <a name="do-use-single-column-layouts"></a><span data-ttu-id="03db5-201">Do： Use 单列版式</span><span class="sxs-lookup"><span data-stu-id="03db5-201">Do: Use single-column layouts</span></span>

<span data-ttu-id="03db5-202">由于对话位于会议阶段的中心，因此任务完成应快速而简单，以避免用户不满。</span><span class="sxs-lookup"><span data-stu-id="03db5-202">Since the dialogs are at the center of the meeting stage, task completion should be fast and simple to avoid user frustration.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-layout-dont.png" alt-text="显示不建议的会议中对话框的布局的图示。" border="false":::

#### <a name="dont-clutter-the-space"></a><span data-ttu-id="03db5-204">不：打乱空间</span><span class="sxs-lookup"><span data-stu-id="03db5-204">Don't: Clutter the space</span></span>

<span data-ttu-id="03db5-205">密集或过于复杂的内容可能会分散注意力，尤其是在会议过程中。</span><span class="sxs-lookup"><span data-stu-id="03db5-205">Dense or overly structured content can be distracting and overwhelming, especially during a meeting.</span></span>

   :::column-end:::
:::row-end:::

### <a name="size"></a><span data-ttu-id="03db5-206">Size</span><span class="sxs-lookup"><span data-stu-id="03db5-206">Size</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-size-do.png" alt-text="图中显示会议对话框大小应始终是相同的。" border="false":::

#### <a name="do-keep-it-consistent"></a><span data-ttu-id="03db5-208">Do：使其保持一致</span><span class="sxs-lookup"><span data-stu-id="03db5-208">Do: Keep it consistent</span></span>

<span data-ttu-id="03db5-209">这一点很重要，因为会议中的对话框始终显示在相同的位置。</span><span class="sxs-lookup"><span data-stu-id="03db5-209">This is important because in-meeting dialogs always display in the same location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-size-dont.png" alt-text="演示如何使用不同的对话框大小。" border="false":::

#### <a name="dont-always-fit-to-the-content"></a><span data-ttu-id="03db5-211">不：始终填充内容</span><span class="sxs-lookup"><span data-stu-id="03db5-211">Don't: Always fit to the content</span></span>

<span data-ttu-id="03db5-212">您可能试图避免水平滚动，但同一应用程序中的多个会议对话大小的体验不一致。</span><span class="sxs-lookup"><span data-stu-id="03db5-212">You may be trying to avoid horizontal scrolling, but multiple in-meeting dialog sizes within the same app is an inconsistent experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="controls"></a><span data-ttu-id="03db5-213">控件</span><span class="sxs-lookup"><span data-stu-id="03db5-213">Controls</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-controls-do.png" alt-text="显示 "在会议中放置按钮的位置" 对话框的图示。" border="false":::

#### <a name="do-right-align-the-primary-action"></a><span data-ttu-id="03db5-215">操作：将主要操作右对齐</span><span class="sxs-lookup"><span data-stu-id="03db5-215">Do: Right align the primary action</span></span>

<span data-ttu-id="03db5-216">建议将最具视觉的繁重操作定位到最右侧的位置。</span><span class="sxs-lookup"><span data-stu-id="03db5-216">We recommend positioning the most visually heavy action to the right-most location.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/calls-and-meetings/in-meeting-dialog-controls-dont.png" alt-text="显示 "在会议中不放置按钮的位置" 对话框的图示。" border="false":::

#### <a name="dont-left-or-center-align-actions"></a><span data-ttu-id="03db5-218">不：左对齐或居中对齐操作</span><span class="sxs-lookup"><span data-stu-id="03db5-218">Don't: Left or center align actions</span></span>

<span data-ttu-id="03db5-219">这与对话框中的控件放置的标准团队模式不同，可能与顶部的对话框冲突。</span><span class="sxs-lookup"><span data-stu-id="03db5-219">This deviates from the standard Teams pattern for control placement in a dialog and may conflict with a dialog behind the top one.</span></span>

   :::column-end:::
:::row-end:::

## <a name="accessibility"></a><span data-ttu-id="03db5-220">辅助功能</span><span class="sxs-lookup"><span data-stu-id="03db5-220">Accessibility</span></span>

<span data-ttu-id="03db5-221">有关辅助功能的信息，请参阅 <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>。</span><span class="sxs-lookup"><span data-stu-id="03db5-221">For information on accessibility, see <a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Figma</a>.</span></span>

## <a name="resources"></a><span data-ttu-id="03db5-222">资源</span><span class="sxs-lookup"><span data-stu-id="03db5-222">Resources</span></span>

* <span data-ttu-id="03db5-223"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft 团队会议扩展 Figma 文件</a></span><span class="sxs-lookup"><span data-stu-id="03db5-223"><a href="https://www.figma.com/community/file/888593778835180533" target="_blank">Microsoft Teams meeting extensions Figma file</a></span></span>

## <a name="validate-your-design"></a><span data-ttu-id="03db5-224">验证设计</span><span class="sxs-lookup"><span data-stu-id="03db5-224">Validate your design</span></span>

<span data-ttu-id="03db5-225">如果计划将应用程序发布到 AppSource，则应了解通常会在提交期间导致应用程序失败的设计问题。</span><span class="sxs-lookup"><span data-stu-id="03db5-225">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="03db5-226">检查设计验证准则</span><span class="sxs-lookup"><span data-stu-id="03db5-226">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines)
