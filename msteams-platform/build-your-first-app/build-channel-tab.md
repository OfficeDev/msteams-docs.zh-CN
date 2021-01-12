---
title: 入门 - 生成频道和组选项卡
author: heath-hamilton
description: 使用 Microsoft Teams Toolkit 快速创建 Microsoft Teams 频道和Toolkit。
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 2ad0474859118f302a39e823f7669dc54061d525
ms.sourcegitcommit: 5687a901d48bcf2f5a3a086e0f703f854e8b9c21
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/11/2021
ms.locfileid: "49795452"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a>为 Microsoft Teams 生成频道和组选项卡

在本教程中，你将生成基本频道 *选项卡 (也称为* 组选项卡 *) ，* 它是团队频道或聊天的全屏页面。 与个人选项卡不同，用户可以配置此类选项卡的一些 (例如，重命名该选项卡，以便其通道) 。

## <a name="your-assignment"></a>你的作业

前不久，你的组织创建了一个 Teams 应用，该应用使用选项卡在技术支持、人力资源等 (显示重要的) 。 但是，由于它是个人选项卡，因此每个用户必须安装该选项卡以查看它，并且采用率低于预期。 换句话说，太多工作人员仍不知道如何联系技术支持人员。

通过生成频道选项卡，可以使此信息更易于查找，这将消除要求所有人安装应用的负担。 相反，一个用户可以在频道中添加选项卡或聊天，以有利于整个组。

## <a name="what-youll-learn"></a>您将了解哪些知识

> [!div class="checklist"]
>
> * 使用 Microsoft Teams Toolkit for Visual Studio Code 创建应用项目
> * 确定一些与通道选项卡相关的应用配置和基架
> * 创建选项卡内容
> * 为选项卡的配置页创建内容
> * 提供建议的选项卡名称
> * 在本地生成和运行应用
> * 在 Teams 中旁加载应用进行测试

## <a name="before-you-begin"></a>准备工作

