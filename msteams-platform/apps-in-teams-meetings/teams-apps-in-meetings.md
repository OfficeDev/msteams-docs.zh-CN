---
title: Teams 会议中的应用
author: laujan
description: 基于参与者和用户角色的 Teams 会议中应用概述
ms.topic: overview
ms.author: lajanuar
localization_priority: Normal
keywords: teams 应用会议用户参与者角色 api
ms.openlocfilehash: 29a24b70921e51d63d804e7a3edd901f607d3148
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52018381"
---
# <a name="apps-in-teams-meetings"></a><span data-ttu-id="61081-104">Teams 会议中的应用</span><span class="sxs-lookup"><span data-stu-id="61081-104">Apps in Teams meetings</span></span>

<span data-ttu-id="61081-105">会议支持协作、合作关系、明智沟通和在非独占活动论坛中共享反馈。</span><span class="sxs-lookup"><span data-stu-id="61081-105">Meetings enable collaboration, partnership, informed communication, and shared feedback in an inclusive and active forum.</span></span> <span data-ttu-id="61081-106">会议应用可以针对会议生命周期的每个阶段提供用户体验，包括会议前、会议内和会议后应用体验，具体取决于与会者的状态。</span><span class="sxs-lookup"><span data-stu-id="61081-106">The meeting app can deliver a user experience for each stage of the meeting lifecycle including pre-meeting, in-meeting and post-meeting app experience, depending on the attendee's status.</span></span>

<span data-ttu-id="61081-107">Teams 最终用户可以在会议期间使用选项卡库访问应用，例如：</span><span class="sxs-lookup"><span data-stu-id="61081-107">Teams end-users can access apps during meetings using the tab gallery, for example:</span></span>

* <span data-ttu-id="61081-108">预阶段看板</span><span class="sxs-lookup"><span data-stu-id="61081-108">Pre-stage a Kanban board</span></span>
* <span data-ttu-id="61081-109">启动会议内可操作对话框</span><span class="sxs-lookup"><span data-stu-id="61081-109">Launch an in-meeting actionable dialog</span></span>
* <span data-ttu-id="61081-110">创建会议后轮询</span><span class="sxs-lookup"><span data-stu-id="61081-110">Create a post-meeting poll</span></span>

<span data-ttu-id="61081-111">Teams 的会议应用扩展性基于以下概念：</span><span class="sxs-lookup"><span data-stu-id="61081-111">Teams’ meeting app extensibility is based on the following concepts:</span></span>

<span data-ttu-id="61081-112">✔会议生命周期具有阶段，如会议时间框架之前、期间和之后。</span><span class="sxs-lookup"><span data-stu-id="61081-112">✔ Meeting lifecycle has stages such as before, during, and after meeting time frame.</span></span>  
<span data-ttu-id="61081-113">✔会议的参与者角色，例如会议组织者、演示者或与会者。</span><span class="sxs-lookup"><span data-stu-id="61081-113">✔ Participant roles in a meeting such as meeting organizer, presenter, or attendee.</span></span>  
<span data-ttu-id="61081-114">✔用户类型在会议中，如租户内、来宾、联盟或匿名 Teams 用户。</span><span class="sxs-lookup"><span data-stu-id="61081-114">✔ User types in a meeting such as in-tenant, guest, federated, or anonymous Teams user.</span></span>

<span data-ttu-id="61081-115">本文介绍了有关会议生命周期以及如何在会议中集成选项卡、聊天机器人和消息传递扩展的信息。</span><span class="sxs-lookup"><span data-stu-id="61081-115">This article covers information about the meeting lifecycle and how to integrate tabs, bots, and messaging extensions in your meeting.</span></span> <span data-ttu-id="61081-116">它还允许您标识参与者角色，并使用不同的用户类型执行任务。</span><span class="sxs-lookup"><span data-stu-id="61081-116">It also enables you to identify participant roles and also use different user types to perform tasks.</span></span>

