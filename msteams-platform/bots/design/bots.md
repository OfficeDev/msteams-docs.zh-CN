---
title: Bot 设计指南
description: 介绍创建 bot 的指南
keywords: 团队设计指南参考框架 bot 对话
ms.openlocfilehash: 4f474278b37058f61886a620af634780d2e3cb19
ms.sourcegitcommit: d0ca6a4856ffd03d197d47338e633126723fa78a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/15/2020
ms.locfileid: "45137673"
---
# <a name="start-talking-with-bots"></a><span data-ttu-id="63df4-104">开始与 bot 对话</span><span class="sxs-lookup"><span data-stu-id="63df4-104">Start talking with bots</span></span>

<span data-ttu-id="63df4-105">Bot 是执行一组较窄或特定任务的会话式应用程序。</span><span class="sxs-lookup"><span data-stu-id="63df4-105">Bots are conversational apps that perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="63df4-106">它们为您提供了与用户进行通信的机会，回答了他们的问题，并主动通知他们发生了哪些更改。</span><span class="sxs-lookup"><span data-stu-id="63df4-106">They give you an opportunity to communicate with users, respond to their questions, and proactively notify them about changes.</span></span> <span data-ttu-id="63df4-107">这是一种很好的方法。</span><span class="sxs-lookup"><span data-stu-id="63df4-107">They’re a great way to reach out.</span></span>

---

## <a name="guidelines"></a><span data-ttu-id="63df4-108">准则</span><span class="sxs-lookup"><span data-stu-id="63df4-108">Guidelines</span></span>

### <a name="avatars"></a><span data-ttu-id="63df4-109">虚拟形象</span><span class="sxs-lookup"><span data-stu-id="63df4-109">Avatars</span></span>

<span data-ttu-id="63df4-110">在团队中，Bot 虚拟形象的形状类似于六边形，因此人们可以快速判断他们正在与某个 bot 而不是某人交谈。</span><span class="sxs-lookup"><span data-stu-id="63df4-110">Bot avatars in Teams are shaped like hexagons so people can quickly tell that they’re talking to a bot instead of a person.</span></span> <span data-ttu-id="63df4-111">你将头像作为方块提交，我们将为你进行裁剪。</span><span class="sxs-lookup"><span data-stu-id="63df4-111">You’ll submit your avatar as a square and we’ll crop it for you.</span></span> <span data-ttu-id="63df4-112">当遇到虚拟形象时，我们建议您让您能够在2英尺和使用较高的对比度的情况下清晰地消失。</span><span class="sxs-lookup"><span data-stu-id="63df4-112">When it comes to avatars, we recommend making yours legible from 2 feet away and using a higher contrast.</span></span>

[!include[Avatar image](~/includes/design/bot-avatar-image.html)]

### <a name="buttons"></a><span data-ttu-id="63df4-113">按钮</span><span class="sxs-lookup"><span data-stu-id="63df4-113">Buttons</span></span>

<span data-ttu-id="63df4-114">我们每张卡片最长支持六个按钮。</span><span class="sxs-lookup"><span data-stu-id="63df4-114">We support up to six buttons per card.</span></span> <span data-ttu-id="63df4-115">编写按钮文本时请务必简明扼要，并且请注意，大多数按钮应仅处理手头的任务。</span><span class="sxs-lookup"><span data-stu-id="63df4-115">Be concise when writing button text, and keep in mind that most buttons should only address the task at hand.</span></span>

### <a name="graphics"></a><span data-ttu-id="63df4-116">图形</span><span class="sxs-lookup"><span data-stu-id="63df4-116">Graphics</span></span>

<span data-ttu-id="63df4-117">图形是一种很不错的说明，但并不是所有机器人对话都需要图形，因此使用它们来获得最大影响。</span><span class="sxs-lookup"><span data-stu-id="63df4-117">Graphics are a good way to tell a story, but not all bot conversations require graphics, so use them for maximum impact.</span></span>

