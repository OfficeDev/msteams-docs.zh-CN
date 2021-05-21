---
title: Post external requests to Microsoft Teams with incoming webhooks
author: laujan
description: 如何将传入 Webhook 添加到Teams应用
keywords: teams 选项卡传出 Webhook
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: bb2306cb57c069d3bed06702495da2775694643a
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566815"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a><span data-ttu-id="52423-104">Post external requests to Teams with incoming webhooks</span><span class="sxs-lookup"><span data-stu-id="52423-104">Post external requests to Teams with incoming webhooks</span></span>

## <a name="what-are-incoming-webhooks-in-teams"></a><span data-ttu-id="52423-105">什么是传入 webhook Teams？</span><span class="sxs-lookup"><span data-stu-id="52423-105">What are incoming webhooks in Teams?</span></span>

<span data-ttu-id="52423-106">传入 Webhook 是 Teams 中的特殊类型的连接器，可为外部应用提供一种在团队频道中共享内容的简单方法，并且通常用作跟踪和通知工具。</span><span class="sxs-lookup"><span data-stu-id="52423-106">Incoming webhooks are special type of Connector in Teams that provide a simple way for an external app to share content in team channels and are often used as tracking and notification tools.</span></span> <span data-ttu-id="52423-107">Teams提供一个唯一 URL，您通常会以卡片格式将 JSON 有效负载与要 POST 的邮件一起发送到该 URL。</span><span class="sxs-lookup"><span data-stu-id="52423-107">Teams provides a unique URL to which you send a JSON payload with the message that you want to POST, typically in a card format.</span></span> <span data-ttu-id="52423-108">卡片是用户界面 (UI) 容器，其中包含与单个主题相关的内容和操作，也是以一致的方式显示邮件数据的一种方式。</span><span class="sxs-lookup"><span data-stu-id="52423-108">Cards are user-interface (UI) containers that contain content and actions related to a single topic and are a way to present message data in a consistent way.</span></span> <span data-ttu-id="52423-109">Teams三个功能内使用卡片：</span><span class="sxs-lookup"><span data-stu-id="52423-109">Teams uses cards within three capabilities:</span></span>

* <span data-ttu-id="52423-110">机器人</span><span class="sxs-lookup"><span data-stu-id="52423-110">Bots</span></span>
* <span data-ttu-id="52423-111">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="52423-111">Messaging extensions</span></span>
* <span data-ttu-id="52423-112">连接器</span><span class="sxs-lookup"><span data-stu-id="52423-112">Connectors</span></span>

## <a name="incoming-webhook-key-features"></a><span data-ttu-id="52423-113">传入 Webhook 关键功能</span><span class="sxs-lookup"><span data-stu-id="52423-113">Incoming webhook key features</span></span>

