---
title: 入门-构建个人选项卡
author: heath-hamilton
description: 使用 Microsoft 团队工具包快速创建 Microsoft 团队个人选项卡。
ms.author: lajanuar
ms.date: 11/03/2020
ms.topic: tutorial
ms.openlocfilehash: 89d9a2109a863402dd7641d0882c530a0c2e6f66
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409069"
---
# <a name="build-a-personal-tab-for-microsoft-teams"></a>为 Microsoft 团队构建个人选项卡

通过在团队中嵌入网页，选项卡是在应用程序中呈现内容的一种简单方法。

团队中有两种类型的选项卡。 在本教程中，将为单个用户构建基本的 *个人选项卡*（全屏内容页面）。  (个人选项卡是团队中的传统网站体验中最接近的内容。 ) 

## <a name="before-you-begin"></a>准备工作

若要开始，您需要 "运行一个基本的个人" 选项卡。 如果没有，请参阅 [生成并运行你的首个团队应用](../build-your-first-app/build-and-run.md)。

## <a name="your-assignment"></a>您的分配

组织中的人员在查找重要功能的基本联系人信息时遇到问题 (技术支持、人力资源等 ) 。 你需要确保他们能够在一个位置快速查找此信息。 您该如何操作？ 当然是 "工作组个人" 选项卡。

## <a name="what-youll-learn"></a>你将了解的内容

> [!div class="checklist"]
>
> * 确定与个人选项卡相关的一些应用配置和基架
> * 创建选项卡内容
> * 根据用户首选项更新选项卡的颜色主题

## <a name="1-identify-relevant-app-project-components"></a>1. 确定相关的应用程序项目组件

大部分应用配置和基架是在使用团队工具包创建项目时自动设置的。 我们来看看用于构建个人选项卡的主要组件。

### <a name="app-configurations"></a>应用配置

您可以使用包含在工具包中的应用程序 Studio 查看和更新应用程序配置。

在安装过程中，该工具包最初配置了 "选项卡内容" 页，您可以在其中显示主要内容。 在工具包中，转到 **应用程序 Studio** 并选择 " **选项卡** " 以查看配置。

### <a name="app-scaffolding"></a>应用程序基架

应用程序基架提供用于在团队中呈现个人选项卡的组件。 你可以使用很多，但现在你只需关注以下内容：

* `Tab.js``src/components`项目目录中的文件。 这是为了呈现您的选项卡内容页。
* Microsoft 团队 JavaScript 客户端 SDK，它在项目的前端组件中预加载。

## <a name="2-customize-your-tab-content-page"></a>2. 自定义 "选项卡内容" 页

编译组织中重要联系人的列表。 使用与您相关的信息复制和更新以下代码段，如果需要，请按如下所示使用代码。

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

转到 `src/components` 目录并打开 `Tab.js` 。 找到 `render()` 函数并将内容粘贴 (中， `return()` 如) 所示。

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

将以下规则添加到 `App.css` ，无论使用哪个主题，电子邮件链接更易于阅读。

```CSS
a {
  color: inherit;
}
```

保存所做的更改。 转到团队中的应用程序选项卡以查看新内容。

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-content.png" alt-text="包含静态内容的个人选项卡的屏幕截图。":::

## <a name="3-update-the-tab-theme"></a>3. 更新选项卡主题

理想的应用程序会让团队成为本地用户，因此，您的选项卡与您的用户喜欢的团队主题进行混合是很重要的：默认 (浅) 、深或高对比度。 正如您可能在最后的屏幕截图中已注意到，当客户端使用深色主题时，您的选项卡仍有浅背景。 这不是建议的用户体验。

[团队 JavaScript 客户端 SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)可让你的应用程序知道和响应客户端中的主题更改。 我们来演练一下如何执行此操作。

### <a name="get-context-about-the-teams-client"></a>获取有关团队客户端的上下文

在您的文件中， `Tab.js` 有一个 `microsoftTeams.getContext()` 可提供 [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true) 有关已配置的客户端主题的信息的呼叫。 由于应用程序基架，使用此代码来访问 `context` 接口及其属性。

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

使用这些 `context` 属性，您的应用程序可以清楚地了解团队中的 it 所发生的问题。 但是，应用仍不知道其外观应反映用户选择的任何主题。

您需要处理程序，以便您的应用程序的状态随主题而更改。 在调用后立即插入以下主题更改处理程序 `microsoftTeams.getContext()` 。

```JavaScript
  microsoftTeams.registerOnThemeChangeHandler(theme => {
    if (theme !== this.state.theme) {
      this.setState({ theme });  
    }
  });
```

### <a name="match-theme-styles"></a>匹配主题样式

您的主题更改处理程序已准备就绪，但您需要一些代码来响应这些更改，并将您的选项卡的颜色与当前主题对齐。

> [!NOTE]
> 下面的示例只是将样式应用于选项卡的一种方法。使用的代码为，然后展开或编写自己的代码。

将主题更改处理程序提供的状态存储在中 `isTheme` 。

```JavaScript
  const isTheme = this.state.theme
```

提供一些条件逻辑，以根据当前主题呈现您的选项卡样式。 下面的示例展示了这样做的基本方法： 1) 检查中的当前主题 `isTheme` ，2) 使用与 `newTheme` 当前主题相关的 css 属性创建对象，3) 将 css 应用到您的选项卡内容的根 HTML 元素 (`<div>`) 。

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

检查团队中的选项卡。 外观应与深色主题紧密匹配。

:::image type="content" source="../assets/images/tabs/personal-tab-tutorial-updated-theme.png" alt-text="包含静态内容视图的个人选项卡的屏幕截图。":::

## <a name="well-done"></a>干的好

恭喜！ 您有一个 "个人" 选项卡的团队应用程序，可以更轻松地查找组织中的重要联系人。

## <a name="learn-more"></a>了解详细信息

* [使用 Sso 对选项卡用户进行身份验证](../tabs/how-to/authentication/auth-aad-sso.md)：如果您仅希望授权用户查看您的选项卡，请通过 Azure Active DIRECTORY (AD) 设置单一登录 (SSO) 。
* [从现有 web 应用或网页嵌入内容](../tabs/how-to/add-tab.md#tab-requirements)：我们向您介绍了如何为个人选项卡创建新内容，但您也可以从外部 URL 加载内容。
* [为您的选项卡创建无缝体验](../tabs/design/tabs.md)：有关设计团队选项卡的建议指南，请参阅。
* [为移动设备构建选项卡](../tabs/design/tabs-mobile.md)：了解如何为电话和平板电脑开发选项卡。
* [使用 Microsoft Graph API 的团队数据](https://docs.microsoft.com/graph/teams-concept-overview)
* [创建不带工具箱的选项卡](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>下一课

您知道如何构建用于个人用途的选项卡。 让我们来看看构建团队频道和聊天的选项卡所需的内容。

> [!div class="nextstepaction"]
> [创建频道选项卡](../build-your-first-app/build-channel-tab.md)
