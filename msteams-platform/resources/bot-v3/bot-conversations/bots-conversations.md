---
title: 使用自动程序发送和接收消息
description: 介绍如何在邮件中通过自动程序发送和接收Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: teams 自动程序消息
ms.date: 05/20/2019
ms.openlocfilehash: efa7658aef87650e360c79523ac1c282dc4814fd
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630458"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="4918e-104">与自动程序Microsoft Teams对话</span><span class="sxs-lookup"><span data-stu-id="4918e-104">Have a conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="4918e-105">对话是在你的机器人和一个或以上用户之间发送的一系列消息。</span><span class="sxs-lookup"><span data-stu-id="4918e-105">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="4918e-106">在 Teams 中有三种对话类型（也称范围）：</span><span class="sxs-lookup"><span data-stu-id="4918e-106">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="4918e-107">`teams` 也称为频道对话，对频道的所有成员可见。</span><span class="sxs-lookup"><span data-stu-id="4918e-107">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="4918e-108">`personal` 机器人和单个用户之间的对话。</span><span class="sxs-lookup"><span data-stu-id="4918e-108">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="4918e-109">`groupChat` 机器人与两个或多个用户之间的聊天。</span><span class="sxs-lookup"><span data-stu-id="4918e-109">`groupChat` Chat between a bot and two or more users.</span></span>

<span data-ttu-id="4918e-110">自动程序的行为稍有不同，具体取决于它涉及的对话类型：</span><span class="sxs-lookup"><span data-stu-id="4918e-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="4918e-111">[频道和群聊](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) 对话中的聊天机器人要求用户@mention自动程序在频道中调用它。</span><span class="sxs-lookup"><span data-stu-id="4918e-111">[Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="4918e-112">[单个用户对话中的](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) 自动程序不需要@mention -用户只需键入。</span><span class="sxs-lookup"><span data-stu-id="4918e-112">[Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @mention -  the user can just type.</span></span>

