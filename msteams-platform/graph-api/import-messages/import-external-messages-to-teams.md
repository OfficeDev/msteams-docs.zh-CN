---
title: 使用 Microsoft Graph 将外部平台消息导入到 Teams
description: 介绍如何使用 Microsoft Graph 将消息从外部平台导入到 Teams
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams Slack 导入邮件 API 图形 Microsoft 迁移迁移后内容
ms.openlocfilehash: 8e8b21c9a38570d7ede745e27b9316b7aba29956
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "46820364"
---
# <a name="import-third-party-platform-messages-to-teams-using-microsoft-graph"></a>使用 Microsoft Graph 将第三方平台消息导入到 Teams

>[!IMPORTANT]
> Microsoft Graph 和 Microsoft Teams 公共预览版可提供快速访问权限和反馈。 虽然此版本已经进行了扩展测试，但它不适合用于生产。

使用 Microsoft Graph，可以将用户的现有消息历史记录和数据从外部系统迁移到 Teams 频道。 通过在 Teams 中重新创建第三方平台消息传递层次结构，用户可以无缝地继续通信，并在不中断的情况下继续通信。

## <a name="import-overview"></a>导入概述

从较高的层次上来说，导入过程包括：

1. [创建具有后期时间戳的团队](#step-one-create-a-team)
1. [创建具有后期时间戳的通道](#step-two-create-a-channel)  
1. [导入外部后期时间过期的消息](#step-three-import-messages)
1. [完成团队和渠道迁移过程](#step-four-complete-migration-mode)
1. [添加团队成员](#step-five-add-team-members)

## <a name="necessary-requirements"></a>必需要求

### <a name="analyze-and-prepare-message-data"></a>分析和准备消息数据

✔检查第三方数据以决定要迁移的内容。  
✔从第三方聊天系统提取所选数据。  
✔将导入数据转换为迁移所需的格式。  
✔ 将第三方聊天结构映射到 Teams 结构。

### <a name="set-up-your-office-365-tenant"></a>设置 Office 365 租户

✔确保存在 Office 365 租户以获取导入数据。 有关设置 Teams 的 Office 365 租用的详细信息，请参阅 *： 准备* [Office 365 租户](../../concepts/build-and-test/prepare-your-o365-tenant.md)。  
✔确保团队成员在 Azure Active Directory (AAD) 。  有关详细信息，*请参阅"*[将新用户添加到](/azure/active-directory/fundamentals/add-users-azure-active-directory)Azure Active Directory"。

## <a name="step-one-create-a-team"></a>第 1 步：创建团队

由于正在迁移现有数据，请维护原始邮件时间戳并防止迁移过程中的邮件活动对重新创建 Teams 中用户现有的邮件流至至至多重要。 此操作实现如下：

1. [使用团队资源](/graph/api/team-post?view=graph-rest-beta&tabs=http) 属性创建具有后期时间戳的新  `createdDateTime`  团队。  

1. 将新团队置 `migration mode` 于一个特殊状态，可使用户从团队内的大多数活动中进行，直到迁移过程完成。 在 `teamCreationMode` POST 请求中包括 `migration` 实例属性以及值，明确标识新团队创建用于迁移的内容。  

<!-- markdownlint-disable MD001 -->

#### <a name="permissions"></a>权限

|ScopeName|DisplayName|说明|类型|管理员同意？|涵盖的实体/API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|管理迁移到 Microsoft Teams|创建、管理要迁移到 Microsoft Teams 的资源|**仅限应用程序**|**是**|`POST /teams`|

#### <a name="request-create-a-team-in-migration-state"></a>请求 (在迁移状态下创建) 

```http
POST https://graph.microsoft.com/beta/teams

Content-Type: application/json
{
  "@microsoft.graph.teamCreationMode": "migration",
  "template@odata.bind": "https://graph.microsoft.com/beta/teamsTemplates('standard')",
  "displayName": "My Sample Team",
  "description": "My Sample Team’s Description"
  "createdDateTime": "2020-03-14T11:22:17.067Z"
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

* `createdDateTime`  将来设置。
* `createdDateTime`  正确指定， `teamCreationMode`  但实例属性缺少或设置为无效值。

## <a name="step-two-create-a-channel"></a>第 2 步：创建频道

为导入的消息创建频道与创建团队方案类似： 

1. [使用通道资源](/graph/api/channel-post?view=graph-rest-beta&tabs=http) 属性，使用后期时间戳创建新 `createdDateTime` 频道。

1. 将新频道置于 `migration mode` ，从频道内的大多数聊天活动中栏用户，直到完成迁移过程之前，其状态是一种特殊状态。  在 `channelCreationMode` POST 请求中包括 `migration` 实例属性以及值，明确标识新团队创建用于迁移的内容。  
<!-- markdownlint-disable MD024 -->
#### <a name="permissions"></a>权限

|ScopeName|DisplayName|说明|类型|管理员同意？|涵盖的实体/API|
|-|-|-|-|-|-|
|`Teamwork.Migrate.All`|管理迁移到 Microsoft Teams|创建、管理要迁移到 Microsoft Teams 的资源|**仅限应用程序**|**是**|`POST /teams`|

#### <a name="request-create-a-channel-in-migration-state"></a>请求 (在迁移状态下创建) 

```http
POST https://graph.microsoft.com/beta/teams/{id}/channels

Content-Type: application/json
{
  "@microsoft.graph.channelCreationMode": "migration",
  "displayName": "Architecture Discussion",
  "description": "This channel is where we debate all future architecture plans",
  "membershipType": "standard",
  "createdDateTime": "2020-03-14T11:22:17.067Z"
}
```

#### <a name="response"></a>响应

```http
HTTP/1.1 202 Accepted
Location: /teams/{teamId}/channels/{channelId}/operations/{operationId}
Content-Location: /teams/{teamId}/channels/{channelId}
```

#### <a name="error-message"></a>错误消息

```http
400 Bad Request
```

* `createdDateTime`  将来设置。
* `createdDateTime`  正确指定 `channelCreationMode`  ，但实例属性缺少或设置为无效值。

## <a name="step-three-import-messages"></a>步骤 3：导入邮件

创建团队和频道后，你可以开始使用请求正文中的密钥 `createdDateTime` `from`  发送返回时消息。

#### <a name="request-post-message-that-is-text-only"></a>请求 (文本的 POST 消息) 

```http
POST https://graph.microsoft.com/beta/teams/teamId/channels/channelId/messages

{
    "replyToId": null,
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
        "content": "Hello World"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
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
        "content": "Hello World"
    },
    "attachments": [],
    "mentions": [],
    "reactions": []
}
```

#### <a name="request-post-a-message-with-inline-image"></a>请求 (嵌入式图像) 消息

> **注意**：此方案中没有特殊的权限范围，因为请求是 chatMessage 的一部分;chatMessage 的范围也在此适用。

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
    {
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

消息迁移过程完成后，团队和渠道都使用该方法退出迁移  `completeMigration`  模式。 此步骤将打开团队和频道资源，以供团队成员使用。 操作绑定到 `team` 该实例。

#### <a name="request-end-team-migration-mode"></a>请求 (团队迁移模式) 

```http
POST https://graph.microsoft.com/beta/teams/teamId/completeMigration

```

#### <a name="response"></a>响应

```http
HTTP/1.1 204 NoContent
```

#### <a name="request-end-channel-migration-mode"></a>请求结束 (频道迁移模式) 

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

* 对中或 `team` 不在 `channel` 中的操作 `migrationMode` 调用。

## <a name="step-five-add-team-members"></a>步骤 5：添加团队成员

你可以使用 Teams UI 或 Microsoft Graph [添加成员 API](https://support.microsoft.com/office/add-members-to-a-team-in-teams-aff2249d-b456-4bc3-81e7-52327b6b38e9) 向 [团队添加](/graph/api/group-post-members?view=graph-rest-beta&tabs=http) 成员：

#### <a name="request-add-member"></a>添加 (请求) 

```http
POST https://graph.microsoft.com/beta/groups/{id}/members/$ref
Content-type: application/json
Content-length: 30

{
  "@odata.id": "https://graph.microsoft.com/beta/directoryObjects/{id}"
}
```

#### <a name="response"></a>响应

```http
HTTP/1.1 204 No Content
```

## <a name="tips-and-additional-information"></a>提示和其他信息

<!-- markdownlint-disable MD001 -->
<!-- markdownlint-disable MD026 -->

* 可导入来自 Teams 外部用户的消息。

* 发出请求 `completeMigration` 后，无法将进一步的邮件导入到团队。

* 工作组成员只能在请求返回成功 `completeMigration` 的响应后添加到新团队。

* 限制：每渠道 5 个 RPS 导入邮件。

* 如需更正迁移结果，需要删除团队并重复创建团队和频道并重新迁移消息的步骤。

> [!NOTE]
> 目前，嵌入式图像是导入消息 API 架构唯一支持的媒体类型。

##### <a name="import-content-scope"></a>导入内容范围

|范围内 | 目前超出范围|
|----------|--------------------------|
|团队消息和频道消息|1：1 和群组聊天消息|
|创建原始邮件的时间|专用频道|
|作为邮件的一部分的嵌入式图像|提及|
|指向 SPO/OneDrive 中的现有文件的链接|反应|
|包含 RTF 的邮件|视频|
|邮件答复链|公告|
|高吞吐量处理|代码段|
||自适应卡片|
||Stickers|
||情注|
||引号|
||在通道之间交叉帖子|

> [!div class="nextstepaction"]
>[了解有关 Microsoft Graph 和 Teams 集成的详细信息](/graph/teams-concept-overview)
