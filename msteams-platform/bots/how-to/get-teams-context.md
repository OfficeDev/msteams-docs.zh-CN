---
title: 获取Teams程序的特定上下文
author: laujan
description: 如何获取机器人的 Microsoft 团队的特定上下文，包括对话名单、详细信息和频道列表。
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 6a8f903fb2f3ed8120e31b7536b65f22fdf6d620
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630164"
---
# <a name="get-teams-specific-context-for-your-bot"></a><span data-ttu-id="01eb1-103">获取Teams程序的特定上下文</span><span class="sxs-lookup"><span data-stu-id="01eb1-103">Get Teams specific context for your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="01eb1-104">机器人可以访问有关安装团队或聊天的其他上下文数据。</span><span class="sxs-lookup"><span data-stu-id="01eb1-104">A bot can access additional context data about a team or chat where it is installed.</span></span> <span data-ttu-id="01eb1-105">此信息可用于丰富自动程序的功能并提供更加个性化的体验。</span><span class="sxs-lookup"><span data-stu-id="01eb1-105">This information can be used to enrich the bot's functionality and provide a more personalized experience.</span></span>

## <a name="fetch-the-roster-or-user-profile"></a><span data-ttu-id="01eb1-106">获取名单或用户配置文件</span><span class="sxs-lookup"><span data-stu-id="01eb1-106">Fetch the roster or user profile</span></span>

<span data-ttu-id="01eb1-107">机器人可以查询成员列表及其基本用户配置文件，包括 Teams 用户 ID 和 Azure Active Directory (AAD) 信息，如名称和 objectId。</span><span class="sxs-lookup"><span data-stu-id="01eb1-107">Your bot can query for the list of members and their basic user profiles, including Teams user IDs and Azure Active Directory (AAD) information, such as name and objectId.</span></span> <span data-ttu-id="01eb1-108">可以使用此信息来关联用户标识。</span><span class="sxs-lookup"><span data-stu-id="01eb1-108">You can use this information to correlate user identities.</span></span> <span data-ttu-id="01eb1-109">例如，要检查用户是否通过 AAD 凭据登录到选项卡，是团队的成员。</span><span class="sxs-lookup"><span data-stu-id="01eb1-109">For example, to check whether a user logged into a tab through AAD credentials, is a member of the team.</span></span> <span data-ttu-id="01eb1-110">对于获取对话成员，最小或最大页面大小取决于实现。</span><span class="sxs-lookup"><span data-stu-id="01eb1-110">For get conversation members, minimum or maximum page size depends on the implementation.</span></span> <span data-ttu-id="01eb1-111">小于 50、被视为 50 且大于 500 的页面大小限定为 500。</span><span class="sxs-lookup"><span data-stu-id="01eb1-111">Page size less than 50, are treated as 50, and greater than 500, are capped at 500.</span></span> <span data-ttu-id="01eb1-112">即使你使用非分页版本，它在大型团队中也不可靠，并且不得使用。</span><span class="sxs-lookup"><span data-stu-id="01eb1-112">Even if you use the non-paged version, it is unreliable in large teams and must not be used.</span></span> <span data-ttu-id="01eb1-113">有关详细信息，请参阅[对自动程序 API Teams获取团队或聊天成员的更改](~/resources/team-chat-member-api-changes.md)。</span><span class="sxs-lookup"><span data-stu-id="01eb1-113">For more information, see [changes to Teams Bot APIs for fetching team or chat members](~/resources/team-chat-member-api-changes.md).</span></span>

<span data-ttu-id="01eb1-114">以下示例代码使用分页终结点提取名单：</span><span class="sxs-lookup"><span data-stu-id="01eb1-114">The following sample code uses the paged endpoint for fetching the roster:</span></span>

# <a name="c"></a>[<span data-ttu-id="01eb1-115">C#</span><span class="sxs-lookup"><span data-stu-id="01eb1-115">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="01eb1-116">TypeScript</span><span class="sxs-lookup"><span data-stu-id="01eb1-116">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="01eb1-117">Python</span><span class="sxs-lookup"><span data-stu-id="01eb1-117">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[<span data-ttu-id="01eb1-118">JSON</span><span class="sxs-lookup"><span data-stu-id="01eb1-118">JSON</span></span>](#tab/json)

<span data-ttu-id="01eb1-119">你可以直接在 上发出 GET 请求 `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}` ，将 的值 `serviceUrl` 用作 终结点。</span><span class="sxs-lookup"><span data-stu-id="01eb1-119">You can directly issue a GET request on `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="01eb1-120">的值 `serviceUrl` 稳定，但可以更改。</span><span class="sxs-lookup"><span data-stu-id="01eb1-120">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="01eb1-121">当新消息到达时，机器人必须验证其存储的值 `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="01eb1-121">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="01eb1-122">响应有效负载还指示用户是常规用户还是匿名用户。</span><span class="sxs-lookup"><span data-stu-id="01eb1-122">The response payload also indicates if the user is a regular or anonymous user.</span></span>

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

