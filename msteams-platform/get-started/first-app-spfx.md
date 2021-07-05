---
title: 入门 - 使用应用生成Teams应用SPFx
author: zhenyasav
description: 了解如何使用自定义选项卡生成SharePoint 框架
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.openlocfilehash: 4df2bb71837af520a2d2500a45b8605e5fae08b2
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254221"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a><span data-ttu-id="e5509-103">使用应用生成并运行Microsoft Teams应用SharePoint 框架 (SPFx) </span><span class="sxs-lookup"><span data-stu-id="e5509-103">Build and run your first Microsoft Teams app with SharePoint Framework (SPFx)</span></span>

<span data-ttu-id="e5509-104">本教程介绍如何在实现简单个人Microsoft Teams应用中SharePoint 框架 SPFx应用。</span><span class="sxs-lookup"><span data-stu-id="e5509-104">In this tutorial, you will learn how to create a new Microsoft Teams app in SharePoint Framework SPFx that implements a simple personal app.</span></span> <span data-ttu-id="e5509-105">例如，个人 *应用包括* 一组供个人使用的选项卡。</span><span class="sxs-lookup"><span data-stu-id="e5509-105">For example, a *personal app* includes a set of tabs for individual use.</span></span> <span data-ttu-id="e5509-106">在本教程中，你将了解 Teams 应用的结构、如何在本地运行应用以及如何将应用部署到 SharePoint。</span><span class="sxs-lookup"><span data-stu-id="e5509-106">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to SharePoint.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="e5509-107">开始之前</span><span class="sxs-lookup"><span data-stu-id="e5509-107">Before you begin</span></span>

<span data-ttu-id="e5509-108">请确保通过安装必备组件来设置开发环境。</span><span class="sxs-lookup"><span data-stu-id="e5509-108">Make sure your development environment is set up by installing the prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="e5509-109">安装先决条件</span><span class="sxs-lookup"><span data-stu-id="e5509-109">Install prerequisites</span></span>](prerequisites.md)

## <a name="get-organized"></a><span data-ttu-id="e5509-110">有序整理</span><span class="sxs-lookup"><span data-stu-id="e5509-110">Get organized</span></span>

<span data-ttu-id="e5509-111">除了先决条件之外，您还需要是网站集SharePoint管理员。</span><span class="sxs-lookup"><span data-stu-id="e5509-111">In addition to the prerequisites, you also need to be an Administrator for a SharePoint Site Collection.</span></span>  <span data-ttu-id="e5509-112">你将在此位置部署要托管的应用。</span><span class="sxs-lookup"><span data-stu-id="e5509-112">This is where you will deploy your app for hosting.</span></span>  <span data-ttu-id="e5509-113">如果你使用的是 M365 开发人员计划租户，请使用注册该计划时设置的管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="e5509-113">If you are using an M365 developer program tenant, use the administrator account you set up when you registered for the program.</span></span>  

## <a name="create-your-project"></a><span data-ttu-id="e5509-114">创建项目</span><span class="sxs-lookup"><span data-stu-id="e5509-114">Create your project</span></span>

<span data-ttu-id="e5509-115">使用 Teams 工具包创建你的第一个项目:</span><span class="sxs-lookup"><span data-stu-id="e5509-115">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="e5509-116">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e5509-116">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="e5509-117">打开 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="e5509-117">Open Visual Studio code.</span></span>
1. <span data-ttu-id="e5509-118">选择边Teams图标以打开Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="e5509-118">Select the Teams icon in the sidebar to open the Teams Toolkit.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code 边栏中的 Teams 图标。":::

1. <span data-ttu-id="e5509-120">选择 **创建新项目**。</span><span class="sxs-lookup"><span data-stu-id="e5509-120">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. <span data-ttu-id="e5509-122">选择 **创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="e5509-122">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="&quot;创建新项目&quot;的向导启动":::