### <a name="onboarding-users"></a><span data-ttu-id="63df4-118">载入用户</span><span class="sxs-lookup"><span data-stu-id="63df4-118">Onboarding users</span></span>

<span data-ttu-id="63df4-119">关键是，bot 会自我介绍并传达他们可以为用户执行的操作。</span><span class="sxs-lookup"><span data-stu-id="63df4-119">It is critical that bots introduce themselves and convey what they can do for users.</span></span> <span data-ttu-id="63df4-120">此*值 exchange*可帮助用户了解如何使用 bot，这些限制可能位于何处，并且最重要的是，帮助用户容许与不像真实人员那样直观的计算机进行交互。</span><span class="sxs-lookup"><span data-stu-id="63df4-120">This *value exchange* helps users understand what to do with the bot, where the limitations may lie, and, most importantly, helps users tolerate the interaction with a machine that won’t be as intuitive as a real person .</span></span> <span data-ttu-id="63df4-121">此外，它还向 exchange 中的用户数据授予对该服务提供的真正价值的权限。</span><span class="sxs-lookup"><span data-stu-id="63df4-121">Additionally, it grants permission to user data in exchange for the real value the service provides.</span></span>

#### <a name="welcome-messages"></a><span data-ttu-id="63df4-122">欢迎邮件</span><span class="sxs-lookup"><span data-stu-id="63df4-122">Welcome messages</span></span>

<span data-ttu-id="63df4-123">欢迎邮件是设置你的 bot 语气并应在个人和团队或组方案中使用的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="63df4-123">Welcome messages are the best way to set your bot's tone and should be used in personal and team or group scenarios.</span></span> <span data-ttu-id="63df4-124">该消息指出了 bot 的功能以及与之进行交互的一些常见方法。</span><span class="sxs-lookup"><span data-stu-id="63df4-124">The message states what the bot does and some common ways to interact with it.</span></span> <span data-ttu-id="63df4-125">使用类似 "*请尝试询问*..." 的特定功能示例</span><span class="sxs-lookup"><span data-stu-id="63df4-125">Use specific capability examples like,  “*Try asking ….*”</span></span> <span data-ttu-id="63df4-126">在项目符号列表中。</span><span class="sxs-lookup"><span data-stu-id="63df4-126">in a bulleted list.</span></span> <span data-ttu-id="63df4-127">只要有可能，这些建议应返回存储的响应。</span><span class="sxs-lookup"><span data-stu-id="63df4-127">Whenever possible, these suggestions should return stored responses.</span></span> <span data-ttu-id="63df4-128">此功能示例非常关键，无需用户登录即可正常工作。</span><span class="sxs-lookup"><span data-stu-id="63df4-128">It's critical that the capability examples work without requiring users to sign in.</span></span>

#### <a name="tours"></a><span data-ttu-id="63df4-129">漫游</span><span class="sxs-lookup"><span data-stu-id="63df4-129">Tours</span></span>

<span data-ttu-id="63df4-130">包括使用欢迎邮件的*教程*属性和对与 "*帮助*" 等效的用户输入的响应。</span><span class="sxs-lookup"><span data-stu-id="63df4-130">Include a *Take a tour* attribute with welcome messages and responses to user input equivalent to “*help*”.</span></span> <span data-ttu-id="63df4-131">这是让用户了解机器人可以执行的操作的最有效方法。</span><span class="sxs-lookup"><span data-stu-id="63df4-131">This is the most effective way to let users learn what a bot can do.</span></span> <span data-ttu-id="63df4-132">在一对一体验中，Carousels 是一种很好的方法，可告知这一情景，包括 " *Try it* " 按钮。鼓励可能的响应示例。</span><span class="sxs-lookup"><span data-stu-id="63df4-132">Carousels in one-to-one experiences are an excellent way to tell this story and including *Try it* buttons linking to  examples of possible responses is encouraged.</span></span> <span data-ttu-id="63df4-133">漫游也是谈论应用程序的其他功能的很好的地方。</span><span class="sxs-lookup"><span data-stu-id="63df4-133">Tours are also great places to talk about an app’s other features.</span></span> <span data-ttu-id="63df4-134">例如，可以包括邮件扩展和工作组选项卡的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="63df4-134">For example, you can include screenshots of messaging extensions and Teams tabs.</span></span>  <span data-ttu-id="63df4-135">用户无需登录即可访问和使用教程。</span><span class="sxs-lookup"><span data-stu-id="63df4-135">Users shouldn't have to sign in to access and use a tour.</span></span>

