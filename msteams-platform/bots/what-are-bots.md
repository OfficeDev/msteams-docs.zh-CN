---
title: 什么是对话 bot？
author: clearab
description: Microsoft 团队中的会话 bot 概述。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 6f1ce3cf905b0c638652784fdc76b37ea0f6aca9
ms.sourcegitcommit: 28af65730884b788ff77a4ec4032219380df8b70
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2020
ms.locfileid: "44281844"
---
# <a name="what-are-conversational-bots"></a><span data-ttu-id="7102b-103">什么是对话 bot？</span><span class="sxs-lookup"><span data-stu-id="7102b-103">What are conversational bots?</span></span>

<span data-ttu-id="7102b-104">会话 bot 使用户能够通过文本、交互式卡片和任务模块与 web 服务进行交互。</span><span class="sxs-lookup"><span data-stu-id="7102b-104">Conversational bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span> <span data-ttu-id="7102b-105">它们的灵活性非常灵活—会话间的 bot 可用于处理几个简单的命令或复杂、人工智能化的工作和自然语言处理的虚拟助手。</span><span class="sxs-lookup"><span data-stu-id="7102b-105">They're incredibly flexible — conversational bots can be scoped to handling a few simple commands or complex, artificial-intelligence-powered and natural-language-processing virtual assistants.</span></span> <span data-ttu-id="7102b-106">它们可以是大型应用程序的一个方面，也可以完全独立。</span><span class="sxs-lookup"><span data-stu-id="7102b-106">They can be one aspect of a larger application, or completely stand-alone.</span></span>

<span data-ttu-id="7102b-107">下面的 GIF 显示了用户使用文本和交互式卡片同时在一对一聊天中与 bot 聊天。</span><span class="sxs-lookup"><span data-stu-id="7102b-107">The GIF below shows a user conversing with a bot in a one-to-one chat using both text and interactive cards.</span></span> <span data-ttu-id="7102b-108">查找卡片、文本和任务模块的正确组合是创建有用的 bot 的关键所在。</span><span class="sxs-lookup"><span data-stu-id="7102b-108">Finding the right mix of cards, text, and task modules is key to creating a useful bot.</span></span> <span data-ttu-id="7102b-109">别忘了，机器人要远不止是文本！</span><span class="sxs-lookup"><span data-stu-id="7102b-109">Don't forget, bots are much more than just text!</span></span>

![FAQ 加 gif](~/assets/images/FAQPlusEndUser.gif)

## <a name="build--a-bot-for-teams-with-the-microsoft-bot-framework"></a><span data-ttu-id="7102b-111">为使用 Microsoft Bot 框架的团队构建 bot</span><span class="sxs-lookup"><span data-stu-id="7102b-111">Build  a bot for Teams with the Microsoft Bot Framework</span></span>

<span data-ttu-id="7102b-112">Microsoft Bot 框架] （ https://dev.botframework.com/) 是一种丰富的 SDK，用于使用 c #、Java、Python 和 JavaScript 构建 bot。</span><span class="sxs-lookup"><span data-stu-id="7102b-112">The Microsoft Bot Framework](https://dev.botframework.com/) is a rich SDK for building bots using C#, Java, Python, and JavaScript.</span></span> <span data-ttu-id="7102b-113">如果您已经有一个基于 Bot 框架的 bot，您可以轻松地对其进行调整以在 Microsoft 团队中工作。</span><span class="sxs-lookup"><span data-stu-id="7102b-113">If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.</span></span> <span data-ttu-id="7102b-114">我们建议您使用 c # 或 node.js 来利用我们的[sdk](/microsoftteams/platform/#pivot=sdk-tools)。</span><span class="sxs-lookup"><span data-stu-id="7102b-114">We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="7102b-115">这些包扩展了基本的 Bot 生成器 SDK 类和方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7102b-115">These packages extend the basic Bot Builder SDK classes and methods as follows:</span></span>

* <span data-ttu-id="7102b-116">使用专用的卡片类型，如 Office 365 连接器卡。</span><span class="sxs-lookup"><span data-stu-id="7102b-116">Use specialized card types like the Office 365 Connector card.</span></span>
* <span data-ttu-id="7102b-117">使用和设置活动的团队特定频道数据。</span><span class="sxs-lookup"><span data-stu-id="7102b-117">Consume and set Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="7102b-118">处理邮件扩展请求。</span><span class="sxs-lookup"><span data-stu-id="7102b-118">Process messaging extension requests.</span></span>

