---
title: 创建传入 Webhook
author: laujan
description: 介绍如何将传入 Webhook 添加到 Teams 应用，以及将外部请求Teams传入 Webhook
keywords: teams 选项卡传出 Webhook
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 53fe9725148579325386fa4677bebb61fdb72c56
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140106"
---
# <a name="create-incoming-webhook"></a><span data-ttu-id="545db-104">创建传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="545db-104">Create Incoming Webhook</span></span>

<span data-ttu-id="545db-105">传入 Webhook 允许任何外部应用在Teams内容。</span><span class="sxs-lookup"><span data-stu-id="545db-105">Incoming Webhook allows any external apps to share content in Teams channels.</span></span> <span data-ttu-id="545db-106">这些 Webhook 用作跟踪和通知工具。</span><span class="sxs-lookup"><span data-stu-id="545db-106">These webhooks are used as tracking and notifying tools.</span></span> <span data-ttu-id="545db-107">它们提供唯一的 URL，你可以将 JSON 有效负载与卡片格式的邮件一起发送到该 URL。</span><span class="sxs-lookup"><span data-stu-id="545db-107">They provide a unique URL, to which you send a JSON payload with a message in card format.</span></span> <span data-ttu-id="545db-108">卡片是包含与单个主题相关的内容和操作的用户界面容器。</span><span class="sxs-lookup"><span data-stu-id="545db-108">Cards are user interface containers that include content and actions related to a single topic.</span></span> <span data-ttu-id="545db-109">Teams以下功能内使用卡片：</span><span class="sxs-lookup"><span data-stu-id="545db-109">Teams use cards within the following capabilities:</span></span>

* <span data-ttu-id="545db-110">机器人</span><span class="sxs-lookup"><span data-stu-id="545db-110">Bots</span></span>
* <span data-ttu-id="545db-111">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="545db-111">Messaging extensions</span></span>
* <span data-ttu-id="545db-112">连接器</span><span class="sxs-lookup"><span data-stu-id="545db-112">Connectors</span></span>

## <a name="key-features-of-incoming-webhook"></a><span data-ttu-id="545db-113">传入 Webhook 的主要功能</span><span class="sxs-lookup"><span data-stu-id="545db-113">Key features of Incoming Webhook</span></span>

<span data-ttu-id="545db-114">下表提供了传入 Webhook 的功能和说明：</span><span class="sxs-lookup"><span data-stu-id="545db-114">The following table provides the features and description of Incoming Webhook:</span></span>

