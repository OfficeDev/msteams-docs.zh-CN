---
title: 智能机器人和 SDK
author: clearab
description: 聊天机器人和 SDK Microsoft Teams。
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 2a77b629a645625398fccfd6a18eb1ed3f09844e
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020181"
---
# <a name="bots-and-sdks"></a><span data-ttu-id="c01ea-103">智能机器人和 SDK</span><span class="sxs-lookup"><span data-stu-id="c01ea-103">Bots and SDKs</span></span>

<span data-ttu-id="c01ea-104">若要创建在 Microsoft Teams中工作的自动程序，可以使用下列方法之一：</span><span class="sxs-lookup"><span data-stu-id="c01ea-104">To create a bot that works in Microsoft Teams, you can use one of the following:</span></span>
* <span data-ttu-id="c01ea-105">基于 sdk 构建的现有Microsoft Bot Framework程序。</span><span class="sxs-lookup"><span data-stu-id="c01ea-105">An existing bot built on the Microsoft Bot Framework SDK.</span></span>
* <span data-ttu-id="c01ea-106">Power Virtual Agents chatbot 服务。</span><span class="sxs-lookup"><span data-stu-id="c01ea-106">Power Virtual Agents chatbot service.</span></span>
* <span data-ttu-id="c01ea-107">Webhook 和连接器。</span><span class="sxs-lookup"><span data-stu-id="c01ea-107">Webhooks and connectors.</span></span>

## <a name="bots-and-the-microsoft-bot-framework"></a><span data-ttu-id="c01ea-108">机器人和Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="c01ea-108">Bots and the Microsoft Bot Framework</span></span>

<span data-ttu-id="c01ea-109">你的Teams自动程序由以下三个元素组成：</span><span class="sxs-lookup"><span data-stu-id="c01ea-109">Your Teams bot consists of the following three elements:</span></span>

* <span data-ttu-id="c01ea-110">由你主持的公共访问的 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="c01ea-110">A publicly accessible web service that you host.</span></span>
* <span data-ttu-id="c01ea-111">使用 Bot Framework 注册自动程序。</span><span class="sxs-lookup"><span data-stu-id="c01ea-111">Your bot registration with the Bot Framework.</span></span>
* <span data-ttu-id="c01ea-112">你的应用Teams清单一起打包应用包。</span><span class="sxs-lookup"><span data-stu-id="c01ea-112">Your Teams app package with your app manifest.</span></span> <span data-ttu-id="c01ea-113">这是您的用户安装和将 Teams 客户端连接到通过自动程序服务路由的 Web 服务的内容。</span><span class="sxs-lookup"><span data-stu-id="c01ea-113">This is what your users install and connect the Teams client to your web service, routed through the bot service.</span></span>