<span data-ttu-id="63df4-136">在团队或组方案中使用演示时，他们应在任务模块中打开，以便不向用户之间的正在进行的会话添加更多的卡噪音。</span><span class="sxs-lookup"><span data-stu-id="63df4-136">When tours are used in team or group scenarios, they should open in a task module so as not to add more card noise to the ongoing conversations between users.</span></span>

### <a name="responding-to-users-and-failing-gracefully"></a><span data-ttu-id="63df4-137">响应用户并顺利进行故障转移</span><span class="sxs-lookup"><span data-stu-id="63df4-137">Responding to users and failing gracefully</span></span>

<span data-ttu-id="63df4-138">你的 bot 还应能够在考虑常见的拼写错误和俗语时，对诸如 "*Hi*"、"*帮助*" 和 "*感谢*" 这样的内容做出响应。</span><span class="sxs-lookup"><span data-stu-id="63df4-138">Your bot should also be able to respond to things like "*Hi*", "*Help*", and "*Thanks*" while taking common misspellings and colloquialisms into account.</span></span> <span data-ttu-id="63df4-139">例如：</span><span class="sxs-lookup"><span data-stu-id="63df4-139">For example:</span></span>

#### <a name="x2713-hello"></a><span data-ttu-id="63df4-140">&#x2713; Hello</span><span class="sxs-lookup"><span data-stu-id="63df4-140">&#x2713; Hello</span></span>

<span data-ttu-id="63df4-141">`"Hi"`  `"How are you"`  `"Howdy"`</span><span class="sxs-lookup"><span data-stu-id="63df4-141">`"Hi"`  `"How are you"`  `"Howdy"`</span></span>

#### <a name="x2713-help"></a><span data-ttu-id="63df4-142">&#x2713; 帮助</span><span class="sxs-lookup"><span data-stu-id="63df4-142">&#x2713; Help</span></span>

<span data-ttu-id="63df4-143">`"What do you do?"`  `"How does this work?"`  `"What the heck?"`</span><span class="sxs-lookup"><span data-stu-id="63df4-143">`"What do you do?"`  `"How does this work?"`  `"What the heck?"`</span></span>

#### <a name="x2713-thanks"></a><span data-ttu-id="63df4-144">&#x2713; 感谢</span><span class="sxs-lookup"><span data-stu-id="63df4-144">&#x2713; Thanks</span></span>

<span data-ttu-id="63df4-145">`"Thank you"`  `"Thankyou"`  `"Thx"`</span><span class="sxs-lookup"><span data-stu-id="63df4-145">`"Thank you"`  `"Thankyou"`  `"Thx"`</span></span>

<span data-ttu-id="63df4-146">你的 bot 应能够处理以下类型的查询和输入：</span><span class="sxs-lookup"><span data-stu-id="63df4-146">Your bot should be able to handle the following types of queries and inputs:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="63df4-147">**识别的问题**。</span><span class="sxs-lookup"><span data-stu-id="63df4-147">**Recognized questions**.</span></span> <span data-ttu-id="63df4-148">这些是用户预期的 "最佳方案情况" 问题。</span><span class="sxs-lookup"><span data-stu-id="63df4-148">These are the “best case scenario” questions you would expect from users.</span></span>
> * <span data-ttu-id="63df4-149">**识别的无问题**。</span><span class="sxs-lookup"><span data-stu-id="63df4-149">**Recognized non-questions**.</span></span> <span data-ttu-id="63df4-150">有关不受支持的功能和/或随机、无关或 profane 条目的查询。</span><span class="sxs-lookup"><span data-stu-id="63df4-150">Queries about unsupported functionality and/or random, unrelated , or profane entries.</span></span>
> * <span data-ttu-id="63df4-151">**无法识别的问题**：输入或无法识别、无意义或无意义的项。</span><span class="sxs-lookup"><span data-stu-id="63df4-151">**Unrecognized questions**: Input or entries that are unintelligible, meaningless, or nonsense.</span></span>

