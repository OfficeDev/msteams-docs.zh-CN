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
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>与 Microsoft 团队 bot 的频道和组聊天对话

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

通过将 `teams` 或 `groupchat` 作用域添加到你的 bot，可以在团队或组聊天中安装它。 这样，对话的所有成员都可以与你的 bot 进行交互。 一旦安装，它还可以访问有关会话的元数据，如会话成员的列表，以及在团队详细信息中安装的有关该团队和频道的完整列表。

组或频道中的 bot 仅在提到邮件时才接收邮件（"@botname"），它们不会收到发送到对话的任何其他邮件。

> [!NOTE]
> 必须直接 @mentioned 机器人。 在提到团队或频道时，或当某人从你的 bot 回复邮件时不 @mentioning 它，你的 bot 将不会收到邮件。

## <a name="design-considerations"></a>设计注意事项

Bot 应提供与组或通道中的所有成员都适用且相关的信息。 包含该组或频道的所有人都能看到与其相关的对话。 设计良好的 bot 可以为所有用户增加价值，同时不会在不小心的情况下共享更适合一对一对话的信息。 应避免使用对话之类的多个对话-请改用卡片和/或任务模块来收集信息。

## <a name="creating-new-conversation-threads"></a>创建新的对话线索

当你的 bot 安装在团队中时，有时可能需要创建新的会话线程，而不是答复现有的会话线程。 这是一种[主动消息传递](~/bots/how-to/conversations/send-proactive-messages.md)形式。

## <a name="working-with-mentions"></a>处理提及

来自组或频道的每封邮件都将在邮件文本中包含其自己的名称的 @mention，因此您需要确保您的邮件分析处理该邮件。 你的 bot 还可以检索邮件中提及的其他用户，并将提及添加到它发送的任何邮件中。

### <a name="stripping-mentions-from-message-text"></a>从邮件文本中去除提及

你可能会发现需要从你的 bot 接收的邮件的文本中去除 @mentions。

### <a name="retrieving-mentions"></a>检索提及

提到在 `entities` 有效负载的对象中返回，并且包含用户的唯一 ID，在大多数情况下，提到的用户的名称。 邮件文本中还包括提及的 like `<at>@John Smith<at>` 。 但是，不应依赖邮件中的文本来检索有关用户的任何信息;发送邮件的人可以对其进行更改。 而是使用 `entities` 对象。

您可以通过调用自动程序生成器 SDK 中的函数来检索邮件中的所有提及， `GetMentions` 这将返回 `Mention` 对象的数组。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

# <a name="json"></a>[JSON](#tab/json)

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

# <a name="python"></a>[Python](#tab/python)

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

### <a name="adding-mentions-to-your-messages"></a>将提及添加到邮件

你的 bot 可以在发送到频道的邮件中提及其他用户。 若要执行此操作，您的邮件必须执行以下操作：

`Mention`对象具有两个需要设置的属性：

* 在邮件文本中包含<at>@username</at>
* 在实体集合中包含提及的对象

Bot 框架 SDK 提供帮助程序方法和对象，以使所提及的更简单的构造更简单。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

# <a name="json"></a>[JSON](#tab/json)

`text`数组中的对象中的字段 `entities` 必须与消息字段的一部分*完全*匹配 `text` 。 如果不是，则将忽略提及。

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

# <a name="python"></a>[Python](#tab/python)

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

## <a name="sending-a-message-on-installation"></a>在安装时发送邮件

当你的 bot 第一次添加到组或团队时，发送引入邮件的消息可能很有用。 邮件应提供机器人功能的简短说明以及如何使用它们。 你将需要 `conversationUpdate` 使用事件，来订阅事件 `teamMemberAdded` 。  由于添加任何新的团队成员时都会发送事件，因此您需要进行检查以确定添加的新成员是否为 bot。 有关更多详细信息，请参阅[向新的团队成员发送欢迎消息](~/bots/how-to/conversations/send-proactive-messages.md)。

添加 bot 时，您可能还希望向团队的每个成员发送个人消息。 为此，您可以获取团队名单并向每个用户发送一条直接消息。

在下列情况下，不建议发送邮件：

* 团队规模较大（显然是主观，但例如，大于100个成员）。 你的 bot 可能被视为 "垃圾"，添加它的人可能会收到投诉，除非你清楚地将你的 bot 的价值主张传达给可看到欢迎消息的每个人。
* 你的 bot 首先在组或频道中提及（而不是首次添加到团队）
* 重命名组或通道
* 将团队成员添加到组或通道

## <a name="learn-more"></a>了解详细信息

你的 bot 可以访问有关安装了的组聊天或团队的其他信息。 有关为你的 bot 提供的其他 Api，请参阅[获取团队上下文](~/bots/how-to/get-teams-context.md)。

此外，你的 bot 也可以订阅和响应的其他事件。 若要了解如何操作，请参阅[订阅对话事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
