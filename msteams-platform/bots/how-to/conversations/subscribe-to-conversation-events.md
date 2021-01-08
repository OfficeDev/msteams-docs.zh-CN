---
title: 订阅对话事件
author: WashingtonKayaker
description: 如何从 Microsoft Teams 机器人订阅对话事件。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: f0da861834bbf221fe715d35c0beea6c3bd08f26
ms.sourcegitcommit: 5f1d6c12d80d48f403b73586f68bacf15785c855
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/30/2020
ms.locfileid: "49739033"
---
# <a name="subscribe-to-conversation-events"></a><span data-ttu-id="8ea5c-103">订阅对话事件</span><span class="sxs-lookup"><span data-stu-id="8ea5c-103">Subscribe to conversation events</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="8ea5c-104">Microsoft Teams 会向自动程序发送有关在自动程序处于活动状态的范围内发生的事件的通知。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-104">Microsoft Teams sends notifications to your bot for events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="8ea5c-105">可以在代码中捕获这些事件，并针对它们采取措施，例如：</span><span class="sxs-lookup"><span data-stu-id="8ea5c-105">You can capture these events in your code and take action on them, such as the following:</span></span>

* <span data-ttu-id="8ea5c-106">将机器人添加到团队时触发欢迎消息</span><span class="sxs-lookup"><span data-stu-id="8ea5c-106">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="8ea5c-107">添加或删除新团队成员时触发欢迎消息</span><span class="sxs-lookup"><span data-stu-id="8ea5c-107">Trigger a welcome message when a new team member is added or removed</span></span>
* <span data-ttu-id="8ea5c-108">创建、重命名或删除频道时触发通知</span><span class="sxs-lookup"><span data-stu-id="8ea5c-108">Trigger a notification when a channel is created, renamed or deleted</span></span>
* <span data-ttu-id="8ea5c-109">当用户喜欢自动程序消息时</span><span class="sxs-lookup"><span data-stu-id="8ea5c-109">When a bot message is liked by a user</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="8ea5c-110">对话更新事件</span><span class="sxs-lookup"><span data-stu-id="8ea5c-110">Conversation update events</span></span>

> [!Important]
> <span data-ttu-id="8ea5c-111">可以随时添加新事件，机器人将开始接收它们。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-111">New events can be added at any time, and your bot will begin to receive them.</span></span>
> <span data-ttu-id="8ea5c-112">您必须针对接收意外事件的可能性进行设计。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-112">You must design for the possibility of receiving unexpected events.</span></span>
> <span data-ttu-id="8ea5c-113">如果你使用的是 Bot Framework SDK，则自动程序将自动响应你未选择 `200 - OK` 处理的任何事件。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-113">If you are using the Bot Framework SDK, your bot will automatically respond with a `200 - OK` to any events you do not choose to handle.</span></span>

<span data-ttu-id="8ea5c-114">自动程序在将事件添加到对话、将其他成员添加到对话或从对话中删除，或者对话元数据已更改时接收 `conversationUpdate` 事件。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-114">A bot receives a `conversationUpdate` event when it has been added to a conversation, other members have been added to or removed from a conversation, or conversation metadata has changed.</span></span>

<span data-ttu-id="8ea5c-115">当机器人收到有关已添加它的团队的成员身份更新的信息时，该事件 `conversationUpdate` 会发送到机器人。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-115">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="8ea5c-116">当首次专门为个人对话添加更新时，它还会收到更新。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-116">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span>

<span data-ttu-id="8ea5c-117">下表显示了 Teams 对话更新事件的列表，以及指向更多详细信息的链接。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-117">The following table shows a list of Teams conversation update events, with links to more details.</span></span>

