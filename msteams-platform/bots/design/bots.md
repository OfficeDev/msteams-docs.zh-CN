---
title: Bot 设计指南
description: 介绍创建 bot 的指南
keywords: 团队设计指南参考框架 bot 对话
ms.openlocfilehash: f59a1e9c280f27567692b4d10341db79d05c3464
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673411"
---
# <a name="start-talking-with-bots"></a><span data-ttu-id="50a51-104">开始与 bot 对话</span><span class="sxs-lookup"><span data-stu-id="50a51-104">Start talking with bots</span></span>

<span data-ttu-id="50a51-105">Bot 是执行一组较窄或特定任务的会话式应用程序。</span><span class="sxs-lookup"><span data-stu-id="50a51-105">Bots are conversational apps that perform a narrow or specific set of tasks.</span></span> <span data-ttu-id="50a51-106">它们为您提供了与用户进行通信的机会，回答了他们的问题，并主动通知他们发生了哪些更改。</span><span class="sxs-lookup"><span data-stu-id="50a51-106">They give you an opportunity to communicate with users, respond to their questions, and proactively notify them about changes.</span></span> <span data-ttu-id="50a51-107">这是一种很好的方法。</span><span class="sxs-lookup"><span data-stu-id="50a51-107">They’re a great way to reach out.</span></span>

---

## <a name="guidelines"></a><span data-ttu-id="50a51-108">准则</span><span class="sxs-lookup"><span data-stu-id="50a51-108">Guidelines</span></span>

### <a name="avatars"></a><span data-ttu-id="50a51-109">虚拟形象</span><span class="sxs-lookup"><span data-stu-id="50a51-109">Avatars</span></span>

<span data-ttu-id="50a51-110">在团队中，Bot 虚拟形象的形状类似于六边形，因此人们可以快速判断他们正在与某个 bot 而不是某人交谈。</span><span class="sxs-lookup"><span data-stu-id="50a51-110">Bot avatars in Teams are shaped like hexagons so people can quickly tell that they’re talking to a bot instead of a person.</span></span> <span data-ttu-id="50a51-111">你将头像作为方块提交，我们将为你进行裁剪。</span><span class="sxs-lookup"><span data-stu-id="50a51-111">You’ll submit your avatar as a square and we’ll crop it for you.</span></span> <span data-ttu-id="50a51-112">当遇到虚拟形象时，我们建议您让您能够在2英尺和使用较高的对比度的情况下清晰地消失。</span><span class="sxs-lookup"><span data-stu-id="50a51-112">When it comes to avatars, we recommend making yours legible from 2 feet away and using a higher contrast.</span></span>

[!include[Avatar image](~/includes/design/bot-avatar-image.html)]

### <a name="buttons"></a><span data-ttu-id="50a51-113">按钮</span><span class="sxs-lookup"><span data-stu-id="50a51-113">Buttons</span></span>

<span data-ttu-id="50a51-114">我们每张卡片最长支持六个按钮。</span><span class="sxs-lookup"><span data-stu-id="50a51-114">We support up to six buttons per card.</span></span> <span data-ttu-id="50a51-115">编写按钮文本时请务必简明扼要，并且请注意，大多数按钮应仅处理手头的任务。</span><span class="sxs-lookup"><span data-stu-id="50a51-115">Be concise when writing button text, and keep in mind that most buttons should only address the task at hand.</span></span>

### <a name="graphics"></a><span data-ttu-id="50a51-116">图形</span><span class="sxs-lookup"><span data-stu-id="50a51-116">Graphics</span></span>

<span data-ttu-id="50a51-117">图形是一种很不错的说明，但并不是所有机器人对话都需要图形，因此使用它们来获得最大影响。</span><span class="sxs-lookup"><span data-stu-id="50a51-117">Graphics are a good way to tell a story, but not all bot conversations require graphics, so use them for maximum impact.</span></span>

