---
title: 使用 Node.js 和 Microsoft 团队的 Yeoman 生成器创建自定义频道和组选项卡
author: laujan
description: 用于创建带有 Microsoft 团队的 Yeoman 生成器的频道和分组选项卡的快速入门指南。
ms.topic: quickstart
ms.author: lajanuar
ms.openlocfilehash: 77081f83c753f812032ccfebe2accd3cb8859f99
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818932"
---
# <a name="create-a-custom-channel-and-group-tab-with-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="79d24-103">使用 Node.js 和 Microsoft 团队的 Yeoman 生成器创建自定义频道和组选项卡</span><span class="sxs-lookup"><span data-stu-id="79d24-103">Create a custom channel and group tab with Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="79d24-104">此快速入门遵循在 Microsoft OfficeDev GitHub 存储库中 [构建您的第一个 Microsoft 团队应用程序](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki 中概述的步骤。</span><span class="sxs-lookup"><span data-stu-id="79d24-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="79d24-105">在此快速入门中，我们将介绍如何使用 [团队 Yeoman 生成器](https://github.com/OfficeDev/generator-teams/)创建自定义通道和分组选项卡。</span><span class="sxs-lookup"><span data-stu-id="79d24-105">In this quickstart we'll walk-through creating a custom channel and group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="79d24-106">**是否要创建 "可配置" 或 "静态" 选项卡？**</span><span class="sxs-lookup"><span data-stu-id="79d24-106">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="79d24-107">使用箭头键选择 "可配置" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="79d24-107">Use the arrow keys to select configurable tab.</span></span>

<span data-ttu-id="79d24-108">**您打算将哪些范围用于您的选项卡？**</span><span class="sxs-lookup"><span data-stu-id="79d24-108">**What scopes do you intend to use for your Tab?**</span></span>

<span data-ttu-id="79d24-109">您可以选择团队和/或组聊天</span><span class="sxs-lookup"><span data-stu-id="79d24-109">You can select a Team and/or a group chat</span></span>

<span data-ttu-id="79d24-110">\*\*您是否希望此选项卡在 SharePoint Online 中可用？ (Y/n) \*\*</span><span class="sxs-lookup"><span data-stu-id="79d24-110">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span> 

