---
title: 会议应用可扩展性
author: surbhigupta
description: 了解会议应用程序扩展性
ms.topic: conceptual
ms.openlocfilehash: 1b9cc381879a12d5c9d26711dde93e308d3e4231
ms.sourcegitcommit: 3560ee1619e3ab6483a250f1d7f2ceb69353b2dc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/08/2021
ms.locfileid: "53335383"
---
# <a name="meeting-app-extensibility"></a><span data-ttu-id="5c940-103">会议应用可扩展性</span><span class="sxs-lookup"><span data-stu-id="5c940-103">Meeting app extensibility</span></span>

<span data-ttu-id="5c940-104">Teams应用程序扩展性基于以下概念：</span><span class="sxs-lookup"><span data-stu-id="5c940-104">Teams’ meeting app extensibility is based on the following concepts:</span></span>

* <span data-ttu-id="5c940-105">会议生命周期具有不同的阶段，如会议前、会中和会议后。</span><span class="sxs-lookup"><span data-stu-id="5c940-105">Meeting lifecycle has different stages such as pre-meeting, in-meeting, and post-meeting.</span></span>  
* <span data-ttu-id="5c940-106">会议有三个不同的参与者角色：组织者、演示者和与会者。</span><span class="sxs-lookup"><span data-stu-id="5c940-106">There are three distinct participant roles in a meeting: organizer, presenter, and attendee.</span></span> <span data-ttu-id="5c940-107">有关详细信息，请参阅[会议Teams角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="5c940-107">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>  
* <span data-ttu-id="5c940-108">会议有 [各种](/microsoftteams/non-standard-users#:~:text=An%20anonymous%20user%20is%20a,their%20Microsoft%20or%20organization's%20account.) 用户类型：租户内用户、 [来宾](/microsoftteams/guest-access)用户、 [联盟用户](/microsoftteams/manage-external-access)和匿名用户。</span><span class="sxs-lookup"><span data-stu-id="5c940-108">There are various [user types](/microsoftteams/non-standard-users#:~:text=An%20anonymous%20user%20is%20a,their%20Microsoft%20or%20organization's%20account.) in a meeting: in-tenant, [guest](/microsoftteams/guest-access), [federated](/microsoftteams/manage-external-access), and anonymous users.</span></span>

<span data-ttu-id="5c940-109">本文介绍了有关会议生命周期以及如何在会议中集成选项卡、聊天机器人和消息传递扩展的信息。</span><span class="sxs-lookup"><span data-stu-id="5c940-109">This article covers information about meeting lifecycle and how to integrate tabs, bots, and messaging extensions in the meeting.</span></span> <span data-ttu-id="5c940-110">它提供用于标识不同参与者角色和用于执行任务的不同用户类型的信息。</span><span class="sxs-lookup"><span data-stu-id="5c940-110">It provides information to identify different participant roles and different user types to perform tasks.</span></span>

## <a name="meeting-lifecycle"></a><span data-ttu-id="5c940-111">会议生命周期</span><span class="sxs-lookup"><span data-stu-id="5c940-111">Meeting lifecycle</span></span>

<span data-ttu-id="5c940-112">会议生命周期由会议前、会议内和会议后应用体验组成。</span><span class="sxs-lookup"><span data-stu-id="5c940-112">Meeting lifecycle consists of pre-meeting, in-meeting, and post-meeting app experience.</span></span> <span data-ttu-id="5c940-113">可以在会议生命周期的每个阶段集成选项卡、聊天机器人和消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="5c940-113">You can integrate tabs, bots, and messaging extensions in each stage of the meeting lifecycle.</span></span>

### <a name="integrate-tabs-into-the-meeting-lifecycle"></a><span data-ttu-id="5c940-114">将选项卡集成到会议生命周期</span><span class="sxs-lookup"><span data-stu-id="5c940-114">Integrate tabs into the meeting lifecycle</span></span>

<span data-ttu-id="5c940-115">选项卡允许团队成员访问会议内特定空间中的服务和内容。</span><span class="sxs-lookup"><span data-stu-id="5c940-115">Tabs allow team members to access services and content in a specific space within a meeting.</span></span> <span data-ttu-id="5c940-116">该团队直接与选项卡协作，并展开有关选项卡中可用的工具和数据的对话。</span><span class="sxs-lookup"><span data-stu-id="5c940-116">The team works directly with tabs and has conversations about the tools and data available within tabs.</span></span> <span data-ttu-id="5c940-117">在Teams中，用户可以通过选择</span><span class="sxs-lookup"><span data-stu-id="5c940-117">In Teams meeting, users can add a tab by selecting</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="5c940-118">，并选择要安装的应用。</span><span class="sxs-lookup"><span data-stu-id="5c940-118">, and choosing the app that they want to install.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="5c940-119">如果已将选项卡与会议集成，则应用必须遵循选项卡的 Teams 单一登录[ (SSO) 身份验证流](../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="5c940-119">If you have integrated a tab with your meeting, then your app must follow the Teams [single sign-on (SSO) authentication flow for tabs](../tabs/how-to/authentication/auth-aad-sso.md).</span></span>

> [!NOTE]
> <span data-ttu-id="5c940-120">应用仅在私人安排的会议中受支持。</span><span class="sxs-lookup"><span data-stu-id="5c940-120">Apps are supported in private scheduled meetings only.</span></span>

#### <a name="pre-meeting-app-experience"></a><span data-ttu-id="5c940-121">会议前应用体验</span><span class="sxs-lookup"><span data-stu-id="5c940-121">Pre-meeting app experience</span></span>

<span data-ttu-id="5c940-122">通过会议前应用体验，你可以查找和添加会议应用并执行会议前任务，例如开发投票以调查会议参与者。</span><span class="sxs-lookup"><span data-stu-id="5c940-122">With the pre-meeting app experience, you can find and add meeting apps and perform pre-meeting tasks, such as developing a poll to survey meeting participants.</span></span>

<span data-ttu-id="5c940-123">**向现有会议添加选项卡**</span><span class="sxs-lookup"><span data-stu-id="5c940-123">**To add tabs to an existing meeting**</span></span>

1. <span data-ttu-id="5c940-124">在日历中，选择要添加选项卡的会议。</span><span class="sxs-lookup"><span data-stu-id="5c940-124">In your calendar, select a meeting to which you want to add a tab.</span></span>
1. <span data-ttu-id="5c940-125">选择" **详细信息"** 选项卡并选择</span><span class="sxs-lookup"><span data-stu-id="5c940-125">Select the **Details** tab and select</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/><span data-ttu-id="5c940-126">.</span><span class="sxs-lookup"><span data-stu-id="5c940-126">.</span></span> <span data-ttu-id="5c940-127">将显示选项卡库。</span><span class="sxs-lookup"><span data-stu-id="5c940-127">The tab gallery appears.</span></span>

    ![会议前体验](../assets/images/apps-in-meetings/PreMeeting.png)

1. <span data-ttu-id="5c940-129">在选项卡库中，选择要添加的应用并按照所需步骤操作。</span><span class="sxs-lookup"><span data-stu-id="5c940-129">In the tab gallery, select the app that you want to add and follow the steps as required.</span></span> <span data-ttu-id="5c940-130">应用作为选项卡安装。</span><span class="sxs-lookup"><span data-stu-id="5c940-130">The app is installed as a tab.</span></span>

    > [!NOTE]
    > * <span data-ttu-id="5c940-131">您还可以使用现有会议中的"会议 **聊天** "选项卡添加选项卡。</span><span class="sxs-lookup"><span data-stu-id="5c940-131">You can also add a tab using the meeting **Chat** tab in an existing meeting.</span></span>
    > * <span data-ttu-id="5c940-132">如果投票或调查超过 10 个，则选项卡布局必须组织在一个状态。</span><span class="sxs-lookup"><span data-stu-id="5c940-132">Tab layout must be in an organized state, if there are more than ten polls or surveys.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="5c940-133">桌面设备</span><span class="sxs-lookup"><span data-stu-id="5c940-133">Desktop</span></span>](#tab/desktop)

![会议前选项卡视图](../assets/images/apps-in-meetings/PreMeetingTab.png)

# <a name="mobile"></a>[<span data-ttu-id="5c940-135">移动设备</span><span class="sxs-lookup"><span data-stu-id="5c940-135">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="5c940-136">将选项卡添加到桌面或 Web 上的现有会议后，可以在会议详细信息的"更多部分"下看到会议前体验中的相同应用。</span><span class="sxs-lookup"><span data-stu-id="5c940-136">After the tabs are added to an existing meeting on desktop or web, you can see the same apps in pre-meeting experience under **More** section of the meeting details.</span></span>

<img src="../assets/images/apps-in-meetings/mobilepremeeting.png" alt="Mobile pre-meeting experience" width="200"/>  

---

#### <a name="in-meeting-app-experience"></a><span data-ttu-id="5c940-137">会议内应用体验</span><span class="sxs-lookup"><span data-stu-id="5c940-137">In-meeting app experience</span></span>

<span data-ttu-id="5c940-138">借助会议内应用体验，可以使用应用和会议内对话框在会议期间与参与者互动。</span><span class="sxs-lookup"><span data-stu-id="5c940-138">With the in-meeting app experience, you can engage participants during the meeting by using apps and the in-meeting dialog box.</span></span> <span data-ttu-id="5c940-139">会议应用程序作为会议中的选项卡托管在会议窗口的顶部栏中。使用"会议内"对话框为会议参与者展示可操作内容。</span><span class="sxs-lookup"><span data-stu-id="5c940-139">Meeting apps are hosted in the top upper bar of the meeting window as an in-meeting tab. Use the in-meeting dialog box to showcase actionable content for meeting participants.</span></span> <span data-ttu-id="5c940-140">有关详细信息，请参阅[为会议创建Teams应用](create-apps-for-teams-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="5c940-140">For more information, see [create apps for Teams meetings](create-apps-for-teams-meetings.md).</span></span>

<span data-ttu-id="5c940-141">对于移动版，会议应用可从会议>省略号 &#x25CF;&#x25CF;&#x25CF; 提供。</span><span class="sxs-lookup"><span data-stu-id="5c940-141">For mobile, meeting apps are available from **Apps** > ellipses &#x25CF;&#x25CF;&#x25CF; in the meeting.</span></span> <span data-ttu-id="5c940-142">选择 **"** 应用"以查看会议提供的所有应用。</span><span class="sxs-lookup"><span data-stu-id="5c940-142">Select **Apps** to view all the apps available in the meeting.</span></span>

<span data-ttu-id="5c940-143">**在会议期间使用选项卡**</span><span class="sxs-lookup"><span data-stu-id="5c940-143">**To use tabs during a meeting**</span></span>

1. <span data-ttu-id="5c940-144">转到Teams。</span><span class="sxs-lookup"><span data-stu-id="5c940-144">Go to Teams.</span></span>
1. <span data-ttu-id="5c940-145">在日历中，选择要使用选项卡的会议。</span><span class="sxs-lookup"><span data-stu-id="5c940-145">In your calendar, select a meeting where you want to use a tab.</span></span>
1. <span data-ttu-id="5c940-146">进入会议后，从聊天窗口的顶部栏中，选择所需的应用。</span><span class="sxs-lookup"><span data-stu-id="5c940-146">After entering the meeting, from the top upper bar of the chat window, select the required app.</span></span>
    <span data-ttu-id="5c940-147">应用在侧面板Teams会议对话框中的"会议"对话框中可见。</span><span class="sxs-lookup"><span data-stu-id="5c940-147">An app is visible in a Teams meeting in the side panel or the in-meeting dialog box.</span></span>
1. <span data-ttu-id="5c940-148">在"会议内"对话框中，输入你的回复作为反馈。</span><span class="sxs-lookup"><span data-stu-id="5c940-148">In the in-meeting dialog box, enter your response as a feedback.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="5c940-149">桌面设备</span><span class="sxs-lookup"><span data-stu-id="5c940-149">Desktop</span></span>](#tab/desktop)

![对话框视图](../assets/images/apps-in-meetings/in-meeting-dialog-view.png)

# <a name="mobile"></a>[<span data-ttu-id="5c940-151">移动设备</span><span class="sxs-lookup"><span data-stu-id="5c940-151">Mobile</span></span>](#tab/mobile)

<span data-ttu-id="5c940-152">进入会议并添加桌面或 Web 中的应用后，该应用在移动Teams应用程序部分 **下可见**。</span><span class="sxs-lookup"><span data-stu-id="5c940-152">After entering the meeting and adding the app from desktop or web, the app is visible in mobile Teams meeting under the **Apps** section.</span></span> <span data-ttu-id="5c940-153">选择 **"** 应用"以显示应用列表。</span><span class="sxs-lookup"><span data-stu-id="5c940-153">Select **Apps** to show the list of apps.</span></span> <span data-ttu-id="5c940-154">用户可以启动任何应用作为应用的会议侧面板。</span><span class="sxs-lookup"><span data-stu-id="5c940-154">User can launch any of the apps as an in-meeting side panel of the app.</span></span>

<span data-ttu-id="5c940-155">将显示"会议内"对话框，可在其中输入回复作为反馈。</span><span class="sxs-lookup"><span data-stu-id="5c940-155">The in-meeting dialog box is displayed where you can enter your response as a feedback.</span></span>

<img src="../assets/images/apps-in-meetings/mobile-in-meeting-dialog-view.png" alt="Mobile dialog box view" width="200"/>

> [!NOTE]
> <span data-ttu-id="5c940-156">无需更改应用清单，应用就适用于移动设备。</span><span class="sxs-lookup"><span data-stu-id="5c940-156">You need not change the app manifest for the apps to work on mobile.</span></span>

---

> [!NOTE]
> * <span data-ttu-id="5c940-157">应用可以利用 Teams 客户端 SDK 来访问 `meetingId` 、 `userMri` 和 `frameContext` ，并适当地呈现体验。</span><span class="sxs-lookup"><span data-stu-id="5c940-157">Apps can leverage the Teams Client SDK to access the `meetingId`, `userMri`, and `frameContext` to render the experience appropriately.</span></span>
> * <span data-ttu-id="5c940-158">如果成功呈现了会议内对话框，则你得到一条通知，告知已成功下载结果。</span><span class="sxs-lookup"><span data-stu-id="5c940-158">If the in-meeting dialog box is rendered successfully, you will get a notification that the results are successfully downloaded.</span></span>
> * <span data-ttu-id="5c940-159">应用清单指定希望它们显示的位置。</span><span class="sxs-lookup"><span data-stu-id="5c940-159">Your app manifest specifies the places that you want them to appear.</span></span> <span data-ttu-id="5c940-160">上下文字段用于此目的。</span><span class="sxs-lookup"><span data-stu-id="5c940-160">The context field is used for this purpose.</span></span> <span data-ttu-id="5c940-161">它还是共享托盘体验的一部分，但需遵循指定的设计准则。</span><span class="sxs-lookup"><span data-stu-id="5c940-161">It is also the part of a share-tray experience, subject to specified design guidelines.</span></span>

<span data-ttu-id="5c940-162">下图演示了会议侧面板：</span><span class="sxs-lookup"><span data-stu-id="5c940-162">The following image illustrates the in-meeting side panel:</span></span>

![会议侧面板](../assets/images/apps-in-meetings/in-meeting-dialog.png)

<span data-ttu-id="5c940-164">下表介绍了应用程序在获得批准和未获得批准时的行为：</span><span class="sxs-lookup"><span data-stu-id="5c940-164">The following table describes the behavior of app when it is approved and not approved:</span></span>

|<span data-ttu-id="5c940-165">应用功能</span><span class="sxs-lookup"><span data-stu-id="5c940-165">App capability</span></span> | <span data-ttu-id="5c940-166">应用已批准</span><span class="sxs-lookup"><span data-stu-id="5c940-166">App is approved</span></span> | <span data-ttu-id="5c940-167">应用未获得批准</span><span class="sxs-lookup"><span data-stu-id="5c940-167">App is not approved</span></span> |
|---|---|---|
| <span data-ttu-id="5c940-168">会议可扩展性</span><span class="sxs-lookup"><span data-stu-id="5c940-168">Meeting extensibility</span></span> | <span data-ttu-id="5c940-169">该应用将显示在会议中。</span><span class="sxs-lookup"><span data-stu-id="5c940-169">The app will appear in meetings.</span></span> | <span data-ttu-id="5c940-170">该应用不会显示在移动客户端的会议中。</span><span class="sxs-lookup"><span data-stu-id="5c940-170">The app will not appear in meetings for the mobile clients.</span></span> |

#### <a name="post-meeting-app-experience"></a><span data-ttu-id="5c940-171">会议后应用体验</span><span class="sxs-lookup"><span data-stu-id="5c940-171">Post-meeting app experience</span></span>

<span data-ttu-id="5c940-172">通过会议后应用体验，可以查看会议结果，如投票调查结果或反馈。</span><span class="sxs-lookup"><span data-stu-id="5c940-172">With post-meeting app experience, you can view the results of the meeting, such as poll survey results or feedback.</span></span> <span data-ttu-id="5c940-173">Select</span><span class="sxs-lookup"><span data-stu-id="5c940-173">Select</span></span> <img src="~/assets/images/apps-in-meetings/plusbutton.png" alt="Plus button" width="30"/> <span data-ttu-id="5c940-174">添加选项卡、获取会议笔记以及组织者和与会者必须采取措施的结果。</span><span class="sxs-lookup"><span data-stu-id="5c940-174">to add a tab, get meeting notes, and results on which organizers and attendees must take action.</span></span>

<span data-ttu-id="5c940-175">下图显示了 **"Contoso"** 选项卡，其中显示来自与会者的投票结果和反馈：</span><span class="sxs-lookup"><span data-stu-id="5c940-175">The following image displays the **Contoso** tab with results of poll and feedback received from meeting attendees:</span></span>

# <a name="desktop"></a>[<span data-ttu-id="5c940-176">桌面设备</span><span class="sxs-lookup"><span data-stu-id="5c940-176">Desktop</span></span>](#tab/desktop)

![会议后视图](../assets/images/apps-in-meetings/PostMeeting.png)

# <a name="mobile"></a>[<span data-ttu-id="5c940-178">移动设备</span><span class="sxs-lookup"><span data-stu-id="5c940-178">Mobile</span></span>](#tab/mobile)

<img src="../assets/images/apps-in-meetings/mobilePostMeeting.png" alt="Mobile post meeting view" width="200"/>

---

> [!NOTE]
> <span data-ttu-id="5c940-179">当有 10 多个投票或调查时，必须组织选项卡布局。</span><span class="sxs-lookup"><span data-stu-id="5c940-179">Tab layout must be organized when there are more than 10 polls or surveys.</span></span>

### <a name="integrate-bots-into-the-meeting-lifecycle"></a><span data-ttu-id="5c940-180">将机器人集成到会议生命周期</span><span class="sxs-lookup"><span data-stu-id="5c940-180">Integrate bots into the meeting lifecycle</span></span>

<span data-ttu-id="5c940-181">在群聊范围内启用的聊天机器人开始在会议中运行。</span><span class="sxs-lookup"><span data-stu-id="5c940-181">Bots enabled in groupchat scope start functioning in meetings.</span></span> <span data-ttu-id="5c940-182">若要实现机器人，请从[生成自动程序开始](../build-your-first-app/build-bot.md)，然后继续为会议[创建Teams应用](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-references)。</span><span class="sxs-lookup"><span data-stu-id="5c940-182">To implement bots, start with [build a bot](../build-your-first-app/build-bot.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-references).</span></span>

### <a name="integrate-messaging-extensions-into-the-meeting-lifecycle"></a><span data-ttu-id="5c940-183">将消息传递扩展集成到会议生命周期</span><span class="sxs-lookup"><span data-stu-id="5c940-183">Integrate messaging extensions into the meeting lifecycle</span></span>

<span data-ttu-id="5c940-184">若要实现消息传递扩展，请从[构建](../messaging-extensions/how-to/create-messaging-extension.md)消息传递扩展开始，然后继续为会议[创建Teams应用](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-references)。</span><span class="sxs-lookup"><span data-stu-id="5c940-184">To implement messaging extensions, start with [build a messaging extension](../messaging-extensions/how-to/create-messaging-extension.md) and then continue with [create apps for Teams meetings](../apps-in-teams-meetings/create-apps-for-teams-meetings.md#meeting-apps-api-references).</span></span>

<span data-ttu-id="5c940-185">会议Teams可扩展性允许你根据会议中的参与者角色设计应用。</span><span class="sxs-lookup"><span data-stu-id="5c940-185">The Teams meeting app extensibility allows you to design your app based on participant roles in a meeting.</span></span>

## <a name="participant-roles-in-a-meeting"></a><span data-ttu-id="5c940-186">会议中的参与者角色</span><span class="sxs-lookup"><span data-stu-id="5c940-186">Participant roles in a meeting</span></span>

![会议参与者](../assets/images/apps-in-meetings/participant-roles.png)

<span data-ttu-id="5c940-188">默认参与者设置由组织的 IT 管理员确定。</span><span class="sxs-lookup"><span data-stu-id="5c940-188">Default participant settings are determined by an organization's IT administrator.</span></span> <span data-ttu-id="5c940-189">以下是会议中的参与者角色：</span><span class="sxs-lookup"><span data-stu-id="5c940-189">The following are the participant roles in a meeting:</span></span>

* <span data-ttu-id="5c940-190">**组织者**：组织者安排会议、设置会议选项、分配会议角色和启动会议。</span><span class="sxs-lookup"><span data-stu-id="5c940-190">**Organizer**: The organizer schedules a meeting, sets the meeting options, assigns meeting roles, and starts the meeting.</span></span> <span data-ttu-id="5c940-191">只有拥有 M365 帐户Teams许可证的用户才能成为组织者，并控制与会者权限。</span><span class="sxs-lookup"><span data-stu-id="5c940-191">Only users with M365 account and Teams license can be organizers, and control attendee permissions.</span></span> <span data-ttu-id="5c940-192">会议组织者可以更改特定会议的设置。</span><span class="sxs-lookup"><span data-stu-id="5c940-192">A meeting organizer can change the settings for a specific meeting.</span></span> <span data-ttu-id="5c940-193">组织者可以在"会议选项" **网页上进行** 这些更改。</span><span class="sxs-lookup"><span data-stu-id="5c940-193">Organizers can make these changes on the **Meeting options** web page.</span></span>
* <span data-ttu-id="5c940-194">**演示** 者：演示者具有与排除项相同的组织者功能。</span><span class="sxs-lookup"><span data-stu-id="5c940-194">**Presenter**: Presenters have same capabilities of organizers with exclusions.</span></span> <span data-ttu-id="5c940-195">演示者无法从会话中删除组织者或修改会话的会议选项。</span><span class="sxs-lookup"><span data-stu-id="5c940-195">A presenter cannot remove an organizer from the session or modify meeting options for the session.</span></span> <span data-ttu-id="5c940-196">默认情况下，加入会议的参与者具有演示者角色。</span><span class="sxs-lookup"><span data-stu-id="5c940-196">By default, participants joining a meeting have the presenter role.</span></span>
* <span data-ttu-id="5c940-197">**与会者**：与会者是受邀参加会议但无权担任演示者的用户。</span><span class="sxs-lookup"><span data-stu-id="5c940-197">**Attendee**: An attendee is a user who has been invited to attend a meeting but is not authorized to act as a presenter.</span></span> <span data-ttu-id="5c940-198">与会者可以与其他会议成员交互，但不能管理任何会议设置或共享内容。</span><span class="sxs-lookup"><span data-stu-id="5c940-198">Attendees can interact with other meeting members but cannot manage any of the meeting settings or share content.</span></span>

> [!NOTE]
> <span data-ttu-id="5c940-199">只有组织者或演示者才能添加、删除或卸载应用。</span><span class="sxs-lookup"><span data-stu-id="5c940-199">Only an organizer or presenter can add, remove, or uninstall apps.</span></span>

<span data-ttu-id="5c940-200">有关详细信息，请参阅[会议Teams角色](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019)。</span><span class="sxs-lookup"><span data-stu-id="5c940-200">For more information, see [roles in a Teams meeting](https://support.microsoft.com/office/roles-in-a-teams-meeting-c16fa7d0-1666-4dde-8686-0a0bfe16e019).</span></span>

<span data-ttu-id="5c940-201">在基于会议中的参与者角色设计应用后，你可以为会议标识每个用户类型并选择他们可以访问的类型。</span><span class="sxs-lookup"><span data-stu-id="5c940-201">After you design your app based on participant roles in a meeting, you can identify each user type for meetings and select what they can access.</span></span>

## <a name="user-types-in-a-meeting"></a><span data-ttu-id="5c940-202">会议中的用户类型</span><span class="sxs-lookup"><span data-stu-id="5c940-202">User types in a meeting</span></span>

> [!NOTE]
> <span data-ttu-id="5c940-203">用户类型不包含在 **getParticipantRole** API 中。</span><span class="sxs-lookup"><span data-stu-id="5c940-203">The user type is not included in the **getParticipantRole** API.</span></span>

<span data-ttu-id="5c940-204">会议中的用户类型（如组织者、演示者或与会者）可以在会议中执行其中一 [个参与者角色](#participant-roles-in-a-meeting)。</span><span class="sxs-lookup"><span data-stu-id="5c940-204">User types, such as, organizer, presenter, or attendee in a meeting can perform one of the [participant roles in a meeting](#participant-roles-in-a-meeting).</span></span>

<span data-ttu-id="5c940-205">以下列表详细介绍了不同的用户类型及其辅助功能和性能：</span><span class="sxs-lookup"><span data-stu-id="5c940-205">The following list details the different user types along with their accessibility and performance:</span></span>

* <span data-ttu-id="5c940-206">**租户内**：租户内用户属于组织，在租户的 AAD Azure Active Directory () 凭据。</span><span class="sxs-lookup"><span data-stu-id="5c940-206">**In-tenant**: In-tenant users belong to the organization and have credentials in Azure Active Directory (AAD) for the tenant.</span></span> <span data-ttu-id="5c940-207">他们通常是全职、现场或远程员工。</span><span class="sxs-lookup"><span data-stu-id="5c940-207">They are usually full-time, onsite, or remote employees.</span></span> <span data-ttu-id="5c940-208">租户内用户可以是组织者、演示者或与会者。</span><span class="sxs-lookup"><span data-stu-id="5c940-208">An in-tenant user can be an organizer, presenter, or attendee.</span></span>
* <span data-ttu-id="5c940-209">**来宾**：来宾是受邀访问组织租户中的Teams或其他资源的另一个组织的参与者。</span><span class="sxs-lookup"><span data-stu-id="5c940-209">**Guest**: A guest is a participant from another organization invited to access Teams or other resources in the organization's tenant.</span></span> <span data-ttu-id="5c940-210">来宾将添加到组织的 AAD，并且具有与Teams团队成员相同的功能，可以访问团队聊天、会议和文件。</span><span class="sxs-lookup"><span data-stu-id="5c940-210">Guests are added to the organization’s AAD and have same Teams capabilities as a native team member with access to team chats, meetings, and files.</span></span> <span data-ttu-id="5c940-211">来宾用户可以是组织者、演示者或与会者。</span><span class="sxs-lookup"><span data-stu-id="5c940-211">A guest user can be an organizer, presenter, or attendee.</span></span> <span data-ttu-id="5c940-212">有关详细信息，请参阅 Teams 中的[来宾访问](/microsoftteams/guest-access)。</span><span class="sxs-lookup"><span data-stu-id="5c940-212">For more information, see [guest access in Teams](/microsoftteams/guest-access).</span></span>
* <span data-ttu-id="5c940-213">**联盟或外部**：联盟用户是Teams组织中受邀加入会议的外部用户。</span><span class="sxs-lookup"><span data-stu-id="5c940-213">**Federated or external**: A federated user is an external Teams user in another organization who has been invited to join a meeting.</span></span> <span data-ttu-id="5c940-214">联盟用户具有联盟伙伴的有效凭据，并且由联盟Teams。</span><span class="sxs-lookup"><span data-stu-id="5c940-214">Federated users have valid credentials with federated partners and are authorized by Teams.</span></span> <span data-ttu-id="5c940-215">他们无法访问你的团队或组织的其他共享资源。</span><span class="sxs-lookup"><span data-stu-id="5c940-215">They do not have access to your teams or other shared resources from your organization.</span></span> <span data-ttu-id="5c940-216">对于外部用户来说，来宾访问是访问团队和频道的更好选择。</span><span class="sxs-lookup"><span data-stu-id="5c940-216">Guest access is a better option for external users to have access to teams and channels.</span></span> <span data-ttu-id="5c940-217">有关详细信息，请参阅管理[Teams 中的外部访问](/microsoftteams/manage-external-access)。</span><span class="sxs-lookup"><span data-stu-id="5c940-217">For more information, see [manage external access in Teams](/microsoftteams/manage-external-access).</span></span>

    > [!NOTE]
    > <span data-ttu-id="5c940-218">你的Teams用户可以在主持与其他组织的会议或聊天时添加应用。</span><span class="sxs-lookup"><span data-stu-id="5c940-218">Your Teams users can add apps when they host meetings or chats with other organizations.</span></span> <span data-ttu-id="5c940-219">当用户加入由其他组织托管的会议或聊天时，用户可以使用由外部用户共享的应用。</span><span class="sxs-lookup"><span data-stu-id="5c940-219">The users can use apps shared by external users when your users join meetings or chats hosted by other organizations.</span></span> <span data-ttu-id="5c940-220">托管用户组织的数据策略以及该用户组织共享的第三方应用的数据共享做法将生效。</span><span class="sxs-lookup"><span data-stu-id="5c940-220">The data policies of the hosting user's organization, as well as the data sharing practices of the third-party apps shared by that user's organization, will be in effect.</span></span>

* <span data-ttu-id="5c940-221">**匿名**：匿名用户没有 AAD 标识，并且未与租户联盟。</span><span class="sxs-lookup"><span data-stu-id="5c940-221">**Anonymous**: Anonymous users do not have an AAD identity and are not federated with a tenant.</span></span> <span data-ttu-id="5c940-222">匿名参与者与外部用户类似，但其身份不会在会议中预测。</span><span class="sxs-lookup"><span data-stu-id="5c940-222">The anonymous participants are like external users, but their identity is not projected in the meeting.</span></span> <span data-ttu-id="5c940-223">匿名用户无法访问会议窗口中的应用。</span><span class="sxs-lookup"><span data-stu-id="5c940-223">Anonymous users are not able to access apps in a meeting window.</span></span> <span data-ttu-id="5c940-224">匿名用户不能是组织者，但可以是演示者或与会者。</span><span class="sxs-lookup"><span data-stu-id="5c940-224">An anonymous user cannot be an organizer but can be a presenter or attendee.</span></span>

    > [!NOTE]
    > <span data-ttu-id="5c940-225">匿名用户继承全局默认用户级别应用程序权限策略。</span><span class="sxs-lookup"><span data-stu-id="5c940-225">Anonymous users inherit the global default user-level app permission policy.</span></span> <span data-ttu-id="5c940-226">有关详细信息，请参阅管理 [应用](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access)。</span><span class="sxs-lookup"><span data-stu-id="5c940-226">For more information, see [manage Apps](/microsoftteams/non-standard-users#anonymous-user-in-meetings-access).</span></span>

<span data-ttu-id="5c940-227">来宾或匿名用户无法添加、删除或卸载应用。</span><span class="sxs-lookup"><span data-stu-id="5c940-227">A guest or anonymous user cannot add, remove, or uninstall apps.</span></span>

<span data-ttu-id="5c940-228">下表提供了用户类型以及每个用户可以访问的功能：</span><span class="sxs-lookup"><span data-stu-id="5c940-228">The following table provides the user types and what features each user can access:</span></span>

| <span data-ttu-id="5c940-229">用户类型</span><span class="sxs-lookup"><span data-stu-id="5c940-229">User type</span></span> | <span data-ttu-id="5c940-230">选项卡</span><span class="sxs-lookup"><span data-stu-id="5c940-230">Tabs</span></span> | <span data-ttu-id="5c940-231">机器人</span><span class="sxs-lookup"><span data-stu-id="5c940-231">Bots</span></span> | <span data-ttu-id="5c940-232">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="5c940-232">Messaging extensions</span></span> | <span data-ttu-id="5c940-233">自适应卡</span><span class="sxs-lookup"><span data-stu-id="5c940-233">Adaptive Cards</span></span> | <span data-ttu-id="5c940-234">任务模块</span><span class="sxs-lookup"><span data-stu-id="5c940-234">Task modules</span></span> | <span data-ttu-id="5c940-235">会议内的对话框</span><span class="sxs-lookup"><span data-stu-id="5c940-235">In-meeting dialog</span></span> |
| :-- | :-- | :-- | :-- | :-- | :-- | :-- |
| <span data-ttu-id="5c940-236">匿名用户</span><span class="sxs-lookup"><span data-stu-id="5c940-236">Anonymous user</span></span> | <span data-ttu-id="5c940-237">不可用</span><span class="sxs-lookup"><span data-stu-id="5c940-237">Not available</span></span> | <span data-ttu-id="5c940-238">不可用</span><span class="sxs-lookup"><span data-stu-id="5c940-238">Not available</span></span> | <span data-ttu-id="5c940-239">不可用</span><span class="sxs-lookup"><span data-stu-id="5c940-239">Not available</span></span> | <span data-ttu-id="5c940-240">允许会议聊天中的交互。</span><span class="sxs-lookup"><span data-stu-id="5c940-240">Interactions in the meeting chat are allowed.</span></span> | <span data-ttu-id="5c940-241">允许通过自适应卡片在会议聊天中交互。</span><span class="sxs-lookup"><span data-stu-id="5c940-241">Interactions in the meeting chat from an Adaptive Card are allowed.</span></span> | <span data-ttu-id="5c940-242">不可用</span><span class="sxs-lookup"><span data-stu-id="5c940-242">Not available</span></span> |
| <span data-ttu-id="5c940-243">属于租户 AAD 的来宾</span><span class="sxs-lookup"><span data-stu-id="5c940-243">Guest that is part of the tenant AAD</span></span> | <span data-ttu-id="5c940-244">允许交互。</span><span class="sxs-lookup"><span data-stu-id="5c940-244">Interaction is allowed.</span></span> <span data-ttu-id="5c940-245">不允许创建、更新和删除。</span><span class="sxs-lookup"><span data-stu-id="5c940-245">Creating, updating, and deleting are not allowed.</span></span> | <span data-ttu-id="5c940-246">不可用</span><span class="sxs-lookup"><span data-stu-id="5c940-246">Not available</span></span> | <span data-ttu-id="5c940-247">不可用</span><span class="sxs-lookup"><span data-stu-id="5c940-247">Not available</span></span> | <span data-ttu-id="5c940-248">允许会议聊天中的交互。</span><span class="sxs-lookup"><span data-stu-id="5c940-248">Interactions in the meeting chat are allowed.</span></span> | <span data-ttu-id="5c940-249">允许通过自适应卡片在会议聊天中交互。</span><span class="sxs-lookup"><span data-stu-id="5c940-249">Interactions in the meeting chat from an Adaptive Card are allowed.</span></span> | <span data-ttu-id="5c940-250">可用</span><span class="sxs-lookup"><span data-stu-id="5c940-250">Available</span></span> |
| <span data-ttu-id="5c940-251">联盟用户。</span><span class="sxs-lookup"><span data-stu-id="5c940-251">Federated user.</span></span> <span data-ttu-id="5c940-252">有关详细信息，请参阅 [非标准用户](/microsoftteams/non-standard-users)。</span><span class="sxs-lookup"><span data-stu-id="5c940-252">For more information, see [non-standard users](/microsoftteams/non-standard-users).</span></span> | <span data-ttu-id="5c940-253">允许交互。</span><span class="sxs-lookup"><span data-stu-id="5c940-253">Interaction is allowed.</span></span> <span data-ttu-id="5c940-254">不允许创建、更新和删除。</span><span class="sxs-lookup"><span data-stu-id="5c940-254">Creating, updating, and deleting are not allowed.</span></span> | <span data-ttu-id="5c940-255">允许交互。</span><span class="sxs-lookup"><span data-stu-id="5c940-255">Interaction is allowed.</span></span> <span data-ttu-id="5c940-256">不允许获取、更新和删除。</span><span class="sxs-lookup"><span data-stu-id="5c940-256">Acquiring, updating, and deleting are not allowed.</span></span> | <span data-ttu-id="5c940-257">不可用</span><span class="sxs-lookup"><span data-stu-id="5c940-257">Not available</span></span> | <span data-ttu-id="5c940-258">允许会议聊天中的交互。</span><span class="sxs-lookup"><span data-stu-id="5c940-258">Interactions in the meeting chat are allowed.</span></span> | <span data-ttu-id="5c940-259">允许通过自适应卡片在会议聊天中交互。</span><span class="sxs-lookup"><span data-stu-id="5c940-259">Interactions in the meeting chat from an Adaptive Card are allowed.</span></span> | <span data-ttu-id="5c940-260">不可用</span><span class="sxs-lookup"><span data-stu-id="5c940-260">Not available</span></span> |

## <a name="see-also"></a><span data-ttu-id="5c940-261">另请参阅</span><span class="sxs-lookup"><span data-stu-id="5c940-261">See also</span></span>

* [<span data-ttu-id="5c940-262">Tab</span><span class="sxs-lookup"><span data-stu-id="5c940-262">Tab</span></span>](../tabs/what-are-tabs.md#understand-how-tabs-work)
* [<span data-ttu-id="5c940-263">Bot</span><span class="sxs-lookup"><span data-stu-id="5c940-263">Bot</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="5c940-264">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="5c940-264">Messaging extension</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="5c940-265">设计应用</span><span class="sxs-lookup"><span data-stu-id="5c940-265">Design your app</span></span>](../apps-in-teams-meetings/design/designing-apps-in-meetings.md)

## <a name="next-step"></a><span data-ttu-id="5c940-266">后续步骤</span><span class="sxs-lookup"><span data-stu-id="5c940-266">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="5c940-267">Teams 会议中应用的先决条件和 API 参考</span><span class="sxs-lookup"><span data-stu-id="5c940-267">Prerequisites and API references for apps in Teams meetings</span></span>](create-apps-for-teams-meetings.md)