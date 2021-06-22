---
title: 入门 - 使用应用生成Teams应用SPFx
author: zhenyasav
description: 了解如何使用自定义选项卡生成SharePoint 框架
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.openlocfilehash: 7bbbf7ae1d74a9094af5bc6ca4b3ac797ba05d5d
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037661"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a><span data-ttu-id="71158-103">使用应用生成并运行Microsoft Teams应用SharePoint 框架 (SPFx) </span><span class="sxs-lookup"><span data-stu-id="71158-103">Build and run your first Microsoft Teams app with SharePoint Framework (SPFx)</span></span>

<span data-ttu-id="71158-104">在本教程中，你将在Microsoft Teams应用SharePoint 框架 (SPFx) 一个简单的个人应用。</span><span class="sxs-lookup"><span data-stu-id="71158-104">In this tutorial, you will create a new Microsoft Teams app in SharePoint Framework (SPFx) that implements a simple personal app.</span></span> <span data-ttu-id="71158-105"> (个人应用包括一组作用域为供个人使用的选项卡。) 在本教程中，你将了解 Teams 应用的结构、如何在本地运行应用以及如何将应用部署到 SharePoint。</span><span class="sxs-lookup"><span data-stu-id="71158-105">(A *personal app* includes a set of tabs scoped for individual use.) During the tutorial, you will learn about the structure of a Teams app, how to run the app locally, and how to deploy the app to SharePoint.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="71158-106">准备工作</span><span class="sxs-lookup"><span data-stu-id="71158-106">Before you begin</span></span>

<span data-ttu-id="71158-107">通过安装[先决条件](prerequisites.md)确保您的开发环境已设置</span><span class="sxs-lookup"><span data-stu-id="71158-107">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="71158-108">安装先决条件</span><span class="sxs-lookup"><span data-stu-id="71158-108">Install prerequisites</span></span>](prerequisites.md)

## <a name="get-organized"></a><span data-ttu-id="71158-109">有序整理</span><span class="sxs-lookup"><span data-stu-id="71158-109">Get organized</span></span>

<span data-ttu-id="71158-110">除了先决条件之外，您还需要是网站集SharePoint管理员。</span><span class="sxs-lookup"><span data-stu-id="71158-110">In addition to the prerequisites, you also need to be an Administrator for a SharePoint Site Collection.</span></span>  <span data-ttu-id="71158-111">你将在此位置部署要托管的应用。</span><span class="sxs-lookup"><span data-stu-id="71158-111">This is where you will deploy your app for hosting.</span></span>  <span data-ttu-id="71158-112">如果你使用的是 M365 开发人员计划租户，请使用注册该计划时设置的管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="71158-112">If you are using an M365 developer program tenant, use the administrator account you set up when you registered for the program.</span></span>  

## <a name="create-your-project"></a><span data-ttu-id="71158-113">创建项目</span><span class="sxs-lookup"><span data-stu-id="71158-113">Create your project</span></span>

<span data-ttu-id="71158-114">使用 Teams 工具包创建你的第一个项目:</span><span class="sxs-lookup"><span data-stu-id="71158-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="71158-115">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="71158-115">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="71158-116">打开 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="71158-116">Open Visual Studio code.</span></span>
1. <span data-ttu-id="71158-117">通过选择边栏中的 Teams 图标，打开 Teams 工具包:</span><span class="sxs-lookup"><span data-stu-id="71158-117">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code 边栏中的 Teams 图标。":::

1. <span data-ttu-id="71158-119">选择 **创建新项目**。</span><span class="sxs-lookup"><span data-stu-id="71158-119">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. <span data-ttu-id="71158-121">选择 **创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="71158-121">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="&quot;创建新项目&quot;的向导启动":::

1. <span data-ttu-id="71158-123">在 **选择功能** 步骤中， **选项卡** 功能已被选中。</span><span class="sxs-lookup"><span data-stu-id="71158-123">On the **Select capabilities** step, the **Tab** capability will already be selected.</span></span>  <span data-ttu-id="71158-124">按 **确定**。</span><span class="sxs-lookup"><span data-stu-id="71158-124">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="显示如何向新应用添加功能的屏幕截图。":::

1. <span data-ttu-id="71158-126">在"**前端托管类型"步骤中**，选择 **"SharePoint 框架 (SPFx) "。**</span><span class="sxs-lookup"><span data-stu-id="71158-126">On the **Frontend hosting type** step, select **SharePoint Framework (SPFx)**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="显示如何选择新应用的托管的屏幕截图。":::

