---
title: 使用 bot 发送和接收邮件
description: 介绍如何使用 Microsoft 团队中的 bot 发送和接收邮件
keywords: 工作组 bot 消息
ms.date: 05/20/2019
ms.openlocfilehash: 864473c7f502d96987a48e5837840236c45f59c7
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673484"
---
# <a name="have-a-conversation-with-a-microsoft-teams-bot"></a>与 Microsoft 团队 bot 进行对话

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

对话是在你的 bot 和一个或多个用户之间发送的一系列邮件。 团队中有三种对话（也称为 "作用域"）：

* `teams`也称为频道对话，对频道的所有成员可见。
* `personal`Bot 和单个用户之间的对话。
* `groupChat`在 bot 和两个或更多用户之间聊天。

Bot 的行为略有不同，具体取决于它涉及的对话类型：

* [频道和分组聊天对话中的 bot](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)要求用户在频道中提及机器人以调用它。
* [单个用户对话中的 bot](~/resources/bot-v3/bot-conversations/bots-conv-personal.md)不需要 @ 提及-用户只需键入即可。

为了使机器人能够在特定范围内工作，应将其列为清单中支持该范围。 在[清单参考](~/resources/schema/manifest-schema.md)中定义和进一步讨论范围。

## <a name="proactive-messages"></a>主动消息

Bot 可以参与对话或启动对话。 大多数通信是对另一封邮件的响应。 如果 bot 启动对话，则它称为*主动消息*。 示例包括：

* 欢迎邮件
* 事件通知
* 轮询邮件

## <a name="conversation-basics"></a>对话基础知识

每封邮件都`Activity`是一种`messageType: message`类型的对象。 当用户发送邮件时，工作组会将邮件发送到你的 bot。具体来说，它会将 JSON 对象发送到你的 bot 的邮件终结点。 你的 bot 将检查邮件以确定其类型并相应地做出响应。

Bot 还支持事件样式的邮件。 有关详细信息，请参阅[在 Microsoft 团队中处理 bot 事件](~/resources/bot-v3/bots-notifications.md)。 目前不支持语音。

邮件在所有作用域中的作用最大，但在 UI 中访问 bot 的方式与在需要了解的幕后的差异方面存在差异。

基本对话通过 Bot 框架连接器（单个 REST API）处理，使你的 bot 能够与团队和其他频道进行通信。 机器人生成器 SDK 提供了轻松访问此 API 的功能、用于管理对话流和状态的附加功能，以及用于集成认知服务（如自然语言处理（NLP））的简单方法。

## <a name="message-content"></a>邮件内容

你的 bot 可以发送多信息文本、图片和卡片。 用户可以向你的 bot 发送丰富的文本和图片。 您可以在你的 bot 的 Microsoft 团队设置页中指定你的 bot 可以处理的内容类型。

| Format | 从用户到 bot  | 从 bot 到用户 |  注释 |
| --- | :---: | :---: | --- |
| 格式文本  | ✔ | ✔ |  |
| 图片 | ✔ | ✔ | 最大1024×1024和 1 MB，PNG、JPEG 或 GIF 格式;不支持动态 GIF |
| 圣诞卡 | ✖ | ✔ | 有关支持的卡片，请参阅[团队卡片参考](~/task-modules-and-cards/cards/cards-reference.md) |
| 表情符号 | ✖ | ✔ | 团队目前支持通过 UTF-16 进行的表情符号（例如，U + 1F600 for grinning 脸） |
|

有关 Bot 框架（团队中的自动程序基于）所支持的 bot 交互类型的详细信息，请参阅有关适用于[.net 的 Bot 生成器 sdk](/azure/bot-service/dotnet/bot-builder-dotnet-overview?view=azure-bot-service-3.0)的文档中的 "bot 框架"[框架和相关](/azure/bot-service/dotnet/bot-builder-dotnet-manage-conversation-flow?view=azure-bot-service-3.0)概念，以及[node.js 的 bot 生成器 sdk](/azure/bot-service/nodejs/bot-builder-nodejs-overview?view=azure-bot-service-3.0)。

## <a name="message-formatting"></a>邮件格式

