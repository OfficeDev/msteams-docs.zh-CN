---
title: 选择用于测试和调试应用的设置
description: 介绍用于测试和调试 Microsoft Teams 应用的选项
keywords: 团队运行调试应用
ms.topic: conceptual
ms.openlocfilehash: fde8a5907e0815ff798a3acc316cba8336ab8704
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634732"
---
# <a name="choose-a-setup-to-test-and-debug-your-microsoft-teams-app"></a><span data-ttu-id="36d40-104">选择用于测试和调试 Microsoft Teams 应用的设置</span><span class="sxs-lookup"><span data-stu-id="36d40-104">Choose a setup to test and debug your Microsoft Teams app</span></span>

<span data-ttu-id="36d40-105">Microsoft Teams 应用包含一个或多个功能，并且运行甚至托管这些功能的方式有所不同。</span><span class="sxs-lookup"><span data-stu-id="36d40-105">Microsoft Teams apps contain one or more capabilities and the ways to run or even host them are different.</span></span> <span data-ttu-id="36d40-106">对于调试，请使用以下方法之一：</span><span class="sxs-lookup"><span data-stu-id="36d40-106">For debugging, use one of the following ways:</span></span>

* <span data-ttu-id="36d40-107">**纯本地**：对于机器人，可以在 Bot 模拟器中测试你的体验。</span><span class="sxs-lookup"><span data-stu-id="36d40-107">**Purely local**: For bots, you can test your experience in the Bot Emulator.</span></span> <span data-ttu-id="36d40-108">对于其他内容，可以在浏览器中本地运行，并通过 地址内容 `http://localhost` 。</span><span class="sxs-lookup"><span data-stu-id="36d40-108">For other content, you can run locally in your browser and address content through `http://localhost`.</span></span>
* <span data-ttu-id="36d40-109">**本地托管在 Teams** 中：这涉及在隧道软件中本地运行应用，并 [](~/concepts/build-and-test/apps-package.md)创建要 [上传到](~/concepts/deploy-and-publish/apps-upload.md)Teams 的程序包。</span><span class="sxs-lookup"><span data-stu-id="36d40-109">**Locally hosted in Teams**: This involves running the app locally in tunneling software and [creating a package](~/concepts/build-and-test/apps-package.md) to [upload](~/concepts/deploy-and-publish/apps-upload.md) into Teams.</span></span> <span data-ttu-id="36d40-110">这样，你可以轻松地在 Teams 客户端中运行和调试应用。</span><span class="sxs-lookup"><span data-stu-id="36d40-110">This permits you to easily run and debug your app within the Teams client.</span></span>
* <span data-ttu-id="36d40-111">**Teams 中托管的云**：这真正模拟了 Teams 应用的生产级别支持。</span><span class="sxs-lookup"><span data-stu-id="36d40-111">**Cloud-hosted in Teams**: This truly simulates the production level support for a Teams app.</span></span> <span data-ttu-id="36d40-112">它涉及将解决方案上载到可从外部访问的服务器或选择的云提供商，以及创建要上传到[](~/concepts/build-and-test/apps-package.md)Teams[的程序包](~/concepts/deploy-and-publish/apps-upload.md)。</span><span class="sxs-lookup"><span data-stu-id="36d40-112">It involves uploading your solution to your externally accessible server or cloud provider of choice and [creating a package](~/concepts/build-and-test/apps-package.md) to [upload](~/concepts/deploy-and-publish/apps-upload.md) into Teams.</span></span>

<span data-ttu-id="36d40-113">从你自己的计算机运行体验，进行纯本地或本地 Teams 测试。</span><span class="sxs-lookup"><span data-stu-id="36d40-113">Run the experience from your own computer for purely local or local Teams testing.</span></span> <span data-ttu-id="36d40-114">通过执行此操作，可以在集成开发环境中编译和运行，并充分利用技术（如断点和步骤调试）。</span><span class="sxs-lookup"><span data-stu-id="36d40-114">By doing this, you can compile and run within your integrated development environment and take full advantage of techniques, such as breakpoints and step debugging.</span></span> 

> [!NOTE]
> <span data-ttu-id="36d40-115">对于生产规模调试和测试，我们建议您遵循自己的公司准则，以确保能够通过自己的流程支持测试、暂存和部署。</span><span class="sxs-lookup"><span data-stu-id="36d40-115">For production-scale debugging and testing, we recommend that you follow your own company guidelines to ensure you are able to support testing, staging, and deployment through your own processes.</span></span>

