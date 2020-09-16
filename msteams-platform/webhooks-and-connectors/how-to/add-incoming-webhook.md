---
title: 向具有传入 webhook 的 Microsoft 团队发布外部请求
author: laujan
description: 如何将传入 webhook 添加到团队应用
keywords: 团队选项卡传出 webhook *
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 3aa795170af9695fc375043c94e794f814b38646
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "47819065"
---
# <a name="post-external-requests-to-teams-with-incoming-webhooks"></a><span data-ttu-id="7ee95-104">向具有传入 webhook 的团队发布外部请求</span><span class="sxs-lookup"><span data-stu-id="7ee95-104">Post external requests to Teams with incoming webhooks</span></span>

## <a name="what-are-incoming-webhooks-in-teams"></a><span data-ttu-id="7ee95-105">哪些是团队中的传入 webhook？</span><span class="sxs-lookup"><span data-stu-id="7ee95-105">What are incoming webhooks in Teams?</span></span>

<span data-ttu-id="7ee95-106">传入 webhook 是在团队中提供的一种特殊类型的连接器，可提供一种简单的方法，让外部应用程序在团队频道中共享内容，并经常用作跟踪和通知工具。</span><span class="sxs-lookup"><span data-stu-id="7ee95-106">Incoming webhooks are special type of Connector in Teams that provide a simple way for an external app to share content in team channels and are often used as tracking and notification tools.</span></span> <span data-ttu-id="7ee95-107">团队提供一个唯一的 URL，您将 JSON 有效负载与要发布的邮件（通常采用卡片格式）一起发送。</span><span class="sxs-lookup"><span data-stu-id="7ee95-107">Teams provides a unique URL to which you send a JSON payload with the message that you want to POST, typically in a card format.</span></span> <span data-ttu-id="7ee95-108">卡片是用户界面 (UI) 容器，其中包含与单个主题相关的内容和操作，并且是以一致的方式显示邮件数据的一种方式。</span><span class="sxs-lookup"><span data-stu-id="7ee95-108">Cards are user-interface (UI) containers that contain content and actions related to a single topic and are a way to present message data in a consistent way.</span></span> <span data-ttu-id="7ee95-109">团队使用三种功能中的卡片：</span><span class="sxs-lookup"><span data-stu-id="7ee95-109">Teams uses cards within three capabilities:</span></span>

* <span data-ttu-id="7ee95-110">机器人</span><span class="sxs-lookup"><span data-stu-id="7ee95-110">Bots</span></span>
* <span data-ttu-id="7ee95-111">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="7ee95-111">Messaging extensions</span></span>
* <span data-ttu-id="7ee95-112">连接器</span><span class="sxs-lookup"><span data-stu-id="7ee95-112">Connectors</span></span>

## <a name="incoming-webhook-key-features"></a><span data-ttu-id="7ee95-113">传入 webhook 密钥功能</span><span class="sxs-lookup"><span data-stu-id="7ee95-113">Incoming webhook key features</span></span>

