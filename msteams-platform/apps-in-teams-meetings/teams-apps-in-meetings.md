---
title: Teams 会议中的应用
author: laujan
description: 基于参与者和用户角色的 Teams 会议中应用概述
ms.topic: overview
ms.author: lajanuar
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: ac4e270090dd89d370d37de88b8cba552b77a5cb
ms.sourcegitcommit: 3727fc58e84b6f1752612884c2e0b25e207fb56e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/26/2021
ms.locfileid: "51382336"
---
# <a name="apps-in-teams-meetings"></a>Teams 会议中的应用

会议支持协作、合作关系、明智沟通和在非独占活动论坛中共享反馈。 会议应用可以针对会议生命周期的每个阶段提供用户体验，包括会议前、会议内和会议后应用体验，具体取决于与会者的状态。

Teams 最终用户可以在会议期间使用选项卡库访问应用，例如：

* 预阶段看板
* 启动会议内可操作对话框
* 创建会议后轮询

Teams 的会议应用扩展性基于以下概念：

✔会议生命周期具有阶段，如会议时间框架之前、期间和之后。  
✔会议的参与者角色，例如会议组织者、演示者或与会者。  
✔用户类型在会议中，如租户内、来宾、联盟或匿名 Teams 用户。

本文介绍了有关会议生命周期以及如何在会议中集成选项卡、聊天机器人和消息传递扩展的信息。 它还允许您标识参与者角色，并使用不同的用户类型执行任务。

> [!NOTE]
> 若要使用会议应用程序扩展性功能，您必须具有相应的权限。

### <a name="meeting-lifecycle"></a>会议生命周期

会议生命周期由会议前、会议内和会议后应用体验组成。 可以在会议生命周期的每个阶段集成选项卡、聊天机器人和消息传递扩展。

## <a name="integrate-tabs-into-the-meeting-lifecycle"></a>将选项卡集成到会议生命周期

利用选项卡，团队成员可以访问频道或聊天内特定空间中的服务和内容。 这使团队可以直接使用选项卡，并展开有关选项卡中可用的工具和数据的对话。 在 Teams 会议中，用户可以通过选择加号添加选项卡 <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/>，并选择要作为选项卡安装的应用。

> [!IMPORTANT]
> 如果你已将选项卡与会议集成，则你的应用必须遵循 Teams 单一登录 ([SSO](../tabs/how-to/authentication/auth-aad-sso.md)) 选项卡的身份验证流。

> [!NOTE]
> * 移动客户端仅在会议前和会议后阶段支持选项卡。 会议内对话框和面板中的会议体验当前在移动设备上不可用。
> * 应用仅在私人安排的会议中受支持。

### <a name="pre-meeting-app-experience"></a>会议前应用体验

**会议前体验：**

![会议前体验](../assets/images/apps-in-meetings/PreMeeting.png)

**"会议前"选项卡：**

![会议前选项卡视图](../assets/images/apps-in-meetings/PreMeetingTab.png)

✔权限的用户是可以在会议生命周期的不同阶段向会议添加应用的用户。 这些用户可以使用两种方式通过选项卡库向会议添加应用：

   * 使用 **Teams** 计划表单上的"详细信息"选项卡。

   * 使用现有 **会议** 中的"会议聊天"选项卡。

✔选项卡应用可通过会议"详细信息"和"聊天 **"** 页面使用加号按钮➕访问。

✔投票或调查数超过 10 个，则选项卡布局必须组织在一个状态。

### <a name="in-meeting-app-experience"></a>会议内应用体验

✔会议应用程序承载在聊天窗口的顶部栏中，并且作为使用"会议内"选项卡的会议内选项卡体验托管。当用户通过选项卡库向会议添加选项卡时，将显示会议 **体验期间** 的应用。

✔权限用户可以在会议期间添加应用。

✔在会议上下文中加载时，应用可以利用 Teams 客户端 SDK 访问 、 和 `meetingId` 以 `userMri` `frameContext` 适当呈现体验。

✔导出调查或投票的结果会通知用户结果已成功下载。

