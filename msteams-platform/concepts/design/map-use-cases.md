---
title: 将用例映射到Teams功能
author: clearab
description: 确定你的应用用例在应用体验Teams工作。
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 271bb38a9d8cc3d9921c757b6fc722754bb63017
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101770"
---
# <a name="map-your-use-cases-to-teams-app-capabilities"></a><span data-ttu-id="c7589-103">将用例映射到Teams功能</span><span class="sxs-lookup"><span data-stu-id="c7589-103">Map your use cases to Teams app capabilities</span></span>

<span data-ttu-id="c7589-104">确定用户 *是谁* 以及要解决的问题后，可以决定 *如何* 解决问题了。</span><span class="sxs-lookup"><span data-stu-id="c7589-104">After you have identified *who* the user is and *what* problem you will solve, it is time to decide *how* to solve the problem.</span></span> <span data-ttu-id="c7589-105">The *who，* *what*， and *how* completes the process of understanding and mapping your use cases to Teams app capabilities.</span><span class="sxs-lookup"><span data-stu-id="c7589-105">The *who*, *what*, and *how* completes the process of understanding and mapping your use cases to Teams app capabilities.</span></span> <span data-ttu-id="c7589-106">你需要根据从用户收到的查询响应来定义应用的范围，然后确定最适合生成应用的功能。</span><span class="sxs-lookup"><span data-stu-id="c7589-106">You need to define the scope of the app based on the responses you have received from the user to your queries, and then decide which capability is best suited to build your app.</span></span>

> [!NOTE]
> <span data-ttu-id="c7589-107">你必须深入了解可用于应用的 [入口点和 UI](../../concepts/extensibility-points.md) 元素。</span><span class="sxs-lookup"><span data-stu-id="c7589-107">You must have a good understanding of the [entry points and UI elements](../../concepts/extensibility-points.md) available for your app.</span></span> <span data-ttu-id="c7589-108">此外，还必须确保仔细考虑 [用例](../../concepts/design/understand-use-cases.md) 。</span><span class="sxs-lookup"><span data-stu-id="c7589-108">You must also make sure that you [considered your use cases](../../concepts/design/understand-use-cases.md) carefully.</span></span>

## <a name="choose-the-correct-scope-for-your-app"></a><span data-ttu-id="c7589-109">为应用选择正确的作用域</span><span class="sxs-lookup"><span data-stu-id="c7589-109">Choose the correct scope for your app</span></span>

<span data-ttu-id="c7589-110">选择应用范围时，请考虑以下事项：</span><span class="sxs-lookup"><span data-stu-id="c7589-110">While choosing the app scope, consider the following:</span></span>

* <span data-ttu-id="c7589-111">应用可以跨范围存在。</span><span class="sxs-lookup"><span data-stu-id="c7589-111">An app can exist across scopes.</span></span>
* <span data-ttu-id="c7589-112">应用功能（如邮件扩展）可跨范围关注用户。</span><span class="sxs-lookup"><span data-stu-id="c7589-112">App capabilities, such as messaging extensions, follow users across scopes.</span></span>
* <span data-ttu-id="c7589-113">用户通常对将应用添加到频道或Teams很不一样。</span><span class="sxs-lookup"><span data-stu-id="c7589-113">Users are often hesitant to add apps to Teams or channels.</span></span>
* <span data-ttu-id="c7589-114">来宾用户可以访问在一个或多个Teams公开的内容。</span><span class="sxs-lookup"><span data-stu-id="c7589-114">Guest users can access content exposed in Teams or channels.</span></span>

<span data-ttu-id="c7589-115">你可以根据以下条件在个人范围和团队或频道范围之间选择：</span><span class="sxs-lookup"><span data-stu-id="c7589-115">You can choose between personal scope and team or channel scope for your app depending on the following:</span></span>