| <span data-ttu-id="7ee95-114">功能</span><span class="sxs-lookup"><span data-stu-id="7ee95-114">Feature</span></span> | <span data-ttu-id="7ee95-115">说明</span><span class="sxs-lookup"><span data-stu-id="7ee95-115">Description</span></span> |
| ------- | ----------- |
|<span data-ttu-id="7ee95-116">作用域配置</span><span class="sxs-lookup"><span data-stu-id="7ee95-116">Scoped Configuration</span></span>|<span data-ttu-id="7ee95-117">传入 webhook 的范围和配置在频道级别 (例如，传出 webhook 的范围和在团队一级) 配置。</span><span class="sxs-lookup"><span data-stu-id="7ee95-117">Incoming webhooks are scoped and configured at the channel level (e.g., outgoing webhooks are scoped and configured at the team level).</span></span>|
|<span data-ttu-id="7ee95-118">安全资源定义</span><span class="sxs-lookup"><span data-stu-id="7ee95-118">Secure resource definitions</span></span>|<span data-ttu-id="7ee95-119">将邮件格式化为 JSON 有效负载。</span><span class="sxs-lookup"><span data-stu-id="7ee95-119">Messages are formatted as JSON payloads.</span></span> <span data-ttu-id="7ee95-120">此声明性邮件结构阻止了恶意代码的注入，因为在客户端上没有执行任何代码。</span><span class="sxs-lookup"><span data-stu-id="7ee95-120">This declarative messaging structure prevents the injection of malicious code as there is no code execution on the client.</span></span>|
|<span data-ttu-id="7ee95-121">可操作邮件支持</span><span class="sxs-lookup"><span data-stu-id="7ee95-121">Actionable messaging support</span></span>|<span data-ttu-id="7ee95-122">如果选择通过卡片发送邮件，则必须使用可 **操作邮件卡片** 格式。</span><span class="sxs-lookup"><span data-stu-id="7ee95-122">If you choose to send messages via cards, you must use the **actionable message card** format.</span></span> <span data-ttu-id="7ee95-123">所有 Office 365 组（包括团队）都支持可操作邮件卡。</span><span class="sxs-lookup"><span data-stu-id="7ee95-123">Actionable message cards are supported in all Office 365 groups including Teams.</span></span> <span data-ttu-id="7ee95-124">下面是指向旧版可 [操作邮件卡参考](/outlook/actionable-messages/message-card-reference) 和 [邮件卡样本](https://messagecardplayground.azurewebsites.net)的链接。</span><span class="sxs-lookup"><span data-stu-id="7ee95-124">Here are links to the [Legacy actionable message card reference](/outlook/actionable-messages/message-card-reference) and the [Message card playground](https://messagecardplayground.azurewebsites.net).</span></span>|
|<span data-ttu-id="7ee95-125">独立 HTTPS 消息支持</span><span class="sxs-lookup"><span data-stu-id="7ee95-125">Independent HTTPS messaging support</span></span>| <span data-ttu-id="7ee95-126">卡片是以清晰一致的方式呈现信息的绝佳方式。</span><span class="sxs-lookup"><span data-stu-id="7ee95-126">Cards are a great way to present information in a clear and consistent way.</span></span> <span data-ttu-id="7ee95-127">任何可发送 HTTPS POST 请求的工具或框架都可以通过传入 webhook 向团队发送邮件。</span><span class="sxs-lookup"><span data-stu-id="7ee95-127">Any tool or framework that can send HTTPS POST requests can send messages to Teams via an incoming webhook.</span></span>|
|<span data-ttu-id="7ee95-128">Markdown 支持</span><span class="sxs-lookup"><span data-stu-id="7ee95-128">Markdown support</span></span>|<span data-ttu-id="7ee95-129">可操作邮件卡中的所有文本字段都支持基本 Markdown。</span><span class="sxs-lookup"><span data-stu-id="7ee95-129">All text fields in actionable messaging cards support basic Markdown.</span></span> <span data-ttu-id="7ee95-130">**请勿在卡片中使用 HTML 标记**。</span><span class="sxs-lookup"><span data-stu-id="7ee95-130">**Don't use HTML markup in your cards**.</span></span> <span data-ttu-id="7ee95-131">将忽略 HTML 并将其视为纯文本。</span><span class="sxs-lookup"><span data-stu-id="7ee95-131">HTML is ignored and treated as plain text.</span></span>|

> [!Note]  
> <span data-ttu-id="7ee95-132">团队 bot、邮件扩展和 Bot 框架支持自适应卡，即开放式跨卡片平台框架。</span><span class="sxs-lookup"><span data-stu-id="7ee95-132">Teams bots, messaging extensions, and the Bot Framework support Adaptive Cards, an open cross-card platform framework.</span></span> <span data-ttu-id="7ee95-133">工作组连接器目前不支持自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="7ee95-133">Teams connectors do not currently support Adaptive Cards.</span></span> <span data-ttu-id="7ee95-134">但是，可以创建将自适应卡发布到团队频道的 [流](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) 。</span><span class="sxs-lookup"><span data-stu-id="7ee95-134">However, it is possible to create a [flow](https://flow.microsoft.com/blog/microsoft-flow-in-microsoft-teams/) that posts adaptive cards to a Teams channel.</span></span>

## <a name="add-an-incoming-webhook-to-a-teams-channel"></a><span data-ttu-id="7ee95-135">将传入 webhook 添加到团队频道</span><span class="sxs-lookup"><span data-stu-id="7ee95-135">Add an incoming webhook to a Teams channel</span></span>

> [!Important]  
> <span data-ttu-id="7ee95-136">如果您的团队的**设置**  =>  **成员权限**  =>  **允许成员创建、更新和删除连接器**，则任何团队成员都可以添加、修改或删除连接器。</span><span class="sxs-lookup"><span data-stu-id="7ee95-136">If your team's **Settings** => **Member permissions** => **Allow members to create, update, and remove connectors** is selected, any team member can add, modify, or delete a connector.</span></span>

1. <span data-ttu-id="7ee95-137">导航到要在其中添加 webhook 的通道，然后从顶部导航栏中选择 " ( # A3) *更多选项* "。</span><span class="sxs-lookup"><span data-stu-id="7ee95-137">Navigate to the channel where you want to add the webhook and select (&#8226;&#8226;&#8226;) *More Options* from the top navigation bar.</span></span>
1. <span data-ttu-id="7ee95-138">从下拉菜单中选择 " **连接器** "，并搜索 **传入的 Webhook**。</span><span class="sxs-lookup"><span data-stu-id="7ee95-138">Choose **Connectors** from the drop-down menu and search for **Incoming Webhook**.</span></span>
1. <span data-ttu-id="7ee95-139">选择 " **配置** " 按钮，提供一个名称，并为 webhook 上传图像头像（可选）。</span><span class="sxs-lookup"><span data-stu-id="7ee95-139">Select the **Configure** button, provide a name, and, optionally, upload an image avatar for your webhook.</span></span>
1. <span data-ttu-id="7ee95-140">对话框窗口将提供一个将映射到通道的唯一 URL。</span><span class="sxs-lookup"><span data-stu-id="7ee95-140">The dialog window will present a unique URL that will map to the channel.</span></span> <span data-ttu-id="7ee95-141">请确保 **复制并保存该 URL**-您需要将其提供给外部服务。</span><span class="sxs-lookup"><span data-stu-id="7ee95-141">Make sure that you **copy and save the URL**—you will need to provide it to the outside service.</span></span>
1. <span data-ttu-id="7ee95-142">选择 " **完成** " 按钮。</span><span class="sxs-lookup"><span data-stu-id="7ee95-142">Select the **Done** button.</span></span> <span data-ttu-id="7ee95-143">将在团队频道中提供 webhook。</span><span class="sxs-lookup"><span data-stu-id="7ee95-143">The webhook will be available in the team channel.</span></span>

## <a name="remove-an-incoming-webhook-from-a-teams-channel"></a><span data-ttu-id="7ee95-144">从团队频道中删除传入 webhook</span><span class="sxs-lookup"><span data-stu-id="7ee95-144">Remove an incoming webhook from a Teams channel</span></span>

1. <span data-ttu-id="7ee95-145">导航到添加了 webhook 的通道，然后从顶部导航栏中选择 " ( # A3) *更多选项* "。</span><span class="sxs-lookup"><span data-stu-id="7ee95-145">Navigate to the channel where the webhook was added and select (&#8226;&#8226;&#8226;) *More Options* from the top navigation bar.</span></span>
1. <span data-ttu-id="7ee95-146">从下拉菜单中选择 " **连接器** "。</span><span class="sxs-lookup"><span data-stu-id="7ee95-146">Choose **Connectors** from the drop-down menu.</span></span>
1. <span data-ttu-id="7ee95-147">在左侧的 " **管理**" 下，选择 " **已配置**"。</span><span class="sxs-lookup"><span data-stu-id="7ee95-147">On the left, under **Manage**, choose **Configured**.</span></span>
1. <span data-ttu-id="7ee95-148">选择配置为查看当前连接器列表的 *号码* 。</span><span class="sxs-lookup"><span data-stu-id="7ee95-148">Select the *number Configured* to see a list of your current connectors.</span></span>
1. <span data-ttu-id="7ee95-149">选择要删除的连接器旁边的 " **管理** "。</span><span class="sxs-lookup"><span data-stu-id="7ee95-149">Select **Manage** next to the connector that you want to delete.</span></span>
1. <span data-ttu-id="7ee95-150">选择 " **删除** " 按钮，将显示 " *删除配置* " 对话框。</span><span class="sxs-lookup"><span data-stu-id="7ee95-150">Select the **Remove** button and you will be presented with a *Remove Configuration* dialog box.</span></span>
1. <span data-ttu-id="7ee95-151">（可选）在选择 " **删除** " 按钮之前填写对话框字段和复选框。</span><span class="sxs-lookup"><span data-stu-id="7ee95-151">Optionally, complete the dialog box fields and checkboxes prior to selecting the **Remove** button.</span></span> <span data-ttu-id="7ee95-152">将从团队通道中删除 webhook。</span><span class="sxs-lookup"><span data-stu-id="7ee95-152">The webhook will be deleted from the team channel.</span></span>

## <a name="distribution"></a><span data-ttu-id="7ee95-153">分发</span><span class="sxs-lookup"><span data-stu-id="7ee95-153">Distribution</span></span>

<span data-ttu-id="7ee95-154">您有三个用于分发传入 webhook 的选项：</span><span class="sxs-lookup"><span data-stu-id="7ee95-154">You have three options for distributing your incoming webhook:</span></span>

* <span data-ttu-id="7ee95-155">为你的团队直接设置传入 webhook。</span><span class="sxs-lookup"><span data-stu-id="7ee95-155">Set up an incoming webhook directly for your team.</span></span>
* <span data-ttu-id="7ee95-156">添加配置页面并将传入 webhook 包装在[O365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)中</span><span class="sxs-lookup"><span data-stu-id="7ee95-156">Add a configuration page and wrap your incoming webhook in a [O365 Connector](~/webhooks-and-connectors/how-to/connectors-creating.md)</span></span>
* <span data-ttu-id="7ee95-157">将连接器打包并发布为您的 [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) 提交的一部分。</span><span class="sxs-lookup"><span data-stu-id="7ee95-157">Package and publish your Connector as part of your [AppSource](~/concepts/deploy-and-publish/office-store-guidance.md) submission.</span></span>

## <a name="learn-more"></a><span data-ttu-id="7ee95-158">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="7ee95-158">Learn more</span></span>

* [<span data-ttu-id="7ee95-159">将邮件发送到连接器和 Webhook</span><span class="sxs-lookup"><span data-stu-id="7ee95-159">Sending messages to Connectors and Webhooks</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
