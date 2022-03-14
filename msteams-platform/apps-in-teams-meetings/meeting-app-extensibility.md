---
title: 统一会议应用
author: surbhigupta
description: 了解会议生命周期、在桌面和移动环境中构建用户在整个会议生命周期中的会议体验、参与者角色和用户类型。 此外，了解如何在会议生命周期中集成机器人和消息传递扩展。
ms.topic: conceptual
ms.localizationpriority: none
ms.openlocfilehash: 01b24c96e19f11fe32ac511bc1c3f091f23b6cfb
ms.sourcegitcommit: ca902f505a125641c379a917ee745ab418bd1ce6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/14/2022
ms.locfileid: "63466476"
---
# <a name="unified-meetings-apps"></a>统一会议应用

Teams统一会议应用基于以下概念：

* 会议生命周期具有不同的阶段: 会议前、会议内和会议后。  
* 会议中有三个不同的参与者角色: 组织者、演示者和与会者。 有关详细信息，请参阅[会议Teams角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。  
* 会议有 [各种](/microsoftteams/non-standard-users#:~:text=An%20anonymous%20user%20is%20a,their%20Microsoft%20or%20organization's%20account.) 用户类型：租户内用户、 [来宾](/microsoftteams/guest-access)用户、 [联盟](/microsoftteams/manage-external-access)用户和匿名用户。

本文介绍了有关会议生命周期以及如何集成选项卡、机器人和消息传递扩展的信息。 它标识不同的参与者角色和用户类型。

## <a name="meeting-lifecycle"></a>会议生命周期

会议生命周期包括会议前、会议内和会议后应用体验。 可以在会议生命周期的每个阶段集成选项卡、机器人和消息传递扩展。

### <a name="integrate-tabs-into-the-meeting-lifecycle"></a>将选项卡集成到会议生命周期

选项卡允许团队成员访问会议中特定空间内的服务和内容。 团队直接使用选项卡，并就选项卡中可用的工具和数据进行对话。 在Teams中，可以通过选择 <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>，然后选择要安装的应用。

> [!IMPORTANT]
> 如果已将选项卡与会议集成，则应用必须遵循Teams SSO (单一) [身份验证流](../tabs/how-to/authentication/auth-aad-sso.md)。

> [!NOTE]
>
> * 专用计划会议仅支持应用。
> * 在 Web 客户端Teams会议扩展选项卡应用的添加Teams选项。

#### <a name="pre-meeting-app-experience"></a>会议前应用体验

通过会议前应用体验，你可以查找和添加会议应用。 你还可以执行会议前任务，例如发起投票以调查会议参与者。

若要向现有会议添加选项卡：

1. 在日历中，选择要添加选项卡的会议。
1. 选择" **详细信息"** 选项卡并选择 <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. 将显示选项卡库。

    :::image type="content" source="~/assets/images/apps-in-meetings/Pre-Meeting-002.png" alt-text="会议前应用体验":::

1. 在选项卡库中，选择要添加的应用并按照所需步骤操作。 应用作为选项卡安装。

   > [!NOTE]
   >
   > * 您还可以使用"会议聊天"选项卡向现有会议 **添加** 选项卡。
   > * 如果投票或调查超过 10 个，则选项卡布局必须组织在一个状态。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="~/assets/images/apps-in-meetings/PreMeetingTab.png" alt-text="会议期间的选项卡":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

将选项卡添加到移动设备上的现有会议后，可以在会议详细信息的"更多部分"下看到会议前体验中的相同应用。

<img src="../assets/images/apps-in-meetings/mobilePostMeeting.png" alt="Mobile pre-meeting experience" width="200"/>  

---

#### <a name="in-meeting-app-experience"></a>会议内应用体验

借助会议内应用体验，可以在会议期间通过使用应用和会议中的对话框来吸引与会者。 会议应用作为会议内选项卡托管在会议窗口的工具栏上。使用会议内对话框为会议参与者展示可操作的内容。 有关详细信息，请参阅[为会议启用和配置Teams应用](enable-and-configure-your-app-for-teams-meetings.md)。

对于移动版，会议应用可从会议>省略号 &#x25CF;&#x25CF;&#x25CF; 提供。 选择 **"** 应用"以查看会议提供的所有应用。

在会议期间使用选项卡：

1. 转到Teams。
1. 在日历中，选择要使用选项卡的会议。
1. 进入会议后，从聊天窗口的工具栏中选择所需的应用。
    应用在侧面板Teams会议对话框中的"会议"对话框中可见。
1. 在"会议内"对话框中，输入你的回复作为反馈。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

# <a name="mobile"></a>[移动设备](#tab/mobile)

进入会议并添加桌面或 Web 中的应用后，该应用在移动Teams应用程序部分 **下可见**。 选择 **"** 应用"以显示应用列表。 用户可以启动任何应用作为应用的会议侧面板。

将显示"会议内"对话框，可在其中输入作为反馈的响应。

<img src="../assets/images/apps-in-meetings/mobile-in-meeting-dialog-view.png" alt="Mobile dialog box view" width="200"/>

> [!NOTE]
> 无需更改应用清单，应用就适用于移动设备。

---

> [!NOTE]
>
> * 应用可以利用 Teams 客户端 SDK 来访问 `meetingId`、 `userMri`和 `frameContext` ，并适当地呈现体验。
> * 如果成功呈现会议内对话框，则它会发送成功下载结果的通知。
> * 应用清单指定希望应用显示的位置。 可通过在清单中指定上下文字段来完成此操作。 它还属于共享会议阶段体验的一部分，但需遵循指定的 [设计准则](~\apps-in-teams-meetings\design\designing-apps-in-meetings.md)。

下图演示了会议侧面板：

# <a name="desktop"></a>[桌面设备](#tab/desktop)

![会议侧面板](../assets/images/in-meeting-dialog.png)

# <a name="mobile"></a>[移动设备](#tab/mobile)

<img src="../assets/images/apps-in-meetings/sidepanelmobile.png" alt="In-meeting side panel mobile" width="300"/>

---

下表介绍了应用在验证和未验证时的行为：

|应用功能 | 验证应用 | 应用未验证 |
|---|---|---|
| 会议可扩展性 | 该应用将显示在会议中。 | 该应用不会在移动客户端的会议中显示。 |

有关详细信息，请参阅 [应用商店验证指南](../concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)。

#### <a name="post-meeting-app-experience"></a>会议后应用体验

通过会议后应用体验，可以查看会议结果，如投票调查结果或反馈。 选择 <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/> 添加选项卡，获取会议笔记，并查看组织者和与会者必须采取措施的结果。

下图显示了 **"Contoso** "选项卡，其中显示来自与会者的投票结果和反馈：

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="~/assets/images/apps-in-meetings/post.png" alt-text="包含结果的 Contoso 选项卡":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

:::image type="content" source="~/assets/images/apps-in-meetings/mobilepremeeting.png" alt-text="会议后应用体验":::

---

> [!NOTE]
> 当有 10 多个投票或调查时，必须组织选项卡布局。

### <a name="integrate-bots-into-the-meeting-lifecycle"></a>将机器人集成到会议生命周期

在群聊范围内启用的聊天机器人开始在会议中运行。 若要实现机器人，请首先[构建自动](../build-your-first-app/build-bot.md)程序，然后继续[创建用于](../apps-in-teams-meetings/API-references.md#meeting-apps-api-references)会议Teams应用。

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a>将消息传递扩展集成到会议生命周期

若要实现消息传递扩展，请首先构建[](../messaging-extensions/how-to/create-messaging-extension.md)消息传递扩展，然后继续创建用于会议Teams[应用](../apps-in-teams-meetings/API-references.md#meeting-apps-api-references)。

通过Teams会议应用，你可以根据会议中的参与者角色设计应用。

## <a name="participant-roles-in-a-meeting"></a>会议中的参与者角色

:::image type="content" source="~/assets/images/apps-in-meetings/participant-roles.png" alt-text="会议中的参与者角色":::

默认参与者设置由组织的 IT 管理员确定。 以下是会议中的参与者角色：

* **组织者**：组织者安排会议、设置会议选项、分配会议角色和启动会议。 拥有Microsoft 365和Teams的用户只能是组织者，并且只能控制与会者权限。 会议组织者可以更改特定会议的设置。 组织者可以在"会议选项" **网页上进行** 这些更改。
* **演示** 者：演示者具有组织者的相同功能，但排除在一起。 演示者无法从会话中删除组织者或修改会话的会议选项。 默认情况下，加入会议的参与者具有演示者角色。
* **与会者**：与会者是受邀参加会议的用户。 但与会者无权担任演示者。 与会者可以与其他会议成员交互，但不能管理任何会议设置或共享内容。

> [!NOTE]
> 只有组织者或演示者才能添加、删除或卸载应用。

有关详细信息，请参阅[会议Teams角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

在基于会议中的参与者角色设计应用后，你可以为会议标识每个用户类型并选择他们可以访问的类型。

## <a name="user-types-in-a-meeting"></a>会议中的用户类型

会议中的组织者、演示者或与会者等用户类型可在会议中担任 [参与者角色之一](#participant-roles-in-a-meeting)。

> [!NOTE]
> 用户类型不包含在 **getParticipantRole** API 中。

以下列表详细介绍了各种用户类型及其辅助功能和性能：

* **租户内**：租户内用户属于组织，拥有租户Microsoft Azure Active Directory (Azure AD) 凭据。 他们是全职、现场或远程员工。 租户内用户可以是组织者、演示者或与会者。
* **来宾**：来宾是受邀访问组织租户中的Teams或其他资源的另一个组织的参与者。 来宾将添加到组织的Azure AD，并且具有Teams团队成员的相同功能。 他们有权访问团队聊天、会议和文件。 来宾可以是组织者、演示者或与会者。 有关详细信息，请参阅 Teams 中的[来宾Teams](/microsoftteams/guest-access)。
* **联盟用户或** 外部用户：联盟用户是Teams组织中受邀加入会议的外部用户。 联盟用户具有联盟伙伴的有效凭据，并且由联盟Teams。 他们无法访问你的团队或组织的其他共享资源。 对于外部用户来说，来宾访问是访问团队和频道的更好选择。 有关详细信息，请参阅管理 [Teams 中的外部访问](/microsoftteams/manage-external-access)。

    > [!NOTE]
    > 你的Teams用户可以在主持与其他组织的会议或聊天时添加应用。 当用户加入由其他组织托管的会议或聊天时，用户可以使用由外部用户共享的应用。 托管用户组织的数据策略以及该用户组织共享的第三方应用的数据共享做法将生效。

    > [!IMPORTANT]
    > 目前，第三方应用在 政府社区云 (GCC) 中可用，但不适用于 GCC-High 和国防部 (DOD) 。 默认情况下，对于第三方应用，GCC。 若要打开第三方应用GCC，请参阅[管理应用权限策略](/microsoftteams/teams-app-permission-policies)[和管理应用](/microsoftteams/manage-apps)。

* **匿名**：匿名用户没有Azure AD身份，并且未与租户联盟。 匿名参与者与外部用户类似，但其身份不会显示在会议中。 匿名用户无法访问会议窗口中的应用。 匿名用户不能是组织者，但可以是演示者或与会者。

    > [!NOTE]
    > 匿名用户继承全局默认用户级别应用程序权限策略。 有关详细信息，请参阅 [管理应用](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access)。

来宾或匿名用户无法添加、删除或卸载应用。

下表提供了用户类型并列出了每个用户可以访问的功能：

| 用户类型 | 选项卡 | 机器人 | 消息传递扩展 | 自适应卡 | 任务模块 | 会议内的对话框 | 会议阶段 | 内容气泡 |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| 匿名用户 | 不可用 | 不可用 | 不可用 | 允许会议聊天中的交互。 | 允许通过自适应卡片在会议聊天中交互。 | 不可用 | 可在会议阶段查看应用并与之交互 | 不可用 |
| 来宾，租户租户的一Azure AD | 允许交互。 不允许创建、更新和删除。 | 不可用 | 不可用 | 允许会议聊天中的交互。 | 允许通过自适应卡片在会议聊天中交互。 | 可用 | 可以在会议阶段启动、查看应用并与之交互 | 可用 |
| 联合用户有关详细信息，请参阅 [非标准用户](/microsoftteams/non-standard-users)。 | 允许交互。 不允许创建、更新和删除。 | 允许交互。 不允许获取、更新和删除。 | 不可用 | 允许会议聊天中的交互。 | 允许通过自适应卡片在会议聊天中交互。 | 不可用 | 可以在会议阶段启动、查看应用并与之交互 | 不可用 |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [为会议启用和配置Teams应用](enable-and-configure-your-app-for-teams-meetings.md)

## <a name="see-also"></a>另请参阅

* [Tab](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [Bot](../bots/what-are-bots.md)
* [消息传递扩展](../messaging-extensions/what-are-messaging-extensions.md)
* [设计应用](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
