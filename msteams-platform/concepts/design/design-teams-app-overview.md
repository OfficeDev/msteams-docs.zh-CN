---
title: 设计自定义应用
author: heath-hamilton
description: 了解如何设计Microsoft Teams应用。 资源包括Microsoft Teams UI 工具包、最佳做法、示例等。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 19b8f8cbcbc52aa02ccd5d94f5bc4c088f2ae28a
ms.sourcegitcommit: 4224c44d169b1a289cbf1d3353de6bc6de7c7ea8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2021
ms.locfileid: "52644873"
---
# <a name="designing-your-microsoft-teams-app"></a><span data-ttu-id="ed15a-104">设计Microsoft Teams应用</span><span class="sxs-lookup"><span data-stu-id="ed15a-104">Designing your Microsoft Teams app</span></span>

:::image type="content" source="../../assets/images/design-guidelines-overview.png" alt-text="概念性图像，Microsoft Teams设计指南。":::

<span data-ttu-id="ed15a-106">无论你是使用低代码工具的设计人员、产品经理、开发人员还是制造商，这些指南都可以帮助你快速做出正确的设计决策，Microsoft Teams应用。</span><span class="sxs-lookup"><span data-stu-id="ed15a-106">Whether you're a designer, product manager, developer, or maker using low-code tools, these guidelines can help you quickly make the right design decisions for your Microsoft Teams app.</span></span>

## <a name="creating-a-cohesive-experience"></a><span data-ttu-id="ed15a-107">创建统一体验</span><span class="sxs-lookup"><span data-stu-id="ed15a-107">Creating a cohesive experience</span></span>

<span data-ttu-id="ed15a-108">设计Teams应用与设计传统的 Web 应用类似，但有些不同。</span><span class="sxs-lookup"><span data-stu-id="ed15a-108">Designing a Teams app is like designing a conventional web app—but also a little different.</span></span> <span data-ttu-id="ed15a-109">有效的设计可突出显示应用的独特属性，同时自然地适应Teams和上下文。</span><span class="sxs-lookup"><span data-stu-id="ed15a-109">An effective design highlights your app's unique attributes while fitting naturally with Teams features and contexts.</span></span>

<span data-ttu-id="ed15a-110">这些指南和资源可以帮助您实现此平衡。</span><span class="sxs-lookup"><span data-stu-id="ed15a-110">These guidelines and resources can help you strike that balance.</span></span> <span data-ttu-id="ed15a-111">你将了解在设计 Teams 应用模型时 (该做什么，例如选项卡应用中的多级) 。</span><span class="sxs-lookup"><span data-stu-id="ed15a-111">You'll know what to do and what to avoid when designing your Teams app (such as multi-level navigation in a tab).</span></span>

## <a name="teams-app-design-principles"></a><span data-ttu-id="ed15a-112">Teams应用设计原则</span><span class="sxs-lookup"><span data-stu-id="ed15a-112">Teams app design principles</span></span>

<span data-ttu-id="ed15a-113">Teams应用可帮助用户共同实现更多目标。</span><span class="sxs-lookup"><span data-stu-id="ed15a-113">Teams apps help people achieve more together.</span></span> <span data-ttu-id="ed15a-114">使用这些原则来指导你的设计。</span><span class="sxs-lookup"><span data-stu-id="ed15a-114">Use these principles to guide your design.</span></span>

:::row:::
   :::column span="":::

### <a name="collaborative"></a><span data-ttu-id="ed15a-115">协作</span><span class="sxs-lookup"><span data-stu-id="ed15a-115">Collaborative</span></span>

<span data-ttu-id="ed15a-116">Teams应用可帮助用户共同实现更多目标。</span><span class="sxs-lookup"><span data-stu-id="ed15a-116">Teams apps help people achieve more together.</span></span> <span data-ttu-id="ed15a-117">使用这些原则来指导你的设计。</span><span class="sxs-lookup"><span data-stu-id="ed15a-117">Use these principles to guide your design.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="trustworthy"></a><span data-ttu-id="ed15a-118">可信赖性</span><span class="sxs-lookup"><span data-stu-id="ed15a-118">Trustworthy</span></span>

