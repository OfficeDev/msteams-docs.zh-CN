---
title: '开始使用 c #/.NET'
description: '使用 c #/.NET 在 Microsoft 团队中开始构建出色的应用程序'
keywords: '入门 .net c # csharp'
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 3aca72a43765036c0014a9e16fa585575fe97b2e
ms.sourcegitcommit: d61f14053fc695bc1956bf50e83956613c19ccca
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/13/2020
ms.locfileid: "48452841"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-cnet-and-app-studio"></a><span data-ttu-id="f1487-104">使用 c #/.NET 和应用程序工作室在 Microsoft 团队平台上开始使用</span><span class="sxs-lookup"><span data-stu-id="f1487-104">Get started on the Microsoft Teams platform with C#/.NET and App Studio</span></span>

<span data-ttu-id="f1487-105">[Microsoft 团队](/microsoftteams/)开发人员平台使您能够轻松扩展团队并将自己的应用程序和服务与团队工作区无缝集成。</span><span class="sxs-lookup"><span data-stu-id="f1487-105">The [Microsoft Teams](/microsoftteams/) developer platform makes it easy for you to extend Teams and integrate your own applications and services seamlessly into the Teams workspace.</span></span> <span data-ttu-id="f1487-106">然后，可以将这些应用分发到企业或世界各地的团队。</span><span class="sxs-lookup"><span data-stu-id="f1487-106">These apps can then be distributed to your enterprise or for teams around the world.</span></span>

<span data-ttu-id="f1487-107">若要扩展 Microsoft 团队，你将需要创建 Microsoft 团队应用。</span><span class="sxs-lookup"><span data-stu-id="f1487-107">To extend Microsoft Teams, you will need to create a Microsoft Teams app.</span></span> <span data-ttu-id="f1487-108">Microsoft 团队应用程序是您承载的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f1487-108">A Microsoft Teams app is a web application that you host.</span></span> <span data-ttu-id="f1487-109">然后，可以将此应用集成到团队中的用户工作区中。</span><span class="sxs-lookup"><span data-stu-id="f1487-109">This app can then be integrated into the user's workspace in Teams.</span></span>

<span data-ttu-id="f1487-110">本教程将帮助您开始使用 .NET 中的 c # 创建 Microsoft 团队应用程序。</span><span class="sxs-lookup"><span data-stu-id="f1487-110">This tutorial helps you get started creating a Microsoft Teams app using C# on .NET.</span></span> <span data-ttu-id="f1487-111">您可以通过将应用程序加载到您有权访问的团队，或使用 Office 开发人员程序创建的测试租户来测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="f1487-111">You can test the app by loading it into a Team that you have permissions for, or into a test tenant created using the Office Developer Program.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="f1487-112">获取先决条件</span><span class="sxs-lookup"><span data-stu-id="f1487-112">Get prerequisites</span></span>

<span data-ttu-id="f1487-113">若要完成本教程，您需要获取以下工具：</span><span class="sxs-lookup"><span data-stu-id="f1487-113">To complete this tutorial, you need to get the following tools:</span></span>

