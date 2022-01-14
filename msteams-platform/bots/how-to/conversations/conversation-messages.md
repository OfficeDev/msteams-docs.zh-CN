---
title: 智能机器人对话中的邮件
description: 介绍与自动程序进行Microsoft Teams的方法。 了解Teams数据、消息通知、图片消息、使用代码示例的自适应卡片。
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
keyword: receive message send message picture message channel data adaptive cards
ms.openlocfilehash: b78ca5b46442f30db3adfe314d627d3fc95682be
ms.sourcegitcommit: 25a33b31cc56c05169fc52c65d44c65c601aefef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/14/2022
ms.locfileid: "62043229"
---
# <a name="messages-in-bot-conversations"></a>智能机器人对话中的邮件

对话中每条消息都是一 `Activity` 个类型 为 的对象 `messageType: message` 。 当用户发送消息时，Teams将邮件发送到自动程序。 Teams JSON 对象发送到机器人的消息终结点。 自动程序将检查消息以确定其类型并相应地做出响应。

基本对话通过 Bot Framework 连接器（一个 REST API）进行处理。 此 API 使机器人能够与Teams通信。 Bot Builder SDK 提供以下功能：

* 轻松访问 Bot Framework 连接器。
* 用于管理对话流和状态的其他功能。
* 合并认知服务的简单方法，如自然语言处理 (NLP) 。

自动程序使用 Teams接收来自用户的邮件，并且它会向用户发送 `Text` 一个或多个邮件响应。

## <a name="receive-a-message"></a>接收消息

若要接收短信，请使用 `Activity` 对象的 `Text` 属性。 在机器人的活动处理程序中，使用圈上下文对象的 `Activity` 来读取单一消息请求。

以下代码显示了一个接收邮件的示例：

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity(`Echo: '${context.activity.text}'`);
            await next();
        });
    }
}

```

# <a name="python"></a>[Python](#tab/python)

<!-- Verify -->
```python

