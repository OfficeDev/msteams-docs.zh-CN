---
title: Teams 会议中应用的先决条件和 API 参考
author: surbhigupta
description: 使用用于会议Teams应用程序
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: bc13fa7b8c3af9a7c48463eab7198e908164ffbe
ms.sourcegitcommit: 0a775ae12419f3bc7484e557f4b4ae815bab64ec
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2021
ms.locfileid: "53333685"
---
# <a name="prerequisites-and-api-references-for-apps-in-teams-meetings"></a>Teams 会议中应用的先决条件和 API 参考

若要在会议生命周期内扩展应用功能，Teams使用会议Teams应用程序。 必须完成先决条件，并且可以使用会议应用 API 引用来增强会议体验。

## <a name="prerequisites"></a>先决条件

使用用于会议Teams，您必须了解以下内容：

* 你必须知道如何开发应用Teams知识。 有关详细信息，请参阅应用[Teams开发](../overview.md)。

* 必须更新Teams清单，以指示该应用可用于会议。 有关详细信息，请参阅 [应用清单](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)。

* 您的应用程序必须支持 groupchat 作用域中的可配置选项卡，你的应用必须在会议生命周期中作为选项卡运行。有关详细信息，请参阅 [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md)。

* 对于会议前和Teams方案，必须遵循常规选项卡设计准则。 有关会议期间的体验，请参阅会议内选项卡和会议内对话框设计指南。 有关详细信息，请参阅Teams[选项卡设计指南](../tabs/design/tabs.md)、会议中的[选项卡](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)设计指南和[会议中的对话框设计指南](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

* 必须支持范围才能在会议前和会议后聊天 `groupchat` 中启用应用。 通过会议前应用体验，你可以查找和添加会议应用并执行会议前任务。 通过会议后应用体验，可以查看会议结果，如投票调查结果或反馈。

* 会议 API URL 参数必须具有 `meetingId` 、 `userId` 和 `tenantId` 。 它们作为客户端 SDK 和自动程序Teams的一部分提供。 此外，您可以使用选项卡 SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。

* `GetParticipant`API 必须具有自动程序注册和 ID，以生成身份验证令牌。 有关详细信息，请参阅自动[程序注册和 ID。](../build-your-first-app/build-bot.md)

* 若要实时更新应用，应用必须基于会议中的活动活动是最新的。 这些事件可以位于会议中的对话框内以及整个会议生命周期的其他阶段。 有关会议中的对话框，请参阅 `bot Id` API 中的完成 `NotificationSignal` 参数。

* 会议详细信息 API 必须具有自动程序注册和自动程序 ID。 它需要 Bot SDK 才能获取 `TurnContext` 。

* 对于实时会议事件，你必须熟悉通过 `TurnContext` Bot SDK 提供的对象。 `Activity`中的 对象 `TurnContext` 包含具有实际开始时间和结束时间的有效负载。 实时会议事件需要来自会议平台的已注册Teams ID。

完成先决条件后，可以使用会议应用 API 引用、 和会议详细信息 API，以便使用属性访问信息并显示 `GetUserContext` `GetParticipant` `NotificationSignal` 相关内容。

## <a name="meeting-apps-api-references"></a>会议应用 API 参考

新的会议可扩展性为您提供了可转换会议体验的 API。 借助此新功能，可以在会议生命周期内生成应用或集成现有应用。 可以使用 API 让应用了解会议。 你可以选择想要用于增强会议体验的 API。

下表提供了这些 API 的列表：

|API|说明|请求|Source|
|---|---|----|---|
|**GetUserContext**| 此 API 使你能够获取上下文信息，以在"开始"选项卡中Teams内容。 |_**microsoftTeams.getContext ( ( ) => { /*...*/ } )**_|Microsoft Teams客户端 SDK|
|**GetParticipant**| 此 API 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。 |**GET** _**/v1/meetings/{meetingId}/participants/{participantId}？tenantId={tenantId}**_ |Microsoft Bot FrameworkSDK|
|**NotificationSignal** | 此 API 使你能够提供使用用户-机器人聊天的现有对话通知 API 传递的会议信号。 它允许您根据显示会议内对话框的用户操作发出信号。 |**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot FrameworkSDK|
|**会议详细信息** | 此 API 使你能够获取静态会议元数据。 |**GET** _**/v1/meetings/{meetingId}**_| Bot SDK |

### <a name="getusercontext-api"></a>GetUserContext API

若要标识和检索选项卡内容的上下文信息，请参阅获取选项卡Teams[上下文](../tabs/how-to/access-teams-context.md#get-context-by-using-the-microsoft-teams-javascript-library)。`meetingId`在会议上下文中运行时选项卡使用，并添加响应有效负载。

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * 不要缓存参与者角色，因为会议组织者可以随时更改角色。
> * Teams API 当前不支持超过 350 个参与者的大型通讯组列表或名单 `GetParticipant` 大小。

API `GetParticipant` 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。 API 包括查询参数、示例和响应代码。

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
| **403** | 不允许应用获取参与者信息。 这是最常见的错误响应，如果会议未安装应用，将触发此错误响应。 例如，如果租户管理员禁用应用或在实时网站迁移期间阻止应用。|
| **200** | 成功检索参与者信息。|
| **401** | 应用使用无效令牌进行响应。|
| **404** | 会议已过期或找不到参与者。|

### <a name="notificationsignal-api"></a>NotificationSignal API

会议中的所有用户都接收通过 API 发送 `NotificationSignal` 的通知。

> [!NOTE]
> * 调用会议内对话框时，内容将显示为聊天消息。
> * 目前，不支持发送定向通知。

`NotificationSignal` API 使你能够提供使用用户-机器人聊天的现有对话通知 API 传递的会议信号。 此 API 允许你根据显示会议内对话框的用户操作发出信号。 API 包括查询参数、示例和响应代码。

#### <a name="query-parameter"></a>查询参数

`NotificationSignal`API 包括以下查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**conversationId**| 字符串 | 是 | 对话标识符作为 Bot Invoke 的一部分提供。 |

#### <a name="examples"></a>示例

`Bot ID`在清单中声明 ，机器人将接收结果对象。

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

#### <a name="response-codes"></a>响应代码

`NotificationSignal`API 包括以下响应代码：

|响应代码|说明|
|---|---|
| **201** | 具有信号的活动已成功发送。 |
| **401** | 应用使用无效令牌进行响应。 |
| **403** | 应用无法发送信号。 发生这种情况的原因有多种，例如租户管理员禁用应用、实时网站迁移期间阻止应用等。 在这种情况下，有效负载包含详细的错误消息。 |
| **404** | 会议聊天不存在。 |

### <a name="meeting-details-api"></a>会议详细信息 API

> [!NOTE]
> 此功能目前仅适用于公共 [开发人员预览](../resources/dev-preview/developer-preview-intro.md) 版。

会议详细信息 API 使你的应用能够获取静态会议元数据。 这些是不会动态更改的数据点。
API 通过 Bot Services 提供。

#### <a name="prerequisite"></a>先决条件

若要使用会议详细信息 API，必须获取 RSC 权限。 使用以下示例配置应用清单 `webApplicationInfo` 的属性：

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

会议详细信息 API 包括以下查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**meetingId**| 字符串 | 是 | 会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。 |

#### <a name="example"></a>示例

会议详细信息 API 包括以下示例：

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
var connectorClient = turnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage(HttpMethod.Get, new Uri(new Uri(connectorClient.BaseUri.OriginalString), $"v1/meetings/{meetingId}"));
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, CancellationToken.None).ConfigureAwait(false);
string content;
if (response.Content != null)
{
    content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
}
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

## <a name="real-time-teams-meeting-events"></a>实时Teams会议事件

> [!NOTE]
> 此功能目前仅适用于公共 [开发人员预览](../resources/dev-preview/developer-preview-intro.md) 版。

用户可以接收实时会议事件。 只要任何应用与会议关联，就会与机器人共享实际会议开始时间和会议结束时间。

会议的实际开始时间和结束时间与计划的开始时间和结束时间不同。 会议详细信息 API 提供计划的开始时间和结束时间，而事件提供实际的开始时间和结束时间。

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
        "Id":"meeting id", 
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

为了反初始化 json 有效负载，引入了一个模型对象，用于获取会议元数据。 会议元数据驻留在事件有效 `value` 负载中的 属性中。 将 `MeetingStartEndEventvalue` 创建模型对象，其成员变量对应于事件有效负载 `value` 中的 属性下的键。

以下代码演示如何从会议开始和结束事件捕获会议元数据，即 、 和 `MeetingType` `Title` `Id` `JoinUrl` `StartTime` `EndTime` ：

```csharp
protected override async Task OnEventActivityAsync(
ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
{
    // Event Name is either 'application/vnd.microsoft.meetingStart' or 'application/vnd.microsoft.meetingEnd'
    var meetingEventName = turnContext.Activity.Name;
    // Value contains meeting information (ex: meeting type, start time, etc).
    var meetingEventInfo = turnContext.Activity.Value as JObject; 
    var meetingEventInfoObject =
meetingEventInfo.ToObject<MeetingStartEndEventValue>();
    // Create a very simple adaptive card with meeting information
var attachmentCard = createMeetingStartOrEndEventAttachment(meetingEventName,
meetingEventInfoObject);
    await turnContext.SendActivityAsync(MessageFactory.Attachment(attachmentCard));
}
```

MeetingStartEndEventvalue.cs 包括以下代码：

```csharp
public class MeetingStartEndEventValue
{
    public string Id { get; set; }
    public string Title { get; set; }
    public string MeetingType { get; set; }
    public string JoinUrl { get; set; }
    public string StartTime { get; set; }
    public string EndTime { get; set; }
}
```

## <a name="code-sample"></a>代码示例

|示例名称 | 说明 | .NET | Node.js |
|----------------|-----------------|--------------|--------------|
| 会议可扩展性 | Microsoft Teams令牌的会议扩展性示例。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| 会议内容气泡机器人 | Microsoft Teams会议扩展性示例，用于与会议内容气泡机器人进行交互。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| Meeting meetingSidePanel | Microsoft Teams与会议中的侧面板交互的会议扩展性示例。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/nodejs)|
| 会议详细信息选项卡 | Microsoft Teams会议扩展性示例，以在会议中通过详细信息选项卡进行激活。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-details-tab/nodejs)|

## <a name="see-also"></a>另请参阅

* [会议内对话设计指南](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams选项卡的身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)
* [会议Teams应用程序](teams-apps-in-meetings.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [为会议启用和配置Teams应用程序](enable-and-configure-your-app-for-teams-meetings.md)
