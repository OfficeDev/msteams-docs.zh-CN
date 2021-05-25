---
title: 应用设计过程
author: heath-hamilton
description: 了解如何使用 Microsoft 工具和资源设计有效的应用，以及Microsoft Teams概念。
localization_priority: Normal
ms.author: surbhigupta
ms.topic: overview
ms.openlocfilehash: 533d386db2aa784fc7de955f92f64d07789f0553
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631260"
---
# <a name="design-process-for-microsoft-teams-apps"></a><span data-ttu-id="4b0c2-103">应用程序的设计Microsoft Teams过程</span><span class="sxs-lookup"><span data-stu-id="4b0c2-103">Design process for Microsoft Teams apps</span></span>

<span data-ttu-id="4b0c2-104">有多种工具和资源可用于设计Microsoft Teams应用。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-104">There are multiple tools and resources for designing your Microsoft Teams app.</span></span> <span data-ttu-id="4b0c2-105">以下步骤介绍了在设计过程中可能何时以及如何使用这些元素。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-105">The following steps describe when and how you might use these during the design process.</span></span> <span data-ttu-id="4b0c2-106"> (一些步骤可能在设计过程之外，但包含在其他上下文中。) </span><span class="sxs-lookup"><span data-stu-id="4b0c2-106">(Some of steps might be technically outside the design process but are included for additional context.)</span></span>

:::image type="content" source="~/assets/images/design-guidelines/teams-app-design-process.png" alt-text="显示应用设计Teams示例的关系图。" border="false":::

## <a name="plan-your-app"></a><span data-ttu-id="4b0c2-108">规划应用</span><span class="sxs-lookup"><span data-stu-id="4b0c2-108">Plan your app</span></span>

<span data-ttu-id="4b0c2-109">设计高质量的Teams需要了解希望应用执行哪些操作，以及你认为用户会如何使用它。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-109">Designing a high-quality Teams app requires understanding what you want the app to do and how you think people will use it.</span></span> <span data-ttu-id="4b0c2-110">但在开始设计之前，请回答以下问题：</span><span class="sxs-lookup"><span data-stu-id="4b0c2-110">Before you start designing, however, answer the following questions:</span></span>

* <span data-ttu-id="4b0c2-111">你的用户是谁？</span><span class="sxs-lookup"><span data-stu-id="4b0c2-111">Who are your users?</span></span>
* <span data-ttu-id="4b0c2-112">他们有什么问题？</span><span class="sxs-lookup"><span data-stu-id="4b0c2-112">What’s their problem?</span></span>
* <span data-ttu-id="4b0c2-113">你的应用如何解决他们的问题？</span><span class="sxs-lookup"><span data-stu-id="4b0c2-113">How can your app solve their problem?</span></span>
* <span data-ttu-id="4b0c2-114">你的应用将多久使用一次？</span><span class="sxs-lookup"><span data-stu-id="4b0c2-114">How often will your app be used?</span></span>
* <span data-ttu-id="4b0c2-115">有多少人将使用你的应用？</span><span class="sxs-lookup"><span data-stu-id="4b0c2-115">How many people will use your app?</span></span>
* <span data-ttu-id="4b0c2-116">你的应用可以提供哪种类型的投资回报？</span><span class="sxs-lookup"><span data-stu-id="4b0c2-116">What kind of return on investment can your app provide?</span></span>

<span data-ttu-id="4b0c2-117">有关详细信息，请参阅[了解应用的用例，以及](~/concepts/design/understand-use-cases.md)将用例映射到[Teams。](~/concepts/design/map-use-cases.md)</span><span class="sxs-lookup"><span data-stu-id="4b0c2-117">For more information, see [understand your app’s use cases](~/concepts/design/understand-use-cases.md) and [map use cases to Teams](~/concepts/design/map-use-cases.md).</span></span>

## <a name="get-teams-design-tools"></a><span data-ttu-id="4b0c2-118">获取Teams设计工具</span><span class="sxs-lookup"><span data-stu-id="4b0c2-118">Get Teams design tools</span></span>

<span data-ttu-id="4b0c2-119">Microsoft 提供了工具，可更轻松地设计Teams应用。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-119">Microsoft provides tools to make it easier to design your Teams app.</span></span> <span data-ttu-id="4b0c2-120">我们强烈建议至少使用 Microsoft Teams UI 工具包。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-120">At minimum, we strongly recommend using the Microsoft Teams UI Kit.</span></span>

