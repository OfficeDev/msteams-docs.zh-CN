---
title: 入门 - 生成邮件扩展
author: girliemac
description: 使用 Microsoft Teams 快速创建邮件Microsoft Teams Toolkit。
ms.author: timura
ms.date: 03/25/2021
ms.topic: tutorial
ms.openlocfilehash: 91a5a15697163ee9103607511047a6411a5acf1a
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068757"
---
# <a name="build-your-first-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="a47dd-103">生成首个邮件扩展Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="a47dd-103">Build your first messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="a47dd-104">邮件扩展有两Teams：[搜索命令](../messaging-extensions/how-to/search-commands/define-search-command.md)[和操作命令](../messaging-extensions/how-to/action-commands/define-action-command.md)。 </span><span class="sxs-lookup"><span data-stu-id="a47dd-104">There are two types of Teams *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="a47dd-105">本教程指导你创建搜索命令 (也称为基于搜索的邮件扩展 *) ，* 它是查找外部内容并共享外部内容的快捷方式Teams。</span><span class="sxs-lookup"><span data-stu-id="a47dd-105">This tutorial teaches you to create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="a47dd-106">用户可以从"撰写"或Teams访问搜索命令。</span><span class="sxs-lookup"><span data-stu-id="a47dd-106">Users can access search commands from the Teams compose or command box.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="a47dd-107">您将了解哪些功能</span><span class="sxs-lookup"><span data-stu-id="a47dd-107">What you'll learn</span></span>

* <span data-ttu-id="a47dd-108">使用 Microsoft Teams Toolkit for Visual Studio Code 创建应用项目和消息传递扩展Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="a47dd-108">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code.</span></span>
* <span data-ttu-id="a47dd-109">了解与邮件扩展相关的应用配置和基架。</span><span class="sxs-lookup"><span data-stu-id="a47dd-109">Understand the app configurations and the scaffolding relevant to messaging extensions.</span></span>
* <span data-ttu-id="a47dd-110">在本地托管应用。</span><span class="sxs-lookup"><span data-stu-id="a47dd-110">Host an app locally.</span></span>
* <span data-ttu-id="a47dd-111">为邮件扩展配置自动程序。</span><span class="sxs-lookup"><span data-stu-id="a47dd-111">Configure the bot for your messaging extension.</span></span>
* <span data-ttu-id="a47dd-112">旁加载和测试邮件扩展Teams。</span><span class="sxs-lookup"><span data-stu-id="a47dd-112">Sideload and test a messaging extension in Teams.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="a47dd-113">必备条件</span><span class="sxs-lookup"><span data-stu-id="a47dd-113">Prerequisites</span></span>

