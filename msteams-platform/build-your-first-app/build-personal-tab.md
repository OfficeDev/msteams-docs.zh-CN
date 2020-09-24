---
title: 生成工作组个人选项卡
author: heath-hamilton
description: 了解如何为你的首个 Microsoft 团队应用构建个人选项卡。
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: tutorial
ms.openlocfilehash: a86c9e1e46b97c6b265bfa9ad2f618655c524ee4
ms.sourcegitcommit: f9a2f5cedc9d30ef7a9cf78a47d01cfd277e150d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2020
ms.locfileid: "48237802"
---
# <a name="build-a-teams-personal-tab"></a><span data-ttu-id="5e2e8-103">生成工作组个人选项卡</span><span class="sxs-lookup"><span data-stu-id="5e2e8-103">Build a Teams personal tab</span></span>

<span data-ttu-id="5e2e8-104">通过在团队中嵌入网页，选项卡是在应用程序中呈现内容的一种简单方法。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-104">Tabs are a simple way to surface content in your app by essentially embedding a webpage in Teams.</span></span>

<span data-ttu-id="5e2e8-105">团队中有两种类型的选项卡。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-105">There are two types of tabs in Teams.</span></span> <span data-ttu-id="5e2e8-106">在本教程中，将为单个用户构建基本的 *个人选项卡*（全屏内容页面）。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-106">In this tutorial, you'll build basic a *personal tab*, a full-screen content page for individual users.</span></span> <span data-ttu-id="5e2e8-107"> (个人选项卡是团队中的传统网站体验中最接近的内容。 ) </span><span class="sxs-lookup"><span data-stu-id="5e2e8-107">(Personal tabs are the closest thing to a traditional website experience in Teams.)</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5e2e8-108">准备工作</span><span class="sxs-lookup"><span data-stu-id="5e2e8-108">Before you begin</span></span>

<span data-ttu-id="5e2e8-109">若要开始，您需要 "运行一个基本的个人" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-109">You need a basic running personal tab to get started.</span></span> <span data-ttu-id="5e2e8-110">如果没有，请参阅 [生成并运行你的首个团队应用](../build-your-first-app/build-and-run.md)。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-110">If you don't have one, see [build and run your first Teams app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="5e2e8-111">您的分配</span><span class="sxs-lookup"><span data-stu-id="5e2e8-111">Your assignment</span></span>

<span data-ttu-id="5e2e8-112">组织中的人员在查找重要功能的基本联系人信息时遇到问题 (技术支持、人力资源等 ) 。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-112">People in your organization have trouble finding basic contact information for important functions (help desk, HR, etc.).</span></span> <span data-ttu-id="5e2e8-113">你需要确保他们能够在一个位置快速查找此信息。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-113">You're in charge of making sure they can quickly find this information in one place.</span></span> <span data-ttu-id="5e2e8-114">您该如何操作？</span><span class="sxs-lookup"><span data-stu-id="5e2e8-114">How would you do that?</span></span> <span data-ttu-id="5e2e8-115">当然是 "工作组个人" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-115">A Teams personal tab, of course.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="5e2e8-116">你将了解的内容</span><span class="sxs-lookup"><span data-stu-id="5e2e8-116">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="5e2e8-117">确定与个人选项卡相关的一些应用程序清单属性和基架</span><span class="sxs-lookup"><span data-stu-id="5e2e8-117">Identify some of the app manifest properties and scaffolding relevant to personal tabs</span></span>
> * <span data-ttu-id="5e2e8-118">创建选项卡内容</span><span class="sxs-lookup"><span data-stu-id="5e2e8-118">Create tab content</span></span>
> * <span data-ttu-id="5e2e8-119">根据用户首选项更新选项卡的颜色主题</span><span class="sxs-lookup"><span data-stu-id="5e2e8-119">Update a tab's color theme based on user preference</span></span>

## <a name="1-identify-relevant-app-project-components"></a><span data-ttu-id="5e2e8-120">1. 确定相关的应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="5e2e8-120">1. Identify relevant app project components</span></span>

<span data-ttu-id="5e2e8-121">大多数应用程序清单和基架是在使用团队工具包创建项目时自动设置的。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-121">Much of the app manifest and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="5e2e8-122">我们来看看用于构建个人选项卡的主要组件。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-122">Let's look at the main components for building a personal tab.</span></span>

