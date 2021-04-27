---
title: 使用 Microsoft Teams Toolkit 和 Visual Studio 代码生成应用
description: 开始使用 Microsoft Teams Visual Studio直接在 Visual Studio Code 中生成出色的自定义Toolkit
keywords: teams visual studio code toolkit
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 59f2943f37856c42346b2ffad4e01d88910679ae
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020259"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="c8696-104">使用 Teams 应用和Toolkit Visual Studio生成应用</span><span class="sxs-lookup"><span data-stu-id="c8696-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="c8696-105">借助 Microsoft Teams 工具包，可以直接在 Visual Studio Code 环境中创建自定义 Teams 应用程序。</span><span class="sxs-lookup"><span data-stu-id="c8696-105">The Microsoft Teams Toolkit enables you to create custom Teams apps directly within the Visual Studio Code environment.</span></span> <span data-ttu-id="c8696-106">此工具包将引导你完成整个过程，并提供构建、调试和启动 Teams 应用所需的一切资源。</span><span class="sxs-lookup"><span data-stu-id="c8696-106">The toolkit guides you through the process and provides everything you need to build, debug, and launch your Teams app.</span></span>

## <a name="installing-the-teams-toolkit"></a><span data-ttu-id="c8696-107">安装 Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="c8696-107">Installing the Teams Toolkit</span></span>

