---
title: 向 Microsoft 团队应用程序添加 bot
description: 介绍如何开始在 Microsoft 团队中开发 bot
keywords: 团队 bot 开发
ms.date: 05/20/2018
ms.openlocfilehash: 0ecb268c34275e958103c9905b2ed1f0858cafda
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673030"
---
# <a name="add-bots-to-microsoft-teams-apps"></a><span data-ttu-id="91446-104">向 Microsoft 团队应用程序添加 bot</span><span class="sxs-lookup"><span data-stu-id="91446-104">Add bots to Microsoft Teams apps</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="91446-105">构建和连接智能机器人，以便通过聊天自然与 Microsoft 团队用户交互。</span><span class="sxs-lookup"><span data-stu-id="91446-105">Build and connect intelligent bots to interact with Microsoft Teams users naturally through chat.</span></span> <span data-ttu-id="91446-106">或者提供一个简单的基于命令的 bot，用作您更广泛的团队应用体验的 "命令行" 界面。</span><span class="sxs-lookup"><span data-stu-id="91446-106">Or provide a simple commands-based bot, to be used as your "command-line" interface for your broader Teams app experience.</span></span> <span data-ttu-id="91446-107">您可以创建仅通知 bot，这可以在频道或直接消息中直接将与用户相关的信息推送到他们。</span><span class="sxs-lookup"><span data-stu-id="91446-107">You can make a notification-only bot, which can push information relevant to your users directly to them in a channel or direct message.</span></span> <span data-ttu-id="91446-108">您甚至可以引入现有的基于 Bot 框架的 bot 并添加团队特定的支持，以实现您的体验的亮点。</span><span class="sxs-lookup"><span data-stu-id="91446-108">You can even bring your existing Bot Framework-based bot and add Teams-specific support to make your experience shine.</span></span>

