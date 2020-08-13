---
title: 什么是 bot？
author: clearab
description: Microsoft 团队中的 bot 概述。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 1e07d56769cbb303f9af98f84c8ae6064325c1a7
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651880"
---
# <a name="what-are-bots"></a><span data-ttu-id="dc679-103">什么是 bot？</span><span class="sxs-lookup"><span data-stu-id="dc679-103">What are bots?</span></span>

<span data-ttu-id="dc679-104">Bot 允许用户通过文本、交互式卡片和任务模块与 web 服务进行交互。</span><span class="sxs-lookup"><span data-stu-id="dc679-104">Bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span> <span data-ttu-id="dc679-105">它们的灵活性非常惊人，您可以通过智能化和自然语言处理的几个简单命令或虚拟助手来处理这些 bot。</span><span class="sxs-lookup"><span data-stu-id="dc679-105">They're incredibly flexible — you can scope bots to handle a few simple commands or virtual assistants powered by artificial intelligence and natural language processing.</span></span> <span data-ttu-id="dc679-106">它们可以是大型应用程序的一个方面，也可以完全独立。</span><span class="sxs-lookup"><span data-stu-id="dc679-106">They can be one aspect of a larger application or completely standalone.</span></span>

<span data-ttu-id="dc679-107">查找卡片、文本和任务模块的正确组合是创建有用的 bot 的关键所在。</span><span class="sxs-lookup"><span data-stu-id="dc679-107">Finding the right mix of cards, text, and task modules is key to creating a useful bot.</span></span> <span data-ttu-id="dc679-108">别忘了，机器人要远不止是文本！</span><span class="sxs-lookup"><span data-stu-id="dc679-108">Don't forget, bots are much more than just text!</span></span>

![FAQ 加 gif](~/assets/images/FAQPlusEndUser.gif)

## <a name="user-scenarios"></a><span data-ttu-id="dc679-110">用户方案</span><span class="sxs-lookup"><span data-stu-id="dc679-110">User scenarios</span></span>

<span data-ttu-id="dc679-111">Microsoft 团队中的 bot 可以是频道、组聊天或一对一聊天的一部分。</span><span class="sxs-lookup"><span data-stu-id="dc679-111">Bots in Microsoft Teams can be part of a channel, group chat, or one-on-one chat.</span></span> <span data-ttu-id="dc679-112">每个范围都将为您的会话 bot 提供独特的机会和挑战。</span><span class="sxs-lookup"><span data-stu-id="dc679-112">Each scope will provide unique opportunities, and challenges, for your conversational bot.</span></span>

### <a name="in-a-channel"></a><span data-ttu-id="dc679-113">通道中</span><span class="sxs-lookup"><span data-stu-id="dc679-113">In a channel</span></span>

<span data-ttu-id="dc679-114">频道包含多人之间的线程对话—可能会有许多人 (目前最多为 2000) 。</span><span class="sxs-lookup"><span data-stu-id="dc679-114">Channels contain threaded conversations between multiple people — potentially lots of people (currently, up to two thousand).</span></span> <span data-ttu-id="dc679-115">这可能会为你的 bot 提供大规模的访问，但各个交互需要简明。</span><span class="sxs-lookup"><span data-stu-id="dc679-115">This potentially gives your bot massive reach, but individual interactions need to be concise.</span></span> <span data-ttu-id="dc679-116">传统的多项交互操作可能不会很好。</span><span class="sxs-lookup"><span data-stu-id="dc679-116">Traditional multi-turn interactions probably won't work well.</span></span> <span data-ttu-id="dc679-117">相反，如果需要收集大量信息，请查看使用互动卡片或任务模块，或者可能将对话移动到一对一对话中。</span><span class="sxs-lookup"><span data-stu-id="dc679-117">Instead, look to use interactive cards or task modules, or potentially move the conversation to a one-to-one conversation if you need to collect lots of information.</span></span> <span data-ttu-id="dc679-118">你的 bot 也只能访问 `@mentioned` 直接邮件，尽管你可以使用 Microsoft Graph 和提升的组织级权限检索来自对话的其他邮件。</span><span class="sxs-lookup"><span data-stu-id="dc679-118">Your bot will also only have access to messages where it's `@mentioned` directly, although you can retrieve additional messages from the conversation using Microsoft Graph and elevated organization-level permissions.</span></span>

