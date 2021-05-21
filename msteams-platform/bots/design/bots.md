---
title: 设计机器人
description: 了解如何设计 Teams 自动程序并获取 Microsoft Teams UI Kit。
author: heath-hamilton
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.openlocfilehash: da289b37340f575eda8eb858b13810df48783728
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566143"
---
# <a name="designing-your-microsoft-teams-bot"></a><span data-ttu-id="4b328-103">设计 Microsoft Teams 自动程序</span><span class="sxs-lookup"><span data-stu-id="4b328-103">Designing your Microsoft Teams bot</span></span>

<span data-ttu-id="4b328-104">自动程序是执行一组特定任务的对话应用。</span><span class="sxs-lookup"><span data-stu-id="4b328-104">Bots are conversational apps that perform a specific set of tasks.</span></span> <span data-ttu-id="4b328-105">根据 Microsoft <a href="https://dev.botframework.com/" target="_blank">框架</a>，自动程序会与用户进行通信、回复其问题，并主动通知他们更改和其他事件。</span><span class="sxs-lookup"><span data-stu-id="4b328-105">Based on the <a href="https://dev.botframework.com/" target="_blank">Microsoft Bot Framework</a>, bots communicate with users, respond to their questions, and proactively notify them about changes and other events.</span></span> <span data-ttu-id="4b328-106">这是一个很好的方法。</span><span class="sxs-lookup"><span data-stu-id="4b328-106">They're a great way to reach out.</span></span>

<span data-ttu-id="4b328-107">为指导应用设计，以下信息描述并说明用户可以如何在 Teams 中添加、使用和管理机器人。</span><span class="sxs-lookup"><span data-stu-id="4b328-107">To guide your app design, the following information describes and illustrates how people can add, use, and manage bots in Teams.</span></span>

## <a name="microsoft-teams-ui-kit"></a><span data-ttu-id="4b328-108">Microsoft Teams UI Kit</span><span class="sxs-lookup"><span data-stu-id="4b328-108">Microsoft Teams UI Kit</span></span>

<span data-ttu-id="4b328-109">可在 Microsoft Teams UI Kit 中查看更全面的机器人设计指南，包括可根据需要获取和修改的元素。</span><span class="sxs-lookup"><span data-stu-id="4b328-109">You can find more comprehensive bot design guidelines, including elements that you can grab and modify as needed, in the Microsoft Teams UI Kit.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4b328-110">获取 Microsoft Teams UI Kit （用户）</span><span class="sxs-lookup"><span data-stu-id="4b328-110">Get the Microsoft Teams UI Kit (Figma)</span></span>](https://www.figma.com/community/file/916836509871353159)

## <a name="add-a-bot"></a><span data-ttu-id="4b328-111">添加机器人</span><span class="sxs-lookup"><span data-stu-id="4b328-111">Add a bot</span></span>

<span data-ttu-id="4b328-112">自动程序可用于聊天、频道和个人应用。</span><span class="sxs-lookup"><span data-stu-id="4b328-112">Bots are available in chats, channels, and personal apps.</span></span> <span data-ttu-id="4b328-113">可以以下方法之一添加自动程序：</span><span class="sxs-lookup"><span data-stu-id="4b328-113">You can add a bot one of the following ways:</span></span>

* <span data-ttu-id="4b328-114">从 Teams 应用商店 （AppSource）。</span><span class="sxs-lookup"><span data-stu-id="4b328-114">From the Teams store (AppSource).</span></span>
* <span data-ttu-id="4b328-115">通过使用应用飞出，选择 teams **"更多应用"** 图标。</span><span class="sxs-lookup"><span data-stu-id="4b328-115">Using the app flyout by selecting the **More** icon on the left side of Teams.</span></span>
* <span data-ttu-id="4b328-116">当有@mention聊天或撰写框时（以下示例显示了如何在群组聊天中执行这一操作）。</span><span class="sxs-lookup"><span data-stu-id="4b328-116">With an @mention in the new chat or compose box (the following example shows how you can do this in a group chat).</span></span>

    :::image type="content" source="../../assets/images/bots/add-bot-chat-at-mention.png" alt-text="示例演示了如何使用智能机器人在群组聊天中添加@mention。" border="false":::

## <a name="introduce-a-bot"></a><span data-ttu-id="4b328-118">介绍机器人</span><span class="sxs-lookup"><span data-stu-id="4b328-118">Introduce a bot</span></span>

<span data-ttu-id="4b328-119">自动程序要自行介绍并描述其功能，这一点至关重要。</span><span class="sxs-lookup"><span data-stu-id="4b328-119">It’s critical that your bot introduces itself and describes what it can do.</span></span> <span data-ttu-id="4b328-120">此初始交换可帮助用户了解与智能机器人有关的方式，了解其限制，最重要的是，熟悉与智能机器人的交互。</span><span class="sxs-lookup"><span data-stu-id="4b328-120">This initial exchange helps people understand what to do with the bot, find out its limitations and, most importantly, get comfortable interacting with it.</span></span>

### <a name="welcome-message-in-a-one-on-one-chat"></a><span data-ttu-id="4b328-121">一对一聊天中的欢迎消息</span><span class="sxs-lookup"><span data-stu-id="4b328-121">Welcome message in a one-on-one chat</span></span>

