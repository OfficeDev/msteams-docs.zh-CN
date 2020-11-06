---
title: 开始使用应用程序 Studio 和 Node.js
description: 使用 Node.js 和应用程序工作室开始在 Microsoft 团队中构建出色的应用程序
keywords: node.js nodejs App Studio 入门
ms.topic: tutorial
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 3d86738d32c049d31a84c6c47746e275db5e6349
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931811"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-nodejs-and-app-studio"></a><span data-ttu-id="8775b-104">使用 Node.js 和应用程序工作室开始使用 Microsoft 团队平台</span><span class="sxs-lookup"><span data-stu-id="8775b-104">Get started on the Microsoft Teams platform with Node.js and App Studio</span></span>

<span data-ttu-id="8775b-105">[Microsoft 团队](/microsoftteams/)开发人员平台使您能够轻松扩展团队并将自己的应用程序和服务与团队工作区无缝集成。</span><span class="sxs-lookup"><span data-stu-id="8775b-105">The [Microsoft Teams](/microsoftteams/) developer platform makes it easy for you to extend Teams and integrate your own applications and services seamlessly into the Teams workspace.</span></span> <span data-ttu-id="8775b-106">然后，可以将这些应用分发到企业或世界各地的团队。</span><span class="sxs-lookup"><span data-stu-id="8775b-106">These apps can then be distributed to your enterprise or for teams around the world.</span></span>

<span data-ttu-id="8775b-107">若要扩展 Microsoft 团队，您需要创建 Microsoft 团队应用程序。</span><span class="sxs-lookup"><span data-stu-id="8775b-107">To extend Microsoft Teams, you need to create a Microsoft Teams app.</span></span> <span data-ttu-id="8775b-108">Microsoft 团队应用程序是您承载的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8775b-108">A Microsoft Teams app is a web application that you host.</span></span> <span data-ttu-id="8775b-109">然后，可以将此应用集成到团队中的用户工作区中。</span><span class="sxs-lookup"><span data-stu-id="8775b-109">This app can then be integrated into the user's workspace in Teams.</span></span>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a><span data-ttu-id="8775b-110">下载并托管你的应用程序</span><span class="sxs-lookup"><span data-stu-id="8775b-110">Download and host your app</span></span>

<span data-ttu-id="8775b-111">按照以下步骤在团队中下载并托管一个简单的 "hello world" 应用。</span><span class="sxs-lookup"><span data-stu-id="8775b-111">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a><span data-ttu-id="8775b-112">获取先决条件</span><span class="sxs-lookup"><span data-stu-id="8775b-112">Get prerequisites</span></span>

