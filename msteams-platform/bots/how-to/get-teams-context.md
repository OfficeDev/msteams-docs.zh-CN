---
title: 获取团队针对你的 bot 的特定上下文
author: clearab
description: 如何：获取 Microsoft 团队针对你的 bot 的特定上下文，包括对话名单、详细信息和频道列表。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 9f70e3e052903365f03c541db83f196f33fc2322
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673382"
---
# <a name="get-teams-specific-context-for-your-bot"></a>获取团队针对你的 bot 的特定上下文

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

Bot 可以访问有关安装它的团队或聊天的其他上下文数据。 此信息可用于丰富 bot 的功能，并提供更个性化的体验。

## <a name="fetching-the-roster-or-user-profile"></a>提取名单或用户配置文件

你的 bot 可以查询成员列表和基本配置文件，包括团队用户 Id 和 Azure Active Directory （Azure AD）等信息，如名称和 objectId。 您可以使用此信息来关联用户标识（例如，检查用户是否通过 Azure AD 凭据登录到选项卡）是团队的成员。 您还可以在一对一聊天中使用此呼叫来获取有关用户的其他信息。

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

```csharp
public class MyBot : TeamsActivityHandler
{
    protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
    {
        IEnumerable<TeamsChannelAccount> members = await TeamsInfo.GetMembersAsync(turnContext, cancellationToken);
    }
}
```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();

        // See https://aka.ms/about-bot-activity-message to learn more about the message and other activity types.
        this.onMessage(async (turnContext, next) => {
            const members = await TeamsInfo.getMembers(turnContext);

            // By calling next() you ensure that the next BotHandler is run.
            await next();
        });
    }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)
您可以使用`serviceUrl`作为终结点的值`/v3/conversations/{teamId}/members/`，直接发出 GET 请求。 值往往是`serviceUrl`稳定的，但可能会发生变化。 新邮件到达时，您的 bot 应验证其存储的`serviceUrl`值。

```http
GET /v3/conversations/19:ja0cu120i1jod12j@skype.net/members

Response body
[{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "objectId": "9d3e08f9-a7ae-43aa-a4d3-de3f319a8a9c",
    "givenName": "Larry",
    "surname": "Brown",
    "email": "Larry.Brown@fabrikam.com",
    "userPrincipalName": "labrown@fabrikam.com"
}, {
    "id": "29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
    "objectId": "76b0b09f-d410-48fd-993e-84da521a597b",
    "givenName": "John",
    "surname": "Patterson",
    "email": "johnp@fabrikam.com",
    "userPrincipalName": "johnp@fabrikam.com"
}, {
    "id": "29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
    "objectId": "6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
    "givenName": "Rick",
    "surname": "Stevens",
    "email": "Rick.Stevens@fabrikam.com",
    "userPrincipalName": "rstevens@fabrikam.com"
}]
```

# <a name="pythontabpython"></a>[Python](#tab/python)

```python
async def _show_members(
    self, turn_context: TurnContext
):
    members = await TeamsInfo.get_team_members(turn_context)
```

* * *

## <a name="get-teams-details"></a>获取团队的详细信息

在团队中安装时，你的 bot 可以查询有关此团队的元数据，包括 Azure AD groupId。

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

您可以使用`serviceUrl`作为终结点的值`/v3/teams/{teamId}`，直接发出 GET 请求。 值往往是`serviceUrl`稳定的，但可能会发生变化。 新邮件到达时，您的 bot 应验证其存储的`serviceUrl`值。

```http
GET /v3/teams/19:ja0cu120i1jod12j@skype.net

Response body
{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "The Team Name",
    "aadGroupId": "02ce3874-dd86-41ba-bddc-013f34019978"
}
```

# <a name="pythontabpython"></a>[Python](#tab/python)

```python
async def _show_details(self, turn_context: TurnContext):
    team_details = await TeamsInfo.get_team_details(turn_context)
    reply = MessageFactory.text(f"The team name is {team_details.name}. The team ID is {team_details.id}. The AADGroupID is {team_details.aad_group_id}.")
    await turn_context.send_activity(reply)
```

* * *

## <a name="get-the-list-of-channels-in-a-team"></a>获取团队中频道的列表

你的 bot 可以查询团队中的频道列表。

> [!NOTE]
>
>* 将返回默认常规通道的名称， `null`以允许进行本地化。
>* 常规通道的通道 ID 始终与团队 ID 匹配。

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

您可以使用`serviceUrl`作为终结点的值`/v3/teams/{teamId}/conversations`，直接发出 GET 请求。 值往往是`serviceUrl`稳定的，但可能会发生变化。 新邮件到达时，您的 bot 应验证其存储的`serviceUrl`值。

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


# <a name="pythontabpython"></a>[Python](#tab/python)

```python
async def _show_channels(
    self, turn_context: TurnContext
):
    channels = await TeamsInfo.get_team_channels(turn_context)
    reply = MessageFactory.text(f"Total of {len(channels)} channels are currently in team")
    await turn_context.send_activity(reply)
```

* * *

[!INCLUDE [sample](~/includes/bots/teams-bot-samples.md)]
