---
title: Webhook 和连接器
author: clearab
description: 了解 webhook 和连接器如何将 Web 服务连接到 Teams 客户端。
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2cb763a6637abd3faa500de871119f0b829871bf
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140052"
---
# <a name="webhooks-and-connectors"></a><span data-ttu-id="03d52-103">Webhook 和连接器</span><span class="sxs-lookup"><span data-stu-id="03d52-103">Webhooks and connectors</span></span>

<span data-ttu-id="03d52-104">Webhook 和连接器有助于将 Web 服务连接到 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="03d52-104">Webhooks and connectors help to connect the web services to channels and teams in Microsoft Teams.</span></span> <span data-ttu-id="03d52-105">Webhook 是用户定义的 HTTP 回调，用于通知用户有关在 Microsoft Teams 通道中发生的任何操作。</span><span class="sxs-lookup"><span data-stu-id="03d52-105">Webhooks are user defined HTTP callback that notifies users about any action that has taken place in the Microsoft Teams channel.</span></span> <span data-ttu-id="03d52-106">它是应用获取实时数据的方法。</span><span class="sxs-lookup"><span data-stu-id="03d52-106">It is a way for an app to get real time data.</span></span> <span data-ttu-id="03d52-107">连接器允许用户订阅以接收来自 Web 服务的通知和消息。</span><span class="sxs-lookup"><span data-stu-id="03d52-107">Connectors allow users to subscribe to receive notifications and messages from your web services.</span></span> <span data-ttu-id="03d52-108">它们公开你的服务的 HTTPS 终结点，以卡片形式发布消息。</span><span class="sxs-lookup"><span data-stu-id="03d52-108">They expose an HTTPS endpoint for your service to post messages in the form of cards.</span></span>

## <a name="outgoing-webhooks"></a><span data-ttu-id="03d52-109">传出 Webhook</span><span class="sxs-lookup"><span data-stu-id="03d52-109">Outgoing Webhooks</span></span>

<span data-ttu-id="03d52-110">Webhook 可帮助Teams外部应用集成。</span><span class="sxs-lookup"><span data-stu-id="03d52-110">Webhooks help Teams to integrate with external apps.</span></span> <span data-ttu-id="03d52-111">使用传出 Webhook，您可以将短信从频道发送到 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="03d52-111">With Outgoing Webhooks, you can send text messages from a channel to the web services.</span></span> <span data-ttu-id="03d52-112">配置传出 Webhook 后，用户可以@mention传出 Webhook 并将消息发送到 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="03d52-112">After configuring the Outgoing Webhooks, users can @mention Outgoing Webhook and send a message to web services.</span></span> <span data-ttu-id="03d52-113">该服务在 10 秒钟内使用文本或卡片对邮件做出响应。</span><span class="sxs-lookup"><span data-stu-id="03d52-113">The service responds within ten seconds to the message with a text or a card.</span></span>

> [!NOTE]
> <span data-ttu-id="03d52-114">传出 Webhook 基于每个团队进行配置，不能作为正常 webhook 应用的一Teams一部分。</span><span class="sxs-lookup"><span data-stu-id="03d52-114">Outgoing Webhooks are configured on a per team basis and cannot be included as part of a normal Teams app.</span></span>

## <a name="connectors"></a><span data-ttu-id="03d52-115">连接器</span><span class="sxs-lookup"><span data-stu-id="03d52-115">Connectors</span></span>

<span data-ttu-id="03d52-116">连接器允许用户订阅从 Web 服务接收通知和消息。</span><span class="sxs-lookup"><span data-stu-id="03d52-116">Connectors allow users to subscribe to receive notifications and messages from the web services.</span></span> <span data-ttu-id="03d52-117">它们公开服务的 HTTPS 终结点，以将消息Teams频道，通常采用卡片形式。</span><span class="sxs-lookup"><span data-stu-id="03d52-117">They expose the HTTPS endpoint for the service to post messages to Teams channels, typically in the form of cards.</span></span>

### <a name="incoming-webhooks"></a><span data-ttu-id="03d52-118">传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="03d52-118">Incoming Webhooks</span></span>

