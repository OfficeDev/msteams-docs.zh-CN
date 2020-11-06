---
title: 入门-构建通道和组选项卡
author: heath-hamilton
description: 使用 Microsoft 团队工具包快速创建 Microsoft 团队频道和分组选项卡。
ms.author: lajanuar
ms.date: 10/09/2020
ms.topic: tutorial
ms.openlocfilehash: 46b5410a1ae7c866f8998362765dfe5462df94cb
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931762"
---
# <a name="build-a-channel-and-group-tab-for-microsoft-teams"></a>为 Microsoft 团队构建通道和组选项卡

在本教程中，你将构建基本的 *频道选项卡* (也称为 " *组" 选项* 卡) （它是团队频道或聊天的全屏页面）。 与 "个人" 选项卡不同，用户可以配置此类选项卡的某些方面 (例如，重命名选项卡，使其对频道) 有意义。

## <a name="your-assignment"></a>您的分配

以前，您的组织创建了一个团队应用程序，该应用程序使用选项卡来显示重要的联系人信息， (技术支持、人力资源等 ) 。 但是，由于它是一个 "个人" 选项卡，因此每个用户都必须安装该选项卡，才能看到它，并且采用情况低于预期。 换句话说，工作线程太多仍不知道如何联系技术支持人员。

您可以通过构建通道选项卡使此信息更易于查找，这将消除要求每个人安装应用程序的负担。 相反，一个用户可以在频道或聊天中添加该选项卡，以了解整个组的好处。

## <a name="what-youll-learn"></a>你将了解的内容

> [!div class="checklist"]
>
> * 使用 Microsoft 团队工具包创建适用于 Visual Studio Code 的应用程序项目
> * 确定与频道和组选项卡相关的一些应用配置和基架
> * 创建选项卡内容
> * 创建选项卡的配置页的内容
> * 提供建议的选项卡名称
> * 在本地生成和运行应用程序
> * 在团队中旁加载您的应用程序以供测试

## <a name="before-you-begin"></a>准备工作

