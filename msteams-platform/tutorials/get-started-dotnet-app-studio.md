---
title: 教程 - 使用 C 创建第一个应用#
description: 了解如何开始使用 C# 或 .NET 生成 Microsoft Teams 应用。
keywords: 入门 .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: b37a8d555117e38383504dc99d82d564439a3ebf
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231519"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a><span data-ttu-id="83409-104">使用 C# 或 .NET 创建你的第一个 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="83409-104">Create your first Teams app using C# or .NET</span></span>

<span data-ttu-id="83409-105">本教程帮助你使用 C# 或 .NET 创建 Microsoft Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="83409-105">This tutorial helps you to create a Microsoft Teams app using C# or .NET.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="83409-106">获取先决条件</span><span class="sxs-lookup"><span data-stu-id="83409-106">Get prerequisites</span></span>

<span data-ttu-id="83409-107">若要完成本教程，你需要获取以下工具：</span><span class="sxs-lookup"><span data-stu-id="83409-107">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="83409-108">安装 Git</span><span class="sxs-lookup"><span data-stu-id="83409-108">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="83409-109">[安装Visual Studio](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="83409-109">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="83409-110">你可以安装免费的社区版。</span><span class="sxs-lookup"><span data-stu-id="83409-110">You can install the free community edition.</span></span>

<span data-ttu-id="83409-111">在安装过程中，如果有要添加到 PATH 的选项， `git` 请选择它。</span><span class="sxs-lookup"><span data-stu-id="83409-111">During installation, if there is an option to add `git` to the PATH, choose it.</span></span>

<span data-ttu-id="83409-112">在终端窗口中，运行以下命令来验证 `git` 您的安装：</span><span class="sxs-lookup"><span data-stu-id="83409-112">In a terminal window, run the following command to verify your `git` installation:</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> <span data-ttu-id="83409-113">在平台上使用合适的终端窗口。</span><span class="sxs-lookup"><span data-stu-id="83409-113">Use a suitable terminal window on your platform.</span></span> <span data-ttu-id="83409-114">这些示例使用 Bash，但在大多数平台上运行。</span><span class="sxs-lookup"><span data-stu-id="83409-114">These examples use Bash but run on most platforms.</span></span>

<span data-ttu-id="83409-115">请确保启动最新版本的 Visual Studio并安装任何更新。</span><span class="sxs-lookup"><span data-stu-id="83409-115">Make sure to launch the latest version of Visual Studio and install any updates.</span></span>

<span data-ttu-id="83409-116">可以使用同一终端窗口运行本教程中的命令。</span><span class="sxs-lookup"><span data-stu-id="83409-116">You can use the same terminal window to run the commands in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="83409-117">下载示例</span><span class="sxs-lookup"><span data-stu-id="83409-117">Download the sample</span></span>

<span data-ttu-id="83409-118">你可以开始使用简单的 [Hello， World！](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="83409-118">You can get started with a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span></span> <span data-ttu-id="83409-119">C# 中的示例。</span><span class="sxs-lookup"><span data-stu-id="83409-119">sample in C#.</span></span> <span data-ttu-id="83409-120">在终端窗口中，运行以下命令将示例存储库克隆到本地计算机：</span><span class="sxs-lookup"><span data-stu-id="83409-120">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> <span data-ttu-id="83409-121">你可以 [分叉](https://help.github.com/articles/fork-a-repo/) 此 [存储库以](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) 修改所做的更改并将其保存到 GitHub 以参考。</span><span class="sxs-lookup"><span data-stu-id="83409-121">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) to modify and save your changes to GitHub for reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="83409-122">生成和运行示例</span><span class="sxs-lookup"><span data-stu-id="83409-122">Build and run the sample</span></span>

<span data-ttu-id="83409-123">克隆存储库后，Visual Studio从示例的根目录打开解决方案文件，然后 `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` 从菜单中 `Build` 选择。</span><span class="sxs-lookup"><span data-stu-id="83409-123">After the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the root directory of the sample and select `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="83409-124">若要运行示例， `F5` 请按或 `Start Debugging` 从菜单中 `Debug` 选择。</span><span class="sxs-lookup"><span data-stu-id="83409-124">To run the sample press `F5` or choose `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="83409-125">当应用启动时，浏览器窗口将打开，并启动应用的根。</span><span class="sxs-lookup"><span data-stu-id="83409-125">When the app starts, a browser window opens with the root of the app launched.</span></span> <span data-ttu-id="83409-126">你可以导航到以下 URL 以验证是否正在加载所有应用 URL：</span><span class="sxs-lookup"><span data-stu-id="83409-126">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- <span data-ttu-id="83409-127">[https://localhost:44327/second]https://localhost:44327/second)</span><span class="sxs-lookup"><span data-stu-id="83409-127">[https://localhost:44327/second]https://localhost:44327/second)</span></span>

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="83409-128">如果收到错误 `Could not find a part of the path … bin\roslyn\csc.exe` ，则使用命令更新程序包 `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。</span><span class="sxs-lookup"><span data-stu-id="83409-128">If you receive an error `Could not find a part of the path … bin\roslyn\csc.exe`, update the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="83409-129">有关详细信息，请参阅 [StackOverflow 上的此问题](https://stackoverflow.com/questions/32780315)。</span><span class="sxs-lookup"><span data-stu-id="83409-129">For more information, see [this question on StackOverflow](https://stackoverflow.com/questions/32780315).</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="83409-130">托管示例应用</span><span class="sxs-lookup"><span data-stu-id="83409-130">Host the sample app</span></span>

<span data-ttu-id="83409-131">Microsoft Teams 中的应用是提供一个或多个功能的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="83409-131">Apps in Microsoft Teams are web applications that provide one or more capabilities.</span></span> <span data-ttu-id="83409-132">若要使 Teams 平台加载你的应用，必须从 Internet 访问你的应用。</span><span class="sxs-lookup"><span data-stu-id="83409-132">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="83409-133">若要使应用从 Internet 访问，你需要托管你的应用。</span><span class="sxs-lookup"><span data-stu-id="83409-133">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="83409-134">你可以免费在 Microsoft Azure 中托管它，或者使用 创建到开发计算机上本地进程的隧道 `ngrok` 。</span><span class="sxs-lookup"><span data-stu-id="83409-134">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="83409-135">托管完应用后，请记下其根 URL。</span><span class="sxs-lookup"><span data-stu-id="83409-135">When you finish hosting your app, note its root URL.</span></span> <span data-ttu-id="83409-136">例如， `https://yourteamsapp.ngrok.io` 或 `https://yourteamsapp.azurewebsites.net` 。</span><span class="sxs-lookup"><span data-stu-id="83409-136">For example, `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="83409-137">使用 ngrok 的隧道</span><span class="sxs-lookup"><span data-stu-id="83409-137">Tunnel using ngrok</span></span>

<span data-ttu-id="83409-138">为了快速测试，可以在本地计算机上运行应用，并通过 Web 终结点创建一个隧道。</span><span class="sxs-lookup"><span data-stu-id="83409-138">For quick testing, you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="83409-139">[ngrok](https://ngrok.com) 是一款免费工具，您可以使用该工具获取 Web 地址，如 `https://d0ac14a5.ngrok.io` 。</span><span class="sxs-lookup"><span data-stu-id="83409-139">[ngrok](https://ngrok.com) is a free tool with which you can get a web address such as `https://d0ac14a5.ngrok.io`.</span></span> <span data-ttu-id="83409-140">您可以 [下载并安装](https://ngrok.com/download) ngrok。</span><span class="sxs-lookup"><span data-stu-id="83409-140">You can [download and install](https://ngrok.com/download) ngrok.</span></span> <span data-ttu-id="83409-141">请确保将其添加到您的位置 `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="83409-141">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="83409-142">安装 ngrok 后，打开一个新的终端窗口并运行以下命令以创建隧道：</span><span class="sxs-lookup"><span data-stu-id="83409-142">After you install ngrok, open a new terminal window and run the following command to create a tunnel:</span></span>

```bash
ngrok http 44327 -host-header=localhost:44327
```

<span data-ttu-id="83409-143">此示例使用端口 44327，请务必指定它。</span><span class="sxs-lookup"><span data-stu-id="83409-143">The sample uses port 44327 be sure to specify it.</span></span>

<span data-ttu-id="83409-144">Ngrok 侦听来自 Internet 的请求，将它们路由到在端口 44327 上运行的应用。</span><span class="sxs-lookup"><span data-stu-id="83409-144">Ngrok listens to requests from the internet and routes them to your app running on port 44327.</span></span> <span data-ttu-id="83409-145">若要验证，请打开浏览器并转到 `https://d0ac14a5.ngrok.io/hello` 加载应用的 Hello 页面。</span><span class="sxs-lookup"><span data-stu-id="83409-145">To verify, open your browser and go to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="83409-146">请使用控制台会话中 ngrok 显示的转发地址，而不是此 URL。</span><span class="sxs-lookup"><span data-stu-id="83409-146">Instead of this URL, use the forwarding address displayed by ngrok in your console session.</span></span>

> [!NOTE]
> <span data-ttu-id="83409-147">如果在生成和运行步骤中使用不同的端口，[](#build-and-run-the-sample)请确保使用相同的端口号来设置 `ngrok` 隧道。</span><span class="sxs-lookup"><span data-stu-id="83409-147">If you have used a different port in the [build and run](#build-and-run-the-sample) step, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>

> [!TIP]
> <span data-ttu-id="83409-148">建议在不同的终端窗口中 `ngrok` 运行。</span><span class="sxs-lookup"><span data-stu-id="83409-148">It is a good idea to run `ngrok` in a different terminal window.</span></span> <span data-ttu-id="83409-149">这是为了阻止 ngrok 在不会影响应用的情况下运行，你必须停止、重新生成和重新运行应用。</span><span class="sxs-lookup"><span data-stu-id="83409-149">This is done to keep ngrok from running without interfering with the app, which you have to stop, rebuild, and rerun.</span></span> <span data-ttu-id="83409-150">会话 `ngrok` 在此窗口中提供有用的调试信息。</span><span class="sxs-lookup"><span data-stu-id="83409-150">The `ngrok` session provides useful debugging information in this window.</span></span>

<span data-ttu-id="83409-151">该应用仅在开发计算机上当前会话期间可用。</span><span class="sxs-lookup"><span data-stu-id="83409-151">The app is only available during the current session on your development machine.</span></span> <span data-ttu-id="83409-152">如果计算机已关闭或进入睡眠状态，服务将不再可用。</span><span class="sxs-lookup"><span data-stu-id="83409-152">If the machine is shut down or goes to sleep, the service is no longer available.</span></span> <span data-ttu-id="83409-153">在将应用共享给其他用户进行测试时，请记住这一点。</span><span class="sxs-lookup"><span data-stu-id="83409-153">Remember this when you share the app for testing to other users.</span></span> <span data-ttu-id="83409-154">如果必须重新启动该服务，应用将返回一个新地址，并且必须更新使用该地址的每一个位置。</span><span class="sxs-lookup"><span data-stu-id="83409-154">If you have to restart the service, the app returns a new address and you must update every location that uses that address.</span></span> <span data-ttu-id="83409-155">ngrok 的付费版本没有此限制。</span><span class="sxs-lookup"><span data-stu-id="83409-155">The paid version of ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="83409-156">Azure 中的主机</span><span class="sxs-lookup"><span data-stu-id="83409-156">Host in Azure</span></span>

<span data-ttu-id="83409-157">Microsoft Azure 使用共享基础结构在免费层托管 .NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="83409-157">Microsoft Azure hosts your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="83409-158">这足以运行 `Hello World` 示例。</span><span class="sxs-lookup"><span data-stu-id="83409-158">This is sufficient to run the `Hello World` sample.</span></span> <span data-ttu-id="83409-159">有关详细信息，请参阅 [创建新的免费帐户](https://azure.microsoft.com/free/)。</span><span class="sxs-lookup"><span data-stu-id="83409-159">For more information, see [creating a new free account](https://azure.microsoft.com/free/).</span></span>

<span data-ttu-id="83409-160">Visual Studio向不同提供程序（包括 Azure）部署应用提供内置支持。</span><span class="sxs-lookup"><span data-stu-id="83409-160">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="83409-161">更新托管应用的凭据</span><span class="sxs-lookup"><span data-stu-id="83409-161">Update the credentials for your hosted app</span></span>

<span data-ttu-id="83409-162">示例应用需要将以下环境变量设置为之前记下的值。</span><span class="sxs-lookup"><span data-stu-id="83409-162">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="83409-163">打开文件appsettings.js文件。</span><span class="sxs-lookup"><span data-stu-id="83409-163">Open up the appsettings.json file.</span></span> <span data-ttu-id="83409-164">使用之前保存的自动程序 ID 更新 *MicrosoftAppId* 值。</span><span class="sxs-lookup"><span data-stu-id="83409-164">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="83409-165">使用之前保存的自动程序密码更新 *MicrosoftAppPassword。*</span><span class="sxs-lookup"><span data-stu-id="83409-165">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="83409-166">进行这些更改后，重新生成应用。</span><span class="sxs-lookup"><span data-stu-id="83409-166">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="83409-167">如果你使用的是 ngrok，请在本地运行该应用，如果你正在 Azure 中托管，请重新部署该应用。</span><span class="sxs-lookup"><span data-stu-id="83409-167">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="83409-168">配置应用选项卡</span><span class="sxs-lookup"><span data-stu-id="83409-168">Configure the app tab</span></span>

<span data-ttu-id="83409-169">将应用安装到团队后，你需要将其配置为显示内容。</span><span class="sxs-lookup"><span data-stu-id="83409-169">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="83409-170">转到已安装示例应用的团队中的频道，然后单击 **"+"** 按钮以添加新选项卡。然后，可以从 `Hello World` "添加选项卡 **"列表中选择** 。</span><span class="sxs-lookup"><span data-stu-id="83409-170">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="83409-171">然后，将显示配置对话框。</span><span class="sxs-lookup"><span data-stu-id="83409-171">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="83409-172">此对话框将让你选择要在此通道中显示哪个选项卡。</span><span class="sxs-lookup"><span data-stu-id="83409-172">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="83409-173">选择该选项卡并单击后，即可看到已加载的 `Save` `Hello World` 选项卡以及您选择的选项卡。</span><span class="sxs-lookup"><span data-stu-id="83409-173">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="83409-174">在 Teams 中测试机器人</span><span class="sxs-lookup"><span data-stu-id="83409-174">Test your bot in Teams</span></span>

<span data-ttu-id="83409-175">你现在可以在 Teams 中与机器人交互。</span><span class="sxs-lookup"><span data-stu-id="83409-175">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="83409-176">选择你在团队中注册应用并键入的频道 `@your-bot-name` 。</span><span class="sxs-lookup"><span data-stu-id="83409-176">Choose a channel in the team where you registered your app and type `@your-bot-name`.</span></span> <span data-ttu-id="83409-177">这称为 **\@ 提及**。</span><span class="sxs-lookup"><span data-stu-id="83409-177">This is called an **\@mention**.</span></span> <span data-ttu-id="83409-178">发送到自动程序的任何邮件都将作为回复发送回。</span><span class="sxs-lookup"><span data-stu-id="83409-178">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="83409-179">测试邮件扩展</span><span class="sxs-lookup"><span data-stu-id="83409-179">Test your messaging extension</span></span>

<span data-ttu-id="83409-180">若要测试消息扩展，可以单击对话视图中输入框下方的三个点。</span><span class="sxs-lookup"><span data-stu-id="83409-180">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="83409-181">菜单将弹出，并包含 **"Hello World"** 应用。</span><span class="sxs-lookup"><span data-stu-id="83409-181">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="83409-182">单击它时，你将看到一组随机文本显示。</span><span class="sxs-lookup"><span data-stu-id="83409-182">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="83409-183">你可以选择其中任何一个，并将其插入到对话中。</span><span class="sxs-lookup"><span data-stu-id="83409-183">You can choose any one of them and it is inserted into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="83409-184">选择其中一个随机文本，你将在底部看到格式化的卡片，并准备好随自己的邮件一起发送。</span><span class="sxs-lookup"><span data-stu-id="83409-184">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
