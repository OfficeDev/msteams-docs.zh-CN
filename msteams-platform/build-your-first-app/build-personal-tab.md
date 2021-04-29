---
title: 入门 - 生成个人选项卡
author: girliemac
description: 使用 Microsoft Teams 管理中心快速创建 Microsoft Teams 个人Toolkit。
ms.author: timura
ms.date: 03/16/2020
ms.topic: tutorial
ms.openlocfilehash: 05ef9913e338a54c7e6ebc301825b27d4bec9705
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068577"
---
# <a name="build-a-basic-personal-tab-for-microsoft-teams"></a><span data-ttu-id="b226f-103">为 Microsoft Teams 生成基本个人选项卡</span><span class="sxs-lookup"><span data-stu-id="b226f-103">Build a basic personal tab for Microsoft Teams</span></span>

<span data-ttu-id="b226f-104">本教程指导你在 Microsoft Teams 中生成基本个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="b226f-104">This tutorial teaches you to build a basic personal tab in Microsoft Teams.</span></span> <span data-ttu-id="b226f-105">选项卡是一种通过托管 Teams 中的 Web 内容在应用中显示信息的简单方法。</span><span class="sxs-lookup"><span data-stu-id="b226f-105">Tabs are a simple way to surface information in your app by hosting web content in Teams.</span></span> <span data-ttu-id="b226f-106">选项卡是个人应用的一项常见功能，可为各个用户提供专用工作区。</span><span class="sxs-lookup"><span data-stu-id="b226f-106">Tabs are a common feature of personal apps that provide a private workspace for individual users.</span></span> <span data-ttu-id="b226f-107">个人选项卡是最接近 Teams 中传统 Web 体验的内容。</span><span class="sxs-lookup"><span data-stu-id="b226f-107">Personal tabs are the closest thing to a traditional web experience in Teams.</span></span> 

## <a name="what-youll-learn"></a><span data-ttu-id="b226f-108">您将了解哪些功能</span><span class="sxs-lookup"><span data-stu-id="b226f-108">What you'll learn</span></span>

* <span data-ttu-id="b226f-109">了解与个人选项卡相关的应用配置和基架。</span><span class="sxs-lookup"><span data-stu-id="b226f-109">Understand the app configurations and scaffolding relevant to personal tabs.</span></span>
* <span data-ttu-id="b226f-110">使用组织的联系人列表创建选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="b226f-110">Create a tab content with a contact list of your organization.</span></span>
* <span data-ttu-id="b226f-111">根据用户首选项更新选项卡的颜色主题。</span><span class="sxs-lookup"><span data-stu-id="b226f-111">Update a tab's color theme based on user preference.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="b226f-112">先决条件</span><span class="sxs-lookup"><span data-stu-id="b226f-112">Prerequisites</span></span>

<span data-ttu-id="b226f-113">确保你了解如何设置和构建简单的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="b226f-113">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="b226f-114">有关详细信息，请参阅创建 [你的第一个 Microsoft Teams"Hello， World！"应用](../build-your-first-app/build-and-run.md)。</span><span class="sxs-lookup"><span data-stu-id="b226f-114">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-understand-your-app-project-components"></a><span data-ttu-id="b226f-115">1. 了解应用项目组件</span><span class="sxs-lookup"><span data-stu-id="b226f-115">1. Understand your app project components</span></span>

<span data-ttu-id="b226f-116">创建基本个人选项卡后，生成的应用基架提供在 Teams 中呈现个人选项卡的组件。</span><span class="sxs-lookup"><span data-stu-id="b226f-116">After you have created a basic personal tab, the generated app scaffold provides the components for rendering your personal tab in Teams.</span></span> <span data-ttu-id="b226f-117">可以使用许多方法，但现在让我们关注以下内容：</span><span class="sxs-lookup"><span data-stu-id="b226f-117">There's a lot you can work with, but for now let us focus on the following:</span></span> 

* <span data-ttu-id="b226f-118">`Tab.js` 文件 `src/components` 。</span><span class="sxs-lookup"><span data-stu-id="b226f-118">`Tab.js` file in the `src/components` directory of your project.</span></span> <span data-ttu-id="b226f-119">这用于呈现选项卡内容页。</span><span class="sxs-lookup"><span data-stu-id="b226f-119">This is for rendering your tab content page.</span></span>
* <span data-ttu-id="b226f-120">Microsoft Teams JavaScript 客户端 SDK，预加载到项目的前端组件中。</span><span class="sxs-lookup"><span data-stu-id="b226f-120">Microsoft Teams JavaScript client SDK, which is pre-loaded in your project's front-end components.</span></span>

