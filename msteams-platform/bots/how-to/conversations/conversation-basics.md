---
title: 对话基础知识
description: 介绍与 Microsoft Teams 自动程序对话的方法
ms.topic: overview
ms.author: anclear
keyword: conversations basics receive message send message picture message channel data adaptive cards
ms.openlocfilehash: a045f02a146782ebdbbbb14fe5f4187cb517a109
ms.sourcegitcommit: 55a4246e62d69d631a63bdd33de34f1b62cc0132
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093955"
---
# <a name="conversation-basics"></a>对话基础知识

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

对话是在机器人与一个或多个用户之间发送的一系列消息。 有三种类型的对话，在 Teams 中也称为范围：

| 对话类型 | Description |
| ------- | ----------- |
|  `teams` | 也称为频道对话，对频道的所有成员可见。 |
| `personal` | 机器人与单个用户之间的对话。 |
| `groupChat` | 机器人与两个或多个用户之间的聊天。 此外，还可以在会议聊天中启用机器人。 |

自动程序的行为略有不同，具体取决于它涉及的对话类型：

* 频道和群聊对话中的聊天机器人要求用户 @ 提及机器人，以在频道中调用它。
* 一对一对话中的机器人不需要 @ 提及。 用户发送的所有消息将路由到自动程序。

若要启用特定作用域中的自动程序，请将此范围添加到[应用清单。](~/resources/schema/manifest-schema.md)

## <a name="activities"></a>活动

每封邮件都是 `Activity` 一个类型对象 `messageType: message` 。 当用户发送消息时，Teams 会向自动程序发布消息;具体来说，它会将 JSON 对象发送到机器人的消息终结点。 机器人会检查消息以确定其类型并相应地做出响应。

基本对话通过 Bot Framework 连接器（一个 REST API）进行处理。 此 API 使机器人能够与 Teams 和其他频道进行通信。 Bot Builder SDK 提供对此 API 的轻松访问、用于管理对话流和状态的其他功能，以及合并认知服务（如自然语言处理 (NLP) ） 的简单方法。

## <a name="receive-a-message"></a>接收邮件

若要接收短信，请使用 `Text` 对象 `Activity` 的属性。 在机器人的活动处理程序中，使用 turn context 对象读取 `Activity` 单个消息请求。

以下代码是一个示例。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Echo: {turnContext.Activity.Text}"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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
    "text": "Hello Teams TestBot",
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

## <a name="send-a-message"></a>发送邮件

若要发送短信，请指定要作为活动发送的字符串。 在机器人的活动处理程序中，使用 turn context 对象的方法发送 `SendActivityAsync` 单个消息响应。 使用对象的方法 `SendActivitiesAsync` 一次发送多个响应。 以下代码显示将某人添加到对话时发送邮件的示例。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMembersAddedAsync(IList<ChannelAccount> membersAdded, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
  await turnContext.SendActivityAsync(MessageFactory.Text($"Hello and welcome!"), cancellationToken);
}

