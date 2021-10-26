---
title: Teams 会议中应用的先决条件
author: surbhigupta
description: 确定会议Teams的先决条件
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: 2cd0012a36d3cc941ebcf7e83a4156c9780149a6
ms.sourcegitcommit: 781e7b82240075e9d1f55e97f3f1dcbba82a5e4d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/25/2021
ms.locfileid: "60566132"
---
# <a name="prerequisites-for-apps-in-teams-meetings"></a>Teams 会议中应用的先决条件

借助Teams会议，可以在会议生命周期内扩展应用的功能。 使用会议Teams之前，必须满足以下先决条件：

* 了解如何开发Teams应用程序。 若要详细了解如何开发应用Teams，请参阅Teams[应用开发](../overview.md)。

* 更新Teams应用清单，以指示该应用可用于会议。 有关详细信息，请参阅 [应用清单](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)。

* 使用支持 groupchat 作用域中的可配置选项卡的应用。 有关详细信息，请参阅群[聊范围和](../resources/schema/manifest-schema.md#configurabletabs)[构建组选项卡](../build-your-first-app/build-channel-tab.md)。

* 遵守Teams和会议后方案的常规选项卡设计准则。 有关会议期间的体验，请参阅会议中的选项卡和会议内对话框设计指南。 有关详细信息，请参阅Teams[选项卡设计指南](../tabs/design/tabs.md)、会议中的[选项卡](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)设计指南和[会议中的对话框设计指南](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

* 支持 `groupchat` 范围以在会议前和会议后聊天中启用你的应用。 通过会议前应用体验，你可以查找和添加会议应用，以及执行会议前任务。 使用会议后应用体验，可以查看会议结果，例如投票调查结果或费用
* 会议 API URL 参数必须具有 `meetingId` 、 `userId` 和 `tenantId` 。 这些参数作为客户端 SDK 和自动程序Teams的一部分提供。 此外，您可以使用选项卡 SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。

* `GetParticipant`API 必须具有自动程序注册和 ID，以生成身份验证令牌。 有关详细信息，请参阅自动[程序注册和 ID。](../build-your-first-app/build-bot.md)

* 若要实时更新应用，应用必须基于会议中的活动活动是最新的。 这些事件可以位于会议中的对话框内以及整个会议生命周期的其他阶段。 有关会议中的对话框，请参阅 `bot Id` API 中的完成 `NotificationSignal` 参数。

* `Meeting Details`API 必须具有自动程序注册和自动程序 ID。 它需要 Bot SDK 才能获取 `TurnContext` 。

* 对于实时会议事件，你必须熟悉通过 `TurnContext` Bot SDK 提供的对象。 `Activity`中的 `TurnContext` 对象包含具有实际开始时间和结束时间的有效负载。 实时会议事件需要来自会议平台的已注册Teams ID。

完成先决条件后，可以使用会议应用 API 引用 、 、 和 ，以便使用 属性访问信息并显示 `GetUserContext` `GetParticipant` `NotificationSignal` `Meeting Details` 相关内容。

## <a name="meeting-apps-api-references"></a>会议应用 API 参考

以下新的会议扩展提供了用于转换会议体验的 API：

* 在会议生命周期内生成应用或集成现有应用。
* 使用 API 让应用了解会议。
* 选择要用于增强会议体验的 API。

下表提供了这些 API 的列表：

|API|说明|请求|Source|
|---|---|----|---|
|**GetUserContext**| 此 API 使你能够获取上下文信息，以在"开始"选项卡中Teams内容。 |_**microsoftTeams.getContext ( ( ) => { /*...*/ } )**_|Microsoft Teams客户端 SDK|
|**GetParticipant**| 此 API 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。 |**GET** _**/v1/meetings/{meetingId}/participants/{participantId}？tenantId={tenantId}**_ |Microsoft Bot FrameworkSDK|
|**NotificationSignal** | 此 API 使你能够提供使用用户-机器人聊天的现有对话通知 API 传递的会议信号。 它允许您根据显示会议内对话框的用户操作发出信号。 |**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot FrameworkSDK|
|**会议详细信息** | 此 API 使你能够获取静态会议元数据。 |**GET** _**/v1/meetings/{meetingId}**_| Bot SDK |

下表提供了适用于 API 的 Bot Framework SDK 方法：

|API|Bot Framework SDK 方法|
|---|---|
|**GetParticipant**| `GetMeetingParticipantAsync (Microsoft.Bot.Builder.ITurnContext turnContext, string meetingId = default, string participantId = default, string tenantId = default, System.Threading.CancellationToken cancellationToken = default);` |
|**NotificationSignal** | `activity.TeamsNotifyUser(true, "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<title>&completionBotId=BOT_APP_ID");` |
|**会议详细信息** | `TeamsMeetingInfo (string id = default);` |

### <a name="getusercontext-api"></a>GetUserContext API

若要标识和检索选项卡内容的上下文信息，请参阅获取选项卡[Teams上下文](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library)。`meetingId`在会议上下文中运行时选项卡使用，并添加响应有效负载。

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * 不要缓存参与者角色，因为会议组织者可以随时更改角色。
> * Teams API 当前不支持超过 350 个参与者的大型通讯组列表或名单 `GetParticipant` 大小。

API `GetParticipant` 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。 API 包括查询参数、示例和响应代码。 该 API 在专用计划会议或定期会议以及频道计划会议或定期会议中均受支持。 

#### <a name="query-parameters"></a>查询参数

`GetParticipant`API 包括以下查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**meetingId**| 字符串 | 是 | 会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。|
|**participantId**| 字符串 | 是 | 参与者 ID 是用户 ID。 它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。 建议从选项卡 SSO 获取参与者 ID。 |
|**tenantId**| 字符串 | 是 | 租户用户需要租户 ID。 它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。 建议从选项卡 SSO 获取租户 ID。 |

#### <a name="example"></a>示例

`GetParticipant`API 包括以下示例：

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

API 的 JSON 响应 `GetParticipant` 正文为：

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

#### <a name="response-codes"></a>响应代码

`GetParticipant`API 返回以下响应代码：

|响应代码|说明|
|---|---|
| **403** | 不会与应用共享获取参与者信息。 如果会议未安装该应用，它将触发最常见的错误响应 403。 如果租户管理员在实时网站迁移期间禁用或阻止应用，将触发 403 错误响应。 |
| **200** | 成功检索参与者信息。|
| **401** | 应用使用无效令牌进行响应。|
| **404** | 会议已过期或找不到参与者。|

### <a name="notificationsignal-api"></a>NotificationSignal API

会议中的所有用户都接收通过 API 发送 `NotificationSignal` 的通知。

> [!NOTE]
> * 调用会议中的对话框时，内容将显示为聊天消息。
> * 目前，不支持发送定向通知。

API 使你能够提供使用用户-机器人聊天的现有对话通知 API 传递 `NotificationSignal` 的会议信号。 此 API 允许你根据显示会议内对话框的用户操作发出信号。 API 包括查询参数、示例和响应代码。

#### <a name="query-parameter"></a>查询参数

`NotificationSignal`API 包括以下查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**conversationId**| 字符串 | 是 | 对话标识符作为 Bot Invoke 的一部分提供。 |

#### <a name="examples"></a>示例

`Bot ID`在清单中声明，机器人将接收结果对象。

> [!NOTE]
> * `completionBotId`在请求 `externalResourceUrl` 的有效负载示例中，的 参数是可选的。 `Bot ID` 在清单中声明，机器人将接收结果对象。
> * `externalResourceUrl`宽度和高度参数必须以像素为单位。 若要确保尺寸在允许的限制内，请参阅 [设计指南](design/designing-apps-in-meetings.md)。
> * URL 是在会议对话框中作为 `<iframe>` 加载的页面。 域必须在你的应用清单 `validDomains` 的应用数组中。

`NotificationSignal`API 包括以下示例：

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
        externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID'
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

#### <a name="response-codes"></a>响应代码

`NotificationSignal`API 包括以下响应代码：

|响应代码|说明|
|---|---|
| **201** | 具有信号的活动已成功发送。 |
| **401** | 应用使用无效令牌进行响应。 |
| **403** | 应用无法发送信号。 403 响应代码可能由于各种原因发生，例如租户管理员在实时网站迁移期间禁用和阻止应用。 在这种情况下，有效负载包含详细的错误消息。 |
| **404** | 会议聊天不存在。 |

### <a name="meeting-details-api"></a>会议详细信息 API

> [!NOTE]
> 此功能目前仅适用于公共 [开发人员预览](../resources/dev-preview/developer-preview-intro.md) 版。

`Meeting Details`API 使你的应用能够获取静态会议元数据。 元数据提供不动态更改的数据点。
API 通过 Bot Services 提供。

#### <a name="prerequisite"></a>先决条件

若要使用 `Meeting Details` API，必须获取 RSC 权限。 使用以下示例配置应用清单 `webApplicationInfo` 的属性：

```json
"webApplicationInfo": {
    "id": "<bot id>",
    "resource": "https://RscPermission",
    "applicationPermissions": [
      "OnlineMeeting.ReadBasic.Chat"
    ]
}
 ```
 
#### <a name="query-parameter"></a>查询参数

`Meeting Details`API 包括以下查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**meetingId**| 字符串 | 是 | 会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。 |

#### <a name="example"></a>示例

`Meeting Details`API 包括以下示例：

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

API 的 JSON 响应 `Meeting Details` 正文如下所示：

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

## <a name="real-time-teams-meeting-events"></a>实时Teams会议事件

用户可以接收实时会议事件。 只要任何应用与会议关联，就会与机器人共享实际会议开始时间和会议结束时间。

会议的实际开始时间和结束时间与计划的开始时间和结束时间不同。 `Meeting Details`API 提供计划的开始时间和结束时间。 该事件提供实际的开始时间和结束时间。

### <a name="prerequisite"></a>先决条件

应用清单必须具有 `webApplicationInfo` 属性，以接收会议开始和结束事件。 使用以下示例配置清单：

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

为了反初始化 JSON 有效负载，引入了一个模型对象，用于获取会议元数据。 会议元数据位于事件 `value` 有效负载中的 属性中。 将 `MeetingStartEndEventvalue` 创建模型对象，其成员变量对应于事件有效负载 `value` 中的 属性下的键。
     
> [!NOTE]      
> * 从 获取会议 `turnContext.ChannelData` ID。    
> * 不要将对话 ID 用作会议 ID。     
> * 请勿使用会议事件有效负载中的会议 `turncontext.activity.value` ID。 
      
以下代码演示如何从会议开始/结束事件捕获会议元数据，即 、 和 `MeetingType` `Title` `Id` `JoinUrl` `StartTime` `EndTime` ：

会议开始事件

```csharp
protected override async Task OnEventActivityAsync(
ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
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

* 在会议 API URL 中具有 参数 `meetingId` `userId` 、 和 `tenantId` 。 这些参数作为客户端 SDK 和自动程序Teams的一部分提供。 此外，您可以使用选项卡 SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。

* 在 API 中拥有自动程序注册 `GetParticipant` 和 ID 以生成身份验证令牌。 有关详细信息，请参阅自动[程序注册和 ID。](../build-your-first-app/build-bot.md)

* 根据会议中的活动活动使应用保持最新。 这些事件可以位于会议中的对话框内以及整个会议生命周期的其他阶段。 对于"会议内"对话框，请检查 API `bot Id` 中的完成 `NotificationSignal` 参数。

* 在 API 中拥有自动程序注册和自动程序 `MeetingDetails` ID。 它需要 Bot SDK 才能获取 `TurnContext` 。

* 熟悉通过 `TurnContext` Bot SDK 提供的对象。 `Activity`中的 `TurnContext` 对象包含具有实际开始时间和结束时间的有效负载。 实时会议事件需要来自会议平台的已注册Teams ID。

## <a name="see-also"></a>另请参阅

* [会议内对话设计指南](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams选项卡的身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)
* [会议Teams应用程序](teams-apps-in-meetings.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [会议应用 API 参考](API-references.md)