> [!NOTE]
> <span data-ttu-id="61081-117">若要使用会议应用程序扩展性功能，您必须具有相应的权限。</span><span class="sxs-lookup"><span data-stu-id="61081-117">To work with the meeting app extensibility features, you must have the appropriate permissions.</span></span>

### <a name="meeting-lifecycle"></a><span data-ttu-id="61081-118">会议生命周期</span><span class="sxs-lookup"><span data-stu-id="61081-118">Meeting lifecycle</span></span>

<span data-ttu-id="61081-119">会议生命周期由会议前、会议内和会议后应用体验组成。</span><span class="sxs-lookup"><span data-stu-id="61081-119">Meeting lifecycle consists of pre-meeting, in-meeting, and post-meeting app experience.</span></span> <span data-ttu-id="61081-120">可以在会议生命周期的每个阶段集成选项卡、聊天机器人和消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="61081-120">You can integrate tabs, bots, and messaging extensions in each stage of the meeting lifecycle.</span></span>

## <a name="integrate-tabs-into-the-meeting-lifecycle"></a><span data-ttu-id="61081-121">将选项卡集成到会议生命周期</span><span class="sxs-lookup"><span data-stu-id="61081-121">Integrate tabs into the meeting lifecycle</span></span>

<span data-ttu-id="61081-122">利用选项卡，团队成员可以访问频道或聊天内特定空间中的服务和内容。</span><span class="sxs-lookup"><span data-stu-id="61081-122">Tabs allow team members to access services and content in a specific space within a channel or chat.</span></span> <span data-ttu-id="61081-123">这使团队可以直接使用选项卡，并展开有关选项卡中可用的工具和数据的对话。</span><span class="sxs-lookup"><span data-stu-id="61081-123">This lets the team work directly with tabs and have conversations about the tools and data available within tabs.</span></span> <span data-ttu-id="61081-124">在 Teams 会议中，用户可以通过选择加号添加选项卡</span><span class="sxs-lookup"><span data-stu-id="61081-124">In Teams meeting, users can add a tab by selecting plus</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="61081-125">，并选择要作为选项卡安装的应用。</span><span class="sxs-lookup"><span data-stu-id="61081-125">, and choosing the app that they want to install as a tab.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="61081-126">如果你已将选项卡与会议集成，则你的应用必须遵循 Teams 单一登录 ([SSO](../tabs/how-to/authentication/auth-aad-sso.md)) 选项卡的身份验证流。</span><span class="sxs-lookup"><span data-stu-id="61081-126">If you have integrated a tab with your meeting, then your app must follow the Teams [single sign-on (SSO) authentication flow](../tabs/how-to/authentication/auth-aad-sso.md) for tabs.</span></span>

> [!NOTE]
> * <span data-ttu-id="61081-127">移动客户端仅在会议前和会议后阶段支持选项卡。</span><span class="sxs-lookup"><span data-stu-id="61081-127">Mobile clients support tabs only in pre and post meeting stages.</span></span> <span data-ttu-id="61081-128">会议内对话框和面板中的会议体验当前在移动设备上不可用。</span><span class="sxs-lookup"><span data-stu-id="61081-128">The in-meeting experiences that is in-meeting dialog and panel are currently not available on mobile.</span></span>
> * <span data-ttu-id="61081-129">应用仅在私人安排的会议中受支持。</span><span class="sxs-lookup"><span data-stu-id="61081-129">Apps are supported only in private scheduled meetings.</span></span>

### <a name="pre-meeting-app-experience"></a><span data-ttu-id="61081-130">会议前应用体验</span><span class="sxs-lookup"><span data-stu-id="61081-130">Pre-meeting app experience</span></span>

<span data-ttu-id="61081-131">**会议前体验：**</span><span class="sxs-lookup"><span data-stu-id="61081-131">**Pre-meeting experience:**</span></span>

![会议前体验](../assets/images/apps-in-meetings/PreMeeting.png)

<span data-ttu-id="61081-133">**"会议前"选项卡：**</span><span class="sxs-lookup"><span data-stu-id="61081-133">**Pre-meeting tab:**</span></span>

