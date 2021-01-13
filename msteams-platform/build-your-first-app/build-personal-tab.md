---
title: 入门 - 生成个人选项卡
author: heath-hamilton
description: 使用 Microsoft Teams Toolkit 快速创建 Microsoft Teams 个人Toolkit。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: 86be39503ec4e4fde5fafe63f83b3a4fb6d956bf
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797804"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a><span data-ttu-id="fced3-103">为 Microsoft Teams 生成个人选项卡</span><span class="sxs-lookup"><span data-stu-id="fced3-103">Build a personal tab for Microsoft Teams</span></span>

<span data-ttu-id="fced3-104">通过本质上在 Teams 中嵌入网页，选项卡是显示应用中内容的一种简单方法。</span><span class="sxs-lookup"><span data-stu-id="fced3-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="fced3-105">Teams 中具有两种类型的选项卡。</span><span class="sxs-lookup"><span data-stu-id="fced3-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="fced3-106">在本教程中，你将生成基本的个人 *选项卡*，一个适用于单个用户的全屏内容页。</span><span class="sxs-lookup"><span data-stu-id="fced3-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="fced3-107"> (个人选项卡是最接近 Teams.) </span><span class="sxs-lookup"><span data-stu-id="fced3-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fced3-108">准备工作</span><span class="sxs-lookup"><span data-stu-id="fced3-108">Before you begin</span></span>

<span data-ttu-id="fced3-109">你需要一个基本的运行个人选项卡才能开始。</span><span class="sxs-lookup"><span data-stu-id="fced3-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="fced3-110">如果你没有，请参阅生成并 [运行你的第一个 Teams 应用](../build-your-first-app/build-and-run.md)。</span><span class="sxs-lookup"><span data-stu-id="fced3-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="fced3-111">你的作业</span><span class="sxs-lookup"><span data-stu-id="fced3-111">Your assignment</span></span>

<span data-ttu-id="fced3-112">您的组织中的人员在查找重要功能的基本联系信息时 (技术支持、人力资源等) 。</span><span class="sxs-lookup"><span data-stu-id="fced3-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="fced3-113">你负责确保他们可以在一个地方快速找到此信息。</span><span class="sxs-lookup"><span data-stu-id="fced3-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="fced3-114">如何执行？</span><span class="sxs-lookup"><span data-stu-id="fced3-114">How would you do that?</span></span> <span data-ttu-id="fced3-115">当然，Teams 个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="fced3-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="fced3-116">您将了解哪些知识</span><span class="sxs-lookup"><span data-stu-id="fced3-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="fced3-117">确定一些与个人选项卡相关的应用配置和基架</span><span class="sxs-lookup"><span data-stu-id="fced3-117">Identify some of the app configurations and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="fced3-118">创建选项卡内容</span><span class="sxs-lookup"><span data-stu-id="fced3-118">Create tab content</span></span>
> * <span data-ttu-id="fced3-119">根据用户首选项更新选项卡的颜色主题</span><span class="sxs-lookup"><span data-stu-id="fced3-119">Update a tab's color theme based on user preference</span></span>

## <a name="1-identify-relevant-app-project-components"></a><span data-ttu-id="fced3-120">1. 确定相关应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="fced3-120">1. Identify relevant app project components</span></span>

<span data-ttu-id="fced3-121">使用 Teams 解决方案创建项目时，会自动设置大部分应用配置和基架Toolkit。</span><span class="sxs-lookup"><span data-stu-id="fced3-121">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="fced3-122">让我们看一下生成个人选项卡的主要组件。</span><span class="sxs-lookup"><span data-stu-id="fced3-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="fced3-123">应用配置</span><span class="sxs-lookup"><span data-stu-id="fced3-123">App configurations</span></span>

<span data-ttu-id="fced3-124">在工具包中，转到 **App Studio** 以查看和更新应用配置。</span><span class="sxs-lookup"><span data-stu-id="fced3-124">In the toolkit, go to **App Studio** to view and update your app configurations.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="fced3-125">应用基架</span><span class="sxs-lookup"><span data-stu-id="fced3-125">App scaffolding</span></span>

<span data-ttu-id="fced3-126">应用基架提供在 Teams 中呈现个人选项卡的组件。</span><span class="sxs-lookup"><span data-stu-id="fced3-126">The app scaffolding provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="fced3-127">可以使用许多方法，但目前只需关注以下内容：</span><span class="sxs-lookup"><span data-stu-id="fced3-127">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="fced3-128">`Tab.js` 文件 `src/components` 。</span><span class="sxs-lookup"><span data-stu-id="fced3-128">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="fced3-129">这用于呈现选项卡内容页。</span><span class="sxs-lookup"><span data-stu-id="fced3-129">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="fced3-130">Microsoft Teams JavaScript 客户端 SDK，预加载到项目的前端组件中。</span><span class="sxs-lookup"><span data-stu-id="fced3-130">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="fced3-131">2. 自定义选项卡内容页</span><span class="sxs-lookup"><span data-stu-id="fced3-131">2. Customize your tab content page</span></span>

