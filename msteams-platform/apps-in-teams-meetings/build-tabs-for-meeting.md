---
title: 会议的生成选项卡
author: surbhigupta
description: 了解如何在 Microsoft Teams 会议中为会议聊天、会议侧面板和会议阶段生成选项卡。
ms.topic: conceptual
ms.author: surbhigupta
ms.localizationpriority: high
ms.date: 04/07/2022
ms.openlocfilehash: d86f0931cb6338ef331f2afe3a4a5fdb217bb316
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615379"
---
# <a name="build-tabs-for-meeting"></a>会议的生成选项卡

每个团队都有不同的方式来传达和协作任务。 若要完成这些不同的任务，请使用会议应用自定义 Teams。 为 Teams 会议启用应用，并将应用配置为在其应用清单的会议范围内可用。

## <a name="tabs-in-teams-meetings"></a>Teams 会议中的选项卡

选项卡允许会议参与者访问会议中特定空间中的服务和内容。 如果你不了解 Microsoft Teams 选项卡开发，请参阅 [Teams 的“生成”选项卡](/microsoftteams/platform/tabs/what-are-tabs)。

在创建会议选项卡之前，请务必了解可用于面向会议聊天视图、会议详细信息视图、会议侧面板视图和会议阶段视图的图面。

### <a name="meeting-details-view"></a>会议详细信息视图

1. 在日历中，选择要向其添加选项卡的会议。
1. 选择“ **详细信息”** 选项卡并选择 :::image type="icon" source="../assets/icons/add-icon.png" Border = "false":::” 将显示应用库。

   :::image type="content" source="~/assets/images/apps-in-meetings/Pre-Meeting-002.png" alt-text="此屏幕截图显示了 Teams 会议中的会议前应用体验。":::

1. 在应用库中，选择要添加的应用，并根据需要执行步骤。 该选项卡将添加到会议详细信息页。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

下图显示了在 Teams 桌面客户端中添加到会议详细信息页的选项卡：

   :::image type="content" source="~/assets/images/apps-in-meetings/PreMeetingTab.png" alt-text="屏幕截图显示 Teams 会议中会议详细信息视图中的桌面 Teams 选项卡。":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

下图显示了添加到 Teams 移动客户端中的会议详细信息页的选项卡：

   :::image type="content" source="../assets/images/mobile-tab.png" alt-text="屏幕截图显示 Teams 会议中会议详细信息视图中的移动 Teams 选项卡。":::

---

### <a name="meeting-chat-view"></a>会议聊天视图

1. 在 Teams 聊天面板中，选择会议聊天视图。

1. 选择 :::image type="icon" source="../assets/icons/add-icon.png" Border = "false"::: 并显示应用库。

1. 在应用库中，选择要添加的应用，并根据需要执行步骤。 该选项卡将添加到会议聊天中。

   :::image type="content" source="../assets/images/apps-in-meetings/meeting-chat-view.png" alt-text="屏幕截图显示 Teams 会议中的会议聊天视图。":::

### <a name="meeting-side-panel-view"></a>会议侧面板视图

1. 在会议期间，你可以从 Teams 会议窗口中选择:::image type="icon" source="../assets/icons/add-icon.png" Border = "false":::**“应用**”以向会议添加应用。

   :::image type="content" source="../assets/images/apps-in-meetings/add-app.png" alt-text="此屏幕截图显示了如何在 Teams 会议窗口中添加应用。":::

1. 在应用库中，选择要添加的应用，并根据需要执行步骤。 该应用将添加到会议侧面板。

   :::image type="content" source="../assets/images/side-panel-view.png" alt-text="此屏幕截图显示了包含应用列表的侧面板视图。":::

### <a name="meeting-stage-view"></a>会议阶段视图

1. 将选项卡添加到会议侧面板后，现在可以选择加入全局应用共享。

1. 这会导致会议中每个参与者在舞台上呈现选项卡。

   :::image type="content" source="../assets/images/meeting-stage-view.png" alt-text="此屏幕截图显示了你共享到会议的应用的会议阶段视图。":::

### <a name="apps-in-channel-meeting"></a>频道会议中的应用

公共计划频道会议的应用列表与其父团队相同。 将应用安装到频道会议还可以在父团队中使用，反之亦然。

