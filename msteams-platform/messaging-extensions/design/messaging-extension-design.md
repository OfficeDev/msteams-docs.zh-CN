---
title: 设计邮件扩展
description: 了解如何设计一个Teams扩展并获取 Microsoft Teams UI 工具包。
keywords: 团队设计指南参考消息传递扩展提示最佳做法
author: heath-hamilton
localization_priority: Normal
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: fd870d8e10ef74c36f8f6d145d48980f53e9303c
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52631025"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="d8bbf-104">设计邮件Microsoft Teams扩展</span><span class="sxs-lookup"><span data-stu-id="d8bbf-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="d8bbf-105">消息传递扩展是插入应用内容或在离开对话的情况下对消息操作快捷方式。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="d8bbf-106">为了指导应用设计，以下信息介绍了并说明了用户如何在应用中添加、使用和管理Teams。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="d8bbf-107">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="d8bbf-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="d8bbf-108">你可以找到全面的消息传递扩展设计指南，包括你可以根据需要获取和修改的元素，Microsoft Teams UI 工具包。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="d8bbf-109">获取 Microsoft Teams UI Kit （用户）</span><span class="sxs-lookup"><span data-stu-id="d8bbf-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="d8bbf-110">添加消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="d8bbf-110">Add a messaging extension</span></span>

<span data-ttu-id="d8bbf-111">可以在以下上下文上下文中添加Teams扩展：</span><span class="sxs-lookup"><span data-stu-id="d8bbf-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="d8bbf-112">从Teams存储。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-112">From the Teams store.</span></span>
* <span data-ttu-id="d8bbf-113">在靠近撰写框 (、在频道、聊天或会议) 、聊天或会议。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="d8bbf-114">值得注意的是，如果您在这些位置之一添加邮件扩展，则仅可以在该上下文中使用它。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="d8bbf-115">以下示例演示如何在频道中添加消息扩展：</span><span class="sxs-lookup"><span data-stu-id="d8bbf-115">The following example shows how you add a messaging extension in a channel:</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d8bbf-116">桌面</span><span class="sxs-lookup"><span data-stu-id="d8bbf-116">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="示例演示如何在频道中的撰写框附近添加消息传递扩展。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d8bbf-118">移动</span><span class="sxs-lookup"><span data-stu-id="d8bbf-118">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="示例演示如何在移动设备上的频道中的撰写框附近添加消息扩展。" border="false":::

---

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="d8bbf-120">设置邮件扩展</span><span class="sxs-lookup"><span data-stu-id="d8bbf-120">Set up a messaging extension</span></span>

<span data-ttu-id="d8bbf-121">身份验证不是强制性的，但是如果你的应用与票证跟踪工具类似，你可能需要用户登录以使用消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-121">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="d8bbf-122">若要在Teams一致，你无法自定义登录屏幕。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-122">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="d8bbf-123">如果使用单一登录 (SSO) 身份验证，用户将自动登录。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-123">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d8bbf-124">桌面</span><span class="sxs-lookup"><span data-stu-id="d8bbf-124">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="示例显示具有登录按钮的消息扩展设置屏幕。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d8bbf-126">移动</span><span class="sxs-lookup"><span data-stu-id="d8bbf-126">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="示例显示移动设备上具有登录按钮的邮件扩展设置屏幕。" border="false":::

---

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="d8bbf-128">邮件扩展类型</span><span class="sxs-lookup"><span data-stu-id="d8bbf-128">Types of messaging extensions</span></span>

<span data-ttu-id="d8bbf-129">邮件扩展可以具有搜索命令和/或操作命令。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-129">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="d8bbf-130">你的命令取决于你的应用的功能以及这些功能如何适应Teams用例。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-130">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="d8bbf-131">搜索命令</span><span class="sxs-lookup"><span data-stu-id="d8bbf-131">Search commands</span></span>

