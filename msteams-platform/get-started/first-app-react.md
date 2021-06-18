---
title: 开始 - 使用回车功能生成第一个 Teams 应用
author: adrianhall
description: 快速创建显示"Hello，World！"的 Microsoft Teams 应用。 使用 Microsoft Teams 工具包并响应的消息。
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: edd7cf8048dd89156b4b91afecb329d91baf3f53
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994111"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-react"></a><span data-ttu-id="ad307-104">使用 React 构建和运行第一个 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="ad307-104">Build and run your first Microsoft Teams app with React</span></span>

<span data-ttu-id="ad307-105">在本教程中，将在回车应用中创建新的 Microsoft Teams 应用，该应用实施简单的个人应用，从 Microsoft Graph 提取信息。</span><span class="sxs-lookup"><span data-stu-id="ad307-105">In this tutorial, you will create a new Microsoft Teams app in React that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="ad307-106">例如，个人 *应用包括* 一组作用域为供个人使用的选项卡。</span><span class="sxs-lookup"><span data-stu-id="ad307-106">For example, a *personal app* includes a set of tabs scoped for individual use.</span></span> <span data-ttu-id="ad307-107">在本教程中，你将了解 Teams 应用的结构、如何在本地运行应用以及如何将应用部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="ad307-107">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="ad307-108">构建的应用将显示当前用户的基本用户信息。</span><span class="sxs-lookup"><span data-stu-id="ad307-108">The app that is built displays basic user information for the current user.</span></span> <span data-ttu-id="ad307-109">授予权限后，应用会作为当前用户连接到 Microsoft Graph 以获取完整配置文件。</span><span class="sxs-lookup"><span data-stu-id="ad307-109">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="ad307-110">准备工作</span><span class="sxs-lookup"><span data-stu-id="ad307-110">Before you begin</span></span>

<span data-ttu-id="ad307-111">请确保通过安装必备组件来设置开发 [环境](prerequisites.md)。</span><span class="sxs-lookup"><span data-stu-id="ad307-111">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md).</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ad307-112">安装先决条件</span><span class="sxs-lookup"><span data-stu-id="ad307-112">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="ad307-113">创建项目</span><span class="sxs-lookup"><span data-stu-id="ad307-113">Create your project</span></span>

<span data-ttu-id="ad307-114">使用 Teams 工具包创建你的第一个项目:</span><span class="sxs-lookup"><span data-stu-id="ad307-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="ad307-115">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="ad307-115">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="ad307-116">打开 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="ad307-116">Open Visual Studio code.</span></span>
1. <span data-ttu-id="ad307-117">通过选择边栏中的 Teams 图标，打开 Teams 工具包:</span><span class="sxs-lookup"><span data-stu-id="ad307-117">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code 边栏中的 Teams 图标。":::

1. <span data-ttu-id="ad307-119">选择 **创建新项目**。</span><span class="sxs-lookup"><span data-stu-id="ad307-119">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. <span data-ttu-id="ad307-121">选择 **创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="ad307-121">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="&quot;创建新项目&quot;的向导启动":::

1. <span data-ttu-id="ad307-123">在 **"选择功能"** 步骤中， **已** 选择 Tab 功能。</span><span class="sxs-lookup"><span data-stu-id="ad307-123">On the **Select capabilities** step, the **Tab** capability is already selected.</span></span> <span data-ttu-id="ad307-124">按 **确定**。</span><span class="sxs-lookup"><span data-stu-id="ad307-124">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="显示如何向新应用添加功能的屏幕截图。":::

1. <span data-ttu-id="ad307-126">在 **前端托管类型** 步骤中， 选择 **Azure**。</span><span class="sxs-lookup"><span data-stu-id="ad307-126">On the **Frontend hosting type** step, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="显示如何选择新应用的托管的屏幕截图。":::