### <a name="responding-to-users-and-failing-gracefully"></a><span data-ttu-id="50a51-118">响应用户并顺利进行故障转移</span><span class="sxs-lookup"><span data-stu-id="50a51-118">Responding to users and failing gracefully</span></span>

<span data-ttu-id="50a51-119">你的 bot 还应能够在考虑常见的拼写错误和俗语时，对诸如 "Hi"、"帮助" 和 "谢谢" 这样的事情做出响应。</span><span class="sxs-lookup"><span data-stu-id="50a51-119">Your bot should also be able to respond to things like 'Hi', 'Help', and 'Thanks' while taking common misspellings and colloquialisms into account.</span></span> <span data-ttu-id="50a51-120">例如：</span><span class="sxs-lookup"><span data-stu-id="50a51-120">For example:</span></span>

#### <a name="x2713-hello"></a><span data-ttu-id="50a51-121">&#x2713; Hello</span><span class="sxs-lookup"><span data-stu-id="50a51-121">&#x2713; Hello</span></span>

<span data-ttu-id="50a51-122">`Hi` `how are you` `howdy`</span><span class="sxs-lookup"><span data-stu-id="50a51-122">`Hi` `how are you` `howdy`</span></span>

#### <a name="x2713-help"></a><span data-ttu-id="50a51-123">&#x2713; 帮助</span><span class="sxs-lookup"><span data-stu-id="50a51-123">&#x2713; Help</span></span>

<span data-ttu-id="50a51-124">`What do you do?` `How does this work?` `What the heck?`</span><span class="sxs-lookup"><span data-stu-id="50a51-124">`What do you do?` `How does this work?` `What the heck?`</span></span>

#### <a name="x2713-thanks"></a><span data-ttu-id="50a51-125">&#x2713; 感谢</span><span class="sxs-lookup"><span data-stu-id="50a51-125">&#x2713; Thanks</span></span>

<span data-ttu-id="50a51-126">`Thank you` `thankyou` `thx`</span><span class="sxs-lookup"><span data-stu-id="50a51-126">`Thank you` `thankyou` `thx`</span></span>

<span data-ttu-id="50a51-127">你的 bot 应能够处理以下类型的查询和输入：</span><span class="sxs-lookup"><span data-stu-id="50a51-127">Your bot should be able to handle the following types of queries and inputs:</span></span>

* <span data-ttu-id="50a51-128">**识别的问题**：这些是用户预计会遇到的 "最佳方案" 问题。</span><span class="sxs-lookup"><span data-stu-id="50a51-128">**Recognized questions**: These are the “best case scenario” questions you’d anticipate from users.</span></span>
* <span data-ttu-id="50a51-129">**可识别的无问题**：查询不受支持的功能、随机的信息，或当有人想在你的 bot 咒骂时。</span><span class="sxs-lookup"><span data-stu-id="50a51-129">**Recognized non-questions**: Queries about unsupported functionality, random pieces of information, or when someone wants to curse at your bot.</span></span>
* <span data-ttu-id="50a51-130">**无法识别的问题：无法**识别的输入（例如，杂乱）。</span><span class="sxs-lookup"><span data-stu-id="50a51-130">**Unrecognized questions**: Unintelligible inputs (i.e., gibberish).</span></span>

<span data-ttu-id="50a51-131">Bot 的个性和响应类型的示例：</span><span class="sxs-lookup"><span data-stu-id="50a51-131">Examples of bot personality and response types:</span></span>

[!include[Bot responses](~/includes/design/bot-responses-table.html)]

> [!TIP]
> <span data-ttu-id="50a51-132">编写机器人脚本时，请询问自己： "我的公司是否为 embarrassed 如果响应是通过屏幕捕获并共享吗？"</span><span class="sxs-lookup"><span data-stu-id="50a51-132">When writing your bot script, ask yourself: “Will my company be embarrassed if a response is screen captured and shared?”</span></span>

