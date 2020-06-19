---
title: 频道和群组对话
author: clearab
description: 如何：在频道或组聊天中发送、接收和处理机器人的邮件。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: ccc27d7638820cfa3c2b7cfe12b91b3a3a9fef1d
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2020
ms.locfileid: "44801149"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a><span data-ttu-id="6b6f0-103">与 Microsoft 团队 bot 的频道和组聊天对话</span><span class="sxs-lookup"><span data-stu-id="6b6f0-103">Channel and Group chat conversations with a Microsoft Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="6b6f0-104">通过将 `teams` 或 `groupchat` 作用域添加到你的 bot，可以在团队或组聊天中安装它。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-104">By adding the `teams` or `groupchat` scope to your bot, it can be available to be installed in a team or group chat.</span></span> <span data-ttu-id="6b6f0-105">这样，对话的所有成员都可以与你的 bot 进行交互。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="6b6f0-106">一旦安装，它还可以访问有关会话的元数据，如会话成员的列表，以及在团队详细信息中安装的有关该团队和频道的完整列表。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-106">Once installed, it will also have access to metadata about the conversation like the list of conversation members, and when installed in a team details about that team and the full list of channels.</span></span>

<span data-ttu-id="6b6f0-107">组或频道中的 bot 仅在提到邮件时才接收邮件（"@botname"），它们不会收到发送到对话的任何其他邮件。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-107">Bots in a group or channel only receive messages when they are mentioned ("@botname"), they do not receive any other messages sent to the conversation.</span></span>

> [!NOTE]
> <span data-ttu-id="6b6f0-108">必须直接 @mentioned 机器人。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-108">The bot must be @mentioned directly.</span></span> <span data-ttu-id="6b6f0-109">在提到团队或频道时，或当某人从你的 bot 回复邮件时不 @mentioning 它，你的 bot 将不会收到邮件。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-109">Your bot will not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

## <a name="design-considerations"></a><span data-ttu-id="6b6f0-110">设计注意事项</span><span class="sxs-lookup"><span data-stu-id="6b6f0-110">Design considerations</span></span>

<span data-ttu-id="6b6f0-111">Bot 应提供与组或通道中的所有成员都适用且相关的信息。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-111">A bot should provide information that is both appropriate and relevant to all members in a group or channel.</span></span> <span data-ttu-id="6b6f0-112">包含该组或频道的所有人都能看到与其相关的对话。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-112">Conversations with it are visible to everyone that is a part of the group or channel.</span></span> <span data-ttu-id="6b6f0-113">设计良好的 bot 可以为所有用户增加价值，同时不会在不小心的情况下共享更适合一对一对话的信息。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-113">A well designed bot can add value to all users while not inadvertently sharing information that is more appropriate in a one-to-one conversation.</span></span> <span data-ttu-id="6b6f0-114">应避免使用对话之类的多个对话-请改用卡片和/或任务模块来收集信息。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-114">Multi-turn conversations like dialogs should be avoided - use cards and/or task modules to collect information instead.</span></span>

## <a name="creating-new-conversation-threads"></a><span data-ttu-id="6b6f0-115">创建新的对话线索</span><span class="sxs-lookup"><span data-stu-id="6b6f0-115">Creating new conversation threads</span></span>

<span data-ttu-id="6b6f0-116">当你的 bot 安装在团队中时，有时可能需要创建新的会话线程，而不是答复现有的会话线程。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-116">When your bot is installed in a team, it can sometimes be necessary to create a new conversation thread rather than replying to an existing one.</span></span> <span data-ttu-id="6b6f0-117">这是一种[主动消息传递](~/bots/how-to/conversations/send-proactive-messages.md)形式。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-117">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

## <a name="working-with-mentions"></a><span data-ttu-id="6b6f0-118">处理提及</span><span class="sxs-lookup"><span data-stu-id="6b6f0-118">Working with mentions</span></span>

<span data-ttu-id="6b6f0-119">来自组或频道的每封邮件都将在邮件文本中包含其自己的名称的 @mention，因此您需要确保您的邮件分析处理该邮件。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-119">Every message to your bot from a group or channel will contain an @mention with its own name in the message text, so you'll need to ensure your message parsing handles that.</span></span> <span data-ttu-id="6b6f0-120">你的 bot 还可以检索邮件中提及的其他用户，并将提及添加到它发送的任何邮件中。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-120">Your bot can also retrieve other users mentioned in a message, and add mentions to any messages it sends.</span></span>

