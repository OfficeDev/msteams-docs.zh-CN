---
title: 将用例映射到应用程序功能
author: clearab
description: 决定如何分发您的应用程序
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5ebfa73df9b4f2c83533a33fbc6366c2c0ccffb4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673322"
---
# <a name="map-your-use-cases-to-teams-app-capabilities"></a><span data-ttu-id="d2950-103">将用例映射到团队应用程序功能</span><span class="sxs-lookup"><span data-stu-id="d2950-103">Map your use cases to teams app capabilities</span></span>

<span data-ttu-id="d2950-104">如果你还没有，请确保你已认真[考虑了你的用例](~/concepts/design/map-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="d2950-104">If you haven't already, make sure you've [considered your use cases](~/concepts/design/map-use-cases.md) carefully.</span></span> <span data-ttu-id="d2950-105">此外，您还应充分了解适用于您的应用程序的[扩展性点和 UI 元素](~/concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="d2950-105">You should also have a good understanding of the [extensibility points and UI elements](~/concepts/extensibility-points.md) available for your app.</span></span> <span data-ttu-id="d2950-106">在确定了您尝试解决的*内容*以及您要解决的*用户*后，就可以开始考虑*如何*操作。</span><span class="sxs-lookup"><span data-stu-id="d2950-106">Once you've figured out *what* your trying to solve, and *who* you're solving it for, it is time to start thinking about *how*.</span></span>

<span data-ttu-id="d2950-107">在下面，你将发现一些常见方案，以及可与它们配合使用的扩展性点和 UI 元素的选择。</span><span class="sxs-lookup"><span data-stu-id="d2950-107">Below you'll find some common scenarios, and a selection of extensibility points and UI elements that work well with them.</span></span> <span data-ttu-id="d2950-108">它并不打算成为一个详尽的列表，只是为了帮助您考虑一些适用于您和团队平台的可能。</span><span class="sxs-lookup"><span data-stu-id="d2950-108">It isn't intended to be an exhaustive list, just to help you think through some of the possibilities available to you and the Teams platform.</span></span>

## <a name="create-share-and-collaborate-on-items-in-an-external-system"></a><span data-ttu-id="d2950-109">对外部系统中的项目创建、共享和协作</span><span class="sxs-lookup"><span data-stu-id="d2950-109">Create, share and collaborate on items in an external system</span></span>

<span data-ttu-id="d2950-110">Microsoft 团队的应用程序是与数据进行交互的一种非常好的方法，可从中选择多种集成点。</span><span class="sxs-lookup"><span data-stu-id="d2950-110">App for Microsoft Teams are a great way to interact with your data, and there are a variety of integration points to choose from.</span></span>

* <span data-ttu-id="d2950-111">带有搜索命令的邮件扩展-搜索外部系统并将结果共享为交互式卡。</span><span class="sxs-lookup"><span data-stu-id="d2950-111">Messaging extensions with search commands - Search external systems and share the results as an interactive card.</span></span>

* <span data-ttu-id="d2950-112">带有操作命令的邮件扩展-收集要插入到数据存储或执行高级搜索的信息。</span><span class="sxs-lookup"><span data-stu-id="d2950-112">Messaging extensions with action commands - Collect information to insert into a data store or perform advanced searches.</span></span>

* <span data-ttu-id="d2950-113">选项卡-创建嵌入的 web 体验以查看、使用和共享数据。</span><span class="sxs-lookup"><span data-stu-id="d2950-113">Tabs - Create embedded web experiences to view, work with, and share data.</span></span>

* <span data-ttu-id="d2950-114">连接器和 webhook-将数据推送到中并将数据发送到团队客户端的简单方法。</span><span class="sxs-lookup"><span data-stu-id="d2950-114">Connectors and webhooks - A simple way to push data into, and send data out of the Teams client.</span></span>

* <span data-ttu-id="d2950-115">任务模块-从任何需要它们收集或显示信息的交互模式窗体。</span><span class="sxs-lookup"><span data-stu-id="d2950-115">Task modules - Interactive modal forms from wherever you need them to collect or display information.</span></span>

## <a name="initiate-workflows-and-processes"></a><span data-ttu-id="d2950-116">启动工作流和过程</span><span class="sxs-lookup"><span data-stu-id="d2950-116">Initiate workflows and processes</span></span>

<span data-ttu-id="d2950-117">有时，您只需在外部系统中启动流程或工作流的快速方法即可。</span><span class="sxs-lookup"><span data-stu-id="d2950-117">Sometimes you just need a quick way to start a process or workflow in an external system.</span></span>

* <span data-ttu-id="d2950-118">邮件扩展操作命令-从邮件中触发，使用户可以将邮件的内容快速发送到 web 服务。</span><span class="sxs-lookup"><span data-stu-id="d2950-118">Messaging extensions action commands - Trigger from messages, allowing your users to quickly send the contents of a message to your web services.</span></span>

* <span data-ttu-id="d2950-119">任务模块-在启动工作流之前，从选项卡、bot 或邮件扩展中打开它们，以收集信息。</span><span class="sxs-lookup"><span data-stu-id="d2950-119">Task modules - Open them from a tab, a bot, or a messaging extension to collect information before initiating a workflow.</span></span>

* <span data-ttu-id="d2950-120">会话 bot-通过文本和丰富卡片与您的用户进行交互。</span><span class="sxs-lookup"><span data-stu-id="d2950-120">Conversational bots - Interact with your users through text and rich cards.</span></span>

* <span data-ttu-id="d2950-121">传出的 webhook-当您无需构建整个对话机器人时，简单的后端交互是一种很好的选择。</span><span class="sxs-lookup"><span data-stu-id="d2950-121">Outgoing webhooks - A good choice for a simple back-and-forth interaction when you don't need to build an entire conversational bot.</span></span>

## <a name="send-notifications-and-alerts"></a><span data-ttu-id="d2950-122">发送通知和警报</span><span class="sxs-lookup"><span data-stu-id="d2950-122">Send notifications and alerts</span></span>

<span data-ttu-id="d2950-123">向团队中的用户发送异步通知和警报。</span><span class="sxs-lookup"><span data-stu-id="d2950-123">Send asynchronous notifications and alerts to your users in Teams.</span></span> <span data-ttu-id="d2950-124">使用交互式卡片提供对常用操作的快速访问以及指向其他信息的链接。</span><span class="sxs-lookup"><span data-stu-id="d2950-124">Use interactive cards to provide quick access to commonly used actions and links to additional information.</span></span>

* <span data-ttu-id="d2950-125">会话 bot-向组、频道或单个用户发送主动消息。</span><span class="sxs-lookup"><span data-stu-id="d2950-125">Conversational bots - Send proactive messages to groups, channels, or individual users.</span></span>

* <span data-ttu-id="d2950-126">连接器 & 传入 webhook-允许通道订阅接收邮件。</span><span class="sxs-lookup"><span data-stu-id="d2950-126">Connectors & incoming webhooks - Allow a channel to subscribe to receive messages.</span></span> <span data-ttu-id="d2950-127">通过使用连接器，用户可以使用配置页面自适应订阅。</span><span class="sxs-lookup"><span data-stu-id="d2950-127">With a connector let users tailor the subscription with a configuration page.</span></span>

## <a name="ask-questions-and-get-answers"></a><span data-ttu-id="d2950-128">提出问题并获取答案</span><span class="sxs-lookup"><span data-stu-id="d2950-128">Ask questions and get answers</span></span>

<span data-ttu-id="d2950-129">人有问题。</span><span class="sxs-lookup"><span data-stu-id="d2950-129">People have questions.</span></span> <span data-ttu-id="d2950-130">您可能已将很多答案存储在某个位置。</span><span class="sxs-lookup"><span data-stu-id="d2950-130">You've probably got a lot of the answers stored away somewhere.</span></span> <span data-ttu-id="d2950-131">遗憾的是，将两者连接在一起通常相当困难。</span><span class="sxs-lookup"><span data-stu-id="d2950-131">Unfortunately, its often quite difficult to connect the two together.</span></span>

* <span data-ttu-id="d2950-132">会话 bot-自然语言处理、AI、机器学习和所有 buzzwords。</span><span class="sxs-lookup"><span data-stu-id="d2950-132">Conversational bots - Natural language processing, AI, machine learning, all the buzzwords.</span></span> <span data-ttu-id="d2950-133">使用智能云所支持的 bot 将用户连接到所需的答案。</span><span class="sxs-lookup"><span data-stu-id="d2950-133">Use a bot powered by the intelligent cloud to connect your users to the answers they need.</span></span>

* <span data-ttu-id="d2950-134">选项卡-在团队中嵌入现有 web 门户，或创建特定于团队的版本以添加功能。</span><span class="sxs-lookup"><span data-stu-id="d2950-134">Tabs - Embed your existing web portal in Teams, or create a Teams-specific version for added functionality.</span></span>

## <a name="get-social"></a><span data-ttu-id="d2950-135">获取社交</span><span class="sxs-lookup"><span data-stu-id="d2950-135">Get social</span></span>

<span data-ttu-id="d2950-136">协作平台本身就是社交平台。</span><span class="sxs-lookup"><span data-stu-id="d2950-136">A collaboration platform is inherently a social platform.</span></span> <span data-ttu-id="d2950-137">让你的创意面免费，并在工作区中添加一些有趣的娱乐。</span><span class="sxs-lookup"><span data-stu-id="d2950-137">Let your creative side be free, and add some fun into your workplace.</span></span>

* <span data-ttu-id="d2950-138">所有用户-发送笑话、提供荣誉、获取一些 meme、丢弃一些表情或任何其他的您别致的东西。</span><span class="sxs-lookup"><span data-stu-id="d2950-138">All of them - Send jokes, give kudos, get some memes, toss out some emoji's or whatever else strikes your fancy.</span></span>

## <a name="anything-you-can-do-in-a-single-page-app-spa"></a><span data-ttu-id="d2950-139">可以在单个页面应用程序（SPA）中执行的任何操作</span><span class="sxs-lookup"><span data-stu-id="d2950-139">Anything you can do in a Single Page App (SPA)</span></span>

<span data-ttu-id="d2950-140">选项卡是嵌入的网页。</span><span class="sxs-lookup"><span data-stu-id="d2950-140">Tabs are embedded web pages.</span></span> <span data-ttu-id="d2950-141">您可以在 SPA 中执行的操作非常多，您可以在团队中的选项卡上执行操作。</span><span class="sxs-lookup"><span data-stu-id="d2950-141">Pretty much anything you can do in a SPA, you can do in a tab in Teams.</span></span> <span data-ttu-id="d2950-142">只需确保为 "范围组" 和 "频道" 选项卡提供 "共享体验"，个人选项卡适用于 .。。个人体验。</span><span class="sxs-lookup"><span data-stu-id="d2950-142">Just be sure to pay attention to scope - group and channel tabs are for shared experiences, personal tabs are for ... personal experiences.</span></span> <span data-ttu-id="d2950-143">工作组的资料列表在 "频道" 选项卡上，您的资料列表将放在 "个人" 选项卡中。</span><span class="sxs-lookup"><span data-stu-id="d2950-143">The team's list of stuff goes on the channel tab, the list of your stuff goes in the personal tab.</span></span>

## <a name="start-small"></a><span data-ttu-id="d2950-144">启动小型</span><span class="sxs-lookup"><span data-stu-id="d2950-144">Start small</span></span>

<span data-ttu-id="d2950-145">不确定从哪里开始？</span><span class="sxs-lookup"><span data-stu-id="d2950-145">Not sure where to start?</span></span> <span data-ttu-id="d2950-146">感到对你可用的各种选项，感到有点不知所措？</span><span class="sxs-lookup"><span data-stu-id="d2950-146">Feeling a bit overwhelmed with the awesome variety of options available to you?</span></span> <span data-ttu-id="d2950-147">不要 fret，请选择您的应用程序的核心功能并启动此处。</span><span class="sxs-lookup"><span data-stu-id="d2950-147">Don't fret, choose a core feature of your app and start there.</span></span> <span data-ttu-id="d2950-148">一旦通过团队中的各种上下文对信息流进行了感受，更简单的操作就是将更复杂的交互与图片进行比较。</span><span class="sxs-lookup"><span data-stu-id="d2950-148">Once you get a feel for the flow of information through the various contexts in Teams, it will be a lot simpler to picture a more complex interaction.</span></span>

## <a name="putting-it-all-together"></a><span data-ttu-id="d2950-149">汇总</span><span class="sxs-lookup"><span data-stu-id="d2950-149">Putting it all together</span></span>

<span data-ttu-id="d2950-150">也就是说，最佳应用程序通常会组合多种功能，从而创建一个应用程序，在适当的时间使用适当的功能在适当的上下文中参与用户。</span><span class="sxs-lookup"><span data-stu-id="d2950-150">That being said, the best apps usually combine multiple features, creating an app that engages users in the right context with the right functionality at the right time.</span></span> <span data-ttu-id="d2950-151">请勿尝试将功能强制置于不属于其中的位置，因为如果你具有良好的一对一会话机器人并不意味着你只需将其添加到团队即可。</span><span class="sxs-lookup"><span data-stu-id="d2950-151">Don't try to force functionality into a place it doesn't belong - just because you've got a good one-to-one conversational bot doesn't mean you should just add it to a team.</span></span> <span data-ttu-id="d2950-152">不同的扩展点对于不同的情况很有用;请在其优势中发挥作用，你的应用将会照射。</span><span class="sxs-lookup"><span data-stu-id="d2950-152">Different extensibility points are good for different things; play to their strengths and your app will shine.</span></span>