1. <span data-ttu-id="ad307-128">在 **云资源** 步骤中， 选择 **确定**。</span><span class="sxs-lookup"><span data-stu-id="ad307-128">On the **Cloud resources** step, press **OK**.</span></span>  <span data-ttu-id="ad307-129">本教程不需要其他云资源。</span><span class="sxs-lookup"><span data-stu-id="ad307-129">We do not need additional cloud resources for this tutorial.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="显示如何为新应用添加云资源的屏幕截图。":::

1. <span data-ttu-id="ad307-131">在" **编程语言** 步骤中， 选择 **JavaScript**。</span><span class="sxs-lookup"><span data-stu-id="ad307-131">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="显示如何选择编程语言的屏幕截图。":::

1. <span data-ttu-id="ad307-133">选择工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="ad307-133">Select a workspace folder.</span></span> <span data-ttu-id="ad307-134">在工作区文件夹中为要创建的项目创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="ad307-134">A folder is created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="ad307-135">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="ad307-135">Enter a suitable name for your app, like `helloworld`.</span></span> <span data-ttu-id="ad307-136">应用的名称只能包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="ad307-136">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="ad307-137">按 **Enter** 以继续。</span><span class="sxs-lookup"><span data-stu-id="ad307-137">Press **Enter** to continue.</span></span>

