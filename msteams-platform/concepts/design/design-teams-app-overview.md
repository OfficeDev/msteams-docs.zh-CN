---
title: 设计自定义应用
author: heath-hamilton
description: 了解如何设计Microsoft Teams应用。 资源包括Microsoft Teams UI 工具包、最佳做法、示例等。
localization_priority: Normal
ms.author: lajanuar
ms.topic: overview
ms.openlocfilehash: 2f21872bd8c37026528ff6fde282e8c433d5e052
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565114"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="f18ad-104">设计Microsoft Teams应用</span><span class="sxs-lookup"><span data-stu-id="f18ad-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="概念性图像，Microsoft Teams设计指南。":::

<span data-ttu-id="f18ad-106">无论你是使用低代码工具的设计人员、产品经理、开发人员还是制造商，这些指南都可以帮助你快速做出正确的设计决策，Microsoft Teams应用。</span><span class="sxs-lookup"><span data-stu-id="f18ad-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="f18ad-107">Teams应用设计原则</span><span class="sxs-lookup"><span data-stu-id="f18ad-107">Teams app design principles</span></span>

<span data-ttu-id="f18ad-108">Teams应用可帮助用户共同实现更多目标。</span><span class="sxs-lookup"><span data-stu-id="f18ad-108">Teams apps help people achieve more together.</span></span> <span data-ttu-id="f18ad-109">使用这些原则来指导你的设计。</span><span class="sxs-lookup"><span data-stu-id="f18ad-109">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="f18ad-110">协作</span><span class="sxs-lookup"><span data-stu-id="f18ad-110">Collaborative</span></span>

<span data-ttu-id="f18ad-111">Teams应用可帮助用户共同实现更多目标。</span><span class="sxs-lookup"><span data-stu-id="f18ad-111">Teams apps help people achieve more together.</span></span> <span data-ttu-id="f18ad-112">使用这些原则来指导你的设计。</span><span class="sxs-lookup"><span data-stu-id="f18ad-112">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="f18ad-113">可信赖性</span><span class="sxs-lookup"><span data-stu-id="f18ad-113">Trustworthy</span></span>

<span data-ttu-id="f18ad-114">应用安全且合规。</span><span class="sxs-lookup"><span data-stu-id="f18ad-114">The app is secure and compliant.</span></span> <span data-ttu-id="f18ad-115">用户可以轻松查找有关隐私的信息。</span><span class="sxs-lookup"><span data-stu-id="f18ad-115">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="f18ad-116">全局包含</span><span class="sxs-lookup"><span data-stu-id="f18ad-116">Globally inclusive</span></span>

<span data-ttu-id="f18ad-117">具有所有背景、技能集和专业的人都可以使用该应用。</span><span class="sxs-lookup"><span data-stu-id="f18ad-117">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="f18ad-118">它在文化、种族和社会上是感知的。</span><span class="sxs-lookup"><span data-stu-id="f18ad-118">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="f18ad-119">轻负载</span><span class="sxs-lookup"><span data-stu-id="f18ad-119">Light</span></span>

<span data-ttu-id="f18ad-120">该应用侧重于与工作流混合的核心Teams方案。</span><span class="sxs-lookup"><span data-stu-id="f18ad-120">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="f18ad-121">本机或不同</span><span class="sxs-lookup"><span data-stu-id="f18ad-121">Native or distinct</span></span>

<span data-ttu-id="f18ad-122">应用使用本机Teams设计组件或你自己的组件。</span><span class="sxs-lookup"><span data-stu-id="f18ad-122">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="f18ad-123">不混合配色方案、控件等。</span><span class="sxs-lookup"><span data-stu-id="f18ad-123">There’s no blend of color schemes, controls, and so on.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="f18ad-124">有用</span><span class="sxs-lookup"><span data-stu-id="f18ad-124">Useful</span></span>

