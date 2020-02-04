---
title: 什么是对话 bot？
author: clearab
description: Microsoft 团队中的会话 bot 概述。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 7bde886b67788a355181c83287d999a3bfb9727a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673117"
---
# <a name="what-are-conversational-bots"></a><span data-ttu-id="64c8c-103">什么是对话 bot？</span><span class="sxs-lookup"><span data-stu-id="64c8c-103">What are conversational bots?</span></span>

<span data-ttu-id="64c8c-104">会话 bot 使用户能够通过文本、交互式卡片和任务模块与 web 服务进行交互。</span><span class="sxs-lookup"><span data-stu-id="64c8c-104">Conversational bots allow users to interact with your web service through text, interactive cards, and task modules.</span></span> <span data-ttu-id="64c8c-105">它们的灵活性非常灵活—会话间的 bot 可用于处理几个简单的命令或复杂、人工智能的智能化和自然语言处理虚拟助理。</span><span class="sxs-lookup"><span data-stu-id="64c8c-105">They're incredibly flexible — conversational bots can be scoped to handling a few simple commands or complex, artificial intelligence powered and natural language processing virtual assistants.</span></span> <span data-ttu-id="64c8c-106">它们可以是大型应用程序的一个方面，也可以完全独立。</span><span class="sxs-lookup"><span data-stu-id="64c8c-106">They can be one aspect of a larger application, or completely stand alone.</span></span>

<span data-ttu-id="64c8c-107">下面的 GIF 显示了用户使用文本和交互式卡片同时在一对一聊天中与 bot 聊天。</span><span class="sxs-lookup"><span data-stu-id="64c8c-107">The GIF below shows a user conversing with a bot in a one-to-one chat using both text and interactive cards.</span></span> <span data-ttu-id="64c8c-108">查找卡片、文本和任务模块的正确组合是创建有用的 bot 的关键所在。</span><span class="sxs-lookup"><span data-stu-id="64c8c-108">Finding the right mix of cards, text, and task modules is key to creating a useful bot.</span></span> <span data-ttu-id="64c8c-109">别忘了，机器人要远不止是文本！</span><span class="sxs-lookup"><span data-stu-id="64c8c-109">Don't forget, bots are much more than just text!</span></span>

![FAQ 加 gif](~/assets/images/FAQPlusEndUser.gif)

## <a name="what-tasks-are-best-handled-by-bots"></a><span data-ttu-id="64c8c-111">哪些任务最适合通过 bot 处理？</span><span class="sxs-lookup"><span data-stu-id="64c8c-111">What tasks are best handled by bots?</span></span>

<span data-ttu-id="64c8c-112">Microsoft 团队中的 bot 可以是一对一对话、组聊天或团队中的频道的一部分。</span><span class="sxs-lookup"><span data-stu-id="64c8c-112">Bots in Microsoft Teams can be part of a one-to-one conversation, a group chat, or a channel in a Team.</span></span> <span data-ttu-id="64c8c-113">每个范围都将为您的会话 bot 提供独特的机会和挑战。</span><span class="sxs-lookup"><span data-stu-id="64c8c-113">Each scope will provide unique opportunities, and challenges, for your conversational bot.</span></span>

### <a name="in-a-channel"></a><span data-ttu-id="64c8c-114">通道中</span><span class="sxs-lookup"><span data-stu-id="64c8c-114">In a channel</span></span>

