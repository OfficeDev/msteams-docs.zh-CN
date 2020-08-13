---
title: 团队开发人员平台
author: clearab
description: 概述开发人员如何使用团队平台扩展和自定义 Microsoft 团队功能。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: d127acb33212f23dff9cf0dd83a1936044c10d5e
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651875"
---
# <a name="building-for-microsoft-teams"></a><span data-ttu-id="cabcc-103">为 Microsoft 团队构建</span><span class="sxs-lookup"><span data-stu-id="cabcc-103">Building for Microsoft Teams</span></span>

<span data-ttu-id="cabcc-104">Microsoft 团队应用程序可提供关键信息、常见工具和受信任的过程，以便人们越来越多地收集、学习和工作。</span><span class="sxs-lookup"><span data-stu-id="cabcc-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="cabcc-105">应用程序是您扩展团队以满足您的需求的方式。</span><span class="sxs-lookup"><span data-stu-id="cabcc-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="cabcc-106">您可以为团队创建全新的品牌，或者只是在收藏的应用和服务中集成功能。</span><span class="sxs-lookup"><span data-stu-id="cabcc-106">You can create something brand new for Teams or simply integrate features in your favorite apps and services.</span></span>

## <a name="what-can-teams-apps-do"></a><span data-ttu-id="cabcc-107">团队应用程序可以做什么？</span><span class="sxs-lookup"><span data-stu-id="cabcc-107">What can Teams apps do?</span></span>

<span data-ttu-id="cabcc-108">人员通过一组平台[功能](capabilities-overview.md)发现和使用团队应用。</span><span class="sxs-lookup"><span data-stu-id="cabcc-108">People discover and use Teams apps through a set of platform [capabilities](capabilities-overview.md).</span></span>

<span data-ttu-id="cabcc-109">有些应用程序很简单 (发送通知) ，其他应用程序 (查看患者记录) 的复杂。</span><span class="sxs-lookup"><span data-stu-id="cabcc-109">Some apps are simple (send notifications), while others are complex (view patient records).</span></span> <span data-ttu-id="cabcc-110">在规划您的应用程序时，请记住，团队是协作中心。</span><span class="sxs-lookup"><span data-stu-id="cabcc-110">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="cabcc-111">最佳团队应用可帮助人们自己表达自己并更好地协同工作。</span><span class="sxs-lookup"><span data-stu-id="cabcc-111">The best Teams apps help people express themselves and work better together.</span></span>

### <a name="get-information-more-conveniently"></a><span data-ttu-id="cabcc-112">更方便地获取信息</span><span class="sxs-lookup"><span data-stu-id="cabcc-112">Get information more conveniently</span></span>

