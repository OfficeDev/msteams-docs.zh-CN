---
title: 什么是邮件扩展？
author: clearab
description: Microsoft 团队平台上的邮件扩展概述
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 3ea9649a22ecc134e983037d1ef109be918a26b3
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587795"
---
# <a name="what-are-messaging-extensions"></a><span data-ttu-id="27cea-103">什么是邮件扩展？</span><span class="sxs-lookup"><span data-stu-id="27cea-103">What are messaging extensions?</span></span>

<span data-ttu-id="27cea-104">邮件扩展允许用户通过 Microsoft 团队客户端中的按钮和表单与 web 服务进行交互。</span><span class="sxs-lookup"><span data-stu-id="27cea-104">Messaging extensions allow users to interact with your web service through buttons and forms in the Microsoft Teams client.</span></span> <span data-ttu-id="27cea-105">他们可以通过撰写邮件区域、命令框或直接从邮件中搜索或启动外部系统中的操作。</span><span class="sxs-lookup"><span data-stu-id="27cea-105">They can search, or initiate actions, in an external system from the compose message area, the command box, or directly from a message.</span></span> <span data-ttu-id="27cea-106">然后，您可以将该交互的结果发送回 Microsoft 团队客户端（通常采用格式丰富的卡片的形式）。</span><span class="sxs-lookup"><span data-stu-id="27cea-106">You can then send the results of that interaction back to the Microsoft Teams client, typically in the form of a richly formatted card.</span></span>

<span data-ttu-id="27cea-107">下面的屏幕截图显示可以从中调用邮件扩展的位置。</span><span class="sxs-lookup"><span data-stu-id="27cea-107">The screenshot below shows the locations where messaging extensions can be invoked from.</span></span>

