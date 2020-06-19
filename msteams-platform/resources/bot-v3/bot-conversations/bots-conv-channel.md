---
title: 与 bot 的频道和组聊天对话
description: 介绍在 Microsoft 团队中与频道中的 bot 进行对话的端到端方案
keywords: 团队方案频道对话机器人
ms.date: 06/25/2019
ms.openlocfilehash: d2d72bdba43de6ebb10c7504dd309459cb09d56c
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801031"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="578ff-104">与 Microsoft 团队 bot 的频道和组聊天对话</span><span class="sxs-lookup"><span data-stu-id="578ff-104">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="578ff-105">Microsoft 团队允许用户将 bot 引入其频道或组聊天对话。</span><span class="sxs-lookup"><span data-stu-id="578ff-105">Microsoft Teams allows users to bring bots into their channel or group chat conversations.</span></span> <span data-ttu-id="578ff-106">通过向团队或聊天添加机器人，对话的所有用户都可以充分利用对话中的 bot 功能。</span><span class="sxs-lookup"><span data-stu-id="578ff-106">By adding a bot to a team or chat, all users of the conversation can take advantage of the bot functionality right in the conversation.</span></span> <span data-ttu-id="578ff-107">您还可以访问您的 bot 中特定于团队的功能，例如查询团队信息和 @mentioning 用户。</span><span class="sxs-lookup"><span data-stu-id="578ff-107">You can also access Teams-specific functionality within your bot like querying team information and @mentioning users.</span></span>

<span data-ttu-id="578ff-108">频道和组聊天中的聊天与个人聊天中的不同之处在于用户需要 @mention 机器人。</span><span class="sxs-lookup"><span data-stu-id="578ff-108">Chat in channels and group chats differ from personal chat in that the user needs to @mention the bot.</span></span> <span data-ttu-id="578ff-109">如果在多个作用域（个人、groupchat 或通道）中使用了 bot，则需要检测 bot 邮件的作用域，并相应地进行处理。</span><span class="sxs-lookup"><span data-stu-id="578ff-109">If a bot is used in multiple scopes (personal, groupchat or channel) you will need to detect what scope the bot messages came from, and process them accordingly.</span></span>

## <a name="designing-a-great-bot-for-channels-or-groups"></a><span data-ttu-id="578ff-110">为频道或组设计出色的 bot</span><span class="sxs-lookup"><span data-stu-id="578ff-110">Designing a great bot for channels or groups</span></span>

<span data-ttu-id="578ff-111">添加到团队的 bot 成为另一个团队成员，可作为对话的一部分 @mentioned。</span><span class="sxs-lookup"><span data-stu-id="578ff-111">Bots added to a team become another team member, who can be @mentioned as part of the conversation.</span></span> <span data-ttu-id="578ff-112">事实上，bot 仅在 @mentioned 时收到邮件，因此频道上的其他对话不会发送到机器人。</span><span class="sxs-lookup"><span data-stu-id="578ff-112">In fact, bots only receive messages when they are @mentioned, so other conversations on the channel are not sent to the bot.</span></span>

> [!NOTE]
> <span data-ttu-id="578ff-113">为了在回复频道中的 bot 邮件时方便起见，自动将 bot 名称附加到撰写消息框中。</span><span class="sxs-lookup"><span data-stu-id="578ff-113">For convenience when replying to bot messages in a channel, the bot name is prepended in the compose message box automatically.</span></span>

<span data-ttu-id="578ff-114">组或频道中的 bot 应提供与所有成员相关且适用的信息。</span><span class="sxs-lookup"><span data-stu-id="578ff-114">A bot in a group or channel should provide information relevant and appropriate for all members.</span></span> <span data-ttu-id="578ff-115">虽然你的 bot 可以提供与体验相关的任何信息，但请记住，每个人都能看到与之相关的对话。</span><span class="sxs-lookup"><span data-stu-id="578ff-115">While your bot can certainly provide any information relevant to the experience, keep in mind conversations with it are visible to everyone.</span></span> <span data-ttu-id="578ff-116">因此，组或频道中的一个很棒的 bot 应为所有用户添加值，当然不会在一对一对话中无意中共享更多的信息。</span><span class="sxs-lookup"><span data-stu-id="578ff-116">Therefore, a great bot in a group or channel should add value to all users, and certainly not inadvertently share information more appropriate in a one-to-one conversation.</span></span>

