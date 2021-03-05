---
title: 创建适用于团队会议的应用
author: laujan
description: 为团队会议创建应用
ms.topic: conceptual
ms.author: lajanuar
keywords: Teams 应用会议用户参与者角色 api
ms.openlocfilehash: bd0f53ae34a23bdbbdc2e6f3992c7dd0836e9f28
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449491"
---
# <a name="create-apps-for-teams-meetings"></a>创建适用于 Teams 会议的应用

## <a name="prerequisites-and-considerations"></a>先决条件和注意事项

* 会议中的应用需要 Teams 应用开发 [方面的一些基本知识](../overview.md)。 会议中的应用可以包括[选项卡](../tabs/what-are-tabs.md)、聊天机器人和消息传递[](../bots/what-are-bots.md)扩展功能，并且[](../messaging-extensions/what-are-messaging-extensions.md)需要[Teams](#update-your-app-manifest)应用清单更新，以指示该应用可用于会议

* 若要使应用在会议生命周期中作为选项卡运行，它必须支持组聊天范围中的可配置[选项卡 (了解如何](../resources/schema/manifest-schema.md#configurabletabs)生成组选项卡) 。 [](../build-your-first-app/build-channel-tab.md) 支持范围 `groupchat` 将启用会议前 [和](teams-apps-in-meetings.md#pre-meeting-app-experience) 会议 [后聊天中的](teams-apps-in-meetings.md#post-meeting-app-experience) 应用。

* 会议 API URL 参数可能需要 `meetingId` 和 `userId` [tenantId，](/onedrive/find-your-office-365-tenant-id) 这些参数作为 Teams 客户端 SDK 和自动程序活动的一部分提供。 此外，可以使用 Tab SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。

* 某些会议 API（例如 `GetParticipant` ，需要自动 [程序注册和 ID）](../build-your-first-app/build-bot.md) 才能生成身份验证令牌。

* 您必须遵守针对会议前 [和会议后](../tabs/design/tabs.md) 方案的 Teams 选项卡设计一般准则。 有关会议期间的体验，请参阅会议内 [选项卡](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) 和 [会议内对话框](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) 设计指南。

* 若要实时更新应用，应用必须基于会议中的事件活动是最新的。 这些事件可以位于会议对话框内， (在会议生命周期中的) 和其他图面中引用 `bot Id` `Notification Signal API` 完成参数

## <a name="meeting-apps-api-reference"></a>会议应用 API 参考

|API|说明|请求|源|
|---|---|----|---|
|**GetUserContext**| 获取上下文信息以在 Teams 选项卡中显示相关内容。 |_**microsoftTeams.getContext ( ( ) => { /*...*/ } )**_|Microsoft Teams 客户端 SDK|
|**GetParticipant**|此 API 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。|**GET** _**/v1/meetings/{meetingId}/participants/{participantId}？tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** |会议信号将采用以下现有对话通知 API (用于用户聊天聊天) 。 此 API 允许开发人员根据最终用户操作发出信号，以显示会议内对话气泡。|**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|

### <a name="getusercontext"></a>GetUserContext

请参阅 Teams 选项卡 [文档的"](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) 获取上下文"，获取有关标识和检索选项卡内容的上下文信息的指南。 作为会议可扩展性的一部分，为响应有效负载添加了一个新值：

✔ **meetingId**： 在会议上下文中运行时由选项卡使用。

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
>
> * 不要缓存参与者角色，因为会议组织者可以随时更改角色。
>
> * Teams 当前不支持 API 参与者超过 350 人的大型通讯组列表或名单 `GetParticipant` 。

#### <a name="query-parameters"></a>查询参数

|值|类型|必需|说明|
|---|---|----|---|
|**meetingId**| string | 是 | 会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。|
|**participantId**| string | 是 | participantId 是用户 ID。 它在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中可用。 强烈建议从 Tab SSO 获取 participantId。 |
|**tenantId**| string | 是 | 租户用户需要 tenantId。 它在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中可用。 强烈建议从 Tab SSO 获取 tenantId。 |

#### <a name="example"></a>示例

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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
            TeamsMeetingParticipant participant = GetMeetingParticipantAsync(turnContext, "yourMeetingId", "yourParticipantId", "yourTenantId");
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

响应正文为：

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

* * *

#### <a name="response-codes"></a>响应代码

* **403：** 不允许应用获取参与者信息。 这是最常见的错误响应，如果未在会议中安装应用，将触发此错误响应。 例如，如果租户管理员禁用应用或在网站缓解期间阻止应用。
* **200：** 已成功检索参与者信息。
* **401：** 令牌无效。
* **404：** 找不到参与者。
* **500：** 会议自 (结束以来超过 60 天) 或者参与者没有基于其角色的权限。


**即将推出**

* **404：** 会议已过期或找不到参与者。


### <a name="notificationsignal-api"></a>NotificationSignal API

会议中的所有用户都接收通过 NotificationSignal API 发送的通知。

> [!NOTE]
> 目前，不支持发送定向通知。
> 调用会议内对话框时，相同的内容还将呈现为聊天消息。

#### <a name="query-parameters"></a>查询参数

|值|类型|必需|说明|
|---|---|----|---|
|**conversationId**| string | 是 | 对话标识符作为自动程序调用的一部分提供 |

#### <a name="example"></a>示例

在 `Bot ID` 清单中声明，自动程序接收结果对象。 在下面的示例中，所请求的有效负载中的参数 `completionBotId` `externalResourceUrl` 是可选的：

> [!NOTE]
> * `externalResourceUrl`宽度和高度参数必须以像素为单位。 若要确保尺寸在允许的限制内，请参阅 [设计指南](design/designing-apps-in-meetings.md)。
> * URL 是在会议对话框中作为 `<iframe>` 页面加载的页面。 域必须在你的应用清单 `validDomains` 中的应用数组中。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

* **201：** 已成功发送具有信号的活动。 
* **401：** 令牌无效。
* **403：** 应用无法发送信号。 由于各种原因（如租户管理员禁用应用、应用在实时网站迁移期间被阻止等）可能会发生这种情况。 在这种情况下，有效负载包含详细的错误消息。 
* **404：** 会议聊天不存在。
 

## <a name="enable-your-app-for-teams-meetings"></a>为 Teams 会议启用应用

### <a name="update-your-app-manifest"></a>更新应用清单

会议应用功能通过 **configurableTabs** 作用域和上下文数组在应用清单  ->  **中** 声明。 *范围* 定义谁， *上下文* 定义你的应用的可用位置。

> [!NOTE]
> 请使用 [开发者预览版清单架构](../resources/schema/manifest-schema-dev-preview.md) 在应用清单中尝试此操作。

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
        "meetingSidePanel"
     ]
    }
  ]
```

### <a name="context-property"></a>Context 属性

选项卡 `context` 和 `scopes` 属性协调工作，允许你确定希望应用显示在何处。 或作用域 `team` 中的 `groupchat` 选项卡可以具有多个上下文。 上下文属性的可能值如下所示：

* **channelTab**：团队频道标题中的选项卡。
* **privateChatTab**：不在团队或会议上下文中的一组用户之间的群聊标题中的选项卡。
* **meetingChatTab**：计划会议上下文中一组用户之间的群聊标题中的选项卡。
* **meetingDetailsTab：** 日历的会议详细信息视图标题中的选项卡。
* **meetingSidePanel：** 通过统一栏打开的 (u 栏) 。

> [!NOTE]
> "Context"属性当前不受支持，因此将在移动客户端上被忽略

## <a name="configure-your-app-for-meeting-scenarios"></a>为会议方案配置应用

> [!NOTE]
> * 若要使应用在选项卡库中可见，需要支持可 **配置的选项卡** 和 **群聊范围**。
>
> * 移动客户端仅支持会议前和会议后 Surface 中的选项卡。 即将在移动设备上 (会议内对话框和选项卡) 体验。 在创建 [适用于移动设备的选项卡时](../tabs/design/tabs-mobile.md) ，请遵循移动选项卡指南。

### <a name="before-a-meeting"></a>在会议之前

具有组织者和/或演示者角色的用户使用会议聊天和会议详细信息➕中的加号 **按钮将选项卡****添加到会议。** 消息扩展通过位于聊天中的撰写消息 &#x25CF;&#x25CF;&#x25CF; 下的省略号/溢出菜单添加到。 使用""键并选择"获取机器人"将聊天机器人添加到 **@** **会议聊天** 中。

✔必须通过选项卡 SSO确认[用户标识](../tabs/how-to/authentication/auth-aad-sso.md)。 在此身份验证后，应用可以通过 GetParticipant API 检索用户角色。

 ✔基于用户角色，应用现在能够呈现角色特定体验。 例如，轮询应用只允许组织者和演示者创建新轮询。

> **注意**：可以在会议进行时更改角色分配。  *请参阅* [Teams 会议的角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。 

### <a name="during-a-meeting"></a>会议期间

#### <a name="sidepanel"></a>**sidePanel**

✔在应用清单中向上下文数组添加 **sidePanel，** 如上所述。 

✔会议以及所有方案中，应用程序将在宽度为 320px 的会议内选项卡中呈现。 您的选项卡必须针对这一点进行优化。 *请参阅* [，FrameContext 接口](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)

✔ Teams [SDK，](../tabs/how-to/access-teams-context.md#user-context) 以使用 **userContext** API 相应地路由请求。

✔选项卡 [的 Teams 身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。 选项卡的身份验证流与网站的身份验证流非常相似。 因此，选项卡可以直接使用 OAuth 2.0。 *另请参阅* [，Microsoft 标识平台和 OAuth 2.0 授权代码流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

✔用户位于会议视图中时，邮件扩展应按预期工作，并且应该能够发布撰写邮件扩展卡。

✔ AppName- 工具提示应指出会议 U 栏中的应用名称。

#### <a name="in-meeting-dialog"></a>**会议内的对话框**

✔必须遵守会议 [对话设计准则](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

✔选项卡 [的 Teams 身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。

✔ [使用 NotificationSignal API](create-apps-for-teams-meetings.md#notificationsignal-api) 发出需要触发气泡通知的信号。

✔作为通知请求有效负载的一部分，包括要展示内容的托管 URL。

✔会议对话不得使用任务模块。

> [!NOTE]
>
> * 这些通知本质上是永久性的。 您必须调用 [**submitTask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 函数，以在用户执行 Web 视图中的操作后自动消除。 这是应用提交的要求。 *另请参阅* [，Teams SDK：任务模块](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。
>
> * 如果希望应用支持匿名用户，初始调用请求有效负载必须依赖于用户) 请求元数据的 () ID，而不是用户请求元数据的 `from.id` `from` (Azure Active `from.aadObjectId` Directory) ID。 *请参阅*[使用选项卡中的任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md)[以及创建和发送任务模块](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。

### <a name="after-a-meeting"></a>会议后

会议后和会前配置是等效的。

## <a name="meeting-app-sample"></a>会议应用示例

 > [!div class="nextstepaction"]
> [会议令牌生成器应用](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
