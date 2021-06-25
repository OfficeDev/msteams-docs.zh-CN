---
title: 教程 - 使用工具创建第一Node.js
description: 了解如何开始使用 Microsoft Teams 生成Node.js。
keywords: nodejs app Studio node.js入门
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: bbb2e50592eaa8a69a2cd9abda6a17ba2aa0e6bc
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114446"
---
# <a name="build-your-first-microsoft-teams-app-using-nodejs"></a><span data-ttu-id="fb4f0-104">使用应用生成Microsoft Teams应用Node.js</span><span class="sxs-lookup"><span data-stu-id="fb4f0-104">Build your first Microsoft Teams app using Node.js</span></span>

<span data-ttu-id="fb4f0-105">本教程介绍如何使用应用生成首个Microsoft Teams应用Node.js。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-105">In this tutorial, you will learn how to build your very first Microsoft Teams app using Node.js.</span></span> <span data-ttu-id="fb4f0-106">它还将引导你完成以下步骤：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-106">It also walks you through the steps to:</span></span> 

1. [<span data-ttu-id="fb4f0-107">准备环境</span><span class="sxs-lookup"><span data-stu-id="fb4f0-107">Prepare your environment</span></span>](#prepare-environment)
1. [<span data-ttu-id="fb4f0-108">获取先决条件</span><span class="sxs-lookup"><span data-stu-id="fb4f0-108">Get prerequisites</span></span>](#GetPrerequisites)
1. [<span data-ttu-id="fb4f0-109">下载示例</span><span class="sxs-lookup"><span data-stu-id="fb4f0-109">Download the sample</span></span>](#DownloadSample)
1. [<span data-ttu-id="fb4f0-110">生成和运行示例</span><span class="sxs-lookup"><span data-stu-id="fb4f0-110">Build and run the sample</span></span>](#BuildRun)
1. [<span data-ttu-id="fb4f0-111">托管示例应用</span><span class="sxs-lookup"><span data-stu-id="fb4f0-111">Host the sample app</span></span>](#HostSample)
1. [<span data-ttu-id="fb4f0-112">更新托管应用的凭据</span><span class="sxs-lookup"><span data-stu-id="fb4f0-112">Update the credentials for your hosted app</span></span>](#updatecredentials)
1. [<span data-ttu-id="fb4f0-113">配置"应用"选项卡</span><span class="sxs-lookup"><span data-stu-id="fb4f0-113">Configure the app tab</span></span>](#ConfigureTheAppTab)

<a name="prepare-environment"></a>

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

### <a name="download-and-host-your-app"></a><span data-ttu-id="fb4f0-114">下载和托管应用</span><span class="sxs-lookup"><span data-stu-id="fb4f0-114">Download and host your app</span></span>

<span data-ttu-id="fb4f0-115">按照以下步骤在应用程序下载并托管简单的"hello world"Teams。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-115">Follow these steps to download and host a simple "hello world" app in Teams.</span></span>

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a><span data-ttu-id="fb4f0-116">获取先决条件</span><span class="sxs-lookup"><span data-stu-id="fb4f0-116">Get prerequisites</span></span>

<span data-ttu-id="fb4f0-117">若要完成本教程，你需要以下工具。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-117">To complete this tutorial, you need the following tools.</span></span> <span data-ttu-id="fb4f0-118">如果尚未安装，可以通过这些链接进行安装。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-118">If you don't already have them you can install them from these links.</span></span>

- [<span data-ttu-id="fb4f0-119">Git</span><span class="sxs-lookup"><span data-stu-id="fb4f0-119">Git</span></span>](https://git-scm.com/downloads)
- [<span data-ttu-id="fb4f0-120">Node.js 和 NPM</span><span class="sxs-lookup"><span data-stu-id="fb4f0-120">Node.js and NPM</span></span>](https://nodejs.org/)
- <span data-ttu-id="fb4f0-121">获取任何文本编辑器或 IDE。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-121">Get any text editor or IDE.</span></span> <span data-ttu-id="fb4f0-122">你可以免费安装和[Visual Studio Code](https://code.visualstudio.com/download)应用程序。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-122">You can install and use [Visual Studio Code](https://code.visualstudio.com/download) for free.</span></span>

<span data-ttu-id="fb4f0-123">如果在安装过程中看到要向 PATH 添加 、、 和 `git` `node` 的选项， `npm` `code` 请选择这些选项。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-123">If you see options to add `git`, `node`, `npm`, and `code` to the PATH during installation, select the options.</span></span> 

<span data-ttu-id="fb4f0-124">在终端窗口中运行以下代码，验证这些工具是否可用：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-124">Verify that the tools are available by running the following in a terminal window:</span></span>

> [!NOTE]
> <span data-ttu-id="fb4f0-125">使用你最熟悉平台的终端窗口。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-125">Use the terminal window that you are most comfortable with on your platform.</span></span> <span data-ttu-id="fb4f0-126">这些示例使用 Git (中包含的 Bash) ，但这些脚本将在大多数平台上运行。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-126">These examples use Bash (which is included in Git), but these scripts will run on most platforms.</span></span>

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

<span data-ttu-id="fb4f0-127">这些应用程序可能具有不同的版本。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-127">You may have a different version of these applications.</span></span> <span data-ttu-id="fb4f0-128">这应该不是问题，但 gulp 除外。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-128">This should not be a problem, except for gulp.</span></span> <span data-ttu-id="fb4f0-129">对于 gulp，你需要使用版本 4.0.0 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-129">For gulp you'll need to use version 4.0.0 or later.</span></span>

<span data-ttu-id="fb4f0-130">如果没有在终端窗口中安装 gulp (或安装的版本) ，现在在终端窗口中 `npm install gulp` 运行。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-130">If you don't have gulp installed (or have the wrong version installed), do so now by running `npm install gulp` in your terminal window.</span></span>

<span data-ttu-id="fb4f0-131">如果已安装Visual Studio Code，可以运行以下代码验证安装：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-131">If you have installed Visual Studio Code, you can verify the installation by running:</span></span>

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

<span data-ttu-id="fb4f0-132">你可以继续使用此终端窗口运行本教程中遵循的命令。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-132">You can continue to use this terminal window to run the commands that follow in this tutorial.</span></span>

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a><span data-ttu-id="fb4f0-133">下载示例</span><span class="sxs-lookup"><span data-stu-id="fb4f0-133">Download the sample</span></span>

<span data-ttu-id="fb4f0-134">我们提供了简单的 [Hello， World！](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span><span class="sxs-lookup"><span data-stu-id="fb4f0-134">We have provided a simple [Hello, World!](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs)</span></span> <span data-ttu-id="fb4f0-135">示例，以开始。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-135">sample to get you started.</span></span> <span data-ttu-id="fb4f0-136">在终端窗口中，运行以下命令将示例存储库克隆到本地计算机：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-136">In a terminal window, run the following command to clone the sample repository to your local machine:</span></span>

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> <span data-ttu-id="fb4f0-137">如果要[修改和](https://help.github.com/articles/fork-a-repo/)[签入对](https://github.com/OfficeDev/Microsoft-Teams-Samples)存储库所做的更改，可以分叉此存储库GitHub供将来参考。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-137">You can [fork](https://help.github.com/articles/fork-a-repo/) this [repo](https://github.com/OfficeDev/Microsoft-Teams-Samples) if you want to modify and check in your changes to your GitHub repo for future reference.</span></span>

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a><span data-ttu-id="fb4f0-138">生成和运行示例</span><span class="sxs-lookup"><span data-stu-id="fb4f0-138">Build and run the sample</span></span>

<span data-ttu-id="fb4f0-139">克隆存储库后，在终端中运行更改目录命令，将目录更改为示例：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-139">After the repository is cloned, run the change directory command in terminal to change the directory to the sample:</span></span>

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

<span data-ttu-id="fb4f0-140">为了生成示例，需要安装其所有依赖项。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-140">In order to build the sample, you need to install all its dependencies.</span></span> <span data-ttu-id="fb4f0-141">为此，运行以下命令：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-141">Run the following command to do this:</span></span>

```bash
npm install
```

<span data-ttu-id="fb4f0-142">你应该会看到一组依赖项正在安装。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-142">You should see a bunch of dependencies getting installed.</span></span> <span data-ttu-id="fb4f0-143">安装后，可以使用以下命令运行应用：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-143">After installation you can run the app with the following command:</span></span>

```bash
npm start
```

<span data-ttu-id="fb4f0-144">当 Hello-world 应用启动时，它显示在 `App started listening on port 3333` 终端窗口中。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-144">When the hello-world app starts, it displays `App started listening on port 3333` in the terminal window.</span></span>

> [!NOTE]
> <span data-ttu-id="fb4f0-145">如果看到上述消息中显示的端口号不同，这是因为您设置了一个 PORT 环境变量。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-145">If you see a different port number displayed in the message above, it is because you have a PORT environment variable set.</span></span> <span data-ttu-id="fb4f0-146">您可以继续使用该端口，也可以将环境变量更改为 3333。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-146">You can continue to use that port or change your environment variable to 3333.</span></span>

<span data-ttu-id="fb4f0-147">此时，你可以打开浏览器窗口并导航到以下 URL 以验证所有应用 URL 是否正在加载：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-147">At this point, you can open a browser window and navigate to the following URLs to verify that all the app URLs are loading:</span></span>

- `http://localhost:3333`
- `http://localhost:3333/hello`
- `http://localhost:3333/first`
- `http://localhost:3333/second`

<a name="HostSample"></a>

## <a name="deploy-your-sample-app"></a><span data-ttu-id="fb4f0-148">部署示例应用</span><span class="sxs-lookup"><span data-stu-id="fb4f0-148">Deploy your sample app</span></span>

<span data-ttu-id="fb4f0-149">请记住，Microsoft Teams应用程序是公开一个或多个功能的 Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-149">Remember that apps in Microsoft Teams are web applications exposing one or more capabilities.</span></span> <span data-ttu-id="fb4f0-150">若要Teams加载应用，应用必须从 Internet 访问。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-150">For the Teams platform to load your app, your app must be reachable from the internet.</span></span> <span data-ttu-id="fb4f0-151">若要使你的应用从 Internet 上访问，你需要 *托管* 你的应用。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-151">To make your app reachable from the internet, you need to *host* your app.</span></span>

<span data-ttu-id="fb4f0-152">对于本地测试，可以在本地计算机上运行应用，并创建一个使用 Web 终结点的隧道。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-152">For local testing you can run the app on your local machine and create a tunnel to it with a web endpoint.</span></span> <span data-ttu-id="fb4f0-153">[ngrok](https://ngrok.com) 是一款免费工具，允许你这样做。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-153">[ngrok](https://ngrok.com) is a free tool that lets you do just that.</span></span> <span data-ttu-id="fb4f0-154">使用 *ngrok，* 你可以获取 Web 地址 `https://d0ac14a5.ngrok.io` ， (此 URL 只是一个) 。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-154">With *ngrok* you can get a web address such as `https://d0ac14a5.ngrok.io` (this URL is just an example).</span></span> <span data-ttu-id="fb4f0-155">你可以 [为环境下载](https://ngrok.com/download)*并安装 ngrok。*</span><span class="sxs-lookup"><span data-stu-id="fb4f0-155">You can [download and install](https://ngrok.com/download) *ngrok* for your environment.</span></span> <span data-ttu-id="fb4f0-156">请确保将其添加到 中的位置 `PATH` 。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-156">Make sure you add it to a location in your `PATH`.</span></span>

<span data-ttu-id="fb4f0-157">安装后，可以打开一个新的终端窗口并运行以下命令以创建隧道。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-157">After you install it, you can open a new terminal window and run the following command to create a tunnel.</span></span> <span data-ttu-id="fb4f0-158">此示例使用端口 3333，因此请务必在此处指定它：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-158">The sample uses port 3333, so be sure to specify it here:</span></span>

```bash
ngrok http 3333 -host-header=localhost:3333
```

<span data-ttu-id="fb4f0-159">*Ngrok* 将侦听来自 Internet 的请求，并将它们路由到在端口 3333 上运行的应用。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-159">*Ngrok* will listen to requests from the internet and will route them to your app running on port 3333.</span></span> <span data-ttu-id="fb4f0-160">你可以打开浏览器并加载应用的 Hello 页面 `https://d0ac14a5.ngrok.io/hello` 来进行验证。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-160">You can verify by opening your browser and going to `https://d0ac14a5.ngrok.io/hello` to load your app's hello page.</span></span> <span data-ttu-id="fb4f0-161">请务必使用 *ngrok* 在控制台会话中显示的转发地址，而不是此 URL。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-161">Please be sure to use the forwarding address displayed by *ngrok* in your console session instead of this URL.</span></span>

> [!NOTE]
> <span data-ttu-id="fb4f0-162">如果在以上构建和运行步骤中使用不同的端口 [](#build-and-run-the-sample)，请确保使用相同的端口号来设置 *ngrok* 隧道。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-162">If you have used a different port in the [build and run](#build-and-run-the-sample) step above, make sure you use the same port number to setup the *ngrok* tunnel.</span></span>
> [!TIP]
> <span data-ttu-id="fb4f0-163">建议在不同的终端窗口中运行 *ngrok* 以保持其运行，而不会影响节点应用，稍后您可能必须停止、重新生成和重新运行节点应用。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-163">It is a good idea to run *ngrok* in a different terminal window to keep it running without interfering with the node app which you might later have to stop, rebuild and rerun.</span></span> <span data-ttu-id="fb4f0-164">*ngrok* 会话将在此窗口中返回有用的调试信息。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-164">The *ngrok* session will return useful debugging information in this window.</span></span>

<span data-ttu-id="fb4f0-165">存在允许永久名称的 *ngrok* 付费版本。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-165">There is a paid version of *ngrok* that allows persistent names.</span></span> <span data-ttu-id="fb4f0-166">如果你使用免费版本，你的应用将仅在开发计算机上当前会话期间可用。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-166">If you use the free version your app will only be available during the current session on your development machine.</span></span> <span data-ttu-id="fb4f0-167">如果计算机关闭或进入睡眠状态，服务将不再可用。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-167">If the machine is shut down or goes to sleep the service will no longer be available.</span></span> <span data-ttu-id="fb4f0-168">在共享应用供其他用户进行测试时，请记住这一点。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-168">Remember this when sharing the app for testing by other users.</span></span> <span data-ttu-id="fb4f0-169">如果必须重新启动服务，它将返回一个新地址，并且必须更新使用该地址的每一处地址。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-169">If you have to restart the service it will return a new address and you will have to update every place that uses that address.</span></span>

<span data-ttu-id="fb4f0-170">记下应用的 URL。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-170">Make a note of the URL of your app.</span></span> <span data-ttu-id="fb4f0-171">稍后在使用 App studio 或开发人员门户向 Teams注册应用时，将需要此操作。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-171">You will need this later when you register the app with Teams using App studio or Developer Portal.</span></span>

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a><span data-ttu-id="fb4f0-172">将应用部署到Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="fb4f0-172">Deploy your app to Microsoft Teams</span></span>

<span data-ttu-id="fb4f0-173">此时，你拥有一个在 Internet 上托管的应用，但你尚无法告知Teams在哪里查找它，甚至告诉用户你的应用被调用了什么。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-173">At this point you have an app hosted on the internet, but you have no way yet of telling Teams where to look for it, or even what your app is called.</span></span> <span data-ttu-id="fb4f0-174">为此，现在必须创建应用包。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-174">To do this you now have to create an app package.</span></span> <span data-ttu-id="fb4f0-175">这不仅仅是一个包含应用清单和一些图标的文本文件，Teams客户端将使用这些图标来正确显示你的应用并打造你的应用品牌。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-175">This is little more than a text file that contains the app manifest and some icons that the Teams client will use to properly display and brand your app.</span></span> <span data-ttu-id="fb4f0-176">你可以手动创建此应用包，或者可以使用 App Studio 或开发人员门户（在 Teams 中运行的工具）来简化注册应用的过程。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-176">You can manually create this app package, or you can use App Studio or Developer Portal, tools that run in Teams, that will simplify the process of registering the app.</span></span> <span data-ttu-id="fb4f0-177">App Studio 和开发人员门户是创建和更新应用包的推荐方法。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-177">App Studio and Developer Portal are the recommended ways of creating and updating the app package.</span></span>

<span data-ttu-id="fb4f0-178">对于任一方法，你都需要：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-178">For either method you will need the following:</span></span>

- <span data-ttu-id="fb4f0-179">可以在 Internet 上找到应用的 URL。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-179">The URL where your app can be found on the internet.</span></span>
- <span data-ttu-id="fb4f0-180">用于Teams应用品牌的图标。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-180">Icons that Teams will use to brand your app.</span></span> <span data-ttu-id="fb4f0-181">此示例附带位于"src\static\images"中的占位符图标。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-181">The sample comes with placeholder icons located in "src\static\images.</span></span> <span data-ttu-id="fb4f0-182">App Studio 还会根据需要提供默认图标。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-182">App Studio also will provide default icons if needed.</span></span>

<span data-ttu-id="fb4f0-183">**更新应用包**</span><span class="sxs-lookup"><span data-stu-id="fb4f0-183">**Update the app package**</span></span>

# <a name="app-studio"></a>[<span data-ttu-id="fb4f0-184">应用程序 Studio</span><span class="sxs-lookup"><span data-stu-id="fb4f0-184">App Studio</span></span>](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[<span data-ttu-id="fb4f0-185">开发人员门户</span><span class="sxs-lookup"><span data-stu-id="fb4f0-185">Developer Portal</span></span>](#tab/DP)

<span data-ttu-id="fb4f0-186">**安装开发人员门户 (预览) 中Teams**</span><span class="sxs-lookup"><span data-stu-id="fb4f0-186">**To install Developer Portal (preview) in Teams**</span></span>

1. <span data-ttu-id="fb4f0-187">选择 **左侧** 栏底部的"应用"图标，然后搜索"开发人员 **门户"。**</span><span class="sxs-lookup"><span data-stu-id="fb4f0-187">Select the **Apps** icon at the bottom of the left-hand bar, and search for **Developer Portal**.</span></span>

    <img width="430px" alt="Screenshot of TDP" src="~/assets/images/Screen1.png"/>

1. <span data-ttu-id="fb4f0-188">选择 **"开发人员门户"，** 然后选择"打开 **"。**</span><span class="sxs-lookup"><span data-stu-id="fb4f0-188">Select **Developer Portal** and select **Open**.</span></span>

    <img width="430px" alt="Screenshot of TDP Open" src="~/assets/images/screen2.png"/>

1. <span data-ttu-id="fb4f0-189">选择"应用"选项卡，然后选择 **"导入现有应用"。**</span><span class="sxs-lookup"><span data-stu-id="fb4f0-189">Select the Apps tab and select **Import an existing app**.</span></span>

    <img width="430px" alt="Screenshot of import app in tdp" src="~/assets/images/screen3.png"/>

1. <span data-ttu-id="fb4f0-190">选择 **Hello World，\*\*\*\*然后选择导入**。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-190">Select **Hello World** and select **Import**.</span></span> <span data-ttu-id="fb4f0-191">Hello **World** 应用在开发人员门户中导入。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-191">The **Hello World** app is imported in Developer Portal.</span></span> 

    <span data-ttu-id="fb4f0-192">可以使用开发人员门户配置Teams应用。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-192">You can configure your app using the Teams Developer Portal.</span></span> <span data-ttu-id="fb4f0-193">清单位于"分发"下。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-193">The Manifest is found under Distribute.</span></span> <span data-ttu-id="fb4f0-194">可以使用清单为应用配置功能、必需资源和重要的属性。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-194">You can use the Manifest to configure capabilities, required resources, and other important attributes for your app.</span></span> <span data-ttu-id="fb4f0-195">有关如何使用开发人员门户配置应用的更多详细信息，请参阅开发人员Teams[门户](../concepts/build-and-test/teams-developer-portal.md)。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-195">For more details on how to configure your app using Developer Portal, see [Teams Developer Portal](../concepts/build-and-test/teams-developer-portal.md).</span></span>

    <img width="430px" alt="Screenshot of configure tdp" src="~/assets/images/Screen4.png"/>

---
<a name="updatecredentials"></a>

## <a name="update-the-credentials-for-your-hosted-app"></a><span data-ttu-id="fb4f0-196">更新托管应用的凭据</span><span class="sxs-lookup"><span data-stu-id="fb4f0-196">Update the credentials for your hosted app</span></span>

<span data-ttu-id="fb4f0-197">示例应用需要将以下环境变量设置为之前记下的值：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-197">The sample app requires the following environment variables to be set to the values you made a note of earlier:</span></span>

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

<span data-ttu-id="fb4f0-198">具体操作方式因应用托管方式不同而不同。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-198">How you do that differs depending on how you hosted your app.</span></span> <span data-ttu-id="fb4f0-199">使用环境变量的一个重要内容是，这些值是环境的一部分，可通过应用的代码访问它们，但它们不会向可能检查网站文件的第三方公开。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-199">The important thing about using environment variables is that these values are part of your environment - they can be accessed by the code for your app, but they are not exposed to third parties who might examine the files that make up your site.</span></span>

<span data-ttu-id="fb4f0-200">如果使用 ngrok 运行应用，则需要设置一些本地环境变量。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-200">If you are running the app using ngrok you'll need to set up some local environment variables.</span></span> <span data-ttu-id="fb4f0-201">执行此操作的方法有很多，但如果使用的是Visual Studio Code，最简单的方法是添加启动[配置](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-201">There are many ways to do this, but the easiest, if you are using Visual Studio Code, is to add a [launch configuration](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations):</span></span>

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

<span data-ttu-id="fb4f0-202">其中：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-202">Where:</span></span>

<span data-ttu-id="fb4f0-203">MICROSOFT_APP_ID和MICROSOFT_APP_PASSWORD是自动程序 ID 和密码。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-203">MICROSOFT_APP_ID and MICROSOFT_APP_PASSWORD is the ID and password, respectively, for your bot.</span></span>
<span data-ttu-id="fb4f0-204">NODE_DEBUG将在调试控制台中显示自动程序Visual Studio Code发生了什么。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-204">NODE_DEBUG will show you what's happening in your bot in the Visual Studio Code debug console.</span></span>
<span data-ttu-id="fb4f0-205">NODE_CONFIG_DIR指向存储库根目录（默认情况下 (，当本地运行应用时，它将在 src 文件夹的) 。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-205">NODE_CONFIG_DIR points to the directory at the root of the repository (by default, when the app is run locally, it looks for it in the src folder).</span></span>

> [!Note]
> <span data-ttu-id="fb4f0-206">如果你尚未从本教程的前面部分停止 npm，则需要运行 ，以便Visual Studio Code正确拾取启动配置 `npm stop` 变量。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-206">If you have not stopped npm from earlier in the tutorial, you'll need to run `npm stop` in order for Visual Studio Code to pickup your launch configuration variables correctly.</span></span>

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a><span data-ttu-id="fb4f0-207">配置"应用"选项卡</span><span class="sxs-lookup"><span data-stu-id="fb4f0-207">Configure the app tab</span></span>

<span data-ttu-id="fb4f0-208">将应用安装到团队后，你需要将其配置为显示内容。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-208">After you install the app into a team, you will need to configure it to show content.</span></span> <span data-ttu-id="fb4f0-209">转到团队中的频道，然后单击 **"+"** 按钮以添加新选项卡。然后，可以从 `Hello World` "添加 **选项卡"列表中选择** 。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-209">Go to a channel in the team and click on the **'+'** button to add a new tab. You can then choose `Hello World` from the **Add a tab** list.</span></span> <span data-ttu-id="fb4f0-210">然后，你将看到配置对话框。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-210">You will then be presented with a configuration dialog.</span></span> <span data-ttu-id="fb4f0-211">此对话框将让你选择要在此通道中显示哪个选项卡。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-211">This dialog will let you choose which tab to display in this channel.</span></span> <span data-ttu-id="fb4f0-212">选择选项卡并单击"保存 **"** 后，可以看到已加载选项卡 `Hello World` 的选项卡已选择：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-212">After you select the tab and click **Save** you can see the `Hello World` tab loaded with the tab you chose:</span></span>

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a><span data-ttu-id="fb4f0-213">在设备中测试Teams</span><span class="sxs-lookup"><span data-stu-id="fb4f0-213">Test your bot in Teams</span></span>

<span data-ttu-id="fb4f0-214">现在，你可以与自动程序在 Teams。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-214">You can now interact with the bot in Teams.</span></span> <span data-ttu-id="fb4f0-215">选择你注册应用的团队中的频道，然后键入 `@your-bot-name` ，然后键入消息。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-215">Choose a channel in the team where you registered your app, and type `@your-bot-name`, followed by your message.</span></span> <span data-ttu-id="fb4f0-216">这称为 **\@ 提及**。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-216">This is called an **\@mention**.</span></span> <span data-ttu-id="fb4f0-217">发送到自动程序的任何消息都将作为回复发送回：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-217">Whatever message you send to the bot will be sent back to you as a reply:</span></span>

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a><span data-ttu-id="fb4f0-218">测试邮件扩展</span><span class="sxs-lookup"><span data-stu-id="fb4f0-218">Test your messaging extension</span></span>

<span data-ttu-id="fb4f0-219">若要测试消息扩展，可以单击对话视图中输入框下方的三个点。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-219">To test your messaging extension, you can click on the three dots below the input box in your conversation view.</span></span> <span data-ttu-id="fb4f0-220">菜单将弹出，并包含 **"Hello World"** 应用。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-220">A menu will pop up with the **'Hello World'** app in it.</span></span> <span data-ttu-id="fb4f0-221">单击它时，你将看到大量随机文本。</span><span class="sxs-lookup"><span data-stu-id="fb4f0-221">When you click it, you will see a number of random texts.</span></span> <span data-ttu-id="fb4f0-222">可以选择其中任何一个，并将其插入到对话中：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-222">You can choose any one of them and it will be inserted it into your conversation:</span></span>

<img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

<img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

<span data-ttu-id="fb4f0-223">选择随机文本之一，你将在底部看到格式化的卡片，并准备好发送自己的邮件：</span><span class="sxs-lookup"><span data-stu-id="fb4f0-223">Select one of the random texts, and you will see a card formatted and ready to send with your own message at the bottom:</span></span>

<img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

 ## <a name="see-also"></a><span data-ttu-id="fb4f0-224">另请参阅</span><span class="sxs-lookup"><span data-stu-id="fb4f0-224">See also</span></span>

* [<span data-ttu-id="fb4f0-225">教程概述</span><span class="sxs-lookup"><span data-stu-id="fb4f0-225">Tutorials Overview</span></span>](code-samples.md)
* [<span data-ttu-id="fb4f0-226">代码示例</span><span class="sxs-lookup"><span data-stu-id="fb4f0-226">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)