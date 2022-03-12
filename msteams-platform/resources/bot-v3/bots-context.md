---
title: 获取自动程序Microsoft Teams上下文
description: 介绍如何获取自动程序在Microsoft Teams
keywords: teams 机器人上下文
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: c4f2df1168b5e429b1d5a1107cd07264e10243bc
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453143"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>获取自动程序Microsoft Teams上下文

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

机器人可以访问有关团队或聊天的其他上下文，如用户配置文件。 此信息可用于丰富自动程序的功能并提供更加个性化的体验。

> [!NOTE]
>
> * Microsoft Teams聊天机器人 API 的最佳访问方式是通过 Bot Builder SDK 的扩展。
> * 对于 C# 或 .NET，请下载 [Microsoft.Bot.Connector.Teams NuGet](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) 程序包。
> * For Node.js development， the Bot Builder for Teams functionality is incorporated into the [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6.

## <a name="fetch-the-team-roster"></a>提取团队名单

机器人可以查询团队成员及其基本个人资料的列表。 基本配置文件包括Teams ID 和Microsoft Azure Active Directory (Azure AD) ，如名称和对象 ID。 可以使用此信息来关联用户标识。 例如，检查用户是否通过登录选项卡Microsoft Azure Active Directory (Azure AD) 凭据是团队成员。

### <a name="rest-api-example"></a>REST API 示例

直接在 上发出 GET 请求 [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members)，使用 `serviceUrl` 值作为终结点。

可以在 `teamId` 自动程序在 `channeldata` 下列情况下接收的活动有效负载的对象中找到 ：

* 当用户在团队上下文中向机器人发送消息或与之交互时。 有关详细信息，请参阅 [接收邮件](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)。
* 将新用户或机器人添加到团队时。 有关详细信息，请参阅添加到 [团队的机器人或用户](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)。

> [!NOTE]
>
>* 调用 API 时始终使用团队 ID。
>* 值 `serviceUrl` 往往很稳定，但可能会更改。 当新消息到达时，机器人必须验证其存储 `serviceUrl` 值。

```json
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

### <a name="net-example"></a>.NET 示例

调用 `GetConversationMembersAsync` using `Team.Id` 可返回用户 ID 列表。

```csharp
// Fetch the members in the current conversation
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));
var teamId = context.Activity.GetChannelData<TeamsChannelData>().Team.Id;
var members = await connector.Conversations.GetConversationMembersAsync(teamId);

// Concatenate information about all members into a string
var sb = new StringBuilder();
foreach (var member in members.AsTeamsChannelAccounts())
{
    sb.AppendFormat(
        "GivenName = {0}, TeamsMemberId = {1}",
        member.Name, member.Id);

    sb.AppendLine();
}

// Post the member info back into the conversation
await context.PostAsync($"People in this conversation: {sb.ToString()}");
```

### <a name="nodejs-or-typescript-example"></a>Node.js或 TypeScript 示例

```typescript

[...]
import * as builder from "botbuilder";
[...]

var teamId = session.message.sourceEvent.team.id;
connector.fetchMembers(
  (<builder.IChatConnectorAddress>session.message.address).serviceUrl,
  teamId,
  (err, result) => {
    if (err) {
      session.endDialog('There is some error');
    }
    else {
      session.endDialog('%s', JSON.stringify(result));
    }
  }
);
```

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>在个人或群组聊天中提取用户配置文件或名单

你可以对任意个人聊天进行 API 调用，以获取与机器人聊天的用户的个人资料信息。

API 调用、SDK 方法和响应对象与提取团队名单完全相同。 唯一的区别是传递 `conversationId` ，而不是 `teamId`传递 。

## <a name="fetch-the-list-of-channels-in-a-team"></a>获取团队中的频道列表

机器人可以查询团队中的频道列表。

> [!NOTE]
>
>* 返回默认"常规"频道的名称，以 `null` 允许本地化。
>* 常规频道的频道 ID 始终与团队 ID 匹配。

### <a name="rest-api-example"></a>REST API 示例

直接在 上发出 GET 请求 `/teams/{teamId}/conversations/`，使用 `serviceUrl` 值作为终结点。

的唯一来源 `teamId` 是团队上下文中的消息。 该消息可以是来自用户的消息，或者是机器人在添加到团队时收到的消息。 有关详细信息，请参阅添加到 [团队的机器人或用户](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)。

> [!NOTE]
> 值 `serviceUrl` 往往很稳定，但可能会更改。 当新消息到达时，机器人必须验证其存储 `serviceUrl` 值。

```json
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

#### <a name="net-example"></a>.NET 示例

以下示例使用来自`FetchChannelList`适用于 [.NET 的自动Teams SDK 的扩展的调用](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)：

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Node.js示例

下面的示例使用自动`fetchChannelList`程序生成器 SDK Teams[扩展](https://www.npmjs.com/package/botbuilder-teams)中的调用Node.js：

```javascript
var teamId = session.message.sourceEvent.team.id;
connector.fetchChannelList(
  (session.message.address).serviceUrl,
  teamId,
  (err, result) => {
    if (err) {
      session.endDialog('There is an error');
    }
    else {
      session.endDialog('%s', JSON.stringify(result));
    }
  }
);
```

## <a name="get-clientinfo-in-your-bot-context"></a>在自动程序上下文中获取 clientInfo

可以在自动程序的活动内获取 clientInfo。 clientInfo 包含以下属性：

* Locale
* 国家/地区
* 平台
* Timezone

### <a name="json-example"></a>JSON 示例

```json
[
    {
        "type": "clientInfo",
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "Asia/Calcutta"
    }
]
```

### <a name="c-example"></a>C#示例

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```

## <a name="see-also"></a>另请参阅

[Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
