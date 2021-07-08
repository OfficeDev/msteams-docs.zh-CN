---
title: 卡片类型
description: 介绍自动程序可用的所有卡片和Teams
localization_priority: Normal
keywords: 机器人卡参考
ms.topic: reference
ms.openlocfilehash: d3b84344eccee7c2595b0e978c72d7e331b198cb
ms.sourcegitcommit: b1f9162a0bbcd276064ae9e4f1e8bccc06cb7035
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2021
ms.locfileid: "53328070"
---
# <a name="types-of-cards"></a><span data-ttu-id="0d37f-104">卡片类型</span><span class="sxs-lookup"><span data-stu-id="0d37f-104">Types of cards</span></span>

<span data-ttu-id="0d37f-105">自动程序支持自适应、Office 365、列表、Office 365 连接器、收据、登录以及缩略图卡和卡片Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="0d37f-105">Adaptive, hero, list, Office 365 Connector, receipt, signin, and thumbnail cards and card collections are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="0d37f-106">它们基于 Bot Framework 定义的卡，Teams不支持所有 Bot Framework 卡，并添加了一些自己的卡。</span><span class="sxs-lookup"><span data-stu-id="0d37f-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span>

<span data-ttu-id="0d37f-107">确定不同的卡片类型之前，请了解如何创建 Hero 卡片、缩略图卡片或自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="0d37f-107">Before you identify the different card types, understand how to create a a hero card, thumbnail card, or Adaptive Card.</span></span>

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a><span data-ttu-id="0d37f-108">创建 Hero 卡片、缩略图卡或自适应卡片</span><span class="sxs-lookup"><span data-stu-id="0d37f-108">Create a hero card, thumbnail card, or Adaptive Card</span></span>

<span data-ttu-id="0d37f-109">**从 App Studio 创建 Hero 卡片、缩略图卡片或自适应卡片**</span><span class="sxs-lookup"><span data-stu-id="0d37f-109">**To create a hero card, thumbnail card, or Adaptive Card from App Studio**</span></span>

1. <span data-ttu-id="0d37f-110">从应用商店 **转到 App Studio** Teams。</span><span class="sxs-lookup"><span data-stu-id="0d37f-110">Go to **App Studio** from Teams.</span></span>
1. <span data-ttu-id="0d37f-111">选择 **"卡片编辑器"。**</span><span class="sxs-lookup"><span data-stu-id="0d37f-111">Select **Card editor**.</span></span>
1. <span data-ttu-id="0d37f-112">选择 **创建新卡片**。</span><span class="sxs-lookup"><span data-stu-id="0d37f-112">Select **Create a new card**.</span></span>
1. <span data-ttu-id="0d37f-113">从 **Hero Card、Thumbnail** **Card** 或 **Adaptive** Card 中选择其中一张卡片 **的"创建"。**</span><span class="sxs-lookup"><span data-stu-id="0d37f-113">Select **Create** for one of the cards from **Hero Card**, **Thumbnail Card**, or **Adaptive Card**.</span></span> <span data-ttu-id="0d37f-114">显示该卡片的元数据详细信息、按钮以及 json、csharp 和节点代码示例。</span><span class="sxs-lookup"><span data-stu-id="0d37f-114">The metadata details, buttons, and json, csharp, and node code examples are shown for that card.</span></span>

    ![Hero card details](~/assets/images/Cards/Herocarddetails.png)

1. <span data-ttu-id="0d37f-116">选择 **"向我发送此卡"。**</span><span class="sxs-lookup"><span data-stu-id="0d37f-116">Select **Send me this card**.</span></span> <span data-ttu-id="0d37f-117">该卡片作为聊天消息发送给您。</span><span class="sxs-lookup"><span data-stu-id="0d37f-117">The card is sent to you as a chat message.</span></span>

## <a name="card-examples"></a><span data-ttu-id="0d37f-118">卡片示例</span><span class="sxs-lookup"><span data-stu-id="0d37f-118">Card examples</span></span>

<span data-ttu-id="0d37f-119">有关如何使用卡的其他信息，请参阅 Bot Builder SDK v3 的文档。</span><span class="sxs-lookup"><span data-stu-id="0d37f-119">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="0d37f-120">代码示例也可在 **Microsoft/BotBuilder-Samples** 存储库上GitHub。</span><span class="sxs-lookup"><span data-stu-id="0d37f-120">Code samples are also available in the **Microsoft/BotBuilder-Samples** repository on GitHub.</span></span> <span data-ttu-id="0d37f-121">以下是一些卡片示例：</span><span class="sxs-lookup"><span data-stu-id="0d37f-121">Following are a few card examples:</span></span>

