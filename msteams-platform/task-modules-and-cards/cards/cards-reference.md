---
title: 卡片参考
description: 介绍可供团队中的 bot 的所有卡片和卡片操作
keywords: bot 卡片参考
ms.openlocfilehash: 76b9cb7e2508d300deb2e3cd4f392fdb9850062d
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673200"
---
# <a name="cards-reference"></a><span data-ttu-id="675da-104">卡片参考</span><span class="sxs-lookup"><span data-stu-id="675da-104">Cards Reference</span></span>

<span data-ttu-id="675da-105">本部分中列出的卡片在团队的 bot 中受支持。</span><span class="sxs-lookup"><span data-stu-id="675da-105">The cards listed in this section are supported in bots for Teams.</span></span> <span data-ttu-id="675da-106">它们基于由 Bot 框架定义的卡，但团队不支持所有机器人框架卡，并已添加了其自己的部分。</span><span class="sxs-lookup"><span data-stu-id="675da-106">They are based on cards defined by the Bot Framework, but Teams does not support all Bot Framework cards and has added some of its own.</span></span> <span data-ttu-id="675da-107">下面的参考中称为不同之处。</span><span class="sxs-lookup"><span data-stu-id="675da-107">Differences are called out in the references below.</span></span>

## <a name="card-examples"></a><span data-ttu-id="675da-108">卡片示例</span><span class="sxs-lookup"><span data-stu-id="675da-108">Card examples</span></span>

<span data-ttu-id="675da-109">您可以在机器人生成器 SDK （v3）的文档中找到有关如何使用卡片的其他信息。</span><span class="sxs-lookup"><span data-stu-id="675da-109">You can find additional information on how to use cards in the documentation for the Bot Builder SDK (v3).</span></span> <span data-ttu-id="675da-110">GitHub 上的 Microsoft/BotBuilder-示例存储库中也提供了代码示例。</span><span class="sxs-lookup"><span data-stu-id="675da-110">There are also code samples available in the Microsoft/BotBuilder-Samples repository on GitHub.</span></span>

