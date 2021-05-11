---
title: 设计任务模块
author: heath-hamilton
description: 了解如何为应用设计任务Teams并获取 Microsoft Teams UI 工具包。
localization_priority: Normal
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 347ce42c41706f698e2f8897a0518aae0850a275
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101728"
---
# <a name="designing-task-modules-for-your-microsoft-teams-app"></a><span data-ttu-id="97d1e-103">为应用程序设计Microsoft Teams模块</span><span class="sxs-lookup"><span data-stu-id="97d1e-103">Designing task modules for your Microsoft Teams app</span></span>

<span data-ttu-id="97d1e-104">可以使用任务模块在 Teams应用中创建模式弹出体验。</span><span class="sxs-lookup"><span data-stu-id="97d1e-104">You can create modal popup experiences in your Teams app with task modules.</span></span> <span data-ttu-id="97d1e-105">使用此功能可显示富媒体和信息或完成复杂的任务。</span><span class="sxs-lookup"><span data-stu-id="97d1e-105">Use this capability to display rich media and information or complete a complex task.</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-overview.png" alt-text="示例显示任务模块。" border="false":::

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="97d1e-107">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="97d1e-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="97d1e-108">可以在自定义 UI 工具包中查找更全面的任务模块设计指南，包括可根据需要获取和修改Microsoft Teams元素。</span><span class="sxs-lookup"><span data-stu-id="97d1e-108">You can find more comprehensive task module design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="97d1e-109">获取 Microsoft Teams UI Kit （用户）</span><span class="sxs-lookup"><span data-stu-id="97d1e-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="open-a-task-module"></a><span data-ttu-id="97d1e-110">打开任务模块</span><span class="sxs-lookup"><span data-stu-id="97d1e-110">Open a task module</span></span>

<span data-ttu-id="97d1e-111">任务模块几乎可以从你的应用中的任何位置启动。</span><span class="sxs-lookup"><span data-stu-id="97d1e-111">Task modules can be launched from almost anywhere in your app.</span></span>

* <span data-ttu-id="97d1e-112">**Tab：** 可以从选项卡内的任何链接启动任务模块。在希望用户专注于交互的方案中使用。</span><span class="sxs-lookup"><span data-stu-id="97d1e-112">**Tab**: A task module can be launched from any link within a tab. Use in scenarios where you want the user to focus on an interaction.</span></span>
* <span data-ttu-id="97d1e-113">**自动** 程序：可以从自动程序消息内的链接启动任务模块。</span><span class="sxs-lookup"><span data-stu-id="97d1e-113">**Bot**: A task module can be launched from a link inside a bot message.</span></span>
* <span data-ttu-id="97d1e-114">**自适应卡片**：任务模块可以从随消息传递扩展 (发送的自适应卡片启动，也可在用户选择按钮) 自动程序启动。</span><span class="sxs-lookup"><span data-stu-id="97d1e-114">**Adaptive Card**: A task module can be launched from an Adaptive Card (sent with a messaging extension or by a bot) when a user selects a button.</span></span>
* <span data-ttu-id="97d1e-115">**邮件扩展 (操作命令) ：** 邮件扩展允许您对邮件内容执行特定操作。</span><span class="sxs-lookup"><span data-stu-id="97d1e-115">**Messaging extension (action commands)**: Messaging extensions allow you to take a particular action on message content.</span></span> <span data-ttu-id="97d1e-116">选择操作将打开任务模块。</span><span class="sxs-lookup"><span data-stu-id="97d1e-116">Selecting an action opens a task module.</span></span>
* <span data-ttu-id="97d1e-117">**邮件扩展 (撰写**) ：在撰写框中，可以设计邮件扩展以打开任务模块，而不是典型的飞出框。</span><span class="sxs-lookup"><span data-stu-id="97d1e-117">**Messaging extension (compose box context)**: In the compose box, you can design a messaging extension to open a task module instead of the typical flyout.</span></span> <span data-ttu-id="97d1e-118">保留用于复杂交互的任务模块，例如完成表单。</span><span class="sxs-lookup"><span data-stu-id="97d1e-118">Reserve task modules for complex interactions, such as completing a form.</span></span>

