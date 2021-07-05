---
title: 入门 - 使用 Blazor 生成Teams应用程序
author: adrianhall
description: 快速创建显示"Hello，World！"的 Microsoft Teams 应用。 message using the Microsoft Teams Toolkit and .NET Blazor.
ms.author: adhal
ms.date: 04/27/2021
ms.topic: quickstart
ms.openlocfilehash: c14f55d014af120cab88044d31ee8600017e3c57
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254305"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-blazor"></a><span data-ttu-id="f20e4-104">使用 Blazor 生成Microsoft Teams应用程序</span><span class="sxs-lookup"><span data-stu-id="f20e4-104">Build and run your first Microsoft Teams app with Blazor</span></span>

<span data-ttu-id="f20e4-105">本教程介绍如何在 .NET/Blazor 中创建新的 Microsoft Teams 应用，该应用实现简单的个人应用，以从 Microsoft Graph。</span><span class="sxs-lookup"><span data-stu-id="f20e4-105">In this tutorial, you will learn how to create a new Microsoft Teams app in .NET/Blazor that implements a simple personal app to pull information from the Microsoft Graph.</span></span> <span data-ttu-id="f20e4-106">例如，个人 *应用包括* 一组供个人使用的选项卡。</span><span class="sxs-lookup"><span data-stu-id="f20e4-106">For example, a *personal app* includes a set of tabs for individual use.</span></span> <span data-ttu-id="f20e4-107">在本教程中，你将了解 Teams 应用的结构、如何在本地运行应用以及如何将应用部署到 Azure。</span><span class="sxs-lookup"><span data-stu-id="f20e4-107">During the tutorial, you will learn about the structure of a Teams app, how to run an app locally, and how to deploy the app to Azure.</span></span>

<span data-ttu-id="f20e4-108">构建的应用将显示当前用户的基本用户信息。</span><span class="sxs-lookup"><span data-stu-id="f20e4-108">The app that is built displays basic user information for the current user.</span></span>  <span data-ttu-id="f20e4-109">授予权限后，应用会作为当前用户连接到 Microsoft Graph 以获取完整配置文件。</span><span class="sxs-lookup"><span data-stu-id="f20e4-109">When permission is granted, the app will connect to the Microsoft Graph as the current user to get the complete profile.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="f20e4-110">准备工作</span><span class="sxs-lookup"><span data-stu-id="f20e4-110">Before you begin</span></span>

<span data-ttu-id="f20e4-111">请确保通过安装必备组件来设置开发环境。</span><span class="sxs-lookup"><span data-stu-id="f20e4-111">Make sure your development environment is set up by installing the prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f20e4-112">安装先决条件</span><span class="sxs-lookup"><span data-stu-id="f20e4-112">Install prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="f20e4-113">创建项目</span><span class="sxs-lookup"><span data-stu-id="f20e4-113">Create your project</span></span>

