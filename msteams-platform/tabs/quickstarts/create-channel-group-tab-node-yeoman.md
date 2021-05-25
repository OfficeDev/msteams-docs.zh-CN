---
title: 使用自定义频道和组选项卡Node.js Yeoman 生成器进行Microsoft Teams
author: laujan
description: 使用 Yeoman 生成器为用户创建频道和组选项卡的快速Microsoft Teams。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 70b1dbe5a5abafa44ddbdf9045c55a33cf8fcb20
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630236"
---
# <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>使用自定义频道和组选项卡，Node.js Yeoman 生成器进行Microsoft Teams

>[!NOTE]
>本快速入门遵循 Microsoft OfficeDev Microsoft Teams存储库中的构建第一个 Microsoft Teams [App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki 中概述GitHub步骤。

在此快速入门中，我们将演练使用[Yeoman](https://github.com/OfficeDev/generator-teams/)生成器创建自定义频道Teams选项卡。

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**是否要创建可配置选项卡或静态选项卡？**

使用箭头键选择可配置的选项卡。

**您打算对 Tab 使用哪些范围？**

可以选择团队和/或群聊

**是否希望此选项卡在 SharePoint Online 中可用？ (Y/n)** 

选择 **n**。

>[!IMPORTANT]
>本快速入门中引用的路径组件 **yourDefaultTabNameTab** 是在生成器中为" **默认** 选项卡名称"加上单词 **"Tab"输入的值**。
>
>例如：DefaultTabName：MyTab   =>  **/MyTabTab/**

在项目目录中，导航到以下内容：

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

你将在这里找到选项卡逻辑。 找到 `render()` 方法，将以下 `<div>` 标记和内容添加到容器 `<PanelBody>` 代码的顶部：

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

确保保存更新后的文件。

## <a name="build-and-run-your-application"></a>生成并运行应用程序

在项目目录中打开命令提示符以完成下一个任务。

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

若要查看选项卡配置页面，请转到 `https://localhost:3007/<yourDefaultAppNameTab>/config.html` 。 应看到以下内容：

![配置页面屏幕截图](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到选项卡的安全隧道

Microsoft Teams完全基于云的产品，并且要求使用 HTTPS 终结点从云中提供选项卡内容。 Teams不允许本地托管，因此，你需要将选项卡发布到公用 URL 或使用将本地端口公开给面向 Internet 的 URL 的代理。

若要测试选项卡扩展，你将使用内置于此应用程序中的[ngrok。](https://ngrok.com/docs) Ngrok 是反向代理软件工具，它将创建到本地运行的 Web 服务器公开可用的 HTTPS 终结点的隧道。 你的服务器的 Web 终结点将在本地计算机上在当前会话期间可用。 当计算机关闭或进入睡眠状态时，服务将不再可用。

在命令提示符中，退出 localhost 并输入以下内容：

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> 将选项卡上传到 Microsoft 团队并成功保存后，可以在选项卡库中查看它，将其添加到选项卡栏，并与其交互，直到 ngrok 隧道会话结束。 如果重新启动 ngrok 会话，将需要使用新的 URL 更新应用。

## <a name="upload-your-application-to-teams"></a>Upload应用程序以Teams

- 打开 Microsoft Teams 客户端。 如果使用基于 [Web 的版本，](https://teams.microsoft.com) 可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。
- 在左侧 *的 YourTeams* 面板中，选择用于测试选项卡的团队旁边的菜单，然后选择 `...` "**管理团队"。**
- 在主面板中，从选项卡栏中选择"应用"，Upload位于页面右下角的自定义应用。 
- 打开项目目录，浏览到 **./package** 文件夹，选择应用包 zip 文件夹并选择"打开 **"。** 您的选项卡将上载到Teams。
- 返回到团队，选择要显示选项卡的频道，从选项卡➕选择选项卡，然后从库中选择您的选项卡。
- 按照添加选项卡的说明操作。请注意，频道/组选项卡有一个自定义配置对话框。
- 选择 **"** 保存"，您的选项卡将添加到频道的选项卡栏中。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [使用 ASP.NETCore 创建自定义频道和组选项卡](~/tabs/quickstarts/create-channel-group-tab-dotnet-core.md)
