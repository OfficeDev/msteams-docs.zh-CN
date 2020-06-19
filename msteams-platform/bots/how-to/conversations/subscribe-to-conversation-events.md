---
title: 订阅对话事件
author: WashingtonKayaker
description: 如何订阅来自 Microsoft 团队 bot 的对话事件。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: a8c6c39989a7d09a325412438f0d2ace78259cb7
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801010"
---
# <a name="subscribe-to-conversation-events"></a><span data-ttu-id="6bd04-103">订阅对话事件</span><span class="sxs-lookup"><span data-stu-id="6bd04-103">Subscribe to conversation events</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="6bd04-104">Microsoft 团队将通知发送到你的 bot，以获取在你的 bot 处于活动状态的范围内发生的事件。</span><span class="sxs-lookup"><span data-stu-id="6bd04-104">Microsoft Teams sends notifications to your bot for events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="6bd04-105">您可以在代码中捕获这些事件，并对其执行操作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6bd04-105">You can capture these events in your code and take action on them, such as the following:</span></span>

* <span data-ttu-id="6bd04-106">在将你的 bot 添加到团队时触发欢迎消息</span><span class="sxs-lookup"><span data-stu-id="6bd04-106">Trigger a welcome message when your bot is added to a team</span></span>
* <span data-ttu-id="6bd04-107">添加或删除新的工作组成员时触发欢迎消息</span><span class="sxs-lookup"><span data-stu-id="6bd04-107">Trigger a welcome message when a new team member is added or removed</span></span>
* <span data-ttu-id="6bd04-108">创建、重命名或删除频道时触发通知</span><span class="sxs-lookup"><span data-stu-id="6bd04-108">Trigger a notification when a channel is created, renamed or deleted</span></span>
* <span data-ttu-id="6bd04-109">当用户对 bot 邮件进行了赞时</span><span class="sxs-lookup"><span data-stu-id="6bd04-109">When a bot message is liked by a user</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="6bd04-110">对话更新事件</span><span class="sxs-lookup"><span data-stu-id="6bd04-110">Conversation update events</span></span>

<span data-ttu-id="6bd04-111">`conversationUpdate`当 bot 被添加到对话中时，即会收到事件，其他成员已添加到对话中或从会话中删除，或者对话元数据已更改。</span><span class="sxs-lookup"><span data-stu-id="6bd04-111">A bot receives a `conversationUpdate` event when it has been added to a conversation, other members have been added to or removed from a conversation, or conversation metadata has changed.</span></span>

<span data-ttu-id="6bd04-112">`conversationUpdate`当该事件收到有关已添加的团队成员身份更新的信息时，该事件将发送到你的 bot。</span><span class="sxs-lookup"><span data-stu-id="6bd04-112">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="6bd04-113">它还会在首次专门为个人对话而添加时收到更新。</span><span class="sxs-lookup"><span data-stu-id="6bd04-113">It also receives an update when it has been added for the first time specifically for personal conversations.</span></span>

<span data-ttu-id="6bd04-114">下表显示了团队对话更新事件的列表，并提供了更多详细信息的链接。</span><span class="sxs-lookup"><span data-stu-id="6bd04-114">The following table shows a list of Teams conversation update events, with links to more details.</span></span>

