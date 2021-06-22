---
title: 对话事件
author: WashingtonKayaker
description: 如何处理来自自动程序的对话Microsoft Teams事件。
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 39d3a6d54b275fd6b9f28eb38b124435e9ba8bfd
ms.sourcegitcommit: 3d02dfc13331b28cffba42b39560cfeb1503abe2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2021
ms.locfileid: "53049042"
---
# <a name="conversation-events-in-your-teams-bot"></a><span data-ttu-id="afbec-103">Teams 智能机器人中的对话活动</span><span class="sxs-lookup"><span data-stu-id="afbec-103">Conversation events in your Teams bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="afbec-104">为用户生成对话机器人Microsoft Teams，可以使用对话事件。</span><span class="sxs-lookup"><span data-stu-id="afbec-104">When building your conversational bots for Microsoft Teams, you can work with conversation events.</span></span> <span data-ttu-id="afbec-105">Teams在自动程序处于活动状态的范围中发生的对话事件向机器人发送通知。</span><span class="sxs-lookup"><span data-stu-id="afbec-105">Teams sends notifications to your bot for conversation events that happen in scopes where your bot is active.</span></span> <span data-ttu-id="afbec-106">可以在代码中捕获这些事件，并执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="afbec-106">You can capture these events in your code and take the following actions:</span></span>

* <span data-ttu-id="afbec-107">将机器人添加到团队时触发欢迎消息。</span><span class="sxs-lookup"><span data-stu-id="afbec-107">Trigger a welcome message when your bot is added to a team.</span></span>
* <span data-ttu-id="afbec-108">在添加或删除新的团队成员时触发欢迎消息。</span><span class="sxs-lookup"><span data-stu-id="afbec-108">Trigger a welcome message when a new team member is added or removed.</span></span>
* <span data-ttu-id="afbec-109">创建、重命名或删除频道时触发通知。</span><span class="sxs-lookup"><span data-stu-id="afbec-109">Trigger a notification when a channel is created, renamed, or deleted.</span></span>
* <span data-ttu-id="afbec-110">当用户喜欢自动程序消息时。</span><span class="sxs-lookup"><span data-stu-id="afbec-110">When a bot message is liked by a user.</span></span>

## <a name="conversation-update-events"></a><span data-ttu-id="afbec-111">对话更新事件</span><span class="sxs-lookup"><span data-stu-id="afbec-111">Conversation update events</span></span>

<span data-ttu-id="afbec-112">可以使用对话更新事件提供更好的通知和更有效的自动程序操作。</span><span class="sxs-lookup"><span data-stu-id="afbec-112">You can use conversation update events to provide better notifications and more effective bot actions.</span></span>

> [!IMPORTANT]
> * <span data-ttu-id="afbec-113">你随时都可以添加新事件，并且机器人开始接收它们。</span><span class="sxs-lookup"><span data-stu-id="afbec-113">You can add new events any time and your bot begins to receive them.</span></span>
> * <span data-ttu-id="afbec-114">必须将机器人设计为接收意外事件。</span><span class="sxs-lookup"><span data-stu-id="afbec-114">You must design your bot to receive unexpected events.</span></span>
> * <span data-ttu-id="afbec-115">如果你使用的是 Bot Framework SDK，则自动自动响应你选择不处理 `200 - OK` 的任何事件。</span><span class="sxs-lookup"><span data-stu-id="afbec-115">If you are using the Bot Framework SDK, your bot automatically responds with a `200 - OK` to any events you choose not to handle.</span></span>

<span data-ttu-id="afbec-116">在下列任一 `conversationUpdate` 情况下，自动程序接收事件：</span><span class="sxs-lookup"><span data-stu-id="afbec-116">A bot receives a `conversationUpdate` event in either of the following cases:</span></span>

* <span data-ttu-id="afbec-117">自动程序已添加到对话中时。</span><span class="sxs-lookup"><span data-stu-id="afbec-117">When bot has been added to a conversation.</span></span>
* <span data-ttu-id="afbec-118">在对话中添加或删除其他成员。</span><span class="sxs-lookup"><span data-stu-id="afbec-118">Other members are added to or removed from a conversation.</span></span>
* <span data-ttu-id="afbec-119">对话元数据已更改。</span><span class="sxs-lookup"><span data-stu-id="afbec-119">Conversation metadata has changed.</span></span>

<span data-ttu-id="afbec-120">当机器人收到关于其所属团队的成员身份更新信息时，`conversationUpdate` 事件就会发送到机器人。</span><span class="sxs-lookup"><span data-stu-id="afbec-120">The `conversationUpdate` event is sent to your bot when it receives information on membership updates for teams where it has been added.</span></span> <span data-ttu-id="afbec-121">它还在首次为个人对话添加更新时接收更新。</span><span class="sxs-lookup"><span data-stu-id="afbec-121">It also receives an update when it has been added for the first time for personal conversations.</span></span>

<span data-ttu-id="afbec-122">下表显示了包含更多详细信息Teams对话更新事件的列表：</span><span class="sxs-lookup"><span data-stu-id="afbec-122">The following table shows a list of Teams conversation update events with more details:</span></span>

