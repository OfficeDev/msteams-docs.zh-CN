---
title: 获取你的 bot 的上下文
description: 介绍如何在 Microsoft 团队中获取 bot 的上下文
keywords: 团队 bot 上下文
ms.date: 05/20/2019
ms.openlocfilehash: 8f054661664850ffb843714230e209c8e4737f0a
ms.sourcegitcommit: 6c5c0574228310f844c81df0d57f11e2037e90c8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/21/2020
ms.locfileid: "42227995"
---
# <a name="get-context-for-your-microsoft-teams-bot"></a>获取你的 Microsoft 团队 bot 的上下文

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

你的 bot 可以访问有关团队或聊天的其他上下文，如用户配置文件。 此信息可用于丰富你的 bot 的功能，并提供更个性化的体验。

> [!NOTE]
> 通过使用机器人&ndash;生成器 SDK 的扩展，可以更好地访问这些 Microsoft 团队特定的 bot api。 对于 c #/.NET，请下载我们的 ".[团队](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)" NuGet 包。 对于 node.js 开发，BotBuilder for Microsoft 团队功能已并入到来自 v4.0 的[Bot 框架 SDK](https://github.com/microsoft/botframework-sdk)中。

## <a name="fetching-the-team-roster"></a>提取团队名单

你的 bot 可以查询工作组成员的列表及其基本配置文件，其中包括团队用户 Id 和 Azure Active Directory （Azure AD）等信息，如名称和 objectId。 您可以使用此信息来关联用户标识;例如，检查通过 Azure AD 凭据登录到选项卡的用户是否是团队的成员。

### <a name="rest-api-example"></a>REST API 示例

您可以使用`serviceUrl`作为终结点的值[`/conversations/{teamId}/members/`](/bot-framework/rest-api/bot-framework-rest-connector-api-reference#get-conversation-members)，直接发出 GET 请求。

`teamId`可以在你的 bot 在`channeldata`以下情况下收到的活动负载的对象中找到：
* 当用户在团队上下文中发送邮件或与你的 bot 交互时（请参阅[接收邮件](~/resources/bot-v3/bot-conversations/bots-conversations.md#receiving-messages)）
* 将新用户或 bot 添加到团队时（请参阅[机器人或用户添加到团队](~/resources/bot-v3/bots-notifications.md#bot-or-user-added-to-a-team)）

> [!NOTE]
>* 调用 api 时，请务必使用团队 id
>* 值往往是`serviceUrl`稳定的，但可能会发生变化。 当新邮件到达时，你的 bot 应验证其存储值`serviceUrl`。

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

使用`GetConversationMembersAsync` `Team.Id`调用可返回用户 id 的列表。

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

### <a name="nodejstypescript-example"></a>Node.js/TypeScript 示例

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

*另请参阅* [Bot 框架示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。

## <a name="fetching-user-profile-or-roster-in-personal-or-group-chat"></a>获取个人聊天或组聊天中的用户配置文件或名单

您还可以对任何个人聊天进行相同的 API 调用，以获取用户与你的 bot 聊天的配置文件信息。

API 调用和 SDK 方法与获取团队名单完全相同，响应对象也一样。 唯一的区别是传递的`conversationId`是，而不`teamId`是。

## <a name="fetching-the-list-of-channels-in-a-team"></a>获取团队中通道的列表

你的 bot 可以查询团队中的频道列表。

> [!NOTE]
>
>* 将返回默认常规通道的名称， `null`以允许进行本地化。
>* 常规通道的通道 ID 始终与团队 ID 匹配。

### <a name="rest-api-example"></a>REST API 示例

您可以使用`serviceUrl`作为终结点的值`/teams/{teamId}/conversations/`，直接发出 GET 请求。

唯一的`teamId`来源是来自团队上下文的邮件-来自用户的邮件，或者是在将你的 bot 添加到团队时接收的消息（请参阅[bot 或用户添加到团队](~/resources/bot-v3/bots-notifications.md#team-member-or-bot-addition)）。

> [!NOTE]
> 值往往是`serviceUrl`稳定的，但可能会发生变化。 当新邮件到达时，你的 bot 应验证其存储值`serviceUrl`。

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

下面的示例使用来自`FetchChannelList` Microsoft 团队分机号的 Microsoft 团队分机号的调用，用于[.Net 的机器人生成器 SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)：

```csharp
ConversationList channels = client.GetTeamsConnectorClient().Teams.FetchChannelList(activity.GetChannelData<TeamsChannelData>().Team.Id);
```

#### <a name="nodejs-example"></a>Node.js 示例

下面的示例使用`fetchChannelList`来自[Microsoft 团队扩展的来自用于 Node.js 的 Bot 生成器 SDK](https://www.npmjs.com/package/botbuilder-teams)的调用。

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