<span data-ttu-id="79d24-111">选择 " **n**"。</span><span class="sxs-lookup"><span data-stu-id="79d24-111">Select **n**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="79d24-112">此快速入门中引用的路径组件 **yourDefaultTabNameTab**，是您在 **默认选项卡名称** 和 "word" **选项卡**的生成器中输入的值。</span><span class="sxs-lookup"><span data-stu-id="79d24-112">The path component **yourDefaultTabNameTab**, referenced in this quickstart, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
>
><span data-ttu-id="79d24-113">例如： DefaultTabName： **MyTab**  =>  **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="79d24-113">For example: DefaultTabName: **MyTab** => **/MyTabTab/**</span></span>

<span data-ttu-id="79d24-114">在项目目录中，导航到以下内容：</span><span class="sxs-lookup"><span data-stu-id="79d24-114">In your project directory, navigate to the following:</span></span>

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

<span data-ttu-id="79d24-115">可以在其中找到您的选项卡逻辑。</span><span class="sxs-lookup"><span data-stu-id="79d24-115">That is where you'll find your tab logic.</span></span> <span data-ttu-id="79d24-116">找到 `render()` 方法，并将以下 `<div>` 标签和内容添加到容器代码的顶部 `<PanelBody>` ：</span><span class="sxs-lookup"><span data-stu-id="79d24-116">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

<span data-ttu-id="79d24-117">请务必保存更新后的文件。</span><span class="sxs-lookup"><span data-stu-id="79d24-117">Make sure to save the updated file.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="79d24-118">生成并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="79d24-118">Build and Run Your Application</span></span>

<span data-ttu-id="79d24-119">在项目目录中打开命令提示符以完成后续任务。</span><span class="sxs-lookup"><span data-stu-id="79d24-119">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="79d24-120">若要查看您的选项卡配置页，请转到 `https://localhost:3007/<yourDefaultAppNameTab>/config.html` 。</span><span class="sxs-lookup"><span data-stu-id="79d24-120">To view your tab configuration page go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="79d24-121">应看到以下内容：</span><span class="sxs-lookup"><span data-stu-id="79d24-121">You should see the following:</span></span>

![配置页面屏幕截图](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="79d24-123">建立到您的选项卡的安全隧道</span><span class="sxs-lookup"><span data-stu-id="79d24-123">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="79d24-124">Microsoft 团队是完全基于云的产品，要求使用 HTTPS 终结点从云中获取你的选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="79d24-124">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="79d24-125">团队不允许本地托管，因此，您需要将选项卡发布到公用 URL，或使用将本地端口公开给面向 internet 的 URL 的代理。</span><span class="sxs-lookup"><span data-stu-id="79d24-125">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="79d24-126">若要测试您的选项卡扩展，您将使用内置于此应用程序中的 [ngrok](https://ngrok.com/docs)。</span><span class="sxs-lookup"><span data-stu-id="79d24-126">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="79d24-127">Ngrok 是一种反向代理软件工具，它将创建到本地运行的 web 服务器的公开可用 HTTPS 终结点的隧道。</span><span class="sxs-lookup"><span data-stu-id="79d24-127">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="79d24-128">您的服务器的 web 终结点将在本地计算机上的当前会话过程中可用。</span><span class="sxs-lookup"><span data-stu-id="79d24-128">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="79d24-129">当计算机关闭或进入睡眠状态时，该服务将不再可用。</span><span class="sxs-lookup"><span data-stu-id="79d24-129">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="79d24-130">在命令提示符下，退出 localhost 并输入以下内容：</span><span class="sxs-lookup"><span data-stu-id="79d24-130">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="79d24-131">将选项卡上载到 Microsoft 团队并成功保存后，可以在 "选项卡" 库中查看它，将其添加到选项卡栏，并与之交互，直到 ngrok 隧道会话结束。</span><span class="sxs-lookup"><span data-stu-id="79d24-131">After your tab has been uploaded to Microsoft teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="79d24-132">如果重新启动 ngrok 会话，则需要使用新的 URL 更新应用程序。</span><span class="sxs-lookup"><span data-stu-id="79d24-132">If you restart your ngrok session, you'll need to update your app with the new URL.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="79d24-133">将应用程序上载到团队</span><span class="sxs-lookup"><span data-stu-id="79d24-133">Upload your application to Teams</span></span>

- <span data-ttu-id="79d24-134">打开 Microsoft 团队客户端。</span><span class="sxs-lookup"><span data-stu-id="79d24-134">Open the Microsoft Teams client.</span></span> <span data-ttu-id="79d24-135">如果您使用的是 [基于 web 的版本](https://teams.microsoft.com) ，则可以使用浏览器的 [开发人员工具](~/tabs/how-to/developer-tools.md)检查您的前端代码。</span><span class="sxs-lookup"><span data-stu-id="79d24-135">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="79d24-136">在左侧的 " *YourTeams* " 面板中，选择要用于 `...` 测试选项卡的团队旁边的菜单，然后选择 " **管理团队**"。</span><span class="sxs-lookup"><span data-stu-id="79d24-136">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="79d24-137">在主面板中，从选项卡栏中选择 " **应用** "，然后选择 "上载" 位于页面右下角的 **自定义应用程序** 。</span><span class="sxs-lookup"><span data-stu-id="79d24-137">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="79d24-138">打开您的项目目录，浏览到 " **/package** " 文件夹，选择 "应用程序包" zip 文件夹，然后选择 " **打开**"。</span><span class="sxs-lookup"><span data-stu-id="79d24-138">Open your project directory, browse to the **./package** folder, select the app package zip folder and choose **Open**.</span></span> <span data-ttu-id="79d24-139">您的选项卡将上传到团队。</span><span class="sxs-lookup"><span data-stu-id="79d24-139">Your tab will upload into Teams.</span></span>
- <span data-ttu-id="79d24-140">返回到您的团队，选择要在其中显示选项卡的频道，从选项卡栏中选择 "➕"，然后从库中选择您的选项卡。</span><span class="sxs-lookup"><span data-stu-id="79d24-140">Return to your team, choose the channel where you would like to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
- <span data-ttu-id="79d24-141">按照有关添加选项卡的说明操作。请注意，"通道/组" 选项卡有一个自定义配置对话框。</span><span class="sxs-lookup"><span data-stu-id="79d24-141">Follow the directions for adding a tab. Note that there's a custom configuration dialog for your channel/group tab.</span></span>
- <span data-ttu-id="79d24-142">选择 " **保存** "，您的选项卡将添加到频道的选项卡栏中。</span><span class="sxs-lookup"><span data-stu-id="79d24-142">Select **Save** and your tab will be added to the channel's tab bar.</span></span>
