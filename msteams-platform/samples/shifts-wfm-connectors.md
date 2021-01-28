---
title: Teams Shifts 连接器
description: Teams 的员工管理班次连接器
ms.topic: reference
author: laujan
ms.date: 03/09/2020
keywords: Microsoft Teams 连接器 kronos
ms.author: lajanuar
ms.openlocfilehash: 9d32c9e1aa3baba660440492df55bb00f677baa4
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014591"
---
# <a name="microsoft-teams-shifts-wfm-connectors"></a><span data-ttu-id="d10c6-104">Microsoft Teams Shifts WFM 连接器</span><span class="sxs-lookup"><span data-stu-id="d10c6-104">Microsoft Teams Shifts WFM connectors</span></span>  

## <a name="workforce-management-connectors-wfm-for-firstline-workers"></a><span data-ttu-id="d10c6-105">适用于一线员工 (WFM) 员工管理连接器</span><span class="sxs-lookup"><span data-stu-id="d10c6-105">Workforce management connectors (WFM) for firstline workers</span></span> 

<span data-ttu-id="d10c6-106">Teams Shifts WFM 连接器是生产就绪、开放源代码和社区驱动的集成，为使用 Teams Shift 实现一线工作人员的数字转换提供了无缝体验和快速流程。</span><span class="sxs-lookup"><span data-stu-id="d10c6-106">Teams Shifts WFM connectors are production-ready, open-source, and community-driven integrations that offer a seamless experience and quick process for the digital transformation of firstline workers with Teams Shifts.</span></span> 

<span data-ttu-id="d10c6-107">每个连接器都提供有关部署和集成到组织的详细指导。</span><span class="sxs-lookup"><span data-stu-id="d10c6-107">Each connector provides detailed guidance for deployment and integration to your organization.</span></span> <span data-ttu-id="d10c6-108">GitHub 存储库中提供了完整的源代码，可在其中详细浏览和/或分叉和定制，以满足你的特定需求。</span><span class="sxs-lookup"><span data-stu-id="d10c6-108">The complete source code is available in our GitHub repo where it can be explored in detail and/or forked and tailored to meet your specific needs.</span></span>

## <a name="key-benefits-teams-shifts-wfm-connectors"></a><span data-ttu-id="d10c6-109">主要优势：Teams Shifts WFM 连接器</span><span class="sxs-lookup"><span data-stu-id="d10c6-109">Key benefits: Teams Shifts WFM connectors</span></span>

* <span data-ttu-id="d10c6-110">**即插即用体验。**</span><span class="sxs-lookup"><span data-stu-id="d10c6-110">**Plug and play experience.**</span></span> <span data-ttu-id="d10c6-111">所有 Shifts WFM 连接器都ARM Azure 部署脚本，允许你在 Microsoft Azure 中托管所有必要的服务。</span><span class="sxs-lookup"><span data-stu-id="d10c6-111">All Shifts WFM connectors include ARM Azure deployment scripts that allow you to host all necessary services in Microsoft Azure.</span></span> <span data-ttu-id="d10c6-112">部署应用不需要编码。</span><span class="sxs-lookup"><span data-stu-id="d10c6-112">No coding is required to deploy the apps.</span></span>

* <span data-ttu-id="d10c6-113">**生产就绪代码。**</span><span class="sxs-lookup"><span data-stu-id="d10c6-113">**Production-ready code.**</span></span> <span data-ttu-id="d10c6-114">所有 Shifts 连接器都符合建议的安全性和基础结构最佳做法，并审查所有社区提交的更改以确保持续一致性。</span><span class="sxs-lookup"><span data-stu-id="d10c6-114">All  Shifts connectors conform to recommended security and infrastructure best practices and all community-submitted changes are reviewed to ensure continued conformance.</span></span>

* <span data-ttu-id="d10c6-115">**可自定义和可扩展。**</span><span class="sxs-lookup"><span data-stu-id="d10c6-115">**Customizable and extensible.**</span></span> <span data-ttu-id="d10c6-116"> 尽管所有 Shifts WFM 连接器都已准备好部署以便立即使用，但我们提供了整个代码库和部署脚本，以便你可以轻松地自定义或扩展它们以满足你的独特需求。</span><span class="sxs-lookup"><span data-stu-id="d10c6-116"> While all Shifts WFM connectors are ready to deploy for immediate use, we provide the entire code base and deployment scripts so that you can easily customize or extend them to fit your unique needs.</span></span>

* <span data-ttu-id="d10c6-117">**详细的文档&支持。**</span><span class="sxs-lookup"><span data-stu-id="d10c6-117">**Detailed documentation & support.**</span></span> <span data-ttu-id="d10c6-118"> 所有 Shifts WFM 连接器都附带了有关解决方案体系结构、部署和配置步骤的端到端文档。</span><span class="sxs-lookup"><span data-stu-id="d10c6-118"> All Shifts WFM connectors are accompanied by end-to-end documentation for solution architecture, deployment, and configuration steps.</span></span> <span data-ttu-id="d10c6-119">连接器存储库受到监视，因此请通过存储库的 GitHub 问题跟踪器报告你遇到的任何问题、挑战或困难。</span><span class="sxs-lookup"><span data-stu-id="d10c6-119">The connector repositories are monitored, so please report any issues, challenges or difficulties you encounter through the repo's GitHub Issues tracker.</span></span>

* <span data-ttu-id="d10c6-120">**无缝集成。**</span><span class="sxs-lookup"><span data-stu-id="d10c6-120">**Seamless integration.**</span></span> <span data-ttu-id="d10c6-121">WFM 解决方案与 Teams Shifts 之间的集成使一线工作人员可以使用 Teams Shifts 应用查看/管理其日程安排和班次时间，并使用它的移动设备或桌面版中提供的所有其他丰富的协作功能，而无需将上下文切换到其他应用。</span><span class="sxs-lookup"><span data-stu-id="d10c6-121">The integration between WFM solutions and Teams Shifts allows firstline workers to use the Teams Shifts app to view/manage their schedules and shift times, and use all the other rich collaboration features provided in Teams right from their mobile device or desktop without having to switch context to another app.</span></span>

<span data-ttu-id="d10c6-122">**Teams 中的"打开班次"视图**</span><span class="sxs-lookup"><span data-stu-id="d10c6-122">**Open shifts view in Teams**</span></span>  
<span data-ttu-id="d10c6-123">![Teams 中的开放班次](../assets/images/teams-open-shifts-view.png)</span><span class="sxs-lookup"><span data-stu-id="d10c6-123">![Open shifts in Teams](../assets/images/teams-open-shifts-view.png)</span></span>

## <a name="kronos-to-teams-shifts-connector"></a><span data-ttu-id="d10c6-124">Kronos-to-Teams Shifts 连接器</span><span class="sxs-lookup"><span data-stu-id="d10c6-124">Kronos-to-Teams Shifts connector</span></span>

<span data-ttu-id="d10c6-125">借助开放源代码，你可以将 Kronos 员工中心版本 8.1 及以上版本与 Teams Shifts (桌面/移动 Teams 应用) 集成，用于以下一线员工和经理方案：</span><span class="sxs-lookup"><span data-stu-id="d10c6-125">With open-source code, you can integrate Kronos Workforce Central Version 8.1 and above, with Teams Shifts (desktop/mobile Teams app) for the following firstline worker and manager scenarios:</span></span>

1. <span data-ttu-id="d10c6-126">查看日程安排。</span><span class="sxs-lookup"><span data-stu-id="d10c6-126">View schedule.</span></span>

1. <span data-ttu-id="d10c6-127">发布和请求打开的班次。</span><span class="sxs-lookup"><span data-stu-id="d10c6-127">Publish and request open shifts.</span></span>

1. <span data-ttu-id="d10c6-128">交换班次。</span><span class="sxs-lookup"><span data-stu-id="d10c6-128">Swap shifts.</span></span>

1. <span data-ttu-id="d10c6-129">请求请假。</span><span class="sxs-lookup"><span data-stu-id="d10c6-129">Request time off.</span></span>

1. <span data-ttu-id="d10c6-130">提供班次。</span><span class="sxs-lookup"><span data-stu-id="d10c6-130">Offer shifts.</span></span>

[<span data-ttu-id="d10c6-131">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="d10c6-131">Get it on GitHub</span></span>]( https://aka.ms/KronosShiftsConnector)

## <a name="jda-to-teams-shifts-connector"></a><span data-ttu-id="d10c6-132">JDA 到 Teams Shifts 连接器</span><span class="sxs-lookup"><span data-stu-id="d10c6-132">JDA-to-Teams Shifts connector</span></span>

<span data-ttu-id="d10c6-133">借助开放源代码，你可以将 JDA (BlueYonder) 版本 17.2 及以上版本与 Teams Shifts (桌面/移动 Teams 应用) 集成，用于以下一线员工和经理方案：</span><span class="sxs-lookup"><span data-stu-id="d10c6-133">With open-source code, you can integrate JDA (BlueYonder) Version 17.2 and above, with Teams Shifts (desktop/mobile Teams app) for the following firstline worker and manager scenarios:</span></span>

1. <span data-ttu-id="d10c6-134">在 JDA 中发布班次和日程安排组，在 Teams 中查看。</span><span class="sxs-lookup"><span data-stu-id="d10c6-134">Publish shifts and schedule groups in JDA and view in Teams.</span></span>

1. <span data-ttu-id="d10c6-135">启用丰富的计划方案，包括请求班次交换和请假。</span><span class="sxs-lookup"><span data-stu-id="d10c6-135">Enable rich scheduling scenarios, including requesting shift swaps and time off.</span></span>

1. <span data-ttu-id="d10c6-136">使用适用于班次的 [Microsoft Graph API 设置用户可用性](/graph/api/resources/shift?view=graph-rest-beta) 。</span><span class="sxs-lookup"><span data-stu-id="d10c6-136">Set  user availability using the [Microsoft Graph API for Shifts](/graph/api/resources/shift?view=graph-rest-beta) .</span></span>

[<span data-ttu-id="d10c6-137">在 GitHub 上获取</span><span class="sxs-lookup"><span data-stu-id="d10c6-137">Get it on GitHub</span></span>](https://aka.ms/JDAShiftsConnector)</br></br>