<span data-ttu-id="7102b-119">你的团队 bot 由三个元素组成：</span><span class="sxs-lookup"><span data-stu-id="7102b-119">Your Teams bot consists of three elements:</span></span>

* <span data-ttu-id="7102b-120">您承载的可公开访问的 web 服务。</span><span class="sxs-lookup"><span data-stu-id="7102b-120">A publicly accessible web service that you host.</span></span>
* <span data-ttu-id="7102b-121">使用 Bot 框架的 bot 注册。</span><span class="sxs-lookup"><span data-stu-id="7102b-121">Your bot registration with the Bot Framework.</span></span>
* <span data-ttu-id="7102b-122">您的团队应用程序包与您的应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="7102b-122">Your Teams app package with your app manifest.</span></span> <span data-ttu-id="7102b-123">这是用户将安装的内容，并将团队客户端连接到 web 服务，并通过 Bot 服务进行路由。</span><span class="sxs-lookup"><span data-stu-id="7102b-123">This is what your users will install and connects the Teams client to your web service, routed through the Bot Service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="7102b-124">您可以在任何 web 编程技术中开发团队应用程序，并直接调用[Bot 框架 REST api](/bot-framework/rest-api/bot-framework-rest-overview) ，但您必须自己执行所有令牌处理。</span><span class="sxs-lookup"><span data-stu-id="7102b-124">You can develop Teams apps in any web-programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

