---
title: 获取团队针对你的 bot 的特定上下文
author: laujan
description: 如何：获取 Microsoft 团队针对你的 bot 的特定上下文，包括对话名单、详细信息和频道列表。
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 7f3b2fbea33f64659dcd5d9d39bb95e2d953dbea
ms.sourcegitcommit: bfdcd122b6b4ffc52d92320d4741f870c07f0542
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/02/2020
ms.locfileid: "49552470"
---
# <a name="get-teams-specific-context-for-your-bot"></a><span data-ttu-id="1ad5b-103">获取团队针对你的 bot 的特定上下文</span><span class="sxs-lookup"><span data-stu-id="1ad5b-103">Get Team's specific context for your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="1ad5b-104">Bot 可以访问有关安装它的团队或聊天的其他上下文数据。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-104">A bot can access additional context data about a team or chat it is installed in.</span></span> <span data-ttu-id="1ad5b-105">此信息可用于丰富 bot 的功能，并提供更个性化的体验。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-105">This information can be used to enrich the bot's functionality and provide a more personalized experience.</span></span>

## <a name="fetching-the-roster-or-user-profile"></a><span data-ttu-id="1ad5b-106">提取名单或用户配置文件</span><span class="sxs-lookup"><span data-stu-id="1ad5b-106">Fetching the roster or user profile</span></span>

