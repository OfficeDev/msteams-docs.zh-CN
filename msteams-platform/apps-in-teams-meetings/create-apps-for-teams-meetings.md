---
title: 创建适用于团队会议的应用
author: laujan
description: 创建团队会议的应用程序
ms.topic: conceptual
ms.author: lajanuar
keywords: 团队应用会议用户参与者角色 api
ms.openlocfilehash: f448885e3664209858eb90fa9f0853c3d31e015a
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409111"
---
# <a name="create-apps-for-teams-meetings"></a>创建适用于 Teams 会议的应用

## <a name="prerequisites-and-considerations"></a>先决条件和注意事项

1. 会议中的应用程序需要一些有关 [团队应用程序开发](../overview.md)的基本知识。 会议中的应用程序可以包含 [选项卡](../tabs/what-are-tabs.md)、 [bot](../bots/what-are-bots.md)和 [邮件扩展](../messaging-extensions/what-are-messaging-extensions.md) 功能，并将要求对团队 [应用程序清单](#update-your-app-manifest) 进行更新以指示该应用程序可用于会议

1. 为了使您的应用程序在会议生命周期中作为选项卡运行，它必须支持 [groupchat 范围](../resources/schema/manifest-schema.md#configurabletabs)中可配置的选项卡。 *请参阅*[使用自定义选项卡扩展团队应用](../tabs/how-to/add-tab.md)。如果支持此 `groupchat` 范围，您的应用程序将在 [会议前](teams-apps-in-meetings.md#pre-meeting-app-experience)和 [会议后](teams-apps-in-meetings.md#post-meeting-app-experience)的聊天中启用。

1. 会议 API URL 参数可能需要 `meetingId` 、 `userId` 和 [tenantId](/onedrive/find-your-office-365-tenant-id) 这些参数可用作团队客户端 SDK 和 bot 活动的一部分。 此外，还可以使用 [选项卡 SSO 身份验证](../tabs/how-to/authentication/auth-aad-sso.md)检索用户 ID 和租户 ID 的可靠信息。

1. 某些会议 Api （如 `GetParticipant` 将需要 [机器人注册和 BOT 应用 ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) 生成身份验证令牌）。

1. 作为开发人员，您必须遵循在团队会议期间触发的会议前和会议中对话框[的 "常规](design/designing-in-meeting-dialog.md)[团队" 选项卡设计指导方针](../tabs/design/tabs.md)。

1. 请注意，为了使您的应用程序实时更新，必须根据会议中的事件活动保持最新。 这些事件可以在会议中的对话框 (引用 `bot Id` `Notification Signal API` 会议生命周期的) 和其他表面中的完成参数

## <a name="meeting-apps-api-reference"></a>会议应用程序 API 参考

|API|说明|请求|源|
|---|---|----|---|
|**GetUserContext**| 获取上下文信息以在 "团队" 选项卡中显示相关内容。 |_**microsoftTeams getContext ( ( ) => {/*...*/} )**_|Microsoft 团队客户端 SDK|
|**GetParticipant**|此 API 允许 bot 按会议 id 和参与者 id 提取参与者信息。|**获取** _**/v1/meetings/{meetingId}/participants/{participantId}？ tenantId = {tenantId}**_ |Microsoft Bot 框架 SDK|
|**NotificationSignal** |将使用以下现有对话通知 API 为用户-bot 聊天) 传递会议信号 (。 通过此 API，开发人员可以基于最终用户操作发出信号，以显示会议中的对话气泡图。|**POST** _**/v3/conversations/{conversationId}/activities**_|Microsoft Bot 框架 SDK|

### <a name="getusercontext"></a>GetUserContext

请参阅我们 [的 "获取团队上下文" 选项卡](../tabs/how-to/access-teams-context.md#getting-context-by-using-the-microsoft-teams-javascript-library) 文档，获取有关标识和检索您的选项卡内容的上下文信息的指南。 作为会议扩展性的一部分，已为响应负载添加了一个新值：

✔ **meetingId**：在会议上下文中运行时由选项卡使用。

### <a name="getparticipant-api"></a>GetParticipant API

> [!NOTE]
>
> * 不缓存参与者角色，因为会议组织者可以在任何时间点更改角色。
>
> * 团队目前不支持 API 的多350个参与者的大型通讯组列表或名单大小 `GetParticipant` 。
>
> * 即将推出对 Bot 框架 SDK 的支持。


#### <a name="request"></a>请求

```http
GET /v3/meetings/{meetingId}/participants/{participantId}?tenantId={tenantId}
```

*请参阅* [Bot 框架 API 参考](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)。

<!-- markdownlint-disable MD025 -->

**C # 示例**

```csharp
string meetingId = "meetingid?";
string participantId = "participantidhere";
var connectorClient = turnContext.TurnState.Get<IConnectorClient>();
var creds = connectorClient.Credentials as AppCredentials;
var bearerToken = await creds.GetTokenAsync().ConfigureAwait(false);
var request = new HttpRequestMessage();
request.Headers.Authorization = new AuthenticationHeaderValue("Bearer", bearerToken);
request.Method = new HttpMethod("GET");
request.RequestUri = new System.Uri(Path.Combine(connectorClient.BaseUri.OriginalString, $"/meetings/{meetingId}/participants/{participantId}"));
HttpResponseMessage response = await (connectorClient as ServiceClient<ConnectorClient>).HttpClient.SendAsync(request, cancellationToken).ConfigureAwait(false);
if (response.StatusCode == System.Net.HttpStatusCode.OK)
{
    var content = await response.Content.ReadAsStringAsync().ConfigureAwait(false);
    var theObject = Rest.Serialization.SafeJsonConvert.DeserializeObject<WhateverObjectIsReturned>(content, connectorClient.DeserializationSettings);
}
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a>查询参数

|值|类型|必需|说明|
|---|---|----|---|
|**meetingId**| string | 是 | 会议标识符可通过 Bot 调用和团队客户端 SDK 获取。|
|**participantId**| string | 是 | 此字段是用户 ID，可在选项卡 SSO、Bot 调用和团队客户端 SDK 中使用。 强烈建议使用 Tab SSO|
|**tenantId**| string | 是 | 租户用户所需的。 它在选项卡 SSO、Bot 调用和团队客户端 SDK 中可用。 强烈建议使用 Tab SSO|

#### <a name="response-payload"></a>响应有效负载
<!-- markdownlint-disable MD036 -->

"会议" 下的 **角色** 可以是 *组织者*、*演示者* 或 *与会者*。

**示例 1**

```json
{
  "user":
  {
      "id": "29:1JKiJGPAX9TTxtGxhVo0wLx_zwzo-gG8Z-X03306vBwi9p-xMTEbDXsT6KH7-0kkTS8cD-2zkrsoV6f5WJ6_aYw",
      "aadObjectId": "6aebbad0-e5a5-424a-834a-20fb051f3c1a",
      "name": "Allan Deyoung",
      "givenName": "Allan",
      "surname": "Deyoung",
      "email": "Allan.Deyoung@microsoft.com",
      "userPrincipalName": "Allan.Deyoung@microsoft.com",
      "tenantId": "72f988bf-86f1-41af-91ab-2d7cd011db47",
      "userRole": "user"
  },
  "meeting":
  {
      "role ": "Presenter",
      "inMeeting":true
  },
  "conversation":
  {
      "id": "<conversation id>"
  }
}
```
#### <a name="response-codes"></a>响应代码

**403**：不允许应用获取参与者信息。 这是最常见的错误响应，当应用程序未安装在会议中时（如租户管理员禁用或在实时网站迁移过程中被阻止）时，会触发此响应。  
**200**：成功检索参与者信息。  
**401**：令牌无效。  
**404**：找不到参与者。 
**500**：会议已过期 (超过60天，自会议结束) 或参与者没有基于其角色的权限。

**即将推出**

**404**：会议已过期，或者找不到参与者。 

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a>NotificationSignal API

> [!NOTE]
> 在调用会议内对话时，相同的内容也会显示为聊天消息。

#### <a name="request"></a>请求

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a>查询参数

|值|类型|必需|说明|
|---|---|----|---|
|**conversationId**| string | 是 | 会话标识符作为机器人 invoke 的一部分提供 |

#### <a name="request-payload"></a>请求有效负载

> [!NOTE]
>
> *  在下面请求的负载中， `completionBotId` 的参数 `externalResourceUrl` 是可选的。 它是 `Bot ID` 在清单中声明的。 机器人将接收到一个 result 对象。
> * ExternalResourceUrl width 和 height 参数必须以像素为单位。 请参阅 [设计准则](design/designing-in-meeting-dialog.md) ，以确保尺寸在允许的限制范围内。
> * URL 是 `<iframe>` 在会议对话中加载的页面。 URL 的域必须位于 `validDomains` 应用程序清单中的应用程序阵列中。


# <a name="json"></a>[JSON](#tab/json)

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

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
MeetingNotification notification = new MeetingNotification
  {
    AlertInMeeting = true,
    ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
  };
activity.ChannelData = new TeamsChannelData
  {
    Notification = notification
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

* * *

> [!IMPORTANT]
> 内容气泡 (taskInfo URL 中的 URL) 必须包含在团队应用程序清单中的 [有效域](../resources/schema/manifest-schema.md#validdomains) 列表中。

#### <a name="response-codes"></a>响应代码

**201**：已成功发送信号活动  
**401**：令牌无效  
**403**：不允许应用发送信号。 在这种情况下，有效负载应包含更详细的错误消息。 可能有多种原因：应用程序因租户管理员而被禁用，在 live 网站缓解等过程中被阻止。  
**404**：会议聊天不存在  

## <a name="enable-your-app-for-teams-meetings"></a>为团队会议启用您的应用程序

### <a name="update-your-app-manifest"></a>更新应用程序清单

会议应用程序功能是通过 **configurableTabs**  ->  **作用域** 和 **上下文** 数组在应用程序清单中声明的。 *作用域* 定义了您的应用程序将在何处定义的人员和 *上下文* 。

> [!NOTE]
> * 请使用 [开发人员预览版清单架构](../resources/schema/manifest-schema-dev-preview.md) 在你的应用程序清单中试用此架构。

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

该选项卡 `context` 和 `scopes` 属性在协调中使用，以确定您希望应用程序的显示位置。 或范围中的选项卡 `team` `groupchat` 可以有多个上下文。 Context 属性的可能值如下所示：

* **channelTab**：团队频道标头中的一个选项卡。
* **privateChatTab**：组标头中的一个选项卡，在一组不在团队或会议的上下文中的一组用户之间聊天。
* **meetingChatTab**：组标头中的一个选项卡，在计划会议上下文中的一组用户之间聊天。
* **meetingDetailsTab**：日历的 "会议详细信息" 视图标头中的一个选项卡。
* **meetingSidePanel**：通过 (u) 的统一栏打开的会议面板。

> [!NOTE]
> "Context" 属性目前不受支持，因此在移动客户端上将被忽略

## <a name="configure-your-app-for-meeting-scenarios"></a>为会议方案配置应用程序

> [!NOTE]
> * 若要使您的应用程序在选项卡库中可见，它需要 **支持可配置的选项卡** 和 **组聊天作用域**。
>
> * 移动客户端仅支持准备会议和投递会议表面中的选项卡。 在会议中 (会议中的对话和面板) 的体验将很快推出。 创建移动电话选项卡时，请遵循 [移动电话上的选项卡指南](../tabs/design/tabs-mobile.md) 。 

### <a name="pre-meeting"></a>会议前

拥有组织者和/或演示者角色的用户使用会议 **聊天** 和会议 **详细信息** 页中的加号➕按钮将选项卡添加到会议。 邮件扩展通过位于聊天的撰写邮件区域下的省略号/溢出菜单 &#x25CF;&#x25CF;&#x25CF; 添加到中。 将 bot 添加到会议聊天中，使用 " **@** " 键，然后选择 " **获取 bot**"。

✔ *必须* 通过 [选项卡 SSO](../tabs/how-to/authentication/auth-aad-sso.md)确认用户标识。 遵循此身份验证后，应用可以通过 GetParticipant API 检索用户角色。

 ✔基于用户角色，应用现在将能够呈现特定于角色的体验。 例如，轮询应用程序可以仅允许组织者和演示者创建新的轮询。

> **注意**：在会议进行过程中，可以更改角色分配。  *请参阅*[团队会议中的角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。 

### <a name="in-meeting"></a>会议中

#### <a name="sidepanel"></a>**sidePanel**

在您的应用程序清单中✔将 **sidePanel** 添加到 **上下文** 阵列中，如上文所述。

✔在会议中以及在所有情况下，应用程序将呈现在320px 中的 "会议" 选项卡中，宽度为宽。 您的选项卡必须针对此进行优化。 *请参阅* [FrameContext 接口](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/framecontext?view=msteams-client-js-latest&preserve-view=true
)

✔请参阅 [团队 SDK](../tabs/how-to/access-teams-context.md#user-context) ，以使用 **userContext** API 进行相应的路由请求。

✔引用 [选项卡的团队身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。 选项卡的身份验证流非常类似于网站的身份验证流。 因此，选项卡可以直接使用 OAuth 2.0。 *另请参阅* [Microsoft Identity platform 和 OAuth 2.0 授权代码流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

当用户处于会议视图中时，✔邮件扩展应按预期方式工作，并且应该能够发布撰写邮件扩展卡。

✔的 AppName 工作项-工具提示应声明应用程序名称在会议中的 U-条形图中。

#### <a name="in-meeting-dialog"></a>**会议对话**

✔您必须遵守 [会议中的对话框设计准则](design/designing-in-meeting-dialog.md)。

✔引用 [选项卡的团队身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。

✔使用 [通知](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API 指示需要触发气泡通知。

✔作为通知请求负载的一部分，请添加承载要 showcased 内容的 URL。

✔会议对话中不能使用任务模块。

> [!NOTE]
>
> * 这些通知在本质上是永久性的。 在用户在 web 视图中执行某项操作后，必须调用 [**submitTask ( # B1**](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 函数以自动消除。 这是应用程序提交的必要条件。 *另请参阅*[团队 SDK：任务模块](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。
>
> * 如果您希望您的应用程序支持匿名用户，初始的调用请求负载必须依赖于 `from.id`  用户的 (ID) 对象中的请求元数据 `from` ，而不是 `from.aadObjectId` 用户) 请求元数据的 (AZURE Active Directory ID。 *请参阅*[在选项卡中使用任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md)和 [创建并发送任务模块](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。

### <a name="post-meeting"></a>会议后

会议后和会议前配置是等效的。

## <a name="meeting-app-sample"></a>会议应用程序示例

 > [!div class="nextstepaction"]
> [会议令牌生成器应用](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
