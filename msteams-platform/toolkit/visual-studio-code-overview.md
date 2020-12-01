---
title: 使用 Microsoft 团队工具包和 Visual Studio Code 生成应用程序
description: 开始在 Visual Studio Code 中使用 Microsoft 团队工具包直接构建强大的自定义应用程序
keywords: 团队 visual studio code 工具包
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 41b0eeaeef1c7094fc9c8cbdc05c2db899245fc6
ms.sourcegitcommit: 7e47bf158249050c36d97509eea00e77089a54e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2020
ms.locfileid: "49476928"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="181cb-104">使用团队工具包和 Visual Studio Code 生成应用程序</span><span class="sxs-lookup"><span data-stu-id="181cb-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="181cb-105">Microsoft 团队工具包使你能够在 Visual Studio Code 环境中直接创建自定义团队应用。</span><span class="sxs-lookup"><span data-stu-id="181cb-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="181cb-106">该工具包将引导您完成整个过程，并提供生成、调试和启动团队应用程序所需的所有内容。</span><span class="sxs-lookup"><span data-stu-id="181cb-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="181cb-107">安装团队工具包</span><span class="sxs-lookup"><span data-stu-id="181cb-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="181cb-108">Visual studio Code 的 Microsoft 团队工具包可从 [Visual Studio Marketplace](https://aka.ms/teams-toolkit) 下载，也可直接作为 Visual studio code 中的扩展。</span><span class="sxs-lookup"><span data-stu-id="181cb-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="181cb-109">安装完成后，应在 Visual Studio Code 活动栏中看到 "团队" 工具包。</span><span class="sxs-lookup"><span data-stu-id="181cb-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="181cb-110">如果不是，请在活动栏中右键单击，然后选择 " **Microsoft 团队** " 以固定该工具包以方便访问。</span><span class="sxs-lookup"><span data-stu-id="181cb-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="181cb-111">使用工具包</span><span class="sxs-lookup"><span data-stu-id="181cb-111">Using the toolkit</span></span>

- [<span data-ttu-id="181cb-112">设置新项目</span><span class="sxs-lookup"><span data-stu-id="181cb-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="181cb-113">导入现有项目</span><span class="sxs-lookup"><span data-stu-id="181cb-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="181cb-114">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="181cb-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="181cb-115">打包应用程序</span><span class="sxs-lookup"><span data-stu-id="181cb-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="181cb-116">在本地或在团队中运行应用程序</span><span class="sxs-lookup"><span data-stu-id="181cb-116">Run your app locally or in Teams</span></span>](#run-your-app)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="181cb-117">设置新的团队项目</span><span class="sxs-lookup"><span data-stu-id="181cb-117">Set up a new Teams project</span></span>

1. <span data-ttu-id="181cb-118">在本地环境中为项目创建一个工作区/文件夹。</span><span class="sxs-lookup"><span data-stu-id="181cb-118">Create a workspace/folder for your project in your local environment.</span></span>
1. <span data-ttu-id="181cb-119">在 Visual Studio Code 中，选择 "团队" 图标</span><span class="sxs-lookup"><span data-stu-id="181cb-119">In Visual Studio Code, select the Teams icon</span></span> ![Teams 图标](../assets/icons/favicon-16x16.png) <span data-ttu-id="181cb-121">从窗口左侧的活动栏中进行。</span><span class="sxs-lookup"><span data-stu-id="181cb-121">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="181cb-122">从 "命令" 菜单中选择 **"打开 Microsoft 团队工具包"** 。</span><span class="sxs-lookup"><span data-stu-id="181cb-122">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="181cb-123">从 "命令" 菜单中选择 " **创建新的团队应用** "。</span><span class="sxs-lookup"><span data-stu-id="181cb-123">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="181cb-124">出现提示时，输入工作区的名称。</span><span class="sxs-lookup"><span data-stu-id="181cb-124">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="181cb-125">这将用作项目将驻留的文件夹的名称和应用程序的默认名称。</span><span class="sxs-lookup"><span data-stu-id="181cb-125">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="181cb-126">按 **enter** ，你将进入 " **添加功能** " 屏幕，为新应用配置属性。</span><span class="sxs-lookup"><span data-stu-id="181cb-126">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="181cb-127">选择 " **完成** " 按钮完成配置过程。</span><span class="sxs-lookup"><span data-stu-id="181cb-127">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="181cb-128">导入现有团队应用程序项目</span><span class="sxs-lookup"><span data-stu-id="181cb-128">Import an existing Teams app project</span></span>

1. <span data-ttu-id="181cb-129">在 Visual Studio Code 中，选择 "团队" 图标</span><span class="sxs-lookup"><span data-stu-id="181cb-129">In Visual Studio Code, select the Teams icon</span></span> ![Teams 图标](../assets/icons/favicon-16x16.png) <span data-ttu-id="181cb-131">从窗口左侧的活动栏中进行。</span><span class="sxs-lookup"><span data-stu-id="181cb-131">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="181cb-132">从 "命令" 菜单中选择 " **导入应用程序包** "。</span><span class="sxs-lookup"><span data-stu-id="181cb-132">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="181cb-133">选择现有 [团队应用程序包](../concepts/build-and-test/apps-package.md) zip 文件。</span><span class="sxs-lookup"><span data-stu-id="181cb-133">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="181cb-134">选择 " **选择发布包** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="181cb-134">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="181cb-135">此时，工具包的 "配置" 选项卡应包含您的应用程序的详细信息。</span><span class="sxs-lookup"><span data-stu-id="181cb-135">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="181cb-136">在 visual studio code 中，选择 "**文件**" "  ->  **将文件夹添加到工作区**"，将源代码目录添加到 Visual studio code Workspace。</span><span class="sxs-lookup"><span data-stu-id="181cb-136">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="181cb-137">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="181cb-137">Configure your app</span></span>

<span data-ttu-id="181cb-138">在其核心中，团队应用程序包含三个组件：</span><span class="sxs-lookup"><span data-stu-id="181cb-138">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="181cb-139">Microsoft 团队客户端 (web、桌面或移动) ，用户与您的应用程序进行交互。</span><span class="sxs-lookup"><span data-stu-id="181cb-139">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="181cb-140">对将在团队中显示的内容请求做出响应的服务器，例如，HTML 选项卡内容或 bot 自适应卡。</span><span class="sxs-lookup"><span data-stu-id="181cb-140">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="181cb-141">由三个文件组成的团队 [应用程序包](/concepts/build-and-test/apps-package.md) ：</span><span class="sxs-lookup"><span data-stu-id="181cb-141">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="181cb-142">上的 manifest.js</span><span class="sxs-lookup"><span data-stu-id="181cb-142">The manifest.json</span></span> 
  > - <span data-ttu-id="181cb-143">显示在公用或组织应用程序目录中的应用程序的[彩色图标](../resources/schema/manifest-schema.md#icons)</span><span class="sxs-lookup"><span data-stu-id="181cb-143">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="181cb-144">"团队" 活动栏中显示的 [大纲图标](../resources/schema/manifest-schema.md#icons) 。</span><span class="sxs-lookup"><span data-stu-id="181cb-144">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="181cb-145">在安装应用程序时，团队客户端会分析清单文件以确定所需的信息，如应用程序的名称和服务所在的 URL。</span><span class="sxs-lookup"><span data-stu-id="181cb-145">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="181cb-146">若要配置您的应用程序，请导航到 Visual Studio Code 中的 " **Microsoft 团队工具包** " 选项卡。</span><span class="sxs-lookup"><span data-stu-id="181cb-146">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="181cb-147">选择 " **编辑应用程序包** " 以查看 **应用程序详细信息** 页。</span><span class="sxs-lookup"><span data-stu-id="181cb-147">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="181cb-148">编辑应用程序详细信息页中的字段将更新作为应用程序包一部分最终交付的文件上的 manifest.js的内容。</span><span class="sxs-lookup"><span data-stu-id="181cb-148">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> <span data-ttu-id="181cb-149">*请参阅*[应用程序 Studio 清单编辑器](https://aka.ms/teams-toolkit-manifest)</span><span class="sxs-lookup"><span data-stu-id="181cb-149">*See* [App Studio manifest editor](https://aka.ms/teams-toolkit-manifest)</span></span>

## <a name="package-your-app"></a><span data-ttu-id="181cb-150">打包应用程序</span><span class="sxs-lookup"><span data-stu-id="181cb-150">Package your app</span></span>

<span data-ttu-id="181cb-151">修改 **应用程序详细信息** 页或更新 **清单**，或应用程序的 **. publish** 文件夹中的 **env** 文件将自动生成 **Development.zip** 文件。</span><span class="sxs-lookup"><span data-stu-id="181cb-151">Modifying the **app details** page or updating the **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="181cb-152">您需要在同一文件夹中包含 [两个图标](../concepts/build-and-test/apps-package.md#icons) 。</span><span class="sxs-lookup"><span data-stu-id="181cb-152">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#icons) in that same folder.</span></span>

## <a name="run-your-app"></a><span data-ttu-id="181cb-153">运行应用程序</span><span class="sxs-lookup"><span data-stu-id="181cb-153">Run your app</span></span>

### <a name="install-and-run-your-app-locally"></a><span data-ttu-id="181cb-154">在本地安装和运行应用程序</span><span class="sxs-lookup"><span data-stu-id="181cb-154">Install and run your app locally</span></span>

<span data-ttu-id="181cb-155">有关如何打包和测试您的应用程序的详细说明，请参阅在项目主页中 *生成和运行* 内容。</span><span class="sxs-lookup"><span data-stu-id="181cb-155">Refer to the \**Build and Run* content in your project homepage for detailed instructions on how to package and test your app.</span></span> <span data-ttu-id="181cb-156">通常情况下，您需要安装应用程序的服务器，使其运行，然后设置隧道解决方案，以便团队可以访问本地主机中运行的内容。</span><span class="sxs-lookup"><span data-stu-id="181cb-156">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

### <a name="enable-development-from-localhost"></a><span data-ttu-id="181cb-157">启用从 localhost 开发</span><span class="sxs-lookup"><span data-stu-id="181cb-157">Enable development from localhost</span></span>

<span data-ttu-id="181cb-158">如果您希望使用 HTTPS 在 localhost 上调试基于选项卡的应用程序，您需要告诉浏览器信任正在提供的应用程序 <https://localhost> 。</span><span class="sxs-lookup"><span data-stu-id="181cb-158">If you wish to debug your tab based app on localhost using HTTPS, you will need to tell your browser to trust the app being served from <https://localhost>.</span></span> <span data-ttu-id="181cb-159">导航到 <https://localhost:3000/tab>。</span><span class="sxs-lookup"><span data-stu-id="181cb-159">Navigate to <https://localhost:3000/tab>.</span></span> <span data-ttu-id="181cb-160">如果您看到一条警告消息，指示该网站不受信任，请选择 "继续" 选项。</span><span class="sxs-lookup"><span data-stu-id="181cb-160">If you see a warning indicating that the site isn't trusted, choose the option to proceed anyway.</span></span> <span data-ttu-id="181cb-161">现在应可以从团队客户端访问您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="181cb-161">Your app should now be accessible from the Teams client.</span></span>

### <a name="run-your-app-in-teams"></a><span data-ttu-id="181cb-162">在团队中运行应用程序</span><span class="sxs-lookup"><span data-stu-id="181cb-162">Run your app in Teams</span></span>

<span data-ttu-id="181cb-163">先决条件： [启用团队开发人员预览模式](https://aka.ms/teams-toolkit-enable-devpreview)</span><span class="sxs-lookup"><span data-stu-id="181cb-163">Prerequisites: [Enable Teams developer preview mode](https://aka.ms/teams-toolkit-enable-devpreview)</span></span>

1. <span data-ttu-id="181cb-164">导航到 Visual Studio "代码" 窗口左侧的 "活动" 栏。</span><span class="sxs-lookup"><span data-stu-id="181cb-164">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="181cb-165">选择 " **运行** " 图标以显示 " **运行" 和 "调试** " 视图。</span><span class="sxs-lookup"><span data-stu-id="181cb-165">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="181cb-166">您还可以使用键盘快捷方式 `Ctrl+Shift+D` 。</span><span class="sxs-lookup"><span data-stu-id="181cb-166">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="181cb-167">下一步：维护和支持发布的应用程序</span><span class="sxs-lookup"><span data-stu-id="181cb-167">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