### <a name="get-the-microsoft-teams-ui-kit"></a><span data-ttu-id="4b0c2-121">获取 Microsoft Teams UI 工具包</span><span class="sxs-lookup"><span data-stu-id="4b0c2-121">Get the Microsoft Teams UI Kit</span></span>

<span data-ttu-id="4b0c2-122">Microsoft Teams UI 工具包可以帮助你在最短时间内Teams开发有效的应用。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-122">The Microsoft Teams UI Kit can help you develop an effective Teams app in the shortest amount of time.</span></span> <span data-ttu-id="4b0c2-123">UI 工具包包含你在这些与应用设计相关的文档Teams，包括大量示例和变体。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-123">The UI kit has everything you see in these docs related to Teams app design and much more, including extensive examples and variations.</span></span>

<span data-ttu-id="4b0c2-124">UI 工具包还具有预建的模板和组件，你可以根据需要复制和修改这些模板和组件，以便你可以花费更多时间来设计最佳用户体验，而不是担心按钮的外观。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-124">The UI kit also has pre-built templates and components that you can copy and modify as needed, so you can spend more time designing the best user experience instead worrying about what a button should look like.</span></span>

> [!TIP]
> <span data-ttu-id="4b0c2-125">**UI 工具包是否适合我？**</span><span class="sxs-lookup"><span data-stu-id="4b0c2-125">**Is the UI kit for me?**</span></span> <span data-ttu-id="4b0c2-126">如果你对创建应用有Teams，可以。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-126">If you have any part in creating a Teams app, yes.</span></span> <span data-ttu-id="4b0c2-127">了解如何制作 Teams 应用不仅对设计人员、产品经理、使用 ID 的开发人员以及使用低代码工具（如 Microsoft Power Platform) ）构建的 (也很有帮助。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-127">Understanding how to craft a Teams app is not only helpful to designers but product managers, developers using IDEs, and makers building with low-code tools (such as the Microsoft Power Platform).</span></span>

1. <span data-ttu-id="4b0c2-128">转到["Microsoft Teams UI 工具包""图块"页面](https://www.figma.com/community/file/916836509871353159)。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-128">Go to the [Microsoft Teams UI Kit Figma page](https://www.figma.com/community/file/916836509871353159).</span></span>
1. <span data-ttu-id="4b0c2-129">选择 **"复制** "以打开 UI 工具包。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-129">Select **Duplicate** to open the UI kit.</span></span> <span data-ttu-id="4b0c2-130"> (可能需要先创建一个图块帐户。) </span><span class="sxs-lookup"><span data-stu-id="4b0c2-130">(You may have to first create a Figma account.)</span></span>

### <a name="try-the-sample-app"></a><span data-ttu-id="4b0c2-131">试用示例应用</span><span class="sxs-lookup"><span data-stu-id="4b0c2-131">Try the sample app</span></span>

<span data-ttu-id="4b0c2-132">你可以上载示例应用，以查看应用在客户端中的外观Teams行为。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-132">You can upload a sample app to see how apps should look and behave in the Teams client.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4b0c2-133">获取示例应用 (GitHub) </span><span class="sxs-lookup"><span data-stu-id="4b0c2-133">Get the sample app (GitHub)</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-ui-templates/ts)

## <a name="learn-teams-design-system"></a><span data-ttu-id="4b0c2-134">了解Teams设计系统</span><span class="sxs-lookup"><span data-stu-id="4b0c2-134">Learn Teams design system</span></span>

<span data-ttu-id="4b0c2-135">深入了解或至少熟悉应用设计[Teams，](design-teams-app-fundamentals.md)包括布局、配色方案等。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-135">Read in depth about or at least familiarize yourself with the [fundamentals of Teams app design](design-teams-app-fundamentals.md), including layout, color schemes, and more.</span></span>

## <a name="choose-app-capabilities"></a><span data-ttu-id="4b0c2-136">选择应用功能</span><span class="sxs-lookup"><span data-stu-id="4b0c2-136">Choose app capabilities</span></span>

