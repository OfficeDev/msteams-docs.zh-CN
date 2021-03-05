---
title: 卡片中的文本格式
description: 介绍 Microsoft Teams 中的卡片文本格式
keywords: teams 自动程序卡片格式
ms.date: 03/29/2018
ms.openlocfilehash: 1221693ab9ae002ee982ef34a05ead1feb8b1f27
ms.sourcegitcommit: 47cf0d05e15e5c23616b18ae4e815fd871bbf827
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50455392"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="08871-104">在 Teams 中设置卡片格式</span><span class="sxs-lookup"><span data-stu-id="08871-104">Format cards in Teams</span></span>

<span data-ttu-id="08871-105">可以使用 Markdown 或 HTML 将格式文本格式添加到卡片，具体取决于卡片类型。</span><span class="sxs-lookup"><span data-stu-id="08871-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="08871-106">卡片仅支持文本属性中的格式设置，不支持标题或副标题属性中的格式设置。</span><span class="sxs-lookup"><span data-stu-id="08871-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="08871-107">可以使用 XML 子集指定格式 (HTML) ，也可以根据卡片类型指定 Markdown。</span><span class="sxs-lookup"><span data-stu-id="08871-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="08871-108">对于当前和将来的开发，建议使用 Markdown 格式的自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="08871-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="08871-109">格式设置支持因卡类型不同而不同，并且桌面版和移动 Teams 客户端以及桌面浏览器中的 Teams 的卡片呈现可能略有不同。</span><span class="sxs-lookup"><span data-stu-id="08871-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="08871-110">你可以将内联图像与任意 Teams 卡一起包含。</span><span class="sxs-lookup"><span data-stu-id="08871-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="08871-111">格式设置为 ，或文件的图像不能超过  `.png` `.jpg` `.gif` 1024 × 1024 像素或 1 MB。</span><span class="sxs-lookup"><span data-stu-id="08871-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="08871-112">动态 GIF 不受正式支持。</span><span class="sxs-lookup"><span data-stu-id="08871-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="08871-113">*请参阅*[卡片参考](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="08871-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="08871-114">使用 Markdown 格式化卡片</span><span class="sxs-lookup"><span data-stu-id="08871-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="08871-115">Teams 中支持 Markdown 的卡类型有两种：</span><span class="sxs-lookup"><span data-stu-id="08871-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="08871-116">**自适应卡片**：Markdown 在自适应卡片 `Textblock` 字段中受支持，以及 `Fact.Title` `Fact.Value` .</span><span class="sxs-lookup"><span data-stu-id="08871-116">**Adaptive cards**: Markdown is supported in Adaptive card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="08871-117">自适应卡片不支持 HTML。</span><span class="sxs-lookup"><span data-stu-id="08871-117">HTML is not supported in Adaptive cards.</span></span>
> * <span data-ttu-id="08871-118">**O365 连接器卡**：文本字段中的 Office 365 连接器卡支持 Markdown 和有限的 HTML。</span><span class="sxs-lookup"><span data-stu-id="08871-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="08871-119">**Markdown 格式：自适应卡片**</span><span class="sxs-lookup"><span data-stu-id="08871-119">**Markdown formatting: Adaptive cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="08871-120">支持的样式包括 `Textblock` `Fact.Title` `Fact.Value` ：</span><span class="sxs-lookup"><span data-stu-id="08871-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="08871-121">样式</span><span class="sxs-lookup"><span data-stu-id="08871-121">Style</span></span> | <span data-ttu-id="08871-122">示例</span><span class="sxs-lookup"><span data-stu-id="08871-122">Example</span></span> | <span data-ttu-id="08871-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="08871-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08871-124">bold</span><span class="sxs-lookup"><span data-stu-id="08871-124">bold</span></span> | <span data-ttu-id="08871-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="08871-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="08871-126">italic</span><span class="sxs-lookup"><span data-stu-id="08871-126">italic</span></span> | <span data-ttu-id="08871-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="08871-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="08871-128">无序列表</span><span class="sxs-lookup"><span data-stu-id="08871-128">unordered list</span></span> | <ul><li><span data-ttu-id="08871-129">text</span><span class="sxs-lookup"><span data-stu-id="08871-129">text</span></span></li><li><span data-ttu-id="08871-130">text</span><span class="sxs-lookup"><span data-stu-id="08871-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="08871-131">排序列表</span><span class="sxs-lookup"><span data-stu-id="08871-131">ordered list</span></span> | <ol><li><span data-ttu-id="08871-132">text</span><span class="sxs-lookup"><span data-stu-id="08871-132">text</span></span></li><li><span data-ttu-id="08871-133">text</span><span class="sxs-lookup"><span data-stu-id="08871-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="08871-134">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="08871-134">Hyperlinks</span></span> |[<span data-ttu-id="08871-135">必应</span><span class="sxs-lookup"><span data-stu-id="08871-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="08871-136">不支持以下 Markdown 标记：</span><span class="sxs-lookup"><span data-stu-id="08871-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="08871-137">标头</span><span class="sxs-lookup"><span data-stu-id="08871-137">Headers</span></span>
* <span data-ttu-id="08871-138">表格</span><span class="sxs-lookup"><span data-stu-id="08871-138">Tables</span></span>
* <span data-ttu-id="08871-139">图像</span><span class="sxs-lookup"><span data-stu-id="08871-139">Images</span></span>
* <span data-ttu-id="08871-140">预先格式化的文本</span><span class="sxs-lookup"><span data-stu-id="08871-140">Preformatted text</span></span>
* <span data-ttu-id="08871-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="08871-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="08871-142">自适应卡片不支持 HTML 格式。</span><span class="sxs-lookup"><span data-stu-id="08871-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="08871-143">自适应卡片的行</span><span class="sxs-lookup"><span data-stu-id="08871-143">Newlines for Adaptive cards</span></span>

<span data-ttu-id="08871-144">在列表中，可以使用 `\r` 新行的转 `\n` 义序列或转义序列。</span><span class="sxs-lookup"><span data-stu-id="08871-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="08871-145">在 `\n\n` 列表中使用将导致列表中的下一个元素缩进。</span><span class="sxs-lookup"><span data-stu-id="08871-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="08871-146">如果需要在 textblock 中的其他地方使用新行，请使用 `\n\n` 。</span><span class="sxs-lookup"><span data-stu-id="08871-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="08871-147">自适应卡片的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="08871-147">Mobile and desktop differences for Adaptive cards</span></span>

<span data-ttu-id="08871-148">桌面版和移动版 Teams 之间的格式略有不同。</span><span class="sxs-lookup"><span data-stu-id="08871-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="08871-149">在桌面上，自适应卡片 Markdown 格式在 Web 浏览器和 Teams 客户端应用程序中如下所示：</span><span class="sxs-lookup"><span data-stu-id="08871-149">On the desktop, Adaptive card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![桌面客户端中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="08871-151">在 iOS 上，自适应卡片 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="08871-151">On iOS, Adaptive card Markdown formatting appears like this:</span></span>

![iOS 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="08871-153">在 Android 上，自适应卡片 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="08871-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Android 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="08871-155">自适应卡片上更多信息</span><span class="sxs-lookup"><span data-stu-id="08871-155">More information on Adaptive cards</span></span>

<span data-ttu-id="08871-156">[自适应卡片中的文本功能](/adaptive-cards/create/textfeatures) 本主题中提到的日期和本地化功能在 Teams 中不受支持。</span><span class="sxs-lookup"><span data-stu-id="08871-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="08871-157">自适应卡片的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="08871-157">Formatting sample for Adaptive cards</span></span>

``` json
{
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
    "type": "AdaptiveCard",
    "version": "1.0",
    "body": [
        {
            "type": "TextBlock",
            "text": "This is some **bold** text"
        },
        {
            "type": "TextBlock",
            "text": "This is some _italic_ text"
        },
        {
            "type": "TextBlock",
            "text": "- Bullet \r- List \r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "1. Numbered\r2. List\r",
            "wrap": true
        },
        {
            "type": "TextBlock",
            "text": "Check out [Adaptive Cards](https://adaptivecards.io)"
        }
    ]
}
```

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="08871-158">在自适应卡片 v1.2 中提及支持</span><span class="sxs-lookup"><span data-stu-id="08871-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="08871-159">Web、桌面和移动客户端支持基于卡片的提及。</span><span class="sxs-lookup"><span data-stu-id="08871-159">Card based mentions are supported in Web, Desktop and mobile clients.</span></span> <span data-ttu-id="08871-160">你可以为机器人和消息传递扩展响应在自适应卡片正文中添加 @ 提及。</span><span class="sxs-lookup"><span data-stu-id="08871-160">You can add @ mentions within an Adaptive card body for bots and messaging extension responses.</span></span>  <span data-ttu-id="08871-161">若要在卡片中添加 @ 提及，请遵循与频道和群聊对话中基于消息的提及相同的通知逻辑 [和呈现](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions )。</span><span class="sxs-lookup"><span data-stu-id="08871-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions ).</span></span>

<span data-ttu-id="08871-162">自动程序和消息传递扩展可以在 [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 和 [FactSet](https://adaptivecards.io/explorer/FactSet.html) 元素中的卡片内容中包括提及。</span><span class="sxs-lookup"><span data-stu-id="08871-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="08871-163">[Teams 平台上](https://adaptivecards.io/explorer/Media.html) 自适应卡片 v1.2 中当前不支持媒体元素。</span><span class="sxs-lookup"><span data-stu-id="08871-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="08871-164">频道&团队提及在机器人消息中不受支持。</span><span class="sxs-lookup"><span data-stu-id="08871-164">Channel & Team mentions are not supported in bot messages.</span></span>

#### <a name="constructing-mentions"></a><span data-ttu-id="08871-165">构造提及</span><span class="sxs-lookup"><span data-stu-id="08871-165">Constructing mentions</span></span>

<span data-ttu-id="08871-166">若要在自适应卡片中包括提及，应用需要包括以下元素</span><span class="sxs-lookup"><span data-stu-id="08871-166">To include a mention in an Adaptive card your app needs to include the following elements</span></span>

* <span data-ttu-id="08871-167">`<at>username</at>` 在支持的自适应卡片元素中</span><span class="sxs-lookup"><span data-stu-id="08871-167">`<at>username</at>` in the supported Adaptive card elements</span></span>
* <span data-ttu-id="08871-168">`mention`卡片内容中属性内的对象，其中包括被提及 `msteams` 用户的 Teams 用户 ID</span><span class="sxs-lookup"><span data-stu-id="08871-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="08871-169">带提及的示例自适应卡片</span><span class="sxs-lookup"><span data-stu-id="08871-169">Sample Adaptive card with a mention</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.card.adaptive",
  "content": {
    "type": "AdaptiveCard",
    "body": [
      {
        "type": "TextBlock",
        "text": "Hi <at>John Doe</at>"
      }
    ],
    "$schema": "https://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.0",
    "msteams": {
      "entities": [
        {
          "type": "mention",
          "text": "<at>John Doe</at>",
          "mentioned": {
            "id": "29:123124124124",
            "name": "John Doe"
          }
        }
      ]
    }
  }
}
```


### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="08871-170">自适应卡片中的信息屏蔽</span><span class="sxs-lookup"><span data-stu-id="08871-170">Information masking in Adaptive cards</span></span>
<span data-ttu-id="08871-171">使用信息屏蔽属性可以屏蔽特定信息，例如密码或来自用户的敏感信息。</span><span class="sxs-lookup"><span data-stu-id="08871-171">Use the information masking property to mask specific information, such as password or sensitive information from users.</span></span>

> [!NOTE]
> <span data-ttu-id="08871-172">信息屏蔽属性当前仅在开发人员预览版中可用。</span><span class="sxs-lookup"><span data-stu-id="08871-172">The information masking property is currently available in the developer preview only.</span></span>

#### <a name="mask-information"></a><span data-ttu-id="08871-173">掩码信息</span><span class="sxs-lookup"><span data-stu-id="08871-173">Mask information</span></span>
<span data-ttu-id="08871-174">若要在自适应卡片中屏蔽信息，请添加要键入的属性 `isMasked`  `Input.Text` ，将其值设置为 *true。*</span><span class="sxs-lookup"><span data-stu-id="08871-174">To mask information in Adaptive cards, add the `isMasked` property to **type** `Input.Text`, and set its value to *true*.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="08871-175">带屏蔽属性的示例自适应卡片</span><span class="sxs-lookup"><span data-stu-id="08871-175">Sample Adaptive card with masking property</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

<span data-ttu-id="08871-176">下图是自适应卡片中屏蔽信息的一个示例：</span><span class="sxs-lookup"><span data-stu-id="08871-176">The following image is an example of masking information in Adaptive cards:</span></span>

![屏蔽信息图像](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="08871-178">全宽自适应卡片</span><span class="sxs-lookup"><span data-stu-id="08871-178">Full width Adaptive card</span></span>
<span data-ttu-id="08871-179">可以使用该属性来扩展自适应卡片的宽度， `msteams` 并充分利用额外的画布空间。</span><span class="sxs-lookup"><span data-stu-id="08871-179">You can use the `msteams` property to expand the width of an Adaptive card and make use of additional canvas space.</span></span> <span data-ttu-id="08871-180">有关如何使用属性的信息，请参阅以下示例：</span><span class="sxs-lookup"><span data-stu-id="08871-180">For information on how to use the property, see the following example:</span></span>

#### <a name="constructing-full-width-cards"></a><span data-ttu-id="08871-181">构造全宽卡片</span><span class="sxs-lookup"><span data-stu-id="08871-181">Constructing full width cards</span></span>
<span data-ttu-id="08871-182">若要使全宽自适应卡片，卡片内容 `width` `msteams` 中的属性中的对象必须设置为 `Full` 。</span><span class="sxs-lookup"><span data-stu-id="08871-182">To make a full width Adaptive card the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>
<span data-ttu-id="08871-183">此外，你的应用必须包含以下元素：</span><span class="sxs-lookup"><span data-stu-id="08871-183">In addition, your app must include the following elements:</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="08871-184">全宽自适应卡片示例</span><span class="sxs-lookup"><span data-stu-id="08871-184">Sample adaptive card with full width</span></span>

``` json
{
    "type": "AdaptiveCard",
    "body": [{
        "type": "Container",
        "items": [{
            "type": "TextBlock",
            "text": "Digest card",
            "size": "Large",
            "weight": "Bolder"
        }]
    }],
    
    "msteams": {
        "width": "Full"
    },
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

<span data-ttu-id="08871-185">完整宽度自适应卡片如下所示： ![ 全宽自适应卡片视图](../../assets/images/cards/full-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="08871-185">A full width Adaptive Card appears as follows: ![Full width Adaptive Card view](../../assets/images/cards/full-width-adaptive-card.png)</span></span>

<span data-ttu-id="08871-186">如果尚未将该属性设置为 `width` *Full，* 则自适应卡片的默认视图如下所示： ![ 小宽度自适应卡片视图](../../assets/images/cards/small-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="08871-186">If you have not set the `width` property to *Full*, then the default view of the Adaptive Card is as follows: ![Small width Adaptive Card view](../../assets/images/cards/small-width-adaptive-card.png)</span></span>



# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="08871-187">**Markdown 格式：O365 连接器卡**</span><span class="sxs-lookup"><span data-stu-id="08871-187">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="08871-188">连接器卡支持有限的 Markdown 和 HTML 格式。</span><span class="sxs-lookup"><span data-stu-id="08871-188">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="08871-189">最后一节介绍了 HTML 支持。</span><span class="sxs-lookup"><span data-stu-id="08871-189">HTML support is described in the last section.</span></span>

| <span data-ttu-id="08871-190">样式</span><span class="sxs-lookup"><span data-stu-id="08871-190">Style</span></span> | <span data-ttu-id="08871-191">示例</span><span class="sxs-lookup"><span data-stu-id="08871-191">Example</span></span> | <span data-ttu-id="08871-192">Markdown</span><span class="sxs-lookup"><span data-stu-id="08871-192">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08871-193">bold</span><span class="sxs-lookup"><span data-stu-id="08871-193">bold</span></span> | <span data-ttu-id="08871-194">**text**</span><span class="sxs-lookup"><span data-stu-id="08871-194">**text**</span></span> | `**text**` |
| <span data-ttu-id="08871-195">italic</span><span class="sxs-lookup"><span data-stu-id="08871-195">italic</span></span> | <span data-ttu-id="08871-196">*text*</span><span class="sxs-lookup"><span data-stu-id="08871-196">*text*</span></span> | `*text*` |
| <span data-ttu-id="08871-197">标头 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="08871-197">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="08871-198">**Text**</span><span class="sxs-lookup"><span data-stu-id="08871-198">**Text**</span></span> | `### Text`|
| <span data-ttu-id="08871-199">strikethrough</span><span class="sxs-lookup"><span data-stu-id="08871-199">strikethrough</span></span> | <span data-ttu-id="08871-200">~~text~~</span><span class="sxs-lookup"><span data-stu-id="08871-200">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="08871-201">无序列表</span><span class="sxs-lookup"><span data-stu-id="08871-201">unordered list</span></span> | <ul><li><span data-ttu-id="08871-202">text</span><span class="sxs-lookup"><span data-stu-id="08871-202">text</span></span></li><li><span data-ttu-id="08871-203">text</span><span class="sxs-lookup"><span data-stu-id="08871-203">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="08871-204">排序列表</span><span class="sxs-lookup"><span data-stu-id="08871-204">ordered list</span></span> | <ol><li><span data-ttu-id="08871-205">text</span><span class="sxs-lookup"><span data-stu-id="08871-205">text</span></span></li><li><span data-ttu-id="08871-206">text</span><span class="sxs-lookup"><span data-stu-id="08871-206">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="08871-207">预先格式化的文本</span><span class="sxs-lookup"><span data-stu-id="08871-207">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="08871-208">blockquote</span><span class="sxs-lookup"><span data-stu-id="08871-208">blockquote</span></span> | <span data-ttu-id="08871-209">>blockquote 文本</span><span class="sxs-lookup"><span data-stu-id="08871-209">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="08871-210">超链接</span><span class="sxs-lookup"><span data-stu-id="08871-210">hyperlink</span></span> | [<span data-ttu-id="08871-211">必应</span><span class="sxs-lookup"><span data-stu-id="08871-211">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="08871-212">图像链接</span><span class="sxs-lookup"><span data-stu-id="08871-212">image link</span></span> |![在一块石子上闪避](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="08871-214">在连接器卡中，为 或 呈现新行，但不 `\n\n` 呈现 `\n` `\r` 。</span><span class="sxs-lookup"><span data-stu-id="08871-214">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="08871-215">使用 Markdown 的连接器卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="08871-215">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="08871-216">在桌面上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="08871-216">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![桌面客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="08871-218">在 iOS 上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="08871-218">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![iOS 客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="08871-220">问题：</span><span class="sxs-lookup"><span data-stu-id="08871-220">Issues:</span></span>

* <span data-ttu-id="08871-221">Teams 的 iOS 客户端不会在连接器卡中呈现 Markdown 或 HTML 内嵌图像。</span><span class="sxs-lookup"><span data-stu-id="08871-221">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="08871-222">Blockquote 呈现为缩进，但不呈现灰色背景。</span><span class="sxs-lookup"><span data-stu-id="08871-222">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="08871-223">在 Android 上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="08871-223">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Android 客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="08871-225">Markdown 连接器卡的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="08871-225">Formatting example for Markdown Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card Markdown formatting",
    "sections": [
        {
            "text": "This is some **bold** text"
        },
        {
            "text": "This is some _italic_ text"
        },
        {
            "text": "# Header 1\r## Header 2\r### Header 3"
        },
        {
            "text": "- Bullet \r- List \r"
        },
        {
            "text": "1. Numbered\r1. List \r"
        },
        {
            "text": "Link: [Bing](https://www.bing.com)"
        },
        {
            "text": "embedded image link: ![Duck on a rock](https://aka.ms/Fo983c)"
        },
        {
            "text": "`preformatted text`"
        },
        {
            "text": "Newlines (backslash n, backslash n):\n\nline a\n\nline b\n\nline c"
        },
        {
            "text": ">This is a blockquote"
        }
     ]
  }
}

```

---

## <a name="formatting-cards-with-html"></a><span data-ttu-id="08871-226">使用 HTML 设置卡片格式</span><span class="sxs-lookup"><span data-stu-id="08871-226">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="08871-227">**HTML 格式：O365 连接器卡**</span><span class="sxs-lookup"><span data-stu-id="08871-227">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="08871-228">连接器卡支持有限的 Markdown 和 HTML 格式。</span><span class="sxs-lookup"><span data-stu-id="08871-228">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="08871-229">下一节将介绍 Markdown。</span><span class="sxs-lookup"><span data-stu-id="08871-229">Markdown is described in the next section.</span></span>

| <span data-ttu-id="08871-230">样式</span><span class="sxs-lookup"><span data-stu-id="08871-230">Style</span></span> | <span data-ttu-id="08871-231">示例</span><span class="sxs-lookup"><span data-stu-id="08871-231">Example</span></span> | <span data-ttu-id="08871-232">HTML</span><span class="sxs-lookup"><span data-stu-id="08871-232">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08871-233">bold</span><span class="sxs-lookup"><span data-stu-id="08871-233">bold</span></span> | <span data-ttu-id="08871-234">**text**</span><span class="sxs-lookup"><span data-stu-id="08871-234">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="08871-235">italic</span><span class="sxs-lookup"><span data-stu-id="08871-235">italic</span></span> | <span data-ttu-id="08871-236">*text*</span><span class="sxs-lookup"><span data-stu-id="08871-236">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="08871-237">标头 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="08871-237">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="08871-238">**Text**</span><span class="sxs-lookup"><span data-stu-id="08871-238">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="08871-239">strikethrough</span><span class="sxs-lookup"><span data-stu-id="08871-239">strikethrough</span></span> | <span data-ttu-id="08871-240">~~text~~</span><span class="sxs-lookup"><span data-stu-id="08871-240">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="08871-241">无序列表</span><span class="sxs-lookup"><span data-stu-id="08871-241">unordered list</span></span> | <ul><li><span data-ttu-id="08871-242">text</span><span class="sxs-lookup"><span data-stu-id="08871-242">text</span></span></li><li><span data-ttu-id="08871-243">text</span><span class="sxs-lookup"><span data-stu-id="08871-243">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="08871-244">排序列表</span><span class="sxs-lookup"><span data-stu-id="08871-244">ordered list</span></span> | <ol><li><span data-ttu-id="08871-245">text</span><span class="sxs-lookup"><span data-stu-id="08871-245">text</span></span></li><li><span data-ttu-id="08871-246">text</span><span class="sxs-lookup"><span data-stu-id="08871-246">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="08871-247">预先格式化的文本</span><span class="sxs-lookup"><span data-stu-id="08871-247">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="08871-248">blockquote</span><span class="sxs-lookup"><span data-stu-id="08871-248">blockquote</span></span> | <blockquote><span data-ttu-id="08871-249">text</span><span class="sxs-lookup"><span data-stu-id="08871-249">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="08871-250">超链接</span><span class="sxs-lookup"><span data-stu-id="08871-250">hyperlink</span></span> | [<span data-ttu-id="08871-251">必应</span><span class="sxs-lookup"><span data-stu-id="08871-251">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="08871-252">图像链接</span><span class="sxs-lookup"><span data-stu-id="08871-252">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="08871-253">在连接器卡中，使用标记以 HTML 格式呈现 `<p>` 新行。</span><span class="sxs-lookup"><span data-stu-id="08871-253">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="08871-254">使用 HTML 的连接器卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="08871-254">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="08871-255">在桌面上，连接器卡的 HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="08871-255">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![桌面客户端中连接器卡的 HTML 格式](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="08871-257">在 iOS 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="08871-257">On iOS, HTML formatting looks like this:</span></span>

![iOS 客户端中连接器卡的 HTML 格式](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="08871-259">问题：</span><span class="sxs-lookup"><span data-stu-id="08871-259">Issues:</span></span>

* <span data-ttu-id="08871-260">内嵌图像不会在 iOS 上使用 Markdown 或 HTML 在连接器卡上呈现。</span><span class="sxs-lookup"><span data-stu-id="08871-260">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="08871-261">呈现格式文本，但没有灰色背景。</span><span class="sxs-lookup"><span data-stu-id="08871-261">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="08871-262">在 Android 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="08871-262">On Android, HTML formatting looks like this:</span></span>

![Android 客户端中连接器卡的 HTML 格式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="08871-264">HTML 连接器卡的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="08871-264">Formatting sample for HTML Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "https://schema.org/extensions",
    "summary": "Summary",
    "title": "Connector Card HTML formatting",
    "sections": [
        {
            "text": "This is some <strong>bold</strong> text"
        },
        {
            "text": "This is some <em>italic</em> text"
        },
        {
            "text": "This is some <strike>strikethrough</strike> text"
        },
        {
            "text": "<h1>Header 1</h1>\r<h2>Header 2</h2>\r <h3>Header 3</h3>"
        },
        {
            "text": "bullet list <ul><li>text</li><li>text</li></ul>"
        },
        {
            "text": "ordered list <ol><li>text</li><li>text</li></ol>"
        },
        {
            "text": "hyperlink <a href=\"https://www.bing.com/\">Bing</a>"
        },
        {
            "text": "embedded image <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
        },
        {
            "text": "preformatted text <pre>text</pre>"
        },
        {
            "text": "Paragraphs <p>Line a</p><p>Line b</p>"
        },
        {
            "text": "<blockquote>Blockquote text</blockquote>"
        }
     ]
  }
}

```

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="08871-265">**HTML 格式：hero 和 thumbnail cards**</span><span class="sxs-lookup"><span data-stu-id="08871-265">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="08871-266">HTML 标记受简单卡片（如大图和缩略图卡）的支持。</span><span class="sxs-lookup"><span data-stu-id="08871-266">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="08871-267">不支持 Markdown。</span><span class="sxs-lookup"><span data-stu-id="08871-267">Markdown is not supported.</span></span>

| <span data-ttu-id="08871-268">样式</span><span class="sxs-lookup"><span data-stu-id="08871-268">Style</span></span> | <span data-ttu-id="08871-269">示例</span><span class="sxs-lookup"><span data-stu-id="08871-269">Example</span></span> | <span data-ttu-id="08871-270">HTML</span><span class="sxs-lookup"><span data-stu-id="08871-270">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="08871-271">bold</span><span class="sxs-lookup"><span data-stu-id="08871-271">bold</span></span> | <span data-ttu-id="08871-272">**text**</span><span class="sxs-lookup"><span data-stu-id="08871-272">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="08871-273">italic</span><span class="sxs-lookup"><span data-stu-id="08871-273">italic</span></span> | <span data-ttu-id="08871-274">*text*</span><span class="sxs-lookup"><span data-stu-id="08871-274">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="08871-275">标头 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="08871-275">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="08871-276">**Text**</span><span class="sxs-lookup"><span data-stu-id="08871-276">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="08871-277">strikethrough</span><span class="sxs-lookup"><span data-stu-id="08871-277">strikethrough</span></span> | <span data-ttu-id="08871-278">~~text~~</span><span class="sxs-lookup"><span data-stu-id="08871-278">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="08871-279">无序列表</span><span class="sxs-lookup"><span data-stu-id="08871-279">unordered list</span></span> | <ul><li><span data-ttu-id="08871-280">text</span><span class="sxs-lookup"><span data-stu-id="08871-280">text</span></span></li><li><span data-ttu-id="08871-281">text</span><span class="sxs-lookup"><span data-stu-id="08871-281">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="08871-282">排序列表</span><span class="sxs-lookup"><span data-stu-id="08871-282">ordered list</span></span> | <ol><li><span data-ttu-id="08871-283">text</span><span class="sxs-lookup"><span data-stu-id="08871-283">text</span></span></li><li><span data-ttu-id="08871-284">text</span><span class="sxs-lookup"><span data-stu-id="08871-284">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="08871-285">预先格式化的文本</span><span class="sxs-lookup"><span data-stu-id="08871-285">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="08871-286">blockquote</span><span class="sxs-lookup"><span data-stu-id="08871-286">blockquote</span></span> | <blockquote><span data-ttu-id="08871-287">text</span><span class="sxs-lookup"><span data-stu-id="08871-287">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="08871-288">超链接</span><span class="sxs-lookup"><span data-stu-id="08871-288">hyperlink</span></span> | [<span data-ttu-id="08871-289">必应</span><span class="sxs-lookup"><span data-stu-id="08871-289">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="08871-290">图像链接</span><span class="sxs-lookup"><span data-stu-id="08871-290">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="08871-291">简单卡片的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="08871-291">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="08871-292">由于桌面平台和移动平台之间的分辨率差异，桌面版和移动版 Teams 之间的格式设置不同。</span><span class="sxs-lookup"><span data-stu-id="08871-292">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="08871-293">在桌面上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="08871-293">On the desktop, HTML formatting appears like this:</span></span>

![桌面客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="08871-295">在 iOS 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="08871-295">On iOS, HTML formatting appears like this:</span></span>

![iOS 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="08871-297">问题：</span><span class="sxs-lookup"><span data-stu-id="08871-297">Issues:</span></span>

* <span data-ttu-id="08871-298">字符格式（如粗体和 italic）不会在 iOS 上呈现。</span><span class="sxs-lookup"><span data-stu-id="08871-298">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="08871-299">在 Android 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="08871-299">On Android, HTML formatting appears like this:</span></span>

![Android 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="08871-301">在 Android 上正确显示粗体和 italic 等字符格式。</span><span class="sxs-lookup"><span data-stu-id="08871-301">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="08871-302">简单卡片中 HTML 格式的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="08871-302">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="08871-303">这些屏幕截图是使用 Teams AppStudio 创建的，其中，Hero 卡片的文本属性已设置为以下字符串。</span><span class="sxs-lookup"><span data-stu-id="08871-303">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="08871-304">可以通过修改此代码来测试自己的卡片格式。</span><span class="sxs-lookup"><span data-stu-id="08871-304">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
