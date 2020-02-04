---
title: 快速入门：使用 node.js 和 Microsoft 团队的 Yeoman 生成器创建自定义个人选项卡
author: laujan
description: 用于使用 Microsoft 团队的 Yeoman 生成器创建个人选项卡的快速入门指南。
ms.topic: quickstart
ms.author: laujan
ms.openlocfilehash: 2d1b17360b92a161179091c1f6ba06ffa194e958
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41672989"
---
# <a name="quickstart-create-a-custom-personal-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="9312e-103">快速入门：使用 node.js 和 Microsoft 团队的 Yeoman 生成器创建自定义个人选项卡</span><span class="sxs-lookup"><span data-stu-id="9312e-103">Quickstart: Create a custom personal tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="9312e-104">此快速入门遵循在 Microsoft OfficeDev GitHub 存储库中[构建您的第一个 Microsoft 团队应用程序](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)Wiki 中概述的步骤。</span><span class="sxs-lookup"><span data-stu-id="9312e-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="9312e-105">在此快速入门中，我们将介绍如何使用[团队 Yeoman 生成器](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App)创建自定义个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="9312e-105">In this quickstart we'll walk-through creating a custom personal tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App).</span></span> <span data-ttu-id="9312e-106">我们还将把应用程序上传到团队。</span><span class="sxs-lookup"><span data-stu-id="9312e-106">We'll also upload the application to Team.</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="9312e-107">**是否要创建 "可配置" 或 "静态" 选项卡？**</span><span class="sxs-lookup"><span data-stu-id="9312e-107">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="9312e-108">使用箭头键选择 "静态" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="9312e-108">Use the arrow keys to select static tab.</span></span>

