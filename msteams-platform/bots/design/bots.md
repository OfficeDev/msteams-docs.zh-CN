---
title: 正在设计你的 bot
description: 了解如何设计团队 bot 并获取 Microsoft 团队 UI 工具包。
author: heath-hamilton
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: d1a7470f4986de22ecca7071823b620cb0234abb
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605390"
---
# <a name="designing-your-microsoft-teams-bot"></a><span data-ttu-id="1c2a8-103">正在设计你的 Microsoft 团队 bot</span><span class="sxs-lookup"><span data-stu-id="1c2a8-103">Designing your Microsoft Teams bot</span></span>

<span data-ttu-id="1c2a8-104">Bot 是执行一组特定任务的会话中应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-104">Bots are conversational apps that perform a specific set of tasks.</span></span> <span data-ttu-id="1c2a8-105">根据 <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot 框架</a>，bot 与用户进行通信，响应他们的问题，并主动通知他们发生更改和其他事件。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-105">Based on the <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, bots communicate with users, respond to their questions, and proactively notify them about changes and other events.</span></span> <span data-ttu-id="1c2a8-106">这是一种很好的方法。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-106">They're a great way to reach out.</span></span>

<span data-ttu-id="1c2a8-107">若要指导您的应用程序设计，以下信息介绍并说明了用户如何在团队中添加、使用和管理 bot。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-107">To guide your app design, the following information describes and illustrates how people can add, use, and manage bots in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="1c2a8-108">Microsoft 团队 UI 工具包</span><span class="sxs-lookup"><span data-stu-id="1c2a8-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="1c2a8-109">您可以在 Microsoft 团队 UI 工具包中找到更全面的 bot 设计指南，包括您可以根据需要获取和修改的元素。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-109">You can find more comprehensive bot design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1c2a8-110"> (Figma) 获取 Microsoft 团队 UI 工具包 </span><span class="sxs-lookup"><span data-stu-id="1c2a8-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a><span data-ttu-id="1c2a8-111">添加 bot</span><span class="sxs-lookup"><span data-stu-id="1c2a8-111">Add a bot</span></span>

<span data-ttu-id="1c2a8-112">聊天、频道和个人应用中提供了 bot。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-112">Bots are available in chats, channels, and personal apps.</span></span> <span data-ttu-id="1c2a8-113">您可以通过以下方式之一添加机器人：</span><span class="sxs-lookup"><span data-stu-id="1c2a8-113">You can add a bot one of the following ways:</span></span>

* <span data-ttu-id="1c2a8-114">从团队存储 (AppSource) 。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-114">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="1c2a8-115">通过在工作组左侧选择 " **更多** " 图标来使用应用浮出控件。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-115">Using the app flyout by selecting the **More** icon on the left side of Teams.</span></span>
* <span data-ttu-id="1c2a8-116">在 "新聊天" 或 "撰写" 框中使用 @mention (下面的示例演示如何在组聊天) 中执行此操作。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-116">With an @mention in the new chat or compose box (the following example shows how you can do this in a group chat).</span></span>

:::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="示例演示如何使用 @mention 在组中添加机器人。" border="false":::

## <a name="introduce-a-bot"></a><span data-ttu-id="1c2a8-118">引入机器人</span><span class="sxs-lookup"><span data-stu-id="1c2a8-118">Introduce a bot</span></span>

<span data-ttu-id="1c2a8-119">你的 bot 会自行引入并描述它可以执行的操作，这一点非常重要。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-119">It’s critical that your bot introduces itself and describes what it can do.</span></span> <span data-ttu-id="1c2a8-120">此初始 exchange 可帮助用户了解如何使用 bot，找出它的局限性，最重要的是，让他们能够轻松地与之进行交互。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-120">This initial exchange helps people understand what to do with the bot, find out its limitations and, most importantly, get comfortable interacting with it.</span></span>

### <a name="welcome-message-in-a-one-on-one-chat"></a><span data-ttu-id="1c2a8-121">一对一聊天中的欢迎消息</span><span class="sxs-lookup"><span data-stu-id="1c2a8-121">Welcome message in a one-on-one chat</span></span>

