---
title: 会议应用 API 参考
author: surbhigupta
description: 通过示例和代码示例识别会议应用程序 API 参考
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: Teams 应用会议用户参与者角色 API 用户上下文通知信号查询
ms.openlocfilehash: 75dc6dde65b24fd05931021544fafe3af956d88d
ms.sourcegitcommit: c197fe4c721822b6195dfc5c7d8e9ccd47f142fe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2022
ms.locfileid: "65667981"
---
# <a name="meeting-apps-api-references"></a>会议应用 API 参考

会议扩展性提供 API 来增强会议体验。 可以在列出的 API 的帮助下执行以下操作：

* 在会议生命周期内生成应用或集成现有应用。
* 使用 API 使应用了解会议。
* 选择所需的 API 来改进会议体验。

> [!NOTE]
> 使用 Teams [JavaScript SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)（*版本*：1.10 及更高版本）使 SSO 在会议侧面板中得以使用。

下表提供了 Microsoft Teams 客户端 (MSTC) 和 Microsoft Bot Framework (MSBF) SDK 中可用的 API 列表：

|方法| 说明| 源|
|---|---|----|
|[**获取用户上下文**](#get-user-context-api)| 获取上下文信息，以便在 Teams 选项卡中显示相关内容。| MSTC SDK|
|[**获取参与者**](#get-participant-api)| 通过会议 ID 和参与者 ID 提取参与者信息。 |MSBF SDK|
|[**发送会议内通知**](#send-an-in-meeting-notification)| 使用用户机器人聊天的现有对话通知 API 提供会议信号，并允许通知显示会议内通知的用户操作。 |MSBF SDK|
|[**获取会议详细信息**](#get-meeting-details-api)| 获取会议的静态元数据。 |MSBF SDK |
|[**发送实时字幕**](#send-real-time-captions-api)| 将实时字幕发送到正在进行的会议。 |MSTC SDK|
|[**将应用内容共享到演示区域**](#share-app-content-to-stage-api)| 从会议中的应用侧面板将应用的特定部分共享到会议演示区域。 |MSTC SDK|
|[**获取应用内容演示区域共享状态**](#get-app-content-stage-sharing-state-api)| 获取会议演示区域应用共享状态的信息。 |MSTC SDK|
|[**获取应用内容演示区域共享功能**](#get-app-content-stage-sharing-capabilities-api)| 获取应用共享到会议演示区域的功能。 |MSTC SDK|
|[**获取实时 Teams 会议事件**](#get-real-time-teams-meeting-events-api)|获取实时会议事件，例如实际开始时间和结束时间。| MSBF SDK|

## <a name="get-user-context-api"></a>获取用户上下文 API

若要标识和检索选项卡内容的上下文信息，请参阅[获取 Teams 选项卡上下文](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library)。`meetingId` 由在会议上下文中运行的选项卡使用，并添加到响应有效负载中。

## <a name="get-participant-api"></a>获取参与者 API

`GetParticipant` API 必须有机器人注册和 ID 才能生成身份验证令牌。 有关详细信息，请参阅[机器人注册和 ID](../build-your-first-app/build-bot.md)。

> [!NOTE]
>
> * 请勿缓存参与者角色，因为会议组织者可以随时更改角色。
> * 目前，只有少于 350 名参与者的通讯组列表或名单才支持 `GetParticipant` API。

### <a name="query-parameters"></a>查询参数

> [!TIP]
> 从 [选项卡 SSO 身份验证](../tabs/how-to/authentication/auth-aad-sso.md)中获取参与者 ID 和租户 ID。

`Meeting` API 必须将`meetingId`、`participantId` 和 `tenantId` 作为 URL 参数。 这些参数作为 Teams 客户端 SDK 和机器人活动的一部分提供。

下表列出了查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**meetingId**| 字符串 | 是 | 会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。|
|**participantId**| 字符串 | 是 | 参与者 ID 就是用户 ID。 它在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中可用。 建议从 Tab SSO 获取参与者 ID。 |
|**tenantId**| 字符串 | 是 | 租户用户需要租户 ID。 它在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中可用。 建议从 Tab SSO 获取租户 ID。 |

### <a name="example"></a>示例

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = await TeamsInfo.GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourParticipantTenantId").ConfigureAwait(false);
  TeamsChannelAccount member = participant.User;
  MeetingParticipantInfo meetingInfo = participant.Meeting;
  ConversationAccount conversation = participant.Conversation;

  await turnContext.SendActivityAsync(MessageFactory.Text($"The participant role is: {meetingInfo.Role}"), cancellationToken);
}
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```typescript
export class MyBot extends TeamsActivityHandler {
    constructor() {
        super();
        this.onMessage(async (context, next) => {
            TeamsMeetingParticipant participant = getMeetingParticipant(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
            let member = participant.user;
            let meetingInfo = participant.meeting;
            let conversation = participant.conversation;
            
            await context.sendActivity(`The participant role is: '${meetingInfo.role}'`);
            await next();
        });
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

```json
{
   "user":{
      "id":"29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId":"e236c4bf-88b1-4f3a-b1d7-8891dfc332b5",
      "name":"Bob Young",
      "givenName":"Bob",
      "surname":"Young",
      "email":"Bob.young@microsoft.com",
      "userPrincipalName":"Bob.young@microsoft.com",
      "tenantId":"2fe477ab-0efc-4dfd-bde2-484374e2c373",
      "userRole":"user"
   },
   "meeting":{
      "role ":"Presenter",
      "inMeeting":true
   },
   "conversation":{
      "id":"<conversation id>",
      "isGroup":true
   }
}
```

---

### <a name="response-codes"></a>响应代码

下表列出了响应代码：

|响应代码|说明|
|---|---|
| **403** | 获取参与者信息未与应用共享。 如果未在会议中安装应用，则会触发错误响应 403。 如果租户管理员在实时站点迁移期间禁用或阻止应用，则会触发错误响应 403。 |
| **200** | 成功检索参与者信息。|
| **401** | 应用使用无效的令牌进行响应。|
| **404** | 会议已过期或参与者不可用。|

## <a name="send-an-in-meeting-notification"></a>发送会议内通知

会议中的所有用户都会收到通过会议内通知有效负载发送的通知。 会议内通知有效负载会触发会议内通知，并能够帮助提供使用用户机器人聊天的现有聊天通知 API 传递的会议信号。 可以根据用户操作发送会议内通知。 可通过机器人服务获取有效负载。

> [!NOTE]
>
> * 调用会议内通知时，内容将显示为聊天消息。
> * 目前，不支持发送目标通知和对 Web 应用的支持。
> * 在用户在 Web 视图中执行操作后，必须调用 [submitTask()](../task-modules-and-cards/task-modules/task-modules-bots.md#submit-the-result-of-a-task-module) 函数才能自动关闭。 这是应用提交的要求。 有关详细信息，请参阅 [Teams SDK 任务模块](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。
> * 如果希望应用支持匿名用户，初始调用请求有效负载必须依赖于 `from` 对象中的 `from.id` 请求元数据，而不是 `from.aadObjectId` 请求元数据。 `from.id` 是用户 ID，`from.aadObjectId` 是用户的 Microsoft Azure Active Directory (Azure AD) ID。 有关详细信息，请参阅[在选项卡中使用任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md)和[创建和发送任务模块](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。

### <a name="query-parameter"></a>查询参数

下表列出了查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**conversationId**| 字符串 | 是 | 聊天标识符作为 Bot Invoke 的一部分提供。 |

### <a name="examples"></a>示例

`Bot ID` 在清单中声明，机器人会接收结果对象。

> [!NOTE]
>
> * 在请求的有效负载示例中，`externalResourceUrl` 的 `completionBotId` 参数是可选的。
> * `externalResourceUrl` 宽度和高度参数必须以像素为单位。 有关详细信息，请参阅[设计指南](design/designing-apps-in-meetings.md)。
> * URL 是页面，在会议内通知中加载为 `<iframe>`。 域必须位于应用清单中的应用 `validDomains` 数组中。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
activity.TeamsNotifyUser(true, "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID");
await turnContext.SendActivityAsync(activity).ConfigureAwait(false);
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

```javascript
const replyActivity = MessageFactory.text('Hi'); // this could be an adaptive card instead
replyActivity.channelData = {
    notification: {
        alertInMeeting: true,
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID’
    }
};
await context.sendActivity(replyActivity);
```

# <a name="json"></a>[JSON](#tab/json)

```http
POST /v3/conversations/{conversationId}/activities
```

```json

{
    "type": "message",
    "text": "John Phillips assigned you a weekly todo",
    "summary": "Don't forget to meet with Marketing next week",
    "channelData": {
        "notification": {
            "alertInMeeting": true,
            "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
        }
    },
    "replyToId": "1493070356924"
}
```

---

### <a name="response-codes"></a>响应代码

下表列出了响应代码：

|响应代码|说明|
|---|---|
| **201** | 已成功发送活动信号。 |
| **401** | 应用使用无效的令牌进行响应。 |
| **403** | 应用无法发送信号。 403 响应代码可能出现有很多原因，例如租户管理员在实时站点迁移期间禁用和阻止应用。 在这种情况下，有效负载包含详细的错误消息。 |
| **404** | 会议聊天不存在。 |

## <a name="get-meeting-details-api"></a>获取会议详细信息 API

会议详细信息 API 使应用能够获取会议的静态元数据。 元数据提供不会动态变化的数据点。 API 可通过机器人服务使用。 目前，私人计划会议或定期会议以及安排的频道会议或定期会议分别支持具有不同 RSC 权限的 API。

`Meeting Details` API 必须具有机器人注册和机器人 ID。 它要求 Bot SDK 获取 `TurnContext`。 若要使用会议详细信息 API，必须根据任何会议的范围（例如私人会议或频道会议）获取不同的 RSC 权限。

### <a name="prerequisite"></a>先决条件

若要使用会议详细信息 API，必须根据任何会议的范围（例如私人会议或频道会议）获取不同的 RSC 权限。

<br>

<details>

<summary><b>针对应用清单版本 1.12</b></summary>

使用以下示例为任何私人会议配置应用清单的 `webApplicationInfo` 和 `authorization` 属性：

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
},
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            }
        ]
    }
}
 ```

使用以下示例为任何频道会议配置应用清单的 `webApplicationInfo` 和 `authorization` 属性：

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
},
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "ChannelMeeting.ReadBasic.Group",
                "type": "Application"
            }
        ]
    }
}
 ```

<br>

</details>

<br>

<details>

<summary><b>针对应用清单版本 1.11 或更低版本</b></summary>

使用以下示例为任何私人会议配置应用清单的 `webApplicationInfo` 属性：

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

使用以下示例为任何频道会议配置应用清单的 `webApplicationInfo` 属性：

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "ChannelMeeting.ReadBasic.Group"
    ]
}
 ```

<br>

</details>

> [!NOTE]
> 机器人可以通过将 `ChannelMeeting.ReadBasic.Group` 添加到清单以获得 RSC 权限，自动从所有频道中创建的所有会议接收会议开始或结束事件。

### <a name="query-parameter"></a>查询参数

下表列出了查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**meetingId**| 字符串 | 是 | 会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。 |

### <a name="example"></a>示例

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
MeetingInfo result = await TeamsInfo.GetMeetingInfoAsync(turnContext);
await turnContext.SendActivityAsync(JsonConvert.SerializeObject(result));
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

不可用

# <a name="json"></a>[JSON](#tab/json)

```http
GET /v1/meetings/{meetingId}
```

会议详细信息 API 的 JSON 响应正文如下所示：

```json
{ 
   "details": { 
        "id": "meeting ID", 
        "msGraphResourceId": "", 
        "scheduledStartTime": "2020-08-21T02:30:00+00:00", 
        "scheduledEndTime": "2020-08-21T03:00:00+00:00", 
        "joinUrl": "https://teams.microsoft.com/l/xx", 
        "title": "All Hands", 
        "type": "Scheduled" 
    }, 
    "conversation": { 
            "isGroup": true, 
            "conversationType": "groupchat", 
            "id": "meeting chat ID" 
    }, 
    "organizer": { 
        "id": "<organizer user ID>", 
        "aadObjectId": "<AAD ID>", 
        "tenantId": "<Tenant ID>" 
    }
} 
```

---

## <a name="send-real-time-captions-api"></a>发送实时字幕 API

发送实时字幕 API 可以公开 POST 终结点，让 Microsoft Teams 通信访问实时翻译 (CART) 字幕（人工键入的隐藏字幕）。 当最终用户启用了字幕时，发送到此终结点的文本内容将显示在 Microsoft Teams 会议中。

### <a name="cart-url"></a>CART URL

你可以从 Microsoft Teams 会议的 **会议选项** 页面获取 POST 终结点的 CART URL。 有关详细信息，请参阅 [Microsoft Teams 会议中的 CART 字幕](https://support.microsoft.com/office/use-cart-captions-in-a-microsoft-teams-meeting-human-generated-captions-2dd889e8-32a8-4582-98b8-6c96cf14eb47)。 无需修改 CART URL 即可使用 CART 字幕。

#### <a name="query-parameter"></a>查询参数

CART URL 包括以下查询参数：

|值|类型|必需|说明|
|---|---|----|----|
|**meetingId**| 字符串 | 是 |会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。 <br/>例如：meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d|
|**令牌**| 字符串 | 是 |授权令牌。<br/> 例如：token=04751eac |

#### <a name="example"></a>示例

```http
https://api.captions.office.microsoft.com/cartcaption?meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d&token=gjs44ra
```

### <a name="method"></a>方法

|Resource|方法|说明|
|----|----|----|
|/cartcaption|POST|处理会议的字幕（已启动）|

> [!NOTE]
> 确保所有请求的内容类型都是采用 UTF-8 编码的纯文本。 请求正文仅包含字幕。

#### <a name="example"></a>示例

```http
POST /cartcaption?meetingid=04751eac-30e6-47d9-9c3f-0b4ebe8e30d9&token=04751eac&lang=en-us HTTP/1.1
Host: api.captions.office.microsoft.com
Content-Type: text/plain
Content-Length: 22
Hello I’m Cortana, welcome to my meeting. 
```

> [!Note]  
> 每个 POST 请求都会生成新的字幕行。 若要确保最终用户有足够的时间读取内容，请将每个 POST 请求正文限制为 80-120 个字符。

### <a name="error-codes"></a>错误代码

下表列出了错误代码：

|错误代码|说明|
|---|---|
| **400** | 错误请求。 响应正文包含过多信息。 例如，无法显示所有必需的参数。|
| **401** | 未经授权。 令牌错误或过期。 如果收到此错误，请在 Teams 中生成新的 CART URL。 |
| **404** | 找不到会议或未开始会议。 如果收到此错误，请确保启动会议并选择开始字幕。 在会议中启用字幕后，可以开始让会议显示字幕。|
| **500** |内部服务器错误。 有关详细信息，[请联系支持人员或提供反馈](../feedback.md)。|

## <a name="share-app-content-to-stage-api"></a>将应用内容共享到演示区域

`shareAppContentToStage` API 能够帮助将应用的特定部分共享到会议演示区域。 可通过 Teams 客户端 SDK 获取 API。

### <a name="prerequisite"></a>先决条件

*  若要使用 `shareAppContentToStage` API，必须获取 RSC 权限。 在应用清单中，配置 `authorization` 属性，以及 `resourceSpecific` 字段中的 `name` 和 `type`。 例如：

    ```json
    "authorization": {
        "permissions": { 
        "resourceSpecific": [
        { 
        "name": "MeetingStage.Write.Chat",
        "type": "Delegated"
        }
        ]
    }
    }
    ```
*  manifest.json 中的 `validDomains` 数组必须允许 `appContentUrl`，否则 API 将返回 501。

### <a name="query-parameter"></a>查询参数

下表列出了查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**callback**| 字符串 | 是 | 回调包含 error 和 result 两个参数。 *error* 包含 *SdkError* 类型的错误，或在共享成功时返回 null。 如果共享成功，*result* 包含 true 值，或者在共享失败返回 null。|
|**appContentURL**| 字符串 | 是 | 将共享到演示区域上的 URL。|

### <a name="example"></a>示例

```javascript
const appContentUrl = "https://www.bing.com/";

microsoftTeams.meeting.shareAppContentToStage((err, result) => {
    if (result) {
        // handle success
    }
    if (err) {
        // handle error
    }
}, appContentUrl);
```

### <a name="response-codes"></a>响应代码

下表列出了响应代码：

|响应代码|说明|
|---|---|
| **500** | 内部错误。 |
| **501** | 当前上下文不支持 API。|
| **1000** | 应用没有允许共享到演示区域的相应权限。|

## <a name="get-app-content-stage-sharing-state-api"></a>获取应用内容演示区域共享状态 API

`getAppContentStageSharingState` API 能够帮助获取有关应用在会议演示区域共享的内容信息。

### <a name="query-parameter"></a>查询参数

下表列出了查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**callback**| 字符串 | 是 | 回调包含 error 和 result 两个参数。 *error* 包含 *SdkError* 类型的错误（如果出错），或在共享成功时返回 null。 *result* 包含指示检索成功的 `AppContentStageSharingState` 对象，或指示检索失败的 null。|

### <a name="example"></a>示例

```javascript
microsoftTeams.meeting.getAppContentStageSharingState((err, result) => {
    if (result.isAppSharing) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

`getAppContentStageSharingState` API 的 JSON 响应正文为：

```json
{
   "isAppSharing":true
} 
```

### <a name="response-codes"></a>响应代码

下表列出了响应代码：

|响应代码|说明|
|---|---|
| **500** | 内部错误。 |
| **501** | 当前上下文不支持 API。|
| **1000** | 应用没有允许共享到演示区域的相应权限。|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>获取应用内容演示区域共享功能 API

`getAppContentStageSharingCapabilities` API 可帮助获取应用共享到会议演示区域的功能。

### <a name="query-parameter"></a>查询参数

下表列出了查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**callback**| 字符串 | 是 | 回调包含 error 和 result 两个参数。 *error* 包含 *SdkError* 类型的错误，或在共享成功时返回 null。 result 包含指示检索成功的 `AppContentStageSharingState` 对象，或指示检索失败的 null。|

### <a name="example"></a>示例

```javascript
microsoftTeams.meeting.getAppContentStageSharingCapabilities((err, result) => {
    if (result.doesAppHaveSharePermission) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

`getAppContentStageSharingCapabilities` API 的 JSON 响应正文为：

```json
{
   "doesAppHaveSharePermission":true
} 
```

### <a name="response-codes"></a>响应代码

下表列出了响应代码：

|响应代码|说明|
|---|---|
| **500** | 内部错误。 |
| **1000** | 应用没有允许共享到演示区域的权限。|

## <a name="get-real-time-teams-meeting-events-api"></a>获取实时 Teams 会议事件 API

用户可以接收实时会议事件。 只要任何应用与会议关联，就会与机器人共享会议实际开始时间和结束时间。 会议实际开始和结束时间不同于计划的开始和结束时间。 会议详细信息 API 提供计划的开始和结束时间。 该事件提供实际开始和结束时间。

必须熟悉通过 Bot SDK 提供的 `TurnContext` 对象。 `TurnContext`中的`Activity`对象包含具有实际开始和结束时间的有效负载。 实时会议事件需要 Teams 平台中的已注册机器人 ID。 机器人可以通过在清单中添加 `ChannelMeeting.ReadBasic.Group` 自动接收会议开始或结束事件。

### <a name="prerequisite"></a>先决条件

应用清单必须具有 `webApplicationInfo` 属性才能接收会议开始和结束事件。 使用以下示例配置清单：

<br>

<details>

<summary><b>针对应用清单版本 1.12</b></summary>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            }
        ]    
    }
}
 ```

<br>

</details>

<br>

<details>

<summary><b>针对应用清单版本 1.11 或更低版本</b></summary>

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

<br>

</details>

### <a name="example-of-getting-meetingstartendeventvalue"></a>获取 `MeetingStartEndEventvalue` 示例

机器人通过 `OnEventActivityAsync` 处理程序接收事件。 若要反序列化 JSON 有效负载，将引入一个模型对象来获取会议的元数据。 会议的元数据位于事件有效负载的 `value` 属性中。 创建 `MeetingStartEndEventvalue` 模型对象，其成员变量对应于事件有效负载中 `value` 属性下的键。

> [!NOTE]
>
> * 从 `turnContext.ChannelData` 获取会议 ID。
> * 请勿使用会话 ID 作为会议 ID。
> * 请勿使用会议事件有效负载 `turncontext.activity.value` 中的会议 ID。

以下代码演示如何从会议开始/结束事件中捕获会议元数据 `MeetingType`、`Title`、`Id`、`JoinUrl`、`StartTime` 和 `EndTime`：

会议开始事件

```csharp
protected override async Task OnTeamsMeetingStartAsync(MeetingStartEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    await turnContext.SendActivityAsync(JsonConvert.SerializeObject(meeting));
}
```

会议结束事件

```csharp
protected override async Task OnTeamsMeetingEndAsync(MeetingEndEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    await turnContext.SendActivityAsync(JsonConvert.SerializeObject(meeting));
}
```

### <a name="example-of-meeting-start-event-payload"></a>会议开始事件有效负载的示例

以下代码提供了会议开始事件有效负载的示例：

```json
{ 
    "name": "application/vnd.microsoft.meetingStart", 
    "type": "event", 
    "timestamp": "2021-04-29T16:10:41.1252256Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "userID", 
        "aadObjectId": "aadOnjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user Id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event", 
        "Id": "meeting id", 
        "JoinUrl": "url" 
        "StartTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

### <a name="example-of-meeting-end-event-payload"></a>会议结束事件有效负载的示例

以下代码提供了会议结束事件有效负载的示例：

```json
{ 
    "name": "application/vnd.microsoft.meetingEnd", 
    "type": "event", 
    "timestamp": "2021-04-29T16:17:17.4388966Z", 
    "id": "123", 
    "channelId": "msteams", 
    "serviceUrl": "https://microsoft.com", 
    "from": { 
        "id": "user id", 
        "aadObjectId": "aadObjectId" 
    }, 
    "conversation": { 
        "isGroup": true, 
        "tenantId": "tenantId", 
        "id": "thread id" 
    }, 
    "recipient": { 
        "id": "user id", 
        "name": "user name" 
    }, 
    "entities": [ 
        { 
            "locale": "en-US", 
            "country": "US", 
            "type": "clientInfo" 
        } 
    ], 
    "channelData": { 
        "tenant": { 
            "id": "channel id" 
        }, 
        "source": null, 
        "meeting": { 
            "id": "meeting Id" 
        } 
    }, 
    "value": { 
        "MeetingType": "Scheduled", 
        "Title": "Meeting Start/End Event in Canary", 
        "Id": "19:meeting_NTM3ZDJjOTUtZGRhOS00MzYxLTk5NDAtMzY4M2IzZWFjZGE1@thread.v2", 
        "JoinUrl": "url", 
        "EndTime": "2021-04-29T16:17:17.4388966Z" 
    }, 
    "locale": "en-US" 
}
```

## <a name="code-sample"></a>代码示例

|示例名称 | Description | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| 会议扩展性 | 用于传递令牌的 Microsoft Teams 会议扩展性示例。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| 会议内容气泡机器人 | Microsoft Teams 会议扩展性示例，用于在会议中与内容气泡机器人交互。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| 会议的 meetingSidePanel | Microsoft Teams 会议扩展性示例，演示与会内侧面板交互。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| 会议中的“详细信息”选项卡 | Microsoft Teams 会议扩展性示例，演示与会议中的“详细信息”选项卡进行交互。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|
|会议事件示例|显示实时 Teams 会议事件的示例应用|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/nodejs)|
|会议招聘示例|显示招聘情景的会议体验的示例应用。|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/nodejs)|
|使用 QR 代码安装应用|生成 QR 代码并使用 QR 代码安装应用的示例应用|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/nodejs)|

## <a name="see-also"></a>另请参阅

* [选项卡的 Teams 身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)
* [Teams 会议应用](teams-apps-in-meetings.md)
* [Live Share SDK](teams-live-share-overview.md)

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [为 Teams 会议启用和配置应用](enable-and-configure-your-app-for-teams-meetings.md)
