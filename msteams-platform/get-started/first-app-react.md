---
title: 开始 - 使用回车功能生成第一个 Teams 应用
author: adrianhall
description: 快速创建显示"Hello，World！"的 Microsoft Teams 应用。 使用 Microsoft Teams 工具包并响应的消息。
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: c257bcd805a6b7b38ab657cb31cad961df1c4704
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254319"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-react"></a><span data-ttu-id="b6d65-104">使用 React 构建和运行第一个 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="b6d65-104">Build and run your first Microsoft Teams app with React</span></span>

<span data-ttu-id="b6d65-105">本教程介绍如何在 React 中创建新的 Microsoft Teams 应用，该应用实现简单的个人应用，以从 Microsoft Graph。</span><span class="sxs-lookup"><span data-stu-id="b6d65-105">In this tutorial, you will learn how to create a new Microsoft Teams app in React that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="b6d65-106">例如，个人 *应用包括* 一组供个人使用的选项卡。</span><span class="sxs-lookup"><span data-stu-id="b6d65-106">For example, a *personal app* includes a set of tabs for individual use.</span></span> <span data-ttu-id="b6d65-107">在本教程中，你将了解 Teams 应用的结构、如何在本地运行应用以及如何将应用部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="b6d65-107">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="b6d65-108">构建的应用将显示当前用户的基本用户信息。</span><span class="sxs-lookup"><span data-stu-id="b6d65-108">The app that is built displays basic user information for the current user.</span></span> <span data-ttu-id="b6d65-109">授予权限后，应用会作为当前用户连接到 Microsoft Graph 以获取完整配置文件。</span><span class="sxs-lookup"><span data-stu-id="b6d65-109">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="b6d65-110">准备工作</span><span class="sxs-lookup"><span data-stu-id="b6d65-110">Before you begin</span></span>

<span data-ttu-id="b6d65-111">请确保通过安装必备组件来设置开发环境。</span><span class="sxs-lookup"><span data-stu-id="b6d65-111">Make sure your development environment is set up by installing the prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b6d65-112">安装先决条件</span><span class="sxs-lookup"><span data-stu-id="b6d65-112">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="b6d65-113">创建项目</span><span class="sxs-lookup"><span data-stu-id="b6d65-113">Create your project</span></span>

<span data-ttu-id="b6d65-114">使用 Teams 工具包创建你的第一个项目:</span><span class="sxs-lookup"><span data-stu-id="b6d65-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="b6d65-115">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="b6d65-115">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="b6d65-116">打开 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="b6d65-116">Open Visual Studio code.</span></span>
1. <span data-ttu-id="b6d65-117">打开Teams Toolkit，然后选择边Teams图标：</span><span class="sxs-lookup"><span data-stu-id="b6d65-117">Open the Teams Toolkit and select the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code 边栏中的 Teams 图标。":::

1. <span data-ttu-id="b6d65-119">选择 **创建新项目**。</span><span class="sxs-lookup"><span data-stu-id="b6d65-119">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. <span data-ttu-id="b6d65-121">选择 **创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="b6d65-121">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="&quot;创建新项目&quot;的向导启动":::

1. <span data-ttu-id="b6d65-123">在 **"选择功能"** 部分，验证 **选择"选项卡**"并选择"确定 **"。**</span><span class="sxs-lookup"><span data-stu-id="b6d65-123">In the **Select capabilities** section, varify that **Tab** is selected and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="显示如何向新应用添加功能的屏幕截图。":::

1. <span data-ttu-id="b6d65-125">在"**前端托管类型"部分，** 选择 **"Azure"。**</span><span class="sxs-lookup"><span data-stu-id="b6d65-125">In the **Frontend hosting type** section, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="显示如何选择新应用的托管的屏幕截图。":::

