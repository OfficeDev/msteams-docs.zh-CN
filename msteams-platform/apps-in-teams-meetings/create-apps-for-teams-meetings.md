---
title: Teams 会议中应用的先决条件
author: surbhigupta
description: 确定会议Teams的先决条件
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: 4c42a66f7891691b8c53d61d1ce637d57048eae8
ms.sourcegitcommit: 54f6690b559beedc330b971618e574d33d69e8a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2022
ms.locfileid: "62362737"
---
# <a name="prerequisites-for-apps-in-teams-meetings"></a>Teams 会议中应用的先决条件

借助Teams会议，你可以扩展整个会议生命周期的应用功能。 使用会议Teams之前，必须满足以下先决条件：

* 了解如何开发Teams应用程序。 若要详细了解如何开发应用Teams，请参阅Teams[应用开发](../overview.md)。

* 更新Teams应用清单，以指示该应用可用于会议。 有关详细信息，请参阅 [应用清单](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)。

* 使用支持 groupchat 作用域中的可配置选项卡的应用。 有关详细信息，请参阅群[聊范围和](../resources/schema/manifest-schema.md#configurabletabs)[构建组选项卡](../build-your-first-app/build-channel-tab.md)。

* 遵守Teams和会议后方案的常规选项卡设计准则。 有关会议期间的体验，请参阅会议中的选项卡和会议内对话框设计指南。 有关详细信息，请参阅Teams选项卡设计[指南](../tabs/design/tabs.md)、会议中的[选项卡](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)设计指南和[会议中的对话框设计指南](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

* `groupchat`支持范围以在会议前和会议后聊天中启用你的应用。 通过会议前应用体验，你可以查找和添加会议应用，以及执行会议前任务。 使用会议后应用体验，可以查看会议结果，例如投票调查结果或费用
* 会议 API URL 参数必须具有 、 `meetingId``userId`和 `tenantId`。 这些参数作为客户端 SDK 和自动程序Teams的一部分提供。 此外，您可以使用选项卡 SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。

* API `GetParticipant` 必须具有自动程序注册和 ID，以生成身份验证令牌。 有关详细信息，请参阅自动 [程序注册和 ID](../build-your-first-app/build-bot.md)。

* 若要实时更新应用，应用必须基于会议中的活动活动是最新的。 这些事件可以位于会议中的对话框内以及整个会议生命周期的其他阶段。 有关会议中的对话框，请参阅 API 中的完成`bot Id``NotificationSignal`参数。

* API `Meeting Details` 必须具有自动程序注册和自动程序 ID。 它需要 Bot SDK 才能获取 `TurnContext`。 若要使用会议详细信息 API，必须基于任何会议的范围（如私人会议或频道会议）获取不同的 RSC 权限。

* 对于实时会议事件，你必须 `TurnContext` 熟悉通过 Bot SDK 提供的对象。 中的 `Activity` 对象 `TurnContext` 包含具有实际开始时间和结束时间的有效负载。 实时会议事件需要来自会议平台的已注册Teams ID。 机器人可以通过在清单中添加 来自动接收会议开始或 `ChannelMeeting.ReadBasic.Group` 结束事件。

* 在会议 `meetingId``userId``tenantId` API URL 中具有 参数 、 和 。 这些参数作为客户端 SDK 和自动程序Teams的一部分提供。 此外，您可以使用选项卡 SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。

* 在 API 中拥有自动程序注册 `GetParticipant` 和 ID 以生成身份验证令牌。 有关详细信息，请参阅自动 [程序注册和 ID](../build-your-first-app/build-bot.md)。

* 根据会议中的活动活动使应用保持最新。 这些事件可以位于会议中的对话框内以及整个会议生命周期的其他阶段。 对于"会议内"对话框，请检查 API 中的`NotificationSignal`完成`bot Id`参数。

* 在 API 中拥有自动程序注册和自动程序 `MeetingDetails` ID。 它需要 Bot SDK 才能获取 `TurnContext`。

* 熟悉通过 `TurnContext` Bot SDK 提供的对象。 中的 `Activity` 对象 `TurnContext` 包含具有实际开始时间和结束时间的有效负载。 实时会议事件需要来自会议平台的已注册Teams ID。

完成先决条件后，可以使用会议应用 API `GetUserContext``GetParticipant``NotificationSignal``Meeting Details` 引用 、 、 和 ，以便使用 属性访问信息并显示相关内容。

> [!NOTE]
> Teams JavaScript SDK (_版本_：1.10) 更高版本，SSO 在会议侧面板中工作。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [为会议启用和配置Teams应用](enable-and-configure-your-app-for-teams-meetings.md)

## <a name="see-also"></a>另请参阅

* [会议内对话设计指南](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams选项卡的身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)
* [Teams 会议应用](teams-apps-in-meetings.md)
* [Teams自动程序 API 更改以提取团队或聊天成员](~/resources/team-chat-member-api-changes.md)