<span data-ttu-id="4b328-122">在个人环境中，欢迎消息可设置机器人的风格。</span><span class="sxs-lookup"><span data-stu-id="4b328-122">In personal contexts, welcome messages set your bot's tone.</span></span> <span data-ttu-id="4b328-123">消息包括问候语、机器人可以做什么，以及一些如何交互的建议。</span><span class="sxs-lookup"><span data-stu-id="4b328-123">The message includes a greeting, what the bot can do, and some suggestions for how to interact.</span></span> <span data-ttu-id="4b328-124">例如，"尝试询问我..."。</span><span class="sxs-lookup"><span data-stu-id="4b328-124">For example, “Try asking me about …”.</span></span> <span data-ttu-id="4b328-125">如果可能，建议应返回存储的响应，无需登录。</span><span class="sxs-lookup"><span data-stu-id="4b328-125">If possible, these suggestions should return stored responses without having to sign in.</span></span>

:::image type="content" source="../../assets/images/bots/bot-personal-welcome.png" alt-text="例如，显示了个人应用中的机器人简介。" border="false":::

### <a name="introductions-in-group-chats-and-channels"></a><span data-ttu-id="4b328-127">群聊和频道简介</span><span class="sxs-lookup"><span data-stu-id="4b328-127">Introductions in group chats and channels</span></span>

<span data-ttu-id="4b328-128">与个人上下文（如个人应用）相比，群聊和频道中的智能机器人简介应略有不同。</span><span class="sxs-lookup"><span data-stu-id="4b328-128">Your bot's introduction should be slightly different in group chats and channels compared to a personal context (like a personal app).</span></span> <span data-ttu-id="4b328-129">在现实中，如果进入一个人员完整的房间;你可自我介绍，而不是每个已存在的人。</span><span class="sxs-lookup"><span data-stu-id="4b328-129">In real life, if you entered a room full of people; you’d introduce yourself instead of welcoming everyone who’s already there.</span></span> <span data-ttu-id="4b328-130">将这一思路融入你的机器人设计中。</span><span class="sxs-lookup"><span data-stu-id="4b328-130">Carry that thinking into your bot design.</span></span>

:::image type="content" source="../../assets/images/bots/bot-group-welcome.png" alt-text="在协作上下文中显示自动介绍的示例。" border="false":::

### <a name="bot-authentication-with-single-sign-on"></a><span data-ttu-id="4b328-132">使用单一登录的自动身份验证</span><span class="sxs-lookup"><span data-stu-id="4b328-132">Bot authentication with single sign-on</span></span>

<span data-ttu-id="4b328-133">当用户向机器人发送消息时，可能需要登录才能使用其所有功能。</span><span class="sxs-lookup"><span data-stu-id="4b328-133">When a person messages a bot, sign in may be required use all its features.</span></span> <span data-ttu-id="4b328-134">可以使用单一登录 （SSO） 简化身份验证过程。</span><span class="sxs-lookup"><span data-stu-id="4b328-134">You can simplify the authentication process using single sign-on (SSO).</span></span>

<span data-ttu-id="4b328-135">请不要忘记：在自动程序命令菜单（**我该怎么办？**）中，还必须提供一个命令以注销。</span><span class="sxs-lookup"><span data-stu-id="4b328-135">Don’t forget: In the bot command menu (**What can I do?**), you must also provide a command to sign out.</span></span>

:::image type="content" source="../../assets/images/bots/bot-sso-example.png" alt-text="示例显示具有登录按钮的自动程序。" border="false":::

### <a name="tours"></a><span data-ttu-id="4b328-137">导览</span><span class="sxs-lookup"><span data-stu-id="4b328-137">Tours</span></span>

<span data-ttu-id="4b328-138">可在包含欢迎消息的教程以及自动程序响应类似"帮助"命令时包括教程。</span><span class="sxs-lookup"><span data-stu-id="4b328-138">You can include a tour with welcome messages and if the bot responds to something like a “help” command.</span></span> <span data-ttu-id="4b328-139">教程是介绍机器人功能最有效的方法。</span><span class="sxs-lookup"><span data-stu-id="4b328-139">A tour is the most effective way to describe what your bot can do.</span></span> <span data-ttu-id="4b328-140">如果适用，它们还非常适用于描述应用的其他功能。</span><span class="sxs-lookup"><span data-stu-id="4b328-140">If applicable, they’re also great for describing your app’s other features.</span></span> <span data-ttu-id="4b328-141">例如，包括邮件扩展的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="4b328-141">For example, include screenshots of your messaging extension.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4b328-142">无需登录即可访问教程。</span><span class="sxs-lookup"><span data-stu-id="4b328-142">Tours should be accessible without having to sign in.</span></span>

#### <a name="one-on-one-chats"></a><span data-ttu-id="4b328-143">一对一聊天</span><span class="sxs-lookup"><span data-stu-id="4b328-143">One-on-one chats</span></span>

