---
title: 应用开发基础概述
author: heath-hamilton
description: 介绍 Teams 平台开发的基础概念。
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: 6d0c22049e828426cfe963da6631b4c289566bf0
ms.sourcegitcommit: a732789190f59ec1f3699e8ad2f06387e8fe1458
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2021
ms.locfileid: "52058458"
---
# <a name="microsoft-teams-app-development-fundamentals"></a><span data-ttu-id="1652b-103">Microsoft Teams 应用开发基础</span><span class="sxs-lookup"><span data-stu-id="1652b-103">Microsoft Teams app development fundamentals</span></span>

<span data-ttu-id="1652b-104">Microsoft Teams 应用基础提供创建自定义 Teams 应用所需的方向。</span><span class="sxs-lookup"><span data-stu-id="1652b-104">Microsoft Teams app fundamentals give the direction you need to create your custom Teams app.</span></span> <span data-ttu-id="1652b-105">你可以识别规划 Teams 应用所需的框架。</span><span class="sxs-lookup"><span data-stu-id="1652b-105">You can recognize the framework required to plan your Teams app.</span></span> <span data-ttu-id="1652b-106">本文档可帮助你了解用户-应用通信，并找出你需要使用的应用图面类型或你的应用在进程中可能需要的 API。</span><span class="sxs-lookup"><span data-stu-id="1652b-106">The document helps you to understand the user-app communication and figure out the kind of app surfaces you need to use or the APIs your app might require in the process.</span></span> <span data-ttu-id="1652b-107">获得一些灵感，以在集成 Teams 时融入可加强应用体验的交互性。</span><span class="sxs-lookup"><span data-stu-id="1652b-107">Get some inspiration to embrace interactivity that can deepen the app experience when you integrate with Teams.</span></span>

## <a name="capabilities-and-entry-points"></a><span data-ttu-id="1652b-108">功能和入口点</span><span class="sxs-lookup"><span data-stu-id="1652b-108">Capabilities and entry points</span></span>

<span data-ttu-id="1652b-109">可以通过多种方式扩展 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="1652b-109">You can extend your Teams app in multiple ways.</span></span> <span data-ttu-id="1652b-110">为了能够扩展你的应用，你必须了解在协作空间中工作的所有核心功能和入口点。</span><span class="sxs-lookup"><span data-stu-id="1652b-110">To be able to extend your app you must understand all the core capabilities and the entry points that work in a collaborative space.</span></span> <span data-ttu-id="1652b-111">你可以尝试构建应用的扩展点。</span><span class="sxs-lookup"><span data-stu-id="1652b-111">You can experiment with the extension points for building your apps.</span></span> <span data-ttu-id="1652b-112">重要应用项目组件可帮助你正确配置应用页面。</span><span class="sxs-lookup"><span data-stu-id="1652b-112">Important app project components help you to correctly configure your app page.</span></span> <span data-ttu-id="1652b-113">Teams 应用可以[有多个功能和](../concepts/capabilities-overview.md)[入口点](../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="1652b-113">Teams app can have [multiple capabilities](../concepts/capabilities-overview.md) and [entry points](../concepts/extensibility-points.md).</span></span>

## <a name="understand-your-use-cases"></a><span data-ttu-id="1652b-114">了解用例</span><span class="sxs-lookup"><span data-stu-id="1652b-114">Understand your use cases</span></span>

<span data-ttu-id="1652b-115">你可以识别用户问题并确定用户面临的一些常见问题的解答。</span><span class="sxs-lookup"><span data-stu-id="1652b-115">You can recognize user issues and identify the answers to some common problems the users face.</span></span> <span data-ttu-id="1652b-116">通过查找满足用户需求的正确组合，可以生成 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="1652b-116">You can build your Teams app by finding the right combination to meet your user's needs.</span></span> <span data-ttu-id="1652b-117">[了解用例](../concepts/design/understand-use-cases.md) 以了解最终用户如何与你的应用交互。</span><span class="sxs-lookup"><span data-stu-id="1652b-117">[Understand use cases](../concepts/design/understand-use-cases.md) to know how an end-user interacts with your app.</span></span> <span data-ttu-id="1652b-118">了解如何了解用户及其问题。</span><span class="sxs-lookup"><span data-stu-id="1652b-118">You learn to understand the user and their problem.</span></span> <span data-ttu-id="1652b-119">回答的一些常见问题如下所示：</span><span class="sxs-lookup"><span data-stu-id="1652b-119">Some common questions answered are as follows:</span></span>

* <span data-ttu-id="1652b-120">是否需要身份验证？</span><span class="sxs-lookup"><span data-stu-id="1652b-120">Do you need authentication?</span></span>
* <span data-ttu-id="1652b-121">你的应用要解决什么问题？</span><span class="sxs-lookup"><span data-stu-id="1652b-121">What problem is your app going to solve?</span></span>
* <span data-ttu-id="1652b-122">应用程序的最终用户是谁？</span><span class="sxs-lookup"><span data-stu-id="1652b-122">Who are the end-users of the app?</span></span>
* <span data-ttu-id="1652b-123">载入体验应该如何以及应用还可以执行哪些操作？</span><span class="sxs-lookup"><span data-stu-id="1652b-123">How should the onboarding experience be and what else the app can do?</span></span>

## <a name="map-your-use-cases-to-teams-app-capabilities"></a><span data-ttu-id="1652b-124">将用例映射到 Teams 应用功能</span><span class="sxs-lookup"><span data-stu-id="1652b-124">Map your use cases to Teams app capabilities</span></span>

<span data-ttu-id="1652b-125">[映射用例涵盖了](../concepts/design/map-use-cases.md) 一些常见方案以及如何选择应用的功能。</span><span class="sxs-lookup"><span data-stu-id="1652b-125">[Map your use cases](../concepts/design/map-use-cases.md) covers some common scenarios and how to choose your app's capabilities.</span></span> <span data-ttu-id="1652b-126">提供了在外部系统中共享应用和协作处理项目的信息。</span><span class="sxs-lookup"><span data-stu-id="1652b-126">Information to share your app and collaborate on items in an external system is provided.</span></span> <span data-ttu-id="1652b-127">您还可以了解如何启动工作流和向用户发送通知。</span><span class="sxs-lookup"><span data-stu-id="1652b-127">You can also learn how to initiate workflows and send notifications to users.</span></span> <span data-ttu-id="1652b-128">获取有关开始位置、如何与用户社交、对话机器人以及组合多个功能的其他提示。</span><span class="sxs-lookup"><span data-stu-id="1652b-128">Get additional tips on where to start, how to get social with users, conversational bots, and combining multiple features.</span></span>

## <a name="see-also"></a><span data-ttu-id="1652b-129">另请参阅</span><span class="sxs-lookup"><span data-stu-id="1652b-129">See also</span></span>

- [<span data-ttu-id="1652b-130">将 Web 应用与 Teams 集成</span><span class="sxs-lookup"><span data-stu-id="1652b-130">Integrate web apps with Teams</span></span>](../samples/integrating-web-apps.md)

- [<span data-ttu-id="1652b-131">生成首个 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="1652b-131">Build your first Microsoft Teams app</span></span>](../build-your-first-app/build-first-app-overview.md)

## <a name="next-step"></a><span data-ttu-id="1652b-132">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1652b-132">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1652b-133">了解 Teams 应用功能</span><span class="sxs-lookup"><span data-stu-id="1652b-133">Understand Teams app capabilities</span></span>](capabilities-overview.md)

