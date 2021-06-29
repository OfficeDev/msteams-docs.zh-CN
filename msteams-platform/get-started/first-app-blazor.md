---
title: 入门 - 使用 Blazor 生成Teams应用程序
author: adrianhall
description: 快速创建显示"Hello，World！"的 Microsoft Teams 应用。 message using the Microsoft Teams Toolkit and .NET Blazor.
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.openlocfilehash: f40331ed06a401d60092e884add2cfa747c3ebdc
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179949"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a><span data-ttu-id="0e911-104">使用 Blazor 生成Microsoft Teams应用程序</span><span class="sxs-lookup"><span data-stu-id="0e911-104">Build and run your first Microsoft Teams app with Blazor</span></span>

<span data-ttu-id="0e911-105">在本教程中，你将在 .NET/Blazor Microsoft Teams一个新的应用程序，该应用实现简单的个人应用以从 Microsoft Graph。</span><span class="sxs-lookup"><span data-stu-id="0e911-105">In this tutorial, you will create a new Microsoft Teams app in .NET/Blazor that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="0e911-106"> (个人应用包括一组作用域为供个人使用的选项卡。) 在本教程中，你将了解 Teams 应用的结构、如何在本地运行应用以及如何将应用部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="0e911-106">(A *personal app* includes a set of tabs scoped for individual use.)  During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="0e911-107">构建的应用将显示当前用户的基本用户信息。</span><span class="sxs-lookup"><span data-stu-id="0e911-107">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="0e911-108">授予权限后，应用会作为当前用户连接到 Microsoft Graph 以获取完整配置文件。</span><span class="sxs-lookup"><span data-stu-id="0e911-108">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="0e911-109">准备工作</span><span class="sxs-lookup"><span data-stu-id="0e911-109">Before you begin</span></span>

