---
title: 订阅对话事件
author: WashingtonKayaker
description: 如何从 Microsoft Teams 机器人订阅对话事件。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: bc4ae36d8cffe5b19ee778a71e1c7b1c00c5e88c
ms.sourcegitcommit: b50f6d68482cad43a60642a9947d1be17809a7df
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634500"
---
# <a name="subscribe-to-conversation-events"></a><span data-ttu-id="72e86-103">订阅对话事件</span><span class="sxs-lookup"><span data-stu-id="72e86-103">Subscribe to conversation events</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="72e86-104">对于发生在机器人活动范围内的事件，Microsoft Teams 会向机器人发送通知。</span><span class="sxs-lookup"><span data-stu-id="72e86-104">Microsoft Teams sends notifications to your bot for events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="72e86-105">可以在代码中捕获这些事件，并针对事件采取行动，如下文所示：</span><span class="sxs-lookup"><span data-stu-id="72e86-105">You can capture these events in your code and take action on them, such as the following:</span></span>

* <span data-ttu-id="72e86-106">将机器人添加到团队时触发欢迎消息</span><span class="sxs-lookup"><span data-stu-id="72e86-106">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="72e86-107">添加或删除新团队成员时触发欢迎消息</span><span class="sxs-lookup"><span data-stu-id="72e86-107">Trigger a welcome message when a new team member is added or removed</span></span>
* <span data-ttu-id="72e86-108">创建、重命名或删除频道时触发通知</span><span class="sxs-lookup"><span data-stu-id="72e86-108">Trigger a notification when a channel is created, renamed or deleted</span></span>
* <span data-ttu-id="72e86-109">用户喜欢自动程序消息时</span><span class="sxs-lookup"><span data-stu-id="72e86-109">When a bot message is liked by a user</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="72e86-110">对话更新事件</span><span class="sxs-lookup"><span data-stu-id="72e86-110">Conversation update events</span></span>

> [!Important]
> <span data-ttu-id="72e86-111">你随时都可以添加新事件，你的机器人将开始接收它们。</span><span class="sxs-lookup"><span data-stu-id="72e86-111">New events can be added at any time, and your bot will begin to receive them.</span></span>
> <span data-ttu-id="72e86-112">您必须针对接收意外事件的可能性进行设计。</span><span class="sxs-lookup"><span data-stu-id="72e86-112">You must design for the possibility of receiving unexpected events.</span></span>
> <span data-ttu-id="72e86-113">如果你使用的是 Bot Framework SDK，则自动程序将自动响应你未选择 `200 - OK` 处理的任何事件。</span><span class="sxs-lookup"><span data-stu-id="72e86-113">If you are using the Bot Framework SDK, your bot will automatically respond with a `200 - OK` to any events you do not choose to handle.</span></span>

<span data-ttu-id="72e86-114">将机器人添加到对话后、将其他成员添加到对话或从对话中删除其他成员后，或更改对话元数据后，机器人将收到 `conversationUpdate` 事件。</span><span class="sxs-lookup"><span data-stu-id="72e86-114">A bot receives a `conversationUpdate` event when it has been added to a conversation, other members have been added to or removed from a conversation, or conversation metadata has changed.</span></span>

<span data-ttu-id="72e86-115">当机器人收到关于其所属团队的成员身份更新信息时，`conversationUpdate` 事件就会发送到机器人。</span><span class="sxs-lookup"><span data-stu-id="72e86-115">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="72e86-116">在首次专门为个人对话添加机器人时，机器人也会收到更新。</span><span class="sxs-lookup"><span data-stu-id="72e86-116">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span>

<span data-ttu-id="72e86-117">下表显示了 Teams 对话更新事件的列表，以及指向更多详细信息的链接。</span><span class="sxs-lookup"><span data-stu-id="72e86-117">The following table shows a list of Teams conversation update events, with links to more details.</span></span>

