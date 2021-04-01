---
title: 构建适用于 Microsoft Teams 平台的应用
author: heath-hamilton
description: 大致了解开发人员如何使用自定义应用扩展 Microsoft Teams 功能。
ms.topic: overview
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: e40d2b0d8b0d12e6275b97f79d103310d22f9720
ms.sourcegitcommit: 3bd2627b7a334568f61ccc606395e3d89aa521d9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "51475926"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="41f66-103">构建 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="41f66-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="41f66-104">Microsoft Teams 应用将关键信息、常用工具和受信任流程引入人们越来越集中、学习和工作的地方。</span><span class="sxs-lookup"><span data-stu-id="41f66-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="41f66-105">应用是扩展 Teams 以满足你的需求。</span><span class="sxs-lookup"><span data-stu-id="41f66-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="41f66-106">为 Teams 创建新内容或集成现有应用。</span><span class="sxs-lookup"><span data-stu-id="41f66-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="41f66-107">从这里开始</span><span class="sxs-lookup"><span data-stu-id="41f66-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="41f66-108">什么是 Teams 应用？</span><span class="sxs-lookup"><span data-stu-id="41f66-108">What are Teams apps?</span></span>

<span data-ttu-id="41f66-109">Teams 应用是功能和[入口点](concepts/capabilities-overview.md)[的组合](concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="41f66-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md) and [entry points](concepts/extensibility-points.md).</span></span> <span data-ttu-id="41f66-110">例如，用户可以与你的应用的聊天机器人功能 (在) 入口点 (聊天) 。 </span><span class="sxs-lookup"><span data-stu-id="41f66-110">For example, people can chat with your app's *bot* (capability) in a *channel* (entry point).</span></span>

<span data-ttu-id="41f66-111">某些应用使用简单的 (发送) ，而其他应用则复杂 (患者记录) 。</span><span class="sxs-lookup"><span data-stu-id="41f66-111">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="41f66-112">规划应用时，请记住 Teams 是协作中心。</span><span class="sxs-lookup"><span data-stu-id="41f66-112">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="41f66-113">最佳的 Teams 应用可帮助用户表达自己，并更好地协同工作。</span><span class="sxs-lookup"><span data-stu-id="41f66-113">The best Teams apps help people express themselves and work better together.</span></span>

:::row:::
   :::column span="":::

### <a name="tabs"></a><span data-ttu-id="41f66-114">选项卡</span><span class="sxs-lookup"><span data-stu-id="41f66-114">Tabs</span></span>

<span data-ttu-id="41f66-115">**更方便地获取信息**：有时你只需使内容更易于查找。</span><span class="sxs-lookup"><span data-stu-id="41f66-115">**Get information more conveniently**: Sometimes you just need to make things easier to find.</span></span> <span data-ttu-id="41f66-116">在选项卡中 [显示重要网页](tabs/what-are-tabs.md)，为 Teams 中的静态和动态内容提供全屏 Web 体验。</span><span class="sxs-lookup"><span data-stu-id="41f66-116">Display an important webpage in a [tab](tabs/what-are-tabs.md), which provides a full-screen web experience for static and dynamic content in Teams.</span></span>

:::image type="content" source="assets/images/overview-tabs.png" alt-text="Teams 客户端中选项卡外观的概念表示形式。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="bots"></a><span data-ttu-id="41f66-118">机器人</span><span class="sxs-lookup"><span data-stu-id="41f66-118">Bots</span></span>

<span data-ttu-id="41f66-119">**将字词转换为操作**：对话通常导致需要执行某些操作 (生成订单、查看代码、检查票证状态等) 。</span><span class="sxs-lookup"><span data-stu-id="41f66-119">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, etc.).</span></span> <span data-ttu-id="41f66-120">机器人 [可以在](bots/what-are-bots.md) Teams 内启动这些类型的工作流。</span><span class="sxs-lookup"><span data-stu-id="41f66-120">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

