---
title: 使用 UI 模板设计应用
author: heath-hamilton
description: 使用通常在整个应用中看到的标准化 UI 组件、布局和模式更快地Microsoft Teams。
ms.author: lajanuar
localization_priority: Normal
ms.topic: reference
ms.openlocfilehash: 5026554070396dcc55390496b6754961e8e037bc
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644816"
---
# <a name="designing-your-microsoft-teams-app-with-ui-templates"></a><span data-ttu-id="3b7ef-103">使用 UI Microsoft Teams设计应用</span><span class="sxs-lookup"><span data-stu-id="3b7ef-103">Designing your Microsoft Teams app with UI templates</span></span>

<span data-ttu-id="3b7ef-104">使用 UI Microsoft Teams更快地设计应用。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-104">Design your Microsoft Teams app faster with UI templates.</span></span> <span data-ttu-id="3b7ef-105">模板是基于 Fluent UI 的组件的集合，这些组件可跨常见Teams用例工作，从而为您提供更多时间来为用户找到最佳体验。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-105">The templates are a collection of Fluent UI-based components that work across common Teams use cases, giving you more time to figure out the best experience for your users.</span></span>

## <a name="getting-started-with-tools-and-samples"></a><span data-ttu-id="3b7ef-106">工具和示例入门</span><span class="sxs-lookup"><span data-stu-id="3b7ef-106">Getting started with tools and samples</span></span>

<span data-ttu-id="3b7ef-107">以下资源可帮助你使用 UI 模板设计和开发应用。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-107">The following resources can help you design and develop your app using UI templates.</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="3b7ef-108">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="3b7ef-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="3b7ef-109">从应用 UI 工具包中为应用设计获取 UI 模板Microsoft Teams，其中还包括有关用法、结构分析、辅助功能和最佳做法的广泛信息。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-109">Grab UI templates for your app design from the Microsoft Teams UI Kit, which also includes extensive information about usage, anatomy, accessibility, and best practices.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b7ef-110">获取图 (UI) </span><span class="sxs-lookup"><span data-stu-id="3b7ef-110">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="3b7ef-111">Microsoft TeamsUI 库</span><span class="sxs-lookup"><span data-stu-id="3b7ef-111">Microsoft Teams UI Library</span></span>

<span data-ttu-id="3b7ef-112">在浏览器中查看和测试Teams UI 模板和相关组件。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-112">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b7ef-113">尝试 UI 库 (场) </span><span class="sxs-lookup"><span data-stu-id="3b7ef-113">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="3b7ef-114">将这些模板和相关组件直接导入到Teams应用项目中。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-114">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b7ef-115">获取 UI 库 (GitHub) </span><span class="sxs-lookup"><span data-stu-id="3b7ef-115">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="3b7ef-116">示例应用</span><span class="sxs-lookup"><span data-stu-id="3b7ef-116">Sample app</span></span>

<span data-ttu-id="3b7ef-117">安装示例应用以查看 UI 模板在上下文中的外观Teams行为。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-117">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3b7ef-118">获取示例应用 (GitHub) </span><span class="sxs-lookup"><span data-stu-id="3b7ef-118">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="dashboard"></a><span data-ttu-id="3b7ef-119">仪表板</span><span class="sxs-lookup"><span data-stu-id="3b7ef-119">Dashboard</span></span>

<span data-ttu-id="3b7ef-120">仪表板在中心位置显示不同类型的内容， (Teams应用或选项卡) 。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-120">A dashboard displays different types of content in a central location (Teams personal app or tab).</span></span> <span data-ttu-id="3b7ef-121">用户至少应该能够自定义他们在仪表板上看到部分内容。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-121">Users should be able to customize at least some of what they see on a dashboard.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="3b7ef-122">热门用例</span><span class="sxs-lookup"><span data-stu-id="3b7ef-122">Top use cases</span></span>

* <span data-ttu-id="3b7ef-123">分析数据</span><span class="sxs-lookup"><span data-stu-id="3b7ef-123">Analyze data</span></span>
* <span data-ttu-id="3b7ef-124">报告指标</span><span class="sxs-lookup"><span data-stu-id="3b7ef-124">Report metrics</span></span>
* <span data-ttu-id="3b7ef-125">在一个地方组织不同的信息</span><span class="sxs-lookup"><span data-stu-id="3b7ef-125">Organize different information in one place</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3b7ef-126">桌面</span><span class="sxs-lookup"><span data-stu-id="3b7ef-126">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/dashboard.png" alt-text="示例显示桌面上的仪表板 UI 模板。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3b7ef-128">移动</span><span class="sxs-lookup"><span data-stu-id="3b7ef-128">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-dashboard.png" alt-text="示例显示移动设备上的仪表板 UI 模板。" border="false":::

---

