---
title: 会议应用 API 参考
author: surbhigupta
description: 使用示例和代码示例标识会议应用 API 引用
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: teams 应用会议用户参与者角色 api usercontext 通知信号查询
ms.openlocfilehash: dd46dc2622915055e46e07ae34d48c690d6d8d8e
ms.sourcegitcommit: 58a24422bb04a529b6629a56803ed2efabc17cb1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2022
ms.locfileid: "62323146"
---
# <a name="meeting-apps-api-references"></a>会议应用 API 参考

会议可扩展性提供了用于转换会议体验的 API：

* 在会议生命周期内生成应用或集成现有应用。
* 使用 API 让应用了解会议。
* 选择要用于增强会议体验的 API。

下表提供了 API 列表：

|API|说明|请求|Source|
|---|---|----|---|
|**GetUserContext**| 使您可以获取上下文信息，以在"开始"选项卡中Teams内容。 |_**microsoftTeams.getContext ( ( ) => { /*...*/ } )**_|Microsoft Teams客户端 SDK|
|**GetParticipant**| 使机器人能够按会议 ID 和参与者 ID 获取参与者信息。 |**GET** _**/v1/meetings/{meetingId}/participants/{participantId}？tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** | 使你可以提供使用用户-机器人聊天的现有对话通知 API 传递的会议信号。 它允许您根据显示会议内对话框的用户操作发出信号。 |**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|
|**会议详细信息** | 使您可以获取静态会议元数据。 |**GET** _**/v1/meetings/{meetingId}**_| Bot SDK |
|**CART**|使您可以发布会议的标题（已启动）。|**POST /cartcaption？meetingid=04751eac-30e6-47d9-9c3f-0b4ebe8e30d9&token=04751eac&lang=en-us HTTP/1.1**|Microsoft Teams客户端 SDK|

## <a name="getusercontext-api"></a>GetUserContext API

若要标识和检索选项卡内容的上下文信息，请参阅[获取 Teams](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library)`meetingId` 选项卡的上下文。选项卡在会议上下文中运行时使用，并添加用于响应负载。

## <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * 不要缓存参与者角色，因为会议组织者可以随时更改角色。
> * Teams当前不支持超过 350 个参与者的大型通讯组列表或名单大小，`GetParticipant`API。

API `GetParticipant` 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。 API 包括查询参数、示例和响应代码。

### <a name="query-parameters"></a>查询参数

API `GetParticipant` 包括以下查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**meetingId**| 字符串 | 是 | 会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。|
|**participantId**| 字符串 | 是 | 参与者 ID 是用户 ID。 它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。 建议从选项卡 SSO 获取参与者 ID。 |
|**tenantId**| 字符串 | 是 | 租户用户需要租户 ID。 它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。 建议从选项卡 SSO 获取租户 ID。 |

### <a name="example"></a>示例

API `GetParticipant` 包括以下示例：

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

API 的 JSON 响应正文 `GetParticipant` 为：

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

API `GetParticipant` 返回以下响应代码：

|响应代码|说明|
|---|---|
| **403** | 不会与应用共享获取参与者信息。 如果会议未安装该应用，它将触发最常见的错误响应 403。 如果租户管理员在实时网站迁移期间禁用或阻止应用，将触发 403 错误响应。 |
| **200** | 成功检索参与者信息。|
| **401** | 应用使用无效令牌进行响应。|
| **404** | 会议已过期或找不到参与者。|

## <a name="notificationsignal-api"></a>NotificationSignal API

会议中的所有用户都接收通过 API 发送的通知 `NotificationSignal` 。

> [!NOTE]
> * 调用会议内对话框时，内容将显示为聊天消息。
> * 目前，不支持发送定向通知。

`NotificationSignal` API 使你能够提供使用用户-机器人聊天的现有对话通知 API 传递的会议信号。 此 API 允许你根据显示会议内对话框的用户操作发出信号。 API 包括查询参数、示例和响应代码。

### <a name="query-parameter"></a>查询参数

API `NotificationSignal` 包括以下查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**conversationId**| 字符串 | 是 | 对话标识符作为 Bot Invoke 的一部分提供。 |

### <a name="examples"></a>示例

在 `Bot ID` 清单中声明，机器人将接收结果对象。

> [!NOTE]
> * 在 `completionBotId` 请求 `externalResourceUrl` 的有效负载示例中，的 参数是可选的。 `Bot ID` 在清单中声明，机器人将接收结果对象。
> * 宽度 `externalResourceUrl` 和高度参数必须以像素为单位。 若要确保尺寸在允许的限制内，请参阅 [设计指南](design/designing-apps-in-meetings.md)。
> * URL 是在会议对话框中作为 `<iframe>` 加载的页面。 域必须在你的应用清单的应用 `validDomains` 数组中。