1. <span data-ttu-id="e5509-124">在"**选择功能"** 部分，选择 **"选项卡**"，然后选择"确定 **"。**</span><span class="sxs-lookup"><span data-stu-id="e5509-124">In the **Select capabilities** section, select **Tab** and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="显示如何向新应用添加功能的屏幕截图。":::

1. <span data-ttu-id="e5509-126">在"**前端托管类型"部分**，选择 **"SharePoint 框架 (SPFx) "。**</span><span class="sxs-lookup"><span data-stu-id="e5509-126">In the **Frontend hosting type** section, select **SharePoint Framework (SPFx)**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="显示如何选择新应用的托管的屏幕截图。":::

1. <span data-ttu-id="e5509-128">在"**框架"** 部分，选择 **"React"。**</span><span class="sxs-lookup"><span data-stu-id="e5509-128">In the **Framework** section, select **React**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="选择框架":::

1. <span data-ttu-id="e5509-130">当系统询问 **Web 部件名称时**，按 **Enter** 接受默认值。</span><span class="sxs-lookup"><span data-stu-id="e5509-130">When asked for a **Webpart Name**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="e5509-131">当系统询问 **Web 部件说明时**，按 **Enter** 接受默认值。</span><span class="sxs-lookup"><span data-stu-id="e5509-131">When asked for the **Webpart Description**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="e5509-132">当系统要求 **使用编程语言时**，按 **Enter** 接受默认值。</span><span class="sxs-lookup"><span data-stu-id="e5509-132">When asked for the **Programming Language**, press **Enter** to accept the default.</span></span>

