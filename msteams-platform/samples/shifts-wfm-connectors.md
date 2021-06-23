---
title: 生产准备就绪的排班连接器
description: 员工管理 针对员工的轮班Teams
ms.topic: reference
author: surbhigupta
ms.date: 03/09/2020
localization_priority: Normal
keywords: Microsoft Teams连接器 kronos
ms.author: lajanuar
ms.openlocfilehash: 088c049342c36b4f126b4a9d2f788601378b7db4
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069145"
---
# <a name="production-ready-shifts-connectors"></a><span data-ttu-id="e0f45-104">生产准备就绪的排班连接器</span><span class="sxs-lookup"><span data-stu-id="e0f45-104">Production-ready Shifts Connectors</span></span>  

<span data-ttu-id="e0f45-105">TeamsShifts 员工 (WFM) 连接器是生产就绪型、开放源代码和社区驱动的集成，对一线工作人员非常有用。</span><span class="sxs-lookup"><span data-stu-id="e0f45-105">Teams Shifts Workforce management (WFM) connectors are production-ready, open-source, and community-driven integrations, useful for firstline workers.</span></span> <span data-ttu-id="e0f45-106">它们通过 Shift 为一线员工的数字转换提供了无缝体验Teams流程。</span><span class="sxs-lookup"><span data-stu-id="e0f45-106">They offer a seamless experience and quick process for the digital transformation of firstline workers with Teams Shifts.</span></span> 

<span data-ttu-id="e0f45-107">每个连接器都提供有关部署和集成到组织的详细指导。</span><span class="sxs-lookup"><span data-stu-id="e0f45-107">Each connector provides detailed guidance for deployment and integration to your organization.</span></span> <span data-ttu-id="e0f45-108">完整的源代码可在GitHub中提供。</span><span class="sxs-lookup"><span data-stu-id="e0f45-108">The complete source code is available in GitHub repository.</span></span> <span data-ttu-id="e0f45-109">您可以详细浏览或分叉，并自定义以满足您的特定需求。</span><span class="sxs-lookup"><span data-stu-id="e0f45-109">You can explore in detail or fork, and customize to meet your specific needs.</span></span>   

<span data-ttu-id="e0f45-110">本文档概述了 Teams Shifts WFM 连接器、Kronos 到 Teams Shifts 连接器和 JDA 到 Teams Shifts 连接器的主要优势。</span><span class="sxs-lookup"><span data-stu-id="e0f45-110">This document gives an overview of key benefits of Teams Shifts WFM connectors, Kronos-to-Teams Shifts connector, and JDA-to-Teams Shifts connector.</span></span>

## <a name="key-benefits-of-teams-shifts-wfm-connectors"></a><span data-ttu-id="e0f45-111">Shifts WFM Teams的主要好处</span><span class="sxs-lookup"><span data-stu-id="e0f45-111">Key benefits of Teams Shifts WFM connectors</span></span>

<span data-ttu-id="e0f45-112">下面是 Shifts WFM Teams的主要好处：</span><span class="sxs-lookup"><span data-stu-id="e0f45-112">Following are the key benefits of Teams Shifts WFM connectors:</span></span>

* <span data-ttu-id="e0f45-113">**即插即用体验：** 所有 Shifts WFM 连接器都ARM Azure 部署脚本，这些脚本允许你在 Microsoft Azure 中托管Microsoft Azure。</span><span class="sxs-lookup"><span data-stu-id="e0f45-113">**Plug and play experience:** All Shifts WFM connectors include ARM Azure deployment scripts that allow you to host all necessary services in Microsoft Azure.</span></span> <span data-ttu-id="e0f45-114">部署应用不需要编码。</span><span class="sxs-lookup"><span data-stu-id="e0f45-114">No coding is required to deploy the apps.</span></span>

* <span data-ttu-id="e0f45-115">**生产就绪代码：** 所有 Shifts 连接器都符合建议的安全性和基础结构最佳做法，并检查所有社区提交的更改以确保持续一致性。</span><span class="sxs-lookup"><span data-stu-id="e0f45-115">**Production-ready code:** All  Shifts connectors conform to the recommended security and infrastructure best practices and all community-submitted changes are reviewed to ensure continued conformance.</span></span>

* <span data-ttu-id="e0f45-116">**可自定义和可扩展：**  尽管所有 Shifts WFM 连接器都已准备好部署以立即使用，但整个代码库和部署脚本随时可用。</span><span class="sxs-lookup"><span data-stu-id="e0f45-116">**Customizable and extensible:**  While all Shifts WFM connectors are ready to deploy for immediate use, with the entire code base and deployment scripts readily available.</span></span> <span data-ttu-id="e0f45-117">你可以轻松自定义或扩展它们，以满足你的独特需求。</span><span class="sxs-lookup"><span data-stu-id="e0f45-117">You can easily customize or extend them to fit your unique needs.</span></span>

* <span data-ttu-id="e0f45-118">**详细的文档&支持：**  所有 Shifts WFM 连接器都附带了有关解决方案体系结构、部署和配置步骤的端到端文档。</span><span class="sxs-lookup"><span data-stu-id="e0f45-118">**Detailed documentation & support:**  All Shifts WFM connectors are accompanied by end-to-end documentation for solution architecture, deployment, and configuration steps.</span></span> <span data-ttu-id="e0f45-119">连接器存储库受到监视，以便可以通过存储库的"问题跟踪器"报告遇到GitHub问题。</span><span class="sxs-lookup"><span data-stu-id="e0f45-119">The connector repositories are monitored, so that you can report any issues, challenges or difficulties you encounter through the repo's GitHub Issues tracker.</span></span>