<span data-ttu-id="4918e-113">为了使机器人能够处理特定范围，应在清单中列为支持该范围。</span><span class="sxs-lookup"><span data-stu-id="4918e-113">In order for the bot to work in a particular scope it should be listed as supporting that scope in the manifest.</span></span> <span data-ttu-id="4918e-114">范围在清单参考中进行了进一步 [的定义和讨论](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="4918e-114">Scopes are defined and discussed further in the [Manifest Reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="proactive-messages"></a><span data-ttu-id="4918e-115">主动邮件</span><span class="sxs-lookup"><span data-stu-id="4918e-115">Proactive messages</span></span>

<span data-ttu-id="4918e-116">机器人可以参与对话或启动对话。</span><span class="sxs-lookup"><span data-stu-id="4918e-116">Bots can participate in a conversation or initiate one.</span></span> <span data-ttu-id="4918e-117">大多数通信都是为了响应另一条消息。</span><span class="sxs-lookup"><span data-stu-id="4918e-117">Most communication is in response to another message.</span></span> <span data-ttu-id="4918e-118">如果机器人启动对话，则称为主动 *消息*。</span><span class="sxs-lookup"><span data-stu-id="4918e-118">If a bot initiates a conversation it is called a *proactive message*.</span></span> <span data-ttu-id="4918e-119">示例包括：</span><span class="sxs-lookup"><span data-stu-id="4918e-119">Examples include:</span></span>

* <span data-ttu-id="4918e-120">欢迎消息</span><span class="sxs-lookup"><span data-stu-id="4918e-120">Welcome messages</span></span>
* <span data-ttu-id="4918e-121">事件通知</span><span class="sxs-lookup"><span data-stu-id="4918e-121">Event notifications</span></span>
* <span data-ttu-id="4918e-122">轮询消息</span><span class="sxs-lookup"><span data-stu-id="4918e-122">Polling messages</span></span>

## <a name="conversation-basics"></a><span data-ttu-id="4918e-123">对话基础知识</span><span class="sxs-lookup"><span data-stu-id="4918e-123">Conversation basics</span></span>

<span data-ttu-id="4918e-124">每条消息是类型 `messageType: message` 的一个 `Activity` 对象。</span><span class="sxs-lookup"><span data-stu-id="4918e-124">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="4918e-125">当用户发送消息时，Teams 会将消息发布给你的机器人。具体地说，它会发送一个 JSON 对象给你的机器人的消息传递端点。</span><span class="sxs-lookup"><span data-stu-id="4918e-125">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="4918e-126">自动程序将检查消息以确定其类型并相应地做出响应。</span><span class="sxs-lookup"><span data-stu-id="4918e-126">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="4918e-127">机器人还支持事件样式的消息。</span><span class="sxs-lookup"><span data-stu-id="4918e-127">Bots also support event-style messages.</span></span> <span data-ttu-id="4918e-128">有关详细信息，请参阅处理[Microsoft Teams 中的自动程序事件](~/resources/bot-v3/bots-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="4918e-128">For more information, see [Handle bot events in Microsoft Teams](~/resources/bot-v3/bots-notifications.md).</span></span> <span data-ttu-id="4918e-129">语音当前不受支持。</span><span class="sxs-lookup"><span data-stu-id="4918e-129">Speech is currently not supported.</span></span>

<span data-ttu-id="4918e-130">消息在所有范围内大部分都相同，但在 UI 中访问自动程序的方式和你需要了解的场景差异存在差异。</span><span class="sxs-lookup"><span data-stu-id="4918e-130">Messages are for the most part the same in across all scopes, but there are differences in how the bot is accessed in the UI and differences behind the scenes which you will need to know about.</span></span>

<span data-ttu-id="4918e-131">基本对话通过 Bot Framework 连接器进行处理，该连接器是一个 REST API，使机器人能够Teams和其他频道进行通信。</span><span class="sxs-lookup"><span data-stu-id="4918e-131">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="4918e-132">Bot Builder SDK 提供了轻松访问此 API、管理对话流和状态的其他功能，以及合并认知服务（如自然语言处理和 NLP (）) 。</span><span class="sxs-lookup"><span data-stu-id="4918e-132">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="message-content"></a><span data-ttu-id="4918e-133">邮件内容</span><span class="sxs-lookup"><span data-stu-id="4918e-133">Message content</span></span>

<span data-ttu-id="4918e-134">机器人可以发送格式文本、图片和卡片。</span><span class="sxs-lookup"><span data-stu-id="4918e-134">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="4918e-135">用户可以向自动程序发送格式文本和图片。</span><span class="sxs-lookup"><span data-stu-id="4918e-135">Users can send rich text and pictures to your bot.</span></span> <span data-ttu-id="4918e-136">你可以指定自动程序可以在自动程序Microsoft Teams设置页中处理的内容类型。</span><span class="sxs-lookup"><span data-stu-id="4918e-136">You can specify the type of content your bot can handle in the Microsoft Teams settings page for your bot.</span></span>

| <span data-ttu-id="4918e-137">Format</span><span class="sxs-lookup"><span data-stu-id="4918e-137">Format</span></span> | <span data-ttu-id="4918e-138">从用户到机器人</span><span class="sxs-lookup"><span data-stu-id="4918e-138">From user to bot</span></span>  | <span data-ttu-id="4918e-139">从自动程序到用户</span><span class="sxs-lookup"><span data-stu-id="4918e-139">From bot to user</span></span> |  <span data-ttu-id="4918e-140">注释</span><span class="sxs-lookup"><span data-stu-id="4918e-140">Notes</span></span> |
| --- | :---: | :---: | --- |
| <span data-ttu-id="4918e-141">格式文本 </span><span class="sxs-lookup"><span data-stu-id="4918e-141">Rich text</span></span> | <span data-ttu-id="4918e-142">✔</span><span class="sxs-lookup"><span data-stu-id="4918e-142">✔</span></span> | <span data-ttu-id="4918e-143">✔</span><span class="sxs-lookup"><span data-stu-id="4918e-143">✔</span></span> |  |
| <span data-ttu-id="4918e-144">图片</span><span class="sxs-lookup"><span data-stu-id="4918e-144">Pictures</span></span> | <span data-ttu-id="4918e-145">✔</span><span class="sxs-lookup"><span data-stu-id="4918e-145">✔</span></span> | <span data-ttu-id="4918e-146">✔</span><span class="sxs-lookup"><span data-stu-id="4918e-146">✔</span></span> | <span data-ttu-id="4918e-147">PNG、JPEG 或 GIF 格式的最大大小为 1024×1024 和 1 MB;不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="4918e-147">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported.</span></span> |
| <span data-ttu-id="4918e-148">卡</span><span class="sxs-lookup"><span data-stu-id="4918e-148">Cards</span></span> | <span data-ttu-id="4918e-149">✖</span><span class="sxs-lookup"><span data-stu-id="4918e-149">✖</span></span> | <span data-ttu-id="4918e-150">✔</span><span class="sxs-lookup"><span data-stu-id="4918e-150">✔</span></span> | <span data-ttu-id="4918e-151">有关支持的[Teams，](~/task-modules-and-cards/cards/cards-reference.md)请参阅卡片参考。</span><span class="sxs-lookup"><span data-stu-id="4918e-151">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards.</span></span> |
| <span data-ttu-id="4918e-152">表情符号</span><span class="sxs-lookup"><span data-stu-id="4918e-152">Emojis</span></span> | <span data-ttu-id="4918e-153">✖</span><span class="sxs-lookup"><span data-stu-id="4918e-153">✖</span></span> | <span data-ttu-id="4918e-154">✔</span><span class="sxs-lookup"><span data-stu-id="4918e-154">✔</span></span> | <span data-ttu-id="4918e-155">Teams UTF-16 支持表情符号，例如 U+1F600 表示表情符号。</span><span class="sxs-lookup"><span data-stu-id="4918e-155">Teams currently supports emojis via UTF-16 such as, U+1F600 for grinning face.</span></span> |
|

<span data-ttu-id="4918e-156">有关自动程序框架支持的机器人交互类型（团队中的机器人基于这些机器人）的信息，请参阅适用于[.NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true)的 Bot Builder [](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) SDK 和适用于 Node.js的 Bot [Builder SDK](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true)文档中有关对话流和相关概念的 Bot Framework 文档。</span><span class="sxs-lookup"><span data-stu-id="4918e-156">For more information on the types of bot interaction supported by the Bot Framework, which bots in teams are based on, see the Bot Framework documentation on [conversation flow](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) and related concepts in the documentation for [the Bot Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) and [the Bot Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true).</span></span>

## <a name="message-formatting"></a><span data-ttu-id="4918e-157">消息格式</span><span class="sxs-lookup"><span data-stu-id="4918e-157">Message formatting</span></span>

<span data-ttu-id="4918e-158">可以设置 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) 的可选属性 `message` ，以控制邮件文本内容的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="4918e-158">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) property of a `message` to control how your message's text content is rendered.</span></span> <span data-ttu-id="4918e-159">有关 [自动程序消息](~/resources/bot-v3/bots-message-format.md) 中支持的格式的详细说明，请参阅邮件格式。</span><span class="sxs-lookup"><span data-stu-id="4918e-159">See [Message formatting](~/resources/bot-v3/bots-message-format.md) for a detailed description of supported formatting in bot messages.</span></span>
<span data-ttu-id="4918e-160">可以设置可选 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) 属性来控制邮件文本内容的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="4918e-160">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="4918e-161">有关团队中文本格式Teams的详细信息，请参阅自动[程序消息中的文本格式](~/resources/bot-v3/bots-text-formats.md)。</span><span class="sxs-lookup"><span data-stu-id="4918e-161">For detailed information on how Teams supports text formatting in teams see [Text formatting in bot messages](~/resources/bot-v3/bots-text-formats.md).</span></span>

