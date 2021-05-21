---
title: 生成适用于 Microsoft Teams 平台的应用
author: heath-hamilton
description: 大致了解开发人员如何使用自定义Microsoft Teams扩展自定义功能。
ms.topic: overview
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 8724b669476b11aa8cb1aca6d9586fc7ea42587d
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566507"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="d72b3-103">构建 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="d72b3-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="d72b3-104">Microsoft Teams应用将关键信息、常用工具和受信任流程引入人们越来越集中、学习和工作的地方。</span><span class="sxs-lookup"><span data-stu-id="d72b3-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="d72b3-105">应用是扩展Teams以满足你的需求。</span><span class="sxs-lookup"><span data-stu-id="d72b3-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="d72b3-106">为现有应用创建全新的Teams或集成现有应用。</span><span class="sxs-lookup"><span data-stu-id="d72b3-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d72b3-107">从这里开始</span><span class="sxs-lookup"><span data-stu-id="d72b3-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="d72b3-108">什么是Teams应用？</span><span class="sxs-lookup"><span data-stu-id="d72b3-108">What are Teams apps?</span></span>

<span data-ttu-id="d72b3-109">Teams应用是功能和[入口点](concepts/capabilities-overview.md)[的组合](concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="d72b3-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="d72b3-110">例如，用户可以与你的应用的聊天机器人功能 (在) 入口点 (聊天) 。 </span><span class="sxs-lookup"><span data-stu-id="d72b3-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="d72b3-111">某些应用使用简单的 (发送) ，而其他应用则复杂 (患者记录) 。</span><span class="sxs-lookup"><span data-stu-id="d72b3-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="d72b3-112">规划应用时，请记住Teams协作中心。</span><span class="sxs-lookup"><span data-stu-id="d72b3-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="d72b3-113">应用的最佳Teams有助于用户表达自己，并更好地协同工作。</span><span class="sxs-lookup"><span data-stu-id="d72b3-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="d72b3-114">选项卡</span><span class="sxs-lookup"><span data-stu-id="d72b3-114">Tabs</span></span>

<span data-ttu-id="d72b3-115">**更方便地获取信息**：有时你只需使内容更易于查找。</span><span class="sxs-lookup"><span data-stu-id="d72b3-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="d72b3-116">在选项卡中[显示一个重要的](tabs/what-are-tabs.md)网页，它为网站中的静态和动态内容提供Teams。</span><span class="sxs-lookup"><span data-stu-id="d72b3-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="选项卡在客户端中的外观的概念Teams表示。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="d72b3-118">机器人</span><span class="sxs-lookup"><span data-stu-id="d72b3-118">Bots</span></span>

<span data-ttu-id="d72b3-119">**将字词转换为操作**：对话通常导致需要执行某些操作 (生成订单、查看代码、检查票证状态等) 。</span><span class="sxs-lookup"><span data-stu-id="d72b3-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, and so on).</span></span> <span data-ttu-id="d72b3-120">机器人[可以在](bots/what-are-bots.md)内部启动这些类型的Teams。</span><span class="sxs-lookup"><span data-stu-id="d72b3-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="自动程序在客户端中的外观的概念Teams表示。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="d72b3-122">消息扩展</span><span class="sxs-lookup"><span data-stu-id="d72b3-122">Messaging extensions</span></span>

<span data-ttu-id="d72b3-123">**使多任务更容易**[：使用消息传递](messaging-extensions/what-are-messaging-extensions.md)扩展，可以在对话中快速共享外部信息。</span><span class="sxs-lookup"><span data-stu-id="d72b3-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="d72b3-124">还可以对消息采取行动，例如根据频道帖子的内容创建帮助票证。</span><span class="sxs-lookup"><span data-stu-id="d72b3-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="在概念上表示邮件扩展在 Teams 中的外观。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="d72b3-126">Webhook</span><span class="sxs-lookup"><span data-stu-id="d72b3-126">Webhooks</span></span>

<span data-ttu-id="d72b3-127">**与外部应用通信**[：传入 Webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks)是一种将通知从另一个应用自动发送到 Teams 通道的简单方法。</span><span class="sxs-lookup"><span data-stu-id="d72b3-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="d72b3-128">使用 [传出 webhook，](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)使用 @mention 发送 web 服务。</span><span class="sxs-lookup"><span data-stu-id="d72b3-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="连接器在客户端中的外观的概念Teams表示。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="d72b3-130">Microsoft Graph for Teams</span><span class="sxs-lookup"><span data-stu-id="d72b3-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="d72b3-131">**利用Teams** [：Microsoft Graph API for Teams](/graph/teams-concept-overview)提供对团队、频道、用户和消息的访问权限，这些信息可帮助你创建或增强应用的功能。</span><span class="sxs-lookup"><span data-stu-id="d72b3-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="Microsoft Graph API Teams。" border="false":::

   :::column-end:::

   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="d72b3-133">开始构建</span><span class="sxs-lookup"><span data-stu-id="d72b3-133">Start building</span></span>

<span data-ttu-id="d72b3-134">通过设置环境和创建简单的Teams快速熟悉构建环境。</span><span class="sxs-lookup"><span data-stu-id="d72b3-134">Quickly familiarize yourself with building for Teams by setting up your environment and creating a simple app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d72b3-135">构建首个应用</span><span class="sxs-lookup"><span data-stu-id="d72b3-135">Build your first app</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="d72b3-136">与Teams整合</span><span class="sxs-lookup"><span data-stu-id="d72b3-136">Integrate with Teams</span></span>

<span data-ttu-id="d72b3-137">将用户喜欢的现有 Web 应用、服务或系统的功能与 Teams。</span><span class="sxs-lookup"><span data-stu-id="d72b3-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d72b3-138">集成现有应用</span><span class="sxs-lookup"><span data-stu-id="d72b3-138">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="d72b3-139">一个小代码会大有作为</span><span class="sxs-lookup"><span data-stu-id="d72b3-139">A little code goes a long way</span></span>

<span data-ttu-id="d72b3-140">你无需成为专家程序员来构建出色的Teams应用。</span><span class="sxs-lookup"><span data-stu-id="d72b3-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="d72b3-141">请尝试几种低代码解决方案之一。</span><span class="sxs-lookup"><span data-stu-id="d72b3-141">Try one of the several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d72b3-142">创建低代码应用</span><span class="sxs-lookup"><span data-stu-id="d72b3-142">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a><span data-ttu-id="d72b3-143">获取应用灵感</span><span class="sxs-lookup"><span data-stu-id="d72b3-143">Get ideas for your app</span></span>

<span data-ttu-id="d72b3-144">寻找应用开发灵感？</span><span class="sxs-lookup"><span data-stu-id="d72b3-144">Looking for app development inspiration?</span></span> <span data-ttu-id="d72b3-145">浏览我们具有高保真概念的实际方案和行业解决方案列表，了解应用Teams用户的各种方式。</span><span class="sxs-lookup"><span data-stu-id="d72b3-145">Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways Teams apps can help your users.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d72b3-146">请参阅应用方案</span><span class="sxs-lookup"><span data-stu-id="d72b3-146">See app scenarios</span></span>](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="d72b3-147">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d72b3-147">See also</span></span>

* [<span data-ttu-id="d72b3-148">将"共享到Teams"按钮添加到您的网站</span><span class="sxs-lookup"><span data-stu-id="d72b3-148">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="d72b3-149">设计Teams应用</span><span class="sxs-lookup"><span data-stu-id="d72b3-149">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="d72b3-150">Microsoft TeamsJavaScript 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="d72b3-150">Microsoft Teams JavaScript client SDK</span></span>](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="d72b3-151">适用于[JavaScript](https://github.com/Microsoft/botbuilder-js)和[.NET](https://github.com/Microsoft/botbuilder-dotnet/)的 Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="d72b3-151">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="d72b3-152">分发Teams应用</span><span class="sxs-lookup"><span data-stu-id="d72b3-152">Distribute your Teams app</span></span>](concepts/deploy-and-publish/apps-publish-overview.md)
