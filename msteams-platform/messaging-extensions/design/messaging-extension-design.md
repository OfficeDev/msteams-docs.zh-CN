---
title: 设计消息传递扩展
description: 了解如何设计 Microsoft Teams 消息传递并获取 Microsoft Teams UI Kit。
keywords: Microsoft Teams 设计指南参考消息传递扩展提示最佳实践
author: heath-hamilton
localization_priority: Priority
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: f4d1ba1e6e0b71b37e2b7b2d2a32fb729822ba1c
ms.sourcegitcommit: 99b1f151e4e36a86c6a5d2ccbde01bf45b61f526
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2021
ms.locfileid: "53037668"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="1b0cb-104">设计 Microsoft Teams 消息传递</span><span class="sxs-lookup"><span data-stu-id="1b0cb-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="1b0cb-105">消息传递是插入应用程序内容或对消息采取行动的快捷方式，而无需从对话中导航。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>
<span data-ttu-id="1b0cb-106">为指导应用设计，以下信息描述并说明用户可以如何在 Teams 中添加、使用和管理消息传递。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="1b0cb-107">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="1b0cb-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="1b0cb-108">可在 Microsoft Teams UI Kit 中查看全面的消息传递设计指南，包括可根据需要获取和修改的元素。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1b0cb-109">获取 Microsoft Teams UI Kit（用户）</span><span class="sxs-lookup"><span data-stu-id="1b0cb-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="1b0cb-110">添加消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="1b0cb-110">Add a messaging extension</span></span>

<span data-ttu-id="1b0cb-111">可以在以下 Teams 上下文中添加消息传递扩展：</span><span class="sxs-lookup"><span data-stu-id="1b0cb-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="1b0cb-112">从 Teams 应用商店。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-112">From the Teams store.</span></span>
* <span data-ttu-id="1b0cb-113">在频道、聊天或会议（会议之前、期间和之后）中的撰写框旁边。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="1b0cb-114">值得注意的是，如果在这些位置之一添加消息传递扩展，则只能在该上下文中使用。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="1b0cb-115">下面的示例演示了如何在频道中添加消息传递扩展：</span><span class="sxs-lookup"><span data-stu-id="1b0cb-115">The following example shows how you add a messaging extension in a channel:</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1b0cb-116">桌面设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-116">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="示例：如何在频道的撰写框附近添加消息传递扩展。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="1b0cb-118">移动设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-118">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-add-in-channel.png" alt-text="示例：在移动设备上，如何在频道的撰写框附近添加消息传递扩展。" border="false":::

---

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="1b0cb-120">设置消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="1b0cb-120">Set up a messaging extension</span></span>

<span data-ttu-id="1b0cb-121">虽然并不强制进行身份验证，但如果应用类似于票证跟踪工具，则需要用户登录才能使用消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-121">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="1b0cb-122">为确保 Teams 应用的一致性，你无法自定义登录屏幕。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-122">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="1b0cb-123">如果使用单一登录 (SSO) 身份验证，则用户会自动登录。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-123">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1b0cb-124">桌面设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-124">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="示例：带有登录按钮的消息传递扩展设置屏幕。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="1b0cb-126">移动设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-126">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-set-up.png" alt-text="示例：移动设备上带有登录按钮的消息传递扩展设置屏幕。" border="false":::

---

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="1b0cb-128">消息扩展类型</span><span class="sxs-lookup"><span data-stu-id="1b0cb-128">Types of messaging extensions</span></span>

<span data-ttu-id="1b0cb-129">消息传递扩展可以包含搜索命令、操作命令或两者兼有。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-129">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="1b0cb-130">你的命令取决于应用的功能以及这些功能在 Teams 用例中的适用性。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-130">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="1b0cb-131">搜索命令</span><span class="sxs-lookup"><span data-stu-id="1b0cb-131">Search commands</span></span>