```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            await context.sendActivity('Hello and welcome!');
            await next();
        });
    }
}
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
    "text": "hi",
    "textFormat": "plain",
    "type": "message",
    "timestamp": "2019-10-31T20:57:27.2347285Z",
    "localTimestamp": "2019-10-31T13:57:27.2347285-07:00",
    "id": "1572555447214",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer/",
    "from": {
        "id": "29:1Xv-kvy4dKirR0rZfSF_kAVUzotoT1SXuEzkC9XGkuZng8YBw8qyu5uh4128fQRjlGgvEiRLx-0XP4KYMwcgdZw",
        "name": "Jane Doe",
        "aadObjectId": "df486eae-88fd-42a5-b45e-c581588186db"
    },
    "conversation": {
        "conversationType": "personal",
        "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
        "id": "a:1oAmWTVBBe9E0JrpGxauqNyx4CCE_iQf2ZuWon9D42722Fon3wYIpbhgbRChE3wgVS1Gwl9zS1pZy4FSu6-x1vGEq5KBQK-EbBgyPyeP_C-lbLBY3vxnGk9m9D_282jbg"
    },
    "recipient": {
        "id": "28:5baea8d1-d4ea-43a1-b101-882f4c8d9cb4",
        "name": "Imported Bot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Windows",
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

## <a name="teams-channel-data"></a>Teams 频道数据

该对象 `channelData` 包含特定于 Teams 的信息，是团队和频道的明确来源。 你可能需要缓存这些 ID，并使用它们作为本地存储的密钥。 SDK 中通常从对象中拉 `TeamsActivityHandler` 出重要信息 `channelData` ，使其易于访问。 但是，您始终可以从对象访问 `turnContext` 原始数据。

`channelData`该对象不包含在个人对话中的邮件中，因为这些事件发生在任何频道之外。

发送给自动程序的活动中的典型 channelData 对象包含以下信息：

* `eventType` Teams 事件类型;仅在通道修改 [事件的情况下传递](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
* `tenant.id` 在所有上下文中传递的 Azure Active Directory 租户 ID。
* `team` 仅在频道上下文中传递，而不是在个人聊天中传递。
  * `id` 通道的 GUID。
  * `name` 团队名称;仅在团队重命名 [事件的情况下传递](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
* `channel` 仅在提到自动程序时在频道上下文中传递，或针对团队中已添加自动程序的团队中的事件传递。
  * `id` 通道的 GUID。
  * `name` 频道名称;仅在通道修改 [事件的情况下传递](~/bots/how-to/conversations/subscribe-to-conversation-events.md)。
* `channelData.teamsTeamId` 已弃用。 包含此属性仅仅是为了向后兼容。
* `channelData.teamsChannelId` 已弃用。 包含此属性仅仅是为了向后兼容。

### <a name="example-channeldata-object-channelcreated-event"></a>channelCreated 事件 (的 channelData 对象) 

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

## <a name="message-content"></a>邮件内容

机器人可以发送格式文本、图片和卡片。 用户可以将格式文本和图片发送到机器人。

| Format    | 从用户到机器人 | 从自动程序到用户 | 注释                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| 格式文本  | ✔                | ✔                |                                                                                         |
| 图片  | ✔                | ✔                | PNG、JPEG 或 GIF 格式的最大大小为 1024×1024 和 1 MB;不支持动态 GIF  |
| 卡     | ✖                | ✔                | 有关受支持的 [卡，](~/task-modules-and-cards/cards/cards-reference.md) 请参阅 Teams 卡参考 |
| 表情符号    | ✖                | ✔                | Teams 当前支持通过 UTF-16 (表情符号，例如 U+1F600，用于面部)           |

## <a name="adding-notifications-to-your-message"></a>向邮件添加通知

通知会提醒用户有关他们正在处理或需要查看的新任务、提及和注释，只需在活动源中插入通知。 可以通过将 objects 属性设置为 true，将通知设置为从自动 `TeamsChannelData` 程序 `Notification.Alert` 消息触发。 是否引发通知最终取决于单个用户的 Teams 设置，你无法以编程方式覆盖这些设置。 通知类型为横幅或横幅和电子邮件。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  var message = MessageFactory.Text("You'll get a notification, if you've turned them on.");
  message.TeamsNotifyUser();

  await turnContext.SendActivityAsync(message);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

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

## <a name="picture-messages"></a>图片消息

图片通过向邮件添加附件来发送。 您可以在 Bot Framework 文档中找到有关 [附件的更多信息](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)。

图片最多为 1024×1024 和 1 MB（采用 PNG、JPEG 或 GIF 格式）。 不支持动态 GIF。

始终使用 XML 指定每个图像的高度和宽度。 在 Markdown 中，图像大小默认为 256×256。 例如：

* 使用 - `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* 请勿使用 - `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="adaptive-cards"></a>自适应卡片

使用以下代码发送简单的自适应卡片：

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
当响应包含短信和附件时，将单独发送这两个响应。 附件在短信之后发送。

## <a name="code-sample"></a>代码示例
|**示例名称** | **说明** | **.NETCore** | **JavaScript** | **Python**|
|----------------|-----------------|--------------|----------------|-----------|
| Teams 对话机器人 | 消息和对话事件处理。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-steps"></a>后续步骤

* [发送主动邮件](~/bots/how-to/conversations/send-proactive-messages.md)
* [订阅对话事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