* <span data-ttu-id="0d37f-122">.NET</span><span class="sxs-lookup"><span data-stu-id="0d37f-122">.NET</span></span>
  * <span data-ttu-id="0d37f-123">[将卡片添加为邮件的附件](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="0d37f-123">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="0d37f-124">[卡片示例代码自动程序生成器 v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards)。</span><span class="sxs-lookup"><span data-stu-id="0d37f-124">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="0d37f-125">Node.js</span><span class="sxs-lookup"><span data-stu-id="0d37f-125">Node.js</span></span>
  * <span data-ttu-id="0d37f-126">[将卡片添加为邮件的附件](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="0d37f-126">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="0d37f-127">[卡片示例代码自动程序生成器 v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards)。</span><span class="sxs-lookup"><span data-stu-id="0d37f-127">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="card-types"></a><span data-ttu-id="0d37f-128">卡片类型</span><span class="sxs-lookup"><span data-stu-id="0d37f-128">Card types</span></span>

<span data-ttu-id="0d37f-129">你可以根据应用程序要求标识和使用不同类型的卡片。</span><span class="sxs-lookup"><span data-stu-id="0d37f-129">You can identify and use different types of cards based on your application requirements.</span></span> <span data-ttu-id="0d37f-130">下表显示了可供你使用卡片的类型：</span><span class="sxs-lookup"><span data-stu-id="0d37f-130">The following table shows the types of cards available to you:</span></span>

| <span data-ttu-id="0d37f-131">卡片类型</span><span class="sxs-lookup"><span data-stu-id="0d37f-131">Card type</span></span> | <span data-ttu-id="0d37f-132">说明</span><span class="sxs-lookup"><span data-stu-id="0d37f-132">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="0d37f-133">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="0d37f-133">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="0d37f-134">此卡片可高度自定义，可以包含文本、语音、图像、按钮和输入字段的任意组合。</span><span class="sxs-lookup"><span data-stu-id="0d37f-134">This card is highly customizable and can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="0d37f-135">Hero card</span><span class="sxs-lookup"><span data-stu-id="0d37f-135">Hero card</span></span>](#hero-card) | <span data-ttu-id="0d37f-136">此卡片通常包含一个大图像、一个或多个按钮和少量文本。</span><span class="sxs-lookup"><span data-stu-id="0d37f-136">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="0d37f-137">列表卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-137">List card</span></span>](#list-card) | <span data-ttu-id="0d37f-138">此卡片包含项目的滚动列表。</span><span class="sxs-lookup"><span data-stu-id="0d37f-138">This card contains a scrolling list of items.</span></span> |
| [<span data-ttu-id="0d37f-139">Office 365连接器卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-139">Office 365 Connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="0d37f-140">此卡片具有具有多个分区、字段、图像和操作的灵活性布局。</span><span class="sxs-lookup"><span data-stu-id="0d37f-140">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="0d37f-141">收据卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-141">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="0d37f-142">此卡为用户提供收据。</span><span class="sxs-lookup"><span data-stu-id="0d37f-142">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="0d37f-143">登录卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-143">Signin card</span></span>](#signin-card) | <span data-ttu-id="0d37f-144">此卡使机器人可以请求用户登录。</span><span class="sxs-lookup"><span data-stu-id="0d37f-144">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="0d37f-145">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="0d37f-145">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="0d37f-146">此卡片通常包含一个缩略图图像、一些短文本以及一个或多个按钮。</span><span class="sxs-lookup"><span data-stu-id="0d37f-146">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="0d37f-147">卡片集合</span><span class="sxs-lookup"><span data-stu-id="0d37f-147">Card collections</span></span>](#card-collections) | <span data-ttu-id="0d37f-148">此卡片集合用于在单个响应中返回多个项目。</span><span class="sxs-lookup"><span data-stu-id="0d37f-148">This card collection is used to return multiple items in a single response.</span></span> |

## <a name="features-that-support-different-card-types"></a><span data-ttu-id="0d37f-149">支持不同卡片类型的功能</span><span class="sxs-lookup"><span data-stu-id="0d37f-149">Features that support different card types</span></span>

| <span data-ttu-id="0d37f-150">卡片类型</span><span class="sxs-lookup"><span data-stu-id="0d37f-150">Card type</span></span> | <span data-ttu-id="0d37f-151">机器人</span><span class="sxs-lookup"><span data-stu-id="0d37f-151">Bots</span></span> | <span data-ttu-id="0d37f-152">邮件扩展预览</span><span class="sxs-lookup"><span data-stu-id="0d37f-152">Message extension previews</span></span> | <span data-ttu-id="0d37f-153">邮件扩展结果</span><span class="sxs-lookup"><span data-stu-id="0d37f-153">Message extension results</span></span> | <span data-ttu-id="0d37f-154">任务模块</span><span class="sxs-lookup"><span data-stu-id="0d37f-154">Task modules</span></span> | <span data-ttu-id="0d37f-155">传出 Webhook</span><span class="sxs-lookup"><span data-stu-id="0d37f-155">Outgoing Webhooks</span></span> | <span data-ttu-id="0d37f-156">传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="0d37f-156">Incoming Webhooks</span></span> | <span data-ttu-id="0d37f-157">O365 连接器</span><span class="sxs-lookup"><span data-stu-id="0d37f-157">O365 Connectors</span></span> |
| --- | --- | --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="0d37f-158">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="0d37f-158">Adaptive Card</span></span> | <span data-ttu-id="0d37f-159">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-159">✔</span></span> | <span data-ttu-id="0d37f-160">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-160">✖</span></span> | <span data-ttu-id="0d37f-161">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-161">✔</span></span> | <span data-ttu-id="0d37f-162">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-162">✔</span></span> | <span data-ttu-id="0d37f-163">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-163">✔</span></span> | <span data-ttu-id="0d37f-164">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-164">✔</span></span> | <span data-ttu-id="0d37f-165">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-165">✖</span></span> |
| <span data-ttu-id="0d37f-166">O365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-166">O365 Connector card</span></span> | <span data-ttu-id="0d37f-167">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-167">✔</span></span> | <span data-ttu-id="0d37f-168">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-168">✖</span></span> | <span data-ttu-id="0d37f-169">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-169">✔</span></span> | <span data-ttu-id="0d37f-170">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-170">✖</span></span> | <span data-ttu-id="0d37f-171">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-171">✔</span></span> | <span data-ttu-id="0d37f-172">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-172">✔</span></span> | <span data-ttu-id="0d37f-173">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-173">✔</span></span> |
| <span data-ttu-id="0d37f-174">Hero card</span><span class="sxs-lookup"><span data-stu-id="0d37f-174">Hero card</span></span> | <span data-ttu-id="0d37f-175">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-175">✔</span></span> | <span data-ttu-id="0d37f-176">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-176">✔</span></span> | <span data-ttu-id="0d37f-177">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-177">✔</span></span> | <span data-ttu-id="0d37f-178">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-178">✖</span></span> | <span data-ttu-id="0d37f-179">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-179">✔</span></span> | <span data-ttu-id="0d37f-180">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-180">✔</span></span> | <span data-ttu-id="0d37f-181">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-181">✖</span></span> |
| <span data-ttu-id="0d37f-182">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="0d37f-182">Thumbnail card</span></span> | <span data-ttu-id="0d37f-183">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-183">✔</span></span> | <span data-ttu-id="0d37f-184">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-184">✔</span></span> | <span data-ttu-id="0d37f-185">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-185">✔</span></span> | <span data-ttu-id="0d37f-186">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-186">✖</span></span> | <span data-ttu-id="0d37f-187">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-187">✔</span></span> | <span data-ttu-id="0d37f-188">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-188">✔</span></span> | <span data-ttu-id="0d37f-189">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-189">✖</span></span> |
| <span data-ttu-id="0d37f-190">列表卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-190">List card</span></span> | <span data-ttu-id="0d37f-191">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-191">✔</span></span> | <span data-ttu-id="0d37f-192">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-192">✖</span></span> | <span data-ttu-id="0d37f-193">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-193">✖</span></span> | <span data-ttu-id="0d37f-194">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-194">✖</span></span> | <span data-ttu-id="0d37f-195">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-195">✔</span></span> | <span data-ttu-id="0d37f-196">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-196">✔</span></span> | <span data-ttu-id="0d37f-197">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-197">✖</span></span> |
| <span data-ttu-id="0d37f-198">收据卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-198">Receipt card</span></span> | <span data-ttu-id="0d37f-199">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-199">✔</span></span> | <span data-ttu-id="0d37f-200">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-200">✖</span></span> | <span data-ttu-id="0d37f-201">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-201">✖</span></span> | <span data-ttu-id="0d37f-202">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-202">✖</span></span> | <span data-ttu-id="0d37f-203">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-203">✖</span></span> | <span data-ttu-id="0d37f-204">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-204">✔</span></span> | <span data-ttu-id="0d37f-205">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-205">✖</span></span> |
| <span data-ttu-id="0d37f-206">登录卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-206">Signin card</span></span> | <span data-ttu-id="0d37f-207">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-207">✔</span></span> | <span data-ttu-id="0d37f-208">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-208">✖</span></span> | <span data-ttu-id="0d37f-209">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-209">✖</span></span> | <span data-ttu-id="0d37f-210">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-210">✖</span></span> | <span data-ttu-id="0d37f-211">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-211">✖</span></span> | <span data-ttu-id="0d37f-212">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-212">✖</span></span> | <span data-ttu-id="0d37f-213">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-213">✖</span></span> |

> [!NOTE]
> <span data-ttu-id="0d37f-214">对于传入 Webhook 中的自适应卡片，完全支持除 以外的所有本机自适应 `Action.Submit` 卡片架构元素。</span><span class="sxs-lookup"><span data-stu-id="0d37f-214">For Adaptive Cards in Incoming Webhooks, all native Adaptive Card schema elements, except `Action.Submit`, are fully supported.</span></span> <span data-ttu-id="0d37f-215">支持的操作包括 Action.OpenURL、Action.ShowCard、Action.ToggleVisibility [**和Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)。 [](https://adaptivecards.io/explorer/Action.OpenUrl.html) [](https://adaptivecards.io/explorer/Action.ShowCard.html) [](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)</span><span class="sxs-lookup"><span data-stu-id="0d37f-215">The supported actions are [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html), [**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html), [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html), and [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute).</span></span>

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="0d37f-216">所有卡片的常见属性</span><span class="sxs-lookup"><span data-stu-id="0d37f-216">Common properties for all cards</span></span>

<span data-ttu-id="0d37f-217">你可以浏览一些适用于所有卡片的常见属性。</span><span class="sxs-lookup"><span data-stu-id="0d37f-217">You can go through some common properties that are applicable to all cards.</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="0d37f-218">内联卡片图像</span><span class="sxs-lookup"><span data-stu-id="0d37f-218">Inline card images</span></span>

<span data-ttu-id="0d37f-219">卡片可以包含内联图像，包括指向公开可用图像的链接。</span><span class="sxs-lookup"><span data-stu-id="0d37f-219">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="0d37f-220">出于性能目的，强烈建议你将映像托管在公用内容分发网络 (CDN) 。</span><span class="sxs-lookup"><span data-stu-id="0d37f-220">For performance purposes, it is highly recommended you host the image on a public Content Delivery Network (CDN).</span></span>

<span data-ttu-id="0d37f-221">图像的大小会向上或向下扩展，以保持覆盖图像区的纵横比。</span><span class="sxs-lookup"><span data-stu-id="0d37f-221">Images are scaled up or down in size to maintain the aspect ratio for covering the image area.</span></span> <span data-ttu-id="0d37f-222">然后从中心裁剪图像，以实现卡片的适当纵横比。</span><span class="sxs-lookup"><span data-stu-id="0d37f-222">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="0d37f-223">图像必须最多为 1024×1024 和 PNG、JPEG 或 GIF 格式。</span><span class="sxs-lookup"><span data-stu-id="0d37f-223">Images must be at most 1024×1024 and in PNG, JPEG, or GIF format.</span></span> <span data-ttu-id="0d37f-224">不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="0d37f-224">Animated GIF is not supported.</span></span>

<span data-ttu-id="0d37f-225">下表提供了内联卡片图像的属性：</span><span class="sxs-lookup"><span data-stu-id="0d37f-225">The following table provides the properties of inline card images:</span></span>

| <span data-ttu-id="0d37f-226">属性</span><span class="sxs-lookup"><span data-stu-id="0d37f-226">Property</span></span> | <span data-ttu-id="0d37f-227">类型</span><span class="sxs-lookup"><span data-stu-id="0d37f-227">Type</span></span>  | <span data-ttu-id="0d37f-228">说明</span><span class="sxs-lookup"><span data-stu-id="0d37f-228">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d37f-229">url</span><span class="sxs-lookup"><span data-stu-id="0d37f-229">url</span></span> | <span data-ttu-id="0d37f-230">URL</span><span class="sxs-lookup"><span data-stu-id="0d37f-230">URL</span></span> | <span data-ttu-id="0d37f-231">图像的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="0d37f-231">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="0d37f-232">alt</span><span class="sxs-lookup"><span data-stu-id="0d37f-232">alt</span></span> | <span data-ttu-id="0d37f-233">字符串</span><span class="sxs-lookup"><span data-stu-id="0d37f-233">String</span></span> | <span data-ttu-id="0d37f-234">图像的辅助说明。</span><span class="sxs-lookup"><span data-stu-id="0d37f-234">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="0d37f-235">如果卡片包含的图像 URL 在最终图像之前重定向，则不支持图像 URL 中的重定向。</span><span class="sxs-lookup"><span data-stu-id="0d37f-235">If a card includes an image URL that is redirected before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="0d37f-236">对于在公有云上共享的图像，会出现此情况。</span><span class="sxs-lookup"><span data-stu-id="0d37f-236">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="0d37f-237">按钮</span><span class="sxs-lookup"><span data-stu-id="0d37f-237">Buttons</span></span>

<span data-ttu-id="0d37f-238">按钮显示在卡片底部堆叠。</span><span class="sxs-lookup"><span data-stu-id="0d37f-238">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="0d37f-239">按钮文本始终位于单行，如果文本超过按钮宽度，则将被截断。</span><span class="sxs-lookup"><span data-stu-id="0d37f-239">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="0d37f-240">不会显示超过卡支持的最大数目的其他任何按钮。</span><span class="sxs-lookup"><span data-stu-id="0d37f-240">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="0d37f-241">有关详细信息，请参阅 [卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="0d37f-241">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="0d37f-242">卡片格式</span><span class="sxs-lookup"><span data-stu-id="0d37f-242">Card formatting</span></span>

<span data-ttu-id="0d37f-243">有关卡片中的文本格式设置详细信息，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="0d37f-243">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

<span data-ttu-id="0d37f-244">确定所有卡片的常见属性后，你现在可以使用自适应卡片，这可通过将可操作内容直接添加到你使用的应用来帮助你提高参与度和效率。</span><span class="sxs-lookup"><span data-stu-id="0d37f-244">After identifying the common properties for all cards, you can now work with Adaptive Cards, which help you increase engagement and efficiency by adding your actionable content directly into the apps you use.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="0d37f-245">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="0d37f-245">Adaptive Card</span></span>

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

<span data-ttu-id="0d37f-246">自适应卡片是可自定义的卡片，可以包含文本、语音、图像、按钮和输入字段的任意组合。</span><span class="sxs-lookup"><span data-stu-id="0d37f-246">An Adaptive Card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="0d37f-247">有关详细信息，请参阅自适应[卡片 v1.2.0。](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)</span><span class="sxs-lookup"><span data-stu-id="0d37f-247">For more information, see [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="0d37f-248">自适应卡片支持</span><span class="sxs-lookup"><span data-stu-id="0d37f-248">Support for Adaptive Cards</span></span>

<span data-ttu-id="0d37f-249">下表提供支持自适应卡片的功能：</span><span class="sxs-lookup"><span data-stu-id="0d37f-249">The following table provides the features that support Adaptive Cards:</span></span>

| <span data-ttu-id="0d37f-250">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="0d37f-250">Bots in Teams</span></span> | <span data-ttu-id="0d37f-251">消息扩展</span><span class="sxs-lookup"><span data-stu-id="0d37f-251">Messaging extensions</span></span>  | <span data-ttu-id="0d37f-252">连接器</span><span class="sxs-lookup"><span data-stu-id="0d37f-252">Connectors</span></span> | <span data-ttu-id="0d37f-253">机器人框架</span><span class="sxs-lookup"><span data-stu-id="0d37f-253">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d37f-254">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-254">✔</span></span> | <span data-ttu-id="0d37f-255">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-255">✔</span></span> | <span data-ttu-id="0d37f-256">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-256">✖</span></span> | <span data-ttu-id="0d37f-257">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-257">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="0d37f-258">Teams平台支持 v1.2 或更早的自适应卡片功能。</span><span class="sxs-lookup"><span data-stu-id="0d37f-258">Teams platform supports v1.2 or earlier of Adaptive Card features.</span></span>
> * <span data-ttu-id="0d37f-259">在游戏平台上的自适应卡片中不支持正面或破坏性Teams样式。</span><span class="sxs-lookup"><span data-stu-id="0d37f-259">Positive or destructive action styling is not supported in Adaptive Cards on the Teams platform.</span></span>
> * <span data-ttu-id="0d37f-260">媒体元素当前在应用平台上的自适应卡片Teams支持。</span><span class="sxs-lookup"><span data-stu-id="0d37f-260">Media elements are currently not supported in Adaptive Card on the Teams platform.</span></span>

### <a name="example-of-adaptive-card"></a><span data-ttu-id="0d37f-261">自适应卡片示例</span><span class="sxs-lookup"><span data-stu-id="0d37f-261">Example of Adaptive Card</span></span>

![自适应卡片示例](~/assets/images/cards/adaptivecard.png)

<span data-ttu-id="0d37f-263">以下代码显示了自适应卡片的示例：</span><span class="sxs-lookup"><span data-stu-id="0d37f-263">The following code shows an example of an Adaptive Card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
      {
        "type": "Container",
        "items": [
          {
            "type": "TextBlock",
            "text": "Publish Adaptive Card schema",
            "weight": "bolder",
            "size": "medium"
          },
          {
            "type": "ColumnSet",
            "columns": [
              {
                "type": "Column",
                "width": "auto",
                "items": [
                  {
                    "type": "Image",
                    "url": "https://pbs.twimg.com/profile_images/3647943215/d7f12830b3c17a5a9e4afcc370e3a37e_400x400.jpeg",
                    "size": "small",
                    "style": "person"
                  }
                ]
              },
              {
                "type": "Column",
                "width": "stretch",
                "items": [
                  {
                    "type": "TextBlock",
                    "text": "Matt Hidinger",
                    "weight": "bolder",
                    "wrap": true
                  },
                  {
                    "type": "TextBlock",
                    "spacing": "none",
                    "text": "Created {{DATE(2017-02-14T06:08:39Z, SHORT)}}",
                    "isSubtle": true,
                    "wrap": true
                  }
                ]
              }
            ]
          }
        ]
      },
      {
        "type": "Container",
        "items": [
          {
            "type": "TextBlock",
            "text": "Now that we have defined the main rules and features of the format, we need to produce a schema and publish it to GitHub. The schema will be the starting point of our reference documentation.",
            "wrap": true
          },
          {
            "type": "FactSet",
            "facts": [
              {
                "title": "Board:",
                "value": "Adaptive Card"
              },
              {
                "title": "List:",
                "value": "Backlog"
              },
              {
                "title": "Assigned to:",
                "value": "Matt Hidinger"
              },
              {
                "title": "Due date:",
                "value": "Not set"
              }
            ]
          }
        ]
      }
    ],
    "actions": [
      {
        "type": "Action.ShowCard",
        "title": "Set due date",
        "card": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Input.Date",
              "id": "dueDate"
            }
          ],
          "actions": [
            {
              "type": "Action.Submit",
              "title": "OK"
            }
          ]
        }
      },
      {
        "type": "Action.ShowCard",
        "title": "Comment",
        "card": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Input.Text",
              "id": "comment",
              "isMultiline": true,
              "placeholder": "Enter your comment"
            }
          ],
          "actions": [
            {
              "type": "Action.Submit",
              "title": "OK"
            }
          ]
        }
      }
    ]
  }  
}
```

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="0d37f-264">自适应卡片的其他信息</span><span class="sxs-lookup"><span data-stu-id="0d37f-264">Additional information on Adaptive Cards</span></span>

<span data-ttu-id="0d37f-265">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="0d37f-265">Bot Framework reference:</span></span>

* [<span data-ttu-id="0d37f-266">自适应卡片节点</span><span class="sxs-lookup"><span data-stu-id="0d37f-266">Adaptive Cards Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="0d37f-267">自适应卡片 C#</span><span class="sxs-lookup"><span data-stu-id="0d37f-267">Adaptive Card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

<span data-ttu-id="0d37f-268">你现在可以使用一张 hero card，这是一种用于直观突出显示潜在用户选择的多用途卡片。</span><span class="sxs-lookup"><span data-stu-id="0d37f-268">You can now work with a hero card, which is a multipurpose card used to visually highlight a potential user selection.</span></span>

## <a name="hero-card"></a><span data-ttu-id="0d37f-269">Hero card</span><span class="sxs-lookup"><span data-stu-id="0d37f-269">Hero card</span></span>

<span data-ttu-id="0d37f-270">通常包含单个大图像、一个或多个按钮和文本的卡片。</span><span class="sxs-lookup"><span data-stu-id="0d37f-270">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="0d37f-271">支持人物卡片</span><span class="sxs-lookup"><span data-stu-id="0d37f-271">Support for hero cards</span></span>

<span data-ttu-id="0d37f-272">下表提供了支持人物卡片的功能：</span><span class="sxs-lookup"><span data-stu-id="0d37f-272">The following table provides the features that support hero cards:</span></span>

| <span data-ttu-id="0d37f-273">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="0d37f-273">Bots in Teams</span></span> | <span data-ttu-id="0d37f-274">消息扩展</span><span class="sxs-lookup"><span data-stu-id="0d37f-274">Messaging extensions</span></span>  | <span data-ttu-id="0d37f-275">连接器</span><span class="sxs-lookup"><span data-stu-id="0d37f-275">Connectors</span></span> | <span data-ttu-id="0d37f-276">机器人框架</span><span class="sxs-lookup"><span data-stu-id="0d37f-276">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d37f-277">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-277">✔</span></span> | <span data-ttu-id="0d37f-278">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-278">✔</span></span> | <span data-ttu-id="0d37f-279">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-279">✖</span></span> | <span data-ttu-id="0d37f-280">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-280">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="0d37f-281">Hero 卡片的属性</span><span class="sxs-lookup"><span data-stu-id="0d37f-281">Properties of a hero card</span></span>

<span data-ttu-id="0d37f-282">下表提供 Hero 卡片的属性：</span><span class="sxs-lookup"><span data-stu-id="0d37f-282">The following table provides the properties of a hero card:</span></span>

| <span data-ttu-id="0d37f-283">属性</span><span class="sxs-lookup"><span data-stu-id="0d37f-283">Property</span></span> | <span data-ttu-id="0d37f-284">类型</span><span class="sxs-lookup"><span data-stu-id="0d37f-284">Type</span></span>  | <span data-ttu-id="0d37f-285">说明</span><span class="sxs-lookup"><span data-stu-id="0d37f-285">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d37f-286">title</span><span class="sxs-lookup"><span data-stu-id="0d37f-286">title</span></span> | <span data-ttu-id="0d37f-287">格式文本 </span><span class="sxs-lookup"><span data-stu-id="0d37f-287">Rich text</span></span> | <span data-ttu-id="0d37f-288">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="0d37f-288">Title of the card.</span></span> <span data-ttu-id="0d37f-289">最多两行。</span><span class="sxs-lookup"><span data-stu-id="0d37f-289">Maximum two lines.</span></span> |
| <span data-ttu-id="0d37f-290">subtitle</span><span class="sxs-lookup"><span data-stu-id="0d37f-290">subtitle</span></span> | <span data-ttu-id="0d37f-291">格式文本 </span><span class="sxs-lookup"><span data-stu-id="0d37f-291">Rich text</span></span> | <span data-ttu-id="0d37f-292">卡片的副标题。</span><span class="sxs-lookup"><span data-stu-id="0d37f-292">Subtitle of the card.</span></span> <span data-ttu-id="0d37f-293">最多两行。</span><span class="sxs-lookup"><span data-stu-id="0d37f-293">Maximum two lines.</span></span>|
| <span data-ttu-id="0d37f-294">text</span><span class="sxs-lookup"><span data-stu-id="0d37f-294">text</span></span> | <span data-ttu-id="0d37f-295">格式文本 </span><span class="sxs-lookup"><span data-stu-id="0d37f-295">Rich text</span></span> | <span data-ttu-id="0d37f-296">文本显示在副标题下。</span><span class="sxs-lookup"><span data-stu-id="0d37f-296">Text appears under the subtitle.</span></span> <span data-ttu-id="0d37f-297">有关格式设置选项，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="0d37f-297">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="0d37f-298">images</span><span class="sxs-lookup"><span data-stu-id="0d37f-298">images</span></span> | <span data-ttu-id="0d37f-299">图像数组</span><span class="sxs-lookup"><span data-stu-id="0d37f-299">Array of images</span></span> | <span data-ttu-id="0d37f-300">显示在卡片顶部的图像。</span><span class="sxs-lookup"><span data-stu-id="0d37f-300">Image displayed at the top of the card.</span></span> <span data-ttu-id="0d37f-301">纵横比 16：9。</span><span class="sxs-lookup"><span data-stu-id="0d37f-301">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="0d37f-302">按钮</span><span class="sxs-lookup"><span data-stu-id="0d37f-302">buttons</span></span> | <span data-ttu-id="0d37f-303">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="0d37f-303">Array of action objects</span></span> | <span data-ttu-id="0d37f-304">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="0d37f-304">Set of actions applicable to the current card.</span></span> <span data-ttu-id="0d37f-305">最多六个。</span><span class="sxs-lookup"><span data-stu-id="0d37f-305">Maximum six.</span></span> |
| <span data-ttu-id="0d37f-306">点击</span><span class="sxs-lookup"><span data-stu-id="0d37f-306">tap</span></span> | <span data-ttu-id="0d37f-307">Action 对象</span><span class="sxs-lookup"><span data-stu-id="0d37f-307">Action object</span></span> | <span data-ttu-id="0d37f-308">当用户点击卡片本身时激活。</span><span class="sxs-lookup"><span data-stu-id="0d37f-308">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="0d37f-309">Hero 卡片示例</span><span class="sxs-lookup"><span data-stu-id="0d37f-309">Example of a hero card</span></span>

![Hero 卡片示例](~/assets/images/cards/hero.png)

<span data-ttu-id="0d37f-311">以下代码显示了一个展示卡片的示例：</span><span class="sxs-lookup"><span data-stu-id="0d37f-311">The following code shows an example of a hero card:</span></span>

```json
{
   "contentType": "application/vnd.microsoft.card.hero",
   "content": {
     "title": "Seattle Center Monorail",
     "subtitle": "Seattle Center Monorail",
     "text": "The Seattle Center Monorail is an elevated train line between Seattle Center (near the Space Needle) and downtown Seattle. It was built for the 1962 World's Fair. Its original two trains, completed in 1961, are still in service.",
     "images": [
       {
         "url":"https://upload.wikimedia.org/wikipedia/commons/thumb/4/49/Seattle_monorail01_2008-02-25.jpg/1024px-Seattle_monorail01_2008-02-25.jpg"
       }
     ],
    "buttons": [
      {
         "type": "openUrl",
         "title": "Official website",
         "value": "https://www.seattlemonorail.com"
       },
      {
        "type": "openUrl",
        "title": "Wikipeda page",
        "value": "https://en.wikipedia.org/wiki/Seattle_Center_Monorail"
       }
     ]
   }
}