![消息扩展调用位置](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="what-kinds-of-tasks-are-they-good-for"></a><span data-ttu-id="27cea-109">哪些类型的任务适合？</span><span class="sxs-lookup"><span data-stu-id="27cea-109">What kinds of tasks are they good for?</span></span>

<span data-ttu-id="27cea-110">**方案：** 我需要一些外部系统执行某些操作，并希望将操作的结果发送回我的对话。</span><span class="sxs-lookup"><span data-stu-id="27cea-110">**Scenario:** I need some external system to do something and I want the result of the action to be sent back to my conversation.\</span></span>
<span data-ttu-id="27cea-111">**示例：** 预订资源并让频道知道您为其预留的日期/时间。</span><span class="sxs-lookup"><span data-stu-id="27cea-111">**Example:** Reserve a resource and let the channel know what day/time you reserved it for.</span></span>

<span data-ttu-id="27cea-112">**方案：** 我需要在外部系统中查找内容，我想要与我的对话共享结果。</span><span class="sxs-lookup"><span data-stu-id="27cea-112">**Scenario:** I need to find something in an external system, and I want to share the results with my conversation.\</span></span>
<span data-ttu-id="27cea-113">**示例：** 在 Azure DevOps 中搜索工作项，并将其与组共享为自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="27cea-113">**Example:**  Search for a work item in Azure DevOps, and share it with the group as an adaptive card.</span></span>

<span data-ttu-id="27cea-114">**方案：** 我需要在外部系统中完成涉及多个步骤 (或大量信息) 的复杂任务，并且应与会话共享结果。</span><span class="sxs-lookup"><span data-stu-id="27cea-114">**Scenario:** I need to complete a complex task involving multiple steps (or lots of information) in an external system, and the results should be shared with a conversation.\</span></span>
<span data-ttu-id="27cea-115">**示例：** 在跟踪系统中创建基于团队消息的 bug，将该 bug 分配给 Bob，然后将卡片发送给会话线程，并提供 bug 的详细信息。</span><span class="sxs-lookup"><span data-stu-id="27cea-115">**Example:** Create a bug in your tracking system based on a Teams message, assign that bug to Bob, then send a card to the conversation thread with the bug's details.</span></span>

## <a name="how-do-messaging-extensions-work"></a><span data-ttu-id="27cea-116">邮件扩展功能扩展的工作原理是什么？</span><span class="sxs-lookup"><span data-stu-id="27cea-116">How do messaging extensions work?</span></span>

<span data-ttu-id="27cea-117">邮件扩展由您承载的 web 服务和应用程序清单组成，该服务定义在 Microsoft 团队客户端中可从何处调用 web 服务。</span><span class="sxs-lookup"><span data-stu-id="27cea-117">A messaging extension consists of a web service you host and your app manifest which defines where your web service can be invoked from in the Microsoft Teams client.</span></span> <span data-ttu-id="27cea-118">他们利用 Bot 框架的邮件架构和安全通信协议，因此您还需要将 web 服务注册为 Bot 框架中的 bot。</span><span class="sxs-lookup"><span data-stu-id="27cea-118">They take advantage of the Bot Framework's messaging schema and secure communication protocol, so you'll also need to register your web service as a bot in the Bot Framework.</span></span> <span data-ttu-id="27cea-119">尽管您可以手动创建 web 服务，但我们建议您充分利用[Bot 框架 SDK](https://github.com/microsoft/botframework)来更简单地使用协议。</span><span class="sxs-lookup"><span data-stu-id="27cea-119">Although you can create your web service completely by hand, we recommend you take advantage of the [Bot Framework SDK](https://github.com/microsoft/botframework) to make working with the protocol simpler.</span></span>

<span data-ttu-id="27cea-120">在 Microsoft 团队应用程序的应用程序清单中，你将定义最大为十个不同命令的单一消息扩展。</span><span class="sxs-lookup"><span data-stu-id="27cea-120">In the app manifest for your Microsoft Teams app you'll define a single messaging extension with up to ten different commands.</span></span> <span data-ttu-id="27cea-121">每个命令定义一种类型 (操作或搜索) ，并且客户端中的位置可以从 (撰写邮件区域、命令栏和/或邮件) 中调用。</span><span class="sxs-lookup"><span data-stu-id="27cea-121">Each command defines a type (action or search), and the locations in the client it can be invoked from (compose message area, command bar, and/or message).</span></span> <span data-ttu-id="27cea-122">调用后，web 服务将收到具有 JSON 有效负载的 HTTPS 消息，其中包括所有相关信息。</span><span class="sxs-lookup"><span data-stu-id="27cea-122">Once invoked, your web service will receive an HTTPS message with a JSON payload including all the relevant information.</span></span> <span data-ttu-id="27cea-123">你将使用 JSON 有效负载进行响应，让团队客户端了解下一步要启用的交互。</span><span class="sxs-lookup"><span data-stu-id="27cea-123">You'll respond with a JSON payload, letting the Teams client know what interaction to enable next.</span></span>

## <a name="types-of-messaging-extension-commands"></a><span data-ttu-id="27cea-124">邮件扩展命令的类型</span><span class="sxs-lookup"><span data-stu-id="27cea-124">Types of messaging extension commands</span></span>

<span data-ttu-id="27cea-125">消息扩展命令的类型定义了可用于 web 服务的 UI 元素和交互流。</span><span class="sxs-lookup"><span data-stu-id="27cea-125">The type of messaging extension command defines the UI elements and interaction flows available to your web service.</span></span> <span data-ttu-id="27cea-126">某些交互（如身份验证和配置）可用于这两种类型的命令。</span><span class="sxs-lookup"><span data-stu-id="27cea-126">Some interactions, like authentication and configuration, are available for both types of commands.</span></span>

### <a name="action-commands"></a><span data-ttu-id="27cea-127">操作命令</span><span class="sxs-lookup"><span data-stu-id="27cea-127">Action commands</span></span>

<span data-ttu-id="27cea-128">操作命令使您可以向用户呈现模式弹出窗口，以收集或显示信息。</span><span class="sxs-lookup"><span data-stu-id="27cea-128">Action commands allow you to present your users with a modal popup to collect or display information.</span></span> <span data-ttu-id="27cea-129">当用户提交表单时，您的 web 服务可以通过直接在对话中插入邮件，或在撰写邮件区域中插入邮件并允许用户提交邮件来做出响应。</span><span class="sxs-lookup"><span data-stu-id="27cea-129">When they submit the form, your web service can respond by inserting a message into the conversation directly, or by inserting a message into the compose message area and allowing the user to submit the message.</span></span> <span data-ttu-id="27cea-130">甚至可以将多个表单链接在一起，以获取更复杂的工作流。</span><span class="sxs-lookup"><span data-stu-id="27cea-130">You can even chain multiple forms together for more complex workflows.</span></span>

<span data-ttu-id="27cea-131">它们可以通过撰写邮件区域、命令框或邮件触发。</span><span class="sxs-lookup"><span data-stu-id="27cea-131">They can be triggered from the compose message area, the command box, or from a message.</span></span> <span data-ttu-id="27cea-132">从邮件中调用时，发送到你的 bot 的初始 JSON 有效负载将包含从中调用的整个邮件。</span><span class="sxs-lookup"><span data-stu-id="27cea-132">When invoked from a message, the initial JSON payload sent to your bot will include the entire message it was invoked from.</span></span>

![邮件扩展操作命令任务模块](~/assets/images/task-module.png)

### <a name="search-commands"></a><span data-ttu-id="27cea-134">搜索命令</span><span class="sxs-lookup"><span data-stu-id="27cea-134">Search commands</span></span>

<span data-ttu-id="27cea-135">搜索命令允许用户在搜索框中手动搜索外部系统，或者通过将指向受监视域的链接粘贴到 "撰写" 邮件区域中来 (的信息) ，然后将搜索结果插入到邮件中。</span><span class="sxs-lookup"><span data-stu-id="27cea-135">Search commands allow your users to search an external system for information (either manually through a search box, or by pasting a link to a monitored domain into the compose message area), then insert the results of the search into a message.</span></span> <span data-ttu-id="27cea-136">在最基本的搜索命令流中，初始调用邮件将包含用户提交的搜索字符串。</span><span class="sxs-lookup"><span data-stu-id="27cea-136">In the most basic search command flow, the initial invoke message will include the search string the user submitted.</span></span> <span data-ttu-id="27cea-137">你将使用卡片和卡片预览的列表进行响应。</span><span class="sxs-lookup"><span data-stu-id="27cea-137">You'll respond with a list of cards and card previews.</span></span> <span data-ttu-id="27cea-138">团队客户端将在列表中呈现卡片预览，以便最终用户可以从中进行选择。</span><span class="sxs-lookup"><span data-stu-id="27cea-138">The Teams client will render the card previews in a list for the end user to select from.</span></span> <span data-ttu-id="27cea-139">当用户选择卡片时，完整大小的卡片将插入到撰写邮件区域中。</span><span class="sxs-lookup"><span data-stu-id="27cea-139">When the user selects a card, the full-size card will be inserted into the compose message area.</span></span>

<span data-ttu-id="27cea-140">它们可以通过撰写消息区域或命令框触发。</span><span class="sxs-lookup"><span data-stu-id="27cea-140">They can be triggered from the compose message area or the command box.</span></span> <span data-ttu-id="27cea-141">与 action 命令不同，它们不能从邮件中触发。</span><span class="sxs-lookup"><span data-stu-id="27cea-141">Unlike action commands, they cannot be triggered from a message.</span></span>

![邮件扩展搜索命令](~/assets/images/search-extension.png)

### <a name="link-unfurling"></a><span data-ttu-id="27cea-143">链接展开</span><span class="sxs-lookup"><span data-stu-id="27cea-143">Link unfurling</span></span>

<span data-ttu-id="27cea-144">在将 URL 粘贴到撰写邮件区域中时，您还可以选择调用您的服务。</span><span class="sxs-lookup"><span data-stu-id="27cea-144">You also have the option to invoke your service when a URL is pasted in the compose message area.</span></span> <span data-ttu-id="27cea-145">此功能称为**链接 unfurling**，使您可以在将包含特定域的 url 粘贴到撰写邮件区域时订阅接收调用。</span><span class="sxs-lookup"><span data-stu-id="27cea-145">This functionality, known as **link unfurling**, allows you to subscribe to receive an invoke when URLs containing a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="27cea-146">您的 web 服务可以将 URL "unfurl" 到详细卡片中，提供的信息比标准网站预览卡更多。</span><span class="sxs-lookup"><span data-stu-id="27cea-146">Your web service can "unfurl" the URL into a detailed card, providing more information than the standard website preview card.</span></span> <span data-ttu-id="27cea-147">您甚至可以添加按钮以允许用户立即执行操作，而无需离开 Microsoft 团队客户端。</span><span class="sxs-lookup"><span data-stu-id="27cea-147">You can even add buttons to allow your users to immediately take action without leaving the Microsoft Teams client.</span></span>

## <a name="get-started"></a><span data-ttu-id="27cea-148">开始使用</span><span class="sxs-lookup"><span data-stu-id="27cea-148">Get Started</span></span>

<span data-ttu-id="27cea-149">准备好开始构建了吗？</span><span class="sxs-lookup"><span data-stu-id="27cea-149">Ready to get started building?</span></span> <span data-ttu-id="27cea-150">尝试一下我们的快速入门：</span><span class="sxs-lookup"><span data-stu-id="27cea-150">Try one of our quickstarts:</span></span>

* <span data-ttu-id="27cea-151">**C#**</span><span class="sxs-lookup"><span data-stu-id="27cea-151">**C#**</span></span>
  * [<span data-ttu-id="27cea-152">带有基于操作的命令的消息扩展</span><span class="sxs-lookup"><span data-stu-id="27cea-152">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="27cea-153">包含基于搜索的命令的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="27cea-153">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)
* <span data-ttu-id="27cea-154">**JavaScript**</span><span class="sxs-lookup"><span data-stu-id="27cea-154">**JavaScript**</span></span>
  * [<span data-ttu-id="27cea-155">带有基于操作的命令的消息扩展</span><span class="sxs-lookup"><span data-stu-id="27cea-155">Messaging extension with action-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action)
  * [<span data-ttu-id="27cea-156">包含基于搜索的命令的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="27cea-156">Messaging extension with search-based commands</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)

## <a name="learn-more"></a><span data-ttu-id="27cea-157">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="27cea-157">Learn more</span></span>

<span data-ttu-id="27cea-158">构建消息扩展：</span><span class="sxs-lookup"><span data-stu-id="27cea-158">Build a messaging extension:</span></span>

* [<span data-ttu-id="27cea-159">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="27cea-159">Create a messaging extension</span></span>](~/messaging-extensions/how-to/create-messaging-extension.md)
* [<span data-ttu-id="27cea-160">定义操作消息扩展命令</span><span class="sxs-lookup"><span data-stu-id="27cea-160">Define action messaging extension command</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)
* [<span data-ttu-id="27cea-161">定义搜索邮件扩展命令</span><span class="sxs-lookup"><span data-stu-id="27cea-161">Define search messaging extension command</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)