* <span data-ttu-id="c7589-116">对于个人范围，请提出以下问题：</span><span class="sxs-lookup"><span data-stu-id="c7589-116">For personal scope, ask the following questions:</span></span>
  * <span data-ttu-id="c7589-117">出于隐私或其他原因，是否要求与应用进行一对一交互？</span><span class="sxs-lookup"><span data-stu-id="c7589-117">Are there one-on-one interactions with the app required for privacy or other reasons?</span></span> <span data-ttu-id="c7589-118">例如，检查休假余额或其他私人信息。</span><span class="sxs-lookup"><span data-stu-id="c7589-118">For example, checking leave balance or other private information.</span></span>
  * <span data-ttu-id="c7589-119">用户之间是否可能没有任何共同协作Teams？</span><span class="sxs-lookup"><span data-stu-id="c7589-119">Is there going to be collaboration among users who might not have any common Teams?</span></span> <span data-ttu-id="c7589-120">例如，在公司中查找即将推出的组织范围事件。</span><span class="sxs-lookup"><span data-stu-id="c7589-120">For example, finding upcoming organization wide events in a company.</span></span>
  * <span data-ttu-id="c7589-121">在应用体验中，是否需要向用户发送任何Teams消息？</span><span class="sxs-lookup"><span data-stu-id="c7589-121">Are there any personalized notifications or messages that will need to be sent to a user throughout the Teams app experience?</span></span> <span data-ttu-id="c7589-122">例如，审批或注册提醒。</span><span class="sxs-lookup"><span data-stu-id="c7589-122">For example, reminders for approvals or registrations.</span></span>
* <span data-ttu-id="c7589-123">对于共享范围 (团队、频道或聊天) ，请提出以下问题：</span><span class="sxs-lookup"><span data-stu-id="c7589-123">For a shared scope (team, channel, or chat), ask the following questions:</span></span>
  * <span data-ttu-id="c7589-124">应用在选项卡或机器人中呈现的信息是否与团队中的大多数成员相关且有用？</span><span class="sxs-lookup"><span data-stu-id="c7589-124">Is the information presented by the app, either in tab or through a bot, relevant and useful for most members in a Team?</span></span> <span data-ttu-id="c7589-125">例如，Scrum 应用。</span><span class="sxs-lookup"><span data-stu-id="c7589-125">For example, Scrum app.</span></span>
  * <span data-ttu-id="c7589-126">应用上下文是否可能随应用添加到的团队而更改？</span><span class="sxs-lookup"><span data-stu-id="c7589-126">Could the app’s context change depending on the team in which it is added to?</span></span> <span data-ttu-id="c7589-127">例如，Planner 的任务在不同团队中有所不同。</span><span class="sxs-lookup"><span data-stu-id="c7589-127">For example, Planner’s tasks are different in different teams.</span></span> 
  * <span data-ttu-id="c7589-128">需要协作的人物中的所有成员是否可能是单个团队的一部分？</span><span class="sxs-lookup"><span data-stu-id="c7589-128">Is it possible that all members in a persona who need to collaborate are a part of a single team?</span></span> <span data-ttu-id="c7589-129">例如，处理票证的代理。</span><span class="sxs-lookup"><span data-stu-id="c7589-129">For example, agents working on a ticket.</span></span>

<span data-ttu-id="c7589-130">以下方案将指导你了解与应用功能良好协作的入口点和 UI Teams选择：</span><span class="sxs-lookup"><span data-stu-id="c7589-130">The following scenarios will guide you in understanding the selection of entry points and UI elements that work well with Teams app capabilities:</span></span>

> [!NOTE]
> <span data-ttu-id="c7589-131">这不是一个详尽的列表，但有助于你思考一些可用的可能性。</span><span class="sxs-lookup"><span data-stu-id="c7589-131">It is not an exhaustive list, but will help you think through some of the possibilities available to you.</span></span>

## <a name="create-share-and-collaborate-on-items-in-an-external-system"></a><span data-ttu-id="c7589-132">在外部系统中创建、共享和协作处理项目</span><span class="sxs-lookup"><span data-stu-id="c7589-132">Create, share, and collaborate on items in an external system</span></span>