async def on_message_activity(self, turn_context: TurnContext):
    return await turn_context.send_activity(MessageFactory.text(f"Echo: {turn_context.activity.text}"))

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "message",
    "id": "1485983408511",
    "timestamp": "2017-02-01T21:10:07.437Z",
    "localTimestamp": "2017-02-01T14:10:07.437-07:00",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "channelId": "msteams",
    "from": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB39ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen",
        "aadObjectId": "7faf8ab2-3d56-4244-b585-20c8a42ed2b8"
    },
    "conversation": {
        "conversationType": "personal",
        "id": "a:17I0kl9EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-"
    },
    "recipient": {
        "id": "28:c9e8c047-2a74-40a2-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "textFormat": "plain",
    "text": "Hello Teams TestBot.Sending bold-italic rich text",
    "attachments": [
      {
            "contentType": "text/html",
            "content": "<div><div>Hello Teams TestBot. Sending <strong>bold</strong>-<em>italic</em> rich text.</div>\n</div>"
      } 
    ],
    "entities": [
      { 
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo"
      }
    ],
    "channelData": {
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "locale": "en-US"
}
```

---

## <a name="send-a-message"></a>发送消息

若要发送短信，请指定你想要作为活动发送的字符串。 在机器人的活动处理程序中，使用 turn context 对象的方法发送 `SendActivityAsync` 单个消息响应。 使用 对象的 `SendActivitiesAsync` 方法一次发送多个响应。

以下代码显示向对话中添加用户时发送邮件的示例：

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript

    this.onMembersAddedActivity(async (context, next) => {
        await Promise.all((context.activity.membersAdded || []).map(async (member) => {
            if (member.id !== context.activity.recipient.id) {
                await context.sendActivity(
                    `Welcome to the team ${member.givenName} ${member.surname}`
                );
            }
        }));

        await next();
    });
```

# <a name="python"></a>[Python](#tab/python)

<!-- Verify -->

```python

async def on_members_added_activity(
    self, members_added: [ChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(f"Welcome your new team member {member.id}")
    return

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "message",
    "from": {
        "id": "28:c9e8c047-2a34-40a1-b28a-b162d5f5327c",
        "name": "Teams TestBot"
    },
    "conversation": {
        "id": "a:17I0kl8EkpE1O9PH5TWrzrLNwnWWcfrU7QZjKR0WSfOpzbfcAg2IaydGElSo10tVr4C7Fc6GtieTJX663WuJCc1uA83n4CSrHSgGBj5XNYLcVlJAs2ZX8DbYBPck201w-",
        "name": "Convo1"
   },
   "recipient": {
        "id": "29:1XJKJMvc5GBtc2JwZq0oj8tHZmzrQgFmB25ATiQWA85gQtHieVkKilBZ9XHoq9j7Zaqt7CZ-NJWi7me2kHTL3Bw",
        "name": "Megan Bowen"
    },
    "text": "My bot's reply",
    "replyToId": "1632474074231"
}

```

---

> [!NOTE]
> 在同一活动有效负载中发送短信和附件时，将发生邮件拆分。 此活动按以下方式Microsoft Teams活动，一个仅包含一条短信，另一个包含附件。 拆分活动时，您不会收到响应消息 ID，该 ID 用于主动更新或删除[](~/bots/how-to/update-and-delete-bot-messages.md)邮件。 建议发送单独的活动，而不是根据邮件拆分。

在用户和机器人之间发送的消息包含邮件中的内部通道数据。 此数据允许机器人在此频道上正常通信。 Bot Builder SDK 允许你修改消息结构。

## <a name="teams-channel-data"></a>Teams频道数据

对象 `channelData` 包含Teams特定的信息，是团队和频道的一个明确来源。 （可选）你可以缓存这些 ID 并用作本地存储的密钥。 `TeamsActivityHandler`SDK 中的 从 对象提取重要信息 `channelData` ，使其易于访问。 但是，您始终可以从对象访问 `turnContext` 原始数据。

`channelData`对象不包含在个人对话中的邮件中，因为邮件在频道外发生。

发送给 `channelData` 自动程序的活动中的典型对象包含以下信息：

* `eventType`：Teams修改事件时传递的事件[类型](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
* `tenant.id`：Azure Active Directory上下文中传递的租户 ID。
* `team`：仅在频道上下文中传递，而不是在个人聊天中传递。
  * `id`：通道的 GUID。
  * `name`：仅在团队重命名事件的情况下传递 [的团队名称](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
* `channel`：仅在频道上下文中传递，当提到自动程序时或在团队中为频道中的事件传递，其中添加了自动程序。
  * `id`：通道的 GUID。
  * `name`：仅在通道修改事件的情况下传递 [的频道名称](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
* `channelData.teamsTeamId`：已弃用。 此属性仅包含用于向后兼容。
* `channelData.teamsChannelId`：已弃用。 此属性仅包含用于向后兼容。

### <a name="example-channeldata-object-or-channelcreated-event"></a>channelData 对象或 channelCreated 事件示例

以下代码显示了 channelData 对象的示例：

```json
"channelData": {
    "eventType": "channelCreated",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    },
    "channel": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype",
        "name": "My New Channel"
    },
    "team": {
        "id": "19:693ecdb923ac4458a5c23661b505fc84@thread.skype"
    }
}
```

从自动程序接收或发送到自动程序的邮件可以包括不同类型的邮件内容。

## <a name="message-content"></a>邮件内容

| 格式    | 从用户到机器人 | 从自动程序到用户 | 注释                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| 格式文本  | ✔                | ✔                | 机器人可以发送格式文本、图片和卡片。 用户可以向自动程序发送格式文本和图片。                                                                                        |
| 图片  | ✔                | ✔                | PNG、JPEG 或 GIF 格式的最大大小为 1024×1024 和 1 MB。 不支持动态 GIF。  |
| 卡片     | ✖                | ✔                | 有关支持的[Teams，](~/task-modules-and-cards/cards/cards-reference.md)请参阅卡片参考。 |
| 表情符号    | ✖                | ✔                | Teams UTF-16 支持表情符号，例如 U+1F600 用于表情符号。 |

您还可以使用 属性向邮件添加 `Notification.Alert` 通知。

## <a name="notifications-to-your-message"></a>邮件通知

通知会提醒用户有关新任务、提及和评论。 这些警报与用户正在处理或必须通过向活动源中插入通知来查看内容相关。 对于从自动程序消息触发的通知，将 `TeamsChannelData` objects `Notification.Alert` 属性设置为 *true*。 是否引发通知取决于单个用户Teams设置，你无法替代这些设置。 通知类型可以是横幅，也可以同时为横幅和电子邮件。

> [!NOTE]
> " **摘要"** 字段将来自用户的任何文本显示为源中的通知消息。

以下代码显示向邮件添加通知的示例：

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

```typescript
this.onMessage(async (turnContext, next) => {
    let message = MessageFactory.text("You'll get a notification, if you've turned them on.");
    teamsNotifyUser(message);

    await turnContext.sendActivity(message);

    // By calling next() you ensure that the next BotHandler is run.
    await next();
});
```

# <a name="python"></a>[Python](#tab/python)

```python

async def on_message_activity(self, turn_context: TurnContext):
    message = MessageFactory.text("You'll get a notification, if you've turned them on.")
    teams_notify_user(message)

    await turn_context.send_activity(message)

```

# <a name="json"></a>[JSON](#tab/json)

```json
{
  "type": "message",
  "timestamp": "2017-04-24T21:46:00.9663655Z",
  "localTimestamp": "2017-04-24T14:46:00.9663655-07:00",
  "serviceUrl": "https://callback.com",
  "channelId": "msteams",
  "from": {
    "id": "28:e4fda94a-4b80-40eb-9bf0-6314491bc793",
    "name": "The bot"
  },
  "conversation": {
    "id": "a:1pL6i0oY3C0K8oAj8"
  },
  "recipient": {
    "id": "29:1rsVJmSSFMScF0YFyCXpvNWlo",
    "name": "User"
  },
  "text": "John Phillips assigned you a weekly todo",
  "summary": "Don't forget to meet with Marketing next week",
  "channelData": {
    "notification": {
      "alert": true
    }
  },
  "replyToId": "1493070356924"
}
```

---

若要增强邮件功能，可以将图片作为邮件附件进行添加。

## <a name="picture-messages"></a>图片消息

图片通过向邮件添加附件来发送。 有关附件详细信息，请参阅 [Bot Framework 文档](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)。

图片可以是最多 1024×1024 和 1 MB PNG、 JPEG 或 GIF 格式。 不支持动态 GIF。

使用 XML 指定每个图像的高度和宽度。 在 markdown 中，图像大小默认为 256×256。 例如：

* 使用 `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>` ：。
* 请勿使用 `![Duck on a rock](http://aka.ms/Fo983c)` ：。

对话机器人可以包含可简化业务工作流的自适应卡片。 自适应卡片提供丰富的可自定义文本、语音、图像、按钮和输入字段。

## <a name="adaptive-cards"></a>自适应卡

自适应卡片可以在机器人中创作，并可在多个应用（如Teams、网站等）中显示。 有关详细信息，请参阅自适应 [卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)。

以下代码显示发送简单自适应卡片的示例：

```json
{
    "type": "AdaptiveCard",
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.5",
    "body": [
    {
        "items": [
        {
            "size": "large",
            "text": " Simple Adaptivecard Example with a Textbox",
            "type": "TextBlock",
            "weight": "bolder",
            "wrap": true
        },
        ],
        "spacing": "extraLarge",
        "type": "Container",
        "verticalContentAlignment": "center"
    }
    ]
}
```

若要了解有关机器人中的卡和卡的更多信息，请参阅 [卡片文档](~/task-modules-and-cards/what-are-cards.md)。

## <a name="status-code-responses"></a>状态代码响应

以下是状态代码及其错误代码和消息值：

| 状态代码 | 错误代码和消息值 | 说明 |
|----------------|-----------------|-----------------|
| 403 | **代码**： `ConversationBlockedByUser` <br/> **消息**：用户阻止了与机器人的对话。 | 用户通过审核设置在一对一聊天或频道中阻止机器人。 |
| 403 | **代码**： `BotNotInConversationRoster` <br/> **消息**：机器人不是对话名单中的一部分。 | 机器人不是对话的一部分。 |
| 403 | **代码**： `BotDisabledByAdmin` <br/> **消息**：租户管理员已禁用此自动程序。 | 租户阻止了机器人。 |
| 401 | **代码**： `BotNotRegistered` <br/> **消息**：未找到此自动程序注册。 | 未找到此自动程序注册。 |
| 412 | **代码**： `PreconditionFailed` <br/> **消息**：先决条件失败，请重试。 | 由于同一对话上的多个并发操作，某一依赖项的前提条件失败。 |
| 404 | **代码**： `ConversationNotFound` <br/> **消息**：未找到对话。 | 未找到对话。 |
| 413 | **代码**： `MessageSizeTooBig` <br/> **邮件**：邮件大小过大。 | 传入请求的大小太大。 |
| 429 | **代码**： `Throttled` <br/> **消息**：请求过多。 还返回在之后重试时间。 | 机器人发送的请求过多。 有关详细信息，请参阅速率 [限制](~/bots/how-to/rate-limit.md)。 |

## <a name="code-sample"></a>代码示例

|示例名称 | 说明 | .NETCore | Node.js | Python |
|----------------|-----------------|--------------|----------------|-----------|
| Teams 对话自动程序 | 消息和对话事件处理。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [自动程序命令菜单](~/bots/how-to/create-a-bot-commands-menu.md)

## <a name="see-also"></a>另请参阅

* [发送主动邮件](~/bots/how-to/conversations/send-proactive-messages.md)
* [订阅对话事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [通过自动程序发送和接收文件](~/bots/how-to/bots-filesv4.md)
* [将租户 ID 和对话 ID 发送到机器人的请求标头](~/bots/how-to/conversations/request-headers-of-the-bot.md)
