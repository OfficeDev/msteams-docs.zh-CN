---
title: 卡片参考
description: 介绍 Teams 中自动程序可用的所有卡片和卡片操作
keywords: 机器人卡参考
ms.topic: reference
ms.openlocfilehash: 5cb289738f379dedf53f3a96a7dcff61b908e901
ms.sourcegitcommit: 1ce74ed167bb81bf09f7f6f8d518093efafb549e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2021
ms.locfileid: "50827933"
---
# <a name="cards-reference"></a><span data-ttu-id="00e30-104">卡参考</span><span class="sxs-lookup"><span data-stu-id="00e30-104">Cards reference</span></span>

<span data-ttu-id="00e30-105">本部分中列出的卡片在 Microsoft Teams 的自动程序中受支持。</span><span class="sxs-lookup"><span data-stu-id="00e30-105">The cards listed in this section are supported in bots for Microsoft Teams.</span></span> <span data-ttu-id="00e30-106">它们基于 Bot Framework 定义的卡，但 Teams 不支持所有 Bot Framework 卡，并且已添加了一些自己的卡。</span><span class="sxs-lookup"><span data-stu-id="00e30-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="00e30-107">本文档的参考中已指出区别。</span><span class="sxs-lookup"><span data-stu-id="00e30-107">Differences are called out in the references in this document.</span></span>

## <a name="card-examples"></a><span data-ttu-id="00e30-108">卡片示例</span><span class="sxs-lookup"><span data-stu-id="00e30-108">Card examples</span></span>

<span data-ttu-id="00e30-109">有关如何使用卡的其他信息，请参阅 v3 版本 3 中自动程序生成器 SDK () 。</span><span class="sxs-lookup"><span data-stu-id="00e30-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="00e30-110">GitHub 上的 Microsoft/BotBuilder-Samples 存储库中也提供了代码示例。</span><span class="sxs-lookup"><span data-stu-id="00e30-110">Code samples are also available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="00e30-111">.NET</span><span class="sxs-lookup"><span data-stu-id="00e30-111">.NET</span></span>
  * [<span data-ttu-id="00e30-112">将卡片添加为邮件附件</span><span class="sxs-lookup"><span data-stu-id="00e30-112">Add cards as attachments to messages</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)
  * [<span data-ttu-id="00e30-113">自动程序生成器 v4 (的卡片示例) </span><span class="sxs-lookup"><span data-stu-id="00e30-113">Cards sample code (Bot Builder v4)</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards)

