---
title: 什么是 webhook 和连接器？
author: clearab
description: 了解 webhook 和连接器如何将您的 web 服务连接到团队客户端。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 740806e43af94d5a5da876affec2070a5a461b11
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651876"
---
# <a name="what-are-webhooks-and-connectors"></a><span data-ttu-id="77da1-103">什么是 webhook 和连接器？</span><span class="sxs-lookup"><span data-stu-id="77da1-103">What are webhooks and connectors?</span></span>

<span data-ttu-id="77da1-104">Webhook 和连接器是使用 Microsoft 团队频道和聊天连接外部系统和服务的简单方法。</span><span class="sxs-lookup"><span data-stu-id="77da1-104">Webhooks and connectors are straightforward ways to connect external systems and services with Microsoft Teams channels and chats.</span></span>

<span data-ttu-id="77da1-105">例如，用户可以从其他应用订阅通知 (通常采用卡片) 形式。</span><span class="sxs-lookup"><span data-stu-id="77da1-105">Users can, for example, subscribe to notifications from another app (typically in the form of cards).</span></span>

## <a name="incoming-webhooks"></a><span data-ttu-id="77da1-106">传入 webhook</span><span class="sxs-lookup"><span data-stu-id="77da1-106">Incoming webhooks</span></span>

<span data-ttu-id="77da1-107">传入 webhook 是最简单的连接器类型，以及将团队的通道连接到外部服务的快速而简单的方式。</span><span class="sxs-lookup"><span data-stu-id="77da1-107">Incoming webhooks are the simplest type of connector and a quick and easy way to connect a team's channel to an external service.</span></span> <span data-ttu-id="77da1-108">对于为该团队) 启用的任何频道 (，您可以公开一个 HTTPS 终结点，该终结点接受正确格式化的 JSON 并在通道中插入邮件。</span><span class="sxs-lookup"><span data-stu-id="77da1-108">For any channel (if enabled for that team), you can expose an HTTPS endpoint that accepts correctly formatted JSON and insert messages into the channel.</span></span>

<span data-ttu-id="77da1-109">请参阅[创建传入 webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="77da1-109">See [Create an incoming webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="77da1-110">用户方案</span><span class="sxs-lookup"><span data-stu-id="77da1-110">User scenarios</span></span>

<span data-ttu-id="77da1-111">传入 webhook 最适用于特定团队特有的方案。</span><span class="sxs-lookup"><span data-stu-id="77da1-111">Incoming webhooks are best for scenarios unique to a particular team.</span></span> <span data-ttu-id="77da1-112">例如，可以在 DevOps 通道中创建传入 webhook，并将生成、部署和监视服务配置为发送警报。</span><span class="sxs-lookup"><span data-stu-id="77da1-112">For example, you could create an incoming webhook in your DevOps channel and configure your build, deployment, and monitoring services to send alerts.</span></span>

## <a name="office-365-connectors"></a><span data-ttu-id="77da1-113">Office 365 连接器</span><span class="sxs-lookup"><span data-stu-id="77da1-113">Office 365 Connectors</span></span>

<span data-ttu-id="77da1-114">Office 365 连接器允许您为传入的 webhook 创建自定义配置页，并将其打包为团队应用程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="77da1-114">An Office 365 Connector allows you to create a custom configuration page for your incoming webhook and package it as part of a Teams app.</span></span> <span data-ttu-id="77da1-115">然后，可以将该应用更广泛地分发到应用商店。</span><span class="sxs-lookup"><span data-stu-id="77da1-115">You can then distribute that app more broadly or even to our app store.</span></span> <span data-ttu-id="77da1-116">您主要使用 Office 365 连接器卡发送邮件，这些卡也可以具有一组有限的卡片操作。</span><span class="sxs-lookup"><span data-stu-id="77da1-116">You send messages primarily using Office 365 Connector cards that can also have a limited set of card actions.</span></span> <span data-ttu-id="77da1-117">它们在频道级别上配置，但在团队级别安装。</span><span class="sxs-lookup"><span data-stu-id="77da1-117">They are configured on the channel level but installed at the team level.</span></span>

<span data-ttu-id="77da1-118">请参阅[创建 Office 365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)。</span><span class="sxs-lookup"><span data-stu-id="77da1-118">See [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="77da1-119">用户方案</span><span class="sxs-lookup"><span data-stu-id="77da1-119">User scenarios</span></span>

<span data-ttu-id="77da1-120">一个天气连接器，可让你选择一天的位置和时间接收有关明天的预测的更新。</span><span class="sxs-lookup"><span data-stu-id="77da1-120">A weather connector that lets you choose a location and time of day to receive updates about tomorrow's forecast.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="77da1-121">传出 webhook</span><span class="sxs-lookup"><span data-stu-id="77da1-121">Outgoing webhooks</span></span>

<span data-ttu-id="77da1-122">传出 webhook 允许用户向 web 服务发送来自频道的短信。</span><span class="sxs-lookup"><span data-stu-id="77da1-122">Outgoing webhooks allow your users to send text messages from a channel to your web services.</span></span> <span data-ttu-id="77da1-123">配置完成后，用户可以 @mention 您的应用程序并向外部服务发送邮件。</span><span class="sxs-lookup"><span data-stu-id="77da1-123">Once configured, users can @mention your app and send a message to your external service.</span></span> <span data-ttu-id="77da1-124">服务有5秒的时间向邮件发送响应，可能包含文本或卡。</span><span class="sxs-lookup"><span data-stu-id="77da1-124">Your service has five seconds to send a response to the message, potentially containing text or a card.</span></span>

<span data-ttu-id="77da1-125">传出 webhook 是基于每个团队配置的，不能作为普通团队应用程序的一部分包括在内。</span><span class="sxs-lookup"><span data-stu-id="77da1-125">Outgoing webhooks are configured on a per-team basis and can't be included as part of a normal Teams app.</span></span>

<span data-ttu-id="77da1-126">请参阅[创建传出 webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="77da1-126">See [Create an outgoing webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span></span>

### <a name="user-scenarios"></a><span data-ttu-id="77da1-127">用户方案</span><span class="sxs-lookup"><span data-stu-id="77da1-127">User scenarios</span></span>

<span data-ttu-id="77da1-128">传出 webhook 最适合用于完成不需要收集或交换大量信息的特定于团队的工作流。</span><span class="sxs-lookup"><span data-stu-id="77da1-128">Outgoing webhooks are best suited for completing team-specific workflows that don't require collecting or exchanging large amounts of information.</span></span>

## <a name="learn-more"></a><span data-ttu-id="77da1-129">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="77da1-129">Learn more</span></span>

* [<span data-ttu-id="77da1-130">规划应用程序</span><span class="sxs-lookup"><span data-stu-id="77da1-130">Planning your app</span></span>](../../concepts/extensibility-points.md)
* [<span data-ttu-id="77da1-131">生成应用程序</span><span class="sxs-lookup"><span data-stu-id="77da1-131">Building your app</span></span>](../../concepts/building-an-app.md)
* [<span data-ttu-id="77da1-132">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="77da1-132">Publishing your app</span></span>](../../concepts/deploy-and-publish/overview.md)
