---
title: " Microsoft Teams 中的自动程序"
author: clearab
description: Microsoft Teams 中的聊天机器人概述。
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 9ba7b6b96a8cbd55fac968975794d7c41d57f514
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058493"
---
# <a name="bots-in-microsoft-teams"></a><span data-ttu-id="87fe1-103"> Microsoft Teams 中的自动程序</span><span class="sxs-lookup"><span data-stu-id="87fe1-103">Bots in Microsoft Teams</span></span>

<span data-ttu-id="87fe1-104">聊天机器人也称为聊天机器人或对话机器人，它是运行由用户（如客户服务或支持人员）执行的简单且重复的自动化任务的应用。</span><span class="sxs-lookup"><span data-stu-id="87fe1-104">A bot also referred to as a chatbot or conversational bot is an app that runs simple and repetitive automated tasks performed by the users, such as customer service or support staff.</span></span> <span data-ttu-id="87fe1-105">日常使用中的机器人示例包括提供有关天气信息的机器人、预订预订或提供旅行信息。</span><span class="sxs-lookup"><span data-stu-id="87fe1-105">Examples of bots in everyday use include, bots that provide information about the weather, make dinner reservations, or provide travel information.</span></span> <span data-ttu-id="87fe1-106">机器人交互可以是一个快速的问题和答案，也可以是提供对服务的访问权限的复杂对话。</span><span class="sxs-lookup"><span data-stu-id="87fe1-106">A bot interaction can be a quick question and answer, or it can be a complex conversation that provides access to services.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/zSIysk0yL0Q]

<span data-ttu-id="87fe1-107">会话机器人允许用户通过文本、交互卡和任务模块与 web 服务进行交互。</span><span class="sxs-lookup"><span data-stu-id="87fe1-107">Conversational bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span>

![使用文本调用自动程序](~/assets/images/invokebotwithtext.png)