| <span data-ttu-id="545db-115">功能</span><span class="sxs-lookup"><span data-stu-id="545db-115">Features</span></span> | <span data-ttu-id="545db-116">说明</span><span class="sxs-lookup"><span data-stu-id="545db-116">Description</span></span> |
| ------- | ----------- |
|<span data-ttu-id="545db-117">使用传入 Webhook 的自适应卡片</span><span class="sxs-lookup"><span data-stu-id="545db-117">Adaptive Cards using an Incoming Webhook</span></span>|<span data-ttu-id="545db-118">自适应卡片可以通过传入 Webhook 发送。</span><span class="sxs-lookup"><span data-stu-id="545db-118">Adaptive Cards can be sent through Incoming Webhooks.</span></span> <span data-ttu-id="545db-119">有关详细信息，请参阅使用 [传入 Webhook 发送自适应卡片](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook)。</span><span class="sxs-lookup"><span data-stu-id="545db-119">For more information, see [Send Adaptive Cards using Incoming Webhooks](../../webhooks-and-connectors/how-to/connectors-using.md#send-adaptive-cards-using-an-incoming-webhook).</span></span>|
|<span data-ttu-id="545db-120">可操作邮件支持</span><span class="sxs-lookup"><span data-stu-id="545db-120">Actionable messaging support</span></span>|<span data-ttu-id="545db-121">可操作邮件卡在所有邮件组中Office 365，包括Teams。</span><span class="sxs-lookup"><span data-stu-id="545db-121">Actionable message cards are supported in all Office 365 groups including Teams.</span></span> <span data-ttu-id="545db-122">如果通过卡片发送邮件，则必须使用可操作邮件卡片格式。</span><span class="sxs-lookup"><span data-stu-id="545db-122">If you send messages through cards, you must use the actionable message card format.</span></span> <span data-ttu-id="545db-123">有关详细信息，请参阅旧版可[操作邮件卡参考](/outlook/actionable-messages/message-card-reference)[和邮件卡的场](https://messagecardplayground.azurewebsites.net)。</span><span class="sxs-lookup"><span data-stu-id="545db-123">For more information, see [legacy actionable message card reference](/outlook/actionable-messages/message-card-reference) and [message card playground](https://messagecardplayground.azurewebsites.net).</span></span>|
|<span data-ttu-id="545db-124">独立 HTTPS 消息支持</span><span class="sxs-lookup"><span data-stu-id="545db-124">Independent HTTPS messaging support</span></span>|<span data-ttu-id="545db-125">卡片清晰且一致地提供信息。</span><span class="sxs-lookup"><span data-stu-id="545db-125">Cards provide information clearly and consistently.</span></span> <span data-ttu-id="545db-126">任何可以发送 HTTPS POST 请求的工具或框架都可以通过传入 Webhook Teams消息。</span><span class="sxs-lookup"><span data-stu-id="545db-126">Any tool or framework that can send HTTPS POST requests, can send messages to Teams through an Incoming Webhook.</span></span>|
|<span data-ttu-id="545db-127">Markdown 支持</span><span class="sxs-lookup"><span data-stu-id="545db-127">Markdown support</span></span>|<span data-ttu-id="545db-128">可操作邮件卡中所有文本字段都支持基本 Markdown。</span><span class="sxs-lookup"><span data-stu-id="545db-128">All text fields in actionable messaging cards support basic Markdown.</span></span> <span data-ttu-id="545db-129">请勿在卡片中使用 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="545db-129">Do not use HTML markup in your cards.</span></span> <span data-ttu-id="545db-130">HTML 会遭忽略并被视为纯文本。</span><span class="sxs-lookup"><span data-stu-id="545db-130">HTML is ignored and treated as plain text.</span></span>|
|<span data-ttu-id="545db-131">作用域配置</span><span class="sxs-lookup"><span data-stu-id="545db-131">Scoped configuration</span></span>|<span data-ttu-id="545db-132">传入 Webhook 在通道级别进行范围设置和配置。</span><span class="sxs-lookup"><span data-stu-id="545db-132">Incoming Webhook is scoped and configured at the channel level.</span></span>|
|<span data-ttu-id="545db-133">安全资源定义</span><span class="sxs-lookup"><span data-stu-id="545db-133">Secure resource definitions</span></span>|<span data-ttu-id="545db-134">邮件的格式设置为 JSON 有效负载。</span><span class="sxs-lookup"><span data-stu-id="545db-134">Messages are formatted as JSON payloads.</span></span> <span data-ttu-id="545db-135">此声明性消息结构可防止插入恶意代码。</span><span class="sxs-lookup"><span data-stu-id="545db-135">This declarative messaging structure prevents the insertion of malicious code.</span></span>|

> [!NOTE]
> * <span data-ttu-id="545db-136">Teams机器人、消息传递扩展、传入 Webhook 和 Bot Framework 支持自适应卡片，这是一个开放的跨卡平台框架。</span><span class="sxs-lookup"><span data-stu-id="545db-136">Teams bots, messaging extensions, Incoming Webhook, and the Bot Framework support Adaptive Cards, an open cross card platform framework.</span></span> <span data-ttu-id="545db-137">目前[，Teams](../../webhooks-and-connectors/how-to/connectors-creating.md)连接器不支持自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="545db-137">Currently, [Teams connectors](../../webhooks-and-connectors/how-to/connectors-creating.md) do not support Adaptive Cards.</span></span> <span data-ttu-id="545db-138">但是，可以创建一个将[自适应卡片张贴](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/)到Teams流。</span><span class="sxs-lookup"><span data-stu-id="545db-138">However, it is possible to create a [flow](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) that posts Adaptive Cards to a Teams channel.</span></span>
> * <span data-ttu-id="545db-139">有关卡片和 Webhook 的信息，请参阅[自适应卡片和传入 Webhook。](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks)</span><span class="sxs-lookup"><span data-stu-id="545db-139">For more information on cards and webhooks, see [Adaptive cards and Incoming Webhooks](~/task-modules-and-cards/what-are-cards.md#adaptive-cards-and-incoming-webhooks).</span></span>

## <a name="create-incoming-webhook"></a><span data-ttu-id="545db-140">创建传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="545db-140">Create Incoming Webhook</span></span>

<span data-ttu-id="545db-141">**将传入 Webhook 添加到 Teams 通道**</span><span class="sxs-lookup"><span data-stu-id="545db-141">**To add an Incoming Webhook to a Teams channel**</span></span>

1. <span data-ttu-id="545db-142">转到要添加 Webhook 的频道，然后从顶部导航 &#8226;&#8226;&#8226; 选择"更多选项"。</span><span class="sxs-lookup"><span data-stu-id="545db-142">Go to the channel where you want to add the webhook and select &#8226;&#8226;&#8226; **More options** from the top navigation bar.</span></span>
1. <span data-ttu-id="545db-143">从 **下拉菜单中选择** "连接器"：</span><span class="sxs-lookup"><span data-stu-id="545db-143">Select **Connectors** from the dropdown menu:</span></span>

    ![选择连接器](~/assets/images/connectors.png)

1. <span data-ttu-id="545db-145">搜索"**传入 Webhook"，** 然后选择"添加 **"。**</span><span class="sxs-lookup"><span data-stu-id="545db-145">Search for **Incoming Webhook** and select **Add**.</span></span>
1. <span data-ttu-id="545db-146">选择 **"配置**"，提供名称，并上传 Webhook 图像（如果需要）：</span><span class="sxs-lookup"><span data-stu-id="545db-146">Select **Configure**, provide a name, and upload an image for your webhook if required:</span></span>

    ![配置按钮](~/assets/images/configure.png)

1. <span data-ttu-id="545db-148">对话框窗口显示映射到通道的唯一 URL。</span><span class="sxs-lookup"><span data-stu-id="545db-148">The dialog window presents a unique URL that maps to the channel.</span></span> <span data-ttu-id="545db-149">复制并保存 webhook URL，以将信息Microsoft Teams并选择"完成 **"：**</span><span class="sxs-lookup"><span data-stu-id="545db-149">Copy and save the webhook URL, to send information to Microsoft Teams and select **Done**:</span></span>

    ![唯一 URL](~/assets/images/url.png)

<span data-ttu-id="545db-151">webhook 在 Teams 中可用。</span><span class="sxs-lookup"><span data-stu-id="545db-151">The webhook is available in the Teams channel.</span></span>

> [!NOTE]
> <span data-ttu-id="545db-152">在Teams中，设置"成员权限""允许成员创建、更新和删除连接器"，以便任何团队成员都可以添加、修改  >    >  或删除连接器。</span><span class="sxs-lookup"><span data-stu-id="545db-152">In Teams, select **Settings** > **Member permissions** > **Allow members to create, update, and remove connectors**, so that any team member can add, modify, or delete a connector.</span></span>

## <a name="remove-incoming-webhook"></a><span data-ttu-id="545db-153">删除传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="545db-153">Remove Incoming Webhook</span></span>

<span data-ttu-id="545db-154">**从传入 Webhook 通道Teams Webhook**</span><span class="sxs-lookup"><span data-stu-id="545db-154">**To remove an Incoming Webhook from a Teams channel**</span></span>

1. <span data-ttu-id="545db-155">转到频道。</span><span class="sxs-lookup"><span data-stu-id="545db-155">Go to the channel.</span></span>
1. <span data-ttu-id="545db-156">Select &#8226;&#8226;&#8226; **More options** from the top navigation bar.</span><span class="sxs-lookup"><span data-stu-id="545db-156">Select &#8226;&#8226;&#8226; **More options** from the top navigation bar.</span></span>
1. <span data-ttu-id="545db-157">从 **下拉菜单中选择** "连接器"。</span><span class="sxs-lookup"><span data-stu-id="545db-157">Select **Connectors** from the dropdown menu.</span></span>
1. <span data-ttu-id="545db-158">在左侧的"管理 **"下，** 选择"**已配置"。**</span><span class="sxs-lookup"><span data-stu-id="545db-158">On the left, under **Manage**, select **Configured**.</span></span>
1. <span data-ttu-id="545db-159">选择 **< *"1>"*** 以查看当前连接器的列表：</span><span class="sxs-lookup"><span data-stu-id="545db-159">Select the **<*1*> Configured** to see a list of your current connectors:</span></span>

    ![已配置的 Webhook](~/assets/images/configured.png)

1. <span data-ttu-id="545db-161">选择要 **删除** 的连接器旁边的"管理"：</span><span class="sxs-lookup"><span data-stu-id="545db-161">Select **Manage** next to the connector that you want to remove:</span></span>

    ![管理 webhook](~/assets/images/manage.png)

1. <span data-ttu-id="545db-163">选择 **"删除"：**</span><span class="sxs-lookup"><span data-stu-id="545db-163">Select **Remove**:</span></span>

    ![删除 webhook](~/assets/images/remove.png)

    <span data-ttu-id="545db-165">将显示 **"删除配置** "对话框：</span><span class="sxs-lookup"><span data-stu-id="545db-165">The **Remove Configuration** dialog box appears:</span></span>

    ![删除配置](~/assets/images/removeconfiguration.png)

1. <span data-ttu-id="545db-167">填写对话框字段和复选框， **然后选择删除**：</span><span class="sxs-lookup"><span data-stu-id="545db-167">Complete the dialog box fields and checkboxes and select **Remove**:</span></span>

    ![最终删除](~/assets/images/finalremove.png)

    <span data-ttu-id="545db-169">Webhook 已从 webhook Teams中删除。</span><span class="sxs-lookup"><span data-stu-id="545db-169">The webhook is removed from the Teams channel.</span></span>

## <a name="see-also"></a><span data-ttu-id="545db-170">另请参阅</span><span class="sxs-lookup"><span data-stu-id="545db-170">See also</span></span>

* [<span data-ttu-id="545db-171">创建传出 Webhook</span><span class="sxs-lookup"><span data-stu-id="545db-171">Create an Outgoing Webhook</span></span>](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [<span data-ttu-id="545db-172">创建 Office 365 连接器</span><span class="sxs-lookup"><span data-stu-id="545db-172">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="545db-173">创建和发送邮件</span><span class="sxs-lookup"><span data-stu-id="545db-173">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