<span data-ttu-id="f18ad-125">该应用基于用户需要在应用中Teams。</span><span class="sxs-lookup"><span data-stu-id="f18ad-125">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="f18ad-126">易于使用</span><span class="sxs-lookup"><span data-stu-id="f18ad-126">Easy to use</span></span>

<span data-ttu-id="f18ad-127">UI 易于理解、外观和声调舒适，并且使用户工作效率更高。</span><span class="sxs-lookup"><span data-stu-id="f18ad-127">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="f18ad-128">快速响应</span><span class="sxs-lookup"><span data-stu-id="f18ad-128">Responsive</span></span>

<span data-ttu-id="f18ad-129">应用与设备和屏幕无关。</span><span class="sxs-lookup"><span data-stu-id="f18ad-129">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="f18ad-130">辅助功能</span><span class="sxs-lookup"><span data-stu-id="f18ad-130">Accessible</span></span>

<span data-ttu-id="f18ad-131">应用在Teams对比度、导航替代项等方面满足辅助功能要求。</span><span class="sxs-lookup"><span data-stu-id="f18ad-131">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="f18ad-132">描述良好</span><span class="sxs-lookup"><span data-stu-id="f18ad-132">Well described</span></span>

<span data-ttu-id="f18ad-133">文本、图标和图像可明确应用用途及其使用方法。</span><span class="sxs-lookup"><span data-stu-id="f18ad-133">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="f18ad-134">创建统一体验</span><span class="sxs-lookup"><span data-stu-id="f18ad-134">Creating a cohesive experience</span></span>

<span data-ttu-id="f18ad-135">设计Teams应用与设计传统的 Web 应用类似，但有些不同。</span><span class="sxs-lookup"><span data-stu-id="f18ad-135">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="f18ad-136">有效的设计可突出显示应用的独特属性，同时自然地适应Teams和上下文。</span><span class="sxs-lookup"><span data-stu-id="f18ad-136">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="f18ad-137">这些指南和资源可以帮助您实现此平衡。</span><span class="sxs-lookup"><span data-stu-id="f18ad-137">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="f18ad-138">你将了解在设计 Teams 应用模型时 (该做什么，例如选项卡应用中的多级) 。</span><span class="sxs-lookup"><span data-stu-id="f18ad-138">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="planning-your-app"></a><span data-ttu-id="f18ad-139">规划应用</span><span class="sxs-lookup"><span data-stu-id="f18ad-139">Planning your app</span></span>