<span data-ttu-id="f20e4-114">使用 Teams 工具包创建你的第一个项目:</span><span class="sxs-lookup"><span data-stu-id="f20e4-114">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="f20e4-115">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="f20e4-115">Visual Studio 2019</span></span>](#tab/vs)

1. <span data-ttu-id="f20e4-116">打开Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="f20e4-116">Open Visual Studio 2019.</span></span>

1. <span data-ttu-id="f20e4-117">选择 **创建新项目**。</span><span class="sxs-lookup"><span data-stu-id="f20e4-117">Select **Create a new project**.</span></span>

1. <span data-ttu-id="f20e4-118">选择 **Microsoft Teams应用"，** 然后选择"下一 **步"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-118">Select **Microsoft Teams App**, then select **Next**.</span></span>  <span data-ttu-id="f20e4-119">若要帮助您查找模板，请使用项目类型 **Microsoft Teams**。</span><span class="sxs-lookup"><span data-stu-id="f20e4-119">To help you find the template, use the project type **Microsoft Teams**.</span></span>

1. <span data-ttu-id="f20e4-120">输入名称，然后选择下一 **步**。</span><span class="sxs-lookup"><span data-stu-id="f20e4-120">Enter a name and select **Next**.</span></span>

1. <span data-ttu-id="f20e4-121">输入应用程序名称和公司名称。</span><span class="sxs-lookup"><span data-stu-id="f20e4-121">Enter the application name and company name.</span></span>

1. <span data-ttu-id="f20e4-122">选择“创建”。</span><span class="sxs-lookup"><span data-stu-id="f20e4-122">Select **Create**.</span></span>  <span data-ttu-id="f20e4-123">应用程序名称和公司名称将显示给最终用户。</span><span class="sxs-lookup"><span data-stu-id="f20e4-123">The application name and company name are displayed to your end users.</span></span> <span data-ttu-id="f20e4-124">将在数秒钟内创建你的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="f20e4-124">Your Teams app will be created within a few seconds.</span></span>  <span data-ttu-id="f20e4-125">创建项目后，使用 M365 设置单一登录：</span><span class="sxs-lookup"><span data-stu-id="f20e4-125">After the project is created, set up single sign-on with M365:</span></span>

   1. <span data-ttu-id="f20e4-126">选择 **Project**  >  **TeamsFx**  >  **配置 SSO..."。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-126">Select **Project** > **TeamsFx** > **Configure for SSO...**.</span></span>
   1. <span data-ttu-id="f20e4-127">系统提示时，登录到 M365 管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="f20e4-127">When prompted, sign in to your M365 administrator account.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="f20e4-128">命令行</span><span class="sxs-lookup"><span data-stu-id="f20e4-128">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="f20e4-129">打开终端并选择你希望创建项目的目录。</span><span class="sxs-lookup"><span data-stu-id="f20e4-129">Open a Terminal and select the directory where you wish to create the project.</span></span>

1. <span data-ttu-id="f20e4-130">运行 `dotnet new -i` 以从以下位置安装NuGet：</span><span class="sxs-lookup"><span data-stu-id="f20e4-130">Run `dotnet new -i` to install the template from NuGet:</span></span>

   ``` bash
   dotnet new --install Microsoft.TeamsFx.VisualStudio.ProjectTemplates::0.1.43-beta
   ```

   <span data-ttu-id="f20e4-131">你只需在首次或更新模板时这样做。</span><span class="sxs-lookup"><span data-stu-id="f20e4-131">You only need to do this the first time or when updating the template.</span></span> <span data-ttu-id="f20e4-132">检查[NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/)程序包的最新版本。</span><span class="sxs-lookup"><span data-stu-id="f20e4-132">Check [NuGet](https://www.nuget.org/packages/Microsoft.TeamsFx.VisualStudio.ProjectTemplates/) for the latest version of this package.</span></span>

1. <span data-ttu-id="f20e4-133">创建目录：</span><span class="sxs-lookup"><span data-stu-id="f20e4-133">Create a directory:</span></span>

   ``` bash
   mkdir helloworld
   ```

1. <span data-ttu-id="f20e4-134">运行 `dotnet new` 以创建新项目：</span><span class="sxs-lookup"><span data-stu-id="f20e4-134">Run `dotnet new` to create a new project:</span></span>

   ``` bash
   dotnet new teamsapp --shortName my-teams-app --companyName "My Company"
   ```

1. <span data-ttu-id="f20e4-135">搭建基架后，配置用于部署Teams项目：</span><span class="sxs-lookup"><span data-stu-id="f20e4-135">After scaffolding, configure the project for Teams deployment:</span></span>

   ``` bash
   teamsfx init
   ```

   <span data-ttu-id="f20e4-136">现在可以在 Visual Studio 中打开解决方案进行调试。</span><span class="sxs-lookup"><span data-stu-id="f20e4-136">You can now open the solution in Visual Studio for debugging.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="f20e4-137">浏览源代码</span><span class="sxs-lookup"><span data-stu-id="f20e4-137">Take a tour of the source code</span></span>

<span data-ttu-id="f20e4-138">若要暂时跳过此部分，可以 [在本地运行应用](#run-your-app-locally)。</span><span class="sxs-lookup"><span data-stu-id="f20e4-138">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="f20e4-139">在Teams Toolkit项目后，你拥有组件来构建基本个人应用Teams。</span><span class="sxs-lookup"><span data-stu-id="f20e4-139">After the Teams Toolkit configures your project, you have the components to build a basic personal app for Teams.</span></span> <span data-ttu-id="f20e4-140">项目目录和文件显示在 2019 年 10 月Visual Studio资源管理器"区域中。</span><span class="sxs-lookup"><span data-stu-id="f20e4-140">The project directories and files display in the Solution Explorer area of Visual Studio 2019.</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/blazor-file-layout.png" alt-text="Screenshot showing app project files for a personal app in Visual Studio 2019.":::

- <span data-ttu-id="f20e4-142">应用图标在 `color.png` 和 `outline.png`中存储为 PNG 文件。</span><span class="sxs-lookup"><span data-stu-id="f20e4-142">The app icons are stored as PNG files in `color.png` and `outline.png`.</span></span>
- <span data-ttu-id="f20e4-143">用于通过开发人员门户发布的应用程序清单Teams存储在 中 `Properties/manifest.json` 。</span><span class="sxs-lookup"><span data-stu-id="f20e4-143">The app manifest for publishing through the Developer Portal for Teams is stored in `Properties/manifest.json`.</span></span>
- <span data-ttu-id="f20e4-144">提供后端控制器以帮助 `Controllers/BackendController.cs` 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="f20e4-144">A backend controller is provided in `Controllers/BackendController.cs` for assisting with authentication.</span></span>

<span data-ttu-id="f20e4-145">由于在设置期间创建了选项卡应用程序，Teams Toolkit将基本选项卡的所有必要代码搭建为[Blazor Server](/aspnet/core/blazor)。</span><span class="sxs-lookup"><span data-stu-id="f20e4-145">Since you created a tab app during setup, the Teams Toolkit scaffolds all the necessary code for a basic tab as a [Blazor Server](/aspnet/core/blazor).</span></span>

- <span data-ttu-id="f20e4-146">`Pages/Tab.razor` 是前端应用程序的入口点。</span><span class="sxs-lookup"><span data-stu-id="f20e4-146">`Pages/Tab.razor` is the front-end application's entry point.</span></span>
- <span data-ttu-id="f20e4-147">`TeamsFx.cs``JS/src/index.js`和 用于初始化与主机Teams通信。</span><span class="sxs-lookup"><span data-stu-id="f20e4-147">`TeamsFx.cs` and `JS/src/index.js` is used for initializing communications with the Teams host.</span></span>

<span data-ttu-id="f20e4-148">可以通过向应用程序添加其他 ASP.NET Core控制器来添加后端功能。</span><span class="sxs-lookup"><span data-stu-id="f20e4-148">You can add backend functionality by adding additional ASP.NET Core controllers to your application.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="f20e4-149">在本地运行应用</span><span class="sxs-lookup"><span data-stu-id="f20e4-149">Run your app locally</span></span>

<span data-ttu-id="f20e4-150">使用 Teams 工具包，你可以在本地运行应用。</span><span class="sxs-lookup"><span data-stu-id="f20e4-150">Teams Toolkit allows you to run your app locally.</span></span>  <span data-ttu-id="f20e4-151">这包含几个部分，是提供 Teams 所需的正确基础结构所必需的：</span><span class="sxs-lookup"><span data-stu-id="f20e4-151">This consists of several parts that are necessary to provide the correct infrastructure that Teams expects:</span></span>

- <span data-ttu-id="f20e4-152">应用程序已注册 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="f20e4-152">An application is registered with Azure Active Directory.</span></span>  <span data-ttu-id="f20e4-153">此应用程序具有与从加载应用的位置及其访问的任何后端资源相关联的权限。</span><span class="sxs-lookup"><span data-stu-id="f20e4-153">This application has permissions associated with the location that the app is loaded from and any backend resources it accesses.</span></span>
- <span data-ttu-id="f20e4-154">Web API 通过 (托管IIS Express) ，以帮助执行身份验证任务，充当应用和 Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="f20e4-154">A web API is hosted (via IIS Express) to assist with authentication tasks, acting as a proxy between the app and Azure Active Directory.</span></span>  
- <span data-ttu-id="f20e4-155">生成应用清单，存在于 Teams 开发人员门户中。</span><span class="sxs-lookup"><span data-stu-id="f20e4-155">An app manifest is generated and exists in the Developer Portal for Teams.</span></span>  <span data-ttu-id="f20e4-156">Teams 使用应用清单告诉已连接客户端从何处加载应用。</span><span class="sxs-lookup"><span data-stu-id="f20e4-156">Teams uses the app manifest to tell connected clients where to load the app from.</span></span>

<span data-ttu-id="f20e4-157">完成此操作后，应用可以在客户端Teams加载。</span><span class="sxs-lookup"><span data-stu-id="f20e4-157">After this is done, the app can be loaded within the Teams client.</span></span>  <span data-ttu-id="f20e4-158">我们使用 Teams Web 客户端，以便可以在标准 Web 开发环境中查看 HTML、CSS 和 JavaScript 代码。</span><span class="sxs-lookup"><span data-stu-id="f20e4-158">We use the Teams web client so that we can see the HTML, CSS, and JavaScript code within a standard web development environment.</span></span>

<span data-ttu-id="f20e4-159">若要在本地构建并运行应用程序:</span><span class="sxs-lookup"><span data-stu-id="f20e4-159">To build and run your app locally:</span></span>


1. <span data-ttu-id="f20e4-160">在Visual Studio Code中，按 **F5** 键以在调试模式下运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="f20e4-160">From Visual Studio Code, press the **F5** key to run your application in debug mode.</span></span>


1. <span data-ttu-id="f20e4-161">如果需要，请安装自签名 SSL 证书进行本地调试。</span><span class="sxs-lookup"><span data-stu-id="f20e4-161">If requested, install the self-signed SSL certificate for local debugging.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="显示如何安装 SSL 证书以便 Teams 从 localhost 加载应用程序提示的屏幕截图。":::

1. <span data-ttu-id="f20e4-163">将在 Web 浏览器中加载 Teams，并提示进行登录。</span><span class="sxs-lookup"><span data-stu-id="f20e4-163">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="f20e4-164">如果系统提示打开 Microsoft Teams，请选择"取消"以保留在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="f20e4-164">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="f20e4-165">使用 M365 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="f20e4-165">Sign in with your M365 account.</span></span>

1. <span data-ttu-id="f20e4-166">当系统提示将应用安装到 Teams 时，选择"添加 **"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-166">When prompted to install the app onto Teams, select **Add**.</span></span>

   <span data-ttu-id="f20e4-167">此时将显示应用：</span><span class="sxs-lookup"><span data-stu-id="f20e4-167">Your app will now be displayed:</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-completed-app.png" alt-text="已完成应用的屏幕截图":::

   <span data-ttu-id="f20e4-169">你可以执行调试活动，就像执行任何其他 Web 应用程序（如设置断点）一样。</span><span class="sxs-lookup"><span data-stu-id="f20e4-169">You can perform the debugging activities as if this were any other web application like setting breakpoints.</span></span> <span data-ttu-id="f20e4-170">该应用支持热重新加载。</span><span class="sxs-lookup"><span data-stu-id="f20e4-170">The app supports hot reloading.</span></span>  <span data-ttu-id="f20e4-171">如果更改了项目内的任何文件，将重新加载页面。</span><span class="sxs-lookup"><span data-stu-id="f20e4-171">If you change any file within the project, the page will be reloaded.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="f20e4-172">在调试器中本地运行应用时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="f20e4-172">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="f20e4-173">按 **F5 键** 时，Teams Toolkit：</span><span class="sxs-lookup"><span data-stu-id="f20e4-173">When you press the **F5** key, the Teams Toolkit:</span></span>

1. <span data-ttu-id="f20e4-174">向应用程序注册Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="f20e4-174">Registers your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="f20e4-175">将应用程序注册为"旁加载"Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="f20e4-175">Registers your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="f20e4-176">在本地运行启动应用程序后端。</span><span class="sxs-lookup"><span data-stu-id="f20e4-176">Starts your application backend running locally.</span></span>
1. <span data-ttu-id="f20e4-177">在本地托管应用程序前端启动。</span><span class="sxs-lookup"><span data-stu-id="f20e4-177">Starts your application front-end hosted locally.</span></span>
1. <span data-ttu-id="f20e4-178">使用Microsoft Teams启动 Web 浏览器中的 url，以指示Teams应用程序旁加载 (URL 在应用程序清单) 。</span><span class="sxs-lookup"><span data-stu-id="f20e4-178">Starts Microsoft Teams in a web browser with a command to instruct Teams to side load the application (the URL is registered inside the application manifest).</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="f20e4-179">了解如何在本地运行应用时解决常见问题。</span><span class="sxs-lookup"><span data-stu-id="f20e4-179">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="f20e4-180">若要在应用中成功运行Teams，你必须拥有一个Microsoft 365支持应用旁加载的一个开发帐户。</span><span class="sxs-lookup"><span data-stu-id="f20e4-180">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app side loading.</span></span> <span data-ttu-id="f20e4-181">有关开设帐户的详细信息，请参阅 [先决条件](prerequisites.md#enable-sideloading)。</span><span class="sxs-lookup"><span data-stu-id="f20e4-181">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

</details>

## <a name="deploy-your-app-to-azure"></a><span data-ttu-id="f20e4-182">将应用部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="f20e4-182">Deploy your app to Azure</span></span>

<span data-ttu-id="f20e4-183">部署包含两个步骤：</span><span class="sxs-lookup"><span data-stu-id="f20e4-183">Deployment consists of two steps:</span></span> 

1. <span data-ttu-id="f20e4-184">创建必要的云资源。</span><span class="sxs-lookup"><span data-stu-id="f20e4-184">Necessary cloud resources are created.</span></span> <span data-ttu-id="f20e4-185">这也称为预配。</span><span class="sxs-lookup"><span data-stu-id="f20e4-185">This is also known as provisioning.</span></span>
1. <span data-ttu-id="f20e4-186">开始编码，将应用复制到已创建的云资源。</span><span class="sxs-lookup"><span data-stu-id="f20e4-186">Start coding and copy your app into the created cloud resources.</span></span>

> <span data-ttu-id="f20e4-187">**预览**</span><span class="sxs-lookup"><span data-stu-id="f20e4-187">**PREVIEW**</span></span>
>
> <span data-ttu-id="f20e4-188">对 Blazor 应用的支持是 Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="f20e4-188">Support for Blazor apps is new in Teams Toolkit.</span></span>  <span data-ttu-id="f20e4-189">设置和部署是结合 Visual Studio 2019 和开发人员门户Teams。</span><span class="sxs-lookup"><span data-stu-id="f20e4-189">Provisioning and deployment are done with a combination of Visual Studio 2019 and the Developer Portal for Teams.</span></span>

## <a name="provision-and-deploy-your-app-to-azure-app-service"></a><span data-ttu-id="f20e4-190">预配应用并部署到 Azure 应用服务</span><span class="sxs-lookup"><span data-stu-id="f20e4-190">Provision and deploy your app to Azure App Service</span></span>

1. <span data-ttu-id="f20e4-191">在"解决方案资源管理器"中，右键单击项目节点并选择"发布 **"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-191">In Solution Explorer, right-click the project node and select **Publish**.</span></span> <span data-ttu-id="f20e4-192">您还可以使用"生成  >  **发布"** 菜单项。</span><span class="sxs-lookup"><span data-stu-id="f20e4-192">You can also use the **Build** > **Publish** menu item.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish1.png" alt-text="选择项目的&quot;发布&quot;操作":::

1. <span data-ttu-id="f20e4-194">在"**发布"** 窗口中，选择 **"Azure"，** 然后选择"下一步 **"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-194">In the **Publish** window, select **Azure** and selct **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish2.png" alt-text="选择 Azure 作为发布目标":::

1. <span data-ttu-id="f20e4-196">选择 **Azure 应用服务 (Windows) ，** 然后选择下一 **步**。</span><span class="sxs-lookup"><span data-stu-id="f20e4-196">Select **Azure App Service (Windows)** and select **Next**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish3.png" alt-text="选择 Azure 应用服务作为发布目标":::

1. <span data-ttu-id="f20e4-198">选择 **+** 以创建新的应用服务实例。</span><span class="sxs-lookup"><span data-stu-id="f20e4-198">Select **+** to create a new App Service instance.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish4.png" alt-text="创建新实例。":::

1. <span data-ttu-id="f20e4-200">在"**创建应用服务 (Windows)** 对话框中，将填充"名称"、"订阅名称"、"资源组"和"**托管** 计划"条目字段。 </span><span class="sxs-lookup"><span data-stu-id="f20e4-200">In the **Create App Service (Windows)** dialog, the **Name**, **Subscription name**, **Resource Group**, and **Hosting Plan** entry fields are populated.</span></span> <span data-ttu-id="f20e4-201">如果已运行应用服务，则选择现有设置。</span><span class="sxs-lookup"><span data-stu-id="f20e4-201">If you have already got an App Service running, existing settings are selected.</span></span>  <span data-ttu-id="f20e4-202">可以选择创建新的资源组和托管计划。</span><span class="sxs-lookup"><span data-stu-id="f20e4-202">You can opt to create a new resource group and hosting plan.</span></span>  <span data-ttu-id="f20e4-203">准备就绪后，选择"创建 **"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-203">When ready, select **Create**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish5.png" alt-text="选择托管计划和订阅":::

1. <span data-ttu-id="f20e4-205">在 **"发布** "对话框中，已自动选择新创建的实例。</span><span class="sxs-lookup"><span data-stu-id="f20e4-205">In the **Publish** dialog, the newly created instance has been automatically selected.</span></span>  <span data-ttu-id="f20e4-206">准备就绪后，选择"**完成"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-206">When ready, select **Finish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish6.png" alt-text="选择新实例。":::

1. <span data-ttu-id="f20e4-208">选择部署 **(** 旁边的 **) "编辑** 铅笔图标"，然后选择"**自包含"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-208">Select the **Edit** (pencil) icon next to **Deployment Mode**, and select **Self-contained**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish8.png" alt-text="选择自包含部署模式。":::

1. <span data-ttu-id="f20e4-210">选择“**发布**”。</span><span class="sxs-lookup"><span data-stu-id="f20e4-210">Select **Publish**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/blazor-vs2019-publish7.png" alt-text="将应用发布到应用服务":::

   <span data-ttu-id="f20e4-212">Visual Studio将应用部署到 Azure 应用服务，并且 Web 应用在浏览器中加载。</span><span class="sxs-lookup"><span data-stu-id="f20e4-212">Visual Studio deploys the app to your Azure App Service, and the web app loads in your browser.</span></span>  <span data-ttu-id="f20e4-213">添加到 `/tab` URL 的末尾以查看你的页面。</span><span class="sxs-lookup"><span data-stu-id="f20e4-213">Add `/tab` to the end of the URL to see your page.</span></span>

   <span data-ttu-id="f20e4-214">"项目属性 **发布** "窗格显示网站 URL 和其他详细信息。</span><span class="sxs-lookup"><span data-stu-id="f20e4-214">The project properties **Publish** pane shows the site URL and other details.</span></span> <span data-ttu-id="f20e4-215">记下网站 URL。</span><span class="sxs-lookup"><span data-stu-id="f20e4-215">Make a note of the site URL.</span></span>

## <a name="create-an-environment-for-your-app"></a><span data-ttu-id="f20e4-216">为应用创建环境</span><span class="sxs-lookup"><span data-stu-id="f20e4-216">Create an environment for your app</span></span>

<span data-ttu-id="f20e4-217">开发人员门户的 Teams管理使用 Environment 加载应用的选项卡 **位置**。</span><span class="sxs-lookup"><span data-stu-id="f20e4-217">The Developer Portal for Teams manages where the tabs for your app are loaded from with an **Environment**.</span></span>  

<span data-ttu-id="f20e4-218">**创建环境：**</span><span class="sxs-lookup"><span data-stu-id="f20e4-218">**To create an environment:**</span></span>

1. <span data-ttu-id="f20e4-219">打开[开发人员门户，Teams。](https://dev.teams.microsoft.com)</span><span class="sxs-lookup"><span data-stu-id="f20e4-219">Open the [Developer Portal for Teams](https://dev.teams.microsoft.com).</span></span>  <span data-ttu-id="f20e4-220">使用 M365 管理帐户登录。</span><span class="sxs-lookup"><span data-stu-id="f20e4-220">Sign in with your M365 administrative account.</span></span>

1. <span data-ttu-id="f20e4-221">从边栏中，**选择应用。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-221">From the sidebar, select **Apps**.</span></span>

1. <span data-ttu-id="f20e4-222">如果只有一个应用，将自动选择它。</span><span class="sxs-lookup"><span data-stu-id="f20e4-222">If you only have one app, it will be automatically selected.</span></span>  <span data-ttu-id="f20e4-223">如果没有，请从列表中选择你的应用。</span><span class="sxs-lookup"><span data-stu-id="f20e4-223">If not, select your app from the list.</span></span>

1. <span data-ttu-id="f20e4-224">选择 **"环境"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-224">Select **Environments**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments1.png" alt-text="选择环境":::

1. <span data-ttu-id="f20e4-226">选择 **"创建你的第一个环境"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-226">Select **Create your first environment**.</span></span>

1. <span data-ttu-id="f20e4-227">输入你的环境的名称， **然后选择添加**。</span><span class="sxs-lookup"><span data-stu-id="f20e4-227">Enter a name for your environment and select **Add**.</span></span> <span data-ttu-id="f20e4-228">例如，`_Production_`。</span><span class="sxs-lookup"><span data-stu-id="f20e4-228">For example, `_Production_`.</span></span>

1. <span data-ttu-id="f20e4-229">选择 **"创建第一个环境变量"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-229">Select **Create your first environment variable**.</span></span>

1. <span data-ttu-id="f20e4-230">输入 `azure_app_url` 名称。</span><span class="sxs-lookup"><span data-stu-id="f20e4-230">Enter `azure_app_url` for the **Name**.</span></span>  <span data-ttu-id="f20e4-231">输入 Azure 网站 URL，但不带 `https://` 值 。 </span><span class="sxs-lookup"><span data-stu-id="f20e4-231">Enter your Azure site URL without the `https://` as the **Value**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments2.png" alt-text="创建环境变量":::

   <span data-ttu-id="f20e4-233">按 **"添加"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-233">Press **Add**.</span></span>

## <a name="update-the-app-manifest"></a><span data-ttu-id="f20e4-234">更新应用清单</span><span class="sxs-lookup"><span data-stu-id="f20e4-234">Update the app manifest</span></span>

<span data-ttu-id="f20e4-235">应用清单从 URL 加载 `localhost` 选项卡。</span><span class="sxs-lookup"><span data-stu-id="f20e4-235">The app manifest loads the tab from a `localhost` URL.</span></span>  <span data-ttu-id="f20e4-236">在此部分中，你将配置应用清单，以从刚创建的环境中列出的 URL 加载选项卡。</span><span class="sxs-lookup"><span data-stu-id="f20e4-236">In this section, you will configure the app manifest to load the tab from the URL listed within the environment you just created.</span></span>

1. <span data-ttu-id="f20e4-237">从边栏中，选择 **"基本信息"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-237">From the sidebar, select **Basic information**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments3.png" alt-text="选择基本信息":::

1. <span data-ttu-id="f20e4-239">清单中有几个位置将 列出为 `locahost:XXXXX` URL 的一部分。</span><span class="sxs-lookup"><span data-stu-id="f20e4-239">There are several places within the manifest that list a `locahost:XXXXX` as part of a URL.</span></span>  <span data-ttu-id="f20e4-240">将所有匹配项替换为 `{{azure_app_url}}` ，包括大括号。</span><span class="sxs-lookup"><span data-stu-id="f20e4-240">Replace all occurrences with `{{azure_app_url}}`, including the curly braces.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments4.png" alt-text="调整环境的基本信息":::

1. <span data-ttu-id="f20e4-242">完成后，**选择保存。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-242">When complete, select **Save**.</span></span>

1. <span data-ttu-id="f20e4-243">从边栏中，选择 **"功能"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-243">From the sidebar, select **Capabilities**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments5.png" alt-text="选择功能":::

1. <span data-ttu-id="f20e4-245">选择 **"个人"选项卡**。</span><span class="sxs-lookup"><span data-stu-id="f20e4-245">Select **Personal Tab**.</span></span>
1. <span data-ttu-id="f20e4-246">在"个人 **"选项卡旁边**，选择三个点，然后选择"编辑 **"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-246">Next to the **Personal Tab**, select the triple dots, then select **Edit**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments6.png" alt-text="编辑个人选项卡设置":::

1. <span data-ttu-id="f20e4-248">将 URL 替换为"内容 Url"和"网站 **Url"** 字段中 **的环境** 变量。</span><span class="sxs-lookup"><span data-stu-id="f20e4-248">Replace the URL with the environment variable within the **Content Url** and **Website Url** fields.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments7.png" alt-text="编辑个人选项卡 URL":::

1. <span data-ttu-id="f20e4-250">选择 **“更新”**。</span><span class="sxs-lookup"><span data-stu-id="f20e4-250">Select **Update**.</span></span>

1. <span data-ttu-id="f20e4-251">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="f20e4-251">Select **Save**.</span></span>

1. <span data-ttu-id="f20e4-252">从边栏中，选择 **"单一登录"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-252">From the sidebar, select **Single Sign-On**.</span></span>

1. <span data-ttu-id="f20e4-253">将 `localhost` 应用程序 **ID URI 中的** 替换为 `{{azure_app_url}}` 。</span><span class="sxs-lookup"><span data-stu-id="f20e4-253">Replace the `localhost` within the **Application ID URI** with `{{azure_app_url}}`.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments8.png" alt-text="编辑单一登录应用程序 ID URI":::

1. <span data-ttu-id="f20e4-255">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="f20e4-255">Select **Save**.</span></span>

1. <span data-ttu-id="f20e4-256">从边栏中， **选择域**。</span><span class="sxs-lookup"><span data-stu-id="f20e4-256">From the sidebar, select **Domains**.</span></span>

1. <span data-ttu-id="f20e4-257">选择“**添加域**”。</span><span class="sxs-lookup"><span data-stu-id="f20e4-257">Select **Add a domain**.</span></span>

1. <span data-ttu-id="f20e4-258">如果未 `{{azure_app_url}}` 列为有效域，请将其添加为有效域，然后选择"添加 **"。**</span><span class="sxs-lookup"><span data-stu-id="f20e4-258">If `{{azure_app_url}}` is not listed as a valid domain, add it as a valid domain, then select **Add**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/devcenter-environments9.png" alt-text="添加域":::

   <span data-ttu-id="f20e4-260">现在，可以使用页面顶部的"Teams预览"选项在应用中启动Teams。</span><span class="sxs-lookup"><span data-stu-id="f20e4-260">You can now use the **Preview in Teams** option at the top of the page to launch your app within Teams.</span></span>

## <a name="see-also"></a><span data-ttu-id="f20e4-261">另请参阅</span><span class="sxs-lookup"><span data-stu-id="f20e4-261">See also</span></span>

* [<span data-ttu-id="f20e4-262">教程概述</span><span class="sxs-lookup"><span data-stu-id="f20e4-262">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="f20e4-263">创建对话机器人应用</span><span class="sxs-lookup"><span data-stu-id="f20e4-263">Create a conversational bot app</span></span>](first-app-bot.md)
* [<span data-ttu-id="f20e4-264">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="f20e4-264">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="f20e4-265">代码示例</span><span class="sxs-lookup"><span data-stu-id="f20e4-265">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)