<span data-ttu-id="cabcc-113">有时，您只需更轻松地查找内容。</span><span class="sxs-lookup"><span data-stu-id="cabcc-113">Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="cabcc-114">在[选项卡](doc-links/what-are-tabs.md)中显示一个重要的网页，该网页为工作组中的静态和动态内容提供了全屏 web 体验。</span><span class="sxs-lookup"><span data-stu-id="cabcc-114">Display an important webpage in a [tab](doc-links/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

![选项卡在团队客户端中的外观的概念性表示。](doc-links/images/overview-tabs.png)

### <a name="share-links-without-switching-context"></a><span data-ttu-id="cabcc-116">在不切换上下文的情况下共享链接</span><span class="sxs-lookup"><span data-stu-id="cabcc-116">Share links without switching context</span></span>

<span data-ttu-id="cabcc-117">将信息提取到对话中，永远不会离开团队。</span><span class="sxs-lookup"><span data-stu-id="cabcc-117">Pull information into a conversation and never leave Teams.</span></span> <span data-ttu-id="cabcc-118">例如，通过邮件[扩展](doc-links/what-are-messaging-extensions.md)，您可以使用邮件撰写框，通过外部系统共享丰富的、易于 digestible 的内容。</span><span class="sxs-lookup"><span data-stu-id="cabcc-118">For example, with [messaging extensions](doc-links/what-are-messaging-extensions.md) you can share rich, easily digestible content from an external system using the message compose box.</span></span>

![邮件扩展在团队客户端中的显示方式的概念性表示](doc-links\images\overview-messaging.png)

### <a name="turn-words-into-actions"></a><span data-ttu-id="cabcc-120">将词语转换为操作</span><span class="sxs-lookup"><span data-stu-id="cabcc-120">Turn words into actions</span></span>

<span data-ttu-id="cabcc-121">对话通常会导致需要执行某些操作 (创建订单、查看我的代码等 ) 。</span><span class="sxs-lookup"><span data-stu-id="cabcc-121">Conversations often result in the need to do something (create an order, review my code, etc.).</span></span> <span data-ttu-id="cabcc-122">[机器人](doc-links/what-are-bots.md)可以直接在团队内部启动这些类型的工作流。</span><span class="sxs-lookup"><span data-stu-id="cabcc-122">A [bot](doc-links/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

![团队客户端中的 bot 外观的概念性表示](doc-links/images/overview-bots.png)

### <a name="communicate-with-external-apps-and-services"></a><span data-ttu-id="cabcc-124">与外部应用程序和服务进行通信</span><span class="sxs-lookup"><span data-stu-id="cabcc-124">Communicate with external apps and services</span></span>

<span data-ttu-id="cabcc-125">[传入 webhook](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks)是一种将来自其他应用程序的通知自动发送到团队频道或聊天的简单方法。</span><span class="sxs-lookup"><span data-stu-id="cabcc-125">[Incoming webhooks](doc-links/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send alerts from another app to a Teams channel or chat.</span></span> <span data-ttu-id="cabcc-126">通过[传出的 webhook](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks)，您可以使用 @mention 向 web 服务发送邮件。</span><span class="sxs-lookup"><span data-stu-id="cabcc-126">With [outgoing webhooks](doc-links/what-are-webhooks-and-connectors.md#outgoing-webhooks), you can send a message to your web service with an @mention.</span></span>

![团队客户端中的连接器外观的概念性表示。](doc-links/images/overview-connectors.png)

### <a name="utilize-teams-data"></a><span data-ttu-id="cabcc-128">利用团队数据</span><span class="sxs-lookup"><span data-stu-id="cabcc-128">Utilize Teams data</span></span>

<span data-ttu-id="cabcc-129">[适用于团队的 Microsoft GRAPH REST API](https://docs.microsoft.com/graph/teams-concept-overview)提供了有关可帮助您创建或增强应用程序功能的团队、频道、用户和消息的信息的访问权限。</span><span class="sxs-lookup"><span data-stu-id="cabcc-129">The [Microsoft Graph REST API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

!["适用于团队的 Microsoft Graph REST API 的概念性表示](doc-links/images/overview-graph.png)
  
## <a name="start-building"></a><span data-ttu-id="cabcc-131">开始构建</span><span class="sxs-lookup"><span data-stu-id="cabcc-131">Start building</span></span>

   <span data-ttu-id="cabcc-132">通过创建一个简单的应用程序并添加一些常用功能，快速熟悉为团队构建。</span><span class="sxs-lookup"><span data-stu-id="cabcc-132">Quickly familiarize yourself with building for Teams by creating a simple app and adding a couple commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="cabcc-133">立即构建您的第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="cabcc-133">Build your first app now</span></span>](build-your-first-app/build-real-world-app.md)

### <a name="bring-it-all-together"></a><span data-ttu-id="cabcc-134">将所有组合在一起</span><span class="sxs-lookup"><span data-stu-id="cabcc-134">Bring it all together</span></span>

   <span data-ttu-id="cabcc-135">通过将组织最喜爱的 web 应用程序、服务和系统与团队协作功能混合在一起，简化用户的流程和工作流。</span><span class="sxs-lookup"><span data-stu-id="cabcc-135">Simplify processes and workflows for users by blending your organization's favorite web apps, services, and systems with Teams collaborative features.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="cabcc-136">集成现有应用程序</span><span class="sxs-lookup"><span data-stu-id="cabcc-136">Integrate an existing app</span></span>](doc-links/integrating-web-apps.md)

### <a name="trust-the-process"></a><span data-ttu-id="cabcc-137">信任流程</span><span class="sxs-lookup"><span data-stu-id="cabcc-137">Trust the process</span></span>

   <span data-ttu-id="cabcc-138">了解整个团队平台开发过程，以便有效地为您的组织或任何人规划、设计、构建和发布应用程序。</span><span class="sxs-lookup"><span data-stu-id="cabcc-138">Understand the entire Teams platform development process to effectively plan, design, build, and publish an app for your organization or anyone.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="cabcc-139">开始规划您的应用程序</span><span class="sxs-lookup"><span data-stu-id="cabcc-139">Start planning your app</span></span>](doc-links/extensibility-points.md)

### <a name="no-code-no-worries"></a><span data-ttu-id="cabcc-140">无代码，无照管</span><span class="sxs-lookup"><span data-stu-id="cabcc-140">No code, no worries</span></span>

   <span data-ttu-id="cabcc-141">您无需成为程序员即可构建出色的应用程序。</span><span class="sxs-lookup"><span data-stu-id="cabcc-141">You don't need to be a programmer to build a great app.</span></span> <span data-ttu-id="cabcc-142">使用 Microsoft Power Platform 创建一个几乎不包含任何代码的团队应用程序。</span><span class="sxs-lookup"><span data-stu-id="cabcc-142">Create a Teams app with little to no code using the Microsoft Power Platform.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="cabcc-143">导入 Power Platform 应用</span><span class="sxs-lookup"><span data-stu-id="cabcc-143">Import a Power Platform app</span></span>](doc-links/importing-custom-microsoft-apps.md)

## <a name="resources"></a><span data-ttu-id="cabcc-144">资源</span><span class="sxs-lookup"><span data-stu-id="cabcc-144">Resources</span></span>

* [<span data-ttu-id="cabcc-145">向您的网站添加 "共享到团队" 按钮</span><span class="sxs-lookup"><span data-stu-id="cabcc-145">Add a Share to Teams button to your website</span></span>](doc-links/share-to-teams.md)
* [<span data-ttu-id="cabcc-146">使用推荐指南设计你的应用</span><span class="sxs-lookup"><span data-stu-id="cabcc-146">Design your app using recommended guidelines</span></span>](doc-links/designing-overview.md)
* [<span data-ttu-id="cabcc-147">熟知的 UI 设计系统</span><span class="sxs-lookup"><span data-stu-id="cabcc-147">Fluent UI Design System</span></span>](https://fluentsite.z22.web.core.windows.net/)
* [<span data-ttu-id="cabcc-148">Microsoft 团队 JavaScript 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="cabcc-148">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest)
* <span data-ttu-id="cabcc-149">用于 .NET 的 JavaScript 和[Bot 框架 sdk](https://github.com/Microsoft/botbuilder-dotnet/)的[bot 框架 sdk](https://github.com/Microsoft/botbuilder-js)</span><span class="sxs-lookup"><span data-stu-id="cabcc-149">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