<span data-ttu-id="4b328-144">在个人应用中，变盘可提供自动程序的有效概述以及应用的其他任意功能。</span><span class="sxs-lookup"><span data-stu-id="4b328-144">In a personal app, a carousel can provide an effective overview of your bot and any other features of your app.</span></span> <span data-ttu-id="4b328-145">建议包括允许用户试用自动程序命令的按钮。</span><span class="sxs-lookup"><span data-stu-id="4b328-145">Including buttons the let users try bot commands is encouraged.</span></span> <span data-ttu-id="4b328-146">例如， **创建任务**。</span><span class="sxs-lookup"><span data-stu-id="4b328-146">For example, **Create a task**.</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-personal.png" alt-text="一对一聊天中的自动浏览示例。" border="false":::

#### <a name="channels-and-group-chats"></a><span data-ttu-id="4b328-148">频道和群组聊天</span><span class="sxs-lookup"><span data-stu-id="4b328-148">Channels and group chats</span></span>

<span data-ttu-id="4b328-149">在频道和群组聊天中，应在模式（也称为 [任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) 中打开浏览，这样不会中断持续对话。</span><span class="sxs-lookup"><span data-stu-id="4b328-149">In channels and group chats, a tour should open in a modal (also known as a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) so it doesn’t interrupt ongoing conversations.</span></span> <span data-ttu-id="4b328-150">还可选择为教程实施基于角色的视图。</span><span class="sxs-lookup"><span data-stu-id="4b328-150">This also gives you the option to implement role-based views for your tour.</span></span>

:::image type="content" source="../../assets/images/bots/bot-tour-channel.png" alt-text="示例显示频道中的自动浏览。" border="false":::

## <a name="chat-with-a-bot"></a><span data-ttu-id="4b328-152">与聊天机器人聊天</span><span class="sxs-lookup"><span data-stu-id="4b328-152">Chat with a bot</span></span>

<span data-ttu-id="4b328-153">自动程序可直接集成到团队的消息框架。</span><span class="sxs-lookup"><span data-stu-id="4b328-153">Bots integrate directly into Team’s messaging framework.</span></span> <span data-ttu-id="4b328-154">用户可以与智能机器人聊天，以获得其问题的解答或键入命令，让智能机器人执行一组窄或特定的任务。</span><span class="sxs-lookup"><span data-stu-id="4b328-154">Users can chat with a bot to get their questions answered or type commands to have the bot perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="4b328-155">自动程序可主动通过聊天通知用户应用更改或更新。</span><span class="sxs-lookup"><span data-stu-id="4b328-155">Bots can proactively notify users about changes or updates to your app via chat.</span></span>

### <a name="chat-with-a-bot-in-different-contexts"></a><span data-ttu-id="4b328-156">在不同上下文中与机器人聊天</span><span class="sxs-lookup"><span data-stu-id="4b328-156">Chat with a bot in different contexts</span></span>

<span data-ttu-id="4b328-157">可在下列上下文中使用自动程序：</span><span class="sxs-lookup"><span data-stu-id="4b328-157">You can use bots in the following contexts:</span></span>

* <span data-ttu-id="4b328-158">**个人应用**：在个人应用中，机器人具有专用的聊天选项卡。</span><span class="sxs-lookup"><span data-stu-id="4b328-158">**Personal apps**: In a personal app, a bot has a dedicated chat tab.</span></span>
* <span data-ttu-id="4b328-159">**一对一聊天**：用户可以启动与机器人的私密对话。</span><span class="sxs-lookup"><span data-stu-id="4b328-159">**One-on-one chat**: A user can initiate a private conversation with a bot.</span></span> <span data-ttu-id="4b328-160">体验与在个人应用中使用机器人相同。</span><span class="sxs-lookup"><span data-stu-id="4b328-160">It's the same experience as using a bot in a personal app.</span></span>
* <span data-ttu-id="4b328-161">**群组聊天**：通过智能机器人，用户可以在群组聊天中@mentioning机器人。</span><span class="sxs-lookup"><span data-stu-id="4b328-161">**Group chat**: People can interact with a bot in a group chat by @mentioning the bot.</span></span>
* <span data-ttu-id="4b328-162">**频道**：用户可以与频道中的机器人交互。</span><span class="sxs-lookup"><span data-stu-id="4b328-162">**Channel**: People can interact with a bot in a channel.</span></span> <span data-ttu-id="4b328-163">选择@mentioning组合框中的机器人姓名。</span><span class="sxs-lookup"><span data-stu-id="4b328-163">by @mentioning the bot name in the compose box.</span></span> <span data-ttu-id="4b328-164">请记住，在此上下文中，自动程序可供整个团队使用，而不只是频道。</span><span class="sxs-lookup"><span data-stu-id="4b328-164">Remember, in this context, the bot is available to the entire team, not just the channel.</span></span>

### <a name="anatomy"></a><span data-ttu-id="4b328-165">解剖</span><span class="sxs-lookup"><span data-stu-id="4b328-165">Anatomy</span></span>

:::image type="content" source="../../assets/images/bots/bot-anatomy.png" alt-text="示例显示了机器人的结构分析。" border="false":::

