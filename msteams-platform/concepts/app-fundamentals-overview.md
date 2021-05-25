---
title: 应用开发基础概述
author: heath-hamilton
description: 介绍开发平台Teams概念。
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 1ecae34c38950f16e49fc123f73bdc746c4b28cc
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630156"
---
# <a name="microsoft-teams-app-development-fundamentals"></a><span data-ttu-id="84ad9-103">Microsoft Teams应用开发基础</span><span class="sxs-lookup"><span data-stu-id="84ad9-103">Microsoft Teams app development fundamentals</span></span>

<span data-ttu-id="84ad9-104">Microsoft Teams应用基础提供创建自定义应用Teams方向。</span><span class="sxs-lookup"><span data-stu-id="84ad9-104">Microsoft Teams app fundamentals give the direction you need to create your custom Teams app.</span></span> <span data-ttu-id="84ad9-105">你可以识别规划应用所需的Teams框架。</span><span class="sxs-lookup"><span data-stu-id="84ad9-105">You can recognize the framework required to plan your Teams app.</span></span> <span data-ttu-id="84ad9-106">本文档可帮助你了解用户-应用通信，并找出你需要使用的应用图面类型或你的应用在进程中可能需要的 API。</span><span class="sxs-lookup"><span data-stu-id="84ad9-106">The document helps you to understand the user-app communication and figure out the kind of app surfaces you need to use or the APIs your app might require in the process.</span></span> <span data-ttu-id="84ad9-107">获得一些灵感，以利用交互性，在集成应用时可加强Teams。</span><span class="sxs-lookup"><span data-stu-id="84ad9-107">Get some inspiration to embrace interactivity that can deepen the app experience when you integrate with Teams.</span></span>

## <a name="capabilities-and-entry-points"></a><span data-ttu-id="84ad9-108">功能和入口点</span><span class="sxs-lookup"><span data-stu-id="84ad9-108">Capabilities and entry points</span></span>

