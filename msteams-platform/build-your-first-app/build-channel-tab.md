---
title: 入门 - 生成频道和组选项卡
author: girliemac
description: 使用"Microsoft Teams快速创建一个"频道和组"Microsoft Teams Toolkit。
ms.author: timura
ms.date: 03/22/2020
ms.topic: tutorial
ms.openlocfilehash: 868a471499bf2015196b7b741e340d070d0ed458
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068740"
---
# <a name="build-your-first-channel-and-group-tab-for-microsoft-teams"></a>为用户生成你的第一个频道和组Microsoft Teams

本教程指导你生成基本频道 *选项卡，也称为* 组选项卡，它是团队频道或聊天的全屏页面。 还可以配置此类选项卡的某些方面，例如，重命名选项卡，以便对通道有意义，而您无法在个人选项卡中这样做。

## <a name="what-youll-learn"></a>您将了解哪些功能

* 使用 Microsoft Teams Toolkit 创建应用Visual Studio Code。
* 了解与通道选项卡相关的应用配置和基架。
* 创建选项卡内容和选项卡配置。
* 在团队中生成并运行应用进行测试。

## <a name="prerequisites"></a>先决条件

确保你了解如何设置和构建简单的Teams应用程序。 有关详细信息，请参阅创建[你的第一个Microsoft Teams Hello， World！"应用](../build-your-first-app/build-and-run.md)。

## <a name="1-create-your-app-project"></a>1. 创建应用项目

The Microsoft Teams Toolkit helps you to configure your app and set up the scaffolding relevant to channel and group tabs. 它还包含显示"Hello， World！"的基本配置页和内容页。 消息。

**创建应用项目**

1. 转到"Visual Studio Code"，然后选择Microsoft Teams :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 栏上的"活动栏"。
1. 当系统提示Microsoft 365，使用你的开发帐户登录。
1. 在"**选择项目"** 屏幕上，选择"频道和组 (下的 **"JS**) **JavaScript 应用"。**
1. 输入你的应用Teams名称。 

    > [!NOTE]
    > 这是应用的默认名称，也是本地计算机上应用项目目录的名称。

1. 选择 **组或Teams频道选项卡**。
1. 选择 **屏幕** 底部的"完成"以配置项目，并在本地计算机上保存项目。  

## <a name="2-understand-your-app-project-components"></a>2. 了解应用项目组件

使用工具包创建项目时，将自动设置大部分应用配置和基架。 让我们看一下生成频道选项卡的主要组件。

* **应用配置**：在 **工具包** 中打开 App Studio 以查看和更新应用配置。
* **应用基架**：应用基架提供在应用中呈现通道选项卡所需的Teams。 不过，你可以处理很多项目，但现在让我们关注以下内容：
  * 位于项目目录中 `src/components` 的文件：
    * `Tab.js` 用于呈现选项卡的内容页。
    * `TabConfig.js` 用于呈现选项卡的配置页面。
  * Microsoft TeamsJavaScript 客户端 SDK，预加载到项目的前端组件中。

## <a name="3-customize-your-tab-content-page"></a>3. 自定义选项卡内容页

1. 复制并修改以下代码示例，并包含与组织有关的信息。 也可以按以下代码段使用代码段：
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
1. 转到 `src/components` 目录并打开 `Tab.js` 文件。 找到 `render()` 函数，然后将代码粘贴到 内 `return()` ，如以下示例所示：
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
1. 转到 目录，然后用以下代码更新文件，使电子邮件链接更易于在任何使用的主题 `src/components` `App.css` 中阅读：
    ```CSS
    a {
      color: inherit;
    }
    ```

## <a name="4-customize-your-tab-configuration-page"></a>4. 自定义选项卡配置页

频道或聊天中的每个选项卡都有一个配置页面，即至少具有一个设置选项的模式，在用户添加应用时显示此选项。 默认情况下，配置页会询问用户是否要在安装选项卡时通知频道或聊天。 您可以通过添加自定义内容来自定义配置页。