如果尚未安装，请确保了解并 [安装 Teams 开发先决条件](build-first-app-overview.md#get-prerequisites)。

## <a name="1-create-your-app-project"></a>1. 创建应用项目

Microsoft Teams Toolkit帮助配置你的应用和设置与频道和组选项卡相关的基架，包括显示"Hello， World！" 的基本配置页面和内容页。 消息。

> [!TIP]
> 如果你之前尚未创建 Teams 应用项目，你可能会发现按照这些说明更详细地解释项目非常有用[](../build-your-first-app/build-and-run.md)。

1. 在Visual Studio代码中，选择左侧活动栏上的 **Microsoft Teams，** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 **"创建新的 Teams 应用"。**
1. 当系统提示时，使用 Microsoft 365 开发帐户登录。
1. 在"**添加功能"屏幕上**，选择 **"Tab"，** 然后选择"**下一步"。**
1. 输入 Teams 应用的名称。  (这是应用的默认名称，也是本地计算机上应用项目目录的名称。) 选择组或 **Teams 频道选项卡**。
1. 选择 **屏幕** 底部的"完成"以配置项目。  

## <a name="2-identify-relevant-app-project-components"></a>2. 确定相关应用程序项目组件

使用工具包创建项目时，会自动设置大部分应用配置和基架。 让我们看一下用于生成频道选项卡的主要组件。

### <a name="app-configurations"></a>应用配置

在工具包中，转到 **App Studio** 以查看和更新应用配置。

### <a name="app-scaffolding"></a>应用基架

应用基架提供在 Teams 中呈现频道选项卡的组件。 可以使用许多方法，但目前只需关注以下内容：

* 位于项目目录中的两 `src/components` 个文件：
  * `Tab.js` 用于呈现选项卡的内容页。
  * `TabConfig.js` 用于呈现选项卡的配置页。
* Microsoft Teams JavaScript 客户端 SDK，预加载到项目的前端组件中。

## <a name="3-customize-your-tab-content-page"></a>3. 自定义选项卡内容页

复制并更新以下代码段，并包含与您的组织有关的信息，或者出于时间考虑，按如下所示使用代码。

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

将以下规则 (也位于) 中，以便无论使用哪个主题，电子邮件链接都更易于 `App.css` `src/components` 阅读。

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a>4. 自定义选项卡配置页

频道或聊天中的每个选项卡都有一个配置页，这是一个模式，具有至少一个设置选项，在用户添加你的应用时显示。 默认情况下，配置页询问用户是否要在安装选项卡时通知频道或聊天。

向配置页面添加一些自定义内容。 转到项目的目录，打开并更新 (中的占位符内容，如下面的示例 `src/components` `TabConfig.js` `return()`) 。

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
> 至少应在此页面上提供有关你的应用的一些简短信息，因为这可能是用户第一次了解它。 还可以包括自定义配置选项或身份验证 [工作流](../tabs/how-to/authentication/auth-aad-sso.md)（在选项卡配置页面上很常见）。

## <a name="5-provide-a-suggested-tab-name"></a>5. 提供建议的选项卡名称

添加通道选项卡时，默认情况下应用名称 (例如，第一 **个应用) 。**

这可能适合你调用你的应用，但你可能希望提供一个在组协作上下文中更有意义的名称 (例如，团队联系人) 。 

1. 在 `TabConfig.js` 中，转到 `microsoftTeams.settings.setSettings` 。
2. 使用 `suggestedDisplayName` 要默认显示的选项卡名称添加属性。 
3. 使用以下示例中提供的名称或键入您的名称。  (默认情况下，用户可以更改 name.) 

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a>6. 生成并运行应用

为符合时间需要，你将在本地生成和运行应用。

 (工具包 .) 中也提供了 `README` 此信息。

1. 在终端中，转到应用项目的根目录并运行 `npm install` 。
1. 运行 `npm start`。

完成后，将成功 **进行编译！** 消息。 你的应用正在运行 `https://localhost:3000` 。

## <a name="7-sideload-your-app-in-teams"></a>7. 在 Teams 中旁加载应用

你的应用已准备好在 Teams 中进行测试。 为此，你必须具有允许应用旁加载的帐户。  (如果不确定是否拥有，请了解如何获取 Teams 开发 [帐户](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).) 

1. 在Visual Studio中，按 **F5** 键启动 Teams Web 客户端。
1. 若要在 Teams 中显示你的应用内容，请指定你的应用在哪些 () `localhost` 可信赖：
   1. 默认情况下，在 Google Chrome 的相同浏览器窗口中打开 (新选项卡) 按 **F5** 后打开。
   1. 转到 `https://localhost:3000/tab` 并转到页面。
1. 返回到 Teams。 在模式中，选择"添加到 **团队** "或"添加到 **聊天** "，并找到可用于测试的频道或聊天。
1. 选择 **"设置"选项卡**。配置页以模式显示。<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="频道选项卡配置页面的屏幕截图。":::
1. 选择 **"保存** "以配置选项卡。显示内容页。<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="具有静态内容视图的频道选项卡的屏幕截图。":::

## <a name="well-done"></a>干的好

恭喜！ 你有一个 Teams 应用，该应用具有一个选项卡，用于显示频道和聊天中的有用内容。

## <a name="learn-more"></a>了解详细信息

* 使用[SSO](../tabs/how-to/authentication/auth-aad-sso.md)对选项卡用户进行身份验证：如果仅希望授权用户查看您的选项卡，请通过 Azure Active Directory) AD (设置单一登录 (SSO) 。
* [嵌入现有 Web](../tabs/how-to/add-tab.md#tab-requirements)应用或网页中的内容：我们展示了如何为选项卡创建新内容，但您也可以从外部 URL 加载内容。
* [创建无缝选项卡体验](../tabs/design/tabs.md)：请参阅设计 Teams 选项卡的建议准则。
* [构建适用于移动设备的选项卡](../tabs/design/tabs-mobile.md)：了解如何开发适用于手机和平板电脑的选项卡。
* [使用 Microsoft Graph API 利用 Teams 数据](https://docs.microsoft.com/graph/teams-concept-overview)
* [创建不带工具包的选项卡](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>下一课程

你知道如何生成用于协作的选项卡。 想要尝试生成不同类型的 Teams 应用？

> [!div class="nextstepaction"]
> [创建机器人](../build-your-first-app/build-bot.md)