<span data-ttu-id="dc679-119">在频道中 excel 的一些应用场景包括：</span><span class="sxs-lookup"><span data-stu-id="dc679-119">Some scenarios where bots excel in a channel include:</span></span>

* <span data-ttu-id="dc679-120">**通知**，尤其是为用户提供用于获取其他信息的互动卡片时。</span><span class="sxs-lookup"><span data-stu-id="dc679-120">**Notifications**, particularly if you provide an interactive card for users to take additional information.</span></span>
* <span data-ttu-id="dc679-121">**反馈方案**，如投票和调查。</span><span class="sxs-lookup"><span data-stu-id="dc679-121">**Feedback scenarios** like polls and surveys.</span></span>
* <span data-ttu-id="dc679-122">可在**单个请求/响应周期**中解决的交互，其中的结果对对话的多个成员很有用。</span><span class="sxs-lookup"><span data-stu-id="dc679-122">Interactions that can be resolved in a **single request/response cycle**, where the results are useful for multiple members of the conversation.</span></span>
* <span data-ttu-id="dc679-123">**社交/趣味 bot** —获取非常棒的 cat 图像，随机挑选获奖者等。</span><span class="sxs-lookup"><span data-stu-id="dc679-123">**Social/fun bots** — get an awesome cat image, randomly pick a winner, etc.</span></span>

### <a name="in-a-group-chat"></a><span data-ttu-id="dc679-124">在群聊中</span><span class="sxs-lookup"><span data-stu-id="dc679-124">In a group chat</span></span>

<span data-ttu-id="dc679-125">组聊天是三个或更多人之间的非线程对话。</span><span class="sxs-lookup"><span data-stu-id="dc679-125">Group chats are non-threaded conversations between three or more people.</span></span> <span data-ttu-id="dc679-126">它们的成员数往往少于通道，并且更具暂时性。</span><span class="sxs-lookup"><span data-stu-id="dc679-126">They tend to have fewer members than a channel, and are more transient.</span></span> <span data-ttu-id="dc679-127">与频道类似，你的 bot 仅可直接访问邮件 `@mentioned` 。</span><span class="sxs-lookup"><span data-stu-id="dc679-127">Similar to a channel, your bot will only have access to messages where it's `@mentioned` directly.</span></span>

<span data-ttu-id="dc679-128">在频道中正常工作的方案通常在组聊天中也会起作用。</span><span class="sxs-lookup"><span data-stu-id="dc679-128">Scenarios that work well in a channel will usually work just as well in a group chat.</span></span>

### <a name="in-a-one-on-one-chat"></a><span data-ttu-id="dc679-129">在一对一聊天中</span><span class="sxs-lookup"><span data-stu-id="dc679-129">In a one-on-one chat</span></span>

<span data-ttu-id="dc679-130">这是对话机器人与用户进行交互的传统方法。</span><span class="sxs-lookup"><span data-stu-id="dc679-130">This is the traditional way for a conversational bot to interact with a user.</span></span> <span data-ttu-id="dc679-131">他们可以实现多元化不同的工作负载。</span><span class="sxs-lookup"><span data-stu-id="dc679-131">They can enable incredibly diverse workloads.</span></span> <span data-ttu-id="dc679-132">问：&bot、在其他系统中启动工作流的 bot、通知笑话的 bot 以及记录笔记的 bot 只是几个示例。</span><span class="sxs-lookup"><span data-stu-id="dc679-132">Q&A bots, bots that initiate workflows in other systems, bots that tell jokes, and bots that take notes are just a few examples.</span></span> <span data-ttu-id="dc679-133">只需记住，应考虑基于会话的界面是否是展示功能的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="dc679-133">Just remember to consider whether a conversation-based interface is the best way to present your functionality.</span></span>

## <a name="building-a-teams-bot-with-the-microsoft-bot-framework"></a><span data-ttu-id="dc679-134">使用 Microsoft Bot 框架构建团队 bot</span><span class="sxs-lookup"><span data-stu-id="dc679-134">Building a Teams bot with the Microsoft Bot Framework</span></span>

