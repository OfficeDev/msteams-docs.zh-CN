---
title: 使用机器人发送和接收消息
description: 介绍如何在 Microsoft Teams 中使用机器人发送和接收消息
ms.topic: overview
ms.localizationpriority: medium
keywords: teams 机器人消息
ms.date: 05/20/2019
ms.openlocfilehash: 0d4665d098e0e14fa3de5f2667c7e970b545b284
ms.sourcegitcommit: 430bf416bb8d1b74f926c8b5d5ffd3dbb0782286
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/10/2022
ms.locfileid: "65296971"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>与 Microsoft Teams 机器人进行对话

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

对话是在你的机器人和一个或以上用户之间发送的一系列消息。 在 Teams 中有三种对话类型（也称范围）：

* `teams`：也称频道对话，对频道的所有成员可见。
* `personal`：机器人与单一用户之间的对话。
* `groupChat`：机器人与两个及以上用户之间的聊天。

取决于机器人所处的对话种类，它们的行为可能略微不同：

* [频道和群聊对话中的机器人](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)要求用户@提及机器人来在频道中调用它。
* [单个用户对话中的机器人](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) 不需要@提及 - 用户只需键入即可。

为了使机器人在特定搜索范围中工作，它应在清单中列为支持该搜索范围。在 [清单参考](~/resources/schema/manifest-schema.md) 中进一步定义和讨论搜索范围。

## <a name="proactive-messages"></a>主动邮件

机器人可以参与对话或启动对话。 大多数通信是对另一条消息的响应。 如果机器人启动会话，则称为 *主动消息*。 示例包括：

* 欢迎消息
* 事件通知
* 轮询消息

## <a name="conversation-basics"></a>对话基础知识

每条消息是类型 `messageType: message` 的一个 `Activity` 对象。 当用户发送消息时，Teams 会将消息发布给你的机器人。具体地说，它会发送一个 JSON 对象给你的机器人的消息传递端点。 机器人会检查消息来确定其类型并作出相应响应。

机器人还支持事件样式消息。 有关详细信息，请参阅[处理 Microsoft Teams 中的机器人事件](~/resources/bot-v3/bots-notifications.md)。 当前不支持语音。

消息在所有范围内都是相同的，但是在 UI 中访问机器人的方式以及需要了解的幕后差异方面有些区别。

基本对话通过 Bot Framework Connector 进行处理，它是单个 REST API，使机器人能够与 Teams 和其他频道通信。 Bot Builder SDK 提供对此 API 的轻松访问、管理对话流和状态的附加功能，以及整合认知服务（如自然语言处理 (NLP)）的简单方法。

## <a name="message-content"></a>邮件内容

机器人可以发送格式文本、图片和卡片。 用户可以向机器人发送格式文本和图片。 可以在机器人的 Microsoft Teams 设置页面中指定机器人可处理的内容类型。

| 格式 | 从用户到机器人  | 从机器人到用户 |  注释 |
| --- | :---: | :---: | --- |
| 格式文本  | ✔ | ✔ |  |
| 图片 | ✔ | ✔ | 最大为 1024×1024 MB 以及 1 MB 的 PNG、JPEG 或 GIF 格式; 不支持动画 GIF。 |
| 卡片 | ✖ | ✔ | 有关支持的卡片，请参阅 [Teams 卡片参考](~/task-modules-and-cards/cards/cards-reference.md)。 |
| 表情符号 | ✖ | ✔ | Teams 目前支持通过 UTF-16 进行表情符号处理，例如 U+1F600 代表露齿笑。 |
|

有关 Bot Framework 支持的机器人交互类型（团队中的机器人基于这些类型）的详细信息，请参阅有关[对话流](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true)的 Bot Framework 文档以及文档中 [Bot Builder SDK for .NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true) 和 [Bot Builder SDK for Node.js](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true)的相关概念。

## <a name="message-formatting"></a>消息格式

可以设置 `message` 的可选 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) 属性来控制消息文本内容的呈现方式。 有关机器人消息中支持的格式的详细说明，请参阅[消息格式](~/resources/bot-v3/bots-message-format.md)。
可以设置可选 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) 属性来控制消息文本内容的呈现方式。

有关 Teams 如何支持团队中的文本格式的详细信息，请参阅[机器人消息中的文本格式](~/resources/bot-v3/bots-text-formats.md)。

有关在消息中设置卡片格式的详细信息，请参阅[卡片格式](~/task-modules-and-cards/cards/cards-format.md)。

## <a name="picture-messages"></a>图片消息

图片是通过将附件添加到消息来发送的。 可以在 [Bot Framework 文档](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)中找到有关附件的详细信息。

