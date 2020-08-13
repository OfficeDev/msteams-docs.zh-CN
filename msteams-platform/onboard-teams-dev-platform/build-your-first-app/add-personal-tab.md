---
title: 为团队创建个人选项卡
author: heath-hamilton
description: 了解如何在您的首个 Microsoft 团队应用程序中构建个人选项卡。
ms.topic: tutorial
ms.openlocfilehash: 1c782adce2201550d30d658907d507dc6a1337f3
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651924"
---
# <a name="create-a-personal-tab-for-teams"></a>为团队创建个人选项卡

通过在团队中嵌入网页，选项卡是在应用程序中呈现内容的一种简单方法。

团队中有两种类型的选项卡。 在本教程中，将为单个用户构建基本的 *个人选项卡*（全屏内容页面）。  (个人选项卡是团队中的传统网站体验中最接近的内容。 ) 

## <a name="before-you-begin"></a>准备工作

您需要一个基本运行的应用程序才能开始使用。 如果没有，请参阅 [生成并运行你的首个团队应用](build-and-run-with-toolkit.md)。

## <a name="your-assignment"></a>您的分配

组织中的人员在查找重要功能的基本联系人信息时遇到问题 (技术支持、人力资源等 ) 。 你需要确保他们能够在一个位置快速查找此信息。 您该如何操作？ 当然是 "工作组个人" 选项卡。

## <a name="what-youll-learn"></a>你将了解的内容

> [!div class="checklist"]
>
> * 标识与个人选项卡相关的应用部件清单（manifest）属性和基架
> * 创建选项卡的内容
> * 根据用户首选项更新选项卡的颜色主题

## <a name="identify-relevant-app-manifest-and-scaffolding-components"></a>确定相关的应用程序清单和基架组件

大多数个人选项卡应用程序基架和清单在您使用团队工具包创建项目时自动设置。 我们来看看用于构建个人选项卡的主要组件。

### <a name="app-manifest"></a>应用程序清单

应用程序清单中的以下代码片段 (`manifest.json` 项目目录中的文件 `.publish`) 显示 [`staticTabs`](../../resources/schema/manifest-schema.md#statictabs) ，其中包括与个人选项卡相关的属性和默认值。

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

* `entityId`：选项卡显示的页面的唯一标识符。
* `name`：该选项卡的显示名称 (例如，"我的联系人" ) 。
* `contentUrl`：主机 URL "选项卡内容" 页面 (必须是 HTTPS) 。
* `scopes`：指定选项卡仅供个人使用。

### <a name="app-scaffolding"></a>应用程序基架

应用程序基架提供用于在团队中呈现选项卡的组件。 你可以使用很多，但现在你只需关注以下内容：

* `Tab.js``src/components`项目目录中的文件
* Microsoft 团队 JavaScript 客户端 SDK，它在项目的前端组件中预加载

## <a name="create-your-tab-content"></a>创建选项卡内容

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

![包含静态内容的个人选项卡的示例屏幕截图](../doc-links/images/personal-tab-tutorial-content.png)

## <a name="update-the-tab-theme"></a>更新选项卡主题

理想的应用程序会让团队成为本地用户，因此，您的选项卡与您的用户喜欢的团队主题进行混合是很重要的：默认 (浅) 、深或高对比度。 正如您可能在最后的屏幕截图中已注意到，当客户端使用深色主题时，您的选项卡仍有浅背景。 这不是建议的用户体验。

[团队 JavaScript 客户端 SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest)可让你的应用程序知道和响应客户端中的主题更改。 我们来演练一下如何执行此操作。

### <a name="get-context-about-the-teams-client"></a>获取有关团队客户端的上下文

在您的文件中， `Tab.js` 有一个 `microsoftTeams.getContext()` 可提供 [`context`](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/microsoftteams.context?view=msteams-client-js-latest) 有关已配置的客户端主题的信息的呼叫。 由于应用程序基架，使用此代码来访问 `context` 接口及其属性。

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
> 下面的示例只是将样式应用于选项卡的一种方式。使用代码为，再展开或编写自己的代码。

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

![包含静态内容的个人选项卡的示例屏幕截图](../doc-links/images/personal-tab-tutorial-updated-theme.png)

## <a name="well-done"></a>干的好

恭喜你！ 您有一个 "个人" 选项卡的团队应用程序，可以更轻松地查找组织中的重要联系人。

## <a name="next-step"></a>后续步骤

您知道如何构建用于个人用途的选项卡。 让我们来看看构建团队频道和聊天的选项卡所需的内容。

> [!div class="nextstepaction"]
> [生成通道选项卡](add-channel-tab.md)

## <a name="learn-more"></a>了解详细信息

* [使用 Sso 对选项卡用户进行身份验证](../../tabs/how-to/authentication/auth-aad-sso.md)：如果您仅希望授权用户查看您的选项卡，请通过 Azure Active DIRECTORY (AD) 设置单一登录 (SSO) 。
* [从现有 web 应用或网页嵌入内容](../../tabs/how-to/add-tab.md#tab-requirements)：我们向您介绍了如何为个人选项卡创建新内容，但您也可以从外部 URL 加载内容。
* [为您的选项卡创建无缝体验](../../tabs/design/tabs.md)：有关设计团队选项卡的建议指南，请参阅。
* [为移动设备构建选项卡](../../tabs/design/tabs-mobile.md)：了解如何为智能手机和平板电脑开发选项卡。

