---
title: Teams 会议应用
author: surbhigupta
description: 本文介绍基于参与者、用户角色和应用扩展性的 Microsoft Teams 会议中的应用工作原理。
ms.topic: overview
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: a462c3e4f5e6aef332fbb0b05cce8b1f2fa7d5a7
ms.sourcegitcommit: b9ec2a17094cb8b24c3017815257431fb0a679d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2022
ms.locfileid: "67990887"
---
# <a name="apps-for-teams-meetings-and-calls"></a>Teams 会议和呼叫的应用

会议可实现协作、合作、明智的沟通和共享反馈。 会议应用可以为会议生命周期的每个阶段提供用户体验。 会议生命周期包括会议前、会议内和会议后应用体验，具体取决于与会者的状态。

> [!Note]
>
> 用于即时会议、计划的公共频道会议、一对一和组呼叫的应用目前仅在 [公共开发人员预览版](../resources/dev-preview/developer-preview-intro.md)中可用。

Teams 支持在会议期间针对以下会议类型访问应用：

* [**计划会议**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop)：通过 Teams 日历安排的会议。
* [**计划频道会议**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop)：通过 Teams 公共频道安排的会议。
* [**一对一呼叫**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798)：在一对一聊天中发起的呼叫。
* [**组呼叫**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798)：在群聊中启动的呼叫。
* [**即时会议**](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5)：Teams 日历中通过 **“立即开会”** 按钮启动的会议。

用户可以使用 **+** Teams 会议窗口中的选项向会议添加应用。

:::image type="content" source="../assets/images/apps-in-meetings/add-app.png" alt-text="在会议中添加应用" border="true":::

访问 [Teams 应用商店](https://go.microsoft.com/fwlink/p/?LinkID=2183121) 并浏览专为会议设计的应用。

> [!Note]
>
> * 当前，当第三人称添加到一对一呼叫时，调用将提升为组调用，这意味着新会话将启动。 添加到一对一调用的应用在组调用中不可用。 但是，可以再次添加它们。
>
> * 目前，Teams 即时频道会议不支持应用体验。

下图提供了会议应用扩展性功能的概念：

![会议应用可扩展性](../assets/images/apps-in-meetings/meetingappextensibility.png)

本文概述了 Teams 中的会议应用扩展性、API 参考、为会议启用和配置应用以及自定义“在一起”模式场景。

* **扩展会议应用**：使用会议扩展性功能增强会议体验。 此功能使你能够在会议中集成应用。 它还包括会议生命周期的不同阶段，你可以在其中集成选项卡、机器人和消息扩展。 可以识别各种参与者角色和用户类型、获取会议事件并生成会议内对话框。
* **为会议配置应用**：若要使用会议应用自定义 Teams，请通过更新应用清单为 Teams 会议启用应用，同时为会议方案配置应用。
* **使用“一起模式”场景进行自定义**：新的自定义“一起模式”场景功能使用户能够在一个位置与其团队的会议中进行协作。
* **在共享通道中自定义应用权限**：如果应用在共享通道中共享重要信息，则可以自定义外部成员的应用权限。 [共享频道](../concepts/build-and-test/Shared-channels.md)中的应用权限遵循主机团队的应用名册和主机租户的应用策略。
* **检索会议脚本**：可以在会后方案中访问和检索会议脚本。 将应用配置为自动获取计划会议的脚本，并将其用于见解、智能分析等。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [统一会议应用](meeting-app-extensibility.md)

## <a name="see-also"></a>另请参阅

* [设计 Microsoft Teams 会议扩展](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [会议应用 API 参考 - Teams](~/apps-in-teams-meetings/api-references.md)
* [自定义全体模式场景](~/apps-in-teams-meetings/teams-together-mode.md)
* [为 Teams 会议启用和配置应用](~/apps-in-teams-meetings/enable-and-configure-your-app-for-teams-meetings.md)
* [会议生命周期](meeting-app-extensibility.md#meeting-lifecycle)
* [通过 Live Share SDK 增强协作](teams-live-share-overview.md)
