---
title: 卡参考
description: 介绍自动程序可用的所有卡片和Teams
localization_priority: Normal
keywords: 机器人卡参考
ms.topic: reference
ms.openlocfilehash: d3f0904326f951475c8a0d3e17daf720d9aad489
ms.sourcegitcommit: c59d90ae03eae32996db49f162855965b55c52fe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/26/2021
ms.locfileid: "52668860"
---
# <a name="cards-reference"></a><span data-ttu-id="3ea1e-104">卡参考</span><span class="sxs-lookup"><span data-stu-id="3ea1e-104">Cards reference</span></span>

<span data-ttu-id="3ea1e-105">自动程序支持本文档中列出的Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-105">The cards listed in this document are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="3ea1e-106">它们基于 Bot Framework (BF) 定义的卡，Teams不支持所有 Bot Framework 卡，而是添加了Teams一些自动程序卡。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-106">They are based on cards defined by the Bot Framework (BF), but Teams does not support all Bot Framework cards and instead some Teams cards have been added.</span></span> <span data-ttu-id="3ea1e-107">本文档的参考中已指出区别。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="3ea1e-108">卡片示例</span><span class="sxs-lookup"><span data-stu-id="3ea1e-108">Card examples</span></span>

<span data-ttu-id="3ea1e-109">有关如何使用卡的其他信息，请参阅 Bot Builder SDK v3 的文档。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="3ea1e-110">代码示例也可在 Microsoft/BotBuilder-Samples 存储库上GitHub。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="3ea1e-111">.NET</span><span class="sxs-lookup"><span data-stu-id="3ea1e-111">.NET</span></span>
  * <span data-ttu-id="3ea1e-112">[将卡片添加为邮件的附件](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-112">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="3ea1e-113">[卡片示例代码自动程序生成器 v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards)。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-113">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="3ea1e-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="3ea1e-114">Node.js</span></span>
  * <span data-ttu-id="3ea1e-115">[将卡片添加为邮件的附件](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-115">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="3ea1e-116">[卡片示例代码自动程序生成器 v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards)。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-116">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="3ea1e-117">卡片类型</span><span class="sxs-lookup"><span data-stu-id="3ea1e-117">Types of cards</span></span>

<span data-ttu-id="3ea1e-118">此表显示了可供你使用卡片的类型：</span><span class="sxs-lookup"><span data-stu-id="3ea1e-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="3ea1e-119">卡片类型</span><span class="sxs-lookup"><span data-stu-id="3ea1e-119">Card type</span></span> | <span data-ttu-id="3ea1e-120">说明</span><span class="sxs-lookup"><span data-stu-id="3ea1e-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="3ea1e-121">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="3ea1e-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="3ea1e-122">此卡片是可高度自定义的卡片，可以包含文本、语音、图像、按钮和输入字段的任意组合。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-122">This card is highly customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="3ea1e-123">Hero card</span><span class="sxs-lookup"><span data-stu-id="3ea1e-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="3ea1e-124">此卡片通常包含一个大图像、一个或多个按钮和少量文本。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-124">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="3ea1e-125">列表卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-125">List card</span></span>](#list-card) | <span data-ttu-id="3ea1e-126">此卡片是项的滚动列表。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-126">This card is a scrolling list of items.</span></span> |
| [<span data-ttu-id="3ea1e-127">Office 365连接器卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="3ea1e-128">此卡片具有具有多个分区、字段、图像和操作的灵活性布局。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-128">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="3ea1e-129">收据卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="3ea1e-130">此卡为用户提供收据。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-130">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="3ea1e-131">登录卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="3ea1e-132">此卡使机器人可以请求用户登录。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-132">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="3ea1e-133">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="3ea1e-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="3ea1e-134">此卡片通常包含一个缩略图图像、一些短文本以及一个或多个按钮。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-134">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="3ea1e-135">卡片集合</span><span class="sxs-lookup"><span data-stu-id="3ea1e-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="3ea1e-136">此卡片用于在单个响应中返回多个项目。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-136">This cards is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="3ea1e-137">所有卡片的常见属性</span><span class="sxs-lookup"><span data-stu-id="3ea1e-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="3ea1e-138">内联卡片图像</span><span class="sxs-lookup"><span data-stu-id="3ea1e-138">Inline card images</span></span>

<span data-ttu-id="3ea1e-139">卡片可以包含内联图像，包括指向公开可用图像的链接。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="3ea1e-140">出于性能目的，强烈建议您将映像托管在公共内容交付网络或 (CDN) 。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="3ea1e-141">在保持纵横比以覆盖图像区域的同时，图像大小会向上或向下扩展。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area.</span></span> <span data-ttu-id="3ea1e-142">然后从中心裁剪图像，以实现卡片的适当纵横比。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-142">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="3ea1e-143">图像必须最多为 1024×1024 PNG、JPEG 或 GIF 格式，并且不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-143">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and do not support animated GIF.</span></span>

| <span data-ttu-id="3ea1e-144">属性</span><span class="sxs-lookup"><span data-stu-id="3ea1e-144">Property</span></span> | <span data-ttu-id="3ea1e-145">类型</span><span class="sxs-lookup"><span data-stu-id="3ea1e-145">Type</span></span>  | <span data-ttu-id="3ea1e-146">说明</span><span class="sxs-lookup"><span data-stu-id="3ea1e-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3ea1e-147">url</span><span class="sxs-lookup"><span data-stu-id="3ea1e-147">url</span></span> | <span data-ttu-id="3ea1e-148">URL</span><span class="sxs-lookup"><span data-stu-id="3ea1e-148">URL</span></span> | <span data-ttu-id="3ea1e-149">图像的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-149">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="3ea1e-150">alt</span><span class="sxs-lookup"><span data-stu-id="3ea1e-150">alt</span></span> | <span data-ttu-id="3ea1e-151">String</span><span class="sxs-lookup"><span data-stu-id="3ea1e-151">String</span></span> | <span data-ttu-id="3ea1e-152">图像的辅助说明。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-152">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="3ea1e-153">如果卡片包含的图像 URL 在最终图像之前经过重定向，则不支持图像 URL 中的重定向。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-153">If a card includes an image URL that goes through a redirect before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="3ea1e-154">对于在公有云上共享的图像，会出现此情况。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-154">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="3ea1e-155">按钮</span><span class="sxs-lookup"><span data-stu-id="3ea1e-155">Buttons</span></span>

<span data-ttu-id="3ea1e-156">按钮显示在卡片底部堆叠。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-156">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="3ea1e-157">按钮文本始终位于单行，如果文本超过按钮宽度，则将被截断。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-157">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="3ea1e-158">不会显示超过卡支持的最大数目的其他任何按钮。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-158">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="3ea1e-159">有关详细信息，请参阅 [卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-159">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="3ea1e-160">卡片格式</span><span class="sxs-lookup"><span data-stu-id="3ea1e-160">Card formatting</span></span>

<span data-ttu-id="3ea1e-161">有关卡片中的文本格式设置详细信息，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-161">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="3ea1e-162">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="3ea1e-162">Adaptive card</span></span>

<span data-ttu-id="3ea1e-163">自适应卡片是可自定义的卡片，可以包含文本、语音、图像、按钮和输入字段的任意组合。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-163">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="3ea1e-164">有关详细信息，请参阅[自适应卡片 v1.2.0。](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)</span><span class="sxs-lookup"><span data-stu-id="3ea1e-164">For more information, see [adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="3ea1e-165">自适应卡片支持</span><span class="sxs-lookup"><span data-stu-id="3ea1e-165">Support for adaptive cards</span></span>

| <span data-ttu-id="3ea1e-166">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="3ea1e-166">Bots in Teams</span></span> | <span data-ttu-id="3ea1e-167">消息扩展</span><span class="sxs-lookup"><span data-stu-id="3ea1e-167">Messaging extensions</span></span>  | <span data-ttu-id="3ea1e-168">连接器</span><span class="sxs-lookup"><span data-stu-id="3ea1e-168">Connectors</span></span> | <span data-ttu-id="3ea1e-169">机器人框架</span><span class="sxs-lookup"><span data-stu-id="3ea1e-169">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ea1e-170">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-170">✔</span></span> | <span data-ttu-id="3ea1e-171">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-171">✔</span></span> | <span data-ttu-id="3ea1e-172">✖</span><span class="sxs-lookup"><span data-stu-id="3ea1e-172">✖</span></span> | <span data-ttu-id="3ea1e-173">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-173">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="3ea1e-174">Teams平台支持 v1.2 或更早的自适应卡片功能。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-174">Teams platform supports v1.2 or earlier of adaptive card features.</span></span>
> * <span data-ttu-id="3ea1e-175">媒体元素当前在应用平台上的自适应卡片 v1.2 中Teams支持。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-175">Media elements are currently not supported in adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="3ea1e-176">自适应卡片示例</span><span class="sxs-lookup"><span data-stu-id="3ea1e-176">Example of an adaptive card</span></span>

![自适应卡片示例](~/assets/images/cards/adaptivecard.png)

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="3ea1e-178">自适应卡片的其他信息</span><span class="sxs-lookup"><span data-stu-id="3ea1e-178">Additional information on adaptive cards</span></span>

<span data-ttu-id="3ea1e-179">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="3ea1e-179">Bot Framework reference:</span></span>

* [<span data-ttu-id="3ea1e-180">自适应卡片Node.js</span><span class="sxs-lookup"><span data-stu-id="3ea1e-180">Adaptive cards Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="3ea1e-181">自适应卡片 C#</span><span class="sxs-lookup"><span data-stu-id="3ea1e-181">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="3ea1e-182">Hero card</span><span class="sxs-lookup"><span data-stu-id="3ea1e-182">Hero card</span></span>

<span data-ttu-id="3ea1e-183">通常包含单个大图像、一个或多个按钮和文本的卡片。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-183">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="3ea1e-184">支持人物卡片</span><span class="sxs-lookup"><span data-stu-id="3ea1e-184">Support for hero cards</span></span>

| <span data-ttu-id="3ea1e-185">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="3ea1e-185">Bots in Teams</span></span> | <span data-ttu-id="3ea1e-186">消息扩展</span><span class="sxs-lookup"><span data-stu-id="3ea1e-186">Messaging extensions</span></span>  | <span data-ttu-id="3ea1e-187">连接器</span><span class="sxs-lookup"><span data-stu-id="3ea1e-187">Connectors</span></span> | <span data-ttu-id="3ea1e-188">机器人框架</span><span class="sxs-lookup"><span data-stu-id="3ea1e-188">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ea1e-189">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-189">✔</span></span> | <span data-ttu-id="3ea1e-190">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-190">✔</span></span> | <span data-ttu-id="3ea1e-191">✖</span><span class="sxs-lookup"><span data-stu-id="3ea1e-191">✖</span></span> | <span data-ttu-id="3ea1e-192">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-192">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="3ea1e-193">Hero 卡片的属性</span><span class="sxs-lookup"><span data-stu-id="3ea1e-193">Properties of a hero card</span></span>

| <span data-ttu-id="3ea1e-194">属性</span><span class="sxs-lookup"><span data-stu-id="3ea1e-194">Property</span></span> | <span data-ttu-id="3ea1e-195">类型</span><span class="sxs-lookup"><span data-stu-id="3ea1e-195">Type</span></span>  | <span data-ttu-id="3ea1e-196">说明</span><span class="sxs-lookup"><span data-stu-id="3ea1e-196">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3ea1e-197">title</span><span class="sxs-lookup"><span data-stu-id="3ea1e-197">title</span></span> | <span data-ttu-id="3ea1e-198">格式文本 </span><span class="sxs-lookup"><span data-stu-id="3ea1e-198">Rich text</span></span> | <span data-ttu-id="3ea1e-199">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-199">Title of the card.</span></span> <span data-ttu-id="3ea1e-200">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-200">Maximum 2 lines.</span></span> |
| <span data-ttu-id="3ea1e-201">subtitle</span><span class="sxs-lookup"><span data-stu-id="3ea1e-201">subtitle</span></span> | <span data-ttu-id="3ea1e-202">格式文本 </span><span class="sxs-lookup"><span data-stu-id="3ea1e-202">Rich text</span></span> | <span data-ttu-id="3ea1e-203">卡片的副标题。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-203">Subtitle of the card.</span></span> <span data-ttu-id="3ea1e-204">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-204">Maximum 2 lines.</span></span>|
| <span data-ttu-id="3ea1e-205">text</span><span class="sxs-lookup"><span data-stu-id="3ea1e-205">text</span></span> | <span data-ttu-id="3ea1e-206">格式文本 </span><span class="sxs-lookup"><span data-stu-id="3ea1e-206">Rich text</span></span> | <span data-ttu-id="3ea1e-207">文本显示在副标题下。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-207">Text appears under the subtitle.</span></span> <span data-ttu-id="3ea1e-208">有关格式设置选项，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-208">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="3ea1e-209">images</span><span class="sxs-lookup"><span data-stu-id="3ea1e-209">images</span></span> | <span data-ttu-id="3ea1e-210">图像数组</span><span class="sxs-lookup"><span data-stu-id="3ea1e-210">Array of images</span></span> | <span data-ttu-id="3ea1e-211">显示在卡片顶部的图像。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-211">Image displayed at the top of the card.</span></span> <span data-ttu-id="3ea1e-212">纵横比 16：9。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-212">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="3ea1e-213">按钮</span><span class="sxs-lookup"><span data-stu-id="3ea1e-213">buttons</span></span> | <span data-ttu-id="3ea1e-214">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="3ea1e-214">Array of action objects</span></span> | <span data-ttu-id="3ea1e-215">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-215">Set of actions applicable to the current card.</span></span> <span data-ttu-id="3ea1e-216">最大值 6。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-216">Maximum 6.</span></span> |
| <span data-ttu-id="3ea1e-217">点击</span><span class="sxs-lookup"><span data-stu-id="3ea1e-217">tap</span></span> | <span data-ttu-id="3ea1e-218">Action 对象</span><span class="sxs-lookup"><span data-stu-id="3ea1e-218">Action object</span></span> | <span data-ttu-id="3ea1e-219">当用户点击卡片本身时激活。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-219">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="3ea1e-220">Hero 卡片示例</span><span class="sxs-lookup"><span data-stu-id="3ea1e-220">Example of a hero card</span></span>

![Hero 卡片示例](~/assets/images/cards/hero.png)

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="3ea1e-222">有关 hero cards 的其他信息</span><span class="sxs-lookup"><span data-stu-id="3ea1e-222">Additional information on hero cards</span></span>

<span data-ttu-id="3ea1e-223">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="3ea1e-223">Bot Framework reference:</span></span>

* [<span data-ttu-id="3ea1e-224">Hero card Node.js</span><span class="sxs-lookup"><span data-stu-id="3ea1e-224">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="3ea1e-225">Hero card C#</span><span class="sxs-lookup"><span data-stu-id="3ea1e-225">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="3ea1e-226">列表卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-226">List card</span></span>

<span data-ttu-id="3ea1e-227">列表卡片已由列表Teams，以提供列表集合可以提供的功能之外的功能。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-227">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="3ea1e-228">列表卡片提供项的滚动列表。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-228">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="3ea1e-229">支持列表卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-229">Support for list cards</span></span>

| <span data-ttu-id="3ea1e-230">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="3ea1e-230">Bots in Teams</span></span> | <span data-ttu-id="3ea1e-231">消息扩展</span><span class="sxs-lookup"><span data-stu-id="3ea1e-231">Messaging extensions</span></span>  | <span data-ttu-id="3ea1e-232">连接器</span><span class="sxs-lookup"><span data-stu-id="3ea1e-232">Connectors</span></span> | <span data-ttu-id="3ea1e-233">机器人框架</span><span class="sxs-lookup"><span data-stu-id="3ea1e-233">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ea1e-234">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-234">✔</span></span> | <span data-ttu-id="3ea1e-235">✖</span><span class="sxs-lookup"><span data-stu-id="3ea1e-235">✖</span></span> | <span data-ttu-id="3ea1e-236">✖</span><span class="sxs-lookup"><span data-stu-id="3ea1e-236">✖</span></span> |<span data-ttu-id="3ea1e-237">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-237">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="3ea1e-238">列表卡片的属性</span><span class="sxs-lookup"><span data-stu-id="3ea1e-238">Properties of a list card</span></span>

| <span data-ttu-id="3ea1e-239">属性</span><span class="sxs-lookup"><span data-stu-id="3ea1e-239">Property</span></span> | <span data-ttu-id="3ea1e-240">类型</span><span class="sxs-lookup"><span data-stu-id="3ea1e-240">Type</span></span>  | <span data-ttu-id="3ea1e-241">说明</span><span class="sxs-lookup"><span data-stu-id="3ea1e-241">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3ea1e-242">title</span><span class="sxs-lookup"><span data-stu-id="3ea1e-242">title</span></span> | <span data-ttu-id="3ea1e-243">格式文本 </span><span class="sxs-lookup"><span data-stu-id="3ea1e-243">Rich text</span></span> | <span data-ttu-id="3ea1e-244">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-244">Title of the card.</span></span> <span data-ttu-id="3ea1e-245">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-245">Maximum 2 lines.</span></span>|
| <span data-ttu-id="3ea1e-246">项目</span><span class="sxs-lookup"><span data-stu-id="3ea1e-246">items</span></span> | <span data-ttu-id="3ea1e-247">列表项数组</span><span class="sxs-lookup"><span data-stu-id="3ea1e-247">Array of list items</span></span> ||
| <span data-ttu-id="3ea1e-248">按钮</span><span class="sxs-lookup"><span data-stu-id="3ea1e-248">buttons</span></span> | <span data-ttu-id="3ea1e-249">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="3ea1e-249">Array of action objects</span></span> | <span data-ttu-id="3ea1e-250">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-250">Set of actions applicable to the current card.</span></span> <span data-ttu-id="3ea1e-251">最大值 6。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-251">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="3ea1e-252">列表卡片示例</span><span class="sxs-lookup"><span data-stu-id="3ea1e-252">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="3ea1e-253">Office 365连接器卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-253">Office 365 connector card</span></span>

<span data-ttu-id="3ea1e-254">自动Office 365支持自动Teams，而不是 Bot Framework。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-254">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="3ea1e-255">此卡片提供具有多个分区、字段、图像和操作的灵活性布局。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-255">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="3ea1e-256">此卡封装连接器卡，以便机器人可以使用它。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-256">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="3ea1e-257">有关连接器卡和 O365 卡之间的差异，请参阅连接器卡[上的Office 365注释](#notes-on-the-office-365-connector-card)。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-257">For differences between connector cards and the O365 card, see [Notes on the Office 365 connector card](#notes-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="3ea1e-258">支持 Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-258">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="3ea1e-259">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="3ea1e-259">Bots in Teams</span></span> | <span data-ttu-id="3ea1e-260">消息扩展</span><span class="sxs-lookup"><span data-stu-id="3ea1e-260">Messaging extensions</span></span>  | <span data-ttu-id="3ea1e-261">连接器</span><span class="sxs-lookup"><span data-stu-id="3ea1e-261">Connectors</span></span> | <span data-ttu-id="3ea1e-262">机器人框架</span><span class="sxs-lookup"><span data-stu-id="3ea1e-262">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ea1e-263">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-263">✔</span></span> | <span data-ttu-id="3ea1e-264">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-264">✔</span></span> | <span data-ttu-id="3ea1e-265">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-265">✔</span></span> | <span data-ttu-id="3ea1e-266">✖</span><span class="sxs-lookup"><span data-stu-id="3ea1e-266">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="3ea1e-267">连接器Office 365的属性</span><span class="sxs-lookup"><span data-stu-id="3ea1e-267">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="3ea1e-268">属性</span><span class="sxs-lookup"><span data-stu-id="3ea1e-268">Property</span></span> | <span data-ttu-id="3ea1e-269">类型</span><span class="sxs-lookup"><span data-stu-id="3ea1e-269">Type</span></span>  | <span data-ttu-id="3ea1e-270">说明</span><span class="sxs-lookup"><span data-stu-id="3ea1e-270">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3ea1e-271">title</span><span class="sxs-lookup"><span data-stu-id="3ea1e-271">title</span></span> | <span data-ttu-id="3ea1e-272">格式文本 </span><span class="sxs-lookup"><span data-stu-id="3ea1e-272">Rich text</span></span> | <span data-ttu-id="3ea1e-273">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-273">Title of the card.</span></span> <span data-ttu-id="3ea1e-274">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-274">Maximum 2 lines.</span></span> |
| <span data-ttu-id="3ea1e-275">摘要</span><span class="sxs-lookup"><span data-stu-id="3ea1e-275">summary</span></span> | <span data-ttu-id="3ea1e-276">格式文本 </span><span class="sxs-lookup"><span data-stu-id="3ea1e-276">Rich text</span></span> | <span data-ttu-id="3ea1e-277">卡片摘要。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-277">Summary of the card.</span></span> <span data-ttu-id="3ea1e-278">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-278">Maximum 2 lines.</span></span> |
| <span data-ttu-id="3ea1e-279">text</span><span class="sxs-lookup"><span data-stu-id="3ea1e-279">text</span></span> | <span data-ttu-id="3ea1e-280">格式文本 </span><span class="sxs-lookup"><span data-stu-id="3ea1e-280">Rich text</span></span> | <span data-ttu-id="3ea1e-281">文本显示在副标题下。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-281">Text appears under the subtitle.</span></span> <span data-ttu-id="3ea1e-282">有关格式设置选项，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-282">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="3ea1e-283">themeColor</span><span class="sxs-lookup"><span data-stu-id="3ea1e-283">themeColor</span></span> | <span data-ttu-id="3ea1e-284">十六进制字符串</span><span class="sxs-lookup"><span data-stu-id="3ea1e-284">HEX string</span></span> | <span data-ttu-id="3ea1e-285">替代应用程序清单中提供的 accentColor 的颜色。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-285">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="3ea1e-286">连接器卡Office 365备注</span><span class="sxs-lookup"><span data-stu-id="3ea1e-286">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="3ea1e-287">Office 365连接器卡在 Microsoft Teams中正常工作，包括[ActionCard 操作](/outlook/actionable-messages/card-reference#actioncard-action)。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-287">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="3ea1e-288">从连接器使用连接器卡和在机器人中使用连接器卡之间的一个重要区别是处理卡操作。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-288">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="3ea1e-289">对于连接器，终结点通过 HTTP POST 接收卡有效负载。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-289">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="3ea1e-290">对于自动程序，该操作将触发仅向自动程序发送操作 ID 和 `HttpPOST` `invoke` 正文的活动。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-290">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="3ea1e-291">每个连接器卡最多可以显示 10 个部分，每个部分最多可以包含 5 个图像和 5 个操作。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-291">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="3ea1e-292">邮件中不显示任何其他节、图像或操作。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-292">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="3ea1e-293">所有文本字段都支持 markdown 和 HTML。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-293">All text fields support markdown and HTML.</span></span> <span data-ttu-id="3ea1e-294">您可以通过在邮件中设置 属性来控制使用 markdown 或 HTML `markdown` 的部分。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-294">You can control which sections use markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="3ea1e-295">默认情况下， `markdown` 设置为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-295">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="3ea1e-296">如果要改为使用 HTML，请设置为 `markdown` `false` 。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-296">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="3ea1e-297">如果指定 `themeColor` 属性，它将替代 `accentColor` 应用清单中的 属性。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-297">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="3ea1e-298">若要指定 的呈现样式 `activityImage` ，可以按 `activityImageType` 如下方式设置：</span><span class="sxs-lookup"><span data-stu-id="3ea1e-298">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="3ea1e-299">值</span><span class="sxs-lookup"><span data-stu-id="3ea1e-299">Value</span></span> | <span data-ttu-id="3ea1e-300">说明</span><span class="sxs-lookup"><span data-stu-id="3ea1e-300">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="3ea1e-301">默认值; `activityImage` 裁剪为圆形。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-301">Default; `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="3ea1e-302">`activityImage` 显示为矩形并保留其纵横比。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-302">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="3ea1e-303">有关连接器卡属性的所有其他详细信息，请参阅 [可操作邮件卡参考](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-303">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="3ea1e-304">当前不支持的唯Microsoft Teams连接器卡属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="3ea1e-304">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="3ea1e-305">`startGroup`始终视为 `true` 在Teams</span><span class="sxs-lookup"><span data-stu-id="3ea1e-305">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="3ea1e-306">连接Office 365示例</span><span class="sxs-lookup"><span data-stu-id="3ea1e-306">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="3ea1e-307">收据卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-307">Receipt card</span></span>

<span data-ttu-id="3ea1e-308">Teams支持收据卡。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-308">Teams supports receipt card.</span></span> <span data-ttu-id="3ea1e-309">它是使机器人能够为用户提供收据的卡片。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-309">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="3ea1e-310">它通常包含要包含在收据上的项目列表，如税务和总信息。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-310">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="3ea1e-311">支持收据卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-311">Support for receipt cards</span></span>

| <span data-ttu-id="3ea1e-312">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="3ea1e-312">Bots in Teams</span></span> | <span data-ttu-id="3ea1e-313">消息扩展</span><span class="sxs-lookup"><span data-stu-id="3ea1e-313">Messaging extensions</span></span>  | <span data-ttu-id="3ea1e-314">连接器</span><span class="sxs-lookup"><span data-stu-id="3ea1e-314">Connectors</span></span> | <span data-ttu-id="3ea1e-315">机器人框架</span><span class="sxs-lookup"><span data-stu-id="3ea1e-315">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ea1e-316">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-316">✔</span></span> | <span data-ttu-id="3ea1e-317">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-317">✔</span></span> | <span data-ttu-id="3ea1e-318">✖</span><span class="sxs-lookup"><span data-stu-id="3ea1e-318">✖</span></span> | <span data-ttu-id="3ea1e-319">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-319">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="3ea1e-320">收据卡示例</span><span class="sxs-lookup"><span data-stu-id="3ea1e-320">Example of a receipt card</span></span>

![收据卡示例](~/assets/images/cards/receipt.png)

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="3ea1e-322">收据卡上的其他信息</span><span class="sxs-lookup"><span data-stu-id="3ea1e-322">Additional information on receipt cards</span></span>

<span data-ttu-id="3ea1e-323">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="3ea1e-323">Bot Framework reference:</span></span>

* [<span data-ttu-id="3ea1e-324">收据卡Node.js</span><span class="sxs-lookup"><span data-stu-id="3ea1e-324">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="3ea1e-325">收据卡 C#</span><span class="sxs-lookup"><span data-stu-id="3ea1e-325">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="3ea1e-326">登录卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-326">Signin card</span></span>

<span data-ttu-id="3ea1e-327">登录卡使机器人可以请求用户登录。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-327">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="3ea1e-328">在自动Teams中支持它，其形式与 Bot Framework 中略有不同。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-328">It is supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="3ea1e-329">自动Teams中的登录卡类似于 Bot 框架中的登录卡，只不过 Teams 中的登录卡仅支持两个操作： 和 `signin` `openUrl` 。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-329">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="3ea1e-330">登录操作可以从登录卡Teams，而不只是从登录卡使用。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-330">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="3ea1e-331">有关身份验证详细信息，请参阅自动[Microsoft Teams的身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-331">For more information on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="3ea1e-332">支持登录卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-332">Support for signin cards</span></span>

| <span data-ttu-id="3ea1e-333">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="3ea1e-333">Bots in Teams</span></span> | <span data-ttu-id="3ea1e-334">消息扩展</span><span class="sxs-lookup"><span data-stu-id="3ea1e-334">Messaging extensions</span></span>  | <span data-ttu-id="3ea1e-335">连接器</span><span class="sxs-lookup"><span data-stu-id="3ea1e-335">Connectors</span></span> | <span data-ttu-id="3ea1e-336">机器人框架</span><span class="sxs-lookup"><span data-stu-id="3ea1e-336">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ea1e-337">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-337">✔</span></span> | <span data-ttu-id="3ea1e-338">✖</span><span class="sxs-lookup"><span data-stu-id="3ea1e-338">✖</span></span> | <span data-ttu-id="3ea1e-339">✖</span><span class="sxs-lookup"><span data-stu-id="3ea1e-339">✖</span></span> | <span data-ttu-id="3ea1e-340">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-340">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="3ea1e-341">登录卡的其他信息</span><span class="sxs-lookup"><span data-stu-id="3ea1e-341">Additional information on signin cards</span></span>

<span data-ttu-id="3ea1e-342">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="3ea1e-342">Bot Framework reference:</span></span>

* [<span data-ttu-id="3ea1e-343">登录卡Node.js</span><span class="sxs-lookup"><span data-stu-id="3ea1e-343">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="3ea1e-344">登录卡 C#</span><span class="sxs-lookup"><span data-stu-id="3ea1e-344">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="3ea1e-345">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="3ea1e-345">Thumbnail card</span></span>

<span data-ttu-id="3ea1e-346">通常包含单个缩略图图像、一个或多个按钮和文本的卡片。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-346">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="3ea1e-347">对缩略图卡的支持</span><span class="sxs-lookup"><span data-stu-id="3ea1e-347">Support for thumbnail cards</span></span>

| <span data-ttu-id="3ea1e-348">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="3ea1e-348">Bots in Teams</span></span> | <span data-ttu-id="3ea1e-349">消息扩展</span><span class="sxs-lookup"><span data-stu-id="3ea1e-349">Messaging extensions</span></span>  | <span data-ttu-id="3ea1e-350">连接器</span><span class="sxs-lookup"><span data-stu-id="3ea1e-350">Connectors</span></span> | <span data-ttu-id="3ea1e-351">机器人框架</span><span class="sxs-lookup"><span data-stu-id="3ea1e-351">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ea1e-352">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-352">✔</span></span> | <span data-ttu-id="3ea1e-353">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-353">✔</span></span> | <span data-ttu-id="3ea1e-354">✖</span><span class="sxs-lookup"><span data-stu-id="3ea1e-354">✖</span></span> | <span data-ttu-id="3ea1e-355">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-355">✔</span></span> |

![缩略图卡片示例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="3ea1e-357">缩略图卡片的属性</span><span class="sxs-lookup"><span data-stu-id="3ea1e-357">Properties of a thumbnail card</span></span>

| <span data-ttu-id="3ea1e-358">属性</span><span class="sxs-lookup"><span data-stu-id="3ea1e-358">Property</span></span> | <span data-ttu-id="3ea1e-359">类型</span><span class="sxs-lookup"><span data-stu-id="3ea1e-359">Type</span></span>  | <span data-ttu-id="3ea1e-360">说明</span><span class="sxs-lookup"><span data-stu-id="3ea1e-360">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3ea1e-361">title</span><span class="sxs-lookup"><span data-stu-id="3ea1e-361">title</span></span> | <span data-ttu-id="3ea1e-362">格式文本 </span><span class="sxs-lookup"><span data-stu-id="3ea1e-362">Rich text</span></span> | <span data-ttu-id="3ea1e-363">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-363">Title of the card.</span></span> <span data-ttu-id="3ea1e-364">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-364">Maximum 2 lines.</span></span>|
| <span data-ttu-id="3ea1e-365">subtitle</span><span class="sxs-lookup"><span data-stu-id="3ea1e-365">subtitle</span></span> | <span data-ttu-id="3ea1e-366">格式文本 </span><span class="sxs-lookup"><span data-stu-id="3ea1e-366">Rich text</span></span> | <span data-ttu-id="3ea1e-367">卡片的副标题。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-367">Subtitle of the card.</span></span> <span data-ttu-id="3ea1e-368">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-368">Maximum 2 lines.</span></span>|
| <span data-ttu-id="3ea1e-369">text</span><span class="sxs-lookup"><span data-stu-id="3ea1e-369">text</span></span> | <span data-ttu-id="3ea1e-370">格式文本 </span><span class="sxs-lookup"><span data-stu-id="3ea1e-370">Rich text</span></span> | <span data-ttu-id="3ea1e-371">文本显示在副标题下。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-371">Text appears under the subtitle.</span></span> <span data-ttu-id="3ea1e-372">有关格式设置选项，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-372">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="3ea1e-373">images</span><span class="sxs-lookup"><span data-stu-id="3ea1e-373">images</span></span> | <span data-ttu-id="3ea1e-374">图像数组</span><span class="sxs-lookup"><span data-stu-id="3ea1e-374">Array of images</span></span> | <span data-ttu-id="3ea1e-375">显示在卡片顶部的图像。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-375">Image displayed at the top of the card.</span></span> <span data-ttu-id="3ea1e-376">纵横比 1：1 正方形。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-376">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="3ea1e-377">按钮</span><span class="sxs-lookup"><span data-stu-id="3ea1e-377">buttons</span></span> | <span data-ttu-id="3ea1e-378">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="3ea1e-378">Array of action objects</span></span> | <span data-ttu-id="3ea1e-379">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-379">Set of actions applicable to the current card.</span></span> <span data-ttu-id="3ea1e-380">最大值 6。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-380">Maximum 6.</span></span> |
| <span data-ttu-id="3ea1e-381">点击</span><span class="sxs-lookup"><span data-stu-id="3ea1e-381">tap</span></span> | <span data-ttu-id="3ea1e-382">Action 对象</span><span class="sxs-lookup"><span data-stu-id="3ea1e-382">Action object</span></span> | <span data-ttu-id="3ea1e-383">当用户点击卡片本身时激活。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-383">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="3ea1e-384">缩略图卡片示例</span><span class="sxs-lookup"><span data-stu-id="3ea1e-384">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="3ea1e-385">其他信息</span><span class="sxs-lookup"><span data-stu-id="3ea1e-385">Additional information</span></span>

<span data-ttu-id="3ea1e-386">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="3ea1e-386">Bot Framework reference:</span></span>

* [<span data-ttu-id="3ea1e-387">缩略图卡片Node.js</span><span class="sxs-lookup"><span data-stu-id="3ea1e-387">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="3ea1e-388">缩略图卡片 C#</span><span class="sxs-lookup"><span data-stu-id="3ea1e-388">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="3ea1e-389">卡片集合</span><span class="sxs-lookup"><span data-stu-id="3ea1e-389">Card collections</span></span>

<span data-ttu-id="3ea1e-390">Teams卡片集合。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-390">Teams supports Card collections.</span></span>

<span data-ttu-id="3ea1e-391">卡片集合包括 `builder.AttachmentLayout.carousel` `builder.AttachmentLayout.list` 和 。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-391">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="3ea1e-392">这些集合包含自适应、hero 或缩略图卡片。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-392">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="3ea1e-393">Carousel 集合</span><span class="sxs-lookup"><span data-stu-id="3ea1e-393">Carousel collection</span></span>

<span data-ttu-id="3ea1e-394">盘 [选布局](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) 显示卡片的盘选（可选）以及关联的操作按钮。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-394">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="3ea1e-395">支持木马集合</span><span class="sxs-lookup"><span data-stu-id="3ea1e-395">Support for carousel collections</span></span>

| <span data-ttu-id="3ea1e-396">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="3ea1e-396">Bots in Teams</span></span> | <span data-ttu-id="3ea1e-397">消息扩展</span><span class="sxs-lookup"><span data-stu-id="3ea1e-397">Messaging extensions</span></span>  | <span data-ttu-id="3ea1e-398">连接器</span><span class="sxs-lookup"><span data-stu-id="3ea1e-398">Connectors</span></span> | <span data-ttu-id="3ea1e-399">机器人框架</span><span class="sxs-lookup"><span data-stu-id="3ea1e-399">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ea1e-400">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-400">✔</span></span> | <span data-ttu-id="3ea1e-401">✖</span><span class="sxs-lookup"><span data-stu-id="3ea1e-401">✖</span></span> | <span data-ttu-id="3ea1e-402">✖</span><span class="sxs-lookup"><span data-stu-id="3ea1e-402">✖</span></span> | <span data-ttu-id="3ea1e-403">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-403">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="3ea1e-404">一个盘式消息最多可显示每封邮件 10 张卡片。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-404">A carousel can display a maximum of ten cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="3ea1e-405">单盘式卡片的属性</span><span class="sxs-lookup"><span data-stu-id="3ea1e-405">Properties of a carousel card</span></span>

<span data-ttu-id="3ea1e-406">单盘式播放卡片的属性与 hero 卡和缩略图卡片的属性相同。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-406">Properties of a carousel card are same as those of the hero and thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="3ea1e-407">一个木马集合的示例</span><span class="sxs-lookup"><span data-stu-id="3ea1e-407">Example of a carousel collection</span></span>

![卡片的盘点示例](~/assets/images/cards/carousel.png)

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="3ea1e-409">盘车集合的语法</span><span class="sxs-lookup"><span data-stu-id="3ea1e-409">Syntax for carousel collections</span></span>

<span data-ttu-id="3ea1e-410">`builder.AttachmentLayoutTypes.Carousel` 是木马集合的语法。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-410">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

## <a name="list-collection"></a><span data-ttu-id="3ea1e-411">列表集合</span><span class="sxs-lookup"><span data-stu-id="3ea1e-411">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="3ea1e-412">支持列表集合</span><span class="sxs-lookup"><span data-stu-id="3ea1e-412">Support for list collections</span></span>

<span data-ttu-id="3ea1e-413">列表布局显示卡片的垂直堆叠列表（可选）以及关联的操作按钮。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-413">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="3ea1e-414">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="3ea1e-414">Bots in Teams</span></span> | <span data-ttu-id="3ea1e-415">消息扩展</span><span class="sxs-lookup"><span data-stu-id="3ea1e-415">Messaging extensions</span></span>  | <span data-ttu-id="3ea1e-416">连接器</span><span class="sxs-lookup"><span data-stu-id="3ea1e-416">Connectors</span></span> | <span data-ttu-id="3ea1e-417">机器人框架</span><span class="sxs-lookup"><span data-stu-id="3ea1e-417">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="3ea1e-418">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-418">✔</span></span> | <span data-ttu-id="3ea1e-419">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-419">✔</span></span> | <span data-ttu-id="3ea1e-420">✖</span><span class="sxs-lookup"><span data-stu-id="3ea1e-420">✖</span></span> | <span data-ttu-id="3ea1e-421">✔</span><span class="sxs-lookup"><span data-stu-id="3ea1e-421">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="3ea1e-422">列表集合的示例</span><span class="sxs-lookup"><span data-stu-id="3ea1e-422">Example of a list collection</span></span>

![卡片列表示例](~/assets/images/cards/list.png)

<span data-ttu-id="3ea1e-424">属性与 hero 或 thumbnail 卡片的属性相同。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-424">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="3ea1e-425">列表最多可显示每封邮件 10 张卡片。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-425">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="3ea1e-426">iOS 和 Android 上尚不支持列表卡的一些组合。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-426">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="3ea1e-427">列表集合的语法</span><span class="sxs-lookup"><span data-stu-id="3ea1e-427">Syntax for list collections</span></span>

<span data-ttu-id="3ea1e-428">`builder.AttachmentLayout.list` 是列表集合的语法。</span><span class="sxs-lookup"><span data-stu-id="3ea1e-428">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="3ea1e-429">不支持的Teams</span><span class="sxs-lookup"><span data-stu-id="3ea1e-429">Cards not supported in Teams</span></span>

<span data-ttu-id="3ea1e-430">以下卡片由 Bot Framework 实现，但不受自动程序Teams：</span><span class="sxs-lookup"><span data-stu-id="3ea1e-430">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="3ea1e-431">动画卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-431">Animation cards</span></span>
* <span data-ttu-id="3ea1e-432">音频卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-432">Audio cards</span></span>
* <span data-ttu-id="3ea1e-433">视频卡</span><span class="sxs-lookup"><span data-stu-id="3ea1e-433">Video cards</span></span>
