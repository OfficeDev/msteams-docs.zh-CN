---
title: Teams 会议中的应用
author: laujan
description: 基于参与者和用户角色的 Teams 会议中应用概述
ms.topic: overview
ms.author: lajanuar
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: 63c383f1bc7eaa92e2bd4ff378756064ee85ed70
ms.sourcegitcommit: 92fa912a51f295bb8a2dc1593a46ce103752dcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/21/2021
ms.locfileid: "49917595"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="cdddb-104">Teams 会议中的应用</span><span class="sxs-lookup"><span data-stu-id="cdddb-104">Apps in Teams meetings</span></span>

<span data-ttu-id="cdddb-105">会议是 Teams 生产力的关键。</span><span class="sxs-lookup"><span data-stu-id="cdddb-105">Meetings are key to productivity in Teams.</span></span> <span data-ttu-id="cdddb-106">它们支持协作、合作关系、明智沟通和在非独占活动论坛中共享反馈。</span><span class="sxs-lookup"><span data-stu-id="cdddb-106">They enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="cdddb-107">作为开发人员，你可以创建[可配置的选项卡](../tabs/what-are-tabs.md#how-do-tabs-work)、机器人和[](../bots/what-are-bots.md)消息[扩展应用程序，](../messaging-extensions/what-are-messaging-extensions.md)以增强和丰富 Teams 会议体验。</span><span class="sxs-lookup"><span data-stu-id="cdddb-107">As a developer, you can create [configurable tab](../tabs/what-are-tabs.md#how-do-tabs-work), [bot](../bots/what-are-bots.md), and [message extension](../messaging-extensions/what-are-messaging-extensions.md) applications to enhance and enrich a Teams meeting experience.</span></span> <span data-ttu-id="cdddb-108">会议用户可以通过选项卡库访问应用，以启用相关方案，例如预暂存看板、启动会议内可操作对话框或创建会议后轮询。</span><span class="sxs-lookup"><span data-stu-id="cdddb-108">Meeting users can access apps, via the tab gallery, to enable relevant scenarios such as pre-staging a Kanban board, launching an in-meeting actionable dialog, or creating a post-meeting poll.</span></span> <span data-ttu-id="cdddb-109">会议应用可以基于与会者状态为会议生命周期的每个阶段提供用户体验。</span><span class="sxs-lookup"><span data-stu-id="cdddb-109">Your meeting app can deliver a user experience for each stage of the meeting lifecycle based upon attendee status.</span></span>

<span data-ttu-id="cdddb-110">Teams 的会议应用扩展性以三个概念为中心：</span><span class="sxs-lookup"><span data-stu-id="cdddb-110">Teams’ meeting app extensibility centers on three concepts:</span></span>

<span data-ttu-id="cdddb-111">✔ **会议生命周期** - 会议时间框架之前、期间和之后。</span><span class="sxs-lookup"><span data-stu-id="cdddb-111">✔ **Meeting lifecycle** — before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="cdddb-112">✔ **参与者角色** — 会议组织者、演示者或与会者。</span><span class="sxs-lookup"><span data-stu-id="cdddb-112">✔ **Participant role** — meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="cdddb-113">✔ **用户类型** — 租户内、来宾、联盟或匿名 Teams 用户。</span><span class="sxs-lookup"><span data-stu-id="cdddb-113">✔ **User type** — in-tenant, guest, federated, or anonymous Teams user.</span></span>

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a><span data-ttu-id="cdddb-114">会议生命周期方案</span><span class="sxs-lookup"><span data-stu-id="cdddb-114">Meeting lifecycle scenarios</span></span>

## <a name="tabs"></a><span data-ttu-id="cdddb-115">选项卡</span><span class="sxs-lookup"><span data-stu-id="cdddb-115">Tabs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="cdddb-116">与所有选项卡应用程序一样，你的应用将需要遵循选项卡的 Teams [SSO 身份验证](../tabs/how-to/authentication/auth-aad-sso.md) 流程。</span><span class="sxs-lookup"><span data-stu-id="cdddb-116">As with all tab applications, Your app will need to follow the Teams [SSO authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> <span data-ttu-id="cdddb-117">移动客户端仅在会议前和会议后支持选项卡。</span><span class="sxs-lookup"><span data-stu-id="cdddb-117">Mobile clients support Tabs only in Pre and Post Meeting Surfaces.</span></span> <span data-ttu-id="cdddb-118">即将在移动设备上 (会议内对话框和) 面板体验</span><span class="sxs-lookup"><span data-stu-id="cdddb-118">The In-meeting experiences (in-meeting dialog and panel) on mobile will be available soon</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="cdddb-119">会议前应用体验</span><span class="sxs-lookup"><span data-stu-id="cdddb-119">Pre-meeting app experience</span></span>

<span data-ttu-id="cdddb-120">**会议前体验：**</span><span class="sxs-lookup"><span data-stu-id="cdddb-120">**Pre-meeting experience:**</span></span>

![会议前体验](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="cdddb-122">**"会议前"选项卡：**</span><span class="sxs-lookup"><span data-stu-id="cdddb-122">**Pre-meeting tab:**</span></span>

![会议前选项卡视图](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="cdddb-124">✔权限的用户可以通过两种方式通过选项卡库向会议添加应用：</span><span class="sxs-lookup"><span data-stu-id="cdddb-124">✔ Permissioned users can add apps to a meeting via the tab gallery in two ways:</span></span>

<span data-ttu-id="cdddb-125">&emsp;&emsp;&#9679; Teams 计划 **表单** 上的"详细信息"选项卡进行查看。</span><span class="sxs-lookup"><span data-stu-id="cdddb-125">&emsp;&emsp;&#9679; Via the **Details** tab on the Teams scheduling form.</span></span>

<span data-ttu-id="cdddb-126">&emsp;&emsp;&#9679;通过现有会议中的"会议 **聊天** "选项卡进行聊天。</span><span class="sxs-lookup"><span data-stu-id="cdddb-126">&emsp;&emsp;&#9679;  Via the meeting **Chat** tab in an existing meeting.</span></span></br> </br>

<span data-ttu-id="cdddb-127">✔选项卡应用可在会议详细信息和聊天页面中使用加号图标 (➕) 按钮。|</span><span class="sxs-lookup"><span data-stu-id="cdddb-127">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus icon (➕) button.|</span></span>

<span data-ttu-id="cdddb-128">✔投票或调查数超过 10 个，则选项卡布局应具有组织状态。</span><span class="sxs-lookup"><span data-stu-id="cdddb-128">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="cdddb-129">会议内应用体验</span><span class="sxs-lookup"><span data-stu-id="cdddb-129">In-meeting app experience</span></span>

<span data-ttu-id="cdddb-130">✔会议应用将托管在聊天窗口的顶部栏中，并作为会议内选项卡体验通过"会议内"选项卡托管。当用户通过选项卡库向会议添加选项卡时，将显示会议体验期间的应用。 </span><span class="sxs-lookup"><span data-stu-id="cdddb-130">✔ Meeting apps will be hosted in the top upper bar of the chat window and as in-meeting tab experience via the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences will be surfaced.</span></span>

<span data-ttu-id="cdddb-131">✔权限的用户可以在会议期间添加应用。</span><span class="sxs-lookup"><span data-stu-id="cdddb-131">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="cdddb-132">✔在会议上下文中加载时，应用将能够利用 Teams 客户端 SDK 访问 ，并适当地 `meetingId` `userMri` `frameContext` 呈现体验。</span><span class="sxs-lookup"><span data-stu-id="cdddb-132">✔ When loaded in the context of a meeting, apps will be able to leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="cdddb-133">✔调查或投票的结果时，应通知用户"已成功下载结果"。</span><span class="sxs-lookup"><span data-stu-id="cdddb-133">✔ Exporting a result of a survey or polls should notify the users stating, ‘results successfully downloaded’.</span></span>

<span data-ttu-id="cdddb-134">✔在 Teams 会议（在两个方面）中显示应用：</span><span class="sxs-lookup"><span data-stu-id="cdddb-134">✔ For an app to be visible in a Teams meeting in two areas:</span></span>

<span data-ttu-id="cdddb-135">&emsp;&emsp;&#9679; **侧面板**。</span><span class="sxs-lookup"><span data-stu-id="cdddb-135">&emsp;&emsp;&#9679; **Side panel**.</span></span> </br>

> [!NOTE]
> <span data-ttu-id="cdddb-136">如果你 _的应用清单_ 指定你的选项卡已 [针对](create-apps-for-teams-meetings.md#during-a-meeting)侧面板进行了优化，它将显示在该位置。</span><span class="sxs-lookup"><span data-stu-id="cdddb-136">If your _app manifest_ specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#during-a-meeting), that is where it will be displayed.</span></span> <span data-ttu-id="cdddb-137">它还可以是共享托盘体验的一部分，但需遵循指定的设计准则。</span><span class="sxs-lookup"><span data-stu-id="cdddb-137">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="cdddb-138">&emsp;&emsp;&#9679; **会议内对话框**。</span><span class="sxs-lookup"><span data-stu-id="cdddb-138">&emsp;&emsp;&#9679; **In-meeting dialog**.</span></span> <span data-ttu-id="cdddb-139">使用会议内对话框向会议参与者展示可操作内容。</span><span class="sxs-lookup"><span data-stu-id="cdddb-139">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="cdddb-140">*请参阅*["创建 Teams 应用"会议](create-apps-for-teams-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="cdddb-140">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

<span data-ttu-id="cdddb-141">**会议内体验：**</span><span class="sxs-lookup"><span data-stu-id="cdddb-141">**In-meeting experience:**</span></span>

![会议内体验](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会议内对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog.png)

<span data-ttu-id="cdddb-144">**适用于用户的"会议内可操作"对话框：**</span><span class="sxs-lookup"><span data-stu-id="cdddb-144">**In-meeting actionable dialog for users:**</span></span>

![对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="cdddb-146">会议后应用体验</span><span class="sxs-lookup"><span data-stu-id="cdddb-146">Post-meeting app experience</span></span>

<span data-ttu-id="cdddb-147">**会议后体验：**</span><span class="sxs-lookup"><span data-stu-id="cdddb-147">**Post-meeting experience:**</span></span>

![会议后视图](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="cdddb-149">✔会议后应用方案类似于当前的会议后体验，同时具有表存在于图面中的附加优势。</span><span class="sxs-lookup"><span data-stu-id="cdddb-149">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span> 

<span data-ttu-id="cdddb-150">✔用户可以通过 Teams 计划表单上的"详细信息"选项卡和现有会议中的"会议聊天"选项卡，将选项卡库中的应用添加到会议。 </span><span class="sxs-lookup"><span data-stu-id="cdddb-150">✔ Permissioned users can add apps from the tab gallery to a meeting via the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="cdddb-151">✔投票或调查数超过 10 个，则选项卡布局应具有组织状态。</span><span class="sxs-lookup"><span data-stu-id="cdddb-151">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="bots"></a><span data-ttu-id="cdddb-152">机器人</span><span class="sxs-lookup"><span data-stu-id="cdddb-152">Bots</span></span>

<span data-ttu-id="cdddb-153">有关机器人实现，请参阅 Teams 会议 [文档中的聊天机器人](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) 。</span><span class="sxs-lookup"><span data-stu-id="cdddb-153">For bot implementation, please see our [Bots in Teams meetings](../bots/how-to/create-a-bot-for-teams.md#bots-in-teams-meetings) documentation.</span></span>

### <a name="messaging-extensions"></a><span data-ttu-id="cdddb-154">消息扩展</span><span class="sxs-lookup"><span data-stu-id="cdddb-154">Messaging Extensions</span></span>

<span data-ttu-id="cdddb-155">有关消息传递扩展实现，请参阅 Teams 会议文档中 [的消息扩展](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) 。</span><span class="sxs-lookup"><span data-stu-id="cdddb-155">For messaging extension implementation, please see our [Messaging extensions in Teams meetings](../messaging-extensions/how-to/create-messaging-extension.md#messaging-extensions-in-teams-meetings) documentation.</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="cdddb-156">会议中的参与者角色和用户类型</span><span class="sxs-lookup"><span data-stu-id="cdddb-156">Participant roles and user types in a meeting</span></span>

![会议的参与者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="cdddb-158">参与者角色</span><span class="sxs-lookup"><span data-stu-id="cdddb-158">Participant roles</span></span>

<span data-ttu-id="cdddb-159">可以使用特定于参与者的授权设计应用。</span><span class="sxs-lookup"><span data-stu-id="cdddb-159">You can design your app with participant-specific authorization.</span></span> <span data-ttu-id="cdddb-160">例如，可能只有组织者和/或演示者可以在会议中创建投票。</span><span class="sxs-lookup"><span data-stu-id="cdddb-160">For example, perhaps only an organizer and/or presenter can create a poll in meetings.</span></span> <span data-ttu-id="cdddb-161">尽管默认参与者设置由组织的 IT 管理员确定，但会议组织者可能希望更改特定会议的设置。</span><span class="sxs-lookup"><span data-stu-id="cdddb-161">Although default participant settings are determined by an organization's IT administrator, a meeting organizer may want to change the settings for a specific meeting.</span></span> <span data-ttu-id="cdddb-162">组织者可以在"会议选项"网页上进行这些更改。</span><span class="sxs-lookup"><span data-stu-id="cdddb-162">Organizers can make these changes on the Meeting options web page.</span></span>

1. <span data-ttu-id="cdddb-163">**组织者**。</span><span class="sxs-lookup"><span data-stu-id="cdddb-163">**Organizer**.</span></span> <span data-ttu-id="cdddb-164">组织者安排会议、设置会议选项、分配会议角色和启动会议。</span><span class="sxs-lookup"><span data-stu-id="cdddb-164">The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="cdddb-165">只有拥有 M365 帐户 (拥有 Teams 许可证) 才能成为组织者和控制与会者权限。</span><span class="sxs-lookup"><span data-stu-id="cdddb-165">Only users with a M365 account (possessing a Teams license) can be organizers and control attendee permissions.</span></span>
1. <span data-ttu-id="cdddb-166">**演示者**。</span><span class="sxs-lookup"><span data-stu-id="cdddb-166">**Presenter**.</span></span> <span data-ttu-id="cdddb-167">演示者具有与组织者几乎相同的功能;但是，演示者无法从会话中删除组织者或修改会话的会议选项。</span><span class="sxs-lookup"><span data-stu-id="cdddb-167">Presenters have nearly the same capabilities as organizer; however, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="cdddb-168">默认情况下，加入会议的参与者具有演示者角色。</span><span class="sxs-lookup"><span data-stu-id="cdddb-168">By default, participants joining a meeting have the presenter role.</span></span>
1. <span data-ttu-id="cdddb-169">**与会者**。</span><span class="sxs-lookup"><span data-stu-id="cdddb-169">**Attendee**.</span></span> <span data-ttu-id="cdddb-170">与会者是受邀参加会议但无权担任演示者的用户。</span><span class="sxs-lookup"><span data-stu-id="cdddb-170">An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="cdddb-171">与会者可以与其他会议成员交互，但不能管理任何会议设置或共享内容。</span><span class="sxs-lookup"><span data-stu-id="cdddb-171">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="cdddb-172">_查看_ [ **Teams 会议的角色**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="cdddb-172">_See_ [**Roles in a Teams meeting**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span></span>

<span data-ttu-id="cdddb-173">您可以按如下  **方式访问"会议选项** "页：</span><span class="sxs-lookup"><span data-stu-id="cdddb-173">You can access the  **Meeting options** page as follows:</span></span>

<span data-ttu-id="cdddb-174">&#11200; Teams 中，转到 **"日历** ![ "日历徽标， ](../assets/images/apps-in-meetings/calendar-logo.png) 选择会议，然后选择 **"会议"选项**。</span><span class="sxs-lookup"><span data-stu-id="cdddb-174">&#11200; In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

<span data-ttu-id="cdddb-175">&#11200;在会议邀请中，选择 **"会议选项"。**</span><span class="sxs-lookup"><span data-stu-id="cdddb-175">&#11200; In a meeting invitation, select **Meeting options**.</span></span>

<span data-ttu-id="cdddb-176">&#11200;会议期间，选择"在会议控件中显示参与者 ![ ](../assets/images/apps-in-meetings/show-participants.png) 显示参与者"图标。</span><span class="sxs-lookup"><span data-stu-id="cdddb-176">&#11200; During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="cdddb-177">然后，在参与者列表上方，选择 **"管理权限"。**</span><span class="sxs-lookup"><span data-stu-id="cdddb-177">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="cdddb-178">用户类型</span><span class="sxs-lookup"><span data-stu-id="cdddb-178">User types</span></span>

> [!NOTE]
> <span data-ttu-id="cdddb-179">用户类型可以加入会议并假定上述参与者角色之一。</span><span class="sxs-lookup"><span data-stu-id="cdddb-179">User types can join meetings and assume one of the participant roles described above.</span></span> <span data-ttu-id="cdddb-180">用户类型不会作为 **getParticipantRole** API 的一部分公开。</span><span class="sxs-lookup"><span data-stu-id="cdddb-180">The User type is not exposed as part of the **getParticipantRole** API.</span></span>

1. <span data-ttu-id="cdddb-181">**租户内 。**</span><span class="sxs-lookup"><span data-stu-id="cdddb-181">**In-tenant**.</span></span> <span data-ttu-id="cdddb-182">这些用户属于组织，并且具有租户的 Azure Active Directory 中的凭据。</span><span class="sxs-lookup"><span data-stu-id="cdddb-182">These users belong to the organization and have credentials in Azure Active Directory for the tenant.</span></span> <span data-ttu-id="cdddb-183">他们通常是全职、现场或远程员工。</span><span class="sxs-lookup"><span data-stu-id="cdddb-183">They are usually full-time, onsite or remote employees.</span></span>
1. <span data-ttu-id="cdddb-184">**来宾**。</span><span class="sxs-lookup"><span data-stu-id="cdddb-184">**Guest**.</span></span> <span data-ttu-id="cdddb-185">来宾是另一个组织的参与者，该参与者受邀访问贵组织租户中的 Teams 或其他资源。</span><span class="sxs-lookup"><span data-stu-id="cdddb-185">A guest is a participant from another organization who has been invited to access Teams or other resources in your organization's tenant.</span></span> <span data-ttu-id="cdddb-186">来宾已添加到组织的 Active Directory，并且几乎可以像本机团队成员一样获得与本机团队成员相同的 Teams 功能，这些成员具有团队聊天、会议和文件的完全访问权限。</span><span class="sxs-lookup"><span data-stu-id="cdddb-186">Guests are added to your organization’s Active Directory and can be given nearly all the same Teams capabilities as a native team member with full access to team chats, meetings, and files.</span></span> <span data-ttu-id="cdddb-187">_请参阅_ [Microsoft Teams 中的来宾访问](/microsoftteams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="cdddb-187">_See_ [Guest access in Microsoft Teams](/microsoftteams/guest-access)</span></span>
1. <span data-ttu-id="cdddb-188">**联合/外部**。</span><span class="sxs-lookup"><span data-stu-id="cdddb-188">**Federated/External**.</span></span> <span data-ttu-id="cdddb-189">联盟用户是另一个组织中受邀加入会议的外部 Teams 用户。</span><span class="sxs-lookup"><span data-stu-id="cdddb-189">A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="cdddb-190">由于这些用户具有与联盟伙伴的有效凭据，因此他们将被视为通过 Teams 身份验证，但无法访问你的团队或组织的其他共享资源。</span><span class="sxs-lookup"><span data-stu-id="cdddb-190">Since these users have valid credentials with federated partners, they are treated as authenticated by Teams but do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="cdddb-191">如果希望外部用户能够访问团队和频道，则来宾访问可能是更好的选择。</span><span class="sxs-lookup"><span data-stu-id="cdddb-191">If you want external users to have access to teams and channels, guest access might be a better option.</span></span> <span data-ttu-id="cdddb-192">_请参阅_["在 Microsoft Teams 中管理外部访问"](/microsoftteams/manage-external-access)</span><span class="sxs-lookup"><span data-stu-id="cdddb-192">_See_ [Manage external access in Microsoft Teams](/microsoftteams/manage-external-access)</span></span>
1. <span data-ttu-id="cdddb-193">**匿名**。</span><span class="sxs-lookup"><span data-stu-id="cdddb-193">**Anonymous**.</span></span> <span data-ttu-id="cdddb-194">匿名用户没有 Active Directory 标识，并且未与租户联盟。</span><span class="sxs-lookup"><span data-stu-id="cdddb-194">Anonymous users do not have an Active Directory identity and are not federated with a tenant.</span></span> <span data-ttu-id="cdddb-195">匿名参与者与外部用户类似，但他们的标识不会预测到会议中。</span><span class="sxs-lookup"><span data-stu-id="cdddb-195">The anonymous participant is like an external user, but their identity is not projected into the meeting.</span></span> <span data-ttu-id="cdddb-196">匿名用户将无法在会议窗口中访问应用。</span><span class="sxs-lookup"><span data-stu-id="cdddb-196">Anonymous users will not be able to access apps in a meeting window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="cdddb-197">后续步骤</span><span class="sxs-lookup"><span data-stu-id="cdddb-197">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="cdddb-198">设计应用</span><span class="sxs-lookup"><span data-stu-id="cdddb-198">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="cdddb-199">生成应用程序</span><span class="sxs-lookup"><span data-stu-id="cdddb-199">Build your app</span></span>](create-apps-for-teams-meetings.md)
