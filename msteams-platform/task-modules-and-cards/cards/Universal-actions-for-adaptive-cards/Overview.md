---
title: 自适应卡片的通用操作概述
description: 自适应卡片的通用操作快速概述。
ms.topic: overview
localization_priority: Normal
ms.openlocfilehash: f0adf3d1a01262ff9cbdf14128c9ffe088ae8072
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088857"
---
# <a name="universal-actions-for-adaptive-cards"></a><span data-ttu-id="b4e25-103">自适应卡片的通用操作</span><span class="sxs-lookup"><span data-stu-id="b4e25-103">Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="b4e25-104">自适应卡片的通用操作从开发人员反馈中发展，尽管自适应卡片的布局和呈现是通用的，但操作处理不是。</span><span class="sxs-lookup"><span data-stu-id="b4e25-104">Universal Actions for Adaptive Cards evolved from developer feedback that even though layout and rendering for Adaptive Cards was universal, action handling was not.</span></span> <span data-ttu-id="b4e25-105">即使开发人员希望将同一张卡片发送到不同位置，他们必须处理不同的操作。</span><span class="sxs-lookup"><span data-stu-id="b4e25-105">Even if a developer wanted to send the same card to different places, they have to handle actions differently.</span></span>

<span data-ttu-id="b4e25-106">自适应卡片的通用操作将机器人作为处理操作的通用后端引入，并引入了新的操作类型，它适用于应用，如 Teams `Action.Execute` 和 Outlook。</span><span class="sxs-lookup"><span data-stu-id="b4e25-106">Universal Actions for Adaptive Cards brings the bot as the common backend for handling actions and introduces a new action type, `Action.Execute`, which works across apps, such as Teams and Outlook.</span></span>

<span data-ttu-id="b4e25-107">本文档可帮助你了解如何使用通用操作模型增强跨平台和应用程序与自适应卡片交互的用户体验。</span><span class="sxs-lookup"><span data-stu-id="b4e25-107">This document helps you to understand how you can use Universal Actions model to enhance user experience of interacting with Adaptive Cards across platforms and applications.</span></span>

> [!NOTE]
> <span data-ttu-id="b4e25-108">仅对自动程序发送的卡片支持自适应卡片的通用操作。</span><span class="sxs-lookup"><span data-stu-id="b4e25-108">Support for Universal Actions for Adaptive Cards is only available for cards sent by bot.</span></span> <span data-ttu-id="b4e25-109">即将推出对通过撰写框和链接取消点击卡片发送的卡片的支持。</span><span class="sxs-lookup"><span data-stu-id="b4e25-109">Support for cards sent through compose box and link unfurling cards is coming soon.</span></span>

## <a name="enhance-user-experiences-with-universal-actions-for-adaptive-cards"></a><span data-ttu-id="b4e25-110">使用自适应卡片的通用操作增强用户体验</span><span class="sxs-lookup"><span data-stu-id="b4e25-110">Enhance user experiences with Universal Actions for Adaptive Cards</span></span>

<span data-ttu-id="b4e25-111">自适应卡片的通用操作通过启用以下方案来增强用户体验：</span><span class="sxs-lookup"><span data-stu-id="b4e25-111">Universal Actions for Adaptive Cards enhances user experience by enabling the following scenarios:</span></span>