## <a name="data-visualization"></a><span data-ttu-id="3b7ef-130">数据可视化</span><span class="sxs-lookup"><span data-stu-id="3b7ef-130">Data visualization</span></span>

<span data-ttu-id="3b7ef-131">可以使用不同的卡片大小 (、双精度和) ，以在同一页面上堆叠和组织数据可视化效果。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-131">You can use different card sizes (single, double, and full) to stack and organize data visualizations on the same page.</span></span> <span data-ttu-id="3b7ef-132">卡片可缩放以适合列布局并填充空白区域。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-132">The cards scale to fit the column layout and fill in blank spaces.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="3b7ef-133">热门用例</span><span class="sxs-lookup"><span data-stu-id="3b7ef-133">Top use cases</span></span>

* <span data-ttu-id="3b7ef-134">显示复杂信息</span><span class="sxs-lookup"><span data-stu-id="3b7ef-134">Display complex information</span></span>
* <span data-ttu-id="3b7ef-135">创建仪表板</span><span class="sxs-lookup"><span data-stu-id="3b7ef-135">Create a dashboard</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3b7ef-136">桌面</span><span class="sxs-lookup"><span data-stu-id="3b7ef-136">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/data-viz.png" alt-text="示例显示桌面上的数据可视化 UI 模板。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3b7ef-138">移动</span><span class="sxs-lookup"><span data-stu-id="3b7ef-138">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-data-viz.png" alt-text="示例演示移动设备上的数据可视化 UI 模板。" border="false":::

---

## <a name="empty-state"></a><span data-ttu-id="3b7ef-140">空状态</span><span class="sxs-lookup"><span data-stu-id="3b7ef-140">Empty state</span></span>

<span data-ttu-id="3b7ef-141">空状态模板可用于多种方案，包括登录、首次运行体验、错误消息等。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-141">The empty state template can be used for many scenarios, including sign in, first-run experiences, error messages, and more.</span></span> <span data-ttu-id="3b7ef-142">它非常灵活，可调整它以使用以下设计中一个组件、一些组件或所有组件。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-142">It’s highly flexible⁠—adapt it to use one, a few, or all of the components in the following design.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="3b7ef-143">热门用例</span><span class="sxs-lookup"><span data-stu-id="3b7ef-143">Top use cases</span></span>

* <span data-ttu-id="3b7ef-144">登录</span><span class="sxs-lookup"><span data-stu-id="3b7ef-144">Sign in</span></span>
* <span data-ttu-id="3b7ef-145">欢迎消息和首次运行体验</span><span class="sxs-lookup"><span data-stu-id="3b7ef-145">Welcome messages and first-run experiences</span></span>
* <span data-ttu-id="3b7ef-146">成功消息</span><span class="sxs-lookup"><span data-stu-id="3b7ef-146">Success messages</span></span>
* <span data-ttu-id="3b7ef-147">错误消息</span><span class="sxs-lookup"><span data-stu-id="3b7ef-147">Error messages</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3b7ef-148">桌面</span><span class="sxs-lookup"><span data-stu-id="3b7ef-148">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/empty-state.png" alt-text="示例在桌面上显示空状态 UI 模板。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3b7ef-150">移动</span><span class="sxs-lookup"><span data-stu-id="3b7ef-150">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-empty-state.png" alt-text="示例显示移动设备上的空状态 UI 模板。" border="false":::

---

## <a name="filter"></a><span data-ttu-id="3b7ef-152">筛选器</span><span class="sxs-lookup"><span data-stu-id="3b7ef-152">Filter</span></span>

<span data-ttu-id="3b7ef-153">利用筛选器，您可以根据所选条件减少看到的信息。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-153">A filter allows you to reduce the information you see based on the criteria selected.</span></span> <span data-ttu-id="3b7ef-154">您可以将筛选器与表、列表、卡片和其他用于组织内容的组件一起包含。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-154">You can include filters with tables, lists, cards, and other components that organize content.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="3b7ef-155">热门用例</span><span class="sxs-lookup"><span data-stu-id="3b7ef-155">Top use cases</span></span>

<span data-ttu-id="3b7ef-156">组织内容，包括：</span><span class="sxs-lookup"><span data-stu-id="3b7ef-156">Organizing content in:</span></span>

* <span data-ttu-id="3b7ef-157">列表</span><span class="sxs-lookup"><span data-stu-id="3b7ef-157">Lists</span></span>
* <span data-ttu-id="3b7ef-158">表格</span><span class="sxs-lookup"><span data-stu-id="3b7ef-158">Tables</span></span>
* <span data-ttu-id="3b7ef-159">仪表板</span><span class="sxs-lookup"><span data-stu-id="3b7ef-159">Dashboards</span></span>
* <span data-ttu-id="3b7ef-160">数据可视化</span><span class="sxs-lookup"><span data-stu-id="3b7ef-160">Data visualization</span></span>

