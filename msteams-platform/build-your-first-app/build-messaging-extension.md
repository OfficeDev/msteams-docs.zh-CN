---
title: 入门-构建消息扩展
author: heath-hamilton
description: 使用 Microsoft 团队工具包快速创建 Microsoft 团队消息扩展。
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 160878d92969d57680e6fa25eb6fc13e82bf2a82
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931748"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="7042d-103">为 Microsoft 团队构建消息扩展</span><span class="sxs-lookup"><span data-stu-id="7042d-103">Build a messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="7042d-104">有两种类型的团队应用程序 *消息扩展* ： [搜索命令](../messaging-extensions/how-to/search-commands/define-search-command.md) 和 [操作命令](../messaging-extensions/how-to/action-commands/define-action-command.md)。</span><span class="sxs-lookup"><span data-stu-id="7042d-104">There are two types of Teams app *messaging extensions* : [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="7042d-105">在本课中，您将创建一个 *搜索命令* (也称为 " *基于搜索的邮件扩展* ") ，这是查找外部内容并在团队中共享它的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="7042d-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension* ), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="7042d-106">用户可以从 " [团队撰写" 或 "命令" 框](../messaging-extensions/what-are-messaging-extensions.md)中访问搜索命令。</span><span class="sxs-lookup"><span data-stu-id="7042d-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="7042d-107">您的分配</span><span class="sxs-lookup"><span data-stu-id="7042d-107">Your assignment</span></span>

<span data-ttu-id="7042d-108">您的组织的技术支持人员通过团队与用户通信，但票证驻留在单独的系统中。</span><span class="sxs-lookup"><span data-stu-id="7042d-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="7042d-109">这意味着支持人员必须在应用程序之间持续来回切换。</span><span class="sxs-lookup"><span data-stu-id="7042d-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="7042d-110">您将通过为工作组创建简单的基于搜索的邮件扩展功能，来研究如何减少这种更多的上下文切换。</span><span class="sxs-lookup"><span data-stu-id="7042d-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="7042d-111">你将了解的内容</span><span class="sxs-lookup"><span data-stu-id="7042d-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="7042d-112">使用 Microsoft 团队工具包为 Visual Studio Code 创建应用程序项目和邮件扩展 bot</span><span class="sxs-lookup"><span data-stu-id="7042d-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="7042d-113">标识与邮件扩展相关的应用程序配置和一些基架</span><span class="sxs-lookup"><span data-stu-id="7042d-113">Identify the app configurations and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="7042d-114">在本地托管应用程序</span><span class="sxs-lookup"><span data-stu-id="7042d-114">Host an app locally</span></span>
> * <span data-ttu-id="7042d-115">为邮件扩展配置 bot</span><span class="sxs-lookup"><span data-stu-id="7042d-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="7042d-116">旁加载和测试团队中的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="7042d-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="7042d-117">准备工作</span><span class="sxs-lookup"><span data-stu-id="7042d-117">Before you begin</span></span>

