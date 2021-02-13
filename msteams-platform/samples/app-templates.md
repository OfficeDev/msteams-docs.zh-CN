---
title: Microsoft Teams 应用模板
description: Microsoft Teams 平台的应用模板的链接和说明
ms.topic: reference
keywords: Microsoft Teams 模板示例演示
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 21721848ba7893380ac217b5f47ce6a6e669e869
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231636"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="420f7-104">Microsoft Teams 的应用模板</span><span class="sxs-lookup"><span data-stu-id="420f7-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="420f7-105">应用模板是 Microsoft Teams 的完整应用示例，这些应用是开源的，在 GitHub 上可用。</span><span class="sxs-lookup"><span data-stu-id="420f7-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="420f7-106">每个应用模板都包含有关为组织部署和安装该应用的详细说明。</span><span class="sxs-lookup"><span data-stu-id="420f7-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="420f7-107">它还提供可立即安装并开始使用的示例应用。</span><span class="sxs-lookup"><span data-stu-id="420f7-107">It also provides a sample app that you can install and begin using immediately.</span></span> <span data-ttu-id="420f7-108">完整的源代码也可用，这允许你详细浏览它或分叉代码并更改它以满足你的特定要求。</span><span class="sxs-lookup"><span data-stu-id="420f7-108">The complete source code is available too, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="420f7-109">所有应用模板都根据 MIT 许可 [条款](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) 提供。</span><span class="sxs-lookup"><span data-stu-id="420f7-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>
>[!NOTE] 
><span data-ttu-id="420f7-110">你，而不是 Microsoft 必须许可和支持通过用户和组织的应用模板创建的应用。</span><span class="sxs-lookup"><span data-stu-id="420f7-110">You, not Microsoft must license and support apps created from app templates for your users and organizations.</span></span>

<span data-ttu-id="420f7-111">**&#9734;指示新发布的应用模板。**</span><span class="sxs-lookup"><span data-stu-id="420f7-111">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="420f7-112">主要优势</span><span class="sxs-lookup"><span data-stu-id="420f7-112">Key benefits</span></span>

* <span data-ttu-id="420f7-113">**直接部署到云：** 所有应用模板均包括部署脚本，允许你在 Microsoft Azure 或 Power Platform 中托管所有必需服务。</span><span class="sxs-lookup"><span data-stu-id="420f7-113">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="420f7-114">**建议的示例代码：** 应用模板符合有关安全性和基础结构的建议最佳做法。</span><span class="sxs-lookup"><span data-stu-id="420f7-114">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="420f7-115">将审查所有社区提交的应用模板更改，以确保一致性。</span><span class="sxs-lookup"><span data-stu-id="420f7-115">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="420f7-116">**可自定义和可扩展：** 虽然所有应用模板都可以以最少的配置进行部署，但我们提供了整个代码库和部署脚本，以便你可以轻松地自定义或扩展它们以满足你的独特需求。</span><span class="sxs-lookup"><span data-stu-id="420f7-116">**Customizable and extensible:** While all app templates can be deployed with minimal configuration, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="420f7-117">**详细文档：** 所有应用模板都附带了有关解决方案体系结构、部署和配置步骤的端到端文档。</span><span class="sxs-lookup"><span data-stu-id="420f7-117">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot-9734"></a><span data-ttu-id="420f7-118">采用自动程序&#9734;</span><span class="sxs-lookup"><span data-stu-id="420f7-118">Adoption Bot &#9734;</span></span>

<span data-ttu-id="420f7-119">采用自动程序是使用 Power Virtual Agent for Teams (PVA) 构建的用户关注聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="420f7-119">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams (PVA).</span></span> <span data-ttu-id="420f7-120">它可视为常见问题增强版的 PVA 版本。</span><span class="sxs-lookup"><span data-stu-id="420f7-120">It can be considered as the PVA version of FAQPlus.</span></span> <span data-ttu-id="420f7-121">采用自动程序解答了 100 多个有关 Microsoft 365 和 Teams 的常见问题。</span><span class="sxs-lookup"><span data-stu-id="420f7-121">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="420f7-122">你可以编辑包含的主题、添加你自己的主题和加入现有常见问题解答。</span><span class="sxs-lookup"><span data-stu-id="420f7-122">You can edit the included topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="420f7-123">如果用户需要额外的帮助，采用机器人可以将其连接到专家，甚至可以扩展为使用高级流连接器打开服务票证。</span><span class="sxs-lookup"><span data-stu-id="420f7-123">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.</span></span>

