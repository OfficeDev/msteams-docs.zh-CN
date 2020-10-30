---
title: 团队/聊天成员 (2020 更新) 的 Bot API 更改
author: ojasvichoudhary
description: 介绍用于检索团队和聊天成员的 Bot Api 的即将进行和正在进行的更改
keywords: bot 框架 api 团队成员名单
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: 243969796d9d1dc427ab7736cf5e0f0d320731c7
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796139"
---
# <a name="changes-to-teams-bot-apis-for-fetching-teamchat-members"></a>对用于提取团队/聊天成员的团队 Bot Api 的更改

目前，要检索聊天或团队的一个或多个成员的信息的 bot 开发人员使用 Microsoft 团队 bot Api `TeamsInfo.GetMembersAsync` (For c # ) 或 `TeamsInfo.getMembers` (的 TypeScript/Node.js) api ([ 在此处) 记录 ](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetching-the-roster-or-user-profile)。 这些 Api 目前有几项缺点：

* **对于大型团队，性能较差且超时更有可能。** 由于 Microsoft 团队在早期2017发布，因此团队的最大大小已大大增加。 由于 `GetMembersAsync` / `getMembers` 返回整个成员列表，API 调用为大型团队返回的时间较长，因此调用超时并不常见，您必须重试。
* **获取单个用户的配置文件详细信息非常麻烦。** 若要获取单个用户的配置文件信息，您必须检索整个成员列表，然后搜索所需的成员列表。 True，在 Bot 框架 SDK 中有一个 helper 函数可使其更简单，但在覆盖它的效率不高的情况下。

此外，随着组织范围内的团队的推出，我们已意识到，可以更好地将这些 Api 与 Office 365 隐私控件对齐：大型团队中使用的 bot 能够检索基本配置文件信息，这与 `User.ReadBasic.All` Microsoft Graph 权限类似。 租户管理员可以很好地控制可在其租户中使用的应用程序和 bot，但这些设置不同于控制 Microsoft Graph 的用户。

下面是这些 Api 的当前返回内容的示例 JSON 表示形式。 我将参考下面的一些字段。

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
以下是即将发布的 API 更改：

* 我们创建了一个新的 API [`TeamsInfo.GetPagedMembersAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#fetching-the-roster-or-user-profile) ，用于检索聊天/团队成员的配置文件信息。 此 API 现在可在 Bot 框架 4.8 SDK 中使用。 若要在所有其他版本中进行开发，请使用 [`GetConversationPagedMembers`](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable) 方法。 **注意** ：在 v3 或 v4 中，最佳操作是分别升级到最新的点 (3.30.2 或 4.8) 。 
* 我们创建了一个新的 API [`TeamsInfo.GetMemberAsync`](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=dotnet#get-single-member-details) ，用于检索单个用户的配置文件信息。 它采用团队/聊天和 [UPN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) (的 ID `userPrincipalName` ， *请参阅以上* ) 的 Azure Active Directory 对象 ID (`objectId` ， *参阅以上* ) 或团队用户 ID (`id` ，请 *参阅以上* ) 作为参数，并返回该用户的配置文件信息。 **注意** ：我们正在将更改 `objectId` 为， `aadObjectId` 以匹配在 `Activity` Bot 框架消息的对象中调用的内容。 在 Bot 框架 SDK 的4.8 版中提供了新的 API。 此外，还将在团队 SDK 扩展 Bot Framework 3 中提供此功能。同时，您可以使用 [REST](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#get-single-member-details) 终结点。
* `TeamsInfo.GetMembersAsync` (c # ) 和 `TeamsInfo.getMembers` (TypeScript/Node.js) 已正式弃用，并将在后期2021中停止工作。 我们将根据开发人员的反馈，在5月2020日宣布特定的时间表。 一旦新的页面调度 API 可用，开发人员就应更新其机器人以使用它。  (这也适用于 [这些 api 使用的基础 REST API](https://docs.microsoft.com/microsoftteams/platform/bots/how-to/get-teams-context?tabs=json#tabpanel_CeZOj-G++Q_json)。 ) 
* 通过后期2021，bot 将无法主动检索 `userPrincipalName` `email` 聊天/团队成员的或属性，并且需要使用 Microsoft Graph 来检索它们。 具体说来， `userPrincipalName` `email` 不会从晚2021开始的新 API 中返回属性 `GetConversationPagedMembers` 。 Bot 必须使用具有访问令牌的 Microsoft Graph 来检索此信息。 这显然是一项重大更改：我们必须让 bot 更轻松地获取访问令牌，并且我们必须优化和简化最终用户同意过程。

## <a name="feedback-and-more-information"></a>反馈和详细信息
我们将使用此页面提供有关这些更改的最新信息。 如果有问题，请使用下面 " **反馈** " 部分中的 "发送反馈 > 此页面"。 
