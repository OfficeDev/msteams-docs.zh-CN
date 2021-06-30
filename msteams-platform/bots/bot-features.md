---
title: 智能机器人和 SDK
author: surbhigupta
description: 用于构建自动程序的工具和 SDK Microsoft Teams概述。
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: c346d7b7a1c720e651a847fb8a650fc549689654
ms.sourcegitcommit: f62634c59b697107e5bb3c38867b21007d328b1e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2021
ms.locfileid: "53196241"
---
# <a name="bots-and-sdks"></a><span data-ttu-id="75e4d-103">智能机器人和 SDK</span><span class="sxs-lookup"><span data-stu-id="75e4d-103">Bots and SDKs</span></span>

<span data-ttu-id="75e4d-104">你可以创建适用于以下工具Microsoft Teams之一的聊天机器人：</span><span class="sxs-lookup"><span data-stu-id="75e4d-104">You can create a bot that works in Microsoft Teams with one of the following tools or capabilities:</span></span>

* [<span data-ttu-id="75e4d-105">Microsoft Bot FrameworkSDK</span><span class="sxs-lookup"><span data-stu-id="75e4d-105">Microsoft Bot Framework SDK</span></span>](#bots-with-the-microsoft-bot-framework)
* [<span data-ttu-id="75e4d-106">Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="75e4d-106">Power Virtual Agents</span></span>](#bots-with-power-virtual-agents)
* [<span data-ttu-id="75e4d-107">虚拟助理</span><span class="sxs-lookup"><span data-stu-id="75e4d-107">Virtual Assistant</span></span>](~/samples/virtual-assistant.md)
* [<span data-ttu-id="75e4d-108">Webhook 和连接器</span><span class="sxs-lookup"><span data-stu-id="75e4d-108">Webhooks and connectors</span></span>](#bots-with-webhooks-and-connectors)

## <a name="bots-with-the-microsoft-bot-framework"></a><span data-ttu-id="75e4d-109">具有自动程序Microsoft Bot Framework</span><span class="sxs-lookup"><span data-stu-id="75e4d-109">Bots with the Microsoft Bot Framework</span></span>

<span data-ttu-id="75e4d-110">你的Teams自动程序由以下内容组成：</span><span class="sxs-lookup"><span data-stu-id="75e4d-110">Your Teams bot consists of the following:</span></span>

* <span data-ttu-id="75e4d-111">由你托管的可公开访问的 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="75e4d-111">A publicly accessible web service hosted by you.</span></span>
* <span data-ttu-id="75e4d-112">Web 服务的自动程序框架注册。</span><span class="sxs-lookup"><span data-stu-id="75e4d-112">A Bot Framework registration for your web service.</span></span>
* <span data-ttu-id="75e4d-113">你的Teams应用包，可将Teams客户端连接到 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="75e4d-113">Your Teams app package, which connects the Teams client to your web service.</span></span>

> [!TIP]
> <span data-ttu-id="75e4d-114">使用开发人员门户向 Bot Framework 注册 Web 服务并指定应用配置。</span><span class="sxs-lookup"><span data-stu-id="75e4d-114">Use the Developer Portal to register your web service with the Bot Framework and specify your app configurations.</span></span> <span data-ttu-id="75e4d-115">有关详细信息，请参阅使用开发人员门户[管理应用Teams。](~/concepts/build-and-test/teams-developer-portal.md)</span><span class="sxs-lookup"><span data-stu-id="75e4d-115">For more information, see [manage your apps with the Developer Portal for Teams](~/concepts/build-and-test/teams-developer-portal.md).</span></span>

<span data-ttu-id="75e4d-116">Bot [Framework](https://dev.botframework.com/) 是一个丰富的 SDK，用于创建使用 C#、Java、Python 和 JavaScript 的聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="75e4d-116">The [Bot Framework](https://dev.botframework.com/) is a rich SDK used to create bots using C#, Java, Python, and JavaScript.</span></span> <span data-ttu-id="75e4d-117">如果你已有基于 Bot Framework 的自动程序，你可以轻松修改它以在 Teams。</span><span class="sxs-lookup"><span data-stu-id="75e4d-117">If you already have a bot that is based on the Bot Framework, you can easily modify it to work in Teams.</span></span> <span data-ttu-id="75e4d-118">使用 C# 或 Node.js 来利用[我们的 SDK。](/microsoftteams/platform/#pivot=sdk-tools)</span><span class="sxs-lookup"><span data-stu-id="75e4d-118">Use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="75e4d-119">这些包扩展基本 Bot Builder SDK 类和方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="75e4d-119">These packages extend the basic Bot Builder SDK classes and methods as follows:</span></span>

* <span data-ttu-id="75e4d-120">使用专用卡类型，如Office 365卡。</span><span class="sxs-lookup"><span data-stu-id="75e4d-120">Use specialized card types like the Office 365 connector card.</span></span>
* <span data-ttu-id="75e4d-121">在Teams设置特定于频道的数据。</span><span class="sxs-lookup"><span data-stu-id="75e4d-121">Set Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="75e4d-122">处理邮件扩展请求。</span><span class="sxs-lookup"><span data-stu-id="75e4d-122">Process messaging extension requests.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="75e4d-123">可以使用任何 Web Teams技术开发应用，并直接调用 Bot [Framework REST API。](/bot-framework/rest-api/bot-framework-rest-overview)</span><span class="sxs-lookup"><span data-stu-id="75e4d-123">You can develop Teams apps in any web programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly.</span></span> <span data-ttu-id="75e4d-124">但是，你必须在所有情况下执行令牌处理。</span><span class="sxs-lookup"><span data-stu-id="75e4d-124">But you must perform token handling in all cases.</span></span>

## <a name="bots-with-power-virtual-agents"></a><span data-ttu-id="75e4d-125">具有自动程序Power Virtual Agents</span><span class="sxs-lookup"><span data-stu-id="75e4d-125">Bots with Power Virtual Agents</span></span>

<span data-ttu-id="75e4d-126">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents)是一项基于 Microsoft Power 平台和 Bot Framework 构建的 chatbot 服务。</span><span class="sxs-lookup"><span data-stu-id="75e4d-126">[Power Virtual Agents](/power-virtual-agents/fundamentals-what-is-power-virtual-agents) is a chatbot service built on the Microsoft Power platform and Bot Framework.</span></span> <span data-ttu-id="75e4d-127">Power Virtual Agent 开发过程使用引导式无代码和图形界面方法，使团队成员能够轻松创建和维护智能虚拟代理。</span><span class="sxs-lookup"><span data-stu-id="75e4d-127">The Power Virtual Agent development process uses a guided, no-code, and graphical interface approach that empowers your team members to easily create and maintain an intelligent virtual agent.</span></span> <span data-ttu-id="75e4d-128">在聊天门户创建聊天Power Virtual Agents[后](https://powervirtualagents.microsoft.com)，你可以轻松地[将其与](how-to/add-power-virtual-agents-bot-to-teams.md)Teams 集成。</span><span class="sxs-lookup"><span data-stu-id="75e4d-128">After creating your chatbot in the [Power Virtual Agents portal](https://powervirtualagents.microsoft.com), you can easily [integrate it with Teams](how-to/add-power-virtual-agents-bot-to-teams.md).</span></span> <span data-ttu-id="75e4d-129">有关入门详细信息，请参阅Power Virtual Agents[文档](/power-virtual-agents)。</span><span class="sxs-lookup"><span data-stu-id="75e4d-129">For more information on getting started, see [Power Virtual Agents documentation](/power-virtual-agents).</span></span>

## <a name="bots-with-webhooks-and-connectors"></a><span data-ttu-id="75e4d-130">具有 Webhook 和连接器的机器人</span><span class="sxs-lookup"><span data-stu-id="75e4d-130">Bots with webhooks and connectors</span></span>

<span data-ttu-id="75e4d-131">Webhook 和连接器将机器人连接到 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="75e4d-131">Webhooks and connectors connect your bot to your web services.</span></span> <span data-ttu-id="75e4d-132">使用 webhook 和连接器，可以创建简单的机器人进行基本交互，例如创建工作流或其他简单命令。</span><span class="sxs-lookup"><span data-stu-id="75e4d-132">Using webhooks and connectors, you can create a simple bot for basic interaction, such as creating a workflow or other simple commands.</span></span> <span data-ttu-id="75e4d-133">它们仅在创建它们的团队中可用，并且适用于特定于公司工作流的简单流程。</span><span class="sxs-lookup"><span data-stu-id="75e4d-133">They are available only in the team where you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="75e4d-134">有关详细信息，请参阅什么是 [Webhook 和连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)。</span><span class="sxs-lookup"><span data-stu-id="75e4d-134">For more information, see [what are webhooks and connectors](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

## <a name="advantages-of-bots"></a><span data-ttu-id="75e4d-135">自动程序的优点</span><span class="sxs-lookup"><span data-stu-id="75e4d-135">Advantages of bots</span></span>

<span data-ttu-id="75e4d-136">Microsoft Teams 中的机器人可以进行一对一对话、群聊或参与团队的频道。</span><span class="sxs-lookup"><span data-stu-id="75e4d-136">Bots in Microsoft Teams can be part of a one-to-one conversation, a group chat, or a channel in a team.</span></span> <span data-ttu-id="75e4d-137">每个范围都为对话机器人提供了独特的机遇与挑战。</span><span class="sxs-lookup"><span data-stu-id="75e4d-137">Each scope provides unique opportunities and challenges for your conversational bot.</span></span>

| <span data-ttu-id="75e4d-138">在频道中</span><span class="sxs-lookup"><span data-stu-id="75e4d-138">In a channel</span></span> | <span data-ttu-id="75e4d-139">在群聊中</span><span class="sxs-lookup"><span data-stu-id="75e4d-139">In a group chat</span></span> | <span data-ttu-id="75e4d-140">在一对一聊天中</span><span class="sxs-lookup"><span data-stu-id="75e4d-140">In a one-to-one chat</span></span> |
| :-- | :-- | :-- |
| <span data-ttu-id="75e4d-141">大规模覆盖</span><span class="sxs-lookup"><span data-stu-id="75e4d-141">Massive reach</span></span> | <span data-ttu-id="75e4d-142">成员更少</span><span class="sxs-lookup"><span data-stu-id="75e4d-142">Fewer members</span></span> | <span data-ttu-id="75e4d-143">传统方式</span><span class="sxs-lookup"><span data-stu-id="75e4d-143">Traditional way</span></span> |
| <span data-ttu-id="75e4d-144">简洁的单个交互</span><span class="sxs-lookup"><span data-stu-id="75e4d-144">Concise individual interactions</span></span> | <span data-ttu-id="75e4d-145">@mention自动程序</span><span class="sxs-lookup"><span data-stu-id="75e4d-145">@mention to bot</span></span>  | <span data-ttu-id="75e4d-146">Q&A bots</span><span class="sxs-lookup"><span data-stu-id="75e4d-146">Q&A bots</span></span> |
| <span data-ttu-id="75e4d-147">@mention自动程序</span><span class="sxs-lookup"><span data-stu-id="75e4d-147">@mention to bot</span></span> | <span data-ttu-id="75e4d-148">类似于频道</span><span class="sxs-lookup"><span data-stu-id="75e4d-148">Similar to channel</span></span> | <span data-ttu-id="75e4d-149">告知小人并做笔记的机器人</span><span class="sxs-lookup"><span data-stu-id="75e4d-149">Bots that tell jokes and take notes</span></span> |

### <a name="in-a-channel"></a><span data-ttu-id="75e4d-150">在频道中</span><span class="sxs-lookup"><span data-stu-id="75e4d-150">In a channel</span></span>

<span data-ttu-id="75e4d-151">频道包含多个人员之间的线程对话，甚至最多包含两千个。</span><span class="sxs-lookup"><span data-stu-id="75e4d-151">Channels contain threaded conversations between multiple people even up to two thousand.</span></span> <span data-ttu-id="75e4d-152">这可能会导致自动程序大规模访问，但个人交互必须简洁。</span><span class="sxs-lookup"><span data-stu-id="75e4d-152">This potentially gives your bot massive reach, but individual interactions must be concise.</span></span> <span data-ttu-id="75e4d-153">传统的多向交互不起作用。</span><span class="sxs-lookup"><span data-stu-id="75e4d-153">Traditional multi-turn interactions do not work.</span></span> <span data-ttu-id="75e4d-154">相反，必须查找使用交互式卡片或任务模块，或将对话移动到一对一对话以收集大量信息。</span><span class="sxs-lookup"><span data-stu-id="75e4d-154">Instead, you must look to use interactive cards or task modules, or move the conversation to a one-to-one conversation to collect lots of information.</span></span> <span data-ttu-id="75e4d-155">自动程序仅有权访问其为 的邮件 `@mentioned` 。</span><span class="sxs-lookup"><span data-stu-id="75e4d-155">Your bot only has access to messages where it is `@mentioned`.</span></span> <span data-ttu-id="75e4d-156">您可以使用 Microsoft 权限和组织级别权限从Graph检索其他邮件。</span><span class="sxs-lookup"><span data-stu-id="75e4d-156">You can retrieve additional messages from the conversation using Microsoft Graph and organization-level permissions.</span></span>

<span data-ttu-id="75e4d-157">在下列情况下，自动程序在频道中可以更好地工作：</span><span class="sxs-lookup"><span data-stu-id="75e4d-157">Bots work better in a channel in the following cases:</span></span>

* <span data-ttu-id="75e4d-158">通知，你提供交互式卡片供用户获取其他信息。</span><span class="sxs-lookup"><span data-stu-id="75e4d-158">Notifications, where you provide an interactive card for users to take additional information.</span></span>
* <span data-ttu-id="75e4d-159">反馈方案，如投票和调查。</span><span class="sxs-lookup"><span data-stu-id="75e4d-159">Feedback scenarios, such as polls and surveys.</span></span>
* <span data-ttu-id="75e4d-160">单个请求或响应周期可解析交互，并且结果对对话中的多个成员很有用。</span><span class="sxs-lookup"><span data-stu-id="75e4d-160">Single request or response cycle resolves interactions and the results are useful for multiple members of the conversation.</span></span>
* <span data-ttu-id="75e4d-161">社交或有趣的机器人，你可获取出色的 cat 图像，随机选择获胜方等。</span><span class="sxs-lookup"><span data-stu-id="75e4d-161">Social or fun bots, where you get an awesome cat image, randomly pick a winner, and so on.</span></span>

### <a name="in-a-group-chat"></a><span data-ttu-id="75e4d-162">在群聊中</span><span class="sxs-lookup"><span data-stu-id="75e4d-162">In a group chat</span></span>

<span data-ttu-id="75e4d-163">群聊是在三个及以上人员之间进行的非按线索组织的对话。</span><span class="sxs-lookup"><span data-stu-id="75e4d-163">Group chats are non-threaded conversations between three or more people.</span></span> <span data-ttu-id="75e4d-164">其中的成员一般比频道中的少且更短暂。</span><span class="sxs-lookup"><span data-stu-id="75e4d-164">They tend to have fewer members than a channel and are more transient.</span></span> <span data-ttu-id="75e4d-165">与频道类似，自动程序仅有权访问直接位于其中 `@mentioned` 的消息。</span><span class="sxs-lookup"><span data-stu-id="75e4d-165">Similar to a channel, your bot only has access to messages where it is `@mentioned` directly.</span></span>

<span data-ttu-id="75e4d-166">在机器人在频道中更好地工作的情况下，也更好地在群聊中工作。</span><span class="sxs-lookup"><span data-stu-id="75e4d-166">In the cases where bots work better in a channel also work better in a group chat.</span></span>

### <a name="in-a-one-to-one-chat"></a><span data-ttu-id="75e4d-167">在一对一聊天中</span><span class="sxs-lookup"><span data-stu-id="75e4d-167">In a one-to-one chat</span></span>

<span data-ttu-id="75e4d-168">一对一聊天是对话机器人与用户交互的传统方式。</span><span class="sxs-lookup"><span data-stu-id="75e4d-168">One-to-one chat is a traditional way for a conversational bot to interact with a user.</span></span> <span data-ttu-id="75e4d-169">一对一对话机器人的一些示例包括 Q&A bot、在其他系统中启动工作流的机器人、告知机器人和记录笔记的机器人。</span><span class="sxs-lookup"><span data-stu-id="75e4d-169">A few examples of one-to-one conversational bots are Q&A bots, bots that initiate workflows in other systems, bots that tell jokes, and bots that take notes.</span></span> <span data-ttu-id="75e4d-170">在创建一对一聊天机器人之前，请考虑基于对话的界面是否是显示功能的最佳方法。</span><span class="sxs-lookup"><span data-stu-id="75e4d-170">Before creating one-to-one chatbots, consider whether a conversation-based interface is the best way to present your functionality.</span></span>

## <a name="disadvantages-of-bots"></a><span data-ttu-id="75e4d-171">机器人的缺点</span><span class="sxs-lookup"><span data-stu-id="75e4d-171">Disadvantages of bots</span></span>

<span data-ttu-id="75e4d-172">自动程序与用户之间的广泛对话是完成任务的一种缓慢而复杂的方法。</span><span class="sxs-lookup"><span data-stu-id="75e4d-172">An extensive dialog between your bot and the user is a slow and complex way to get a task completed.</span></span> <span data-ttu-id="75e4d-173">支持过多命令（尤其是大量命令）的自动程序未成功，或者用户无法积极查看。</span><span class="sxs-lookup"><span data-stu-id="75e4d-173">A bot that supports excessive commands, especially a broad range of commands, is not successful or viewed positively by users.</span></span>

### <a name="have-multi-turn-experiences-in-chat"></a><span data-ttu-id="75e4d-174">在聊天中拥有多轮体验</span><span class="sxs-lookup"><span data-stu-id="75e4d-174">Have multi-turn experiences in chat</span></span>

<span data-ttu-id="75e4d-175">一个广泛的对话框要求开发人员保持状态。</span><span class="sxs-lookup"><span data-stu-id="75e4d-175">An extensive dialog requires the developer to maintain state.</span></span> <span data-ttu-id="75e4d-176">若要退出此状态，用户必须退出 **或选择取消**。</span><span class="sxs-lookup"><span data-stu-id="75e4d-176">To exit this state a user must either time-out or select **Cancel**.</span></span> <span data-ttu-id="75e4d-177">此外，该过程很繁琐。</span><span class="sxs-lookup"><span data-stu-id="75e4d-177">Also, the process is tedious.</span></span> <span data-ttu-id="75e4d-178">例如，请参阅以下对话方案：</span><span class="sxs-lookup"><span data-stu-id="75e4d-178">For example, see the following conversation scenario:</span></span>

<span data-ttu-id="75e4d-179">用户：安排与 Megan 的会议。</span><span class="sxs-lookup"><span data-stu-id="75e4d-179">USER: Schedule a meeting with Megan.</span></span>

<span data-ttu-id="75e4d-180">BOT：我找到了 200 个结果，请包含名字和姓氏。</span><span class="sxs-lookup"><span data-stu-id="75e4d-180">BOT: I’ve found 200 results, please include a first and last name.</span></span>

<span data-ttu-id="75e4d-181">用户：与 Megan Bowen 安排会议。</span><span class="sxs-lookup"><span data-stu-id="75e4d-181">USER: Schedule a meeting with Megan Bowen.</span></span>

<span data-ttu-id="75e4d-182">BOT：好的，你要在什么时间与 Megan Bowen 会面？</span><span class="sxs-lookup"><span data-stu-id="75e4d-182">BOT: OK, what time would you like to meet with Megan Bowen?</span></span>

<span data-ttu-id="75e4d-183">用户：下午 1：00。</span><span class="sxs-lookup"><span data-stu-id="75e4d-183">USER: 1:00 pm.</span></span>

<span data-ttu-id="75e4d-184">BOT：哪一天？</span><span class="sxs-lookup"><span data-stu-id="75e4d-184">BOT: On which day?</span></span>

### <a name="support-too-many-commands"></a><span data-ttu-id="75e4d-185">支持过多命令</span><span class="sxs-lookup"><span data-stu-id="75e4d-185">Support too many commands</span></span>

<span data-ttu-id="75e4d-186">由于当前自动程序菜单中只有六个可见命令，因此不可能以任何频率使用其他任何命令。</span><span class="sxs-lookup"><span data-stu-id="75e4d-186">As there are only six visible commands in the current bot menu, anything more is unlikely to be used with any frequency.</span></span> <span data-ttu-id="75e4d-187">深入到特定领域的机器人，而不是尝试成为广泛的助手，可以更好地工作并提供更好的帮助。</span><span class="sxs-lookup"><span data-stu-id="75e4d-187">Bots that go deep into a specific area rather than trying to be a broad assistant work and fare better.</span></span>

### <a name="maintain-a-large-knowledge-base"></a><span data-ttu-id="75e4d-188">维护大型知识库</span><span class="sxs-lookup"><span data-stu-id="75e4d-188">Maintain a large knowledge base</span></span>

<span data-ttu-id="75e4d-189">自动程序的缺点之一是很难维护具有未应答响应的大型检索知识库。</span><span class="sxs-lookup"><span data-stu-id="75e4d-189">One of the disadvantages of bots is that it is difficult to maintain a large retrieval knowledge base with unranked responses.</span></span> <span data-ttu-id="75e4d-190">自动程序最适合于短而快速交互，而不是通过长列表来寻找答案。</span><span class="sxs-lookup"><span data-stu-id="75e4d-190">Bots are best suited for short, quick interactions, and not sifting through long lists looking for an answer.</span></span>

## <a name="code-sample"></a><span data-ttu-id="75e4d-191">代码示例</span><span class="sxs-lookup"><span data-stu-id="75e4d-191">Code sample</span></span>

|<span data-ttu-id="75e4d-192">示例名称</span><span class="sxs-lookup"><span data-stu-id="75e4d-192">Sample name</span></span> | <span data-ttu-id="75e4d-193">说明</span><span class="sxs-lookup"><span data-stu-id="75e4d-193">Description</span></span> | <span data-ttu-id="75e4d-194">.NETCore</span><span class="sxs-lookup"><span data-stu-id="75e4d-194">.NETCore</span></span> | <span data-ttu-id="75e4d-195">Node.js</span><span class="sxs-lookup"><span data-stu-id="75e4d-195">Node.js</span></span> |
|----------------|-----------------|--------------|----------------|
| <span data-ttu-id="75e4d-196">Teams 对话自动程序</span><span class="sxs-lookup"><span data-stu-id="75e4d-196">Teams conversation bot</span></span> | <span data-ttu-id="75e4d-197">消息和对话事件处理。</span><span class="sxs-lookup"><span data-stu-id="75e4d-197">Messaging and conversation event handling.</span></span> |[<span data-ttu-id="75e4d-198">View</span><span class="sxs-lookup"><span data-stu-id="75e4d-198">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="75e4d-199">View</span><span class="sxs-lookup"><span data-stu-id="75e4d-199">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)|

## <a name="next-step"></a><span data-ttu-id="75e4d-200">后续步骤</span><span class="sxs-lookup"><span data-stu-id="75e4d-200">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="75e4d-201">智能机器人活动处理程序</span><span class="sxs-lookup"><span data-stu-id="75e4d-201">Bot activity handlers</span></span>](~/bots/bot-basics.md)