### <a name="understanding-what-users-are-trying-to-say"></a><span data-ttu-id="50a51-133">了解用户试图说出的内容</span><span class="sxs-lookup"><span data-stu-id="50a51-133">Understanding what users are trying to say</span></span>

#### <a name="use-a-thesaurus-for-synonyms"></a><span data-ttu-id="50a51-134">对同义词使用同义词库</span><span class="sxs-lookup"><span data-stu-id="50a51-134">Use a thesaurus for synonyms</span></span>

<span data-ttu-id="50a51-135">当灵感触发变体时，请使用同义词库并从尽可能多的不同背景中获取人员，以帮助您生成每个查询的不同解释。</span><span class="sxs-lookup"><span data-stu-id="50a51-135">When brainstorming variants, use a thesaurus and get people from as many different backgrounds as possible to help you generate different interpretations of each query.</span></span>

#### <a name="make-use-of-telemetry-and-interviews"></a><span data-ttu-id="50a51-136">使用遥测和访谈</span><span class="sxs-lookup"><span data-stu-id="50a51-136">Make use of telemetry and interviews</span></span>

<span data-ttu-id="50a51-137">了解用户在查询你的 bot 时所说的含义以及它们的意图。</span><span class="sxs-lookup"><span data-stu-id="50a51-137">Find out what users are saying and what was their intent when querying your bot.</span></span> <span data-ttu-id="50a51-138">当你在不同位置和公司类型中获取用户时，这将是一个持续的过程。</span><span class="sxs-lookup"><span data-stu-id="50a51-138">This will be an ongoing process as you get users in different locations and types of companies.</span></span> <span data-ttu-id="50a51-139">您可以使用语言理解智能服务（[LUIS](/azure/cognitive-services/luis/what-is-luis)）微调语言识别和意图映射。</span><span class="sxs-lookup"><span data-stu-id="50a51-139">You can fine-tune language recognition and intent mapping with Language Understanding Intelligent Service ([LUIS](/azure/cognitive-services/luis/what-is-luis)).</span></span>

### <a name="how-often-should-you-use-your-bot-to-reach-out-to-a-user"></a><span data-ttu-id="50a51-140">应多长时间使用你的 bot 与用户联系？</span><span class="sxs-lookup"><span data-stu-id="50a51-140">How often should you use your bot to reach out to a user?</span></span>

#### <a name="x2713-when-a-state-has-changed"></a><span data-ttu-id="50a51-141">状态更改时 &#x2713;</span><span class="sxs-lookup"><span data-stu-id="50a51-141">&#x2713; When a state has changed</span></span>

<span data-ttu-id="50a51-142">例如，如果工作分配标记为 "已完成"、"bug 更改时"、"新社交媒体可用" 或 "已完成轮询"。</span><span class="sxs-lookup"><span data-stu-id="50a51-142">For example, if an assignment is marked as complete, when a bug changes, when new social media is available, or when a poll has been completed.</span></span>

#### <a name="x2713-when-the-timing-is-right"></a><span data-ttu-id="50a51-143">当计时正确时 &#x2713;</span><span class="sxs-lookup"><span data-stu-id="50a51-143">&#x2713; When the timing is right</span></span>

<span data-ttu-id="50a51-144">你的 bot 可以像每日摘要那样操作，以特定频率向用户或频道发送通知。</span><span class="sxs-lookup"><span data-stu-id="50a51-144">Your bot can act like a daily digest, sending a notification to the user or channel at a specific frequency.</span></span>

<span data-ttu-id="50a51-145">将用户保持在控制之下。</span><span class="sxs-lookup"><span data-stu-id="50a51-145">Leave the user in control.</span></span> <span data-ttu-id="50a51-146">提供包括频率和优先级的通知设置。</span><span class="sxs-lookup"><span data-stu-id="50a51-146">Provide notification settings that include frequency and priority.</span></span>

[!include[Bot notification](~/includes/design/bot-notification-image.html)]

---