<span data-ttu-id="63df4-152">Bot 的个性和响应类型的示例：</span><span class="sxs-lookup"><span data-stu-id="63df4-152">Examples of bot personality and response types:</span></span>

[!include[Bot responses](~/includes/design/bot-responses-table.html)]

> [!TIP]
> <span data-ttu-id="63df4-153">编写机器人脚本时，请询问自己： "我的公司是否为 embarrassed 如果响应是通过屏幕捕获并共享吗？"</span><span class="sxs-lookup"><span data-stu-id="63df4-153">When writing your bot script, ask yourself: “Will my company be embarrassed if a response is screen captured and shared?”</span></span>

### <a name="understanding-what-users-are-trying-to-say"></a><span data-ttu-id="63df4-154">了解用户试图说出的内容</span><span class="sxs-lookup"><span data-stu-id="63df4-154">Understanding what users are trying to say</span></span>

#### <a name="use-a-thesaurus-for-synonyms"></a><span data-ttu-id="63df4-155">对同义词使用同义词库</span><span class="sxs-lookup"><span data-stu-id="63df4-155">Use a thesaurus for synonyms</span></span>

<span data-ttu-id="63df4-156">当灵感触发变体时，请使用同义词库并从尽可能多的不同背景中获取人员，以帮助您生成每个查询的不同解释。</span><span class="sxs-lookup"><span data-stu-id="63df4-156">When brainstorming variants, use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of each query.</span></span>

#### <a name="make-use-of-telemetry-and-interviews"></a><span data-ttu-id="63df4-157">使用遥测和访谈</span><span class="sxs-lookup"><span data-stu-id="63df4-157">Make use of telemetry and interviews</span></span>

<span data-ttu-id="63df4-158">了解用户在查询你的 bot 时所说的含义以及它们的意图。</span><span class="sxs-lookup"><span data-stu-id="63df4-158">Find out what users are saying and what was their intent when querying your bot.</span></span> <span data-ttu-id="63df4-159">当你在不同位置和公司类型中获取用户时，这将是一个持续的过程。</span><span class="sxs-lookup"><span data-stu-id="63df4-159">This will be an ongoing process as you get users in different locations and types of companies.</span></span> <span data-ttu-id="63df4-160">您可以使用语言理解智能服务（[LUIS](/azure/cognitive-services/luis/what-is-luis)）微调语言识别和意图映射。</span><span class="sxs-lookup"><span data-stu-id="63df4-160">You can fine-tune language recognition and intent mapping with Language Understanding Intelligent Service ([LUIS](/azure/cognitive-services/luis/what-is-luis)).</span></span>

### <a name="how-often-should-you-use-your-bot-to-reach-out-to-a-user"></a><span data-ttu-id="63df4-161">应多长时间使用你的 bot 与用户联系？</span><span class="sxs-lookup"><span data-stu-id="63df4-161">How often should you use your bot to reach out to a user?</span></span>

#### <a name="x2713-when-a-state-has-changed"></a><span data-ttu-id="63df4-162">状态更改时 &#x2713;</span><span class="sxs-lookup"><span data-stu-id="63df4-162">&#x2713; When a state has changed</span></span>

