---
title: 会议应用程序扩展性
author: laujan
description: 了解会议应用程序扩展性
ms.topic: conceptual
ms.openlocfilehash: 96770a6a06d7a4478d8a00a7928c74b38d7b4b2c
ms.sourcegitcommit: 999f5c607671e088ea8a461fa7dbb63f8d61c39b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2021
ms.locfileid: "52649770"
---
# <a name="meeting-app-extensibility"></a>会议应用程序扩展性

Teams应用程序扩展性基于以下概念：

* 会议生命周期具有不同的阶段，如会议前、会中和会议后。  
* 会议有三个不同的参与者角色：组织者、演示者和与会者。 有关详细信息，请参阅[会议Teams角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。  
* 会议有 [各种](/microsoftteams/non-standard-users#:~:text=An%20anonymous%20user%20is%20a,their%20Microsoft%20or%20organization's%20account.) 用户类型：租户内用户、 [来宾](/microsoftteams/guest-access)用户、 [联盟用户](/microsoftteams/manage-external-access)和匿名用户。

本文介绍了有关会议生命周期以及如何在会议中集成选项卡、聊天机器人和消息传递扩展的信息。 它提供用于标识不同参与者角色和用于执行任务的不同用户类型的信息。

## <a name="meeting-lifecycle"></a>会议生命周期

会议生命周期由会议前、会议内和会议后应用体验组成。 可以在会议生命周期的每个阶段集成选项卡、聊天机器人和消息传递扩展。

### <a name="integrate-tabs-into-the-meeting-lifecycle"></a>将选项卡集成到会议生命周期

选项卡允许团队成员访问会议内特定空间中的服务和内容。 该团队直接与选项卡协作，并展开有关选项卡中可用的工具和数据的对话。 在Teams中，用户可以通过选择 <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>，并选择要安装的应用。

> [!IMPORTANT]
> 如果已将选项卡与会议集成，则应用必须遵循选项卡的 Teams 单一登录[ (SSO) 身份验证流](../tabs/how-to/authentication/auth-aad-sso.md)。

> [!NOTE]
> * 移动客户端仅在会议前和会议后阶段支持选项卡。 会议内对话框和面板中的会议体验当前在移动设备上不可用。
> * 应用仅在私人安排的会议中受支持。

#### <a name="pre-meeting-app-experience"></a>会议前应用体验

通过会议前应用体验，你可以查找和添加会议应用并执行会议前任务，例如开发投票以调查会议参与者。

**向现有会议添加选项卡**

1. 在日历中，选择要添加选项卡的会议。
1. 选择" **详细信息"** 选项卡并选择 <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>. 将显示选项卡库。

    ![会议前体验](../assets/images/apps-in-meetings/PreMeeting.png)

1. 在选项卡库中，选择要添加的应用并按照所需步骤操作。 应用作为选项卡安装。

    ![会议前选项卡视图](../assets/images/apps-in-meetings/PreMeetingTab.png)

    > [!NOTE]
    > * 您还可以使用现有会议中的"会议 **聊天** "选项卡添加选项卡。
    > * 如果投票或调查超过 10 个，则选项卡布局必须组织在一个状态。

#### <a name="in-meeting-app-experience"></a>会议内应用体验

借助会议内应用体验，可以使用应用和会议内对话框在会议期间与参与者互动。 会议应用程序作为会议中的选项卡托管在会议窗口的顶部栏中。使用"会议内"对话框为会议参与者展示可操作内容。 有关详细信息，请参阅[为会议创建Teams应用](create-apps-for-teams-meetings.md)。

**在会议期间使用选项卡**

1. 进入会议后，从聊天窗口的顶部栏中，选择想要使用的应用。 应用在侧面板Teams会议对话框中的"会议"对话框中可见。
1. 在"会议内"对话框中，输入你的回复作为反馈。

    ![对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

    > [!NOTE]
    > * 应用可以利用 Teams 客户端 SDK 来访问 `meetingId` 、 `userMri` 和 `frameContext` ，并适当地呈现体验。
    > * 如果成功呈现了会议内对话框，则通知你已成功下载结果。
    > * 应用清单指定希望它们显示的位置。 上下文字段用于此目的。 它还可以是共享托盘体验的一部分，但需遵循指定的设计准则。

    下图演示了会议侧面板：

    ![会议侧面板](../assets/images/apps-in-meetings/in-meeting-dialog.png)

#### <a name="post-meeting-app-experience"></a>会议后应用体验

通过会议后应用体验，你可以查看会议结果，如投票测试结果或反馈。 Select <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/> 添加选项卡并获取组织者和与会者必须采取措施的会议笔记和结果。

下图显示了 **"Contoso"** 选项卡，其中显示来自与会者的投票结果和反馈：

![会议后视图](../assets/images/apps-in-meetings/PostMeeting.png)

> [!NOTE]
> 当投票或调查多于 10 个时，必须组织选项卡布局。

### <a name="integrate-bots-into-the-meeting-lifecycle"></a>将机器人集成到会议生命周期

在群聊范围内启用的聊天机器人开始在会议中运行。 若要实现机器人，请从[生成自动程序开始](../build-your-first-app/build-bot.md)，然后继续为会议[创建Teams应用](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-references)。

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a>将消息传递扩展集成到会议生命周期

若要实现消息传递扩展，请从[构建](../messaging-extensions/how-to/create-messaging-extension.md)消息传递扩展开始，然后继续为会议[创建Teams应用](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-references)。

会议Teams可扩展性允许你根据会议中的参与者角色设计应用。

## <a name="participant-roles-in-a-meeting"></a>会议中的参与者角色

![会议参与者](../assets/images/apps-in-meetings/participant-roles.png)

默认参与者设置由组织的 IT 管理员确定。 以下是会议中的参与者角色：

* **组织者**：组织者安排会议、设置会议选项、分配会议角色和启动会议。 只有拥有 M365 帐户Teams许可证的用户才能成为组织者，并控制与会者权限。 会议组织者可以更改特定会议的设置。 组织者可以在"会议选项" **网页上进行** 这些更改。
* **演示** 者：演示者具有与排除项相同的组织者功能。 演示者无法从会话中删除组织者或修改会话的会议选项。 默认情况下，加入会议的参与者具有演示者角色。
* **与会者**：与会者是受邀参加会议但无权担任演示者的用户。 与会者可以与其他会议成员交互，但不能管理任何会议设置或共享内容。

> [!NOTE]
> 只有组织者或演示者才能添加、删除或卸载应用。

有关详细信息，请参阅[会议Teams角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

在基于会议中的参与者角色设计应用后，你可以为会议标识每个用户类型并选择他们可以访问的类型。

## <a name="user-types-in-a-meeting"></a>会议中的用户类型

> [!NOTE]
> 用户类型不包含在 **getParticipantRole** API 中。

会议中的用户类型（如组织者、演示者或与会者）可以在会议中执行其中一 [个参与者角色](#participant-roles-in-a-meeting)。

以下列表详细介绍了不同的用户类型及其辅助功能和性能：

* **租户内**：租户内用户属于组织，在租户的 AAD Azure Active Directory () 凭据。 他们通常是全职、现场或远程员工。 租户内用户可以是组织者、演示者或与会者。
* **来宾**：来宾是受邀访问组织租户中的Teams或其他资源的另一个组织的参与者。 来宾将添加到组织的 AAD，并且具有与Teams团队成员相同的功能，可以访问团队聊天、会议和文件。 来宾用户可以是组织者、演示者或与会者。 有关详细信息，请参阅 Teams 中的[来宾访问](/microsoftteams/guest-access)。
* **联盟或外部**：联盟用户是Teams组织中受邀加入会议的外部用户。 联盟用户具有联盟伙伴的有效凭据，并且由联盟Teams。 他们无法访问你的团队或组织的其他共享资源。 对于外部用户来说，来宾访问是访问团队和频道的更好选择。 有关详细信息，请参阅管理[Teams 中的外部访问](/microsoftteams/manage-external-access)。

    > [!NOTE]
    > 你的Teams用户可以在主持与其他组织的会议或聊天时添加应用。 当用户加入由其他组织托管的会议或聊天时，用户可以使用由外部用户共享的应用。 托管用户组织的数据策略以及该用户组织共享的第三方应用的数据共享做法将生效。

* **匿名**：匿名用户没有 AAD 标识，并且未与租户联盟。 匿名参与者与外部用户类似，但其身份不会在会议中预测。 匿名用户无法访问会议窗口中的应用。 匿名用户不能是组织者，但可以是演示者或与会者。

    > [!NOTE]
    > 匿名用户继承全局默认用户级别应用程序权限策略。 有关详细信息，请参阅管理 [应用](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access)。

来宾或匿名用户无法添加、删除或卸载应用。

下表提供了用户类型以及每个用户可以访问的功能：

| 用户类型 | 选项卡 | 机器人 | 消息传递扩展 | 自适应卡 | 任务模块 | 会议内的对话框 |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| 匿名用户 | 不可用 | 不可用 | 不可用 | 允许会议聊天中的交互。 | 允许通过自适应卡片在会议聊天中交互。 | 不可用 |
| 属于租户 AAD 的来宾 | 允许交互。 不允许创建、更新和删除。 | 不可用 | 不可用 | 允许会议聊天中的交互。 | 允许通过自适应卡片在会议聊天中交互。 | 可用 |
| Federated | 不可用 | 不可用 | 不可用 | 不可用 | 不可用 | 不可用 |

## <a name="see-also"></a>另请参阅

* [Tab](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [机器人](../bots/what-are-bots.md)
* [消息传递扩展](../messaging-extensions/what-are-messaging-extensions.md)
* [设计应用](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [会议应用的先决条件和 API Teams参考](create-apps-for-teams-meetings.md)