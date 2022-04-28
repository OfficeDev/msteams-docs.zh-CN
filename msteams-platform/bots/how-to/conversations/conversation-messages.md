---
title: 智能机器人对话中的邮件
description: 介绍如何与Microsoft Teams机器人进行对话。 了解Teams通道数据、消息通知、图片消息、使用代码示例的自适应卡片。
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
keyword: receive message send message picture message channel data adaptive cards
ms.openlocfilehash: d31f528b17c671074f3009c435cfff7bad728a09
ms.sourcegitcommit: e40383d9081bf117030f7e6270140e6b94214e8b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65102110"
---
# <a name="messages-in-bot-conversations"></a>智能机器人对话中的邮件

对话中的每个消息都是类型的`Activity``messageType: message`对象。 当用户发送消息时，Teams将消息发布到机器人。 Teams将 JSON 对象发送到机器人的消息传送终结点。 机器人检查消息以确定其类型并做出相应响应。

基本对话通过 Bot Framework 连接器（单个 REST API）进行处理。 此 API 使机器人能够与Teams和其他通道通信。 Bot Builder SDK 提供以下功能：

* 轻松访问 Bot Framework 连接器。
* 用于管理会话流和状态的其他功能。
* 合并认知服务的简单方法，例如自然语言处理 (NLP) 。

机器人使用`Text`该属性从Teams接收消息，并向用户发送单个或多个消息响应。

## <a name="receive-a-message"></a>接收消息

若要接收短信，请使用 `Activity` 对象的 `Text` 属性。 在机器人的活动处理程序中，使用圈上下文对象的 `Activity` 来读取单一消息请求。

以下代码演示接收消息的示例：

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

若要发送短信，请指定你想要作为活动发送的字符串。 在机器人的活动处理程序中，使用 turn 上下文对象 `SendActivityAsync` 的方法发送单个消息响应。 使用对象 `SendActivitiesAsync` 的方法一次发送多个响应。

以下代码演示在将用户添加到对话时发送消息的示例：

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
> 在同一活动有效负载中发送短信和附件时，将发生消息拆分。 通过Microsoft Teams将此活动拆分为单独的活动，其中一个活动仅包含一条短信，另一个活动包含附件。 由于活动是拆分的，因此不会收到响应中的消息 ID，该 ID 用于主动 [更新或删除](~/bots/how-to/update-and-delete-bot-messages.md) 消息。 建议发送单独的活动，而不是根据消息拆分。

用户和机器人之间发送的消息包括消息中的内部通道数据。 此数据允许机器人在该通道上正确通信。 Bot Builder SDK 允许修改消息结构。

## <a name="teams-channel-data"></a>Teams通道数据

该`channelData`对象包含Teams特定的信息，是团队和频道 ID 的明确源。 （可选）可以缓存这些 ID 并使用这些 ID 作为本地存储的密钥。 `TeamsActivityHandler` SDK 中的用户从`channelData`对象中提取重要信息，使其易于访问。 但是，始终可以从 `turnContext` 对象访问原始数据。

该 `channelData` 对象不包括在个人对话中的消息中，因为这些内容发生在频道外部。

发送到机器人的活动中的典型 `channelData` 对象包含以下信息：

* `eventType`：Teams事件类型，仅在[通道修改事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)的情况下传递。
* `tenant.id`：在所有上下文中传递Microsoft Azure Active Directory (Azure AD) 租户 ID。
* `team`：仅在频道上下文中传递，而不是在个人聊天中传递。
  * `id`：通道的 GUID。
  * `name`：仅在 [团队重命名事件中](~/bots/how-to/conversations/subscribe-to-conversation-events.md)传递的团队名称。
* `channel`：仅在频道上下文中传递、提及机器人时，或在添加了机器人的团队中的频道中传递事件。
  * `id`：通道的 GUID。
  * `name`：通道名称仅在 [通道修改事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)的情况下传递。
* `channelData.teamsTeamId`：已弃用。 此属性仅包含用于向后兼容性。
* `channelData.teamsChannelId`：已弃用。 此属性仅包含用于向后兼容性。

### <a name="example-channeldata-object-channelcreated-event"></a>channelData 对象 (channelCreated 事件) 示例

以下代码演示 channelData 对象的示例：

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

从机器人接收或发送到机器人的消息可以包含不同类型的消息内容。

| 格式    | 从用户到机器人 | 从机器人到用户 | 笔记                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| 格式文本  | ✔                | ✔                | 机器人可以发送丰富的文本、图片和卡片。 用户可以向机器人发送丰富的文本和图片。                                                                                        |
| 图片  | ✔                | ✔                | PNG、JPEG 或 GIF 格式的最大 1024×1024 和 1 MB。 不支持动态 GIF。  |
| 卡片     | ✖                | ✔                | 请参阅[支持的卡Teams卡参考](~/task-modules-and-cards/cards/cards-reference.md)。 |
| 表情符号    | ✔                | ✔                | Teams目前通过 UTF-16 支持表情符号，例如 U+1F600，用于笑脸。 |

