---
title: 入门 - 生成自动程序
author: heath-hamilton
description: 使用 Microsoft Teams 工具快速创建 Microsoft Teams Toolkit。
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 3e07c148e1b03431dc419a4e3679abac0229ff72
ms.sourcegitcommit: e08f309f62db2cf0f505f2aadfe728e5b46c17a5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/08/2021
ms.locfileid: "50140466"
---
# <a name="build-a-bot-for-microsoft-teams"></a><span data-ttu-id="fe2cf-103">为 Microsoft Teams 生成自动程序</span><span class="sxs-lookup"><span data-stu-id="fe2cf-103">Build a bot for Microsoft Teams</span></span>

<span data-ttu-id="fe2cf-104">本教程中将 *生成基本机器人* 应用。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-104">You'll build a basic *bot* app in this tutorial.</span></span> <span data-ttu-id="fe2cf-105">机器人充当 Teams 用户和 Web 服务之间的中介。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-105">A bot acts as an intermediary between Teams users and your web service.</span></span> <span data-ttu-id="fe2cf-106">用户可以与机器人聊天，以快速获取信息或启动由你的服务执行的工作流和任务。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-106">People can chat with a bot to quickly get information or initiate workflows and tasks performed by your service.</span></span>

## <a name="your-assignment"></a><span data-ttu-id="fe2cf-107">你的作业</span><span class="sxs-lookup"><span data-stu-id="fe2cf-107">Your assignment</span></span>

<span data-ttu-id="fe2cf-108">你的工作场所创建了一个 Teams 应用，该应用 [使用选项卡](../build-your-first-app/build-personal-tab.md) 来显示重要的联系信息。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-108">Your workplace created a Teams app that uses [tabs](../build-your-first-app/build-personal-tab.md) to surface important contact information.</span></span> <span data-ttu-id="fe2cf-109">例如，同事可以快速访问技术支持电话号码。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-109">For example, colleagues have quick access to the help desk phone number.</span></span> <span data-ttu-id="fe2cf-110">但是，如果人们能够使用聊天机器人联系技术支持，而不是通话呢？</span><span class="sxs-lookup"><span data-stu-id="fe2cf-110">But instead of calling, what if people could contact the help desk using a chatbot?</span></span> <span data-ttu-id="fe2cf-111">你的领导要求你查看在 Teams 中快速启动和运行基本对话机器人。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-111">Your boss asks you to look at how quickly you can get a basic conversational bot up and running in Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="fe2cf-112">您将了解哪些知识</span><span class="sxs-lookup"><span data-stu-id="fe2cf-112">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="fe2cf-113">使用 Microsoft Teams Toolkit for Visual Studio Code 创建应用项目和自动程序</span><span class="sxs-lookup"><span data-stu-id="fe2cf-113">Create an app project and bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="fe2cf-114">确定一些与机器人相关的应用配置和基架</span><span class="sxs-lookup"><span data-stu-id="fe2cf-114">Identify some of the app configurations and scaffolding relevant to bots</span></span>
> * <span data-ttu-id="fe2cf-115">在本地托管应用</span><span class="sxs-lookup"><span data-stu-id="fe2cf-115">Host an app locally</span></span>
> * <span data-ttu-id="fe2cf-116">为 Teams 配置自动程序</span><span class="sxs-lookup"><span data-stu-id="fe2cf-116">Configure a bot for Teams</span></span>
> * <span data-ttu-id="fe2cf-117">在 Teams 中旁加载和测试机器人</span><span class="sxs-lookup"><span data-stu-id="fe2cf-117">Sideload and test a bot in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="fe2cf-118">准备工作</span><span class="sxs-lookup"><span data-stu-id="fe2cf-118">Before you begin</span></span>

