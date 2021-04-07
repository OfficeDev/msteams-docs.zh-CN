---
title: 教程 - 使用 C 创建第一个应用#
description: 了解如何开始使用 microsoft Teams 或 .NET C# Microsoft Teams 应用。
keywords: 入门 .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 99a0982a0fa453c6eb7ffeea25ba8a2607cf2d5e
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596257"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a><span data-ttu-id="a1316-104">使用 C# .NET 创建你的第一个 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="a1316-104">Create your first Teams app using C# or .NET</span></span>

<span data-ttu-id="a1316-105">本教程帮助你使用 C# .NET 创建 Microsoft Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="a1316-105">This tutorial helps you to create a Microsoft Teams app using C# or .NET.</span></span> <span data-ttu-id="a1316-106">为此，你必须：</span><span class="sxs-lookup"><span data-stu-id="a1316-106">To do this, you must:</span></span>

* <span data-ttu-id="a1316-107">准备环境</span><span class="sxs-lookup"><span data-stu-id="a1316-107">Prepare your environment</span></span>
* <span data-ttu-id="a1316-108">获取先决条件</span><span class="sxs-lookup"><span data-stu-id="a1316-108">Get prerequisites</span></span>
* <span data-ttu-id="a1316-109">下载示例</span><span class="sxs-lookup"><span data-stu-id="a1316-109">Download the sample</span></span>
* <span data-ttu-id="a1316-110">生成和运行示例</span><span class="sxs-lookup"><span data-stu-id="a1316-110">Build and run the sample</span></span>
* <span data-ttu-id="a1316-111">托管示例应用</span><span class="sxs-lookup"><span data-stu-id="a1316-111">Host the sample app</span></span>
* <span data-ttu-id="a1316-112">更新托管应用的凭据</span><span class="sxs-lookup"><span data-stu-id="a1316-112">Update the credentials for your hosted app</span></span>
* <span data-ttu-id="a1316-113">配置"应用"选项卡</span><span class="sxs-lookup"><span data-stu-id="a1316-113">Configure the app tab</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="a1316-114">获取先决条件</span><span class="sxs-lookup"><span data-stu-id="a1316-114">Get prerequisites</span></span>

<span data-ttu-id="a1316-115">若要完成本教程，需要安装以下工具：</span><span class="sxs-lookup"><span data-stu-id="a1316-115">To complete this tutorial, you need to install the following tools:</span></span>