## <a name="anatomy"></a><span data-ttu-id="97d1e-119">解剖</span><span class="sxs-lookup"><span data-stu-id="97d1e-119">Anatomy</span></span>

:::image type="content" source="../../assets/images/task-module/task-module-anatomy.png" alt-text="显示任务模块的 UI 分析的图示。" border="false":::

<span data-ttu-id="97d1e-121">任务模块非常灵活。</span><span class="sxs-lookup"><span data-stu-id="97d1e-121">Task modules are very flexible surfaces.</span></span> <span data-ttu-id="97d1e-122">它们可以使用 iframe 生成，并拉取其他 UI 模板，以托管合作伙伴构建的体验。</span><span class="sxs-lookup"><span data-stu-id="97d1e-122">They can be built with iframes, pulling in other UI templates, to host partner-built experiences.</span></span> <span data-ttu-id="97d1e-123">这是最完善体验的首选。</span><span class="sxs-lookup"><span data-stu-id="97d1e-123">This is preferred for the most polished experience.</span></span>

<span data-ttu-id="97d1e-124">它们还可使用自适应卡片框架生成[](../../task-modules-and-cards/cards/design-effective-cards.md)，该框架可以更简单、更快速地执行窗体或 (应用场景) 。</span><span class="sxs-lookup"><span data-stu-id="97d1e-124">They can also be built with the [Adaptive Card](../../task-modules-and-cards/cards/design-effective-cards.md) framework, which can be a simpler and faster way to execute common scenarios (such as forms).</span></span>

|<span data-ttu-id="97d1e-125">计数器</span><span class="sxs-lookup"><span data-stu-id="97d1e-125">Counter</span></span>|<span data-ttu-id="97d1e-126">说明</span><span class="sxs-lookup"><span data-stu-id="97d1e-126">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="97d1e-127">1</span><span class="sxs-lookup"><span data-stu-id="97d1e-127">1</span></span>|<span data-ttu-id="97d1e-128">**应用程序图标**</span><span class="sxs-lookup"><span data-stu-id="97d1e-128">**App icon**</span></span>|
|<span data-ttu-id="97d1e-129">2</span><span class="sxs-lookup"><span data-stu-id="97d1e-129">2</span></span>|<span data-ttu-id="97d1e-130">**应用名称**：应用的完整名称。</span><span class="sxs-lookup"><span data-stu-id="97d1e-130">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="97d1e-131">3</span><span class="sxs-lookup"><span data-stu-id="97d1e-131">3</span></span>|<span data-ttu-id="97d1e-132">**标头**：使标题简洁明了。</span><span class="sxs-lookup"><span data-stu-id="97d1e-132">**Header**: Make headers clear and concise.</span></span> <span data-ttu-id="97d1e-133">描述希望用户完成的任务。</span><span class="sxs-lookup"><span data-stu-id="97d1e-133">Describe the task you want users to complete.</span></span>
|<span data-ttu-id="97d1e-134">4 </span><span class="sxs-lookup"><span data-stu-id="97d1e-134">4</span></span>|<span data-ttu-id="97d1e-135">**关闭按钮**：允许用户查找要插入的应用内容。</span><span class="sxs-lookup"><span data-stu-id="97d1e-135">**Close button**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="97d1e-136">5 </span><span class="sxs-lookup"><span data-stu-id="97d1e-136">5</span></span>|<span data-ttu-id="97d1e-137">**iframe：** 托管应用内容的响应空间。</span><span class="sxs-lookup"><span data-stu-id="97d1e-137">**iframe**: Responsive space that hosts your app content.</span></span>|
|<span data-ttu-id="97d1e-138">6 </span><span class="sxs-lookup"><span data-stu-id="97d1e-138">6</span></span>|<span data-ttu-id="97d1e-139">**操作 (可选) ：** 与应用内容相关的按钮。</span><span class="sxs-lookup"><span data-stu-id="97d1e-139">**Actions (optional)**: Buttons related to your app content.</span></span>|

## <a name="designing-with-ui-templates"></a><span data-ttu-id="97d1e-140">使用 UI 模板进行设计</span><span class="sxs-lookup"><span data-stu-id="97d1e-140">Designing with UI templates</span></span>