|<span data-ttu-id="4b328-167">计数器</span><span class="sxs-lookup"><span data-stu-id="4b328-167">Counter</span></span>|<span data-ttu-id="4b328-168">说明</span><span class="sxs-lookup"><span data-stu-id="4b328-168">Description</span></span>|
|----------|-----------|
|<span data-ttu-id="4b328-169">1</span><span class="sxs-lookup"><span data-stu-id="4b328-169">1</span></span>|<span data-ttu-id="4b328-170">**应用名称和图标**</span><span class="sxs-lookup"><span data-stu-id="4b328-170">**App name and icon**</span></span>|
|<span data-ttu-id="4b328-171">2</span><span class="sxs-lookup"><span data-stu-id="4b328-171">2</span></span>|<span data-ttu-id="4b328-172">**"聊天** 选项卡"中：打开与机器人对话的空白（仅适用于个人应用）。</span><span class="sxs-lookup"><span data-stu-id="4b328-172">**Chat tab**: Opens the space to talk with your bot (applicable only to personal apps).</span></span>|
|<span data-ttu-id="4b328-173">3</span><span class="sxs-lookup"><span data-stu-id="4b328-173">3</span></span>|<span data-ttu-id="4b328-174">**自定义选项卡**：打开与应用相关的其他内容。</span><span class="sxs-lookup"><span data-stu-id="4b328-174">**Custom tabs**: Opens other content related to your app.</span></span>|
|<span data-ttu-id="4b328-175">4 </span><span class="sxs-lookup"><span data-stu-id="4b328-175">4</span></span>|<span data-ttu-id="4b328-176">**关于选项卡**：显示有关应用的基本信息。</span><span class="sxs-lookup"><span data-stu-id="4b328-176">**About tab**: Displays basic information about your app.</span></span>|
|<span data-ttu-id="4b328-177">5 </span><span class="sxs-lookup"><span data-stu-id="4b328-177">5</span></span>|<span data-ttu-id="4b328-178">**聊天气泡**：自动对话使用 Teams 消息框架。</span><span class="sxs-lookup"><span data-stu-id="4b328-178">**Chat bubble**: Bot conversations use the Teams messaging framework.</span></span>|
|<span data-ttu-id="4b328-179">6 </span><span class="sxs-lookup"><span data-stu-id="4b328-179">6</span></span>|<span data-ttu-id="4b328-180">**自适应卡片**：如果自动执行者的答复包括自适应卡片，则卡片将占用聊天气泡的全部宽度。</span><span class="sxs-lookup"><span data-stu-id="4b328-180">**Adaptive Card**: If your bot’s responses include Adaptive Cards, the card takes up the full width of the chat bubble.</span></span>|
|<span data-ttu-id="4b328-181">7 </span><span class="sxs-lookup"><span data-stu-id="4b328-181">7</span></span>|<span data-ttu-id="4b328-182">**命令菜单**：显示自动程序的标准命令（由你定义）。</span><span class="sxs-lookup"><span data-stu-id="4b328-182">**Command menu**: Displays your bot's standard commands (defined by you).</span></span>

### <a name="command-menu"></a><span data-ttu-id="4b328-183">命令菜单</span><span class="sxs-lookup"><span data-stu-id="4b328-183">Command menu</span></span>

<span data-ttu-id="4b328-184">命令菜单提供希望自动程序始终响应的字词或短语的列表。</span><span class="sxs-lookup"><span data-stu-id="4b328-184">The command menu provides a list of words or phrases you want your bot to always respond to.</span></span> <span data-ttu-id="4b328-185">当某人与机器人进行聊天时，命令菜单显示在组合框上方。</span><span class="sxs-lookup"><span data-stu-id="4b328-185">The command menu displays above the compose box when someone is conversing with a bot.</span></span> <span data-ttu-id="4b328-186">当选择命令时，它将插入到邮件中。</span><span class="sxs-lookup"><span data-stu-id="4b328-186">When a command is selected, it gets inserted into a message.</span></span>

<span data-ttu-id="4b328-187">命令列表应简短。</span><span class="sxs-lookup"><span data-stu-id="4b328-187">The list of commands should be brief.</span></span> <span data-ttu-id="4b328-188">此菜单旨在突出显示机器人的主要功能。</span><span class="sxs-lookup"><span data-stu-id="4b328-188">The menu is only meant to highlight your bot’s primary features.</span></span> <span data-ttu-id="4b328-189">命令保持简明性。</span><span class="sxs-lookup"><span data-stu-id="4b328-189">Keep commands concise, too.</span></span> <span data-ttu-id="4b328-190">例如，创建名为"帮助 **命令** 而不是 **"命令，请帮我**？</span><span class="sxs-lookup"><span data-stu-id="4b328-190">For example, create a command called **Help** instead of **Can you please help me**?</span></span>
<span data-ttu-id="4b328-191">无论对话状态如何，命令菜单必须始终可用。</span><span class="sxs-lookup"><span data-stu-id="4b328-191">The command menu must always be available regardless of the state of the conversation.</span></span>

:::image type="content" source="../../assets/images/bots/bot-command-menu.png" alt-text="示例显示自动程序的命令菜单。" border="false":::

## <a name="understand-what-people-are-saying"></a><span data-ttu-id="4b328-193">了解人们所说的</span><span class="sxs-lookup"><span data-stu-id="4b328-193">Understand what people are saying</span></span>

