---
title: 设计个人应用
description: 了解如何设计个人Teams并获取 Microsoft Teams UI 工具包。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: b3f08c39a7900b80fb46d167fae8d9e8bdbcc574
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101553"
---
# <a name="designing-your-personal-app-for-microsoft-teams"></a><span data-ttu-id="fecb4-103">为用户设计个人Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fecb4-103">Designing your personal app for Microsoft Teams</span></span>

<span data-ttu-id="fecb4-104">个人应用可以是自动程序、专用工作区，也可以同时为两者。</span><span class="sxs-lookup"><span data-stu-id="fecb4-104">A personal app can be a bot, private workspace, or both.</span></span> <span data-ttu-id="fecb4-105">有时，它的功能与创建或查看内容的位置类似，其他时候，当应用被配置为多个频道中的选项卡时，它会为用户提供其所有内容的鸟眼视图。</span><span class="sxs-lookup"><span data-stu-id="fecb4-105">Sometimes it functions like a place to create or view content, other times it offers the user a bird’s eye view of everything that's theirs when the app has been configured as a tab in multiple channels.</span></span>

<span data-ttu-id="fecb4-106">为了指导你的应用设计，以下信息介绍了并说明了用户如何添加、使用和管理应用中的个人Teams。</span><span class="sxs-lookup"><span data-stu-id="fecb4-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage personal apps in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="fecb4-107">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="fecb4-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="fecb4-108">你可以找到全面的个人应用设计指南，包括你可以根据需要获取和修改的元素，Microsoft Teams UI 工具包。</span><span class="sxs-lookup"><span data-stu-id="fecb4-108">You can find comprehensive personal app design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span> <span data-ttu-id="fecb4-109">UI 工具包还具有辅助功能和响应式大小调整等基本主题，此处未介绍这些主题。</span><span class="sxs-lookup"><span data-stu-id="fecb4-109">The UI kit also has essential topics such as accessibility and responsive sizing that aren't covered here.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fecb4-110">获取 Microsoft Teams UI Kit （用户）</span><span class="sxs-lookup"><span data-stu-id="fecb4-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-personal-app"></a><span data-ttu-id="fecb4-111">添加个人应用</span><span class="sxs-lookup"><span data-stu-id="fecb4-111">Add a personal app</span></span>

