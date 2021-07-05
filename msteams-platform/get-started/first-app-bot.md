---
title: 入门 - 构建你的第一个对话机器人
author: adrianhall
description: 使用 Teams 工具包为 Microsoft Teams 创建对话机器人。
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: 96bbddd99b6901a4b92e1e2f2dc98482c755dc66
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254249"
---
# <a name="build-your-first-conversational-bot-for-microsoft-teams"></a><span data-ttu-id="c0515-103">构建你的第一个 Microsoft Teams 对话机器人</span><span class="sxs-lookup"><span data-stu-id="c0515-103">Build your first conversational bot for Microsoft Teams</span></span>

<span data-ttu-id="c0515-104">在本教程中，你将了解如何构建、运行和部署 Teams 机器人应用。</span><span class="sxs-lookup"><span data-stu-id="c0515-104">In this tutorial, you will learn how to build, run, and deploy a Teams bot app.</span></span> <span data-ttu-id="c0515-105">机器人是 Teams 用户和 Web 服务之间的中介。</span><span class="sxs-lookup"><span data-stu-id="c0515-105">A bot acts as an intermediary between a Teams user and a web service.</span></span>  <span data-ttu-id="c0515-106">用户可以与机器人聊天，以快速获取信息、启动工作流或启动 Web 服务能够执行的任何操作。</span><span class="sxs-lookup"><span data-stu-id="c0515-106">Users can chat with a bot to quickly get information, initiate workflows, or anything else your web service can do.</span></span> 

## <a name="before-you-begin"></a><span data-ttu-id="c0515-107">开始之前</span><span class="sxs-lookup"><span data-stu-id="c0515-107">Before you begin</span></span>

<span data-ttu-id="c0515-108">通过安装先决条件确保已设置开发环境。</span><span class="sxs-lookup"><span data-stu-id="c0515-108">Make sure your development environment is set up by installing the Prerequisites.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c0515-109">安装先决条件</span><span class="sxs-lookup"><span data-stu-id="c0515-109">Install Prerequisites</span></span>](prerequisites.md)

## <a name="create-your-project"></a><span data-ttu-id="c0515-110">创建项目</span><span class="sxs-lookup"><span data-stu-id="c0515-110">Create your project</span></span>

<span data-ttu-id="c0515-111">使用 Teams 工具包创建你的第一个项目:</span><span class="sxs-lookup"><span data-stu-id="c0515-111">Use the Teams Toolkit to create your first project:</span></span>

# <a name="visual-studio-code"></a>[<span data-ttu-id="c0515-112">Visual Studio Code</span><span class="sxs-lookup"><span data-stu-id="c0515-112">Visual Studio Code</span></span>](#tab/vscode)

1. <span data-ttu-id="c0515-113">打开 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="c0515-113">Open Visual Studio code.</span></span>
1. <span data-ttu-id="c0515-114">选择边Teams图标以打开Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="c0515-114">Select the Teams icon in the sidebar to open the Teams Toolkit.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code 边栏中的 Teams 图标。":::

1. <span data-ttu-id="c0515-116">选择 **创建新项目**。</span><span class="sxs-lookup"><span data-stu-id="c0515-116">Select **Create New Project**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. <span data-ttu-id="c0515-118">选择 **创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="c0515-118">Select **Create a new Teams app**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="&quot;创建新项目&quot;的向导启动":::

1. <span data-ttu-id="c0515-120">在"**选择功能"** 部分，选择"**自动** 程序"，取消选择 **"选项卡**"，然后选择"确定 **"。**</span><span class="sxs-lookup"><span data-stu-id="c0515-120">In the **Select capabilities** section, select **Bot**, deselect **Tab** and select **OK**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities-bot.png" alt-text="显示如何向新应用添加功能的屏幕截图。":::