<span data-ttu-id="a47dd-114">确保你了解如何设置和构建简单的Teams应用程序。</span><span class="sxs-lookup"><span data-stu-id="a47dd-114">Make sure that you understand how to set up and build a simple Teams app.</span></span> <span data-ttu-id="a47dd-115">有关详细信息，请参阅创建[你的第一个Microsoft Teams Hello， World！"应用](../build-your-first-app/build-and-run.md)。</span><span class="sxs-lookup"><span data-stu-id="a47dd-115">For more information, see [create your first Microsoft Teams "Hello, World!" app](../build-your-first-app/build-and-run.md).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="a47dd-116">1. 创建应用项目</span><span class="sxs-lookup"><span data-stu-id="a47dd-116">1. Create your app project</span></span>

<span data-ttu-id="a47dd-117">下表Microsoft Teams Toolkit设置邮件扩展的以下组件：</span><span class="sxs-lookup"><span data-stu-id="a47dd-117">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="a47dd-118">**与邮件扩展相关的** 应用配置和基架</span><span class="sxs-lookup"><span data-stu-id="a47dd-118">**App configurations and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="a47dd-119">**自动** 程序用于自动注册到自动聊天机器人服务Microsoft Azure聊天扩展</span><span class="sxs-lookup"><span data-stu-id="a47dd-119">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

<span data-ttu-id="a47dd-120">**创建应用项目**</span><span class="sxs-lookup"><span data-stu-id="a47dd-120">**To create your app project**</span></span>

1. In Visual Studio Code， select **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: on the left Activity Bar and choose Create a new **Teams app**.
1. <span data-ttu-id="a47dd-122">当系统提示时，使用你的 Microsoft 365帐户登录。</span><span class="sxs-lookup"><span data-stu-id="a47dd-122">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="a47dd-123">在"**选择项目"屏幕上的**"**消息传递扩展搜索**"  >  **中**，单击 **"JS (JavaScript) "。**</span><span class="sxs-lookup"><span data-stu-id="a47dd-123">On the **Select project** screen, at **Messaging Extensions** > **Search**, click **JS (JavaScript)**.</span></span> 
1. <span data-ttu-id="a47dd-124">输入你的应用Teams名称。</span><span class="sxs-lookup"><span data-stu-id="a47dd-124">Enter a name for your Teams app.</span></span> <span data-ttu-id="a47dd-125">这是应用的默认名称，也是本地计算机上应用项目目录的名称。</span><span class="sxs-lookup"><span data-stu-id="a47dd-125">This is the default name for your app and also the name of the app project directory on your local machine.</span></span>
1. <span data-ttu-id="a47dd-126">选择 **"创建新自动程序"，** 然后单击 **"创建自动程序注册"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="a47dd-126">Select **Create a new Bot** then click **Create Bot Registration** button.</span></span> <span data-ttu-id="a47dd-127">如果成功，你的新自动程序将具有 *"已注册"* 状态。</span><span class="sxs-lookup"><span data-stu-id="a47dd-127">If successful, your new bot will have a *Registered* status.</span></span> <span data-ttu-id="a47dd-128">现在，自动程序将自动注册到 Microsoft Azure Bot Service。</span><span class="sxs-lookup"><span data-stu-id="a47dd-128">Now your bot is automatically registered with the Microsoft Azure Bot Service.</span></span> 
1. <span data-ttu-id="a47dd-129">选择 **屏幕** 底部的"完成"以配置项目，并在本地计算机上保存项目。</span><span class="sxs-lookup"><span data-stu-id="a47dd-129">Select **Finish** at the bottom of the screen to configure your project and save your project on your local machine.</span></span>

## <a name="2-understand-your-app-project-components"></a><span data-ttu-id="a47dd-130">2. 了解应用项目组件</span><span class="sxs-lookup"><span data-stu-id="a47dd-130">2. Understand your app project components</span></span>

<span data-ttu-id="a47dd-131">使用应用程序配置和基架创建项目时，许多应用配置和基架Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="a47dd-131">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

* <span data-ttu-id="a47dd-132">应用配置：若要查看或更新邮件扩展的配置，请在工具包中选择 App **Studio，** 然后转到消息传递 **扩展**。</span><span class="sxs-lookup"><span data-stu-id="a47dd-132">App configurations: To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>
* <span data-ttu-id="a47dd-133">应用基架：应用基架提供位于项目根目录中的文件，用于处理邮件扩展 (或技术上邮件扩展的自动程序) 如何响应 Teams 中的搜索 `botActivityHandler.js` 查询[](#4-configure-the-bot-for-your-messaging-extension)。</span><span class="sxs-lookup"><span data-stu-id="a47dd-133">App scaffolding: The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="a47dd-134">3. 设置应用的安全隧道</span><span class="sxs-lookup"><span data-stu-id="a47dd-134">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="a47dd-135">出于测试目的，让我们在端口 3978 (本地 Web 服务器上托管邮件) 。</span><span class="sxs-lookup"><span data-stu-id="a47dd-135">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span> <span data-ttu-id="a47dd-136">您将使用 [ngrok](https://ngrok.com/download) 设置到 localhost 的安全隧道。</span><span class="sxs-lookup"><span data-stu-id="a47dd-136">You are going to use [ngrok](https://ngrok.com/download) to set up a secure tunnel to localhost.</span></span> <span data-ttu-id="a47dd-137">有关详细信息[，请参阅生成第一Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet)聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="a47dd-137">See [build your first bot for Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet) for details.</span></span> 

1. <span data-ttu-id="a47dd-138">如果尚未安装，请安装 [ngrok](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="a47dd-138">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="a47dd-139">在终端中，运行 `ngrok http -host-header=rewrite 3978` 。</span><span class="sxs-lookup"><span data-stu-id="a47dd-139">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="a47dd-140">复制输出链接中的 HTTPS URL，例如 (，) `https://468b9ab725e9.ngrok.io` HTTPS Teams HTTPS 连接。</span><span class="sxs-lookup"><span data-stu-id="a47dd-140">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

   <span data-ttu-id="a47dd-141">通过此 URL，Teams (需要 HTTPS) 的应用程序将能够隧道连接到你在 `localhost` 端口 3978 (托管应用) 。</span><span class="sxs-lookup"><span data-stu-id="a47dd-141">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="a47dd-142">4. 为邮件扩展配置自动程序</span><span class="sxs-lookup"><span data-stu-id="a47dd-142">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="a47dd-143">邮件扩展依赖机器人将用户请求从 Teams发送到托管服务。</span><span class="sxs-lookup"><span data-stu-id="a47dd-143">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="a47dd-144">自动程序必须在 Azure Bot 服务中注册，该服务是在使用 Azure 自动程序服务设置应用Teams Toolkit。</span><span class="sxs-lookup"><span data-stu-id="a47dd-144">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="a47dd-145">您仍必须指定自动程序终结点 URL 以接收并处理邮件扩展中的搜索查询。</span><span class="sxs-lookup"><span data-stu-id="a47dd-145">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="a47dd-146">通常，URL 类似于 `https://HOST_URL/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="a47dd-146">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="a47dd-147">可以在工具包中快速进行配置。</span><span class="sxs-lookup"><span data-stu-id="a47dd-147">You can configure this quickly in the toolkit.</span></span>

1. In Visual Studio Code， select **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: on the left Activity Bar and choose Open **Microsoft Teams Toolkit**.
1. <span data-ttu-id="a47dd-149">转到自动 **程序>现有自动程序注册并选择** 你在安装期间创建的自动程序。</span><span class="sxs-lookup"><span data-stu-id="a47dd-149">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="a47dd-150">在 **"自动程序终结点** 地址"字段中，输入 ngrok URL (例如，) 托管自动程序并追加到其中 `https://468b9ab725e9.ngrok.io` `/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="a47dd-150">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

   <span data-ttu-id="a47dd-151">自动程序将能够处理邮件扩展中的查询。</span><span class="sxs-lookup"><span data-stu-id="a47dd-151">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="a47dd-152">5. 生成并运行应用</span><span class="sxs-lookup"><span data-stu-id="a47dd-152">5. Build and run your app</span></span>

<span data-ttu-id="a47dd-153">你已设置用于托管邮件扩展的 URL，并配置为处理搜索。</span><span class="sxs-lookup"><span data-stu-id="a47dd-153">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="a47dd-154">可以启动并运行应用了。</span><span class="sxs-lookup"><span data-stu-id="a47dd-154">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="a47dd-155">打开终端并转到应用项目的根目录</span><span class="sxs-lookup"><span data-stu-id="a47dd-155">Open terminal and go to the root directory of your app project</span></span>
1. <span data-ttu-id="a47dd-156">运行 `npm install`。</span><span class="sxs-lookup"><span data-stu-id="a47dd-156">Run `npm install`.</span></span>
1. <span data-ttu-id="a47dd-157">运行 `npm start`。</span><span class="sxs-lookup"><span data-stu-id="a47dd-157">Run `npm start`.</span></span>

   <span data-ttu-id="a47dd-158">如果成功，你将看到以下消息，指示邮件扩展服务正在侦听你的活动 `localhost` ：</span><span class="sxs-lookup"><span data-stu-id="a47dd-158">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="a47dd-159">6. 在客户端中旁加载Teams</span><span class="sxs-lookup"><span data-stu-id="a47dd-159">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="a47dd-160">在邮件扩展运行时，你可以将其安装在Teams。</span><span class="sxs-lookup"><span data-stu-id="a47dd-160">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="a47dd-161">如果你之前未旁加载Teams并遇到问题，请按照以下[说明操作](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="a47dd-161">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="a47dd-162">在Visual Studio Code中，选择 **F5** 键以启动 Teams Web 客户端。</span><span class="sxs-lookup"><span data-stu-id="a47dd-162">In Visual Studio Code, select the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="a47dd-163">在应用安装对话框中，选择 **"为我添加"。**</span><span class="sxs-lookup"><span data-stu-id="a47dd-163">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="a47dd-164">7. 测试邮件扩展</span><span class="sxs-lookup"><span data-stu-id="a47dd-164">7. Test your messaging extension</span></span>

<span data-ttu-id="a47dd-165">了解消息传递扩展在聊天Teams工作。</span><span class="sxs-lookup"><span data-stu-id="a47dd-165">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="a47dd-166">启动新聊天。</span><span class="sxs-lookup"><span data-stu-id="a47dd-166">Start a new chat.</span></span> 在撰写框中，选择 **"更多** :::image type="icon" source="../assets/icons/teams-client-more.png"::: "并选择你刚刚旁加载的邮件扩展应用。
1. <span data-ttu-id="a47dd-168">尝试搜索某些内容 (例如 **，Tickets**) 。</span><span class="sxs-lookup"><span data-stu-id="a47dd-168">Try searching for something (for example, **Tickets**).</span></span> <span data-ttu-id="a47dd-169">如果你的应用正常工作，你将看到示例搜索结果 (你可以稍后添加自己的) 。</span><span class="sxs-lookup"><span data-stu-id="a47dd-169">If your app is working, you'll see sample search results (you can add your own later).</span></span>

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Screenshot showing how a search-based messaging extension is used in the Teams compose box.":::

## <a name="troubleshooting"></a><span data-ttu-id="a47dd-171">疑难解答</span><span class="sxs-lookup"><span data-stu-id="a47dd-171">Troubleshooting</span></span>

<span data-ttu-id="a47dd-172">如果你在完成本教程时有问题，以下信息可能会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="a47dd-172">The following information may help if you had issues completing this tutorial.</span></span>

<span data-ttu-id="a47dd-173">**自动程序未连接到Teams**</span><span class="sxs-lookup"><span data-stu-id="a47dd-173">**Bot isn't connected to Teams**</span></span>

<span data-ttu-id="a47dd-174">如果你安装了应用，但它无法工作，请确保消息扩展的自动程序已连接到 Azure 自动程序服务的 Teams [*通道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="a47dd-174">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="a47dd-175">了解这一点与 Teams 中的频道Teams。</span><span class="sxs-lookup"><span data-stu-id="a47dd-175">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="a47dd-176">在这种情况下，通道是 Azure 自动程序服务如何将机器人连接到Teams受支持的 Microsoft 或第三方[通信应用](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="a47dd-176">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="see-also"></a><span data-ttu-id="a47dd-177">另请参阅</span><span class="sxs-lookup"><span data-stu-id="a47dd-177">See also</span></span>

* [<span data-ttu-id="a47dd-178">Teams撰写或命令框</span><span class="sxs-lookup"><span data-stu-id="a47dd-178">Teams compose or command box</span></span>](../messaging-extensions/what-are-messaging-extensions.md) 
* [<span data-ttu-id="a47dd-179">包含链接展开功能</span><span class="sxs-lookup"><span data-stu-id="a47dd-179">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="a47dd-180">设计准则</span><span class="sxs-lookup"><span data-stu-id="a47dd-180">Design guidelines</span></span>](../messaging-extensions/design/messaging-extension-design.md) 
* [<span data-ttu-id="a47dd-181">生产就绪 UI 模板</span><span class="sxs-lookup"><span data-stu-id="a47dd-181">Production-ready UI templates</span></span>](../concepts/design/design-teams-app-ui-templates.md) 
* [<span data-ttu-id="a47dd-182">添加身份验证</span><span class="sxs-lookup"><span data-stu-id="a47dd-182">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="a47dd-183">创建基于操作的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="a47dd-183">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="a47dd-184">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="a47dd-184">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)

## <a name="next-steps"></a><span data-ttu-id="a47dd-185">后续步骤</span><span class="sxs-lookup"><span data-stu-id="a47dd-185">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a47dd-186">定义搜索命令</span><span class="sxs-lookup"><span data-stu-id="a47dd-186">Define search commands</span></span>](../messaging-extensions/how-to/search-commands/define-search-command.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="a47dd-187">响应用户的搜索</span><span class="sxs-lookup"><span data-stu-id="a47dd-187">Respond to users' searches</span></span>](../messaging-extensions/how-to/search-commands/respond-to-search.md)