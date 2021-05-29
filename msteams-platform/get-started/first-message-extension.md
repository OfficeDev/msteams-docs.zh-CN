---
title: 开始 - 构建第一个邮件扩展
author: adrianhall
description: 使用 Teams 工具包为 Microsoft Teams 创建邮件扩展。
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: ad341c386cc9e1bf03cf6e25c0d8be8add0880c6
ms.sourcegitcommit: 2c8b35899dd845acd66f1f927e40d99523c29a91
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2021
ms.locfileid: "52698104"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="d201f-103">构建并运行 Microsoft Teams 的第一个消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="d201f-103">Build and run your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="d201f-104">有两种类型的 Teams **消息扩展**：</span><span class="sxs-lookup"><span data-stu-id="d201f-104">There are two types of Teams **messaging extensions**:</span></span>

- <span data-ttu-id="d201f-105">[搜索命令](../messaging-extensions/how-to/search-commands/define-search-command.md)允许您搜索外部系统并将搜索结果以卡片的形式插入到消息中。</span><span class="sxs-lookup"><span data-stu-id="d201f-105">[Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) allow you to search external systems and insert the results of that search into a message in the form of a card.</span></span>
- <span data-ttu-id="d201f-106">[动作命令](../messaging-extensions/how-to/action-commands/define-action-command.md)允许为用户提供一个模式弹出式窗口来收集或显示信息，然后处理他们的互动并将信息发送回 Teams。</span><span class="sxs-lookup"><span data-stu-id="d201f-106">[Action commands](../messaging-extensions/how-to/action-commands/define-action-command.md) allow you present your users with a modal popup to collect or display information, then process their interaction and send information back to Teams.</span></span>

<span data-ttu-id="d201f-107">在本教程中，您将创建一 *搜索命令* 搜索外部数据并将结果插入邮件。</span><span class="sxs-lookup"><span data-stu-id="d201f-107">In this tutorial, you will create a *search command* to search for external data and insert the results into a message.</span></span>  

## <a name="before-you-begin"></a><span data-ttu-id="d201f-108">准备工作</span><span class="sxs-lookup"><span data-stu-id="d201f-108">Before you begin</span></span>