### <a name="stripping-mentions-from-message-text"></a><span data-ttu-id="6b6f0-121">从邮件文本中去除提及</span><span class="sxs-lookup"><span data-stu-id="6b6f0-121">Stripping mentions from message text</span></span>

<span data-ttu-id="6b6f0-122">你可能会发现需要从你的 bot 接收的邮件的文本中去除 @mentions。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-122">You may find it necessary to strip out the @mentions from the text of the message your bot receives.</span></span>

### <a name="retrieving-mentions"></a><span data-ttu-id="6b6f0-123">检索提及</span><span class="sxs-lookup"><span data-stu-id="6b6f0-123">Retrieving mentions</span></span>

<span data-ttu-id="6b6f0-124">提到在 `entities` 有效负载的对象中返回，并且包含用户的唯一 ID，在大多数情况下，提到的用户的名称。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-124">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and, in most cases, the name of user mentioned.</span></span> <span data-ttu-id="6b6f0-125">邮件文本中还包括提及的 like `<at>@John Smith<at>` 。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-125">The text of the message will also include the mention like `<at>@John Smith<at>`.</span></span> <span data-ttu-id="6b6f0-126">但是，不应依赖邮件中的文本来检索有关用户的任何信息;发送邮件的人可以对其进行更改。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-126">However, you should not rely on the text in the message to retrieve any information about the user; it is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="6b6f0-127">而是使用 `entities` 对象。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-127">Instead, use the `entities` object.</span></span>

<span data-ttu-id="6b6f0-128">您可以通过调用自动程序生成器 SDK 中的函数来检索邮件中的所有提及， `GetMentions` 这将返回 `Mention` 对象的数组。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-128">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK which returns an array of `Mention` objects.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6b6f0-129">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6b6f0-129">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6b6f0-130">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6b6f0-130">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="6b6f0-131">JSON</span><span class="sxs-lookup"><span data-stu-id="6b6f0-131">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="6b6f0-132">Python</span><span class="sxs-lookup"><span data-stu-id="6b6f0-132">Python</span></span>](#tab/python)

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

### <a name="adding-mentions-to-your-messages"></a><span data-ttu-id="6b6f0-133">将提及添加到邮件</span><span class="sxs-lookup"><span data-stu-id="6b6f0-133">Adding mentions to your messages</span></span>

<span data-ttu-id="6b6f0-134">你的 bot 可以在发送到频道的邮件中提及其他用户。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-134">Your bot can mention other users in messages posted into channels.</span></span> <span data-ttu-id="6b6f0-135">若要执行此操作，您的邮件必须执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="6b6f0-135">To do this, your message must do the following:</span></span>

<span data-ttu-id="6b6f0-136">`Mention`对象具有两个需要设置的属性：</span><span class="sxs-lookup"><span data-stu-id="6b6f0-136">The `Mention` object has two properties that you will need to set:</span></span>

* <span data-ttu-id="6b6f0-137">在邮件文本中包含<at>@username</at></span><span class="sxs-lookup"><span data-stu-id="6b6f0-137">Include <at>@username</at> in the message text</span></span>
* <span data-ttu-id="6b6f0-138">在实体集合中包含提及的对象</span><span class="sxs-lookup"><span data-stu-id="6b6f0-138">Include the mention object inside the entities collection</span></span>

<span data-ttu-id="6b6f0-139">Bot 框架 SDK 提供帮助程序方法和对象，以使所提及的更简单的构造更简单。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-139">The Bot Framework SDK provides helper methods and objects to make constructing the mention easier.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6b6f0-140">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6b6f0-140">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6b6f0-141">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6b6f0-141">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="6b6f0-142">JSON</span><span class="sxs-lookup"><span data-stu-id="6b6f0-142">JSON</span></span>](#tab/json)

