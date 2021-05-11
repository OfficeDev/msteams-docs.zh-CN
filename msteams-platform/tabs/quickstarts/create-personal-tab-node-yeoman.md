---
title: 快速入门：使用 Node.js 和 Yeoman 生成器为用户创建自定义Microsoft Teams
author: laujan
description: 使用 Yeoman 生成器为用户创建个人选项卡的快速Microsoft Teams。
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
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="c2889-103">快速入门：使用 Node.js 和 Yeoman 生成器为用户创建自定义Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="c2889-103">Quickstart: Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="c2889-104">本快速入门遵循 Microsoft OfficeDev Microsoft Teams存储库中的构建第一个 Microsoft Teams [App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki 中概述GitHub步骤。</span><span class="sxs-lookup"><span data-stu-id="c2889-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="c2889-105">在此快速入门中，我们将演练使用[Yeoman](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)生成器创建自定义Teams选项卡。</span><span class="sxs-lookup"><span data-stu-id="c2889-105">In this quickstart we'll walk-through creating a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="c2889-106">我们还将应用程序上载到 Team。</span><span class="sxs-lookup"><span data-stu-id="c2889-106">We'll also upload the application to Team.</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="c2889-107">**是否要创建可配置选项卡或静态选项卡？**</span><span class="sxs-lookup"><span data-stu-id="c2889-107">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="c2889-108">使用箭头键选择静态选项卡。</span><span class="sxs-lookup"><span data-stu-id="c2889-108">Use the arrow keys to select static tab.</span></span>

>[!IMPORTANT]
><span data-ttu-id="c2889-109">本快速入门中引用的路径组件 *yourDefaultTabNameTab* 是在生成器中为" *默认* 选项卡名称"加上单词 *"Tab"输入的值*。</span><span class="sxs-lookup"><span data-stu-id="c2889-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span></span>
>
><span data-ttu-id="c2889-110">例如：DefaultTabName：MyTab   =>  */MyTabTab/*</span><span class="sxs-lookup"><span data-stu-id="c2889-110">For example: DefaultTabName: *MyTab* => */MyTabTab/*</span></span>

## <a name="create-your-personal-tab"></a><span data-ttu-id="c2889-111">创建个人选项卡</span><span class="sxs-lookup"><span data-stu-id="c2889-111">Create your personal tab</span></span>

<span data-ttu-id="c2889-112">若要将个人选项卡添加到此应用程序，您将创建一个内容页并更新现有文件：</span><span class="sxs-lookup"><span data-stu-id="c2889-112">To add a personal tab to this application you'll create a content page and update existing files:</span></span>

- <span data-ttu-id="c2889-113">在代码编辑器中，新建 HTML 文件，personal.htm **l** 并添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="c2889-113">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

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

- <span data-ttu-id="c2889-114">在 **personal.htm** Web 文件夹中保存personal.htm **l：**</span><span class="sxs-lookup"><span data-stu-id="c2889-114">Save **personal.html** in your application's **web** folder:</span></span>

```bash
./src/app/web/<yourDefaultTabNameTab>/personal.html
```

- <span data-ttu-id="c2889-115">在 **manifest.js** 打开"打开"：</span><span class="sxs-lookup"><span data-stu-id="c2889-115">Open **manifest.json** in your code editor:</span></span>

```bash
./src/manifest/manifest.json/
```

<span data-ttu-id="c2889-116">将以下内容添加到空 `staticTabs` 数组 `staticTabs":[]` () 并添加以下 JSON 对象：</span><span class="sxs-lookup"><span data-stu-id="c2889-116">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

<span data-ttu-id="c2889-117">请记住使用实际选项卡 **名称更新"contentURL"** 路径组件 **yourDefaultTabNameTab。**</span><span class="sxs-lookup"><span data-stu-id="c2889-117">Remember to update the **"contentURL"** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

- <span data-ttu-id="c2889-118">将更新manifest.js **保存到 上**。</span><span class="sxs-lookup"><span data-stu-id="c2889-118">Save the updated **manifest.json**.</span></span>

- <span data-ttu-id="c2889-119">必须在 IFrame 中提供内容页。</span><span class="sxs-lookup"><span data-stu-id="c2889-119">Your content page must be served in an IFrame.</span></span> <span data-ttu-id="c2889-120">在 **代码编辑器中打开 Tab.ts：**</span><span class="sxs-lookup"><span data-stu-id="c2889-120">Open **Tab.ts** in your code editor:</span></span>

 ```bash
./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
```

- <span data-ttu-id="c2889-121">将以下内容添加到 IFrame 修饰符列表中：</span><span class="sxs-lookup"><span data-stu-id="c2889-121">Add the following to the list of IFrame decorators:</span></span>

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
```

- <span data-ttu-id="c2889-122">确保保存更新的 **Tab.ts** 文件。</span><span class="sxs-lookup"><span data-stu-id="c2889-122">Make sure to save the updated **Tab.ts** file.</span></span> <span data-ttu-id="c2889-123">您的选项卡代码已完成。</span><span class="sxs-lookup"><span data-stu-id="c2889-123">Your tab code is complete.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="c2889-124">生成并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="c2889-124">Build and Run Your Application</span></span>

<span data-ttu-id="c2889-125">在项目目录中打开命令提示符以完成下一个任务。</span><span class="sxs-lookup"><span data-stu-id="c2889-125">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="c2889-126">若要查看你的个人选项卡，请转到 `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span><span class="sxs-lookup"><span data-stu-id="c2889-126">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span></span>

>![个人选项卡屏幕截图](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="c2889-128">建立到选项卡的安全隧道</span><span class="sxs-lookup"><span data-stu-id="c2889-128">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="c2889-129">Microsoft Teams完全基于云的产品，并且要求使用 HTTPS 终结点从云中提供选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="c2889-129">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="c2889-130">Teams不允许本地托管，因此，你需要将选项卡发布到公用 URL 或使用将本地端口公开给面向 Internet 的 URL 的代理。</span><span class="sxs-lookup"><span data-stu-id="c2889-130">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="c2889-131">若要测试选项卡扩展，你将使用内置于此应用程序中的[ngrok。](https://ngrok.com/docs)</span><span class="sxs-lookup"><span data-stu-id="c2889-131">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="c2889-132">Ngrok 是反向代理软件工具，它将创建到本地运行的 Web 服务器公开可用的 HTTPS 终结点的隧道。</span><span class="sxs-lookup"><span data-stu-id="c2889-132">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="c2889-133">你的服务器的 Web 终结点将在本地计算机上在当前会话期间可用。</span><span class="sxs-lookup"><span data-stu-id="c2889-133">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="c2889-134">当计算机关闭或进入睡眠状态时，服务将不再可用。</span><span class="sxs-lookup"><span data-stu-id="c2889-134">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="c2889-135">在命令提示符中，退出 localhost 并输入以下内容：</span><span class="sxs-lookup"><span data-stu-id="c2889-135">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="c2889-136">通过 *ngrok* 将选项卡上传到 Microsoft 团队并成功保存后，可以在 Teams 中查看它，直到隧道会话结束。</span><span class="sxs-lookup"><span data-stu-id="c2889-136">After your tab has been uploaded to Microsoft teams, via *ngrok*, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="c2889-137">Upload应用程序以Teams</span><span class="sxs-lookup"><span data-stu-id="c2889-137">Upload your application to Teams</span></span>

- <span data-ttu-id="c2889-138">打开 Microsoft Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="c2889-138">Open the Microsoft Teams client.</span></span> <span data-ttu-id="c2889-139">如果使用基于 [Web 的版本，](https://teams.microsoft.com) 可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="c2889-139">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="c2889-140">在左侧 *的 YourTeams* 面板中，选择用于测试选项卡的团队旁边的菜单，然后选择 `...` "**管理团队"。**</span><span class="sxs-lookup"><span data-stu-id="c2889-140">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="c2889-141">在主面板中，从选项卡栏中选择"应用"，Upload位于页面右下角的自定义应用。 </span><span class="sxs-lookup"><span data-stu-id="c2889-141">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="c2889-142">打开项目目录，浏览到 **./package** 文件夹，选择 zip 文件夹，右键单击，然后选择"打开 **"。**</span><span class="sxs-lookup"><span data-stu-id="c2889-142">Open your project directory, browse to the **./package** folder, select the zip folder, right-click, and choose **Open**.</span></span> <span data-ttu-id="c2889-143">您的选项卡将上载到Teams。</span><span class="sxs-lookup"><span data-stu-id="c2889-143">Your tab will upload into Teams.</span></span>

## <a name="view-your-personal-tabs"></a><span data-ttu-id="c2889-144">查看个人选项卡</span><span class="sxs-lookup"><span data-stu-id="c2889-144">View your personal tabs</span></span>

<span data-ttu-id="c2889-145">在位于客户端最左侧的导航Teams，选择菜单，然后 `...` 从列表中选择你的应用。</span><span class="sxs-lookup"><span data-stu-id="c2889-145">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>