## <a name="using-tabs"></a><span data-ttu-id="50a51-147">使用选项卡</span><span class="sxs-lookup"><span data-stu-id="50a51-147">Using tabs</span></span>

<span data-ttu-id="50a51-148">选项卡使你的 bot 功能更强大。</span><span class="sxs-lookup"><span data-stu-id="50a51-148">Tabs make your bot much more functional.</span></span> <span data-ttu-id="50a51-149">通过选项卡，您可以创建以下内容：</span><span class="sxs-lookup"><span data-stu-id="50a51-149">With tabs, you can create the following:</span></span>

### <a name="x2713-a-place-to-host-standing-queries"></a><span data-ttu-id="50a51-150">&#x2713; 承载驻留查询的位置</span><span class="sxs-lookup"><span data-stu-id="50a51-150">&#x2713; A place to host standing queries</span></span>

<span data-ttu-id="50a51-151">在 bot 和单个用户之间的个人对话中，选项卡可以容纳用户特定的信息和列表。</span><span class="sxs-lookup"><span data-stu-id="50a51-151">In personal conversations between a bot and a single person, tabs can house user-specific information and lists.</span></span> <span data-ttu-id="50a51-152">它们也是维护对常见问题（Faq）的 bot 响应的理想位置，因此用户无需继续提问。</span><span class="sxs-lookup"><span data-stu-id="50a51-152">They’re also a good place to maintain bot responses to frequently-asked questions (FAQs) — so users don’t need to keep asking.</span></span>

### <a name="x2713-a-place-to-finish-a-conversation"></a><span data-ttu-id="50a51-153">&#x2713; 完成对话的位置</span><span class="sxs-lookup"><span data-stu-id="50a51-153">&#x2713; A place to finish a conversation</span></span>

<span data-ttu-id="50a51-154">您可以从卡片链接到选项卡。</span><span class="sxs-lookup"><span data-stu-id="50a51-154">You can link to a tab from a card.</span></span> <span data-ttu-id="50a51-155">如果你的 bot 提供了需要更多步骤的答案，则它可以链接到选项卡以完成任务或流。</span><span class="sxs-lookup"><span data-stu-id="50a51-155">If your bot provides an answer that requires a few more steps, it can link to a tab to complete the task or flow.</span></span>

### <a name="x2713-a-place-to-provide-some-help"></a><span data-ttu-id="50a51-156">&#x2713; 提供一些帮助的位置</span><span class="sxs-lookup"><span data-stu-id="50a51-156">&#x2713; A place to provide some help</span></span>

<span data-ttu-id="50a51-157">添加一个选项卡，educates 用户如何与你的 bot 进行通信。</span><span class="sxs-lookup"><span data-stu-id="50a51-157">Add a tab that educates users about how to communicate with your bot.</span></span> <span data-ttu-id="50a51-158">您可以为其所做的操作或 Faq 提供一些上下文。</span><span class="sxs-lookup"><span data-stu-id="50a51-158">You can provide some context for what it does or FAQs.</span></span>

![提供帮助](~/assets/images/framework/framework_bots_tbot-help.png)

> [!TIP]
> <span data-ttu-id="50a51-160">在选项卡中嵌入网站的各个部分可帮助某人在使用您的服务时维护对话的上下文。</span><span class="sxs-lookup"><span data-stu-id="50a51-160">Embedding parts of your site in a tab will help someone maintain the context of a conversation as they use your service.</span></span> <span data-ttu-id="50a51-161">它消除了在浏览器中启动服务的需求，并在应用程序之间来回切换。</span><span class="sxs-lookup"><span data-stu-id="50a51-161">It removes the need to launch your service in a browser and switch back and forth between apps.</span></span>

---

## <a name="best-practices"></a><span data-ttu-id="50a51-162">最佳做法</span><span class="sxs-lookup"><span data-stu-id="50a51-162">Best practices</span></span>

