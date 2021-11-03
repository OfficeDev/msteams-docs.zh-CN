---
title: Teams 会议中应用的先决条件
author: surbhigupta
description: 确定会议Teams的先决条件
ms.topic: conceptual
ms.author: lajanuar
ms.localizationpriority: medium
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: 9ac6e87a8f85d0e8d73c6bf58dd705a55f887f43
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720230"
---
# <a name="prerequisites-for-apps-in-teams-meetings"></a>Teams 会议中应用的先决条件

借助Teams会议，可以在会议生命周期内扩展应用的功能。 使用会议Teams之前，必须满足以下先决条件：

* 了解如何开发Teams应用程序。 若要详细了解如何开发应用Teams，请参阅Teams[应用开发](../overview.md)。

* 更新Teams应用清单，以指示该应用可用于会议。 有关详细信息，请参阅 [应用清单](enable-and-configure-your-app-for-teams-meetings.md#update-your-app-manifest)。

* 使用支持 groupchat 作用域中的可配置选项卡的应用。 有关详细信息，请参阅群[聊范围和](../resources/schema/manifest-schema.md#configurabletabs)[构建组选项卡](../build-your-first-app/build-channel-tab.md)。

* 遵守Teams和会议后方案的常规选项卡设计准则。 有关会议期间的体验，请参阅会议中的选项卡和会议内对话框设计指南。 有关详细信息，请参阅Teams[选项卡](../tabs/design/tabs.md)设计指南、会议中的[选项卡](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-tab)设计指南和[会议中的对话框设计指南](../apps-in-teams-meetings/design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)。

* 支持 `groupchat` 范围以在会议前和会议后聊天中启用你的应用。 通过会议前应用体验，你可以查找和添加会议应用，以及执行会议前任务。 使用会议后应用体验，可以查看会议结果，例如投票调查结果或费用
* 会议 API URL 参数必须具有 `meetingId` 、 `userId` 和 `tenantId` 。 这些参数作为客户端 SDK 和自动程序Teams的一部分提供。 此外，您可以使用选项卡 SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。

* `GetParticipant`API 必须具有自动程序注册和 ID，以生成身份验证令牌。 有关详细信息，请参阅自动[程序注册和 ID。](../build-your-first-app/build-bot.md)

* 若要实时更新应用，应用必须基于会议中的活动活动是最新的。 这些事件可以位于会议中的对话框内以及整个会议生命周期的其他阶段。 有关会议中的对话框，请参阅 `bot Id` API 中的完成 `NotificationSignal` 参数。

* `Meeting Details`API 必须具有自动程序注册和自动程序 ID。 它需要 Bot SDK 才能获取 `TurnContext` 。

* 对于实时会议事件，你必须熟悉通过 `TurnContext` Bot SDK 提供的对象。 `Activity`中的 `TurnContext` 对象包含具有实际开始时间和结束时间的有效负载。 实时会议事件需要来自会议平台的已注册Teams ID。

* 在会议 API URL 中具有 参数 `meetingId` `userId` 、 和 `tenantId` 。 这些参数作为客户端 SDK 和自动程序Teams的一部分提供。 此外，您可以使用选项卡 SSO 身份验证检索用户 ID 和租户 ID [的可靠信息](../tabs/how-to/authentication/auth-aad-sso.md)。

* 在 API 中拥有自动程序注册 `GetParticipant` 和 ID 以生成身份验证令牌。 有关详细信息，请参阅自动[程序注册和 ID。](../build-your-first-app/build-bot.md)

* 根据会议中的活动活动使应用保持最新。 这些事件可以位于会议中的对话框内以及整个会议生命周期的其他阶段。 对于"会议内"对话框，请检查 API `bot Id` 中的完成 `NotificationSignal` 参数。

* 在 API 中拥有自动程序注册和自动程序 `MeetingDetails` ID。 它需要 Bot SDK 才能获取 `TurnContext` 。

* 熟悉通过 `TurnContext` Bot SDK 提供的对象。 `Activity`中的 `TurnContext` 对象包含具有实际开始时间和结束时间的有效负载。 实时会议事件需要来自会议平台的已注册Teams ID。

完成先决条件后，可以使用会议应用 API 引用 、 、 和 ，以便使用 属性访问信息并显示 `GetUserContext` `GetParticipant` `NotificationSignal` `Meeting Details` 相关内容。

> [!NOTE]
> TeamsJavaScript SDK (_版本_：1.10) 更高版本，SSO 在会议侧面板中运行。

## <a name="see-also"></a>另请参阅

* [会议内对话设计指南](design/designing-apps-in-meetings.md#use-an-in-meeting-dialog)
* [Teams选项卡的身份验证流](../tabs/how-to/authentication/auth-flow-tab.md)
* [会议Teams应用程序](teams-apps-in-meetings.md)

## <a name="next-step"></a>下一步

> [!div class="nextstepaction"]
> [会议应用 API 参考](API-references.md)
