---
title: 设计邮件扩展
description: 了解如何设计团队消息扩展并获取 Microsoft 团队 UI 工具包。
keywords: 团队设计准则参考邮件扩展提示最佳实践
author: heath-hamilton
ms.author: qinch
ms.topic: conceptual
ms.openlocfilehash: ad628bdaa46058aed4acdcea1a224c7ebfe40f89
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604805"
---
# <a name="designing-your-microsoft-teams-messaging-extension"></a><span data-ttu-id="573b9-104">正在设计你的 Microsoft 团队消息扩展</span><span class="sxs-lookup"><span data-stu-id="573b9-104">Designing your Microsoft Teams messaging extension</span></span>

<span data-ttu-id="573b9-105">邮件扩展是用于插入应用程序内容或在不离开对话的情况下对邮件进行操作的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="573b9-105">Messaging extensions are shortcuts for inserting app content or acting on a message without navigating away from the conversation.</span></span>

<span data-ttu-id="573b9-106">若要指导您的应用程序设计，以下信息介绍并说明了用户如何在团队中添加、使用和管理邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="573b9-106">To guide your app design, the following information describes and illustrates how people can add, use, and manage messaging extensions in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="573b9-107">Microsoft 团队 UI 工具包</span><span class="sxs-lookup"><span data-stu-id="573b9-107">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="573b9-108">您可以在 Microsoft 团队 UI 工具包中找到全面的邮件扩展设计准则，包括您可以根据需要获取和修改的元素。</span><span class="sxs-lookup"><span data-stu-id="573b9-108">You can find comprehensive messaging extension design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="573b9-109"> (Figma) 获取 Microsoft 团队 UI 工具包 </span><span class="sxs-lookup"><span data-stu-id="573b9-109">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-messaging-extension"></a><span data-ttu-id="573b9-110">添加消息扩展</span><span class="sxs-lookup"><span data-stu-id="573b9-110">Add a messaging extension</span></span>

<span data-ttu-id="573b9-111">您可以在以下团队上下文中添加消息扩展：</span><span class="sxs-lookup"><span data-stu-id="573b9-111">You can add a messaging extension in the following Teams contexts:</span></span>

* <span data-ttu-id="573b9-112">从团队存储 (AppSource) 。</span><span class="sxs-lookup"><span data-stu-id="573b9-112">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="573b9-113">在频道、聊天或会议 (之前、在 "撰写" 框附近) 的前后。</span><span class="sxs-lookup"><span data-stu-id="573b9-113">In a channel, chat, or meeting (before, during, and after) near the compose box.</span></span> <span data-ttu-id="573b9-114">值得注意的是，如果在其中一个位置添加了邮件扩展插件，则只有您可以在该上下文中使用它。</span><span class="sxs-lookup"><span data-stu-id="573b9-114">It's worth noting if you add a messaging extension in one of these places, only you can use it in that context.</span></span>

<span data-ttu-id="573b9-115">下面的示例展示了如何在频道中添加邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="573b9-115">The following example shows how you add a messaging extension in a channel.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/add-in-channel.png" alt-text="示例演示如何在频道中的撰写框附近添加消息扩展。" border="false":::

## <a name="set-up-a-messaging-extension"></a><span data-ttu-id="573b9-117">设置邮件扩展</span><span class="sxs-lookup"><span data-stu-id="573b9-117">Set up a messaging extension</span></span>

<span data-ttu-id="573b9-118">身份验证不是强制性的，但是，如果您的应用程序类似于票证跟踪工具，则可能需要用户登录才能使用邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="573b9-118">Authentication isn't mandatory, but if your app is something like a ticket tracking tool, you may need people to sign in to use the messaging extension.</span></span>

<span data-ttu-id="573b9-119">为了实现跨团队应用的一致性，无法自定义登录屏幕。</span><span class="sxs-lookup"><span data-stu-id="573b9-119">For consistency across Teams apps, you can't customize the sign-in screen.</span></span> <span data-ttu-id="573b9-120">如果使用单一登录 (SSO) 身份验证，则会自动登录用户。</span><span class="sxs-lookup"><span data-stu-id="573b9-120">If you use single sign-on (SSO) authentication, users are signed in automatically.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/set-up.png" alt-text="示例显示带有登录按钮的邮件扩展安装程序屏幕。" border="false":::

