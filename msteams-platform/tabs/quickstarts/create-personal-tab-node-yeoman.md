---
title: 快速入门：使用 Microsoft Teams Node.js Yeoman 生成器创建自定义个人选项卡
author: laujan
description: 使用适用于 Microsoft Teams 的 Yeoman 生成器创建个人选项卡的快速入门指南。
localization_priority: Normal
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 30143fa3c84a68ae6c34176b252badaa4cef9613
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019550"
---
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a>快速入门：使用 Microsoft Teams Node.js Yeoman 生成器创建自定义个人选项卡

>[!NOTE]
>本快速入门遵循 Microsoft OfficeDev GitHub 存储库中的构建 [首个 Microsoft Teams 应用](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki 中概述的步骤。

在此快速入门中，我们将演练使用 [Teams Yeoman](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)生成器创建自定义个人选项卡。 我们还将应用程序上载到 Team。

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

**是否要创建可配置选项卡或静态选项卡？**

使用箭头键选择静态选项卡。

>[!IMPORTANT]
>本快速入门中引用的路径组件 *yourDefaultTabNameTab* 是在生成器中为" *默认* 选项卡名称"加上单词 *"Tab"输入的值*。
>
>例如：DefaultTabName：MyTab   =>  */MyTabTab/*

## <a name="create-your-personal-tab"></a>创建个人选项卡

若要将个人选项卡添加到此应用程序，您将创建一个内容页并更新现有文件：

- 在代码编辑器中，新建 HTML 文件，personal.htm **l** 并添加以下标记：

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

- 在 **personal.htm** Web 文件夹中保存personal.htm **l：**

```bash
./src/app/web/<yourDefaultTabNameTab>/personal.html
```

- 在 **manifest.js** 打开"打开"：

```bash
./src/manifest/manifest.json/
```

将以下内容添加到空 `staticTabs` 数组 `staticTabs":[]` () 并添加以下 JSON 对象：

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

请记住使用实际选项卡 **名称更新"contentURL"** 路径组件 **yourDefaultTabNameTab。**

- 将更新manifest.js **保存到 上**。

- 必须在 IFrame 中提供内容页。 在 **代码编辑器中打开 Tab.ts：**

 ```bash
./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
```

- 将以下内容添加到 IFrame 修饰符列表中：

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
```

- 确保保存更新的 **Tab.ts** 文件。 您的选项卡代码已完成。

## <a name="build-and-run-your-application"></a>生成并运行应用程序

在项目目录中打开命令提示符以完成下一个任务。

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

若要查看你的个人选项卡，请转到 `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`

>![个人选项卡屏幕截图](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a>建立到选项卡的安全隧道

Microsoft Teams 是完全基于云的产品，要求使用 HTTPS 终结点从云中提供选项卡内容。 Teams 不允许本地托管，因此，你需要将选项卡发布到公用 URL 或使用将本地端口公开给面向 Internet 的 URL 的代理。

若要测试选项卡扩展，你将使用内置于此应用程序中的[ngrok。](https://ngrok.com/docs) Ngrok 是反向代理软件工具，它将创建到本地运行的 Web 服务器公开可用的 HTTPS 终结点的隧道。 你的服务器的 Web 终结点将在本地计算机上在当前会话期间可用。 当计算机关闭或进入睡眠状态时，服务将不再可用。

在命令提示符中，退出 localhost 并输入以下内容：

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> 通过 *ngrok* 将选项卡上传到 Microsoft 团队并成功保存后，可以在 Teams 中查看它，直到隧道会话结束。

## <a name="upload-your-application-to-teams"></a>将应用程序上传到 Teams

- 打开 Microsoft Teams 客户端。 如果使用基于 [Web 的版本，](https://teams.microsoft.com) 可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。
- 在左侧 *的 YourTeams* 面板中，选择用于测试选项卡的团队旁边的菜单，然后选择 `...` "**管理团队"。**
- 在主面板中，**从选项卡** 栏中选择"应用"，然后选择"上载位于页面右下角的自定义应用"。 
- 打开项目目录，浏览到 **./package** 文件夹，选择 zip 文件夹，右键单击，然后选择"打开 **"。** 你的选项卡将上传到 Teams。

## <a name="view-your-personal-tabs"></a>查看个人选项卡

在位于 Teams 客户端最左侧的导航栏中，选择菜单， `...` 然后从列表中选择你的应用。
