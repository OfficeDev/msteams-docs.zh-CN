---
title: " Microsoft Teams 中的自动程序"
author: surbhigupta
description: 自动程序在Microsoft Teams。
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 655684ef4f2a93d3f9c3858e3bf5a84eab4bd43c
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2021
ms.locfileid: "53068970"
---
# <a name="bots-in-microsoft-teams"></a><span data-ttu-id="9bd77-103"> Microsoft Teams 中的自动程序</span><span class="sxs-lookup"><span data-stu-id="9bd77-103">Bots in Microsoft Teams</span></span>

<span data-ttu-id="9bd77-104">聊天机器人也称为聊天机器人或对话机器人，它是运行由用户（如客户服务或支持人员）执行的简单且重复的自动化任务的应用。</span><span class="sxs-lookup"><span data-stu-id="9bd77-104">A bot also referred to as a chatbot or conversational bot is an app that runs simple and repetitive automated tasks performed by the users, such as customer service or support staff.</span></span> <span data-ttu-id="9bd77-105">日常使用中的机器人示例包括提供有关天气信息的机器人、预订预订或提供旅行信息。</span><span class="sxs-lookup"><span data-stu-id="9bd77-105">Examples of bots in everyday use include, bots that provide information about the weather, make dinner reservations, or provide travel information.</span></span> <span data-ttu-id="9bd77-106">机器人交互可以是一个快速的问题和答案，也可以是提供对服务的访问权限的复杂对话。</span><span class="sxs-lookup"><span data-stu-id="9bd77-106">A bot interaction can be a quick question and answer, or it can be a complex conversation that provides access to services.</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/zSIysk0yL0Q]

<span data-ttu-id="9bd77-107">会话机器人允许用户通过文本、交互卡和任务模块与 web 服务进行交互。</span><span class="sxs-lookup"><span data-stu-id="9bd77-107">Conversational bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span>

![使用文本调用自动程序](~/assets/images/invokebotwithtext.png)