:::image type="content" source="../../assets/images/ui-templates/filter.png" alt-text="示例显示筛选器模板。" border="false":::

## <a name="form"></a><span data-ttu-id="3b7ef-162">表单</span><span class="sxs-lookup"><span data-stu-id="3b7ef-162">Form</span></span>

<span data-ttu-id="3b7ef-163">表单用于以结构化方式收集、验证和提交用户输入。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-163">Forms are used to collect, validate, and submit user input in a structured way.</span></span> <span data-ttu-id="3b7ef-164">对输入字段进行清晰标记和逻辑分组对于获得良好的用户体验至关重要。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-164">Clear labeling and logical groupings of input fields are critical for a good user experience.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="3b7ef-165">热门用例</span><span class="sxs-lookup"><span data-stu-id="3b7ef-165">Top use cases</span></span>

* <span data-ttu-id="3b7ef-166">登录</span><span class="sxs-lookup"><span data-stu-id="3b7ef-166">Sign in</span></span>
* <span data-ttu-id="3b7ef-167">用户配置文件</span><span class="sxs-lookup"><span data-stu-id="3b7ef-167">User profiles</span></span>
* <span data-ttu-id="3b7ef-168">设置</span><span class="sxs-lookup"><span data-stu-id="3b7ef-168">Settings</span></span>
* <span data-ttu-id="3b7ef-169">用户输入集合</span><span class="sxs-lookup"><span data-stu-id="3b7ef-169">User input collection</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3b7ef-170">桌面</span><span class="sxs-lookup"><span data-stu-id="3b7ef-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/form.png" alt-text="示例在桌面上显示表单 UI 模板。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3b7ef-172">移动</span><span class="sxs-lookup"><span data-stu-id="3b7ef-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-form.png" alt-text="示例显示移动设备上的表单 UI 模板。" border="false":::

---

## <a name="list"></a><span data-ttu-id="3b7ef-174">列表</span><span class="sxs-lookup"><span data-stu-id="3b7ef-174">List</span></span>

<span data-ttu-id="3b7ef-175">可以使用列表以可扫描的格式显示相关项目，并允许用户对整个列表或单个项目采取操作。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-175">You can use a list to display related items in a scannable format and allow users to take actions on an entire list or individual items.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="3b7ef-176">热门用例</span><span class="sxs-lookup"><span data-stu-id="3b7ef-176">Top use cases</span></span>

* <span data-ttu-id="3b7ef-177">显示数据</span><span class="sxs-lookup"><span data-stu-id="3b7ef-177">Display data</span></span>
* <span data-ttu-id="3b7ef-178">应用内容的上下文操作</span><span class="sxs-lookup"><span data-stu-id="3b7ef-178">Contextual actions on app content</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3b7ef-179">桌面</span><span class="sxs-lookup"><span data-stu-id="3b7ef-179">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/list.png" alt-text="示例显示桌面上的列表 UI 模板。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3b7ef-181">移动</span><span class="sxs-lookup"><span data-stu-id="3b7ef-181">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-list.png" alt-text="示例显示移动设备上的列表 UI 模板。" border="false":::

---

## <a name="sign-in"></a><span data-ttu-id="3b7ef-183">登录</span><span class="sxs-lookup"><span data-stu-id="3b7ef-183">Sign in</span></span>

<span data-ttu-id="3b7ef-184">你可以为不同的上下文和标识提供程序设计Teams登录流。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-184">You can design app sign-in flows for different Teams contexts and identity providers.</span></span> <span data-ttu-id="3b7ef-185">以下示例包括单一登录 (SSO) ，建议这样做以简化身份验证体验。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-185">The following example includes single sign-on (SSO), which we recommend for the simplest authentication experience.</span></span>

### <a name="top-use-case"></a><span data-ttu-id="3b7ef-186">热门用例</span><span class="sxs-lookup"><span data-stu-id="3b7ef-186">Top use case</span></span>

* <span data-ttu-id="3b7ef-187">对用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="3b7ef-187">Authenticate users</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3b7ef-188">桌面</span><span class="sxs-lookup"><span data-stu-id="3b7ef-188">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/sign-in.png" alt-text="示例显示桌面上的登录 UI 模板。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3b7ef-190">移动</span><span class="sxs-lookup"><span data-stu-id="3b7ef-190">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-sign-in.png" alt-text="示例显示移动设备上的登录 UI 模板。" border="false":::

---

## <a name="settings"></a><span data-ttu-id="3b7ef-192">设置</span><span class="sxs-lookup"><span data-stu-id="3b7ef-192">Settings</span></span>