<span data-ttu-id="36d40-116">使用多个清单和程序包保持生产和开发服务之间的分隔。</span><span class="sxs-lookup"><span data-stu-id="36d40-116">Use multiple manifests and packages to maintain separation between production and development services.</span></span> <span data-ttu-id="36d40-117">例如，你可以选择注册单独的开发和生产机器人，并创建相应的程序包以在测试环境中上载它们。</span><span class="sxs-lookup"><span data-stu-id="36d40-117">For example, you might choose to register separate development and production bots and create appropriate packages to upload them in your testing environment.</span></span> <span data-ttu-id="36d40-118">我们还建议你在提交应用以在我们的应用商店中发布或分发给客户之前上载和测试你的生产包。</span><span class="sxs-lookup"><span data-stu-id="36d40-118">We also recommend, you upload and test your production package before submitting your app for publishing in our app store or distributing to customers.</span></span>

## <a name="purely-local"></a><span data-ttu-id="36d40-119">纯本地</span><span class="sxs-lookup"><span data-stu-id="36d40-119">Purely local</span></span>

> [!NOTE]
> <span data-ttu-id="36d40-120">在本地运行自动程序并不能让你访问 Teams 应用功能或特定于 Teams 的自动程序功能，如名单呼叫和其他特定于频道的功能。</span><span class="sxs-lookup"><span data-stu-id="36d40-120">Running the bot locally does not give you access to Teams app functionality or Teams-specific bot functions like roster calls and other channel-specific functionality.</span></span> <span data-ttu-id="36d40-121">此外，自动程序仿真器中的自动程序框架允许某些功能在 Microsoft Teams 中运行时可能无法运行。</span><span class="sxs-lookup"><span data-stu-id="36d40-121">In addition, some capabilities are permitted by the Bot Framework in the Bot Emulator that might not function when running in Microsoft Teams.</span></span>

<span data-ttu-id="36d40-122">机器人可以在自动程序仿真器中运行。</span><span class="sxs-lookup"><span data-stu-id="36d40-122">Your bot can run within the Bot Emulator.</span></span> <span data-ttu-id="36d40-123">这使你能够测试机器人的一些核心逻辑、查看消息的粗略布局和执行简单测试。</span><span class="sxs-lookup"><span data-stu-id="36d40-123">This enables you to test some of the core logic of the bot, see a rough layout of messages, and perform simple tests.</span></span> <span data-ttu-id="36d40-124">步骤如下：</span><span class="sxs-lookup"><span data-stu-id="36d40-124">Following are the steps:</span></span>

1. <span data-ttu-id="36d40-125">在本地运行代码。</span><span class="sxs-lookup"><span data-stu-id="36d40-125">Run the code locally.</span></span>
2. <span data-ttu-id="36d40-126">启动自动程序仿真器并设置 URL：</span><span class="sxs-lookup"><span data-stu-id="36d40-126">Launch the Bot Emulator and set the URL:</span></span>
   * <span data-ttu-id="36d40-127">Node.js： `http://localhost:3978/api/messages`</span><span class="sxs-lookup"><span data-stu-id="36d40-127">Node.js: `http://localhost:3978/api/messages`</span></span>
   * <span data-ttu-id="36d40-128">.NET/C#： `http://localhost:3979/api/messages`</span><span class="sxs-lookup"><span data-stu-id="36d40-128">.NET/C#: `http://localhost:3979/api/messages`</span></span>
3. <span data-ttu-id="36d40-129">将 Microsoft 应用 ID 和 Microsoft 应用密码留空，以匹配默认环境变量。</span><span class="sxs-lookup"><span data-stu-id="36d40-129">Leave the Microsoft app ID and Microsoft app password blank, to match the default environment variables.</span></span>

## <a name="locally-hosted"></a><span data-ttu-id="36d40-130">本地托管</span><span class="sxs-lookup"><span data-stu-id="36d40-130">Locally hosted</span></span>

