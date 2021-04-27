---
title: 使用 UI 模板设计应用
author: heath-hamilton
description: 使用 Microsoft Teams 中常见的标准化 UI 组件、布局和模式更快地设计应用。
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: d627ce3b29ffa071d0d7e238c572c7cb69fa4cd9
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020763"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="833ba-103">使用 UI 模板设计 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="833ba-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="833ba-104">使用 UI 模板更快地设计 Microsoft Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="833ba-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="833ba-105">模板是基于 Fluent UI 的组件的集合，这些组件适用于常见的 Teams 用例，让你有更多的时间来为用户找到最佳体验。</span><span class="sxs-lookup"><span data-stu-id="833ba-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="833ba-106">工具和示例入门</span><span class="sxs-lookup"><span data-stu-id="833ba-106">Getting started with tools and samples</span></span>

<span data-ttu-id="833ba-107">以下资源可帮助你使用 UI 模板设计和开发应用。</span><span class="sxs-lookup"><span data-stu-id="833ba-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="833ba-108">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="833ba-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="833ba-109">从 Microsoft Teams UI 工具包获取应用设计的 UI 模板，其中还包括有关用法、结构分析、辅助功能和最佳做法的广泛信息。</span><span class="sxs-lookup"><span data-stu-id="833ba-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="833ba-110">获取图 (UI) </span><span class="sxs-lookup"><span data-stu-id="833ba-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="833ba-111">Microsoft Teams UI 库</span><span class="sxs-lookup"><span data-stu-id="833ba-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="833ba-112">在浏览器中查看和测试单个 Teams UI 模板和相关组件。</span><span class="sxs-lookup"><span data-stu-id="833ba-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="833ba-113">尝试 UI 库 (场) </span><span class="sxs-lookup"><span data-stu-id="833ba-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="833ba-114">直接将这些模板和相关组件导入到 Teams 应用项目中。</span><span class="sxs-lookup"><span data-stu-id="833ba-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="833ba-115">使用 GitHub (获取 UI) </span><span class="sxs-lookup"><span data-stu-id="833ba-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="833ba-116">示例应用</span><span class="sxs-lookup"><span data-stu-id="833ba-116">Sample app</span></span>

<span data-ttu-id="833ba-117">安装示例应用以查看 UI 模板在 Teams 上下文中的外观和行为。</span><span class="sxs-lookup"><span data-stu-id="833ba-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="833ba-118">从 GitHub (获取) </span><span class="sxs-lookup"><span data-stu-id="833ba-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="list"></a><span data-ttu-id="833ba-119">列表</span><span class="sxs-lookup"><span data-stu-id="833ba-119">List</span></span>

<span data-ttu-id="833ba-120">可以使用列表以可扫描的格式显示相关项目，并允许用户对整个列表或单个项目采取操作。</span><span class="sxs-lookup"><span data-stu-id="833ba-120">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="示例显示列表 UI 模板。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="833ba-122">热门用例</span><span class="sxs-lookup"><span data-stu-id="833ba-122">Top use cases</span></span>

* <span data-ttu-id="833ba-123">显示数据</span><span class="sxs-lookup"><span data-stu-id="833ba-123">Display data</span></span>
* <span data-ttu-id="833ba-124">应用内容的上下文操作</span><span class="sxs-lookup"><span data-stu-id="833ba-124">Contextual actions on app content</span></span>

## <a name="dashboard"></a><span data-ttu-id="833ba-125">仪表板</span><span class="sxs-lookup"><span data-stu-id="833ba-125">Dashboard</span></span>

<span data-ttu-id="833ba-126">仪表板在 Teams 个人应用或选项卡 (集中显示不同类型的) 。</span><span class="sxs-lookup"><span data-stu-id="833ba-126">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="833ba-127">用户至少应该能够自定义他们在仪表板上看到部分内容。</span><span class="sxs-lookup"><span data-stu-id="833ba-127">Users should be able to customize at least some of what they see on a dashboard.</span></span>

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="示例显示仪表板 UI 模板。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="833ba-129">热门用例</span><span class="sxs-lookup"><span data-stu-id="833ba-129">Top use cases</span></span>

* <span data-ttu-id="833ba-130">分析数据</span><span class="sxs-lookup"><span data-stu-id="833ba-130">Analyze data</span></span>
* <span data-ttu-id="833ba-131">报告指标</span><span class="sxs-lookup"><span data-stu-id="833ba-131">Report metrics</span></span>
* <span data-ttu-id="833ba-132">在一个地方组织不同的信息</span><span class="sxs-lookup"><span data-stu-id="833ba-132">Organize different information in one place</span></span>

## <a name="form"></a><span data-ttu-id="833ba-133">表单</span><span class="sxs-lookup"><span data-stu-id="833ba-133">Form</span></span>

