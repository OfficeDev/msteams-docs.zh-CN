---
title: 构建并运行 "Hello，World！" Teams 应用
author: heath-hamilton
description: 生成并运行您的首个 Microsoft 团队应用程序（一个显示 "Hello，World！" 的个人选项卡）
ms.author: lajanuar
ms.date: 09/22/2020
ms.topic: quickstart
ms.openlocfilehash: 5be2e8f2932a91ed11137f3a7be544e12bd65559
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210149"
---
# <a name="build-a-hello-world-teams-app"></a><span data-ttu-id="1e1d2-104">构建 "Hello，World！"</span><span class="sxs-lookup"><span data-stu-id="1e1d2-104">Build a "Hello, World!"</span></span> <span data-ttu-id="1e1d2-105">Teams 应用</span><span class="sxs-lookup"><span data-stu-id="1e1d2-105">Teams app</span></span>

<span data-ttu-id="1e1d2-106">您可以通过构建显示为 "Hello，World！" 的个人选项卡，直接跳转到 Microsoft 团队平台开发。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-106">You can jump right into Microsoft Teams platform development by building a personal tab that displays "Hello, World!"</span></span>

## <a name="create-your-app-project"></a><span data-ttu-id="1e1d2-107">创建您的应用程序项目</span><span class="sxs-lookup"><span data-stu-id="1e1d2-107">Create your app project</span></span>

<span data-ttu-id="1e1d2-108">使用 Visual Studio Code 中的 Microsoft 团队工具包设置您的首个应用程序项目。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-108">Use the Microsoft Teams Toolkit in Visual Studio Code to set up your first app project.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队**"， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用**"。
:::image type="content" source="../assets/images/build-your-first-app/create-teams-app.png" alt-text="显示如何使用 Visual Studio Code 团队工具包创建新应用程序的屏幕截图。":::
1. <span data-ttu-id="1e1d2-111">为你的团队应用输入名称。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-111">Enter a name for your Teams app.</span></span> <span data-ttu-id="1e1d2-112"> (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) </span><span class="sxs-lookup"><span data-stu-id="1e1d2-112">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="1e1d2-113">在 " **添加功能** " 屏幕上，依次选择 **"** **下一步**"。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-113">On the **Add capabilities** screen, select **Tab** then **Next**.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/choose-tab.png" alt-text="显示如何使用 Visual Studio Code 团队工具包配置应用程序项目的屏幕截图。":::
1. <span data-ttu-id="1e1d2-115">检查 " **个人" 选项卡** 选项，然后选择屏幕底部的 " **完成** " 以配置项目。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-115">Check the **Personal tab** option and select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="understand-important-app-project-components"></a><span data-ttu-id="1e1d2-116">了解重要的应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="1e1d2-116">Understand important app project components</span></span>

<span data-ttu-id="1e1d2-117">工具包配置项目后，您就可以使用组件为团队构建基本的个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-117">Once the toolkit configures your project, you have the components to build a basic personal tab for Teams.</span></span> <span data-ttu-id="1e1d2-118">项目目录和文件显示在 Visual Studio Code 的 "资源管理器" 区域中。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-118">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/app-project-files.png" alt-text="显示 Visual Studio Code 中的 "个人" 选项卡的应用程序项目文件的屏幕截图。":::

<span data-ttu-id="1e1d2-120">让我们花点时间了解一些主要文件团队应用程序开发人员使用的。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-120">Let's take a moment to understand some of the key files Teams app developers work with.</span></span>

### <a name="app-manifest-manifestjson"></a><span data-ttu-id="1e1d2-121">应用程序清单 (`manifest.json`) </span><span class="sxs-lookup"><span data-stu-id="1e1d2-121">App manifest (`manifest.json`)</span></span>

<span data-ttu-id="1e1d2-122">在目录中 `.publish` ，应用程序清单是任何应用程序项目的起始点。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-122">Located in the `.publish` directory, the app manifest is the starting point for any app project.</span></span> <span data-ttu-id="1e1d2-123">清单定义您的应用程序的基本属性并指向所需的资源。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-123">The manifest defines your app's fundamental attributes and points to required resources.</span></span> <span data-ttu-id="1e1d2-124">在安装应用程序时，团队会对清单进行分析，以了解如何在客户端中呈现您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-124">When you install an app, Teams parses the manifest to understand how to render your app in the client.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="1e1d2-125">应用程序基架</span><span class="sxs-lookup"><span data-stu-id="1e1d2-125">App scaffolding</span></span>