<span data-ttu-id="1b0cb-132">借助搜索命令，用户可以使用消息传递扩展来快速查找外部内容并插入到消息中。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-132">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="1b0cb-133">搜索命令通常在撰写框中可用。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-133">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="1b0cb-134">例如，你可以通过共享一段内容来开始讨论或添加到讨论中，而无需离开 Teams。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-134">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1b0cb-135">桌面设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-135">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="示例：从撰写框启动的基于搜索的消息传递扩展。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="1b0cb-137">移动设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-137">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-search-command-type.png" alt-text="示例：在移动设备上，从撰写框启动的基于搜索的消息传递扩展。" border="false":::

---

#### <a name="compose-box-layout-options"></a><span data-ttu-id="1b0cb-139">撰写框布局选项</span><span class="sxs-lookup"><span data-stu-id="1b0cb-139">Compose box layout options</span></span>

<span data-ttu-id="1b0cb-140">Teams 中提供多种选项，来显示消息扩展搜索结果，包括[列表和网格视图](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-140">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="图例：消息传递扩展搜索结果的布局选项" border="false":::

### <a name="action-commands"></a><span data-ttu-id="1b0cb-142">操作命令</span><span class="sxs-lookup"><span data-stu-id="1b0cb-142">Action commands</span></span>

<span data-ttu-id="1b0cb-143">操作命令允许用户在 Teams 中触发外部服务的操作和流程请求。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-143">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="1b0cb-144">例如，如果应用跟踪订单，则用户可以直接从聊天中，使用同事的消息内容新建订单。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-144">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="1b0cb-145">基于操作的消息传递扩展通常要求用户填写某个模式中的一个表单或一些其他类型的配置。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-145">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="1b0cb-146">你可以使用[任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)创建这些体验。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-146">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="1b0cb-147">打开邮件扩展</span><span class="sxs-lookup"><span data-stu-id="1b0cb-147">Open a messaging extension</span></span>

<span data-ttu-id="1b0cb-148">撰写框和消息或帖子是用户使用消息扩展的主要上下文。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-148">The compose box and messages or posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="1b0cb-149">从撰写框</span><span class="sxs-lookup"><span data-stu-id="1b0cb-149">From the compose box</span></span>

<span data-ttu-id="1b0cb-150">添加后，用户可以选择撰写框下方的应用图标来打开消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-150">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="1b0cb-151">在这些示例中，扩展同时拥有搜索和操作命令。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-151">In these examples, the extension has search and action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1b0cb-152">桌面设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-152">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="示例：如何从撰写框打开消息传递扩展。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="1b0cb-154">移动设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-154">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-compose-box.png" alt-text="示例：在移动设备上，如何从撰写框打开消息传递扩展。" border="false":::

---

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="1b0cb-156">从聊天消息或频道帖子</span><span class="sxs-lookup"><span data-stu-id="1b0cb-156">From a chat message or channel post</span></span>

添加后，用户可以选择聊天消息或频道帖子上的“**更多**:::image type="icon" source="../../assets/icons/teams-client-more.png":::”图标来查找扩展的操作命令。 <span data-ttu-id="1b0cb-158">根据使用情况，扩展可能列在 **更多操作** 的下方。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-158">Your extension may be listed under **More actions** based on usage.</span></span>

> [!NOTE]
> <span data-ttu-id="1b0cb-159">Microsoft Teams 移动平台上不支持通过聊天消息或频道帖子执行更多操作。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-159">Support for more actions from a chat message or channel post is not available on Microsoft Teams mobile platform.</span></span> 

#### <a name="chat-message"></a><span data-ttu-id="1b0cb-160">聊天消息</span><span class="sxs-lookup"><span data-stu-id="1b0cb-160">Chat message</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1b0cb-161">桌面设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-161">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="示例：如何从聊天消息打开消息传递扩展。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="1b0cb-163">移动设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-163">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-chat-post.png" alt-text="示例：在移动设备上，如何从聊天消息打开消息传递扩展。" border="false":::

---
':::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
':::image type="content" source="../../assets/images/messaging-extension/mobile-open-from-channel-post.png" alt-text="Example shows how to open a messaging extension from a channel post on mobile." border="false"::': null
---

## <a name="use-a-messaging-extension"></a><span data-ttu-id="1b0cb-165">使用邮件扩展</span><span class="sxs-lookup"><span data-stu-id="1b0cb-165">Use a messaging extension</span></span>

<span data-ttu-id="1b0cb-166">以下场景介绍了用户使用消息传递扩展的主要方式。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-166">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="1b0cb-167">在消息中插入内容</span><span class="sxs-lookup"><span data-stu-id="1b0cb-167">Insert content into a message</span></span>

<span data-ttu-id="1b0cb-168">**1. 选择消息传递扩展**。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-168">**1. Select a messaging extension**.</span></span> <span data-ttu-id="1b0cb-169">用户可以从撰写框中搜索要共享的内容。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-169">Users can search for the content they want to share from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1b0cb-170">桌面设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-170">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="示例：用户从撰写框搜索要插入的内容。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="1b0cb-172">移动设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-172">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-search.png" alt-text="示例：用户在移动设备上从撰写框搜索要插入的内容。" border="false":::

---

<span data-ttu-id="1b0cb-174">**2. 插入内容**。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-174">**2. Insert content**.</span></span> <span data-ttu-id="1b0cb-175">发布内容后，其他人可以回复或选择内容，查看应用中的详细信息。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-175">Once posted, others can reply or select the content to see more information in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1b0cb-176">桌面设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-176">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="示例：用户在频道对话中发布内容。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="1b0cb-178">移动设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-178">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-content-posted.png" alt-text="示例：用户在移动设备上，在频道对话中发布内容。" border="false":::

---

### <a name="take-action-on-a-message"></a><span data-ttu-id="1b0cb-180">对消息执行操作</span><span class="sxs-lookup"><span data-stu-id="1b0cb-180">Take action on a message</span></span>

<span data-ttu-id="1b0cb-181">**1. 选择消息传递扩展**。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-181">**1. Select a messaging extension**.</span></span> <span data-ttu-id="1b0cb-182">应用可以包含一个或多个操作命令。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-182">Your app can include one or more action commands.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1b0cb-183">桌面设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-183">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="示例：用户选择消息传递扩展操作命令。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="1b0cb-185">移动设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-185">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-select-action-command.png" alt-text="示例：用户在移动设备上选择消息传递扩展操作命令。" border="false":::

---

<span data-ttu-id="1b0cb-187">**2. 完成操作**。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-187">**2. Complete the action**.</span></span> <span data-ttu-id="1b0cb-188">应用可以接收和处理消息操作发送的任何内容或数据。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-188">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="1b0cb-189">这样，用户可以留在对话中（如以下示例），安心地直接在应用中输入信息。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-189">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1b0cb-190">桌面设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-190">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="示例：如何对消息执行操作。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="1b0cb-192">移动设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-192">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-complete-action-command.png" alt-text="示例：如何在移动设备上对消息执行操作。" border="false":::

---

### <a name="preview-links"></a><span data-ttu-id="1b0cb-194">预览链接</span><span class="sxs-lookup"><span data-stu-id="1b0cb-194">Preview links</span></span>

<span data-ttu-id="1b0cb-195">消息传递扩展还允许将识别到的 URL 中的富链接插入到消息中（此功能称为“[链接特殊解析](../../messaging-extensions/how-to/link-unfurling.md)”。）</span><span class="sxs-lookup"><span data-stu-id="1b0cb-195">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="1b0cb-196">**1. 在撰写框中粘贴识别到的链接**。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-196">**1. Paste a recognized link** in the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1b0cb-197">桌面设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-197">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="示例：用户在撰写框中粘贴链接。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="1b0cb-199">移动设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-199">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-paste-preview-link.png" alt-text="示例：用户在移动设备上，在撰写框中粘贴链接。" border="false":::

---

<span data-ttu-id="1b0cb-201">**2. 插入内容**。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-201">**2. Insert content**.</span></span> <span data-ttu-id="1b0cb-202">如果应用识别撰写框中的 URL，则会将链接呈现为提供 Web 内容内容丰富的预览卡片。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-202">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="1b0cb-203">（有关详细信息，请参阅[自适应卡设计准则](../../task-modules-and-cards/cards/design-effective-cards.md)。）</span><span class="sxs-lookup"><span data-stu-id="1b0cb-203">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1b0cb-204">桌面设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-204">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="示例：在被应用识别后，URL 如何在撰写框中包含一些丰富内容。" border="false":::

# <a name="mobile"></a>[<span data-ttu-id="1b0cb-206">移动设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-206">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-insert-preview-link.png" alt-text="示例：移动设备上，在被应用识别后，URL 如何在撰写框中包含一些丰富内容。" border="false":::

---

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="1b0cb-208">管理消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="1b0cb-208">Manage a messaging extension</span></span>

<span data-ttu-id="1b0cb-209">用户可以右键单击图标来固定、删除或配置消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-209">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="1b0cb-210">解剖</span><span class="sxs-lookup"><span data-stu-id="1b0cb-210">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="1b0cb-211">撰写框中的消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="1b0cb-211">Messaging extension in the compose box</span></span>

<span data-ttu-id="1b0cb-212">下面的示例是从撰写框打开的消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-212">The following example is a messaging extension opened from the compose box.</span></span>

# <a name="desktop"></a>[<span data-ttu-id="1b0cb-213">桌面设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-213">Desktop</span></span>](#tab/desktop)

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="图例：撰写框中消息传递扩展的 UI 解剖。" border="false":::

|<span data-ttu-id="1b0cb-215">计数器</span><span class="sxs-lookup"><span data-stu-id="1b0cb-215">Counter</span></span>|<span data-ttu-id="1b0cb-216">说明</span><span class="sxs-lookup"><span data-stu-id="1b0cb-216">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1b0cb-217">1</span><span class="sxs-lookup"><span data-stu-id="1b0cb-217">1</span></span>|<span data-ttu-id="1b0cb-218">**应用徽标**：应用徽标的彩色图标。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-218">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="1b0cb-219">2</span><span class="sxs-lookup"><span data-stu-id="1b0cb-219">2</span></span>|<span data-ttu-id="1b0cb-220">**应用名称**：应用的全名。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-220">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="1b0cb-221">3</span><span class="sxs-lookup"><span data-stu-id="1b0cb-221">3</span></span>|<span data-ttu-id="1b0cb-222">**操作命令菜单图标（可选）**：打开消息传递扩展的操作命令列表（如果指定）。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-222">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="1b0cb-223">4</span><span class="sxs-lookup"><span data-stu-id="1b0cb-223">4</span></span>|<span data-ttu-id="1b0cb-224">**搜索框**：允许用户查找要插入的应用内容。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-224">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="1b0cb-225">5</span><span class="sxs-lookup"><span data-stu-id="1b0cb-225">5</span></span>|<span data-ttu-id="1b0cb-226">**选项卡菜单（可选）**：提供多个内容类别。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-226">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="1b0cb-227">6</span><span class="sxs-lookup"><span data-stu-id="1b0cb-227">6</span></span>|<span data-ttu-id="1b0cb-228">**操作命令菜单（可选）**：显示操作命令列表（如果指定）。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-228">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="1b0cb-229">7</span><span class="sxs-lookup"><span data-stu-id="1b0cb-229">7</span></span>|<span data-ttu-id="1b0cb-230">**应用内容**：主要用于显示搜索结果。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-230">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="1b0cb-231">此处的示例使用的是列表布局（另一个选项是网格布局）。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-231">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="1b0cb-232">8</span><span class="sxs-lookup"><span data-stu-id="1b0cb-232">8</span></span>|<span data-ttu-id="1b0cb-233">**应用徽标**：应用徽标的大纲图标。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-233">**App logo**: Outline icon of your app logo.</span></span>|

# <a name="mobile"></a>[<span data-ttu-id="1b0cb-234">移动设备</span><span class="sxs-lookup"><span data-stu-id="1b0cb-234">Mobile</span></span>](#tab/mobile)

:::image type="content" source="../../assets/images/messaging-extension/mobile-anatomy-compose.png" alt-text="图例：在移动设备上撰写框中消息传递扩展的 UI 解剖。" border="false":::

|<span data-ttu-id="1b0cb-236">计数器</span><span class="sxs-lookup"><span data-stu-id="1b0cb-236">Counter</span></span>|<span data-ttu-id="1b0cb-237">说明</span><span class="sxs-lookup"><span data-stu-id="1b0cb-237">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1b0cb-238">1</span><span class="sxs-lookup"><span data-stu-id="1b0cb-238">1</span></span>|<span data-ttu-id="1b0cb-239">**应用名称**：应用的全名。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-239">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="1b0cb-240">2</span><span class="sxs-lookup"><span data-stu-id="1b0cb-240">2</span></span>|<span data-ttu-id="1b0cb-241">**操作命令菜单图标（可选）**：打开消息传递扩展的操作命令列表（如果指定）。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-241">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="1b0cb-242">3</span><span class="sxs-lookup"><span data-stu-id="1b0cb-242">3</span></span>|<span data-ttu-id="1b0cb-243">**搜索框**：允许用户查找要插入的应用内容。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-243">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="1b0cb-244">4</span><span class="sxs-lookup"><span data-stu-id="1b0cb-244">4</span></span>|<span data-ttu-id="1b0cb-245">**选项卡菜单（可选）**：提供多个内容类别。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-245">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="1b0cb-246">5</span><span class="sxs-lookup"><span data-stu-id="1b0cb-246">5</span></span>|<span data-ttu-id="1b0cb-247">**操作命令菜单（可选）**：显示操作命令列表（如果指定）。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-247">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="1b0cb-248">6</span><span class="sxs-lookup"><span data-stu-id="1b0cb-248">6</span></span>|<span data-ttu-id="1b0cb-249">**应用内容**：主要用于显示搜索结果。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-249">**App content**: Primarily to display search results.</span></span>|

---

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="1b0cb-250">消息传递扩展管理菜单</span><span class="sxs-lookup"><span data-stu-id="1b0cb-250">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="图例：消息传递扩展管理菜单的 UI 解剖。" border="false":::

|<span data-ttu-id="1b0cb-252">计数器</span><span class="sxs-lookup"><span data-stu-id="1b0cb-252">Counter</span></span>|<span data-ttu-id="1b0cb-253">说明</span><span class="sxs-lookup"><span data-stu-id="1b0cb-253">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1b0cb-254">1</span><span class="sxs-lookup"><span data-stu-id="1b0cb-254">1</span></span>|<span data-ttu-id="1b0cb-255">**取消固定**：如果用户已固定应用，则可用。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-255">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="1b0cb-256">2</span><span class="sxs-lookup"><span data-stu-id="1b0cb-256">2</span></span>|<span data-ttu-id="1b0cb-257">**删除**：从频道、聊天或会议中删除消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-257">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="1b0cb-258">最佳实践</span><span class="sxs-lookup"><span data-stu-id="1b0cb-258">Best practices</span></span>

<span data-ttu-id="1b0cb-259">使用上述建议打造优质应用体验。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-259">Use these recommendations to create a quality app experience.</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="1b0cb-260">设置和一般用途</span><span class="sxs-lookup"><span data-stu-id="1b0cb-260">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="示例：设置和一般用途。" border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="1b0cb-262">建议：与单一登录集成</span><span class="sxs-lookup"><span data-stu-id="1b0cb-262">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="1b0cb-263">单一登录可使登录过程更轻松、更快速、更安全。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-263">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="1b0cb-264">此外，如果用户已登录到你的个人应用，则无需再次登录即可访问消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-264">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="示例：与单一登录集成。" border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="1b0cb-266">不建议：让用户离开对话</span><span class="sxs-lookup"><span data-stu-id="1b0cb-266">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="1b0cb-267">消息传递扩展是旨在减少上下文切换的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-267">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="1b0cb-268">例如，你的扩展不应将用户定向到 Teams 外部的网页。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-268">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="1b0cb-269">建议：突出显示消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="1b0cb-269">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="1b0cb-270">要找到消息传递扩展常常并不容易。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-270">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="1b0cb-271">在应用详细信息页面中包含如何使用教程屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-271">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="1b0cb-272">如果应用还包括机器人，则可以在机器人欢迎教程中包含消息传递扩展帮助文档。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-272">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="1b0cb-273">模板化</span><span class="sxs-lookup"><span data-stu-id="1b0cb-273">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="示例：模板化。" border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="1b0cb-275">建议：如果可能，让 Teams 处理一些设计工作</span><span class="sxs-lookup"><span data-stu-id="1b0cb-275">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="1b0cb-276">如果对用例有意义，请考虑创建基于搜索的消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-276">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="1b0cb-277">Teams 使用内置主题和辅助功能来呈现这一类型的扩展。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-277">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="示例：处理设计工作。" border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="1b0cb-279">不建议：在任务模块中嵌入整个应用</span><span class="sxs-lookup"><span data-stu-id="1b0cb-279">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="1b0cb-280">如果消息传递扩展需要操作命令，请保持任务模块的简洁性，并仅显示完成操作所需的组件。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-280">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="1b0cb-281">主题</span><span class="sxs-lookup"><span data-stu-id="1b0cb-281">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="示例：主题。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="1b0cb-283">建议：充分利用 Teams 颜色令牌</span><span class="sxs-lookup"><span data-stu-id="1b0cb-283">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="1b0cb-284">每个 Teams 主题都有自己的配色方案。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-284">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="1b0cb-285">若要自动处理主题更改，请在设计中使用<a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">颜色令牌 (Fluent UI)</a>。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-285">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="示例：颜色令牌。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="1b0cb-287">不建议：硬编码颜色值</span><span class="sxs-lookup"><span data-stu-id="1b0cb-287">Don't: Hard code color values</span></span>

<span data-ttu-id="1b0cb-288">如果不使用 Teams 颜色令牌，则设计将无法缩放，并需要更多时间进行管理。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-288">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="1b0cb-289">操作</span><span class="sxs-lookup"><span data-stu-id="1b0cb-289">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="示例：操作。" border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="1b0cb-291">建议：包含上下文中有意义的操作命令</span><span class="sxs-lookup"><span data-stu-id="1b0cb-291">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="1b0cb-292">消息操作应与用户正在查看的内容相关。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-292">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="1b0cb-293">例如，为用户提供使用某人帖子中的文本创建问题或工作项的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-293">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="示例：操作命令。" border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="1b0cb-295">不建议：包含与上下文无关的操作命令</span><span class="sxs-lookup"><span data-stu-id="1b0cb-295">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="1b0cb-296">用于 **查看仪表板** 的消息操作，可能似乎与绝大多数对话都没有关联。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-296">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="1b0cb-297">搜索</span><span class="sxs-lookup"><span data-stu-id="1b0cb-297">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="1b0cb-298">建议：键入时显示搜索结果</span><span class="sxs-lookup"><span data-stu-id="1b0cb-298">Do: Show search results while typing</span></span>

<span data-ttu-id="1b0cb-299">当用户键入时，提供建议的搜索结果。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-299">Provide suggested search results while users type.</span></span> <span data-ttu-id="1b0cb-300">用户可以用最少的字符数量，更快地查找到所需内容。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-300">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="1b0cb-301">不建议：要求用户提交查询</span><span class="sxs-lookup"><span data-stu-id="1b0cb-301">Don't: Require users to submit a query</span></span>

<span data-ttu-id="1b0cb-302">可以让用户按一个键或选择一个按钮将查询发送到应用。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-302">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="1b0cb-303">虽然从应用服务来看，这样做可能更容易，但用户可能会感到困惑，因为他们在键入时并不能看到实时搜索结果。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-303">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="1b0cb-304">建议：考虑零关键词查询</span><span class="sxs-lookup"><span data-stu-id="1b0cb-304">Do: Consider zero-term queries</span></span>

<span data-ttu-id="1b0cb-305">例如，当用户在搜索框中写入任何内容之前，显示他们上次在应用中查看的内容。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-305">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="1b0cb-306">这些可能正是他们希望插入到对话中的内容。</span><span class="sxs-lookup"><span data-stu-id="1b0cb-306">It's possible that they want to insert that content into their conversation.</span></span>
