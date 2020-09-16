---
title: 快速入门：使用 Node.js 创建自定义个人选项卡和 Microsoft 团队的 Yeoman 生成器
author: laujan
description: 用于使用 Microsoft 团队的 Yeoman 生成器创建个人选项卡的快速入门指南。
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: e39878d117b0b1b1f8c0e2450021d9238f5b7877
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818883"
---
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>快速入门：使用 Node.js 创建自定义个人选项卡和 Microsoft 团队的 Yeoman 生成器

>[!NOTE]
>此快速入门遵循在 Microsoft OfficeDev GitHub 存储库中 [构建您的第一个 Microsoft 团队应用程序](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki 中概述的步骤。

在此快速入门中，我们将介绍如何使用 [团队 Yeoman 生成器](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)创建自定义个人选项卡。 我们还将把应用程序上传到团队。

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**是否要创建 "可配置" 或 "静态" 选项卡？**

使用箭头键选择 "静态" 选项卡。

>[!IMPORTANT]
>此快速入门中引用的路径组件 *yourDefaultTabNameTab*，是您在 *默认选项卡名称* 和 "word" *选项卡*的生成器中输入的值。
>
>例如： DefaultTabName： *MyTab*  =>  */MyTabTab/*

## <a name="create-your-personal-tab"></a>创建您的个人选项卡

若要将 "个人" 选项卡添加到此应用程序，您将创建内容页并更新现有文件：

- 在代码编辑器中，创建一个新的 HTML 文件， **personal.html** ，然后添加以下标记：

```html
<!DOCTYPE html>
<html>
    <head>
        <meta charset="UTF-8">
        <title>
            <!-- Todo: add your a title here -->
        </title>
        <meta name="viewport" content="width=device-width, initial-scale=1.0">
        <!-- inject:css -->
        <!-- endinject -->
    </head>
        <body>
            <h1>Personal Tab</h1>
            <p><img src="/assets/icon.png"></p>
            <p>This is your personal tab!</p>
        </body>
</html>
```

- 将 **personal.html** 保存在应用程序的 **web** 文件夹中：

```bash
./src/app/web/<yourDefaultTabNameTab>/personal.html
```

- 在代码编辑器中打开 **manifest.js** ：

```bash
./src/manifest/manifest.json/
```

将以下内容添加到 `staticTabs` () 的空数组中 `staticTabs":[]` ，并添加以下 JSON 对象：

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

请记住使用实际的选项卡名称更新 **"contentURL"** 路径组件 **yourDefaultTabNameTab** 。

- 将更新的 **manifest.js保存在上**。

- 必须在 IFrame 中提供您的内容页面。 在代码编辑器中打开 **"Ts"** ：

 ```bash
./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
```

- 将以下内容添加到 IFrame decorators 的列表中：

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
```

- 请务必保存已更新的**选项卡。** 您的选项卡代码已完成。

## <a name="build-and-run-your-application"></a>生成并运行应用程序

在项目目录中打开命令提示符以完成后续任务。

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

若要查看您的个人选项卡，请转到 `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`

>![个人选项卡屏幕截图](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到您的选项卡的安全隧道

Microsoft 团队是完全基于云的产品，要求使用 HTTPS 终结点从云中获取你的选项卡内容。 团队不允许本地托管，因此，您需要将选项卡发布到公用 URL，或使用将本地端口公开给面向 internet 的 URL 的代理。

若要测试您的选项卡扩展，您将使用内置于此应用程序中的 [ngrok](https://ngrok.com/docs)。 Ngrok 是一种反向代理软件工具，它将创建到本地运行的 web 服务器的公开可用 HTTPS 终结点的隧道。 您的服务器的 web 终结点将在本地计算机上的当前会话过程中可用。 当计算机关闭或进入睡眠状态时，该服务将不再可用。

在命令提示符下，退出 localhost 并输入以下内容：

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> 在将选项卡上载到 Microsoft 团队后，通过 *ngrok*并成功保存后，您可以在您的隧道会话结束之前在团队中查看它。

## <a name="upload-your-application-to-teams"></a>将应用程序上载到团队

- 打开 Microsoft 团队客户端。 如果您使用的是 [基于 web 的版本](https://teams.microsoft.com) ，则可以使用浏览器的 [开发人员工具](~/tabs/how-to/developer-tools.md)检查您的前端代码。
- 在左侧的 " *YourTeams* " 面板中，选择要用于 `...` 测试选项卡的团队旁边的菜单，然后选择 " **管理团队**"。
- 在主面板中，从选项卡栏中选择 " **应用** "，然后选择 "上载" 位于页面右下角的 **自定义应用程序** 。
- 打开项目目录，浏览到 " **./package** " 文件夹，选择 "zip" 文件夹，右键单击，然后选择 " **打开**"。 您的选项卡将上传到团队。

## <a name="view-your-personal-tabs"></a>查看你的个人选项卡

在位于团队客户端最左侧的导航栏中，选择 `...` 菜单并从列表中选择您的应用程序。
