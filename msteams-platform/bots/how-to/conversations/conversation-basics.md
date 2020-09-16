---
title: 对话基础知识
author: clearab
description: 如何与 Microsoft 团队 bot 进行对话
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: bc016a8f0dcce474f80898dc93e309692ba20471
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819051"
---
# <a name="conversation-basics"></a>对话基础知识

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

对话是在你的 bot 和一个或多个用户之间发送的一系列邮件。 有三种对话 (也称为 "作用域) 在团队中：

* `teams` 也称为频道对话，对频道的所有成员可见。
* `personal` Bot 和单个用户之间的对话。
* `groupChat` 在 bot 和两个或更多用户之间聊天。 此外，还可以在会议聊天中启用你的 bot。

Bot 的行为略有不同，具体取决于它涉及的对话类型：

* 频道和分组聊天对话中的 bot 要求用户在频道中提及机器人以调用它。
* 一对一对话中的 bot 不需要 @ 提及。 用户发送的所有邮件都将被路由到你的 bot。

若要在特定范围内启用你的 bot，请将该作用域添加到你的 [应用程序清单](~/resources/schema/manifest-schema.md)。

## <a name="activities"></a>活动

每封邮件都是一 `Activity` 种类型的对象 `messageType: message` 。 当用户发送邮件时，工作组会将邮件发送到你的 bot。具体来说，它会将 JSON 对象发送到你的 bot 的邮件终结点。 你的 bot 将检查邮件以确定其类型并相应地做出响应。

基本对话通过 Bot 框架连接器（单个 REST API）处理，使你的 bot 能够与团队和其他频道进行通信。 自动程序生成器 SDK 提供了轻松访问此 API 的功能、用于管理对话流和状态的附加功能，以及将认知服务（如自然语言处理） (NLP) 集成的简单方法。

## <a name="receive-a-message"></a>接收邮件

若要接收短信，请使用 `Text` 对象的属性 `Activity` 。 在 bot 的活动处理程序中，使用 turn context 对象 `Activity` 读取单个邮件请求。

下面的代码显示了一个示例。

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

若要发送短信，请指定要作为活动发送的字符串。 在 bot 的活动处理程序中，使用 turn context 对象的 `SendActivityAsync` 方法发送单个邮件响应。 您还可以使用对象的 `SendActivitiesAsync` 方法一次发送多个响应。 下面的代码展示了在将某人添加到对话中时发送邮件的示例  

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

## <a name="teams-channel-data"></a>团队频道数据

该 `channelData` 对象包含特定于团队的信息，是团队和通道 id 的权威源。 您可能需要缓存这些 id 并将其用作本地存储的键。 `TeamsActivityHandler`SDK 中的通常会从对象中提取重要信息 `channelData` ，以使其更易于访问，但您始终可以访问对象中的原始信息 `turnContext` 。

在 `channelData` 个人对话的邮件中不包含该对象，因为它们在任何频道之外发生。

发送到你的 bot 的活动中的典型 channelData 对象包含以下信息：

* `eventType`团队事件类型;仅在[频道修改事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)的情况下传递
* `tenant.id` Azure Active Directory 租户 ID;在所有上下文中传递
* `team` 仅在通道上下文中传递，而不是在个人聊天中传递。
  * `id` 通道的 GUID
  * `name`团队的名称;仅在[团队重命名事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)的情况下传递
* `channel` 当提及 bot 时，仅在通道上下文中传递，或在已添加机器人的团队中的频道中传递事件
  * `id` 通道的 GUID
  * `name` 通道名称;仅在 [频道修改事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)的情况下传递。
* `channelData.teamsTeamId` 被. 包含此属性只是为了向后兼容。
* `channelData.teamsChannelId` 被. 包含此属性只是为了向后兼容。

### <a name="example-channeldata-object-channelcreated-event"></a> (channelCreated 事件的示例 channelData 对象) 

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

你的 bot 可以发送多信息文本、图片和卡片。 用户可以向你的 bot 发送丰富的文本和图片。

| Format    | 从用户到 bot | 从 bot 到用户 | 注释                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| 格式文本  | ✔                | ✔                |                                                                                         |
| 图片  | ✔                | ✔                | 最大1024×1024和 1 MB，PNG、JPEG 或 GIF 格式;不支持动态 GIF  |
| 卡     | ✖                | ✔                | 有关支持的卡片，请参阅[团队卡片参考](~/task-modules-and-cards/cards/cards-reference.md) |
| 表情符号    | ✖                | ✔                | 团队当前支持通过 UTF-16 (的表情符号，例如 U + 1F600 for grinning 脸)           |

## <a name="adding-notifications-to-your-message"></a>向邮件中添加通知

通知会提醒用户有关新任务、提及和注释（与他们的工作方式相关），或者需要将通知插入到其活动源中来查看。 您可以通过将 `TeamsChannelData` 对象属性设置为 true，将通知设置为触发来自 bot 邮件 `Notification.Alert` 。 是否引发通知将最终取决于单个用户的团队设置，并且无法以编程方式重写这些设置。 通知类型可以是横幅，也可以同时是横幅和电子邮件。

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

## <a name="picture-messages"></a>图片邮件

通过将附件添加到邮件来发送图片。 您可以在 [Bot 框架文档](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0)中找到有关附件的详细信息。

图片最多可以为1024×1024和 1 MB （PNG、JPEG 或 GIF 格式）;不支持动态 GIF。

建议使用 XML 指定每个图像的高度和宽度。 如果使用 Markdown，则图像大小默认为256×256。 例如：

* 改用 `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* 请勿使用- `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="next-steps"></a>后续步骤

* [发送主动消息](~/bots/how-to/conversations/send-proactive-messages.md)
* [订阅对话事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