![使用卡片调用机器人](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

<span data-ttu-id="87fe1-110">对话机器人非常灵活，并且范围可以处理几个简单的命令，或复杂的、由人工智能支持且自然语言处理任务。</span><span class="sxs-lookup"><span data-stu-id="87fe1-110">Conversational bots are incredibly flexible and can be scoped to handle a few simple commands, or complex, artificial-intelligence-powered, and natural-language-processing tasks.</span></span> <span data-ttu-id="87fe1-111">它们可以是较大应用程序的一个方面，也可以完全独立。</span><span class="sxs-lookup"><span data-stu-id="87fe1-111">They can be one aspect of a larger application, or be completely stand-alone.</span></span>

<span data-ttu-id="87fe1-112">找到卡片、文本和任务模块的合适组合是创建有用的自动程序的关键。</span><span class="sxs-lookup"><span data-stu-id="87fe1-112">Finding the right mix of cards, text, and task modules are key to create a useful bot.</span></span> <span data-ttu-id="87fe1-113">下图显示了用户在一对一聊天中同时使用文本和交互式卡片与机器人进行对话：</span><span class="sxs-lookup"><span data-stu-id="87fe1-113">The following image shows a user conversing with a bot in a one-to-one chat using both, text and interactive cards:</span></span>

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="常见问题解答自动程序示例" border="true":::

<span data-ttu-id="87fe1-115">用户和机器人之间的每次交互都表示为活动。</span><span class="sxs-lookup"><span data-stu-id="87fe1-115">Every interaction between the user and the bot is represented as an activity.</span></span> <span data-ttu-id="87fe1-116">当机器人收到活动时，它会将活动传递给其活动处理程序。</span><span class="sxs-lookup"><span data-stu-id="87fe1-116">When a bot receives an activity, it passes it on to its activity handlers.</span></span> <span data-ttu-id="87fe1-117">有关详细信息，请参阅 [自动程序活动处理程序](~/bots/bot-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="87fe1-117">For more information, see [bot activity handlers](~/bots/bot-basics.md).</span></span> 

<span data-ttu-id="87fe1-118">此外，机器人是具有对话界面的应用。</span><span class="sxs-lookup"><span data-stu-id="87fe1-118">In addition, bots are apps that have a conversational interface.</span></span> <span data-ttu-id="87fe1-119">可以使用文本、交互式卡片和语音与机器人交互。</span><span class="sxs-lookup"><span data-stu-id="87fe1-119">You can interact with a bot using text, interactive cards, and speech.</span></span> <span data-ttu-id="87fe1-120">根据对话是频道还是群聊对话，还是一对一对话，机器人的行为会有所不同。</span><span class="sxs-lookup"><span data-stu-id="87fe1-120">A bot behaves differently depending on whether the conversation is a channel or group chat conversation, or it is a one-to-one conversation.</span></span> <span data-ttu-id="87fe1-121">对话通过 Bot Framework 连接器处理。</span><span class="sxs-lookup"><span data-stu-id="87fe1-121">Conversations are handled through the Bot Framework connector.</span></span> <span data-ttu-id="87fe1-122">有关详细信息，请参阅 [对话基础知识](~/bots/how-to/conversations/conversation-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="87fe1-122">For more information, see [conversation basics](~/bots/how-to/conversations/conversation-basics.md).</span></span>

<span data-ttu-id="87fe1-123">自动程序需要上下文信息（如用户配置文件详细信息）来访问相关内容并增强机器人体验。</span><span class="sxs-lookup"><span data-stu-id="87fe1-123">Your bot requires contextual information, such as user profile details to access relevant content and enhance the bot experience.</span></span> <span data-ttu-id="87fe1-124">有关详细信息，请参阅获取 [Teams 上下文](~/bots/how-to/get-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="87fe1-124">For more information, see [get Teams context](~/bots/how-to/get-teams-context.md).</span></span> 

<span data-ttu-id="87fe1-125">还可使用 Graph API 或 Teams 自动程序 API 通过自动程序发送和接收文件。</span><span class="sxs-lookup"><span data-stu-id="87fe1-125">You can also send and receive files through the bot using Graph APIs or Teams bot APIs.</span></span> <span data-ttu-id="87fe1-126">有关详细信息，请参阅通过自动 [程序发送和接收文件](~/bots/how-to/bots-filesv4.md)。</span><span class="sxs-lookup"><span data-stu-id="87fe1-126">For more information, see [send and receive files through the bot](~/bots/how-to/bots-filesv4.md).</span></span>

<span data-ttu-id="87fe1-127">此外，速率限制用于优化用于 Teams 应用程序的聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="87fe1-127">In addition, rate limiting is used to optimize bots used for your Teams application.</span></span> <span data-ttu-id="87fe1-128">为了保护 Microsoft Teams 及其用户，机器人 API 提供了传入请求的速率限制。</span><span class="sxs-lookup"><span data-stu-id="87fe1-128">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="87fe1-129">有关详细信息，请参阅在 [Teams 中通过速率限制优化机器人](~/bots/how-to/rate-limit.md)。</span><span class="sxs-lookup"><span data-stu-id="87fe1-129">For more information, see [optimize your bot with rate limiting in Teams](~/bots/how-to/rate-limit.md).</span></span>

<span data-ttu-id="87fe1-130">借助用于通话和联机会议的 Microsoft Graph API，Microsoft Teams 应用现在可以使用语音和视频与用户进行交互。</span><span class="sxs-lookup"><span data-stu-id="87fe1-130">With Microsoft Graph APIs for calls and online meetings, Microsoft Teams apps can now interact with users using voice and video.</span></span> <span data-ttu-id="87fe1-131">有关详细信息，请参阅 [通话和会议机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="87fe1-131">For more information, see [calls and meetings bots](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span> 

<span data-ttu-id="87fe1-132">可以使用 Teams 机器人 API 获取聊天或团队的一个或多个成员的信息。</span><span class="sxs-lookup"><span data-stu-id="87fe1-132">You can use the Teams bot APIs to get information for one or more members of a chat or team.</span></span> <span data-ttu-id="87fe1-133">有关详细信息，请参阅对 [Teams 自动程序 API 所做的更改，以提取团队或聊天成员](~/resources/team-chat-member-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="87fe1-133">For more information, see [changes to Teams bot APIs for fetching team or chat members](~/resources/team-chat-member-api-changes.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="87fe1-134">另请参阅</span><span class="sxs-lookup"><span data-stu-id="87fe1-134">See also</span></span>

- [<span data-ttu-id="87fe1-135">创建适合 Teams 的机器人</span><span class="sxs-lookup"><span data-stu-id="87fe1-135">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)

## <a name="next-step"></a><span data-ttu-id="87fe1-136">后续步骤</span><span class="sxs-lookup"><span data-stu-id="87fe1-136">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="87fe1-137">智能机器人和 SDK</span><span class="sxs-lookup"><span data-stu-id="87fe1-137">Bots and SDKs</span></span>](~/bots/bot-features.md)
