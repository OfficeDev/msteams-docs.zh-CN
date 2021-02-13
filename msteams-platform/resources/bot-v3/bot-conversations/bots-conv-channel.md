---
title: 与机器人的频道和群聊对话
description: 介绍在 Microsoft Teams 的频道中与机器人对话的端到端方案
keywords: 团队方案频道对话机器人
ms.date: 06/25/2019
ms.openlocfilehash: e556eb006257a83ddf93adb62f79857201d6a9ad
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231629"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="e73d3-104">与 Microsoft Teams 机器人的频道和群聊对话</span><span class="sxs-lookup"><span data-stu-id="e73d3-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="e73d3-105">Microsoft Teams 允许用户将机器人引入其频道或群聊对话。</span><span class="sxs-lookup"><span data-stu-id="e73d3-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="e73d3-106">通过将机器人添加到团队或聊天，对话的所有用户都可以在对话中充分利用机器人功能。</span><span class="sxs-lookup"><span data-stu-id="e73d3-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="e73d3-107">还可以在机器人中访问特定于 Teams 的功能，例如查询团队信息和@mentioning用户。</span><span class="sxs-lookup"><span data-stu-id="e73d3-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="e73d3-108">频道和群聊中的聊天不同于个人聊天，因为用户需要@mention聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="e73d3-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="e73d3-109">如果自动程序用于个人、 (或频道) 则需要检测自动程序消息来自的作用域，并相应地处理它们。</span><span class="sxs-lookup"><span data-stu-id="e73d3-109">If a bot is used in multiple scopes (personal, groupchat or channel) you will need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="e73d3-110">为频道或组设计出色的自动程序</span><span class="sxs-lookup"><span data-stu-id="e73d3-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="e73d3-111">添加到团队的机器人将成为另一个团队成员，@mentioned对话的一部分。</span><span class="sxs-lookup"><span data-stu-id="e73d3-111">Bots added to a team become another team member and can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="e73d3-112">事实上，自动程序仅在收到@mentioned时接收消息，因此频道上的其他对话不会发送给机器人。</span><span class="sxs-lookup"><span data-stu-id="e73d3-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

<span data-ttu-id="e73d3-113">组或频道中的机器人应提供与所有成员相关且合适的信息。</span><span class="sxs-lookup"><span data-stu-id="e73d3-113">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="e73d3-114">虽然机器人当然可以提供与体验相关的任何信息，但请记住，与体验相关的对话对所有人都可见。</span><span class="sxs-lookup"><span data-stu-id="e73d3-114">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="e73d3-115">因此，组或频道中出色的自动程序应该为所有用户增加价值，并且当然不会无意中共享更适用于一对一对话的信息。</span><span class="sxs-lookup"><span data-stu-id="e73d3-115">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate to a one-to-one conversation.</span></span>