✔在 Teams 会议侧面板或会议内对话框中显示应用。 使用会议内对话框为会议参与者展示可操作内容。 *请参阅*[创建 Teams 应用会议](create-apps-for-teams-meetings.md)。

   > [!NOTE]
   > 应用清单指定你的选项卡已 [针对](create-apps-for-teams-meetings.md#during-a-meeting)侧面板进行了优化，即它的显示位置。 它还可以是共享托盘体验的一部分，但需遵循指定的设计准则。

以下图像将应用显示为会议中的对话框和单独的侧面板：

![会议内体验](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会议内对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog.png)

#### <a name="in-meeting-actionable-dialog-for-users"></a>用户的"会议内可操作"对话框

![对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a>会议后应用体验

![会议后视图](../assets/images/apps-in-meetings/PostMeeting.png)

✔会议后应用方案类似于当前的会议后体验，同时具有存在于图面中的选项卡的附加优势。

✔权限用户可以使用 Teams 计划表单上的"详细信息"选项卡和现有会议中的"会议聊天"选项卡，将选项卡库中的应用添加到会议。

✔投票或调查数超过 10 次时，必须组织选项卡布局。

### <a name="integrate-bots-into-the-meeting-lifecycle"></a>将机器人集成到会议生命周期

对于自动程序实现，首先 [构建自动](../build-your-first-app/build-bot.md) 程序，然后继续 [创建 Teams 会议应用](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a>将消息传递扩展集成到会议生命周期

对于消息传递扩展实现，首先 [构建](../messaging-extensions/how-to/create-messaging-extension.md) 消息传递扩展，然后继续 [为 Teams 会议创建应用](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。

## <a name="participant-roles-and-user-types-in-a-meeting"></a>会议的参与者角色和用户类型

![会议参与者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a>参与者角色

默认参与者设置由组织的 IT 管理员确定。 以下是会议中的参与者角色：

* **组织者**：组织者安排会议、设置会议选项、分配会议角色和启动会议。 只有拥有具有 Teams 许可证的 M365 帐户的用户才能是组织者和控制与会者权限。 会议组织者可以更改特定会议的设置。 组织者可以在"会议选项" **网页上进行** 这些更改。
* **演示** 者：演示者具有与组织者相同的功能。 但是，演示者无法从会话中删除组织者或修改会话的会议选项。 默认情况下，加入会议的参与者具有演示者角色。
* **与会者**：与会者是受邀参加会议但无权担任演示者的用户。 与会者可以与其他会议成员交互，但不能管理任何会议设置或共享内容。

只有组织者或演示者才能添加、删除或卸载应用。 只有组织者或演示者可以在会议创建投票。

有关详细信息，请参阅 [Teams 会议中的角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。

您可以按如下  **方式访问"会议选项** "页：

* 在 Teams 中，转到 **日历** ![ 日历徽标 ](../assets/images/apps-in-meetings/calendar-logo.png) ，选择会议，然后选择会议 **选项**。

* 在会议邀请中，选择"**会议选项"。**

* 在会议期间，选择 **"显示参与者** ![ 在会议控件 ](../assets/images/apps-in-meetings/show-participants.png) 中显示参与者图标"。 然后，在参与者列表上方，选择"**管理权限"。**

### <a name="user-types"></a>用户类型

> [!NOTE]
> 分配了特定用户类型的用户可以加入会议，并承担参与者角色中所述的参与者 [角色之一](#participant-roles)。 用户类型不包含在 **getParticipantRole** API 中。

以下用户类型标识每个用户可以执行哪些操作以及可以访问哪些内容：

* **租户内**：租户内用户属于组织，拥有租户的 Azure Active Directory (AAD) 凭据。 他们通常是全职、现场或远程员工。 租户内用户可以是组织者、演示者或与会者。
* **来宾**：来宾是受邀访问组织租户中的 Teams 或其他资源的另一个组织的参与者。 来宾将添加到组织的 AAD，并且具有与本机团队成员相同的 Teams 功能，可以访问团队聊天、会议和文件。 来宾用户可以是组织者、演示者或与会者。 有关详细信息，请参阅 Teams [中的来宾访问](/microsoftteams/guest-access)。
* **联盟或外部**：联盟用户是另一个组织中受邀加入会议的外部 Teams 用户。 这些用户具有联盟伙伴的有效凭据，并且由 Teams 授权。 他们无法访问你的团队或组织的其他共享资源。 对于外部用户来说，来宾访问是访问团队和频道的更好选择。 有关详细信息，请参阅在 [Teams 中管理外部访问](/microsoftteams/manage-external-access)。
* **匿名**：匿名用户没有 AAD 标识，并且未与租户联盟。 匿名参与者与外部用户类似，但其身份不会在会议中预测。 匿名用户无法访问会议窗口中的应用。 匿名用户不能是组织者，但可以是演示者或与会者。

## <a name="see-also"></a>另请参阅

> [!div class="nextstepaction"]
> [Tab](../tabs/what-are-tabs.md#how-do-tabs-work)

> [!div class="nextstepaction"]
> [Bot](../bots/what-are-bots.md)

> [!div class="nextstepaction"]
> [消息传递扩展](../messaging-extensions/what-are-messaging-extensions.md)

> [!div class="nextstepaction"]
> [设计应用](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [生成应用程序](create-apps-for-teams-meetings.md)
