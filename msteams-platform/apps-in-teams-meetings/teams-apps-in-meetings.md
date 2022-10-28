---
title: Teams 会议应用
author: surbhigupta
description: 本文将基于参与者和用户角色以及应用扩展性了解应用在 Microsoft Teams 会议中的工作原理。
ms.topic: overview
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: f253a4ca3d09e48f99df36fdcb77bdd740fab5ff
ms.sourcegitcommit: bb15ce26cd65bec90991b703069424ab4b4e1a61
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/28/2022
ms.locfileid: "68772270"
---
# <a name="apps-for-teams-meetings-and-calls"></a>Teams 会议和通话应用

会议可实现协作、合作、明智的沟通和共享反馈。 会议空间可以为会议生命周期的每个阶段提供用户体验。 下图提供了会议应用扩展性功能的概念：

:::image type="content" source="../assets/images/apps-in-meetings/meetingappextensibility.png" alt-text="屏幕截图显示了会议应用扩展性的工作原理。":::

你必须熟悉以下产品概念，才能在 Microsoft Teams 中使用应用创建自定义会议体验。

## <a name="supported-meeting-types-in-teams"></a>Teams 中支持的会议类型

Teams 支持在会议期间访问以下会议类型的应用：

* [**计划会议**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop)：通过 Teams 日历安排的会议。
* [**计划频道会议**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop)：通过 Teams 公共频道安排的会议。
* [**一对一通话**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798)：在一对一聊天中发起的通话。
* [**群组通话**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798)：群组聊天中发起的通话。
* [**即时会议**](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5)：通过 Teams 日历中的“ **立即开会** ”按钮启动的会议。
* [**网络研讨会**](https://support.microsoft.com/office/get-started-with-teams-webinars-42f3f874-22dc-4289-b53f-bbc1a69013e3)：通过 **“新建会议**”下拉列表下的 **“网络研讨会**”按钮启动的网络研讨会。

详细了解 [Teams 会议、过期和策略](/MicrosoftTeams/meeting-expiration) 以及 [会议、网络研讨会和实时事件](/microsoftteams/quick-start-meetings-live-events)。
> [!NOTE]
>
> * 计划公共频道会议的应用目前仅在 [公共开发人员预览版](../resources/dev-preview/developer-preview-intro.md)中可用。
> * 以下各项不支持应用：
>   * [公用电话交换网 (PSTN) Teams 呼叫](/microsoftteams/cloud-voice-landing-page#public-switched-telephone-network-connectivity-options)
>   * [端到端加密 Teams 调用](https://support.microsoft.com/office/use-end-to-end-encryption-for-teams-calls-1274b4d2-b5c5-4b24-a376-606fa6728a90)
>   * [即时频道会议](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5)
>   * [共享频道](https://support.microsoft.com/office/what-is-a-shared-channel-in-teams-e70a8c22-fee4-4d6e-986f-9e0781d7d11d)中的会议

## <a name="meeting-lifecycle"></a>会议生命周期

会议生命周期包括会议前、会议中和会议后应用体验，具体取决于用户类型和用户在 Teams 会议中的角色。

## <a name="user-types-in-teams"></a>Teams 中的用户类型

Teams 支持 Teams 会议中的用户类型，例如租户内用户、来宾用户、联合用户或外部用户。 每个用户类型都可以 [在 Teams 会议中](#user-roles-in-teams-meeting)具有一个用户角色。

> [!NOTE]
>
> 目前，当第三人被添加到一对一呼叫时，该呼叫将提升为组呼叫，这意味着新会话将启动。 添加到一对一呼叫的应用在组呼叫中不可用。 但是，可以再次添加它们。

以下列表详细介绍了各种用户类型及其辅助功能：

* **租户内**：租户内用户属于组织，在 Azure Active Directory (AAD) 中拥有凭据。 他们是全职、现场或远程员工。 租户内用户可以是组织者、演示者或与会者。
* **来宾**：来宾是受邀访问 Teams 或组织租户中其他资源的来自其他组织的参与者。 来宾将添加到组织的 Azure AD，并且具有与本机团队成员相同的 Teams 功能。 他们有权访问团队聊天、会议和文件。 来宾可以是组织者、演示者或与会者。 有关详细信息，请参阅 [Teams 中的来宾访问](/microsoftteams/guest-access)。
* **联合或外部**：联合或外部用户是来自另一个组织的 Teams 用户，该用户已被邀请加入会议。 联合用户具有与联合合作伙伴的有效凭据，并且由 Teams 授权。 他们无权访问你的 Teams 或来自你的组织的其他共享资源。 来宾访问是外部用户有权访问 Teams 和频道的更好选项。 有关详细信息，请参阅 [在 Teams 中管理外部访问](/microsoftteams/manage-external-access)。

    > [!NOTE]
    > Teams 用户可以在主持会议或与其他组织聊天时添加应用。 当外部用户向会议共享应用时，所有用户都可以访问该应用。 由该用户组织共享的第三方应用的数据策略和数据共享做法将生效。

* **匿名**：匿名用户没有 Azure AD 标识，并且不与租户联合。 匿名参与者与外部用户类似，但其标识不会显示在会议中。 匿名用户无法访问会议窗口中的应用。 匿名用户无法在会议聊天中查看机器人徽标。 匿名用户可以是演示者或与会者，但不能是组织者。

    > [!NOTE]
    > 匿名用户继承全局默认用户级应用权限策略。 有关详细信息，请参阅 [管理应用](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access)。

## <a name="user-roles-in-teams-meeting"></a>Teams 会议中的用户角色

以下是 Teams 会议中的用户角色：

* **组织者**：组织者安排会议、设置会议选项、分配会议角色、控制与会者权限以及启动会议。 只有拥有 Microsoft 365 帐户和 Teams 许可证的用户才能成为组织者。 会议组织者可以从“ [**会议选项** ”页](https://support.microsoft.com/en-us/office/change-participant-settings-for-a-teams-meeting-53261366-dbd5-45f9-aae9-a70e6354f88e)更改特定会议的设置。

* **演示者**：会议中的演示者具有与组织者类似的功能，但从会话中删除组织者和修改会话的会议选项除外。

* **与会者**：与会者是受邀参加会议的用户。 与会者在会议期间的功能有限。

> [!NOTE]
> 只有组织者或演示者可以添加、删除或卸载应用。

有关详细信息，请参阅 [Teams 会议中的角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

> [!TIP]
>
> * [默认参与者设置](/microsoftteams/meeting-policies-participants-and-guests)由组织的 IT 管理员确定。根据默认设置，加入会议的参与者具有演示者角色。
> * 演示者角色在一对一调用中不可用。
> * 从聊天启动群组呼叫的用户被视为组织者。

> [!IMPORTANT]
>
> * 目前，第三方应用在政府社区云 (GCC) 中可用，但不适用于GCC-High和国防部 (DOD) 租户。
> * GCC 默认关闭第三方应用。 若要为 GCC 启用第三方应用，请参阅[管理应用权限策略](/microsoftteams/teams-app-permission-policies)和[管理应用](/microsoftteams/manage-apps)。

## <a name="see-also"></a>另请参阅

* [设计 Microsoft Teams 会议扩展](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [会议的“生成”选项卡](~/apps-in-teams-meetings/build-tabs-for-meeting.md)
* [为 Teams 会议阶段生成应用](build-apps-for-teams-meeting-stage.md)
* [为会议聊天构建可扩展的对话](build-extensible-conversation-for-meeting-chat.md)
* [为匿名用户生成应用](build-apps-for-anonymous-user.md)
* [会议应用 API](meeting-apps-apis.md)
* [通过 Live Share SDK 增强协作](teams-live-share-overview.md)
* [自定义全体模式场景](~/apps-in-teams-meetings/teams-together-mode.md)