```

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="0d37f-312">有关 hero cards 的其他信息</span><span class="sxs-lookup"><span data-stu-id="0d37f-312">Additional information on hero cards</span></span>

<span data-ttu-id="0d37f-313">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="0d37f-313">Bot Framework reference:</span></span>

* [<span data-ttu-id="0d37f-314">Hero card Node.js</span><span class="sxs-lookup"><span data-stu-id="0d37f-314">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="0d37f-315">Hero card C#</span><span class="sxs-lookup"><span data-stu-id="0d37f-315">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="0d37f-316">列表卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-316">List card</span></span>

<span data-ttu-id="0d37f-317">列表卡片已由列表Teams，以提供列表集合可以提供的功能之外的功能。</span><span class="sxs-lookup"><span data-stu-id="0d37f-317">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="0d37f-318">列表卡片提供项的滚动列表。</span><span class="sxs-lookup"><span data-stu-id="0d37f-318">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="0d37f-319">支持列表卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-319">Support for list cards</span></span>

<span data-ttu-id="0d37f-320">下表提供了支持列表卡片的功能：</span><span class="sxs-lookup"><span data-stu-id="0d37f-320">The following table provides the features that support list cards:</span></span>

| <span data-ttu-id="0d37f-321">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="0d37f-321">Bots in Teams</span></span> | <span data-ttu-id="0d37f-322">消息扩展</span><span class="sxs-lookup"><span data-stu-id="0d37f-322">Messaging extensions</span></span>  | <span data-ttu-id="0d37f-323">连接器</span><span class="sxs-lookup"><span data-stu-id="0d37f-323">Connectors</span></span> | <span data-ttu-id="0d37f-324">机器人框架</span><span class="sxs-lookup"><span data-stu-id="0d37f-324">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d37f-325">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-325">✔</span></span> | <span data-ttu-id="0d37f-326">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-326">✖</span></span> | <span data-ttu-id="0d37f-327">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-327">✖</span></span> |<span data-ttu-id="0d37f-328">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-328">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="0d37f-329">列表卡片的属性</span><span class="sxs-lookup"><span data-stu-id="0d37f-329">Properties of a list card</span></span>

<span data-ttu-id="0d37f-330">下表提供列表卡片的属性：</span><span class="sxs-lookup"><span data-stu-id="0d37f-330">The following table provides the properties of a list card:</span></span>

| <span data-ttu-id="0d37f-331">属性</span><span class="sxs-lookup"><span data-stu-id="0d37f-331">Property</span></span> | <span data-ttu-id="0d37f-332">类型</span><span class="sxs-lookup"><span data-stu-id="0d37f-332">Type</span></span>  | <span data-ttu-id="0d37f-333">说明</span><span class="sxs-lookup"><span data-stu-id="0d37f-333">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d37f-334">title</span><span class="sxs-lookup"><span data-stu-id="0d37f-334">title</span></span> | <span data-ttu-id="0d37f-335">格式文本 </span><span class="sxs-lookup"><span data-stu-id="0d37f-335">Rich text</span></span> | <span data-ttu-id="0d37f-336">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="0d37f-336">Title of the card.</span></span> <span data-ttu-id="0d37f-337">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="0d37f-337">Maximum 2 lines.</span></span>|
| <span data-ttu-id="0d37f-338">项目</span><span class="sxs-lookup"><span data-stu-id="0d37f-338">items</span></span> | <span data-ttu-id="0d37f-339">列表项数组</span><span class="sxs-lookup"><span data-stu-id="0d37f-339">Array of list items</span></span> | <span data-ttu-id="0d37f-340">适用于卡片的项目集。</span><span class="sxs-lookup"><span data-stu-id="0d37f-340">Set of items applicable to the card.</span></span>|
| <span data-ttu-id="0d37f-341">按钮</span><span class="sxs-lookup"><span data-stu-id="0d37f-341">buttons</span></span> | <span data-ttu-id="0d37f-342">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="0d37f-342">Array of action objects</span></span> | <span data-ttu-id="0d37f-343">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="0d37f-343">Set of actions applicable to the current card.</span></span> <span data-ttu-id="0d37f-344">最大值 6。</span><span class="sxs-lookup"><span data-stu-id="0d37f-344">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="0d37f-345">列表卡片示例</span><span class="sxs-lookup"><span data-stu-id="0d37f-345">Example of a list card</span></span>

<span data-ttu-id="0d37f-346">以下代码显示了列表卡片的示例：</span><span class="sxs-lookup"><span data-stu-id="0d37f-346">The following code shows an example of a list card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.teams.card.list",
  "content": {
    "title": "Card title",
    "items": [
      {
        "type": "file",
        "id": "https://contoso.sharepoint.com/teams/new/Shared%20Documents/Report.xlsx",
        "title": "Report",
        "subtitle": "teams > new > design",
        "tap": {
          "type": "imBack",
          "value": "editOnline https://contoso.sharepoint.com/teams/new/Shared%20Documents/Report.xlsx"
        }
      },
      {
        "type": "resultItem",
        "icon": "https://cdn2.iconfinder.com/data/icons/social-icons-33/128/Trello-128.png",
        "title": "Trello title",
        "subtitle": "A Trello subtitle",
        "tap": {
          "type": "openUrl",
          "value": "http://trello.com"
        }
      },
      {
        "type": "section",
        "title": "Manager"
      },
      {
        "type": "person",
        "id": "JohnDoe@contoso.com",
        "title": "John Doe",
        "subtitle": "Manager",
        "tap": {
          "type": "imBack",
          "value": "whois JohnDoe@contoso.com"
        }
      }
    ],
    "buttons": [
      {
        "type": "imBack",
        "title": "Select",
        "value": "whois"
      }
    ]
  }
}
```