> [!TIP]
> <span data-ttu-id="7102b-125">团队应用程序 Studio \* 可帮助您创建和配置应用程序清单，并可将 web 服务注册为 Bot 框架上的 bot。</span><span class="sxs-lookup"><span data-stu-id="7102b-125">Teams App Studio\* helps you create and configure your app manifest, and can register your web service as a bot on the Bot Framework.</span></span> <span data-ttu-id="7102b-126">它还包含响应控制库和交互式卡片生成器。</span><span class="sxs-lookup"><span data-stu-id="7102b-126">It also contains a React control library and an interactive card builder.</span></span> <span data-ttu-id="7102b-127">*请参阅*[开始使用团队应用 Studio](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7102b-127">*See* [Getting started with Teams App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="create-a-chatbot-for-teams-with-microsoft-power-virtual-agents"></a><span data-ttu-id="7102b-128">为具有 Microsoft Power Virtual 代理的团队创建 chatbot</span><span class="sxs-lookup"><span data-stu-id="7102b-128">Create a chatbot for Teams with Microsoft Power Virtual Agents</span></span>

<span data-ttu-id="7102b-129">[电源虚拟代理](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)是一个基于 Microsoft Power Platform 和 Bot 框架构建的 chatbot 服务。</span><span class="sxs-lookup"><span data-stu-id="7102b-129">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) is a chatbot service, built on the Microsoft Power platform and Bot Framework.</span></span>  <span data-ttu-id="7102b-130">Power Virtual Agent 开发过程使用无代码的图形界面方法，使团队的每个成员都能轻松创建和维护智能虚拟代理。</span><span class="sxs-lookup"><span data-stu-id="7102b-130">The Power Virtual Agent development process uses a guided, no-code, graphical interface approach to empower every member of your team to easily create and maintain an intelligent virtual agent.</span></span>  <span data-ttu-id="7102b-131">在[Power Virtual agent 门户](https://powervirtualagents.microsoft.com)中完成创建 chatbot 后，可以轻松地[将 Power virtual Agent chatbot 与团队集成](how-to/add-power-virtual-agents-bot-to-teams.md)。</span><span class="sxs-lookup"><span data-stu-id="7102b-131">Once you have completed creating your chatbot in the [Power Virtual Agents portal](https://powervirtualagents.microsoft.com), you can easily [integrate your Power Virtual Agents chatbot with Teams](how-to/add-power-virtual-agents-bot-to-teams.md).</span></span> <span data-ttu-id="7102b-132">若要开始创建电源虚拟代理 chatbot，*请参阅* [power virtual agent 文档](https://docs.microsoft.com/power-virtual-agents/)。</span><span class="sxs-lookup"><span data-stu-id="7102b-132">To get started creating your Power Virtual Agents chatbot, *see* the [Power Virtual Agents documentation](https://docs.microsoft.com/power-virtual-agents/).</span></span>

## <a name="webhooks-and-connectors"></a><span data-ttu-id="7102b-133">Webhook 和连接器</span><span class="sxs-lookup"><span data-stu-id="7102b-133">Webhooks and connectors</span></span>

<span data-ttu-id="7102b-134">Webhook 和连接器允许您创建简单的 bot 来实现基本交互，例如启动脱离工作流或其他简单命令。</span><span class="sxs-lookup"><span data-stu-id="7102b-134">Webhooks and connectors allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands.</span></span> <span data-ttu-id="7102b-135">它们仅在您创建它们的团队中运行，适用于特定于贵公司的工作流的简单流程。</span><span class="sxs-lookup"><span data-stu-id="7102b-135">They live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="7102b-136">*请参阅*[什么是 webhook 和连接器？](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)有关详细信息，请参阅。</span><span class="sxs-lookup"><span data-stu-id="7102b-136">*See* [What are webhooks and connectors?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) for more information.</span></span>

## <a name="where-bots-work-best"></a><span data-ttu-id="7102b-137">在何处最适合使用 bot</span><span class="sxs-lookup"><span data-stu-id="7102b-137">Where bots work best</span></span>

<span data-ttu-id="7102b-138">Microsoft 团队中的 bot 可以是一对一对话、组聊天或团队中的频道的一部分。</span><span class="sxs-lookup"><span data-stu-id="7102b-138">Bots in Microsoft Teams can be part of a one-to-one conversation, a group chat, or a channel in a Team.</span></span> <span data-ttu-id="7102b-139">每个范围都将为您的会话 bot 提供独特的机会和挑战。</span><span class="sxs-lookup"><span data-stu-id="7102b-139">Each scope will provide unique opportunities, and challenges, for your conversational bot.</span></span>

### <a name="in-a-channel"></a><span data-ttu-id="7102b-140">通道中</span><span class="sxs-lookup"><span data-stu-id="7102b-140">In a channel</span></span>

<span data-ttu-id="7102b-141">频道包含多个用户之间的线程对话—可能有很多人（目前最多为2000）。</span><span class="sxs-lookup"><span data-stu-id="7102b-141">Channels contain threaded conversations between multiple people — potentially lots of people (currently, up to two thousand).</span></span> <span data-ttu-id="7102b-142">这可能会为你的 bot 提供大规模的访问，但各个交互需要简明。</span><span class="sxs-lookup"><span data-stu-id="7102b-142">This potentially gives your bot massive reach, but individual interactions need to be concise.</span></span> <span data-ttu-id="7102b-143">传统的多项交互操作可能不会很好。</span><span class="sxs-lookup"><span data-stu-id="7102b-143">Traditional multi-turn interactions probably won't work well.</span></span> <span data-ttu-id="7102b-144">相反，如果需要收集大量信息，请查看使用互动卡片或任务模块，或者可能将对话移动到一对一对话中。</span><span class="sxs-lookup"><span data-stu-id="7102b-144">Instead, look to use interactive cards or task modules, or potentially move the conversation to a one-to-one conversation if you need to collect lots of information.</span></span> <span data-ttu-id="7102b-145">你的 bot 也只能访问直接访问邮件的邮件 `@mentioned` ，无法使用 Microsoft Graph 和提升的组织级别权限从对话中检索其他邮件。</span><span class="sxs-lookup"><span data-stu-id="7102b-145">Your bot will also only have access to messages where it's `@mentioned` directly, you cannot retrieve additional messages from the conversation using Microsoft Graph and elevated organization-level permissions.</span></span>

<span data-ttu-id="7102b-146">在频道中 excel 的一些应用场景包括：</span><span class="sxs-lookup"><span data-stu-id="7102b-146">Some scenarios where bots excel in a channel include:</span></span>

* <span data-ttu-id="7102b-147">**通知**，尤其是为用户提供用于获取其他信息的互动卡片时。</span><span class="sxs-lookup"><span data-stu-id="7102b-147">**Notifications**, particularly if you provide an interactive card for users to take additional information.</span></span>
* <span data-ttu-id="7102b-148">**反馈方案**，如投票和调查。</span><span class="sxs-lookup"><span data-stu-id="7102b-148">**Feedback scenarios** like polls and surveys.</span></span>
* <span data-ttu-id="7102b-149">可在**单个请求/响应周期**中解决的交互，其中的结果对对话的多个成员很有用。</span><span class="sxs-lookup"><span data-stu-id="7102b-149">Interactions that can be resolved in a **single request/response cycle**, where the results are useful for multiple members of the conversation.</span></span>
* <span data-ttu-id="7102b-150">**社交/趣味 bot** —获取非常棒的 cat 图像，随机挑选获奖者等。</span><span class="sxs-lookup"><span data-stu-id="7102b-150">**Social/fun bots** — get an awesome cat image, randomly pick a winner, etc.</span></span>

### <a name="in-a-group-chat"></a><span data-ttu-id="7102b-151">在群聊中</span><span class="sxs-lookup"><span data-stu-id="7102b-151">In a group chat</span></span>

<span data-ttu-id="7102b-152">组聊天是三个或更多人之间的非线程对话。</span><span class="sxs-lookup"><span data-stu-id="7102b-152">Group chats are non-threaded conversations between three or more people.</span></span> <span data-ttu-id="7102b-153">它们的成员数往往少于通道，并且更具暂时性。</span><span class="sxs-lookup"><span data-stu-id="7102b-153">They tend to have fewer members than a channel, and are more transient.</span></span> <span data-ttu-id="7102b-154">与频道类似，你的 bot 仅可直接访问邮件 `@mentioned` 。</span><span class="sxs-lookup"><span data-stu-id="7102b-154">Similar to a channel, your bot will only have access to messages where it's `@mentioned` directly.</span></span>

<span data-ttu-id="7102b-155">在频道中正常工作的方案通常在组聊天中也会起作用。</span><span class="sxs-lookup"><span data-stu-id="7102b-155">Scenarios that work well in a channel will usually work just as well in a group chat.</span></span>

### <a name="in-a-one-to-one-chat"></a><span data-ttu-id="7102b-156">以一对一聊天</span><span class="sxs-lookup"><span data-stu-id="7102b-156">In a one-to-one chat</span></span>

<span data-ttu-id="7102b-157">这是对话机器人与用户进行交互的传统方法。</span><span class="sxs-lookup"><span data-stu-id="7102b-157">This is the traditional way for a conversational bot to interact with a user.</span></span> <span data-ttu-id="7102b-158">他们可以实现多元化不同的工作负载。</span><span class="sxs-lookup"><span data-stu-id="7102b-158">They can enable incredibly diverse workloads.</span></span> <span data-ttu-id="7102b-159">问：&bot、在其他系统中启动工作流的 bot、通知笑话的 bot 以及记录笔记的 bot 只是几个示例。</span><span class="sxs-lookup"><span data-stu-id="7102b-159">Q&A bots, bots that initiate workflows in other systems, bots that tell jokes, and bots that take notes are just a few examples.</span></span> <span data-ttu-id="7102b-160">只需记住，应考虑基于会话的界面是否是展示功能的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="7102b-160">Just remember to consider whether a conversation-based interface is the best way to present your functionality.</span></span>

## <a name="bot-fails"></a><span data-ttu-id="7102b-161">机器人失败</span><span class="sxs-lookup"><span data-stu-id="7102b-161">Bot fails</span></span>

### <a name="having-multi-turn-experiences-in-chat"></a><span data-ttu-id="7102b-162">在聊天中拥有多轮体验</span><span class="sxs-lookup"><span data-stu-id="7102b-162">Having multi-turn experiences in chat</span></span>

<span data-ttu-id="7102b-163">您的 bot 和用户之间的一个广泛的对话框是一种缓慢且过于复杂的方法来使任务完成，还需要开发人员维护状态。</span><span class="sxs-lookup"><span data-stu-id="7102b-163">An extensive dialog between your bot and the user is a slow and overly complex way to get a task completed and it also requires the developer to maintain state.</span></span> <span data-ttu-id="7102b-164">若要退出此状态，用户必须是超时时间或键入 "*取消*"。</span><span class="sxs-lookup"><span data-stu-id="7102b-164">To exit this state a user must either time-out or type “*Cancel*”.</span></span> <span data-ttu-id="7102b-165">在所有情况下，此过程是不必要的单调操作：</span><span class="sxs-lookup"><span data-stu-id="7102b-165">Above all, the process is unnecessarily tedious:</span></span>

<span data-ttu-id="7102b-166">用户：使用 Megan 安排会议。</span><span class="sxs-lookup"><span data-stu-id="7102b-166">USER: Schedule a meeting with Megan.</span></span>

<span data-ttu-id="7102b-167">BOT：我发现了200结果，请包含姓和名。</span><span class="sxs-lookup"><span data-stu-id="7102b-167">BOT: I’ve found 200 results, please include a first and last name.</span></span>

<span data-ttu-id="7102b-168">用户：使用 Megan Bowen 安排会议。</span><span class="sxs-lookup"><span data-stu-id="7102b-168">USER: Schedule a meeting with Megan Bowen.</span></span>

<span data-ttu-id="7102b-169">机器人：好了，您想要使用 Megan Bowen 来满足什么时间？</span><span class="sxs-lookup"><span data-stu-id="7102b-169">BOT: OK, what time would you like to meet with Megan Bowen?</span></span>

<span data-ttu-id="7102b-170">用户： 1:00 pm。</span><span class="sxs-lookup"><span data-stu-id="7102b-170">USER: 1:00 pm.</span></span>

<span data-ttu-id="7102b-171">机器人：在哪天？</span><span class="sxs-lookup"><span data-stu-id="7102b-171">BOT: On which day?</span></span>

### <a name="supporting-too-many-commands"></a><span data-ttu-id="7102b-172">支持的命令过多</span><span class="sxs-lookup"><span data-stu-id="7102b-172">Supporting too many commands</span></span>

<span data-ttu-id="7102b-173">用户不能成功或查看不支持过多命令的 bot （尤其是一系列命令）。</span><span class="sxs-lookup"><span data-stu-id="7102b-173">A bot that supports excessive commands, especially a broad range of commands, will not be successful or viewed positively by users.</span></span> <span data-ttu-id="7102b-174">由于当前机器人菜单中只有6个可见的命令，因此任何频率都不大可能使用。</span><span class="sxs-lookup"><span data-stu-id="7102b-174">Since there are only 6 visible commands in the current bot menu, anything more is unlikely to be used with any frequency.</span></span> <span data-ttu-id="7102b-175">深入了解特定区域的 bot，而不是尝试成为一家广泛的助理将会更好地发挥作用并 fare。</span><span class="sxs-lookup"><span data-stu-id="7102b-175">Bots that go deep into a specific area rather than trying to be a broad assistant will work and fare better.</span></span>

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a><span data-ttu-id="7102b-176">使用 unranked 响应维护大型检索知识库</span><span class="sxs-lookup"><span data-stu-id="7102b-176">Maintaining a large retrieval knowledge base with unranked responses</span></span>

<span data-ttu-id="7102b-177">Bot 最适用于简短的快速交互，而不是 sifting 通过长列表查找答案。</span><span class="sxs-lookup"><span data-stu-id="7102b-177">Bots are best suited for short, quick interactions, not sifting through long lists looking for an answer.</span></span>

## <a name="get-started"></a><span data-ttu-id="7102b-178">入门</span><span class="sxs-lookup"><span data-stu-id="7102b-178">Get started</span></span>

* [<span data-ttu-id="7102b-179">C # 中的团队对话机器人/dotnet</span><span class="sxs-lookup"><span data-stu-id="7102b-179">Teams conversation bot in C#/dotnet</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [<span data-ttu-id="7102b-180">JavaScript 中的 Teams 对话机器人</span><span class="sxs-lookup"><span data-stu-id="7102b-180">Teams conversation bot in JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a><span data-ttu-id="7102b-181">了解更多</span><span class="sxs-lookup"><span data-stu-id="7102b-181">Learn more</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7102b-182">团队中的 bot 的基础知识</span><span class="sxs-lookup"><span data-stu-id="7102b-182">The basics of bots in Teams</span></span>](~/bots/bot-basics.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="7102b-183">创建适合 Teams 的机器人</span><span class="sxs-lookup"><span data-stu-id="7102b-183">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)