<span data-ttu-id="ed15a-119">应用安全且合规。</span><span class="sxs-lookup"><span data-stu-id="ed15a-119">The app is secure and compliant.</span></span> <span data-ttu-id="ed15a-120">用户可以轻松查找有关隐私的信息。</span><span class="sxs-lookup"><span data-stu-id="ed15a-120">Users can easily find information about privacy.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="globally-inclusive"></a><span data-ttu-id="ed15a-121">全局包含</span><span class="sxs-lookup"><span data-stu-id="ed15a-121">Globally inclusive</span></span>

<span data-ttu-id="ed15a-122">具有所有背景、技能集和专业的人都可以使用该应用。</span><span class="sxs-lookup"><span data-stu-id="ed15a-122">People of all backgrounds, skillsets, and disciplines can use the app.</span></span> <span data-ttu-id="ed15a-123">它在文化、种族和社会上是感知的。</span><span class="sxs-lookup"><span data-stu-id="ed15a-123">It’s culturally, racially, and socially aware.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="light"></a><span data-ttu-id="ed15a-124">轻负载</span><span class="sxs-lookup"><span data-stu-id="ed15a-124">Light</span></span>

<span data-ttu-id="ed15a-125">该应用侧重于与工作流混合的核心Teams方案。</span><span class="sxs-lookup"><span data-stu-id="ed15a-125">The app focuses on core scenarios that blend with Teams workflows.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="native-or-distinct"></a><span data-ttu-id="ed15a-126">本机或不同</span><span class="sxs-lookup"><span data-stu-id="ed15a-126">Native or distinct</span></span>

<span data-ttu-id="ed15a-127">应用使用本机Teams设计组件或你自己的组件。</span><span class="sxs-lookup"><span data-stu-id="ed15a-127">The app uses native Teams design components or your own.</span></span> <span data-ttu-id="ed15a-128">不混合配色方案、控件等。</span><span class="sxs-lookup"><span data-stu-id="ed15a-128">There’s no blend of color schemes, controls, and so on.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="useful"></a><span data-ttu-id="ed15a-129">有用</span><span class="sxs-lookup"><span data-stu-id="ed15a-129">Useful</span></span>

<span data-ttu-id="ed15a-130">该应用基于用户需要在应用中Teams。</span><span class="sxs-lookup"><span data-stu-id="ed15a-130">The app is based on a scenario people need to do in Teams.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="easy-to-use"></a><span data-ttu-id="ed15a-131">易于使用</span><span class="sxs-lookup"><span data-stu-id="ed15a-131">Easy to use</span></span>

<span data-ttu-id="ed15a-132">UI 易于理解、外观和声调舒适，并且使用户工作效率更高。</span><span class="sxs-lookup"><span data-stu-id="ed15a-132">The UI is easy to understand, pleasant in look and tone, and makes people more productive.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="responsive"></a><span data-ttu-id="ed15a-133">快速响应</span><span class="sxs-lookup"><span data-stu-id="ed15a-133">Responsive</span></span>

<span data-ttu-id="ed15a-134">应用与设备和屏幕无关。</span><span class="sxs-lookup"><span data-stu-id="ed15a-134">The app is device and screen agnostic.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="accessible"></a><span data-ttu-id="ed15a-135">辅助功能</span><span class="sxs-lookup"><span data-stu-id="ed15a-135">Accessible</span></span>

<span data-ttu-id="ed15a-136">应用在Teams对比度、导航替代项等方面满足辅助功能要求。</span><span class="sxs-lookup"><span data-stu-id="ed15a-136">The app meets Teams accessibility requirements in terms of color contrast, navigation alternatives, and more.</span></span>

   :::column-end:::
   :::column span="":::

