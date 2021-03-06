---
title: 为会议启用和配置Teams应用程序
author: surbhigupta
description: 为会议启用和配置Teams应用程序
ms.topic: conceptual
ms.openlocfilehash: 16112b75e109702f1f0be6d335b8d407d35211b5
ms.sourcegitcommit: 3560ee1619e3ab6483a250f1d7f2ceb69353b2dc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2021
ms.locfileid: "53335366"
---
# <a name="enable-and-configure-your-apps-for-teams-meetings"></a>为会议启用和配置Teams应用程序

每个团队都有不同的通信和协作任务方式。 可以通过使用会议应用自定义Teams实现这些不同的任务。 若要自定义和完成不同的任务，必须启用用于会议Teams应用程序，并在其应用清单内将应用配置为在会议范围内可用。

## <a name="enable-your-app-for-teams-meetings"></a>为应用启用Teams会议

若要为应用启用Teams会议，必须更新应用清单，并使用上下文属性确定应用必须出现在何处。

### <a name="update-your-app-manifest"></a>更新应用清单

会议应用功能使用 、 和 数组在应用清单 `configurableTabs` `scopes` `context` 中声明。 范围定义谁，上下文定义你的应用的可用位置。

> [!NOTE]
> * 尝试使用清单架构更新 [应用清单](../resources/schema/manifest-schema-dev-preview.md)。
> * 会议中的应用程序需要群聊范围。 团队作用域仅适用于频道中的选项卡。

应用程序清单必须包含以下代码段：

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
> `meetingStage` 当前仅适用于开发人员 [预览](../resources/dev-preview/developer-preview-intro.md) 版。

### <a name="context-property"></a>Context 属性

属性确定当用户在会议调用应用时必须显示哪些内容，具体取决于用户 `context` 调用该应用的地方。 选项卡 `context` 和 `scopes` 属性使你可以确定应用必须出现在何处。 或 作用域 `team` `groupchat` 中的选项卡可以具有多个上下文。 以下是可以使用所有或部分 `context` 值的 属性的值：

|值|说明|
|---|---|
| **channelTab** | 团队频道标题中的选项卡。 |
| **privateChatTab** | 一组用户之间的群聊标题中的选项卡，不在团队或会议上下文中。 |
| **meetingChatTab** | 计划会议上下文中的一组用户之间的群聊标题中的选项卡。 可以指定 **meetingChatTab** 或 **meetingDetailsTab** 以确保应用在移动版中运行。 |
| **meetingDetailsTab** | 日历的会议详细信息视图标题中的选项卡。 可以指定 **meetingChatTab** 或 **meetingDetailsTab** 以确保应用在移动版中运行。 |
| **meetingSidePanel** | 通过统一栏打开的会议内面板 (U 条形图) 。 |
| **meetingStage** | meetingSidePanel 中的应用可以共享到会议阶段。 此选项卡在移动电话上不受支持。 |

为会议启用应用Teams，必须在会议前、会议期间和会议后配置应用。

## <a name="configure-your-app-for-meeting-scenarios"></a>为会议方案配置应用

> [!NOTE]
> 若要使应用在选项卡库中可见，它必须支持可配置的选项卡和群聊范围。

Teams会议可为组织提供独特的协作体验。 它提供了为不同的会议方案配置应用的机会。 你可以配置应用，以基于参与者角色或用户类型增强会议体验。 现在，您可以确定可以在以下会议方案中执行哪些操作：

