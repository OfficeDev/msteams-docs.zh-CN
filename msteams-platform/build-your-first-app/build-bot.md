---
title: 入门 - 生成自动程序
author: girliemac
description: 使用Microsoft Teams快速创建自动程序Microsoft Teams Toolkit。
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: 2cbd90b293e8ac8343febc7b3d23278d5bb5bf82
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565884"
---
# <a name="create-your-first-bot-for-teams"></a><span data-ttu-id="10d1c-103">创建第一个自动程序Teams</span><span class="sxs-lookup"><span data-stu-id="10d1c-103">Create your first bot for Teams</span></span>

<span data-ttu-id="10d1c-104">本教程指导你生成基本自动程序应用。</span><span class="sxs-lookup"><span data-stu-id="10d1c-104">This tutorial teaches you to build a basic bot app.</span></span> <span data-ttu-id="10d1c-105">自动程序充当用户Teams会话界面的 Web 应用或服务之间的中介。</span><span class="sxs-lookup"><span data-stu-id="10d1c-105">A bot acts as an intermediary between Teams users and your web app or service with a conversational interface.</span></span> <span data-ttu-id="10d1c-106">用户可以与机器人聊天，以快速获取信息或启动服务执行的工作流和任务。</span><span class="sxs-lookup"><span data-stu-id="10d1c-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="10d1c-107">您将了解哪些功能</span><span class="sxs-lookup"><span data-stu-id="10d1c-107">What you'll learn</span></span>

* <span data-ttu-id="10d1c-108">使用 Microsoft Teams Toolkit 创建应用项目和Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="10d1c-108">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="10d1c-109">了解Teams自动程序相关的应用配置。</span><span class="sxs-lookup"><span data-stu-id="10d1c-109">Understand the Teams app configurations relevant to bots.</span></span>
* <span data-ttu-id="10d1c-110">使用 localhost 隧道解决方案在本地托管和运行应用。</span><span class="sxs-lookup"><span data-stu-id="10d1c-110">Host and run an app locally using a localhost tunneling solution.</span></span>
* <span data-ttu-id="10d1c-111">旁加载和测试自动程序Teams。</span><span class="sxs-lookup"><span data-stu-id="10d1c-111">Sideload and test a bot in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="10d1c-112">先决条件</span><span class="sxs-lookup"><span data-stu-id="10d1c-112">Prerequisites</span></span>