<span data-ttu-id="c7589-133">Microsoft Teams应用是一种与数据交互的不错方法，并且有多种集成点可供选择。</span><span class="sxs-lookup"><span data-stu-id="c7589-133">App for Microsoft Teams is a great way to interact with your data and there are a variety of integration points to choose from.</span></span>

* <span data-ttu-id="c7589-134">**使用搜索命令的邮件扩展**：搜索外部系统，并作为交互式卡片共享结果。</span><span class="sxs-lookup"><span data-stu-id="c7589-134">**Messaging extensions with search commands**: Search external systems and share the results as an interactive card.</span></span>

* <span data-ttu-id="c7589-135">**使用操作命令的消息** 扩展：收集信息以插入数据存储或执行高级搜索。</span><span class="sxs-lookup"><span data-stu-id="c7589-135">**Messaging extensions with action commands**: Collect information to insert into a data store or perform advanced searches.</span></span>

* <span data-ttu-id="c7589-136">**选项卡**：创建用于查看、处理和共享数据的嵌入式 Web 体验。</span><span class="sxs-lookup"><span data-stu-id="c7589-136">**Tabs**: Create embedded web experiences to view, work with and share data.</span></span>

* <span data-ttu-id="c7589-137">**连接器和 webhook：** 一种将数据推送和发送出客户端的简单Teams方法。</span><span class="sxs-lookup"><span data-stu-id="c7589-137">**Connectors and webhooks**: A simple way to push data and send data out of the Teams client.</span></span>

* <span data-ttu-id="c7589-138">**任务模块**：需要它们收集或显示信息的交互式模式表单。</span><span class="sxs-lookup"><span data-stu-id="c7589-138">**Task modules**: Interactive modal forms from wherever you need them to collect or display information.</span></span>

## <a name="initiate-workflows-and-processes"></a><span data-ttu-id="c7589-139">启动工作流和流程</span><span class="sxs-lookup"><span data-stu-id="c7589-139">Initiate workflows and processes</span></span>

<span data-ttu-id="c7589-140">有时，只需一种在外部系统中快速启动流程或工作流的方法。</span><span class="sxs-lookup"><span data-stu-id="c7589-140">Sometimes you just need a quick way to start a process or workflow in an external system.</span></span>

* <span data-ttu-id="c7589-141">**邮件扩展操作命令**：从邮件触发，允许用户将邮件内容快速发送到 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="c7589-141">**Messaging extensions action commands**: Trigger from messages, allowing your users to quickly send the contents of a message to your web services.</span></span>

* <span data-ttu-id="c7589-142">**任务模块**：在启动工作流之前，从选项卡、自动程序或消息传递扩展中打开它们以收集信息。</span><span class="sxs-lookup"><span data-stu-id="c7589-142">**Task modules**: Open them from a tab, a bot, or a messaging extension to collect information before initiating a workflow.</span></span>

* <span data-ttu-id="c7589-143">**对话机器人**：通过文本和富卡片与用户交互。</span><span class="sxs-lookup"><span data-stu-id="c7589-143">**Conversational bots**: Interact with your users through text and rich cards.</span></span>

* <span data-ttu-id="c7589-144">**传出 Webhook：** 当你不需要生成整个对话机器人时，进行简单的来回交互是一个不错的选择。</span><span class="sxs-lookup"><span data-stu-id="c7589-144">**Outgoing webhooks**: A good choice for a simple back-and-forth interaction when you don't need to build an entire conversational bot.</span></span>

## <a name="send-notifications-and-alerts"></a><span data-ttu-id="c7589-145">发送通知和警报</span><span class="sxs-lookup"><span data-stu-id="c7589-145">Send notifications and alerts</span></span>

