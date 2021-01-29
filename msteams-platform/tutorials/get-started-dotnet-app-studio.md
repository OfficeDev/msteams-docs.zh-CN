---
title: 教程 - 使用 C 创建第一个应用#
description: 了解如何开始使用 C#/.NET 生成 Microsoft Teams 应用。
keywords: 入门 .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: c28c4d00c375b8e37f82c343eec2c5405ae0c1c8
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037037"
---
# <a name="create-your-first-microsoft-teams-app-using-c"></a><span data-ttu-id="8ee50-104">使用 C 创建你的第一个 Microsoft Teams 应用#</span><span class="sxs-lookup"><span data-stu-id="8ee50-104">Create your first Microsoft Teams app using C#</span></span>

<span data-ttu-id="8ee50-105">本教程可帮助你开始使用 .NET 上的 C# 创建 Microsoft Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="8ee50-105">This tutorial helps you get started creating a Microsoft Teams app using C# on .NET.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="8ee50-106">获取先决条件</span><span class="sxs-lookup"><span data-stu-id="8ee50-106">Get prerequisites</span></span>

<span data-ttu-id="8ee50-107">若要完成本教程，你需要获取以下工具：</span><span class="sxs-lookup"><span data-stu-id="8ee50-107">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="8ee50-108">安装 Git</span><span class="sxs-lookup"><span data-stu-id="8ee50-108">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="8ee50-109">[安装Visual Studio](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="8ee50-109">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="8ee50-110">你可以安装免费的社区版。</span><span class="sxs-lookup"><span data-stu-id="8ee50-110">You can install the free community edition.</span></span>

<span data-ttu-id="8ee50-111">如果在安装过程中看到要添加到 PATH 的选项， `git` 请选择这样做。</span><span class="sxs-lookup"><span data-stu-id="8ee50-111">If you see an option to add `git` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="8ee50-112">它很方便。</span><span class="sxs-lookup"><span data-stu-id="8ee50-112">It will be handy.</span></span>

<span data-ttu-id="8ee50-113">在 `git` 终端窗口中运行以下代码，验证安装：</span><span class="sxs-lookup"><span data-stu-id="8ee50-113">Verify your `git` installation by running the following in a terminal window:</span></span>
> [!NOTE]
> <span data-ttu-id="8ee50-114">使用你最熟悉平台的终端窗口。</span><span class="sxs-lookup"><span data-stu-id="8ee50-114">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="8ee50-115">这些示例使用 Bash，但将在大多数平台上运行。</span><span class="sxs-lookup"><span data-stu-id="8ee50-115">These examples use Bash, but will run on most platforms.</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

<span data-ttu-id="8ee50-116">请确保启动最新版本的 Visual Studio并安装任何更新（如果显示）。</span><span class="sxs-lookup"><span data-stu-id="8ee50-116">Make sure to launch the latest version of Visual Studio and install any updates if shown.</span></span>

<span data-ttu-id="8ee50-117">你可以继续使用此终端窗口运行本教程中遵循的命令。</span><span class="sxs-lookup"><span data-stu-id="8ee50-117">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="8ee50-118">下载示例</span><span class="sxs-lookup"><span data-stu-id="8ee50-118">Download the sample</span></span>

<span data-ttu-id="8ee50-119">我们提供了简单的 [Hello， World！](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="8ee50-119">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span></span> <span data-ttu-id="8ee50-120">示例。</span><span class="sxs-lookup"><span data-stu-id="8ee50-120">sample in C# to get you started.</span></span> <span data-ttu-id="8ee50-121">在终端窗口中，运行以下命令将示例存储库克隆到本地计算机：</span><span class="sxs-lookup"><span data-stu-id="8ee50-121">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> <span data-ttu-id="8ee50-122">如果要[修改并](https://help.github.com/articles/fork-a-repo/)[签入对](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)GitHub 所做的更改，可分叉此存储库供将来参考。</span><span class="sxs-lookup"><span data-stu-id="8ee50-122">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) if you want to modify and check in your changes to GitHub for future reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="8ee50-123">生成和运行示例</span><span class="sxs-lookup"><span data-stu-id="8ee50-123">Build and run the sample</span></span>

<span data-ttu-id="8ee50-124">克隆存储库后，使用Visual Studio从示例的根目录打开解决方案文件，然后 `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` 从菜单中 `Build` 单击。</span><span class="sxs-lookup"><span data-stu-id="8ee50-124">Once the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the root directory of the sample and click `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="8ee50-125">可以通过按或从菜单中 `F5` 选择来 `Start Debugging` 运行 `Debug` 示例。</span><span class="sxs-lookup"><span data-stu-id="8ee50-125">You can run the sample by pressing `F5` or choosing `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="8ee50-126">当应用启动时，你将看到浏览器窗口打开，并且应用的根已启动。</span><span class="sxs-lookup"><span data-stu-id="8ee50-126">When the app starts, you will see a browser window open with the root of the app launched.</span></span> <span data-ttu-id="8ee50-127">你可以导航到以下 URL 以验证是否正在加载所有应用 URL：</span><span class="sxs-lookup"><span data-stu-id="8ee50-127">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="8ee50-128">如果收到类似错误 `Could not find a part of the path … bin\roslyn\csc.exe` ，请尝试使用命令更新程序包 `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。</span><span class="sxs-lookup"><span data-stu-id="8ee50-128">If you receive an error like `Could not find a part of the path … bin\roslyn\csc.exe`, try updating the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="8ee50-129">有关 [其他详细信息，请参阅 StackOverflow](https://stackoverflow.com/questions/32780315) 上的此问题。</span><span class="sxs-lookup"><span data-stu-id="8ee50-129">See [this question on StackOverflow](https://stackoverflow.com/questions/32780315) for additional details.</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="8ee50-130">托管示例应用</span><span class="sxs-lookup"><span data-stu-id="8ee50-130">Host the sample app</span></span>

<span data-ttu-id="8ee50-131">请记住，Microsoft Teams 中的应用是公开一个或多个功能的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8ee50-131">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="8ee50-132">若要让 Teams 平台加载你的应用，必须从 Internet 访问你的应用。</span><span class="sxs-lookup"><span data-stu-id="8ee50-132">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="8ee50-133">若要使应用从 Internet 访问，你需要托管你的应用。</span><span class="sxs-lookup"><span data-stu-id="8ee50-133">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="8ee50-134">你可以免费在 Microsoft Azure 中托管它，或者使用创建到开发计算机上本地进程的隧道 `ngrok` 。</span><span class="sxs-lookup"><span data-stu-id="8ee50-134">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="8ee50-135">托管完应用后，记下其根 URL。</span><span class="sxs-lookup"><span data-stu-id="8ee50-135">When you finish hosting your app make a note of its root URL.</span></span> <span data-ttu-id="8ee50-136">它的外观如下所示：或 `https://yourteamsapp.ngrok.io` `https://yourteamsapp.azurewebsites.net` 。</span><span class="sxs-lookup"><span data-stu-id="8ee50-136">It will look something like: `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="8ee50-137">使用 ngrok 的隧道</span><span class="sxs-lookup"><span data-stu-id="8ee50-137">Tunnel using ngrok</span></span>

<span data-ttu-id="8ee50-138">为了快速测试，可以在本地计算机上运行应用，并通过 Web 终结点创建一个隧道。</span><span class="sxs-lookup"><span data-stu-id="8ee50-138">For quick testing you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="8ee50-139">[ngrok](https://ngrok.com) 是一款免费工具，允许你执行这一操作。</span><span class="sxs-lookup"><span data-stu-id="8ee50-139">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="8ee50-140">通过 ngrok，您可以获取 Web 地址 `https://d0ac14a5.ngrok.io` ， (此 URL 只是一个) 。</span><span class="sxs-lookup"><span data-stu-id="8ee50-140">With ngrok you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="8ee50-141">您可以 [为环境](https://ngrok.com/download) 下载并安装 ngrok。</span><span class="sxs-lookup"><span data-stu-id="8ee50-141">You can [download and install](https://ngrok.com/download) ngrok for your environment.</span></span> <span data-ttu-id="8ee50-142">请确保将其添加到您的位置 `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="8ee50-142">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="8ee50-143">安装后，可以打开一个新的终端窗口并运行以下命令以创建隧道。</span><span class="sxs-lookup"><span data-stu-id="8ee50-143">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="8ee50-144">此示例使用端口 3333，因此请务必在此处指定它。</span><span class="sxs-lookup"><span data-stu-id="8ee50-144">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="8ee50-145">Ngrok 将侦听来自 Internet 的请求，并路由到在端口 3333 上运行的应用。</span><span class="sxs-lookup"><span data-stu-id="8ee50-145">Ngrok will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="8ee50-146">可以通过打开浏览器并加载 `https://d0ac14a5.ngrok.io/hello` 应用的 Hello 页面进行验证。</span><span class="sxs-lookup"><span data-stu-id="8ee50-146">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="8ee50-147">请确保使用 ngrok 在控制台会话中显示的转发地址，而不是此 URL。</span><span class="sxs-lookup"><span data-stu-id="8ee50-147">Please be sure to use the forwarding address displayed by ngrok in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="8ee50-148">如果在以上构建和运行步骤中使用不同的端口[](#build-and-run-the-sample)，请确保使用相同的端口号来设置 `ngrok` 隧道。</span><span class="sxs-lookup"><span data-stu-id="8ee50-148">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="8ee50-149">建议在不同的终端窗口中运行，以保持其运行，而不会影响应用，稍后可能需要停止、重新生成 `ngrok` 和重新运行。</span><span class="sxs-lookup"><span data-stu-id="8ee50-149">It is a good idea to run `ngrok` in a different terminal window to keep it running without interfering with the app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="8ee50-150">会话 `ngrok` 将在此窗口中返回有用的调试信息。</span><span class="sxs-lookup"><span data-stu-id="8ee50-150">The `ngrok` session will return useful debugging information in this window.</span></span>

<span data-ttu-id="8ee50-151">该应用仅在开发计算机上当前会话期间可用。</span><span class="sxs-lookup"><span data-stu-id="8ee50-151">The app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="8ee50-152">如果计算机关闭或进入睡眠状态，服务将不再可用。</span><span class="sxs-lookup"><span data-stu-id="8ee50-152">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="8ee50-153">在共享应用供其他用户进行测试时，请记住这一点。</span><span class="sxs-lookup"><span data-stu-id="8ee50-153">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="8ee50-154">如果必须重新启动服务，它将返回一个新地址，并且必须更新使用该地址的每一位置。</span><span class="sxs-lookup"><span data-stu-id="8ee50-154">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span> <span data-ttu-id="8ee50-155">Ngrok 的付费版本没有此限制。</span><span class="sxs-lookup"><span data-stu-id="8ee50-155">The paid version of Ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="8ee50-156">Azure 中的主机</span><span class="sxs-lookup"><span data-stu-id="8ee50-156">Host in Azure</span></span>

<span data-ttu-id="8ee50-157">Microsoft Azure 允许你使用共享基础结构在免费层托管 .NET 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8ee50-157">Microsoft Azure lets you host your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="8ee50-158">这将足以运行 `Hello World` 此示例。</span><span class="sxs-lookup"><span data-stu-id="8ee50-158">This will be sufficient to run this `Hello World` sample.</span></span> <span data-ttu-id="8ee50-159">有关详细信息 [，请参阅创建新的免费](https://azure.microsoft.com/free/) 帐户。</span><span class="sxs-lookup"><span data-stu-id="8ee50-159">See [creating a new free account](https://azure.microsoft.com/free/) for more information.</span></span>

<span data-ttu-id="8ee50-160">Visual Studio对应用部署到不同提供程序（包括 Azure）的内置支持。</span><span class="sxs-lookup"><span data-stu-id="8ee50-160">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="8ee50-161">更新托管应用的凭据</span><span class="sxs-lookup"><span data-stu-id="8ee50-161">Update the credentials for your hosted app</span></span>

<span data-ttu-id="8ee50-162">示例应用要求将以下环境变量设置为之前记录的值。</span><span class="sxs-lookup"><span data-stu-id="8ee50-162">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="8ee50-163">打开文件appsettings.js文件。</span><span class="sxs-lookup"><span data-stu-id="8ee50-163">Open up the appsettings.json file.</span></span> <span data-ttu-id="8ee50-164">使用之前保存的自动程序 ID 更新 *MicrosoftAppId* 值。</span><span class="sxs-lookup"><span data-stu-id="8ee50-164">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="8ee50-165">使用之前保存的自动程序密码更新 *MicrosoftAppPassword。*</span><span class="sxs-lookup"><span data-stu-id="8ee50-165">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="8ee50-166">进行这些更改后，重新生成应用。</span><span class="sxs-lookup"><span data-stu-id="8ee50-166">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="8ee50-167">如果你使用的是 ngrok，请在本地运行应用，如果你托管在 Azure 中，请重新部署该应用。</span><span class="sxs-lookup"><span data-stu-id="8ee50-167">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="8ee50-168">配置应用选项卡</span><span class="sxs-lookup"><span data-stu-id="8ee50-168">Configure the app tab</span></span>

<span data-ttu-id="8ee50-169">将应用安装到团队后，你需要将其配置为显示内容。</span><span class="sxs-lookup"><span data-stu-id="8ee50-169">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="8ee50-170">转到你安装示例应用的团队中的频道，然后单击 **"+"** 按钮以添加新选项卡。然后，可以从 `Hello World` "添加选项卡 **"列表中选择** 。</span><span class="sxs-lookup"><span data-stu-id="8ee50-170">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="8ee50-171">然后，将显示配置对话框。</span><span class="sxs-lookup"><span data-stu-id="8ee50-171">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="8ee50-172">此对话框将让你选择要在此通道中显示的选项卡。</span><span class="sxs-lookup"><span data-stu-id="8ee50-172">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="8ee50-173">选择该选项卡并单击后，即可看到已加载的 `Save` `Hello World` 选项卡以及您选择的选项卡。</span><span class="sxs-lookup"><span data-stu-id="8ee50-173">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="8ee50-174">在 Teams 中测试机器人</span><span class="sxs-lookup"><span data-stu-id="8ee50-174">Test your bot in Teams</span></span>

<span data-ttu-id="8ee50-175">现在，你可以与 Teams 中的机器人进行交互。</span><span class="sxs-lookup"><span data-stu-id="8ee50-175">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="8ee50-176">选择你注册应用的团队中的频道，然后键入 `@your-bot-name` 。</span><span class="sxs-lookup"><span data-stu-id="8ee50-176">Choose a channel in the team where you registered your app, and type `@your-bot-name`.</span></span> <span data-ttu-id="8ee50-177">这称为 **\@ 提及**。</span><span class="sxs-lookup"><span data-stu-id="8ee50-177">This is called an **\@mention**.</span></span> <span data-ttu-id="8ee50-178">向自动程序发送的任何消息都将作为回复发送回。</span><span class="sxs-lookup"><span data-stu-id="8ee50-178">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="8ee50-179">测试邮件扩展</span><span class="sxs-lookup"><span data-stu-id="8ee50-179">Test your messaging extension</span></span>

<span data-ttu-id="8ee50-180">若要测试消息扩展，可以单击对话视图中输入框下方的三个点。</span><span class="sxs-lookup"><span data-stu-id="8ee50-180">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="8ee50-181">菜单将弹出，并 **包含"Hello World"** 应用。</span><span class="sxs-lookup"><span data-stu-id="8ee50-181">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="8ee50-182">单击它时，你将看到一组随机文本显示。</span><span class="sxs-lookup"><span data-stu-id="8ee50-182">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="8ee50-183">可以选择其中任何一个，并将其插入到对话中。</span><span class="sxs-lookup"><span data-stu-id="8ee50-183">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="8ee50-184">选择随机文本之一，你将在底部看到一张格式化卡片，并准备好随自己的邮件一起发送。</span><span class="sxs-lookup"><span data-stu-id="8ee50-184">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