图片最多可以为 1024×1024 MB 以及 1 MB 的 PNG、JPEG 或 GIF 格式; 不支持动画 GIF。

建议使用 XML 指定每个图像的高度和宽度。 如果使用 Markdown，则图像大小默认为 256×256。 例如：

* 使用 `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* 请勿使用 `![Duck on a rock](http://aka.ms/Fo983c)`。

## <a name="receiving-messages"></a>接收消息

根据声明的范围，机器人可以在以下上下文中接收消息：

* **个人聊天** 用户可以在聊天历史记录中选择添加的机器人，或在新聊天的“收件人:”框中键入其名称或应用 ID，即可与机器人进行私人对话。
* **频道** 如果已将机器人添加到团队，则可以在频道中提及机器人（“@*botname*”）。 请注意，对频道中机器人的其他回复需要提及机器人。 它不会对未提及它的回复作出响应。

对于传入消息，机器人会收到类型 `messageType: message` 的 [活动](../../../bots/how-to/conversations/conversation-messages.md) 对象。尽管 `Activity` 对象可以包含其他类型的信息 (如发送到机器人的 [通道更新](~/resources/bot-v3/bots-notifications.md#channel-updates))，但 `message` 类型代表了机器人和用户之间的通信。

机器人会收到包含用户消息 `Text` 的有效负载以及有关用户的其他信息、消息源和 Teams 信息。注意:

* `timestamp` 以协调世界时 (UTC) 显示的消息日期和时间。
* `localTimestamp` 以发件人时区显示的消息日期和时间。
* `channelId` 始终为“msteams”。这指的是机器人框架频道，而不是团队频道。
* `from.id` 机器人用户的唯一和加密 ID；如果应用需要存储用户数据，则适合作为密钥。 这对于机器人是唯一的，不能以任何有意义的方式直接在机器人实例外部用于标识该用户。
* `channelData.tenant.id` 用户的租户 ID。

> [!NOTE]
> `from.id` 对于机器人是唯一的，不能以任何有意义的方式直接在机器人实例外部用于标识该用户。

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>将频道和专用交互与机器人结合使用

在频在频道中进行交互时，机器人应能够智能地与用户进行某些脱机对话。 例如，假设用户尝试协调复杂的任务，例如安排一组团队成员。 请考虑向用户发送个人聊天消息，而不是让整个交互序列对频道可见。 机器人应该能够轻松地在个人对话和频道对话之间转换用户，而不会失去状态。

> [!NOTE]
>交互完成后，请不要忘记更新频道以通知其他团队成员。

## <a name="full-inbound-schema-example"></a>完整入站架构示例

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

> [!NOTE]
> 入站消息的文本字段有时包含提及。 请务必正确检查并删除这些内容。 有关详细信息，请参阅[提及](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)。

## <a name="teams-channel-data"></a>Teams 频道数据

`channelData` 对象包含 Teams 特定的信息，是团队和频道 ID 的最终来源。 应缓存这些 ID 并将其用作本地存储的密钥。

发送给机器人的活动中的典型 channelData 对象包含以下信息：

* `eventType` Teams 事件类型；仅对[通道修改事件](~/resources/bot-v3/bots-notifications.md#channel-updates)传递。
* `tenant.id`Microsoft Azure Active Directory (Azure AD) 租户 ID；在所有上下文中传递。
* `team` 仅在频道上下文中传递，而不是在个人聊天中传递。
  * `id` 频道的 GUID。
  * `name` 团队名称；仅对[团队重命名事件](~/resources/bot-v3/bots-notifications.md#team-name-updates)传递。
* `channel` 仅在提及机器人时在频道上下文中传递，或者对在已添加机器人的 Teams 频道的事件传递。
  * `id` 频道的 GUID。
  * `name` 频道名称；仅对[频道修改事件](~/resources/bot-v3/bots-notifications.md#channel-updates)传递。
* `channelData.teamsTeamId` 已弃用。仅为向后兼容性而包含此属性。
* `channelData.teamsChannelId` 已弃用。仅为向后兼容性而包含此属性。

### <a name="example-channeldata-object-channelcreated-event"></a>示例 channelData 对象（channelCreated 事件）

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

### <a name="net-example"></a>.NET 示例

[Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet 包提供了一个专用 `TeamsChannelData` 对象，该对象将公开属性以访问 Teams 特定信息。

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>发送对消息的回复

若要回复现有消息，请在 .NET 中调用 [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) 或在 Node.js 中调用 [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true)。 Bot Builder SDK 会处理所有详细信息。

如果选择使用 REST API，则也可以调用 [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) 终结点。

消息内容本身可以包含简单的文本或 Bot Framework 提供的一些[卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。

请注意，在出站架构中，应始终使用与收到的相同的 `serviceUrl`。 请注意，`serviceUrl` 的值往往是稳定的，但可能会发生变化。 当新消息到达时，机器人应验证其存储的 `serviceUrl` 值。

## <a name="updating-messages"></a>更新消息

机器人可以在发送消息后以内联方式动态更新消息，而不是将消息设置为数据的静态快照。 可以针对轮询更新、按下按钮后修改可用操作或任何其他异步状态更改等方案使用动态消息更新。

新消息在类型上不需要与原始消息匹配。 例如，如果原始消息包含附件，则新消息可以是文本消息。

> [!NOTE]
> 只能更新在单附件消息和轮播布局中发送的内容。 不支持将更新发布到列表布局中包含多个附件的消息。

### <a name="rest-api"></a>REST API

若要发出消息更新，只需使用给定的活动 ID 对 `/v3/conversations/<conversationId>/activities/<activityId>/` 终结点执行 PUT 请求。 若要完成此方案，应缓存原始 POST 调用返回的活动 ID。

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>.NET 示例

可以使用 Bot Builder SDK 中的 `UpdateActivityAsync` 方法更新现有消息。

```csharp
public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
{
  if (activity.Type == ActivityTypes.Message)
  {
    ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
    Activity reply = activity.CreateReply($"You sent {activity.Text} which was {activity.Text.Length} characters");
    var msgToUpdate = await connector.Conversations.ReplyToActivityAsync(reply);
    Activity updatedReply = activity.CreateReply($"This is an updated message");
    await connector.Conversations.UpdateActivityAsync(reply.Conversation.Id, msgToUpdate.Id, updatedReply);
  }
}
```

### <a name="nodejs-example"></a>Node.js 示例

可以使用 Bot Builder SDK 中的 `session.connector.update` 方法更新现有消息。

```javascript
function sendCardUpdate(bot, session, originalMessage, address) {

  var origAttachment = originalMessage.data.attachments[0];
  origAttachment.content.subtitle = 'Assigned to Larry Jin';

  var updatedMsg = new builder.Message()
    .address(address)
    .textFormat(builder.TextFormat.markdown)
    .addAttachment(origAttachment)
    .toMessage();

  session.connector.update(updatedMsg, function(err, addresses) {
    if (err) {
      console.log(`Could not update the message`);
    }
  });
}
```

## <a name="starting-a-conversation-proactive-messaging"></a>启动对话（主动消息传递）

可以与用户创建个人对话，或在团队机器人的频道中启动新的回复链。 这让你可以向用户发送信息，而无需要用户首先主动与你的机器人联系。 有关详细信息，请参阅以下文章：

有关机器人启动的对话的更多常规信息，请参阅[机器人的主动消息传递](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。

## <a name="deleting-messages"></a>删除消息

可以使用 [BotBuilder SDK](/bot-framework/bot-builder-overview-getstarted) 中的连接器 [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html) 方法删除消息。

```typescript
bot.dialog('BotDeleteMessage', function (session: builder.Session) {
  var msg = new teams.TeamsMessage(session).text("Bot will delete this message in 5 sec.")
  bot.send(msg, function (err, response) {
    if (err) {
      console.log(err);
      session.endDialog();
    }

    console.log('Proactive message response:');
    console.log(response);
    console.log('---------------------------------------------------')
    setTimeout(function () {
      var activityId: string = null;
      var messageAddress: builder.IChatConnectorAddress = null;
      if (response[0]){
        messageAddress = response[0];
        activityId = messageAddress.id;
      }

      if (activityId == null)
      {
        console.log('Message failed to send.');
        session.endDialog();
        return;
      }

      // Bot delete message
      let address: builder.IChatConnectorAddress  = {
        channelId: 'msteams',
        user: messageAddress.user,
        bot: messageAddress.bot,
        id : activityId,
        serviceUrl : (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
        conversation: {
          id: session.message.address.conversation.id
        }
      };

      connector.delete(address, function (err) {
        if (err)
        {
          console.log(err);
        }
        else
        {
          console.log("Message: " + activityId + " deleted successfully.");
        }

        // Try editing deleted message would fail
        var newMsg = new builder.Message().address(address).text("To edit message.");
        connector.update(newMsg.toMessage(), function (err, address) {
          if (err)
          {
            console.log(err);
            console.log('Deleted message can not be edited.');
          }
          else
          {
            console.log("There is something wrong. Message: " + activityId + " edited successfully.");
            console.log(address);
          }

          session.endDialog();
        });
      });
    }, 5000);
  });
})
```