<span data-ttu-id="c7589-146">向用户发送异步通知和通知，Teams。</span><span class="sxs-lookup"><span data-stu-id="c7589-146">Send asynchronous notifications and alerts to your users in Teams.</span></span> <span data-ttu-id="c7589-147">使用交互式卡片可以快速访问常用操作和指向其他信息的链接。</span><span class="sxs-lookup"><span data-stu-id="c7589-147">Use interactive cards to provide quick access to commonly used actions and links to additional information.</span></span>

* <span data-ttu-id="c7589-148">**对话机器人**：向组、频道或单个用户发送主动消息。</span><span class="sxs-lookup"><span data-stu-id="c7589-148">**Conversational bots**: Send proactive messages to groups, channels, or individual users.</span></span>

* <span data-ttu-id="c7589-149">**连接器和传入 Webhook：** 允许订阅频道以接收邮件。</span><span class="sxs-lookup"><span data-stu-id="c7589-149">**Connectors and incoming webhooks**: Permit a channel to subscribe to receive messages.</span></span> <span data-ttu-id="c7589-150">连接器允许用户使用配置页面定制订阅。</span><span class="sxs-lookup"><span data-stu-id="c7589-150">A connector lets users tailor the subscription with a configuration page.</span></span>

## <a name="ask-questions-and-get-answers"></a><span data-ttu-id="c7589-151">提问并获取答案</span><span class="sxs-lookup"><span data-stu-id="c7589-151">Ask questions and get answers</span></span>

<span data-ttu-id="c7589-152">人们有疑问，你可能会得到存储在某处的很多答案。</span><span class="sxs-lookup"><span data-stu-id="c7589-152">People have questions and you probably got a lot of the answers stored away somewhere.</span></span> <span data-ttu-id="c7589-153">遗憾的是，连接这两者通常非常困难。</span><span class="sxs-lookup"><span data-stu-id="c7589-153">Unfortunately, it's often quite difficult to connect the two.</span></span>

* <span data-ttu-id="c7589-154">**对话机器人**：自然语言处理、AI、机器学习以及所有话题。</span><span class="sxs-lookup"><span data-stu-id="c7589-154">**Conversational bots**: Natural language processing, AI, machine learning, and all the buzzwords.</span></span> <span data-ttu-id="c7589-155">使用由智能云支持自动程序将用户连接到他们需要的答案。</span><span class="sxs-lookup"><span data-stu-id="c7589-155">Use a bot powered by the intelligent cloud to connect your users to the answers they need.</span></span>

* <span data-ttu-id="c7589-156">**选项卡**：将现有 Web 门户嵌入Teams或为添加Teams创建特定于 Web 门户的版本。</span><span class="sxs-lookup"><span data-stu-id="c7589-156">**Tabs**: Embed your existing web portal in Teams or create a Teams-specific version for added functionality.</span></span>

## <a name="get-social"></a><span data-ttu-id="c7589-157">获取社交</span><span class="sxs-lookup"><span data-stu-id="c7589-157">Get social</span></span>

<span data-ttu-id="c7589-158">协作平台本质上是一个社交平台。</span><span class="sxs-lookup"><span data-stu-id="c7589-158">A collaboration platform is inherently a social platform.</span></span> <span data-ttu-id="c7589-159">让创造力的一面是免费的，为工作场所添加一些有趣的内容。</span><span class="sxs-lookup"><span data-stu-id="c7589-159">Let your creative side be free and add some fun into your workplace.</span></span> <span data-ttu-id="c7589-160">所有用户都必须能够发送彩信、提供 kudos、获取一些 meme、删除一些表情符号或其他任何能够影响你奇特感的符号。</span><span class="sxs-lookup"><span data-stu-id="c7589-160">All users must be able to send jokes, give kudos, get some memes, toss out some emojis, or anything else that strikes your fancy.</span></span>

## <a name="think-in-terms-of-a-single-page-app"></a><span data-ttu-id="c7589-161">从单页应用考虑</span><span class="sxs-lookup"><span data-stu-id="c7589-161">Think in terms of a single-page app</span></span>