<span data-ttu-id="833ba-134">表单用于以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="833ba-134">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="833ba-135">对输入字段进行清晰标记和逻辑分组对于获得良好的用户体验至关重要。</span><span class="sxs-lookup"><span data-stu-id="833ba-135">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="示例显示表单 UI 模板。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="833ba-137">热门用例</span><span class="sxs-lookup"><span data-stu-id="833ba-137">Top use cases</span></span>

* <span data-ttu-id="833ba-138">登录</span><span class="sxs-lookup"><span data-stu-id="833ba-138">Sign in</span></span>
* <span data-ttu-id="833ba-139">用户配置文件</span><span class="sxs-lookup"><span data-stu-id="833ba-139">User profiles</span></span>
* <span data-ttu-id="833ba-140">设置</span><span class="sxs-lookup"><span data-stu-id="833ba-140">Settings</span></span>
* <span data-ttu-id="833ba-141">用户输入集合</span><span class="sxs-lookup"><span data-stu-id="833ba-141">User input collection</span></span>

## <a name="sign-in"></a><span data-ttu-id="833ba-142">登录</span><span class="sxs-lookup"><span data-stu-id="833ba-142">Sign in</span></span>

<span data-ttu-id="833ba-143">你可以为不同的 Teams 上下文和标识提供程序设计应用登录流。</span><span class="sxs-lookup"><span data-stu-id="833ba-143">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="833ba-144">以下示例包括单一登录 (SSO) ，建议这样做以简化身份验证体验。</span><span class="sxs-lookup"><span data-stu-id="833ba-144">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="示例显示登录 UI 模板。" border="false":::

### <a name="top-use-case"></a><span data-ttu-id="833ba-146">热门用例</span><span class="sxs-lookup"><span data-stu-id="833ba-146">Top use case</span></span>

* <span data-ttu-id="833ba-147">对用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="833ba-147">Authenticate users</span></span>

## <a name="task-board"></a><span data-ttu-id="833ba-148">任务板</span><span class="sxs-lookup"><span data-stu-id="833ba-148">Task board</span></span>

<span data-ttu-id="833ba-149">任务板（有时称为看板或街道）是一组卡片，通常用于跟踪工作项或票证的状态。</span><span class="sxs-lookup"><span data-stu-id="833ba-149">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="833ba-150">它还可用于将任何类型的内容分类为类别。</span><span class="sxs-lookup"><span data-stu-id="833ba-150">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="833ba-151">可以在列之间编辑和移动卡片。</span><span class="sxs-lookup"><span data-stu-id="833ba-151">You can edit and move the cards between columns.</span></span>

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="示例显示任务板 UI 模板。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="833ba-153">热门用例</span><span class="sxs-lookup"><span data-stu-id="833ba-153">Top use cases</span></span>

* <span data-ttu-id="833ba-154">项目管理。</span><span class="sxs-lookup"><span data-stu-id="833ba-154">Project management.</span></span> <span data-ttu-id="833ba-155">分配任务和跟踪状态</span><span class="sxs-lookup"><span data-stu-id="833ba-155">Assigning tasks and tracking status</span></span>
* <span data-ttu-id="833ba-156">集体讨论。</span><span class="sxs-lookup"><span data-stu-id="833ba-156">Brainstorming.</span></span> <span data-ttu-id="833ba-157">在不同类别中添加想法</span><span class="sxs-lookup"><span data-stu-id="833ba-157">Adding ideas in different categories</span></span>
* <span data-ttu-id="833ba-158">对练习进行排序。</span><span class="sxs-lookup"><span data-stu-id="833ba-158">Sorting exercises.</span></span> <span data-ttu-id="833ba-159">将任何类型的信息组织到存储桶</span><span class="sxs-lookup"><span data-stu-id="833ba-159">Organizing any kind of information into buckets</span></span>

## <a name="data-visualization"></a><span data-ttu-id="833ba-160">数据可视化</span><span class="sxs-lookup"><span data-stu-id="833ba-160">Data visualization</span></span>

<span data-ttu-id="833ba-161">可以使用不同的卡片大小 (、双精度和) ，以在同一页面上堆叠和组织数据可视化效果。</span><span class="sxs-lookup"><span data-stu-id="833ba-161">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="833ba-162">卡片可缩放以适合列布局并填充空白区域。</span><span class="sxs-lookup"><span data-stu-id="833ba-162">The cards scale to fit the column layout and fill in blank spaces.</span></span>

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="示例显示数据可视化 UI 模板。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="833ba-164">热门用例</span><span class="sxs-lookup"><span data-stu-id="833ba-164">Top use cases</span></span>