<span data-ttu-id="1c2a8-122">在个人上下文中，欢迎邮件设置你的 bot 的语气。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-122">In personal contexts, welcome messages set your bot's tone.</span></span> <span data-ttu-id="1c2a8-123">该邮件包含问候语、bot 可以执行的操作以及有关如何在 (进行交互的一些建议（例如，"请尝试询问我 ..."） ) 。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-123">The message includes a greeting, what the bot can do, and some suggestions for how to interact (for example, “Try asking me about …”).</span></span> <span data-ttu-id="1c2a8-124">如果可能，这些建议应返回存储的响应，而无需登录。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-124">If possible, these suggestions should return stored responses without having to sign in.</span></span>

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="示例显示了个人应用程序中的 bot 简介。" border="false":::

### <a name="introductions-in-group-chats-and-channels"></a><span data-ttu-id="1c2a8-126">群研讨和频道中的简介</span><span class="sxs-lookup"><span data-stu-id="1c2a8-126">Introductions in group chats and channels</span></span>

<span data-ttu-id="1c2a8-127">你的 bot 的简介与个人上下文 (（如个人应用) ）相比，在组聊天和频道中略有不同。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-127">Your bot's introduction should be slightly little different in group chats and channels compared to a personal context (like a personal app).</span></span> <span data-ttu-id="1c2a8-128">在实际生活中，如果你输入的会议室完全为人，则为你将自行引入，而不是欢迎大家已经在那里的人。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-128">In real life, if you entered a room full of people; you’d introduce yourself instead of welcoming everyone who’s already there.</span></span> <span data-ttu-id="1c2a8-129">将这种想法引入到你的 bot 设计中。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-129">Carry that thinking into your bot design.</span></span>

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="示例显示了协作上下文中的 bot 简介。" border="false":::

### <a name="bot-authentication-with-single-sign-on"></a><span data-ttu-id="1c2a8-131">单一登录的 Bot 身份验证</span><span class="sxs-lookup"><span data-stu-id="1c2a8-131">Bot authentication with single sign-on</span></span>

<span data-ttu-id="1c2a8-132">当某个人将邮件发送到 bot 时，可能需要登录才能使用其所有功能。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-132">When a person messages a bot, sign in may be required use all its features.</span></span> <span data-ttu-id="1c2a8-133">您可以使用单一登录 (SSO) 简化身份验证过程。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-133">You can simplify the authentication process using single sign-on (SSO).</span></span>

<span data-ttu-id="1c2a8-134">别忘了：在机器人命令菜单中 (**我可以执行哪些操作？**) ，还必须提供命令来注销。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-134">Don’t forget: In the bot command menu (**What can I do?**), you must also provide a command to sign out.</span></span>

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="示例显示了带有登录按钮的 bot。" border="false":::

### <a name="tours"></a><span data-ttu-id="1c2a8-136">漫游</span><span class="sxs-lookup"><span data-stu-id="1c2a8-136">Tours</span></span>

<span data-ttu-id="1c2a8-137">您可以包含欢迎邮件的教程，如果 bot 响应的是 "帮助" 命令之类的内容。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-137">You can include a tour with welcome messages and if the bot responds to something like a “help” command.</span></span> <span data-ttu-id="1c2a8-138">教程是描述你的 bot 可以执行的操作的最有效方式。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-138">A tour is the most effective way to describe what your bot can do.</span></span> <span data-ttu-id="1c2a8-139">如果适用，它们也很适合描述应用程序的其他功能 (例如，包括邮件扩展) 的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-139">If applicable, they’re also great for describing your app’s other features (for example, include screenshots of your messaging extension).</span></span>

> [!IMPORTANT]
> <span data-ttu-id="1c2a8-140">无需登录即可访问教程。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-140">Tours should be accessible without having to sign in.</span></span>

#### <a name="one-on-one-chats"></a><span data-ttu-id="1c2a8-141">一对一聊天</span><span class="sxs-lookup"><span data-stu-id="1c2a8-141">One-on-one chats</span></span>

<span data-ttu-id="1c2a8-142">在个人应用程序中，轮播可提供对你的 bot 和你的应用程序的任何其他功能的有效概述。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-142">In a personal app, a carousel can provide an effective overview of your bot and any other features of your app.</span></span> <span data-ttu-id="1c2a8-143">包含按钮鼓励用户尝试使用 bot 命令 (例如， **创建任务**) 。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-143">Including buttons the let users try bot commands is encouraged (for example, **Create a task**).</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="示例显示了一次一对一聊天中的 bot 教程。" border="false":::