<span data-ttu-id="0e911-110">通过安装[先决条件](prerequisites.md)确保您的开发环境已设置</span><span class="sxs-lookup"><span data-stu-id="0e911-110">Make sure your development environment is set up by installing the [prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e911-111">安装先决条件</span><span class="sxs-lookup"><span data-stu-id="0e911-111">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="0e911-112">创建项目</span><span class="sxs-lookup"><span data-stu-id="0e911-112">Create your project</span></span>

<span data-ttu-id="0e911-113">使用 Teams 工具包创建你的第一个项目:</span><span class="sxs-lookup"><span data-stu-id="0e911-113">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="0e911-114">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="0e911-114">Visual Studio 2019</span></span>](#tab/vs)

1. <span data-ttu-id="0e911-115">打开Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="0e911-115">Open Visual Studio 2019.</span></span>

1. <span data-ttu-id="0e911-116">选择 **创建新项目**。</span><span class="sxs-lookup"><span data-stu-id="0e911-116">Select **Create a new project**.</span></span>

1. <span data-ttu-id="0e911-117">选择 **Microsoft Teams应用**"，然后按"下一 **步"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-117">Select **Microsoft Teams App**, then press **Next**.</span></span>  <span data-ttu-id="0e911-118">若要帮助您查找模板，请使用项目类型 **Microsoft Teams**。</span><span class="sxs-lookup"><span data-stu-id="0e911-118">To help you find the template, use the project type **Microsoft Teams**.</span></span>

1. <span data-ttu-id="0e911-119">为项目和解决方案命名，然后按"下一步 **"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-119">Give the project and solution a good name, then press **Next**.</span></span>

1. <span data-ttu-id="0e911-120">提供应用程序名称和公司名称，然后按"创建 **"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-120">Provide the application name and company name, then press **Create**.</span></span>  <span data-ttu-id="0e911-121">应用程序名称和公司名称将显示给最终用户。</span><span class="sxs-lookup"><span data-stu-id="0e911-121">The application name and company name are displayed to your end users.</span></span>

1. <span data-ttu-id="0e911-122">将在数秒钟内创建你的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="0e911-122">Your Teams app will be created within a few seconds.</span></span>  <span data-ttu-id="0e911-123">创建项目后，使用 M365 设置单一登录：</span><span class="sxs-lookup"><span data-stu-id="0e911-123">Once the project is created, set up single sign-on with M365:</span></span>

   - <span data-ttu-id="0e911-124">选择 **Project**  >  **TeamsFx**  >  **配置 SSO..."。**</span><span class="sxs-lookup"><span data-stu-id="0e911-124">Select **Project** > **TeamsFx** > **Configure for SSO...**.</span></span>
   - <span data-ttu-id="0e911-125">系统提示时，登录到 M365 管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="0e911-125">When prompted, sign in to your M365 administrator account.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="0e911-126">命令行</span><span class="sxs-lookup"><span data-stu-id="0e911-126">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="0e911-127">打开终端并选择你希望创建项目的目录。</span><span class="sxs-lookup"><span data-stu-id="0e911-127">Open a Terminal and select the directory where you wish to create the project.</span></span>

1. <span data-ttu-id="0e911-128">运行 `dotnet new -i` 以从以下位置安装NuGet：</span><span class="sxs-lookup"><span data-stu-id="0e911-128">Run `dotnet new -i` to install the template from NuGet:</span></span>

   ``` bash
   dotnet new --install Microsoft.TeamsFx.VisualStudio.ProjectTemplates::0.1.43-beta
   ```

   <span data-ttu-id="0e911-129">你只需在首次或更新模板时这样做。</span><span class="sxs-lookup"><span data-stu-id="0e911-129">You only need to do this the first time or when updating the template.</span></span> <span data-ttu-id="0e911-130">检查[NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/)程序包的最新版本。</span><span class="sxs-lookup"><span data-stu-id="0e911-130">Check [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) for the latest version of this package.</span></span>

1. <span data-ttu-id="0e911-131">创建目录：</span><span class="sxs-lookup"><span data-stu-id="0e911-131">Create a directory:</span></span>

   ``` bash
   mkdir helloworld
   ```

1. <span data-ttu-id="0e911-132">运行 `dotnet new` 以创建新项目：</span><span class="sxs-lookup"><span data-stu-id="0e911-132">Run `dotnet new` to create a new project:</span></span>

   ``` bash
   dotnet new teamsapp --shortName my-teams-app --companyName "My Company"
   ```

1. <span data-ttu-id="0e911-133">搭建基架后，配置用于部署Teams项目：</span><span class="sxs-lookup"><span data-stu-id="0e911-133">Once scaffolded, configure the project for Teams deployment:</span></span>

   ``` bash
   teamsfx init
   ```

<span data-ttu-id="0e911-134">现在可以在 Visual Studio 中打开解决方案进行调试。</span><span class="sxs-lookup"><span data-stu-id="0e911-134">You can now open the solution in Visual Studio for debugging.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="0e911-135">浏览源代码</span><span class="sxs-lookup"><span data-stu-id="0e911-135">Take a tour of the source code</span></span>

<span data-ttu-id="0e911-136">若要暂时跳过此部分， 你可以[运行本地应用](#run-your-app-locally)。</span><span class="sxs-lookup"><span data-stu-id="0e911-136">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="0e911-137">在 Teams 工具包配置你的项目后，你只需这些组件就可以使用这些组件为 Teams 构建基本的个人应用。</span><span class="sxs-lookup"><span data-stu-id="0e911-137">Once the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="0e911-138">项目目录和文件显示在 2019 年 10 月Visual Studio资源管理器"区域中。</span><span class="sxs-lookup"><span data-stu-id="0e911-138">The project directories and files display in the Solution Explorer area of Visual Studio 2019.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="Screenshot showing app project files for a personal app in Visual Studio 2019.":::

- <span data-ttu-id="0e911-140">应用图标在 `color.png` 和 `outline.png`中存储为 PNG 文件。</span><span class="sxs-lookup"><span data-stu-id="0e911-140">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="0e911-141">用于通过开发人员门户发布的应用程序清单Teams存储在 中 `Properties/manifest.json` 。</span><span class="sxs-lookup"><span data-stu-id="0e911-141">The app manifest for publishing through the Developer Portal for Teams is stored in `Properties/manifest.json`.</span></span>
- <span data-ttu-id="0e911-142">提供后端控制器以帮助 `Controllers/BackendController.cs` 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="0e911-142">A backend controller is provided in `Controllers/BackendController.cs` for assisting with authentication.</span></span>

<span data-ttu-id="0e911-143">由于在设置期间创建了选项卡应用程序，Teams Toolkit将基本选项卡的所有必要代码搭建为[Blazor Server](/aspnet/core/blazor)。</span><span class="sxs-lookup"><span data-stu-id="0e911-143">Since you created a tab app during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab as a [Blazor Server](/aspnet/core/blazor).</span></span>

- <span data-ttu-id="0e911-144">`Pages/Tab.razor` 是前端应用程序的入口点。</span><span class="sxs-lookup"><span data-stu-id="0e911-144">`Pages/Tab.razor` is the front-end application's entry point.</span></span>
- <span data-ttu-id="0e911-145">`TeamsFx.cs``JS/src/index.js`和 用于初始化与主机Teams通信。</span><span class="sxs-lookup"><span data-stu-id="0e911-145">`TeamsFx.cs` and `JS/src/index.js` is used for initializing communications with the Teams host.</span></span>

<span data-ttu-id="0e911-146">可以通过向应用程序添加其他 ASP.NET Core控制器来添加后端功能。</span><span class="sxs-lookup"><span data-stu-id="0e911-146">You can add backend functionality by adding additional ASP.NET Core controllers to your application.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="0e911-147">在本地运行应用</span><span class="sxs-lookup"><span data-stu-id="0e911-147">Run your app locally</span></span>

<span data-ttu-id="0e911-148">使用 Teams 工具包，你可以在本地运行应用。</span><span class="sxs-lookup"><span data-stu-id="0e911-148">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="0e911-149">这包含几个部分，是提供 Teams 所需的正确基础结构所必需的：</span><span class="sxs-lookup"><span data-stu-id="0e911-149">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="0e911-150">应用程序已注册 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="0e911-150">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="0e911-151">此应用程序具有与从加载应用的位置及其访问的任何后端资源相关联的权限。</span><span class="sxs-lookup"><span data-stu-id="0e911-151">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="0e911-152">Web API 通过 (托管IIS Express) ，以帮助执行身份验证任务，充当应用和 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="0e911-152">A web API is hosted (via IIS Express) to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  
- <span data-ttu-id="0e911-153">生成应用清单，存在于 Teams 开发人员门户中。</span><span class="sxs-lookup"><span data-stu-id="0e911-153">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="0e911-154">Teams 使用应用清单告诉已连接客户端从何处加载应用。</span><span class="sxs-lookup"><span data-stu-id="0e911-154">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="0e911-155">完成后，可在 Teams 客户端中加载该应用。</span><span class="sxs-lookup"><span data-stu-id="0e911-155">Once this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="0e911-156">我们使用 Teams Web 客户端，以便可以在标准 Web 开发环境中查看 HTML、CSS 和 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="0e911-156">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

<span data-ttu-id="0e911-157">若要在本地构建并运行应用程序:</span><span class="sxs-lookup"><span data-stu-id="0e911-157">To build and run your app locally:</span></span>

1. <span data-ttu-id="0e911-158">在Visual Studio中，按 **F5** 以在调试模式下运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="0e911-158">From Visual Studio, press **F5** to run your application in debug mode.</span></span>

1. <span data-ttu-id="0e911-159">如果需要，请安装自签名 SSL 证书进行本地调试。</span><span class="sxs-lookup"><span data-stu-id="0e911-159">If requested, install the self-signed SSL certificate for local debugging.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="显示如何安装 SSL 证书以便 Teams 从 localhost 加载应用程序提示的屏幕截图。":::

1. <span data-ttu-id="0e911-161">将在 Web 浏览器中加载 Teams，并提示进行登录。</span><span class="sxs-lookup"><span data-stu-id="0e911-161">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="0e911-162">如果系统提示打开 Microsoft Teams，请选择"取消"以保留在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="0e911-162">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="0e911-163">使用 M365 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="0e911-163">Sign in with your M365 account.</span></span>
1. <span data-ttu-id="0e911-164">系统提示将应用安装到 Teams 时，按 **添加**。</span><span class="sxs-lookup"><span data-stu-id="0e911-164">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="0e911-165">此时将显示应用：</span><span class="sxs-lookup"><span data-stu-id="0e911-165">Your app will now be displayed:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="已完成应用的屏幕截图":::

<span data-ttu-id="0e911-167">你可以像调试任何其他 Web 应用程序一样执行正常调试活动（例如设置断点）。</span><span class="sxs-lookup"><span data-stu-id="0e911-167">You can do normal debugging activities as if this were any other web application (such as setting breakpoints).</span></span> <span data-ttu-id="0e911-168">该应用支持热重新加载。</span><span class="sxs-lookup"><span data-stu-id="0e911-168">The app supports hot reloading.</span></span>  <span data-ttu-id="0e911-169">如果更改了项目内的任何文件，将重新加载页面。</span><span class="sxs-lookup"><span data-stu-id="0e911-169">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="0e911-170">在调试器中本地运行应用时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="0e911-170">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="0e911-171">按 F5 时，Teams 工具包:</span><span class="sxs-lookup"><span data-stu-id="0e911-171">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="0e911-172">使用 Azure Active Directory 注册应用程序。</span><span class="sxs-lookup"><span data-stu-id="0e911-172">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="0e911-173">在 Microsoft Teams 中将你的应用程序注册为“旁加载”。</span><span class="sxs-lookup"><span data-stu-id="0e911-173">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="0e911-174">在本地启动应用程序后端运行。</span><span class="sxs-lookup"><span data-stu-id="0e911-174">Started your application backend running locally.</span></span>
1. <span data-ttu-id="0e911-175">启动应用程序本地托管的前端。</span><span class="sxs-lookup"><span data-stu-id="0e911-175">Started your application front-end hosted locally.</span></span>
1. <span data-ttu-id="0e911-176">已Microsoft Teams Web 浏览器中使用命令启动，以指示Teams在应用程序清单 (中注册 URL 时旁加载) 。</span><span class="sxs-lookup"><span data-stu-id="0e911-176">Started Microsoft Teams in a web browser with a command to instruct Teams to side load the application (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="0e911-177">了解如何在本地运行应用时解决常见问题。</span><span class="sxs-lookup"><span data-stu-id="0e911-177">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="0e911-178">若要在应用中成功运行Teams，你必须拥有一个Microsoft 365支持应用旁加载的一个开发帐户。</span><span class="sxs-lookup"><span data-stu-id="0e911-178">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app side loading.</span></span> <span data-ttu-id="0e911-179">有关开设帐户的详细信息，请参阅 [先决条件](prerequisites.md#enable-sideloading)。</span><span class="sxs-lookup"><span data-stu-id="0e911-179">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="0e911-180">将应用部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="0e911-180">Deploy your app to Azure</span></span>

<span data-ttu-id="0e911-181">部署包含两个步骤。</span><span class="sxs-lookup"><span data-stu-id="0e911-181">Deployment consists of two steps.</span></span>  <span data-ttu-id="0e911-182">首先，创建必要的云 (也称为预配) ，然后将应用的代码复制到已创建的云资源中。</span><span class="sxs-lookup"><span data-stu-id="0e911-182">First, necessary cloud resources are created (also known as provisioning), then the code that makes up your app is copied into the created cloud resources.</span></span>

> <span data-ttu-id="0e911-183">**预览**</span><span class="sxs-lookup"><span data-stu-id="0e911-183">**PREVIEW**</span></span>
>
> <span data-ttu-id="0e911-184">对 Blazor 应用的支持是 Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="0e911-184">Support for Blazor apps is new in Teams Toolkit.</span></span>  <span data-ttu-id="0e911-185">设置和部署是结合 Visual Studio 2019 和开发人员门户Teams。</span><span class="sxs-lookup"><span data-stu-id="0e911-185">Provisioning and deployment are done with a combination of Visual Studio 2019 and the Developer Portal for Teams.</span></span>

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a><span data-ttu-id="0e911-186">预配应用并部署到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="0e911-186">Provision and deploy your app to Azure App Service</span></span>

1. <span data-ttu-id="0e911-187">在"解决方案资源管理器"中，右键单击项目节点并选择"发布 (或使用"生成发布"  >  菜单项) 。</span><span class="sxs-lookup"><span data-stu-id="0e911-187">In Solution Explorer, right-click the project node and choose **Publish** (or use the **Build** > **Publish** menu item).</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="选择项目的&quot;发布&quot;操作":::

1. <span data-ttu-id="0e911-189">在"**发布"** 窗口中，选择 **"Azure"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-189">In the **Publish** window, select **Azure**.</span></span>  <span data-ttu-id="0e911-190">按 **"下一步"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-190">Press **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="选择 Azure 作为发布目标":::

1. <span data-ttu-id="0e911-192">选择 **"Azure 应用服务 (Windows) "。**</span><span class="sxs-lookup"><span data-stu-id="0e911-192">Select **Azure App Service (Windows)**.</span></span>  <span data-ttu-id="0e911-193">按 **"下一步"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-193">Press **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="选择 Azure 应用服务作为发布目标":::

1. <span data-ttu-id="0e911-195">选择 **+** 以创建新的应用服务实例。</span><span class="sxs-lookup"><span data-stu-id="0e911-195">Select **+** to create a new App Service instance.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="创建新实例。":::

1. <span data-ttu-id="0e911-197">在"**创建应用服务 (Windows)** 对话框中，将填充"名称"、"订阅名称"、"资源组"和"**托管** 计划"条目字段。 </span><span class="sxs-lookup"><span data-stu-id="0e911-197">In the **Create App Service (Windows)** dialog, the **Name**, **Subscription name**, **Resource Group**, and **Hosting Plan** entry fields are populated.</span></span> <span data-ttu-id="0e911-198">如果已运行应用服务，则选择现有设置。</span><span class="sxs-lookup"><span data-stu-id="0e911-198">If you have already got an App Service running, existing settings will be selected.</span></span>  <span data-ttu-id="0e911-199">你可以选择创建新的资源组和托管计划 (推荐) 。</span><span class="sxs-lookup"><span data-stu-id="0e911-199">You can opt to create a new resource group and hosting plan (Recommended).</span></span>  <span data-ttu-id="0e911-200">准备就绪后，选择"创建 **"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-200">When ready, select **Create**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="选择托管计划和订阅":::

1. <span data-ttu-id="0e911-202">在 **"发布** "对话框中，已自动选择新创建的实例。</span><span class="sxs-lookup"><span data-stu-id="0e911-202">In the **Publish** dialog, the newly created instance has been automatically selected.</span></span>  <span data-ttu-id="0e911-203">准备就绪后，选择"**完成"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-203">When ready, select **Finish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="选择新实例。":::

1. <span data-ttu-id="0e911-205">按"**部署** (旁边的) "铅笔图标 **，** 然后选择"**自包含"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-205">Press the **Edit** (pencil) icon next to **Deployment Mode**, then select **Self-contained**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="选择自包含部署模式。":::

1. <span data-ttu-id="0e911-207">选择“**发布**”。</span><span class="sxs-lookup"><span data-stu-id="0e911-207">Select **Publish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="将应用发布到应用服务":::

<span data-ttu-id="0e911-209">Visual Studio将应用部署到 Azure 应用服务，并且 Web 应用在浏览器中加载。</span><span class="sxs-lookup"><span data-stu-id="0e911-209">Visual Studio deploys the app to your Azure App Service, and the web app loads in your browser.</span></span>  <span data-ttu-id="0e911-210">添加到 `/tab` URL 的末尾以查看你的页面。</span><span class="sxs-lookup"><span data-stu-id="0e911-210">Add `/tab` to the end of the URL to see your page.</span></span>

<span data-ttu-id="0e911-211">"项目属性 **发布** "窗格显示网站 URL 和其他详细信息。</span><span class="sxs-lookup"><span data-stu-id="0e911-211">The project properties **Publish** pane shows the site URL and other details.</span></span> <span data-ttu-id="0e911-212">记下网站 URL。</span><span class="sxs-lookup"><span data-stu-id="0e911-212">Make a note of the site URL.</span></span>

## <a name="create-an-environment-for-your-app"></a><span data-ttu-id="0e911-213">为应用创建环境</span><span class="sxs-lookup"><span data-stu-id="0e911-213">Create an environment for your app</span></span>

<span data-ttu-id="0e911-214">开发人员门户的 Teams管理使用 Environment 加载应用的选项卡 **位置**。</span><span class="sxs-lookup"><span data-stu-id="0e911-214">The Developer Portal for Teams manages where the tabs for your app are loaded from with an **Environment**.</span></span>  <span data-ttu-id="0e911-215">创建环境：</span><span class="sxs-lookup"><span data-stu-id="0e911-215">To create an environment:</span></span>

1. <span data-ttu-id="0e911-216">打开[开发人员门户，Teams。](https://dev.teams.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="0e911-216">Open the [Developer Portal for Teams](https://dev.teams.microsoft.com).</span></span>  <span data-ttu-id="0e911-217">使用 M365 管理帐户登录。</span><span class="sxs-lookup"><span data-stu-id="0e911-217">Sign in with your M365 administrative account.</span></span>

1. <span data-ttu-id="0e911-218">从边栏中，**选择应用。**</span><span class="sxs-lookup"><span data-stu-id="0e911-218">From the sidebar, select **Apps**.</span></span>

1. <span data-ttu-id="0e911-219">如果只有一个应用，将自动选择它。</span><span class="sxs-lookup"><span data-stu-id="0e911-219">If you only have one app, it will be automatically selected.</span></span>  <span data-ttu-id="0e911-220">如果没有，请从列表中选择你的应用。</span><span class="sxs-lookup"><span data-stu-id="0e911-220">If not, select your app from the list.</span></span>

1. <span data-ttu-id="0e911-221">选择 **"环境"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-221">Select **Environments**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="选择环境":::

1. <span data-ttu-id="0e911-223">选择 **"创建你的第一个环境"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-223">Select **Create your first environment**.</span></span>

1. <span data-ttu-id="0e911-224">输入环境名称，然后按"添加 **";** 例如 _生产_。</span><span class="sxs-lookup"><span data-stu-id="0e911-224">Enter a name for your environment, then press **Add**; for example _Production_.</span></span>

1. <span data-ttu-id="0e911-225">选择新创建的环境后，按 **"创建第一个环境变量"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-225">With the newly created environment selected, press **Create your first environment variable**.</span></span>

1. <span data-ttu-id="0e911-226">输入 `azure_app_url` 名称。</span><span class="sxs-lookup"><span data-stu-id="0e911-226">Enter `azure_app_url` for the **Name**.</span></span>  <span data-ttu-id="0e911-227">输入 Azure 站点 URL (，) `https://` 值 。 </span><span class="sxs-lookup"><span data-stu-id="0e911-227">Enter your Azure site URL (without the `https://`) as the **Value**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="创建环境变量":::

   <span data-ttu-id="0e911-229">按 **"添加"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-229">Press **Add**.</span></span>

## <a name="update-the-app-manifest"></a><span data-ttu-id="0e911-230">更新应用清单</span><span class="sxs-lookup"><span data-stu-id="0e911-230">Update the app manifest</span></span>

<span data-ttu-id="0e911-231">应用清单正在从 URL 加载 `localhost` 选项卡。</span><span class="sxs-lookup"><span data-stu-id="0e911-231">The app manifest is loading the tab from a `localhost` URL.</span></span>  <span data-ttu-id="0e911-232">在此部分中，你将调整应用清单，以从刚创建的环境中列出的 URL 加载选项卡。</span><span class="sxs-lookup"><span data-stu-id="0e911-232">In this section, you will adjust the app manifest to load the tab from the URL listed within the environment you just created.</span></span>

1. <span data-ttu-id="0e911-233">从边栏中，选择 **"基本信息"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-233">From the sidebar, select **Basic information**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="选择基本信息":::

1. <span data-ttu-id="0e911-235">清单中有几个位置将 列出为 `localhost:XXXXX` URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="0e911-235">There are several places within the manifest that list a `localhost:XXXXX` as part of a URL.</span></span>  <span data-ttu-id="0e911-236">将出现的所有事件 `{{azure_app_url}}` 替换为 (括号，包括大括号) 。</span><span class="sxs-lookup"><span data-stu-id="0e911-236">Replace all occurrences with `{{azure_app_url}}` (including the curly braces).</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="调整环境的基本信息":::

1. <span data-ttu-id="0e911-238">完成后，按"保存 **"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-238">When complete, press **Save**.</span></span>

1. <span data-ttu-id="0e911-239">从边栏中，选择 **"功能"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-239">From the sidebar, select **Capabilities**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="选择功能":::

1. <span data-ttu-id="0e911-241">选择 **"个人"选项卡**。</span><span class="sxs-lookup"><span data-stu-id="0e911-241">Select **Personal Tab**.</span></span>
1. <span data-ttu-id="0e911-242">在"个人 **"选项卡旁边**，选择三个点，然后选择"编辑 **"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-242">Next to the **Personal Tab**, select the triple dots, then select **Edit**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="编辑个人选项卡设置":::

1. <span data-ttu-id="0e911-244">将 URL 替换为"内容 Url"和"网站 **Url"** 字段中 **的环境** 变量。</span><span class="sxs-lookup"><span data-stu-id="0e911-244">Replace the URL with the environment variable within the **Content Url** and **Website Url** fields.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="编辑个人选项卡 URL":::

1. <span data-ttu-id="0e911-246">按 **"更新"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-246">Press **Update**.</span></span>

1. <span data-ttu-id="0e911-247">按“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="0e911-247">Press **Save**.</span></span>

1. <span data-ttu-id="0e911-248">从边栏中，选择 **"单一登录"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-248">From the sidebar, select **Single Sign-On**.</span></span>

1. <span data-ttu-id="0e911-249">将 `localhost` 应用程序 **ID URI 中的** 替换为 `{{azure_app_url}}` 。</span><span class="sxs-lookup"><span data-stu-id="0e911-249">Replace the `localhost` within the **Application ID URI** with `{{azure_app_url}}`.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="编辑单一登录应用程序 ID URI":::

1. <span data-ttu-id="0e911-251">按“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="0e911-251">Press **Save**.</span></span>

1. <span data-ttu-id="0e911-252">在边栏中，按 **"域"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-252">From the sidebar, press **Domains**.</span></span>

1. <span data-ttu-id="0e911-253">按 **"添加域"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-253">Press **Add a domain**.</span></span>

1. <span data-ttu-id="0e911-254">如果未 `{{azure_app_url}}` 列为有效域，请将其添加为有效域，然后按 **"添加"。**</span><span class="sxs-lookup"><span data-stu-id="0e911-254">If `{{azure_app_url}}` is not listed as a valid domain, add it as a valid domain, then press **Add**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="添加域":::

<span data-ttu-id="0e911-256">现在，可以使用页面顶部的"Teams预览"按钮在应用中启动Teams。</span><span class="sxs-lookup"><span data-stu-id="0e911-256">You can now use the **Preview in Teams** button at the top of the page to launch your app within Teams.</span></span>

## <a name="see-also"></a><span data-ttu-id="0e911-257">另请参阅</span><span class="sxs-lookup"><span data-stu-id="0e911-257">See also</span></span>

- [<span data-ttu-id="0e911-258">使用 React 创建 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="0e911-258">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="0e911-259">创建Teams应用作为SharePoint Web 部件</span><span class="sxs-lookup"><span data-stu-id="0e911-259">Create a Teams app as a SharePoint Web Part</span></span>](first-app-spfx.md)
- [<span data-ttu-id="0e911-260">创建对话机器人应用</span><span class="sxs-lookup"><span data-stu-id="0e911-260">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="0e911-261">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="0e911-261">Create a messaging extension</span></span>](first-message-extension.md)

## <a name="next-step"></a><span data-ttu-id="0e911-262">后续步骤</span><span class="sxs-lookup"><span data-stu-id="0e911-262">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="0e911-263">创建Teams应用作为SharePoint Web 部件</span><span class="sxs-lookup"><span data-stu-id="0e911-263">Create a Teams app as a SharePoint Web Part</span></span>](first-app-spfx.md)