<span data-ttu-id="63df4-163">例如，如果工作分配标记为 "已完成"、"bug 更改时"、"新社交媒体可用" 或 "已完成轮询"。</span><span class="sxs-lookup"><span data-stu-id="63df4-163">For example, if an assignment is marked as complete, when a bug changes, when new social media is available, or when a poll has been completed.</span></span>

#### <a name="x2713-when-the-timing-is-right"></a><span data-ttu-id="63df4-164">当计时正确时 &#x2713;</span><span class="sxs-lookup"><span data-stu-id="63df4-164">&#x2713; When the timing is right</span></span>

<span data-ttu-id="63df4-165">你的 bot 可以像每日摘要那样操作，以特定频率向用户或频道发送通知。</span><span class="sxs-lookup"><span data-stu-id="63df4-165">Your bot can act like a daily digest, sending a notification to the user or channel at a specific frequency.</span></span>

<span data-ttu-id="63df4-166">将用户保持在控制之下。</span><span class="sxs-lookup"><span data-stu-id="63df4-166">Leave the user in control.</span></span> <span data-ttu-id="63df4-167">提供包括频率和优先级的通知设置。</span><span class="sxs-lookup"><span data-stu-id="63df4-167">Provide notification settings that include frequency and priority.</span></span>

[!include[Bot notification](~/includes/design/bot-notification-image.html)]

---

## <a name="using-tabs"></a><span data-ttu-id="63df4-168">使用选项卡</span><span class="sxs-lookup"><span data-stu-id="63df4-168">Using tabs</span></span>

<span data-ttu-id="63df4-169">选项卡使你的 bot 功能更强大。</span><span class="sxs-lookup"><span data-stu-id="63df4-169">Tabs make your bot much more functional.</span></span> <span data-ttu-id="63df4-170">通过选项卡，您可以创建以下内容：</span><span class="sxs-lookup"><span data-stu-id="63df4-170">With tabs, you can create the following:</span></span>

### <a name="x2713-a-place-to-host-standing-queries"></a><span data-ttu-id="63df4-171">&#x2713; 承载驻留查询的位置</span><span class="sxs-lookup"><span data-stu-id="63df4-171">&#x2713; A place to host standing queries</span></span>

<span data-ttu-id="63df4-172">在 bot 和单个用户之间的个人对话中，选项卡可以包含用户特定的信息和列表。</span><span class="sxs-lookup"><span data-stu-id="63df4-172">In personal conversations between a bot and a single person, tabs can contain user-specific information and lists.</span></span> <span data-ttu-id="63df4-173">它们也是维护对常见问题（Faq）的 bot 响应的理想位置，因此用户无需继续提问。</span><span class="sxs-lookup"><span data-stu-id="63df4-173">They’re also a good place to maintain bot responses to frequently-asked questions (FAQs) — so users don’t need to keep asking.</span></span>

### <a name="x2713-a-place-to-finish-a-conversation"></a><span data-ttu-id="63df4-174">&#x2713; 完成对话的位置</span><span class="sxs-lookup"><span data-stu-id="63df4-174">&#x2713; A place to finish a conversation</span></span>

<span data-ttu-id="63df4-175">您可以从卡片链接到选项卡。</span><span class="sxs-lookup"><span data-stu-id="63df4-175">You can link to a tab from a card.</span></span> <span data-ttu-id="63df4-176">如果你的 bot 提供了需要更多步骤的答案，则它可以链接到选项卡以完成任务或流。</span><span class="sxs-lookup"><span data-stu-id="63df4-176">If your bot provides an answer that requires a few more steps, it can link to a tab to complete the task or flow.</span></span> <span data-ttu-id="63df4-177">例如，为了响应，"如何设置 iPhone 的格式？" 好的响应可能是一个卡片，它概括了前几个步骤，并具有一个*显示更多*步骤的按钮，然后将用户带到 bot 的 "*帮助*" 选项卡和指向特定说明的深层链接。</span><span class="sxs-lookup"><span data-stu-id="63df4-177">For instance, in response to, "How do I format my iPhone?", a good response might be a card which outlines the first few steps and has a button for *Show more* that then takes the user to the bot's *Help* tab and deep links to the specific instructions.</span></span>

