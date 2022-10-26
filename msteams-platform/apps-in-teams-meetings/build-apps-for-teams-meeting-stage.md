---
title: 为 Teams 会议阶段生成应用
author: v-sdhakshina
description: 了解如何为 Teams 会议阶段生成应用、共享以暂存 API，以及如何生成一个深度链接来共享内容以在会议中登台。
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: ea5d7b57b9ee6344d34fcc6ed560936ac6109304
ms.sourcegitcommit: 4e355e22ddcd10ba9a8f37965c4f5c8fa04f5776
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/26/2022
ms.locfileid: "68701032"
---
# <a name="build-apps-for-teams-meeting-stage"></a>为 Teams 会议阶段生成应用

共享到阶段允许用户在正在进行的会议中从会议侧面板将应用共享到会议阶段。 与被动屏幕共享相比，此共享是交互式和协作的。

若要将共享调用到阶段，用户可以选择会议侧面板右上角的 **“共享到阶段** ”图标。 **“共享到阶段** ”图标原生于 Teams 客户端，选择它可将整个应用共享到会议阶段。

## <a name="app-manifest-settings-for-apps-in-meeting-stage"></a>会议阶段应用的应用清单设置

若要将应用共享到会议阶段，请 `context` 更新应用清单中的属性，如下所示：

```json
"context":[ 
    "meetingSidePanel", 
    "meetingStage" 
     ] 
```

## <a name="advanced-share-to-stage-apis"></a>用于暂存 API 的高级共享

在许多情况下，将整个应用共享到会议阶段并不像共享应用的特定部分那样有用：  

1. 对于集思广益或白板应用，用户可能希望在会议中与所有板共享整个应用的特定板。  

1. 对于医疗应用，医生可能只想与患者共享屏幕上的 X 射线，而不是与所有患者记录或结果共享整个应用，等等。

1. 用户可能希望一次从单个内容提供程序共享内容 (例如，YouTube) 而不是将整个视频目录共享到舞台上。

为了帮助此类情况下的用户，我们在 Teams 客户端 SDK 中发布了 API，允许你通过会议侧面板中的按钮以编程方式调用共享以暂存应用的特定部分。

:::image type="content" source="../assets/images/apps-in-meetings/shared-meeting-stage-edit-review-component.png" alt-text="屏幕截图显示“共享到会议阶段”视图。":::

使用以下 API 共享应用的特定部分：

