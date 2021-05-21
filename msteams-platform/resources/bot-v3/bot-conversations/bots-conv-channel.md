---
title: 与机器人的频道和群组聊天对话
description: 介绍在 Microsoft Teams 中与频道中的机器人对话的端到端Microsoft Teams
keywords: teams 方案频道对话机器人
localization_priority: Normal
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: e254302271cf101638c897e1a1952d302705d6a4
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566794"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="63898-104">带有 Microsoft Teams 机器人的频道和群聊对话</span><span class="sxs-lookup"><span data-stu-id="63898-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="63898-105">Microsoft Teams允许用户将机器人引入其频道或群组聊天对话。</span><span class="sxs-lookup"><span data-stu-id="63898-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="63898-106">通过将聊天机器人添加到团队或聊天中，对话的所有用户都可以在对话中利用机器人功能。</span><span class="sxs-lookup"><span data-stu-id="63898-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="63898-107">还可以在自动Teams访问特定于团队的功能，如查询团队信息和@mentioning用户。</span><span class="sxs-lookup"><span data-stu-id="63898-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="63898-108">频道和群聊中的聊天不同于个人聊天，因为用户需要@mention聊天。</span><span class="sxs-lookup"><span data-stu-id="63898-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="63898-109">如果自动程序在多个范围（如个人、群聊或频道）中使用，则需要检测自动程序消息来自什么范围，并相应地处理它们。</span><span class="sxs-lookup"><span data-stu-id="63898-109">If a bot is used in multiple scopes such as personal, groupchat, or channel, you need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="63898-110">为频道或组设计出色的自动程序</span><span class="sxs-lookup"><span data-stu-id="63898-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="63898-111">添加到团队的机器人将成为另一个团队成员，@mentioned对话的一部分。</span><span class="sxs-lookup"><span data-stu-id="63898-111">Bots added to a team become another team member and can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="63898-112">事实上，聊天机器人仅在@mentioned接收消息，因此频道上的其他对话不会发送给机器人。</span><span class="sxs-lookup"><span data-stu-id="63898-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

<span data-ttu-id="63898-113">组或频道中的机器人应提供与所有成员相关且合适的信息。</span><span class="sxs-lookup"><span data-stu-id="63898-113">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="63898-114">尽管机器人当然可以提供与体验相关的任何信息，但请记住，与它的对话对所有人都可见。</span><span class="sxs-lookup"><span data-stu-id="63898-114">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="63898-115">因此，组或频道中出色的机器人应该为所有用户增加价值，并且当然不会无意中共享更适合于一对一对话的信息。</span><span class="sxs-lookup"><span data-stu-id="63898-115">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate to a one-to-one conversation.</span></span>

<span data-ttu-id="63898-116">与现在一样，自动程序可能在所有范围内完全相关，无需额外工作。</span><span class="sxs-lookup"><span data-stu-id="63898-116">Your bot, just as it is, may be entirely relevant in all scopes without requiring additional work.</span></span> <span data-ttu-id="63898-117">In Microsoft Teams there is no expectation that your bot function in all scopes， but you should ensure that your bot provides user value in whichever scope (s) you choose to support.</span><span class="sxs-lookup"><span data-stu-id="63898-117">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure that your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="63898-118">有关范围详细信息，请参阅应用程序中[Microsoft Teams。](~/concepts/build-and-test/app-studio-overview.md)</span><span class="sxs-lookup"><span data-stu-id="63898-118">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="63898-119">开发在组或频道中工作的自动程序使用与个人对话相同的许多功能。</span><span class="sxs-lookup"><span data-stu-id="63898-119">Developing a bot that works in groups or channels uses much of the same functionality as personal conversations.</span></span> <span data-ttu-id="63898-120">有效负载中的其他事件和数据Teams组和频道信息。</span><span class="sxs-lookup"><span data-stu-id="63898-120">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="63898-121">以下各节介绍了这些差异以及常见功能的主要差异。</span><span class="sxs-lookup"><span data-stu-id="63898-121">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="63898-122">创建邮件</span><span class="sxs-lookup"><span data-stu-id="63898-122">Creating messages</span></span>

<span data-ttu-id="63898-123">有关在频道中创建消息的机器人详细信息，请参阅 [针对](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)机器人的主动消息，特别是 [创建频道对话](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)。</span><span class="sxs-lookup"><span data-stu-id="63898-123">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="63898-124">接收邮件</span><span class="sxs-lookup"><span data-stu-id="63898-124">Receiving messages</span></span>