<span data-ttu-id="fecb4-112">可以通过选择 Teams (左侧的"更多"图标从 Teams app) Source ( (应用商店或应用Teams (添加个人应用，如以下示例) 所示。</span><span class="sxs-lookup"><span data-stu-id="fecb4-112">You can add a personal app from the Teams store (AppSource) or the app flyout by selecting the **More** icon on the left side of Teams (shown in the following example).</span></span>

:::image type="content" source="../../assets/images/personal-apps/add-from-app-flyout.png" alt-text="示例演示如何从应用飞出内容添加个人应用。" border="false":::

## <a name="use-a-personal-app-private-workspace"></a><span data-ttu-id="fecb4-114">使用个人应用 (工作区) </span><span class="sxs-lookup"><span data-stu-id="fecb4-114">Use a personal app (private workspace)</span></span>

<span data-ttu-id="fecb4-115">使用专用工作区，可以在中心位置查看对你有意义的应用内容，而无需离开Teams。</span><span class="sxs-lookup"><span data-stu-id="fecb4-115">With a private workspace, you can view app content that's meaningful to you in a central location without leaving Teams.</span></span>

<span data-ttu-id="fecb4-116"> (：专用工作区基于个人 [*选项卡功能*](../../build-your-first-app/build-personal-tab.md) 。) </span><span class="sxs-lookup"><span data-stu-id="fecb4-116">(Implementation note: The private workspace is based on the [*personal tab*](../../build-your-first-app/build-personal-tab.md) capability.)</span></span>

### <a name="anatomy-personal-app-private-workspace"></a><span data-ttu-id="fecb4-117">分析：个人应用 (专用工作区) </span><span class="sxs-lookup"><span data-stu-id="fecb4-117">Anatomy: Personal app (private workspace)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-component-anatomy.png" alt-text="示例显示个人选项卡的组件分析。" border="false":::

|<span data-ttu-id="fecb4-119">计数器</span><span class="sxs-lookup"><span data-stu-id="fecb4-119">Counter</span></span>|<span data-ttu-id="fecb4-120">说明</span><span class="sxs-lookup"><span data-stu-id="fecb4-120">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fecb4-121">A</span><span class="sxs-lookup"><span data-stu-id="fecb4-121">A</span></span>|<span data-ttu-id="fecb4-122">**应用属性**：应用徽标和名称。</span><span class="sxs-lookup"><span data-stu-id="fecb4-122">**App attribution**: Your app logo and name.</span></span>|
|<span data-ttu-id="fecb4-123">B</span><span class="sxs-lookup"><span data-stu-id="fecb4-123">B</span></span>|<span data-ttu-id="fecb4-124">**选项卡**：为个人应用提供导航。</span><span class="sxs-lookup"><span data-stu-id="fecb4-124">**Tabs**: Provides navigation for your personal app.</span></span> <span data-ttu-id="fecb4-125">例如，包括"关于 **"** 或"帮助 **"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="fecb4-125">For example, include an **About** or **Help** tab.</span></span>|
|<span data-ttu-id="fecb4-126">C</span><span class="sxs-lookup"><span data-stu-id="fecb4-126">C</span></span>|<span data-ttu-id="fecb4-127">**弹出视图**：将应用内容从父窗口推送到独立子窗口。</span><span class="sxs-lookup"><span data-stu-id="fecb4-127">**Popout view**: Pushes your app content from a parent window to a standalone child window.</span></span>|
|<span data-ttu-id="fecb4-128">D</span><span class="sxs-lookup"><span data-stu-id="fecb4-128">D</span></span>|<span data-ttu-id="fecb4-129">**更多菜单**：包括其他应用信息和选项。</span><span class="sxs-lookup"><span data-stu-id="fecb4-129">**More menu**: Includes additional app information and options.</span></span> <span data-ttu-id="fecb4-130"> (您也可以将选项卡设置 tab.) </span><span class="sxs-lookup"><span data-stu-id="fecb4-130">(You could alternatively make **Settings** a tab.)</span></span>|

:::image type="content" source="../../assets/images/personal-apps/personal-tab-structural-anatomy.png" alt-text="示例显示个人选项卡的结构结构分析。" border="false":::

|<span data-ttu-id="fecb4-132">计数器</span><span class="sxs-lookup"><span data-stu-id="fecb4-132">Counter</span></span>|<span data-ttu-id="fecb4-133">说明</span><span class="sxs-lookup"><span data-stu-id="fecb4-133">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fecb4-134">A</span><span class="sxs-lookup"><span data-stu-id="fecb4-134">A</span></span>|<span data-ttu-id="fecb4-135">**选项卡**：为个人应用提供导航。</span><span class="sxs-lookup"><span data-stu-id="fecb4-135">**Tabs**: Provides navigation for your personal app.</span></span>|
|<span data-ttu-id="fecb4-136">1</span><span class="sxs-lookup"><span data-stu-id="fecb4-136">1</span></span>|<span data-ttu-id="fecb4-137">**iframe：** 显示应用内容。</span><span class="sxs-lookup"><span data-stu-id="fecb4-137">**iframe**: Displays your app content.</span></span>|

### <a name="designing-with-ui-templates"></a><span data-ttu-id="fecb4-138">使用 UI 模板进行设计</span><span class="sxs-lookup"><span data-stu-id="fecb4-138">Designing with UI templates</span></span>

<span data-ttu-id="fecb4-139">使用以下 UI 模板Teams之一来帮助设计个人选项卡：</span><span class="sxs-lookup"><span data-stu-id="fecb4-139">Use one of the following Teams UI templates to help design your personal tab:</span></span>

* <span data-ttu-id="fecb4-140">[列表](../../concepts/design/design-teams-app-ui-templates.md#list)：列表可以以可扫描的格式显示相关项，并允许用户对整个列表或单个项目采取操作。</span><span class="sxs-lookup"><span data-stu-id="fecb4-140">[List](../../concepts/design/design-teams-app-ui-templates.md#list): Lists can display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>
* <span data-ttu-id="fecb4-141">[任务板](../../concepts/design/design-teams-app-ui-templates.md#task-board)：任务板（有时称为看板或街道）是一组卡片，通常用于跟踪工作项或票证的状态。</span><span class="sxs-lookup"><span data-stu-id="fecb4-141">[Task board](../../concepts/design/design-teams-app-ui-templates.md#task-board): A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span>
* <span data-ttu-id="fecb4-142">[仪表板](../../concepts/design/design-teams-app-ui-templates.md#dashboard)：仪表板是包含多个卡片的画布，可提供数据或内容的概述。</span><span class="sxs-lookup"><span data-stu-id="fecb4-142">[Dashboard](../../concepts/design/design-teams-app-ui-templates.md#dashboard): A dashboard is a canvas containing multiple cards that provide an overview of data or content.</span></span>
* <span data-ttu-id="fecb4-143">[表单](../../concepts/design/design-teams-app-ui-templates.md#form)：表单用于以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="fecb4-143">[Form](../../concepts/design/design-teams-app-ui-templates.md#form): Forms are for collecting, validating, and submitting user input in a structured way.</span></span>
* <span data-ttu-id="fecb4-144">[空状态](../../concepts/design/design-teams-app-ui-templates.md#empty-state)：空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="fecb4-144">[Empty state](../../concepts/design/design-teams-app-ui-templates.md#empty-state): The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span>
* <span data-ttu-id="fecb4-145">[左侧导航](../../concepts/design/design-teams-app-ui-templates.md#left-nav)：如果你的选项卡需要一些导航，左侧导航模板可以提供帮助。</span><span class="sxs-lookup"><span data-stu-id="fecb4-145">[Left nav](../../concepts/design/design-teams-app-ui-templates.md#left-nav): The left nav template can help if your tab requires some navigation.</span></span> <span data-ttu-id="fecb4-146">通常，应使 Tab 键导航保持在最低程度。</span><span class="sxs-lookup"><span data-stu-id="fecb4-146">In general, you should keep tab navigation to a minimum.</span></span>

## <a name="use-a-personal-app-bot"></a><span data-ttu-id="fecb4-147">使用个人应用 (自动) </span><span class="sxs-lookup"><span data-stu-id="fecb4-147">Use a personal app (bot)</span></span>

<span data-ttu-id="fecb4-148">个人应用可以包含用于一对一对话的自动程序以及私人通知 (例如，当同事在剪贴板上发布评论时) 。</span><span class="sxs-lookup"><span data-stu-id="fecb4-148">Personal apps can include a bot for one-on-one conversations and private notifications (for instance, when a colleague posts a comment on your artboard).</span></span> <span data-ttu-id="fecb4-149">自动程序在指定的选项卡中可用。</span><span class="sxs-lookup"><span data-stu-id="fecb4-149">The bot is available in a tab you specify.</span></span>

### <a name="anatomy-personal-app-bot"></a><span data-ttu-id="fecb4-150">结构：个人应用 (自动) </span><span class="sxs-lookup"><span data-stu-id="fecb4-150">Anatomy: Personal app (bot)</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-bot-anatomy.png" alt-text="示例显示个人自动程序组件分析。" border="false":::

|<span data-ttu-id="fecb4-152">计数器</span><span class="sxs-lookup"><span data-stu-id="fecb4-152">Counter</span></span>|<span data-ttu-id="fecb4-153">说明</span><span class="sxs-lookup"><span data-stu-id="fecb4-153">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="fecb4-154">A</span><span class="sxs-lookup"><span data-stu-id="fecb4-154">A</span></span>|<span data-ttu-id="fecb4-155">**自动程序** 选项卡：例如，包括一个 **聊天选项卡** 来访问机器人对话和通知。</span><span class="sxs-lookup"><span data-stu-id="fecb4-155">**Bot tab**: For example, include a **Chat** tab to access bot conversations and notifications.</span></span>|
|<span data-ttu-id="fecb4-156">B</span><span class="sxs-lookup"><span data-stu-id="fecb4-156">B</span></span>|<span data-ttu-id="fecb4-157">**自动程序** 消息：机器人通常以卡片形式发送消息和通知， (自适应卡片) 。</span><span class="sxs-lookup"><span data-stu-id="fecb4-157">**Bot message**: Bots often send messages and notifications in the form of a card (such as an Adaptive Card).</span></span>|
|<span data-ttu-id="fecb4-158">C</span><span class="sxs-lookup"><span data-stu-id="fecb4-158">C</span></span>|<span data-ttu-id="fecb4-159">**撰写框**：用于向自动程序发送邮件的输入字段。</span><span class="sxs-lookup"><span data-stu-id="fecb4-159">**Compose box**: Input field for sending messages to the bot.</span></span>|

## <a name="manage-a-personal-tab"></a><span data-ttu-id="fecb4-160">管理个人选项卡</span><span class="sxs-lookup"><span data-stu-id="fecb4-160">Manage a personal tab</span></span>

<span data-ttu-id="fecb4-161">在应用左侧Teams，用户可以右键单击个人应用以固定、删除和配置其他应用选项。</span><span class="sxs-lookup"><span data-stu-id="fecb4-161">On the left side of Teams, users can right click the personal app to pin, remove, and configure other app options.</span></span>

:::image type="content" source="../../assets/images/personal-apps/manage-personal-tab.png" alt-text="示例显示用于管理个人应用的选项。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="fecb4-163">最佳做法</span><span class="sxs-lookup"><span data-stu-id="fecb4-163">Best practices</span></span>

<span data-ttu-id="fecb4-164">使用这些建议创建高质量的应用体验。</span><span class="sxs-lookup"><span data-stu-id="fecb4-164">Use these recommendations to create a quality app experience.</span></span>

### <a name="tab-priority"></a><span data-ttu-id="fecb4-165">选项卡优先级</span><span class="sxs-lookup"><span data-stu-id="fecb4-165">Tab priority</span></span>

#### <a name="do-show-the-most-relevant-content-in-the-first-tab"></a><span data-ttu-id="fecb4-166">操作：显示第一个选项卡中最相关的内容</span><span class="sxs-lookup"><span data-stu-id="fecb4-166">Do: Show the most relevant content in the first tab</span></span>

<span data-ttu-id="fecb4-167">使用响应式大小调整时，右侧选项卡可能会被截断或退出视图。</span><span class="sxs-lookup"><span data-stu-id="fecb4-167">With responsive sizing, tabs on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-do.png" alt-text="示例显示第一个选项卡中显示最相关内容的个人应用。" border="false":::

#### <a name="dont-lead-with-secondary-content-or-metadata"></a><span data-ttu-id="fecb4-169">请勿：使用辅助内容或元数据领导</span><span class="sxs-lookup"><span data-stu-id="fecb4-169">Don’t: Lead with secondary content or metadata</span></span>

<span data-ttu-id="fecb4-170">与标准 Web 应用一样，选项卡导航应按有助于了解应用主要功能的顺序进行。</span><span class="sxs-lookup"><span data-stu-id="fecb4-170">Like a standard web app, tab navigation should progress in an order that helps make sense of your app’s primary features.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-priority-dont.png" alt-text="示例显示以辅助内容或元数据作为前导的个人应用。" border="false":::

### <a name="tab-hierarchy"></a><span data-ttu-id="fecb4-172">选项卡层次结构</span><span class="sxs-lookup"><span data-stu-id="fecb4-172">Tab hierarchy</span></span>

#### <a name="do-tabs-should-be-of-equal-hierarchy-and-represent-key-app-pages"></a><span data-ttu-id="fecb4-173">应做：选项卡的层次结构应相同，并代表关键应用页面</span><span class="sxs-lookup"><span data-stu-id="fecb4-173">Do: Tabs should be of equal hierarchy and represent key app pages</span></span>

<span data-ttu-id="fecb4-174">选项卡应分类应用的主要功能和内容。</span><span class="sxs-lookup"><span data-stu-id="fecb4-174">Your tabs should categorize your app’s primary features and content.</span></span> <span data-ttu-id="fecb4-175">使用响应式大小调整时，右侧的内容可能会被截断或退出视图。</span><span class="sxs-lookup"><span data-stu-id="fecb4-175">With responsive sizing, content on the right may become truncated or out of view.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-do.png" alt-text="示例显示具有相同层次结构选项卡的个人应用。" border="false":::

#### <a name="dont-include-different-levels-of-hierarchy"></a><span data-ttu-id="fecb4-177">请勿：包括不同级别的层次结构</span><span class="sxs-lookup"><span data-stu-id="fecb4-177">Don't: Include different levels of hierarchy</span></span>

<span data-ttu-id="fecb4-178">内容应按逻辑顺序进行，以帮助用户理解它。</span><span class="sxs-lookup"><span data-stu-id="fecb4-178">Your content should progress in a logical order that helps users make sense of it.</span></span> <span data-ttu-id="fecb4-179">如果您有两个紧密相关的选项卡，请考虑将它们合并到一个选项卡中。</span><span class="sxs-lookup"><span data-stu-id="fecb4-179">If you have two tabs that are closely related, consider combining them into one tab.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-hierarchy-dont.png" alt-text="示例显示层次结构级别不同的个人应用。" border="false":::

### <a name="first-run-experience"></a><span data-ttu-id="fecb4-181">首次运行体验</span><span class="sxs-lookup"><span data-stu-id="fecb4-181">First-run experience</span></span>

#### <a name="do-include-a-first-run-experience"></a><span data-ttu-id="fecb4-182">应做：包括首次运行体验</span><span class="sxs-lookup"><span data-stu-id="fecb4-182">Do: Include a first-run experience</span></span>

<span data-ttu-id="fecb4-183">首次使用个人应用时，应该至少有一个欢迎屏幕。</span><span class="sxs-lookup"><span data-stu-id="fecb4-183">There should be at least a welcome screen the first time you use a personal app.</span></span> <span data-ttu-id="fecb4-184">对于自动程序，描述自动程序可以执行哪些操作并提供快速操作，例如登录按钮。</span><span class="sxs-lookup"><span data-stu-id="fecb4-184">For bots, describe what your bot can do and provide quick actions, such as a sign-in button.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-do.png" alt-text="示例显示个人应用首次运行体验期间要执行哪些操作。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-fre-do.png" alt-text="另一个示例演示在个人应用首次运行体验期间要执行哪些操作。" border="false":::

#### <a name="dont-start-with-a-blank-screen"></a><span data-ttu-id="fecb4-187">不要：从空白屏幕开始</span><span class="sxs-lookup"><span data-stu-id="fecb4-187">Don't: Start with a blank screen</span></span>

<span data-ttu-id="fecb4-188">如果用户第一次运行你的应用时没有显示任何内容，用户可能会感到困惑。</span><span class="sxs-lookup"><span data-stu-id="fecb4-188">Users might be confused if nothing displays the first time they run your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-fre-dont.png" alt-text="示例显示个人应用首次运行体验期间不执行哪些操作。" border="false":::

### <a name="personalized-content"></a><span data-ttu-id="fecb4-190">个性化内容</span><span class="sxs-lookup"><span data-stu-id="fecb4-190">Personalized content</span></span>

#### <a name="do-aggregate-app-content-relevant-to-a-user"></a><span data-ttu-id="fecb4-191">操作：聚合与用户相关的应用内容</span><span class="sxs-lookup"><span data-stu-id="fecb4-191">Do: Aggregate app content relevant to a user</span></span>

<span data-ttu-id="fecb4-192">无论是个人选项卡还是自动程序，在应用中仅显示与用户活动相关的内容。</span><span class="sxs-lookup"><span data-stu-id="fecb4-192">Whether it's a personal tab or bot, display content related to only a user's activity in your app.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-do.png" alt-text="示例演示了使用个人应用和个性化内容要执行哪些操作。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-do.png" alt-text="另一个示例演示了使用个人应用和个性化内容要执行哪些操作。" border="false":::

#### <a name="dont-show-unrelated-or-overly-broad-content"></a><span data-ttu-id="fecb4-195">请勿：显示不相关或过于宽泛的内容</span><span class="sxs-lookup"><span data-stu-id="fecb4-195">Don’t: Show unrelated or overly broad content</span></span>

<span data-ttu-id="fecb4-196">在个人上下文中，请勿显示用户不是团队的一部分的内容。</span><span class="sxs-lookup"><span data-stu-id="fecb4-196">In personal contexts, don’t display content for teams a user isn't part of.</span></span> <span data-ttu-id="fecb4-197">个人自动程序内容应侧重于个人，而不是组。</span><span class="sxs-lookup"><span data-stu-id="fecb4-197">Personal bot content should focus on the individual—not a group.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-personalized-content-dont.png" alt-text="示例显示对个人应用和个性化内容不执行哪些操作。" border="false":::

:::image type="content" source="../../assets/images/personal-apps/personal-bot-personalized-content-dont.png" alt-text="另一个示例演示了对个人应用和个性化内容不执行哪些操作。" border="false":::

### <a name="complex-app-features"></a><span data-ttu-id="fecb4-200">复杂的应用功能</span><span class="sxs-lookup"><span data-stu-id="fecb4-200">Complex app features</span></span>

#### <a name="do-allow-users-to-access-complex-features-in-a-browser"></a><span data-ttu-id="fecb4-201">应做：允许用户在浏览器中访问复杂功能</span><span class="sxs-lookup"><span data-stu-id="fecb4-201">Do: Allow users to access complex features in a browser</span></span>

<span data-ttu-id="fecb4-202">你的应用应专注于应用中的核心Teams，但你仍然可以在浏览器中查看完整的独立应用。</span><span class="sxs-lookup"><span data-stu-id="fecb4-202">Your app should focus on core tasks in Teams, but you can still view the full, standalone app in a browser.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-do.png" alt-text="示例演示如何使用个人应用处理复杂的应用功能。" border="false":::

#### <a name="dont-include-your-entire-app"></a><span data-ttu-id="fecb4-204">请勿：包括整个应用</span><span class="sxs-lookup"><span data-stu-id="fecb4-204">Don’t: Include your entire app</span></span>

<span data-ttu-id="fecb4-205">除非你专门为用户创建了Teams，否则你在协作工具中可能没有意义的功能。</span><span class="sxs-lookup"><span data-stu-id="fecb4-205">Unless you created your app specifically for Teams, you probably have features that don’t make sense in a collaboration tool.</span></span>

:::image type="content" source="../../assets/images/personal-apps/personal-tab-feature-dont.png" alt-text="示例演示如何不通过个人应用处理复杂的应用功能。" border="false":::

## <a name="see-also"></a><span data-ttu-id="fecb4-207">另请参阅</span><span class="sxs-lookup"><span data-stu-id="fecb4-207">See also</span></span>

<span data-ttu-id="fecb4-208">以下其他设计指南可能会有所帮助，具体取决于你的个人应用的范围：</span><span class="sxs-lookup"><span data-stu-id="fecb4-208">These other design guidelines may help depending on the scope of your personal app:</span></span>

* [<span data-ttu-id="fecb4-209">设计选项卡</span><span class="sxs-lookup"><span data-stu-id="fecb4-209">Designing your tab</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="fecb4-210">正在设计自动程序</span><span class="sxs-lookup"><span data-stu-id="fecb4-210">Designing you bot</span></span>](../../bots/design/bots.md)