若要添加自定义内容，请从 目录中打开 `TabConfig.js` `src/components` 文件并更新内的占位符内容 `return()` ，如以下示例所示：

  ```JavaScript
  return (
      <div>
        <h1>Add My Contoso Contacts</h1>
        <div>
          Select <b>Save</b> to add our organization's important contacts to this workspace.
        </div>
      </div>
  );
  ```
 
> [!TIP]
> 在此页面上提供有关你的应用的简短信息，因为这将是用户第一次阅读它。 还可以包括自定义配置选项或身份验证 [工作流](../tabs/how-to/authentication/auth-aad-sso.md)，这是在选项卡配置页面上很常见的。

## <a name="5-customize-your-tab-name"></a>5. 自定义选项卡名称

添加通道选项卡时，应用程序名称默认显示，例如，第 **一个应用**。 还可以提供在组协作上下文中更有意义的名称，例如，"**团队联系人"：**

1. 转到 `src/components` 目录并打开 `TabConfig.js` 文件。
1. 在 `suggestedDisplayName` 下面添加包含要默认显示的选项卡名称的属性 `microsoftTeams.settings.setSettings` ，如以下示例所示：

  ```JavaScript
    microsoftTeams.settings.setSettings({
    "contentUrl": "https://localhost:3000/tab",
    "suggestedDisplayName": "Team Contacts"
  });
  ```

## <a name="6-build-and-run-your-app"></a>6. 生成并运行应用

本教程指导你在本地生成和运行应用。 

1. 转到终端中应用项目的根目录。
1. 运行 `npm install`。
1. 运行 `npm start`。

此信息也存在于工具包 `README` 的 部分中。
你的应用在编译 `https://localhost:3000` 成功后 **运行！** 消息显示在终端中。 

## <a name="7-sideload-your-app-in-teams"></a>7. 在应用程序中旁加载Teams

你的应用已准备好在 Teams 中进行测试。 为此，你必须具有允许应用旁加载的帐户。 

1. 使用 **F5** Teams打开 Visual Studio Code Web 客户端。
1. 按照 () 使应用内容显示在应用中，添加可信赖 `localhost` Teams：

   1. 默认情况下，在 Google Chrome (打开一个新选项卡，) **F5** 键打开该选项卡。
   1. 打开 `https://localhost:3000/tab` 并继续执行页面。

1. 选择 **"添加到团队"** 或"添加到聊天"，并找到可用于从 Teams 模式进行测试的频道或Teams。
1. 选择 **"设置选项卡"。** 配置页以模式显示。

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="频道选项卡配置页面的屏幕截图。":::

1. 选择 **"保存** "以配置选项卡。将显示以下内容页：

   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="具有静态内容视图的频道选项卡的屏幕截图。":::

## <a name="see-also"></a>另请参阅

* [生成并运行你的第一个Microsoft Teams应用](../build-your-first-app/build-and-run.md) 
* [团队 JavaScript 客户端 SDK](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* [设计适用于桌面Microsoft Teams Web 的选项卡](../tabs/design/tabs.md) 
* [使用 UI Microsoft Teams设计应用](../concepts/design/design-teams-app-ui-templates.md) 
* [移动设备上的选项卡](../tabs/design/tabs-mobile.md)
* [单一登录 (SSO) 选项卡支持](../tabs/how-to/authentication/auth-aad-sso.md)
* [Microsoft Teams API 概述](https://docs.microsoft.com/graph/teams-concept-overview)
* [使用自定义个人选项卡和Node.js Yeoman 生成器创建自定义Microsoft Teams](../tabs/quickstarts/create-personal-tab-node-yeoman.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建机器人](../build-your-first-app/build-bot.md)

> [!div class="nextstepaction"]
> [创建邮件扩展](../build-your-first-app/build-messaging-extension.md)