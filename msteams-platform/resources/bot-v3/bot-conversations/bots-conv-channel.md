---
title: 与机器人的频道和群聊对话
description: 介绍在 Microsoft Teams 的频道中与机器人对话的端到端方案
keywords: 团队方案频道对话机器人
ms.date: 06/25/2019
ms.openlocfilehash: e556eb006257a83ddf93adb62f79857201d6a9ad
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231629"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>与 Microsoft Teams 机器人的频道和群聊对话

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams 允许用户将机器人引入其频道或群聊对话。 通过将机器人添加到团队或聊天，对话的所有用户都可以在对话中充分利用机器人功能。 还可以在机器人中访问特定于 Teams 的功能，例如查询团队信息和@mentioning用户。

频道和群聊中的聊天不同于个人聊天，因为用户需要@mention聊天机器人。 如果自动程序用于个人、 (或频道) 则需要检测自动程序消息来自的作用域，并相应地处理它们。

## <a name="designing-a-great-bot-for-channels-or-groups"></a>为频道或组设计出色的自动程序

添加到团队的机器人将成为另一个团队成员，@mentioned对话的一部分。 事实上，自动程序仅在收到@mentioned时接收消息，因此频道上的其他对话不会发送给机器人。

组或频道中的机器人应提供与所有成员相关且合适的信息。 虽然机器人当然可以提供与体验相关的任何信息，但请记住，与体验相关的对话对所有人都可见。 因此，组或频道中出色的自动程序应该为所有用户增加价值，并且当然不会无意中共享更适用于一对一对话的信息。

与现在一样，机器人可能在所有范围内完全相关，无需额外工作。 在 Microsoft Teams 中，机器人功能在所有范围内都没有任何预期，但应确保自动程序在选择支持的任何 (范围内) 用户价值。 有关范围详细信息，请参阅 Microsoft [Teams 中的应用](~/concepts/build-and-test/app-studio-overview.md)。

开发在组或频道中工作的自动程序使用与个人对话相同的大部分功能。 有效负载中的其他事件和数据提供 Teams 组和频道信息。 以下各节介绍了这些差异以及常见功能的主要差异。

### <a name="creating-messages"></a>创建邮件

有关机器人在频道中创建消息详细信息，请参阅 [自动](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)程序主动消息传递，尤其是 [创建频道对话](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)。

### <a name="receiving-messages"></a>接收邮件

对于组或频道中的自动程序，除了常规邮件 [架构](https://docs.botframework.com/core-concepts/reference/#activity)之外，机器人还会收到以下属性：

* `channelData` 请参阅 [Teams 频道数据](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)。 在群聊中，包含特定于该聊天的信息。
* `conversation.id` 回复链 ID，由频道 ID 以及回复链中第一封邮件的 ID 组成
* `conversation.isGroup` 用于 `true` 频道或群聊中的自动程序消息
* `conversation.conversationType`或者 `groupChat``channel`
* `entities`可包含一个或多个提及 ([请参阅"提及) ](#-mentions)

### <a name="replying-to-messages"></a>回复邮件

若要答复现有邮件，请通过 [`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) .NET 或 [`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler) Node.js。 自动程序生成器 SDK 处理所有详细信息。

如果选择使用 REST API，还可以调用 [`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply) 终结点。

在频道中，回复消息将显示为对启动回复链的回复。 包含 `conversation.id` 通道和顶级邮件 ID。 尽管 Bot Framework 会处理详细信息，但您可以根据需要缓存这些详细信息，供以后回复该 `conversation.id` 对话线程。

### <a name="best-practice-welcome-messages-in-teams"></a>最佳做法：Teams 中的欢迎消息

当你的机器人首次添加到组或团队时，向所有用户发送一条欢迎消息，向所有用户介绍机器人通常很有用。 欢迎消息应提供自动程序功能和用户优势的说明。 理想情况下，该消息还应包含用户与应用交互的命令。 为此，请确保机器人使用 `conversationUpdate` `teamsAddMembers` 对象的 eventType 响应 `channelData` 邮件。 请确保 ID 是自动程序的应用 ID 本身，因为将用户添加到团队时将发送相同的 `memberAdded` 事件。 有关 [更多详细信息，请参阅团队成员或](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition) 机器人添加。

添加自动程序时，您可能还需要向团队的每个成员发送个人消息。 为此，你可以获取 [团队名单](~/resources/bot-v3/bots-context.md#fetch-the-team-roster) ，并发送一条直接 [消息给每个用户](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。

建议机器人 *在* 下列情况下不要发送欢迎消息：

* 团队规模较大 (明显具有主观性，但例如，超过 100 个成员) 。 你的机器人可能会被视为"spabot"，并且添加它的人可能会收到投诉，除非你向看到欢迎消息的每个人清楚地传达了机器人的价值主张。
* 你的自动程序首先在组或频道 (，而不是先添加到团队) 
* 重命名组或频道
* 将团队成员添加到组或频道

## <a name="-mentions"></a>@ 提及

由于组或频道中的自动程序仅在消息中提到 ("@_botname_") 时进行响应，因此组频道中的自动程序接收的每封邮件都包含其自己的名称，并且必须确保邮件分析能够处理该名称。 此外，机器人可以分析提及的其他用户，并提及用户作为消息的一部分。

### <a name="retrieving-mentions"></a>检索提及

提及在有效负载的对象中返回，并且同时包含用户的唯一 ID，在大多数情况下，还包含 `entities` 提及的用户名称。 可以通过调用 .NET 的 Bot Builder SDK 中的函数来检索邮件中提及的所有内容，这将 `GetMentions` 返回对象 `Mentioned` 数组。

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>.NET 示例代码：检查并去除@bot提及

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
> 您还可以使用 Teams 扩展函数，该函数去除所有提及， `GetTextWithoutMentions` 包括自动程序。

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.js代码：检查并去除@bot提及

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

您还可以使用 Teams 扩展函数，该函数去除所有提及， `getTextWithoutMentions` 包括自动程序。

### <a name="constructing-mentions"></a>构造提及

机器人可以在发布到频道的消息中提及其他用户。 为此，您的邮件必须执行以下操作：

* 包括在 `<at>@username</at>` 邮件文本中
* 将 `mention` 对象包括在实体集合内

#### <a name="net-example"></a>.NET 示例

此示例使用 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet 程序包。

```csharp
// Create reply activity
Activity replyActivity = activity.CreateReply();

// Construct text of the form @sender Hello
replyActivity.Text = "Hello ";
replyActivity.AddMentionToText(activity.From, MentionTextLocation.AppendText);

// Send the reply activity
await client.Conversations.ReplyToActivityAsync(replyActivity);
```

#### <a name="nodejs-example"></a>Node.js示例

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

#### <a name="example-outgoing-message-with-user-mentioned"></a>示例：已提及用户的传出邮件

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

## <a name="accessing-groupchat-or-channel-scope"></a>访问群聊或频道范围

机器人可以执行更多操作，而不是在组和团队中发送和接收消息。 例如，它还可以获取成员列表，包括其配置文件信息以及频道列表。 有关详细信息 [，请参阅"获取 Microsoft Teams 机器人](~/resources/bot-v3/bots-context.md) 的上下文"。

*另请参阅 Bot* [Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
