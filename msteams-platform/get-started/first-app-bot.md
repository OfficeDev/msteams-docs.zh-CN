---
title: 入门 - 构建你的第一个对话机器人
author: adrianhall
description: 使用 Teams 工具包为 Microsoft Teams 创建对话机器人。
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: 3084020000cf53fbb33ffc25d141b41ffff83160
ms.sourcegitcommit: 2c8b35899dd845acd66f1f927e40d99523c29a91
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/28/2021
ms.locfileid: "52697949"
---
# <a name="build-your-first-conversational-bot-for-microsoft-teams"></a><span data-ttu-id="32505-103">构建你的第一个 Microsoft Teams 对话机器人</span><span class="sxs-lookup"><span data-stu-id="32505-103">Build your first conversational bot for Microsoft Teams</span></span>

<span data-ttu-id="32505-104">机器人是 Teams 用户和 Web 服务之间的中介。</span><span class="sxs-lookup"><span data-stu-id="32505-104">A bot acts as an intermediary between a Teams user and a web service.</span></span>  <span data-ttu-id="32505-105">用户可以与机器人聊天，以快速获取信息、启动工作流或启动 Web 服务能够执行的任何操作。</span><span class="sxs-lookup"><span data-stu-id="32505-105">Users can chat with a bot to quickly get information, initiate workflows, or anything else your web service can do.</span></span>  <span data-ttu-id="32505-106">在本教程中，你将了解如何构建、运行和部署 Teams 机器人应用。</span><span class="sxs-lookup"><span data-stu-id="32505-106">In this tutorial, you will learn how to build, run, and deploy a Teams bot app.</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="32505-107">准备工作</span><span class="sxs-lookup"><span data-stu-id="32505-107">Before you begin</span></span>

<span data-ttu-id="32505-108">通过安装[先决条件](prerequisites.md)确保你的开发环境已设置</span><span class="sxs-lookup"><span data-stu-id="32505-108">Make sure your development environment is set up by installing the [Prerequisites](prerequisites.md)</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="32505-109">安装先决条件</span><span class="sxs-lookup"><span data-stu-id="32505-109">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="32505-110">创建项目</span><span class="sxs-lookup"><span data-stu-id="32505-110">Create your project</span></span>

<span data-ttu-id="32505-111">使用 Teams 工具包创建你的第一个项目:</span><span class="sxs-lookup"><span data-stu-id="32505-111">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="32505-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="32505-112">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="32505-113">打开 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="32505-113">Open Visual Studio code.</span></span>
1. <span data-ttu-id="32505-114">通过选择边栏中的 Teams 图标，打开 Teams 工具包:</span><span class="sxs-lookup"><span data-stu-id="32505-114">Open the Teams Toolkit by selecting the Teams icon in the sidebar:</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code 边栏中的 Teams 图标。":::

1. <span data-ttu-id="32505-116">选择 **创建新项目**。</span><span class="sxs-lookup"><span data-stu-id="32505-116">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. <span data-ttu-id="32505-118">选择 **创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="32505-118">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="&quot;创建新项目&quot;的向导启动":::

1. <span data-ttu-id="32505-120">在 **选择功能** 步骤，选择 **机器人**，然后取消选择 **选项卡**。按 **确定**。</span><span class="sxs-lookup"><span data-stu-id="32505-120">On the **Select capabilities** step, select **Bot** and deselect **Tab**.  Press **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities-bot.png" alt-text="显示如何向新应用添加功能的屏幕截图。":::

1. <span data-ttu-id="32505-122">在 **机器人注册** 步骤中，选择 **创建新的机器人注册**。</span><span class="sxs-lookup"><span data-stu-id="32505-122">On the **Bot registration** step, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="选择创建新的机器人注册":::

1. <span data-ttu-id="32505-124">在 **编程语言** 步骤中，选择 **JavaScript**。</span><span class="sxs-lookup"><span data-stu-id="32505-124">On the **Programming Language** step, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="显示如何选择编程语言的屏幕截图。":::

