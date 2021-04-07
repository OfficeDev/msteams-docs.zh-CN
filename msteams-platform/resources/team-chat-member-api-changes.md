---
title: 为团队和聊天成更改机器人 API
author: ojasvichoudhary
description: 介绍即将对用于检索团队和聊天成员的 Bot API 进行的更改和进行中的更改
keywords: 机器人框架 apis 团队成员名单
ms.topic: reference
ms.author: ojchoudh
ms.openlocfilehash: ee90c9c324f11e191cf596bcf8e27cd2bef41240
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596180"
---
# <a name="changes-to-teams-bot-apis-for-fetching-team-and-chat-members"></a>对用于提取团队和聊天成员的 Teams 自动程序 API 的更改

>[!NOTE]
> 我们开始使用和 API 的弃 `TeamsInfo.getMembers` `TeamsInfo.GetMembersAsync` 用过程。 最初，它们将被严格限制为每分钟 5 个请求，并且每个团队最多返回 10，000 个成员。 这样，随着团队规模增加，将不会返回整个名单。 
> 
> **必须更新到 4.10** 版或更高版本的 Bot Framework SDK，并切换到分页 API 终结点或 `TeamsInfo.GetMemberAsync` 单个用户 API。 这也适用于自动程序，即使你没有直接使用这些 API，因为较旧的 SDK 在 [membersAdded](../bots/how-to/conversations/subscribe-to-conversation-events.md#team-members-added) 事件期间调用这些 API。 若要查看即将进行的更改的列表，请参阅 API [更改](team-chat-member-api-changes.md#api-changes)。 

目前，想要检索聊天或团队的一个或多个成员信息的聊天机器人开发人员使用 microsoft Teams 自动程序 API (for C#) 或 `TeamsInfo.GetMembersAsync` (`TeamsInfo.getMembers` for TypeScript/Node.js) API [ (](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile)记录在此处) 。 这些 API 现在存在一些缺点：

* **对于大型团队，性能较差，超时的可能性较大。** 自 Microsoft Teams 于 2017 年初发布以来，最大团队规模已大幅提升。 由于 `GetMembersAsync` 返回整个成员列表，因此 API 调用需要很长时间来为大型团队返回，并且调用会花费很长时间来退出，因此必须 / `getMembers` 重试。
* **获取单个用户的配置文件详细信息很麻烦。** 若要获取单个用户的配置文件信息，您必须检索整个成员列表，然后搜索您想要的成员列表。 如果为 True，则 Bot Framework SDK 中提供了帮助程序函数，使其更简单，但实际上效率并不高。

另外，随着组织范围的团队的引入，我们意识到应该更好地将这些 API 与 Office 365 隐私控件保持一致：大型团队中使用的机器人能够检索基本个人资料信息，这类似于 Microsoft Graph 权限。 `User.ReadBasic.All` 租户管理员可大量控制哪些应用和机器人可以在租户中使用，但这些设置不同于管理 Microsoft Graph 的设置。

下面是这些 API 今天返回的示例 JSON 表示形式。 我将参考下面的一些字段。

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

下面是即将推出的 API 更改：

* 我们创建了一个新的 [`TeamsInfo.GetPagedMembersAsync`](~/bots/how-to/get-teams-context.md?tabs=dotnet#fetching-the-roster-or-user-profile) API，用于检索聊天/团队成员的个人资料信息。 此 API 现已与 Bot Framework 4.10 SDK 一起提供。 对于所有其他版本中的开发，请使用 [`GetConversationPagedMembers`](/dotnet/api/microsoft.bot.connector.conversationsextensions.getconversationpagedmembersasync?view=botbuilder-dotnet-stable&preserve-view=true) 方法。
  > [!NOTE]
  > 在 v3 或 v4 中，最佳操作是升级到最新点版本。
* 我们创建了一个新的 [`TeamsInfo.GetMemberAsync`](~/bots/how-to/get-teams-context.md?tabs=dotnet#get-single-member-details) API，用于检索单个用户的配置文件信息。 它将团队/聊天的 ID 和[UPN](https://docs.microsoft.com/windows/win32/ad/naming-properties#userprincipalname) (（请参阅上面的 `userPrincipalName`) 、Azure Active Directory 对象ID (、) 或 Teams 用户 ID `objectId` (，请参阅上面的 `id`) 作为参数，并返回该用户的配置文件信息。
  > [!NOTE]
  > 我们正在更改 `objectId` 以匹配在 Bot Framework 消息的对象 `aadObjectId` `Activity` 中调用的对象。 新 API 适用于 Bot Framework SDK 版本 4.10。 它将很快在 Teams SDK 扩展 Bot Framework 3.x 中提供;，您可以使用 [REST](~/bots/how-to/get-teams-context.md?tabs=json#get-single-member-details) 终结点。
* `TeamsInfo.GetMembersAsync` (C#)  (TypeScript/Node.js) 已正式弃用，并 `TeamsInfo.getMembers` 将于 2021 年后期停止工作。 Please update your bots to use the paged APIs.  (这也适用于这些 API 使用 [.) ](~/bots/how-to/get-teams-context.md?tabs=json)的基础 REST API
* 到 2021 年底，聊天机器人将无法主动检索聊天/团队成员的 或 属性，并且将需要使用 Microsoft Graph 来 `userPrincipalName` `email` 检索它们。 具体而言 `userPrincipalName` ， `email` 自 2021 年后期起，将不会从新 API 返回 `GetConversationPagedMembers` 属性。 机器人必须借助访问令牌使用 Microsoft Graph 来检索此信息。 这明显是一个主要更改：我们必须让机器人更轻松地获取访问令牌，并且必须简化和简化最终用户同意过程。

## <a name="feedback-and-more-information"></a>反馈和详细信息

我们将使用此页提供有关这些更改最新信息。 如果你有问题，请使用以下反馈部分>在此页面上发送 **反馈** "。