<span data-ttu-id="03d52-119">传入 Webhook 可帮助将邮件从应用发布到Teams。</span><span class="sxs-lookup"><span data-stu-id="03d52-119">Incoming Webhooks help in posting messages from apps to Teams.</span></span> <span data-ttu-id="03d52-120">如果在任何频道中为团队启用了传入 Webhook，它将公开 HTTPS 终结点，该终结点接受格式正确的 JSON 并将消息插入到该通道中。</span><span class="sxs-lookup"><span data-stu-id="03d52-120">If Incoming Webhooks are enabled for a team in any channel, it exposes the HTTPS endpoint, which accepts correctly formatted JSON and inserts the messages into that channel.</span></span> <span data-ttu-id="03d52-121">例如，可以在客户端通道DevOps传入 Webhook，配置生成，并同时部署和监视服务以发送警报。</span><span class="sxs-lookup"><span data-stu-id="03d52-121">For example, you can create an Incoming Webhook in your DevOps channel, configure your build, and simultaneously deploy and monitor services to send alerts.</span></span>

### <a name="office-365-connectors"></a><span data-ttu-id="03d52-122">Office 365 连接器</span><span class="sxs-lookup"><span data-stu-id="03d52-122">Office 365 Connectors</span></span>

<span data-ttu-id="03d52-123">Office 365连接器允许你为传入 Webhook 创建自定义配置页，并打包它们作为 Teams 应用的一部分。</span><span class="sxs-lookup"><span data-stu-id="03d52-123">Office 365 Connectors allow you to create a custom configuration page for your Incoming Webhook and package them as part of a Teams app.</span></span> <span data-ttu-id="03d52-124">你主要使用 Office 365 连接器卡发送邮件，并且能够向这些连接器卡添加一组有限的卡片操作。</span><span class="sxs-lookup"><span data-stu-id="03d52-124">You send messages primarily using Office 365 Connector cards and have the ability to add a limited set of card actions to them.</span></span> <span data-ttu-id="03d52-125">例如，天气连接器允许用户选择一天中的位置和时间，以接收有关明天天气的更新。</span><span class="sxs-lookup"><span data-stu-id="03d52-125">For example, a weather connector that allows users to select a location and time of day, to receive updates about tomorrow's weather.</span></span> <span data-ttu-id="03d52-126">它们在频道级别配置，但安装在团队级别。</span><span class="sxs-lookup"><span data-stu-id="03d52-126">They are configured on a channel level but are installed at a team level.</span></span>

> [!NOTE]
> <span data-ttu-id="03d52-127">您可以将 Office 365 连接器Teams应用程序分发到我们的 AppStore。</span><span class="sxs-lookup"><span data-stu-id="03d52-127">You can distribute the Office 365 Connector Teams app to our AppStore.</span></span>

## <a name="create-and-send-messages"></a><span data-ttu-id="03d52-128">创建和发送邮件</span><span class="sxs-lookup"><span data-stu-id="03d52-128">Create and send messages</span></span>

<span data-ttu-id="03d52-129">可操作邮件允许用户在不离开其电子邮件客户端的情况下采取措施，从而增加用户参与度。</span><span class="sxs-lookup"><span data-stu-id="03d52-129">Actionable messages allow users to take action without leaving their email client, increasing user engagement.</span></span> <span data-ttu-id="03d52-130">使用 Office 365 和传入 Webhook，可以通过将 JSON 有效负载发布到 webhook URL 来发送消息。</span><span class="sxs-lookup"><span data-stu-id="03d52-130">With Office 365 and Incoming Webhooks, you can send messages by posting a JSON payload to the webhook URL.</span></span>

## <a name="see-also"></a><span data-ttu-id="03d52-131">另请参阅</span><span class="sxs-lookup"><span data-stu-id="03d52-131">See also</span></span>

* [<span data-ttu-id="03d52-132">创建传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="03d52-132">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="03d52-133">创建 Office 365 连接器</span><span class="sxs-lookup"><span data-stu-id="03d52-133">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="03d52-134">创建和发送邮件</span><span class="sxs-lookup"><span data-stu-id="03d52-134">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)

## <a name="next-step"></a><span data-ttu-id="03d52-135">后续步骤</span><span class="sxs-lookup"><span data-stu-id="03d52-135">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="03d52-136">创建传出 Webhook</span><span class="sxs-lookup"><span data-stu-id="03d52-136">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