<span data-ttu-id="36d40-131">Microsoft Teams 是完全基于云的产品，它要求它访问的所有服务都使用 HTTPS 终结点公开提供。</span><span class="sxs-lookup"><span data-stu-id="36d40-131">Microsoft Teams is an entirely cloud-based product, it requires all services it accesses to be available publicly using HTTPS endpoints.</span></span> <span data-ttu-id="36d40-132">因此，若要使你的应用在 Teams 中运行，你需要将代码发布到你选择的云，或使本地运行的实例可从外部访问。</span><span class="sxs-lookup"><span data-stu-id="36d40-132">Therefore, to enable your app to work within Teams, you need to either publish the code to the cloud of your choice or make our local running instance externally accessible.</span></span> <span data-ttu-id="36d40-133">我们可以使用隧道软件执行后者。</span><span class="sxs-lookup"><span data-stu-id="36d40-133">We can do the latter with tunneling software.</span></span>

<span data-ttu-id="36d40-134">尽管可以使用你选择的任何工具，但我们使用并推荐 [ngrok](https://ngrok.com/download)，这将为计算机上本地打开的端口创建一个外部可地址 URL。</span><span class="sxs-lookup"><span data-stu-id="36d40-134">Although you can use any tool of your choice, we use and recommend [ngrok](https://ngrok.com/download), which creates an externally addressable URL for a port you open locally on your machine.</span></span> 

<span data-ttu-id="36d40-135">**设置 ngrok 以准备在本地运行 Microsoft Teams 应用**</span><span class="sxs-lookup"><span data-stu-id="36d40-135">**To set up ngrok in preparation for running your Microsoft Teams app locally**</span></span>

1. <span data-ttu-id="36d40-136">转到在终端应用程序中安装ngrok.exe的目录。</span><span class="sxs-lookup"><span data-stu-id="36d40-136">Go to the directory where you have ngrok.exe installed in a terminal application.</span></span> <span data-ttu-id="36d40-137">您可能需要将其添加为路径变量以避免此步骤。</span><span class="sxs-lookup"><span data-stu-id="36d40-137">You may want to add it as a path variable to avoid this step.</span></span>
2. <span data-ttu-id="36d40-138">运行 ，例如 `ngrok http 3978 --host-header=localhost:3978` ， 或根据需要替换端口号。</span><span class="sxs-lookup"><span data-stu-id="36d40-138">Run, for example, `ngrok http 3978 --host-header=localhost:3978`, or replace the port number as needed.</span></span>
   <span data-ttu-id="36d40-139">这会启动 ngrok 以在指定的端口上列出。</span><span class="sxs-lookup"><span data-stu-id="36d40-139">This launches ngrok to list on the port you specify.</span></span> <span data-ttu-id="36d40-140">作为返回，它为你提供一个外部可地址 URL，只要 ngrok 正在运行，该 URL 就有效。</span><span class="sxs-lookup"><span data-stu-id="36d40-140">In return, it gives you an externally addressable URL valid for as long as ngrok is running.</span></span>

> [!NOTE]
> <span data-ttu-id="36d40-141">如果停止并重新启动 ngrok，URL 将发生更改。</span><span class="sxs-lookup"><span data-stu-id="36d40-141">If you stop and restart ngrok, the URL changes.</span></span>

<span data-ttu-id="36d40-142">若要根据你使用的功能在项目中使用 ngrok，必须替换代码、配置和文件上的所有 URL manifest.js以使用此 URL 终结点。</span><span class="sxs-lookup"><span data-stu-id="36d40-142">To use ngrok in your project based on the capabilities you are using, you must replace all URL references in your code, configuration, and manifest.json file to use this URL endpoint.</span></span>

<span data-ttu-id="36d40-143">对于在 Microsoft Bot Framework 中注册的机器人，更新机器人的消息终结点以使用此新的 ngrok 终结点。</span><span class="sxs-lookup"><span data-stu-id="36d40-143">For bots registered in the Microsoft Bot Framework, update the bot's messaging endpoint to use this new ngrok endpoint.</span></span> <span data-ttu-id="36d40-144">例如，`https://2d1224fb.ngrok.io/api/messages`。</span><span class="sxs-lookup"><span data-stu-id="36d40-144">For example, `https://2d1224fb.ngrok.io/api/messages`.</span></span> <span data-ttu-id="36d40-145">可以通过在 Bot Framework 门户的"测试"聊天窗口中测试自动程序响应来验证 ngrok 是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="36d40-145">You can validate that ngrok is working by testing the bot response in the Bot Framework portal's Test chat window.</span></span> <span data-ttu-id="36d40-146">同样，与仿真器一样，此测试不允许你访问特定于 Teams 的功能。</span><span class="sxs-lookup"><span data-stu-id="36d40-146">Again, like the emulator, this test does not permit you to access Teams-specific functionality.</span></span>

> [!NOTE]
> <span data-ttu-id="36d40-147">若要更新机器人的消息终结点，必须使用 Bot 框架。</span><span class="sxs-lookup"><span data-stu-id="36d40-147">To update the messaging endpoint for a bot, you must use the Bot Framework.</span></span> <span data-ttu-id="36d40-148">在 Bot [Framework 中的自动程序列表中选择自动程序](https://dev.botframework.com/bots)。</span><span class="sxs-lookup"><span data-stu-id="36d40-148">Select your bot in [your list of bots in Bot Framework](https://dev.botframework.com/bots).</span></span> <span data-ttu-id="36d40-149">无需将机器人迁移到 Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="36d40-149">You do not need to migrate your bot to Microsoft Azure.</span></span> <span data-ttu-id="36d40-150">您还可以通过 App Studio 更新消息 [终结点](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="36d40-150">You can also update your messaging endpoint through [App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="cloud-hosted"></a><span data-ttu-id="36d40-151">云托管</span><span class="sxs-lookup"><span data-stu-id="36d40-151">Cloud-hosted</span></span>

<span data-ttu-id="36d40-152">可以使用任何外部可地址服务来托管开发和生产代码及其 HTTPS 终结点。</span><span class="sxs-lookup"><span data-stu-id="36d40-152">You can use any externally addressable service to host your development and production code and their HTTPS endpoints.</span></span> <span data-ttu-id="36d40-153">无法预期你的功能驻留在同一个服务上。</span><span class="sxs-lookup"><span data-stu-id="36d40-153">There is no expectation that your capabilities reside on the same service.</span></span> <span data-ttu-id="36d40-154">我们要求从文件对象中列出的 Microsoft Teams 应用访问 [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) 所有 `manifest.json` 域。</span><span class="sxs-lookup"><span data-stu-id="36d40-154">We require all domains to be accessed from your Microsoft Teams apps listed in the [`validDomains`](~/resources/schema/manifest-schema.md#validdomains) object in the `manifest.json` file.</span></span>

> [!NOTE]
> <span data-ttu-id="36d40-155">若要确保安全环境，请明确引用的确切域和子域，这些域必须在你的控制中。</span><span class="sxs-lookup"><span data-stu-id="36d40-155">To ensure a secure environment, be explicit about the exact domain and subdomains you reference and those domains must be in your control.</span></span> <span data-ttu-id="36d40-156">例如， `*.azurewebsites.net` 不建议使用 ，但 `contoso.azurewebsites.net` 建议这样做。</span><span class="sxs-lookup"><span data-stu-id="36d40-156">For example, `*.azurewebsites.net` is not recommended, however `contoso.azurewebsites.net` is recommended.</span></span>

## <a name="load-and-run-your-experience"></a><span data-ttu-id="36d40-157">加载并运行体验</span><span class="sxs-lookup"><span data-stu-id="36d40-157">Load and run your experience</span></span>

<span data-ttu-id="36d40-158">若要在 Microsoft Teams 中加载并运行你的体验，你需要创建一个程序包并将其上传到 Teams。</span><span class="sxs-lookup"><span data-stu-id="36d40-158">To load and run your experience within Microsoft Teams, you need to create a package and upload it into Teams.</span></span> <span data-ttu-id="36d40-159">有关详细信息，请参阅：</span><span class="sxs-lookup"><span data-stu-id="36d40-159">For more information, see:</span></span>

* [<span data-ttu-id="36d40-160">为 Microsoft Teams 应用创建程序包</span><span class="sxs-lookup"><span data-stu-id="36d40-160">Create the package for your Microsoft Teams app</span></span>](~/concepts/build-and-test/apps-package.md)
* [<span data-ttu-id="36d40-161">在 Microsoft Teams 中上传应用</span><span class="sxs-lookup"><span data-stu-id="36d40-161">Upload your app in Microsoft Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)

## <a name="next-step"></a><span data-ttu-id="36d40-162">后续步骤</span><span class="sxs-lookup"><span data-stu-id="36d40-162">Next step</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="36d40-163">向环境中添加测试数据</span><span class="sxs-lookup"><span data-stu-id="36d40-163">Add test data to your environment</span></span>](~/concepts/build-and-test/test-data.md)