### <a name="well-described"></a><span data-ttu-id="ed15a-137">描述良好</span><span class="sxs-lookup"><span data-stu-id="ed15a-137">Well described</span></span>

<span data-ttu-id="ed15a-138">文本、图标和图像可明确应用用途及其使用方法。</span><span class="sxs-lookup"><span data-stu-id="ed15a-138">Text, icons, and images make it clear what the app is for and how to use it.</span></span>

   :::column-end:::
:::row-end:::

## <a name="teams-design-system"></a><span data-ttu-id="ed15a-139">Teams设计系统</span><span class="sxs-lookup"><span data-stu-id="ed15a-139">Teams design system</span></span>

<span data-ttu-id="ed15a-140">了解[应用设计Teams基础](design-teams-app-fundamentals.md)，包括布局、配色方案等。</span><span class="sxs-lookup"><span data-stu-id="ed15a-140">Learn the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="ed15a-141">应用功能</span><span class="sxs-lookup"><span data-stu-id="ed15a-141">App capabilities</span></span>

<span data-ttu-id="ed15a-142">了解用户如何添加、使用和管理Teams应用，以充分利用设计中每个功能。</span><span class="sxs-lookup"><span data-stu-id="ed15a-142">Understand how people add, use, and manage Teams apps to make the most of each capability in your design.</span></span>