<span data-ttu-id="ad307-138">你的应用Teams数秒钟内创建。</span><span class="sxs-lookup"><span data-stu-id="ad307-138">Your Teams app is created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="ad307-139">命令行</span><span class="sxs-lookup"><span data-stu-id="ad307-139">Command line</span></span>](#tab/cli)

<span data-ttu-id="ad307-140">使用 `teamsfx` CLI 创建你的第一个项目。</span><span class="sxs-lookup"><span data-stu-id="ad307-140">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="ad307-141">从要创建项目文件夹的文件夹开始。</span><span class="sxs-lookup"><span data-stu-id="ad307-141">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="ad307-142">CLI 会提出一些问题来引导创建项目。</span><span class="sxs-lookup"><span data-stu-id="ad307-142">The CLI walks through some questions to create the project.</span></span> <span data-ttu-id="ad307-143">每个问题将告诉你如何回答它，例如，使用箭头键来选择一个选项。</span><span class="sxs-lookup"><span data-stu-id="ad307-143">Each question will tell you how to answer it, for example, use arrow keys to select an option.</span></span> <span data-ttu-id="ad307-144">如果已回答问题，请通过按 **Enter** 确认。</span><span class="sxs-lookup"><span data-stu-id="ad307-144">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="ad307-145">选择 **"创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="ad307-145">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="ad307-146">选择" **选项卡** 功能。</span><span class="sxs-lookup"><span data-stu-id="ad307-146">Choose the **Tab** capability.</span></span>
1. <span data-ttu-id="ad307-147">选择 **Azure** 前端托管。</span><span class="sxs-lookup"><span data-stu-id="ad307-147">Select **Azure** frontend hosting.</span></span>
1. <span data-ttu-id="ad307-148">请勿选择任何云资源。</span><span class="sxs-lookup"><span data-stu-id="ad307-148">Do not select any cloud resources.</span></span>
1. <span data-ttu-id="ad307-149">选择 **JavaScript** 作为编程语言。</span><span class="sxs-lookup"><span data-stu-id="ad307-149">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="ad307-150">按 **Enter** 选择默认工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="ad307-150">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="ad307-151">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="ad307-151">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="ad307-152">应用的名称只能包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="ad307-152">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="ad307-153">在回答所有问题后，将创建项目。</span><span class="sxs-lookup"><span data-stu-id="ad307-153">Once all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="ad307-154">浏览源代码</span><span class="sxs-lookup"><span data-stu-id="ad307-154">Take a tour of the source code</span></span>

<span data-ttu-id="ad307-155">若要暂时跳过此部分， 你可以[运行本地应用](#run-your-app-locally)。</span><span class="sxs-lookup"><span data-stu-id="ad307-155">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="ad307-156">在 Teams 工具包配置你的项目后，你只需这些组件就可以使用这些组件为 Teams 构建基本的个人应用。</span><span class="sxs-lookup"><span data-stu-id="ad307-156">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="ad307-157">项目目录和文件显示在 Visual Studio 代码的资源管理器区域中。</span><span class="sxs-lookup"><span data-stu-id="ad307-157">The project directories and files display in the Explorer area of Visual Studio Code.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-app-project.png" alt-text="显示 Visual Studio Code 中个人应用的应用项目文件的屏幕截图。":::

<span data-ttu-id="ad307-159">工具包根据你在设置过程中添加的功能，自动在项目目录中创建标点文件夹。</span><span class="sxs-lookup"><span data-stu-id="ad307-159">The Toolkit automatically creates scaffolding for you in the project directory based on the capabilities you added during setup.</span></span> <span data-ttu-id="ad307-160">Teams 工具包将保持其对于新目录中 `.fx` 的状态。</span><span class="sxs-lookup"><span data-stu-id="ad307-160">The Teams Toolkit maintains its state for your app in the `.fx` directory.</span></span>  <span data-ttu-id="ad307-161">此目录中的其他项：</span><span class="sxs-lookup"><span data-stu-id="ad307-161">Among other items in this directory:</span></span>

- <span data-ttu-id="ad307-162">应用图标在 `color.png` 和 `outline.png`中存储为 PNG 文件。</span><span class="sxs-lookup"><span data-stu-id="ad307-162">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="ad307-163">发布到 Developer Portal for Teams 的应用清单存储在 `manifest.source.json`。</span><span class="sxs-lookup"><span data-stu-id="ad307-163">The app manifest for publishing to the Developer Portal for Teams is stored in `manifest.source.json`.</span></span>
- <span data-ttu-id="ad307-164">创建项目时选择的设置存储在 `settings.json`。</span><span class="sxs-lookup"><span data-stu-id="ad307-164">The settings you chose when creating the project are stored in `settings.json`.</span></span>

<span data-ttu-id="ad307-165">由于在设置过程中选择了选项卡功能，因此 Teams 工具包会为网站目录中的基本选项卡 `tabs` 代码。</span><span class="sxs-lookup"><span data-stu-id="ad307-165">Since you selected the tab capability during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab in the `tabs` directory.</span></span> <span data-ttu-id="ad307-166">此目录中有几个重要文件：</span><span class="sxs-lookup"><span data-stu-id="ad307-166">Within this directory there are several important files:</span></span>

- <span data-ttu-id="ad307-167">`tabs/src/index.jsx` 是前端应用的入口点，其中主应用程序组件 `App` 呈现为 `ReactDOM.render()`。</span><span class="sxs-lookup"><span data-stu-id="ad307-167">`tabs/src/index.jsx` is the front-end app's entry point, where the main `App` component is rendered with `ReactDOM.render()`.</span></span>
- <span data-ttu-id="ad307-168">`tabs/src/components/App.jsx` 处理应用中的 URL 路由。</span><span class="sxs-lookup"><span data-stu-id="ad307-168">`tabs/src/components/App.jsx` handles URL routing in your app.</span></span> <span data-ttu-id="ad307-169">它调用了 [JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md) 应用和团队之间建立通信。</span><span class="sxs-lookup"><span data-stu-id="ad307-169">It calls the [Microsoft Teams JavaScript client SDK](../tabs/how-to/using-teams-client-sdk.md) to establish communication between your app and Teams.</span></span>
- <span data-ttu-id="ad307-170">`tabs/src/components/Tab.jsx` 包含用于实现应用 UI 的代码。</span><span class="sxs-lookup"><span data-stu-id="ad307-170">`tabs/src/components/Tab.jsx` contains the code to implement the UI of your app.</span></span>
- <span data-ttu-id="ad307-171">`tabs/src/components/TabConfig.jsx` 包含用于实施配置应用的 UI 的代码。</span><span class="sxs-lookup"><span data-stu-id="ad307-171">`tabs/src/components/TabConfig.jsx` contains the code to implement the UI that configures your app.</span></span>

<span data-ttu-id="ad307-172">Teams 运行时需要几个选项卡，包括隐私声明、使用条款和配置选项卡。</span><span class="sxs-lookup"><span data-stu-id="ad307-172">Several tabs are required by the Teams runtime, including the privacy notice, terms of use, and configuration tabs.</span></span>  <span data-ttu-id="ad307-173">隐私声明和使用条款的代码位于同一目录中。</span><span class="sxs-lookup"><span data-stu-id="ad307-173">The code for the privacy notice and terms of use are located in the same directory.</span></span>

<span data-ttu-id="ad307-174">添加云功能时，会向项目添加其他目录。</span><span class="sxs-lookup"><span data-stu-id="ad307-174">When you add cloud functionality, additional directories are added to the project.</span></span>  <span data-ttu-id="ad307-175">最为明显的是， `api` 目录将代码存储到所编写的任何 Azure 函数中。</span><span class="sxs-lookup"><span data-stu-id="ad307-175">Most notably, the `api` directory holds the code to any Azure Functions you write.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="ad307-176">在本地运行应用</span><span class="sxs-lookup"><span data-stu-id="ad307-176">Run your app locally</span></span>

<span data-ttu-id="ad307-177">使用 Teams 工具包，你可以在本地运行应用。</span><span class="sxs-lookup"><span data-stu-id="ad307-177">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="ad307-178">这包含几个部分，是提供 Teams 所需的正确基础结构所必需的：</span><span class="sxs-lookup"><span data-stu-id="ad307-178">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="ad307-179">应用程序已注册 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="ad307-179">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="ad307-180">此应用程序具有与从加载应用的位置及其访问的任何后端资源相关联的权限。</span><span class="sxs-lookup"><span data-stu-id="ad307-180">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="ad307-181">托管 Web API 以辅助身份验证任务，作为应用和 Azure Active Directory 之间的代理。</span><span class="sxs-lookup"><span data-stu-id="ad307-181">A web API is hosted to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  <span data-ttu-id="ad307-182">这由 Azure 函数核心工具运行。</span><span class="sxs-lookup"><span data-stu-id="ad307-182">This is run by Azure Functions Core Tools.</span></span>  <span data-ttu-id="ad307-183">可以在 URL 位置访问 `https://localhost:5000`。</span><span class="sxs-lookup"><span data-stu-id="ad307-183">It can be accessed at the URL `https://localhost:5000`.</span></span>
- <span data-ttu-id="ad307-184">位于应用程序前端的 HTML、CSS 和 JavaScript 资源托管在本地服务中。</span><span class="sxs-lookup"><span data-stu-id="ad307-184">The HTML, CSS, and JavaScript resources that make up the front end of the app are hosted on a local service.</span></span> <span data-ttu-id="ad307-185">可通过访问文件 `https://localhost:3000`。</span><span class="sxs-lookup"><span data-stu-id="ad307-185">It can be accessed at `https://localhost:3000`.</span></span>
- <span data-ttu-id="ad307-186">生成应用清单，存在于 Teams 开发人员门户中。</span><span class="sxs-lookup"><span data-stu-id="ad307-186">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="ad307-187">Teams 使用应用清单告诉已连接客户端从何处加载应用。</span><span class="sxs-lookup"><span data-stu-id="ad307-187">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="ad307-188">完成后，可在 Teams 客户端中加载该应用。</span><span class="sxs-lookup"><span data-stu-id="ad307-188">Once this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="ad307-189">我们使用 Teams Web 客户端，以便可以在标准 Web 开发环境中查看 HTML、CSS 和 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="ad307-189">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a><span data-ttu-id="ad307-190">在 Visual Studio Code 本地生成和运行应用</span><span class="sxs-lookup"><span data-stu-id="ad307-190">Build and run your app locally in Visual Studio Code</span></span>

<span data-ttu-id="ad307-191">若要在本地构建和运行应用，请执行：</span><span class="sxs-lookup"><span data-stu-id="ad307-191">To build and run your app locally:</span></span>

1. <span data-ttu-id="ad307-192">在 Visual Studio Code 中，按 **F5** 以在调试模式下运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="ad307-192">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="ad307-193">首次运行该应用时，将下载所有依赖项并编译该应用。</span><span class="sxs-lookup"><span data-stu-id="ad307-193">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="ad307-194">编译完成后，将自动打开浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="ad307-194">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="ad307-195">这可能需要 3-5 分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="ad307-195">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="ad307-196">如果需要Toolkit，系统会提示您安装本地证书。</span><span class="sxs-lookup"><span data-stu-id="ad307-196">The Toolkit prompts you to install a local certificate if required.</span></span> <span data-ttu-id="ad307-197">此证书允许 Teams 从 `https://localhost`。</span><span class="sxs-lookup"><span data-stu-id="ad307-197">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="ad307-198">出现下列对话框时，选择"是"：</span><span class="sxs-lookup"><span data-stu-id="ad307-198">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="显示如何安装 SSL 证书以便 Teams 从 localhost 加载应用程序提示的屏幕截图。":::

1. <span data-ttu-id="ad307-200">Web 浏览器开始运行该应用。</span><span class="sxs-lookup"><span data-stu-id="ad307-200">Your web browser starts to run the app.</span></span> <span data-ttu-id="ad307-201">如果系统提示打开Teams，请选择 **"取消**"以保留在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="ad307-201">If prompted to open Teams desktop, select **Cancel** to remain in the browser.</span></span> <span data-ttu-id="ad307-202">系统有时还可能会提示你切换到Teams桌面;选择Teams Web 应用。</span><span class="sxs-lookup"><span data-stu-id="ad307-202">You may also be prompted to switch to Teams desktop at other times; select the Teams web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="显示启动后如何选择 Teams 的 Web 版本的屏幕截图":::

1. <span data-ttu-id="ad307-204">系统可能会提示你登录。</span><span class="sxs-lookup"><span data-stu-id="ad307-204">You may be prompted to sign in.</span></span>  <span data-ttu-id="ad307-205">如果是这样，则使用你的 M365 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="ad307-205">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="ad307-206">系统提示将应用安装到 Teams 时，按 **添加**。</span><span class="sxs-lookup"><span data-stu-id="ad307-206">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="ad307-207">现在将显示你的应用：</span><span class="sxs-lookup"><span data-stu-id="ad307-207">Your app is now displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/react-finished-app.png" alt-text="已完成应用的屏幕截图":::

<span data-ttu-id="ad307-209">你可以像执行任何其他 Web 应用程序一样执行正常的调试活动，例如设置断点。</span><span class="sxs-lookup"><span data-stu-id="ad307-209">You can do normal debugging activities as if this were any other web application, such as setting breakpoints.</span></span> <span data-ttu-id="ad307-210">该应用支持热重新加载。</span><span class="sxs-lookup"><span data-stu-id="ad307-210">The app supports hot reloading.</span></span> <span data-ttu-id="ad307-211">如果更改了项目内的任何文件，将重新加载页面。</span><span class="sxs-lookup"><span data-stu-id="ad307-211">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="ad307-212">在调试器中本地运行应用时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="ad307-212">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="ad307-213">按 F5 时，Teams 工具包:</span><span class="sxs-lookup"><span data-stu-id="ad307-213">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="ad307-214">使用 Azure Active Directory 注册应用程序。</span><span class="sxs-lookup"><span data-stu-id="ad307-214">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="ad307-215">*已并行* Teams 中的应用。</span><span class="sxs-lookup"><span data-stu-id="ad307-215">*Sideloaded* your app in Teams.</span></span>
1. <span data-ttu-id="ad307-216">使用 Azure 函数核心工具中心 [本地运行的应用程序后端](/azure/azure-functions/functions-run-local?#start)。</span><span class="sxs-lookup"><span data-stu-id="ad307-216">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="ad307-217">启动应用程序本地托管的前端。</span><span class="sxs-lookup"><span data-stu-id="ad307-217">Started your application front-end hosted locally.</span></span>
1. <span data-ttu-id="ad307-218">启动Microsoft Teams Web 浏览器中使用命令指示Teams从 旁加载应用程序 `https://localhost:3000/tab` 。</span><span class="sxs-lookup"><span data-stu-id="ad307-218">Started Microsoft Teams in a web browser with a command to instruct Teams to side load the application from `https://localhost:3000/tab`.</span></span> <span data-ttu-id="ad307-219">这是在应用程序清单中注册的 URL。</span><span class="sxs-lookup"><span data-stu-id="ad307-219">This is the URL registered in the application manifest.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="ad307-220">了解如何在本地运行应用时解决常见问题。</span><span class="sxs-lookup"><span data-stu-id="ad307-220">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="ad307-221">若要在 Teams 中成功运行应用，必须具有允许应用旁加载的 Teams 帐户。</span><span class="sxs-lookup"><span data-stu-id="ad307-221">To successfully run your app in Teams, you must have a Teams account that allows app sideloading.</span></span> <span data-ttu-id="ad307-222">有关打开帐户详细信息，请参阅 [先决条件](prerequisites.md#enable-sideloading)。</span><span class="sxs-lookup"><span data-stu-id="ad307-222">For more information on account opening, see [prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="ad307-223">了解将应用部署到 Azure 时会发生的情况</span><span class="sxs-lookup"><span data-stu-id="ad307-223">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="ad307-224">部署之前，应用程序已在本地运行:</span><span class="sxs-lookup"><span data-stu-id="ad307-224">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="ad307-225">后端使用 **Azure Functions Core Tools** 运行。</span><span class="sxs-lookup"><span data-stu-id="ad307-225">The backend runs using **Azure Functions Core Tools**.</span></span>
1. <span data-ttu-id="ad307-226">应用程序 HTTP 终结点 (Microsoft Teams 在此加载应用程序) 在本地运行。</span><span class="sxs-lookup"><span data-stu-id="ad307-226">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="ad307-227">部署涉及在活动的 Azure 订阅上预配资源，以及将应用程序的后端和前端代码部署或上载到 Azure。</span><span class="sxs-lookup"><span data-stu-id="ad307-227">Deployment involves provisioning resources on an active Azure subscription and deploying or uploading the backend and frontend code for the application to Azure.</span></span>

1. <span data-ttu-id="ad307-228">后端（如果已配置）使用各种 Azure 服务，包括 Azure 应用服务和 Azure 存储空间。</span><span class="sxs-lookup"><span data-stu-id="ad307-228">The backend if configured uses a variety of Azure services, including Azure App Service and Azure Storage.</span></span>
1. <span data-ttu-id="ad307-229">将前端应用程序部署到配置用于静态 Web 托管的 Azure 存储帐户。</span><span class="sxs-lookup"><span data-stu-id="ad307-229">The frontend application will be deployed to an Azure Storage account configured for static web hosting.</span></span>

</details>

## <a name="see-also"></a><span data-ttu-id="ad307-230">另请参阅</span><span class="sxs-lookup"><span data-stu-id="ad307-230">See also</span></span>

- [<span data-ttu-id="ad307-231">使用 Blazor 创建 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="ad307-231">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="ad307-232">[创建 Teams 应用作为 SharePoint Web 部件](first-app-spfx.md) （不需要 Azure）</span><span class="sxs-lookup"><span data-stu-id="ad307-232">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="ad307-233">创建对话机器人应用</span><span class="sxs-lookup"><span data-stu-id="ad307-233">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="ad307-234">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="ad307-234">Create a messaging extension</span></span>](first-message-extension.md)

## <a name="next-step"></a><span data-ttu-id="ad307-235">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ad307-235">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="ad307-236">使用 Blazor 创建 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="ad307-236">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
