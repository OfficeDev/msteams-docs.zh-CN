---
title: 为 Microsoft 团队平台生成应用程序
author: heath-hamilton
description: 概述开发人员如何使用自定义应用程序扩展和自定义 Microsoft 团队功能。
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: c430add71e7c23a44a552270c5e3c1bacbe650e4
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "48209791"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="3f5ea-103">为 Microsoft 团队构建应用程序</span><span class="sxs-lookup"><span data-stu-id="3f5ea-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="3f5ea-104">Microsoft 团队应用程序可提供关键信息、常见工具和受信任的过程，以便人们越来越多地收集、学习和工作。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="3f5ea-105">应用程序是您扩展团队以满足您的需求的方式。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="3f5ea-106">创建适用于团队的全新功能或集成现有应用程序。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-106">Create something brand new for Teams or integrate an existing app.</span></span>

## <a name="what-are-teams-apps"></a><span data-ttu-id="3f5ea-107">什么是团队应用？</span><span class="sxs-lookup"><span data-stu-id="3f5ea-107">What are Teams apps?</span></span>

<span data-ttu-id="3f5ea-108">团队应用程序是 [功能](concepts/capabilities-overview.md) 和 [入口点](concepts/extensibility-points.md)的组合。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-108">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="3f5ea-109">例如，用户可以与您的应用程序的 *bot* 聊天 (功能) 在 *频道* (入口点) 中。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-109">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="3f5ea-110">有些应用程序很简单 (发送通知) ，而其他应用则 (管理患者记录) 的复杂。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-110">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="3f5ea-111">在规划您的应用程序时，请记住，团队是协作中心。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-111">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="3f5ea-112">最佳团队应用可帮助人们自己表达自己并更好地协同工作。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-112">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="3f5ea-113">选项卡</span><span class="sxs-lookup"><span data-stu-id="3f5ea-113">Tabs</span></span>

<span data-ttu-id="3f5ea-114">**更方便地获取信息**：有时只需更轻松地找到一些内容。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-114">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="3f5ea-115">在 [选项卡](tabs/what-are-tabs.md)中显示一个重要的网页，该网页为工作组中的静态和动态内容提供了全屏 web 体验。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-115">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="选项卡在团队客户端中的外观的概念性表示。" border="false":::

   :::column-end:::
   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="3f5ea-117">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="3f5ea-117">Messaging extensions</span></span>

<span data-ttu-id="3f5ea-118">**更轻松**地执行多项工作：使用 [邮件扩展](messaging-extensions/what-are-messaging-extensions.md)，可以在对话中快速共享外部信息。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-118">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="3f5ea-119">您还可以对邮件执行操作，例如根据频道帖子的内容创建帮助票证。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-119">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="邮件扩展在团队客户端中的显示方式的概念性表示。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="bots"></a><span data-ttu-id="3f5ea-121">机器人</span><span class="sxs-lookup"><span data-stu-id="3f5ea-121">Bots</span></span>

<span data-ttu-id="3f5ea-122">将**单词转换为操作**：对话通常会导致需要执行某些操作， (生成订单、查看我的代码、检查票证状态等 ) 。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-122">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="3f5ea-123">[机器人](bots/what-are-bots.md)可以直接在团队内部启动这些类型的工作流。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-123">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="团队客户端中的 bot 外观的概念性表示。" border="false":::

   :::column-end:::
   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="3f5ea-125">Webhook</span><span class="sxs-lookup"><span data-stu-id="3f5ea-125">Webhooks</span></span>

<span data-ttu-id="3f5ea-126">**与外部应用程序通信**： [传入 webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) 是一种将通知从另一个应用程序自动发送到团队频道的简单方法。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-126">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="3f5ea-127">使用 [传出的 webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)，将 @mention 的 web 服务进行消息处理。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-127">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="团队客户端中的连接器外观的概念性表示。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="3f5ea-129">适用于团队的 Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="3f5ea-129">Microsoft Graph for Teams</span></span>