<span data-ttu-id="4b0c2-137">在规划阶段后，你可以确定哪些Teams适合应用的用例。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-137">After the planning phase, you can determine which Teams capabilities fit your app’s use cases.</span></span> <span data-ttu-id="4b0c2-138">例如，如果你想要主动通知用户，则自动程序可能是正确的功能。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-138">For example, if you want to proactively notify people, a bot might be the right capability.</span></span>

<span data-ttu-id="4b0c2-139">UI 工具包具有预建设计，可展示用户通常如何添加、设置、使用和管理每个功能。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-139">The UI kit has pre-built designs that show you how people typically add, set up, use, and manage each capability.</span></span> <span data-ttu-id="4b0c2-140">为了快速参考，此信息也位于这些文档内，但借助 UI 工具包，你可以将其中任何设计复制并粘贴到应用设计中。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-140">For quick reference, this information is also in these docs, but with the UI kit you can copy and paste any of these designs into your app’s design.</span></span>

1. <span data-ttu-id="4b0c2-141">在 UI 工具包的左侧导航中，转到应用 **功能** ，然后选择你需要的应用功能。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-141">In the UI kit’s left nav, go to **App capabilities** and select the capability you want for your app.</span></span>
1. <span data-ttu-id="4b0c2-142">从该页面复制所需的内容以设计应用。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-142">Copy what you need from that page to design your app.</span></span><br />
   <span data-ttu-id="4b0c2-143">例如，如果你的应用支持使用单一登录进行身份验证，请复制并粘贴用于处理该确切方案的设计。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-143">For example, if your app supports authentication with single sign-on, copy and paste the design for handling that exact scenario.</span></span>

## <a name="design-your-ux-flow"></a><span data-ttu-id="4b0c2-144">设计用户体验流</span><span class="sxs-lookup"><span data-stu-id="4b0c2-144">Design your UX flow</span></span>

<span data-ttu-id="4b0c2-145">拥有基本应用设计后，你可以根据需要修改和优化它 (并快速) 从 UI 工具包复制 Teams UI 模板和基本组件。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-145">Once you have a basic app design, you can modify and refine it as much as you want (and quickly) by copying Teams UI templates and basic components from the UI kit.</span></span>

### <a name="design-with-ui-templates"></a><span data-ttu-id="4b0c2-146">使用 UI 模板进行设计</span><span class="sxs-lookup"><span data-stu-id="4b0c2-146">Design with UI templates</span></span>

<span data-ttu-id="4b0c2-147">UI 模板是复杂的高保真设计，适用于Teams用例和工作流。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-147">UI templates are complex, high-fidelity designs for common Teams use cases and workflows.</span></span> <span data-ttu-id="4b0c2-148">我们建议您使用这些模板来简化和加快设计过程，而不是从底部开始使用基本组件。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-148">Instead of starting from the bottom up with basic components, we recommend you use these templates to simplify and speed up the design process.</span></span>

1. <span data-ttu-id="4b0c2-149">在 UI 工具包的左侧导航中，转到 **"UI 模板"。**</span><span class="sxs-lookup"><span data-stu-id="4b0c2-149">In the UI kit’s left nav, go to **UI templates**.</span></span>
1. <span data-ttu-id="4b0c2-150">复制对你的应用设计有意义的模板。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-150">Copy templates that make sense for your app design.</span></span><br />
   <span data-ttu-id="4b0c2-151">例如，如果你正在设计个人应用，你可能想要使用仪表板模板。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-151">For example, if you’re designing a personal app, you may want to use a Dashboard template.</span></span>

### <a name="design-with-basic-ui-components"></a><span data-ttu-id="4b0c2-152">使用基本 UI 组件进行设计</span><span class="sxs-lookup"><span data-stu-id="4b0c2-152">Design with basic UI components</span></span>

<span data-ttu-id="4b0c2-153">这些是基于 Fluent UI 的核心元素，用于创建熟悉的Teams接口。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-153">Based on Fluent UI, these are the core elements for creating familiar Teams interfaces.</span></span> <span data-ttu-id="4b0c2-154">如果 UI 模板缺少你需要的内容，或者你只想从头开始设计应用，请使用这些组件。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-154">Use these components if a UI template is missing something you need or you just want to design your app from scratch.</span></span>

1. <span data-ttu-id="4b0c2-155">在 UI 工具包的左侧导航中，转到 **基本 UI 组件**。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-155">In the UI kit’s left nav, go to **Basic UI components**.</span></span>
1. <span data-ttu-id="4b0c2-156">复制应用设计方案所需的组件 (例如按钮或切换) 。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-156">Copy the components you need for your app design (for example, a button or toggle).</span></span>

