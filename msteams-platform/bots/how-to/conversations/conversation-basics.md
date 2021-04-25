---
title: 对话基础知识
description: 对话简介
ms.topic: overview
ms.author: anclear
keyword: conversations basics messages
ms.openlocfilehash: eff1c6fe18f7b2ba082b5075b6c1806f41b68a6b
ms.sourcegitcommit: dd2220f691029d043aaddfc7c229e332735acb1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/24/2021
ms.locfileid: "51996035"
---
# <a name="conversation-basics"></a><span data-ttu-id="c8684-103">对话基础知识</span><span class="sxs-lookup"><span data-stu-id="c8684-103">Conversation basics</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="c8684-104">对话是在 Microsoft Teams 自动程序与一个或多个用户之间发送的一系列消息。</span><span class="sxs-lookup"><span data-stu-id="c8684-104">A conversation is a series of messages sent between your Microsoft Teams bot and one or more users.</span></span> <span data-ttu-id="c8684-105">下表提供了三种类型的对话，在 Teams 中也称为范围：</span><span class="sxs-lookup"><span data-stu-id="c8684-105">The following table provides the three types of conversations, also called scopes in Teams:</span></span>

| <span data-ttu-id="c8684-106">对话类型</span><span class="sxs-lookup"><span data-stu-id="c8684-106">Conversation type</span></span> | <span data-ttu-id="c8684-107">说明</span><span class="sxs-lookup"><span data-stu-id="c8684-107">Description</span></span> |
| ------- | ----------- |
| `channel` | <span data-ttu-id="c8684-108">此对话类型对频道的所有成员可见。</span><span class="sxs-lookup"><span data-stu-id="c8684-108">This conversation type is visible to all members of the channel.</span></span> |
| `personal` | <span data-ttu-id="c8684-109">此对话类型包括机器人和单个用户之间的对话。</span><span class="sxs-lookup"><span data-stu-id="c8684-109">This conversation type includes conversations between bots and a single user.</span></span> |
| `groupChat` | <span data-ttu-id="c8684-110">此对话类型包括机器人与两个或多个用户之间的聊天。</span><span class="sxs-lookup"><span data-stu-id="c8684-110">This conversation type includes chat between a bot and two or more users.</span></span> <span data-ttu-id="c8684-111">它还可在会议聊天中启用机器人。</span><span class="sxs-lookup"><span data-stu-id="c8684-111">It also enables your bot in meeting chats.</span></span> |

<span data-ttu-id="c8684-112">自动程序的行为方式有所不同，具体取决于它涉及的对话：</span><span class="sxs-lookup"><span data-stu-id="c8684-112">A bot behaves differently depending on the conversation it is involved in:</span></span>

* <span data-ttu-id="c8684-113">频道和群聊对话中的聊天机器人要求用户 @ 提及机器人，以在频道中调用它。</span><span class="sxs-lookup"><span data-stu-id="c8684-113">Bots in channel and group chat conversations require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="c8684-114">一对一对话中的机器人不需要 @ 提及。</span><span class="sxs-lookup"><span data-stu-id="c8684-114">Bots in a one-to-one conversation do not require an @ mention.</span></span> <span data-ttu-id="c8684-115">用户发送的所有消息将路由到自动程序。</span><span class="sxs-lookup"><span data-stu-id="c8684-115">All messages sent by the user routes to your bot.</span></span>

<span data-ttu-id="c8684-116">若要使机器人能够处理特定对话或范围，在应用清单 中添加对此 [范围的支持](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="c8684-116">For the bot to work in a particular conversation or scope, add support to that scope in the [app manifest](~/resources/schema/manifest-schema.md).</span></span>

<span data-ttu-id="c8684-117">自动程序对话中每条消息都是 `Activity` 一个类型 为 的对象 `messageType: message` 。</span><span class="sxs-lookup"><span data-stu-id="c8684-117">Each message in a bot conversation is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="c8684-118">当用户发送消息时，Teams 会向机器人发布消息，机器人会处理该消息。</span><span class="sxs-lookup"><span data-stu-id="c8684-118">When a user sends a message, Teams posts the message to your bot and the bot handles the message.</span></span> <span data-ttu-id="c8684-119">此外，若要定义自动程序响应的核心命令，可以添加命令菜单以及自动程序命令的下拉列表。</span><span class="sxs-lookup"><span data-stu-id="c8684-119">In addition, to define core commands that your bot responds to, you can add a command menu with a drop-down list of commands for your bot.</span></span> <span data-ttu-id="c8684-120">组或频道中的聊天机器人仅在被提及时接收@botname。</span><span class="sxs-lookup"><span data-stu-id="c8684-120">Bots in a group or channel only receive messages when they are mentioned @botname.</span></span> <span data-ttu-id="c8684-121">Teams 会向自动程序发送有关在自动程序处于活动状态的范围中发生的对话事件的通知。</span><span class="sxs-lookup"><span data-stu-id="c8684-121">Teams sends notifications to your bot for conversation events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="c8684-122">可以在代码中捕获这些事件，然后对它们采取措施。</span><span class="sxs-lookup"><span data-stu-id="c8684-122">You can capture these events in your code and take action on them.</span></span> 

<span data-ttu-id="c8684-123">机器人还可以向用户发送主动消息。</span><span class="sxs-lookup"><span data-stu-id="c8684-123">A bot can also send proactive messages to users.</span></span> <span data-ttu-id="c8684-124">主动消息是自动程序发送的任何不响应用户请求的消息。</span><span class="sxs-lookup"><span data-stu-id="c8684-124">A proactive message is any message sent by a bot that is not in response to a request from a user.</span></span> <span data-ttu-id="c8684-125">你可以设置自动程序消息的格式，以包含包含交互式元素（如按钮、文本、图像、音频、视频等）的丰富卡片。</span><span class="sxs-lookup"><span data-stu-id="c8684-125">You can format your bot messages to include rich cards that include interactive elements, such as buttons, text, images, audio, video, and so on.</span></span> <span data-ttu-id="c8684-126">自动程序可以在发送邮件后动态更新消息，而不是将消息作为数据的静态快照。</span><span class="sxs-lookup"><span data-stu-id="c8684-126">Bot can dynamically update messages after sending them, instead of having your messages as static snapshots of data.</span></span> <span data-ttu-id="c8684-127">也可使用 Bot Framework 的方法删除 `DeleteActivity` 邮件。</span><span class="sxs-lookup"><span data-stu-id="c8684-127">Messages can also be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

## <a name="next-step"></a><span data-ttu-id="c8684-128">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c8684-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c8684-129">智能机器人对话中的邮件</span><span class="sxs-lookup"><span data-stu-id="c8684-129">Messages in bot conversations</span></span>](~/bots/how-to/conversations/conversation-messages.md)