<span data-ttu-id="01eb1-123">获取名单或用户配置文件后，可以获取单个成员的详细信息。</span><span class="sxs-lookup"><span data-stu-id="01eb1-123">After you fetch the roster or user profile, you can get details of a single member.</span></span> <span data-ttu-id="01eb1-124">目前，若要检索聊天或团队的一个或多个成员的信息，请使用 Microsoft Teams 聊天机器人 API 或 `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` C# Api。</span><span class="sxs-lookup"><span data-stu-id="01eb1-124">Currently, to retrieve information for one or more members of a chat or team, use the Microsoft Teams bot APIs `TeamsInfo.GetMembersAsync` for C# or `TeamsInfo.getMembers` for TypeScript APIs.</span></span>

## <a name="get-single-member-details"></a><span data-ttu-id="01eb1-125">获取单个成员详细信息</span><span class="sxs-lookup"><span data-stu-id="01eb1-125">Get single member details</span></span>

<span data-ttu-id="01eb1-126">您还可以使用特定用户的用户 ID、UPN 或 AAD Teams检索其详细信息。</span><span class="sxs-lookup"><span data-stu-id="01eb1-126">You can also retrieve the details of a particular user using their Teams user ID, UPN, or AAD Object ID.</span></span>

<span data-ttu-id="01eb1-127">以下示例代码用于获取单个成员详细信息：</span><span class="sxs-lookup"><span data-stu-id="01eb1-127">The following sample code is used to get single member details:</span></span>

# <a name="c"></a>[<span data-ttu-id="01eb1-128">C#</span><span class="sxs-lookup"><span data-stu-id="01eb1-128">C#</span></span>](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescript"></a>[<span data-ttu-id="01eb1-129">TypeScript</span><span class="sxs-lookup"><span data-stu-id="01eb1-129">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="01eb1-130">Python</span><span class="sxs-lookup"><span data-stu-id="01eb1-130">Python</span></span>](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = await TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[<span data-ttu-id="01eb1-131">JSON</span><span class="sxs-lookup"><span data-stu-id="01eb1-131">JSON</span></span>](#tab/json)

<span data-ttu-id="01eb1-132">你可以直接在 上发出 GET 请求 `/v3/conversations/{conversationId}/members/{userId}` ，将 的值 `serviceUrl` 用作 终结点。</span><span class="sxs-lookup"><span data-stu-id="01eb1-132">You can directly issue a GET request on `/v3/conversations/{conversationId}/members/{userId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="01eb1-133">的值 `serviceUrl` 稳定，但可以更改。</span><span class="sxs-lookup"><span data-stu-id="01eb1-133">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="01eb1-134">当新消息到达时，机器人必须验证其存储的值 `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="01eb1-134">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span> <span data-ttu-id="01eb1-135">这可用于常规用户和匿名用户。</span><span class="sxs-lookup"><span data-stu-id="01eb1-135">This can be used for regular users and anonymous users.</span></span>

<span data-ttu-id="01eb1-136">下面是常规用户的响应示例：</span><span class="sxs-lookup"><span data-stu-id="01eb1-136">The following is the response sample for regular user:</span></span>

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

<span data-ttu-id="01eb1-137">下面是匿名用户的响应示例：</span><span class="sxs-lookup"><span data-stu-id="01eb1-137">The following is the response sample for anonymous user:</span></span>

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

<span data-ttu-id="01eb1-138">获取单个成员的详细信息后，可以获取团队的详细信息。</span><span class="sxs-lookup"><span data-stu-id="01eb1-138">After you get details of a single member, you can get details of the team.</span></span> <span data-ttu-id="01eb1-139">目前，若要检索团队的信息，请使用 Microsoft Teams 或 TypeScript C# `TeamsInfo.GetMemberDetailsAsync` `TeamsInfo.getTeamDetails` 自动程序 API。</span><span class="sxs-lookup"><span data-stu-id="01eb1-139">Currently, to retrieve information for a team, use the Microsoft Teams bot APIs `TeamsInfo.GetMemberDetailsAsync` for C# or `TeamsInfo.getTeamDetails` for TypeScript.</span></span>

## <a name="get-teams-details"></a><span data-ttu-id="01eb1-140">获取团队的详细信息</span><span class="sxs-lookup"><span data-stu-id="01eb1-140">Get team's details</span></span>

<span data-ttu-id="01eb1-141">在团队中安装后，机器人可以查询有关该团队的元数据，包括 AAD 组 ID。</span><span class="sxs-lookup"><span data-stu-id="01eb1-141">When installed in a team, your bot can query for metadata about that team including the AAD group ID.</span></span>

<span data-ttu-id="01eb1-142">以下示例代码用于获取团队的详细信息：</span><span class="sxs-lookup"><span data-stu-id="01eb1-142">The following sample code is used to get team's details:</span></span>

