---
title: 为匿名用户生成应用
author: v-sdhakshina
description: 了解如何为匿名用户生成应用，并在具有所有管理员设置的会议应用中测试传递给匿名用户的体验。
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: ff897c5135740557e12898e7e5d231557b2e2823
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615419"
---
# <a name="build-apps-for-anonymous-users"></a>为匿名用户生成应用

可以在应用中生成机器人、消息传递扩展、卡片和任务模块，以与匿名会议参与者互动。

若要测试匿名用户的应用体验，请在会议邀请中选择 URL，然后从专用浏览器窗口加入会议。

## <a name="admin-setting-for-anonymous-user-app-interaction"></a>匿名用户应用交互的管理员设置

Teams 管理员可以使用管理门户为整个租户启用或禁用匿名用户应用交互。 默认启用此设置。 有关详细信息，请参阅 [允许匿名用户在会议中与应用交互](/microsoftteams/meeting-settings-in-teams)。

## <a name="in-meeting-getcontext-from-teams-client-sdk"></a>In-Meeting从 Teams 客户端 SDK 获取Context

应用从共享应用阶段调用 `getContext` API 时，会收到匿名用户的以下信息。 可以通过检查`userLicenseType`未知值来识别匿名 **用户。**

```csharp
"userObjectId": "8:anon:<GUID1>",
"userLicenseType": "Unknown",
"loginHint": "8:teamsvisitor:<ID>",
"userPrincipalName": "8:teamsvisitor:<ID>",
"tid": "<meeting organizer tenant ID>"
```

| **属性名称** | **说明** |
| --- | --- |
| `userObjectId` | 匿名用户的唯一生成值。 此值不能用于对图形 API 的调用。 |
| `userLicenseType` | `Unknown`，表示匿名用户。 |
| `loginHint` | 唯一生成的值。 此值不能用作登录流中的提示。 |
| `userPrincipalName` | 唯一生成的值。 此值不能用于对图形 API 的调用。 |
| `tid` | 会议组织者的租户 ID。 |

> [!NOTE]
> 当匿名用户加入会议时，将生成新的用户 ID。 每当匿名用户重新加入会议时，都会生成不同的用户 ID。

## <a name="bot-activities-and-apis"></a>机器人活动和 API

由于存在一些差异，发送到机器人的活动及其从机器人 API 接收的响应在匿名和非匿名会议参与者之间是一致的。 通常：

* 用户 ID 是一个生成的值，每次匿名用户加入会议时，该值都不同。
* 省略该 `aadObjectId` 属性。
* 属性 `userRole` 设置为 **匿名**。
* 提供的租户 ID 设置为会议组织者的租户 ID。

### <a name="get-members-and-get-single-member-apis"></a>获取成员并获取单个成员 API

[获取成员](/microsoftteams/platform/bots/how-to/get-teams-context#fetch-the-roster-or-user-profile)并[获取单个成员](/microsoftteams/platform/bots/how-to/get-teams-context#get-single-member-details) API 返回匿名用户的有限信息：

```json
{ 
  "id": "<GUID1>", 
  "name": "<AnonTest (Guest)>",  
  "tenantId": "<GUID2>", 
  "userRole": "anonymous" 
} 
```

| **属性名称** | **说明** |
| --- | --- |
| `id` | 匿名用户的唯一生成值。 |
| `name` | 加入会议时匿名用户提供的名称。 |
| `tenantId` | 会议组织者的租户 ID。 |
| `userRole` | `anonymous`，表示匿名用户。 |

> [!NOTE]
> 从机器人 API 和 Teams 客户端 SDK API 接收的 ID 不同。

### <a name="conversationupdate-activity-membersadded-and-membersremoved"></a>ConversationUpdate 活动 MembersAdded 和 MembersRemoved

```csharp
{ 
  "membersAdded": [ 
    { 
      "id": "<GUID1>" 
    } 
  ], 
  "type": "conversationUpdate", 
  "timestamp": "<timestamp>", 
  "id": "<event unique identifier>", 
  "channelId": "msteams", 
  "serviceUrl": "<serviceURL>", 
  "from": { 
    "id": "<GUID2>" 
  }, 
  "conversation": { 
    "isGroup": true, 
    "tenantId": "<tenant id>", 
    "id": "<conversation id>" 
  }, 
  "recipient": { 
    "id": "<bot id>", 
    "name": "<bot name>" 
  }, 
  "channelData": { 
    "tenant": { 
      "id": "<tenant id>" 
    }, 
    "source": null, 
    "meeting": { 
      "id": "<meeting id>" 
    } 
  } 
} 
```

| **属性名称** | **说明** |
| --- | --- |
| `membersAdded.id` | 匿名用户 ID。 |
| `from.id` | 会议组织者 ID。 |
| `conversation.tenantId` | 会议组织者的租户 ID。 |
| `conversation.id` | 会议聊天的对话 ID。 |
| `tenant.id` | 会议组织者的租户 ID。 |

类似的更改适用于 `membersRemoved` 活动有效负载。

> [!NOTE]
>
> 当匿名用户加入或离开会议时， `from` 有效负载中的对象始终具有会议组织者的 ID，即使该操作是由其他人执行的。

### <a name="create-conversation-api"></a>创建对话 API

不允许机器人与匿名用户启动一对一对话。 如果机器人使用匿名用户的用户 ID 调用 Create Conversation API，它将收到 `400` 错误的请求状态代码和以下错误响应：

```csharp
{ 
  "error": {
    "code": "BadArgument",
    "message": "Bot cannot create a conversation with an anonymous user"
  }
} 
```

### <a name="adaptive-cards"></a>自适应卡片

匿名用户可以在会议聊天中查看自适应卡片并与之交互。 自适应卡片操作对匿名用户和非匿名用户的行为方式相同。 有关详细信息，请参阅 [卡片操作](/microsoftteams/platform/task-modules-and-cards/cards/cards-actions?tabs=json)。

## <a name="known-issues-and-limitations"></a>已知问题和限制

* 侧面板选项卡和内容气泡不适用于匿名用户。 匿名用户仍可以看到共享到会议阶段的应用内容。

* 对于匿名用户，机器人收到 `getContext` 的用户 ID 和用户 ID 是不同的。 无法直接关联两者。 如果需要在选项卡和机器人之间跟踪用户的标识，则必须提示用户使用外部标识提供者进行身份验证。

* 匿名用户将在机器人消息和卡片上看到通用应用图标，而不是应用的实际图标。 例如：

    :::image type="content" source="../assets/images/apps-in-meetings/app-icon.png" alt-text="此屏幕截图显示匿名用户的应用图标显示方式。":::

## <a name="see-also"></a>另请参阅

* [为 Teams 会议阶段生成应用](build-apps-for-teams-meeting-stage.md)
* [会议应用 API](meeting-apps-apis.md)
* [Microsoft Teams 机器人的工作原理](/azure/bot-service/bot-builder-basics-teams)