<span data-ttu-id="63898-125">对于组或频道中的自动程序，除了常规邮件架构之外[](https://docs.botframework.com/core-concepts/reference/#activity)，机器人还会收到以下属性：</span><span class="sxs-lookup"><span data-stu-id="63898-125">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="63898-126">`channelData`请参阅[Teams频道数据](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)。</span><span class="sxs-lookup"><span data-stu-id="63898-126">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="63898-127">在群聊中，包含特定于该聊天的信息。</span><span class="sxs-lookup"><span data-stu-id="63898-127">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="63898-128">`conversation.id` 回复链 ID，由频道 ID 和回复链中第一封邮件的 ID 组成。</span><span class="sxs-lookup"><span data-stu-id="63898-128">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain.</span></span>
* <span data-ttu-id="63898-129">`conversation.isGroup` 适用于 `true` 频道或群聊中的聊天机器人消息。</span><span class="sxs-lookup"><span data-stu-id="63898-129">`conversation.isGroup` Is `true` for bot messages in channels or group chats.</span></span>
* <span data-ttu-id="63898-130">`conversation.conversationType` 或 `groupChat` `channel` 。</span><span class="sxs-lookup"><span data-stu-id="63898-130">`conversation.conversationType` Either `groupChat` or `channel`.</span></span>
* <span data-ttu-id="63898-131">`entities` 可以包含一个或多个提及。</span><span class="sxs-lookup"><span data-stu-id="63898-131">`entities` Can contain one or more mentions.</span></span> <span data-ttu-id="63898-132">有关详细信息，请参阅 [提及](#-mentions)。</span><span class="sxs-lookup"><span data-stu-id="63898-132">For more information, see [Mentions](#-mentions).</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="63898-133">回复邮件</span><span class="sxs-lookup"><span data-stu-id="63898-133">Replying to messages</span></span>

<span data-ttu-id="63898-134">若要回复现有邮件，请调用 [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) .NET 或 [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) Node.js。</span><span class="sxs-lookup"><span data-stu-id="63898-134">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="63898-135">Bot Builder SDK 处理所有详细信息。</span><span class="sxs-lookup"><span data-stu-id="63898-135">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="63898-136">如果选择使用 REST API，还可以调用 [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) 终结点。</span><span class="sxs-lookup"><span data-stu-id="63898-136">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="63898-137">在频道中，回复消息将显示为对启动回复链的回复。</span><span class="sxs-lookup"><span data-stu-id="63898-137">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="63898-138">`conversation.id`包含频道和顶级消息 ID。</span><span class="sxs-lookup"><span data-stu-id="63898-138">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="63898-139">尽管 Bot Framework 负责处理详细信息，但可以根据需要缓存该对话线程的将来 `conversation.id` 回复。</span><span class="sxs-lookup"><span data-stu-id="63898-139">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="63898-140">最佳做法：欢迎邮件Teams</span><span class="sxs-lookup"><span data-stu-id="63898-140">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="63898-141">首次将机器人添加到组或团队时，向所有用户发送向机器人介绍的欢迎消息通常很有用。</span><span class="sxs-lookup"><span data-stu-id="63898-141">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="63898-142">欢迎消息应提供自动程序功能和用户优势的说明。</span><span class="sxs-lookup"><span data-stu-id="63898-142">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="63898-143">理想情况下，消息还应包含用户与应用交互的命令。</span><span class="sxs-lookup"><span data-stu-id="63898-143">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="63898-144">为此，请确保自动程序在 对象中以 `conversationUpdate` `teamsAddMembers` eventType 响应 `channelData` 消息。</span><span class="sxs-lookup"><span data-stu-id="63898-144">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="63898-145">请确保 ID 是机器人的应用 ID 本身，因为在将用户添加到团队时将发送相同的 `memberAdded` 事件。</span><span class="sxs-lookup"><span data-stu-id="63898-145">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="63898-146">有关详细信息 [，请参阅团队成员或](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) 机器人添加。</span><span class="sxs-lookup"><span data-stu-id="63898-146">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="63898-147">添加自动程序时，你可能还希望向团队的每个成员发送个人邮件。</span><span class="sxs-lookup"><span data-stu-id="63898-147">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="63898-148">为此，你可以提取 [团队名单](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) ，并给每个用户发送一条 [直接消息](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。</span><span class="sxs-lookup"><span data-stu-id="63898-148">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="63898-149">建议自动程序 *在* 下列情况下不要发送欢迎消息：</span><span class="sxs-lookup"><span data-stu-id="63898-149">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="63898-150">团队是一 (的成员，例如，超过 100 个成员) 。</span><span class="sxs-lookup"><span data-stu-id="63898-150">The team is big (obviously subjective, for example, more than 100 members).</span></span> <span data-ttu-id="63898-151">您的自动程序可能会被视为"spa一"，添加它的人可能会收到投诉，除非您向看到欢迎消息的每个人清楚地传达了机器人的价值主张。</span><span class="sxs-lookup"><span data-stu-id="63898-151">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="63898-152">你的机器人首先在组或频道中提及，而不是先添加到团队。</span><span class="sxs-lookup"><span data-stu-id="63898-152">Your bot is first mentioned in a group or channel, versus being first added to a team.</span></span>
* <span data-ttu-id="63898-153">重命名组或频道。</span><span class="sxs-lookup"><span data-stu-id="63898-153">A group or channel is renamed.</span></span>
* <span data-ttu-id="63898-154">将团队成员添加到组或频道。</span><span class="sxs-lookup"><span data-stu-id="63898-154">A team member is added to a group or channel.</span></span>

## <a name="-mentions"></a><span data-ttu-id="63898-155">@ 提及</span><span class="sxs-lookup"><span data-stu-id="63898-155">@ Mentions</span></span>

<span data-ttu-id="63898-156">由于组或频道中的机器人仅在邮件中提到 ("@_botname_") 时做出响应，因此组频道中的自动程序接收的每封邮件都包含其自己的名称，因此必须确保邮件分析能够处理。</span><span class="sxs-lookup"><span data-stu-id="63898-156">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="63898-157">此外，机器人可以分析提及的其他用户，并提及用户作为消息的一部分。</span><span class="sxs-lookup"><span data-stu-id="63898-157">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="63898-158">检索提及</span><span class="sxs-lookup"><span data-stu-id="63898-158">Retrieving mentions</span></span>

<span data-ttu-id="63898-159">提及在有效负载中的 对象中返回，并且包含用户的唯一 ID，并且在大多数情况下，还包含 `entities` 提及的用户名称。</span><span class="sxs-lookup"><span data-stu-id="63898-159">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="63898-160">可以通过调用 .NET 的 Bot Builder SDK 中的 函数来检索邮件中提及的所有内容，该函数 `GetMentions` 将返回对象 `Mentioned` 数组。</span><span class="sxs-lookup"><span data-stu-id="63898-160">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="63898-161">.NET 示例代码：检查并去除@bot提及</span><span class="sxs-lookup"><span data-stu-id="63898-161">.NET example code: Check for and strip @bot mention</span></span>

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
> <span data-ttu-id="63898-162">您还可以使用 Teams 扩展函数，该函数去除所有提及， `GetTextWithoutMentions` 包括自动程序。</span><span class="sxs-lookup"><span data-stu-id="63898-162">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="63898-163">Node.js代码：检查并去除@bot提及</span><span class="sxs-lookup"><span data-stu-id="63898-163">Node.js example code: Check for and strip @bot mention</span></span>

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

<span data-ttu-id="63898-164">您还可以使用 Teams 扩展函数，该函数去除所有提及， `getTextWithoutMentions` 包括自动程序。</span><span class="sxs-lookup"><span data-stu-id="63898-164">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="63898-165">构造提及</span><span class="sxs-lookup"><span data-stu-id="63898-165">Constructing mentions</span></span>

<span data-ttu-id="63898-166">机器人可以在发布至频道的消息中提及其他用户。</span><span class="sxs-lookup"><span data-stu-id="63898-166">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="63898-167">为此，您的邮件必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="63898-167">To do this, your message must do the following:</span></span>

* <span data-ttu-id="63898-168">包括在 `<at>@username</at>` 邮件文本中。</span><span class="sxs-lookup"><span data-stu-id="63898-168">Include `<at>@username</at>` in the message text.</span></span>
* <span data-ttu-id="63898-169">将 `mention` 对象包括在 entities 集合中。</span><span class="sxs-lookup"><span data-stu-id="63898-169">Include the `mention` object inside the entities collection.</span></span>

#### <a name="net-example"></a><span data-ttu-id="63898-170">.NET 示例</span><span class="sxs-lookup"><span data-stu-id="63898-170">.NET example</span></span>

<span data-ttu-id="63898-171">此示例使用[Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)包。</span><span class="sxs-lookup"><span data-stu-id="63898-171">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="63898-172">Node.js示例</span><span class="sxs-lookup"><span data-stu-id="63898-172">Node.js example</span></span>

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

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="63898-173">示例：已提及用户的传出邮件</span><span class="sxs-lookup"><span data-stu-id="63898-173">Example: Outgoing message with user mentioned</span></span>

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

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="63898-174">访问 groupChat 或 channel 作用域</span><span class="sxs-lookup"><span data-stu-id="63898-174">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="63898-175">机器人可以执行更多操作，而不是在组和团队中发送和接收消息。</span><span class="sxs-lookup"><span data-stu-id="63898-175">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="63898-176">例如，它还可以提取成员列表，包括其配置文件信息以及频道列表。</span><span class="sxs-lookup"><span data-stu-id="63898-176">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="63898-177">有关详细信息，请参阅[获取自动程序Microsoft Teams上下文](~/resources/bot-v3/bots-context.md)。</span><span class="sxs-lookup"><span data-stu-id="63898-177">For more information, see [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md).</span></span>

## <a name="see-also"></a><span data-ttu-id="63898-178">另请参阅</span><span class="sxs-lookup"><span data-stu-id="63898-178">See also</span></span>

[<span data-ttu-id="63898-179">Bot Framework 示例</span><span class="sxs-lookup"><span data-stu-id="63898-179">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