<span data-ttu-id="8775b-113">若要完成本教程，您需要以下工具。</span><span class="sxs-lookup"><span data-stu-id="8775b-113">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="8775b-114">如果尚不具备这些链接，可以从这些链接进行安装。</span><span class="sxs-lookup"><span data-stu-id="8775b-114">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="8775b-115">Git</span><span class="sxs-lookup"><span data-stu-id="8775b-115">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="8775b-116">Node.js 和 NPM</span><span class="sxs-lookup"><span data-stu-id="8775b-116">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="8775b-117">获取任何文本编辑器或 IDE。</span><span class="sxs-lookup"><span data-stu-id="8775b-117">Get any text editor or IDE.</span></span> <span data-ttu-id="8775b-118">您可以免费安装和使用 [Visual Studio Code](https://code.visualstudio.com/download) 。</span><span class="sxs-lookup"><span data-stu-id="8775b-118">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="8775b-119">如果您在 `git` 安装过程中看到要向路径添加、 `node` 、和的选项，请 `npm` `code` 选择执行此操作。</span><span class="sxs-lookup"><span data-stu-id="8775b-119">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, choose to do so.</span></span> <span data-ttu-id="8775b-120">这将很方便。</span><span class="sxs-lookup"><span data-stu-id="8775b-120">It will be handy.</span></span>

<span data-ttu-id="8775b-121">在终端窗口中运行以下命令，验证这些工具是否可用：</span><span class="sxs-lookup"><span data-stu-id="8775b-121">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="8775b-122">在你的平台上使用你最舒适的终端窗口。</span><span class="sxs-lookup"><span data-stu-id="8775b-122">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="8775b-123">这些示例使用在 Git) 中包含的 Bash (，但这些脚本将在大多数平台上运行。</span><span class="sxs-lookup"><span data-stu-id="8775b-123">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 2.3.0
Local version 4.0.2
```

<span data-ttu-id="8775b-124">您可能具有这些应用程序的不同版本。</span><span class="sxs-lookup"><span data-stu-id="8775b-124">You may have a different version of these applications.</span></span> <span data-ttu-id="8775b-125">这不应是问题，gulp 除外。</span><span class="sxs-lookup"><span data-stu-id="8775b-125">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="8775b-126">对于 gulp，你将需要使用版本4.0.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="8775b-126">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="8775b-127">如果未 (安装 gulp，或者安装了错误的版本) ，请立即 `npm install gulp` 在终端窗口中运行以执行此操作。</span><span class="sxs-lookup"><span data-stu-id="8775b-127">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="8775b-128">如果已安装 Visual Studio Code，可以通过运行以下命令来验证安装：</span><span class="sxs-lookup"><span data-stu-id="8775b-128">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="8775b-129">您可以继续使用此终端窗口运行本教程后面的命令。</span><span class="sxs-lookup"><span data-stu-id="8775b-129">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a><span data-ttu-id="8775b-130">下载示例</span><span class="sxs-lookup"><span data-stu-id="8775b-130">Download the sample</span></span>

<span data-ttu-id="8775b-131">我们提供了一个简单的 [Hello，World！](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span><span class="sxs-lookup"><span data-stu-id="8775b-131">We have provided a simple [Hello, World!](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)</span></span> <span data-ttu-id="8775b-132">入门示例。</span><span class="sxs-lookup"><span data-stu-id="8775b-132">sample to get you started.</span></span> <span data-ttu-id="8775b-133">在终端窗口中，运行以下命令以将示例存储库克隆到本地计算机：</span><span class="sxs-lookup"><span data-stu-id="8775b-133">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-nodejs.git
```

> [!TIP]
> <span data-ttu-id="8775b-134">[如果要](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)修改和签入 GitHub 存储库的更改，以供将来参考，可以[派生](https://help.github.com/articles/fork-a-repo/)此存储库。</span><span class="sxs-lookup"><span data-stu-id="8775b-134">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a><span data-ttu-id="8775b-135">生成和运行示例</span><span class="sxs-lookup"><span data-stu-id="8775b-135">Build and run the sample</span></span>

<span data-ttu-id="8775b-136">克隆存储库后，转到包含示例的目录：</span><span class="sxs-lookup"><span data-stu-id="8775b-136">Once the repo is cloned, change to the directory that holds the sample:</span></span>

```bash
cd msteams-samples-hello-world-nodejs
```

<span data-ttu-id="8775b-137">为了生成示例，您需要安装其所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="8775b-137">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="8775b-138">运行以下命令来执行此操作：</span><span class="sxs-lookup"><span data-stu-id="8775b-138">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="8775b-139">您应该会看到一组已安装的依赖项。</span><span class="sxs-lookup"><span data-stu-id="8775b-139">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="8775b-140">完成后，您可以运行应用程序：</span><span class="sxs-lookup"><span data-stu-id="8775b-140">Once they are finished, you can run the app:</span></span>

```bash
npm start
```

<span data-ttu-id="8775b-141">当 hello world 应用程序启动时，它将显示 `App started listening on port 3333` 在终端窗口中。</span><span class="sxs-lookup"><span data-stu-id="8775b-141">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="8775b-142">如果您看到上面的消息中显示了不同的端口号，则是因为您有一个端口环境变量集。</span><span class="sxs-lookup"><span data-stu-id="8775b-142">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="8775b-143">您可以继续使用该端口或将环境变量更改为3333。</span><span class="sxs-lookup"><span data-stu-id="8775b-143">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="8775b-144">此时，您可以打开浏览器窗口并导航到以下 Url，以验证是否已加载所有应用程序 Url：</span><span class="sxs-lookup"><span data-stu-id="8775b-144">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a><span data-ttu-id="8775b-145">承载示例应用程序</span><span class="sxs-lookup"><span data-stu-id="8775b-145">Host the sample app</span></span>

<span data-ttu-id="8775b-146">请注意，Microsoft 团队中的应用是公开一个或多个功能的 web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="8775b-146">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="8775b-147">若要使团队平台加载您的应用程序，您的应用程序必须可从 internet 访问。</span><span class="sxs-lookup"><span data-stu-id="8775b-147">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="8775b-148">若要使您的应用程序可从 internet 访问，您需要 *托管* 您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="8775b-148">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="8775b-149">对于本地测试，可以在本地计算机上运行应用程序，并使用 web 终结点创建与之的隧道。</span><span class="sxs-lookup"><span data-stu-id="8775b-149">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="8775b-150">[ngrok](https://ngrok.com) 是一个免费工具，可让你做到这一点。</span><span class="sxs-lookup"><span data-stu-id="8775b-150">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="8775b-151">通过 *ngrok* ，您可以获取 web 地址（如 `https://d0ac14a5.ngrok.io` (此 URL 只是一个示例) ）。</span><span class="sxs-lookup"><span data-stu-id="8775b-151">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="8775b-152">您可以为您的环境 [下载并安装](https://ngrok.com/download) *ngrok* 。</span><span class="sxs-lookup"><span data-stu-id="8775b-152">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="8775b-153">请确保将其添加到中的某个位置 `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="8775b-153">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="8775b-154">安装后，可以打开一个新的终端窗口并运行以下命令来创建隧道。</span><span class="sxs-lookup"><span data-stu-id="8775b-154">Once you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="8775b-155">此示例使用端口3333，因此请务必在此处指定它。</span><span class="sxs-lookup"><span data-stu-id="8775b-155">The sample uses port 3333, so be sure to specify it here.</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="8775b-156">*Ngrok* 将侦听来自 internet 的请求，并将其路由到在端口3333上运行的应用。</span><span class="sxs-lookup"><span data-stu-id="8775b-156">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="8775b-157">您可以通过打开浏览器并转到 `https://d0ac14a5.ngrok.io/hello` 加载应用程序的 hello 页面来进行验证。</span><span class="sxs-lookup"><span data-stu-id="8775b-157">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="8775b-158">请务必使用控制台会话中由 *ngrok* 显示的转发地址，而不是此 URL。</span><span class="sxs-lookup"><span data-stu-id="8775b-158">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="8775b-159">如果您在上面的 " [内部版本" 和 "运行](#build-and-run-the-sample) " 步骤中使用了不同的端口，请确保使用相同的端口号设置 *ngrok* 隧道。</span><span class="sxs-lookup"><span data-stu-id="8775b-159">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="8775b-160">最好在不同的终端窗口中运行 *ngrok* ，使其保持运行状态，而不会干扰您稍后可能需要停止、重新生成和重新运行的节点应用。</span><span class="sxs-lookup"><span data-stu-id="8775b-160">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="8775b-161">*Ngrok* 会话将在此窗口中返回有用的调试信息。</span><span class="sxs-lookup"><span data-stu-id="8775b-161">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="8775b-162">有 *ngrok* 的付费版本允许使用永久名称。</span><span class="sxs-lookup"><span data-stu-id="8775b-162">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="8775b-163">如果您使用的是免费版本，应用程序将仅在开发计算机上的当前会话过程中可用。</span><span class="sxs-lookup"><span data-stu-id="8775b-163">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="8775b-164">如果计算机关闭或进入睡眠状态，服务将不再可用。</span><span class="sxs-lookup"><span data-stu-id="8775b-164">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="8775b-165">在共享应用程序以供其他用户测试时，请记住这一点。</span><span class="sxs-lookup"><span data-stu-id="8775b-165">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="8775b-166">如果必须重新启动服务，它将返回一个新地址，并且您必须更新使用该地址的每个位置。</span><span class="sxs-lookup"><span data-stu-id="8775b-166">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="8775b-167">请记住，请记下你的应用程序的 URL，因为你稍后在使用应用程序 studio 向团队注册应用时将需要这样做。</span><span class="sxs-lookup"><span data-stu-id="8775b-167">Remember, make a note of the URL of your app because you will need this later when you register the app with Teams using App studio.</span></span> <span data-ttu-id="8775b-168">为了实现此目的，记事本工作正常。</span><span class="sxs-lookup"><span data-stu-id="8775b-168">Notepad works fine for this purpose.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="8775b-169">将应用程序部署到 Microsoft 团队</span><span class="sxs-lookup"><span data-stu-id="8775b-169">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="8775b-170">此时，您有一个托管在 internet 上的应用程序，但您还没有办法告诉团队在哪里查找它，甚至您的应用程序已被调用。</span><span class="sxs-lookup"><span data-stu-id="8775b-170">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="8775b-171">若要执行此操作，您现在必须创建一个应用程序包。</span><span class="sxs-lookup"><span data-stu-id="8775b-171">To do this you now have to create an app package.</span></span> <span data-ttu-id="8775b-172">这只是一个文本文件，其中包含应用程序清单和一些图标，团队客户端将使用这些图标来正确地显示应用程序并为其打造品牌。</span><span class="sxs-lookup"><span data-stu-id="8775b-172">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="8775b-173">您可以手动创建此应用程序包，也可以使用应用程序工作室（在将简化应用程序注册过程的团队中运行的工具）。</span><span class="sxs-lookup"><span data-stu-id="8775b-173">You can manually create this app package, or you can use App Studio, a tool that runs in Teams that will simplify the process of registering the app.</span></span> <span data-ttu-id="8775b-174">应用程序使用 Studio 是创建和更新应用程序包的推荐方法。</span><span class="sxs-lookup"><span data-stu-id="8775b-174">App Studio is the recommended way of creating and updating the app package.</span></span>

<span data-ttu-id="8775b-175">对于这两种方法，您都需要以下各项：</span><span class="sxs-lookup"><span data-stu-id="8775b-175">For either method you will need the following:</span></span>

- <span data-ttu-id="8775b-176">在 internet 上可以找到你的应用程序的 URL。</span><span class="sxs-lookup"><span data-stu-id="8775b-176">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="8775b-177">团队将用来为你的应用程序建立品牌的图标。</span><span class="sxs-lookup"><span data-stu-id="8775b-177">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="8775b-178">示例附带了位于 "src\static\images." 中的占位符图标。</span><span class="sxs-lookup"><span data-stu-id="8775b-178">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="8775b-179">如果需要，应用程序 Studio 还将提供默认图标。</span><span class="sxs-lookup"><span data-stu-id="8775b-179">App Studio also will provide default icons if needed.</span></span>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a><span data-ttu-id="8775b-180">更新承载的应用程序</span><span class="sxs-lookup"><span data-stu-id="8775b-180">Update your hosted app</span></span>

<span data-ttu-id="8775b-181">示例应用程序需要将以下环境变量设置为您在前面记下的值。</span><span class="sxs-lookup"><span data-stu-id="8775b-181">The sample app requires the following environment variables to be set to the values you made a note of earlier.</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="8775b-182">执行此操作的方式取决于您的应用程序的承载方式。</span><span class="sxs-lookup"><span data-stu-id="8775b-182">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="8775b-183">使用环境变量的重要一点是，这些值是环境的一部分-可以通过应用程序的代码来访问它们，但它们不会向可能检查构成网站的文件的第三方公开。</span><span class="sxs-lookup"><span data-stu-id="8775b-183">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="8775b-184">如果您正在使用 ngrok 运行应用程序，则需要设置一些本地环境变量。</span><span class="sxs-lookup"><span data-stu-id="8775b-184">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="8775b-185">有多种方法可以实现此目的，但如果您使用 Visual Studio Code，最简单的方法是添加 [启动配置](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)：</span><span class="sxs-lookup"><span data-stu-id="8775b-185">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

``` 
{
    "type": "node",
    "request": "launch",
    "name": "Launch - Teams Debug",
    "program": "${workspaceRoot}/src/app.js",
    "cwd": "${workspaceFolder}/src",
    "env": {
        "BASE_URI": "https://yourNgrokURL.ngrok.io",
        "MICROSOFT_APP_ID": "00000000-0000-0000-0000-000000000000",
        "MICROSOFT_APP_PASSWORD": "yourBotAppPassword",
        "NODE_DEBUG": "botbuilder",
        "SUPPRESS_NO_CONFIG_WARNING": "y",
        "NODE_CONFIG_DIR": "../config"
    }
}
```

<span data-ttu-id="8775b-186">其中：</span><span class="sxs-lookup"><span data-stu-id="8775b-186">Where:</span></span>

<span data-ttu-id="8775b-187">MICROSOFT_APP_ID 和 MICROSOFT_APP_PASSWORD 分别是您的 bot 的 ID 和密码。</span><span class="sxs-lookup"><span data-stu-id="8775b-187">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="8775b-188">NODE_DEBUG 将在 Visual Studio Code 调试控制台中显示你的 bot 中发生的情况。</span><span class="sxs-lookup"><span data-stu-id="8775b-188">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="8775b-189">NODE_CONFIG_DIR 指向存储库根目录下的目录 (默认情况下，在本地运行应用程序时，它会在 src 文件夹) 中查找它。</span><span class="sxs-lookup"><span data-stu-id="8775b-189">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="8775b-190">如果您在本教程的前面部分没有停止 npm，则需要运行 `npm stop` Visual Studio 代码，以便正确地拾取您的启动配置变量。</span><span class="sxs-lookup"><span data-stu-id="8775b-190">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="8775b-191">配置 "应用程序" 选项卡</span><span class="sxs-lookup"><span data-stu-id="8775b-191">Configure the app tab</span></span>

<span data-ttu-id="8775b-192">将应用程序安装到团队后，需要将其配置为显示内容。</span><span class="sxs-lookup"><span data-stu-id="8775b-192">Once you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="8775b-193">转到团队中的频道并单击 **"+"** 按钮以添加新的选项卡。然后，可以 `Hello World` 从 " **添加选项卡** " 列表中进行选择。</span><span class="sxs-lookup"><span data-stu-id="8775b-193">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="8775b-194">随后将显示配置对话框。</span><span class="sxs-lookup"><span data-stu-id="8775b-194">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="8775b-195">此对话框将允许您选择要在此通道中显示的选项卡。</span><span class="sxs-lookup"><span data-stu-id="8775b-195">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="8775b-196">选择选项卡并单击 "" 时， `Save` 可以看到在所 `Hello World` 选的选项卡上加载的选项卡。</span><span class="sxs-lookup"><span data-stu-id="8775b-196">Once you select the tab and click on `Save` you can see the `Hello World` tab loaded with the tab you chose.</span></span>

<img width="430px" src="~/assets/images/samples-hello-world-tab-configure.png" alt-text="Screenshot of configure" />

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="8775b-197">在团队中测试你的 bot</span><span class="sxs-lookup"><span data-stu-id="8775b-197">Test your bot in Teams</span></span>

<span data-ttu-id="8775b-198">现在可以与团队中的 bot 进行交互。</span><span class="sxs-lookup"><span data-stu-id="8775b-198">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="8775b-199">选择您在其中注册应用程序的团队中的频道，然后键入，然后键入 `@your-bot-name` 您的消息。</span><span class="sxs-lookup"><span data-stu-id="8775b-199">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="8775b-200">这称为 " **\@ 提及** "。</span><span class="sxs-lookup"><span data-stu-id="8775b-200">This is called an **\@mention**.</span></span> <span data-ttu-id="8775b-201">发送到 bot 的任何邮件都将作为答复发送回您。</span><span class="sxs-lookup"><span data-stu-id="8775b-201">Whatever message you send to the bot will be sent back to you as a reply.</span></span>

<img width="450px" alt-text="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="8775b-202">测试消息扩展</span><span class="sxs-lookup"><span data-stu-id="8775b-202">Test your messaging extension</span></span>

<span data-ttu-id="8775b-203">若要测试您的邮件扩展插件，可以单击对话视图中输入框下的三个点。</span><span class="sxs-lookup"><span data-stu-id="8775b-203">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="8775b-204">将弹出一个菜单，其中包含 **"Hello World"** 应用。</span><span class="sxs-lookup"><span data-stu-id="8775b-204">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="8775b-205">当您单击它时，您将看到大量随机文本。</span><span class="sxs-lookup"><span data-stu-id="8775b-205">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="8775b-206">您可以选择其中的任何一个，并将其插入到对话中。</span><span class="sxs-lookup"><span data-stu-id="8775b-206">You can choose any one of them and it will be inserted it into your conversation.</span></span>

<img width="430px" alt-text="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt-text="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

<span data-ttu-id="8775b-207">选择一种随机文本，您将看到一张卡片的格式并准备好在底部使用您自己的消息进行发送。</span><span class="sxs-lookup"><span data-stu-id="8775b-207">Choose one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom.</span></span>

<img width="430px" alt-text="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