1. <span data-ttu-id="c0515-122">在"**自动程序注册"** 部分，**选择"创建新的自动程序注册"。**</span><span class="sxs-lookup"><span data-stu-id="c0515-122">In the **Bot registration** section, select **Create a new bot registration**.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="选择创建新的机器人注册":::

1. <span data-ttu-id="c0515-124">在"**编程语言"部分**，选择 **"JavaScript"。**</span><span class="sxs-lookup"><span data-stu-id="c0515-124">In the **Programming Language** section, select **JavaScript**.</span></span>

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="显示如何选择编程语言的屏幕截图。":::

1. <span data-ttu-id="c0515-126">选择工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="c0515-126">Select a workspace folder.</span></span>  <span data-ttu-id="c0515-127">将在工作区文件夹中为正在创建的项目创建一个文件夹。</span><span class="sxs-lookup"><span data-stu-id="c0515-127">A folder will be created within your workspace folder for the project you are creating.</span></span>

1. <span data-ttu-id="c0515-128">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="c0515-128">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="c0515-129">应用的名称必须仅包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="c0515-129">The name of the app must contain only alphanumeric characters.</span></span>  <span data-ttu-id="c0515-130">按 **Enter** 以继续。</span><span class="sxs-lookup"><span data-stu-id="c0515-130">Press **Enter** to continue.</span></span>

<span data-ttu-id="c0515-131">将在数秒钟内创建你的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="c0515-131">Your Teams app will be created within a few seconds.</span></span>

# <a name="command-line"></a>[<span data-ttu-id="c0515-132">命令行</span><span class="sxs-lookup"><span data-stu-id="c0515-132">Command line</span></span>](#tab/cli)

<span data-ttu-id="c0515-133">使用 `teamsfx` CLI 创建你的第一个项目。</span><span class="sxs-lookup"><span data-stu-id="c0515-133">Use the `teamsfx` CLI to create your first project.</span></span>  <span data-ttu-id="c0515-134">从要创建项目文件夹的文件夹开始。</span><span class="sxs-lookup"><span data-stu-id="c0515-134">Start from the folder where you want to create the project folder.</span></span>

``` bash
teamsfx new
```

<span data-ttu-id="c0515-135">CLI 会提出一些问题来引导创建项目。</span><span class="sxs-lookup"><span data-stu-id="c0515-135">The CLI walks through some questions to create the project.</span></span>  <span data-ttu-id="c0515-136">每个问题将告诉你该如何回答（例如，使用箭头键选择一个选项）。</span><span class="sxs-lookup"><span data-stu-id="c0515-136">Each question will tell you how to answer it (for example, to use arrow keys to select an option).</span></span>  <span data-ttu-id="c0515-137">如果已回答问题，请通过按 **Enter** 确认。</span><span class="sxs-lookup"><span data-stu-id="c0515-137">When you have answered the question, confirm your choice by pressing **Enter**.</span></span>

1. <span data-ttu-id="c0515-138">选择 **创建新的 Teams 应用**。</span><span class="sxs-lookup"><span data-stu-id="c0515-138">Select **Create a new Teams app**.</span></span>
1. <span data-ttu-id="c0515-139">选择 **自动程序** ，然后取消选择 **选项卡**。</span><span class="sxs-lookup"><span data-stu-id="c0515-139">Select **Bot** and deselect **Tab**.</span></span>
1. <span data-ttu-id="c0515-140">选择 **创建新的机器人注册**。</span><span class="sxs-lookup"><span data-stu-id="c0515-140">Select **Create a new bot registration**.</span></span>
1. <span data-ttu-id="c0515-141">选择 **JavaScript** 作为编程语言。</span><span class="sxs-lookup"><span data-stu-id="c0515-141">Select **JavaScript** as the programming language.</span></span>
1. <span data-ttu-id="c0515-142">按 **Enter** 选择默认工作区文件夹。</span><span class="sxs-lookup"><span data-stu-id="c0515-142">Press **Enter** to select the default workspace folder.</span></span>
1. <span data-ttu-id="c0515-143">为应用输入合适的名称，如 `helloworld`。</span><span class="sxs-lookup"><span data-stu-id="c0515-143">Enter a suitable name for your app, like `helloworld`.</span></span>  <span data-ttu-id="c0515-144">应用的名称只能包含字母数字字符。</span><span class="sxs-lookup"><span data-stu-id="c0515-144">The name of the app must consist only of alphanumeric characters.</span></span>