* <span data-ttu-id="833ba-165">显示复杂信息</span><span class="sxs-lookup"><span data-stu-id="833ba-165">Display complex information</span></span>
* <span data-ttu-id="833ba-166">创建仪表板</span><span class="sxs-lookup"><span data-stu-id="833ba-166">Create a dashboard</span></span>

## <a name="wizard"></a><span data-ttu-id="833ba-167">向导</span><span class="sxs-lookup"><span data-stu-id="833ba-167">Wizard</span></span>

<span data-ttu-id="833ba-168">向导将指导用户完成多个屏幕以完成任务 (如设置过程) 。</span><span class="sxs-lookup"><span data-stu-id="833ba-168">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="示例显示向导 UI 模板。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="833ba-170">热门用例</span><span class="sxs-lookup"><span data-stu-id="833ba-170">Top use cases</span></span>

* <span data-ttu-id="833ba-171">设置</span><span class="sxs-lookup"><span data-stu-id="833ba-171">Setup</span></span>
* <span data-ttu-id="833ba-172">载入</span><span class="sxs-lookup"><span data-stu-id="833ba-172">Onboarding</span></span>
* <span data-ttu-id="833ba-173">首次运行体验</span><span class="sxs-lookup"><span data-stu-id="833ba-173">First-run experiences</span></span>

## <a name="empty-state"></a><span data-ttu-id="833ba-174">空状态</span><span class="sxs-lookup"><span data-stu-id="833ba-174">Empty state</span></span>

<span data-ttu-id="833ba-175">空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="833ba-175">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="833ba-176">它非常灵活，可调整它以使用以下设计中一个组件、一些组件或所有组件。</span><span class="sxs-lookup"><span data-stu-id="833ba-176">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="示例显示空状态 UI 模板。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="833ba-178">热门用例</span><span class="sxs-lookup"><span data-stu-id="833ba-178">Top use cases</span></span>

* <span data-ttu-id="833ba-179">登录</span><span class="sxs-lookup"><span data-stu-id="833ba-179">Sign in</span></span>
* <span data-ttu-id="833ba-180">欢迎消息和首次运行体验</span><span class="sxs-lookup"><span data-stu-id="833ba-180">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="833ba-181">成功消息</span><span class="sxs-lookup"><span data-stu-id="833ba-181">Success messages</span></span>
* <span data-ttu-id="833ba-182">错误消息</span><span class="sxs-lookup"><span data-stu-id="833ba-182">Error messages</span></span>

## <a name="notification-bar"></a><span data-ttu-id="833ba-183">通知栏</span><span class="sxs-lookup"><span data-stu-id="833ba-183">Notification bar</span></span>

<span data-ttu-id="833ba-184">通知栏是一个专用区域，用于显示无需用户立即采取措施的简短重要消息。</span><span class="sxs-lookup"><span data-stu-id="833ba-184">A notification bar is a dedicated area for displaying a brief, important messages that do not require the user to take immediate action.</span></span> <span data-ttu-id="833ba-185">特定背景颜色和图标与特定类型的邮件相关联， (请参阅下面的) 。</span><span class="sxs-lookup"><span data-stu-id="833ba-185">Specific background colors and icons are associated with specific types of messages (see below).</span></span>

:::image type="content" source="../../assets/images/ui-templates/notification-bar.png" alt-text="示例显示通知栏模板。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="833ba-187">热门用例</span><span class="sxs-lookup"><span data-stu-id="833ba-187">Top use cases</span></span>

* <span data-ttu-id="833ba-188">关键消息、错误和警告</span><span class="sxs-lookup"><span data-stu-id="833ba-188">Critical messages, errors, and warnings</span></span>
* <span data-ttu-id="833ba-189">成功消息</span><span class="sxs-lookup"><span data-stu-id="833ba-189">Success messages</span></span>
* <span data-ttu-id="833ba-190">信息性或促销性消息</span><span class="sxs-lookup"><span data-stu-id="833ba-190">Informational or promotional messages</span></span>

## <a name="left-nav"></a><span data-ttu-id="833ba-191">左导航</span><span class="sxs-lookup"><span data-stu-id="833ba-191">Left nav</span></span>

<span data-ttu-id="833ba-192">使用左侧导航键浏览 Teams 选项卡内的多个页面。在下面的示例中，左侧导航位于通道列表和选项卡内容之间。</span><span class="sxs-lookup"><span data-stu-id="833ba-192">Use the left nav to browse multiple pages within your Teams tab. In the following example, the left nav is between the channel list and tab content.</span></span>

:::image type="content" source="../../assets/images/ui-templates/left-nav.png" alt-text="示例显示左侧导航模板。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="833ba-194">热门用例</span><span class="sxs-lookup"><span data-stu-id="833ba-194">Top use cases</span></span>

