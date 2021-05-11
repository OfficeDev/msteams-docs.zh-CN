---
title: 入门 - 生成个人选项卡
author: girliemac
description: 使用"Microsoft Teams快速创建个人Microsoft Teams Toolkit。
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
# <a name="build-a-basic-personal-tab-for-microsoft-teams"></a>为用户生成基本个人Microsoft Teams

本教程指导你生成基本个人选项卡，Microsoft Teams。 选项卡是一种在应用程序中通过托管 Web 内容在应用中显示Teams。 选项卡是个人应用的一项常见功能，可为各个用户提供专用工作区。 个人选项卡是最接近传统 Web 体验Teams。 

## <a name="what-youll-learn"></a>您将了解哪些功能

* 了解与个人选项卡相关的应用配置和基架。
* 使用组织的联系人列表创建选项卡内容。
* 根据用户首选项更新选项卡的颜色主题。

## <a name="prerequisites"></a>先决条件

确保你了解如何设置和构建简单的Teams应用程序。 有关详细信息，请参阅创建[你的第一个Microsoft Teams Hello， World！"应用](../build-your-first-app/build-and-run.md)。

## <a name="1-understand-your-app-project-components"></a>1. 了解应用项目组件

创建基本个人选项卡后，生成的应用基架提供组件，用于Teams。 可以使用许多方法，但现在让我们关注以下内容： 

* `Tab.js` 文件 `src/components` 。 这用于呈现选项卡内容页。
* Microsoft TeamsJavaScript 客户端 SDK，预加载到项目的前端组件中。

正如您可能从文件顶部的部分注意到的，示例代码使用 React，这是一个开源 JavaScript 库，用于构建 `import` `Tabs.js` 用户界面。 [](https://reactjs.org/) 

> [!NOTE]
> 尽管React _开发不需要_ Teams，但本教程将指导你React。

## <a name="2-customize-your-tab-content-page"></a>2. 自定义选项卡内容页

您可以自定义选项卡内容页，以呈现组织中的重要联系人列表。 

**自定义选项卡内容页**

1. 使用与自己相关的信息复制和修改以下代码示例。 也可以像现在一样使用代码： 
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
1. 到达 目录 `src/components` 并打开 `Tab.js` 文件。 
1. 转到 `render()` ，将模板代码替换为内部修改后的代码 `return()` ，如以下示例所示：
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
1. 转到 目录，并修改包含以下代码的文件，以便使用任何主题更轻松地阅读电子邮件 `src/components` `App.css` 链接：
    ```CSS
    a {
      color: inherit;
    }
    ```
1. 保存所做的更改。 

   可以在应用选项卡中查看新内容，Teams。

   :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-content.png" alt-text="包含静态内容的个人选项卡的屏幕截图。":::

## <a name="3-update-your-tab-theme"></a>3. 更新选项卡主题

对于选项卡来说，让主题感觉对于用户来说是本机主题Teams。 必须将选项卡与主题Teams混合。 用户通常首选默认 (浅) 、深色或高对比度主题。 正如你可能在上一张屏幕截图中注意到的，当用户使用深色主题时，选项卡仍具有浅色背景。 这不是建议的用户体验。

JavaScript Teams SDK 可以使你的应用注意到和响应客户端中的主题更改。 为此，请按照下列步骤操作：

1. **获取有关已配置的客户端Teams上下文** 在 `microsoftTeams.getContext()` 文件中调用 `Tab.js` ，可提供一些有关已配置的客户端主题 (的上下文，如深色主题) 。 以下代码访问 `context` 接口及其属性：

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
1. **创建主题更改处理程序** 有了属性，你的应用可以深入了解应用在应用中 `context` Teams。 但是，当用户更新应用时，该应用的外观仍无法反映主题。

   你需要一个处理程序来使用主题更新应用的状态。 若要创建处理程序，在调用后立即插入以下主题更改 `microsoftTeams.getContext()` 处理程序：

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
1. **匹配主题样式** 主题更改处理程序已就位，但仍必须响应更改，将选项卡的颜色与当前主题保持一致。

   在 `render()` 函数中，将主题更改处理程序提供的状态存储在 `isTheme` 中：

    ```JavaScript
      const isTheme = this.state.context.theme
    ```
    
    > [!NOTE]
    > 本示例只是一种将样式应用到选项卡的方法。像现在一样使用代码，展开它，或编写你自己的代码。

    存储主题更改处理程序提供的状态后，提供条件逻辑以根据当前主题呈现选项卡的样式。 以下示例演示了执行此操作的基本方法：

    1. 转到 `render()` 并检查 中的当前主题 `isTheme` 。
    1. 使用 `newTheme` 与当前主题相关的 CSS 属性创建对象。
    1. 将以下 CSS 应用到选项卡内容的根 HTML 元素 `<div style={newTheme}>` () ：

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

       检查选项卡中的Teams。 外观现在与深色主题紧密匹配。

       :::image type="content" source="../assets/images/build-your-first-app/personal-tab-tutorial-updated-theme.png" alt-text="具有静态内容视图的个人选项卡的屏幕截图。":::

## <a name="see-also"></a>另请参阅

* [团队 JavaScript 客户端 SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [设计适用于桌面Microsoft Teams Web 的选项卡](../tabs/design/tabs.md) 
* [上下文接口](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/context?view=msteams-client-js-latest&preserve-view=true)
* [使用 UI Microsoft Teams设计应用](../concepts/design/design-teams-app-ui-templates.md) 
* [移动设备上的选项卡](../tabs/design/tabs-mobile.md)
* [单一登录 (SSO) 选项卡支持](../tabs/how-to/authentication/auth-aad-sso.md)
* [Microsoft Teams API 概述](https://docs.microsoft.com/graph/teams-concept-overview)
* [使用自定义个人选项卡和Node.js Yeoman 生成器创建自定义Microsoft Teams](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建频道选项卡](../build-your-first-app/build-channel-tab.md)