<span data-ttu-id="c0515-145">在回答所有问题后，将创建项目。</span><span class="sxs-lookup"><span data-stu-id="c0515-145">After all the questions have been answered, your project is created.</span></span>

---

## <a name="take-a-tour-of-the-source-code"></a><span data-ttu-id="c0515-146">浏览源代码</span><span class="sxs-lookup"><span data-stu-id="c0515-146">Take a tour of the source code</span></span>

<span data-ttu-id="c0515-147">若要暂时跳过此部分，可以 [在本地运行应用](#run-your-app-locally)。</span><span class="sxs-lookup"><span data-stu-id="c0515-147">If you wish to skip this section for now, you can [run your app locally](#run-your-app-locally).</span></span>

<span data-ttu-id="c0515-148">消息扩展使用 [Bot Framework](https://docs.botframework.com) 以允许用户通过对话与你的服务交互。</span><span class="sxs-lookup"><span data-stu-id="c0515-148">A messaging extension uses the [Bot Framework](https://docs.botframework.com) to allow the user to interact with your service via a conversation.</span></span>  <span data-ttu-id="c0515-149">设置标点文件夹后，你的项目将如下所示:</span><span class="sxs-lookup"><span data-stu-id="c0515-149">After scaffolding, your project will look like this:</span></span>

:::image type="content" source="../assets/images/teams-toolkit-v2/bot-file-layout.png" alt-text="机器人项目的文件布局。":::

<span data-ttu-id="c0515-151">机器人程序代码存储在 `bot` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="c0515-151">The bot code is stored in the `bot` directory.</span></span>  <span data-ttu-id="c0515-152">`bot/teamsBot.js` 是机器人的主入口点，对话将存储在 `dialogs` 文件夹中。</span><span class="sxs-lookup"><span data-stu-id="c0515-152">The `bot/teamsBot.js` is the main entry point for the bot, and the dialogs are stored in the `dialogs` directory.</span></span>

> [!Tip]
> <span data-ttu-id="c0515-153">在将第一个机器人集成到 Teams 中之前，请熟悉 Teams 以外的机器人。</span><span class="sxs-lookup"><span data-stu-id="c0515-153">Familiarize yourself with bots outside of Teams before you integrate your first bot within Teams.</span></span>  <span data-ttu-id="c0515-154">可以通过查看 [Azure 机器人服务](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)教程找到有关机器人的更多信息。</span><span class="sxs-lookup"><span data-stu-id="c0515-154">You can find more information about bots by reviewing the [Azure Bot Service](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true) tutorials.</span></span>

## <a name="run-your-app-locally"></a><span data-ttu-id="c0515-155">在本地运行应用</span><span class="sxs-lookup"><span data-stu-id="c0515-155">Run your app locally</span></span>

<span data-ttu-id="c0515-156">Teams 工具包允许你在本地托管应用。</span><span class="sxs-lookup"><span data-stu-id="c0515-156">Teams Toolkit allows you to host your app locally.</span></span>  <span data-ttu-id="c0515-157">为此，请执行以下操作:</span><span class="sxs-lookup"><span data-stu-id="c0515-157">To do this:</span></span>

- <span data-ttu-id="c0515-158">Azure Active Directory 应用程序是在 M365 租户中注册的。</span><span class="sxs-lookup"><span data-stu-id="c0515-158">An Azure Active Directory Application is registered within the M365 tenant.</span></span>
- <span data-ttu-id="c0515-159">向 Teams 开发人员中心提交应用清单。</span><span class="sxs-lookup"><span data-stu-id="c0515-159">An app manifest is submitted to the Developer Center for Teams.</span></span>
- <span data-ttu-id="c0515-160">在本地使用 Azure Functions Core Tools 运行 API，以支持你的应用。</span><span class="sxs-lookup"><span data-stu-id="c0515-160">An API is run locally using Azure Functions Core Tools to support your app.</span></span>
- <span data-ttu-id="c0515-161">[ngrok](https://ngrok.io) 安装并用于在 Teams 和机器人代码之间提供一个隧道。</span><span class="sxs-lookup"><span data-stu-id="c0515-161">[ngrok](https://ngrok.io) is installed and used to provide a tunnel between Teams and your bot code.</span></span>

<span data-ttu-id="c0515-162">若要在本地构建并运行应用程序:</span><span class="sxs-lookup"><span data-stu-id="c0515-162">To build and run your app locally:</span></span>

1. <span data-ttu-id="c0515-163">在Visual Studio Code中，按 **F5** 键以在调试模式下运行应用程序。</span><span class="sxs-lookup"><span data-stu-id="c0515-163">From Visual Studio Code, press the **F5** key to run your application in debug mode.</span></span>

   > <span data-ttu-id="c0515-164">首次运行该应用时，将下载所有依赖项并编译该应用。</span><span class="sxs-lookup"><span data-stu-id="c0515-164">When you run the app for the first time, all dependencies are downloaded and the app is built.</span></span>  <span data-ttu-id="c0515-165">编译完成后，将自动打开浏览器窗口。</span><span class="sxs-lookup"><span data-stu-id="c0515-165">A browser window automatically opens when the build is complete.</span></span>  <span data-ttu-id="c0515-166">这可能需要 3-5 分钟才能完成。</span><span class="sxs-lookup"><span data-stu-id="c0515-166">This can take 3-5 minutes to complete.</span></span>

1. <span data-ttu-id="c0515-167">Web 浏览器开始运行该应用。</span><span class="sxs-lookup"><span data-stu-id="c0515-167">Your web browser starts to run the app.</span></span> <span data-ttu-id="c0515-168">如果系统提示打开Teams，请选择 **"取消**"以保留在浏览器中。</span><span class="sxs-lookup"><span data-stu-id="c0515-168">If prompted to open Teams desktop, select **Cancel** to remain in the browser.</span></span> <span data-ttu-id="c0515-169">系统有时还可能会提示你切换到Teams桌面;选择Teams Web 应用。</span><span class="sxs-lookup"><span data-stu-id="c0515-169">You may also be prompted to switch to Teams desktop at other times; select the Teams web app when this happens.</span></span>

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="显示启动后如何选择 Teams 的 Web 版本的屏幕截图":::

1. <span data-ttu-id="c0515-171">系统可能会提示你登录。</span><span class="sxs-lookup"><span data-stu-id="c0515-171">You may be prompted to sign in.</span></span>  <span data-ttu-id="c0515-172">如果是这样，则使用你的 M365 帐户登录。</span><span class="sxs-lookup"><span data-stu-id="c0515-172">If so, sign in with your M365 account.</span></span>
1. <span data-ttu-id="c0515-173">当系统提示将应用安装到 Teams 时，选择"添加 **"。**</span><span class="sxs-lookup"><span data-stu-id="c0515-173">When prompted to install the app onto Teams, select **Add**.</span></span>

   <span data-ttu-id="c0515-174">加载应用后，你将直接进入与机器人的聊天会话。</span><span class="sxs-lookup"><span data-stu-id="c0515-174">After the app is loaded, you will be taken directly to a chat session with the bot.</span></span>  <span data-ttu-id="c0515-175">你可以键入 `intro` 以显示简介卡，键入 `show` 以显示你在 Microsoft Graph 中的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c0515-175">You can type `intro` to show an introduction card, and `show` to show your details from Microsoft Graph.</span></span>  <span data-ttu-id="c0515-176">(这需要额外审批权限)。</span><span class="sxs-lookup"><span data-stu-id="c0515-176">(This will require an additional permissions approval).</span></span>

   <span data-ttu-id="c0515-177">调试工作如你通常预期一样 - 自己试一试！</span><span class="sxs-lookup"><span data-stu-id="c0515-177">Debugging works as you normally would expect - try it yourself!</span></span> <span data-ttu-id="c0515-178">打开 `bot/dialogs/rootDialog.js` 文件并找到 `triggerCommand(...)` 方法。</span><span class="sxs-lookup"><span data-stu-id="c0515-178">Open the `bot/dialogs/rootDialog.js` file and locate the `triggerCommand(...)` method.</span></span>  <span data-ttu-id="c0515-179">为默认情况设置断点。</span><span class="sxs-lookup"><span data-stu-id="c0515-179">Set a breakpoint on the default case.</span></span>  <span data-ttu-id="c0515-180">然后键入一些文本。</span><span class="sxs-lookup"><span data-stu-id="c0515-180">Then type some text.</span></span>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="c0515-181">在本地调试器中运行应用时，了解会发生什么情况。</span><span class="sxs-lookup"><span data-stu-id="c0515-181">Learn what happens when you run your app locally in the debugger.</span></span></summary>

<span data-ttu-id="c0515-182">按 **F5 键** 时，Teams Toolkit：</span><span class="sxs-lookup"><span data-stu-id="c0515-182">When you press the **F5** key, the Teams Toolkit:</span></span>

1. <span data-ttu-id="c0515-183">向应用程序注册Azure Active Directory。</span><span class="sxs-lookup"><span data-stu-id="c0515-183">Registers your application with Azure Active Directory.</span></span>
1. <span data-ttu-id="c0515-184">将应用程序注册为"旁加载"Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="c0515-184">Registers your application for "side loading" in Microsoft Teams.</span></span>
1. <span data-ttu-id="c0515-185">使用 Azure 函数核心工具 启动本地 [运行的应用程序后端](/azure/azure-functions/functions-run-local?#start)。</span><span class="sxs-lookup"><span data-stu-id="c0515-185">Starts your application backend running locally using [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start).</span></span>
1. <span data-ttu-id="c0515-186">启动 ngrok 隧道，Teams应用进行通信。</span><span class="sxs-lookup"><span data-stu-id="c0515-186">Starts an ngrok tunnel so Teams can communicate with your app.</span></span>
1. <span data-ttu-id="c0515-187">首先Microsoft Teams命令指示Teams旁加载应用程序。</span><span class="sxs-lookup"><span data-stu-id="c0515-187">Starts Microsoft Teams with a command to instruct Teams to sideload the application.</span></span>

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary><span data-ttu-id="c0515-188">了解如何在本地运行应用时解决常见问题。</span><span class="sxs-lookup"><span data-stu-id="c0515-188">Learn how to troubleshoot common issues when running your app locally.</span></span></summary>

<span data-ttu-id="c0515-189">若要在 Teams 中成功运行应用，必须具有允许应用程序旁加载的 Microsoft 365 开发帐户。</span><span class="sxs-lookup"><span data-stu-id="c0515-189">To successfully run your app in Teams, you must have a Microsoft 365 development account that allows app sideloading.</span></span> <span data-ttu-id="c0515-190">有关开设帐户的详细信息，请参阅 [先决条件](prerequisites.md#enable-sideloading)。</span><span class="sxs-lookup"><span data-stu-id="c0515-190">For more information on account opening, see [Prerequisites](prerequisites.md#enable-sideloading).</span></span>

> [!TIP]
> <span data-ttu-id="c0515-191">在旁加载应用之前，使用工具包中包含的 [应用验证工具](https://dev.teams.microsoft.com/appvalidation.html) 检查问题。</span><span class="sxs-lookup"><span data-stu-id="c0515-191">Check for issues before sideloading your app, using the [app validation tool](https://dev.teams.microsoft.com/appvalidation.html), which is included in the toolkit.</span></span> <span data-ttu-id="c0515-192">修复错误以成功旁加载应用。</span><span class="sxs-lookup"><span data-stu-id="c0515-192">Fix the errors to successfully sideload the app.</span></span>
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary><span data-ttu-id="c0515-193">了解将应用部署到 Azure 时会发生的情况</span><span class="sxs-lookup"><span data-stu-id="c0515-193">Learn what happens when you deployed your app to Azure</span></span></summary>

<span data-ttu-id="c0515-194">部署之前，应用程序已在本地运行:</span><span class="sxs-lookup"><span data-stu-id="c0515-194">Before deployment, the application has been running locally:</span></span>

1. <span data-ttu-id="c0515-195">后端使用 _Azure Functions Core Tools_ 运行。</span><span class="sxs-lookup"><span data-stu-id="c0515-195">The backend runs using _Azure Functions Core Tools_.</span></span>
1. <span data-ttu-id="c0515-196">应用程序 HTTP 终结点 (Microsoft Teams 在此加载应用程序) 在本地运行。</span><span class="sxs-lookup"><span data-stu-id="c0515-196">The application HTTP endpoint, where Microsoft Teams loads the application, runs locally.</span></span>

   <span data-ttu-id="c0515-197">部署涉及预配活动 Azure 订阅上的资源，以及将应用程序后端和前端代码部署（上传）到 Azure。</span><span class="sxs-lookup"><span data-stu-id="c0515-197">Deployment involves provisioning resources on an active Azure subscription and deploying (uploading) the backend and frontend code for the application to Azure.</span></span> <span data-ttu-id="c0515-198">后端使用多种 Azure 服务，包括 Azure 应用服务 和 Azure 机器人服务。</span><span class="sxs-lookup"><span data-stu-id="c0515-198">The backend uses a variety of Azure services, including Azure App Service and Azure Bot Service.</span></span>

</details>

## <a name="see-also"></a><span data-ttu-id="c0515-199">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c0515-199">See also</span></span>

* [<span data-ttu-id="c0515-200">教程概述</span><span class="sxs-lookup"><span data-stu-id="c0515-200">Tutorials Overview</span></span>](code-samples.md) 
* [<span data-ttu-id="c0515-201">使用应用程序创建React</span><span class="sxs-lookup"><span data-stu-id="c0515-201">Create an app using React</span></span>](first-app-react.md)
* [<span data-ttu-id="c0515-202">使用 Blazor 创建应用</span><span class="sxs-lookup"><span data-stu-id="c0515-202">Create an app using Blazor</span></span>](first-app-blazor.md)
* [<span data-ttu-id="c0515-203">使用应用程序创建SPFx</span><span class="sxs-lookup"><span data-stu-id="c0515-203">Create an app using SPFx</span></span>](first-app-spfx.md)
* [<span data-ttu-id="c0515-204">使用或 C# .NET 创建应用</span><span class="sxs-lookup"><span data-stu-id="c0515-204">Create an app using C# or .NET</span></span>](get-started-dotnet-app-studio.md)
* [<span data-ttu-id="c0515-205">使用Node.js创建应用</span><span class="sxs-lookup"><span data-stu-id="c0515-205">Create an app using Node.js</span></span>](get-started-nodejs-app-studio.md)
* [<span data-ttu-id="c0515-206">使用 Yeoman 生成器创建应用</span><span class="sxs-lookup"><span data-stu-id="c0515-206">Create an app using Yeoman generator</span></span>](get-started-yeoman.md)
* [<span data-ttu-id="c0515-207">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="c0515-207">Create a messaging extension</span></span>](first-message-extension.md)
* [<span data-ttu-id="c0515-208">代码示例</span><span class="sxs-lookup"><span data-stu-id="c0515-208">Code Samples</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples)