---
title: Microsoft Teams应用模板
description: 适用于应用平台的应用模板Microsoft Teams说明
ms.topic: reference
keywords: Microsoft Teams模板示例演示
localization_priority: Normal
ms.author: lajanuar
author: laujan
ms.openlocfilehash: 8cfb066ee3c202fb8611a61bbde3058207a62a35
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566251"
---
# <a name="app-templates-for-microsoft-teams"></a><span data-ttu-id="6d06f-104">Microsoft Teams 的应用模板</span><span class="sxs-lookup"><span data-stu-id="6d06f-104">App templates for Microsoft Teams</span></span>

<span data-ttu-id="6d06f-105">应用程序模板是开放源代码且Microsoft Teams应用程序的完整应用程序示例GitHub。</span><span class="sxs-lookup"><span data-stu-id="6d06f-105">App templates are examples of complete apps for Microsoft Teams that are open-source and available on GitHub.</span></span> <span data-ttu-id="6d06f-106">每个应用模板都包含有关为组织部署和安装该应用的详细说明。</span><span class="sxs-lookup"><span data-stu-id="6d06f-106">Each app template contains detailed instructions for deploying and installing that app for your organization.</span></span> <span data-ttu-id="6d06f-107">它还提供了一个示例应用，你可以立即安装和开始使用该应用。</span><span class="sxs-lookup"><span data-stu-id="6d06f-107">It also provides a sample app that you can install and start using immediately.</span></span> <span data-ttu-id="6d06f-108">完整的源代码也可用，它允许您详细浏览它或分叉代码，并更改它以满足您的特定要求。</span><span class="sxs-lookup"><span data-stu-id="6d06f-108">The complete source code is also available, which allows you to explore it in detail or fork the code and alter it to meet your specific requirements.</span></span>
<span data-ttu-id="6d06f-109">所有应用模板都根据 MIT 许可 [条款](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) 提供。</span><span class="sxs-lookup"><span data-stu-id="6d06f-109">All app templates are provided under the [MIT License](https://github.com/OfficeDev/microsoft-teams-apps-eprescription/blob/master/LICENSE) terms.</span></span>

> [!NOTE] 
> <span data-ttu-id="6d06f-110">你必须许可和支持使用用户和组织的应用模板创建的应用。</span><span class="sxs-lookup"><span data-stu-id="6d06f-110">You must license and support apps created from app templates for your users and organizations.</span></span>

<span data-ttu-id="6d06f-111">**&#9734;指示新发布的应用模板。**</span><span class="sxs-lookup"><span data-stu-id="6d06f-111">**&#9734; Indicates newly released app templates.**</span></span>

### <a name="key-benefits"></a><span data-ttu-id="6d06f-112">主要优势</span><span class="sxs-lookup"><span data-stu-id="6d06f-112">Key benefits</span></span>

* <span data-ttu-id="6d06f-113">**直接部署到云：** 所有应用模板均包括部署脚本，通过这些脚本，可以在 Microsoft Azure Power Platform 中托管所有必需服务。</span><span class="sxs-lookup"><span data-stu-id="6d06f-113">**Deploy directly to the cloud:** All app templates include deployment scripts that allows you to host all required services in Microsoft Azure or the Power Platform.</span></span> 
* <span data-ttu-id="6d06f-114">**建议的示例代码：** 应用模板遵循有关安全性和基础结构的建议最佳做法。</span><span class="sxs-lookup"><span data-stu-id="6d06f-114">**Recommended sample code:** The app templates conform to recommended best practices around security and infrastructure.</span></span> <span data-ttu-id="6d06f-115">审查所有社区提交的对应用模板的更改以确保一致性。</span><span class="sxs-lookup"><span data-stu-id="6d06f-115">All community submitted changes to the app templates are reviewed to ensure conformance.</span></span>
* <span data-ttu-id="6d06f-116">**可自定义和可扩展：** 虽然所有应用模板都使用最少的配置进行部署，但会提供整个代码库和部署脚本，以便你可以轻松自定义或扩展它们以满足你的独特需求。</span><span class="sxs-lookup"><span data-stu-id="6d06f-116">**Customizable and extensible:** While all app templates are deployed with minimal configuration, the entire code base and deployment scripts are provided, so that you can easily customize or extend them to fit your unique needs.</span></span>
* <span data-ttu-id="6d06f-117">**详细文档：** 所有应用模板都附带了有关解决方案体系结构、部署和配置步骤的端到端文档。</span><span class="sxs-lookup"><span data-stu-id="6d06f-117">**Detailed documentation:** All app templates are accompanied by end-to-end documentation on solution architecture, deployment, and configuration steps.</span></span>  

## <a name="adoption-bot"></a><span data-ttu-id="6d06f-118">采用自动程序</span><span class="sxs-lookup"><span data-stu-id="6d06f-118">Adoption Bot</span></span> 

<span data-ttu-id="6d06f-119">采用机器人是使用 Power Virtual Agent 为 PVA 构建的用户Teams聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="6d06f-119">Adoption Bot is a user care chat bot built with Power Virtual Agent for Teams PVA.</span></span> <span data-ttu-id="6d06f-120">它被视为 FAQ Plus 的 PVA 版本。</span><span class="sxs-lookup"><span data-stu-id="6d06f-120">It is considered as the PVA version of FAQ Plus.</span></span> <span data-ttu-id="6d06f-121">采用自动程序解答了 100 多个有关Microsoft 365和Teams。</span><span class="sxs-lookup"><span data-stu-id="6d06f-121">Adoption Bot answers 100+ common questions about Microsoft 365 and Teams.</span></span> <span data-ttu-id="6d06f-122">可以编辑现有主题、添加自己的主题以及加入现有常见问题解答。</span><span class="sxs-lookup"><span data-stu-id="6d06f-122">You can edit the existing topics, add your own topics, and ingest existing FAQs.</span></span> <span data-ttu-id="6d06f-123">如果用户需要其他帮助，采用机器人可以将其与专家联系，甚至可以扩展为使用高级流连接器打开服务票证。</span><span class="sxs-lookup"><span data-stu-id="6d06f-123">If users need additional help, Adoption Bot can connect them to experts or even be extended to open service tickets with premium flow connectors.</span></span> <span data-ttu-id="6d06f-124">此自动程序是自安装或内置于自定义应用，例如采用 [中心](https://github.com/akporzondek/adoption_hub)。</span><span class="sxs-lookup"><span data-stu-id="6d06f-124">This bot is self-installed or built into a custom app, such as the [Adoption Hub](https://github.com/akporzondek/adoption_hub).</span></span>

[<span data-ttu-id="6d06f-125">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-125">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-adopt-bot)

## <a name="adoption-tool--champion-management-platform-9734"></a><span data-ttu-id="6d06f-126">采用工具 - 冠军管理平台&#9734;</span><span class="sxs-lookup"><span data-stu-id="6d06f-126">Adoption Tool- Champion Management Platform &#9734;</span></span>

<span data-ttu-id="6d06f-127">CMP (平台) 模板可帮助你管理、扩展和激发团队合作冠军取得更多成就。</span><span class="sxs-lookup"><span data-stu-id="6d06f-127">The Champion Management Platform (CMP) app template helps you manage, scale, and inspire your teamwork champions to achieve more.</span></span> <span data-ttu-id="6d06f-128">此应用程序模板构建于团队SharePoint 框架并加载到团队中的选项卡中。</span><span class="sxs-lookup"><span data-stu-id="6d06f-128">This app template is built on the SharePoint Framework and loaded into a tab within a team.</span></span> <span data-ttu-id="6d06f-129">组可以利用此工具帮助管理计划成员身份、提供用于日志记录的排行榜和事件类型，以及用于向计划参与者覆盖数字锁屏提醒的工具。</span><span class="sxs-lookup"><span data-stu-id="6d06f-129">Groups can leverage this tool to help manage program membership, provide a leaderboard and event types for logging, and tools to overlay digital badges to program participants.</span></span>

[<span data-ttu-id="6d06f-130">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-130">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-champion-management)

## <a name="adoption-tool--microsoft-365-learning-pathways-get-started-9734"></a><span data-ttu-id="6d06f-131">采用工具- Microsoft 365学习路径 (入门) &#9734;</span><span class="sxs-lookup"><span data-stu-id="6d06f-131">Adoption Tool- Microsoft 365 Learning Pathways (Get Started) &#9734;</span></span>

<span data-ttu-id="6d06f-132">通过入门应用模板，你可以将学习路径Microsoft 365到 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="6d06f-132">The Get Started app template allows you to bring the power of Microsoft 365 learning pathways inside of Microsoft Teams.</span></span> <span data-ttu-id="6d06f-133">此应用程序模板允许你轻松访问特定培训页面或其他 Intranet 资产，并直接在 Teams。</span><span class="sxs-lookup"><span data-stu-id="6d06f-133">This app template allows you to grant easy access to specific training pages or other intranet assets and load the content directly within Teams.</span></span> <span data-ttu-id="6d06f-134">还可以更改应用名称或徽标，以匹配你的公司品牌。</span><span class="sxs-lookup"><span data-stu-id="6d06f-134">You can also change the app name or logo to match your company branding.</span></span>

[<span data-ttu-id="6d06f-135">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-135">Get it on GitHub</span></span>](https://github.com/msft-teams/tools/tree/master/M365%20Learning%20Pathways)

## <a name="appointment-manager"></a><span data-ttu-id="6d06f-136">约会管理器</span><span class="sxs-lookup"><span data-stu-id="6d06f-136">Appointment Manager</span></span> 

<span data-ttu-id="6d06f-137">约会管理器是一Teams模板，可帮助企业通过约会模板创建、管理和与消费者进行Teams。</span><span class="sxs-lookup"><span data-stu-id="6d06f-137">Appointment Manager is a Teams app template to help businesses create, manage, and conduct virtual appointments with consumers through Teams.</span></span> <span data-ttu-id="6d06f-138">来自客户的新约会请求显示在Teams频道中，可快速分配这些请求并将其重新分配到团队中的员工。</span><span class="sxs-lookup"><span data-stu-id="6d06f-138">New appointment requests from consumers are visible in Teams channels, where they are quickly assigned and reassigned to staff in a team.</span></span> <span data-ttu-id="6d06f-139">通过自定义选项卡在团队或个人级别查看约会请求。</span><span class="sxs-lookup"><span data-stu-id="6d06f-139">Appointment requests are viewed at team or personal levels through custom tabs.</span></span> <span data-ttu-id="6d06f-140">每个约会都与一Teams在线会议相关联，因此员工和使用者可以在计划的时间轻松加入会议。</span><span class="sxs-lookup"><span data-stu-id="6d06f-140">Every appointment is associated with a Teams online meeting, hence the staff and consumers can easily join the meeting at the scheduled time.</span></span>

<span data-ttu-id="6d06f-141">该应用模板与 Microsoft Bookings 集成，便于进行约会管理。</span><span class="sxs-lookup"><span data-stu-id="6d06f-141">The app template integrates with Microsoft Bookings for easy appointment management.</span></span> <span data-ttu-id="6d06f-142">安排的约会会自动显示在已分配员工成员的日历上，并且消费者通过嵌入的会议链接接收可自定义的电子邮件通知和提醒。</span><span class="sxs-lookup"><span data-stu-id="6d06f-142">Scheduled appointments automatically appear on assigned staff members' calendars, and consumers receive customizable email notifications and reminders with embedded meeting links.</span></span>

[<span data-ttu-id="6d06f-143">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-143">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-appointment-manager)

<span data-ttu-id="6d06f-144">![约会管理器 ](../assets/images/appointment-manager-overview.png)
 ![ 中的约会管理器概述Teams](../assets/images/appointment-manager-2.png)</span><span class="sxs-lookup"><span data-stu-id="6d06f-144">![Appointment Manager Overview](../assets/images/appointment-manager-overview.png)
![Appointment Manager in Teams](../assets/images/appointment-manager-2.png)</span></span>

## <a name="ask-away"></a><span data-ttu-id="6d06f-145">询问离开</span><span class="sxs-lookup"><span data-stu-id="6d06f-145">Ask Away</span></span>

<span data-ttu-id="6d06f-146">"[离开Microsoft Teams是](../bots/what-are-bots.md)一种自动程序，它使用户能够执行问答，称为&问答Teams。</span><span class="sxs-lookup"><span data-stu-id="6d06f-146">Ask Away is a [Microsoft Teams bot](../bots/what-are-bots.md) that enables users to conduct Question and Answer, called Q&A sessions within Teams.</span></span> <span data-ttu-id="6d06f-147">使用"&询问离开"自动程序，团队成员可以提交和投票支持同事共享的问题，从而允许问答主机轻松地在频道或聊天中收集首要问题。</span><span class="sxs-lookup"><span data-stu-id="6d06f-147">Using the Ask Away bot, team members can submit and up-vote questions shared by colleagues allowing Q&A hosts to easily gather top-of-mind questions within a channel or chat.</span></span> <span data-ttu-id="6d06f-148">机器人用于在会议&实时问答Teams，并允许与会者通过聊天实时提交问题。</span><span class="sxs-lookup"><span data-stu-id="6d06f-148">The bot is used to conduct a real-time Q&A session in a Teams meeting and allows attendees to submit questions live through chat.</span></span>

[<span data-ttu-id="6d06f-149">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-149">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-askaway)

:::row:::
  :::column span="2":::
    ![用户对问题进行投票的排行榜弹出对话框视图](../assets/images/ask-away-app.png)  
:::column-end:::
:::row-end:::

## <a name="associate-insights"></a><span data-ttu-id="6d06f-151">员工见解</span><span class="sxs-lookup"><span data-stu-id="6d06f-151">Associate Insights</span></span>

<span data-ttu-id="6d06f-152">关联见解是一[Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)模板，它使一线员工可以直接捕获和提交客户的意见、情绪和认知。</span><span class="sxs-lookup"><span data-stu-id="6d06f-152">Associate Insights is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that empowers firstline workers to directly capture and submit customer opinion, sentiment, and perception.</span></span> <span data-ttu-id="6d06f-153">一线员工通常是第一个在一对一联系点与客户互动的公司代表。</span><span class="sxs-lookup"><span data-stu-id="6d06f-153">Firstline workers are often the first company representative to engage with customers in a one-to-one point-of contact.</span></span> <span data-ttu-id="6d06f-154">收集的数据由业务团队共享和协同使用，例如通过"Power BI Teams"选项卡，以改进产品并增强客户体验。</span><span class="sxs-lookup"><span data-stu-id="6d06f-154">The collected data are shared and used collaboratively by business teams, such as through a Power BI Teams tab, for product improvement and enhancing the customer experience.</span></span>

[<span data-ttu-id="6d06f-155">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-155">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-associateinsights)

:::row:::
  :::column span="2":::
    ![应用生成的见解的反馈视图](../assets/images/associate-insights-app.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![Power BI生成的见解的视图](../assets/images/associate-insights-app2.png)
:::column-end:::
:::row-end:::

## <a name="attendance"></a><span data-ttu-id="6d06f-158">考勤</span><span class="sxs-lookup"><span data-stu-id="6d06f-158">Attendance</span></span>

<span data-ttu-id="6d06f-159">"考[勤"应用](/powerapps/maker/canvas-apps/embed-teams-app)Power Apps固定在团队中的"参加"选项卡。</span><span class="sxs-lookup"><span data-stu-id="6d06f-159">The Attendance app is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) tab that are pinned in a team.</span></span> <span data-ttu-id="6d06f-160">它旨在记录设置（如学习和培训环境）中的状态。</span><span class="sxs-lookup"><span data-stu-id="6d06f-160">It is designed to record presence in settings, such as learning and training environments.</span></span> <span data-ttu-id="6d06f-161">用户可以标记或编辑过去最多 30 天的出席时间，并查看整个组或单个与会者的汇总出席报告。</span><span class="sxs-lookup"><span data-stu-id="6d06f-161">Users can mark or edit attendance for up to 30 days in the past and view summarized attendance reports for an entire group or individual attendees.</span></span> <span data-ttu-id="6d06f-162">有关团队出席情况详细信息，请参阅在 GitHub[上获取](https://github.com/OfficeDev/microsoft-teams-apps-attendance)。</span><span class="sxs-lookup"><span data-stu-id="6d06f-162">For more information on teams attendance, see [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-attendance).</span></span>

<span data-ttu-id="6d06f-163">下图显示了参加应用演示：</span><span class="sxs-lookup"><span data-stu-id="6d06f-163">The following image displays the attendance app demo:</span></span>  

![参加应用演示](../assets/images/attendance-app.png)

## <a name="book-a-room"></a><span data-ttu-id="6d06f-165">预订聊天室</span><span class="sxs-lookup"><span data-stu-id="6d06f-165">Book-a-room</span></span>

<span data-ttu-id="6d06f-166">会议室预订是一Microsoft Teams自动程序[](../bots/what-are-bots.md)，它允许用户从当前时间开始快速查找和预留会议室 30、60 或 90 分钟。</span><span class="sxs-lookup"><span data-stu-id="6d06f-166">Book-a-room is a [Microsoft Teams bot](../bots/what-are-bots.md) that allows users quickly to find and reserve a meeting room for 30, 60, or 90 minutes starting from the current time.</span></span> <span data-ttu-id="6d06f-167">默认时间为 30 分钟。</span><span class="sxs-lookup"><span data-stu-id="6d06f-167">The default time is 30 minutes.</span></span> <span data-ttu-id="6d06f-168">Book-a-room bot 作用域为个人对话或 1：1 对话。</span><span class="sxs-lookup"><span data-stu-id="6d06f-168">The Book-a-room bot scopes to personal or 1:1 conversations.</span></span> <span data-ttu-id="6d06f-169">有关"预订-会议室"应用详细信息，请参阅在[GitHub 上获取](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom)它。</span><span class="sxs-lookup"><span data-stu-id="6d06f-169">For more information on Book-a-room app, see [Get it on GitHub](https://github.com/OfficeDev/microsoft-teams-apps-bookaroom).</span></span>  
<span data-ttu-id="6d06f-170">下图显示了 Book-a-room 演示：</span><span class="sxs-lookup"><span data-stu-id="6d06f-170">The following image displays the Book-a-room demo:</span></span>

![会议室预订演示](../assets/images/book-a-room.png)

## <a name="building-access"></a><span data-ttu-id="6d06f-172">Building Access</span><span class="sxs-lookup"><span data-stu-id="6d06f-172">Building Access</span></span>

<span data-ttu-id="6d06f-173">Building Access 是一款基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) 的应用，它支持通过允许设施控制器管理、跟踪和报告员工现场状态来管理建筑物阈值和社会实例规范。</span><span class="sxs-lookup"><span data-stu-id="6d06f-173">Building Access is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that supports the administration of building occupancy thresholds and social distancing norms by enabling facilities directors to manage, track, and report employee on-site presence.</span></span> <span data-ttu-id="6d06f-174">使用 Microsoft [Power Apps](/powerapps/powerapps-overview)和[Power Automate](/power-automate/getting-started)构建的应用与 Microsoft Teams 深度集成，使组织可以确定构建就绪情况、建立现场访问的资格标准，并收集用于将来规划的见解。</span><span class="sxs-lookup"><span data-stu-id="6d06f-174">The app, built using Microsoft [Power Apps](/powerapps/powerapps-overview), and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams and enables organizations to determine building readiness, establish eligibility criteria for on-site access, and gather insights for future planning.</span></span>

[<span data-ttu-id="6d06f-175">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-175">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-buildingaccess)

:::row:::
   :::column span="":::
     ![Building Access 预订卡](../assets/images/building-access-reservation.png)
   :::column-end:::
   :::column span="":::
      ![生成访问键视图](../assets/images/building-access-access-key.png)
   :::column-end:::
:::row-end:::

## <a name="celebrations"></a><span data-ttu-id="6d06f-178">Celebrations</span><span class="sxs-lookup"><span data-stu-id="6d06f-178">Celebrations</span></span>

<span data-ttu-id="6d06f-179">庆祝是一Teams，可帮助团队成员庆祝彼此的生日、纪念日和其他定期事件。</span><span class="sxs-lookup"><span data-stu-id="6d06f-179">Celebrations is a Teams app that helps team members to celebrate each others' birthdays, anniversaries, and other recurring events.</span></span> <span data-ttu-id="6d06f-180">它记住所有团队成员的特殊场合，并发送在事件创建时选定的所有团队中的友好消息，使团队成员在一天中感觉特别。</span><span class="sxs-lookup"><span data-stu-id="6d06f-180">It remembers special occasions of all the team members and sends a friendly message in all the teams selected at the time of event creation, to make the team members feel special on their day.</span></span>

<span data-ttu-id="6d06f-181">该应用提供了一个简单的界面，供所有团队成员个人添加和查看其事件，还允许用户选择共享事件的团队。</span><span class="sxs-lookup"><span data-stu-id="6d06f-181">The app provides an easy interface for all the team members to personally add and view their events and also allows the user to select the teams in which the events gets shared.</span></span>

[<span data-ttu-id="6d06f-182">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-182">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-celebrations-app)

## <a name="checklist"></a><span data-ttu-id="6d06f-183">检查表</span><span class="sxs-lookup"><span data-stu-id="6d06f-183">Checklist</span></span>

<span data-ttu-id="6d06f-184">清单是一Microsoft Teams扩展应用的自定义清单[](../messaging-extensions/what-are-messaging-extensions.md)，它使您能够通过创建聊天或频道中的共享清单与团队协作。</span><span class="sxs-lookup"><span data-stu-id="6d06f-184">Checklist is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to collaborate with your team by creating a shared checklist in a chat or channel.</span></span> <span data-ttu-id="6d06f-185">该应用在所有 Teams客户端（如桌面浏览器、iOS 和 Android）中均受支持。</span><span class="sxs-lookup"><span data-stu-id="6d06f-185">The app is supported across all Teams platform clients, such as desktop browser, iOS, and Android.</span></span> <span data-ttu-id="6d06f-186">应用已准备就绪，可以部署为订阅Microsoft 365一部分。</span><span class="sxs-lookup"><span data-stu-id="6d06f-186">The app is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="6d06f-187">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-187">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-checklist-app)

:::row:::
:::column span="2":::
    ![在视图视图中Teams清单](../assets/images/checklist-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="classroom-drop-in"></a><span data-ttu-id="6d06f-189">课堂放置</span><span class="sxs-lookup"><span data-stu-id="6d06f-189">Classroom Drop-in</span></span> 

<span data-ttu-id="6d06f-190">Classroom Drop-in 是一款基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)的应用，它使系统领导能够根据需要查找课堂团队、虚拟教室以及将自己或其他人员添加到这些课堂团队中。</span><span class="sxs-lookup"><span data-stu-id="6d06f-190">Classroom Drop-in is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/)-based app that enables system leaders to find class teams, means virtual classrooms and add themselves or others to these class teams for a specified drop-in period, as needed.</span></span> <span data-ttu-id="6d06f-191">使用 Microsoft [Power Apps](/powerapps/powerapps-overview)和[Power Automate](/power-automate/getting-started)构建的应用与 Microsoft Teams 深度集成，以确保教育机构可以针对每个业务要求向相关利益干系人提供访问权限，从而优化他们在混合学习环境中的操作。</span><span class="sxs-lookup"><span data-stu-id="6d06f-191">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to ensure educational institutes can optimize their operations in a hybrid learning environment by providing access to relevant stakeholders for class teams per business requirements.</span></span>

[<span data-ttu-id="6d06f-192">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-192">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-classroom-dropin)

![课堂下拉请求](../assets/images/classroom-drop-in-request.png)

## <a name="company-communicator"></a><span data-ttu-id="6d06f-194">Company Communicator</span><span class="sxs-lookup"><span data-stu-id="6d06f-194">Company Communicator</span></span>

<span data-ttu-id="6d06f-195">公司Communicator应用使企业团队可以创建和发送供多个团队或大量员工使用的消息，通过聊天允许组织在员工协作的地方与员工联系。</span><span class="sxs-lookup"><span data-stu-id="6d06f-195">The Company Communicator app enables corporate teams to create and send messages intended for multiple teams or large number of employees over chat allowing organization to reach employees right where they collaborate.</span></span> <span data-ttu-id="6d06f-196">此模板可用于多个方案，例如新计划公告、员工入职培训、新式学习、开发或组织范围的广播。</span><span class="sxs-lookup"><span data-stu-id="6d06f-196">Utilize this template for multiple scenarios such as new initiative announcements, employee onboarding, modern learning, and development or organization-wide broadcasts.</span></span>

<span data-ttu-id="6d06f-197">该应用为指定用户提供了一个简单的界面，用于创建、预览、协作和发送邮件。</span><span class="sxs-lookup"><span data-stu-id="6d06f-197">The app provides an easy interface for designated users to create, preview, collaborate and send messages.</span></span>

<span data-ttu-id="6d06f-198">它为构建自定义目标通信功能（如有关确认或与邮件交互的用户数的自定义遥测）提供了基础。</span><span class="sxs-lookup"><span data-stu-id="6d06f-198">It provides a foundation to build custom targeted communication capabilities such as custom telemetry on how many users acknowledged or interacted with a message.</span></span>

[<span data-ttu-id="6d06f-199">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-199">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-company-communicator-app)

![jCompany Communicator撰写框视图](../assets/images/CompanyCommunicatorCompose.png)

## <a name="contact-group-lookup"></a><span data-ttu-id="6d06f-201">联系人组查找</span><span class="sxs-lookup"><span data-stu-id="6d06f-201">Contact Group Lookup</span></span>

<span data-ttu-id="6d06f-202">联系人组查找应用程序提供了一种方便且有用的方法，用于创建、访问和管理您组织的联系人组（以前称为通讯组列表或通信组）。</span><span class="sxs-lookup"><span data-stu-id="6d06f-202">The Contact Group Lookup app provides a convenient and useful approach to creating, accessing, and managing your organization's contact groups, formerly known as distribution lists or communication groups.</span></span> <span data-ttu-id="6d06f-203">用户可以快速查看和与团队成员聊天、查看成员状态，以及创建与联系人组中选定成员的群聊，所有这些都在 Teams 环境中。</span><span class="sxs-lookup"><span data-stu-id="6d06f-203">Users can quickly view and chat with group members, view member status, and create a group chat with selected members in the contact group, all within the Teams environment.</span></span>

[<span data-ttu-id="6d06f-204">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-204">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-contactgrouplookup)

:::row:::
:::column span="2":::
    ![联系人组查找固定的收藏夹视图](../assets/images/contact-group-lookup-favorites.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![联系人组查找开始聊天演示](../assets/images/contact-group-lookup-chat.png)
:::column-end:::
:::row-end:::

## <a name="co-worker-appreciation"></a><span data-ttu-id="6d06f-207">同事的感谢</span><span class="sxs-lookup"><span data-stu-id="6d06f-207">Co-worker Appreciation</span></span> 

<span data-ttu-id="6d06f-208">通过使用工作环境中的同事Microsoft Teams模板，用户可以在工作环境中识别Teams的成就。</span><span class="sxs-lookup"><span data-stu-id="6d06f-208">Using the co-worker appreciation template in Microsoft Teams, users can recognize their colleagues' achievements within the Teams’ context.</span></span> <span data-ttu-id="6d06f-209">当同事选择奖励同事时，将在频道对话中标记收件人和其他团队成员，并接收有关该频道的奖励详细信息的通知。</span><span class="sxs-lookup"><span data-stu-id="6d06f-209">When co-workers select to reward a colleague, recipients and other team members are tagged in a channel conversation and they receive a notification about the channel's award details.</span></span> <span data-ttu-id="6d06f-210">这些奖励记录在Teams应用中，安全、便携且易于共享。</span><span class="sxs-lookup"><span data-stu-id="6d06f-210">The awards are recorded in the Teams app, which is secure, portable, and easily shareable.</span></span> <span data-ttu-id="6d06f-211">这被视为基于 PowerApps 的开放锁屏提醒应用模板版本，具有排行榜。</span><span class="sxs-lookup"><span data-stu-id="6d06f-211">This is considered as the PowerApps based version of the Open Badges app template, with a leaderboard.</span></span>

[<span data-ttu-id="6d06f-212">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-212">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-coworker-appreciation)

![总体](../assets/images/coworker-appreciation-1.png)

## <a name="crowdsourcer"></a><span data-ttu-id="6d06f-214">CrowdSourcer</span><span class="sxs-lookup"><span data-stu-id="6d06f-214">CrowdSourcer</span></span>

<span data-ttu-id="6d06f-215">众源是一[Microsoft Teams](../bots/what-are-bots.md)自动程序，它提供团队查询信息，这些信息以协作方式从组成员获取。</span><span class="sxs-lookup"><span data-stu-id="6d06f-215">CrowdSourcer is a [Microsoft Teams bot](../bots/what-are-bots.md) that gives teams queried information sourced collaboratively from group members.</span></span> <span data-ttu-id="6d06f-216">它有助于回答常见问题，同时使参与者能够积极参与并参与一个有趣而有用的信息资源。</span><span class="sxs-lookup"><span data-stu-id="6d06f-216">It helps to answer frequently asked questions while enabling participants to actively engage in and contribute to a fun and helpful information resource.</span></span>

[<span data-ttu-id="6d06f-217">在 Github 上获取</span><span class="sxs-lookup"><span data-stu-id="6d06f-217">Get it on Github</span></span>](https://github.com/OfficeDev/microsoft-teams-crowdsourcer-app)

![众包最终用户交互](../assets/images/crowdsourcer.png)

## <a name="custom-stickers"></a><span data-ttu-id="6d06f-219">自定义贴纸</span><span class="sxs-lookup"><span data-stu-id="6d06f-219">Custom Stickers</span></span>

<span data-ttu-id="6d06f-220">自我表达是健康团队文化的核心。</span><span class="sxs-lookup"><span data-stu-id="6d06f-220">Self-expression is core to a healthy team culture.</span></span> <span data-ttu-id="6d06f-221">此应用模板是[一个消息](~/messaging-extensions/what-are-messaging-extensions.md)扩展，使你的用户能够在应用中使用自定义贴纸Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="6d06f-221">This app template is a [messaging extension](~/messaging-extensions/what-are-messaging-extensions.md) that enables your users to use custom stickers and GIFs within Microsoft Teams.</span></span> <span data-ttu-id="6d06f-222">此模板提供了一种基于 Web 的轻松配置体验，具有配置访问权限的任何人都可以上传希望用户拥有的 GIF、贴纸和图像，从而允许整个团队使用你选择的任何一组贴纸。</span><span class="sxs-lookup"><span data-stu-id="6d06f-222">This template provides an easy web-based configuration experience where anyone with configuration access can upload the GIFs, stickers, and images they want their users to have, allowing your entire team to use any set of stickers you choose.</span></span>

<span data-ttu-id="6d06f-223">此应用还支持跨团队轻松共享图像、GIF、贴纸，而无需访问 SharePoint 网站或单个通道作为存储和共享机制。</span><span class="sxs-lookup"><span data-stu-id="6d06f-223">This app also enables easy sharing of images, GIFs, stickers across teams without needing access to SharePoint sites or individual channels as storage and sharing mechanisms.</span></span> <span data-ttu-id="6d06f-224">例如，产品团队可以通过编程方式轻松地将产品图像和 GIF 共享到社交媒体、市场营销和销售团队。</span><span class="sxs-lookup"><span data-stu-id="6d06f-224">For example, product teams can easily share product images and GIFs to social media, marketing, and sales teams programmatically.</span></span> <span data-ttu-id="6d06f-225">还可以在提供新映像和 GIF 时，通过向特定团队或个人触发通知流来扩展此应用。</span><span class="sxs-lookup"><span data-stu-id="6d06f-225">One can also extend this app by triggering a notification flow to specific teams or individuals when new images, and GIFs are made available.</span></span>

[<span data-ttu-id="6d06f-226">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-226">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-stickers-app)

![贴纸应用](../assets/images/stickers.png)

## <a name="employee-ideas"></a><span data-ttu-id="6d06f-228">员工想法</span><span class="sxs-lookup"><span data-stu-id="6d06f-228">Employee Ideas</span></span>

<span data-ttu-id="6d06f-229">员工创意应用是基于 Azure 的"创意型创意"应用模板的 PowerApps 版本。</span><span class="sxs-lookup"><span data-stu-id="6d06f-229">The Employee Ideas app is the PowerApps version of the Azure based Great Ideas app template.</span></span> <span data-ttu-id="6d06f-230">该应用使Teams用户能够设置和配置创意活动。</span><span class="sxs-lookup"><span data-stu-id="6d06f-230">The app enables the Teams users to set up and configure an idea campaign.</span></span> <span data-ttu-id="6d06f-231">想法活动是围绕常见主题对想法进行分组的类别。</span><span class="sxs-lookup"><span data-stu-id="6d06f-231">An idea campaign is a category for grouping ideas around common themes.</span></span>

<span data-ttu-id="6d06f-232">Teams用户还可以执行以下活动：</span><span class="sxs-lookup"><span data-stu-id="6d06f-232">Teams users can also perform the following activities:</span></span>

* <span data-ttu-id="6d06f-233">配置员工必须为每个想法提交的标准提交表单。</span><span class="sxs-lookup"><span data-stu-id="6d06f-233">Configure a standard submission form that employees must submit for each idea.</span></span> 
* <span data-ttu-id="6d06f-234">查看和管理活动的想法和列表。</span><span class="sxs-lookup"><span data-stu-id="6d06f-234">Review and manage the ideas and list of campaigns.</span></span>
* <span data-ttu-id="6d06f-235">修改和删除市场活动。</span><span class="sxs-lookup"><span data-stu-id="6d06f-235">Modify and delete campaigns.</span></span>
* <span data-ttu-id="6d06f-236">查看想法的排行榜。</span><span class="sxs-lookup"><span data-stu-id="6d06f-236">Review leader boards of ideas.</span></span>
* <span data-ttu-id="6d06f-237">投票支持并共享优先想法。</span><span class="sxs-lookup"><span data-stu-id="6d06f-237">Vote for and share prioritized ideas.</span></span>
* <span data-ttu-id="6d06f-238">提交活动想法。</span><span class="sxs-lookup"><span data-stu-id="6d06f-238">Submit ideas for a campaign.</span></span>
* <span data-ttu-id="6d06f-239">查看其他团队成员的想法。</span><span class="sxs-lookup"><span data-stu-id="6d06f-239">View other team member's idea.</span></span>
* <span data-ttu-id="6d06f-240">对最喜欢的想法投票。</span><span class="sxs-lookup"><span data-stu-id="6d06f-240">Vote on most liked ideas.</span></span>
* <span data-ttu-id="6d06f-241">查看他们与市场活动中其他人相比想法的性能。</span><span class="sxs-lookup"><span data-stu-id="6d06f-241">Review the performance of their ideas compared with others within a campaign.</span></span>

[<span data-ttu-id="6d06f-242">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-242">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeeideas)

![管理市场活动视图](../assets/images/employee-ideas-manage-campaigns.png) 

## <a name="e-prescriptions"></a><span data-ttu-id="6d06f-244">E-Prescriptions</span><span class="sxs-lookup"><span data-stu-id="6d06f-244">E-Prescriptions</span></span> 

<span data-ttu-id="6d06f-245">E-Patients 是[Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)一款基于应用的应用，它通过自动执行向患者发布电子医疗方案的过程来增强远程医疗与虚拟医疗。</span><span class="sxs-lookup"><span data-stu-id="6d06f-245">E-Prescriptions is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) based app that enhances telemedicine and virtual care by automating the process of issuing e-prescriptions to patients.</span></span> <span data-ttu-id="6d06f-246">医疗专业人员可以直接在安全中心平台中查看约会、生成电子Teams附件的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="6d06f-246">Medical professionals can quickly review appointments, generate e-prescriptions, and send emails with e-prescription attachments to patients directly within the Teams platform.</span></span>

[<span data-ttu-id="6d06f-247">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-247">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-eprescription) 

:::row:::
:::column span="2":::
    ![E-Prescriptions 应用的屏幕截图。](../assets/images/e-prescriptions-app-template.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![E-Prescriptions 应用的屏幕截图。](../assets/images/e-prescriptions-app-template-admin.png)
:::column-end:::
:::row-end:::

## <a name="employee-training"></a><span data-ttu-id="6d06f-252">员工培训</span><span class="sxs-lookup"><span data-stu-id="6d06f-252">Employee Training</span></span> 

<span data-ttu-id="6d06f-253">员工培训是一Microsoft Teams，使组织者可以轻松发布、跟踪和提升组织的学习与培训计划。</span><span class="sxs-lookup"><span data-stu-id="6d06f-253">Employee training is a Microsoft Teams app that enables organizers to easily publish, track, and promote learning and training events for your organization.</span></span>  <span data-ttu-id="6d06f-254">借助该应用，事件规划人员可以将提醒和通知发送给事件注册人，员工可以指示对即将发生事件的关注，及时了解当前事件，并通过 Teams 消息扩展与同事共享事件详细信息。</span><span class="sxs-lookup"><span data-stu-id="6d06f-254">With the app, event planners can send reminders and notifications to event registrants and employees can indicate interest in upcoming events, stay updated on current events, and share event details with colleagues through the Teams messaging extension.</span></span>

[<span data-ttu-id="6d06f-255">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-255">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-employeetraining)

:::row:::
:::column span="2":::
    <span data-ttu-id="6d06f-256">**查看员工培训计划** ![员工培训选项卡图像](../assets/images/employee-training-discover-tab.png)</span><span class="sxs-lookup"><span data-stu-id="6d06f-256">**View employee training events** ![Employee training tab image](../assets/images/employee-training-discover-tab.png)</span></span>  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="6d06f-257">**创建员工培训计划** ![员工培训创建事件表单](../assets/images/employee-training-create-event.jpg)</span><span class="sxs-lookup"><span data-stu-id="6d06f-257">**Create employee training event** ![Employee training create event form](../assets/images/employee-training-create-event.jpg)</span></span>
:::column-end:::
:::row-end:::

## <a name="expert-finder"></a><span data-ttu-id="6d06f-258">专家查找器</span><span class="sxs-lookup"><span data-stu-id="6d06f-258">Expert Finder</span></span>

<span data-ttu-id="6d06f-259">专家查找器是[一Microsoft Teams](../bots/what-are-bots.md)自动程序，可基于特定组织成员的技能、兴趣和教育属性标识这些成员。</span><span class="sxs-lookup"><span data-stu-id="6d06f-259">Expert Finder is a [Microsoft Teams bot](../bots/what-are-bots.md) that identifies specific organization members based on their skills, interests, and education attributes.</span></span> <span data-ttu-id="6d06f-260">成员在组织中查找与用户配置文件的关键字搜索Azure Active Directory专家。</span><span class="sxs-lookup"><span data-stu-id="6d06f-260">Members find experts within an organization that match a keyword search of Azure Active Directory user profiles.</span></span>

[<span data-ttu-id="6d06f-261">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-261">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-expertfinder)

![专家查找器搜索结果演示](../assets/images/expert-finder.png)

## <a name="faq-plus"></a><span data-ttu-id="6d06f-263">常见问题 +</span><span class="sxs-lookup"><span data-stu-id="6d06f-263">FAQ Plus</span></span>

<span data-ttu-id="6d06f-264">对话&聊天机器人是为用户提供常见问题解答的一种简单方法。</span><span class="sxs-lookup"><span data-stu-id="6d06f-264">Conversational Q&A bots are an easy way to provide answers to frequently asked questions by users.</span></span> <span data-ttu-id="6d06f-265">但是，大多数机器人无法以有意义的方式与用户互动，因为当机器人出现故障时，循环中没有任何人。</span><span class="sxs-lookup"><span data-stu-id="6d06f-265">But, most bots fail to engage with users in meaningful way because there is no human in the loop when the bot fails.</span></span> <span data-ttu-id="6d06f-266">常见问题自动程序是一&的问答，当机器人无法提供帮助时，它会在循环中引入用户。</span><span class="sxs-lookup"><span data-stu-id="6d06f-266">FAQ bot is a friendly Q&A bot that brings a human in the loop when it is unable to help.</span></span> <span data-ttu-id="6d06f-267">用户可以向机器人提问，如果问题包含在知识库中，机器人会以答案进行响应。</span><span class="sxs-lookup"><span data-stu-id="6d06f-267">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="6d06f-268">如果没有，机器人允许用户提交查询，该查询随后会发布给预配置的专家团队，这些专家通过处理来自团队本身的通知来帮助提供支持。</span><span class="sxs-lookup"><span data-stu-id="6d06f-268">If not, the bot allows the user to submit a query which then gets posted to a pre-configured team of experts who help to provide support by acting upon the notifications from within the team itself.</span></span>

> [!NOTE]
> <span data-ttu-id="6d06f-269">最新版 **FAQ Plus** 支持改进&问答解决方案，使专家团队能够完成以下任务：</span><span class="sxs-lookup"><span data-stu-id="6d06f-269">The latest release of **FAQ Plus** supports improved Q&A resolutions by enabling a team of experts to complete the following:</span></span>
>
> <span data-ttu-id="6d06f-270">&#x2714;使用消息&将新的问答直接添加到知识库。</span><span class="sxs-lookup"><span data-stu-id="6d06f-270">&#x2714; Add new Q&As directly to the knowledge base using message extensions.</span></span>
>
> <span data-ttu-id="6d06f-271">&#x2714;编辑和删除&自动程序添加的问答。</span><span class="sxs-lookup"><span data-stu-id="6d06f-271">&#x2714; Edit and delete Q&A pairs added by a bot.</span></span>
>
> <span data-ttu-id="6d06f-272">&#x2714;跟踪问答的&历史记录。</span><span class="sxs-lookup"><span data-stu-id="6d06f-272">&#x2714; Track the revision history of Q&As.</span></span>
>
> <span data-ttu-id="6d06f-273">&#x2714;配置包含其他详细信息的答案，以显示为自适应 [卡片](../task-modules-and-cards/cards/cards-reference.md#adaptive-card)。</span><span class="sxs-lookup"><span data-stu-id="6d06f-273">&#x2714; Configure an answer with additional details to display as an [Adaptive Card](../task-modules-and-cards/cards/cards-reference.md#adaptive-card).</span></span>
>
[<span data-ttu-id="6d06f-274">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-274">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-faqplusv2)

![FAQ Plus gif](../assets/images/FAQPlusEndUser.gif)

## <a name="get-support-app"></a><span data-ttu-id="6d06f-276">获取支持应用</span><span class="sxs-lookup"><span data-stu-id="6d06f-276">Get Support App</span></span>

<span data-ttu-id="6d06f-277">"获取支持"应用由使用 Microsoft Teams 的组织使用，以允许任何一组用户向主管请求帮助。</span><span class="sxs-lookup"><span data-stu-id="6d06f-277">The Get Support app is used by organizations that are using Microsoft Teams, to enable any set of users to request assistance from supervisors.</span></span> <span data-ttu-id="6d06f-278">此应用程序包括以下功能：</span><span class="sxs-lookup"><span data-stu-id="6d06f-278">This app includes the following features:</span></span>
* <span data-ttu-id="6d06f-279">从 Power App 请求不同类别的帮助。</span><span class="sxs-lookup"><span data-stu-id="6d06f-279">Requesting assistance on different categories from a Power App.</span></span>
* <span data-ttu-id="6d06f-280">发送给请求者的通知，告知他们分配了谁。</span><span class="sxs-lookup"><span data-stu-id="6d06f-280">Notifications sent to requestors informing them of who hare assigned.</span></span>
* <span data-ttu-id="6d06f-281">发送给指定监督员的通知，告知他们谁需要协助。</span><span class="sxs-lookup"><span data-stu-id="6d06f-281">Notifications sent to assigned supervisors informing them of who needs assistance.</span></span> 
* <span data-ttu-id="6d06f-282">分析 SharePoint 和 PowerBI.S 中的升级和模式。</span><span class="sxs-lookup"><span data-stu-id="6d06f-282">Analyzing escalations and patterns in SharePoint and PowerBI.S.</span></span>

[<span data-ttu-id="6d06f-283">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-283">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-get-support/)

![获取支持 Gif](../assets/images/get-support.gif)

## <a name="goal-tracker"></a><span data-ttu-id="6d06f-285">目标跟踪器</span><span class="sxs-lookup"><span data-stu-id="6d06f-285">Goal Tracker</span></span>

<span data-ttu-id="6d06f-286">目标跟踪器应用是一个全面的解决方案，可支持组织建立目标、观察进度和确认Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="6d06f-286">The Goal Tracker app is a comprehensive solution for your organization to support establishing goals, observing progress, and acknowledging success within Microsoft Teams.</span></span> <span data-ttu-id="6d06f-287">该应用使用户能够在专业、个人和团队级别设置、跟踪和更新目标。</span><span class="sxs-lookup"><span data-stu-id="6d06f-287">The app enables users to set, track, and update objectives on a professional, personal, and team level.</span></span> <span data-ttu-id="6d06f-288">团队成员还收到及时的提醒和状态更新，保持专注并保持跟踪状态。</span><span class="sxs-lookup"><span data-stu-id="6d06f-288">Team members also receive timely reminders and status updates to remain focused and stay on track.</span></span>

[<span data-ttu-id="6d06f-289">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-289">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-goaltracker)

:::row:::
  :::column span="2":::
    ![设置目标](../assets/images/goal-tracker-set-goals-view.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![查看设置目标](../assets/images/goal-tracker-your-goals-view.png)
:::column-end:::
:::row-end:::

## <a name="great-ideas"></a><span data-ttu-id="6d06f-292">出色的创意</span><span class="sxs-lookup"><span data-stu-id="6d06f-292">Great Ideas</span></span>

<span data-ttu-id="6d06f-293">出色的创意应用支持并增强组织内部的创造力和创造力。</span><span class="sxs-lookup"><span data-stu-id="6d06f-293">The Great Ideas app supports and empowers innovation and creativity within your organization.</span></span> <span data-ttu-id="6d06f-294">利用该应用，你的员工可以与同事和领导分享想法、发现新提交、聚焦贡献以用于对等考虑，并投票选择 Microsoft Teams 中的最佳建议。</span><span class="sxs-lookup"><span data-stu-id="6d06f-294">The app enables your employees to share ideas with colleagues and leadership, discover new submissions, spotlight contributions for peer consideration, and cast their vote for the best proposals within Microsoft Teams.</span></span>

[<span data-ttu-id="6d06f-295">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-295">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-greatideas)

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

## <a name="group-activities"></a><span data-ttu-id="6d06f-298">组活动</span><span class="sxs-lookup"><span data-stu-id="6d06f-298">Group Activities</span></span>

<span data-ttu-id="6d06f-299">组活动是一Microsoft Teams应用程序，使团队所有者可以轻松快速创建活动组，并在其上下文中管理Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="6d06f-299">Group Activities is a Microsoft Teams app that makes it easy for team owners to quickly create activity groups and manage collaboration workflows within the context of Microsoft Teams.</span></span> <span data-ttu-id="6d06f-300">活动作者可以创建活动、在组中随机分配团队成员，并可以选择让机器人发送提醒，直到活动完成。</span><span class="sxs-lookup"><span data-stu-id="6d06f-300">Activity authors are enabled to create activities, randomly distribute team members in groups, and optionally have the bot send reminders until activities are complete.</span></span>

[<span data-ttu-id="6d06f-301">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-301">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupactivities)

:::row:::
  :::column span="2":::
    ![列表中的组活动Teams](../assets/images/group-activities-1.png)  
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![频道中的组活动通知消息](../assets/images/group-activities-2.png)
:::column-end:::
:::row-end:::

## <a name="group-connect-9734"></a><span data-ttu-id="6d06f-304">组连接 &#9734;</span><span class="sxs-lookup"><span data-stu-id="6d06f-304">Group Connect &#9734;</span></span>

<span data-ttu-id="6d06f-305">组连接是一Microsoft Teams应用程序，可帮助组织成员发现员工组并查找与员工组有关的信息。</span><span class="sxs-lookup"><span data-stu-id="6d06f-305">Group Connect is a Microsoft Teams app that helps organization members discover employee groups and find information relevant to employee groups.</span></span> <span data-ttu-id="6d06f-306">该应用内置有丰富的功能，组织领导可以与员工就组、事件和资源进行沟通。</span><span class="sxs-lookup"><span data-stu-id="6d06f-306">The app comes built-in with rich capabilities for organization leaders to communicate with their employees regarding groups, events, and resources.</span></span> <span data-ttu-id="6d06f-307">组连接应用还按所需频率相互匹配，以鼓励在组内建立网络和建立关系。</span><span class="sxs-lookup"><span data-stu-id="6d06f-307">The Group Connect app also matches group members with each other at their desired frequency to encourage networking and cohesion within a group.</span></span> <span data-ttu-id="6d06f-308">若要详细了解如何利用组和 连接 应用来帮助员工组在组织内部培养，请参阅 GitHub。</span><span class="sxs-lookup"><span data-stu-id="6d06f-308">For more information on how you can leverage the Group Connect app to help employee groups foster within your organization, see the app on GitHub.</span></span>

[<span data-ttu-id="6d06f-309">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-309">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-groupconnect)

![发现 D&I 组](https://github.com/OfficeDev/microsoft-teams-apps-diversityandinclusion/wiki/Images/temp_group_connect_landing.png)

## <a name="grow-your-skills"></a><span data-ttu-id="6d06f-311">提高技能</span><span class="sxs-lookup"><span data-stu-id="6d06f-311">Grow Your Skills</span></span>

<span data-ttu-id="6d06f-312">"发展你的技能"应用通过允许员工在同时学习新技能的同时为组织提供补充项目，从而支持专业增长和开发。</span><span class="sxs-lookup"><span data-stu-id="6d06f-312">The Grow Your Skills app supports professional growth and development by enabling employees to contribute to supplemental projects for your organization while simultaneously learning new skills.</span></span> <span data-ttu-id="6d06f-313">员工可以使用该应用找到满足其兴趣的机会，与同行进行有意义的协作，并获得新的专业技能Teams级别。</span><span class="sxs-lookup"><span data-stu-id="6d06f-313">Employees can use the app to locate opportunities that meet their interests, enjoy meaningful collaboration with peers, and acquire new levels of expertise and capabilities, all within the Teams environment.</span></span>

[<span data-ttu-id="6d06f-314">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-314">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-growyourskills)

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

## <a name="hr-support"></a><span data-ttu-id="6d06f-317">HR 支持</span><span class="sxs-lookup"><span data-stu-id="6d06f-317">HR Support</span></span>

<span data-ttu-id="6d06f-318">HR 支持机器人是一个友好的&聊天机器人，当无法提供帮助时，它会在循环中引入 HR 团队的支持专业人员或专家。</span><span class="sxs-lookup"><span data-stu-id="6d06f-318">HR Support bot is a friendly Q&A bot that brings a support professional or expert from the HR team in the loop when it is unable to help.</span></span> <span data-ttu-id="6d06f-319">用户可以向机器人提问，如果问题包含在知识库中，机器人会以答案进行响应。</span><span class="sxs-lookup"><span data-stu-id="6d06f-319">One can ask the bot a question and the bot responds with an answer if it is contained in the knowledge base.</span></span> <span data-ttu-id="6d06f-320">如果没有，机器人允许用户提交查询，该查询随后将在预配置的专家团队中发布，这些专家通过处理来自团队本身的通知提供帮助。</span><span class="sxs-lookup"><span data-stu-id="6d06f-320">If not, the bot allows the user to submit a query which then gets posted in a pre-configured team of experts who are help to provide support by acting upon the notifications from within their team itself.</span></span> <span data-ttu-id="6d06f-321">此外，机器人通过搜索问题中的预配置标记，提供指向建议的 HR 策略或问题的链接。</span><span class="sxs-lookup"><span data-stu-id="6d06f-321">Additionally, the bot suggests links to recommended HR policies or questions by searching for pre-configured tags in the question.</span></span> <span data-ttu-id="6d06f-322">这些磁贴在关联的选项卡中作为快速参考找到。</span><span class="sxs-lookup"><span data-stu-id="6d06f-322">These tiles are found in the associated tab as a quick reference.</span></span> <span data-ttu-id="6d06f-323">HR 支持适用于轻型问答&在组织中启动新项目或计划时提供快速支持。</span><span class="sxs-lookup"><span data-stu-id="6d06f-323">HR Support works well for light weight Q&A and to provide quick support when launching new projects or initiatives in the organization.</span></span>

[<span data-ttu-id="6d06f-324">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-324">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-hrsupport-app)

![HR 支持](../assets/images/expert-user.png)

## <a name="icebreaker"></a><span data-ttu-id="6d06f-326">Icebreaker</span><span class="sxs-lookup"><span data-stu-id="6d06f-326">Icebreaker</span></span>

<span data-ttu-id="6d06f-327">Icebreaker 是一[Microsoft Teams](../bots/what-are-bots.md)聊天机器人，通过每周配对两个随机团队成员来开会来帮助你的团队建立关系。</span><span class="sxs-lookup"><span data-stu-id="6d06f-327">Icebreaker is a [Microsoft Teams bot](../bots/what-are-bots.md) that helps your team get closer by pairing two random team members up every week to meet.</span></span> <span data-ttu-id="6d06f-328">自动程序通过自动建议适用于这两个成员的空闲时间来轻松安排日程。</span><span class="sxs-lookup"><span data-stu-id="6d06f-328">The bot makes scheduling easy by automatically suggesting free times that work for both members.</span></span> <span data-ttu-id="6d06f-329">通过此应用加强个人连接并构建紧密社区。</span><span class="sxs-lookup"><span data-stu-id="6d06f-329">Strengthen personal connections and build a tightly knit community with this app.</span></span>

<span data-ttu-id="6d06f-330">除了鼓励整个团队中的个人连接之外，Icebreaker 应用还可以帮助促进组织中基于兴趣的社区。</span><span class="sxs-lookup"><span data-stu-id="6d06f-330">In addition to encouraging personal connections across your entire team, the Icebreaker app can help cultivate interest-based communities within your organization.</span></span> <span data-ttu-id="6d06f-331">例如，你可以将该应用用于一个DevOps组，以帮助在组织中自然地传播想法和最佳做法。</span><span class="sxs-lookup"><span data-stu-id="6d06f-331">For example, you can use this app for a DevOps interest group to help ideas and best practices organically spread across your organization.</span></span>

[<span data-ttu-id="6d06f-332">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-332">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-icebreaker-app)

![Icebreaker 应用](../assets/images/icebreaker.png)

## <a name="incentives"></a><span data-ttu-id="6d06f-334">奖励</span><span class="sxs-lookup"><span data-stu-id="6d06f-334">Incentives</span></span>

<span data-ttu-id="6d06f-335">奖励是一[Power Apps](/powerapps/maker/canvas-apps/embed-teams-app)模板，用于管理和跟踪已激活的员工参与指定活动，如培训和变更管理计划。</span><span class="sxs-lookup"><span data-stu-id="6d06f-335">Incentives is a [Power Apps](/powerapps/maker/canvas-apps/embed-teams-app) template that manages and tracks incentivized employee participation in designated activities, such as trainings and change management initiatives.</span></span> <span data-ttu-id="6d06f-336">管理员使用该应用建立指定活动、分配完成分数，并指定奖励所需的资格点级别。</span><span class="sxs-lookup"><span data-stu-id="6d06f-336">Admins use the app to establish designated activities, assign points for completion, and specify required eligibility point levels for rewards.</span></span> <span data-ttu-id="6d06f-337">员工使用应用查看累积的积分，在达到资格后，请求和申请可兑换奖励。</span><span class="sxs-lookup"><span data-stu-id="6d06f-337">Employees use the app to view their accumulated points and, upon reaching eligibility, request and claim redeemable rewards.</span></span>

[<span data-ttu-id="6d06f-338">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-338">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incentives)

![奖励应用演示](../assets/images/incentives-app.png)

## <a name="incident-reporter"></a><span data-ttu-id="6d06f-340">事件报告者</span><span class="sxs-lookup"><span data-stu-id="6d06f-340">Incident Reporter</span></span>

<span data-ttu-id="6d06f-341">事件报告[Microsoft Teams](../bots/what-are-bots.md)自动程序，可优化对组织中事件的管理。</span><span class="sxs-lookup"><span data-stu-id="6d06f-341">Incident Reporter is a [Microsoft Teams bot](../bots/what-are-bots.md)  that optimizes the management of incidents in your organization.</span></span> <span data-ttu-id="6d06f-342">自动程序可促进自动事件数据收集、自定义事件报告、相关利益干系人通知和端到端事件跟踪。</span><span class="sxs-lookup"><span data-stu-id="6d06f-342">The bot facilitates automated incident data collection, customized incident reports, relevant stakeholder notifications, and end-to-end incident tracking.</span></span>

[<span data-ttu-id="6d06f-343">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-343">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-incidentreport)

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

## <a name="inspection"></a><span data-ttu-id="6d06f-346">检查</span><span class="sxs-lookup"><span data-stu-id="6d06f-346">Inspection</span></span> 

 <span data-ttu-id="6d06f-347">检查是一Microsoft Teams应用程序，使前端工作人员可以检查从位置到资产和设备之间的任何内容。</span><span class="sxs-lookup"><span data-stu-id="6d06f-347">Inspection is a Microsoft Teams app that enables front line workers to inspect anything from  locations to assets and equipments.</span></span> <span data-ttu-id="6d06f-348">例如，零售商店、制造工厂或车辆和计算机。</span><span class="sxs-lookup"><span data-stu-id="6d06f-348">For example, a retail store, manufacturing plant, or vehicles and machines.</span></span> <span data-ttu-id="6d06f-349">此解决方案中具有两个应用，每个应用都适用于不同类型的用户。</span><span class="sxs-lookup"><span data-stu-id="6d06f-349">There are two apps in this solution, each intended for different types of users.</span></span>

<span data-ttu-id="6d06f-350">该应用使第一线工作人员能够检查资产或区域，管理产品和服务的质量，或维护工作场所的安全性。</span><span class="sxs-lookup"><span data-stu-id="6d06f-350">The app empowers the front line workers to inspect an asset or area, to manage quality of products and services, or maintain safety at workplace.</span></span> <span data-ttu-id="6d06f-351">它便于工作组成员之间的通信，以解决在检查过程中发现的问题。</span><span class="sxs-lookup"><span data-stu-id="6d06f-351">It facilitates communication between team members to address issues found during inspection.</span></span> <span data-ttu-id="6d06f-352">该应用为经理提供了简单的报告，以加快问题解决并突出显示趋势。</span><span class="sxs-lookup"><span data-stu-id="6d06f-352">The app provides simple reports for managers to expedite issue resolution and highlight trends.</span></span>

[<span data-ttu-id="6d06f-353">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-353">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-inspection)

 ![检查概述](../assets/images/inspection-app.png)  


## <a name="issue-reporting"></a><span data-ttu-id="6d06f-355">问题报告</span><span class="sxs-lookup"><span data-stu-id="6d06f-355">Issue Reporting</span></span>

<span data-ttu-id="6d06f-356">问题报告应用程序使员工和经理能够提出和管理问题。</span><span class="sxs-lookup"><span data-stu-id="6d06f-356">The Issue Reporting app empowers the employees and managers to raise and manage issues.</span></span> <span data-ttu-id="6d06f-357">它包含两个应用：用于报告问题的"问题报告"应用和用于管理问题的"管理问题"应用。</span><span class="sxs-lookup"><span data-stu-id="6d06f-357">It consists of two apps, Issue reporting app for reporting issues and Manage Issues app for managing issues.</span></span>

<span data-ttu-id="6d06f-358">团队经理使用"管理问题"应用配置应用体验，包括Microsoft Teams创建邮件和 Planner 任务的频道。</span><span class="sxs-lookup"><span data-stu-id="6d06f-358">The team managers use the Manage Issues app to configure the app experience, including the channel in which Microsoft Teams messages and Planner tasks are created by the app.</span></span> <span data-ttu-id="6d06f-359">管理员还使用该应用创建模板表单，以在用户报告问题时收集详细信息。</span><span class="sxs-lookup"><span data-stu-id="6d06f-359">Managers also use the app to create template forms to collect details when a user reports an issue.</span></span> <span data-ttu-id="6d06f-360">例如，查看、编辑或删除问题模板表单。</span><span class="sxs-lookup"><span data-stu-id="6d06f-360">For example, review, edit, or delete issue template forms.</span></span> <span data-ttu-id="6d06f-361">该应用还用于查看团队问题、报告问题历史记录并高效管理问题解决。</span><span class="sxs-lookup"><span data-stu-id="6d06f-361">The app is also used to review team issues, report on issue history, and efficiently manage issue resolution.</span></span>

<span data-ttu-id="6d06f-362">员工使用问题报告应用记录解决问题所需的问题和详细信息。</span><span class="sxs-lookup"><span data-stu-id="6d06f-362">The employees use the Issue reporting app to log issues and details required to resolve them.</span></span> <span data-ttu-id="6d06f-363">该应用还用于修改和解决现有问题，并获取个人或团队问题的高级别视图。</span><span class="sxs-lookup"><span data-stu-id="6d06f-363">The app is also used to modify and resolve existing issues and get a high-level view of individual or team issues.</span></span>

[<span data-ttu-id="6d06f-364">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-364">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-issuereporting)

![问题报告团队视图](../assets/images/issue-reporting-team-view.png)  

## <a name="new-employee-onboarding"></a><span data-ttu-id="6d06f-366">新员工入职培训</span><span class="sxs-lookup"><span data-stu-id="6d06f-366">New Employee Onboarding</span></span> 

<span data-ttu-id="6d06f-367">新员工入职培训是Microsoft Teams SharePoint新员工入职培训解决方案，[](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19)使组织能够在新员工旅程中为员工提供一致、高质量的入职体验。</span><span class="sxs-lookup"><span data-stu-id="6d06f-367">New Employee Onboarding is an integrated Microsoft Teams and [SharePoint New Employee Onboarding Solution](https://lookbook.microsoft.com/details/75e60a32-9849-4ed4-b83e-b2b08983ad19) that enables your organization to provide a consistent, high-quality onboarding experience for employees on their new-hire journey.</span></span> <span data-ttu-id="6d06f-368">人力资源团队和招聘经理使用该应用在整个定向和入职培训过程中提供相关信息，由新员工用来共享反馈、提供简介和完成载入任务。</span><span class="sxs-lookup"><span data-stu-id="6d06f-368">The app is used by human resource teams and hiring managers to provide relevant information throughout the orientation and induction process and by new hires to share feedback, provide introductions, and complete onboarding tasks.</span></span>

[<span data-ttu-id="6d06f-369">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-369">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-newemployeeonboarding)

:::row:::
  :::column span="2":::
    <span data-ttu-id="6d06f-370">**新员工欢迎卡片** ![新员工欢迎卡片的图像](../assets/images/new-employee-welcome-card.png)</span><span class="sxs-lookup"><span data-stu-id="6d06f-370">**New employee welcome card** ![Image of new employee welcome card](../assets/images/new-employee-welcome-card.png)</span></span>
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    <span data-ttu-id="6d06f-371">**新员工清单** ![新员工清单的图像](../assets/images/new-employee-checklist.png)</span><span class="sxs-lookup"><span data-stu-id="6d06f-371">**New employee checklist** ![Image of new employee checklist](../assets/images/new-employee-checklist.png)</span></span>  
:::column-end:::
:::row-end:::

## <a name="open-badges"></a><span data-ttu-id="6d06f-372">打开锁屏提醒</span><span class="sxs-lookup"><span data-stu-id="6d06f-372">Open Badges</span></span>

<span data-ttu-id="6d06f-373">开放锁屏提醒是Microsoft Teams一款应用，使个人能够在企业上下文中获得数字学习Teams徽章，并可在任何位置共享。</span><span class="sxs-lookup"><span data-stu-id="6d06f-373">Open Badges is a Microsoft Teams app that enables individuals to earn digital learning credential badges within the Teams context and share them everywhere.</span></span> <span data-ttu-id="6d06f-374">使用来自第三方数字锁屏提醒颁发机构 [Badgr](https://badgr.org/)的功能，已授予徽章记录在收件人的 Badgr 配置文件中，可用于生成和共享生命周期学习旅程的丰富图片。</span><span class="sxs-lookup"><span data-stu-id="6d06f-374">Using capabilities from the third-party digital badge issuing authority, [Badgr](https://badgr.org/), awarded badges are recorded in a recipient's Badgr profile and available to build and share a rich picture of lifetime learning journeys.</span></span>

[<span data-ttu-id="6d06f-375">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-375">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-openbadges)

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

## <a name="poll"></a><span data-ttu-id="6d06f-378">投票</span><span class="sxs-lookup"><span data-stu-id="6d06f-378">Poll</span></span> 

<span data-ttu-id="6d06f-379">投票是一Microsoft Teams消息扩展应用，[](../messaging-extensions/what-are-messaging-extensions.md)它使您能够在聊天或频道中快速创建和发送投票，以收集团队的意见和偏好。</span><span class="sxs-lookup"><span data-stu-id="6d06f-379">Poll is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to quickly create and send polls in a chat or a channel to gather team opinions and preferences.</span></span> <span data-ttu-id="6d06f-380">该应用在所有 Teams 平台客户端（如桌面、浏览器、iOS 和 Android）中均受支持，并且已准备好部署为 Microsoft 365 订阅的一部分。</span><span class="sxs-lookup"><span data-stu-id="6d06f-380">The app is supported across all Teams platform clients, such as desktop, browser, iOS, and Android and is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="6d06f-381">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-381">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-poll-app)

:::row:::
  :::column span="1":::
    ![在视图视图中Teams轮询](../assets/images/poll-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="quick-responses"></a><span data-ttu-id="6d06f-383">快速响应</span><span class="sxs-lookup"><span data-stu-id="6d06f-383">Quick Responses</span></span>

<span data-ttu-id="6d06f-384">快速响应是一Microsoft Teams应用程序，可提供一个可靠解决方案，有效回答用户的常见问题常见问题。</span><span class="sxs-lookup"><span data-stu-id="6d06f-384">Quick Responses is a Microsoft Teams app that delivers a robust solution for effectively answering users' commonly asked questions FAQs.</span></span> <span data-ttu-id="6d06f-385">应用通过消息传递扩展构建交互式用户体验响应库，而不是手动且连续地Teams[信息](../messaging-extensions/what-are-messaging-extensions.md)。</span><span class="sxs-lookup"><span data-stu-id="6d06f-385">Instead of answering each query manually and continuously repeating information, the app builds a library of responses for an interactive user experience through Teams [messaging extensions](../messaging-extensions/what-are-messaging-extensions.md).</span></span>

[<span data-ttu-id="6d06f-386">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-386">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quickresponses)

![响应示例视图](../assets/images/quick-responses.png)

## <a name="quiz--9734"></a><span data-ttu-id="6d06f-388">测验&#9734;</span><span class="sxs-lookup"><span data-stu-id="6d06f-388">Quiz  &#9734;</span></span>

<span data-ttu-id="6d06f-389">测验是一[个Teams](../messaging-extensions/what-are-messaging-extensions.md)扩展应用，可用于在聊天或频道内创建测验，用于进行知识检查和即时结果。</span><span class="sxs-lookup"><span data-stu-id="6d06f-389">Quiz is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a quiz within a chat or a channel for knowledge check and instantaneous results.</span></span> <span data-ttu-id="6d06f-390">可以使用测验、课堂和离线考试、团队内的知识检查，以及团队中的有趣测验。</span><span class="sxs-lookup"><span data-stu-id="6d06f-390">You can use Quiz for, In-class and offline exams, Knowledge check within team, and for fun quizzes within a team.</span></span> <span data-ttu-id="6d06f-391">测验应用支持跨多个平台，Teams、浏览器、iOS 和 Android 客户端。</span><span class="sxs-lookup"><span data-stu-id="6d06f-391">Quiz app is supported across multiple platforms, such as Teams desktop, browser, iOS, and Android clients.</span></span> <span data-ttu-id="6d06f-392">此应用已准备好作为现有订阅的一Microsoft 365部署。</span><span class="sxs-lookup"><span data-stu-id="6d06f-392">This app is ready for deployment as part of your existing Microsoft 365 subscription.</span></span>

[<span data-ttu-id="6d06f-393">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-393">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-quiz)

:::row:::
  :::column span="1":::
    ![在视图视图中Teams测验](../assets/images/quiz-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="rapid-assist"></a><span data-ttu-id="6d06f-395">快速协助</span><span class="sxs-lookup"><span data-stu-id="6d06f-395">Rapid Assist</span></span>

<span data-ttu-id="6d06f-396">快速协助是一款基于 Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) 的应用，面向客户的关联人员可以快速与专家联系，以快速获得答案、搜索信息、跟进打开的请求，并允许专家接收通知以快速接听电话以帮助回答问题。</span><span class="sxs-lookup"><span data-stu-id="6d06f-396">Rapid Assist is a Microsoft [Power Platform](https://powerapps.microsoft.com/blog/now-in-preview-customize-teams-with-built-in-power-platform-capabilities/) based app that allows customer facing associates to rapidly connect with the experts to get quick answers, search for information, follow up open requests, and allow experts to receive notifications to quickly get on a call to help answer questions.</span></span> <span data-ttu-id="6d06f-397">使用 Microsoft [Power Apps](/powerapps/powerapps-overview)和[Power Automate](/power-automate/getting-started)构建的应用与 Microsoft Teams 深度集成，使组织能够轻松地将一线员工与公司代表联系，从而解决客户查询并提供出色的客户体验。</span><span class="sxs-lookup"><span data-stu-id="6d06f-397">The app built using Microsoft [Power Apps](/powerapps/powerapps-overview) and [Power Automate](/power-automate/getting-started), deeply integrates with Microsoft Teams to enable organizations to easily connect frontline workers with corporate liaisons to resolve customer queries and deliver a great customer experience.</span></span> 

[<span data-ttu-id="6d06f-398">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-398">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-rapid-assist)

:::row:::
   :::column span="":::
     ![最终用户请求界面](../assets/images/EndUserHome.png)
   :::column-end:::
   :::column span="":::
      ![专家请求视图](../assets/images/ExpertViewRequests.png)
   :::column-end:::
:::row-end:::

## <a name="reflect"></a><span data-ttu-id="6d06f-401">反射</span><span class="sxs-lookup"><span data-stu-id="6d06f-401">Reflect</span></span> 

<span data-ttu-id="6d06f-402">"反映"是Microsoft Teams应用，它[](../messaging-extensions/what-are-messaging-extensions.md)可为团队成员提供安全且包含的资源，以与同事或组领导直接在 Teams 中共享其情绪Teams。</span><span class="sxs-lookup"><span data-stu-id="6d06f-402">Reflect is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that provides a safe and inclusive resource for your team members to share the state of their emotional well-being with colleagues or group leaders directly within Teams.</span></span> <span data-ttu-id="6d06f-403">该应用在频道、组、会议以及一对一聊天中可用，并且签入响应设置为公共、私人到发件人或完全匿名。</span><span class="sxs-lookup"><span data-stu-id="6d06f-403">The app is available in channel, group, meeting, and 1:1 chats and the check-in response is set to public, private-to-sender, or fully anonymous.</span></span>

[<span data-ttu-id="6d06f-404">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-404">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-App-Reflect)

:::row:::
    :::column:::
    <span data-ttu-id="6d06f-405">**健康投票**</span><span class="sxs-lookup"><span data-stu-id="6d06f-405">**Well-being poll**</span></span>
    
    ![反映应用用户轮询](../assets/images/reflect-app-user-poll.png)
    :::column-end:::
:::row-end:::

## <a name="remote-support"></a><span data-ttu-id="6d06f-407">远程支持</span><span class="sxs-lookup"><span data-stu-id="6d06f-407">Remote Support</span></span>

<span data-ttu-id="6d06f-408">远程[支持是Microsoft Teams](../bots/what-are-bots.md)自动程序，可为整个组织的支持请求者和内部支持团队提供一个集中的界面。</span><span class="sxs-lookup"><span data-stu-id="6d06f-408">Remote Support is a [Microsoft Teams bot](../bots/what-are-bots.md) that provides a focused interface between support requesters throughout your organization and the internal support team.</span></span>  <span data-ttu-id="6d06f-409">最终用户可以提交、编辑或撤消支持请求，支持团队可以在所有支持平台内响应、管理和Teams请求。</span><span class="sxs-lookup"><span data-stu-id="6d06f-409">End-users can submit, edit, or withdraw requests for support and the support team can respond, manage, and update requests all within the Teams platform.</span></span>

[<span data-ttu-id="6d06f-410">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-410">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-remotesupport)

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

## <a name="request-a-team"></a><span data-ttu-id="6d06f-413">请求团队</span><span class="sxs-lookup"><span data-stu-id="6d06f-413">Request-a-team</span></span>

<span data-ttu-id="6d06f-414">请求团队是一个Microsoft Teams应用程序，可优化企业组织的新团队创建。</span><span class="sxs-lookup"><span data-stu-id="6d06f-414">Request-a-team is a Microsoft Teams app that optimizes new team creation for your enterprise organization.</span></span> <span data-ttu-id="6d06f-415">应用通过集成向导引导的请求表单、嵌入式审批流程、请求状态仪表板和自动化团队生成来创建新团队实例时，支持标准化和最佳做法。</span><span class="sxs-lookup"><span data-stu-id="6d06f-415">The app supports standardization and best practices when creating new team instances through the integration of a wizard-guided request form, an embedded approval process, a request status dashboard, and automated team builds.</span></span>

[<span data-ttu-id="6d06f-416">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-416">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-requestateam)

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

## <a name="scrums-for-channels"></a><span data-ttu-id="6d06f-419">适用于频道的 Scrums</span><span class="sxs-lookup"><span data-stu-id="6d06f-419">Scrums for Channels</span></span>

<span data-ttu-id="6d06f-420">适用于频道的 Scrums 是一个 scrum 助手应用，使用户能够在 Microsoft Teams 内的频道中安排和运行 scrum。</span><span class="sxs-lookup"><span data-stu-id="6d06f-420">Scrums for Channels is a scrum assistant app that enables users to schedule and run scrums in channels within Microsoft Teams.</span></span> <span data-ttu-id="6d06f-421">该应用非常适用于由来自不同地理位置和时区的成员组成的远程团队和团队，以共享每日更新并确保参与大量独立会议。</span><span class="sxs-lookup"><span data-stu-id="6d06f-421">The app is great for remote teams and teams comprised of members from varied geographical locations and time zones to share daily updates and ensure participation in scrum stand-up meetings.</span></span>

[<span data-ttu-id="6d06f-422">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-422">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforchannels)

> [!NOTE]
> <span data-ttu-id="6d06f-423">若要在群聊中召开 scrum 会议，请参阅 [Scrums for Group Chat](#scrums-for-group-chat) 应用模板。</span><span class="sxs-lookup"><span data-stu-id="6d06f-423">To conduct scrum meetings in a group chat, see [Scrums for Group Chat](#scrums-for-group-chat) app template.</span></span>

:::row:::
  :::column span="2":::
    ![通道设置视图的 Scrum](../assets/images/scrum-for-channels-settings.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![频道团队成员状态视图的 Scrums](../assets/images/scrum-for-channels-status.png)
:::column-end:::
:::row-end:::

## <a name="scrums-for-group-chat"></a><span data-ttu-id="6d06f-426">用于群聊的 Scrums</span><span class="sxs-lookup"><span data-stu-id="6d06f-426">Scrums for Group Chat</span></span>

> [!NOTE]
> <span data-ttu-id="6d06f-427">Scrums 状态应用模板已更新，现为用于群聊的 Scrums。</span><span class="sxs-lookup"><span data-stu-id="6d06f-427">The Scrums Status app template is updated and is now Scrums for Group Chat.</span></span>

<span data-ttu-id="6d06f-428">适用于群聊的 Scrums 是一种支持性的 scrum 助手，允许群聊成员运行异步独立会议并轻松共享其每日更新。</span><span class="sxs-lookup"><span data-stu-id="6d06f-428">Scrums for Group Chat is a supportive scrum assistant that enables group chat members to run asynchronous stand-up meetings and easily share their daily updates.</span></span> <span data-ttu-id="6d06f-429">它允许群聊的所有成员参与 scrum，并查看运行中的 scrum 中其他人的更新。</span><span class="sxs-lookup"><span data-stu-id="6d06f-429">It allows all members of the group chat to contribute to the scrum and view the updates made by others in the running scrum.</span></span>

[<span data-ttu-id="6d06f-430">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-430">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-scrumsforgroupchat)

![用于群聊演示的 Scrums](https://raw.githubusercontent.com/wiki/OfficeDev/microsoft-teams-app-scrumstatus/images/StartScrum.jpg)

## <a name="share-now"></a><span data-ttu-id="6d06f-432">现在共享</span><span class="sxs-lookup"><span data-stu-id="6d06f-432">Share Now</span></span> 

<span data-ttu-id="6d06f-433">"现在共享"应用使用户能够轻松地在工作环境中共享内容，从而推动同事之间的Teams交换。</span><span class="sxs-lookup"><span data-stu-id="6d06f-433">The Share Now app promotes the positive exchange of information between colleagues by enabling your users to easily share content within the Teams environment.</span></span> <span data-ttu-id="6d06f-434">用户通过应用与团队成员共享感兴趣的项目、发现新的共享内容、设置首选项和书签收藏夹以便稍后阅读。</span><span class="sxs-lookup"><span data-stu-id="6d06f-434">Users engage the app to share items of interest with team members, discover new shared content, set preferences, and bookmark favorites for later reading.</span></span>

[<span data-ttu-id="6d06f-435">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-435">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-sharenow)

![选择内容视图](../assets/images/share-now-suggested-content.png)

## <a name="sharepoint-list-search"></a><span data-ttu-id="6d06f-437">SharePoint 列表搜索</span><span class="sxs-lookup"><span data-stu-id="6d06f-437">SharePoint List Search</span></span>

<span data-ttu-id="6d06f-438">协作Microsoft Teams通常引用列表项中包含的SharePoint信息。</span><span class="sxs-lookup"><span data-stu-id="6d06f-438">Collaboration in Microsoft Teams quite often references information contained within items in a SharePoint list.</span></span> <span data-ttu-id="6d06f-439">粘贴相关项目的链接会强制每个人从对话切换上下文，查找所需信息，然后返回到Teams继续对话。</span><span class="sxs-lookup"><span data-stu-id="6d06f-439">Paste a link to the item in question forces everyone to switch context away from the conversation, find the needed information, then return to Teams to continue the conversation.</span></span> <span data-ttu-id="6d06f-440">随着对话的继续，用户必须多次切换回引用项目，以验证新注释并刷新其对项目中包含的信息的了解。</span><span class="sxs-lookup"><span data-stu-id="6d06f-440">As the conversation continues  people have to switch back to the reference item multiple times to verify new comments and refresh their memories of the information contained within the item.</span></span> <span data-ttu-id="6d06f-441">此上下文切换为顺利协作创建了障碍。</span><span class="sxs-lookup"><span data-stu-id="6d06f-441">This context switching creates a barrier to smooth collaboration.</span></span>
<span data-ttu-id="6d06f-442">若要解决此问题，使用了"列表搜索"应用模板。</span><span class="sxs-lookup"><span data-stu-id="6d06f-442">To resolve this problem, the List Search app template is used.</span></span> <span data-ttu-id="6d06f-443">许多用户使用 SharePoint为组织中某些核心工作流提供电源。</span><span class="sxs-lookup"><span data-stu-id="6d06f-443">Many users use SharePoint to power some of the core workflows in their organizations.</span></span> <span data-ttu-id="6d06f-444">但是，很难围绕列表进行协作。</span><span class="sxs-lookup"><span data-stu-id="6d06f-444">However, collaborating around lists is difficult.</span></span> <span data-ttu-id="6d06f-445">通过使用 Microsoft Teams 中的"列表搜索"应用模板，用户可以直接在聊天对话中插入 SharePoint 列表项的信息，以缓解仅将链接插入聊天时导致的上下文切换。</span><span class="sxs-lookup"><span data-stu-id="6d06f-445">Using the List Search app template in Microsoft Teams, users can insert information from SharePoint list items directly within a chat conversation to alleviate the context-switching caused when simply inserting a link into a chat.</span></span> <span data-ttu-id="6d06f-446">信息作为易于阅读的自动格式化卡片插入，帮助用户继续参与对话。</span><span class="sxs-lookup"><span data-stu-id="6d06f-446">The information is inserted as an easy-to-read auto-formatted card, helping the users stay engaged in the conversation.</span></span>

[<span data-ttu-id="6d06f-447">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-447">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-list-search-app)

![列出搜索应用程序](../assets/images/list-search-template.png)

## <a name="staff-check-ins"></a><span data-ttu-id="6d06f-449">员工签入</span><span class="sxs-lookup"><span data-stu-id="6d06f-449">Staff Check-ins</span></span>

<span data-ttu-id="6d06f-450">员工签入是一种[基于Power Apps](/powerapps/powerapps-overview)应用程序，支持你的业务和现场人员之间的监督通信。</span><span class="sxs-lookup"><span data-stu-id="6d06f-450">Staff Check-ins is a [Power Apps](/powerapps/powerapps-overview) based app that enables oversight communication between your business and field personnel.</span></span> <span data-ttu-id="6d06f-451">员工可以直接在计划或临时的基础上直接从任务中提供时间关键Teams。</span><span class="sxs-lookup"><span data-stu-id="6d06f-451">Staff can easily provide time-critical information and status updates on either a scheduled or ad-hoc basis directly from Teams.</span></span> <span data-ttu-id="6d06f-452">应用支持实时位置、照片、笔记、提醒通知和自动工作流。</span><span class="sxs-lookup"><span data-stu-id="6d06f-452">The app supports real-time location, photos, notes, reminder notifications, and automated workflows.</span></span>

[<span data-ttu-id="6d06f-453">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-453">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-staffcheckins)

![创建签入视图](../assets/images/staff-check-ins-create.png)

## <a name="survey"></a><span data-ttu-id="6d06f-455">调查</span><span class="sxs-lookup"><span data-stu-id="6d06f-455">Survey</span></span>

<span data-ttu-id="6d06f-456">调查是一Microsoft Teams消息扩展应用，[](../messaging-extensions/what-are-messaging-extensions.md)它使您能够在聊天或频道中创建调查以收集数据并获取可操作见解。</span><span class="sxs-lookup"><span data-stu-id="6d06f-456">Survey is a custom Microsoft Teams [messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables you to create a survey in a chat or a channel to gather data and gain actionable insight.</span></span> <span data-ttu-id="6d06f-457">该应用在所有 Teams 平台客户端（如桌面、浏览器、iOS 和 Android）中均受支持，并且已准备好部署为 Microsoft 365 订阅的一部分。</span><span class="sxs-lookup"><span data-stu-id="6d06f-457">The app is supported across all Teams platform clients, such as desktop, browser, iOS, and Android and is ready for deployment as part of your Microsoft 365 subscription.</span></span>  

[<span data-ttu-id="6d06f-458">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-458">Get it on GitHub</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Survey-app)

:::row:::
  :::column span="2":::
    ![在视图视图中Teams调查](../assets/images/survey-app-template-compose-view.gif)
:::column-end:::
:::row-end:::

## <a name="time-tally"></a><span data-ttu-id="6d06f-460">Time Tally</span><span class="sxs-lookup"><span data-stu-id="6d06f-460">Time Tally</span></span> 

<span data-ttu-id="6d06f-461">一个项目可以包含多个任务，并且可以将各种项目分配给员工。</span><span class="sxs-lookup"><span data-stu-id="6d06f-461">A project can include multiple tasks, and various projects can be assigned to employees.</span></span> <span data-ttu-id="6d06f-462">经理必须了解在员工执行这些任务所花的时间内的项目进度。</span><span class="sxs-lookup"><span data-stu-id="6d06f-462">Managers are required to understand the project progress through the time spent by the employees on these tasks.</span></span> <span data-ttu-id="6d06f-463">这会是一项很麻烦的活动，因为员工需要填写时间表。</span><span class="sxs-lookup"><span data-stu-id="6d06f-463">This can be a cumbersome activity, as the employees need to fill in the timesheets.</span></span> <span data-ttu-id="6d06f-464">利用时间表应用程序，员工能够使用移动设备快速填写其时间表，经理也不需要跟进员工的时间表条目。</span><span class="sxs-lookup"><span data-stu-id="6d06f-464">Time Tally app enables employees to fill their timesheets quickly, using the mobile device, and managers do not have to follow up with employees on the timesheet entry.</span></span> <span data-ttu-id="6d06f-465">经理可以基于资源查看项目利用率，并可以批准或拒绝这些条目。</span><span class="sxs-lookup"><span data-stu-id="6d06f-465">Managers get to view the project utilization based on resources, and they can approve or reject the entries.</span></span> <span data-ttu-id="6d06f-466">发送提醒通知以确保时间表合规性。</span><span class="sxs-lookup"><span data-stu-id="6d06f-466">Reminder notifications are sent to ensure timesheet compliance.</span></span> <span data-ttu-id="6d06f-467">此外，历史数据和使用情况可用于分析。</span><span class="sxs-lookup"><span data-stu-id="6d06f-467">Also, historical data and utilizations are available for analytics.</span></span>

[<span data-ttu-id="6d06f-468">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-468">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-timetally)

![Time Tally](../assets/images/11zon_gif.gif)

## <a name="training--9734"></a><span data-ttu-id="6d06f-470">培训&#9734;</span><span class="sxs-lookup"><span data-stu-id="6d06f-470">Training  &#9734;</span></span>

<span data-ttu-id="6d06f-471">培训是自定义[Teams](../messaging-extensions/what-are-messaging-extensions.md)扩展应用，允许用户在聊天或频道中发布培训，以便进行脱机知识共享和学习。</span><span class="sxs-lookup"><span data-stu-id="6d06f-471">Training is a custom [Teams messaging extension](../messaging-extensions/what-are-messaging-extensions.md) app that enables users to publish a training within a chat or a channel for offline knowledge sharing and upskilling.</span></span> <span data-ttu-id="6d06f-472">该应用支持跨多个 Teams 平台客户端，如桌面、浏览器、iOS 和 Android。</span><span class="sxs-lookup"><span data-stu-id="6d06f-472">The app is supported across multiple Teams platform clients, such as desktop, browser, iOS, and Android.</span></span> <span data-ttu-id="6d06f-473">此应用已准备好作为你的订阅的一Microsoft 365部署。</span><span class="sxs-lookup"><span data-stu-id="6d06f-473">This app is ready for deployment as part of your Microsoft 365 subscription.</span></span>

[<span data-ttu-id="6d06f-474">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-474">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-training)

:::row:::
  :::column span="1":::
    ![Create Training in Teams view](../assets/images/training-app-template-compose-view.gif)  
:::column-end:::
:::row-end:::

## <a name="virtual-rounding"></a><span data-ttu-id="6d06f-476">虚拟舍入</span><span class="sxs-lookup"><span data-stu-id="6d06f-476">Virtual Rounding</span></span>

<span data-ttu-id="6d06f-477">医院和紧急会议室提供商每天 **进行许多** 轮次。</span><span class="sxs-lookup"><span data-stu-id="6d06f-477">Hospital and emergency room providers make many **rounds** per day.</span></span> <span data-ttu-id="6d06f-478">这些患者快速签入旨在提供对患者情况的状态检查，并确保解决患者的问题。</span><span class="sxs-lookup"><span data-stu-id="6d06f-478">These quick check-ins on patients are intended to provide a status check on how the patient is doing and ensure that the patient’s concerns are addressed.</span></span> <span data-ttu-id="6d06f-479">尽管舍入是确保由多种类型的提供商监控患者的基本做法，但是它们表示 PPE 会消耗大量资源，因为每次访问时，每个提供商会使用一个新的掩码和一组新的面罩。</span><span class="sxs-lookup"><span data-stu-id="6d06f-479">While rounding is an essential practice to ensure patients are being monitored by multiple types of providers, they represent a huge drain on PPE, because for each visit, from each provider, a new mask, and new set of gloves are used.</span></span> <span data-ttu-id="6d06f-480">使用此应用模板，医疗工作者可以通过提供商和患者之间的Microsoft Teams轻松进行轮次。</span><span class="sxs-lookup"><span data-stu-id="6d06f-480">With this app templates, medical workers can easily conduct rounds virtually, through a Microsoft Teams meeting between the provider and the patient.</span></span>

<span data-ttu-id="6d06f-481">虚拟舍入解决方案还被《Microsoft Health和科学》[博客文章引用](https://aka.ms/teamsvirtualrounding)。</span><span class="sxs-lookup"><span data-stu-id="6d06f-481">The Virtual Rounding solution is also referenced in the Microsoft Health and Life Sciences [blog post](https://aka.ms/teamsvirtualrounding).</span></span>

[<span data-ttu-id="6d06f-482">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-482">Get it on GitHub</span></span>](https://github.com/SmartterHealth/Virtual-Rounding)

![虚拟舍入](../assets/images/virtual-rounding-overview.png)

## <a name="visitor-management"></a><span data-ttu-id="6d06f-484">访问者管理</span><span class="sxs-lookup"><span data-stu-id="6d06f-484">Visitor Management</span></span>

<span data-ttu-id="6d06f-485">利用访问者管理应用，组织和员工可以直接从网站管理中心轻松高效地管理Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="6d06f-485">The Visitor Management app enables your organization and employees to easily and efficiently manage the on-site visitor process, directly from Microsoft Teams.</span></span> <span data-ttu-id="6d06f-486">利用该应用，员工可以创建访问者请求、通过访问者仪表板集中跟踪请求状态，以及当访问者到达时接收实时通知。</span><span class="sxs-lookup"><span data-stu-id="6d06f-486">The app enables employees to create visitor requests, centrally track a request status through the visitor dashboard, and receive real-time notifications when a visitor arrives.</span></span>

[<span data-ttu-id="6d06f-487">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-487">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-app-visitormanagement)

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

## <a name="workplace-awards"></a><span data-ttu-id="6d06f-490">Workplace Awards</span><span class="sxs-lookup"><span data-stu-id="6d06f-490">Workplace Awards</span></span>

<span data-ttu-id="6d06f-491">Workplace Workplace Workplace 是一Teams一款应用模板，提供一个积极框架，促进员工在现代工作场所中的认知和培养文化。</span><span class="sxs-lookup"><span data-stu-id="6d06f-491">Workplace Awards is a Teams app template that provides a positive framework to foster recognition and encourage the culture of employee appreciation in the modern workplace.</span></span> <span data-ttu-id="6d06f-492">该应用使你能够设置和管理员工奖励和识别，称为 R&R 计划，员工可以在该计划中轻松指定和认可同事，R&R 领导者可以查看提交的候选人、授予奖励和宣布收件人。</span><span class="sxs-lookup"><span data-stu-id="6d06f-492">The app enables you to setup and manage an employee rewards and recognition, called R&R program where employees can easily nominate and endorse colleagues and your R&R leader can view submitted nominations, grant awards, and announce recipients.</span></span>

[<span data-ttu-id="6d06f-493">获取GitHub</span><span class="sxs-lookup"><span data-stu-id="6d06f-493">Get it on GitHub</span></span>](https://github.com/OfficeDev/microsoft-teams-apps-workplaceawards)

:::row:::
  :::column span="2":::
    ![<span data-ttu-id="6d06f-494">工作区候选人卡</span><span class="sxs-lookup"><span data-stu-id="6d06f-494">Workplace awards nomination card</span></span> ](../assets/images/workplace-awards-nominate.png)
:::column-end:::
:::row-end:::
:::row:::
:::column span="2":::
    ![工作区奖励列表选项卡](../assets/images/workplace-awards-champion-tab.png)
:::column-end:::
:::row-end:::

<span data-ttu-id="6d06f-496">有关应用模板的信息，请参阅应用 [模板](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u)。</span><span class="sxs-lookup"><span data-stu-id="6d06f-496">For more information on app template, see [App template](https://forms.office.com/Pages/ResponsePage.aspx?id=v4j5cvGGr0GRqy180BHbR2_7qFm_lcZAr4eqEhnLsZ9UMVZGT1lCT0FXUDdZMUM0RkpBS1BESTAwWC4u).</span></span>

## <a name="see-also"></a><span data-ttu-id="6d06f-497">另请参阅</span><span class="sxs-lookup"><span data-stu-id="6d06f-497">See also</span></span>

[<span data-ttu-id="6d06f-498">集成 web 应用</span><span class="sxs-lookup"><span data-stu-id="6d06f-498">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