![使用卡片调用机器人](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

<span data-ttu-id="9bd77-110">对话机器人非常灵活，并且范围可以处理几个简单的命令，或复杂的、由人工智能支持且自然语言处理任务。</span><span class="sxs-lookup"><span data-stu-id="9bd77-110">Conversational bots are incredibly flexible and can be scoped to handle a few simple commands, or complex, artificial-intelligence-powered, and natural-language-processing tasks.</span></span> <span data-ttu-id="9bd77-111">它们可以是较大应用程序的一个方面，也可以完全独立。</span><span class="sxs-lookup"><span data-stu-id="9bd77-111">They can be one aspect of a larger application, or be completely stand-alone.</span></span>

<span data-ttu-id="9bd77-112">找到卡片、文本和任务模块的合适组合是创建有用的自动程序的关键。</span><span class="sxs-lookup"><span data-stu-id="9bd77-112">Finding the right mix of cards, text, and task modules are key to create a useful bot.</span></span> <span data-ttu-id="9bd77-113">下图显示了用户在一对一聊天中同时使用文本和交互式卡片与机器人进行对话：</span><span class="sxs-lookup"><span data-stu-id="9bd77-113">The following image shows a user conversing with a bot in a one-to-one chat using both, text and interactive cards:</span></span>

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="常见问题解答自动程序示例" border="true":::

<span data-ttu-id="9bd77-115">用户和机器人之间的每次交互都表示为活动。</span><span class="sxs-lookup"><span data-stu-id="9bd77-115">Every interaction between the user and the bot is represented as an activity.</span></span> <span data-ttu-id="9bd77-116">当机器人收到活动时，它会将活动传递给其活动处理程序。</span><span class="sxs-lookup"><span data-stu-id="9bd77-116">When a bot receives an activity, it passes it on to its activity handlers.</span></span> <span data-ttu-id="9bd77-117">有关详细信息，请参阅 [自动程序活动处理程序](~/bots/bot-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="9bd77-117">For more information, see [bot activity handlers](~/bots/bot-basics.md).</span></span> 

<span data-ttu-id="9bd77-118">此外，机器人是具有对话界面的应用。</span><span class="sxs-lookup"><span data-stu-id="9bd77-118">In addition, bots are apps that have a conversational interface.</span></span> <span data-ttu-id="9bd77-119">可以使用文本、交互式卡片和语音与机器人交互。</span><span class="sxs-lookup"><span data-stu-id="9bd77-119">You can interact with a bot using text, interactive cards, and speech.</span></span> <span data-ttu-id="9bd77-120">根据对话是频道还是群聊对话，还是一对一对话，机器人的行为会有所不同。</span><span class="sxs-lookup"><span data-stu-id="9bd77-120">A bot behaves differently depending on whether the conversation is a channel or group chat conversation, or it is a one-to-one conversation.</span></span> <span data-ttu-id="9bd77-121">对话通过 Bot Framework 连接器处理。</span><span class="sxs-lookup"><span data-stu-id="9bd77-121">Conversations are handled through the Bot Framework connector.</span></span> <span data-ttu-id="9bd77-122">有关详细信息，请参阅 [对话基础知识](~/bots/how-to/conversations/conversation-basics.md)。</span><span class="sxs-lookup"><span data-stu-id="9bd77-122">For more information, see [conversation basics](~/bots/how-to/conversations/conversation-basics.md).</span></span>

<span data-ttu-id="9bd77-123">自动程序需要上下文信息（如用户配置文件详细信息）来访问相关内容并增强机器人体验。</span><span class="sxs-lookup"><span data-stu-id="9bd77-123">Your bot requires contextual information, such as user profile details to access relevant content and enhance the bot experience.</span></span> <span data-ttu-id="9bd77-124">有关详细信息，请参阅获取[Teams上下文](~/bots/how-to/get-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="9bd77-124">For more information, see [get Teams context](~/bots/how-to/get-teams-context.md).</span></span> 

<span data-ttu-id="9bd77-125">您还可以使用自动程序 API 或自动程序 API Graph发送和接收Teams文件。</span><span class="sxs-lookup"><span data-stu-id="9bd77-125">You can also send and receive files through the bot using Graph APIs or Teams bot APIs.</span></span> <span data-ttu-id="9bd77-126">有关详细信息，请参阅通过自动 [程序发送和接收文件](~/bots/how-to/bots-filesv4.md)。</span><span class="sxs-lookup"><span data-stu-id="9bd77-126">For more information, see [send and receive files through the bot](~/bots/how-to/bots-filesv4.md).</span></span>

<span data-ttu-id="9bd77-127">此外，速率限制还用于优化用于应用程序应用程序的Teams程序。</span><span class="sxs-lookup"><span data-stu-id="9bd77-127">In addition, rate limiting is used to optimize bots used for your Teams application.</span></span> <span data-ttu-id="9bd77-128">为了保护Microsoft Teams用户，自动程序 API 为传入请求提供了速率限制。</span><span class="sxs-lookup"><span data-stu-id="9bd77-128">To protect Microsoft Teams and its users, the bot APIs provide a rate limit for incoming requests.</span></span> <span data-ttu-id="9bd77-129">有关详细信息，请参阅使用 Teams[中的速率限制优化自动程序](~/bots/how-to/rate-limit.md)。</span><span class="sxs-lookup"><span data-stu-id="9bd77-129">For more information, see [optimize your bot with rate limiting in Teams](~/bots/how-to/rate-limit.md).</span></span>

<span data-ttu-id="9bd77-130">借助 Microsoft Graph API 进行呼叫和联机会议，Microsoft Teams应用现在可以使用语音和视频与用户进行交互。</span><span class="sxs-lookup"><span data-stu-id="9bd77-130">With Microsoft Graph APIs for calls and online meetings, Microsoft Teams apps can now interact with users using voice and video.</span></span> <span data-ttu-id="9bd77-131">有关详细信息，请参阅 [通话和会议机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="9bd77-131">For more information, see [calls and meetings bots](~/bots/calls-and-meetings/calls-meetings-bots-overview.md).</span></span> 

<span data-ttu-id="9bd77-132">可以使用聊天Teams API 获取聊天或团队的一个或多个成员的信息。</span><span class="sxs-lookup"><span data-stu-id="9bd77-132">You can use the Teams bot APIs to get information for one or more members of a chat or team.</span></span> <span data-ttu-id="9bd77-133">有关详细信息，请参阅[对自动程序 API Teams获取团队或聊天成员的更改](~/resources/team-chat-member-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="9bd77-133">For more information, see [changes to Teams bot APIs for fetching team or chat members](~/resources/team-chat-member-api-changes.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="9bd77-134">另请参阅</span><span class="sxs-lookup"><span data-stu-id="9bd77-134">See also</span></span>

[<span data-ttu-id="9bd77-135">创建适合 Teams 的机器人</span><span class="sxs-lookup"><span data-stu-id="9bd77-135">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)

## <a name="next-step"></a><span data-ttu-id="9bd77-136">后续步骤</span><span class="sxs-lookup"><span data-stu-id="9bd77-136">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="9bd77-137">智能机器人和 SDK</span><span class="sxs-lookup"><span data-stu-id="9bd77-137">Bots and SDKs</span></span>](~/bots/bot-features.md)
