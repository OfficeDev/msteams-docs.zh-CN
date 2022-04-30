---
title: 使用机器人进行频道和群组聊天对话
description: 介绍在 Microsoft Teams 的频道中使用机器人进行对话的端到端方案
keywords: Teams, 方案, 频道, 对话, 机器人
ms.localizationpriority: high
ms.topic: conceptual
ms.date: 06/25/2019
ms.openlocfilehash: a3b508a5caa70ff2ecea24840c24448f3f8622b6
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111666"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>带有 Microsoft Teams 机器人的频道和群聊对话

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams 允许用户将机器人引入其频道或群组聊天对话。 通过将机器人添加到团队或聊天，对话的所有用户都可以直接在对话中利用机器人功能。 你还可以访问机器人中特定于 Teams 的功能，例如查询团队信息和 @提及用户。

频道和群组聊天中的聊天不同于个人聊天，因为用户需要 @提及机器人。 如果在多个范围（例如个人、群组聊天或频道）中使用机器人，则需要检测机器人消息来自什么范围，并相应地处理它们。

## <a name="designing-a-great-bot-for-channels-or-groups"></a>为频道或群组设计出色的机器人

添加到团队的机器人将成为另一个团队成员，并且可以作为对话的一部分 @提及。 事实上，机器人只有在被 @提及时才会收到消息，因此频道上的其他对话不会发送给机器人。

群组或频道中的机器人应为所有成员提供相关且适当的信息。 虽然机器人当然可以提供与体验相关的任何信息，但请记住，每个人都能看到与它的对话。 因此，群组或频道中的出色机器人应该为所有用户增加价值，当然不会无意中分享更适合一对一对话的信息。

正如设计的那样，机器人可能在所有范围内都完全相关，而无需额外的工作。 在 Microsoft Teams 中，不期望机器人在所有范围内都能正常工作，但应确保机器人在你选择支持的任何范围内都能提供用户价值。 有关范围的详细信息，请参阅 [Microsoft Teams 中的应用](~/concepts/build-and-test/app-studio-overview.md)。

开发在群组或频道中工作的机器人使用与个人对话相同的许多功能。 有效负载中的其他事件和数据提供 Teams 群组和频道信息。 以下部分介绍了这些差异以及常见功能的主要差异。

### <a name="creating-messages"></a>创建消息

有关机器人在频道中创建消息的详细信息，请参阅[机器人的主动消息传递](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)，特别是[创建频道对话](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)。

### <a name="receiving-messages"></a>接收消息