## <a name="office-365-connector-card"></a><span data-ttu-id="0d37f-347">Office 365连接器卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-347">Office 365 connector card</span></span>

<span data-ttu-id="0d37f-348">可以使用提供灵活布局的 Office 365 连接器卡，这是获取有用信息的一种很好的方法。</span><span class="sxs-lookup"><span data-stu-id="0d37f-348">You can work with an Office 365 Connector card that provides a flexible layout and is a great way to get useful information.</span></span> <span data-ttu-id="0d37f-349">自动Office 365支持自动Teams，而不是 Bot Framework。</span><span class="sxs-lookup"><span data-stu-id="0d37f-349">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="0d37f-350">此卡片提供具有多个分区、字段、图像和操作的灵活性布局。</span><span class="sxs-lookup"><span data-stu-id="0d37f-350">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="0d37f-351">此卡包含连接器卡，以便机器人可以使用它。</span><span class="sxs-lookup"><span data-stu-id="0d37f-351">This card contains a connector card so that it can be used by bots.</span></span> <span data-ttu-id="0d37f-352">有关连接器卡和连接器Office 365卡之间的差异，请参阅连接器Office 365[卡上的其他信息](#additional-information-on-the-office-365-connector-card)。</span><span class="sxs-lookup"><span data-stu-id="0d37f-352">For differences between connector cards and the Office 365 Connector card, see [Additional information on the Office 365 Connector card](#additional-information-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="0d37f-353">支持 Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-353">Support for Office 365 Connector cards</span></span>

<span data-ttu-id="0d37f-354">下表提供了支持连接器Office 365的功能：</span><span class="sxs-lookup"><span data-stu-id="0d37f-354">The following table provides the features that support Office 365 Connector cards:</span></span>

| <span data-ttu-id="0d37f-355">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="0d37f-355">Bots in Teams</span></span> | <span data-ttu-id="0d37f-356">消息扩展</span><span class="sxs-lookup"><span data-stu-id="0d37f-356">Messaging extensions</span></span>  | <span data-ttu-id="0d37f-357">连接器</span><span class="sxs-lookup"><span data-stu-id="0d37f-357">Connectors</span></span> | <span data-ttu-id="0d37f-358">机器人框架</span><span class="sxs-lookup"><span data-stu-id="0d37f-358">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d37f-359">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-359">✔</span></span> | <span data-ttu-id="0d37f-360">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-360">✔</span></span> | <span data-ttu-id="0d37f-361">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-361">✔</span></span> | <span data-ttu-id="0d37f-362">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-362">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="0d37f-363">连接器Office 365的属性</span><span class="sxs-lookup"><span data-stu-id="0d37f-363">Properties of the Office 365 Connector card</span></span>

<span data-ttu-id="0d37f-364">下表提供了连接器卡Office 365属性：</span><span class="sxs-lookup"><span data-stu-id="0d37f-364">The following table provides the properties of the Office 365 connector card:</span></span>

| <span data-ttu-id="0d37f-365">属性</span><span class="sxs-lookup"><span data-stu-id="0d37f-365">Property</span></span> | <span data-ttu-id="0d37f-366">类型</span><span class="sxs-lookup"><span data-stu-id="0d37f-366">Type</span></span>  | <span data-ttu-id="0d37f-367">说明</span><span class="sxs-lookup"><span data-stu-id="0d37f-367">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d37f-368">title</span><span class="sxs-lookup"><span data-stu-id="0d37f-368">title</span></span> | <span data-ttu-id="0d37f-369">格式文本 </span><span class="sxs-lookup"><span data-stu-id="0d37f-369">Rich text</span></span> | <span data-ttu-id="0d37f-370">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="0d37f-370">Title of the card.</span></span> <span data-ttu-id="0d37f-371">最多两行。</span><span class="sxs-lookup"><span data-stu-id="0d37f-371">Maximum two lines.</span></span> |
| <span data-ttu-id="0d37f-372">摘要</span><span class="sxs-lookup"><span data-stu-id="0d37f-372">summary</span></span> | <span data-ttu-id="0d37f-373">格式文本 </span><span class="sxs-lookup"><span data-stu-id="0d37f-373">Rich text</span></span> | <span data-ttu-id="0d37f-374">卡片摘要。</span><span class="sxs-lookup"><span data-stu-id="0d37f-374">Summary of the card.</span></span> <span data-ttu-id="0d37f-375">最多两行。</span><span class="sxs-lookup"><span data-stu-id="0d37f-375">Maximum two lines.</span></span> |
| <span data-ttu-id="0d37f-376">text</span><span class="sxs-lookup"><span data-stu-id="0d37f-376">text</span></span> | <span data-ttu-id="0d37f-377">格式文本 </span><span class="sxs-lookup"><span data-stu-id="0d37f-377">Rich text</span></span> | <span data-ttu-id="0d37f-378">文本显示在副标题下。</span><span class="sxs-lookup"><span data-stu-id="0d37f-378">Text appears under the subtitle.</span></span> <span data-ttu-id="0d37f-379">有关格式设置选项，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="0d37f-379">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="0d37f-380">themeColor</span><span class="sxs-lookup"><span data-stu-id="0d37f-380">themeColor</span></span> | <span data-ttu-id="0d37f-381">十六进制字符串</span><span class="sxs-lookup"><span data-stu-id="0d37f-381">HEX string</span></span> | <span data-ttu-id="0d37f-382">替代应用程序清单 `accentColor` 中提供的颜色。</span><span class="sxs-lookup"><span data-stu-id="0d37f-382">Color that overrides the `accentColor` provided from the application manifest.</span></span> |

### <a name="additional-information-on-the-office-365-connector-card"></a><span data-ttu-id="0d37f-383">连接器卡上Office 365信息</span><span class="sxs-lookup"><span data-stu-id="0d37f-383">Additional information on the Office 365 Connector card</span></span>

<span data-ttu-id="0d37f-384">Office 365连接器卡在连接器Microsoft Teams，包括[ `ActionCard` 操作](/outlook/actionable-messages/card-reference#actioncard-action)。</span><span class="sxs-lookup"><span data-stu-id="0d37f-384">Office 365 Connector cards function properly in Microsoft Teams, including [`ActionCard` actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="0d37f-385">在机器人中从连接器使用连接器卡和使用连接器卡之间的重要区别是处理卡操作。</span><span class="sxs-lookup"><span data-stu-id="0d37f-385">The important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span> <span data-ttu-id="0d37f-386">下表列出了区别：</span><span class="sxs-lookup"><span data-stu-id="0d37f-386">The following table lists the difference:</span></span>

| <span data-ttu-id="0d37f-387">Connector</span><span class="sxs-lookup"><span data-stu-id="0d37f-387">Connector</span></span> | <span data-ttu-id="0d37f-388">Bot</span><span class="sxs-lookup"><span data-stu-id="0d37f-388">Bot</span></span> |
| --- | --- |
| <span data-ttu-id="0d37f-389">终结点通过 HTTP POST 接收卡有效负载。</span><span class="sxs-lookup"><span data-stu-id="0d37f-389">The endpoint receives the card payload through HTTP POST.</span></span> | <span data-ttu-id="0d37f-390">`HttpPOST`该操作将触发 `invoke` 仅向自动程序发送操作 ID 和正文的活动。</span><span class="sxs-lookup"><span data-stu-id="0d37f-390">The `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>|

<span data-ttu-id="0d37f-391">每个连接器卡最多可以显示 10 个部分，每个部分最多可以包含 5 个图像和 5 个操作。</span><span class="sxs-lookup"><span data-stu-id="0d37f-391">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="0d37f-392">邮件中不显示任何其他节、图像或操作。</span><span class="sxs-lookup"><span data-stu-id="0d37f-392">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="0d37f-393">所有文本字段都支持 Markdown 和 HTML。</span><span class="sxs-lookup"><span data-stu-id="0d37f-393">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="0d37f-394">您可以通过在邮件中设置 属性来控制哪些部分使用 Markdown `markdown` 或 HTML。</span><span class="sxs-lookup"><span data-stu-id="0d37f-394">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="0d37f-395">默认情况下， `markdown` 设置为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="0d37f-395">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="0d37f-396">如果要改为使用 HTML，请设置为 `markdown` `false` 。</span><span class="sxs-lookup"><span data-stu-id="0d37f-396">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="0d37f-397">如果指定 `themeColor` 属性，它将替代 `accentColor` 应用清单中的 属性。</span><span class="sxs-lookup"><span data-stu-id="0d37f-397">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="0d37f-398">若要指定 的呈现样式 `activityImage` ，可以如下 `activityImageType` 表所示进行设置：</span><span class="sxs-lookup"><span data-stu-id="0d37f-398">To specify the rendering style for `activityImage`, you can set `activityImageType` as shown in the following table:</span></span>

| <span data-ttu-id="0d37f-399">值</span><span class="sxs-lookup"><span data-stu-id="0d37f-399">Value</span></span> | <span data-ttu-id="0d37f-400">说明</span><span class="sxs-lookup"><span data-stu-id="0d37f-400">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="0d37f-401">默认值 `activityImage` ，裁剪为圆形。</span><span class="sxs-lookup"><span data-stu-id="0d37f-401">Default, `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="0d37f-402">`activityImage` 显示为矩形并保留其纵横比。</span><span class="sxs-lookup"><span data-stu-id="0d37f-402">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="0d37f-403">有关连接器卡属性的所有其他详细信息，请参阅 [可操作邮件卡参考](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="0d37f-403">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="0d37f-404">当前不支持的唯Teams连接器卡属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="0d37f-404">The only connector card properties that Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="0d37f-405">`startGroup`始终视为 `true` 在Teams</span><span class="sxs-lookup"><span data-stu-id="0d37f-405">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="0d37f-406">连接器Office 365示例</span><span class="sxs-lookup"><span data-stu-id="0d37f-406">Example of an Office 365 Connector card</span></span>

<span data-ttu-id="0d37f-407">以下代码显示了连接器Office 365示例：</span><span class="sxs-lookup"><span data-stu-id="0d37f-407">The following code shows an example of an Office 365 Connector card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "summary": "John Doe commented on Trello",
    "title": "Project Tango",
    "sections": [
        {
            "activityTitle": "John Doe commented",
            "activitySubtitle": "On Project Tango",
            "activityText": "\"Here are the designs\"",
            "activityImage": "http://connectorsdemo.azurewebsites.net/images/MSC12_Oscar_002.jpg"
        },
        {
            "title": "Details",
            "facts": [
                {
                    "name": "Labels",
                    "value": "Designs, redlines"
                },
                {
                    "name": "Due date",
                    "value": "Dec 7, 2016"
                },
                {
                    "name": "Attachments",
                    "value": "[final.jpg](http://connectorsdemo.azurewebsites.net/images/WIN14_Jan_04.jpg)"
                }
            ]
        },
        {
            "title": "Images",
            "images": [
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/MicrosoftSurface_024_Cafe_OH-06315_VS_R1c.jpg"
                },
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/WIN12_Scene_01.jpg"
                },
                {
                    "image":"http://connectorsdemo.azurewebsites.net/images/WIN12_Anthony_02.jpg"
                }
            ]
        }
    ],
    "potentialAction": [
        {
            "@context": "http://schema.org",
            "@type": "ViewAction",
            "name": "View in Trello",
            "target": [
                "https://trello.com/c/1101/"
            ]
        }
    ]
  }
}
```

## <a name="receipt-card"></a><span data-ttu-id="0d37f-408">收据卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-408">Receipt card</span></span>

<span data-ttu-id="0d37f-409">Teams支持收据卡。</span><span class="sxs-lookup"><span data-stu-id="0d37f-409">Teams supports receipt card.</span></span> <span data-ttu-id="0d37f-410">它是使机器人能够为用户提供收据的卡片。</span><span class="sxs-lookup"><span data-stu-id="0d37f-410">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="0d37f-411">它通常包含要包含在收据上的项目列表，如税务和总信息。</span><span class="sxs-lookup"><span data-stu-id="0d37f-411">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="0d37f-412">支持收据卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-412">Support for receipt cards</span></span>

<span data-ttu-id="0d37f-413">下表提供了支持收据卡的功能：</span><span class="sxs-lookup"><span data-stu-id="0d37f-413">The following table provides the features that support receipt cards:</span></span>

| <span data-ttu-id="0d37f-414">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="0d37f-414">Bots in Teams</span></span> | <span data-ttu-id="0d37f-415">消息扩展</span><span class="sxs-lookup"><span data-stu-id="0d37f-415">Messaging extensions</span></span>  | <span data-ttu-id="0d37f-416">连接器</span><span class="sxs-lookup"><span data-stu-id="0d37f-416">Connectors</span></span> | <span data-ttu-id="0d37f-417">机器人框架</span><span class="sxs-lookup"><span data-stu-id="0d37f-417">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d37f-418">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-418">✔</span></span> | <span data-ttu-id="0d37f-419">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-419">✔</span></span> | <span data-ttu-id="0d37f-420">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-420">✖</span></span> | <span data-ttu-id="0d37f-421">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-421">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="0d37f-422">收据卡示例</span><span class="sxs-lookup"><span data-stu-id="0d37f-422">Example of a receipt card</span></span>

![收据卡示例](~/assets/images/cards/receipt.png)

<span data-ttu-id="0d37f-424">以下代码显示收据卡的示例：</span><span class="sxs-lookup"><span data-stu-id="0d37f-424">The following code shows an example of a receipt card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.card.receipt",
  "content": {
    "title": "John Doe",
    "facts": [
      {
        "key": "Order Number",
        "value": "1234"
      },
      {
        "key": "Payment Method",
        "value": "VISA 5555-****"
      }
    ],
    "items": [
      {
        "title": "Data Transfer",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/traffic-manager.png"
        },
        "price": "$ 38.45",
        "quantity": "368"
      },
      {
        "title": "App Service",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/cloud-service.png"
        },
        "price": "$ 45.00",
        "quantity": "720"
      }
    ],
    "total": "$ 90.95",
    "tax": "$ 7.50",
    "buttons": [
      {
        "type": "openUrl",
        "title": "More information",
        "image": "https://account.windowsazure.com/content/6.10.1.38-.8225.160809-1618/aux-pre/images/offer-icon-freetrial.png",
        "value": "https://azure.microsoft.com/en-us/pricing/"
      }
    ]
  }
}
```

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="0d37f-425">收据卡上的其他信息</span><span class="sxs-lookup"><span data-stu-id="0d37f-425">Additional information on receipt cards</span></span>

