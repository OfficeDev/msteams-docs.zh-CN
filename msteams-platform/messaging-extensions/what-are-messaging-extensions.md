---
title: 消息扩展
author: clearab
description: 邮件扩展在 Microsoft Teams 概述
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: ee59a7ad96572f5a8ebc6afedd2e0e8485169e5a
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075666"
---
# <a name="messaging-extensions"></a><span data-ttu-id="8901d-103">消息扩展</span><span class="sxs-lookup"><span data-stu-id="8901d-103">Messaging extensions</span></span>

<span data-ttu-id="8901d-104">邮件扩展允许用户通过客户端中的按钮和表单与 web Microsoft Teams交互。</span><span class="sxs-lookup"><span data-stu-id="8901d-104">Messaging extensions allow the users to interact with your web service through buttons and forms in the Microsoft Teams client.</span></span> <span data-ttu-id="8901d-105">他们可以从撰写邮件区域、命令框或直接从邮件搜索或启动外部系统中的操作。</span><span class="sxs-lookup"><span data-stu-id="8901d-105">They can search or initiate actions in an external system from the compose message area, the command box, or directly from a message.</span></span> <span data-ttu-id="8901d-106">你可以以格式丰富的卡片的形式将交互结果发送回 Microsoft Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="8901d-106">You can send back the results of that interaction to the Microsoft Teams client in the form of a richly formatted card.</span></span> <span data-ttu-id="8901d-107">本文档概述了邮件扩展、在不同方案中执行的任务、邮件扩展的工作、操作和搜索命令以及链接取消点击。</span><span class="sxs-lookup"><span data-stu-id="8901d-107">This document gives an overview of the messaging extension, tasks performed under different scenarios, working of messaging extension, action and search commands, and link unfurling.</span></span>

<span data-ttu-id="8901d-108">下图显示了调用邮件扩展的位置：</span><span class="sxs-lookup"><span data-stu-id="8901d-108">The following image displays the locations from where messaging extensions are invoked:</span></span>