### <a name="x2713-bots-arent-assistants"></a><span data-ttu-id="50a51-163">&#x2713; Bot 不助手</span><span class="sxs-lookup"><span data-stu-id="50a51-163">&#x2713; Bots aren’t assistants</span></span>

<span data-ttu-id="50a51-164">与代理不同，例如 Cortana、bot 充当专家。</span><span class="sxs-lookup"><span data-stu-id="50a51-164">Unlike agents, e.g., Cortana, bots act as specialists.</span></span>

### <a name="x2713-discourage-chitchat"></a><span data-ttu-id="50a51-165">&#x2713; 阻止 chitchat</span><span class="sxs-lookup"><span data-stu-id="50a51-165">&#x2713; Discourage chitchat</span></span>

<span data-ttu-id="50a51-166">除非为对话构建了你的 bot，否则会发现将 chitchat 重定向到任务完成的方法。</span><span class="sxs-lookup"><span data-stu-id="50a51-166">Unless your bot is built for conversation, find ways to redirect chitchat toward task completion.</span></span>

### <a name="x2713-introduce-some-personality"></a><span data-ttu-id="50a51-167">&#x2713; 引入了一些个性</span><span class="sxs-lookup"><span data-stu-id="50a51-167">&#x2713; Introduce some personality</span></span>

<span data-ttu-id="50a51-168">保持你的 bot 个人与你的产品的语音一致。</span><span class="sxs-lookup"><span data-stu-id="50a51-168">Keep your bot personality consistent with the voice of your product.</span></span> <span data-ttu-id="50a51-169">将你的 bot 想象为你的公司说话。</span><span class="sxs-lookup"><span data-stu-id="50a51-169">Think of your bot as speaking for your company.</span></span>

### <a name="x2713-maintain-tone"></a><span data-ttu-id="50a51-170">&#x2713; 保持音调</span><span class="sxs-lookup"><span data-stu-id="50a51-170">&#x2713; Maintain tone</span></span>

<span data-ttu-id="50a51-171">确定您是否希望您的语气是友好和浅、"只是真实" 还是超级 quirky。</span><span class="sxs-lookup"><span data-stu-id="50a51-171">Determine whether you want your tone to be friendly and light, “just the facts”, or super quirky.</span></span>

### <a name="x2713-encourage-easy-task-flow"></a><span data-ttu-id="50a51-172">&#x2713; 鼓励轻松的任务流</span><span class="sxs-lookup"><span data-stu-id="50a51-172">&#x2713; Encourage easy task flow</span></span>

<span data-ttu-id="50a51-173">支持多项交互，同时仍允许完整构建的问题。</span><span class="sxs-lookup"><span data-stu-id="50a51-173">Support multi-turn interactions while still allowing for fully formed questions.</span></span> <span data-ttu-id="50a51-174">预测下一步将帮助用户更轻松地完成任务流。</span><span class="sxs-lookup"><span data-stu-id="50a51-174">Anticipating the next step will help users get through task flows much easier.</span></span>

<span data-ttu-id="50a51-175">如果用户需要几个步骤来完成某项任务，则允许你的 bot 在每个步骤中执行这些步骤，但通过让其建议更快速的途径来完成。</span><span class="sxs-lookup"><span data-stu-id="50a51-175">If a user takes several steps to complete a task, allow your bot to take them through each step, but finish by having it suggest a quicker path.</span></span> <span data-ttu-id="50a51-176">例如，如果用户已进行了多个会话设置，则会设置一个会议（通过先指定一个会议，然后确定要通知的时间，然后指出一天），使用以下建议完成对话：下一次，请尝试询问您是否可以 "安排在明天1:00 的 Bob 开会"。</span><span class="sxs-lookup"><span data-stu-id="50a51-176">For example, if a user has taken several conversational turns to set a meeting (by first specifying a meeting, then identifying with whom, then stating the time, then stating the day), finish the conversation with the following suggestion: Next time, try asking if you can ‘schedule a meeting with Bob at 1:00 tomorrow’.</span></span>