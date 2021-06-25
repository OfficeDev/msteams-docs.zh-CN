---
title: 教程 - 使用 C 创建第一个应用#
description: 了解如何开始使用 Microsoft Teams 或 .NET C#应用程序。
keywords: 入门 .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 58e11312e61124bf09fcb55d2bcd0fc475e75a49
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114609"
---
# <a name="build-your-first-teams-app-using-c"></a><span data-ttu-id="8d49d-104">使用 C 生成Teams应用#</span><span class="sxs-lookup"><span data-stu-id="8d49d-104">Build your first Teams app using C#</span></span>

<span data-ttu-id="8d49d-105">本教程介绍如何使用 .NET 或 Microsoft Teams 生成首个 C#。</span><span class="sxs-lookup"><span data-stu-id="8d49d-105">In this tutorial, you will learn how to build your very first Microsoft Teams app using .NET or C#.</span></span> <span data-ttu-id="8d49d-106">它还将引导你完成以下步骤：</span><span class="sxs-lookup"><span data-stu-id="8d49d-106">It also walks you through the steps to:</span></span>

1. [<span data-ttu-id="8d49d-107">准备环境</span><span class="sxs-lookup"><span data-stu-id="8d49d-107">Prepare your environment</span></span>](#prepare-your-environment)
1. [<span data-ttu-id="8d49d-108">获取先决条件</span><span class="sxs-lookup"><span data-stu-id="8d49d-108">Get prerequisites</span></span>](#GetPrerequisites)
1. [<span data-ttu-id="8d49d-109">下载示例</span><span class="sxs-lookup"><span data-stu-id="8d49d-109">Download the sample</span></span>](#DownloadSample)
1. [<span data-ttu-id="8d49d-110">生成和运行示例</span><span class="sxs-lookup"><span data-stu-id="8d49d-110">Build and run the sample</span></span>](#BuildRun)
1. [<span data-ttu-id="8d49d-111">托管示例应用</span><span class="sxs-lookup"><span data-stu-id="8d49d-111">Host the sample app</span></span>](#hostsample)
1. [<span data-ttu-id="8d49d-112">更新托管应用的凭据</span><span class="sxs-lookup"><span data-stu-id="8d49d-112">Update the credentials for your hosted app</span></span>](#updatecredentials)
1. [<span data-ttu-id="8d49d-113">配置"应用"选项卡</span><span class="sxs-lookup"><span data-stu-id="8d49d-113">Configure the app tab</span></span>](#configureapptab)

<a name="prepare-your-environment"></a>
[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="8d49d-114">获取先决条件</span><span class="sxs-lookup"><span data-stu-id="8d49d-114">Get prerequisites</span></span>

<span data-ttu-id="8d49d-115">若要完成本教程，需要安装以下工具：</span><span class="sxs-lookup"><span data-stu-id="8d49d-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="8d49d-116">安装 Git</span><span class="sxs-lookup"><span data-stu-id="8d49d-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="8d49d-117">安装 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8d49d-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="8d49d-118">你可以安装免费社区版本的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="8d49d-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="8d49d-119">在安装过程中，如果有要添加到路径的选项 `git` ，请选择它。</span><span class="sxs-lookup"><span data-stu-id="8d49d-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="8d49d-120">在终端窗口中，运行以下命令来验证 `git` 安装：</span><span class="sxs-lookup"><span data-stu-id="8d49d-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="8d49d-121">在平台上使用合适的终端窗口。</span><span class="sxs-lookup"><span data-stu-id="8d49d-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="8d49d-122">这些示例使用 Git Bash，但可在大多数平台上运行。</span><span class="sxs-lookup"><span data-stu-id="8d49d-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="8d49d-123">打开最新版本的 Visual Studio并安装任何更新。</span><span class="sxs-lookup"><span data-stu-id="8d49d-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="8d49d-124">可以使用同一终端窗口运行本教程中的命令。</span><span class="sxs-lookup"><span data-stu-id="8d49d-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="8d49d-125">下载示例</span><span class="sxs-lookup"><span data-stu-id="8d49d-125">Download the sample</span></span>

<span data-ttu-id="8d49d-126">你可以开始使用简单的 [Hello， World！](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="8d49d-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="8d49d-127">C# 示例。</span><span class="sxs-lookup"><span data-stu-id="8d49d-127">sample in C#.</span></span> <span data-ttu-id="8d49d-128">在终端窗口中，运行以下命令将示例存储库克隆到计算机：</span><span class="sxs-lookup"><span data-stu-id="8d49d-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="8d49d-129">可以[分叉此](https://help.github.com/articles/fork-a-repo/)[存储库以](https://github.com/OfficeDev/Microsoft-Teams-Samples)修改所做的更改并将其保存到GitHub。</span><span class="sxs-lookup"><span data-stu-id="8d49d-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="8d49d-130">生成和运行示例</span><span class="sxs-lookup"><span data-stu-id="8d49d-130">Build and run the sample</span></span>

<span data-ttu-id="8d49d-131">可以在克隆 smaple 后生成并运行它。</span><span class="sxs-lookup"><span data-stu-id="8d49d-131">You can build and run the smaple after it is cloned.</span></span> 

<span data-ttu-id="8d49d-132">**生成并运行克隆的示例**</span><span class="sxs-lookup"><span data-stu-id="8d49d-132">**To build and run the cloned sample**</span></span>

1. <span data-ttu-id="8d49d-133">打开解决方案文件 **Microsoft.Teams。示例的** **Microsoft-Teams-Samples/samples/app-hello-world/csharp** 目录中的 Samples.HelloWorld.sln。</span><span class="sxs-lookup"><span data-stu-id="8d49d-133">Open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span>
1. <span data-ttu-id="8d49d-134">从 **"生成"菜单中** 选择" **生成解决方案** "。</span><span class="sxs-lookup"><span data-stu-id="8d49d-134">Select **Build Solution** from the **Build** menu.</span></span>
1. <span data-ttu-id="8d49d-135">选择 **F5** 键，或者从"调试 **"** 菜单中选择"开始调试"以运行示例。</span><span class="sxs-lookup"><span data-stu-id="8d49d-135">Select the **F5** key, or select **Start Debugging** from the **Debug** menu to run the sample.</span></span>

<span data-ttu-id="8d49d-136">当应用启动时，浏览器窗口将打开，并启动应用的根。</span><span class="sxs-lookup"><span data-stu-id="8d49d-136">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="8d49d-137">你可以转到以下 URL 以验证是否正在加载所有应用 URL：</span><span class="sxs-lookup"><span data-stu-id="8d49d-137">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

- `https://localhost:44327/`
- `https://localhost:44327/hello`
- `https://localhost:44327/first`
- `https://localhost:44327/second`

> [!Note]
> <span data-ttu-id="8d49d-138">如果收到错误 `Could not find a part of the path … bin\roslyn\csc.exe` ，则使用 命令 更新程序包 `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。</span><span class="sxs-lookup"><span data-stu-id="8d49d-138">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="8d49d-139">有关详细信息，请参阅 Stack [Overflow 上的此问题](https://stackoverflow.com/questions/32780315)。</span><span class="sxs-lookup"><span data-stu-id="8d49d-139">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

<a name="hostsample"></a>
## <a name="deploy-your-sample-app"></a><span data-ttu-id="8d49d-140">部署示例应用</span><span class="sxs-lookup"><span data-stu-id="8d49d-140">Deploy your sample app</span></span>

<span data-ttu-id="8d49d-141">应用程序中Microsoft Teams是提供一个或多个功能的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8d49d-141">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="8d49d-142">若要Teams加载应用，应用必须在 Internet 上可用。</span><span class="sxs-lookup"><span data-stu-id="8d49d-142">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="8d49d-143">为此，你需要托管应用。</span><span class="sxs-lookup"><span data-stu-id="8d49d-143">To do this, you need to host your app.</span></span> <span data-ttu-id="8d49d-144">你可以免费在 Microsoft Azure中托管它，或者使用 创建到计算机上本地进程的隧道 `ngrok` 。</span><span class="sxs-lookup"><span data-stu-id="8d49d-144">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="8d49d-145">托管应用后，记下其根 URL，如 `https://yourteamsapp.ngrok.io` 或 `https://yourteamsapp.azurewebsites.net` 。</span><span class="sxs-lookup"><span data-stu-id="8d49d-145">After you host your app, make a note of its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="8d49d-146">Tunnel ngrok</span><span class="sxs-lookup"><span data-stu-id="8d49d-146">Tunnel using ngrok</span></span>

<span data-ttu-id="8d49d-147">为了快速测试，可以在计算机上运行应用，并通过 Web 终结点创建一个隧道。</span><span class="sxs-lookup"><span data-stu-id="8d49d-147">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="8d49d-148">[`ngrok`](https://ngrok.com) 是一款免费工具，可用于获取 Web 地址，例如 `https://d0ac14a5.ngrok.io` 。</span><span class="sxs-lookup"><span data-stu-id="8d49d-148">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="8d49d-149">你可以 [下载并安装](https://ngrok.com/download) ngrok，并将其添加到 中的位置 `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="8d49d-149">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="8d49d-150">安装后 `ngrok` ，打开一个新的终端窗口并运行以下命令以创建隧道：</span><span class="sxs-lookup"><span data-stu-id="8d49d-150">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="8d49d-151">`Ngrok` 响应来自 Internet 的请求，将它们路由到在端口 44327 上运行的应用。</span><span class="sxs-lookup"><span data-stu-id="8d49d-151">`Ngrok` responds to requests from the internet and routes them to your app running on port 44327.</span></span> 

<span data-ttu-id="8d49d-152">**验证响应**</span><span class="sxs-lookup"><span data-stu-id="8d49d-152">**To verify the response**</span></span>

1. <span data-ttu-id="8d49d-153">打开浏览器并转到 `https://d0ac14a5.ngrok.io/hello` 。</span><span class="sxs-lookup"><span data-stu-id="8d49d-153">Open your browser and go to `https://d0ac14a5.ngrok.io/hello`.</span></span> <span data-ttu-id="8d49d-154">这将加载应用的 Hello 页面。</span><span class="sxs-lookup"><span data-stu-id="8d49d-154">This will load your app's Hello page.</span></span>
1. <span data-ttu-id="8d49d-155">使用控制台会话中显示的转发地址，而不是步骤 1 中提到的 `ngrok` URL。</span><span class="sxs-lookup"><span data-stu-id="8d49d-155">Instead of the URL mentioned in Step 1, use the forwarding address displayed by `ngrok` in your console session.</span></span>
    > [!NOTE]
    > <span data-ttu-id="8d49d-156">如果在生成和运行步骤中使用不同的 [端口，请确保](#build-and-run-the-sample) 使用相同的端口号来设置 `ngrok` 隧道。</span><span class="sxs-lookup"><span data-stu-id="8d49d-156">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>
    > [!TIP]
    > <span data-ttu-id="8d49d-157">建议在不同的终端 `ngrok` 窗口中运行。</span><span class="sxs-lookup"><span data-stu-id="8d49d-157">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="8d49d-158">这是为了在不 `ngrok` 干扰应用的情况下阻止运行。</span><span class="sxs-lookup"><span data-stu-id="8d49d-158">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="8d49d-159">必须停止、重新生成和重新运行应用。</span><span class="sxs-lookup"><span data-stu-id="8d49d-159">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="8d49d-160">会话 `ngrok` 在此窗口中提供有用的调试信息。</span><span class="sxs-lookup"><span data-stu-id="8d49d-160">The `ngrok` session provides useful debugging information in this window.</span></span>

    <span data-ttu-id="8d49d-161">该应用仅在您的计算机上的当前会话期间可用。</span><span class="sxs-lookup"><span data-stu-id="8d49d-161">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="8d49d-162">如果计算机关闭或进入睡眠状态，服务将不再可用。</span><span class="sxs-lookup"><span data-stu-id="8d49d-162">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="8d49d-163">在将应用共享给其他用户进行测试时，请记住这一点。</span><span class="sxs-lookup"><span data-stu-id="8d49d-163">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="8d49d-164">如果必须重新启动该服务，应用将返回一个新地址，并且必须更新使用该地址的每一个位置。</span><span class="sxs-lookup"><span data-stu-id="8d49d-164">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="8d49d-165">的付费 `ngrok` 版本没有此限制。</span><span class="sxs-lookup"><span data-stu-id="8d49d-165">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="8d49d-166">Azure 中的主机</span><span class="sxs-lookup"><span data-stu-id="8d49d-166">Host in Azure</span></span>

<span data-ttu-id="8d49d-167">Microsoft Azure共享基础结构在免费层托管 .NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8d49d-167">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="8d49d-168">这足以运行 `Hello World` 示例。</span><span class="sxs-lookup"><span data-stu-id="8d49d-168">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="8d49d-169">有关详细信息，请参阅 [创建新的免费 Azure 帐户](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="8d49d-169">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="8d49d-170">Visual Studio对将应用部署到不同提供程序（包括 Azure）提供内置支持：</span><span class="sxs-lookup"><span data-stu-id="8d49d-170">Visual Studio has built-in support for app deployment to different providers, including Azure:</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

<span data-ttu-id="8d49d-171">**更新应用包**</span><span class="sxs-lookup"><span data-stu-id="8d49d-171">**Update the app package**</span></span>

# <a name="app-studio"></a>[<span data-ttu-id="8d49d-172">应用程序 Studio</span><span class="sxs-lookup"><span data-stu-id="8d49d-172">App Studio</span></span>](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[<span data-ttu-id="8d49d-173">开发人员门户</span><span class="sxs-lookup"><span data-stu-id="8d49d-173">Developer Portal</span></span>](#tab/DP)

<span data-ttu-id="8d49d-174">**安装开发人员门户 (预览) 中Teams**</span><span class="sxs-lookup"><span data-stu-id="8d49d-174">**To install Developer Portal (preview) in Teams**</span></span>


1. <span data-ttu-id="8d49d-175">选择 **左侧** 栏底部的"应用"图标，然后搜索"开发人员 **门户"。**</span><span class="sxs-lookup"><span data-stu-id="8d49d-175">Select the **Apps** icon at the bottom of the left-hand bar, and search for **Developer Portal**.</span></span>

    <img width="430px" alt="Screenshot of TDP" src="~/assets/images/Screen1.png"/>

1. <span data-ttu-id="8d49d-176">选择 **"开发人员门户"，** 然后选择"打开 **"。**</span><span class="sxs-lookup"><span data-stu-id="8d49d-176">Select **Developer Portal** and select **Open**.</span></span>

    <img width="430px" alt="Screenshot of TDP Open" src="~/assets/images/screen2.png"/>

1. <span data-ttu-id="8d49d-177">选择"应用"选项卡，然后选择 **"导入现有应用"。**</span><span class="sxs-lookup"><span data-stu-id="8d49d-177">Select the Apps tab and select **Import an existing app**.</span></span>

    <img width="430px" alt="Screenshot of import app in tdp" src="~/assets/images/screen3.png"/>

1. <span data-ttu-id="8d49d-178">选择 **Hello World，\*\*\*\*然后选择导入**。</span><span class="sxs-lookup"><span data-stu-id="8d49d-178">Select **Hello World** and select **Import**.</span></span> <span data-ttu-id="8d49d-179">Hello **World** 应用在开发人员门户中导入。</span><span class="sxs-lookup"><span data-stu-id="8d49d-179">The **Hello World** app is imported in Developer Portal.</span></span> 

    <span data-ttu-id="8d49d-180">可以使用开发人员门户配置Teams应用。</span><span class="sxs-lookup"><span data-stu-id="8d49d-180">You can configure your app using the Teams Developer Portal.</span></span> <span data-ttu-id="8d49d-181">清单位于"分发"下。</span><span class="sxs-lookup"><span data-stu-id="8d49d-181">The Manifest is found under Distribute.</span></span> <span data-ttu-id="8d49d-182">可以使用清单为应用配置功能、必需资源和重要的属性。</span><span class="sxs-lookup"><span data-stu-id="8d49d-182">You can use the Manifest to configure capabilities, required resources, and other important attributes for your app.</span></span> <span data-ttu-id="8d49d-183">有关如何使用开发人员门户配置应用的更多详细信息，请参阅开发人员Teams[门户](../concepts/build-and-test/teams-developer-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="8d49d-183">For more details on how to configure your app using Developer Portal, see [Teams Developer Portal](../concepts/build-and-test/teams-developer-portal.md).</span></span>

    <img width="430px" alt="Screenshot of configure tdp" src="~/assets/images/Screen4.png"/>
---

<a name="updatecredentials"></a>
## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="8d49d-184">更新托管应用的凭据</span><span class="sxs-lookup"><span data-stu-id="8d49d-184">Update the credentials for your hosted app</span></span>

<span data-ttu-id="8d49d-185">示例应用要求将环境变量设置为文本文件中保存的值。</span><span class="sxs-lookup"><span data-stu-id="8d49d-185">The sample app requires the environment variables to be set to the values that you saved in the text file.</span></span>

<span data-ttu-id="8d49d-186">**更新托管应用的凭据**</span><span class="sxs-lookup"><span data-stu-id="8d49d-186">**To update the credentials for your hosted app**</span></span>

1. <span data-ttu-id="8d49d-187">打开 `appsettings.json`文件。</span><span class="sxs-lookup"><span data-stu-id="8d49d-187">Open the `appsettings.json` file.</span></span> 
1. <span data-ttu-id="8d49d-188">使用保存在文本文件中的自动程序 ID 更新 **MicrosoftAppId** 值。</span><span class="sxs-lookup"><span data-stu-id="8d49d-188">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> 
1. <span data-ttu-id="8d49d-189">使用保存的自动程序密码更新 **MicrosoftAppPassword。**</span><span class="sxs-lookup"><span data-stu-id="8d49d-189">Update the **MicrosoftAppPassword** with the bot password that you saved.</span></span>

    <img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

    <span data-ttu-id="8d49d-190">进行这些更改后，重新生成应用。</span><span class="sxs-lookup"><span data-stu-id="8d49d-190">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="8d49d-191">如果你使用的是 ngrok，请在本地运行应用，如果你要托管在 Azure 中，请重新部署该应用。</span><span class="sxs-lookup"><span data-stu-id="8d49d-191">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

<a name="configureapptab"></a>
## <a name="configure-the-app-tab"></a><span data-ttu-id="8d49d-192">配置"应用"选项卡</span><span class="sxs-lookup"><span data-stu-id="8d49d-192">Configure the app tab</span></span>

<span data-ttu-id="8d49d-193">将应用安装到团队后，必须将其配置为显示内容。</span><span class="sxs-lookup"><span data-stu-id="8d49d-193">After you have installed the app into teams, you must configure it to display the content.</span></span> 

<span data-ttu-id="8d49d-194">**配置"应用"选项卡**</span><span class="sxs-lookup"><span data-stu-id="8d49d-194">**To configure the app tab**</span></span>

1. <span data-ttu-id="8d49d-195">转到你安装了示例应用的团队中的频道，然后选择 **"+"** 按钮以添加新选项卡。</span><span class="sxs-lookup"><span data-stu-id="8d49d-195">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab.</span></span>
1. <span data-ttu-id="8d49d-196">从 **添加选项卡** 列表中选择Hello World。</span><span class="sxs-lookup"><span data-stu-id="8d49d-196">Select **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="8d49d-197">将显示一个配置对话框，允许您选择要在此通道中显示的选项卡。</span><span class="sxs-lookup"><span data-stu-id="8d49d-197">A configuration dialog box is displayed that enables you to select the tab to display in this channel.</span></span> 
1. <span data-ttu-id="8d49d-198">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="8d49d-198">Select **Save**.</span></span> <span data-ttu-id="8d49d-199">选项卡 `Hello World` 随选项卡一起加载。</span><span class="sxs-lookup"><span data-stu-id="8d49d-199">The `Hello World` tab is loaded with the tab.</span></span>

    <img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="8d49d-200">在设备中测试Teams</span><span class="sxs-lookup"><span data-stu-id="8d49d-200">Test your bot in Teams</span></span>

<span data-ttu-id="8d49d-201">现在可以在 Teams 中测试自动程序。</span><span class="sxs-lookup"><span data-stu-id="8d49d-201">You can now test the bot in Teams.</span></span> 

<span data-ttu-id="8d49d-202">**测试机器人**</span><span class="sxs-lookup"><span data-stu-id="8d49d-202">**To test your bot**</span></span>

* <span data-ttu-id="8d49d-203">选择你注册应用的团队中的频道并键入 `@your-bot-name` 。</span><span class="sxs-lookup"><span data-stu-id="8d49d-203">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="8d49d-204">这称为 **\@ 提及**。</span><span class="sxs-lookup"><span data-stu-id="8d49d-204">This is called an **\@mention**.</span></span> <span data-ttu-id="8d49d-205">机器人将回复你发送的任何消息。</span><span class="sxs-lookup"><span data-stu-id="8d49d-205">The bot replies to any message that you send.</span></span>

    <img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="8d49d-206">测试邮件扩展</span><span class="sxs-lookup"><span data-stu-id="8d49d-206">Test your messaging extension</span></span>

<span data-ttu-id="8d49d-207">若要测试消息扩展，请选择 **对话** 视图中输入框下方的"..."。</span><span class="sxs-lookup"><span data-stu-id="8d49d-207">To test your messaging extension, select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="8d49d-208">将显示包含 **"Hello World"应用的** 菜单。</span><span class="sxs-lookup"><span data-stu-id="8d49d-208">A menu with the **'Hello World'** app is displayed.</span></span> <span data-ttu-id="8d49d-209">选择它时，将显示一组随机文本。</span><span class="sxs-lookup"><span data-stu-id="8d49d-209">When you select it, a set of random texts is displayed.</span></span> <span data-ttu-id="8d49d-210">可以选择其中一个随机文本，该文本将插入到对话中。</span><span class="sxs-lookup"><span data-stu-id="8d49d-210">You can select one of the random text and that is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

<span data-ttu-id="8d49d-211">选择随机文本之一。</span><span class="sxs-lookup"><span data-stu-id="8d49d-211">Select one of the random text.</span></span> <span data-ttu-id="8d49d-212">将显示格式化的卡片，并准备随自己的邮件一起发送。</span><span class="sxs-lookup"><span data-stu-id="8d49d-212">A card formatted and ready to send with your own message is shown.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

## <a name="see-also"></a><span data-ttu-id="8d49d-213">另请参阅</span><span class="sxs-lookup"><span data-stu-id="8d49d-213">See also</span></span>

* [<span data-ttu-id="8d49d-214">教程概述</span><span class="sxs-lookup"><span data-stu-id="8d49d-214">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="8d49d-215">代码示例</span><span class="sxs-lookup"><span data-stu-id="8d49d-215">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)