<span data-ttu-id="4918e-162">有关邮件中卡片格式设置详细信息，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="4918e-162">For more information on formatting cards in messages, see [Card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="picture-messages"></a><span data-ttu-id="4918e-163">图片消息</span><span class="sxs-lookup"><span data-stu-id="4918e-163">Picture messages</span></span>

<span data-ttu-id="4918e-164">图片通过向邮件添加附件来发送。</span><span class="sxs-lookup"><span data-stu-id="4918e-164">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="4918e-165">有关附件的更多信息，请参阅 [Bot Framework 文档](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="4918e-165">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true).</span></span>

<span data-ttu-id="4918e-166">图片最多为 1024×1024 和 1 MB（PNG、JPEG 或 GIF 格式）;不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="4918e-166">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="4918e-167">建议您使用 XML 指定每个图像的高度和宽度。</span><span class="sxs-lookup"><span data-stu-id="4918e-167">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="4918e-168">如果使用 Markdown，图像大小默认为 256×256。</span><span class="sxs-lookup"><span data-stu-id="4918e-168">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="4918e-169">例如：</span><span class="sxs-lookup"><span data-stu-id="4918e-169">For example:</span></span>

* <span data-ttu-id="4918e-170">使用 `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="4918e-170">Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="4918e-171">请勿使用 `![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="4918e-171">Don't use `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="receiving-messages&quot;></a><span data-ttu-id=&quot;4918e-172&quot;>接收邮件</span><span class=&quot;sxs-lookup&quot;><span data-stu-id=&quot;4918e-172&quot;>Receiving messages</span></span>

<span data-ttu-id=&quot;4918e-173&quot;>根据声明的范围，自动程序可以在以下上下文中接收消息：</span><span class=&quot;sxs-lookup&quot;><span data-stu-id=&quot;4918e-173&quot;>Depending on which scopes are declared, your bot can receive messages in the following contexts:</span></span>

* <span data-ttu-id=&quot;4918e-174&quot;>**个人聊天** 用户只需在聊天历史记录中选择已添加的聊天机器人，或在新聊天的&quot;目标：&quot;框中键入其名称或应用 ID，即可与机器人在私人对话中进行交互。</span><span class=&quot;sxs-lookup&quot;><span data-stu-id=&quot;4918e-174&quot;>**personal chat** Users can interact in a private conversation with a bot by simply selecting the added bot in the chat history, or typing its name or app ID in the To: box on a new chat.</span></span>
* <span data-ttu-id=&quot;4918e-175&quot;>**频道** 可以将机器人 (&quot;@_botname_") 如果已添加到团队，可以在频道中提及它。</span><span class="sxs-lookup"><span data-stu-id="4918e-175">**Channels** A bot can be mentioned ("@_botname_") in a channel if it has been added to the team.</span></span> <span data-ttu-id="4918e-176">请注意，频道中对自动程序的其他回复需要提及机器人。</span><span class="sxs-lookup"><span data-stu-id="4918e-176">Note that additional replies to a bot in a channel require mentioning the bot.</span></span> <span data-ttu-id="4918e-177">它将不会在未提及的回复中回复。</span><span class="sxs-lookup"><span data-stu-id="4918e-177">It will not respond to replies where it is not mentioned.</span></span>

<span data-ttu-id="4918e-178">对于传入消息，机器人会收到类型 为 [的 Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) 对象 `messageType: message` 。</span><span class="sxs-lookup"><span data-stu-id="4918e-178">For incoming messages, your bot receives an [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object of type `messageType: message`.</span></span> <span data-ttu-id="4918e-179">虽然对象可以包含其他类型的信息（如发送到机器人的频道更新），但类型 `Activity` 表示机器人[](~/resources/bot-v3/bots-notifications.md#channel-updates) `message` 和用户之间的通信。</span><span class="sxs-lookup"><span data-stu-id="4918e-179">Although the `Activity` object can contain other types of information, like [channel updates](~/resources/bot-v3/bots-notifications.md#channel-updates) sent to your bot, the `message` type represents communication between bot and user.</span></span>

<span data-ttu-id="4918e-180">自动程序会收到包含用户消息的有效负载，以及有关用户的其他信息、消息源和Teams `Text` 信息。</span><span class="sxs-lookup"><span data-stu-id="4918e-180">Your bot receives a payload that contains the user message `Text` as well as other information about the user, the source of the message, and Teams information.</span></span> <span data-ttu-id="4918e-181">注意：</span><span class="sxs-lookup"><span data-stu-id="4918e-181">Of note:</span></span>

* <span data-ttu-id="4918e-182">`timestamp` 使用协调世界时 UTC 格式 (邮件) 。</span><span class="sxs-lookup"><span data-stu-id="4918e-182">`timestamp` The date and time of the message in Coordinated Universal Time (UTC).</span></span>
* <span data-ttu-id="4918e-183">`localTimestamp` 发件人时区的邮件日期和时间。</span><span class="sxs-lookup"><span data-stu-id="4918e-183">`localTimestamp` The date and time of the message in the time zone of the sender.</span></span>
* <span data-ttu-id="4918e-184">`channelId` 始终为"msteams"。</span><span class="sxs-lookup"><span data-stu-id="4918e-184">`channelId` Always "msteams".</span></span> <span data-ttu-id="4918e-185">这是指自动程序框架频道，而不是团队频道。</span><span class="sxs-lookup"><span data-stu-id="4918e-185">This refers to a bot framework channel, not a teams channel.</span></span>
* <span data-ttu-id="4918e-186">`from.id` 自动程序的用户的唯一加密 ID;如果应用需要存储用户数据，则适合用作密钥。</span><span class="sxs-lookup"><span data-stu-id="4918e-186">`from.id` A unique and encrypted ID for that user for your bot; suitable as a key if your app needs to store user data.</span></span> <span data-ttu-id="4918e-187">它对于自动程序来说是唯一的，不能以任何有意义的方式直接在自动程序实例外部使用来标识该用户。</span><span class="sxs-lookup"><span data-stu-id="4918e-187">It is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>
* <span data-ttu-id="4918e-188">`channelData.tenant.id` 用户的租户 ID。</span><span class="sxs-lookup"><span data-stu-id="4918e-188">`channelData.tenant.id` The tenant ID for the user.</span></span>

> [!NOTE]
> <span data-ttu-id="4918e-189">`from.id` 对于自动程序是唯一的，不能以任何有意义的方式直接在自动程序实例外部使用来标识该用户。</span><span class="sxs-lookup"><span data-stu-id="4918e-189">`from.id` is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>

## <a name="combining-channel-and-private-interactions-with-your-bot"></a><span data-ttu-id="4918e-190">将频道和私人交互与机器人结合使用</span><span class="sxs-lookup"><span data-stu-id="4918e-190">Combining channel and private interactions with your bot</span></span>

<span data-ttu-id="4918e-191">当在频道中交互时，自动程序应智能地与用户离线进行某些对话。</span><span class="sxs-lookup"><span data-stu-id="4918e-191">When interacting in a channel, your bot should be smart about taking certain conversations offline with a user.</span></span> <span data-ttu-id="4918e-192">例如，假设用户尝试协调复杂的任务，例如与一组团队成员进行日程安排。</span><span class="sxs-lookup"><span data-stu-id="4918e-192">For instance, suppose a user is trying to coordinate a complex task, such as scheduling with a set of team members.</span></span> <span data-ttu-id="4918e-193">请考虑向用户发送个人聊天消息，而不是让整个交互序列对频道可见。</span><span class="sxs-lookup"><span data-stu-id="4918e-193">Rather than have the entire sequence of interactions visible to the channel, consider sending a personal chat message to the user.</span></span> <span data-ttu-id="4918e-194">自动程序应该能够在个人和频道对话之间轻松转换用户，而不会丢失状态。</span><span class="sxs-lookup"><span data-stu-id="4918e-194">Your bot should be able to easily transition the user between personal and channel conversations without losing state.</span></span>

> [!NOTE]
><span data-ttu-id="4918e-195">在交互完成时，不要忘记更新频道以通知其他团队成员。</span><span class="sxs-lookup"><span data-stu-id="4918e-195">Don’t forget to update the channel when the interaction is complete to notify the other team members.</span></span>

## <a name="full-inbound-schema-example"></a><span data-ttu-id="4918e-196">完整的入站架构示例</span><span class="sxs-lookup"><span data-stu-id="4918e-196">Full inbound schema example</span></span>

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot",
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

> [!NOTE]
> <span data-ttu-id="4918e-197">入站邮件的文本字段有时包含提及。</span><span class="sxs-lookup"><span data-stu-id="4918e-197">The text field for inbound messages sometimes contains mentions.</span></span> <span data-ttu-id="4918e-198">请务必正确检查并去除这些复选框。</span><span class="sxs-lookup"><span data-stu-id="4918e-198">Be sure to properly check and strip those.</span></span> <span data-ttu-id="4918e-199">有关详细信息，请参阅 [提及](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)。</span><span class="sxs-lookup"><span data-stu-id="4918e-199">For more information, see [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="4918e-200">Teams频道数据</span><span class="sxs-lookup"><span data-stu-id="4918e-200">Teams channel data</span></span>

<span data-ttu-id="4918e-201">对象 `channelData` 包含Teams特定的信息，是团队和频道的明确来源。</span><span class="sxs-lookup"><span data-stu-id="4918e-201">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="4918e-202">应缓存这些 ID，并用作本地存储的密钥。</span><span class="sxs-lookup"><span data-stu-id="4918e-202">You should cache and use these ids as keys for local storage.</span></span>

<span data-ttu-id="4918e-203">`channelData`对象不包含在个人对话中的邮件中，因为这些事件发生在任何频道之外。</span><span class="sxs-lookup"><span data-stu-id="4918e-203">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="4918e-204">发送给自动程序的活动中的典型 channelData 对象包含以下信息：</span><span class="sxs-lookup"><span data-stu-id="4918e-204">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="4918e-205">`eventType`Teams事件类型;仅在通道修改[事件的情况下传递](~/resources/bot-v3/bots-notifications.md#channel-updates)。</span><span class="sxs-lookup"><span data-stu-id="4918e-205">`eventType` Teams event type; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="4918e-206">`tenant.id`Azure Active Directory租户 ID;在所有上下文中传递。</span><span class="sxs-lookup"><span data-stu-id="4918e-206">`tenant.id` Azure Active Directory tenant ID; passed in all contexts.</span></span>
* <span data-ttu-id="4918e-207">`team` 仅在频道上下文中传递，而不是在个人聊天中传递。</span><span class="sxs-lookup"><span data-stu-id="4918e-207">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="4918e-208">`id` 频道的 GUID。</span><span class="sxs-lookup"><span data-stu-id="4918e-208">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="4918e-209">`name` 团队名称;仅在团队重命名 [事件的情况下传递](~/resources/bot-v3/bots-notifications.md#team-name-updates)。</span><span class="sxs-lookup"><span data-stu-id="4918e-209">`name` Name of the team; passed only in cases of [team rename events](~/resources/bot-v3/bots-notifications.md#team-name-updates).</span></span>
* <span data-ttu-id="4918e-210">`channel` 仅在提到自动程序时在频道上下文中传递，或针对团队中已添加自动程序的团队中的事件传递。</span><span class="sxs-lookup"><span data-stu-id="4918e-210">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added.</span></span>
  * <span data-ttu-id="4918e-211">`id` 频道的 GUID。</span><span class="sxs-lookup"><span data-stu-id="4918e-211">`id` GUID for the channel.</span></span>
  * <span data-ttu-id="4918e-212">`name` 频道名称;仅在通道修改 [事件的情况下传递](~/resources/bot-v3/bots-notifications.md#channel-updates)。</span><span class="sxs-lookup"><span data-stu-id="4918e-212">`name` Channel name; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="4918e-213">`channelData.teamsTeamId` 已弃用。</span><span class="sxs-lookup"><span data-stu-id="4918e-213">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="4918e-214">此属性仅包含用于向后兼容。</span><span class="sxs-lookup"><span data-stu-id="4918e-214">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="4918e-215">`channelData.teamsChannelId` 已弃用。</span><span class="sxs-lookup"><span data-stu-id="4918e-215">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="4918e-216">此属性仅包含用于向后兼容。</span><span class="sxs-lookup"><span data-stu-id="4918e-216">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="4918e-217">channelCreated 事件 (channelCreated 事件示例) </span><span class="sxs-lookup"><span data-stu-id="4918e-217">Example channelData object (channelCreated event)</span></span>

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

### <a name="net-example"></a><span data-ttu-id="4918e-218">.NET 示例</span><span class="sxs-lookup"><span data-stu-id="4918e-218">.NET example</span></span>

<span data-ttu-id="4918e-219">[Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)包提供了一个专用对象，该对象公开用于访问Teams `TeamsChannelData` 特定信息的属性。</span><span class="sxs-lookup"><span data-stu-id="4918e-219">The [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package provides a specialized `TeamsChannelData` object, which exposes properties to access Teams-specific information.</span></span>

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a><span data-ttu-id="4918e-220">发送对邮件的答复</span><span class="sxs-lookup"><span data-stu-id="4918e-220">Sending replies to messages</span></span>

<span data-ttu-id="4918e-221">若要回复现有邮件，请调用 [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) .NET 或 [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) Node.js。</span><span class="sxs-lookup"><span data-stu-id="4918e-221">To reply to an existing message, call [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) in .NET or [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) in Node.js.</span></span> <span data-ttu-id="4918e-222">Bot Builder SDK 处理所有详细信息。</span><span class="sxs-lookup"><span data-stu-id="4918e-222">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="4918e-223">如果选择使用 REST API，还可以调用 [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) 终结点。</span><span class="sxs-lookup"><span data-stu-id="4918e-223">If you choose to use the REST API, you can also call the [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) endpoint.</span></span>

<span data-ttu-id="4918e-224">邮件内容本身可以包含简单的文本，也可以包含一些 Bot Framework 提供的 [卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="4918e-224">The message content itself can contain simple text or some of the Bot Framework supplied [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="4918e-225">请注意，在出站架构中，应始终使用与收到的 `serviceUrl` 相同。</span><span class="sxs-lookup"><span data-stu-id="4918e-225">Please note that in your outbound schema you should always use the same `serviceUrl` as the one you received.</span></span> <span data-ttu-id="4918e-226">请注意，的值往往 `serviceUrl` 很稳定，但可能会更改。</span><span class="sxs-lookup"><span data-stu-id="4918e-226">Be aware that the value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="4918e-227">当新消息到达时，机器人应验证其存储的值 `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="4918e-227">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

## <a name="updating-messages"></a><span data-ttu-id="4918e-228">更新邮件</span><span class="sxs-lookup"><span data-stu-id="4918e-228">Updating messages</span></span>

<span data-ttu-id="4918e-229">自动程序可以在发送邮件后动态更新内联消息，而不是让消息成为数据的静态快照。</span><span class="sxs-lookup"><span data-stu-id="4918e-229">Rather than have your messages be static snapshots of data, your bot can dynamically update messages inline after sending them.</span></span> <span data-ttu-id="4918e-230">你可以将动态消息更新用于轮询更新、在按下按钮后修改可用操作，或者任何其他异步状态更改。</span><span class="sxs-lookup"><span data-stu-id="4918e-230">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="4918e-231">新邮件的类型不需要与原始邮件匹配。</span><span class="sxs-lookup"><span data-stu-id="4918e-231">The new message need not match the original in type.</span></span> <span data-ttu-id="4918e-232">例如，如果原始邮件包含附件，则新邮件可以是简单的短信。</span><span class="sxs-lookup"><span data-stu-id="4918e-232">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

> [!NOTE]
> <span data-ttu-id="4918e-233">只能更新在单附件邮件和盘车布局中发送的内容。</span><span class="sxs-lookup"><span data-stu-id="4918e-233">You can update only content sent in single-attachment messages and carousel layouts.</span></span> <span data-ttu-id="4918e-234">不支持在列表布局中发布具有多个附件的邮件更新。</span><span class="sxs-lookup"><span data-stu-id="4918e-234">Posting updates to messages with multiple attachments in list layout is not supported.</span></span>

### <a name="rest-api"></a><span data-ttu-id="4918e-235">REST API</span><span class="sxs-lookup"><span data-stu-id="4918e-235">REST API</span></span>

<span data-ttu-id="4918e-236">若要发出消息更新，只需使用给定的活动 ID 对终结点执行 PUT `/v3/conversations/<conversationId>/activities/<activityId>/` 请求。</span><span class="sxs-lookup"><span data-stu-id="4918e-236">To issue a message update, simply perform a PUT request against the `/v3/conversations/<conversationId>/activities/<activityId>/` endpoint using a given activity ID.</span></span> <span data-ttu-id="4918e-237">若要完成此方案，您应缓存原始 POST 调用返回的活动 ID。</span><span class="sxs-lookup"><span data-stu-id="4918e-237">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a><span data-ttu-id="4918e-238">.NET 示例</span><span class="sxs-lookup"><span data-stu-id="4918e-238">.NET example</span></span>

<span data-ttu-id="4918e-239">可以使用 Bot Builder SDK 中的 方法 `UpdateActivityAsync` 更新现有邮件。</span><span class="sxs-lookup"><span data-stu-id="4918e-239">You can use the `UpdateActivityAsync` method in the Bot Builder SDK to update an existing message.</span></span>

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
  if (activity.Type == ActivityTypes.Message)
  {
    ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
    Activity reply = activity.CreateReply($"You sent {activity.Text} which was {activity.Text.Length} characters");
    var msgToUpdate = await connector.Conversations.ReplyToActivityAsync(reply);
    Activity updatedReply = activity.CreateReply($"This is an updated message");
    await connector.Conversations.UpdateActivityAsync(reply.Conversation.Id, msgToUpdate.Id, updatedReply);
  }
}
```

### <a name="nodejs-example"></a><span data-ttu-id="4918e-240">Node.js示例</span><span class="sxs-lookup"><span data-stu-id="4918e-240">Node.js example</span></span>

<span data-ttu-id="4918e-241">可以使用 Bot Builder SDK 中的 方法 `session.connector.update` 更新现有邮件。</span><span class="sxs-lookup"><span data-stu-id="4918e-241">You can use the `session.connector.update` method in the Bot Builder SDK to update an existing message.</span></span>

```javascript
function sendCardUpdate(bot, session, originalMessage, address) {

  var origAttachment = originalMessage.data.attachments[0];
  origAttachment.content.subtitle = 'Assigned to Larry Jin';

  var updatedMsg = new builder.Message()
    .address(address)
    .textFormat(builder.TextFormat.markdown)
    .addAttachment(origAttachment)
    .toMessage();

  session.connector.update(updatedMsg, function(err, addresses) {
    if (err) {
      console.log(`Could not update the message`);
    }
  });
}
```

## <a name="starting-a-conversation-proactive-messaging"></a><span data-ttu-id="4918e-242">启动对话 (主动消息传递) </span><span class="sxs-lookup"><span data-stu-id="4918e-242">Starting a conversation (proactive messaging)</span></span>

<span data-ttu-id="4918e-243">你可以与用户创建个人对话，或在频道中为团队机器人启动新的回复链。</span><span class="sxs-lookup"><span data-stu-id="4918e-243">You can create a personal conversation with a user or start a new reply chain in a channel for your team bot.</span></span> <span data-ttu-id="4918e-244">这使你可以向用户发送消息，而无需让他们首先与机器人联系。</span><span class="sxs-lookup"><span data-stu-id="4918e-244">This lets you to message your user or users without having them first initiate contact with your bot.</span></span> <span data-ttu-id="4918e-245">有关详细信息，请参阅下列主题：</span><span class="sxs-lookup"><span data-stu-id="4918e-245">For more information, see the following topics:</span></span>

<span data-ttu-id="4918e-246">有关 [自动程序启动的对话](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) 的更多常规信息，请参阅自动程序主动消息传递。</span><span class="sxs-lookup"><span data-stu-id="4918e-246">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more general information on conversations started by bots.</span></span>

## <a name="deleting-messages"></a><span data-ttu-id="4918e-247">删除邮件</span><span class="sxs-lookup"><span data-stu-id="4918e-247">Deleting messages</span></span>

<span data-ttu-id="4918e-248">可以使用 BotBuilder SDK 中的 connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) 方法 [删除邮件](/bot-framework/bot-builder-overview-getstarted)。</span><span class="sxs-lookup"><span data-stu-id="4918e-248">Messages can be deleted using the connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) method in the [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).</span></span>

```typescript
bot.dialog('BotDeleteMessage', function (session: builder.Session) {
  var msg = new teams.TeamsMessage(session).text("Bot will delete this message in 5 sec.")
  bot.send(msg, function (err, response) {
    if (err) {
      console.log(err);
      session.endDialog();
    }

    console.log('Proactive message response:');
    console.log(response);
    console.log('---------------------------------------------------')
    setTimeout(function () {
      var activityId: string = null;
      var messageAddress: builder.IChatConnectorAddress = null;
      if (response[0]){
        messageAddress = response[0];
        activityId = messageAddress.id;
      }

      if (activityId == null)
      {
        console.log('Message failed to send.');
        session.endDialog();
        return;
      }

      // Bot delete message
      let address: builder.IChatConnectorAddress  = {
        channelId: 'msteams',
        user: messageAddress.user,
        bot: messageAddress.bot,
        id : activityId,
        serviceUrl : (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
        conversation: {
          id: session.message.address.conversation.id
        }
      };

      connector.delete(address, function (err) {
        if (err)
        {
          console.log(err);
        }
        else
        {
          console.log("Message: " + activityId + " deleted successfully.");
        }

        // Try editing deleted message would fail
        var newMsg = new builder.Message().address(address).text("To edit message.");
        connector.update(newMsg.toMessage(), function (err, address) {
          if (err)
          {
            console.log(err);
            console.log('Deleted message can not be edited.');
          }
          else
          {
            console.log("There is something wrong. Message: " + activityId + " edited successfully.");
            console.log(address);
          }

          session.endDialog();
        });
      });
    }, 5000);
  });
})
```