<span data-ttu-id="3f5ea-130">**利用团队数据**： [适用于团队的 Microsoft Graph API](https://docs.microsoft.com/graph/teams-concept-overview) 提供了有关可帮助您创建或增强应用程序功能的团队、频道、用户和消息的信息的访问。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-130">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="适用于团队的 Microsoft Graph API 的概念性表示。" border="false":::

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="get-started"></a><span data-ttu-id="3f5ea-132">入门</span><span class="sxs-lookup"><span data-stu-id="3f5ea-132">Get started</span></span>

<span data-ttu-id="3f5ea-133">通过我们的第一个应用教程或了解如何集成和导入现有应用，直接参与。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-133">Jump right in with our first app tutorials or find out how to integrate and import existing apps.</span></span>

:::row:::
   :::column span="2":::

### <a name="start-building"></a><span data-ttu-id="3f5ea-134">开始构建</span><span class="sxs-lookup"><span data-stu-id="3f5ea-134">Start building</span></span>

   <span data-ttu-id="3f5ea-135">通过创建一个简单的应用程序并添加一些常用功能，快速熟悉为团队构建。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-135">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="3f5ea-136">立即构建您的第一个应用程序</span><span class="sxs-lookup"><span data-stu-id="3f5ea-136">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="integrate-with-teams"></a><span data-ttu-id="3f5ea-137">与团队集成</span><span class="sxs-lookup"><span data-stu-id="3f5ea-137">Integrate with Teams</span></span>

   <span data-ttu-id="3f5ea-138">将用户喜爱的功能与团队协作功能的现有 web 应用、服务或系统融合。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-138">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="3f5ea-139">集成现有应用程序</span><span class="sxs-lookup"><span data-stu-id="3f5ea-139">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

### <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="3f5ea-140">较小的代码是一段较长的方法</span><span class="sxs-lookup"><span data-stu-id="3f5ea-140">A little code goes a long way</span></span>

   <span data-ttu-id="3f5ea-141">您无需成为专家级程序员即可构建出色的团队应用程序。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-141">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="3f5ea-142">尝试几个低代码解决方案中的一个。</span><span class="sxs-lookup"><span data-stu-id="3f5ea-142">Try one of several low-code solutions.</span></span>

   > [!div class="nextstepaction"]
   > [<span data-ttu-id="3f5ea-143">创建低代码应用程序</span><span class="sxs-lookup"><span data-stu-id="3f5ea-143">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="resources"></a><span data-ttu-id="3f5ea-144">资源</span><span class="sxs-lookup"><span data-stu-id="3f5ea-144">Resources</span></span>

* [<span data-ttu-id="3f5ea-145">向您的网站添加 "共享到团队" 按钮</span><span class="sxs-lookup"><span data-stu-id="3f5ea-145">Add a Share to Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="3f5ea-146">熟知设计系统</span><span class="sxs-lookup"><span data-stu-id="3f5ea-146">Fluent Design System</span></span>](https://fluentsite.z22.web.core.windows.net/)
* [<span data-ttu-id="3f5ea-147">Microsoft 团队 JavaScript 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="3f5ea-147">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="3f5ea-148">用于 .NET 的 JavaScript 和[Bot 框架 sdk](https://github.com/Microsoft/botbuilder-dotnet/)的[bot 框架 sdk](https://github.com/Microsoft/botbuilder-js)</span><span class="sxs-lookup"><span data-stu-id="3f5ea-148">[Bot Framework SDK for JavaScript](https://github.com/Microsoft/botbuilder-js) and [Bot Framework SDK for .NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="3f5ea-149">将应用发布到组织或 AppSource</span><span class="sxs-lookup"><span data-stu-id="3f5ea-149">Publish your app to an organization or AppSource</span></span>](concepts/deploy-and-publish/overview.md)