* <span data-ttu-id="675da-111">.NET</span><span class="sxs-lookup"><span data-stu-id="675da-111">.NET</span></span>
  * [<span data-ttu-id="675da-112">将卡片添加为邮件附件</span><span class="sxs-lookup"><span data-stu-id="675da-112">Add cards as attachments to messages</span></span>](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [<span data-ttu-id="675da-113">卡片示例代码（Bot 生成器 v3）</span><span class="sxs-lookup"><span data-stu-id="675da-113">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* <span data-ttu-id="675da-114">Node.js</span><span class="sxs-lookup"><span data-stu-id="675da-114">Node.js</span></span>
  * [<span data-ttu-id="675da-115">将卡片添加为邮件附件</span><span class="sxs-lookup"><span data-stu-id="675da-115">Add cards as attachments to messages</span></span>](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [<span data-ttu-id="675da-116">卡片示例代码（Bot 生成器 v3）</span><span class="sxs-lookup"><span data-stu-id="675da-116">Cards sample code (Bot Builder v3)</span></span>](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a><span data-ttu-id="675da-117">卡片类型</span><span class="sxs-lookup"><span data-stu-id="675da-117">Types of cards</span></span>

<span data-ttu-id="675da-118">此表显示了可供您使用的卡片类型。</span><span class="sxs-lookup"><span data-stu-id="675da-118">This table shows the types of cards available to you.</span></span>

| <span data-ttu-id="675da-119">卡片类型</span><span class="sxs-lookup"><span data-stu-id="675da-119">Card Type</span></span> | <span data-ttu-id="675da-120">说明</span><span class="sxs-lookup"><span data-stu-id="675da-120">Description</span></span> |
| --- | --- |
| [<span data-ttu-id="675da-121">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="675da-121">Adaptive Card</span></span>](#adaptive-card) | <span data-ttu-id="675da-122">可包含文本、语音、图像、按钮和输入字段的任意组合的高度可自定义卡片。</span><span class="sxs-lookup"><span data-stu-id="675da-122">Highly customizable card that can contain any combination of text, speech, images, buttons and input fields.</span></span> |
| [<span data-ttu-id="675da-123">英雄卡片</span><span class="sxs-lookup"><span data-stu-id="675da-123">Hero Card</span></span>](#hero-card) | <span data-ttu-id="675da-124">通常包含一个大图像、一个或多个按钮以及少量文本。</span><span class="sxs-lookup"><span data-stu-id="675da-124">Typically contains a single large image, one or more buttons, and a small amount of text.</span></span> |
| [<span data-ttu-id="675da-125">列出卡片</span><span class="sxs-lookup"><span data-stu-id="675da-125">List Card</span></span>](#list-card) | <span data-ttu-id="675da-126">项目的滚动列表。</span><span class="sxs-lookup"><span data-stu-id="675da-126">A scrolling list of items.</span></span> |
| [<span data-ttu-id="675da-127">Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="675da-127">Office 365 Connector Card</span></span>](#office-365-connector-card) | <span data-ttu-id="675da-128">具有多个节、字段、图像和操作的灵活布局。</span><span class="sxs-lookup"><span data-stu-id="675da-128">Flexible layout with multiple sections, fields, images and actions.</span></span> |
| [<span data-ttu-id="675da-129">收据卡</span><span class="sxs-lookup"><span data-stu-id="675da-129">Receipt Card</span></span>](#receipt-card) | <span data-ttu-id="675da-130">向用户提供收据。</span><span class="sxs-lookup"><span data-stu-id="675da-130">Provides a receipt to the user.</span></span> |
| [<span data-ttu-id="675da-131">登录卡片</span><span class="sxs-lookup"><span data-stu-id="675da-131">Signin Card</span></span>](#signin-card) | <span data-ttu-id="675da-132">启用机器人以请求用户登录。</span><span class="sxs-lookup"><span data-stu-id="675da-132">Enables a bot to request that a user sign in.</span></span> |
| [<span data-ttu-id="675da-133">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="675da-133">Thumbnail Card</span></span>](#thumbnail-card) | <span data-ttu-id="675da-134">通常包含一个缩略图图像、一些短文本以及一个或多个按钮。</span><span class="sxs-lookup"><span data-stu-id="675da-134">Typically contains a single thumbnail image, some short text, and one or more buttons.</span></span> |
| [<span data-ttu-id="675da-135">卡片集合</span><span class="sxs-lookup"><span data-stu-id="675da-135">Card Collections</span></span>](#card-collections) | <span data-ttu-id="675da-136">用于在单个响应中返回多个项目</span><span class="sxs-lookup"><span data-stu-id="675da-136">Used to return multiple items in a single response</span></span> |

## <a name="common-properties-for-all-cards"></a><span data-ttu-id="675da-137">所有卡片的通用属性</span><span class="sxs-lookup"><span data-stu-id="675da-137">Common properties for all cards</span></span>

### <a name="inline-card-images"></a><span data-ttu-id="675da-138">内嵌卡片图像</span><span class="sxs-lookup"><span data-stu-id="675da-138">Inline card images</span></span>

<span data-ttu-id="675da-139">您的卡片可以通过包含指向您的公开可用图像的链接来包含内嵌图像。</span><span class="sxs-lookup"><span data-stu-id="675da-139">Your card can contain an inline image by including a link to your publically available image.</span></span> <span data-ttu-id="675da-140">出于性能考虑，强烈建议您将映像托管在公共内容传递网络（CDN）上。</span><span class="sxs-lookup"><span data-stu-id="675da-140">For performance purposes we highly recommend you host your image on a public content-delivery network (CDN).</span></span>

<span data-ttu-id="675da-141">图像在大小上向上或向下放大，同时保持纵横比以覆盖图像区域，然后从中心裁剪以达到适合该卡片的纵横比。</span><span class="sxs-lookup"><span data-stu-id="675da-141">Images are scaled up or down in size while maintaining the aspect ratio to cover the image area, and then cropped from center to achieve the appropriate aspect ratio for the card.</span></span>

<span data-ttu-id="675da-142">图像必须最多为1024×1024和 1 MB （PNG、JPEG 或 GIF 格式）;不正式支持动画 GIF。</span><span class="sxs-lookup"><span data-stu-id="675da-142">Images must be at most 1024×1024 and 1 MB in PNG, JPEG, or GIF format; animated GIF is not officially supported.</span></span>

| <span data-ttu-id="675da-143">属性</span><span class="sxs-lookup"><span data-stu-id="675da-143">Property</span></span> | <span data-ttu-id="675da-144">类型</span><span class="sxs-lookup"><span data-stu-id="675da-144">Type</span></span>  | <span data-ttu-id="675da-145">说明</span><span class="sxs-lookup"><span data-stu-id="675da-145">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="675da-146">url</span><span class="sxs-lookup"><span data-stu-id="675da-146">url</span></span> | <span data-ttu-id="675da-147">URL</span><span class="sxs-lookup"><span data-stu-id="675da-147">URL</span></span> | <span data-ttu-id="675da-148">指向图像的 HTTPS URL</span><span class="sxs-lookup"><span data-stu-id="675da-148">HTTPS URL to the image</span></span> |
| <span data-ttu-id="675da-149">alt</span><span class="sxs-lookup"><span data-stu-id="675da-149">alt</span></span> | <span data-ttu-id="675da-150">String</span><span class="sxs-lookup"><span data-stu-id="675da-150">String</span></span> | <span data-ttu-id="675da-151">图像的可访问说明</span><span class="sxs-lookup"><span data-stu-id="675da-151">Accessible description of the image</span></span> |

### <a name="buttons"></a><span data-ttu-id="675da-152">按钮</span><span class="sxs-lookup"><span data-stu-id="675da-152">Buttons</span></span>

<span data-ttu-id="675da-153">按钮以堆叠方式显示在卡片底部。</span><span class="sxs-lookup"><span data-stu-id="675da-153">Buttons are shown stacked at the bottom of the card.</span></span> <span data-ttu-id="675da-154">按钮文本总是在单行上，如果文本超出按钮宽度，则将被截尾取整。</span><span class="sxs-lookup"><span data-stu-id="675da-154">Button text is always on a single line and will be truncated if the text exceeds the button width.</span></span> <span data-ttu-id="675da-155">不会显示超出卡片支持的最大数量的任何其他按钮。</span><span class="sxs-lookup"><span data-stu-id="675da-155">Any additional buttons beyond the maximum number supported by the card will not be shown.</span></span>

<span data-ttu-id="675da-156">有关详细信息，请参阅[卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="675da-156">See [Card Actions](~/task-modules-and-cards/cards/cards-actions.md) for more information.</span></span>

### <a name="card-formatting"></a><span data-ttu-id="675da-157">卡片格式</span><span class="sxs-lookup"><span data-stu-id="675da-157">Card Formatting</span></span>

<span data-ttu-id="675da-158">有关卡片中的文本格式的详细信息，请参阅[卡片格式](~/task-modules-and-cards/cards/cards-format.md)。</span><span class="sxs-lookup"><span data-stu-id="675da-158">See [Card Formatting](~/task-modules-and-cards/cards/cards-format.md) for more information on text formatting in cards.</span></span>

## <a name="adaptive-card"></a><span data-ttu-id="675da-159">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="675da-159">Adaptive card</span></span>

> [!NOTE]
> <span data-ttu-id="675da-160">对于所有用户，仅支持1.0 版自适应卡。</span><span class="sxs-lookup"><span data-stu-id="675da-160">Only version 1.0 of Adaptive Cards is supported for all users.</span></span> <span data-ttu-id="675da-161">版本1.2 当前仅适用于开发人员预览版</span><span class="sxs-lookup"><span data-stu-id="675da-161">Version 1.2 is currently available only in Developer Preview</span></span>

<span data-ttu-id="675da-162">一种可自定义的卡片，可包含文本、语音、图像、按钮和输入字段的任意组合。</span><span class="sxs-lookup"><span data-stu-id="675da-162">A customizable card that can contain any combination of text, speech, images, buttons, and input fields.</span></span>

### <a name="support-for-adaptive-cards"></a><span data-ttu-id="675da-163">对自适应卡片的支持</span><span class="sxs-lookup"><span data-stu-id="675da-163">Support for Adaptive cards</span></span>

| <span data-ttu-id="675da-164">团队中的 bot</span><span class="sxs-lookup"><span data-stu-id="675da-164">Bots in Teams</span></span> | <span data-ttu-id="675da-165">邮件扩展</span><span class="sxs-lookup"><span data-stu-id="675da-165">Messaging Extensions</span></span>  | <span data-ttu-id="675da-166">连接器</span><span class="sxs-lookup"><span data-stu-id="675da-166">Connectors</span></span> | <span data-ttu-id="675da-167">Bot 框架</span><span class="sxs-lookup"><span data-stu-id="675da-167">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="675da-168">✔</span><span class="sxs-lookup"><span data-stu-id="675da-168">✔</span></span> | <span data-ttu-id="675da-169">✔</span><span class="sxs-lookup"><span data-stu-id="675da-169">✔</span></span> | <span data-ttu-id="675da-170">✖</span><span class="sxs-lookup"><span data-stu-id="675da-170">✖</span></span> | <span data-ttu-id="675da-171">✔</span><span class="sxs-lookup"><span data-stu-id="675da-171">✔</span></span> |
|

### <a name="example-adaptive-card"></a><span data-ttu-id="675da-172">自适应卡片示例</span><span class="sxs-lookup"><span data-stu-id="675da-172">Example Adaptive card</span></span>

![自适应卡片卡的示例](~/assets/images/cards/adaptivecard.png)

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

#### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="675da-174">有关自适应卡片的详细信息</span><span class="sxs-lookup"><span data-stu-id="675da-174">For more information on Adaptive cards</span></span>

* [<span data-ttu-id="675da-175">自适应卡片概述</span><span class="sxs-lookup"><span data-stu-id="675da-175">Adaptive Cards Overview</span></span>](/adaptive-cards/)
* [<span data-ttu-id="675da-176">团队中的自适应卡片操作</span><span class="sxs-lookup"><span data-stu-id="675da-176">Adaptive card actions in Teams</span></span>](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a><span data-ttu-id="675da-177">英雄卡片</span><span class="sxs-lookup"><span data-stu-id="675da-177">Hero card</span></span>

<span data-ttu-id="675da-178">通常包含一个大图像（一个或多个按钮和文本）的卡片。</span><span class="sxs-lookup"><span data-stu-id="675da-178">A card that typically contains a single large image, one or more buttons and text.</span></span>

### <a name="support-for-hero-cards"></a><span data-ttu-id="675da-179">对英雄卡片的支持</span><span class="sxs-lookup"><span data-stu-id="675da-179">Support for Hero cards</span></span>

| <span data-ttu-id="675da-180">团队中的 bot</span><span class="sxs-lookup"><span data-stu-id="675da-180">Bots in Teams</span></span> | <span data-ttu-id="675da-181">邮件扩展</span><span class="sxs-lookup"><span data-stu-id="675da-181">Messaging Extensions</span></span>  | <span data-ttu-id="675da-182">连接器</span><span class="sxs-lookup"><span data-stu-id="675da-182">Connectors</span></span> | <span data-ttu-id="675da-183">Bot 框架</span><span class="sxs-lookup"><span data-stu-id="675da-183">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="675da-184">✔</span><span class="sxs-lookup"><span data-stu-id="675da-184">✔</span></span> | <span data-ttu-id="675da-185">✔</span><span class="sxs-lookup"><span data-stu-id="675da-185">✔</span></span> | <span data-ttu-id="675da-186">✖</span><span class="sxs-lookup"><span data-stu-id="675da-186">✖</span></span> | <span data-ttu-id="675da-187">✔</span><span class="sxs-lookup"><span data-stu-id="675da-187">✔</span></span> |
|

### <a name="properties-of-a-hero-card"></a><span data-ttu-id="675da-188">一个英雄卡片的属性</span><span class="sxs-lookup"><span data-stu-id="675da-188">Properties of a Hero card</span></span>

| <span data-ttu-id="675da-189">属性</span><span class="sxs-lookup"><span data-stu-id="675da-189">Property</span></span> | <span data-ttu-id="675da-190">类型</span><span class="sxs-lookup"><span data-stu-id="675da-190">Type</span></span>  | <span data-ttu-id="675da-191">说明</span><span class="sxs-lookup"><span data-stu-id="675da-191">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="675da-192">title</span><span class="sxs-lookup"><span data-stu-id="675da-192">title</span></span> | <span data-ttu-id="675da-193">格式文本 </span><span class="sxs-lookup"><span data-stu-id="675da-193">Rich text</span></span> | <span data-ttu-id="675da-194">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="675da-194">Title of the card.</span></span> <span data-ttu-id="675da-195">最多2行;当前不支持的格式</span><span class="sxs-lookup"><span data-stu-id="675da-195">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="675da-196">字幕</span><span class="sxs-lookup"><span data-stu-id="675da-196">subtitle</span></span> | <span data-ttu-id="675da-197">格式文本 </span><span class="sxs-lookup"><span data-stu-id="675da-197">Rich text</span></span> | <span data-ttu-id="675da-198">卡片的副标题。</span><span class="sxs-lookup"><span data-stu-id="675da-198">Subtitle of the card.</span></span> <span data-ttu-id="675da-199">最多2行;当前不支持的格式</span><span class="sxs-lookup"><span data-stu-id="675da-199">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="675da-200">text</span><span class="sxs-lookup"><span data-stu-id="675da-200">text</span></span> | <span data-ttu-id="675da-201">格式文本 </span><span class="sxs-lookup"><span data-stu-id="675da-201">Rich text</span></span> | <span data-ttu-id="675da-202">文本显示在副标题的正下方;请参阅[卡片格式](~/task-modules-and-cards/cards/cards-format.md)设置选项</span><span class="sxs-lookup"><span data-stu-id="675da-202">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="675da-203">图形</span><span class="sxs-lookup"><span data-stu-id="675da-203">images</span></span> | <span data-ttu-id="675da-204">图像数组</span><span class="sxs-lookup"><span data-stu-id="675da-204">Array of images</span></span> | <span data-ttu-id="675da-205">显示在卡片顶部的图像。</span><span class="sxs-lookup"><span data-stu-id="675da-205">Image displayed at top of card.</span></span> <span data-ttu-id="675da-206">纵横比16:9</span><span class="sxs-lookup"><span data-stu-id="675da-206">Aspect ratio 16:9</span></span> |
| <span data-ttu-id="675da-207">按钮</span><span class="sxs-lookup"><span data-stu-id="675da-207">buttons</span></span> | <span data-ttu-id="675da-208">Action 对象的数组</span><span class="sxs-lookup"><span data-stu-id="675da-208">Array of action objects</span></span> | <span data-ttu-id="675da-209">适用于当前卡片的一组操作。</span><span class="sxs-lookup"><span data-stu-id="675da-209">Set of actions applicable to the current card.</span></span> <span data-ttu-id="675da-210">最大6</span><span class="sxs-lookup"><span data-stu-id="675da-210">Maximum 6</span></span> |
| <span data-ttu-id="675da-211">即可</span><span class="sxs-lookup"><span data-stu-id="675da-211">tap</span></span> | <span data-ttu-id="675da-212">Action 对象</span><span class="sxs-lookup"><span data-stu-id="675da-212">Action object</span></span> | <span data-ttu-id="675da-213">当用户点击卡片本身时，将激活此操作</span><span class="sxs-lookup"><span data-stu-id="675da-213">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-hero-card"></a><span data-ttu-id="675da-214">示例英雄卡片</span><span class="sxs-lookup"><span data-stu-id="675da-214">Example Hero card</span></span>

![一个英雄卡片示例](~/assets/images/cards/hero.png)

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

### <a name="for-more-information-on-hero-cards"></a><span data-ttu-id="675da-216">有关英雄卡片的详细信息</span><span class="sxs-lookup"><span data-stu-id="675da-216">For more information on Hero cards</span></span>

<span data-ttu-id="675da-217">Bot 框架参考：</span><span class="sxs-lookup"><span data-stu-id="675da-217">Bot Framework reference:</span></span>

* [<span data-ttu-id="675da-218">"英雄卡片" 节点</span><span class="sxs-lookup"><span data-stu-id="675da-218">Hero card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [<span data-ttu-id="675da-219">英雄卡片 C#</span><span class="sxs-lookup"><span data-stu-id="675da-219">Hero card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0)

## <a name="list-card"></a><span data-ttu-id="675da-220">列出卡片</span><span class="sxs-lookup"><span data-stu-id="675da-220">List card</span></span>

<span data-ttu-id="675da-221">团队添加了列表卡，以提供列表集合可以提供的功能之外的功能。</span><span class="sxs-lookup"><span data-stu-id="675da-221">The list card has been added by Teams to provide functions beyond what the list collection can provide.</span></span> <span data-ttu-id="675da-222">清单卡片提供了项的滚动列表。</span><span class="sxs-lookup"><span data-stu-id="675da-222">The list card provides a scrolling list of items.</span></span>

### <a name="support-for-list-cards"></a><span data-ttu-id="675da-223">支持列表卡片</span><span class="sxs-lookup"><span data-stu-id="675da-223">Support for List cards</span></span>

| <span data-ttu-id="675da-224">团队中的 bot</span><span class="sxs-lookup"><span data-stu-id="675da-224">Bots in Teams</span></span> | <span data-ttu-id="675da-225">邮件扩展</span><span class="sxs-lookup"><span data-stu-id="675da-225">Messaging Extensions</span></span>  | <span data-ttu-id="675da-226">连接器</span><span class="sxs-lookup"><span data-stu-id="675da-226">Connectors</span></span> | <span data-ttu-id="675da-227">Bot 框架</span><span class="sxs-lookup"><span data-stu-id="675da-227">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="675da-228">✔</span><span class="sxs-lookup"><span data-stu-id="675da-228">✔</span></span> | <span data-ttu-id="675da-229">✖</span><span class="sxs-lookup"><span data-stu-id="675da-229">✖</span></span> | <span data-ttu-id="675da-230">✖</span><span class="sxs-lookup"><span data-stu-id="675da-230">✖</span></span> |<span data-ttu-id="675da-231">✔</span><span class="sxs-lookup"><span data-stu-id="675da-231">✔</span></span> |
|

### <a name="properties-of-a-list-card"></a><span data-ttu-id="675da-232">列表卡的属性</span><span class="sxs-lookup"><span data-stu-id="675da-232">Properties of a List card</span></span>

| <span data-ttu-id="675da-233">属性</span><span class="sxs-lookup"><span data-stu-id="675da-233">Property</span></span> | <span data-ttu-id="675da-234">类型</span><span class="sxs-lookup"><span data-stu-id="675da-234">Type</span></span>  | <span data-ttu-id="675da-235">说明</span><span class="sxs-lookup"><span data-stu-id="675da-235">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="675da-236">title</span><span class="sxs-lookup"><span data-stu-id="675da-236">title</span></span> | <span data-ttu-id="675da-237">格式文本 </span><span class="sxs-lookup"><span data-stu-id="675da-237">Rich text</span></span> | <span data-ttu-id="675da-238">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="675da-238">Title of the card.</span></span> <span data-ttu-id="675da-239">最多2行;当前不支持的格式</span><span class="sxs-lookup"><span data-stu-id="675da-239">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="675da-240">items</span><span class="sxs-lookup"><span data-stu-id="675da-240">items</span></span> | <span data-ttu-id="675da-241">列表项的数组</span><span class="sxs-lookup"><span data-stu-id="675da-241">Array of list items</span></span>  ||
| <span data-ttu-id="675da-242">按钮</span><span class="sxs-lookup"><span data-stu-id="675da-242">buttons</span></span> | <span data-ttu-id="675da-243">Action 对象的数组</span><span class="sxs-lookup"><span data-stu-id="675da-243">Array of action objects</span></span> | <span data-ttu-id="675da-244">适用于当前卡片的一组操作。</span><span class="sxs-lookup"><span data-stu-id="675da-244">Set of actions applicable to the current card.</span></span> <span data-ttu-id="675da-245">最大6。</span><span class="sxs-lookup"><span data-stu-id="675da-245">Maximum 6.</span></span> <span data-ttu-id="675da-246">不会在移动设备上呈现。</span><span class="sxs-lookup"><span data-stu-id="675da-246">Does not render on mobile.</span></span> |
|

### <a name="example-list-card"></a><span data-ttu-id="675da-247">列表卡片示例</span><span class="sxs-lookup"><span data-stu-id="675da-247">Example List card</span></span>

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

## <a name="office-365-connector-card"></a><span data-ttu-id="675da-248">Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="675da-248">Office 365 connector card</span></span>

<span data-ttu-id="675da-249">在团队中受支持，而不是在 Bot 框架中。</span><span class="sxs-lookup"><span data-stu-id="675da-249">Supported in Teams, not in Bot Framework.</span></span>

<span data-ttu-id="675da-250">Office 365 连接器卡提供了具有多个节、字段、图像和操作的灵活布局。</span><span class="sxs-lookup"><span data-stu-id="675da-250">The Office 365 Connector card provides a flexible layout with multiple sections, fields, images, and actions.</span></span> <span data-ttu-id="675da-251">此卡封装连接器卡，以便 bot 可以使用它。</span><span class="sxs-lookup"><span data-stu-id="675da-251">This card encapsulates a connector card so that it can be used by bots.</span></span> <span data-ttu-id="675da-252">有关连接器卡和 O365 卡之间的差异，请参阅 "注释" 部分。</span><span class="sxs-lookup"><span data-stu-id="675da-252">See the notes section for differences between connector cards and the O365 card.</span></span>

### <a name="support-for-office-365-connector-cards"></a><span data-ttu-id="675da-253">支持 Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="675da-253">Support for Office 365 connector cards</span></span>

| <span data-ttu-id="675da-254">团队中的 bot</span><span class="sxs-lookup"><span data-stu-id="675da-254">Bots in Teams</span></span> | <span data-ttu-id="675da-255">邮件扩展</span><span class="sxs-lookup"><span data-stu-id="675da-255">Messaging Extensions</span></span>  | <span data-ttu-id="675da-256">连接器</span><span class="sxs-lookup"><span data-stu-id="675da-256">Connectors</span></span> | <span data-ttu-id="675da-257">Bot 框架</span><span class="sxs-lookup"><span data-stu-id="675da-257">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="675da-258">✔</span><span class="sxs-lookup"><span data-stu-id="675da-258">✔</span></span> | <span data-ttu-id="675da-259">✔</span><span class="sxs-lookup"><span data-stu-id="675da-259">✔</span></span> | <span data-ttu-id="675da-260">✔</span><span class="sxs-lookup"><span data-stu-id="675da-260">✔</span></span> | <span data-ttu-id="675da-261">✖</span><span class="sxs-lookup"><span data-stu-id="675da-261">✖</span></span> |
|

### <a name="properties-of-the-office-365-connector-card"></a><span data-ttu-id="675da-262">Office 365 连接器卡的属性</span><span class="sxs-lookup"><span data-stu-id="675da-262">Properties of the Office 365 connector card</span></span>

| <span data-ttu-id="675da-263">属性</span><span class="sxs-lookup"><span data-stu-id="675da-263">Property</span></span> | <span data-ttu-id="675da-264">类型</span><span class="sxs-lookup"><span data-stu-id="675da-264">Type</span></span>  | <span data-ttu-id="675da-265">说明</span><span class="sxs-lookup"><span data-stu-id="675da-265">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="675da-266">title</span><span class="sxs-lookup"><span data-stu-id="675da-266">title</span></span> | <span data-ttu-id="675da-267">格式文本 </span><span class="sxs-lookup"><span data-stu-id="675da-267">Rich text</span></span> | <span data-ttu-id="675da-268">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="675da-268">Title of the card.</span></span> <span data-ttu-id="675da-269">最多2行;当前不支持的格式</span><span class="sxs-lookup"><span data-stu-id="675da-269">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="675da-270">摘要</span><span class="sxs-lookup"><span data-stu-id="675da-270">summary</span></span> | <span data-ttu-id="675da-271">格式文本 </span><span class="sxs-lookup"><span data-stu-id="675da-271">Rich text</span></span> | <span data-ttu-id="675da-272">卡片摘要。</span><span class="sxs-lookup"><span data-stu-id="675da-272">Summary of the card.</span></span> <span data-ttu-id="675da-273">最多2行;当前不支持的格式</span><span class="sxs-lookup"><span data-stu-id="675da-273">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="675da-274">text</span><span class="sxs-lookup"><span data-stu-id="675da-274">text</span></span> | <span data-ttu-id="675da-275">格式文本 </span><span class="sxs-lookup"><span data-stu-id="675da-275">Rich text</span></span> | <span data-ttu-id="675da-276">文本显示在副标题的正下方;请参阅[卡片格式](~/task-modules-and-cards/cards/cards-format.md)设置选项</span><span class="sxs-lookup"><span data-stu-id="675da-276">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="675da-277">themeColor</span><span class="sxs-lookup"><span data-stu-id="675da-277">themeColor</span></span> | <span data-ttu-id="675da-278">十六进制字符串</span><span class="sxs-lookup"><span data-stu-id="675da-278">HEX string</span></span> | <span data-ttu-id="675da-279">重写从应用程序清单提供的 accentColor 的颜色</span><span class="sxs-lookup"><span data-stu-id="675da-279">color that overrides the accentColor provided from the application manifest</span></span> |

### <a name="notes-on-the-office-365-connector-card"></a><span data-ttu-id="675da-280">Office 365 连接器卡上的备注</span><span class="sxs-lookup"><span data-stu-id="675da-280">Notes on the Office 365 connector card</span></span>

<span data-ttu-id="675da-281">Office 365 连接器卡在 Microsoft 团队中正常工作，包括[ActionCard 操作](/outlook/actionable-messages/card-reference#actioncard-action)。</span><span class="sxs-lookup"><span data-stu-id="675da-281">Office 365 Connector cards function properly on Microsoft Teams, including [ActionCard actions](/outlook/actionable-messages/card-reference#actioncard-action).</span></span>

<span data-ttu-id="675da-282">使用连接器中的连接器卡和在你的 bot 中使用连接器卡的一个重要区别是处理智能卡操作。</span><span class="sxs-lookup"><span data-stu-id="675da-282">One important difference between using Connector cards from a Connector and using Connector cards in your bot is the handling of card actions.</span></span>

* <span data-ttu-id="675da-283">对于连接器，终结点通过 HTTP POST 接收卡有效负载。</span><span class="sxs-lookup"><span data-stu-id="675da-283">For a Connector, the endpoint receives the card payload via HTTP POST.</span></span>
* <span data-ttu-id="675da-284">对于 bot，该`HttpPOST`操作触发仅将`invoke`操作 ID 和正文发送到 bot 的活动。</span><span class="sxs-lookup"><span data-stu-id="675da-284">For a bot, the `HttpPOST` action triggers an `invoke` activity that sends only the action ID and body to the bot.</span></span>

<span data-ttu-id="675da-285">每个连接器卡最多可以显示10个部分，每个部分最多可包含5个图像和5个操作。</span><span class="sxs-lookup"><span data-stu-id="675da-285">Each Connector card can display a maximum of 10 sections, and each section can contain a maximum of 5 images and 5 actions.</span></span>

> [!NOTE]
> <span data-ttu-id="675da-286">将不会显示邮件中的任何其他节、图像或操作。</span><span class="sxs-lookup"><span data-stu-id="675da-286">Any additional sections, images, or actions in a message will not appear.</span></span>

<span data-ttu-id="675da-287">所有文本字段都支持 Markdown 和 HTML。</span><span class="sxs-lookup"><span data-stu-id="675da-287">All text fields support Markdown and HTML.</span></span> <span data-ttu-id="675da-288">您可以通过在邮件中设置`markdown`属性来控制哪些部分使用 MARKDOWN 或 HTML。</span><span class="sxs-lookup"><span data-stu-id="675da-288">You can control which sections use Markdown or HTML by setting the `markdown` property in a message.</span></span> <span data-ttu-id="675da-289">默认情况下`markdown` ，设置为`true`;如果要改为使用 HTML，则将`markdown`设置`false`为。</span><span class="sxs-lookup"><span data-stu-id="675da-289">By default, `markdown` is set to `true`; if you want to use HTML instead, set `markdown` to `false`.</span></span>

<span data-ttu-id="675da-290">如果指定`themeColor`属性，它将替代应用程序`accentColor`清单中的属性。</span><span class="sxs-lookup"><span data-stu-id="675da-290">If you specify the `themeColor` property, it overrides the `accentColor` property in the app manifest.</span></span>

<span data-ttu-id="675da-291">若要指定的呈现样式`activityImage`，可以按如下`activityImageType`所示进行设置。</span><span class="sxs-lookup"><span data-stu-id="675da-291">To specify the rendering style for `activityImage`, you can set `activityImageType` as follows.</span></span>

| <span data-ttu-id="675da-292">值</span><span class="sxs-lookup"><span data-stu-id="675da-292">Value</span></span> | <span data-ttu-id="675da-293">说明</span><span class="sxs-lookup"><span data-stu-id="675da-293">Description</span></span> |
| --- | --- |
| `avatar` | <span data-ttu-id="675da-294">设置`activityImage`将裁剪为圆形</span><span class="sxs-lookup"><span data-stu-id="675da-294">Default; `activityImage` will be cropped as a circle</span></span> |
| `article` | <span data-ttu-id="675da-295">`activityImage`将显示为一个矩形，并保持其纵横比</span><span class="sxs-lookup"><span data-stu-id="675da-295">`activityImage` will be displayed as a rectangle and retain its aspect ratio</span></span> |

<span data-ttu-id="675da-296">有关连接器卡属性的所有其他详细信息，请参阅可[操作邮件卡参考](/outlook/actionable-messages/card-reference)。</span><span class="sxs-lookup"><span data-stu-id="675da-296">For all other details about Connector card properties, see the [Actionable message card reference](/outlook/actionable-messages/card-reference).</span></span> <span data-ttu-id="675da-297">Microsoft 团队目前不支持的连接器卡片属性如下所示：</span><span class="sxs-lookup"><span data-stu-id="675da-297">The only Connector card properties that Microsoft Teams does not currently support are as follows:</span></span>

* `heroImage`
* `hideOriginalBody`
* <span data-ttu-id="675da-298">`startGroup`（始终按`true`团队处理）</span><span class="sxs-lookup"><span data-stu-id="675da-298">`startGroup` (always treated as `true` in Teams)</span></span>
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a><span data-ttu-id="675da-299">示例 Office 365 连接器卡</span><span class="sxs-lookup"><span data-stu-id="675da-299">Example Office 365 connector card</span></span>

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

## <a name="receipt-card"></a><span data-ttu-id="675da-300">收据卡</span><span class="sxs-lookup"><span data-stu-id="675da-300">Receipt card</span></span>

<span data-ttu-id="675da-301">在团队中受支持。</span><span class="sxs-lookup"><span data-stu-id="675da-301">Supported in Teams.</span></span>

<span data-ttu-id="675da-302">使 bot 能够向用户提供收据的卡片。</span><span class="sxs-lookup"><span data-stu-id="675da-302">A card that enables a bot to provide a receipt to the user.</span></span> <span data-ttu-id="675da-303">它通常包含要包含在收据、税和总计信息以及其他文本中的项的列表。</span><span class="sxs-lookup"><span data-stu-id="675da-303">It typically contains the list of items to include on the receipt, tax and total information, and other text.</span></span>

### <a name="support-for-receipts-cards"></a><span data-ttu-id="675da-304">对收据卡的支持</span><span class="sxs-lookup"><span data-stu-id="675da-304">Support for Receipts cards</span></span>

| <span data-ttu-id="675da-305">团队中的 bot</span><span class="sxs-lookup"><span data-stu-id="675da-305">Bots in Teams</span></span> | <span data-ttu-id="675da-306">邮件扩展</span><span class="sxs-lookup"><span data-stu-id="675da-306">Messaging Extensions</span></span>  | <span data-ttu-id="675da-307">连接器</span><span class="sxs-lookup"><span data-stu-id="675da-307">Connectors</span></span> | <span data-ttu-id="675da-308">Bot 框架</span><span class="sxs-lookup"><span data-stu-id="675da-308">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="675da-309">✔</span><span class="sxs-lookup"><span data-stu-id="675da-309">✔</span></span> | <span data-ttu-id="675da-310">✔</span><span class="sxs-lookup"><span data-stu-id="675da-310">✔</span></span> | <span data-ttu-id="675da-311">✖</span><span class="sxs-lookup"><span data-stu-id="675da-311">✖</span></span> | <span data-ttu-id="675da-312">✔</span><span class="sxs-lookup"><span data-stu-id="675da-312">✔</span></span> |
|

### <a name="for-more-information-on-receipt-cards"></a><span data-ttu-id="675da-313">有关收据卡的详细信息</span><span class="sxs-lookup"><span data-stu-id="675da-313">For more information on Receipt cards</span></span>

<span data-ttu-id="675da-314">Bot 框架参考：</span><span class="sxs-lookup"><span data-stu-id="675da-314">Bot Framework reference:</span></span>

* [<span data-ttu-id="675da-315">"收据卡" 节点</span><span class="sxs-lookup"><span data-stu-id="675da-315">Receipt card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest)
* [<span data-ttu-id="675da-316">收据卡 C#</span><span class="sxs-lookup"><span data-stu-id="675da-316">Receipt card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0)

## <a name="signin-card"></a><span data-ttu-id="675da-317">登录卡片</span><span class="sxs-lookup"><span data-stu-id="675da-317">Signin card</span></span>

<span data-ttu-id="675da-318">使机器人能够请求用户登录的卡片。</span><span class="sxs-lookup"><span data-stu-id="675da-318">A card that enables a bot to request that a user sign in.</span></span> <span data-ttu-id="675da-319">在与 Bot 框架中相比，在不同表单中的团队中支持。</span><span class="sxs-lookup"><span data-stu-id="675da-319">Supported in Teams in a slightly different form than is found in the Bot Framework.</span></span> <span data-ttu-id="675da-320">团队中的登录卡片与 bot 框架中的登录卡片类似，但在团队登录卡仅支持两个操作时除外： `signin`和。 `openUrl`</span><span class="sxs-lookup"><span data-stu-id="675da-320">The signin card in Teams is similar to the signin card in the bot framework with the exception that the signin card in Teams only supports two actions: `signin` and `openUrl`.</span></span>

<span data-ttu-id="675da-321">*登录操作*可用于团队中的任何卡片，而不仅仅是登录卡。</span><span class="sxs-lookup"><span data-stu-id="675da-321">The *signin action* can be used from any card in Teams, not just the signin card.</span></span> <span data-ttu-id="675da-322">有关身份验证的详细信息，请参阅[Microsoft 团队身份验证流的](~/bots/how-to/authentication/auth-flow-bot.md)主题相关主题。</span><span class="sxs-lookup"><span data-stu-id="675da-322">See the topic [Microsoft Teams authentication flow for bots](~/bots/how-to/authentication/auth-flow-bot.md) for more details on authentication.</span></span>

### <a name="support-for-signin-cards"></a><span data-ttu-id="675da-323">对登录卡的支持</span><span class="sxs-lookup"><span data-stu-id="675da-323">Support for Signin cards</span></span>

| <span data-ttu-id="675da-324">团队中的 bot</span><span class="sxs-lookup"><span data-stu-id="675da-324">Bots in Teams</span></span> | <span data-ttu-id="675da-325">邮件扩展</span><span class="sxs-lookup"><span data-stu-id="675da-325">Messaging Extensions</span></span>  | <span data-ttu-id="675da-326">连接器</span><span class="sxs-lookup"><span data-stu-id="675da-326">Connectors</span></span> | <span data-ttu-id="675da-327">Bot 框架</span><span class="sxs-lookup"><span data-stu-id="675da-327">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="675da-328">✔</span><span class="sxs-lookup"><span data-stu-id="675da-328">✔</span></span> | <span data-ttu-id="675da-329">✖</span><span class="sxs-lookup"><span data-stu-id="675da-329">✖</span></span> | <span data-ttu-id="675da-330">✖</span><span class="sxs-lookup"><span data-stu-id="675da-330">✖</span></span> | <span data-ttu-id="675da-331">✔</span><span class="sxs-lookup"><span data-stu-id="675da-331">✔</span></span> |
|

### <a name="for-more-information-on-signin-cards"></a><span data-ttu-id="675da-332">有关登录卡的详细信息</span><span class="sxs-lookup"><span data-stu-id="675da-332">For more information on Signin cards</span></span>

<span data-ttu-id="675da-333">Bot 框架参考：</span><span class="sxs-lookup"><span data-stu-id="675da-333">Bot Framework reference:</span></span>

* [<span data-ttu-id="675da-334">登录卡片节点</span><span class="sxs-lookup"><span data-stu-id="675da-334">Signin card Node</span></span>](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest)
* [<span data-ttu-id="675da-335">登录卡 C#</span><span class="sxs-lookup"><span data-stu-id="675da-335">Signin card C#</span></span>](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0)

## <a name="thumbnail-card"></a><span data-ttu-id="675da-336">缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="675da-336">Thumbnail card</span></span>

<span data-ttu-id="675da-337">通常包含单个缩略图图像、一个或多个按钮以及文本的卡片。</span><span class="sxs-lookup"><span data-stu-id="675da-337">A card that typically contains a single thumbnail image, one or more buttons, and text.</span></span>

### <a name="support-for-thumbnail-cards"></a><span data-ttu-id="675da-338">支持缩略图卡片</span><span class="sxs-lookup"><span data-stu-id="675da-338">Support for Thumbnail cards</span></span>

| <span data-ttu-id="675da-339">团队中的 bot</span><span class="sxs-lookup"><span data-stu-id="675da-339">Bots in Teams</span></span> | <span data-ttu-id="675da-340">邮件扩展</span><span class="sxs-lookup"><span data-stu-id="675da-340">Messaging Extensions</span></span>  | <span data-ttu-id="675da-341">连接器</span><span class="sxs-lookup"><span data-stu-id="675da-341">Connectors</span></span> | <span data-ttu-id="675da-342">Bot 框架</span><span class="sxs-lookup"><span data-stu-id="675da-342">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="675da-343">✔</span><span class="sxs-lookup"><span data-stu-id="675da-343">✔</span></span> | <span data-ttu-id="675da-344">✔</span><span class="sxs-lookup"><span data-stu-id="675da-344">✔</span></span> | <span data-ttu-id="675da-345">✖</span><span class="sxs-lookup"><span data-stu-id="675da-345">✖</span></span> | <span data-ttu-id="675da-346">✔</span><span class="sxs-lookup"><span data-stu-id="675da-346">✔</span></span> |
|

![缩略图示例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a><span data-ttu-id="675da-348">缩略图卡的属性</span><span class="sxs-lookup"><span data-stu-id="675da-348">Properties of a Thumbnail card</span></span>

| <span data-ttu-id="675da-349">属性</span><span class="sxs-lookup"><span data-stu-id="675da-349">Property</span></span> | <span data-ttu-id="675da-350">类型</span><span class="sxs-lookup"><span data-stu-id="675da-350">Type</span></span>  | <span data-ttu-id="675da-351">说明</span><span class="sxs-lookup"><span data-stu-id="675da-351">Description</span></span> |
| --- | --- | --- |
| <span data-ttu-id="675da-352">title</span><span class="sxs-lookup"><span data-stu-id="675da-352">title</span></span> | <span data-ttu-id="675da-353">格式文本 </span><span class="sxs-lookup"><span data-stu-id="675da-353">Rich text</span></span> | <span data-ttu-id="675da-354">卡片的标题。</span><span class="sxs-lookup"><span data-stu-id="675da-354">Title of the card.</span></span> <span data-ttu-id="675da-355">最多2行;当前不支持的格式</span><span class="sxs-lookup"><span data-stu-id="675da-355">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="675da-356">字幕</span><span class="sxs-lookup"><span data-stu-id="675da-356">subtitle</span></span> | <span data-ttu-id="675da-357">格式文本 </span><span class="sxs-lookup"><span data-stu-id="675da-357">Rich text</span></span> | <span data-ttu-id="675da-358">卡片的副标题。</span><span class="sxs-lookup"><span data-stu-id="675da-358">Subtitle of the card.</span></span> <span data-ttu-id="675da-359">最多2行;当前不支持的格式</span><span class="sxs-lookup"><span data-stu-id="675da-359">Maximum 2 lines; formatting not currently supported</span></span> |
| <span data-ttu-id="675da-360">text</span><span class="sxs-lookup"><span data-stu-id="675da-360">text</span></span> | <span data-ttu-id="675da-361">格式文本 </span><span class="sxs-lookup"><span data-stu-id="675da-361">Rich text</span></span> | <span data-ttu-id="675da-362">文本显示在副标题的正下方;请参阅[卡片格式](~/task-modules-and-cards/cards/cards-format.md)设置选项</span><span class="sxs-lookup"><span data-stu-id="675da-362">Text appears just below the subtitle; see [Card formatting](~/task-modules-and-cards/cards/cards-format.md) for formatting options</span></span> |
| <span data-ttu-id="675da-363">图形</span><span class="sxs-lookup"><span data-stu-id="675da-363">images</span></span> | <span data-ttu-id="675da-364">图像数组</span><span class="sxs-lookup"><span data-stu-id="675da-364">Array of images</span></span> | <span data-ttu-id="675da-365">显示在卡片顶部的图像。</span><span class="sxs-lookup"><span data-stu-id="675da-365">Image displayed at top of card.</span></span> <span data-ttu-id="675da-366">纵横比1:1 （方形）</span><span class="sxs-lookup"><span data-stu-id="675da-366">Aspect ratio 1:1 (square)</span></span> |
| <span data-ttu-id="675da-367">按钮</span><span class="sxs-lookup"><span data-stu-id="675da-367">buttons</span></span> | <span data-ttu-id="675da-368">Action 对象的数组</span><span class="sxs-lookup"><span data-stu-id="675da-368">Array of action objects</span></span> | <span data-ttu-id="675da-369">适用于当前卡片的一组操作。</span><span class="sxs-lookup"><span data-stu-id="675da-369">Set of actions applicable to the current card.</span></span> <span data-ttu-id="675da-370">最大6</span><span class="sxs-lookup"><span data-stu-id="675da-370">Maximum 6</span></span> |
| <span data-ttu-id="675da-371">即可</span><span class="sxs-lookup"><span data-stu-id="675da-371">tap</span></span> | <span data-ttu-id="675da-372">Action 对象</span><span class="sxs-lookup"><span data-stu-id="675da-372">Action object</span></span> | <span data-ttu-id="675da-373">当用户点击卡片本身时，将激活此操作</span><span class="sxs-lookup"><span data-stu-id="675da-373">This action will be activated when the user taps on the card itself</span></span> |
|

### <a name="example-thumbnail-card"></a><span data-ttu-id="675da-374">缩略图示例卡片</span><span class="sxs-lookup"><span data-stu-id="675da-374">Example Thumbnail card</span></span>

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

### <a name="for-more-information"></a><span data-ttu-id="675da-375">更多详细信息</span><span class="sxs-lookup"><span data-stu-id="675da-375">For more information</span></span>

<span data-ttu-id="675da-376">Bot 框架参考：</span><span class="sxs-lookup"><span data-stu-id="675da-376">Bot Framework reference:</span></span>

* [<span data-ttu-id="675da-377">缩略图卡片节点</span><span class="sxs-lookup"><span data-stu-id="675da-377">Thumbnail card Node</span></span>](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest)
* [<span data-ttu-id="675da-378">缩略图卡片 C#</span><span class="sxs-lookup"><span data-stu-id="675da-378">Thumbnail card C#</span></span>](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0)

## <a name="card-collections"></a><span data-ttu-id="675da-379">卡片集合</span><span class="sxs-lookup"><span data-stu-id="675da-379">Card collections</span></span>

<span data-ttu-id="675da-380">团队中支持卡片集合。</span><span class="sxs-lookup"><span data-stu-id="675da-380">Card collections are supported in Teams.</span></span>

<span data-ttu-id="675da-381">卡集合由 Bot 框架（ `builder.AttachmentLayout.carousel`和`builder.AttachmentLayout.list`）提供。</span><span class="sxs-lookup"><span data-stu-id="675da-381">Card collections are provided by the Bot Framework: `builder.AttachmentLayout.carousel` and `builder.AttachmentLayout.list`.</span></span> <span data-ttu-id="675da-382">这些集合可以包含自适应、英雄或缩略图卡片。</span><span class="sxs-lookup"><span data-stu-id="675da-382">These collections can contain Adaptive, Hero, or Thumbnail cards.</span></span>

## <a name="carousel-collection"></a><span data-ttu-id="675da-383">轮播集合</span><span class="sxs-lookup"><span data-stu-id="675da-383">Carousel collection</span></span>

<span data-ttu-id="675da-384">[轮播布局](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0)显示了卡片的轮播，也可以选择使用关联的动作按钮。</span><span class="sxs-lookup"><span data-stu-id="675da-384">The [carousel layout](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0) shows a carousel of cards, optionally with associated action buttons.</span></span>

### <a name="support-for-carousel-collections"></a><span data-ttu-id="675da-385">对轮播集合的支持</span><span class="sxs-lookup"><span data-stu-id="675da-385">Support for Carousel collections</span></span>

| <span data-ttu-id="675da-386">团队中的 bot</span><span class="sxs-lookup"><span data-stu-id="675da-386">Bots in Teams</span></span> | <span data-ttu-id="675da-387">邮件扩展</span><span class="sxs-lookup"><span data-stu-id="675da-387">Messaging Extensions</span></span>  | <span data-ttu-id="675da-388">连接器</span><span class="sxs-lookup"><span data-stu-id="675da-388">Connectors</span></span> | <span data-ttu-id="675da-389">Bot 框架</span><span class="sxs-lookup"><span data-stu-id="675da-389">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="675da-390">✔</span><span class="sxs-lookup"><span data-stu-id="675da-390">✔</span></span> | <span data-ttu-id="675da-391">✖</span><span class="sxs-lookup"><span data-stu-id="675da-391">✖</span></span> | <span data-ttu-id="675da-392">✖</span><span class="sxs-lookup"><span data-stu-id="675da-392">✖</span></span> | <span data-ttu-id="675da-393">✔</span><span class="sxs-lookup"><span data-stu-id="675da-393">✔</span></span> |
|

> [!NOTE]
> <span data-ttu-id="675da-394">每封邮件的轮播最多可显示10张卡片。</span><span class="sxs-lookup"><span data-stu-id="675da-394">A carousel can display a maximum of 10 cards per message.</span></span>

### <a name="example-carousel-collection"></a><span data-ttu-id="675da-395">示例轮播集合</span><span class="sxs-lookup"><span data-stu-id="675da-395">Example Carousel collection</span></span>

![卡片轮播的示例](~/assets/images/cards/carousel.png)

<span data-ttu-id="675da-397">属性与对英雄或缩略图卡片的属性相同。</span><span class="sxs-lookup"><span data-stu-id="675da-397">Properties are the same as for the hero or thumbnail card.</span></span>

### <a name="syntax-for-carousel-collections"></a><span data-ttu-id="675da-398">轮播集合的语法</span><span class="sxs-lookup"><span data-stu-id="675da-398">Syntax for Carousel collections</span></span>

`builder.AttachmentLayout.carousel`

## <a name="list-collection"></a><span data-ttu-id="675da-399">列表集合</span><span class="sxs-lookup"><span data-stu-id="675da-399">List collection</span></span>

### <a name="support-for-list-collections"></a><span data-ttu-id="675da-400">对列表集合的支持</span><span class="sxs-lookup"><span data-stu-id="675da-400">Support for List collections</span></span>

<span data-ttu-id="675da-401">列表布局显示垂直堆叠的卡片列表，可以选择使用关联的操作按钮。</span><span class="sxs-lookup"><span data-stu-id="675da-401">The list layout shows a vertically stacked list of cards, optionally with associated action buttons.</span></span>

| <span data-ttu-id="675da-402">团队中的 bot</span><span class="sxs-lookup"><span data-stu-id="675da-402">Bots in Teams</span></span> | <span data-ttu-id="675da-403">邮件扩展</span><span class="sxs-lookup"><span data-stu-id="675da-403">Messaging Extensions</span></span>  | <span data-ttu-id="675da-404">连接器</span><span class="sxs-lookup"><span data-stu-id="675da-404">Connectors</span></span> | <span data-ttu-id="675da-405">Bot 框架</span><span class="sxs-lookup"><span data-stu-id="675da-405">Bot Framework</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="675da-406">✔</span><span class="sxs-lookup"><span data-stu-id="675da-406">✔</span></span> | <span data-ttu-id="675da-407">✔</span><span class="sxs-lookup"><span data-stu-id="675da-407">✔</span></span> | <span data-ttu-id="675da-408">✖</span><span class="sxs-lookup"><span data-stu-id="675da-408">✖</span></span> | <span data-ttu-id="675da-409">✔</span><span class="sxs-lookup"><span data-stu-id="675da-409">✔</span></span> |
|

### <a name="example-list-collection"></a><span data-ttu-id="675da-410">示例列表集合</span><span class="sxs-lookup"><span data-stu-id="675da-410">Example List collection</span></span>

![卡片列表的示例](~/assets/images/cards/list.png)

<span data-ttu-id="675da-412">属性与对英雄或缩略图卡片的属性相同。</span><span class="sxs-lookup"><span data-stu-id="675da-412">Properties are the same as for the hero or thumbnail card.</span></span>

<span data-ttu-id="675da-413">列表最多可显示10个卡片（每封邮件）。</span><span class="sxs-lookup"><span data-stu-id="675da-413">A list can display a maximum of 10 cards per message.</span></span>

> [!NOTE]
> <span data-ttu-id="675da-414">清单卡的某些组合在 iOS 和 Android 上尚不受支持。</span><span class="sxs-lookup"><span data-stu-id="675da-414">Some combinations of list cards are not yet supported on iOS and Android.</span></span>

### <a name="syntax-for-list-collections"></a><span data-ttu-id="675da-415">列表集合的语法</span><span class="sxs-lookup"><span data-stu-id="675da-415">Syntax for List collections</span></span>

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a><span data-ttu-id="675da-416">团队不支持的卡片</span><span class="sxs-lookup"><span data-stu-id="675da-416">Cards not supported in Teams</span></span>

<span data-ttu-id="675da-417">以下卡片由 Bot 框架实现，但团队不支持。</span><span class="sxs-lookup"><span data-stu-id="675da-417">The following cards are implemented by the Bot Framework, but are NOT supported by Teams.</span></span>

* <span data-ttu-id="675da-418">动画卡片</span><span class="sxs-lookup"><span data-stu-id="675da-418">Animation cards</span></span>
* <span data-ttu-id="675da-419">音频卡</span><span class="sxs-lookup"><span data-stu-id="675da-419">Audio cards</span></span>
* <span data-ttu-id="675da-420">视频卡</span><span class="sxs-lookup"><span data-stu-id="675da-420">Video cards</span></span>