<span data-ttu-id="1ad5b-107">你的 bot 可以查询成员列表和基本配置文件，包括团队用户 Id 和 Azure Active Directory (Azure AD) 信息（如 name 和 objectId）。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-107">Your bot can query for the list of members and their basic profiles, including Teams user IDs and Azure Active Directory (Azure AD) information such as name and objectId.</span></span> <span data-ttu-id="1ad5b-108">您可以使用此信息来关联用户标识（例如，检查用户是否通过 Azure AD 凭据登录到选项卡）是团队的成员。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-108">You can use this information to correlate user identities, e.g., to check whether a user, logged into a tab through Azure AD credentials, is a member of the team.</span></span> <span data-ttu-id="1ad5b-109">下面的示例代码使用分页终结点检索名单。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-109">The sample code below uses the paged endpoint for retrieving the roster.</span></span> <span data-ttu-id="1ad5b-110">对于 get 对话成员，最小或最大页面大小取决于实现。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-110">For get conversation members, minimum or maximum page size depends on the implementation.</span></span> <span data-ttu-id="1ad5b-111">小于50的页面大小被视为50，页面大小大于500，它们的上限为500。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-111">Page size less than 50, are treated as 50, and page size greater than 500, are capped at 500.</span></span> <span data-ttu-id="1ad5b-112">虽然您仍可以使用非页面版本，但它在大型团队中不可靠，不应使用。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-112">Although you may still use the non-paged version, it will be unreliable in large teams and should not be used.</span></span> <span data-ttu-id="1ad5b-113">有关获取团队/聊天成员的详细信息，*请参阅*[对团队 Bot api 所做的更改](~/resources/team-chat-member-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-113">*See* [Changes to Teams Bot APIs for Fetching Team/Chat Members](~/resources/team-chat-member-api-changes.md) for additional information.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="1ad5b-114">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="1ad5b-114">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var members = new List<TeamsChannelAccount>();
        string continuationToken = null;

        do
        {
            var currentPage = await TeamsInfo.GetPagedMembersAsync(turnContext, 100, continuationToken, cancellationToken);
            continuationToken = currentPage.ContinuationToken;
            members.AddRange(currentPage.Members);
         }
         while (continuationToken != null);
     }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="1ad5b-115">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="1ad5b-115">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            var continuationToken;
            var members = [];

            do {
                var pagedMembers = await TeamsInfo.getPagedMembers(context, 100, continuationToken);
                continuationToken = pagedMembers.continuationToken;
                members.push(...pagedMembers.members);
            }
            while(continuationToken !== undefined)

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="1ad5b-116">Python</span><span class="sxs-lookup"><span data-stu-id="1ad5b-116">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[<span data-ttu-id="1ad5b-117">JSON</span><span class="sxs-lookup"><span data-stu-id="1ad5b-117">JSON</span></span>](#tab/json)

<span data-ttu-id="1ad5b-118">您可以 `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}` 使用作为终结点的值，直接发出 GET 请求 `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-118">You can directly issue a GET request on `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="1ad5b-119">值 `serviceUrl` 往往是稳定的，但可能会发生变化。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-119">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="1ad5b-120">新邮件到达时，您的 bot 应验证其存储的值 `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-120">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="1ad5b-121">响应有效负载还将指示用户是常规用户还是匿名用户。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-121">The response payload will also indicate if the user is a regular or anonymous user.</span></span>

```http
GET /v3/conversations/19:meeting_N2QzYTA3YmItYmMwOC00OTJmLThkYzMtZWMzZGU0NGIyZGI0@thread.v2/pagedmembers?pageSize=100&continuationToken=asdfasdfalkdsjfalksjdf

Response body
{
   "continuationToken":"asdfqwerueiqpiewr",
   "members":[
      {
         "id":"29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
         "name":"Anon1 (Guest)",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"anonymous"
      },
      {
         "id":"29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
         "objectId":"76b0b09f-d410-48fd-993e-84da521a597b",
         "givenName":"John",
         "surname":"Patterson",
         "email":"johnp@fabrikam.com",
         "userPrincipalName":"johnp@fabrikam.com",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"user"
      },
      {
         "id":"29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
         "objectId":"6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
         "givenName":"Rick",
         "surname":"Stevens",
         "email":"Rick.Stevens@fabrikam.com",
         "userPrincipalName":"rstevens@fabrikam.com",
         "tenantId":"29:1UX7p8Fkx7p93MZlBFS71swTB9juQOCfnXf2L3wxOUITCcIGpFcRX-JiFjLDVZhxGpEfzSTGNsZeEyTKr1iu3Vw",
         "userRole":"user"
      }
   ]
}
```

* * *

## <a name="get-single-member-details"></a><span data-ttu-id="1ad5b-122">获取单个成员详细信息</span><span class="sxs-lookup"><span data-stu-id="1ad5b-122">Get single member details</span></span>

<span data-ttu-id="1ad5b-123">您还可以使用团队用户 Id、UPN 或 AAD 对象 Id 检索特定用户的详细信息。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-123">You can also retrieve the details of a particular user using their Teams user Id, UPN, or AAD Object Id.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="1ad5b-124">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="1ad5b-124">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="1ad5b-125">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="1ad5b-125">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        const member = await TeamsInfo.getMember(context, encodeURI('someone@somecompany.com'));

        // By calling next() you ensure that the next BotHandler is run.
        await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="1ad5b-126">Python</span><span class="sxs-lookup"><span data-stu-id="1ad5b-126">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[<span data-ttu-id="1ad5b-127">JSON</span><span class="sxs-lookup"><span data-stu-id="1ad5b-127">JSON</span></span>](#tab/json)

<span data-ttu-id="1ad5b-128">您可以 `/v3/conversations/{conversationId}/members/{userId}` 使用作为终结点的值，直接发出 GET 请求 `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-128">You can directly issue a GET request on `/v3/conversations/{conversationId}/members/{userId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="1ad5b-129">值 `serviceUrl` 往往是稳定的，但可能会发生变化。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-129">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="1ad5b-130">新邮件到达时，您的 bot 应验证其存储的值 `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-130">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="1ad5b-131">这可用于 regualr 用户和匿名用户。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-131">This can be used for regualr users and anonymous users.</span></span>

<span data-ttu-id="1ad5b-132">以下是常规用户的响应示例</span><span class="sxs-lookup"><span data-stu-id="1ad5b-132">Below is a response sample for regular user</span></span>

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47", 
    "userRole":"user"
}
```

<span data-ttu-id="1ad5b-133">以下是匿名用户的响应</span><span class="sxs-lookup"><span data-stu-id="1ad5b-133">Below is response for anonymous user</span></span>

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members/<anonymous user id>"

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "Anon1 (Guest)",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47", 
    "userRole":"anonymous"
}
```

* * *

## <a name="get-teams-details"></a><span data-ttu-id="1ad5b-134">获取团队的详细信息</span><span class="sxs-lookup"><span data-stu-id="1ad5b-134">Get team's details</span></span>

<span data-ttu-id="1ad5b-135">在团队中安装时，你的 bot 可以查询有关此团队的元数据，包括 Azure AD groupId。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-135">When installed in a team, your bot can query for metadata about that team including the Azure AD groupId.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="1ad5b-136">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="1ad5b-136">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        TeamDetails teamDetails = await TeamsInfo.GetTeamDetailsAsync(turnContext, turnContext.Activity.TeamsGetTeamInfo().Id, cancellationToken);
        if (teamDetails != null) {
            await turnContext.SendActivityAsync($"The groupId is: {teamDetails.AadGroupId}");
        }
        else {
            await turnContext.SendActivityAsync($"Message did not come from a channel in a team.");
        }
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="1ad5b-137">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="1ad5b-137">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const teamDetails = await TeamsInfo.getTeamDetails(turnContext);
            if (teamDetails) {
                await turnContext.sendActivity(`The group ID is: ${teamDetails.aadGroupId}`);
            } else {
                await turnContext.sendActivity('This message did not come from a channel in a team.');
            }

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="1ad5b-138">Python</span><span class="sxs-lookup"><span data-stu-id="1ad5b-138">Python</span></span>](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="1ad5b-139">JSON</span><span class="sxs-lookup"><span data-stu-id="1ad5b-139">JSON</span></span>](#tab/json)

<span data-ttu-id="1ad5b-140">您可以 `/v3/teams/{teamId}` 使用作为终结点的值，直接发出 GET 请求 `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-140">You can directly issue a GET request on `/v3/teams/{teamId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="1ad5b-141">值 `serviceUrl` 往往是稳定的，但可能会发生变化。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-141">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="1ad5b-142">新邮件到达时，您的 bot 应验证其存储的值 `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-142">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
GET /v3/teams/19:ja0cu120i1jod12j@skype.net

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "The Team Name",
    "aadGroupId": "02ce3874-dd86-41ba-bddc-013f34019978"
}
```

* * *

## <a name="get-the-list-of-channels-in-a-team"></a><span data-ttu-id="1ad5b-143">获取团队中频道的列表</span><span class="sxs-lookup"><span data-stu-id="1ad5b-143">Get the list of channels in a team</span></span>

<span data-ttu-id="1ad5b-144">你的 bot 可以查询团队中的频道列表。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-144">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="1ad5b-145">将返回默认常规通道的名称， `null` 以允许进行本地化。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-145">The name of the default General channel is returned as `null` to allow for localization.</span></span>
>* <span data-ttu-id="1ad5b-146">常规通道的通道 ID 始终与团队 ID 匹配。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-146">The channel ID for the General channel always matches the team ID.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="1ad5b-147">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="1ad5b-147">C#/.NET</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        IEnumerable<ChannelInfo> channels = await TeamsInfo.GetTeamChannelsAsync(turnContext, turnContext.Activity.TeamsGetTeamInfo().Id, cancellationToken);

        await turnContext.SendActivityAsync($"The channel count is: {channels.Count()}");
    }
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="1ad5b-148">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="1ad5b-148">TypeScript/Node.js</span></span>](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const channels = await TeamsInfo.getTeamChannels(turnContext);

            await turnContext.sendActivity(`The channel count is: ${channels.length}`);

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="python"></a>[<span data-ttu-id="1ad5b-149">Python</span><span class="sxs-lookup"><span data-stu-id="1ad5b-149">Python</span></span>](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="1ad5b-150">JSON</span><span class="sxs-lookup"><span data-stu-id="1ad5b-150">JSON</span></span>](#tab/json)

<span data-ttu-id="1ad5b-151">您可以 `/v3/teams/{teamId}/conversations` 使用作为终结点的值，直接发出 GET 请求 `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-151">You can directly issue a GET request on `/v3/teams/{teamId}/conversations`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="1ad5b-152">值 `serviceUrl` 往往是稳定的，但可能会发生变化。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-152">The value of `serviceUrl` tends to be stable but can change.</span></span> <span data-ttu-id="1ad5b-153">新邮件到达时，您的 bot 应验证其存储的值 `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="1ad5b-153">When a new message arrives, your bot should verify its stored value for `serviceUrl`.</span></span>

```http
GET /v3/teams/19%3A033451497ea84fcc83d17ed7fb08a1b6%40thread.skype/conversations

Response body
{
    "conversations": [{
        "id": "19:033451497ea84fcc83d17ed7fb08a1b6@thread.skype",
        "name": null
    }, {
        "id": "19:cc25e4aae50746ecbb11473bba24c70a@thread.skype",
        "name": "Materials"
    }, {
        "id": "19:b7b84cba410c406ba671dbbf5e0a3519@thread.skype",
        "name": "Design"
    }, {
        "id": "19:fc5db2aed489454e8f8c06829ed6c986@thread.skype",
        "name": "Marketing"
    }]
}
```

* * *

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