<span data-ttu-id="c8696-108">Microsoft Teams Toolkit for Visual Studio Code 可从 Visual Studio [Marketplace](https://aka.ms/teams-toolkit) 下载，或直接作为 Visual Studio Code 中的扩展。</span><span class="sxs-lookup"><span data-stu-id="c8696-108">The Microsoft Teams Toolkit for Visual Studio Code is available for download from the [Visual Studio Marketplace](https://aka.ms/teams-toolkit) or directly as an extension within Visual Studio Code.</span></span>

> [!TIP]
> <span data-ttu-id="c8696-109">安装后，你应该会看到 Teams Toolkit代码Visual Studio栏中。</span><span class="sxs-lookup"><span data-stu-id="c8696-109">After installation, you should see the Teams Toolkit in the Visual Studio Code activity bar.</span></span> <span data-ttu-id="c8696-110">如果没有，请在活动栏中右键单击并选择 Microsoft **Teams** 固定工具包，方便访问。</span><span class="sxs-lookup"><span data-stu-id="c8696-110">If not, right-click within the activity bar and select **Microsoft Teams** to pin the toolkit for easy access.</span></span>

## <a name="using-the-toolkit"></a><span data-ttu-id="c8696-111">使用工具包</span><span class="sxs-lookup"><span data-stu-id="c8696-111">Using the toolkit</span></span>

- [<span data-ttu-id="c8696-112">设置新项目</span><span class="sxs-lookup"><span data-stu-id="c8696-112">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="c8696-113">导入现有项目</span><span class="sxs-lookup"><span data-stu-id="c8696-113">Import an existing project</span></span>](#import-an-existing-teams-app-project)
- [<span data-ttu-id="c8696-114">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="c8696-114">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="c8696-115">打包应用</span><span class="sxs-lookup"><span data-stu-id="c8696-115">Package your app</span></span>](#package-your-app)
- [<span data-ttu-id="c8696-116">在本地或在 Teams 中运行应用</span><span class="sxs-lookup"><span data-stu-id="c8696-116">Run your app locally or in Teams</span></span>](#run-your-app)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="c8696-117">设置新的 Teams 项目</span><span class="sxs-lookup"><span data-stu-id="c8696-117">Set up a new Teams project</span></span>

1. <span data-ttu-id="c8696-118">在本地环境中为项目创建工作区/文件夹。</span><span class="sxs-lookup"><span data-stu-id="c8696-118">Create a workspace/folder for your project in your local environment.</span></span>
1. <span data-ttu-id="c8696-119">在Visual Studio代码"中，选择 Teams 图标</span><span class="sxs-lookup"><span data-stu-id="c8696-119">In Visual Studio Code, select the Teams icon</span></span> ![Teams 图标](../assets/icons/favicon-16x16.png) <span data-ttu-id="c8696-121">从窗口左侧的活动栏中。</span><span class="sxs-lookup"><span data-stu-id="c8696-121">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="c8696-122">从 **命令菜单中选择Toolkit** 打开 Microsoft Teams 选项。</span><span class="sxs-lookup"><span data-stu-id="c8696-122">Select **Open the Microsoft Teams Toolkit** from the command menu.</span></span>
1. <span data-ttu-id="c8696-123">从 **命令菜单中选择创建新的 Teams** 应用。</span><span class="sxs-lookup"><span data-stu-id="c8696-123">Select **Create a new Teams app** from the command menu.</span></span>
1. <span data-ttu-id="c8696-124">当系统提示时，输入工作区的名称。</span><span class="sxs-lookup"><span data-stu-id="c8696-124">When prompted, enter the name of the workspace .</span></span> <span data-ttu-id="c8696-125">这将同时用作项目将驻留的文件夹的名称以及应用的默认名称。</span><span class="sxs-lookup"><span data-stu-id="c8696-125">This will be used as both the name of the folder where your project will reside, and the default name of your app.</span></span>
1. <span data-ttu-id="c8696-126">按 **Enter，** 你将到达" **添加功能"** 屏幕，为新应用配置属性。</span><span class="sxs-lookup"><span data-stu-id="c8696-126">Press **Enter** and you will arrive at the **Add capabilities** screen configure the properties for your new app.</span></span>
1. <span data-ttu-id="c8696-127">选择" **完成** "按钮以完成配置过程。</span><span class="sxs-lookup"><span data-stu-id="c8696-127">Select the **Finish** button to complete the configuration process.</span></span>

## <a name="import-an-existing-teams-app-project"></a><span data-ttu-id="c8696-128">导入现有 Teams 应用项目</span><span class="sxs-lookup"><span data-stu-id="c8696-128">Import an existing Teams app project</span></span>

1. <span data-ttu-id="c8696-129">在Visual Studio代码"中，选择 Teams 图标</span><span class="sxs-lookup"><span data-stu-id="c8696-129">In Visual Studio Code, select the Teams icon</span></span> ![Teams 图标](../assets/icons/favicon-16x16.png) <span data-ttu-id="c8696-131">从窗口左侧的活动栏中。</span><span class="sxs-lookup"><span data-stu-id="c8696-131">from the activity bar on the left side of the window.</span></span>
1. <span data-ttu-id="c8696-132">从 **命令菜单中选择** 导入应用包。</span><span class="sxs-lookup"><span data-stu-id="c8696-132">Select **Import app package** from the command menu.</span></span>
1. <span data-ttu-id="c8696-133">选择现有的 [Teams 应用包](../concepts/build-and-test/apps-package.md) zip 文件。</span><span class="sxs-lookup"><span data-stu-id="c8696-133">Choose your existing [Teams app package](../concepts/build-and-test/apps-package.md) zip file.</span></span>
1. <span data-ttu-id="c8696-134">选择" **选择发布程序包"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="c8696-134">Choose the **Select publishing package** button.</span></span> <span data-ttu-id="c8696-135">现在，应该使用应用的详细信息填充工具包的配置选项卡。</span><span class="sxs-lookup"><span data-stu-id="c8696-135">The configuration tab of the toolkit should now be populated with your app's details.</span></span>
1. <span data-ttu-id="c8696-136">In Visual Studio Code， select **File**  ->  **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span><span class="sxs-lookup"><span data-stu-id="c8696-136">In Visual Studio Code, select **File** -> **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="c8696-137">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="c8696-137">Configure your app</span></span>

<span data-ttu-id="c8696-138">Teams 应用的核心包括三个组件：</span><span class="sxs-lookup"><span data-stu-id="c8696-138">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="c8696-139">Microsoft Teams 客户端 (Web、桌面或移动) 用户与你的应用进行交互。</span><span class="sxs-lookup"><span data-stu-id="c8696-139">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="c8696-140">响应将在 Teams 中显示的内容请求的服务器，例如 HTML 选项卡内容或自动程序自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="c8696-140">A server that responds to requests for content that will be displayed in Teams, e.g., HTML tab content or a bot adaptive card .</span></span>
  1. <span data-ttu-id="c8696-141">包含 [三个文件的](/concepts/build-and-test/apps-package.md) Teams 应用包：</span><span class="sxs-lookup"><span data-stu-id="c8696-141">A Teams [app package](/concepts/build-and-test/apps-package.md) consisting of three files:</span></span>

  > [!div class="checklist"]
  >
  > - <span data-ttu-id="c8696-142">打开manifest.js</span><span class="sxs-lookup"><span data-stu-id="c8696-142">The manifest.json</span></span> 
  > - <span data-ttu-id="c8696-143">[要显示在](../resources/schema/manifest-schema.md#icons)公共或组织应用程序目录中的应用的颜色图标</span><span class="sxs-lookup"><span data-stu-id="c8696-143">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog</span></span>
 > - <span data-ttu-id="c8696-144">显示在 [Teams](../resources/schema/manifest-schema.md#icons) 活动栏上的大纲图标。</span><span class="sxs-lookup"><span data-stu-id="c8696-144">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="c8696-145">安装应用后，Teams 客户端将分析清单文件以确定所需信息，如应用名称和服务所在的 URL。</span><span class="sxs-lookup"><span data-stu-id="c8696-145">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="c8696-146">若要配置你的应用，请导航到 Microsoft **Teams Toolkit** 代码Visual Studio选项卡。</span><span class="sxs-lookup"><span data-stu-id="c8696-146">To configure your app, navigate to the **Microsoft Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="c8696-147">选择 **"编辑应用包** "以查看 **"应用详细信息"** 页。</span><span class="sxs-lookup"><span data-stu-id="c8696-147">Select **Edit app package** to view the **App details** page.</span></span>
1. <span data-ttu-id="c8696-148">编辑"应用详细信息"页中的字段将更新manifest.js文件（最终作为应用包的一部分提供）上的内容。</span><span class="sxs-lookup"><span data-stu-id="c8696-148">Editing the fields in the App details page updates the contents of the manifest.json file that will ultimately ship as part of the app package.</span></span> <span data-ttu-id="c8696-149">*请参阅* [App Studio 清单编辑器](https://aka.ms/teams-toolkit-manifest)</span><span class="sxs-lookup"><span data-stu-id="c8696-149">*See* [App Studio manifest editor](https://aka.ms/teams-toolkit-manifest)</span></span>

## <a name="package-your-app"></a><span data-ttu-id="c8696-150">打包应用</span><span class="sxs-lookup"><span data-stu-id="c8696-150">Package your app</span></span>

<span data-ttu-id="c8696-151">修改 **应用的**.publish文件夹中的应用程序详细信息页面、清单或 **.env** 文件将自动生成 **Development.zip文件。**</span><span class="sxs-lookup"><span data-stu-id="c8696-151">Modifying the **app details** page, **manifest**, or **.env** files in your app's  **.publish** folder will automatically generate your **Development.zip** file.</span></span> <span data-ttu-id="c8696-152">你需要在同一文件夹中 [包含两](../concepts/build-and-test/apps-package.md#app-icons) 个图标。</span><span class="sxs-lookup"><span data-stu-id="c8696-152">You'll need to include [two icons](../concepts/build-and-test/apps-package.md#app-icons) in that same folder.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="c8696-153">在本地安装和运行应用</span><span class="sxs-lookup"><span data-stu-id="c8696-153">Install and run your app locally</span></span>

## <a name="run-your-app"></a><span data-ttu-id="c8696-154">运行应用</span><span class="sxs-lookup"><span data-stu-id="c8696-154">Run your app</span></span>

### <a name="install-and-run-your-app-locally"></a><span data-ttu-id="c8696-155">在本地安装和运行应用</span><span class="sxs-lookup"><span data-stu-id="c8696-155">Install and run your app locally</span></span>

<span data-ttu-id="c8696-156">有关如何打包 *和测试应用的* 详细说明，请参阅项目主页中的 \*生成和运行内容。</span><span class="sxs-lookup"><span data-stu-id="c8696-156">Refer to the \**Build and Run* content in your project homepage for detailed instructions on how to package and test your app.</span></span> <span data-ttu-id="c8696-157">通常，你需要安装你的应用的服务器，使它运行，然后设置隧道解决方案，以便 Teams 可以访问从 localhost 运行的内容。</span><span class="sxs-lookup"><span data-stu-id="c8696-157">In general, you need to install your app's server, get it running, then setup a tunneling solution so that Teams can access content running from localhost.</span></span>

### <a name="enable-development-from-localhost"></a><span data-ttu-id="c8696-158">从 localhost 启用开发</span><span class="sxs-lookup"><span data-stu-id="c8696-158">Enable development from localhost</span></span>

<span data-ttu-id="c8696-159">如果你想要使用 HTTPS 在 localhost 上调试基于选项卡的应用，则需要告诉浏览器信任从 中提供的应用 <https://localhost> 。</span><span class="sxs-lookup"><span data-stu-id="c8696-159">If you wish to debug your tab based app on localhost using HTTPS, you will need to tell your browser to trust the app being served from <https://localhost>.</span></span> <span data-ttu-id="c8696-160">导航到 <https://localhost:3000/tab>。</span><span class="sxs-lookup"><span data-stu-id="c8696-160">Navigate to <https://localhost:3000/tab>.</span></span> <span data-ttu-id="c8696-161">如果您看到一条指示该网站不受信任的警告，请选择继续继续的选项。</span><span class="sxs-lookup"><span data-stu-id="c8696-161">If you see a warning indicating that the site isn't trusted, choose the option to proceed anyway.</span></span> <span data-ttu-id="c8696-162">现在，你的应用应可从 Teams 客户端访问。</span><span class="sxs-lookup"><span data-stu-id="c8696-162">Your app should now be accessible from the Teams client.</span></span>

### <a name="run-your-app-in-teams"></a><span data-ttu-id="c8696-163">在 Teams 中运行应用</span><span class="sxs-lookup"><span data-stu-id="c8696-163">Run your app in Teams</span></span>

<span data-ttu-id="c8696-164">先决条件： [启用 Teams 开发人员预览模式](https://aka.ms/teams-toolkit-enable-devpreview)</span><span class="sxs-lookup"><span data-stu-id="c8696-164">Prerequisites: [Enable Teams developer preview mode](https://aka.ms/teams-toolkit-enable-devpreview)</span></span>

1. <span data-ttu-id="c8696-165">导航到"代码"窗口左侧的活动Visual Studio栏。</span><span class="sxs-lookup"><span data-stu-id="c8696-165">Navigate to the activity bar on the left side of the Visual Studio Code window.</span></span>
1. <span data-ttu-id="c8696-166">选择" **运行** "图标以显示 **"运行和调试"** 视图。</span><span class="sxs-lookup"><span data-stu-id="c8696-166">Select the **Run** icon to display the **Run and Debug** view.</span></span>
1. <span data-ttu-id="c8696-167">您还可以使用键盘快捷方式 `Ctrl+Shift+D` 。</span><span class="sxs-lookup"><span data-stu-id="c8696-167">You can also use the keyboard shortcut `Ctrl+Shift+D`.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c8696-168">下一步：维护和支持已发布的应用</span><span class="sxs-lookup"><span data-stu-id="c8696-168">Next step: Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
