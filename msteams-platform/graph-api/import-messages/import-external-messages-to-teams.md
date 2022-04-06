---
title: 使用 Microsoft Graph 将外部平台消息导入到Teams
description: 介绍如何使用 Microsoft Graph将消息从外部平台导入到Teams
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: Overview
keywords: teams 导入消息 api graph microsoft 迁移后
ms.openlocfilehash: 5a33334367d0f5c229874decd5e45c5bb89ceafc
ms.sourcegitcommit: f892125106adb6731a20127f15d6e92f279127c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2022
ms.locfileid: "64685630"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>使用 Microsoft Graph 将第三方平台消息导入 Teams

借助 Microsoft Graph，可以将用户的现有消息历史记录和数据从外部系统迁移到Teams通道。 通过在Teams中启用第三方平台消息传送层次结构的重新创建，用户可以无缝地继续其通信，并且不会中断。

> [!NOTE]
> 将来，Microsoft 可能要求你或你的客户根据导入的数据量支付其他费用。

## <a name="import-overview"></a>导入概述

在高级别上，导入过程包括以下内容：

1. [创建具有时间后退戳的团队](#step-1-create-a-team)。
1. [使用时间后退戳创建通道](#step-2-create-a-channel)。
1. [导入外部时间后退日期消息](#step-3-import-messages)。
1. [完成团队和频道迁移过程](#step-4-complete-migration-mode)。
1. [添加团队成员](#step-five-add-team-members)。

## <a name="prerequisites"></a>先决条件

### <a name="analyze-and-prepare-message-data"></a>分析和准备消息数据

* 查看第三方数据，确定要迁移的内容。  
* 从第三方聊天系统中提取所选数据。  
* 将第三方聊天结构映射到Teams结构。  
* 将导入数据转换为迁移所需的格式。  

### <a name="set-up-your-office-365-tenant"></a>设置 Office 365 租户

* 确保导入数据存在Office 365租户。 有关为Teams设置Office 365租户的详细信息，请参阅[准备Office 365租户](../../concepts/build-and-test/prepare-your-o365-tenant.md)。
* 确保团队成员处于Azure Active Directory状态。 有关详细信息，请参阅[将新用户添加](/azure/active-directory/fundamentals/add-users-azure-active-directory)到Azure AD。

## <a name="step-1-create-a-team"></a>步骤 1：创建团队

由于要迁移现有数据，因此，在迁移过程中保留原始消息时间戳和阻止消息传送活动是重新创建用户在Teams中的现有消息流的关键。 实现此目的如下所示：

> 使用团队资源`createdDateTime`属性创建具有后退时间戳[的新团队](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true)。 将新团队 `migration mode`置于特殊状态，在迁移过程完成之前限制用户参与团队中的大多数活动。 `teamCreationMode`在 POST 请求中包含具有值的`migration`实例属性，以显式标识要为迁移创建的新团队。  

> [!NOTE]
> 该 `createdDateTime` 字段将仅针对已迁移的团队或频道的实例进行填充。

<!-- markdownlint-disable MD001 -->

#### <a name="permission"></a>权限

|ScopeName|DisplayName|说明|类型|管理员同意？|涵盖的实体/API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|管理迁移到 Microsoft Teams|创建和管理用于迁移到Microsoft Teams的资源。|**仅限应用程序**|**是**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>请求 (创建处于迁移状态的团队) 

```http
POST https://graph.microsoft.com/v1.0/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/v1.0/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description",
  "createdDateTime": "2020-03-14T11:22:17.043Z"
}
```

#### <a name="response"></a>响应

```http
HTTP/1.1 202 Accepted
Location: /teams/{team-id}/operations/{operation-id}
Content-Location: /teams/{team-id}
```

#### <a name="error-message"></a>错误消息

```http
400 Bad Request
```

可在以下方案中收到错误消息：

* 如果 `createdDateTime` 已设置为将来。
* 如果 `createdDateTime` 指定正确，但 `teamCreationMode` 实例属性缺失或设置为无效值。

## <a name="step-2-create-a-channel"></a>步骤 2：创建通道

为导入的消息创建通道类似于创建团队方案：

> 使用通道资源`createdDateTime`属性创建具有后退时间戳[的新通道](/graph/api/channel-post?view=graph-rest-v1.0&tabs=http&preserve-view=true)。 将新频道 `migration mode`置于一种特殊状态，在迁移过程完成之前限制用户在通道内进行大多数聊天活动。 `channelCreationMode`在 POST 请求中包含具有值的`migration`实例属性，以显式标识要为迁移创建的新团队。  
<!-- markdownlint-disable MD024 -->
#### <a name="permission"></a>权限

|ScopeName|DisplayName|说明|类型|管理员同意？|涵盖的实体/API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|管理迁移到 Microsoft Teams|创建和管理用于迁移到Microsoft Teams的资源。|**仅限应用程序**|**是**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>请求 (在迁移状态下创建通道) 

```http
POST https://graph.microsoft.com/v1.0/teams/{team-id}/channels

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
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels/$entity",
   "id":"id-value",
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

可在以下方案中收到错误消息：

* 如果 `createdDateTime` 已设置为将来。
* 如果 `createdDateTime` 指定正确，但 `channelCreationMode` 实例属性缺失或设置为无效值。

## <a name="step-3-import-messages"></a>步骤 3：导入消息

创建团队和频道后，可以使用 `createdDateTime`  请求正文中的密 `from` 钥开始发送回程消息。

> [!NOTE]
>
> * 不支持使用 `createdDateTime` 早于消息线程 `createdDateTime` 导入的消息。
> * `createdDateTime` 在同一线程中的消息必须是唯一的。
> * `createdDateTime` 支持具有毫秒精度的时间戳。 例如，如果传入请求消息的 `createdDateTime` 值设置为 *2020-09-16T05：50：31.0025302Z*，则在引入消息时将转换为 *2020-09-16T05：50：31.002Z* 。

#### <a name="request-post-message-that-is-text-only"></a>请求 (仅限文本的 POST 消息) 

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/messages

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
   "@odata.context":"https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels('channel-id')/messages/$entity",
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

#### <a name="error-message"></a>错误消息

```http
400 Bad Request
```

#### <a name="request-post-a-message-with-inline-image"></a>请求 (使用内联图像) 发布消息

> [!NOTE]
>
> * 此方案中没有特殊权限范围，因为请求是其中的一 `chatMessage`部分。
> * 此处适用 `chatMessage` 的范围。

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/messages

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
    "@odata.context": "https://graph.microsoft.com/v1.0/$metadata#teams('team-id')/channels('channel-id')/messages/$entity",
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

## <a name="step-4-complete-migration-mode"></a>步骤 4：完成迁移模式

消息迁移过程完成后，团队和通道都将使用  `completeMigration` 该方法退出迁移模式。 此步骤将打开团队和频道资源供团队成员一般使用。 操作绑定到实 `team` 例。 在团队完成之前，必须在迁移模式下完成所有通道。

#### <a name="request-end-channel-migration-mode"></a>请求 (端通道迁移模式) 

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/channels/channel-id/completeMigration

```

#### <a name="response"></a>响应

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-team-migration-mode"></a>请求 (最终团队迁移模式) 

```http
POST https://graph.microsoft.com/v1.0/teams/team-id/completeMigration
```

#### <a name="response"></a>响应

```http
HTTP/1.1 204 NoContent
```

对某个或`channel`不在`migrationMode`其中的操作调`team`用。

## <a name="step-five-add-team-members"></a>步骤 5：添加团队成员

可以[使用 Teams UI](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) 或 Microsoft Graph添加成员 API 将[成员添加](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true)到团队：

#### <a name="request-add-member"></a>请求 (添加成员) 

```http
POST https://graph.microsoft.com/beta/teams/{team-id}/members
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

## <a name="tips-and-additional-information"></a>使用技巧和其他信息

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* `completeMigration`发出请求后，无法将更多消息导入团队。

* 只有在请求返回成功响应后， `completeMigration` 才能将团队成员添加到新团队。

* 限制：每个通道以 5 RPS 的速度导入消息。

* 如果需要对迁移结果进行更正，则必须删除团队并重复创建团队和频道以及重新迁移消息的步骤。

> [!NOTE]
> 目前，内联映像是导入消息 API 架构支持的唯一媒体类型。

##### <a name="import-content-scope"></a>导入内容范围

下表提供了内容范围：

|作用域内 | 当前超出范围|
|----------|--------------------------|
|团队和频道消息|1：1 和群组聊天消息|
|原始消息的创建时间|专用频道|
|作为消息的一部分的内联图像|提及时|
|指向 SPO 或 OneDrive 中现有文件的链接|反应|
|具有丰富文本的消息|视频|
|消息回复链|公告|
|高吞吐量处理|代码段|
||贴纸|
||表情符号|
||报价单|
||跨频道间的帖子|
||共享频道|

## <a name="see-also"></a>另请参阅

[Microsoft Graph和 Teams 集成](/graph/teams-concept-overview)
