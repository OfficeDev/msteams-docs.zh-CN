---
title: 卡参考
description: 介绍自动程序可用的所有卡片和Teams
localization_priority: Normal
keywords: 机器人卡参考
ms.topic: reference
ms.openlocfilehash: 741980ea79dd23659dd2b8a240d767b8292ca251
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994383"
---
# <a name="cards-reference"></a><span data-ttu-id="555b8-104">卡参考</span><span class="sxs-lookup"><span data-stu-id="555b8-104">Cards reference</span></span>

<span data-ttu-id="555b8-105">自动程序支持本文档中列出的Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="555b8-105">The cards listed in this document are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="555b8-106">它们基于 Bot Framework (BF) 定义的卡，Teams不支持所有 Bot Framework 卡，而是添加了Teams一些自动程序卡。</span><span class="sxs-lookup"><span data-stu-id="555b8-106">They are based on cards defined by the Bot Framework (BF), but Teams does not support all Bot Framework cards and instead some Teams cards have been added.</span></span> <span data-ttu-id="555b8-107">本文档的参考中已指出区别。</span><span class="sxs-lookup"><span data-stu-id="555b8-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="555b8-108">卡片示例</span><span class="sxs-lookup"><span data-stu-id="555b8-108">Card examples</span></span>

<span data-ttu-id="555b8-109">有关如何使用卡的其他信息，请参阅 Bot Builder SDK v3 的文档。</span><span class="sxs-lookup"><span data-stu-id="555b8-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK v3.</span></span> <span data-ttu-id="555b8-110">代码示例也可在 Microsoft/BotBuilder-Samples 存储库上GitHub。</span><span class="sxs-lookup"><span data-stu-id="555b8-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="555b8-111">.NET</span><span class="sxs-lookup"><span data-stu-id="555b8-111">.NET</span></span>
  * <span data-ttu-id="555b8-112">[将卡片添加为邮件的附件](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="555b8-112">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="555b8-113">[卡片示例代码自动程序生成器 v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards)。</span><span class="sxs-lookup"><span data-stu-id="555b8-113">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards).</span></span>

