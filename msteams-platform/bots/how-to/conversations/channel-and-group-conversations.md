---
title: 使用机器人进行频道和群组对话
author: clearab
description: 如何在频道或群聊中发送、接收和处理机器人的消息。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 8a9a58208fff5cc2fe376fcb9932bad6ac2bf36f
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797839"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="826c4-103">与 Microsoft Teams 自动程序进行频道和群组聊天对话</span><span class="sxs-lookup"><span data-stu-id="826c4-103">Channel and group chat conversations with a Microsoft Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="826c4-104">通过将或范围添加到自动程序，可以安装在团队或群聊 `teams` `groupchat` 中。</span><span class="sxs-lookup"><span data-stu-id="826c4-104">By adding the `teams` or `groupchat` scope to your bot, it can be available to be installed in a team or group chat.</span></span> <span data-ttu-id="826c4-105">这允许对话的所有成员与机器人交互。</span><span class="sxs-lookup"><span data-stu-id="826c4-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="826c4-106">安装后，它还可以访问对话的元数据（如对话成员列表）以及当安装在有关该团队的团队详细信息和频道的完整列表中时。</span><span class="sxs-lookup"><span data-stu-id="826c4-106">Once installed, it will also have access to metadata about the conversation like the list of conversation members, and when installed in a team details about that team and the full list of channels.</span></span>

<span data-ttu-id="826c4-107">组或频道中的聊天机器人仅在 (@botname) 时接收消息，不会收到发送到对话的其他任何消息。</span><span class="sxs-lookup"><span data-stu-id="826c4-107">Bots in a group or channel only receive messages when they are mentioned (@botname), they do not receive any other messages sent to the conversation.</span></span>

> [!NOTE]
> <span data-ttu-id="826c4-108">必须直接@mentioned自动程序。</span><span class="sxs-lookup"><span data-stu-id="826c4-108">The bot must be @mentioned directly.</span></span> <span data-ttu-id="826c4-109">当提及团队或频道时，或者当有人回复来自自动程序的邮件时，系统不会收到@mentioning消息。</span><span class="sxs-lookup"><span data-stu-id="826c4-109">Your bot will not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

## <a name="design-guidelines"></a><span data-ttu-id="826c4-110">设计准则</span><span class="sxs-lookup"><span data-stu-id="826c4-110">Design guidelines</span></span>

<span data-ttu-id="826c4-111">了解如何在 [频道和聊天中设计机器人对话](~/bots/design/bots.md)。</span><span class="sxs-lookup"><span data-stu-id="826c4-111">See how to [design bot conversations in channels and chats](~/bots/design/bots.md).</span></span>

## <a name="creating-new-conversation-threads"></a><span data-ttu-id="826c4-112">创建新的对话线程</span><span class="sxs-lookup"><span data-stu-id="826c4-112">Creating new conversation threads</span></span>