![会议前选项卡视图](../assets/images/apps-in-meetings/PreMeetingTab.png)

<span data-ttu-id="61081-135">✔权限的用户是可以在会议生命周期的不同阶段向会议添加应用的用户。</span><span class="sxs-lookup"><span data-stu-id="61081-135">✔ Permissioned users are users who can add apps to a meeting during different stages of the meeting lifecycle.</span></span> <span data-ttu-id="61081-136">这些用户可以使用两种方式通过选项卡库向会议添加应用：</span><span class="sxs-lookup"><span data-stu-id="61081-136">These users can add apps to a meeting through the tab gallery in two ways:</span></span>

   * <span data-ttu-id="61081-137">使用 **Teams** 计划表单上的"详细信息"选项卡。</span><span class="sxs-lookup"><span data-stu-id="61081-137">Using the **Details** tab on the Teams scheduling form.</span></span>

   * <span data-ttu-id="61081-138">使用现有 **会议** 中的"会议聊天"选项卡。</span><span class="sxs-lookup"><span data-stu-id="61081-138">Using the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="61081-139">✔选项卡应用可通过会议"详细信息"和"聊天 **"** 页面使用加号按钮➕访问。</span><span class="sxs-lookup"><span data-stu-id="61081-139">✔ Tab apps are accessible in meetings **Details** and **Chats** pages using a plus ➕ button.</span></span>

<span data-ttu-id="61081-140">✔投票或调查数超过 10 个，则选项卡布局必须组织在一个状态。</span><span class="sxs-lookup"><span data-stu-id="61081-140">✔ Tab layout must be in an organized state if there are more than ten polls or surveys.</span></span>

### <a name="in-meeting-app-experience"></a><span data-ttu-id="61081-141">会议内应用体验</span><span class="sxs-lookup"><span data-stu-id="61081-141">In-meeting app experience</span></span>

<span data-ttu-id="61081-142">✔会议应用程序承载在聊天窗口的顶部栏中，并且作为使用"会议内"选项卡的会议内选项卡体验托管。当用户通过选项卡库向会议添加选项卡时，将显示会议 **体验期间** 的应用。</span><span class="sxs-lookup"><span data-stu-id="61081-142">✔ Meeting apps are hosted in the top upper bar of the chat window and as in-meeting tab experience using the in-meeting tab. When users add a tab to a meeting through the tab gallery, apps that are **during meeting** experiences are shown.</span></span>

<span data-ttu-id="61081-143">✔权限用户可以在会议期间添加应用。</span><span class="sxs-lookup"><span data-stu-id="61081-143">✔ Permissioned users can add apps while in the meeting.</span></span>

<span data-ttu-id="61081-144">✔在会议上下文中加载时，应用可以利用 Teams 客户端 SDK 访问 、 和 以 `meetingId` `userMri` `frameContext` 适当呈现体验。</span><span class="sxs-lookup"><span data-stu-id="61081-144">✔ When loaded in the context of a meeting, apps can leverage the Teams client SDK to access the `meetingId`, `userMri`, and `frameContext` to appropriately render the experience.</span></span>

<span data-ttu-id="61081-145">✔导出调查或投票的结果会通知用户结果已成功下载。</span><span class="sxs-lookup"><span data-stu-id="61081-145">✔ Exporting a result of a survey or poll notifies the users that the results successfully downloaded.</span></span>

