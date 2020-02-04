---
title: 处理 bot 事件
description: 介绍如何处理 Microsoft 团队的 bot 中的事件
keywords: 团队 bot 事件
ms.date: 05/20/2019
ms.openlocfilehash: 06da5e6b0668e86012d87af3184493cdeb70aecd
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673298"
---
# <a name="handle-bot-events-in-microsoft-teams"></a><span data-ttu-id="ad297-104">在 Microsoft 团队中处理 bot 事件</span><span class="sxs-lookup"><span data-stu-id="ad297-104">Handle bot events in Microsoft Teams</span></span>

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

<span data-ttu-id="ad297-105">Microsoft 团队将通知发送到你的 bot，以获取在你的 bot 处于活动状态的范围内发生的更改或事件。</span><span class="sxs-lookup"><span data-stu-id="ad297-105">Microsoft Teams sends notifications to your bot for changes or events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="ad297-106">您可以使用这些事件来触发服务逻辑，如以下内容：</span><span class="sxs-lookup"><span data-stu-id="ad297-106">You can use these events to trigger service logic, such as the following:</span></span>

* <span data-ttu-id="ad297-107">在将你的 bot 添加到团队时触发欢迎消息</span><span class="sxs-lookup"><span data-stu-id="ad297-107">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="ad297-108">在将 bot 添加到组聊天时查询和缓存组信息</span><span class="sxs-lookup"><span data-stu-id="ad297-108">Query and cache group information when the bot is added to a group chat</span></span>
* <span data-ttu-id="ad297-109">更新有关团队成员资格或通道信息的缓存信息</span><span class="sxs-lookup"><span data-stu-id="ad297-109">Update cached information on team membership or channel information</span></span>
* <span data-ttu-id="ad297-110">删除团队的缓存信息（如果删除了 bot）</span><span class="sxs-lookup"><span data-stu-id="ad297-110">Remove cached information for a team if the bot is removed</span></span>
* <span data-ttu-id="ad297-111">当用户对 bot 邮件进行了赞时</span><span class="sxs-lookup"><span data-stu-id="ad297-111">When a bot message is liked by a user</span></span>

<span data-ttu-id="ad297-112">每个 bot 事件都以`Activity`对象的形式发送`messageType` ，其中定义了对象中的信息。</span><span class="sxs-lookup"><span data-stu-id="ad297-112">Each bot event is sent as an `Activity` object in which `messageType` defines what information is in the object.</span></span> <span data-ttu-id="ad297-113">有关类型`message`的邮件，请参阅[发送和接收邮件](~/resources/bot-v3/bot-conversations/bots-conversations.md)。</span><span class="sxs-lookup"><span data-stu-id="ad297-113">For messages of type `message`, see [Sending and receiving messages](~/resources/bot-v3/bot-conversations/bots-conversations.md).</span></span>

<span data-ttu-id="ad297-114">团队和组事件（通常`conversationUpdate`触发类型）具有作为`channelData`对象的一部分传递的其他团队事件信息，因此您的事件处理程序必须查询团队`channelData` `eventType`的有效负载和其他特定于事件的元数据。</span><span class="sxs-lookup"><span data-stu-id="ad297-114">Teams and group events, usually triggered off the `conversationUpdate` type, have additional Teams event information passed as part of the `channelData` object, and therefore your event handler must query the `channelData` payload for the Teams `eventType` and additional event-specific metadata.</span></span>

<span data-ttu-id="ad297-115">下表列出了你的 bot 可以接收并对其执行操作的事件。</span><span class="sxs-lookup"><span data-stu-id="ad297-115">The following table lists the events that your bot can receive and take action on.</span></span>