<span data-ttu-id="826c4-113">在团队中安装自动程序时，有时可能需要创建新的对话线程，而不是回复现有的对话线程。</span><span class="sxs-lookup"><span data-stu-id="826c4-113">When your bot is installed in a team, it can sometimes be necessary to create a new conversation thread rather than replying to an existing one.</span></span> <span data-ttu-id="826c4-114">这是一种 [主动消息形式](~/bots/how-to/conversations/send-proactive-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="826c4-114">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

## <a name="working-with-mentions"></a><span data-ttu-id="826c4-115">使用提及</span><span class="sxs-lookup"><span data-stu-id="826c4-115">Working with mentions</span></span>

<span data-ttu-id="826c4-116">从组或频道发送到自动程序的每封邮件都将包含一个@mention在消息文本中具有自己的名称，因此你将需要确保邮件分析能够处理这一点。</span><span class="sxs-lookup"><span data-stu-id="826c4-116">Every message to your bot from a group or channel will contain an @mention with its own name in the message text, so you'll need to ensure your message parsing handles that.</span></span> <span data-ttu-id="826c4-117">机器人还可以检索邮件中提到的其他用户，并将提及内容添加到它发送的任何邮件中。</span><span class="sxs-lookup"><span data-stu-id="826c4-117">Your bot can also retrieve other users mentioned in a message, and add mentions to any messages it sends.</span></span>

### <a name="stripping-mentions-from-message-text"></a><span data-ttu-id="826c4-118">从邮件文本中去除提及</span><span class="sxs-lookup"><span data-stu-id="826c4-118">Stripping mentions from message text</span></span>

<span data-ttu-id="826c4-119">你可能会发现有必要从自动程序@mentions文本中去除此限制。</span><span class="sxs-lookup"><span data-stu-id="826c4-119">You may find it necessary to strip out the @mentions from the text of the message your bot receives.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="826c4-120">检索提及</span><span class="sxs-lookup"><span data-stu-id="826c4-120">Retrieving mentions</span></span>

<span data-ttu-id="826c4-121">在有效负载的对象中返回提及内容，同时包含用户的唯一 ID，在大多数情况下，还包含 `entities` 提及的用户名称。</span><span class="sxs-lookup"><span data-stu-id="826c4-121">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="826c4-122">邮件的文本还将包含类似提及的内容 `<at>@John Smith<at>` 。</span><span class="sxs-lookup"><span data-stu-id="826c4-122">The text of the message will also include the mention like `<at>@John Smith<at>`.</span></span> <span data-ttu-id="826c4-123">但是，不应依赖邮件中的文本来检索有关用户的任何信息;发送邮件的人可以更改它。</span><span class="sxs-lookup"><span data-stu-id="826c4-123">However, you should not rely on the text in the message to retrieve any information about the user; it is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="826c4-124">请改为使用 `entities` 对象。</span><span class="sxs-lookup"><span data-stu-id="826c4-124">Instead, use the `entities` object.</span></span>

<span data-ttu-id="826c4-125">可以通过调用返回对象数组的 Bot Builder SDK 中的函数来检索邮件中提及 `GetMentions` `Mention` 的所有内容。</span><span class="sxs-lookup"><span data-stu-id="826c4-125">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK which returns an array of `Mention` objects.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="826c4-126">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="826c4-126">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    Mention[] mentions = turnContext.Activity.GetMentions();
    if(mentions != null)
    {
        ChannelAccount firstMention = mentions[0].Mentioned;
        await turnContext.SendActivityAsync($"Hello {firstMention.Name}");
    }
    else
    {
        await turnContext.SendActivityAsync("Aw, no one was mentioned.");
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="826c4-127">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="826c4-127">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mentions = TurnContext.getMentions(turnContext.activity);
    if (mentions){
        const firstMention = mentions[0].mentioned;
        await turnContext.sendActivity(`Hello ${firstMention.name}.`);
    } else {
        await turnContext.sendActivity(`Aw, no one was mentioned.`);
    }

    await next();
});
```

# <a name="json"></a>[<span data-ttu-id="826c4-128">JSON</span><span class="sxs-lookup"><span data-stu-id="826c4-128">JSON</span></span>](#tab/json)

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
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

# <a name="python"></a>[<span data-ttu-id="826c4-129">Python</span><span class="sxs-lookup"><span data-stu-id="826c4-129">Python</span></span>](#tab/python)

```python
@staticmethod
def get_mentions(activity: Activity) -> List[Mention]:
    result: List[Mention] = []
    if activity.entities is not None:
        for entity in activity.entities:
            if entity.type.lower() == "mention":
                    result.append(entity)
     return result
