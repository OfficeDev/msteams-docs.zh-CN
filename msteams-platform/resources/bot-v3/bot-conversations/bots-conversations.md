---
title: 使用 bot 发送和接收邮件
description: 介绍如何使用 Microsoft 团队中的 bot 发送和接收邮件
keywords: 工作组 bot 消息
ms.date: 05/20/2019
ms.openlocfilehash: 4a15bb9b4ae8c0ede3214d3a534649e2769baf6e
ms.sourcegitcommit: 2b1fd50466d807869fd173371ba7dfd82a0064ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2020
ms.locfileid: "44801133"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a><span data-ttu-id="c9c8f-104">与 Microsoft 团队 bot 进行对话</span><span class="sxs-lookup"><span data-stu-id="c9c8f-104">Have a conversation with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="c9c8f-105">对话是在你的 bot 和一个或多个用户之间发送的一系列邮件。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-105">A conversation is a series of messages sent between your bot and one or more users.</span></span> <span data-ttu-id="c9c8f-106">团队中有三种对话（也称为 "作用域"）：</span><span class="sxs-lookup"><span data-stu-id="c9c8f-106">There are three kinds of conversations (also called scopes) in Teams:</span></span>

* <span data-ttu-id="c9c8f-107">`teams`也称为频道对话，对频道的所有成员可见。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-107">`teams` Also called channel conversations, visible to all members of the channel.</span></span>
* <span data-ttu-id="c9c8f-108">`personal`Bot 和单个用户之间的对话。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-108">`personal` Conversations between bots and a single user.</span></span>
* <span data-ttu-id="c9c8f-109">`groupChat`在 bot 和两个或更多用户之间聊天。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-109">`groupChat` Chat between a bot and two or more users.</span></span>

<span data-ttu-id="c9c8f-110">Bot 的行为略有不同，具体取决于它涉及的对话类型：</span><span class="sxs-lookup"><span data-stu-id="c9c8f-110">A bot behaves slightly differently depending on what kind of conversation it is involved in:</span></span>

* <span data-ttu-id="c9c8f-111">[频道和分组聊天对话中的 bot](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)要求用户在频道中提及机器人以调用它。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-111">[Bots in channel and group chat conversations](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) require the user to @ mention the bot to invoke it in a channel.</span></span>
* <span data-ttu-id="c9c8f-112">[单个用户对话中的 bot](~/resources/bot-v3/bot-conversations/bots-conv-personal.md)不需要 @ 提及-用户只需键入即可。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-112">[Bots in single user conversations](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) do not require an @ mention -  the user can just type.</span></span>

<span data-ttu-id="c9c8f-113">为了使机器人能够在特定范围内工作，应将其列为清单中支持该范围。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-113">In order for the bot to work in a particular scope it should be listed as supporting that scope in the manifest.</span></span> <span data-ttu-id="c9c8f-114">在[清单参考](~/resources/schema/manifest-schema.md)中定义和进一步讨论范围。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-114">Scopes are defined and discussed further in the [Manifest Reference](~/resources/schema/manifest-schema.md).</span></span>

## <a name="proactive-messages"></a><span data-ttu-id="c9c8f-115">主动消息</span><span class="sxs-lookup"><span data-stu-id="c9c8f-115">Proactive messages</span></span>

<span data-ttu-id="c9c8f-116">Bot 可以参与对话或启动对话。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-116">Bots can participate in a conversation or initiate one.</span></span> <span data-ttu-id="c9c8f-117">大多数通信是对另一封邮件的响应。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-117">Most communication is in response to another message.</span></span> <span data-ttu-id="c9c8f-118">如果 bot 启动对话，则它称为*主动消息*。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-118">If a bot initiates a conversation it is called a *proactive message*.</span></span> <span data-ttu-id="c9c8f-119">示例包括：</span><span class="sxs-lookup"><span data-stu-id="c9c8f-119">Examples include:</span></span>

