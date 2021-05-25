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
# <a name="create-a-custom-channel-and-group-tab-using-nodejs-and-the-yeoman-generator-for-microsoft-teams"></a><span data-ttu-id="fdc6c-103">使用自定义频道和组选项卡，Node.js Yeoman 生成器进行Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fdc6c-103">Create a custom channel and group tab using Node.js and the Yeoman Generator for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="fdc6c-104">本快速入门遵循 Microsoft OfficeDev Microsoft Teams存储库中的构建第一个 Microsoft Teams [App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki 中概述GitHub步骤。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-104">This quickstart follows the steps outlined in the [Build Your First Microsoft Teams App](https://github.com/OfficeDev/generator-teams/wiki/Build-Your-First-Microsoft-Teams-App) Wiki found in the Microsoft OfficeDev GitHub repository.</span></span>

<span data-ttu-id="fdc6c-105">在此快速入门中，我们将演练使用[Yeoman](https://github.com/OfficeDev/generator-teams/)生成器创建自定义频道Teams选项卡。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-105">In this quickstart we'll walk-through creating a custom channel and group tab using the [Teams Yeoman generator](https://github.com/OfficeDev/generator-teams/).</span></span>

[!INCLUDE [node-js-yeoman-prereq](~/includes/tabs/node-js-yeoman-prereq.md)]

<span data-ttu-id="fdc6c-106">**是否要创建可配置选项卡或静态选项卡？**</span><span class="sxs-lookup"><span data-stu-id="fdc6c-106">**Do you want to create a configurable or static tab?**</span></span>

<span data-ttu-id="fdc6c-107">使用箭头键选择可配置的选项卡。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-107">Use the arrow keys to select configurable tab.</span></span>

<span data-ttu-id="fdc6c-108">**您打算对 Tab 使用哪些范围？**</span><span class="sxs-lookup"><span data-stu-id="fdc6c-108">**What scopes do you intend to use for your Tab?**</span></span>

<span data-ttu-id="fdc6c-109">可以选择团队和/或群聊</span><span class="sxs-lookup"><span data-stu-id="fdc6c-109">You can select a Team and/or a group chat</span></span>

<span data-ttu-id="fdc6c-110">**是否希望此选项卡在 SharePoint Online 中可用？ (Y/n)**</span><span class="sxs-lookup"><span data-stu-id="fdc6c-110">**Do you want this tab to be available in SharePoint Online? (Y/n)**</span></span> 

<span data-ttu-id="fdc6c-111">选择 **n**。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-111">Select **n**.</span></span>

>[!IMPORTANT]
><span data-ttu-id="fdc6c-112">本快速入门中引用的路径组件 **yourDefaultTabNameTab** 是在生成器中为" **默认** 选项卡名称"加上单词 **"Tab"输入的值**。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-112">The path component **yourDefaultTabNameTab**, referenced in this quickstart, is the value that you entered in the generator for **Default Tab Name** plus the word **Tab**.</span></span>
>
><span data-ttu-id="fdc6c-113">例如：DefaultTabName：MyTab   =>  **/MyTabTab/**</span><span class="sxs-lookup"><span data-stu-id="fdc6c-113">For example: DefaultTabName: **MyTab** => **/MyTabTab/**</span></span>

<span data-ttu-id="fdc6c-114">在项目目录中，导航到以下内容：</span><span class="sxs-lookup"><span data-stu-id="fdc6c-114">In your project directory, navigate to the following:</span></span>

```bash
./src/app/scripts/<yourDefaultTabNameTab>/<yourDefaultTabNameTab>.tsx
```

<span data-ttu-id="fdc6c-115">你将在这里找到选项卡逻辑。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-115">That is where you'll find your tab logic.</span></span> <span data-ttu-id="fdc6c-116">找到 `render()` 方法，将以下 `<div>` 标记和内容添加到容器 `<PanelBody>` 代码的顶部：</span><span class="sxs-lookup"><span data-stu-id="fdc6c-116">Locate the `render()` method and add the following `<div>` tag and content to the top of the `<PanelBody>` container code:</span></span>

```html
    <PanelBody>
        <div style={styles.section}>
            Hello World! Yo Teams rocks!
        </div>
    </PanelBody>
```

<span data-ttu-id="fdc6c-117">确保保存更新后的文件。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-117">Make sure to save the updated file.</span></span>

## <a name="build-and-run-your-application"></a><span data-ttu-id="fdc6c-118">生成并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="fdc6c-118">Build and Run Your Application</span></span>

<span data-ttu-id="fdc6c-119">在项目目录中打开命令提示符以完成下一个任务。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-119">Open a command prompt in your project directory to complete the next tasks.</span></span>

[!INCLUDE [node-js-yeoman-gulp-tasks](~/includes/tabs/node-js-yeoman-gulp-tasks.md)]

<span data-ttu-id="fdc6c-120">若要查看选项卡配置页面，请转到 `https://localhost:3007/<yourDefaultAppNameTab>/config.html` 。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-120">To view your tab configuration page go to `https://localhost:3007/<yourDefaultAppNameTab>/config.html`.</span></span> <span data-ttu-id="fdc6c-121">应看到以下内容：</span><span class="sxs-lookup"><span data-stu-id="fdc6c-121">You should see the following:</span></span>

![配置页面屏幕截图](~/assets/images/tab-images/configurationPage.png)

## <a name="establish-a-secure-tunnel-to-your-tab"></a><span data-ttu-id="fdc6c-123">建立到选项卡的安全隧道</span><span class="sxs-lookup"><span data-stu-id="fdc6c-123">Establish a secure tunnel to your tab</span></span>

<span data-ttu-id="fdc6c-124">Microsoft Teams完全基于云的产品，并且要求使用 HTTPS 终结点从云中提供选项卡内容。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-124">Microsoft Teams is an entirely cloud-based product and requires that your tab content be available from the cloud using HTTPS endpoints.</span></span> <span data-ttu-id="fdc6c-125">Teams不允许本地托管，因此，你需要将选项卡发布到公用 URL 或使用将本地端口公开给面向 Internet 的 URL 的代理。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-125">Teams doesn't allow local hosting, therefore, you need to either publish your tab to a public URL or use a proxy that will expose your local port to an internet-facing URL.</span></span>

<span data-ttu-id="fdc6c-126">若要测试选项卡扩展，你将使用内置于此应用程序中的[ngrok。](https://ngrok.com/docs)</span><span class="sxs-lookup"><span data-stu-id="fdc6c-126">To test your tab extension, you'll use [ngrok](https://ngrok.com/docs), which is built into this application.</span></span> <span data-ttu-id="fdc6c-127">Ngrok 是反向代理软件工具，它将创建到本地运行的 Web 服务器公开可用的 HTTPS 终结点的隧道。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-127">Ngrok is a reverse proxy software tool that will create a tunnel to your locally running web server's publicly-available HTTPS endpoints.</span></span> <span data-ttu-id="fdc6c-128">你的服务器的 Web 终结点将在本地计算机上在当前会话期间可用。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-128">Your server's web endpoints will be available during the current session on your local machine.</span></span> <span data-ttu-id="fdc6c-129">当计算机关闭或进入睡眠状态时，服务将不再可用。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-129">When the machine is shut down or goes to sleep the service will no longer be available.</span></span>

<span data-ttu-id="fdc6c-130">在命令提示符中，退出 localhost 并输入以下内容：</span><span class="sxs-lookup"><span data-stu-id="fdc6c-130">In your command prompt, exit localhost and enter the following:</span></span>

```bash
gulp ngrok-serve
```

> [!IMPORTANT]
> <span data-ttu-id="fdc6c-131">将选项卡上传到 Microsoft 团队并成功保存后，可以在选项卡库中查看它，将其添加到选项卡栏，并与其交互，直到 ngrok 隧道会话结束。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-131">After your tab has been uploaded to Microsoft teams and successfully saved, you can view it in the tabs gallery, add it to the tabs bar, and interact with it until your ngrok tunnel session ends.</span></span> <span data-ttu-id="fdc6c-132">如果重新启动 ngrok 会话，将需要使用新的 URL 更新应用。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-132">If you restart your ngrok session, you'll need to update your app with the new URL.</span></span>

## <a name="upload-your-application-to-teams"></a><span data-ttu-id="fdc6c-133">Upload应用程序以Teams</span><span class="sxs-lookup"><span data-stu-id="fdc6c-133">Upload your application to Teams</span></span>

- <span data-ttu-id="fdc6c-134">打开 Microsoft Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-134">Open the Microsoft Teams client.</span></span> <span data-ttu-id="fdc6c-135">如果使用基于 [Web 的版本，](https://teams.microsoft.com) 可以使用浏览器的开发人员工具检查前端 [代码](~/tabs/how-to/developer-tools.md)。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-135">If you use the [web based version](https://teams.microsoft.com) you can inspect your front-end code using your browser's [developer tools](~/tabs/how-to/developer-tools.md).</span></span>
- <span data-ttu-id="fdc6c-136">在左侧 *的 YourTeams* 面板中，选择用于测试选项卡的团队旁边的菜单，然后选择 `...` "**管理团队"。**</span><span class="sxs-lookup"><span data-stu-id="fdc6c-136">In the *YourTeams* panel on the left, select the `...` menu next to the team that you're using to test your tab and choose **Manage team**.</span></span>
- <span data-ttu-id="fdc6c-137">在主面板中，从选项卡栏中选择"应用"，Upload位于页面右下角的自定义应用。 </span><span class="sxs-lookup"><span data-stu-id="fdc6c-137">In the main panel select **Apps** from the tab bar and choose **Upload a custom app** located in the lower right-hand corner of the page.</span></span>
- <span data-ttu-id="fdc6c-138">打开项目目录，浏览到 **./package** 文件夹，选择应用包 zip 文件夹并选择"打开 **"。**</span><span class="sxs-lookup"><span data-stu-id="fdc6c-138">Open your project directory, browse to the **./package** folder, select the app package zip folder and choose **Open**.</span></span> <span data-ttu-id="fdc6c-139">您的选项卡将上载到Teams。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-139">Your tab will upload into Teams.</span></span>
- <span data-ttu-id="fdc6c-140">返回到团队，选择要显示选项卡的频道，从选项卡➕选择选项卡，然后从库中选择您的选项卡。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-140">Return to your team, choose the channel where you would like to display the tab, select ➕ from the tab bar, and choose your tab from the gallery.</span></span>
- <span data-ttu-id="fdc6c-141">按照添加选项卡的说明操作。请注意，频道/组选项卡有一个自定义配置对话框。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-141">Follow the directions for adding a tab. Note that there's a custom configuration dialog for your channel/group tab.</span></span>
- <span data-ttu-id="fdc6c-142">选择 **"** 保存"，您的选项卡将添加到频道的选项卡栏中。</span><span class="sxs-lookup"><span data-stu-id="fdc6c-142">Select **Save** and your tab will be added to the channel's tab bar.</span></span>

## <a name="next-step"></a><span data-ttu-id="fdc6c-143">后续步骤</span><span class="sxs-lookup"><span data-stu-id="fdc6c-143">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="fdc6c-144">使用 ASP.NETCore 创建自定义频道和组选项卡</span><span class="sxs-lookup"><span data-stu-id="fdc6c-144">Create a Custom Channel and Group Tab with ASP.NETCore</span></span>](~/tabs/quickstarts/create-channel-group-tab-dotnet-core.md)