对于群组或频道中的机器人，除了[常规消息架构](https://docs.botframework.com/core-concepts/reference/#activity)外，机器人还会收到以下属性：

* `channelData` 请参阅 [Teams 频道数据](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)。 在群组聊天中，包含特定于该聊天的信息。
* `conversation.id` 回复链 ID，包括频道 ID 和回复链中第一条消息的 ID。
* `conversation.isGroup` 对于频道或群组聊天中的机器人消息为 `true`。
* `conversation.conversationType` `groupChat` 或 `channel`。
* `entities` 可以包含一个或多个提及。 有关详细信息，请参阅[提及](#-mentions)。

### <a name="replying-to-messages"></a>回复消息

若要回复现有消息，请在 .NET 中调用 [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) 或在 Node.js 中调用 [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler)。 Bot Builder SDK 会处理所有详细信息。

如果选择使用 REST API，则也可以调用 [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) 终结点。

在频道中，回复消息将显示为对启动回复链的回复。 `conversation.id` 包含频道和顶级消息 ID。 尽管 Bot Framework 会处理详细信息，但你可以缓存该 `conversation.id`，以便将来根据回复该对话线程。

### <a name="best-practice-welcome-messages-in-teams"></a>最佳做法：Teams 中的欢迎消息

首次将机器人添加到群组或团队时，向所有用户发送介绍机器人的欢迎消息通常非常有用。 欢迎消息应提供机器人功能和用户权益的说明。 理想情况下，消息还应包括用户与应用交互的命令。 为此，请确保机器人使用 `channelData` 对象中的 `teamsAddMembers` eventType 响应 `conversationUpdate` 消息。 请确保 `memberAdded` ID 是机器人的应用 ID 本身，因为在将用户添加到团队时会发送相同的事件。 有关更多详细信息，请参阅[团队成员或机器人添加](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)。

添加机器人时，可能还需要向团队的每个成员发送个人消息。 为此，可以[提取团队名单](~/resources/bot-v3/bots-context.md#fetch-the-team-roster)并向每个用户发送[直接消息](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。

建议机器人在以下情况下 *不要* 发送欢迎消息：

* 团队非常庞大（很明显是主观的，例如，超过 100 个成员）。 机器人可能会被视为“垃圾”，添加它的人可能会收到投诉，除非你清楚地将机器人的价值主张传达给看到欢迎消息的每个人。
* 首先在群组或频道中提及机器人，而不是首先将其添加到团队。
* 群组或频道已重命名。
* 将团队成员添加到群组或频道。

## <a name="-mentions"></a>@提及

由于群组或频道中的机器人只有当在消息中被提及时才会响应（“@*botname*”），因此群组频道中的机器人收到的每条消息都包含自己的名称，必须确保消息分析功能处理该名称。 此外，机器人可以分析提及的其他用户，并在其消息中提及用户。

### <a name="retrieving-mentions"></a>检索提及

提及在有效负载的 `entities` 对象中返回，并包含用户的唯一 ID，在大多数情况下，还包含提及的用户名。 可以通过调用 Bot Builder SDK for .NET 中的 `GetMentions` 函数来检索消息中的所有提及，该函数将返回一组 `Mentioned` 对象。

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>.NET 示例代码：检查和删除 @bot 提及

```csharp
Mention[] m = sourceMessage.GetMentions();
var messageText = sourceMessage.Text;

for (int i = 0;i < m.Length;i++)
{
    if (m[i].Mentioned.Id == sourceMessage.Recipient.Id)
    {
        //Bot is in the @mention list.
        //The below example will strip the bot name out of the message, so you can parse it as if it wasn't included. Note that the Text object will contain the full bot name, if applicable.
        if (m[i].Text != null)
            messageText = messageText.Replace(m[i].Text, "");
    }
}
```

> [!NOTE]
> 你还可以使用 Teams 扩展函数 `GetTextWithoutMentions` 删除所有提及（包括机器人）。

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.js 示例代码：检查和删除 @bot 提及

```javascript
var text = message.text;
if (message.entities) {
    message.entities
        .filter(entity => ((entity.type === "mention") && (entity.mentioned.id.toLowerCase() === botId)))
        .forEach(entity => {
            text = text.replace(entity.text, "");
        });
    text = text.trim();
}
```

你还可以使用 Teams 扩展函数 `getTextWithoutMentions` 删除所有提及（包括机器人）。

### <a name="constructing-mentions"></a>构造提及

机器人可以在发布到频道的消息中提及其他用户。 为此，消息必须执行以下操作：

* 在消息文本中包含 `<at>@username</at>`。
* 在实体集合中包括 `mention` 对象。

#### <a name="net-example"></a>.NET 示例

此示例使用 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet 包。

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a>Node.js 示例

```javascript
// User to mention
var toMention: builder.IIdentity = {
    name: 'John Doe',
    id: userId
};

// Create a message and add mention to it
var msg = new teams.TeamsMessage(session).text(teams.TeamsMessage.getTenantId(session.message));
var mentionedMsg = msg.addMentionToText(toMention);

// Post the message
var generalMessage = mentionedMsg.routeReplyToGeneralChannel();
session.send(generalMessage);
```

#### <a name="example-outgoing-message-with-user-mentioned"></a>示例：与所提及用户的传出消息

```json
{
    "type": "message", 
    "text": "Hey <at>Pranav Smith</at> check out this message",
    "timestamp": "2017-10-29T00:51:05.9908157Z",
    "localTimestamp": "2017-10-28T17:51:05.9908157-07:00",
    "serviceUrl": "https://skype.botframework.com",
    "channelId": "msteams",
    "from": {
        "id": "28:9e52142b-5e5e-4d7b-bb3e- e82dcf620000",
        "name": "SchemaTestBot"
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

## <a name="accessing-groupchat-or-channel-scope"></a>访问群组聊天或频道范围

机器人可以执行的不仅仅是在群组和团队中发送和接收消息。 例如，它还可以提取成员列表，包括其个人资料信息以及频道列表。 有关详细信息，请参阅[获取 Microsoft Teams 机器人的上下文](~/resources/bot-v3/bots-context.md)。

## <a name="see-also"></a>另请参阅

[Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
