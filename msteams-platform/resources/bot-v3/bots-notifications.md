---
title: 处理机器人事件
description: 在本模块中，了解如何在机器人中处理Microsoft Teams、Teams成员或机器人添加、已删除团队成员或机器人等事件
ms.date: 05/20/2019
ms.topic: how-to
ms.localizationpriority: medium
ms.author: lajanuar
author: surbhigupta
ms.openlocfilehash: 95d6439d396a61471c0e7dbe5942d4b88cc00a87
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189320"
---
# <a name="handle-bot-events-in-microsoft-teams"></a>处理 Microsoft Teams 中的机器人事件

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

对于在机器人活动范围内发生的事件，Microsoft Teams 会向机器人发送通知。 可以使用这些事件触发服务逻辑，例如：

* 在将机器人添加到团队时，触发欢迎消息。
* 将机器人添加到群组聊天时，查询并缓存组群组信息。
* 更新关于团队成员身份或频道信息的缓存信息。
* 如果删除了机器人，则删除团队的缓存信息。
* 用户对机器人消息点赞时。

每个机器人事件都作为 `Activity` 对象发送，其中 `messageType` 定义对象中的信息。 有关类型 `message` 的消息，请参阅 [ 发送和接收消息 ](~/resources/bot-v3/bot-conversations/bots-conversations.md)。

Teams和组事件（从类型中触发）`conversationUpdate`具有作为对象一`channelData`部分传递的更多Teams事件信息，因此事件处理程序必须查询`channelData`Teams`eventType`和更多特定于事件的元数据的有效负载。

下表列出了机器人可以接收并采取措施的事件。