| <span data-ttu-id="6bd04-115">执行的操作</span><span class="sxs-lookup"><span data-stu-id="6bd04-115">Action Taken</span></span>        | <span data-ttu-id="6bd04-116">EventType</span><span class="sxs-lookup"><span data-stu-id="6bd04-116">EventType</span></span>         | <span data-ttu-id="6bd04-117">调用的方法</span><span class="sxs-lookup"><span data-stu-id="6bd04-117">Method Called</span></span>              | <span data-ttu-id="6bd04-118">说明</span><span class="sxs-lookup"><span data-stu-id="6bd04-118">Description</span></span>                | <span data-ttu-id="6bd04-119">范围</span><span class="sxs-lookup"><span data-stu-id="6bd04-119">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="6bd04-120">通道已创建</span><span class="sxs-lookup"><span data-stu-id="6bd04-120">channel created</span></span>     | <span data-ttu-id="6bd04-121">channelCreated</span><span class="sxs-lookup"><span data-stu-id="6bd04-121">channelCreated</span></span>    | <span data-ttu-id="6bd04-122">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="6bd04-122">OnTeamsChannelCreatedAsync</span></span> | [<span data-ttu-id="6bd04-123">通道已创建</span><span class="sxs-lookup"><span data-stu-id="6bd04-123">A channel was created</span></span>](#channel-created) | <span data-ttu-id="6bd04-124">团队</span><span class="sxs-lookup"><span data-stu-id="6bd04-124">Team</span></span> |
| <span data-ttu-id="6bd04-125">频道已重命名</span><span class="sxs-lookup"><span data-stu-id="6bd04-125">channel renamed</span></span>     | <span data-ttu-id="6bd04-126">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="6bd04-126">channelRenamed</span></span>    | <span data-ttu-id="6bd04-127">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="6bd04-127">OnTeamsChannelRenamedAsync</span></span> | [<span data-ttu-id="6bd04-128">频道已重命名</span><span class="sxs-lookup"><span data-stu-id="6bd04-128">A channel was renamed</span></span>](#channel-renamed) | <span data-ttu-id="6bd04-129">团队</span><span class="sxs-lookup"><span data-stu-id="6bd04-129">Team</span></span> |
| <span data-ttu-id="6bd04-130">频道已删除</span><span class="sxs-lookup"><span data-stu-id="6bd04-130">channel deleted</span></span>     | <span data-ttu-id="6bd04-131">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="6bd04-131">channelDeleted</span></span>    | <span data-ttu-id="6bd04-132">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="6bd04-132">OnTeamsChannelDeletedAsync</span></span> | [<span data-ttu-id="6bd04-133">频道已删除</span><span class="sxs-lookup"><span data-stu-id="6bd04-133">A channel was deleted</span></span>](#channel-deleted) | <span data-ttu-id="6bd04-134">团队</span><span class="sxs-lookup"><span data-stu-id="6bd04-134">Team</span></span> |
| <span data-ttu-id="6bd04-135">添加的团队成员</span><span class="sxs-lookup"><span data-stu-id="6bd04-135">team members added</span></span>   | <span data-ttu-id="6bd04-136">teamMemberAdded</span><span class="sxs-lookup"><span data-stu-id="6bd04-136">teamMemberAdded</span></span>   | <span data-ttu-id="6bd04-137">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="6bd04-137">OnTeamsMembersAddedAsync</span></span>   | [<span data-ttu-id="6bd04-138">添加到团队的成员</span><span class="sxs-lookup"><span data-stu-id="6bd04-138">A Member added to team</span></span>](#team-members-added)   | <span data-ttu-id="6bd04-139">全部</span><span class="sxs-lookup"><span data-stu-id="6bd04-139">All</span></span> |
| <span data-ttu-id="6bd04-140">删除了团队成员</span><span class="sxs-lookup"><span data-stu-id="6bd04-140">team members removed</span></span> | <span data-ttu-id="6bd04-141">teamMemberRemoved</span><span class="sxs-lookup"><span data-stu-id="6bd04-141">teamMemberRemoved</span></span> | <span data-ttu-id="6bd04-142">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="6bd04-142">OnTeamsMembersRemovedAsync</span></span> | [<span data-ttu-id="6bd04-143">成员已从团队中删除</span><span class="sxs-lookup"><span data-stu-id="6bd04-143">A Member was removed from team</span></span>](#team-members-removed) | <span data-ttu-id="6bd04-144">groupChat & 团队</span><span class="sxs-lookup"><span data-stu-id="6bd04-144">groupChat & team</span></span> |
| <span data-ttu-id="6bd04-145">重命名团队</span><span class="sxs-lookup"><span data-stu-id="6bd04-145">team renamed</span></span>        | <span data-ttu-id="6bd04-146">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="6bd04-146">teamRenamed</span></span>       | <span data-ttu-id="6bd04-147">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="6bd04-147">OnTeamsTeamRenamedAsync</span></span>    | [<span data-ttu-id="6bd04-148">团队已重命名</span><span class="sxs-lookup"><span data-stu-id="6bd04-148">A Team was renamed</span></span>](#team-renamed)       | <span data-ttu-id="6bd04-149">团队</span><span class="sxs-lookup"><span data-stu-id="6bd04-149">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="6bd04-150">通道已创建</span><span class="sxs-lookup"><span data-stu-id="6bd04-150">Channel created</span></span>

<span data-ttu-id="6bd04-151">只要在安装了 bot 的团队中创建了新通道，就会将频道创建事件发送到你的机器人。</span><span class="sxs-lookup"><span data-stu-id="6bd04-151">The channel created event is sent to your bot whenever a new channel is created in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6bd04-152">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6bd04-152">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6bd04-153">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6bd04-153">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="6bd04-154">JSON</span><span class="sxs-lookup"><span data-stu-id="6bd04-154">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="6bd04-155">Python</span><span class="sxs-lookup"><span data-stu-id="6bd04-155">Python</span></span>](#tab/python)

```python
async def on_teams_channel_created_activity(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(
            f"The new channel is {channel_info.name}. The channel id is {channel_info.id}"
        )
    )
```

* * *

### <a name="channel-renamed"></a><span data-ttu-id="6bd04-156">频道已重命名</span><span class="sxs-lookup"><span data-stu-id="6bd04-156">Channel renamed</span></span>

<span data-ttu-id="6bd04-157">只要在安装了 bot 的团队中重命名频道，就会将频道重命名事件发送到你的机器人。</span><span class="sxs-lookup"><span data-stu-id="6bd04-157">The channel renamed event is sent to your bot whenever a channel is renamed in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6bd04-158">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6bd04-158">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6bd04-159">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6bd04-159">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="6bd04-160">JSON</span><span class="sxs-lookup"><span data-stu-id="6bd04-160">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="6bd04-161">Python</span><span class="sxs-lookup"><span data-stu-id="6bd04-161">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed_activity(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

* * *

### <a name="channel-deleted"></a><span data-ttu-id="6bd04-162">频道已删除</span><span class="sxs-lookup"><span data-stu-id="6bd04-162">Channel Deleted</span></span>

<span data-ttu-id="6bd04-163">只要在安装了 bot 的团队中删除频道时，就会将频道删除事件发送到你的机器人。</span><span class="sxs-lookup"><span data-stu-id="6bd04-163">The channel deleted event is sent to your bot whenever a channel is deleted in a team your bot is installed in.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6bd04-164">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6bd04-164">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6bd04-165">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6bd04-165">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="6bd04-166">JSON</span><span class="sxs-lookup"><span data-stu-id="6bd04-166">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="6bd04-167">Python</span><span class="sxs-lookup"><span data-stu-id="6bd04-167">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted_activity(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

* * *

### <a name="team-members-added"></a><span data-ttu-id="6bd04-168">添加的团队成员</span><span class="sxs-lookup"><span data-stu-id="6bd04-168">Team members added</span></span>

<span data-ttu-id="6bd04-169">在 `teamMemberAdded` 首次将事件添加到对话中，以及每次向团队或组聊天中安装了你的 bot 时，都会将该事件发送到你的 bot。</span><span class="sxs-lookup"><span data-stu-id="6bd04-169">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation and every time a new user is added to a team or group chat that your bot is installed in.</span></span> <span data-ttu-id="6bd04-170">用户信息（ID）对你的 bot 是唯一的，并且可以缓存以供你的服务将来使用（例如，向特定用户发送邮件）。</span><span class="sxs-lookup"><span data-stu-id="6bd04-170">The user information (ID) is unique for your bot and can be cached for future use by your service (such as sending a message to a specific user).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6bd04-171">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6bd04-171">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsMembersAddedAsync(IList<ChannelAccount> membersAdded, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    foreach (TeamsChannelAccount member in membersAdded)
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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6bd04-172">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6bd04-172">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="6bd04-173">JSON</span><span class="sxs-lookup"><span data-stu-id="6bd04-173">JSON</span></span>](#tab/json)

<span data-ttu-id="6bd04-174">这是在将 bot 添加**到团队**时，你的 bot 将收到的邮件。</span><span class="sxs-lookup"><span data-stu-id="6bd04-174">This is the message your bot will receive when the bot is added **to a team**.</span></span>

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

<span data-ttu-id="6bd04-175">这是在将 bot 添加*到一对一聊天*时，你的 bot 将收到的邮件。</span><span class="sxs-lookup"><span data-stu-id="6bd04-175">This is the message your bot will receive when the bot is added \**to a one-to-one chat*.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="6bd04-176">Python</span><span class="sxs-lookup"><span data-stu-id="6bd04-176">Python</span></span>](#tab/python)

```python
async def on_teams_members_added_activity(
    self, teams_members_added: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_added:
        await turn_context.send_activity(
            MessageFactory.text(f"Welcome your new team member {member.id}")
        )
    return
```

* * *

### <a name="team-members-removed"></a><span data-ttu-id="6bd04-177">删除了团队成员</span><span class="sxs-lookup"><span data-stu-id="6bd04-177">Team members removed</span></span>

<span data-ttu-id="6bd04-178">`teamMemberRemoved`如果从团队中删除了该事件，并且每次从你的 bot 所属的团队中删除任何用户，则该事件将发送到你的 bot。</span><span class="sxs-lookup"><span data-stu-id="6bd04-178">The `teamMemberRemoved` event is sent to your bot if it is removed from a team and every time any user is removed from a team that your bot is a member of.</span></span> <span data-ttu-id="6bd04-179">您可以通过查看的对象确定删除的新成员是机器人本身还是用户 `Activity` `turnContext` 。</span><span class="sxs-lookup"><span data-stu-id="6bd04-179">You can determine if the new member removed was the bot itself or a user by looking at the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="6bd04-180">如果 `Id` 对象的字段与 `MembersRemoved` 对象的 `Id` 字段相同 `Recipient` ，则删除的成员是 bot，否则是用户。</span><span class="sxs-lookup"><span data-stu-id="6bd04-180">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, otherwise it is a user.</span></span>  <span data-ttu-id="6bd04-181">`Id`通常情况下，bot 将：`28:<MicrosoftAppId>`</span><span class="sxs-lookup"><span data-stu-id="6bd04-181">The bot's `Id` will generally be: `28:<MicrosoftAppId>`</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6bd04-182">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6bd04-182">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6bd04-183">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6bd04-183">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="6bd04-184">JSON</span><span class="sxs-lookup"><span data-stu-id="6bd04-184">JSON</span></span>](#tab/json)

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


# <a name="python"></a>[<span data-ttu-id="6bd04-185">Python</span><span class="sxs-lookup"><span data-stu-id="6bd04-185">Python</span></span>](#tab/python)

```python
async def on_teams_members_removed_activity(
    self, teams_members_removed: [TeamsChannelAccount], turn_context: TurnContext
):
    for member in teams_members_removed:
        await turn_context.send_activity(
            MessageFactory.text(f"Say goodbye to your team member {member.id}")
        )
    return
```

* * *

### <a name="team-renamed"></a><span data-ttu-id="6bd04-186">重命名团队</span><span class="sxs-lookup"><span data-stu-id="6bd04-186">Team renamed</span></span>

<span data-ttu-id="6bd04-187">重命名你的 bot 时，会通知你的你的团队。</span><span class="sxs-lookup"><span data-stu-id="6bd04-187">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="6bd04-188">它接收 `conversationUpdate` `eventType.teamRenamed` 对象中的事件 `channelData` 。</span><span class="sxs-lookup"><span data-stu-id="6bd04-188">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6bd04-189">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6bd04-189">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6bd04-190">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6bd04-190">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="6bd04-191">JSON</span><span class="sxs-lookup"><span data-stu-id="6bd04-191">JSON</span></span>](#tab/json)

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


# <a name="python"></a>[<span data-ttu-id="6bd04-192">Python</span><span class="sxs-lookup"><span data-stu-id="6bd04-192">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed_activity(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

* * *

## <a name="message-reaction-events"></a><span data-ttu-id="6bd04-193">邮件反应事件</span><span class="sxs-lookup"><span data-stu-id="6bd04-193">Message reaction events</span></span>

<span data-ttu-id="6bd04-194">`messageReaction`当用户添加或删除由你的 bot 发送的邮件的反应时，会发送此事件。</span><span class="sxs-lookup"><span data-stu-id="6bd04-194">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="6bd04-195">`replyToId`包含特定邮件的 ID， `Type` 是文本格式的反应类型。</span><span class="sxs-lookup"><span data-stu-id="6bd04-195">The `replyToId` contains the ID of the specific message, and the `Type` is the type of reaction in text format.</span></span>  <span data-ttu-id="6bd04-196">反应类型包括： "生气"、"心形"、"laugh"、"like"、"Sad"、"惊讶"。</span><span class="sxs-lookup"><span data-stu-id="6bd04-196">The types of reactions include: "angry", "heart", "laugh", "like", "Sad", "surprised".</span></span> <span data-ttu-id="6bd04-197">此事件不包含原始邮件的内容，因此，如果处理邮件的反应对你的 bot 非常重要，则在发送邮件时需要将其存储起来。</span><span class="sxs-lookup"><span data-stu-id="6bd04-197">This event does not contain the contents of the original message, so if processing reactions to your messages is important for your bot you'll need to store the messages when you send them.</span></span>

| <span data-ttu-id="6bd04-198">EventType</span><span class="sxs-lookup"><span data-stu-id="6bd04-198">EventType</span></span>       | <span data-ttu-id="6bd04-199">有效负载对象</span><span class="sxs-lookup"><span data-stu-id="6bd04-199">Payload object</span></span>   | <span data-ttu-id="6bd04-200">说明</span><span class="sxs-lookup"><span data-stu-id="6bd04-200">Description</span></span>                                                             | <span data-ttu-id="6bd04-201">范围</span><span class="sxs-lookup"><span data-stu-id="6bd04-201">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="6bd04-202">messageReaction</span><span class="sxs-lookup"><span data-stu-id="6bd04-202">messageReaction</span></span> | <span data-ttu-id="6bd04-203">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="6bd04-203">reactionsAdded</span></span>   | [<span data-ttu-id="6bd04-204">对 bot 邮件的反应</span><span class="sxs-lookup"><span data-stu-id="6bd04-204">Reaction to bot message</span></span>](#reactions-to-a-bot-message)                   | <span data-ttu-id="6bd04-205">全部</span><span class="sxs-lookup"><span data-stu-id="6bd04-205">All</span></span>   |
| <span data-ttu-id="6bd04-206">messageReaction</span><span class="sxs-lookup"><span data-stu-id="6bd04-206">messageReaction</span></span> | <span data-ttu-id="6bd04-207">reactionsRemoved</span><span class="sxs-lookup"><span data-stu-id="6bd04-207">reactionsRemoved</span></span> | [<span data-ttu-id="6bd04-208">从 bot 邮件中删除的反应</span><span class="sxs-lookup"><span data-stu-id="6bd04-208">Reaction removed from bot message</span></span>](#reactions-removed-from-bot-message) | <span data-ttu-id="6bd04-209">全部</span><span class="sxs-lookup"><span data-stu-id="6bd04-209">All</span></span>   |

### <a name="reactions-to-a-bot-message"></a><span data-ttu-id="6bd04-210">Bot 邮件的反应</span><span class="sxs-lookup"><span data-stu-id="6bd04-210">Reactions to a bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6bd04-211">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6bd04-211">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6bd04-212">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6bd04-212">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="6bd04-213">JSON</span><span class="sxs-lookup"><span data-stu-id="6bd04-213">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="6bd04-214">Python</span><span class="sxs-lookup"><span data-stu-id="6bd04-214">Python</span></span>](#tab/python)

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

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="6bd04-215">从 bot 邮件中删除的反应</span><span class="sxs-lookup"><span data-stu-id="6bd04-215">Reactions removed from bot message</span></span>

# <a name="cnet"></a>[<span data-ttu-id="6bd04-216">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="6bd04-216">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="typescriptnodejs"></a>[<span data-ttu-id="6bd04-217">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="6bd04-217">TypeScript/Node.js</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="6bd04-218">JSON</span><span class="sxs-lookup"><span data-stu-id="6bd04-218">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="6bd04-219">Python</span><span class="sxs-lookup"><span data-stu-id="6bd04-219">Python</span></span>](#tab/python)

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