<span data-ttu-id="64c8c-115">频道包含多个用户之间的线程对话—可能有很多人（目前最多为2000）。</span><span class="sxs-lookup"><span data-stu-id="64c8c-115">Channels contain threaded conversations between multiple people — potentially lots of people (currently, up to two thousand).</span></span> <span data-ttu-id="64c8c-116">这可能会为你的 bot 提供大规模的访问，但各个交互需要简明。</span><span class="sxs-lookup"><span data-stu-id="64c8c-116">This potentially gives your bot massive reach, but individual interactions need to be concise.</span></span> <span data-ttu-id="64c8c-117">传统的多项交互操作可能不会很好。</span><span class="sxs-lookup"><span data-stu-id="64c8c-117">Traditional multi-turn interactions probably won't work well.</span></span> <span data-ttu-id="64c8c-118">相反，如果需要收集大量信息，请查看使用互动卡片或任务模块，或者可能将对话移动到一对一对话中。</span><span class="sxs-lookup"><span data-stu-id="64c8c-118">Instead, look to use interactive cards or task modules, or potentially move the conversation to a one-to-one conversation if you need to collect lots of information.</span></span> <span data-ttu-id="64c8c-119">你的 bot 也只能访问直接访问邮件的`@mentioned`邮件，无法使用 Microsoft Graph 和提升的组织级别权限从对话中检索其他邮件。</span><span class="sxs-lookup"><span data-stu-id="64c8c-119">Your bot will also only have access to messages where it's `@mentioned` directly, you cannot retrieve additional messages from the conversation using Microsoft Graph and elevated organization-level permissions.</span></span>

<span data-ttu-id="64c8c-120">在频道中 excel 的一些应用场景包括：</span><span class="sxs-lookup"><span data-stu-id="64c8c-120">Some scenarios where bots excel in a channel include:</span></span>

* <span data-ttu-id="64c8c-121">**通知**，尤其是为用户提供用于获取其他信息的互动卡片时。</span><span class="sxs-lookup"><span data-stu-id="64c8c-121">**Notifications**, particularly if you provide an interactive card for users to take additional information.</span></span>
* <span data-ttu-id="64c8c-122">**反馈方案**，如投票和调查。</span><span class="sxs-lookup"><span data-stu-id="64c8c-122">**Feedback scenarios** like polls and surveys.</span></span>
* <span data-ttu-id="64c8c-123">可在**单个请求/响应周期**中解决的交互，其中的结果对对话的多个成员很有用。</span><span class="sxs-lookup"><span data-stu-id="64c8c-123">Interactions that can be resolved in a **single request/response cycle**, where the results are useful for multiple members of the conversation.</span></span>
* <span data-ttu-id="64c8c-124">**社交/趣味 bot** —获取非常棒的 cat 图像，随机挑选获奖者等。</span><span class="sxs-lookup"><span data-stu-id="64c8c-124">**Social/fun bots** — get an awesome cat image, randomly pick a winner, etc.</span></span>

### <a name="in-a-group-chat"></a><span data-ttu-id="64c8c-125">在群聊中</span><span class="sxs-lookup"><span data-stu-id="64c8c-125">In a group chat</span></span>

<span data-ttu-id="64c8c-126">组聊天是三个或更多人之间的非线程对话。</span><span class="sxs-lookup"><span data-stu-id="64c8c-126">Group chats are non-threaded conversations between three or more people.</span></span> <span data-ttu-id="64c8c-127">它们的成员数往往少于通道，并且更具暂时性。</span><span class="sxs-lookup"><span data-stu-id="64c8c-127">They tend to have fewer members than a channel, and are more transient.</span></span> <span data-ttu-id="64c8c-128">与频道类似，你的`@mentioned` bot 仅可直接访问邮件。</span><span class="sxs-lookup"><span data-stu-id="64c8c-128">Similar to a channel, your bot will only have access to messages where it's `@mentioned` directly.</span></span>

<span data-ttu-id="64c8c-129">在频道中正常工作的方案通常在组聊天中也会起作用。</span><span class="sxs-lookup"><span data-stu-id="64c8c-129">Scenarios that work well in a channel will usually work just as well in a group chat.</span></span>

### <a name="in-a-one-to-one-chat"></a><span data-ttu-id="64c8c-130">以一对一聊天</span><span class="sxs-lookup"><span data-stu-id="64c8c-130">In a one-to-one chat</span></span>

