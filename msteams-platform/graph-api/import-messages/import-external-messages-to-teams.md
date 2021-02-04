---
title: 使用 Microsoft Graph 将外部平台消息导入 Teams
description: 介绍如何使用 Microsoft Graph 将邮件从外部平台导入 Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: teams 导入消息 api graph microsoft 迁移迁移文章
ms.openlocfilehash: 97f24c34ebb825aad0fd104c9a814e46f9b5fa0d
ms.sourcegitcommit: f74b74d5bed1df193e59f46121ada443fb57277b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093258"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>使用 Microsoft Graph 将第三方平台消息导入 Teams

>[!IMPORTANT]
> Microsoft Graph 和 Microsoft Teams 公共预览版可用于早期访问和反馈。 尽管此版本已经过大量测试，但不适合在生产中使用。

使用 Microsoft Graph，可以将用户的现有邮件历史记录和数据从外部系统迁移到 Teams 频道。 通过支持在 Teams 内恢复第三方平台消息层次结构，用户可以继续无缝通信，并且无需中断。

## <a name="import-overview"></a>导入概述

在高级别上，导入过程由以下内容组成：

1. [创建具有返回时间戳的团队](#step-one-create-a-team)
1. [创建具有返回时间戳的频道](#step-two-create-a-channel)  
1. [导入外部实时日期消息](#step-three-import-messages)
1. [完成团队和频道迁移过程](#step-four-complete-migration-mode)
1. [添加团队成员](#step-five-add-team-members)

## <a name="necessary-requirements"></a>所需要求

### <a name="analyze-and-prepare-message-data"></a>分析和准备邮件数据

✔查看第三方数据，以决定要迁移哪些内容。  
✔从第三方聊天系统提取所选数据。  
✔将第三方聊天结构映射到 Teams 结构。  
✔将导入数据转换为迁移所需的格式。  

### <a name="set-up-your-office-365-tenant"></a>设置 Office 365 租户

✔确保导入数据存在 Office 365 租户。 有关为 Teams 设置 Office 365 租户详细信息，请参阅"[准备 Office 365 租户"。](../../concepts/build-and-test/prepare-your-o365-tenant.md)  
✔确保团队成员在 Azure Active Directory (AAD) 。  有关详细信息，*请参阅将*[新用户添加到](/azure/active-directory/fundamentals/add-users-azure-active-directory)Azure Active Directory。

## <a name="step-one-create-a-team"></a>步骤 1：创建团队

由于正在迁移现有数据，因此在迁移过程中维护原始邮件时间戳并阻止邮件活动是在 Teams 中重新创建用户的现有邮件流的关键。 实现此目的，如下所示：

> [使用工作组资源](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) 属性创建一个时间戳返回的新  `createdDateTime`  团队。 将新团队放在一种特殊状态中，在迁移过程完成之前，会禁止用户参与团队中的 `migration mode` 大多数活动。 在 POST 请求中将实例属性与值一起包含，以明确标识要创建的 `teamCreationMode` `migration` 迁移新团队。  

> **注意**：将仅为已迁移的团队或频道的实例 `createdDateTime` 填充该字段。

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>权限

|ScopeName|DisplayName|说明|类型|管理员同意？|涵盖的实体/API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|管理迁移到 Microsoft Teams|创建、管理迁移到 Microsoft Teams 的资源|**仅应用程序**|**是**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>请求 (迁移状态创建) 

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.043Z"
}
```

#### <a name="response"></a>响应

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/operations/{operationId}
Content-Location: /teams/{teamId}
```

#### <a name="error-messages"></a>错误消息

```http
400 Bad Request
```

* `createdDateTime`  设置为将来。
* `createdDateTime`  正确指定，但 `teamCreationMode`  实例属性缺失或设置为无效值。

## <a name="step-two-create-a-channel"></a>步骤 2：创建通道

为导入的邮件创建频道与创建团队方案类似：

> [使用通道资源](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) 属性创建一个时间戳返回的新 `createdDateTime` 通道。 将新频道放在一种特殊状态中，在迁移过程完成之前，会禁止用户参与频道内大多数 `migration mode` 聊天活动。  在 POST 请求中将实例属性与值一起包含，以明确标识要创建的 `channelCreationMode` `migration` 迁移新团队。  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>权限

|ScopeName|DisplayName|说明|类型|管理员同意？|涵盖的实体/API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|管理迁移到 Microsoft Teams|创建、管理迁移到 Microsoft Teams 的资源|**仅应用程序**|**是**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>请求 (在迁移状态创建) 

```http
POST https://graph.microsoft.com/beta/teams/{id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.047Z"
}
```

#### <a name="response"></a>响应

```http
HTTP/1.1 202 Accepted

{
   "@odata.context":"https://canary.graph.microsoft.com/testprodbetateamsgraphsvcncus/$metadata#teams('9cc6d6ab-07d8-4d14-bc2b-7db8995d6d23')/channels/$entity",
   "id":"19:e90f6814ce674072a4126206e7de485e@thread.tacv2",
   "createdDateTime":null,
   "displayName":"Architecture Discussion",
   "description":"This channel is where we debate all future architecture plans",
   "isFavoriteByDefault":null,
   "email":null,
   "webUrl":null,
   "membershipType":null,
   "moderationSettings":null
}
```

#### <a name="error-message"></a>错误消息

```http
400 Bad Request
```

* `createdDateTime`  设置为将来。
* `createdDateTime`  正确指定， `channelCreationMode`  但实例属性缺失或设置为无效值。

## <a name="step-three-import-messages"></a>步骤 3：导入邮件

创建团队和频道后，可以使用请求正文中的 and 键开始发送返回 `createdDateTime` `from`  时间消息。 **注意**：不支持使用邮件 `createdDateTime` 线程之前导入 `createdDateTime` 的邮件。

> [!NOTE]
> * `createdDateTime` 在同一线程中的邮件之间必须是唯一的。
> * `createdDateTime` 支持精度为毫秒的时间戳。 例如，如果传入请求邮件的值设置为 `createdDateTime` *2020-09-16T05：50：31.0025302Z，* 那么在接收邮件时，它将转换为 *2020-09-16T05：50：31.002Z。*

#### <a name="request-post-message-that-is-text-only"></a>请求 (文本格式的 POST) 

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
   "createdDateTime":"2019-02-04T19:58:15.511Z",
   "from":{
      "user":{
         "id":"id-value",
         "displayName":"Joh Doe",
         "userIdentityType":"aadUser"
      }
   },
   "body":{
      "contentType":"html",
      "content":"Hello World"
   }
}
```

#### <a name="response"></a>响应

```http
HTTP/1.1 200 OK

{
   "@odata.context":"https://graph.microsoft.com/beta/$metadata#teams('teamId')/channels('channelId')/messages/$entity",
   "id":"id-value",
   "replyToId":null,
   "etag":"id-value",
   "messageType":"message",
   "createdDateTime":"2019-02-04T19:58:15.58Z",
   "lastModifiedDateTime":null,
   "deleted":false,
   "subject":null,
   "summary":null,
   "importance":"normal",
   "locale":"en-us",
   "policyViolation":null,
   "from":{
      "application":null,
      "device":null,
      "conversation":null,
      "user":{
         "id":"id-value",
         "displayName":"Joh Doe",
         "userIdentityType":"aadUser"
      }
   },
   "body":{
      "contentType":"html",
      "content":"Hello World"
   },
   "attachments":[
   ],
   "mentions":[
   ],
   "reactions":[
   ]
}
```

#### <a name="error-messages"></a>错误消息

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a>请求 (内联图像消息的 POST) 

> **注意**：此方案中没有特殊权限范围，因为请求是 chatMessage 的一部分;chatMessage 的范围也适用于此处。

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
  "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"../hostedContents/1/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "hostedContents":[
        {
            "@microsoft.graph.temporaryId": "1",
            "contentBytes": "iVBORw0KGgoAAAANSUhEUgAAANcAAAExCAYAAADvFzeeAAAXjklEQVR4Ae2d/XNU1RnH+9e0FFrA0RCIyaS8hRA0HV5KbS1gHRgVpjMClY4GHJ3yYm1HCmXaWttaaZUZtIIFKYi8lFAkvOQ9u5vN225IARVBbX9/Os9NbrLZbMjmhCfJPX5+2Lmb3T25y3O+n/M599x7w9f+++UXwoMakIF7n4GvUdR7X1RqSk01A8CFuZm5GGUAuIwKi72wF3ABF+YyygBwGRUWc2Eu4AIuzGWUAeAyKizmwlzABVyYyygDwGVUWMyFuYALuDCXUQaAy6iwmAtzARdwfWXMdeuzT+TGxz3Sfb1LunrapL07IW3pePDQ5/qavqef0c+OdYAELuAac4jGGkLL9rdvfyo9N9ODQAqBGmmrwGlb/R0u3xG4gMspOC5hG882CoRaaCSA8n1ff9doIQMu4PIOrus3u+8ZVNnw6e/Od5AALuDKOyz5hmqiPnfnzi1J9bSbgRWCpvvQfY307wQu4BoxJCOFaDK8rwsQmQsUIQhWW93XSIsewAVckYdLQ24F0Ui/926AARdwRRounZ6Np7GyYdN9DzdFBC7gijRc43GMlQ1U9s/6HXJNjYELuHI<<-----Removed----->>>>",
            "contentType": "image/png"
        }
    ]
}
```

#### <a name="response"></a>响应

```http
HTTP/1.1 200 OK

{
    "@odata.context": "https://graph.microsoft.com/beta/$metadata#teams('teamId')/channels('channelId')/messages/$entity",
    "id": "id-value",
    "replyToId": null,
    "etag": "id-value",
    "messageType": "message",
    "createdDateTime": "2019-02-04T19:58:15.511Z",
    "lastModifiedDateTime": null,
    "deleted": false,
    "subject": null,
    "summary": null,
    "importance": "normal",
    "locale": "en-us",
    "policyViolation": null,
    "from": {
        "application": null,
        "device": null,
        "conversation": null,
        "user": {
            "id": "id-value",
            "displayName": "Joh Doe",
            "userIdentityType": "aadUser"
        }
    },
      "body": {
        "contentType": "html",
        "content": "<div><div>\n<div><span><img height=\"250\" src=\"https://graph.microsoft.com/teams/teamId/channels/channelId/messages/id-value/hostedContents/hostedContentId/$value\" width=\"176.2295081967213\" style=\"vertical-align:bottom; width:176px; height:250px\"></span>\n\n</div>\n\n\n</div>\n</div>"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

## <a name="step-four-complete-migration-mode"></a>步骤 4：完成迁移模式

邮件迁移过程完成后，使用该方法将团队和频道从迁移  `completeMigration`  模式退出。 此步骤将打开团队和频道资源，供团队成员常规使用。 该操作绑定到 `team` 实例。

#### <a name="request-end-team-migration-mode"></a>请求 (团队迁移模式) 

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a>响应

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a>请求 (通道迁移模式) 

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/completeMigration

```

#### <a name="response"></a>响应

```http
HTTP/1.1 204 NoContent
```

#### <a name="error-response"></a>错误响应

```http
400 Bad Request
```

* 对或不在 `team` `channel` 中调用的操作 `migrationMode` 。

## <a name="step-five-add-team-members"></a>步骤 5：添加团队成员

可以使用 Teams [UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) 或 Microsoft Graph 添加成员 API 将成员 [添加到团队](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) ：

#### <a name="request-add-member"></a>请求 (成员) 

```http
POST https://graph.microsoft.com/beta/teams/{id}/members
Content-type: application/json
Content-length: 30
{
"@odata.type": "#microsoft.graph.aadUserConversationMember",
"roles": [],
"user@odata.bind": "https://graph.microsoft.com/beta/users/{user-id}"
}
```

#### <a name="response"></a>响应

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a>提示和其他信息

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* 你可以从不在 Teams 中的用户导入邮件。 **注意**：为租户中不存在的用户导入的邮件在公共预览版期间在 Teams 客户端或合规性门户中不可搜索。

* 提出 `completeMigration` 请求后，无法向团队导入进一步的消息。

* 只有在请求返回成功响应后，才能将团队成员 `completeMigration` 添加到新团队。

* 限制：邮件按每个通道 5 RPS 导入。

* 如果需要更正迁移结果，需要删除该团队，并重复这些步骤以创建团队和频道并重新迁移邮件。

> [!NOTE]
> 目前，内联图像是导入邮件 API 架构唯一支持的媒体类型。

##### <a name="import-content-scope"></a>导入内容范围

|作用域内 | 当前超出范围|
|----------|--------------------------|
|团队和频道消息|1：1 和群聊消息|
|原始邮件的创建时间|专用频道|
|作为邮件一部分的内联图像|在提及时|
|指向 SPO/OneDrive 中的现有文件的链接|反应|
|包含格式文本的邮件|视频|
|邮件回复链|公告|
|高吞吐量处理|代码段|
||自适应卡片|
||贴纸|
||表情符号|
||引号|
||跨渠道发布|

> [!div class="nextstepaction"]
>[详细了解 Microsoft Graph 和 Teams 集成](/graph/teams-concept-overview)
