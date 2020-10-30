---
title: 处理 bot 事件
description: 介绍如何处理 Microsoft 团队的 bot 中的事件
keywords: 团队 bot 事件
ms.date: 05/20/2019
author: laujan
ms.openlocfilehash: 5ef37a931d421f245cca4fbb984b69217f779785
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796174"
---
# <a name="handle-bot-events-in-microsoft-teams"></a>在 Microsoft 团队中处理 bot 事件

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft 团队将通知发送到你的 bot，以获取在你的 bot 处于活动状态的范围内发生的更改或事件。 您可以使用这些事件来触发服务逻辑，如以下内容：

* 在将你的 bot 添加到团队时触发欢迎消息
* 在将 bot 添加到组聊天时查询和缓存组信息
* 更新有关团队成员资格或通道信息的缓存信息
* 删除团队的缓存信息（如果删除了 bot）
* 当用户对 bot 邮件进行了赞时

每个 bot 事件都以对象的形式发送， `Activity` 其中定义了对象中的 `messageType` 信息。 有关类型的邮件 `message` ，请参阅 [发送和接收邮件](~/resources/bot-v3/bot-conversations/bots-conversations.md)。

团队和组事件（通常触发 `conversationUpdate` 类型）具有作为对象的一部分传递的其他团队事件信息 `channelData` ，因此您的事件处理程序必须查询团队的 `channelData` 有效负载 `eventType` 和其他特定于事件的元数据。

下表列出了你的 bot 可以接收并对其执行操作的事件。