<span data-ttu-id="0d37f-426">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="0d37f-426">Bot Framework reference:</span></span>

* [<span data-ttu-id="0d37f-427">收据卡Node.js</span><span class="sxs-lookup"><span data-stu-id="0d37f-427">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="0d37f-428">收据卡 C#</span><span class="sxs-lookup"><span data-stu-id="0d37f-428">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="0d37f-429">登录卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-429">Signin card</span></span>

<span data-ttu-id="0d37f-430">自动Teams中的登录卡类似于 Bot 框架中的登录卡，只不过 Teams 中的登录卡仅支持两个 `signin` 操作 `openUrl` 和 。</span><span class="sxs-lookup"><span data-stu-id="0d37f-430">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions `signin` and `openUrl`.</span></span>

<span data-ttu-id="0d37f-431">登录操作可以从登录卡Teams，而不只是从登录卡使用。</span><span class="sxs-lookup"><span data-stu-id="0d37f-431">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="0d37f-432">有关详细信息，请参阅自动[Teams的身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="0d37f-432">For more information, see [Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="0d37f-433">支持登录卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-433">Support for signin cards</span></span>

<span data-ttu-id="0d37f-434">下表提供了支持登录卡的功能：</span><span class="sxs-lookup"><span data-stu-id="0d37f-434">The following table provides the features that support signin cards:</span></span>

| <span data-ttu-id="0d37f-435">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="0d37f-435">Bots in Teams</span></span> | <span data-ttu-id="0d37f-436">消息扩展</span><span class="sxs-lookup"><span data-stu-id="0d37f-436">Messaging extensions</span></span>  | <span data-ttu-id="0d37f-437">连接器</span><span class="sxs-lookup"><span data-stu-id="0d37f-437">Connectors</span></span> | <span data-ttu-id="0d37f-438">机器人框架</span><span class="sxs-lookup"><span data-stu-id="0d37f-438">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d37f-439">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-439">✔</span></span> | <span data-ttu-id="0d37f-440">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-440">✖</span></span> | <span data-ttu-id="0d37f-441">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-441">✖</span></span> | <span data-ttu-id="0d37f-442">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-442">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="0d37f-443">登录卡的其他信息</span><span class="sxs-lookup"><span data-stu-id="0d37f-443">Additional information on signin cards</span></span>

<span data-ttu-id="0d37f-444">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="0d37f-444">Bot Framework reference:</span></span>

* [<span data-ttu-id="0d37f-445">登录卡Node.js</span><span class="sxs-lookup"><span data-stu-id="0d37f-445">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="0d37f-446">登录卡 C#</span><span class="sxs-lookup"><span data-stu-id="0d37f-446">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="0d37f-447">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="0d37f-447">Thumbnail card</span></span>

<span data-ttu-id="0d37f-448">可以使用用于发送简单的可操作邮件的缩略图卡。</span><span class="sxs-lookup"><span data-stu-id="0d37f-448">You can work with a thumbnail card that is used for sending a simple actionable message.</span></span> <span data-ttu-id="0d37f-449">通常包含单个缩略图图像、一个或多个按钮和文本的卡片。</span><span class="sxs-lookup"><span data-stu-id="0d37f-449">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="0d37f-450">对缩略图卡的支持</span><span class="sxs-lookup"><span data-stu-id="0d37f-450">Support for thumbnail cards</span></span>

<span data-ttu-id="0d37f-451">下表提供了支持缩略图卡的功能：</span><span class="sxs-lookup"><span data-stu-id="0d37f-451">The following table provides the features that support thumbnail cards:</span></span>

| <span data-ttu-id="0d37f-452">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="0d37f-452">Bots in Teams</span></span> | <span data-ttu-id="0d37f-453">消息扩展</span><span class="sxs-lookup"><span data-stu-id="0d37f-453">Messaging extensions</span></span>  | <span data-ttu-id="0d37f-454">连接器</span><span class="sxs-lookup"><span data-stu-id="0d37f-454">Connectors</span></span> | <span data-ttu-id="0d37f-455">机器人框架</span><span class="sxs-lookup"><span data-stu-id="0d37f-455">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d37f-456">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-456">✔</span></span> | <span data-ttu-id="0d37f-457">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-457">✔</span></span> | <span data-ttu-id="0d37f-458">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-458">✖</span></span> | <span data-ttu-id="0d37f-459">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-459">✔</span></span> |

![缩略图卡片示例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="0d37f-461">缩略图卡片的属性</span><span class="sxs-lookup"><span data-stu-id="0d37f-461">Properties of a thumbnail card</span></span>

<span data-ttu-id="0d37f-462">下表提供缩略图卡片的属性：</span><span class="sxs-lookup"><span data-stu-id="0d37f-462">The following table provides the properties of a thumbnail card:</span></span>

| <span data-ttu-id="0d37f-463">属性</span><span class="sxs-lookup"><span data-stu-id="0d37f-463">Property</span></span> | <span data-ttu-id="0d37f-464">类型</span><span class="sxs-lookup"><span data-stu-id="0d37f-464">Type</span></span>  | <span data-ttu-id="0d37f-465">说明</span><span class="sxs-lookup"><span data-stu-id="0d37f-465">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="0d37f-466">title</span><span class="sxs-lookup"><span data-stu-id="0d37f-466">title</span></span> | <span data-ttu-id="0d37f-467">格式文本 </span><span class="sxs-lookup"><span data-stu-id="0d37f-467">Rich text</span></span> | <span data-ttu-id="0d37f-468">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="0d37f-468">Title of the card.</span></span> <span data-ttu-id="0d37f-469">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="0d37f-469">Maximum 2 lines.</span></span>|
| <span data-ttu-id="0d37f-470">subtitle</span><span class="sxs-lookup"><span data-stu-id="0d37f-470">subtitle</span></span> | <span data-ttu-id="0d37f-471">格式文本 </span><span class="sxs-lookup"><span data-stu-id="0d37f-471">Rich text</span></span> | <span data-ttu-id="0d37f-472">卡片的副标题。</span><span class="sxs-lookup"><span data-stu-id="0d37f-472">Subtitle of the card.</span></span> <span data-ttu-id="0d37f-473">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="0d37f-473">Maximum 2 lines.</span></span>|
| <span data-ttu-id="0d37f-474">text</span><span class="sxs-lookup"><span data-stu-id="0d37f-474">text</span></span> | <span data-ttu-id="0d37f-475">格式文本 </span><span class="sxs-lookup"><span data-stu-id="0d37f-475">Rich text</span></span> | <span data-ttu-id="0d37f-476">文本显示在副标题下。</span><span class="sxs-lookup"><span data-stu-id="0d37f-476">Text appears under the subtitle.</span></span> <span data-ttu-id="0d37f-477">有关格式设置选项，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="0d37f-477">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="0d37f-478">images</span><span class="sxs-lookup"><span data-stu-id="0d37f-478">images</span></span> | <span data-ttu-id="0d37f-479">图像数组</span><span class="sxs-lookup"><span data-stu-id="0d37f-479">Array of images</span></span> | <span data-ttu-id="0d37f-480">显示在卡片顶部的图像。</span><span class="sxs-lookup"><span data-stu-id="0d37f-480">Image displayed at the top of the card.</span></span> <span data-ttu-id="0d37f-481">纵横比 1：1 正方形。</span><span class="sxs-lookup"><span data-stu-id="0d37f-481">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="0d37f-482">按钮</span><span class="sxs-lookup"><span data-stu-id="0d37f-482">buttons</span></span> | <span data-ttu-id="0d37f-483">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="0d37f-483">Array of action objects</span></span> | <span data-ttu-id="0d37f-484">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="0d37f-484">Set of actions applicable to the current card.</span></span> <span data-ttu-id="0d37f-485">最大值 6。</span><span class="sxs-lookup"><span data-stu-id="0d37f-485">Maximum 6.</span></span> |
| <span data-ttu-id="0d37f-486">点击</span><span class="sxs-lookup"><span data-stu-id="0d37f-486">tap</span></span> | <span data-ttu-id="0d37f-487">Action 对象</span><span class="sxs-lookup"><span data-stu-id="0d37f-487">Action object</span></span> | <span data-ttu-id="0d37f-488">当用户点击卡片本身时激活。</span><span class="sxs-lookup"><span data-stu-id="0d37f-488">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="0d37f-489">缩略图卡片示例</span><span class="sxs-lookup"><span data-stu-id="0d37f-489">Example of a thumbnail card</span></span>

<span data-ttu-id="0d37f-490">以下代码显示了缩略图卡片的示例：</span><span class="sxs-lookup"><span data-stu-id="0d37f-490">The following code shows an example of a thumbnail card:</span></span>

```json
{
  "contentType": "application/vnd.microsoft.card.thumbnail",
  "content": {
    "title": "Bender",
    "subtitle": "tale of a robot who dared to love",
    "text": "Bender Bending Rodríguez is a main character in the animated television series Futurama. He was created by series creators Matt Groening and David X. Cohen, and is voiced by John DiMaggio",
    "images": [
      {
        "url": "https://upload.wikimedia.org/wikipedia/en/a/a6/Bender_Rodriguez.png",
        "alt": "Bender Rodríguez"
      }
    ],
    "buttons": [
      {
        "type": "imBack",
        "title": "Thumbs Up",
        "image": "http://moopz.com/assets_c/2012/06/emoji-thumbs-up-150-thumb-autox125-140616.jpg",
        "value": "I like it"
      },
      {
        "type": "imBack",
        "title": "Thumbs Down",
        "image": "http://yourfaceisstupid.com/wp-content/uploads/2014/08/thumbs-down.png",
        "value": "I don't like it"
      },
      {
        "type": "openUrl",
        "title": "I feel lucky",
        "image": "http://thumb9.shutterstock.com/photos/thumb_large/683806/148441982.jpg",
        "value": "https://www.bing.com/images/search?q=bender&qpvt=bender&qpvt=bender&qpvt=bender&FORM=IGRE"
      }
    ],
    "tap": {
      "type": "imBack",
      "value": "Tapped it!"
    }
  }
}
```

### <a name="additional-information"></a><span data-ttu-id="0d37f-491">其他信息</span><span class="sxs-lookup"><span data-stu-id="0d37f-491">Additional information</span></span>

<span data-ttu-id="0d37f-492">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="0d37f-492">Bot Framework reference:</span></span>

* [<span data-ttu-id="0d37f-493">缩略图卡片Node.js</span><span class="sxs-lookup"><span data-stu-id="0d37f-493">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="0d37f-494">缩略图卡片 C#</span><span class="sxs-lookup"><span data-stu-id="0d37f-494">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="0d37f-495">卡片集合</span><span class="sxs-lookup"><span data-stu-id="0d37f-495">Card collections</span></span>

<span data-ttu-id="0d37f-496">可以使用包括木马和列表集合的卡片集合。</span><span class="sxs-lookup"><span data-stu-id="0d37f-496">You can work with card collections that include carousel and list collections.</span></span> <span data-ttu-id="0d37f-497">Teams支持卡片集合。</span><span class="sxs-lookup"><span data-stu-id="0d37f-497">Teams supports card collections.</span></span> <span data-ttu-id="0d37f-498">卡片集合包括 `builder.AttachmentLayout.carousel` `builder.AttachmentLayout.list` 和 。</span><span class="sxs-lookup"><span data-stu-id="0d37f-498">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="0d37f-499">这些集合包含自适应、hero 或缩略图卡片。</span><span class="sxs-lookup"><span data-stu-id="0d37f-499">These collections contain Adaptive, hero, or thumbnail cards.</span></span>

### <a name="carousel-collection"></a><span data-ttu-id="0d37f-500">Carousel 集合</span><span class="sxs-lookup"><span data-stu-id="0d37f-500">Carousel collection</span></span>

<span data-ttu-id="0d37f-501">盘 [选布局](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) 显示卡片的盘选（可选）以及关联的操作按钮。</span><span class="sxs-lookup"><span data-stu-id="0d37f-501">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-carousel-collections"></a><span data-ttu-id="0d37f-502">支持木马集合</span><span class="sxs-lookup"><span data-stu-id="0d37f-502">Support for carousel collections</span></span>

<span data-ttu-id="0d37f-503">下表提供了支持盘车集合的功能：</span><span class="sxs-lookup"><span data-stu-id="0d37f-503">The following table provides the features that support carousel collections:</span></span>

| <span data-ttu-id="0d37f-504">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="0d37f-504">Bots in Teams</span></span> | <span data-ttu-id="0d37f-505">消息扩展</span><span class="sxs-lookup"><span data-stu-id="0d37f-505">Messaging extensions</span></span>  | <span data-ttu-id="0d37f-506">连接器</span><span class="sxs-lookup"><span data-stu-id="0d37f-506">Connectors</span></span> | <span data-ttu-id="0d37f-507">机器人框架</span><span class="sxs-lookup"><span data-stu-id="0d37f-507">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d37f-508">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-508">✔</span></span> | <span data-ttu-id="0d37f-509">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-509">✖</span></span> | <span data-ttu-id="0d37f-510">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-510">✖</span></span> | <span data-ttu-id="0d37f-511">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-511">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="0d37f-512">一个盘式消息最多可显示每封邮件 10 张卡片。</span><span class="sxs-lookup"><span data-stu-id="0d37f-512">A carousel can display a maximum of ten cards per message.</span></span>

#### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="0d37f-513">单盘式卡片的属性</span><span class="sxs-lookup"><span data-stu-id="0d37f-513">Properties of a carousel card</span></span>

<span data-ttu-id="0d37f-514">单盘式播放卡片的属性与 hero 和 thumbnail 卡片相同。</span><span class="sxs-lookup"><span data-stu-id="0d37f-514">Properties of a carousel card are same as the hero and thumbnail cards.</span></span>

#### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="0d37f-515">一个木马集合的示例</span><span class="sxs-lookup"><span data-stu-id="0d37f-515">Example of a carousel collection</span></span>

![卡片的盘点示例](~/assets/images/cards/carousel.png)

<span data-ttu-id="0d37f-517">以下代码显示了一个盘车集合示例：</span><span class="sxs-lookup"><span data-stu-id="0d37f-517">The following code shows an example of a carousel collection:</span></span>

```json
{
 "attachmentLayout": "carousel",
 "attachments":[
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "extraLarge",
                "weight": "bolder",
                "text": "Welcome to Employee Connect",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "size": "medium",
                "weight": "bolder",
                "text": "Add events to your calendar",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "The bot can send \r\rnotification to remind \r\ryou about the latest \r\revents and trainings.",
                "wrap": true,
                "height": "stretch"
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.2",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee connect"
              },
              {
                "type": "TextBlock",
                "text": "The bot can send notifications \r\rto remind you about the latest \r\r events and trainings",
                "wrap": true,
                "maxWidth": 2
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee Connect final"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Create and manage your tasks",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "text": "The app identifies all your pending tasks \r\r and helps you manage everything at \r\r one place.",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Try these commands \r\r- Pending Submissions \r\r- Pending Approvals- My Tools",
                "wrap": true,
                "height": "stretch"
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    }
  ]
}
```

#### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="0d37f-518">盘车集合的语法</span><span class="sxs-lookup"><span data-stu-id="0d37f-518">Syntax for carousel collections</span></span>

<span data-ttu-id="0d37f-519">`builder.AttachmentLayoutTypes.Carousel` 是木马集合的语法。</span><span class="sxs-lookup"><span data-stu-id="0d37f-519">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

### <a name="list-collection"></a><span data-ttu-id="0d37f-520">列表集合</span><span class="sxs-lookup"><span data-stu-id="0d37f-520">List collection</span></span>

<span data-ttu-id="0d37f-521">列表布局显示卡片的垂直堆叠列表（可选）以及关联的操作按钮。</span><span class="sxs-lookup"><span data-stu-id="0d37f-521">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

#### <a name="support-for-list-collections"></a><span data-ttu-id="0d37f-522">支持列表集合</span><span class="sxs-lookup"><span data-stu-id="0d37f-522">Support for list collections</span></span>

<span data-ttu-id="0d37f-523">下表提供了支持列表集合的功能：</span><span class="sxs-lookup"><span data-stu-id="0d37f-523">The following table provides the features that support list collections:</span></span>

| <span data-ttu-id="0d37f-524">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="0d37f-524">Bots in Teams</span></span> | <span data-ttu-id="0d37f-525">消息扩展</span><span class="sxs-lookup"><span data-stu-id="0d37f-525">Messaging extensions</span></span>  | <span data-ttu-id="0d37f-526">连接器</span><span class="sxs-lookup"><span data-stu-id="0d37f-526">Connectors</span></span> | <span data-ttu-id="0d37f-527">机器人框架</span><span class="sxs-lookup"><span data-stu-id="0d37f-527">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0d37f-528">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-528">✔</span></span> | <span data-ttu-id="0d37f-529">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-529">✔</span></span> | <span data-ttu-id="0d37f-530">✖</span><span class="sxs-lookup"><span data-stu-id="0d37f-530">✖</span></span> | <span data-ttu-id="0d37f-531">✔</span><span class="sxs-lookup"><span data-stu-id="0d37f-531">✔</span></span> |

#### <a name="example-of-a-list-collection"></a><span data-ttu-id="0d37f-532">列表集合的示例</span><span class="sxs-lookup"><span data-stu-id="0d37f-532">Example of a list collection</span></span>

![卡片列表示例](~/assets/images/cards/list.png)

<span data-ttu-id="0d37f-534">列表集合的属性与 hero 或 thumbnail 卡片相同。</span><span class="sxs-lookup"><span data-stu-id="0d37f-534">Properties of list collections are same as the hero or thumbnail cards.</span></span>

<span data-ttu-id="0d37f-535">列表最多可显示每封邮件 10 张卡片。</span><span class="sxs-lookup"><span data-stu-id="0d37f-535">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="0d37f-536">iOS 和 Android 上尚不支持列表卡的一些组合。</span><span class="sxs-lookup"><span data-stu-id="0d37f-536">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

#### <a name="syntax-for-list-collections"></a><span data-ttu-id="0d37f-537">列表集合的语法</span><span class="sxs-lookup"><span data-stu-id="0d37f-537">Syntax for list collections</span></span>

<span data-ttu-id="0d37f-538">`builder.AttachmentLayout.list` 是列表集合的语法。</span><span class="sxs-lookup"><span data-stu-id="0d37f-538">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="0d37f-539">不支持的Teams</span><span class="sxs-lookup"><span data-stu-id="0d37f-539">Cards not supported in Teams</span></span>

<span data-ttu-id="0d37f-540">以下卡片由 Bot Framework 实现，但不受自动程序Teams：</span><span class="sxs-lookup"><span data-stu-id="0d37f-540">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="0d37f-541">动画卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-541">Animation cards</span></span>
* <span data-ttu-id="0d37f-542">音频卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-542">Audio cards</span></span>
* <span data-ttu-id="0d37f-543">视频卡</span><span class="sxs-lookup"><span data-stu-id="0d37f-543">Video cards</span></span>

## <a name="see-also"></a><span data-ttu-id="0d37f-544">另请参阅</span><span class="sxs-lookup"><span data-stu-id="0d37f-544">See also</span></span>

* [<span data-ttu-id="0d37f-545">任务模块</span><span class="sxs-lookup"><span data-stu-id="0d37f-545">Task modules</span></span>](~/task-modules-and-cards/what-are-task-modules.md)
* [<span data-ttu-id="0d37f-546">格式化卡片</span><span class="sxs-lookup"><span data-stu-id="0d37f-546">Format cards</span></span>](~/task-modules-and-cards/cards/cards-format.md)