<span data-ttu-id="10d1c-113">确保你了解如何设置和构建简单的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="10d1c-113">Ensure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="10d1c-114">有关详细信息，请参阅创建[你的第一个Microsoft Teams Hello， World！"应用](../build-your-first-app/build-and-run.md)。</span><span class="sxs-lookup"><span data-stu-id="10d1c-114">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span> 

## <a name="1-create-your-app-project"></a><span data-ttu-id="10d1c-115">1. 创建应用项目</span><span class="sxs-lookup"><span data-stu-id="10d1c-115">1. Create your app project</span></span>

<span data-ttu-id="10d1c-116">以下Microsoft Teams Toolkit可帮助你为应用设置以下组件：</span><span class="sxs-lookup"><span data-stu-id="10d1c-116">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span> 

* <span data-ttu-id="10d1c-117">**与机器人相关的应用** 配置和基架。</span><span class="sxs-lookup"><span data-stu-id="10d1c-117">**App configurations and scaffolding** relevant to bots.</span></span>
* <span data-ttu-id="10d1c-118">**自动** 注册到自动程序服务Microsoft Azure自动程序。</span><span class="sxs-lookup"><span data-stu-id="10d1c-118">**Bot** that's automatically registered with the Microsoft Azure Bot Service.</span></span>

<span data-ttu-id="10d1c-119">**创建应用项目**</span><span class="sxs-lookup"><span data-stu-id="10d1c-119">**To create your app project**</span></span>

1. In Visual Studio Code， select **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: on the left Activity Bar and choose Create a new **Teams app**.

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="显示如何在应用商店中创建应用的Teams Toolkit。":::

1. <span data-ttu-id="10d1c-122">当系统提示时，使用你的 Microsoft 365帐户登录。</span><span class="sxs-lookup"><span data-stu-id="10d1c-122">When prompted, sign in with your Microsoft 365 development account.</span></span> 
1. <span data-ttu-id="10d1c-123">在"选择项目"屏幕上，选择"对话机器人"：</span><span class="sxs-lookup"><span data-stu-id="10d1c-123">On the Select project screen, select Conversation bots:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Screenshot showing how to create a new bot in the Teams Toolkit.":::

1. <span data-ttu-id="10d1c-125">在" **配置项目"** 屏幕上，输入自动程序的名称。</span><span class="sxs-lookup"><span data-stu-id="10d1c-125">On the **Configure project** screen, enter a name for your bot.</span></span> <span data-ttu-id="10d1c-126">这是应用的默认名称，也是本地计算机上应用项目目录的名称。</span><span class="sxs-lookup"><span data-stu-id="10d1c-126">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="10d1c-127">选择 **"新建自动**  >  **程序创建自动** 程序注册"，如下图所示：</span><span class="sxs-lookup"><span data-stu-id="10d1c-127">Select **Create a new Bot** > **Create Bot Registration** as shown in the following image:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Screenshot showing naming new bot in the Teams Toolkit.":::

    <span data-ttu-id="10d1c-129">如果成功，你的新自动程序将具有 **"已注册"** 状态。</span><span class="sxs-lookup"><span data-stu-id="10d1c-129">If successful, your new bot will have a **Registered** status.</span></span> <span data-ttu-id="10d1c-130">现在，自动程序将自动注册到 Microsoft Azure Bot Service。</span><span class="sxs-lookup"><span data-stu-id="10d1c-130">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Screenshot showing registering new bot in the Teams Toolkit.":::

1. <span data-ttu-id="10d1c-132">选择 **屏幕** 底部的"完成"，然后在你的计算机上保存项目。</span><span class="sxs-lookup"><span data-stu-id="10d1c-132">Select **Finish** at the bottom of the screen and save your project on your machine.</span></span>  

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="10d1c-133">2. 了解应用项目组件</span><span class="sxs-lookup"><span data-stu-id="10d1c-133">2. Understand your app project components</span></span>

<span data-ttu-id="10d1c-134">使用应用程序配置和基架创建项目时，许多应用配置和基架Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="10d1c-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="10d1c-135">让我们看一下构建自动程序的主要组件：</span><span class="sxs-lookup"><span data-stu-id="10d1c-135">Let's look at the main components for building a bot:</span></span>

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="显示项目基架的屏幕截图Teams Toolkit。":::

<span data-ttu-id="10d1c-137">如果你在另一个教程中创建选项卡，则机器人的应用基架将有所不同。</span><span class="sxs-lookup"><span data-stu-id="10d1c-137">If you created a tab in another tutorial, the app scaffolding for the bot is different.</span></span> <span data-ttu-id="10d1c-138">与选项卡不同，机器人开发不需要你生成任何前端 Web 组件或使用 JavaScript Teams SDK。</span><span class="sxs-lookup"><span data-stu-id="10d1c-138">Unlike tabs, bot development doesn't require you to build any front-end web components or use the Teams JavaScript client SDK.</span></span>  <span data-ttu-id="10d1c-139">相反，基架使用[Microsoft Bot Framework](https://dev.botframework.com/)，这是一个开源 SDK，用于构建可在 Web、移动以及当然Teams！</span><span class="sxs-lookup"><span data-stu-id="10d1c-139">Instead, the scaffolding uses the [Microsoft Bot Framework](https://dev.botframework.com/), which is an open-source SDK for building intelligent, enterprise-grade bots that can work on the web, mobile, and of course Teams!</span></span> 

<span data-ttu-id="10d1c-140">该文件位于项目的根目录中，是Teams聊天机器人活动（如机器人如何响应特定消息）的 `botActivityHandler.js` 特定于 Teams 处理程序。</span><span class="sxs-lookup"><span data-stu-id="10d1c-140">The `botActivityHandler.js` file, located in the root directory of your project, is the Teams-specific handler that handles bot activities, such as how the bot responds to specific messages.</span></span> <span data-ttu-id="10d1c-141">应用基架提供位于项目根目录中的文件，是 Teams 特定处理程序，用于处理机器人活动，如机器人如何响应 `botActivityHandler.js` 特定消息。</span><span class="sxs-lookup"><span data-stu-id="10d1c-141">The app scaffolding provides a `botActivityHandler.js` file located in the root directory of your project, is the Teams specific handler that handles bot activities such as how the bot responds to specific messages.</span></span>

## <a name="3-securely-expose-your-localhost-to-the-internet"></a><span data-ttu-id="10d1c-142">3. 安全地将 localhost 公开到 Internet</span><span class="sxs-lookup"><span data-stu-id="10d1c-142">3. Securely expose your localhost to the internet</span></span>

<span data-ttu-id="10d1c-143">查看文件，该文件将创建 HTTP 服务器并处理路由，以侦听对机器人 `index.js` 的传入请求。</span><span class="sxs-lookup"><span data-stu-id="10d1c-143">Take a look at the `index.js` file, which creates an HTTP server and handles routing to listen for incoming requests to your bot.</span></span> <span data-ttu-id="10d1c-144">`/api/messages`是应用用于响应客户端请求的终结点 URL：</span><span class="sxs-lookup"><span data-stu-id="10d1c-144">The `/api/messages` is your app's endpoint URL to respond to client requests:</span></span> 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

<span data-ttu-id="10d1c-145">若要将请求转发到机器人的逻辑，必须设置一个可公开访问的 URL，例如 `https://example.com/api/messages` ，而不是 `https://localhost` 。</span><span class="sxs-lookup"><span data-stu-id="10d1c-145">To forward the requests to your bot's logic, you must set up a publicly accessible URL, such as `https://example.com/api/messages`, instead of `https://localhost`.</span></span> <span data-ttu-id="10d1c-146">由于你的应用当前正在从 localhost 运行，因此你必须 *对网络进行* 隧道传输。</span><span class="sxs-lookup"><span data-stu-id="10d1c-146">Because your app is running from your localhost currently, you must *tunnel* the network.</span></span>

<span data-ttu-id="10d1c-147">隧道是一种协议，允许你跨网络传输数据。</span><span class="sxs-lookup"><span data-stu-id="10d1c-147">Tunneling is a protocol that allows you to transport data across a network.</span></span> <span data-ttu-id="10d1c-148">localhost 隧道提供本地计算机和远程连接之间的连接。</span><span class="sxs-lookup"><span data-stu-id="10d1c-148">And localhost tunneling gives you a connection between your local machine and a remote connection.</span></span> <span data-ttu-id="10d1c-149">若要安全地将 localhost 公开到 Internet，建议使用名为 **ngrok** 的第三方工具。</span><span class="sxs-lookup"><span data-stu-id="10d1c-149">To securely expose your localhost to the internet, we recommend you to use the 3rd party tool called, **ngrok**.</span></span> <span data-ttu-id="10d1c-150">这将为您提供一个安全 URL。</span><span class="sxs-lookup"><span data-stu-id="10d1c-150">This will give you a secure URL.</span></span> 

1. <span data-ttu-id="10d1c-151">转到 ["ngrok.com](https://ngrok.com/download) 网站，并按照说明在您的环境中安装和设置 ngrok。</span><span class="sxs-lookup"><span data-stu-id="10d1c-151">Go to the [ngrok.com](https://ngrok.com/download) site and follow the instruction to install and set up ngrok in your environment.</span></span> 
    
    <span data-ttu-id="10d1c-152">将已安装的 ngrok.exe 文件的完整路径添加到系统 PATH 环境变量。</span><span class="sxs-lookup"><span data-stu-id="10d1c-152">Add the full path to the ngrok.exe file that you installed to the system PATH environment variable.</span></span> <span data-ttu-id="10d1c-153">具体步骤特定于您使用的命令行管理程序。</span><span class="sxs-lookup"><span data-stu-id="10d1c-153">The exact steps are specific to the shell that you are using.</span></span>

1.  <span data-ttu-id="10d1c-154">完成设置后，打开终端并运行 `ngrok http -host-header=rewrite 3978` 。</span><span class="sxs-lookup"><span data-stu-id="10d1c-154">After you have finished setting it up, open a terminal and run `ngrok http -host-header=rewrite 3978`.</span></span> 

    <span data-ttu-id="10d1c-155">现在 ngrok 提供了一个在端口 3978 上转发到 localhost 的公共安全 URL，因此请复制 HTTPS URL，如下面的屏幕截图所示，因为 `https://287a4f4223bc.ngrok.io` Teams 需要 HTTPS 连接：</span><span class="sxs-lookup"><span data-stu-id="10d1c-155">Now ngrok provides you a public, secure URL that forwards to your localhost at port 3978, so copy the HTTPS URL, for example, `https://287a4f4223bc.ngrok.io` as shown in the screenshot below, since Teams requires HTTPS connections:</span></span> 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="显示具有 ngrok 的 localhost 隧道的屏幕截图。":::

1. <span data-ttu-id="10d1c-157">在应用清单中注册 URL。</span><span class="sxs-lookup"><span data-stu-id="10d1c-157">Register the URL in your app manifest.</span></span> 

## <a name="4-register-your-bot-endpoint"></a><span data-ttu-id="10d1c-158">4. 注册自动程序终结点</span><span class="sxs-lookup"><span data-stu-id="10d1c-158">4. Register your bot endpoint</span></span>

<span data-ttu-id="10d1c-159">若要在 Azure Teams自动程序，必须使用 Azure Bot 服务注册它。</span><span class="sxs-lookup"><span data-stu-id="10d1c-159">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="10d1c-160">当你使用应用设置应用时，这会自动Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="10d1c-160">This is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="10d1c-161">仍必须指定终结点地址，以接收并处理用户消息或发送给机器人的请求。</span><span class="sxs-lookup"><span data-stu-id="10d1c-161">You must still specify an endpoint address to receive and process user messages, or requests sent to the bot.</span></span> <span data-ttu-id="10d1c-162">通常，URL 类似于 `https://HOST_URL/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="10d1c-162">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="10d1c-163">可以在工具包中对此进行配置。</span><span class="sxs-lookup"><span data-stu-id="10d1c-163">You can configure this in the toolkit.</span></span>

1. <span data-ttu-id="10d1c-164">在Visual Studio Code中，打开 **"Microsoft Teams Toolkit"。**</span><span class="sxs-lookup"><span data-stu-id="10d1c-164">In Visual Studio Code, open **Microsoft Teams Toolkit**.</span></span>
1. <span data-ttu-id="10d1c-165">选择 **"自动**  >  **程序""** 现有自动程序注册"，然后选择在安装期间创建的自动程序。</span><span class="sxs-lookup"><span data-stu-id="10d1c-165">Select **Bots** > **Existing bot registrations** and select the bot you created during setup.</span></span> 
1. <span data-ttu-id="10d1c-166">在 **"Bot 终结点地址** "字段中，输入 ngrok URL，例如 ，您将托管机器人并 `https://287a4f4223bc.ngrok.io` 附加到 `/api/messages` 其中：</span><span class="sxs-lookup"><span data-stu-id="10d1c-166">In the **Bot endpoint address** field, enter the ngrok URL, for example, `https://287a4f4223bc.ngrok.io`, where you're hosting the bot and append `/api/messages` to it:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="显示如何使用 ngrok 隧道 localhost 的屏幕截图。":::

    <span data-ttu-id="10d1c-168">正确设置终结点后，自动程序Teams响应邮件。</span><span class="sxs-lookup"><span data-stu-id="10d1c-168">Your bot will be able to respond to messages in Teams, after you set up the endpoint correctly.</span></span> 

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="10d1c-169">5. 生成并运行应用</span><span class="sxs-lookup"><span data-stu-id="10d1c-169">5. Build and run your app</span></span>

<span data-ttu-id="10d1c-170">你已设置 URL 以托管自动程序，并配置为处理消息。</span><span class="sxs-lookup"><span data-stu-id="10d1c-170">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="10d1c-171">可以启动并运行应用了。</span><span class="sxs-lookup"><span data-stu-id="10d1c-171">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="10d1c-172">在终端中，转到应用项目的根目录并运行 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="10d1c-172">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="10d1c-173">运行 `npm start`。</span><span class="sxs-lookup"><span data-stu-id="10d1c-173">Run `npm start`.</span></span>

   <span data-ttu-id="10d1c-174">如果成功，你将看到以下消息，指示机器人正在侦听你的活动 `localhost` ：</span><span class="sxs-lookup"><span data-stu-id="10d1c-174">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="10d1c-175">6. 将自动程序旁加载Teams</span><span class="sxs-lookup"><span data-stu-id="10d1c-175">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="10d1c-176">运行自动程序后，你可以将其安装在Teams。</span><span class="sxs-lookup"><span data-stu-id="10d1c-176">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="10d1c-177">如果你之前未旁加载Teams并遇到问题，请按照以下[说明操作](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="10d1c-177">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="10d1c-178">在Visual Studio Code中，选择 **F5** 键以启动 Teams Web 客户端。</span><span class="sxs-lookup"><span data-stu-id="10d1c-178">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="10d1c-179">在应用安装对话框中，选择 **"为我添加"。**</span><span class="sxs-lookup"><span data-stu-id="10d1c-179">In the app install dialog, select **Add for me**.</span></span> 

   > [!Note]
   > <span data-ttu-id="10d1c-180">默认情况下，应用将添加到你的一对一直接聊天消息中，但是你可以选择将其安装到团队或聊天，方法是单击"为我添加"旁边的小 **箭头**。</span><span class="sxs-lookup"><span data-stu-id="10d1c-180">By default, the app is added to your 1:1 direct chat message, however you can choose to install it to a team or chat by clicking the little arrow beside **Add for me**.</span></span> <span data-ttu-id="10d1c-181">在本教程中，我们只需单击"添加"。</span><span class="sxs-lookup"><span data-stu-id="10d1c-181">In this tutorial, let’s just click Add.</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="显示使用 ngrok 的隧道 localhost 的屏幕截图。":::

## <a name="7-test-your-bot"></a><span data-ttu-id="10d1c-183">7. 测试机器人</span><span class="sxs-lookup"><span data-stu-id="10d1c-183">7. Test your bot</span></span>

<span data-ttu-id="10d1c-184">让我们对机器人说"Hello"。</span><span class="sxs-lookup"><span data-stu-id="10d1c-184">Let's say "Hello" to your bot.</span></span>

* <span data-ttu-id="10d1c-185">在撰写框中，发送邮件 `Hello` 。</span><span class="sxs-lookup"><span data-stu-id="10d1c-185">In the compose box, send a `Hello` message.</span></span>
    <span data-ttu-id="10d1c-186">自动程序使用类似以下消息的回复：</span><span class="sxs-lookup"><span data-stu-id="10d1c-186">Your bot replies with something like the following message:</span></span>

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="显示用户向自动程序Teams&quot;Hello&quot;并收到响应的屏幕截图。":::

    <span data-ttu-id="10d1c-188">现在，你已创建一Teams聊天机器人，该机器人可以与用户一对一进行通信，或在组设置中 (频道和聊天) 🎉。</span><span class="sxs-lookup"><span data-stu-id="10d1c-188">You have now created a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats) 🎉.</span></span>

## <a name="troubleshoot-your-bot"></a><span data-ttu-id="10d1c-189">自动程序疑难解答</span><span class="sxs-lookup"><span data-stu-id="10d1c-189">Troubleshoot your bot</span></span>

<span data-ttu-id="10d1c-190">如果你在完成本教程时有问题，以下信息可能会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="10d1c-190">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="10d1c-191">自动程序未连接到Teams</span><span class="sxs-lookup"><span data-stu-id="10d1c-191">Bot isn't connected to Teams</span></span>


<span data-ttu-id="10d1c-192">如果你安装了应用，但自动程序无法工作，请确保自动程序已连接到 Azure 自动程序服务Teams [*频道*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="10d1c-192">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="10d1c-193">了解这一点与 Teams 中的频道Teams。</span><span class="sxs-lookup"><span data-stu-id="10d1c-193">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="10d1c-194">在这种情况下，通道是 Azure 自动程序服务如何将机器人连接到Teams受支持的 Microsoft 或第三方[通信应用](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="10d1c-194">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="10d1c-195">另请参阅</span><span class="sxs-lookup"><span data-stu-id="10d1c-195">See also</span></span>

* [<span data-ttu-id="10d1c-196">Bot 基础知识</span><span class="sxs-lookup"><span data-stu-id="10d1c-196">Bot basics</span></span>](../bots/bot-basics.md)
* [<span data-ttu-id="10d1c-197">为用户生成个人Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="10d1c-197">Build a personal tab for Microsoft Teams</span></span>](../build-your-first-app/build-personal-tab.md)
* [<span data-ttu-id="10d1c-198">查看其他Teams机器人可以使用我们的示例之一执行哪些功能</span><span class="sxs-lookup"><span data-stu-id="10d1c-198">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="10d1c-199">自动程序对话基础知识</span><span class="sxs-lookup"><span data-stu-id="10d1c-199">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="10d1c-200">设计准则</span><span class="sxs-lookup"><span data-stu-id="10d1c-200">Design guidelines</span></span>](../bots/design/bots.md) 
* [<span data-ttu-id="10d1c-201">生产就绪 UI 模板</span><span class="sxs-lookup"><span data-stu-id="10d1c-201">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md)
* [<span data-ttu-id="10d1c-202">自动程序身份验证Teams</span><span class="sxs-lookup"><span data-stu-id="10d1c-202">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="10d1c-203">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="10d1c-203">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="10d1c-204">创建没有工具包的自动程序</span><span class="sxs-lookup"><span data-stu-id="10d1c-204">Create a bot without the toolkit</span></span>](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a><span data-ttu-id="10d1c-205">后续步骤</span><span class="sxs-lookup"><span data-stu-id="10d1c-205">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="10d1c-206">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="10d1c-206">Build a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)