<span data-ttu-id="1e1d2-126">该工具包将根据您在安装过程中添加的功能，在目录中自动为您创建基架 `src` 。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-126">The toolkit automatically creates scaffolding for you in the `src` directory based on the capabilities you added during setup.</span></span>

<span data-ttu-id="1e1d2-127">例如，如果在安装过程中创建选项卡，则该 `App.js` 目录中的文件 `src/components` 很重要，因为它会处理您的应用程序的初始化和路由。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-127">If you create a tab during setup, for example, the `App.js` file in the `src/components` directory is important because it handles the initialization and routing of your app.</span></span> <span data-ttu-id="1e1d2-128">它调用 [Microsoft 团队 SDK](../tabs/how-to/using-teams-client-sdk.md) 以在您的应用程序和团队之间建立通信。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-128">It calls the [Microsoft Teams SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>

### <a name="app-package-developmentzip"></a><span data-ttu-id="1e1d2-129">应用程序包 (`Development.zip`) </span><span class="sxs-lookup"><span data-stu-id="1e1d2-129">App package (`Development.zip`)</span></span>

<span data-ttu-id="1e1d2-130">位于目录中 `.publish` ，您需要应用程序包以在团队中 [旁加载您的应用程序](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) 。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-130">Located in the `.publish` directory, you need the app package to [sideload your app](../concepts/deploy-and-publish/overview.md#upload-your-app-directly) in Teams.</span></span> <span data-ttu-id="1e1d2-131">[发布到组织的应用程序目录](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog)或[AppSource](../concepts/deploy-and-publish/appsource/publish.md)时，也可以使用包。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-131">The package is also used when [publishing to your organization's app catalog](../concepts/deploy-and-publish/overview.md#publish-to-your-organizations-app-catalog) or [AppSource](../concepts/deploy-and-publish/appsource/publish.md).</span></span>

<span data-ttu-id="1e1d2-132">以下是有关应用程序包文件的一些详细信息：</span><span class="sxs-lookup"><span data-stu-id="1e1d2-132">Here are some details about the app package files:</span></span>

|<span data-ttu-id="1e1d2-133">名称</span><span class="sxs-lookup"><span data-stu-id="1e1d2-133">Name</span></span>|<span data-ttu-id="1e1d2-134">类型</span><span class="sxs-lookup"><span data-stu-id="1e1d2-134">Type</span></span>|<span data-ttu-id="1e1d2-135">Size</span><span class="sxs-lookup"><span data-stu-id="1e1d2-135">Size</span></span>|<span data-ttu-id="1e1d2-136">清单位置</span><span class="sxs-lookup"><span data-stu-id="1e1d2-136">Manifest location</span></span>|<span data-ttu-id="1e1d2-137">工具包文件名</span><span class="sxs-lookup"><span data-stu-id="1e1d2-137">Toolkit filename</span></span>|
|---|---|:---:|:---:|-----|
|<span data-ttu-id="1e1d2-138">**应用程序清单**</span><span class="sxs-lookup"><span data-stu-id="1e1d2-138">**App manifest**</span></span>|`.json`| <span data-ttu-id="1e1d2-139">—</span><span class="sxs-lookup"><span data-stu-id="1e1d2-139">—</span></span> | <span data-ttu-id="1e1d2-140">—</span><span class="sxs-lookup"><span data-stu-id="1e1d2-140">—</span></span> |`.publish/manifest.json`|
|<span data-ttu-id="1e1d2-141">**颜色徽标**</span><span class="sxs-lookup"><span data-stu-id="1e1d2-141">**Color logo**</span></span>|`.png`|<span data-ttu-id="1e1d2-142">192 &times; 192 像素</span><span class="sxs-lookup"><span data-stu-id="1e1d2-142">192&times;192 pixels</span></span>|`icon.color`|`.publish/color.png`|
|<span data-ttu-id="1e1d2-143">**大纲徽标**</span><span class="sxs-lookup"><span data-stu-id="1e1d2-143">**Outline logo**</span></span>|`.png`|<span data-ttu-id="1e1d2-144">32 &times; 32 像素</span><span class="sxs-lookup"><span data-stu-id="1e1d2-144">32&times;32 pixels</span></span>|`icon.outline`|`.publish/outline.png`|

## <a name="run-your-app"></a><span data-ttu-id="1e1d2-145">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="1e1d2-145">Run your app</span></span>

<span data-ttu-id="1e1d2-146">在时间方面，你将在本地构建和运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-146">In the interest of time, you'll build and run your app locally.</span></span>

<span data-ttu-id="1e1d2-147"> (工具包中也提供了此信息 `README` 。 ) </span><span class="sxs-lookup"><span data-stu-id="1e1d2-147">(This information is also available in the toolkit `README`.)</span></span>

1. <span data-ttu-id="1e1d2-148">在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-148">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="1e1d2-149">运行 `npm start` 。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-149">Run `npm start`.</span></span> <span data-ttu-id="1e1d2-150">完成后，已 **成功编译了！**</span><span class="sxs-lookup"><span data-stu-id="1e1d2-150">Once complete, there's a **Compiled successfully!**</span></span> <span data-ttu-id="1e1d2-151">终端中的邮件。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-151">message in the terminal.</span></span>
1. <span data-ttu-id="1e1d2-152">打开浏览器并转到 `https://localhost:3000` 以查看名为 **Microsoft 团队选项卡**的空白网页。 (不会担心您无法看到页面上的任何内容。 ) </span><span class="sxs-lookup"><span data-stu-id="1e1d2-152">Open a browser and go to `https://localhost:3000` to view a blank webpage called **Microsoft Teams Tab**. (Don't worry that you can't see any content on the page.)</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/local-host-tab.png" alt-text="显示要在浏览器中查看正在运行的应用程序的外观的屏幕截图。":::

## <a name="set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="1e1d2-154">设置到您的应用程序的安全隧道</span><span class="sxs-lookup"><span data-stu-id="1e1d2-154">Set up a secure tunnel to your app</span></span>

<span data-ttu-id="1e1d2-155">您的应用程序已启动并在本地 web 服务器上运行。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-155">Your app is up and running on your local web server.</span></span> <span data-ttu-id="1e1d2-156">若要在团队中运行您的应用程序，您必须 `localhost` 通过 HTTPS 进行访问。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-156">To run your app in Teams, you must make your `localhost` accessible through HTTPS.</span></span>

<span data-ttu-id="1e1d2-157">如果还未安装 [ngrok](https://ngrok.com/download) ，请安装。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-157">Install [ngrok](https://ngrok.com/download) if you haven't already.</span></span> <span data-ttu-id="1e1d2-158">运行此工具时，将创建两个全局可用的 Url，它们指向您的本地 web 服务器 (`http://localhost:3000`) 。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-158">When you run this tool, you create two globally available URLs that point to your local web server (`http://localhost:3000`).</span></span> <span data-ttu-id="1e1d2-159">您需要以的开头的转发 URL `HTTPS` 。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-159">You need the forwarding URL that begins with `HTTPS`.</span></span>

1. <span data-ttu-id="1e1d2-160">打开一个新的终端并运行 `ngrok http 3000` 。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-160">Open a new terminal and run `ngrok http 3000`.</span></span>
1. <span data-ttu-id="1e1d2-161">复制你提供的 HTTPS URL (请参阅以下示例) 。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-161">Copy the HTTPS URL you're provided (see the following example).</span></span>
:::image type="content" source="../assets/images/build-your-first-app/ngrok-running.png" alt-text="显示 ngrok 正在运行的终端的屏幕截图。":::
1. <span data-ttu-id="1e1d2-163">在 `.publish` 目录中，打开 `Development.env` 。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-163">In your `.publish` directory, open `Development.env`.</span></span>
1. <span data-ttu-id="1e1d2-164">将 `baseUrl0` 值替换为复制的 URL。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-164">Replace the `baseUrl0` value with the copied URL.</span></span> <span data-ttu-id="1e1d2-165"> (例如，改 `baseUrl0=http://localhost:3000` 为 `baseUrl0=https://85528b2b3ba5.ngrok.io` 。 ) </span><span class="sxs-lookup"><span data-stu-id="1e1d2-165">(For example, change `baseUrl0=http://localhost:3000` to `baseUrl0=https://85528b2b3ba5.ngrok.io`.)</span></span>

<span data-ttu-id="1e1d2-166">您的应用程序清单现在指向您在其中承载应用程序的位置。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-166">Your app manifest now points to where you're hosting the app.</span></span>

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="1e1d2-167">在团队中旁加载您的应用程序</span><span class="sxs-lookup"><span data-stu-id="1e1d2-167">Sideload your app in Teams</span></span>

<span data-ttu-id="1e1d2-168">通过 HTTPS 运行并可访问应用程序后，即可将其上载到团队。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-168">With your app running and accessible via HTTPS, you're ready to upload it to Teams.</span></span>

> [!TIP]
> <span data-ttu-id="1e1d2-169">在向您的应用程序进行旁加载之前，请使用 [工具包的验证功能](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool)检查是否存在问题。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-169">Before sideloading your app, check for issues using the [toolkit's validation feature](../concepts/deploy-and-publish/appsource/prepare/submission-checklist.md#teams-app-validation-tool).</span></span> <span data-ttu-id="1e1d2-170">必须修复错误才能成功旁加载应用。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-170">Errors must be fixed to successfully sideload the app.</span></span>

1. <span data-ttu-id="1e1d2-171">使用允许应用旁加载的帐户登录到团队客户端。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-171">Log in to the Teams client with your account that allows app sideloading.</span></span> <span data-ttu-id="1e1d2-172"> (如果您不能确定，请了解如何获取 [团队开发帐户](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account)。 ) </span><span class="sxs-lookup"><span data-stu-id="1e1d2-172">(If you aren't sure you have that, learn about getting a [Teams development account](../build-your-first-app/build-first-app-overview.md#set-up-your-development-account).)</span></span>
1. <span data-ttu-id="1e1d2-173">选择 " **应用**"，然后选择 " **上载自定义应用**"。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-173">Select **Apps**, then choose **Upload a custom app**.</span></span>
1. <span data-ttu-id="1e1d2-174">转到您的应用程序项目 `.publish` 文件夹，然后选择 `Development.zip` 。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-174">Go to your app project `.publish` folder and select `Development.zip`.</span></span> <span data-ttu-id="1e1d2-175">将显示安装模式。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-175">An installation modal displays.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/add-teams-app.png" alt-text="显示团队应用安装模式示例的屏幕截图。":::
1. <span data-ttu-id="1e1d2-177">选择 " **添加** " 以安装您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-177">Select **Add** to install your app.</span></span>
:::image type="content" source="../assets/images/build-your-first-app/tab-running.png" alt-text="显示在团队中运行的示例 "Hello，World！" 个人选项卡应用程序的屏幕截图。":::

<span data-ttu-id="1e1d2-179">🎉祝贺！</span><span class="sxs-lookup"><span data-stu-id="1e1d2-179">🎉 Congratulations!</span></span> <span data-ttu-id="1e1d2-180">你的应用程序正在团队中运行。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-180">Your app is running in Teams.</span></span>

## <a name="next-step"></a><span data-ttu-id="1e1d2-181">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1e1d2-181">Next step</span></span>

<span data-ttu-id="1e1d2-182">展开刚创建的 "个人" 选项卡或生成另一种类型的 "团队" 应用。</span><span class="sxs-lookup"><span data-stu-id="1e1d2-182">Expand on the personal tab you just created or build another type of Teams app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1e1d2-183">添加到你的个人选项卡</span><span class="sxs-lookup"><span data-stu-id="1e1d2-183">Add to your personal tab</span></span>](../build-your-first-app/build-personal-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="1e1d2-184">生成通道选项卡</span><span class="sxs-lookup"><span data-stu-id="1e1d2-184">Build a channel tab</span></span>](../build-your-first-app/build-channel-tab.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="1e1d2-185">构建 bot</span><span class="sxs-lookup"><span data-stu-id="1e1d2-185">Build a bot</span></span>](../build-your-first-app/build-bot.md)