* <span data-ttu-id="555b8-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="555b8-114">Node.js</span></span>
  * <span data-ttu-id="555b8-115">[将卡片添加为邮件的附件](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="555b8-115">[Add cards as attachments to messages](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true).</span></span>
  * <span data-ttu-id="555b8-116">[卡片示例代码自动程序生成器 v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards)。</span><span class="sxs-lookup"><span data-stu-id="555b8-116">[Cards sample code Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards).</span></span>

## <a name="types-of-cards"></a><span data-ttu-id="555b8-117">卡片类型</span><span class="sxs-lookup"><span data-stu-id="555b8-117">Types of cards</span></span>

<span data-ttu-id="555b8-118">此表显示了可供你使用卡片的类型：</span><span class="sxs-lookup"><span data-stu-id="555b8-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="555b8-119">卡片类型</span><span class="sxs-lookup"><span data-stu-id="555b8-119">Card type</span></span> | <span data-ttu-id="555b8-120">说明</span><span class="sxs-lookup"><span data-stu-id="555b8-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="555b8-121">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="555b8-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="555b8-122">此卡片是可高度自定义的卡片，可以包含文本、语音、图像、按钮和输入字段的任意组合。</span><span class="sxs-lookup"><span data-stu-id="555b8-122">This card is highly customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> |
| [<span data-ttu-id="555b8-123">Hero card</span><span class="sxs-lookup"><span data-stu-id="555b8-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="555b8-124">此卡片通常包含一个大图像、一个或多个按钮和少量文本。</span><span class="sxs-lookup"><span data-stu-id="555b8-124">This card typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="555b8-125">列表卡</span><span class="sxs-lookup"><span data-stu-id="555b8-125">List card</span></span>](#list-card) | <span data-ttu-id="555b8-126">此卡片是项的滚动列表。</span><span class="sxs-lookup"><span data-stu-id="555b8-126">This card is a scrolling list of items.</span></span> |
| [<span data-ttu-id="555b8-127">Office 365连接器卡</span><span class="sxs-lookup"><span data-stu-id="555b8-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="555b8-128">此卡片具有具有多个分区、字段、图像和操作的灵活性布局。</span><span class="sxs-lookup"><span data-stu-id="555b8-128">This card has a flexible layout with multiple sections, fields, images, and actions.</span></span> |
| [<span data-ttu-id="555b8-129">收据卡</span><span class="sxs-lookup"><span data-stu-id="555b8-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="555b8-130">此卡为用户提供收据。</span><span class="sxs-lookup"><span data-stu-id="555b8-130">This card provides a receipt to the user.</span></span> |
| [<span data-ttu-id="555b8-131">登录卡</span><span class="sxs-lookup"><span data-stu-id="555b8-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="555b8-132">此卡使机器人可以请求用户登录。</span><span class="sxs-lookup"><span data-stu-id="555b8-132">This card enables a bot to request that a user signs in.</span></span> |
| [<span data-ttu-id="555b8-133">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="555b8-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="555b8-134">此卡片通常包含一个缩略图图像、一些短文本以及一个或多个按钮。</span><span class="sxs-lookup"><span data-stu-id="555b8-134">This card typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="555b8-135">卡片集合</span><span class="sxs-lookup"><span data-stu-id="555b8-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="555b8-136">此卡片用于在单个响应中返回多个项目。</span><span class="sxs-lookup"><span data-stu-id="555b8-136">This cards is used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="555b8-137">所有卡片的常见属性</span><span class="sxs-lookup"><span data-stu-id="555b8-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="555b8-138">内联卡片图像</span><span class="sxs-lookup"><span data-stu-id="555b8-138">Inline card images</span></span>

<span data-ttu-id="555b8-139">卡片可以包含内联图像，包括指向公开可用图像的链接。</span><span class="sxs-lookup"><span data-stu-id="555b8-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="555b8-140">出于性能目的，强烈建议您将映像托管在公共内容交付网络或 (CDN) 。</span><span class="sxs-lookup"><span data-stu-id="555b8-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="555b8-141">在保持纵横比以覆盖图像区域的同时，图像大小会向上或向下扩展。</span><span class="sxs-lookup"><span data-stu-id="555b8-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area.</span></span> <span data-ttu-id="555b8-142">然后从中心裁剪图像，以实现卡片的适当纵横比。</span><span class="sxs-lookup"><span data-stu-id="555b8-142">Images are then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="555b8-143">图像必须最多为 1024×1024 PNG、JPEG 或 GIF 格式，并且不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="555b8-143">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and do not support animated GIF.</span></span>

| <span data-ttu-id="555b8-144">属性</span><span class="sxs-lookup"><span data-stu-id="555b8-144">Property</span></span> | <span data-ttu-id="555b8-145">类型</span><span class="sxs-lookup"><span data-stu-id="555b8-145">Type</span></span>  | <span data-ttu-id="555b8-146">说明</span><span class="sxs-lookup"><span data-stu-id="555b8-146">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555b8-147">url</span><span class="sxs-lookup"><span data-stu-id="555b8-147">url</span></span> | <span data-ttu-id="555b8-148">URL</span><span class="sxs-lookup"><span data-stu-id="555b8-148">URL</span></span> | <span data-ttu-id="555b8-149">图像的 HTTPS URL。</span><span class="sxs-lookup"><span data-stu-id="555b8-149">HTTPS URL to the image.</span></span> |
| <span data-ttu-id="555b8-150">alt</span><span class="sxs-lookup"><span data-stu-id="555b8-150">alt</span></span> | <span data-ttu-id="555b8-151">String</span><span class="sxs-lookup"><span data-stu-id="555b8-151">String</span></span> | <span data-ttu-id="555b8-152">图像的辅助说明。</span><span class="sxs-lookup"><span data-stu-id="555b8-152">Accessible description of the image.</span></span> |

> [!NOTE]
> <span data-ttu-id="555b8-153">如果卡片包含的图像 URL 在最终图像之前经过重定向，则不支持图像 URL 中的重定向。</span><span class="sxs-lookup"><span data-stu-id="555b8-153">If a card includes an image URL that goes through a redirect before the final image, the redirect in image URL is not supported.</span></span> <span data-ttu-id="555b8-154">对于在公有云上共享的图像，会出现此情况。</span><span class="sxs-lookup"><span data-stu-id="555b8-154">This occurs for images shared on the public cloud.</span></span>

### <a name="buttons"></a><span data-ttu-id="555b8-155">按钮</span><span class="sxs-lookup"><span data-stu-id="555b8-155">Buttons</span></span>

<span data-ttu-id="555b8-156">按钮显示在卡片底部堆叠。</span><span class="sxs-lookup"><span data-stu-id="555b8-156">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="555b8-157">按钮文本始终位于单行，如果文本超过按钮宽度，则将被截断。</span><span class="sxs-lookup"><span data-stu-id="555b8-157">Button text is always on a single line and is truncated if the text exceeds the button width.</span></span> <span data-ttu-id="555b8-158">不会显示超过卡支持的最大数目的其他任何按钮。</span><span class="sxs-lookup"><span data-stu-id="555b8-158">Any additional buttons beyond the maximum number supported by the card are not shown.</span></span>

<span data-ttu-id="555b8-159">有关详细信息，请参阅 [卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="555b8-159">For more information, see [card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

### <a name="card-formatting"></a><span data-ttu-id="555b8-160">卡片格式</span><span class="sxs-lookup"><span data-stu-id="555b8-160">Card formatting</span></span>

<span data-ttu-id="555b8-161">有关卡片中的文本格式设置详细信息，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="555b8-161">For more information on text formatting in cards, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="555b8-162">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="555b8-162">Adaptive card</span></span>

<span data-ttu-id="555b8-163">自适应卡片是可自定义的卡片，可以包含文本、语音、图像、按钮和输入字段的任意组合。</span><span class="sxs-lookup"><span data-stu-id="555b8-163">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="555b8-164">有关详细信息，请参阅[自适应卡片 v1.2.0。](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)</span><span class="sxs-lookup"><span data-stu-id="555b8-164">For more information, see [adaptive cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="555b8-165">自适应卡片支持</span><span class="sxs-lookup"><span data-stu-id="555b8-165">Support for adaptive cards</span></span>

| <span data-ttu-id="555b8-166">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="555b8-166">Bots in Teams</span></span> | <span data-ttu-id="555b8-167">消息扩展</span><span class="sxs-lookup"><span data-stu-id="555b8-167">Messaging extensions</span></span>  | <span data-ttu-id="555b8-168">连接器</span><span class="sxs-lookup"><span data-stu-id="555b8-168">Connectors</span></span> | <span data-ttu-id="555b8-169">机器人框架</span><span class="sxs-lookup"><span data-stu-id="555b8-169">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555b8-170">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-170">✔</span></span> | <span data-ttu-id="555b8-171">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-171">✔</span></span> | <span data-ttu-id="555b8-172">✖</span><span class="sxs-lookup"><span data-stu-id="555b8-172">✖</span></span> | <span data-ttu-id="555b8-173">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-173">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="555b8-174">Teams平台支持 v1.2 或更早的自适应卡片功能。</span><span class="sxs-lookup"><span data-stu-id="555b8-174">Teams platform supports v1.2 or earlier of adaptive card features.</span></span>
> * <span data-ttu-id="555b8-175">在游戏平台上的自适应卡片中不支持正面或破坏性Teams样式。</span><span class="sxs-lookup"><span data-stu-id="555b8-175">Positive or destructive action styling is not supported in Adaptive Cards on the Teams platform.</span></span>
> * <span data-ttu-id="555b8-176">媒体元素当前在 Teams 平台上的自适应卡片中不受支持。</span><span class="sxs-lookup"><span data-stu-id="555b8-176">Media elements are currently not supported in Adaptive Cards on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="555b8-177">自适应卡片示例</span><span class="sxs-lookup"><span data-stu-id="555b8-177">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="555b8-179">自适应卡片的其他信息</span><span class="sxs-lookup"><span data-stu-id="555b8-179">Additional information on adaptive cards</span></span>

<span data-ttu-id="555b8-180">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="555b8-180">Bot Framework reference:</span></span>

* [<span data-ttu-id="555b8-181">自适应卡片Node.js</span><span class="sxs-lookup"><span data-stu-id="555b8-181">Adaptive cards Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="555b8-182">自适应卡片 C#</span><span class="sxs-lookup"><span data-stu-id="555b8-182">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="555b8-183">Hero card</span><span class="sxs-lookup"><span data-stu-id="555b8-183">Hero card</span></span>

<span data-ttu-id="555b8-184">通常包含单个大图像、一个或多个按钮和文本的卡片。</span><span class="sxs-lookup"><span data-stu-id="555b8-184">A card that typically contains a single large image, one or more buttons, and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="555b8-185">支持人物卡片</span><span class="sxs-lookup"><span data-stu-id="555b8-185">Support for hero cards</span></span>

| <span data-ttu-id="555b8-186">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="555b8-186">Bots in Teams</span></span> | <span data-ttu-id="555b8-187">消息扩展</span><span class="sxs-lookup"><span data-stu-id="555b8-187">Messaging extensions</span></span>  | <span data-ttu-id="555b8-188">连接器</span><span class="sxs-lookup"><span data-stu-id="555b8-188">Connectors</span></span> | <span data-ttu-id="555b8-189">机器人框架</span><span class="sxs-lookup"><span data-stu-id="555b8-189">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555b8-190">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-190">✔</span></span> | <span data-ttu-id="555b8-191">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-191">✔</span></span> | <span data-ttu-id="555b8-192">✖</span><span class="sxs-lookup"><span data-stu-id="555b8-192">✖</span></span> | <span data-ttu-id="555b8-193">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-193">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="555b8-194">Hero 卡片的属性</span><span class="sxs-lookup"><span data-stu-id="555b8-194">Properties of a hero card</span></span>

| <span data-ttu-id="555b8-195">属性</span><span class="sxs-lookup"><span data-stu-id="555b8-195">Property</span></span> | <span data-ttu-id="555b8-196">类型</span><span class="sxs-lookup"><span data-stu-id="555b8-196">Type</span></span>  | <span data-ttu-id="555b8-197">说明</span><span class="sxs-lookup"><span data-stu-id="555b8-197">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555b8-198">title</span><span class="sxs-lookup"><span data-stu-id="555b8-198">title</span></span> | <span data-ttu-id="555b8-199">格式文本 </span><span class="sxs-lookup"><span data-stu-id="555b8-199">Rich text</span></span> | <span data-ttu-id="555b8-200">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="555b8-200">Title of the card.</span></span> <span data-ttu-id="555b8-201">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="555b8-201">Maximum 2 lines.</span></span> |
| <span data-ttu-id="555b8-202">subtitle</span><span class="sxs-lookup"><span data-stu-id="555b8-202">subtitle</span></span> | <span data-ttu-id="555b8-203">格式文本 </span><span class="sxs-lookup"><span data-stu-id="555b8-203">Rich text</span></span> | <span data-ttu-id="555b8-204">卡片的副标题。</span><span class="sxs-lookup"><span data-stu-id="555b8-204">Subtitle of the card.</span></span> <span data-ttu-id="555b8-205">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="555b8-205">Maximum 2 lines.</span></span>|
| <span data-ttu-id="555b8-206">text</span><span class="sxs-lookup"><span data-stu-id="555b8-206">text</span></span> | <span data-ttu-id="555b8-207">格式文本 </span><span class="sxs-lookup"><span data-stu-id="555b8-207">Rich text</span></span> | <span data-ttu-id="555b8-208">文本显示在副标题下。</span><span class="sxs-lookup"><span data-stu-id="555b8-208">Text appears under the subtitle.</span></span> <span data-ttu-id="555b8-209">有关格式设置选项，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="555b8-209">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="555b8-210">images</span><span class="sxs-lookup"><span data-stu-id="555b8-210">images</span></span> | <span data-ttu-id="555b8-211">图像数组</span><span class="sxs-lookup"><span data-stu-id="555b8-211">Array of images</span></span> | <span data-ttu-id="555b8-212">显示在卡片顶部的图像。</span><span class="sxs-lookup"><span data-stu-id="555b8-212">Image displayed at the top of the card.</span></span> <span data-ttu-id="555b8-213">纵横比 16：9。</span><span class="sxs-lookup"><span data-stu-id="555b8-213">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="555b8-214">按钮</span><span class="sxs-lookup"><span data-stu-id="555b8-214">buttons</span></span> | <span data-ttu-id="555b8-215">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="555b8-215">Array of action objects</span></span> | <span data-ttu-id="555b8-216">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="555b8-216">Set of actions applicable to the current card.</span></span> <span data-ttu-id="555b8-217">最大值 6。</span><span class="sxs-lookup"><span data-stu-id="555b8-217">Maximum 6.</span></span> |
| <span data-ttu-id="555b8-218">点击</span><span class="sxs-lookup"><span data-stu-id="555b8-218">tap</span></span> | <span data-ttu-id="555b8-219">Action 对象</span><span class="sxs-lookup"><span data-stu-id="555b8-219">Action object</span></span> | <span data-ttu-id="555b8-220">当用户点击卡片本身时激活。</span><span class="sxs-lookup"><span data-stu-id="555b8-220">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="555b8-221">Hero 卡片示例</span><span class="sxs-lookup"><span data-stu-id="555b8-221">Example of a hero card</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="555b8-223">有关 hero cards 的其他信息</span><span class="sxs-lookup"><span data-stu-id="555b8-223">Additional information on hero cards</span></span>

<span data-ttu-id="555b8-224">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="555b8-224">Bot Framework reference:</span></span>

* [<span data-ttu-id="555b8-225">Hero card Node.js</span><span class="sxs-lookup"><span data-stu-id="555b8-225">Hero card Node.js</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="555b8-226">Hero card C#</span><span class="sxs-lookup"><span data-stu-id="555b8-226">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="555b8-227">列表卡</span><span class="sxs-lookup"><span data-stu-id="555b8-227">List card</span></span>

<span data-ttu-id="555b8-228">列表卡片已由列表Teams，以提供列表集合可以提供的功能之外的功能。</span><span class="sxs-lookup"><span data-stu-id="555b8-228">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="555b8-229">列表卡片提供项的滚动列表。</span><span class="sxs-lookup"><span data-stu-id="555b8-229">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="555b8-230">支持列表卡</span><span class="sxs-lookup"><span data-stu-id="555b8-230">Support for list cards</span></span>

| <span data-ttu-id="555b8-231">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="555b8-231">Bots in Teams</span></span> | <span data-ttu-id="555b8-232">消息扩展</span><span class="sxs-lookup"><span data-stu-id="555b8-232">Messaging extensions</span></span>  | <span data-ttu-id="555b8-233">连接器</span><span class="sxs-lookup"><span data-stu-id="555b8-233">Connectors</span></span> | <span data-ttu-id="555b8-234">机器人框架</span><span class="sxs-lookup"><span data-stu-id="555b8-234">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555b8-235">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-235">✔</span></span> | <span data-ttu-id="555b8-236">✖</span><span class="sxs-lookup"><span data-stu-id="555b8-236">✖</span></span> | <span data-ttu-id="555b8-237">✖</span><span class="sxs-lookup"><span data-stu-id="555b8-237">✖</span></span> |<span data-ttu-id="555b8-238">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-238">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="555b8-239">列表卡片的属性</span><span class="sxs-lookup"><span data-stu-id="555b8-239">Properties of a list card</span></span>

| <span data-ttu-id="555b8-240">属性</span><span class="sxs-lookup"><span data-stu-id="555b8-240">Property</span></span> | <span data-ttu-id="555b8-241">类型</span><span class="sxs-lookup"><span data-stu-id="555b8-241">Type</span></span>  | <span data-ttu-id="555b8-242">说明</span><span class="sxs-lookup"><span data-stu-id="555b8-242">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555b8-243">title</span><span class="sxs-lookup"><span data-stu-id="555b8-243">title</span></span> | <span data-ttu-id="555b8-244">格式文本 </span><span class="sxs-lookup"><span data-stu-id="555b8-244">Rich text</span></span> | <span data-ttu-id="555b8-245">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="555b8-245">Title of the card.</span></span> <span data-ttu-id="555b8-246">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="555b8-246">Maximum 2 lines.</span></span>|
| <span data-ttu-id="555b8-247">项目</span><span class="sxs-lookup"><span data-stu-id="555b8-247">items</span></span> | <span data-ttu-id="555b8-248">列表项数组</span><span class="sxs-lookup"><span data-stu-id="555b8-248">Array of list items</span></span> ||
| <span data-ttu-id="555b8-249">按钮</span><span class="sxs-lookup"><span data-stu-id="555b8-249">buttons</span></span> | <span data-ttu-id="555b8-250">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="555b8-250">Array of action objects</span></span> | <span data-ttu-id="555b8-251">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="555b8-251">Set of actions applicable to the current card.</span></span> <span data-ttu-id="555b8-252">最大值 6。</span><span class="sxs-lookup"><span data-stu-id="555b8-252">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="555b8-253">列表卡片示例</span><span class="sxs-lookup"><span data-stu-id="555b8-253">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="555b8-254">Office 365连接器卡</span><span class="sxs-lookup"><span data-stu-id="555b8-254">Office 365 connector card</span></span>

<span data-ttu-id="555b8-255">自动Office 365支持自动Teams，而不是 Bot Framework。</span><span class="sxs-lookup"><span data-stu-id="555b8-255">The Office 365 connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="555b8-256">此卡片提供具有多个分区、字段、图像和操作的灵活性布局。</span><span class="sxs-lookup"><span data-stu-id="555b8-256">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="555b8-257">此卡封装连接器卡，以便机器人可以使用它。</span><span class="sxs-lookup"><span data-stu-id="555b8-257">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="555b8-258">有关连接器卡和 O365 卡之间的差异，请参阅连接器卡[上的Office 365注释](#notes-on-the-office-365-connector-card)。</span><span class="sxs-lookup"><span data-stu-id="555b8-258">For differences between connector cards and the O365 card, see [Notes on the Office 365 connector card](#notes-on-the-office-365-connector-card).</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="555b8-259">支持 Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="555b8-259">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="555b8-260">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="555b8-260">Bots in Teams</span></span> | <span data-ttu-id="555b8-261">消息扩展</span><span class="sxs-lookup"><span data-stu-id="555b8-261">Messaging extensions</span></span>  | <span data-ttu-id="555b8-262">连接器</span><span class="sxs-lookup"><span data-stu-id="555b8-262">Connectors</span></span> | <span data-ttu-id="555b8-263">机器人框架</span><span class="sxs-lookup"><span data-stu-id="555b8-263">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555b8-264">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-264">✔</span></span> | <span data-ttu-id="555b8-265">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-265">✔</span></span> | <span data-ttu-id="555b8-266">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-266">✔</span></span> | <span data-ttu-id="555b8-267">✖</span><span class="sxs-lookup"><span data-stu-id="555b8-267">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="555b8-268">连接器Office 365的属性</span><span class="sxs-lookup"><span data-stu-id="555b8-268">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="555b8-269">属性</span><span class="sxs-lookup"><span data-stu-id="555b8-269">Property</span></span> | <span data-ttu-id="555b8-270">类型</span><span class="sxs-lookup"><span data-stu-id="555b8-270">Type</span></span>  | <span data-ttu-id="555b8-271">说明</span><span class="sxs-lookup"><span data-stu-id="555b8-271">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555b8-272">title</span><span class="sxs-lookup"><span data-stu-id="555b8-272">title</span></span> | <span data-ttu-id="555b8-273">格式文本 </span><span class="sxs-lookup"><span data-stu-id="555b8-273">Rich text</span></span> | <span data-ttu-id="555b8-274">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="555b8-274">Title of the card.</span></span> <span data-ttu-id="555b8-275">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="555b8-275">Maximum 2 lines.</span></span> |
| <span data-ttu-id="555b8-276">摘要</span><span class="sxs-lookup"><span data-stu-id="555b8-276">summary</span></span> | <span data-ttu-id="555b8-277">格式文本 </span><span class="sxs-lookup"><span data-stu-id="555b8-277">Rich text</span></span> | <span data-ttu-id="555b8-278">卡片摘要。</span><span class="sxs-lookup"><span data-stu-id="555b8-278">Summary of the card.</span></span> <span data-ttu-id="555b8-279">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="555b8-279">Maximum 2 lines.</span></span> |
| <span data-ttu-id="555b8-280">text</span><span class="sxs-lookup"><span data-stu-id="555b8-280">text</span></span> | <span data-ttu-id="555b8-281">格式文本 </span><span class="sxs-lookup"><span data-stu-id="555b8-281">Rich text</span></span> | <span data-ttu-id="555b8-282">文本显示在副标题下。</span><span class="sxs-lookup"><span data-stu-id="555b8-282">Text appears under the subtitle.</span></span> <span data-ttu-id="555b8-283">有关格式设置选项，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="555b8-283">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="555b8-284">themeColor</span><span class="sxs-lookup"><span data-stu-id="555b8-284">themeColor</span></span> | <span data-ttu-id="555b8-285">十六进制字符串</span><span class="sxs-lookup"><span data-stu-id="555b8-285">HEX string</span></span> | <span data-ttu-id="555b8-286">替代应用程序清单中提供的 accentColor 的颜色。</span><span class="sxs-lookup"><span data-stu-id="555b8-286">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="555b8-287">连接器卡Office 365备注</span><span class="sxs-lookup"><span data-stu-id="555b8-287">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="555b8-288">Office 365连接器卡在 Microsoft Teams中正常工作，包括[ActionCard 操作](/outlook/actionable-messages/card-reference#actioncard-action)。</span><span class="sxs-lookup"><span data-stu-id="555b8-288">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="555b8-289">从连接器使用连接器卡和在机器人中使用连接器卡之间的一个重要区别是处理卡操作。</span><span class="sxs-lookup"><span data-stu-id="555b8-289">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="555b8-290">对于连接器，终结点通过 HTTP POST 接收卡有效负载。</span><span class="sxs-lookup"><span data-stu-id="555b8-290">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="555b8-291">对于自动程序，该操作将触发仅向自动程序发送操作 ID 和 `HttpPOST` `invoke` 正文的活动。</span><span class="sxs-lookup"><span data-stu-id="555b8-291">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="555b8-292">每个连接器卡最多可以显示 10 个部分，每个部分最多可以包含 5 个图像和 5 个操作。</span><span class="sxs-lookup"><span data-stu-id="555b8-292">Each connector card can display a maximum of ten sections, and each section can contain a maximum of five images and five actions.</span></span>

> [!NOTE]
> <span data-ttu-id="555b8-293">邮件中不显示任何其他节、图像或操作。</span><span class="sxs-lookup"><span data-stu-id="555b8-293">Any additional sections, images, or actions in a message do not appear.</span></span>

<span data-ttu-id="555b8-294">所有文本字段都支持 markdown 和 HTML。</span><span class="sxs-lookup"><span data-stu-id="555b8-294">All text fields support markdown and HTML.</span></span> <span data-ttu-id="555b8-295">您可以通过在邮件中设置 属性来控制使用 markdown 或 HTML `markdown` 的部分。</span><span class="sxs-lookup"><span data-stu-id="555b8-295">You can control which sections use markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="555b8-296">默认情况下， `markdown` 设置为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="555b8-296">By default, `markdown` is set to `true`.</span></span> <span data-ttu-id="555b8-297">如果要改为使用 HTML，请设置为 `markdown` `false` 。</span><span class="sxs-lookup"><span data-stu-id="555b8-297">If you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="555b8-298">如果指定 `themeColor` 属性，它将替代 `accentColor` 应用清单中的 属性。</span><span class="sxs-lookup"><span data-stu-id="555b8-298">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="555b8-299">若要指定 的呈现样式 `activityImage` ，可以按 `activityImageType` 如下方式设置：</span><span class="sxs-lookup"><span data-stu-id="555b8-299">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="555b8-300">值</span><span class="sxs-lookup"><span data-stu-id="555b8-300">Value</span></span> | <span data-ttu-id="555b8-301">说明</span><span class="sxs-lookup"><span data-stu-id="555b8-301">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="555b8-302">默认值; `activityImage` 裁剪为圆形。</span><span class="sxs-lookup"><span data-stu-id="555b8-302">Default; `activityImage` is cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="555b8-303">`activityImage` 显示为矩形并保留其纵横比。</span><span class="sxs-lookup"><span data-stu-id="555b8-303">`activityImage` is displayed as a rectangle and retains its aspect ratio.</span></span> |

<span data-ttu-id="555b8-304">有关连接器卡属性的所有其他详细信息，请参阅 [可操作邮件卡参考](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="555b8-304">For all other details about connector card properties, see [actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="555b8-305">当前不支持的唯Microsoft Teams连接器卡属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="555b8-305">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="555b8-306">`startGroup`始终视为 `true` 在Teams</span><span class="sxs-lookup"><span data-stu-id="555b8-306">`startGroup` always treated as `true` in Teams</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="555b8-307">连接Office 365示例</span><span class="sxs-lookup"><span data-stu-id="555b8-307">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="555b8-308">收据卡</span><span class="sxs-lookup"><span data-stu-id="555b8-308">Receipt card</span></span>

<span data-ttu-id="555b8-309">Teams支持收据卡。</span><span class="sxs-lookup"><span data-stu-id="555b8-309">Teams supports receipt card.</span></span> <span data-ttu-id="555b8-310">它是使机器人能够为用户提供收据的卡片。</span><span class="sxs-lookup"><span data-stu-id="555b8-310">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="555b8-311">它通常包含要包含在收据上的项目列表，如税务和总信息。</span><span class="sxs-lookup"><span data-stu-id="555b8-311">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="555b8-312">支持收据卡</span><span class="sxs-lookup"><span data-stu-id="555b8-312">Support for receipt cards</span></span>

| <span data-ttu-id="555b8-313">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="555b8-313">Bots in Teams</span></span> | <span data-ttu-id="555b8-314">消息扩展</span><span class="sxs-lookup"><span data-stu-id="555b8-314">Messaging extensions</span></span>  | <span data-ttu-id="555b8-315">连接器</span><span class="sxs-lookup"><span data-stu-id="555b8-315">Connectors</span></span> | <span data-ttu-id="555b8-316">机器人框架</span><span class="sxs-lookup"><span data-stu-id="555b8-316">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555b8-317">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-317">✔</span></span> | <span data-ttu-id="555b8-318">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-318">✔</span></span> | <span data-ttu-id="555b8-319">✖</span><span class="sxs-lookup"><span data-stu-id="555b8-319">✖</span></span> | <span data-ttu-id="555b8-320">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-320">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="555b8-321">收据卡示例</span><span class="sxs-lookup"><span data-stu-id="555b8-321">Example of a receipt card</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="555b8-323">收据卡上的其他信息</span><span class="sxs-lookup"><span data-stu-id="555b8-323">Additional information on receipt cards</span></span>

<span data-ttu-id="555b8-324">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="555b8-324">Bot Framework reference:</span></span>

* [<span data-ttu-id="555b8-325">收据卡Node.js</span><span class="sxs-lookup"><span data-stu-id="555b8-325">Receipt card Node.js</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="555b8-326">收据卡 C#</span><span class="sxs-lookup"><span data-stu-id="555b8-326">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="555b8-327">登录卡</span><span class="sxs-lookup"><span data-stu-id="555b8-327">Signin card</span></span>

<span data-ttu-id="555b8-328">登录卡使机器人可以请求用户登录。</span><span class="sxs-lookup"><span data-stu-id="555b8-328">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="555b8-329">在自动Teams中支持它，其形式与 Bot Framework 中略有不同。</span><span class="sxs-lookup"><span data-stu-id="555b8-329">It is supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="555b8-330">自动Teams中的登录卡类似于 Bot 框架中的登录卡，只不过 Teams 中的登录卡仅支持两个操作： 和 `signin` `openUrl` 。</span><span class="sxs-lookup"><span data-stu-id="555b8-330">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="555b8-331">登录操作可以从登录卡Teams，而不只是从登录卡使用。</span><span class="sxs-lookup"><span data-stu-id="555b8-331">The signin action can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="555b8-332">有关身份验证详细信息，请参阅自动[Microsoft Teams的身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="555b8-332">For more information on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="555b8-333">支持登录卡</span><span class="sxs-lookup"><span data-stu-id="555b8-333">Support for signin cards</span></span>

| <span data-ttu-id="555b8-334">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="555b8-334">Bots in Teams</span></span> | <span data-ttu-id="555b8-335">消息扩展</span><span class="sxs-lookup"><span data-stu-id="555b8-335">Messaging extensions</span></span>  | <span data-ttu-id="555b8-336">连接器</span><span class="sxs-lookup"><span data-stu-id="555b8-336">Connectors</span></span> | <span data-ttu-id="555b8-337">机器人框架</span><span class="sxs-lookup"><span data-stu-id="555b8-337">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555b8-338">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-338">✔</span></span> | <span data-ttu-id="555b8-339">✖</span><span class="sxs-lookup"><span data-stu-id="555b8-339">✖</span></span> | <span data-ttu-id="555b8-340">✖</span><span class="sxs-lookup"><span data-stu-id="555b8-340">✖</span></span> | <span data-ttu-id="555b8-341">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-341">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="555b8-342">登录卡的其他信息</span><span class="sxs-lookup"><span data-stu-id="555b8-342">Additional information on signin cards</span></span>

<span data-ttu-id="555b8-343">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="555b8-343">Bot Framework reference:</span></span>

* [<span data-ttu-id="555b8-344">登录卡Node.js</span><span class="sxs-lookup"><span data-stu-id="555b8-344">Signin card Node.js</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="555b8-345">登录卡 C#</span><span class="sxs-lookup"><span data-stu-id="555b8-345">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="555b8-346">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="555b8-346">Thumbnail card</span></span>

<span data-ttu-id="555b8-347">通常包含单个缩略图图像、一个或多个按钮和文本的卡片。</span><span class="sxs-lookup"><span data-stu-id="555b8-347">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="555b8-348">对缩略图卡的支持</span><span class="sxs-lookup"><span data-stu-id="555b8-348">Support for thumbnail cards</span></span>

| <span data-ttu-id="555b8-349">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="555b8-349">Bots in Teams</span></span> | <span data-ttu-id="555b8-350">消息扩展</span><span class="sxs-lookup"><span data-stu-id="555b8-350">Messaging extensions</span></span>  | <span data-ttu-id="555b8-351">连接器</span><span class="sxs-lookup"><span data-stu-id="555b8-351">Connectors</span></span> | <span data-ttu-id="555b8-352">机器人框架</span><span class="sxs-lookup"><span data-stu-id="555b8-352">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555b8-353">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-353">✔</span></span> | <span data-ttu-id="555b8-354">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-354">✔</span></span> | <span data-ttu-id="555b8-355">✖</span><span class="sxs-lookup"><span data-stu-id="555b8-355">✖</span></span> | <span data-ttu-id="555b8-356">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-356">✔</span></span> |

![缩略图卡片示例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="555b8-358">缩略图卡片的属性</span><span class="sxs-lookup"><span data-stu-id="555b8-358">Properties of a thumbnail card</span></span>

| <span data-ttu-id="555b8-359">属性</span><span class="sxs-lookup"><span data-stu-id="555b8-359">Property</span></span> | <span data-ttu-id="555b8-360">类型</span><span class="sxs-lookup"><span data-stu-id="555b8-360">Type</span></span>  | <span data-ttu-id="555b8-361">说明</span><span class="sxs-lookup"><span data-stu-id="555b8-361">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="555b8-362">title</span><span class="sxs-lookup"><span data-stu-id="555b8-362">title</span></span> | <span data-ttu-id="555b8-363">格式文本 </span><span class="sxs-lookup"><span data-stu-id="555b8-363">Rich text</span></span> | <span data-ttu-id="555b8-364">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="555b8-364">Title of the card.</span></span> <span data-ttu-id="555b8-365">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="555b8-365">Maximum 2 lines.</span></span>|
| <span data-ttu-id="555b8-366">subtitle</span><span class="sxs-lookup"><span data-stu-id="555b8-366">subtitle</span></span> | <span data-ttu-id="555b8-367">格式文本 </span><span class="sxs-lookup"><span data-stu-id="555b8-367">Rich text</span></span> | <span data-ttu-id="555b8-368">卡片的副标题。</span><span class="sxs-lookup"><span data-stu-id="555b8-368">Subtitle of the card.</span></span> <span data-ttu-id="555b8-369">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="555b8-369">Maximum 2 lines.</span></span>|
| <span data-ttu-id="555b8-370">text</span><span class="sxs-lookup"><span data-stu-id="555b8-370">text</span></span> | <span data-ttu-id="555b8-371">格式文本 </span><span class="sxs-lookup"><span data-stu-id="555b8-371">Rich text</span></span> | <span data-ttu-id="555b8-372">文本显示在副标题下。</span><span class="sxs-lookup"><span data-stu-id="555b8-372">Text appears under the subtitle.</span></span> <span data-ttu-id="555b8-373">有关格式设置选项，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="555b8-373">For formatting options, see [card formatting](~/task-modules-and-cards/cards/cards-format.md).</span></span> |
| <span data-ttu-id="555b8-374">images</span><span class="sxs-lookup"><span data-stu-id="555b8-374">images</span></span> | <span data-ttu-id="555b8-375">图像数组</span><span class="sxs-lookup"><span data-stu-id="555b8-375">Array of images</span></span> | <span data-ttu-id="555b8-376">显示在卡片顶部的图像。</span><span class="sxs-lookup"><span data-stu-id="555b8-376">Image displayed at the top of the card.</span></span> <span data-ttu-id="555b8-377">纵横比 1：1 正方形。</span><span class="sxs-lookup"><span data-stu-id="555b8-377">Aspect ratio 1:1 square.</span></span> |
| <span data-ttu-id="555b8-378">按钮</span><span class="sxs-lookup"><span data-stu-id="555b8-378">buttons</span></span> | <span data-ttu-id="555b8-379">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="555b8-379">Array of action objects</span></span> | <span data-ttu-id="555b8-380">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="555b8-380">Set of actions applicable to the current card.</span></span> <span data-ttu-id="555b8-381">最大值 6。</span><span class="sxs-lookup"><span data-stu-id="555b8-381">Maximum 6.</span></span> |
| <span data-ttu-id="555b8-382">点击</span><span class="sxs-lookup"><span data-stu-id="555b8-382">tap</span></span> | <span data-ttu-id="555b8-383">Action 对象</span><span class="sxs-lookup"><span data-stu-id="555b8-383">Action object</span></span> | <span data-ttu-id="555b8-384">当用户点击卡片本身时激活。</span><span class="sxs-lookup"><span data-stu-id="555b8-384">Activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="555b8-385">缩略图卡片示例</span><span class="sxs-lookup"><span data-stu-id="555b8-385">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="555b8-386">其他信息</span><span class="sxs-lookup"><span data-stu-id="555b8-386">Additional information</span></span>

<span data-ttu-id="555b8-387">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="555b8-387">Bot Framework reference:</span></span>

* [<span data-ttu-id="555b8-388">缩略图卡片Node.js</span><span class="sxs-lookup"><span data-stu-id="555b8-388">Thumbnail card Node.js</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="555b8-389">缩略图卡片 C#</span><span class="sxs-lookup"><span data-stu-id="555b8-389">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="555b8-390">卡片集合</span><span class="sxs-lookup"><span data-stu-id="555b8-390">Card collections</span></span>

<span data-ttu-id="555b8-391">Teams卡片集合。</span><span class="sxs-lookup"><span data-stu-id="555b8-391">Teams supports Card collections.</span></span>

<span data-ttu-id="555b8-392">卡片集合包括 `builder.AttachmentLayout.carousel` `builder.AttachmentLayout.list` 和 。</span><span class="sxs-lookup"><span data-stu-id="555b8-392">Card collections include `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="555b8-393">这些集合包含自适应、hero 或缩略图卡片。</span><span class="sxs-lookup"><span data-stu-id="555b8-393">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="555b8-394">Carousel 集合</span><span class="sxs-lookup"><span data-stu-id="555b8-394">Carousel collection</span></span>

<span data-ttu-id="555b8-395">盘 [选布局](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) 显示卡片的盘选（可选）以及关联的操作按钮。</span><span class="sxs-lookup"><span data-stu-id="555b8-395">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="555b8-396">支持木马集合</span><span class="sxs-lookup"><span data-stu-id="555b8-396">Support for carousel collections</span></span>

| <span data-ttu-id="555b8-397">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="555b8-397">Bots in Teams</span></span> | <span data-ttu-id="555b8-398">消息扩展</span><span class="sxs-lookup"><span data-stu-id="555b8-398">Messaging extensions</span></span>  | <span data-ttu-id="555b8-399">连接器</span><span class="sxs-lookup"><span data-stu-id="555b8-399">Connectors</span></span> | <span data-ttu-id="555b8-400">机器人框架</span><span class="sxs-lookup"><span data-stu-id="555b8-400">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555b8-401">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-401">✔</span></span> | <span data-ttu-id="555b8-402">✖</span><span class="sxs-lookup"><span data-stu-id="555b8-402">✖</span></span> | <span data-ttu-id="555b8-403">✖</span><span class="sxs-lookup"><span data-stu-id="555b8-403">✖</span></span> | <span data-ttu-id="555b8-404">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-404">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="555b8-405">一个盘式消息最多可显示每封邮件 10 张卡片。</span><span class="sxs-lookup"><span data-stu-id="555b8-405">A carousel can display a maximum of ten cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="555b8-406">单盘式卡片的属性</span><span class="sxs-lookup"><span data-stu-id="555b8-406">Properties of a carousel card</span></span>

<span data-ttu-id="555b8-407">单盘式播放卡片的属性与 hero 卡和缩略图卡片的属性相同。</span><span class="sxs-lookup"><span data-stu-id="555b8-407">Properties of a carousel card are same as those of the hero and thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="555b8-408">一个木马集合的示例</span><span class="sxs-lookup"><span data-stu-id="555b8-408">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="555b8-410">盘车集合的语法</span><span class="sxs-lookup"><span data-stu-id="555b8-410">Syntax for carousel collections</span></span>

<span data-ttu-id="555b8-411">`builder.AttachmentLayoutTypes.Carousel` 是木马集合的语法。</span><span class="sxs-lookup"><span data-stu-id="555b8-411">`builder.AttachmentLayoutTypes.Carousel` is the syntax for carousel collections.</span></span>

## <a name="list-collection"></a><span data-ttu-id="555b8-412">列表集合</span><span class="sxs-lookup"><span data-stu-id="555b8-412">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="555b8-413">支持列表集合</span><span class="sxs-lookup"><span data-stu-id="555b8-413">Support for list collections</span></span>

<span data-ttu-id="555b8-414">列表布局显示卡片的垂直堆叠列表（可选）以及关联的操作按钮。</span><span class="sxs-lookup"><span data-stu-id="555b8-414">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="555b8-415">聊天机器人Teams</span><span class="sxs-lookup"><span data-stu-id="555b8-415">Bots in Teams</span></span> | <span data-ttu-id="555b8-416">消息扩展</span><span class="sxs-lookup"><span data-stu-id="555b8-416">Messaging extensions</span></span>  | <span data-ttu-id="555b8-417">连接器</span><span class="sxs-lookup"><span data-stu-id="555b8-417">Connectors</span></span> | <span data-ttu-id="555b8-418">机器人框架</span><span class="sxs-lookup"><span data-stu-id="555b8-418">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="555b8-419">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-419">✔</span></span> | <span data-ttu-id="555b8-420">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-420">✔</span></span> | <span data-ttu-id="555b8-421">✖</span><span class="sxs-lookup"><span data-stu-id="555b8-421">✖</span></span> | <span data-ttu-id="555b8-422">✔</span><span class="sxs-lookup"><span data-stu-id="555b8-422">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="555b8-423">列表集合的示例</span><span class="sxs-lookup"><span data-stu-id="555b8-423">Example of a list collection</span></span>

![卡片列表示例](~/assets/images/cards/list.png)

<span data-ttu-id="555b8-425">属性与 hero 或 thumbnail 卡片的属性相同。</span><span class="sxs-lookup"><span data-stu-id="555b8-425">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="555b8-426">列表最多可显示每封邮件 10 张卡片。</span><span class="sxs-lookup"><span data-stu-id="555b8-426">A list can display a maximum of ten cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="555b8-427">iOS 和 Android 上尚不支持列表卡的一些组合。</span><span class="sxs-lookup"><span data-stu-id="555b8-427">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="555b8-428">列表集合的语法</span><span class="sxs-lookup"><span data-stu-id="555b8-428">Syntax for list collections</span></span>

<span data-ttu-id="555b8-429">`builder.AttachmentLayout.list` 是列表集合的语法。</span><span class="sxs-lookup"><span data-stu-id="555b8-429">`builder.AttachmentLayout.list` is the syntax for list collections.</span></span>

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="555b8-430">不支持的Teams</span><span class="sxs-lookup"><span data-stu-id="555b8-430">Cards not supported in Teams</span></span>

<span data-ttu-id="555b8-431">以下卡片由 Bot Framework 实现，但不受自动程序Teams：</span><span class="sxs-lookup"><span data-stu-id="555b8-431">The following cards are implemented by the Bot Framework, but are not supported by Teams:</span></span>

* <span data-ttu-id="555b8-432">动画卡</span><span class="sxs-lookup"><span data-stu-id="555b8-432">Animation cards</span></span>
* <span data-ttu-id="555b8-433">音频卡</span><span class="sxs-lookup"><span data-stu-id="555b8-433">Audio cards</span></span>
* <span data-ttu-id="555b8-434">视频卡</span><span class="sxs-lookup"><span data-stu-id="555b8-434">Video cards</span></span>