1. <span data-ttu-id="32505-126">选择工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="32505-126">Select a workspace folder.</span></span>  <span data-ttu-id="32505-127">将在工作区文件夹中为正在创建的项目创建一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="32505-127">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="32505-128">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="32505-128">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="32505-129">应用的名称只能包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="32505-129">The name of the app must consist only of alphanumeric characters.</span></span>  <span data-ttu-id="32505-130">按 **Enter** 以继续。</span><span class="sxs-lookup"><span data-stu-id="32505-130">Press **Enter** to continue.</span></span>

<span data-ttu-id="32505-131">将在数秒钟内创建你的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="32505-131">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="32505-132">命令行</span><span class="sxs-lookup"><span data-stu-id="32505-132">Command line</span></span>](#tab/cli)

<span data-ttu-id="32505-133">使用 `teamsfx` CLI 创建你的第一个项目。</span><span class="sxs-lookup"><span data-stu-id="32505-133">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="32505-134">从要创建项目文件夹的文件夹开始。</span><span class="sxs-lookup"><span data-stu-id="32505-134">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="32505-135">CLI 会提出一些问题来引导创建项目。</span><span class="sxs-lookup"><span data-stu-id="32505-135">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="32505-136">每个问题将告诉你该如何回答（例如，使用箭头键选择一个选项）。</span><span class="sxs-lookup"><span data-stu-id="32505-136">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="32505-137">如果已回答问题，请通过按 **Enter** 确认。</span><span class="sxs-lookup"><span data-stu-id="32505-137">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="32505-138">选择 **创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="32505-138">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="32505-139">选择 **机器人** 功能，然后取消选择 **选项卡** 功能。</span><span class="sxs-lookup"><span data-stu-id="32505-139">Select the **Bot** capability and deselect the **Tab** capability.</span></span>
1. <span data-ttu-id="32505-140">选择 **创建新的机器人注册**。</span><span class="sxs-lookup"><span data-stu-id="32505-140">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="32505-141">选择 **JavaScript** 作为编程语言。</span><span class="sxs-lookup"><span data-stu-id="32505-141">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="32505-142">按 **Enter** 选择默认工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="32505-142">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="32505-143">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="32505-143">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="32505-144">应用的名称只能包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="32505-144">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="32505-145">回答所有问题后，将创建项目。</span><span class="sxs-lookup"><span data-stu-id="32505-145">Once all the questions have been answered, your project will be created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="32505-146">浏览源代码</span><span class="sxs-lookup"><span data-stu-id="32505-146">Take a tour of the source code</span></span>

<span data-ttu-id="32505-147">若要暂时跳过此部分，可以 [在本地运行应用](#run-your-app-locally)。</span><span class="sxs-lookup"><span data-stu-id="32505-147">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="32505-148">消息扩展使用 [Bot Framework](https://docs.botframework.com) 以允许用户通过对话与你的服务交互。</span><span class="sxs-lookup"><span data-stu-id="32505-148">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="32505-149">设置标点文件夹后，你的项目将如下所示:</span><span class="sxs-lookup"><span data-stu-id="32505-149">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/bot-file-layout.png" alt-text="机器人项目的文件布局。":::

<span data-ttu-id="32505-151">机器人程序代码存储在 `bot` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="32505-151">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="32505-152">`bots/teamsBot.js` 是机器人的主入口点，对话将存储在 `dialogs` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="32505-152">The `bots/teamsBot.js` is the main entry point for the bot, and the dialogs are stored in the `dialogs` directory.</span></span>

> [!Tip]
> <span data-ttu-id="32505-153">在将第一个机器人集成到 Teams 中之前，请熟悉 Teams 以外的机器人。</span><span class="sxs-lookup"><span data-stu-id="32505-153">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="32505-154">可以通过查看 [Azure 机器人服务](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)教程找到有关机器人的更多信息。</span><span class="sxs-lookup"><span data-stu-id="32505-154">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="32505-155">在本地运行应用</span><span class="sxs-lookup"><span data-stu-id="32505-155">Run your app locally</span></span>

<span data-ttu-id="32505-156">Teams 工具包允许你在本地托管应用。</span><span class="sxs-lookup"><span data-stu-id="32505-156">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="32505-157">为此，请执行以下操作:</span><span class="sxs-lookup"><span data-stu-id="32505-157">To do this:</span></span>

- <span data-ttu-id="32505-158">Azure Active Directory 应用程序是在 M365 租户中注册的。</span><span class="sxs-lookup"><span data-stu-id="32505-158">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="32505-159">向 Teams 开发人员中心提交应用清单。</span><span class="sxs-lookup"><span data-stu-id="32505-159">An app manifest is submitted to the Developer Center for Teams.</span></span>
- <span data-ttu-id="32505-160">在本地使用 Azure Functions Core Tools 运行 API，以支持你的应用。</span><span class="sxs-lookup"><span data-stu-id="32505-160">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="32505-161">[ngrok](https://ngrok.io) 安装并用于在 Teams 和机器人代码之间提供一个隧道。</span><span class="sxs-lookup"><span data-stu-id="32505-161">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your bot code.</span></span>

<span data-ttu-id="32505-162">若要在本地构建并运行应用程序:</span><span class="sxs-lookup"><span data-stu-id="32505-162">To build and run your app locally:</span></span>

1. <span data-ttu-id="32505-163">在 Visual Studio Code 中，按 **F5** 以在调试模式下运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="32505-163">From Visual Studio Code, press **F5** to run your application in debug mode.</span></span>

   > <span data-ttu-id="32505-164">首次运行该应用时，将下载所有依赖项并编译该应用。</span><span class="sxs-lookup"><span data-stu-id="32505-164">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="32505-165">编译完成后，将自动打开浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="32505-165">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="32505-166">这可能需要 3-5 分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="32505-166">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="32505-167">启动 Web 浏览器以运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="32505-167">Your web browser is started to run the application.</span></span> <span data-ttu-id="32505-168">如果系统提示打开 Microsoft Teams，请选择"取消"以留在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="32505-168">If prompted to open Microsoft Teams, select Cancel to remain within the browser.</span></span> <span data-ttu-id="32505-169">系统提示时，选择 **使用 Web 应用**。</span><span class="sxs-lookup"><span data-stu-id="32505-169">When prompted, select **Use the web app instead**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="显示启动后如何选择 Teams 的 Web 版本的屏幕截图":::

1. <span data-ttu-id="32505-171">系统可能会提示你登录。</span><span class="sxs-lookup"><span data-stu-id="32505-171">You may be prompted to sign in.</span></span>  <span data-ttu-id="32505-172">如果是这样，则使用你的 M365 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="32505-172">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="32505-173">系统提示将应用安装到 Teams 时，按 **添加**。</span><span class="sxs-lookup"><span data-stu-id="32505-173">When prompted to install the app onto Teams, press **Add**.</span></span>

<span data-ttu-id="32505-174">加载应用后，你将直接进入与机器人的聊天会话。</span><span class="sxs-lookup"><span data-stu-id="32505-174">Once the app is loaded, you will be taken directly to a chat session with the bot.</span></span>  <span data-ttu-id="32505-175">你可以键入 `intro` 以显示简介卡，键入 `show` 以显示你在 Microsoft Graph 中的详细信息。</span><span class="sxs-lookup"><span data-stu-id="32505-175">You can type `intro` to show an introduction card, and `show` to show your details from Microsoft Graph.</span></span>  <span data-ttu-id="32505-176">(这需要额外审批权限)。</span><span class="sxs-lookup"><span data-stu-id="32505-176">(This will require an additional permissions approval).</span></span>

<span data-ttu-id="32505-177">调试工作如你通常预期一样 - 自己试一试！</span><span class="sxs-lookup"><span data-stu-id="32505-177">Debugging works as you normally would expect - try it yourself!</span></span> <span data-ttu-id="32505-178">打开 `bot/dialogs/rootDialog.js` 文件并找到 `triggerCommand(...)` 方法。</span><span class="sxs-lookup"><span data-stu-id="32505-178">Open the `bot/dialogs/rootDialog.js` file and locate the `triggerCommand(...)` method.</span></span>  <span data-ttu-id="32505-179">为默认情况设置断点。</span><span class="sxs-lookup"><span data-stu-id="32505-179">Set a breakpoint on the default case.</span></span>  <span data-ttu-id="32505-180">然后键入一些文本。</span><span class="sxs-lookup"><span data-stu-id="32505-180">Then type some text.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="32505-181">在本地调试器中运行应用时，了解会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="32505-181">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="32505-182">按 F5 时，Teams 工具包:</span><span class="sxs-lookup"><span data-stu-id="32505-182">When you pressed F5, the Teams Toolkit:</span></span>

1. <span data-ttu-id="32505-183">使用 Azure Active Directory 注册应用程序。</span><span class="sxs-lookup"><span data-stu-id="32505-183">Registered your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="32505-184">在 Microsoft Teams 中将你的应用程序注册为“旁加载”。</span><span class="sxs-lookup"><span data-stu-id="32505-184">Registered your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="32505-185">使用 [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start) 启动在本地运行的应用程序后端。</span><span class="sxs-lookup"><span data-stu-id="32505-185">Started your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="32505-186">启动 ngrok 隧道，以便 Teams 可以与你的应用通信。</span><span class="sxs-lookup"><span data-stu-id="32505-186">Started an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="32505-187">启动 Microsoft Teams，并用命令指示 Teams 旁加载该应用程序。</span><span class="sxs-lookup"><span data-stu-id="32505-187">Started Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="32505-188">了解如何在本地运行应用时解决常见问题。</span><span class="sxs-lookup"><span data-stu-id="32505-188">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="32505-189">若要在 Teams 中成功运行应用，必须具有允许应用程序旁加载的 Microsoft 365 开发帐户。</span><span class="sxs-lookup"><span data-stu-id="32505-189">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="32505-190">有关开设帐户的详细信息，请参阅 [先决条件](prerequisites.md#enable-sideloading)。</span><span class="sxs-lookup"><span data-stu-id="32505-190">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="32505-191">在旁加载应用之前，使用工具包中包含的 [应用验证工具](https://dev.teams.microsoft.com/appvalidation.html) 检查问题。</span><span class="sxs-lookup"><span data-stu-id="32505-191">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="32505-192">修复错误以成功旁加载应用。</span><span class="sxs-lookup"><span data-stu-id="32505-192">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="32505-193">了解将应用部署到 Azure 时会发生的情况</span><span class="sxs-lookup"><span data-stu-id="32505-193">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="32505-194">部署之前，应用程序已在本地运行:</span><span class="sxs-lookup"><span data-stu-id="32505-194">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="32505-195">后端使用 _Azure Functions Core Tools_ 运行。</span><span class="sxs-lookup"><span data-stu-id="32505-195">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="32505-196">应用程序 HTTP 终结点 (Microsoft Teams 在此加载应用程序) 在本地运行。</span><span class="sxs-lookup"><span data-stu-id="32505-196">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

<span data-ttu-id="32505-197">部署涉及预配活动 Azure 订阅上的资源，以及将应用程序后端和前端代码部署（上传）到 Azure。</span><span class="sxs-lookup"><span data-stu-id="32505-197">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="32505-198">后端使用多种 Azure 服务，包括 Azure 应用服务 和 Azure 机器人服务。</span><span class="sxs-lookup"><span data-stu-id="32505-198">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="next-steps"></a><span data-ttu-id="32505-199">后续步骤</span><span class="sxs-lookup"><span data-stu-id="32505-199">Next steps</span></span>

<span data-ttu-id="32505-200">了解创建 Teams 应用的其他方法:</span><span class="sxs-lookup"><span data-stu-id="32505-200">Learn about other methods for creating Teams apps:</span></span>

- [<span data-ttu-id="32505-201">使用 React 创建 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="32505-201">Create a Teams app with React</span></span>](first-app-react.md)
- [<span data-ttu-id="32505-202">使用 Blazor 创建 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="32505-202">Create a Teams app with Blazor</span></span>](first-app-blazor.md)
- <span data-ttu-id="32505-203">[将 Teams 应用创建为 SharePoint Web 部件](first-app-spfx.md) (不需要 Azure)</span><span class="sxs-lookup"><span data-stu-id="32505-203">[Create a Teams app as a SharePoint Web Part](first-app-spfx.md) (Azure not required)</span></span>
- [<span data-ttu-id="32505-204">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="32505-204">Create a messaging extension</span></span>](first-message-extension.md)
