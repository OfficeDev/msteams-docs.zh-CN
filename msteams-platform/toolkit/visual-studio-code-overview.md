---
title: 使用 Microsoft Teams Toolkit 和 Visual Studio Code
description: 开始使用自定义工具直接在Visual Studio Code生成出色的自定义Microsoft Teams Toolkit
keywords: teams visual studio code toolkit
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: efd0962e9c4c0d64dbac47caf29b2e56907937b3
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566556"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="30a32-104">使用 Teams Toolkit 和 Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="30a32-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="30a32-105">借助 Microsoft Teams 工具包，可以直接在 Visual Studio Code 环境中创建自定义 Teams 应用程序。</span><span class="sxs-lookup"><span data-stu-id="30a32-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="30a32-106">此工具包将引导你完成整个过程，并提供构建、调试和启动 Teams 应用所需的一切资源。</span><span class="sxs-lookup"><span data-stu-id="30a32-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="30a32-107">安装Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="30a32-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="30a32-108">可以从 Microsoft Teams Toolkit 应用商店Visual Studio Code下载 Visual Studio [for Visual Studio Code。](https://aka.ms/teams-toolkit)</span><span class="sxs-lookup"><span data-stu-id="30a32-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="30a32-109">安装后，您应在活动Teams Toolkit看到Visual Studio Code栏。</span><span class="sxs-lookup"><span data-stu-id="30a32-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="30a32-110">如果没有，请在活动栏中右键单击并选择"Microsoft Teams固定工具包以轻松访问。</span><span class="sxs-lookup"><span data-stu-id="30a32-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="30a32-111">使用工具包</span><span class="sxs-lookup"><span data-stu-id="30a32-111">Using the toolkit</span></span>

