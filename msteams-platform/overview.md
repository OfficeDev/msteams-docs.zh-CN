---
title: 生成适用于 Microsoft Teams 平台的应用
author: heath-hamilton
description: 大致了解开发人员如何使用自定义Microsoft Teams扩展自定义功能。
ms.topic: overview
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 645b8087b367dd3cc9f5efdd53c53974307ce65e
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630491"
---
# <a name="build-apps-for-microsoft-teams"></a><span data-ttu-id="d6b93-103">构建 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="d6b93-103">Build apps for Microsoft Teams</span></span>

<span data-ttu-id="d6b93-104">Microsoft Teams应用将关键信息、常用工具和受信任流程引入人们越来越集中、学习和工作的地方。</span><span class="sxs-lookup"><span data-stu-id="d6b93-104">Microsoft Teams apps bring key information, common tools, and trusted processes to where people increasingly gather, learn, and work.</span></span>

<span data-ttu-id="d6b93-105">应用是扩展Teams以满足你的需求。</span><span class="sxs-lookup"><span data-stu-id="d6b93-105">Apps are how you extend Teams to fit your needs.</span></span> <span data-ttu-id="d6b93-106">为现有应用创建全新的Teams或集成现有应用。</span><span class="sxs-lookup"><span data-stu-id="d6b93-106">Create something brand new for Teams or integrate an existing app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6b93-107">从这里开始</span><span class="sxs-lookup"><span data-stu-id="d6b93-107">Start here</span></span>](build-your-first-app/build-first-app-overview.md)

## <a name="what-are-teams-apps"></a><span data-ttu-id="d6b93-108">什么是Teams应用？</span><span class="sxs-lookup"><span data-stu-id="d6b93-108">What are Teams apps?</span></span>