* <span data-ttu-id="e0f45-120">**无缝集成：** WFM 解决方案与 Teams Shifts 之间的集成允许一线工作人员使用 Teams Shifts 应用查看或管理其日程安排和班次时间，并使用 Teams 中提供的所有其他丰富的协作功能，而无需将上下文切换到其他应用。</span><span class="sxs-lookup"><span data-stu-id="e0f45-120">**Seamless integration:** The integration between WFM solutions and Teams Shifts allows firstline workers to use the Teams Shifts app to view or manage their schedules and shift times, and use all the other rich collaboration features provided in Teams right from their mobile device or desktop without having to switch context to another app.</span></span>  

<span data-ttu-id="e0f45-121">**在"打开"视图中打开Teams**</span><span class="sxs-lookup"><span data-stu-id="e0f45-121">**Open shifts view in Teams**</span></span> 

<span data-ttu-id="e0f45-122">以下图像Teams班次视图：</span><span class="sxs-lookup"><span data-stu-id="e0f45-122">The shifts view in Teams is shown in the following image:</span></span> 

![在"打开"Teams](../assets/images/teams-open-shifts-view.png)

## <a name="kronos-to-teams-shifts-connector"></a><span data-ttu-id="e0f45-124">Kronos 到 Teams Shifts 连接器</span><span class="sxs-lookup"><span data-stu-id="e0f45-124">Kronos-to-Teams Shifts connector</span></span>

<span data-ttu-id="e0f45-125">借助开放源代码，可以将 Kronos 员工中心版本 8.1 及以上版本与 Teams 班次（如桌面或移动 Teams 应用）集成，以用于以下一线员工和经理方案：</span><span class="sxs-lookup"><span data-stu-id="e0f45-125">With open-source code, you can integrate Kronos Workforce Central Version 8.1 and above, with Teams Shifts such as, desktop or mobile Teams app for the following firstline worker and manager scenarios:</span></span>

* <span data-ttu-id="e0f45-126">查看日程安排。</span><span class="sxs-lookup"><span data-stu-id="e0f45-126">View schedule.</span></span>

* <span data-ttu-id="e0f45-127">发布和请求打开的班次。</span><span class="sxs-lookup"><span data-stu-id="e0f45-127">Publish and request open shifts.</span></span>

* <span data-ttu-id="e0f45-128">交换班次。</span><span class="sxs-lookup"><span data-stu-id="e0f45-128">Swap shifts.</span></span>

* <span data-ttu-id="e0f45-129">请求请假。</span><span class="sxs-lookup"><span data-stu-id="e0f45-129">Request time off.</span></span>

* <span data-ttu-id="e0f45-130">提供班次。</span><span class="sxs-lookup"><span data-stu-id="e0f45-130">Offer shifts.</span></span>

<span data-ttu-id="e0f45-131">有关部署 Kronos 到 Teams Shifts 连接器[GitHub。](https://aka.ms/KronosShiftsConnector)</span><span class="sxs-lookup"><span data-stu-id="e0f45-131">For more information on deployment of Kronos-to-Teams Shifts connector, see [Get it on GitHub](https://aka.ms/KronosShiftsConnector).</span></span>

## <a name="jda-to-teams-shifts-connector"></a><span data-ttu-id="e0f45-132">JDA 到 Teams Shifts 连接器</span><span class="sxs-lookup"><span data-stu-id="e0f45-132">JDA-to-Teams Shifts connector</span></span>

<span data-ttu-id="e0f45-133">借助开放源代码，你可以将 JDA（如 BlueYonder 版本 17.2 及以上）与 Teams Shift（如桌面或移动 Teams 应用）集成，用于以下一线工作人员和经理方案：</span><span class="sxs-lookup"><span data-stu-id="e0f45-133">With open-source code, you can integrate JDA, such as BlueYonder Version 17.2 and above, with Teams Shifts  such as, desktop or mobile Teams app for the following firstline worker and manager scenarios:</span></span>

* <span data-ttu-id="e0f45-134">在 JDA 中发布班次和计划组，并查看Teams。</span><span class="sxs-lookup"><span data-stu-id="e0f45-134">Publish shifts and schedule groups in JDA and view them in Teams.</span></span>

* <span data-ttu-id="e0f45-135">启用丰富的计划方案，包括请求转换交换和请假。</span><span class="sxs-lookup"><span data-stu-id="e0f45-135">Enable rich scheduling scenarios, including requesting shift swaps and time off.</span></span>

* <span data-ttu-id="e0f45-136">使用适用于班次的[Microsoft Graph API 设置用户可用性](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="e0f45-136">Set user availability using the [Microsoft Graph API for Shifts](/graph/api/resources/shift?view=graph-rest-beta&preserve-view=true).</span></span>

<span data-ttu-id="e0f45-137">有关贡献和建议的信息，请参阅在"开始["GitHub。](https://aka.ms/JDAShiftsConnector)</span><span class="sxs-lookup"><span data-stu-id="e0f45-137">For more information on contribution and suggestion, see [Get it on GitHub](https://aka.ms/JDAShiftsConnector).</span></span></br></br>

## <a name="see-also"></a><span data-ttu-id="e0f45-138">另请参阅</span><span class="sxs-lookup"><span data-stu-id="e0f45-138">See also</span></span>

[<span data-ttu-id="e0f45-139">集成 web 应用</span><span class="sxs-lookup"><span data-stu-id="e0f45-139">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
