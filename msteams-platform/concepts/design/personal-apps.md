---
title: 正在设计你的个人应用
description: 了解如何设计工作组个人应用程序并获取 Microsoft 团队 UI 工具包。
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 971071be9f345815f5461646d7970efdf05fd5c4
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604973"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="38fcf-103">为 Microsoft 团队设计个人应用程序</span><span class="sxs-lookup"><span data-stu-id="38fcf-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="38fcf-104">个人应用程序可以是 bot、专用工作区或两者。</span><span class="sxs-lookup"><span data-stu-id="38fcf-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="38fcf-105">有时它的工作方式类似于创建或查看内容的位置，而另一些时候它为用户提供了在将应用程序配置为多个频道中的选项卡时的所有内容的鸟瞰视图。</span><span class="sxs-lookup"><span data-stu-id="38fcf-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that’s theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="38fcf-106">若要指导您的应用程序设计，以下信息介绍并说明了用户如何添加、使用和管理团队中的个人应用程序。</span><span class="sxs-lookup"><span data-stu-id="38fcf-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="38fcf-107">Microsoft 团队 UI 工具包</span><span class="sxs-lookup"><span data-stu-id="38fcf-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="38fcf-108">您可以在 Microsoft 团队 UI 工具包中找到全面的个人应用程序设计指南，包括可在需要时获取和修改的元素。</span><span class="sxs-lookup"><span data-stu-id="38fcf-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="38fcf-109">UI 工具包还包含此处未介绍的辅助功能和响应大小等基本主题。</span><span class="sxs-lookup"><span data-stu-id="38fcf-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="38fcf-110"> (Figma) 获取 Microsoft 团队 UI 工具包 </span><span class="sxs-lookup"><span data-stu-id="38fcf-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="38fcf-111">添加个人应用程序</span><span class="sxs-lookup"><span data-stu-id="38fcf-111">Add a personal app</span></span>