<span data-ttu-id="d6b93-109">Teams应用是功能[的组合](concepts/capabilities-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="d6b93-109">Teams apps are a combination of [capabilities](concepts/capabilities-overview.md).</span></span> <span data-ttu-id="d6b93-110">某些应用使用简单的 (发送) ，而其他应用则复杂 (患者记录) 。</span><span class="sxs-lookup"><span data-stu-id="d6b93-110">Some apps are simple (send notifications), while others are complex (manage patient records).</span></span> <span data-ttu-id="d6b93-111">规划应用时，请记住Teams协作中心。</span><span class="sxs-lookup"><span data-stu-id="d6b93-111">When planning your app, remember that Teams is a collaboration hub.</span></span> <span data-ttu-id="d6b93-112">应用的最佳Teams有助于用户表达自己，并更好地协同工作。</span><span class="sxs-lookup"><span data-stu-id="d6b93-112">The best Teams apps help people express themselves and work better together.</span></span>

### <a name="personal-apps"></a><span data-ttu-id="d6b93-113">个人应用</span><span class="sxs-lookup"><span data-stu-id="d6b93-113">Personal apps</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="d6b93-114">**帮助用户关注**： [个人](concepts/design/personal-apps.md) 应用是一个专用空间或自动程序，可帮助用户专注于自己的任务或查看重要的活动。</span><span class="sxs-lookup"><span data-stu-id="d6b93-114">**Help people focus**: A [personal app](concepts/design/personal-apps.md) is a dedicated space or bot to help users focus on their own tasks or view activities important to them.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-personal-apps-2021.png" alt-text="在概念上表示个人应用在 Teams 客户端中的外观。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="tabs"></a><span data-ttu-id="d6b93-116">选项卡</span><span class="sxs-lookup"><span data-stu-id="d6b93-116">Tabs</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="d6b93-117">**协作更方便：** 在选项卡中显示基于 Web 的内容，[](tabs/what-are-tabs.md)用户可以在选项卡中一起讨论和处理内容。</span><span class="sxs-lookup"><span data-stu-id="d6b93-117">**Collaborate more conveniently**: Display your web-based content in a [tab](tabs/what-are-tabs.md) where people can discuss and work on it together.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-channel-chat-apps-2021.png" alt-text="选项卡在客户端中的外观的概念Teams表示。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="bots"></a><span data-ttu-id="d6b93-119">机器人</span><span class="sxs-lookup"><span data-stu-id="d6b93-119">Bots</span></span>

:::row:::
   :::column span="1":::

<span data-ttu-id="d6b93-120">**将字词转换为操作**：对话通常导致需要执行某些操作 (生成订单、查看代码、检查票证状态等) 。</span><span class="sxs-lookup"><span data-stu-id="d6b93-120">**Turn words into actions**: Conversations often result in the need to do something (generate an order, review my code, check ticket status, and so on).</span></span> <span data-ttu-id="d6b93-121">机器人[可以在](bots/what-are-bots.md)内部启动这些类型的Teams。</span><span class="sxs-lookup"><span data-stu-id="d6b93-121">A [bot](bots/what-are-bots.md) can kick off these kinds of workflows right inside Teams.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-bots-2021.png" alt-text="自动程序在客户端中的外观的概念Teams表示。" border="false":::

   :::column-end:::

:::row-end:::

### <a name="messaging-extensions"></a><span data-ttu-id="d6b93-123">消息扩展</span><span class="sxs-lookup"><span data-stu-id="d6b93-123">Messaging extensions</span></span>

:::row:::

   :::column span="1":::

<span data-ttu-id="d6b93-124">**使多任务更容易**[：使用消息传递](messaging-extensions/what-are-messaging-extensions.md)扩展，可以在对话中快速共享外部信息。</span><span class="sxs-lookup"><span data-stu-id="d6b93-124">**Make it easier to multitask**: With [messaging extensions](messaging-extensions/what-are-messaging-extensions.md), you can quickly share external information in a conversation.</span></span> <span data-ttu-id="d6b93-125">还可以对消息采取行动，例如根据频道帖子的内容创建帮助票证。</span><span class="sxs-lookup"><span data-stu-id="d6b93-125">You also can act on a message, such as creating a help ticket based on the content of a channel post.</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-messaging-extensions-2021.png" alt-text="在概念上表示邮件扩展在 Teams 中的外观。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="meeting-extensions"></a><span data-ttu-id="d6b93-127">会议扩展</span><span class="sxs-lookup"><span data-stu-id="d6b93-127">Meeting extensions</span></span>

:::row:::

   :::column span="1":::

<span data-ttu-id="d6b93-128">**为会议创建应用**：有一些选项用于将你的应用合并到Teams [体验](apps-in-teams-meetings/design/designing-apps-in-meetings.md)。</span><span class="sxs-lookup"><span data-stu-id="d6b93-128">**Create apps for meetings**: There are a few options for [incorporating your app into the Teams calling experience](apps-in-teams-meetings/design/designing-apps-in-meetings.md).</span></span>

   :::column-end:::

   :::column span="3":::

:::image type="content" source="assets/images/overview-meeting-extensions-2021.png" alt-text="在概念上表示会议扩展在 Teams 中的外观。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="webhooks-and-connectors"></a><span data-ttu-id="d6b93-130">Webhook 和连接器</span><span class="sxs-lookup"><span data-stu-id="d6b93-130">Webhooks and connectors</span></span>

:::row:::

   :::column span="":::

<span data-ttu-id="d6b93-131">**与外部应用通信**[：传入 Webhook](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks)是一种将通知从另一个应用自动发送到 Teams 通道的简单方法。</span><span class="sxs-lookup"><span data-stu-id="d6b93-131">**Communicate with external apps**: [Incoming webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#incoming-webhooks) are a simple way to automatically send notifications from another app to a Teams channel.</span></span> <span data-ttu-id="d6b93-132">使用 [传出 webhook，](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks)使用 @mention 发送 web 服务。</span><span class="sxs-lookup"><span data-stu-id="d6b93-132">With [outgoing webhooks](webhooks-and-connectors/what-are-webhooks-and-connectors.md#outgoing-webhooks), message your web service with an @mention.</span></span>

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-connectors.png" alt-text="连接器在客户端中的外观的概念Teams表示。" border="false":::

   :::column-end:::
:::row-end:::

### <a name="microsoft-graph-for-teams"></a><span data-ttu-id="d6b93-134">Microsoft Graph for Teams</span><span class="sxs-lookup"><span data-stu-id="d6b93-134">Microsoft Graph for Teams</span></span>

:::row:::

   :::column span="":::

<span data-ttu-id="d6b93-135">**利用 Teams** 数据：适用于 [Teams](/graph/teams-concept-overview)的 Microsoft Graph API 提供对团队、频道、用户和消息的访问权限，这些信息可帮助你创建或增强应用功能 (如丰富的通知) 。</span><span class="sxs-lookup"><span data-stu-id="d6b93-135">**Utilize Teams data**: The [Microsoft Graph API for Teams](/graph/teams-concept-overview) provides access to information about teams, channels, users, and messages that can help you create or enhance features for your app (such as rich notifications).</span></span>

   :::column-end:::

   :::column span="":::

:::image type="content" source="assets/images/overview-graph.png" alt-text="Microsoft Graph API Teams。" border="false":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="start-building"></a><span data-ttu-id="d6b93-137">开始构建</span><span class="sxs-lookup"><span data-stu-id="d6b93-137">Start building</span></span>

<span data-ttu-id="d6b93-138">通过设置环境和创建简单的Teams快速熟悉构建环境。</span><span class="sxs-lookup"><span data-stu-id="d6b93-138">Quickly familiarize yourself with building for Teams by setting up your environment and creating a simple app.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6b93-139">构建首个应用</span><span class="sxs-lookup"><span data-stu-id="d6b93-139">Build your first app</span></span>](build-your-first-app/build-first-app-overview.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="integrate-with-teams"></a><span data-ttu-id="d6b93-140">与Teams整合</span><span class="sxs-lookup"><span data-stu-id="d6b93-140">Integrate with Teams</span></span>

<span data-ttu-id="d6b93-141">将用户喜欢的现有 Web 应用、服务或系统的功能与 Teams。</span><span class="sxs-lookup"><span data-stu-id="d6b93-141">Blend the features users love about an existing web app, service, or system with the collaborative features of Teams.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6b93-142">集成现有应用</span><span class="sxs-lookup"><span data-stu-id="d6b93-142">Integrate an existing app</span></span>](samples/integrating-web-apps.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="a-little-code-goes-a-long-way"></a><span data-ttu-id="d6b93-143">一个小代码会大有作为</span><span class="sxs-lookup"><span data-stu-id="d6b93-143">A little code goes a long way</span></span>

<span data-ttu-id="d6b93-144">你无需成为专家程序员来构建出色的Teams应用。</span><span class="sxs-lookup"><span data-stu-id="d6b93-144">You don't need to be an expert programmer to build a great Teams app.</span></span> <span data-ttu-id="d6b93-145">请尝试多个低代码解决方案之一。</span><span class="sxs-lookup"><span data-stu-id="d6b93-145">Try one of several low-code solutions.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6b93-146">创建低代码应用</span><span class="sxs-lookup"><span data-stu-id="d6b93-146">Create a low-code app</span></span>](samples/teams-low-code-solutions.md)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="2":::

## <a name="get-ideas-for-your-app"></a><span data-ttu-id="d6b93-147">获取应用灵感</span><span class="sxs-lookup"><span data-stu-id="d6b93-147">Get ideas for your app</span></span>

<span data-ttu-id="d6b93-148">寻找应用开发灵感？</span><span class="sxs-lookup"><span data-stu-id="d6b93-148">Looking for app development inspiration?</span></span> <span data-ttu-id="d6b93-149">浏览我们具有高保真概念的实际方案和行业解决方案列表，了解应用Teams用户的各种方式。</span><span class="sxs-lookup"><span data-stu-id="d6b93-149">Browse our list of real-world scenarios and industry solutions with high fidelity concept mocks to understand the various ways Teams apps can help your users.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d6b93-150">请参阅应用方案</span><span class="sxs-lookup"><span data-stu-id="d6b93-150">See app scenarios</span></span>](https://adoption.microsoft.com/extensibility-look-book/scenarios/)

   :::column-end:::
   :::column span="":::

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="d6b93-151">另请参阅</span><span class="sxs-lookup"><span data-stu-id="d6b93-151">See also</span></span>

* [<span data-ttu-id="d6b93-152">将"共享到Teams"按钮添加到您的网站</span><span class="sxs-lookup"><span data-stu-id="d6b93-152">Add a Share-to-Teams button to your website</span></span>](concepts/build-and-test/share-to-teams.md)
* [<span data-ttu-id="d6b93-153">设计Teams应用</span><span class="sxs-lookup"><span data-stu-id="d6b93-153">Design your Teams app</span></span>](concepts/design/design-teams-app-overview.md)
* [<span data-ttu-id="d6b93-154">Microsoft TeamsJavaScript 客户端 SDK</span><span class="sxs-lookup"><span data-stu-id="d6b93-154">Microsoft Teams JavaScript client SDK</span></span>](/javascript/api/@microsoft/teams-js/?view=msteams-client-js-latest&preserve-view=true)
* <span data-ttu-id="d6b93-155">适用于[JavaScript](https://github.com/Microsoft/botbuilder-js)和[.NET](https://github.com/Microsoft/botbuilder-dotnet/)的 Bot Framework SDK</span><span class="sxs-lookup"><span data-stu-id="d6b93-155">Bot Framework SDK for [JavaScript](https://github.com/Microsoft/botbuilder-js) and [.NET](https://github.com/Microsoft/botbuilder-dotnet/)</span></span>
* [<span data-ttu-id="d6b93-156">分发Teams应用</span><span class="sxs-lookup"><span data-stu-id="d6b93-156">Distribute your Teams app</span></span>](concepts/deploy-and-publish/apps-publish-overview.md)