|<span data-ttu-id="ad297-116">类型</span><span class="sxs-lookup"><span data-stu-id="ad297-116">Type</span></span>|<span data-ttu-id="ad297-117">有效负载对象</span><span class="sxs-lookup"><span data-stu-id="ad297-117">Payload object</span></span>|<span data-ttu-id="ad297-118">团队事件 =</span><span class="sxs-lookup"><span data-stu-id="ad297-118">Teams eventType</span></span> |<span data-ttu-id="ad297-119">说明</span><span class="sxs-lookup"><span data-stu-id="ad297-119">Description</span></span>|<span data-ttu-id="ad297-120">范围</span><span class="sxs-lookup"><span data-stu-id="ad297-120">Scope</span></span>|
|---|---|---|---|---|
| `conversationUpdate` |`membersAdded`| `teamMemberAdded`|[<span data-ttu-id="ad297-121">添加到团队的成员</span><span class="sxs-lookup"><span data-stu-id="ad297-121">Member added to team</span></span>](#team-member-or-bot-addition)| <span data-ttu-id="ad297-122">各种</span><span class="sxs-lookup"><span data-stu-id="ad297-122">all</span></span> |
| `conversationUpdate` |`membersRemoved`| `teamMemberRemoved`|[<span data-ttu-id="ad297-123">成员已从团队中删除</span><span class="sxs-lookup"><span data-stu-id="ad297-123">Member was removed from team</span></span>](#team-member-or-bot-removed)| `groupChat` & `team` |
| `conversationUpdate` | |`teamRenamed`| [<span data-ttu-id="ad297-124">团队已重命名</span><span class="sxs-lookup"><span data-stu-id="ad297-124">Team was renamed</span></span>](#team-name-updates)| `team` |
| `conversationUpdate` | |`channelCreated`| [<span data-ttu-id="ad297-125">通道已创建</span><span class="sxs-lookup"><span data-stu-id="ad297-125">A channel was created</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelRenamed`| [<span data-ttu-id="ad297-126">频道已重命名</span><span class="sxs-lookup"><span data-stu-id="ad297-126">A channel was renamed</span></span>](#channel-updates)|`team` |
| `conversationUpdate` | |`channelDeleted`| [<span data-ttu-id="ad297-127">频道已删除</span><span class="sxs-lookup"><span data-stu-id="ad297-127">A channel was deleted</span></span>](#channel-updates)|`team` |
| `messageReaction` |`reactionsAdded`|| [<span data-ttu-id="ad297-128">对 bot 邮件的反应</span><span class="sxs-lookup"><span data-stu-id="ad297-128">Reaction to bot message</span></span>](#reactions)| <span data-ttu-id="ad297-129">各种</span><span class="sxs-lookup"><span data-stu-id="ad297-129">all</span></span> |
| `messageReaction` |`reactionsRemoved`|| [<span data-ttu-id="ad297-130">从 bot 邮件中删除的反应</span><span class="sxs-lookup"><span data-stu-id="ad297-130">Reaction removed from bot message</span></span>](#reactions)| <span data-ttu-id="ad297-131">各种</span><span class="sxs-lookup"><span data-stu-id="ad297-131">all</span></span> |

## <a name="team-member-or-bot-addition"></a><span data-ttu-id="ad297-132">团队成员或 bot 添加</span><span class="sxs-lookup"><span data-stu-id="ad297-132">Team member or bot addition</span></span>

<span data-ttu-id="ad297-133">当[`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate)该事件收到有关已添加的团队成员身份更新的信息时，该事件将发送到你的 bot。</span><span class="sxs-lookup"><span data-stu-id="ad297-133">The [`conversationUpdate`](/azure/bot-service/dotnet/bot-builder-dotnet-activities?view=azure-bot-service-3.0#conversationupdate) event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="ad297-134">它还会在首次专门为个人对话而添加时收到更新。</span><span class="sxs-lookup"><span data-stu-id="ad297-134">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span> <span data-ttu-id="ad297-135">请注意，用户信息（`Id`）对你的 bot 而言是唯一的，并且可以缓存以供你的服务将来使用（例如，向特定用户发送邮件）。</span><span class="sxs-lookup"><span data-stu-id="ad297-135">Note that the user information (`Id`) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

### <a name="bot-or-user-added-to-a-team"></a><span data-ttu-id="ad297-136">添加到团队的 Bot 或用户</span><span class="sxs-lookup"><span data-stu-id="ad297-136">Bot or user added to a team</span></span>

<span data-ttu-id="ad297-137">当`conversationUpdate`将 bot 添加`membersAdded`到团队或将新用户添加到添加了 bot 的团队中时，会发送具有有效负载中的对象的事件。</span><span class="sxs-lookup"><span data-stu-id="ad297-137">The `conversationUpdate` event with the `membersAdded` object in the payload is sent when either a bot is added to a team or a new user is added to a team where a bot has been added.</span></span> <span data-ttu-id="ad297-138">Microsoft 工作组也会`eventType.teamMemberAdded`添加到`channelData`对象中。</span><span class="sxs-lookup"><span data-stu-id="ad297-138">Microsoft Teams also adds `eventType.teamMemberAdded` in the `channelData` object.</span></span>

<span data-ttu-id="ad297-139">由于在这两种情况下都会发送此事件，因此`membersAdded`应分析该对象以确定添加是用户还是 bot 本身。</span><span class="sxs-lookup"><span data-stu-id="ad297-139">Because this event is sent in both cases, you should parse the `membersAdded` object to determine whether the addition was a user or the bot itself.</span></span> <span data-ttu-id="ad297-140">对于后者，最佳做法是将[欢迎消息](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams)发送到频道，以便用户能够理解你的 bot 提供的功能。</span><span class="sxs-lookup"><span data-stu-id="ad297-140">For the latter, a best practice is to send a [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-channel.md#best-practice-welcome-messages-in-teams) to the channel so users can understand the features your bot provides.</span></span>

#### <a name="example-code-checking-whether-bot-was-the-added-member"></a><span data-ttu-id="ad297-141">示例代码：检查 bot 是否为已添加的成员</span><span class="sxs-lookup"><span data-stu-id="ad297-141">Example code: Checking whether bot was the added member</span></span>

##### <a name="net"></a><span data-ttu-id="ad297-142">.NET</span><span class="sxs-lookup"><span data-stu-id="ad297-142">.NET</span></span>

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

##### <a name="nodejs"></a><span data-ttu-id="ad297-143">Node.js</span><span class="sxs-lookup"><span data-stu-id="ad297-143">Node.js</span></span>

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

#### <a name="schema-example-bot-added-to-team"></a><span data-ttu-id="ad297-144">架构示例：添加到团队的 Bot</span><span class="sxs-lookup"><span data-stu-id="ad297-144">Schema example: Bot added to team</span></span>

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

### <a name="bot-added-for-personal-context-only"></a><span data-ttu-id="ad297-145">仅为个人上下文添加的 Bot</span><span class="sxs-lookup"><span data-stu-id="ad297-145">Bot added for personal context only</span></span>

<span data-ttu-id="ad297-146">当用户直接添加`conversationUpdate`个人`membersAdded`聊天时，你的 bot 会收到。</span><span class="sxs-lookup"><span data-stu-id="ad297-146">Your bot receives a `conversationUpdate` with `membersAdded` when a user adds it directly for personal chat.</span></span> <span data-ttu-id="ad297-147">在这种情况下，你的 bot 接收的有效负载`channelData.team`不包含该对象。</span><span class="sxs-lookup"><span data-stu-id="ad297-147">In this case, the payload that your bot receives doesn't contain the `channelData.team` object.</span></span> <span data-ttu-id="ad297-148">如果您希望您的 bot 根据范围提供不同的[欢迎消息](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations)，则应将此作为筛选器使用。</span><span class="sxs-lookup"><span data-stu-id="ad297-148">You should use this as a filter in case you want your bot to offer a different [welcome message](~/resources/bot-v3/bot-conversations/bots-conv-personal.md#best-practice-welcome-messages-in-personal-conversations) depending on scope.</span></span>

> [!NOTE]
> <span data-ttu-id="ad297-149">对于个人范围内的 bot，你的 bot 只会`conversationUpdate`在一次时间内收到该事件，即使已删除并重新添加了 bot 也是如此。</span><span class="sxs-lookup"><span data-stu-id="ad297-149">For personal scoped bots, your bot will only ever receive the `conversationUpdate` event a single time, even if the bot is removed and re-added.</span></span> <span data-ttu-id="ad297-150">对于开发和测试，您可能会发现，添加帮助程序函数将允许您完全重置你的 bot。</span><span class="sxs-lookup"><span data-stu-id="ad297-150">For development and testing you may find it useful to add a helper function that will allow you to reset your bot completely.</span></span> <span data-ttu-id="ad297-151">有关实现这一点的更多详细信息，请参阅[node.js 示例](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts)或[c # 示例](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238)。</span><span class="sxs-lookup"><span data-stu-id="ad297-151">See a [Node.js example](https://github.com/OfficeDev/microsoft-teams-sample-complete-node/blob/master/src/middleware/SimulateResetBotChat.ts) or [C# example](https://github.com/OfficeDev/microsoft-teams-sample-complete-csharp/blob/master/template-bot-master-csharp/src/controllers/MessagesController.cs#L238) for more details on implementing this.</span></span>

#### <a name="schema-example-bot-added-to-personal-context"></a><span data-ttu-id="ad297-152">架构示例：添加到个人上下文的 bot</span><span class="sxs-lookup"><span data-stu-id="ad297-152">Schema example: bot added to personal context</span></span>

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

## <a name="team-member-or-bot-removed"></a><span data-ttu-id="ad297-153">删除了团队成员或 bot</span><span class="sxs-lookup"><span data-stu-id="ad297-153">Team member or bot removed</span></span>

<span data-ttu-id="ad297-154">当`conversationUpdate`您的 bot `membersRemoved`从团队中删除时，将会发送事件和有效负载中的对象，或者从已添加 bot 的团队中删除用户。</span><span class="sxs-lookup"><span data-stu-id="ad297-154">The `conversationUpdate` event with the `membersRemoved` object in the payload is sent when either your bot is removed from a team, or a user is removed from a team where a bot has been added.</span></span> <span data-ttu-id="ad297-155">Microsoft 工作组也会`eventType.teamMemberRemoved`添加到`channelData`对象中。</span><span class="sxs-lookup"><span data-stu-id="ad297-155">Microsoft Teams also adds `eventType.teamMemberRemoved` in the `channelData` object.</span></span> <span data-ttu-id="ad297-156">与`membersAdded`对象一样，您应该为你的`membersRemoved` bot 的应用 ID 解析对象以确定已删除的用户。</span><span class="sxs-lookup"><span data-stu-id="ad297-156">As with the `membersAdded` object, you should parse the `membersRemoved` object for your bot's App ID to determine who was removed.</span></span>

### <a name="schema-example-team-member-removed"></a><span data-ttu-id="ad297-157">架构示例：删除了工作组成员</span><span class="sxs-lookup"><span data-stu-id="ad297-157">Schema example: Team member removed</span></span>

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

## <a name="team-name-updates"></a><span data-ttu-id="ad297-158">团队名称更新</span><span class="sxs-lookup"><span data-stu-id="ad297-158">Team name updates</span></span>

> [!NOTE]
> <span data-ttu-id="ad297-159">没有用于查询所有团队名称的功能，且未从其他事件的有效负载中返回团队名称。</span><span class="sxs-lookup"><span data-stu-id="ad297-159">There is no functionality to query all team names, and team name is not returned in payloads from other events.</span></span>

<span data-ttu-id="ad297-160">重命名你的 bot 时，会通知你的你的团队。</span><span class="sxs-lookup"><span data-stu-id="ad297-160">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="ad297-161">它接收`channelData`对象`conversationUpdate` `eventType.teamRenamed`中的事件。</span><span class="sxs-lookup"><span data-stu-id="ad297-161">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span> <span data-ttu-id="ad297-162">请注意，没有针对团队创建或删除的通知，因为 bot 仅作为团队的一部分存在，并且在添加它们的范围之外不可见。</span><span class="sxs-lookup"><span data-stu-id="ad297-162">Please note that there are no notifications for team creation or deletion, because bots exist only as part of teams and have no visibility outside the scope in which they have been added.</span></span>

### <a name="schema-example-team-renamed"></a><span data-ttu-id="ad297-163">架构示例：团队已重命名</span><span class="sxs-lookup"><span data-stu-id="ad297-163">Schema example: Team renamed</span></span>

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

## <a name="channel-updates"></a><span data-ttu-id="ad297-164">频道更新</span><span class="sxs-lookup"><span data-stu-id="ad297-164">Channel updates</span></span>

<span data-ttu-id="ad297-165">在已添加频道的团队中创建、重命名或删除频道时，将会通知你的 bot。</span><span class="sxs-lookup"><span data-stu-id="ad297-165">Your bot is notified when a channel is created, renamed, or deleted in a team where it has been added.</span></span> <span data-ttu-id="ad297-166">此外，还`conversationUpdate`会收到该事件，并将特定于团队的事件标识符作为该`channelData.eventType`对象的一部分发送，其中通道数据`channel.id`是通道的 GUID，并且`channel.name`包含通道名称本身。</span><span class="sxs-lookup"><span data-stu-id="ad297-166">Again, the `conversationUpdate` event is received, and a Teams-specific event identifier is sent as part of the `channelData.eventType` object, where the channel data's  `channel.id` is the GUID for the channel, and `channel.name` contains the channel name itself.</span></span>

<span data-ttu-id="ad297-167">通道事件如下所示：</span><span class="sxs-lookup"><span data-stu-id="ad297-167">The channel events are as follows:</span></span>

* <span data-ttu-id="ad297-168">**channelCreated**&emsp;用户向团队添加新频道</span><span class="sxs-lookup"><span data-stu-id="ad297-168">**channelCreated**&emsp;A user adds a new channel to the team</span></span>
* <span data-ttu-id="ad297-169">**channelRenamed**&emsp;用户重命名现有频道</span><span class="sxs-lookup"><span data-stu-id="ad297-169">**channelRenamed**&emsp;A user renames an existing channel</span></span>
* <span data-ttu-id="ad297-170">**channelDeleted**&emsp;用户删除频道</span><span class="sxs-lookup"><span data-stu-id="ad297-170">**channelDeleted**&emsp;A user removes a channel</span></span>

### <a name="full-schema-example-channelcreated"></a><span data-ttu-id="ad297-171">完整架构示例： channelCreated</span><span class="sxs-lookup"><span data-stu-id="ad297-171">Full schema example: channelCreated</span></span>

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

### <a name="schema-excerpt-channeldata-for-channelrenamed"></a><span data-ttu-id="ad297-172">架构摘录： channelData for channelRenamed</span><span class="sxs-lookup"><span data-stu-id="ad297-172">Schema excerpt: channelData for channelRenamed</span></span>

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

### <a name="schema-excerpt-channeldata-for-channeldeleted"></a><span data-ttu-id="ad297-173">架构摘录： channelData for channelDeleted</span><span class="sxs-lookup"><span data-stu-id="ad297-173">Schema excerpt: channelData for channelDeleted</span></span>

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

## <a name="reactions"></a><span data-ttu-id="ad297-174">作出</span><span class="sxs-lookup"><span data-stu-id="ad297-174">Reactions</span></span>

<span data-ttu-id="ad297-175">当`messageReaction`用户在最初由你的 bot 发送的邮件中添加或删除他/她的反应时，会发送此事件。</span><span class="sxs-lookup"><span data-stu-id="ad297-175">The `messageReaction` event is sent when a user adds or removes his or her reaction to a message which was originally sent by your bot.</span></span> <span data-ttu-id="ad297-176">`replyToId`包含特定邮件的 ID。</span><span class="sxs-lookup"><span data-stu-id="ad297-176">`replyToId` contains the ID of the specific message.</span></span>

### <a name="schema-example-a-user-likes-a-message"></a><span data-ttu-id="ad297-177">架构示例：用户喜欢一封邮件</span><span class="sxs-lookup"><span data-stu-id="ad297-177">Schema example: A user likes a message</span></span>

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

### <a name="schema-example-a-user-un-likes-a-message"></a><span data-ttu-id="ad297-178">架构示例：用户不喜欢某封邮件</span><span class="sxs-lookup"><span data-stu-id="ad297-178">Schema example: A user un-likes a message</span></span>

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
