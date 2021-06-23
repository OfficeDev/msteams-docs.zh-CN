---
title: 与机器人的频道和群组对话
author: surbhigupta
description: 如何发送、接收和处理频道或群聊中机器人的消息。
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 399f7d7487b4992e70d4ee515b26101e2b253a62
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069002"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a><span data-ttu-id="51671-103">与机器人的频道和群组聊天对话</span><span class="sxs-lookup"><span data-stu-id="51671-103">Channel and group chat conversations with a bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="51671-104">若要在团队Microsoft Teams聊天中安装聊天机器人，请向 `teams` 自动程序添加 或 `groupchat` 范围。</span><span class="sxs-lookup"><span data-stu-id="51671-104">To install the Microsoft Teams bot in a team or group chat, add the `teams` or `groupchat` scope to your bot.</span></span> <span data-ttu-id="51671-105">此操作允许对话的所有成员与你的机器人互动。</span><span class="sxs-lookup"><span data-stu-id="51671-105">This allows all members of the conversation to interact with your bot.</span></span> <span data-ttu-id="51671-106">安装自动程序后，它有权访问有关对话的元数据，如对话成员列表。</span><span class="sxs-lookup"><span data-stu-id="51671-106">After the bot is installed, it has access to metadata about the conversation, such as the list of conversation members.</span></span> <span data-ttu-id="51671-107">此外，当在团队中安装它时，机器人可以访问有关该团队的详细信息和频道的完整列表。</span><span class="sxs-lookup"><span data-stu-id="51671-107">Also, when it is installed in a team, the bot has access to details about that team and the full list of channels.</span></span>

<span data-ttu-id="51671-108">组或频道中的聊天机器人仅在被提及时接收@botname。</span><span class="sxs-lookup"><span data-stu-id="51671-108">Bots in a group or channel only receive messages when they are mentioned @botname.</span></span> <span data-ttu-id="51671-109">他们不会收到发送到对话的其他任何消息。</span><span class="sxs-lookup"><span data-stu-id="51671-109">They do not receive any other messages sent to the conversation.</span></span> <span data-ttu-id="51671-110">必须直接 @mentioned 机器人。</span><span class="sxs-lookup"><span data-stu-id="51671-110">The bot must be @mentioned directly.</span></span> <span data-ttu-id="51671-111">当提到团队或频道时，或者当有人从你的机器人回复消息时，没有回复消息时，@mentioning消息。</span><span class="sxs-lookup"><span data-stu-id="51671-111">Your bot does not receive a message when the team or channel is mentioned, or when someone replies to a message from your bot without @mentioning it.</span></span>

> [!NOTE]
> <span data-ttu-id="51671-112">此功能目前仅适用于公共 [开发人员预览](../../../resources/dev-preview/developer-preview-intro.md) 版。</span><span class="sxs-lookup"><span data-stu-id="51671-112">This feature is currently available in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md) only.</span></span>
>
> <span data-ttu-id="51671-113">通过使用 RSC (资源) ，机器人可以接收团队中安装它的所有频道消息，而无需@mentioned。</span><span class="sxs-lookup"><span data-stu-id="51671-113">Using resource-specific consent (RSC), bots can receive all channel messages in teams that it is installed in without being @mentioned.</span></span> <span data-ttu-id="51671-114">有关详细信息，请参阅使用 [RSC 接收所有频道消息](channel-messages-with-rsc.md)。</span><span class="sxs-lookup"><span data-stu-id="51671-114">For more information, see [receive all channel messages with RSC](channel-messages-with-rsc.md).</span></span>

## <a name="design-guidelines"></a><span data-ttu-id="51671-115">设计准则</span><span class="sxs-lookup"><span data-stu-id="51671-115">Design guidelines</span></span>

<span data-ttu-id="51671-116">与个人聊天不同，在群聊和频道中，机器人必须提供快速简介。</span><span class="sxs-lookup"><span data-stu-id="51671-116">Unlike personal chats, in group chats and channels, your bot must provide a quick introduction.</span></span> <span data-ttu-id="51671-117">必须遵循这些以及更多自动程序设计指南。</span><span class="sxs-lookup"><span data-stu-id="51671-117">You must follow these and more bot design guidelines.</span></span> <span data-ttu-id="51671-118">若要详细了解如何在聊天中设计聊天机器人Teams，请参阅如何在频道和聊天中设计[机器人对话](~/bots/design/bots.md)。</span><span class="sxs-lookup"><span data-stu-id="51671-118">For more information on how to design bots in Teams, see [how to design bot conversations in channels and chats](~/bots/design/bots.md).</span></span>