| <span data-ttu-id="afbec-123">已采取的操作</span><span class="sxs-lookup"><span data-stu-id="afbec-123">Action taken</span></span>        | <span data-ttu-id="afbec-124">EventType</span><span class="sxs-lookup"><span data-stu-id="afbec-124">EventType</span></span>         | <span data-ttu-id="afbec-125">调用的方法</span><span class="sxs-lookup"><span data-stu-id="afbec-125">Method called</span></span>              | <span data-ttu-id="afbec-126">说明</span><span class="sxs-lookup"><span data-stu-id="afbec-126">Description</span></span>                | <span data-ttu-id="afbec-127">范围</span><span class="sxs-lookup"><span data-stu-id="afbec-127">Scope</span></span> |
| ------------------- | ----------------- | -------------------------- | -------------------------- | ----- |
| <span data-ttu-id="afbec-128">已创建频道</span><span class="sxs-lookup"><span data-stu-id="afbec-128">Channel created</span></span>     | <span data-ttu-id="afbec-129">channelCreated</span><span class="sxs-lookup"><span data-stu-id="afbec-129">channelCreated</span></span>    | <span data-ttu-id="afbec-130">OnTeamsChannelCreatedAsync</span><span class="sxs-lookup"><span data-stu-id="afbec-130">OnTeamsChannelCreatedAsync</span></span> | <span data-ttu-id="afbec-131">[将创建一个通道](#channel-created)。</span><span class="sxs-lookup"><span data-stu-id="afbec-131">[A channel is created](#channel-created).</span></span> | <span data-ttu-id="afbec-132">团队</span><span class="sxs-lookup"><span data-stu-id="afbec-132">Team</span></span> |
| <span data-ttu-id="afbec-133">通道重命名</span><span class="sxs-lookup"><span data-stu-id="afbec-133">Channel renamed</span></span>     | <span data-ttu-id="afbec-134">channelRenamed</span><span class="sxs-lookup"><span data-stu-id="afbec-134">channelRenamed</span></span>    | <span data-ttu-id="afbec-135">OnTeamsChannelRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="afbec-135">OnTeamsChannelRenamedAsync</span></span> | <span data-ttu-id="afbec-136">[频道被重命名](#channel-renamed)。</span><span class="sxs-lookup"><span data-stu-id="afbec-136">[A channel is renamed](#channel-renamed).</span></span> | <span data-ttu-id="afbec-137">团队</span><span class="sxs-lookup"><span data-stu-id="afbec-137">Team</span></span> |
| <span data-ttu-id="afbec-138">频道已删除</span><span class="sxs-lookup"><span data-stu-id="afbec-138">Channel deleted</span></span>     | <span data-ttu-id="afbec-139">channelDeleted</span><span class="sxs-lookup"><span data-stu-id="afbec-139">channelDeleted</span></span>    | <span data-ttu-id="afbec-140">OnTeamsChannelDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="afbec-140">OnTeamsChannelDeletedAsync</span></span> | <span data-ttu-id="afbec-141">[频道被删除](#channel-deleted)。</span><span class="sxs-lookup"><span data-stu-id="afbec-141">[A channel is deleted](#channel-deleted).</span></span> | <span data-ttu-id="afbec-142">团队</span><span class="sxs-lookup"><span data-stu-id="afbec-142">Team</span></span> |
| <span data-ttu-id="afbec-143">已还原频道</span><span class="sxs-lookup"><span data-stu-id="afbec-143">Channel restored</span></span>    | <span data-ttu-id="afbec-144">channelRestored</span><span class="sxs-lookup"><span data-stu-id="afbec-144">channelRestored</span></span>    | <span data-ttu-id="afbec-145">OnTeamsChannelRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="afbec-145">OnTeamsChannelRestoredAsync</span></span> | <span data-ttu-id="afbec-146">[频道已还原](#channel-deleted)。</span><span class="sxs-lookup"><span data-stu-id="afbec-146">[A channel is restored](#channel-deleted).</span></span> | <span data-ttu-id="afbec-147">团队</span><span class="sxs-lookup"><span data-stu-id="afbec-147">Team</span></span> |
| <span data-ttu-id="afbec-148">添加的成员</span><span class="sxs-lookup"><span data-stu-id="afbec-148">Members added</span></span>   | <span data-ttu-id="afbec-149">membersAdded</span><span class="sxs-lookup"><span data-stu-id="afbec-149">membersAdded</span></span>   | <span data-ttu-id="afbec-150">OnTeamsMembersAddedAsync</span><span class="sxs-lookup"><span data-stu-id="afbec-150">OnTeamsMembersAddedAsync</span></span>   | <span data-ttu-id="afbec-151">[添加成员](#team-members-added)。</span><span class="sxs-lookup"><span data-stu-id="afbec-151">[A member is added](#team-members-added).</span></span> | <span data-ttu-id="afbec-152">所有</span><span class="sxs-lookup"><span data-stu-id="afbec-152">All</span></span> |
| <span data-ttu-id="afbec-153">已删除成员</span><span class="sxs-lookup"><span data-stu-id="afbec-153">Members removed</span></span> | <span data-ttu-id="afbec-154">membersRemoved</span><span class="sxs-lookup"><span data-stu-id="afbec-154">membersRemoved</span></span> | <span data-ttu-id="afbec-155">OnTeamsMembersRemovedAsync</span><span class="sxs-lookup"><span data-stu-id="afbec-155">OnTeamsMembersRemovedAsync</span></span> | <span data-ttu-id="afbec-156">[将删除成员](#team-members-removed)。</span><span class="sxs-lookup"><span data-stu-id="afbec-156">[A member is removed](#team-members-removed).</span></span> | <span data-ttu-id="afbec-157">groupChat and team</span><span class="sxs-lookup"><span data-stu-id="afbec-157">groupChat and team</span></span> |
| <span data-ttu-id="afbec-158">团队重命名</span><span class="sxs-lookup"><span data-stu-id="afbec-158">Team renamed</span></span>        | <span data-ttu-id="afbec-159">teamRenamed</span><span class="sxs-lookup"><span data-stu-id="afbec-159">teamRenamed</span></span>       | <span data-ttu-id="afbec-160">OnTeamsTeamRenamedAsync</span><span class="sxs-lookup"><span data-stu-id="afbec-160">OnTeamsTeamRenamedAsync</span></span>    | <span data-ttu-id="afbec-161">[团队重命名为](#team-renamed)。</span><span class="sxs-lookup"><span data-stu-id="afbec-161">[A team is renamed](#team-renamed).</span></span>       | <span data-ttu-id="afbec-162">团队</span><span class="sxs-lookup"><span data-stu-id="afbec-162">Team</span></span> |
| <span data-ttu-id="afbec-163">团队已删除</span><span class="sxs-lookup"><span data-stu-id="afbec-163">Team deleted</span></span>        | <span data-ttu-id="afbec-164">teamDeleted</span><span class="sxs-lookup"><span data-stu-id="afbec-164">teamDeleted</span></span>       | <span data-ttu-id="afbec-165">OnTeamsTeamDeletedAsync</span><span class="sxs-lookup"><span data-stu-id="afbec-165">OnTeamsTeamDeletedAsync</span></span>    | <span data-ttu-id="afbec-166">[团队已删除](#team-deleted)。</span><span class="sxs-lookup"><span data-stu-id="afbec-166">[A team is deleted](#team-deleted).</span></span>       | <span data-ttu-id="afbec-167">团队</span><span class="sxs-lookup"><span data-stu-id="afbec-167">Team</span></span> |
| <span data-ttu-id="afbec-168">团队存档</span><span class="sxs-lookup"><span data-stu-id="afbec-168">Team archived</span></span>        | <span data-ttu-id="afbec-169">teamArchived</span><span class="sxs-lookup"><span data-stu-id="afbec-169">teamArchived</span></span>       | <span data-ttu-id="afbec-170">OnTeamsTeamArchivedAsync</span><span class="sxs-lookup"><span data-stu-id="afbec-170">OnTeamsTeamArchivedAsync</span></span>    | <span data-ttu-id="afbec-171">[团队已存档](#team-archived)。</span><span class="sxs-lookup"><span data-stu-id="afbec-171">[A team is archived](#team-archived).</span></span>       | <span data-ttu-id="afbec-172">团队</span><span class="sxs-lookup"><span data-stu-id="afbec-172">Team</span></span> |
| <span data-ttu-id="afbec-173">团队未存档</span><span class="sxs-lookup"><span data-stu-id="afbec-173">Team unarchived</span></span>        | <span data-ttu-id="afbec-174">teamUnarchived</span><span class="sxs-lookup"><span data-stu-id="afbec-174">teamUnarchived</span></span>       | <span data-ttu-id="afbec-175">OnTeamsTeamUnarchivedAsync</span><span class="sxs-lookup"><span data-stu-id="afbec-175">OnTeamsTeamUnarchivedAsync</span></span>    | <span data-ttu-id="afbec-176">[团队未存档](#team-unarchived)。</span><span class="sxs-lookup"><span data-stu-id="afbec-176">[A team is unarchived](#team-unarchived).</span></span>       | <span data-ttu-id="afbec-177">团队</span><span class="sxs-lookup"><span data-stu-id="afbec-177">Team</span></span> |
| <span data-ttu-id="afbec-178">已还原团队</span><span class="sxs-lookup"><span data-stu-id="afbec-178">Team restored</span></span>        | <span data-ttu-id="afbec-179">teamRestored</span><span class="sxs-lookup"><span data-stu-id="afbec-179">teamRestored</span></span>      | <span data-ttu-id="afbec-180">OnTeamsTeamRestoredAsync</span><span class="sxs-lookup"><span data-stu-id="afbec-180">OnTeamsTeamRestoredAsync</span></span>    | [<span data-ttu-id="afbec-181">已还原团队</span><span class="sxs-lookup"><span data-stu-id="afbec-181">A team is restored</span></span>](#team-restored)       | <span data-ttu-id="afbec-182">团队</span><span class="sxs-lookup"><span data-stu-id="afbec-182">Team</span></span> |

### <a name="channel-created"></a><span data-ttu-id="afbec-183">已创建频道</span><span class="sxs-lookup"><span data-stu-id="afbec-183">Channel created</span></span>

<span data-ttu-id="afbec-184">只要在安装了自动程序的团队中创建了新频道，就会将频道创建事件发送给机器人。</span><span class="sxs-lookup"><span data-stu-id="afbec-184">The channel created event is sent to your bot whenever a new channel is created in a team where your bot is installed.</span></span>

<span data-ttu-id="afbec-185">以下代码显示了通道创建事件的示例：</span><span class="sxs-lookup"><span data-stu-id="afbec-185">The following code shows an example of channel created event:</span></span>

# <a name="c"></a>[<span data-ttu-id="afbec-186">C#</span><span class="sxs-lookup"><span data-stu-id="afbec-186">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel created");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="afbec-187">TypeScript</span><span class="sxs-lookup"><span data-stu-id="afbec-187">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afbec-188">JSON</span><span class="sxs-lookup"><span data-stu-id="afbec-188">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afbec-189">Python</span><span class="sxs-lookup"><span data-stu-id="afbec-189">Python</span></span>](#tab/python)

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

---

### <a name="channel-renamed"></a><span data-ttu-id="afbec-190">通道重命名</span><span class="sxs-lookup"><span data-stu-id="afbec-190">Channel renamed</span></span>

<span data-ttu-id="afbec-191">只要频道在安装自动程序的团队中重命名，频道重命名事件就会发送到机器人。</span><span class="sxs-lookup"><span data-stu-id="afbec-191">The channel renamed event is sent to your bot whenever a channel is renamed in a team where your bot is installed.</span></span>

<span data-ttu-id="afbec-192">以下代码显示了通道重命名事件的示例：</span><span class="sxs-lookup"><span data-stu-id="afbec-192">The following code shows an example of channel renamed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="afbec-193">C#</span><span class="sxs-lookup"><span data-stu-id="afbec-193">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the new Channel name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="afbec-194">TypeScript</span><span class="sxs-lookup"><span data-stu-id="afbec-194">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afbec-195">JSON</span><span class="sxs-lookup"><span data-stu-id="afbec-195">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afbec-196">Python</span><span class="sxs-lookup"><span data-stu-id="afbec-196">Python</span></span>](#tab/python)

```python
async def on_teams_channel_renamed(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new channel name is {channel_info.name}")
    )
```

---

### <a name="channel-deleted"></a><span data-ttu-id="afbec-197">频道已删除</span><span class="sxs-lookup"><span data-stu-id="afbec-197">Channel deleted</span></span>

<span data-ttu-id="afbec-198">只要在安装了自动程序的团队中删除频道，频道删除事件就会发送给机器人。</span><span class="sxs-lookup"><span data-stu-id="afbec-198">The channel deleted event is sent to your bot whenever a channel is deleted in a team where your bot is installed.</span></span>

<span data-ttu-id="afbec-199">以下代码显示了频道删除事件的示例：</span><span class="sxs-lookup"><span data-stu-id="afbec-199">The following code shows an example of channel deleted event:</span></span>

# <a name="c"></a>[<span data-ttu-id="afbec-200">C#</span><span class="sxs-lookup"><span data-stu-id="afbec-200">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel deleted");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="afbec-201">TypeScript</span><span class="sxs-lookup"><span data-stu-id="afbec-201">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afbec-202">JSON</span><span class="sxs-lookup"><span data-stu-id="afbec-202">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afbec-203">Python</span><span class="sxs-lookup"><span data-stu-id="afbec-203">Python</span></span>](#tab/python)

```python
async def on_teams_channel_deleted(
    self, channel_info: ChannelInfo, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The deleted channel is {channel_info.name}")
    )
```

---

### <a name="channel-restored"></a><span data-ttu-id="afbec-204">已还原频道</span><span class="sxs-lookup"><span data-stu-id="afbec-204">Channel restored</span></span>

<span data-ttu-id="afbec-205">只要在已安装自动程序的团队中还原以前删除的频道，就会将频道还原事件发送给机器人。</span><span class="sxs-lookup"><span data-stu-id="afbec-205">The channel restored event is sent to your bot whenever a channel that was previously deleted is restored in a team where your bot is already installed.</span></span>

<span data-ttu-id="afbec-206">以下代码显示了通道还原事件的示例：</span><span class="sxs-lookup"><span data-stu-id="afbec-206">The following code shows an example of channel restored event:</span></span>

# <a name="c"></a>[<span data-ttu-id="afbec-207">C#</span><span class="sxs-lookup"><span data-stu-id="afbec-207">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsChannelRestoredAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{channelInfo.Name} is the Channel restored.");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="afbec-208">TypeScript</span><span class="sxs-lookup"><span data-stu-id="afbec-208">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afbec-209">JSON</span><span class="sxs-lookup"><span data-stu-id="afbec-209">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afbec-210">Python</span><span class="sxs-lookup"><span data-stu-id="afbec-210">Python</span></span>](#tab/python)

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

---

### <a name="team-members-added"></a><span data-ttu-id="afbec-211">添加了工作组成员</span><span class="sxs-lookup"><span data-stu-id="afbec-211">Team members added</span></span>

<span data-ttu-id="afbec-212">`teamMemberAdded`该事件在首次添加到对话时发送到机器人。</span><span class="sxs-lookup"><span data-stu-id="afbec-212">The `teamMemberAdded` event is sent to your bot the first time it is added to a conversation.</span></span> <span data-ttu-id="afbec-213">每次将新用户添加到安装自动程序的团队或群聊时，都会向机器人发送该事件。</span><span class="sxs-lookup"><span data-stu-id="afbec-213">The event is sent to your bot every time a new user is added to a team or group chat where your bot is installed.</span></span> <span data-ttu-id="afbec-214">ID 为 ID 的用户信息对于自动程序是唯一的，可以缓存此信息供服务将来使用，例如向特定用户发送消息。</span><span class="sxs-lookup"><span data-stu-id="afbec-214">The user information that is ID is unique for your bot and can be cached for future use by your service, such as sending a message to a specific user.</span></span>

<span data-ttu-id="afbec-215">以下代码显示了团队成员添加事件的示例：</span><span class="sxs-lookup"><span data-stu-id="afbec-215">The following code shows an example of team members added event:</span></span>

# <a name="c"></a>[<span data-ttu-id="afbec-216">C#</span><span class="sxs-lookup"><span data-stu-id="afbec-216">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="afbec-217">TypeScript</span><span class="sxs-lookup"><span data-stu-id="afbec-217">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afbec-218">JSON</span><span class="sxs-lookup"><span data-stu-id="afbec-218">JSON</span></span>](#tab/json)

<span data-ttu-id="afbec-219">这是自动程序在添加到团队时收到的消息。</span><span class="sxs-lookup"><span data-stu-id="afbec-219">This is the message your bot receives when the bot is added to a team.</span></span>

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

<span data-ttu-id="afbec-220">这是自动程序在将机器人添加到一对一聊天时收到的消息。</span><span class="sxs-lookup"><span data-stu-id="afbec-220">This is the message your bot receives when the bot is added to a one-to-one chat.</span></span>

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

# <a name="python"></a>[<span data-ttu-id="afbec-221">Python</span><span class="sxs-lookup"><span data-stu-id="afbec-221">Python</span></span>](#tab/python)

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

---

### <a name="team-members-removed"></a><span data-ttu-id="afbec-222">已删除团队成员</span><span class="sxs-lookup"><span data-stu-id="afbec-222">Team members removed</span></span>

<span data-ttu-id="afbec-223">如果 `teamMemberRemoved` 从团队中删除了事件，则此事件将发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="afbec-223">The `teamMemberRemoved` event is sent to your bot if it is removed from a team.</span></span> <span data-ttu-id="afbec-224">每当从自动程序是成员的团队中删除任何用户时，都会将事件发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="afbec-224">The event is sent to your bot every time any user is removed from a team where your bot is a member.</span></span> <span data-ttu-id="afbec-225">若要确定删除的新增成员是自动程序本身还是用户，请检查 `Activity` 的对象 `turnContext` 。</span><span class="sxs-lookup"><span data-stu-id="afbec-225">To determine if the new member removed was the bot itself or a user, check the `Activity` object of the `turnContext`.</span></span>  <span data-ttu-id="afbec-226">如果对象的字段与对象的字段相同，则删除的成员是自动程序 `Id` `MembersRemoved` `Id` `Recipient` ，否则它是用户。</span><span class="sxs-lookup"><span data-stu-id="afbec-226">If the `Id` field of the `MembersRemoved` object is the same as the `Id` field of the `Recipient` object, then the member removed is the bot, else it is a user.</span></span> <span data-ttu-id="afbec-227">自动程序 `Id` 通常为 `28:<MicrosoftAppId>` 。</span><span class="sxs-lookup"><span data-stu-id="afbec-227">The bot's `Id` generally is `28:<MicrosoftAppId>`.</span></span>

> [!NOTE]
> <span data-ttu-id="afbec-228">从租户中永久删除用户时， `membersRemoved conversationUpdate` 将触发事件。</span><span class="sxs-lookup"><span data-stu-id="afbec-228">When a user is permanently deleted from a tenant, `membersRemoved conversationUpdate` event is triggered.</span></span>

<span data-ttu-id="afbec-229">以下代码显示了工作组成员删除事件的示例：</span><span class="sxs-lookup"><span data-stu-id="afbec-229">The following code shows an example of team members removed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="afbec-230">C#</span><span class="sxs-lookup"><span data-stu-id="afbec-230">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="afbec-231">TypeScript</span><span class="sxs-lookup"><span data-stu-id="afbec-231">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afbec-232">JSON</span><span class="sxs-lookup"><span data-stu-id="afbec-232">JSON</span></span>](#tab/json)

<span data-ttu-id="afbec-233">以下有效负载示例中的对象基于将成员添加到团队（而不是群组聊天）或启动新的一对 `channelData` 一对话：</span><span class="sxs-lookup"><span data-stu-id="afbec-233">The `channelData` object in the following payload example is based on adding a member to a team rather than a group chat, or initiating a new one-to-one conversation:</span></span>

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


# <a name="python"></a>[<span data-ttu-id="afbec-234">Python</span><span class="sxs-lookup"><span data-stu-id="afbec-234">Python</span></span>](#tab/python)

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

---

### <a name="team-renamed"></a><span data-ttu-id="afbec-235">团队重命名</span><span class="sxs-lookup"><span data-stu-id="afbec-235">Team renamed</span></span>

<span data-ttu-id="afbec-236">当自动程序位于的团队重命名时，将会收到通知。</span><span class="sxs-lookup"><span data-stu-id="afbec-236">Your bot is notified when the team it is in has been renamed.</span></span> <span data-ttu-id="afbec-237">它接收 `conversationUpdate` 对象中的 `eventType.teamRenamed` 事件 `channelData` 。</span><span class="sxs-lookup"><span data-stu-id="afbec-237">It receives a `conversationUpdate` event with `eventType.teamRenamed` in the `channelData` object.</span></span>

<span data-ttu-id="afbec-238">以下代码显示了团队重命名事件的示例：</span><span class="sxs-lookup"><span data-stu-id="afbec-238">The following code shows an example of team renamed event:</span></span>

# <a name="c"></a>[<span data-ttu-id="afbec-239">C#</span><span class="sxs-lookup"><span data-stu-id="afbec-239">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the new Team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="afbec-240">TypeScript</span><span class="sxs-lookup"><span data-stu-id="afbec-240">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afbec-241">JSON</span><span class="sxs-lookup"><span data-stu-id="afbec-241">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afbec-242">Python</span><span class="sxs-lookup"><span data-stu-id="afbec-242">Python</span></span>](#tab/python)

```python
async def on_teams_team_renamed(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The new team name is {team_info.name}")
    )
```

---

### <a name="team-deleted"></a><span data-ttu-id="afbec-243">团队已删除</span><span class="sxs-lookup"><span data-stu-id="afbec-243">Team deleted</span></span>

<span data-ttu-id="afbec-244">当自动程序位于的团队被删除时，将会收到通知。</span><span class="sxs-lookup"><span data-stu-id="afbec-244">Your bot is notified when the team it is in has been deleted.</span></span> <span data-ttu-id="afbec-245">它接收 `conversationUpdate` 对象中的 `eventType.teamDeleted` 事件 `channelData` 。</span><span class="sxs-lookup"><span data-stu-id="afbec-245">It receives a `conversationUpdate` event with `eventType.teamDeleted` in the `channelData` object.</span></span>

<span data-ttu-id="afbec-246">以下代码显示了团队已删除事件的示例：</span><span class="sxs-lookup"><span data-stu-id="afbec-246">The following code shows an example of team deleted event:</span></span>

# <a name="c"></a>[<span data-ttu-id="afbec-247">C#</span><span class="sxs-lookup"><span data-stu-id="afbec-247">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamDeletedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    //handle delete event
}
```

# <a name="typescript"></a>[<span data-ttu-id="afbec-248">TypeScript</span><span class="sxs-lookup"><span data-stu-id="afbec-248">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afbec-249">JSON</span><span class="sxs-lookup"><span data-stu-id="afbec-249">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afbec-250">Python</span><span class="sxs-lookup"><span data-stu-id="afbec-250">Python</span></span>](#tab/python)

```python
async def on_teams_team_deleted(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    //handle delete event
    )
```

---

### <a name="team-restored"></a><span data-ttu-id="afbec-251">已还原团队</span><span class="sxs-lookup"><span data-stu-id="afbec-251">Team restored</span></span>

<span data-ttu-id="afbec-252">删除团队后，机器人会收到通知。</span><span class="sxs-lookup"><span data-stu-id="afbec-252">The bot receives a notification when a team is restored after being deleted.</span></span> <span data-ttu-id="afbec-253">它接收 `conversationUpdate` 对象中的 `eventType.teamrestored` 事件 `channelData` 。</span><span class="sxs-lookup"><span data-stu-id="afbec-253">It receives a `conversationUpdate` event with `eventType.teamrestored` in the `channelData` object.</span></span>

<span data-ttu-id="afbec-254">以下代码显示了团队还原事件的示例：</span><span class="sxs-lookup"><span data-stu-id="afbec-254">The following code shows an example of team restored event:</span></span>

# <a name="c"></a>[<span data-ttu-id="afbec-255">C#</span><span class="sxs-lookup"><span data-stu-id="afbec-255">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamrestoredAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="afbec-256">TypeScript</span><span class="sxs-lookup"><span data-stu-id="afbec-256">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afbec-257">JSON</span><span class="sxs-lookup"><span data-stu-id="afbec-257">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afbec-258">Python</span><span class="sxs-lookup"><span data-stu-id="afbec-258">Python</span></span>](#tab/python)

```python
async def on_teams_team_restored(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

---

### <a name="team-archived"></a><span data-ttu-id="afbec-259">团队存档</span><span class="sxs-lookup"><span data-stu-id="afbec-259">Team archived</span></span>

<span data-ttu-id="afbec-260">自动程序在存档安装它的团队时收到通知。</span><span class="sxs-lookup"><span data-stu-id="afbec-260">The bot receives a notification when the team it is installed in is archived.</span></span> <span data-ttu-id="afbec-261">它接收 `conversationUpdate` 对象中的 `eventType.teamarchived` 事件 `channelData` 。</span><span class="sxs-lookup"><span data-stu-id="afbec-261">It receives a `conversationUpdate` event with `eventType.teamarchived` in the `channelData` object.</span></span>

<span data-ttu-id="afbec-262">以下代码显示了团队存档事件的示例：</span><span class="sxs-lookup"><span data-stu-id="afbec-262">The following code shows an example of team archived event:</span></span>

# <a name="c"></a>[<span data-ttu-id="afbec-263">C#</span><span class="sxs-lookup"><span data-stu-id="afbec-263">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamArchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="afbec-264">TypeScript</span><span class="sxs-lookup"><span data-stu-id="afbec-264">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afbec-265">JSON</span><span class="sxs-lookup"><span data-stu-id="afbec-265">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afbec-266">Python</span><span class="sxs-lookup"><span data-stu-id="afbec-266">Python</span></span>](#tab/python)

```python
async def on_teams_team_archived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

---


### <a name="team-unarchived"></a><span data-ttu-id="afbec-267">团队未存档</span><span class="sxs-lookup"><span data-stu-id="afbec-267">Team unarchived</span></span>

<span data-ttu-id="afbec-268">自动程序在安装它的团队未存档时收到通知。</span><span class="sxs-lookup"><span data-stu-id="afbec-268">The bot receives a notification when the team it is installed in is unarchived.</span></span> <span data-ttu-id="afbec-269">它接收 `conversationUpdate` 对象中的 `eventType.teamUnarchived` 事件 `channelData` 。</span><span class="sxs-lookup"><span data-stu-id="afbec-269">It receives a `conversationUpdate` event with `eventType.teamUnarchived` in the `channelData` object.</span></span>

<span data-ttu-id="afbec-270">以下代码显示了团队未存档事件的示例：</span><span class="sxs-lookup"><span data-stu-id="afbec-270">The following code shows an example of team unarchived event:</span></span>

# <a name="c"></a>[<span data-ttu-id="afbec-271">C#</span><span class="sxs-lookup"><span data-stu-id="afbec-271">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task OnTeamsTeamUnarchivedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
{
    var heroCard = new HeroCard(text: $"{teamInfo.Name} is the team name");
    await turnContext.SendActivityAsync(MessageFactory.Attachment(heroCard.ToAttachment()), cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="afbec-272">TypeScript</span><span class="sxs-lookup"><span data-stu-id="afbec-272">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afbec-273">JSON</span><span class="sxs-lookup"><span data-stu-id="afbec-273">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afbec-274">Python</span><span class="sxs-lookup"><span data-stu-id="afbec-274">Python</span></span>](#tab/python)

```python
async def on_teams_team_unarchived(
    self, team_info: TeamInfo, turn_context: TurnContext
):
    return await turn_context.send_activity(
        MessageFactory.text(f"The team name is {team_info.name}")
    )
```

---

<span data-ttu-id="afbec-275">现在，你已使用对话更新事件，可以了解对消息的不同反应所发生的消息反应事件。</span><span class="sxs-lookup"><span data-stu-id="afbec-275">Now that you have worked with the conversation update events, you can understand the message reaction events that occur for different reactions to a message.</span></span>

## <a name="message-reaction-events"></a><span data-ttu-id="afbec-276">邮件反应事件</span><span class="sxs-lookup"><span data-stu-id="afbec-276">Message reaction events</span></span>

<span data-ttu-id="afbec-277">当用户 `messageReaction` 向自动程序发送的消息添加或删除反应时，将发送该事件。</span><span class="sxs-lookup"><span data-stu-id="afbec-277">The `messageReaction` event is sent when a user adds or removes reactions to a message which was sent by your bot.</span></span> <span data-ttu-id="afbec-278">`replyToId`包含邮件的 ID， `Type` 并且 是文本格式的反应类型。</span><span class="sxs-lookup"><span data-stu-id="afbec-278">The `replyToId` contains the ID of the message, and the `Type` is the type of reaction in text format.</span></span> <span data-ttu-id="afbec-279">反应类型包括笑人、心声、笑人、喜欢、沮丧和意外。</span><span class="sxs-lookup"><span data-stu-id="afbec-279">The types of reactions include angry, heart, laugh, like, sad, and surprised.</span></span> <span data-ttu-id="afbec-280">此事件不包含原始邮件的内容。</span><span class="sxs-lookup"><span data-stu-id="afbec-280">This event does not contain the contents of the original message.</span></span> <span data-ttu-id="afbec-281">如果处理对消息的反应对自动程序很重要，则必须在发送邮件时存储这些消息。</span><span class="sxs-lookup"><span data-stu-id="afbec-281">If processing reactions to your messages is important for your bot, you must store the messages when you send them.</span></span> <span data-ttu-id="afbec-282">下表提供了有关事件类型和有效负载对象的信息：</span><span class="sxs-lookup"><span data-stu-id="afbec-282">The following table provides more information about the event type and payload objects:</span></span>

| <span data-ttu-id="afbec-283">EventType</span><span class="sxs-lookup"><span data-stu-id="afbec-283">EventType</span></span>       | <span data-ttu-id="afbec-284">Payload 对象</span><span class="sxs-lookup"><span data-stu-id="afbec-284">Payload object</span></span>   | <span data-ttu-id="afbec-285">说明</span><span class="sxs-lookup"><span data-stu-id="afbec-285">Description</span></span>                                                             | <span data-ttu-id="afbec-286">范围</span><span class="sxs-lookup"><span data-stu-id="afbec-286">Scope</span></span> |
| --------------- | ---------------- | ----------------------------------------------------------------------- | ----- |
| <span data-ttu-id="afbec-287">messageReaction</span><span class="sxs-lookup"><span data-stu-id="afbec-287">messageReaction</span></span> | <span data-ttu-id="afbec-288">reactionsAdded</span><span class="sxs-lookup"><span data-stu-id="afbec-288">reactionsAdded</span></span>   | <span data-ttu-id="afbec-289">[向自动程序消息添加了反应](#reactions-added-to-bot-message)。</span><span class="sxs-lookup"><span data-stu-id="afbec-289">[Reactions added to bot message](#reactions-added-to-bot-message).</span></span>           | <span data-ttu-id="afbec-290">所有</span><span class="sxs-lookup"><span data-stu-id="afbec-290">All</span></span>   |
| <span data-ttu-id="afbec-291">messageReaction</span><span class="sxs-lookup"><span data-stu-id="afbec-291">messageReaction</span></span> | <span data-ttu-id="afbec-292">将removed</span><span class="sxs-lookup"><span data-stu-id="afbec-292">reactionsRemoved</span></span> | <span data-ttu-id="afbec-293">[从自动程序消息中删除了反应](#reactions-removed-from-bot-message)。</span><span class="sxs-lookup"><span data-stu-id="afbec-293">[Reactions removed from bot message](#reactions-removed-from-bot-message).</span></span> | <span data-ttu-id="afbec-294">所有</span><span class="sxs-lookup"><span data-stu-id="afbec-294">All</span></span> |

### <a name="reactions-added-to-bot-message"></a><span data-ttu-id="afbec-295">添加到自动程序消息的反应</span><span class="sxs-lookup"><span data-stu-id="afbec-295">Reactions added to bot message</span></span>

<span data-ttu-id="afbec-296">以下代码显示了对自动程序消息的反应示例：</span><span class="sxs-lookup"><span data-stu-id="afbec-296">The following code shows an example of reactions to a bot message:</span></span>

# <a name="c"></a>[<span data-ttu-id="afbec-297">C#</span><span class="sxs-lookup"><span data-stu-id="afbec-297">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="afbec-298">TypeScript</span><span class="sxs-lookup"><span data-stu-id="afbec-298">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afbec-299">JSON</span><span class="sxs-lookup"><span data-stu-id="afbec-299">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afbec-300">Python</span><span class="sxs-lookup"><span data-stu-id="afbec-300">Python</span></span>](#tab/python)

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

---

### <a name="reactions-removed-from-bot-message"></a><span data-ttu-id="afbec-301">从自动程序消息中删除的反应</span><span class="sxs-lookup"><span data-stu-id="afbec-301">Reactions removed from bot message</span></span>

<span data-ttu-id="afbec-302">以下代码显示了从自动程序消息中删除的反应示例：</span><span class="sxs-lookup"><span data-stu-id="afbec-302">The following code shows an example of reactions removed from bot message:</span></span>

# <a name="c"></a>[<span data-ttu-id="afbec-303">C#</span><span class="sxs-lookup"><span data-stu-id="afbec-303">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="afbec-304">TypeScript</span><span class="sxs-lookup"><span data-stu-id="afbec-304">TypeScript</span></span>](#tab/typescript)

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

# <a name="json"></a>[<span data-ttu-id="afbec-305">JSON</span><span class="sxs-lookup"><span data-stu-id="afbec-305">JSON</span></span>](#tab/json)

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

# <a name="python"></a>[<span data-ttu-id="afbec-306">Python</span><span class="sxs-lookup"><span data-stu-id="afbec-306">Python</span></span>](#tab/python)

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

---

## <a name="installation-update-event"></a><span data-ttu-id="afbec-307">安装更新事件</span><span class="sxs-lookup"><span data-stu-id="afbec-307">Installation update event</span></span>

<span data-ttu-id="afbec-308">当您将机器人 `installationUpdate` 安装到对话线程时，机器人会收到一个事件。</span><span class="sxs-lookup"><span data-stu-id="afbec-308">The bot receives an `installationUpdate` event when you install a bot to a conversation thread.</span></span> <span data-ttu-id="afbec-309">从线程卸载自动程序也会触发事件。</span><span class="sxs-lookup"><span data-stu-id="afbec-309">Uninstallation of the bot from the thread also triggers the event.</span></span> <span data-ttu-id="afbec-310">安装自动程序时，事件的操作字段设置为 *添加*，当卸载机器人时，操作字段设置为 *删除*。 </span><span class="sxs-lookup"><span data-stu-id="afbec-310">On installing a bot, the **action** field in the event is set to *add*, and when the bot is uninstalled the **action** field is set to *remove*.</span></span>
 
> [!NOTE]
> <span data-ttu-id="afbec-311">升级应用程序，然后添加或删除自动程序时，该操作还会触发 `installationUpdate` 事件。</span><span class="sxs-lookup"><span data-stu-id="afbec-311">When you upgrade an application, and then add or remove a bot, the action also triggers the `installationUpdate` event.</span></span> <span data-ttu-id="afbec-312">如果 **添加** 自动程序或删除自动 *程序*，则操作字段将设置为"添加升级"。</span><span class="sxs-lookup"><span data-stu-id="afbec-312">The **action** field is set to *add-upgrade* if you add a bot or *remove-upgrade* if you remove a bot.</span></span> 

> [!IMPORTANT]
> <span data-ttu-id="afbec-313">安装更新事件目前为开发人员预览版，并将于 2021 年 3 月 (GA) 通用版本。</span><span class="sxs-lookup"><span data-stu-id="afbec-313">Installation update events are in developer preview today and will be Generally Available (GA) in March 2021.</span></span> <span data-ttu-id="afbec-314">To see the installation update events， you can move your Teams client to public developer preview， and add your app personally or to a team or a chat.</span><span class="sxs-lookup"><span data-stu-id="afbec-314">To see the installation update events, you can move your Teams client to public developer preview, and add your app personally or to a team or a chat.</span></span>

### <a name="install-update-event"></a><span data-ttu-id="afbec-315">安装更新事件</span><span class="sxs-lookup"><span data-stu-id="afbec-315">Install update event</span></span>
<span data-ttu-id="afbec-316">使用 `installationUpdate` 事件在安装时从机器人发送介绍性消息。</span><span class="sxs-lookup"><span data-stu-id="afbec-316">Use the `installationUpdate` event to send an introductory message from your bot on installation.</span></span> <span data-ttu-id="afbec-317">此事件有助于满足隐私和数据保留要求。</span><span class="sxs-lookup"><span data-stu-id="afbec-317">This event helps you to meet your privacy and data retention requirements.</span></span> <span data-ttu-id="afbec-318">还可以在卸载机器人时清理和删除用户或线程数据。</span><span class="sxs-lookup"><span data-stu-id="afbec-318">You can also clean up and delete user or thread data when the bot is uninstalled.</span></span>

# <a name="c"></a>[<span data-ttu-id="afbec-319">C#</span><span class="sxs-lookup"><span data-stu-id="afbec-319">C#</span></span>](#tab/dotnet)

```csharp
protected override async Task
OnInstallationUpdateActivityAsync(ITurnContext<IInstallationUpdateActivity> turnContext, CancellationToken cancellationToken) {
var activity = turnContext.Activity; if
(string.Equals(activity.Action, "Add",
StringComparison.InvariantCultureIgnoreCase)) {
// TO:DO Installation workflow }
else
{ // TO:DO Uninstallation workflow
} return; }
```

<span data-ttu-id="afbec-320">还可以将添加或删除方案的专用处理程序用作捕获事件的替代方法。</span><span class="sxs-lookup"><span data-stu-id="afbec-320">You can also use a dedicated handler for *add* or *remove* scenarios as an alternative method to capture an event.</span></span>

```csharp
protected override async Task
OnInstallationUpdateAddAsync(ITurnContext<IInstallationUpdateActivity>
turnContext, CancellationToken cancellationToken) {
// TO:DO Installation workflow return;
}
```

# <a name="typescript"></a>[<span data-ttu-id="afbec-321">TypeScript</span><span class="sxs-lookup"><span data-stu-id="afbec-321">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="afbec-322">不可用</span><span class="sxs-lookup"><span data-stu-id="afbec-322">Not available</span></span>

# <a name="json"></a>[<span data-ttu-id="afbec-323">JSON</span><span class="sxs-lookup"><span data-stu-id="afbec-323">JSON</span></span>](#tab/json)

```json
{ 
  "action": "add", 
  "type": "installationUpdate", 
  "timestamp": "2020-10-20T22:08:07.869Z", 
  "id": "f:3033745319439849398", 
  "channelId": "msteams", 
  "serviceUrl": "https://smba.trafficmanager.net/amer/", 
  "from": { 
    "id": "sample id", 
    "aadObjectId": "sample AAD Object ID" 
  },
  "conversation": { 
    "isGroup": true, 
    "conversationType": "channel", 
    "tenantId": "sample tenant ID", 
    "id": "sample conversation Id@thread.skype" 
  }, 

  "recipient": { 
    "id": "sample reciepent bot ID", 
    "name": "bot name" 
  }, 
  "entities": [ 
    { 
      "locale": "en", 
      "platform": "Windows", 
      "type": "clientInfo" 
    } 
  ], 
  "channelData": { 
    "settings": { 
      "selectedChannel": { 
        "id": "sample channel ID@thread.skype" 
      } 
    }, 
    "channel": { 
      "id": "sample channel ID" 
    }, 
    "team": { 
      "id": "sample team ID" 
    }, 
    "tenant": { 
      "id": "sample tenant ID" 
    }, 
    "source": { 
      "name": "message" 
    } 
  }, 
  "locale": "en" 
}
```

# <a name="python"></a>[<span data-ttu-id="afbec-324">Python</span><span class="sxs-lookup"><span data-stu-id="afbec-324">Python</span></span>](#tab/python)

<span data-ttu-id="afbec-325">不可用</span><span class="sxs-lookup"><span data-stu-id="afbec-325">Not available</span></span>

---

## <a name="uninstall-behavior-for-personal-app-with-bot"></a><span data-ttu-id="afbec-326">使用自动程序卸载个人应用的行为</span><span class="sxs-lookup"><span data-stu-id="afbec-326">Uninstall behavior for personal app with bot</span></span>

> [!NOTE]
> <span data-ttu-id="afbec-327">使用自动程序的个人应用的卸载行为当前仅适用于公共开发人员 [预览版](../../../resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="afbec-327">Uninstall behavior for personal app with bot is currently available only in [public developer preview](../../../resources/dev-preview/developer-preview-intro.md).</span></span>

<span data-ttu-id="afbec-328">卸载应用时，也会卸载自动程序。</span><span class="sxs-lookup"><span data-stu-id="afbec-328">When you uninstall an app, the bot is also uninstalled.</span></span> <span data-ttu-id="afbec-329">当用户向你的应用发送邮件时，他们会收到 403 响应代码。</span><span class="sxs-lookup"><span data-stu-id="afbec-329">When a user sends a message to your app, they receive a 403 response code.</span></span> <span data-ttu-id="afbec-330">自动程序会收到由机器人发布的新消息的 403 响应代码。</span><span class="sxs-lookup"><span data-stu-id="afbec-330">Your bot receives a 403 response code for new messages posted by your bot.</span></span> <span data-ttu-id="afbec-331">现在，具有 Teams 和 groupChat 作用域的个人作用域中的聊天机器人的帖子卸载行为已保持一致。</span><span class="sxs-lookup"><span data-stu-id="afbec-331">The post uninstall behavior for bots in the personal scope with the Teams and groupChat scopes are now aligned.</span></span> <span data-ttu-id="afbec-332">卸载应用后，你无法发送或接收邮件。</span><span class="sxs-lookup"><span data-stu-id="afbec-332">You cannot send or receive messages after an app has been uninstalled.</span></span>

<img src="~/assets/images/bots/uninstallbot.png" alt="Uninstall event" width="900" height="900"/>

## <a name="event-handling-for-install-and-uninstall-events"></a><span data-ttu-id="afbec-333">安装和卸载事件的事件处理</span><span class="sxs-lookup"><span data-stu-id="afbec-333">Event handling for install and uninstall events</span></span>

<span data-ttu-id="afbec-334">使用这些安装和卸载事件时，在一些实例中，自动程序在从用户接收意外事件时Teams。</span><span class="sxs-lookup"><span data-stu-id="afbec-334">When you use these install and uninstall events, there are some instances where bots give exceptions on receiving unexpected events from Teams.</span></span> <span data-ttu-id="afbec-335">在下列情况下会出现此情况：</span><span class="sxs-lookup"><span data-stu-id="afbec-335">This occurs in the following cases:</span></span>

* <span data-ttu-id="afbec-336">无需使用 SDK Microsoft Bot Framework自动程序，因此机器人在收到意外事件时出现异常。</span><span class="sxs-lookup"><span data-stu-id="afbec-336">You build your bot without the Microsoft Bot Framework SDK, and as a result the bot gives an exception on receiving an unexpected event.</span></span>
* <span data-ttu-id="afbec-337">使用 Microsoft Bot Framework SDK 生成自动程序，并选择通过替代基本事件句柄来更改默认事件行为。</span><span class="sxs-lookup"><span data-stu-id="afbec-337">You build your bot with the Microsoft Bot Framework SDK, and you select to alter the default event behavior by overriding the base event handle.</span></span>

<span data-ttu-id="afbec-338">了解以后可以随时添加新事件，并且机器人开始接收它们，了解这一点很重要。</span><span class="sxs-lookup"><span data-stu-id="afbec-338">It is important to know that new events can be added anytime in the future and your bot begins to receive them.</span></span> <span data-ttu-id="afbec-339">因此，您必须针对接收意外事件的可能性进行设计。</span><span class="sxs-lookup"><span data-stu-id="afbec-339">So you must design for the possibility of receiving unexpected events.</span></span> <span data-ttu-id="afbec-340">如果你使用的是 Bot Framework SDK，则自动程序会自动对未选择处理的任何事件进行 200 – OK 响应。</span><span class="sxs-lookup"><span data-stu-id="afbec-340">If you are using the Bot Framework SDK, your bot automatically responds with a 200 – OK to any events you do not choose to handle.</span></span>

## <a name="code-sample"></a><span data-ttu-id="afbec-341">代码示例</span><span class="sxs-lookup"><span data-stu-id="afbec-341">Code sample</span></span>

| <span data-ttu-id="afbec-342">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="afbec-342">**Sample name**</span></span> | <span data-ttu-id="afbec-343">**描述**</span><span class="sxs-lookup"><span data-stu-id="afbec-343">**Description**</span></span> | <span data-ttu-id="afbec-344">**.NET**</span><span class="sxs-lookup"><span data-stu-id="afbec-344">**.NET**</span></span> | <span data-ttu-id="afbec-345">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="afbec-345">**Node.js**</span></span> | <span data-ttu-id="afbec-346">**Python**</span><span class="sxs-lookup"><span data-stu-id="afbec-346">**Python**</span></span> |
|----------|-----------------|----------|
| <span data-ttu-id="afbec-347">对话机器人</span><span class="sxs-lookup"><span data-stu-id="afbec-347">Conversation bot</span></span> | <span data-ttu-id="afbec-348">机器人对话事件的示例代码。</span><span class="sxs-lookup"><span data-stu-id="afbec-348">Sample code for bots conversation events.</span></span> | [<span data-ttu-id="afbec-349">View</span><span class="sxs-lookup"><span data-stu-id="afbec-349">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)  | [<span data-ttu-id="afbec-350">View</span><span class="sxs-lookup"><span data-stu-id="afbec-350">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="afbec-351">View</span><span class="sxs-lookup"><span data-stu-id="afbec-351">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a><span data-ttu-id="afbec-352">后续步骤</span><span class="sxs-lookup"><span data-stu-id="afbec-352">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="afbec-353">发送主动邮件</span><span class="sxs-lookup"><span data-stu-id="afbec-353">Send proactive messages</span></span>](~/bots/how-to/conversations/send-proactive-messages.md)