<span data-ttu-id="fe2cf-119">如果尚未安装，请确保了解并 [安装 Teams 开发先决条件](build-first-app-overview.md#get-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-119">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="fe2cf-120">1. 创建应用项目</span><span class="sxs-lookup"><span data-stu-id="fe2cf-120">1. Create your app project</span></span>

<span data-ttu-id="fe2cf-121">Microsoft Teams Toolkit可帮助你为应用设置以下组件：</span><span class="sxs-lookup"><span data-stu-id="fe2cf-121">The Microsoft Teams Toolkit helps you set up the following components for your app:</span></span>

* <span data-ttu-id="fe2cf-122">**与机器人相关的** 应用配置和基架</span><span class="sxs-lookup"><span data-stu-id="fe2cf-122">**App configurations and scaffolding** relevant to bots</span></span>
* <span data-ttu-id="fe2cf-123">**自动** 注册到 Microsoft Azure 自动程序服务的自动程序</span><span class="sxs-lookup"><span data-stu-id="fe2cf-123">**Bot** that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="fe2cf-124">如果你之前尚未创建 Teams 应用项目，你可能会发现按照这些说明更详细地解释项目会[](../build-your-first-app/build-and-run.md)很有帮助。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-124">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. 在Visual Studio代码中，选择左侧活动栏上的 **Microsoft Teams，** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 **"创建新的 Teams 应用"。**
1. <span data-ttu-id="fe2cf-126">当系统提示时，使用 Microsoft 365 开发帐户登录。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-126">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="fe2cf-127">在"**添加功能"屏幕上**，选择 **"自动程序**"，然后选择"**下一步"。**</span><span class="sxs-lookup"><span data-stu-id="fe2cf-127">On the **Add capabilities** screen, select **Bot** then **Next**.</span></span>
1. <span data-ttu-id="fe2cf-128">输入 Teams 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-128">Enter a name for your Teams app.</span></span> <span data-ttu-id="fe2cf-129"> (这是应用的默认名称，也是本地计算机上应用项目目录的名称。) </span><span class="sxs-lookup"><span data-stu-id="fe2cf-129">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="fe2cf-130">转到"**配置自动程序**"，然后选择 **"新建自动程序**，**然后创建自动程序注册"。**</span><span class="sxs-lookup"><span data-stu-id="fe2cf-130">Go to **Configure bot** and select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="fe2cf-131">如果成功，你的新自动 **程序将具有** 注册状态。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-131">If successful, your new bot will have a **Registered** status.</span></span>
1. <span data-ttu-id="fe2cf-132">选择 **屏幕** 底部的"完成"，然后选择创建项目的位置。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-132">Select **Finish** at the bottom of the screen and choose a location to create your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="fe2cf-133">2. 确定相关应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="fe2cf-133">2. Identify relevant app project components</span></span>

<span data-ttu-id="fe2cf-134">使用 Teams 解决方案创建项目时，会自动设置大部分应用配置和基架Toolkit。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-134">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span> <span data-ttu-id="fe2cf-135">让我们看一下生成自动程序的主要组件。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-135">Let's look at the main components for building a bot.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="fe2cf-136">应用配置</span><span class="sxs-lookup"><span data-stu-id="fe2cf-136">App configurations</span></span>

<span data-ttu-id="fe2cf-137">若要查看或更新机器人的配置，请在工具包中选择 **App Studio** 并转到 **Bots。**</span><span class="sxs-lookup"><span data-stu-id="fe2cf-137">To view or update your bot's configurations, select **App Studio** in the toolkit and go to **Bots**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="fe2cf-138">应用基架</span><span class="sxs-lookup"><span data-stu-id="fe2cf-138">App scaffolding</span></span>

<span data-ttu-id="fe2cf-139">应用基架提供了一个文件，该文件位于项目的根目录中，用于处理机器人如何处理 Teams (中的活动，例如机器人如何响应特定消息，如 `botActivityHandler.js` "Hello") 。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-139">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your bot processes activities in Teams (for example, how the bot responds to specific messages such as "Hello").</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="fe2cf-140">3. 为应用设置安全隧道</span><span class="sxs-lookup"><span data-stu-id="fe2cf-140">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="fe2cf-141">出于测试目的，让我们在本地 Web 服务器上托管应用， (端口 3978) 。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-141">For testing purposes, let's host your app on a local web server (port 3978).</span></span>

1. <span data-ttu-id="fe2cf-142">如果尚未安装，请安装 [ngrok](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-142">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="fe2cf-143">在终端中，运行 `ngrok http -host-header=rewrite 3978` 。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-143">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="fe2cf-144">例如，复制输出 URL (，) `https://468b9ab725e9.ngrok.io` Teams 需要 HTTPS 连接。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-144">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="fe2cf-145">通过此 URL， (需要 HTTPS 连接的 Teams) 将能够隧道连接到在 `localhost` 端口 3978 (托管应用) 。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-145">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-your-bot"></a><span data-ttu-id="fe2cf-146">4. 配置机器人</span><span class="sxs-lookup"><span data-stu-id="fe2cf-146">4. Configure your bot</span></span>

<span data-ttu-id="fe2cf-147">若要在 Teams 中使用自动程序，你必须向 Azure Bot 服务注册它。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-147">To use a bot in Teams, you must register it with the Azure Bot Service.</span></span> <span data-ttu-id="fe2cf-148">如果你使用 Teams 服务设置应用，这将自动Toolkit。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-148">Lucky for you, this is done automatically when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="fe2cf-149">您仍必须指定终结点地址，以接收并处理 (消息，即发送到自动) 的请求。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-149">You still must specify an endpoint address to receive and process user messages (i.e., requests) sent to the bot.</span></span> <span data-ttu-id="fe2cf-150">通常，URL 如下所示 `https://HOST_URL/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-150">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="fe2cf-151">可以在工具包中快速配置此功能。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-151">You can configure this quickly in the toolkit.</span></span>

1. 在Visual Studio代码中，选择左侧活动栏上的 **Microsoft Teams，** 然后选择" :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 打开 Microsoft **Teams** Toolkit。
1. <span data-ttu-id="fe2cf-153">转到 **自动程序>自动程序注册，** 然后选择在安装期间创建的自动程序。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-153">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="fe2cf-154">在 **Bot 终结点地址** 字段中，输入 ngrok URL (例如，) 自动程序并追加 `https://468b9ab725e9.ngrok.io` `/api/messages` 到其中。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-154">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span><br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="显示可在 Teams 服务中配置自动程序终结点 URL 的Toolkit。":::

<span data-ttu-id="fe2cf-156">机器人将能够响应 Teams 中的消息。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-156">Your bot will be able to respond to messages in Teams.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="fe2cf-157">5. 生成并运行应用</span><span class="sxs-lookup"><span data-stu-id="fe2cf-157">5. Build and run your app</span></span>

<span data-ttu-id="fe2cf-158">你已设置 URL 来托管自动程序，并配置它以处理消息。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-158">You've set up a URL to host your bot and configured it to handle messages.</span></span> <span data-ttu-id="fe2cf-159">是时候让应用启动并运行了。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="fe2cf-160">在终端中，转到应用项目的根目录并运行 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="fe2cf-161">运行 `npm start`。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-161">Run `npm start`.</span></span>

<span data-ttu-id="fe2cf-162">如果成功，你将看到以下消息，指示机器人正在侦听你的活动 `localhost` ：</span><span class="sxs-lookup"><span data-stu-id="fe2cf-162">If successful, you see the following message indicating your bot is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a><span data-ttu-id="fe2cf-163">6. 在 Teams 中旁加载机器人</span><span class="sxs-lookup"><span data-stu-id="fe2cf-163">6. Sideload your bot in Teams</span></span>

<span data-ttu-id="fe2cf-164">运行自动程序后，可以在 Teams 中安装它。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-164">With your bot running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="fe2cf-165">如果你之前没有旁加载 Teams 应用并遇到问题，请按照以下 [说明操作](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="fe2cf-166">在Visual Studio代码中，按 **F5** 键启动 Teams Web 客户端。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="fe2cf-167">在应用安装对话框中，选择 **"为我添加"。**</span><span class="sxs-lookup"><span data-stu-id="fe2cf-167">In the app install dialog, select **Add for me**.</span></span> <span data-ttu-id="fe2cf-168"> (你可以将聊天机器人添加到频道或聊天中，但对其他人来说，在一对一聊天中测试机器人的干扰性) </span><span class="sxs-lookup"><span data-stu-id="fe2cf-168">(You could add the bot to a channel or chat, but it's less intrusive to others to test a bot in a one-on-one chat.)</span></span>

## <a name="7-test-your-bot"></a><span data-ttu-id="fe2cf-169">7. 测试机器人</span><span class="sxs-lookup"><span data-stu-id="fe2cf-169">7. Test your bot</span></span>

<span data-ttu-id="fe2cf-170">现在，对于有趣的部分：让我们对机器人说"Hello"。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-170">Now for the fun part: Let's say "Hello" to your bot.</span></span>

1. <span data-ttu-id="fe2cf-171">在撰写框中，发送邮件 `Hello` 。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-171">In the compose box, send a `Hello` message.</span></span>

<span data-ttu-id="fe2cf-172">机器人使用如下消息进行回复。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-172">Your bot replies with something like the following message.</span></span>

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="显示用户向 Teams 机器人说&quot;Hello&quot;并收到响应的屏幕截图。":::

## <a name="well-done"></a><span data-ttu-id="fe2cf-174">干的好</span><span class="sxs-lookup"><span data-stu-id="fe2cf-174">Well done</span></span>

<span data-ttu-id="fe2cf-175">恭喜！</span><span class="sxs-lookup"><span data-stu-id="fe2cf-175">Congratulations!</span></span> <span data-ttu-id="fe2cf-176">你拥有一个基本的 Teams 机器人，可以一对一地与用户通信，或在频道和聊天 (组设置中) 。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-176">You have a basic Teams bot that can communicate with users one-on-one or in group settings (channels and chats).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="fe2cf-177">疑难解答</span><span class="sxs-lookup"><span data-stu-id="fe2cf-177">Troubleshooting</span></span>

<span data-ttu-id="fe2cf-178">如果你在完成本教程时出问题，以下信息可能会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-178">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="fe2cf-179">自动程序未连接到 Teams</span><span class="sxs-lookup"><span data-stu-id="fe2cf-179">Bot isn't connected to Teams</span></span>

<span data-ttu-id="fe2cf-180">如果已安装应用，但自动程序无法工作，请确保自动程序已连接到 Azure [Bot 服务的 Teams *频道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-180">If you installed your app but the bot isn't working, make sure the bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="fe2cf-181">了解这与 Teams 中的频道不同，了解这一点很重要。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-181">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="fe2cf-182">在这种情况下，频道是 Azure 自动程序服务如何将机器人连接到 Teams 或其他受支持的 [Microsoft 或第三方通信应用](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-182">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="fe2cf-183">了解更多</span><span class="sxs-lookup"><span data-stu-id="fe2cf-183">Learn more</span></span>

* [<span data-ttu-id="fe2cf-184">了解 Teams 机器人可以使用我们的一个示例执行哪些其他功能</span><span class="sxs-lookup"><span data-stu-id="fe2cf-184">See what else Teams bots can do with one of our samples</span></span>](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [<span data-ttu-id="fe2cf-185">自动程序对话基础知识</span><span class="sxs-lookup"><span data-stu-id="fe2cf-185">Bot conversation basics</span></span>](../bots/how-to/conversations/conversation-basics.md)
* <span data-ttu-id="fe2cf-186">遵循 [我们的设计准则，](../bots/design/bots.md) 使用 [生产就绪 UI](../concepts/design/design-teams-app-ui-templates.md) 模板生成，以创建无缝体验。</span><span class="sxs-lookup"><span data-stu-id="fe2cf-186">Follow our [design guidelines](../bots/design/bots.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* [<span data-ttu-id="fe2cf-187">Teams 中的自动程序身份验证</span><span class="sxs-lookup"><span data-stu-id="fe2cf-187">Bot authentication in Teams</span></span>](../bots/how-to/authentication/auth-flow-bot.md)
* [<span data-ttu-id="fe2cf-188">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="fe2cf-188">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
* [<span data-ttu-id="fe2cf-189">创建没有工具包的机器人</span><span class="sxs-lookup"><span data-stu-id="fe2cf-189">Create a bot without the toolkit</span></span>](../resources/bot-v3/bots-create.md)