<span data-ttu-id="fced3-132">编译组织中重要联系人的列表。</span><span class="sxs-lookup"><span data-stu-id="fced3-132">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="fced3-133">复制并更新以下代码段，并包含与自己相关的信息，或者出于时间考虑，按如下所示使用代码。</span><span class="sxs-lookup"><span data-stu-id="fced3-133">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="fced3-134">转到 `src/components` 目录并打开 `Tab.js` 。</span><span class="sxs-lookup"><span data-stu-id="fced3-134">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="fced3-135">找到 `render()` 该函数，然后将内容粘贴到 `return()` (，如下所示) 。</span><span class="sxs-lookup"><span data-stu-id="fced3-135">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="fced3-136">添加以下规则，以便无论使用哪个主题，电子邮件 `App.css` 链接都更易于阅读。</span><span class="sxs-lookup"><span data-stu-id="fced3-136">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

<span data-ttu-id="fced3-137">保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="fced3-137">Save your changes.</span></span> <span data-ttu-id="fced3-138">转到 Teams 中你的应用的选项卡以查看新内容。</span><span class="sxs-lookup"><span data-stu-id="fced3-138">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="包含静态内容的个人选项卡的屏幕截图。":::

## <a name="3-update-the-tab-theme"></a><span data-ttu-id="fced3-140">3. 更新选项卡主题</span><span class="sxs-lookup"><span data-stu-id="fced3-140">3. Update the tab theme</span></span>

<span data-ttu-id="fced3-141">良好的应用感觉与 Teams 本机一样，因此选项卡与用户喜欢的 Teams 主题混合很重要：默认 (浅色) 、深色或高对比度。</span><span class="sxs-lookup"><span data-stu-id="fced3-141">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="fced3-142">正如你可能在上一张屏幕截图中注意到的，当客户端使用深色主题时，选项卡仍具有浅色背景。</span><span class="sxs-lookup"><span data-stu-id="fced3-142">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="fced3-143">这不是建议的用户体验。</span><span class="sxs-lookup"><span data-stu-id="fced3-143">This is not a recommended user experience.</span></span>

<span data-ttu-id="fced3-144">[Teams JavaScript 客户端 SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)可以使你的应用注意到和响应客户端中的主题更改。</span><span class="sxs-lookup"><span data-stu-id="fced3-144">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="fced3-145">让我们演练一下如何完成此操作。</span><span class="sxs-lookup"><span data-stu-id="fced3-145">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="fced3-146">获取有关 Teams 客户端的上下文</span><span class="sxs-lookup"><span data-stu-id="fced3-146">Get context about the Teams client</span></span>

<span data-ttu-id="fced3-147">在你的 `Tab.js` 文件中，有一个调用提供有关配置的客户端主题的一些信息，以及其他 `microsoftTeams.getContext()` [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) 详细信息。</span><span class="sxs-lookup"><span data-stu-id="fced3-147">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="fced3-148">由于应用基架，因此使用此代码即会访问 `context` 接口及其属性。</span><span class="sxs-lookup"><span data-stu-id="fced3-148">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

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

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="fced3-149">创建主题更改处理程序</span><span class="sxs-lookup"><span data-stu-id="fced3-149">Create a theme change handler</span></span>

<span data-ttu-id="fced3-150">有了属性，你的应用可以深入了解 Teams `context` 中围绕它发生的情况。</span><span class="sxs-lookup"><span data-stu-id="fced3-150">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="fced3-151">但应用仍然不知道其外观应反映用户选择的主题。</span><span class="sxs-lookup"><span data-stu-id="fced3-151">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="fced3-152">你需要一个处理程序，以便应用的状态随主题一起更改。</span><span class="sxs-lookup"><span data-stu-id="fced3-152">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="fced3-153">在调用后立即插入以下主题更改 `microsoftTeams.getContext()` 处理程序。</span><span class="sxs-lookup"><span data-stu-id="fced3-153">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="fced3-154">匹配主题样式</span><span class="sxs-lookup"><span data-stu-id="fced3-154">Match theme styles</span></span>

