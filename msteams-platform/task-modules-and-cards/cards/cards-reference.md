---
title: 卡片参考
description: 介绍 Teams 中自动程序可用的所有卡片和卡片操作
keywords: 机器人卡参考
ms.topic: reference
ms.openlocfilehash: 839430baa5ce5e8950a21a1472036c6fd96f4edf
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911894"
---
# <a name="cards-reference"></a><span data-ttu-id="64030-104">卡参考</span><span class="sxs-lookup"><span data-stu-id="64030-104">Cards reference</span></span>

<span data-ttu-id="64030-105">本部分中列出的卡片在 Microsoft Teams 的自动程序中受支持。</span><span class="sxs-lookup"><span data-stu-id="64030-105">The cards listed in this section are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="64030-106">它们基于 Bot Framework 定义的卡，但 Teams 不支持所有 Bot Framework 卡，并且已添加自己的一些卡。</span><span class="sxs-lookup"><span data-stu-id="64030-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="64030-107">本文档的参考中已指出差异。</span><span class="sxs-lookup"><span data-stu-id="64030-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="64030-108">卡片示例</span><span class="sxs-lookup"><span data-stu-id="64030-108">Card examples</span></span>

<span data-ttu-id="64030-109">有关如何使用自动程序生成器 SDK (v3) 文档中的其他信息。</span><span class="sxs-lookup"><span data-stu-id="64030-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="64030-110">GitHub 上的 Microsoft/BotBuilder 示例存储库中也提供了代码示例。</span><span class="sxs-lookup"><span data-stu-id="64030-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="64030-111">.NET</span><span class="sxs-lookup"><span data-stu-id="64030-111">.NET</span></span>
  * [<span data-ttu-id="64030-112">将卡片添加为邮件附件</span><span class="sxs-lookup"><span data-stu-id="64030-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="64030-113">自动程序生成器 v3 (的卡片示例) </span><span class="sxs-lookup"><span data-stu-id="64030-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="64030-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="64030-114">Node.js</span></span>
  * [<span data-ttu-id="64030-115">将卡片添加为邮件附件</span><span class="sxs-lookup"><span data-stu-id="64030-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="64030-116">自动程序生成器 v3 (的卡片示例) </span><span class="sxs-lookup"><span data-stu-id="64030-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="64030-117">卡片类型</span><span class="sxs-lookup"><span data-stu-id="64030-117">Types of cards</span></span>

<span data-ttu-id="64030-118">此表显示了可用的卡片类型：</span><span class="sxs-lookup"><span data-stu-id="64030-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="64030-119">卡片类型</span><span class="sxs-lookup"><span data-stu-id="64030-119">Card type</span></span> | <span data-ttu-id="64030-120">说明</span><span class="sxs-lookup"><span data-stu-id="64030-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="64030-121">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="64030-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="64030-122">可包含文本、语音、图像、按钮和输入字段的任意组合的高度可自定义卡片。</span><span class="sxs-lookup"><span data-stu-id="64030-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="64030-123">Hero 卡片</span><span class="sxs-lookup"><span data-stu-id="64030-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="64030-124">通常包含单个大图像、一个或多个按钮和少量文本。</span><span class="sxs-lookup"><span data-stu-id="64030-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="64030-125">列表卡</span><span class="sxs-lookup"><span data-stu-id="64030-125">List card</span></span>](#list-card) | <span data-ttu-id="64030-126">项的滚动列表。</span><span class="sxs-lookup"><span data-stu-id="64030-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="64030-127">Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="64030-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="64030-128">具有多个分区、字段、图像和操作的灵活性布局。</span><span class="sxs-lookup"><span data-stu-id="64030-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="64030-129">收据卡</span><span class="sxs-lookup"><span data-stu-id="64030-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="64030-130">向用户提供收据。</span><span class="sxs-lookup"><span data-stu-id="64030-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="64030-131">登录卡</span><span class="sxs-lookup"><span data-stu-id="64030-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="64030-132">使机器人能够请求用户登录。</span><span class="sxs-lookup"><span data-stu-id="64030-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="64030-133">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="64030-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="64030-134">通常包含单个缩略图图像、一些短文本和一个或多个按钮。</span><span class="sxs-lookup"><span data-stu-id="64030-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="64030-135">卡片集合</span><span class="sxs-lookup"><span data-stu-id="64030-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="64030-136">用于在单个响应中返回多个项目。</span><span class="sxs-lookup"><span data-stu-id="64030-136">Used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="64030-137">所有卡片的常见属性</span><span class="sxs-lookup"><span data-stu-id="64030-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="64030-138">内联卡片图像</span><span class="sxs-lookup"><span data-stu-id="64030-138">Inline card images</span></span>

<span data-ttu-id="64030-139">该卡片可以通过包含指向公开可用图像的链接来包含内嵌图像。</span><span class="sxs-lookup"><span data-stu-id="64030-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="64030-140">出于性能目的，强烈建议在 CDN 服务的公共内容交付网络上 (该) 。</span><span class="sxs-lookup"><span data-stu-id="64030-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="64030-141">在保持纵横比以覆盖图像区域的同时，图像会放大或缩小大小，然后从中心裁剪以实现卡片的适当纵横比。</span><span class="sxs-lookup"><span data-stu-id="64030-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="64030-142">图像必须最多为 1024×1024，采用 PNG、JPEG 或 GIF 格式，并且不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="64030-142">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and animated GIF is not supported.</span></span>

| <span data-ttu-id="64030-143">属性</span><span class="sxs-lookup"><span data-stu-id="64030-143">Property</span></span> | <span data-ttu-id="64030-144">类型</span><span class="sxs-lookup"><span data-stu-id="64030-144">Type</span></span>  | <span data-ttu-id="64030-145">说明</span><span class="sxs-lookup"><span data-stu-id="64030-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64030-146">url</span><span class="sxs-lookup"><span data-stu-id="64030-146">url</span></span> | <span data-ttu-id="64030-147">URL</span><span class="sxs-lookup"><span data-stu-id="64030-147">URL</span></span> | <span data-ttu-id="64030-148">图像的 HTTPS URL</span><span class="sxs-lookup"><span data-stu-id="64030-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="64030-149">alt</span><span class="sxs-lookup"><span data-stu-id="64030-149">alt</span></span> | <span data-ttu-id="64030-150">String</span><span class="sxs-lookup"><span data-stu-id="64030-150">String</span></span> | <span data-ttu-id="64030-151">图像的辅助说明</span><span class="sxs-lookup"><span data-stu-id="64030-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="64030-152">按钮</span><span class="sxs-lookup"><span data-stu-id="64030-152">Buttons</span></span>

<span data-ttu-id="64030-153">按钮显示在卡片底部堆叠。</span><span class="sxs-lookup"><span data-stu-id="64030-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="64030-154">按钮文本始终在一行上，如果文本超过按钮宽度，按钮文本将被截断。</span><span class="sxs-lookup"><span data-stu-id="64030-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="64030-155">不会显示超出卡支持的最大数目的其他任何按钮。</span><span class="sxs-lookup"><span data-stu-id="64030-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="64030-156">有关详细信息 [，](~/task-modules-and-cards/cards/cards-actions.md) 请参阅卡片操作。</span><span class="sxs-lookup"><span data-stu-id="64030-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="64030-157">卡片格式</span><span class="sxs-lookup"><span data-stu-id="64030-157">Card formatting</span></span>

<span data-ttu-id="64030-158">有关 [卡片中的](~/task-modules-and-cards/cards/cards-format.md) 文本格式设置详细信息，请参阅卡片格式。</span><span class="sxs-lookup"><span data-stu-id="64030-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="64030-159">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="64030-159">Adaptive card</span></span>

<span data-ttu-id="64030-160">自适应卡片是可自定义的卡片，可以包含文本、语音、图像、按钮和输入字段的任意组合。</span><span class="sxs-lookup"><span data-stu-id="64030-160">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="64030-161">请参阅 [自适应卡片 v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)。</span><span class="sxs-lookup"><span data-stu-id="64030-161">See [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="64030-162">支持自适应卡片</span><span class="sxs-lookup"><span data-stu-id="64030-162">Support for adaptive cards</span></span>

| <span data-ttu-id="64030-163">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="64030-163">Bots in Teams</span></span> | <span data-ttu-id="64030-164">消息扩展</span><span class="sxs-lookup"><span data-stu-id="64030-164">Messaging extensions</span></span>  | <span data-ttu-id="64030-165">连接器</span><span class="sxs-lookup"><span data-stu-id="64030-165">Connectors</span></span> | <span data-ttu-id="64030-166">机器人框架</span><span class="sxs-lookup"><span data-stu-id="64030-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="64030-167">✔</span><span class="sxs-lookup"><span data-stu-id="64030-167">✔</span></span> | <span data-ttu-id="64030-168">✔</span><span class="sxs-lookup"><span data-stu-id="64030-168">✔</span></span> | <span data-ttu-id="64030-169">✖</span><span class="sxs-lookup"><span data-stu-id="64030-169">✖</span></span> | <span data-ttu-id="64030-170">✔</span><span class="sxs-lookup"><span data-stu-id="64030-170">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="64030-171">Teams 平台支持 v1.2 或更早的自适应卡片功能。</span><span class="sxs-lookup"><span data-stu-id="64030-171">Teams platform supports v1.2 or earlier of Adaptive card features.</span></span>
> * <span data-ttu-id="64030-172">Teams 平台上的自适应卡片 v1.2 当前不支持媒体元素。</span><span class="sxs-lookup"><span data-stu-id="64030-172">Media elements are currently not supported in Adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="64030-173">自适应卡片示例</span><span class="sxs-lookup"><span data-stu-id="64030-173">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="64030-175">自适应卡片的其他信息</span><span class="sxs-lookup"><span data-stu-id="64030-175">Additional information on adaptive cards</span></span>

* [<span data-ttu-id="64030-176">自适应卡片概述</span><span class="sxs-lookup"><span data-stu-id="64030-176">Adaptive cards overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="64030-177">Teams 中的自适应卡片操作</span><span class="sxs-lookup"><span data-stu-id="64030-177">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="64030-178">Hero 卡片</span><span class="sxs-lookup"><span data-stu-id="64030-178">Hero card</span></span>

<span data-ttu-id="64030-179">通常包含单个大图像、一个或多个按钮和文本的卡片。</span><span class="sxs-lookup"><span data-stu-id="64030-179">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="64030-180">支持 Hero 卡片</span><span class="sxs-lookup"><span data-stu-id="64030-180">Support for hero cards</span></span>

| <span data-ttu-id="64030-181">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="64030-181">Bots in Teams</span></span> | <span data-ttu-id="64030-182">消息扩展</span><span class="sxs-lookup"><span data-stu-id="64030-182">Messaging Extensions</span></span>  | <span data-ttu-id="64030-183">连接器</span><span class="sxs-lookup"><span data-stu-id="64030-183">Connectors</span></span> | <span data-ttu-id="64030-184">机器人框架</span><span class="sxs-lookup"><span data-stu-id="64030-184">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="64030-185">✔</span><span class="sxs-lookup"><span data-stu-id="64030-185">✔</span></span> | <span data-ttu-id="64030-186">✔</span><span class="sxs-lookup"><span data-stu-id="64030-186">✔</span></span> | <span data-ttu-id="64030-187">✖</span><span class="sxs-lookup"><span data-stu-id="64030-187">✖</span></span> | <span data-ttu-id="64030-188">✔</span><span class="sxs-lookup"><span data-stu-id="64030-188">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="64030-189">Hero 卡片的属性</span><span class="sxs-lookup"><span data-stu-id="64030-189">Properties of a hero card</span></span>

| <span data-ttu-id="64030-190">属性</span><span class="sxs-lookup"><span data-stu-id="64030-190">Property</span></span> | <span data-ttu-id="64030-191">类型</span><span class="sxs-lookup"><span data-stu-id="64030-191">Type</span></span>  | <span data-ttu-id="64030-192">说明</span><span class="sxs-lookup"><span data-stu-id="64030-192">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64030-193">title</span><span class="sxs-lookup"><span data-stu-id="64030-193">title</span></span> | <span data-ttu-id="64030-194">格式文本 </span><span class="sxs-lookup"><span data-stu-id="64030-194">Rich text</span></span> | <span data-ttu-id="64030-195">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="64030-195">Title of the card.</span></span> <span data-ttu-id="64030-196">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="64030-196">Maximum 2 lines.</span></span> |
| <span data-ttu-id="64030-197">subtitle</span><span class="sxs-lookup"><span data-stu-id="64030-197">subtitle</span></span> | <span data-ttu-id="64030-198">格式文本 </span><span class="sxs-lookup"><span data-stu-id="64030-198">Rich text</span></span> | <span data-ttu-id="64030-199">卡片的副标题。</span><span class="sxs-lookup"><span data-stu-id="64030-199">Subtitle of the card.</span></span> <span data-ttu-id="64030-200">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="64030-200">Maximum 2 lines.</span></span>|
| <span data-ttu-id="64030-201">text</span><span class="sxs-lookup"><span data-stu-id="64030-201">text</span></span> | <span data-ttu-id="64030-202">格式文本 </span><span class="sxs-lookup"><span data-stu-id="64030-202">Rich text</span></span> | <span data-ttu-id="64030-203">文本显示在副标题正下方;请参阅 [格式选项](~/task-modules-and-cards/cards/cards-format.md) 的卡片格式。</span><span class="sxs-lookup"><span data-stu-id="64030-203">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="64030-204">images</span><span class="sxs-lookup"><span data-stu-id="64030-204">images</span></span> | <span data-ttu-id="64030-205">图像数组</span><span class="sxs-lookup"><span data-stu-id="64030-205">Array of images</span></span> | <span data-ttu-id="64030-206">显示在卡片顶部的图像。</span><span class="sxs-lookup"><span data-stu-id="64030-206">Image displayed at top of card.</span></span> <span data-ttu-id="64030-207">纵横比 16：9。</span><span class="sxs-lookup"><span data-stu-id="64030-207">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="64030-208">buttons</span><span class="sxs-lookup"><span data-stu-id="64030-208">buttons</span></span> | <span data-ttu-id="64030-209">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="64030-209">Array of action objects</span></span> | <span data-ttu-id="64030-210">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="64030-210">Set of actions applicable to the current card.</span></span> <span data-ttu-id="64030-211">最大值 6。</span><span class="sxs-lookup"><span data-stu-id="64030-211">Maximum 6.</span></span> |
| <span data-ttu-id="64030-212">点击</span><span class="sxs-lookup"><span data-stu-id="64030-212">tap</span></span> | <span data-ttu-id="64030-213">Action 对象</span><span class="sxs-lookup"><span data-stu-id="64030-213">Action object</span></span> | <span data-ttu-id="64030-214">当用户点击卡片本身时，将激活此操作。</span><span class="sxs-lookup"><span data-stu-id="64030-214">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="64030-215">Hero 卡片示例</span><span class="sxs-lookup"><span data-stu-id="64030-215">Example of a hero card</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="64030-217">有关 Hero 卡片的其他信息</span><span class="sxs-lookup"><span data-stu-id="64030-217">Additional information on hero cards</span></span>

<span data-ttu-id="64030-218">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="64030-218">Bot Framework reference:</span></span>

* [<span data-ttu-id="64030-219">主卡节点</span><span class="sxs-lookup"><span data-stu-id="64030-219">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="64030-220">Hero card C#</span><span class="sxs-lookup"><span data-stu-id="64030-220">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="64030-221">列表卡</span><span class="sxs-lookup"><span data-stu-id="64030-221">List card</span></span>

<span data-ttu-id="64030-222">Teams 已添加列表卡片，以提供列表集合无法提供的功能。</span><span class="sxs-lookup"><span data-stu-id="64030-222">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="64030-223">列表卡提供项的滚动列表。</span><span class="sxs-lookup"><span data-stu-id="64030-223">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="64030-224">支持列表卡</span><span class="sxs-lookup"><span data-stu-id="64030-224">Support for list cards</span></span>

| <span data-ttu-id="64030-225">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="64030-225">Bots in Teams</span></span> | <span data-ttu-id="64030-226">消息扩展</span><span class="sxs-lookup"><span data-stu-id="64030-226">Messaging extensions</span></span>  | <span data-ttu-id="64030-227">连接器</span><span class="sxs-lookup"><span data-stu-id="64030-227">Connectors</span></span> | <span data-ttu-id="64030-228">机器人框架</span><span class="sxs-lookup"><span data-stu-id="64030-228">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="64030-229">✔</span><span class="sxs-lookup"><span data-stu-id="64030-229">✔</span></span> | <span data-ttu-id="64030-230">✖</span><span class="sxs-lookup"><span data-stu-id="64030-230">✖</span></span> | <span data-ttu-id="64030-231">✖</span><span class="sxs-lookup"><span data-stu-id="64030-231">✖</span></span> |<span data-ttu-id="64030-232">✔</span><span class="sxs-lookup"><span data-stu-id="64030-232">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="64030-233">列表卡片的属性</span><span class="sxs-lookup"><span data-stu-id="64030-233">Properties of a list card</span></span>

| <span data-ttu-id="64030-234">属性</span><span class="sxs-lookup"><span data-stu-id="64030-234">Property</span></span> | <span data-ttu-id="64030-235">类型</span><span class="sxs-lookup"><span data-stu-id="64030-235">Type</span></span>  | <span data-ttu-id="64030-236">说明</span><span class="sxs-lookup"><span data-stu-id="64030-236">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64030-237">title</span><span class="sxs-lookup"><span data-stu-id="64030-237">title</span></span> | <span data-ttu-id="64030-238">格式文本 </span><span class="sxs-lookup"><span data-stu-id="64030-238">Rich text</span></span> | <span data-ttu-id="64030-239">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="64030-239">Title of the card.</span></span> <span data-ttu-id="64030-240">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="64030-240">Maximum 2 lines.</span></span>|
| <span data-ttu-id="64030-241">items</span><span class="sxs-lookup"><span data-stu-id="64030-241">items</span></span> | <span data-ttu-id="64030-242">列表项数组</span><span class="sxs-lookup"><span data-stu-id="64030-242">Array of list items</span></span>  ||
| <span data-ttu-id="64030-243">buttons</span><span class="sxs-lookup"><span data-stu-id="64030-243">buttons</span></span> | <span data-ttu-id="64030-244">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="64030-244">Array of action objects</span></span> | <span data-ttu-id="64030-245">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="64030-245">Set of actions applicable to the current card.</span></span> <span data-ttu-id="64030-246">最大值 6。</span><span class="sxs-lookup"><span data-stu-id="64030-246">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="64030-247">列表卡示例</span><span class="sxs-lookup"><span data-stu-id="64030-247">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="64030-248">Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="64030-248">Office 365 connector card</span></span>

<span data-ttu-id="64030-249">Office 365 连接器卡在 Teams 中受支持，在 Bot Framework 中不受支持。</span><span class="sxs-lookup"><span data-stu-id="64030-249">The Office 365 Connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="64030-250">此卡片提供具有多个分区、字段、图像和操作的灵活性布局。</span><span class="sxs-lookup"><span data-stu-id="64030-250">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="64030-251">此卡封装连接器卡，以便机器人可以使用它。</span><span class="sxs-lookup"><span data-stu-id="64030-251">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="64030-252">有关连接器卡和 O365 卡之间的差异，请参阅"备注"部分。</span><span class="sxs-lookup"><span data-stu-id="64030-252">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="64030-253">支持 Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="64030-253">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="64030-254">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="64030-254">Bots in Teams</span></span> | <span data-ttu-id="64030-255">消息扩展</span><span class="sxs-lookup"><span data-stu-id="64030-255">Messaging extensions</span></span>  | <span data-ttu-id="64030-256">连接器</span><span class="sxs-lookup"><span data-stu-id="64030-256">Connectors</span></span> | <span data-ttu-id="64030-257">机器人框架</span><span class="sxs-lookup"><span data-stu-id="64030-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="64030-258">✔</span><span class="sxs-lookup"><span data-stu-id="64030-258">✔</span></span> | <span data-ttu-id="64030-259">✔</span><span class="sxs-lookup"><span data-stu-id="64030-259">✔</span></span> | <span data-ttu-id="64030-260">✔</span><span class="sxs-lookup"><span data-stu-id="64030-260">✔</span></span> | <span data-ttu-id="64030-261">✖</span><span class="sxs-lookup"><span data-stu-id="64030-261">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="64030-262">Office 365 连接器卡的属性</span><span class="sxs-lookup"><span data-stu-id="64030-262">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="64030-263">属性</span><span class="sxs-lookup"><span data-stu-id="64030-263">Property</span></span> | <span data-ttu-id="64030-264">类型</span><span class="sxs-lookup"><span data-stu-id="64030-264">Type</span></span>  | <span data-ttu-id="64030-265">说明</span><span class="sxs-lookup"><span data-stu-id="64030-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64030-266">title</span><span class="sxs-lookup"><span data-stu-id="64030-266">title</span></span> | <span data-ttu-id="64030-267">格式文本 </span><span class="sxs-lookup"><span data-stu-id="64030-267">Rich text</span></span> | <span data-ttu-id="64030-268">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="64030-268">Title of the card.</span></span> <span data-ttu-id="64030-269">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="64030-269">Maximum 2 lines.</span></span> |
| <span data-ttu-id="64030-270">摘要</span><span class="sxs-lookup"><span data-stu-id="64030-270">summary</span></span> | <span data-ttu-id="64030-271">格式文本 </span><span class="sxs-lookup"><span data-stu-id="64030-271">Rich text</span></span> | <span data-ttu-id="64030-272">卡片的摘要。</span><span class="sxs-lookup"><span data-stu-id="64030-272">Summary of the card.</span></span> <span data-ttu-id="64030-273">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="64030-273">Maximum 2 lines.</span></span> |
| <span data-ttu-id="64030-274">text</span><span class="sxs-lookup"><span data-stu-id="64030-274">text</span></span> | <span data-ttu-id="64030-275">格式文本 </span><span class="sxs-lookup"><span data-stu-id="64030-275">Rich text</span></span> | <span data-ttu-id="64030-276">文本显示在副标题正下方;请参阅 [格式选项](~/task-modules-and-cards/cards/cards-format.md) 的卡片格式。</span><span class="sxs-lookup"><span data-stu-id="64030-276">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="64030-277">themeColor</span><span class="sxs-lookup"><span data-stu-id="64030-277">themeColor</span></span> | <span data-ttu-id="64030-278">十六进制字符串</span><span class="sxs-lookup"><span data-stu-id="64030-278">HEX string</span></span> | <span data-ttu-id="64030-279">替代应用程序清单中提供的 accentColor 的颜色。</span><span class="sxs-lookup"><span data-stu-id="64030-279">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="64030-280">Office 365 连接器卡上的备注</span><span class="sxs-lookup"><span data-stu-id="64030-280">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="64030-281">Office 365 连接器卡在 Microsoft Teams 中正常运行，包括 [ActionCard 操作](/outlook/actionable-messages/card-reference#actioncard-action)。</span><span class="sxs-lookup"><span data-stu-id="64030-281">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="64030-282">从连接器使用连接器卡和在机器人中使用连接器卡之间的一个重要区别是处理卡操作。</span><span class="sxs-lookup"><span data-stu-id="64030-282">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="64030-283">对于连接器，终结点通过 HTTP POST 接收卡有效负载。</span><span class="sxs-lookup"><span data-stu-id="64030-283">For a connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="64030-284">对于自动程序，该操作将触发仅向自动程序发送操作 `HttpPOST` `invoke` ID 和正文的活动。</span><span class="sxs-lookup"><span data-stu-id="64030-284">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="64030-285">每个连接器卡最多可以显示 10 个部分，并且每个部分最多可以包含 5 个图像和 5 个操作。</span><span class="sxs-lookup"><span data-stu-id="64030-285">Each connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="64030-286">邮件中其他任何部分、图像或操作将不会显示。</span><span class="sxs-lookup"><span data-stu-id="64030-286">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="64030-287">所有文本字段都支持 Markdown 和 HTML。</span><span class="sxs-lookup"><span data-stu-id="64030-287">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="64030-288">您可以通过在邮件中设置属性来控制使用 Markdown 或 HTML `markdown` 的部分。</span><span class="sxs-lookup"><span data-stu-id="64030-288">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="64030-289">默认情况下， `markdown` 设置为;如果要改为使用 `true` HTML，则设置为 `markdown` `false` 。</span><span class="sxs-lookup"><span data-stu-id="64030-289">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="64030-290">如果指定 `themeColor` 该属性，它将覆盖 `accentColor` 应用清单中的属性。</span><span class="sxs-lookup"><span data-stu-id="64030-290">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="64030-291">若要指定其呈现样式 `activityImage` ，可以按 `activityImageType` 如下方式设置：</span><span class="sxs-lookup"><span data-stu-id="64030-291">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="64030-292">值</span><span class="sxs-lookup"><span data-stu-id="64030-292">Value</span></span> | <span data-ttu-id="64030-293">说明</span><span class="sxs-lookup"><span data-stu-id="64030-293">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="64030-294">默认值; `activityImage` 将被裁剪为圆形。</span><span class="sxs-lookup"><span data-stu-id="64030-294">Default; `activityImage` will be cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="64030-295">`activityImage` 将显示为矩形并保留其纵横比。</span><span class="sxs-lookup"><span data-stu-id="64030-295">`activityImage` will be displayed as a rectangle and retain its aspect ratio.</span></span> |

<span data-ttu-id="64030-296">有关连接器卡属性的所有其他详细信息，请参阅 [可操作邮件卡参考](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="64030-296">For all other details about connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="64030-297">Microsoft Teams 当前不支持的唯一连接器卡属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="64030-297">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="64030-298">`startGroup` (Teams `true`) </span><span class="sxs-lookup"><span data-stu-id="64030-298">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="64030-299">Office 365 连接器卡示例</span><span class="sxs-lookup"><span data-stu-id="64030-299">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="64030-300">收据卡</span><span class="sxs-lookup"><span data-stu-id="64030-300">Receipt card</span></span>

<span data-ttu-id="64030-301">Teams 支持收据卡。</span><span class="sxs-lookup"><span data-stu-id="64030-301">Teams supports receipt card.</span></span> <span data-ttu-id="64030-302">它是使机器人能够为用户提供收据的卡片。</span><span class="sxs-lookup"><span data-stu-id="64030-302">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="64030-303">它通常包含要包含在收据上的项目列表，例如税务和总信息。</span><span class="sxs-lookup"><span data-stu-id="64030-303">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="64030-304">支持收据卡</span><span class="sxs-lookup"><span data-stu-id="64030-304">Support for receipt cards</span></span>

| <span data-ttu-id="64030-305">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="64030-305">Bots in Teams</span></span> | <span data-ttu-id="64030-306">消息扩展</span><span class="sxs-lookup"><span data-stu-id="64030-306">Messaging extensions</span></span>  | <span data-ttu-id="64030-307">连接器</span><span class="sxs-lookup"><span data-stu-id="64030-307">Connectors</span></span> | <span data-ttu-id="64030-308">机器人框架</span><span class="sxs-lookup"><span data-stu-id="64030-308">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="64030-309">✔</span><span class="sxs-lookup"><span data-stu-id="64030-309">✔</span></span> | <span data-ttu-id="64030-310">✔</span><span class="sxs-lookup"><span data-stu-id="64030-310">✔</span></span> | <span data-ttu-id="64030-311">✖</span><span class="sxs-lookup"><span data-stu-id="64030-311">✖</span></span> | <span data-ttu-id="64030-312">✔</span><span class="sxs-lookup"><span data-stu-id="64030-312">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="64030-313">收据卡示例</span><span class="sxs-lookup"><span data-stu-id="64030-313">Example of a receipt card</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="64030-315">收据卡的其他信息</span><span class="sxs-lookup"><span data-stu-id="64030-315">Additional information on receipt cards</span></span>

<span data-ttu-id="64030-316">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="64030-316">Bot Framework reference:</span></span>

* [<span data-ttu-id="64030-317">收据卡节点</span><span class="sxs-lookup"><span data-stu-id="64030-317">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="64030-318">收据卡 C#</span><span class="sxs-lookup"><span data-stu-id="64030-318">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="64030-319">登录卡</span><span class="sxs-lookup"><span data-stu-id="64030-319">Signin card</span></span>

<span data-ttu-id="64030-320">登录卡使机器人可以请求用户登录。</span><span class="sxs-lookup"><span data-stu-id="64030-320">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="64030-321">在 Teams 中受支持的形式与在 Bot Framework 中稍有不同。</span><span class="sxs-lookup"><span data-stu-id="64030-321">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="64030-322">Teams 中的登录卡类似于 Bot 框架中的登录卡，只是 Teams 中的登录卡仅支持两个操作： `signin` 和 `openUrl` 。</span><span class="sxs-lookup"><span data-stu-id="64030-322">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="64030-323">登录 *操作可以从* Teams 中的任意卡使用，而不只是从登录卡使用。</span><span class="sxs-lookup"><span data-stu-id="64030-323">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="64030-324">有关身份验证的更多详细信息，请参阅 [适用于机器人的 Microsoft Teams 身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="64030-324">For more details on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="64030-325">支持登录卡</span><span class="sxs-lookup"><span data-stu-id="64030-325">Support for Signin cards</span></span>

| <span data-ttu-id="64030-326">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="64030-326">Bots in Teams</span></span> | <span data-ttu-id="64030-327">消息扩展</span><span class="sxs-lookup"><span data-stu-id="64030-327">Messaging extensions</span></span>  | <span data-ttu-id="64030-328">连接器</span><span class="sxs-lookup"><span data-stu-id="64030-328">Connectors</span></span> | <span data-ttu-id="64030-329">机器人框架</span><span class="sxs-lookup"><span data-stu-id="64030-329">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="64030-330">✔</span><span class="sxs-lookup"><span data-stu-id="64030-330">✔</span></span> | <span data-ttu-id="64030-331">✖</span><span class="sxs-lookup"><span data-stu-id="64030-331">✖</span></span> | <span data-ttu-id="64030-332">✖</span><span class="sxs-lookup"><span data-stu-id="64030-332">✖</span></span> | <span data-ttu-id="64030-333">✔</span><span class="sxs-lookup"><span data-stu-id="64030-333">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="64030-334">登录卡的其他信息</span><span class="sxs-lookup"><span data-stu-id="64030-334">Additional information on signin cards</span></span>

<span data-ttu-id="64030-335">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="64030-335">Bot Framework reference:</span></span>

* [<span data-ttu-id="64030-336">登录卡节点</span><span class="sxs-lookup"><span data-stu-id="64030-336">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="64030-337">登录卡 C#</span><span class="sxs-lookup"><span data-stu-id="64030-337">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="64030-338">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="64030-338">Thumbnail card</span></span>

<span data-ttu-id="64030-339">通常包含单个缩略图图像、一个或多个按钮和文本的卡片。</span><span class="sxs-lookup"><span data-stu-id="64030-339">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="64030-340">支持缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="64030-340">Support for thumbnail cards</span></span>

| <span data-ttu-id="64030-341">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="64030-341">Bots in Teams</span></span> | <span data-ttu-id="64030-342">消息扩展</span><span class="sxs-lookup"><span data-stu-id="64030-342">Messaging extensions</span></span>  | <span data-ttu-id="64030-343">连接器</span><span class="sxs-lookup"><span data-stu-id="64030-343">Connectors</span></span> | <span data-ttu-id="64030-344">机器人框架</span><span class="sxs-lookup"><span data-stu-id="64030-344">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="64030-345">✔</span><span class="sxs-lookup"><span data-stu-id="64030-345">✔</span></span> | <span data-ttu-id="64030-346">✔</span><span class="sxs-lookup"><span data-stu-id="64030-346">✔</span></span> | <span data-ttu-id="64030-347">✖</span><span class="sxs-lookup"><span data-stu-id="64030-347">✖</span></span> | <span data-ttu-id="64030-348">✔</span><span class="sxs-lookup"><span data-stu-id="64030-348">✔</span></span> |

![缩略图卡片示例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="64030-350">缩略图卡片的属性</span><span class="sxs-lookup"><span data-stu-id="64030-350">Properties of a thumbnail card</span></span>

| <span data-ttu-id="64030-351">属性</span><span class="sxs-lookup"><span data-stu-id="64030-351">Property</span></span> | <span data-ttu-id="64030-352">类型</span><span class="sxs-lookup"><span data-stu-id="64030-352">Type</span></span>  | <span data-ttu-id="64030-353">说明</span><span class="sxs-lookup"><span data-stu-id="64030-353">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="64030-354">title</span><span class="sxs-lookup"><span data-stu-id="64030-354">title</span></span> | <span data-ttu-id="64030-355">格式文本 </span><span class="sxs-lookup"><span data-stu-id="64030-355">Rich text</span></span> | <span data-ttu-id="64030-356">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="64030-356">Title of the card.</span></span> <span data-ttu-id="64030-357">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="64030-357">Maximum 2 lines.</span></span>|
| <span data-ttu-id="64030-358">subtitle</span><span class="sxs-lookup"><span data-stu-id="64030-358">subtitle</span></span> | <span data-ttu-id="64030-359">格式文本 </span><span class="sxs-lookup"><span data-stu-id="64030-359">Rich text</span></span> | <span data-ttu-id="64030-360">卡片的副标题。</span><span class="sxs-lookup"><span data-stu-id="64030-360">Subtitle of the card.</span></span> <span data-ttu-id="64030-361">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="64030-361">Maximum 2 lines.</span></span>|
| <span data-ttu-id="64030-362">text</span><span class="sxs-lookup"><span data-stu-id="64030-362">text</span></span> | <span data-ttu-id="64030-363">格式文本 </span><span class="sxs-lookup"><span data-stu-id="64030-363">Rich text</span></span> | <span data-ttu-id="64030-364">文本显示在副标题正下方;请参阅 [格式选项](~/task-modules-and-cards/cards/cards-format.md) 的卡片格式。</span><span class="sxs-lookup"><span data-stu-id="64030-364">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="64030-365">images</span><span class="sxs-lookup"><span data-stu-id="64030-365">images</span></span> | <span data-ttu-id="64030-366">图像数组</span><span class="sxs-lookup"><span data-stu-id="64030-366">Array of images</span></span> | <span data-ttu-id="64030-367">显示在卡片顶部的图像。</span><span class="sxs-lookup"><span data-stu-id="64030-367">Image displayed at top of card.</span></span> <span data-ttu-id="64030-368">纵横比为 1：1 (平方) 。</span><span class="sxs-lookup"><span data-stu-id="64030-368">Aspect ratio 1:1 (square).</span></span> |
| <span data-ttu-id="64030-369">buttons</span><span class="sxs-lookup"><span data-stu-id="64030-369">buttons</span></span> | <span data-ttu-id="64030-370">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="64030-370">Array of action objects</span></span> | <span data-ttu-id="64030-371">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="64030-371">Set of actions applicable to the current card.</span></span> <span data-ttu-id="64030-372">最大值 6。</span><span class="sxs-lookup"><span data-stu-id="64030-372">Maximum 6.</span></span> |
| <span data-ttu-id="64030-373">点击</span><span class="sxs-lookup"><span data-stu-id="64030-373">tap</span></span> | <span data-ttu-id="64030-374">Action 对象</span><span class="sxs-lookup"><span data-stu-id="64030-374">Action object</span></span> | <span data-ttu-id="64030-375">当用户点击卡片本身时，将激活此操作。</span><span class="sxs-lookup"><span data-stu-id="64030-375">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="64030-376">缩略图卡片示例</span><span class="sxs-lookup"><span data-stu-id="64030-376">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="64030-377">其他信息</span><span class="sxs-lookup"><span data-stu-id="64030-377">Additional information</span></span>

<span data-ttu-id="64030-378">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="64030-378">Bot Framework reference:</span></span>

* [<span data-ttu-id="64030-379">缩略图卡片节点</span><span class="sxs-lookup"><span data-stu-id="64030-379">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="64030-380">缩略图卡片 C#</span><span class="sxs-lookup"><span data-stu-id="64030-380">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="64030-381">卡片集合</span><span class="sxs-lookup"><span data-stu-id="64030-381">Card collections</span></span>

<span data-ttu-id="64030-382">Teams 支持卡片收集。</span><span class="sxs-lookup"><span data-stu-id="64030-382">Teams supports Card collections.</span></span>

<span data-ttu-id="64030-383">卡片集合： `builder.AttachmentLayout.carousel` `builder.AttachmentLayout.list` 和 。</span><span class="sxs-lookup"><span data-stu-id="64030-383">Card collections: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="64030-384">这些集合包含自适应、hero 或缩略图卡片。</span><span class="sxs-lookup"><span data-stu-id="64030-384">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="64030-385">Carousel 集合</span><span class="sxs-lookup"><span data-stu-id="64030-385">Carousel collection</span></span>

<span data-ttu-id="64030-386">盘 [盘布局显示](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) 卡片的盘选（可选）和关联的操作按钮。</span><span class="sxs-lookup"><span data-stu-id="64030-386">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="64030-387">支持木马集合</span><span class="sxs-lookup"><span data-stu-id="64030-387">Support for carousel collections</span></span>

| <span data-ttu-id="64030-388">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="64030-388">Bots in Teams</span></span> | <span data-ttu-id="64030-389">消息扩展</span><span class="sxs-lookup"><span data-stu-id="64030-389">Messaging extensions</span></span>  | <span data-ttu-id="64030-390">连接器</span><span class="sxs-lookup"><span data-stu-id="64030-390">Connectors</span></span> | <span data-ttu-id="64030-391">机器人框架</span><span class="sxs-lookup"><span data-stu-id="64030-391">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="64030-392">✔</span><span class="sxs-lookup"><span data-stu-id="64030-392">✔</span></span> | <span data-ttu-id="64030-393">✖</span><span class="sxs-lookup"><span data-stu-id="64030-393">✖</span></span> | <span data-ttu-id="64030-394">✖</span><span class="sxs-lookup"><span data-stu-id="64030-394">✖</span></span> | <span data-ttu-id="64030-395">✔</span><span class="sxs-lookup"><span data-stu-id="64030-395">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="64030-396">一个盘式消息最多可显示每封邮件 10 张卡片。</span><span class="sxs-lookup"><span data-stu-id="64030-396">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="64030-397">木马卡片的属性</span><span class="sxs-lookup"><span data-stu-id="64030-397">Properties of a carousel card</span></span>

<span data-ttu-id="64030-398">"木马"卡片的属性与"Hero"和"Thumbnail"卡片的属性相同。</span><span class="sxs-lookup"><span data-stu-id="64030-398">Properties of a Carousel card are same as those of the Hero and Thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="64030-399">一个木马集合的示例</span><span class="sxs-lookup"><span data-stu-id="64030-399">Example of a carousel collection</span></span>

![卡片的盘盘示例](~/assets/images/cards/carousel.png)

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="64030-401">木马集合的语法</span><span class="sxs-lookup"><span data-stu-id="64030-401">Syntax for carousel collections</span></span>

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a><span data-ttu-id="64030-402">列表集合</span><span class="sxs-lookup"><span data-stu-id="64030-402">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="64030-403">支持列表集合</span><span class="sxs-lookup"><span data-stu-id="64030-403">Support for list collections</span></span>

<span data-ttu-id="64030-404">列表布局显示垂直堆叠的卡片列表（可选）以及关联的操作按钮。</span><span class="sxs-lookup"><span data-stu-id="64030-404">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="64030-405">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="64030-405">Bots in Teams</span></span> | <span data-ttu-id="64030-406">消息扩展</span><span class="sxs-lookup"><span data-stu-id="64030-406">Messaging extensions</span></span>  | <span data-ttu-id="64030-407">连接器</span><span class="sxs-lookup"><span data-stu-id="64030-407">Connectors</span></span> | <span data-ttu-id="64030-408">机器人框架</span><span class="sxs-lookup"><span data-stu-id="64030-408">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="64030-409">✔</span><span class="sxs-lookup"><span data-stu-id="64030-409">✔</span></span> | <span data-ttu-id="64030-410">✔</span><span class="sxs-lookup"><span data-stu-id="64030-410">✔</span></span> | <span data-ttu-id="64030-411">✖</span><span class="sxs-lookup"><span data-stu-id="64030-411">✖</span></span> | <span data-ttu-id="64030-412">✔</span><span class="sxs-lookup"><span data-stu-id="64030-412">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="64030-413">列表集合的示例</span><span class="sxs-lookup"><span data-stu-id="64030-413">Example of a list collection</span></span>

![卡片列表示例](~/assets/images/cards/list.png)

<span data-ttu-id="64030-415">属性与 Hero 或缩略图卡片的属性相同。</span><span class="sxs-lookup"><span data-stu-id="64030-415">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="64030-416">一个列表最多可显示每封邮件 10 张卡片。</span><span class="sxs-lookup"><span data-stu-id="64030-416">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="64030-417">iOS 和 Android 上尚不支持列表卡的一些组合。</span><span class="sxs-lookup"><span data-stu-id="64030-417">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="64030-418">列表集合的语法</span><span class="sxs-lookup"><span data-stu-id="64030-418">Syntax for list collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="64030-419">Teams 中不支持的卡片</span><span class="sxs-lookup"><span data-stu-id="64030-419">Cards not supported in Teams</span></span>

<span data-ttu-id="64030-420">以下卡片由 Bot Framework 实现，但不受 Teams 支持。</span><span class="sxs-lookup"><span data-stu-id="64030-420">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="64030-421">动画卡</span><span class="sxs-lookup"><span data-stu-id="64030-421">Animation cards</span></span>
* <span data-ttu-id="64030-422">音频卡</span><span class="sxs-lookup"><span data-stu-id="64030-422">Audio cards</span></span>
* <span data-ttu-id="64030-423">视频卡</span><span class="sxs-lookup"><span data-stu-id="64030-423">Video cards</span></span>
