---
title: 入门 - 生成个人选项卡
author: heath-hamilton
description: 使用 Microsoft Teams Toolkit 快速创建 Microsoft Teams 个人Toolkit。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: 17263303207ffb5bee333f1ec0e655096b1062ee
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911910"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a>为 Microsoft Teams 生成个人选项卡

通过本质上在 Teams 中嵌入网页，选项卡是显示应用中内容的一种简单方法。

Teams 中具有两种类型的选项卡。 在本教程中，你将生成基本的个人 *选项卡*，一个适用于单个用户的全屏内容页。  (个人选项卡是最接近 Teams.) 

## <a name="before-you-begin"></a>准备工作

你需要一个基本的运行个人选项卡才能开始。 如果你没有，请参阅生成并 [运行你的第一个 Teams 应用](../build-your-first-app/build-and-run.md)。

## <a name="your-assignment"></a>你的作业

您的组织中的人员在查找重要功能的基本联系信息时 (技术支持、人力资源等) 。 你负责确保他们可以在一个地方快速找到此信息。 如何执行？ 当然，Teams 个人选项卡。

## <a name="what-youll-learn"></a>您将了解哪些知识

> [!div class="checklist"]
>
> * 确定一些与个人选项卡相关的应用配置和基架
> * 创建选项卡内容
> * 根据用户首选项更新选项卡的颜色主题

## <a name="1-identify-relevant-app-project-components"></a>1. 确定相关应用程序项目组件

使用 Teams 解决方案创建项目时，会自动设置大部分应用配置和基架Toolkit。 让我们看一下生成个人选项卡的主要组件。

### <a name="app-configurations"></a>应用配置

在工具包中，转到 **App Studio** 以查看和更新应用配置。

### <a name="app-scaffolding"></a>应用基架

应用基架提供在 Teams 中呈现个人选项卡的组件。 可以使用许多方法，但目前只需关注以下内容：

* `Tab.js` 文件 `src/components` 。 这用于呈现选项卡内容页。
* Microsoft Teams JavaScript 客户端 SDK，预加载到项目的前端组件中。

## <a name="2-customize-your-tab-content-page"></a>2. 自定义选项卡内容页

编译组织中重要联系人的列表。 复制并更新以下代码段，并包含与自己相关的信息，或者出于时间考虑，按如下所示使用代码。

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

转到 `src/components` 目录并打开 `Tab.js` 。 找到 `render()` 该函数，然后将内容粘贴到 `return()` (，如下所示) 。

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

添加以下规则，以便无论使用哪个主题，电子邮件 `App.css` 链接都更易于阅读。

```CSS
a {
  color: inherit;
}
```

保存所做的更改。 转到 Teams 中你的应用的选项卡以查看新内容。

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="包含静态内容的个人选项卡的屏幕截图。":::

## <a name="3-update-the-tab-theme"></a>3. 更新选项卡主题

良好的应用感觉对于 Teams 而言是原生的，因此选项卡与用户喜欢的 Teams 主题混合很重要：默认 (浅色) 、深色或高对比度。 正如你可能在上一张屏幕截图中注意到的，当客户端使用深色主题时，选项卡仍具有浅色背景。 这不是建议的用户体验。

[Teams JavaScript 客户端 SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)可以使你的应用注意到和响应客户端中的主题更改。 让我们演练一下如何完成此操作。

### <a name="get-context-about-the-teams-client"></a>获取有关 Teams 客户端的上下文

在你的 `Tab.js` 文件中，有一个调用提供有关配置的客户端主题的一些信息，以及其他 `microsoftTeams.getContext()` [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) 详细信息。 由于应用基架，因此可使用此代码，就像访问 `context` 接口及其属性一样。

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

### <a name="create-a-theme-change-handler"></a>创建主题更改处理程序

有了属性，你的应用可以深入了解 Teams `context` 中围绕它发生的情况。 但应用仍然不知道其外观应反映用户选择的主题。

你需要一个处理程序，以便应用的状态随主题一起更改。 在调用后立即插入以下主题更改 `microsoftTeams.getContext()` 处理程序。

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a>匹配主题样式

主题更改处理程序已就位，但你需要一些代码来响应这些更改，并且将选项卡的颜色与当前主题对齐。

> [!NOTE]
> 以下示例只是将样式应用到选项卡的一种方式。像现在一样使用代码，展开它，或编写你自己的代码。

在 `render()` 函数中，将主题更改处理程序提供的状态存储在中 `isTheme` 。

```JavaScript
  const isTheme = this.state.theme
```

存储主题更改处理程序提供的状态后，提供一些条件逻辑以根据当前主题呈现选项卡的样式。 以下示例演示了一种基本方法：
1. 检查 中的当前主题 `isTheme` 。
2. 使用 `newTheme` 与当前主题相关的 CSS 属性创建对象。
3. 将 CSS 应用到选项卡内容的根 HTML 元素 `<div>` () 。

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

在 Teams 中查看你的选项卡。 外观应该与深色主题紧密匹配。

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="具有静态内容视图的个人选项卡的屏幕截图。":::

## <a name="well-done"></a>干的好

恭喜！ 你拥有一个 Teams 应用，该应用具有个人选项卡，可更轻松地查找组织中的重要联系人。

## <a name="learn-more"></a>了解详细信息

* 遵循 [我们的设计准则，](../tabs/design/tabs.md) 使用 [生产就绪 UI](../concepts/design/design-teams-app-ui-templates.md) 模板生成，以创建无缝体验。
* 了解 [选项卡的移动](../tabs/design/tabs-mobile.md) 注意事项。
* [将 SSO 身份验证添加到您的选项卡](../tabs/how-to/authentication/auth-aad-sso.md)。
* 利用 Microsoft [Graph 的](https://docs.microsoft.com/graph/teams-concept-overview)Teams 数据。
* [创建没有工具包的选项卡](../tabs/quickstarts/create-personal-tab-node-yeoman.md)。

## <a name="next-lesson"></a>下一课程

你知道如何生成供个人使用的选项卡。 让我们看一下为团队频道和聊天构建选项卡需要哪些内容。

> [!div class="nextstepaction"]
> [创建频道选项卡](../build-your-first-app/build-channel-tab.md)