<span data-ttu-id="c01ea-114">Bot [Framework](https://dev.botframework.com/) 是一个丰富的 SDK，用于创建使用 C#、Java、Python 和 JavaScript 的聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="c01ea-114">The [Bot Framework](https://dev.botframework.com/) is a rich SDK used to create bots using C#, Java, Python, and JavaScript.</span></span> <span data-ttu-id="c01ea-115">如果已有基于 Bot Framework 的自动程序，可以轻松修改它以在 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="c01ea-115">If you already have a bot that is based on the Bot Framework, you can easily modify it to work in Microsoft Teams.</span></span> <span data-ttu-id="c01ea-116">使用 C# 或 Node.js 来利用[我们的 SDK。](/microsoftteams/platform/#pivot=sdk-tools)</span><span class="sxs-lookup"><span data-stu-id="c01ea-116">Use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="c01ea-117">这些包扩展基本 Bot Builder SDK 类和方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c01ea-117">These packages extend the basic Bot Builder SDK classes and methods as follows:</span></span>

* <span data-ttu-id="c01ea-118">使用专用卡类型，如Office 365卡。</span><span class="sxs-lookup"><span data-stu-id="c01ea-118">Use specialized card types like the Office 365 connector card.</span></span>
* <span data-ttu-id="c01ea-119">在Teams设置特定于频道的数据。</span><span class="sxs-lookup"><span data-stu-id="c01ea-119">Set Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="c01ea-120">处理邮件扩展请求。</span><span class="sxs-lookup"><span data-stu-id="c01ea-120">Process messaging extension requests.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="c01ea-121">可以使用任何 Web Teams技术开发应用，并直接调用 Bot [Framework REST API。](/bot-framework/rest-api/bot-framework-rest-overview)</span><span class="sxs-lookup"><span data-stu-id="c01ea-121">You can develop Teams apps in any web programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly.</span></span> <span data-ttu-id="c01ea-122">但是，你必须在所有情况下执行令牌处理。</span><span class="sxs-lookup"><span data-stu-id="c01ea-122">But you must perform token handling in all cases.</span></span>

> [!TIP]
> <span data-ttu-id="c01ea-123">TeamsApp Studio 可帮助你创建和配置应用清单，以及将 Web 服务注册为 Bot Framework 上的自动程序。</span><span class="sxs-lookup"><span data-stu-id="c01ea-123">Teams App Studio helps you create and configure your app manifest, and register your web service as a bot on the Bot Framework.</span></span> <span data-ttu-id="c01ea-124">它还包含一个React库和交互式卡片生成器。</span><span class="sxs-lookup"><span data-stu-id="c01ea-124">It also contains a React control library and an interactive card builder.</span></span> <span data-ttu-id="c01ea-125">有关详细信息，请参阅[App Studio Teams入门](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c01ea-125">For more information, see [getting started with Teams App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="bots-and-the-microsoft-power-virtual-agents"></a><span data-ttu-id="c01ea-126">机器人和 Microsoft Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="c01ea-126">Bots and the Microsoft Power Virtual Agents</span></span>

<span data-ttu-id="c01ea-127">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)是一项基于 Microsoft Power 平台和 Bot Framework 构建的 chatbot 服务。</span><span class="sxs-lookup"><span data-stu-id="c01ea-127">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) is a chatbot service built on the Microsoft Power platform and Bot Framework.</span></span> <span data-ttu-id="c01ea-128">Power Virtual Agent 开发过程使用引导式无代码和图形界面方法，使团队成员能够轻松创建和维护智能虚拟代理。</span><span class="sxs-lookup"><span data-stu-id="c01ea-128">The Power Virtual Agent development process uses a guided, no-code, and graphical interface approach that empowers your team members to easily create and maintain an intelligent virtual agent.</span></span> <span data-ttu-id="c01ea-129">在聊天门户创建聊天Power Virtual Agents[后](https://powervirtualagents.microsoft.com)，你可以轻松地[将其与](how-to/add-power-virtual-agents-bot-to-teams.md)Teams 集成。</span><span class="sxs-lookup"><span data-stu-id="c01ea-129">After creating your chatbot in the [Power Virtual Agents portal](https://powervirtualagents.microsoft.com), you can easily [integrate it with Teams](how-to/add-power-virtual-agents-bot-to-teams.md).</span></span> <span data-ttu-id="c01ea-130">有关入门详细信息，请参阅Power Virtual Agents[文档](https://docs.microsoft.com/power-virtual-agents/)。</span><span class="sxs-lookup"><span data-stu-id="c01ea-130">For more information on getting started, see [Power Virtual Agents documentation](https://docs.microsoft.com/power-virtual-agents/).</span></span>

## <a name="bots-and-webhooks-and-connectors"></a><span data-ttu-id="c01ea-131">机器人、Webhook 和连接器</span><span class="sxs-lookup"><span data-stu-id="c01ea-131">Bots and webhooks and connectors</span></span>

<span data-ttu-id="c01ea-132">Webhook 和连接器将机器人连接到 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="c01ea-132">Webhooks and connectors connect your bot to your web services.</span></span> <span data-ttu-id="c01ea-133">使用 webhook 和连接器，可以创建简单的机器人进行基本交互，例如创建工作流或其他简单命令。</span><span class="sxs-lookup"><span data-stu-id="c01ea-133">Using webhooks and connectors, you can create a simple bot for basic interaction, such as creating a workflow or other simple commands.</span></span> <span data-ttu-id="c01ea-134">它们仅在创建它们的团队中可用，并且适用于特定于公司工作流的简单流程。</span><span class="sxs-lookup"><span data-stu-id="c01ea-134">They are available only in the team where you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="c01ea-135">有关详细信息，请参阅什么是 [Webhook 和连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="c01ea-135">For more information, see [what are webhooks and connectors](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="advantages-of-bots"></a><span data-ttu-id="c01ea-136">自动程序的优点</span><span class="sxs-lookup"><span data-stu-id="c01ea-136">Advantages of bots</span></span>

<span data-ttu-id="c01ea-137">Microsoft Teams 中的机器人可以进行一对一对话、群聊或参与团队的频道。</span><span class="sxs-lookup"><span data-stu-id="c01ea-137">Bots in Microsoft Teams can be part of a one-to-one conversation, a group chat, or a channel in a team.</span></span> <span data-ttu-id="c01ea-138">每个范围都为对话机器人提供了独特的机遇与挑战。</span><span class="sxs-lookup"><span data-stu-id="c01ea-138">Each scope provides unique opportunities and challenges for your conversational bot.</span></span>

| <span data-ttu-id="c01ea-139">在频道中</span><span class="sxs-lookup"><span data-stu-id="c01ea-139">In a channel</span></span> | <span data-ttu-id="c01ea-140">在群聊中</span><span class="sxs-lookup"><span data-stu-id="c01ea-140">In a group chat</span></span> | <span data-ttu-id="c01ea-141">在一对一聊天中</span><span class="sxs-lookup"><span data-stu-id="c01ea-141">In a one-to-one chat</span></span> |
| :-- | :-- | :-- |
| <span data-ttu-id="c01ea-142">大规模覆盖</span><span class="sxs-lookup"><span data-stu-id="c01ea-142">Massive reach</span></span> | <span data-ttu-id="c01ea-143">成员更少</span><span class="sxs-lookup"><span data-stu-id="c01ea-143">Fewer members</span></span> | <span data-ttu-id="c01ea-144">传统方式</span><span class="sxs-lookup"><span data-stu-id="c01ea-144">Traditional way</span></span> |
| <span data-ttu-id="c01ea-145">简洁的单个交互</span><span class="sxs-lookup"><span data-stu-id="c01ea-145">Concise individual interactions</span></span> | <span data-ttu-id="c01ea-146">@mention自动程序</span><span class="sxs-lookup"><span data-stu-id="c01ea-146">@mention to bot</span></span>  | <span data-ttu-id="c01ea-147">Q&A bots</span><span class="sxs-lookup"><span data-stu-id="c01ea-147">Q&A bots</span></span> |
| <span data-ttu-id="c01ea-148">@mention自动程序</span><span class="sxs-lookup"><span data-stu-id="c01ea-148">@mention to bot</span></span> | <span data-ttu-id="c01ea-149">类似于频道</span><span class="sxs-lookup"><span data-stu-id="c01ea-149">Similar to channel</span></span> | <span data-ttu-id="c01ea-150">告知小人并做笔记的机器人</span><span class="sxs-lookup"><span data-stu-id="c01ea-150">Bots that tell jokes and take notes</span></span> |

### <a name="in-a-channel"></a><span data-ttu-id="c01ea-151">在频道中</span><span class="sxs-lookup"><span data-stu-id="c01ea-151">In a channel</span></span>

<span data-ttu-id="c01ea-152">频道包含多个人员之间的线程对话，甚至最多包含两千个。</span><span class="sxs-lookup"><span data-stu-id="c01ea-152">Channels contain threaded conversations between multiple people even up to two thousand.</span></span> <span data-ttu-id="c01ea-153">这可能会导致自动程序大规模访问，但个人交互必须简洁。</span><span class="sxs-lookup"><span data-stu-id="c01ea-153">This potentially gives your bot massive reach, but individual interactions must be concise.</span></span> <span data-ttu-id="c01ea-154">传统的多向交互不起作用。</span><span class="sxs-lookup"><span data-stu-id="c01ea-154">Traditional multi-turn interactions do not work.</span></span> <span data-ttu-id="c01ea-155">相反，必须查找使用交互式卡片或任务模块，或将对话移动到一对一对话以收集大量信息。</span><span class="sxs-lookup"><span data-stu-id="c01ea-155">Instead, you must look to use interactive cards or task modules, or move the conversation to a one-to-one conversation to collect lots of information.</span></span> <span data-ttu-id="c01ea-156">自动程序仅有权访问其为 的邮件 `@mentioned` 。</span><span class="sxs-lookup"><span data-stu-id="c01ea-156">Your bot only has access to messages where it is `@mentioned`.</span></span> <span data-ttu-id="c01ea-157">您可以使用 Microsoft 权限和组织级别权限从Graph检索其他邮件。</span><span class="sxs-lookup"><span data-stu-id="c01ea-157">You can retrieve additional messages from the conversation using Microsoft Graph and organization-level permissions.</span></span>

<span data-ttu-id="c01ea-158">在下列情况下，自动程序在频道中可以更好地工作：</span><span class="sxs-lookup"><span data-stu-id="c01ea-158">Bots work better in a channel in the following cases:</span></span>

* <span data-ttu-id="c01ea-159">通知，你提供交互式卡片供用户获取其他信息。</span><span class="sxs-lookup"><span data-stu-id="c01ea-159">Notifications, where you provide an interactive card for users to take additional information.</span></span>
* <span data-ttu-id="c01ea-160">反馈方案，如投票和调查。</span><span class="sxs-lookup"><span data-stu-id="c01ea-160">Feedback scenarios, such as polls and surveys.</span></span>
* <span data-ttu-id="c01ea-161">单个请求或响应周期可解析交互，并且结果对对话中的多个成员很有用。</span><span class="sxs-lookup"><span data-stu-id="c01ea-161">Single request or response cycle resolves interactions and the results are useful for multiple members of the conversation.</span></span>
* <span data-ttu-id="c01ea-162">社交或有趣的机器人，你可获取出色的 cat 图像，随机选择获胜方等。</span><span class="sxs-lookup"><span data-stu-id="c01ea-162">Social or fun bots, where you get an awesome cat image, randomly pick a winner, and so on.</span></span>

### <a name="in-a-group-chat"></a><span data-ttu-id="c01ea-163">在群聊中</span><span class="sxs-lookup"><span data-stu-id="c01ea-163">In a group chat</span></span>

<span data-ttu-id="c01ea-164">群聊是在三个及以上人员之间进行的非按线索组织的对话。</span><span class="sxs-lookup"><span data-stu-id="c01ea-164">Group chats are non-threaded conversations between three or more people.</span></span> <span data-ttu-id="c01ea-165">其中的成员一般比频道中的少且更短暂。</span><span class="sxs-lookup"><span data-stu-id="c01ea-165">They tend to have fewer members than a channel and are more transient.</span></span> <span data-ttu-id="c01ea-166">与频道类似，自动程序仅有权访问直接位于其中 `@mentioned` 的消息。</span><span class="sxs-lookup"><span data-stu-id="c01ea-166">Similar to a channel, your bot only has access to messages where it is `@mentioned` directly.</span></span>

<span data-ttu-id="c01ea-167">在机器人在频道中更好地工作的情况下，也更好地在群聊中工作。</span><span class="sxs-lookup"><span data-stu-id="c01ea-167">In the cases where bots work better in a channel also work better in a group chat.</span></span>

### <a name="in-a-one-to-one-chat"></a><span data-ttu-id="c01ea-168">在一对一聊天中</span><span class="sxs-lookup"><span data-stu-id="c01ea-168">In a one-to-one chat</span></span>

<span data-ttu-id="c01ea-169">一对一聊天是对话机器人与用户交互的传统方式。</span><span class="sxs-lookup"><span data-stu-id="c01ea-169">One-to-one chat is a traditional way for a conversational bot to interact with a user.</span></span> <span data-ttu-id="c01ea-170">一对一对话机器人的一些示例包括 Q&A bot、在其他系统中启动工作流的机器人、告知机器人和记录笔记的机器人。</span><span class="sxs-lookup"><span data-stu-id="c01ea-170">A few examples of one-to-one conversational bots are Q&A bots, bots that initiate workflows in other systems, bots that tell jokes, and bots that take notes.</span></span> <span data-ttu-id="c01ea-171">在创建一对一聊天机器人之前，请考虑基于对话的界面是否是显示功能的最佳方法。</span><span class="sxs-lookup"><span data-stu-id="c01ea-171">Before creating one-to-one chatbots, consider whether a conversation-based interface is the best way to present your functionality.</span></span>

## <a name="disadvantages-of-bots"></a><span data-ttu-id="c01ea-172">机器人的缺点</span><span class="sxs-lookup"><span data-stu-id="c01ea-172">Disadvantages of bots</span></span>

<span data-ttu-id="c01ea-173">自动程序与用户之间的广泛对话是完成任务的一种缓慢而复杂的方法。</span><span class="sxs-lookup"><span data-stu-id="c01ea-173">An extensive dialog between your bot and the user is a slow and complex way to get a task completed.</span></span> <span data-ttu-id="c01ea-174">支持过多命令（尤其是大量命令）的自动程序未成功，或者用户无法积极查看。</span><span class="sxs-lookup"><span data-stu-id="c01ea-174">A bot that supports excessive commands, especially a broad range of commands, is not successful or viewed positively by users.</span></span>

### <a name="have-multi-turn-experiences-in-chat"></a><span data-ttu-id="c01ea-175">在聊天中拥有多轮体验</span><span class="sxs-lookup"><span data-stu-id="c01ea-175">Have multi-turn experiences in chat</span></span>

<span data-ttu-id="c01ea-176">一个广泛的对话框要求开发人员保持状态。</span><span class="sxs-lookup"><span data-stu-id="c01ea-176">An extensive dialog requires the developer to maintain state.</span></span> <span data-ttu-id="c01ea-177">若要退出此状态，用户必须退出 **或选择取消**。</span><span class="sxs-lookup"><span data-stu-id="c01ea-177">To exit this state a user must either time-out or select **Cancel**.</span></span> <span data-ttu-id="c01ea-178">此外，该过程很繁琐。</span><span class="sxs-lookup"><span data-stu-id="c01ea-178">Also, the process is tedious.</span></span> <span data-ttu-id="c01ea-179">例如，请参阅以下对话方案：</span><span class="sxs-lookup"><span data-stu-id="c01ea-179">For example, see the following conversation scenario:</span></span>

<span data-ttu-id="c01ea-180">用户：安排与 Megan 的会议。</span><span class="sxs-lookup"><span data-stu-id="c01ea-180">USER: Schedule a meeting with Megan.</span></span>

<span data-ttu-id="c01ea-181">BOT：我找到了 200 个结果，请包含名字和姓氏。</span><span class="sxs-lookup"><span data-stu-id="c01ea-181">BOT: I’ve found 200 results, please include a first and last name.</span></span>

<span data-ttu-id="c01ea-182">用户：与 Megan Bowen 安排会议。</span><span class="sxs-lookup"><span data-stu-id="c01ea-182">USER: Schedule a meeting with Megan Bowen.</span></span>

<span data-ttu-id="c01ea-183">BOT：好的，你要在什么时间与 Megan Bowen 会面？</span><span class="sxs-lookup"><span data-stu-id="c01ea-183">BOT: OK, what time would you like to meet with Megan Bowen?</span></span>

<span data-ttu-id="c01ea-184">用户：下午 1：00。</span><span class="sxs-lookup"><span data-stu-id="c01ea-184">USER: 1:00 pm.</span></span>

<span data-ttu-id="c01ea-185">BOT：哪一天？</span><span class="sxs-lookup"><span data-stu-id="c01ea-185">BOT: On which day?</span></span>

### <a name="support-too-many-commands"></a><span data-ttu-id="c01ea-186">支持过多命令</span><span class="sxs-lookup"><span data-stu-id="c01ea-186">Support too many commands</span></span>

<span data-ttu-id="c01ea-187">由于当前自动程序菜单中只有六个可见命令，因此不可能以任何频率使用其他任何命令。</span><span class="sxs-lookup"><span data-stu-id="c01ea-187">As there are only six visible commands in the current bot menu, anything more is unlikely to be used with any frequency.</span></span> <span data-ttu-id="c01ea-188">深入到特定领域的机器人，而不是尝试成为广泛的助手，可以更好地工作并提供更好的帮助。</span><span class="sxs-lookup"><span data-stu-id="c01ea-188">Bots that go deep into a specific area rather than trying to be a broad assistant work and fare better.</span></span>

### <a name="maintain-a-large-knowledge-base"></a><span data-ttu-id="c01ea-189">维护大型知识库</span><span class="sxs-lookup"><span data-stu-id="c01ea-189">Maintain a large knowledge base</span></span>

<span data-ttu-id="c01ea-190">自动程序的缺点之一是很难维护具有未应答响应的大型检索知识库。</span><span class="sxs-lookup"><span data-stu-id="c01ea-190">One of the disadvantages of bots is that it is difficult to maintain a large retrieval knowledge base with unranked responses.</span></span> <span data-ttu-id="c01ea-191">自动程序最适合于短而快速交互，而不是通过长列表来寻找答案。</span><span class="sxs-lookup"><span data-stu-id="c01ea-191">Bots are best suited for short, quick interactions, and not sifting through long lists looking for an answer.</span></span>

## <a name="code-sample"></a><span data-ttu-id="c01ea-192">代码示例</span><span class="sxs-lookup"><span data-stu-id="c01ea-192">Code sample</span></span>

|<span data-ttu-id="c01ea-193">示例名称</span><span class="sxs-lookup"><span data-stu-id="c01ea-193">Sample name</span></span> | <span data-ttu-id="c01ea-194">说明</span><span class="sxs-lookup"><span data-stu-id="c01ea-194">Description</span></span> | <span data-ttu-id="c01ea-195">.NETCore</span><span class="sxs-lookup"><span data-stu-id="c01ea-195">.NETCore</span></span> | <span data-ttu-id="c01ea-196">Node.js</span><span class="sxs-lookup"><span data-stu-id="c01ea-196">Node.js</span></span> |
|----------------|-----------------|--------------|----------------|
| <span data-ttu-id="c01ea-197">Teams 对话自动程序</span><span class="sxs-lookup"><span data-stu-id="c01ea-197">Teams conversation bot</span></span> | <span data-ttu-id="c01ea-198">消息和对话事件处理。</span><span class="sxs-lookup"><span data-stu-id="c01ea-198">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="c01ea-199">View</span><span class="sxs-lookup"><span data-stu-id="c01ea-199">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="c01ea-200">View</span><span class="sxs-lookup"><span data-stu-id="c01ea-200">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|

## <a name="next-step"></a><span data-ttu-id="c01ea-201">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c01ea-201">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c01ea-202">智能机器人活动处理程序</span><span class="sxs-lookup"><span data-stu-id="c01ea-202">Bot activity handlers</span></span>](~/bots/bot-basics.md)
