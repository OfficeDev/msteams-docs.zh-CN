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
# <a name="using-the-control-library-in-app-studio"></a>在应用程序 Studio 中使用控件库

[Microsoft 团队应用程序 Studio](~/get-started/get-started-app-studio.md)为你提供了一组可在你自己的应用程序中使用的控件。 这些控件在应用程序 Studio 的 "*控件库*" 选项卡中提供。

这些控件由 Microsoft 团队设计人员创建，用于简化其自己的工作流，并对控件行为和支持团队的默认主题进行标准化。 您可以在自己的应用程序中使用此库来实现统一的外观和感觉。

控件包括：

* 按钮
* 下拉
* 复选框
* 单选按钮
* 关
* 测试区域
* 链接
* 选项卡
* 表格
* 图标

## <a name="optionally-use-react-controls"></a>（可选）使用响应控件

完整的团队控制库使用对[JAVASCRIPT UI 框架的响应](https://reactjs.org/)，但它是构建的，因此不会绑定到特定的 UI 框架。 有四种不同的 npm 包：

* **msteams-ui-样式-核心**UI 组件的核心 CSS 样式。 它独立于任何 UI 框架。
* **msteams-ui-图标-核心**团队的核心图标集图标。
* **msteams-组件-响应**响应绑定库。 这取决于 msteams--核心。
* **msteams-ui-图标-响应**团队图标集的响应绑定库。 这取决于 msteams-------图标-核心。

这些库都是开放源代码，您可以使用 msteams-ui-styles-core 和 msteams-ui-无响应的核心。

## <a name="adding-the-control-library"></a>添加控件库

安装控件库及其对等依赖项`typestyle`：

```terminal
npm install --save typestyle && npm install --save msteams-ui-components-react
```

*可选：* 安装团队图标。

```terminal
npm install --save msteams-ui-icons-react
```

查找并打开`src/App.js`它的内容并将其替换为以下代码：

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

运行应用

```terminal
npm run start
```

导航到http://localhost:3000时，您应该会看到以下屏幕：

<img width="530px" src="~/assets/images/get-started/control-library-button.png" title="控制库按钮"/>

## <a name="dynamically-handling-theme-changes"></a>动态处理主题更改

您的应用程序需要在以下情况处理主题：

* 最初加载该选项卡
* 用户在选项卡已加载之后更改主题

主题包含在选项卡的[上下文](/javascript/api/@microsoft/teams-js/context&view=msteams-client-js-latest)中，可以在通过 URL 占位符值加载选项卡之前，也可以通过使用[Microsoft 团队 JAVASCRIPT 客户端 SDK](/javascript/api/%40microsoft/teams-js/context)在任何时候进行检索。

下面讨论了如何检索当前主题以及如何响应主题更改：[获取你的 Microsoft 团队选项卡的上下文](~/concepts/tabs/tabs-context.md)。

此示例代码演示如何执行此操作。

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

## <a name="connect-your-own-component-to-the-teamscomponentcontext"></a>将您自己的组件连接到 TeamsComponentContext

如果您想要使用自己的 CSS 代码，您仍可以响应主题更改，并使用工作组定义的颜色。 TeamsComponentContext 允许您执行此操作。

再次编辑您`src/App.js`的文件并将其内容替换为以下代码：

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

在此代码中，定义了名为 MyComponent 的新组件。 然后，添加名为 ConnectedComponent 的控件库中的特殊组件。 ConnectedComponent 具有一个名`render`为的属性，该属性采用函数作为参数。 在呈现时，将使用您的选项卡的相应上下文调用此函数。上下文包括呈现页面的主题，以及可用于将团队颜色应用于选项卡的全局颜色对象。正如您在`switch`语句中所看到的那样`<div>` ，将根据主题选择相应的。

若要更改主题，我们需要将根级别的 TeamsComponentContext 传递给不同的主题。 当主题发生更改时，将重新呈现 ConnectedComponent 中包装的所有子元素。 请参阅上一节 "动态处理主题更改"。

可以通过其他方式将组件连接到 TeamsComponentContext。 如果你熟悉[Redux](https://redux.js.org/basics/usage-with-react)，则可能更喜欢以下模式：

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

在此方法中，不使用 ConnectedComponent，而是使用 connectTeamsComponent 函数。 ConnectTeamsComponent 函数将使用当前组件，并返回一个新组件，其中插入了 context 对象。

## <a name="next-steps"></a>后续步骤

指向团队应用程序 Studio，并查看我们提供的所有控件以及如何使用它们的示例代码。 不要忘记在不同主题中浏览它们。