[<span data-ttu-id="420f7-124">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-124">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="appointment-manager-9734"></a><span data-ttu-id="420f7-125">约会管理器&#9734;</span><span class="sxs-lookup"><span data-stu-id="420f7-125">Appointment Manager &#9734;</span></span>

<span data-ttu-id="420f7-126">约会管理器是一个 Teams 应用模板，可帮助企业通过 Teams 创建、管理和与消费者进行虚拟约会。</span><span class="sxs-lookup"><span data-stu-id="420f7-126">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="420f7-127">来自消费者的新约会请求在 Teams 频道中可见，可在这些频道中快速分配和重新分配到团队中的员工。</span><span class="sxs-lookup"><span data-stu-id="420f7-127">New appointment requests from consumers are visible in Teams channels, where they can quickly be assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="420f7-128">可以通过自定义选项卡在团队或个人级别查看约会请求。</span><span class="sxs-lookup"><span data-stu-id="420f7-128">Appointment requests can be viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="420f7-129">每个约会都与 Teams 联机会议关联，因此员工和使用者可以在计划的时间轻松加入会议。</span><span class="sxs-lookup"><span data-stu-id="420f7-129">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="420f7-130">该应用模板与 Microsoft Bookings 集成，便于约会管理。</span><span class="sxs-lookup"><span data-stu-id="420f7-130">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="420f7-131">安排的约会会自动显示在已分配员工的日历上，并且消费者会收到包含嵌入式会议链接的可自定义电子邮件通知和提醒。</span><span class="sxs-lookup"><span data-stu-id="420f7-131">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="420f7-132">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-132">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="420f7-133">![Teams 中的 ](../assets/images/appointment-manager-overview.png)
 ![ 约会管理器概述约会管理器](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="420f7-133">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="420f7-134">询问离开</span><span class="sxs-lookup"><span data-stu-id="420f7-134">Ask Away</span></span>

<span data-ttu-id="420f7-135">"离开"是 [一](../bots/what-are-bots.md) 个 Microsoft Teams 机器人，允许用户在 Teams 中&问答 (问答) 问答。</span><span class="sxs-lookup"><span data-stu-id="420f7-135">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Q&A (Question and Answer) sessions within Teams.</span></span> <span data-ttu-id="420f7-136">使用"询问离开"自动程序，团队成员可以提交和投票给同事共享的问题，从而允许问答&主机在频道或聊天中轻松收集首要问题。</span><span class="sxs-lookup"><span data-stu-id="420f7-136">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="420f7-137">机器人可用于在 Teams&会话进行实时问答，并允许与会者通过聊天实时提交问题。</span><span class="sxs-lookup"><span data-stu-id="420f7-137">The bot can be used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live via chat.</span></span>

[<span data-ttu-id="420f7-138">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-138">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![用户对问题进行投票的排行榜弹出对话框视图](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="420f7-140">员工见解</span><span class="sxs-lookup"><span data-stu-id="420f7-140">Associate Insights</span></span>

<span data-ttu-id="420f7-141">关联见解是一个 [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) 模板，它使一线工作人员可以直接捕获和提交客户意见、情绪和感知。</span><span class="sxs-lookup"><span data-stu-id="420f7-141">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="420f7-142">一线员工通常是第一个在一对一联系点与客户互动的公司代表。</span><span class="sxs-lookup"><span data-stu-id="420f7-142">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="420f7-143">业务团队可以共享和协作使用收集的数据，例如通过 Power BI Teams 选项卡，以改进产品并增强客户体验。</span><span class="sxs-lookup"><span data-stu-id="420f7-143">The collected data can be shared and used collaboratively by business teams, e.g., via a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="420f7-144">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-144">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![应用生成的见解的反馈视图](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![应用生成的见解的 Power BI 视图](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a><span data-ttu-id="420f7-147">考勤</span><span class="sxs-lookup"><span data-stu-id="420f7-147">Attendance</span></span>

<span data-ttu-id="420f7-148">"出席"应用是可在团队中固定的"Power [Apps"](/powerapps/maker/canvas-apps/embed-teams-app) 选项卡。</span><span class="sxs-lookup"><span data-stu-id="420f7-148">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that can be pinned in a team.</span></span> <span data-ttu-id="420f7-149">它旨在记录状态，通常位于学习和培训环境等设置中。</span><span class="sxs-lookup"><span data-stu-id="420f7-149">It is designed to record presence, typically in settings such as learning and training environments.</span></span> <span data-ttu-id="420f7-150">用户可以标记或编辑过去最多 30 天的出席情况，并查看整个组或单个与会者的汇总出席报告。</span><span class="sxs-lookup"><span data-stu-id="420f7-150">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span>

[<span data-ttu-id="420f7-151">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-151">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-attendance)

![出席应用演示](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="420f7-153">会议室预订</span><span class="sxs-lookup"><span data-stu-id="420f7-153">Book-a-room</span></span>

<span data-ttu-id="420f7-154">会议室预订是一个 [Microsoft Teams](../bots/what-are-bots.md) 自动程序，用户可以从当前时间开始快速查找和保留 30 (默认) 、60 或 90 分钟的会议室。</span><span class="sxs-lookup"><span data-stu-id="420f7-154">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that lets users quickly find and reserve a meeting room for 30 (default), 60, or 90 minutes starting from the current  time.</span></span> <span data-ttu-id="420f7-155">会议室预订自动程序的范围为个人对话或一对一对话。</span><span class="sxs-lookup"><span data-stu-id="420f7-155">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span>

[<span data-ttu-id="420f7-156">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-156">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)

![会议室预订演示](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="420f7-158">生成访问</span><span class="sxs-lookup"><span data-stu-id="420f7-158">Building Access</span></span>

<span data-ttu-id="420f7-159">Building Access 是一款基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)的应用，它通过允许设施控制器管理、跟踪和报告员工现场状态，支持管理建筑物占用阈值和社会性距离规范。</span><span class="sxs-lookup"><span data-stu-id="420f7-159">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="420f7-160">使用 Microsoft Power [Apps](/powerapps/powerapps-overview)和 [Power Automate](/power-automate/getting-started)构建的应用与 Microsoft Teams 深度集成，使组织可以确定构建就绪情况、建立现场访问资格标准，并收集未来规划的见解。</span><span class="sxs-lookup"><span data-stu-id="420f7-160">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="420f7-161">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-161">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Building Access 预订卡](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![生成 Access 键视图](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="420f7-164">Celebrations</span><span class="sxs-lookup"><span data-stu-id="420f7-164">Celebrations</span></span>

<span data-ttu-id="420f7-165">庆祝是一款 Teams 应用，可帮助团队成员为彼此的生日、周年纪念和其他定期活动而庆祝。</span><span class="sxs-lookup"><span data-stu-id="420f7-165">Celebrations is a Teams app that helps team members celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="420f7-166">它记住所有团队成员的特殊场合，并发送在事件创建时选择的所有团队中的友好消息，使团队成员在一天中感觉特别。</span><span class="sxs-lookup"><span data-stu-id="420f7-166">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="420f7-167">该应用提供了一个简单界面，供所有团队成员个人添加和查看其事件，还允许用户选择共享事件的团队。</span><span class="sxs-lookup"><span data-stu-id="420f7-167">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="420f7-168">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-168">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="420f7-169">清单</span><span class="sxs-lookup"><span data-stu-id="420f7-169">Checklist</span></span>

<span data-ttu-id="420f7-170">检查表是一个自定义 Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) 消息传递扩展应用，通过此应用，可以在聊天或频道中创建共享清单，从而与团队协作。</span><span class="sxs-lookup"><span data-stu-id="420f7-170">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="420f7-171">该应用在所有 Teams 平台客户端（桌面、浏览器、iOS 和 Android）中均受支持，并且已准备好作为 Microsoft 365 订阅的一部分进行部署。</span><span class="sxs-lookup"><span data-stu-id="420f7-171">The app is supported across all Teams platform clients —  desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="420f7-172">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-172">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app )

:::row:::
:::column span="2":::
    ![在 Teams 视图中创建清单](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in-9734"></a><span data-ttu-id="420f7-174">课堂下拉&#9734;</span><span class="sxs-lookup"><span data-stu-id="420f7-174">Classroom Drop-in &#9734;</span></span>

<span data-ttu-id="420f7-175">课堂下拉列表是基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)的应用，系统领导可根据需要查找课堂团队 (虚拟教室) 并根据需要将自己或其他人添加到这些课堂团队中。</span><span class="sxs-lookup"><span data-stu-id="420f7-175">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams (virtual classrooms) and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="420f7-176">使用 Microsoft [Power Apps](/powerapps/powerapps-overview) 和 [Power Automate](/power-automate/getting-started)构建的应用与 Microsoft Teams 深度集成，以确保教育机构可以针对每个业务要求向课程团队的相关利益干系人提供访问权限，从而优化他们在混合学习环境中的操作。</span><span class="sxs-lookup"><span data-stu-id="420f7-176">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="420f7-177">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-177">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![课堂下拉请求](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="420f7-179">Company Communicator</span><span class="sxs-lookup"><span data-stu-id="420f7-179">Company Communicator</span></span>

<span data-ttu-id="420f7-180">公司Communicator应用允许企业团队通过聊天创建和发送面向多个团队或大量员工的消息，从而允许组织在员工协作的地方与员工联系。</span><span class="sxs-lookup"><span data-stu-id="420f7-180">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="420f7-181">将此模板用于多个方案，例如新计划公告、员工入职培训、新式学习与开发或组织范围的广播。</span><span class="sxs-lookup"><span data-stu-id="420f7-181">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="420f7-182">该应用为指定用户提供了一个简单的界面，用于创建、预览、协作和发送消息。</span><span class="sxs-lookup"><span data-stu-id="420f7-182">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="420f7-183">它为构建自定义目标通信功能（如自定义遥测）提供了一个基础，这些功能基于确认或与邮件交互的用户数。</span><span class="sxs-lookup"><span data-stu-id="420f7-183">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="420f7-184">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-184">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator撰写框视图](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="420f7-186">联系人组查找</span><span class="sxs-lookup"><span data-stu-id="420f7-186">Contact Group Lookup</span></span>

<span data-ttu-id="420f7-187">联系人组查找应用提供了一种便捷且有用的方法，用于创建、访问和管理组织的联系人组 (以前称为通讯组列表或通讯组) 。</span><span class="sxs-lookup"><span data-stu-id="420f7-187">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups (formerly known as distribution lists or communication groups).</span></span> <span data-ttu-id="420f7-188">用户可以在 Teams 环境中快速查看和与团队成员聊天、查看成员状态，以及创建与联系人组中选定成员的群聊。</span><span class="sxs-lookup"><span data-stu-id="420f7-188">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="420f7-189">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-189">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

:::row:::
:::column span="2":::
    ![联系人组查找固定收藏夹视图](../assets/images/contact-group-lookup-favorites.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![联系人组查找开始聊天演示](../assets/images/contact-group-lookup-chat.png)
:::column-end:::
:::row-end:::

## <a name="co-worker-appreciation-9734"></a><span data-ttu-id="420f7-192">同事的"共同&#9734;</span><span class="sxs-lookup"><span data-stu-id="420f7-192">Co-worker Appreciation &#9734;</span></span>

<span data-ttu-id="420f7-193">使用 Microsoft Teams 中的同事认可模板，用户可以在 Teams 上下文中识别同事的成就。</span><span class="sxs-lookup"><span data-stu-id="420f7-193">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="420f7-194">当同事选择奖励同事时，将在频道对话中标记收件人和其他团队成员，并收到有关频道的奖励详细信息的通知。</span><span class="sxs-lookup"><span data-stu-id="420f7-194">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="420f7-195">奖励记录在 Teams 应用中，安全、便携且易于共享。</span><span class="sxs-lookup"><span data-stu-id="420f7-195">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="420f7-196">这可视为基于 PowerApps 的开放锁屏提醒应用模板版本，具有排行榜。</span><span class="sxs-lookup"><span data-stu-id="420f7-196">This can be considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="420f7-197">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-197">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![整体](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="420f7-199">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="420f7-199">CrowdSourcer</span></span>

<span data-ttu-id="420f7-200">CrowdSourcer 是 [一](../bots/what-are-bots.md) 个 Microsoft Teams 机器人，它向团队提供协作从团队成员获取的查询信息。</span><span class="sxs-lookup"><span data-stu-id="420f7-200">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="420f7-201">这是一种很好的方法，可以回答常见问题，同时使参与者能够积极参与并参与一个有趣且有用的信息资源。</span><span class="sxs-lookup"><span data-stu-id="420f7-201">It's a great way to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="420f7-202">在 Github 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-202">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![群源最终用户交互](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="420f7-204">自定义贴纸</span><span class="sxs-lookup"><span data-stu-id="420f7-204">Custom Stickers</span></span>

<span data-ttu-id="420f7-205">自我表达是健康团队文化的核心。</span><span class="sxs-lookup"><span data-stu-id="420f7-205">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="420f7-206">此应用模板是 [一个消息](~/messaging-extensions/what-are-messaging-extensions.md) 扩展，允许用户在 Microsoft Teams 内使用自定义贴纸和 GIF。</span><span class="sxs-lookup"><span data-stu-id="420f7-206">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="420f7-207">此模板提供了一种基于 Web 的轻松配置体验，具有配置访问权限的任何人都可以上载他们希望最终用户拥有的 GIF/贴纸/图像，从而允许整个团队使用你选择的任何一组贴纸。</span><span class="sxs-lookup"><span data-stu-id="420f7-207">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs/stickers/images they want their end-users to have, allowing your entire team to use any set of stickers you chose.</span></span>

<span data-ttu-id="420f7-208">此应用程序还支持跨团队轻松共享图像/GIF/贴纸，而无需访问 SharePoint 网站或作为存储和共享机制的单个通道。</span><span class="sxs-lookup"><span data-stu-id="420f7-208">This app also enables easy sharing of images/GIFs/stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="420f7-209">例如，产品团队可以轻松地以编程方式将产品图像和 GIF 共享到社交媒体、市场营销和销售团队。</span><span class="sxs-lookup"><span data-stu-id="420f7-209">For example, product teams can easily share product images and GIFs to social media, marketing and sales teams programmatically.</span></span> <span data-ttu-id="420f7-210">当提供新图像/GIF 时，还可以通过向特定团队/个人触发通知流来扩展此应用。</span><span class="sxs-lookup"><span data-stu-id="420f7-210">One can also extend this app by triggering a notification flow to specific teams/individuals when new images/GIFs are made available.</span></span>

[<span data-ttu-id="420f7-211">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-211">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![贴纸应用](../assets/images/stickers.png)

## <a name="employee-ideas-9734"></a><span data-ttu-id="420f7-213">员工想法&#9734;</span><span class="sxs-lookup"><span data-stu-id="420f7-213">Employee Ideas &#9734;</span></span>

<span data-ttu-id="420f7-214">"员工想法"应用是基于 Azure 的"创意"应用模板的 PowerApps 版本。</span><span class="sxs-lookup"><span data-stu-id="420f7-214">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="420f7-215">通过该应用，Teams 用户可以设置和配置创意活动。</span><span class="sxs-lookup"><span data-stu-id="420f7-215">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="420f7-216">想法活动是围绕常见主题对想法进行分组的类别。</span><span class="sxs-lookup"><span data-stu-id="420f7-216">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="420f7-217">Teams 用户还可以执行以下活动：</span><span class="sxs-lookup"><span data-stu-id="420f7-217">Teams users can also perform following activities:</span></span>
* <span data-ttu-id="420f7-218">配置员工需要为每个想法提交的标准提交表单。</span><span class="sxs-lookup"><span data-stu-id="420f7-218">Configure a standard submission form that employees need to submit for each idea.</span></span> 
* <span data-ttu-id="420f7-219">查看和管理市场活动的想法和列表。</span><span class="sxs-lookup"><span data-stu-id="420f7-219">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="420f7-220">修改和删除市场活动。</span><span class="sxs-lookup"><span data-stu-id="420f7-220">Modify and delete campaigns.</span></span>
* <span data-ttu-id="420f7-221">审阅想法领导板。</span><span class="sxs-lookup"><span data-stu-id="420f7-221">Review leader boards of ideas.</span></span>
* <span data-ttu-id="420f7-222">投票讨论并分享优先想法。</span><span class="sxs-lookup"><span data-stu-id="420f7-222">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="420f7-223">提交市场活动想法。</span><span class="sxs-lookup"><span data-stu-id="420f7-223">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="420f7-224">查看其他团队成员的想法。</span><span class="sxs-lookup"><span data-stu-id="420f7-224">View other team member's idea.</span></span>
* <span data-ttu-id="420f7-225">对最喜欢的想法投票。</span><span class="sxs-lookup"><span data-stu-id="420f7-225">Vote on most liked ideas.</span></span>
* <span data-ttu-id="420f7-226">与活动中的其他人相比，查看他们想法的绩效。</span><span class="sxs-lookup"><span data-stu-id="420f7-226">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="420f7-227">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-227">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![管理市场活动视图](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="420f7-229">E-就地</span><span class="sxs-lookup"><span data-stu-id="420f7-229">E-Prescriptions</span></span> 

<span data-ttu-id="420f7-230">电子医疗是一种基于 [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)的应用，它通过自动向患者发布电子医疗方案的过程来增强远程医疗与虚拟医疗。</span><span class="sxs-lookup"><span data-stu-id="420f7-230">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)-based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="420f7-231">医疗专业人员可以直接在 Teams 平台内快速查看约会、生成电子医疗方案以及向患者发送包含电子医疗附件的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="420f7-231">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="420f7-232">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-232">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

:::row:::
:::column span="2":::
    !["电子医疗"应用的屏幕截图。](../assets/images/e-prescriptions-app-template.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    !["电子医疗"应用的屏幕截图。](../assets/images/e-prescriptions-app-template-admin.png)
:::column-end:::
:::row-end:::

## <a name="employee-training"></a><span data-ttu-id="420f7-237">员工培训</span><span class="sxs-lookup"><span data-stu-id="420f7-237">Employee Training</span></span> 

<span data-ttu-id="420f7-238">员工培训是一款 Microsoft Teams 应用，可让组织者轻松发布、跟踪和推广组织的学习和培训活动。</span><span class="sxs-lookup"><span data-stu-id="420f7-238">Employee training is a Microsoft Teams app that enables organizers to easily publish,  track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="420f7-239">借助该应用，事件规划人员可以向事件注册人发送提醒和通知，员工可以指示对即将开始的事件感兴趣，及时了解当前事件，以及通过 Teams 消息扩展与同事共享事件详细信息。</span><span class="sxs-lookup"><span data-stu-id="420f7-239">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues via the Teams messaging extension.</span></span>

[<span data-ttu-id="420f7-240">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-240">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="420f7-241">**查看员工培训计划** ![员工培训选项卡图像](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="420f7-241">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="420f7-242">**创建员工培训计划** ![员工培训创建事件表单](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="420f7-242">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="420f7-243">专家查找器</span><span class="sxs-lookup"><span data-stu-id="420f7-243">Expert Finder</span></span>

<span data-ttu-id="420f7-244">专家查找器是一个 [Microsoft Teams](../bots/what-are-bots.md) 机器人，可基于特定组织成员的技能、兴趣和教育属性识别这些成员。</span><span class="sxs-lookup"><span data-stu-id="420f7-244">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="420f7-245">成员在组织中查找与 Azure Active Directory 用户配置文件的关键字搜索匹配的专家。</span><span class="sxs-lookup"><span data-stu-id="420f7-245">Members find experts within an organization  that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="420f7-246">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-246">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![专家查找器搜索结果演示](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="420f7-248">常见问题 +</span><span class="sxs-lookup"><span data-stu-id="420f7-248">FAQ Plus</span></span>

<span data-ttu-id="420f7-249">对话问答&自动程序是为用户提供常见问题解答的一种简单方法。</span><span class="sxs-lookup"><span data-stu-id="420f7-249">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="420f7-250">但是，大多数机器人无法以有意义的方式与用户互动，因为机器人失败时循环中没有任何人。</span><span class="sxs-lookup"><span data-stu-id="420f7-250">However, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="420f7-251">常见问题解答机器人是一&一个友好的问答，当机器人无法提供帮助时，它会在循环中引入人。</span><span class="sxs-lookup"><span data-stu-id="420f7-251">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="420f7-252">可以询问机器人一个问题，如果问题包含在知识库中，机器人会以答案进行响应。</span><span class="sxs-lookup"><span data-stu-id="420f7-252">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="420f7-253">如果没有，自动程序允许用户提交查询，查询随后将发布给预先配置的专家团队，这些专家通过处理来自团队本身的通知来帮助提供支持。</span><span class="sxs-lookup"><span data-stu-id="420f7-253">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="420f7-254">最新版本的 **FAQ Plus** 支持通过&团队完成以下操作来改进问答解决方案：</span><span class="sxs-lookup"><span data-stu-id="420f7-254">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="420f7-255">&#x2714;使用邮件&将新问答直接添加到知识库。</span><span class="sxs-lookup"><span data-stu-id="420f7-255">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="420f7-256">&#x2714;自动程序&的对编辑和删除问答。</span><span class="sxs-lookup"><span data-stu-id="420f7-256">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="420f7-257">&#x2714;跟踪问答的&历史记录。</span><span class="sxs-lookup"><span data-stu-id="420f7-257">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="420f7-258">&#x2714;配置答案，并添加其他详细信息以显示为 [自适应卡片](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)。</span><span class="sxs-lookup"><span data-stu-id="420f7-258">&#x2714; Configure an answer with additional details to display as an [adaptive card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="420f7-259">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-259">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![FAQ Plus gif](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app-9734"></a><span data-ttu-id="420f7-261">获取支持应用&#9734;</span><span class="sxs-lookup"><span data-stu-id="420f7-261">Get Support App &#9734;</span></span>

<span data-ttu-id="420f7-262">使用 Microsoft Teams 的组织可以使用"获取支持"应用，以允许任何一组用户向监督员请求帮助。</span><span class="sxs-lookup"><span data-stu-id="420f7-262">The Get Support app can be used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="420f7-263">此应用包括各种功能，例如：</span><span class="sxs-lookup"><span data-stu-id="420f7-263">This app includes various features, such as:</span></span>
-   <span data-ttu-id="420f7-264">从 Power App 请求有关不同类别的帮助</span><span class="sxs-lookup"><span data-stu-id="420f7-264">Requesting assistance on different categories from a Power App</span></span>
-   <span data-ttu-id="420f7-265">发送给请求者的通知，告知他们已分配了谁</span><span class="sxs-lookup"><span data-stu-id="420f7-265">Notifications sent to requestors informing them of who has been assigned</span></span> 
-   <span data-ttu-id="420f7-266">发送给指定监督员的通知，告知他们谁需要帮助</span><span class="sxs-lookup"><span data-stu-id="420f7-266">Notifications sent to assigned supervisors informing them of who needs assistance</span></span> 
-   <span data-ttu-id="420f7-267">分析 SharePoint 和 PowerBI 中的升级和模式</span><span class="sxs-lookup"><span data-stu-id="420f7-267">Analyzing escalations and patterns in SharePoint and PowerBI</span></span>

[<span data-ttu-id="420f7-268">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-268">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![获取支持 Gif](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="420f7-270">目标跟踪程序</span><span class="sxs-lookup"><span data-stu-id="420f7-270">Goal Tracker</span></span>

<span data-ttu-id="420f7-271">"目标跟踪程序"应用是一款全面的解决方案，可支持在 Microsoft Teams 中建立目标、观察进度和确认成功。</span><span class="sxs-lookup"><span data-stu-id="420f7-271">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="420f7-272">该应用使用户能够在专业、个人和团队级别设置、跟踪和更新目标。</span><span class="sxs-lookup"><span data-stu-id="420f7-272">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="420f7-273">团队成员还收到及时的提醒和状态更新，保持专注并保持跟踪。</span><span class="sxs-lookup"><span data-stu-id="420f7-273">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="420f7-274">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-274">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

:::row:::
  :::column span="2":::
    ![设置目标](../assets/images/goal-tracker-set-goals-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![查看集目标](../assets/images/goal-tracker-your-goals-view.png)
:::column-end:::
:::row-end:::

## <a name="great-ideas"></a><span data-ttu-id="420f7-277">出色的创意</span><span class="sxs-lookup"><span data-stu-id="420f7-277">Great Ideas</span></span>

<span data-ttu-id="420f7-278">出色的创意应用支持并增强组织中创新与创造力。</span><span class="sxs-lookup"><span data-stu-id="420f7-278">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="420f7-279">利用该应用，员工可以与同事和领导分享想法、发现新提交、聚焦供同事考虑的投稿，并投票选择 Microsoft Teams 中的最佳建议。</span><span class="sxs-lookup"><span data-stu-id="420f7-279">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="420f7-280">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-280">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

:::row:::
  :::column span="2":::
    ![查看提交的想法](../assets/images/great-ideas-all-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![查看想法](../assets/images/great-ideas-digest-view.png)
:::column-end:::
:::row-end:::

## <a name="group-activities"></a><span data-ttu-id="420f7-283">组活动</span><span class="sxs-lookup"><span data-stu-id="420f7-283">Group Activities</span></span>

<span data-ttu-id="420f7-284">组活动是一款 Microsoft Teams 应用，使团队所有者可以轻松在 Microsoft Teams 上下文中快速创建活动组和管理协作工作流。</span><span class="sxs-lookup"><span data-stu-id="420f7-284">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="420f7-285">活动作者可创建活动、在组中随机分配团队成员，并可以选择让机器人发送提醒，直到活动完成。</span><span class="sxs-lookup"><span data-stu-id="420f7-285">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="420f7-286">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-286">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

:::row:::
  :::column span="2":::
    ![Teams 中的组活动列表](../assets/images/group-activities-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![频道中的组活动通知消息](../assets/images/group-activities-2.png)
:::column-end:::
:::row-end:::

## <a name="grow-your-skills"></a><span data-ttu-id="420f7-289">提升技能</span><span class="sxs-lookup"><span data-stu-id="420f7-289">Grow Your Skills</span></span>

<span data-ttu-id="420f7-290">"发展你的技能"应用通过允许员工在同时学习新技能的同时为组织提供补充项目，从而支持专业增长和开发。</span><span class="sxs-lookup"><span data-stu-id="420f7-290">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="420f7-291">员工可以使用该应用在 Teams 环境中找到满足其兴趣、与同事进行有意义的协作以及获得新级别的专业技能和功能的机会。</span><span class="sxs-lookup"><span data-stu-id="420f7-291">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="420f7-292">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-292">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

:::row:::
  :::column span="2":::
    ![可用项目视图](../assets/images/grow-your-skills-all-projects-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![查看者获取的技能视图](../assets/images/grow-your-skills-acquired-skills-view.png)
:::column-end:::
:::row-end:::

## <a name="hr-support"></a><span data-ttu-id="420f7-295">HR 支持</span><span class="sxs-lookup"><span data-stu-id="420f7-295">HR Support</span></span>

<span data-ttu-id="420f7-296">HR 支持机器人是一个友好的&聊天机器人，当人力资源团队无法提供帮助时，它将在循环中引入支持专业人员/专家。</span><span class="sxs-lookup"><span data-stu-id="420f7-296">HR Support bot is a friendly Q&A bot that brings a support professional/expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="420f7-297">可以询问机器人一个问题，如果问题包含在知识库中，机器人会以答案进行响应。</span><span class="sxs-lookup"><span data-stu-id="420f7-297">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="420f7-298">如果没有，自动程序允许用户提交查询，该查询随后将发布在预先配置的专家团队中，这些专家通过处理来自团队自身的通知来帮助提供支持。</span><span class="sxs-lookup"><span data-stu-id="420f7-298">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="420f7-299">此外，自动程序通过搜索问题中的预配置标记来建议指向建议的 HR 策略/问题的链接。</span><span class="sxs-lookup"><span data-stu-id="420f7-299">Additionally, the bot suggests links to recommended HR policies/questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="420f7-300">这些磁贴也可以作为快速参考在关联的选项卡中找到。</span><span class="sxs-lookup"><span data-stu-id="420f7-300">These tiles can also be found in the associated tab as a quick reference.</span></span> <span data-ttu-id="420f7-301">HR 支持适用于轻型 QnA，在组织中启动新项目/计划时可提供快速支持。</span><span class="sxs-lookup"><span data-stu-id="420f7-301">HR Support works well for light weight QnA and to provide quick support when launching new projects/initiatives in the organization.</span></span>

[<span data-ttu-id="420f7-302">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-302">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![HR 支持](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="420f7-304">Icebreaker</span><span class="sxs-lookup"><span data-stu-id="420f7-304">Icebreaker</span></span>

<span data-ttu-id="420f7-305">Icebreaker 是 [一](../bots/what-are-bots.md) 个 Microsoft Teams 机器人，通过每周配对两个随机团队成员来开会，帮助你的团队拉近距离。</span><span class="sxs-lookup"><span data-stu-id="420f7-305">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="420f7-306">自动程序通过自动建议适用于这两个成员的空闲时间来轻松安排。</span><span class="sxs-lookup"><span data-stu-id="420f7-306">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="420f7-307">通过此应用加强个人连接并构建紧密的社区。</span><span class="sxs-lookup"><span data-stu-id="420f7-307">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="420f7-308">除了鼓励整个团队的个人连接之外，Icebreaker 应用还有助于在组织中培养基于兴趣的社区。</span><span class="sxs-lookup"><span data-stu-id="420f7-308">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="420f7-309">例如，你可以将此应用用于 DevOps 兴趣组，以帮助想法和最佳做法在组织中以自然方式传播。</span><span class="sxs-lookup"><span data-stu-id="420f7-309">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="420f7-310">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-310">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Icebreaker 应用](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="420f7-312">奖励</span><span class="sxs-lookup"><span data-stu-id="420f7-312">Incentives</span></span>

<span data-ttu-id="420f7-313">奖励是一个 [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) 模板，用于管理和跟踪鼓励员工参与指定活动，如培训和变更管理计划。</span><span class="sxs-lookup"><span data-stu-id="420f7-313">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities such as trainings and change management initiatives.</span></span> <span data-ttu-id="420f7-314">管理员使用该应用建立指定活动、分配完成分数，并指定奖励所需的资格分数级别。</span><span class="sxs-lookup"><span data-stu-id="420f7-314">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="420f7-315">员工使用该应用查看累积的点数，在达到资格后，请求和申请可兑换奖励。</span><span class="sxs-lookup"><span data-stu-id="420f7-315">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="420f7-316">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-316">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![奖励应用演示](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="420f7-318">事件报告者</span><span class="sxs-lookup"><span data-stu-id="420f7-318">Incident Reporter</span></span>

<span data-ttu-id="420f7-319">事件报告程序 [是 Microsoft Teams 机器人](../bots/what-are-bots.md)  ，可优化组织中事件的管理。</span><span class="sxs-lookup"><span data-stu-id="420f7-319">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="420f7-320">自动程序可促进自动事件数据收集、自定义事件报告、相关利益干系人通知和端到端事件跟踪。</span><span class="sxs-lookup"><span data-stu-id="420f7-320">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="420f7-321">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-321">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

:::row:::
  :::column span="2":::
    ![事件报告器组范围视图](../assets/images/incident-reporter-02.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![事件报告器个人范围视图](../assets/images/incident-reporter-01.jpg)
:::column-end:::
:::row-end:::

## <a name="inspection-9734"></a><span data-ttu-id="420f7-324">检查&#9734;</span><span class="sxs-lookup"><span data-stu-id="420f7-324">Inspection &#9734;</span></span>

 <span data-ttu-id="420f7-325">检查是一款 Microsoft Teams 应用，它使第一线工作人员可以检查从位置到资产和设备之间的任何内容。</span><span class="sxs-lookup"><span data-stu-id="420f7-325">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="420f7-326">例如，零售商店、制造工厂或车辆和计算机。</span><span class="sxs-lookup"><span data-stu-id="420f7-326">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="420f7-327">此解决方案中具有两个应用，每个应用都适用于不同类型的用户。</span><span class="sxs-lookup"><span data-stu-id="420f7-327">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="420f7-328">该应用使一线工作人员能够检查资产或区域，管理产品和服务的质量，或维护工作场所的安全。</span><span class="sxs-lookup"><span data-stu-id="420f7-328">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="420f7-329">它可促进团队成员之间的通信，以解决在检查过程中发现的问题。</span><span class="sxs-lookup"><span data-stu-id="420f7-329">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="420f7-330">该应用为经理提供了简单的报告，以加快问题解决并突出显示趋势。</span><span class="sxs-lookup"><span data-stu-id="420f7-330">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="420f7-331">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-331">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![检查概述](../assets/images/inspection-app.png)  


## <a name="issue-reporting-9734"></a><span data-ttu-id="420f7-333">问题报告&#9734;</span><span class="sxs-lookup"><span data-stu-id="420f7-333">Issue Reporting &#9734;</span></span>

<span data-ttu-id="420f7-334">"问题报告"应用使员工和经理能够提出和管理问题。</span><span class="sxs-lookup"><span data-stu-id="420f7-334">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="420f7-335">它包含两个应用：用于报告问题的"问题报告"应用和用于管理问题的"管理问题"应用。</span><span class="sxs-lookup"><span data-stu-id="420f7-335">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="420f7-336">团队经理使用"管理问题"应用配置应用体验，包括应用创建 Microsoft Teams 消息和 Planner 任务的频道。</span><span class="sxs-lookup"><span data-stu-id="420f7-336">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="420f7-337">经理还使用此应用创建模板表单，以在用户报告问题时收集详细信息。</span><span class="sxs-lookup"><span data-stu-id="420f7-337">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="420f7-338">例如，查看、编辑或删除问题模板表单。</span><span class="sxs-lookup"><span data-stu-id="420f7-338">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="420f7-339">该应用还可用于查看团队问题、报告问题历史记录并高效管理问题解决。</span><span class="sxs-lookup"><span data-stu-id="420f7-339">The app can also be used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="420f7-340">员工使用"问题报告"应用记录解决问题所需的问题和详细信息。</span><span class="sxs-lookup"><span data-stu-id="420f7-340">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="420f7-341">该应用还用于修改和解决现有问题，并获取个人或团队问题的高级别视图。</span><span class="sxs-lookup"><span data-stu-id="420f7-341">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="420f7-342">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-342">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![问题报告团队视图](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="420f7-344">新员工入职培训</span><span class="sxs-lookup"><span data-stu-id="420f7-344">New Employee Onboarding</span></span> 

<span data-ttu-id="420f7-345">新员工入职培训是一款集成的 Microsoft Teams 和 [SharePoint](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) 新员工入职培训解决方案，使你的组织能够在新员工旅程中为员工提供一致、高质量的入职体验。</span><span class="sxs-lookup"><span data-stu-id="420f7-345">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="420f7-346">人力资源团队和招聘经理可以使用该应用在整个入职培训与入职培训过程中提供相关信息，由新员工提供相关信息，以共享反馈、提供简介和完成载入任务。</span><span class="sxs-lookup"><span data-stu-id="420f7-346">The app can be used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="420f7-347">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-347">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="420f7-348">**新员工欢迎卡片** ![新员工欢迎卡片的图像](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="420f7-348">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="420f7-349">**新员工清单** ![新员工清单的图像](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="420f7-349">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="420f7-350">打开锁屏提醒</span><span class="sxs-lookup"><span data-stu-id="420f7-350">Open Badges</span></span>

<span data-ttu-id="420f7-351">开放锁屏提醒是一款 Microsoft Teams 应用，使个人可以在 Teams 上下文中获取数字学习凭据锁屏提醒，并可在任何位置共享。</span><span class="sxs-lookup"><span data-stu-id="420f7-351">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="420f7-352">使用来自第三方数字锁屏提醒颁发机构 [Badgr](https://badgr.org/)的功能，获得奖励的徽章将记录在收件人的 Badgr 个人资料中，可用于生成和共享生命周期学习旅程的丰富图片。</span><span class="sxs-lookup"><span data-stu-id="420f7-352">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="420f7-353">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-353">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

:::row:::
  :::column span="2":::
    ![可用锁屏提醒的图像](../assets/images/open-badges-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![奖励锁屏提醒视图](../assets/images/open-badges-2.png)
:::column-end:::
:::row-end:::

## <a name="poll"></a><span data-ttu-id="420f7-356">轮询</span><span class="sxs-lookup"><span data-stu-id="420f7-356">Poll</span></span> 

<span data-ttu-id="420f7-357">轮询是一个自定义 Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) 消息传递扩展应用，它使您能够在聊天或频道中快速创建和发送投票，以收集团队观点和偏好。</span><span class="sxs-lookup"><span data-stu-id="420f7-357">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="420f7-358">该应用在所有 Teams 平台客户端（桌面、浏览器、iOS 和 Android）中均受支持，并且已准备好作为 Microsoft 365 订阅的一部分进行部署。</span><span class="sxs-lookup"><span data-stu-id="420f7-358">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android  — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="420f7-359">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-359">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![在 Teams 视图中创建轮询](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="420f7-361">快速响应</span><span class="sxs-lookup"><span data-stu-id="420f7-361">Quick Responses</span></span>

<span data-ttu-id="420f7-362">"快速响应"是一款 Microsoft Teams 应用，可提供一个可靠的解决方案，以有效回答用户常见问题解答 (常见问题) 。</span><span class="sxs-lookup"><span data-stu-id="420f7-362">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions (FAQs).</span></span> <span data-ttu-id="420f7-363">应用将构建一个响应库，用于通过 Teams 消息扩展实现交互式用户体验，而不是手动和连续重复地回答 [每个查询](../messaging-extensions/what-are-messaging-extensions.md)。</span><span class="sxs-lookup"><span data-stu-id="420f7-363">Instead of answering each query manually and  continuously repeating information, the app will build a library of responses for an interactive user experience via Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="420f7-364">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-364">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![响应示例视图](../assets/images/quick-responses.png)

## <a name="rapid-assist-9734"></a><span data-ttu-id="420f7-366">快速协助&#9734;</span><span class="sxs-lookup"><span data-stu-id="420f7-366">Rapid Assist &#9734;</span></span>

<span data-ttu-id="420f7-367">快速协助是一款基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) 的应用，它使面向客户的关联人员可以快速与专家联系，以快速获得答案、搜索信息、跟进打开的请求，并允许专家接收通知以快速接听电话以帮助回答问题。</span><span class="sxs-lookup"><span data-stu-id="420f7-367">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="420f7-368">使用 Microsoft [Power Apps](/powerapps/powerapps-overview) 和 [Power Automate](/power-automate/getting-started)构建的应用与 Microsoft Teams 深度集成，使组织能够轻松地将一线工作人员与公司形象联系，从而解决客户查询并提供出色的客户体验。</span><span class="sxs-lookup"><span data-stu-id="420f7-368">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="420f7-369">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-369">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![最终用户请求界面](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![专家请求视图](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="420f7-372">反射</span><span class="sxs-lookup"><span data-stu-id="420f7-372">Reflect</span></span> 

<span data-ttu-id="420f7-373">反射是一个自定义 Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) 消息传递扩展应用，它可为团队成员提供安全且包含的资源，以直接与 Teams 内的同事和/或组领导共享其情绪状态。</span><span class="sxs-lookup"><span data-stu-id="420f7-373">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues and/or group leaders directly within Teams.</span></span> <span data-ttu-id="420f7-374">该应用在频道、组、会议以及一对一聊天中可用，并且签入响应可以设置为公共、私人到发件人或完全匿名。</span><span class="sxs-lookup"><span data-stu-id="420f7-374">The app is available in channel, group, meeting, and 1:1 chats and the check-in response can be set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="420f7-375">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-375">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="420f7-376">**健康轮询**</span><span class="sxs-lookup"><span data-stu-id="420f7-376">**Well-being poll**</span></span>
    
    ![反映应用用户轮询](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="420f7-378">远程支持</span><span class="sxs-lookup"><span data-stu-id="420f7-378">Remote Support</span></span>

<span data-ttu-id="420f7-379">远程支持是一个 [Microsoft Teams](../bots/what-are-bots.md) 机器人，它在整个组织和内部支持团队的支持请求者之间提供一个重点界面。</span><span class="sxs-lookup"><span data-stu-id="420f7-379">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="420f7-380">最终用户可以提交、编辑或撤消支持请求，支持团队可以在 Teams 平台内响应、管理和更新所有请求。</span><span class="sxs-lookup"><span data-stu-id="420f7-380">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="420f7-381">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-381">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

:::row:::
  :::column span="2":::
    ![请求支持表单](../assets/images/remote-support-request-form.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![请求支持详细信息](../assets/images/remote-support-request-details.jpg)
:::column-end:::
:::row-end:::

## <a name="request-a-team"></a><span data-ttu-id="420f7-384">请求团队</span><span class="sxs-lookup"><span data-stu-id="420f7-384">Request-a-team</span></span>

<span data-ttu-id="420f7-385">请求团队是一款 Microsoft Teams 应用，可优化企业组织的新团队创建。</span><span class="sxs-lookup"><span data-stu-id="420f7-385">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="420f7-386">通过集成向导指导的请求表单、嵌入式审批流程、请求状态仪表板和自动团队生成，该应用支持标准化和最佳做法。创建新的团队实例。</span><span class="sxs-lookup"><span data-stu-id="420f7-386">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="420f7-387">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-387">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

:::row:::
  :::column span="2":::
    ![请求团队起始页视图](../assets/images/request-a-team-two.jpg)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![请求团队向导页面视图](../assets/images/request-a-team-three.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-channels"></a><span data-ttu-id="420f7-390">频道的 Scrum</span><span class="sxs-lookup"><span data-stu-id="420f7-390">Scrums for Channels</span></span>

<span data-ttu-id="420f7-391">适用于频道的 Scrum 是一个 scrum 助手应用，使用户能够在 Microsoft Teams 内的频道中安排和运行 scrum。</span><span class="sxs-lookup"><span data-stu-id="420f7-391">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="420f7-392">该应用非常适用于由来自不同地理位置和时区的成员组成的远程团队和团队，以共享每日更新并确保参与重要独立会议。</span><span class="sxs-lookup"><span data-stu-id="420f7-392">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="420f7-393">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-393">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="420f7-394">若要在群聊中召开 scrum 会议，请参阅 [我们的 Scrums for Group Chat](#scrums-for-group-chat) 应用模板。</span><span class="sxs-lookup"><span data-stu-id="420f7-394">To conduct scrum meetings in a group chat, please see our [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

:::row:::
  :::column span="2":::
    ![通道设置视图的 Scrum](../assets/images/scrum-for-channels-settings.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![频道团队成员状态视图的 Scrum](../assets/images/scrum-for-channels-status.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-group-chat"></a><span data-ttu-id="420f7-397">群聊的 Scrum</span><span class="sxs-lookup"><span data-stu-id="420f7-397">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="420f7-398">Scrums 状态应用模板已更新，现在是群聊的 Scrums。</span><span class="sxs-lookup"><span data-stu-id="420f7-398">The Scrums Status app template has been updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="420f7-399">群聊的 Scrum 是一种支持性的 scrum 助手，使群聊成员能够运行异步独立会议并轻松共享其每日更新。</span><span class="sxs-lookup"><span data-stu-id="420f7-399">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="420f7-400">它允许群聊的所有成员参与讨论，并查看运行中的 scrum 中其他人的更新。</span><span class="sxs-lookup"><span data-stu-id="420f7-400">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="420f7-401">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-401">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![群聊演示的 Scrums](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="420f7-403">现在共享</span><span class="sxs-lookup"><span data-stu-id="420f7-403">Share Now</span></span> 

<span data-ttu-id="420f7-404">"现在共享"应用使用户可以轻松地在 Teams 环境中共享内容，从而促进同事之间的积极信息交换。</span><span class="sxs-lookup"><span data-stu-id="420f7-404">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="420f7-405">用户参与应用以与团队成员共享感兴趣的项目、发现新的共享内容、设置首选项和书签收藏夹供以后阅读。</span><span class="sxs-lookup"><span data-stu-id="420f7-405">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="420f7-406">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-406">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![选择内容视图](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="420f7-408">SharePoint 列表搜索</span><span class="sxs-lookup"><span data-stu-id="420f7-408">SharePoint List Search</span></span>

<span data-ttu-id="420f7-409">Microsoft Teams 中的协作通常引用 SharePoint 列表中的项目中包含的信息。</span><span class="sxs-lookup"><span data-stu-id="420f7-409">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="420f7-410">只需将链接粘贴到相关项目，将强制每个人从对话切换上下文，查找所需信息，然后返回到 Teams 以继续对话。</span><span class="sxs-lookup"><span data-stu-id="420f7-410">Simply pasting a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="420f7-411">随着对话的继续，通常用户必须多次切换回引用项，以验证新注释并刷新对项目中包含的信息的了解。</span><span class="sxs-lookup"><span data-stu-id="420f7-411">As the conversation continues typically people will have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="420f7-412">此上下文切换为顺利协作创建了障碍，也是解决失败问题的方式。</span><span class="sxs-lookup"><span data-stu-id="420f7-412">This context switching creates a barrier to smooth collaboration, and is a recipe for things falling through the cracks.</span></span>

<span data-ttu-id="420f7-413">为了帮助缓解这种负担，我们乐意为你带来"列表搜索"应用模板。</span><span class="sxs-lookup"><span data-stu-id="420f7-413">To help alleviate this pain, we are happy to bring to you the List Search app template.</span></span> <span data-ttu-id="420f7-414">数百万用户使用 SharePoint 为组织中某些核心工作流提供支持。</span><span class="sxs-lookup"><span data-stu-id="420f7-414">Millions of users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="420f7-415">但是，围绕列表进行协作可能尤其繁琐。</span><span class="sxs-lookup"><span data-stu-id="420f7-415">However, collaborating around lists can be especially tedious.</span></span> <span data-ttu-id="420f7-416">使用 Microsoft Teams 中的列表搜索应用程序模板，用户可以直接在聊天对话中插入 SharePoint 列表项的信息，以缓解仅向聊天中插入链接时导致上下文切换的情况。</span><span class="sxs-lookup"><span data-stu-id="420f7-416">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="420f7-417">信息作为易于阅读的自动格式化卡片插入，帮助用户保持参与对话。</span><span class="sxs-lookup"><span data-stu-id="420f7-417">The information is inserted as an easy-to-read auto-formatted card, helping your users stay engaged in the conversation.</span></span>

[<span data-ttu-id="420f7-418">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-418">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![列出搜索应用](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="420f7-420">员工签入</span><span class="sxs-lookup"><span data-stu-id="420f7-420">Staff Check-ins</span></span>

<span data-ttu-id="420f7-421">员工签入是基于 [Power Apps](/powerapps/powerapps-overview)的应用，支持业务和现场人员之间的监督通信。</span><span class="sxs-lookup"><span data-stu-id="420f7-421">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview)-based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="420f7-422">员工可直接从 Teams 中定期或临时提供时间关键信息和状态更新。</span><span class="sxs-lookup"><span data-stu-id="420f7-422">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="420f7-423">该应用支持实时位置、照片和笔记以及提醒通知和自动工作流。</span><span class="sxs-lookup"><span data-stu-id="420f7-423">The app supports real-time location, photos, and notes as well as reminder notifications and automated workflows.</span></span>

[<span data-ttu-id="420f7-424">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-424">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![创建签入视图](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="420f7-426">调查</span><span class="sxs-lookup"><span data-stu-id="420f7-426">Survey</span></span>

<span data-ttu-id="420f7-427">调查是一个自定义 Microsoft [Teams](../messaging-extensions/what-are-messaging-extensions.md) 消息传递扩展应用，使你能够在聊天或频道中创建调查，以收集数据并获取可操作见解。</span><span class="sxs-lookup"><span data-stu-id="420f7-427">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span>  <span data-ttu-id="420f7-428">该应用在所有 Teams 平台客户端（桌面、浏览器、iOS 和 Android）中均受支持，并且已准备好作为 Microsoft 365 订阅的一部分进行部署。</span><span class="sxs-lookup"><span data-stu-id="420f7-428">The app is supported across all Teams platform clients — desktop, browser, iOS, and Android — and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="420f7-429">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-429">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![在 Teams 视图中创建调查](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="virtual-rounding-9734"></a><span data-ttu-id="420f7-431">虚拟舍入&#9734;</span><span class="sxs-lookup"><span data-stu-id="420f7-431">Virtual Rounding &#9734;</span></span>

<span data-ttu-id="420f7-432">医院和紧急会议室提供商每天进行数十次，通常数百次"轮"。</span><span class="sxs-lookup"><span data-stu-id="420f7-432">Hospital and emergency room providers make dozens, and often hundreds of “rounds” per day.</span></span> <span data-ttu-id="420f7-433">这些患者快速签入旨在提供患者工作情况的状态检查，并确保解决患者的问题。</span><span class="sxs-lookup"><span data-stu-id="420f7-433">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="420f7-434">尽管舍入是确保由多种类型的提供商监视患者的基本做法，但是它们表示 PPE 上的大量消耗，因为对于每个访问，每个提供商都必须使用一个新的掩码和一组新的面罩。</span><span class="sxs-lookup"><span data-stu-id="420f7-434">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves must be used.</span></span> <span data-ttu-id="420f7-435">借助此应用模板，医疗工作者可以轻松地通过提供商和患者之间的 Microsoft Teams 会议进行虚拟轮次。</span><span class="sxs-lookup"><span data-stu-id="420f7-435">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="420f7-436">Microsoft Health and Life Sciences 博客文章还引用了虚拟舍入 [解决方案](https://aka.ms/teamsvirtualrounding)。</span><span class="sxs-lookup"><span data-stu-id="420f7-436">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="420f7-437">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-437">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![虚拟舍入](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="420f7-439">访问者管理</span><span class="sxs-lookup"><span data-stu-id="420f7-439">Visitor Management</span></span>

<span data-ttu-id="420f7-440">利用访问者管理应用，组织和员工可以直接从 Microsoft Teams 轻松高效地管理现场访问者流程。</span><span class="sxs-lookup"><span data-stu-id="420f7-440">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="420f7-441">该应用程序使员工能够创建访问者请求、通过访问者仪表板集中跟踪请求状态，以及当访问者到达时接收实时通知。</span><span class="sxs-lookup"><span data-stu-id="420f7-441">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="420f7-442">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-442">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

:::row:::
  :::column span="2":::
    ![创建请求视图](../assets/images/visitor-management-create-request.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![访问者到达通知](../assets/images/visitor-management-notify-host.png)
:::column-end:::
:::row-end:::

## <a name="workplace-awards"></a><span data-ttu-id="420f7-445">工作区奖励</span><span class="sxs-lookup"><span data-stu-id="420f7-445">Workplace Awards</span></span>

<span data-ttu-id="420f7-446">工作区奖励是一个 Teams 应用模板，提供一个积极框架，以培养现代工作场所中员工认可和鼓励员工文化。</span><span class="sxs-lookup"><span data-stu-id="420f7-446">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="420f7-447">通过该应用，你可以设置和管理员工奖励和识别 (R&R) 计划，员工可以在该计划中轻松指定和认可同事，R&R 领导可以查看提交的候选人、授予奖励和宣布收件人。</span><span class="sxs-lookup"><span data-stu-id="420f7-447">The app enables you to setup and manage an employee rewards and recognition (R&R) program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="420f7-448">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="420f7-448">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="420f7-449">工作场所奖励候选人卡</span><span class="sxs-lookup"><span data-stu-id="420f7-449">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![工作区奖励列表选项卡](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="420f7-451">对要查看的应用模板有一个想法？</span><span class="sxs-lookup"><span data-stu-id="420f7-451">Have an idea for an app template you'd like to see?</span></span> <span data-ttu-id="420f7-452">[请告诉我们](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)。</span><span class="sxs-lookup"><span data-stu-id="420f7-452">[Please let us know](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>