<span data-ttu-id="64c8c-131">这是对话机器人与用户进行交互的传统方法。</span><span class="sxs-lookup"><span data-stu-id="64c8c-131">This is the traditional way for a conversational bot to interact with a user.</span></span> <span data-ttu-id="64c8c-132">他们可以实现多元化不同的工作负载。</span><span class="sxs-lookup"><span data-stu-id="64c8c-132">They can enable incredibly diverse workloads.</span></span> <span data-ttu-id="64c8c-133">问：&bot、在其他系统中启动工作流的 bot、通知笑话的 bot 以及记录笔记的 bot 只是几个示例。</span><span class="sxs-lookup"><span data-stu-id="64c8c-133">Q&A bots, bots that initiate workflows in other systems, bots that tell jokes, and bots that take notes are just a few examples.</span></span> <span data-ttu-id="64c8c-134">只需记住，应考虑基于会话的界面是否是展示功能的最佳方式。</span><span class="sxs-lookup"><span data-stu-id="64c8c-134">Just remember to consider whether a conversation-based interface is the best way to present your functionality.</span></span>

## <a name="how-do-bots-work"></a><span data-ttu-id="64c8c-135">Bot 的工作原理是什么？</span><span class="sxs-lookup"><span data-stu-id="64c8c-135">How do bots work?</span></span>

<span data-ttu-id="64c8c-136">你的 bot 由三部分组成：</span><span class="sxs-lookup"><span data-stu-id="64c8c-136">Your bot consists of three pieces:</span></span>

* <span data-ttu-id="64c8c-137">您承载的可公开访问的 web 服务。</span><span class="sxs-lookup"><span data-stu-id="64c8c-137">A publicly accessible web service that you host.</span></span>
* <span data-ttu-id="64c8c-138">您的 bot 注册，用于向 Bot 框架注册你的 bot。</span><span class="sxs-lookup"><span data-stu-id="64c8c-138">Your bot registration that registers your bot with the Bot Framework.</span></span>
* <span data-ttu-id="64c8c-139">您的团队应用程序包，其中包含您的应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="64c8c-139">Your Teams app package that contains your app manifest.</span></span> <span data-ttu-id="64c8c-140">这是您的用户安装并将团队客户端连接到 web 服务（通过 Bot 服务路由）的内容。</span><span class="sxs-lookup"><span data-stu-id="64c8c-140">This is what your users install and connects the Teams client to your web service (routed through the Bot Service).</span></span>

