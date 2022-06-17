---
title: 获取Microsoft Teams机器人的上下文
description: 在本模块中，了解如何获取Microsoft Teams中的机器人的上下文，在个人或群组聊天中提取团队名册和用户个人资料或名册
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 05/20/2019
ms.openlocfilehash: 3fd75e063f9b12c09bc4dded167bd8cdaead6b7a
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143114"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>获取Microsoft Teams机器人的上下文

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

机器人可以访问有关团队或聊天的其他上下文，例如用户配置文件。 此信息可用于丰富机器人的功能并提供更个性化的体验。

> [!NOTE]
>
> * Microsoft Teams特定的机器人 API 最好通过 Bot Builder SDK 的扩展进行访问。
> * 对于 C# 或 .NET，请下载 [Microsoft.Bot.Connector.Teams](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) NuGet包。
> * 对于Node.js开发，Bot Builder for Teams 功能已合并到 [Bot Framework SDK](https://github.com/microsoft/botframework-sdk) v4.6 中。

## <a name="fetch-the-team-roster"></a>提取团队名单

机器人可以查询团队成员列表及其基本配置文件。 基本配置文件包括Teams用户 ID 和 Microsoft Azure Active Directory (Azure AD) 信息，例如名称和对象 ID。 可以使用此信息来关联用户标识。 例如，检查用户是否通过Microsoft Azure Active Directory (Azure AD 登录到选项卡) 凭据是团队成员。

### <a name="rest-api-example"></a>REST API 示例

直接发出 [`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members)GET 请求，使用 `serviceUrl` 该值作为终结点。

可以在 `teamId` 机器人在以下方案中 `channeldata` 接收的活动有效负载的对象中找到：

* 当用户在团队上下文中发送消息或与机器人交互时。 有关详细信息，请参阅 [接收消息](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)。
* 将新用户或机器人添加到团队时。 有关详细信息，请参阅 [添加到团队的机器人或用户](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)。

> [!NOTE]
>
>* 调用 API 时始终使用团队 ID。
>* 该 `serviceUrl` 值通常稳定，但可能会更改。 当新消息到达时，机器人必须验证其存储 `serviceUrl` 值。

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

用于`Team.Id`返回用户 ID 列表的调用`GetConversationMembersAsync`。

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

## <a name="fetch-user-profile-or-roster-in-personal-or-group-chat"></a>在个人或群组聊天中提取用户配置文件或名册

可以对任何个人聊天进行 API 调用，以获取用户与机器人聊天的配置文件信息。

API 调用、SDK 方法和响应对象与提取团队名单相同。 唯一的区别是你传递而不是`conversationId``teamId`传递。

## <a name="fetch-the-list-of-channels-in-a-team"></a>提取团队中的频道列表

机器人可以查询团队中的频道列表。

> [!NOTE]
>
>* 默认常规频道的名称作为 `null` 返回，以允许本地化。
>* 常规频道的频道 ID 始终与团队 ID 匹配。

### <a name="rest-api-example"></a>REST API 示例

直接发出 `/teams/{teamId}/conversations/`GET 请求，使用 `serviceUrl` 该值作为终结点。

唯一的 `teamId` 来源是来自团队上下文的消息。 该消息是来自用户的消息，或者是机器人在添加到团队时收到的消息。 有关详细信息，请参阅 [添加到团队的机器人或用户](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)。

> [!NOTE]
> 该 `serviceUrl` 值通常稳定，但可能会更改。 当新消息到达时，机器人必须验证其存储 `serviceUrl` 值。

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

以下示例使用 `FetchChannelList` [Bot Builder SDK for .NET 的Teams扩展](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)的调用：

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Node.js 示例

以下示例使用 `fetchChannelList` [Bot Builder SDK for Node.js的 Teams 扩展](https://www.npmjs.com/package/botbuilder-teams)的调用：

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

## <a name="get-clientinfo-in-your-bot-context"></a>获取机器人上下文中的 clientInfo

可以在机器人活动中提取 clientInfo。 clientInfo 包含以下属性：

* Locale
* 国家/地区
* 平台
* 时区

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

### <a name="c-example"></a>C# 示例

```csharp
var connector = new ConnectorClient(new Uri(context.Activity.ServiceUrl));

{
    var clientinfo = context.Activity.Entities[0];
    await context.PostAsync($"ClientInfo: clientinfo ");
}
```

## <a name="see-also"></a>另请参阅

[Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。