:::image type="content" source="assets/images/overview-bots.png" alt-text="Teams 客户端中机器人外观的概念表示形式。" border="false":::

   :::column-end:::

:::row-end:::

:::row:::

   :::column span="":::

### <a name="messaging-extensions"></a><span data-ttu-id="41f66-122">消息扩展</span><span class="sxs-lookup"><span data-stu-id="41f66-122">Messaging extensions</span></span>

<span data-ttu-id="41f66-123">**使多任务更容易**[：使用消息传递](messaging-extensions/what-are-messaging-extensions.md)扩展，可以在对话中快速共享外部信息。</span><span class="sxs-lookup"><span data-stu-id="41f66-123">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="41f66-124">还可以对消息采取行动，例如根据频道帖子的内容创建帮助票证。</span><span class="sxs-lookup"><span data-stu-id="41f66-124">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

:::image type="content" source="assets\images\overview-messaging.png" alt-text="概念性表示在 Teams 客户端中邮件扩展的外观。" border="false":::

   :::column-end:::

   :::column span="":::

### <a name="webhooks"></a><span data-ttu-id="41f66-126">Webhook</span><span class="sxs-lookup"><span data-stu-id="41f66-126">Webhooks</span></span>

<span data-ttu-id="41f66-127">**与外部应用通信**[：传入 Webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks)是一种将通知从另一个应用自动发送到 Teams 频道的简单方法。</span><span class="sxs-lookup"><span data-stu-id="41f66-127">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="41f66-128">使用 [传出 webhook，](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)使用 @mention 发送 web 服务。</span><span class="sxs-lookup"><span data-stu-id="41f66-128">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

:::image type="content" source="assets/images/overview-connectors.png" alt-text="在概念上表示 Teams 客户端中的连接器外观。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="41f66-130">适用于 Teams 的 Microsoft Graph</span><span class="sxs-lookup"><span data-stu-id="41f66-130">Microsoft Graph for Teams</span></span>