<span data-ttu-id="f18ad-140">若要设计高质量的Teams，你必须先了解希望应用执行哪些操作，以及你认为用户如何使用它。</span><span class="sxs-lookup"><span data-stu-id="f18ad-140">To design a high-quality Teams app, you must first understand what you want your app to do and how you think people will use it.</span></span> <span data-ttu-id="f18ad-141">如果尚未开始，请花些时间正确 [规划你的应用](../../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="f18ad-141">If you haven't already, take some time to properly [plan your app](../../concepts/extensibility-points.md).</span></span>

## <a name="design-fundamentals"></a><span data-ttu-id="f18ad-142">设计基础知识</span><span class="sxs-lookup"><span data-stu-id="f18ad-142">Design fundamentals</span></span>

<span data-ttu-id="f18ad-143">了解[应用设计Teams基础](design-teams-app-fundamentals.md)，包括布局、配色方案等。</span><span class="sxs-lookup"><span data-stu-id="f18ad-143">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="basic-fluent-ui-components-for-teams"></a><span data-ttu-id="f18ad-144">适用于用户的基本 Fluent UI Teams</span><span class="sxs-lookup"><span data-stu-id="f18ad-144">Basic Fluent UI components for Teams</span></span>

<span data-ttu-id="f18ad-145">这些是基于 Fluent UI 的核心元素，用于创建熟悉的Teams[接口](design-teams-app-basic-ui-components.md)。</span><span class="sxs-lookup"><span data-stu-id="f18ad-145">Based on Fluent UI, these are the [core elements for creating familiar Teams interfaces](design-teams-app-basic-ui-components.md).</span></span>

## <a name="ui-templates"></a><span data-ttu-id="f18ad-146">UI 模板</span><span class="sxs-lookup"><span data-stu-id="f18ad-146">UI templates</span></span>

<span data-ttu-id="f18ad-147">使用常见用例和工作流的模板快速Teams[高保真度设计](design-teams-app-ui-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="f18ad-147">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="f18ad-148">应用功能</span><span class="sxs-lookup"><span data-stu-id="f18ad-148">App capabilities</span></span>

<span data-ttu-id="f18ad-149">了解用户如何添加、使用和管理Teams应用，以充分利用设计中每个功能。</span><span class="sxs-lookup"><span data-stu-id="f18ad-149">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="f18ad-150">个人应用</span><span class="sxs-lookup"><span data-stu-id="f18ad-150">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="f18ad-151">选项卡</span><span class="sxs-lookup"><span data-stu-id="f18ad-151">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="f18ad-152">消息扩展</span><span class="sxs-lookup"><span data-stu-id="f18ad-152">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="f18ad-153">机器人</span><span class="sxs-lookup"><span data-stu-id="f18ad-153">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="f18ad-154">会议扩展</span><span class="sxs-lookup"><span data-stu-id="f18ad-154">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [<span data-ttu-id="f18ad-155">任务模块</span><span class="sxs-lookup"><span data-stu-id="f18ad-155">Task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
* [<span data-ttu-id="f18ad-156">自适应卡</span><span class="sxs-lookup"><span data-stu-id="f18ad-156">Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)

## <a name="app-customization"></a><span data-ttu-id="f18ad-157">应用自定义</span><span class="sxs-lookup"><span data-stu-id="f18ad-157">App customization</span></span>

<span data-ttu-id="f18ad-158">了解Teams管理员如何根据组织需求自定义或重新品牌应用。</span><span class="sxs-lookup"><span data-stu-id="f18ad-158">Understand how the Teams admin can customize or rebrand the app based on the organization's need.</span></span> <span data-ttu-id="f18ad-159">如果在清单架构中定义 ，则 `configurableProperties` 启用此自定义。</span><span class="sxs-lookup"><span data-stu-id="f18ad-159">This customization is enabled if you define the `configurableProperties` in the manifest schema.</span></span> <span data-ttu-id="f18ad-160">有关详细信息，请参阅自定义[应用程序中Microsoft Teams。](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="f18ad-160">For more information, see [Customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

> [!NOTE]
> <span data-ttu-id="f18ad-161">通过应用自定义，管理员可以更改通过机器人、消息传递扩展、选项卡和连接器加载的应用的外观。</span><span class="sxs-lookup"><span data-stu-id="f18ad-161">App customization enables admins to change the look-and-feel of the apps loaded through bots, messaging extensions, tabs, and connectors.</span></span> <span data-ttu-id="f18ad-162">例如，如果Teams将 *Contoso* 中的应用程序的名称自定义为 *Contoso 代理*，则应用将显示为用户的新名称 *Contoso Agent。*</span><span class="sxs-lookup"><span data-stu-id="f18ad-162">For example, if the Teams admin customizes the name of an app from *Contoso* to *Contoso Agent*, then the app will appear with the new name *Contoso Agent* to users.</span></span> <span data-ttu-id="f18ad-163">但是，向聊天添加连接器时，连接器仍将在列表中显示应用的名称为 *Contoso*。</span><span class="sxs-lookup"><span data-stu-id="f18ad-163">However, while adding a connector to a chat, in the list the connectors will still show the name of the app as *Contoso*.</span></span>
> 
> <span data-ttu-id="f18ad-164">最佳做法是，你必须提供自定义指南，以便应用用户和客户在自定义应用时遵循这些准则。</span><span class="sxs-lookup"><span data-stu-id="f18ad-164">As a best practice, you must provide customization guidelines for app users and customers to follow when customizing your app.</span></span> <span data-ttu-id="f18ad-165">有关详细信息，请参阅自定义[应用程序中Microsoft Teams。](/MicrosoftTeams/customize-apps)</span><span class="sxs-lookup"><span data-stu-id="f18ad-165">For more information, see [customize apps in Microsoft Teams](/MicrosoftTeams/customize-apps).</span></span>

## <a name="tools-and-samples"></a><span data-ttu-id="f18ad-166">工具和示例</span><span class="sxs-lookup"><span data-stu-id="f18ad-166">Tools and samples</span></span>

<span data-ttu-id="f18ad-167">以下工具可帮助设计人员和开发人员入门：</span><span class="sxs-lookup"><span data-stu-id="f18ad-167">The following tools can help designers and developers get started:</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="f18ad-168">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="f18ad-168">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="f18ad-169">设计Teams UI 组件、模板以及可根据需要拖放和修改的示例设计应用。</span><span class="sxs-lookup"><span data-stu-id="f18ad-169">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="f18ad-170">UI 工具包还包括有关应用在不同的应用场景中的外观和行为Teams信息。</span><span class="sxs-lookup"><span data-stu-id="f18ad-170">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f18ad-171">获取图 (UI) </span><span class="sxs-lookup"><span data-stu-id="f18ad-171">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="f18ad-172">Microsoft TeamsUI 库</span><span class="sxs-lookup"><span data-stu-id="f18ad-172">Microsoft Teams UI Library</span></span>

<span data-ttu-id="f18ad-173">在浏览器中查看和测试Teams UI 模板和相关组件。</span><span class="sxs-lookup"><span data-stu-id="f18ad-173">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f18ad-174">尝试 UI 库 (场) </span><span class="sxs-lookup"><span data-stu-id="f18ad-174">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="f18ad-175">将这些模板和相关组件直接导入到Teams应用项目中。</span><span class="sxs-lookup"><span data-stu-id="f18ad-175">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f18ad-176">获取 UI 库 (GitHub) </span><span class="sxs-lookup"><span data-stu-id="f18ad-176">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="f18ad-177">示例应用</span><span class="sxs-lookup"><span data-stu-id="f18ad-177">Sample app</span></span>

<span data-ttu-id="f18ad-178">安装示例应用以查看 UI 模板在上下文中的外观Teams行为。</span><span class="sxs-lookup"><span data-stu-id="f18ad-178">Install a sample app to see how UI templates look and behave within Teams contexts.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f18ad-179">获取示例应用 (GitHub) </span><span class="sxs-lookup"><span data-stu-id="f18ad-179">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="f18ad-180">其他资源</span><span class="sxs-lookup"><span data-stu-id="f18ad-180">Other resources</span></span>

<span data-ttu-id="f18ad-181">若要了解更多信息，请尝试以下资源之一：</span><span class="sxs-lookup"><span data-stu-id="f18ad-181">To learn more, try one of the following resources:</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="f18ad-182">Fluent UI 文档</span><span class="sxs-lookup"><span data-stu-id="f18ad-182">Fluent UI documentation</span></span>

<span data-ttu-id="f18ad-183">获取用于构建用户体验的基于 Fluent UI 的组件的代码示例Teams详细信息。</span><span class="sxs-lookup"><span data-stu-id="f18ad-183">Get code samples and implementation details for the Fluent UI-based components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f18ad-184">尝试Teams Fluent UI (UI 组件) </span><span class="sxs-lookup"><span data-stu-id="f18ad-184">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="f18ad-185">自适应卡片设计器</span><span class="sxs-lookup"><span data-stu-id="f18ad-185">Adaptive Cards designer</span></span>

<span data-ttu-id="f18ad-186">在基于 Web 的工具中设计自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="f18ad-186">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f18ad-187">试用自适应卡片设计器</span><span class="sxs-lookup"><span data-stu-id="f18ad-187">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
