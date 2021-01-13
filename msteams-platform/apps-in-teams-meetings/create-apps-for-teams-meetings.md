---
title: 创建适用于团队会议的应用
author: laujan
description: 为团队会议创建应用
ms.topic: conceptual
ms.author: lajanuar
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: 82327eca86dcdac5c47f5f4471bc91d55484d07e
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797762"
---
# <a name="create-apps-for-teams-meetings"></a>创建适用于 Teams 会议的应用

## <a name="prerequisites-and-considerations"></a>先决条件和注意事项

* 会议中的应用需要一些 Teams [应用开发的基本知识](../overview.md)。 会议中的应用可以包括[选项卡](../tabs/what-are-tabs.md)、聊天机器人和消息传递[](../bots/what-are-bots.md)扩展功能，并且[](../messaging-extensions/what-are-messaging-extensions.md)[需要更新](#update-your-app-manifest)Teams 应用清单以指示该应用可用于会议

* 若要使应用在会议生命周期中作为选项卡运行，它必须支持群聊范围中的可配置选项卡 ([](../resources/schema/manifest-schema.md#configurabletabs)了解如何生成组选项卡) 。 [](../build-your-first-app/build-channel-tab.md) 支持范围 `groupchat` 将启用会议前 [和](teams-apps-in-meetings.md#pre-meeting-app-experience) 会议 [后聊天中的](teams-apps-in-meetings.md#post-meeting-app-experience) 应用。

* 会议 API URL 参数可能需要 ，并且 tenantId These 作为 Teams 客户端 SDK 和聊天机器人活动的一 `meetingId` `userId` 部分提供。 [](/onedrive/find-your-office-365-tenant-id) 此外，可以使用 Tab SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。

* 某些会议 API（例如 `GetParticipant` ，需要自动 [程序注册和 ID）](../build-your-first-app/build-bot.md) 才能生成身份验证令牌。

* 对于会议前和会议[](../tabs/design/tabs.md)后方案，必须遵守 Teams 选项卡设计一般准则。 有关会议期间的体验，请参阅 [会议内选项卡](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) 和 [会议内对话框](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog) 设计指南。

* 若要实时更新应用，应用必须基于会议中的事件活动是最新的。 这些事件可以位于会议内对话框内， (整个会议) 和其他图面中的 `bot Id` `Notification Signal API` 完成参数

## <a name="meeting-apps-api-reference"></a>会议应用 API 参考

|API|说明|请求|Source|
|---|---|----|---|
|**GetUserContext**| 获取上下文信息以在 Teams 选项卡中显示相关内容。 |_**microsoftTeams.getContext ( ( ) => { /*...*/ } )**_|Microsoft Teams 客户端 SDK|
|**GetParticipant**|此 API 允许机器人通过会议 ID 和参与者 ID 获取参与者信息。|**GET** _**/v1/meetings/{meetingId}/participants/{participantId}？tenantId={tenantId}**_ |Microsoft Bot Framework SDK|
|**NotificationSignal** |会议信号将采用以下现有对话通知 API (用于用户聊天聊天) 。 此 API 允许开发人员根据最终用户操作发出信号，以显示会议内对话气泡。|**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot Framework SDK|

### <a name="getusercontext"></a>GetUserContext

请参阅 Teams 选项卡 [文档的"](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) 获取上下文"，获取有关标识和检索选项卡内容的上下文信息的指南。 作为会议扩展的一部分，为响应有效负载添加了一个新值：

✔ **meetingId**： 在会议上下文中运行时由选项卡使用。

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
>
> * 不要缓存参与者角色，因为会议组织者可以在任何时间点更改角色。
>
> * Teams 当前不支持 API 参与者超过 350 人的大型通讯组列表或名单 `GetParticipant` 大小。

#### <a name="query-parameters"></a>查询参数

|值|类型|必需|说明|
|---|---|----|---|
|**meetingId**| string | 是 | 会议标识符通过 Bot Invoke 和 Teams 客户端 SDK 提供。|
|**participantId**| string | 是 | participantId 是用户 ID。 它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。 强烈建议从 Tab SSO 获取 participantId。 |
|**tenantId**| string | 是 | 租户用户需要 tenantId。 它可在 Tab SSO、Bot Invoke 和 Teams 客户端 SDK 中提供。 强烈建议从 Tab SSO 获取 tenantId。 |

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
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
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

* **403：** 不允许应用获取参与者信息。  这是最常见的错误响应，如果未在会议中安装应用，将触发此错误响应。 例如，如果租户管理员禁用应用或在实时网站迁移过程中阻止应用。
* **200：** 已成功检索参与者信息。
* **401：** 令牌无效。
* **404：** 找不到参与者。
* **500：** 会议 (自会议结束以来超过 60 天) 或者参与者没有基于其角色的权限。


**即将推出**

* **404：** 会议已过期或找不到参与者。


### <a name="notificationsignal-api"></a>NotificationSignal API

> [!NOTE]
> 调用会议内对话框时，相同的内容还将呈现为聊天消息。

#### <a name="query-parameters"></a>查询参数

|值|类型|必需|说明|
|---|---|----|---|
|**conversationId**| string | 是 | 对话标识符作为自动程序调用的一部分提供 |

#### <a name="example"></a>示例

> [!NOTE]
>
在 `completionBotId` 请求 `externalResourceUrl` 的有效负载示例中，参数是可选的。 `Bot ID` 在清单中声明，机器人会收到结果对象。
> * externalResourceUrl 宽度和高度参数必须以像素为单位。 请参阅 [设计指南](design/designing-apps-in-meetings.md) 以确保尺寸在允许的限制范围内。
> * URL 是作为会议内 `<iframe>` 对话框中的一个页面加载的页面。 域必须在你的应用清单 `validDomains` 中的应用数组中。

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

* **201**： 具有信号的活动已成功发送  
* **401**： 令牌无效  
* **201：** 已成功发送具有信号的活动。 
* **401：** 令牌无效。
* **403：** 应用无法发送信号。 发生这种情况的原因有多种，如租户管理员禁用应用、实时网站迁移期间阻止应用等。 在这种情况下，有效负载包含详细的错误消息。 
* **404：** 会议聊天不存在。
 

## <a name="enable-your-app-for-teams-meetings"></a>为 Teams 会议启用应用

### <a name="update-your-app-manifest"></a>更新应用清单

会议应用功能通过 **configurableTabs** 作用域和上下文数组在应用清单  ->  **中** 声明。 *范围* 定义谁 *，上下文* 定义你的应用的可用位置。

> [!NOTE]
> 请使用开发者预览版 [清单架构](../resources/schema/manifest-schema-dev-preview.md) 在应用清单中尝试此操作。

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

选项卡 `context` 和 `scopes` 属性协调工作，以允许你确定希望应用显示在何处。 或作用域 `team` 中的 `groupchat` 选项卡可以具有多个上下文。 上下文属性的可能值如下所示：

* **channelTab**：团队频道标题中的选项卡。
* **privateChatTab**：一组不在团队或会议上下文中的用户之间的群聊标题中的选项卡。
* **meetingChatTab**：计划会议上下文中一组用户之间的群聊标题中的选项卡。
* **meetingDetailsTab**：日历的会议详细信息视图标题中的选项卡。
* **meetingSidePanel**：通过统一栏打开的 (u-bar) 。

> [!NOTE]
> "Context"属性当前不受支持，因此将在移动客户端上被忽略

## <a name="configure-your-app-for-meeting-scenarios"></a>为会议方案配置应用

> [!NOTE]
> * 若要使应用在选项卡库中可见，它需要支持可配置的 **选项卡** 和 **群聊范围**。
>
> * 移动客户端仅在会议前和会议后支持选项卡。 即将在移动设备上 (会议内对话框和选项卡) 体验。 在创建 [适用于移动的选项卡时](../tabs/design/tabs-mobile.md) ，请遵循移动选项卡指南。

### <a name="before-a-meeting"></a>会议之前

具有组织者和/或演示者角色的用户使用会议聊天和会议详细信息页面中的 ➕ **按钮将选项卡** 添加到 **会议** 。 消息扩展通过省略号/溢出菜单添加到 &#x25CF;&#x25CF;&#x25CF; 位于聊天的撰写消息区域下。 聊天机器人会使用""键并选择"获取机器人"添加到 **@** **会议聊天中**。

✔用户标识 *必须通过* 选项卡 [SSO 确认](../tabs/how-to/authentication/auth-aad-sso.md)。 在此身份验证后，应用可以通过 GetParticipant API 检索用户角色。

 ✔基于用户角色，应用现在能够呈现特定于角色的体验。 例如，轮询应用只允许组织者和演示者创建新轮询。

> **注意**：可以在会议进行时更改角色分配。  *请参阅* [Teams 会议的角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。 

### <a name="during-a-meeting"></a>会议期间

#### <a name="sidepanel"></a>**sidePanel**

✔在应用清单中向上下文数组添加 **sidePanel，** 如上所述。 

✔在会议以及所有方案中，应用程序将在宽度为 320px 的"会议内"选项卡中呈现。 必须针对这一点对选项卡进行优化。 *请参阅* [，FrameContext 接口](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)

✔ Teams [SDK，](../tabs/how-to/access-teams-context.md#user-context) 以使用 **userContext** API 相应地路由请求。

✔请参阅 [选项卡的 Teams 身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。 选项卡的身份验证流与网站的身份验证流非常相似。 因此，选项卡可以直接使用 OAuth 2.0。 *另请参阅* [，Microsoft 标识平台和 OAuth 2.0 授权代码流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

✔用户位于会议视图中时，邮件扩展应按预期工作，并且应该能够发布撰写邮件扩展卡。

✔ AppName 会议 - 工具提示应说明会议中的 U 栏的应用名称。

#### <a name="in-meeting-dialog"></a>**会议内的对话框**

✔必须遵守会议 [内对话框设计准则](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

✔请参阅 [选项卡的 Teams 身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。

✔ 使用 [通知](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API 发出需要触发气泡通知的信号。

✔作为通知请求有效负载的一部分，请包含要展示内容的托管 URL。

✔会议内对话框不得使用任务模块。

> [!NOTE]
>
> * 这些通知本质上是永久性的。 您必须调用 [**submitTask ()**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 函数，以在用户执行 Web 视图中的操作后自动消除。 这是应用提交的要求。 *另请参阅* [，Teams SDK：任务模块](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。
>
> * 如果希望应用支持匿名用户，初始调用请求有效负载必须依赖于对象中的用户) 请求元数据的 (ID，而不是用户请求元数据的 `from.id` `from` (Azure Active `from.aadObjectId` Directory) ID。 *请参阅*[使用选项卡中的任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md)[以及创建和发送任务模块](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。

### <a name="after-a-meeting"></a>会议后

会后和会前配置是等效的。

## <a name="meeting-app-sample"></a>会议应用程序示例

 > [!div class="nextstepaction"]
> [会议令牌生成器应用](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