* <span data-ttu-id="00e30-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="00e30-114">Node.js</span></span>
  * [<span data-ttu-id="00e30-115">将卡片添加为邮件附件</span><span class="sxs-lookup"><span data-stu-id="00e30-115">Add cards as attachments to messages</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
  * [<span data-ttu-id="00e30-116">自动程序生成器 v4 (的卡片示例) </span><span class="sxs-lookup"><span data-stu-id="00e30-116">Cards sample code (Bot Builder v4)</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards)

## <a name="types-of-cards"></a><span data-ttu-id="00e30-117">卡片类型</span><span class="sxs-lookup"><span data-stu-id="00e30-117">Types of cards</span></span>

<span data-ttu-id="00e30-118">此表显示了可供你使用卡片的类型：</span><span class="sxs-lookup"><span data-stu-id="00e30-118">This table shows the types of cards available to you:</span></span>

| <span data-ttu-id="00e30-119">卡片类型</span><span class="sxs-lookup"><span data-stu-id="00e30-119">Card type</span></span> | <span data-ttu-id="00e30-120">说明</span><span class="sxs-lookup"><span data-stu-id="00e30-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="00e30-121">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="00e30-121">Adaptive card</span></span>](#adaptive-card) | <span data-ttu-id="00e30-122">可包含文本、语音、图像、按钮和输入字段的任意组合的高度可自定义的卡片。</span><span class="sxs-lookup"><span data-stu-id="00e30-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="00e30-123">Hero card</span><span class="sxs-lookup"><span data-stu-id="00e30-123">Hero card</span></span>](#hero-card) | <span data-ttu-id="00e30-124">通常包含单个大图像、一个或多个按钮和少量文本。</span><span class="sxs-lookup"><span data-stu-id="00e30-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="00e30-125">列表卡</span><span class="sxs-lookup"><span data-stu-id="00e30-125">List card</span></span>](#list-card) | <span data-ttu-id="00e30-126">项的滚动列表。</span><span class="sxs-lookup"><span data-stu-id="00e30-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="00e30-127">Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="00e30-127">Office 365 connector card</span></span>](#office-365-connector-card) | <span data-ttu-id="00e30-128">具有多个分区、字段、图像和操作的灵活性布局。</span><span class="sxs-lookup"><span data-stu-id="00e30-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="00e30-129">收据卡</span><span class="sxs-lookup"><span data-stu-id="00e30-129">Receipt card</span></span>](#receipt-card) | <span data-ttu-id="00e30-130">向用户提供收据。</span><span class="sxs-lookup"><span data-stu-id="00e30-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="00e30-131">登录卡</span><span class="sxs-lookup"><span data-stu-id="00e30-131">Signin card</span></span>](#signin-card) | <span data-ttu-id="00e30-132">使机器人能够请求用户登录。</span><span class="sxs-lookup"><span data-stu-id="00e30-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="00e30-133">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="00e30-133">Thumbnail card</span></span>](#thumbnail-card) | <span data-ttu-id="00e30-134">通常包含一个缩略图图像、一些短文本以及一个或多个按钮。</span><span class="sxs-lookup"><span data-stu-id="00e30-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="00e30-135">卡片集合</span><span class="sxs-lookup"><span data-stu-id="00e30-135">Card collections</span></span>](#card-collections) | <span data-ttu-id="00e30-136">用于在单个响应中返回多个项目。</span><span class="sxs-lookup"><span data-stu-id="00e30-136">Used to return multiple items in a single response.</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="00e30-137">所有卡片的常见属性</span><span class="sxs-lookup"><span data-stu-id="00e30-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="00e30-138">内联卡片图像</span><span class="sxs-lookup"><span data-stu-id="00e30-138">Inline card images</span></span>

<span data-ttu-id="00e30-139">卡片可以包含内联图像，包括指向公开可用图像的链接。</span><span class="sxs-lookup"><span data-stu-id="00e30-139">The card can contain an inline image by including a link to the publicly available image.</span></span> <span data-ttu-id="00e30-140">出于性能目的，强烈建议你将映像托管在公用内容交付网络或 CDN (上) 。</span><span class="sxs-lookup"><span data-stu-id="00e30-140">For performance purposes, it is highly recommended you host the image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="00e30-141">在保持纵横比以覆盖图像区域的同时，图像大小会向上或向下扩展，然后从中心裁剪以实现卡片的适当纵横比。</span><span class="sxs-lookup"><span data-stu-id="00e30-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="00e30-142">图像必须最多为 1024×1024、PNG、JPEG 或 GIF 格式，并且不支持动态 GIF。</span><span class="sxs-lookup"><span data-stu-id="00e30-142">Images must be at most 1024×1024, in PNG, JPEG, or GIF format, and animated GIF is not supported.</span></span>

| <span data-ttu-id="00e30-143">属性</span><span class="sxs-lookup"><span data-stu-id="00e30-143">Property</span></span> | <span data-ttu-id="00e30-144">类型</span><span class="sxs-lookup"><span data-stu-id="00e30-144">Type</span></span>  | <span data-ttu-id="00e30-145">说明</span><span class="sxs-lookup"><span data-stu-id="00e30-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="00e30-146">url</span><span class="sxs-lookup"><span data-stu-id="00e30-146">url</span></span> | <span data-ttu-id="00e30-147">URL</span><span class="sxs-lookup"><span data-stu-id="00e30-147">URL</span></span> | <span data-ttu-id="00e30-148">图像的 HTTPS URL</span><span class="sxs-lookup"><span data-stu-id="00e30-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="00e30-149">alt</span><span class="sxs-lookup"><span data-stu-id="00e30-149">alt</span></span> | <span data-ttu-id="00e30-150">String</span><span class="sxs-lookup"><span data-stu-id="00e30-150">String</span></span> | <span data-ttu-id="00e30-151">图像的辅助说明</span><span class="sxs-lookup"><span data-stu-id="00e30-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="00e30-152">按钮</span><span class="sxs-lookup"><span data-stu-id="00e30-152">Buttons</span></span>

<span data-ttu-id="00e30-153">按钮显示在卡片底部堆叠。</span><span class="sxs-lookup"><span data-stu-id="00e30-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="00e30-154">按钮文本始终位于单行中，如果文本超过按钮宽度，按钮文本将被截断。</span><span class="sxs-lookup"><span data-stu-id="00e30-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="00e30-155">不会显示超出卡支持的最大数目的其他任何按钮。</span><span class="sxs-lookup"><span data-stu-id="00e30-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="00e30-156">有关详细信息 [，请参阅卡片](~/task-modules-and-cards/cards/cards-actions.md) 操作。</span><span class="sxs-lookup"><span data-stu-id="00e30-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="00e30-157">卡片格式</span><span class="sxs-lookup"><span data-stu-id="00e30-157">Card formatting</span></span>

<span data-ttu-id="00e30-158">有关 [卡片中的](~/task-modules-and-cards/cards/cards-format.md) 文本格式设置详细信息，请参阅卡片格式。</span><span class="sxs-lookup"><span data-stu-id="00e30-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="00e30-159">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="00e30-159">Adaptive card</span></span>

<span data-ttu-id="00e30-160">自适应卡片是可自定义的卡片，可以包含文本、语音、图像、按钮和输入字段的任意组合。</span><span class="sxs-lookup"><span data-stu-id="00e30-160">An adaptive card is a customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span> <span data-ttu-id="00e30-161">请参阅[自适应卡片 v1.2.0。](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)</span><span class="sxs-lookup"><span data-stu-id="00e30-161">See [Adaptive Cards v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0).</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="00e30-162">自适应卡片支持</span><span class="sxs-lookup"><span data-stu-id="00e30-162">Support for adaptive cards</span></span>

| <span data-ttu-id="00e30-163">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="00e30-163">Bots in Teams</span></span> | <span data-ttu-id="00e30-164">消息扩展</span><span class="sxs-lookup"><span data-stu-id="00e30-164">Messaging extensions</span></span>  | <span data-ttu-id="00e30-165">连接器</span><span class="sxs-lookup"><span data-stu-id="00e30-165">Connectors</span></span> | <span data-ttu-id="00e30-166">机器人框架</span><span class="sxs-lookup"><span data-stu-id="00e30-166">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00e30-167">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-167">✔</span></span> | <span data-ttu-id="00e30-168">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-168">✔</span></span> | <span data-ttu-id="00e30-169">✖</span><span class="sxs-lookup"><span data-stu-id="00e30-169">✖</span></span> | <span data-ttu-id="00e30-170">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-170">✔</span></span> |

> [!NOTE]
> * <span data-ttu-id="00e30-171">Teams 平台支持 v1.2 或更早的自适应卡片功能。</span><span class="sxs-lookup"><span data-stu-id="00e30-171">Teams platform supports v1.2 or earlier of Adaptive card features.</span></span>
> * <span data-ttu-id="00e30-172">Teams 平台上的自适应卡片 v1.2 当前不支持媒体元素。</span><span class="sxs-lookup"><span data-stu-id="00e30-172">Media elements are currently not supported in Adaptive card v1.2 on the Teams platform.</span></span>

### <a name="example-of-an-adaptive-card"></a><span data-ttu-id="00e30-173">自适应卡片示例</span><span class="sxs-lookup"><span data-stu-id="00e30-173">Example of an adaptive card</span></span>

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

#### <a name="additional-information-on-adaptive-cards"></a><span data-ttu-id="00e30-175">自适应卡片的其他信息</span><span class="sxs-lookup"><span data-stu-id="00e30-175">Additional information on adaptive cards</span></span>

<span data-ttu-id="00e30-176">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="00e30-176">Bot Framework reference:</span></span>

* [<span data-ttu-id="00e30-177">自适应卡片节点</span><span class="sxs-lookup"><span data-stu-id="00e30-177">Adaptive cards Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [<span data-ttu-id="00e30-178">自适应卡片 C#</span><span class="sxs-lookup"><span data-stu-id="00e30-178">Adaptive card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

## <a name="hero-card"></a><span data-ttu-id="00e30-179">Hero card</span><span class="sxs-lookup"><span data-stu-id="00e30-179">Hero card</span></span>

<span data-ttu-id="00e30-180">通常包含单个大图像、一个或多个按钮和文本的卡片。</span><span class="sxs-lookup"><span data-stu-id="00e30-180">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="00e30-181">支持人物卡片</span><span class="sxs-lookup"><span data-stu-id="00e30-181">Support for hero cards</span></span>

| <span data-ttu-id="00e30-182">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="00e30-182">Bots in Teams</span></span> | <span data-ttu-id="00e30-183">消息扩展</span><span class="sxs-lookup"><span data-stu-id="00e30-183">Messaging Extensions</span></span>  | <span data-ttu-id="00e30-184">连接器</span><span class="sxs-lookup"><span data-stu-id="00e30-184">Connectors</span></span> | <span data-ttu-id="00e30-185">机器人框架</span><span class="sxs-lookup"><span data-stu-id="00e30-185">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00e30-186">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-186">✔</span></span> | <span data-ttu-id="00e30-187">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-187">✔</span></span> | <span data-ttu-id="00e30-188">✖</span><span class="sxs-lookup"><span data-stu-id="00e30-188">✖</span></span> | <span data-ttu-id="00e30-189">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-189">✔</span></span> |

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="00e30-190">Hero 卡片的属性</span><span class="sxs-lookup"><span data-stu-id="00e30-190">Properties of a hero card</span></span>

| <span data-ttu-id="00e30-191">属性</span><span class="sxs-lookup"><span data-stu-id="00e30-191">Property</span></span> | <span data-ttu-id="00e30-192">类型</span><span class="sxs-lookup"><span data-stu-id="00e30-192">Type</span></span>  | <span data-ttu-id="00e30-193">说明</span><span class="sxs-lookup"><span data-stu-id="00e30-193">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="00e30-194">title</span><span class="sxs-lookup"><span data-stu-id="00e30-194">title</span></span> | <span data-ttu-id="00e30-195">格式文本 </span><span class="sxs-lookup"><span data-stu-id="00e30-195">Rich text</span></span> | <span data-ttu-id="00e30-196">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="00e30-196">Title of the card.</span></span> <span data-ttu-id="00e30-197">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="00e30-197">Maximum 2 lines.</span></span> |
| <span data-ttu-id="00e30-198">subtitle</span><span class="sxs-lookup"><span data-stu-id="00e30-198">subtitle</span></span> | <span data-ttu-id="00e30-199">格式文本 </span><span class="sxs-lookup"><span data-stu-id="00e30-199">Rich text</span></span> | <span data-ttu-id="00e30-200">卡片的副标题。</span><span class="sxs-lookup"><span data-stu-id="00e30-200">Subtitle of the card.</span></span> <span data-ttu-id="00e30-201">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="00e30-201">Maximum 2 lines.</span></span>|
| <span data-ttu-id="00e30-202">text</span><span class="sxs-lookup"><span data-stu-id="00e30-202">text</span></span> | <span data-ttu-id="00e30-203">格式文本 </span><span class="sxs-lookup"><span data-stu-id="00e30-203">Rich text</span></span> | <span data-ttu-id="00e30-204">文本显示在副标题下;请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md) 设置，了解格式设置选项。</span><span class="sxs-lookup"><span data-stu-id="00e30-204">Text appears under the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="00e30-205">images</span><span class="sxs-lookup"><span data-stu-id="00e30-205">images</span></span> | <span data-ttu-id="00e30-206">图像数组</span><span class="sxs-lookup"><span data-stu-id="00e30-206">Array of images</span></span> | <span data-ttu-id="00e30-207">显示在卡片顶部的图像。</span><span class="sxs-lookup"><span data-stu-id="00e30-207">Image displayed at top of card.</span></span> <span data-ttu-id="00e30-208">纵横比 16：9。</span><span class="sxs-lookup"><span data-stu-id="00e30-208">Aspect ratio 16:9.</span></span> |
| <span data-ttu-id="00e30-209">按钮</span><span class="sxs-lookup"><span data-stu-id="00e30-209">buttons</span></span> | <span data-ttu-id="00e30-210">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="00e30-210">Array of action objects</span></span> | <span data-ttu-id="00e30-211">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="00e30-211">Set of actions applicable to the current card.</span></span> <span data-ttu-id="00e30-212">最大值 6。</span><span class="sxs-lookup"><span data-stu-id="00e30-212">Maximum 6.</span></span> |
| <span data-ttu-id="00e30-213">点击</span><span class="sxs-lookup"><span data-stu-id="00e30-213">tap</span></span> | <span data-ttu-id="00e30-214">Action 对象</span><span class="sxs-lookup"><span data-stu-id="00e30-214">Action object</span></span> | <span data-ttu-id="00e30-215">当用户点击卡片本身时，将激活此操作。</span><span class="sxs-lookup"><span data-stu-id="00e30-215">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-hero-card"></a><span data-ttu-id="00e30-216">Hero 卡片示例</span><span class="sxs-lookup"><span data-stu-id="00e30-216">Example of a hero card</span></span>

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

### <a name="additional-information-on-hero-cards"></a><span data-ttu-id="00e30-218">有关 hero cards 的其他信息</span><span class="sxs-lookup"><span data-stu-id="00e30-218">Additional information on hero cards</span></span>

<span data-ttu-id="00e30-219">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="00e30-219">Bot Framework reference:</span></span>

* [<span data-ttu-id="00e30-220">Hero card Node</span><span class="sxs-lookup"><span data-stu-id="00e30-220">Hero card Node</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [<span data-ttu-id="00e30-221">Hero card C#</span><span class="sxs-lookup"><span data-stu-id="00e30-221">Hero card C#</span></span>](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a><span data-ttu-id="00e30-222">列表卡</span><span class="sxs-lookup"><span data-stu-id="00e30-222">List card</span></span>

<span data-ttu-id="00e30-223">Teams 已添加列表卡片，以提供列表集合可以提供的功能之外的功能。</span><span class="sxs-lookup"><span data-stu-id="00e30-223">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="00e30-224">列表卡片提供项的滚动列表。</span><span class="sxs-lookup"><span data-stu-id="00e30-224">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="00e30-225">支持列表卡</span><span class="sxs-lookup"><span data-stu-id="00e30-225">Support for list cards</span></span>

| <span data-ttu-id="00e30-226">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="00e30-226">Bots in Teams</span></span> | <span data-ttu-id="00e30-227">消息扩展</span><span class="sxs-lookup"><span data-stu-id="00e30-227">Messaging extensions</span></span>  | <span data-ttu-id="00e30-228">连接器</span><span class="sxs-lookup"><span data-stu-id="00e30-228">Connectors</span></span> | <span data-ttu-id="00e30-229">机器人框架</span><span class="sxs-lookup"><span data-stu-id="00e30-229">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00e30-230">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-230">✔</span></span> | <span data-ttu-id="00e30-231">✖</span><span class="sxs-lookup"><span data-stu-id="00e30-231">✖</span></span> | <span data-ttu-id="00e30-232">✖</span><span class="sxs-lookup"><span data-stu-id="00e30-232">✖</span></span> |<span data-ttu-id="00e30-233">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-233">✔</span></span> |

### <a name="properties-of-a-list-card"></a><span data-ttu-id="00e30-234">列表卡片的属性</span><span class="sxs-lookup"><span data-stu-id="00e30-234">Properties of a list card</span></span>

| <span data-ttu-id="00e30-235">属性</span><span class="sxs-lookup"><span data-stu-id="00e30-235">Property</span></span> | <span data-ttu-id="00e30-236">类型</span><span class="sxs-lookup"><span data-stu-id="00e30-236">Type</span></span>  | <span data-ttu-id="00e30-237">说明</span><span class="sxs-lookup"><span data-stu-id="00e30-237">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="00e30-238">title</span><span class="sxs-lookup"><span data-stu-id="00e30-238">title</span></span> | <span data-ttu-id="00e30-239">格式文本 </span><span class="sxs-lookup"><span data-stu-id="00e30-239">Rich text</span></span> | <span data-ttu-id="00e30-240">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="00e30-240">Title of the card.</span></span> <span data-ttu-id="00e30-241">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="00e30-241">Maximum 2 lines.</span></span>|
| <span data-ttu-id="00e30-242">items</span><span class="sxs-lookup"><span data-stu-id="00e30-242">items</span></span> | <span data-ttu-id="00e30-243">列表项数组</span><span class="sxs-lookup"><span data-stu-id="00e30-243">Array of list items</span></span>  ||
| <span data-ttu-id="00e30-244">按钮</span><span class="sxs-lookup"><span data-stu-id="00e30-244">buttons</span></span> | <span data-ttu-id="00e30-245">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="00e30-245">Array of action objects</span></span> | <span data-ttu-id="00e30-246">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="00e30-246">Set of actions applicable to the current card.</span></span> <span data-ttu-id="00e30-247">最大值 6。</span><span class="sxs-lookup"><span data-stu-id="00e30-247">Maximum 6.</span></span> |

### <a name="example-of-a-list-card"></a><span data-ttu-id="00e30-248">列表卡片示例</span><span class="sxs-lookup"><span data-stu-id="00e30-248">Example of a list card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="00e30-249">Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="00e30-249">Office 365 connector card</span></span>

<span data-ttu-id="00e30-250">Office 365 连接器卡在 Teams 中受支持，在 Bot 框架中不受支持。</span><span class="sxs-lookup"><span data-stu-id="00e30-250">The Office 365 Connector card is supported in Teams, not in Bot Framework.</span></span> <span data-ttu-id="00e30-251">此卡片提供具有多个分区、字段、图像和操作的灵活性布局。</span><span class="sxs-lookup"><span data-stu-id="00e30-251">This card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="00e30-252">此卡封装连接器卡，以便机器人可以使用它。</span><span class="sxs-lookup"><span data-stu-id="00e30-252">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="00e30-253">有关连接器卡和 O365 卡之间的差异，请参阅备注部分。</span><span class="sxs-lookup"><span data-stu-id="00e30-253">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="00e30-254">支持 Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="00e30-254">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="00e30-255">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="00e30-255">Bots in Teams</span></span> | <span data-ttu-id="00e30-256">消息扩展</span><span class="sxs-lookup"><span data-stu-id="00e30-256">Messaging extensions</span></span>  | <span data-ttu-id="00e30-257">连接器</span><span class="sxs-lookup"><span data-stu-id="00e30-257">Connectors</span></span> | <span data-ttu-id="00e30-258">机器人框架</span><span class="sxs-lookup"><span data-stu-id="00e30-258">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00e30-259">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-259">✔</span></span> | <span data-ttu-id="00e30-260">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-260">✔</span></span> | <span data-ttu-id="00e30-261">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-261">✔</span></span> | <span data-ttu-id="00e30-262">✖</span><span class="sxs-lookup"><span data-stu-id="00e30-262">✖</span></span> |

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="00e30-263">Office 365 连接器卡的属性</span><span class="sxs-lookup"><span data-stu-id="00e30-263">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="00e30-264">属性</span><span class="sxs-lookup"><span data-stu-id="00e30-264">Property</span></span> | <span data-ttu-id="00e30-265">类型</span><span class="sxs-lookup"><span data-stu-id="00e30-265">Type</span></span>  | <span data-ttu-id="00e30-266">说明</span><span class="sxs-lookup"><span data-stu-id="00e30-266">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="00e30-267">title</span><span class="sxs-lookup"><span data-stu-id="00e30-267">title</span></span> | <span data-ttu-id="00e30-268">格式文本 </span><span class="sxs-lookup"><span data-stu-id="00e30-268">Rich text</span></span> | <span data-ttu-id="00e30-269">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="00e30-269">Title of the card.</span></span> <span data-ttu-id="00e30-270">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="00e30-270">Maximum 2 lines.</span></span> |
| <span data-ttu-id="00e30-271">摘要</span><span class="sxs-lookup"><span data-stu-id="00e30-271">summary</span></span> | <span data-ttu-id="00e30-272">格式文本 </span><span class="sxs-lookup"><span data-stu-id="00e30-272">Rich text</span></span> | <span data-ttu-id="00e30-273">卡片摘要。</span><span class="sxs-lookup"><span data-stu-id="00e30-273">Summary of the card.</span></span> <span data-ttu-id="00e30-274">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="00e30-274">Maximum 2 lines.</span></span> |
| <span data-ttu-id="00e30-275">text</span><span class="sxs-lookup"><span data-stu-id="00e30-275">text</span></span> | <span data-ttu-id="00e30-276">格式文本 </span><span class="sxs-lookup"><span data-stu-id="00e30-276">Rich text</span></span> | <span data-ttu-id="00e30-277">文本显示在副标题下;请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md) 设置，了解格式设置选项。</span><span class="sxs-lookup"><span data-stu-id="00e30-277">Text appears under the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="00e30-278">themeColor</span><span class="sxs-lookup"><span data-stu-id="00e30-278">themeColor</span></span> | <span data-ttu-id="00e30-279">十六进制字符串</span><span class="sxs-lookup"><span data-stu-id="00e30-279">HEX string</span></span> | <span data-ttu-id="00e30-280">替代应用程序清单中提供的 accentColor 的颜色。</span><span class="sxs-lookup"><span data-stu-id="00e30-280">Color that overrides the accentColor provided from the application manifest.</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="00e30-281">Office 365 连接器卡上的备注</span><span class="sxs-lookup"><span data-stu-id="00e30-281">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="00e30-282">Office 365 连接器卡在 Microsoft Teams 中正常运行，包括 [ActionCard 操作](/outlook/actionable-messages/card-reference#actioncard-action)。</span><span class="sxs-lookup"><span data-stu-id="00e30-282">Office 365 connector cards function properly in Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="00e30-283">从连接器使用连接器卡和在机器人中使用连接器卡之间的一个重要区别是处理卡操作。</span><span class="sxs-lookup"><span data-stu-id="00e30-283">One important difference between using connector cards from a connector and using connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="00e30-284">对于连接器，终结点通过 HTTP POST 接收卡有效负载。</span><span class="sxs-lookup"><span data-stu-id="00e30-284">For a connector, the endpoint receives the card payload through HTTP POST.</span></span>
* <span data-ttu-id="00e30-285">对于自动程序，该操作将触发仅向自动程序发送操作 ID 和 `HttpPOST` `invoke` 正文的活动。</span><span class="sxs-lookup"><span data-stu-id="00e30-285">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="00e30-286">每个连接器卡最多可以显示 10 个部分，每个部分最多可以包含 5 个图像和 5 个操作。</span><span class="sxs-lookup"><span data-stu-id="00e30-286">Each connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="00e30-287">邮件中不会显示任何其他部分、图像或操作。</span><span class="sxs-lookup"><span data-stu-id="00e30-287">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="00e30-288">所有文本字段都支持 Markdown 和 HTML。</span><span class="sxs-lookup"><span data-stu-id="00e30-288">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="00e30-289">您可以通过在邮件中设置 属性来控制哪些部分使用 Markdown `markdown` 或 HTML。</span><span class="sxs-lookup"><span data-stu-id="00e30-289">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="00e30-290">默认情况下，设置为 ;如果要改为使用 `markdown` `true` HTML，则设置为 `markdown` `false` 。</span><span class="sxs-lookup"><span data-stu-id="00e30-290">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="00e30-291">如果指定 `themeColor` 属性，它将替代 `accentColor` 应用清单中的 属性。</span><span class="sxs-lookup"><span data-stu-id="00e30-291">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="00e30-292">若要指定 的呈现样式 `activityImage` ，可以按 `activityImageType` 如下方式设置：</span><span class="sxs-lookup"><span data-stu-id="00e30-292">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows:</span></span>

| <span data-ttu-id="00e30-293">值</span><span class="sxs-lookup"><span data-stu-id="00e30-293">Value</span></span> | <span data-ttu-id="00e30-294">说明</span><span class="sxs-lookup"><span data-stu-id="00e30-294">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="00e30-295">默认值; `activityImage` 将被裁剪为圆形。</span><span class="sxs-lookup"><span data-stu-id="00e30-295">Default; `activityImage` will be cropped as a circle.</span></span> |
| `article` | <span data-ttu-id="00e30-296">`activityImage` 将显示为矩形并保留其纵横比。</span><span class="sxs-lookup"><span data-stu-id="00e30-296">`activityImage` will be displayed as a rectangle and retain its aspect ratio.</span></span> |

<span data-ttu-id="00e30-297">有关连接器卡属性的所有其他详细信息，请参阅 [可操作邮件卡参考](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="00e30-297">For all other details about connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="00e30-298">Microsoft Teams 当前不支持的唯一连接器卡属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="00e30-298">The only connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="00e30-299">`startGroup` (Teams `true`) </span><span class="sxs-lookup"><span data-stu-id="00e30-299">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a><span data-ttu-id="00e30-300">Office 365 连接器卡示例</span><span class="sxs-lookup"><span data-stu-id="00e30-300">Example of an Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="00e30-301">收据卡</span><span class="sxs-lookup"><span data-stu-id="00e30-301">Receipt card</span></span>

<span data-ttu-id="00e30-302">Teams 支持收据卡。</span><span class="sxs-lookup"><span data-stu-id="00e30-302">Teams supports receipt card.</span></span> <span data-ttu-id="00e30-303">它是使机器人能够为用户提供收据的卡片。</span><span class="sxs-lookup"><span data-stu-id="00e30-303">It is a card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="00e30-304">它通常包含要包含在收据上的项目列表，如税务和总信息。</span><span class="sxs-lookup"><span data-stu-id="00e30-304">It typically contains the list of items to include on the receipt, such as tax and total information.</span></span>

### <a name="support-for-receipt-cards"></a><span data-ttu-id="00e30-305">支持收据卡</span><span class="sxs-lookup"><span data-stu-id="00e30-305">Support for receipt cards</span></span>

| <span data-ttu-id="00e30-306">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="00e30-306">Bots in Teams</span></span> | <span data-ttu-id="00e30-307">消息扩展</span><span class="sxs-lookup"><span data-stu-id="00e30-307">Messaging extensions</span></span>  | <span data-ttu-id="00e30-308">连接器</span><span class="sxs-lookup"><span data-stu-id="00e30-308">Connectors</span></span> | <span data-ttu-id="00e30-309">机器人框架</span><span class="sxs-lookup"><span data-stu-id="00e30-309">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00e30-310">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-310">✔</span></span> | <span data-ttu-id="00e30-311">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-311">✔</span></span> | <span data-ttu-id="00e30-312">✖</span><span class="sxs-lookup"><span data-stu-id="00e30-312">✖</span></span> | <span data-ttu-id="00e30-313">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-313">✔</span></span> |

### <a name="example-of-a-receipt-card"></a><span data-ttu-id="00e30-314">收据卡示例</span><span class="sxs-lookup"><span data-stu-id="00e30-314">Example of a receipt card</span></span>

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

### <a name="additional-information-on-receipt-cards"></a><span data-ttu-id="00e30-316">收据卡上的其他信息</span><span class="sxs-lookup"><span data-stu-id="00e30-316">Additional information on receipt cards</span></span>

<span data-ttu-id="00e30-317">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="00e30-317">Bot Framework reference:</span></span>

* [<span data-ttu-id="00e30-318">收据卡节点</span><span class="sxs-lookup"><span data-stu-id="00e30-318">Receipt card Node</span></span>](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="00e30-319">收据卡 C#</span><span class="sxs-lookup"><span data-stu-id="00e30-319">Receipt card C#</span></span>](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a><span data-ttu-id="00e30-320">登录卡</span><span class="sxs-lookup"><span data-stu-id="00e30-320">Signin card</span></span>

<span data-ttu-id="00e30-321">登录卡使机器人可以请求用户登录。</span><span class="sxs-lookup"><span data-stu-id="00e30-321">Signin card enables a bot to request a user to sign in.</span></span> <span data-ttu-id="00e30-322">Teams 中支持的表单与 Bot Framework 支持的表单略有不同。</span><span class="sxs-lookup"><span data-stu-id="00e30-322">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="00e30-323">Teams 中的登录卡类似于 Bot 框架中的登录卡，只不过 Teams 中的登录卡仅支持两项操作： 和 `signin` `openUrl` 。</span><span class="sxs-lookup"><span data-stu-id="00e30-323">The signin card in Teams is similar to the signin card in the Bot Framework except that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="00e30-324">登录 **操作可以从** Teams 中的任意卡使用，而不只是从登录卡使用。</span><span class="sxs-lookup"><span data-stu-id="00e30-324">The **signin action** can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="00e30-325">有关身份验证的更多详细信息，请参阅适用于机器人的 [Microsoft Teams 身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="00e30-325">For more details on authentication, see [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="00e30-326">支持登录卡</span><span class="sxs-lookup"><span data-stu-id="00e30-326">Support for Signin cards</span></span>

| <span data-ttu-id="00e30-327">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="00e30-327">Bots in Teams</span></span> | <span data-ttu-id="00e30-328">消息扩展</span><span class="sxs-lookup"><span data-stu-id="00e30-328">Messaging extensions</span></span>  | <span data-ttu-id="00e30-329">连接器</span><span class="sxs-lookup"><span data-stu-id="00e30-329">Connectors</span></span> | <span data-ttu-id="00e30-330">机器人框架</span><span class="sxs-lookup"><span data-stu-id="00e30-330">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00e30-331">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-331">✔</span></span> | <span data-ttu-id="00e30-332">✖</span><span class="sxs-lookup"><span data-stu-id="00e30-332">✖</span></span> | <span data-ttu-id="00e30-333">✖</span><span class="sxs-lookup"><span data-stu-id="00e30-333">✖</span></span> | <span data-ttu-id="00e30-334">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-334">✔</span></span> |

### <a name="additional-information-on-signin-cards"></a><span data-ttu-id="00e30-335">登录卡的其他信息</span><span class="sxs-lookup"><span data-stu-id="00e30-335">Additional information on signin cards</span></span>

<span data-ttu-id="00e30-336">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="00e30-336">Bot Framework reference:</span></span>

* [<span data-ttu-id="00e30-337">登录卡节点</span><span class="sxs-lookup"><span data-stu-id="00e30-337">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="00e30-338">登录卡 C#</span><span class="sxs-lookup"><span data-stu-id="00e30-338">Signin card C#</span></span>](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a><span data-ttu-id="00e30-339">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="00e30-339">Thumbnail card</span></span>

<span data-ttu-id="00e30-340">通常包含单个缩略图图像、一个或多个按钮和文本的卡片。</span><span class="sxs-lookup"><span data-stu-id="00e30-340">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="00e30-341">对缩略图卡的支持</span><span class="sxs-lookup"><span data-stu-id="00e30-341">Support for thumbnail cards</span></span>

| <span data-ttu-id="00e30-342">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="00e30-342">Bots in Teams</span></span> | <span data-ttu-id="00e30-343">消息扩展</span><span class="sxs-lookup"><span data-stu-id="00e30-343">Messaging extensions</span></span>  | <span data-ttu-id="00e30-344">连接器</span><span class="sxs-lookup"><span data-stu-id="00e30-344">Connectors</span></span> | <span data-ttu-id="00e30-345">机器人框架</span><span class="sxs-lookup"><span data-stu-id="00e30-345">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00e30-346">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-346">✔</span></span> | <span data-ttu-id="00e30-347">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-347">✔</span></span> | <span data-ttu-id="00e30-348">✖</span><span class="sxs-lookup"><span data-stu-id="00e30-348">✖</span></span> | <span data-ttu-id="00e30-349">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-349">✔</span></span> |

![缩略图卡片示例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="00e30-351">缩略图卡片的属性</span><span class="sxs-lookup"><span data-stu-id="00e30-351">Properties of a thumbnail card</span></span>

| <span data-ttu-id="00e30-352">属性</span><span class="sxs-lookup"><span data-stu-id="00e30-352">Property</span></span> | <span data-ttu-id="00e30-353">类型</span><span class="sxs-lookup"><span data-stu-id="00e30-353">Type</span></span>  | <span data-ttu-id="00e30-354">说明</span><span class="sxs-lookup"><span data-stu-id="00e30-354">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="00e30-355">title</span><span class="sxs-lookup"><span data-stu-id="00e30-355">title</span></span> | <span data-ttu-id="00e30-356">格式文本 </span><span class="sxs-lookup"><span data-stu-id="00e30-356">Rich text</span></span> | <span data-ttu-id="00e30-357">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="00e30-357">Title of the card.</span></span> <span data-ttu-id="00e30-358">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="00e30-358">Maximum 2 lines.</span></span>|
| <span data-ttu-id="00e30-359">subtitle</span><span class="sxs-lookup"><span data-stu-id="00e30-359">subtitle</span></span> | <span data-ttu-id="00e30-360">格式文本 </span><span class="sxs-lookup"><span data-stu-id="00e30-360">Rich text</span></span> | <span data-ttu-id="00e30-361">卡片的副标题。</span><span class="sxs-lookup"><span data-stu-id="00e30-361">Subtitle of the card.</span></span> <span data-ttu-id="00e30-362">最多 2 行。</span><span class="sxs-lookup"><span data-stu-id="00e30-362">Maximum 2 lines.</span></span>|
| <span data-ttu-id="00e30-363">text</span><span class="sxs-lookup"><span data-stu-id="00e30-363">text</span></span> | <span data-ttu-id="00e30-364">格式文本 </span><span class="sxs-lookup"><span data-stu-id="00e30-364">Rich text</span></span> | <span data-ttu-id="00e30-365">文本显示在副标题下;请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md) 设置，了解格式设置选项。</span><span class="sxs-lookup"><span data-stu-id="00e30-365">Text appears under the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options.</span></span> |
| <span data-ttu-id="00e30-366">images</span><span class="sxs-lookup"><span data-stu-id="00e30-366">images</span></span> | <span data-ttu-id="00e30-367">图像数组</span><span class="sxs-lookup"><span data-stu-id="00e30-367">Array of images</span></span> | <span data-ttu-id="00e30-368">显示在卡片顶部的图像。</span><span class="sxs-lookup"><span data-stu-id="00e30-368">Image displayed at top of card.</span></span> <span data-ttu-id="00e30-369">纵横比 1：1 (正方形) 。</span><span class="sxs-lookup"><span data-stu-id="00e30-369">Aspect ratio 1:1 (square).</span></span> |
| <span data-ttu-id="00e30-370">按钮</span><span class="sxs-lookup"><span data-stu-id="00e30-370">buttons</span></span> | <span data-ttu-id="00e30-371">操作对象数组</span><span class="sxs-lookup"><span data-stu-id="00e30-371">Array of action objects</span></span> | <span data-ttu-id="00e30-372">适用于当前卡片的操作集。</span><span class="sxs-lookup"><span data-stu-id="00e30-372">Set of actions applicable to the current card.</span></span> <span data-ttu-id="00e30-373">最大值 6。</span><span class="sxs-lookup"><span data-stu-id="00e30-373">Maximum 6.</span></span> |
| <span data-ttu-id="00e30-374">点击</span><span class="sxs-lookup"><span data-stu-id="00e30-374">tap</span></span> | <span data-ttu-id="00e30-375">Action 对象</span><span class="sxs-lookup"><span data-stu-id="00e30-375">Action object</span></span> | <span data-ttu-id="00e30-376">当用户点击卡片本身时，将激活此操作。</span><span class="sxs-lookup"><span data-stu-id="00e30-376">This action will be activated when the user taps on the card itself.</span></span> |

### <a name="example-of-a-thumbnail-card"></a><span data-ttu-id="00e30-377">缩略图卡片示例</span><span class="sxs-lookup"><span data-stu-id="00e30-377">Example of a thumbnail card</span></span>

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

### <a name="additional-information"></a><span data-ttu-id="00e30-378">其他信息</span><span class="sxs-lookup"><span data-stu-id="00e30-378">Additional information</span></span>

<span data-ttu-id="00e30-379">Bot Framework 参考：</span><span class="sxs-lookup"><span data-stu-id="00e30-379">Bot Framework reference:</span></span>

* [<span data-ttu-id="00e30-380">缩略图卡片节点</span><span class="sxs-lookup"><span data-stu-id="00e30-380">Thumbnail card Node</span></span>](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [<span data-ttu-id="00e30-381">缩略图卡片 C#</span><span class="sxs-lookup"><span data-stu-id="00e30-381">Thumbnail card C#</span></span>](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a><span data-ttu-id="00e30-382">卡片集合</span><span class="sxs-lookup"><span data-stu-id="00e30-382">Card collections</span></span>

<span data-ttu-id="00e30-383">Teams 支持卡片集合。</span><span class="sxs-lookup"><span data-stu-id="00e30-383">Teams supports Card collections.</span></span>

<span data-ttu-id="00e30-384">卡片集合： `builder.AttachmentLayout.carousel` 和 `builder.AttachmentLayout.list` 。</span><span class="sxs-lookup"><span data-stu-id="00e30-384">Card collections: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="00e30-385">这些集合包含自适应、hero 或缩略图卡片。</span><span class="sxs-lookup"><span data-stu-id="00e30-385">These collections contain adaptive, hero, or thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="00e30-386">Carousel 集合</span><span class="sxs-lookup"><span data-stu-id="00e30-386">Carousel collection</span></span>

<span data-ttu-id="00e30-387">盘 [选布局](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) 显示卡片的盘选（可选）以及关联的操作按钮。</span><span class="sxs-lookup"><span data-stu-id="00e30-387">The [carousel layout](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="00e30-388">支持木马集合</span><span class="sxs-lookup"><span data-stu-id="00e30-388">Support for carousel collections</span></span>

| <span data-ttu-id="00e30-389">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="00e30-389">Bots in Teams</span></span> | <span data-ttu-id="00e30-390">消息扩展</span><span class="sxs-lookup"><span data-stu-id="00e30-390">Messaging extensions</span></span>  | <span data-ttu-id="00e30-391">连接器</span><span class="sxs-lookup"><span data-stu-id="00e30-391">Connectors</span></span> | <span data-ttu-id="00e30-392">机器人框架</span><span class="sxs-lookup"><span data-stu-id="00e30-392">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00e30-393">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-393">✔</span></span> | <span data-ttu-id="00e30-394">✖</span><span class="sxs-lookup"><span data-stu-id="00e30-394">✖</span></span> | <span data-ttu-id="00e30-395">✖</span><span class="sxs-lookup"><span data-stu-id="00e30-395">✖</span></span> | <span data-ttu-id="00e30-396">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-396">✔</span></span> |

> [!NOTE]
> <span data-ttu-id="00e30-397">一个盘车可显示每封邮件最多 10 张卡片。</span><span class="sxs-lookup"><span data-stu-id="00e30-397">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="properties-of-a-carousel-card"></a><span data-ttu-id="00e30-398">单盘式卡片的属性</span><span class="sxs-lookup"><span data-stu-id="00e30-398">Properties of a carousel card</span></span>

<span data-ttu-id="00e30-399">Carousel 卡片的属性与 Hero 和 Thumbnail 卡片的属性相同。</span><span class="sxs-lookup"><span data-stu-id="00e30-399">Properties of a Carousel card are same as those of the Hero and Thumbnail cards.</span></span>

### <a name="example-of-a-carousel-collection"></a><span data-ttu-id="00e30-400">一个木马集合的示例</span><span class="sxs-lookup"><span data-stu-id="00e30-400">Example of a carousel collection</span></span>

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

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="00e30-402">盘车集合的语法</span><span class="sxs-lookup"><span data-stu-id="00e30-402">Syntax for carousel collections</span></span>

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a><span data-ttu-id="00e30-403">列表集合</span><span class="sxs-lookup"><span data-stu-id="00e30-403">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="00e30-404">支持列表集合</span><span class="sxs-lookup"><span data-stu-id="00e30-404">Support for list collections</span></span>

<span data-ttu-id="00e30-405">列表布局显示卡片的垂直堆叠列表（可选）以及关联的操作按钮。</span><span class="sxs-lookup"><span data-stu-id="00e30-405">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="00e30-406">Teams 中的聊天机器人</span><span class="sxs-lookup"><span data-stu-id="00e30-406">Bots in Teams</span></span> | <span data-ttu-id="00e30-407">消息扩展</span><span class="sxs-lookup"><span data-stu-id="00e30-407">Messaging extensions</span></span>  | <span data-ttu-id="00e30-408">连接器</span><span class="sxs-lookup"><span data-stu-id="00e30-408">Connectors</span></span> | <span data-ttu-id="00e30-409">机器人框架</span><span class="sxs-lookup"><span data-stu-id="00e30-409">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="00e30-410">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-410">✔</span></span> | <span data-ttu-id="00e30-411">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-411">✔</span></span> | <span data-ttu-id="00e30-412">✖</span><span class="sxs-lookup"><span data-stu-id="00e30-412">✖</span></span> | <span data-ttu-id="00e30-413">✔</span><span class="sxs-lookup"><span data-stu-id="00e30-413">✔</span></span> |

### <a name="example-of-a-list-collection"></a><span data-ttu-id="00e30-414">列表集合的示例</span><span class="sxs-lookup"><span data-stu-id="00e30-414">Example of a list collection</span></span>

![卡片列表示例](~/assets/images/cards/list.png)

<span data-ttu-id="00e30-416">属性与 hero 或 thumbnail 卡片的属性相同。</span><span class="sxs-lookup"><span data-stu-id="00e30-416">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="00e30-417">列表最多可显示每封邮件 10 张卡片。</span><span class="sxs-lookup"><span data-stu-id="00e30-417">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="00e30-418">iOS 和 Android 上尚不支持列表卡的一些组合。</span><span class="sxs-lookup"><span data-stu-id="00e30-418">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="00e30-419">列表集合的语法</span><span class="sxs-lookup"><span data-stu-id="00e30-419">Syntax for list collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="00e30-420">Teams 中不支持的卡片</span><span class="sxs-lookup"><span data-stu-id="00e30-420">Cards not supported in Teams</span></span>

<span data-ttu-id="00e30-421">以下卡片由 Bot Framework 实现，但不受 Teams 支持。</span><span class="sxs-lookup"><span data-stu-id="00e30-421">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="00e30-422">动画卡</span><span class="sxs-lookup"><span data-stu-id="00e30-422">Animation cards</span></span>
* <span data-ttu-id="00e30-423">音频卡</span><span class="sxs-lookup"><span data-stu-id="00e30-423">Audio cards</span></span>
* <span data-ttu-id="00e30-424">视频卡</span><span class="sxs-lookup"><span data-stu-id="00e30-424">Video cards</span></span>