* [<span data-ttu-id="b4e25-112">通用操作</span><span class="sxs-lookup"><span data-stu-id="b4e25-112">Universal Actions</span></span>](#universal-actions)
* [<span data-ttu-id="b4e25-113">特定于用户的视图</span><span class="sxs-lookup"><span data-stu-id="b4e25-113">User Specific Views</span></span>](#user-specific-views)
* [<span data-ttu-id="b4e25-114">顺序工作流支持</span><span class="sxs-lookup"><span data-stu-id="b4e25-114">Sequential Workflow support</span></span>](#sequential-workflow-support)
* [<span data-ttu-id="b4e25-115">最新视图</span><span class="sxs-lookup"><span data-stu-id="b4e25-115">Up to date views</span></span>](#up-to-date-views)

### <a name="universal-actions"></a><span data-ttu-id="b4e25-116">通用操作</span><span class="sxs-lookup"><span data-stu-id="b4e25-116">Universal Actions</span></span>

<span data-ttu-id="b4e25-117">在自适应卡片的通用操作之前，不同的主机提供不同的操作模型，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b4e25-117">Before the Universal Actions for Adaptive Cards, different hosts provided different action models as follows:</span></span>

* <span data-ttu-id="b4e25-118">Teams或聊天机器人，这是一种将实际 `Action.Submit` 通信模型延迟到基础通道的方法。</span><span class="sxs-lookup"><span data-stu-id="b4e25-118">Teams or bots used `Action.Submit`, an approach which defers the actual communication model to the underlying channel.</span></span>
* <span data-ttu-id="b4e25-119">Outlook与 `Action.Http` 自适应卡片有效负载中显式指定的后端服务通信。</span><span class="sxs-lookup"><span data-stu-id="b4e25-119">Outlook used `Action.Http` to communicate with the backend service explicitly specified in the Adaptive Card payload.</span></span>

<span data-ttu-id="b4e25-120">下图显示了当前不一致的操作模型：</span><span class="sxs-lookup"><span data-stu-id="b4e25-120">The following image shows the current inconsistent action model:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/current-teams-outlook-action-model.png" alt-text="不一致的操作模型":::

<span data-ttu-id="b4e25-122">借助自适应卡片的通用操作，可用于 `Action.Execute` 跨不同平台的操作处理。</span><span class="sxs-lookup"><span data-stu-id="b4e25-122">With the Universal Actions for Adaptive Cards, you can use `Action.Execute` for action handling across different platforms.</span></span> <span data-ttu-id="b4e25-123">`Action.Execute`适用于中心，包括Teams Outlook。</span><span class="sxs-lookup"><span data-stu-id="b4e25-123">`Action.Execute` works across hubs including Teams and Outlook.</span></span> <span data-ttu-id="b4e25-124">此外，自适应卡片还可以作为触发的调用 `Action.Execute` 请求的响应返回。</span><span class="sxs-lookup"><span data-stu-id="b4e25-124">In addition, an Adaptive Card can be returned as response for an `Action.Execute` triggered invoke request.</span></span>

<span data-ttu-id="b4e25-125">下图显示了新的通用操作模型：</span><span class="sxs-lookup"><span data-stu-id="b4e25-125">The following image shows the new Universal Action model:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-action-model.png" alt-text="自适应卡片的新通用操作":::

<span data-ttu-id="b4e25-127">现在，你可以向两者发送相同的Teams和Outlook，然后使用基础自动程序保持它们相互同步。</span><span class="sxs-lookup"><span data-stu-id="b4e25-127">You can now send the same card to both, Teams and Outlook, and keep them in sync with each other using the underlying bot.</span></span> <span data-ttu-id="b4e25-128">通过此内部版本，在任一平台上执行的任何操作都反映给另一个平台， (自适应卡片的通用操作) 模型。</span><span class="sxs-lookup"><span data-stu-id="b4e25-128">Any action taken on either platform is reflected to the other with this *build once, deploy anywhere* (Universal Actions for Adaptive Cards) model.</span></span>

<span data-ttu-id="b4e25-129">下图描述了适用于用户和用户的通用自适应卡片Teams Outlook：</span><span class="sxs-lookup"><span data-stu-id="b4e25-129">The following image depicts the Universal Actions for Adaptive Cards for both Teams and Outlook:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-teams-outlook.png" alt-text="与 Teams 和 Outlook":::

### <a name="user-specific-views"></a><span data-ttu-id="b4e25-131">特定于用户的视图</span><span class="sxs-lookup"><span data-stu-id="b4e25-131">User Specific Views</span></span>

<span data-ttu-id="b4e25-132">现在，聊天Teams频道中的每个用户都会在自适应卡片上看到完全相同的视图和按钮操作。</span><span class="sxs-lookup"><span data-stu-id="b4e25-132">Today every user in the Teams chat or channel sees the exact same view and button actions on the Adaptive Card.</span></span> <span data-ttu-id="b4e25-133">但是，在某些情况下，要求某些用户采取不同的行动，并有权访问同一聊天或频道中的不同信息。</span><span class="sxs-lookup"><span data-stu-id="b4e25-133">However, in certain scenarios there is a requirement for certain users to act differently and have access to different information within the same chat or channel.</span></span>

<span data-ttu-id="b4e25-134">例如，如果您在聊天或频道中发送事件报告卡，则只有分配了事件的用户才能看到"解决 **"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="b4e25-134">For example, if you send an incident reporting card in a chat or channel, only the user who is assigned the incident must see a **Resolve** button.</span></span> <span data-ttu-id="b4e25-135">另一方面，事件创建者必须看到"编辑"按钮，并且所有其他用户只能查看事件的详细信息。</span><span class="sxs-lookup"><span data-stu-id="b4e25-135">On the other hand, the incident creator must see an **Edit** button and all other users must only be able to view details of the incident.</span></span> <span data-ttu-id="b4e25-136">这是由 属性启用的用户特定视图 `refresh` 所实现。</span><span class="sxs-lookup"><span data-stu-id="b4e25-136">This is made possible by User Specific Views that is enabled by the `refresh` property.</span></span>

<span data-ttu-id="b4e25-137">下图显示了一个票证消息传递扩展 (ME) ，其中聊天中的不同用户根据要求显示了不同的操作：</span><span class="sxs-lookup"><span data-stu-id="b4e25-137">The following image shows an example of a ticketing messaging extension (ME) where different users in the chat are shown different actions based on the requirement:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-incident-management.png" alt-text="特定于用户的视图":::

<span data-ttu-id="b4e25-139">有关详细信息，请参阅用户 [特定视图的示例](User-Specific-Views.md)。</span><span class="sxs-lookup"><span data-stu-id="b4e25-139">For more information, see [sample for User Specific Views](User-Specific-Views.md).</span></span>

### <a name="sequential-workflow-support"></a><span data-ttu-id="b4e25-140">顺序工作流支持</span><span class="sxs-lookup"><span data-stu-id="b4e25-140">Sequential Workflow support</span></span>

<span data-ttu-id="b4e25-141">借助顺序工作流支持，用户可以执行一系列工作流，而无需单独发送不同的卡片。</span><span class="sxs-lookup"><span data-stu-id="b4e25-141">With Sequential Workflow support, users can progress through a series of workflows without sending different cards separately.</span></span> <span data-ttu-id="b4e25-142">这是通过返回自适应卡片以响应操作 `Action.Execute` 而实现。</span><span class="sxs-lookup"><span data-stu-id="b4e25-142">This is made possible by the ability of `Action.Execute` to return an Adaptive Card in response to an action.</span></span> <span data-ttu-id="b4e25-143">此外，聊天或频道中的任意用户都可以通过其工作流进行，而无需修改聊天中其他用户的卡片。</span><span class="sxs-lookup"><span data-stu-id="b4e25-143">Also, any user in the chat or channel can progress through their workflow without modifying the card for other users in the chat.</span></span>

<span data-ttu-id="b4e25-144">下图演示了一个食物订购机器人示例：</span><span class="sxs-lookup"><span data-stu-id="b4e25-144">The following image illustrates a food ordering bot example:</span></span> <br/>

<img src="~/assets/images/bots/sequentialWorkflow.gif" alt="Sequential Workflow" width="400"/>

<span data-ttu-id="b4e25-145">下图显示了聊天或频道中不同用户的不同状态：</span><span class="sxs-lookup"><span data-stu-id="b4e25-145">The following image shows the various states for different users in the chat or channel:</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-catering-bot.png" alt-text="适应机器人状态":::

<span data-ttu-id="b4e25-147">有关详细信息，请参阅顺序 [工作流的示例](Sequential-Workflows.md)。</span><span class="sxs-lookup"><span data-stu-id="b4e25-147">For more information, see [sample for Sequential Workflow](Sequential-Workflows.md).</span></span>

### <a name="up-to-date-views"></a><span data-ttu-id="b4e25-148">最新视图</span><span class="sxs-lookup"><span data-stu-id="b4e25-148">Up to date views</span></span>

<span data-ttu-id="b4e25-149">你可以创建自动更新的自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="b4e25-149">You can create Adaptive Cards that update automatically.</span></span> <span data-ttu-id="b4e25-150">例如，它可以是由用户发送的审批请求。</span><span class="sxs-lookup"><span data-stu-id="b4e25-150">For example, it can be an approval request sent by a user.</span></span> <span data-ttu-id="b4e25-151">审批后，该卡片必须自动显示有关请求审批时间和批准请求者的详细信息。</span><span class="sxs-lookup"><span data-stu-id="b4e25-151">After approval, the card must automatically display details about the request approval time and who approved the request.</span></span> <span data-ttu-id="b4e25-152">刷新模型使您能够提供此类最新视图。</span><span class="sxs-lookup"><span data-stu-id="b4e25-152">The refresh model enables you to provide such up to date views.</span></span> <span data-ttu-id="b4e25-153">下图显示了多步骤审批流以及如何显示不同用户的视图。</span><span class="sxs-lookup"><span data-stu-id="b4e25-153">The following image shows a multi-step approval flow and how the views for different users is shown.</span></span>

:::image type="content" source="~/assets/images/adaptive-cards/universal-bots-up-to-date-views.png" alt-text="最新用户特定视图":::

<span data-ttu-id="b4e25-155">有关详细信息，请参阅 [最新视图的示例](Up-To-Date-Views.md)。</span><span class="sxs-lookup"><span data-stu-id="b4e25-155">For more information, see [sample for up to date views](Up-To-Date-Views.md).</span></span>

<span data-ttu-id="b4e25-156">现在，你可以了解如何使用新的通用操作模型转换自适应卡片，以提供独特且增强的用户体验。</span><span class="sxs-lookup"><span data-stu-id="b4e25-156">Now, you can understand how Adaptive Cards can be transformed with the new Universal Actions model to provide a unique and enhanced user experience.</span></span>

## <a name="adaptive-cards-and-the-new-universal-actions-model"></a><span data-ttu-id="b4e25-157">自适应卡片和新的通用操作模型</span><span class="sxs-lookup"><span data-stu-id="b4e25-157">Adaptive Cards and the new Universal Actions model</span></span>

<span data-ttu-id="b4e25-158">自适应卡片是内容（如文本和图形）以及用户可以执行的操作的组合。</span><span class="sxs-lookup"><span data-stu-id="b4e25-158">Adaptive Cards are a combination of content, such as text and graphics, and actions that can be performed by a user.</span></span> <span data-ttu-id="b4e25-159">有关详细信息，请参阅自适应 [卡片](http://adaptivecards.io/)。</span><span class="sxs-lookup"><span data-stu-id="b4e25-159">For more information, see [Adaptive Cards](http://adaptivecards.io/).</span></span> <span data-ttu-id="b4e25-160">自适应卡片的新通用操作支持跨平台和应用程序常见处理自适应卡片操作。</span><span class="sxs-lookup"><span data-stu-id="b4e25-160">The new Universal Actions for Adaptive Cards enables a common handling of the Adaptive Card actions across platforms and applications.</span></span> <span data-ttu-id="b4e25-161">有关详细信息，请参阅通用 [操作模型](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model)。</span><span class="sxs-lookup"><span data-stu-id="b4e25-161">For more information, see [Universal Action Model](https://docs.microsoft.com/adaptive-cards/authoring-cards/universal-action-model).</span></span>

<span data-ttu-id="b4e25-162">[使用适用于自适应卡片的通用操作](Work-with-universal-actions-for-adaptive-cards.md) 文档将介绍为解决方案使用通用操作自适应卡片功能的步骤。</span><span class="sxs-lookup"><span data-stu-id="b4e25-162">[Work with Universal Actions for Adaptive Cards](Work-with-universal-actions-for-adaptive-cards.md) document takes you through the steps to use the capabilities of Universal Actions for Adaptive Cards for your solution.</span></span>

## <a name="see-also"></a><span data-ttu-id="b4e25-163">另请参阅</span><span class="sxs-lookup"><span data-stu-id="b4e25-163">See also</span></span>

* [<span data-ttu-id="b4e25-164">什么是自动程序</span><span class="sxs-lookup"><span data-stu-id="b4e25-164">What are bots</span></span>](~/bots/what-are-bots.md)
* [<span data-ttu-id="b4e25-165">自适应卡片概述</span><span class="sxs-lookup"><span data-stu-id="b4e25-165">Adaptive Cards overview</span></span>](~/task-modules-and-cards/what-are-cards.md)
* [<span data-ttu-id="b4e25-166">自适应卡片 @ Microsoft Build 2020</span><span class="sxs-lookup"><span data-stu-id="b4e25-166">Adaptive Cards @ Microsoft Build 2020</span></span>](https://youtu.be/hEBhwB72Qn4?t=1393)
* [<span data-ttu-id="b4e25-167">Adaptive Cards @ Ignite 2020</span><span class="sxs-lookup"><span data-stu-id="b4e25-167">Adaptive Cards @ Ignite 2020</span></span>](https://techcommunity.microsoft.com/t5/video-hub/elevate-user-experiences-with-teams-and-adaptive-cards/m-p/1689460)

## <a name="next-step"></a><span data-ttu-id="b4e25-168">后续步骤</span><span class="sxs-lookup"><span data-stu-id="b4e25-168">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="b4e25-169">使用自适应卡片的通用操作</span><span class="sxs-lookup"><span data-stu-id="b4e25-169">Work with Universal Actions for Adaptive Cards</span></span>](Work-with-universal-actions-for-adaptive-cards.md)
