---
title: 应用到团队会议
author: laujan
description: 基于参与者和用户角色的团队会议中的应用程序概述
ms.topic: overview
ms.author: lajanuar
keywords: 团队应用会议用户参与者角色 api
ms.openlocfilehash: b5e649f1630ff6c4a120c4b7aefbac1f5f6df06f
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279714"
---
# <a name="apps-in-teams-meetings-preview"></a>团队会议中的应用 (预览) 

>[!IMPORTANT]
> Microsoft 团队预览版中包含的功能仅用于早期访问、测试和反馈目的。 他们可能会在公开发布之前进行更改，并且不应在生产应用程序中使用。

会议是团队中的工作效率的关键。 它们在包含和活跃的论坛中启用协作、合作、有通知的通信和共享反馈。 作为开发人员，您可以创建 [可配置的选项卡](../tabs/what-are-tabs.md#how-do-tabs-work)、 [bot](../bots/what-are-bots.md)和 [邮件扩展](../messaging-extensions/what-are-messaging-extensions.md) 应用程序，以增强和丰富团队会议体验。 会议用户可以通过选项卡库访问应用程序，以启用相关方案，如预暂存看板面板、启动会议内操作对话框或创建会议后轮询。 您的会议应用程序可以根据与会者的状态为会议生命周期的每个阶段提供用户体验。

团队的会议应用可扩展性以三个概念为中心：

✔ **会议生命周期** —在会议时间范围之前、之后和之后。  
✔ **参与者角色** （会议组织者、演示者或与会者）。  
✔ **用户类型** —租户、来宾、联合或匿名团队用户。

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a>会议生命周期方案

## <a name="tabs"></a>选项卡

> [!IMPORTANT]
> 与所有选项卡应用程序一样，您的应用程序将需要遵循针对选项卡的团队 [SSO 身份验证流](../tabs/how-to/authentication/auth-aad-sso.md) 。

### <a name="pre-meeting-app-experience"></a>预会议应用程序体验

**会议前体验：**

![会议前体验](../assets/images/apps-in-meetings/PreMeeting.png)

**"会议前" 选项卡：**

![会议前选项卡视图](../assets/images/apps-in-meetings/PreMeetingTab.png)

✔具有独特权限用户可以通过选项卡库通过以下两种方式向会议添加应用程序：

&emsp;&emsp; 通过 "团队计划" 窗体上的 " **详细信息** " 选项卡&#9679;。

&emsp;&emsp; 通过现有会议中的 "会议 **聊天** " 选项卡&#9679;。</br> </br>

✔选项卡应用程序可在会议 **详细信息** 和 **聊天** 页面中使用加号图标 (➕) "按钮。 |

### <a name="in-meeting-app-experience"></a>会议中的应用程序体验

✔会议应用程序将托管在聊天窗口顶部的上方栏中，并可通过 "会议" 选项卡中的 "会议" 选项卡体验。当用户通过选项卡库将选项卡添加到会议时，将显示 **会议体验期间** 的应用程序。

✔具有独特权限用户可以在会议中添加应用程序。

✔在会议上下文中加载时，应用程序将能够利用团队客户端 SDK 访问 `meetingId` 、 `userMri` 和，并 `frameContext` 适当地呈现体验。

可以在两个区域中的团队会议中查看应用程序的✔：

&emsp;&emsp;&#9679; **侧面板**。 </br>

> [!NOTE]
> 如果您的 _应用程序清单_ 指定选项卡是 [针对侧面板优化](create-apps-for-teams-meetings.md#in-meeting)的，则它将显示在该面板中。 它也可以是共享任务栏体验的一部分，根据指定的设计准则。

&emsp;&emsp;&#9679; **会议中的对话框**。 使用 "会议内" 对话框展示会议参与者的可操作内容。 *请参阅*[创建适用于团队的应用程序会议](create-apps-for-teams-meetings.md)。

**会议体验：**

![会议体验](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会议对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog.png)

**用户的会议中的可操作对话框：**

![对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a>会议后应用程序体验

**会议后体验：**

![会议后视图](../assets/images/apps-in-meetings/PostMeeting.png)

会议后应用场景与当前的会议后体验类似，在表面中存在带有选项卡的额外优势。 具有独特权限用户可以通过 "工作组计划" 窗体中的 " **详细信息** " 选项卡和现有会议中的 "会议 **聊天** " 选项卡，将选项卡库中的应用程序添加到会议中。

### <a name="bots"></a>机器人

对于机器人实施，请参阅 [团队会议文档中的 bot](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) 。

### <a name="messaging-extensions"></a>消息扩展

有关邮件扩展实现，请参阅我们 [的工作组会议文档中的邮件扩展](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) 。

## <a name="participant-roles-and-user-types-in-a-meeting"></a>会议中的参与者角色和用户类型

![会议中的参与者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a>参与者角色

您可以使用特定于参与者的授权来设计您的应用程序。 例如，也许只有组织者和/或演示者可以在会议中创建轮询。 尽管默认参与者设置由组织的 IT 管理员决定，但会议组织者可能需要更改特定会议的设置。 组织者可以在 "会议选项" 网页上进行这些更改。

1. **组织者**。 组织者安排会议、设置会议选项、分配会议角色并启动会议。 只有拥有团队许可证) 的 M365 (帐户的用户才可以是组织者并控制与会者权限。
1. **演示者**。 演示者与组织者的功能几乎相同;但是，演示者不能从会话中删除组织者，也不能修改会话的会议选项。 默认情况下，加入会议的参与者具有演示者角色。
1. **与会者**。 "与会者" 是受邀参加会议但无权充当演示者的用户。 与会者可以与其他会议成员进行交互，但不能管理任何会议设置或共享内容。

_请参阅_ [**团队会议中的角色**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)

您可以访问 "  **会议选项** " 页，如下所示：

在团队中 &#11200;，转到 " **日历** ![ 日历" 徽标 ](../assets/images/apps-in-meetings/calendar-logo.png) ，选择一个会议，然后选择 " **会议选项**"。

&#11200; 会议邀请中，选择 " **会议选项**"。

在会议过程中 &#11200;，请选择 "在会议控件中 **显示参与者** ![ 显示参与者图标 ](../assets/images/apps-in-meetings/show-participants.png) "。 然后，在参与者列表的上方，选择 " **管理权限**"。

### <a name="user-types"></a>用户类型

> [!NOTE]
> 用户类型可以加入会议，并假设上述参与者角色之一。 用户类型不作为 **getParticipantRole** API 的一部分公开。

1. **租户中**。 这些用户属于组织，并拥有租户的 Azure Active Directory 中的凭据。 他们通常是全职、现场或远程员工。
1. **来宾**。 来宾是来自另一个组织的参与者，受邀访问团队或组织租户中的其他资源。 将来宾添加到您的组织的 Active Directory 中，并且可以获得与本机工作组成员完全相同的工作组成员功能，并拥有对团队聊天、会议和文件的完全访问权限。 _请参阅_ [Microsoft 团队中的来宾访问](/microsoftteams/guest-access)
1. **联合/外部**。 联合用户是已被邀请加入会议的另一个组织中的外部团队用户。 由于这些用户具有联合合作伙伴的有效凭据，因此这些用户将被视为通过团队进行身份验证，但无法访问你的团队或组织中的其他共享资源。 如果您希望外部用户具有对团队和频道的访问权限，则来宾访问可能是更好的选择。 _请参阅_[在 Microsoft 团队中管理外部访问](/microsoftteams/manage-external-access)
1. **匿名**。 匿名用户不具有 Active Directory 标识，并且不与租户联合。 匿名参与者类似于外部用户，但其身份不会投影到会议中。 匿名用户将无法访问会议窗口中的应用程序。

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [创建适用于 Teams 会议的应用](create-apps-for-teams-meetings.md)