<span data-ttu-id="51671-119">现在，你可以创建新的对话线程并轻松管理频道中的不同对话。</span><span class="sxs-lookup"><span data-stu-id="51671-119">Now, you can create new conversation threads and easily manage different conversations in channels.</span></span>

## <a name="create-new-conversation-threads"></a><span data-ttu-id="51671-120">创建新的对话线程</span><span class="sxs-lookup"><span data-stu-id="51671-120">Create new conversation threads</span></span>

<span data-ttu-id="51671-121">在团队中安装自动程序时，必须创建新的对话线程，而不是答复现有对话线程。</span><span class="sxs-lookup"><span data-stu-id="51671-121">When your bot is installed in a team, you must create a new conversation thread rather than reply to an existing one.</span></span> <span data-ttu-id="51671-122">有时很难区分两个对话。</span><span class="sxs-lookup"><span data-stu-id="51671-122">At times it is difficult to differentiate between two conversations.</span></span> <span data-ttu-id="51671-123">如果会话是按线索组织的，则更易于组织和管理频道中的不同对话。</span><span class="sxs-lookup"><span data-stu-id="51671-123">If the conversation is threaded, it is easier to organize and manage different conversations in channels.</span></span> <span data-ttu-id="51671-124">这是一种 [主动消息形式](~/bots/how-to/conversations/send-proactive-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="51671-124">This is a form of [proactive messaging](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

<span data-ttu-id="51671-125">接下来，可以使用 对象检索提及 `entities` 内容，然后使用 对象向邮件添加 `Mention` 提及。</span><span class="sxs-lookup"><span data-stu-id="51671-125">Next, you can retrieve mentions using the `entities` object and add mentions to your messages using the `Mention` object.</span></span>

## <a name="work-with-mentions"></a><span data-ttu-id="51671-126">使用提及</span><span class="sxs-lookup"><span data-stu-id="51671-126">Work with mentions</span></span>

<span data-ttu-id="51671-127">从组或频道向自动程序发送的每条消息都包含一个@mention消息文本中具有其名称的聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="51671-127">Every message to your bot from a group or channel contains an @mention with its name in the message text.</span></span> <span data-ttu-id="51671-128">自动程序还可以检索邮件中提及的其他用户，并将提及添加到它发送的任何邮件中。</span><span class="sxs-lookup"><span data-stu-id="51671-128">Your bot can also retrieve other users mentioned in a message and add mentions to any messages it sends.</span></span>

<span data-ttu-id="51671-129">还必须从自动程序@mentions内容中去除此限制。</span><span class="sxs-lookup"><span data-stu-id="51671-129">You must also strip out the @mentions from the content of the message your bot receives.</span></span>

### <a name="retrieve-mentions"></a><span data-ttu-id="51671-130">检索提及</span><span class="sxs-lookup"><span data-stu-id="51671-130">Retrieve mentions</span></span>

<span data-ttu-id="51671-131">在有效负载中的 对象中返回提及，同时包含用户的唯一 ID 和 `entities` 提及用户的名称。</span><span class="sxs-lookup"><span data-stu-id="51671-131">Mentions are returned in the `entities` object in payload and contain both the unique ID of the user and the name of the user mentioned.</span></span> <span data-ttu-id="51671-132">邮件文本还包括提及，例如 `<at>@John Smith<at>` 。</span><span class="sxs-lookup"><span data-stu-id="51671-132">The text of the message also includes the mention, such as `<at>@John Smith<at>`.</span></span> <span data-ttu-id="51671-133">但是，不要依赖邮件中的文本来检索有关用户的任何信息。</span><span class="sxs-lookup"><span data-stu-id="51671-133">However, do not rely on the text in the message to retrieve any information about the user.</span></span> <span data-ttu-id="51671-134">发送邮件的人可以更改它。</span><span class="sxs-lookup"><span data-stu-id="51671-134">It is possible for the person sending the message to alter it.</span></span> <span data-ttu-id="51671-135">因此，请使用 `entities` 对象。</span><span class="sxs-lookup"><span data-stu-id="51671-135">Therefore, use the `entities` object.</span></span>

<span data-ttu-id="51671-136">可以通过调用 Bot Builder SDK 中的 函数来检索邮件中提及的所有内容，该 `GetMentions` 函数将返回对象 `Mention` 数组。</span><span class="sxs-lookup"><span data-stu-id="51671-136">You can retrieve all mentions in the message by calling the `GetMentions` function in the Bot Builder SDK, which returns an array of `Mention` objects.</span></span>

<span data-ttu-id="51671-137">以下代码显示检索提及的示例：</span><span class="sxs-lookup"><span data-stu-id="51671-137">The following code shows an example of retrieving mentions:</span></span>

# <a name="c"></a>[<span data-ttu-id="51671-138">C#</span><span class="sxs-lookup"><span data-stu-id="51671-138">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="51671-139">TypeScript</span><span class="sxs-lookup"><span data-stu-id="51671-139">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="51671-140">JSON</span><span class="sxs-lookup"><span data-stu-id="51671-140">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="51671-141">Python</span><span class="sxs-lookup"><span data-stu-id="51671-141">Python</span></span>](#tab/python)

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

### <a name="add-mentions-to-your-messages"></a><span data-ttu-id="51671-142">向邮件添加提及</span><span class="sxs-lookup"><span data-stu-id="51671-142">Add mentions to your messages</span></span>

<span data-ttu-id="51671-143">机器人可以在发布至频道的消息中提及其他用户。</span><span class="sxs-lookup"><span data-stu-id="51671-143">Your bot can mention other users in messages posted into channels.</span></span>

<span data-ttu-id="51671-144">`Mention`对象具有两个必须具有以下设置的属性：</span><span class="sxs-lookup"><span data-stu-id="51671-144">The `Mention` object has two properties that you must set using the following:</span></span>

* <span data-ttu-id="51671-145">在 <at>@username</at> 文本中包括邮件。</span><span class="sxs-lookup"><span data-stu-id="51671-145">Include <at>@username</at> in the message text.</span></span>
* <span data-ttu-id="51671-146">在 entities 集合中包括 mention 对象。</span><span class="sxs-lookup"><span data-stu-id="51671-146">Include the mention object inside the entities collection.</span></span>

<span data-ttu-id="51671-147">Bot Framework SDK 提供了用于创建提及项的帮助程序方法和对象。</span><span class="sxs-lookup"><span data-stu-id="51671-147">The Bot Framework SDK provides helper methods and objects to create mentions.</span></span>

<span data-ttu-id="51671-148">以下代码显示向邮件添加提及的示例：</span><span class="sxs-lookup"><span data-stu-id="51671-148">The following code shows an example of adding mentions to your messages:</span></span>

# <a name="c"></a>[<span data-ttu-id="51671-149">C#</span><span class="sxs-lookup"><span data-stu-id="51671-149">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="51671-150">TypeScript</span><span class="sxs-lookup"><span data-stu-id="51671-150">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="51671-151">JSON</span><span class="sxs-lookup"><span data-stu-id="51671-151">JSON</span></span>](#tab/json)

<span data-ttu-id="51671-152">`text`数组中对象中的 `entities` 字段必须与邮件字段的一部分 `text` 匹配。</span><span class="sxs-lookup"><span data-stu-id="51671-152">The `text` field in the object in the `entities` array must match a portion of the message `text` field.</span></span> <span data-ttu-id="51671-153">如果没有，则忽略提及。</span><span class="sxs-lookup"><span data-stu-id="51671-153">If it does not, the mention is ignored.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="51671-154">Python</span><span class="sxs-lookup"><span data-stu-id="51671-154">Python</span></span>](#tab/python)

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

<span data-ttu-id="51671-155">现在，可以在首次安装自动程序或将其添加到组或团队时发送简介消息。</span><span class="sxs-lookup"><span data-stu-id="51671-155">Now you can send an introduction message when your bot is first installed or added to a group or team.</span></span>

## <a name="send-a-message-on-installation"></a><span data-ttu-id="51671-156">安装时发送邮件</span><span class="sxs-lookup"><span data-stu-id="51671-156">Send a message on installation</span></span>

<span data-ttu-id="51671-157">首次将机器人添加到组或团队时，必须发送一条介绍消息。</span><span class="sxs-lookup"><span data-stu-id="51671-157">When your bot is first added to the group or team, an introduction message must be sent.</span></span> <span data-ttu-id="51671-158">该消息必须提供自动程序功能及其使用方法的简要说明。</span><span class="sxs-lookup"><span data-stu-id="51671-158">The message must provide a brief description of the bot's features and how to use them.</span></span> <span data-ttu-id="51671-159">必须使用 `conversationUpdate` `teamMemberAdded` eventType 订阅事件。</span><span class="sxs-lookup"><span data-stu-id="51671-159">You must subscribe to the `conversationUpdate` event with the `teamMemberAdded` eventType.</span></span>  <span data-ttu-id="51671-160">当添加任何新的团队成员时，将发送该事件。</span><span class="sxs-lookup"><span data-stu-id="51671-160">The event is sent when any new team member is added.</span></span> <span data-ttu-id="51671-161">检查添加的新增成员是否就是机器人。</span><span class="sxs-lookup"><span data-stu-id="51671-161">Check if the new member added is the bot.</span></span> <span data-ttu-id="51671-162">有关详细信息，请参阅 [向新团队成员发送欢迎消息](~/bots/how-to/conversations/send-proactive-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="51671-162">For more information, see [sending a welcome message to a new team member](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>

<span data-ttu-id="51671-163">添加自动程序时，向每个团队成员发送个人消息。</span><span class="sxs-lookup"><span data-stu-id="51671-163">Send a personal message to each team member when the bot is added.</span></span> <span data-ttu-id="51671-164">为此，请获取团队名单，并给每个用户发送一条直接消息。</span><span class="sxs-lookup"><span data-stu-id="51671-164">To do this, get the team roster and send each user a direct message.</span></span>

<span data-ttu-id="51671-165">在下列情况下不要发送邮件：</span><span class="sxs-lookup"><span data-stu-id="51671-165">Do not send a message in the following cases:</span></span>

* <span data-ttu-id="51671-166">例如，团队规模较大，成员超过 100 人。</span><span class="sxs-lookup"><span data-stu-id="51671-166">The team is large, for example, larger than 100 members.</span></span> <span data-ttu-id="51671-167">机器人可能会被视为垃圾邮件，添加它的人可能会收到投诉。</span><span class="sxs-lookup"><span data-stu-id="51671-167">Your bot can be seen as spam and the person who added it can get complaints.</span></span> <span data-ttu-id="51671-168">你必须向看到欢迎消息的每个人清楚地传达机器人的价值主张。</span><span class="sxs-lookup"><span data-stu-id="51671-168">You must clearly communicate your bot's value proposition to everyone who sees the welcome message.</span></span>
* <span data-ttu-id="51671-169">你的机器人首先在组或频道中提及，而不是先添加到团队。</span><span class="sxs-lookup"><span data-stu-id="51671-169">Your bot is first mentioned in a group or channel instead of being first added to a team.</span></span>
* <span data-ttu-id="51671-170">重命名组或频道。</span><span class="sxs-lookup"><span data-stu-id="51671-170">A group or channel is renamed.</span></span>
* <span data-ttu-id="51671-171">将团队成员添加到组或频道。</span><span class="sxs-lookup"><span data-stu-id="51671-171">A team member is added to a group or channel.</span></span>

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="see-also"></a><span data-ttu-id="51671-172">另请参阅</span><span class="sxs-lookup"><span data-stu-id="51671-172">See also</span></span>

[<span data-ttu-id="51671-173">获取Teams上下文</span><span class="sxs-lookup"><span data-stu-id="51671-173">Get Teams context</span></span>](~/bots/how-to/get-teams-context.md)

## <a name="next-step"></a><span data-ttu-id="51671-174">后续步骤</span><span class="sxs-lookup"><span data-stu-id="51671-174">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="51671-175">订阅对话事件</span><span class="sxs-lookup"><span data-stu-id="51671-175">Subscribe to conversation events</span></span>](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