![消息扩展调用位置](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="scenarios-where-messaging-extensions-are-used"></a><span data-ttu-id="8901d-110">使用邮件扩展的方案</span><span class="sxs-lookup"><span data-stu-id="8901d-110">Scenarios where messaging extensions are used</span></span>

| <span data-ttu-id="8901d-111">应用场景</span><span class="sxs-lookup"><span data-stu-id="8901d-111">Scenario</span></span> | <span data-ttu-id="8901d-112">示例</span><span class="sxs-lookup"><span data-stu-id="8901d-112">Example</span></span> |
|:-----------------|:-----------------|
|<span data-ttu-id="8901d-113">您希望某些外部系统执行一个操作，并且此操作的结果将发送回您的对话。</span><span class="sxs-lookup"><span data-stu-id="8901d-113">You want some external system to do an action  and the result of the action to be sent back to your conversation.</span></span>|<span data-ttu-id="8901d-114">预留资源并允许频道知道预留的时间段。</span><span class="sxs-lookup"><span data-stu-id="8901d-114">Reserve a resource and allow the channel to know the reserved time slot.</span></span>|
|<span data-ttu-id="8901d-115">您希望在外部系统中查找内容，并与对话共享结果。</span><span class="sxs-lookup"><span data-stu-id="8901d-115">You want to find something in an external system, and share the results with the conversation.</span></span>|<span data-ttu-id="8901d-116">在工作组中搜索工作项Azure DevOps，并作为自适应卡片与组共享。</span><span class="sxs-lookup"><span data-stu-id="8901d-116">Search for a work item in Azure DevOps, and share it with the group as an Adaptive Card.</span></span>|
|<span data-ttu-id="8901d-117">您希望完成涉及外部系统中多个步骤或大量信息的复杂任务，并与对话共享结果。</span><span class="sxs-lookup"><span data-stu-id="8901d-117">You want to complete a complex task involving multiple steps or lots of information in an external system, and share the results with a conversation.</span></span>|<span data-ttu-id="8901d-118">基于邮件创建跟踪系统中Teams Bug，将 bug 分配给 Bob，然后向对话线程发送包含 bug 详细信息的卡片。</span><span class="sxs-lookup"><span data-stu-id="8901d-118">Create a bug in your tracking system based on a Teams message, assign that bug to Bob, and send a card to the conversation thread with the bug's details.</span></span>|

## <a name="understand-how-messaging-extensions-work"></a><span data-ttu-id="8901d-119">了解邮件扩展如何工作</span><span class="sxs-lookup"><span data-stu-id="8901d-119">Understand how messaging extensions work</span></span>

<span data-ttu-id="8901d-120">消息扩展由您托管的 Web 服务和应用程序清单组成，它定义 Web 服务在 Microsoft Teams 客户端中的调用位置。</span><span class="sxs-lookup"><span data-stu-id="8901d-120">A messaging extension consists of a web service that you host and an app manifest, which defines where your web service is invoked from in the Microsoft Teams client.</span></span> <span data-ttu-id="8901d-121">Web 服务利用 Bot Framework 的消息架构和安全通信协议，因此你必须在 Bot Framework 中将 Web 服务注册为自动程序。</span><span class="sxs-lookup"><span data-stu-id="8901d-121">The web service takes advantage of the Bot Framework's messaging schema and secure communication protocol, so you must register your web service as a bot in the Bot Framework.</span></span> 

> [!NOTE]
> <span data-ttu-id="8901d-122">虽然可以手动创建 Web 服务，但使用 [Bot Framework SDK](https://github.com/microsoft/botframework) 处理协议。</span><span class="sxs-lookup"><span data-stu-id="8901d-122">Though you can create the web service manually, use [Bot Framework SDK](https://github.com/microsoft/botframework) to work with the protocol.</span></span>

<span data-ttu-id="8901d-123">在应用程序的应用清单Microsoft Teams，使用最多十个不同的命令定义单个消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="8901d-123">In the app manifest for Microsoft Teams app, a single messaging extension is defined with up to ten different commands.</span></span> <span data-ttu-id="8901d-124">每个命令都定义一种类型，如操作或搜索以及客户端中调用它的位置。</span><span class="sxs-lookup"><span data-stu-id="8901d-124">Each command defines a type, such as action or search and the locations in the client from where it is invoked.</span></span> <span data-ttu-id="8901d-125">调用位置包括撰写邮件区域、命令栏和邮件。</span><span class="sxs-lookup"><span data-stu-id="8901d-125">The invoke locations are compose message area, command bar, and message.</span></span> <span data-ttu-id="8901d-126">在调用时，Web 服务会收到一条包含 JSON 有效负载的 HTTPS 消息，其中包括所有相关信息。</span><span class="sxs-lookup"><span data-stu-id="8901d-126">On invoke, the web service receives an HTTPS message with a JSON payload including all the relevant information.</span></span> <span data-ttu-id="8901d-127">使用 JSON 有效负载进行响应，Teams客户端知道要启用的下一次交互。</span><span class="sxs-lookup"><span data-stu-id="8901d-127">Respond with a JSON payload, allowing the Teams client to know the next interaction to enable.</span></span> 

## <a name="types-of-messaging-extension-commands"></a><span data-ttu-id="8901d-128">邮件扩展命令的类型</span><span class="sxs-lookup"><span data-stu-id="8901d-128">Types of messaging extension commands</span></span>

<span data-ttu-id="8901d-129">邮件扩展命令有两种类型：操作命令和搜索命令。</span><span class="sxs-lookup"><span data-stu-id="8901d-129">There are two types of messaging extension commands, action command and search command.</span></span> <span data-ttu-id="8901d-130">消息扩展命令类型定义可用于 Web 服务的 UI 元素和交互流。</span><span class="sxs-lookup"><span data-stu-id="8901d-130">The messaging extension command type defines the UI elements and interaction flows available to your web service.</span></span> <span data-ttu-id="8901d-131">某些交互（如身份验证和配置）可用于两种类型的命令。</span><span class="sxs-lookup"><span data-stu-id="8901d-131">Some interactions, such as authentication and configuration are available for both types of commands.</span></span>

### <a name="action-commands"></a><span data-ttu-id="8901d-132">操作命令</span><span class="sxs-lookup"><span data-stu-id="8901d-132">Action commands</span></span>

<span data-ttu-id="8901d-133">操作命令用于向用户显示用于收集或显示信息的模式弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="8901d-133">Action commands are used to present the users with a modal popup to collect or display information.</span></span> <span data-ttu-id="8901d-134">当用户提交表单时，Web 服务会通过直接将邮件插入对话或将邮件插入撰写邮件区域来做出响应。</span><span class="sxs-lookup"><span data-stu-id="8901d-134">When the user submits the form, your web service responds by inserting a message into the conversation directly or by inserting a message into the compose message area.</span></span> <span data-ttu-id="8901d-135">之后，用户可以提交邮件。</span><span class="sxs-lookup"><span data-stu-id="8901d-135">After that the user can submit the message.</span></span> <span data-ttu-id="8901d-136">可以将多个表单链接在一起，以使用更复杂的工作流。</span><span class="sxs-lookup"><span data-stu-id="8901d-136">You can chain multiple forms together for more complex workflows.</span></span>

<span data-ttu-id="8901d-137">操作命令从撰写邮件区域、命令框或邮件中触发。</span><span class="sxs-lookup"><span data-stu-id="8901d-137">The action commands are triggered from the compose message area, the command box, or from a message.</span></span> <span data-ttu-id="8901d-138">从邮件调用命令时，发送到机器人的初始 JSON 有效负载包括从其中调用它的整个消息。</span><span class="sxs-lookup"><span data-stu-id="8901d-138">When the command is invoked from a message, the initial JSON payload sent to your bot includes the entire message it was invoked from.</span></span> <span data-ttu-id="8901d-139">下图显示了邮件扩展操作命令任务模块 ![ ：邮件扩展操作命令任务模块](~/assets/images/task-module.png)</span><span class="sxs-lookup"><span data-stu-id="8901d-139">The following image displays the messaging extension action command task module: ![messaging extension action command task module](~/assets/images/task-module.png)</span></span>

### <a name="search-commands"></a><span data-ttu-id="8901d-140">搜索命令</span><span class="sxs-lookup"><span data-stu-id="8901d-140">Search commands</span></span>

<span data-ttu-id="8901d-141">搜索命令允许用户通过搜索框手动搜索外部系统的信息，或者将受监视域的链接粘贴到撰写邮件区域，然后将搜索结果插入邮件中。</span><span class="sxs-lookup"><span data-stu-id="8901d-141">Search commands allow the users to search an external system for information either manually through a search box, or by pasting a link to a monitored domain into the compose message area, and insert the results of the search into a message.</span></span> <span data-ttu-id="8901d-142">在最基本的搜索命令流中，初始调用消息包括用户提交的搜索字符串。</span><span class="sxs-lookup"><span data-stu-id="8901d-142">In the most basic search command flow, the initial invoke message includes the search string that the user submitted.</span></span> <span data-ttu-id="8901d-143">使用卡片和卡片预览列表进行响应。</span><span class="sxs-lookup"><span data-stu-id="8901d-143">You respond with a list of cards and card previews.</span></span> <span data-ttu-id="8901d-144">客户端Teams为用户呈现卡片预览列表。</span><span class="sxs-lookup"><span data-stu-id="8901d-144">The Teams client renders a list of card previews for the user.</span></span> <span data-ttu-id="8901d-145">当用户从列表中选择卡片时，全尺寸卡片将插入到撰写邮件区域中。</span><span class="sxs-lookup"><span data-stu-id="8901d-145">When the user selects a card from the list, the full-size card is inserted into the compose message area.</span></span>

<span data-ttu-id="8901d-146">卡片从撰写邮件区域或命令框触发，不会从邮件中触发。</span><span class="sxs-lookup"><span data-stu-id="8901d-146">The cards are triggered from the compose message area or the command box and not triggered from a message.</span></span> <span data-ttu-id="8901d-147">无法从邮件中触发它们。</span><span class="sxs-lookup"><span data-stu-id="8901d-147">They can not be triggered from a message.</span></span>
<span data-ttu-id="8901d-148">下图显示了邮件扩展搜索命令任务模块：</span><span class="sxs-lookup"><span data-stu-id="8901d-148">The following image displays the messaging extension search command task module:</span></span>

![邮件扩展搜索命令](~/assets/images/search-extension.png)

> [!NOTE]
> <span data-ttu-id="8901d-150">有关卡片详细信息，请参阅 [什么是卡片](../task-modules-and-cards/what-are-cards.md)。</span><span class="sxs-lookup"><span data-stu-id="8901d-150">For more information on cards, see [what are cards](../task-modules-and-cards/what-are-cards.md).</span></span>

## <a name="link-unfurling"></a><span data-ttu-id="8901d-151">链接展开</span><span class="sxs-lookup"><span data-stu-id="8901d-151">Link unfurling</span></span>

<span data-ttu-id="8901d-152">在撰写邮件区域中粘贴 URL 时，将调用 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="8901d-152">A web service is invoked when a URL is pasted in the compose message area.</span></span> <span data-ttu-id="8901d-153">此功能称为链接取消点击。</span><span class="sxs-lookup"><span data-stu-id="8901d-153">This functionality is known as link unfurling.</span></span> <span data-ttu-id="8901d-154">当包含特定域的 URL 粘贴到撰写邮件区域中时，可以订阅接收调用。</span><span class="sxs-lookup"><span data-stu-id="8901d-154">You can subscribe to receive an invoke when URLs containing a particular domain are pasted into the compose message area.</span></span> <span data-ttu-id="8901d-155">Web 服务可以将 URL"取消展开"为详细卡片，提供比标准网站预览卡更多的信息。</span><span class="sxs-lookup"><span data-stu-id="8901d-155">Your web service can "unfurl" the URL into a detailed card, providing more information than the standard website preview card.</span></span> <span data-ttu-id="8901d-156">您可以添加按钮以允许用户立即采取措施，而无需离开 Microsoft Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="8901d-156">You can add buttons to allow the users to immediately take action without leaving the Microsoft Teams client.</span></span>
<span data-ttu-id="8901d-157">在邮件扩展中粘贴链接时，以下图像显示链接展开功能：</span><span class="sxs-lookup"><span data-stu-id="8901d-157">The following images display link unfurling feature when a link is pasted in messaging extension:</span></span>
 
![取消链接](../assets/images/messaging-extension/unfurl-link.png)

![链接取消点击](../assets/images/messaging-extension/link-unfurl.gif)

## <a name="code-sample"></a><span data-ttu-id="8901d-160">代码示例</span><span class="sxs-lookup"><span data-stu-id="8901d-160">Code sample</span></span>

| <span data-ttu-id="8901d-161">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="8901d-161">**Sample name**</span></span> | <span data-ttu-id="8901d-162">**说明**</span><span class="sxs-lookup"><span data-stu-id="8901d-162">**Description**</span></span> | <span data-ttu-id="8901d-163">**.NET**</span><span class="sxs-lookup"><span data-stu-id="8901d-163">**.NET**</span></span> | <span data-ttu-id="8901d-164">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="8901d-164">**Node.js**</span></span> | <span data-ttu-id="8901d-165">**Python**</span><span class="sxs-lookup"><span data-stu-id="8901d-165">**Python**</span></span> |
|------------|-------------|----------------|------------|
| <span data-ttu-id="8901d-166">使用基于操作的命令的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="8901d-166">Messaging extension with action-based commands</span></span> | <span data-ttu-id="8901d-167">此示例演示如何构建基于操作的邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="8901d-167">This sample illustrates how to build an action-based messaging extension.</span></span> | [<span data-ttu-id="8901d-168">View</span><span class="sxs-lookup"><span data-stu-id="8901d-168">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action) | [<span data-ttu-id="8901d-169">View</span><span class="sxs-lookup"><span data-stu-id="8901d-169">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | [<span data-ttu-id="8901d-170">View</span><span class="sxs-lookup"><span data-stu-id="8901d-170">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/51.teams-messaging-extensions-action) |
| <span data-ttu-id="8901d-171">使用基于搜索的命令的邮件扩展</span><span class="sxs-lookup"><span data-stu-id="8901d-171">Messaging extension with search-based commands</span></span> | <span data-ttu-id="8901d-172">此示例演示如何构建基于搜索的消息扩展。</span><span class="sxs-lookup"><span data-stu-id="8901d-172">This sample illustrates how to build a Search-based Messaging Extension.</span></span> | [<span data-ttu-id="8901d-173">View</span><span class="sxs-lookup"><span data-stu-id="8901d-173">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search) | [<span data-ttu-id="8901d-174">View</span><span class="sxs-lookup"><span data-stu-id="8901d-174">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search) | [<span data-ttu-id="8901d-175">View</span><span class="sxs-lookup"><span data-stu-id="8901d-175">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## <a name="see-also"></a><span data-ttu-id="8901d-176">另请参阅</span><span class="sxs-lookup"><span data-stu-id="8901d-176">See also</span></span>

[<span data-ttu-id="8901d-177">创建邮件扩展</span><span class="sxs-lookup"><span data-stu-id="8901d-177">Create a messaging extension</span></span>](../build-your-first-app/build-messaging-extension.md)


## <a name="next-step"></a><span data-ttu-id="8901d-178">后续步骤</span><span class="sxs-lookup"><span data-stu-id="8901d-178">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8901d-179">定义操作消息传递扩展命令</span><span class="sxs-lookup"><span data-stu-id="8901d-179">Define action messaging extension command</span></span>](~/messaging-extensions/how-to/action-commands/define-action-command.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="8901d-180">定义搜索邮件扩展命令</span><span class="sxs-lookup"><span data-stu-id="8901d-180">Define search messaging extension command</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)
