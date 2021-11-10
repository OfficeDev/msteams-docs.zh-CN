---
title: 获取Teams程序的特定上下文
author: surbhigupta
description: 如何获取机器人的 Microsoft 团队的特定上下文，包括对话名单、单个成员或团队的详细信息、频道列表、代码示例。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
keywords: 自动程序上下文名单用户配置文件通道列表
ms.openlocfilehash: eb935515e4f130e57cf634dd9716306cce9f3a05
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60888242"
---
# <a name="get-teams-specific-context-for-your-bot"></a>获取Teams程序的特定上下文

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

机器人可以访问有关安装团队或聊天的其他上下文数据。 此信息可用于丰富自动程序的功能并提供更加个性化的体验。

## <a name="fetch-the-roster-or-user-profile"></a>获取名单或用户配置文件

机器人可以查询成员列表及其基本用户配置文件，包括Teams ID 和Azure Active Directory (AAD) 信息，如名称和 objectId。 可以使用此信息来关联用户标识。 例如，要检查用户是否通过凭据登录选项卡AAD，是团队的成员。 对于获取对话成员，最小或最大页面大小取决于实现。 小于 50、被视为 50 且大于 500 的页面大小限定为 500。 即使你使用非分页版本，它在大型团队中也不可靠，并且不得使用。 有关详细信息，请参阅[对自动Teams API 的更改，以提取团队或聊天成员](~/resources/team-chat-member-api-changes.md)。

以下示例代码使用分页终结点提取名单：

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

# <a name="json"></a>[JSON](#tab/json)

你可以直接在 上发出 GET 请求 `/v3/conversations/{conversationId}/pagedmembers?pageSize={pageSize}&continuationToken={continuationToken}` ，使用 的值 `serviceUrl` 作为 终结点。 的值 `serviceUrl` 稳定，但可以更改。 当新消息到达时，机器人必须验证其存储的值 `serviceUrl` 。 响应有效负载还指示用户是常规用户还是匿名用户。

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

获取名单或用户配置文件后，可以获取单个成员的详细信息。 目前，若要检索聊天或团队的一个或多个成员的信息，请使用 Microsoft Teams 聊天机器人 API 或 `TeamsInfo.GetMembersAsync` `TeamsInfo.getMembers` C# Api。

## <a name="get-single-member-details"></a>获取单个成员详细信息

您还可以使用特定用户的用户 ID、UPN 或 Teams对象 ID 来检索AAD的详细信息。

以下示例代码用于获取单个成员详细信息：

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        var member = await TeamsInfo.GetMemberAsync(turnContext, turnContext.Activity.From.Id, cancellationToken);
    }
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    member = await TeamsInfo.get_member(turn_context, turn_context.activity.from_property.id)
```

# <a name="json"></a>[JSON](#tab/json)

你可以直接在 上发出 GET 请求 `/v3/conversations/{conversationId}/members/{userId}` ，使用 的值 `serviceUrl` 作为 终结点。 的值 `serviceUrl` 稳定，但可以更改。 当新消息到达时，机器人必须验证其存储的值 `serviceUrl` 。 这可用于常规用户和匿名用户。

下面是常规用户的响应示例：

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

下面是匿名用户的响应示例：

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

获取单个成员的详细信息后，可以获取团队的详细信息。 目前，若要检索团队的信息，请使用适用于 Microsoft Teams 或 TypeScript C# `TeamsInfo.GetMemberDetailsAsync` `TeamsInfo.getTeamDetails` 自动程序 API。

## <a name="get-teams-details"></a>获取团队的详细信息

在团队中安装后，机器人可以查询有关该团队的元数据，包括AAD ID。

以下示例代码用于获取团队的详细信息：

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[JSON](#tab/json)

你可以直接在 上发出 GET 请求 `/v3/teams/{teamId}` ，使用 的值 `serviceUrl` 作为 终结点。 的值 `serviceUrl` 稳定，但可以更改。 当新消息到达时，机器人必须验证其存储的值 `serviceUrl` 。

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

获取团队的详细信息后，可以获取团队中的频道列表。 目前，若要检索团队中频道列表的信息，请使用 Microsoft Teams 自动程序 API C# `TeamsInfo.GetTeamChannelsAsync` `TeamsInfo.getTeamChannels` TypeScript API。

## <a name="get-the-list-of-channels-in-a-team"></a>获取团队中的频道列表

机器人可以查询团队中的频道列表。

> [!NOTE]
> * 返回默认"常规"频道的名称， `null` 以允许本地化。
> * 常规频道的频道 ID 始终与团队 ID 匹配。

以下示例代码用于获取团队中的频道列表：

# <a name="c"></a>[C#](#tab/dotnet)

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

# <a name="typescript"></a>[TypeScript](#tab/typescript)

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

# <a name="python"></a>[Python](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

# <a name="json"></a>[JSON](#tab/json)

你可以直接在 上发出 GET 请求 `/v3/teams/{teamId}/conversations` ，使用 的值 `serviceUrl` 作为 终结点。 的值 `serviceUrl` 稳定，但可以更改。 当新消息到达时，机器人必须验证其存储的值 `serviceUrl` 。

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

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [通过自动程序发送和接收文件](~/bots/how-to/bots-filesv4.md)