## <a name="implement-your-design"></a><span data-ttu-id="4b0c2-157">实现你的设计</span><span class="sxs-lookup"><span data-stu-id="4b0c2-157">Implement your design</span></span>

<span data-ttu-id="4b0c2-158">设计已完成，你已准备好开始构建。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-158">The design is done and you’re ready to start building.</span></span> <span data-ttu-id="4b0c2-159">以下工具有助于简化应用的前端开发。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-159">The following tools can help simplify the front-end development of your app.</span></span>

### <a name="build-with-ui-templates"></a><span data-ttu-id="4b0c2-160">使用 UI 模板生成</span><span class="sxs-lookup"><span data-stu-id="4b0c2-160">Build with UI templates</span></span>

<span data-ttu-id="4b0c2-161">如果在设计中使用了 UI 模板，可以使用 Microsoft Teams UI 库实现这些模板 (Fluent UI React Fluent UI) 。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-161">If you used UI templates in your design, you can implement these templates with the Microsoft Teams UI Library (a React component library based on Fluent UI).</span></span>

<span data-ttu-id="4b0c2-162">目前，并非 UI 工具包中列出的所有模板在库中都可用。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-162">Currently, not all templates listed in the UI kit are available in the library.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4b0c2-163">获取库 (GitHub) </span><span class="sxs-lookup"><span data-stu-id="4b0c2-163">Get the library (GitHub)</span></span>](https://github.com/OfficeDev/microsoft-teams-ui-component-library)

### <a name="build-with-basic-ui-components"></a><span data-ttu-id="4b0c2-164">使用基本 UI 组件生成</span><span class="sxs-lookup"><span data-stu-id="4b0c2-164">Build with basic UI components</span></span>

<span data-ttu-id="4b0c2-165">与设计阶段不同，如果 UI 模板缺少你需要的内容，或者你只想从头开始构建应用，可以在应用项目中使用这些 Fluent UI 组件。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-165">Not unlike the design phase, you can use these Fluent UI components in your app project if a UI template is missing something you need, or you just want to build the app from scratch.</span></span> 

<span data-ttu-id="4b0c2-166"> (注意：如果你注意到缺少某些内容或对模板有一些想法，请考虑为Teams UI 库存储库) </span><span class="sxs-lookup"><span data-stu-id="4b0c2-166">(Note: If you notice something missing or have an idea for a template, consider contributing to the Teams UI Library repo.)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4b0c2-167">使用 Fluent UI (库) </span><span class="sxs-lookup"><span data-stu-id="4b0c2-167">Get the library (Fluent UI)</span></span>](https://fluentsite.z22.web.core.windows.net/)

## <a name="review-design-resources"></a><span data-ttu-id="4b0c2-168">查看设计资源</span><span class="sxs-lookup"><span data-stu-id="4b0c2-168">Review design resources</span></span>

<span data-ttu-id="4b0c2-169">无论你是刚开始使用应用还是接近生产就绪型应用，我们建议你定期查看以下资源：</span><span class="sxs-lookup"><span data-stu-id="4b0c2-169">Whether you’re just starting on your app or close to a production-ready app, we recommend that you periodically review the following resources:</span></span>

* <span data-ttu-id="4b0c2-170">**Microsoft Teams应用商店验证** 指南：提供所有Teams应用都应当努力 (应用商店中列出的应用) 。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-170">**Microsoft Teams store validation guidelines**: Provides standards that all Teams apps should strive for (not just apps listed in the store).</span></span> <span data-ttu-id="4b0c2-171">有关详细信息，请参阅 [指南](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-171">For more information, see the [guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).</span></span>
* <span data-ttu-id="4b0c2-172">**设计最佳做法**：这些文档和 UI 工具包提供了设计高质量应用的最佳方案。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-172">**Design best practices**: These docs and the UI kit provide best practices for designing high-quality apps.</span></span> <span data-ttu-id="4b0c2-173">例如，请参阅 [设计机器人的最佳实践](~/bots/design/bots.md#best-practices)。</span><span class="sxs-lookup"><span data-stu-id="4b0c2-173">For example, see the [best practices for designing bots](~/bots/design/bots.md#best-practices).</span></span>