- [<span data-ttu-id="a1316-116">安装 Git</span><span class="sxs-lookup"><span data-stu-id="a1316-116">Install Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="a1316-117">安装 Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a1316-117">Install Visual Studio</span></span>](https://www.visualstudio.com/downloads/)

<span data-ttu-id="a1316-118">你可以安装免费社区版本的 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="a1316-118">You can install the free community edition of Visual Studio.</span></span> <span data-ttu-id="a1316-119">在安装过程中，如果有要添加到路径的选项 `git` ，请选择它。</span><span class="sxs-lookup"><span data-stu-id="a1316-119">During installation, if there is an option to add `git` to the path, select it.</span></span> <span data-ttu-id="a1316-120">在终端窗口中，运行以下命令来验证 `git` 安装：</span><span class="sxs-lookup"><span data-stu-id="a1316-120">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="a1316-121">在平台上使用合适的终端窗口。</span><span class="sxs-lookup"><span data-stu-id="a1316-121">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="a1316-122">这些示例使用 Git Bash，但可在大多数平台上运行。</span><span class="sxs-lookup"><span data-stu-id="a1316-122">These examples use Git Bash but can be run on most platforms.</span></span>

<span data-ttu-id="a1316-123">打开最新版本的 Visual Studio并安装任何更新。</span><span class="sxs-lookup"><span data-stu-id="a1316-123">Open the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="a1316-124">可以使用同一终端窗口运行本教程中的命令。</span><span class="sxs-lookup"><span data-stu-id="a1316-124">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="a1316-125">下载示例</span><span class="sxs-lookup"><span data-stu-id="a1316-125">Download the sample</span></span>

<span data-ttu-id="a1316-126">你可以开始使用简单的 [Hello， World！](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span><span class="sxs-lookup"><span data-stu-id="a1316-126">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp)</span></span> <span data-ttu-id="a1316-127">C# 示例。</span><span class="sxs-lookup"><span data-stu-id="a1316-127">sample in C#.</span></span> <span data-ttu-id="a1316-128">在终端窗口中，运行以下命令将示例存储库克隆到计算机：</span><span class="sxs-lookup"><span data-stu-id="a1316-128">In a terminal window, run the following command to clone the sample repository to your computer:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="a1316-129">可以[分叉此](https://help.github.com/articles/fork-a-repo/)[存储库来](https://github.com/OfficeDev/Microsoft-Teams-Samples)修改更改并将其保存到 GitHub。</span><span class="sxs-lookup"><span data-stu-id="a1316-129">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) to modify and save your changes to GitHub.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="a1316-130">生成和运行示例</span><span class="sxs-lookup"><span data-stu-id="a1316-130">Build and run the sample</span></span>

<span data-ttu-id="a1316-131">克隆存储库后，使用 Visual Studio 从示例的 **Microsoft-Teams-Samples/samples/app-hello-world/csharp** 目录中打开解决方案文件 **Microsoft.Teams.Samples.HelloWorld.sln。**</span><span class="sxs-lookup"><span data-stu-id="a1316-131">After the repo is cloned, use Visual Studio to open the solution file **Microsoft.Teams.Samples.HelloWorld.sln** from the **Microsoft-Teams-Samples/samples/app-hello-world/csharp** directory of the sample.</span></span> <span data-ttu-id="a1316-132">然后，从 **"生成"菜单中选择** "生成 **解决方案** "。</span><span class="sxs-lookup"><span data-stu-id="a1316-132">Then, select **Build Solution** from the **Build** menu.</span></span> <span data-ttu-id="a1316-133">若要运行该示例，请按 **F5** 或从"调试 **"** 菜单中选择"开始 **调试** "。</span><span class="sxs-lookup"><span data-stu-id="a1316-133">To run the sample, press **F5** or select **Start Debugging** from the **Debug** menu.</span></span>

<span data-ttu-id="a1316-134">当应用启动时，浏览器窗口将打开，并启动应用的根。</span><span class="sxs-lookup"><span data-stu-id="a1316-134">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="a1316-135">你可以转到以下 URL 以验证是否正在加载所有应用 URL：</span><span class="sxs-lookup"><span data-stu-id="a1316-135">You can go to the following URLs to verify that all the app URLs are loading:</span></span>

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- [https://localhost:44327/second](https://localhost:44327/second)

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="a1316-136">如果收到错误 `Could not find a part of the path … bin\roslyn\csc.exe` ，则使用 命令 更新程序包 `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。</span><span class="sxs-lookup"><span data-stu-id="a1316-136">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="a1316-137">有关详细信息，请参阅 Stack [Overflow 上的此问题](https://stackoverflow.com/questions/32780315)。</span><span class="sxs-lookup"><span data-stu-id="a1316-137">For more information, see [this question on Stack Overflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="a1316-138">托管示例应用</span><span class="sxs-lookup"><span data-stu-id="a1316-138">Host the sample app</span></span>

<span data-ttu-id="a1316-139">Microsoft Teams 中的应用是提供一个或多个功能的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a1316-139">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="a1316-140">若要使 Teams 平台加载你的应用，你的应用必须在 Internet 上可用。</span><span class="sxs-lookup"><span data-stu-id="a1316-140">For the Teams platform to load your app, your app must be available on the internet.</span></span> <span data-ttu-id="a1316-141">为此，你需要托管应用。</span><span class="sxs-lookup"><span data-stu-id="a1316-141">To do this, you need to host your app.</span></span> <span data-ttu-id="a1316-142">你可以免费在 Microsoft Azure 中托管它，或者使用 创建到计算机上本地进程的隧道 `ngrok` 。</span><span class="sxs-lookup"><span data-stu-id="a1316-142">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your computer using `ngrok`.</span></span> <span data-ttu-id="a1316-143">托管应用后，请记下其根 URL，如 `https://yourteamsapp.ngrok.io` 或 `https://yourteamsapp.azurewebsites.net` 。</span><span class="sxs-lookup"><span data-stu-id="a1316-143">After you host your app, note its root URL, such as `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="a1316-144">使用 ngrok 的隧道</span><span class="sxs-lookup"><span data-stu-id="a1316-144">Tunnel using ngrok</span></span>

<span data-ttu-id="a1316-145">为了快速测试，可以在计算机上运行应用，并通过 Web 终结点创建一个隧道。</span><span class="sxs-lookup"><span data-stu-id="a1316-145">For quick testing, you can run the app on your computer and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="a1316-146">[`ngrok`](https://ngrok.com) 是一款免费工具，可用于获取 Web 地址，例如 `https://d0ac14a5.ngrok.io` 。</span><span class="sxs-lookup"><span data-stu-id="a1316-146">[`ngrok`](https://ngrok.com) is a free tool with which you can get a web address, such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="a1316-147">你可以 [下载并安装](https://ngrok.com/download) ngrok，并将其添加到 中的位置 `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="a1316-147">You can [download and install](https://ngrok.com/download) ngrok and add it to a location in your `PATH`.</span></span>

<span data-ttu-id="a1316-148">安装后 `ngrok` ，打开一个新的终端窗口并运行以下命令以创建隧道：</span><span class="sxs-lookup"><span data-stu-id="a1316-148">After you install `ngrok`, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="a1316-149">`Ngrok` 侦听来自 Internet 的请求，将它们路由到在端口 44327 上运行的应用。</span><span class="sxs-lookup"><span data-stu-id="a1316-149">`Ngrok` listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="a1316-150">若要验证，请打开浏览器并转到 `https://d0ac14a5.ngrok.io/hello` 加载应用的 hello 页面。</span><span class="sxs-lookup"><span data-stu-id="a1316-150">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="a1316-151">使用控制台会话中显示的转发地址， `ngrok` 而不是此 URL。</span><span class="sxs-lookup"><span data-stu-id="a1316-151">Instead of this URL, use the forwarding address displayed by `ngrok` in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="a1316-152">如果在生成和运行步骤中使用不同的 [端口，请确保](#build-and-run-the-sample) 使用相同的端口号来设置 `ngrok` 隧道。</span><span class="sxs-lookup"><span data-stu-id="a1316-152">If you have used a different port in the [build and run](#build-and-run-the-sample) step, ensure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="a1316-153">建议在不同的终端 `ngrok` 窗口中运行。</span><span class="sxs-lookup"><span data-stu-id="a1316-153">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="a1316-154">这是为了在不 `ngrok` 干扰应用的情况下阻止运行。</span><span class="sxs-lookup"><span data-stu-id="a1316-154">This is done to keep `ngrok` from running without interfering with the app.</span></span> <span data-ttu-id="a1316-155">必须停止、重新生成和重新运行应用。</span><span class="sxs-lookup"><span data-stu-id="a1316-155">You have to stop, rebuild, and rerun the app.</span></span> <span data-ttu-id="a1316-156">会话 `ngrok` 在此窗口中提供有用的调试信息。</span><span class="sxs-lookup"><span data-stu-id="a1316-156">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="a1316-157">该应用仅在您的计算机上的当前会话期间可用。</span><span class="sxs-lookup"><span data-stu-id="a1316-157">The app is only available during the current session on your computer.</span></span> <span data-ttu-id="a1316-158">如果计算机关闭或进入睡眠状态，服务将不再可用。</span><span class="sxs-lookup"><span data-stu-id="a1316-158">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="a1316-159">在将应用共享给其他用户进行测试时，请记住这一点。</span><span class="sxs-lookup"><span data-stu-id="a1316-159">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="a1316-160">如果必须重新启动该服务，应用将返回一个新地址，并且必须更新使用该地址的每一个位置。</span><span class="sxs-lookup"><span data-stu-id="a1316-160">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="a1316-161">的付费 `ngrok` 版本没有此限制。</span><span class="sxs-lookup"><span data-stu-id="a1316-161">The paid version of `ngrok` does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="a1316-162">Azure 中的主机</span><span class="sxs-lookup"><span data-stu-id="a1316-162">Host in Azure</span></span>

<span data-ttu-id="a1316-163">Microsoft Azure 使用共享基础结构在免费层托管 .NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="a1316-163">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="a1316-164">这足以运行 `Hello World` 示例。</span><span class="sxs-lookup"><span data-stu-id="a1316-164">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="a1316-165">有关详细信息，请参阅 [创建新的免费 Azure 帐户](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="a1316-165">For more information, see [creating a new free Azure account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="a1316-166">Visual Studio对将应用部署到不同提供程序（包括 Azure）提供内置支持。</span><span class="sxs-lookup"><span data-stu-id="a1316-166">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="a1316-167">更新托管应用的凭据</span><span class="sxs-lookup"><span data-stu-id="a1316-167">Update the credentials for your hosted app</span></span>

<span data-ttu-id="a1316-168">示例应用要求将环境变量设置为保存在文本文件中的值。</span><span class="sxs-lookup"><span data-stu-id="a1316-168">The sample app requires the environment variables be set to the values that you saved in the text file.</span></span>

<span data-ttu-id="a1316-169">打开 `appsettings.json`文件。</span><span class="sxs-lookup"><span data-stu-id="a1316-169">Open the `appsettings.json` file.</span></span> <span data-ttu-id="a1316-170">使用保存在文本文件中的自动程序 ID 更新 **MicrosoftAppId** 值。</span><span class="sxs-lookup"><span data-stu-id="a1316-170">Update the **MicrosoftAppId** value with your bot ID that you saved in the text file.</span></span> <span data-ttu-id="a1316-171">使用保存的自动程序密码更新 **MicrosoftAppPassword。**</span><span class="sxs-lookup"><span data-stu-id="a1316-171">Update the **MicrosoftAppPassword** with the bot password you saved.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="a1316-172">进行这些更改后，重新生成应用。</span><span class="sxs-lookup"><span data-stu-id="a1316-172">After these changes are made, rebuild the app.</span></span> <span data-ttu-id="a1316-173">如果你使用的是 ngrok，请在本地运行应用，如果你要托管在 Azure 中，请重新部署该应用。</span><span class="sxs-lookup"><span data-stu-id="a1316-173">If you are using ngrok, run the app locally, and if you are hosting in Azure, redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="a1316-174">配置"应用"选项卡</span><span class="sxs-lookup"><span data-stu-id="a1316-174">Configure the app tab</span></span>

<span data-ttu-id="a1316-175">将应用安装到团队后，必须将其配置为显示内容。</span><span class="sxs-lookup"><span data-stu-id="a1316-175">Once you install the app into a team, you must configure it to show content.</span></span> <span data-ttu-id="a1316-176">转到你安装了示例应用的团队中的频道，然后选择 **"+"** 按钮以添加新选项卡。从 **添加选项卡** 列表中选择Hello World。</span><span class="sxs-lookup"><span data-stu-id="a1316-176">Go to a channel in the team where you installed the sample app and select the **'+'** button to add a new tab. Choose **Hello World** from the **Add a tab** list.</span></span> <span data-ttu-id="a1316-177">将显示一个配置对话框，允许您选择要在此通道中显示的选项卡。</span><span class="sxs-lookup"><span data-stu-id="a1316-177">A configuration dialog box is displayed that enables you to choose the tab to display in this channel.</span></span> <span data-ttu-id="a1316-178">选择选项卡并选择保存选项卡 `Hello World` 后，选项卡将随选项卡一起加载。</span><span class="sxs-lookup"><span data-stu-id="a1316-178">After you select the tab and select **Save** the `Hello World` tab is loaded with the tab.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="a1316-179">在 Teams 中测试机器人</span><span class="sxs-lookup"><span data-stu-id="a1316-179">Test your bot in Teams</span></span>

<span data-ttu-id="a1316-180">现在，可以在 Teams 中测试机器人。</span><span class="sxs-lookup"><span data-stu-id="a1316-180">Now you can test the bot in Teams.</span></span> <span data-ttu-id="a1316-181">选择你注册应用的团队中的频道并键入 `@your-bot-name` 。</span><span class="sxs-lookup"><span data-stu-id="a1316-181">Select a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="a1316-182">这称为 **\@ 提及**。</span><span class="sxs-lookup"><span data-stu-id="a1316-182">This is called an **\@mention**.</span></span> <span data-ttu-id="a1316-183">机器人将回复你发送的任何消息。</span><span class="sxs-lookup"><span data-stu-id="a1316-183">The bot replies to any message that you send.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="a1316-184">测试邮件扩展</span><span class="sxs-lookup"><span data-stu-id="a1316-184">Test your messaging extension</span></span>

<span data-ttu-id="a1316-185">若要测试消息扩展，可以选择 **对话视图中** 输入框下方的"..."。</span><span class="sxs-lookup"><span data-stu-id="a1316-185">To test your messaging extension, you can select **...** below the input box in your conversation view.</span></span> <span data-ttu-id="a1316-186">将显示包含 **"Hello World"应用的** 菜单。</span><span class="sxs-lookup"><span data-stu-id="a1316-186">A menu with the **'Hello World'** app is displayed.</span></span> <span data-ttu-id="a1316-187">选择它时，将显示一组随机文本。</span><span class="sxs-lookup"><span data-stu-id="a1316-187">When you select it, a set of random texts is displayed.</span></span> <span data-ttu-id="a1316-188">可以选择其中一个随机文本，该文本将插入到对话中。</span><span class="sxs-lookup"><span data-stu-id="a1316-188">You can select one of the random text and that is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="a1316-189">选择随机文本之一。</span><span class="sxs-lookup"><span data-stu-id="a1316-189">Select one of the random text.</span></span> <span data-ttu-id="a1316-190">将显示格式化的卡片，并准备随自己的邮件一起发送。</span><span class="sxs-lookup"><span data-stu-id="a1316-190">A card formatted and ready to send with your own message is shown.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
