---
title: 为团队和聊天成更改机器人 API
author: ojasvichoudhary
description: 介绍即将对用于检索团队和聊天成员的 Bot API 进行的更改和进行中的更改
keywords: 机器人框架 apis 团队成员名单
localization_priority: Normal
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: d2eb75a69100a6daaf3af3a021b9896c42abe5f1
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114243"
---
# <a name="teams-bot-api-changes-to-fetch-team-or-chat-members"></a>Teams自动程序 API 更改以提取团队或聊天成员

>[!NOTE]
> 和 API 的弃用 `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` 过程已启动。 最初，它们被严格限制为每分钟五个请求，并且每个团队最多返回 10，000 个成员。 这样，随着团队规模增加，不会返回全部名单。
> 必须更新到 4.10 版或更高版本的 Bot Framework SDK，并切换到分页 API 终结点或 `TeamsInfo.GetMemberAsync` 单个用户 API。 这也适用于自动程序，即使你未直接使用这些 API，因为较旧的 SDK 在 [membersAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) 事件期间调用这些 API。 若要查看即将进行的更改的列表，请参阅 API [更改](team-chat-member-api-changes.md#api-changes)。 

目前，要检索聊天或团队的一个或多个成员信息的聊天机器人开发人员使用 Microsoft Teams 自动程序 API C# 或 `TeamsInfo.GetMembersAsync` TypeScript 或 `TeamsInfo.getMembers` Node.js API。 有关详细信息，请参阅提取 [名单或用户配置文件](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)。 这些 API 存在一些缺点。

目前，如果要检索聊天或团队的一个或多个成员的信息，可以使用[Microsoft Teams 自动](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile)程序 API C# 或 TypeScript 或 `TeamsInfo.GetMembersAsync` Node.js `TeamsInfo.getMembers` API。 这些 API 有以下缺点：

* 对于大型团队，性能较差且超时的可能性较大：自 2017 年初发布以来，最大团队Teams大大增加。 作为或返回整个成员列表，对于大型团队，API 调用需要很长时间来返回，并且调用通常要过长，必须 `GetMembersAsync` `getMembers` 重试。
* 获取单个用户的配置文件详细信息非常困难：若要获取单个用户的配置文件信息，您必须检索整个成员列表，然后搜索您想要的成员列表。 Bot Framework SDK 中提供了一个帮助程序函数，使其更简单，但效率并不高。

随着组织范围的团队的引入，需要更好地使这些 API 与Office 365保持一致。 大型团队中使用的机器人能够检索基本个人资料信息，类似于 Microsoft Graph `User.ReadBasic.All` 权限。 租户管理员可大量控制可以在租户中使用的应用和机器人，但这些设置不同于 Microsoft Graph。

以下代码提供了由自动程序 API 返回Teams JSON 表示形式：

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

以下是即将推出的 API 更改：

* 将创建一个新的 [`TeamsInfo.GetPagedMembersAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetch-the-roster-or-user-profile) API，用于检索聊天或团队成员的配置文件信息。 此 API 现已与 Bot Framework 版本 4.8 或更高版本 SDK 一起提供。 对于所有其他版本中的开发，请使用 [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) 方法。

    > [!NOTE]
    > 在 v3 或 v4 中，最佳操作是升级到分别为 3.30.2 或 4.8 或更高版本的最新点版本。

* 将创建一个新的 [`TeamsInfo.GetMemberAsync`](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) API，用于检索单个用户的配置文件信息。 它将团队或聊天的 ID 和[UPN（](/windows/win32/ad/naming-properties#userprincipalname)即 Azure Active Directory 对象 ID 或 Teams 用户 ID）作为参数，并返回该用户的 `userPrincipalName` `objectId` `id` 配置文件信息。

    > [!NOTE]
    > `objectId` 更改为匹配 `aadObjectId` Bot Framework 消息的对象 `Activity` 中调用的对象。 新 API 适用于 4.8 版或更高版本的 Bot Framework SDK。 它还在 Teams SDK 扩展 Bot Framework 3.x 中提供。 同时，您可以使用 [REST](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) 终结点。

* `TeamsInfo.GetMembersAsync` 中C# TypeScript 或 `TeamsInfo.getMembers` Node.js已正式弃用。 新 API 可用后，必须更新机器人以使用它。 这也适用于这些 API[使用的基础 REST API。](/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)
* 到 2022 年底，聊天机器人无法主动检索 `userPrincipalName` 聊天或 `email` 团队成员的 或 属性。 机器人必须使用Graph来检索它们。 从 `userPrincipalName` `email` `GetConversationPagedMembers` 2022 年后期开始，不会从新 API 返回 和 属性。 自动程序必须Graph访问令牌来检索信息。 机器人必须更轻松地获取访问令牌，并简化和简化最终用户同意过程。