1. <span data-ttu-id="e5509-133">选择工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="e5509-133">Select a workspace folder.</span></span>  <span data-ttu-id="e5509-134">将在工作区文件夹中为正在创建的项目创建一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="e5509-134">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="e5509-135">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="e5509-135">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="e5509-136">应用的名称只能包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="e5509-136">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="e5509-137">按 **Enter** 以继续。</span><span class="sxs-lookup"><span data-stu-id="e5509-137">Press **Enter** to continue.</span></span>

   <span data-ttu-id="e5509-138">将在数秒钟内创建你的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="e5509-138">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="e5509-139">命令行</span><span class="sxs-lookup"><span data-stu-id="e5509-139">Command line</span></span>](#tab/cli)

<span data-ttu-id="e5509-140">使用 `teamsfx` CLI 创建你的第一个项目。</span><span class="sxs-lookup"><span data-stu-id="e5509-140">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="e5509-141">从要创建项目文件夹的文件夹开始。</span><span class="sxs-lookup"><span data-stu-id="e5509-141">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="e5509-142">CLI 会提出一些问题来引导创建项目。</span><span class="sxs-lookup"><span data-stu-id="e5509-142">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="e5509-143">每个问题将告诉你该如何回答（例如，使用箭头键选择一个选项）。</span><span class="sxs-lookup"><span data-stu-id="e5509-143">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="e5509-144">如果已回答问题，请通过按 **Enter** 确认。</span><span class="sxs-lookup"><span data-stu-id="e5509-144">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="e5509-145">选择 **创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="e5509-145">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="e5509-146">选择 **选项卡**。</span><span class="sxs-lookup"><span data-stu-id="e5509-146">Select **Tab**.</span></span>
1. <span data-ttu-id="e5509-147">选择 **SharePoint 框架 (SPFx)** 前端托管。</span><span class="sxs-lookup"><span data-stu-id="e5509-147">Select **SharePoint Framework (SPFx)** frontend hosting.</span></span>
1. <span data-ttu-id="e5509-148">选择 **React** 框架"。</span><span class="sxs-lookup"><span data-stu-id="e5509-148">Select **React** framework.</span></span>
1. <span data-ttu-id="e5509-149">按 **Enter** 作为 **Web 部件名称**。</span><span class="sxs-lookup"><span data-stu-id="e5509-149">Press **Enter** for the **Webpart Name**.</span></span>
1. <span data-ttu-id="e5509-150">按 **Enter** 键查看 **Web 部件说明**。</span><span class="sxs-lookup"><span data-stu-id="e5509-150">Press **Enter** for the **Webpart Description**.</span></span>
1. <span data-ttu-id="e5509-151">按 **Enter** 键 **以使用编程语言**。</span><span class="sxs-lookup"><span data-stu-id="e5509-151">Press **Enter** for the **Programming Language**.</span></span>
1. <span data-ttu-id="e5509-152">按 **Enter** 选择默认工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="e5509-152">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="e5509-153">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="e5509-153">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="e5509-154">应用的名称只能包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="e5509-154">The name of the app must consist only of alphanumeric characters.</span></span>

   <span data-ttu-id="e5509-155">在回答所有问题后，将创建项目。</span><span class="sxs-lookup"><span data-stu-id="e5509-155">After all the questions have been answered, your project will be created.</span></span>

---

- [<span data-ttu-id="e5509-156">详细了解如何针对 SharePoint 框架</span><span class="sxs-lookup"><span data-stu-id="e5509-156">Learn more about developing for SharePoint Framework</span></span>](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="e5509-157">浏览源代码</span><span class="sxs-lookup"><span data-stu-id="e5509-157">Take a tour of the source code</span></span>

<span data-ttu-id="e5509-158">若要暂时跳过此部分，可以 [在本地运行应用](#run-your-app-locally)。</span><span class="sxs-lookup"><span data-stu-id="e5509-158">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="e5509-159">配置Teams Toolkit后，你具有组件来为托管在项目Teams应用程序生成基本个人SharePoint 框架。</span><span class="sxs-lookup"><span data-stu-id="e5509-159">After the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams that is hosted within the SharePoint Framework.</span></span>  <span data-ttu-id="e5509-160">项目目录和文件显示在 Visual Studio 代码的资源管理器区域中。</span><span class="sxs-lookup"><span data-stu-id="e5509-160">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="显示 Visual Studio Code 中个人应用的应用项目文件的屏幕截图。":::

<span data-ttu-id="e5509-162">工具包根据你在设置过程中添加的功能，自动在项目目录中创建标点文件夹。</span><span class="sxs-lookup"><span data-stu-id="e5509-162">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="e5509-163">Teams 工具包将保持其对于新目录中 `.fx` 的状态。</span><span class="sxs-lookup"><span data-stu-id="e5509-163">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="e5509-164">此目录中的其他项：</span><span class="sxs-lookup"><span data-stu-id="e5509-164">Among other items in this directory:</span></span>

- <span data-ttu-id="e5509-165">应用图标在 `color.png` 和 `outline.png`中存储为 PNG 文件。</span><span class="sxs-lookup"><span data-stu-id="e5509-165">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="e5509-166">发布到开发人员门户 for Teams的应用程序清单存储在 中 `manifest.source.json` 。</span><span class="sxs-lookup"><span data-stu-id="e5509-166">The app manifest for publishing to Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="e5509-167">创建项目时选择的设置存储在 `settings.json`。</span><span class="sxs-lookup"><span data-stu-id="e5509-167">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="e5509-168">由于你选择了SPFx Web 部件项目，因此以下文件与 UI 相关：</span><span class="sxs-lookup"><span data-stu-id="e5509-168">Since you selected a SPFx Webpart project, the following files are relevant to your UI:</span></span>

- <span data-ttu-id="e5509-169">该文件夹 `SPFx/src/webparts/{webpart}` 包含你的SPFx Web 部件。</span><span class="sxs-lookup"><span data-stu-id="e5509-169">The folder `SPFx/src/webparts/{webpart}` contains your SPFx webpart.</span></span>
- <span data-ttu-id="e5509-170">该文件 `.vscode/launch.json` 描述了调试调色板中提供的调试配置。</span><span class="sxs-lookup"><span data-stu-id="e5509-170">The file `.vscode/launch.json` describes the debugging configurations available in the debug palette.</span></span>

<span data-ttu-id="e5509-171">有关 Web 部件SharePoint有关详细信息，Teams请参阅[SharePoint文档](/sharepoint/dev/spfx/build-for-teams-overview)。</span><span class="sxs-lookup"><span data-stu-id="e5509-171">For more information about SharePoint Webparts for Teams, [refer to the SharePoint documentation](/sharepoint/dev/spfx/build-for-teams-overview).</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="e5509-172">在本地运行应用</span><span class="sxs-lookup"><span data-stu-id="e5509-172">Run your app locally</span></span>

<span data-ttu-id="e5509-173">Teams Toolkit允许你在本地托管应用，并通过工作台SharePoint 框架[它](/sharepoint/dev/spfx/debug-in-vscode)。</span><span class="sxs-lookup"><span data-stu-id="e5509-173">Teams Toolkit allows you to host your app locally and run it through the [SharePoint Framework Workbench](/sharepoint/dev/spfx/debug-in-vscode).</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="e5509-174">在 Visual Studio Code 本地生成和运行应用</span><span class="sxs-lookup"><span data-stu-id="e5509-174">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="e5509-175">若要在本地构建和运行应用，请执行：</span><span class="sxs-lookup"><span data-stu-id="e5509-175">To build and run your app locally:</span></span>

1. <span data-ttu-id="e5509-176">从Visual Studio Code按 **F5** 键。</span><span class="sxs-lookup"><span data-stu-id="e5509-176">From Visual Studio Code, press the **F5** key.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="显示如何在本地工作台SPFx应用屏幕截图。":::

   > [!NOTE]
   > <span data-ttu-id="e5509-178">首次运行该应用时，将下载所有依赖项并编译该应用。</span><span class="sxs-lookup"><span data-stu-id="e5509-178">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="e5509-179">生成完成后，浏览器窗口将自动打开并SharePoint工作台。</span><span class="sxs-lookup"><span data-stu-id="e5509-179">A browser window automatically opens and loads the SharePoint Workbench when the build is complete.</span></span>  <span data-ttu-id="e5509-180">这可能需要 3-5 分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="e5509-180">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="e5509-181">加载SharePoint工作台后。</span><span class="sxs-lookup"><span data-stu-id="e5509-181">After the SharePoint Workbench is loaded.</span></span>

   >[!NOTE]
   > <span data-ttu-id="e5509-182">如有必要，工具包会提示你安装本地证书。</span><span class="sxs-lookup"><span data-stu-id="e5509-182">The Toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="e5509-183">此证书允许 Teams 从 `https://localhost`。</span><span class="sxs-lookup"><span data-stu-id="e5509-183">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="e5509-184">出现下列对话框时，选择"是"：</span><span class="sxs-lookup"><span data-stu-id="e5509-184">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="显示如何安装 SSL 证书以便 Teams 从 localhost 加载应用程序提示的屏幕截图。":::

1. <span data-ttu-id="e5509-186">选择 **"添加 Web 部件 +** 图标"以添加 Web 部件。</span><span class="sxs-lookup"><span data-stu-id="e5509-186">Select **Add Webpart +** icons to add your webpart.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart.png" alt-text="Screenshot showing the SPFx workbench running with the popup to add a webpart showing.":::

1. <span data-ttu-id="e5509-188">从菜单中选择 Web 部件。</span><span class="sxs-lookup"><span data-stu-id="e5509-188">Select your webpart from the menu.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart2.png" alt-text="Screenshot showing the SPFx workbench running with the popup to add a webpart selection.":::

   <span data-ttu-id="e5509-190">你的应用现在应该正在运行。</span><span class="sxs-lookup"><span data-stu-id="e5509-190">Your app should now be running.</span></span>  <span data-ttu-id="e5509-191">你可以执行正常的调试活动，就像在 Web 部件SPFx一样 (例如设置断点) 。</span><span class="sxs-lookup"><span data-stu-id="e5509-191">You can do normal debugging activities as if this were any other SPFx webpart (such as setting breakpoints).</span></span>

   > [!TIP]
   > <span data-ttu-id="e5509-192">请尝试在 的 render 方法中放置断点 `SPFx/src/webparts/{webpart}/{webpart}.ts` 并重新加载浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="e5509-192">Try placing breakpoints in the render method of `SPFx/src/webparts/{webpart}/{webpart}.ts` and reloading the browser window.</span></span> <span data-ttu-id="e5509-193">VS Code断点处停止。</span><span class="sxs-lookup"><span data-stu-id="e5509-193">VS Code will stop on breakpoints in your code.</span></span>

## <a name="deploy-your-app-to-sharepoint"></a><span data-ttu-id="e5509-194">将应用部署到SharePoint</span><span class="sxs-lookup"><span data-stu-id="e5509-194">Deploy your app to SharePoint</span></span>

<span data-ttu-id="e5509-195">确保SharePoint中存在应用程序目录。</span><span class="sxs-lookup"><span data-stu-id="e5509-195">Ensure a SharePoint App Catalog exists in your deployment.</span></span>  <span data-ttu-id="e5509-196">如果其中一个不存在， [请创建一个](/sharepoint/use-app-catalog)。</span><span class="sxs-lookup"><span data-stu-id="e5509-196">If one does not exist, [create one](/sharepoint/use-app-catalog).</span></span>  <span data-ttu-id="e5509-197">可能需要 15 分钟才能完全创建应用程序目录。</span><span class="sxs-lookup"><span data-stu-id="e5509-197">It may take up to 15 minutes for the app catalog to be fully created.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="e5509-198">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="e5509-198">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="e5509-199">打开 Visual Studio 代码。</span><span class="sxs-lookup"><span data-stu-id="e5509-199">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="e5509-200">选择Teams Toolkit图标，从边栏Teams图标。</span><span class="sxs-lookup"><span data-stu-id="e5509-200">Select the Teams Toolkit from the sidebar by selecting the Teams icon.</span></span>
1. <span data-ttu-id="e5509-201">选择 **"在云中预配"。**</span><span class="sxs-lookup"><span data-stu-id="e5509-201">Select **Provision in the Cloud**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="显示设置命令的屏幕截图":::

   <span data-ttu-id="e5509-203">可以通过查看右下角的对话框来监视进度。</span><span class="sxs-lookup"><span data-stu-id="e5509-203">You can monitor the progress by watching the dialogs in the bottom right corner.</span></span>  <span data-ttu-id="e5509-204">几秒钟后，你将看到以下通知：</span><span class="sxs-lookup"><span data-stu-id="e5509-204">After a few seconds, you will see the following notice:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="显示预配完成对话框的屏幕截图。":::

1. <span data-ttu-id="e5509-206">预配完成后，选择部署到 **云**。</span><span class="sxs-lookup"><span data-stu-id="e5509-206">After provisioning is complete, select **Deploy to the cloud**.</span></span>

1. <span data-ttu-id="e5509-207">目前，自动化部署不可用。</span><span class="sxs-lookup"><span data-stu-id="e5509-207">Currently, automated deployment is not available.</span></span>  <span data-ttu-id="e5509-208">将弹出一个对话框，提示你手动生成和部署。</span><span class="sxs-lookup"><span data-stu-id="e5509-208">A dialog will pop up prompting you to build and deploy manually.</span></span> <span data-ttu-id="e5509-209">选择 **生成SharePoint包。**</span><span class="sxs-lookup"><span data-stu-id="e5509-209">Select **Build SharePoint Package**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/build-sharepoint-package.png" alt-text="&quot;生成 Sharepoint 包&quot;对话框的屏幕截图":::

# <a name="command-line"></a>[<span data-ttu-id="e5509-211">命令行</span><span class="sxs-lookup"><span data-stu-id="e5509-211">Command line</span></span>](#tab/cli)

<span data-ttu-id="e5509-212">在终端窗口中：</span><span class="sxs-lookup"><span data-stu-id="e5509-212">In your terminal window:</span></span>

1. <span data-ttu-id="e5509-213">运行 `teamsfx provision`。</span><span class="sxs-lookup"><span data-stu-id="e5509-213">Run `teamsfx provision`.</span></span>

   ``` bash
   teamsfx provision
   ```

   <span data-ttu-id="e5509-214">系统可能会提示你登录到 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="e5509-214">You may be prompted to log in to your Azure subscription.</span></span>  <span data-ttu-id="e5509-215">如果需要，系统将提示你选择要用于 Azure 资源的 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="e5509-215">If required, you will be prompted to select an Azure subscription to use for the Azure resources.</span></span>

   > [!NOTE]
   > <span data-ttu-id="e5509-216">始终有一些用于托管应用的 Azure 资源。</span><span class="sxs-lookup"><span data-stu-id="e5509-216">There are always some Azure resources used for hosting your app.</span></span>

1. <span data-ttu-id="e5509-217">运行 `teamsfx deploy`。</span><span class="sxs-lookup"><span data-stu-id="e5509-217">Run `teamsfx deploy`.</span></span>

   ``` bash
   teamsfx deploy
   ```

1. <span data-ttu-id="e5509-218">当系统提示时，选择生成 **SharePoint包"。**</span><span class="sxs-lookup"><span data-stu-id="e5509-218">When prompted, select **Build SharePoint Package**.</span></span>

---

<span data-ttu-id="e5509-219">the SharePoint package is located `SPFx/sharepoint/solution` in within your project.</span><span class="sxs-lookup"><span data-stu-id="e5509-219">The SharePoint package is located in `SPFx/sharepoint/solution` within your project.</span></span>  <span data-ttu-id="e5509-220">Upload程序包以SharePoint：</span><span class="sxs-lookup"><span data-stu-id="e5509-220">Upload the package to SharePoint:</span></span>

1. <span data-ttu-id="e5509-221">登录到 M365 管理控制台，然后导航到SharePoint应用程序目录。</span><span class="sxs-lookup"><span data-stu-id="e5509-221">Log into the M365 Admin Console, then navigate to the SharePoint App Catalog.</span></span>

   1. <span data-ttu-id="e5509-222">打开 `https://admin.microsoft.com/AdminPortal/Home` 。</span><span class="sxs-lookup"><span data-stu-id="e5509-222">Open `https://admin.microsoft.com/AdminPortal/Home`.</span></span>
   1. <span data-ttu-id="e5509-223">在 **"管理中心**"下 **，SharePoint管理** 中心"。</span><span class="sxs-lookup"><span data-stu-id="e5509-223">Under **Admin centers**, select the **SharePoint** admin center.</span></span>
   1. <span data-ttu-id="e5509-224">从 **边栏菜单中** 选择"更多功能"。</span><span class="sxs-lookup"><span data-stu-id="e5509-224">Select **More features** from the sidebar menu.</span></span>
   1. <span data-ttu-id="e5509-225">按 **"应用"** 下的"**打开"。**</span><span class="sxs-lookup"><span data-stu-id="e5509-225">Press **Open** under **Apps**.</span></span>
   1. <span data-ttu-id="e5509-226">选择 **"应用程序目录"。**</span><span class="sxs-lookup"><span data-stu-id="e5509-226">Select **App Catalog**.</span></span>

1. <span data-ttu-id="e5509-227">选择 **"为用户分配SharePoint"。**</span><span class="sxs-lookup"><span data-stu-id="e5509-227">Select **Distribute apps for SharePoint**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="分配适用于SharePoint。":::

1. <span data-ttu-id="e5509-229">选择 **"Upload"。**</span><span class="sxs-lookup"><span data-stu-id="e5509-229">Select **Upload**.</span></span>

1. <span data-ttu-id="e5509-230">选择 **"选择文件"。**</span><span class="sxs-lookup"><span data-stu-id="e5509-230">Select **Choose File**.</span></span>

1. <span data-ttu-id="e5509-231">在 `{project}.sppkg` 项目内的 `SPFx/sharepoint/solution` 文件夹中找到文件。</span><span class="sxs-lookup"><span data-stu-id="e5509-231">Locate your `{project}.sppkg` file in the `SPFx/sharepoint/solution` folder within your project.</span></span> <span data-ttu-id="e5509-232">选择 **“打开”**。</span><span class="sxs-lookup"><span data-stu-id="e5509-232">Select **Open**.</span></span>

1. <span data-ttu-id="e5509-233">选择“**确定**”。</span><span class="sxs-lookup"><span data-stu-id="e5509-233">Select **OK**.</span></span>

1. <span data-ttu-id="e5509-234">将自动SharePoint部署过程。</span><span class="sxs-lookup"><span data-stu-id="e5509-234">The SharePoint deployment process will automatically start.</span></span> <span data-ttu-id="e5509-235">验证 **是否选择了"使此解决方案对组织的所有网站都** 可用"。</span><span class="sxs-lookup"><span data-stu-id="e5509-235">Verify that **Make this solution available to all sites in the organization** is selected.</span></span> <span data-ttu-id="e5509-236">然后选择部署。</span><span class="sxs-lookup"><span data-stu-id="e5509-236">Then select **Deploy**.</span></span>

1. <span data-ttu-id="e5509-237">选择" **文件"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="e5509-237">Select the **FILES** tab.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="选择应用程序目录中的文件SharePoint选项卡。":::

1. <span data-ttu-id="e5509-239">选择已部署的程序包，**然后选择"同步** Teams右上角选择" 同步"。</span><span class="sxs-lookup"><span data-stu-id="e5509-239">select the package you deployed, then select **Sync to Teams** from the upper right corner.</span></span>

    > [!Note]
    > <span data-ttu-id="e5509-240">同步到Teams可能需要几分钟。</span><span class="sxs-lookup"><span data-stu-id="e5509-240">The Sync to Teams process can take a couple of minutes.</span></span>  <span data-ttu-id="e5509-241">你将在浏览器的右侧看到一条消息，指示应用已成功同步到Teams。</span><span class="sxs-lookup"><span data-stu-id="e5509-241">You will see a message on the right-hand side of the browser indicating that the app has successfully synchronized to Teams.</span></span>

   <span data-ttu-id="e5509-242">打开Teams应用程序 (或登录 `https://teams.microsoft.com`) 。</span><span class="sxs-lookup"><span data-stu-id="e5509-242">Open the Teams application (or sign in at `https://teams.microsoft.com`).</span></span>  <span data-ttu-id="e5509-243">按边栏上的三点，然后选择"所有 **应用"。**</span><span class="sxs-lookup"><span data-stu-id="e5509-243">Press the triple-dot on the sidebar, then select **All apps**.</span></span>  <span data-ttu-id="e5509-244">该应用将放置在为 **组织类别构建的应用** 中。</span><span class="sxs-lookup"><span data-stu-id="e5509-244">The app will be placed in the **Apps built for your org** category.</span></span>  <span data-ttu-id="e5509-245">你可以从该添加应用。</span><span class="sxs-lookup"><span data-stu-id="e5509-245">You can add the app from there.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="显示应用程序内应用的Teams":::

## <a name="see-also"></a><span data-ttu-id="e5509-247">另请参阅</span><span class="sxs-lookup"><span data-stu-id="e5509-247">See also</span></span>

* [<span data-ttu-id="e5509-248">教程概述</span><span class="sxs-lookup"><span data-stu-id="e5509-248">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="e5509-249">创建对话机器人应用</span><span class="sxs-lookup"><span data-stu-id="e5509-249">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="e5509-250">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="e5509-250">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="e5509-251">代码示例</span><span class="sxs-lookup"><span data-stu-id="e5509-251">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)