* [<span data-ttu-id="ed15a-143">个人应用</span><span class="sxs-lookup"><span data-stu-id="ed15a-143">Personal apps</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="ed15a-144">选项卡</span><span class="sxs-lookup"><span data-stu-id="ed15a-144">Tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="ed15a-145">消息扩展</span><span class="sxs-lookup"><span data-stu-id="ed15a-145">Messaging extensions</span></span>](../../messaging-extensions/design/messaging-extension-design.md)
* [<span data-ttu-id="ed15a-146">机器人</span><span class="sxs-lookup"><span data-stu-id="ed15a-146">Bots</span></span>](../../bots/design/bots.md)
* [<span data-ttu-id="ed15a-147">会议扩展</span><span class="sxs-lookup"><span data-stu-id="ed15a-147">Meeting extensions</span></span>](../../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="ui-templates"></a><span data-ttu-id="ed15a-148">UI 模板</span><span class="sxs-lookup"><span data-stu-id="ed15a-148">UI templates</span></span>

<span data-ttu-id="ed15a-149">使用常见用例和工作流的模板快速Teams[高保真度设计](design-teams-app-ui-templates.md)。</span><span class="sxs-lookup"><span data-stu-id="ed15a-149">Quickly create complex, high-fidelity designs with [templates for common Teams use cases and workflows](design-teams-app-ui-templates.md).</span></span>

## <a name="basic-ui-components"></a><span data-ttu-id="ed15a-150">基本 UI 组件</span><span class="sxs-lookup"><span data-stu-id="ed15a-150">Basic UI components</span></span>

<span data-ttu-id="ed15a-151">这些是基于 Fluent UI 的核心[](design-teams-app-basic-ui-components.md)元素，可用于从头开始Teams体验。</span><span class="sxs-lookup"><span data-stu-id="ed15a-151">Based on Fluent UI, these are the [core elements](design-teams-app-basic-ui-components.md) you can use to create Teams experiences from scratch.</span></span>

## <a name="tools-and-samples"></a><span data-ttu-id="ed15a-152">工具和示例</span><span class="sxs-lookup"><span data-stu-id="ed15a-152">Tools and samples</span></span>

<span data-ttu-id="ed15a-153">以下工具可帮助设计人员和开发人员入门：</span><span class="sxs-lookup"><span data-stu-id="ed15a-153">The following tools can help designers and developers get started:</span></span>

### <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="ed15a-154">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="ed15a-154">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="ed15a-155">设计Teams UI 组件、模板以及可根据需要拖放和修改的示例设计应用。</span><span class="sxs-lookup"><span data-stu-id="ed15a-155">Design a Teams app with UI components, templates, and examples that you can drag, drop, and modify as needed.</span></span> <span data-ttu-id="ed15a-156">UI 工具包还包括有关应用在不同的应用场景中的外观和行为Teams信息。</span><span class="sxs-lookup"><span data-stu-id="ed15a-156">The UI kit also includes comprehensive information about how apps should look and behave in different Teams scenarios.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ed15a-157">获取图 (UI) </span><span class="sxs-lookup"><span data-stu-id="ed15a-157">Get the UI kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

### <a name="microsoft-teams-ui-library"></a><span data-ttu-id="ed15a-158">Microsoft TeamsUI 库</span><span class="sxs-lookup"><span data-stu-id="ed15a-158">Microsoft Teams UI Library</span></span>

<span data-ttu-id="ed15a-159">在浏览器中查看和测试Teams UI 模板和相关组件。</span><span class="sxs-lookup"><span data-stu-id="ed15a-159">View and test individual Teams UI templates and related components in your browser.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ed15a-160">尝试 UI 库 (场) </span><span class="sxs-lookup"><span data-stu-id="ed15a-160">Try the UI library (playground)</span></span>](https://dev-int.teams.microsoft.com/storybook/main/index.html)

<span data-ttu-id="ed15a-161">将这些模板和相关组件直接导入到Teams应用项目中。</span><span class="sxs-lookup"><span data-stu-id="ed15a-161">Import these templates and related components directly into your Teams app project.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ed15a-162">获取 UI 库 (GitHub) </span><span class="sxs-lookup"><span data-stu-id="ed15a-162">Get the UI library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="sample-app"></a><span data-ttu-id="ed15a-163">示例应用</span><span class="sxs-lookup"><span data-stu-id="ed15a-163">Sample app</span></span>

<span data-ttu-id="ed15a-164">你可以上载示例应用，以查看应用在客户端中的外观Teams行为。</span><span class="sxs-lookup"><span data-stu-id="ed15a-164">You can upload a sample app to see how apps should look and behave in the Teams client.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ed15a-165">获取示例应用 (GitHub) </span><span class="sxs-lookup"><span data-stu-id="ed15a-165">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="other-resources"></a><span data-ttu-id="ed15a-166">其他资源</span><span class="sxs-lookup"><span data-stu-id="ed15a-166">Other resources</span></span>

<span data-ttu-id="ed15a-167">若要了解更多信息，请尝试以下资源之一：</span><span class="sxs-lookup"><span data-stu-id="ed15a-167">To learn more, try one of the following resources:</span></span>

### <a name="fluent-ui-documentation"></a><span data-ttu-id="ed15a-168">Fluent UI 文档</span><span class="sxs-lookup"><span data-stu-id="ed15a-168">Fluent UI documentation</span></span>

<span data-ttu-id="ed15a-169">获取用于构建用户体验的基本 Fluent UI 组件的代码示例Teams详细信息。</span><span class="sxs-lookup"><span data-stu-id="ed15a-169">Get code samples and implementation details for the basic Fluent UI components used to build Teams experiences.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ed15a-170">尝试Teams Fluent UI (UI 组件) </span><span class="sxs-lookup"><span data-stu-id="ed15a-170">Try Teams UI components (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

### <a name="adaptive-cards-designer"></a><span data-ttu-id="ed15a-171">自适应卡片设计器</span><span class="sxs-lookup"><span data-stu-id="ed15a-171">Adaptive Cards designer</span></span>

<span data-ttu-id="ed15a-172">在基于 Web 的工具中设计自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="ed15a-172">Design Adaptive Cards in our web-based tool.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ed15a-173">试用自适应卡片设计器</span><span class="sxs-lookup"><span data-stu-id="ed15a-173">Try the Adaptive Cards designer</span></span>](https://adaptivecards.io/designer/)
