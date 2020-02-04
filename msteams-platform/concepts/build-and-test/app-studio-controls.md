---
title: 使用控件库
description: 如何使用 Microsoft 团队应用程序 Studio 提供的控件库
keywords: 团队应用程序 Studio 控件库
ms.openlocfilehash: d817f55bd75216f77375b7848c5c32cbd29304c2
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673116"
---
# <a name="using-the-control-library-in-app-studio"></a><span data-ttu-id="cfe87-104">在应用程序 Studio 中使用控件库</span><span class="sxs-lookup"><span data-stu-id="cfe87-104">Using the control library in App Studio</span></span>

<span data-ttu-id="cfe87-105">[Microsoft 团队应用程序 Studio](~/get-started/get-started-app-studio.md)为你提供了一组可在你自己的应用程序中使用的控件。</span><span class="sxs-lookup"><span data-stu-id="cfe87-105">[Microsoft Teams App Studio](~/get-started/get-started-app-studio.md) provides you with a set of controls that you can use in your own apps.</span></span> <span data-ttu-id="cfe87-106">这些控件在应用程序 Studio 的 "*控件库*" 选项卡中提供。</span><span class="sxs-lookup"><span data-stu-id="cfe87-106">These controls are provided in the *Control Library* tab of App Studio.</span></span>

<span data-ttu-id="cfe87-107">这些控件由 Microsoft 团队设计人员创建，用于简化其自己的工作流，并对控件行为和支持团队的默认主题进行标准化。</span><span class="sxs-lookup"><span data-stu-id="cfe87-107">These controls were created by the Microsoft Teams designers to streamline their own workflows, standardize control behavior and support Team's default themes.</span></span> <span data-ttu-id="cfe87-108">您可以在自己的应用程序中使用此库来实现统一的外观和感觉。</span><span class="sxs-lookup"><span data-stu-id="cfe87-108">You can use this library in your own apps to achieve a unified look and feel.</span></span>

<span data-ttu-id="cfe87-109">控件包括：</span><span class="sxs-lookup"><span data-stu-id="cfe87-109">Controls include:</span></span>

* <span data-ttu-id="cfe87-110">按钮</span><span class="sxs-lookup"><span data-stu-id="cfe87-110">Buttons</span></span>
* <span data-ttu-id="cfe87-111">下拉</span><span class="sxs-lookup"><span data-stu-id="cfe87-111">Dropdowns</span></span>
* <span data-ttu-id="cfe87-112">复选框</span><span class="sxs-lookup"><span data-stu-id="cfe87-112">Checkboxes</span></span>
* <span data-ttu-id="cfe87-113">单选按钮</span><span class="sxs-lookup"><span data-stu-id="cfe87-113">Radio Buttons</span></span>
* <span data-ttu-id="cfe87-114">关</span><span class="sxs-lookup"><span data-stu-id="cfe87-114">Toggles</span></span>
* <span data-ttu-id="cfe87-115">测试区域</span><span class="sxs-lookup"><span data-stu-id="cfe87-115">Test Areas</span></span>
* <span data-ttu-id="cfe87-116">链接</span><span class="sxs-lookup"><span data-stu-id="cfe87-116">Links</span></span>
* <span data-ttu-id="cfe87-117">选项卡</span><span class="sxs-lookup"><span data-stu-id="cfe87-117">Tabs</span></span>
* <span data-ttu-id="cfe87-118">表格</span><span class="sxs-lookup"><span data-stu-id="cfe87-118">Tables</span></span>
* <span data-ttu-id="cfe87-119">图标</span><span class="sxs-lookup"><span data-stu-id="cfe87-119">Icons</span></span>

## <a name="optionally-use-react-controls"></a><span data-ttu-id="cfe87-120">（可选）使用响应控件</span><span class="sxs-lookup"><span data-stu-id="cfe87-120">Optionally use React controls</span></span>