![帮助用户的机器人示例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a><span data-ttu-id="91446-110">您需要了解的内容： Bot</span><span class="sxs-lookup"><span data-stu-id="91446-110">What you need to know: Bots</span></span>

<span data-ttu-id="91446-111">与在对话中交互的任何其他团队成员类似，不同之处在于它具有一个六角头像图标，并且始终处于联机状态。</span><span class="sxs-lookup"><span data-stu-id="91446-111">A bot appears just like any other team member you interact with in a conversation except that it has a hexagonal avatar icon and is always online.</span></span>

<span data-ttu-id="91446-112">Bot 的行为有所不同，具体取决于所涉及的对话类型。</span><span class="sxs-lookup"><span data-stu-id="91446-112">A bot behaves differently depending on what kind of conversation it is involved in.</span></span> <span data-ttu-id="91446-113">团队中的 bot 支持几种对话（在[应用程序清单](~/resources/schema/manifest-schema.md)中称为 "作用域"）。</span><span class="sxs-lookup"><span data-stu-id="91446-113">Bots in Teams support several kinds of conversations (called scopes in the [app manifest](~/resources/schema/manifest-schema.md)).</span></span>

* <span data-ttu-id="91446-114">`teams`也称为频道对话</span><span class="sxs-lookup"><span data-stu-id="91446-114">`teams` Also called channel conversations</span></span>
* <span data-ttu-id="91446-115">`personal`Bot 和单个用户之间的对话</span><span class="sxs-lookup"><span data-stu-id="91446-115">`personal` Conversations between a bot and a single user</span></span>
* <span data-ttu-id="91446-116">`groupChat`机器人和2个或更多用户之间的对话</span><span class="sxs-lookup"><span data-stu-id="91446-116">`groupChat` A conversation between a bot and 2 or more users</span></span>

<span data-ttu-id="91446-117">有关详细信息，请参阅[与 Microsoft 团队 bot 进行对话](~/resources/bot-v3/bot-conversations/bots-conversations.md)。</span><span class="sxs-lookup"><span data-stu-id="91446-117">See [Have a conversation with a Microsoft Teams bot](~/resources/bot-v3/bot-conversations/bots-conversations.md) for more information.</span></span>

<span data-ttu-id="91446-118">在 Microsoft 团队应用程序中，你可以将 bot 设置为你的体验的明星或仅提供帮助者。</span><span class="sxs-lookup"><span data-stu-id="91446-118">With Microsoft Teams apps, you can make the bot the star of your experience, or just a helper.</span></span> <span data-ttu-id="91446-119">将 bot 作为更广泛的应用程序包的一部分进行分发，其中可能包括[选项卡](~/tabs/what-are-tabs.md)或[邮件扩展](~/messaging-extensions/what-are-messaging-extensions.md)等其他功能。</span><span class="sxs-lookup"><span data-stu-id="91446-119">Bots are distributed as part of your broader app package which can include other capabilities such as [tabs](~/tabs/what-are-tabs.md) or [messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="bot-apis"></a><span data-ttu-id="91446-120">Bot Api</span><span class="sxs-lookup"><span data-stu-id="91446-120">Bot APIs</span></span>

<span data-ttu-id="91446-121">Microsoft 团队支持大多数[Microsoft Bot 框架](https://dev.botframework.com/)。</span><span class="sxs-lookup"><span data-stu-id="91446-121">Microsoft Teams supports most of the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span> <span data-ttu-id="91446-122">（如果已经有一个基于 Bot 框架的 bot，可以轻松地将其调整为在 Microsoft 团队中工作。）我们建议您使用 c # 或 node.js 来利用我们的[sdk](/microsoftteams/platform/#pivot=sdk-tools)。</span><span class="sxs-lookup"><span data-stu-id="91446-122">(If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.) We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="91446-123">这些包扩展了基本的 Bot 生成器 SDK 类和方法：</span><span class="sxs-lookup"><span data-stu-id="91446-123">These packages extend the basic Bot Builder SDK classes and methods:</span></span>

* <span data-ttu-id="91446-124">使用专用的卡片类型，如 Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="91446-124">Using specialized card types like the Office 365 Connector card</span></span>
* <span data-ttu-id="91446-125">使用和设置针对活动的特定于团队的频道数据</span><span class="sxs-lookup"><span data-stu-id="91446-125">Consuming and setting Teams-specific channel data on activities</span></span>
* <span data-ttu-id="91446-126">处理邮件扩展请求</span><span class="sxs-lookup"><span data-stu-id="91446-126">Processing messaging extension requests</span></span>

<span data-ttu-id="91446-127">SDK 扩展安装了依赖项，包括机器人生成器 SDK。</span><span class="sxs-lookup"><span data-stu-id="91446-127">The SDK extensions install dependencies, including the Bot Builder SDK.</span></span>

* <span data-ttu-id="91446-128">**.Net**若要使用适用于 .NET 的机器人生成器 SDK 的 Microsoft 团队扩展，请在 Visual Studio 项目中安装 ".[团队](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)" NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="91446-128">**.NET** To use the Microsoft Teams extensions for the Bot Builder SDK for .NET, install the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package in your Visual Studio project.</span></span>
* <span data-ttu-id="91446-129">**Node.js 若要**使用用于 Node.js 的 BOT 生成器 SDK 的 Microsoft 团队扩展，请添加[botbuilder](https://www.npmjs.com/package/botbuilder-teams) npm 程序包。</span><span class="sxs-lookup"><span data-stu-id="91446-129">**Node.js** To use the Microsoft Teams extensions for the Bot Builder SDK for Node.js, add the [botbuilder-teams](https://www.npmjs.com/package/botbuilder-teams) npm package.</span></span>
* <span data-ttu-id="91446-130">**源代码**您可以在 Github 上的[BotBuilder-MicrosoftTeams](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams)存储库中查找扩展的完整源代码。</span><span class="sxs-lookup"><span data-stu-id="91446-130">**Source code** You can find the full source code for the extensions in the [BotBuilder-MicrosoftTeams](https://github.com/OfficeDev/BotBuilder-MicrosoftTeams) repo on Github.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="91446-131">您可以在任何其他 web 编程技术中开发团队应用程序，并直接调用[Bot 框架 REST api](/bot-framework/rest-api/bot-framework-rest-overview) ，但您必须自己执行所有令牌处理。</span><span class="sxs-lookup"><span data-stu-id="91446-131">You can develop Teams apps in any other web-programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

<span data-ttu-id="91446-132">*团队应用程序 Studio*可帮助您创建和配置应用程序清单，并可为您创建您的 Bot 框架 Bot。</span><span class="sxs-lookup"><span data-stu-id="91446-132">*Teams App Studio* helps you create and configure your app manifest, and can create your Bot Framework bot for you.</span></span> <span data-ttu-id="91446-133">它还包含响应控制库和交互式卡片生成器。</span><span class="sxs-lookup"><span data-stu-id="91446-133">It also contains a React control library and an interactive card builder.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="91446-134">传出 webhook</span><span class="sxs-lookup"><span data-stu-id="91446-134">Outgoing webhooks</span></span>

<span data-ttu-id="91446-135">通过传出 webhook，您可以创建简单的 bot 来实现基本交互，例如启动关闭工作流或您可能需要的其他简单命令。</span><span class="sxs-lookup"><span data-stu-id="91446-135">Outgoing webhooks allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands you may need.</span></span> <span data-ttu-id="91446-136">传出 webhook 仅在您创建它们的团队中实时发布，适用于特定于贵公司的工作流的简单流程。</span><span class="sxs-lookup"><span data-stu-id="91446-136">Outgoing webhooks live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="91446-137">有关详细信息，请参阅[出局 webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md) 。</span><span class="sxs-lookup"><span data-stu-id="91446-137">See [outgoing webhooks](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md) for more information.</span></span>

## <a name="build-a-great-teams-bot"></a><span data-ttu-id="91446-138">构建一个出色的团队 bot</span><span class="sxs-lookup"><span data-stu-id="91446-138">Build a great Teams bot</span></span>

<span data-ttu-id="91446-139">以下主题将指导您完成为团队创建出色的 bot 的过程。</span><span class="sxs-lookup"><span data-stu-id="91446-139">The following topics will guide you through the process of creating a great bot for Teams.</span></span>

* <span data-ttu-id="91446-140">[创建机器人](~/resources/bot-v3/bots-create.md)：充分利用由 bot 框架团队提供的强大工具、文档和社区。</span><span class="sxs-lookup"><span data-stu-id="91446-140">[Create a bot](~/resources/bot-v3/bots-create.md): Take advantage of the great tools, documentation, and community provided by the Bot Framework team.</span></span>
* <span data-ttu-id="91446-141">[与你的 Bot 对话](~/resources/bot-v3/bot-conversations/bots-conversations.md)：添加基本对话流和利用特定于频道的功能。</span><span class="sxs-lookup"><span data-stu-id="91446-141">[Talk to your bot](~/resources/bot-v3/bot-conversations/bots-conversations.md): Add basic conversation flow and leverage channel-specific functionality.</span></span> <span data-ttu-id="91446-142">如果是在 .NET 或 node.js 中进行开发，请使用机器人生成器 SDK 的扩展来简化您的工作。</span><span class="sxs-lookup"><span data-stu-id="91446-142">If you develop in .NET or Node.js, use our extensions for the Bot Builder SDK to simplify your work.</span></span>
* <span data-ttu-id="91446-143">[在你的 bot 中使用卡片](~/resources/bot-v3/bots-cards.md)设计卡片以传达和接受用户响应。</span><span class="sxs-lookup"><span data-stu-id="91446-143">[Using cards in your bot](~/resources/bot-v3/bots-cards.md) Design cards to communicate and accept user response.</span></span>
* <span data-ttu-id="91446-144">[响应 bot 事件](~/resources/bot-v3/bots-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="91446-144">[Respond to bot events](~/resources/bot-v3/bots-notifications.md).</span></span>
* <span data-ttu-id="91446-145">[仅通知 bot](~/resources/bot-v3/bots-notification-only.md)使用 bot 向您的应用程序发送通知。</span><span class="sxs-lookup"><span data-stu-id="91446-145">[Notification-only bots](~/resources/bot-v3/bots-notification-only.md) Using bots to send notifications for your app.</span></span>
* <span data-ttu-id="91446-146">[获取上下文](~/resources/bot-v3/bots-context.md)获取有关用户的信息。</span><span class="sxs-lookup"><span data-stu-id="91446-146">[Get context](~/resources/bot-v3/bots-context.md) Get information about the user.</span></span>
* <span data-ttu-id="91446-147">[Bot 菜单](~/resources/bot-v3/bots-menus.md)在 bot 中使用菜单。</span><span class="sxs-lookup"><span data-stu-id="91446-147">[Bot menus](~/resources/bot-v3/bots-menus.md) Using menus in bots.</span></span>
* <span data-ttu-id="91446-148">[Bot 和文件](~/resources/bot-v3/bots-files.md)从 bot 发送和接收文件。</span><span class="sxs-lookup"><span data-stu-id="91446-148">[Bots and files](~/resources/bot-v3/bots-files.md) Sending and receiving files from bots.</span></span>
* <span data-ttu-id="91446-149">[使用带 bot 的选项卡](~/resources/bot-v3/bots-with-tabs.md)使选项卡和 bot 协同工作。</span><span class="sxs-lookup"><span data-stu-id="91446-149">[Using tabs with bots](~/resources/bot-v3/bots-with-tabs.md) Making tabs and bots work together.</span></span>
* <span data-ttu-id="91446-150">[测试你的 bot](~/resources/bot-v3/bots-test.md)：添加你的个人或团队对话的 bot 以查看其操作。</span><span class="sxs-lookup"><span data-stu-id="91446-150">[Test your bot](~/resources/bot-v3/bots-test.md): Add your bot for personal or team conversations to see it in action.</span></span>
