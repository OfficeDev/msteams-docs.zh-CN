---
title: 创建适用于团队会议的应用
author: laujan
description: 创建团队会议的应用程序
ms.topic: conceptual
ms.author: lajanuar
keywords: 团队应用会议用户参与者角色 api
ms.openlocfilehash: a489a2a439c8aaacc2900e4c62084f13b34b3e30
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279676"
---
# <a name="create-apps-for-teams-meetings-preview"></a>为团队会议 (预览) 创建应用程序

>[!IMPORTANT]
> Microsoft 团队预览版中包含的功能仅用于早期访问、测试和反馈目的。 他们可能会在公开发布之前进行更改，并且不应在生产应用程序中使用。

## <a name="prerequisites-and-considerations"></a>先决条件和注意事项

1. 会议中的应用程序需要一些有关 [团队应用程序开发](../overview.md)的基本知识。 会议中的应用程序可以包含 [选项卡](../tabs/what-are-tabs.md)、 [bot](../bots/what-are-bots.md)和 [邮件扩展](../messaging-extensions/what-are-messaging-extensions.md) 功能，并将要求对团队 [应用程序清单](#update-your-app-manifest) 进行更新以指示该应用程序可用于会议

1. 为了使您的应用程序在会议生命周期中作为选项卡运行，它必须支持 [groupchat 范围](../resources/schema/manifest-schema.md#configurabletabs)中可配置的选项卡。 *请参阅*[使用自定义选项卡扩展团队应用](../tabs/how-to/add-tab.md)。如果支持此 `groupchat` 范围，您的应用程序将在[会议前](teams-apps-in-meetings.md#pre-meeting-app-experience)和[会议后](teams-apps-in-meetings.md#post-meeting-app-experience)的聊天中启用。

1. 会议 API URL 参数可能需要 `meetingId` 、 `userId` 和 [tenantId](/onedrive/find-your-office-365-tenant-id) 这些参数可用作团队客户端 SDK 和 bot 活动的一部分。 此外，还可以使用 [选项卡 SSO 身份验证](../tabs/how-to/authentication/auth-aad-sso.md)检索用户 ID 和租户 ID 的可靠信息。

1. 某些会议 Api （如 `GetParticipant` 将需要 [机器人注册和 BOT 应用 ID](../bots/how-to/create-a-bot-for-teams.md#with-an-azure-subscription) 生成身份验证令牌）。

1. 开发人员必须遵循 ["常规团队" 选项卡设计指南](../tabs/design/tabs.md) （适用于会议前后方案以及会议期间） (参阅 [会议对话框](../apps-in-teams-meetings/design/designing-in-meeting-dialog.md) 和 [会议中的选项卡](../apps-in-teams-meetings/design/designing-in-meeting-tab.md) 设计准则) 。

## <a name="meeting-apps-api-reference"></a>会议应用程序 API 参考

|API|说明|请求|Source|
|---|---|----|---|
|**GetUserContext**| 获取上下文信息以在 "团队" 选项卡中显示相关内容。 |_**microsoftTeams getContext ( ( ) => {/*...*/} ) **_|Microsoft 团队客户端 SDK|
|**GetParticipant**|此 API 允许 bot 按会议 id 和参与者 id 提取参与者信息。|**获取** _ **/v1/meetings/{meetingId}/participants/{participantId}？ tenantId = {tenantId}**_ |Microsoft Bot 框架 SDK|
|**NotificationSignal** |将使用以下现有对话通知 API 为用户-bot 聊天) 传递会议信号 (。 通过此 API，开发人员可以基于最终用户操作发出信号，以显示会议中的对话气泡图。|**POST** _ **/v3/conversations/{conversationId}/activities**_|Microsoft Bot 框架 SDK|

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
```

* * *
<!-- markdownlint-disable MD001 -->

#### <a name="query-parameters"></a>查询参数

**meetingId**。 会议标识符是必需的。  
**participantId**。 参与者标识符是必需的。  
**tenantId**。 参与者的[租户 id](/onedrive/find-your-office-365-tenant-id) 。 租户用户的必需。

#### <a name="response-payload"></a>响应有效负载
<!-- markdownlint-disable MD036 -->

**示例 1**

```json
{
   "meetingRole":"Presenter",
   "conversation":{
      "isGroup":true,
      "id":"19:meeting_NDQxMzg1YjUtMGIzNC00Yjc1LWFmYWYtYzk1MGY2MTMwNjE0@thread.v2"
   }
}
```

**meetingRole** 可以是 *组织者*、 *演示者*或 *与会者*。

**示例 2**

```json
{
   "meetingRole":"Attendee",
   "conversation":{
      "isGroup":true,
      "id":"19:meeting_OWIyYWVhZWMtM2ExMi00ZTc2LTg0OGEtYWNhMTM4MmZlZTNj@thread.v2"
   }
}
```

#### <a name="response-codes"></a>响应代码

**403**：不允许应用获取参与者信息。 这是最常见的错误响应，当应用程序未安装在会议中时（例如，当租户管理员禁用应用或在 live 网站缓解过程中被阻止）时，将会触发此响应。  
**200**：成功检索参与者信息  
**401**：令牌无效  
**404**：会议不存在或无法找到参与者。

<!-- markdownlint-disable MD024 -->
### <a name="notificationsignal-api"></a>NotificationSignal API

> [!NOTE]
> 在调用会议内对话时，相同的内容也会显示为聊天消息。

#### <a name="request"></a>请求

```http
POST /v3/conversations/{conversationId}/activities
```

#### <a name="query-parameters"></a>查询参数

**conversationId**：会话标识符。 必需

#### <a name="request-payload"></a>请求有效负载

# <a name="json"></a>[JSON](#tab/json)

```json
{
   "type":"message",
   "text":"John Phillips assigned you a weekly todo",
   "summary":"Don't forget to meet with Marketing next week",
   "channelData":{
      "notification":{
         "alert":true,
         "externalResourceUrl":"https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<TaskInfo.title>"
      }
   },
   "replyToId":"1493070356924"
}
```

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
Activity activity = MessageFactory.Text("This is a meeting signal test");
MeetingNotification notification = new MeetingNotification
{
    AlertInMeeting = true,
    ExternalResourceUrl = "https://teams.microsoft.com/l/bubble/APP_ID?url=&height=&width=&title=<TaskInfo.title>"
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
                externalResourceUrl: 'https://teams.microsoft.com/l/bubble/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>’
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

会议应用程序功能是通过**configurableTabs**  ->  **作用域**和**上下文**数组在应用程序清单中声明的。 *作用域* 定义了您的应用程序将在何处定义的人员和 *上下文* 。

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

该选项卡 `context` 和 `scopes` 属性在协调中使用，以确定您希望应用程序的显示位置。 当作用域中的选项卡 `personal` 只能有一个上下文，即， `personalTab`  `team` 或 `groupchat` 作用域的选项卡可以有多个上下文。 Context 属性的可能值如下所示：

* **channelTab**：团队频道标头中的一个选项卡。
* **privateChatTab**：组标头中的一个选项卡，在一组不在团队或会议的上下文中的一组用户之间聊天。
* **meetingChatTab**：组标头中的一个选项卡，在计划会议上下文中的一组用户之间聊天。
* **meetingDetailsTab**：日历的 "会议详细信息" 视图标头中的一个选项卡。
* **meetingSidePanel**：通过 (u) 的统一栏打开的会议面板。

## <a name="configure-your-app-for-meeting-scenarios"></a>为会议方案配置应用程序

> [!NOTE]
> 若要使您的应用程序在选项卡库中可见，它需要 **支持可配置的选项卡** 和 **组聊天作用域**。

### <a name="pre-meeting"></a>会议前

拥有组织者和/或演示者角色的用户使用会议 **聊天** 和会议 **详细信息** 页中的加号➕按钮将选项卡添加到会议。 邮件扩展通过位于聊天的撰写邮件区域下的省略号/溢出菜单 &#x25CF;&#x25CF;&#x25CF; 添加到中。 将 bot 添加到会议聊天中，使用 " **@** " 键，然后选择 " **获取 bot**"。

✔ *必须* 通过 [选项卡 SSO](../tabs/how-to/authentication/auth-aad-sso.md)确认用户标识。 遵循此身份验证后，应用可以通过 GetParticipant API 检索用户角色。

 ✔基于用户角色，应用现在将能够呈现特定于角色的体验。 例如，轮询应用程序可以仅允许组织者和演示者创建新的轮询。

> **注意**：在会议进行过程中，可以更改角色分配。  *请参阅*[团队会议中的角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。 

### <a name="in-meeting"></a>会议中

#### <a name="side-panel"></a>**侧面板**

在应用程序清单中✔将 **sidePanel** 添加到 **meetingSurfaces** 数组中，如上文所述。

✔在会议中以及在所有情况下，应用程序将呈现在320px 中的 "会议" 选项卡中，宽度为宽。 您的选项卡必须针对此进行优化。 *请参阅* [FrameContext 接口](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)

✔请参阅 [团队 SDK](../tabs/how-to/access-teams-context.md#user-context) ，以使用 **userContext** API 进行相应的路由请求。

✔引用 [选项卡的团队身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。 选项卡的身份验证流非常类似于网站的身份验证流。 因此，选项卡可以直接使用 OAuth 2.0。 *另请参阅* [Microsoft Identity platform 和 OAuth 2.0 授权代码流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

#### <a name="in-meeting-dialog"></a>**会议对话**

✔您必须遵守 [会议中的对话框设计准则](../apps-in-teams-meetings/design/designing-in-meeting-dialog.md)。

✔引用 [选项卡的团队身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。

✔使用 [通知](/graph/api/resources/notifications-api-overview?view=graph-rest-beta&preserve-view=true) API 指示需要触发气泡通知。

✔作为通知请求负载的一部分，请添加承载要 showcased 内容的 URL。

> [!NOTE]
> 这些通知在本质上是永久性的。 在用户在 web 视图中执行某项操作后，必须调用 [**submitTask ( # B1 **](../task-modules-and-cards/task-modules/task-modules-bots.md#submitting-the-result-of-a-task-module) 函数以自动消除。 这是应用程序提交的必要条件。 *另请参阅*[团队 SDK：任务模块](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。

### <a name="post-meeting"></a>会议后

会议后和会议前配置是等效的。

## <a name="meeting-app-sample"></a>会议应用程序示例

 > [!div class="nextstepaction"]
> [会议令牌生成器应用](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token)