1. <span data-ttu-id="b6d65-127">在"**云资源"** 部分，选择"确定 **"。**</span><span class="sxs-lookup"><span data-stu-id="b6d65-127">In the **Cloud resources** section, select **OK**.</span></span>  <span data-ttu-id="b6d65-128">本教程不需要其他云资源。</span><span class="sxs-lookup"><span data-stu-id="b6d65-128">We do not need additional cloud resources for this tutorial.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="显示如何为新应用添加云资源的屏幕截图。":::

1. <span data-ttu-id="b6d65-130">在"**编程语言"部分**，选择 **"JavaScript"。**</span><span class="sxs-lookup"><span data-stu-id="b6d65-130">In the **Programming Language** section, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="显示如何选择编程语言的屏幕截图。":::

1. <span data-ttu-id="b6d65-132">选择工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="b6d65-132">Select a workspace folder.</span></span> <span data-ttu-id="b6d65-133">在工作区文件夹中为要创建的项目创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="b6d65-133">A folder is created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="b6d65-134">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="b6d65-134">Enter a suitable name for your app, like `helloworld`.</span></span> <span data-ttu-id="b6d65-135">应用的名称只能包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="b6d65-135">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="b6d65-136">按 **Enter** 以继续。</span><span class="sxs-lookup"><span data-stu-id="b6d65-136">Press **Enter** to continue.</span></span>

   <span data-ttu-id="b6d65-137">你的应用Teams数秒钟内创建。</span><span class="sxs-lookup"><span data-stu-id="b6d65-137">Your Teams app is created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="b6d65-138">命令行</span><span class="sxs-lookup"><span data-stu-id="b6d65-138">Command line</span></span>](#tab/cli)

<span data-ttu-id="b6d65-139">使用 `teamsfx` CLI 创建你的第一个项目。</span><span class="sxs-lookup"><span data-stu-id="b6d65-139">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="b6d65-140">从要创建项目文件夹的文件夹开始。</span><span class="sxs-lookup"><span data-stu-id="b6d65-140">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="b6d65-141">CLI 会提出一些问题来引导创建项目。</span><span class="sxs-lookup"><span data-stu-id="b6d65-141">The CLI walks through some questions to create the project.</span></span> <span data-ttu-id="b6d65-142">每个问题将告诉你如何回答它，例如，使用箭头键来选择一个选项。</span><span class="sxs-lookup"><span data-stu-id="b6d65-142">Each question will tell you how to answer it, for example, use arrow keys to select an option.</span></span> <span data-ttu-id="b6d65-143">如果已回答问题，请通过按 **Enter** 确认。</span><span class="sxs-lookup"><span data-stu-id="b6d65-143">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="b6d65-144">选择 **创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="b6d65-144">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="b6d65-145">选择 **Tab** 功能。</span><span class="sxs-lookup"><span data-stu-id="b6d65-145">Select the **Tab** capability.</span></span>
1. <span data-ttu-id="b6d65-146">选择 **Azure** 前端托管。</span><span class="sxs-lookup"><span data-stu-id="b6d65-146">Select **Azure** frontend hosting.</span></span> <span data-ttu-id="b6d65-147">请勿选择任何云资源。</span><span class="sxs-lookup"><span data-stu-id="b6d65-147">Do not select any cloud resources.</span></span>
1. <span data-ttu-id="b6d65-148">选择 **JavaScript** 作为编程语言。</span><span class="sxs-lookup"><span data-stu-id="b6d65-148">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="b6d65-149">按 **Enter** 选择默认工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="b6d65-149">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="b6d65-150">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="b6d65-150">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="b6d65-151">应用的名称只能包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="b6d65-151">The name of the app must consist only of alphanumeric characters.</span></span>

   <span data-ttu-id="b6d65-152">在回答所有问题后，将创建项目。</span><span class="sxs-lookup"><span data-stu-id="b6d65-152">After all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="b6d65-153">浏览源代码</span><span class="sxs-lookup"><span data-stu-id="b6d65-153">Take a tour of the source code</span></span>

<span data-ttu-id="b6d65-154">若要暂时跳过此部分，可以 [在本地运行应用](#run-your-app-locally)。</span><span class="sxs-lookup"><span data-stu-id="b6d65-154">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="b6d65-155">在Teams Toolkit项目后，你拥有组件来构建基本个人应用Teams。</span><span class="sxs-lookup"><span data-stu-id="b6d65-155">After the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="b6d65-156">项目目录和文件显示在 Visual Studio 代码的资源管理器区域中。</span><span class="sxs-lookup"><span data-stu-id="b6d65-156">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-app-project.png" alt-text="显示 Visual Studio Code 中个人应用的应用项目文件的屏幕截图。":::

<span data-ttu-id="b6d65-158">工具包根据你在设置过程中添加的功能，自动在项目目录中创建标点文件夹。</span><span class="sxs-lookup"><span data-stu-id="b6d65-158">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="b6d65-159">Teams 工具包将保持其对于新目录中 `.fx` 的状态。</span><span class="sxs-lookup"><span data-stu-id="b6d65-159">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="b6d65-160">此目录中的其他项：</span><span class="sxs-lookup"><span data-stu-id="b6d65-160">Among other items in this directory:</span></span>

- <span data-ttu-id="b6d65-161">应用图标在 `color.png` 和 `outline.png`中存储为 PNG 文件。</span><span class="sxs-lookup"><span data-stu-id="b6d65-161">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="b6d65-162">发布到 Developer Portal for Teams 的应用清单存储在 `manifest.source.json`。</span><span class="sxs-lookup"><span data-stu-id="b6d65-162">The app manifest for publishing to the Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="b6d65-163">创建项目时选择的设置存储在 `settings.json`。</span><span class="sxs-lookup"><span data-stu-id="b6d65-163">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="b6d65-164">由于在设置过程中选择了选项卡功能，因此 Teams 工具包会为网站目录中的基本选项卡 `tabs` 代码。</span><span class="sxs-lookup"><span data-stu-id="b6d65-164">Since you selected the tab capability during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab in the `tabs` directory.</span></span> <span data-ttu-id="b6d65-165">此目录中有几个重要文件：</span><span class="sxs-lookup"><span data-stu-id="b6d65-165">Within this directory there are several important files:</span></span>

- <span data-ttu-id="b6d65-166">`tabs/src/index.jsx` 是前端应用的入口点，其中主应用程序组件 `App` 呈现为 `ReactDOM.render()`。</span><span class="sxs-lookup"><span data-stu-id="b6d65-166">`tabs/src/index.jsx` is the front-end app's entry point, where the main `App` component is rendered with `ReactDOM.render()`.</span></span>
- <span data-ttu-id="b6d65-167">`tabs/src/components/App.jsx` 处理应用中的 URL 路由。</span><span class="sxs-lookup"><span data-stu-id="b6d65-167">`tabs/src/components/App.jsx` handles URL routing in your app.</span></span> <span data-ttu-id="b6d65-168">它调用了 [JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md) 应用和团队之间建立通信。</span><span class="sxs-lookup"><span data-stu-id="b6d65-168">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>
- <span data-ttu-id="b6d65-169">`tabs/src/components/Tab.jsx` 包含用于实现应用 UI 的代码。</span><span class="sxs-lookup"><span data-stu-id="b6d65-169">`tabs/src/components/Tab.jsx` contains the code to implement the UI of your app.</span></span>
- <span data-ttu-id="b6d65-170">`tabs/src/components/TabConfig.jsx` 包含用于实施配置应用的 UI 的代码。</span><span class="sxs-lookup"><span data-stu-id="b6d65-170">`tabs/src/components/TabConfig.jsx` contains the code to implement the UI that configures your app.</span></span>

<span data-ttu-id="b6d65-171">Teams 运行时需要几个选项卡，包括隐私声明、使用条款和配置选项卡。</span><span class="sxs-lookup"><span data-stu-id="b6d65-171">Several tabs are required by the Teams runtime, including the privacy notice, terms of use, and configuration tabs.</span></span>  <span data-ttu-id="b6d65-172">隐私声明和使用条款的代码位于同一目录中。</span><span class="sxs-lookup"><span data-stu-id="b6d65-172">The code for the privacy notice and terms of use are located in the same directory.</span></span>

<span data-ttu-id="b6d65-173">添加云功能时，会向项目添加其他目录。</span><span class="sxs-lookup"><span data-stu-id="b6d65-173">When you add cloud functionality, additional directories are added to the project.</span></span>  <span data-ttu-id="b6d65-174">最为明显的是， `api` 目录将代码存储到所编写的任何 Azure 函数中。</span><span class="sxs-lookup"><span data-stu-id="b6d65-174">Most notably, the `api` directory holds the code to any Azure Functions you write.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="b6d65-175">在本地运行应用</span><span class="sxs-lookup"><span data-stu-id="b6d65-175">Run your app locally</span></span>

<span data-ttu-id="b6d65-176">使用 Teams 工具包，你可以在本地运行应用。</span><span class="sxs-lookup"><span data-stu-id="b6d65-176">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="b6d65-177">这包含几个部分，是提供 Teams 所需的正确基础结构所必需的：</span><span class="sxs-lookup"><span data-stu-id="b6d65-177">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="b6d65-178">应用程序已注册 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="b6d65-178">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="b6d65-179">此应用程序具有与从加载应用的位置及其访问的任何后端资源相关联的权限。</span><span class="sxs-lookup"><span data-stu-id="b6d65-179">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="b6d65-180">托管 Web API 以辅助身份验证任务，作为应用和 Azure Active Directory 之间的代理。</span><span class="sxs-lookup"><span data-stu-id="b6d65-180">A web API is hosted to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  <span data-ttu-id="b6d65-181">这由 Azure 函数核心工具运行。</span><span class="sxs-lookup"><span data-stu-id="b6d65-181">This is run by Azure Functions Core Tools.</span></span>  <span data-ttu-id="b6d65-182">可以在 URL 位置访问 `https://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="b6d65-182">It can be accessed at the URL `https://localhost:5000`.</span></span>
- <span data-ttu-id="b6d65-183">位于应用程序前端的 HTML、CSS 和 JavaScript 资源托管在本地服务中。</span><span class="sxs-lookup"><span data-stu-id="b6d65-183">The HTML, CSS, and JavaScript resources that make up the front end of the app are hosted on a local service.</span></span> <span data-ttu-id="b6d65-184">可通过访问文件 `https://localhost:3000`。</span><span class="sxs-lookup"><span data-stu-id="b6d65-184">It can be accessed at `https://localhost:3000`.</span></span>
- <span data-ttu-id="b6d65-185">生成应用清单，存在于 Teams 开发人员门户中。</span><span class="sxs-lookup"><span data-stu-id="b6d65-185">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="b6d65-186">Teams 使用应用清单告诉已连接客户端从何处加载应用。</span><span class="sxs-lookup"><span data-stu-id="b6d65-186">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="b6d65-187">完成此操作后，应用可以在客户端Teams加载。</span><span class="sxs-lookup"><span data-stu-id="b6d65-187">After this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="b6d65-188">我们使用 Teams Web 客户端，以便可以在标准 Web 开发环境中查看 HTML、CSS 和 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="b6d65-188">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="b6d65-189">在 Visual Studio Code 本地生成和运行应用</span><span class="sxs-lookup"><span data-stu-id="b6d65-189">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="b6d65-190">若要在本地构建和运行应用，请执行：</span><span class="sxs-lookup"><span data-stu-id="b6d65-190">To build and run your app locally:</span></span>

1. <span data-ttu-id="b6d65-191">在 Visual Studio Code 中，按 **F5** 以在调试模式下运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="b6d65-191">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="b6d65-192">首次运行该应用时，将下载所有依赖项并编译该应用。</span><span class="sxs-lookup"><span data-stu-id="b6d65-192">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="b6d65-193">编译完成后，将自动打开浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="b6d65-193">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="b6d65-194">这可能需要 3-5 分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="b6d65-194">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="b6d65-195">如果需要Toolkit，系统会提示您安装本地证书。</span><span class="sxs-lookup"><span data-stu-id="b6d65-195">The Toolkit prompts you to install a local certificate if required.</span></span> <span data-ttu-id="b6d65-196">此证书允许 Teams 从 `https://localhost`。</span><span class="sxs-lookup"><span data-stu-id="b6d65-196">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="b6d65-197">出现下列对话框时，选择"是"：</span><span class="sxs-lookup"><span data-stu-id="b6d65-197">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="显示如何安装 SSL 证书以便 Teams 从 localhost 加载应用程序提示的屏幕截图。":::

1. <span data-ttu-id="b6d65-199">Web 浏览器开始运行该应用。</span><span class="sxs-lookup"><span data-stu-id="b6d65-199">Your web browser starts to run the app.</span></span> <span data-ttu-id="b6d65-200">如果系统提示打开Teams，请选择 **"取消**"以保留在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="b6d65-200">If prompted to open Teams desktop, select **Cancel** to remain in the browser.</span></span> <span data-ttu-id="b6d65-201">系统有时还可能会提示你切换到Teams桌面;选择Teams Web 应用。</span><span class="sxs-lookup"><span data-stu-id="b6d65-201">You may also be prompted to switch to Teams desktop at other times; select the Teams web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="显示启动后如何选择 Teams 的 Web 版本的屏幕截图":::

1. <span data-ttu-id="b6d65-203">系统提示时，使用 M365 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="b6d65-203">Sign in with your M365 account when prompted.</span></span>
1. <span data-ttu-id="b6d65-204">系统提示将应用安装到 Teams 时，按 **添加**。</span><span class="sxs-lookup"><span data-stu-id="b6d65-204">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="b6d65-205">现在将显示你的应用：</span><span class="sxs-lookup"><span data-stu-id="b6d65-205">Your app is now displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-finished-app.png" alt-text="已完成应用的屏幕截图":::

<span data-ttu-id="b6d65-207">你可以像执行任何其他 Web 应用程序一样执行正常的调试活动，例如设置断点。</span><span class="sxs-lookup"><span data-stu-id="b6d65-207">You can do normal debugging activities as if this were any other web application, such as setting breakpoints.</span></span> <span data-ttu-id="b6d65-208">该应用支持热重新加载。</span><span class="sxs-lookup"><span data-stu-id="b6d65-208">The app supports hot reloading.</span></span> <span data-ttu-id="b6d65-209">如果更改了项目内的任何文件，将重新加载页面。</span><span class="sxs-lookup"><span data-stu-id="b6d65-209">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="b6d65-210">在调试器中本地运行应用时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="b6d65-210">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="b6d65-211">按 **F5 键** 时，Teams Toolkit：</span><span class="sxs-lookup"><span data-stu-id="b6d65-211">When you press the **F5** key, the Teams Toolkit:</span></span>

* <span data-ttu-id="b6d65-212">向应用程序注册Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="b6d65-212">Registers your application with Azure Active Directory.</span></span>
* <span data-ttu-id="b6d65-213">*在应用中* 旁加载Teams。</span><span class="sxs-lookup"><span data-stu-id="b6d65-213">*Sideloads* your app in Teams.</span></span>
* <span data-ttu-id="b6d65-214">使用 Azure 函数核心工具 启动本地 [运行的应用程序后端](/azure/azure-functions/functions-run-local?#start)。</span><span class="sxs-lookup"><span data-stu-id="b6d65-214">Starts your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
* <span data-ttu-id="b6d65-215">在本地托管应用程序前端启动。</span><span class="sxs-lookup"><span data-stu-id="b6d65-215">Starts your application front-end hosted locally.</span></span>
* <span data-ttu-id="b6d65-216">使用Microsoft Teams命令在 Web 浏览器中启动 Teams，以从 旁加载应用程序 `https://localhost:3000/tab` 。</span><span class="sxs-lookup"><span data-stu-id="b6d65-216">Starts Microsoft Teams in a web browser with a command to instruct Teams to side load the application from `https://localhost:3000/tab`.</span></span> <span data-ttu-id="b6d65-217">这是在应用程序清单中注册的 URL。</span><span class="sxs-lookup"><span data-stu-id="b6d65-217">This is the URL registered in the application manifest.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="b6d65-218">了解如何在本地运行应用时解决常见问题。</span><span class="sxs-lookup"><span data-stu-id="b6d65-218">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="b6d65-219">若要在 Teams 中成功运行应用，必须具有允许应用旁加载的 Teams 帐户。</span><span class="sxs-lookup"><span data-stu-id="b6d65-219">To successfully run your app in Teams, you must have a Teams account that allows app sideloading.</span></span> <span data-ttu-id="b6d65-220">有关打开帐户详细信息，请参阅 [先决条件](prerequisites.md#enable-sideloading)。</span><span class="sxs-lookup"><span data-stu-id="b6d65-220">For more information on account opening, see [prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="b6d65-221">了解将应用部署到 Azure 时会发生的情况</span><span class="sxs-lookup"><span data-stu-id="b6d65-221">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="b6d65-222">部署之前，应用程序已在本地运行:</span><span class="sxs-lookup"><span data-stu-id="b6d65-222">Before deployment, the application has been running locally:</span></span>

* <span data-ttu-id="b6d65-223">后端使用 **Azure Functions Core Tools** 运行。</span><span class="sxs-lookup"><span data-stu-id="b6d65-223">The backend runs using **Azure Functions Core Tools**.</span></span>
* <span data-ttu-id="b6d65-224">应用程序 HTTP 终结点 (Microsoft Teams 在此加载应用程序) 在本地运行。</span><span class="sxs-lookup"><span data-stu-id="b6d65-224">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="b6d65-225">部署涉及在活动的 Azure 订阅上预配资源，以及将应用程序的后端和前端代码部署或上载到 Azure。</span><span class="sxs-lookup"><span data-stu-id="b6d65-225">Deployment involves provisioning resources on an active Azure subscription and deploying or uploading the backend and frontend code for the application to Azure.</span></span>

* <span data-ttu-id="b6d65-226">后端（如果已配置）使用各种 Azure 服务，包括 Azure 应用服务和 Azure 存储。</span><span class="sxs-lookup"><span data-stu-id="b6d65-226">The backend if configured uses a variety of Azure services, including Azure App Service and Azure Storage.</span></span>
* <span data-ttu-id="b6d65-227">将前端应用程序部署到配置用于静态 Web 托管的 Azure 存储帐户。</span><span class="sxs-lookup"><span data-stu-id="b6d65-227">The frontend application will be deployed to an Azure Storage account configured for static web hosting.</span></span>

</details>

## <a name="see-also"></a><span data-ttu-id="b6d65-228">另请参阅</span><span class="sxs-lookup"><span data-stu-id="b6d65-228">See also</span></span>

* [<span data-ttu-id="b6d65-229">教程概述</span><span class="sxs-lookup"><span data-stu-id="b6d65-229">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="b6d65-230">创建对话机器人应用</span><span class="sxs-lookup"><span data-stu-id="b6d65-230">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="b6d65-231">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="b6d65-231">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="b6d65-232">代码示例</span><span class="sxs-lookup"><span data-stu-id="b6d65-232">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)