* <span data-ttu-id="c9c8f-120">欢迎邮件</span><span class="sxs-lookup"><span data-stu-id="c9c8f-120">Welcome messages</span></span>
* <span data-ttu-id="c9c8f-121">事件通知</span><span class="sxs-lookup"><span data-stu-id="c9c8f-121">Event notifications</span></span>
* <span data-ttu-id="c9c8f-122">轮询邮件</span><span class="sxs-lookup"><span data-stu-id="c9c8f-122">Polling messages</span></span>

## <a name="conversation-basics"></a><span data-ttu-id="c9c8f-123">对话基础知识</span><span class="sxs-lookup"><span data-stu-id="c9c8f-123">Conversation basics</span></span>

<span data-ttu-id="c9c8f-124">每封邮件都是一 `Activity` 种类型的对象 `messageType: message` 。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-124">Each message is an `Activity` object of type `messageType: message`.</span></span> <span data-ttu-id="c9c8f-125">当用户发送邮件时，工作组会将邮件发送到你的 bot。具体来说，它会将 JSON 对象发送到你的 bot 的邮件终结点。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-125">When a user sends a message, Teams posts the message to your bot; specifically, it sends a JSON object to your bot's messaging endpoint.</span></span> <span data-ttu-id="c9c8f-126">你的 bot 将检查邮件以确定其类型并相应地做出响应。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-126">Your bot examines the message to determine its type and responds accordingly.</span></span>

<span data-ttu-id="c9c8f-127">Bot 还支持事件样式的邮件。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-127">Bots also support event-style messages.</span></span> <span data-ttu-id="c9c8f-128">有关详细信息，请参阅[在 Microsoft 团队中处理 bot 事件](~/resources/bot-v3/bots-notifications.md)。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-128">See [Handle bot events in Microsoft Teams](~/resources/bot-v3/bots-notifications.md) for more details.</span></span> <span data-ttu-id="c9c8f-129">目前不支持语音。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-129">Speech is currently not supported.</span></span>

<span data-ttu-id="c9c8f-130">邮件在所有作用域中的作用最大，但在 UI 中访问 bot 的方式与在需要了解的幕后的差异方面存在差异。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-130">Messages are for the most part the same in across all scopes, but there are differences in how the bot is accessed in the UI and differences behind the scenes which you will need to know about.</span></span>

<span data-ttu-id="c9c8f-131">基本对话通过 Bot 框架连接器（单个 REST API）处理，使你的 bot 能够与团队和其他频道进行通信。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-131">Basic conversation is handled through the Bot Framework Connector, a single REST API to enable your bot to communicate with Teams and other channels.</span></span> <span data-ttu-id="c9c8f-132">机器人生成器 SDK 提供了轻松访问此 API 的功能、用于管理对话流和状态的附加功能，以及用于集成认知服务（如自然语言处理（NLP））的简单方法。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-132">The Bot Builder SDK provides easy access to this API, additional functionality to manage conversation flow and state, and simple ways to incorporate cognitive services such as natural language processing (NLP).</span></span>

## <a name="message-content"></a><span data-ttu-id="c9c8f-133">邮件内容</span><span class="sxs-lookup"><span data-stu-id="c9c8f-133">Message content</span></span>

<span data-ttu-id="c9c8f-134">你的 bot 可以发送多信息文本、图片和卡片。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-134">Your bot can send rich text, pictures, and cards.</span></span> <span data-ttu-id="c9c8f-135">用户可以向你的 bot 发送丰富的文本和图片。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-135">Users can send rich text and pictures to your bot.</span></span> <span data-ttu-id="c9c8f-136">您可以在你的 bot 的 Microsoft 团队设置页中指定你的 bot 可以处理的内容类型。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-136">You can specify the type of content your bot can handle in the Microsoft Teams settings page for your bot.</span></span>

