---
title: 团队会议中的应用
author: laujan
description: 基于参与者和用户角色的团队会议中的应用程序概述
ms.topic: overview
ms.author: lajanuar
keywords: 团队应用会议用户参与者角色 api
ms.openlocfilehash: db14049d3150eaaa9634b4fa535a989528b1c6a2
ms.sourcegitcommit: e70d41ae793a407fdbb71bc79ef7b67b40386c96
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/19/2020
ms.locfileid: "49358019"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="c5536-104">团队会议中的应用</span><span class="sxs-lookup"><span data-stu-id="c5536-104">Apps in Teams meetings</span></span>

<span data-ttu-id="c5536-105">会议是团队中的工作效率的关键。</span><span class="sxs-lookup"><span data-stu-id="c5536-105">Meetings are key to productivity in Teams.</span></span> <span data-ttu-id="c5536-106">它们在包含和活跃的论坛中启用协作、合作、有通知的通信和共享反馈。</span><span class="sxs-lookup"><span data-stu-id="c5536-106">They enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="c5536-107">作为开发人员，您可以创建 [可配置的选项卡](../tabs/what-are-tabs.md#how-do-tabs-work)、 [bot](../bots/what-are-bots.md)和 [邮件扩展](../messaging-extensions/what-are-messaging-extensions.md) 应用程序，以增强和丰富团队会议体验。</span><span class="sxs-lookup"><span data-stu-id="c5536-107">As a developer, you can create [configurable tab](../tabs/what-are-tabs.md#how-do-tabs-work), [bot](../bots/what-are-bots.md), and [message extension](../messaging-extensions/what-are-messaging-extensions.md) applications to enhance and enrich a Teams meeting experience.</span></span> <span data-ttu-id="c5536-108">会议用户可以通过选项卡库访问应用程序，以启用相关方案，如预暂存看板面板、启动会议内操作对话框或创建会议后轮询。</span><span class="sxs-lookup"><span data-stu-id="c5536-108">Meeting users can access apps, via the tab gallery, to enable relevant scenarios such as pre-staging a Kanban board, launching an in-meeting actionable dialog, or creating a post-meeting poll.</span></span> <span data-ttu-id="c5536-109">您的会议应用程序可以根据与会者的状态为会议生命周期的每个阶段提供用户体验。</span><span class="sxs-lookup"><span data-stu-id="c5536-109">Your meeting app can deliver a user experience for each stage of the meeting lifecycle based upon attendee status.</span></span>

<span data-ttu-id="c5536-110">团队的会议应用可扩展性以三个概念为中心：</span><span class="sxs-lookup"><span data-stu-id="c5536-110">Teams’ meeting app extensibility centers on three concepts:</span></span>

<span data-ttu-id="c5536-111">✔ **会议生命周期** —在会议时间范围之前、之后和之后。</span><span class="sxs-lookup"><span data-stu-id="c5536-111">✔ **Meeting lifecycle** — before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="c5536-112">✔ **参与者角色** （会议组织者、演示者或与会者）。</span><span class="sxs-lookup"><span data-stu-id="c5536-112">✔ **Participant role** — meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="c5536-113">✔ **用户类型** —租户、来宾、联合或匿名团队用户。</span><span class="sxs-lookup"><span data-stu-id="c5536-113">✔ **User type** — in-tenant, guest, federated, or anonymous Teams user.</span></span>

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a><span data-ttu-id="c5536-114">会议生命周期方案</span><span class="sxs-lookup"><span data-stu-id="c5536-114">Meeting lifecycle scenarios</span></span>

## <a name="tabs"></a><span data-ttu-id="c5536-115">选项卡</span><span class="sxs-lookup"><span data-stu-id="c5536-115">Tabs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c5536-116">与所有选项卡应用程序一样，您的应用程序将需要遵循针对选项卡的团队 [SSO 身份验证流](../tabs/how-to/authentication/auth-aad-sso.md) 。</span><span class="sxs-lookup"><span data-stu-id="c5536-116">As with all tab applications, Your app will need to follow the Teams [SSO authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> <span data-ttu-id="c5536-117">移动客户端仅支持准备会议和投递会议表面中的选项卡。</span><span class="sxs-lookup"><span data-stu-id="c5536-117">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="c5536-118">在会议中 (会议中的对话和面板) 的会议体验将很快可用</span><span class="sxs-lookup"><span data-stu-id="c5536-118">The In-meeting experiences (in-meeting dialog and panel) on mobile will be available soon</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="c5536-119">预会议应用程序体验</span><span class="sxs-lookup"><span data-stu-id="c5536-119">Pre-meeting app experience</span></span>

<span data-ttu-id="c5536-120">**会议前体验：**</span><span class="sxs-lookup"><span data-stu-id="c5536-120">**Pre-meeting experience:**</span></span>

![会议前体验](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="c5536-122">**"会议前" 选项卡：**</span><span class="sxs-lookup"><span data-stu-id="c5536-122">**Pre-meeting tab:**</span></span>

![会议前选项卡视图](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="c5536-124">✔具有独特权限用户可以通过选项卡库通过以下两种方式向会议添加应用程序：</span><span class="sxs-lookup"><span data-stu-id="c5536-124">✔ Permissioned users can add apps to a meeting via the tab gallery in two ways:</span></span>

<span data-ttu-id="c5536-125">&emsp;&emsp; 通过 "团队计划" 窗体上的 " **详细信息** " 选项卡&#9679;。</span><span class="sxs-lookup"><span data-stu-id="c5536-125">&emsp;&emsp;&#9679; Via the **Details** tab on the Teams scheduling form.</span></span>

<span data-ttu-id="c5536-126">&emsp;&emsp; 通过现有会议中的 "会议 **聊天** " 选项卡&#9679;。</span><span class="sxs-lookup"><span data-stu-id="c5536-126">&emsp;&emsp;&#9679;  Via the meeting **Chat** tab in an existing meeting.</span></span></br> </br>

<span data-ttu-id="c5536-127">✔选项卡应用程序可在会议 **详细信息** 和 **聊天** 页面中使用加号图标 (➕) "按钮。 |</span><span class="sxs-lookup"><span data-stu-id="c5536-127">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus icon (➕) button.|</span></span>

<span data-ttu-id="c5536-128">如果有10个以上的轮询或调查，✔选项卡布局应处于已组织状态。</span><span class="sxs-lookup"><span data-stu-id="c5536-128">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="c5536-129">会议中的应用程序体验</span><span class="sxs-lookup"><span data-stu-id="c5536-129">In-meeting app experience</span></span>

<span data-ttu-id="c5536-130">✔会议应用程序将托管在聊天窗口顶部的上方栏中，并可通过 "会议" 选项卡中的 "会议" 选项卡体验。当用户通过选项卡库将选项卡添加到会议时，将显示 **会议体验期间** 的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c5536-130">✔ Meeting apps will be hosted in the top upper bar of the chat window and as in-meeting tab experience via the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences will be surfaced.</span></span>

<span data-ttu-id="c5536-131">✔具有独特权限用户可以在会议中添加应用程序。</span><span class="sxs-lookup"><span data-stu-id="c5536-131">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="c5536-132">✔在会议上下文中加载时，应用程序将能够利用团队客户端 SDK 访问 `meetingId` 、 `userMri` 和，并 `frameContext` 适当地呈现体验。</span><span class="sxs-lookup"><span data-stu-id="c5536-132">✔ When loaded in the context of a meeting, apps will be able to leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="c5536-133">✔导出调查结果或轮询的结果应通知用户声明 "结果已成功下载"。</span><span class="sxs-lookup"><span data-stu-id="c5536-133">✔ Exporting a result of a survey or polls should notify the users stating, ‘results successfully downloaded’.</span></span>

<span data-ttu-id="c5536-134">✔要在两个区域中的团队会议中显示的应用程序：</span><span class="sxs-lookup"><span data-stu-id="c5536-134">✔ For an app to be visible in a Teams meeting in two areas:</span></span>

<span data-ttu-id="c5536-135">&emsp;&emsp;&#9679; **侧面板**。</span><span class="sxs-lookup"><span data-stu-id="c5536-135">&emsp;&emsp;&#9679; **Side panel**.</span></span> </br>

> [!NOTE]
> <span data-ttu-id="c5536-136">如果您的 _应用程序清单_ 指定选项卡是 [针对侧面板优化](create-apps-for-teams-meetings.md#in-meeting)的，则它将显示在该面板中。</span><span class="sxs-lookup"><span data-stu-id="c5536-136">If your _app manifest_ specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#in-meeting), that is where it will be displayed.</span></span> <span data-ttu-id="c5536-137">它也可以是共享任务栏体验的一部分，根据指定的设计准则。</span><span class="sxs-lookup"><span data-stu-id="c5536-137">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="c5536-138">&emsp;&emsp;&#9679; **会议中的对话框**。</span><span class="sxs-lookup"><span data-stu-id="c5536-138">&emsp;&emsp;&#9679; **In-meeting dialog**.</span></span> <span data-ttu-id="c5536-139">使用 "会议内" 对话框展示会议参与者的可操作内容。</span><span class="sxs-lookup"><span data-stu-id="c5536-139">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="c5536-140">*请参阅*[创建适用于团队的应用程序会议](create-apps-for-teams-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="c5536-140">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

<span data-ttu-id="c5536-141">**会议体验：**</span><span class="sxs-lookup"><span data-stu-id="c5536-141">**In-meeting experience:**</span></span>

![会议体验](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会议对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog.png)

<span data-ttu-id="c5536-144">**用户的会议中的可操作对话框：**</span><span class="sxs-lookup"><span data-stu-id="c5536-144">**In-meeting actionable dialog for users:**</span></span>

![对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="c5536-146">会议后应用程序体验</span><span class="sxs-lookup"><span data-stu-id="c5536-146">Post-meeting app experience</span></span>

<span data-ttu-id="c5536-147">**会议后体验：**</span><span class="sxs-lookup"><span data-stu-id="c5536-147">**Post-meeting experience:**</span></span>

![会议后视图](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="c5536-149">✔后会议应用程序方案与当前的会议后体验类似，其中增加了包含在表面中存在的选项卡的好处。</span><span class="sxs-lookup"><span data-stu-id="c5536-149">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span> 

<span data-ttu-id="c5536-150">✔具有独特权限用户可以通过 "团队计划" 窗体上的 " **详细信息** " 选项卡和现有会议中的 "会议 **聊天** " 选项卡，将选项卡库中的应用程序添加到会议。</span><span class="sxs-lookup"><span data-stu-id="c5536-150">✔ Permissioned users can add apps from the tab gallery to a meeting via the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="c5536-151">如果有10个以上的轮询或调查，✔选项卡布局应处于已组织状态。</span><span class="sxs-lookup"><span data-stu-id="c5536-151">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="bots"></a><span data-ttu-id="c5536-152">机器人</span><span class="sxs-lookup"><span data-stu-id="c5536-152">Bots</span></span>

<span data-ttu-id="c5536-153">对于机器人实施，请参阅 [团队会议文档中的 bot](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) 。</span><span class="sxs-lookup"><span data-stu-id="c5536-153">For bot implementation, please see our [Bots in Teams meetings](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) documentation.</span></span>

### <a name="messaging-extensions"></a><span data-ttu-id="c5536-154">消息扩展</span><span class="sxs-lookup"><span data-stu-id="c5536-154">Messaging Extensions</span></span>

<span data-ttu-id="c5536-155">有关邮件扩展实现，请参阅我们 [的工作组会议文档中的邮件扩展](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) 。</span><span class="sxs-lookup"><span data-stu-id="c5536-155">For messaging extension implementation, please see our [Messaging extensions in Teams meetings](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) documentation.</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="c5536-156">会议中的参与者角色和用户类型</span><span class="sxs-lookup"><span data-stu-id="c5536-156">Participant roles and user types in a meeting</span></span>

![会议中的参与者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="c5536-158">参与者角色</span><span class="sxs-lookup"><span data-stu-id="c5536-158">Participant roles</span></span>

<span data-ttu-id="c5536-159">您可以使用特定于参与者的授权来设计您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c5536-159">You can design your app with participant-specific authorization.</span></span> <span data-ttu-id="c5536-160">例如，也许只有组织者和/或演示者可以在会议中创建轮询。</span><span class="sxs-lookup"><span data-stu-id="c5536-160">For example, perhaps only an organizer and/or presenter can create a poll in meetings.</span></span> <span data-ttu-id="c5536-161">尽管默认参与者设置由组织的 IT 管理员决定，但会议组织者可能需要更改特定会议的设置。</span><span class="sxs-lookup"><span data-stu-id="c5536-161">Although default participant settings are determined by an organization's IT administrator, a meeting organizer may want to change the settings for a specific meeting.</span></span> <span data-ttu-id="c5536-162">组织者可以在 "会议选项" 网页上进行这些更改。</span><span class="sxs-lookup"><span data-stu-id="c5536-162">Organizers can make these changes on the Meeting options web page.</span></span>

1. <span data-ttu-id="c5536-163">**组织者**。</span><span class="sxs-lookup"><span data-stu-id="c5536-163">**Organizer**.</span></span> <span data-ttu-id="c5536-164">组织者安排会议、设置会议选项、分配会议角色并启动会议。</span><span class="sxs-lookup"><span data-stu-id="c5536-164">The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="c5536-165">只有拥有团队许可证) 的 M365 (帐户的用户才可以是组织者并控制与会者权限。</span><span class="sxs-lookup"><span data-stu-id="c5536-165">Only users with a M365 account (possessing a Teams license) can be organizers and control attendee permissions.</span></span>
1. <span data-ttu-id="c5536-166">**演示者**。</span><span class="sxs-lookup"><span data-stu-id="c5536-166">**Presenter**.</span></span> <span data-ttu-id="c5536-167">演示者与组织者的功能几乎相同;但是，演示者不能从会话中删除组织者，也不能修改会话的会议选项。</span><span class="sxs-lookup"><span data-stu-id="c5536-167">Presenters have nearly the same capabilities as organizer; however, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="c5536-168">默认情况下，加入会议的参与者具有演示者角色。</span><span class="sxs-lookup"><span data-stu-id="c5536-168">By default, participants joining a meeting have the presenter role.</span></span>
1. <span data-ttu-id="c5536-169">**与会者**。</span><span class="sxs-lookup"><span data-stu-id="c5536-169">**Attendee**.</span></span> <span data-ttu-id="c5536-170">"与会者" 是受邀参加会议但无权充当演示者的用户。</span><span class="sxs-lookup"><span data-stu-id="c5536-170">An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="c5536-171">与会者可以与其他会议成员进行交互，但不能管理任何会议设置或共享内容。</span><span class="sxs-lookup"><span data-stu-id="c5536-171">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="c5536-172">_请参阅_ [**团队会议中的角色**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="c5536-172">_See_ [**Roles in a Teams meeting**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span></span>

<span data-ttu-id="c5536-173">您可以访问 "  **会议选项** " 页，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c5536-173">You can access the  **Meeting options** page as follows:</span></span>

<span data-ttu-id="c5536-174">在团队中 &#11200;，转到 " **日历** ![ 日历" 徽标 ](../assets/images/apps-in-meetings/calendar-logo.png) ，选择一个会议，然后选择 " **会议选项**"。</span><span class="sxs-lookup"><span data-stu-id="c5536-174">&#11200; In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

<span data-ttu-id="c5536-175">&#11200; 会议邀请中，选择 " **会议选项**"。</span><span class="sxs-lookup"><span data-stu-id="c5536-175">&#11200; In a meeting invitation, select **Meeting options**.</span></span>

<span data-ttu-id="c5536-176">在会议过程中 &#11200;，请选择 "在会议控件中 **显示参与者** ![ 显示参与者图标 ](../assets/images/apps-in-meetings/show-participants.png) "。</span><span class="sxs-lookup"><span data-stu-id="c5536-176">&#11200; During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="c5536-177">然后，在参与者列表的上方，选择 " **管理权限**"。</span><span class="sxs-lookup"><span data-stu-id="c5536-177">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="c5536-178">用户类型</span><span class="sxs-lookup"><span data-stu-id="c5536-178">User types</span></span>

> [!NOTE]
> <span data-ttu-id="c5536-179">用户类型可以加入会议，并假设上述参与者角色之一。</span><span class="sxs-lookup"><span data-stu-id="c5536-179">User types can join meetings and assume one of the participant roles described above.</span></span> <span data-ttu-id="c5536-180">用户类型不作为 **getParticipantRole** API 的一部分公开。</span><span class="sxs-lookup"><span data-stu-id="c5536-180">The User type is not exposed as part of the **getParticipantRole** API.</span></span>

1. <span data-ttu-id="c5536-181">**租户中**。</span><span class="sxs-lookup"><span data-stu-id="c5536-181">**In-tenant**.</span></span> <span data-ttu-id="c5536-182">这些用户属于组织，并拥有租户的 Azure Active Directory 中的凭据。</span><span class="sxs-lookup"><span data-stu-id="c5536-182">These users belong to the organization and have credentials in Azure Active Directory for the tenant.</span></span> <span data-ttu-id="c5536-183">他们通常是全职、现场或远程员工。</span><span class="sxs-lookup"><span data-stu-id="c5536-183">They are usually full-time, onsite or remote employees.</span></span>
1. <span data-ttu-id="c5536-184">**来宾**。</span><span class="sxs-lookup"><span data-stu-id="c5536-184">**Guest**.</span></span> <span data-ttu-id="c5536-185">来宾是来自另一个组织的参与者，受邀访问团队或组织租户中的其他资源。</span><span class="sxs-lookup"><span data-stu-id="c5536-185">A guest is a participant from another organization who has been invited to access Teams or other resources in your organization's tenant.</span></span> <span data-ttu-id="c5536-186">将来宾添加到您的组织的 Active Directory 中，并且可以获得与本机工作组成员完全相同的工作组成员功能，并拥有对团队聊天、会议和文件的完全访问权限。</span><span class="sxs-lookup"><span data-stu-id="c5536-186">Guests are added to your organization’s Active Directory and can be given nearly all the same Teams capabilities as a native team member with full access to team chats, meetings, and files.</span></span> <span data-ttu-id="c5536-187">_请参阅_ [Microsoft 团队中的来宾访问](/microsoftteams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="c5536-187">_See_ [Guest access in Microsoft Teams](/microsoftteams/guest-access)</span></span>
1. <span data-ttu-id="c5536-188">**联合/外部**。</span><span class="sxs-lookup"><span data-stu-id="c5536-188">**Federated/External**.</span></span> <span data-ttu-id="c5536-189">联合用户是已被邀请加入会议的另一个组织中的外部团队用户。</span><span class="sxs-lookup"><span data-stu-id="c5536-189">A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="c5536-190">由于这些用户具有联合合作伙伴的有效凭据，因此这些用户将被视为通过团队进行身份验证，但无法访问你的团队或组织中的其他共享资源。</span><span class="sxs-lookup"><span data-stu-id="c5536-190">Since these users have valid credentials with federated partners, they are treated as authenticated by Teams but do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="c5536-191">如果您希望外部用户具有对团队和频道的访问权限，则来宾访问可能是更好的选择。</span><span class="sxs-lookup"><span data-stu-id="c5536-191">If you want external users to have access to teams and channels, guest access might be a better option.</span></span> <span data-ttu-id="c5536-192">_请参阅_[在 Microsoft 团队中管理外部访问](/microsoftteams/manage-external-access)</span><span class="sxs-lookup"><span data-stu-id="c5536-192">_See_ [Manage external access in Microsoft Teams](/microsoftteams/manage-external-access)</span></span>
1. <span data-ttu-id="c5536-193">**匿名**。</span><span class="sxs-lookup"><span data-stu-id="c5536-193">**Anonymous**.</span></span> <span data-ttu-id="c5536-194">匿名用户不具有 Active Directory 标识，并且不与租户联合。</span><span class="sxs-lookup"><span data-stu-id="c5536-194">Anonymous users do not have an Active Directory identity and are not federated with a tenant.</span></span> <span data-ttu-id="c5536-195">匿名参与者类似于外部用户，但其身份不会投影到会议中。</span><span class="sxs-lookup"><span data-stu-id="c5536-195">The anonymous participant is like an external user, but their identity is not projected into the meeting.</span></span> <span data-ttu-id="c5536-196">匿名用户将无法访问会议窗口中的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c5536-196">Anonymous users will not be able to access apps in a meeting window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="c5536-197">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c5536-197">Next Steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c5536-198">创建适用于 Teams 会议的应用</span><span class="sxs-lookup"><span data-stu-id="c5536-198">Create apps for Teams meetings</span></span>](create-apps-for-teams-meetings.md)
