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
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="a02e8-104">Teams 会议中的应用</span><span class="sxs-lookup"><span data-stu-id="a02e8-104">Apps in Teams meetings</span></span>

<span data-ttu-id="a02e8-105">会议是 Teams 工作效率的关键。</span><span class="sxs-lookup"><span data-stu-id="a02e8-105">Meetings are key to productivity in Teams.</span></span> <span data-ttu-id="a02e8-106">它们支持协作、合作关系、明智沟通和在非独占活动论坛中共享反馈。</span><span class="sxs-lookup"><span data-stu-id="a02e8-106">They enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="a02e8-107">作为开发人员，你可以创建[可配置的选项卡](../tabs/what-are-tabs.md#how-do-tabs-work)、机器人和[](../bots/what-are-bots.md)消息[扩展应用程序，](../messaging-extensions/what-are-messaging-extensions.md)以增强和丰富 Teams 会议体验。</span><span class="sxs-lookup"><span data-stu-id="a02e8-107">As a developer, you can create [configurable tab](../tabs/what-are-tabs.md#how-do-tabs-work), [bot](../bots/what-are-bots.md), and [message extension](../messaging-extensions/what-are-messaging-extensions.md) applications to enhance and enrich a Teams meeting experience.</span></span> <span data-ttu-id="a02e8-108">会议用户可以通过选项卡库访问应用，以启用相关方案，例如预暂存看板、启动会议中的可操作对话框或创建会议后投票。</span><span class="sxs-lookup"><span data-stu-id="a02e8-108">Meeting users can access apps, via the tab gallery, to enable relevant scenarios such as pre-staging a Kanban board, launching an in-meeting actionable dialog, or creating a post-meeting poll.</span></span> <span data-ttu-id="a02e8-109">会议应用可以基于与会者状态为会议生命周期的每个阶段提供用户体验。</span><span class="sxs-lookup"><span data-stu-id="a02e8-109">Your meeting app can deliver a user experience for each stage of the meeting lifecycle based upon attendee status.</span></span>

<span data-ttu-id="a02e8-110">Teams 的会议应用扩展性以三个概念为中心：</span><span class="sxs-lookup"><span data-stu-id="a02e8-110">Teams’ meeting app extensibility centers on three concepts:</span></span>

<span data-ttu-id="a02e8-111">✔ **会议生命周期** - 会议时间框架之前、期间和之后。</span><span class="sxs-lookup"><span data-stu-id="a02e8-111">✔ **Meeting lifecycle** — before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="a02e8-112">✔ **参与者角色** — 会议组织者、演示者或与会者。</span><span class="sxs-lookup"><span data-stu-id="a02e8-112">✔ **Participant role** — meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="a02e8-113">✔ **用户类型** — 租户内、来宾、联盟或匿名 Teams 用户。</span><span class="sxs-lookup"><span data-stu-id="a02e8-113">✔ **User type** — in-tenant, guest, federated, or anonymous Teams user.</span></span>

<!-- markdownlint-disable MD001 -->
### <a name="meeting-lifecycle-scenarios"></a><span data-ttu-id="a02e8-114">会议生命周期方案</span><span class="sxs-lookup"><span data-stu-id="a02e8-114">Meeting lifecycle scenarios</span></span>

## <a name="tabs"></a><span data-ttu-id="a02e8-115">选项卡</span><span class="sxs-lookup"><span data-stu-id="a02e8-115">Tabs</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a02e8-116">与所有选项卡应用程序一样，你的应用将需要遵循选项卡的 Teams [SSO 身份验证](../tabs/how-to/authentication/auth-aad-sso.md) 流。</span><span class="sxs-lookup"><span data-stu-id="a02e8-116">As with all tab applications, Your app will need to follow the Teams [SSO authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> * <span data-ttu-id="a02e8-117">移动客户端仅在会议前和会议后支持选项卡。</span><span class="sxs-lookup"><span data-stu-id="a02e8-117">Mobile clients support tabs only in pre-meeting and post-meeting surfaces.</span></span> <span data-ttu-id="a02e8-118">即将推出会议内体验，例如移动设备上的会议内对话框和面板。</span><span class="sxs-lookup"><span data-stu-id="a02e8-118">The in-meeting experiences, such as in-meeting dialog and panel on mobile will be available soon.</span></span>
> * <span data-ttu-id="a02e8-119">应用仅在私人安排的会议中受支持。</span><span class="sxs-lookup"><span data-stu-id="a02e8-119">Apps are supported only in private scheduled meetings.</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="a02e8-120">会议前应用体验</span><span class="sxs-lookup"><span data-stu-id="a02e8-120">Pre-meeting app experience</span></span>

<span data-ttu-id="a02e8-121">**会议前体验：**</span><span class="sxs-lookup"><span data-stu-id="a02e8-121">**Pre-meeting experience:**</span></span>

![会议前体验](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="a02e8-123">**"会议前"选项卡：**</span><span class="sxs-lookup"><span data-stu-id="a02e8-123">**Pre-meeting tab:**</span></span>

![会议前选项卡视图](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="a02e8-125">✔权限的用户可以通过选项卡库以两种方式将应用添加到会议：</span><span class="sxs-lookup"><span data-stu-id="a02e8-125">✔ Permissioned users can add apps to a meeting via the tab gallery in two ways:</span></span>

<span data-ttu-id="a02e8-126">&emsp;&emsp;&#9679;通过 Teams 计划 **表单上的"** 详细信息"选项卡进行选择。</span><span class="sxs-lookup"><span data-stu-id="a02e8-126">&emsp;&emsp;&#9679; Via the **Details** tab on the Teams scheduling form.</span></span>

<span data-ttu-id="a02e8-127">&emsp;&emsp;&#9679;通过现有会议 **中的** 会议聊天选项卡。</span><span class="sxs-lookup"><span data-stu-id="a02e8-127">&emsp;&emsp;&#9679;  Via the meeting **Chat** tab in an existing meeting.</span></span></br> </br>

<span data-ttu-id="a02e8-128">✔选项卡应用可在会议详细信息和聊天页面中使用加号图标或按钮 (➕) 访问。|</span><span class="sxs-lookup"><span data-stu-id="a02e8-128">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus icon (➕) button.|</span></span>

<span data-ttu-id="a02e8-129">✔投票或调查数超过 10 个，则选项卡布局应具有组织状态。</span><span class="sxs-lookup"><span data-stu-id="a02e8-129">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="a02e8-130">会议内应用体验</span><span class="sxs-lookup"><span data-stu-id="a02e8-130">In-meeting app experience</span></span>

<span data-ttu-id="a02e8-131">✔会议应用将承载在聊天窗口的顶部栏中，并且作为会议中的选项卡体验通过"会议内"选项卡托管。当用户通过选项卡库向会议添加选项卡时，将显示会议体验期间的应用。 </span><span class="sxs-lookup"><span data-stu-id="a02e8-131">✔ Meeting apps will be hosted in the top upper bar of the chat window and as in-meeting tab experience via the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences will be surfaced.</span></span>

<span data-ttu-id="a02e8-132">✔权限用户可以在会议期间添加应用。</span><span class="sxs-lookup"><span data-stu-id="a02e8-132">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="a02e8-133">✔在会议上下文中加载时，应用将能够利用 Teams 客户端 SDK 访问 、 和 以 `meetingId` `userMri` `frameContext` 适当呈现体验。</span><span class="sxs-lookup"><span data-stu-id="a02e8-133">✔ When loaded in the context of a meeting, apps will be able to leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="a02e8-134">✔导出调查或投票的结果时，应通知用户"结果已成功下载"。</span><span class="sxs-lookup"><span data-stu-id="a02e8-134">✔ Exporting a result of a survey or polls should notify the users stating, ‘results successfully downloaded’.</span></span>

<span data-ttu-id="a02e8-135">✔在 Teams 会议（有两个方面）中显示应用：</span><span class="sxs-lookup"><span data-stu-id="a02e8-135">✔ For an app to be visible in a Teams meeting in two areas:</span></span>

<span data-ttu-id="a02e8-136">&emsp;&emsp;&#9679;**侧面板 。**</span><span class="sxs-lookup"><span data-stu-id="a02e8-136">&emsp;&emsp;&#9679; **Side panel**.</span></span> </br>

> [!NOTE]
> <span data-ttu-id="a02e8-137">如果你 _的应用清单_ 指定你的选项卡已 [针对](create-apps-for-teams-meetings.md#during-a-meeting)侧面板进行了优化，则它是它的显示位置。</span><span class="sxs-lookup"><span data-stu-id="a02e8-137">If your _app manifest_ specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#during-a-meeting), that is where it will be displayed.</span></span> <span data-ttu-id="a02e8-138">它还可以是共享托盘体验的一部分，但需遵循指定的设计准则。</span><span class="sxs-lookup"><span data-stu-id="a02e8-138">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="a02e8-139">&emsp;&emsp;**&#9679;"会议内"对话框**。</span><span class="sxs-lookup"><span data-stu-id="a02e8-139">&emsp;&emsp;&#9679; **In-meeting dialog**.</span></span> <span data-ttu-id="a02e8-140">使用会议内对话框为会议参与者展示可操作内容。</span><span class="sxs-lookup"><span data-stu-id="a02e8-140">Use the in-meeting dialog to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="a02e8-141">*请参阅*[创建 Teams 应用会议](create-apps-for-teams-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="a02e8-141">*See* [Create Apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

<span data-ttu-id="a02e8-142">**会议体验：**</span><span class="sxs-lookup"><span data-stu-id="a02e8-142">**In-meeting experience:**</span></span>

![会议内体验](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会议内对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog.png)

<span data-ttu-id="a02e8-145">**适用于用户的"会议内可操作"对话框：**</span><span class="sxs-lookup"><span data-stu-id="a02e8-145">**In-meeting actionable dialog for users:**</span></span>

![对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="a02e8-147">会议后应用体验</span><span class="sxs-lookup"><span data-stu-id="a02e8-147">Post-meeting app experience</span></span>

<span data-ttu-id="a02e8-148">**会议后体验：**</span><span class="sxs-lookup"><span data-stu-id="a02e8-148">**Post-meeting experience:**</span></span>

![会议后视图](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="a02e8-150">✔会议后应用方案类似于当前的会议后体验，同时具有存在于图面中的选项卡的附加优势。</span><span class="sxs-lookup"><span data-stu-id="a02e8-150">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span> 

<span data-ttu-id="a02e8-151">✔权限的用户可以通过 Teams 计划表单上的"详细信息"选项卡和现有会议中的"会议聊天"选项卡将应用从选项卡库添加到会议。 </span><span class="sxs-lookup"><span data-stu-id="a02e8-151">✔ Permissioned users can add apps from the tab gallery to a meeting via the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="a02e8-152">✔投票或调查数超过 10 个，则选项卡布局应具有组织状态。</span><span class="sxs-lookup"><span data-stu-id="a02e8-152">✔  Tab layout should be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="bots"></a><span data-ttu-id="a02e8-153">机器人</span><span class="sxs-lookup"><span data-stu-id="a02e8-153">Bots</span></span>

<span data-ttu-id="a02e8-154">对于自动程序实现，首先 [构建自动](../build-your-first-app/build-bot.md) 程序，然后继续 [创建 Teams 会议应用](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="a02e8-154">For bot implementation, start with [build a bot](../build-your-first-app/build-bot.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

### <a name="messaging-extensions"></a><span data-ttu-id="a02e8-155">消息扩展</span><span class="sxs-lookup"><span data-stu-id="a02e8-155">Messaging extensions</span></span>

<span data-ttu-id="a02e8-156">对于消息传递扩展实现，首先 [构建](../messaging-extensions/how-to/create-messaging-extension.md) 消息传递扩展，然后继续 [为 Teams 会议创建应用](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="a02e8-156">For messaging extension implementation, start with [build a messaging extension](../messaging-extensions/how-to/create-messaging-extension.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="a02e8-157">会议的参与者角色和用户类型</span><span class="sxs-lookup"><span data-stu-id="a02e8-157">Participant roles and user types in a meeting</span></span>

![会议参与者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="a02e8-159">参与者角色</span><span class="sxs-lookup"><span data-stu-id="a02e8-159">Participant roles</span></span>

<span data-ttu-id="a02e8-160">可以使用特定于参与者的授权设计应用。</span><span class="sxs-lookup"><span data-stu-id="a02e8-160">You can design your app with participant-specific authorization.</span></span> <span data-ttu-id="a02e8-161">例如，可能只有组织者和/或演示者可以在会议中创建投票。</span><span class="sxs-lookup"><span data-stu-id="a02e8-161">For example, perhaps only an organizer and/or presenter can create a poll in meetings.</span></span> <span data-ttu-id="a02e8-162">尽管默认参与者设置由组织的 IT 管理员确定，但会议组织者可能希望更改特定会议的设置。</span><span class="sxs-lookup"><span data-stu-id="a02e8-162">Although default participant settings are determined by an organization's IT administrator, a meeting organizer may want to change the settings for a specific meeting.</span></span> <span data-ttu-id="a02e8-163">组织者可以在"会议选项"网页上进行这些更改。</span><span class="sxs-lookup"><span data-stu-id="a02e8-163">Organizers can make these changes on the Meeting options web page.</span></span>

1. <span data-ttu-id="a02e8-164">**组织者**。</span><span class="sxs-lookup"><span data-stu-id="a02e8-164">**Organizer**.</span></span> <span data-ttu-id="a02e8-165">组织者安排会议、设置会议选项、分配会议角色和启动会议。</span><span class="sxs-lookup"><span data-stu-id="a02e8-165">The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="a02e8-166">只有拥有 M365 帐户 (拥有 Teams 许可证) 才能成为组织者并控制与会者权限。</span><span class="sxs-lookup"><span data-stu-id="a02e8-166">Only users with a M365 account (possessing a Teams license) can be organizers and control attendee permissions.</span></span>
1. <span data-ttu-id="a02e8-167">**演示者**。</span><span class="sxs-lookup"><span data-stu-id="a02e8-167">**Presenter**.</span></span> <span data-ttu-id="a02e8-168">演示者具有与组织者几乎相同的功能;但是，演示者无法从会话中删除组织者或修改会话的会议选项。</span><span class="sxs-lookup"><span data-stu-id="a02e8-168">Presenters have nearly the same capabilities as organizer; however, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="a02e8-169">默认情况下，加入会议的参与者具有演示者角色。</span><span class="sxs-lookup"><span data-stu-id="a02e8-169">By default, participants joining a meeting have the presenter role.</span></span>
1. <span data-ttu-id="a02e8-170">**与会者**。</span><span class="sxs-lookup"><span data-stu-id="a02e8-170">**Attendee**.</span></span> <span data-ttu-id="a02e8-171">与会者是受邀参加会议但无权担任演示者的用户。</span><span class="sxs-lookup"><span data-stu-id="a02e8-171">An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="a02e8-172">与会者可以与其他会议成员交互，但不能管理任何会议设置或共享内容。</span><span class="sxs-lookup"><span data-stu-id="a02e8-172">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="a02e8-173">_请参阅_ [ **Teams 会议的角色**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span><span class="sxs-lookup"><span data-stu-id="a02e8-173">_See_ [**Roles in a Teams meeting**](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)</span></span>

<span data-ttu-id="a02e8-174">您可以按如下  **方式访问"会议选项** "页：</span><span class="sxs-lookup"><span data-stu-id="a02e8-174">You can access the  **Meeting options** page as follows:</span></span>

<span data-ttu-id="a02e8-175">&#11200; Teams 中，转到日历 ![ 日历徽标 ](../assets/images/apps-in-meetings/calendar-logo.png) ，选择会议，然后选择会议 **选项**。</span><span class="sxs-lookup"><span data-stu-id="a02e8-175">&#11200; In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

<span data-ttu-id="a02e8-176">&#11200;在会议邀请中，选择"**会议选项"。**</span><span class="sxs-lookup"><span data-stu-id="a02e8-176">&#11200; In a meeting invitation, select **Meeting options**.</span></span>

<span data-ttu-id="a02e8-177">&#11200;会议期间，选择" **显示** 参与者在会议控件 ![ ](../assets/images/apps-in-meetings/show-participants.png) 中显示参与者图标"。</span><span class="sxs-lookup"><span data-stu-id="a02e8-177">&#11200; During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="a02e8-178">然后，在参与者列表上方，选择"**管理权限"。**</span><span class="sxs-lookup"><span data-stu-id="a02e8-178">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="a02e8-179">用户类型</span><span class="sxs-lookup"><span data-stu-id="a02e8-179">User types</span></span>

> [!NOTE]
> <span data-ttu-id="a02e8-180">用户类型可以加入会议并承担上述参与者角色之一。</span><span class="sxs-lookup"><span data-stu-id="a02e8-180">User types can join meetings and assume one of the participant roles described above.</span></span> <span data-ttu-id="a02e8-181">用户类型不会作为 **getParticipantRole** API 的一部分公开。</span><span class="sxs-lookup"><span data-stu-id="a02e8-181">The User type is not exposed as part of the **getParticipantRole** API.</span></span>

1. <span data-ttu-id="a02e8-182">**租户内 。**</span><span class="sxs-lookup"><span data-stu-id="a02e8-182">**In-tenant**.</span></span> <span data-ttu-id="a02e8-183">这些用户属于组织，在租户的 Azure Active Directory 中拥有凭据。</span><span class="sxs-lookup"><span data-stu-id="a02e8-183">These users belong to the organization and have credentials in Azure Active Directory for the tenant.</span></span> <span data-ttu-id="a02e8-184">他们通常是全职、现场或远程员工。</span><span class="sxs-lookup"><span data-stu-id="a02e8-184">They are usually full-time, onsite or remote employees.</span></span>
1. <span data-ttu-id="a02e8-185">**来宾**。</span><span class="sxs-lookup"><span data-stu-id="a02e8-185">**Guest**.</span></span> <span data-ttu-id="a02e8-186">来宾是另一个组织的参与者，已受邀访问 Teams 或组织租户中的其他资源。</span><span class="sxs-lookup"><span data-stu-id="a02e8-186">A guest is a participant from another organization who has been invited to access Teams or other resources in your organization's tenant.</span></span> <span data-ttu-id="a02e8-187">来宾将添加到组织的 Active Directory，并且几乎可以像本机团队成员一样获得所有相同的 Teams 功能，具有对团队聊天、会议和文件的完全访问权限。</span><span class="sxs-lookup"><span data-stu-id="a02e8-187">Guests are added to your organization’s Active Directory and can be given nearly all the same Teams capabilities as a native team member with full access to team chats, meetings, and files.</span></span> <span data-ttu-id="a02e8-188">_请参阅_ [Microsoft Teams 中的来宾访问](/microsoftteams/guest-access)</span><span class="sxs-lookup"><span data-stu-id="a02e8-188">_See_ [Guest access in Microsoft Teams](/microsoftteams/guest-access)</span></span>
1. <span data-ttu-id="a02e8-189">**联合/外部**。</span><span class="sxs-lookup"><span data-stu-id="a02e8-189">**Federated/External**.</span></span> <span data-ttu-id="a02e8-190">联盟用户是另一个组织中受邀加入会议的外部 Teams 用户。</span><span class="sxs-lookup"><span data-stu-id="a02e8-190">A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="a02e8-191">由于这些用户具有与联盟伙伴的有效凭据，因此他们将视为通过 Teams 身份验证，但无法访问你的团队或组织的其他共享资源。</span><span class="sxs-lookup"><span data-stu-id="a02e8-191">Since these users have valid credentials with federated partners, they are treated as authenticated by Teams but do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="a02e8-192">如果希望外部用户能够访问团队和频道，则来宾访问可能是更好的选择。</span><span class="sxs-lookup"><span data-stu-id="a02e8-192">If you want external users to have access to teams and channels, guest access might be a better option.</span></span> <span data-ttu-id="a02e8-193">_请参阅_[在 Microsoft Teams 中管理外部访问](/microsoftteams/manage-external-access)</span><span class="sxs-lookup"><span data-stu-id="a02e8-193">_See_ [Manage external access in Microsoft Teams](/microsoftteams/manage-external-access)</span></span>
1. <span data-ttu-id="a02e8-194">**匿名**。</span><span class="sxs-lookup"><span data-stu-id="a02e8-194">**Anonymous**.</span></span> <span data-ttu-id="a02e8-195">匿名用户没有 Active Directory 标识，并且未与租户联盟。</span><span class="sxs-lookup"><span data-stu-id="a02e8-195">Anonymous users do not have an Active Directory identity and are not federated with a tenant.</span></span> <span data-ttu-id="a02e8-196">匿名参与者与外部用户类似，但其身份不会预测到会议。</span><span class="sxs-lookup"><span data-stu-id="a02e8-196">The anonymous participant is like an external user, but their identity is not projected into the meeting.</span></span> <span data-ttu-id="a02e8-197">匿名用户将无法访问会议窗口中的应用。</span><span class="sxs-lookup"><span data-stu-id="a02e8-197">Anonymous users will not be able to access apps in a meeting window.</span></span>

## <a name="next-steps"></a><span data-ttu-id="a02e8-198">后续步骤</span><span class="sxs-lookup"><span data-stu-id="a02e8-198">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a02e8-199">设计应用</span><span class="sxs-lookup"><span data-stu-id="a02e8-199">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="a02e8-200">生成应用程序</span><span class="sxs-lookup"><span data-stu-id="a02e8-200">Build your app</span></span>](create-apps-for-teams-meetings.md)
