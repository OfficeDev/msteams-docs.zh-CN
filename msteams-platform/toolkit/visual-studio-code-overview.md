---
title: 使用 Microsoft Teams Toolkit 和 Visual Studio 代码生成应用
description: 开始使用 Microsoft Teams Visual Studio直接在 Visual Studio Code 中生成出色的自定义Toolkit
keywords: teams visual studio code toolkit
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: b2cfab5cb2ea2d727608b6ea3bbfec3271b2b039
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994138"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a><span data-ttu-id="012d6-104">使用 Teams 应用和Toolkit Visual Studio生成应用</span><span class="sxs-lookup"><span data-stu-id="012d6-104">Build apps with the Teams Toolkit and Visual Studio Code</span></span>

<span data-ttu-id="012d6-105">Teams Toolkit for Visual Studio Code 通过针对开发人员体验的"零配置"方法帮助开发人员创建和部署具有集成标识、访问云存储、Microsoft Graph 数据以及 Azure 和 M365 中其他服务的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="012d6-105">The Teams Toolkit for Visual Studio Code helps developers create and deploy Teams apps with integrated identity, access to cloud storage, data from Microsoft Graph, and other services in Azure and M365 with a “zero-configuration” approach to the developer experience.</span></span>  

<span data-ttu-id="012d6-106">还可以将工具包与 Visual Studio一 (CLI `teamsfx`) 。</span><span class="sxs-lookup"><span data-stu-id="012d6-106">You also can use the toolkit with Visual Studio or as a CLI (called `teamsfx`).</span></span>

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a><span data-ttu-id="012d6-107">安装 Teams Toolkit for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="012d6-107">Install the Teams Toolkit for Visual Studio Code</span></span>

1. <span data-ttu-id="012d6-108">打开 Visual Studio 代码。</span><span class="sxs-lookup"><span data-stu-id="012d6-108">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="012d6-109">Select the Extensions view (**Ctrl+Shift+X**  /  **⌘⇧-X** or **View > Extensions**) .</span><span class="sxs-lookup"><span data-stu-id="012d6-109">Select the Extensions view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions**).</span></span>
1. <span data-ttu-id="012d6-110">在搜索框中，输入 _Teams Toolkit_。</span><span class="sxs-lookup"><span data-stu-id="012d6-110">In the search box, enter _Teams Toolkit_.</span></span>
1. <span data-ttu-id="012d6-111">在 Teams 应用旁的绿色安装按钮上选择Toolkit。</span><span class="sxs-lookup"><span data-stu-id="012d6-111">Select on the green install button next to the Teams Toolkit.</span></span>

<span data-ttu-id="012d6-112">还可以在"Toolkit代码Visual Studio [上找到 Teams 服务](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。</span><span class="sxs-lookup"><span data-stu-id="012d6-112">You also can find the Teams Toolkit on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span></span>

<span data-ttu-id="012d6-113">以下工具由代码扩展Visual Studio安装。</span><span class="sxs-lookup"><span data-stu-id="012d6-113">The following tools are installed by the Visual Studio Code extension when they are needed.</span></span> <span data-ttu-id="012d6-114">如果已安装，则改为使用已安装的版本。</span><span class="sxs-lookup"><span data-stu-id="012d6-114">If already installed, the installed version is used instead.</span></span> <span data-ttu-id="012d6-115">如果使用 Linux (WSL) ，则必须先安装这些工具，然后才能使用：</span><span class="sxs-lookup"><span data-stu-id="012d6-115">If using Linux (including WSL), you must install these tools before use:</span></span>

- [<span data-ttu-id="012d6-116">Azure 函数核心工具</span><span class="sxs-lookup"><span data-stu-id="012d6-116">Azure Functions Core Tools</span></span>](/azure/azure-functions/functions-run-local)

    <span data-ttu-id="012d6-117">Azure Functions Core Tools 用于在本地调试运行期间在本地运行任何后端组件，包括在 Azure 中运行服务时所需的身份验证帮助程序。</span><span class="sxs-lookup"><span data-stu-id="012d6-117">Azure Functions Core Tools is used to run any backend components locally during a local debug run, including the authentication helpers required when running your services in Azure.</span></span> <span data-ttu-id="012d6-118">它使用 npm 安装在项目目录中 `devDependencies` 。</span><span class="sxs-lookup"><span data-stu-id="012d6-118">It is installed within the project directory using the npm `devDependencies`.</span></span>

