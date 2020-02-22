---
title: 与 bot 的频道和组聊天对话
description: 介绍在 Microsoft 团队中与频道中的 bot 进行对话的端到端方案
keywords: 团队方案频道对话机器人
ms.date: 06/25/2019
ms.openlocfilehash: d2d72bdba43de6ebb10c7504dd309459cb09d56c
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "42227996"
---
# <a name="channel-and-group-chat-conversations-with-a-microsoft-teams-bot"></a>与 Microsoft 团队 bot 的频道和组聊天对话

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft 团队允许用户将 bot 引入其频道或组聊天对话。 通过向团队或聊天添加机器人，对话的所有用户都可以充分利用对话中的 bot 功能。 您还可以访问您的 bot 中特定于团队的功能，例如查询团队信息和 @mentioning 用户。

频道和组聊天中的聊天与个人聊天中的不同之处在于用户需要 @mention 机器人。 如果在多个作用域（个人、groupchat 或通道）中使用了 bot，则需要检测 bot 邮件的作用域，并相应地进行处理。

## <a name="designing-a-great-bot-for-channels-or-groups"></a>为频道或组设计出色的 bot

添加到团队的 bot 成为另一个团队成员，可作为对话的一部分 @mentioned。 事实上，bot 仅在 @mentioned 时收到邮件，因此频道上的其他对话不会发送到机器人。

> [!NOTE]
> 为了在回复频道中的 bot 邮件时方便起见，自动将 bot 名称附加到撰写消息框中。

组或频道中的 bot 应提供与所有成员相关且适用的信息。 虽然你的 bot 可以提供与体验相关的任何信息，但请记住，每个人都能看到与之相关的对话。 因此，组或频道中的一个很棒的 bot 应为所有用户添加值，当然不会在一对一对话中无意中共享更多的信息。

你的 bot 在所有作用域中都可能完全相关，并且不需要执行大量额外的工作来允许你的机器人在它们之间工作。 在 Microsoft 团队中，不会认为你的 bot 在所有作用域中都能正常运行，但应确保你的 bot 在你选择支持的任何范围内提供用户值。 有关作用域的详细信息，请参阅[Microsoft 团队中的应用](~/concepts/build-and-test/app-studio-overview.md)。

开发在组或频道中工作的 bot 使用的功能与个人对话中的功能非常相似。 有效负载中的其他事件和数据提供团队组和通道信息。 以下各节介绍了这些差异以及常见功能中的主要差异。

### <a name="creating-messages"></a>创建邮件