如果还没有，请确保 [了解并安装团队开发先决条件](build-first-app-overview.md#get-prerequisites)。

## <a name="1-create-your-app-project"></a>1. 创建您的应用程序项目

Microsoft 团队工具包可帮助配置您的应用程序，并设置与通道和组选项卡相关的基架，包括显示 "Hello，World！" 的基本配置页和内容页。 消息。

> [!TIP]
> 如果之前尚未创建团队应用程序项目，您可能会发现，请按照 [以下说明](../build-your-first-app/build-and-run.md) 更详细地说明项目。

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队** "， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用** "。
1. 出现提示时，使用 Microsoft 365 开发帐户登录。
1. 在 " **添加功能** " 屏幕上，依次选择 **"** **下一步** "。
1. 为你的团队应用输入名称。  (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) 
1. 检查 " **个人" 选项卡** 和 **"组" 或 "工作组通道" 选项卡** 选项。  (你将很快了解为什么需要两种类型的选项卡。 ) 
1. 选择屏幕底部的 " **完成** " 以配置项目。  

## <a name="2-identify-relevant-app-project-components"></a>2. 确定相关的应用程序项目组件

大部分应用配置和基架是在使用团队工具包创建项目时自动设置的。 我们来看看构建通道和组选项卡的主要组件。

### <a name="app-configurations"></a>应用配置

您可以使用包含在工具包中的应用程序 Studio 查看和更新应用程序配置。

在安装过程中，该工具包最初配置了通道和组选项卡的两个基本组件：

* **配置页面** ：用于将选项卡添加到频道或聊天的对话框。  (在应用程序 Studio 中，通过转到 **"团队" 选项卡 > "团队" 选项卡** ，可以找到此页面。 ) 
* **内容页面** ：显示主要内容的位置。  (在应用程序 Studio 中，通过转到 " **添加个人" 选项卡 > 的选项** 卡可以找到此页面。 ) 

### <a name="app-scaffolding"></a>应用程序基架

应用程序基架提供用于在团队中呈现个人选项卡的组件。 你可以使用很多，但现在你只需关注以下内容：

* 位于项目目录中的两个文件 `src/components` ：
  * `Tab.js` 用于呈现选项卡的内容页。
  * `TabConfig.js` 用于呈现选项卡的配置页。
* Microsoft 团队 JavaScript 客户端 SDK，它在项目的前端组件中预加载。

## <a name="3-customize-your-tab-content-page"></a>3. 自定义 "选项卡内容" 页

使用与您的组织相关的信息复制和更新以下代码段，如果有时间，请使用代码。

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

将以下规则添加到 `App.css` (也位于 `src/components`) 中，这样无论使用哪个主题，电子邮件链接都更易于阅读。

```CSS
a {
  color: inherit;
}
```

## <a name="4-customize-your-tab-configuration-page"></a>4. 自定义您的选项卡配置页

频道或聊天中的每个选项卡都有一个配置页面，其中包含至少一个安装选项的对话框，在用户添加您的应用程序时显示。 默认情况下，配置页面会询问用户是否要在安装该选项卡时通知频道或聊天。

将一些自定义内容添加到配置页面。 转到项目的 `src/components` 目录，打开 `TabConfig.js` ，并更新中的占位符内容 (中， `return()` 如下面的示例所示) 。

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
> 至少，在此页面上提供有关您的应用程序的一些简要信息，因为这可能是用户首次了解它。 您还可以包括自定义配置选项或 [身份验证工作流](../tabs/how-to/authentication/auth-aad-sso.md)，这在选项卡配置页上很常见。

## <a name="5-provide-a-suggested-tab-name"></a>5. 提供建议的选项卡名称

在添加频道或组选项卡时，默认情况下，应用名称会显示 (例如， **第一个应用程序** ) 。

这可能会很好，具体取决于您调用应用程序的内容，但您可能希望提供一个名称，以便在组协作的上下文中更有意义 (例如， **工作组联系人** ) 。

在中 `TabConfig.js` ，转到 `microsoftTeams.settings.setSettings` 。 添加 `suggestedDisplayName` 默认情况下要显示的选项卡名称的属性 (如) 所示。 使用提供的名称或创建自己的名称。  (默认情况下，用户可以根据需要更改名称。 ) 

```JavaScript
microsoftTeams.settings.setSettings({
  "contentUrl": "https://localhost:3000/tab",
  "suggestedDisplayName": "Team Contacts"
});
```

## <a name="6-build-and-run-your-app"></a>6. 生成并运行应用程序

在时间方面，你将在本地构建和运行应用程序。

 (工具包中也提供了此信息 `README` 。 ) 

1. 在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。
1. 运行 `npm start` 。

完成后，已 **成功编译了！** 终端中的邮件。 您的应用程序正在运行 `https://localhost:3000` 。

## <a name="7-sideload-your-app-in-teams"></a>7. 在团队中旁加载您的应用程序

您的应用程序已准备好在团队中进行测试。 若要执行此操作，您必须具有允许应用旁加载的帐户。  (如果您不能确定，请了解如何获取 [团队开发帐户](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)。 ) 

1. 在 Visual Studio Code 中，按 **F5** 键以启动团队 web 客户端。
1. 若要在团队中显示应用内容，请指定您的应用程序的运行位置 (`localhost`) 是可信的：
   1. 默认情况下，在同一浏览器窗口中打开一个新选项卡 () 按 **F5** 后打开的。
   1. 转到 `https://localhost:3000/tab` ""，然后继续转到 "" 页。
1. 返回到 "团队"。 在对话框中，选择 " **添加到团队** " 或 " **添加到聊天** "，并找到可用于测试的频道或聊天。
1. 选择 **"设置选项卡"** 。"配置" 页将显示在对话框中。<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content.png" alt-text="频道选项卡配置页的屏幕截图。":::
1. 选择 " **保存** " 以配置选项卡。将显示内容页。<br/>
   :::image type="content" source="../assets/images/tabs/channel-tab-tutorial-content-installed.png" alt-text="包含静态内容视图的频道选项卡的屏幕截图。":::

## <a name="well-done"></a>干的好

祝贺你！ 您有一个包含选项卡的团队应用程序，用于在频道和聊天中显示有用的内容。

## <a name="learn-more"></a>了解更多

* [使用 Sso 对选项卡用户进行身份验证](../tabs/how-to/authentication/auth-aad-sso.md)：如果您仅希望授权用户查看您的选项卡，请通过 Azure Active DIRECTORY (AD) 设置单一登录 (SSO) 。
* [从现有 web 应用或网页嵌入内容](../tabs/how-to/add-tab.md#tab-requirements)：我们向您介绍了如何为个人选项卡创建新内容，但您也可以从外部 URL 加载内容。
* [为您的选项卡创建无缝体验](../tabs/design/tabs.md)：有关设计团队选项卡的建议指南，请参阅。
* [为移动设备构建选项卡](../tabs/design/tabs-mobile.md)：了解如何为电话和平板电脑开发选项卡。
* [使用 Microsoft Graph API 的团队数据](https://docs.microsoft.com/graph/teams-concept-overview)
* [创建不带工具箱的选项卡](../tabs/how-to/add-tab.md)

## <a name="next-lesson"></a>下一课

您知道如何构建协作选项卡。 想要尝试构建不同种类的团队应用吗？

> [!div class="nextstepaction"]
> [创建机器人](../build-your-first-app/build-bot.md)