### <a name="app-manifest"></a><span data-ttu-id="5e2e8-123">应用程序清单</span><span class="sxs-lookup"><span data-stu-id="5e2e8-123">App manifest</span></span>

<span data-ttu-id="5e2e8-124">应用程序清单中的以下代码片段 (`manifest.json` 项目目录中的文件 `.publish`) 显示 [`staticTabs`](../resources/schema/manifest-schema.md#statictabs) ，其中包括与个人选项卡相关的属性和默认值。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-124">The following snippet from the app manifest (the `manifest.json` file in your project's `.publish` directory) shows [`staticTabs`](../resources/schema/manifest-schema.md#statictabs), which includes properties and default values relevant to personal tabs.</span></span>

```JSON
"staticTabs": [
    {
        "entityId": "index",
        "name": "Personal Tab",
        "contentUrl": "{baseUrl0}/tab",
        "scopes": [ "personal" ]
    }
],
```

* <span data-ttu-id="5e2e8-125">`entityId`：选项卡显示的页面的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-125">`entityId`: A unique identifier for the page displayed by the tab.</span></span>
* <span data-ttu-id="5e2e8-126">`name`：该选项卡的显示名称 (例如，"我的联系人" ) 。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-126">`name`: The tab's display name (for example, "My Contacts").</span></span>
* <span data-ttu-id="5e2e8-127">`contentUrl`：主机 URL "选项卡内容" 页面 (必须是 HTTPS) 。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-127">`contentUrl`: The host URL the tab content page (must be HTTPS).</span></span>
* <span data-ttu-id="5e2e8-128">`scopes`：指定选项卡仅供个人使用。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-128">`scopes`: Specifies the tab is for personal use only.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="5e2e8-129">应用程序基架</span><span class="sxs-lookup"><span data-stu-id="5e2e8-129">App scaffolding</span></span>

<span data-ttu-id="5e2e8-130">应用程序基架提供用于在团队中呈现选项卡的组件。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-130">The app scaffolding provides the components for rendering your tab in Teams.</span></span> <span data-ttu-id="5e2e8-131">你可以使用很多，但现在你只需关注以下内容：</span><span class="sxs-lookup"><span data-stu-id="5e2e8-131">There's a lot you can work with, but for now you only need to focus on the following:</span></span>

* <span data-ttu-id="5e2e8-132">`Tab.js``src/components`项目目录中的文件</span><span class="sxs-lookup"><span data-stu-id="5e2e8-132">`Tab.js` file in the `src/components` directory of your project</span></span>
* <span data-ttu-id="5e2e8-133">Microsoft 团队 JavaScript 客户端 SDK，它在项目的前端组件中预加载</span><span class="sxs-lookup"><span data-stu-id="5e2e8-133">Microsoft Teams JavaScript client SDK, which comes pre-loaded in your project's front-end components</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="5e2e8-134">2. 自定义 "选项卡内容" 页</span><span class="sxs-lookup"><span data-stu-id="5e2e8-134">2. Customize your tab content page</span></span>

<span data-ttu-id="5e2e8-135">编译组织中重要联系人的列表。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-135">Compile a list of important contacts in your organization.</span></span> <span data-ttu-id="5e2e8-136">使用与您相关的信息复制和更新以下代码段，如果需要，请按如下所示使用代码。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-136">Copy and update the following snippet with information that's relevant to you or, for the sake of time, use the code as is.</span></span>

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

<span data-ttu-id="5e2e8-137">转到 `src/components` 目录并打开 `Tab.js` 。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-137">Go to the `src/components` directory and open `Tab.js`.</span></span> <span data-ttu-id="5e2e8-138">找到 `render()` 函数并将内容粘贴 (中， `return()` 如) 所示。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-138">Locate the `render()` function and paste your content inside `return()` (as shown).</span></span>

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

<span data-ttu-id="5e2e8-139">将以下规则添加到 `App.css` ，无论使用哪个主题，电子邮件链接更易于阅读。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-139">Add the following rule to `App.css` so the email links are easier to read no matter which theme is used.</span></span>

```CSS
a {
  color: inherit;
}
```

<span data-ttu-id="5e2e8-140">保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-140">Save your changes.</span></span> <span data-ttu-id="5e2e8-141">转到团队中的应用程序选项卡以查看新内容。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-141">Go to your app's tab in Teams to view the new content.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="包含静态内容的个人选项卡的屏幕截图。":::

## <a name="3-update-the-tab-theme"></a><span data-ttu-id="5e2e8-143">3. 更新选项卡主题</span><span class="sxs-lookup"><span data-stu-id="5e2e8-143">3. Update the tab theme</span></span>

<span data-ttu-id="5e2e8-144">理想的应用程序会让团队成为本地用户，因此，您的选项卡与您的用户喜欢的团队主题进行混合是很重要的：默认 (浅) 、深或高对比度。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-144">Good apps feel native to Teams, so it's important your tab blends with the Teams theme your users prefer: default (light), dark, or high contrast.</span></span> <span data-ttu-id="5e2e8-145">正如您可能在最后的屏幕截图中已注意到，当客户端使用深色主题时，您的选项卡仍有浅背景。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-145">As you might have noticed in the last screenshot, your tab still has a light background when the client's using the dark theme.</span></span> <span data-ttu-id="5e2e8-146">这不是建议的用户体验。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-146">This is not a recommended user experience.</span></span>

<span data-ttu-id="5e2e8-147">[团队 JavaScript 客户端 SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)可让你的应用程序知道和响应客户端中的主题更改。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-147">The [Teams JavaScript client SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true) can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="5e2e8-148">我们来演练一下如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-148">Let's walk through how to do this.</span></span>

### <a name="get-context-about-the-teams-client"></a><span data-ttu-id="5e2e8-149">获取有关团队客户端的上下文</span><span class="sxs-lookup"><span data-stu-id="5e2e8-149">Get context about the Teams client</span></span>

<span data-ttu-id="5e2e8-150">在您的文件中， `Tab.js` 有一个 `microsoftTeams.getContext()` 可提供 [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) 有关已配置的客户端主题的信息的呼叫。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-150">In your `Tab.js` file, there's a `microsoftTeams.getContext()` call that provides some [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest&preserve-view=true) about, among other details, the configured client theme.</span></span> <span data-ttu-id="5e2e8-151">由于应用程序基架，使用此代码来访问 `context` 接口及其属性。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-151">Thanks to the app scaffolding, use this code as is to access the `context` interface and its properties.</span></span>

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

### <a name="create-a-theme-change-handler"></a><span data-ttu-id="5e2e8-152">创建主题更改处理程序</span><span class="sxs-lookup"><span data-stu-id="5e2e8-152">Create a theme change handler</span></span>

<span data-ttu-id="5e2e8-153">使用这些 `context` 属性，您的应用程序可以清楚地了解团队中的 it 所发生的问题。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-153">With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="5e2e8-154">但是，应用仍不知道其外观应反映用户选择的任何主题。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-154">But the app still doesn't know its appearance should reflect whatever theme a user chooses.</span></span>

<span data-ttu-id="5e2e8-155">您需要处理程序，以便您的应用程序的状态随主题而更改。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-155">You need a handler so that your app's state changes with the theme.</span></span> <span data-ttu-id="5e2e8-156">在调用后立即插入以下主题更改处理程序 `microsoftTeams.getContext()` 。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-156">Insert the following theme change handler immediately after the `microsoftTeams.getContext()` call.</span></span>

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a><span data-ttu-id="5e2e8-157">匹配主题样式</span><span class="sxs-lookup"><span data-stu-id="5e2e8-157">Match theme styles</span></span>

<span data-ttu-id="5e2e8-158">您的主题更改处理程序已准备就绪，但您需要一些代码来响应这些更改，并将您的选项卡的颜色与当前主题对齐。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-158">Your theme change handler is in place, but you need some code that responds to those changes and aligns your tab's colors with the current theme.</span></span>

> [!NOTE]
> <span data-ttu-id="5e2e8-159">下面的示例只是将样式应用于选项卡的一种方法。使用的代码为，然后展开或编写自己的代码。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-159">The following example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

<span data-ttu-id="5e2e8-160">将主题更改处理程序提供的状态存储在中 `isTheme` 。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-160">Store the state provided by the theme change handler in `isTheme`.</span></span>

```JavaScript
  const isTheme = this.state.theme
```

<span data-ttu-id="5e2e8-161">提供一些条件逻辑，以根据当前主题呈现您的选项卡样式。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-161">Provide some conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="5e2e8-162">下面的示例展示了这样做的基本方法： 1) 检查中的当前主题 `isTheme` ，2) 使用与 `newTheme` 当前主题相关的 css 属性创建对象，3) 将 css 应用到您的选项卡内容的根 HTML 元素 (`<div>`) 。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-162">The following example shows a basic way to do this by 1) checking the current theme in `isTheme`, 2) creating a `newTheme` object with CSS properties relevant to the current theme, and 3) applying the CSS to your tab content's root HTML element (`<div>`).</span></span>

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