#### <a name="channels-and-group-chats"></a><span data-ttu-id="1c2a8-145">频道和组聊天</span><span class="sxs-lookup"><span data-stu-id="1c2a8-145">Channels and group chats</span></span>

<span data-ttu-id="1c2a8-146">在频道和群研讨中，应在模式 (（也称为 [任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) ）中打开一个教程，使其不会中断正在进行的对话。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-146">In channels and group chats, a tour should open in a modal (also known as a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) so it doesn’t interrupt ongoing conversations.</span></span> <span data-ttu-id="1c2a8-147">这还为您提供了为您的演示实现基于角色的视图的选项。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-147">This also gives you the option to implement role-based views for your tour.</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="示例显示频道中的 bot 教程。" border="false":::

## <a name="chat-with-a-bot"></a><span data-ttu-id="1c2a8-149">与 bot 聊天</span><span class="sxs-lookup"><span data-stu-id="1c2a8-149">Chat with a bot</span></span>

<span data-ttu-id="1c2a8-150">Bot 直接集成到团队的消息传递框架中。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-150">Bots integrate directly into Team’s messaging framework.</span></span> <span data-ttu-id="1c2a8-151">用户可以与机器人聊天以获取其问题，或键入命令让 bot 执行一组或一组特定的任务。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-151">Users can chat with a bot to get their questions answered or type commands to have the bot perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="1c2a8-152">Bot 可以通过聊天主动通知用户对你的应用所做的更改或更新。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-152">Bots can proactively notify users about changes or updates to your app via chat.</span></span>

### <a name="chat-with-a-bot-in-different-contexts"></a><span data-ttu-id="1c2a8-153">与不同上下文中的 bot 聊天</span><span class="sxs-lookup"><span data-stu-id="1c2a8-153">Chat with a bot in different contexts</span></span>

<span data-ttu-id="1c2a8-154">您可以在以下上下文中使用 bot：</span><span class="sxs-lookup"><span data-stu-id="1c2a8-154">You can use bots in the following contexts:</span></span>

* <span data-ttu-id="1c2a8-155">**个人应用程序**：在个人应用程序中，bot 具有专用的聊天选项卡。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-155">**Personal apps**: In a personal app, a bot has a dedicated chat tab.</span></span>
* <span data-ttu-id="1c2a8-156">**一对一聊天**：用户可以启动与 bot 的专用对话。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-156">**One-on-one chat**: A user can initiate a private conversation with a bot.</span></span> <span data-ttu-id="1c2a8-157">这与在个人应用程序中使用 bot 的体验相同。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-157">It's the same experience as using a bot in a personal app.</span></span>
* <span data-ttu-id="1c2a8-158">**分组聊天**：用户可以通过 @mentioning bot 与组聊天中的 bot 进行交互。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-158">**Group chat**: People can interact with a bot in a group chat by @mentioning the bot.</span></span>
* <span data-ttu-id="1c2a8-159">**频道**：用户可以与频道中的 bot 进行交互。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-159">**Channel**: People can interact with a bot in a channel.</span></span> <span data-ttu-id="1c2a8-160">通过 @mentioning "撰写" 框中的 bot 名称。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-160">by @mentioning the bot name in the compose box.</span></span> <span data-ttu-id="1c2a8-161">请记住，在此上下文中，bot 可用于整个团队，而不仅仅是通道。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-161">Remember, in this context, the bot is available to the entire team, not just the channel.</span></span>

### <a name="anatomy"></a><span data-ttu-id="1c2a8-162">解析</span><span class="sxs-lookup"><span data-stu-id="1c2a8-162">Anatomy</span></span>

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="示例显示 bot 的结构剖析。" border="false":::

|<span data-ttu-id="1c2a8-164">计数器</span><span class="sxs-lookup"><span data-stu-id="1c2a8-164">Counter</span></span>|<span data-ttu-id="1c2a8-165">说明</span><span class="sxs-lookup"><span data-stu-id="1c2a8-165">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="1c2a8-166">1</span><span class="sxs-lookup"><span data-stu-id="1c2a8-166">1</span></span>|<span data-ttu-id="1c2a8-167">**应用程序名称和图标**</span><span class="sxs-lookup"><span data-stu-id="1c2a8-167">**App name and icon**</span></span>|
|<span data-ttu-id="1c2a8-168">2 </span><span class="sxs-lookup"><span data-stu-id="1c2a8-168">2</span></span>|<span data-ttu-id="1c2a8-169">**"聊天" 选项卡**：打开与你的 bot 对话的空间 (仅适用于个人应用) 。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-169">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="1c2a8-170">3 </span><span class="sxs-lookup"><span data-stu-id="1c2a8-170">3</span></span>|<span data-ttu-id="1c2a8-171">**自定义选项卡**：打开与您的应用程序相关的其他内容。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-171">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="1c2a8-172">4 </span><span class="sxs-lookup"><span data-stu-id="1c2a8-172">4</span></span>|<span data-ttu-id="1c2a8-173">**"关于" 选项卡**：显示有关您的应用程序的基本信息。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-173">**About tab**: Displays basic information about your app.</span></span>|
|<span data-ttu-id="1c2a8-174">5 </span><span class="sxs-lookup"><span data-stu-id="1c2a8-174">5</span></span>|<span data-ttu-id="1c2a8-175">**聊天气泡**： Bot 对话使用团队消息传递框架。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-175">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="1c2a8-176">6 </span><span class="sxs-lookup"><span data-stu-id="1c2a8-176">6</span></span>|<span data-ttu-id="1c2a8-177">**自适应卡片**：如果你的 bot 的响应包含自适应卡片，卡片将占用完整的聊天气泡宽度。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-177">**Adaptive Card**: If your bot’s responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|
|<span data-ttu-id="1c2a8-178">7 </span><span class="sxs-lookup"><span data-stu-id="1c2a8-178">7</span></span>|<span data-ttu-id="1c2a8-179">**命令菜单**：显示你)  (定义的你的 bot 的标准命令。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-179">**Command menu**: Displays your bot's standard commands (defined by you).</span></span>

### <a name="command-menu"></a><span data-ttu-id="1c2a8-180">命令菜单</span><span class="sxs-lookup"><span data-stu-id="1c2a8-180">Command menu</span></span>

<span data-ttu-id="1c2a8-181">命令菜单提供您希望机器人始终响应的单词或短语的列表。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-181">The command menu provides a list of words or phrases you want your bot to always respond to.</span></span> <span data-ttu-id="1c2a8-182">当有人正在使用 bot 时，"命令" 菜单将显示在 "撰写" 框的上方。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-182">The command menu displays above the compose box when someone is conversing with a bot.</span></span> <span data-ttu-id="1c2a8-183">当选中某个命令时，它会插入到邮件中。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-183">When a command is selected, it gets inserted into a message.</span></span>

<span data-ttu-id="1c2a8-184">命令列表应简短。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-184">The list of commands should be brief.</span></span> <span data-ttu-id="1c2a8-185">此菜单仅用于突出显示你的 bot 的主要功能。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-185">The menu is only meant to highlight your bot’s primary features.</span></span> <span data-ttu-id="1c2a8-186">也将命令保持简洁。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-186">Keep commands concise, too.</span></span> <span data-ttu-id="1c2a8-187">例如，创建一个名为 " **帮助** " 的命令，而不 **能帮助我** 吗？</span><span class="sxs-lookup"><span data-stu-id="1c2a8-187">For example, create a command called **Help** instead of **Can you please help me**?</span></span>
<span data-ttu-id="1c2a8-188">无论会话的状态如何，命令菜单都必须始终可用。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-188">The command menu must always be available regardless of the state of the conversation.</span></span>

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="示例显示 bot 的命令菜单。" border="false":::

## <a name="understand-what-people-are-saying"></a><span data-ttu-id="1c2a8-190">了解人们的评价</span><span class="sxs-lookup"><span data-stu-id="1c2a8-190">Understand what people are saying</span></span>

<span data-ttu-id="1c2a8-191">使用同义词库并从尽可能多的不同背景中获取人员，以帮助您生成标准查询的不同解释。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-191">Use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of standard queries.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="显示机器人可能如何解释 &quot;Hello&quot; 的插图。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="图示：机器人如何解释 &quot;帮助&quot;。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="显示机器人可能解释 &quot;感谢&quot; 的说明。" border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a><span data-ttu-id="1c2a8-195">从邮件中提取意图和数据</span><span class="sxs-lookup"><span data-stu-id="1c2a8-195">Extract intent and data from messages</span></span>

<span data-ttu-id="1c2a8-196">将你的 bot 设计为识别意图，这将从你的人员那里获取某人想要响应邮件或查询的内容。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-196">Design your bot to recognize intent, which captures what someone wants from a bot in response to a message or query.</span></span> <span data-ttu-id="1c2a8-197">意向将邮件或查询分类为单个操作，其中包含一个或多个受操作影响的数据对象。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-197">Intent classifies a message or query as a single action with one or more data objects that are affected by the action.</span></span> 

<span data-ttu-id="1c2a8-198">下面的示例概述了发送到 bot 的邮件中的用户意图和数据。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-198">The following examples outline the user intent and data in messages sent to bots.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="示例中所示的 &quot;将航班预订给西雅图&quot; 这一句，用户意图是 &quot;书籍 a 航班&quot;，数据是 &quot;西雅图&quot;。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="示例显示在句子 &quot;何时打开存储&quot;，用户意图是 &quot;when&quot;，且数据为 &quot;开放&quot;。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="示例中显示了句子 &quot;安排会议时，在通讯组中使用王俊元&quot;、用户意向为 &quot;安排会议&quot; 和 &quot;分发中的 Bob&quot; 等数据。" border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a><span data-ttu-id="1c2a8-202">分析和改进</span><span class="sxs-lookup"><span data-stu-id="1c2a8-202">Analyze and improve</span></span>

<span data-ttu-id="1c2a8-203">了解用户在与你的 bot 聊天时应说出的内容。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-203">Learn what users say when chatting with your bot.</span></span> <span data-ttu-id="1c2a8-204">随着用户群在不同位置和 emc 的增长，这将是一个持续的反复发生的过程。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-204">This will be an ongoing, iterative process as your user base grows in different locations and orgs.</span></span> <span data-ttu-id="1c2a8-205">您可以使用 (Microsoft LUIS) 调整您的 bot 的语言识别和意图映射。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-205">You can tune your bot's language recognition and intent mapping with Microsoft Language Understanding (LUIS).</span></span>

* <span data-ttu-id="1c2a8-206">[了解 LUIS](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence)：了解 LUIS 如何使用 AI 提供对应用数据的自然语言理解 (NLU) 。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-206">[Understanding LUIS](https://docs.microsoft.com/azure/cognitive-services/luis/artificial-intelligence): Find out how LUIS uses AI to provide natural language understanding (NLU) to your app data.</span></span>
* <span data-ttu-id="1c2a8-207">[与 LUIS 集成](https://www.luis.ai/)：将自然语言功能添加到你的机器人中，而不是创建机器学习模型的复杂过程。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-207">[Integrating with LUIS](https://www.luis.ai/): Add natural language capabilities to your bot without the complex process of creating machine learning models.</span></span>

## <a name="use-cases"></a><span data-ttu-id="1c2a8-208">用例</span><span class="sxs-lookup"><span data-stu-id="1c2a8-208">Use cases</span></span>

### <a name="simple-queries"></a><span data-ttu-id="1c2a8-209">简单查询</span><span class="sxs-lookup"><span data-stu-id="1c2a8-209">Simple queries</span></span>

<span data-ttu-id="1c2a8-210">Bot 可以提供与查询或一组相关匹配项完全匹配的项，以帮助消除歧义。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-210">Bots can deliver an exact match to a query or a group of related matches to help with disambiguation.</span></span> <span data-ttu-id="1c2a8-211">对于相关的匹配项，请使用列表卡片对内容进行分组。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-211">For related matches, group the content using a list card.</span></span>

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="示例显示与 bot 的简单查询交互。" border="false":::

### <a name="multi-turn-interactions"></a><span data-ttu-id="1c2a8-213">多转换交互</span><span class="sxs-lookup"><span data-stu-id="1c2a8-213">Multi-turn interactions</span></span>

<span data-ttu-id="1c2a8-214">虽然你的 bot 可以支持完整的请求和问题，但它还应能够处理多项交互。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-214">While your bot can support complete requests and questions, it should also be able to handle multi-turn interactions.</span></span> <span data-ttu-id="1c2a8-215">预测可能的后续步骤使用户可以更轻松地执行完整的任务流 (而不是期望他们手工创建一个全面的请求) 。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-215">Anticipating possible next steps makes it much easier for people to a complete task flow (rather than expecting them to craft a comprehensive request).</span></span>

<span data-ttu-id="1c2a8-216">在下面的示例中，bot 将使用有关下一步操作的选项来响应每个邮件。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-216">In the following example, the bot responds to each message with options for what might want to do next.</span></span>

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="示例显示与 bot 之间的多路交互交互。" border="false":::

### <a name="reach-out-to-users"></a><span data-ttu-id="1c2a8-218">与用户联系</span><span class="sxs-lookup"><span data-stu-id="1c2a8-218">Reach out to users</span></span>

<span data-ttu-id="1c2a8-219">通过主动消息传递，你的 bot 可以像摘要那样操作，以特定频率发送与个人、组聊天或频道相关的通知。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-219">With proactive messaging, your bot can act like a digest that sends notifications relevant to an individual, group chat, or channel at a specific frequency.</span></span> <span data-ttu-id="1c2a8-220">当文档中的内容发生了更改或工作项关闭时，bot 可能会发送一封邮件。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-220">A bot may send a message when something has changed in a document or a work item is closed.</span></span>

<span data-ttu-id="1c2a8-221">在以下示例中，用户将收到 toast 通知，即 bot 在另一个频道中将其推广。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-221">In the following example, a user gets a toast notification that a bot messaged them in another channel.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="示例展示了自动将用户从另一个频道传递给用户的 toast。" border="false":::

<span data-ttu-id="1c2a8-223">现在，该频道中的用户可以从 bot 读取其邮件。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-223">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="示例显示了用户查看 bot 的主动消息。" border="false":::

### <a name="use-tabs-with-bots"></a><span data-ttu-id="1c2a8-225">使用带 bot 的选项卡</span><span class="sxs-lookup"><span data-stu-id="1c2a8-225">Use tabs with bots</span></span>

<span data-ttu-id="1c2a8-226">选项卡可使你的 bot 更易于使用。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-226">A tab can make your bot easier to use.</span></span> <span data-ttu-id="1c2a8-227">例如，如果你的 bot 可以创建工作项，则在选项卡中的一个中心位置显示所有这些项会非常好。有关 [设计选项卡](../../tabs/design/tabs.md)的详细信息，请参阅。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-227">For example, if your bot can create work items, it would be nice to show all those items in a central location inside a tab. See more about [designing tabs](../../tabs/design/tabs.md).</span></span>

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="示例显示选项卡如何帮助组织 bot 内容。" border="false":::

## <a name="manage-a-bot"></a><span data-ttu-id="1c2a8-229">管理 bot</span><span class="sxs-lookup"><span data-stu-id="1c2a8-229">Manage a bot</span></span>

<span data-ttu-id="1c2a8-230">用户应该能够更改机器人的设置。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-230">Users should be able to change a bot's settings.</span></span> <span data-ttu-id="1c2a8-231">您可以使用 bot 命令提供此功能，但在 [任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) 中包含所有设置通常效率更高 (如以下示例中所示) 。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-231">You can provide this functionality with bot commands, but it's usually more efficient to include all settings in a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (as shown in the following example).</span></span>

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="示例显示了用于配置 bot 设置的任务模块。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="1c2a8-233">最佳做法</span><span class="sxs-lookup"><span data-stu-id="1c2a8-233">Best practices</span></span>

### <a name="content"></a><span data-ttu-id="1c2a8-234">内容</span><span class="sxs-lookup"><span data-stu-id="1c2a8-234">Content</span></span>

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="do-establish-a-clear-persona"></a><span data-ttu-id="1c2a8-236">操作：建立明确角色</span><span class="sxs-lookup"><span data-stu-id="1c2a8-236">Do: Establish a clear persona</span></span>

<span data-ttu-id="1c2a8-237">你的 bot 的语气是否友好和轻型、"只是真实" 还是超级 quirky？</span><span class="sxs-lookup"><span data-stu-id="1c2a8-237">Is your bot's tone friendly and light, “just the facts”, or super quirky?</span></span> <span data-ttu-id="1c2a8-238">它应如何在不同的方案中做出响应？</span><span class="sxs-lookup"><span data-stu-id="1c2a8-238">How should it respond in different scenarios?</span></span> <span data-ttu-id="1c2a8-239">规划和记录你的 bot 角色可以更轻松地编写看似自然和内聚的响应。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-239">Planning and documenting your bot's persona makes it easier to write responses that seem natural and cohesive.</span></span>

<span data-ttu-id="1c2a8-240">有关在<a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft 团队 UI 工具包 (Figma) </a>中写入 bot 的详细信息，请参阅。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-240">See more about writing for bots in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma).</a></span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a><span data-ttu-id="1c2a8-242">操作：清楚地传达机器人可以执行的操作</span><span class="sxs-lookup"><span data-stu-id="1c2a8-242">Do: Clearly convey what your bot can do</span></span>

<span data-ttu-id="1c2a8-243">欢迎消息和教程帮助用户了解使用你的 bot 可以执行的操作。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-243">Welcome messages and tours help people understand what they can do with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="dont-obscure-your-bots-features"></a><span data-ttu-id="1c2a8-245">不：遮盖你的 bot 的功能</span><span class="sxs-lookup"><span data-stu-id="1c2a8-245">Don't: Obscure your bot's features</span></span>

<span data-ttu-id="1c2a8-246">第一事是印象。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-246">First impressions matter.</span></span> <span data-ttu-id="1c2a8-247">在使用 nondescript 登录邮件时，用户可能会感到困惑或有疑问。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-247">People will likely be confused or suspicious when presented with a nondescript sign-in message.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="do-recognize-non-questions"></a><span data-ttu-id="1c2a8-249">操作：识别非问题</span><span class="sxs-lookup"><span data-stu-id="1c2a8-249">Do: Recognize non-questions</span></span>

<span data-ttu-id="1c2a8-250">你的 bot 应能够响应类似于 "Hi"、"帮助" 和 "感谢" 的邮件，同时还可以对常见的拼写错误和俗语进行评估。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-250">Your bot should be able to respond to messages like "Hi", "Help", and "Thanks" while also accounting for common misspellings and colloquialisms.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a><span data-ttu-id="1c2a8-252">请勿：错过对欣喜的机会</span><span class="sxs-lookup"><span data-stu-id="1c2a8-252">Don't: Miss out on opportunities to delight</span></span>

<span data-ttu-id="1c2a8-253">有些人希望对话以流的方式自然，就像真正的人一样。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-253">Some people expect conversations to flow naturally like they would with a real person.</span></span> <span data-ttu-id="1c2a8-254">尽量避免对简单邮件的 clumsy 响应。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-254">Try to avoid clumsy responses to simple messages.</span></span>

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a><span data-ttu-id="1c2a8-255">疑难解答</span><span class="sxs-lookup"><span data-stu-id="1c2a8-255">Troubleshooting</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="do-provide-help"></a><span data-ttu-id="1c2a8-257">Do：提供帮助</span><span class="sxs-lookup"><span data-stu-id="1c2a8-257">Do: Provide help</span></span>

<span data-ttu-id="1c2a8-258">如果你的 bot 无法满足请求，请为用户提供用于教育自己与你的 bot 进行交互的方法。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-258">If your bot can’t satisfy a request, provide ways for a user to educate themselves about interacting with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="dont-leave-users-stranded"></a><span data-ttu-id="1c2a8-260">请勿：让用户处于进退两难</span><span class="sxs-lookup"><span data-stu-id="1c2a8-260">Don't: Leave users stranded</span></span>

<span data-ttu-id="1c2a8-261">如果用户无法解决问题，他们将很快放弃你的机器人。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-261">People will quickly abandon your bot if they can’t troubleshoot issues.</span></span>

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a><span data-ttu-id="1c2a8-262">复杂的交互</span><span class="sxs-lookup"><span data-stu-id="1c2a8-262">Complex interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="do-use-task-modules-or-tabs"></a><span data-ttu-id="1c2a8-264">操作：使用任务模块或选项卡</span><span class="sxs-lookup"><span data-stu-id="1c2a8-264">Do: Use task modules or tabs</span></span>

<span data-ttu-id="1c2a8-265">如果你的 bot 提供了需要更多步骤的答案，则可以链接到任务模块或选项卡以完成任务或流。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-265">If your bot provides an answer that requires a few more steps, you can link to a task module or tab to complete the task or flow.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a><span data-ttu-id="1c2a8-267">请勿：使多项交互变单调乏味</span><span class="sxs-lookup"><span data-stu-id="1c2a8-267">Don't: Make multi-turn interactions tedious</span></span>

<span data-ttu-id="1c2a8-268">完成单个任务的一个广泛的对话速度缓慢且过于复杂。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-268">An extensive conversation to complete a single task is slow and overly complex.</span></span> <span data-ttu-id="1c2a8-269">它还要求开发人员考虑状态更改 (例如，会话超时或发送 "取消" 邮件) 。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-269">It also requires the developer to account for state changes (such as the conversation timing out or you sending a “Cancel” message).</span></span>

   :::column-end:::
:::row-end:::

### <a name="privacy"></a><span data-ttu-id="1c2a8-270">隐私</span><span class="sxs-lookup"><span data-stu-id="1c2a8-270">Privacy</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a><span data-ttu-id="1c2a8-272">操作：仅在个人上下文中显示敏感信息</span><span class="sxs-lookup"><span data-stu-id="1c2a8-272">Do: Only show sensitive info in a personal context</span></span>

<span data-ttu-id="1c2a8-273">如果你的 bot 位于组聊天或频道中，我们建议将用户定向到专用位置 (如任务模块、选项卡或浏览器) 查看敏感信息。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-273">If your bot is in a group chat or channel, we recommend directing users to a private location (such as a task module, tab, or browser) to view sensitive information.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="显示 bot 最佳实践的示例。" border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a><span data-ttu-id="1c2a8-275">请勿：某些内容并非每个人都能看到</span><span class="sxs-lookup"><span data-stu-id="1c2a8-275">Don't: Some content isn’t meant to be seen by everyone</span></span>

<span data-ttu-id="1c2a8-276">你的 bot 不应将敏感信息泄露给一组用户。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-276">Your bot shouldn’t reveal sensitive information to a group of people.</span></span>

   :::column-end:::
:::row-end:::

## <a name="learn-more"></a><span data-ttu-id="1c2a8-277">了解更多</span><span class="sxs-lookup"><span data-stu-id="1c2a8-277">Learn more</span></span>

<span data-ttu-id="1c2a8-278">这些其他指南可帮助你使用你的 bot 设计：</span><span class="sxs-lookup"><span data-stu-id="1c2a8-278">These other guidelines may help with your bot design:</span></span>

* [<span data-ttu-id="1c2a8-279">正在设计你的个人应用</span><span class="sxs-lookup"><span data-stu-id="1c2a8-279">Designing your personal app</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="1c2a8-280">设计自适应卡片</span><span class="sxs-lookup"><span data-stu-id="1c2a8-280">Designing Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)
* [<span data-ttu-id="1c2a8-281">正在设计任务模块</span><span class="sxs-lookup"><span data-stu-id="1c2a8-281">Designing task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)

## <a name="validate-your-design"></a><span data-ttu-id="1c2a8-282">验证设计</span><span class="sxs-lookup"><span data-stu-id="1c2a8-282">Validate your design</span></span>

<span data-ttu-id="1c2a8-283">如果计划将应用程序发布到 AppSource，则应了解通常会在提交期间导致应用程序失败的设计问题。</span><span class="sxs-lookup"><span data-stu-id="1c2a8-283">If you plan to publish your app to AppSource, you should understand the design issues that commonly cause apps to fail during submission.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1c2a8-284">检查设计验证准则</span><span class="sxs-lookup"><span data-stu-id="1c2a8-284">Check design validation guidelines</span></span>](../../concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#validation-guidelines--most-failed-test-cases)