| <span data-ttu-id="8ea5c-118">已采取的操作</span><span class="sxs-lookup"><span data-stu-id="8ea5c-118">Action Taken</span></span>        | <span data-ttu-id="8ea5c-119">EventType</span><span class="sxs-lookup"><span data-stu-id="8ea5c-119">EventType</span></span>         | <span data-ttu-id="8ea5c-120">调用的方法</span><span class="sxs-lookup"><span data-stu-id="8ea5c-120">Method Called</span></span>              | <span data-ttu-id="8ea5c-121">说明</span><span class="sxs-lookup"><span data-stu-id="8ea5c-121">Description</span></span>                | <span data-ttu-id="8ea5c-122">范围</span><span class="sxs-lookup"><span data-stu-id="8ea5c-122">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="8ea5c-123">创建通道</span><span class="sxs-lookup"><span data-stu-id="8ea5c-123">channel created</span></span>     | <span data-ttu-id="8ea5c-124">channelCreated</span><span class="sxs-lookup"><span data-stu-id="8ea5c-124">channelCreated</span></span>    | <span data-ttu-id="8ea5c-125">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="8ea5c-125">OnTeamsChannelCreatedAsync</span></span> | [<span data-ttu-id="8ea5c-126">已创建频道</span><span class="sxs-lookup"><span data-stu-id="8ea5c-126">A channel was created</span></span>](#channel-created) | <span data-ttu-id="8ea5c-127">团队</span><span class="sxs-lookup"><span data-stu-id="8ea5c-127">Team</span></span> |
| <span data-ttu-id="8ea5c-128">通道重命名</span><span class="sxs-lookup"><span data-stu-id="8ea5c-128">channel renamed</span></span>     | <span data-ttu-id="8ea5c-129">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="8ea5c-129">channelRenamed</span></span>    | <span data-ttu-id="8ea5c-130">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="8ea5c-130">OnTeamsChannelRenamedAsync</span></span> | [<span data-ttu-id="8ea5c-131">频道已重命名</span><span class="sxs-lookup"><span data-stu-id="8ea5c-131">A channel was renamed</span></span>](#channel-renamed) | <span data-ttu-id="8ea5c-132">团队</span><span class="sxs-lookup"><span data-stu-id="8ea5c-132">Team</span></span> |
| <span data-ttu-id="8ea5c-133">频道已删除</span><span class="sxs-lookup"><span data-stu-id="8ea5c-133">channel deleted</span></span>     | <span data-ttu-id="8ea5c-134">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="8ea5c-134">channelDeleted</span></span>    | <span data-ttu-id="8ea5c-135">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="8ea5c-135">OnTeamsChannelDeletedAsync</span></span> | [<span data-ttu-id="8ea5c-136">频道已删除</span><span class="sxs-lookup"><span data-stu-id="8ea5c-136">A channel was deleted</span></span>](#channel-deleted) | <span data-ttu-id="8ea5c-137">团队</span><span class="sxs-lookup"><span data-stu-id="8ea5c-137">Team</span></span> |
| <span data-ttu-id="8ea5c-138">通道已还原</span><span class="sxs-lookup"><span data-stu-id="8ea5c-138">channel restored</span></span>    | <span data-ttu-id="8ea5c-139">channelRestored</span><span class="sxs-lookup"><span data-stu-id="8ea5c-139">channelRestored</span></span>    | <span data-ttu-id="8ea5c-140">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="8ea5c-140">OnTeamsChannelRestoredAsync</span></span> | [<span data-ttu-id="8ea5c-141">已还原频道</span><span class="sxs-lookup"><span data-stu-id="8ea5c-141">A channel was restored</span></span>](#channel-deleted) | <span data-ttu-id="8ea5c-142">团队</span><span class="sxs-lookup"><span data-stu-id="8ea5c-142">Team</span></span> |
| <span data-ttu-id="8ea5c-143">members added</span><span class="sxs-lookup"><span data-stu-id="8ea5c-143">members added</span></span>   | <span data-ttu-id="8ea5c-144">membersAdded</span><span class="sxs-lookup"><span data-stu-id="8ea5c-144">membersAdded</span></span>   | <span data-ttu-id="8ea5c-145">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="8ea5c-145">OnTeamsMembersAddedAsync</span></span>   | [<span data-ttu-id="8ea5c-146">已添加成员</span><span class="sxs-lookup"><span data-stu-id="8ea5c-146">A member added</span></span>](#team-members-added)   | <span data-ttu-id="8ea5c-147">全部</span><span class="sxs-lookup"><span data-stu-id="8ea5c-147">All</span></span> |
| <span data-ttu-id="8ea5c-148">成员已删除</span><span class="sxs-lookup"><span data-stu-id="8ea5c-148">members removed</span></span> | <span data-ttu-id="8ea5c-149">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="8ea5c-149">membersRemoved</span></span> | <span data-ttu-id="8ea5c-150">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="8ea5c-150">OnTeamsMembersRemovedAsync</span></span> | [<span data-ttu-id="8ea5c-151">已删除成员</span><span class="sxs-lookup"><span data-stu-id="8ea5c-151">A member was removed</span></span>](#team-members-removed) | <span data-ttu-id="8ea5c-152">groupChat & team</span><span class="sxs-lookup"><span data-stu-id="8ea5c-152">groupChat & team</span></span> |
| <span data-ttu-id="8ea5c-153">团队重命名</span><span class="sxs-lookup"><span data-stu-id="8ea5c-153">team renamed</span></span>        | <span data-ttu-id="8ea5c-154">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="8ea5c-154">teamRenamed</span></span>       | <span data-ttu-id="8ea5c-155">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="8ea5c-155">OnTeamsTeamRenamedAsync</span></span>    | [<span data-ttu-id="8ea5c-156">已重命名团队</span><span class="sxs-lookup"><span data-stu-id="8ea5c-156">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="8ea5c-157">团队</span><span class="sxs-lookup"><span data-stu-id="8ea5c-157">Team</span></span> |
| <span data-ttu-id="8ea5c-158">团队存档</span><span class="sxs-lookup"><span data-stu-id="8ea5c-158">team archived</span></span>        | <span data-ttu-id="8ea5c-159">teamArchived</span><span class="sxs-lookup"><span data-stu-id="8ea5c-159">teamArchived</span></span>       | <span data-ttu-id="8ea5c-160">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="8ea5c-160">OnTeamsTeamArchivedAsync</span></span>    | [<span data-ttu-id="8ea5c-161">团队已存档</span><span class="sxs-lookup"><span data-stu-id="8ea5c-161">A Team was archived</span></span>](#team-archived)       | <span data-ttu-id="8ea5c-162">团队</span><span class="sxs-lookup"><span data-stu-id="8ea5c-162">Team</span></span> |
| <span data-ttu-id="8ea5c-163">团队已还原</span><span class="sxs-lookup"><span data-stu-id="8ea5c-163">team restored</span></span>        | <span data-ttu-id="8ea5c-164">teamRestored</span><span class="sxs-lookup"><span data-stu-id="8ea5c-164">teamRestored</span></span>      | <span data-ttu-id="8ea5c-165">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="8ea5c-165">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="8ea5c-166">已重命名团队</span><span class="sxs-lookup"><span data-stu-id="8ea5c-166">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="8ea5c-167">团队</span><span class="sxs-lookup"><span data-stu-id="8ea5c-167">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="8ea5c-168">已创建频道</span><span class="sxs-lookup"><span data-stu-id="8ea5c-168">Channel created</span></span>

<span data-ttu-id="8ea5c-169">只要在安装自动程序的团队中创建了新频道，就会将频道创建事件发送给机器人。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-169">The channel created event is sent to your bot whenever a new channel is created in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8ea5c-170">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8ea5c-170">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8ea5c-171">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8ea5c-171">TypeScript/Node.js</span></span>](#tab/typescript)

<!-- From sample: botbuilder-js\libraries\botbuilder\tests\teams\conversationUpdate\src\conversationUpdateBot.ts -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelCreatedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Created', `${channelInfo.name} is the Channel created`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="8ea5c-172">JSON</span><span class="sxs-lookup"><span data-stu-id="8ea5c-172">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="8ea5c-173">Python</span><span class="sxs-lookup"><span data-stu-id="8ea5c-173">Python</span></span>](#tab/python)

```python
async def on_teams_channel_created(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(
            f"The new channel is {channel_info.name}. The channel id is {channel_info.id}"
        )
    )
```

* * *

### <a name="channel-renamed"></a><span data-ttu-id="8ea5c-174">已重命名频道</span><span class="sxs-lookup"><span data-stu-id="8ea5c-174">Channel renamed</span></span>

<span data-ttu-id="8ea5c-175">只要在安装了自动程序的团队中重命名频道，频道重命名事件就会发送到机器人。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-175">The channel renamed event is sent to your bot whenever a channel is renamed in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8ea5c-176">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8ea5c-176">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8ea5c-177">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8ea5c-177">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelRenamedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Renamed', `${channelInfo.name} is the new Channel name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
```

# <a name="json"></a>[<span data-ttu-id="8ea5c-178">JSON</span><span class="sxs-lookup"><span data-stu-id="8ea5c-178">JSON</span></span>](#tab/json)

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
}
```

# <a name="python"></a>[<span data-ttu-id="8ea5c-179">Python</span><span class="sxs-lookup"><span data-stu-id="8ea5c-179">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="8ea5c-180">频道已删除</span><span class="sxs-lookup"><span data-stu-id="8ea5c-180">Channel Deleted</span></span>

<span data-ttu-id="8ea5c-181">只要在安装了自动程序的团队中删除频道，频道删除事件就会发送到机器人。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-181">The channel deleted event is sent to your bot whenever a channel is deleted in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8ea5c-182">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8ea5c-182">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8ea5c-183">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8ea5c-183">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelDeletedEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Deleted', `${channelInfo.name} is the Channel deleted`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="8ea5c-184">JSON</span><span class="sxs-lookup"><span data-stu-id="8ea5c-184">JSON</span></span>](#tab/json)

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
}
```

# <a name="python"></a>[<span data-ttu-id="8ea5c-185">Python</span><span class="sxs-lookup"><span data-stu-id="8ea5c-185">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="channel-restored"></a><span data-ttu-id="8ea5c-186">已还原频道</span><span class="sxs-lookup"><span data-stu-id="8ea5c-186">Channel restored</span></span>

<span data-ttu-id="8ea5c-187">只要在已安装自动程序的团队中还原以前删除的频道，就会将频道还原事件发送给自动程序。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-187">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team that your bot is already installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8ea5c-188">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8ea5c-188">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8ea5c-189">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8ea5c-189">TypeScript/Node.js</span></span>](#tab/typescript)

<!-- From sample: botbuilder-js\libraries\botbuilder\tests\teams\conversationUpdate\src\conversationUpdateBot.ts -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsChannelRestoredEvent(async (channelInfo: ChannelInfo, teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Channel Restored', `${channelInfo.name} is the Channel restored`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="8ea5c-190">JSON</span><span class="sxs-lookup"><span data-stu-id="8ea5c-190">JSON</span></span>](#tab/json)

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
        "eventType": "channelRestored",
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="8ea5c-191">Python</span><span class="sxs-lookup"><span data-stu-id="8ea5c-191">Python</span></span>](#tab/python)

```python
async def on_teams_channel_restored(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(
            f"The restored channel is {channel_info.name}. The channel id is {channel_info.id}"
        )
    )
```

* * *

### <a name="team-members-added"></a><span data-ttu-id="8ea5c-192">已添加团队成员</span><span class="sxs-lookup"><span data-stu-id="8ea5c-192">Team members added</span></span>

<span data-ttu-id="8ea5c-193">该事件在首次添加到对话时以及每次向安装自动程序的团队或群聊中添加新用户时 `teamMemberAdded` 发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-193">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation and every time a new user is added to a team or group chat that your bot is installed in.</span></span> <span data-ttu-id="8ea5c-194">自动 (ID) 信息是唯一的，可以缓存这些信息供你的服务 (例如向特定用户发送) 。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-194">The user information (ID) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8ea5c-195">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8ea5c-195">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersAddedAsync(IList<TeamsChannelAccount> teamsMembersAdded , TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in teamsMembersAdded)
    {
        if (member.Id == turnContext.Activity.Recipient.Id)
        {
            // Send a message to introduce the bot to the team
            var heroCard = new HeroCard(text: $"The {member.Name} bot has joined {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
        else
        {
            var heroCard = new HeroCard(text: $"{member.Name} joined {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8ea5c-196">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8ea5c-196">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsMembersAddedEvent(async (membersAdded: ChannelAccount[], teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
                let newMembers: string = '';
                console.log(JSON.stringify(membersAdded));
                membersAdded.forEach((account) => {
                    newMembers += account.id + ' ';
                });
                const name = !teamInfo ? 'not in team' : teamInfo.name;
                const card = CardFactory.heroCard('Account Added', `${newMembers} joined ${name}.`);
                const message = MessageFactory.attachment(card);
                await turnContext.sendActivity(message);
                await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="8ea5c-197">JSON</span><span class="sxs-lookup"><span data-stu-id="8ea5c-197">JSON</span></span>](#tab/json)

<span data-ttu-id="8ea5c-198">这是自动程序添加到团队时，机器人将收到 **的消息**。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-198">This is the message your bot will receive when the bot is added **to a team**.</span></span>

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

<span data-ttu-id="8ea5c-199">这是自动程序将\* 添加到一对一聊天时机器人 *将接收的消息*。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-199">This is the message your bot will receive when the bot is added \**to a one-to-one chat*.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="8ea5c-200">Python</span><span class="sxs-lookup"><span data-stu-id="8ea5c-200">Python</span></span>](#tab/python)

```python
async def on_teams_members_added(
    self, teams_members_added: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(
            MessageFactory.text(f"Welcome your new team member {member.id}")
        )
    return
```

<span data-ttu-id="8ea5c-201">_ \* \*</span><span class="sxs-lookup"><span data-stu-id="8ea5c-201">_ \* \*</span></span>

### <a name="team-members-removed"></a><span data-ttu-id="8ea5c-202">已删除团队成员</span><span class="sxs-lookup"><span data-stu-id="8ea5c-202">Team members removed</span></span>

<span data-ttu-id="8ea5c-203">如果从团队中删除了事件，并且每次从自动程序成员团队中删除任何用户，该事件都会 `teamMemberRemoved` 发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-203">The `teamMemberRemoved` event is sent to your bot if it is removed from a team and every time any user is removed from a team that your bot is a member of.</span></span> <span data-ttu-id="8ea5c-204">通过查看对象，可以确定删除的新增成员是机器人本身还是 `Activity` 用户 `turnContext` 。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-204">You can determine if the new member removed was the bot itself or a user by looking at the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="8ea5c-205">如果对象的字段与对象的字段相同，则删除的成员为自动程序， `Id` `MembersRemoved` 否则为 `Id` `Recipient` 用户。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-205">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, otherwise, it is a user.</span></span>  <span data-ttu-id="8ea5c-206">自动程序 `Id` 通常为： `28:<MicrosoftAppId>`</span><span class="sxs-lookup"><span data-stu-id="8ea5c-206">The bot's `Id` will generally be: `28:<MicrosoftAppId>`</span></span>

[!Note] <span data-ttu-id="8ea5c-207">从租户中永久删除用户时， `membersRemoved conversationUpdate` 将触发事件。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-207">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8ea5c-208">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8ea5c-208">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersRemovedAsync(IList<ChannelAccount> membersRemoved, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in membersRemoved)
    {
        if (member.Id == turnContext.Activity.Recipient.Id)
        {
            // The bot was removed
            // You should clear any cached data you have for this team
        }
        else
        {
            var heroCard = new HeroCard(text: $"{member.Name} was removed from {teamInfo.Name}");
            await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
        }
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8ea5c-209">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8ea5c-209">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsMembersRemovedEvent(async (membersRemoved: ChannelAccount[], teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            let removedMembers: string = '';
            console.log(JSON.stringify(membersRemoved));
            membersRemoved.forEach((account) => {
                removedMembers += account.id + ' ';
            });
            const name = !teamInfo ? 'not in team' : teamInfo.name;
            const card = CardFactory.heroCard('Account Removed', `${removedMembers} removed from ${teamInfo.name}.`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="8ea5c-210">JSON</span><span class="sxs-lookup"><span data-stu-id="8ea5c-210">JSON</span></span>](#tab/json)

<span data-ttu-id="8ea5c-211">以下有效负载示例中的对象基于向团队（而不是群聊）添加成员，或启动新的一对 `channelData` 一对话：</span><span class="sxs-lookup"><span data-stu-id="8ea5c-211">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="8ea5c-212">Python</span><span class="sxs-lookup"><span data-stu-id="8ea5c-212">Python</span></span>](#tab/python)

```python
async def on_teams_members_removed(
    self, teams_members_removed: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_removed:
        await turn_context.send_activity(
            MessageFactory.text(f"Say goodbye to {member.id}")
        )
    return
```

* * *

### <a name="team-renamed"></a><span data-ttu-id="8ea5c-213">团队重命名</span><span class="sxs-lookup"><span data-stu-id="8ea5c-213">Team renamed</span></span>

<span data-ttu-id="8ea5c-214">自动程序在已重命名其团队时收到通知。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-214">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="8ea5c-215">它接收 `conversationUpdate` 对象 `eventType.teamRenamed` 中的 `channelData` 事件。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-215">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8ea5c-216">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8ea5c-216">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8ea5c-217">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8ea5c-217">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamRenamedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team Renamed', `${teamInfo.name} is the new Team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="8ea5c-218">JSON</span><span class="sxs-lookup"><span data-stu-id="8ea5c-218">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="8ea5c-219">Python</span><span class="sxs-lookup"><span data-stu-id="8ea5c-219">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

### <a name="team-archived"></a><span data-ttu-id="8ea5c-220">团队存档</span><span class="sxs-lookup"><span data-stu-id="8ea5c-220">Team archived</span></span>

<span data-ttu-id="8ea5c-221">自动程序在存档安装它的团队时收到通知。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-221">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="8ea5c-222">它接收 `conversationUpdate` 对象 `eventType.teamarchived` 中的 `channelData` 事件。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-222">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8ea5c-223">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8ea5c-223">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8ea5c-224">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8ea5c-224">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamArchivedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team archived', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="8ea5c-225">JSON</span><span class="sxs-lookup"><span data-stu-id="8ea5c-225">JSON</span></span>](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamArchived",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="8ea5c-226">Python</span><span class="sxs-lookup"><span data-stu-id="8ea5c-226">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

### <a name="team-restored"></a><span data-ttu-id="8ea5c-227">团队已还原</span><span class="sxs-lookup"><span data-stu-id="8ea5c-227">Team restored</span></span>

<span data-ttu-id="8ea5c-228">自动程序在安装它的团队还原时收到通知。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-228">The bot receives a notification when the team it is installed in is restored.</span></span> <span data-ttu-id="8ea5c-229">它接收 `conversationUpdate` 对象 `eventType.teamrestored` 中的 `channelData` 事件。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-229">It receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8ea5c-230">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8ea5c-230">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8ea5c-231">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8ea5c-231">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamrestoredEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team restored', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="8ea5c-232">JSON</span><span class="sxs-lookup"><span data-stu-id="8ea5c-232">JSON</span></span>](#tab/json)

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
            "name": "Team Name"
        },
        "eventType": "teamrestored",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="8ea5c-233">Python</span><span class="sxs-lookup"><span data-stu-id="8ea5c-233">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

## <a name="message-reaction-events"></a><span data-ttu-id="8ea5c-234">消息反应事件</span><span class="sxs-lookup"><span data-stu-id="8ea5c-234">Message reaction events</span></span>

<span data-ttu-id="8ea5c-235">`messageReaction`当用户向自动程序发送的消息添加或删除反应时，将发送该事件。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-235">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="8ea5c-236">包含 `replyToId` 特定消息的 ID，它是 `Type` 文本格式的反应类型。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-236">The `replyToId` contains the ID of the specific message, and the `Type` is the type of reaction in text format.</span></span>  <span data-ttu-id="8ea5c-237">反应类型包括："heart"、"heart"、"heart"、"like"、"Heart"、"surprised"、"surprised"。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-237">The types of reactions include: "angry", "heart", "laugh", "like", "Sad", "surprised".</span></span> <span data-ttu-id="8ea5c-238">此事件不包含原始邮件的内容，因此，如果处理对消息的反应对于自动程序非常重要，则需要在发送邮件时存储它们。</span><span class="sxs-lookup"><span data-stu-id="8ea5c-238">This event does not contain the contents of the original message, so if processing reactions to your messages is important for your bot you'll need to store the messages when you send them.</span></span>

| <span data-ttu-id="8ea5c-239">EventType</span><span class="sxs-lookup"><span data-stu-id="8ea5c-239">EventType</span></span>       | <span data-ttu-id="8ea5c-240">Payload 对象</span><span class="sxs-lookup"><span data-stu-id="8ea5c-240">Payload object</span></span>   | <span data-ttu-id="8ea5c-241">说明</span><span class="sxs-lookup"><span data-stu-id="8ea5c-241">Description</span></span>                                                             | <span data-ttu-id="8ea5c-242">范围</span><span class="sxs-lookup"><span data-stu-id="8ea5c-242">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="8ea5c-243">messageReaction</span><span class="sxs-lookup"><span data-stu-id="8ea5c-243">messageReaction</span></span> | <span data-ttu-id="8ea5c-244">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="8ea5c-244">reactionsAdded</span></span>   | [<span data-ttu-id="8ea5c-245">对机器人消息的反应</span><span class="sxs-lookup"><span data-stu-id="8ea5c-245">Reaction to bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="8ea5c-246">全部</span><span class="sxs-lookup"><span data-stu-id="8ea5c-246">All</span></span>   |
| <span data-ttu-id="8ea5c-247">messageReaction</span><span class="sxs-lookup"><span data-stu-id="8ea5c-247">messageReaction</span></span> | <span data-ttu-id="8ea5c-248">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="8ea5c-248">reactionsRemoved</span></span> | [<span data-ttu-id="8ea5c-249">从自动程序消息中删除了反应</span><span class="sxs-lookup"><span data-stu-id="8ea5c-249">Reaction removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="8ea5c-250">全部</span><span class="sxs-lookup"><span data-stu-id="8ea5c-250">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="8ea5c-251">对自动程序消息的反应</span><span class="sxs-lookup"><span data-stu-id="8ea5c-251">Reactions to a bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8ea5c-252">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8ea5c-252">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnReactionsAddedAsync(IList<MessageReaction> messageReactions, ITurnContext<IMessageReactionActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (var reaction in messageReactions)
    {
      var newReaction = $"You reacted with '{reaction.Type}' to the following message: '{turnContext.Activity.ReplyToId}'";
      var replyActivity = MessageFactory.Text(newReaction);
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8ea5c-253">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8ea5c-253">TypeScript/Node.js</span></span>](#tab/typescript)

<!-- Verify -->

```typescript

export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onReactionsAdded(async (context, next) => {
           const reactionsAdded = context.activity.reactionsAdded;
            if (reactionsAdded && reactionsAdded.length > 0) {
                for (let i = 0; i < reactionsAdded.length; i++) {
                    const reaction = reactionsAdded[i];
                    const newReaction = `You reacted with '${reaction.type}' to the following message: '${context.activity.replyToId}'`;
                    const resourceResponse = context.sendActivity(newReaction);
                    // Save information about the sent message and its ID (resourceResponse.id).
                }
            }
        });
    }
}

```

# <a name="json"></a>[<span data-ttu-id="8ea5c-254">JSON</span><span class="sxs-lookup"><span data-stu-id="8ea5c-254">JSON</span></span>](#tab/json)

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
    "replyToId": "1575667808184",
    "legacy": {
      "replyToId": "1:19uJ8TZA1cZcms7-2HLOW3pWRF4nSWEoVnRqc0DPa_kY"
    }
}
```

# <a name="python"></a>[<span data-ttu-id="8ea5c-255">Python</span><span class="sxs-lookup"><span data-stu-id="8ea5c-255">Python</span></span>](#tab/python)

```python
async def on_reactions_added(
    self, message_reactions: List[MessageReaction], turn_context: TurnContext
):
    for reaction in message_reactions:
        activity = await self._log.find(turn_context.activity.reply_to_id)
        if not activity:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"Activity {turn_context.activity.reply_to_id} not found in log",
            )
        else:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"You added '{reaction.type}' regarding '{activity.text}'",
            )
    return
```

* * *

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="8ea5c-256">从自动程序消息中删除的反应</span><span class="sxs-lookup"><span data-stu-id="8ea5c-256">Reactions removed from bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="8ea5c-257">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="8ea5c-257">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnReactionsRemovedAsync(IList<MessageReaction> messageReactions, ITurnContext<IMessageReactionActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (var reaction in messageReactions)
    {
      var newReaction = $"You removed the reaction '{reaction.Type}' from the following message: '{turnContext.Activity.ReplyToId}'";
      var replyActivity = MessageFactory.Text(newReaction);
      var resourceResponse = await turnContext.SendActivityAsync(replyActivity, cancellationToken);
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="8ea5c-258">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="8ea5c-258">TypeScript/Node.js</span></span>](#tab/typescript)

<!-- Verify -->

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onReactionsRemoved(async(context,next)=>{
            const reactionsRemoved = context.activity.reactionsRemoved;
            if (reactionsRemoved && reactionsRemoved.length > 0) {
                for (let i = 0; i < reactionsRemoved.length; i++) {
                    const reaction = reactionsRemoved[i];
                    const newReaction = `You removed the reaction '${reaction.type}' from the message: '${context.activity.replyToId}'`;
                    const resourceResponse = context.sendActivity(newReaction);
                    // Save information about the sent message and its ID (resourceResponse.id).
                }
            }
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="8ea5c-259">JSON</span><span class="sxs-lookup"><span data-stu-id="8ea5c-259">JSON</span></span>](#tab/json)

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
    "replyToId": "1575667808184",
    "legacy": {
      "replyToId": "1:19uJ8TZA1cZcms7-2HLOW3pWRF4nSWEoVnRqc0DPa_kY"
    }
}
```

# <a name="python"></a>[<span data-ttu-id="8ea5c-260">Python</span><span class="sxs-lookup"><span data-stu-id="8ea5c-260">Python</span></span>](#tab/python)

```python
async def on_reactions_removed(
    self, message_reactions: List[MessageReaction], turn_context: TurnContext
):
    for reaction in message_reactions:
        activity = await self._log.find(turn_context.activity.reply_to_id)
        if not activity:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"Activity {turn_context.activity.reply_to_id} not found in log",
            )
        else:
            await self._send_message_and_log_activity_id(
                turn_context,
                f"You removed '{reaction.type}' regarding '{activity.text}'",
            )
    return
```

* * *
