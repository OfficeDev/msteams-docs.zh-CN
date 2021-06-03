---
title: 开始 - 使用回车功能生成第一个 Teams 应用
author: adrianhall
description: 快速创建显示"Hello，World！"的 Microsoft Teams 应用。 使用 Microsoft Teams 工具包并响应的消息。
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: 8c6a957dc01cfaac0f8463166a6647d6b18babed
ms.sourcegitcommit: 33a43c61f27ae750776616b2cf90159455d8ba6c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2021
ms.locfileid: "52721834"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-react"></a><span data-ttu-id="c4e07-104">使用 React 构建和运行第一个 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="c4e07-104">Build and run your first Microsoft Teams app with React</span></span>

<span data-ttu-id="c4e07-105">在本教程中，将在回车应用中创建新的 Microsoft Teams 应用，该应用实施简单的个人应用，从 Microsoft Graph 提取信息。</span><span class="sxs-lookup"><span data-stu-id="c4e07-105">In this tutorial, you will create a new Microsoft Teams app in React that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="c4e07-106">（ *个人应用* 包括一组适用于个人使用的选项卡。）在本教程中，你将了解 Teams 应用的结构、在本地运行应用以及如何将应用部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="c4e07-106">(A *personal app* includes a set of tabs scoped for individual use.) During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="c4e07-107">构建的应用将显示当前用户的基本用户信息。</span><span class="sxs-lookup"><span data-stu-id="c4e07-107">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="c4e07-108">授予权限后，应用会作为当前用户连接到 Microsoft Graph 以获取完整配置文件。</span><span class="sxs-lookup"><span data-stu-id="c4e07-108">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="c4e07-109">准备工作</span><span class="sxs-lookup"><span data-stu-id="c4e07-109">Before you begin</span></span>

<span data-ttu-id="c4e07-110">通过安装[先决条件](prerequisites.md)确保您的开发环境已设置</span><span class="sxs-lookup"><span data-stu-id="c4e07-110">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c4e07-111">安装先决条件</span><span class="sxs-lookup"><span data-stu-id="c4e07-111">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="c4e07-112">创建项目</span><span class="sxs-lookup"><span data-stu-id="c4e07-112">Create your project</span></span>

<span data-ttu-id="c4e07-113">使用 Teams 工具包创建你的第一个项目:</span><span class="sxs-lookup"><span data-stu-id="c4e07-113">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="c4e07-114">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c4e07-114">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="c4e07-115">打开 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="c4e07-115">Open Visual Studio code.</span></span>
1. <span data-ttu-id="c4e07-116">通过选择边栏中的 Teams 图标，打开 Teams 工具包:</span><span class="sxs-lookup"><span data-stu-id="c4e07-116">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code 边栏中的 Teams 图标。":::

1. <span data-ttu-id="c4e07-118">选择 **创建新项目**。</span><span class="sxs-lookup"><span data-stu-id="c4e07-118">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. <span data-ttu-id="c4e07-120">选择 **创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="c4e07-120">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="&quot;创建新项目&quot;的向导启动":::

1. <span data-ttu-id="c4e07-122">在 **选择功能** 步骤中， **选项卡** 功能已被选中。</span><span class="sxs-lookup"><span data-stu-id="c4e07-122">On the **Select capabilities** step, the **Tab** capability will already be selected.</span></span>  <span data-ttu-id="c4e07-123">按 **确定**。</span><span class="sxs-lookup"><span data-stu-id="c4e07-123">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="显示如何向新应用添加功能的屏幕截图。":::

1. <span data-ttu-id="c4e07-125">在 **前端托管类型** 步骤中， 选择 **Azure**。</span><span class="sxs-lookup"><span data-stu-id="c4e07-125">On the **Frontend hosting type** step, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="显示如何选择新应用的托管的屏幕截图。":::

1. <span data-ttu-id="c4e07-127">在 **云资源** 步骤中， 选择 **确定**。</span><span class="sxs-lookup"><span data-stu-id="c4e07-127">On the **Cloud resources** step, press **OK**.</span></span>  <span data-ttu-id="c4e07-128">本教程不需要其他云资源。</span><span class="sxs-lookup"><span data-stu-id="c4e07-128">We do not need additional cloud resources for this tutorial.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="显示如何为新应用添加云资源的屏幕截图。":::

1. <span data-ttu-id="c4e07-130">在" **编程语言** 步骤中， 选择 **JavaScript**。</span><span class="sxs-lookup"><span data-stu-id="c4e07-130">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="显示如何选择编程语言的屏幕截图。":::

