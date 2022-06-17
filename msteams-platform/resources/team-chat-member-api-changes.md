---
title: 为团队和聊天成更改机器人 API
author: ojasvichoudhary
description: 在本模块中，了解用于检索团队成员和聊天成员的机器人 API 即将进行的更改和正在进行的更改
ms.localizationpriority: medium
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 5f5bb009abd5a9e0dc8a14d0bea5bdd0f43a71c9
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66142323"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Teams 机器人 API 在提取团队或聊天成员方面的更改

>[!NOTE]
> `TeamsInfo.getMembers` 和 `TeamsInfo.GetMembersAsync` API 的弃用过程已启动。 最初，它们被严格限制为每分钟 5 个请求，并且每个团队最多返回 1 万个成员。 这导致随着团队规模的增加，不会返回完整的名单。
> 必须更新到 Bot Framework SDK 版本 4.10 或更高版本，并切换到分页 API 终结点或 `TeamsInfo.GetMemberAsync` 单用户 API。 即使未直接使用这些 API，这也适用于你的机器人，因为旧版 SDK 在 [membersAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#members-added) 事件期间会调用这些 API。 若要查看即将进行的更改的列表，请参阅 [API 更改](team-chat-member-api-changes.md#api-changes)。

目前，如果要检索聊天或团队的一个或多个成员的信息，可以使用 [Microsoft Teams 机器人 API](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) `TeamsInfo.GetMembersAsync`（对于 C#）或 `TeamsInfo.getMembers`（对于 TypeScript 或 Node.js API）。 有关详细信息，请参阅[提取名单或用户个人资料](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)。

这些 API 有以下缺点：

* 对于大型团队，性能较差且超时的可能性更大：自 2017 年初发布 Teams 以来，最大团队规模已大幅增加。 作为 `GetMembersAsync` 或 `getMembers` 返回整个成员列表，API 调用需要很长时间才能返回大型团队，并且调用超时是很常见的，必须重试。
* 获取单个用户的个人资料详细信息很困难：若要获取单个用户的个人资料信息，必须检索整个成员列表，然后搜索所需的用户。 Bot Framework SDK 中有一个帮助程序函数，可使其更简单，但效率不高。

随着组织范围团队的引入，需要更好地将这些 API 与Office 365隐私控制保持一致。 大型团队中使用的机器人能够检索类似于 `User.ReadBasic.All` Microsoft Graph 权限的基本个人资料信息。 租户管理员可以很好地控制哪些应用和机器人可在其租户中使用，但这些设置不同于 Microsoft Graph。

以下代码提供 Teams 机器人 API 返回的内容的示例 JSON 表示形式：

```json
[{
    "id": "29:1GcS4EyB_oSI8A88XmWBN7NJFyMqe3QGnJdgLfFGkJnVelzRGos0bPbpsfJjcbAD22bmKc4GMbrY2g4JDrrA8vM06X1-cHHle4zOE6U4ttcc",
    "name": "Anon1 (Guest)",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
 "userRole": "anonymous"
}, {
    "id": "29:1bSnHZ7Js2STWrgk6ScEErLk1Lp2zQuD5H2qQ960rtvstKp8tKLl-3r8b6DoW0QxZimuTxk_kupZ1DBMpvIQQUAZL-PNj0EORDvRZXy8kvWk",
    "objectId": "76b0b09f-d410-48fd-993e-84da521a597b",
    "givenName": "John",
    "surname": "Patterson",
    "email": "johnp@fabrikam.com",
    "userPrincipalName": "johnp@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
 "userRole": "user"
}, {
    "id": "29:1URzNQM1x1PNMr1D7L5_lFe6qF6gEfAbkdG8_BUxOW2mTKryQqEZtBTqDt10-MghkzjYDuUj4KG6nvg5lFAyjOLiGJ4jzhb99WrnI7XKriCs",
    "objectId": "6b7b3b2a-2c4b-4175-8582-41c9e685c1b5",
    "givenName": "Rick",
    "surname": "Stevens",
    "email": "Rick.Stevens@fabrikam.com",
    "userPrincipalName": "rstevens@fabrikam.com",
    "tenantId":"72f988bf-86f1-41af-91ab-2d7cd011db47",
 "userRole": "user"
}]
```

## <a name="api-changes"></a>API 更改

下面是即将进行的 API 更改：

* 将创建新 API [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)，用于检索聊天或团队成员的个人资料信息。 此 API 现在适用于 Bot Framework 版本 4.8 或更高版本的 SDK。 若要在所有其他版本中进行开发，请使用 [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) 方法。

    > [!NOTE]
    > 在 v3 或 v4 中，最佳操作是升级到最新版，分别为 3.30.2 或 4.8 或更高版本。

* 将创建新 API [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details)，用于检索单个用户的个人资料信息。 它使用团队或聊天的 ID 和 [UPN](/windows/win32/ad/naming-properties#userprincipalname)（即 `userPrincipalName`）、Microsoft Azure Active Directory (Azure AD) 对象 ID `objectId` 或 Teams 用户 ID `id` 作为参数，并返回该用户的个人资料信息。

    > [!NOTE]
    > `objectId` 更改为 `aadObjectId` 以匹配 Bot Framework 消息的 `Activity` 对象中调用的内容。 新 API 适用于版本 4.8 或更高版本的 Bot Framework SDK。 它还可在 Teams SDK 扩展 Bot Framework 3.x 中使用。 同时，可以使用 [REST](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) 终结点。

* C# 中的 `TeamsInfo.GetMembersAsync` 和 TypeScript 或 Node.js 中的 `TeamsInfo.getMembers` 已正式弃用。 新 API 可用后，必须更新机器人才能使用它。 这也适用于[这些 API 使用的基础 REST API](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)。
* 到 2022 年底，机器人无法主动检索聊天或团队成员的 `userPrincipalName` 或 `email` 属性。 机器人必须使用Graph API 来检索所需的信息。 从 2022 年末开始，新 `GetConversationPagedMembers` API 无法返回 `userPrincipalName` 和 `email` 属性。 机器人必须将 Graph API 与访问令牌配合使用才能检索信息。 