<span data-ttu-id="b226f-121">正如您可能从文件顶部的部分注意到的，示例代码使用 React，这是一个开源 JavaScript 库，用于构建 `import` `Tabs.js` 用户界面。 [](https://reactjs.org/)</span><span class="sxs-lookup"><span data-stu-id="b226f-121">As you may notice from the `import` section at the top of `Tabs.js` file, the sample code uses [React](https://reactjs.org/), an open-source JavaScript library for building user-interface.</span></span> 

> [!NOTE]
> <span data-ttu-id="b226f-122">尽管 Teams _开发不需要_ 使用 React，但本教程将指导你使用 React。</span><span class="sxs-lookup"><span data-stu-id="b226f-122">Although using React is _not_ required for Teams development, this tutorial teaches you with React.</span></span>

## <a name="2-customize-your-tab-content-page"></a><span data-ttu-id="b226f-123">2. 自定义选项卡内容页</span><span class="sxs-lookup"><span data-stu-id="b226f-123">2. Customize your tab content page</span></span>

<span data-ttu-id="b226f-124">您可以自定义选项卡内容页，以呈现组织中的重要联系人列表。</span><span class="sxs-lookup"><span data-stu-id="b226f-124">You can customize your tab content page to render a list of important contacts in your organization.</span></span> 

<span data-ttu-id="b226f-125">**自定义选项卡内容页**</span><span class="sxs-lookup"><span data-stu-id="b226f-125">**To customize your tab content page**</span></span>

1. <span data-ttu-id="b226f-126">使用与自己相关的信息复制和修改以下代码示例。</span><span class="sxs-lookup"><span data-stu-id="b226f-126">Copy and modify the following code sample with information that's relevant to you.</span></span> <span data-ttu-id="b226f-127">也可以像现在一样使用代码：</span><span class="sxs-lookup"><span data-stu-id="b226f-127">You can also use the code as is:</span></span> 
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
1. <span data-ttu-id="b226f-128">到达 目录 `src/components` 并打开 `Tab.js` 文件。</span><span class="sxs-lookup"><span data-stu-id="b226f-128">Got to the `src/components` directory and open the `Tab.js` file.</span></span> 
1. <span data-ttu-id="b226f-129">转到 `render()` ，将模板代码替换为内部修改后的代码 `return()` ，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="b226f-129">Go to `render()` and replace the template code with the modified code inside `return()` as shown in the following example:</span></span>
    ```JavaScript
    render() {
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
1. <span data-ttu-id="b226f-130">转到 目录，并修改包含以下代码的文件，以便使用任何主题更轻松地阅读电子邮件 `src/components` `App.css` 链接：</span><span class="sxs-lookup"><span data-stu-id="b226f-130">Go to the `src/components` directory and modify the `App.css` file with the following code to make the email links easier to read with any theme that is used:</span></span>
    ```CSS
    a {
      color: inherit;
    }
    ```
1. <span data-ttu-id="b226f-131">保存所做的更改。</span><span class="sxs-lookup"><span data-stu-id="b226f-131">Save your changes.</span></span> 

   <span data-ttu-id="b226f-132">可以在 Teams 的应用选项卡中查看新内容。</span><span class="sxs-lookup"><span data-stu-id="b226f-132">You can view the new content in your app's tab in Teams.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-content.png" alt-text="包含静态内容的个人选项卡的屏幕截图。":::

## <a name="3-update-your-tab-theme"></a><span data-ttu-id="b226f-134">3. 更新选项卡主题</span><span class="sxs-lookup"><span data-stu-id="b226f-134">3. Update your tab theme</span></span>

<span data-ttu-id="b226f-135">对于选项卡来说，让主题感觉对于 Teams 来说很原生，这一点非常重要。</span><span class="sxs-lookup"><span data-stu-id="b226f-135">It is important for your tab to have a theme that feels native to Teams.</span></span> <span data-ttu-id="b226f-136">必须将选项卡与 Teams 主题混合。</span><span class="sxs-lookup"><span data-stu-id="b226f-136">You must blend your tab with the Teams theme.</span></span> <span data-ttu-id="b226f-137">用户通常首选默认 (浅) 、深色或高对比度主题。</span><span class="sxs-lookup"><span data-stu-id="b226f-137">Your users generally prefer default (light), dark, or high contrast themes.</span></span> <span data-ttu-id="b226f-138">正如你可能在上一张屏幕截图中注意到的，当用户使用深色主题时，选项卡仍具有浅色背景。</span><span class="sxs-lookup"><span data-stu-id="b226f-138">As you might have noticed in the last screenshot, your tab still has a light background when your user is using the dark theme.</span></span> <span data-ttu-id="b226f-139">这不是建议的用户体验。</span><span class="sxs-lookup"><span data-stu-id="b226f-139">This is not a recommended user experience.</span></span>

<span data-ttu-id="b226f-140">Teams JavaScript 客户端 SDK 可以使你的应用注意到和响应客户端中的主题更改。</span><span class="sxs-lookup"><span data-stu-id="b226f-140">The Teams JavaScript client SDK can make your app aware of and react to theme changes in the client.</span></span> <span data-ttu-id="b226f-141">为此，请按照下列步骤操作：</span><span class="sxs-lookup"><span data-stu-id="b226f-141">To do this, follow these steps:</span></span>

1. <span data-ttu-id="b226f-142">**获取有关已配置的 Teams 客户端主题的上下文** 在 `microsoftTeams.getContext()` 文件中调用 `Tab.js` ，可提供一些有关已配置的客户端主题 (的上下文，如深色主题) 。</span><span class="sxs-lookup"><span data-stu-id="b226f-142">**Get context about the configured Teams client theme** The `microsoftTeams.getContext()` call in your `Tab.js` file, provides some context about the configured client theme (such as dark theme).</span></span> <span data-ttu-id="b226f-143">以下代码访问 `context` 接口及其属性：</span><span class="sxs-lookup"><span data-stu-id="b226f-143">The following code accesses the `context` interface and its properties:</span></span>

    ```JavaScript
    componentDidMount(){
      // Get the user context from Teams and set it in the state
      microsoftTeams.getContext((context, error) => {
        this.setState({
          context: context,
          theme: context.theme
        });
      });
    }
    ```
1. <span data-ttu-id="b226f-144">**创建主题更改处理程序** 有了属性，你的应用可以深入了解 Teams 中 `context` 正在发生的情况。</span><span class="sxs-lookup"><span data-stu-id="b226f-144">**Create a theme change handler** With the `context` properties in hand, your app has a solid understanding of what's happening around it in Teams.</span></span> <span data-ttu-id="b226f-145">但是，当用户更新应用时，该应用的外观仍无法反映主题。</span><span class="sxs-lookup"><span data-stu-id="b226f-145">However, the app still doesn't have an appearance reflecting the theme when a user updates it.</span></span>

   <span data-ttu-id="b226f-146">你需要一个处理程序来使用主题更新应用的状态。</span><span class="sxs-lookup"><span data-stu-id="b226f-146">You need a handler to update your app's state with the theme.</span></span> <span data-ttu-id="b226f-147">若要创建处理程序，在调用后立即插入以下主题更改 `microsoftTeams.getContext()` 处理程序：</span><span class="sxs-lookup"><span data-stu-id="b226f-147">To create a handler, insert the following theme change handler immediately after the `microsoftTeams.getContext()` call:</span></span>

    ```JavaScript
    microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.context.theme) {
    this.setState({
      context: {
      ...this.state.context,
      theme
      }
      })   
      }
    });
      ```
1. <span data-ttu-id="b226f-148">**匹配主题样式** 主题更改处理程序已就位，但仍必须响应更改，将选项卡的颜色与当前主题保持一致。</span><span class="sxs-lookup"><span data-stu-id="b226f-148">**Match the theme styles** Your theme change handler is in place, however, you still have to respond to changes and align your tab's colors with the current theme.</span></span>

   <span data-ttu-id="b226f-149">在 `render()` 函数中，将主题更改处理程序提供的状态存储在 `isTheme` 中：</span><span class="sxs-lookup"><span data-stu-id="b226f-149">In the `render()` function, store the state provided by the theme change handler in `isTheme`:</span></span>

    ```JavaScript
      const isTheme = this.state.context.theme
    ```
    
    > [!NOTE]
    > <span data-ttu-id="b226f-150">本示例只是一种将样式应用到选项卡的方法。像现在一样使用代码，展开它，或编写你自己的代码。</span><span class="sxs-lookup"><span data-stu-id="b226f-150">This example is just one way you might apply styles to your tab. Use the code as is, expand on it, or write your own.</span></span>

    <span data-ttu-id="b226f-151">存储主题更改处理程序提供的状态后，提供条件逻辑以根据当前主题呈现选项卡的样式。</span><span class="sxs-lookup"><span data-stu-id="b226f-151">After storing the state provided by the theme change handler, provide the conditional logic to render your tab's styles based on the current theme.</span></span> <span data-ttu-id="b226f-152">以下示例演示了执行此操作的基本方法：</span><span class="sxs-lookup"><span data-stu-id="b226f-152">The following example shows a basic way to do this:</span></span>

    1. <span data-ttu-id="b226f-153">转到 `render()` 并检查 中的当前主题 `isTheme` 。</span><span class="sxs-lookup"><span data-stu-id="b226f-153">Go to `render()` and check the current theme in `isTheme`.</span></span>
    1. <span data-ttu-id="b226f-154">使用 `newTheme` 与当前主题相关的 CSS 属性创建对象。</span><span class="sxs-lookup"><span data-stu-id="b226f-154">Create a `newTheme` object with CSS properties relevant to the current theme.</span></span>
    1. <span data-ttu-id="b226f-155">将以下 CSS 应用到选项卡内容的根 HTML 元素 `<div style={newTheme}>` () ：</span><span class="sxs-lookup"><span data-stu-id="b226f-155">Apply the following CSS to your tab content's root HTML element (`<div style={newTheme}>`):</span></span>

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

       <span data-ttu-id="b226f-156">在 Teams 中查看你的选项卡。</span><span class="sxs-lookup"><span data-stu-id="b226f-156">Check your tab in Teams.</span></span> <span data-ttu-id="b226f-157">外观现在与深色主题紧密匹配。</span><span class="sxs-lookup"><span data-stu-id="b226f-157">The appearance now closely matches the dark theme.</span></span>

       :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-updated-theme.png" alt-text="具有静态内容视图的个人选项卡的屏幕截图。":::

## <a name="see-also"></a><span data-ttu-id="b226f-159">另请参阅</span><span class="sxs-lookup"><span data-stu-id="b226f-159">See also</span></span>

* [<span data-ttu-id="b226f-160">团队 JavaScript 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="b226f-160">Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="b226f-161">为 Microsoft Teams 桌面和 Web 设计选项卡</span><span class="sxs-lookup"><span data-stu-id="b226f-161">Designing your tab for Microsoft Teams desktop and web</span></span>](../tabs/design/tabs.md) 
* [<span data-ttu-id="b226f-162">上下文接口</span><span class="sxs-lookup"><span data-stu-id="b226f-162">Context interface</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)
* [<span data-ttu-id="b226f-163">使用 UI 模板设计 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="b226f-163">Designing your Microsoft Teams app with UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="b226f-164">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="b226f-164">Tabs on mobile</span></span>](../tabs/design/tabs-mobile.md)
* [<span data-ttu-id="b226f-165">单一登录 (SSO) 选项卡支持</span><span class="sxs-lookup"><span data-stu-id="b226f-165">Single sign-on (SSO) support for tabs</span></span>](../tabs/how-to/authentication/auth-aad-sso.md)
* [<span data-ttu-id="b226f-166">Microsoft Teams API 概述</span><span class="sxs-lookup"><span data-stu-id="b226f-166">Microsoft Teams API overview</span></span>](https://docs.microsoft.com/graph/teams-concept-overview)
* [<span data-ttu-id="b226f-167">使用 Microsoft Teams Node.js Yeoman 生成器创建自定义个人选项卡</span><span class="sxs-lookup"><span data-stu-id="b226f-167">Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a><span data-ttu-id="b226f-168">后续步骤</span><span class="sxs-lookup"><span data-stu-id="b226f-168">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b226f-169">创建频道选项卡</span><span class="sxs-lookup"><span data-stu-id="b226f-169">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)