- [<span data-ttu-id="f1487-114">安装 Git</span><span class="sxs-lookup"><span data-stu-id="f1487-114">Install Git</span></span>](https://git-scm.com/downloads)
- <span data-ttu-id="f1487-115">[安装 Visual Studio](https://www.visualstudio.com/downloads/)。</span><span class="sxs-lookup"><span data-stu-id="f1487-115">[Install Visual Studio](https://www.visualstudio.com/downloads/).</span></span> <span data-ttu-id="f1487-116">您可以安装免费社区版。</span><span class="sxs-lookup"><span data-stu-id="f1487-116">You can install the free community edition.</span></span>

<span data-ttu-id="f1487-117">如果您在 `git` 安装过程中看到一个添加到路径的选项，请选择执行此操作。</span><span class="sxs-lookup"><span data-stu-id="f1487-117">If you see an option to add `git` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="f1487-118">这将很方便。</span><span class="sxs-lookup"><span data-stu-id="f1487-118">It will be handy.</span></span>

<span data-ttu-id="f1487-119">`git`通过在终端窗口中运行以下命令来验证您的安装：</span><span class="sxs-lookup"><span data-stu-id="f1487-119">Verify your `git` installation by running the following in a terminal window:</span></span>
> [!NOTE]
> <span data-ttu-id="f1487-120">在你的平台上使用你最舒适的终端窗口。</span><span class="sxs-lookup"><span data-stu-id="f1487-120">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="f1487-121">这些示例使用 Bash，但将在大多数平台上运行。</span><span class="sxs-lookup"><span data-stu-id="f1487-121">These examples use Bash, but will run on most platforms.</span></span>

```bash
$ git --version
git version 2.17.1.windows.2

```

<span data-ttu-id="f1487-122">请务必启动最新版本的 Visual Studio，并安装任何更新（如图所示）。</span><span class="sxs-lookup"><span data-stu-id="f1487-122">Make sure to launch the latest version of Visual Studio and install any updates if shown.</span></span>

<span data-ttu-id="f1487-123">您可以继续使用此终端窗口运行本教程后面的命令。</span><span class="sxs-lookup"><span data-stu-id="f1487-123">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="f1487-124">下载示例</span><span class="sxs-lookup"><span data-stu-id="f1487-124">Download the sample</span></span>

<span data-ttu-id="f1487-125">我们提供了一个简单的 [Hello，World！](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span><span class="sxs-lookup"><span data-stu-id="f1487-125">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)</span></span> <span data-ttu-id="f1487-126">在 c # 中的示例可帮助您入门。</span><span class="sxs-lookup"><span data-stu-id="f1487-126">sample in C# to get you started.</span></span> <span data-ttu-id="f1487-127">在终端窗口中，运行以下命令以将示例存储库克隆到本地计算机：</span><span class="sxs-lookup"><span data-stu-id="f1487-127">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> <span data-ttu-id="f1487-128">如果要将所做的更改修改并签入 GitHub 以供将来参考[，则可以](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)[派生](https://help.github.com/articles/fork-a-repo/)此存储库。</span><span class="sxs-lookup"><span data-stu-id="f1487-128">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) if you want to modify and check in your changes to GitHub for future reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="f1487-129">生成和运行示例</span><span class="sxs-lookup"><span data-stu-id="f1487-129">Build and run the sample</span></span>

<span data-ttu-id="f1487-130">克隆存储库后，使用 Visual Studio 从示例的根目录中打开解决方案文件， `Microsoft.Teams.Samples.HelloWorld.sln` 然后单击 `Build Solution` 菜单中的 `Build` 。</span><span class="sxs-lookup"><span data-stu-id="f1487-130">Once the repo is cloned, use Visual Studio to open the solution file `Microsoft.Teams.Samples.HelloWorld.sln` from the root directory of the sample and click `Build Solution` from the `Build` menu.</span></span> <span data-ttu-id="f1487-131">您可以通过按 `F5` 或 `Start Debugging` 从菜单中选择来运行该示例 `Debug` 。</span><span class="sxs-lookup"><span data-stu-id="f1487-131">You can run the sample by pressing `F5` or choosing `Start Debugging` from the `Debug` menu.</span></span>

<span data-ttu-id="f1487-132">当应用启动时，您将看到一个打开的浏览器窗口，其中启动了应用程序的根目录。</span><span class="sxs-lookup"><span data-stu-id="f1487-132">When the app starts, you will see a browser window open with the root of the app launched.</span></span> <span data-ttu-id="f1487-133">您可以导航到以下 Url，以验证是否已加载所有应用程序 Url：</span><span class="sxs-lookup"><span data-stu-id="f1487-133">You can navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> <span data-ttu-id="f1487-134">如果收到类似的错误 `Could not find a part of the path … bin\roslyn\csc.exe` ，请尝试使用命令更新该包 `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。</span><span class="sxs-lookup"><span data-stu-id="f1487-134">If you receive an error like `Could not find a part of the path … bin\roslyn\csc.exe`, try updating the package with the command `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`.</span></span> <span data-ttu-id="f1487-135">有关更多详细信息，请参阅 [StackOverflow 上的此问题](https://stackoverflow.com/questions/32780315) 。</span><span class="sxs-lookup"><span data-stu-id="f1487-135">See [this question on StackOverflow](https://stackoverflow.com/questions/32780315) for additional details.</span></span>

## <a name="host-the-sample-app"></a><span data-ttu-id="f1487-136">承载示例应用程序</span><span class="sxs-lookup"><span data-stu-id="f1487-136">Host the sample app</span></span>

<span data-ttu-id="f1487-137">请注意，Microsoft 团队中的应用是公开一个或多个功能的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="f1487-137">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="f1487-138">若要使团队平台加载您的应用程序，您的应用程序必须可从 internet 访问。</span><span class="sxs-lookup"><span data-stu-id="f1487-138">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="f1487-139">若要使您的应用程序可从 internet 访问，您需要托管您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f1487-139">To make your app reachable from the internet, you need to host your app.</span></span> <span data-ttu-id="f1487-140">你可以在 Microsoft Azure 中将其托管为免费，或使用在开发计算机上的本地进程创建隧道 `ngrok` 。</span><span class="sxs-lookup"><span data-stu-id="f1487-140">You can either host it in Microsoft Azure for free or create a tunnel to the local process on your development machine using `ngrok`.</span></span> <span data-ttu-id="f1487-141">当您完成应用程序的托管时，请记下其根 URL。</span><span class="sxs-lookup"><span data-stu-id="f1487-141">When you finish hosting your app make a note of its root URL.</span></span> <span data-ttu-id="f1487-142">它的外观如下所示： `https://yourteamsapp.ngrok.io` 或 `https://yourteamsapp.azurewebsites.net` 。</span><span class="sxs-lookup"><span data-stu-id="f1487-142">It will look something like: `https://yourteamsapp.ngrok.io` or `https://yourteamsapp.azurewebsites.net`.</span></span>

### <a name="tunnel-using-ngrok"></a><span data-ttu-id="f1487-143">使用 ngrok 的隧道</span><span class="sxs-lookup"><span data-stu-id="f1487-143">Tunnel using ngrok</span></span>

<span data-ttu-id="f1487-144">若要快速测试，可以在本地计算机上运行应用程序，并通过 web 终结点创建到它的隧道。</span><span class="sxs-lookup"><span data-stu-id="f1487-144">For quick testing you can run the app on your local machine and create a tunnel to it through a web endpoint.</span></span> <span data-ttu-id="f1487-145">[ngrok](https://ngrok.com) 是一个免费工具，可让你做到这一点。</span><span class="sxs-lookup"><span data-stu-id="f1487-145">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="f1487-146">通过 ngrok，您可以获取 web 地址（如 `https://d0ac14a5.ngrok.io` (此 URL 只是一个示例) ）。</span><span class="sxs-lookup"><span data-stu-id="f1487-146">With ngrok you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="f1487-147">您可以为您的环境 [下载并安装](https://ngrok.com/download) ngrok。</span><span class="sxs-lookup"><span data-stu-id="f1487-147">You can [download and install](https://ngrok.com/download) ngrok for your environment.</span></span> <span data-ttu-id="f1487-148">请确保将其添加到中的某个位置 `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="f1487-148">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="f1487-149">安装后，可以打开一个新的终端窗口并运行以下命令来创建隧道。</span><span class="sxs-lookup"><span data-stu-id="f1487-149">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="f1487-150">此示例使用端口3333，因此请务必在此处指定它。</span><span class="sxs-lookup"><span data-stu-id="f1487-150">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="f1487-151">Ngrok 将侦听来自 internet 的请求，并将其路由到在端口3333上运行的应用。</span><span class="sxs-lookup"><span data-stu-id="f1487-151">Ngrok will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="f1487-152">您可以通过打开浏览器并转到 `https://d0ac14a5.ngrok.io/hello` 加载应用程序的 hello 页面来进行验证。</span><span class="sxs-lookup"><span data-stu-id="f1487-152">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="f1487-153">请务必使用控制台会话中由 ngrok 显示的转发地址，而不是此 URL。</span><span class="sxs-lookup"><span data-stu-id="f1487-153">Please be sure to use the forwarding address displayed by ngrok in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="f1487-154">如果您在上面的 " [内部版本" 和 "运行](#build-and-run-the-sample) " 步骤中使用了不同的端口，请确保使用相同的端口号设置 `ngrok` 隧道。</span><span class="sxs-lookup"><span data-stu-id="f1487-154">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the `ngrok` tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="f1487-155">最好 `ngrok` 在不同的终端窗口中运行，以使其保持运行状态，而不影响您稍后可能需要停止、重新生成和重新运行的应用程序。</span><span class="sxs-lookup"><span data-stu-id="f1487-155">It is a good idea to run `ngrok` in a different terminal window to keep it running without interfering with the app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="f1487-156">`ngrok`该会话将在此窗口中返回有用的调试信息。</span><span class="sxs-lookup"><span data-stu-id="f1487-156">The `ngrok` session will return useful debugging information in this window.</span></span>

<span data-ttu-id="f1487-157">应用将仅在开发计算机上的当前会话过程中可用。</span><span class="sxs-lookup"><span data-stu-id="f1487-157">The app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="f1487-158">如果计算机关闭或进入睡眠状态，服务将不再可用。</span><span class="sxs-lookup"><span data-stu-id="f1487-158">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="f1487-159">在共享应用程序以供其他用户测试时，请记住这一点。</span><span class="sxs-lookup"><span data-stu-id="f1487-159">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="f1487-160">如果必须重新启动服务，它将返回一个新地址，并且您必须更新使用该地址的每个位置。</span><span class="sxs-lookup"><span data-stu-id="f1487-160">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span> <span data-ttu-id="f1487-161">付费版本的 Ngrok 没有此限制。</span><span class="sxs-lookup"><span data-stu-id="f1487-161">The paid version of Ngrok does not have this limitation.</span></span>

### <a name="host-in-azure"></a><span data-ttu-id="f1487-162">Azure 中的主机</span><span class="sxs-lookup"><span data-stu-id="f1487-162">Host in Azure</span></span>

<span data-ttu-id="f1487-163">Microsoft Azure 允许你使用共享基础结构将 .NET 应用程序托管在免费的层上。</span><span class="sxs-lookup"><span data-stu-id="f1487-163">Microsoft Azure lets you host your .NET application on a free tier using shared infrastructure.</span></span> <span data-ttu-id="f1487-164">这就足够了运行此 `Hello World` 示例。</span><span class="sxs-lookup"><span data-stu-id="f1487-164">This will be sufficient to run this `Hello World` sample.</span></span> <span data-ttu-id="f1487-165">有关详细信息，请参阅 [创建新的免费帐户](https://azure.microsoft.com/free/) 。</span><span class="sxs-lookup"><span data-stu-id="f1487-165">See [creating a new free account](https://azure.microsoft.com/free/) for more information.</span></span>

<span data-ttu-id="f1487-166">Visual Studio 为对不同提供程序（包括 Azure）的应用程序部署提供内置支持。</span><span class="sxs-lookup"><span data-stu-id="f1487-166">Visual Studio has built-in support for app deployment to different providers, including Azure.</span></span>

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="f1487-167">更新承载的应用程序的凭据</span><span class="sxs-lookup"><span data-stu-id="f1487-167">Update the credentials for your hosted app</span></span>

<span data-ttu-id="f1487-168">示例应用程序需要将以下环境变量设置为您在前面记下的值。</span><span class="sxs-lookup"><span data-stu-id="f1487-168">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

<span data-ttu-id="f1487-169">打开文件上的 appsettings.js。</span><span class="sxs-lookup"><span data-stu-id="f1487-169">Open up the appsettings.json file.</span></span> <span data-ttu-id="f1487-170">使用之前保存的你的 Bot ID 更新 *MicrosoftAppId* 值。</span><span class="sxs-lookup"><span data-stu-id="f1487-170">Update the *MicrosoftAppId* value with your Bot ID that you saved earlier.</span></span> <span data-ttu-id="f1487-171">使用之前保存的 Bot 密码更新 *MicrosoftAppPassword* 。</span><span class="sxs-lookup"><span data-stu-id="f1487-171">Update the *MicrosoftAppPassword* with the Bot password you saved earlier.</span></span>

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

<span data-ttu-id="f1487-172">进行这些更改后，请重新生成应用程序。</span><span class="sxs-lookup"><span data-stu-id="f1487-172">Once these changes are made, rebuild the app.</span></span> <span data-ttu-id="f1487-173">如果您使用的是 ngrok，请在本地运行应用程序，如果您是在 Azure 中托管，请重新部署应用程序。</span><span class="sxs-lookup"><span data-stu-id="f1487-173">If you are using ngrok, run the app locally, and if you are hosting in Azure redeploy the app.</span></span>

## <a name="configure-the-app-tab"></a><span data-ttu-id="f1487-174">配置 "应用程序" 选项卡</span><span class="sxs-lookup"><span data-stu-id="f1487-174">Configure the app tab</span></span>

<span data-ttu-id="f1487-175">将应用程序安装到团队后，需要将其配置为显示内容。</span><span class="sxs-lookup"><span data-stu-id="f1487-175">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="f1487-176">转到安装了示例应用程序的团队中的某个频道，然后单击 **"+"** 按钮以添加新的选项卡。然后，可以 `Hello World` 从 " **添加选项卡** " 列表中进行选择。</span><span class="sxs-lookup"><span data-stu-id="f1487-176">Go to a channel in the team where you installed the sample app and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="f1487-177">随后将显示配置对话框。</span><span class="sxs-lookup"><span data-stu-id="f1487-177">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="f1487-178">此对话框将允许您选择要在此通道中显示的选项卡。</span><span class="sxs-lookup"><span data-stu-id="f1487-178">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="f1487-179">选择选项卡并单击 "打开" 后 `Save` ，即可看到 `Hello World` 使用所选的选项卡加载的选项卡。</span><span class="sxs-lookup"><span data-stu-id="f1487-179">Once you select the tab and click on `Save` then you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="f1487-180">在团队中测试你的 bot</span><span class="sxs-lookup"><span data-stu-id="f1487-180">Test your bot in Teams</span></span>

<span data-ttu-id="f1487-181">现在可以与团队中的 bot 进行交互。</span><span class="sxs-lookup"><span data-stu-id="f1487-181">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="f1487-182">选择您在其中注册应用程序的团队中的频道，然后键入 `@your-bot-name` 。</span><span class="sxs-lookup"><span data-stu-id="f1487-182">Choose a channel in the team where you registered your app, and type `@your-bot-name`.</span></span> <span data-ttu-id="f1487-183">这称为 " \*\* \@ 提及\*\*"。</span><span class="sxs-lookup"><span data-stu-id="f1487-183">This is called an **\@mention**.</span></span> <span data-ttu-id="f1487-184">发送到 bot 的任何邮件都将作为答复发送回您。</span><span class="sxs-lookup"><span data-stu-id="f1487-184">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a><span data-ttu-id="f1487-185">测试消息扩展</span><span class="sxs-lookup"><span data-stu-id="f1487-185">Test your messaging extension</span></span>

<span data-ttu-id="f1487-186">若要测试您的邮件扩展插件，可以单击对话视图中输入框下的三个点。</span><span class="sxs-lookup"><span data-stu-id="f1487-186">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="f1487-187">将弹出一个菜单，其中包含 **"Hello World"** 应用。</span><span class="sxs-lookup"><span data-stu-id="f1487-187">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="f1487-188">当您单击它时，您将看到一组随机文本显示。</span><span class="sxs-lookup"><span data-stu-id="f1487-188">When you click it, you will see a bunch of random texts showing up.</span></span> <span data-ttu-id="f1487-189">您可以选择其中的任何一个，并将其插入到对话中。</span><span class="sxs-lookup"><span data-stu-id="f1487-189">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="f1487-190">选择一种随机文本，您将看到一张卡片的格式并准备好在底部使用您自己的消息进行发送。</span><span class="sxs-lookup"><span data-stu-id="f1487-190">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