## <a name="notifications-to-your-message"></a>消息通知

还可以使用该 `Notification.Alert` 属性向邮件添加通知。 通知会提醒用户有关新任务、提及和注释的信息。 这些警报与用户正在处理的内容或必须通过在活动源中插入通知来查看的内容相关。 若要从机器人消息触发通知，请将 `TeamsChannelData` 对象 `Notification.Alert` 属性设置为 *true*。 是否引发通知取决于单个用户的Teams设置，不能重写这些设置。 通知类型是横幅，或者是横幅和电子邮件。

> [!NOTE]
> “ **摘要** ”字段将用户的任何文本显示为源中的通知消息。

以下代码演示向消息添加通知的示例：

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

若要增强邮件，可以将图片作为该邮件的附件包含在一起。

## <a name="picture-messages"></a>图片消息

图片是通过将附件添加到邮件来发送的。 有关附件的详细信息，请参阅 [Bot Framework 文档](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)。

图片最多可以是 1024×1024 和 1 MB PNG、JPEG 或 GIF 格式。 不支持动态 GIF。

使用 XML 指定每个图像的高度和宽度。 在 markdown 中，映像大小默认为 256×256。 例如：

* 使用： `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`.
* 请勿使用： `![Duck on a rock](http://aka.ms/Fo983c)`.

会话机器人可以包含可简化业务工作流的自适应卡片。 自适应卡片提供丰富的可自定义文本、语音、图像、按钮和输入字段。

## <a name="adaptive-cards"></a>自适应卡

自适应卡片可以在机器人中创作，并显示在多个应用中，例如Teams、网站等。 有关详细信息，请参阅 [自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)。

以下代码演示了发送简单自适应卡片的示例：

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

### <a name="form-completion-feedback"></a>表单完成反馈

向机器人发送响应时，窗体完成消息将显示在自适应卡片中。 消息可以是两种类型，错误或成功：

* **错误**：当发送到机器人的响应不成功时， **出现错误，将显示“重试** ”消息。

     :::image type="content" source="../../../assets/images/Cards/error-message.png" alt-text="错误消息"border="true":::

* **成功**：当发送到机器人的响应成功时， **将显示发送到应用消息的响应** 。

:::image type="content" source="../../../assets/images/Cards/success.PNG" alt-text="成功消息"border="true":::

可以选择 **关闭** 或切换聊天以关闭消息。

**移动设备上的响应**：

错误消息显示在自适应卡片的底部。

有关机器人中的卡片和卡片的详细信息，请参阅 [卡片文档](~/task-modules-and-cards/what-are-cards.md)。

## <a name="status-code-responses"></a>状态代码响应

下面是状态代码及其错误代码和消息值：

| 状态代码 | 错误代码和消息值 | 说明 |
|----------------|-----------------|-----------------|
| 403 | **代码**： `ConversationBlockedByUser` <br/> **消息**：用户阻止了与机器人的对话。 | 用户通过审查设置在 1：1 聊天或频道中阻止了机器人。 |
| 403 | **代码**： `BotNotInConversationRoster` <br/> **消息**：机器人不是聊天名单的一部分。 | 机器人不是对话的一部分。 |
| 403 | **代码**： `BotDisabledByAdmin` <br/> **消息**：租户管理员禁用了此机器人。 | 租户阻止了机器人。 |
| 401 | **代码**： `BotNotRegistered` <br/> **消息**：未为此机器人找到注册。 | 找不到此机器人的注册。 |
| 412 | **代码**： `PreconditionFailed` <br/> **消息**：先决条件失败，请重试。 | 由于同一会话上的多个并发操作，我们的某个依赖项的先决条件失败。 |
| 404 | **代码**： `ConversationNotFound` <br/> **消息**：找不到对话。 | 未找到对话。 |
| 413 | **代码**： `MessageSizeTooBig` <br/> **消息**：消息大小太大。 | 传入请求的大小太大。 |
| 429 | **代码**： `Throttled` <br/> **消息**：请求过多。 另请返回重试时间。 | 机器人发送的请求过多。 有关详细信息，请参阅 [速率限制](~/bots/how-to/rate-limit.md)。 |

## <a name="code-sample"></a>代码示例

|示例名称 | Description | .NETCore | Node.js | Python |
|----------------|-----------------|--------------|----------------|-----------|
| Teams 对话自动程序 | 消息传送和会话事件处理。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot)| [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [机器人命令菜单](~/bots/how-to/create-a-bot-commands-menu.md)

## <a name="see-also"></a>另请参阅

* [发送主动邮件](~/bots/how-to/conversations/send-proactive-messages.md)
* [订阅对话事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [通过机器人发送和接收文件](~/bots/how-to/bots-filesv4.md)
* [将租户 ID 和会话 ID 发送到机器人的请求标头](~/bots/how-to/conversations/request-headers-of-the-bot.md)
