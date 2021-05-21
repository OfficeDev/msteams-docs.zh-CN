---
title: 使用自动程序发送和接收消息
description: 介绍如何在邮件中通过自动程序发送和接收Microsoft Teams
ms.topic: overview
localization_priority: Normal
keywords: teams 自动程序消息
ms.date: 05/20/2019
ms.openlocfilehash: e1926afe42bca45eda5f39be1be8342452b3aa24
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566493"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>与自动程序Microsoft Teams对话

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

对话是在你的机器人和一个或以上用户之间发送的一系列消息。 在 Teams 中有三种对话类型（也称范围）：

* `teams` 也称为频道对话，对频道的所有成员可见。
* `personal` 机器人和单个用户之间的对话。
* `groupChat` 机器人与两个或多个用户之间的聊天。

自动程序的行为稍有不同，具体取决于它涉及的对话类型：

* [频道和群聊](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) 对话中的聊天机器人要求用户@mention自动程序在频道中调用它。
* [单个用户对话中的](~/resources/bot-v3/bot-conversations/bots-conv-personal.md) 自动程序不需要@mention -用户只需键入。

为了使机器人能够处理特定范围，应在清单中列为支持该范围。 范围在清单参考中进行了进一步 [的定义和讨论](~/resources/schema/manifest-schema.md)。

## <a name="proactive-messages"></a>主动邮件

机器人可以参与对话或启动对话。 大多数通信都是为了响应另一条消息。 如果机器人启动对话，则称为主动 *消息*。 示例包括：

* 欢迎消息
* 事件通知
* 轮询消息

## <a name="conversation-basics"></a>对话基础知识

每条消息是类型 `messageType: message` 的一个 `Activity` 对象。 当用户发送消息时，Teams 会将消息发布给你的机器人。具体地说，它会发送一个 JSON 对象给你的机器人的消息传递端点。 自动程序将检查消息以确定其类型并相应地做出响应。

机器人还支持事件样式的消息。 有关详细信息，请参阅处理[Microsoft Teams 中的自动程序事件](~/resources/bot-v3/bots-notifications.md)。 语音当前不受支持。

消息在所有范围内大部分都相同，但在 UI 中访问自动程序的方式和你需要了解的场景差异存在差异。

基本对话通过 Bot Framework 连接器进行处理，该连接器是一个 REST API，使机器人能够Teams和其他频道进行通信。 Bot Builder SDK 提供了轻松访问此 API、管理对话流和状态的其他功能，以及合并认知服务（如自然语言处理和 NLP (）) 。

## <a name="message-content"></a>邮件内容

机器人可以发送格式文本、图片和卡片。 用户可以向自动程序发送格式文本和图片。 你可以指定自动程序可以在自动程序Microsoft Teams设置页中处理的内容类型。

| Format | 从用户到机器人  | 从自动程序到用户 |  备注 |
| --- | :---: | :---: | --- |
| 格式文本  | ✔ | ✔ |  |
| 图片 | ✔ | ✔ | PNG、JPEG 或 GIF 格式的最大大小为 1024×1024 和 1 MB;不支持动态 GIF。 |
| 卡 | ✖ | ✔ | 有关支持的[Teams，](~/task-modules-and-cards/cards/cards-reference.md)请参阅卡片参考。 |
| 表情符号 | ✖ | ✔ | Teams UTF-16 支持表情符号，例如 U+1F600 表示表情符号。 |
|

有关自动程序框架支持的机器人交互类型（团队中的机器人基于这些机器人）的信息，请参阅适用于[.NET](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0&preserve-view=true)的 Bot Builder [](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0&preserve-view=true) SDK 和适用于 Node.js的 Bot [Builder SDK](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0&preserve-view=true)文档中有关对话流和相关概念的 Bot Framework 文档。

## <a name="message-formatting"></a>消息格式