<span data-ttu-id="6b6f0-143">`text`数组中的对象中的字段 `entities` 必须与消息字段的一部分*完全*匹配 `text` 。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-143">The `text` field in the object in the `entities` array must *exactly* match a portion of the message `text` field.</span></span> <span data-ttu-id="6b6f0-144">如果不是，则将忽略提及。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-144">If it does not, the mention will be ignored.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="6b6f0-145">Python</span><span class="sxs-lookup"><span data-stu-id="6b6f0-145">Python</span></span>](#tab/python)

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

## <a name="sending-a-message-on-installation"></a><span data-ttu-id="6b6f0-146">在安装时发送邮件</span><span class="sxs-lookup"><span data-stu-id="6b6f0-146">Sending a message on installation</span></span>

<span data-ttu-id="6b6f0-147">当你的 bot 第一次添加到组或团队时，发送引入邮件的消息可能很有用。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-147">When your bot is first added to the group or team, it may be useful to send a message introducing it.</span></span> <span data-ttu-id="6b6f0-148">邮件应提供机器人功能的简短说明以及如何使用它们。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-148">The message should provide a brief description of the bot's features, and how to use them.</span></span> <span data-ttu-id="6b6f0-149">你将需要 `conversationUpdate` 使用事件，来订阅事件 `teamMemberAdded` 。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-149">You'll want to subscribe to the `conversationUpdate` event, with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="6b6f0-150">由于添加任何新的团队成员时都会发送事件，因此您需要进行检查以确定添加的新成员是否为 bot。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-150">Since the event is sent when any new team member is added, you need to check to determine if the new member added is the bot.</span></span> <span data-ttu-id="6b6f0-151">有关更多详细信息，请参阅[向新的团队成员发送欢迎消息](~/bots/how-to/conversations/send-proactive-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-151">See [Sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md) for more details.</span></span>

<span data-ttu-id="6b6f0-152">添加 bot 时，您可能还希望向团队的每个成员发送个人消息。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-152">You might also want to send a personal message to each member of the team when the bot is added.</span></span> <span data-ttu-id="6b6f0-153">为此，您可以获取团队名单并向每个用户发送一条直接消息。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-153">To do this, you could get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="6b6f0-154">在下列情况下，不建议发送邮件：</span><span class="sxs-lookup"><span data-stu-id="6b6f0-154">It is not recommended to send a message in the following situations:</span></span>

* <span data-ttu-id="6b6f0-155">团队规模较大（显然是主观，但例如，大于100个成员）。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-155">The team is large (obviously subjective, but for example larger than 100 members).</span></span> <span data-ttu-id="6b6f0-156">你的 bot 可能被视为 "垃圾"，添加它的人可能会收到投诉，除非你清楚地将你的 bot 的价值主张传达给可看到欢迎消息的每个人。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-156">Your bot may be seen as 'spammy' and the person who added it may get complaints unless you clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="6b6f0-157">你的 bot 首先在组或频道中提及（而不是首次添加到团队）</span><span class="sxs-lookup"><span data-stu-id="6b6f0-157">Your bot is first mentioned in a group or channel (versus being first added to a team)</span></span>
* <span data-ttu-id="6b6f0-158">重命名组或通道</span><span class="sxs-lookup"><span data-stu-id="6b6f0-158">A group or channel is renamed</span></span>
* <span data-ttu-id="6b6f0-159">将团队成员添加到组或通道</span><span class="sxs-lookup"><span data-stu-id="6b6f0-159">A team member is added to a group or channel</span></span>

## <a name="learn-more"></a><span data-ttu-id="6b6f0-160">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="6b6f0-160">Learn more</span></span>

<span data-ttu-id="6b6f0-161">你的 bot 可以访问有关安装了的组聊天或团队的其他信息。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-161">Your bot has access to additional information about the group chat or team it is installed in.</span></span> <span data-ttu-id="6b6f0-162">有关为你的 bot 提供的其他 Api，请参阅[获取团队上下文](~/bots/how-to/get-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-162">See [get teams context](~/bots/how-to/get-teams-context.md) for additional APIs available for your bot.</span></span>

<span data-ttu-id="6b6f0-163">此外，你的 bot 也可以订阅和响应的其他事件。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-163">There are also additional events that your bot can subscribe and respond to.</span></span> <span data-ttu-id="6b6f0-164">若要了解如何操作，请参阅[订阅对话事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。</span><span class="sxs-lookup"><span data-stu-id="6b6f0-164">See [subscribe to conversation events](~/bots/how-to/conversations/subscribe-to-conversation-events.md) to learn how.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