有关在通道中创建邮件的 bot 的详细信息，请参阅[针对 bot 的主动消息传送](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)，以及专门[创建通道对话](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md#creating-a-channel-conversation)。

### <a name="receiving-messages"></a>接收邮件

对于组或通道中的 bot，除了[常规邮件架构](https://docs.botframework.com/core-concepts/reference/#activity)之外，你的 bot 也会收到以下属性：

* `channelData`请参阅[团队频道数据](~/resources/bot-v3/bot-conversations/bots-conversations.md#teams-channel-data)。 在组聊天中，包含与该聊天相关的信息。
* `conversation.id`答复链 ID，由通道 ID 和回复链中的第一封邮件的 ID 组成
* `conversation.isGroup``true`用于频道或组聊天中的 bot 邮件
* `conversation.conversationType``groupChat`或者`channel`
* `entities`可以包含一个或多个提及（请参阅[提及](#-mentions)）

### <a name="replying-to-messages"></a>答复邮件

若要答复现有邮件，请在[`ReplyToActivity`](/bot-framework/dotnet/bot-builder-dotnet-connector#send-a-reply) .net 或[`session.send`](/bot-framework/nodejs/bot-builder-nodejs-use-default-message-handler)在 node.js 中调用。 机器人生成器 SDK 处理所有详细信息。

如果选择使用 REST API，则还可以调用[`/conversations/{conversationId}/activities/{activityId}`](/bot-framework/rest-api/bot-framework-rest-connector-send-and-receive-messages#send-the-reply)终结点。

在频道中，回复邮件显示为对启动答复链的答复。 `conversation.id`包含通道和顶级邮件 ID。 尽管 Bot 框架`conversation.id`提供了详细信息，但您可以根据需要将其缓存，以供将来对该会话线程的回复。

### <a name="best-practice-welcome-messages-in-teams"></a>最佳实践：团队中的欢迎邮件

当你的 bot 第一次添加到组或团队时，向所有用户发送欢迎消息向所有用户引入的欢迎消息通常很有用。 欢迎消息应提供 bot 功能和用户权益的说明。 理想情况下，邮件还应包括用户与应用程序进行交互的命令。 为此，请确保你的 bot 对`conversationUpdate`邮件做出响应，并在`teamsAddMembers` `channelData`对象中使用事件类型。 请确保`memberAdded` ID 是 Bot 的应用程序 ID 本身，因为当用户添加到团队中时，会发送相同的事件。 有关更多详细信息，请参阅[团队成员或 bot 添加](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)。

添加 bot 时，您可能还希望向团队的每个成员发送个人消息。 为此，您可以[提取团队名单](~/resources/bot-v3/bots-context.md#fetching-the-team-roster)并向每个用户发送一[条直接消息](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。

建议您在以下情况下*不*发送欢迎邮件：

* 团队规模较大（显然是主观，但例如，大于100个成员）。 你的 bot 可能被视为 "垃圾"，添加它的人可能会收到投诉，除非你清楚地将你的 bot 的价值主张传达给可看到欢迎消息的每个人。
* 你的 bot 首先在组或频道中提及（而不是首次添加到团队）
* 重命名组或通道
* 将团队成员添加到组或通道

## <a name="-mentions"></a>@ 提到

由于组或通道中的 bot 仅在邮件中被提及（"@_botname_"）时响应，因此组频道中的 bot 收到的每封邮件都包含其自己的名称，您必须确保您的邮件分析处理该情况。 此外，bot 还可以分析提到的其他用户，并将用户提及为其邮件的一部分。

### <a name="retrieving-mentions"></a>检索提及

提到在有效负载的`entities`对象中返回，并且包含用户的唯一 ID，在大多数情况下，提到的用户的名称。 您可以通过在用于 .NET 的 Bot 生成器 SDK 中`GetMentions`调用函数来检索邮件中的所有提及，这将返回对象`Mentioned`的数组。

#### <a name="net-example-code-check-for-and-strip-bot-mention"></a>.NET 示例代码：检查并去除 @bot 提及

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
> 您还可以使用 "团队扩展" `GetTextWithoutMentions`功能，该函数将去除所有提及内容，包括 bot。

#### <a name="nodejs-example-code-check-for-and-strip-bot-mention"></a>Node.js 示例代码：检查并去除 @bot 提及的内容

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

您还可以使用 "团队扩展" `getTextWithoutMentions`功能，该函数将去除所有提及内容，包括 bot。

### <a name="constructing-mentions"></a>构建提及

你的 bot 可以在发送到频道的邮件中提及其他用户。 若要执行此操作，您的邮件必须执行以下操作：

* 在`<at>@username</at>`邮件文本中包含
* 将`mention`对象包括在实体集合中

#### <a name="net-example"></a>.NET 示例

本示例使用的是 ".[团队](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)" NuGet 包。

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

#### <a name="example-outgoing-message-with-user-mentioned"></a>示例：提到的用户的传出邮件

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

## <a name="accessing-groupchat-or-channel-scope"></a>访问 groupChat 或通道范围

你的 bot 可以执行的操作不仅仅是在组和团队中发送和接收邮件。 例如，它还可以提取成员列表，包括其配置文件信息和通道列表。 若要了解详细信息，请参阅[获取 Microsoft 团队 bot 的上下文](~/resources/bot-v3/bots-context.md)。

*另请参阅* [Bot 框架示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
