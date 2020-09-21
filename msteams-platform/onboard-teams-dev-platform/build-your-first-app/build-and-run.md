---
title: 构建和运行第一个团队应用程序
author: heath-hamilton
ms.author: lajanuar
description: 运行你的首个 Microsoft 团队应用。
ms.date: 08/31/2020
ms.topic: quickstart
ms.openlocfilehash: 441b70480d9c177e9c6140342df8c9ea29494a29
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964654"
---
# <a name="build-and-run-your-first-microsoft-teams-app"></a><span data-ttu-id="783d4-103">生成并运行你的首个 Microsoft 团队应用</span><span class="sxs-lookup"><span data-stu-id="783d4-103">Build and run your first Microsoft Teams app</span></span>

<span data-ttu-id="783d4-104">您可以通过快速构建和运行基本的个人选项卡来直接在 Microsoft 团队平台上进行开发。</span><span class="sxs-lookup"><span data-stu-id="783d4-104">You can jump right into developing on the Microsoft Teams platform by quickly building and running a basic personal tab.</span></span>

## <a name="create-your-app-project"></a><span data-ttu-id="783d4-105">创建您的应用程序项目</span><span class="sxs-lookup"><span data-stu-id="783d4-105">Create your app project</span></span>

<span data-ttu-id="783d4-106">使用 Visual Studio Code 中的 Microsoft 团队工具包设置您的首个应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="783d4-106">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../doc-links/images/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用**"。
:::image type="content" source="../doc-links/images/create-teams-app.png" alt-text="创建团队应用程序图像":::
1. <span data-ttu-id="783d4-109">为你的团队应用输入名称。</span><span class="sxs-lookup"><span data-stu-id="783d4-109">Enter a name for your Teams app.</span></span> <span data-ttu-id="783d4-110"> (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) </span><span class="sxs-lookup"><span data-stu-id="783d4-110">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="783d4-111">在 " **添加功能** " 屏幕上，依次选择 **"** **下一步**"。</span><span class="sxs-lookup"><span data-stu-id="783d4-111">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../doc-links/images/choose-tab.png" alt-text="创建团队应用程序图像视图":::
1. <span data-ttu-id="783d4-113">检查 " **个人" 选项卡** 选项，然后选择屏幕底部的 " **完成** " 以配置项目。</span><span class="sxs-lookup"><span data-stu-id="783d4-113">Check the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="understand-important-app-project-components"></a><span data-ttu-id="783d4-114">了解重要的应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="783d4-114">Understand important app project components</span></span>

<span data-ttu-id="783d4-115">工具包配置项目后，您就可以使用组件为团队构建基本的个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="783d4-115">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="783d4-116">项目目录和文件显示在 Visual Studio Code 的 "资源管理器" 区域中。</span><span class="sxs-lookup"><span data-stu-id="783d4-116">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../doc-links/images/app-project-files.png" alt-text="Visual Studio Code 中的应用程序项目文件。":::

<span data-ttu-id="783d4-118">让我们花些时间了解一些主要文件团队应用程序开发人员使用的关键文件。</span><span class="sxs-lookup"><span data-stu-id="783d4-118">Let's take time to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="783d4-119">应用程序清单 (`manifest.json`) </span><span class="sxs-lookup"><span data-stu-id="783d4-119">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="783d4-120">在目录中 `.publish` ，应用程序清单是任何应用程序项目的起始点。</span><span class="sxs-lookup"><span data-stu-id="783d4-120">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="783d4-121">清单定义您的应用程序的基本属性并指向所需的资源。</span><span class="sxs-lookup"><span data-stu-id="783d4-121">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="783d4-122">在安装应用程序时，团队会对清单进行分析，以了解如何在客户端中呈现您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="783d4-122">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="783d4-123">应用程序基架</span><span class="sxs-lookup"><span data-stu-id="783d4-123">App scaffolding</span></span>