| <span data-ttu-id="c9c8f-137">Format</span><span class="sxs-lookup"><span data-stu-id="c9c8f-137">Format</span></span> | <span data-ttu-id="c9c8f-138">从用户到 bot</span><span class="sxs-lookup"><span data-stu-id="c9c8f-138">From user to bot</span></span>  | <span data-ttu-id="c9c8f-139">从 bot 到用户</span><span class="sxs-lookup"><span data-stu-id="c9c8f-139">From bot to user</span></span> |  <span data-ttu-id="c9c8f-140">注释</span><span class="sxs-lookup"><span data-stu-id="c9c8f-140">Notes</span></span> |
| --- | :---: | :---: | --- |
| <span data-ttu-id="c9c8f-141">格式文本 </span><span class="sxs-lookup"><span data-stu-id="c9c8f-141">Rich text</span></span> | <span data-ttu-id="c9c8f-142">✔</span><span class="sxs-lookup"><span data-stu-id="c9c8f-142">✔</span></span> | <span data-ttu-id="c9c8f-143">✔</span><span class="sxs-lookup"><span data-stu-id="c9c8f-143">✔</span></span> |  |
| <span data-ttu-id="c9c8f-144">图片</span><span class="sxs-lookup"><span data-stu-id="c9c8f-144">Pictures</span></span> | <span data-ttu-id="c9c8f-145">✔</span><span class="sxs-lookup"><span data-stu-id="c9c8f-145">✔</span></span> | <span data-ttu-id="c9c8f-146">✔</span><span class="sxs-lookup"><span data-stu-id="c9c8f-146">✔</span></span> | <span data-ttu-id="c9c8f-147">最大1024×1024和 1 MB，PNG、JPEG 或 GIF 格式;不支持动态 GIF</span><span class="sxs-lookup"><span data-stu-id="c9c8f-147">Maximum 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF are not supported</span></span> |
| <span data-ttu-id="c9c8f-148">卡</span><span class="sxs-lookup"><span data-stu-id="c9c8f-148">Cards</span></span> | <span data-ttu-id="c9c8f-149">✖</span><span class="sxs-lookup"><span data-stu-id="c9c8f-149">✖</span></span> | <span data-ttu-id="c9c8f-150">✔</span><span class="sxs-lookup"><span data-stu-id="c9c8f-150">✔</span></span> | <span data-ttu-id="c9c8f-151">有关支持的卡片，请参阅[团队卡片参考](~/task-modules-and-cards/cards/cards-reference.md)</span><span class="sxs-lookup"><span data-stu-id="c9c8f-151">See the [Teams Card Reference](~/task-modules-and-cards/cards/cards-reference.md) for supported cards</span></span> |
| <span data-ttu-id="c9c8f-152">表情符号</span><span class="sxs-lookup"><span data-stu-id="c9c8f-152">Emojis</span></span> | <span data-ttu-id="c9c8f-153">✖</span><span class="sxs-lookup"><span data-stu-id="c9c8f-153">✖</span></span> | <span data-ttu-id="c9c8f-154">✔</span><span class="sxs-lookup"><span data-stu-id="c9c8f-154">✔</span></span> | <span data-ttu-id="c9c8f-155">团队目前支持通过 UTF-16 进行的表情符号（例如，U + 1F600 for grinning 脸）</span><span class="sxs-lookup"><span data-stu-id="c9c8f-155">Teams currently supports emojis via UTF-16 (such as U+1F600 for grinning face)</span></span> |
|

<span data-ttu-id="c9c8f-156">有关 Bot 框架（团队中的自动程序基于）支持的 bot 交互类型的详细信息，请参阅用于[.net 的 Bot 生成器 sdk](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0)的文档中的 "bot 框架" 和 "相关概念" 的 "Bot" 框架[文档，以及](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0)[适用于 Node.js的 bot 生成器 sdk ](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0)。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-156">For more information on the types of bot interaction supported by the Bot Framework (which bots in teams are based on), see the Bot Framework documentation on [conversation flow](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0) and related concepts in the documentation for [the Bot Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0) and [the Bot Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0).</span></span>

## <a name="message-formatting"></a><span data-ttu-id="c9c8f-157">消息格式</span><span class="sxs-lookup"><span data-stu-id="c9c8f-157">Message formatting</span></span>

