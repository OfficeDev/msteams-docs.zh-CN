---
title: 入门 - 生成个人选项卡
author: heath-hamilton
description: 使用 Microsoft Teams 管理中心快速创建 Microsoft Teams 个人Toolkit。
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: dabe427142dd3e6a1d2f01f83601cbffd4a20dbd
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019977"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a><span data-ttu-id="bb081-103">为 Microsoft Teams 生成个人选项卡</span><span class="sxs-lookup"><span data-stu-id="bb081-103">Build a personal tab for Microsoft Teams</span></span>

<span data-ttu-id="bb081-104">选项卡是在 Teams 中嵌入网页，在应用中显示内容的一种简单方法。</span><span class="sxs-lookup"><span data-stu-id="bb081-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="bb081-105">Teams 中具有两种类型的选项卡。</span><span class="sxs-lookup"><span data-stu-id="bb081-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="bb081-106">在本教程中，你将生成基本的个人 *选项卡*，即单个用户的全屏内容页。</span><span class="sxs-lookup"><span data-stu-id="bb081-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="bb081-107"> (个人选项卡是最接近 Teams.) </span><span class="sxs-lookup"><span data-stu-id="bb081-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="bb081-108">开始之前</span><span class="sxs-lookup"><span data-stu-id="bb081-108">Before you begin</span></span>

<span data-ttu-id="bb081-109">你需要一个基本的正在运行的个人选项卡才能开始。</span><span class="sxs-lookup"><span data-stu-id="bb081-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="bb081-110">如果你没有，请参阅生成并运行 [你的第一个 Teams 应用](../build-your-first-app/build-and-run.md)。</span><span class="sxs-lookup"><span data-stu-id="bb081-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="bb081-111">您的工作分配</span><span class="sxs-lookup"><span data-stu-id="bb081-111">Your assignment</span></span>

<span data-ttu-id="bb081-112">您的组织中的人员在查找重要职能的基本联系信息时 (技术支持、人力资源等) 。</span><span class="sxs-lookup"><span data-stu-id="bb081-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="bb081-113">你负责确保他们可以在一个地方快速找到此信息。</span><span class="sxs-lookup"><span data-stu-id="bb081-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="bb081-114">如何执行这些工作？</span><span class="sxs-lookup"><span data-stu-id="bb081-114">How would you do that?</span></span> <span data-ttu-id="bb081-115">当然，Teams 个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="bb081-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="bb081-116">您将了解哪些功能</span><span class="sxs-lookup"><span data-stu-id="bb081-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="bb081-117">确定一些与个人选项卡相关的应用配置和基架</span><span class="sxs-lookup"><span data-stu-id="bb081-117">Identify some of the app configurations and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="bb081-118">创建选项卡内容</span><span class="sxs-lookup"><span data-stu-id="bb081-118">Create tab content</span></span>
> * <span data-ttu-id="bb081-119">根据用户首选项更新选项卡的颜色主题</span><span class="sxs-lookup"><span data-stu-id="bb081-119">Update a tab's color theme based on user preference</span></span>

## <a name="1-identify-relevant-app-project-components"></a><span data-ttu-id="bb081-120">1. 确定相关的应用项目组件</span><span class="sxs-lookup"><span data-stu-id="bb081-120">1. Identify relevant app project components</span></span>

<span data-ttu-id="bb081-121">当你使用 Teams 解决方案创建项目时，许多应用配置和基架会自动Toolkit。</span><span class="sxs-lookup"><span data-stu-id="bb081-121">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="bb081-122">让我们看一下生成个人选项卡的主要组件。</span><span class="sxs-lookup"><span data-stu-id="bb081-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="bb081-123">应用配置</span><span class="sxs-lookup"><span data-stu-id="bb081-123">App configurations</span></span>

<span data-ttu-id="bb081-124">在工具包中，转到 **App Studio** 以查看和更新应用配置。</span><span class="sxs-lookup"><span data-stu-id="bb081-124">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="bb081-125">应用基架</span><span class="sxs-lookup"><span data-stu-id="bb081-125">App scaffolding</span></span>

<span data-ttu-id="bb081-126">应用基架提供在 Teams 中呈现个人选项卡的组件。</span><span class="sxs-lookup"><span data-stu-id="bb081-126">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="bb081-127">你可以处理很多项目，但现在你只需关注以下内容：</span><span class="sxs-lookup"><span data-stu-id="bb081-127">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="bb081-128">`Tab.js` 文件 `src/components` 。</span><span class="sxs-lookup"><span data-stu-id="bb081-128">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="bb081-129">这用于呈现选项卡内容页。</span><span class="sxs-lookup"><span data-stu-id="bb081-129">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="bb081-130">Microsoft Teams JavaScript 客户端 SDK，预加载到项目的前端组件中。</span><span class="sxs-lookup"><span data-stu-id="bb081-130">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="bb081-131">2. 自定义选项卡内容页</span><span class="sxs-lookup"><span data-stu-id="bb081-131">2. Customize your tab content page</span></span>