```

* * *

### <a name="adding-mentions-to-your-messages"></a><span data-ttu-id="826c4-130">向邮件添加提及</span><span class="sxs-lookup"><span data-stu-id="826c4-130">Adding mentions to your messages</span></span>

<span data-ttu-id="826c4-131">机器人可以在张贴到频道的消息中提及其他用户。</span><span class="sxs-lookup"><span data-stu-id="826c4-131">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="826c4-132">为此，您的邮件必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="826c4-132">To do this, your message must do the following:</span></span>

<span data-ttu-id="826c4-133">`Mention`该对象具有两个需要设置的属性：</span><span class="sxs-lookup"><span data-stu-id="826c4-133">The `Mention` object has two properties that you will need to set:</span></span>

* <span data-ttu-id="826c4-134">将 <at>@username</at> 包括在邮件文本中</span><span class="sxs-lookup"><span data-stu-id="826c4-134">Include <at>@username</at> in the message text</span></span>
* <span data-ttu-id="826c4-135">在实体集合中包括 mention 对象</span><span class="sxs-lookup"><span data-stu-id="826c4-135">Include the mention object inside the entities collection</span></span>

<span data-ttu-id="826c4-136">Bot Framework SDK 提供了帮助程序方法和对象，以便更轻松地构建提及。</span><span class="sxs-lookup"><span data-stu-id="826c4-136">The Bot Framework SDK provides helper methods and objects to make constructing the mention easier.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="826c4-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="826c4-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
    var mention = new Mention
    {
        Mentioned = turnContext.Activity.From,
        Text = $"<at>{XmlConvert.EncodeName(turnContext.Activity.From.Name)}</at>",
    };

    var replyActivity = MessageFactory.Text($"Hello {mention.Text}.");
    replyActivity.Entities = new List<Entity> { mention };

    await turnContext.SendActivityAsync(replyActivity, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="826c4-138">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="826c4-138">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    const mention = {
        mentioned: turnContext.activity.from,
        text: `<at>${ new TextEncoder().encode(turnContext.activity.from.name) }</at>`,
    } as Mention;

    const replyActivity = MessageFactory.text(`Hello ${mention.text}`);
    replyActivity.entities = [mention];

    await turnContext.sendActivity(replyActivity);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="json"></a>[<span data-ttu-id="826c4-139">JSON</span><span class="sxs-lookup"><span data-stu-id="826c4-139">JSON</span></span>](#tab/json)

<span data-ttu-id="826c4-140">`text`数组中对象中的 `entities` 字段必须与邮件字段的一部分完全 `text` 匹配。</span><span class="sxs-lookup"><span data-stu-id="826c4-140">The `text` field in the object in the `entities` array must *exactly* match a portion of the message `text` field.</span></span> <span data-ttu-id="826c4-141">如果没有，则忽略提及。</span><span class="sxs-lookup"><span data-stu-id="826c4-141">If it does not, the mention will be ignored.</span></span>

```json
{
    "type": "message",
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "29:9e52142b-5e5e-4d7b-bb3e-e82dcf620000",
        "name": "Jane Smith"
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

# <a name="python"></a>[<span data-ttu-id="826c4-142">Python</span><span class="sxs-lookup"><span data-stu-id="826c4-142">Python</span></span>](#tab/python)

```python
async def _mention_activity(self, turn_context: TurnContext):
        mention = Mention(
            mentioned=turn_context.activity.from_property,
            text=f"<at>{turn_context.activity.from_property.name}</at>",
            type="mention"
        )

        reply_activity = MessageFactory.text(f"Hello {mention.text}")
        reply_activity.entities = [Mention().deserialize(mention.serialize())]
        await turn_context.send_activity(reply_activity)
```

* * *

## <a name="sending-a-message-on-installation"></a><span data-ttu-id="826c4-143">在安装时发送邮件</span><span class="sxs-lookup"><span data-stu-id="826c4-143">Sending a message on installation</span></span>

<span data-ttu-id="826c4-144">首次将机器人添加到组或团队时，发送介绍它的消息可能很有用。</span><span class="sxs-lookup"><span data-stu-id="826c4-144">When your bot is first added to the group or team, it may be useful to send a message introducing it.</span></span> <span data-ttu-id="826c4-145">该消息应提供自动程序功能的简要说明及其使用方法。</span><span class="sxs-lookup"><span data-stu-id="826c4-145">The message should provide a brief description of the bot's features, and how to use them.</span></span> <span data-ttu-id="826c4-146">你需要使用 `conversationUpdate` `teamMemberAdded` eventType 订阅事件。</span><span class="sxs-lookup"><span data-stu-id="826c4-146">You'll want to subscribe to the `conversationUpdate` event, with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="826c4-147">由于在添加任何新团队成员时发送事件，因此需要检查以确定添加的团队成员是否为机器人。</span><span class="sxs-lookup"><span data-stu-id="826c4-147">Since the event is sent when any new team member is added, you need to check to determine if the new member added is the bot.</span></span> <span data-ttu-id="826c4-148">有关 [更多详细信息，请参阅向新团队成员](~/bots/how-to/conversations/send-proactive-messages.md) 发送欢迎消息。</span><span class="sxs-lookup"><span data-stu-id="826c4-148">See [Sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md) for more details.</span></span>

<span data-ttu-id="826c4-149">添加自动程序时，你可能还需要向团队的每个成员发送个人消息。</span><span class="sxs-lookup"><span data-stu-id="826c4-149">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="826c4-150">为此，你可以获取团队名单，并给每个用户发送直接消息。</span><span class="sxs-lookup"><span data-stu-id="826c4-150">To do this, you could get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="826c4-151">不建议在下列情况下发送邮件：</span><span class="sxs-lookup"><span data-stu-id="826c4-151">It is not recommended to send a message in the following situations:</span></span>

* <span data-ttu-id="826c4-152">团队规模较大 (明显具有主观性，但例如超过 100 个成员) 。</span><span class="sxs-lookup"><span data-stu-id="826c4-152">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="826c4-153">你的自动程序可能会被视为"spa一"，并且添加它的人可能会收到投诉，除非你向看到欢迎消息的每个人清楚地传达了机器人的价值主张。</span><span class="sxs-lookup"><span data-stu-id="826c4-153">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="826c4-154">你的自动程序首先在组或频道 (提及，而不是先添加到团队) </span><span class="sxs-lookup"><span data-stu-id="826c4-154">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="826c4-155">重命名组或频道</span><span class="sxs-lookup"><span data-stu-id="826c4-155">A group or channel is renamed</span></span>
* <span data-ttu-id="826c4-156">将团队成员添加到组或频道</span><span class="sxs-lookup"><span data-stu-id="826c4-156">A team member is added to a group or channel</span></span>

## <a name="learn-more"></a><span data-ttu-id="826c4-157">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="826c4-157">Learn more</span></span>

<span data-ttu-id="826c4-158">机器人可以访问有关其安装的群聊或团队的其他信息。</span><span class="sxs-lookup"><span data-stu-id="826c4-158">Your bot has access to additional information about the group chat or team it is installed in.</span></span> <span data-ttu-id="826c4-159">请参阅 [获取适用于机器人](~/bots/how-to/get-teams-context.md) 的其他 API 的团队上下文。</span><span class="sxs-lookup"><span data-stu-id="826c4-159">See [get teams context](~/bots/how-to/get-teams-context.md) for additional APIs available for your bot.</span></span>

<span data-ttu-id="826c4-160">此外，机器人还可以订阅和响应其他事件。</span><span class="sxs-lookup"><span data-stu-id="826c4-160">There are also additional events that your bot can subscribe and respond to.</span></span> <span data-ttu-id="826c4-161">请参阅 [订阅对话事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md) 以了解方式。</span><span class="sxs-lookup"><span data-stu-id="826c4-161">See [subscribe to conversation events](~/bots/how-to/conversations/subscribe-to-conversation-events.md) to learn how.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