|方法| 说明| 源|
|---|---|----|
|[**将应用内容共享到演示区域**](#share-app-content-to-stage-api)| 在会议中从会议侧面板将应用的特定部分共享到会议阶段。 | [Microsoft Teams JavaScript 库 SDK](/javascript/api/@microsoft/teams-js/meeting) |
|[**获取应用内容演示区域共享状态**](#get-app-content-stage-sharing-state-api)| 获取会议演示区域应用共享状态的信息。 | [Microsoft Teams JavaScript 库 SDK](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingstate) |
|[**获取应用内容演示区域共享功能**](#get-app-content-stage-sharing-capabilities-api)| 获取应用共享到会议演示区域的功能。 | [Microsoft Teams JavaScript 库 SDK](/javascript/api/@microsoft/teams-js/meeting.iappcontentstagesharingcapabilities) |

## <a name="share-app-content-to-stage-api"></a>将应用内容共享到演示区域

`shareAppContentToStage` API 能够帮助将应用的特定部分共享到会议演示区域。 可通过 Teams 客户端 SDK 获取 API。

### <a name="prerequisite"></a>先决条件

* 若要使用 `shareAppContentToStage` API，必须获取 RSC 权限。 在应用清单中，配置 `authorization` 属性，以及 `resourceSpecific` 字段中的 `name` 和 `type`。 例如：

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

* `appContentUrl` 必须允许 manifest.json 内的 `validDomains` 数组，否则 API 返回 501 错误。

### <a name="query-parameter"></a>查询参数

下表列出了查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**callback**| 字符串 | 是 | 回调包含 error 和 result 两个参数。 *error* 包含 *SdkError* 类型的错误，或在共享成功时返回 null。 如果共享成功， *则结果* 可以包含真正的值，或者在共享失败时为 null。 |
|**appContentURL**| 字符串 | 是 | 将共享到演示区域上的 URL。 |

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

下表列出了响应代码：

|响应代码|说明|
|---|---|
| **500** | 内部错误。 |
| **501** | 当前上下文不支持 API。|
| **1000** | 应用没有允许共享登台的适当权限。|

## <a name="get-app-content-stage-sharing-state-api"></a>获取应用内容演示区域共享状态 API

API `getAppContentStageSharingState` 使你能够获取有关在会议阶段共享的应用的信息。

### <a name="query-parameter"></a>查询参数

下表包含查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**callback**| 字符串 | 是 | 回调包含两个参数、错误和结果。 *error* 包含 *SdkError* 类型的错误（如果出错），或在共享成功时返回 null。 如果共享成功， *则结果* 可以包含 `IAppContentStageSharingState` 对象，如果出现错误，则为 null。|

### <a name="example"></a>示例

```javascript
microsoftTeams.meeting.getAppContentStageSharingState((err, result) => {
    if (result.isAppSharing) {
        // Indicates if app is sharing content on the meeting stage.
    }
});
```

`getAppContentStageSharingState` API 的 JSON 响应正文为：

```json
{
   "isAppSharing":true
} 
```

### <a name="response-codes"></a>响应代码

下表列出了响应代码：

|响应代码|说明|
|---|---|
| **500** | 内部错误。 |
| **501** | 当前上下文不支持 API。|
| **1000** | 应用没有允许共享登台的适当权限。|

## <a name="get-app-content-stage-sharing-capabilities-api"></a>获取应用内容演示区域共享功能 API

`getAppContentStageSharingCapabilities` API 可帮助获取应用共享到会议演示区域的功能。

### <a name="query-parameter"></a>查询参数

下表包含查询参数：

|值|类型|必需|说明|
|---|---|----|---|
|**callback**| 字符串 | 是 | 回调包含两个参数、错误和结果。 *error* 包含 *SdkError* 类型的错误，或在共享成功时返回 null。 如果共享成功，则结果可以包含 `IAppContentStageSharingCapabilities` 对象，如果出现错误，则为 null。|

### <a name="example"></a>示例

```javascript
microsoftTeams.meeting.getAppContentStageSharingCapabilities((err, result) => {
    if (result.doesAppHaveSharePermission) {
        // Indicates app has permission to share contents to meeting stage.
    }
});
```

`getAppContentStageSharingCapabilities` API 的 JSON 响应正文为：

```json
{
   "doesAppHaveSharePermission":true
} 
```

### <a name="response-codes"></a>响应代码

下表列出了响应代码：

|响应代码|说明|
|---|---|
| **500** | 内部错误。 |
| **501** | 当前上下文不支持 API。|
| **1000** | 应用没有允许共享登台的权限。|

## <a name="generate-a-deep-link-to-share-content-to-stage-in-meetings"></a>生成一个深度链接以共享要在会议中登台的内容

你还可以生成一个深度链接来共享应用以暂存和启动或加入会议。

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
* `appSharingUrl`：需要在舞台上共享的 URL 应是应用清单中定义的有效域。 如果 URL 不是有效的域，则会弹出一个错误对话框，为用户提供错误说明。
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

## <a name="build-an-in-meeting-document-signing-app"></a>生成会议内文档签名应用

可以生成会议内应用，使会议参与者能够实时登录文档。 它有助于在单个会话中查看和签名文档。 参与者可以使用其当前租户标识对文档进行签名。

可以使用会议内签名应用执行以下操作：

- 添加要在会议期间审阅的文档
- 共享要查看到主阶段的文档
- 使用签名者的标识对文档进行签名

参与者可以查看和签署文档，如采购协议和采购订单。

:::image type="content" source="../assets/images/sbs-inmeeting-doc-signing/final-output.png" alt-text="会议内文档签名应用":::

会议期间可能涉及以下参与者角色：

- **文档创建者**：此角色可以添加要审阅和签名的文档。
- **签名者**：此角色可以对已审阅的文档进行签名。
- **读者**：此角色可以查看添加到会议的文档。

## <a name="code-sample"></a>代码示例

|示例名称 | Description | C# | Node.js |
|----------------|-----------------|--------------|----------------|
|会议阶段示例 | 示例应用，用于在会议阶段显示用于协作的选项卡 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
| 会议内通知 | 演示如何使用机器人实现会议内通知。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |
| 会议内文档签名 | 演示如何实现文档签名 Teams 应用。 包括将特定应用内容共享到阶段、Teams SSO 和用户特定的阶段视图。 | [View](https://github.com/officedev/microsoft-teams-samples/tree/main/samples/meetings-share-to-stage-signing/csharp) | 不适用 |

## <a name="step-by-step-guide"></a>分步指南

按照 [分步指南](../sbs-inmeeting-document-signing.yml) 生成会议内文档签名应用。

## <a name="see-also"></a>另请参阅

* [选项卡的 Teams 身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)
* [Teams 会议应用](teams-apps-in-meetings.md)
* [会议的生成选项卡](build-tabs-for-meeting.md)
* [为会议聊天生成可扩展对话](build-extensible-conversation-for-meeting-chat.md)
* [为匿名用户生成应用](build-apps-for-anonymous-user.md)
* [高级会议 API](meeting-apps-apis.md)
* [自定义全体模式场景](~/apps-in-teams-meetings/teams-together-mode.md)
* [实时共享 SDK](teams-live-share-overview.md)