<span data-ttu-id="c7589-162">选项卡是嵌入式网页。</span><span class="sxs-lookup"><span data-stu-id="c7589-162">Tabs are embedded web pages.</span></span> <span data-ttu-id="c7589-163">您可以在 SPA 中执行几乎任何操作，您可以在 Teams 中的选项卡中Teams。</span><span class="sxs-lookup"><span data-stu-id="c7589-163">Pretty much anything you can do in a SPA, you can do in a tab in Teams.</span></span> <span data-ttu-id="c7589-164">只需注意作用域。</span><span class="sxs-lookup"><span data-stu-id="c7589-164">Just be sure to pay attention to scope.</span></span> <span data-ttu-id="c7589-165">组和频道选项卡用于共享体验，个人选项卡用于个人体验。</span><span class="sxs-lookup"><span data-stu-id="c7589-165">Group and channel tabs are for shared experiences and personal tabs are for personal experiences.</span></span> <span data-ttu-id="c7589-166">团队的资料列表位于频道选项卡上，而资料列表在个人选项卡中。</span><span class="sxs-lookup"><span data-stu-id="c7589-166">The team's list of stuff goes on the channel tab and the list of your stuff goes in the personal tab.</span></span>

## <a name="start-small"></a><span data-ttu-id="c7589-167">小型启动</span><span class="sxs-lookup"><span data-stu-id="c7589-167">Start small</span></span>

<span data-ttu-id="c7589-168">不确定从何处开始？</span><span class="sxs-lookup"><span data-stu-id="c7589-168">Not sure where to start?</span></span> <span data-ttu-id="c7589-169">觉得使用各种可用选项有点不知所措？</span><span class="sxs-lookup"><span data-stu-id="c7589-169">Feeling a bit overwhelmed with the awesome variety of options available to you?</span></span> <span data-ttu-id="c7589-170">你必须选择应用的核心功能，然后开始操作。</span><span class="sxs-lookup"><span data-stu-id="c7589-170">You must choose a core feature of your app and start there.</span></span> <span data-ttu-id="c7589-171">在了解信息通过环境中的各个上下文Teams后，可以更加简单地了解更复杂的交互。</span><span class="sxs-lookup"><span data-stu-id="c7589-171">After you get a feel for the flow of information through the various contexts in Teams, it is a lot simpler to picture a more complex interaction.</span></span>

## <a name="put-it-all-together"></a><span data-ttu-id="c7589-172">全部放在一起</span><span class="sxs-lookup"><span data-stu-id="c7589-172">Put it all together</span></span>

<span data-ttu-id="c7589-173">也就是说，最佳应用通常组合多个功能，从而创建在正确的上下文中使用正确功能吸引用户的应用。</span><span class="sxs-lookup"><span data-stu-id="c7589-173">That being said, the best apps usually combine multiple features, creating an app that engages users in the right context with the right functionality at the right time.</span></span> <span data-ttu-id="c7589-174">不得将任何功能强制放入不属于它的位置。</span><span class="sxs-lookup"><span data-stu-id="c7589-174">You must not force any functionality into a place it does not belong.</span></span> <span data-ttu-id="c7589-175">仅仅因为有一对一对话机器人，并不意味着将其添加到任何团队。</span><span class="sxs-lookup"><span data-stu-id="c7589-175">Just because you have a good one-to-one conversational bot does not mean you add it to any team.</span></span> <span data-ttu-id="c7589-176">不同的扩展点适用于不同的内容，可以发挥它们创建成功应用的优势。</span><span class="sxs-lookup"><span data-stu-id="c7589-176">Different extensibility points are good for different things, play to their strengths for creating a successful app.</span></span>

## <a name="see-also"></a><span data-ttu-id="c7589-177">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c7589-177">See also</span></span>

* [<span data-ttu-id="c7589-178">构建 Microsoft Teams 应用</span><span class="sxs-lookup"><span data-stu-id="c7589-178">Build apps for Microsoft Teams</span></span>](../../overview.md)