<span data-ttu-id="bb081-132">编译组织中重要联系人的列表。</span><span class="sxs-lookup"><span data-stu-id="bb081-132">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="bb081-133">复制以下代码段，并使用与自己相关的信息进行更新，或者出于时间考虑，按如下所示使用代码。</span><span class="sxs-lookup"><span data-stu-id="bb081-133">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

```JSX
<div>
  <h1>Important Contacts</h1>
    <ul>
      <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
      <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
      <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
    </ul>
</div>
```

<span data-ttu-id="bb081-134">转到 目录 `src/components` 并打开 `Tab.js` 。</span><span class="sxs-lookup"><span data-stu-id="bb081-134">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="bb081-135">找到 `render()` 函数，然后将内容粘贴到 `return()` (，如) 。</span><span class="sxs-lookup"><span data-stu-id="bb081-135">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

```JavaScript
render() {

    let userName = Object.keys(this.state.context).length > 0 ? this.state.context['upn'] : "";

    return (
    <div>
      <h1>Important Contacts</h1>
        <ul>
          <li>Help Desk: <a href="mailto:support@company.com">support@company.com</a></li>
          <li>Human Resources: <a href="mailto:hr@company.com">hr@company.com</a></li>
          <li>Facilities: <a href="mailto:facilities@company.com">facilities@company.com</a></li>
        </ul>
    </div>
    );
}
```

<span data-ttu-id="bb081-136">将以下规则添加到 ，以便无论使用哪个主题，电子邮件 `App.css` 链接都更易于阅读。</span><span class="sxs-lookup"><span data-stu-id="bb081-136">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

<span data-ttu-id="bb081-137">保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="bb081-137">Save your changes.</span></span> <span data-ttu-id="bb081-138">转到 Teams 中你的应用选项卡以查看新内容。</span><span class="sxs-lookup"><span data-stu-id="bb081-138">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="包含静态内容的个人选项卡的屏幕截图。":::

## <a name="3-update-the-tab-theme"></a><span data-ttu-id="bb081-140">3. 更新选项卡主题</span><span class="sxs-lookup"><span data-stu-id="bb081-140">3. Update the tab theme</span></span>

<span data-ttu-id="bb081-141">良好的应用感觉是 Teams 的原生应用，因此选项卡与用户喜欢的 Teams 主题混合很重要：默认 (浅色) 、深色或高对比度。</span><span class="sxs-lookup"><span data-stu-id="bb081-141">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="bb081-142">正如你上次屏幕截图中所示，当客户端使用深色主题时，选项卡仍具有浅色背景。</span><span class="sxs-lookup"><span data-stu-id="bb081-142">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="bb081-143">这不是建议的用户体验。</span><span class="sxs-lookup"><span data-stu-id="bb081-143">This is not a recommended user experience.</span></span>

<span data-ttu-id="bb081-144">[Teams JavaScript 客户端 SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)可以使你的应用注意到和响应客户端中的主题更改。</span><span class="sxs-lookup"><span data-stu-id="bb081-144">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="bb081-145">让我们演练一下如何这样做。</span><span class="sxs-lookup"><span data-stu-id="bb081-145">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="bb081-146">获取 Teams 客户端的上下文</span><span class="sxs-lookup"><span data-stu-id="bb081-146">Get context about the Teams client</span></span>

<span data-ttu-id="bb081-147">在你的文件中，有一个调用提供了配置的客户端主题的一 `Tab.js` `microsoftTeams.getContext()` [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) 些信息以及其他详细信息。</span><span class="sxs-lookup"><span data-stu-id="bb081-147">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="bb081-148">借助应用基架，使用此代码，就像访问 `context` 接口及其属性一样。</span><span class="sxs-lookup"><span data-stu-id="bb081-148">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

```JavaScript
componentDidMount(){
  // Get the user context from Teams and set it in the state
  microsoftTeams.getContext((context, error) => {
    this.setState({
      context: context
    });
  });
  // Next steps: Error handling using the error object
}
```

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="bb081-149">创建主题更改处理程序</span><span class="sxs-lookup"><span data-stu-id="bb081-149">Create a theme change handler</span></span>

<span data-ttu-id="bb081-150">有了属性，你的应用可以深入了解 Teams 中 `context` 正在发生的情况。</span><span class="sxs-lookup"><span data-stu-id="bb081-150">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="bb081-151">但是应用仍不知道它的外观应反映用户选择的主题。</span><span class="sxs-lookup"><span data-stu-id="bb081-151">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="bb081-152">你需要一个处理程序，以便应用的状态随主题一起更改。</span><span class="sxs-lookup"><span data-stu-id="bb081-152">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="bb081-153">在调用后立即插入以下主题更改 `microsoftTeams.getContext()` 处理程序。</span><span class="sxs-lookup"><span data-stu-id="bb081-153">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="bb081-154">匹配主题样式</span><span class="sxs-lookup"><span data-stu-id="bb081-154">Match theme styles</span></span>