## <a name="types-of-messaging-extensions"></a><span data-ttu-id="573b9-122">邮件扩展类型</span><span class="sxs-lookup"><span data-stu-id="573b9-122">Types of messaging extensions</span></span>

<span data-ttu-id="573b9-123">邮件扩展可以包含搜索命令、操作命令或同时具有这两者。</span><span class="sxs-lookup"><span data-stu-id="573b9-123">Messaging extensions can have search commands, action commands, or both.</span></span> <span data-ttu-id="573b9-124">您的命令取决于您的应用程序的功能以及这些功能在团队使用案例中的工作方式。</span><span class="sxs-lookup"><span data-stu-id="573b9-124">Your commands depend on your app's features and how those fit within Teams use cases.</span></span>

### <a name="search-commands"></a><span data-ttu-id="573b9-125">搜索命令</span><span class="sxs-lookup"><span data-stu-id="573b9-125">Search commands</span></span>

<span data-ttu-id="573b9-126">使用搜索命令，用户可以使用您的邮件扩展来快速查找外部内容并将其插入到邮件中。</span><span class="sxs-lookup"><span data-stu-id="573b9-126">With search commands, people can use your messaging extension to quickly find external content and insert into a message.</span></span> <span data-ttu-id="573b9-127">搜索命令通常在 "撰写" 框中可用。</span><span class="sxs-lookup"><span data-stu-id="573b9-127">Search commands are commonly made available in the compose box.</span></span> <span data-ttu-id="573b9-128">例如，您可以通过共享一小部分内容来启动或添加讨论，而无需离开团队。</span><span class="sxs-lookup"><span data-stu-id="573b9-128">For example, you can start or add to a discussion by sharing a piece of content—without ever leaving Teams.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-command-type.png" alt-text="示例显示从 &quot;撰写&quot; 框启动的基于搜索的邮件扩展插件。" border="false":::

#### <a name="compose-box-layout-options"></a><span data-ttu-id="573b9-130">组合框版式选项</span><span class="sxs-lookup"><span data-stu-id="573b9-130">Compose box layout options</span></span>