>[!IMPORTANT]
><span data-ttu-id="9312e-109">此快速入门中引用的路径组件*yourDefaultTabNameTab*，是您在*默认选项卡名称*和 "word"*选项卡*的生成器中输入的值。</span><span class="sxs-lookup"><span data-stu-id="9312e-109">The path component *yourDefaultTabNameTab*, referenced in this quickstart, is the value that you entered in the generator for *Default Tab Name* plus the word *Tab*.</span></span>
>
><span data-ttu-id="9312e-110">例如： DefaultTabName： *MyTab* => */MyTabTab/*</span><span class="sxs-lookup"><span data-stu-id="9312e-110">For example: DefaultTabName: *MyTab* => */MyTabTab/*</span></span>

## <a name="create-your-personal-tab"></a><span data-ttu-id="9312e-111">创建您的个人选项卡</span><span class="sxs-lookup"><span data-stu-id="9312e-111">Create your personal tab</span></span>

<span data-ttu-id="9312e-112">若要将 "个人" 选项卡添加到此应用程序，您将创建内容页并更新现有文件：</span><span class="sxs-lookup"><span data-stu-id="9312e-112">To add a personal tab to this application you'll create a content page and update existing files:</span></span>

- <span data-ttu-id="9312e-113">在代码编辑器中，创建一个新的 HTML 文件 " **personal .html** "，并添加以下标记：</span><span class="sxs-lookup"><span data-stu-id="9312e-113">In your code editor, create a new HTML file, **personal.html** and add the following markup:</span></span>

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

- <span data-ttu-id="9312e-114">在您的应用程序的**web**文件夹中保存**个人版 .html** ：</span><span class="sxs-lookup"><span data-stu-id="9312e-114">Save **personal.html** in your application's **web** folder:</span></span>

```bash
./src/app/web/<yourDefaultTabNameTab>/personal.html
```

- <span data-ttu-id="9312e-115">在代码编辑器中打开**manifest json** ：</span><span class="sxs-lookup"><span data-stu-id="9312e-115">Open **manifest.json** in your code editor:</span></span>

```bash
./src/manifest/manifest.json/
```

<span data-ttu-id="9312e-116">将以下内容添加到空`staticTabs`数组（`staticTabs":[]`）中，并添加以下 JSON 对象：</span><span class="sxs-lookup"><span data-stu-id="9312e-116">Add the following to the empty `staticTabs` array (`staticTabs":[]`) and add the following JSON object:</span></span>

```json
{
    "entityId": "personalTab",
    "name": "Personal Tab ",
    "contentUrl": "https://{{HOSTNAME}}/<yourDefaultTabNameTab>/personal.html",
    "websiteUrl": "https://{{HOSTNAME}}",
    "scopes": ["personal"]
}

```

<span data-ttu-id="9312e-117">请记住使用实际的选项卡名称更新 **"contentURL"** 路径组件**yourDefaultTabNameTab** 。</span><span class="sxs-lookup"><span data-stu-id="9312e-117">Remember to update the **"contentURL"** path component **yourDefaultTabNameTab** with your actual tab name.</span></span>

- <span data-ttu-id="9312e-118">保存更新的**清单 json**。</span><span class="sxs-lookup"><span data-stu-id="9312e-118">Save the updated **manifest.json**.</span></span>

- <span data-ttu-id="9312e-119">必须在 IFrame 中提供您的内容页面。</span><span class="sxs-lookup"><span data-stu-id="9312e-119">Your content page must be served in an IFrame.</span></span> <span data-ttu-id="9312e-120">在代码编辑器中打开 **"Ts"** ：</span><span class="sxs-lookup"><span data-stu-id="9312e-120">Open **Tab.ts** in your code editor:</span></span>

 ```bash
./src/app/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.ts
```

- <span data-ttu-id="9312e-121">将以下内容添加到 IFrame decorators 的列表中：</span><span class="sxs-lookup"><span data-stu-id="9312e-121">Add the following to the list of IFrame decorators:</span></span>

```typescript
 @PreventIframe("/<yourDefaultAppName>TabNameTab>/personal.html")
```

- <span data-ttu-id="9312e-122">请务必保存已更新的**选项卡。**</span><span class="sxs-lookup"><span data-stu-id="9312e-122">Make sure to save the updated **Tab.ts** file.</span></span> <span data-ttu-id="9312e-123">您的选项卡代码已完成。</span><span class="sxs-lookup"><span data-stu-id="9312e-123">Your tab code is complete.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="9312e-124">生成并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="9312e-124">Build and Run Your Application</span></span>

<span data-ttu-id="9312e-125">在项目目录中打开命令提示符以完成后续任务。</span><span class="sxs-lookup"><span data-stu-id="9312e-125">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="9312e-126">若要查看您的个人选项卡，请转到`http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span><span class="sxs-lookup"><span data-stu-id="9312e-126">To view your personal tab, go to `http://localhost:3007/<yourDefaultAppNameTab>/personal.html`</span></span>

>![个人选项卡屏幕截图](/microsoftteams/platform/assets/images/tab-images/personalTab.PNG)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="9312e-128">建立到您的选项卡的安全隧道</span><span class="sxs-lookup"><span data-stu-id="9312e-128">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="9312e-129">Microsoft 团队是完全基于云的产品，要求使用 HTTPS 终结点从云中获取你的选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="9312e-129">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="9312e-130">团队不允许本地托管，因此，您需要将选项卡发布到公用 URL，或使用将本地端口公开给面向 internet 的 URL 的代理。</span><span class="sxs-lookup"><span data-stu-id="9312e-130">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="9312e-131">若要测试您的选项卡扩展，您将使用内置于此应用程序中的[ngrok](https://ngrok.com/docs)。</span><span class="sxs-lookup"><span data-stu-id="9312e-131">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="9312e-132">Ngrok 是一种反向代理软件工具，它将创建到本地运行的 web 服务器的公开可用 HTTPS 终结点的隧道。</span><span class="sxs-lookup"><span data-stu-id="9312e-132">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="9312e-133">您的服务器的 web 终结点将在本地计算机上的当前会话过程中可用。</span><span class="sxs-lookup"><span data-stu-id="9312e-133">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="9312e-134">当计算机关闭或进入睡眠状态时，该服务将不再可用。</span><span class="sxs-lookup"><span data-stu-id="9312e-134">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="9312e-135">在命令提示符下，退出 localhost 并输入以下内容：</span><span class="sxs-lookup"><span data-stu-id="9312e-135">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="9312e-136">在将选项卡上载到 Microsoft 团队后，通过*ngrok*并成功保存后，您可以在您的隧道会话结束之前在团队中查看它。</span><span class="sxs-lookup"><span data-stu-id="9312e-136">After your tab has been uploaded to Microsoft teams, via *ngrok*, and successfully saved, you can view it in Teams until your tunnel session ends.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="9312e-137">将应用程序上载到团队</span><span class="sxs-lookup"><span data-stu-id="9312e-137">Upload your application to Teams</span></span>

- <span data-ttu-id="9312e-138">打开 Microsoft 团队客户端。</span><span class="sxs-lookup"><span data-stu-id="9312e-138">Open the Microsoft Teams client.</span></span> <span data-ttu-id="9312e-139">如果您使用的是[基于 web 的版本](https://teams.microsoft.com)，则可以使用浏览器的[开发人员工具](~/tabs/how-to/developer-tools.md)检查您的前端代码。</span><span class="sxs-lookup"><span data-stu-id="9312e-139">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="9312e-140">在左侧的 " *YourTeams* " 面板中，选择`...`要用于测试选项卡的团队旁边的菜单，然后选择 "**管理团队**"。</span><span class="sxs-lookup"><span data-stu-id="9312e-140">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="9312e-141">在主面板中，从选项卡栏中选择 "**应用**"，然后选择 "上载" 位于页面右下角的**自定义应用程序**。</span><span class="sxs-lookup"><span data-stu-id="9312e-141">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="9312e-142">打开项目目录，浏览到 " **./package** " 文件夹，选择 "zip" 文件夹，右键单击，然后选择 "**打开**"。</span><span class="sxs-lookup"><span data-stu-id="9312e-142">Open your project directory, browse to the **./package** folder, select the zip folder, right-click, and choose **Open**.</span></span> <span data-ttu-id="9312e-143">您的选项卡将上传到团队。</span><span class="sxs-lookup"><span data-stu-id="9312e-143">Your tab will upload into Teams.</span></span>

## <a name="view-your-personal-tabs"></a><span data-ttu-id="9312e-144">查看你的个人选项卡</span><span class="sxs-lookup"><span data-stu-id="9312e-144">View your personal tabs</span></span>

<span data-ttu-id="9312e-145">在位于团队客户端最左侧的导航栏中，选择`...`菜单并从列表中选择您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="9312e-145">In the navbar located at the far-left of the Teams client, select the `...` menu and choose your app from the list.</span></span>