<span data-ttu-id="64c8c-141">Microsoft 团队的 bot 基于[Microsoft Bot 框架](https://dev.botframework.com/)构建。</span><span class="sxs-lookup"><span data-stu-id="64c8c-141">Bots for Microsoft Teams are built on the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span> <span data-ttu-id="64c8c-142">（如果已经有一个基于 Bot 框架的 bot，可以轻松地将其调整为在 Microsoft 团队中工作。）我们建议您使用 c # 或 node.js 来利用我们的[sdk](/microsoftteams/platform/#pivot=sdk-tools)。</span><span class="sxs-lookup"><span data-stu-id="64c8c-142">(If you already have a bot that's based on the Bot Framework, you can easily adapt it to work in Microsoft Teams.) We recommend you use either C# or Node.js to take advantage of our [SDKs](/microsoftteams/platform/#pivot=sdk-tools).</span></span> <span data-ttu-id="64c8c-143">这些包扩展了基本的 Bot 生成器 SDK 类和方法：</span><span class="sxs-lookup"><span data-stu-id="64c8c-143">These packages extend the basic Bot Builder SDK classes and methods:</span></span>

* <span data-ttu-id="64c8c-144">使用专用的卡片类型，如 Office 365 连接器卡。</span><span class="sxs-lookup"><span data-stu-id="64c8c-144">Using specialized card types like the Office 365 Connector card.</span></span>
* <span data-ttu-id="64c8c-145">使用和设置针对活动的特定于团队的频道数据。</span><span class="sxs-lookup"><span data-stu-id="64c8c-145">Consuming and setting Teams-specific channel data on activities.</span></span>
* <span data-ttu-id="64c8c-146">处理消息扩展请求。</span><span class="sxs-lookup"><span data-stu-id="64c8c-146">Processing messaging extension requests.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="64c8c-147">您可以在任何 web 编程技术中开发团队应用程序，并直接调用[Bot 框架 REST api](/bot-framework/rest-api/bot-framework-rest-overview) ，但您必须自己执行所有令牌处理。</span><span class="sxs-lookup"><span data-stu-id="64c8c-147">You can develop Teams apps in any web-programming technology and call the [Bot Framework REST APIs](/bot-framework/rest-api/bot-framework-rest-overview) directly, but you must perform all token handling yourself.</span></span>

<span data-ttu-id="64c8c-148">*团队应用程序 Studio*可帮助您创建和配置应用程序清单，并可将 web 服务注册为 bot 框架上的 bot。</span><span class="sxs-lookup"><span data-stu-id="64c8c-148">*Teams App Studio* helps you create and configure your app manifest, and can register your web service as a bot on the Bot Framework.</span></span> <span data-ttu-id="64c8c-149">它还包含响应控制库和交互式卡片生成器。</span><span class="sxs-lookup"><span data-stu-id="64c8c-149">It also contains a React control library and an interactive card builder.</span></span> <span data-ttu-id="64c8c-150">*请参阅*[开始使用团队应用 Studio](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="64c8c-150">*See* [Getting started with Teams App Studio](~/concepts/build-and-test/app-studio-overview.md).</span></span>

## <a name="webhooks-and-connectors"></a><span data-ttu-id="64c8c-151">Webhook 和连接器</span><span class="sxs-lookup"><span data-stu-id="64c8c-151">Webhooks and connectors</span></span>

<span data-ttu-id="64c8c-152">Webhook 和连接器允许您创建简单的 bot 来实现基本交互，例如启动脱离工作流或其他简单命令。</span><span class="sxs-lookup"><span data-stu-id="64c8c-152">Webhooks and connectors allow you to create a simple bot for basic interaction, like kicking off a workflow or other simple commands.</span></span> <span data-ttu-id="64c8c-153">它们仅在您创建它们的团队中运行，适用于特定于贵公司的工作流的简单流程。</span><span class="sxs-lookup"><span data-stu-id="64c8c-153">They live only in the team in which you create them and are intended for simple processes specific to your company's workflow.</span></span> <span data-ttu-id="64c8c-154">*请参阅*[什么是 webhook 和连接器？](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)有关详细信息，请参阅。</span><span class="sxs-lookup"><span data-stu-id="64c8c-154">*See* [What are webhooks and connectors?](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) for more information.</span></span>

## <a name="get-started"></a><span data-ttu-id="64c8c-155">入门</span><span class="sxs-lookup"><span data-stu-id="64c8c-155">Get started</span></span>

* [<span data-ttu-id="64c8c-156">C # 中的团队对话机器人/dotnet</span><span class="sxs-lookup"><span data-stu-id="64c8c-156">Teams conversation bot in C#/dotnet</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/57.teams-conversation-bot)
* [<span data-ttu-id="64c8c-157">JavaScript 中的团队对话机器人</span><span class="sxs-lookup"><span data-stu-id="64c8c-157">Teams conversation bot in JavaScript</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/57.teams-conversation-bot)

## <a name="learn-more"></a><span data-ttu-id="64c8c-158">了解更多</span><span class="sxs-lookup"><span data-stu-id="64c8c-158">Learn more</span></span>

* [<span data-ttu-id="64c8c-159">团队中的 bot 的基础知识</span><span class="sxs-lookup"><span data-stu-id="64c8c-159">The basics of bots in Teams</span></span>](~/bots/bot-basics.md)
* [<span data-ttu-id="64c8c-160">为团队创建机器人</span><span class="sxs-lookup"><span data-stu-id="64c8c-160">Create a bot for Teams</span></span>](~/bots/how-to/create-a-bot-for-teams.md)
