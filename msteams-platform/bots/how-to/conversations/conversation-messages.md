---
title: 智能机器人对话中的邮件
description: 了解如何发送接收消息、建议的操作、通知、附件、图像、自适应卡片和状态错误代码响应。
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: 16849a9e8ed97854e91934aef9de463eb355fec5
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833203"
---
# <a name="messages-in-bot-conversations"></a>智能机器人对话中的邮件

对话中的每个消息都是 `Activity` 类型的 `messageType: message`对象。 当用户发送消息时，Microsoft Teams 会将消息发布到机器人。 Teams 将 JSON 对象发送到机器人的消息传送终结点，Teams 仅允许一个终结点进行消息传递。 机器人会检查消息来确定其类型并作出相应响应。

基本对话通过 Bot Framework 连接器（单个 REST API）进行处理。 此 API 使机器人能够与 Teams 和其他频道通信。 Bot Builder SDK 提供以下功能：

* 轻松访问 Bot Framework 连接器。
* 用于管理聊天流和状态的功能。
* 合并认知服务的简单方法，例如自然语言处理 (NLP) 。

机器人使用 属性从 Teams 接收消息， `Text` 并向用户发送单个或多个消息响应。

有关详细信息，请参阅 [机器人消息的用户属性](/microsoftteams/platform/messaging-extensions/how-to/action-commands/respond-to-task-module-submit?tabs=dotnet%2Cdotnet-1&branch=pr-en-us-5926#user-attribution-for-bots-messages)。

## <a name="receive-a-message"></a>接收消息

若要接收文本消息，请使用 `Text` 对象的 属性 `Activity` 。 在机器人的活动处理程序中，使用圈上下文对象的 `Activity` 来读取单一消息请求。

以下代码演示了接收消息的示例：

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

若要发送文本消息，请指定要作为活动发送的字符串。 在机器人的活动处理程序中，使用轮次上下文对象的 `SendActivityAsync` 方法发送单个消息响应。 使用 对象的 `SendActivitiesAsync` 方法发送多个响应。

以下代码演示了在将用户添加到对话时发送消息的示例：

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
>
>* 在同一活动有效负载中发送短信和附件时，会发生消息拆分。 Teams 将此活动拆分为两个单独的活动，一个活动包含短信，另一个包含附件。 拆分活动时，不会在响应中收到消息 ID，该 ID 用于主动 [更新或删除](~/bots/how-to/update-and-delete-bot-messages.md) 消息。 建议发送单独的活动，而不是根据消息拆分。
>* 可以本地化发送的消息以提供个性化设置。 有关详细信息，请参阅 [本地化应用](../../../concepts/build-and-test/apps-localization.md)。

在用户和机器人之间发送的消息包括消息中的内部通道数据。 此数据允许机器人在该通道上正确通信。 Bot Builder SDK 允许修改消息结构。

## <a name="send-suggested-actions"></a>发送建议的操作

建议的操作使机器人能够显示用户可以选择提供输入的按钮。 建议的操作可让用户通过选择按钮来回答问题或做出选择，而不是使用键盘键入响应，从而增强用户体验。
当用户选择按钮时，它在富卡中保持可见和可访问，但对于建议的操作则不可见。 这可以防止用户在对话中选择过时的按钮。

若要向消息添加建议的操作，请设置`suggestedActions`[活动](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference)对象的 属性，以指定表示要向用户显示的按钮的[卡片操作](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference)对象列表。 有关更多信息，请参阅[`sugestedActions`](/dotnet/api/microsoft.bot.builder.messagefactory.suggestedactions)。

下面是建议操作的实现和体验的示例：

``` json
"suggestedActions": {
    "actions": [
      {
        "type": "imBack",
        "title": "Action 1",
        "value": "Action 1"
      },
      {
        "type": "imBack",
        "title": "Action 2",
        "value": "Action 2"
      }
    ],
    "to": [<list of recepientIds>]
  }
```

下面演示了建议的操作的示例：

:::image type="content" source="~/assets/images/Cards/suggested-actions.png" alt-text="机器人建议的操作" border="true":::

> [!NOTE]
>
> * `SuggestedActions` 仅支持一对一聊天机器人和基于文本的消息，而不适用于自适应卡片或附件。
> * `imBack` 是唯一受支持的操作类型，Teams 最多显示三个建议的操作。

## <a name="teams-channel-data"></a>Teams 频道数据

对象 `channelData` 包含特定于 Teams 的信息，是团队和频道 ID 的权威源。 （可选）可以缓存这些 ID 并将其用作本地存储的密钥。 `TeamsActivityHandler` SDK 中的 从 `channelData` 对象中提取重要信息，使其可访问。 但是，始终可以从 对象访问原始数据 `turnContext` 。

对象 `channelData` 不包括在个人对话的消息中，因为这些发生在频道之外。

发送到机器人的活动中的典型 `channelData` 对象包含以下信息：

* `eventType`：仅在 [通道修改](~/bots/how-to/conversations/subscribe-to-conversation-events.md)事件的情况下传递的 Teams 事件类型。
* `tenant.id`：Microsoft Azure Active Directory (在所有上下文中传递的 Azure AD) 租户 ID。
* `team`：仅在频道上下文中传递，不在个人聊天中传递。
  * `id`：通道的 GUID。
  * `name`：仅在团队 [重命名事件](subscribe-to-conversation-events.md#team-renamed)的情况下传递的团队名称。
* `channel`：仅在通道上下文中传递，当机器人被提及时，或者对于团队中已添加机器人的频道中的事件。
  * `id`：通道的 GUID。
  * `name`：仅在通道 [修改事件的情况下传递的通道](~/bots/how-to/conversations/subscribe-to-conversation-events.md)名称。
* `channelData.teamsTeamId`：废弃。 仅为了向后兼容而包含此属性。
* `channelData.teamsChannelId`：废弃。 仅为了向后兼容而包含此属性。

### <a name="example-channeldata-object-channelcreated-event"></a>示例 channelData 对象（channelCreated 事件）

以下代码显示了 channelData 对象的一个示例：

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

从机器人接收或发送到机器人的消息可以包括不同类型的消息内容。

| 格式    | 从用户到机器人 | 从机器人到用户 | 注释                                                                                   |
|-----------|------------------|------------------|-----------------------------------------------------------------------------------------|
| 格式文本  | ✔️                | ✔️                | 机器人可以发送格式文本、图片和卡片。 用户可以向机器人发送格式文本和图片。                                                                                        |
| 图片  | ✔️                | ✔️                | PNG、JPEG 或 GIF 格式的最大 1024 × 1024 像素和 1 MB。 不支持动态 GIF。 |
| 卡片     | ❌                | ✔️                | 有关支持的卡片，请参阅 [Teams 卡参考](~/task-modules-and-cards/cards/cards-reference.md) 。 |
| 表情符号    | ✔️                | ✔️                | Teams 目前通过 UTF-16 支持表情符号，例如用于笑脸的 U+1F600。 |

### <a name="picture-messages"></a>图片消息

若要增强邮件，可以将图片作为附件包含在邮件中。 有关附件的详细信息，请参阅 [向邮件添加媒体附件](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments)。

图片最多可以为 1024 × 1024 像素和 1 MB，采用 PNG、JPEG 或 GIF 格式。 不支持动态 GIF。

使用 XML 指定每个图像的高度和宽度。 在 Markdown 中，图像大小默认为 256×256。 例如：

* 使用： `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`。
* 请勿使用： `![Duck on a rock](http://aka.ms/Fo983c)`。

聊天机器人可以包含可简化业务工作流的自适应卡片。 自适应卡片提供丰富的可自定义文本、语音、图像、按钮和输入字段。

### <a name="adaptive-cards"></a>自适应卡

自适应卡片可以在机器人中创作，并在多个应用（如 Teams、网站等）中显示。 有关详细信息，请参阅 [自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)。

以下代码演示发送简单自适应卡片的示例：

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

#### <a name="form-completion-feedback"></a>表单完成反馈

可以使用自适应卡片生成表单完成反馈。 向机器人发送响应时，表单完成消息显示在自适应卡片中。 消息可以是两种类型：错误或成功：

* **错误**：当发送到机器人的响应不成功时， **出现错误，将显示“重试”** 消息。

     :::image type="content" source="../../../assets/images/Cards/error-message.png" alt-text="错误消息"border="true":::

* **成功**：当发送到机器人的响应成功时， **将显示“你的响应已发送到应用”** 消息。

     :::image type="content" source="../../../assets/images/Cards/success.PNG" alt-text="成功消息"border="true":::

     可以选择“ **关闭** ”或“切换聊天”以消除消息。

     如果不想显示成功消息，请在 属性中`msTeams``feedback`将 属性`hide``true`设置为 。 下面是一个示例：

     ```json
        "content": {
            "type": "AdaptiveCard",
            "title": "Card with hidden footer messages",
            "version": "1.0",
            "actions": [
            {
                "type": "Action.Submit",
                "title": "Submit",
                "msTeams": {
                    "feedback": {
                    "hide": true
                    }
                }
            }
            ]
        } 
     ```

有关机器人中的卡片和卡片的详细信息，请参阅 [卡片文档](~/task-modules-and-cards/what-are-cards.md)。

## <a name="add-notifications-to-your-message"></a>向邮件添加通知

可通过两种方式从应用程序发送通知：

* 通过在机器人消息上设置 `Notification.Alert` 属性。
* 通过使用图形 API发送活动源通知。

可以使用 属性向消息 `Notification.Alert` 添加通知。 通知会提醒用户注意应用程序中的事件，例如新任务、提及或注释。 这些警报与用户正在处理的内容或用户必须查看的内容（通过将通知插入其活动源）相关。 若要从机器人消息触发通知，请将 `TeamsChannelData` objects `Notification.Alert` 属性设置为 *true*。 如果引发通知取决于单个用户的 Teams 设置，则无法替代这些设置。

如果要生成任意通知而不向用户发送消息，则可以使用 图形 API。 有关详细信息，请参阅[如何使用图形 API发送活动源通知](/graph/teams-send-activityfeednotifications)以及[最佳做法](/graph/teams-activity-feed-notifications-best-practices)。

> [!NOTE]
> “ **摘要”** 字段在源中将来自用户的任何文本显示为通知消息。

以下代码演示了向消息添加通知的示例：

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

## <a name="status-codes-from-bot-conversational-apis"></a>机器人对话 API 中的状态代码

确保在 Teams 应用中正确处理这些错误。 下表列出了生成错误的错误代码和说明：

| 状态代码 | 错误代码和消息值 | 说明 | 重试请求 | 开发人员操作 |
|----------------|-----------------|-----------------|----------------|----------------|
| 400 | **代码**： `Bad Argument` <br/> **消息**：*方案特定 | 机器人提供的请求有效负载无效。 有关具体的详细信息，请参阅错误消息。 | 否 | 重新评估错误的请求有效负载。 有关详细信息，请查看返回的错误消息。 |
| 401 | **代码**： `BotNotRegistered` <br/> **消息**：找不到此机器人的注册。 | 找不到此机器人的注册。 | 否 | 验证机器人 ID 和密码。 确保机器人 ID (AAD ID) 已在 Teams 开发人员门户中注册，或通过 Azure 中的 Azure 机器人通道注册（已启用“Teams”通道）。|
| 403 | **代码**： `BotDisabledByAdmin` <br/> **消息**：租户管理员已禁用此机器人 | 租户管理员已阻止用户与机器人应用之间的交互。 租户管理员需要在应用策略中允许用户使用应用。 有关详细信息，请参阅 [应用策略](/microsoftteams/app-policies)。 | 否 | 停止发布到聊天，直到聊天中的用户显式启动与机器人的交互，指示机器人不再被阻止。 |
| 403 | **代码**： `BotNotInConversationRoster` <br/> **消息**：机器人不是对话名单的一部分。 | 机器人不是对话的一部分。 需要在对话中重新安装应用。 | 否 | 在尝试发送另一个会话请求之前，请等待事件 [`installationUpdate`](~/bots/how-to/conversations/subscribe-to-conversation-events.md#install-update-event) ，该事件指示机器人已重新添加。|
| 403 | **代码**： `ConversationBlockedByUser` <br/> **消息**：用户阻止了与机器人的对话。 | 用户已通过审查设置在个人聊天或频道中阻止机器人。 | 否 | 从缓存中删除对话。 停止尝试发布到对话，直到聊天中的用户显式启动与机器人的交互，指示机器人不再被阻止。 |
| 403 |**代码**： `InvalidBotApiHost` <br/> **消息**：机器人 API 主机无效。 对于 GCC 租户，请调用 `https://smba.infra.gcc.teams.microsoft.com`。|机器人为属于 GCC 租户的会话调用公共 API 终结点。| 否 | 将会话的服务 URL 更新为 `https://smba.infra.gcc.teams.microsoft.com` 并重试请求。|
| 403 | **代码**： `NotEnoughPermissions` <br/> **消息**：*方案特定 | 机器人没有执行请求的操作所需的权限。 | 否 | 从错误消息中确定所需的操作。 |
| 404 | **代码**： `ActivityNotFoundInConversation` <br/> **消息**：找不到对话。 | 在对话中找不到提供的消息 ID。 消息不存在或已删除。 | 否 | 检查发送的消息 ID 是否为预期值。 如果 ID 已缓存，请删除该 ID。 |
| 404 | **代码**： `ConversationNotFound` <br/> **消息**：找不到对话。 | 找不到对话，因为它不存在或已被删除。 | 否 | 检查发送的对话 ID 是否为预期值。 如果 ID 已缓存，请删除该 ID。 |
| 412 | **代码**： `PreconditionFailed` <br/> **消息**：前置条件失败，请重试。 | 由于同一会话上的多个并发操作，某个依赖项的前置条件失败。 | 是 | 使用指数退避重试。 |
| 413 | **代码**： `MessageSizeTooBig` <br/> **消息**：消息大小过大。 | 传入请求的大小太大。 有关详细信息，请参阅 [设置机器人消息的格式](/microsoftteams/platform/bots/how-to/format-your-bot-messages)。 | 否 | 减小有效负载大小。 |
| 429 | **代码**： `Throttled` <br/> **消息**：请求过多。 还返回稍后重试时间。 | 机器人发送的请求过多。 有关详细信息，请参阅 [速率限制](/microsoftteams/platform/bots/how-to/rate-limit)。 | 是 | 使用 `Retry-After` 标头重试以确定回退时间。 |
| 500 | **代码**： `ServiceError` <br/> **消息**：*各 | 内部服务器错误。 | 否 | 在 [开发人员社区](~/feedback.md#developer-community-help)中报告问题。 |
| 502 | **代码**： `ServiceError` <br/> **消息**：*各 | 服务依赖项问题。 | 是 | 使用指数退避重试。 如果问题仍然存在，请在 [开发人员社区](~/feedback.md#developer-community-help)中报告问题。 |
| 503 | | 服务不可用。 | 是 | 使用指数退避重试。 如果问题仍然存在，请在 [开发人员社区](~/feedback.md#developer-community-help)中报告问题。 |
| 504 | | 网关超时。 | 是 | 使用指数退避重试。 如果问题仍然存在，请在 [开发人员社区](~/feedback.md#developer-community-help)中报告问题。 |

### <a name="status-codes-retry-guidance"></a>状态代码重试指南

下表列出了每个状态代码的常规重试指南，机器人必须避免重试未指定的状态代码：

|状态代码 | 重试策略 |
|----------------|-----------------|
| 403 | 通过调用 的 GCC API `https://smba.infra.gcc.teams.microsoft.com` 进行 `InvalidBotApiHost`重试。|
| 412 | 使用指数退避重试。 |
| 429 | 使用 `Retry-After` 标头重试，以确定等待时间（以秒为单位），以及请求之间的等待时间（如果可用）。 否则，请尽可能使用带线程 ID 的指数回退重试。 |
| 502 | 使用指数退避重试。 |
| 503 | 使用指数退避重试。 |
| 504 | 使用指数退避重试。 |

## <a name="code-sample"></a>代码示例

| 示例名称 | Description | Node.js | .NETCore | Python | .NET |
|----------------|-----------------|--------------|----------------|-----------|-----|
| Teams 对话自动程序 | 消息传递和对话事件处理。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) | 不适用 |
| Teams 应用本地化 | 使用机器人和选项卡的 Teams 应用本地化。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/nodejs) | NA | NA | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-localization/csharp) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [机器人命令菜单](~/bots/how-to/create-a-bot-commands-menu.md)

## <a name="see-also"></a>另请参阅

* [发送主动邮件](~/bots/how-to/conversations/send-proactive-messages.md)
* [订阅对话事件](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
* [通过机器人发送和接收文件](~/bots/how-to/bots-filesv4.md)
* [将租户 ID 和对话 ID 发送到机器人的请求标头](~/bots/how-to/conversations/request-headers-of-the-bot.md)
* [本地化应用](../../../concepts/build-and-test/apps-localization.md)