<span data-ttu-id="5e2e8-163">检查团队中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-163">Check your tab in Teams.</span></span> <span data-ttu-id="5e2e8-164">外观应与深色主题紧密匹配。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-164">The appearance should closely match the dark theme.</span></span>

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="包含静态内容视图的个人选项卡的屏幕截图。":::

## <a name="well-done"></a><span data-ttu-id="5e2e8-166">干的好</span><span class="sxs-lookup"><span data-stu-id="5e2e8-166">Well done</span></span>

<span data-ttu-id="5e2e8-167">恭喜你！</span><span class="sxs-lookup"><span data-stu-id="5e2e8-167">Congratulations!</span></span> <span data-ttu-id="5e2e8-168">您有一个 "个人" 选项卡的团队应用程序，可以更轻松地查找组织中的重要联系人。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-168">You have a Teams app with a personal tab that makes it easier to find important contacts in your organization.</span></span>

## <a name="learn-more"></a><span data-ttu-id="5e2e8-169">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="5e2e8-169">Learn more</span></span>

* <span data-ttu-id="5e2e8-170">[使用 Sso 对选项卡用户进行身份验证](../tabs/how-to/authentication/auth-aad-sso.md)：如果您仅希望授权用户查看您的选项卡，请通过 Azure Active DIRECTORY (AD) 设置单一登录 (SSO) 。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-170">[Authenticate tab users with SSO](../tabs/how-to/authentication/auth-aad-sso.md): If you only want authorized users viewing your tab, set up single sign-on (SSO) through Azure Active Directory (AD).</span></span>
* <span data-ttu-id="5e2e8-171">[从现有 web 应用或网页嵌入内容](../tabs/how-to/add-tab.md#tab-requirements)：我们向您介绍了如何为个人选项卡创建新内容，但您也可以从外部 URL 加载内容。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-171">[Embed content from an existing web app or webpage](../tabs/how-to/add-tab.md#tab-requirements): We showed you how to create new content for a personal tab, but you can also load content from an external URL.</span></span>
* <span data-ttu-id="5e2e8-172">[为您的选项卡创建无缝体验](../tabs/design/tabs.md)：有关设计团队选项卡的建议指南，请参阅。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-172">[Create a seamless experience for your tab](../tabs/design/tabs.md): See the recommended guidelines for designing Teams tabs.</span></span>
* <span data-ttu-id="5e2e8-173">[为移动设备构建选项卡](../tabs/design/tabs-mobile.md)：了解如何为电话和平板电脑开发选项卡。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-173">[Build tabs for mobile](../tabs/design/tabs-mobile.md): Understand how to develop tabs for phones and tablets.</span></span>
* [<span data-ttu-id="5e2e8-174">与 Microsoft Graph API 集成</span><span class="sxs-lookup"><span data-stu-id="5e2e8-174">Integrate with the Microsoft Graph API</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="5e2e8-175">创建不带工具箱的选项卡</span><span class="sxs-lookup"><span data-stu-id="5e2e8-175">Create a tab without the toolkit</span></span>](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a><span data-ttu-id="5e2e8-176">下一课</span><span class="sxs-lookup"><span data-stu-id="5e2e8-176">Next lesson</span></span>

<span data-ttu-id="5e2e8-177">您知道如何构建用于个人用途的选项卡。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-177">You know how to build a tab for personal use.</span></span> <span data-ttu-id="5e2e8-178">让我们来看看构建团队频道和聊天的选项卡所需的内容。</span><span class="sxs-lookup"><span data-stu-id="5e2e8-178">Let's look at what it takes to build a tab for team channels and chats.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5e2e8-179">生成通道选项卡</span><span class="sxs-lookup"><span data-stu-id="5e2e8-179">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