但是，频道会议中的选项卡实例与频道本身的选项卡是分开的。 例如，假设 *开发* 频道有一个 *Polly* 选项卡。如果在该频道中创建 *“站立* 会议”，则该会议将不会有 *Polly* 选项卡，除非你将 [该选项卡显式添加到会议](#meeting-details-view)。

在公共计划的频道会议中，添加会议选项卡后，可以在会议详细信息页中选择会议对象以访问该选项卡。

:::image type="content" source="~/assets/images/apps-in-meetings/after-a-meeting1.png" alt-text="会议后":::

> [!NOTE]
> 在移动设备上，匿名用户无法访问计划的公共频道会议中的应用。

### <a name="app-manifest-settings-for-tabs-in-meeting"></a>会议中 Tabs 的应用清单设置

使用相关上下文属性更新 [应用清单](/microsoftteams/platform/resources/schema/manifest-schema) ，以配置不同的选项卡视图。 会议应用功能使用 configurableTabs 部分下的范围和上下文数组在应用清单中声明。

#### <a name="scope"></a>范围

范围定义谁可以访问应用。

* `groupchat` 作用域使你的应用在组范围内可用，并允许将应用添加到呼叫或会议 (计划的专用会议或即时会议) 中。

* `team` 范围使你的应用在团队范围内可用，并允许在团队或频道或计划频道会议中添加应用。

#### <a name="context"></a>上下文

该 `context` 属性确定在安装和配置后应用是否在特定视图中可用。 下面是 `context` 可用于所有值或部分值的属性的值：

|值|说明|
|---|---|
| **channelTab** | 团队频道标题中的选项卡。 |
| **privateChatTab** | 一组用户之间的群聊标头中的选项卡，而不是在团队或会议的上下文中。 |
| **meetingChatTab** | 计划会议的一组用户之间群组聊天标题中的选项卡。 可以指定 **meetingChatTab** 或 **meetingDetailsTab** 以确保应用在移动设备中工作。 |
| **meetingDetailsTab** | 日历会议详细信息视图标题中的选项卡。 可以指定 **meetingChatTab** 或 **meetingDetailsTab** 以确保应用在移动设备中工作。 |
| **meetingSidePanel** | 通过统一栏（U 栏）打开的会议内面板。 |
| **meetingStage** | 可将来自 `meetingSidePanel` 的应用共享到会议阶段。 不能在移动设备或 Teams 会议室客户端上使用此应用。 |

#### <a name="configure-tab-app-for-a-meeting"></a>为会议配置选项卡应用

会议中的应用可以使用以下上下文：`meetingChatTab`、`meetingDetailsTab`、`meetingSidePanel` 和 `meetingStage`。 在会议参与者安装应用并在会议中配置选项卡后，给定会议应用的其他所有目标上下文都开始呈现该选项卡。

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

---

#### <a name="other-examples"></a>其他示例

如果未指定选项卡的默认上下文 () 为：  

```json
"context":[ 
  "channelTab", 
  "privateChatTab", 
  "meetingChatTab", 
  "meetingDetailsTab" 
     ] 
```

若要防止应用在非会议组聊天中显示，必须设置以下上下文：

```json
"context":[ 
  "meetingSidePanel", 
  "meetingChatTab", 
  "meetingDetailsTab" 
     ] 
```

仅适用于会议侧面板体验：  

```json
"context":[ 
  "meetingSidePanel" 
     ] 
```

### <a name="advanced-tab-sdk-apis"></a>高级选项卡 SDK API

Microsoft Teams JavaScript 客户端 SDK 是一种丰富的 SDK，用于使用 JavaScript 创建选项卡。 使用最新的 TeamsJS (V.2.0 或更高版本) 在 Teams、Office 和 Outlook 中工作。 有关详细信息，请参阅 [Teams JavaScript 客户端 SDK](/microsoftteams/platform/tabs/how-to/using-teams-client-sdk?tabs=javascript%2Cmanifest-teams-toolkit)。

### <a name="frame-context"></a>框架上下文

Microsoft Teams JavaScript 库公开在 getContext API 中加载会议选项卡 URL 的 frameContext。 frameContext 的可能值为内容、任务、设置、删除、sidePanel 和 meetingStage。 这允许基于应用呈现的位置生成自定义体验。 例如，在聊天选项卡中 `meetingStage` 显示特定的协作重点 UI，在聊天选项卡中显示不同的会议准备 UI (`content`) 。 有关详细信息，请参阅 [getContext API](/microsoftteams/platform/tabs/how-to/access-teams-context?tabs=teamsjs-v2)。

## <a name="code-sample"></a>代码示例

|示例名称 | Description | C# | Node.js |
|----------------|-----------------|--------------|----------------|
| 会议应用 | 演示如何使用会议令牌生成器应用请求令牌。 令牌按顺序生成，以便每个参与者都有公平的机会参与会议。 在 Scrum 会议和 Q&A 会话等情况下，令牌非常有用。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-token-app/nodejs) |
| 会议阶段示例 | 示例应用，用于在会议阶段显示用于协作的选项卡 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-stage-view/nodejs) |
| 会议侧面板 | 演示如何在会议侧面板中添加议程的示例应用 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-sidepanel/csharp) |-|
| 会议内通知 | 演示如何使用机器人实现会议内通知。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/meetings-content-bubble/nodejs) |
| 会议内文档签名 | 演示如何实现文档签名 Teams 应用。 包括将特定应用内容共享到阶段、Teams SSO 和用户特定的阶段视图。 | [View](https://github.com/officedev/microsoft-teams-samples/tree/main/samples/meetings-share-to-stage-signing/csharp) | 不适用 |

> [!NOTE]
>
> * Teams 桌面客户端支持会议应用 (侧面板和会议阶段) 。
> * 仅 [当启用开发人员预览](/microsoftteams/platform/resources/dev-preview/developer-preview-intro#enable-developer-preview)版时，才支持 Teams Web 客户端中的会议应用 (侧面板和会议阶段) 。

## <a name="step-by-step-guides"></a>分步指南

* 按照 [分步准则](../sbs-meeting-token-generator.yml) 在 Teams 会议中生成会议令牌。
* 按照 [分步指南](../sbs-meetings-sidepanel.yml) 在 Teams 会议中生成会议侧面板。
* 按照 [分步准则](../sbs-meetings-stage-view.yml) 在 Teams 会议中共享会议阶段视图。
* 按照 [分步指南](../sbs-meeting-content-bubble.yml) 在 Teams 会议中生成会议内通知。

## <a name="see-also"></a>另请参阅

* [会议内通知设计指南](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [选项卡的 Teams 身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)
* [共享会议阶段体验设计准则](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [通过 Microsoft Graph 将应用添加到会议](/graph/api/chat-post-installedapps?view=graph-rest-1.0&tabs=http&preserve-view=true)