<span data-ttu-id="d201f-109">通过安装[先决条件](prerequisites.md)确保您的开发环境已设置</span><span class="sxs-lookup"><span data-stu-id="d201f-109">Make sure your development environment is set up by installing the [Prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d201f-110">安装先决条件</span><span class="sxs-lookup"><span data-stu-id="d201f-110">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="d201f-111">创建项目</span><span class="sxs-lookup"><span data-stu-id="d201f-111">Create your project</span></span>

<span data-ttu-id="d201f-112">使用 Teams 工具包创建你的第一个项目：</span><span class="sxs-lookup"><span data-stu-id="d201f-112">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="d201f-113">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="d201f-113">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="d201f-114">打开 Visual Studio 代码。</span><span class="sxs-lookup"><span data-stu-id="d201f-114">Open Visual Studio Code.</span></span>
1. <span data-ttu-id="d201f-115">选择边栏中的"团队"图标打开 Teams 工具包：</span><span class="sxs-lookup"><span data-stu-id="d201f-115">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio 代码边栏中的&quot;团队&quot;图标。":::

1. <span data-ttu-id="d201f-117">选择 **"创建新的项目**。</span><span class="sxs-lookup"><span data-stu-id="d201f-117">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. <span data-ttu-id="d201f-119">选择 **"创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="d201f-119">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="&quot;创建新项目&quot;的向导启动":::

1. <span data-ttu-id="d201f-121">在" **选择功能"** 步骤 ， 选择 **邮件扩展** ，然后取消选择 **选项卡**。 按 **确定**。</span><span class="sxs-lookup"><span data-stu-id="d201f-121">On the **Select capabilities** step, select **Message Extension** and deselect **Tab**.  Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="显示如何向新应用添加功能的屏幕截图。":::

1. <span data-ttu-id="d201f-123">在" **自动注册** 步骤中， **创建新的自动注册**。</span><span class="sxs-lookup"><span data-stu-id="d201f-123">On the **Bot registration** step, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="选择创建新的自动注册":::

   > [!NOTE]
   > <span data-ttu-id="d201f-125">消息扩展依赖于自动程序，在用户和你的代码之间提供对话框。</span><span class="sxs-lookup"><span data-stu-id="d201f-125">Messaging extensions rely on bots to provide a dialog between the user and your code.</span></span>

1. <span data-ttu-id="d201f-126">在" **编程语言** 步骤中， 选择 **JavaScript**。</span><span class="sxs-lookup"><span data-stu-id="d201f-126">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="显示如何选择编程语言的屏幕截图。":::

1. <span data-ttu-id="d201f-128">选择工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="d201f-128">Select a workspace folder.</span></span>  <span data-ttu-id="d201f-129">将在工作区文件夹中为正在创建的项目创建一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="d201f-129">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="d201f-130">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="d201f-130">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="d201f-131">应用的名称只必须包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="d201f-131">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="d201f-132">按 **Enter** 以继续。</span><span class="sxs-lookup"><span data-stu-id="d201f-132">Press **Enter** to continue.</span></span>

<span data-ttu-id="d201f-133">将在数秒钟内创建你的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="d201f-133">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="d201f-134">命令行</span><span class="sxs-lookup"><span data-stu-id="d201f-134">Command line</span></span>](#tab/cli)

<span data-ttu-id="d201f-135">使用 `teamsfx` CLI 创建您的第一个项目。</span><span class="sxs-lookup"><span data-stu-id="d201f-135">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="d201f-136">从要创建项目文件夹的文件夹开始。</span><span class="sxs-lookup"><span data-stu-id="d201f-136">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="d201f-137">省/市/区会引导他们提出一些问题来创建项目。</span><span class="sxs-lookup"><span data-stu-id="d201f-137">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="d201f-138">每个问题将告诉你如何回答（例如，使用箭头键选择一个选项）。</span><span class="sxs-lookup"><span data-stu-id="d201f-138">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="d201f-139">如果已回答问题，请通过按 Enter 键 **确认**。</span><span class="sxs-lookup"><span data-stu-id="d201f-139">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="d201f-140">选择 **"创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="d201f-140">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="d201f-141">选择 **邮件扩展** 功能，然后取消选择" **选项卡** 功能。</span><span class="sxs-lookup"><span data-stu-id="d201f-141">Select the **Message Extension** capability and deselect the **Tab** capability.</span></span>
1. <span data-ttu-id="d201f-142">选择 **创建新的自动注册**。</span><span class="sxs-lookup"><span data-stu-id="d201f-142">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="d201f-143">选择 **JavaScript** 作为编程语言。</span><span class="sxs-lookup"><span data-stu-id="d201f-143">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="d201f-144">按 **Enter** 选择默认工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="d201f-144">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="d201f-145">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="d201f-145">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="d201f-146">应用的名称只必须包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="d201f-146">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="d201f-147">解答所有问题后，将创建项目。</span><span class="sxs-lookup"><span data-stu-id="d201f-147">Once all the questions have been answered, your project will be created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="d201f-148">浏览源代码</span><span class="sxs-lookup"><span data-stu-id="d201f-148">Take a tour of the source code</span></span>

<span data-ttu-id="d201f-149">若要暂时跳过此部分， 你可以[运行本地应用](#run-your-app-locally)。</span><span class="sxs-lookup"><span data-stu-id="d201f-149">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="d201f-150">消息扩展使用 [Bot Framework](https://docs.botframework.com) 允许用户通过对话与您的服务交互。</span><span class="sxs-lookup"><span data-stu-id="d201f-150">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="d201f-151">设置标点文件夹后，你的项目将如下所示：</span><span class="sxs-lookup"><span data-stu-id="d201f-151">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-file-layout.png" alt-text="自动项目的文件布局。":::

<span data-ttu-id="d201f-153">自动程序代码存储在 `bot` 中。</span><span class="sxs-lookup"><span data-stu-id="d201f-153">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="d201f-154">`bots/messageExtensionBot.js` 是邮件扩展的主入口点。</span><span class="sxs-lookup"><span data-stu-id="d201f-154">The `bots/messageExtensionBot.js` is the main entry point for the messaging extension.</span></span>

> [!Tip]
> <span data-ttu-id="d201f-155">在将第一个机器人集成到 Teams 中之前，请熟悉 Teams 以外的机器人。</span><span class="sxs-lookup"><span data-stu-id="d201f-155">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="d201f-156">可以通过查看 [Azure 机器人服务](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)教程找到有关机器人的更多信息。</span><span class="sxs-lookup"><span data-stu-id="d201f-156">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="d201f-157">在本地运行应用</span><span class="sxs-lookup"><span data-stu-id="d201f-157">Run your app locally</span></span>

<span data-ttu-id="d201f-158">Teams 工具包允许你在本地托管应用。</span><span class="sxs-lookup"><span data-stu-id="d201f-158">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="d201f-159">为此，请执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="d201f-159">To do this:</span></span>

- <span data-ttu-id="d201f-160">Azure Active Directory 应用程序是在 M365 租户中注册的。</span><span class="sxs-lookup"><span data-stu-id="d201f-160">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="d201f-161">向 Teams 开发人员门户提交应用清单。</span><span class="sxs-lookup"><span data-stu-id="d201f-161">An app manifest is submitted to the Developer Portal for Teams.</span></span>
- <span data-ttu-id="d201f-162">在本地使用 Azure 函数核心工具运行 API，以支持你的应用。</span><span class="sxs-lookup"><span data-stu-id="d201f-162">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="d201f-163">[ngrok](https://ngrok.io) 安装并用于在 Teams 和消息扩展之间提供一个隧道。</span><span class="sxs-lookup"><span data-stu-id="d201f-163">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your messaging extension.</span></span>

<span data-ttu-id="d201f-164">若要在本地构建和运行应用，请执行：</span><span class="sxs-lookup"><span data-stu-id="d201f-164">To build and run your app locally:</span></span>

1. <span data-ttu-id="d201f-165">从 Visual Studio Code 中， **F5** 调试模式下运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="d201f-165">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="d201f-166">首次运行该应用时，将下载所有依赖项并构建该应用。</span><span class="sxs-lookup"><span data-stu-id="d201f-166">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="d201f-167">版本完成后，将自动打开浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="d201f-167">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="d201f-168">这可能需要 3-5 分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="d201f-168">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="d201f-169">将在 Web 浏览器中加载 Teams，并提示进行登录。</span><span class="sxs-lookup"><span data-stu-id="d201f-169">Teams will be loaded in a web browser, and you will be prompted to sign in.</span></span> <span data-ttu-id="d201f-170">如果系统提示打开 Microsoft Teams，请选择"取消"以保留在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="d201f-170">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="d201f-171">使用 M365 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="d201f-171">Sign in with your M365 account.</span></span>

1. <span data-ttu-id="d201f-172">按 **添加** 将应用添加到你的帐户。</span><span class="sxs-lookup"><span data-stu-id="d201f-172">Press **Add** to add the app to your account.</span></span>

<span data-ttu-id="d201f-173">加载应用后，你将直接进入搜索对话框：</span><span class="sxs-lookup"><span data-stu-id="d201f-173">Once the app is loaded, you will be taken directly to a search dialog:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-completed-app.png" alt-text="操作中基于搜索的邮件扩展":::

<span data-ttu-id="d201f-175">在搜索框中键入文本，然后选择其中一个选项。</span><span class="sxs-lookup"><span data-stu-id="d201f-175">Type some text in the search box, then select one of the options.</span></span>  <span data-ttu-id="d201f-176">自适应卡片将添加到输入框中。</span><span class="sxs-lookup"><span data-stu-id="d201f-176">An adaptive card will be added to your input box.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="d201f-177">在调试器中本地运行应用时，会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="d201f-177">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="d201f-178">按 F5 时，Teams 工具包：</span><span class="sxs-lookup"><span data-stu-id="d201f-178">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="d201f-179">使用 Azure Active Directory 注册应用程序。</span><span class="sxs-lookup"><span data-stu-id="d201f-179">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="d201f-180">在 Microsoft Teams 中注册"边加载"应用程序。</span><span class="sxs-lookup"><span data-stu-id="d201f-180">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="d201f-181">使用 [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start) 启动在本地运行的应用程序后端。</span><span class="sxs-lookup"><span data-stu-id="d201f-181">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="d201f-182">启动 ngrok 隧道，以便团队可以与你的应用通信。</span><span class="sxs-lookup"><span data-stu-id="d201f-182">Started an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="d201f-183">启动 Microsoft Teams 时，具有指示 Teams 下载该应用程序的命令。</span><span class="sxs-lookup"><span data-stu-id="d201f-183">Started Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="d201f-184">了解如何在本地运行应用时解决常见问题。</span><span class="sxs-lookup"><span data-stu-id="d201f-184">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="d201f-185">若要在 Teams 中成功运行应用，必须具有允许应用程序旁加载的 Microsoft 365 开发帐户。</span><span class="sxs-lookup"><span data-stu-id="d201f-185">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="d201f-186">有关打开帐户详细信息，请参阅 [先决条件](prerequisites.md#enable-sideloading)。</span><span class="sxs-lookup"><span data-stu-id="d201f-186">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="d201f-187">在并行加载应用之前，使用 [应用验证工具](https://dev.teams.microsoft.com/appvalidation.html)中的问题。</span><span class="sxs-lookup"><span data-stu-id="d201f-187">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="d201f-188">修复错误以成功并行加载应用。</span><span class="sxs-lookup"><span data-stu-id="d201f-188">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="d201f-189">了解将应用部署到 Azure 时会发生的情况</span><span class="sxs-lookup"><span data-stu-id="d201f-189">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="d201f-190">部署之前，应用程序已在本地运行：</span><span class="sxs-lookup"><span data-stu-id="d201f-190">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="d201f-191">后端使用 _Azure 函数核心工具_。</span><span class="sxs-lookup"><span data-stu-id="d201f-191">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="d201f-192">应用程序 HTTP 终结点（这是 Microsoft Teams 其中加载应用程序）在本地运行。</span><span class="sxs-lookup"><span data-stu-id="d201f-192">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="d201f-193">部署涉及预配活动 Azure 订阅上的资源，以及将应用程序后端和前端代码部署（上传）到 Azure。</span><span class="sxs-lookup"><span data-stu-id="d201f-193">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="d201f-194">后端使用多种 Azure 服务，包括 Azure 应用服务和 Azure Bot 服务。</span><span class="sxs-lookup"><span data-stu-id="d201f-194">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="next-steps"></a><span data-ttu-id="d201f-195">后续步骤</span><span class="sxs-lookup"><span data-stu-id="d201f-195">Next steps</span></span>

<span data-ttu-id="d201f-196">了解创建 Teams 应用的其他方法：</span><span class="sxs-lookup"><span data-stu-id="d201f-196">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="d201f-197">使用 React 创建 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="d201f-197">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="d201f-198">使用 Blazor 创建 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="d201f-198">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="d201f-199">[创建 Teams 应用作为 SharePoint Web 部件](first-app-spfx.md) （不需要 Azure）</span><span class="sxs-lookup"><span data-stu-id="d201f-199">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="d201f-200">创建对话机器人</span><span class="sxs-lookup"><span data-stu-id="d201f-200">Create a conversation bot</span></span>](first-app-bot.md)