<span data-ttu-id="fced3-155">主题更改处理程序已就位，但你需要一些代码来响应这些更改，并对齐选项卡的颜色与当前主题。</span><span class="sxs-lookup"><span data-stu-id="fced3-155">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="fced3-156">以下示例只是将样式应用到选项卡的一种方式。像现在一样使用代码，展开它，或编写你自己的代码。</span><span class="sxs-lookup"><span data-stu-id="fced3-156">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="fced3-157">在 `render()` 函数中，将主题更改处理程序提供的状态存储在中 `isTheme` 。</span><span class="sxs-lookup"><span data-stu-id="fced3-157">In the `render()` function, store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="fced3-158">存储主题更改处理程序提供的状态后，提供一些条件逻辑以根据当前主题呈现选项卡的样式。</span><span class="sxs-lookup"><span data-stu-id="fced3-158">After storing the state provided by the theme change handler, provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="fced3-159">以下示例演示了一种基本方法：</span><span class="sxs-lookup"><span data-stu-id="fced3-159">The following example shows a basic way to do this:</span></span>
1. <span data-ttu-id="fced3-160">检查中的当前主题 `isTheme` 。</span><span class="sxs-lookup"><span data-stu-id="fced3-160">Check the current theme in `isTheme`.</span></span>
2. <span data-ttu-id="fced3-161">使用 `newTheme` 与当前主题相关的 CSS 属性创建对象。</span><span class="sxs-lookup"><span data-stu-id="fced3-161">Create a `newTheme` object with CSS properties relevant to the current theme.</span></span>
3. <span data-ttu-id="fced3-162">将 CSS 应用到选项卡内容的根 HTML 元素 `<div>` () 。</span><span class="sxs-lookup"><span data-stu-id="fced3-162">Apply the CSS to your tab content's root HTML element (`<div>`).</span></span>

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

<span data-ttu-id="fced3-163">在 Teams 中查看你的选项卡。</span><span class="sxs-lookup"><span data-stu-id="fced3-163">Check your tab in Teams.</span></span> <span data-ttu-id="fced3-164">外观应该与深色主题紧密匹配。</span><span class="sxs-lookup"><span data-stu-id="fced3-164">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="具有静态内容视图的个人选项卡的屏幕截图。":::

## <a name="well-done"></a><span data-ttu-id="fced3-166">干的好</span><span class="sxs-lookup"><span data-stu-id="fced3-166">Well done</span></span>

<span data-ttu-id="fced3-167">恭喜！</span><span class="sxs-lookup"><span data-stu-id="fced3-167">Congratulations!</span></span> <span data-ttu-id="fced3-168">你拥有一个 Teams 应用，该应用具有个人选项卡，可更轻松地查找组织中的重要联系人。</span><span class="sxs-lookup"><span data-stu-id="fced3-168">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="fced3-169">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="fced3-169">Learn more</span></span>

* <span data-ttu-id="fced3-170">使用[SSO](../tabs/how-to/authentication/auth-aad-sso.md)对选项卡用户进行身份验证：如果仅希望授权用户查看选项卡，请通过 Azure Active Directory) AD (设置单一登录 (SSO) 。</span><span class="sxs-lookup"><span data-stu-id="fced3-170">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="fced3-171">[嵌入现有 Web](../tabs/how-to/tab-requirements.md)应用或网页中的内容：我们展示了如何为个人选项卡创建新内容，但您也可以从外部 URL 加载内容。</span><span class="sxs-lookup"><span data-stu-id="fced3-171">[Embed content from an existing web app or webpage](../tabs/how-to/tab-requirements.md): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="fced3-172">[为选项卡创建无缝体验](../tabs/design/tabs.md)：请参阅设计 Teams 选项卡的建议指南。</span><span class="sxs-lookup"><span data-stu-id="fced3-172">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="fced3-173">[构建适用于移动设备的选项卡](../tabs/design/tabs-mobile.md)：了解如何开发适用于手机和平板电脑的选项卡。</span><span class="sxs-lookup"><span data-stu-id="fced3-173">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="fced3-174">使用 Microsoft Graph 利用 Teams 数据</span><span class="sxs-lookup"><span data-stu-id="fced3-174">Utilize Teams data with Microsoft Graph</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="fced3-175">创建不带工具包的选项卡</span><span class="sxs-lookup"><span data-stu-id="fced3-175">Create a tab without the toolkit</span></span>](../tabs/quickstarts/create-channel-group-tab-node-yeoman.md)

## <a name="next-lesson"></a><span data-ttu-id="fced3-176">下一课程</span><span class="sxs-lookup"><span data-stu-id="fced3-176">Next lesson</span></span>

<span data-ttu-id="fced3-177">你知道如何生成供个人使用的选项卡。</span><span class="sxs-lookup"><span data-stu-id="fced3-177">You know how to build a tab for personal use.</span></span> <span data-ttu-id="fced3-178">让我们看一下为团队频道和聊天构建选项卡需要哪些内容。</span><span class="sxs-lookup"><span data-stu-id="fced3-178">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fced3-179">创建频道选项卡</span><span class="sxs-lookup"><span data-stu-id="fced3-179">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