<span data-ttu-id="cfe87-121">完整的团队控制库使用对[JAVASCRIPT UI 框架的响应](https://reactjs.org/)，但它是构建的，因此不会绑定到特定的 UI 框架。</span><span class="sxs-lookup"><span data-stu-id="cfe87-121">The full Teams control library uses the [React JavaScript UI framework](https://reactjs.org/) however it is built so that it is not tied to a specific UI framework.</span></span> <span data-ttu-id="cfe87-122">有四种不同的 npm 包：</span><span class="sxs-lookup"><span data-stu-id="cfe87-122">There are four different npm packages:</span></span>

* <span data-ttu-id="cfe87-123">**msteams-ui-样式-核心**UI 组件的核心 CSS 样式。</span><span class="sxs-lookup"><span data-stu-id="cfe87-123">**msteams-ui-styles-core** The core CSS styles of UI components.</span></span> <span data-ttu-id="cfe87-124">它独立于任何 UI 框架。</span><span class="sxs-lookup"><span data-stu-id="cfe87-124">It’s independent of any UI framework.</span></span>
* <span data-ttu-id="cfe87-125">**msteams-ui-图标-核心**团队的核心图标集图标。</span><span class="sxs-lookup"><span data-stu-id="cfe87-125">**msteams-ui-icons-core** The core set of Teams icons.</span></span>
* <span data-ttu-id="cfe87-126">**msteams-组件-响应**响应绑定库。</span><span class="sxs-lookup"><span data-stu-id="cfe87-126">**msteams-ui-components-react** The React binding library.</span></span> <span data-ttu-id="cfe87-127">这取决于 msteams--核心。</span><span class="sxs-lookup"><span data-stu-id="cfe87-127">It depends on msteams-ui-styles-core.</span></span>
* <span data-ttu-id="cfe87-128">**msteams-ui-图标-响应**团队图标集的响应绑定库。</span><span class="sxs-lookup"><span data-stu-id="cfe87-128">**msteams-ui-icons-react** The React binding library for the set of Teams icons.</span></span> <span data-ttu-id="cfe87-129">这取决于 msteams-------图标-核心。</span><span class="sxs-lookup"><span data-stu-id="cfe87-129">It depends on msteams-ui-icons-core.</span></span>

<span data-ttu-id="cfe87-130">这些库都是开放源代码，您可以使用 msteams-ui-styles-core 和 msteams-ui-无响应的核心。</span><span class="sxs-lookup"><span data-stu-id="cfe87-130">These libraries are all open source, and you can use msteams-ui-styles-core and msteams-ui-icons-core without React.</span></span>

## <a name="adding-the-control-library"></a><span data-ttu-id="cfe87-131">添加控件库</span><span class="sxs-lookup"><span data-stu-id="cfe87-131">Adding the control library</span></span>

<span data-ttu-id="cfe87-132">安装控件库及其对等依赖项`typestyle`：</span><span class="sxs-lookup"><span data-stu-id="cfe87-132">Install the control library and its peer dependency `typestyle`:</span></span>

```terminal
npm install --save typestyle && npm install --save msteams-ui-components-react
```

<span data-ttu-id="cfe87-133">*可选：* 安装团队图标。</span><span class="sxs-lookup"><span data-stu-id="cfe87-133">*Optional:* Install the Teams icons.</span></span>

```terminal
npm install --save msteams-ui-icons-react
```

<span data-ttu-id="cfe87-134">查找并打开`src/App.js`它的内容并将其替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="cfe87-134">Find and open `src/App.js` and replace its content with following code:</span></span>

```javascript
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, PrimaryButton } from ‘msteams-ui-components-react’

class App extends Component {
   render() {
      // Sets up the top-level context for the library. It accepts global
      // configurations such as font size and theme. fontSize is your page’s
      // default font size. We made it a parameter so that you could use this
      // library with CSS frameworks such as Bootstrap. Some CSS frameworks
      // set the default font size for the page; retrieve it and use it
      // instead of {16} in the block.
      // This library uses the power of CSS to do most of the work for you.
      // Instead of passing themes as a parameter to every UI component,
      // we set it on a parent HTML element. All HTML elements nested within
      // that parent will inherit these properties.

      return (
        <TeamsComponentContext
            fontSize={16}
            theme={ThemeStyle.Light}
        />
      );
   }
}
export default App;
```

<span data-ttu-id="cfe87-135">运行应用</span><span class="sxs-lookup"><span data-stu-id="cfe87-135">Run the app</span></span>

```terminal
npm run start
```

<span data-ttu-id="cfe87-136">导航到http://localhost:3000时，您应该会看到以下屏幕：</span><span class="sxs-lookup"><span data-stu-id="cfe87-136">When you navigate to http://localhost:3000, you should see the following screen:</span></span>

<img width="530px" src="~/assets/images/get-started/control-library-button.png" title="控制库按钮"/>

## <a name="dynamically-handling-theme-changes"></a><span data-ttu-id="cfe87-138">动态处理主题更改</span><span class="sxs-lookup"><span data-stu-id="cfe87-138">Dynamically handling theme changes</span></span>

<span data-ttu-id="cfe87-139">您的应用程序需要在以下情况处理主题：</span><span class="sxs-lookup"><span data-stu-id="cfe87-139">Your app needs to handle themes when:</span></span>

* <span data-ttu-id="cfe87-140">最初加载该选项卡</span><span class="sxs-lookup"><span data-stu-id="cfe87-140">The tab is initially loaded</span></span>
* <span data-ttu-id="cfe87-141">用户在选项卡已加载之后更改主题</span><span class="sxs-lookup"><span data-stu-id="cfe87-141">A user changes the theme after the tab is already loaded</span></span>

<span data-ttu-id="cfe87-142">主题包含在选项卡的[上下文](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest)中，可以在通过 URL 占位符值加载选项卡之前，也可以通过使用[Microsoft 团队 JAVASCRIPT 客户端 SDK](/javascript/api/%40microsoft/teams-js/context)在任何时候进行检索。</span><span class="sxs-lookup"><span data-stu-id="cfe87-142">The theme is included in a tab’s [Context](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest), which can be retrieved before the tab is loaded via URL placeholder values, or at any time by using the [Microsoft Teams JavaScript client SDK](/javascript/api/%40microsoft/teams-js/context).</span></span>

<span data-ttu-id="cfe87-143">下面讨论了如何检索当前主题以及如何响应主题更改：[获取你的 Microsoft 团队选项卡的上下文](~/concepts/tabs/tabs-context.md)。</span><span class="sxs-lookup"><span data-stu-id="cfe87-143">How the current theme is retrieved and how to respond to theme changes is discussed here: [Get context for your Microsoft Teams tab](~/concepts/tabs/tabs-context.md).</span></span>

<span data-ttu-id="cfe87-144">此示例代码演示如何执行此操作。</span><span class="sxs-lookup"><span data-stu-id="cfe87-144">This sample code shows how this is done.</span></span>

```js
componentWillMount() {
    // If you are deploying your site as a MS Teams static or configurable tab,
    // you should add “?theme={theme}” to your tabs URL in the manifest.
    // That way you will get the current theme before it’s loaded; getContext()
    // is called only after the tab is loaded, which will cause the tab to flash
    // if the current theme is different than the default.
    this.updateTheme(this.getQueryVariable('theme'));
    this.setState({
        fontSize: this.pageFontSize(),
    });

    // If you are not using the MS Teams Javascript SDK, you can remove this entire
    // if block, but if you want theme changes in the MS Teams client to propagate
    // to the tab, leave it here.
    microsoftTeams.initialize();
    microsoftTeams.registerOnThemeChangeHandler(this.updateTheme);
}
```

## <a name="connect-your-own-component-to-the-teamscomponentcontext"></a><span data-ttu-id="cfe87-145">将您自己的组件连接到 TeamsComponentContext</span><span class="sxs-lookup"><span data-stu-id="cfe87-145">Connect your own component to the TeamsComponentContext</span></span>

<span data-ttu-id="cfe87-146">如果您想要使用自己的 CSS 代码，您仍可以响应主题更改，并使用工作组定义的颜色。</span><span class="sxs-lookup"><span data-stu-id="cfe87-146">If you want to use your own CSS code you can still respond to theme changes and use colors defined by teams.</span></span> <span data-ttu-id="cfe87-147">TeamsComponentContext 允许您执行此操作。</span><span class="sxs-lookup"><span data-stu-id="cfe87-147">TeamsComponentContext allows you to do this.</span></span>

<span data-ttu-id="cfe87-148">再次编辑您`src/App.js`的文件并将其内容替换为以下代码：</span><span class="sxs-lookup"><span data-stu-id="cfe87-148">Once again, edit your `src/App.js` file and replace its content with following code:</span></span>

```javascript
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, ConnectedComponent } from ‘msteams-ui-components-react’

class App extends Component {
    render() {
        return (
            <TeamsComponentContext
                fontSize={16}
                theme={ThemeStyle.HighContrast}>
                <MyComponent />
            </TeamsComponentContext>
        );
    }
}

class MyComponent extends Component {
    render() {
        return (
            <ConnectedComponent render={(props) => {
                const context = props.context;

                switch (context.style) {
                case ThemeStyle.Dark:
                    return <div style={{ color: context.colors.dark.brand00 }}>Dark theme!</div>;
                case ThemeStyle.HighContrast:
                    return <div style={{ color: context.colors.highContrast.black }}>High Contrast theme!</div>;
                case ThemeStyle.Light:
                    return <div style={{ color: context.colors.light.brand00 }}>Light theme!</div>;
                }
            }} />
        );
    }
}

export default App;
```

<span data-ttu-id="cfe87-149">在此代码中，定义了名为 MyComponent 的新组件。</span><span class="sxs-lookup"><span data-stu-id="cfe87-149">In this code, a new component is defined called MyComponent.</span></span> <span data-ttu-id="cfe87-150">然后，添加名为 ConnectedComponent 的控件库中的特殊组件。</span><span class="sxs-lookup"><span data-stu-id="cfe87-150">Then a special component from the control library called ConnectedComponent is added.</span></span> <span data-ttu-id="cfe87-151">ConnectedComponent 具有一个名`render`为的属性，该属性采用函数作为参数。</span><span class="sxs-lookup"><span data-stu-id="cfe87-151">ConnectedComponent has a property called `render` which takes a function as a parameter.</span></span> <span data-ttu-id="cfe87-152">在呈现时，将使用您的选项卡的相应上下文调用此函数。上下文包括呈现页面的主题，以及可用于将团队颜色应用于选项卡的全局颜色对象。正如您在`switch`语句中所看到的那样`<div>` ，将根据主题选择相应的。</span><span class="sxs-lookup"><span data-stu-id="cfe87-152">At render time this function will be called with the appropriate context for your tab. The context includes the theme that the page is being rendered in as well as the global color object that you can use to apply Teams colors to your tab. As you can see in the `switch` statement, the appropriate `<div>` is chosen based on the theme.</span></span>

<span data-ttu-id="cfe87-153">若要更改主题，我们需要将根级别的 TeamsComponentContext 传递给不同的主题。</span><span class="sxs-lookup"><span data-stu-id="cfe87-153">To change themes, we need to pass the root-level TeamsComponentContext a different theme.</span></span> <span data-ttu-id="cfe87-154">当主题发生更改时，将重新呈现 ConnectedComponent 中包装的所有子元素。</span><span class="sxs-lookup"><span data-stu-id="cfe87-154">When a theme changes, all the child elements wrapped in ConnectedComponent will be re-rendered.</span></span> <span data-ttu-id="cfe87-155">请参阅上一节 "动态处理主题更改"。</span><span class="sxs-lookup"><span data-stu-id="cfe87-155">See previous section “Dynamically Handle Theme Changes.”</span></span>

<span data-ttu-id="cfe87-156">可以通过其他方式将组件连接到 TeamsComponentContext。</span><span class="sxs-lookup"><span data-stu-id="cfe87-156">There are other ways to connect your component to TeamsComponentContext.</span></span> <span data-ttu-id="cfe87-157">如果你熟悉[Redux](https://redux.js.org/basics/usage-with-react)，则可能更喜欢以下模式：</span><span class="sxs-lookup"><span data-stu-id="cfe87-157">If you’re familiar with [Redux](https://redux.js.org/basics/usage-with-react), you may prefer the following pattern:</span></span>

```js
import React, { Component } from ‘react’;
import { TeamsComponentContext, ThemeStyle, connectTeamsComponent } from ‘msteams-ui-components-react’

class App extends Component {
    render() {
        return (
            <TeamsComponentContext
                fontSize={16}
                theme={ThemeStyle.HighContrast}>
                <MyComponent />
            </TeamsComponentContext>
        );
    }
}

class MyComponentInner extends Component {
    render() {
        const context = this.props.context;
        switch (context.style) {
            case ThemeStyle.Dark:
                return <div style={{ color: context.colors.dark.brand00 }}>Dark theme!</div>;
            case ThemeStyle.HighContrast:
                return <div style={{ color: context.colors.highContrast.black }}>High Contrast theme!</div>;
            case ThemeStyle.Light:
                return <div style={{ color: context.colors.light.brand00 }}>Light theme!</div>;
        }
    }
}

const MyComponent = connectTeamsComponent(MyComponentInner);

export default App;
```

<span data-ttu-id="cfe87-158">在此方法中，不使用 ConnectedComponent，而是使用 connectTeamsComponent 函数。</span><span class="sxs-lookup"><span data-stu-id="cfe87-158">In this method, instead of using ConnectedComponent, you use the connectTeamsComponent function.</span></span> <span data-ttu-id="cfe87-159">ConnectTeamsComponent 函数将使用当前组件，并返回一个新组件，其中插入了 context 对象。</span><span class="sxs-lookup"><span data-stu-id="cfe87-159">The connectTeamsComponent function takes your current component and returns a new component with the context object injected.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cfe87-160">后续步骤</span><span class="sxs-lookup"><span data-stu-id="cfe87-160">Next steps</span></span>

<span data-ttu-id="cfe87-161">指向团队应用程序 Studio，并查看我们提供的所有控件以及如何使用它们的示例代码。</span><span class="sxs-lookup"><span data-stu-id="cfe87-161">Head to Teams App Studio and check out all the controls we offer and sample code of how to use them.</span></span> <span data-ttu-id="cfe87-162">不要忘记在不同主题中浏览它们。</span><span class="sxs-lookup"><span data-stu-id="cfe87-162">Don’t forget to explore them in different themes.</span></span>