# <a name="c"></a>[<span data-ttu-id="01eb1-143">C#</span><span class="sxs-lookup"><span data-stu-id="01eb1-143">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="01eb1-144">TypeScript</span><span class="sxs-lookup"><span data-stu-id="01eb1-144">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="01eb1-145">Python</span><span class="sxs-lookup"><span data-stu-id="01eb1-145">Python</span></span>](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="01eb1-146">JSON</span><span class="sxs-lookup"><span data-stu-id="01eb1-146">JSON</span></span>](#tab/json)

<span data-ttu-id="01eb1-147">你可以直接在 上发出 GET 请求 `/v3/teams/{teamId}` ，将 的值 `serviceUrl` 用作 终结点。</span><span class="sxs-lookup"><span data-stu-id="01eb1-147">You can directly issue a GET request on `/v3/teams/{teamId}`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="01eb1-148">的值 `serviceUrl` 稳定，但可以更改。</span><span class="sxs-lookup"><span data-stu-id="01eb1-148">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="01eb1-149">当新消息到达时，机器人必须验证其存储的值 `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="01eb1-149">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span>

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

<span data-ttu-id="01eb1-150">获取团队的详细信息后，可以获取团队中的频道列表。</span><span class="sxs-lookup"><span data-stu-id="01eb1-150">After you get details of the team, you can get the list of channels in a team.</span></span> <span data-ttu-id="01eb1-151">目前，若要检索团队中频道列表的信息，请使用 Microsoft Teams 自动程序 API C# `TeamsInfo.GetTeamChannelsAsync` `TeamsInfo.getTeamChannels` TypeScript API。</span><span class="sxs-lookup"><span data-stu-id="01eb1-151">Currently, to retrieve information for a list of channels in a team, use the Microsoft Teams bot APIs `TeamsInfo.GetTeamChannelsAsync` for C# or `TeamsInfo.getTeamChannels` for TypeScript APIs.</span></span>

## <a name="get-the-list-of-channels-in-a-team"></a><span data-ttu-id="01eb1-152">获取团队中的频道列表</span><span class="sxs-lookup"><span data-stu-id="01eb1-152">Get the list of channels in a team</span></span>

<span data-ttu-id="01eb1-153">机器人可以查询团队中的频道列表。</span><span class="sxs-lookup"><span data-stu-id="01eb1-153">Your bot can query the list of channels in a team.</span></span>

> [!NOTE]
> * <span data-ttu-id="01eb1-154">返回默认"常规"频道的名称， `null` 以允许本地化。</span><span class="sxs-lookup"><span data-stu-id="01eb1-154">The name of the default General channel is returned as `null` to allow for localization.</span></span>
> * <span data-ttu-id="01eb1-155">常规频道的频道 ID 始终与团队 ID 匹配。</span><span class="sxs-lookup"><span data-stu-id="01eb1-155">The channel ID for the General channel always matches the team ID.</span></span>

<span data-ttu-id="01eb1-156">以下示例代码用于获取团队中的频道列表：</span><span class="sxs-lookup"><span data-stu-id="01eb1-156">The following sample code is used to get the list of channels in a team:</span></span>

# <a name="c"></a>[<span data-ttu-id="01eb1-157">C#</span><span class="sxs-lookup"><span data-stu-id="01eb1-157">C#</span></span>](#tab/dotnet)

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

# <a name="typescript"></a>[<span data-ttu-id="01eb1-158">TypeScript</span><span class="sxs-lookup"><span data-stu-id="01eb1-158">TypeScript</span></span>](#tab/typescript)

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

# <a name="python"></a>[<span data-ttu-id="01eb1-159">Python</span><span class="sxs-lookup"><span data-stu-id="01eb1-159">Python</span></span>](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[<span data-ttu-id="01eb1-160">JSON</span><span class="sxs-lookup"><span data-stu-id="01eb1-160">JSON</span></span>](#tab/json)

<span data-ttu-id="01eb1-161">你可以直接在 上发出 GET 请求 `/v3/teams/{teamId}/conversations` ，将 的值 `serviceUrl` 用作 终结点。</span><span class="sxs-lookup"><span data-stu-id="01eb1-161">You can directly issue a GET request on `/v3/teams/{teamId}/conversations`, using the value of `serviceUrl` as the endpoint.</span></span> <span data-ttu-id="01eb1-162">的值 `serviceUrl` 稳定，但可以更改。</span><span class="sxs-lookup"><span data-stu-id="01eb1-162">The value of `serviceUrl` is stable but can change.</span></span> <span data-ttu-id="01eb1-163">当新消息到达时，机器人必须验证其存储的值 `serviceUrl` 。</span><span class="sxs-lookup"><span data-stu-id="01eb1-163">When a new message arrives, your bot must verify its stored value for `serviceUrl`.</span></span>

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

## <a name="next-step"></a><span data-ttu-id="01eb1-164">后续步骤</span><span class="sxs-lookup"><span data-stu-id="01eb1-164">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="01eb1-165">通过自动程序发送和接收文件</span><span class="sxs-lookup"><span data-stu-id="01eb1-165">Send and receive files through the bot</span></span>](~/bots/how-to/bots-filesv4.md)