<span data-ttu-id="578ff-117">你的 bot 在所有作用域中都可能完全相关，并且不需要执行大量额外的工作来允许你的机器人在它们之间工作。</span><span class="sxs-lookup"><span data-stu-id="578ff-117">Your bot might be entirely relevant in all scopes as is, and no significant extra work is required to allow your bot to work across them.</span></span> <span data-ttu-id="578ff-118">在 Microsoft 团队中，不会认为你的 bot 在所有作用域中都能正常运行，但应确保你的 bot 在你选择支持的任何范围内提供用户值。</span><span class="sxs-lookup"><span data-stu-id="578ff-118">In Microsoft Teams there is no expectation that your bot function in all scopes, but you should ensure your bot provides user value in whichever scope(s) you choose to support.</span></span> <span data-ttu-id="578ff-119">有关作用域的详细信息，请参阅[Microsoft 团队中的应用](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="578ff-119">For more information on scopes, see [Apps in Microsoft Teams](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="578ff-120">开发在组或频道中工作的 bot 使用的功能与个人对话中的功能非常相似。</span><span class="sxs-lookup"><span data-stu-id="578ff-120">Developing a bot that works in groups or channels uses much of the same functionality from personal conversations.</span></span> <span data-ttu-id="578ff-121">有效负载中的其他事件和数据提供团队组和通道信息。</span><span class="sxs-lookup"><span data-stu-id="578ff-121">Additional events and data in the payload provide Teams group and channel information.</span></span> <span data-ttu-id="578ff-122">以下各节介绍了这些差异以及常见功能中的主要差异。</span><span class="sxs-lookup"><span data-stu-id="578ff-122">Those differences, as well as key differences in common functionality are described in the following sections.</span></span>

### <a name="creating-messages"></a><span data-ttu-id="578ff-123">创建邮件</span><span class="sxs-lookup"><span data-stu-id="578ff-123">Creating messages</span></span>

<span data-ttu-id="578ff-124">有关在通道中创建邮件的 bot 的详细信息，请参阅[针对 bot 的主动消息传送](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)，以及专门[创建通道对话](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)。</span><span class="sxs-lookup"><span data-stu-id="578ff-124">For more information on bots creating messages in channels see [Proactive messaging for bots](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md), and specifically [Creating a channel conversation](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation).</span></span>

### <a name="receiving-messages"></a><span data-ttu-id="578ff-125">接收邮件</span><span class="sxs-lookup"><span data-stu-id="578ff-125">Receiving messages</span></span>

<span data-ttu-id="578ff-126">对于组或通道中的 bot，除了[常规邮件架构](https://docs.botframework.com/core-concepts/reference/#activity)之外，你的 bot 也会收到以下属性：</span><span class="sxs-lookup"><span data-stu-id="578ff-126">For a bot in a group or channel, in addition to the [regular message schema](https://docs.botframework.com/core-concepts/reference/#activity), your bot also receives the following properties:</span></span>

* <span data-ttu-id="578ff-127">`channelData`请参阅[团队频道数据](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)。</span><span class="sxs-lookup"><span data-stu-id="578ff-127">`channelData` See [Teams channel data](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data).</span></span> <span data-ttu-id="578ff-128">在组聊天中，包含与该聊天相关的信息。</span><span class="sxs-lookup"><span data-stu-id="578ff-128">In a group chat, contains information specific to that chat.</span></span>
* <span data-ttu-id="578ff-129">`conversation.id`答复链 ID，由通道 ID 和回复链中的第一封邮件的 ID 组成</span><span class="sxs-lookup"><span data-stu-id="578ff-129">`conversation.id` The reply chain ID, consisting of channel ID plus the ID of the first message in the reply chain</span></span>
* <span data-ttu-id="578ff-130">`conversation.isGroup``true`用于频道或组聊天中的 bot 邮件</span><span class="sxs-lookup"><span data-stu-id="578ff-130">`conversation.isGroup` Is `true` for bot messages in channels or group chats</span></span>
* <span data-ttu-id="578ff-131">`conversation.conversationType``groupChat`或者`channel`</span><span class="sxs-lookup"><span data-stu-id="578ff-131">`conversation.conversationType` Either `groupChat` or `channel`</span></span>
* <span data-ttu-id="578ff-132">`entities`可以包含一个或多个提及（请参阅[提及](#-mentions)）</span><span class="sxs-lookup"><span data-stu-id="578ff-132">`entities` Can contain one or more mentions (see [Mentions](#-mentions))</span></span>

### <a name="replying-to-messages"></a><span data-ttu-id="578ff-133">答复邮件</span><span class="sxs-lookup"><span data-stu-id="578ff-133">Replying to messages</span></span>

<span data-ttu-id="578ff-134">若要答复现有邮件，请 [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) 在 .net 或 Node.js 中进行调用 [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) 。</span><span class="sxs-lookup"><span data-stu-id="578ff-134">To reply to an existing message, call [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) in .NET or [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) in Node.js.</span></span> <span data-ttu-id="578ff-135">机器人生成器 SDK 处理所有详细信息。</span><span class="sxs-lookup"><span data-stu-id="578ff-135">The Bot Builder SDK handles all the details.</span></span>

<span data-ttu-id="578ff-136">如果选择使用 REST API，则还可以调用 [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) 终结点。</span><span class="sxs-lookup"><span data-stu-id="578ff-136">If you choose to use the REST API, you can also call the [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) endpoint.</span></span>

<span data-ttu-id="578ff-137">在频道中，回复邮件显示为对启动答复链的答复。</span><span class="sxs-lookup"><span data-stu-id="578ff-137">In a channel, replying to a message shows as a reply to the initiating reply chain.</span></span> <span data-ttu-id="578ff-138">`conversation.id`包含通道和顶级邮件 ID。</span><span class="sxs-lookup"><span data-stu-id="578ff-138">The `conversation.id` contains the channel and the top level message ID.</span></span> <span data-ttu-id="578ff-139">尽管 Bot 框架提供了详细信息，但您可以根据需要将其缓存，以 `conversation.id` 供将来对该会话线程的回复。</span><span class="sxs-lookup"><span data-stu-id="578ff-139">Although the Bot Framework takes care of the details, you can cache that `conversation.id` for future replies to that conversation thread as needed.</span></span>

### <a name="best-practice-welcome-messages-in-teams"></a><span data-ttu-id="578ff-140">最佳实践：团队中的欢迎邮件</span><span class="sxs-lookup"><span data-stu-id="578ff-140">Best practice: Welcome messages in Teams</span></span>

<span data-ttu-id="578ff-141">当你的 bot 第一次添加到组或团队时，向所有用户发送欢迎消息向所有用户引入的欢迎消息通常很有用。</span><span class="sxs-lookup"><span data-stu-id="578ff-141">When your bot is first added to the group or team, it is generally useful to send a welcome message introducing the bot to all users.</span></span> <span data-ttu-id="578ff-142">欢迎消息应提供 bot 功能和用户权益的说明。</span><span class="sxs-lookup"><span data-stu-id="578ff-142">The welcome message should provide a description of the bot’s functionality and user benefits.</span></span> <span data-ttu-id="578ff-143">理想情况下，邮件还应包括用户与应用程序进行交互的命令。</span><span class="sxs-lookup"><span data-stu-id="578ff-143">Ideally the message should also include commands for the user to interact with the app.</span></span> <span data-ttu-id="578ff-144">为此，请确保你的 bot 对邮件做出响应 `conversationUpdate` ，并在 `teamsAddMembers` 对象中使用事件类型 `channelData` 。</span><span class="sxs-lookup"><span data-stu-id="578ff-144">To do this, ensure that your bot responds to the `conversationUpdate` message, with the `teamsAddMembers` eventType in the `channelData` object.</span></span> <span data-ttu-id="578ff-145">`memberAdded`请确保 ID 是 bot 的应用程序 ID 本身，因为当用户添加到团队中时，会发送相同的事件。</span><span class="sxs-lookup"><span data-stu-id="578ff-145">Be sure that the `memberAdded` ID is the bot's App ID itself, because the same event is sent when a user is added to a team.</span></span> <span data-ttu-id="578ff-146">有关更多详细信息，请参阅[团队成员或 bot 添加](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)。</span><span class="sxs-lookup"><span data-stu-id="578ff-146">See [Team member or bot addition](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) for more details.</span></span>

<span data-ttu-id="578ff-147">添加 bot 时，您可能还希望向团队的每个成员发送个人消息。</span><span class="sxs-lookup"><span data-stu-id="578ff-147">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="578ff-148">为此，您可以[提取团队名单](~/resources/bot-v3/bots-context.md#fetching-the-team-roster)并向每个用户发送一[条直接消息](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。</span><span class="sxs-lookup"><span data-stu-id="578ff-148">To do this, you could [fetch the team roster](~/resources/bot-v3/bots-context.md#fetching-the-team-roster) and send each user a [direct message](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md).</span></span>

<span data-ttu-id="578ff-149">建议您在以下情况下*不*发送欢迎邮件：</span><span class="sxs-lookup"><span data-stu-id="578ff-149">We recommend that your bot *not* send a welcome message in the following situations:</span></span>

* <span data-ttu-id="578ff-150">团队规模较大（显然是主观，但例如，大于100个成员）。</span><span class="sxs-lookup"><span data-stu-id="578ff-150">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="578ff-151">你的 bot 可能被视为 "垃圾"，添加它的人可能会收到投诉，除非你清楚地将你的 bot 的价值主张传达给可看到欢迎消息的每个人。</span><span class="sxs-lookup"><span data-stu-id="578ff-151">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="578ff-152">你的 bot 首先在组或频道中提及（而不是首次添加到团队）</span><span class="sxs-lookup"><span data-stu-id="578ff-152">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="578ff-153">重命名组或通道</span><span class="sxs-lookup"><span data-stu-id="578ff-153">A group or channel is renamed</span></span>
* <span data-ttu-id="578ff-154">将团队成员添加到组或通道</span><span class="sxs-lookup"><span data-stu-id="578ff-154">A team member is added to a group or channel</span></span>

## <a name="-mentions"></a><span data-ttu-id="578ff-155">@ 提到</span><span class="sxs-lookup"><span data-stu-id="578ff-155">@ Mentions</span></span>

<span data-ttu-id="578ff-156">由于组或通道中的 bot 仅在邮件中被提及（"@_botname_"）时响应，因此组频道中的 bot 收到的每封邮件都包含其自己的名称，您必须确保您的邮件分析处理该情况。</span><span class="sxs-lookup"><span data-stu-id="578ff-156">Because bots in a group or channel respond only when they are mentioned ("@_botname_") in a message, every message received by a bot in a group channel contains its own name, and you must ensure your message parsing handles that.</span></span> <span data-ttu-id="578ff-157">此外，bot 还可以分析提到的其他用户，并将用户提及为其邮件的一部分。</span><span class="sxs-lookup"><span data-stu-id="578ff-157">In addition, bots can parse out other users mentioned and mention users as part of their messages.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="578ff-158">检索提及</span><span class="sxs-lookup"><span data-stu-id="578ff-158">Retrieving mentions</span></span>

<span data-ttu-id="578ff-159">提到在 `entities` 有效负载的对象中返回，并且包含用户的唯一 ID，在大多数情况下，提到的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="578ff-159">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="578ff-160">您可以通过在用于 .NET 的 Bot 生成器 SDK 中调用函数来检索邮件中的所有提及 `GetMentions` ，这将返回对象的数组 `Mentioned` 。</span><span class="sxs-lookup"><span data-stu-id="578ff-160">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK for .NET, which returns an array of `Mentioned` objects.</span></span>

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="578ff-161">.NET 示例代码：检查并去除 @bot 提及</span><span class="sxs-lookup"><span data-stu-id="578ff-161">.NET example code: Check for and strip @bot mention</span></span>

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
> <span data-ttu-id="578ff-162">您还可以使用 "团队扩展 `GetTextWithoutMentions` " 功能，该函数将去除所有提及内容，包括 bot。</span><span class="sxs-lookup"><span data-stu-id="578ff-162">You can also use the Teams extension function `GetTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a><span data-ttu-id="578ff-163">Node.js 示例代码：检查并去除 @bot 提及的内容</span><span class="sxs-lookup"><span data-stu-id="578ff-163">Node.js example code: Check for and strip @bot mention</span></span>

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

<span data-ttu-id="578ff-164">您还可以使用 "团队扩展 `getTextWithoutMentions` " 功能，该函数将去除所有提及内容，包括 bot。</span><span class="sxs-lookup"><span data-stu-id="578ff-164">You can also use the Teams extension function `getTextWithoutMentions`, which strips out all mentions, including the bot.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="578ff-165">构建提及</span><span class="sxs-lookup"><span data-stu-id="578ff-165">Constructing mentions</span></span>

<span data-ttu-id="578ff-166">你的 bot 可以在发送到频道的邮件中提及其他用户。</span><span class="sxs-lookup"><span data-stu-id="578ff-166">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="578ff-167">若要执行此操作，您的邮件必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="578ff-167">To do this, your message must do the following:</span></span>

* <span data-ttu-id="578ff-168">`<at>@username</at>`在邮件文本中包含</span><span class="sxs-lookup"><span data-stu-id="578ff-168">Include `<at>@username</at>` in the message text</span></span>
* <span data-ttu-id="578ff-169">`mention`将对象包括在实体集合中</span><span class="sxs-lookup"><span data-stu-id="578ff-169">Include the `mention` object inside the entities collection</span></span>

#### <a name="net-example"></a><span data-ttu-id="578ff-170">.NET 示例</span><span class="sxs-lookup"><span data-stu-id="578ff-170">.NET example</span></span>

<span data-ttu-id="578ff-171">本示例使用的是 ".[团队](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)" NuGet 包。</span><span class="sxs-lookup"><span data-stu-id="578ff-171">This example uses the [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet package.</span></span>

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a><span data-ttu-id="578ff-172">Node.js 示例</span><span class="sxs-lookup"><span data-stu-id="578ff-172">Node.js example</span></span>

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

#### <a name="example-outgoing-message-with-user-mentioned"></a><span data-ttu-id="578ff-173">示例：提到的用户的传出邮件</span><span class="sxs-lookup"><span data-stu-id="578ff-173">Example: Outgoing message with user mentioned</span></span>

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

## <a name="accessing-groupchat-or-channel-scope"></a><span data-ttu-id="578ff-174">访问 groupChat 或通道范围</span><span class="sxs-lookup"><span data-stu-id="578ff-174">Accessing groupChat or channel scope</span></span>

<span data-ttu-id="578ff-175">你的 bot 可以执行的操作不仅仅是在组和团队中发送和接收邮件。</span><span class="sxs-lookup"><span data-stu-id="578ff-175">Your bot can do more than send and receive messages in groups and teams.</span></span> <span data-ttu-id="578ff-176">例如，它还可以提取成员列表，包括其配置文件信息和通道列表。</span><span class="sxs-lookup"><span data-stu-id="578ff-176">For instance, it can also fetch the list of members, including their profile information, as well as the list of channels.</span></span> <span data-ttu-id="578ff-177">若要了解详细信息，请参阅[获取 Microsoft 团队 bot 的上下文](~/resources/bot-v3/bots-context.md)。</span><span class="sxs-lookup"><span data-stu-id="578ff-177">See [Get context for your Microsoft Teams bot](~/resources/bot-v3/bots-context.md) to learn more.</span></span>

<span data-ttu-id="578ff-178">*另请参阅* [Bot 框架示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="578ff-178">*See also* [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>
