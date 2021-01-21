---
title: 入门 - 生成邮件扩展
author: heath-hamilton
description: 使用 Microsoft Teams Toolkit 快速创建 Microsoft Teams 消息传递Toolkit。
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 86d44740feaa2cd33aff0e1dde14d757420d90d6
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911917"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a><span data-ttu-id="5a6b7-103">为 Microsoft Teams 构建消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="5a6b7-103">Build a messaging extension for Microsoft Teams</span></span>

<span data-ttu-id="5a6b7-104">有两种类型的 Teams 应用 *消息传递扩展*：[搜索命令](../messaging-extensions/how-to/search-commands/define-search-command.md)[和操作命令](../messaging-extensions/how-to/action-commands/define-action-command.md)。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-104">There are two types of Teams app *messaging extensions*: [Search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) and [action commands](../messaging-extensions/how-to/action-commands/define-action-command.md).</span></span>

<span data-ttu-id="5a6b7-105">在此课程中，你将创建搜索命令 (*也称为* 基于搜索的邮件扩展) ，它是在 Teams 中查找和共享外部内容的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-105">In this lesson, you'll create a *search command* (also known as a *search-based messaging extension*), which is a shortcut for finding external content and sharing it in Teams.</span></span> <span data-ttu-id="5a6b7-106">用户可以从 Teams 撰写或命令 [框访问搜索命令](../messaging-extensions/what-are-messaging-extensions.md)。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-106">Users can access search commands from the [Teams compose or command box](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="your-assignment"></a><span data-ttu-id="5a6b7-107">你的作业</span><span class="sxs-lookup"><span data-stu-id="5a6b7-107">Your assignment</span></span>

<span data-ttu-id="5a6b7-108">组织的技术支持通过 Teams 与用户进行通信，但票证位于单独的系统中。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-108">Your organization's help desk communicates with users through Teams, but the tickets reside in a separate system.</span></span> <span data-ttu-id="5a6b7-109">这意味着支持人员必须不断在应用之间来回切换。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-109">This means support staff must constantly go back and forth between apps.</span></span> <span data-ttu-id="5a6b7-110">你将调查如何通过为 Teams 创建简单的基于搜索的消息扩展来减少此上下文切换。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-110">You'll investigate how you might reduce this much context switching by creating a simple search-based messaging extension for Teams.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="5a6b7-111">您将了解哪些知识</span><span class="sxs-lookup"><span data-stu-id="5a6b7-111">What you'll learn</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="5a6b7-112">使用 Microsoft Teams Toolkit for Visual Studio Code 创建应用项目和消息传递扩展机器人</span><span class="sxs-lookup"><span data-stu-id="5a6b7-112">Create an app project and messaging extension bot using the Microsoft Teams Toolkit for Visual Studio Code</span></span>
> * <span data-ttu-id="5a6b7-113">确定应用配置和一些与邮件扩展相关的基架</span><span class="sxs-lookup"><span data-stu-id="5a6b7-113">Identify the app configurations and some of the scaffolding relevant to messaging extensions</span></span>
> * <span data-ttu-id="5a6b7-114">在本地托管应用</span><span class="sxs-lookup"><span data-stu-id="5a6b7-114">Host an app locally</span></span>
> * <span data-ttu-id="5a6b7-115">为邮件扩展配置自动程序</span><span class="sxs-lookup"><span data-stu-id="5a6b7-115">Configure the bot for your messaging extension</span></span>
> * <span data-ttu-id="5a6b7-116">在 Teams 中旁加载和测试消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="5a6b7-116">Sideload and test a messaging extension in Teams</span></span>

## <a name="before-you-begin"></a><span data-ttu-id="5a6b7-117">准备工作</span><span class="sxs-lookup"><span data-stu-id="5a6b7-117">Before you begin</span></span>

<span data-ttu-id="5a6b7-118">如果尚未安装，请确保了解并 [安装 Teams 开发先决条件](build-first-app-overview.md#get-prerequisites)。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-118">If you haven't yet, make sure you [understand and install the Teams development prerequisites](build-first-app-overview.md#get-prerequisites).</span></span>

## <a name="1-create-your-app-project"></a><span data-ttu-id="5a6b7-119">1. 创建应用项目</span><span class="sxs-lookup"><span data-stu-id="5a6b7-119">1. Create your app project</span></span>

<span data-ttu-id="5a6b7-120">Microsoft Teams Toolkit可帮助你为邮件扩展设置以下组件：</span><span class="sxs-lookup"><span data-stu-id="5a6b7-120">The Microsoft Teams Toolkit helps you set up the following components for your messaging extension:</span></span>

* <span data-ttu-id="5a6b7-121">**与邮件扩展相关的** 应用配置和基架</span><span class="sxs-lookup"><span data-stu-id="5a6b7-121">**App configurations and scaffolding** relevant to messaging extensions</span></span>
* <span data-ttu-id="5a6b7-122">**自动** 注册到 Microsoft Azure 自动程序服务的邮件扩展的自动程序</span><span class="sxs-lookup"><span data-stu-id="5a6b7-122">**Bot** for your messaging extension that's automatically registered with the Microsoft Azure Bot Service</span></span>

> [!TIP]
> <span data-ttu-id="5a6b7-123">如果你之前尚未创建 Teams 应用项目，你可能会发现按照这些说明更详细地解释项目会[](../build-your-first-app/build-and-run.md)很有帮助。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-123">If you haven't created a Teams app project before, you might find it helpful to follow [these instructions](../build-your-first-app/build-and-run.md) that explain projects in more detail.</span></span>

1. 在Visual Studio代码中，选择左侧活动栏上的 **Microsoft Teams，** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 **"创建新的 Teams 应用"。**
1. <span data-ttu-id="5a6b7-125">当系统提示时，使用 Microsoft 365 开发帐户登录。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-125">When prompted, sign in with your Microsoft 365 development account.</span></span>
1. <span data-ttu-id="5a6b7-126">在"**添加功能"** 屏幕上，选择 **"消息扩展**"，然后选择"**下一步"。**</span><span class="sxs-lookup"><span data-stu-id="5a6b7-126">On the **Add capabilities** screen, select **Messaging Extension** then **Next**.</span></span>
1. <span data-ttu-id="5a6b7-127">输入 Teams 应用的名称。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-127">Enter a name for your Teams app.</span></span> <span data-ttu-id="5a6b7-128"> (这是应用的默认名称，也是本地计算机上应用项目目录的名称。) </span><span class="sxs-lookup"><span data-stu-id="5a6b7-128">(This is the default name for your app and also the name of the app project directory on your local machine.)</span></span>
1. <span data-ttu-id="5a6b7-129">在 **"配置邮件扩展** "屏幕上，执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="5a6b7-129">On the **Configure messaging extension** screen, do the following:</span></span>
    1. <span data-ttu-id="5a6b7-130">仅选择 **邮件扩展类型的** 基于搜索的选项。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-130">Choose only the **Search-based** option for the type of messaging extension.</span></span>
    1. <span data-ttu-id="5a6b7-131">选择 **"新建自动程序**，**然后创建自动程序注册"。**</span><span class="sxs-lookup"><span data-stu-id="5a6b7-131">Select **Create a new Bot** then **Create Bot Registration**.</span></span> <span data-ttu-id="5a6b7-132">如果成功，你的新自动 **程序将具有** 注册状态。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-132">If successful, your new bot will have a **Registered** status.</span></span>
    1. <span data-ttu-id="5a6b7-133">现在 **，为链接** 取消链接选项选择"否"。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-133">For now, select **No** for the link unfurling option.</span></span>
1. <span data-ttu-id="5a6b7-134">选择 **屏幕** 底部的"完成"以配置项目。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-134">Select **Finish** at the bottom of the screen to configure your project.</span></span>

## <a name="2-identify-relevant-app-project-components"></a><span data-ttu-id="5a6b7-135">2. 确定相关应用程序项目组件</span><span class="sxs-lookup"><span data-stu-id="5a6b7-135">2. Identify relevant app project components</span></span>

<span data-ttu-id="5a6b7-136">使用 Teams 解决方案创建项目时，会自动设置大部分应用配置和基架Toolkit。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-136">Much of the app configurations and scaffolding are set up automatically when you create your project with the Teams Toolkit.</span></span>

### <a name="app-configurations"></a><span data-ttu-id="5a6b7-137">应用配置</span><span class="sxs-lookup"><span data-stu-id="5a6b7-137">App configurations</span></span>

<span data-ttu-id="5a6b7-138">若要查看或更新邮件扩展的配置，请在工具包中选择 App **Studio，** 然后转到 **邮件扩展**。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-138">To view or update your messaging extension's configurations, select **App Studio** in the toolkit and go to **Messaging extensions**.</span></span>

### <a name="app-scaffolding"></a><span data-ttu-id="5a6b7-139">应用基架</span><span class="sxs-lookup"><span data-stu-id="5a6b7-139">App scaffolding</span></span>

<span data-ttu-id="5a6b7-140">应用基架提供了一个文件，该文件位于项目的根目录中，用于处理邮件扩展 (或技术上，邮件扩展的自动程序) 如何响应 Teams 中的搜索查询。 `botActivityHandler.js` [](#4-configure-the-bot-for-your-messaging-extension)</span><span class="sxs-lookup"><span data-stu-id="5a6b7-140">The app scaffolding provides a `botActivityHandler.js` file, located in the root directory of your project, for handling how your messaging extension (or technically, the [messaging extension's bot](#4-configure-the-bot-for-your-messaging-extension)) responds to search queries in Teams.</span></span>

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a><span data-ttu-id="5a6b7-141">3. 为应用设置安全隧道</span><span class="sxs-lookup"><span data-stu-id="5a6b7-141">3. Set up a secure tunnel to your app</span></span>

<span data-ttu-id="5a6b7-142">出于测试目的，让我们在本地 Web 服务器上托管邮件扩展， (端口 3978) 。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-142">For testing purposes, let's host your messaging extension on a local web server (port 3978).</span></span>

1. <span data-ttu-id="5a6b7-143">如果尚未安装，请安装 [ngrok](https://ngrok.com/download)。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-143">If you haven't already, install [ngrok](https://ngrok.com/download).</span></span>
1. <span data-ttu-id="5a6b7-144">在终端中，运行 `ngrok http -host-header=rewrite 3978` 。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-144">In a terminal, run `ngrok http -host-header=rewrite 3978`.</span></span>
1. <span data-ttu-id="5a6b7-145">例如，复制输出 URL (，) `https://468b9ab725e9.ngrok.io` Teams 需要 HTTPS 连接。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-145">Copy the HTTPS URL in the output (for example, `https://468b9ab725e9.ngrok.io`) since Teams requires HTTPS connections.</span></span>

<span data-ttu-id="5a6b7-146">通过此 URL， (需要 HTTPS 连接的 Teams) 将能够通过隧道连接到在端口 `localhost` 3978 (托管应用) 。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-146">With this URL, Teams (which requires HTTPS connections) will be able tunnel to where you're hosting your app (`localhost` on port 3978).</span></span>

## <a name="4-configure-the-bot-for-your-messaging-extension"></a><span data-ttu-id="5a6b7-147">4. 为邮件扩展配置自动程序</span><span class="sxs-lookup"><span data-stu-id="5a6b7-147">4. Configure the bot for your messaging extension</span></span>

<span data-ttu-id="5a6b7-148">消息传递扩展依赖机器人将用户请求从 Teams 发送到托管服务并处理。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-148">Messaging extensions rely on bots to send and process user requests from Teams to your hosted service.</span></span> <span data-ttu-id="5a6b7-149">必须在 Azure 自动程序服务中注册自动程序，该服务是在使用 Teams 应用设置应用时Toolkit。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-149">The bot must be registered with the Azure Bot Service, which was done when you set up your app using the Teams Toolkit.</span></span>

<span data-ttu-id="5a6b7-150">您仍必须指定自动程序终结点 URL，以接收并处理邮件扩展中的搜索查询。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-150">You still must specify a bot endpoint URL to receive and process search queries in your messaging extension.</span></span> <span data-ttu-id="5a6b7-151">通常，URL 如下所示 `https://HOST_URL/api/messages` 。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-151">Typically, the URL looks like `https://HOST_URL/api/messages`.</span></span> <span data-ttu-id="5a6b7-152">可以在工具包中快速配置此功能。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-152">You can configure this quickly in the toolkit.</span></span>

1. 在Visual Studio代码中，选择左侧活动栏上的 **Microsoft Teams，** 然后选择" :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 打开 Microsoft **Teams** Toolkit。
1. <span data-ttu-id="5a6b7-154">转到 **"自动>现有自动程序注册** "，然后选择在安装期间创建的自动程序。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-154">Go to **Bots > Existing bot registrations** and select the bot you created during setup.</span></span>
1. <span data-ttu-id="5a6b7-155">在 **Bot 终结点地址** 字段中，输入 ngrok URL (例如，) 自动程序并追加 `https://468b9ab725e9.ngrok.io` `/api/messages` 到其中。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-155">In the **Bot endpoint address** field, enter the ngrok URL (for example, `https://468b9ab725e9.ngrok.io`) where you're hosting the bot and append `/api/messages` to it.</span></span>

<span data-ttu-id="5a6b7-156">机器人将能够处理邮件扩展中的查询。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-156">Your bot will be able to handle queries in your messaging extension.</span></span>

## <a name="5-build-and-run-your-app"></a><span data-ttu-id="5a6b7-157">5. 生成并运行应用</span><span class="sxs-lookup"><span data-stu-id="5a6b7-157">5. Build and run your app</span></span>

<span data-ttu-id="5a6b7-158">你已设置 URL 来托管邮件扩展，并配置它以处理搜索。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-158">You've set up a URL to host your messaging extension and configured it to handle searches.</span></span> <span data-ttu-id="5a6b7-159">是时候让应用启动并运行了。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-159">It's time to get your app up and running.</span></span>

1. <span data-ttu-id="5a6b7-160">在终端中，转到应用项目的根目录并运行 `npm install` 。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-160">In a terminal, go to the root directory of your app project and run `npm install`.</span></span>
1. <span data-ttu-id="5a6b7-161">运行 `npm start`。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-161">Run `npm start`.</span></span>

<span data-ttu-id="5a6b7-162">如果成功，你将看到以下消息，指示你的邮件扩展服务正在侦听你的活动 `localhost` ：</span><span class="sxs-lookup"><span data-stu-id="5a6b7-162">If successful, you see the following message indicating your messaging extension service is listening for activity at your `localhost`:</span></span>

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a><span data-ttu-id="5a6b7-163">6. 在 Teams 中旁加载邮件扩展</span><span class="sxs-lookup"><span data-stu-id="5a6b7-163">6. Sideload your messaging extension in Teams</span></span>

<span data-ttu-id="5a6b7-164">运行消息扩展后，可以在 Teams 中安装它。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-164">With your messaging extension running, you can install it in Teams.</span></span>

> [!TIP]
> <span data-ttu-id="5a6b7-165">如果你之前没有旁加载 Teams 应用并遇到问题，请按照以下 [说明操作](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-165">If you haven't sideloaded a Teams app before and run into issues, follow these [instructions](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams).</span></span>

1. <span data-ttu-id="5a6b7-166">在Visual Studio代码中，按 **F5** 键启动 Teams Web 客户端。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-166">In Visual Studio Code, press the **F5** key to launch a Teams web client.</span></span>
1. <span data-ttu-id="5a6b7-167">在应用安装对话框中，选择 **"为我添加"。**</span><span class="sxs-lookup"><span data-stu-id="5a6b7-167">In the app install dialog, select **Add for me**.</span></span>

## <a name="7-test-your-messaging-extension"></a><span data-ttu-id="5a6b7-168">7. 测试邮件扩展</span><span class="sxs-lookup"><span data-stu-id="5a6b7-168">7. Test your messaging extension</span></span>

<span data-ttu-id="5a6b7-169">了解消息扩展在 Teams 聊天中如何工作。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-169">Learn how messaging extensions work in a Teams chat.</span></span>

1. <span data-ttu-id="5a6b7-170">启动新聊天。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-170">Start a new chat.</span></span> 在撰写框中 **，选择"** 更多"并选择你刚刚旁加载的邮件 :::image type="icon" source="../assets/icons/teams-client-more.png"::: 扩展应用。
1. <span data-ttu-id="5a6b7-172">尝试搜索一些 (例如， **票证**) 。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-172">Try searching for something (for example, **Tickets**).</span></span> <span data-ttu-id="5a6b7-173">如果你的应用正常工作，你将看到示例搜索结果 (你可以稍后添加自己的) 。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-173">If your app is working, you'll see sample search results (you can add your own later).</span></span><br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="显示如何在 Teams 撰写框中使用基于搜索的消息扩展的屏幕截图。":::

## <a name="well-done"></a><span data-ttu-id="5a6b7-175">干的好</span><span class="sxs-lookup"><span data-stu-id="5a6b7-175">Well done</span></span>

<span data-ttu-id="5a6b7-176">恭喜！</span><span class="sxs-lookup"><span data-stu-id="5a6b7-176">Congratulations!</span></span> <span data-ttu-id="5a6b7-177">你拥有一个基本的 Teams 消息传递扩展，该扩展设置为在撰写或命令框中搜索外部内容。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-177">You have a basic Teams messaging extension that's set up to search for external content in the compose or command box.</span></span>

## <a name="next-steps"></a><span data-ttu-id="5a6b7-178">后续步骤</span><span class="sxs-lookup"><span data-stu-id="5a6b7-178">Next steps</span></span>

<span data-ttu-id="5a6b7-179">请参阅以下页面以继续构建功能齐全的邮件扩展：</span><span class="sxs-lookup"><span data-stu-id="5a6b7-179">See the following pages to continue and build a fully featured messaging extension:</span></span>

1. <span data-ttu-id="5a6b7-180">[定义与](../messaging-extensions/how-to/search-commands/define-search-command.md) 服务相关的搜索命令。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-180">[Define search commands](../messaging-extensions/how-to/search-commands/define-search-command.md) that are relevant to your service.</span></span>
1. <span data-ttu-id="5a6b7-181">配置服务 [以响应用户的搜索](../messaging-extensions/how-to/search-commands/respond-to-search.md)。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-181">Configure your service to [respond to users' searches](../messaging-extensions/how-to/search-commands/respond-to-search.md).</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="5a6b7-182">疑难解答</span><span class="sxs-lookup"><span data-stu-id="5a6b7-182">Troubleshooting</span></span>

<span data-ttu-id="5a6b7-183">如果你在完成本教程时出问题，以下信息可能会有所帮助。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-183">The following information may help if you had issues completing this tutorial.</span></span>

### <a name="bot-isnt-connected-to-teams"></a><span data-ttu-id="5a6b7-184">自动程序未连接到 Teams</span><span class="sxs-lookup"><span data-stu-id="5a6b7-184">Bot isn't connected to Teams</span></span>

<span data-ttu-id="5a6b7-185">如果你安装了应用，但它无法工作，请确保消息扩展的机器人已连接到 Azure Bot 服务的 [Teams *频道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-185">If you installed your app but it isn't working, make sure the messaging extension's bot is [connected to the Azure Bot Service's Teams *channel*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true).</span></span>

<span data-ttu-id="5a6b7-186">了解这与 Teams 中的频道不同，了解这一点很重要。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-186">It's important to understand that this isn't the same as a channel in Teams.</span></span> <span data-ttu-id="5a6b7-187">在这种情况下，频道是 Azure 自动程序服务如何将机器人连接到 Teams 或其他受支持的 [Microsoft 或第三方通信应用](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-187">In this case, a channel is how the Azure Bot Service connects your bot to Teams or another [supported Microsoft or third-party communications app](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span>

## <a name="learn-more"></a><span data-ttu-id="5a6b7-188">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="5a6b7-188">Learn more</span></span>

* [<span data-ttu-id="5a6b7-189">包含链接取消链接功能</span><span class="sxs-lookup"><span data-stu-id="5a6b7-189">Include a link unfurling feature</span></span>](../messaging-extensions/how-to/link-unfurling.md)
* <span data-ttu-id="5a6b7-190">遵循 [我们的设计准则，](../messaging-extensions/design/messaging-extension-design.md) 使用 [生产就绪 UI](../concepts/design/design-teams-app-ui-templates.md) 模板生成，以创建无缝体验。</span><span class="sxs-lookup"><span data-stu-id="5a6b7-190">Follow our [design guidelines](../messaging-extensions/design/messaging-extension-design.md) and build with [production-ready UI templates](../concepts/design/design-teams-app-ui-templates.md) to create a seamless experience.</span></span>
* [<span data-ttu-id="5a6b7-191">添加身份验证</span><span class="sxs-lookup"><span data-stu-id="5a6b7-191">Add authentication</span></span>](../messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="5a6b7-192">创建基于操作的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="5a6b7-192">Create an action-based messaging extension</span></span>](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="5a6b7-193">Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="5a6b7-193">Microsoft Bot Framework</span></span>](https://dev.botframework.com/)
