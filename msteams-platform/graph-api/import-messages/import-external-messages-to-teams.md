---
title: 使用 Microsoft Graph 将外部平台消息导入 Teams
description: 介绍如何使用 Microsoft Graph 将邮件从外部平台导入到 Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams 导入消息 api 图形 Microsoft 迁移迁移帖子
ms.openlocfilehash: 8cf4f964aba7ce9375b1b259ae88a7fbcb620631
ms.sourcegitcommit: f6e4a303828224a702138753a8e5e27c8a094c82
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/24/2021
ms.locfileid: "51176954"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>使用 Microsoft Graph 将第三方平台消息导入 Teams

>[!IMPORTANT]
> Microsoft Graph 和 Microsoft Teams 公共预览版可用于早期访问和反馈。 尽管此版本已经过大量测试，但不适合在生产中使用。

使用 Microsoft Graph，可以将用户的现有邮件历史记录和数据从外部系统迁移到 Teams 频道。 通过支持在 Teams 内恢复第三方平台消息层次结构，用户可以无缝地继续通信并不间断地继续。

> [!NOTE] 
> 将来，Microsoft 可能要求你或你的客户根据导入的数据量支付其他费用。

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
✔第三方聊天系统提取所选数据。  
✔将第三方聊天结构映射到 Teams 结构。  
✔将导入数据转换为迁移所需的格式。  

### <a name="set-up-your-office-365-tenant"></a>设置 Office 365 租户

✔确保导入数据存在 Office 365 租户。 有关为 Teams 设置 Office 365 租户的信息，请参阅准备[Office 365 租户](../../concepts/build-and-test/prepare-your-o365-tenant.md)。  
✔确保团队成员在 Azure Active Directory (AAD) 。  有关详细信息，*请参阅将*[新用户添加到](/azure/active-directory/fundamentals/add-users-azure-active-directory)Azure Active Directory。

## <a name="step-one-create-a-team"></a>步骤 1：创建团队

由于正在迁移现有数据，因此在迁移过程中保留原始邮件时间戳并阻止邮件活动对于在 Teams 中重新创建用户的现有邮件流很关键。 实现此目的：：

> [使用 team 资源](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) 属性创建具有返回时间戳的新  `createdDateTime`  团队。 将新团队放在 `migration mode` 中，这是一种特殊状态，可禁止用户参与团队中的大多数活动，直到迁移过程完成。 在 POST 请求中包括具有 值的 instance 属性，以明确标识正在创建 `teamCreationMode` `migration` 用于迁移的新团队。  

> **注意** `createdDateTime` ：将仅为已迁移的团队或频道的实例填充该字段。

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

* `createdDateTime`  设置供将来使用。
* `createdDateTime`  正确指定，但 `teamCreationMode`  实例属性缺失或设置为无效值。

## <a name="step-two-create-a-channel"></a>步骤 2：创建通道

为导入的消息创建频道与创建团队方案类似：

> [使用 channel 资源](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) 属性创建具有返回时间戳的新 `createdDateTime` 频道。 将新频道放在 中，这是一种特殊状态，可禁止用户参与频道内大多数聊天活动，直到 `migration mode` 迁移过程完成。  在 POST 请求中包括具有 值的 instance 属性，以明确标识正在创建 `channelCreationMode` `migration` 用于迁移的新团队。  
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

* `createdDateTime`  设置供将来使用。
* `createdDateTime`  正确指定， `channelCreationMode`  但实例属性缺失或设置为无效值。

## <a name="step-three-import-messages"></a>步骤 3：导入邮件

创建团队和频道后，可以使用 请求正文中的 和 键开始发送返回 `createdDateTime` `from`  时间消息。 **注意**：不支持使用早于 `createdDateTime` 消息线程导入 `createdDateTime` 的邮件。

> [!NOTE]
> * `createdDateTime` 对于同一线程中的消息，必须是唯一的。
> * `createdDateTime` 支持具有毫秒精度的时间戳。 例如，如果传入请求邮件的值设置为 `createdDateTime` *2020-09-16T05：50：31.0025302Z，* 那么在接收邮件时，它将转换为 *2020-09-16T05：50：31.002Z。*

#### <a name="request-post-message-that-is-text-only"></a>请求 (纯文本的 POST) 

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

#### <a name="request-post-a-message-with-inline-image"></a>请求 (内联图像消息 POST) 

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

完成邮件迁移过程后，团队和频道均会使用 方法退出迁移  `completeMigration`  模式。 此步骤将打开工作组和频道资源，供工作组成员常规使用。 操作绑定到 `team` 实例。

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

* 对 不在 `team` 中的 或 `channel` 调用的操作 `migrationMode` 。

## <a name="step-five-add-team-members"></a>步骤 5：添加团队成员

可以使用 Teams UI 或 Microsoft Graph 添加成员 [API](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) 将成员 [添加到](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) 团队：

#### <a name="request-add-member"></a>请求 (添加成员) 

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

* 你可以从不在 Teams 中的用户导入消息。 **注意**：在公共预览版期间，为租户中不存在的用户导入的消息在 Teams 客户端或合规性门户中不可搜索。

* 提出 `completeMigration` 请求后，你将无法将进一步的消息导入团队。

* 仅在请求返回成功响应后，才能将团队成员 `completeMigration` 添加到新团队。

* 限制：邮件以每个通道 5 RPS 的速度导入。

* 如果需要更正迁移结果，则需要删除该团队，并重复这些步骤以创建团队和频道，然后重新迁移邮件。

> [!NOTE]
> 目前，内联图像是导入邮件 API 架构支持的唯一媒体类型。

##### <a name="import-content-scope"></a>导入内容范围

|范围内 | 当前超出范围|
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


## <a name="see-also"></a>另请参阅
> [!div class="nextstepaction"]
>[详细了解 Microsoft Graph 和 Teams 集成](/graph/teams-concept-overview)