* [会议前](#before-a-meeting)
* [会议期间](#during-a-meeting)
* [会议后](#after-a-meeting)

### <a name="before-a-meeting"></a>会议前

在会议之前，用户可以添加选项卡、聊天机器人和消息传递扩展。 具有组织者和演示者角色的用户可以向会议添加选项卡。

**向会议添加选项卡**

1. 在日历中，选择要添加选项卡的会议。
1. 选择" **详细信息"** 选项卡并选择 <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>.

    ![会议前体验](../assets/images/apps-in-meetings/PreMeeting.png)

1. 在出现的选项卡库中，选择要添加的应用并按照所需步骤操作。 应用作为选项卡安装。

    > [!NOTE]
    > 目前，在"会议"选项卡中，不支持获取会议详细信息和参与者信息。

**将消息传递扩展添加到会议**

1. 选择位于 &#x25CF;&#x25CF;&#x25CF; 撰写消息区域中的省略号。
1. 选择要添加的应用并按照所需步骤操作。 应用作为消息传递扩展进行安装。

**将机器人添加到会议**

在会议聊天中，输入 **@** 密钥并选择"**获取机器人"。**

> [!NOTE]
> * 必须使用选项卡 SSO 确认 [用户标识](../tabs/how-to/authentication/auth-aad-sso.md)。 身份验证后，应用可以使用 API 检索用户 `GetParticipant` 角色。
> * 根据用户角色，应用能够提供特定于角色的体验。 例如，轮询应用仅允许组织者和演示者创建新的轮询。
> * 可以在会议进行时更改角色分配。 有关详细信息，请参阅[会议Teams角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

### <a name="during-a-meeting"></a>会议期间

在会议期间，可以使用 meetingSidePanel 或会议内对话框为应用构建独特的体验。

#### <a name="meetingsidepanel"></a>meetingSidePanel

使用 meetingSidePanel，你可以自定义会议体验，使组织者和演示者拥有一组不同的视图和操作。 在应用清单中，必须将 meetingSidePanel 添加到上下文数组。 在会议以及所有方案中，应用在宽度为 320 像素的"会议内"选项卡中呈现。 有关详细信息，请参阅 [FrameContext 接口](/javascript/api/@microsoft/teams-js/microsoftteams.framecontext?view=msteams-client-js-latest&preserve-view=true)。

若要使用 `userContext` API 相应地路由请求，请参阅[Teams SDK。](../tabs/how-to/access-teams-context.md#user-context) 有关详细信息，请参阅Teams[身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)。 选项卡的身份验证流与网站的身份验证流非常相似。 因此选项卡可以直接使用 OAuth 2.0。 有关详细信息，请参阅 Microsoft 标识平台[和 OAuth 2.0 授权代码流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

当用户在会议视图中时，邮件扩展按预期方式工作，用户可以发布撰写邮件扩展卡。 AppName 会议内是一个工具提示，用于指出会议 U 栏中的应用名称。

> [!NOTE]
> 使用版本 1.7.0 或更高版本[的 Teams SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)因为它之前的版本不支持侧面板。

#### <a name="in-meeting-dialog-box"></a>"会议内"对话框

会议内对话框可用于在会议期间与参与者互动，并收集会议期间的信息或反馈。 使用 [`NotificationSignal`](create-apps-for-teams-meetings.md#notificationsignal-api) API 指示必须触发气泡通知。 作为通知请求有效负载的一部分，请包含要显示内容的托管 URL。

会议内对话框不得使用任务模块。 会议聊天中不会调用任务模块。 外部资源 URL 用于在会议中显示内容气泡。 可以使用 方法 `submitTask` 在会议聊天中提交数据。

> [!NOTE]
> * 您必须调用 [submitTask () ](../task-modules-and-cards/task-modules/task-modules-bots.md#submit-the-result-of-a-task-module) 函数，以在用户执行 Web 视图中的操作后自动消除。 这是应用提交的要求。 有关详细信息，请参阅Teams [SDK 任务模块](/javascript/api/@microsoft/teams-js/microsoftteams.tasks?view=msteams-client-js-latest#submittask-string---object--string---string---&preserve-view=true)。
> * 如果希望你的应用支持匿名用户，则初始调用请求有效负载必须依赖于 对象中的请求元数据， `from.id` `from` 而不是 `from.aadObjectId` 请求元数据。 `from.id`是用户 `from.aadObjectId` ID，也是Azure Active Directory (AAD) ID。 有关详细信息，请参阅在 [选项卡中使用任务模块](../task-modules-and-cards/task-modules/task-modules-tabs.md) 以及 [创建和发送任务模块](../messaging-extensions/how-to/action-commands/create-task-module.md?tabs=dotnet#the-initial-invoke-request)。

#### <a name="shared-meeting-stage"></a>共享会议阶段

> [!NOTE]
> * 此功能目前仅适用于开发人员 [预览](../resources/dev-preview/developer-preview-intro.md) 版。

共享会议阶段允许会议参与者实时与应用内容进行交互和协作。

必需的上下文 `meetingStage` 位于应用程序清单中。 这样做的先决条件是拥有 `meetingSidePanel` 上下文。 这将在 meetingSidePanel 中启用"共享"。

![在会议体验期间共享到阶段](~/assets/images/apps-in-meetings/share_to_stage_during_meeting.png)

若要启用共享会议阶段，请配置应用清单，如下所示：

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

了解如何设计 [共享会议阶段体验](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)。

### <a name="after-a-meeting"></a>会议后

会议后 [和会议之前](#before-a-meeting) 的配置相同。

## <a name="code-sample"></a>代码示例

|示例名称 | 说明 | 示例 |
|----------------|-----------------|--------------|----------------|-----------|
| 会议应用程序 | 演示如何使用会议令牌生成器应用请求令牌，该令牌是按顺序生成的，以便每个参与者都有机会参与会议。 这可在 scrum 会议和 Q&A 会话等情况下很有用。 | [View](https://github.com/OfficeDev/microsoft-teams-sample-meetings-token) |

## <a name="see-also"></a>另请参阅

* [会议内对话设计指南](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams选项卡的身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)
