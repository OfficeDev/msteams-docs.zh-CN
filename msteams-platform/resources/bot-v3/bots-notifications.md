---
title: 处理机器人事件
description: 介绍如何处理自动程序 for Microsoft Teams
keywords: teams 机器人事件
ms.date: 05/20/2019
ms.topic: how-to
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 5a7f7971d7f58af315222933f1c1f192868a4171
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020637"
---
# <a name="handle-bot-events-in-microsoft-teams"></a><span data-ttu-id="6057f-104">处理聊天机器人Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="6057f-104">Handle bot events in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="6057f-105">Microsoft Teams自动程序在活动范围内发生的更改或事件，向自动程序发送通知。</span><span class="sxs-lookup"><span data-stu-id="6057f-105">Microsoft Teams sends notifications to your bot for changes or events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="6057f-106">可以使用这些事件触发服务逻辑，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6057f-106">You can use these events to trigger service logic, such as the following:</span></span>

* <span data-ttu-id="6057f-107">将机器人添加到团队时触发欢迎消息</span><span class="sxs-lookup"><span data-stu-id="6057f-107">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="6057f-108">将机器人添加到群聊时查询和缓存组信息</span><span class="sxs-lookup"><span data-stu-id="6057f-108">Query and cache group information when the bot is added to a group chat</span></span>
* <span data-ttu-id="6057f-109">更新有关团队成员身份或频道信息的缓存信息</span><span class="sxs-lookup"><span data-stu-id="6057f-109">Update cached information on team membership or channel information</span></span>
* <span data-ttu-id="6057f-110">删除自动程序时删除团队的缓存信息</span><span class="sxs-lookup"><span data-stu-id="6057f-110">Remove cached information for a team if the bot is removed</span></span>
* <span data-ttu-id="6057f-111">用户喜欢自动程序消息时</span><span class="sxs-lookup"><span data-stu-id="6057f-111">When a bot message is liked by a user</span></span>

