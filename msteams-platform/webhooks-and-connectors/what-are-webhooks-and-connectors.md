---
title: 什么是 webhook 和连接器？
author: clearab
description: 了解 webhook 和连接器如何将您的 web 服务连接到团队客户端。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2be6f82bba0efe05a22a8da9da0acc1e0ad6fa00
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41672985"
---
# <a name="what-are-webhooks-and-connectors"></a><span data-ttu-id="25bcb-103">什么是 webhook 和连接器？</span><span class="sxs-lookup"><span data-stu-id="25bcb-103">What are webhooks and connectors?</span></span>

<span data-ttu-id="25bcb-104">Webhook 和连接器是将 web 服务连接到 Microsoft 团队中的频道和团队的简单方法。</span><span class="sxs-lookup"><span data-stu-id="25bcb-104">Webhooks and connectors are a simple way to connect your web services to channels and teams inside Microsoft Teams.</span></span> 

## <a name="outgoing-webhooks"></a><span data-ttu-id="25bcb-105">传出 webhook</span><span class="sxs-lookup"><span data-stu-id="25bcb-105">Outgoing webhooks</span></span>

<span data-ttu-id="25bcb-106">传出 webhook 允许用户向 web 服务发送来自频道的短信。</span><span class="sxs-lookup"><span data-stu-id="25bcb-106">Outgoing webhooks allow your users to send text messages from a channel to your web services.</span></span> <span data-ttu-id="25bcb-107">配置完成后，你的用户将能够 @mention 你的传出 webhook 并向你的服务发送一条消息。</span><span class="sxs-lookup"><span data-stu-id="25bcb-107">Once configured, your users will be able to @mention your outgoing webhook and send a message to your service.</span></span> <span data-ttu-id="25bcb-108">您的服务将有五秒的时间向邮件发送响应，可能包含文本或卡。</span><span class="sxs-lookup"><span data-stu-id="25bcb-108">Your service will have five seconds to send a response to the message, potentially containing text or a card.</span></span>

<span data-ttu-id="25bcb-109">传出 webhook 是按每个团队配置的，不能作为普通团队应用程序的一部分包括在内。</span><span class="sxs-lookup"><span data-stu-id="25bcb-109">Outgoing webhooks are configured on a per-team basis, cannot be included as part of a normal Teams app.</span></span> <span data-ttu-id="25bcb-110">它们最适合于完成不需要收集或交换大量信息的特定于团队的工作负载。</span><span class="sxs-lookup"><span data-stu-id="25bcb-110">They are best suited for completing team-specific workloads that don't require large amounts of information to be collected or exchanged.</span></span>

<span data-ttu-id="25bcb-111">请参阅[创建传出 webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="25bcb-111">See [Create an outgoing webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md).</span></span>

## <a name="connectors"></a><span data-ttu-id="25bcb-112">连接器</span><span class="sxs-lookup"><span data-stu-id="25bcb-112">Connectors</span></span>

<span data-ttu-id="25bcb-113">连接器允许用户订阅来自 web 服务的接收通知和消息。</span><span class="sxs-lookup"><span data-stu-id="25bcb-113">Connectors allow users to subscribe to receive notifications and messages from your web services.</span></span> <span data-ttu-id="25bcb-114">它们公开服务的 HTTPS 终结点，通常以卡片形式发布邮件。</span><span class="sxs-lookup"><span data-stu-id="25bcb-114">They expose an HTTPS endpoint for your service to post messages to - typically in the form of cards.</span></span>

### <a name="incoming-webhooks"></a><span data-ttu-id="25bcb-115">传入 webhook</span><span class="sxs-lookup"><span data-stu-id="25bcb-115">Incoming webhooks</span></span>

<span data-ttu-id="25bcb-116">传入的 webhook 是最简单的连接器类型。</span><span class="sxs-lookup"><span data-stu-id="25bcb-116">Incoming webhooks are a the simplest type of connector.</span></span> <span data-ttu-id="25bcb-117">对于团队中的任何频道（如果为该工作组启用），可以选择公开 HTTPS 终结点，该终结点将接受正确格式化的 JSON 并将邮件插入到该通道中。</span><span class="sxs-lookup"><span data-stu-id="25bcb-117">For any channel in team (if they are enabled for that team) you can choose to expose an HTTPS endpoint that will accept correctly formatted JSON and insert messages into that channel.</span></span> <span data-ttu-id="25bcb-118">它们是将频道连接到服务的快速、简便的方法，最适用于特定团队特有的方案。</span><span class="sxs-lookup"><span data-stu-id="25bcb-118">They are a quick and easy way to connect a channel to your service, and are best used for scenarios that are unique to a particular team.</span></span> <span data-ttu-id="25bcb-119">例如，可以在 DevOps 通道中创建一个传入 webhook，并将生成、部署和监控服务配置为发送通知。</span><span class="sxs-lookup"><span data-stu-id="25bcb-119">For example, you could create an incoming webhook in your DevOps channel and configure your build, deployment and monitoring services to send alerts.</span></span>

<span data-ttu-id="25bcb-120">请参阅[创建传入 webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)。</span><span class="sxs-lookup"><span data-stu-id="25bcb-120">See [Create an incoming webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md).</span></span>

### <a name="office-365-connectors"></a><span data-ttu-id="25bcb-121">Office 365 连接器</span><span class="sxs-lookup"><span data-stu-id="25bcb-121">Office 365 Connectors</span></span>

<span data-ttu-id="25bcb-122">Office 365 连接器允许您为传入的 webhook 创建自定义配置页，并将它们打包为团队应用程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="25bcb-122">Office 365 Connectors allow you to create a custom configuration page for your incoming webhook, and package them as part of a Teams app.</span></span> <span data-ttu-id="25bcb-123">然后，您可以更广泛地分发该应用程序，甚至可以分发到应用商店。</span><span class="sxs-lookup"><span data-stu-id="25bcb-123">You can then distribute that app more broadly, or even to our app store.</span></span> <span data-ttu-id="25bcb-124">您主要使用 Office 365 连接器卡发送邮件，并且还能够将一组有限的卡片操作添加到其中。</span><span class="sxs-lookup"><span data-stu-id="25bcb-124">You send messages primarily using Office 365 Connector cards, and have the ability to add a limited set of card actions to them as well.</span></span> <span data-ttu-id="25bcb-125">这是一个可供用户选择接收有关明天天气的更新的位置和时间的天气连接器的有用示例。</span><span class="sxs-lookup"><span data-stu-id="25bcb-125">A good example of this is a weather connector that allows users to choose a location and time of day to receive updates about tomorrow's weather.</span></span> <span data-ttu-id="25bcb-126">它们在频道级别上配置，但在团队级别安装。</span><span class="sxs-lookup"><span data-stu-id="25bcb-126">They are configured on a channel level, but are installed at a team level.</span></span>

<span data-ttu-id="25bcb-127">请参阅[创建 Office 365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)。</span><span class="sxs-lookup"><span data-stu-id="25bcb-127">See [Create an Office 365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md).</span></span>