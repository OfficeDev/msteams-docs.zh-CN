---
title: 与机器人的频道和群组对话
author: surbhigupta
description: 如何发送、接收和处理频道或群聊中机器人的消息。 了解设计指南、使用代码示例创建@mentions线程
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 6c3d476ec51c75431d4a39e35b7307771b919d26
ms.sourcegitcommit: 5e5d2d3fb621bcbd9d792a5b450f95167ec8548b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/22/2022
ms.locfileid: "63727497"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a>使用机器人进行频道和群组对话

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

若要在团队Microsoft Teams聊天中安装聊天机器人，请向`teams`自动程序添加 或 `groupchat` 作用域。 此操作允许对话的所有成员与你的机器人互动。 安装自动程序后，它有权访问有关对话的元数据，如对话成员列表。 此外，当在团队中安装它时，机器人可以访问有关该团队的详细信息和频道的完整列表。

组或频道中的机器人仅在被提及时接收@botname。 他们不会收到发送到对话的其他任何消息。 必须直接 @mentioned 机器人。 当提到团队或频道时，或者当有人未经回复而回复来自你的机器人的消息时，机器人不会收到@mentioning消息。

> [!NOTE]
> 此功能目前仅适用于公共 [开发人员预览](../../../resources/dev-preview/developer-preview-intro.md) 版。
>
> 通过使用 RSC (资源) ，机器人可以接收团队中安装它的所有频道消息，而无需@mentioned。 有关详细信息，请参阅使用 [RSC 接收所有频道消息](channel-messages-with-rsc.md)。
>
> 目前不支持将消息或自适应卡片发布到私人频道。

## <a name="design-guidelines"></a>设计准则

与个人聊天不同，在群聊和频道中，机器人必须提供快速简介。 必须遵循这些以及更多自动程序设计指南。 若要详细了解如何在聊天中设计聊天机器人Teams，请参阅如何在频道和聊天中设计机器人[对话](~/bots/design/bots.md)。

现在，你可以创建新的对话线程并轻松管理频道中的不同对话。

## <a name="create-new-conversation-threads"></a>创建新的对话线程

在团队中安装自动程序时，必须创建新的对话线程，而不是回复现有对话线程。 有时很难区分两个对话。 如果会话是按线索组织的，则更易于组织和管理频道中的不同对话。 这是一种 [主动消息形式](~/bots/how-to/conversations/send-proactive-messages.md)。

接下来，可以使用 对象检索 `entities` 提及内容，然后使用 对象向邮件添加 `Mention` 提及。

## <a name="work-with-mentions"></a>使用提及

从组或频道向自动程序发送的每条消息都包含一个@mention消息文本中包含其名称的自动程序。 自动程序还可以检索邮件中提及的其他用户，并将提及添加到它发送的任何邮件中。

还必须从自动程序@mentions内容中去除此限制。

### <a name="retrieve-mentions"></a>检索提及

在有效负载中的 `entities` 对象中返回提及，同时包含用户的唯一 ID 和提及用户的名称。 邮件文本还包括提及，例如 `<at>@John Smith<at>`。 但是，不要依赖邮件中的文本来检索有关用户的任何信息。 发送邮件的人可以更改它。 因此，请使用 `entities` 对象。

可以通过调用 Bot Builder `GetMentions` SDK 中的 函数来检索邮件中提及的所有内容，该函数将返回对象 `Mention` 数组。

以下代码显示检索提及的示例：

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

### <a name="add-mentions-to-your-messages"></a>向邮件添加提及

机器人可以在发布至频道的消息中提及其他用户。

对象 `Mention` 具有两个必须具有以下设置的属性：

* 在 *@username* 文本中包括文本。
* 在 entities 集合中包括 mention 对象。

Bot Framework SDK 提供了用于创建提及项的帮助程序方法和对象。

以下代码显示向邮件添加提及的示例：

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

数组 `text` 中对象中的字段 `entities` 必须与邮件字段的一部分 `text` 匹配。 如果没有，则忽略提及。

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

现在，可以在首次安装自动程序或将其添加到组或团队时发送简介消息。

## <a name="send-a-message-on-installation"></a>安装时发送邮件

首次将机器人添加到组或团队时，必须发送一条介绍消息。 该消息必须提供自动程序功能及其使用方法的简要说明。 `conversationUpdate`必须使用 eventType 订阅`teamMemberAdded`事件。  当添加任何新的团队成员时，将发送该事件。 检查添加的新增成员是否就是机器人。 有关详细信息，请参阅 [向新团队成员发送欢迎消息](~/bots/how-to/conversations/send-proactive-messages.md)。

添加自动程序时，向每个团队成员发送个人消息。 为此，请获取团队名单，并给每个用户发送一条直接消息。

在下列情况下不要发送邮件：

* 例如，团队规模较大，成员超过 100 人。 机器人可能会被视为垃圾邮件，添加它的人可能会收到投诉。 你必须向看到欢迎消息的每个人清楚地传达机器人的价值主张。
* 你的机器人首先在组或频道中提及，而不是先添加到团队。
* 重命名组或频道。
* 将团队成员添加到组或频道。

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [订阅对话事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="see-also"></a>另请参阅

[获取Teams上下文](~/bots/how-to/get-teams-context.md)