<span data-ttu-id="41f66-131">**利用 Teams 数据**：适用于 Teams 的 [Microsoft Graph API](https://docs.microsoft.com/graph/teams-concept-overview) 提供对团队、频道、用户和消息的访问权限，这些信息可帮助你创建或增强应用的功能。</span><span class="sxs-lookup"><span data-stu-id="41f66-131">**Utilize Teams data**: The [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app.</span></span>

:::image type="content" source="assets/images/overview-graph.png" alt-text="适用于 Teams 的 Microsoft Graph API 的概念表示形式。" border="false":::

   :::column-end:::
   :::column span="":::

:::row:::
   :::column span="2":::
   :::column-end:::
:::row-end:::

## <a name="build-solutions-for-microsoft-teams-apps"></a><span data-ttu-id="41f66-133">为 Microsoft Teams 应用生成解决方案</span><span class="sxs-lookup"><span data-stu-id="41f66-133">Build solutions for Microsoft Teams apps</span></span>
 
<span data-ttu-id="41f66-134">Microsoft 提供了一本可扩展性外观书籍，这是一个按行业组织的 Teams 应用的方案库。</span><span class="sxs-lookup"><span data-stu-id="41f66-134">Microsoft offers an extensibility look book, a scenario library for Teams apps organized by industry.</span></span> <span data-ttu-id="41f66-135">本书帮助你在 Teams 平台上生成应用，并了解使用各种 Teams 平台功能的不同可能方案。</span><span class="sxs-lookup"><span data-stu-id="41f66-135">This book helps you build apps on the Teams platform and understand different possible scenarios using various Teams platform capabilities.</span></span> <span data-ttu-id="41f66-136">通讯簿方案从业务问题、所涉及的角色及其挑战开始，以满足业务需求的 Teams 应用解决方案结束。</span><span class="sxs-lookup"><span data-stu-id="41f66-136">The look book scenarios start with a business problem, the personas involved along with their challenges, and end with a Teams app solution addressing the business needs.</span></span>

<span data-ttu-id="41f66-137">此库的每个方案都附带一组高保真设计概念模型，这些模型可作为设计应用和增强用户体验的灵感。</span><span class="sxs-lookup"><span data-stu-id="41f66-137">Each scenario in this library is accompanied by a set of high-fidelity design concept mocks, which can serve as an inspiration for designing your apps and enhancing user experience.</span></span> <span data-ttu-id="41f66-138">此外，该书重点介绍了构建每个应用时遵循的设计和体系结构最佳做法。</span><span class="sxs-lookup"><span data-stu-id="41f66-138">In addition, the look book highlights the design and architecture best practices followed in building each app.</span></span> <span data-ttu-id="41f66-139">有关详细信息，请参阅可扩展性外观书籍。</span><span class="sxs-lookup"><span data-stu-id="41f66-139">For more information, see the extensibility look book.</span></span> <span data-ttu-id="41f66-140">有关详细信息，请参阅 [扩展性外观书籍](https://adoption.microsoft.com/extensibility-look-book/scenarios/)。</span><span class="sxs-lookup"><span data-stu-id="41f66-140">For more information, see [extensibility look book](https://adoption.microsoft.com/extensibility-look-book/scenarios/).</span></span> 

## <a name="start-building"></a><span data-ttu-id="41f66-141">开始构建</span><span class="sxs-lookup"><span data-stu-id="41f66-141">Start building</span></span>

<span data-ttu-id="41f66-142">通过创建简单的应用并添加一些常用功能，快速熟悉 Teams 构建。</span><span class="sxs-lookup"><span data-stu-id="41f66-142">Quickly familiarize yourself with building for Teams by creating a simple app and adding some commonly used capabilities.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="41f66-143">现在生成你的第一个应用</span><span class="sxs-lookup"><span data-stu-id="41f66-143">Build your first app now</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="41f66-144">与Teams整合</span><span class="sxs-lookup"><span data-stu-id="41f66-144">Integrate with Teams</span></span>

<span data-ttu-id="41f66-145">将用户喜欢的现有 Web 应用、服务或系统的功能与 Teams 的协作功能融合在一起。</span><span class="sxs-lookup"><span data-stu-id="41f66-145">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="41f66-146">集成现有应用</span><span class="sxs-lookup"><span data-stu-id="41f66-146">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="41f66-147">一个小代码会大有作为</span><span class="sxs-lookup"><span data-stu-id="41f66-147">A little code goes a long way</span></span>

<span data-ttu-id="41f66-148">你无需成为专家程序员来构建出色的 Teams 应用。</span><span class="sxs-lookup"><span data-stu-id="41f66-148">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="41f66-149">请尝试多个低代码解决方案之一。</span><span class="sxs-lookup"><span data-stu-id="41f66-149">Try one of several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="41f66-150">创建低代码应用</span><span class="sxs-lookup"><span data-stu-id="41f66-150">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="resources"></a><span data-ttu-id="41f66-151">资源</span><span class="sxs-lookup"><span data-stu-id="41f66-151">Resources</span></span>

* [<span data-ttu-id="41f66-152">将"共享到 Teams"按钮添加到网站</span><span class="sxs-lookup"><span data-stu-id="41f66-152">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="41f66-153">设计 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="41f66-153">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="41f66-154">Microsoft Teams JavaScript 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="41f66-154">Microsoft Teams JavaScript client SDK</span></span>](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="41f66-155">适用于[JavaScript](https://github.com/Microsoft/botbuilder-js)和[.NET](https://github.com/Microsoft/botbuilder-dotnet/)的 Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="41f66-155">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="41f66-156">发布 Teams 应用</span><span class="sxs-lookup"><span data-stu-id="41f66-156">Publish your Teams app</span></span>](concepts/deploy-and-publish/overview.md)