<span data-ttu-id="573b9-131">您可以使用一些选项来显示邮件扩展搜索结果，包括 [列表和网格视图](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests)。</span><span class="sxs-lookup"><span data-stu-id="573b9-131">You have some options for displaying messaging extension search results, including [list and grid views](../../messaging-Ask about extensions/how-to/search-commands/respond-to-search.md#respond-to-user-requests).</span></span>

:::image type="content" source="../../assets/images/messaging-extension/search-result-layout.png" alt-text="显示邮件扩展搜索结果的布局选项的插图。" border="false":::

### <a name="action-commands"></a><span data-ttu-id="573b9-133">操作命令</span><span class="sxs-lookup"><span data-stu-id="573b9-133">Action commands</span></span>

<span data-ttu-id="573b9-134">操作命令使用户能够触发操作并处理团队内的外部服务中的请求。</span><span class="sxs-lookup"><span data-stu-id="573b9-134">Action commands allow people to trigger actions and process requests in external services within Teams.</span></span> <span data-ttu-id="573b9-135">例如，如果您的应用程序跟踪订单，则用户可以使用同事的邮件中的内容直接在聊天中创建新的订单。</span><span class="sxs-lookup"><span data-stu-id="573b9-135">For example, if your app tracks orders, a user could create a new order using the contents of a colleague’s message from right inside their chat.</span></span>

<span data-ttu-id="573b9-136">基于操作的邮件扩展通常要求用户在模式中填写表单或某些其他类型的配置。</span><span class="sxs-lookup"><span data-stu-id="573b9-136">Action-based messaging extensions frequently require users to complete a form or some other kind of configuration within a modal.</span></span> <span data-ttu-id="573b9-137">您可以使用 [任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)创建这些体验。</span><span class="sxs-lookup"><span data-stu-id="573b9-137">You can create these experiences with [task modules](../../task-modules-and-cards/task-modules/design-teams-task-modules.md).</span></span>

## <a name="open-a-messaging-extension"></a><span data-ttu-id="573b9-138">打开消息扩展</span><span class="sxs-lookup"><span data-stu-id="573b9-138">Open a messaging extension</span></span>

<span data-ttu-id="573b9-139">"撰写" 框和 "邮件/公告" 是人们使用邮件扩展的主要上下文。</span><span class="sxs-lookup"><span data-stu-id="573b9-139">The compose box and messages/posts are the primary contexts where people use messaging extensions.</span></span>

### <a name="from-the-compose-box"></a><span data-ttu-id="573b9-140">从 "撰写" 框</span><span class="sxs-lookup"><span data-stu-id="573b9-140">From the compose box</span></span>

<span data-ttu-id="573b9-141">添加后，用户可以通过选择 "撰写" 框下的应用图标打开您的邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="573b9-141">Once added, users can open your messaging extension by selecting your app icon below the compose box.</span></span> <span data-ttu-id="573b9-142">在此示例中，扩展包含搜索和操作命令。</span><span class="sxs-lookup"><span data-stu-id="573b9-142">In this example, the extension has search and action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-compose-box.png" alt-text="示例说明如何从 &quot;撰写&quot; 框中打开消息扩展。" border="false":::

### <a name="from-a-chat-message-or-channel-post"></a><span data-ttu-id="573b9-144">从聊天消息或频道帖子</span><span class="sxs-lookup"><span data-stu-id="573b9-144">From a chat message or channel post</span></span>

添加后，用户可以选择 **More** :::image type="icon" source="../../assets/icons/teams-client-more.png"::: 聊天消息或频道帖子上的更多图标以查找您的扩展的操作命令。 <span data-ttu-id="573b9-146">您的扩展可能会列在 "基于使用情况的 **更多操作** " 下。</span><span class="sxs-lookup"><span data-stu-id="573b9-146">Your extension may be listed under **More actions** based on usage.</span></span>

#### <a name="chat-message"></a><span data-ttu-id="573b9-147">聊天消息</span><span class="sxs-lookup"><span data-stu-id="573b9-147">Chat message</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-chat-message.png" alt-text="示例说明如何从聊天消息中打开消息扩展。" border="false":::

#### <a name="channel-post"></a><span data-ttu-id="573b9-149">频道帖子</span><span class="sxs-lookup"><span data-stu-id="573b9-149">Channel post</span></span>

:::image type="content" source="../../assets/images/messaging-extension/open-from-channel-post.png" alt-text="示例说明如何从频道公告中打开邮件扩展插件。" border="false":::

## <a name="use-a-messaging-extension"></a><span data-ttu-id="573b9-151">使用消息扩展</span><span class="sxs-lookup"><span data-stu-id="573b9-151">Use a messaging extension</span></span>

<span data-ttu-id="573b9-152">以下方案展示了人们使用邮件扩展的主要方式。</span><span class="sxs-lookup"><span data-stu-id="573b9-152">The following scenarios show the primary ways people use messaging extensions.</span></span>

### <a name="insert-content-into-a-message"></a><span data-ttu-id="573b9-153">将内容插入邮件</span><span class="sxs-lookup"><span data-stu-id="573b9-153">Insert content into a message</span></span>

<span data-ttu-id="573b9-154">**1. 选择邮件扩展**。</span><span class="sxs-lookup"><span data-stu-id="573b9-154">**1. Select a messaging extension**.</span></span> <span data-ttu-id="573b9-155">用户可以从 "撰写" 框中搜索要共享的内容。</span><span class="sxs-lookup"><span data-stu-id="573b9-155">Users can search for the content they want to share from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-search.png" alt-text="示例显示用户从 &quot;撰写&quot; 框中搜索要插入的内容。" border="false":::

<span data-ttu-id="573b9-157">**2. 插入内容**。</span><span class="sxs-lookup"><span data-stu-id="573b9-157">**2. Insert content**.</span></span> <span data-ttu-id="573b9-158">发布后，其他人可以答复或选择内容以查看您的应用程序中的详细信息。</span><span class="sxs-lookup"><span data-stu-id="573b9-158">Once posted, others can reply or select the content to see more information in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-content-posted.png" alt-text="示例演示了用户将内容发布到频道对话中。" border="false":::

### <a name="take-action-on-a-message"></a><span data-ttu-id="573b9-160">对邮件执行操作</span><span class="sxs-lookup"><span data-stu-id="573b9-160">Take action on a message</span></span>

<span data-ttu-id="573b9-161">**1. 选择邮件扩展**。</span><span class="sxs-lookup"><span data-stu-id="573b9-161">**1. Select a messaging extension**.</span></span> <span data-ttu-id="573b9-162">您的应用程序可以包含一个或多个操作命令。</span><span class="sxs-lookup"><span data-stu-id="573b9-162">Your app can include one or more action commands.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/select-action-command.png" alt-text="示例显示用户选择邮件扩展操作命令。" border="false":::

<span data-ttu-id="573b9-164">**2. 完成操作**。</span><span class="sxs-lookup"><span data-stu-id="573b9-164">**2. Complete the action**.</span></span> <span data-ttu-id="573b9-165">您的应用程序可以接收和处理由邮件操作发送的任何内容或数据。</span><span class="sxs-lookup"><span data-stu-id="573b9-165">Your app can receive and process any content or data sent by the message action.</span></span> <span data-ttu-id="573b9-166">这样，用户就可以继续在对话中，以下示例不会考虑直接在应用程序中输入信息。</span><span class="sxs-lookup"><span data-stu-id="573b9-166">This allows users to remain in their conversation and, the following example, not worry about entering information directly in your app.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/complete-action-command.png" alt-text="示例显示用户从 &quot;撰写&quot; 框中搜索要插入的内容。" border="false":::

### <a name="preview-links"></a><span data-ttu-id="573b9-168">预览链接</span><span class="sxs-lookup"><span data-stu-id="573b9-168">Preview links</span></span>

<span data-ttu-id="573b9-169">邮件扩展还允许您将格式可识别的 URL 中的格式链接插入邮件 (此功能称为 [link unfurling](../../messaging-extensions/how-to/link-unfurling.md)。 ) </span><span class="sxs-lookup"><span data-stu-id="573b9-169">Messaging extensions also allow you to insert rich links from a recognized URL into a message (this capability is called [link unfurling](../../messaging-extensions/how-to/link-unfurling.md).)</span></span>

<span data-ttu-id="573b9-170">1. 在 "撰写" 框中 **粘贴可识别的链接**。</span><span class="sxs-lookup"><span data-stu-id="573b9-170">**1. Paste a recognized link** in the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/paste-preview-link.png" alt-text="示例显示用户在 &quot;compost&quot; 框中粘贴链接。" border="false":::

<span data-ttu-id="573b9-172">**2. 插入内容**。</span><span class="sxs-lookup"><span data-stu-id="573b9-172">**2. Insert content**.</span></span> <span data-ttu-id="573b9-173">如果您的应用程序识别了 "撰写" 框中的 URL，则会将该链接呈现为可提供 web 内容的内容丰富预览的卡片。</span><span class="sxs-lookup"><span data-stu-id="573b9-173">If your app recognizes the URL in the compose box, it renders the link as a card that provides a content-rich preview of the web content.</span></span> <span data-ttu-id="573b9-174"> (有关详细信息，请参阅 [自适应卡片设计指南](../../task-modules-and-cards/cards/design-effective-cards.md) 。 ) </span><span class="sxs-lookup"><span data-stu-id="573b9-174">(See [Adaptive Cards design guidelines](../../task-modules-and-cards/cards/design-effective-cards.md) for more information.)</span></span>

:::image type="content" source="../../assets/images/messaging-extension/insert-preview-link.png" alt-text="示例显示了由于应用程序识别的 URL，在撰写框中包含一些丰富的内容。" border="false":::

## <a name="manage-a-messaging-extension"></a><span data-ttu-id="573b9-176">管理邮件扩展</span><span class="sxs-lookup"><span data-stu-id="573b9-176">Manage a messaging extension</span></span>

<span data-ttu-id="573b9-177">通过右键单击您的图标，用户可以固定、删除或配置您的邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="573b9-177">By right clicking your icon, users can pin, remove, or configure your messaging extension.</span></span>

## <a name="anatomy"></a><span data-ttu-id="573b9-178">解析</span><span class="sxs-lookup"><span data-stu-id="573b9-178">Anatomy</span></span>

### <a name="messaging-extension-in-the-compose-box"></a><span data-ttu-id="573b9-179">撰写框中的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="573b9-179">Messaging extension in the compose box</span></span>

<span data-ttu-id="573b9-180">下面的示例是一个通过撰写框打开的邮件扩展插件。</span><span class="sxs-lookup"><span data-stu-id="573b9-180">The following example is a messaging extension opened from the compose box.</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-compose.png" alt-text="该图显示了撰写框中的邮件扩展的 UI 解析。" border="false":::

|<span data-ttu-id="573b9-182">计数器</span><span class="sxs-lookup"><span data-stu-id="573b9-182">Counter</span></span>|<span data-ttu-id="573b9-183">说明</span><span class="sxs-lookup"><span data-stu-id="573b9-183">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="573b9-184">1</span><span class="sxs-lookup"><span data-stu-id="573b9-184">1</span></span>|<span data-ttu-id="573b9-185">**应用徽标**：应用徽标的颜色图标。</span><span class="sxs-lookup"><span data-stu-id="573b9-185">**App logo**: Color icon of your app logo.</span></span>|
|<span data-ttu-id="573b9-186">2 </span><span class="sxs-lookup"><span data-stu-id="573b9-186">2</span></span>|<span data-ttu-id="573b9-187">**应用程序名称**：应用程序的完整名称。</span><span class="sxs-lookup"><span data-stu-id="573b9-187">**App name**: Full name of your app.</span></span>|
|<span data-ttu-id="573b9-188">3 </span><span class="sxs-lookup"><span data-stu-id="573b9-188">3</span></span>|<span data-ttu-id="573b9-189">**操作命令菜单图标 (可选)**：如果指定任何) ，则打开邮件扩展 (的操作命令列表。</span><span class="sxs-lookup"><span data-stu-id="573b9-189">**Action commands menu icon (optional)**: Opens a list of action commands for your messaging extension (if you specify any).</span></span>
|<span data-ttu-id="573b9-190">4 </span><span class="sxs-lookup"><span data-stu-id="573b9-190">4</span></span>|<span data-ttu-id="573b9-191">**搜索框**：允许用户查找他们想要插入的应用内容。</span><span class="sxs-lookup"><span data-stu-id="573b9-191">**Search box**: Allows users to find app content they want to insert.</span></span>|
|<span data-ttu-id="573b9-192">5 </span><span class="sxs-lookup"><span data-stu-id="573b9-192">5</span></span>|<span data-ttu-id="573b9-193">**选项卡菜单 (可选)**：提供多个内容类别。</span><span class="sxs-lookup"><span data-stu-id="573b9-193">**Tab menu (optional)**: Provides multiple content categories.</span></span>|
|<span data-ttu-id="573b9-194">6 </span><span class="sxs-lookup"><span data-stu-id="573b9-194">6</span></span>|<span data-ttu-id="573b9-195">**操作命令菜单 (可选)**：如果指定任何) ，则显示操作命令的列表 (。</span><span class="sxs-lookup"><span data-stu-id="573b9-195">**Action commands menu (optional)**: Displays list of action commands (if you specify any).</span></span>|
|<span data-ttu-id="573b9-196">7 </span><span class="sxs-lookup"><span data-stu-id="573b9-196">7</span></span>|<span data-ttu-id="573b9-197">**应用内容**：主要用于显示搜索结果。</span><span class="sxs-lookup"><span data-stu-id="573b9-197">**App content**: Primarily to display search results.</span></span> <span data-ttu-id="573b9-198">下面的示例使用的是列表布局 (网格布局是另一个选项) 。</span><span class="sxs-lookup"><span data-stu-id="573b9-198">The example here is using the list layout (grid layout is another option).</span></span>|
|<span data-ttu-id="573b9-199">8 </span><span class="sxs-lookup"><span data-stu-id="573b9-199">8</span></span>|<span data-ttu-id="573b9-200">**应用徽标**：应用徽标的大纲图标。</span><span class="sxs-lookup"><span data-stu-id="573b9-200">**App logo**: Outline icon of your app logo.</span></span>|

### <a name="messaging-extension-management-menu"></a><span data-ttu-id="573b9-201">邮件扩展管理菜单</span><span class="sxs-lookup"><span data-stu-id="573b9-201">Messaging extension management menu</span></span>

:::image type="content" source="../../assets/images/messaging-extension/anatomy-management-menu.png" alt-text="显示邮件扩展管理菜单的 UI 解析的图示。" border="false":::

|<span data-ttu-id="573b9-203">计数器</span><span class="sxs-lookup"><span data-stu-id="573b9-203">Counter</span></span>|<span data-ttu-id="573b9-204">说明</span><span class="sxs-lookup"><span data-stu-id="573b9-204">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="573b9-205">1</span><span class="sxs-lookup"><span data-stu-id="573b9-205">1</span></span>|<span data-ttu-id="573b9-206">**取消固定**：如果用户已固定你的应用程序，则为可用。</span><span class="sxs-lookup"><span data-stu-id="573b9-206">**Unpin**: Available if the user has pinned your app.</span></span>|
|<span data-ttu-id="573b9-207">2 </span><span class="sxs-lookup"><span data-stu-id="573b9-207">2</span></span>|<span data-ttu-id="573b9-208">**Remove**：从频道、聊天或会议中删除邮件分机号码。</span><span class="sxs-lookup"><span data-stu-id="573b9-208">**Remove**: Removes the messaging extension from the channel, chat, or meeting.</span></span>|

## <a name="best-practices"></a><span data-ttu-id="573b9-209">最佳做法</span><span class="sxs-lookup"><span data-stu-id="573b9-209">Best practices</span></span>

### <a name="setup-and-general-usage"></a><span data-ttu-id="573b9-210">设置和常规用法</span><span class="sxs-lookup"><span data-stu-id="573b9-210">Setup and general usage</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-do.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="do-integrate-with-single-sign-on"></a><span data-ttu-id="573b9-212">操作：与单一登录集成</span><span class="sxs-lookup"><span data-stu-id="573b9-212">Do: Integrate with single-sign on</span></span>

<span data-ttu-id="573b9-213">SSO 使登录过程更简单、更快速且安全。</span><span class="sxs-lookup"><span data-stu-id="573b9-213">SSO makes the sign-in process easier, faster, and secure.</span></span> <span data-ttu-id="573b9-214">此外，如果用户已登录到您的个人应用程序，他们也无需再次登录以访问邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="573b9-214">Also, if a user has already signed in to your personal app, they don’t have to also sign in again to access the messaging extension.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/setup-dont.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="dont-take-users-away-from-the-conversation"></a><span data-ttu-id="573b9-216">请勿：使用户离开对话</span><span class="sxs-lookup"><span data-stu-id="573b9-216">Don't: Take users away from the conversation</span></span>

<span data-ttu-id="573b9-217">邮件扩展是指应减少上下文切换的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="573b9-217">Messaging extensions are shortcuts that are supposed reduce context switching.</span></span> <span data-ttu-id="573b9-218">例如，您的扩展不应将用户定向到团队外部的网页。</span><span class="sxs-lookup"><span data-stu-id="573b9-218">Your extension should not, for example, direct users to a webpage outside Teams.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="do-highlight-your-messaging-extension"></a><span data-ttu-id="573b9-219">Do：突出显示你的消息扩展</span><span class="sxs-lookup"><span data-stu-id="573b9-219">Do: Highlight your messaging extension</span></span>

<span data-ttu-id="573b9-220">邮件扩展功能并不总是很容易找到。</span><span class="sxs-lookup"><span data-stu-id="573b9-220">Messaging extensions aren't always easy to find.</span></span> <span data-ttu-id="573b9-221">包括如何在应用程序详细信息页中使用它的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="573b9-221">Include screenshots of how to use it in your app details page.</span></span> <span data-ttu-id="573b9-222">如果您的应用程序还包含一个 bot，则可以在 "机器人欢迎" 教程中包括邮件扩展帮助文档。</span><span class="sxs-lookup"><span data-stu-id="573b9-222">If your app also includes a bot, you can include messaging extension help documentation in a bot welcome tour.</span></span>

### <a name="templating"></a><span data-ttu-id="573b9-223">模板</span><span class="sxs-lookup"><span data-stu-id="573b9-223">Templating</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-do.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="do-let-teams-handle-some-of-the-design-work-if-possible"></a><span data-ttu-id="573b9-225">操作：让团队能够处理一些设计工作（如果可能）</span><span class="sxs-lookup"><span data-stu-id="573b9-225">Do: Let Teams handle some of the design work if possible</span></span>

<span data-ttu-id="573b9-226">如果对用例有意义，请考虑创建基于搜索的邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="573b9-226">If it makes sense for your use cases, consider creating a search-based messaging extension.</span></span> <span data-ttu-id="573b9-227">团队使用内置主题和可访问性呈现这些类型的扩展。</span><span class="sxs-lookup"><span data-stu-id="573b9-227">Teams renders these types of extensions with built-in theming and accessibility.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/templating-dont.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="dont-embed-your-entire-app-in-a-task-module"></a><span data-ttu-id="573b9-229">请勿：在任务模块中嵌入整个应用程序</span><span class="sxs-lookup"><span data-stu-id="573b9-229">Don't: Embed your entire app in a task module</span></span>

<span data-ttu-id="573b9-230">如果邮件扩展需要操作命令，请保持任务模块简单并仅显示完成该操作所需的组件。</span><span class="sxs-lookup"><span data-stu-id="573b9-230">If your messaging extension requires action commands, keep the task module simple and display only the components required to complete the action.</span></span>

   :::column-end:::
:::row-end:::

### <a name="theming"></a><span data-ttu-id="573b9-231">主题</span><span class="sxs-lookup"><span data-stu-id="573b9-231">Theming</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-do.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="do-take-advantage-of-teams-color-tokens"></a><span data-ttu-id="573b9-233">Do：利用团队颜色令牌</span><span class="sxs-lookup"><span data-stu-id="573b9-233">Do: Take advantage of Teams color tokens</span></span>

<span data-ttu-id="573b9-234">每个团队主题都有自己的配色方案。</span><span class="sxs-lookup"><span data-stu-id="573b9-234">Each Teams theme has its own color scheme.</span></span> <span data-ttu-id="573b9-235">若要自动处理主题更改，请在设计中使用 <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank"> (熟知的 UI) 的颜色标记 </a> 。</span><span class="sxs-lookup"><span data-stu-id="573b9-235">To handle theme changes automatically, use <a href="https://fluentsite.z22.web.core.windows.net/0.51.3/colors#color-scheme" target="_blank">color tokens (Fluent UI)</a> in your design.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/theming-dont.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="dont-hard-code-color-values"></a><span data-ttu-id="573b9-237">不：硬编码颜色值</span><span class="sxs-lookup"><span data-stu-id="573b9-237">Don't: Hard code color values</span></span>

<span data-ttu-id="573b9-238">如果您不使用团队颜色令牌，则设计的可伸缩性较小并需要更多时间来管理。</span><span class="sxs-lookup"><span data-stu-id="573b9-238">If you don't use Teams color tokens, your designs will be less scalable and take more time to manage.</span></span>

   :::column-end:::
:::row-end:::

### <a name="actions"></a><span data-ttu-id="573b9-239">操作</span><span class="sxs-lookup"><span data-stu-id="573b9-239">Actions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-do.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="do-include-action-commands-that-make-sense-in-context"></a><span data-ttu-id="573b9-241">操作：包括在上下文中有意义的操作命令</span><span class="sxs-lookup"><span data-stu-id="573b9-241">Do: Include action commands that make sense in context</span></span>

<span data-ttu-id="573b9-242">邮件操作应与用户所关注的内容相关。</span><span class="sxs-lookup"><span data-stu-id="573b9-242">Message actions should relate to what a user is looking at.</span></span> <span data-ttu-id="573b9-243">例如，向用户提供用于使用某人的帖子中的文本创建问题或工作项的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="573b9-243">For example, provide users a shortcut for creating an issue or work item using the text in someone’s post.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/messaging-extension/action-commands-dont.png" alt-text="显示邮件扩展最佳实践的示例。" border="false":::

#### <a name="dont-include-actions-commands-that-arent-contextual"></a><span data-ttu-id="573b9-245">请勿：包含不是上下文的操作命令</span><span class="sxs-lookup"><span data-stu-id="573b9-245">Don't: Include actions commands that aren't contextual</span></span>

<span data-ttu-id="573b9-246">**查看你的仪表板** 的消息操作可能似乎与大多数对话断开连接。</span><span class="sxs-lookup"><span data-stu-id="573b9-246">A message action to **View your dashboard** would probably seem disconnected from most conversations.</span></span>

   :::column-end:::
:::row-end:::

### <a name="searches"></a><span data-ttu-id="573b9-247">搜寻</span><span class="sxs-lookup"><span data-stu-id="573b9-247">Searches</span></span>

#### <a name="do-show-search-results-while-typing"></a><span data-ttu-id="573b9-248">操作：键入时显示搜索结果</span><span class="sxs-lookup"><span data-stu-id="573b9-248">Do: Show search results while typing</span></span>

<span data-ttu-id="573b9-249">在用户键入时提供建议的搜索结果。</span><span class="sxs-lookup"><span data-stu-id="573b9-249">Provide suggested search results while users type.</span></span> <span data-ttu-id="573b9-250">他们可能会以最少的字符数更快地找到所需内容。</span><span class="sxs-lookup"><span data-stu-id="573b9-250">They may find the content they need faster with minimal amount of characters.</span></span>

#### <a name="dont-require-users-to-submit-a-query"></a><span data-ttu-id="573b9-251">不：要求用户提交查询</span><span class="sxs-lookup"><span data-stu-id="573b9-251">Don't: Require users to submit a query</span></span>

<span data-ttu-id="573b9-252">您可以让用户按下某个键或选择一个按钮以将查询发送到您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="573b9-252">You can make users press a key or select a button to send queries to your app.</span></span> <span data-ttu-id="573b9-253">虽然您的应用服务服务可能更简单，但用户可能会感到困惑，他们在键入时不会看到实时搜索结果。</span><span class="sxs-lookup"><span data-stu-id="573b9-253">While that may be easier on your app services service, people may be confused that they're not seeing real-time search results as they type.</span></span>

#### <a name="do-consider-zero-term-queries"></a><span data-ttu-id="573b9-254">操作：考虑零期限的查询</span><span class="sxs-lookup"><span data-stu-id="573b9-254">Do: Consider zero-term queries</span></span>

<span data-ttu-id="573b9-255">例如，用户在搜索框中写入任何内容之前，将显示上次在您的应用程序上查看的内容。</span><span class="sxs-lookup"><span data-stu-id="573b9-255">For example, before a user writes anything in the search box, display what they last viewed on your app.</span></span> <span data-ttu-id="573b9-256">他们可能希望将该内容插入到其对话中。</span><span class="sxs-lookup"><span data-stu-id="573b9-256">It's possible that they want to insert that content into their conversation.</span></span>

## <a name="validate-your-design"></a><span data-ttu-id="573b9-257">验证设计</span><span class="sxs-lookup"><span data-stu-id="573b9-257">Validate your design</span></span>

<span data-ttu-id="573b9-258">如果计划将应用程序发布到 AppSource，则应了解通常会在提交期间导致应用程序失败的设计问题。</span><span class="sxs-lookup"><span data-stu-id="573b9-258">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="573b9-259">检查设计验证准则</span><span class="sxs-lookup"><span data-stu-id="573b9-259">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