- [<span data-ttu-id="012d6-119">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="012d6-119">.NET SDK</span></span>](/dotnet/core/install/)

    <span data-ttu-id="012d6-120">.NET SDK 用于安装用于本地调试和 Azure Functions 应用部署的自定义绑定。</span><span class="sxs-lookup"><span data-stu-id="012d6-120">The .NET SDK is used to install customized bindings for local debugging and Azure Functions app deployments.</span></span> <span data-ttu-id="012d6-121">如果尚未全局安装 .NET 3.1 或更高版本 SDK，则安装可移植版本。</span><span class="sxs-lookup"><span data-stu-id="012d6-121">If you have not installed the .NET 3.1 or later SDK globally, the portable version is installed.</span></span>

- [<span data-ttu-id="012d6-122">ngrok</span><span class="sxs-lookup"><span data-stu-id="012d6-122">ngrok</span></span>](https://ngrok.com/download)

    <span data-ttu-id="012d6-123">一些 Teams 应用 (对话机器人、消息传递扩展和传入 webhook) 需要入站连接。</span><span class="sxs-lookup"><span data-stu-id="012d6-123">Some Teams app features (conversational bots, messaging extensions, and incoming webhooks) require inbound connections.</span></span>  <span data-ttu-id="012d6-124">你需要通过隧道向 Teams 公开你的开发系统。</span><span class="sxs-lookup"><span data-stu-id="012d6-124">You need to expose your development system to Teams through a tunnel.</span></span> <span data-ttu-id="012d6-125">仅包含选项卡的应用不需要隧道。</span><span class="sxs-lookup"><span data-stu-id="012d6-125">A tunnel is not required for apps that only include tabs.</span></span>  <span data-ttu-id="012d6-126">此包安装在项目目录中， (npm `devDependencies`) 。</span><span class="sxs-lookup"><span data-stu-id="012d6-126">This package is installed within the project directory (using npm `devDependencies`).</span></span>

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a><span data-ttu-id="012d6-127">使用 Teams Toolkit for Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="012d6-127">Use the Teams Toolkit for Visual Studio Code</span></span>

- [<span data-ttu-id="012d6-128">设置新项目</span><span class="sxs-lookup"><span data-stu-id="012d6-128">Set up a new project</span></span>](#set-up-a-new-teams-project)
- [<span data-ttu-id="012d6-129">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="012d6-129">Configure your app</span></span>](#configure-your-app)
- [<span data-ttu-id="012d6-130">在本地运行应用</span><span class="sxs-lookup"><span data-stu-id="012d6-130">Run your app locally</span></span>](#install-and-run-your-app-locally)
- [<span data-ttu-id="012d6-131">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="012d6-131">Publish your app</span></span>](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a><span data-ttu-id="012d6-132">设置新的 Teams 项目</span><span class="sxs-lookup"><span data-stu-id="012d6-132">Set up a new Teams project</span></span>

<span data-ttu-id="012d6-133">Teams Toolkit可以创建在托管在 M365 SharePoint 环境的 Azure 或 SPFx Web 部件中的 React 应用。</span><span class="sxs-lookup"><span data-stu-id="012d6-133">The Teams Toolkit can create React apps that are hosted in Azure or SPFx web parts that are hosted on your M365 SharePoint environment.</span></span> <span data-ttu-id="012d6-134">若要创建在 Azure 上托管的新 React 应用：</span><span class="sxs-lookup"><span data-stu-id="012d6-134">To create a new React app to be hosted on Azure:</span></span>

1. <span data-ttu-id="012d6-135">打开 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="012d6-135">Open Visual Studio code.</span></span>
1. <span data-ttu-id="012d6-136">通过选择边栏中的 Teams 图标，打开 Teams 工具包:</span><span class="sxs-lookup"><span data-stu-id="012d6-136">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code 边栏中的 Teams 图标。":::

1. <span data-ttu-id="012d6-138">选择 **创建新项目**。</span><span class="sxs-lookup"><span data-stu-id="012d6-138">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. <span data-ttu-id="012d6-140">选择 **创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="012d6-140">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="&quot;创建新项目&quot;的向导启动":::

1. <span data-ttu-id="012d6-142">在 **"选择功能"** 步骤中， **已** 选择 Tab 功能。</span><span class="sxs-lookup"><span data-stu-id="012d6-142">On the **Select capabilities** step, the **Tab** capability is already selected.</span></span> <span data-ttu-id="012d6-143">还可以选择自动程序 **与\*\*\*\*消息传递扩展**。</span><span class="sxs-lookup"><span data-stu-id="012d6-143">You can also optionally select **Bot** and **Messaging Extension**.</span></span>  <span data-ttu-id="012d6-144">按 **确定**。</span><span class="sxs-lookup"><span data-stu-id="012d6-144">Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="显示如何向新应用添加功能的屏幕截图。":::

1. <span data-ttu-id="012d6-146">在 **前端托管类型** 步骤中， 选择 **Azure**。</span><span class="sxs-lookup"><span data-stu-id="012d6-146">On the **Frontend hosting type** step, select **Azure**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="显示如何选择新应用的托管的屏幕截图。":::

1. <span data-ttu-id="012d6-148">（可选）在"云 **资源"** 步骤中，选择应用程序使用的云资源。</span><span class="sxs-lookup"><span data-stu-id="012d6-148">Optionally, on the **Cloud resources** step, select cloud resources that your application uses.</span></span> <span data-ttu-id="012d6-149">可以选择 CRUD (、读取、更新和删除) 表或 API SQL访问：</span><span class="sxs-lookup"><span data-stu-id="012d6-149">You can select CRUD (create, read, update, and delete) access to a SQL table or an API:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="显示如何为新应用添加云资源的屏幕截图。":::

1. <span data-ttu-id="012d6-151">在 **"编程语言"** 步骤中，可以选择 **"JavaScript"或\*\*\*\*"TypeScript"：**</span><span class="sxs-lookup"><span data-stu-id="012d6-151">On the **Programming Language** step, you can choose **JavaScript** or **TypeScript**:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="显示如何选择编程语言的屏幕截图。":::

1. <span data-ttu-id="012d6-153">选择工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="012d6-153">Select a workspace folder.</span></span> <span data-ttu-id="012d6-154">在工作区文件夹中为要创建的项目创建文件夹。</span><span class="sxs-lookup"><span data-stu-id="012d6-154">A folder is created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="012d6-155">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="012d6-155">Enter a suitable name for your app, like `helloworld`.</span></span> <span data-ttu-id="012d6-156">应用的名称只能包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="012d6-156">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="012d6-157">按 **Enter** 以继续。</span><span class="sxs-lookup"><span data-stu-id="012d6-157">Press **Enter** to continue.</span></span>

<span data-ttu-id="012d6-158">Teams 应用在几秒钟内创建。</span><span class="sxs-lookup"><span data-stu-id="012d6-158">Your Teams app is created within a few seconds.</span></span> <span data-ttu-id="012d6-159">基架应用包含用于处理 Azure Active Directory 单一登录和 Microsoft Graph 访问的代码。</span><span class="sxs-lookup"><span data-stu-id="012d6-159">The scaffolded app contains code to handle single sign-on with Azure Active Directory and access to the Microsoft Graph.</span></span>  <span data-ttu-id="012d6-160">如果你选择了 Azure 资源，则这些资源的代码也可用。</span><span class="sxs-lookup"><span data-stu-id="012d6-160">If you selected Azure resources, then the code for those resources is also available.</span></span>

<span data-ttu-id="012d6-161">有关 SPFx 创建和发布过程的演练，请参阅 [SPFx 教程](../get-started/first-app-spfx.md)。</span><span class="sxs-lookup"><span data-stu-id="012d6-161">For a walk-through of the SPFx creation and publication process, see the [SPFx tutorial](../get-started/first-app-spfx.md).</span></span>

## <a name="configure-your-app"></a><span data-ttu-id="012d6-162">配置应用程序</span><span class="sxs-lookup"><span data-stu-id="012d6-162">Configure your app</span></span>

<span data-ttu-id="012d6-163">Teams 应用的核心包括三个组件：</span><span class="sxs-lookup"><span data-stu-id="012d6-163">At its core, the Teams app embraces three components:</span></span>

  1. <span data-ttu-id="012d6-164">Microsoft Teams 客户端 (Web、桌面或移动) 用户与你的应用进行交互。</span><span class="sxs-lookup"><span data-stu-id="012d6-164">The Microsoft Teams client (web, desktop or mobile) where users interact with your app.</span></span>
  1. <span data-ttu-id="012d6-165">响应对在 Teams 中显示的内容的请求的服务器。</span><span class="sxs-lookup"><span data-stu-id="012d6-165">A server that responds to requests for content that is displayed in Teams.</span></span> <span data-ttu-id="012d6-166">例如，HTML 选项卡内容或自动程序自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="012d6-166">For example, HTML tab content or a bot Adaptive Card.</span></span>
  1. <span data-ttu-id="012d6-167">Teams 应用包包含三个文件：</span><span class="sxs-lookup"><span data-stu-id="012d6-167">A Teams app package consists of three files:</span></span>

      > [!div class="checklist"]
      >
      > - <span data-ttu-id="012d6-168">打开manifest.js。</span><span class="sxs-lookup"><span data-stu-id="012d6-168">The manifest.json.</span></span>
      > - <span data-ttu-id="012d6-169">要 [显示在](../resources/schema/manifest-schema.md#icons) 公共或组织应用程序目录中的应用的颜色图标。</span><span class="sxs-lookup"><span data-stu-id="012d6-169">A [color icon](../resources/schema/manifest-schema.md#icons) for your app to display in the public or organization app catalog.</span></span>
      > - <span data-ttu-id="012d6-170">显示在 [Teams](../resources/schema/manifest-schema.md#icons) 活动栏上的大纲图标。</span><span class="sxs-lookup"><span data-stu-id="012d6-170">An [outline icon](../resources/schema/manifest-schema.md#icons) for display on the Teams activity bar.</span></span>

<span data-ttu-id="012d6-171">清单和图标在上传到 Teams 之前 `.fx` 存储在项目的文件夹中。</span><span class="sxs-lookup"><span data-stu-id="012d6-171">The manifest and icons are stored in the `.fx` folder of your project prior to being uploaded to Teams.</span></span> <span data-ttu-id="012d6-172">安装应用后，Teams 客户端将分析清单文件以确定所需信息，如应用名称和服务所在的 URL。</span><span class="sxs-lookup"><span data-stu-id="012d6-172">When an app is installed, the Teams client parses the manifest file to determine needed information like the name of your app and the URL where the services are located.</span></span>

1. <span data-ttu-id="012d6-173">若要配置你的应用，请导航到"Toolkit代码 **"Visual Studio"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="012d6-173">To configure your app, navigate to the **Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="012d6-174">选择 **"项目"** 部分中的" **清单编辑器** "。</span><span class="sxs-lookup"><span data-stu-id="012d6-174">Select **Manifest Editor** in the **Project** section.</span></span>

<span data-ttu-id="012d6-175">编辑"应用详细信息"页中的字段将更新manifest.js作为应用包的一部分交付的 on 文件的内容。</span><span class="sxs-lookup"><span data-stu-id="012d6-175">Editing the fields in the App details page updates the contents of the manifest.json file that is ultimately shipped as part of the app package.</span></span>

## <a name="install-and-run-your-app-locally"></a><span data-ttu-id="012d6-176">在本地安装和运行应用</span><span class="sxs-lookup"><span data-stu-id="012d6-176">Install and run your app locally</span></span>

<span data-ttu-id="012d6-177">若要在本地构建并运行应用程序:</span><span class="sxs-lookup"><span data-stu-id="012d6-177">To build and run your app locally:</span></span>

1. <span data-ttu-id="012d6-178">在 Visual Studio Code 中，按 **F5** 以在调试模式下运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="012d6-178">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="012d6-179">首次运行该应用时，将下载所有依赖项并编译该应用。</span><span class="sxs-lookup"><span data-stu-id="012d6-179">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="012d6-180">编译完成后，将自动打开浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="012d6-180">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="012d6-181">这可能需要 3-5 分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="012d6-181">This can take 3-5 minutes to complete.</span></span>

   <span data-ttu-id="012d6-182">工具包会提示你安装本地证书（如果需要）。</span><span class="sxs-lookup"><span data-stu-id="012d6-182">The toolkit prompts you to install a local certificate if required.</span></span> <span data-ttu-id="012d6-183">此证书允许 Teams 从 `https://localhost`。</span><span class="sxs-lookup"><span data-stu-id="012d6-183">This certificate allows Teams to load your application from `https://localhost`.</span></span> <span data-ttu-id="012d6-184">出现下列对话框时，选择"是"：</span><span class="sxs-lookup"><span data-stu-id="012d6-184">Select yes when the following dialog appears:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="显示如何安装 SSL 证书以便 Teams 从 localhost 加载应用程序提示的屏幕截图。":::

1. <span data-ttu-id="012d6-186">Web 浏览器开始运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="012d6-186">Your web browser is started to run the application.</span></span> <span data-ttu-id="012d6-187">如果系统提示打开 Microsoft Teams，请选择"取消"以留在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="012d6-187">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="012d6-188">此外，系统还会提示你在其他时间切换到 Teams 应用程序。</span><span class="sxs-lookup"><span data-stu-id="012d6-188">You may also be prompted to switch to the Teams application at other times.</span></span> <span data-ttu-id="012d6-189">发生这种情况时，选择 Web 应用。</span><span class="sxs-lookup"><span data-stu-id="012d6-189">Select the web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="显示启动后如何选择 Teams 的 Web 版本的屏幕截图":::

1. <span data-ttu-id="012d6-191">系统可能会提示你登录。</span><span class="sxs-lookup"><span data-stu-id="012d6-191">You may be prompted to sign in.</span></span> <span data-ttu-id="012d6-192">如果是这样，则使用你的 M365 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="012d6-192">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="012d6-193">系统提示将应用安装到 Teams 时，按 **添加**。</span><span class="sxs-lookup"><span data-stu-id="012d6-193">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="012d6-194">后端和前端都挂钩到 Visual Studio 代码调试器。</span><span class="sxs-lookup"><span data-stu-id="012d6-194">Both the backend and frontend are hooked into the Visual Studio Code debugger.</span></span>  <span data-ttu-id="012d6-195">这允许你在代码中的任意位置设置断点并检查状态。</span><span class="sxs-lookup"><span data-stu-id="012d6-195">This allows you to set breakpoints anywhere in your code and inspect state.</span></span>  <span data-ttu-id="012d6-196">还可以在浏览器中使用任何前端调试 (如 React 开发人员) 工具。</span><span class="sxs-lookup"><span data-stu-id="012d6-196">You can also use any frontend debugging tools (such as the React Developer Tools) within the browser.</span></span>  <span data-ttu-id="012d6-197">有关在代码中调试Visual Studio，请参阅 [文档](https://code.visualstudio.com/Docs/editor/debugging)。</span><span class="sxs-lookup"><span data-stu-id="012d6-197">For more information about debugging in Visual Studio Code, review [the documentation](https://code.visualstudio.com/Docs/editor/debugging).</span></span>

## <a name="publish-your-app-to-teams"></a><span data-ttu-id="012d6-198">将应用发布到 Teams</span><span class="sxs-lookup"><span data-stu-id="012d6-198">Publish your app to Teams</span></span>

<span data-ttu-id="012d6-199">必须先将应用发布到 Teams 开发人员门户，然后才能供其他人使用。</span><span class="sxs-lookup"><span data-stu-id="012d6-199">Before it can be used by other people, you must publish your app to the Developer Portal for Teams.</span></span>

1. <span data-ttu-id="012d6-200">若要发布你的应用，请导航到"Toolkit代码 **"Visual Studio"** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="012d6-200">To publish your app, navigate to the **Teams Toolkit** tab in Visual Studio Code.</span></span>
1. <span data-ttu-id="012d6-201">选择 **"发布Teams"\*\*\*\*部分中的**"Project"。</span><span class="sxs-lookup"><span data-stu-id="012d6-201">Select **Publish to Teams** in the **Project** section.</span></span>

<span data-ttu-id="012d6-202">如果使用 Azure 托管，则必须已预配并部署到云。</span><span class="sxs-lookup"><span data-stu-id="012d6-202">If using Azure hosting, you must have provisioned and deployed to the cloud.</span></span> <span data-ttu-id="012d6-203">有关发布过程SPFx，请参阅 SPFx[教程](../get-started/first-app-spfx.md)。</span><span class="sxs-lookup"><span data-stu-id="012d6-203">For a walk-through of the SPFx publication process, see the [SPFx tutorial](../get-started/first-app-spfx.md).</span></span>

## <a name="next-step"></a><span data-ttu-id="012d6-204">后续步骤</span><span class="sxs-lookup"><span data-stu-id="012d6-204">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="012d6-205">维护和支持已发布的应用</span><span class="sxs-lookup"><span data-stu-id="012d6-205">Maintaining and supporting your published app</span></span>](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