<span data-ttu-id="6057f-112">每个自动程序事件都作为 `Activity` 对象发送，其中 `messageType` 定义了对象中的信息。</span><span class="sxs-lookup"><span data-stu-id="6057f-112">Each bot event is sent as an `Activity` object in which `messageType` defines what information is in the object.</span></span> <span data-ttu-id="6057f-113">对于类型为 的邮件 `message` ，请参阅 [发送和接收邮件](~/resources/bot-v3/bot-conversations/bots-conversations.md)。</span><span class="sxs-lookup"><span data-stu-id="6057f-113">For messages of type `message`, see [Sending and receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span></span>

<span data-ttu-id="6057f-114">Teams和组事件（通常从类型触发）具有作为对象一部分传递的其他 Teams 事件信息，因此事件处理程序必须查询 Teams 的有效负载和其他特定于事件的元数据。 `conversationUpdate` `channelData` `channelData` `eventType`</span><span class="sxs-lookup"><span data-stu-id="6057f-114">Teams and group events, usually triggered off the `conversationUpdate` type, have additional Teams event information passed as part of the `channelData` object, and therefore your event handler must query the `channelData` payload for the Teams `eventType` and additional event-specific metadata.</span></span>

<span data-ttu-id="6057f-115">下表列出了机器人可以接收并采取措施的事件。</span><span class="sxs-lookup"><span data-stu-id="6057f-115">The following table lists the events that your bot can receive and take action on.</span></span>

|<span data-ttu-id="6057f-116">类型</span><span class="sxs-lookup"><span data-stu-id="6057f-116">Type</span></span>|<span data-ttu-id="6057f-117">Payload 对象</span><span class="sxs-lookup"><span data-stu-id="6057f-117">Payload object</span></span>|<span data-ttu-id="6057f-118">Teams eventType</span><span class="sxs-lookup"><span data-stu-id="6057f-118">Teams eventType</span></span> |<span data-ttu-id="6057f-119">说明</span><span class="sxs-lookup"><span data-stu-id="6057f-119">Description</span></span>|<span data-ttu-id="6057f-120">范围</span><span class="sxs-lookup"><span data-stu-id="6057f-120">Scope</span></span>|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[<span data-ttu-id="6057f-121">添加到团队的成员</span><span class="sxs-lookup"><span data-stu-id="6057f-121">Member added to team</span></span>](#team-member-or-bot-addition)| <span data-ttu-id="6057f-122">all</span><span class="sxs-lookup"><span data-stu-id="6057f-122">all</span></span> |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[<span data-ttu-id="6057f-123">已从团队中删除成员</span><span class="sxs-lookup"><span data-stu-id="6057f-123">Member was removed from team</span></span>](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [<span data-ttu-id="6057f-124">团队已重命名</span><span class="sxs-lookup"><span data-stu-id="6057f-124">Team was renamed</span></span>](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [<span data-ttu-id="6057f-125">已创建频道</span><span class="sxs-lookup"><span data-stu-id="6057f-125">A channel was created</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [<span data-ttu-id="6057f-126">频道已重命名</span><span class="sxs-lookup"><span data-stu-id="6057f-126">A channel was renamed</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [<span data-ttu-id="6057f-127">已删除频道</span><span class="sxs-lookup"><span data-stu-id="6057f-127">A channel was deleted</span></span>](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [<span data-ttu-id="6057f-128">对自动程序消息的反应</span><span class="sxs-lookup"><span data-stu-id="6057f-128">Reaction to bot message</span></span>](#reactions)| <span data-ttu-id="6057f-129">all</span><span class="sxs-lookup"><span data-stu-id="6057f-129">all</span></span> |
| `messageReaction` |`reactionsRemoved`|| [<span data-ttu-id="6057f-130">从自动程序消息中删除的反应</span><span class="sxs-lookup"><span data-stu-id="6057f-130">Reaction removed from bot message</span></span>](#reactions)| <span data-ttu-id="6057f-131">all</span><span class="sxs-lookup"><span data-stu-id="6057f-131">all</span></span> |

## <a name="team-member-or-bot-addition"></a><span data-ttu-id="6057f-132">添加团队成员或机器人</span><span class="sxs-lookup"><span data-stu-id="6057f-132">Team member or bot addition</span></span>

<span data-ttu-id="6057f-133">当机器人收到有关已添加它的团队的成员身份更新的信息时，该事件 [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) 将发送给机器人。</span><span class="sxs-lookup"><span data-stu-id="6057f-133">The [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate&preserve-view=true) event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="6057f-134">在首次专门为个人对话添加机器人时，机器人也会收到更新。</span><span class="sxs-lookup"><span data-stu-id="6057f-134">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span> <span data-ttu-id="6057f-135">请注意， () 信息对于自动程序来说是唯一的，可以缓存这些信息供你的服务 (如向特定用户发送 `Id`) 。</span><span class="sxs-lookup"><span data-stu-id="6057f-135">Note that the user information (`Id`) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

### <a name="bot-or-user-added-to-a-team"></a><span data-ttu-id="6057f-136">添加到团队的机器人或用户</span><span class="sxs-lookup"><span data-stu-id="6057f-136">Bot or user added to a team</span></span>

<span data-ttu-id="6057f-137">将机器人添加到团队或将新用户添加到已添加机器人的团队时，将发送有效负载中对象 `conversationUpdate` `membersAdded` 的事件。</span><span class="sxs-lookup"><span data-stu-id="6057f-137">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when either a bot is added to a team or a new user is added to a team where a bot has been added.</span></span> <span data-ttu-id="6057f-138">Microsoft Teams还添加到 `eventType.teamMemberAdded` `channelData` 对象中。</span><span class="sxs-lookup"><span data-stu-id="6057f-138">Microsoft Teams also adds `eventType.teamMemberAdded` in the `channelData` object.</span></span>

<span data-ttu-id="6057f-139">因为在这两种情况下都发送此事件，所以应分析对象以确定添加项是 `membersAdded` 用户还是自动程序本身。</span><span class="sxs-lookup"><span data-stu-id="6057f-139">Because this event is sent in both cases, you should parse the `membersAdded` object to determine whether the addition was a user or the bot itself.</span></span> <span data-ttu-id="6057f-140">对于后者，最佳做法是向频道发送欢迎消息，[](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams)以便用户可以了解机器人提供的功能。</span><span class="sxs-lookup"><span data-stu-id="6057f-140">For the latter, a best practice is to send a [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) to the channel so users can understand the features your bot provides.</span></span>

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a><span data-ttu-id="6057f-141">示例代码：检查机器人是否是已添加的成员</span><span class="sxs-lookup"><span data-stu-id="6057f-141">Example code: Checking whether bot was the added member</span></span>

##### <a name="net"></a><span data-ttu-id="6057f-142">.NET</span><span class="sxs-lookup"><span data-stu-id="6057f-142">.NET</span></span>

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

##### <a name="nodejs"></a><span data-ttu-id="6057f-143">Node.js</span><span class="sxs-lookup"><span data-stu-id="6057f-143">Node.js</span></span>

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

#### <a name="schema-example-bot-added-to-team"></a><span data-ttu-id="6057f-144">架构示例：添加到团队的自动程序</span><span class="sxs-lookup"><span data-stu-id="6057f-144">Schema example: Bot added to team</span></span>

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

### <a name="user-added-to-a-meeting"></a><span data-ttu-id="6057f-145">用户已添加到会议</span><span class="sxs-lookup"><span data-stu-id="6057f-145">User Added to a meeting</span></span>

<span data-ttu-id="6057f-146">将 `conversationUpdate` 用户添加到私人计划会议时，将发送有效负载中对象 `membersAdded` 的事件。</span><span class="sxs-lookup"><span data-stu-id="6057f-146">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when a user is added to a private scheduled meeting.</span></span> <span data-ttu-id="6057f-147">即使匿名用户加入会议，也会发送事件详细信息。</span><span class="sxs-lookup"><span data-stu-id="6057f-147">The event details will be sent even when anonymous users join the meeting.</span></span> 

> [!NOTE]
>
>* <span data-ttu-id="6057f-148">向会议添加匿名用户时，membersAdded 有效负载对象没有 `aadObjectId` 字段。</span><span class="sxs-lookup"><span data-stu-id="6057f-148">When an anonymous user is added to a meeting, membersAdded payload object does not have `aadObjectId` field.</span></span>
>* <span data-ttu-id="6057f-149">向会议添加匿名用户时，有效负载中的对象始终具有会议组织者的 ID，即使该匿名用户是由另一个演示者添加 `from` 的。</span><span class="sxs-lookup"><span data-stu-id="6057f-149">When an anonymous user is added to a meeting, `from` object in the payload always have the id of the meeting organizer, even if the anonymous user was added by another presenter.</span></span>

#### <a name="schema-example-user-added-to-meeting"></a><span data-ttu-id="6057f-150">架构示例：用户已添加到会议</span><span class="sxs-lookup"><span data-stu-id="6057f-150">Schema example: User added to meeting</span></span>

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

### <a name="bot-added-for-personal-context-only"></a><span data-ttu-id="6057f-151">仅针对个人上下文添加的自动程序</span><span class="sxs-lookup"><span data-stu-id="6057f-151">Bot added for personal context only</span></span>

<span data-ttu-id="6057f-152">当用户直接为个人聊天添加时，机器人 `conversationUpdate` `membersAdded` 会收到 with。</span><span class="sxs-lookup"><span data-stu-id="6057f-152">Your bot receives a `conversationUpdate` with `membersAdded` when a user adds it directly for personal chat.</span></span> <span data-ttu-id="6057f-153">在这种情况下，机器人收到的负载不包含 `channelData.team` 对象。</span><span class="sxs-lookup"><span data-stu-id="6057f-153">In this case, the payload that your bot receives doesn't contain the `channelData.team` object.</span></span> <span data-ttu-id="6057f-154">如果你希望机器人根据范围提供不同的欢迎消息，你应使用此筛选器。 [](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations)</span><span class="sxs-lookup"><span data-stu-id="6057f-154">You should use this as a filter in case you want your bot to offer a different [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) depending on scope.</span></span>

> [!NOTE]
> <span data-ttu-id="6057f-155">对于个人范围的自动程序，你的自动程序将接收事件多次，即使机器人 `conversationUpdate` 已删除并重新添加。</span><span class="sxs-lookup"><span data-stu-id="6057f-155">For personal scoped bots, your bot will  receive the `conversationUpdate` event multiple times, even if the bot is removed and re-added.</span></span> <span data-ttu-id="6057f-156">对于开发和测试，你可能会发现添加一个支持你完全重置机器人的帮助程序函数会很有用。</span><span class="sxs-lookup"><span data-stu-id="6057f-156">For development and testing you may find it useful to add a helper function that will allow you to reset your bot completely.</span></span> <span data-ttu-id="6057f-157">有关实现[Node.js的详细信息](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts)[，请参阅C#](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238)示例或示例。</span><span class="sxs-lookup"><span data-stu-id="6057f-157">See a [Node.js example](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) or [C# example](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) for more details on implementing this.</span></span>

#### <a name="schema-example-bot-added-to-personal-context"></a><span data-ttu-id="6057f-158">架构示例：添加到个人上下文的机器人</span><span class="sxs-lookup"><span data-stu-id="6057f-158">Schema example: bot added to personal context</span></span>

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

## <a name="team-member-or-bot-removed"></a><span data-ttu-id="6057f-159">已删除团队成员或机器人</span><span class="sxs-lookup"><span data-stu-id="6057f-159">Team member or bot removed</span></span>

<span data-ttu-id="6057f-160">从团队中删除机器人或将用户从添加自动程序的团队中删除时，将发送有效负载中对象 `conversationUpdate` `membersRemoved` 的事件。</span><span class="sxs-lookup"><span data-stu-id="6057f-160">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when either your bot is removed from a team, or a user is removed from a team where a bot has been added.</span></span> <span data-ttu-id="6057f-161">Microsoft Teams还添加到 `eventType.teamMemberRemoved` `channelData` 对象中。</span><span class="sxs-lookup"><span data-stu-id="6057f-161">Microsoft Teams also adds `eventType.teamMemberRemoved` in the `channelData` object.</span></span> <span data-ttu-id="6057f-162">与 对象一样，应分析机器人的应用 ID 对象 `membersAdded` `membersRemoved` 以确定已删除用户。</span><span class="sxs-lookup"><span data-stu-id="6057f-162">As with the `membersAdded` object, you should parse the `membersRemoved` object for your bot's App ID to determine who was removed.</span></span>

### <a name="schema-example-team-member-removed"></a><span data-ttu-id="6057f-163">架构示例：已删除团队成员</span><span class="sxs-lookup"><span data-stu-id="6057f-163">Schema example: Team member removed</span></span>

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

### <a name="user-removed-from-a-meeting"></a><span data-ttu-id="6057f-164">从会议中删除的用户</span><span class="sxs-lookup"><span data-stu-id="6057f-164">User removed from a meeting</span></span>

<span data-ttu-id="6057f-165">从 `conversationUpdate` 私人计划会议中删除用户时，将发送有效负载中对象 `membersRemoved` 的事件。</span><span class="sxs-lookup"><span data-stu-id="6057f-165">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when a user is removed from a private scheduled meeting.</span></span> <span data-ttu-id="6057f-166">即使匿名用户加入会议，也会发送事件详细信息。</span><span class="sxs-lookup"><span data-stu-id="6057f-166">The event details will be sent even when anonymous users join the meeting.</span></span> 

> [!NOTE]
>
>* <span data-ttu-id="6057f-167">从会议中删除匿名用户时，membersRemoved 有效负载对象没有 `aadObjectId` 字段。</span><span class="sxs-lookup"><span data-stu-id="6057f-167">When an anonymous user is removed from a meeting, membersRemoved payload object does not have `aadObjectId` field.</span></span>
>* <span data-ttu-id="6057f-168">从会议中删除匿名用户时，有效负载中的对象始终具有会议组织者的 ID，即使该匿名用户已被另一个 `from` 演示者删除。</span><span class="sxs-lookup"><span data-stu-id="6057f-168">When an anonymous user is removed from a meeting, `from` object in the payload always have the id of the meeting organizer, even if the anonymous user was removed by another presenter.</span></span>

#### <a name="schema-example-user-removed-from-meeting"></a><span data-ttu-id="6057f-169">架构示例：从会议中删除的用户</span><span class="sxs-lookup"><span data-stu-id="6057f-169">Schema example: User removed from meeting</span></span>

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

## <a name="team-name-updates"></a><span data-ttu-id="6057f-170">团队名称更新</span><span class="sxs-lookup"><span data-stu-id="6057f-170">Team name updates</span></span>

> [!NOTE]
> <span data-ttu-id="6057f-171">没有查询所有团队名称的功能，并且不会在其他事件的负载中返回团队名称。</span><span class="sxs-lookup"><span data-stu-id="6057f-171">There is no functionality to query all team names, and team name is not returned in payloads from other events.</span></span>

<span data-ttu-id="6057f-172">当自动程序位于的团队重命名时，将会收到通知。</span><span class="sxs-lookup"><span data-stu-id="6057f-172">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="6057f-173">它接收 `conversationUpdate` 对象中的 `eventType.teamRenamed` 事件 `channelData` 。</span><span class="sxs-lookup"><span data-stu-id="6057f-173">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span> <span data-ttu-id="6057f-174">请注意，没有有关团队创建或删除的通知，因为聊天机器人仅作为团队的一部分存在，在已添加它们的范围外没有可见性。</span><span class="sxs-lookup"><span data-stu-id="6057f-174">Please note that there are no notifications for team creation or deletion, because bots exist only as part of teams and have no visibility outside the scope in which they have been added.</span></span>

### <a name="schema-example-team-renamed"></a><span data-ttu-id="6057f-175">架构示例：团队重命名</span><span class="sxs-lookup"><span data-stu-id="6057f-175">Schema example: Team renamed</span></span>

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

## <a name="channel-updates"></a><span data-ttu-id="6057f-176">频道更新</span><span class="sxs-lookup"><span data-stu-id="6057f-176">Channel updates</span></span>

<span data-ttu-id="6057f-177">在已添加频道的团队中创建、重命名或删除频道时，将会通知机器人。</span><span class="sxs-lookup"><span data-stu-id="6057f-177">Your bot is notified when a channel is created, renamed, or deleted in a team where it has been added.</span></span> <span data-ttu-id="6057f-178">同样，将接收事件，并且Teams特定事件标识符作为对象的一部分发送，其中通道数据的 是通道 `conversationUpdate` `channelData.eventType` 的 GUID，并且包含通道 `channel.id` `channel.name` 名称本身。</span><span class="sxs-lookup"><span data-stu-id="6057f-178">Again, the `conversationUpdate` event is received, and a Teams-specific event identifier is sent as part of the `channelData.eventType` object, where the channel data's  `channel.id` is the GUID for the channel, and `channel.name` contains the channel name itself.</span></span>

<span data-ttu-id="6057f-179">频道事件如下所示：</span><span class="sxs-lookup"><span data-stu-id="6057f-179">The channel events are as follows:</span></span>

* <span data-ttu-id="6057f-180">**channelCreated** &emsp;用户向团队添加新频道</span><span class="sxs-lookup"><span data-stu-id="6057f-180">**channelCreated**&emsp;A user adds a new channel to the team</span></span>
* <span data-ttu-id="6057f-181">**channelRenamed** &emsp;用户重命名现有频道</span><span class="sxs-lookup"><span data-stu-id="6057f-181">**channelRenamed**&emsp;A user renames an existing channel</span></span>
* <span data-ttu-id="6057f-182">**channelDeleted** &emsp;用户删除频道</span><span class="sxs-lookup"><span data-stu-id="6057f-182">**channelDeleted**&emsp;A user removes a channel</span></span>

### <a name="full-schema-example-channelcreated"></a><span data-ttu-id="6057f-183">完整架构示例：channelCreated</span><span class="sxs-lookup"><span data-stu-id="6057f-183">Full schema example: channelCreated</span></span>

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a><span data-ttu-id="6057f-184">架构摘录：channelRenamed 的 channelData</span><span class="sxs-lookup"><span data-stu-id="6057f-184">Schema excerpt: channelData for channelRenamed</span></span>

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a><span data-ttu-id="6057f-185">架构摘录：channelDeleted 的 channelData</span><span class="sxs-lookup"><span data-stu-id="6057f-185">Schema excerpt: channelData for channelDeleted</span></span>

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

## <a name="reactions"></a><span data-ttu-id="6057f-186">反应</span><span class="sxs-lookup"><span data-stu-id="6057f-186">Reactions</span></span>

<span data-ttu-id="6057f-187">当用户向最初由机器人发送的消息添加或删除他/她的反应时， `messageReaction` 将发送该事件。</span><span class="sxs-lookup"><span data-stu-id="6057f-187">The `messageReaction` event is sent when a user adds or removes his or her reaction to a message which was originally sent by your bot.</span></span> <span data-ttu-id="6057f-188">`replyToId` 包含特定邮件的 ID。</span><span class="sxs-lookup"><span data-stu-id="6057f-188">`replyToId` contains the ID of the specific message.</span></span>

### <a name="schema-example-a-user-likes-a-message"></a><span data-ttu-id="6057f-189">架构示例：用户喜欢消息</span><span class="sxs-lookup"><span data-stu-id="6057f-189">Schema example: A user likes a message</span></span>

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

### <a name="schema-example-a-user-un-likes-a-message"></a><span data-ttu-id="6057f-190">架构示例：用户取消喜欢消息</span><span class="sxs-lookup"><span data-stu-id="6057f-190">Schema example: A user un-likes a message</span></span>

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