<span data-ttu-id="dc679-135">[Microsoft Bot 框架](https://dev.botframework.com/)是一个丰富的 SDK，用于使用 c #、Java、Python 或 JavaScript 构建 bot。</span><span class="sxs-lookup"><span data-stu-id="dc679-135">The [Microsoft Bot Framework](https://dev.botframework.com/) is a rich SDK for building bots using C#, Java, Python, or JavaScript.</span></span> <span data-ttu-id="dc679-136">如果您已经有一个基于 Bot 框架的 bot，您可以轻松地对其进行调整以在 Microsoft 团队中工作。</span><span class="sxs-lookup"><span data-stu-id="dc679-136">If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.</span></span> <span data-ttu-id="dc679-137">我们建议您使用 c # 或 Node.js 来利用我们的[sdk](/microsoftteams/platform/#pivot=sdk-tools)。</span><span class="sxs-lookup"><span data-stu-id="dc679-137">We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="dc679-138">这些包扩展了基本的 Bot 生成器 SDK 类和方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="dc679-138">These packages extend the basic Bot Builder SDK classes and methods as follows:</span></span>

* <span data-ttu-id="dc679-139">使用专用的卡片类型，如 Office 365 连接器卡。</span><span class="sxs-lookup"><span data-stu-id="dc679-139">Use specialized card types like the Office 365 Connector card.</span></span>
* <span data-ttu-id="dc679-140">使用和设置活动的团队特定频道数据。</span><span class="sxs-lookup"><span data-stu-id="dc679-140">Consume and set Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="dc679-141">处理邮件扩展请求。</span><span class="sxs-lookup"><span data-stu-id="dc679-141">Process messaging extension requests.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="dc679-142">您可以在任何 web 编程技术中开发团队应用程序，并直接调用[Bot 框架 REST api](/bot-framework/rest-api/bot-framework-rest-overview) ，但您必须自己执行所有令牌处理。</span><span class="sxs-lookup"><span data-stu-id="dc679-142">You can develop Teams apps in any web programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

<span data-ttu-id="dc679-143">你的团队 bot 由三个元素组成：</span><span class="sxs-lookup"><span data-stu-id="dc679-143">Your Teams bot consists of three elements:</span></span>

* <span data-ttu-id="dc679-144">您承载的可公开访问的 web 服务。</span><span class="sxs-lookup"><span data-stu-id="dc679-144">A publicly accessible web service that you host.</span></span>
* <span data-ttu-id="dc679-145">使用 Bot 框架的 bot 注册。</span><span class="sxs-lookup"><span data-stu-id="dc679-145">Your bot registration with the Bot Framework.</span></span>
* <span data-ttu-id="dc679-146">您的团队应用程序包与您的应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="dc679-146">Your Teams app package with your app manifest.</span></span> <span data-ttu-id="dc679-147">这是用户将安装的内容，并将团队客户端连接到 web 服务，并通过 Bot 服务进行路由。</span><span class="sxs-lookup"><span data-stu-id="dc679-147">This is what your users will install and connects the Teams client to your web service, routed through the Bot Service.</span></span>

> [!TIP]
> <span data-ttu-id="dc679-148">团队应用程序 Studio \* 可帮助您创建和配置您的应用程序清单，并可将您的 web 服务注册为 Bot 框架上的 bot。</span><span class="sxs-lookup"><span data-stu-id="dc679-148">Teams App Studio\* helps you create and configure your app manifest and can register your web service as a bot on the Bot Framework.</span></span> <span data-ttu-id="dc679-149">它还包含响应控制库和交互式卡片生成器。</span><span class="sxs-lookup"><span data-stu-id="dc679-149">It also contains a React control library and an interactive card builder.</span></span> <span data-ttu-id="dc679-150">*请参阅*[开始使用团队应用 Studio](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="dc679-150">*See* [Getting started with Teams App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="building-a-teams-bot-with-microsoft-power-virtual-agents"></a><span data-ttu-id="dc679-151">使用 Microsoft Power Virtual 代理构建团队 bot</span><span class="sxs-lookup"><span data-stu-id="dc679-151">Building a Teams bot with Microsoft Power Virtual Agents</span></span>

<span data-ttu-id="dc679-152">[电源虚拟代理](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)是在 Microsoft Power Platform 和 Bot 框架上构建的一项服务。</span><span class="sxs-lookup"><span data-stu-id="dc679-152">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) is a service built on the Microsoft Power platform and Bot Framework.</span></span> <span data-ttu-id="dc679-153">Power Virtual Agent 开发过程使用无代码的图形界面方法，使团队的每个成员都能轻松创建和维护智能虚拟代理。</span><span class="sxs-lookup"><span data-stu-id="dc679-153">The Power Virtual Agent development process uses a guided, no-code, graphical interface approach to empower every member of your team to easily create and maintain an intelligent virtual agent.</span></span> <span data-ttu-id="dc679-154">在[Power Virtual agent 门户](https://powervirtualagents.microsoft.com)中完成创建 chatbot 后，可以轻松地[将 Power virtual Agent chatbot 与团队集成](../../bots/how-to/add-power-virtual-agents-bot-to-teams.md)。</span><span class="sxs-lookup"><span data-stu-id="dc679-154">Once you have completed creating your chatbot in the [Power Virtual Agents portal](https://powervirtualagents.microsoft.com), you can easily [integrate your Power Virtual Agents chatbot with Teams](../../bots/how-to/add-power-virtual-agents-bot-to-teams.md).</span></span> <span data-ttu-id="dc679-155">若要开始创建电源虚拟代理 chatbot，*请参阅* [power virtual agent 文档](https://docs.microsoft.com/power-virtual-agents/)。</span><span class="sxs-lookup"><span data-stu-id="dc679-155">To get started creating your Power Virtual Agents chatbot, *see* the [Power Virtual Agents documentation](https://docs.microsoft.com/power-virtual-agents/).</span></span>

## <a name="connectors-and-bots"></a><span data-ttu-id="dc679-156">连接器和 bot</span><span class="sxs-lookup"><span data-stu-id="dc679-156">Connectors and bots</span></span>

<span data-ttu-id="dc679-157">连接器允许您创建简单的 bot 进行基本交互，如启动脱离工作流或其他简单命令。</span><span class="sxs-lookup"><span data-stu-id="dc679-157">Connectors allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands.</span></span> <span data-ttu-id="dc679-158">它们仅在您创建它们的团队中运行，适用于特定于贵公司的工作流的简单流程。</span><span class="sxs-lookup"><span data-stu-id="dc679-158">They live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="dc679-159">*请参阅*[什么是 webhook 和连接器？](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)有关详细信息，请参阅。</span><span class="sxs-lookup"><span data-stu-id="dc679-159">*See* [What are webhooks and connectors?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) for more information.</span></span>

## <a name="bot-fails"></a><span data-ttu-id="dc679-160">机器人失败</span><span class="sxs-lookup"><span data-stu-id="dc679-160">Bot fails</span></span>

### <a name="having-multi-turn-experiences-in-chat"></a><span data-ttu-id="dc679-161">在聊天中拥有多轮体验</span><span class="sxs-lookup"><span data-stu-id="dc679-161">Having multi-turn experiences in chat</span></span>

<span data-ttu-id="dc679-162">您的 bot 和用户之间的一个广泛的对话框是一种缓慢且过于复杂的方法来使任务完成，还需要开发人员维护状态。</span><span class="sxs-lookup"><span data-stu-id="dc679-162">An extensive dialog between your bot and the user is a slow and overly complex way to get a task completed and it also requires the developer to maintain state.</span></span> <span data-ttu-id="dc679-163">若要退出此状态，用户必须是超时时间或键入 "*取消*"。</span><span class="sxs-lookup"><span data-stu-id="dc679-163">To exit this state a user must either time-out or type “*Cancel*”.</span></span> <span data-ttu-id="dc679-164">在所有情况下，此过程是不必要的单调操作：</span><span class="sxs-lookup"><span data-stu-id="dc679-164">Above all, the process is unnecessarily tedious:</span></span>

<span data-ttu-id="dc679-165">用户：使用 Megan 安排会议。</span><span class="sxs-lookup"><span data-stu-id="dc679-165">USER: Schedule a meeting with Megan.</span></span>

<span data-ttu-id="dc679-166">BOT：我发现了200结果，请包含姓和名。</span><span class="sxs-lookup"><span data-stu-id="dc679-166">BOT: I’ve found 200 results, please include a first and last name.</span></span>

<span data-ttu-id="dc679-167">用户：使用 Megan Bowen 安排会议。</span><span class="sxs-lookup"><span data-stu-id="dc679-167">USER: Schedule a meeting with Megan Bowen.</span></span>

<span data-ttu-id="dc679-168">机器人：好了，您想要使用 Megan Bowen 来满足什么时间？</span><span class="sxs-lookup"><span data-stu-id="dc679-168">BOT: OK, what time would you like to meet with Megan Bowen?</span></span>

<span data-ttu-id="dc679-169">用户： 1:00 pm。</span><span class="sxs-lookup"><span data-stu-id="dc679-169">USER: 1:00 pm.</span></span>

<span data-ttu-id="dc679-170">机器人：在哪天？</span><span class="sxs-lookup"><span data-stu-id="dc679-170">BOT: On which day?</span></span>

### <a name="supporting-too-many-commands"></a><span data-ttu-id="dc679-171">支持的命令过多</span><span class="sxs-lookup"><span data-stu-id="dc679-171">Supporting too many commands</span></span>

<span data-ttu-id="dc679-172">用户不能成功或查看不支持过多命令的 bot （尤其是一系列命令）。</span><span class="sxs-lookup"><span data-stu-id="dc679-172">A bot that supports excessive commands, especially a broad range of commands, will not be successful or viewed positively by users.</span></span> <span data-ttu-id="dc679-173">由于当前机器人菜单中只有6个可见的命令，因此任何频率都不大可能使用。</span><span class="sxs-lookup"><span data-stu-id="dc679-173">Since there are only 6 visible commands in the current bot menu, anything more is unlikely to be used with any frequency.</span></span> <span data-ttu-id="dc679-174">深入了解特定区域的 bot，而不是尝试成为一家广泛的助理将会更好地发挥作用并 fare。</span><span class="sxs-lookup"><span data-stu-id="dc679-174">Bots that go deep into a specific area rather than trying to be a broad assistant will work and fare better.</span></span>

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a><span data-ttu-id="dc679-175">使用 unranked 响应维护大型检索知识库</span><span class="sxs-lookup"><span data-stu-id="dc679-175">Maintaining a large retrieval knowledge base with unranked responses</span></span>

<span data-ttu-id="dc679-176">Bot 最适用于简短的快速交互，而不是 sifting 通过长列表查找答案。</span><span class="sxs-lookup"><span data-stu-id="dc679-176">Bots are best suited for short, quick interactions, not sifting through long lists looking for an answer.</span></span>

## <a name="get-started"></a><span data-ttu-id="dc679-177">入门</span><span class="sxs-lookup"><span data-stu-id="dc679-177">Get started</span></span>

* [<span data-ttu-id="dc679-178">C # 中的团队对话机器人/dotnet</span><span class="sxs-lookup"><span data-stu-id="dc679-178">Teams conversation bot in C#/dotnet</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [<span data-ttu-id="dc679-179">JavaScript 中的 Teams 对话机器人</span><span class="sxs-lookup"><span data-stu-id="dc679-179">Teams conversation bot in JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a><span data-ttu-id="dc679-180">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="dc679-180">Learn more</span></span>

* [<span data-ttu-id="dc679-181">团队中的 bot 的基础知识</span><span class="sxs-lookup"><span data-stu-id="dc679-181">The basics of bots in Teams</span></span>](~/bots/bot-basics.md)
* [<span data-ttu-id="dc679-182">创建适合 Teams 的机器人</span><span class="sxs-lookup"><span data-stu-id="dc679-182">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)
* [<span data-ttu-id="dc679-183">规划应用程序</span><span class="sxs-lookup"><span data-stu-id="dc679-183">Planning your app</span></span>](../../concepts/extensibility-points.md)
* <span data-ttu-id="dc679-184">[正在设计您的应用程序] .。。/ ( .。。/designing-your-app/designing-overview.md) </span><span class="sxs-lookup"><span data-stu-id="dc679-184">[Designing your app]../(../designing-your-app/designing-overview.md)</span></span>
* [<span data-ttu-id="dc679-185">生成应用程序</span><span class="sxs-lookup"><span data-stu-id="dc679-185">Building your app</span></span>](../../concepts/building-an-app.md)
* [<span data-ttu-id="dc679-186">发布应用程序</span><span class="sxs-lookup"><span data-stu-id="dc679-186">Publishing your app</span></span>](../../concepts/deploy-and-publish/overview.md)
