---
title: 使用 node.js 和 Microsoft 团队的 Yeoman 生成器创建自定义频道和组选项卡
author: laujan
description: 用于创建带有 Microsoft 团队的 Yeoman 生成器的频道和分组选项卡的快速入门指南。
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: c5e028dcc117d729f2bf366923d03568b7f557a4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673204"
---
# <a name="create-a-custom-channel-and-group-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>使用 node.js 和 Microsoft 团队的 Yeoman 生成器创建自定义频道和组选项卡

>[!NOTE]
>此快速入门遵循在 Microsoft OfficeDev GitHub 存储库中[构建您的第一个 Microsoft 团队应用程序](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)Wiki 中概述的步骤。

在此快速入门中，我们将介绍如何使用[团队 Yeoman 生成器](https://github.com/OfficeDev/generator-teams/)创建自定义通道和分组选项卡。

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**是否要创建 "可配置" 或 "静态" 选项卡？**

使用箭头键选择 "可配置" 选项卡。

**您打算将哪些范围用于您的选项卡？**

您可以选择团队和/或组聊天

**您是否希望此选项卡在 SharePoint Online 中可用？（Y/n）** 

选择 " **n**"。

>[!IMPORTANT]
>此快速入门中引用的路径组件**yourDefaultTabNameTab**，是您在**默认选项卡名称**和 "word"**选项卡**的生成器中输入的值。
>
>例如： DefaultTabName： **MyTab** => **/MyTabTab/**

在项目目录中，导航到以下内容：

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

可以在其中找到您的选项卡逻辑。 找到`render()`方法，并将以下`<div>`标签和内容添加到`<PanelBody>`容器代码的顶部：

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

请务必保存更新后的文件。

## <a name="build-and-run-your-application"></a>生成并运行应用程序

在项目目录中打开命令提示符以完成后续任务。

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

若要查看您的选项卡配置`https://localhost:3007/<yourDefaultAppNameTab>/config.html`页，请转到。 应看到以下内容：

![配置页面屏幕截图](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到您的选项卡的安全隧道

Microsoft 团队是完全基于云的产品，要求使用 HTTPS 终结点从云中获取你的选项卡内容。 团队不允许本地托管，因此，您需要将选项卡发布到公用 URL，或使用将本地端口公开给面向 internet 的 URL 的代理。

若要测试您的选项卡扩展，您将使用内置于此应用程序中的[ngrok](https://ngrok.com/docs)。 Ngrok 是一种反向代理软件工具，它将创建到本地运行的 web 服务器的公开可用 HTTPS 终结点的隧道。 您的服务器的 web 终结点将在本地计算机上的当前会话过程中可用。 当计算机关闭或进入睡眠状态时，该服务将不再可用。

在命令提示符下，退出 localhost 并输入以下内容：

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> 将选项卡上载到 Microsoft 团队并成功保存后，可以在 "选项卡" 库中查看它，将其添加到选项卡栏，并与之交互，直到 ngrok 隧道会话结束。 如果重新启动 ngrok 会话，则需要使用新的 URL 更新应用程序。

## <a name="upload-your-application-to-teams"></a>将应用程序上载到团队

- 打开 Microsoft 团队客户端。 如果您使用的是[基于 web 的版本](https://teams.microsoft.com)，则可以使用浏览器的[开发人员工具](~/tabs/how-to/developer-tools.md)检查您的前端代码。
- 在左侧的 " *YourTeams* " 面板中，选择`...`要用于测试选项卡的团队旁边的菜单，然后选择 "**管理团队**"。
- 在主面板中，从选项卡栏中选择 "**应用**"，然后选择 "上载" 位于页面右下角的**自定义应用程序**。
- 打开您的项目目录，浏览到 " **/package** " 文件夹，选择 "应用程序包" zip 文件夹，然后选择 "**打开**"。 您的选项卡将上传到团队。
- 返回到您的团队，选择要在其中显示选项卡的频道，从选项卡栏中选择 "➕"，然后从库中选择您的选项卡。
- 按照说明添加选项卡。请注意，"频道/组" 选项卡有一个自定义配置对话框。
- 选择 "**保存**"，您的选项卡将添加到频道的选项卡栏中。
