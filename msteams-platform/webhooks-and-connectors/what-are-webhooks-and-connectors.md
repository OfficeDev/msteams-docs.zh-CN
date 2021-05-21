---
title: 什么是 Webhook 和连接器？
author: clearab
description: 了解 webhook 和连接器如何将 Web 服务连接到 Teams 客户端。
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: e36b73c0eaed5068311dae6c1ef8fdc073432334
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566801"
---
# <a name="what-are-webhooks-and-connectors"></a><span data-ttu-id="6b745-103">什么是 Webhook 和连接器？</span><span class="sxs-lookup"><span data-stu-id="6b745-103">What are webhooks and connectors?</span></span>

<span data-ttu-id="6b745-104">Webhook 和连接器是将 Web 服务连接到 Microsoft Teams 中的频道和团队的一种简单方法。</span><span class="sxs-lookup"><span data-stu-id="6b745-104">Webhooks and connectors are a simple way to connect your web services to channels and teams inside Microsoft Teams.</span></span> 

## <a name="outgoing-webhooks"></a><span data-ttu-id="6b745-105">传出 webhook</span><span class="sxs-lookup"><span data-stu-id="6b745-105">Outgoing webhooks</span></span>

<span data-ttu-id="6b745-106">通过传出 webhook，用户可以将文本消息从频道发送到 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="6b745-106">Outgoing webhooks allow your users to send text messages from a channel to your web services.</span></span> <span data-ttu-id="6b745-107">配置后，用户将能够@mention发送 Webhook，并发送消息到服务。</span><span class="sxs-lookup"><span data-stu-id="6b745-107">Once configured, your users will be able to @mention your outgoing webhook and send a message to your service.</span></span> <span data-ttu-id="6b745-108">你的服务将在五秒钟内发送对邮件的响应，其中可能包含文本或卡片。</span><span class="sxs-lookup"><span data-stu-id="6b745-108">Your service will have five seconds to send a response to the message, potentially containing text or a card.</span></span>

<span data-ttu-id="6b745-109">传出 Webhook 基于每个团队进行配置，不能作为常规 webhook 应用的一Teams一部分。</span><span class="sxs-lookup"><span data-stu-id="6b745-109">Outgoing webhooks are configured on a per-team basis, cannot be included as part of a normal Teams app.</span></span> <span data-ttu-id="6b745-110">它们最适合完成不需要收集或交换大量信息的特定于团队的工作负荷。</span><span class="sxs-lookup"><span data-stu-id="6b745-110">They are best suited for completing team-specific workloads that don't require large amounts of information to be collected or exchanged.</span></span>

<span data-ttu-id="6b745-111">有关详细信息，请参阅创建 [传出 Webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="6b745-111">For more information, see [Create an outgoing webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span></span>

## <a name="connectors"></a><span data-ttu-id="6b745-112">连接器</span><span class="sxs-lookup"><span data-stu-id="6b745-112">Connectors</span></span>

<span data-ttu-id="6b745-113">连接器允许用户订阅以接收来自 Web 服务的通知和消息。</span><span class="sxs-lookup"><span data-stu-id="6b745-113">Connectors allow users to subscribe to receive notifications and messages from your web services.</span></span> <span data-ttu-id="6b745-114">它们公开你的服务的 HTTPS 终结点，以将消息张贴到 - 通常采用卡片形式。</span><span class="sxs-lookup"><span data-stu-id="6b745-114">They expose an HTTPS endpoint for your service to post messages to - typically in the form of cards.</span></span>

### <a name="incoming-webhooks"></a><span data-ttu-id="6b745-115">传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="6b745-115">Incoming webhooks</span></span>

<span data-ttu-id="6b745-116">传入 webhook 是最简单的连接器类型。</span><span class="sxs-lookup"><span data-stu-id="6b745-116">Incoming webhooks are the simplest type of connector.</span></span> <span data-ttu-id="6b745-117">对于团队策略 (如果已启用该团队) 你可以选择公开接受正确格式的 JSON 的 HTTPS 终结点，并将消息插入到该通道中。</span><span class="sxs-lookup"><span data-stu-id="6b745-117">For any channel in team (if they are enabled for that team) you can choose to expose an HTTPS endpoint that will accept correctly formatted JSON and insert messages into that channel.</span></span> <span data-ttu-id="6b745-118">它们是将频道连接到服务的一种快速而简单的方式，并且最适用于特定团队所特有的方案。</span><span class="sxs-lookup"><span data-stu-id="6b745-118">They are a quick and easy way to connect a channel to your service, and are best used for scenarios that are unique to a particular team.</span></span> <span data-ttu-id="6b745-119">例如，可以在客户端通道中创建传入 webhook DevOps配置生成、部署和监控服务以发送警报。</span><span class="sxs-lookup"><span data-stu-id="6b745-119">For example, you could create an incoming webhook in your DevOps channel and configure your build, deployment and monitoring services to send alerts.</span></span>

<span data-ttu-id="6b745-120">有关详细信息，请参阅创建[传入 Webhook。](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)</span><span class="sxs-lookup"><span data-stu-id="6b745-120">For more information, see [Create an incoming webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).</span></span>

### <a name="office-365-connectors"></a><span data-ttu-id="6b745-121">Office 365 连接器</span><span class="sxs-lookup"><span data-stu-id="6b745-121">Office 365 Connectors</span></span>

<span data-ttu-id="6b745-122">Office 365连接器允许你为传入 Webhook 创建自定义配置页面，将它们打包为 Teams 应用的一部分。</span><span class="sxs-lookup"><span data-stu-id="6b745-122">Office 365 Connectors allow you to create a custom configuration page for your incoming webhook, and package them as part of a Teams app.</span></span> <span data-ttu-id="6b745-123">然后，你可以更广泛地分发该应用，甚至分发到我们的应用商店。</span><span class="sxs-lookup"><span data-stu-id="6b745-123">You can then distribute that app more broadly, or even to our app store.</span></span> <span data-ttu-id="6b745-124">你主要使用Office 365连接器卡发送邮件，并且还能够向它们添加一组有限的卡片操作。</span><span class="sxs-lookup"><span data-stu-id="6b745-124">You send messages primarily using Office 365 Connector cards, and have the ability to add a limited set of card actions to them as well.</span></span> <span data-ttu-id="6b745-125">例如，天气连接器允许用户选择一天中的位置和时间，以接收有关明天天气的更新。</span><span class="sxs-lookup"><span data-stu-id="6b745-125">A good example of this is a weather connector that allows users to choose a location and time of day to receive updates about tomorrow's weather.</span></span> <span data-ttu-id="6b745-126">它们在频道级别配置，但安装在团队级别。</span><span class="sxs-lookup"><span data-stu-id="6b745-126">They are configured on a channel level, but are installed at a team level.</span></span>

<span data-ttu-id="6b745-127">有关详细信息，请参阅创建[Office 365连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)。</span><span class="sxs-lookup"><span data-stu-id="6b745-127">For more information, see [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).</span></span>