<span data-ttu-id="38fcf-112">您可以从团队存储 (AppSource ") " 或 "应用程序" 浮出控件中添加个人应用程序，方法是在团队左侧选择 " **更多** " 图标 (如以下示例) 所示。</span><span class="sxs-lookup"><span data-stu-id="38fcf-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="示例演示如何从应用浮出控件添加个人应用程序。" border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="38fcf-114">使用个人应用 (专用工作区) </span><span class="sxs-lookup"><span data-stu-id="38fcf-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="38fcf-115">使用专用工作区，您可以查看在中心位置有意义的应用程序内容，而无需离开团队。</span><span class="sxs-lookup"><span data-stu-id="38fcf-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="38fcf-116"> (实现注意：专用工作区基于 " [*个人" 选项卡*](../../build-your-first-app/build-personal-tab.md) 功能。 ) </span><span class="sxs-lookup"><span data-stu-id="38fcf-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="38fcf-117">剖析：个人应用程序 (专用工作区) </span><span class="sxs-lookup"><span data-stu-id="38fcf-117">Anatomy: Personal app (private workspace)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="示例显示了个人选项卡的组件解析。" border="false":::

|<span data-ttu-id="38fcf-119">计数器</span><span class="sxs-lookup"><span data-stu-id="38fcf-119">Counter</span></span>|<span data-ttu-id="38fcf-120">描述</span><span class="sxs-lookup"><span data-stu-id="38fcf-120">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="38fcf-121">A</span><span class="sxs-lookup"><span data-stu-id="38fcf-121">A</span></span>|<span data-ttu-id="38fcf-122">**应用程序归属**：您的应用程序徽标和名称。</span><span class="sxs-lookup"><span data-stu-id="38fcf-122">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="38fcf-123">B</span><span class="sxs-lookup"><span data-stu-id="38fcf-123">B</span></span>|<span data-ttu-id="38fcf-124">**选项卡**：提供你的个人应用的导航。</span><span class="sxs-lookup"><span data-stu-id="38fcf-124">**Tabs**: Provides navigation for your personal app.</span></span> <span data-ttu-id="38fcf-125">例如，包括 " **关于** " 或 " **帮助** " 选项卡。</span><span class="sxs-lookup"><span data-stu-id="38fcf-125">For example, include an **About** or **Help** tab.</span></span>|
|<span data-ttu-id="38fcf-126">C</span><span class="sxs-lookup"><span data-stu-id="38fcf-126">C</span></span>|<span data-ttu-id="38fcf-127">**弹出视图**：将您的应用程序内容从父窗口推送到独立子窗口。</span><span class="sxs-lookup"><span data-stu-id="38fcf-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="38fcf-128">D</span><span class="sxs-lookup"><span data-stu-id="38fcf-128">D</span></span>|<span data-ttu-id="38fcf-129">"**更多" 菜单**：包含其他应用程序信息和选项。</span><span class="sxs-lookup"><span data-stu-id="38fcf-129">**More menu**: Includes additional app information and options.</span></span> <span data-ttu-id="38fcf-130"> (您也可以将 **设置设置** 为选项卡。 ) </span><span class="sxs-lookup"><span data-stu-id="38fcf-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="示例显示了个人选项卡的结构剖析。" border="false":::

|<span data-ttu-id="38fcf-132">计数器</span><span class="sxs-lookup"><span data-stu-id="38fcf-132">Counter</span></span>|<span data-ttu-id="38fcf-133">描述</span><span class="sxs-lookup"><span data-stu-id="38fcf-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="38fcf-134">A</span><span class="sxs-lookup"><span data-stu-id="38fcf-134">A</span></span>|<span data-ttu-id="38fcf-135">**选项卡**：提供你的个人应用的导航。</span><span class="sxs-lookup"><span data-stu-id="38fcf-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="38fcf-136">1 </span><span class="sxs-lookup"><span data-stu-id="38fcf-136">1</span></span>|<span data-ttu-id="38fcf-137">**iframe**：显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="38fcf-137">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="38fcf-138">使用 UI 模板进行设计</span><span class="sxs-lookup"><span data-stu-id="38fcf-138">Designing with UI templates</span></span>

<span data-ttu-id="38fcf-139">使用以下团队 UI 模板之一来帮助设计您的个人选项卡：</span><span class="sxs-lookup"><span data-stu-id="38fcf-139">Use one of the following Teams UI templates to help design your personal tab:</span></span>

* <span data-ttu-id="38fcf-140">[列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可浏览的格式显示相关项目，并允许用户对整个列表或单个项目执行操作。</span><span class="sxs-lookup"><span data-stu-id="38fcf-140">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="38fcf-141">[任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为 "看板母板" 或 "泳道"）是用于跟踪工作项或票证状态的卡片的集合。</span><span class="sxs-lookup"><span data-stu-id="38fcf-141">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="38fcf-142">[仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是一个包含多个卡片的画布，可提供数据或内容的概述。</span><span class="sxs-lookup"><span data-stu-id="38fcf-142">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="38fcf-143">[表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="38fcf-143">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="38fcf-144">[空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="38fcf-144">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="38fcf-145">[左侧](../../concepts/design/design-teams-app-ui-templates.md#left-nav)导航：如果您的选项卡需要一些导航，则左侧导航模板可有所帮助。</span><span class="sxs-lookup"><span data-stu-id="38fcf-145">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="38fcf-146">通常情况下，应保持最小的选项卡导航。</span><span class="sxs-lookup"><span data-stu-id="38fcf-146">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="38fcf-147">使用个人应用 (bot) </span><span class="sxs-lookup"><span data-stu-id="38fcf-147">Use a personal app (bot)</span></span>

<span data-ttu-id="38fcf-148">个人应用可以包括用于一对一对话和私人通知 (的 bot，例如，当同事将注释发布到美工板上时) 。</span><span class="sxs-lookup"><span data-stu-id="38fcf-148">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="38fcf-149">可以在指定的选项卡中使用 bot。</span><span class="sxs-lookup"><span data-stu-id="38fcf-149">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="38fcf-150">剖析：个人应用程序 (bot) </span><span class="sxs-lookup"><span data-stu-id="38fcf-150">Anatomy: Personal app (bot)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="示例显示个人 bot 组件解析。" border="false":::

|<span data-ttu-id="38fcf-152">计数器</span><span class="sxs-lookup"><span data-stu-id="38fcf-152">Counter</span></span>|<span data-ttu-id="38fcf-153">描述</span><span class="sxs-lookup"><span data-stu-id="38fcf-153">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="38fcf-154">A</span><span class="sxs-lookup"><span data-stu-id="38fcf-154">A</span></span>|<span data-ttu-id="38fcf-155">**机器人选项卡**：例如，包含一个 " **聊天** " 选项卡来访问机器人对话和通知。</span><span class="sxs-lookup"><span data-stu-id="38fcf-155">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="38fcf-156">B</span><span class="sxs-lookup"><span data-stu-id="38fcf-156">B</span></span>|<span data-ttu-id="38fcf-157">**Bot 邮件**： bot 通常以卡片形式发送邮件和通知 (例如，自适应卡片) 。</span><span class="sxs-lookup"><span data-stu-id="38fcf-157">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="38fcf-158">C</span><span class="sxs-lookup"><span data-stu-id="38fcf-158">C</span></span>|<span data-ttu-id="38fcf-159">**"撰写" 框**：用于将邮件发送到 bot 的输入字段。</span><span class="sxs-lookup"><span data-stu-id="38fcf-159">**Compose box**: Input field for sending messages to the bot.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="38fcf-160">最佳做法</span><span class="sxs-lookup"><span data-stu-id="38fcf-160">Best practices</span></span>

### <a name="tab-priority"></a><span data-ttu-id="38fcf-161">选项卡优先级</span><span class="sxs-lookup"><span data-stu-id="38fcf-161">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="38fcf-162">操作：在第一个选项卡中显示最相关的内容</span><span class="sxs-lookup"><span data-stu-id="38fcf-162">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="38fcf-163">通过快速响应调整大小，右侧的选项卡可能会被截断或无法查看。</span><span class="sxs-lookup"><span data-stu-id="38fcf-163">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="38fcf-165">不：领导辅助内容或元数据</span><span class="sxs-lookup"><span data-stu-id="38fcf-165">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="38fcf-166">与标准 web 应用一样，选项卡导航按照有助于了解应用程序主要功能的顺序进行。</span><span class="sxs-lookup"><span data-stu-id="38fcf-166">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="38fcf-168">选项卡层次结构</span><span class="sxs-lookup"><span data-stu-id="38fcf-168">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="38fcf-169">操作：选项卡应具有相同的层次结构，并表示关键应用程序页面</span><span class="sxs-lookup"><span data-stu-id="38fcf-169">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="38fcf-170">你的选项卡应对你的应用程序的主要功能和内容进行分类。</span><span class="sxs-lookup"><span data-stu-id="38fcf-170">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="38fcf-171">使用快速响应大小，右侧的内容可能会被截断或无法查看。</span><span class="sxs-lookup"><span data-stu-id="38fcf-171">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="38fcf-173">不：包含不同级别的层次结构</span><span class="sxs-lookup"><span data-stu-id="38fcf-173">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="38fcf-174">您的内容应以有助于用户理解的逻辑顺序进行。</span><span class="sxs-lookup"><span data-stu-id="38fcf-174">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="38fcf-175">如果您有两个密切相关的选项卡，请考虑将它们组合成一个选项卡。</span><span class="sxs-lookup"><span data-stu-id="38fcf-175">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="38fcf-177">首次运行体验</span><span class="sxs-lookup"><span data-stu-id="38fcf-177">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="38fcf-178">操作：包括首次运行体验</span><span class="sxs-lookup"><span data-stu-id="38fcf-178">Do: Include a first-run experience</span></span>

<span data-ttu-id="38fcf-179">首次使用个人应用时，应该至少有一个欢迎屏幕。</span><span class="sxs-lookup"><span data-stu-id="38fcf-179">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="38fcf-180">对于 bot，说明你的 bot 可以执行的操作并提供快速操作，如登录按钮。</span><span class="sxs-lookup"><span data-stu-id="38fcf-180">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="38fcf-183">不：从空白屏幕开始</span><span class="sxs-lookup"><span data-stu-id="38fcf-183">Don't: Start with a blank screen</span></span>

<span data-ttu-id="38fcf-184">如果在首次运行应用程序时没有显示任何内容，则可能会对用户感到困惑。</span><span class="sxs-lookup"><span data-stu-id="38fcf-184">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

### <a name="personalized-content"></a><span data-ttu-id="38fcf-186">个性化内容</span><span class="sxs-lookup"><span data-stu-id="38fcf-186">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="38fcf-187">操作：与用户相关的聚合应用内容</span><span class="sxs-lookup"><span data-stu-id="38fcf-187">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="38fcf-188">无论是个人选项卡还是 bot，仅显示与您的应用程序中的用户活动相关的内容。</span><span class="sxs-lookup"><span data-stu-id="38fcf-188">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="38fcf-191">不：显示不相关或过于广泛的内容</span><span class="sxs-lookup"><span data-stu-id="38fcf-191">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="38fcf-192">在个人上下文中，不为不属于用户的团队显示内容。</span><span class="sxs-lookup"><span data-stu-id="38fcf-192">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="38fcf-193">个人 bot 内容应侧重于个人（而不是组）。</span><span class="sxs-lookup"><span data-stu-id="38fcf-193">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="38fcf-196">复杂的应用程序功能</span><span class="sxs-lookup"><span data-stu-id="38fcf-196">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="38fcf-197">Do：允许用户在浏览器中访问复杂功能</span><span class="sxs-lookup"><span data-stu-id="38fcf-197">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="38fcf-198">您的应用程序应重点关注团队中的核心任务，但您仍可以在浏览器中查看完整的独立应用程序。</span><span class="sxs-lookup"><span data-stu-id="38fcf-198">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="38fcf-200">请勿：包含整个应用程序</span><span class="sxs-lookup"><span data-stu-id="38fcf-200">Don’t: Include your entire app</span></span>

<span data-ttu-id="38fcf-201">除非您专为工作组创建应用程序，否则在协作工具中可能没有意义的功能。</span><span class="sxs-lookup"><span data-stu-id="38fcf-201">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="示例展示了个人应用程序最佳实践。" border="false":::

## <a name="manage-a-personal-tab"></a><span data-ttu-id="38fcf-203">管理个人选项卡</span><span class="sxs-lookup"><span data-stu-id="38fcf-203">Manage a personal tab</span></span>

<span data-ttu-id="38fcf-204">在团队的左侧，用户可以右键单击个人应用以固定、删除和配置其他应用程序选项。</span><span class="sxs-lookup"><span data-stu-id="38fcf-204">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="示例显示用于管理个人应用程序的选项。" border="false":::

## <a name="learn-more"></a><span data-ttu-id="38fcf-206">了解更多</span><span class="sxs-lookup"><span data-stu-id="38fcf-206">Learn more</span></span>

<span data-ttu-id="38fcf-207">根据个人应用程序的范围，这些其他设计准则可能会有所帮助：</span><span class="sxs-lookup"><span data-stu-id="38fcf-207">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="38fcf-208">设计选项卡</span><span class="sxs-lookup"><span data-stu-id="38fcf-208">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="38fcf-209">设计机器人</span><span class="sxs-lookup"><span data-stu-id="38fcf-209">Designing you bot</span></span>](../../bots/design/bots.md)

## <a name="validate-your-design"></a><span data-ttu-id="38fcf-210">验证设计</span><span class="sxs-lookup"><span data-stu-id="38fcf-210">Validate your design</span></span>

<span data-ttu-id="38fcf-211">如果计划将应用程序发布到 AppSource，则应了解通常会在提交期间导致应用程序失败的设计问题。</span><span class="sxs-lookup"><span data-stu-id="38fcf-211">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="38fcf-212">检查设计验证准则</span><span class="sxs-lookup"><span data-stu-id="38fcf-212">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