<span data-ttu-id="4b328-194">使用同义词库，尽可能从不同的背景请人员，帮助你生成不同的标准查询理解。</span><span class="sxs-lookup"><span data-stu-id="4b328-194">Use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of standard queries.</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-hello.png" alt-text="显示自动程序如何解读&quot;Hello&quot;的示意图。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-help.png" alt-text="显示自动程序如何解读&quot;帮助&quot;的示意图。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-understanding-thanks.png" alt-text="显示自动程序如何解读&quot;谢谢&quot;的插图。" border="false":::
   :::column-end:::
:::row-end:::

### <a name="extract-intent-and-data-from-messages"></a><span data-ttu-id="4b328-198">从邮件中提取意图和数据</span><span class="sxs-lookup"><span data-stu-id="4b328-198">Extract intent and data from messages</span></span>

<span data-ttu-id="4b328-199">设计智能机器人以识别意图，该意图可捕获智能机器人在响应邮件或查询时所捕获的信息。</span><span class="sxs-lookup"><span data-stu-id="4b328-199">Design your bot to recognize intent, which captures what someone wants from a bot in response to a message or query.</span></span> <span data-ttu-id="4b328-200">意图将邮件或查询分为单个操作，包括受该操作影响的一个或多个数据对象。</span><span class="sxs-lookup"><span data-stu-id="4b328-200">Intent classifies a message or query as a single action with one or more data objects that are affected by the action.</span></span> 

<span data-ttu-id="4b328-201">以下示例概述了发送到自动程序的消息中的用户意图和数据：</span><span class="sxs-lookup"><span data-stu-id="4b328-201">The following examples outline the user intent and data in messages sent to bots:</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-1.png" alt-text="显示在句子&quot;预订到西雅图的航班&quot;中的示例，用户意图是&quot;预定航班&quot;，数据为&quot;西雅图&quot;。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-2.png" alt-text="显示在句子&quot;存储何时打开&quot;中的示例，用户意图是&quot;何时打开&quot;且数据为&quot;打开&quot;。" border="false":::
   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-intent-3.png" alt-text="示例显示在句子&quot;下午 1 点与 Bob 在分发中安排会议&quot;中，用户意图是&quot;安排会议&quot;，数据为&quot;下午 1 点&quot;和&quot;Bob 正在分发&quot;。" border="false":::
   :::column-end:::
:::row-end:::

### <a name="analyze-and-improve"></a><span data-ttu-id="4b328-205">分析和改进</span><span class="sxs-lookup"><span data-stu-id="4b328-205">Analyze and improve</span></span>

<span data-ttu-id="4b328-206">了解用户与机器人聊天时所说的内容。</span><span class="sxs-lookup"><span data-stu-id="4b328-206">Learn what users say when chatting with your bot.</span></span> <span data-ttu-id="4b328-207">随着你的用户群在不同位置和组织之间增长，这一过程将持续迭代。</span><span class="sxs-lookup"><span data-stu-id="4b328-207">This will be an ongoing, iterative process as your user base grows in different locations and orgs.</span></span> <span data-ttu-id="4b328-208">可以使用 Microsoft 语言理解 （TUNE） 优化自动程序的语言识别和意图映射。</span><span class="sxs-lookup"><span data-stu-id="4b328-208">You can tune your bot's language recognition and intent mapping with Microsoft Language Understanding (LUIS).</span></span>

