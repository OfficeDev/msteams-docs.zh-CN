---
title: 向应用添加Microsoft Teams程序
description: 介绍如何开始在 Microsoft Teams
ms.topic: conceptual
keywords: teams 机器人开发
localization_priority: Normal
ms.date: 05/20/2018
ms.openlocfilehash: 674576efccb2916b8a82ae27310d8fe49909a782
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566752"
---
# <a name="add-bots-to-microsoft-teams-apps"></a><span data-ttu-id="5f451-104">向应用添加Microsoft Teams程序</span><span class="sxs-lookup"><span data-stu-id="5f451-104">Add bots to Microsoft Teams apps</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="5f451-105">构建并连接智能机器人，以便Microsoft Teams用户自然地交互。</span><span class="sxs-lookup"><span data-stu-id="5f451-105">Build and connect intelligent bots to interact with Microsoft Teams users naturally through chat.</span></span> <span data-ttu-id="5f451-106">或者提供一个简单的基于命令的机器人，以用作你的"命令行"界面，以便Teams应用体验。</span><span class="sxs-lookup"><span data-stu-id="5f451-106">Or provide a simple commands-based bot, to be used as your "command-line" interface for your broader Teams app experience.</span></span> <span data-ttu-id="5f451-107">你可以制作一个仅通知自动程序，它可以将与用户有关的信息直接推送到频道或直接消息中。</span><span class="sxs-lookup"><span data-stu-id="5f451-107">You can make a notification-only bot, which can push information relevant to your users directly to them in a channel or direct message.</span></span> <span data-ttu-id="5f451-108">你甚至可以引入现有的基于 Bot Framework 的机器人，并添加Teams特定支持，以让你的体验大放异彩。</span><span class="sxs-lookup"><span data-stu-id="5f451-108">You can even bring your existing Bot Framework-based bot and add Teams-specific support to make your experience shine.</span></span>

![机器人协助用户的示例](~/assets/images/bot_example.png)

## <a name="what-you-need-to-know-bots"></a><span data-ttu-id="5f451-110">您需要了解哪些信息：Bots</span><span class="sxs-lookup"><span data-stu-id="5f451-110">What you need to know: Bots</span></span>

<span data-ttu-id="5f451-111">机器人的显示方式与你在对话中交互的其他任何团队成员一样，只是它具有一个六边形的头像图标，并且始终联机。</span><span class="sxs-lookup"><span data-stu-id="5f451-111">A bot appears just like any other team member you interact with in a conversation except that it has a hexagonal avatar icon and is always online.</span></span>

