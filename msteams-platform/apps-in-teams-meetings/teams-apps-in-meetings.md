---
title: Teams 会议中的应用
author: laujan
description: 基于参与者和用户角色的 Teams 会议中应用概述
ms.topic: overview
ms.author: lajanuar
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: 51fe2e0ebdaa56197bbebd1e5dbcf90698fb1f92
ms.sourcegitcommit: 23ed7edf145df10dcfba15c43978eae9e0d451a8
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2021
ms.locfileid: "50753551"
---
# <a name="apps-in-teams-meetings"></a>Teams 会议中的应用

会议是 Teams 工作效率的关键。 它们支持协作、合作关系、明智沟通和在非独占活动论坛中共享反馈。 作为开发人员，你可以创建[可配置的选项卡](../tabs/what-are-tabs.md#how-do-tabs-work)、机器人和[](../bots/what-are-bots.md)消息[扩展应用程序，](../messaging-extensions/what-are-messaging-extensions.md)以增强和丰富 Teams 会议体验。 会议用户可以通过选项卡库访问应用，以启用相关方案，例如预暂存看板、启动会议中的可操作对话框或创建会议后投票。 会议应用可以基于与会者状态为会议生命周期的每个阶段提供用户体验。

Teams 的会议应用扩展性以三个概念为中心：

✔ **会议生命周期** - 会议时间框架之前、期间和之后。  
✔ **参与者角色** — 会议组织者、演示者或与会者。  
✔ **用户类型** — 租户内、来宾、联盟或匿名 Teams 用户。

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a>会议生命周期方案

## <a name="tabs"></a>选项卡

> [!IMPORTANT]
> 与所有选项卡应用程序一样，你的应用将需要遵循选项卡的 Teams [SSO 身份验证](../tabs/how-to/authentication/auth-aad-sso.md) 流。

> [!NOTE]
> * 移动客户端仅在会议前和会议后支持选项卡。 即将推出会议内体验，例如移动设备上的会议内对话框和面板。
> * 应用仅在私人安排的会议中受支持。

### <a name="pre-meeting-app-experience"></a>会议前应用体验

**会议前体验：**

![会议前体验](../assets/images/apps-in-meetings/PreMeeting.png)

**"会议前"选项卡：**

![会议前选项卡视图](../assets/images/apps-in-meetings/PreMeetingTab.png)

✔权限的用户可以通过选项卡库以两种方式将应用添加到会议：

&emsp;&emsp;&#9679;通过 Teams 计划 **表单上的"** 详细信息"选项卡进行选择。

&emsp;&emsp;&#9679;通过现有会议 **中的** 会议聊天选项卡。</br> </br>

✔选项卡应用可在会议详细信息和聊天页面中使用加号图标或按钮 (➕) 访问。|

✔投票或调查数超过 10 个，则选项卡布局应具有组织状态。

### <a name="in-meeting-app-experience"></a>会议内应用体验

✔会议应用将承载在聊天窗口的顶部栏中，并且作为会议中的选项卡体验通过"会议内"选项卡托管。当用户通过选项卡库向会议添加选项卡时，将显示会议体验期间的应用。 

✔权限用户可以在会议期间添加应用。

✔在会议上下文中加载时，应用将能够利用 Teams 客户端 SDK 访问 、 和 以 `meetingId` `userMri` `frameContext` 适当呈现体验。

✔导出调查或投票的结果时，应通知用户"结果已成功下载"。

✔在 Teams 会议（有两个方面）中显示应用：

&emsp;&emsp;&#9679;**侧面板 。** </br>

> [!NOTE]
> 如果你 _的应用清单_ 指定你的选项卡已 [针对](create-apps-for-teams-meetings.md#during-a-meeting)侧面板进行了优化，则它是它的显示位置。 它还可以是共享托盘体验的一部分，但需遵循指定的设计准则。

&emsp;&emsp;**&#9679;"会议内"对话框**。 使用会议内对话框为会议参与者展示可操作内容。 *请参阅*[创建 Teams 应用会议](create-apps-for-teams-meetings.md)。

**会议体验：**

![会议内体验](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会议内对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog.png)

**适用于用户的"会议内可操作"对话框：**

![对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a>会议后应用体验

**会议后体验：**

![会议后视图](../assets/images/apps-in-meetings/PostMeeting.png)

✔会议后应用方案类似于当前的会议后体验，同时具有存在于图面中的选项卡的附加优势。 

✔权限的用户可以通过 Teams 计划表单上的"详细信息"选项卡和现有会议中的"会议聊天"选项卡将应用从选项卡库添加到会议。 

✔投票或调查数超过 10 个，则选项卡布局应具有组织状态。

### <a name="bots"></a>机器人

对于自动程序实现，首先 [构建自动](../build-your-first-app/build-bot.md) 程序，然后继续 [创建 Teams 会议应用](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。

### <a name="messaging-extensions"></a>消息扩展

对于消息传递扩展实现，首先 [构建](../messaging-extensions/how-to/create-messaging-extension.md) 消息传递扩展，然后继续 [为 Teams 会议创建应用](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。

## <a name="participant-roles-and-user-types-in-a-meeting"></a>会议的参与者角色和用户类型

![会议参与者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a>参与者角色

可以使用特定于参与者的授权设计应用。 例如，可能只有组织者和/或演示者可以在会议中创建投票。 尽管默认参与者设置由组织的 IT 管理员确定，但会议组织者可能希望更改特定会议的设置。 组织者可以在"会议选项"网页上进行这些更改。

1. **组织者**。 组织者安排会议、设置会议选项、分配会议角色和启动会议。 只有拥有 M365 帐户 (拥有 Teams 许可证) 才能成为组织者并控制与会者权限。
1. **演示者**。 演示者具有与组织者几乎相同的功能;但是，演示者无法从会话中删除组织者或修改会话的会议选项。 默认情况下，加入会议的参与者具有演示者角色。
1. **与会者**。 与会者是受邀参加会议但无权担任演示者的用户。 与会者可以与其他会议成员交互，但不能管理任何会议设置或共享内容。

_请参阅_ [ **Teams 会议的角色**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

您可以按如下  **方式访问"会议选项** "页：

&#11200; Teams 中，转到日历 ![ 日历徽标 ](../assets/images/apps-in-meetings/calendar-logo.png) ，选择会议，然后选择会议 **选项**。

&#11200;在会议邀请中，选择"**会议选项"。**

&#11200;会议期间，选择" **显示** 参与者在会议控件 ![ ](../assets/images/apps-in-meetings/show-participants.png) 中显示参与者图标"。 然后，在参与者列表上方，选择"**管理权限"。**

### <a name="user-types"></a>用户类型

> [!NOTE]
> 用户类型可以加入会议并承担上述参与者角色之一。 用户类型不会作为 **getParticipantRole** API 的一部分公开。

1. **租户内 。** 这些用户属于组织，在租户的 Azure Active Directory 中拥有凭据。 他们通常是全职、现场或远程员工。
1. **来宾**。 来宾是另一个组织的参与者，已受邀访问 Teams 或组织租户中的其他资源。 来宾将添加到组织的 Active Directory，并且几乎可以像本机团队成员一样获得所有相同的 Teams 功能，具有对团队聊天、会议和文件的完全访问权限。 _请参阅_ [Microsoft Teams 中的来宾访问](/microsoftteams/guest-access)
1. **联合/外部**。 联盟用户是另一个组织中受邀加入会议的外部 Teams 用户。 由于这些用户具有与联盟伙伴的有效凭据，因此他们将视为通过 Teams 身份验证，但无法访问你的团队或组织的其他共享资源。 如果希望外部用户能够访问团队和频道，则来宾访问可能是更好的选择。 _请参阅_[在 Microsoft Teams 中管理外部访问](/microsoftteams/manage-external-access)
1. **匿名**。 匿名用户没有 Active Directory 标识，并且未与租户联盟。 匿名参与者与外部用户类似，但其身份不会预测到会议。 匿名用户将无法访问会议窗口中的应用。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [设计应用](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
> [!div class="nextstepaction"]
> [生成应用程序](create-apps-for-teams-meetings.md)
