---
title: 为频道或群集聊天创建聊天机器人
author: surbhigupta
description: 了解如何在安装时创建新的对话线程、处理提及和发送消息。 浏览 Teams 文件上传示例 (.NET、JavaScript、Python) 。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: 18af255a8d0975878865b101b8787422d5cfa3d5
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100600"
---
# <a name="channel-and-group-chat-conversations-with-a-bot"></a>使用机器人进行频道和群组对话

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

若要在团队或群组聊天中安装 Microsoft Teams 机器人，请为机器人添加 `teams` 或 `groupchat` 范围。 此操作允许对话的所有成员与你的机器人互动。 安装机器人后，它有权访问有关对话的元数据，例如对话成员列表。 此外，在团队中安装时，机器人有权访问有关该团队的详细信息和频道的完整列表。

组或频道中的机器人仅在@botname被提及时才会收到消息。 他们不会收到发送到对话的任何其他消息。 必须直接 @mentioned 机器人。 当提到团队或频道时，或者当有人回复来自机器人的消息而没有@mentioning消息时，机器人不会收到消息。

> [!NOTE]
> 此功能目前仅适用于[公共开发人员预览版](../../../resources/dev-preview/developer-preview-intro.md)。
>
> 使用资源特定的许可 (RSC) ，机器人可以接收团队中安装的所有频道消息，而无需@mentioned。 有关详细信息，请参阅[使用 RSC 接收所有频道消息](channel-messages-with-rsc.md)。
>
> 目前不支持将消息或自适应卡片发布到专用频道。

请参阅以下视频，了解与机器人的频道和群聊对话：
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4NzEs]
<br>

## <a name="design-guidelines"></a>设计准则

与个人聊天不同，在群组聊天和频道中，机器人必须提供快速简介。 必须遵循这些和更多机器人设计准则。 有关如何在 Teams 中设计机器人的详细信息，请参阅[如何在频道和聊天中设计机器人对话](~/bots/design/bots.md)。

现在，可以创建新的对话线程，并轻松管理频道中的不同对话。

## <a name="create-new-conversation-threads"></a>创建新的对话线程

在团队中安装机器人时，必须创建新的对话线程，而不是回复现有对话线程。 有时，很难区分两个对话。 如果会话是线程式的，则更容易在频道中组织和管理不同的对话。 这是[主动消息传送](~/bots/how-to/conversations/send-proactive-messages.md)的一种形式。

接下来，可以使用 `entities` 对象检索提及，并使用 `Mention` 对象向消息添加提及。

## <a name="work-with-mentions"></a>处理提及

从群组或频道发送给机器人的每一条消息都会在消息文本中包含 @提及和名称。 机器人还可以检索消息中提及的其他用户，并在它发送的任何消息中添加提及。

你还必须从机器人收到的消息内容中删除 @提及。

### <a name="retrieve-mentions"></a>检索提及

提及在有效负载的 `entities` 对象中返回，并包含用户的唯一 ID 和提及的用户名。 消息文本还将包括如 `<at>@John Smith<at>` 的提及。 但是，不要依赖消息中的文本来检索有关用户的任何信息。 发送消息的人员可以对其进行更改。 因此，请使用 `entities` 对象。

可以通过调用 Bot Builder SDK 中的 `GetMentions` 函数来检索消息中的所有提及，该函数将返回一组 `Mention` 对象。

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

### <a name="add-mentions-to-your-messages"></a>向消息添加提及

机器人可以在发布到频道的消息中提及其他用户。

`Mention` 对象具有必须使用以下方法设置的两个属性：

* 在消息文本中包含 *@username*。
* 在实体集合中包含提及对象。

Bot Framework SDK 提供帮助程序方法和对象来创建提及。

以下代码显示向消息添加提及的示例：

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

`entities` 数组对象中的 `text` 字段必须与消息 `text` 字段的一部分匹配。 如果没有，则忽略提及。

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

现在，可以在首次安装机器人或将其添加到群组或团队时发送简介消息。

## <a name="send-a-message-on-installation"></a>在安装时发送消息

首次将机器人添加到群组或团队时，必须发送简介消息。 该消息必须简要说明机器人的功能以及如何使用它们。 必须订阅具有 `teamMemberAdded` eventType 的 `conversationUpdate` 事件。  添加任何新团队成员时，将发送该事件。 检查添加的新成员是否为机器人。 有关详细信息，请参阅[向新团队成员发送欢迎消息](~/bots/how-to/conversations/send-proactive-messages.md)。

添加机器人时，可以向团队的每个成员发送个人消息。 为此， [请提取团队名册，](../../../resources/bot-v3/bots-context.md#fetch-the-team-roster) 并向每个用户发送 [一条直接消息](../../../resources/bot-v3/bot-conversations/bots-conv-proactive.md)。

>[!NOTE]
> 确保机器人发送的消息相关，并将值添加到初始消息，并且不会向用户发送垃圾邮件。

在以下情况下，请勿发送消息：

* 例如，当团队规模大于 100 个成员时。 机器人可能被视为垃圾邮件，添加机器人的人员可能会收到投诉。 你必须清楚地向所有看到欢迎消息的成员传达机器人的价值主张。
* 首先在群组或频道中提及机器人，而不是先将其添加到团队。
* 群组或频道已重命名。
* 团队成员将添加到群组或频道。

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]

## <a name="step-by-step-guide"></a>分步指南

按照[分步指南](../../../sbs-teams-conversation-bot.yml)操作，以创建 Teams 对话机器人。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [订阅对话事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)

## <a name="see-also"></a>另请参阅

* [获取 Teams 上下文](~/bots/how-to/get-teams-context.md)
* [代表用户创建专用频道](/graph/api/channel-post#example-2-create-private-channel-on-behalf-of-user)
* [将机器人连接到Web 聊天通道](/azure/bot-service/bot-service-channel-connect-webchat)
