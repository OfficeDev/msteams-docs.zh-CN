---
title: 创建适用于团队会议的应用
author: laujan
description: 创建团队会议应用
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: 84d0f5564d7e8e6e34dde1f3d59cc6e7a68d3332
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565912"
---
# <a name="create-apps-for-teams-meetings"></a>创建适用于 Teams 会议的应用

## <a name="prerequisites-and-considerations"></a>先决条件和注意事项

为会议创建Teams之前，必须了解以下内容：

* 你必须知道如何开发应用Teams知识。 有关详细信息，请参阅应用[Teams开发](../overview.md)。

* 必须更新Teams清单，以指示该应用可用于会议。 有关详细信息，请参阅 [应用清单](#update-your-app-manifest)。

* 若要使应用在会议生命周期中作为选项卡运行，它必须支持 groupchat 作用域中的可配置选项卡。 有关详细信息，请参阅 [groupchat scope](../resources/schema/manifest-schema.md#configurabletabs) and [build a group tab](../build-your-first-app/build-channel-tab.md)。

* 对于会议前和Teams方案，必须遵循常规选项卡设计准则。 有关会议期间的体验，请参阅会议内选项卡和会议内对话框设计指南。 有关详细信息，请参阅Teams[选项卡设计指南](../tabs/design/tabs.md)、会议中的[选项卡](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)设计指南和[会议中的对话框设计指南](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

* 必须支持范围才能在会议前和会议后聊天 `groupchat` 中启用应用。 通过会议前应用体验，你可以查找和添加会议应用并执行会议前任务。 通过会议后应用体验，可以查看会议结果，如投票调查结果或反馈。

* 会议 API URL 参数必须具有 `meetingId` 、 `userId` 和 `tenantId` 。 它们作为客户端 SDK 和自动程序Teams的一部分提供。 此外，可以使用 Tab SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。

* `GetParticipant`API 必须具有自动程序注册和 ID，以生成身份验证令牌。 有关详细信息，请参阅自动[程序注册和 ID。](../build-your-first-app/build-bot.md)

* 若要实时更新应用，应用必须基于会议中的活动活动是最新的。 这些事件可以位于会议中的对话框内以及整个会议生命周期的其他阶段。 有关会议中的对话框，请参阅 中的 `bot Id` 完成参数 `Notification Signal API` 。

## <a name="meeting-apps-api-reference"></a>会议应用 API 参考

|API|描述|请求|源|
|---|---|----|---|
|**GetUserContext**| 此 API 使你能够获取上下文信息，以在"开始"选项卡中Teams内容。 |_**microsoftTeams.getContext ( ( ) => { /*...*/ } )**_|Microsoft Teams客户端 SDK|
|**GetParticipant**| 此 API 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。 |**GET** _**/v1/meetings/{meetingId}/participants/{participantId}？tenantId={tenantId}**_ |Microsoft Bot FrameworkSDK|
|**NotificationSignal** | 此 API 使你能够提供使用用户-机器人聊天的现有对话通知 API 传递的会议信号。 它允许您根据显示会议内对话框的用户操作发出信号。 |**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot FrameworkSDK|

### <a name="getusercontext"></a>GetUserContext

若要标识和检索选项卡内容的上下文信息，请参阅获取选项卡Teams[上下文](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library)。`meetingId`在会议上下文中运行时选项卡使用，并添加响应有效负载。

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
> * 不要缓存参与者角色，因为会议组织者可以随时更改角色。
> * Teams API 当前不支持超过 350 个参与者的大型通讯组列表或名单 `GetParticipant` 大小。

#### <a name="query-parameters"></a>查询参数

|值|类型|必需|说明|
|---|---|----|---|
|**meetingId**| string | 是 | 会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。|
|**participantId**| string | 是 | 参与者 ID 是用户 ID。 它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。 建议从选项卡 SSO 获取参与者 ID。 |
|**tenantId**| string | 是 | 租户用户需要租户 ID。 它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。 建议从选项卡 SSO 获取租户 ID。 |

#### <a name="example"></a>示例

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
protected override async Task OnMessageActivityAsync(ITurnContext<IMessageActivity> turnContext, CancellationToken cancellationToken)
{
  TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
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

* * *

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

|响应代码|描述|
|---|---|
| **403** | 不允许应用获取参与者信息。 这是最常见的错误响应，如果会议未安装应用，将触发此错误响应。 例如，如果租户管理员禁用应用或在实时网站迁移期间阻止应用。|
| **200** | 成功检索参与者信息。|
| **401** | 应用使用无效令牌进行响应。|
| **404** | 会议已过期或找不到参与者。|
| **500** | 会议自会议结束以来的 60 天以上已过期，或者参与者没有基于其角色的权限。|

### <a name="notificationsignal-api"></a>NotificationSignal API

会议中的所有用户都接收通过 API 发送 `NotificationSignal` 的通知。

> [!NOTE]
> * 调用会议内对话框时，内容将显示为聊天消息。
> * 目前，不支持发送定向通知。

#### <a name="query-parameters"></a>查询参数

|值|类型|必需|说明|
|---|---|----|---|
|**conversationId**| string | 是 | 对话标识符作为自动程序调用的一部分提供。 |

#### <a name="example"></a>示例

`Bot ID`在清单中声明 ，机器人将接收结果对象。

> [!NOTE]
> * `completionBotId`在请求 `externalResourceUrl` 的有效负载示例中，的 参数是可选的。 `Bot ID` 在清单中声明，机器人将接收结果对象。
> * `externalResourceUrl`宽度和高度参数必须以像素为单位。 若要确保尺寸在允许的限制内，请参阅 [设计指南](design/designing-apps-in-meetings.md)。
> * URL 是在会议对话框中作为 `<iframe>` 加载的页面。 域必须在你的应用清单 `validDomains` 的应用数组中。

# <a name="c"></a>[C#](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");

activity.ChannelData = new TeamsChannelData
  {
    Notification = new NotificationInfo()
                    {
                        AlertInMeeting = true,
                        ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
                    }
  };
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

* * *

#### <a name="response-codes"></a>响应代码

|响应代码|描述|
|---|---|
| **201** | 具有信号的活动已成功发送。 |
| **401** | 应用使用无效令牌进行响应。 |
| **403** | 应用无法发送信号。 发生这种情况的原因有多种，例如租户管理员禁用应用、实时网站迁移期间阻止应用等。 在这种情况下，有效负载包含详细的错误消息。 |
| **404** | 会议聊天不存在。 |

## <a name="enable-your-app-for-teams-meetings"></a>为应用启用Teams会议

### <a name="update-your-app-manifest"></a>更新应用清单

会议应用功能使用 、 和 数组在应用清单 `configurableTabs` `scopes` `context` 中声明。 范围定义谁，上下文定义你的应用的可用位置。

> [!NOTE]
> 尝试使用清单架构更新 [应用清单](../resources/schema/manifest-schema-dev-preview.md)。
> 会议中的应用程序需要 *群聊* 范围。 团队 *作用域* 仅适用于频道中的选项卡。

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "team",
        "groupchat"
      ],
      "context":[
        "channelTab",
        "privateChatTab",
        "meetingChatTab",
        "meetingDetailsTab",
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```
> [!NOTE]
> `meetingStage` 当前仅适用于开发人员预览版。

### <a name="context-property"></a>Context 属性

选项卡 `context` 和 `scopes` 属性使你可以确定应用必须出现在何处。 或 作用域 `team` `groupchat` 中的选项卡可以具有多个上下文。 以下是可以使用所有或部分 `context` 值的 属性的值：

|值|说明|
|---|---|
| **channelTab** | 团队频道标题中的选项卡。 |
| **privateChatTab** | 一组不在团队或会议上下文中的用户之间的群聊标题中的选项卡。 |
| **meetingChatTab** | 计划会议上下文中的一组用户之间的群聊标题中的选项卡。 |
| **meetingDetailsTab** | 日历的会议详细信息视图标题中的选项卡。 |
| **meetingSidePanel** | 通过统一栏和 U 条形图 (打开的会议内) 。 |
| **meetingStage** | 可以将来自侧窗格的应用共享到会议阶段。 |

> [!NOTE]
> `Context` 属性当前在移动客户端上不受支持。

## <a name="configure-your-app-for-meeting-scenarios"></a>为会议方案配置应用

> [!NOTE]
> * 若要使应用在选项卡库中可见，它必须支持可配置的选项卡和群聊范围。
> * 移动客户端仅在会议前和会议后阶段支持选项卡。
> * 移动客户端当前不支持会议内对话框和选项卡中的会议体验。 有关详细信息，请参阅 [为移动设备创建选项卡](../tabs/design/tabs-mobile.md) 时移动选项卡指南。

### <a name="before-a-meeting"></a>会议前

在会议之前，用户可以向会议添加选项卡、聊天机器人和消息传递扩展。 具有组织者和演示者角色的用户可以向会议添加选项卡。

**向会议添加选项卡**

1. 在日历中，选择要添加选项卡的会议。
1. 选择详细信息 **选项卡** 并选择加号 <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. 将显示选项卡库。

    ![会议前体验](../assets/images/apps-in-meetings/PreMeeting.png)

1. 在选项卡库中，选择要添加的应用并按照所需步骤操作。 应用作为选项卡安装。
    > [!NOTE] 
    > 目前，在"会议"选项卡中，不支持获取会议详细信息和参与者信息。

**将消息传递扩展添加到会议**

1. 选择位于聊天的撰写 &#x25CF;&#x25CF;&#x25CF; 消息区域中的省略号或溢出菜单。
1. 选择要添加的应用并按照所需步骤操作。 应用作为消息传递扩展进行安装。

**将机器人添加到会议**

在会议聊天中， **@** 输入密钥并选择"**获取机器人"。**

> [!NOTE]
> * 必须使用选项卡 SSO 确认 [用户标识](../tabs/how-to/authentication/auth-aad-sso.md)。 身份验证后，应用可以使用 API 检索用户 `GetParticipant` 角色。
> * 根据用户角色，应用能够提供特定于角色的体验。 例如，轮询应用仅允许组织者和演示者创建新的轮询。
> * 可以在会议进行时更改角色分配。 有关详细信息，请参阅[会议Teams角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

### <a name="during-a-meeting"></a>会议期间

#### <a name="sidepanel"></a>sidePanel

借助 sidePanel，你可以自定义会议体验，使组织者和演示者拥有一组不同的视图和操作。 在应用清单中，必须将 sidePanel 添加到上下文数组。 在会议以及所有方案中，应用在宽度为 320 像素的"会议内"选项卡中呈现。 有关详细信息，请参阅 [FrameContext 接口](/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)。

若要使用 `userContext` API 相应地路由请求，请参阅[Teams SDK。](../tabs/how-to/access-teams-context.md#user-context) 请参阅[Teams的身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。 选项卡的身份验证流与网站的身份验证流非常相似。 因此选项卡可以直接使用 OAuth 2.0。 请参阅Microsoft 标识平台[OAuth 2.0 授权代码流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

当用户在会议视图中并且用户可以发布撰写邮件扩展卡时，邮件扩展将按预期方式工作。 AppName 会议内是一个工具提示，用于指出会议 U 栏中的应用名称。

> [!NOTE]
> 使用版本 1.7.0 或更高版本[的 Teams SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)因为它之前的版本不支持侧面板。

#### <a name="in-meeting-dialog"></a>会议内的对话框

会议内对话框可用于在会议期间与参与者互动，并收集会议期间的信息或反馈。 使用 [`NotificationSignal`](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API 指示必须触发气泡通知。 作为通知请求有效负载的一部分，请包含要显示内容的托管 URL。

会议内对话框不得使用任务模块。 会议聊天中不会调用任务模块。 外部资源 URL 用于在会议中显示内容气泡。 可以使用 方法 `submitTask` 在会议聊天中提交数据。

> [!NOTE]
> * 你必须调用 [submitTask () ](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 函数，以在用户执行 Web 视图中的操作后自动消除。 这是应用提交的要求。 有关详细信息，请参阅Teams [SDK 任务模块](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。
> * 如果希望你的应用支持匿名用户，则初始调用请求有效负载必须依赖于 对象中的请求元数据， `from.id` `from` 而不是 `from.aadObjectId` 请求元数据。 `from.id`是用户 `from.aadObjectId` ID，也是Azure Active Directory (AAD) ID。 有关详细信息，请参阅在 [选项卡中使用任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md) 以及 [创建和发送任务模块](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。

#### <a name="share-to-stage"></a>共享到阶段 

> [!NOTE]
> * 此功能目前仅适用于开发人员预览版。
> * 若要使用此功能，应用必须支持会议内侧窗格。


此功能使开发人员能够将应用共享到会议阶段。 通过启用共享到会议阶段，会议参与者可以实时协作。 

必需的上下文 `meetingStage` 位于应用程序清单中。 这样做的先决条件是拥有 `meetingSidePanel` 上下文。 这将启用 **侧窗格** 的"共享"按钮，如下图所示：

  ![share_to_stage_during_meeting体验](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

启用此功能所需的清单更改如下所示： 

```json

"configurableTabs": [
    {
      "configurationUrl": "https://contoso.com/teamstab/configure",
      "canUpdateConfiguration": true,
      "scopes": [
        "groupchat"
      ],
      "context":[
        
        "meetingSidePanel",
        "meetingStage"
     ]
    }
  ]
```



### <a name="after-a-meeting"></a>会议后

会议后和会议前配置是等效的。

## <a name="code-sample"></a>代码示例

|示例名称 | 描述 | .NET | Node.js |
|----------------|-----------------|--------------|--------------|
| 会议可扩展性 | Microsoft Teams令牌的会议扩展性示例。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| 会议内容气泡机器人 | Microsoft Teams会议扩展性示例，用于与会议内容气泡机器人进行交互。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs)|
| Meeting SidePanel | Microsoft Teams会议扩展性示例，以在会议中通过侧面板进行激活。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |

## <a name="see-also"></a>另请参阅

* [会议内对话设计指南](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams选项卡的身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)