1. <span data-ttu-id="71158-128">在"**框架"** 步骤中，选择 **"React"。**</span><span class="sxs-lookup"><span data-stu-id="71158-128">On the **Framework** step, select **React**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="选择框架":::

1. <span data-ttu-id="71158-130">当系统询问 **Web 部件名称时**，按 **Enter** 接受默认值。</span><span class="sxs-lookup"><span data-stu-id="71158-130">When asked for a **Webpart Name**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="71158-131">当系统询问 **Web 部件说明时**，按 **Enter** 接受默认值。</span><span class="sxs-lookup"><span data-stu-id="71158-131">When asked for the **Webpart Description**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="71158-132">当系统要求 **使用编程语言时**，按 **Enter** 接受默认值。</span><span class="sxs-lookup"><span data-stu-id="71158-132">When asked for the **Programming Language**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="71158-133">选择工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="71158-133">Select a workspace folder.</span></span>  <span data-ttu-id="71158-134">将在工作区文件夹中为正在创建的项目创建一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="71158-134">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="71158-135">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="71158-135">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="71158-136">应用的名称只能包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="71158-136">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="71158-137">按 **Enter** 以继续。</span><span class="sxs-lookup"><span data-stu-id="71158-137">Press **Enter** to continue.</span></span>

<span data-ttu-id="71158-138">将在数秒钟内创建你的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="71158-138">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="71158-139">命令行</span><span class="sxs-lookup"><span data-stu-id="71158-139">Command line</span></span>](#tab/cli)

<span data-ttu-id="71158-140">使用 `teamsfx` CLI 创建你的第一个项目。</span><span class="sxs-lookup"><span data-stu-id="71158-140">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="71158-141">从要创建项目文件夹的文件夹开始。</span><span class="sxs-lookup"><span data-stu-id="71158-141">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="71158-142">CLI 会提出一些问题来引导创建项目。</span><span class="sxs-lookup"><span data-stu-id="71158-142">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="71158-143">每个问题将告诉你该如何回答（例如，使用箭头键选择一个选项）。</span><span class="sxs-lookup"><span data-stu-id="71158-143">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="71158-144">如果已回答问题，请通过按 **Enter** 确认。</span><span class="sxs-lookup"><span data-stu-id="71158-144">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="71158-145">选择 **"创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="71158-145">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="71158-146">选择" **选项卡** 功能。</span><span class="sxs-lookup"><span data-stu-id="71158-146">Choose the **Tab** capability.</span></span>
1. <span data-ttu-id="71158-147">选择 **SharePoint 框架 (SPFx)** 前端托管。</span><span class="sxs-lookup"><span data-stu-id="71158-147">Select **SharePoint Framework (SPFx)** frontend hosting.</span></span>
1. <span data-ttu-id="71158-148">选择 **React** 框架"。</span><span class="sxs-lookup"><span data-stu-id="71158-148">Select **React** framework.</span></span>
1. <span data-ttu-id="71158-149">按 **Enter** 作为 **Web 部件名称**。</span><span class="sxs-lookup"><span data-stu-id="71158-149">Press **Enter** for the **Webpart Name**.</span></span>
1. <span data-ttu-id="71158-150">按 **Enter** 键查看 **Web 部件说明**。</span><span class="sxs-lookup"><span data-stu-id="71158-150">Press **Enter** for the **Webpart Description**.</span></span>
1. <span data-ttu-id="71158-151">按 **Enter** 键 **以使用编程语言**。</span><span class="sxs-lookup"><span data-stu-id="71158-151">Press **Enter** for the **Programming Language**.</span></span>
1. <span data-ttu-id="71158-152">按 **Enter** 选择默认工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="71158-152">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="71158-153">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="71158-153">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="71158-154">应用的名称只能包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="71158-154">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="71158-155">回答所有问题后，将创建项目。</span><span class="sxs-lookup"><span data-stu-id="71158-155">Once all the questions have been answered, your project will be created.</span></span>

---

- [<span data-ttu-id="71158-156">详细了解如何针对 SharePoint 框架</span><span class="sxs-lookup"><span data-stu-id="71158-156">Learn more about developing for SharePoint Framework</span></span>](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="71158-157">浏览源代码</span><span class="sxs-lookup"><span data-stu-id="71158-157">Take a tour of the source code</span></span>

<span data-ttu-id="71158-158">若要暂时跳过此部分，可以 [在本地运行应用](#run-your-app-locally)。</span><span class="sxs-lookup"><span data-stu-id="71158-158">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="71158-159">配置Teams Toolkit后，你具有组件来构建托管在项目Teams应用程序内的基本个人SharePoint 框架。</span><span class="sxs-lookup"><span data-stu-id="71158-159">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams that is hosted within the SharePoint Framework.</span></span>  <span data-ttu-id="71158-160">项目目录和文件显示在 Visual Studio 代码的资源管理器区域中。</span><span class="sxs-lookup"><span data-stu-id="71158-160">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="显示 Visual Studio Code 中个人应用的应用项目文件的屏幕截图。":::

<span data-ttu-id="71158-162">工具包根据你在设置过程中添加的功能，自动在项目目录中创建标点文件夹。</span><span class="sxs-lookup"><span data-stu-id="71158-162">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="71158-163">Teams 工具包将保持其对于新目录中 `.fx` 的状态。</span><span class="sxs-lookup"><span data-stu-id="71158-163">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="71158-164">此目录中的其他项：</span><span class="sxs-lookup"><span data-stu-id="71158-164">Among other items in this directory:</span></span>

- <span data-ttu-id="71158-165">应用图标在 `color.png` 和 `outline.png`中存储为 PNG 文件。</span><span class="sxs-lookup"><span data-stu-id="71158-165">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="71158-166">发布到开发人员门户 for Teams的应用程序清单存储在 中 `manifest.source.json` 。</span><span class="sxs-lookup"><span data-stu-id="71158-166">The app manifest for publishing to Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="71158-167">创建项目时选择的设置存储在 `settings.json`。</span><span class="sxs-lookup"><span data-stu-id="71158-167">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="71158-168">由于你选择了SPFx Web 部件项目，因此以下文件与 UI 相关：</span><span class="sxs-lookup"><span data-stu-id="71158-168">Since you selected a SPFx Webpart project, the following files are relevant to your UI:</span></span>

- <span data-ttu-id="71158-169">该文件夹 `SPFx/src/webparts/{webpart}` 包含你的SPFx Web 部件。</span><span class="sxs-lookup"><span data-stu-id="71158-169">The folder `SPFx/src/webparts/{webpart}` contains your SPFx webpart.</span></span>
- <span data-ttu-id="71158-170">该文件 `.vscode/launch.json` 描述了调试调色板中提供的调试配置。</span><span class="sxs-lookup"><span data-stu-id="71158-170">The file `.vscode/launch.json` describes the debugging configurations available in the debug palette.</span></span>

<span data-ttu-id="71158-171">有关 Web 部件SharePoint有关详细信息，Teams请参阅[SharePoint文档](/sharepoint/dev/spfx/build-for-teams-overview)。</span><span class="sxs-lookup"><span data-stu-id="71158-171">For more information about SharePoint Webparts for Teams, [refer to the SharePoint documentation](/sharepoint/dev/spfx/build-for-teams-overview).</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="71158-172">在本地运行应用</span><span class="sxs-lookup"><span data-stu-id="71158-172">Run your app locally</span></span>

<span data-ttu-id="71158-173">Teams Toolkit允许你在本地托管应用，并通过工作台SharePoint 框架[它](/sharepoint/dev/spfx/debug-in-vscode)。</span><span class="sxs-lookup"><span data-stu-id="71158-173">Teams Toolkit allows you to host your app locally and run it through the [SharePoint Framework Workbench](/sharepoint/dev/spfx/debug-in-vscode).</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="71158-174">在 Visual Studio Code 本地生成和运行应用</span><span class="sxs-lookup"><span data-stu-id="71158-174">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="71158-175">若要在本地构建和运行应用，请执行：</span><span class="sxs-lookup"><span data-stu-id="71158-175">To build and run your app locally:</span></span>

1. <span data-ttu-id="71158-176">从Visual Studio Code，按 **F5。**</span><span class="sxs-lookup"><span data-stu-id="71158-176">From Visual Studio Code, press **F5**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="显示如何在本地工作台SPFx应用屏幕截图。":::

   > [!NOTE]
   > <span data-ttu-id="71158-178">首次运行该应用时，将下载所有依赖项并编译该应用。</span><span class="sxs-lookup"><span data-stu-id="71158-178">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="71158-179">生成完成后，浏览器窗口将自动打开并SharePoint工作台。</span><span class="sxs-lookup"><span data-stu-id="71158-179">A browser window automatically opens and loads the SharePoint Workbench when the build is complete.</span></span>  <span data-ttu-id="71158-180">这可能需要 3-5 分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="71158-180">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="71158-181">加载SharePoint工作台后。</span><span class="sxs-lookup"><span data-stu-id="71158-181">Once the SharePoint Workbench is loaded.</span></span>

   >[!NOTE]
   > <span data-ttu-id="71158-182">如有必要，工具包会提示你安装本地证书。</span><span class="sxs-lookup"><span data-stu-id="71158-182">The Toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="71158-183">此证书允许 Teams 从 `https://localhost`。</span><span class="sxs-lookup"><span data-stu-id="71158-183">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="71158-184">出现下列对话框时，选择"是"：</span><span class="sxs-lookup"><span data-stu-id="71158-184">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="显示如何安装 SSL 证书以便 Teams 从 localhost 加载应用程序提示的屏幕截图。":::

1. <span data-ttu-id="71158-186">按"添加 **Web 部件** " (+) 图标之一添加 Web 部件。</span><span class="sxs-lookup"><span data-stu-id="71158-186">Press one of the **Add Webpart** (+) icons to add your webpart.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart.png" alt-text="Screenshot showing the SPFx workbench running with the popup to add a webpart showing.":::

1. <span data-ttu-id="71158-188">从菜单中选择 Web 部件。</span><span class="sxs-lookup"><span data-stu-id="71158-188">Choose your webpart from the menu.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart2.png" alt-text="Screenshot showing the SPFx workbench running with the popup to add a webpart selection.":::

<span data-ttu-id="71158-190">你的应用现在应该正在运行。</span><span class="sxs-lookup"><span data-stu-id="71158-190">Your app should now be running.</span></span>  <span data-ttu-id="71158-191">你可以执行正常的调试活动，就像在 Web 部件SPFx一样 (例如设置断点) 。</span><span class="sxs-lookup"><span data-stu-id="71158-191">You can do normal debugging activities as if this were any other SPFx webpart (such as setting breakpoints).</span></span>

> [!TIP]
> <span data-ttu-id="71158-192">请尝试在 的 render 方法中放置断点 `SPFx/src/webparts/{webpart}/{webpart}.ts` 并重新加载浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="71158-192">Try placing breakpoints in the render method of `SPFx/src/webparts/{webpart}/{webpart}.ts` and reloading the browser window.</span></span> <span data-ttu-id="71158-193">VS Code断点处停止。</span><span class="sxs-lookup"><span data-stu-id="71158-193">VS Code will stop on breakpoints in your code.</span></span>

## <a name="deploy-your-app-to-sharepoint"></a><span data-ttu-id="71158-194">将应用部署到SharePoint</span><span class="sxs-lookup"><span data-stu-id="71158-194">Deploy your app to SharePoint</span></span>

<span data-ttu-id="71158-195">确保SharePoint中存在应用程序目录。</span><span class="sxs-lookup"><span data-stu-id="71158-195">Ensure a SharePoint App Catalog exists in your deployment.</span></span>  <span data-ttu-id="71158-196">如果其中一个不存在， [请创建一个](/sharepoint/use-app-catalog)。</span><span class="sxs-lookup"><span data-stu-id="71158-196">If one does not exist, [create one](/sharepoint/use-app-catalog).</span></span>  <span data-ttu-id="71158-197">可能需要 15 分钟才能完全创建应用程序目录。</span><span class="sxs-lookup"><span data-stu-id="71158-197">It may take up to 15 minutes for the app catalog to be fully created.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="71158-198">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="71158-198">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="71158-199">打开 Visual Studio 代码。</span><span class="sxs-lookup"><span data-stu-id="71158-199">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="71158-200">选择Teams Toolkit图标，从边栏Teams图标。</span><span class="sxs-lookup"><span data-stu-id="71158-200">Select the Teams Toolkit from the sidebar by selecting the Teams icon.</span></span>
1. <span data-ttu-id="71158-201">选择 **"在云中预配"。**</span><span class="sxs-lookup"><span data-stu-id="71158-201">Select **Provision in the Cloud**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="显示设置命令的屏幕截图":::

1. <span data-ttu-id="71158-203">可以通过查看右下角的对话框来监视进度。</span><span class="sxs-lookup"><span data-stu-id="71158-203">You can monitor the progress by watching the dialogs in the bottom right corner.</span></span>  <span data-ttu-id="71158-204">几秒钟后，你将看到以下通知：</span><span class="sxs-lookup"><span data-stu-id="71158-204">After a few seconds, you will see the following notice:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="显示预配完成对话框的屏幕截图。":::

1. <span data-ttu-id="71158-206">预配完成后，选择"**部署到云"。**</span><span class="sxs-lookup"><span data-stu-id="71158-206">Once provisioning is complete, select **Deploy to the cloud**.</span></span>

1. <span data-ttu-id="71158-207">目前，自动化部署不可用。</span><span class="sxs-lookup"><span data-stu-id="71158-207">Currently, automated deployment is not available.</span></span>  <span data-ttu-id="71158-208">将弹出一个对话框，提示你手动生成和部署。</span><span class="sxs-lookup"><span data-stu-id="71158-208">A dialog will pop up prompting you to build and deploy manually.</span></span> <span data-ttu-id="71158-209">按 **生成SharePoint包**。</span><span class="sxs-lookup"><span data-stu-id="71158-209">Press **Build SharePoint Package**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/build-sharepoint-package.png" alt-text="&quot;生成 Sharepoint 包&quot;对话框的屏幕截图":::

# <a name="command-line"></a>[<span data-ttu-id="71158-211">命令行</span><span class="sxs-lookup"><span data-stu-id="71158-211">Command line</span></span>](#tab/cli)

<span data-ttu-id="71158-212">在终端窗口中：</span><span class="sxs-lookup"><span data-stu-id="71158-212">In your terminal window:</span></span>

1. <span data-ttu-id="71158-213">运行 `teamsfx provision`。</span><span class="sxs-lookup"><span data-stu-id="71158-213">Run `teamsfx provision`.</span></span>

   ``` bash
   teamsfx provision
   ```

   <span data-ttu-id="71158-214">系统可能会提示你登录到 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="71158-214">You may be prompted to log in to your Azure subscription.</span></span>  <span data-ttu-id="71158-215">如果需要，系统将提示你选择要用于 Azure 资源的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="71158-215">If required, you will be prompted to select an Azure subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="71158-216">始终有一些用于托管应用的 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="71158-216">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="71158-217">运行 `teamsfx deploy`。</span><span class="sxs-lookup"><span data-stu-id="71158-217">Run `teamsfx deploy`.</span></span>

   ``` bash
   teamsfx deploy
   ```

1. <span data-ttu-id="71158-218">当系统提示时，选择生成 **SharePoint包"。**</span><span class="sxs-lookup"><span data-stu-id="71158-218">When prompted, select **Build SharePoint Package**.</span></span>

---

<span data-ttu-id="71158-219">the SharePoint package is located `SPFx/sharepoint/solution` in within your project.</span><span class="sxs-lookup"><span data-stu-id="71158-219">The SharePoint package is located in `SPFx/sharepoint/solution` within your project.</span></span>  <span data-ttu-id="71158-220">Upload程序包以SharePoint：</span><span class="sxs-lookup"><span data-stu-id="71158-220">Upload the package to SharePoint:</span></span>

1. <span data-ttu-id="71158-221">登录到 M365 管理控制台，然后导航到SharePoint应用程序目录。</span><span class="sxs-lookup"><span data-stu-id="71158-221">Log into the M365 Admin Console, then navigate to the SharePoint App Catalog.</span></span>

   - <span data-ttu-id="71158-222">打开 `https://admin.microsoft.com/AdminPortal/Home` 。</span><span class="sxs-lookup"><span data-stu-id="71158-222">Open `https://admin.microsoft.com/AdminPortal/Home`.</span></span>
   - <span data-ttu-id="71158-223">在 **"管理中心**"下 **，SharePoint管理** 中心"。</span><span class="sxs-lookup"><span data-stu-id="71158-223">Under **Admin centers**, select the **SharePoint** admin center.</span></span>
   - <span data-ttu-id="71158-224">从 **边栏菜单中** 选择"更多功能"。</span><span class="sxs-lookup"><span data-stu-id="71158-224">Select **More features** from the sidebar menu.</span></span>
   - <span data-ttu-id="71158-225">按 **"应用"** 下的"**打开"。**</span><span class="sxs-lookup"><span data-stu-id="71158-225">Press **Open** under **Apps**.</span></span>
   - <span data-ttu-id="71158-226">选择 **"应用程序目录"。**</span><span class="sxs-lookup"><span data-stu-id="71158-226">Select **App Catalog**.</span></span>

1. <span data-ttu-id="71158-227">选择 **"为用户分配SharePoint"。**</span><span class="sxs-lookup"><span data-stu-id="71158-227">Select **Distribute apps for SharePoint**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="分配适用于SharePoint。":::

1. <span data-ttu-id="71158-229">选择 **"Upload"。**</span><span class="sxs-lookup"><span data-stu-id="71158-229">Select **Upload**.</span></span>

1. <span data-ttu-id="71158-230">按 **"选择文件"。**</span><span class="sxs-lookup"><span data-stu-id="71158-230">Press **Choose File**.</span></span>

1. <span data-ttu-id="71158-231">找到 `{project}.sppkg` 位于项目内的 `SPFx/sharepoint/solution` 文件夹中的文件。</span><span class="sxs-lookup"><span data-stu-id="71158-231">Locate your `{project}.sppkg` file, located in the `SPFx/sharepoint/solution` folder within your project.</span></span>  <span data-ttu-id="71158-232">按 **"打开"。**</span><span class="sxs-lookup"><span data-stu-id="71158-232">Press **Open**.</span></span>

1. <span data-ttu-id="71158-233">按 **确定**。</span><span class="sxs-lookup"><span data-stu-id="71158-233">Press **OK**.</span></span>

1. <span data-ttu-id="71158-234">将自动SharePoint部署过程。</span><span class="sxs-lookup"><span data-stu-id="71158-234">The SharePoint deployment process will automatically start.</span></span>  <span data-ttu-id="71158-235">确保 **选中"使此解决方案对组织的所有网站** 都可用"，然后按"部署 **"。**</span><span class="sxs-lookup"><span data-stu-id="71158-235">Ensure **Make this solution available to all sites in the organization** is checked, then press **Deploy**.</span></span>

1. <span data-ttu-id="71158-236">选择" **文件"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="71158-236">Select the **FILES** tab.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="选择应用程序目录中的文件SharePoint选项卡。":::

1. <span data-ttu-id="71158-238">选择已部署的程序包，然后按"同步 **"Teams** 功能区中的"同步"。</span><span class="sxs-lookup"><span data-stu-id="71158-238">select the package you deployed, then press **Sync to Teams** in the ribbon.</span></span>

    > [!Note]
    > <span data-ttu-id="71158-239">同步到Teams可能需要几分钟。</span><span class="sxs-lookup"><span data-stu-id="71158-239">The Sync to Teams process can take a couple of minutes.</span></span>  <span data-ttu-id="71158-240">你将在浏览器的右侧看到一条消息，指示应用已成功同步到Teams。</span><span class="sxs-lookup"><span data-stu-id="71158-240">You will see a message on the right-hand side of the browser indicating that the app has successfully synchronized to Teams.</span></span>

<span data-ttu-id="71158-241">打开Teams应用程序 (或登录 `https://teams.microsoft.com`) 。</span><span class="sxs-lookup"><span data-stu-id="71158-241">Open the Teams application (or sign in at `https://teams.microsoft.com`).</span></span>  <span data-ttu-id="71158-242">按边栏上的三点，然后选择"所有 **应用"。**</span><span class="sxs-lookup"><span data-stu-id="71158-242">Press the triple-dot on the sidebar, then select **All apps**.</span></span>  <span data-ttu-id="71158-243">该应用将放置在为 **组织类别构建的应用** 中。</span><span class="sxs-lookup"><span data-stu-id="71158-243">The app will be placed in the **Apps built for your org** category.</span></span>  <span data-ttu-id="71158-244">你可以从该添加应用。</span><span class="sxs-lookup"><span data-stu-id="71158-244">You can add the app from there.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="显示应用程序内应用的Teams":::

## <a name="see-also"></a><span data-ttu-id="71158-246">另请参阅</span><span class="sxs-lookup"><span data-stu-id="71158-246">See also</span></span>

- [<span data-ttu-id="71158-247">使用 React 创建 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="71158-247">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="71158-248">使用 Blazor 创建 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="71158-248">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- [<span data-ttu-id="71158-249">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="71158-249">Create a messaging extension</span></span>](first-message-extension.md)

## <a name="next-step"></a><span data-ttu-id="71158-250">后续步骤</span><span class="sxs-lookup"><span data-stu-id="71158-250">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="71158-251">创建对话机器人应用</span><span class="sxs-lookup"><span data-stu-id="71158-251">Create a conversational bot app</span></span>](first-app-bot.md)