可以设置 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) 的可选属性 `message` ，以控制邮件文本内容的呈现方式。 有关 [自动程序消息](~/resources/bot-v3/bots-message-format.md) 中支持的格式的详细说明，请参阅邮件格式。
可以设置可选 [`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message&preserve-view=true) 属性来控制邮件文本内容的呈现方式。

有关团队中文本格式Teams的详细信息，请参阅自动[程序消息中的文本格式](~/resources/bot-v3/bots-text-formats.md)。

有关邮件中卡片格式设置详细信息，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。

## <a name="picture-messages"></a>图片消息

图片通过向邮件添加附件来发送。 有关附件的更多信息，请参阅 [Bot Framework 文档](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0&preserve-view=true)。

图片最多为 1024×1024 和 1 MB（PNG、JPEG 或 GIF 格式）;不支持动态 GIF。

建议您使用 XML 指定每个图像的高度和宽度。 如果使用 Markdown，图像大小默认为 256×256。 例如：

* 使用 `<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* 请勿使用 `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages&quot;></a>接收邮件

根据声明的范围，自动程序可以在以下上下文中接收消息：

* **个人聊天** 用户只需在聊天历史记录中选择已添加的聊天机器人，或在新聊天的&quot;目标：&quot;框中键入其名称或应用 ID，即可与机器人在私人对话中进行交互。
* **频道** 可以将机器人 (&quot;@_botname_") 如果已添加到团队，可以在频道中提及它。 请注意，频道中对自动程序的其他回复需要提及机器人。 它将不会在未提及的回复中回复。

对于传入消息，机器人会收到 [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0&preserve-view=true) 类型 为 的对象 `messageType: message` 。 虽然对象可以包含其他类型的信息（如发送到机器人的频道更新），但类型 `Activity` 表示机器人[](~/resources/bot-v3/bots-notifications.md#channel-updates) `message` 和用户之间的通信。

自动程序会收到包含用户消息的有效负载，以及有关用户的其他信息、消息源和Teams `Text` 信息。 注意：

* `timestamp` 使用协调世界时 UTC 格式 (邮件) 。
* `localTimestamp` 发件人时区的邮件日期和时间。
* `channelId` 始终为"msteams"。 这是指自动程序框架频道，而不是团队频道。
* `from.id` 自动程序的用户的唯一加密 ID;如果应用需要存储用户数据，则适合用作密钥。 它对于自动程序来说是唯一的，不能以任何有意义的方式直接在自动程序实例外部使用来标识该用户。
* `channelData.tenant.id` 用户的租户 ID。

> [!NOTE]
> `from.id` 对于自动程序是唯一的，不能以任何有意义的方式直接在自动程序实例外部使用来标识该用户。

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>将频道和私人交互与机器人结合使用

当在频道中交互时，自动程序应智能地与用户离线进行某些对话。 例如，假设用户尝试协调复杂的任务，例如与一组团队成员进行日程安排。 请考虑向用户发送个人聊天消息，而不是让整个交互序列对频道可见。 自动程序应该能够在个人和频道对话之间轻松转换用户，而不会丢失状态。

> [!NOTE]
>在交互完成时，不要忘记更新频道以通知其他团队成员。

## <a name="full-inbound-schema-example"></a>完整的入站架构示例

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
> 入站邮件的文本字段有时包含提及。 请务必正确检查并去除这些复选框。 有关详细信息，请参阅 [提及](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)。

## <a name="teams-channel-data"></a>Teams频道数据

对象 `channelData` 包含Teams特定的信息，是团队和频道的明确来源。 应缓存这些 ID，并用作本地存储的密钥。

`channelData`对象不包含在个人对话中的邮件中，因为这些事件发生在任何频道之外。

发送给自动程序的活动中的典型 channelData 对象包含以下信息：

* `eventType`Teams事件类型;仅在通道修改[事件的情况下传递](~/resources/bot-v3/bots-notifications.md#channel-updates)。
* `tenant.id`Azure Active Directory租户 ID;在所有上下文中传递。
* `team` 仅在频道上下文中传递，而不是在个人聊天中传递。
  * `id` 频道的 GUID。
  * `name` 团队名称;仅在团队重命名 [事件的情况下传递](~/resources/bot-v3/bots-notifications.md#team-name-updates)。
* `channel` 仅在提到自动程序时在频道上下文中传递，或针对团队中已添加自动程序的团队中的事件传递。
  * `id` 频道的 GUID。
  * `name` 频道名称;仅在通道修改 [事件的情况下传递](~/resources/bot-v3/bots-notifications.md#channel-updates)。
* `channelData.teamsTeamId` 已弃用。 此属性仅包含用于向后兼容。
* `channelData.teamsChannelId` 已弃用。 此属性仅包含用于向后兼容。

### <a name="example-channeldata-object-channelcreated-event"></a>channelCreated 事件 (channelCreated 事件示例) 

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

[Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)包提供了一个专用对象，该对象公开用于访问Teams `TeamsChannelData` 特定信息的属性。

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>发送对邮件的答复

若要回复现有邮件，请调用 [`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_&preserve-view=true) .NET 或 [`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities&preserve-view=true) Node.js。 Bot Builder SDK 处理所有详细信息。

如果选择使用 REST API，还可以调用 [`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0&preserve-view=true) 终结点。

邮件内容本身可以包含简单的文本，也可以包含一些 Bot Framework 提供的 [卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。

请注意，在出站架构中，应始终使用与收到的 `serviceUrl` 相同。 请注意，的值往往 `serviceUrl` 很稳定，但可能会更改。 当新消息到达时，机器人应验证其存储的值 `serviceUrl` 。

## <a name="updating-messages"></a>更新邮件

自动程序可以在发送邮件后动态更新内联消息，而不是让消息成为数据的静态快照。 你可以将动态消息更新用于轮询更新、在按下按钮后修改可用操作，或者任何其他异步状态更改。

新邮件的类型不需要与原始邮件匹配。 例如，如果原始邮件包含附件，则新邮件可以是简单的短信。

> [!NOTE]
> 只能更新在单附件邮件和盘车布局中发送的内容。 不支持在列表布局中发布具有多个附件的邮件更新。

### <a name="rest-api"></a>REST API

若要发出消息更新，只需使用给定的活动 ID 对终结点执行 PUT `/v3/conversations/<conversationId>/activities/<activityId>/` 请求。 若要完成此方案，您应缓存原始 POST 调用返回的活动 ID。

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>.NET 示例

可以使用 Bot Builder SDK 中的 方法 `UpdateActivityAsync` 更新现有邮件。

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

### <a name="nodejs-example"></a>Node.js示例

可以使用 Bot Builder SDK 中的 方法 `session.connector.update` 更新现有邮件。

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

## <a name="starting-a-conversation-proactive-messaging"></a>启动对话 (主动消息传递) 

你可以与用户创建个人对话，或在频道中为团队机器人启动新的回复链。 这使你可以向用户发送消息，而无需让他们首先与机器人联系。 有关详细信息，请参阅下列主题：

有关 [自动程序启动的对话](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) 的更多常规信息，请参阅自动程序主动消息传递。

## <a name="deleting-messages"></a>删除邮件

可以使用 BotBuilder SDK 中的 connectors [`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete) 方法 [删除邮件](/bot-framework/bot-builder-overview-getstarted)。

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