|类型|有效负载对象|Teams eventType |说明|范围|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[ 添加到团队的成员 ](#team-member-or-bot-addition)| 全部 |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[ 成员已从团队中删除 ](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [ 已重命名团队 ](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [ 已创建频道 ](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [ 已重命名频道 ](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [ 已删除频道 ](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [ 对机器人消息的回应 ](#reactions)| 全部 |
| `messageReaction` |`reactionsRemoved`|| [ 从机器人消息中删除的回应 ](#reactions)| 全部 |

## <a name="team-member-or-bot-addition"></a>添加团队成员或机器人

当机器人收到关于其所属团队的成员身份更新信息时，[`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) 事件会发送给机器人。 在首次专门为个人对话添加机器人时，机器人也会收到更新。  () `Id` 的用户信息对于机器人是唯一的，可以缓存以供服务将来使用，例如向特定用户发送消息。

### <a name="bot-or-user-added-to-a-team"></a>添加到团队的机器人或用户

将机器人添加到团队或将新用户添加到已添加机器人的团队时，会发送有效负载中包含 `membersAdded` 对象的 `conversationUpdate` 事件。 Teams还会在对象中`channelData`添加`eventType.teamMemberAdded`。

由于此事件在这两种情况下都发送，因此应解析 `membersAdded` 对象以确定添加的对象是用户还是机器人本身。 对于后者，最佳做法是向频道发送 [ 欢迎消息 ](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams)，以便用户可以了解机器人提供的功能。

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a>示例代码：检查机器人是否是添加的成员

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

#### <a name="schema-example-bot-added-to-team"></a>架构示例：添加到团队的机器人

```json
{
   "membersAdded":[
      {
         "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2017-02-23T12:38:35.312-07:00",
   "id":"f:5f85c2ad",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:1I9Is_Sx0OIy2rQ7Xz1lcaPKlO9eqmBRTBuW6XzkFtcjqxTjPaCMij8BVMdBcL9L_RwWNJyAHFQb0TRzXgyQvA"
   },
   "conversation":{
      "isGroup":true,
      "conversationType":"channel",
      "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
   },
   "recipient":{
      "id":"28:f5d48856-5b42-41a0-8c3a-c5f944b679b0",
      "name":"SongsuggesterBot"
   },
   "channelData":{
      "team":{
         "id":"19:efa9296d959346209fea44151c742e73@thread.skype"
      },
      "eventType":"teamMemberAdded",
      "tenant":{
         "id":"72f988bf-86f1-41af-91ab-2d7cd011db47"
      }
   }
}
```

### <a name="user-added-to-a-meeting"></a>添加到会议的用户

将用户添加到私人预定会议时，将发送有效负载中包含 `membersAdded` 对象的 `conversationUpdate` 事件。 即便是匿名用户加入会议，也会发送事件详细信息。

> [!NOTE]
>
>* 将匿名用户添加到会议时，membersAdded 有效负载对象没有 `aadObjectId` 字段。
>* 将匿名用户添加到会议时，即使该匿名用户是由其他演示者添加的，有效负载中的 `from` 对象始终具有会议组织者的 ID。

#### <a name="schema-example-user-added-to-meeting"></a>架构示例：添加到会议中的用户

```json
{
   "membersAdded":[
      {
         "id":"229:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"
      }
   ],
   "type":"conversationUpdate",
   "timestamp":"2017-02-23T19:38:35.312Z",
   "localTimestamp":"2020-09-29T21:11:38.6542339Z",
   "id":"f:a8cd1b51-9ddb-bd35-624b-7f7474165df8",
   "channelId":"msteams",
   "serviceUrl":"https://canary.botapi.skype.com/amer/",
   "from":{
      "id":"29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",
      "aadObjectId":"f30ba569-abef-4e97-8762-35f85cbae706"
   },
   "conversation":{
      "isGroup":true,
      "tenantId":"e15762ef-a8d8-416b-871c-25516354f1fe",
      "id":"19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"
   },
   "recipient":{
      "id":"28:3af3604a-d4fc-486b-911e-86fab41aa91c",
      "name":"EchoBot1_Rename"
   },
   "channelData":{
      "tenant":{
         "id":"e15762ef-a8d8-416b-871c-25516354f1fe"
      },
      "source":null,
      "meeting":{
         "id":"MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="
      }
   }
}

```

### <a name="bot-added-for-personal-context-only"></a>仅针对个人上下文添加的机器人

当用户直接添加它进行个人聊天时，机器人会收到具备 `membersAdded` 的 `conversationUpdate`。 在这种情况下，机器人收到的有效负载不包含 `channelData.team` 对象。 如果希望机器人根据范围提供不同的 [ 欢迎消息 ](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations)，则应使用此选项作为筛选器。

> [!NOTE]
> 对于个人范围的机器人，即使机器人被删除并重新添加，机器人也会多次收到 `conversationUpdate` 事件。 对于开发和测试，你可能会发现添加帮助程序函数非常有用，该函数让你可以完全重置机器人。 有关实现此操作的更多详细信息，请参阅 [ Node.js示例 ](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) 或 [ C# 示例 ](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238)。

#### <a name="schema-example-bot-added-to-personal-context"></a>架构示例：添加到个人上下文中的机器人

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
    "aadObjectId": "***"
  },
  "conversation": {
    "conversationType": "personal",
    "id": "***"
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

## <a name="team-member-or-bot-removed"></a>已删除团队成员或机器人

从团队中删除机器人、或者从添加了机器人的团队中删除用户时，将发送有效负载中具有 `membersRemoved` 对象的 `conversationUpdate` 事件。 Teams还会在对象中`channelData`添加`eventType.teamMemberRemoved`。 与 `membersAdded` 对象一样，应解析机器人应用 ID 的 `membersRemoved` 对象，以确定被删除的对象。

### <a name="schema-example-team-member-removed"></a>架构示例：被删除的团队成员

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

### <a name="user-removed-from-a-meeting"></a>从会议中删除的用户

当用户从私人预定会议中删除时，将发送有效负载中包含 `membersRemoved` 对象的 `conversationUpdate` 事件。 即便是匿名用户加入会议，也会发送事件详细信息。

> [!NOTE]
>
>* 从会议中删除匿名用户时，membersRemoved 有效负载对象没有 `aadObjectId` 字段。
>* 从会议中删除匿名用户时，即使该匿名用户是由其他演示者删除的，有效负载中的 `from` 对象始终具有会议组织者的 ID。

#### <a name="schema-example-user-removed-from-meeting"></a>架构示例：从会议中删除的用户

```
{   
      "membersRemoved": 
        {  
          "id": "29:1Z_XHWBMhDuehhDBYoPQD6Y1DSFsTtqOZx-SA5Jh9Y4zHKm4VbFGRn7-rK7SWiW1JECwxkMdrWpHoBut2sSyQPA"   
        }   
      ],   
      "type": "conversationUpdate",   
      "timestamp": "2020-09-29T21:15:08.6391139Z",   
      "id": "f:ee8dfdf3-54ac-51de-05da-9d49514974bb",   
      "channelId": "msteams",   
      "serviceUrl": "https://canary.botapi.skype.com/amer/",   
      "from": {   
        "id": "29:1siKxZhSoTapsXvI0gyf7Gywm_HM-4kEQW4BJnWuFYVIVu87xCNP99nidgQRCcwD3L3p_schiMShzx8IDRzf8mw",   
        "aadObjectId": "f30ba569-abef-4e97-8762-35f85cbae706"   
      },   
      "conversation": {    
        "isGroup": true,   
        "tenantId": "e15762ef-a8d8-416b-871c-25516354f1fe",   
        "id": "19:meeting_MWJlNGViOTgtMGExYi00NDA3LWExODgtOTZhMWNlYjM4ZTRj@thread.v2"   
      },   
      "recipient": {   
        "id": "28:3af3604a-d4fc-486b-911e-86fab41aa91c",   
        "name": "EchoBot1_Rename"   
      },   
      "channelData": {   
        "tenant": {   
          "id": "e15762ef-a8d8-416b-871c-25516354f1fe"   
        },   
        "source": null,   
        "meeting": {   
          "id": "MCMxOTptZWV0aW5nX01XSmxOR1ZpT1RndE1HRXhZaTAwTkRBM0xXRXhPRGd0T1RaaE1XTmxZak00WlRSakB0aHJlYWQudjIjMA=="   
        }   
      }   
}
```

## <a name="team-name-updates"></a>团队名称更新

> [!NOTE]
> 没有查询所有团队名称的功能，并且没有从其他事件的有效负载中返回团队名称。

当机器人所在的团队已重命名时，机器人会收到通知。 它在 `channelData` 对象中接收具备 `eventType.teamRenamed` 的 `conversationUpdate` 事件。 请注意，没有关于团队创建或删除的通知，因为机器人仅作为团队的一部分存在，并且在添加它们的范围之外没有可见性。

### <a name="schema-example-team-renamed"></a>架构示例：已重命名团队

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

在添加机器人的团队中创建、重命名或删除频道时，会通知机器人。 同样，会收到 `conversationUpdate` 事件，并且将特定于 Teams 的事件标识符作为 `channelData.eventType` 对象的一部分发送，其中频道数据的 `channel.id` 是频道的 GUID，并且 `channel.name` 包含频道名称本身。

频道事件如下所示：

* **channelCreated**&emsp; 用户向团队添加新频道。
* **channelRenamed**&emsp; 用户重命名现有频道。
* **channelDeleted**&emsp; 用户删除频道。

### <a name="full-schema-example-channelcreated"></a>完整架构示例：channelCreated

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a>架构摘录：channelRenamed 的 channelData

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a>架构摘录：channelDeleted 的 channelData

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

## <a name="reactions"></a>回应

`messageReaction`当用户添加或删除其对最初由机器人发送的消息的反应时，将发送该事件。 `replyToId` 包含特定消息的 ID。

### <a name="schema-example-a-user-likes-a-message"></a>架构示例：用户点赞了某条消息

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

### <a name="schema-example-a-user-un-likes-a-message"></a>架构示例：用户未点赞某条消息

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