<span data-ttu-id="783d4-124">该工具包将根据您在安装过程中添加的功能，在目录中自动为您创建基架 `src` 。</span><span class="sxs-lookup"><span data-stu-id="783d4-124">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="783d4-125">例如，如果在安装过程中创建选项卡，则该 `App.js` 目录中的文件 `src/components` 很重要，因为它会处理您的应用程序的初始化和路由。</span><span class="sxs-lookup"><span data-stu-id="783d4-125">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="783d4-126">它调用 [Microsoft 团队 SDK](../../tabs/how-to/using-teams-client-sdk.md) 以在您的应用程序和团队之间建立通信。</span><span class="sxs-lookup"><span data-stu-id="783d4-126">It calls the [Microsoft Teams SDK](../../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-package-developmentzip"></a><span data-ttu-id="783d4-127">应用程序包 (`Development.zip`) </span><span class="sxs-lookup"><span data-stu-id="783d4-127">App package (`Development.zip`)</span></span>

<span data-ttu-id="783d4-128">位于目录中 `.publish` ，您需要应用程序包以在团队中 [旁加载您的应用程序](../../concepts/deploy-and-publish/overview.md#upload-your-app-directly) 。</span><span class="sxs-lookup"><span data-stu-id="783d4-128">Located in the `.publish` directory, you need the app package to [sideload your app](../../concepts/deploy-and-publish/overview.md#upload-your-app-directly) in Teams.</span></span> <span data-ttu-id="783d4-129">[发布到组织的应用程序目录](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)或[AppSource](../../concepts/deploy-and-publish/appsource/publish.md)时，也可以使用包。</span><span class="sxs-lookup"><span data-stu-id="783d4-129">The package is also used when [publishing to your organization's app catalog](../../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [AppSource](../../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="783d4-130">以下是有关应用程序包文件的一些详细信息：</span><span class="sxs-lookup"><span data-stu-id="783d4-130">Here are some details about the app package files:</span></span>

|<span data-ttu-id="783d4-131">名称</span><span class="sxs-lookup"><span data-stu-id="783d4-131">Name</span></span>|<span data-ttu-id="783d4-132">类型</span><span class="sxs-lookup"><span data-stu-id="783d4-132">Type</span></span>|<span data-ttu-id="783d4-133">Size</span><span class="sxs-lookup"><span data-stu-id="783d4-133">Size</span></span>|<span data-ttu-id="783d4-134">清单位置</span><span class="sxs-lookup"><span data-stu-id="783d4-134">Manifest location</span></span>|<span data-ttu-id="783d4-135">工具包文件名</span><span class="sxs-lookup"><span data-stu-id="783d4-135">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="783d4-136">**应用程序清单**</span><span class="sxs-lookup"><span data-stu-id="783d4-136">**App manifest**</span></span>|`.json`| <span data-ttu-id="783d4-137">—</span><span class="sxs-lookup"><span data-stu-id="783d4-137">—</span></span> | <span data-ttu-id="783d4-138">—</span><span class="sxs-lookup"><span data-stu-id="783d4-138">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="783d4-139">**颜色徽标**</span><span class="sxs-lookup"><span data-stu-id="783d4-139">**Color logo**</span></span>|`.png`|<span data-ttu-id="783d4-140">192 &times; 192 像素</span><span class="sxs-lookup"><span data-stu-id="783d4-140">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="783d4-141">**大纲徽标**</span><span class="sxs-lookup"><span data-stu-id="783d4-141">**Outline logo**</span></span>|`.png`|<span data-ttu-id="783d4-142">32 &times; 32 像素</span><span class="sxs-lookup"><span data-stu-id="783d4-142">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

## <a name="run-your-app"></a><span data-ttu-id="783d4-143">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="783d4-143">Run your app</span></span>

<span data-ttu-id="783d4-144">在时间方面，你将在本地构建和运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="783d4-144">In the interest of time, you'll build and run your app locally.</span></span> <span data-ttu-id="783d4-145">生产级团队应用程序托管在云中。</span><span class="sxs-lookup"><span data-stu-id="783d4-145">Production-level Teams apps are hosted in the cloud.</span></span>

<span data-ttu-id="783d4-146"> (工具包中也提供了此信息 `README` 。 ) </span><span class="sxs-lookup"><span data-stu-id="783d4-146">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="783d4-147">在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="783d4-147">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="783d4-148">运行 `npm start` 。</span><span class="sxs-lookup"><span data-stu-id="783d4-148">Run `npm start`.</span></span> <span data-ttu-id="783d4-149">完成后，已 **成功编译了！**</span><span class="sxs-lookup"><span data-stu-id="783d4-149">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="783d4-150">终端中的邮件。</span><span class="sxs-lookup"><span data-stu-id="783d4-150">message in the terminal.</span></span>
1. <span data-ttu-id="783d4-151">打开浏览器并转到 `https://localhost:3000` 以查看名为 **Microsoft 团队选项卡**的空白网页。 (不会担心您无法看到页面上的任何内容。 ) </span><span class="sxs-lookup"><span data-stu-id="783d4-151">Open a browser and go to `https://localhost:3000` to view a blank webpage called **Microsoft Teams Tab**. (Don't worry that you can't see any content on the page.)</span></span><br/>
   :::image type="content" source="../doc-links/images/local-host-tab.png" alt-text="在浏览器中查看应用程序。":::

## <a name="set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="783d4-153">设置到您的应用程序的安全隧道</span><span class="sxs-lookup"><span data-stu-id="783d4-153">Set up a secure tunnel to your app</span></span>

<span data-ttu-id="783d4-154">您的应用程序已启动并在本地 web 服务器上运行。</span><span class="sxs-lookup"><span data-stu-id="783d4-154">Your app is up and running on your local web server.</span></span> <span data-ttu-id="783d4-155">若要在团队中运行您的应用程序，您必须 `localhost` 通过 HTTPS 进行访问。</span><span class="sxs-lookup"><span data-stu-id="783d4-155">To run your app in Teams, you must make your `localhost` accessible through HTTPS.</span></span>

<span data-ttu-id="783d4-156">如果还未安装 [ngrok](https://ngrok.com/download) ，请安装。</span><span class="sxs-lookup"><span data-stu-id="783d4-156">Install [ngrok](https://ngrok.com/download) if you haven't already.</span></span> <span data-ttu-id="783d4-157">运行此工具时，将创建两个全局可用的 Url，它们指向您的本地 web 服务器 (`http://localhost:3000`) 。</span><span class="sxs-lookup"><span data-stu-id="783d4-157">When you run this tool, you create two globally available URLs that point to your local web server (`http://localhost:3000`).</span></span> <span data-ttu-id="783d4-158">您需要以的开头的转发 URL `HTTPS` 。</span><span class="sxs-lookup"><span data-stu-id="783d4-158">You need the forwarding URL that begins with `HTTPS`.</span></span>

1. <span data-ttu-id="783d4-159">打开一个新的终端并运行 `ngrok http 3000` 。</span><span class="sxs-lookup"><span data-stu-id="783d4-159">Open a new terminal and run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="783d4-160">复制你提供的 HTTPS URL (请参阅以下示例) 。</span><span class="sxs-lookup"><span data-stu-id="783d4-160">Copy the HTTPS URL you're provided (see the following example).</span></span>
:::image type="content" source="../doc-links/images/ngrok-running.png" alt-text="ngrok 正在运行的图像":::
1. <span data-ttu-id="783d4-162">在 `.publish` 目录中，打开 `Development.env` 。</span><span class="sxs-lookup"><span data-stu-id="783d4-162">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="783d4-163">将 `baseUrl0` 值替换为复制的 URL。</span><span class="sxs-lookup"><span data-stu-id="783d4-163">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="783d4-164"> (例如，改 `baseUrl0=http://localhost:3000` 为 `baseUrl0=https://85528b2b3ba5.ngrok.io` 。 ) </span><span class="sxs-lookup"><span data-stu-id="783d4-164">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ba5.ngrok.io`.)</span></span>

<span data-ttu-id="783d4-165">您的应用程序清单现在指向您在其中承载应用程序的位置。</span><span class="sxs-lookup"><span data-stu-id="783d4-165">Your app manifest now points to where you're hosting the app.</span></span>

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="783d4-166">在团队中旁加载您的应用程序</span><span class="sxs-lookup"><span data-stu-id="783d4-166">Sideload your app in Teams</span></span>

<span data-ttu-id="783d4-167">通过 HTTPS 运行并可访问应用程序后，即可将其上载到团队。</span><span class="sxs-lookup"><span data-stu-id="783d4-167">With your app running and accessible via HTTPS, you're ready to upload it to Teams.</span></span>

> [!TIP]
> <span data-ttu-id="783d4-168">在向您的应用程序进行旁加载之前，请使用 [工具包的验证功能](../../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)检查是否存在问题。</span><span class="sxs-lookup"><span data-stu-id="783d4-168">Before sideloading your app, check for issues using the [toolkit's validation feature](../../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span></span> <span data-ttu-id="783d4-169">必须修复错误才能成功旁加载应用。</span><span class="sxs-lookup"><span data-stu-id="783d4-169">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="783d4-170">使用允许应用旁加载的帐户登录到团队客户端。</span><span class="sxs-lookup"><span data-stu-id="783d4-170">Log in to the Teams client with your account that allows app sideloading.</span></span> <span data-ttu-id="783d4-171"> (如果您不能确定，请了解如何获取 [团队开发帐户](../build-your-first-app/building-real-world-app.md#set-up-your-development-account)。 ) </span><span class="sxs-lookup"><span data-stu-id="783d4-171">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/building-real-world-app.md#set-up-your-development-account).)</span></span>
1. <span data-ttu-id="783d4-172">选择 " **应用**"，然后选择 " **上载自定义应用**"。</span><span class="sxs-lookup"><span data-stu-id="783d4-172">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="783d4-173">转到您的应用程序项目 `.publish` 文件夹，然后选择 `Development.zip` 。</span><span class="sxs-lookup"><span data-stu-id="783d4-173">Go to your app project `.publish` folder and select `Development.zip`.</span></span> <span data-ttu-id="783d4-174">将显示安装模式。</span><span class="sxs-lookup"><span data-stu-id="783d4-174">An install modal displays.</span></span>
:::image type="content" source="../doc-links/images/add-teams-app.png" alt-text="添加团队应用":::
1. <span data-ttu-id="783d4-176">选择 " **添加** " 以安装您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="783d4-176">Select **Add** to install your app.</span></span>
:::image type="content" source="../doc-links/images/tab-running.png" alt-text="屏幕截图显示了一个示例 Hello，World！团队中的应用程序。":::

<span data-ttu-id="783d4-178">🎉祝贺！</span><span class="sxs-lookup"><span data-stu-id="783d4-178">🎉 Congratulations!</span></span> <span data-ttu-id="783d4-179">你的应用程序正在团队中运行。</span><span class="sxs-lookup"><span data-stu-id="783d4-179">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="783d4-180">后续步骤</span><span class="sxs-lookup"><span data-stu-id="783d4-180">Next step</span></span>

<span data-ttu-id="783d4-181">展开刚创建的 "个人" 选项卡或生成另一种类型的 "团队" 应用。</span><span class="sxs-lookup"><span data-stu-id="783d4-181">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="783d4-182">添加到你的个人选项卡</span><span class="sxs-lookup"><span data-stu-id="783d4-182">Add to your personal tab</span></span>](../build-your-first-app/add-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="783d4-183">生成通道选项卡</span><span class="sxs-lookup"><span data-stu-id="783d4-183">Build a channel tab</span></span>](../build-your-first-app/add-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="783d4-184">构建 bot</span><span class="sxs-lookup"><span data-stu-id="783d4-184">Build a bot</span></span>](../build-your-first-app/add-bot.md)