| <span data-ttu-id="72e86-118">已采取的操作</span><span class="sxs-lookup"><span data-stu-id="72e86-118">Action Taken</span></span>        | <span data-ttu-id="72e86-119">EventType</span><span class="sxs-lookup"><span data-stu-id="72e86-119">EventType</span></span>         | <span data-ttu-id="72e86-120">方法已调用</span><span class="sxs-lookup"><span data-stu-id="72e86-120">Method Called</span></span>              | <span data-ttu-id="72e86-121">说明</span><span class="sxs-lookup"><span data-stu-id="72e86-121">Description</span></span>                | <span data-ttu-id="72e86-122">范围</span><span class="sxs-lookup"><span data-stu-id="72e86-122">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="72e86-123">创建通道</span><span class="sxs-lookup"><span data-stu-id="72e86-123">channel created</span></span>     | <span data-ttu-id="72e86-124">channelCreated</span><span class="sxs-lookup"><span data-stu-id="72e86-124">channelCreated</span></span>    | <span data-ttu-id="72e86-125">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="72e86-125">OnTeamsChannelCreatedAsync</span></span> | [<span data-ttu-id="72e86-126">已创建频道</span><span class="sxs-lookup"><span data-stu-id="72e86-126">A channel was created</span></span>](#channel-created) | <span data-ttu-id="72e86-127">Team</span><span class="sxs-lookup"><span data-stu-id="72e86-127">Team</span></span> |
| <span data-ttu-id="72e86-128">通道重命名</span><span class="sxs-lookup"><span data-stu-id="72e86-128">channel renamed</span></span>     | <span data-ttu-id="72e86-129">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="72e86-129">channelRenamed</span></span>    | <span data-ttu-id="72e86-130">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="72e86-130">OnTeamsChannelRenamedAsync</span></span> | [<span data-ttu-id="72e86-131">频道已重命名</span><span class="sxs-lookup"><span data-stu-id="72e86-131">A channel was renamed</span></span>](#channel-renamed) | <span data-ttu-id="72e86-132">Team</span><span class="sxs-lookup"><span data-stu-id="72e86-132">Team</span></span> |
| <span data-ttu-id="72e86-133">频道已删除</span><span class="sxs-lookup"><span data-stu-id="72e86-133">channel deleted</span></span>     | <span data-ttu-id="72e86-134">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="72e86-134">channelDeleted</span></span>    | <span data-ttu-id="72e86-135">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="72e86-135">OnTeamsChannelDeletedAsync</span></span> | [<span data-ttu-id="72e86-136">已删除频道</span><span class="sxs-lookup"><span data-stu-id="72e86-136">A channel was deleted</span></span>](#channel-deleted) | <span data-ttu-id="72e86-137">Team</span><span class="sxs-lookup"><span data-stu-id="72e86-137">Team</span></span> |
| <span data-ttu-id="72e86-138">通道已还原</span><span class="sxs-lookup"><span data-stu-id="72e86-138">channel restored</span></span>    | <span data-ttu-id="72e86-139">channelRestored</span><span class="sxs-lookup"><span data-stu-id="72e86-139">channelRestored</span></span>    | <span data-ttu-id="72e86-140">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="72e86-140">OnTeamsChannelRestoredAsync</span></span> | [<span data-ttu-id="72e86-141">已还原频道</span><span class="sxs-lookup"><span data-stu-id="72e86-141">A channel was restored</span></span>](#channel-deleted) | <span data-ttu-id="72e86-142">Team</span><span class="sxs-lookup"><span data-stu-id="72e86-142">Team</span></span> |
| <span data-ttu-id="72e86-143">members added</span><span class="sxs-lookup"><span data-stu-id="72e86-143">members added</span></span>   | <span data-ttu-id="72e86-144">membersAdded</span><span class="sxs-lookup"><span data-stu-id="72e86-144">membersAdded</span></span>   | <span data-ttu-id="72e86-145">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="72e86-145">OnTeamsMembersAddedAsync</span></span>   | [<span data-ttu-id="72e86-146">已添加成员</span><span class="sxs-lookup"><span data-stu-id="72e86-146">A member added</span></span>](#team-members-added)   | <span data-ttu-id="72e86-147">全部</span><span class="sxs-lookup"><span data-stu-id="72e86-147">All</span></span> |
| <span data-ttu-id="72e86-148">成员已删除</span><span class="sxs-lookup"><span data-stu-id="72e86-148">members removed</span></span> | <span data-ttu-id="72e86-149">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="72e86-149">membersRemoved</span></span> | <span data-ttu-id="72e86-150">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="72e86-150">OnTeamsMembersRemovedAsync</span></span> | [<span data-ttu-id="72e86-151">已删除成员</span><span class="sxs-lookup"><span data-stu-id="72e86-151">A member was removed</span></span>](#team-members-removed) | <span data-ttu-id="72e86-152">groupChat & team</span><span class="sxs-lookup"><span data-stu-id="72e86-152">groupChat & team</span></span> |
| <span data-ttu-id="72e86-153">团队重命名</span><span class="sxs-lookup"><span data-stu-id="72e86-153">team renamed</span></span>        | <span data-ttu-id="72e86-154">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="72e86-154">teamRenamed</span></span>       | <span data-ttu-id="72e86-155">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="72e86-155">OnTeamsTeamRenamedAsync</span></span>    | [<span data-ttu-id="72e86-156">团队已重命名</span><span class="sxs-lookup"><span data-stu-id="72e86-156">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="72e86-157">Team</span><span class="sxs-lookup"><span data-stu-id="72e86-157">Team</span></span> |
| <span data-ttu-id="72e86-158">团队已删除</span><span class="sxs-lookup"><span data-stu-id="72e86-158">team deleted</span></span>        | <span data-ttu-id="72e86-159">teamDeleted</span><span class="sxs-lookup"><span data-stu-id="72e86-159">teamDeleted</span></span>       | <span data-ttu-id="72e86-160">OnTeamsTeamDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="72e86-160">OnTeamsTeamDeletedAsync</span></span>    | [<span data-ttu-id="72e86-161">已删除团队</span><span class="sxs-lookup"><span data-stu-id="72e86-161">A Team was deleted</span></span>](#team-deleted)       | <span data-ttu-id="72e86-162">Team</span><span class="sxs-lookup"><span data-stu-id="72e86-162">Team</span></span> |
| <span data-ttu-id="72e86-163">团队存档</span><span class="sxs-lookup"><span data-stu-id="72e86-163">team archived</span></span>        | <span data-ttu-id="72e86-164">teamArchived</span><span class="sxs-lookup"><span data-stu-id="72e86-164">teamArchived</span></span>       | <span data-ttu-id="72e86-165">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="72e86-165">OnTeamsTeamArchivedAsync</span></span>    | [<span data-ttu-id="72e86-166">已存档团队</span><span class="sxs-lookup"><span data-stu-id="72e86-166">A Team was archived</span></span>](#team-archived)       | <span data-ttu-id="72e86-167">Team</span><span class="sxs-lookup"><span data-stu-id="72e86-167">Team</span></span> |
| <span data-ttu-id="72e86-168">团队未存档</span><span class="sxs-lookup"><span data-stu-id="72e86-168">team unarchived</span></span>        | <span data-ttu-id="72e86-169">teamUnarchived</span><span class="sxs-lookup"><span data-stu-id="72e86-169">teamUnarchived</span></span>       | <span data-ttu-id="72e86-170">OnTeamsTeamUnarchivedAsync</span><span class="sxs-lookup"><span data-stu-id="72e86-170">OnTeamsTeamUnarchivedAsync</span></span>    | [<span data-ttu-id="72e86-171">团队未存档</span><span class="sxs-lookup"><span data-stu-id="72e86-171">A Team was unarchived</span></span>](#team-unarchived)       | <span data-ttu-id="72e86-172">Team</span><span class="sxs-lookup"><span data-stu-id="72e86-172">Team</span></span> |
| <span data-ttu-id="72e86-173">团队已还原</span><span class="sxs-lookup"><span data-stu-id="72e86-173">team restored</span></span>        | <span data-ttu-id="72e86-174">teamRestored</span><span class="sxs-lookup"><span data-stu-id="72e86-174">teamRestored</span></span>      | <span data-ttu-id="72e86-175">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="72e86-175">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="72e86-176">已还原团队</span><span class="sxs-lookup"><span data-stu-id="72e86-176">A Team was restored</span></span>](#team-restored)       | <span data-ttu-id="72e86-177">Team</span><span class="sxs-lookup"><span data-stu-id="72e86-177">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="72e86-178">已创建频道</span><span class="sxs-lookup"><span data-stu-id="72e86-178">Channel created</span></span>

<span data-ttu-id="72e86-179">只要在安装自动程序的团队中创建了新频道，就会将频道创建事件发送给机器人。</span><span class="sxs-lookup"><span data-stu-id="72e86-179">The channel created event is sent to your bot whenever a new channel is created in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="72e86-180">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="72e86-180">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="72e86-181">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="72e86-181">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="72e86-182">JSON</span><span class="sxs-lookup"><span data-stu-id="72e86-182">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="72e86-183">Python</span><span class="sxs-lookup"><span data-stu-id="72e86-183">Python</span></span>](#tab/python)

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

### <a name="channel-renamed"></a><span data-ttu-id="72e86-184">通道重命名</span><span class="sxs-lookup"><span data-stu-id="72e86-184">Channel renamed</span></span>

<span data-ttu-id="72e86-185">只要频道在安装自动程序的团队中重命名，频道重命名事件就会发送到机器人。</span><span class="sxs-lookup"><span data-stu-id="72e86-185">The channel renamed event is sent to your bot whenever a channel is renamed in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="72e86-186">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="72e86-186">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="72e86-187">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="72e86-187">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="72e86-188">JSON</span><span class="sxs-lookup"><span data-stu-id="72e86-188">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="72e86-189">Python</span><span class="sxs-lookup"><span data-stu-id="72e86-189">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="72e86-190">频道已删除</span><span class="sxs-lookup"><span data-stu-id="72e86-190">Channel Deleted</span></span>

<span data-ttu-id="72e86-191">只要在安装自动程序的团队中删除频道，频道删除事件就会发送给机器人。</span><span class="sxs-lookup"><span data-stu-id="72e86-191">The channel deleted event is sent to your bot whenever a channel is deleted in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="72e86-192">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="72e86-192">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="72e86-193">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="72e86-193">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="72e86-194">JSON</span><span class="sxs-lookup"><span data-stu-id="72e86-194">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="72e86-195">Python</span><span class="sxs-lookup"><span data-stu-id="72e86-195">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="channel-restored"></a><span data-ttu-id="72e86-196">已还原频道</span><span class="sxs-lookup"><span data-stu-id="72e86-196">Channel restored</span></span>

<span data-ttu-id="72e86-197">只要在已安装自动程序的团队中还原以前删除的频道，就会将频道还原事件发送给机器人。</span><span class="sxs-lookup"><span data-stu-id="72e86-197">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team that your bot is already installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="72e86-198">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="72e86-198">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="72e86-199">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="72e86-199">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="72e86-200">JSON</span><span class="sxs-lookup"><span data-stu-id="72e86-200">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="72e86-201">Python</span><span class="sxs-lookup"><span data-stu-id="72e86-201">Python</span></span>](#tab/python)

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

### <a name="team-members-added"></a><span data-ttu-id="72e86-202">添加了工作组成员</span><span class="sxs-lookup"><span data-stu-id="72e86-202">Team members added</span></span>

<span data-ttu-id="72e86-203">该事件在首次添加到对话时以及每次将新用户添加到安装机器人的团队或群聊时发送给 `teamMemberAdded` 机器人。</span><span class="sxs-lookup"><span data-stu-id="72e86-203">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation and every time a new user is added to a team or group chat that your bot is installed in.</span></span> <span data-ttu-id="72e86-204">用户信息 (ID) 对于自动程序来说是唯一的，可以缓存这些信息供你的服务组织 (例如向特定用户发送) 。</span><span class="sxs-lookup"><span data-stu-id="72e86-204">The user information (ID) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="72e86-205">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="72e86-205">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="72e86-206">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="72e86-206">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="72e86-207">JSON</span><span class="sxs-lookup"><span data-stu-id="72e86-207">JSON</span></span>](#tab/json)

<span data-ttu-id="72e86-208">这是在将机器人添加到团队时机器人将收到 **的消息**。</span><span class="sxs-lookup"><span data-stu-id="72e86-208">This is the message your bot will receive when the bot is added **to a team**.</span></span>

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

<span data-ttu-id="72e86-209">这是自动程序在将 \* 添加到一对一聊天时将收到 *的消息*。</span><span class="sxs-lookup"><span data-stu-id="72e86-209">This is the message your bot will receive when the bot is added \**to a one-to-one chat*.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="72e86-210">Python</span><span class="sxs-lookup"><span data-stu-id="72e86-210">Python</span></span>](#tab/python)

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

* * *

### <a name="team-members-removed"></a><span data-ttu-id="72e86-211">已删除团队成员</span><span class="sxs-lookup"><span data-stu-id="72e86-211">Team members removed</span></span>

<span data-ttu-id="72e86-212">如果从团队中删除了事件，并且每次从自动程序是其成员的团队中删除任何用户时，该事件 `teamMemberRemoved` 都会发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="72e86-212">The `teamMemberRemoved` event is sent to your bot if it is removed from a team and every time any user is removed from a team that your bot is a member of.</span></span> <span data-ttu-id="72e86-213">通过查看 的对象，可以确定删除的新增成员是机器人本身还是 `Activity` 用户 `turnContext` 。</span><span class="sxs-lookup"><span data-stu-id="72e86-213">You can determine if the new member removed was the bot itself or a user by looking at the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="72e86-214">如果对象的字段与对象的字段相同，则删除的成员为自动程序，否则 `Id` `MembersRemoved` `Id` `Recipient` 为用户。</span><span class="sxs-lookup"><span data-stu-id="72e86-214">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, otherwise, it is a user.</span></span>  <span data-ttu-id="72e86-215">自动程序 `Id` 通常为： `28:<MicrosoftAppId>`</span><span class="sxs-lookup"><span data-stu-id="72e86-215">The bot's `Id` will generally be: `28:<MicrosoftAppId>`</span></span>

[!Note] <span data-ttu-id="72e86-216">从租户中永久删除用户时， `membersRemoved conversationUpdate` 将触发事件。</span><span class="sxs-lookup"><span data-stu-id="72e86-216">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="72e86-217">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="72e86-217">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="72e86-218">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="72e86-218">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="72e86-219">JSON</span><span class="sxs-lookup"><span data-stu-id="72e86-219">JSON</span></span>](#tab/json)

<span data-ttu-id="72e86-220">以下有效负载示例中的对象基于将成员添加到团队（而不是群组聊天）或启动新的一对 `channelData` 一对话：</span><span class="sxs-lookup"><span data-stu-id="72e86-220">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="72e86-221">Python</span><span class="sxs-lookup"><span data-stu-id="72e86-221">Python</span></span>](#tab/python)

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

### <a name="team-renamed"></a><span data-ttu-id="72e86-222">团队重命名</span><span class="sxs-lookup"><span data-stu-id="72e86-222">Team renamed</span></span>

<span data-ttu-id="72e86-223">当自动程序位于的团队重命名时，将会收到通知。</span><span class="sxs-lookup"><span data-stu-id="72e86-223">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="72e86-224">它接收 `conversationUpdate` 对象中的 `eventType.teamRenamed` 事件 `channelData` 。</span><span class="sxs-lookup"><span data-stu-id="72e86-224">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="72e86-225">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="72e86-225">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="72e86-226">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="72e86-226">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="72e86-227">JSON</span><span class="sxs-lookup"><span data-stu-id="72e86-227">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="72e86-228">Python</span><span class="sxs-lookup"><span data-stu-id="72e86-228">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

### <a name="team-deleted"></a><span data-ttu-id="72e86-229">团队已删除</span><span class="sxs-lookup"><span data-stu-id="72e86-229">Team deleted</span></span>

<span data-ttu-id="72e86-230">当自动程序位于的团队被删除时，将会收到通知。</span><span class="sxs-lookup"><span data-stu-id="72e86-230">Your bot is notified when the team it is in has been deleted.</span></span> <span data-ttu-id="72e86-231">它接收 `conversationUpdate` 对象中的 `eventType.teamDeleted` 事件 `channelData` 。</span><span class="sxs-lookup"><span data-stu-id="72e86-231">It receives a `conversationUpdate` event with `eventType.teamDeleted` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="72e86-232">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="72e86-232">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="72e86-233">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="72e86-233">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamDeletedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            //handle delete event
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="72e86-234">JSON</span><span class="sxs-lookup"><span data-stu-id="72e86-234">JSON</span></span>](#tab/json)

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
        "eventType": "teamDeleted",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="72e86-235">Python</span><span class="sxs-lookup"><span data-stu-id="72e86-235">Python</span></span>](#tab/python)

```python
async def on_teams_team_deleted(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    //handle delete event
    )
```

* * *

### <a name="team-restored"></a><span data-ttu-id="72e86-236">已还原团队</span><span class="sxs-lookup"><span data-stu-id="72e86-236">Team restored</span></span>

<span data-ttu-id="72e86-237">当团队从删除中恢复时，机器人会收到通知。</span><span class="sxs-lookup"><span data-stu-id="72e86-237">The bot receives a notification when the team is restored from deletion.</span></span> <span data-ttu-id="72e86-238">机器人接收 `conversationUpdate` 对象中的 `eventType.teamrestored` 事件 `channelData` 。</span><span class="sxs-lookup"><span data-stu-id="72e86-238">The bot receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="72e86-239">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="72e86-239">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="72e86-240">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="72e86-240">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="72e86-241">JSON</span><span class="sxs-lookup"><span data-stu-id="72e86-241">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="72e86-242">Python</span><span class="sxs-lookup"><span data-stu-id="72e86-242">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

### <a name="team-archived"></a><span data-ttu-id="72e86-243">团队存档</span><span class="sxs-lookup"><span data-stu-id="72e86-243">Team archived</span></span>

<span data-ttu-id="72e86-244">自动程序在存档安装它的团队时收到通知。</span><span class="sxs-lookup"><span data-stu-id="72e86-244">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="72e86-245">它接收 `conversationUpdate` 对象中的 `eventType.teamarchived` 事件 `channelData` 。</span><span class="sxs-lookup"><span data-stu-id="72e86-245">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="72e86-246">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="72e86-246">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="72e86-247">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="72e86-247">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="72e86-248">JSON</span><span class="sxs-lookup"><span data-stu-id="72e86-248">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="72e86-249">Python</span><span class="sxs-lookup"><span data-stu-id="72e86-249">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *


### <a name="team-unarchived"></a><span data-ttu-id="72e86-250">团队未存档</span><span class="sxs-lookup"><span data-stu-id="72e86-250">Team unarchived</span></span>

<span data-ttu-id="72e86-251">自动程序在安装它的团队未存档时收到通知。</span><span class="sxs-lookup"><span data-stu-id="72e86-251">The bot receives a notification when the team it is installed in is unarchived.</span></span> <span data-ttu-id="72e86-252">它接收 `conversationUpdate` 对象中的 `eventType.teamUnarchived` 事件 `channelData` 。</span><span class="sxs-lookup"><span data-stu-id="72e86-252">It receives a `conversationUpdate` event with `eventType.teamUnarchived` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="72e86-253">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="72e86-253">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="72e86-254">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="72e86-254">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onTeamsTeamUnarchivedEvent(async (teamInfo: TeamInfo, turnContext: TurnContext, next: () => Promise<void>): Promise<void> => {
            const card = CardFactory.heroCard('Team archived', `${teamInfo.name} is the team name`);
            const message = MessageFactory.attachment(card);
            await turnContext.sendActivity(message);
            await next();
        });
    }
}
```

# <a name="json"></a>[<span data-ttu-id="72e86-255">JSON</span><span class="sxs-lookup"><span data-stu-id="72e86-255">JSON</span></span>](#tab/json)

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
        "eventType": "teamUnarchived",
        "tenant": { 
           "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    }
}
```

# <a name="python"></a>[<span data-ttu-id="72e86-256">Python</span><span class="sxs-lookup"><span data-stu-id="72e86-256">Python</span></span>](#tab/python)

```python
async def on_teams_team_unarchived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

* * *

## <a name="message-reaction-events"></a><span data-ttu-id="72e86-257">邮件反应事件</span><span class="sxs-lookup"><span data-stu-id="72e86-257">Message reaction events</span></span>

<span data-ttu-id="72e86-258">当用户 `messageReaction` 向自动程序发送的消息添加或删除反应时，将发送该事件。</span><span class="sxs-lookup"><span data-stu-id="72e86-258">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="72e86-259">`replyToId`包含特定邮件的 ID，并且 `Type` 是文本格式的反应类型。</span><span class="sxs-lookup"><span data-stu-id="72e86-259">The `replyToId` contains the ID of the specific message, and the `Type` is the type of reaction in text format.</span></span>  <span data-ttu-id="72e86-260">反应类型包括："heart"、"heart"、"heart"、"like"、"Heart"、"surprised"。</span><span class="sxs-lookup"><span data-stu-id="72e86-260">The types of reactions include: "angry", "heart", "laugh", "like", "Sad", "surprised".</span></span> <span data-ttu-id="72e86-261">此事件不包含原始邮件的内容，因此，如果处理对消息的反应对于自动程序非常重要，则需要在发送邮件时存储这些消息。</span><span class="sxs-lookup"><span data-stu-id="72e86-261">This event does not contain the contents of the original message, so if processing reactions to your messages is important for your bot you'll need to store the messages when you send them.</span></span>

| <span data-ttu-id="72e86-262">EventType</span><span class="sxs-lookup"><span data-stu-id="72e86-262">EventType</span></span>       | <span data-ttu-id="72e86-263">Payload 对象</span><span class="sxs-lookup"><span data-stu-id="72e86-263">Payload object</span></span>   | <span data-ttu-id="72e86-264">说明</span><span class="sxs-lookup"><span data-stu-id="72e86-264">Description</span></span>                                                             | <span data-ttu-id="72e86-265">范围</span><span class="sxs-lookup"><span data-stu-id="72e86-265">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="72e86-266">messageReaction</span><span class="sxs-lookup"><span data-stu-id="72e86-266">messageReaction</span></span> | <span data-ttu-id="72e86-267">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="72e86-267">reactionsAdded</span></span>   | [<span data-ttu-id="72e86-268">对自动程序消息的反应</span><span class="sxs-lookup"><span data-stu-id="72e86-268">Reaction to bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="72e86-269">全部</span><span class="sxs-lookup"><span data-stu-id="72e86-269">All</span></span>   |
| <span data-ttu-id="72e86-270">messageReaction</span><span class="sxs-lookup"><span data-stu-id="72e86-270">messageReaction</span></span> | <span data-ttu-id="72e86-271">将removed</span><span class="sxs-lookup"><span data-stu-id="72e86-271">reactionsRemoved</span></span> | [<span data-ttu-id="72e86-272">从自动程序消息中删除的反应</span><span class="sxs-lookup"><span data-stu-id="72e86-272">Reaction removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="72e86-273">全部</span><span class="sxs-lookup"><span data-stu-id="72e86-273">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="72e86-274">对自动程序消息的反应</span><span class="sxs-lookup"><span data-stu-id="72e86-274">Reactions to a bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="72e86-275">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="72e86-275">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="72e86-276">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="72e86-276">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="72e86-277">JSON</span><span class="sxs-lookup"><span data-stu-id="72e86-277">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="72e86-278">Python</span><span class="sxs-lookup"><span data-stu-id="72e86-278">Python</span></span>](#tab/python)

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

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="72e86-279">从自动程序消息中删除的反应</span><span class="sxs-lookup"><span data-stu-id="72e86-279">Reactions removed from bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="72e86-280">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="72e86-280">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="72e86-281">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="72e86-281">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="72e86-282">JSON</span><span class="sxs-lookup"><span data-stu-id="72e86-282">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="72e86-283">Python</span><span class="sxs-lookup"><span data-stu-id="72e86-283">Python</span></span>](#tab/python)

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

## <a name="samples"></a><span data-ttu-id="72e86-284">示例</span><span class="sxs-lookup"><span data-stu-id="72e86-284">Samples</span></span>

<span data-ttu-id="72e86-285">有关显示机器人对话事件的示例代码，请参阅：</span><span class="sxs-lookup"><span data-stu-id="72e86-285">For sample code showing the bots conversation events, see:</span></span>

[<span data-ttu-id="72e86-286">Microsoft Teams 机器人对话事件示例</span><span class="sxs-lookup"><span data-stu-id="72e86-286">Microsoft Teams bots conversation events sample</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)