- [<span data-ttu-id="30a32-112">设置新项目</span><span class="sxs-lookup"><span data-stu-id="30a32-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="30a32-113">导入现有项目</span><span class="sxs-lookup"><span data-stu-id="30a32-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="30a32-114">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="30a32-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="30a32-115">打包应用</span><span class="sxs-lookup"><span data-stu-id="30a32-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="30a32-116">在本地或本地运行Teams</span><span class="sxs-lookup"><span data-stu-id="30a32-116">Run your app locally or in Teams</span></span>](#run-your-app)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="30a32-117">设置新的Teams项目</span><span class="sxs-lookup"><span data-stu-id="30a32-117">Set up a new Teams project</span></span>

1. <span data-ttu-id="30a32-118">在本地环境中为项目创建工作区或文件夹。</span><span class="sxs-lookup"><span data-stu-id="30a32-118">Create a workspace or folder for your project in your local environment.</span></span>
1. <span data-ttu-id="30a32-119">在Visual Studio Code中，选择Teams图标</span><span class="sxs-lookup"><span data-stu-id="30a32-119">In Visual Studio Code, select the Teams icon</span></span> ![Teams 图标](../assets/icons/favicon-16x16.png) <span data-ttu-id="30a32-121">从窗口左侧的活动栏中。</span><span class="sxs-lookup"><span data-stu-id="30a32-121">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="30a32-122">从 **命令Microsoft Teams Toolkit** 选择"打开"菜单。</span><span class="sxs-lookup"><span data-stu-id="30a32-122">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="30a32-123">从 **命令菜单中Teams新建** 应用"。</span><span class="sxs-lookup"><span data-stu-id="30a32-123">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="30a32-124">当系统提示时，输入工作区的名称。</span><span class="sxs-lookup"><span data-stu-id="30a32-124">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="30a32-125">这将同时用作项目将驻留的文件夹的名称以及应用的默认名称。</span><span class="sxs-lookup"><span data-stu-id="30a32-125">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="30a32-126">按 **Enter，** 你将到达" **添加功能"** 屏幕，为新应用配置属性。</span><span class="sxs-lookup"><span data-stu-id="30a32-126">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="30a32-127">选择" **完成** "按钮以完成配置过程。</span><span class="sxs-lookup"><span data-stu-id="30a32-127">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="30a32-128">导入现有Teams应用程序项目</span><span class="sxs-lookup"><span data-stu-id="30a32-128">Import an existing Teams app project</span></span>

1. <span data-ttu-id="30a32-129">在Visual Studio Code中，选择Teams图标</span><span class="sxs-lookup"><span data-stu-id="30a32-129">In Visual Studio Code, select the Teams icon</span></span> ![Teams 图标](../assets/icons/favicon-16x16.png) <span data-ttu-id="30a32-131">从窗口左侧的活动栏中。</span><span class="sxs-lookup"><span data-stu-id="30a32-131">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="30a32-132">从 **命令菜单中选择** 导入应用包。</span><span class="sxs-lookup"><span data-stu-id="30a32-132">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="30a32-133">选择现有的应用[Teams包](../concepts/build-and-test/apps-package.md)zip 文件。</span><span class="sxs-lookup"><span data-stu-id="30a32-133">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="30a32-134">选择" **选择发布程序包"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="30a32-134">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="30a32-135">现在，应该使用应用的详细信息填充工具包的配置选项卡。</span><span class="sxs-lookup"><span data-stu-id="30a32-135">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="30a32-136">In Visual Studio Code， select **File**  ->  **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span><span class="sxs-lookup"><span data-stu-id="30a32-136">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="30a32-137">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="30a32-137">Configure your app</span></span>

<span data-ttu-id="30a32-138">应用程序的核心是Teams三个组件：</span><span class="sxs-lookup"><span data-stu-id="30a32-138">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="30a32-139">The Microsoft Teams client (web， desktop or mobile) where users interact with your app.</span><span class="sxs-lookup"><span data-stu-id="30a32-139">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="30a32-140">响应将在网站中显示的内容请求的服务器Teams。</span><span class="sxs-lookup"><span data-stu-id="30a32-140">A server that responds to requests for content that will be displayed in Teams.</span></span> <span data-ttu-id="30a32-141">例如，HTML 选项卡内容或自动程序自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="30a32-141">For example, HTML tab content or a bot adaptive card.</span></span>
  1. <span data-ttu-id="30a32-142">一Teams[文件](/concepts/build-and-test/apps-package.md)组成的应用包：</span><span class="sxs-lookup"><span data-stu-id="30a32-142">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="30a32-143">打开manifest.js。</span><span class="sxs-lookup"><span data-stu-id="30a32-143">The manifest.json.</span></span> 
      > - <span data-ttu-id="30a32-144">要 [显示在](../resources/schema/manifest-schema.md#icons) 公共或组织应用程序目录中的应用的颜色图标。</span><span class="sxs-lookup"><span data-stu-id="30a32-144">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      > - <span data-ttu-id="30a32-145">显示在[活动](../resources/schema/manifest-schema.md#icons)栏上的Teams图标。</span><span class="sxs-lookup"><span data-stu-id="30a32-145">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="30a32-146">安装应用后，Teams客户端将分析清单文件以确定所需信息，如应用名称和服务所在的 URL。</span><span class="sxs-lookup"><span data-stu-id="30a32-146">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="30a32-147">若要配置你的应用，请导航到 Microsoft Teams Toolkit **中的**"Visual Studio Code"。</span><span class="sxs-lookup"><span data-stu-id="30a32-147">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="30a32-148">选择 **"编辑应用包** "以查看 **"应用详细信息"** 页。</span><span class="sxs-lookup"><span data-stu-id="30a32-148">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="30a32-149">编辑"应用详细信息"页中的字段将更新manifest.js文件（最终作为应用包的一部分提供）上的内容。</span><span class="sxs-lookup"><span data-stu-id="30a32-149">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> <span data-ttu-id="30a32-150">有关详细信息，请参阅 [App Studio 清单编辑器](https://aka.ms/teams-toolkit-manifest)</span><span class="sxs-lookup"><span data-stu-id="30a32-150">For more information, See [App Studio manifest editor](https://aka.ms/teams-toolkit-manifest)</span></span>

## <a name="package-your-app"></a><span data-ttu-id="30a32-151">打包应用</span><span class="sxs-lookup"><span data-stu-id="30a32-151">Package your app</span></span>

<span data-ttu-id="30a32-152">修改 **应用的**.publish文件夹中的应用程序详细信息页面、清单或 **.env** 文件将自动生成 **Development.zip文件。**</span><span class="sxs-lookup"><span data-stu-id="30a32-152">Modifying the **app details** page, **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="30a32-153">你需要在同一文件夹中 [包含两](../concepts/build-and-test/apps-package.md#app-icons) 个图标。</span><span class="sxs-lookup"><span data-stu-id="30a32-153">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#app-icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="30a32-154">在本地安装和运行应用</span><span class="sxs-lookup"><span data-stu-id="30a32-154">Install and run your app locally</span></span>

## <a name="run-your-app"></a><span data-ttu-id="30a32-155">运行应用</span><span class="sxs-lookup"><span data-stu-id="30a32-155">Run your app</span></span>

### <a name="install-and-run-your-app-locally"></a><span data-ttu-id="30a32-156">在本地安装和运行应用</span><span class="sxs-lookup"><span data-stu-id="30a32-156">Install and run your app locally</span></span>

<span data-ttu-id="30a32-157">有关如何打包 **和测试应用的** 详细说明，请参阅项目主页中的生成和运行内容。</span><span class="sxs-lookup"><span data-stu-id="30a32-157">Refer to the **Build and Run** content in your project homepage for detailed instructions on how to package and test your app.</span></span> <span data-ttu-id="30a32-158">通常，你需要安装应用的服务器，运行它，然后设置隧道解决方案，以便Teams从 localhost 运行的内容。</span><span class="sxs-lookup"><span data-stu-id="30a32-158">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

### <a name="enable-development-from-localhost"></a><span data-ttu-id="30a32-159">从 localhost 启用开发</span><span class="sxs-lookup"><span data-stu-id="30a32-159">Enable development from localhost</span></span>

<span data-ttu-id="30a32-160">如果你想要使用 HTTPS 在 localhost 上调试基于选项卡的应用，则需要告诉浏览器信任从 中提供的应用 <https://localhost> 。</span><span class="sxs-lookup"><span data-stu-id="30a32-160">If you wish to debug your tab based app on localhost using HTTPS, you will need to tell your browser to trust the app being served from <https://localhost>.</span></span> <span data-ttu-id="30a32-161">导航到 <https://localhost:3000/tab>。</span><span class="sxs-lookup"><span data-stu-id="30a32-161">Navigate to <https://localhost:3000/tab>.</span></span> <span data-ttu-id="30a32-162">如果您看到一条指示该网站不受信任的警告，请选择继续继续的选项。</span><span class="sxs-lookup"><span data-stu-id="30a32-162">If you see a warning indicating that the site isn't trusted, choose the option to proceed anyway.</span></span> <span data-ttu-id="30a32-163">现在，你的应用应可从 Teams访问。</span><span class="sxs-lookup"><span data-stu-id="30a32-163">Your app should now be accessible from the Teams client.</span></span>

### <a name="run-your-app-in-teams"></a><span data-ttu-id="30a32-164">在应用商店中Teams</span><span class="sxs-lookup"><span data-stu-id="30a32-164">Run your app in Teams</span></span>

<span data-ttu-id="30a32-165">先决条件：[启用Teams预览模式](https://aka.ms/teams-toolkit-enable-devpreview)</span><span class="sxs-lookup"><span data-stu-id="30a32-165">Prerequisites: [Enable Teams developer preview mode](https://aka.ms/teams-toolkit-enable-devpreview)</span></span>

1. <span data-ttu-id="30a32-166">导航到"活动"窗口左侧的活动Visual Studio Code栏。</span><span class="sxs-lookup"><span data-stu-id="30a32-166">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="30a32-167">选择" **运行** "图标以显示 **"运行和调试"** 视图。</span><span class="sxs-lookup"><span data-stu-id="30a32-167">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="30a32-168">您还可以使用键盘快捷方式 `Ctrl+Shift+D` 。</span><span class="sxs-lookup"><span data-stu-id="30a32-168">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

## <a name="next-step"></a><span data-ttu-id="30a32-169">后续步骤</span><span class="sxs-lookup"><span data-stu-id="30a32-169">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="30a32-170">维护和支持已发布的应用</span><span class="sxs-lookup"><span data-stu-id="30a32-170">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
