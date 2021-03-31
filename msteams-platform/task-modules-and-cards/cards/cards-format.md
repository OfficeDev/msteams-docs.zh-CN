---
title: 卡片中的文本格式
description: 介绍 Microsoft Teams 中的卡片文本格式
keywords: teams 自动程序卡格式
ms.date: 03/29/2018
ms.openlocfilehash: 240481f6deaa9246692ca297712bd311fbd9405d
ms.sourcegitcommit: 2bf651dfbaf5dbab6d466788f668e7a6c5d69c36
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/30/2021
ms.locfileid: "51421615"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="8bad4-104">在 Teams 中设置卡片格式</span><span class="sxs-lookup"><span data-stu-id="8bad4-104">Format cards in Teams</span></span>

<span data-ttu-id="8bad4-105">可以使用 Markdown 或 HTML 将格式文本格式添加到卡片，具体取决于卡片类型。</span><span class="sxs-lookup"><span data-stu-id="8bad4-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="8bad4-106">卡片仅支持文本属性中的格式设置，不支持标题或副标题属性中的格式设置。</span><span class="sxs-lookup"><span data-stu-id="8bad4-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="8bad4-107">可以使用 XML 格式的子集或 HTML (格式) Markdown 来指定格式，具体取决于卡片类型。</span><span class="sxs-lookup"><span data-stu-id="8bad4-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="8bad4-108">对于当前和未来开发，建议使用 Markdown 格式的自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="8bad4-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="8bad4-109">不同卡类型之间的格式支持不同，并且桌面版和移动版 Teams 客户端以及桌面浏览器中的 Teams 的卡片呈现可能略有不同。</span><span class="sxs-lookup"><span data-stu-id="8bad4-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="8bad4-110">你可以将内联图像与任意 Teams 卡一起包含。</span><span class="sxs-lookup"><span data-stu-id="8bad4-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="8bad4-111">格式设置为 、 或 文件的图像不能超过  `.png` `.jpg` `.gif` 1024 像素× 1024 像素或 1 MB。</span><span class="sxs-lookup"><span data-stu-id="8bad4-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="8bad4-112">动态 GIF 不受正式支持。</span><span class="sxs-lookup"><span data-stu-id="8bad4-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="8bad4-113">*请参阅*[卡片参考](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="8bad4-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="8bad4-114">使用 Markdown 格式化卡片</span><span class="sxs-lookup"><span data-stu-id="8bad4-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="8bad4-115">Teams 中支持 Markdown 的卡片类型有两种：</span><span class="sxs-lookup"><span data-stu-id="8bad4-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="8bad4-116">**自适应卡片**： Markdown 在自适应卡片字段中以及 和 `Textblock` `Fact.Title` 中受支持 `Fact.Value` 。</span><span class="sxs-lookup"><span data-stu-id="8bad4-116">**Adaptive cards**: Markdown is supported in Adaptive card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="8bad4-117">自适应卡片不支持 HTML。</span><span class="sxs-lookup"><span data-stu-id="8bad4-117">HTML is not supported in Adaptive cards.</span></span>
> * <span data-ttu-id="8bad4-118">**O365 连接器卡**：文本字段中的 Office 365 连接器卡支持 Markdown 和有限的 HTML。</span><span class="sxs-lookup"><span data-stu-id="8bad4-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="8bad4-119">**Markdown 格式：自适应卡片**</span><span class="sxs-lookup"><span data-stu-id="8bad4-119">**Markdown formatting: Adaptive cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="8bad4-120">和 `Textblock` 支持的 `Fact.Title` `Fact.Value` 样式包括：</span><span class="sxs-lookup"><span data-stu-id="8bad4-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="8bad4-121">样式</span><span class="sxs-lookup"><span data-stu-id="8bad4-121">Style</span></span> | <span data-ttu-id="8bad4-122">示例</span><span class="sxs-lookup"><span data-stu-id="8bad4-122">Example</span></span> | <span data-ttu-id="8bad4-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="8bad4-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8bad4-124">bold</span><span class="sxs-lookup"><span data-stu-id="8bad4-124">bold</span></span> | <span data-ttu-id="8bad4-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="8bad4-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="8bad4-126">italic</span><span class="sxs-lookup"><span data-stu-id="8bad4-126">italic</span></span> | <span data-ttu-id="8bad4-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="8bad4-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="8bad4-128">无序列表</span><span class="sxs-lookup"><span data-stu-id="8bad4-128">unordered list</span></span> | <ul><li><span data-ttu-id="8bad4-129">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-129">text</span></span></li><li><span data-ttu-id="8bad4-130">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="8bad4-131">排序列表</span><span class="sxs-lookup"><span data-stu-id="8bad4-131">ordered list</span></span> | <ol><li><span data-ttu-id="8bad4-132">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-132">text</span></span></li><li><span data-ttu-id="8bad4-133">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="8bad4-134">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="8bad4-134">Hyperlinks</span></span> |[<span data-ttu-id="8bad4-135">必应</span><span class="sxs-lookup"><span data-stu-id="8bad4-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="8bad4-136">不支持以下 Markdown 标记：</span><span class="sxs-lookup"><span data-stu-id="8bad4-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="8bad4-137">标头</span><span class="sxs-lookup"><span data-stu-id="8bad4-137">Headers</span></span>
* <span data-ttu-id="8bad4-138">表格</span><span class="sxs-lookup"><span data-stu-id="8bad4-138">Tables</span></span>
* <span data-ttu-id="8bad4-139">图像</span><span class="sxs-lookup"><span data-stu-id="8bad4-139">Images</span></span>
* <span data-ttu-id="8bad4-140">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="8bad4-140">Preformatted text</span></span>
* <span data-ttu-id="8bad4-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="8bad4-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="8bad4-142">自适应卡片不支持 HTML 格式。</span><span class="sxs-lookup"><span data-stu-id="8bad4-142">Adaptive cards do not support HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="8bad4-143">自适应卡片的 Newlines</span><span class="sxs-lookup"><span data-stu-id="8bad4-143">Newlines for Adaptive cards</span></span>

<span data-ttu-id="8bad4-144">在列表中，可以将 `\r` 或 `\n` 转义序列用于新行。</span><span class="sxs-lookup"><span data-stu-id="8bad4-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="8bad4-145">在 `\n\n` 列表中使用 将导致列表中的下一个元素缩进。</span><span class="sxs-lookup"><span data-stu-id="8bad4-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="8bad4-146">如果你需要在 textblock 中的其他地方使用 newlines，请使用 `\n\n` 。</span><span class="sxs-lookup"><span data-stu-id="8bad4-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="8bad4-147">自适应卡片的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="8bad4-147">Mobile and desktop differences for Adaptive cards</span></span>

<span data-ttu-id="8bad4-148">桌面版和移动版 Teams 的格式略有不同。</span><span class="sxs-lookup"><span data-stu-id="8bad4-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="8bad4-149">在桌面上，自适应卡片 Markdown 格式在 Web 浏览器和 Teams 客户端应用程序中如下所示：</span><span class="sxs-lookup"><span data-stu-id="8bad4-149">On the desktop, Adaptive card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![桌面客户端中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="8bad4-151">在 iOS 上，自适应卡片 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="8bad4-151">On iOS, Adaptive card Markdown formatting appears like this:</span></span>

![iOS 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="8bad4-153">在 Android 上，自适应卡片 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="8bad4-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Android 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="8bad4-155">自适应卡片详细信息</span><span class="sxs-lookup"><span data-stu-id="8bad4-155">More information on Adaptive cards</span></span>

<span data-ttu-id="8bad4-156">[自适应卡片中的文本功能](/adaptive-cards/create/textfeatures) 本主题中提到的日期和本地化功能在 Teams 中不受支持。</span><span class="sxs-lookup"><span data-stu-id="8bad4-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="8bad4-157">自适应卡片的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="8bad4-157">Formatting sample for Adaptive cards</span></span>

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

### <a name="mention-support-within-adaptive-cards-v12"></a><span data-ttu-id="8bad4-158">自适应卡片 v1.2 中的提及支持</span><span class="sxs-lookup"><span data-stu-id="8bad4-158">Mention support within Adaptive cards v1.2</span></span>

<span data-ttu-id="8bad4-159">Web、桌面和移动客户端支持基于卡片的提及。</span><span class="sxs-lookup"><span data-stu-id="8bad4-159">Card based mentions are supported in Web, Desktop and mobile clients.</span></span> <span data-ttu-id="8bad4-160">你可以为机器人和消息传递扩展响应在自适应卡片正文中添加 @ 提及。</span><span class="sxs-lookup"><span data-stu-id="8bad4-160">You can add @ mentions within an Adaptive card body for bots and messaging extension responses.</span></span>  <span data-ttu-id="8bad4-161">若要在卡片中添加 @ 提及，请遵循与频道和群聊对话中基于消息的提及相同的通知 [逻辑和呈现](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions )。</span><span class="sxs-lookup"><span data-stu-id="8bad4-161">To add @ mentions in cards, follow the same notification logic and rendering as that of message based [mentions in channel and group chat conversations](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions ).</span></span>

<span data-ttu-id="8bad4-162">聊天机器人和消息传递扩展可以在 [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 和 [FactSet](https://adaptivecards.io/explorer/FactSet.html) 元素的卡片内容中包括提及。</span><span class="sxs-lookup"><span data-stu-id="8bad4-162">Bots and messaging extensions can include mentions within the card content in [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) and [FactSet](https://adaptivecards.io/explorer/FactSet.html) elements.</span></span>

> [!NOTE]
> * <span data-ttu-id="8bad4-163">[Teams 平台上](https://adaptivecards.io/explorer/Media.html) 的自适应卡片 v1.2 当前不支持媒体元素。</span><span class="sxs-lookup"><span data-stu-id="8bad4-163">[Media elements](https://adaptivecards.io/explorer/Media.html) are currently not supported in Adaptive cards v1.2 on the Teams platform.</span></span>
> * <span data-ttu-id="8bad4-164">频道&团队提及在机器人消息中不受支持。</span><span class="sxs-lookup"><span data-stu-id="8bad4-164">Channel & Team mentions are not supported in bot messages.</span></span>

#### <a name="constructing-mentions"></a><span data-ttu-id="8bad4-165">构造提及</span><span class="sxs-lookup"><span data-stu-id="8bad4-165">Constructing mentions</span></span>

<span data-ttu-id="8bad4-166">若要在自适应卡片中包括提及，应用需要包括以下元素</span><span class="sxs-lookup"><span data-stu-id="8bad4-166">To include a mention in an Adaptive card your app needs to include the following elements</span></span>

* <span data-ttu-id="8bad4-167">`<at>username</at>` 在支持的自适应卡片元素中</span><span class="sxs-lookup"><span data-stu-id="8bad4-167">`<at>username</at>` in the supported Adaptive card elements</span></span>
* <span data-ttu-id="8bad4-168">`mention`卡片内容中属性内的对象，其中包括被提及用户的 `msteams` Teams 用户 ID</span><span class="sxs-lookup"><span data-stu-id="8bad4-168">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

#### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="8bad4-169">带提及功能的示例自适应卡片</span><span class="sxs-lookup"><span data-stu-id="8bad4-169">Sample Adaptive card with a mention</span></span>

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


### <a name="information-masking-in-adaptive-cards"></a><span data-ttu-id="8bad4-170">自适应卡片中的信息屏蔽</span><span class="sxs-lookup"><span data-stu-id="8bad4-170">Information masking in Adaptive cards</span></span>
<span data-ttu-id="8bad4-171">使用信息屏蔽属性可以屏蔽特定信息，如自适应卡片输入元素内用户的密码或 [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) 敏感信息。</span><span class="sxs-lookup"><span data-stu-id="8bad4-171">Use the information masking property to mask specific information, such as password or sensitive information from users within the Adaptive card [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) input element.</span></span> 

> [!NOTE]
> <span data-ttu-id="8bad4-172">该功能仅支持客户端信息屏蔽，将屏蔽的输入文本作为纯文本发送到在机器人配置期间指定的 https [终结点地址](../../build-your-first-app/build-bot.md#4-configure-your-bot)。</span><span class="sxs-lookup"><span data-stu-id="8bad4-172">The feature only supports client side information masking, the masked input text is sent as clear text to the https endpoint address that was specified during [bot configuration](../../build-your-first-app/build-bot.md#4-configure-your-bot).</span></span> 

> [!NOTE]
> <span data-ttu-id="8bad4-173">信息屏蔽属性当前仅在开发人员预览版中可用。</span><span class="sxs-lookup"><span data-stu-id="8bad4-173">The information masking property is currently available in the developer preview only.</span></span>

<span data-ttu-id="8bad4-174">若要屏蔽自适应卡片中的信息，请添加 `isMasked` 属性以 **键入** `Input.Text` ，将其值设置为 *true*。</span><span class="sxs-lookup"><span data-stu-id="8bad4-174">To mask information in Adaptive cards, add the `isMasked` property to **type** `Input.Text`, and set its value to *true*.</span></span>

#### <a name="sample-adaptive-card-with-masking-property"></a><span data-ttu-id="8bad4-175">具有屏蔽属性的示例自适应卡片</span><span class="sxs-lookup"><span data-stu-id="8bad4-175">Sample Adaptive card with masking property</span></span>

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

<span data-ttu-id="8bad4-176">下图是自适应卡片中屏蔽信息的示例：</span><span class="sxs-lookup"><span data-stu-id="8bad4-176">The following image is an example of masking information in Adaptive cards:</span></span>

![屏蔽信息图像](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a><span data-ttu-id="8bad4-178">全宽自适应卡片</span><span class="sxs-lookup"><span data-stu-id="8bad4-178">Full width Adaptive card</span></span>
<span data-ttu-id="8bad4-179">可以使用 属性扩展自适应卡片的宽度， `msteams` 并占用额外的画布空间。</span><span class="sxs-lookup"><span data-stu-id="8bad4-179">You can use the `msteams` property to expand the width of an Adaptive card and make use of additional canvas space.</span></span> <span data-ttu-id="8bad4-180">有关如何使用 属性的信息，请参阅以下示例：</span><span class="sxs-lookup"><span data-stu-id="8bad4-180">For information on how to use the property, see the following example:</span></span>

#### <a name="constructing-full-width-cards"></a><span data-ttu-id="8bad4-181">构造全宽卡片</span><span class="sxs-lookup"><span data-stu-id="8bad4-181">Constructing full width cards</span></span>
<span data-ttu-id="8bad4-182">若要制作全宽自适应卡片，必须将卡片内容 `width` `msteams` 中的 属性中的 对象设置为 `Full` 。</span><span class="sxs-lookup"><span data-stu-id="8bad4-182">To make a full width Adaptive card the `width` object in `msteams` property in the card content must be set to `Full`.</span></span>
<span data-ttu-id="8bad4-183">此外，你的应用必须包含以下元素：</span><span class="sxs-lookup"><span data-stu-id="8bad4-183">In addition, your app must include the following elements:</span></span>

#### <a name="sample-adaptive-card-with-full-width"></a><span data-ttu-id="8bad4-184">全宽自适应卡片示例</span><span class="sxs-lookup"><span data-stu-id="8bad4-184">Sample adaptive card with full width</span></span>

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

<span data-ttu-id="8bad4-185">完整宽度自适应卡片如下所示： ![ 全宽自适应卡片视图](../../assets/images/cards/full-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="8bad4-185">A full width Adaptive Card appears as follows: ![Full width Adaptive Card view](../../assets/images/cards/full-width-adaptive-card.png)</span></span>

<span data-ttu-id="8bad4-186">如果尚未将属性设置为 `width` *Full，* 则自适应卡片的默认视图如下所示： ![ 小宽度自适应卡片视图](../../assets/images/cards/small-width-adaptive-card.png)</span><span class="sxs-lookup"><span data-stu-id="8bad4-186">If you have not set the `width` property to *Full*, then the default view of the Adaptive Card is as follows: ![Small width Adaptive Card view](../../assets/images/cards/small-width-adaptive-card.png)</span></span>

### <a name="typeahead-support"></a><span data-ttu-id="8bad4-187">Typeahead 支持</span><span class="sxs-lookup"><span data-stu-id="8bad4-187">Typeahead support</span></span>

<span data-ttu-id="8bad4-188">在架构元素中，要求用户通过大量选择进行筛选可能会显著降低 [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) 任务完成速度。</span><span class="sxs-lookup"><span data-stu-id="8bad4-188">Within the [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) schema element, asking users to filter through and select through a sizable number of choices can significantly slow down task completion.</span></span> <span data-ttu-id="8bad4-189">自适应卡片中的 Typeahead 支持可以在用户键入输入时缩小或筛选输入选项集，从而简化输入选择。</span><span class="sxs-lookup"><span data-stu-id="8bad4-189">Typeahead support within Adaptive cards can simplify input selection by narrowing or filtering the set of input choices as a user is typing the input.</span></span> 

#### <a name="enable-typeahead-in-adaptive-cards"></a><span data-ttu-id="8bad4-190">在自适应卡片中启用 typeahead</span><span class="sxs-lookup"><span data-stu-id="8bad4-190">Enable typeahead in Adaptive cards</span></span>

<span data-ttu-id="8bad4-191">若要在 设置为 内启用 `Input.Choiceset` `style` typeahead， `filtered` 并确保 `isMultiSelect` 设置为 `false` 。</span><span class="sxs-lookup"><span data-stu-id="8bad4-191">To enable typeahead within the `Input.Choiceset` set `style` to `filtered` and ensure `isMultiSelect` is set to `false`.</span></span> 

#### <a name="sample-adaptive-card-with-typeahead-support"></a><span data-ttu-id="8bad4-192">具有 typeahead 支持的示例自适应卡片</span><span class="sxs-lookup"><span data-stu-id="8bad4-192">Sample adaptive card with typeahead support</span></span>

``` json
{
   "type": "Input.ChoiceSet",
   "label": "Select a user",
   "isMultiSelect": false,
   "choices":  [
      { "title": "User 1", "value": "User1" },
      { "title": "User 2", "value": "User2" }
    ],
   "style": "filtered"
}
``` 

### <a name="stage-view-for-images-in-adaptive-cards"></a><span data-ttu-id="8bad4-193">自适应卡片中的图像阶段视图</span><span class="sxs-lookup"><span data-stu-id="8bad4-193">Stage view for images in Adaptive Cards</span></span>
<span data-ttu-id="8bad4-194">在自适应卡片中，可以使用 属性添加选择性地在阶段 `msteams` 视图中显示图像的能力。</span><span class="sxs-lookup"><span data-stu-id="8bad4-194">In an Adaptive card, you can use the `msteams` property to add the ability to display images in stage view selectively.</span></span> <span data-ttu-id="8bad4-195">当用户将鼠标悬停在图像上时，他们将看到展开图标，其 `allowExpand` 属性设置为 `true` 。</span><span class="sxs-lookup"><span data-stu-id="8bad4-195">When users hover over the images, they would see an expand icon, for which the `allowExpand` attribute is set to `true`.</span></span> <span data-ttu-id="8bad4-196">有关如何使用 属性的信息，请参阅以下示例：</span><span class="sxs-lookup"><span data-stu-id="8bad4-196">For information on how to use the property, see the following example:</span></span>

``` json
{
    "type": "AdaptiveCard",
     "body": [
          {
            "type": "Image",
            "url": "https://picsum.photos/200/200?image=110",
            "msTeams": {
              "allowExpand": true
            }
          },
     ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

<span data-ttu-id="8bad4-197">当用户将鼠标悬停在图像上方时，图像右上角将显示展开图标：带可展开图像的自适应 ![ 卡片](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span><span class="sxs-lookup"><span data-stu-id="8bad4-197">When users hover over the image, an expand icon appears at top right corner of the image: ![Adaptive card with expandable image](../../assets/images/cards/adaptivecard-hover-expand-icon.png)</span></span>

<span data-ttu-id="8bad4-198">当用户选择展开按钮时，图像显示在阶段视图中：展开 ![ 到阶段视图的图像](../../assets/images/cards/adaptivecard-expand-image.png)</span><span class="sxs-lookup"><span data-stu-id="8bad4-198">The image appears in stage view when the user selects the expand button: ![Image expanded to stage view](../../assets/images/cards/adaptivecard-expand-image.png)</span></span>

<span data-ttu-id="8bad4-199">在阶段视图中，用户可以放大和缩小图像。</span><span class="sxs-lookup"><span data-stu-id="8bad4-199">In the stage view, users can zoom in and zoom out of the image.</span></span> <span data-ttu-id="8bad4-200">可以选择自适应卡片中的哪些图像需要具备此功能。</span><span class="sxs-lookup"><span data-stu-id="8bad4-200">You can select which images in your Adaptive card needs to have this capability.</span></span>

> [!NOTE]
> <span data-ttu-id="8bad4-201">放大和缩小功能仅适用于自适应卡片 (图像) 图像元素。</span><span class="sxs-lookup"><span data-stu-id="8bad4-201">Zoom in and zoom out capability applies only to the image elements (Image type) in an Adaptive card.</span></span>

> [!NOTE]
> <span data-ttu-id="8bad4-202">对于 Teams 移动应用，自适应卡片中的图像阶段视图功能默认可用，用户只需点击图像即可在阶段视图中查看自适应卡片图像，而不管属性是否 `allowExpand` 存在。</span><span class="sxs-lookup"><span data-stu-id="8bad4-202">For Teams mobile apps, stage view functionality for images in Adaptive Cards are available by default and users will be able to view Adaptive card images in stage view by simply tapping on the image, irrespective of whether the `allowExpand` attribute is present or not.</span></span>

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="8bad4-203">**Markdown 格式：O365 连接器卡**</span><span class="sxs-lookup"><span data-stu-id="8bad4-203">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="8bad4-204">连接器卡支持有限的 Markdown 和 HTML 格式。</span><span class="sxs-lookup"><span data-stu-id="8bad4-204">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="8bad4-205">HTML 支持在上一节中介绍。</span><span class="sxs-lookup"><span data-stu-id="8bad4-205">HTML support is described in the last section.</span></span>

| <span data-ttu-id="8bad4-206">样式</span><span class="sxs-lookup"><span data-stu-id="8bad4-206">Style</span></span> | <span data-ttu-id="8bad4-207">示例</span><span class="sxs-lookup"><span data-stu-id="8bad4-207">Example</span></span> | <span data-ttu-id="8bad4-208">Markdown</span><span class="sxs-lookup"><span data-stu-id="8bad4-208">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8bad4-209">bold</span><span class="sxs-lookup"><span data-stu-id="8bad4-209">bold</span></span> | <span data-ttu-id="8bad4-210">**text**</span><span class="sxs-lookup"><span data-stu-id="8bad4-210">**text**</span></span> | `**text**` |
| <span data-ttu-id="8bad4-211">italic</span><span class="sxs-lookup"><span data-stu-id="8bad4-211">italic</span></span> | <span data-ttu-id="8bad4-212">*text*</span><span class="sxs-lookup"><span data-stu-id="8bad4-212">*text*</span></span> | `*text*` |
| <span data-ttu-id="8bad4-213">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="8bad4-213">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="8bad4-214">**Text**</span><span class="sxs-lookup"><span data-stu-id="8bad4-214">**Text**</span></span> | `### Text`|
| <span data-ttu-id="8bad4-215">strikethrough</span><span class="sxs-lookup"><span data-stu-id="8bad4-215">strikethrough</span></span> | <span data-ttu-id="8bad4-216">~~text~~</span><span class="sxs-lookup"><span data-stu-id="8bad4-216">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="8bad4-217">无序列表</span><span class="sxs-lookup"><span data-stu-id="8bad4-217">unordered list</span></span> | <ul><li><span data-ttu-id="8bad4-218">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-218">text</span></span></li><li><span data-ttu-id="8bad4-219">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-219">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="8bad4-220">排序列表</span><span class="sxs-lookup"><span data-stu-id="8bad4-220">ordered list</span></span> | <ol><li><span data-ttu-id="8bad4-221">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-221">text</span></span></li><li><span data-ttu-id="8bad4-222">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-222">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="8bad4-223">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="8bad4-223">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="8bad4-224">blockquote</span><span class="sxs-lookup"><span data-stu-id="8bad4-224">blockquote</span></span> | <span data-ttu-id="8bad4-225">>blockquote 文本</span><span class="sxs-lookup"><span data-stu-id="8bad4-225">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="8bad4-226">超链接</span><span class="sxs-lookup"><span data-stu-id="8bad4-226">hyperlink</span></span> | [<span data-ttu-id="8bad4-227">必应</span><span class="sxs-lookup"><span data-stu-id="8bad4-227">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="8bad4-228">图像链接</span><span class="sxs-lookup"><span data-stu-id="8bad4-228">image link</span></span> |![在一个地心上闪避](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="8bad4-230">在连接器卡中，为 呈现新行 `\n\n` ，但不为 或 `\n` 呈现 `\r` 。</span><span class="sxs-lookup"><span data-stu-id="8bad4-230">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="8bad4-231">使用 Markdown 的连接器卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="8bad4-231">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="8bad4-232">在桌面上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="8bad4-232">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![桌面客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="8bad4-234">在 iOS 上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="8bad4-234">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![iOS 客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="8bad4-236">问题：</span><span class="sxs-lookup"><span data-stu-id="8bad4-236">Issues:</span></span>

* <span data-ttu-id="8bad4-237">适用于 Teams 的 iOS 客户端不会在连接器卡中呈现 Markdown 或 HTML 内嵌图像。</span><span class="sxs-lookup"><span data-stu-id="8bad4-237">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="8bad4-238">Blockquotes 呈现为缩进，但不带灰色背景。</span><span class="sxs-lookup"><span data-stu-id="8bad4-238">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="8bad4-239">在 Android 上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="8bad4-239">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Android 客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="8bad4-241">Markdown 连接器卡的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="8bad4-241">Formatting example for Markdown Connector Cards</span></span>

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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="8bad4-242">使用 HTML 设置卡片格式</span><span class="sxs-lookup"><span data-stu-id="8bad4-242">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="8bad4-243">**HTML 格式：O365 连接器卡**</span><span class="sxs-lookup"><span data-stu-id="8bad4-243">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="8bad4-244">连接器卡支持有限的 Markdown 和 HTML 格式。</span><span class="sxs-lookup"><span data-stu-id="8bad4-244">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="8bad4-245">Markdown 将下一节介绍。</span><span class="sxs-lookup"><span data-stu-id="8bad4-245">Markdown is described in the next section.</span></span>

| <span data-ttu-id="8bad4-246">样式</span><span class="sxs-lookup"><span data-stu-id="8bad4-246">Style</span></span> | <span data-ttu-id="8bad4-247">示例</span><span class="sxs-lookup"><span data-stu-id="8bad4-247">Example</span></span> | <span data-ttu-id="8bad4-248">HTML</span><span class="sxs-lookup"><span data-stu-id="8bad4-248">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8bad4-249">bold</span><span class="sxs-lookup"><span data-stu-id="8bad4-249">bold</span></span> | <span data-ttu-id="8bad4-250">**text**</span><span class="sxs-lookup"><span data-stu-id="8bad4-250">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="8bad4-251">italic</span><span class="sxs-lookup"><span data-stu-id="8bad4-251">italic</span></span> | <span data-ttu-id="8bad4-252">*text*</span><span class="sxs-lookup"><span data-stu-id="8bad4-252">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="8bad4-253">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="8bad4-253">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="8bad4-254">**Text**</span><span class="sxs-lookup"><span data-stu-id="8bad4-254">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="8bad4-255">strikethrough</span><span class="sxs-lookup"><span data-stu-id="8bad4-255">strikethrough</span></span> | <span data-ttu-id="8bad4-256">~~text~~</span><span class="sxs-lookup"><span data-stu-id="8bad4-256">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="8bad4-257">无序列表</span><span class="sxs-lookup"><span data-stu-id="8bad4-257">unordered list</span></span> | <ul><li><span data-ttu-id="8bad4-258">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-258">text</span></span></li><li><span data-ttu-id="8bad4-259">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-259">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="8bad4-260">排序列表</span><span class="sxs-lookup"><span data-stu-id="8bad4-260">ordered list</span></span> | <ol><li><span data-ttu-id="8bad4-261">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-261">text</span></span></li><li><span data-ttu-id="8bad4-262">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-262">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="8bad4-263">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="8bad4-263">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="8bad4-264">blockquote</span><span class="sxs-lookup"><span data-stu-id="8bad4-264">blockquote</span></span> | <blockquote><span data-ttu-id="8bad4-265">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-265">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="8bad4-266">超链接</span><span class="sxs-lookup"><span data-stu-id="8bad4-266">hyperlink</span></span> | [<span data-ttu-id="8bad4-267">必应</span><span class="sxs-lookup"><span data-stu-id="8bad4-267">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="8bad4-268">图像链接</span><span class="sxs-lookup"><span data-stu-id="8bad4-268">image link</span></span> | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="8bad4-269">在连接器卡中，使用 标记以 HTML 格式呈现 `<p>` 新行。</span><span class="sxs-lookup"><span data-stu-id="8bad4-269">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="8bad4-270">使用 HTML 的连接器卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="8bad4-270">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="8bad4-271">在桌面上，连接器卡的 HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="8bad4-271">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![桌面客户端中连接器卡的 HTML 格式](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="8bad4-273">在 iOS 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="8bad4-273">On iOS, HTML formatting looks like this:</span></span>

![iOS 客户端中连接器卡的 HTML 格式](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="8bad4-275">问题：</span><span class="sxs-lookup"><span data-stu-id="8bad4-275">Issues:</span></span>

* <span data-ttu-id="8bad4-276">内联图像不会使用连接器卡中的 Markdown 或 HTML 呈现在 iOS 上。</span><span class="sxs-lookup"><span data-stu-id="8bad4-276">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="8bad4-277">呈现预设格式的文本，但没有灰色背景。</span><span class="sxs-lookup"><span data-stu-id="8bad4-277">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="8bad4-278">在 Android 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="8bad4-278">On Android, HTML formatting looks like this:</span></span>

![Android 客户端中连接器卡的 HTML 格式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="8bad4-280">HTML 连接器卡的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="8bad4-280">Formatting sample for HTML Connector Cards</span></span>

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="8bad4-281">**HTML 格式：hero 和 thumbnail 卡片**</span><span class="sxs-lookup"><span data-stu-id="8bad4-281">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="8bad4-282">HTML 标记支持简单的卡片，如 hero 和 thumbnail 卡片。</span><span class="sxs-lookup"><span data-stu-id="8bad4-282">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="8bad4-283">不支持 Markdown。</span><span class="sxs-lookup"><span data-stu-id="8bad4-283">Markdown is not supported.</span></span>

| <span data-ttu-id="8bad4-284">样式</span><span class="sxs-lookup"><span data-stu-id="8bad4-284">Style</span></span> | <span data-ttu-id="8bad4-285">示例</span><span class="sxs-lookup"><span data-stu-id="8bad4-285">Example</span></span> | <span data-ttu-id="8bad4-286">HTML</span><span class="sxs-lookup"><span data-stu-id="8bad4-286">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8bad4-287">bold</span><span class="sxs-lookup"><span data-stu-id="8bad4-287">bold</span></span> | <span data-ttu-id="8bad4-288">**text**</span><span class="sxs-lookup"><span data-stu-id="8bad4-288">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="8bad4-289">italic</span><span class="sxs-lookup"><span data-stu-id="8bad4-289">italic</span></span> | <span data-ttu-id="8bad4-290">*text*</span><span class="sxs-lookup"><span data-stu-id="8bad4-290">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="8bad4-291">页眉 (级别 1 &ndash; 3) </span><span class="sxs-lookup"><span data-stu-id="8bad4-291">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="8bad4-292">**Text**</span><span class="sxs-lookup"><span data-stu-id="8bad4-292">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="8bad4-293">strikethrough</span><span class="sxs-lookup"><span data-stu-id="8bad4-293">strikethrough</span></span> | <span data-ttu-id="8bad4-294">~~text~~</span><span class="sxs-lookup"><span data-stu-id="8bad4-294">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="8bad4-295">无序列表</span><span class="sxs-lookup"><span data-stu-id="8bad4-295">unordered list</span></span> | <ul><li><span data-ttu-id="8bad4-296">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-296">text</span></span></li><li><span data-ttu-id="8bad4-297">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-297">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="8bad4-298">排序列表</span><span class="sxs-lookup"><span data-stu-id="8bad4-298">ordered list</span></span> | <ol><li><span data-ttu-id="8bad4-299">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-299">text</span></span></li><li><span data-ttu-id="8bad4-300">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-300">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="8bad4-301">预设格式的文本</span><span class="sxs-lookup"><span data-stu-id="8bad4-301">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="8bad4-302">blockquote</span><span class="sxs-lookup"><span data-stu-id="8bad4-302">blockquote</span></span> | <blockquote><span data-ttu-id="8bad4-303">text</span><span class="sxs-lookup"><span data-stu-id="8bad4-303">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="8bad4-304">超链接</span><span class="sxs-lookup"><span data-stu-id="8bad4-304">hyperlink</span></span> | [<span data-ttu-id="8bad4-305">必应</span><span class="sxs-lookup"><span data-stu-id="8bad4-305">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="8bad4-306">图像链接</span><span class="sxs-lookup"><span data-stu-id="8bad4-306">image link</span></span> |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="8bad4-307">简单卡片的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="8bad4-307">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="8bad4-308">由于桌面平台和移动平台的分辨率差异，桌面版和移动版 Teams 的格式不同。</span><span class="sxs-lookup"><span data-stu-id="8bad4-308">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="8bad4-309">在桌面上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="8bad4-309">On the desktop, HTML formatting appears like this:</span></span>

![桌面客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="8bad4-311">在 iOS 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="8bad4-311">On iOS, HTML formatting appears like this:</span></span>

![iOS 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="8bad4-313">问题：</span><span class="sxs-lookup"><span data-stu-id="8bad4-313">Issues:</span></span>

* <span data-ttu-id="8bad4-314">粗体和 italic 等字符格式不会呈现在 iOS 上。</span><span class="sxs-lookup"><span data-stu-id="8bad4-314">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="8bad4-315">在 Android 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="8bad4-315">On Android, HTML formatting appears like this:</span></span>

![Android 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="8bad4-317">在 Android 上正确显示粗体和 italic 等字符格式。</span><span class="sxs-lookup"><span data-stu-id="8bad4-317">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="8bad4-318">简单卡片中 HTML 格式的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="8bad4-318">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="8bad4-319">这些屏幕截图是使用 Teams AppStudio 创建的，其中 Hero 卡片的文本属性设置为以下字符串。</span><span class="sxs-lookup"><span data-stu-id="8bad4-319">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="8bad4-320">可以通过修改此代码在你自己的卡片中测试格式。</span><span class="sxs-lookup"><span data-stu-id="8bad4-320">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