<span data-ttu-id="97d1e-141">请考虑对任务模块中的常见布局使用模板。</span><span class="sxs-lookup"><span data-stu-id="97d1e-141">Consider using templates for common layouts inside your task modules.</span></span> <span data-ttu-id="97d1e-142">每个组件都由较小的组件组成，以创建一个简洁、响应迅速的设计，该设计可以使用开箱即用或针对你的方案进行自定义，或者与品牌外观一起自定义。</span><span class="sxs-lookup"><span data-stu-id="97d1e-142">Each one is made up of smaller components to create an elegant, responsive design that can be used out of the box or customized for your scenario or with your brand look and feel.</span></span>

* <span data-ttu-id="97d1e-143">[列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目采取操作。</span><span class="sxs-lookup"><span data-stu-id="97d1e-143">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="97d1e-144">[表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单用于以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="97d1e-144">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="97d1e-145">[空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="97d1e-145">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>

## <a name="examples"></a><span data-ttu-id="97d1e-146">示例</span><span class="sxs-lookup"><span data-stu-id="97d1e-146">Examples</span></span>

### <a name="list"></a><span data-ttu-id="97d1e-147">列表</span><span class="sxs-lookup"><span data-stu-id="97d1e-147">List</span></span>

<span data-ttu-id="97d1e-148">列表在任务模块中运行得非常好，因为它们易于扫描。</span><span class="sxs-lookup"><span data-stu-id="97d1e-148">Lists work nicely in a task module because they’re easy to scan.</span></span>

:::image type="content" source="../../assets/images/task-module/list.png" alt-text="任务模块中的示例列表。" border="false":::

### <a name="form"></a><span data-ttu-id="97d1e-150">表单</span><span class="sxs-lookup"><span data-stu-id="97d1e-150">Form</span></span>

<span data-ttu-id="97d1e-151">任务模块是显示具有顺序用户输入和内联验证的表单的一个很好的位置。</span><span class="sxs-lookup"><span data-stu-id="97d1e-151">Task modules are a great place to surface forms with sequential user inputs and inline validation.</span></span> <span data-ttu-id="97d1e-152">可以利用自适应卡片作为嵌入表单元素的一种方式。</span><span class="sxs-lookup"><span data-stu-id="97d1e-152">You can leverage Adaptive Cards as a way to embed form elements.</span></span>

:::image type="content" source="../../assets/images/task-module/form.png" alt-text="任务模块中的示例窗体。" border="false":::

### <a name="sign-in"></a><span data-ttu-id="97d1e-154">登录</span><span class="sxs-lookup"><span data-stu-id="97d1e-154">Sign in</span></span>

<span data-ttu-id="97d1e-155">创建具有一系列任务模块的集中登录或注册流，使用户能够在顺序步骤中轻松移动。</span><span class="sxs-lookup"><span data-stu-id="97d1e-155">Create a focused sign in or sign-up flow with a series of task modules, letting users move easily through sequential steps.</span></span>

:::image type="content" source="../../assets/images/task-module/sign-in.png" alt-text="任务模块中的登录体验示例。" border="false":::

### <a name="media"></a><span data-ttu-id="97d1e-157">媒体</span><span class="sxs-lookup"><span data-stu-id="97d1e-157">Media</span></span>

<span data-ttu-id="97d1e-158">在任务模块中嵌入媒体内容，实现集中的观看体验。</span><span class="sxs-lookup"><span data-stu-id="97d1e-158">Embed media content in a task module for a focused viewing experience.</span></span>

:::image type="content" source="../../assets/images/task-module/media.png" alt-text="任务模块中的媒体内容示例。" border="false":::

### <a name="empty-state"></a><span data-ttu-id="97d1e-160">空状态</span><span class="sxs-lookup"><span data-stu-id="97d1e-160">Empty state</span></span>

<span data-ttu-id="97d1e-161">用于欢迎、错误和成功消息。</span><span class="sxs-lookup"><span data-stu-id="97d1e-161">Use for welcome, error, and success messages.</span></span>

:::image type="content" source="../../assets/images/task-module/empty-state.png" alt-text="任务模块中的空状态示例。" border="false":::

### <a name="image-gallery"></a><span data-ttu-id="97d1e-163">图像库</span><span class="sxs-lookup"><span data-stu-id="97d1e-163">Image gallery</span></span>

<span data-ttu-id="97d1e-164">在 iframe 中嵌入库的盘点。</span><span class="sxs-lookup"><span data-stu-id="97d1e-164">Embed a gallery carousel in an iframe.</span></span>

:::image type="content" source="../../assets/images/task-module/image-gallery.png" alt-text="任务模块中的示例图像库。" border="false":::

### <a name="poll"></a><span data-ttu-id="97d1e-166">投票</span><span class="sxs-lookup"><span data-stu-id="97d1e-166">Poll</span></span>

<span data-ttu-id="97d1e-167">此示例显示从自适应卡片启动的投票结果。</span><span class="sxs-lookup"><span data-stu-id="97d1e-167">This example shows poll results launched from an Adaptive Card.</span></span> <span data-ttu-id="97d1e-168">轮询也可以放置在任务模块内。</span><span class="sxs-lookup"><span data-stu-id="97d1e-168">The poll can be placed inside a task module, too.</span></span>

:::image type="content" source="../../assets/images/task-module/poll.png" alt-text="任务模块中的轮询示例。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="97d1e-170">最佳做法</span><span class="sxs-lookup"><span data-stu-id="97d1e-170">Best practices</span></span>

<span data-ttu-id="97d1e-171">使用这些建议创建高质量的应用体验。</span><span class="sxs-lookup"><span data-stu-id="97d1e-171">Use these recommendations to create a quality app experience.</span></span>

### <a name="usability"></a><span data-ttu-id="97d1e-172">可用性</span><span class="sxs-lookup"><span data-stu-id="97d1e-172">Usability</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-do.png" alt-text="显示任务模块最佳实践的示例 (一个任务模块一) 。" border="false":::

#### <a name="do-use-one-task-module-at-a-time"></a><span data-ttu-id="97d1e-174">应做：一次使用一个任务模块</span><span class="sxs-lookup"><span data-stu-id="97d1e-174">Do: Use one task module at a time</span></span>

<span data-ttu-id="97d1e-175">目标是使用户专注于完成一项任务！</span><span class="sxs-lookup"><span data-stu-id="97d1e-175">The goal is to focus the user on completing a task after all!</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/usability-dont.png" alt-text="示例显示任务模块最佳实践 (在任务模块模型顶部弹出) 。" border="false":::

#### <a name="dont-pop-a-dialog-on-top-of-a-task-module"></a><span data-ttu-id="97d1e-177">请勿：在任务模块顶部弹出对话框</span><span class="sxs-lookup"><span data-stu-id="97d1e-177">Don't: Pop a dialog on top of a task module</span></span>

<span data-ttu-id="97d1e-178">这将创建一种没有焦点的、令人困惑的用户体验。</span><span class="sxs-lookup"><span data-stu-id="97d1e-178">This creates an unfocused, confusing user experience.</span></span>

   :::column-end:::
:::row-end:::

### <a name="responsive"></a><span data-ttu-id="97d1e-179">快速响应</span><span class="sxs-lookup"><span data-stu-id="97d1e-179">Responsive</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-do.png" alt-text="显示任务模块最佳实践的示例 (确保内容响应迅速) 。" border="false":::

#### <a name="do-make-sure-the-content-is-responsive"></a><span data-ttu-id="97d1e-181">应做：确保内容响应迅速</span><span class="sxs-lookup"><span data-stu-id="97d1e-181">Do: Make sure the content is responsive</span></span>

<span data-ttu-id="97d1e-182">虽然任务模块中托管的自适应卡片在移动设备上可正常呈现，但如果选择使用 iframe 托管应用内容，请确保 UI 响应迅速且跨设备运行良好。</span><span class="sxs-lookup"><span data-stu-id="97d1e-182">While Adaptive Cards hosted in a task module render well on mobile devices, if you choose to use an iframe to host app content, make sure the UI is responsive and works well across devices.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/responsive-dont.png" alt-text="显示任务模块最佳实践的示例 (不使用水平滚动条) 。" border="false":::

#### <a name="dont-use-horizontal-scroll-bars"></a><span data-ttu-id="97d1e-184">禁止：使用水平滚动条</span><span class="sxs-lookup"><span data-stu-id="97d1e-184">Don't: Use horizontal scroll bars</span></span>

<span data-ttu-id="97d1e-185">最佳做法是使内容保持集中，不要过长。</span><span class="sxs-lookup"><span data-stu-id="97d1e-185">It's a best practice to keep content focused and not too lengthy.</span></span> <span data-ttu-id="97d1e-186">如果需要滚动，请垂直滚动，而不是水平滚动。</span><span class="sxs-lookup"><span data-stu-id="97d1e-186">If a scroll is necessary, scroll vertically and not horizontally.</span></span>

   :::column-end:::
:::row-end:::

### <a name="simplicity"></a><span data-ttu-id="97d1e-187">简单性</span><span class="sxs-lookup"><span data-stu-id="97d1e-187">Simplicity</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-do.png" alt-text="显示任务模块最佳实践的示例 (使任务模块) 。" border="false":::

#### <a name="do-keep-it-short"></a><span data-ttu-id="97d1e-189">应做：保持简短</span><span class="sxs-lookup"><span data-stu-id="97d1e-189">Do: Keep it short</span></span>

<span data-ttu-id="97d1e-190">你可以轻松创建多步骤向导，但这并不意味着你应该！</span><span class="sxs-lookup"><span data-stu-id="97d1e-190">You can easily create a multi-step wizard, but that doesn't necessarily mean you should!</span></span> <span data-ttu-id="97d1e-191">多屏幕任务模块可能会出现问题，因为传入的消息会分散注意力并吸引用户退出。</span><span class="sxs-lookup"><span data-stu-id="97d1e-191">A multi-screen task module can be problematic because incoming messages are distracting and tempt users to exit.</span></span> <span data-ttu-id="97d1e-192">如果确实涉及你的任务，请弹出到完整网页，而不是任务模块。</span><span class="sxs-lookup"><span data-stu-id="97d1e-192">If your task is really involved, pop out to a full webpage instead of a task module.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/simplicity-dont.png" alt-text="显示任务模块最佳实践的示例 (操作没有长交互) 。" border="false":::

#### <a name="dont-have-long-interactions"></a><span data-ttu-id="97d1e-194">请勿：进行长交互</span><span class="sxs-lookup"><span data-stu-id="97d1e-194">Don't: Have long interactions</span></span>

<span data-ttu-id="97d1e-195">尽量使交互保持简短并达到目标。</span><span class="sxs-lookup"><span data-stu-id="97d1e-195">Try to keep your interactions short and to the point.</span></span>

   :::column-end:::
:::row-end:::

### <a name="error-messages"></a><span data-ttu-id="97d1e-196">错误消息</span><span class="sxs-lookup"><span data-stu-id="97d1e-196">Error messages</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-do.png" alt-text="显示任务模块最佳实践的示例 (内嵌错误消息) 。" border="false":::

#### <a name="do-use-inline-error-messages"></a><span data-ttu-id="97d1e-198">Do：使用内联错误消息</span><span class="sxs-lookup"><span data-stu-id="97d1e-198">Do: Use inline error messages</span></span>

<span data-ttu-id="97d1e-199">有关内嵌错误处理的准则，请参阅表单 UI 模板。</span><span class="sxs-lookup"><span data-stu-id="97d1e-199">See the forms UI template for guidelines on inline error handling.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/task-module/error-messages-dont.png" alt-text="显示任务模块最佳实践的示例 (将错误消息放入对话框) 。" border="false":::

#### <a name="dont-put-error-messages-in-dialogs"></a><span data-ttu-id="97d1e-201">请勿：在对话框中放入错误消息</span><span class="sxs-lookup"><span data-stu-id="97d1e-201">Don't: Put error messages in dialogs</span></span>

<span data-ttu-id="97d1e-202">不要在任务模块顶部的对话框中弹出错误消息。</span><span class="sxs-lookup"><span data-stu-id="97d1e-202">Don't pop an error message in a dialog on top of a task modules.</span></span> <span data-ttu-id="97d1e-203">它创建令人困惑的用户体验。</span><span class="sxs-lookup"><span data-stu-id="97d1e-203">It creates a confusing user experience.</span></span>

   :::column-end:::
:::row-end:::