<span data-ttu-id="e73d3-116">与现在一样，机器人可能在所有范围内完全相关，无需额外工作。</span><span class="sxs-lookup"><span data-stu-id="e73d3-116">Your bot, just as it is, may be entirely relevant in all scopes without requiring additional work.</span></span> <span data-ttu-id="e73d3-117">在 Microsoft Teams 中，机器人功能在所有范围内都没有任何预期，但应确保自动程序在选择支持的任何 (范围内) 用户价值。</span><span class="sxs-lookup"><span data-stu-id="e73d3-117">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure that your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="e73d3-118">有关范围详细信息，请参阅 Microsoft [Teams 中的应用](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="e73d3-118">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="e73d3-119">开发在组或频道中工作的自动程序使用与个人对话相同的大部分功能。</span><span class="sxs-lookup"><span data-stu-id="e73d3-119">Developing a bot that works in groups or channels uses much of the same functionality as personal conversations.</span></span> <span data-ttu-id="e73d3-120">有效负载中的其他事件和数据提供 Teams 组和频道信息。</span><span class="sxs-lookup"><span data-stu-id="e73d3-120">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="e73d3-121">以下各节介绍了这些差异以及常见功能的主要差异。</span><span class="sxs-lookup"><span data-stu-id="e73d3-121">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="e73d3-122">创建邮件</span><span class="sxs-lookup"><span data-stu-id="e73d3-122">Creating messages</span></span>

<span data-ttu-id="e73d3-123">有关机器人在频道中创建消息详细信息，请参阅 [自动](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)程序主动消息传递，尤其是 [创建频道对话](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)。</span><span class="sxs-lookup"><span data-stu-id="e73d3-123">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="e73d3-124">接收邮件</span><span class="sxs-lookup"><span data-stu-id="e73d3-124">Receiving messages</span></span>

<span data-ttu-id="e73d3-125">对于组或频道中的自动程序，除了常规邮件 [架构](https://docs.botframework.com/core-concepts/reference/#activity)之外，机器人还会收到以下属性：</span><span class="sxs-lookup"><span data-stu-id="e73d3-125">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="e73d3-126">`channelData` 请参阅 [Teams 频道数据](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)。</span><span class="sxs-lookup"><span data-stu-id="e73d3-126">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="e73d3-127">在群聊中，包含特定于该聊天的信息。</span><span class="sxs-lookup"><span data-stu-id="e73d3-127">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="e73d3-128">`conversation.id` 回复链 ID，由频道 ID 以及回复链中第一封邮件的 ID 组成</span><span class="sxs-lookup"><span data-stu-id="e73d3-128">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain</span></span>
* <span data-ttu-id="e73d3-129">`conversation.isGroup` 用于 `true` 频道或群聊中的自动程序消息</span><span class="sxs-lookup"><span data-stu-id="e73d3-129">`conversation.isGroup` Is `true` for bot messages in channels or group chats</span></span>
* <span data-ttu-id="e73d3-130">`conversation.conversationType`或者 `groupChat``channel`</span><span class="sxs-lookup"><span data-stu-id="e73d3-130">`conversation.conversationType` Either `groupChat` or `channel`</span></span>
* <span data-ttu-id="e73d3-131">`entities`可包含一个或多个提及 ([请参阅"提及) ](#-mentions)</span><span class="sxs-lookup"><span data-stu-id="e73d3-131">`entities` Can contain one or more mentions (see [Mentions](#-mentions))</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="e73d3-132">回复邮件</span><span class="sxs-lookup"><span data-stu-id="e73d3-132">Replying to messages</span></span>

<span data-ttu-id="e73d3-133">若要答复现有邮件，请通过 [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) .NET 或 [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) Node.js。</span><span class="sxs-lookup"><span data-stu-id="e73d3-133">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="e73d3-134">自动程序生成器 SDK 处理所有详细信息。</span><span class="sxs-lookup"><span data-stu-id="e73d3-134">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="e73d3-135">如果选择使用 REST API，还可以调用 [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) 终结点。</span><span class="sxs-lookup"><span data-stu-id="e73d3-135">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="e73d3-136">在频道中，回复消息将显示为对启动回复链的回复。</span><span class="sxs-lookup"><span data-stu-id="e73d3-136">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="e73d3-137">包含 `conversation.id` 通道和顶级邮件 ID。</span><span class="sxs-lookup"><span data-stu-id="e73d3-137">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="e73d3-138">尽管 Bot Framework 会处理详细信息，但您可以根据需要缓存这些详细信息，供以后回复该 `conversation.id` 对话线程。</span><span class="sxs-lookup"><span data-stu-id="e73d3-138">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="e73d3-139">最佳做法：Teams 中的欢迎消息</span><span class="sxs-lookup"><span data-stu-id="e73d3-139">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="e73d3-140">当你的机器人首次添加到组或团队时，向所有用户发送一条欢迎消息，向所有用户介绍机器人通常很有用。</span><span class="sxs-lookup"><span data-stu-id="e73d3-140">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="e73d3-141">欢迎消息应提供自动程序功能和用户优势的说明。</span><span class="sxs-lookup"><span data-stu-id="e73d3-141">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="e73d3-142">理想情况下，该消息还应包含用户与应用交互的命令。</span><span class="sxs-lookup"><span data-stu-id="e73d3-142">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="e73d3-143">为此，请确保机器人使用 `conversationUpdate` `teamsAddMembers` 对象的 eventType 响应 `channelData` 邮件。</span><span class="sxs-lookup"><span data-stu-id="e73d3-143">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="e73d3-144">请确保 ID 是自动程序的应用 ID 本身，因为将用户添加到团队时将发送相同的 `memberAdded` 事件。</span><span class="sxs-lookup"><span data-stu-id="e73d3-144">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="e73d3-145">有关 [更多详细信息，请参阅团队成员或](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) 机器人添加。</span><span class="sxs-lookup"><span data-stu-id="e73d3-145">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="e73d3-146">添加自动程序时，您可能还需要向团队的每个成员发送个人消息。</span><span class="sxs-lookup"><span data-stu-id="e73d3-146">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="e73d3-147">为此，你可以获取 [团队名单](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) ，并发送一条直接 [消息给每个用户](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。</span><span class="sxs-lookup"><span data-stu-id="e73d3-147">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="e73d3-148">建议机器人 *在* 下列情况下不要发送欢迎消息：</span><span class="sxs-lookup"><span data-stu-id="e73d3-148">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="e73d3-149">团队规模较大 (明显具有主观性，但例如，超过 100 个成员) 。</span><span class="sxs-lookup"><span data-stu-id="e73d3-149">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="e73d3-150">你的机器人可能会被视为"spabot"，并且添加它的人可能会收到投诉，除非你向看到欢迎消息的每个人清楚地传达了机器人的价值主张。</span><span class="sxs-lookup"><span data-stu-id="e73d3-150">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="e73d3-151">你的自动程序首先在组或频道 (，而不是先添加到团队) </span><span class="sxs-lookup"><span data-stu-id="e73d3-151">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="e73d3-152">重命名组或频道</span><span class="sxs-lookup"><span data-stu-id="e73d3-152">A group or channel is renamed</span></span>
* <span data-ttu-id="e73d3-153">将团队成员添加到组或频道</span><span class="sxs-lookup"><span data-stu-id="e73d3-153">A team member is added to a group or channel</span></span>

## <a name="-mentions"></a><span data-ttu-id="e73d3-154">@ 提及</span><span class="sxs-lookup"><span data-stu-id="e73d3-154">@ Mentions</span></span>

<span data-ttu-id="e73d3-155">由于组或频道中的自动程序仅在消息中提到 ("@_botname_") 时进行响应，因此组频道中的自动程序接收的每封邮件都包含其自己的名称，并且必须确保邮件分析能够处理该名称。</span><span class="sxs-lookup"><span data-stu-id="e73d3-155">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="e73d3-156">此外，机器人可以分析提及的其他用户，并提及用户作为消息的一部分。</span><span class="sxs-lookup"><span data-stu-id="e73d3-156">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="e73d3-157">检索提及</span><span class="sxs-lookup"><span data-stu-id="e73d3-157">Retrieving mentions</span></span>

<span data-ttu-id="e73d3-158">提及在有效负载的对象中返回，并且同时包含用户的唯一 ID，在大多数情况下，还包含 `entities` 提及的用户名称。</span><span class="sxs-lookup"><span data-stu-id="e73d3-158">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="e73d3-159">可以通过调用 .NET 的 Bot Builder SDK 中的函数来检索邮件中提及的所有内容，这将 `GetMentions` 返回对象 `Mentioned` 数组。</span><span class="sxs-lookup"><span data-stu-id="e73d3-159">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="e73d3-160">.NET 示例代码：检查并去除@bot提及</span><span class="sxs-lookup"><span data-stu-id="e73d3-160">.NET example code: Check for and strip @bot mention</span></span>

```csharp
Mention[] m = sourceMessage.GetMentions();
var messageText = sourceMessage.Text;

for (int i = 0;i < m.Length;i++)
{
    if (m[i].Mentioned.Id == sourceMessage.Recipient.Id)
    {
        //Bot is in the @mention list.
        //The below example will strip the bot name out of the message, so you can parse it as if it wasn't included. Note that the Text object will contain the full bot name, if applicable.
        if (m[i].Text != null)
            messageText = messageText.Replace(m[i].Text, "");
    }
}
```

> [!NOTE]
> <span data-ttu-id="e73d3-161">您还可以使用 Teams 扩展函数，该函数去除所有提及， `GetTextWithoutMentions` 包括自动程序。</span><span class="sxs-lookup"><span data-stu-id="e73d3-161">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="e73d3-162">Node.js代码：检查并去除@bot提及</span><span class="sxs-lookup"><span data-stu-id="e73d3-162">Node.js example code: Check for and strip @bot mention</span></span>

```javascript
var text = message.text;
if (message.entities) {
    message.entities
        .filter(entity => ((entity.type === "mention") && (entity.mentioned.id.toLowerCase() === botId)))
        .forEach(entity => {
            text = text.replace(entity.text, "");
        });
    text = text.trim();
}
```

<span data-ttu-id="e73d3-163">您还可以使用 Teams 扩展函数，该函数去除所有提及， `getTextWithoutMentions` 包括自动程序。</span><span class="sxs-lookup"><span data-stu-id="e73d3-163">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="e73d3-164">构造提及</span><span class="sxs-lookup"><span data-stu-id="e73d3-164">Constructing mentions</span></span>

<span data-ttu-id="e73d3-165">机器人可以在发布到频道的消息中提及其他用户。</span><span class="sxs-lookup"><span data-stu-id="e73d3-165">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="e73d3-166">为此，您的邮件必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="e73d3-166">To do this, your message must do the following:</span></span>

* <span data-ttu-id="e73d3-167">包括在 `<at>@username</at>` 邮件文本中</span><span class="sxs-lookup"><span data-stu-id="e73d3-167">Include `<at>@username</at>` in the message text</span></span>
* <span data-ttu-id="e73d3-168">将 `mention` 对象包括在实体集合内</span><span class="sxs-lookup"><span data-stu-id="e73d3-168">Include the `mention` object inside the entities collection</span></span>

#### <a name="net-example"></a><span data-ttu-id="e73d3-169">.NET 示例</span><span class="sxs-lookup"><span data-stu-id="e73d3-169">.NET example</span></span>

<span data-ttu-id="e73d3-170">此示例使用 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet 程序包。</span><span class="sxs-lookup"><span data-stu-id="e73d3-170">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="e73d3-171">Node.js示例</span><span class="sxs-lookup"><span data-stu-id="e73d3-171">Node.js example</span></span>

```javascript
// User to mention
var toMention: builder.IIdentity = {
    name: 'John Doe',
    id: userId
};

// Create a message and add mention to it
var msg = new teams.TeamsMessage(session).text(teams.TeamsMessage.getTenantId(session.message));
var mentionedMsg = msg.addMentionToText(toMention);

// Post the message
var generalMessage = mentionedMsg.routeReplyToGeneralChannel();
session.send(generalMessage);
```

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="e73d3-172">示例：已提及用户的传出邮件</span><span class="sxs-lookup"><span data-stu-id="e73d3-172">Example: Outgoing message with user mentioned</span></span>

```json
{
    "type": "message", 
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "28:9e52142b-5e5e-4d7b-bb3e- e82dcf620000",
        "name": "SchemaTestBot"
    },
    "conversation": {
        "id": "19:aebd0ad4d6ab42c8b9ed19c251c2fc37@thread.skype;messageid=1481567603816"
    },
    "recipient": {
        "id": "8:orgid:6aebbad0-e5a5-424a-834a-20fb051f3c1a",
        "name": "stlrgload100"
    },
    "attachments": [
        {
            "contentType": "image/png",
            "contentUrl": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
            "name": "Bender_Rodriguez.png"
        }
    ],
    "entities": [
        {
            "type":"mention",
            "mentioned":{
                "id":"29:08q2j2o3jc09au90eucae",
                "name":"Pranav Smith"
            },
            "text": "<at>@Pranav Smith</at>"
        }
    ],
    "replyToId": "3UP4UTkzUk1zzeyW"
}
```

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="e73d3-173">访问群聊或频道范围</span><span class="sxs-lookup"><span data-stu-id="e73d3-173">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="e73d3-174">机器人可以执行更多操作，而不是在组和团队中发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="e73d3-174">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="e73d3-175">例如，它还可以获取成员列表，包括其配置文件信息以及频道列表。</span><span class="sxs-lookup"><span data-stu-id="e73d3-175">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="e73d3-176">有关详细信息 [，请参阅"获取 Microsoft Teams 机器人](~/resources/bot-v3/bots-context.md) 的上下文"。</span><span class="sxs-lookup"><span data-stu-id="e73d3-176">See [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md) to learn more.</span></span>

<span data-ttu-id="e73d3-177">*另请参阅 Bot* [Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="e73d3-177">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