<span data-ttu-id="84ad9-109">可以通过多种方式扩展Teams应用。</span><span class="sxs-lookup"><span data-stu-id="84ad9-109">You can extend your Teams app in multiple ways.</span></span> <span data-ttu-id="84ad9-110">为了能够扩展你的应用，你必须了解在协作空间中工作的所有核心功能和入口点。</span><span class="sxs-lookup"><span data-stu-id="84ad9-110">To be able to extend your app you must understand all the core capabilities and the entry points that work in a collaborative space.</span></span> <span data-ttu-id="84ad9-111">你可以尝试构建应用的扩展点。</span><span class="sxs-lookup"><span data-stu-id="84ad9-111">You can experiment with the extension points for building your apps.</span></span> <span data-ttu-id="84ad9-112">重要应用项目组件可帮助你正确配置应用页面。</span><span class="sxs-lookup"><span data-stu-id="84ad9-112">Important app project components help you to correctly configure your app page.</span></span> <span data-ttu-id="84ad9-113">Teams应用可以[有多个功能和](../concepts/capabilities-overview.md)[入口点](../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="84ad9-113">Teams app can have [multiple capabilities](../concepts/capabilities-overview.md) and [entry points](../concepts/extensibility-points.md).</span></span>

## <a name="understand-your-use-cases"></a><span data-ttu-id="84ad9-114">了解用例</span><span class="sxs-lookup"><span data-stu-id="84ad9-114">Understand your use cases</span></span>

<span data-ttu-id="84ad9-115">你可以识别用户问题并确定用户面临的一些常见问题的解答。</span><span class="sxs-lookup"><span data-stu-id="84ad9-115">You can recognize user issues and identify the answers to some common problems the users face.</span></span> <span data-ttu-id="84ad9-116">可以通过查找Teams满足用户需求的正确组合来构建你的应用。</span><span class="sxs-lookup"><span data-stu-id="84ad9-116">You can build your Teams app by finding the right combination to meet your user's needs.</span></span> <span data-ttu-id="84ad9-117">[了解用例](../concepts/design/understand-use-cases.md) 以了解最终用户如何与你的应用交互。</span><span class="sxs-lookup"><span data-stu-id="84ad9-117">[Understand use cases](../concepts/design/understand-use-cases.md) to know how an end-user interacts with your app.</span></span> <span data-ttu-id="84ad9-118">了解如何了解用户及其问题。</span><span class="sxs-lookup"><span data-stu-id="84ad9-118">You learn to understand the user and their problem.</span></span> <span data-ttu-id="84ad9-119">回答的一些常见问题如下所示：</span><span class="sxs-lookup"><span data-stu-id="84ad9-119">Some common questions answered are as follows:</span></span>

* <span data-ttu-id="84ad9-120">是否需要身份验证？</span><span class="sxs-lookup"><span data-stu-id="84ad9-120">Do you need authentication?</span></span>
* <span data-ttu-id="84ad9-121">你的应用要解决什么问题？</span><span class="sxs-lookup"><span data-stu-id="84ad9-121">What problem is your app going to solve?</span></span>
* <span data-ttu-id="84ad9-122">Who是应用的最终用户吗？</span><span class="sxs-lookup"><span data-stu-id="84ad9-122">Who are the end-users of the app?</span></span>
* <span data-ttu-id="84ad9-123">载入体验应该如何以及应用还可以执行哪些操作？</span><span class="sxs-lookup"><span data-stu-id="84ad9-123">How should the onboarding experience be and what else the app can do?</span></span>

## <a name="map-your-use-cases-to-teams-app-capabilities"></a><span data-ttu-id="84ad9-124">将用例映射到Teams功能</span><span class="sxs-lookup"><span data-stu-id="84ad9-124">Map your use cases to Teams app capabilities</span></span>

<span data-ttu-id="84ad9-125">[映射用例涵盖了](../concepts/design/map-use-cases.md) 一些常见方案以及如何选择应用的功能。</span><span class="sxs-lookup"><span data-stu-id="84ad9-125">[Map your use cases](../concepts/design/map-use-cases.md) covers some common scenarios and how to choose your app's capabilities.</span></span> <span data-ttu-id="84ad9-126">提供了在外部系统中共享应用和协作处理项目的信息。</span><span class="sxs-lookup"><span data-stu-id="84ad9-126">Information to share your app and collaborate on items in an external system is provided.</span></span> <span data-ttu-id="84ad9-127">您还可以了解如何启动工作流和向用户发送通知。</span><span class="sxs-lookup"><span data-stu-id="84ad9-127">You can also learn how to initiate workflows and send notifications to users.</span></span> <span data-ttu-id="84ad9-128">获取有关开始位置、如何与用户社交、对话机器人以及组合多个功能的其他提示。</span><span class="sxs-lookup"><span data-stu-id="84ad9-128">Get additional tips on where to start, how to get social with users, conversational bots, and combining multiple features.</span></span>

## <a name="see-also"></a><span data-ttu-id="84ad9-129">另请参阅</span><span class="sxs-lookup"><span data-stu-id="84ad9-129">See also</span></span>

* [<span data-ttu-id="84ad9-130">将 Web 应用与 Teams</span><span class="sxs-lookup"><span data-stu-id="84ad9-130">Integrate web apps with Teams</span></span>](../samples/integrating-web-apps.md)
* [<span data-ttu-id="84ad9-131">生成首个 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="84ad9-131">Build your first Microsoft Teams app</span></span>](../build-your-first-app/build-first-app-overview.md)

## <a name="next-step"></a><span data-ttu-id="84ad9-132">后续步骤</span><span class="sxs-lookup"><span data-stu-id="84ad9-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="84ad9-133">了解Teams应用功能</span><span class="sxs-lookup"><span data-stu-id="84ad9-133">Understand Teams app capabilities</span></span>](capabilities-overview.md)