API `NotificationSignal` 包括以下示例：

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

API `NotificationSignal` 包括以下响应代码：

|响应代码|说明|
|---|---|
| **201** | 具有信号的活动已成功发送。 |
| **401** | 应用使用无效令牌进行响应。 |
| **403** | 应用无法发送信号。 403 响应代码可能由于各种原因发生，例如租户管理员在实时网站迁移期间禁用和阻止应用。 在这种情况下，有效负载包含详细的错误消息。 |
| **404** | 会议聊天不存在。 |

## <a name="meeting-details-api"></a>会议详细信息 API

> [!NOTE]
> 此功能目前仅适用于公共 [开发人员预览](../resources/dev-preview/developer-preview-intro.md) 版。

会议详细信息 API 使你的应用能够获取静态会议元数据。 元数据提供不动态更改的数据点。
API 通过 Bot Services 提供。

### <a name="prerequisite"></a>先决条件

> [!NOTE] 
> 检查你的应用是否满足会议中的应用先决条件中列出的Teams[先决条件](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md)。

若要使用会议详细信息 API，必须获取 RSC 权限。 使用以下示例配置应用清单的属性 `webApplicationInfo` ：

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```
### <a name="query-parameter"></a>查询参数

会议详细信息 API 包括以下查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**meetingId**| 字符串 | 是 | 会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。 |

### <a name="example"></a>示例

会议详细信息 API 包括以下示例：

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
            “conversationType”: “groupchat”, 
            "id": "meeting chat ID" 
    }, 
    "organizer": { 
        "id": "<organizer user ID>", 
        "aadObjectId": "<AAD ID>", 
        "tenantId": "<Tenant ID>" 
    }
} 
```

## <a name="cart-api"></a>购物车 API

通信访问实时翻译 (CART) API 公开了一个 POST 终结点Microsoft Teams购物车标题、人工类型的隐藏式字幕。 发送到此终结点的文本内容在启用了标题Microsoft Teams向会议中的最终用户显示。

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

购物车 API 包括以下错误代码：

|错误代码|说明|
|---|---|
| **400** | 请求错误。 响应正文包含详细信息。 例如，并非所有必需的参数都呈现。|
| **401** | 未经授权。 令牌错误或过期。 如果收到此错误，请生成一个新的购物车 URL，Teams。 |
| **404** | 未找到或未启动会议。 如果收到此错误，请确保启动会议并选择"开始"标题。 在会议启用字幕后，可以开始在会议中放入字幕。|
| **500** |内部服务器错误。 有关详细信息，请联系 [支持人员或提供反馈](../feedback.md)。|

## <a name="real-time-teams-meeting-events"></a>实时Teams会议事件

用户可以接收实时会议事件。 只要任何应用与会议关联，就会与机器人共享实际会议开始时间和结束时间。

会议的实际开始时间和结束时间与计划的开始时间和结束时间不同。 会议详细信息 API 提供计划的开始时间和结束时间。 该事件提供实际的开始时间和结束时间。

### <a name="prerequisite"></a>先决条件

> [!NOTE] 
> 检查你的应用是否满足会议中的应用先决条件中列出的Teams[先决条件](~/apps-in-teams-meetings/create-apps-for-teams-meetings.md)。

应用清单必须具有 属性 `webApplicationInfo` ，以接收会议开始和结束事件。 使用以下示例配置清单：

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
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

### <a name="example-of-getting-metadata-of-a-meeting"></a>获取会议元数据的示例

机器人通过处理程序接收 `OnEventActivityAsync` 事件。

为了反初始化 json 有效负载，引入了一个模型对象，用于获取会议元数据。 会议元数据位于事件有效 `value` 负载中的 属性中。 将 `MeetingStartEndEventvalue` 创建模型对象，其成员变量对应于 `value` 事件有效负载中的 属性下的键。
     
> [!NOTE]      
> * 从 获取会议 `turnContext.ChannelData`ID。    
> * 不要将对话 ID 用作会议 ID。     
> * 请勿使用会议事件有效负载中的会议 ID `turncontext.activity.value`。 
      
以下代码演示如何从`MeetingType``EndTime``Title``Id``JoinUrl``StartTime`会议开始/结束事件捕获会议元数据，即 、 和 ：

会议开始事件
```csharp
protected override async Task OnTeamsMeetingStartAsync(MeetingEndEventDetails meeting, ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
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
> [为会议启用和配置Teams应用程序](enable-and-configure-your-app-for-teams-meetings.md)