<span data-ttu-id="d8bbf-132">借助搜索命令，用户可以使用邮件扩展快速查找外部内容并插入邮件。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-132">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="d8bbf-133">搜索命令通常可在撰写框中使用。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-133">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="d8bbf-134">例如，您可以通过共享一段内容来开始讨论或添加讨论，而无需离开Teams。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-134">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d8bbf-135">桌面</span><span class="sxs-lookup"><span data-stu-id="d8bbf-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="示例显示从撰写框启动的基于搜索的邮件扩展。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d8bbf-137">移动</span><span class="sxs-lookup"><span data-stu-id="d8bbf-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="示例显示从移动设备上的撰写框启动的基于搜索的邮件扩展。" border="false":::

---

#### <a name="compose-box-layout-options"></a><span data-ttu-id="d8bbf-139">撰写框布局选项</span><span class="sxs-lookup"><span data-stu-id="d8bbf-139">Compose box layout options</span></span>

<span data-ttu-id="d8bbf-140">有一些选项用于显示邮件扩展搜索结果，包括 [列表和网格视图](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-140">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="插图显示邮件扩展搜索结果的布局选项。" border="false":::

### <a name="action-commands"></a><span data-ttu-id="d8bbf-142">操作命令</span><span class="sxs-lookup"><span data-stu-id="d8bbf-142">Action commands</span></span>

<span data-ttu-id="d8bbf-143">通过操作命令，用户能够触发操作并处理外部服务Teams。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-143">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="d8bbf-144">例如，如果您的应用程序跟踪订单，则用户可以使用同事消息的内容从聊天的右侧创建新订单。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-144">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="d8bbf-145">基于操作的邮件扩展通常需要用户在模式内完成表单或某种其他种类的配置。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-145">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="d8bbf-146">可以使用任务模块 创建 [这些体验](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-146">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="d8bbf-147">打开消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="d8bbf-147">Open a messaging extension</span></span>

<span data-ttu-id="d8bbf-148">撰写框和消息或帖子是人们使用邮件扩展的主要上下文。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-148">The compose box and messages or posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="d8bbf-149">从撰写框</span><span class="sxs-lookup"><span data-stu-id="d8bbf-149">From the compose box</span></span>

<span data-ttu-id="d8bbf-150">添加后，用户可以通过选择撰写框下方的应用图标来打开邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-150">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="d8bbf-151">在这些示例中，扩展具有搜索和操作命令。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-151">In these examples, the extension has search and action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d8bbf-152">桌面</span><span class="sxs-lookup"><span data-stu-id="d8bbf-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="示例演示如何从撰写框中打开邮件扩展。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d8bbf-154">移动</span><span class="sxs-lookup"><span data-stu-id="d8bbf-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="示例演示如何从移动设备上的撰写框中打开邮件扩展。" border="false":::

---

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="d8bbf-156">从聊天消息或频道帖子</span><span class="sxs-lookup"><span data-stu-id="d8bbf-156">From a chat message or channel post</span></span>

添加后，用户可以选择聊天消息或频道帖子上的"更多"图标 :::image type="icon" source="../../assets/icons/teams-client-more.png"::: 来查找扩展的操作命令。 <span data-ttu-id="d8bbf-158">扩展名可能列在"基于 **使用情况的更多** 操作"下。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-158">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="d8bbf-159">对来自聊天消息或频道帖子的更多操作的支持在移动Microsoft Teams不可用。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-159">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="d8bbf-160">聊天消息</span><span class="sxs-lookup"><span data-stu-id="d8bbf-160">Chat message</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d8bbf-161">桌面</span><span class="sxs-lookup"><span data-stu-id="d8bbf-161">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="示例演示如何从聊天消息中打开消息扩展。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d8bbf-163">移动</span><span class="sxs-lookup"><span data-stu-id="d8bbf-163">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-chat-post.png" alt-text="示例演示如何从移动设备上的聊天帖子打开消息传递扩展。" border="false":::

---
':::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
':::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
---

## <a name="use-a-messaging-extension"></a><span data-ttu-id="d8bbf-165">使用消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="d8bbf-165">Use a messaging extension</span></span>

<span data-ttu-id="d8bbf-166">以下方案显示了人们使用邮件扩展的主要方式。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-166">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="d8bbf-167">将内容插入到邮件中</span><span class="sxs-lookup"><span data-stu-id="d8bbf-167">Insert content into a message</span></span>

<span data-ttu-id="d8bbf-168">**1. 选择邮件扩展**。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-168">**1. Select a messaging extension**.</span></span> <span data-ttu-id="d8bbf-169">用户可以从撰写框中搜索要共享的内容。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-169">Users can search for the content they want to share from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d8bbf-170">桌面</span><span class="sxs-lookup"><span data-stu-id="d8bbf-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="示例显示用户搜索要从撰写框中插入的内容。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d8bbf-172">移动</span><span class="sxs-lookup"><span data-stu-id="d8bbf-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="示例显示用户搜索要从移动设备上的撰写框中插入的内容。" border="false":::

---

<span data-ttu-id="d8bbf-174">**2. 插入内容**。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-174">**2. Insert content**.</span></span> <span data-ttu-id="d8bbf-175">发布后，其他人可以回复或选择内容以查看应用中的更多信息。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-175">Once posted, others can reply or select the content to see more information in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d8bbf-176">桌面</span><span class="sxs-lookup"><span data-stu-id="d8bbf-176">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="示例显示用户在频道对话中发布内容。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d8bbf-178">移动</span><span class="sxs-lookup"><span data-stu-id="d8bbf-178">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="示例显示用户在移动设备上将内容发布到频道对话。" border="false":::

---

### <a name="take-action-on-a-message"></a><span data-ttu-id="d8bbf-180">对邮件采取措施</span><span class="sxs-lookup"><span data-stu-id="d8bbf-180">Take action on a message</span></span>

<span data-ttu-id="d8bbf-181">**1. 选择邮件扩展**。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-181">**1. Select a messaging extension**.</span></span> <span data-ttu-id="d8bbf-182">你的应用可以包含一个或多个操作命令。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-182">Your app can include one or more action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d8bbf-183">桌面</span><span class="sxs-lookup"><span data-stu-id="d8bbf-183">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="示例显示用户选择消息传递扩展操作命令。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d8bbf-185">移动</span><span class="sxs-lookup"><span data-stu-id="d8bbf-185">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-select-action-command.png" alt-text="示例显示用户在移动设备上选择消息传递扩展操作命令。" border="false":::

---

<span data-ttu-id="d8bbf-187">**2. 完成操作**。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-187">**2. Complete the action**.</span></span> <span data-ttu-id="d8bbf-188">你的应用可以接收并处理邮件操作发送的任何内容或数据。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-188">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="d8bbf-189">这允许用户保持其对话，并且（以下示例）无需担心直接在应用中输入信息。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-189">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d8bbf-190">桌面</span><span class="sxs-lookup"><span data-stu-id="d8bbf-190">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="如何对邮件采取操作的示例。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d8bbf-192">移动</span><span class="sxs-lookup"><span data-stu-id="d8bbf-192">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-complete-action-command.png" alt-text="如何对移动设备上的邮件采取操作的示例。" border="false":::

---

### <a name="preview-links"></a><span data-ttu-id="d8bbf-194">预览链接</span><span class="sxs-lookup"><span data-stu-id="d8bbf-194">Preview links</span></span>

<span data-ttu-id="d8bbf-195">邮件扩展还允许您将识别的 URL 中的丰富链接插入邮件 (此功能称为链接取消展开[.) ](../../messaging-extensions/how-to/link-unfurling.md)</span><span class="sxs-lookup"><span data-stu-id="d8bbf-195">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="d8bbf-196">**1. 在撰写框中** 粘贴可识别的链接。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-196">**1. Paste a recognized link** in the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d8bbf-197">桌面</span><span class="sxs-lookup"><span data-stu-id="d8bbf-197">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="示例显示用户在合成器框中粘贴链接。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d8bbf-199">移动</span><span class="sxs-lookup"><span data-stu-id="d8bbf-199">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="示例显示用户将链接粘贴到移动设备上的合成器框中。" border="false":::

---

<span data-ttu-id="d8bbf-201">**2. 插入内容**。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-201">**2. Insert content**.</span></span> <span data-ttu-id="d8bbf-202">如果你的应用识别撰写框中的 URL，它将链接呈现为提供 Web 内容的内容丰富的预览的卡片。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-202">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="d8bbf-203"> (有关详细信息， [请参阅自适应卡片](../../task-modules-and-cards/cards/design-effective-cards.md) 设计指南) </span><span class="sxs-lookup"><span data-stu-id="d8bbf-203">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d8bbf-204">桌面</span><span class="sxs-lookup"><span data-stu-id="d8bbf-204">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="示例显示 URL 如何由你的应用识别，在撰写框中包含一些丰富的内容。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="d8bbf-206">移动</span><span class="sxs-lookup"><span data-stu-id="d8bbf-206">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="示例显示 URL 如何由你的应用识别，如何在移动设备上的撰写框中包含一些丰富的内容。" border="false":::

---

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="d8bbf-208">管理消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="d8bbf-208">Manage a messaging extension</span></span>

<span data-ttu-id="d8bbf-209">通过右键单击图标，用户可以固定、删除或配置邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-209">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="d8bbf-210">解剖</span><span class="sxs-lookup"><span data-stu-id="d8bbf-210">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="d8bbf-211">撰写框中的消息扩展</span><span class="sxs-lookup"><span data-stu-id="d8bbf-211">Messaging extension in the compose box</span></span>

<span data-ttu-id="d8bbf-212">下面的示例是一个从撰写框打开的消息扩展。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-212">The following example is a messaging extension opened from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="d8bbf-213">桌面</span><span class="sxs-lookup"><span data-stu-id="d8bbf-213">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="插图显示撰写框中消息传递扩展的 UI 结构。" border="false":::

|<span data-ttu-id="d8bbf-215">计数器</span><span class="sxs-lookup"><span data-stu-id="d8bbf-215">Counter</span></span>|<span data-ttu-id="d8bbf-216">说明</span><span class="sxs-lookup"><span data-stu-id="d8bbf-216">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d8bbf-217">1</span><span class="sxs-lookup"><span data-stu-id="d8bbf-217">1</span></span>|<span data-ttu-id="d8bbf-218">**应用徽标**：应用徽标的颜色图标。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-218">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="d8bbf-219">2</span><span class="sxs-lookup"><span data-stu-id="d8bbf-219">2</span></span>|<span data-ttu-id="d8bbf-220">**应用名称**：应用的完整名称。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-220">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="d8bbf-221">3</span><span class="sxs-lookup"><span data-stu-id="d8bbf-221">3</span></span>|<span data-ttu-id="d8bbf-222">**操作命令菜单图标 (可选**) ：如果指定任何命令， (邮件扩展策略打开操作) 。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-222">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="d8bbf-223">4 </span><span class="sxs-lookup"><span data-stu-id="d8bbf-223">4</span></span>|<span data-ttu-id="d8bbf-224">**搜索框**：允许用户查找要插入的应用内容。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-224">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="d8bbf-225">5 </span><span class="sxs-lookup"><span data-stu-id="d8bbf-225">5</span></span>|<span data-ttu-id="d8bbf-226">**选项卡菜单 (可选) ：** 提供多个内容类别。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-226">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="d8bbf-227">6 </span><span class="sxs-lookup"><span data-stu-id="d8bbf-227">6</span></span>|<span data-ttu-id="d8bbf-228">**操作命令菜单 (可选) ：** 如果指定任何 (，将显示操作命令) 。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-228">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="d8bbf-229">7 </span><span class="sxs-lookup"><span data-stu-id="d8bbf-229">7</span></span>|<span data-ttu-id="d8bbf-230">**应用内容**：主要用于显示搜索结果。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-230">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="d8bbf-231">此处的示例是使用列表布局 (网格布局是另一个选项) 。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-231">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="d8bbf-232">8 </span><span class="sxs-lookup"><span data-stu-id="d8bbf-232">8</span></span>|<span data-ttu-id="d8bbf-233">**应用徽标**：应用徽标的大纲图标。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-233">**App logo**: Outline icon of your app logo.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="d8bbf-234">移动</span><span class="sxs-lookup"><span data-stu-id="d8bbf-234">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="插图显示移动设备上撰写框中消息传递扩展的 UI 结构。" border="false":::

|<span data-ttu-id="d8bbf-236">计数器</span><span class="sxs-lookup"><span data-stu-id="d8bbf-236">Counter</span></span>|<span data-ttu-id="d8bbf-237">说明</span><span class="sxs-lookup"><span data-stu-id="d8bbf-237">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d8bbf-238">1</span><span class="sxs-lookup"><span data-stu-id="d8bbf-238">1</span></span>|<span data-ttu-id="d8bbf-239">**应用名称**：应用的完整名称。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-239">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="d8bbf-240">2</span><span class="sxs-lookup"><span data-stu-id="d8bbf-240">2</span></span>|<span data-ttu-id="d8bbf-241">**操作命令菜单图标 (可选**) ：如果指定任何命令， (邮件扩展策略打开操作) 。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-241">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="d8bbf-242">3</span><span class="sxs-lookup"><span data-stu-id="d8bbf-242">3</span></span>|<span data-ttu-id="d8bbf-243">**搜索框**：允许用户查找要插入的应用内容。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-243">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="d8bbf-244">4 </span><span class="sxs-lookup"><span data-stu-id="d8bbf-244">4</span></span>|<span data-ttu-id="d8bbf-245">**选项卡菜单 (可选) ：** 提供多个内容类别。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-245">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="d8bbf-246">5 </span><span class="sxs-lookup"><span data-stu-id="d8bbf-246">5</span></span>|<span data-ttu-id="d8bbf-247">**操作命令菜单 (可选) ：** 如果指定任何 (，将显示操作命令) 。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-247">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="d8bbf-248">6 </span><span class="sxs-lookup"><span data-stu-id="d8bbf-248">6</span></span>|<span data-ttu-id="d8bbf-249">**应用内容**：主要用于显示搜索结果。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-249">**App content**: Primarily to display search results.</span></span>|

---

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="d8bbf-250">邮件扩展管理菜单</span><span class="sxs-lookup"><span data-stu-id="d8bbf-250">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="插图显示消息扩展管理菜单的 UI 结构。" border="false":::

|<span data-ttu-id="d8bbf-252">计数器</span><span class="sxs-lookup"><span data-stu-id="d8bbf-252">Counter</span></span>|<span data-ttu-id="d8bbf-253">说明</span><span class="sxs-lookup"><span data-stu-id="d8bbf-253">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="d8bbf-254">1</span><span class="sxs-lookup"><span data-stu-id="d8bbf-254">1</span></span>|<span data-ttu-id="d8bbf-255">**取消固定**：如果用户已固定你的应用，则可用。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-255">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="d8bbf-256">2</span><span class="sxs-lookup"><span data-stu-id="d8bbf-256">2</span></span>|<span data-ttu-id="d8bbf-257">**删除**：从频道、聊天或会议中删除消息扩展。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-257">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="d8bbf-258">最佳做法</span><span class="sxs-lookup"><span data-stu-id="d8bbf-258">Best practices</span></span>

<span data-ttu-id="d8bbf-259">使用这些建议创建高质量的应用体验。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-259">Use these recommendations to create a quality app experience.</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="d8bbf-260">设置和常规用法</span><span class="sxs-lookup"><span data-stu-id="d8bbf-260">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="有关安装和常规用法的示例。" border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="d8bbf-262">操作：与单一登录集成</span><span class="sxs-lookup"><span data-stu-id="d8bbf-262">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="d8bbf-263">SSO 使登录过程更加轻松、快速和安全。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-263">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="d8bbf-264">此外，如果用户已登录到你的个人应用，他们也不必再次登录来访问邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-264">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="与单一登录集成的示例。" border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="d8bbf-266">请勿：使用户离开对话</span><span class="sxs-lookup"><span data-stu-id="d8bbf-266">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="d8bbf-267">消息传递扩展是应该减少上下文切换的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-267">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="d8bbf-268">例如，您的扩展不应将用户直接引导到 Teams。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-268">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="d8bbf-269">要执行：突出显示邮件扩展</span><span class="sxs-lookup"><span data-stu-id="d8bbf-269">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="d8bbf-270">邮件扩展并不总是易于查找。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-270">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="d8bbf-271">在应用详细信息页面中包括如何使用它的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-271">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="d8bbf-272">如果你的应用还包括机器人，你可以将消息传递扩展帮助文档包括在机器人欢迎教程中。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-272">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="d8bbf-273">模板</span><span class="sxs-lookup"><span data-stu-id="d8bbf-273">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="模板示例。" border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="d8bbf-275">Do：Teams处理一些设计工作（如果可能）</span><span class="sxs-lookup"><span data-stu-id="d8bbf-275">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="d8bbf-276">如果对用例有意义，请考虑创建基于搜索的邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-276">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="d8bbf-277">Teams使用内置 theming 和辅助功能呈现这些类型的扩展。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-277">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="有关处理设计工作的示例。" border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="d8bbf-279">请勿：在任务模块中嵌入整个应用</span><span class="sxs-lookup"><span data-stu-id="d8bbf-279">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="d8bbf-280">如果邮件扩展需要操作命令，请保持任务模块简单，并仅显示完成该操作所需的组件。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-280">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="d8bbf-281">主题</span><span class="sxs-lookup"><span data-stu-id="d8bbf-281">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="有关 theming 的示例。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="d8bbf-283">应做：利用Teams令牌</span><span class="sxs-lookup"><span data-stu-id="d8bbf-283">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="d8bbf-284">每个Teams主题都有自己的配色方案。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-284">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="d8bbf-285">若要自动处理主题更改，请 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank"> (Fluent UI </a>) 颜色标记。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-285">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="有关颜色令牌的示例。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="d8bbf-287">请勿：硬编码颜色值</span><span class="sxs-lookup"><span data-stu-id="d8bbf-287">Don't: Hard code color values</span></span>

<span data-ttu-id="d8bbf-288">如果不使用颜色令牌Teams，你的设计将不太可扩展，并且需要更多的时间进行管理。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-288">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="d8bbf-289">操作</span><span class="sxs-lookup"><span data-stu-id="d8bbf-289">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="操作示例。" border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="d8bbf-291">应做：在上下文中包括有意义的操作命令</span><span class="sxs-lookup"><span data-stu-id="d8bbf-291">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="d8bbf-292">邮件操作应该与用户正在查看的内容相关。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-292">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="d8bbf-293">例如，为用户提供使用某人帖子中的文本创建问题或工作项的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-293">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="操作命令示例。" border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="d8bbf-295">请勿：包括不与上下文相关的操作命令</span><span class="sxs-lookup"><span data-stu-id="d8bbf-295">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="d8bbf-296">查看仪表板 **的消息** 操作可能看起来与大多数对话断开连接。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-296">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="d8bbf-297">搜索</span><span class="sxs-lookup"><span data-stu-id="d8bbf-297">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="d8bbf-298">Do：在键入时显示搜索结果</span><span class="sxs-lookup"><span data-stu-id="d8bbf-298">Do: Show search results while typing</span></span>

<span data-ttu-id="d8bbf-299">在用户键入时提供建议的搜索结果。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-299">Provide suggested search results while users type.</span></span> <span data-ttu-id="d8bbf-300">他们可以以最少的字符更快地找到所需的内容。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-300">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="d8bbf-301">请勿：要求用户提交查询</span><span class="sxs-lookup"><span data-stu-id="d8bbf-301">Don't: Require users to submit a query</span></span>

<span data-ttu-id="d8bbf-302">你可以让用户按某个键或选择一个按钮将查询发送到你的应用。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-302">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="d8bbf-303">虽然这在你的应用服务服务上可能更容易，但人们可能会感到困惑，因为他们不会在键入时看到实时搜索结果。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-303">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="d8bbf-304">应做：考虑零术语查询</span><span class="sxs-lookup"><span data-stu-id="d8bbf-304">Do: Consider zero-term queries</span></span>

<span data-ttu-id="d8bbf-305">例如，在用户向搜索框中写入任何内容之前，显示他们上次在你的应用上查看过什么内容。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-305">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="d8bbf-306">他们可能会想要将这些内容插入对话中。</span><span class="sxs-lookup"><span data-stu-id="d8bbf-306">It's possible that they want to insert that content into their conversation.</span></span>
