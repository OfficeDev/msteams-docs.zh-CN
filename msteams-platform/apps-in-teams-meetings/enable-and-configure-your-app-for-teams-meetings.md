---
title: 启用和配置 Teams 会议应用
author: surbhigupta
description: 了解如何为 Teams 会议和不同的会议应用场景启用和配置应用、更新应用清单、配置功能等。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.date: 04/07/2022
ms.openlocfilehash: b551513d61e7bb9ab2b9c118f756b3ce5232dde4
ms.sourcegitcommit: 20070f1708422d800d7b1d84b85cbce264616ead
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/12/2022
ms.locfileid: "68537582"
---
# <a name="enable-and-configure-apps-for-meetings"></a>为会议启用和配置应用

每个团队都有不同的方式来传达和协作任务。 若要完成这些不同的任务，请使用会议应用自定义 Teams。 启用 Teams 会议应用，并将应用配置为在其应用清单的会议范围内可用。

## <a name="prerequisites"></a>先决条件

使用 Teams 会议应用，可以在会议生命周期内扩展应用功能。 在使用 Teams 会议应用之前，必须满足以下先决条件：

* 了解如何开发 Teams 应用。 有关如何开发 Teams 应用的详细信息，请[参阅 Teams 应用开发](../overview.md)。

* 使用支持组聊天和/或团队范围内的可配置选项卡的应用。 有关详细信息，请参阅 [范围](../resources/schema/manifest-schema.md#configurabletabs) 并 [生成第一个选项卡应用](../build-your-first-app/build-channel-tab.md)。

* 会议前和会议后应用场景必须遵守常规 [Teams 选项卡设计准则](../tabs/design/tabs.md)。 有关会议期间的体验，请参阅 [会议内选项卡设计准则](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab) 和 [会议内对话框设计准则](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

* 若要使应用实时更新，它必须基于会议中的事件活动进行最新更新。 这些事件可以在会议内对话框中以及整个会议生命周期中的其他阶段内。 有关会议内对话框，请参阅`completionBotId`[会议内通知有效负载](API-references.md#send-an-in-meeting-notification)中的参数。

## <a name="enable-your-app-for-teams-meetings"></a>启用 Teams 会议应用

若要启用 Teams 会议应用，请更新应用清单并使用上下文属性来确定应用必须显示的位置。

### <a name="update-your-app-manifest"></a>更新应用清单

会议应用功能使用 `configurableTabs`、 `scopes`和 `context` 数组在应用清单中声明。 范围定义谁可以访问，上下文定义应用的可用位置。

> [!NOTE]
>
> * 会议中的应用需要 `groupchat` 或 `team` 作用域。 范围 `team` 适用于频道或频道会议中的选项卡。
> * 若要支持在计划的频道会议中添加选项卡，请在应用清单的 **“范围”** 部分中指定 **团队** 范围。 如果没有 **团队** 范围，应用将不会出现在频道会议的浮出控件中。
> * 会议中的应用可以使用以下上下文：`meetingChatTab`、`meetingDetailsTab`、`meetingSidePanel` 和 `meetingStage`。
> * 委托的 RSC 权 `MeetingStage.Write.Chat` 限，并且 `ChannelMeetingStage.Write.Group` 在清单中是启用会议阶段共享所必需的。

以下代码片段是 Teams 会议的应用中使用的可配置选项卡的示例：

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

### <a name="context-property"></a>Context 属性

`context` 属性确定当用户在会议中调用应用时必须显示的内容，具体取决于用户调用应用的位置。 使用选项卡 `context` 和 `scopes` 属性可以确定应用必须显示的位置。 `team` 或 `groupchat` 范围内的选项卡可以有多个上下文。

支持在会议前和会后聊天中启用 `groupchat` 的范围。 通过会议前应用体验，你可以查找和添加会议应用，并执行会议前任务。 通过会议后应用体验，用户可以查看会议结果，例如投票调查结果或费用。

 下面是可用于所有值或部分值 `context` 属性的值：

|值|说明|
|---|---|
| **channelTab** | 团队频道标题中的选项卡。 |
| **privateChatTab** | 一组用户之间的群聊标头中的选项卡，而不是在团队或会议的上下文中。 |
| **meetingChatTab** | 计划会议的一组用户之间群组聊天标题中的选项卡。 可以指定 **meetingChatTab** 或 **meetingDetailsTab** 以确保应用在移动设备中工作。 |
| **meetingDetailsTab** | 日历会议详细信息视图标题中的选项卡。 可以指定 **meetingChatTab** 或 **meetingDetailsTab** 以确保应用在移动设备中工作。 |
| **meetingSidePanel** | 通过统一栏（U 栏）打开的会议内面板。 |
| **meetingStage** | 可将来自 `meetingSidePanel` 的应用共享到会议阶段。 不能在移动设备或 Teams 会议室客户端上使用此应用。 |

启用 Teams 会议应用后，必须在会议前、会议期间和会议后配置应用。

## <a name="configure-your-app-for-meeting-scenarios"></a>为会议应用场景配置应用

Teams 会议为组织提供协作体验。 为不同的会议应用场景配置应用，并增强会议体验。 现在，可以确定可在以下会议应用场景中执行哪些操作：

* [会议前](#before-a-meeting)
* [会议期间](#during-a-meeting)
* [会议后](#after-a-meeting)

### <a name="before-a-meeting"></a>会议前

在会议之前，用户可以添加选项卡、机器人和消息扩展。 具有组织者和演示者角色的用户可以向会议添加选项卡。

若要将选项卡添加到会议：

1. 在日历中，选择要向其添加选项卡的会议。
1. 选择“**详细信息**”选项卡并选择 <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>.

    <img src="../assets/images/apps-in-meetings/PreMeeting1.png" alt="Pre-meeting experience" width="900"/>

1. 在显示的选项卡库中，选择要添加的应用，并根据需要执行步骤。 安装应用选项卡。

向会议添加消息扩展插件：

1. 选择位于聊天的撰写消息区域中的省略号 &#x25CF;&#x25CF;&#x25CF; 。
1. 选择要添加的应用，并根据需要执行步骤。 安装应用消息扩展。

若要将机器人添加到会议，请执行以下操作：

在会议聊天中，输入 **@** 密钥并选择“**获取机器人**”。

> [!NOTE]
>
> * 会议内对话框在会议中显示对话框，并在会议聊天中同时发布用户可以访问的自适应卡片。 会议聊天中的自适应卡片可帮助用户在参加会议时或 Teams 应用是否调整为最小化。
> * 必须使用 [Tabs SSO](../tabs/how-to/authentication/tab-sso-overview.md) 确认用户标识。 身份验证后，应用可以使用 `GetParticipant`API 检索用户角色。
> * 根据用户角色，应用能够提供特定于角色的体验。 例如，投票应用仅允许组织者和演示者创建新的投票。
> * 当会议正在进行时，可以更改角色分配。 有关详细信息，请参阅 [Teams 会议中的角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

### <a name="during-a-meeting"></a>会议期间

在会议期间，可以使用 `meetingSidePanel` 或会议内通知为应用构建独特的体验。

#### <a name="meeting-sidepanel"></a>Meeting SidePanel

`meetingSidePanel` 可用于自定义会议中的体验，并允许组织者和演示者具有不同的视图和操作集。 在应用清单中，必须添加 `meetingSidePanel` 到上下文数组。 在会议和所有情况下，应用在宽度为 320 像素的会议内选项卡中呈现。 有关详细信息，请参阅 [FrameInfo 接口](/javascript/api/@microsoft/teams-js/frameinfo)（在 TeamsJS v.2.0.0 之前称为 `FrameContext`）。

可以 [使用用户的上下文路由请求](../tabs/how-to/access-teams-context.md#user-context)。 有关详细信息，请参阅 [选项卡的 Teams 身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。 选项卡的身份验证流类似于网站的身份验证流。 选项卡可以直接使用 OAuth 2.0。 有关详细信息，请参阅 [Microsoft 标识平台和 OAuth 2.0 授权代码流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

当用户处于会议内视图中时，消息扩展按预期工作。 用户可以发布撰写消息扩展卡。 会议中的 AppName 是一个工具提示，用于在会议 U 栏中声明应用名称。

> [!NOTE]
> 使用版本 1.7.0 或更高版本的 [Teams SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)，因为之前的版本不支持侧面板。

#### <a name="in-meeting-notification"></a>会议内通知

会议内通知用于在会议期间与与会者接触，并在会议期间收集信息或反馈。 使用 [会议内通知有效负载](API-references.md#send-an-in-meeting-notification) 触发会议内通知。 作为通知请求有效负载的一部分，包括要显示内容托管的 URL。

会议内通知不得使用任务模块。 不会在会议聊天中调用任务模块。 外部资源 URL 用于显示会议内通知。 可以使用该 `submitTask` 方法在会议聊天中提交数据。

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-dialogbox.png" alt-text=" 示例演示如何使用会议内对话框。":::

还可以将用户的 Teams 显示图片和人员卡添加到会议内通知中，具体取决于`onBehalfOf`具有用户 MRI 的令牌以及传入有效负载的显示名称。 下面是一个示例有效负载：

```json
    {
       "type": "message",
       "text": "John Phillips assigned you a weekly todo",
       "summary": "Don't forget to meet with Marketing next week",
       "channelData": {
           onBehalfOf: [
             { 
               itemId: 0, 
               mentionType: 'person', 
               mri: context.activity.from.id, 
               displayname: context.activity.from.name 
             }
            ],
           "notification": {
           "alertInMeeting": true,
           "externalResourceUrl": "https://teams.microsoft.com/l/bubble/APP_ID?url=<url>&height=<height>&width=<width>&title=<title>&completionBotId=BOT_APP_ID"
            }
        },
       "replyToId": "1493070356924"
    }
```

:::image type="content" source="../assets/images/apps-in-meetings/in-meeting-people-card.png" alt-text="示例演示如何将 Teams 显示图片和人员卡片与会议内对话框一起使用。" border="true":::

#### <a name="shared-meeting-stage"></a>共享会议演示区域

共享会议阶段允许会议参与者实时与应用内容进行交互和协作。 可以通过以下方式将应用共享到协作会议阶段：

* [共享整个应用，以](#share-entire-app-to-stage) 在 Teams 客户端的会议侧面板中或通过[[深层链接](#generate-a-deep-link-to-share-content-to-stage-in-meetings)]使用共享暂存按钮。
* [共享应用的特定部分，以便](#share-specific-parts-of-the-app-to-stage)在Teams客户端 SDK 中使用 API 进行暂存。

##### <a name="share-entire-app-to-stage"></a>将整个应用共享暂存

参与者可以使用应用侧面板中的“共享暂存”按钮将整个应用共享到协作会议阶段。

<img src="../assets/images/apps-in-meetings/share_to_stage_during_meeting.png" alt="Share full app" width = "900"/>

若要共享要暂存的整个应用，必须在应用清单中将 `meetingStage` 和 `meetingSidePanel` 配置为帧上下文。 例如：

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

有关详细信息，请参阅 [应用清单](../resources/schema/manifest-schema-dev-preview.md#configurabletabs)。

##### <a name="share-specific-parts-of-the-app-to-stage"></a>共享要暂存应用的特定部分

参与者可以通过使用共享来暂存 API，将应用的特定部分共享到协作会议阶段。 API 在 Teams 客户端 SDK 中可用，并从应用端面板调用。

<img src="../assets/images/apps-in-meetings/share-specific-content-to-stage.png" alt="Share specific parts of the app" width = "900"/>

若要共享应用的特定部分，必须调用 Teams 客户端 SDK 库中的相关 API。 有关详细信息，请参阅 [API 参考](API-references.md)。

> [!NOTE]
>
> * 若要共享要暂存应用的特定部分，请使用 Teams 清单版本 1.12 或更高版本。
> * 只能在 Teams 桌面客户端上将应用的特定部分共享到会议阶段。 移动用户可以共享应用的特定部分，以使用 [共享来暂存 API](API-references.md#share-app-content-to-stage-api)。

### <a name="after-a-meeting"></a>会议后

会议后和 [会议前](#before-a-meeting) 配置相同。

## <a name="generate-a-deep-link-to-share-content-to-stage-in-meetings"></a>生成一个深度链接以共享要在会议中登台的内容

你还可以生成一个深度链接来 [共享应用以暂存](#share-entire-app-to-stage) 和启动或加入会议。

> [!NOTE]
>
> * 目前，用于在会议中分阶段共享内容的深度链接正在进行 UX 改进，并且仅在 [公共开发人员预览](~/resources/dev-preview/developer-preview-intro.md)版中可用。
> * 仅 Teams 桌面客户端支持共享会议阶段内容的深度链接。

当作为正在进行的会议一部分的用户在应用中选择深度链接时，应用将共享到该阶段，并显示权限弹出窗口。 用户可以向参与者授予与应用协作的访问权限。

:::image type="content" source="../assets/images/intergrate-with-teams/screenshot-of-pop-up-permission.png" alt-text="屏幕截图是显示权限弹出窗口的示例。":::

当用户不在会议中时，用户会重定向到 Teams 日历，在那里他们可以加入会议或启动即时会议 (会议现在) 。

:::image type="content" source="../assets/images/intergrate-with-teams/Instant-meetnow-pop-up.png" alt-text="屏幕截图是一个示例，显示在没有正在进行的会议时弹出窗口。":::

一旦用户启动即时会议 (会议现在) ，他们可以添加参与者并与应用交互。

:::image type="content" source="../assets/images/intergrate-with-teams/Screenshot-ofmeet-now-option-pop-up.png" alt-text="屏幕截图是一个示例，其中显示了添加参与者的选项以及如何与应用交互。":::

若要添加深度链接以在舞台上共享内容，需要具有应用上下文。 应用上下文允许 Teams 客户端提取应用清单，并检查是否可以在舞台上共享。 下面是应用上下文的示例。

`{ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9ec80a73-1d41-4bcb-8190-4b9eA9e29fbb" , "useMeetNow": false }`

应用上下文的查询参数为：

* `appID`：这是可以从应用清单获取的 ID。
* `appSharingUrl`：需要在舞台上共享的 URL 应是应用清单中定义的有效域。 如果 URL 不是有效的域，则会弹出错误对话框，向用户提供错误说明。
* `useMeetNow`：这包括可为 true 或 false 的布尔参数。
  * **True**：如果 `UseMeetNow` 值为 true，并且没有正在进行的会议，则将启动新的“立即开会”会议。 当有正在进行的会议时，将忽略此值。

  * **False**：默认值为 `UseMeetNow` false，这意味着当共享到阶段的深层链接且没有正在进行的会议时，将显示日历弹出窗口。 但是，可以在会议期间直接共享。

确保所有查询参数都正确编码了 URI，并且必须在最终 URL 中对应用上下文进行两次编码。 下面是一个示例。

```json
var appContext= JSON.stringify({ "appSharingUrl" : "https://teams.microsoft.com/extensibility-apps/meetingapis/view", "appId": "9cc80a93-1d41-4bcb-8170-4b9ec9e29fbb", "useMeetNow":false })
var encodedContext = encodeURIComponent(appcontext).replace(/'/g,"%27").replace(/"/g,"%22")
var encodedAppContext = encodeURIComponent(encodedContext).replace(/'/g,"%27").replace(/"/g,"%22")
```

可以从 Teams Web 或 Teams 桌面客户端启动深度链接。

* **Teams Web**：使用以下格式从 Teams Web 启动深度链接以在舞台上共享内容。

    `https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`

    例如：`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |深度链接|格式|示例|
    |---------|---------|---------|
    |若要共享应用并打开 Teams 日历，当 UseMeeetNow 为 **false** 时，默认值为默认值。|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |如果 UseMeeetNow **为 true**，则共享应用并启动即时会议。|`https://teams.microsoft.com/l/meeting-share?deeplinkId={deeplinkid}&fqdn={fqdn}}&lm=deeplink%22&appContext={encoded app context}`|`https://teams.microsoft.com/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

* **团队桌面客户端**：使用以下格式从 Teams 桌面客户端启动深度链接，在舞台上共享内容。

    `msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`

    例如：`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`

    |深度链接|格式|示例|
    |---------|---------|---------|
    |若要共享应用并打开 Teams 日历，当 UseMeeetNow 为 **false** 时，默认值为默认值。|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Afalse%257D`|
    |如果 UseMeeetNow **为 true**，则共享应用并启动即时会议。|`msteams:/l/meeting-share?   deeplinkId={deeplinkid}&fqdn={fqdn}&lm=deeplink%22&appContext={encoded app context}`|`msteams:/l/meeting-share?deeplinkId={sampleid}&fqdn=teams.microsoft.com&lm=deeplink%22&appContext=%257B%2522appSharingUrl%2522%253A%2522https%253A%252F%252Fteams.microsoft.com%252Fextensibility-apps%252Fmeetingapis%252Fview%2522%252C%2522appId%2522%253A%25229cc80a93-1d41-4bcb-8170-4b9ec9e29fbb%2522%252C%2522useMeetNow%2522%253Atrue%257D`|

查询参数为：

* `deepLinkId`：用于遥测关联的任何标识符。
* `fqdn`： `fqdn` 是一个可选参数，可用于切换到会议的适当环境以在舞台上共享应用。 它支持特定应用共享在特定环境中发生的情况。 默认值`fqdn`为企业 URL，可能的值`Teams.live.com`适用于 Teams for Life 或 `teams.microsoft.com``teams.microsoft.us`。

若要将整个应用共享到阶段，必须在应用清单中配置`meetingStage``meetingSidePanel`并作为帧上下文，请参阅[应用清单](../resources/schema/manifest-schema.md)。 否则，与会者可能无法在舞台上看到内容。

> [!NOTE]
> 若要使应用通过验证，从网站、Web 应用或自适应卡片创建深度链接时，请使用 **会议中的共享** 作为字符串或复制。

## <a name="code-sample"></a>代码示例

|示例名称 | Description | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| 会议应用 | 演示如何使用会议令牌生成器应用请求令牌。 令牌按顺序生成，以便每个参与者都有公平的机会参与会议。 在 Scrum 会议和 Q&A 会话等情况下，令牌非常有用。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
|会议阶段示例 | 示例应用，用于在会议阶段显示用于协作的选项卡 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
|会议侧面板 | 演示如何在会议侧面板中添加议程的示例应用 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|

## <a name="step-by-step-guides"></a>分步指南

* 按照 [分步准则](../sbs-meeting-token-generator.yml) 在 Teams 会议中生成会议令牌。
* 按照 [分步准则](../sbs-meetings-sidepanel.yml) 在 Teams 会议中生成会议侧窗格。
* 按照 [分步准则](../sbs-meetings-stage-view.yml) 在 Teams 会议中共享会议阶段视图。
* 按照[分步准则](../sbs-meeting-content-bubble.yml) 在 Teams 会议中生成会议内容气泡。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [会议应用 API 参考](API-references.md)

## <a name="see-also"></a>另请参阅

* [会议内对话框设计准则](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [选项卡的 Teams 身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)
* [共享会议阶段体验设计准则](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [通过 Microsoft Graph 将应用添加到会议](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
