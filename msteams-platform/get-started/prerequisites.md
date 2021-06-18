---
title: 入门 - 先决条件
author: adrianhall
description: 了解如何开始使用 Microsoft Teams 应用开发和设置环境。
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 6496d238b3858c1df974732fa57c28eed7c54eb2
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994187"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a><span data-ttu-id="6a53e-103">先决条件：Microsoft Teams 应用开发入门</span><span class="sxs-lookup"><span data-stu-id="6a53e-103">Prerequisites: Get started with Microsoft Teams app development</span></span>

<span data-ttu-id="6a53e-104">创建第一个 Teams 应用之前，必须安装一些工具并设置开发环境。</span><span class="sxs-lookup"><span data-stu-id="6a53e-104">Before your create your first Teams app, you must install a few tools and set up your development environment.</span></span>

## <a name="install-required-tools"></a><span data-ttu-id="6a53e-105">安装所需的工具</span><span class="sxs-lookup"><span data-stu-id="6a53e-105">Install required tools</span></span>

<span data-ttu-id="6a53e-106">你需要的一些工具取决于你更喜欢如何生成 Teams 应用：</span><span class="sxs-lookup"><span data-stu-id="6a53e-106">Some of the tools you need depend on how you you prefer to build your Teams app:</span></span>

- <span data-ttu-id="6a53e-107">[Node.js(](https://nodejs.org/en/download/) 使用最新的 v14 LTS 版本) </span><span class="sxs-lookup"><span data-stu-id="6a53e-107">[Node.js](https://nodejs.org/en/download/) (use the latest v14 LTS release)</span></span>
- <span data-ttu-id="6a53e-108">具有开发人员工具的浏览器 - 如 [Microsoft Edge](https://www.microsoft.com/edge) (推荐) Google [Chrome](https://www.google.com/chrome/)</span><span class="sxs-lookup"><span data-stu-id="6a53e-108">A browser with developer tools - such as [Microsoft Edge](https://www.microsoft.com/edge) (recommended) or [Google Chrome](https://www.google.com/chrome/)</span></span>
- <span data-ttu-id="6a53e-109">如果使用 JavaScript、TypeScript 或 SharePoint 框架 (SPFx) ，请安装 Visual Studio [Code](https://code.visualstudio.com/download)版本 1.55 或更高版本。</span><span class="sxs-lookup"><span data-stu-id="6a53e-109">If you are developing with JavaScript, TypeScript, or the SharePoint Framework (SPFx), install [Visual Studio Code](https://code.visualstudio.com/download), version 1.55 or later.</span></span>  
- <span data-ttu-id="6a53e-110">如果要使用 .NET 进行开发，请安装[Visual Studio 2019。](https://visualstudio.com/download)</span><span class="sxs-lookup"><span data-stu-id="6a53e-110">If you are developing with .NET, install [Visual Studio 2019](https://visualstudio.com/download).</span></span> <span data-ttu-id="6a53e-111">确保安装 ASP.NET **Web 开发** 或 **.NET Core 跨平台开发** 工作负载。</span><span class="sxs-lookup"><span data-stu-id="6a53e-111">Ensure you install the **ASP.NET and web development** or **.NET Core cross-platform development** workload.</span></span>

> [!WARNING]
> <span data-ttu-id="6a53e-112">存在与 打包在 Node `npm@7` v15 及更高版本中的已知问题。</span><span class="sxs-lookup"><span data-stu-id="6a53e-112">There are known issues with `npm@7`, packaged with Node v15 and later.</span></span> <span data-ttu-id="6a53e-113">如果在运行时遇到问题 `npm install` ，请确保使用节点 v14 (LTS) </span><span class="sxs-lookup"><span data-stu-id="6a53e-113">If you have problems running `npm install`, ensure you're using Node v14 (LTS)</span></span>

## <a name="install-the-teams-toolkit"></a><span data-ttu-id="6a53e-114">安装 Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="6a53e-114">Install the Teams Toolkit</span></span>

<span data-ttu-id="6a53e-115">Teams Toolkit使用工具为应用预配和部署云资源、发布到 Teams 应用商店等，帮助简化开发过程。</span><span class="sxs-lookup"><span data-stu-id="6a53e-115">The Teams Toolkit helps simplify the development process with tools to provision and deploy cloud resources for your app, publish to the Teams store, and more.</span></span> <span data-ttu-id="6a53e-116">你可以将工具包与Visual Studio代码、Visual Studio或称为 (CLI `teamsfx`) 。</span><span class="sxs-lookup"><span data-stu-id="6a53e-116">You can use the toolkit with Visual Studio Code, Visual Studio, or as a CLI (called `teamsfx`).</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="6a53e-117">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="6a53e-117">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="6a53e-118">打开 Visual Studio 代码。</span><span class="sxs-lookup"><span data-stu-id="6a53e-118">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="6a53e-119">Select the Extensions view (**Ctrl+Shift+X**  /  **⌘⇧-X** or **View > Extensions**) .</span><span class="sxs-lookup"><span data-stu-id="6a53e-119">Select the Extensions view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions**).</span></span>
1. <span data-ttu-id="6a53e-120">在搜索框中，输入 **Teams Toolkit**。</span><span class="sxs-lookup"><span data-stu-id="6a53e-120">In the search box, enter **Teams Toolkit**.</span></span>
1. <span data-ttu-id="6a53e-121">选择 Teams 应用旁边的绿色安装Toolkit。</span><span class="sxs-lookup"><span data-stu-id="6a53e-121">Select the green install button next to the Teams Toolkit.</span></span>

<span data-ttu-id="6a53e-122">还可以在"Toolkit代码Visual Studio [上找到 Teams 服务](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。</span><span class="sxs-lookup"><span data-stu-id="6a53e-122">You also can find the Teams Toolkit on the [Visual Studio Code Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension).</span></span>

<span data-ttu-id="6a53e-123">如果需要，可以使用代码扩展Visual Studio安装以下工具。</span><span class="sxs-lookup"><span data-stu-id="6a53e-123">The following tools can be installed by the Visual Studio Code extension when they are needed.</span></span> <span data-ttu-id="6a53e-124">如果已安装，可以改为使用已安装的版本。</span><span class="sxs-lookup"><span data-stu-id="6a53e-124">If already installed, the installed version can be used instead.</span></span> <span data-ttu-id="6a53e-125">如果使用 Linux（包括 WSL），则必须先安装这些工具，然后才能使用：</span><span class="sxs-lookup"><span data-stu-id="6a53e-125">If using Linux including WSL, you must install these tools before use:</span></span>

- [<span data-ttu-id="6a53e-126">Azure 函数核心工具</span><span class="sxs-lookup"><span data-stu-id="6a53e-126">Azure Functions Core Tools</span></span>](/azure/azure-functions/functions-run-local)

    <span data-ttu-id="6a53e-127">Azure Functions Core Tools 用于在本地调试运行期间在本地运行任何后端组件，包括在 Azure 中运行服务时所需的身份验证帮助程序。</span><span class="sxs-lookup"><span data-stu-id="6a53e-127">Azure Functions Core Tools is used to run any backend components locally during a local debug run, including the authentication helpers required when running your services in Azure.</span></span> <span data-ttu-id="6a53e-128">它使用 npm (安装在项目目录中 `devDependencies`) 。</span><span class="sxs-lookup"><span data-stu-id="6a53e-128">It is installed within the project directory (using the npm `devDependencies`).</span></span>

- [<span data-ttu-id="6a53e-129">.NET SDK</span><span class="sxs-lookup"><span data-stu-id="6a53e-129">.NET SDK</span></span>](/dotnet/core/install/)

    <span data-ttu-id="6a53e-130">.NET SDK 用于安装用于本地调试和 Azure Functions 应用部署的自定义绑定。</span><span class="sxs-lookup"><span data-stu-id="6a53e-130">The .NET SDK is used to install customized bindings for local debugging and Azure Functions app deployments.</span></span> <span data-ttu-id="6a53e-131">如果尚未全局安装 .NET 3.1 (或更高版本) SDK，可以安装可移植版本。</span><span class="sxs-lookup"><span data-stu-id="6a53e-131">If you have not installed the .NET 3.1 (or later) SDK globally, the portable version can be installed.</span></span>

- [<span data-ttu-id="6a53e-132">ngrok</span><span class="sxs-lookup"><span data-stu-id="6a53e-132">ngrok</span></span>](https://ngrok.com/download)

    <span data-ttu-id="6a53e-133">一些 Teams 应用 (对话机器人、消息传递扩展和传入 webhook) 需要入站连接。</span><span class="sxs-lookup"><span data-stu-id="6a53e-133">Some Teams app features (conversational bots, messaging extensions, and incoming webhooks) require inbound connections.</span></span> <span data-ttu-id="6a53e-134">你需要通过隧道向 Teams 公开你的开发系统。</span><span class="sxs-lookup"><span data-stu-id="6a53e-134">You need to expose your development system to Teams through a tunnel.</span></span> <span data-ttu-id="6a53e-135">仅包含选项卡的应用不需要隧道。</span><span class="sxs-lookup"><span data-stu-id="6a53e-135">A tunnel is not required for apps that only include tabs.</span></span> <span data-ttu-id="6a53e-136">此包安装在项目目录中， (npm `devDependencies`) 。</span><span class="sxs-lookup"><span data-stu-id="6a53e-136">This package is installed within the project directory (using npm `devDependencies`).</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="6a53e-137">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="6a53e-137">Visual Studio 2019</span></span>](#tab/vs)

<span data-ttu-id="6a53e-138">可以使用 Visual Studio 2019 在 .NET 中通过 Blazor Server 开发 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="6a53e-138">You can use Visual Studio 2019 to develop Teams apps with Blazor Server in .NET.</span></span> <span data-ttu-id="6a53e-139">如果不打算在 .NET 中开发 Teams 应用，请安装 Visual Studio Code 版本的 Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="6a53e-139">If you are not intending to develop Teams apps in .NET, install the Visual Studio Code version of Teams Toolkit.</span></span>

<span data-ttu-id="6a53e-140">若要安装 Teams Toolkit扩展：</span><span class="sxs-lookup"><span data-stu-id="6a53e-140">To install the Teams Toolkit extension:</span></span>

1. <span data-ttu-id="6a53e-141">打开Visual Studio 2019。</span><span class="sxs-lookup"><span data-stu-id="6a53e-141">Open Visual Studio 2019.</span></span>
1. <span data-ttu-id="6a53e-142">选择 **扩展**  >  **管理扩展**。</span><span class="sxs-lookup"><span data-stu-id="6a53e-142">Select **Extensions** > **Manage Extensions**.</span></span>
1. <span data-ttu-id="6a53e-143">在搜索框中，输入 **Teams Toolkit**。</span><span class="sxs-lookup"><span data-stu-id="6a53e-143">In the search box, enter **Teams Toolkit**.</span></span>
1. <span data-ttu-id="6a53e-144">选择 Teams Toolkit扩展， **然后选择下载**。</span><span class="sxs-lookup"><span data-stu-id="6a53e-144">Select the Teams Toolkit extension and select **Download**.</span></span>

<span data-ttu-id="6a53e-145">可以下载扩展。</span><span class="sxs-lookup"><span data-stu-id="6a53e-145">The extension can be downloaded.</span></span> <span data-ttu-id="6a53e-146">关闭 Visual Studio 2019 以安装扩展。</span><span class="sxs-lookup"><span data-stu-id="6a53e-146">Close Visual Studio 2019 to install the extension.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="6a53e-147">命令行</span><span class="sxs-lookup"><span data-stu-id="6a53e-147">Command line</span></span>](#tab/cli)

<span data-ttu-id="6a53e-148">若要安装 TeamsFx CLI，请使用 `npm` 程序包管理器：</span><span class="sxs-lookup"><span data-stu-id="6a53e-148">To install the TeamsFx CLI, use the `npm` package manager:</span></span>

``` bash
npm install -g @microsoft/teamsfx-cli
```

<span data-ttu-id="6a53e-149">根据您的配置，您可能需要使用 安装 `sudo` CLI：</span><span class="sxs-lookup"><span data-stu-id="6a53e-149">Depending on your configuration, you may need to use `sudo` to install the CLI:</span></span>

``` bash
sudo npm install -g --unsafe-perm @microsoft/teamsfx-cli
```

<span data-ttu-id="6a53e-150">这更常见于 Linux 和 macOS 系统。</span><span class="sxs-lookup"><span data-stu-id="6a53e-150">This is more common on Linux and macOS systems.</span></span>

<span data-ttu-id="6a53e-151">确保将 npm 全局缓存添加到 PATH。</span><span class="sxs-lookup"><span data-stu-id="6a53e-151">Ensure you add the npm global cache to your PATH.</span></span> <span data-ttu-id="6a53e-152">这通常是作为安装程序的一Node.js一部分。</span><span class="sxs-lookup"><span data-stu-id="6a53e-152">This is normally done as part of the Node.js installer.</span></span>  

<span data-ttu-id="6a53e-153">可以将 CLI 与 命令 `teamsfx` 一同使用。</span><span class="sxs-lookup"><span data-stu-id="6a53e-153">You can use the CLI with the `teamsfx` command.</span></span> <span data-ttu-id="6a53e-154">通过运行 验证命令是否正常工作 `teamsfx -h` 。</span><span class="sxs-lookup"><span data-stu-id="6a53e-154">Verify that the command is working by running `teamsfx -h`.</span></span>

> [!CAUTION]
> <span data-ttu-id="6a53e-155">必须先为 PowerShell 启用"远程签名"执行策略，然后才能在 PowerShell 终端中运行 TeamsFx。</span><span class="sxs-lookup"><span data-stu-id="6a53e-155">Before you can run TeamsFx in PowerShell terminals, you must enable the "remote signed" execution policy for PowerShell.</span></span> <span data-ttu-id="6a53e-156">有关详细信息，请参阅 [PowerShell 文档](/powershell/module/microsoft.powershell.core/about/about_signing)。</span><span class="sxs-lookup"><span data-stu-id="6a53e-156">For more information, refer to the [PowerShell documentation](/powershell/module/microsoft.powershell.core/about/about_signing).</span></span>

---

## <a name="install-optional-tools"></a><span data-ttu-id="6a53e-157">安装可选工具</span><span class="sxs-lookup"><span data-stu-id="6a53e-157">Install optional tools</span></span>

<span data-ttu-id="6a53e-158">安装用于应用开发的浏览器工具。</span><span class="sxs-lookup"><span data-stu-id="6a53e-158">Install browser tools for app development.</span></span> <span data-ttu-id="6a53e-159">例如，如果你的应用是使用 React 编写的，可以使用 React 开发人员工具：</span><span class="sxs-lookup"><span data-stu-id="6a53e-159">For instance, if your app is written with React, you can use React Developer Tools:</span></span>

- [<span data-ttu-id="6a53e-160">Chrome 的 React 开发人员工具</span><span class="sxs-lookup"><span data-stu-id="6a53e-160">React Developer Tools for Chrome</span></span>](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

<span data-ttu-id="6a53e-161">如果你想要访问 Azure 中存储的数据或在 Azure 中为 Teams 应用部署基于云的后端，请安装以下工具：</span><span class="sxs-lookup"><span data-stu-id="6a53e-161">If you want to access data stored in Azure or deploy a cloud-based backend for your Teams app in Azure, install these tools:</span></span>

- [<span data-ttu-id="6a53e-162">Azure 代码Visual Studio工具</span><span class="sxs-lookup"><span data-stu-id="6a53e-162">Azure Tools for Visual Studio Code</span></span>](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [<span data-ttu-id="6a53e-163">Azure CLI</span><span class="sxs-lookup"><span data-stu-id="6a53e-163">Azure CLI</span></span>](/cli/azure/install-azure-cli)

<span data-ttu-id="6a53e-164">如果你使用 Microsoft Graph 数据，你应该了解 Microsoft Graph 资源管理器并添加书签。</span><span class="sxs-lookup"><span data-stu-id="6a53e-164">If you work with Microsoft Graph data, you should learn about and bookmark the Microsoft Graph Explorer.</span></span> <span data-ttu-id="6a53e-165">此基于浏览器的工具允许你在应用外部查询 Microsoft Graph。</span><span class="sxs-lookup"><span data-stu-id="6a53e-165">This browser-based tool allows you to query Microsoft Graph outside of an app.</span></span>

- [<span data-ttu-id="6a53e-166">Microsoft Graph 浏览器</span><span class="sxs-lookup"><span data-stu-id="6a53e-166">Microsoft Graph Explorer</span></span>](https://developer.microsoft.com/graph/graph-explorer)

<span data-ttu-id="6a53e-167">通过 Teams 开发人员门户，你可以配置、管理和分发 Teams 应用，包括你的组织或 Teams 应用商店。</span><span class="sxs-lookup"><span data-stu-id="6a53e-167">With the Developer Portal for Teams, you can configure, manage, and distribute your Teams app including to your organization or the Teams store.</span></span>

- [<span data-ttu-id="6a53e-168">Teams 开发人员门户</span><span class="sxs-lookup"><span data-stu-id="6a53e-168">Developer Portal for Teams</span></span>](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a><span data-ttu-id="6a53e-169">启用旁加载</span><span class="sxs-lookup"><span data-stu-id="6a53e-169">Enable sideloading</span></span>

<span data-ttu-id="6a53e-170">在开发期间，你必须在 Teams 中加载你的应用，而不分发它。</span><span class="sxs-lookup"><span data-stu-id="6a53e-170">During development, you must load your app within Teams without distributing it.</span></span> <span data-ttu-id="6a53e-171">这称为"旁加载"。</span><span class="sxs-lookup"><span data-stu-id="6a53e-171">This is known as "sideloading".</span></span>

1. <span data-ttu-id="6a53e-172">如果你有 Teams 帐户，请验证你能否在 Teams 中旁加载应用：</span><span class="sxs-lookup"><span data-stu-id="6a53e-172">If you have a Teams account, verify if you can sideload apps in Teams:</span></span>

    1. <span data-ttu-id="6a53e-173">在 Teams 客户端中，选择"**应用"。**</span><span class="sxs-lookup"><span data-stu-id="6a53e-173">In the Teams client, select **Apps**.</span></span>
    1. <span data-ttu-id="6a53e-174">查找"上载自定义 **应用"选项**。</span><span class="sxs-lookup"><span data-stu-id="6a53e-174">Look for an option to **Upload a custom app**.</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="显示可以在 Teams 中上传自定义应用位置的图示。":::

> [!NOTE]
> <span data-ttu-id="6a53e-176">如果仍无法旁加载应用，请与 Teams 管理员联系。</span><span class="sxs-lookup"><span data-stu-id="6a53e-176">If you still cannot sideload apps, talk to your Teams administrator.</span></span> <span data-ttu-id="6a53e-177">有关详细信息 [，请参阅](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) 启用自定义 Teams 应用并启用自定义应用上传。</span><span class="sxs-lookup"><span data-stu-id="6a53e-177">See [enable custom Teams apps and turn on custom app uploading](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading) for details.</span></span>

## <a name="get-a-free-teams-developer-tenant-optional"></a><span data-ttu-id="6a53e-178">获取免费的 Teams 开发人员租户 (可选) </span><span class="sxs-lookup"><span data-stu-id="6a53e-178">Get a free Teams developer tenant (optional)</span></span>

<span data-ttu-id="6a53e-179">如果看不到旁加载选项，或者没有 Teams 帐户，可以通过加入 M365 开发人员计划获取免费的 Teams 开发人员帐户。</span><span class="sxs-lookup"><span data-stu-id="6a53e-179">If you cannot see the sideload option, or you do not have a Teams account, you can get a free Teams developer account by joining the M365 developer program.</span></span>  <span data-ttu-id="6a53e-180">注册过程大约需要两分钟。</span><span class="sxs-lookup"><span data-stu-id="6a53e-180">The registration process takes approximately two minutes.</span></span>

1. <span data-ttu-id="6a53e-181">转到 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="6a53e-181">Go to the [Microsoft 365 developer program](https://developer.microsoft.com/microsoft-365/dev-program).</span></span>
1. <span data-ttu-id="6a53e-182">选择 **立即加入** 并按照屏幕上的说明进行操作。</span><span class="sxs-lookup"><span data-stu-id="6a53e-182">Select **Join Now** and follow the onscreen instructions.</span></span>
1. <span data-ttu-id="6a53e-183">当你进入欢迎屏幕时，选择 **"设置 E5 订阅"。**</span><span class="sxs-lookup"><span data-stu-id="6a53e-183">When you get to the welcome screen, select **Set up E5 subscription**.</span></span>
1. <span data-ttu-id="6a53e-184">设置管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="6a53e-184">Set up your administrator account.</span></span> <span data-ttu-id="6a53e-185">完成后，你应该会看到如下所示的屏幕。</span><span class="sxs-lookup"><span data-stu-id="6a53e-185">Once you finish, you should see a screen like this.</span></span>

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="注册 Microsoft 365 开发人员计划后看到的示例。":::

1. <span data-ttu-id="6a53e-187">使用刚设置的管理员帐户登录 Teams。</span><span class="sxs-lookup"><span data-stu-id="6a53e-187">Sign in to Teams using the administrator account you just set up.</span></span>
1. <span data-ttu-id="6a53e-188">验证你现在是否具有" **上载自定义应用"** 选项。</span><span class="sxs-lookup"><span data-stu-id="6a53e-188">Verify if you now have the **Upload a custom app** option.</span></span>

## <a name="get-a-free-azure-account"></a><span data-ttu-id="6a53e-189">获取免费的 Azure 帐户</span><span class="sxs-lookup"><span data-stu-id="6a53e-189">Get a free Azure account</span></span>

<span data-ttu-id="6a53e-190">如果你想要在 Azure 中托管应用或访问资源，则必须拥有 Azure 订阅。</span><span class="sxs-lookup"><span data-stu-id="6a53e-190">If you wish to host your app or access resources within Azure, you must have an Azure subscription.</span></span>  <span data-ttu-id="6a53e-191">可以在 [开始之前创建一](https://azure.microsoft.com/free/) 个免费帐户。</span><span class="sxs-lookup"><span data-stu-id="6a53e-191">You can [create a free account](https://azure.microsoft.com/free/) before you begin.</span></span>

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a><span data-ttu-id="6a53e-192">登录到 Microsoft 365 和 Azure 帐户</span><span class="sxs-lookup"><span data-stu-id="6a53e-192">Sign in to your Microsoft 365 and Azure accounts</span></span>

<span data-ttu-id="6a53e-193">您必须有权访问两个帐户：</span><span class="sxs-lookup"><span data-stu-id="6a53e-193">You must have access to two accounts:</span></span>

- <span data-ttu-id="6a53e-194">你的 Microsoft 365 帐户凭据。</span><span class="sxs-lookup"><span data-stu-id="6a53e-194">Your Microsoft 365 account credentials.</span></span> <span data-ttu-id="6a53e-195">这是用于登录 Teams 的帐户。</span><span class="sxs-lookup"><span data-stu-id="6a53e-195">This is the account that you use to sign in to Teams.</span></span> <span data-ttu-id="6a53e-196">如果你使用的是 Microsoft 365 开发人员计划租户，这是你在注册该计划时设置的管理员帐户。</span><span class="sxs-lookup"><span data-stu-id="6a53e-196">If you're using an Microsoft 365 developer program tenant, this is the admin account you set up when you registered for the program.</span></span>
- - <span data-ttu-id="6a53e-197">你的 Azure 凭据。</span><span class="sxs-lookup"><span data-stu-id="6a53e-197">Your Azure credentials.</span></span> <span data-ttu-id="6a53e-198">这是用于访问 Azure 门户和预配新的云资源以支持你的应用的帐户。</span><span class="sxs-lookup"><span data-stu-id="6a53e-198">This is the account that you use to access the Azure Portal and for provisioning new cloud resources to support your app.</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="6a53e-199">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="6a53e-199">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="6a53e-200">打开Visual Studio代码</span><span class="sxs-lookup"><span data-stu-id="6a53e-200">Open Visual Studio Code</span></span>
1. <span data-ttu-id="6a53e-201">选择Teams栏中的"设置"图标：</span><span class="sxs-lookup"><span data-stu-id="6a53e-201">Select the Teams icon in the sidebar:</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code 边栏中的 Teams 图标。":::

1. <span data-ttu-id="6a53e-203">选择 **"登录 M365"。**</span><span class="sxs-lookup"><span data-stu-id="6a53e-203">Select **Sign in to M365**.</span></span>

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="用于登录的&quot;帐户&quot;部分的位置。":::

1. <span data-ttu-id="6a53e-205">登录过程开始使用正常的 Web 浏览器。</span><span class="sxs-lookup"><span data-stu-id="6a53e-205">The sign-in process starts using your normal web browser.</span></span> <span data-ttu-id="6a53e-206">完成 M365 帐户的登录过程。</span><span class="sxs-lookup"><span data-stu-id="6a53e-206">Complete the sign-in process for your M365 account.</span></span> <span data-ttu-id="6a53e-207">当可以关闭浏览器并返回到浏览器时，系统将Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="6a53e-207">You are prompted when you can close the browser and return to Visual Studio Code.</span></span>
1. <span data-ttu-id="6a53e-208">返回到Teams Toolkit中的Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="6a53e-208">Return to the Teams Toolkit within Visual Studio Code.</span></span>
1. <span data-ttu-id="6a53e-209">选择 **"登录到 Azure"。**</span><span class="sxs-lookup"><span data-stu-id="6a53e-209">Select **Sign in to Azure**.</span></span>

    > [!TIP]
    > <span data-ttu-id="6a53e-210">如果已安装 Azure 帐户扩展并使用相同的帐户，可以跳过此步骤。</span><span class="sxs-lookup"><span data-stu-id="6a53e-210">If you have the Azure Account extension installed and are using the same account, you can skip this step.</span></span> <span data-ttu-id="6a53e-211">请使用与其他扩展中相同的帐户。</span><span class="sxs-lookup"><span data-stu-id="6a53e-211">Use the same account as you are using in other extensions.</span></span>

1. <span data-ttu-id="6a53e-212">登录过程开始使用正常的 Web 浏览器。</span><span class="sxs-lookup"><span data-stu-id="6a53e-212">The sign-in process starts using your normal web browser.</span></span>  <span data-ttu-id="6a53e-213">完成 Azure 帐户的登录过程。</span><span class="sxs-lookup"><span data-stu-id="6a53e-213">Complete the sign-in process for your Azure account.</span></span> <span data-ttu-id="6a53e-214">当可以关闭浏览器并返回到浏览器时，系统将Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="6a53e-214">You are prompted when you can close the browser and return to Visual Studio Code.</span></span>

<span data-ttu-id="6a53e-215">完成后，边栏的 **"帐户** "部分将分别显示两个帐户以及可用的 Azure 订阅数。</span><span class="sxs-lookup"><span data-stu-id="6a53e-215">When complete, the **ACCOUNTS** section of the sidebar shows the two accounts separately, together with the number of usable Azure subscriptions available to you.</span></span> <span data-ttu-id="6a53e-216">确保至少有一个可用的 Azure 订阅可用。</span><span class="sxs-lookup"><span data-stu-id="6a53e-216">Ensure you have at least one usable Azure subscription available.</span></span> <span data-ttu-id="6a53e-217">如果没有，请注销并使用其他帐户。</span><span class="sxs-lookup"><span data-stu-id="6a53e-217">If not, sign out and use a different account.</span></span>

# <a name="visual-studio-2019"></a>[<span data-ttu-id="6a53e-218">Visual Studio 2019</span><span class="sxs-lookup"><span data-stu-id="6a53e-218">Visual Studio 2019</span></span>](#tab/vs)

<span data-ttu-id="6a53e-219">Visual Studio 2019 会提示您登录每个服务（如果需要）。</span><span class="sxs-lookup"><span data-stu-id="6a53e-219">Visual Studio 2019 prompts you to log in to each service as required.</span></span> <span data-ttu-id="6a53e-220">无需提前登录 M365 和 Azure 帐户。</span><span class="sxs-lookup"><span data-stu-id="6a53e-220">You do not need to sign in to your M365 and Azure accounts in advance.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="6a53e-221">命令行</span><span class="sxs-lookup"><span data-stu-id="6a53e-221">Command line</span></span>](#tab/cli)

1. <span data-ttu-id="6a53e-222">登录以Microsoft 365 TeamsFx CLI：</span><span class="sxs-lookup"><span data-stu-id="6a53e-222">Sign in to Microsoft 365 with the TeamsFx CLI:</span></span>

    ``` bash
    teamsfx account login m365
    ```

    <span data-ttu-id="6a53e-223">登录过程开始使用正常的 Web 浏览器。</span><span class="sxs-lookup"><span data-stu-id="6a53e-223">The sign-in process starts using your normal web browser.</span></span> <span data-ttu-id="6a53e-224">完成 M365 帐户的登录过程。</span><span class="sxs-lookup"><span data-stu-id="6a53e-224">Complete the sign-in process for your M365 account.</span></span> <span data-ttu-id="6a53e-225">当可以关闭浏览器时，系统将提示你。</span><span class="sxs-lookup"><span data-stu-id="6a53e-225">You are prompted when you can close the browser.</span></span>

2. <span data-ttu-id="6a53e-226">使用 TeamsFx CLI 登录 Azure：</span><span class="sxs-lookup"><span data-stu-id="6a53e-226">Sign in to Azure with the TeamsFx CLI:</span></span>

    ``` bash
    teamsfx account login azure
    ```

    <span data-ttu-id="6a53e-227">登录过程开始使用正常的 Web 浏览器。</span><span class="sxs-lookup"><span data-stu-id="6a53e-227">The sign-in process starts using your normal web browser.</span></span> <span data-ttu-id="6a53e-228">完成 Azure 帐户的登录过程。</span><span class="sxs-lookup"><span data-stu-id="6a53e-228">Complete the sign-in process for your Azure account.</span></span> <span data-ttu-id="6a53e-229">当可以关闭浏览器时，系统将提示你。</span><span class="sxs-lookup"><span data-stu-id="6a53e-229">You are prompted when you can close the browser.</span></span>

<span data-ttu-id="6a53e-230">帐户登录名在 Visual Studio Code TeamsFx CLI 之间共享。</span><span class="sxs-lookup"><span data-stu-id="6a53e-230">The account logins are shared between Visual Studio Code and the TeamsFx CLI.</span></span>

---

<span data-ttu-id="6a53e-231">现在，你的开发环境已配置，你可以创建、生成和部署你的第一个Teams应用。</span><span class="sxs-lookup"><span data-stu-id="6a53e-231">Now that your development environment is configured, you can create, build, and deploy your first Teams app.</span></span>

## <a name="see-also"></a><span data-ttu-id="6a53e-232">另请参阅</span><span class="sxs-lookup"><span data-stu-id="6a53e-232">See also</span></span>

- [<span data-ttu-id="6a53e-233">使用 Blazor 创建Teams应用程序</span><span class="sxs-lookup"><span data-stu-id="6a53e-233">Create your first Teams app with Blazor</span></span>](first-app-blazor.md)
- [<span data-ttu-id="6a53e-234">使用 Teams 创建第一个SharePoint 框架 (SPFx) </span><span class="sxs-lookup"><span data-stu-id="6a53e-234">Create your first Teams app using SharePoint Framework (SPFx)</span></span>](first-app-spfx.md)
- [<span data-ttu-id="6a53e-235">创建对话机器人应用</span><span class="sxs-lookup"><span data-stu-id="6a53e-235">Create a conversational bot app</span></span>](first-app-bot.md)
- [<span data-ttu-id="6a53e-236">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="6a53e-236">Create a messaging extension</span></span>](first-message-extension.md)

## <a name="next-step"></a><span data-ttu-id="6a53e-237">后续步骤</span><span class="sxs-lookup"><span data-stu-id="6a53e-237">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="6a53e-238">使用 Teams 创建你的第一个React</span><span class="sxs-lookup"><span data-stu-id="6a53e-238">Create your first Teams app using React</span></span>](first-app-react.md)