您可以设置的[`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message) `message`可选属性来控制邮件的文本内容的呈现方式。 有关 bot 邮件中支持的格式的详细说明，请参阅[邮件格式](~/resources/bot-v3/bots-message-format.md)。
您可以设置可选[`TextFormat`](/azure/bot-service/dotnet/bot-builder-dotnet-create-messages?view=azure-bot-service-3.0#customizing-a-message)属性以控制邮件的文本内容的呈现方式。

有关团队如何在团队中支持文本格式的详细信息，请参阅[bot 邮件中的文本格式](~/resources/bot-v3/bots-text-formats.md)。

有关在邮件中设置卡片格式的信息，请参阅[卡片格式](~/task-modules-and-cards/cards/cards-format.md)。

## <a name="picture-messages"></a>图片邮件

通过将附件添加到邮件来发送图片。 您可以在[Bot 框架文档](/azure/bot-service/dotnet/bot-builder-dotnet-add-media-attachments?view=azure-bot-service-3.0)中找到有关附件的详细信息。

图片最多可以为1024×1024和 1 MB （PNG、JPEG 或 GIF 格式）;不支持动态 GIF。

建议使用 XML 指定每个图像的高度和宽度。 如果使用 Markdown，则图像大小默认为256×256。 例如：

* 改用`<img src="http://aka.ms/Fo983c" alt="Duck on a rock" height="150" width="223"></img>`
* 请勿使用 `![Duck on a rock](http://aka.ms/Fo983c)`

## <a name="receiving-messages"></a>接收邮件

根据声明的作用域，你的 bot 可以在以下上下文中接收邮件：

* **个人聊天**用户可以通过在聊天历史记录中选择添加的自动程序，或在新聊天中的 "到：" 框中键入其名称或应用 ID，在私人对话中与机器人进行交互。
* **通道**如果已将 bot 添加到团队，则可以在频道中提及 bot （"@_botname_"）。 请注意，频道中的 bot 的其他回复需要提及机器人。 它不会对未提到答复的答复做出响应。

对于传入的邮件，你的 bot [`Activity`](/azure/bot-service/rest-api/bot-framework-rest-connector-activities?view=azure-bot-service-3.0)接收到一个`messageType: message`类型的对象。 尽管该`Activity`对象可以包含其他类型的信息（如发送给你的 bot 的[频道更新](~/resources/bot-v3/bots-notifications.md#channel-updates)），但类型表示 bot 和用户之间的`message`通信。

你的 bot 将接收包含用户消息`Text`的有效负载，以及有关用户的其他信息、邮件源和团队信息。 注意：

* `timestamp`邮件的日期和时间（采用协调通用时间（UTC））
* `localTimestamp`发件人时区中邮件的日期和时间
* `channelId`始终为 "msteams"。 这指的是 bot 框架通道，而不是团队频道。
* `from.id`该用户对你的 bot 的唯一且加密的 ID;如果您的应用程序需要存储用户数据，则适用于键。 它对于你的 bot 是唯一的，不能以任何有意义的方式直接在机器人实例的外部使用，以标识该用户
* `channelData.tenant.id`用户的租户 ID。

> [!NOTE]
> `from.id`对于你的 bot 而言是唯一的，不能以任何有意义的方式直接在机器人实例外部使用，以标识该用户。

## <a name="combining-channel-and-private-interactions-with-your-bot"></a>将频道和私人交互与你的 bot 结合使用

在频道中进行交互时，您的 bot 应智能化与用户脱机使用某些对话的情况。 例如，假设某个用户试图协调复杂任务，例如，使用一组团队成员进行日程安排。 您可以考虑向用户发送个人聊天消息，而不是将整个交互序列显示在通道中。 你的 bot 应能够轻松在个人和频道对话之间切换用户，而不会失去状态。

> [!NOTE]
>在交互完成时，请不要忘记更新频道，以通知其他团队成员。

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
> 入站邮件的文本字段有时包含提到。 请务必正确检查和去除这些。 有关详细信息，请参阅[提到](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#-mentions)。

## <a name="teams-channel-data"></a>团队频道数据

该`channelData`对象包含特定于团队的信息，是团队和通道 id 的权威源。 应将这些 id 作为本地存储的键进行缓存和使用。

在`channelData`个人对话的邮件中不包含该对象，因为它们在任何频道之外发生。

发送到你的 bot 的活动中的典型 channelData 对象包含以下信息：

* `eventType`团队事件类型;仅在[频道修改事件](~/resources/bot-v3/bots-notifications.md#channel-updates)的情况下传递
* `tenant.id`Azure Active Directory 租户 ID;在所有上下文中传递
* `team`仅在通道上下文中传递，而不是在个人聊天中传递。
  * `id`通道的 GUID
  * `name`团队的名称;仅在[团队重命名事件](~/resources/bot-v3/bots-notifications.md#team-name-updates)的情况下传递
* `channel`当提及 bot 时，仅在通道上下文中传递，或在已添加机器人的团队中的频道中传递事件
  * `id`通道的 GUID
  * `name`通道名称;仅在[频道修改事件](~/resources/bot-v3/bots-notifications.md#channel-updates)的情况下传递。
* `channelData.teamsTeamId`被. 包含此属性只是为了向后兼容。
* `channelData.teamsChannelId`被. 包含此属性只是为了向后兼容。

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

" [Microsoft Bot. 团队](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)" NuGet 包提供专用`TeamsChannelData`对象，该对象公开了用于访问团队特定信息的属性。

```csharp
TeamsChannelData channelData = activity.GetChannelData<TeamsChannelData>();
string tenantId = channelData.Tenant.Id;
```

## <a name="sending-replies-to-messages"></a>向邮件发送答复

若要答复现有邮件，请在[`ReplyToActivity`](/dotnet/api/microsoft.bot.connector.conversationsextensions.replytoactivityasync?view=botbuilder-dotnet-3.0#Microsoft_Bot_Connector_ConversationsExtensions_ReplyToActivityAsync_Microsoft_Bot_Connector_IConversations_System_String_System_String_Microsoft_Bot_Connector_Activity_System_Threading_CancellationToken_) .net 或[`session.send`](/javascript/api/botbuilder-core/TurnContext?view=botbuilder-ts-latest&viewFallbackFrom=botbuilder-ts-3.0#sendactivities)在 node.js 中调用。 机器人生成器 SDK 处理所有详细信息。

如果选择使用 REST API，则还可以调用[`/v3/conversations/{conversationId}/activities/{activityId}`](/azure/bot-service/rest-api/bot-framework-rest-connector-send-and-receive-messages?view=azure-bot-service-3.0)终结点。

邮件内容本身可以包含简单文本或某些机器人框架提供的[卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。

请注意，在出站架构中，应始终使用与`serviceUrl`您接收到的相同。 请注意，的值`serviceUrl`往往是稳定的，但可能会发生变化。 当新邮件到达时，你的 bot 应验证其存储值`serviceUrl`。

## <a name="updating-messages"></a>更新邮件

你的 bot 不是让你的邮件成为数据的静态快照，而你的 bot 可以在发送邮件后动态更新这些邮件。 您可以对轮询更新、在按钮按下时修改可用操作或任何其他异步状态更改的方案使用动态邮件更新。

新邮件需要与类型中的原始邮件不匹配。 例如，如果原始邮件包含附件，则新邮件可以是简单的短信。

> [!NOTE]
> 您可以仅更新在单附件邮件和轮播版式中发送的内容。 不支持将更新发布到列表布局中包含多个附件的邮件。

### <a name="rest-api"></a>REST API

若要发出邮件更新，只需使用给定的活动 ID `/v3/conversations/<conversationId>/activities/<activityId>/`对终结点执行 PUT 请求即可。 若要完成此方案，您应缓存最初的 POST 呼叫返回的活动 ID。

```json
PUT /v3/conversations/19%3Aja0cu120i1jod12j%40skype.net/activities/012ujdo0128
{
    "type": "message",
    "text": "This message has been updated"
}
```

### <a name="net-example"></a>.NET 示例

您可以使用机器人`UpdateActivityAsync`生成器 SDK 中的方法来更新现有邮件。

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

您可以使用机器人`session.connector.update`生成器 SDK 中的方法来更新现有邮件。

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

您可以使用用户创建个人对话，也可以在频道中为您的团队 bot 创建一个新的答复链。 这样，你就可以在不先启动用户和你的 bot 的情况下向你的用户发送消息。 有关详细信息，请参阅下列主题：

有关 bot 启动的对话的更多常规信息，请参阅[短信服务的 bot](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) 。

## <a name="deleting-messages"></a>删除邮件

可以使用[BOTBUILDER SDK](/bot-framework/bot-builder-overview-getstarted)中的连接器[`delete()`](https://docs.botframework.com/node/builder/chat-reference/interfaces/_botbuilder_d_.iconnector.html#delete)方法删除邮件。

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