1. <span data-ttu-id="c4e07-132">选择工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="c4e07-132">Select a workspace folder.</span></span>  <span data-ttu-id="c4e07-133">将在工作区文件夹中为正在创建的项目创建一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="c4e07-133">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="c4e07-134">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="c4e07-134">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="c4e07-135">应用的名称只能包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="c4e07-135">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="c4e07-136">按 **Enter** 以继续。</span><span class="sxs-lookup"><span data-stu-id="c4e07-136">Press **Enter** to continue.</span></span>

<span data-ttu-id="c4e07-137">将在数秒钟内创建你的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="c4e07-137">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="c4e07-138">命令行</span><span class="sxs-lookup"><span data-stu-id="c4e07-138">Command line</span></span>](#tab/cli)

<span data-ttu-id="c4e07-139">使用 `teamsfx` CLI 创建你的第一个项目。</span><span class="sxs-lookup"><span data-stu-id="c4e07-139">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="c4e07-140">从要创建项目文件夹的文件夹开始。</span><span class="sxs-lookup"><span data-stu-id="c4e07-140">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="c4e07-141">CLI 会提出一些问题来引导创建项目。</span><span class="sxs-lookup"><span data-stu-id="c4e07-141">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="c4e07-142">每个问题将告诉你该如何回答（例如，使用箭头键选择一个选项）。</span><span class="sxs-lookup"><span data-stu-id="c4e07-142">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="c4e07-143">如果已回答问题，请通过按 **Enter** 确认。</span><span class="sxs-lookup"><span data-stu-id="c4e07-143">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="c4e07-144">选择 **"创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="c4e07-144">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="c4e07-145">选择" **选项卡** 功能。</span><span class="sxs-lookup"><span data-stu-id="c4e07-145">Choose the **Tab** capability.</span></span>
1. <span data-ttu-id="c4e07-146">选择 **Azure** 前端托管。</span><span class="sxs-lookup"><span data-stu-id="c4e07-146">Select **Azure** frontend hosting.</span></span>
1. <span data-ttu-id="c4e07-147">请勿选择任何云资源。</span><span class="sxs-lookup"><span data-stu-id="c4e07-147">Do not select any cloud resources.</span></span>
1. <span data-ttu-id="c4e07-148">选择 **JavaScript** 作为编程语言。</span><span class="sxs-lookup"><span data-stu-id="c4e07-148">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="c4e07-149">按 **Enter** 选择默认工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="c4e07-149">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="c4e07-150">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="c4e07-150">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="c4e07-151">应用的名称只能包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="c4e07-151">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="c4e07-152">回答所有问题后，将创建项目。</span><span class="sxs-lookup"><span data-stu-id="c4e07-152">Once all the questions have been answered, your project will be created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="c4e07-153">浏览源代码</span><span class="sxs-lookup"><span data-stu-id="c4e07-153">Take a tour of the source code</span></span>

<span data-ttu-id="c4e07-154">若要暂时跳过此部分， 你可以[运行本地应用](#run-your-app-locally)。</span><span class="sxs-lookup"><span data-stu-id="c4e07-154">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="c4e07-155">在 Teams 工具包配置你的项目后，你只需这些组件就可以使用这些组件为 Teams 构建基本的个人应用。</span><span class="sxs-lookup"><span data-stu-id="c4e07-155">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="c4e07-156">项目目录和文件显示在 Visual Studio 代码的资源管理器区域中。</span><span class="sxs-lookup"><span data-stu-id="c4e07-156">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-app-project.png" alt-text="显示 Visual Studio Code 中个人应用的应用项目文件的屏幕截图。":::

<span data-ttu-id="c4e07-158">工具包根据你在设置过程中添加的功能，自动在项目目录中创建标点文件夹。</span><span class="sxs-lookup"><span data-stu-id="c4e07-158">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="c4e07-159">Teams 工具包将保持其对于新目录中 `.fx` 的状态。</span><span class="sxs-lookup"><span data-stu-id="c4e07-159">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="c4e07-160">此目录中的其他项：</span><span class="sxs-lookup"><span data-stu-id="c4e07-160">Among other items in this directory:</span></span>

- <span data-ttu-id="c4e07-161">应用图标在 `color.png` 和 `outline.png`中存储为 PNG 文件。</span><span class="sxs-lookup"><span data-stu-id="c4e07-161">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="c4e07-162">发布到 Developer Portal for Teams 的应用清单存储在 `manifest.source.json`。</span><span class="sxs-lookup"><span data-stu-id="c4e07-162">The app manifest for publishing to the Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="c4e07-163">创建项目时选择的设置存储在 `settings.json`。</span><span class="sxs-lookup"><span data-stu-id="c4e07-163">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="c4e07-164">由于在设置过程中选择了选项卡功能，因此 Teams 工具包会为网站目录中的基本选项卡 `tabs` 代码。</span><span class="sxs-lookup"><span data-stu-id="c4e07-164">Since you selected the tab capability during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab in the `tabs` directory.</span></span> <span data-ttu-id="c4e07-165">此目录中有几个重要文件：</span><span class="sxs-lookup"><span data-stu-id="c4e07-165">Within this directory there are several important files:</span></span>

- <span data-ttu-id="c4e07-166">`tabs/src/index.jsx` 是前端应用的入口点，其中主应用程序组件 `App` 呈现为 `ReactDOM.render()`。</span><span class="sxs-lookup"><span data-stu-id="c4e07-166">`tabs/src/index.jsx` is the front-end app's entry point, where the main `App` component is rendered with `ReactDOM.render()`.</span></span>
- <span data-ttu-id="c4e07-167">`tabs/src/components/App.jsx` 处理应用中的 URL 路由。</span><span class="sxs-lookup"><span data-stu-id="c4e07-167">`tabs/src/components/App.jsx` handles URL routing in your app.</span></span> <span data-ttu-id="c4e07-168">它调用了 [JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md) 应用和团队之间建立通信。</span><span class="sxs-lookup"><span data-stu-id="c4e07-168">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>
- <span data-ttu-id="c4e07-169">`tabs/src/components/Tab.jsx` 包含用于实现应用 UI 的代码。</span><span class="sxs-lookup"><span data-stu-id="c4e07-169">`tabs/src/components/Tab.jsx` contains the code to implement the UI of your app.</span></span>
- <span data-ttu-id="c4e07-170">`tabs/src/components/TabConfig.jsx` 包含用于实施配置应用的 UI 的代码。</span><span class="sxs-lookup"><span data-stu-id="c4e07-170">`tabs/src/components/TabConfig.jsx` contains the code to implement the UI that configures your app.</span></span>

<span data-ttu-id="c4e07-171">Teams 运行时需要几个选项卡，包括隐私声明、使用条款和配置选项卡。</span><span class="sxs-lookup"><span data-stu-id="c4e07-171">Several tabs are required by the Teams runtime, including the privacy notice, terms of use, and configuration tabs.</span></span>  <span data-ttu-id="c4e07-172">隐私声明和使用条款的代码位于同一目录中。</span><span class="sxs-lookup"><span data-stu-id="c4e07-172">The code for the privacy notice and terms of use are located in the same directory.</span></span>

<span data-ttu-id="c4e07-173">添加云功能时，会向项目添加其他目录。</span><span class="sxs-lookup"><span data-stu-id="c4e07-173">When you add cloud functionality, additional directories are added to the project.</span></span>  <span data-ttu-id="c4e07-174">最为明显的是， `api` 目录将代码存储到所编写的任何 Azure 函数中。</span><span class="sxs-lookup"><span data-stu-id="c4e07-174">Most notably, the `api` directory holds the code to any Azure Functions you write.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="c4e07-175">在本地运行应用</span><span class="sxs-lookup"><span data-stu-id="c4e07-175">Run your app locally</span></span>

<span data-ttu-id="c4e07-176">使用 Teams 工具包，你可以在本地运行应用。</span><span class="sxs-lookup"><span data-stu-id="c4e07-176">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="c4e07-177">这包含几个部分，是提供 Teams 所需的正确基础结构所必需的：</span><span class="sxs-lookup"><span data-stu-id="c4e07-177">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="c4e07-178">应用程序已注册 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="c4e07-178">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="c4e07-179">此应用程序具有与从加载应用的位置及其访问的任何后端资源相关联的权限。</span><span class="sxs-lookup"><span data-stu-id="c4e07-179">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="c4e07-180">托管 Web API 以辅助身份验证任务，作为应用和 Azure Active Directory 之间的代理。</span><span class="sxs-lookup"><span data-stu-id="c4e07-180">A web API is hosted to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  <span data-ttu-id="c4e07-181">这由 Azure 函数核心工具运行。</span><span class="sxs-lookup"><span data-stu-id="c4e07-181">This is run by Azure Functions Core Tools.</span></span>  <span data-ttu-id="c4e07-182">可以在 URL 位置访问 `https://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="c4e07-182">It can be accessed at the URL `https://localhost:5000`.</span></span>
- <span data-ttu-id="c4e07-183">位于应用程序前端的 HTML、CSS 和 JavaScript 资源托管在本地服务中。</span><span class="sxs-lookup"><span data-stu-id="c4e07-183">The HTML, CSS, and JavaScript resources that make up the front end of the app are hosted on a local service.</span></span> <span data-ttu-id="c4e07-184">可通过访问文件 `https://localhost:3000`。</span><span class="sxs-lookup"><span data-stu-id="c4e07-184">It can be accessed at `https://localhost:3000`.</span></span>
- <span data-ttu-id="c4e07-185">生成应用清单，存在于 Teams 开发人员门户中。</span><span class="sxs-lookup"><span data-stu-id="c4e07-185">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="c4e07-186">Teams 使用应用清单告诉已连接客户端从何处加载应用。</span><span class="sxs-lookup"><span data-stu-id="c4e07-186">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="c4e07-187">完成后，可在 Teams 客户端中加载该应用。</span><span class="sxs-lookup"><span data-stu-id="c4e07-187">Once this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="c4e07-188">我们使用 Teams Web 客户端，以便可以在标准 Web 开发环境中查看 HTML、CSS 和 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="c4e07-188">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="c4e07-189">在 Visual Studio Code 本地生成和运行应用</span><span class="sxs-lookup"><span data-stu-id="c4e07-189">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="c4e07-190">若要在本地构建和运行应用，请执行：</span><span class="sxs-lookup"><span data-stu-id="c4e07-190">To build and run your app locally:</span></span>

1. <span data-ttu-id="c4e07-191">在 Visual Studio Code 中，按 **F5** 以在调试模式下运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="c4e07-191">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="c4e07-192">首次运行该应用时，将下载所有依赖项并编译该应用。</span><span class="sxs-lookup"><span data-stu-id="c4e07-192">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="c4e07-193">编译完成后，将自动打开浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="c4e07-193">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="c4e07-194">这可能需要 3-5 分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="c4e07-194">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="c4e07-195">如有必要，工具包会提示你安装本地证书。</span><span class="sxs-lookup"><span data-stu-id="c4e07-195">The Toolkit will prompt you to install a local certificate if needed.</span></span> <span data-ttu-id="c4e07-196">此证书允许 Teams 从 `https://localhost`。</span><span class="sxs-lookup"><span data-stu-id="c4e07-196">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="c4e07-197">出现下列对话框时，选择"是"：</span><span class="sxs-lookup"><span data-stu-id="c4e07-197">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="显示如何安装 SSL 证书以便 Teams 从 localhost 加载应用程序提示的屏幕截图。":::

1. <span data-ttu-id="c4e07-199">Web 浏览器开始运行该应用。</span><span class="sxs-lookup"><span data-stu-id="c4e07-199">Your web browser starts to run the app.</span></span> <span data-ttu-id="c4e07-200">如果系统提示打开Teams，请选择 **"取消**"以保留在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="c4e07-200">If prompted to open Teams desktop, select **Cancel** to remain in the browser.</span></span> <span data-ttu-id="c4e07-201">系统有时还可能会提示你切换到Teams桌面;选择Teams Web 应用。</span><span class="sxs-lookup"><span data-stu-id="c4e07-201">You may also be prompted to switch to Teams desktop at other times; select the Teams web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="显示启动后如何选择 Teams 的 Web 版本的屏幕截图":::

1. <span data-ttu-id="c4e07-203">系统可能会提示你登录。</span><span class="sxs-lookup"><span data-stu-id="c4e07-203">You may be prompted to sign in.</span></span>  <span data-ttu-id="c4e07-204">如果是这样，则使用你的 M365 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="c4e07-204">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="c4e07-205">系统提示将应用安装到 Teams 时，按 **添加**。</span><span class="sxs-lookup"><span data-stu-id="c4e07-205">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="c4e07-206">此时将显示应用：</span><span class="sxs-lookup"><span data-stu-id="c4e07-206">Your app will now be displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-finished-app.png" alt-text="已完成应用的屏幕截图":::

<span data-ttu-id="c4e07-208">你可以像调试任何其他 Web 应用程序一样执行正常调试活动（例如设置断点）。</span><span class="sxs-lookup"><span data-stu-id="c4e07-208">You can do normal debugging activities as if this were any other web application (such as setting breakpoints).</span></span> <span data-ttu-id="c4e07-209">该应用支持热重新加载。</span><span class="sxs-lookup"><span data-stu-id="c4e07-209">The app supports hot reloading.</span></span>  <span data-ttu-id="c4e07-210">如果更改了项目内的任何文件，将重新加载页面。</span><span class="sxs-lookup"><span data-stu-id="c4e07-210">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="c4e07-211">在调试器中本地运行应用时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="c4e07-211">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="c4e07-212">按 F5 时，Teams 工具包:</span><span class="sxs-lookup"><span data-stu-id="c4e07-212">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="c4e07-213">使用 Azure Active Directory 注册应用程序。</span><span class="sxs-lookup"><span data-stu-id="c4e07-213">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="c4e07-214">*已并行* Teams 中的应用。</span><span class="sxs-lookup"><span data-stu-id="c4e07-214">*Sideloaded* your app in Teams.</span></span>
1. <span data-ttu-id="c4e07-215">使用 Azure 函数核心工具中心 [本地运行的应用程序后端](/azure/azure-functions/functions-run-local?#start)。</span><span class="sxs-lookup"><span data-stu-id="c4e07-215">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="c4e07-216">启动应用程序本地托管的前端。</span><span class="sxs-lookup"><span data-stu-id="c4e07-216">Started your application front-end hosted locally.</span></span>
1. <span data-ttu-id="c4e07-217">在 Web 浏览器中启动 Microsoft Teams，命令命令 Teams 从 `https://localhost:3000/tab` （URL 在应用程序清单中注册） 并排加载应用程序。</span><span class="sxs-lookup"><span data-stu-id="c4e07-217">Started Microsoft Teams in a web browser with a command to instruct Teams to side load the application from `https://localhost:3000/tab` (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="c4e07-218">了解如何在本地运行应用时解决常见问题。</span><span class="sxs-lookup"><span data-stu-id="c4e07-218">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="c4e07-219">若要在 Teams 中成功运行应用，必须具有允许应用旁加载的 Teams 帐户。</span><span class="sxs-lookup"><span data-stu-id="c4e07-219">To successfully run your app in Teams, you must have a Teams account that allows app sideloading.</span></span> <span data-ttu-id="c4e07-220">有关打开帐户详细信息，请参阅 [先决条件](prerequisites.md#enable-sideloading)。</span><span class="sxs-lookup"><span data-stu-id="c4e07-220">For more information on account opening, see [prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="c4e07-221">了解将应用部署到 Azure 时会发生的情况</span><span class="sxs-lookup"><span data-stu-id="c4e07-221">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="c4e07-222">部署之前，应用程序已在本地运行:</span><span class="sxs-lookup"><span data-stu-id="c4e07-222">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="c4e07-223">后端使用 _Azure Functions Core Tools_ 运行。</span><span class="sxs-lookup"><span data-stu-id="c4e07-223">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="c4e07-224">应用程序 HTTP 终结点 (Microsoft Teams 在此加载应用程序) 在本地运行。</span><span class="sxs-lookup"><span data-stu-id="c4e07-224">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="c4e07-225">部署涉及预配活动 Azure 订阅上的资源，以及将应用程序后端和前端代码部署（上传）到 Azure。</span><span class="sxs-lookup"><span data-stu-id="c4e07-225">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span>

1. <span data-ttu-id="c4e07-226">后端（如果已配置）使用多种 Azure 服务，包括 Azure 应用服务和 Azure 存储。</span><span class="sxs-lookup"><span data-stu-id="c4e07-226">The backend (if configured) uses a variety of Azure services, including Azure App Service and Azure Storage.</span></span>
1. <span data-ttu-id="c4e07-227">将前端应用程序部署到配置用于静态 Web 托管的 Azure 存储帐户。</span><span class="sxs-lookup"><span data-stu-id="c4e07-227">The frontend application will be deployed to an Azure Storage account configured for static web hosting.</span></span>

</details>

## <a name="next-steps"></a><span data-ttu-id="c4e07-228">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c4e07-228">Next steps</span></span>

<span data-ttu-id="c4e07-229">了解创建 Teams 应用的其他方法：</span><span class="sxs-lookup"><span data-stu-id="c4e07-229">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="c4e07-230">使用 Blazor 创建 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="c4e07-230">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="c4e07-231">[创建 Teams 应用作为 SharePoint Web 部件](first-app-spfx.md) （不需要 Azure）</span><span class="sxs-lookup"><span data-stu-id="c4e07-231">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="c4e07-232">创建对话机器人应用</span><span class="sxs-lookup"><span data-stu-id="c4e07-232">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="c4e07-233">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="c4e07-233">Create a messaging extension</span></span>](first-message-extension.md)
