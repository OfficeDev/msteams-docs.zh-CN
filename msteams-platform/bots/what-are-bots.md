---
title: 什么是对话机器人？
author: clearab
description: Microsoft Teams 中的对话机器人概述。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 0304ae436b54db0d111eaed507beb350f1ca4632
ms.sourcegitcommit: 4539479289b43812eaae07a1c0f878bed815d2d2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797867"
---
# <a name="what-are-conversational-bots-in-microsoft-teams"></a><span data-ttu-id="3121a-103">什么是 Microsoft Teams 中的对话机器人？</span><span class="sxs-lookup"><span data-stu-id="3121a-103">What are conversational bots in Microsoft Teams?</span></span>

<span data-ttu-id="3121a-104">对话机器人允许用户通过文本、交互式卡片和任务模块与 Web 服务进行交互。</span><span class="sxs-lookup"><span data-stu-id="3121a-104">Conversational bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span> <span data-ttu-id="3121a-105">它们非常灵活 — 对话机器人的范围可以包括处理一些简单命令或复杂、人工智能和自然语言处理虚拟助理。</span><span class="sxs-lookup"><span data-stu-id="3121a-105">They're incredibly flexible — conversational bots can be scoped to handling a few simple commands or complex, artificial-intelligence-powered and natural-language-processing virtual assistants.</span></span> <span data-ttu-id="3121a-106">它们可以是较大应用程序的一个方面，也可以完全独立。</span><span class="sxs-lookup"><span data-stu-id="3121a-106">They can be one aspect of a larger application, or completely stand-alone.</span></span>

<span data-ttu-id="3121a-107">下面的 GIF 显示用户同时使用文本和交互式卡片在一对一聊天中与机器人交互。</span><span class="sxs-lookup"><span data-stu-id="3121a-107">The GIF below shows a user conversing with a bot in a one-to-one chat using both text and interactive cards.</span></span> <span data-ttu-id="3121a-108">找到卡片、文本和任务模块的合适组合是创建有用的自动程序的关键。</span><span class="sxs-lookup"><span data-stu-id="3121a-108">Finding the right mix of cards, text, and task modules is key to creating a useful bot.</span></span> <span data-ttu-id="3121a-109">不要忘记，机器人不仅仅是文本！</span><span class="sxs-lookup"><span data-stu-id="3121a-109">Don't forget, bots are much more than just text!</span></span>

![FAQ Plus gif](~/assets/images/FAQPlusEndUser.gif)

## <a name="build--a-bot-for-teams-with-the-microsoft-bot-framework"></a><span data-ttu-id="3121a-111">使用 Microsoft Bot Framework 生成适用于 Teams 的自动程序</span><span class="sxs-lookup"><span data-stu-id="3121a-111">Build  a bot for Teams with the Microsoft Bot Framework</span></span>