* <span data-ttu-id="4b328-209">[了解组织](/azure/cognitive-services/luis/artificial-intelligence)：了解用户如何使用 AI 为应用数据提供自然语言理解 （NLU）。</span><span class="sxs-lookup"><span data-stu-id="4b328-209">[Understanding LUIS](/azure/cognitive-services/luis/artificial-intelligence): Find out how LUIS uses AI to provide natural language understanding (NLU) to your app data.</span></span>
* <span data-ttu-id="4b328-210">[与 COMPLEX](https://www.luis.ai/)集成：向机器人添加自然语言功能，而无需创建机器学习模型这个复杂流程。</span><span class="sxs-lookup"><span data-stu-id="4b328-210">[Integrating with LUIS](https://www.luis.ai/): Add natural language capabilities to your bot without the complex process of creating machine learning models.</span></span>

## <a name="use-cases"></a><span data-ttu-id="4b328-211">用例</span><span class="sxs-lookup"><span data-stu-id="4b328-211">Use cases</span></span>

### <a name="simple-queries"></a><span data-ttu-id="4b328-212">简单查询</span><span class="sxs-lookup"><span data-stu-id="4b328-212">Simple queries</span></span>

<span data-ttu-id="4b328-213">自动程序可提供查询或一组相关匹配项的精确匹配，有助于进行语言不匹配。</span><span class="sxs-lookup"><span data-stu-id="4b328-213">Bots can deliver an exact match to a query or a group of related matches to help with disambiguation.</span></span> <span data-ttu-id="4b328-214">相关匹配项，使用列表卡对内容进行分组。</span><span class="sxs-lookup"><span data-stu-id="4b328-214">For related matches, group the content using a list card.</span></span>

:::image type="content" source="../../assets/images/bots/bot-simple-query.png" alt-text="示例显示与自动程序的简单查询交互。" border="false":::

### <a name="multi-turn-interactions"></a><span data-ttu-id="4b328-216">多位交互</span><span class="sxs-lookup"><span data-stu-id="4b328-216">Multi-turn interactions</span></span>

<span data-ttu-id="4b328-217">虽然自动程序可支持完整的请求和问题，但也应能够处理多位交互。</span><span class="sxs-lookup"><span data-stu-id="4b328-217">While your bot can support complete requests and questions, it should also be able to handle multi-turn interactions.</span></span> <span data-ttu-id="4b328-218">如果想了解可能的下一步操作，用户就更轻松完成整个任务流（而不是期望他们精心制作一个全面的请求）。</span><span class="sxs-lookup"><span data-stu-id="4b328-218">Anticipating possible next steps makes it much easier for people to a complete task flow (rather than expecting them to craft a comprehensive request).</span></span>

<span data-ttu-id="4b328-219">在下面的示例中，自动程序使用选项响应每条消息，以选择下一步可能要执行哪些操作：</span><span class="sxs-lookup"><span data-stu-id="4b328-219">In the following example, the bot responds to each message with options for what might want to do next:</span></span>

:::image type="content" source="../../assets/images/bots/bot-multi-turn.png" alt-text="示例显示与自动程序之间的多元交互。" border="false":::

### <a name="reach-out-to-users"></a><span data-ttu-id="4b328-221">联系用户</span><span class="sxs-lookup"><span data-stu-id="4b328-221">Reach out to users</span></span>

<span data-ttu-id="4b328-222">通过主动消息传递，机器人可以充当摘要，以特定频率发送与个人、群组聊天或频道相关的通知。</span><span class="sxs-lookup"><span data-stu-id="4b328-222">With proactive messaging, your bot can act like a digest that sends notifications relevant to an individual, group chat, or channel at a specific frequency.</span></span> <span data-ttu-id="4b328-223">文档更改了某些内容或关闭工作项目时，自动程序可能会发送邮件。</span><span class="sxs-lookup"><span data-stu-id="4b328-223">A bot may send a message when something has changed in a document or a work item is closed.</span></span>

<span data-ttu-id="4b328-224">在下面的示例中，用户收到一条 Toast 通知，提示机器人在另一个频道中向用户发送消息：</span><span class="sxs-lookup"><span data-stu-id="4b328-224">In the following example, a user gets a toast notification that a bot messaged them in another channel:</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message-toast.png" alt-text="示例显示了自动程序主动向另一个频道中的用户消息传递消息的祝念。" border="false":::

<span data-ttu-id="4b328-226">现在，用户可以从自动程序阅读其邮件。</span><span class="sxs-lookup"><span data-stu-id="4b328-226">Now in that channel, the user can read their message from the bot.</span></span>

:::image type="content" source="../../assets/images/bots/bot-proactive-message.png" alt-text="示例显示用户查看自动程序主动的消息。" border="false":::

### <a name="use-tabs-with-bots"></a><span data-ttu-id="4b328-228">将标签用于机器人</span><span class="sxs-lookup"><span data-stu-id="4b328-228">Use tabs with bots</span></span>

<span data-ttu-id="4b328-229">选项卡可以使你的自动程序更易于使用。</span><span class="sxs-lookup"><span data-stu-id="4b328-229">A tab can make your bot easier to use.</span></span> <span data-ttu-id="4b328-230">例如，如果你的机器人可以创建工作项，那么在选项卡内的中心位置显示所有这些项目将是一个不错的选择。有关详细信息，请参阅 [设计选项卡](../../tabs/design/tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="4b328-230">For example, if your bot can create work items, it would be nice to show all those items in a central location inside a tab. For more information, See [designing tabs](../../tabs/design/tabs.md).</span></span>

:::image type="content" source="../../assets/images/bots/bot-with-tab.png" alt-text="示例显示选项卡可如何帮助整理自动程序内容。" border="false":::

## <a name="manage-a-bot"></a><span data-ttu-id="4b328-232">管理自动程序</span><span class="sxs-lookup"><span data-stu-id="4b328-232">Manage a bot</span></span>

<span data-ttu-id="4b328-233">用户应能够更改自动程序的设置。</span><span class="sxs-lookup"><span data-stu-id="4b328-233">Users should be able to change a bot's settings.</span></span> <span data-ttu-id="4b328-234">可通过自动程序命令提供此功能，但将 [任务模块](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) （如下例所示）中所有设置通常更高效。</span><span class="sxs-lookup"><span data-stu-id="4b328-234">You can provide this functionality with bot commands, but it's usually more efficient to include all settings in a [task module](../../task-modules-and-cards/task-modules/design-teams-task-modules.md) (as shown in the following example).</span></span>

:::image type="content" source="../../assets/images/bots/manage-bot-task-module.png" alt-text="示例显示一个任务模块，用于配置机器人的设置。" border="false":::

## <a name="best-practices"></a><span data-ttu-id="4b328-236">最佳做法</span><span class="sxs-lookup"><span data-stu-id="4b328-236">Best practices</span></span>

<span data-ttu-id="4b328-237">使用这些建议创建高质量的应用体验。</span><span class="sxs-lookup"><span data-stu-id="4b328-237">Use these recommendations to create a quality app experience.</span></span>

### <a name="content"></a><span data-ttu-id="4b328-238">Content</span><span class="sxs-lookup"><span data-stu-id="4b328-238">Content</span></span>

:::image type="content" source="../../assets/images/bots/bot-content-persona-do.png" alt-text="显示建立清晰人物的自动程序最佳做法的示例。" border="false":::

#### <a name="do-establish-a-clear-persona"></a><span data-ttu-id="4b328-240">执行：建立一个清晰的人</span><span class="sxs-lookup"><span data-stu-id="4b328-240">Do: Establish a clear persona</span></span>

<span data-ttu-id="4b328-241">你的机器人的口风格是否友好且浅，"仅事实"或超可人？</span><span class="sxs-lookup"><span data-stu-id="4b328-241">Is your bot's tone friendly and light, “just the facts”, or super quirky?</span></span> <span data-ttu-id="4b328-242">如何在不同的情况下进行响应？</span><span class="sxs-lookup"><span data-stu-id="4b328-242">How should it respond in different scenarios?</span></span> <span data-ttu-id="4b328-243">通过规划和记录机器人用户的内容，可以更轻松地编写自然且有凝聚力的答复。</span><span class="sxs-lookup"><span data-stu-id="4b328-243">Planning and documenting your bot's persona makes it easier to write responses that seem natural and cohesive.</span></span>

<span data-ttu-id="4b328-244">在 Microsoft Teams UI Kit （Kitma） 中 <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">机器人编写功能。</a></span><span class="sxs-lookup"><span data-stu-id="4b328-244">See more about writing for bots in the <a href="https://www.figma.com/community/file/916836509871353159" target="_blank">Microsoft Teams UI Kit (Figma).</a></span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-do.png" alt-text="显示以清楚地传达机器人可以执行哪些功能的示例。" border="false":::

#### <a name="do-clearly-convey-what-your-bot-can-do"></a><span data-ttu-id="4b328-246">工作：清楚传达你的机器人可以做什么</span><span class="sxs-lookup"><span data-stu-id="4b328-246">Do: Clearly convey what your bot can do</span></span>

<span data-ttu-id="4b328-247">欢迎消息和导览可帮助用户了解他们可以使用智能机器人执行什么操作。</span><span class="sxs-lookup"><span data-stu-id="4b328-247">Welcome messages and tours help people understand what they can do with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-convey-dont.png" alt-text="显示不遮盖机器人功能的示例。" border="false":::

#### <a name="dont-obscure-your-bots-features"></a><span data-ttu-id="4b328-249">不要：遮住了机器人的功能</span><span class="sxs-lookup"><span data-stu-id="4b328-249">Don't: Obscure your bot's features</span></span>

<span data-ttu-id="4b328-250">第一印象很重要。</span><span class="sxs-lookup"><span data-stu-id="4b328-250">First impressions matter.</span></span> <span data-ttu-id="4b328-251">当显示非描述登录邮件时，用户可能会困惑或可疑。</span><span class="sxs-lookup"><span data-stu-id="4b328-251">People will likely be confused or suspicious when presented with a nondescript sign-in message.</span></span>

   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-do.png" alt-text="显示自动程序应识别非问题的示例。" border="false":::

#### <a name="do-recognize-non-questions"></a><span data-ttu-id="4b328-253">注意：识别非问题</span><span class="sxs-lookup"><span data-stu-id="4b328-253">Do: Recognize non-questions</span></span>

<span data-ttu-id="4b328-254">你的自动程序应能够回复"你好"、"帮助"和"谢谢"等消息，同时还调查常见的拼写错误和拼错的信息。</span><span class="sxs-lookup"><span data-stu-id="4b328-254">Your bot should be able to respond to messages like "Hi", "Help", and "Thanks" while also accounting for common misspellings and colloquialisms.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-content-understand-dont.png" alt-text="显示应避免对简单自动程序消息的不一致响应的示例。" border="false":::

#### <a name="dont-miss-out-on-opportunities-to-delight"></a><span data-ttu-id="4b328-256">不要：错过一些可喜欢的机会</span><span class="sxs-lookup"><span data-stu-id="4b328-256">Don't: Miss out on opportunities to delight</span></span>

<span data-ttu-id="4b328-257">一些人希望对话可以像与真实人员一样自然流式交流。</span><span class="sxs-lookup"><span data-stu-id="4b328-257">Some people expect conversations to flow naturally like they would with a real person.</span></span> <span data-ttu-id="4b328-258">尽量避免对简单邮件的字体显示错误。</span><span class="sxs-lookup"><span data-stu-id="4b328-258">Try to avoid clumsy responses to simple messages.</span></span>

   :::column-end:::
:::row-end:::

### <a name="troubleshooting"></a><span data-ttu-id="4b328-259">疑难解答</span><span class="sxs-lookup"><span data-stu-id="4b328-259">Troubleshooting</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-do.png" alt-text="显示自动程序的示例应帮助用户了解如何使用机器人。" border="false":::

#### <a name="do-provide-help"></a><span data-ttu-id="4b328-261">执行：提供帮助</span><span class="sxs-lookup"><span data-stu-id="4b328-261">Do: Provide help</span></span>

<span data-ttu-id="4b328-262">如果机器人不满足请求，提供用户指导用户与机器人交互的方法。</span><span class="sxs-lookup"><span data-stu-id="4b328-262">If your bot can’t satisfy a request, provide ways for a user to educate themselves about interacting with your bot.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-help-dont.png" alt-text="显示自动程序不应将用户设置成这样一个示例。" border="false":::

#### <a name="dont-leave-users-stranded"></a><span data-ttu-id="4b328-264">请勿参与：将用户困</span><span class="sxs-lookup"><span data-stu-id="4b328-264">Don't: Leave users stranded</span></span>

<span data-ttu-id="4b328-265">用户如果无法解决问题，会迅速离开机器人。</span><span class="sxs-lookup"><span data-stu-id="4b328-265">People will quickly abandon your bot if they can’t troubleshoot issues.</span></span>

   :::column-end:::
:::row-end:::

### <a name="complex-interactions"></a><span data-ttu-id="4b328-266">复杂交互</span><span class="sxs-lookup"><span data-stu-id="4b328-266">Complex interactions</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-do.png" alt-text="显示你可以将任务模块或选项卡与自动程序一起用于复杂交互的示例。" border="false":::

#### <a name="do-use-task-modules-or-tabs"></a><span data-ttu-id="4b328-268">Do：使用任务模块或选项卡</span><span class="sxs-lookup"><span data-stu-id="4b328-268">Do: Use task modules or tabs</span></span>

<span data-ttu-id="4b328-269">如果您的自动程序提供了需要执行更多步骤的答案，您可以链接到任务模块或选项卡以完成任务或流程。</span><span class="sxs-lookup"><span data-stu-id="4b328-269">If your bot provides an answer that requires a few more steps, you can link to a task module or tab to complete the task or flow.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-interactions-dont.png" alt-text="显示自动程序应避免多向交互的示例。" border="false":::

#### <a name="dont-make-multi-turn-interactions-tedious"></a><span data-ttu-id="4b328-271">不要：进行多元交互，件非常乏味</span><span class="sxs-lookup"><span data-stu-id="4b328-271">Don't: Make multi-turn interactions tedious</span></span>

<span data-ttu-id="4b328-272">完成单个任务的丰富对话速度缓慢且过于复杂。</span><span class="sxs-lookup"><span data-stu-id="4b328-272">An extensive conversation to complete a single task is slow and overly complex.</span></span> <span data-ttu-id="4b328-273">这还需要开发人员考虑状态更改（例如对话超时或发送"取消"消息）。</span><span class="sxs-lookup"><span data-stu-id="4b328-273">It also requires the developer to account for state changes (such as the conversation timing out or you sending a “Cancel” message).</span></span>

   :::column-end:::
:::row-end:::

### <a name="privacy"></a><span data-ttu-id="4b328-274">隐私</span><span class="sxs-lookup"><span data-stu-id="4b328-274">Privacy</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-do.png" alt-text="显示自动程序应如何在个人上下文中显示私人信息的示例。" border="false":::

#### <a name="do-only-show-sensitive-info-in-a-personal-context"></a><span data-ttu-id="4b328-276">Do：仅在个人上下文中显示敏感信息</span><span class="sxs-lookup"><span data-stu-id="4b328-276">Do: Only show sensitive info in a personal context</span></span>

<span data-ttu-id="4b328-277">如果自动程序位于群组聊天或频道中，建议将用户引导至专用位置（例如任务模块、选项卡或浏览器）以查看敏感信息。</span><span class="sxs-lookup"><span data-stu-id="4b328-277">If your bot is in a group chat or channel, we recommend directing users to a private location (such as a task module, tab, or browser) to view sensitive information.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/bots/bot-privacy-dont.png" alt-text="显示机器人不应向组或人员显示敏感信息的示例。" border="false":::

#### <a name="dont-some-content-isnt-meant-to-be-seen-by-everyone"></a><span data-ttu-id="4b328-279">不要：某些内容并非由每个人看到</span><span class="sxs-lookup"><span data-stu-id="4b328-279">Don't: Some content isn’t meant to be seen by everyone</span></span>

<span data-ttu-id="4b328-280">你的自动程序不得向一组人员泄露敏感信息。</span><span class="sxs-lookup"><span data-stu-id="4b328-280">Your bot shouldn’t reveal sensitive information to a group of people.</span></span>

   :::column-end:::
:::row-end:::

## <a name="see-also"></a><span data-ttu-id="4b328-281">另请参阅</span><span class="sxs-lookup"><span data-stu-id="4b328-281">See also</span></span>

<span data-ttu-id="4b328-282">以下其他准则可帮助你进行机器人设计：</span><span class="sxs-lookup"><span data-stu-id="4b328-282">These other guidelines may help with your bot design:</span></span>

* [<span data-ttu-id="4b328-283">设计个人应用</span><span class="sxs-lookup"><span data-stu-id="4b328-283">Designing your personal app</span></span>](../../concepts/design/personal-apps.md)
* [<span data-ttu-id="4b328-284">设计自适应卡片</span><span class="sxs-lookup"><span data-stu-id="4b328-284">Designing Adaptive Cards</span></span>](../../task-modules-and-cards/cards/design-effective-cards.md)
* [<span data-ttu-id="4b328-285">设计任务模块</span><span class="sxs-lookup"><span data-stu-id="4b328-285">Designing task modules</span></span>](../../task-modules-and-cards/task-modules/design-teams-task-modules.md)
