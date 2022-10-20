---
title: Teams 会议应用
author: surbhigupta
description: 本文介绍基于参与者、用户角色和应用扩展性的 Microsoft Teams 会议中的应用工作原理。
ms.topic: overview
ms.author: lajanuar
ms.localizationpriority: medium
ms.date: 04/07/2022
ms.openlocfilehash: b98204e1aec3224cad5955a1682d3d5338c47084
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615168"
---
# <a name="apps-for-teams-meetings-and-calls"></a>Teams 会议和呼叫的应用

会议可实现协作、合作、明智的沟通和共享反馈。 会议空间可以为会议生命周期的每个阶段提供用户体验。 下图提供了会议应用扩展性功能的概念：

:::image type="content" source="../assets/images/apps-in-meetings/meetingappextensibility.png" alt-text="屏幕截图显示会议应用扩展性的工作原理。":::

必须熟悉以下产品概念，才能使用 Microsoft Teams 中的应用创建自定义会议体验。

## <a name="supported-meeting-types-in-teams"></a>Teams 中支持的会议类型

Teams 支持在会议期间针对以下会议类型访问应用：

* [**计划会议**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop)：通过 Teams 日历安排的会议。
* [**计划频道会议**](https://support.microsoft.com/office/schedule-a-meeting-in-teams-943507a9-8583-4c58-b5d2-8ec8265e04e5#ID0EFBD=Desktop)：通过 Teams 公共频道安排的会议。
* [**一对一呼叫**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798)：在一对一聊天中发起的呼叫。
* [**组呼叫**](https://support.microsoft.com/office/start-a-call-from-a-chat-in-teams-f5138c9d-df4c-43d8-9cf6-53400c1a7798)：在群聊中启动的呼叫。
* [**即时会议**](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5)：Teams 日历中通过 **“立即开会”** 按钮启动的会议。
* [**网络研讨会**](https://support.microsoft.com/office/get-started-with-teams-webinars-42f3f874-22dc-4289-b53f-bbc1a69013e3)：网络研讨会通过 **“新建会议**”下拉列表下 **的“网络研讨会**”按钮启动。

详细了解 [Teams 会议、到期时间以及策略以及](/MicrosoftTeams/meeting-expiration)[会议、网络研讨会和直播活动](/microsoftteams/quick-start-meetings-live-events)。
> [!NOTE]
>
> * 计划公共频道会议的应用目前仅在 [公共开发人员预览版](../resources/dev-preview/developer-preview-intro.md)中可用。
> * 以下内容不支持应用：
>   * [公共交换电话网络 (PSTN) Teams 呼叫](/microsoftteams/cloud-voice-landing-page#public-switched-telephone-network-connectivity-options)
>   * [端到端加密的 Teams 调用](https://support.microsoft.com/office/use-end-to-end-encryption-for-teams-calls-1274b4d2-b5c5-4b24-a376-606fa6728a90)
>   * [即时频道会议](https://support.microsoft.com/office/start-an-instant-meeting-in-teams-ff95e53f-8231-4739-87fa-00b9723f4ef5)
>   * [共享频道](https://support.microsoft.com/office/what-is-a-shared-channel-in-teams-e70a8c22-fee4-4d6e-986f-9e0781d7d11d)中的会议

## <a name="meeting-lifecycle"></a>会议生命周期

会议生命周期包括会议前、会议内和会后应用体验，具体取决于用户类型和用户在 Teams 会议中的角色。

## <a name="user-types-in-teams"></a>Teams 中的用户类型

Teams 支持用户类型，例如 Teams 会议中的租户内、来宾、联合用户或外部用户。 每个用户类型都可以 [在 Teams 会议中](#user-roles-in-teams-meeting)具有一个用户角色。

> [!NOTE]
>
> 当前，当第三人称添加到一对一呼叫时，调用将提升为组调用，这意味着新会话将启动。 添加到一对一调用的应用在组调用中不可用。 但是，可以再次添加它们。

以下列表详细介绍了各种用户类型及其辅助功能：

* **租户内**：租户内用户属于组织，并在 Azure Active Directory (AAD) 中为租户提供凭据。 他们是全职、现场或远程员工。 租户内用户可以是组织者、演示者或与会者。
* **来宾：来宾** 是另一个组织的参与者，受邀访问 Teams 或组织租户中的其他资源。 来宾将添加到组织的 Azure AD，并且具有与本机团队成员相同的 Teams 功能。 他们有权访问团队聊天、会议和文件。 来宾可以是组织者、演示者或与会者。 有关详细信息，请参阅 [Teams 中的来宾访问权限](/microsoftteams/guest-access)。
* **联合用户或外部** 用户：联合用户或外部用户是另一个组织中受邀加入会议的 Teams 用户。 联合用户具有与联合合作伙伴的有效凭据，并由 Teams 授权。 他们无权访问你的 Teams 或组织中的其他共享资源。 来宾访问是外部用户有权访问 Teams 和频道的更好选择。 有关详细信息，请参阅 [管理 Teams 中的外部访问权限](/microsoftteams/manage-external-access)。

    > [!NOTE]
    > Teams 用户可以在托管会议或与其他组织聊天时添加应用。 当外部用户将应用共享到会议时，所有用户都可以访问该应用。 由该用户组织共享的第三方应用的主机组织的数据策略和数据共享做法将生效。

* **匿名**：匿名用户没有 Azure AD 标识，也不与租户联合。 匿名参与者与外部用户类似，但他们的身份不会显示在会议中。 匿名用户无法访问会议窗口中的应用。 匿名用户可以是演示者或与会者，但不能是组织者。

    > [!NOTE]
    > 匿名用户继承全局默认用户级应用权限策略。 有关详细信息，请参阅 [“管理应用](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access)”。

## <a name="user-roles-in-teams-meeting"></a>Teams 会议中的用户角色

下面是 Teams 会议中的用户角色：

* **组织者**：组织者安排会议，设置会议选项，分配会议角色，控制与会者权限，并启动会议。 只有拥有 Microsoft 365 帐户和 Teams 许可证的用户才能成为组织者。 会议组织者可以从“ [**会议选项** ”页](https://support.microsoft.com/en-us/office/change-participant-settings-for-a-teams-meeting-53261366-dbd5-45f9-aae9-a70e6354f88e)更改特定会议的设置。

* **演示者**：会议中的演示者具有与组织者类似的功能，但从会话中删除组织者和修改会话的会议选项除外。

* **与会者**：与会者是受邀参加会议的用户。 与会者在会议期间的功能有限。

> [!NOTE]
> 只有组织者或演示者才能添加、删除或卸载应用。

有关详细信息，请参阅 [Teams 会议中的角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

> [!TIP]
>
> * [默认参与者设置](/microsoftteams/meeting-policies-participants-and-guests)由组织的 IT 管理员确定。根据默认设置，加入会议的参与者具有演示者角色。
> * 演示者角色在一对一调用中不可用。
> * 从聊天启动组呼叫的用户被视为组织者。

> [!IMPORTANT]
>
> * 目前，第三方应用在政府社区云 (GCC) 中可用，但不适用于GCC-High和国防部 (DOD) 租户。
> * GCC 默认关闭第三方应用。 若要为 GCC 启用第三方应用，请参阅[管理应用权限策略](/microsoftteams/teams-app-permission-policies)和[管理应用](/microsoftteams/manage-apps)。

## <a name="see-also"></a>另请参阅

* [设计 Microsoft Teams 会议扩展](~/apps-in-teams-meetings/design/designing-apps-in-meetings.md)
* [会议的生成选项卡](~/apps-in-teams-meetings/build-tabs-for-meeting.md)
* [为 Teams 会议阶段生成应用](build-apps-for-teams-meeting-stage.md)
* [为会议聊天生成可扩展对话](build-extensible-conversation-for-meeting-chat.md)
* [为匿名用户生成应用](build-apps-for-anonymous-user.md)
* [会议应用 API](meeting-apps-apis.md)
* [通过 Live Share SDK 增强协作](teams-live-share-overview.md)
* [自定义全体模式场景](~/apps-in-teams-meetings/teams-together-mode.md)