* <span data-ttu-id="833ba-195">浏览 Teams 选项卡内的多个页面</span><span class="sxs-lookup"><span data-stu-id="833ba-195">Browse multiple pages within a Teams tab</span></span>
* <span data-ttu-id="833ba-196">将复杂应用分解为多个页面</span><span class="sxs-lookup"><span data-stu-id="833ba-196">Break down complex apps into multiple pages</span></span>

## <a name="breadcrumb"></a><span data-ttu-id="833ba-197">痕迹导航栏</span><span class="sxs-lookup"><span data-stu-id="833ba-197">Breadcrumb</span></span>

<span data-ttu-id="833ba-198">痕迹导航是一种导航帮助，可传达应用的层次结构。</span><span class="sxs-lookup"><span data-stu-id="833ba-198">Breadcrumbs are a navigational aid that convey your app’s hierarchy.</span></span> <span data-ttu-id="833ba-199">它们可帮助用户了解他们查看的页面如何适应整体体验，并提供了对层次结构中较高级别的一键访问。</span><span class="sxs-lookup"><span data-stu-id="833ba-199">They help users understand how the page they’re viewing fits into the overall experience and afford one-click access to higher levels in that hierarchy.</span></span>

:::image type="content" source="../../assets/images/ui-templates/breadcrumb.png" alt-text="示例显示痕迹导航模板。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="833ba-201">热门用例</span><span class="sxs-lookup"><span data-stu-id="833ba-201">Top use cases</span></span>

* <span data-ttu-id="833ba-202">通信层次结构</span><span class="sxs-lookup"><span data-stu-id="833ba-202">Communicate hierarchy</span></span>
* <span data-ttu-id="833ba-203">导航</span><span class="sxs-lookup"><span data-stu-id="833ba-203">Navigation</span></span>

## <a name="toolbar"></a><span data-ttu-id="833ba-204">工具栏</span><span class="sxs-lookup"><span data-stu-id="833ba-204">Toolbar</span></span>

<span data-ttu-id="833ba-205">工具栏是一个容器，用于对一组控件进行分组。</span><span class="sxs-lookup"><span data-stu-id="833ba-205">A toolbar is a container for grouping a set of controls.</span></span>

:::image type="content" source="../../assets/images/ui-templates/toolbar.png" alt-text="示例显示工具栏模板。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="833ba-207">热门用例</span><span class="sxs-lookup"><span data-stu-id="833ba-207">Top use cases</span></span>

* <span data-ttu-id="833ba-208">应用内容的上下文操作</span><span class="sxs-lookup"><span data-stu-id="833ba-208">Contextual actions on app content</span></span>
* <span data-ttu-id="833ba-209">上下文筛选器和查找</span><span class="sxs-lookup"><span data-stu-id="833ba-209">Contextual filter and find</span></span>
* <span data-ttu-id="833ba-210">导航和痕迹导航</span><span class="sxs-lookup"><span data-stu-id="833ba-210">Navigation and breadcrumbs</span></span>

## <a name="stage"></a><span data-ttu-id="833ba-211">阶段</span><span class="sxs-lookup"><span data-stu-id="833ba-211">Stage</span></span>

<span data-ttu-id="833ba-212">Stage 为用户提供了一种在 Teams 中打开实体（如图像、文件或网站）的方法，而不是在另一个应用或浏览器中打开它。</span><span class="sxs-lookup"><span data-stu-id="833ba-212">Stage offers a way for users to open an entity—like an image, file, or website—in Teams instead of opening it in another app or browser.</span></span> <span data-ttu-id="833ba-213">阶段的主要用例是查看;图面不应用于复杂的交互。</span><span class="sxs-lookup"><span data-stu-id="833ba-213">The primary use case of stage is viewing; the surface should not be used for complex interactions.</span></span>

<span data-ttu-id="833ba-214"> (实现说明：使用大型任务模块[.) ](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)</span><span class="sxs-lookup"><span data-stu-id="833ba-214">(Implementation note: Build your stage using a large [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).)</span></span>

:::image type="content" source="../../assets/images/ui-templates/stage.png" alt-text="示例显示阶段模板。" border="false":::

### <a name="top-use-cases"></a><span data-ttu-id="833ba-216">热门用例</span><span class="sxs-lookup"><span data-stu-id="833ba-216">Top use cases</span></span>

* <span data-ttu-id="833ba-217">在 Teams 中打开实体，而不是其他应用或浏览器</span><span class="sxs-lookup"><span data-stu-id="833ba-217">Open an entity in Teams instead of another app or browser</span></span>
* <span data-ttu-id="833ba-218">聚焦媒体或其他内容</span><span class="sxs-lookup"><span data-stu-id="833ba-218">Spotlight media or other content</span></span>