|类型|有效负载对象|团队事件 = |说明|范围|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[添加到团队的成员](#team-member-or-bot-addition)| 各种 |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[成员已从团队中删除](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [团队已重命名](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [通道已创建](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [频道已重命名](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [频道已删除](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [对 bot 邮件的反应](#reactions)| 各种 |
| `messageReaction` |`reactionsRemoved`|| [从 bot 邮件中删除的反应](#reactions)| 各种 |

## <a name="team-member-or-bot-addition"></a>团队成员或 bot 添加

[`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate)当该事件收到有关已添加的团队成员身份更新的信息时，该事件将发送到你的 bot。 它还会在首次专门为个人对话而添加时收到更新。 请注意， () 的用户信息对 `Id` 你的 bot 而言是唯一的，并且可以缓存以供你的服务将来使用 (例如，向特定用户发送邮件) 。

### <a name="bot-or-user-added-to-a-team"></a>添加到团队的 Bot 或用户

`conversationUpdate` `membersAdded` 当将 bot 添加到团队或将新用户添加到添加了 bot 的团队中时，会发送具有有效负载中的对象的事件。 Microsoft 工作组也会添加到 `eventType.teamMemberAdded` `channelData` 对象中。

由于在这两种情况下都会发送此事件，因此应分析该 `membersAdded` 对象以确定添加是用户还是 bot 本身。 对于后者，最佳做法是将 [欢迎消息](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) 发送到频道，以便用户能够理解你的 bot 提供的功能。

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a>示例代码：检查 bot 是否为已添加的成员

##### <a name="net"></a>.NET

```csharp
    for (int i = 0; i < sourceMessage.MembersAdded.Count; i++)
    {
        if (sourceMessage.MembersAdded[i].Id == sourceMessage.Recipient.Id)
        {
            addedBot = true;
            break;
        }
    }
```

##### <a name="nodejs"></a>Node.js

```javascript
const builder = require('botbuilder');

var c = new builder.ChatConnector({appId: BOT_APP_ID, appPassword: .BOT_SECRET});
var bot = new builder.UniversalBot(c);

bot.on('conversationUpdate', (msg) => {
    var members = msg.membersAdded;
    // Loop through all members that were just added to the team
    for (var i = 0; i < members.length; i++) {

        // See if the member added was our bot
        if (members[i].id.includes(BOT_APP_ID)) {
            var botmessage = new builder.Message()
                .address(msg.address)
                .text('Hello World!');

            bot.send(botmessage, function(err) {});
        }
    }
});
```

#### <a name="schema-example-bot-added-to-team"></a>架构示例：添加到团队的 Bot

```json
{
    "membersAdded": [
        {
            "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:38:35.312Z",
    "localTimestamp": "2017-02-23T12:38:35.312-07:00",
    "id": "f:5f85c2ad",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberAdded",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

### <a name="bot-added-for-personal-context-only"></a>仅为个人上下文添加的 Bot

`conversationUpdate` `membersAdded` 当用户直接添加个人聊天时，你的 bot 会收到。 在这种情况下，你的 bot 接收的有效负载不包含该 `channelData.team` 对象。 如果您希望您的 bot 根据范围提供不同的 [欢迎消息](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) ，则应将此作为筛选器使用。

> [!NOTE]
> 对于个人范围内的 bot，你的 bot 只会 `conversationUpdate` 在一次时间内收到该事件，即使已删除并重新添加了 bot 也是如此。 对于开发和测试，您可能会发现，添加帮助程序函数将允许您完全重置你的 bot。 有关实现这一点的更多详细信息，请参阅 [Node.js 示例](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) 或 [c # 示例](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) 。

#### <a name="schema-example-bot-added-to-personal-context"></a>架构示例：添加到个人上下文的 bot

```json
{
  "membersAdded": [{
      "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
    },
    {
      "id": "29:<userID>",
      "aadObjectId": "***"
    }
  ],
  "type": "conversationUpdate",
  "timestamp": "2019-04-23T10:17:44.349Z",
  "id": "f:5f85c2ad",
  "channelId": "msteams",
  "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
  "from": {
    "id": "29:<USERID>",
    "aadObjectId": "**_"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "_*_"
  },
  "recipient": {
    "id": "28:<BOT ID>",
    "name": "<BOT NAME>"
  },
  "channelData": {
    "tenant": {
      "id": "<TENANT ID>"
    }
  }
}
```

## <a name="team-member-or-bot-removed"></a>删除了团队成员或 bot

`conversationUpdate` `membersRemoved` 当您的 bot 从团队中删除时，将会发送事件和有效负载中的对象，或者从已添加 bot 的团队中删除用户。 Microsoft 工作组也会添加到 `eventType.teamMemberRemoved` `channelData` 对象中。 与对象一样 `membersAdded` ，您应该为你的 `membersRemoved` Bot 的应用 ID 解析对象以确定已删除的用户。

### <a name="schema-example-team-member-removed"></a>架构示例：删除了工作组成员

```json
{
    "membersRemoved": [
        {
            "id": "29:1_LCi5Up14pAy65yZuaJzG1uIT7ujYhjjSTsUNqjORsZHjLHKiQIBJa4cX2XsAsRoaY7va2w6ZymA9-1VtSY_g"
        }
    ],
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:37:06.96Z",
    "localTimestamp": "2017-02-23T12:37:06.96-07:00",
    "id": "f:d8a6a4aa",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient":
    {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "teamMemberRemoved",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

## <a name="team-name-updates"></a>团队名称更新

> [!NOTE]
> 没有用于查询所有团队名称的功能，且未从其他事件的有效负载中返回团队名称。

重命名你的 bot 时，会通知你的你的团队。 它接收 `conversationUpdate` `eventType.teamRenamed` 对象中的事件 `channelData` 。 请注意，没有针对团队创建或删除的通知，因为 bot 仅作为团队的一部分存在，并且在添加它们的范围之外不可见。

### <a name="schema-example-team-renamed"></a>架构示例：团队已重命名

```json
{ 
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:35:56.825Z",
    "localTimestamp": "2017-02-23T12:35:56.825-07:00",
    "id": "f:1406033e",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/", 
    "from": { 
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
    }, 
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": { 
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype",
            "name": "New Team Name"
        },
        "eventType": "teamRenamed",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

## <a name="channel-updates"></a>频道更新

在已添加频道的团队中创建、重命名或删除频道时，将会通知你的 bot。 此外，还 `conversationUpdate` 会收到该事件，并将特定于团队的事件标识符作为该对象的一部分发送 `channelData.eventType` ，其中通道数据  `channel.id` 是通道的 GUID，并且 `channel.name` 包含通道名称本身。

通道事件如下所示：

_ **channelCreated** &emsp; 用户向团队添加新频道
* **channelRenamed** &emsp;用户重命名现有频道
* **channelDeleted** &emsp;用户删除频道

### <a name="full-schema-example-channelcreated"></a>完整架构示例： channelCreated

```json
{
    "type": "conversationUpdate",
    "timestamp": "2017-02-23T19:34:07.478Z",
    "localTimestamp": "2017-02-23T12:34:07.478-07:00",
    "id": "f:dd6ec311",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1wR7IdIRIoerMIWbewMi75JA3scaMuxvFon9eRQW2Nix5loMDo0362st2IaRVRirPZBv1WdXT8TIFWWmlQCizZQ"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterBot"
    },
    "channelData": {
        "channel": {
            "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
            "name": "FunDiscussions"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "eventType": "channelCreated",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a>架构摘录： channelData for channelRenamed

```json
⋮
"channelData": {
    "channel": {
        "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
        "name": "PhotographyUpdates"
    },
    "team": {
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "eventType": "channelRenamed",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    }
}
⋮
```

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a>架构摘录： channelData for channelDeleted

```json
⋮
"channelData": {
    "channel": {
        "id": "19:6d97d816470f481dbcda38244b98689a@thread.skype",
        "name": "PhotographyUpdates"
    },
    "team": {
        "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
    },
    "eventType": "channelDeleted",
    "tenant": {
        "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
    }
}
⋮
```

## <a name="reactions"></a>作出

`messageReaction`当用户在最初由你的 bot 发送的邮件中添加或删除他/她的反应时，会发送此事件。 `replyToId` 包含特定邮件的 ID。

### <a name="schema-example-a-user-likes-a-message"></a>架构示例：用户喜欢一封邮件

```json
{
    "reactionsAdded": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

### <a name="schema-example-a-user-un-likes-a-message"></a>架构示例：用户不喜欢某封邮件

```json
{
    "reactionsRemoved": [
        {
            "type": "like"
        }
    ],
    "type": "messageReaction",
    "timestamp": "2017-10-16T18:45:41.943Z",
    "id": "f:9f78d1f3",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1I9Is_Sx0O-Iy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA",
        "aadObjectId": "c33aafc4-646d-4543-9d4c-abd28e4d2110"
    },
    "conversation": {
        "isGroup": true,
        "conversationType": "channel",
        "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
    },
    "recipient": {
        "id": "28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
        "name": "SongsuggesterLocal"
    },
    "channelData": {
        "channel": {
            "id": "19:3629591d4b774aa08cb0887902eee7c1@thread.skype"
        },
        "team": {
            "id": "19:efa9296d959346209fea44151c742e73@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```
