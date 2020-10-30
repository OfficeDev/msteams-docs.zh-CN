---
title: 使用 Microsoft Graph 将外部平台邮件导入到团队
description: 介绍如何使用 Microsoft Graph 将邮件从外部平台导入到团队
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: 团队导入邮件 api 图 microsoft 迁移迁移发布
ms.openlocfilehash: 934e00541773140c90c270a616d6bc50aacac6e1
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796293"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>使用 Microsoft Graph 将第三方平台消息导入 Teams

>[!IMPORTANT]
> Microsoft Graph 和 Microsoft 团队公开预览版适用于早期访问和反馈。 尽管此版本已经历大量测试，但不适合在生产中使用。

使用 Microsoft Graph，可以将用户的现有邮件历史记录和数据从外部系统迁移到团队频道。 通过在团队内启用第三方平台邮件传递层次结构，用户可以采用无缝方式继续进行通信并继续进行而不会中断。

## <a name="import-overview"></a>导入概述

从较高的层次来看，导入过程包含以下内容：

1. [创建具有后时间戳的团队](#step-one-create-a-team)
1. [使用后向时间戳创建通道](#step-two-create-a-channel)  
1. [导入外部定期邮件](#step-three-import-messages)
1. [完成团队和渠道迁移过程](#step-four-complete-migration-mode)
1. [添加团队成员](#step-five-add-team-members)

## <a name="necessary-requirements"></a>必需的要求

### <a name="analyze-and-prepare-message-data"></a>分析和准备邮件数据

✔查看第三方数据以确定将迁移的内容。  
✔从第三方聊天系统中提取所选数据。  
✔将第三方聊天结构映射到团队结构。  
✔将导入数据转换为迁移所需的格式。  

### <a name="set-up-your-office-365-tenant"></a>设置 Office 365 租户

✔确保导入数据存在 Office 365 租户。 有关为团队设置 Office 365 租赁的详细信息， *请参阅*[准备 office 365 租户](../../concepts/build-and-test/prepare-your-o365-tenant.md)。  
✔确保团队成员在 Azure Active Directory (AAD) 中。  有关详细信息， *请参阅* 向 Azure Active Directory [添加新用户](/azure/active-directory/fundamentals/add-users-azure-active-directory) 。

## <a name="step-one-create-a-team"></a>第一步：创建团队

由于现有数据正在迁移，因此在迁移过程中维护原始邮件的时间戳并防止邮件活动是重新创建用户的现有邮件流的关键。 这是通过以下方式实现的：

> 使用 "团队" 资源属性创建具有 "后向时间戳" 的[新团队](/graph/api/team-post?view=graph-rest-beta&tabs=http&preserve-view=true) `createdDateTime` 。 将新团队放在中 `migration mode` ，这是一种特殊状态，可从团队中的大多数活动中对用户进行横栏，直到迁移过程完成。 将 `teamCreationMode` 实例属性包含 `migration` 在 POST 请求中的值，以显式标识新团队为迁移而创建。  

> **注意** ： `createdDateTime` 将仅为已迁移的团队或频道的实例填充字段。

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>权限

|ScopeName|DisplayName|说明|类型|管理员同意？|涵盖的实体/Api|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|管理迁移到 Microsoft Teams|创建、管理用于迁移到 Microsoft 团队的资源|**仅限应用程序**|**是**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>请求 (在迁移状态中创建团队) 

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

* `createdDateTime`  设置为 "将来"。
* `createdDateTime`  正确指定，但 `teamCreationMode`  缺少实例属性或将实例属性设置为无效值。

## <a name="step-two-create-a-channel"></a>步骤2：创建通道

为导入的邮件创建通道与创建团队方案类似：

> 使用 "信道" 资源属性创建具有 "后向时间戳" 的[新通道](/graph/api/channel-post?view=graph-rest-beta&tabs=http&preserve-view=true) `createdDateTime` 。 将新频道放置在中 `migration mode` ，这是一种特殊状态，可用于在迁移过程完成前，从频道内的大多数聊天活动中对用户进行横栏。  将 `channelCreationMode` 实例属性包含 `migration` 在 POST 请求中的值，以显式标识新团队为迁移而创建。  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>权限

|ScopeName|DisplayName|说明|类型|管理员同意？|涵盖的实体/Api|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|管理迁移到 Microsoft Teams|创建、管理用于迁移到 Microsoft 团队的资源|**仅限应用程序**|**是**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>请求 (在迁移状态中创建频道) 

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

* `createdDateTime`  设置为 "将来"。
* `createdDateTime`  正确指定 `channelCreationMode`  ，但缺少实例属性或将实例属性设置为无效值。

## <a name="step-three-import-messages"></a>第三步：导入邮件

在创建团队和频道之后，您可以开始使用 `createdDateTime`  请求正文中的和键发送回送邮件 `from`  。 **注意** ： `createdDateTime` 不支持在邮件线程之前导入的邮件 `createdDateTime` 。

> [!NOTE]
> createdDateTime 在同一线程中的所有邮件中必须是唯一的。

#### <a name="request-post-message-that-is-text-only"></a>请求 (张贴为纯文本的邮件) 

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

#### <a name="request-post-a-message-with-inline-image"></a>请求 (将包含内联图像的邮件发布) 

> **注意** ：此方案中没有特殊的权限范围，因为该请求是了 chatmessage 的一部分;了 chatmessage 的作用域也适用于此处。

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

## <a name="step-four-complete-migration-mode"></a>步骤4：完成迁移模式

邮件迁移过程完成后，团队和通道将使用方法从迁移模式中去掉  `completeMigration`  。 此步骤将打开团队和渠道资源，以供工作组成员进行常规使用。 操作将绑定到 `team` 实例。

#### <a name="request-end-team-migration-mode"></a>请求 (结束团队迁移模式) 

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a>响应

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a>请求 (结束通道迁移模式) 

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

* 在或上调用的操作 `team` `channel` 不在中 `migrationMode` 。

## <a name="step-five-add-team-members"></a>第5步：添加团队成员

您可以 [使用 "团队 UI"](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) 或 Microsoft Graph [添加成员](/graph/api/group-post-members?view=graph-rest-beta&tabs=http&preserve-view=true) API 将成员添加到团队中：

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

* 您可以导入不在工作组中的用户的邮件。 **注意** ：在公共预览过程中，不会在团队客户端或合规性门户中搜索为用户导入的邮件。

* `completeMigration`发出请求后，将无法再向团队中导入邮件。

* 只有在请求返回成功的响应后，才能将团队成员添加到新团队 `completeMigration` 。

* 限制：邮件将导入每通道5个 RPS。

* 如果需要对迁移结果进行更正，则需要删除团队并重复步骤以创建团队和频道并重新迁移邮件。

> [!NOTE]
> 目前，嵌入式图像是导入邮件 API 架构支持的唯一媒体类型。

##### <a name="import-content-scope"></a>导入内容范围

|范围内 | 当前超出范围|
|----------|--------------------------|
|团队和频道消息|1:1 和分组聊天消息|
|原始邮件的创建时间|专用频道|
|作为邮件的一部分的嵌入式图像|提到|
|指向 SPO/OneDrive 中的现有文件的链接|作出|
|带格式文本的邮件|视频|
|邮件答复链|公告|
|高吞吐量处理|代码段|
||自适应卡片|
||不干胶|
||表情符号|
||股票|
||通道之间的跨文章|

> [!div class="nextstepaction"]
>[了解有关 Microsoft Graph 和团队集成的详细信息](/graph/teams-concept-overview)