<span data-ttu-id="bb081-155">主题更改处理程序已就位，但需要一些代码来响应这些更改，使选项卡的颜色与当前主题保持一致。</span><span class="sxs-lookup"><span data-stu-id="bb081-155">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="bb081-156">以下示例只是一种将样式应用到选项卡的方法。像现在一样使用代码，展开它，或编写你自己的代码。</span><span class="sxs-lookup"><span data-stu-id="bb081-156">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="bb081-157">在 `render()` 函数中，将主题更改处理程序提供的状态存储在 中 `isTheme` 。</span><span class="sxs-lookup"><span data-stu-id="bb081-157">In the `render()` function, store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="bb081-158">存储主题更改处理程序提供的状态后，提供一些条件逻辑以根据当前主题呈现选项卡的样式。</span><span class="sxs-lookup"><span data-stu-id="bb081-158">After storing the state provided by the theme change handler, provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="bb081-159">以下示例演示了执行此操作的基本方法：</span><span class="sxs-lookup"><span data-stu-id="bb081-159">The following example shows a basic way to do this:</span></span>
1. <span data-ttu-id="bb081-160">检查 中的当前主题 `isTheme` 。</span><span class="sxs-lookup"><span data-stu-id="bb081-160">Check the current theme in `isTheme`.</span></span>
2. <span data-ttu-id="bb081-161">使用 `newTheme` 与当前主题相关的 CSS 属性创建对象。</span><span class="sxs-lookup"><span data-stu-id="bb081-161">Create a `newTheme` object with CSS properties relevant to the current theme.</span></span>
3. <span data-ttu-id="bb081-162">将 CSS 应用到选项卡内容的根 HTML 元素 `<div style={newTheme}>` () 。</span><span class="sxs-lookup"><span data-stu-id="bb081-162">Apply the CSS to your tab content's root HTML element (`<div style={newTheme}>`).</span></span>

```JavaScript
let newTheme

if (isTheme === "default") {
  newTheme = {
    backgroundColor: "#EEF1F5",
    color: "#16233A"
  };
} else {
  newTheme = {
    backgroundColor: "#2B2B30",
    color: "#FFFFFF"
  };
}
```

<span data-ttu-id="bb081-163">在 Teams 中查看你的选项卡。</span><span class="sxs-lookup"><span data-stu-id="bb081-163">Check your tab in Teams.</span></span> <span data-ttu-id="bb081-164">外观应该与深色主题紧密匹配。</span><span class="sxs-lookup"><span data-stu-id="bb081-164">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="具有静态内容视图的个人选项卡的屏幕截图。":::

## <a name="well-done"></a><span data-ttu-id="bb081-166">干的好</span><span class="sxs-lookup"><span data-stu-id="bb081-166">Well done</span></span>

<span data-ttu-id="bb081-167">恭喜！</span><span class="sxs-lookup"><span data-stu-id="bb081-167">Congratulations!</span></span> <span data-ttu-id="bb081-168">你拥有具有个人选项卡的 Teams 应用，可更轻松地查找组织中的重要联系人。</span><span class="sxs-lookup"><span data-stu-id="bb081-168">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="bb081-169">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="bb081-169">Learn more</span></span>

* <span data-ttu-id="bb081-170">遵循 [我们的设计指南](../tabs/design/tabs.md) ，使用生产就绪 [UI](../concepts/design/design-teams-app-ui-templates.md) 模板构建，以创建无缝体验。</span><span class="sxs-lookup"><span data-stu-id="bb081-170">Follow our [design guidelines](../tabs/design/tabs.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* <span data-ttu-id="bb081-171">了解 [选项卡的移动](../tabs/design/tabs-mobile.md) 注意事项。</span><span class="sxs-lookup"><span data-stu-id="bb081-171">Understand [mobile considerations](../tabs/design/tabs-mobile.md) for tabs.</span></span>
* <span data-ttu-id="bb081-172">[将 SSO 身份验证添加到选项卡](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="bb081-172">[Add SSO authentication to your tab](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>
* <span data-ttu-id="bb081-173">通过 Microsoft [Graph](https://docs.microsoft.com/graph/teams-concept-overview)利用 Teams 数据。</span><span class="sxs-lookup"><span data-stu-id="bb081-173">Utilize Teams data with [Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>
* <span data-ttu-id="bb081-174">[创建不带工具包 的选项卡](../tabs/quickstarts/create-personal-tab-node-yeoman.md)。</span><span class="sxs-lookup"><span data-stu-id="bb081-174">[Create a tab without the toolkit](../tabs/quickstarts/create-personal-tab-node-yeoman.md).</span></span>

## <a name="next-lesson"></a><span data-ttu-id="bb081-175">下一课程</span><span class="sxs-lookup"><span data-stu-id="bb081-175">Next lesson</span></span>

<span data-ttu-id="bb081-176">你知道如何生成供个人使用的选项卡。</span><span class="sxs-lookup"><span data-stu-id="bb081-176">You know how to build a tab for personal use.</span></span> <span data-ttu-id="bb081-177">让我们看一下为团队频道和聊天构建选项卡需要哪些内容。</span><span class="sxs-lookup"><span data-stu-id="bb081-177">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="bb081-178">创建频道选项卡</span><span class="sxs-lookup"><span data-stu-id="bb081-178">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