### <a name="x2713-a-place-to-host-a-settings-page"></a><span data-ttu-id="63df4-178">&#x2713; 承载设置页面的位置</span><span class="sxs-lookup"><span data-stu-id="63df4-178">&#x2713; A place to host a settings page</span></span>

<span data-ttu-id="63df4-179">Bot 应具有一些用户控件。</span><span class="sxs-lookup"><span data-stu-id="63df4-179">Bots should have some user control.</span></span> <span data-ttu-id="63df4-180">对于很多机器人，通过聊天界面允许它;但是，很难记住这些设置。</span><span class="sxs-lookup"><span data-stu-id="63df4-180">For many bots it is allowed through a chat interface; however, it's hard to remember those settings.</span></span> <span data-ttu-id="63df4-181">"设置" 选项卡可以显示 "用户" 设置，允许用户一次更改所有设置，也可能是更复杂的 bot 自定义行为的一个良好的位置。</span><span class="sxs-lookup"><span data-stu-id="63df4-181">A settings tab can display users settings, allow users to change them all at once, and may also be a good hand-off point for more complex bot custom behaviors.</span></span>

### <a name="x2713-a-place-to-provide-some-help"></a><span data-ttu-id="63df4-182">&#x2713; 提供一些帮助的位置</span><span class="sxs-lookup"><span data-stu-id="63df4-182">&#x2713; A place to provide some help</span></span>

<span data-ttu-id="63df4-183">添加一个选项卡，educates 用户如何与你的 bot 进行通信。</span><span class="sxs-lookup"><span data-stu-id="63df4-183">Add a tab that educates users about how to communicate with your bot.</span></span> <span data-ttu-id="63df4-184">您可以为其所做的操作或 Faq 提供一些上下文。</span><span class="sxs-lookup"><span data-stu-id="63df4-184">You can provide some context for what it does or FAQs.</span></span>