<span data-ttu-id="5f451-112">自动程序的行为方式有所不同，具体取决于它涉及的对话类型。</span><span class="sxs-lookup"><span data-stu-id="5f451-112">A bot behaves differently depending on what kind of conversation it is involved in.</span></span> <span data-ttu-id="5f451-113">聊天机器人Teams应用程序清单中称为作用域的[多种对话](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="5f451-113">Bots in Teams support several kinds of conversations called scopes in the [app manifest](~/resources/schema/manifest-schema.md).</span></span>

* <span data-ttu-id="5f451-114">`teams` 也称为频道对话。</span><span class="sxs-lookup"><span data-stu-id="5f451-114">`teams` Also called channel conversations.</span></span>
* <span data-ttu-id="5f451-115">`personal` 机器人和单个用户之间的对话。</span><span class="sxs-lookup"><span data-stu-id="5f451-115">`personal` Conversations between a bot and a single user.</span></span>
* <span data-ttu-id="5f451-116">`groupChat` 机器人与 2 个或多个用户之间的对话。</span><span class="sxs-lookup"><span data-stu-id="5f451-116">`groupChat` A conversation between a bot and 2 or more users.</span></span>

<span data-ttu-id="5f451-117">有关详细信息，请参阅与自动[程序Microsoft Teams对话](~/resources/bot-v3/bot-conversations/bots-conversations.md)。</span><span class="sxs-lookup"><span data-stu-id="5f451-117">For more information, see [Have a conversation with a Microsoft Teams bot](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span></span>

<span data-ttu-id="5f451-118">通过Microsoft Teams应用，你可以使机器人成为你体验的星形，或者只是一个帮助程序。</span><span class="sxs-lookup"><span data-stu-id="5f451-118">With Microsoft Teams apps, you can make the bot the star of your experience, or just a helper.</span></span> <span data-ttu-id="5f451-119">自动程序作为更广泛的应用包的一部分进行分发，其中可以包含选项卡或消息传递[扩展等其他功能](~/messaging-extensions/what-are-messaging-extensions.md)。 [](~/tabs/what-are-tabs.md)</span><span class="sxs-lookup"><span data-stu-id="5f451-119">Bots are distributed as part of your broader app package which can include other capabilities such as [tabs](~/tabs/what-are-tabs.md) or [messaging extensions](~/messaging-extensions/what-are-messaging-extensions.md).</span></span>

## <a name="bot-apis"></a><span data-ttu-id="5f451-120">自动程序 API</span><span class="sxs-lookup"><span data-stu-id="5f451-120">Bot APIs</span></span>

<span data-ttu-id="5f451-121">Microsoft Teams支持[大多数Microsoft Bot Framework。](https://dev.botframework.com/)</span><span class="sxs-lookup"><span data-stu-id="5f451-121">Microsoft Teams supports most of the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span> <span data-ttu-id="5f451-122"> (如果你已有一个基于 Bot Framework 的机器人，你可以轻松调整它以在 Microsoft Teams.) 我们建议你使用 C# 或 Node.js 来利用我们的[SDK。](/microsoftteams/platform/#pivot=sdk-tools)</span><span class="sxs-lookup"><span data-stu-id="5f451-122">(If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.) We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="5f451-123">这些工具包拓展了基本机器人生成器 SDK 的类和方法：</span><span class="sxs-lookup"><span data-stu-id="5f451-123">These packages extend the basic Bot Builder SDK classes and methods:</span></span>

* <span data-ttu-id="5f451-124">使用专用卡类型，如 Office 365 连接器卡。</span><span class="sxs-lookup"><span data-stu-id="5f451-124">Using specialized card types like the Office 365 Connector card.</span></span>
* <span data-ttu-id="5f451-125">使用和设置Teams特定频道数据。</span><span class="sxs-lookup"><span data-stu-id="5f451-125">Consuming and setting Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="5f451-126">处理邮件扩展请求。</span><span class="sxs-lookup"><span data-stu-id="5f451-126">Processing messaging extension requests.</span></span>

<span data-ttu-id="5f451-127">SDK 扩展将安装依赖项，包括 Bot Builder SDK。</span><span class="sxs-lookup"><span data-stu-id="5f451-127">The SDK extensions install dependencies, including the Bot Builder SDK.</span></span>

* <span data-ttu-id="5f451-128">**.NET** 若要使用 Microsoft Teams Builder SDK for .NET 的扩展，请安装 [Visual Studio 项目中的 Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet 程序包。</span><span class="sxs-lookup"><span data-stu-id="5f451-128">**.NET** To use the Microsoft Teams extensions for the Bot Builder SDK for .NET, install the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package in your Visual Studio project.</span></span> <span data-ttu-id="5f451-129">对于Node.js，botBuilder for Microsoft Teams 功能自 v4.6 起已合并到[Bot Framework SDK](https://github.com/microsoft/botframework-sdk)中。</span><span class="sxs-lookup"><span data-stu-id="5f451-129">For Node.js development, the BotBuilder for Microsoft Teams functionality has been incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) as of v4.6.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5f451-130">可以使用任何其他 web Teams技术开发应用程序并直接调用[Bot Framework REST](/bot-framework/rest-api/bot-framework-rest-overview) API，但你必须自己执行所有令牌处理。</span><span class="sxs-lookup"><span data-stu-id="5f451-130">You can develop Teams apps in any other web-programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

<span data-ttu-id="5f451-131">*Teams App Studio* 可帮助你创建和配置应用清单，并可以创建自动程序框架自动程序。</span><span class="sxs-lookup"><span data-stu-id="5f451-131">*Teams App Studio* helps you create and configure your app manifest, and can create your Bot Framework bot for you.</span></span> <span data-ttu-id="5f451-132">它还包含一个React库和交互式卡片生成器。</span><span class="sxs-lookup"><span data-stu-id="5f451-132">It also contains a React control library and an interactive card builder.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="5f451-133">传出 webhook</span><span class="sxs-lookup"><span data-stu-id="5f451-133">Outgoing webhooks</span></span>

<span data-ttu-id="5f451-134">传出 Webhook 允许你创建用于基本交互的简单自动程序，例如启动工作流或其他您可能需要的简单命令。</span><span class="sxs-lookup"><span data-stu-id="5f451-134">Outgoing webhooks allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands you may need.</span></span> <span data-ttu-id="5f451-135">传出 Webhook 仅在你创建它们的团队中活动，并且适用于特定于公司工作流的简单流程。</span><span class="sxs-lookup"><span data-stu-id="5f451-135">Outgoing webhooks live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="5f451-136">有关详细信息，请参阅传出[Webhook。](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="5f451-136">For more information, see [outgoing webhooks](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span></span>

## <a name="build-a-great-teams-bot"></a><span data-ttu-id="5f451-137">构建出色的自动Teams程序</span><span class="sxs-lookup"><span data-stu-id="5f451-137">Build a great Teams bot</span></span>

<span data-ttu-id="5f451-138">以下主题将指导你完成为用户创建出色的自动程序Teams：</span><span class="sxs-lookup"><span data-stu-id="5f451-138">The following topics will guide you through the process of creating a great bot for Teams:</span></span>

* <span data-ttu-id="5f451-139">[创建自动程序](~/resources/bot-v3/bots-create.md)：利用 Bot Framework 团队提供的出色的工具、文档和社区。</span><span class="sxs-lookup"><span data-stu-id="5f451-139">[Create a bot](~/resources/bot-v3/bots-create.md): Take advantage of the great tools, documentation, and community provided by the Bot Framework team.</span></span>
* <span data-ttu-id="5f451-140">[与机器人交谈](~/resources/bot-v3/bot-conversations/bots-conversations.md)：添加基本对话流并利用特定于频道的功能。</span><span class="sxs-lookup"><span data-stu-id="5f451-140">[Talk to your bot](~/resources/bot-v3/bot-conversations/bots-conversations.md): Add basic conversation flow and leverage channel-specific functionality.</span></span> <span data-ttu-id="5f451-141">如果使用 .NET 或 Node.js 开发，请使用自动程序生成器 SDK 的扩展来简化你的工作。</span><span class="sxs-lookup"><span data-stu-id="5f451-141">If you develop in .NET or Node.js, use our extensions for the Bot Builder SDK to simplify your work.</span></span>
* <span data-ttu-id="5f451-142">[在机器人中使用卡片](~/resources/bot-v3/bots-cards.md)：设计卡片以传达并接受用户响应。</span><span class="sxs-lookup"><span data-stu-id="5f451-142">[Using cards in your bot](~/resources/bot-v3/bots-cards.md): Design cards to communicate and accept user response.</span></span>
* [<span data-ttu-id="5f451-143">响应机器人事件</span><span class="sxs-lookup"><span data-stu-id="5f451-143">Respond to bot events</span></span>](~/resources/bot-v3/bots-notifications.md)
* <span data-ttu-id="5f451-144">[仅通知机器人](~/resources/bot-v3/bots-notification-only.md)：使用机器人为应用发送通知。</span><span class="sxs-lookup"><span data-stu-id="5f451-144">[Notification-only bots](~/resources/bot-v3/bots-notification-only.md): Using bots to send notifications for your app.</span></span>
* <span data-ttu-id="5f451-145">[获取上下文](~/resources/bot-v3/bots-context.md)：获取有关用户的信息。</span><span class="sxs-lookup"><span data-stu-id="5f451-145">[Get context](~/resources/bot-v3/bots-context.md): Get information about the user.</span></span>
* <span data-ttu-id="5f451-146">[自动程序](~/resources/bot-v3/bots-menus.md)菜单：使用机器人中的菜单。</span><span class="sxs-lookup"><span data-stu-id="5f451-146">[Bot menus](~/resources/bot-v3/bots-menus.md): Using menus in bots.</span></span>
* <span data-ttu-id="5f451-147">[机器人和文件](~/resources/bot-v3/bots-files.md)：从机器人发送和接收文件。</span><span class="sxs-lookup"><span data-stu-id="5f451-147">[Bots and files](~/resources/bot-v3/bots-files.md): Sending and receiving files from bots.</span></span>
* <span data-ttu-id="5f451-148">[将选项卡与机器人一同使用](~/resources/bot-v3/bots-with-tabs.md)：使选项卡和机器人协同工作。</span><span class="sxs-lookup"><span data-stu-id="5f451-148">[Using tabs with bots](~/resources/bot-v3/bots-with-tabs.md): Making tabs and bots work together.</span></span>
* <span data-ttu-id="5f451-149">[测试机器人](~/resources/bot-v3/bots-test.md)：添加用于个人或团队对话的自动程序以查看其运行。</span><span class="sxs-lookup"><span data-stu-id="5f451-149">[Test your bot](~/resources/bot-v3/bots-test.md): Add your bot for personal or team conversations to see it in action.</span></span>

## <a name="see-also"></a><span data-ttu-id="5f451-150">另请参阅</span><span class="sxs-lookup"><span data-stu-id="5f451-150">See also</span></span>

<span data-ttu-id="5f451-151">[Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="5f451-151">[Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>