<span data-ttu-id="7042d-118">如果还没有，请确保 [了解并安装团队开发先决条件](build-first-app-overview.md#get-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="7042d-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="7042d-119">1. 创建您的应用程序项目</span><span class="sxs-lookup"><span data-stu-id="7042d-119">1. Create your app project</span></span>

<span data-ttu-id="7042d-120">Microsoft 团队工具包可帮助您为邮件扩展设置以下组件：</span><span class="sxs-lookup"><span data-stu-id="7042d-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="7042d-121">与邮件扩展相关的 **应用程序配置和基架**</span><span class="sxs-lookup"><span data-stu-id="7042d-121">**App configurations and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="7042d-122">自动注册到 Microsoft Azure Bot 服务的邮件扩展的 **Bot**</span><span class="sxs-lookup"><span data-stu-id="7042d-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="7042d-123">如果之前尚未创建团队应用程序项目，您可能会发现，请按照 [以下说明](../build-your-first-app/build-and-run.md) 更详细地说明项目。</span><span class="sxs-lookup"><span data-stu-id="7042d-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队** "， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用** "。
1. <span data-ttu-id="7042d-125">出现提示时，使用 Microsoft 365 开发帐户登录。</span><span class="sxs-lookup"><span data-stu-id="7042d-125">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="7042d-126">在 " **添加功能** " 屏幕上，依次选择 " **消息扩展** " 和 " **下一步** "</span><span class="sxs-lookup"><span data-stu-id="7042d-126">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="7042d-127">为你的团队应用输入名称。</span><span class="sxs-lookup"><span data-stu-id="7042d-127">Enter a name for your Teams app.</span></span> <span data-ttu-id="7042d-128"> (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) </span><span class="sxs-lookup"><span data-stu-id="7042d-128">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="7042d-129">在 " **配置消息扩展** " 屏幕上，执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="7042d-129">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="7042d-130">为邮件扩展类型选择 " **基于搜索** 的选项"。</span><span class="sxs-lookup"><span data-stu-id="7042d-130">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="7042d-131">选择 " **创建新的 bot** "，然后 **创建 bot 注册** 。</span><span class="sxs-lookup"><span data-stu-id="7042d-131">Select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="7042d-132">如果成功，新的 bot 将具有 **已注册** 状态。</span><span class="sxs-lookup"><span data-stu-id="7042d-132">If successful, your new bot will have a **Registered** status.</span></span>
    1. <span data-ttu-id="7042d-133">现在，为 "链接 unfurling" 选择 " **否** " 选项。</span><span class="sxs-lookup"><span data-stu-id="7042d-133">For now, select **No** for the link unfurling option.</span></span>
1. <span data-ttu-id="7042d-134">选择屏幕底部的 " **完成** " 以配置项目。</span><span class="sxs-lookup"><span data-stu-id="7042d-134">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="7042d-135">2. 确定相关的应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="7042d-135">2. Identify relevant app project components</span></span>

<span data-ttu-id="7042d-136">大部分应用配置和基架是在使用团队工具包创建项目时自动设置的。</span><span class="sxs-lookup"><span data-stu-id="7042d-136">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="7042d-137">应用配置</span><span class="sxs-lookup"><span data-stu-id="7042d-137">App configurations</span></span>

<span data-ttu-id="7042d-138">若要查看或更新邮件扩展插件的配置，请在工具包中选择 **应用程序 Studio** 并转到 " **邮件扩展** "。</span><span class="sxs-lookup"><span data-stu-id="7042d-138">To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="7042d-139">应用程序基架</span><span class="sxs-lookup"><span data-stu-id="7042d-139">App scaffolding</span></span>

<span data-ttu-id="7042d-140">应用程序基架提供一个 `botActivityHandler.js` 文件，该文件位于项目的根目录中，用于处理邮件扩展 [的](#4-configure-the-bot-for-your-messaging-extension) 自动程序) 对团队中的搜索查询的响应的处理方式 (或技术。</span><span class="sxs-lookup"><span data-stu-id="7042d-140">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="7042d-141">3. 设置应用程序的安全隧道</span><span class="sxs-lookup"><span data-stu-id="7042d-141">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="7042d-142">出于测试目的，让我们在本地 web 服务器上托管您的邮件扩展 (端口 3978) 。</span><span class="sxs-lookup"><span data-stu-id="7042d-142">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="7042d-143">如果还未安装，请安装 [ngrok](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="7042d-143">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="7042d-144">在终端中，运行 `ngrok http -host-header=rewrite 3978` 。</span><span class="sxs-lookup"><span data-stu-id="7042d-144">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="7042d-145">在输出中复制 HTTPS URL (例如， `https://468b9ab725e9.ngrok.io`) 自团队需要 HTTPS 连接。</span><span class="sxs-lookup"><span data-stu-id="7042d-145">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="7042d-146">使用此 URL 时，需要 HTTPS 连接) 的团队 (可以通过 `localhost` 端口 3978) 上的 (承载应用程序的位置进行隧道连接。</span><span class="sxs-lookup"><span data-stu-id="7042d-146">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="7042d-147">4. 配置邮件扩展的 bot</span><span class="sxs-lookup"><span data-stu-id="7042d-147">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="7042d-148">邮件扩展依靠 bot 来发送和处理从团队到托管服务的用户请求。</span><span class="sxs-lookup"><span data-stu-id="7042d-148">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="7042d-149">自动程序必须在 Azure Bot 服务中注册，这是在使用团队工具包设置应用程序时完成的。</span><span class="sxs-lookup"><span data-stu-id="7042d-149">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="7042d-150">您仍必须指定用于接收和处理邮件扩展中的搜索查询的 bot 终结点 URL。</span><span class="sxs-lookup"><span data-stu-id="7042d-150">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="7042d-151">通常，URL 如下所示 `https://HOST_URL/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="7042d-151">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="7042d-152">您可以在工具包中快速配置此设置。</span><span class="sxs-lookup"><span data-stu-id="7042d-152">You can configure this quickly in the toolkit.</span></span>

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队** "， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **打开 Microsoft 团队工具包** "。
1. <span data-ttu-id="7042d-154">转到 " **bot" > 现有的 bot 注册** ，并选择您在安装过程中创建的 bot。</span><span class="sxs-lookup"><span data-stu-id="7042d-154">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="7042d-155">在 " **Bot 终结点地址** " 字段中，输入 ngrok URL (例如， `https://468b9ab725e9.ngrok.io`) 您在其中承载机器人并追加 `/api/messages` 到它的位置。</span><span class="sxs-lookup"><span data-stu-id="7042d-155">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

<span data-ttu-id="7042d-156">你的 bot 将能够处理你的邮件扩展中的查询。</span><span class="sxs-lookup"><span data-stu-id="7042d-156">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="7042d-157">5. 生成并运行应用程序</span><span class="sxs-lookup"><span data-stu-id="7042d-157">5. Build and run your app</span></span>

<span data-ttu-id="7042d-158">您已经设置了一个 URL 来托管您的邮件扩展并将其配置为处理搜索。</span><span class="sxs-lookup"><span data-stu-id="7042d-158">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="7042d-159">现在就可以启动并运行您的应用程序了。</span><span class="sxs-lookup"><span data-stu-id="7042d-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="7042d-160">在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="7042d-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="7042d-161">运行 `npm start` 。</span><span class="sxs-lookup"><span data-stu-id="7042d-161">Run `npm start`.</span></span>

<span data-ttu-id="7042d-162">如果成功，你将看到以下消息，指示你的邮件扩展服务正在侦听你的活动 `localhost` ：</span><span class="sxs-lookup"><span data-stu-id="7042d-162">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="7042d-163">6. 旁加载您的邮件扩展在团队中</span><span class="sxs-lookup"><span data-stu-id="7042d-163">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="7042d-164">在邮件扩展运行的情况下，可以将其安装在团队中。</span><span class="sxs-lookup"><span data-stu-id="7042d-164">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="7042d-165">如果您在之前未旁加载团队应用程序并遇到问题，请按照这些 [说明](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)进行操作。</span><span class="sxs-lookup"><span data-stu-id="7042d-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="7042d-166">在 Visual Studio Code 中，按 **F5** 键以启动团队 web 客户端。</span><span class="sxs-lookup"><span data-stu-id="7042d-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="7042d-167">在 "应用程序安装" 对话框中，选择 " **为我添加** "。</span><span class="sxs-lookup"><span data-stu-id="7042d-167">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="7042d-168">7. 测试邮件扩展</span><span class="sxs-lookup"><span data-stu-id="7042d-168">7. Test your messaging extension</span></span>

<span data-ttu-id="7042d-169">了解邮件扩展在团队聊天中的工作方式。</span><span class="sxs-lookup"><span data-stu-id="7042d-169">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="7042d-170">启动新聊天。</span><span class="sxs-lookup"><span data-stu-id="7042d-170">Start a new chat.</span></span> 在 "撰写" 框中，选择 " **更多** :::image type="icon" source="../assets/icons/teams-client-more.png"::: "，然后选择您刚刚旁加载的邮件扩展应用程序。
1. <span data-ttu-id="7042d-172">尝试搜索 (如 " **票证** ) " 的内容。</span><span class="sxs-lookup"><span data-stu-id="7042d-172">Try searching for something (for example, **Tickets** ).</span></span> <span data-ttu-id="7042d-173">如果你的应用程序正常运行，你将看到示例搜索结果 (你可以在以后添加自己的) 。</span><span class="sxs-lookup"><span data-stu-id="7042d-173">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="显示在 _OL_QUOTE_PLACEHOLDER_团队撰写_OL_QUOTE_PLACEHOLDER_ 框中如何使用基于搜索的邮件扩展的屏幕截图。":::

## <a name="well-done"></a><span data-ttu-id="7042d-175">干的好</span><span class="sxs-lookup"><span data-stu-id="7042d-175">Well done</span></span>

<span data-ttu-id="7042d-176">祝贺你！</span><span class="sxs-lookup"><span data-stu-id="7042d-176">Congratulations!</span></span> <span data-ttu-id="7042d-177">您有一个基本的工作组邮件扩展，它设置为在撰写或命令框中搜索外部内容。</span><span class="sxs-lookup"><span data-stu-id="7042d-177">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="7042d-178">后续步骤</span><span class="sxs-lookup"><span data-stu-id="7042d-178">Next steps</span></span>

<span data-ttu-id="7042d-179">请参阅以下页面以继续操作并生成功能齐全的邮件扩展：</span><span class="sxs-lookup"><span data-stu-id="7042d-179">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="7042d-180">定义与您的服务相关的[搜索命令](../messaging-extensions/how-to/search-commands/define-search-command.md)。</span><span class="sxs-lookup"><span data-stu-id="7042d-180">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="7042d-181">将您的服务配置为 [响应用户的搜索](../messaging-extensions/how-to/search-commands/respond-to-search.md)。</span><span class="sxs-lookup"><span data-stu-id="7042d-181">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="7042d-182">故障排除</span><span class="sxs-lookup"><span data-stu-id="7042d-182">Troubleshooting</span></span>

<span data-ttu-id="7042d-183">如果你在完成本教程时遇到问题，以下信息可能会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="7042d-183">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="7042d-184">机器人未连接到团队</span><span class="sxs-lookup"><span data-stu-id="7042d-184">Bot isn't connected to Teams</span></span>

<span data-ttu-id="7042d-185">如果您安装了应用程序但不能正常运行，请确保消息扩展的 bot 已 [连接到 Azure Bot 服务的团队 *频道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="7042d-185">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="7042d-186">请务必了解，这与团队中的频道不相同。</span><span class="sxs-lookup"><span data-stu-id="7042d-186">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="7042d-187">在这种情况下，通道是 Azure Bot 服务将你的 Bot 连接到团队或其他 [受支持的 Microsoft 或第三方通信应用程序](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)的方式。</span><span class="sxs-lookup"><span data-stu-id="7042d-187">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="7042d-188">了解更多</span><span class="sxs-lookup"><span data-stu-id="7042d-188">Learn more</span></span>

* [<span data-ttu-id="7042d-189">包含链接 unfurling 功能</span><span class="sxs-lookup"><span data-stu-id="7042d-189">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* [<span data-ttu-id="7042d-190">添加身份验证</span><span class="sxs-lookup"><span data-stu-id="7042d-190">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="7042d-191">创建基于操作的消息扩展</span><span class="sxs-lookup"><span data-stu-id="7042d-191">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="7042d-192">Microsoft Bot 框架</span><span class="sxs-lookup"><span data-stu-id="7042d-192">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
