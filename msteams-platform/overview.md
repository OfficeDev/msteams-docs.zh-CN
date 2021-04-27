---
title: 构建适用于 Microsoft Teams 平台的应用
author: heath-hamilton
description: 大致了解开发人员如何使用自定义应用扩展 Microsoft Teams 功能。
ms.topic: overview
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 5009427fc3cdde11de45a55cb0f6216ae36b0d66
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019809"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="2d05f-103">构建 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="2d05f-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="2d05f-104">Microsoft Teams 应用将关键信息、常用工具和受信任流程引入人们越来越集中、学习和工作的地方。</span><span class="sxs-lookup"><span data-stu-id="2d05f-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="2d05f-105">应用是扩展 Teams 以满足你的需求。</span><span class="sxs-lookup"><span data-stu-id="2d05f-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="2d05f-106">为 Teams 创建新内容或集成现有应用。</span><span class="sxs-lookup"><span data-stu-id="2d05f-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d05f-107">从这里开始</span><span class="sxs-lookup"><span data-stu-id="2d05f-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="2d05f-108">什么是 Teams 应用？</span><span class="sxs-lookup"><span data-stu-id="2d05f-108">What are Teams apps?</span></span>

<span data-ttu-id="2d05f-109">Teams 应用是功能和[入口点](concepts/capabilities-overview.md)[的组合](concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="2d05f-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="2d05f-110">例如，用户可以与你的应用的聊天机器人功能 (在) 入口点 (聊天) 。 </span><span class="sxs-lookup"><span data-stu-id="2d05f-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="2d05f-111">某些应用使用简单的 (发送) ，而其他应用则复杂 (患者记录) 。</span><span class="sxs-lookup"><span data-stu-id="2d05f-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="2d05f-112">规划应用时，请记住 Teams 是协作中心。</span><span class="sxs-lookup"><span data-stu-id="2d05f-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="2d05f-113">最佳的 Teams 应用可帮助用户表达自己，并更好地协同工作。</span><span class="sxs-lookup"><span data-stu-id="2d05f-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="2d05f-114">选项卡</span><span class="sxs-lookup"><span data-stu-id="2d05f-114">Tabs</span></span>

<span data-ttu-id="2d05f-115">**更方便地获取信息**：有时你只需使内容更易于查找。</span><span class="sxs-lookup"><span data-stu-id="2d05f-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="2d05f-116">在选项卡中 [显示重要网页](tabs/what-are-tabs.md)，为 Teams 中的静态和动态内容提供全屏 Web 体验。</span><span class="sxs-lookup"><span data-stu-id="2d05f-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Teams 客户端中选项卡外观的概念表示形式。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="2d05f-118">机器人</span><span class="sxs-lookup"><span data-stu-id="2d05f-118">Bots</span></span>

<span data-ttu-id="2d05f-119">**将字词转换为操作**：对话通常导致需要执行某些操作 (生成订单、查看代码、检查票证状态等) 。</span><span class="sxs-lookup"><span data-stu-id="2d05f-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, and so on).</span></span> <span data-ttu-id="2d05f-120">机器人 [可以在](bots/what-are-bots.md) Teams 内启动这些类型的工作流。</span><span class="sxs-lookup"><span data-stu-id="2d05f-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Teams 客户端中机器人外观的概念表示形式。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="2d05f-122">消息扩展</span><span class="sxs-lookup"><span data-stu-id="2d05f-122">Messaging extensions</span></span>

<span data-ttu-id="2d05f-123">**使多任务更容易**[：使用消息传递](messaging-extensions/what-are-messaging-extensions.md)扩展，可以在对话中快速共享外部信息。</span><span class="sxs-lookup"><span data-stu-id="2d05f-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="2d05f-124">还可以对消息采取行动，例如根据频道帖子的内容创建帮助票证。</span><span class="sxs-lookup"><span data-stu-id="2d05f-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="概念性表示在 Teams 客户端中邮件扩展的外观。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="2d05f-126">Webhook</span><span class="sxs-lookup"><span data-stu-id="2d05f-126">Webhooks</span></span>

<span data-ttu-id="2d05f-127">**与外部应用通信**[：传入 Webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks)是一种将通知从另一个应用自动发送到 Teams 频道的简单方法。</span><span class="sxs-lookup"><span data-stu-id="2d05f-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="2d05f-128">使用 [传出 webhook，](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)使用 @mention 发送 web 服务。</span><span class="sxs-lookup"><span data-stu-id="2d05f-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="在概念上表示 Teams 客户端中的连接器外观。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::

   :::column span="":::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="2d05f-130">适用于 Teams 的 Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="2d05f-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="2d05f-131">**利用 Teams 数据**：适用于 Teams 的 [Microsoft Graph API](https://docs.microsoft.com/graph/teams-concept-overview) 提供对团队、频道、用户和消息的访问权限，这些信息可帮助你创建或增强应用的功能。</span><span class="sxs-lookup"><span data-stu-id="2d05f-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="适用于 Teams 的 Microsoft Graph API 的概念表示形式。" border="false":::

   :::column-end:::

   :::column span="":::
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="2d05f-133">开始构建</span><span class="sxs-lookup"><span data-stu-id="2d05f-133">Start building</span></span>

<span data-ttu-id="2d05f-134">通过设置环境和创建简单的应用，快速熟悉 Teams 构建。</span><span class="sxs-lookup"><span data-stu-id="2d05f-134">Quickly familiarize yourself with building for Teams by setting up your environment and creating a simple app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d05f-135">构建首个应用</span><span class="sxs-lookup"><span data-stu-id="2d05f-135">Build your first app</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="2d05f-136">与Teams整合</span><span class="sxs-lookup"><span data-stu-id="2d05f-136">Integrate with Teams</span></span>

<span data-ttu-id="2d05f-137">将用户喜欢的现有 Web 应用、服务或系统的功能与 Teams 的协作功能融合在一起。</span><span class="sxs-lookup"><span data-stu-id="2d05f-137">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d05f-138">集成现有应用</span><span class="sxs-lookup"><span data-stu-id="2d05f-138">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="2d05f-139">一个小代码会大有作为</span><span class="sxs-lookup"><span data-stu-id="2d05f-139">A little code goes a long way</span></span>

<span data-ttu-id="2d05f-140">你无需成为专家程序员来构建出色的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="2d05f-140">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="2d05f-141">请尝试多个低代码解决方案之一。</span><span class="sxs-lookup"><span data-stu-id="2d05f-141">Try one of several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d05f-142">创建低代码应用</span><span class="sxs-lookup"><span data-stu-id="2d05f-142">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a><span data-ttu-id="2d05f-143">获取应用灵感</span><span class="sxs-lookup"><span data-stu-id="2d05f-143">Get ideas for your app</span></span>

<span data-ttu-id="2d05f-144">寻找应用开发灵感？</span><span class="sxs-lookup"><span data-stu-id="2d05f-144">Looking for app development inspiration?</span></span> <span data-ttu-id="2d05f-145">浏览我们具有高保真概念的实际方案和行业解决方案列表，以了解 Teams 应用可以为用户提供帮助的各种方式。</span><span class="sxs-lookup"><span data-stu-id="2d05f-145">Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways Teams apps can help your users.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="2d05f-146">请参阅应用方案</span><span class="sxs-lookup"><span data-stu-id="2d05f-146">See app scenarios</span></span>](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="2d05f-147">另请参阅</span><span class="sxs-lookup"><span data-stu-id="2d05f-147">See also</span></span>

* [<span data-ttu-id="2d05f-148">将"共享到 Teams"按钮添加到网站</span><span class="sxs-lookup"><span data-stu-id="2d05f-148">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="2d05f-149">设计 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="2d05f-149">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="2d05f-150">Microsoft Teams JavaScript 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="2d05f-150">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="2d05f-151">适用于[JavaScript](https://github.com/Microsoft/botbuilder-js)和[.NET](https://github.com/Microsoft/botbuilder-dotnet/)的 Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="2d05f-151">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="2d05f-152">发布 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="2d05f-152">Publish your Teams app</span></span>](concepts/deploy-and-publish/overview.md)
