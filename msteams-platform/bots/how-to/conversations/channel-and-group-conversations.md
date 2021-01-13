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
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>与 Microsoft Teams 自动程序进行频道和群组聊天对话

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

通过将或范围添加到自动程序，可以安装在团队或群聊 `teams` `groupchat` 中。 这允许对话的所有成员与机器人交互。 安装后，它还可以访问对话的元数据（如对话成员列表）以及当安装在有关该团队的团队详细信息和频道的完整列表中时。

组或频道中的聊天机器人仅在 (@botname) 时接收消息，不会收到发送到对话的其他任何消息。

> [!NOTE]
> 必须直接@mentioned自动程序。 当提及团队或频道时，或者当有人回复来自自动程序的邮件时，系统不会收到@mentioning消息。

## <a name="design-guidelines"></a>设计准则

了解如何在 [频道和聊天中设计机器人对话](~/bots/design/bots.md)。

## <a name="creating-new-conversation-threads"></a>创建新的对话线程

在团队中安装自动程序时，有时可能需要创建新的对话线程，而不是回复现有的对话线程。 这是一种 [主动消息形式](~/bots/how-to/conversations/send-proactive-messages.md)。

## <a name="working-with-mentions"></a>使用提及

从组或频道发送到自动程序的每封邮件都将包含一个@mention在消息文本中具有自己的名称，因此你将需要确保邮件分析能够处理这一点。 机器人还可以检索邮件中提到的其他用户，并将提及内容添加到它发送的任何邮件中。

### <a name="stripping-mentions-from-message-text"></a>从邮件文本中去除提及

你可能会发现有必要从自动程序@mentions文本中去除此限制。

### <a name="retrieving-mentions"></a>检索提及

在有效负载的对象中返回提及内容，同时包含用户的唯一 ID，在大多数情况下，还包含 `entities` 提及的用户名称。 邮件的文本还将包含类似提及的内容 `<at>@John Smith<at>` 。 但是，不应依赖邮件中的文本来检索有关用户的任何信息;发送邮件的人可以更改它。 请改为使用 `entities` 对象。

可以通过调用返回对象数组的 Bot Builder SDK 中的函数来检索邮件中提及 `GetMentions` `Mention` 的所有内容。

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

### <a name="adding-mentions-to-your-messages"></a>向邮件添加提及

机器人可以在张贴到频道的消息中提及其他用户。 为此，您的邮件必须执行以下操作：

`Mention`该对象具有两个需要设置的属性：

* 将 <at>@username</at> 包括在邮件文本中
* 在实体集合中包括 mention 对象

Bot Framework SDK 提供了帮助程序方法和对象，以便更轻松地构建提及。

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

`text`数组中对象中的 `entities` 字段必须与邮件字段的一部分完全 `text` 匹配。 如果没有，则忽略提及。

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

首次将机器人添加到组或团队时，发送介绍它的消息可能很有用。 该消息应提供自动程序功能的简要说明及其使用方法。 你需要使用 `conversationUpdate` `teamMemberAdded` eventType 订阅事件。  由于在添加任何新团队成员时发送事件，因此需要检查以确定添加的团队成员是否为机器人。 有关 [更多详细信息，请参阅向新团队成员](~/bots/how-to/conversations/send-proactive-messages.md) 发送欢迎消息。

添加自动程序时，你可能还需要向团队的每个成员发送个人消息。 为此，你可以获取团队名单，并给每个用户发送直接消息。

不建议在下列情况下发送邮件：

* 团队规模较大 (明显具有主观性，但例如超过 100 个成员) 。 你的自动程序可能会被视为"spa一"，并且添加它的人可能会收到投诉，除非你向看到欢迎消息的每个人清楚地传达了机器人的价值主张。
* 你的自动程序首先在组或频道 (提及，而不是先添加到团队) 
* 重命名组或频道
* 将团队成员添加到组或频道

## <a name="learn-more"></a>了解详细信息

机器人可以访问有关其安装的群聊或团队的其他信息。 请参阅 [获取适用于机器人](~/bots/how-to/get-teams-context.md) 的其他 API 的团队上下文。

此外，机器人还可以订阅和响应其他事件。 请参阅 [订阅对话事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md) 以了解方式。

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