<span data-ttu-id="61081-146">✔在 Teams 会议侧面板或会议内对话框中显示应用。</span><span class="sxs-lookup"><span data-stu-id="61081-146">✔ An app is visible in a Teams meeting in the side panel or the in-meeting dialog box.</span></span> <span data-ttu-id="61081-147">使用"会议内"对话框为会议参与者展示可操作内容。</span><span class="sxs-lookup"><span data-stu-id="61081-147">Use the in-meeting dialog box to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="61081-148">有关详细信息，请参阅为 [Teams 会议创建应用](create-apps-for-teams-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="61081-148">For more information, see [create apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

   > [!NOTE]
   > <span data-ttu-id="61081-149">应用清单指定你的选项卡已 [针对](create-apps-for-teams-meetings.md#during-a-meeting)侧面板进行了优化，即它的显示位置。</span><span class="sxs-lookup"><span data-stu-id="61081-149">Your app manifest specifies that your tab is [optimized for side panel](create-apps-for-teams-meetings.md#during-a-meeting), that is where it is displayed.</span></span> <span data-ttu-id="61081-150">它还可以是共享托盘体验的一部分，但需遵循指定的设计准则。</span><span class="sxs-lookup"><span data-stu-id="61081-150">It can also be part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="61081-151">以下图像将应用显示为会议中的对话框和单独的侧面板：</span><span class="sxs-lookup"><span data-stu-id="61081-151">The following images display the app as an in-meeting dialog box and as a separate side panel:</span></span>

![会议内体验](../assets/images/apps-in-meetings/in-meeting-experience.png)

![会议内对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog.png)

#### <a name="in-meeting-actionable-dialog-for-users"></a><span data-ttu-id="61081-154">用户的"会议内可操作"对话框</span><span class="sxs-lookup"><span data-stu-id="61081-154">In-meeting actionable dialog for users</span></span>

![对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

### <a name="post-meeting-app-experience"></a><span data-ttu-id="61081-156">会议后应用体验</span><span class="sxs-lookup"><span data-stu-id="61081-156">Post-meeting app experience</span></span>

![会议后视图](../assets/images/apps-in-meetings/PostMeeting.png)

<span data-ttu-id="61081-158">✔会议后应用方案类似于当前的会议后体验，同时具有存在于图面中的选项卡的附加优势。</span><span class="sxs-lookup"><span data-stu-id="61081-158">✔ The post-meeting app scenario is similar to the current post-meeting experience with the added benefit of having tabs that exist within the surface.</span></span>

<span data-ttu-id="61081-159">✔权限用户可以使用 Teams 计划表单上的"详细信息"选项卡和现有会议中的"会议聊天"选项卡，将选项卡库中的应用添加到会议。</span><span class="sxs-lookup"><span data-stu-id="61081-159">✔ Permissioned users can add apps from the tab gallery to a meeting using the **Details** tab on the Teams scheduling form and the meeting **Chat** tab in an existing meeting.</span></span>

<span data-ttu-id="61081-160">✔投票或调查数超过 10 次时，必须组织选项卡布局。</span><span class="sxs-lookup"><span data-stu-id="61081-160">✔  Tab layout must be organized when there are more than ten polls or surveys.</span></span>

### <a name="integrate-bots-into-the-meeting-lifecycle"></a><span data-ttu-id="61081-161">将机器人集成到会议生命周期</span><span class="sxs-lookup"><span data-stu-id="61081-161">Integrate bots into the meeting lifecycle</span></span>

<span data-ttu-id="61081-162">对于自动程序实现，首先 [构建自动](../build-your-first-app/build-bot.md) 程序，然后继续 [创建 Teams 会议应用](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="61081-162">For bot implementation, start with [build a bot](../build-your-first-app/build-bot.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a><span data-ttu-id="61081-163">将消息传递扩展集成到会议生命周期</span><span class="sxs-lookup"><span data-stu-id="61081-163">Integrate messaging extensions into the meeting lifecycle</span></span>

<span data-ttu-id="61081-164">对于消息传递扩展实现，首先 [构建](../messaging-extensions/how-to/create-messaging-extension.md) 消息传递扩展，然后继续 [为 Teams 会议创建应用](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="61081-164">For messaging extension implementation, start with [build a messaging extension](../messaging-extensions/how-to/create-messaging-extension.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-reference).</span></span>

## <a name="participant-roles-and-user-types-in-a-meeting"></a><span data-ttu-id="61081-165">会议的参与者角色和用户类型</span><span class="sxs-lookup"><span data-stu-id="61081-165">Participant roles and user types in a meeting</span></span>

![会议参与者](../assets/images/apps-in-meetings/participant-roles.png)

### <a name="participant-roles"></a><span data-ttu-id="61081-167">参与者角色</span><span class="sxs-lookup"><span data-stu-id="61081-167">Participant roles</span></span>

<span data-ttu-id="61081-168">默认参与者设置由组织的 IT 管理员确定。</span><span class="sxs-lookup"><span data-stu-id="61081-168">Default participant settings are determined by an organization's IT administrator.</span></span> <span data-ttu-id="61081-169">以下是会议中的参与者角色：</span><span class="sxs-lookup"><span data-stu-id="61081-169">The following are the participant roles in a meeting:</span></span>

* <span data-ttu-id="61081-170">**组织者**：组织者安排会议、设置会议选项、分配会议角色和启动会议。</span><span class="sxs-lookup"><span data-stu-id="61081-170">**Organizer**: The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="61081-171">只有拥有具有 Teams 许可证的 M365 帐户的用户才能是组织者和控制与会者权限。</span><span class="sxs-lookup"><span data-stu-id="61081-171">Only users with a M365 account with a Teams license can be organizers and control attendee permissions.</span></span> <span data-ttu-id="61081-172">会议组织者可以更改特定会议的设置。</span><span class="sxs-lookup"><span data-stu-id="61081-172">A meeting organizer can change the settings for a specific meeting.</span></span> <span data-ttu-id="61081-173">组织者可以在"会议选项" **网页上进行** 这些更改。</span><span class="sxs-lookup"><span data-stu-id="61081-173">Organizers can make these changes on the **Meeting options** web page.</span></span>
* <span data-ttu-id="61081-174">**演示** 者：演示者具有与组织者相同的功能。</span><span class="sxs-lookup"><span data-stu-id="61081-174">**Presenter**: Presenters have the same capabilities as organizer.</span></span> <span data-ttu-id="61081-175">但是，演示者无法从会话中删除组织者或修改会话的会议选项。</span><span class="sxs-lookup"><span data-stu-id="61081-175">However, a presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="61081-176">默认情况下，加入会议的参与者具有演示者角色。</span><span class="sxs-lookup"><span data-stu-id="61081-176">By default, participants joining a meeting have the presenter role.</span></span>
* <span data-ttu-id="61081-177">**与会者**：与会者是受邀参加会议但无权担任演示者的用户。</span><span class="sxs-lookup"><span data-stu-id="61081-177">**Attendee**: An attendee is a user who has been invited to attend a meeting but who is not authorized to act as a presenter.</span></span> <span data-ttu-id="61081-178">与会者可以与其他会议成员交互，但不能管理任何会议设置或共享内容。</span><span class="sxs-lookup"><span data-stu-id="61081-178">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

<span data-ttu-id="61081-179">只有组织者或演示者才能添加、删除或卸载应用。</span><span class="sxs-lookup"><span data-stu-id="61081-179">Only an organizer or presenter can add, remove, or uninstall apps.</span></span> <span data-ttu-id="61081-180">只有组织者或演示者可以在会议创建投票。</span><span class="sxs-lookup"><span data-stu-id="61081-180">Only organizer or presenter can create polls in a meeting.</span></span>

<span data-ttu-id="61081-181">有关详细信息，请参阅 [Teams 会议中的角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="61081-181">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

<span data-ttu-id="61081-182">您可以按如下  **方式访问"会议选项** "页：</span><span class="sxs-lookup"><span data-stu-id="61081-182">You can access the  **Meeting options** page as follows:</span></span>

* <span data-ttu-id="61081-183">在 Teams 中，转到 **日历** ![ 日历徽标 ](../assets/images/apps-in-meetings/calendar-logo.png) ，选择会议，然后选择会议 **选项**。</span><span class="sxs-lookup"><span data-stu-id="61081-183">In Teams, go to **Calendar** ![calendar logo](../assets/images/apps-in-meetings/calendar-logo.png), select a meeting, and then **Meeting options**.</span></span>

* <span data-ttu-id="61081-184">在会议邀请中，选择"**会议选项"。**</span><span class="sxs-lookup"><span data-stu-id="61081-184">In a meeting invitation, select **Meeting options**.</span></span>

* <span data-ttu-id="61081-185">在会议期间，选择 **"显示参与者** ![ 在会议控件 ](../assets/images/apps-in-meetings/show-participants.png) 中显示参与者图标"。</span><span class="sxs-lookup"><span data-stu-id="61081-185">During a meeting, select **Show participants** ![show participants icon](../assets/images/apps-in-meetings/show-participants.png) in the meeting controls.</span></span> <span data-ttu-id="61081-186">然后，在参与者列表上方，选择"**管理权限"。**</span><span class="sxs-lookup"><span data-stu-id="61081-186">Then, above the list of participants, choose **Manage permissions**.</span></span>

### <a name="user-types"></a><span data-ttu-id="61081-187">用户类型</span><span class="sxs-lookup"><span data-stu-id="61081-187">User types</span></span>

> [!NOTE]
> <span data-ttu-id="61081-188">分配了特定用户类型的用户可以加入会议，并承担参与者角色中所述的参与者 [角色之一](#participant-roles)。</span><span class="sxs-lookup"><span data-stu-id="61081-188">Users with specific user types assigned to them can join meetings and assume one of the participant roles described in [participant roles](#participant-roles).</span></span> <span data-ttu-id="61081-189">用户类型不包含在 **getParticipantRole** API 中。</span><span class="sxs-lookup"><span data-stu-id="61081-189">The user type is not included in the **getParticipantRole** API.</span></span>

<span data-ttu-id="61081-190">以下用户类型标识每个用户可以执行哪些操作以及可以访问哪些内容：</span><span class="sxs-lookup"><span data-stu-id="61081-190">The following user types identify what each user can do and what they can access:</span></span>

* <span data-ttu-id="61081-191">**租户内**：租户内用户属于组织，拥有租户的 Azure Active Directory (AAD) 凭据。</span><span class="sxs-lookup"><span data-stu-id="61081-191">**In-tenant**: In-tenant users belong to the organization and have credentials in Azure Active Directory (AAD) for the tenant.</span></span> <span data-ttu-id="61081-192">他们通常是全职、现场或远程员工。</span><span class="sxs-lookup"><span data-stu-id="61081-192">They are usually full-time, onsite, or remote employees.</span></span> <span data-ttu-id="61081-193">租户内用户可以是组织者、演示者或与会者。</span><span class="sxs-lookup"><span data-stu-id="61081-193">An in-tenant user can be an organizer, presenter, or attendee.</span></span>
* <span data-ttu-id="61081-194">**来宾**：来宾是受邀访问组织租户中的 Teams 或其他资源的另一个组织的参与者。</span><span class="sxs-lookup"><span data-stu-id="61081-194">**Guest**: A guest is a participant from another organization invited to access Teams or other resources in the organization's tenant.</span></span> <span data-ttu-id="61081-195">来宾将添加到组织的 AAD，并且具有与本机团队成员相同的 Teams 功能，可以访问团队聊天、会议和文件。</span><span class="sxs-lookup"><span data-stu-id="61081-195">Guests are added to your organization’s AAD and have the same Teams capabilities as a native team member with access to team chats, meetings, and files.</span></span> <span data-ttu-id="61081-196">来宾用户可以是组织者、演示者或与会者。</span><span class="sxs-lookup"><span data-stu-id="61081-196">A guest user can be an organizer, presenter, or attendee.</span></span> <span data-ttu-id="61081-197">有关详细信息，请参阅 Teams [中的来宾访问](/microsoftteams/guest-access)。</span><span class="sxs-lookup"><span data-stu-id="61081-197">For more information, see [guest access in Teams](/microsoftteams/guest-access).</span></span>
* <span data-ttu-id="61081-198">**联盟或外部**：联盟用户是另一个组织中受邀加入会议的外部 Teams 用户。</span><span class="sxs-lookup"><span data-stu-id="61081-198">**Federated or external**: A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="61081-199">这些用户具有联盟伙伴的有效凭据，并且由 Teams 授权。</span><span class="sxs-lookup"><span data-stu-id="61081-199">These users have valid credentials with federated partners and are authorized by Teams.</span></span> <span data-ttu-id="61081-200">他们无法访问你的团队或组织的其他共享资源。</span><span class="sxs-lookup"><span data-stu-id="61081-200">They do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="61081-201">对于外部用户来说，来宾访问是访问团队和频道的更好选择。</span><span class="sxs-lookup"><span data-stu-id="61081-201">Guest access is a better option for external users to have access to teams and channels.</span></span> <span data-ttu-id="61081-202">有关详细信息，请参阅在 [Teams 中管理外部访问](/microsoftteams/manage-external-access)。</span><span class="sxs-lookup"><span data-stu-id="61081-202">For more information, see [manage external access in Teams](/microsoftteams/manage-external-access).</span></span>
* <span data-ttu-id="61081-203">**匿名**：匿名用户没有 AAD 标识，并且未与租户联盟。</span><span class="sxs-lookup"><span data-stu-id="61081-203">**Anonymous**: Anonymous users do not have an AAD identity and are not federated with a tenant.</span></span> <span data-ttu-id="61081-204">匿名参与者与外部用户类似，但其身份不会在会议中预测。</span><span class="sxs-lookup"><span data-stu-id="61081-204">The anonymous participant is like an external user, but their identity is not projected in the meeting.</span></span> <span data-ttu-id="61081-205">匿名用户不能是组织者，但可以是演示者或与会者。</span><span class="sxs-lookup"><span data-stu-id="61081-205">An anonymous user cannot be an organizer but can be a presenter or an attendee.</span></span>

> [!NOTE]
> <span data-ttu-id="61081-206">匿名用户继承全局默认用户级别应用程序权限策略。</span><span class="sxs-lookup"><span data-stu-id="61081-206">Anonymous users inherit the global default user-level app permission policy.</span></span> <span data-ttu-id="61081-207">有关详细信息，请参阅管理 [应用](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access)。</span><span class="sxs-lookup"><span data-stu-id="61081-207">For more information, see [Manage Apps](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access).</span></span>

<span data-ttu-id="61081-208">下表提供了用户类型以及每个用户可以访问的功能：</span><span class="sxs-lookup"><span data-stu-id="61081-208">The following table provides the user types and what features each user can access:</span></span>

| <span data-ttu-id="61081-209">用户类型</span><span class="sxs-lookup"><span data-stu-id="61081-209">User type</span></span> | <span data-ttu-id="61081-210">选项卡</span><span class="sxs-lookup"><span data-stu-id="61081-210">Tabs</span></span> | <span data-ttu-id="61081-211">机器人</span><span class="sxs-lookup"><span data-stu-id="61081-211">Bots</span></span> | <span data-ttu-id="61081-212">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="61081-212">Messaging extensions</span></span> | <span data-ttu-id="61081-213">自适应卡</span><span class="sxs-lookup"><span data-stu-id="61081-213">Adaptive Cards</span></span> | <span data-ttu-id="61081-214">任务模块</span><span class="sxs-lookup"><span data-stu-id="61081-214">Task modules</span></span> | <span data-ttu-id="61081-215">会议内的对话框</span><span class="sxs-lookup"><span data-stu-id="61081-215">In-meeting dialog</span></span> |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| <span data-ttu-id="61081-216">匿名用户</span><span class="sxs-lookup"><span data-stu-id="61081-216">Anonymous user</span></span> | <span data-ttu-id="61081-217">不可用</span><span class="sxs-lookup"><span data-stu-id="61081-217">Not available</span></span> | <span data-ttu-id="61081-218">不可用</span><span class="sxs-lookup"><span data-stu-id="61081-218">Not available</span></span> | <span data-ttu-id="61081-219">不可用</span><span class="sxs-lookup"><span data-stu-id="61081-219">Not available</span></span> | <span data-ttu-id="61081-220">允许会议聊天中的交互。</span><span class="sxs-lookup"><span data-stu-id="61081-220">Interactions in the meeting chat are allowed.</span></span> | <span data-ttu-id="61081-221">允许通过自适应卡片在会议聊天中交互。</span><span class="sxs-lookup"><span data-stu-id="61081-221">Interactions in the meeting chat from an Adaptive Card are allowed.</span></span> | <span data-ttu-id="61081-222">不可用</span><span class="sxs-lookup"><span data-stu-id="61081-222">Not available</span></span> |
| <span data-ttu-id="61081-223">属于租户 AAD 的来宾</span><span class="sxs-lookup"><span data-stu-id="61081-223">Guest that is part of the tenant AAD</span></span> | <span data-ttu-id="61081-224">允许交互。</span><span class="sxs-lookup"><span data-stu-id="61081-224">Interaction is allowed.</span></span> <span data-ttu-id="61081-225">不允许创建、更新和删除。</span><span class="sxs-lookup"><span data-stu-id="61081-225">Creating, updating, and deleting are not allowed.</span></span> | <span data-ttu-id="61081-226">不可用</span><span class="sxs-lookup"><span data-stu-id="61081-226">Not available</span></span> | <span data-ttu-id="61081-227">不可用</span><span class="sxs-lookup"><span data-stu-id="61081-227">Not available</span></span> | <span data-ttu-id="61081-228">允许会议聊天中的交互。</span><span class="sxs-lookup"><span data-stu-id="61081-228">Interactions in the meeting chat are allowed.</span></span> | <span data-ttu-id="61081-229">允许通过自适应卡片在会议聊天中交互。</span><span class="sxs-lookup"><span data-stu-id="61081-229">Interactions in the meeting chat from an Adaptive Card are allowed.</span></span> | <span data-ttu-id="61081-230">可用</span><span class="sxs-lookup"><span data-stu-id="61081-230">Available</span></span> |
| <span data-ttu-id="61081-231">Federated</span><span class="sxs-lookup"><span data-stu-id="61081-231">Federated</span></span> | <span data-ttu-id="61081-232">不可用</span><span class="sxs-lookup"><span data-stu-id="61081-232">Not available</span></span> | <span data-ttu-id="61081-233">不可用</span><span class="sxs-lookup"><span data-stu-id="61081-233">Not available</span></span> | <span data-ttu-id="61081-234">不可用</span><span class="sxs-lookup"><span data-stu-id="61081-234">Not available</span></span> | <span data-ttu-id="61081-235">不可用</span><span class="sxs-lookup"><span data-stu-id="61081-235">Not available</span></span> | <span data-ttu-id="61081-236">不可用</span><span class="sxs-lookup"><span data-stu-id="61081-236">Not available</span></span> | <span data-ttu-id="61081-237">不可用</span><span class="sxs-lookup"><span data-stu-id="61081-237">Not available</span></span> |

## <a name="see-also"></a><span data-ttu-id="61081-238">另请参阅</span><span class="sxs-lookup"><span data-stu-id="61081-238">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61081-239">Tab</span><span class="sxs-lookup"><span data-stu-id="61081-239">Tab</span></span>](../tabs/what-are-tabs.md#how-do-tabs-work)

> [!div class="nextstepaction"]
> [<span data-ttu-id="61081-240">Bot</span><span class="sxs-lookup"><span data-stu-id="61081-240">Bot</span></span>](../bots/what-are-bots.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="61081-241">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="61081-241">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="61081-242">设计应用</span><span class="sxs-lookup"><span data-stu-id="61081-242">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-steps"></a><span data-ttu-id="61081-243">后续步骤</span><span class="sxs-lookup"><span data-stu-id="61081-243">Next steps</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="61081-244">生成应用程序</span><span class="sxs-lookup"><span data-stu-id="61081-244">Build your app</span></span>](create-apps-for-teams-meetings.md)
