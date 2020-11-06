---
title: 入门-构建机器人
author: heath-hamilton
description: 使用 Microsoft 团队工具包快速创建 Microsoft 团队 bot。
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 1229064ac6b7aab73c50048f0764c6a2353ab54a
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931735"
---
# <a name="build-a-bot-for-microsoft-teams"></a><span data-ttu-id="2c86e-103">为 Microsoft 团队构建机器人</span><span class="sxs-lookup"><span data-stu-id="2c86e-103">Build a bot for Microsoft Teams</span></span>

<span data-ttu-id="2c86e-104">您将在本教程中构建基本 *机器人* 应用程序。</span><span class="sxs-lookup"><span data-stu-id="2c86e-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="2c86e-105">Bot 充当团队用户与 web 服务之间的媒介。</span><span class="sxs-lookup"><span data-stu-id="2c86e-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="2c86e-106">用户可以与机器人聊天以快速获取信息或启动服务执行的工作流和任务。</span><span class="sxs-lookup"><span data-stu-id="2c86e-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="2c86e-107">您的分配</span><span class="sxs-lookup"><span data-stu-id="2c86e-107">Your assignment</span></span>

<span data-ttu-id="2c86e-108">你的工作区创建了一个使用 [选项卡](../build-your-first-app/build-personal-tab.md) 来呈现重要联系人信息的团队应用。</span><span class="sxs-lookup"><span data-stu-id="2c86e-108">Your workplace created a Teams app that uses [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information.</span></span> <span data-ttu-id="2c86e-109">例如，同事可以快速访问技术支持电话号码。</span><span class="sxs-lookup"><span data-stu-id="2c86e-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="2c86e-110">而不是打电话，如果用户可以使用 chatbot 联系技术支持，该怎么办？</span><span class="sxs-lookup"><span data-stu-id="2c86e-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="2c86e-111">你的老板要求你查看如何快速启动并在团队中运行基本的会话机器人。</span><span class="sxs-lookup"><span data-stu-id="2c86e-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="2c86e-112">你将了解的内容</span><span class="sxs-lookup"><span data-stu-id="2c86e-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="2c86e-113">使用 Microsoft 团队工具包为 Visual Studio Code 创建一个应用程序项目和机器人</span><span class="sxs-lookup"><span data-stu-id="2c86e-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="2c86e-114">确定与 bot 相关的一些应用配置和基架</span><span class="sxs-lookup"><span data-stu-id="2c86e-114">Identify some of the app configurations and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="2c86e-115">在本地托管应用程序</span><span class="sxs-lookup"><span data-stu-id="2c86e-115">Host an app locally</span></span>
> * <span data-ttu-id="2c86e-116">为团队配置机器人</span><span class="sxs-lookup"><span data-stu-id="2c86e-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="2c86e-117">旁加载和测试团队中的 bot</span><span class="sxs-lookup"><span data-stu-id="2c86e-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="2c86e-118">准备工作</span><span class="sxs-lookup"><span data-stu-id="2c86e-118">Before you begin</span></span>

<span data-ttu-id="2c86e-119">如果还没有，请确保 [了解并安装团队开发先决条件](build-first-app-overview.md#get-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="2c86e-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="2c86e-120">1. 创建您的应用程序项目</span><span class="sxs-lookup"><span data-stu-id="2c86e-120">1. Create your app project</span></span>

<span data-ttu-id="2c86e-121">Microsoft 团队工具包可帮助您为您的应用程序设置以下组件：</span><span class="sxs-lookup"><span data-stu-id="2c86e-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="2c86e-122">与 bot 相关的 **应用程序配置和基架**</span><span class="sxs-lookup"><span data-stu-id="2c86e-122">**App configurations and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="2c86e-123">自动注册到 Microsoft Azure Bot 服务的 **Bot**</span><span class="sxs-lookup"><span data-stu-id="2c86e-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="2c86e-124">如果之前尚未创建团队应用程序项目，您可能会发现，请按照 [以下说明](../build-your-first-app/build-and-run.md) 更详细地说明项目。</span><span class="sxs-lookup"><span data-stu-id="2c86e-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队** "， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用** "。
1. <span data-ttu-id="2c86e-126">出现提示时，使用 Microsoft 365 开发帐户登录。</span><span class="sxs-lookup"><span data-stu-id="2c86e-126">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="2c86e-127">在 " **添加功能** " 屏幕上，依次选择 **Bot** 和 " **下一步** "。</span><span class="sxs-lookup"><span data-stu-id="2c86e-127">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="2c86e-128">为你的团队应用输入名称。</span><span class="sxs-lookup"><span data-stu-id="2c86e-128">Enter a name for your Teams app.</span></span> <span data-ttu-id="2c86e-129"> (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) </span><span class="sxs-lookup"><span data-stu-id="2c86e-129">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="2c86e-130">转到 " **配置 bot** "，选择 " **创建新的 bot** "，然后 **创建 bot 注册** 。</span><span class="sxs-lookup"><span data-stu-id="2c86e-130">Go to **Configure bot** and select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="2c86e-131">如果成功，新的 bot 将具有 **已注册** 状态。</span><span class="sxs-lookup"><span data-stu-id="2c86e-131">If successful, your new bot will have a **Registered** status.</span></span>
1. <span data-ttu-id="2c86e-132">选择屏幕底部的 " **完成** "，然后选择要创建项目的位置。</span><span class="sxs-lookup"><span data-stu-id="2c86e-132">Select **Finish** at the bottom of the screen and choose a location to create your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="2c86e-133">2. 确定相关的应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="2c86e-133">2. Identify relevant app project components</span></span>

<span data-ttu-id="2c86e-134">大部分应用配置和基架是在使用团队工具包创建项目时自动设置的。</span><span class="sxs-lookup"><span data-stu-id="2c86e-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="2c86e-135">我们来看看构建机器人的主要组件。</span><span class="sxs-lookup"><span data-stu-id="2c86e-135">Let's look at the main components for building a bot.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="2c86e-136">应用配置</span><span class="sxs-lookup"><span data-stu-id="2c86e-136">App configurations</span></span>

<span data-ttu-id="2c86e-137">若要查看或更新你的 bot 的配置，请在工具包中选择 **应用程序 Studio** 并转到 " **bot** "。</span><span class="sxs-lookup"><span data-stu-id="2c86e-137">To view or update your bot's configurations, select **App Studio** in the toolkit and go to **Bots**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="2c86e-138">应用程序基架</span><span class="sxs-lookup"><span data-stu-id="2c86e-138">App scaffolding</span></span>

<span data-ttu-id="2c86e-139">应用程序基架提供一个 `botActivityHandler.js` 文件，该文件位于项目的根目录中，用于处理你的 bot 如何处理团队中的活动 (例如，bot 如何对特定邮件（如 "Hello" ) ）进行响应。</span><span class="sxs-lookup"><span data-stu-id="2c86e-139">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="2c86e-140">3. 设置应用程序的安全隧道</span><span class="sxs-lookup"><span data-stu-id="2c86e-140">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="2c86e-141">出于测试目的，让您在本地 web 服务器上托管您的应用程序， (端口 3978) 。</span><span class="sxs-lookup"><span data-stu-id="2c86e-141">For testing purposes, let's host your app on a local web server (port 3978).</span></span>

1. <span data-ttu-id="2c86e-142">如果还未安装，请安装 [ngrok](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="2c86e-142">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="2c86e-143">在终端中，运行 `ngrok http -host-header=rewrite 3978` 。</span><span class="sxs-lookup"><span data-stu-id="2c86e-143">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="2c86e-144">在输出中复制 HTTPS URL (例如， `https://468b9ab725e9.ngrok.io`) 自团队需要 HTTPS 连接。</span><span class="sxs-lookup"><span data-stu-id="2c86e-144">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="2c86e-145">使用此 URL 时，需要 HTTPS 连接) 的团队 (可以通过 `localhost` 端口 3978) 上的 (承载应用程序的位置进行隧道连接。</span><span class="sxs-lookup"><span data-stu-id="2c86e-145">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="2c86e-146">4. 配置你的 bot</span><span class="sxs-lookup"><span data-stu-id="2c86e-146">4. Configure your bot</span></span>

<span data-ttu-id="2c86e-147">若要在团队中使用 bot，必须将其注册到 Azure Bot 服务。</span><span class="sxs-lookup"><span data-stu-id="2c86e-147">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="2c86e-148">幸运的是，当您使用团队工具包设置应用程序时，将自动完成此操作。</span><span class="sxs-lookup"><span data-stu-id="2c86e-148">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="2c86e-149">您仍必须指定接收和处理用户邮件的终结点地址 (例如，发送到 bot 的请求) 。</span><span class="sxs-lookup"><span data-stu-id="2c86e-149">You still must specify an endpoint address to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="2c86e-150">通常，URL 如下所示 `https://HOST_URL/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="2c86e-150">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="2c86e-151">您可以在工具包中快速配置此设置。</span><span class="sxs-lookup"><span data-stu-id="2c86e-151">You can configure this quickly in the toolkit.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队** "， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **打开 Microsoft 团队工具包** "。
1. <span data-ttu-id="2c86e-153">转到 " **bot" > 现有的 bot 注册** ，并选择您在安装过程中创建的 bot。</span><span class="sxs-lookup"><span data-stu-id="2c86e-153">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="2c86e-154">在 " **Bot 终结点地址** " 字段中，输入 ngrok URL (例如， `https://468b9ab725e9.ngrok.io`) 您在其中承载机器人并追加 `/api/messages` 到它的位置。</span><span class="sxs-lookup"><span data-stu-id="2c86e-154">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span><br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="图中显示可在团队工具包中配置 bot 终结点 URL 的位置。":::

<span data-ttu-id="2c86e-156">你的 bot 将能够响应团队中的邮件。</span><span class="sxs-lookup"><span data-stu-id="2c86e-156">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="2c86e-157">5. 生成并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="2c86e-157">5. Build and run your app</span></span>

<span data-ttu-id="2c86e-158">您已经设置了承载你的 bot 并将其配置为处理邮件的 URL。</span><span class="sxs-lookup"><span data-stu-id="2c86e-158">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="2c86e-159">现在就可以启动并运行您的应用程序了。</span><span class="sxs-lookup"><span data-stu-id="2c86e-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="2c86e-160">在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="2c86e-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="2c86e-161">运行 `npm start` 。</span><span class="sxs-lookup"><span data-stu-id="2c86e-161">Run `npm start`.</span></span>

<span data-ttu-id="2c86e-162">如果成功，你将看到以下消息，指示你的 bot 正在侦听你的活动 `localhost` ：</span><span class="sxs-lookup"><span data-stu-id="2c86e-162">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="2c86e-163">6. 在团队中旁加载你的机器人</span><span class="sxs-lookup"><span data-stu-id="2c86e-163">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="2c86e-164">在运行机器人的情况下，可以将其安装在团队中。</span><span class="sxs-lookup"><span data-stu-id="2c86e-164">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="2c86e-165">如果您在之前未旁加载团队应用程序并遇到问题，请按照这些 [说明](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)进行操作。</span><span class="sxs-lookup"><span data-stu-id="2c86e-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="2c86e-166">在 Visual Studio Code 中，按 **F5** 键以启动团队 web 客户端。</span><span class="sxs-lookup"><span data-stu-id="2c86e-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="2c86e-167">在 "应用程序安装" 对话框中，选择 " **为我添加** "。</span><span class="sxs-lookup"><span data-stu-id="2c86e-167">In the app install dialog, select **Add for me**.</span></span> <span data-ttu-id="2c86e-168"> (你可以将机器人添加到频道或聊天，但对其他人来说，在一对一聊天中测试 bot 的干扰较差。 ) </span><span class="sxs-lookup"><span data-stu-id="2c86e-168">(You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="2c86e-169">7. 测试你的 bot</span><span class="sxs-lookup"><span data-stu-id="2c86e-169">7. Test your bot</span></span>

<span data-ttu-id="2c86e-170">现在，为有趣部分：让我们将 "Hello" 告诉你的机器人。</span><span class="sxs-lookup"><span data-stu-id="2c86e-170">Now for the fun part: Let's say "Hello" to your bot.</span></span>

1. <span data-ttu-id="2c86e-171">在 "撰写" 框中，发送一 `Hello` 封邮件。</span><span class="sxs-lookup"><span data-stu-id="2c86e-171">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="2c86e-172">你的 bot 将回复如下邮件等内容。</span><span class="sxs-lookup"><span data-stu-id="2c86e-172">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="显示用户将 _OL_QUOTE_PLACEHOLDER_Hello_OL_QUOTE_PLACEHOLDER_ 告诉团队 bot 并收到响应的屏幕截图。":::

## <a name="well-done"></a><span data-ttu-id="2c86e-174">干的好</span><span class="sxs-lookup"><span data-stu-id="2c86e-174">Well done</span></span>

<span data-ttu-id="2c86e-175">祝贺你！</span><span class="sxs-lookup"><span data-stu-id="2c86e-175">Congratulations!</span></span> <span data-ttu-id="2c86e-176">您有一个基本的团队 bot，可以与用户一次或在组设置 (频道和聊天) 通信。</span><span class="sxs-lookup"><span data-stu-id="2c86e-176">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="2c86e-177">故障排除</span><span class="sxs-lookup"><span data-stu-id="2c86e-177">Troubleshooting</span></span>

<span data-ttu-id="2c86e-178">如果你在完成本教程时遇到问题，以下信息可能会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="2c86e-178">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="2c86e-179">机器人未连接到团队</span><span class="sxs-lookup"><span data-stu-id="2c86e-179">Bot isn't connected to Teams</span></span>

<span data-ttu-id="2c86e-180">如果您安装了应用程序，但机器人无法正常运行，请确保将 bot [连接到 Azure Bot 服务的团队 *频道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="2c86e-180">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="2c86e-181">请务必了解，这与团队中的频道不相同。</span><span class="sxs-lookup"><span data-stu-id="2c86e-181">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="2c86e-182">在这种情况下，通道是 Azure Bot 服务将你的 Bot 连接到团队或其他 [受支持的 Microsoft 或第三方通信应用程序](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)的方式。</span><span class="sxs-lookup"><span data-stu-id="2c86e-182">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="2c86e-183">了解更多</span><span class="sxs-lookup"><span data-stu-id="2c86e-183">Learn more</span></span>

* [<span data-ttu-id="2c86e-184">请参阅使用我们的示例之一可以执行的其他团队 bot</span><span class="sxs-lookup"><span data-stu-id="2c86e-184">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="2c86e-185">自动程序对话基础知识</span><span class="sxs-lookup"><span data-stu-id="2c86e-185">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* [<span data-ttu-id="2c86e-186">团队中的 Bot 身份验证</span><span class="sxs-lookup"><span data-stu-id="2c86e-186">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="2c86e-187">Microsoft Bot 框架</span><span class="sxs-lookup"><span data-stu-id="2c86e-187">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="2c86e-188">在不使用工具包的情况下创建机器人</span><span class="sxs-lookup"><span data-stu-id="2c86e-188">Create a bot without the toolkit</span></span>](../bots/how-to/create-a-bot-for-teams.md)