<span data-ttu-id="3b7ef-193">设置屏幕是用户可以使用你的应用配置其首选项的地方。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-193">Settings screens are where users can configure their preferences with your app.</span></span> <span data-ttu-id="3b7ef-194"> (注意：设置是基本[UI 组件的](~/concepts/design/design-teams-app-basic-ui-components.md)容器 。) </span><span class="sxs-lookup"><span data-stu-id="3b7ef-194">(Note: Settings is a container for [basic UI components](~/concepts/design/design-teams-app-basic-ui-components.md).)</span></span>

### <a name="top-use-case"></a><span data-ttu-id="3b7ef-195">热门用例</span><span class="sxs-lookup"><span data-stu-id="3b7ef-195">Top use case</span></span>

* <span data-ttu-id="3b7ef-196">管理应用功能</span><span class="sxs-lookup"><span data-stu-id="3b7ef-196">Manage app features</span></span>

:::image type="content" source="../../assets/images/ui-templates/settings.png" alt-text="示例显示设置模板。" border="false":::

## <a name="task-board"></a><span data-ttu-id="3b7ef-198">任务板</span><span class="sxs-lookup"><span data-stu-id="3b7ef-198">Task board</span></span>

<span data-ttu-id="3b7ef-199">任务板（有时称为看板或街道）是一组卡片，通常用于跟踪工作项或票证的状态。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-199">A task board, sometimes called a kanban board or swim lanes, is a collection of cards often used to track the status of work items or tickets.</span></span> <span data-ttu-id="3b7ef-200">它还可用于将任何类型的内容分类为类别。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-200">It can also be used to sort any type of content into categories.</span></span> <span data-ttu-id="3b7ef-201">可以在列之间编辑和移动卡片。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-201">You can edit and move the cards between columns.</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="3b7ef-202">热门用例</span><span class="sxs-lookup"><span data-stu-id="3b7ef-202">Top use cases</span></span>

* <span data-ttu-id="3b7ef-203">项目管理。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-203">Project management.</span></span> <span data-ttu-id="3b7ef-204">分配任务和跟踪状态</span><span class="sxs-lookup"><span data-stu-id="3b7ef-204">Assigning tasks and tracking status</span></span>
* <span data-ttu-id="3b7ef-205">集体讨论。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-205">Brainstorming.</span></span> <span data-ttu-id="3b7ef-206">在不同类别中添加想法</span><span class="sxs-lookup"><span data-stu-id="3b7ef-206">Adding ideas in different categories</span></span>
* <span data-ttu-id="3b7ef-207">对练习进行排序。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-207">Sorting exercises.</span></span> <span data-ttu-id="3b7ef-208">将任何类型的信息组织到存储桶</span><span class="sxs-lookup"><span data-stu-id="3b7ef-208">Organizing any kind of information into buckets</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3b7ef-209">桌面</span><span class="sxs-lookup"><span data-stu-id="3b7ef-209">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/task-board.png" alt-text="示例在桌面上显示任务板 UI 模板。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3b7ef-211">移动</span><span class="sxs-lookup"><span data-stu-id="3b7ef-211">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-task-board.png" alt-text="示例显示移动设备上的任务板 UI 模板。" border="false":::

---

## <a name="wizard"></a><span data-ttu-id="3b7ef-213">向导</span><span class="sxs-lookup"><span data-stu-id="3b7ef-213">Wizard</span></span>

<span data-ttu-id="3b7ef-214">向导将指导用户完成多个屏幕以完成任务 (如设置过程) 。</span><span class="sxs-lookup"><span data-stu-id="3b7ef-214">A wizard guides a user through several screens to complete a task (such as a setup process).</span></span>

### <a name="top-use-cases"></a><span data-ttu-id="3b7ef-215">热门用例</span><span class="sxs-lookup"><span data-stu-id="3b7ef-215">Top use cases</span></span>

* <span data-ttu-id="3b7ef-216">设置</span><span class="sxs-lookup"><span data-stu-id="3b7ef-216">Setup</span></span>
* <span data-ttu-id="3b7ef-217">载入</span><span class="sxs-lookup"><span data-stu-id="3b7ef-217">Onboarding</span></span>
* <span data-ttu-id="3b7ef-218">首次运行体验</span><span class="sxs-lookup"><span data-stu-id="3b7ef-218">First-run experiences</span></span>

# <a name="desktop"></a>[<span data-ttu-id="3b7ef-219">桌面</span><span class="sxs-lookup"><span data-stu-id="3b7ef-219">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/ui-templates/wizard.png" alt-text="示例在桌面上显示向导 UI 模板。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="3b7ef-221">移动</span><span class="sxs-lookup"><span data-stu-id="3b7ef-221">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/ui-templates/mobile-wizard.png" alt-text="示例显示移动设备上的向导 UI 模板。" border="false":::

---