| <span data-ttu-id="52423-114">功能</span><span class="sxs-lookup"><span data-stu-id="52423-114">Feature</span></span> | <span data-ttu-id="52423-115">说明</span><span class="sxs-lookup"><span data-stu-id="52423-115">Description</span></span> |
| ------- | ----------- |
|<span data-ttu-id="52423-116">作用域配置</span><span class="sxs-lookup"><span data-stu-id="52423-116">Scoped Configuration</span></span>|<span data-ttu-id="52423-117">传入 Webhook 的范围和配置在通道级别。</span><span class="sxs-lookup"><span data-stu-id="52423-117">Incoming webhooks are scoped and configured at the channel level.</span></span> <span data-ttu-id="52423-118">例如，传出 Webhook 的范围和配置在团队级别。</span><span class="sxs-lookup"><span data-stu-id="52423-118">For example, outgoing webhooks are scoped and configured at the team level.</span></span>|
|<span data-ttu-id="52423-119">安全资源定义</span><span class="sxs-lookup"><span data-stu-id="52423-119">Secure resource definitions</span></span>|<span data-ttu-id="52423-120">邮件的格式设置为 JSON 有效负载。</span><span class="sxs-lookup"><span data-stu-id="52423-120">Messages are formatted as JSON payloads.</span></span> <span data-ttu-id="52423-121">此声明性消息结构可防止注入恶意代码，因为客户端上没有执行代码。</span><span class="sxs-lookup"><span data-stu-id="52423-121">This declarative messaging structure prevents the injection of malicious code as there is no code execution on the client.</span></span>|
|<span data-ttu-id="52423-122">可操作邮件支持</span><span class="sxs-lookup"><span data-stu-id="52423-122">Actionable messaging support</span></span>|<span data-ttu-id="52423-123">如果选择通过卡片发送邮件，则必须使用可 **操作邮件卡片** 格式。</span><span class="sxs-lookup"><span data-stu-id="52423-123">If you choose to send messages via cards, you must use the **actionable message card** format.</span></span> <span data-ttu-id="52423-124">可操作邮件卡在所有邮件组中Office 365，包括Teams。</span><span class="sxs-lookup"><span data-stu-id="52423-124">Actionable message cards are supported in all Office 365 groups including Teams.</span></span> <span data-ttu-id="52423-125">以下是指向旧版可[操作邮件卡参考和](/outlook/actionable-messages/message-card-reference)[邮件卡片的编号的链接](https://messagecardplayground.azurewebsites.net)。</span><span class="sxs-lookup"><span data-stu-id="52423-125">Here are links to the [Legacy actionable message card reference](/outlook/actionable-messages/message-card-reference) and the [Message card playground](https://messagecardplayground.azurewebsites.net).</span></span>|
|<span data-ttu-id="52423-126">独立 HTTPS 消息支持</span><span class="sxs-lookup"><span data-stu-id="52423-126">Independent HTTPS messaging support</span></span>| <span data-ttu-id="52423-127">卡片是一种以清晰且一致的方式呈现信息的方式。</span><span class="sxs-lookup"><span data-stu-id="52423-127">Cards are a great way to present information in a clear and consistent way.</span></span> <span data-ttu-id="52423-128">任何可以发送 HTTPS POST 请求的工具或框架都可以通过传入 webhook Teams消息。</span><span class="sxs-lookup"><span data-stu-id="52423-128">Any tool or framework that can send HTTPS POST requests can send messages to Teams via an incoming webhook.</span></span>|
|<span data-ttu-id="52423-129">Markdown 支持</span><span class="sxs-lookup"><span data-stu-id="52423-129">Markdown support</span></span>|<span data-ttu-id="52423-130">可操作邮件卡中所有文本字段都支持基本 Markdown。</span><span class="sxs-lookup"><span data-stu-id="52423-130">All text fields in actionable messaging cards support basic Markdown.</span></span> <span data-ttu-id="52423-131">**请勿在卡片中使用 HTML 标记**。</span><span class="sxs-lookup"><span data-stu-id="52423-131">**Don't use HTML markup in your cards**.</span></span> <span data-ttu-id="52423-132">HTML 会遭忽略并被视为纯文本。</span><span class="sxs-lookup"><span data-stu-id="52423-132">HTML is ignored and treated as plain text.</span></span>|

> [!Note]
> <span data-ttu-id="52423-133">Teams聊天机器人、消息传递扩展、传入 Webhook 和 Bot Framework 支持自适应卡片，这是一个开放的跨卡平台框架。</span><span class="sxs-lookup"><span data-stu-id="52423-133">Teams bots, messaging extensions, incoming webhooks, and the Bot Framework support Adaptive Cards, an open cross-card platform framework.</span></span> <span data-ttu-id="52423-134">[Teams连接器](../../webhooks-and-connectors/how-to/connectors-creating.md)当前不支持自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="52423-134">[Teams connectors](../../webhooks-and-connectors/how-to/connectors-creating.md) do not currently support Adaptive Cards.</span></span> <span data-ttu-id="52423-135">但是，可以创建一个将[自适应卡片张贴](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/)到Teams流。</span><span class="sxs-lookup"><span data-stu-id="52423-135">However, it is possible to create a [flow](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) that posts Adaptive Cards to a Teams channel.</span></span>

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a><span data-ttu-id="52423-136">将传入 Webhook 添加到Teams通道</span><span class="sxs-lookup"><span data-stu-id="52423-136">Add an incoming webhook to a Teams channel</span></span>

> [!Important]  
> <span data-ttu-id="52423-137">如果已选择设置"成员权限""允许成员创建、更新和删除连接器"，则任何团队成员都可以添加、修改  =>    =>  或删除连接器。</span><span class="sxs-lookup"><span data-stu-id="52423-137">If your team's **Settings** => **Member permissions** => **Allow members to create, update, and remove connectors** is selected, any team member can add, modify, or delete a connector.</span></span>

<span data-ttu-id="52423-138">**添加传入 Webhook**</span><span class="sxs-lookup"><span data-stu-id="52423-138">**To add an incoming webhook**</span></span>

1. <span data-ttu-id="52423-139">导航到要添加 Webhook 的通道，然后从顶部导航栏中 (&#8226;&#8226;&#8226;) 选择 *"更多选项* "。</span><span class="sxs-lookup"><span data-stu-id="52423-139">Navigate to the channel where you want to add the webhook and select (&#8226;&#8226;&#8226;) *More Options* from the top navigation bar.</span></span>
1. <span data-ttu-id="52423-140">从 **下拉菜单中选择**"连接器"，然后搜索"传入 **Webhook"。**</span><span class="sxs-lookup"><span data-stu-id="52423-140">Choose **Connectors** from the drop-down menu and search for **Incoming Webhook**.</span></span>
1. <span data-ttu-id="52423-141">选择 **"配置** "按钮，提供名称，并（可选）为 Webhook 上传图像头像。</span><span class="sxs-lookup"><span data-stu-id="52423-141">Select the **Configure** button, provide a name, and, optionally, upload an image avatar for your webhook.</span></span>
1. <span data-ttu-id="52423-142">对话框窗口将显示将映射到通道的唯一 URL。</span><span class="sxs-lookup"><span data-stu-id="52423-142">The dialog window will present a unique URL that will map to the channel.</span></span> <span data-ttu-id="52423-143">请确保复制 **并保存 URL，** 您需要将其提供给外部服务。</span><span class="sxs-lookup"><span data-stu-id="52423-143">Make sure that you **copy and save the URL**—you will need to provide it to the outside service.</span></span>
1. <span data-ttu-id="52423-144">选择" **完成"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="52423-144">Select the **Done** button.</span></span> <span data-ttu-id="52423-145">webhook 将在团队频道中提供。</span><span class="sxs-lookup"><span data-stu-id="52423-145">The webhook will be available in the team channel.</span></span>

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a><span data-ttu-id="52423-146">从网络通道中删除Teams webhook</span><span class="sxs-lookup"><span data-stu-id="52423-146">Remove an incoming webhook from a Teams channel</span></span>

<span data-ttu-id="52423-147">**删除传入 Webhook**</span><span class="sxs-lookup"><span data-stu-id="52423-147">**To remove an incoming webhook**</span></span>

1. <span data-ttu-id="52423-148">导航到添加 webhook 的通道，然后从顶部导航 (&#8226;&#8226;&#8226;) *选择* "更多选项"。</span><span class="sxs-lookup"><span data-stu-id="52423-148">Navigate to the channel where the webhook was added and select (&#8226;&#8226;&#8226;) *More Options* from the top navigation bar.</span></span>
1. <span data-ttu-id="52423-149">从 **下拉菜单中选择** "连接器"。</span><span class="sxs-lookup"><span data-stu-id="52423-149">Choose **Connectors** from the drop-down menu.</span></span>
1. <span data-ttu-id="52423-150">在左侧的"管理 **"下，** 选择"**已配置"。**</span><span class="sxs-lookup"><span data-stu-id="52423-150">On the left, under **Manage**, choose **Configured**.</span></span>
1. <span data-ttu-id="52423-151">选择 *配置为* 查看当前连接器列表的号码。</span><span class="sxs-lookup"><span data-stu-id="52423-151">Select the *number Configured* to see a list of your current connectors.</span></span>
1. <span data-ttu-id="52423-152">选择要 **删除** 的连接器旁边的"管理"。</span><span class="sxs-lookup"><span data-stu-id="52423-152">Select **Manage** next to the connector that you want to delete.</span></span>
1. <span data-ttu-id="52423-153">选择 **"删除** "按钮，你将看到"删除 *配置"* 对话框。</span><span class="sxs-lookup"><span data-stu-id="52423-153">Select the **Remove** button and you will be presented with a *Remove Configuration* dialog box.</span></span>
1. <span data-ttu-id="52423-154">（可选）在选择"删除"按钮之前填写对话框字段 **和** 复选框。</span><span class="sxs-lookup"><span data-stu-id="52423-154">Optionally, complete the dialog box fields and checkboxes prior to selecting the **Remove** button.</span></span> <span data-ttu-id="52423-155">Webhook 将从团队频道中删除。</span><span class="sxs-lookup"><span data-stu-id="52423-155">The webhook will be deleted from the team channel.</span></span>

## <a name="distribution"></a><span data-ttu-id="52423-156">分发</span><span class="sxs-lookup"><span data-stu-id="52423-156">Distribution</span></span>

<span data-ttu-id="52423-157">有三个选项用于分发传入的 Webhook：</span><span class="sxs-lookup"><span data-stu-id="52423-157">You have three options for distributing your incoming webhook:</span></span>

* <span data-ttu-id="52423-158">直接为团队设置传入 Webhook。</span><span class="sxs-lookup"><span data-stu-id="52423-158">Set up an incoming webhook directly for your team.</span></span>
* <span data-ttu-id="52423-159">添加配置页面，将传入的 Webhook 包装在 [O365 连接器中](~/webhooks-and-connectors/how-to/connectors-creating.md)</span><span class="sxs-lookup"><span data-stu-id="52423-159">Add a configuration page and wrap your incoming webhook in a [O365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md)</span></span>
* <span data-ttu-id="52423-160">将连接器打包并发布为 [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) 提交的一部分。</span><span class="sxs-lookup"><span data-stu-id="52423-160">Package and publish your Connector as part of your [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) submission.</span></span>

## <a name="see-also"></a><span data-ttu-id="52423-161">另请参阅</span><span class="sxs-lookup"><span data-stu-id="52423-161">See also</span></span>

[<span data-ttu-id="52423-162">将邮件发送到连接器和 Webhook</span><span class="sxs-lookup"><span data-stu-id="52423-162">Sending messages to Connectors and Webhooks</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