<span data-ttu-id="c9c8f-158">您可以设置的可选 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) 属性 `message` 来控制邮件的文本内容的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-158">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) property of a `message` to control how your message's text content is rendered.</span></span> <span data-ttu-id="c9c8f-159">有关 bot 邮件中支持的格式的详细说明，请参阅[邮件格式](~/resources/bot-v3/bots-message-format.md)。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-159">See [Message formatting](~/resources/bot-v3/bots-message-format.md) for a detailed description of supported formatting in bot messages.</span></span>
<span data-ttu-id="c9c8f-160">您可以设置可选 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) 属性以控制邮件的文本内容的呈现方式。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-160">You can set the optional [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) property to control how your message's text content is rendered.</span></span>

<span data-ttu-id="c9c8f-161">有关团队如何在团队中支持文本格式的详细信息，请参阅[bot 邮件中的文本格式](~/resources/bot-v3/bots-text-formats.md)。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-161">For detailed information on how Teams supports text formatting in teams see [Text formatting in bot messages](~/resources/bot-v3/bots-text-formats.md).</span></span>

<span data-ttu-id="c9c8f-162">有关在邮件中设置卡片格式的信息，请参阅[卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-162">For information on formatting cards in messages, see [Card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="picture-messages"></a><span data-ttu-id="c9c8f-163">图片邮件</span><span class="sxs-lookup"><span data-stu-id="c9c8f-163">Picture messages</span></span>

<span data-ttu-id="c9c8f-164">通过将附件添加到邮件来发送图片。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-164">Pictures are sent by adding attachments to a message.</span></span> <span data-ttu-id="c9c8f-165">您可以在[Bot 框架文档](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0)中找到有关附件的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-165">You can find more information on attachments in the [Bot Framework documentation](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0).</span></span>

<span data-ttu-id="c9c8f-166">图片最多可以为1024×1024和 1 MB （PNG、JPEG 或 GIF 格式）;不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-166">Pictures can be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not supported.</span></span>

<span data-ttu-id="c9c8f-167">建议使用 XML 指定每个图像的高度和宽度。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-167">We recommend that you specify the height and width of each image by using XML.</span></span> <span data-ttu-id="c9c8f-168">如果使用 Markdown，则图像大小默认为256×256。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-168">If you use Markdown, the image size defaults to 256×256.</span></span> <span data-ttu-id="c9c8f-169">例如：</span><span class="sxs-lookup"><span data-stu-id="c9c8f-169">For example:</span></span>

* <span data-ttu-id="c9c8f-170">改用`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span><span class="sxs-lookup"><span data-stu-id="c9c8f-170">Use `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`</span></span>
* <span data-ttu-id="c9c8f-171">请勿使用`![Duck on a rock](http://aka.ms/Fo983c)`</span><span class="sxs-lookup"><span data-stu-id="c9c8f-171">Don't use `![Duck on a rock](http://aka.ms/Fo983c)`</span></span>

## <a name="receiving-messages"></a><span data-ttu-id="c9c8f-172">接收邮件</span><span class="sxs-lookup"><span data-stu-id="c9c8f-172">Receiving messages</span></span>

<span data-ttu-id="c9c8f-173">根据声明的作用域，你的 bot 可以在以下上下文中接收邮件：</span><span class="sxs-lookup"><span data-stu-id="c9c8f-173">Depending on which scopes are declared, your bot can receive messages in the following contexts:</span></span>

* <span data-ttu-id="c9c8f-174">**个人聊天**用户可以通过在聊天历史记录中选择添加的自动程序，或在新聊天中的 "到：" 框中键入其名称或应用 ID，在私人对话中与机器人进行交互。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-174">**personal chat** Users can interact in a private conversation with a bot by simply selecting the added bot in the chat history, or typing its name or app ID in the To: box on a new chat.</span></span>
* <span data-ttu-id="c9c8f-175">**通道**如果已将 bot 添加到团队，则可以在频道中提及 bot （"@_botname_"）。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-175">**Channels** A bot can be mentioned ("@_botname_") in a channel if it has been added to the team.</span></span> <span data-ttu-id="c9c8f-176">请注意，频道中的 bot 的其他回复需要提及机器人。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-176">Note that additional replies to a bot in a channel require mentioning the bot.</span></span> <span data-ttu-id="c9c8f-177">它不会对未提到答复的答复做出响应。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-177">It will not respond to replies where it is not mentioned.</span></span>

<span data-ttu-id="c9c8f-178">对于传入的邮件，你的 bot 接收到一个 [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) 类型的对象 `messageType: message` 。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-178">For incoming messages, your bot receives an [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0) object of type `messageType: message`.</span></span> <span data-ttu-id="c9c8f-179">尽管该 `Activity` 对象可以包含其他类型的信息（如发送给你的 bot 的[频道更新](~/resources/bot-v3/bots-notifications.md#channel-updates)），但 `message` 类型表示 bot 和用户之间的通信。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-179">Although the `Activity` object can contain other types of information, like [channel updates](~/resources/bot-v3/bots-notifications.md#channel-updates) sent to your bot, the `message` type represents communication between bot and user.</span></span>

<span data-ttu-id="c9c8f-180">你的 bot 将接收包含用户消息的有效负载 `Text` ，以及有关用户的其他信息、邮件源和团队信息。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-180">Your bot receives a payload that contains the user message `Text` as well as other information about the user, the source of the message, and Teams information.</span></span> <span data-ttu-id="c9c8f-181">注意：</span><span class="sxs-lookup"><span data-stu-id="c9c8f-181">Of note:</span></span>

* <span data-ttu-id="c9c8f-182">`timestamp`邮件的日期和时间（采用协调通用时间（UTC））</span><span class="sxs-lookup"><span data-stu-id="c9c8f-182">`timestamp` The date and time of the message in Coordinated Universal Time (UTC)</span></span>
* <span data-ttu-id="c9c8f-183">`localTimestamp`发件人时区中邮件的日期和时间</span><span class="sxs-lookup"><span data-stu-id="c9c8f-183">`localTimestamp` The date and time of the message in the time zone of the sender</span></span>
* <span data-ttu-id="c9c8f-184">`channelId`始终为 "msteams"。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-184">`channelId` Always "msteams".</span></span> <span data-ttu-id="c9c8f-185">这指的是 bot 框架通道，而不是团队频道。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-185">This refers to a bot framework channel, not a teams channel.</span></span>
* <span data-ttu-id="c9c8f-186">`from.id`该用户对你的 bot 的唯一且加密的 ID;如果您的应用程序需要存储用户数据，则适用于键。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-186">`from.id` A unique and encrypted ID for that user for your bot; suitable as a key if your app needs to store user data.</span></span> <span data-ttu-id="c9c8f-187">它对于你的 bot 是唯一的，不能以任何有意义的方式直接在机器人实例的外部使用，以标识该用户</span><span class="sxs-lookup"><span data-stu-id="c9c8f-187">It is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user</span></span>
* <span data-ttu-id="c9c8f-188">`channelData.tenant.id`用户的租户 ID。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-188">`channelData.tenant.id` The tenant ID for the user.</span></span>

> [!NOTE]
> <span data-ttu-id="c9c8f-189">`from.id`对于你的 bot 而言是唯一的，不能以任何有意义的方式直接在机器人实例外部使用，以标识该用户。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-189">`from.id` is unique for your bot and cannot be directly used outside your bot instance in any meaningful way to identify that user.</span></span>

## <a name="combining-channel-and-private-interactions-with-your-bot"></a><span data-ttu-id="c9c8f-190">将频道和私人交互与你的 bot 结合使用</span><span class="sxs-lookup"><span data-stu-id="c9c8f-190">Combining channel and private interactions with your bot</span></span>

<span data-ttu-id="c9c8f-191">在频道中进行交互时，您的 bot 应智能化与用户脱机使用某些对话的情况。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-191">When interacting in a channel, your bot should be smart about taking certain conversations offline with a user.</span></span> <span data-ttu-id="c9c8f-192">例如，假设某个用户试图协调复杂任务，例如，使用一组团队成员进行日程安排。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-192">For instance, suppose a user is trying to coordinate a complex task, such as scheduling with a set of team members.</span></span> <span data-ttu-id="c9c8f-193">您可以考虑向用户发送个人聊天消息，而不是将整个交互序列显示在通道中。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-193">Rather than have the entire sequence of interactions visible to the channel, consider sending a personal chat message to the user.</span></span> <span data-ttu-id="c9c8f-194">你的 bot 应能够轻松在个人和频道对话之间切换用户，而不会失去状态。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-194">Your bot should be able to easily transition the user between personal and channel conversations without losing state.</span></span>

> [!NOTE]
><span data-ttu-id="c9c8f-195">在交互完成时，请不要忘记更新频道，以通知其他团队成员。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-195">Don’t forget to update the channel when the interaction is complete to notify the other team members.</span></span>

## <a name="full-inbound-schema-example"></a><span data-ttu-id="c9c8f-196">完整入站架构示例</span><span class="sxs-lookup"><span data-stu-id="c9c8f-196">Full inbound schema example</span></span>

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
> <span data-ttu-id="c9c8f-197">入站邮件的文本字段有时包含提到。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-197">The text field for inbound messages sometimes contains mentions.</span></span> <span data-ttu-id="c9c8f-198">请务必正确检查和去除这些。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-198">Be sure to properly check and strip those.</span></span> <span data-ttu-id="c9c8f-199">有关详细信息，请参阅[提到](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-199">For more information, see [Mentions](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions).</span></span>

## <a name="teams-channel-data"></a><span data-ttu-id="c9c8f-200">团队频道数据</span><span class="sxs-lookup"><span data-stu-id="c9c8f-200">Teams channel data</span></span>

<span data-ttu-id="c9c8f-201">该 `channelData` 对象包含特定于团队的信息，是团队和通道 id 的权威源。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-201">The `channelData` object contains Teams-specific information and is the definitive source for team and channel IDs.</span></span> <span data-ttu-id="c9c8f-202">应将这些 id 作为本地存储的键进行缓存和使用。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-202">You should cache and use these ids as keys for local storage.</span></span>

<span data-ttu-id="c9c8f-203">在 `channelData` 个人对话的邮件中不包含该对象，因为它们在任何频道之外发生。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-203">The `channelData` object is not included in messages in personal conversations since these take place outside of any channel.</span></span>

<span data-ttu-id="c9c8f-204">发送到你的 bot 的活动中的典型 channelData 对象包含以下信息：</span><span class="sxs-lookup"><span data-stu-id="c9c8f-204">A typical channelData object in an activity sent to your bot contains the following information:</span></span>

* <span data-ttu-id="c9c8f-205">`eventType`团队事件类型;仅在[频道修改事件](~/resources/bot-v3/bots-notifications.md#channel-updates)的情况下传递</span><span class="sxs-lookup"><span data-stu-id="c9c8f-205">`eventType` Teams event type; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates)</span></span>
* <span data-ttu-id="c9c8f-206">`tenant.id`Azure Active Directory 租户 ID;在所有上下文中传递</span><span class="sxs-lookup"><span data-stu-id="c9c8f-206">`tenant.id` Azure Active Directory tenant ID; passed in all contexts</span></span>
* <span data-ttu-id="c9c8f-207">`team`仅在通道上下文中传递，而不是在个人聊天中传递。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-207">`team` Passed only in channel contexts, not in personal chat.</span></span>
  * <span data-ttu-id="c9c8f-208">`id`通道的 GUID</span><span class="sxs-lookup"><span data-stu-id="c9c8f-208">`id` GUID for the channel</span></span>
  * <span data-ttu-id="c9c8f-209">`name`团队的名称;仅在[团队重命名事件](~/resources/bot-v3/bots-notifications.md#team-name-updates)的情况下传递</span><span class="sxs-lookup"><span data-stu-id="c9c8f-209">`name` Name of the team; passed only in cases of [team rename events](~/resources/bot-v3/bots-notifications.md#team-name-updates)</span></span>
* <span data-ttu-id="c9c8f-210">`channel`当提及 bot 时，仅在通道上下文中传递，或在已添加机器人的团队中的频道中传递事件</span><span class="sxs-lookup"><span data-stu-id="c9c8f-210">`channel` Passed only in channel contexts when the bot is mentioned or for events in channels in teams where the bot has been added</span></span>
  * <span data-ttu-id="c9c8f-211">`id`通道的 GUID</span><span class="sxs-lookup"><span data-stu-id="c9c8f-211">`id` GUID for the channel</span></span>
  * <span data-ttu-id="c9c8f-212">`name`通道名称;仅在[频道修改事件](~/resources/bot-v3/bots-notifications.md#channel-updates)的情况下传递。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-212">`name` Channel name; passed only in cases of [channel modification events](~/resources/bot-v3/bots-notifications.md#channel-updates).</span></span>
* <span data-ttu-id="c9c8f-213">`channelData.teamsTeamId`被.</span><span class="sxs-lookup"><span data-stu-id="c9c8f-213">`channelData.teamsTeamId` Deprecated.</span></span> <span data-ttu-id="c9c8f-214">包含此属性只是为了向后兼容。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-214">This property is included only for backwards compatibility.</span></span>
* <span data-ttu-id="c9c8f-215">`channelData.teamsChannelId`被.</span><span class="sxs-lookup"><span data-stu-id="c9c8f-215">`channelData.teamsChannelId` Deprecated.</span></span> <span data-ttu-id="c9c8f-216">包含此属性只是为了向后兼容。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-216">This property is included only for backwards compatibility.</span></span>

### <a name="example-channeldata-object-channelcreated-event"></a><span data-ttu-id="c9c8f-217">示例 channelData 对象（channelCreated 事件）</span><span class="sxs-lookup"><span data-stu-id="c9c8f-217">Example channelData object (channelCreated event)</span></span>

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

### <a name="net-example"></a><span data-ttu-id="c9c8f-218">.NET 示例</span><span class="sxs-lookup"><span data-stu-id="c9c8f-218">.NET example</span></span>

<span data-ttu-id="c9c8f-219">" [Microsoft Bot. 团队](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)" NuGet 包提供专用 `TeamsChannelData` 对象，该对象公开了用于访问团队特定信息的属性。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-219">The [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package provides a specialized `TeamsChannelData` object, which exposes properties to access Teams-specific information.</span></span>

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a><span data-ttu-id="c9c8f-220">向邮件发送答复</span><span class="sxs-lookup"><span data-stu-id="c9c8f-220">Sending replies to messages</span></span>

<span data-ttu-id="c9c8f-221">若要答复现有邮件，请 [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) 在 .net 或 Node.js 中进行调用 [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) 。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-221">To reply to an existing message, call [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) in .NET or [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities) in Node.js.</span></span> <span data-ttu-id="c9c8f-222">机器人生成器 SDK 处理所有详细信息。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-222">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="c9c8f-223">如果选择使用 REST API，则还可以调用 [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) 终结点。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-223">If you choose to use the REST API, you can also call the [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0) endpoint.</span></span>

<span data-ttu-id="c9c8f-224">邮件内容本身可以包含简单文本或某些机器人框架提供的[卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-224">The message content itself can contain simple text or some of the Bot Framework supplied [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

<span data-ttu-id="c9c8f-225">请注意，在出站架构中，应始终使用与 `serviceUrl` 您接收到的相同。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-225">Please note that in your outbound schema you should always use the same `serviceUrl` as the one you received.</span></span> <span data-ttu-id="c9c8f-226">请注意，的值 `serviceUrl` 往往是稳定的，但可能会发生变化。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-226">Be aware that the value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="c9c8f-227">当新邮件到达时，你的 bot 应验证其存储值 `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-227">When a new message arrives, your bot should verify its stored value of `serviceUrl`.</span></span>

## <a name="updating-messages"></a><span data-ttu-id="c9c8f-228">更新邮件</span><span class="sxs-lookup"><span data-stu-id="c9c8f-228">Updating messages</span></span>

<span data-ttu-id="c9c8f-229">你的 bot 不是让你的邮件成为数据的静态快照，而你的 bot 可以在发送邮件后动态更新这些邮件。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-229">Rather than have your messages be static snapshots of data, your bot can dynamically update messages inline after sending them.</span></span> <span data-ttu-id="c9c8f-230">您可以对轮询更新、在按钮按下时修改可用操作或任何其他异步状态更改的方案使用动态邮件更新。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-230">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="c9c8f-231">新邮件需要与类型中的原始邮件不匹配。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-231">The new message need not match the original in type.</span></span> <span data-ttu-id="c9c8f-232">例如，如果原始邮件包含附件，则新邮件可以是简单的短信。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-232">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

> [!NOTE]
> <span data-ttu-id="c9c8f-233">您可以仅更新在单附件邮件和轮播版式中发送的内容。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-233">You can update only content sent in single-attachment messages and carousel layouts.</span></span> <span data-ttu-id="c9c8f-234">不支持将更新发布到列表布局中包含多个附件的邮件。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-234">Posting updates to messages with multiple attachments in list layout is not supported.</span></span>

### <a name="rest-api"></a><span data-ttu-id="c9c8f-235">REST API</span><span class="sxs-lookup"><span data-stu-id="c9c8f-235">REST API</span></span>

<span data-ttu-id="c9c8f-236">若要发出邮件更新，只需 `/v3/conversations/<conversationId>/activities/<activityId>/` 使用给定的活动 ID 对终结点执行 PUT 请求即可。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-236">To issue a message update, simply perform a PUT request against the `/v3/conversations/<conversationId>/activities/<activityId>/` endpoint using a given activity ID.</span></span> <span data-ttu-id="c9c8f-237">若要完成此方案，您应缓存最初的 POST 呼叫返回的活动 ID。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-237">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a><span data-ttu-id="c9c8f-238">.NET 示例</span><span class="sxs-lookup"><span data-stu-id="c9c8f-238">.NET example</span></span>

<span data-ttu-id="c9c8f-239">您可以使用 `UpdateActivityAsync` 机器人生成器 SDK 中的方法来更新现有邮件。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-239">You can use the `UpdateActivityAsync` method in the Bot Builder SDK to update an existing message.</span></span>

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

### <a name="nodejs-example"></a><span data-ttu-id="c9c8f-240">Node.js 示例</span><span class="sxs-lookup"><span data-stu-id="c9c8f-240">Node.js example</span></span>

<span data-ttu-id="c9c8f-241">您可以使用 `session.connector.update` 机器人生成器 SDK 中的方法来更新现有邮件。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-241">You can use the `session.connector.update` method in the Bot Builder SDK to update an existing message.</span></span>

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

## <a name="starting-a-conversation-proactive-messaging"></a><span data-ttu-id="c9c8f-242">启动对话（主动消息传递）</span><span class="sxs-lookup"><span data-stu-id="c9c8f-242">Starting a conversation (proactive messaging)</span></span>

<span data-ttu-id="c9c8f-243">您可以使用用户创建个人对话，也可以在频道中为您的团队 bot 创建一个新的答复链。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-243">You can create a personal conversation with a user or start a new reply chain in a channel for your team bot.</span></span> <span data-ttu-id="c9c8f-244">这样，你就可以在不先启动用户和你的 bot 的情况下向你的用户发送消息。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-244">This lets you to message your user or users without having them first initiate contact with your bot.</span></span> <span data-ttu-id="c9c8f-245">有关详细信息，请参阅下列主题：</span><span class="sxs-lookup"><span data-stu-id="c9c8f-245">For more information, see the following topics:</span></span>

<span data-ttu-id="c9c8f-246">有关 bot 启动的对话的更多常规信息，请参阅[短信服务的 bot](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) 。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-246">See [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) for more general information on conversations started by bots.</span></span>

## <a name="deleting-messages"></a><span data-ttu-id="c9c8f-247">删除邮件</span><span class="sxs-lookup"><span data-stu-id="c9c8f-247">Deleting messages</span></span>

<span data-ttu-id="c9c8f-248">可以使用 [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted)中的连接器方法删除邮件。</span><span class="sxs-lookup"><span data-stu-id="c9c8f-248">Messages can be deleted using the connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) method in the [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted).</span></span>

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
