---
title: 会议应用 API 参考
author: surbhigupta
description: 使用示例和代码示例标识会议应用 API 引用
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: teams 应用会议用户参与者角色 api 用户上下文通知信号查询
ms.openlocfilehash: 2ed9f1682ff3de9022d3de3f93bbfc07933e7b4c
ms.sourcegitcommit: 2fdca6fb0ade3f6b460eb9a4dfea0a8e2ab8d3b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/08/2022
ms.locfileid: "63355788"
---
# <a name="meeting-apps-api-references"></a>会议应用 API 参考

会议扩展性提供了用于增强会议体验的 API。 你可以借助列出的 API 执行以下操作：

* 在会议生命周期内生成应用或集成现有应用。
* 使用 API 让应用了解会议。
* 选择所需的 API 以改进会议体验。

下表提供了跨 MICROSOFT TEAMS Client (MSTC) Microsoft Bot Framework (SDK) API 的列表：

|方法| 说明| 源|
|---|---|----|
|[**获取用户上下文**](#get-user-context-api)| 获取上下文信息以在"列表"选项卡中Teams内容。| MSTC SDK|
|[**获取参与者**](#get-participant-api)| 按会议 ID 和参与者 ID 提取参与者信息。 |MSBF SDK|
|[**发送会议内通知**](#send-an-in-meeting-notification)| 使用用户-机器人聊天的现有对话通知 API 提供会议信号，并允许通知显示会议内通知的用户操作。 |MSBF SDK|
|[**获取会议详细信息**](#get-meeting-details-api)| 获取会议静态元数据。 |MSBF SDK |
|[**发送实时字幕**](#send-real-time-captions-api)| 向正在进行的会议发送实时字幕。 |MSTC SDK|
|[**将应用内容共享到阶段**](#share-app-content-to-stage-api)| 从会议的应用侧面板将应用的特定部分共享到会议阶段。 |MSTC SDK|
|[**获取应用内容阶段共享状态**](#get-app-content-stage-sharing-state-api)| 获取有关会议阶段的应用共享状态的信息。 |MSTC SDK|
|[**获取应用内容阶段共享功能**](#get-app-content-stage-sharing-capabilities-api)| 获取应用共享到会议阶段的功能。 |MSTC SDK|
|[**获取实时Teams会议事件**](#get-real-time-teams-meeting-events-api)|获取实时会议事件，如实际开始时间和结束时间。| MSBF SDK|

## <a name="get-user-context-api"></a>获取用户上下文 API

若要标识和检索选项卡内容的上下文信息，请参阅[获取 Teams](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library)`meetingId` 选项卡的上下文。由在会议上下文中运行的选项卡使用，并添加用于响应负载。

## <a name="get-participant-api"></a>获取参与者 API

> [!NOTE]
> * 不要缓存参与者角色，因为会议组织者可以随时更改角色。
> * 目前， `GetParticipant` 只有参与者少于 350 名的通讯组列表或名单才支持 API。

### <a name="query-parameters"></a>查询参数

> [!TIP]
> 从选项卡 SSO 获取参与者 ID 和租户 ID。

下表包含查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**meetingId**| 字符串 | 是 | 会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。|
|**participantId**| 字符串 | 是 | 参与者 ID 是用户 ID。 它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。 建议从选项卡 SSO 获取参与者 ID。 |
|**tenantId**| 字符串 | 是 | 租户用户需要租户 ID。 它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。 建议从选项卡 SSO 获取租户 ID。 |

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

---

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

### <a name="response-codes"></a>响应代码

下表提供了响应代码：

|响应代码|说明|
|---|---|
| **403** | 不会与应用共享获取参与者信息。 如果会议未安装该应用，它将触发错误响应 403。 如果租户管理员在实时网站迁移期间禁用或阻止应用，它将触发错误响应 403。 |
| **200** | 成功检索参与者信息。|
| **401** | 应用使用无效令牌进行响应。|
| **404** | 会议已过期或参与者不可用。|

## <a name="send-an-in-meeting-notification"></a>发送会议内通知

会议中的所有用户都接收通过会议内通知有效负载发送的通知。 会议通知负载触发会议内通知，并允许您提供使用用户-机器人聊天的现有对话通知 API 传递的会议信号。 你可以根据用户操作发送会议内通知。 有效负载通过 Bot Services 提供。

> [!NOTE]
> * 调用会议内通知时，内容将显示为聊天消息。
> * 目前，不支持发送目标通知和支持 webapp。
> * 您必须调用 [submitTask () ](../task-modules-and-cards/task-modules/task-modules-bots.md#submit-the-result-of-a-task-module) 函数，以在用户执行 Web 视图中的操作后自动消除。 这是应用提交的要求。 有关详细信息，请参阅Teams [SDK 任务模块](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。 
> * 如果希望你的应用支持匿名用户，初始调用请求有效负载必须依赖于 `from.id` 对象中的 `from` 请求元数据，而不是 `from.aadObjectId` 请求元数据。 `from.id`是用户 ID，`from.aadObjectId`Microsoft Azure Active Directory (Azure AD) ID。 有关详细信息，请参阅在 [选项卡中使用任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md) 以及 [创建和发送任务模块](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。

### <a name="query-parameter"></a>查询参数

下表包含查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**conversationId**| 字符串 | 是 | 对话标识符作为 Bot Invoke 的一部分提供。 |

### <a name="examples"></a>示例

在 `Bot ID` 清单中声明，机器人将接收结果对象。

> [!NOTE]
> * 在 `completionBotId` 请求 `externalResourceUrl` 的有效负载示例中，的 参数是可选的。
> * 宽度 `externalResourceUrl` 和高度参数必须以像素为单位。 有关详细信息，请参阅 [设计指南](design/designing-apps-in-meetings.md)。
> * URL 是页面，加载时与在 `<iframe>` 会议通知中一样。 域必须在你的应用清单中的 `validDomains` 应用数组中。

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

下表包含响应代码：

|响应代码|说明|
|---|---|
| **201** | 具有信号的活动已成功发送。 |
| **401** | 应用使用无效令牌进行响应。 |
| **403** | 应用无法发送信号。 403 响应代码可能由于各种原因发生，例如租户管理员在实时网站迁移期间禁用和阻止应用。 在这种情况下，有效负载包含详细的错误消息。 |
| **404** | 会议聊天不存在。 |

## <a name="get-meeting-details-api"></a>获取会议详细信息 API

会议详细信息 API 使你的应用能够获取会议静态元数据。 元数据提供不动态更改的数据点。 API 通过 Bot Services 提供。 目前，私人计划会议或定期会议以及频道计划会议或定期会议均支持分别具有不同的 RSC 权限的 API。

### <a name="prerequisite"></a>先决条件

若要使用会议详细信息 API，必须基于任何会议的范围（如私人会议或频道会议）获取不同的 RSC 权限。

<br>

<details>

<summary><b>对于应用清单版本 1.12</b></summary>

使用以下示例配置任何私人会议`webApplicationInfo``authorization`的应用清单和属性：

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

使用以下示例为任何频道会议`webApplicationInfo``authorization`配置应用清单和属性：

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

<summary><b>对于应用清单版本 1.11 或更早版本</b></summary>

使用以下示例为任何私人会议配置 `webApplicationInfo` 应用清单的属性：

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```

使用以下示例为任何频道会议配置 `webApplicationInfo` 应用清单的属性：

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
> 机器人可以通过向清单添加 `ChannelMeeting.ReadBasic.Group` RSC 权限，自动接收所有频道中创建的所有会议的会议开始或结束事件。
 
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

---

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

## <a name="send-real-time-captions-api"></a>发送实时字幕 API

发送实时标题 API 公开了一个 POST 终结点，Microsoft Teams通信访问实时翻译 (CART) 标题、人工类型的隐藏式字幕。 当最终用户启用标题时，发送到此终结点的文本Microsoft Teams向会议中的最终用户显示。

### <a name="cart-url"></a>购物车 URL

可以从会议选项页获取 POST 终结点的购物车 **URL，Microsoft Teams** 会议。 有关详细信息，请参阅会议[中的购物车Microsoft Teams标题](https://support.microsoft.com/office/use-cart-captions-in-a-microsoft-teams-meeting-human-generated-captions-2dd889e8-32a8-4582-98b8-6c96cf14eb47)。 无需修改购物车 URL 即可使用购物车标题。

#### <a name="query-parameter"></a>查询参数

购物车 URL 包括以下查询参数：

|值|类型|必需|说明|
|---|---|----|----|
|**meetingId**| 字符串 | 是 |会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。 <br/>例如， meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241 -47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d|
|**token**| 字符串 | 是 |授权令牌。<br/> 例如，token=04751eac |

#### <a name="example"></a>示例

```http
https://api.captions.office.microsoft.com/cartcaption?meetingid=%7b%22tId%22%3a%2272f234bf-86f1-41af-91ab-2d7cd0321b47%22%2c%22oId%22%3a%22e071f268-4241-47f8-8cf3-fc6b84437f23%22%2c%22thId%22%3a%2219%3ameeting_NzJiMjNkMGQtYzk3NS00ZDI1LWJjN2QtMDgyODVhZmI3NzJj%40thread.v2%22%2c%22mId%22%3a%220%22%7d&token=gjs44ra
```

### <a name="method"></a>方法

|资源|方法|说明|
|----|----|----|
|/cartcaption|POST|处理会议的标题（已启动）|

> [!NOTE]
> 确保所有请求的内容类型都是使用 UTF-8 编码的纯文本。 请求正文仅包含标题。

#### <a name="example"></a>示例

```http
POST /cartcaption?meetingid=04751eac-30e6-47d9-9c3f-0b4ebe8e30d9&token=04751eac&lang=en-us HTTP/1.1
Host: api.captions.office.microsoft.com
Content-Type: text/plain
Content-Length: 22
Hello I’m Cortana, welcome to my meeting. 
```

> [!Note]  
> 每个 POST 请求都会生成一个新标题行。 为了确保最终用户有足够的时间阅读内容，将每个 POST 请求正文限制为 80-120 个字符。

### <a name="error-codes"></a>错误代码

下表提供了错误代码：

|错误代码|说明|
|---|---|
| **400** | 请求错误。 响应正文包含详细信息。 例如，并非所有必需的参数都呈现。|
| **401** | 未经授权。 令牌错误或过期。 如果收到此错误，请生成一个新的购物车 URL，Teams。 |
| **404** | 未找到或未启动会议。 如果收到此错误，请确保启动会议并选择"开始"标题。 在会议启用字幕后，可以开始在会议中放入字幕。|
| **500** |内部服务器错误。 有关详细信息，请联系 [支持人员或提供反馈](../feedback.md)。|

## <a name="share-app-content-to-stage-api"></a>共享应用内容以阶段 API

API `shareAppContentToStage` 使你能够将应用的特定部分共享到会议阶段。 API 通过 Teams SDK 提供。

### <a name="prerequisite"></a>先决条件

若要使用 `shareAppContentToStage` API，必须获取 RSC 权限。 在应用程序清单中，在 `authorization` 字段中配置 `name` `type` 属性和 和 `resourceSpecific` 。 例如：

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

### <a name="query-parameter"></a>查询参数

下表包含查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**callback**| 字符串 | 是 | Callback 包含两个参数，即 error 和 result。 该 *错误* 可以包含 *SdkError 类型的错误，或* 共享成功时为 null。 *结果* 可以包含 true 值（如果共享成功）或 null（如果共享失败）。|
|**appContentURL**| 字符串 | 是 | 要共享到该阶段的 URL。|

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

下表提供了响应代码：

|响应代码|说明|
|---|---|
| **500** | 内部错误。 |
| **501** | API 在当前上下文中不受支持。|
| **1000** | 应用没有允许共享阶段的适当权限。|

## <a name="get-app-content-stage-sharing-state-api"></a>获取应用内容阶段共享状态 API

API `getAppContentStageSharingState` 使你能够获取有关会议阶段的应用共享的信息。

### <a name="query-parameter"></a>查询参数

下表包含查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**callback**| 字符串 | 是 | Callback 包含两个参数，即 error 和 result。 *如果出现错误*，该错误可以包含 *SdkError* 类型的错误，或者在共享成功时为 null。 *结果可以包含* 指示`AppContentStageSharingState`检索成功的对象，也可以包含 null（表示检索失败）。|

### <a name="example"></a>示例

```javascript
microsoftTeams.meeting.getAppContentStageSharingState((err, result) => {
    if (result.isAppSharing) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
``` 

API 的 JSON 响应 `getAppContentStageSharingState` 正文为：

```json
{
   "isAppSharing":true
} 
```

### <a name="response-codes"></a>响应代码

下表提供了响应代码：

|响应代码|说明|
|---|---|
| **500** | 内部错误。 |
| **501** | API 在当前上下文中不受支持。|
| **1000** | 应用没有允许共享阶段的适当权限。|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>获取应用内容阶段共享功能 API

通过 `getAppContentStageSharingCapabilities` API，你可以获取应用用于共享到会议阶段的功能。

### <a name="query-parameter"></a>查询参数

下表包含查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**callback**| 字符串 | 是 | Callback 包含两个参数，即 error 和 result。 该 *错误* 可以包含 *SdkError 类型的错误，或* 共享成功时为 null。 结果可以包含指示 `AppContentStageSharingState` 检索成功的对象，也可以包含 null（表示检索失败）。|

### <a name="example"></a>示例

```javascript
microsoftTeams.meeting.getAppContentStageSharingCapabilities((err, result) => {
    if (result.doesAppHaveSharePermission) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
``` 

API 的 JSON 响应正文 `getAppContentStageSharingCapabilities` 为：

```json
{
   "doesAppHaveSharePermission":true
} 
```

### <a name="response-codes"></a>响应代码

下表提供了响应代码：

|响应代码|说明|
|---|---|
| **500** | 内部错误。 |
| **1000** | 应用无权允许共享到阶段。|

## <a name="get-real-time-teams-meeting-events-api"></a>获取实时会议Teams API

用户可以接收实时会议事件。 只要任何应用与会议关联，就会与机器人共享实际会议开始时间和结束时间。 会议的实际开始时间和结束时间不同于计划的开始时间和结束时间。 会议详细信息 API 提供计划的开始时间和结束时间。 该事件提供实际的开始时间和结束时间。

### <a name="prerequisite"></a>先决条件

应用清单必须具有 属性 `webApplicationInfo` ，以接收会议开始和结束事件。 使用以下示例配置清单：

<br>

<details>

<summary><b>对于应用清单版本 1.12</b></summary>

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

<summary><b>对于应用清单版本 1.11 或更早版本</b></summary>

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

### <a name="example-of-getting-meetingstartendeventvalue"></a>获取示例 `MeetingStartEndEventvalue`

机器人通过处理程序接收 `OnEventActivityAsync` 事件。 为了反初始化 JSON 有效负载，引入了一个模型对象，用于获取会议元数据。 会议元数据位于事件有效 `value` 负载中的 属性中。 将 `MeetingStartEndEventvalue` 创建模型对象，其成员变量对应于 `value` 事件有效负载中的 属性下的键。

> [!NOTE]
> * 从 获取会议 `turnContext.ChannelData`ID。
> * 不要将对话 ID 用作会议 ID。
> * 请勿使用会议事件有效负载中的会议 ID `turncontext.activity.value`。

以下代码演示如何从`MeetingType``EndTime``Title``Id``JoinUrl``StartTime`会议开始/结束事件捕获会议元数据，即 、 和 ：

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
| 会议可扩展性 | Microsoft Teams令牌的会议扩展性示例。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| 会议内容气泡机器人 | Microsoft Teams会议扩展性示例，用于与会议内容气泡机器人进行交互。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| Meeting meetingSidePanel | Microsoft Teams与会议中的侧面板交互的会议扩展性示例。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| 会议详细信息选项卡 | Microsoft Teams会议扩展性示例，用于与会议中的"详细信息"选项卡进行交互。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|
|会议事件示例|显示实时会议事件Teams应用|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-events/nodejs)|
|会议招聘示例|用于显示招聘方案的会议体验的示例应用。|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meeting-recruitment-app/nodejs)|
|使用 QR 代码安装应用|生成 QR 代码和使用 QR 代码安装应用的示例应用|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-installation-using-qr-code/nodejs)|

## <a name="see-also"></a>另请参阅

* [Teams选项卡的身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)
* [Teams 会议应用](teams-apps-in-meetings.md)

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [为会议启用和配置Teams应用](enable-and-configure-your-app-for-teams-meetings.md)