![提供帮助](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> <span data-ttu-id="63df4-186">在选项卡中嵌入网站的各个部分将有助于用户在使用您的服务时维护对话的上下文。</span><span class="sxs-lookup"><span data-stu-id="63df4-186">Embedding parts of your site in a tab will help users maintain the context of a conversation as they use your service.</span></span> <span data-ttu-id="63df4-187">它消除了在浏览器中启动服务的需求，并在应用程序之间来回切换。</span><span class="sxs-lookup"><span data-stu-id="63df4-187">It removes the need to launch your service in a browser and switch back and forth between apps.</span></span>

---

## <a name="bots-in-channels"></a><span data-ttu-id="63df4-188">通道中的 bot</span><span class="sxs-lookup"><span data-stu-id="63df4-188">Bots in channels</span></span>

<span data-ttu-id="63df4-189">可以通过对频道中的 bot 进行调用来实现 `@mention` 。</span><span class="sxs-lookup"><span data-stu-id="63df4-189">Invoking a bot in a channel can be accomplished by `@mention`.</span></span> <span data-ttu-id="63df4-190">机器人对话框在通道和组中应是唯一的，而不是一对一方案，通常最好是考虑不同的方法。</span><span class="sxs-lookup"><span data-stu-id="63df4-190">Bot dialog should be unique in channels and groups vs. one-to-one scenarios and it's generally a good idea to consider separate approaches.</span></span> <span data-ttu-id="63df4-191">在下列情况下，尤其如此：</span><span class="sxs-lookup"><span data-stu-id="63df4-191">This is especially true in the following cases:</span></span>

### <a name="sensitive-data-sent-by-a-bot"></a><span data-ttu-id="63df4-192">Bot 发送的敏感数据</span><span class="sxs-lookup"><span data-stu-id="63df4-192">Sensitive data sent by a bot</span></span>

<span data-ttu-id="63df4-193">虽然团队中的用户可以在服务中知道，但实际用户角色却不能。</span><span class="sxs-lookup"><span data-stu-id="63df4-193">While the users in a team can be known to the service, the actual user roles cannot.</span></span> <span data-ttu-id="63df4-194">这意味着，在涉及威胁的教育场景中，不会在团队设置中共享父联系人信息和学生联系人信息。</span><span class="sxs-lookup"><span data-stu-id="63df4-194">This means that, for example, in an education scenario involving bullying, parent and student contact information wouldn't be shared in a team setting.</span></span> <span data-ttu-id="63df4-195">而 bot 的邮件可能是： "今天发生两个威胁事件" 和一个显示详细信息的按钮。</span><span class="sxs-lookup"><span data-stu-id="63df4-195">Instead the bot's message might be,"Two bullying incidents occurred today" along with a button to show details.</span></span>

<span data-ttu-id="63df4-196">在网页中启动详细信息，或任务模块可以提示用户凭据或查询与 AAD 帐户配对的用户角色的索引。</span><span class="sxs-lookup"><span data-stu-id="63df4-196">Launching details in a web page, or a task module can prompt for user credentials or query against an index for user roles paired with AAD accounts.</span></span> <span data-ttu-id="63df4-197">在这两个选项中，数据都在一个专用视图作用域中，并且不会有数据泄露。</span><span class="sxs-lookup"><span data-stu-id="63df4-197">In both of these options the data is in a private view scope and there will be no data leakage.</span></span> <span data-ttu-id="63df4-198">如果在用户与 bot 之间的一对一聊天中发送相同的数据，则该数据仅对该上下文中的用户可见，因此，在 bot 邮件中完全显示该数据是安全的。</span><span class="sxs-lookup"><span data-stu-id="63df4-198">If the same data is sent in a one-to-one chat between a user and the bot, the data is only visible to the user in that context and is, therefore safe, to fully display in the bot message.</span></span> <span data-ttu-id="63df4-199">应避免将用户从频道中提取到一对一聊天，因为这会导致强制导航高度中断。</span><span class="sxs-lookup"><span data-stu-id="63df4-199">Taking users from a channel to a one-to-one chat should be avoided however as that forced navigation is highly disruptive.</span></span>

### <a name="sending-cards-as-a-response-to-interactions"></a><span data-ttu-id="63df4-200">作为交互的响应发送卡片</span><span class="sxs-lookup"><span data-stu-id="63df4-200">Sending cards as a response to interactions</span></span>

<span data-ttu-id="63df4-201">发送轮播卡片以在一对一聊天中*进行漫游*是完全可接受的，相同的模式可能会在活动频道中向大量用户发送数十或数百个*漫游 carousels* 。</span><span class="sxs-lookup"><span data-stu-id="63df4-201">While sending a carousel card in response to *Take a tour* in a one-to-one chat is perfectly acceptable, the same pattern could yield tens or hundreds of *tour carousels* in an active channel with lots of users.</span></span> <span data-ttu-id="63df4-202">为避免这种情况，辅助卡应托管在任务模块中。</span><span class="sxs-lookup"><span data-stu-id="63df4-202">To avoid this, secondary cards should be hosted in a task module.</span></span> <span data-ttu-id="63df4-203">此模式使用户在使用频道的上下文中保持用户的正常，并使频道清除过多的 bot 响应，并且可以选择在显示*漫游*时考虑不同的用户角色。</span><span class="sxs-lookup"><span data-stu-id="63df4-203">This pattern keeps users in context with the channel, keeps the channel clean of excessive bot responses, and can optionally consider different user roles when the *tour* is shown.</span></span>

## <a name="useful-tips"></a><span data-ttu-id="63df4-204">有用的提示</span><span class="sxs-lookup"><span data-stu-id="63df4-204">Useful tips</span></span>

### <a name="x2713-remember-bots-arent-assistants"></a><span data-ttu-id="63df4-205">&#x2713; 记住，bot 不助手</span><span class="sxs-lookup"><span data-stu-id="63df4-205">&#x2713; Remember, bots aren’t assistants</span></span>

<span data-ttu-id="63df4-206">与代理不同，例如 Cortana、bot 充当专家。</span><span class="sxs-lookup"><span data-stu-id="63df4-206">Unlike agents, e.g., Cortana, bots act as specialists.</span></span>

### <a name="x2713-discourage-chitchat"></a><span data-ttu-id="63df4-207">&#x2713; 阻止 chitchat</span><span class="sxs-lookup"><span data-stu-id="63df4-207">&#x2713; Discourage chitchat</span></span>

<span data-ttu-id="63df4-208">除非为对话构建了你的 bot，否则会发现将 chitchat 重定向到任务完成的方法。</span><span class="sxs-lookup"><span data-stu-id="63df4-208">Unless your bot is built for conversation, find ways to redirect chitchat toward task completion.</span></span>

### <a name="x2713-introduce-some-personality"></a><span data-ttu-id="63df4-209">&#x2713; 引入了一些个性</span><span class="sxs-lookup"><span data-stu-id="63df4-209">&#x2713; Introduce some personality</span></span>

<span data-ttu-id="63df4-210">保持你的 bot 个人与你的产品的语音一致。</span><span class="sxs-lookup"><span data-stu-id="63df4-210">Keep your bot personality consistent with the voice of your product.</span></span> <span data-ttu-id="63df4-211">将你的 bot 想象为你的公司说话。</span><span class="sxs-lookup"><span data-stu-id="63df4-211">Think of your bot as speaking for your company.</span></span>

### <a name="x2713-maintain-tone"></a><span data-ttu-id="63df4-212">&#x2713; 保持音调</span><span class="sxs-lookup"><span data-stu-id="63df4-212">&#x2713; Maintain tone</span></span>

<span data-ttu-id="63df4-213">确定您是否希望您的语气是友好和浅、"只是真实" 还是超级 quirky。</span><span class="sxs-lookup"><span data-stu-id="63df4-213">Determine whether you want your tone to be friendly and light, “just the facts”, or super quirky.</span></span>

### <a name="x2713-encourage-easy-task-flow"></a><span data-ttu-id="63df4-214">&#x2713; 鼓励轻松的任务流</span><span class="sxs-lookup"><span data-stu-id="63df4-214">&#x2713; Encourage easy task flow</span></span>

<span data-ttu-id="63df4-215">支持多项交互，同时仍允许完整构建的问题。</span><span class="sxs-lookup"><span data-stu-id="63df4-215">Support multi-turn interactions while still allowing for fully formed questions.</span></span> <span data-ttu-id="63df4-216">预测下一步将帮助用户更轻松地完成任务流。</span><span class="sxs-lookup"><span data-stu-id="63df4-216">Anticipating the next step will help users get through task flows much easier.</span></span>

<span data-ttu-id="63df4-217">如果用户需要几个步骤来完成某项任务，则允许你的 bot 在每个步骤中执行这些步骤，但通过让其建议更快速的途径来完成。</span><span class="sxs-lookup"><span data-stu-id="63df4-217">If a user takes several steps to complete a task, allow your bot to take them through each step, but finish by having it suggest a quicker path.</span></span> <span data-ttu-id="63df4-218">例如，如果用户已进行了多个会话设置，则会设置一个会议（通过先指定一个会议，然后确定要通知的时间，然后指出一天），完成与以下建议的对话：下一次，请尝试询问你是否可以在明天为小明安排会议（明天为1:00）。</span><span class="sxs-lookup"><span data-stu-id="63df4-218">For example, if a user has taken several conversational turns to set a meeting (by first specifying a meeting, then identifying with whom, then stating the time, then stating the day), finish the conversation with the following suggestion: Next time, try asking if you can ‘schedule a meeting with Bob at 1:00 tomorrow’.</span></span>