<span data-ttu-id="3121a-112">[Microsoft Bot Framework](https://dev.botframework.com/)是一个丰富的 SDK，用于使用 C#、Java、Python 和 JavaScript 生成机器人。</span><span class="sxs-lookup"><span data-stu-id="3121a-112">The [Microsoft Bot Framework](https://dev.botframework.com/) is a rich SDK for building bots using C#, Java, Python, and JavaScript.</span></span> <span data-ttu-id="3121a-113">如果你已有一个基于 Bot Framework 的自动程序，你可以轻松调整它以在 Microsoft Teams 中工作。</span><span class="sxs-lookup"><span data-stu-id="3121a-113">If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.</span></span> <span data-ttu-id="3121a-114">我们建议你使用 C# 或 Node.js来利用[SDK。](/microsoftteams/platform/#pivot=sdk-tools)</span><span class="sxs-lookup"><span data-stu-id="3121a-114">We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="3121a-115">这些包扩展基本 Bot Builder SDK 类和方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="3121a-115">These packages extend the basic Bot Builder SDK classes and methods as follows:</span></span>

* <span data-ttu-id="3121a-116">使用专用卡类型，如 Office 365 连接器卡。</span><span class="sxs-lookup"><span data-stu-id="3121a-116">Use specialized card types like the Office 365 Connector card.</span></span>
* <span data-ttu-id="3121a-117">使用和设置有关活动的特定于 Teams 的频道数据。</span><span class="sxs-lookup"><span data-stu-id="3121a-117">Consume and set Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="3121a-118">处理邮件扩展请求。</span><span class="sxs-lookup"><span data-stu-id="3121a-118">Process messaging extension requests.</span></span>

<span data-ttu-id="3121a-119">Teams 自动程序由三个元素组成：</span><span class="sxs-lookup"><span data-stu-id="3121a-119">Your Teams bot consists of three elements:</span></span>

* <span data-ttu-id="3121a-120">您托管的可公开访问的 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="3121a-120">A publicly accessible web service that you host.</span></span>
* <span data-ttu-id="3121a-121">使用 Bot Framework 注册机器人。</span><span class="sxs-lookup"><span data-stu-id="3121a-121">Your bot registration with the Bot Framework.</span></span>
* <span data-ttu-id="3121a-122">包含应用清单的 Teams 应用包。</span><span class="sxs-lookup"><span data-stu-id="3121a-122">Your Teams app package with your app manifest.</span></span> <span data-ttu-id="3121a-123">用户将安装 Teams 客户端，并通过自动程序服务将其连接到 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="3121a-123">This is what your users will install and connects the Teams client to your web service, routed through the Bot Service.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="3121a-124">你可以以任何 Web 编程技术开发 Teams 应用并直接调用 [Bot Framework REST API，](/bot-framework/rest-api/bot-framework-rest-overview) 但你必须自己执行所有令牌处理。</span><span class="sxs-lookup"><span data-stu-id="3121a-124">You can develop Teams apps in any web-programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

> [!TIP]
> <span data-ttu-id="3121a-125">Teams App Studio\* 可帮助你创建和配置应用清单，还可以在 Bot Framework 上将 Web 服务注册为自动程序。</span><span class="sxs-lookup"><span data-stu-id="3121a-125">Teams App Studio\* helps you create and configure your app manifest, and can register your web service as a bot on the Bot Framework.</span></span> <span data-ttu-id="3121a-126">它还包含 React 控件库和交互式卡片生成器。</span><span class="sxs-lookup"><span data-stu-id="3121a-126">It also contains a React control library and an interactive card builder.</span></span> <span data-ttu-id="3121a-127">*请参阅* [Teams App Studio 入门](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="3121a-127">*See* [Getting started with Teams App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="create-a-chatbot-for-teams-with-microsoft-power-virtual-agents"></a><span data-ttu-id="3121a-128">使用 Microsoft Power Virtual Agents 为 Teams 创建聊天机器人</span><span class="sxs-lookup"><span data-stu-id="3121a-128">Create a chatbot for Teams with Microsoft Power Virtual Agents</span></span>

<span data-ttu-id="3121a-129">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) 是一项基于 Microsoft Power 平台和 Bot Framework 构建的聊天机器人服务。</span><span class="sxs-lookup"><span data-stu-id="3121a-129">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) is a chatbot service, built on the Microsoft Power platform and Bot Framework.</span></span>  <span data-ttu-id="3121a-130">Power Virtual Agent 开发过程使用引导式无代码图形界面方法，使团队中的每个成员能够轻松创建和维护智能虚拟代理。</span><span class="sxs-lookup"><span data-stu-id="3121a-130">The Power Virtual Agent development process uses a guided, no-code, graphical interface approach to empower every member of your team to easily create and maintain an intelligent virtual agent.</span></span>  <span data-ttu-id="3121a-131">在 Power [Virtual Agents](https://powervirtualagents.microsoft.com)门户中完成聊天机器人的创建后，你可以轻松地将 Power Virtual [Agents 聊天机器人](how-to/add-power-virtual-agents-bot-to-teams.md)与 Teams 集成。</span><span class="sxs-lookup"><span data-stu-id="3121a-131">Once you have completed creating your chatbot in the [Power Virtual Agents portal](https://powervirtualagents.microsoft.com), you can easily [integrate your Power Virtual Agents chatbot with Teams](how-to/add-power-virtual-agents-bot-to-teams.md).</span></span> <span data-ttu-id="3121a-132">若要开始创建 Power Virtual Agents 聊天机器人， *请参阅* [Power Virtual Agents 文档](https://docs.microsoft.com/power-virtual-agents/)。</span><span class="sxs-lookup"><span data-stu-id="3121a-132">To get started creating your Power Virtual Agents chatbot, *see* the [Power Virtual Agents documentation](https://docs.microsoft.com/power-virtual-agents/).</span></span>

## <a name="webhooks-and-connectors"></a><span data-ttu-id="3121a-133">Webhook 和连接器</span><span class="sxs-lookup"><span data-stu-id="3121a-133">Webhooks and connectors</span></span>

<span data-ttu-id="3121a-134">Webhook 和连接器允许你创建用于基本交互的简单自动程序，如启动工作流或其他简单命令。</span><span class="sxs-lookup"><span data-stu-id="3121a-134">Webhooks and connectors allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands.</span></span> <span data-ttu-id="3121a-135">它们仅在您创建的团队中工作，并且适用于特定于公司工作流的简单流程。</span><span class="sxs-lookup"><span data-stu-id="3121a-135">They live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="3121a-136">*有关详细信息*[，请参阅什么是 Webhook 和连接器？](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)</span><span class="sxs-lookup"><span data-stu-id="3121a-136">*See* [What are webhooks and connectors?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) for more information.</span></span>

## <a name="where-bots-work-best"></a><span data-ttu-id="3121a-137">自动程序最工作的地方</span><span class="sxs-lookup"><span data-stu-id="3121a-137">Where bots work best</span></span>

<span data-ttu-id="3121a-138">Microsoft Teams 中的机器人可以是一对一对话、群聊或团队中的频道的一部分。</span><span class="sxs-lookup"><span data-stu-id="3121a-138">Bots in Microsoft Teams can be part of a one-to-one conversation, a group chat, or a channel in a Team.</span></span> <span data-ttu-id="3121a-139">每个范围都将为对话机器人提供独特的机会和挑战。</span><span class="sxs-lookup"><span data-stu-id="3121a-139">Each scope will provide unique opportunities, and challenges, for your conversational bot.</span></span>

### <a name="in-a-channel"></a><span data-ttu-id="3121a-140">在频道中</span><span class="sxs-lookup"><span data-stu-id="3121a-140">In a channel</span></span>

<span data-ttu-id="3121a-141">频道包含多个人之间的线程对话-可能 (，最多两千) 。</span><span class="sxs-lookup"><span data-stu-id="3121a-141">Channels contain threaded conversations between multiple people — potentially lots of people (currently, up to two thousand).</span></span> <span data-ttu-id="3121a-142">这可能会为机器人带来巨大影响，但个人交互需要简洁明了。</span><span class="sxs-lookup"><span data-stu-id="3121a-142">This potentially gives your bot massive reach, but individual interactions need to be concise.</span></span> <span data-ttu-id="3121a-143">传统的多向交互可能不起作用。</span><span class="sxs-lookup"><span data-stu-id="3121a-143">Traditional multi-turn interactions probably won't work well.</span></span> <span data-ttu-id="3121a-144">相反，请查找使用交互式卡片或任务模块，或者如果需要收集大量信息，则可能会将对话移动到一对一对话。</span><span class="sxs-lookup"><span data-stu-id="3121a-144">Instead, look to use interactive cards or task modules, or potentially move the conversation to a one-to-one conversation if you need to collect lots of information.</span></span> <span data-ttu-id="3121a-145">尽管可以使用 Microsoft Graph 和提升的组织级别权限从对话中检索其他邮件，但自动程序也仅有权访问直接接收的邮件 `@mentioned` 。</span><span class="sxs-lookup"><span data-stu-id="3121a-145">Your bot will also only have access to messages where it's `@mentioned` directly, although you can retrieve additional messages from the conversation using Microsoft Graph and elevated organization-level permissions.</span></span>

<span data-ttu-id="3121a-146">机器人在频道中 excel 的一些应用场景包括：</span><span class="sxs-lookup"><span data-stu-id="3121a-146">Some scenarios where bots excel in a channel include:</span></span>

* <span data-ttu-id="3121a-147">**通知**，尤其是提供交互式卡片以便用户获取其他信息时。</span><span class="sxs-lookup"><span data-stu-id="3121a-147">**Notifications**, particularly if you provide an interactive card for users to take additional information.</span></span>
* <span data-ttu-id="3121a-148">**反馈方案，** 如投票和调查。</span><span class="sxs-lookup"><span data-stu-id="3121a-148">**Feedback scenarios** like polls and surveys.</span></span>
* <span data-ttu-id="3121a-149">可以在单个请求 **/** 响应周期中解析的交互，其中结果对对话的多个成员很有用。</span><span class="sxs-lookup"><span data-stu-id="3121a-149">Interactions that can be resolved in a **single request/response cycle**, where the results are useful for multiple members of the conversation.</span></span>
* <span data-ttu-id="3121a-150">**社交/有趣的机器人** — 获取出色的 cat 图像、随机选取获胜者等。</span><span class="sxs-lookup"><span data-stu-id="3121a-150">**Social/fun bots** — get an awesome cat image, randomly pick a winner, etc.</span></span>

### <a name="in-a-group-chat"></a><span data-ttu-id="3121a-151">在群聊中</span><span class="sxs-lookup"><span data-stu-id="3121a-151">In a group chat</span></span>

<span data-ttu-id="3121a-152">群聊是三个或多个人员之间的非线程对话。</span><span class="sxs-lookup"><span data-stu-id="3121a-152">Group chats are non-threaded conversations between three or more people.</span></span> <span data-ttu-id="3121a-153">它们的成员数通常少于频道的成员数，并且具有更多的瞬态成员。</span><span class="sxs-lookup"><span data-stu-id="3121a-153">They tend to have fewer members than a channel, and are more transient.</span></span> <span data-ttu-id="3121a-154">与频道类似，机器人将仅有权访问直接位于其中 `@mentioned` 的消息。</span><span class="sxs-lookup"><span data-stu-id="3121a-154">Similar to a channel, your bot will only have access to messages where it's `@mentioned` directly.</span></span>

<span data-ttu-id="3121a-155">在频道中良好工作的方案通常与群聊中一样。</span><span class="sxs-lookup"><span data-stu-id="3121a-155">Scenarios that work well in a channel will usually work just as well in a group chat.</span></span>

### <a name="in-a-one-to-one-chat"></a><span data-ttu-id="3121a-156">在一对一聊天中</span><span class="sxs-lookup"><span data-stu-id="3121a-156">In a one-to-one chat</span></span>

<span data-ttu-id="3121a-157">这是对话机器人与用户交互的传统方式。</span><span class="sxs-lookup"><span data-stu-id="3121a-157">This is the traditional way for a conversational bot to interact with a user.</span></span> <span data-ttu-id="3121a-158">它们可以启用非常不同的工作负载。</span><span class="sxs-lookup"><span data-stu-id="3121a-158">They can enable incredibly diverse workloads.</span></span> <span data-ttu-id="3121a-159">问&聊天机器人、在其他系统中启动工作流的机器人、告诉机器人和做笔记的机器人只是几个示例。</span><span class="sxs-lookup"><span data-stu-id="3121a-159">Q&A bots, bots that initiate workflows in other systems, bots that tell jokes, and bots that take notes are just a few examples.</span></span> <span data-ttu-id="3121a-160">请记住，基于对话的界面是否是显示功能的最佳方法。</span><span class="sxs-lookup"><span data-stu-id="3121a-160">Just remember to consider whether a conversation-based interface is the best way to present your functionality.</span></span>

## <a name="bot-fails"></a><span data-ttu-id="3121a-161">自动程序失败</span><span class="sxs-lookup"><span data-stu-id="3121a-161">Bot fails</span></span>

### <a name="having-multi-turn-experiences-in-chat"></a><span data-ttu-id="3121a-162">在聊天中拥有多轮体验</span><span class="sxs-lookup"><span data-stu-id="3121a-162">Having multi-turn experiences in chat</span></span>

<span data-ttu-id="3121a-163">自动程序与用户之间的广泛对话是完成任务的一种缓慢且过于复杂的方式，它还需要开发人员保持状态。</span><span class="sxs-lookup"><span data-stu-id="3121a-163">An extensive dialog between your bot and the user is a slow and overly complex way to get a task completed and it also requires the developer to maintain state.</span></span> <span data-ttu-id="3121a-164">若要退出此状态，用户必须退出或键入"*取消*"。</span><span class="sxs-lookup"><span data-stu-id="3121a-164">To exit this state a user must either time-out or type “*Cancel*”.</span></span> <span data-ttu-id="3121a-165">最重要的是，此过程不必要的繁琐：</span><span class="sxs-lookup"><span data-stu-id="3121a-165">Above all, the process is unnecessarily tedious:</span></span>

<span data-ttu-id="3121a-166">用户：安排与 Megan 的会议。</span><span class="sxs-lookup"><span data-stu-id="3121a-166">USER: Schedule a meeting with Megan.</span></span>

<span data-ttu-id="3121a-167">BOT：我找到 200 个结果，请包含名字和姓氏。</span><span class="sxs-lookup"><span data-stu-id="3121a-167">BOT: I’ve found 200 results, please include a first and last name.</span></span>

<span data-ttu-id="3121a-168">用户：安排与 Megan Bowen 的会议。</span><span class="sxs-lookup"><span data-stu-id="3121a-168">USER: Schedule a meeting with Megan Bowen.</span></span>

<span data-ttu-id="3121a-169">BOT：确定，你要在什么时间与 Megan Bowen 会面？</span><span class="sxs-lookup"><span data-stu-id="3121a-169">BOT: OK, what time would you like to meet with Megan Bowen?</span></span>

<span data-ttu-id="3121a-170">用户：下午 1：00。</span><span class="sxs-lookup"><span data-stu-id="3121a-170">USER: 1:00 pm.</span></span>

<span data-ttu-id="3121a-171">BOT：哪一天？</span><span class="sxs-lookup"><span data-stu-id="3121a-171">BOT: On which day?</span></span>

### <a name="supporting-too-many-commands"></a><span data-ttu-id="3121a-172">支持过多命令</span><span class="sxs-lookup"><span data-stu-id="3121a-172">Supporting too many commands</span></span>

<span data-ttu-id="3121a-173">支持过多命令（尤其是广泛的命令）的自动程序将不会成功，或者用户不会积极查看。</span><span class="sxs-lookup"><span data-stu-id="3121a-173">A bot that supports excessive commands, especially a broad range of commands, will not be successful or viewed positively by users.</span></span> <span data-ttu-id="3121a-174">由于当前自动程序菜单中只有 6 个可见命令，因此其他任何命令都不可能以任何频率使用。</span><span class="sxs-lookup"><span data-stu-id="3121a-174">Since there are only 6 visible commands in the current bot menu, anything more is unlikely to be used with any frequency.</span></span> <span data-ttu-id="3121a-175">深入到特定领域的机器人（而不是尝试成为广泛助手）将更好地工作并更好地进行开发。</span><span class="sxs-lookup"><span data-stu-id="3121a-175">Bots that go deep into a specific area rather than trying to be a broad assistant will work and fare better.</span></span>

### <a name="maintaining-a-large-retrieval-knowledge-base-with-unranked-responses"></a><span data-ttu-id="3121a-176">使用未应答的响应维护大型检索知识库</span><span class="sxs-lookup"><span data-stu-id="3121a-176">Maintaining a large retrieval knowledge base with unranked responses</span></span>

<span data-ttu-id="3121a-177">自动程序最适合于短而快速交互，而不是通过长列表查找答案。</span><span class="sxs-lookup"><span data-stu-id="3121a-177">Bots are best suited for short, quick interactions, not sifting through long lists looking for an answer.</span></span>

## <a name="get-started"></a><span data-ttu-id="3121a-178">入门</span><span class="sxs-lookup"><span data-stu-id="3121a-178">Get started</span></span>

* [<span data-ttu-id="3121a-179">C#/dotnet 中的 Teams 对话机器人</span><span class="sxs-lookup"><span data-stu-id="3121a-179">Teams conversation bot in C#/dotnet</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [<span data-ttu-id="3121a-180">JavaScript 中的 Teams 对话机器人</span><span class="sxs-lookup"><span data-stu-id="3121a-180">Teams conversation bot in JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a><span data-ttu-id="3121a-181">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="3121a-181">Learn more</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3121a-182">Teams 中的机器人基础知识</span><span class="sxs-lookup"><span data-stu-id="3121a-182">The basics of bots in Teams</span></span>](~/bots/bot-basics.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="3121a-183">创建适合 Teams 的机器人</span><span class="sxs-lookup"><span data-stu-id="3121a-183">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)
