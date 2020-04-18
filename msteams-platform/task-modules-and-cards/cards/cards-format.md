---
title: 卡片中的文本格式
description: 描述 Microsoft 团队中的卡片文本格式
keywords: 团队 bot 卡片格式
ms.date: 03/29/2018
ms.openlocfilehash: 9ced8a8956265322e91b9d40dc7dc7064ee4659f
ms.sourcegitcommit: 510ae42f72798fb24ddef0afa771ecd9d38e5348
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/17/2020
ms.locfileid: "43550950"
---
# <a name="format-cards-in-teams"></a><span data-ttu-id="a7482-104">设置团队中卡片的格式</span><span class="sxs-lookup"><span data-stu-id="a7482-104">Format cards in Teams</span></span>

<span data-ttu-id="a7482-105">您可以使用 Markdown 或 HTML 向卡片添加格式文本格式，具体取决于卡片类型。</span><span class="sxs-lookup"><span data-stu-id="a7482-105">You can add rich text formatting to your cards using either Markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="a7482-106">卡片仅支持 text 属性中的格式设置，而不支持标题或副标题属性中的格式设置。</span><span class="sxs-lookup"><span data-stu-id="a7482-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="a7482-107">可以使用 XML （HTML）格式子集或 Markdown （具体取决于卡片类型）指定格式。</span><span class="sxs-lookup"><span data-stu-id="a7482-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="a7482-108">对于当前和将来使用 Markdown 格式的开发自适应卡片，建议使用格式设置。</span><span class="sxs-lookup"><span data-stu-id="a7482-108">For current and future development Adaptive cards using Markdown formatting is recommended.</span></span>

<span data-ttu-id="a7482-109">不同的卡片类型之间的格式支持不同，在桌面和移动团队客户端以及桌面浏览器中的团队之间，卡片的呈现可能略有不同。</span><span class="sxs-lookup"><span data-stu-id="a7482-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

<span data-ttu-id="a7482-110">可以在任何团队卡片中添加内嵌图像。</span><span class="sxs-lookup"><span data-stu-id="a7482-110">You can include an inline image with any Teams card.</span></span> <span data-ttu-id="a7482-111">图像的格式为`.png`、 `.jpg`或`.gif`文件，不得超过1024× 1024 px 或 1 MB。</span><span class="sxs-lookup"><span data-stu-id="a7482-111">Images an be formatted as  `.png`, `.jpg`, or `.gif` files and must not exceed 1024 ×1024 px or 1 MB.</span></span> <span data-ttu-id="a7482-112">不正式支持动画 GIF。</span><span class="sxs-lookup"><span data-stu-id="a7482-112">Animated GIF is not officially supported.</span></span> <span data-ttu-id="a7482-113">*请参阅*[卡片参考](./cards-reference.md#inline-card-images)</span><span class="sxs-lookup"><span data-stu-id="a7482-113">*See* [Cards reference](./cards-reference.md#inline-card-images)</span></span>

## <a name="formatting-cards-with-markdown"></a><span data-ttu-id="a7482-114">使用 Markdown 设置卡片格式</span><span class="sxs-lookup"><span data-stu-id="a7482-114">Formatting cards with Markdown</span></span>

<span data-ttu-id="a7482-115">有两种卡类型支持团队中的 Markdown：</span><span class="sxs-lookup"><span data-stu-id="a7482-115">There are two card types that support Markdown in Teams:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="a7482-116">**自适应卡片**： Markdown 在自适应卡片`Textblock`字段以及`Fact.Title`和`Fact.Value`中受支持。</span><span class="sxs-lookup"><span data-stu-id="a7482-116">**Adaptive Cards**: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="a7482-117">自适应卡片中不支持 HTML。</span><span class="sxs-lookup"><span data-stu-id="a7482-117">HTML is not supported in adaptive cards.</span></span>
> * <span data-ttu-id="a7482-118">**O365 连接器卡片**：文本字段中的 Office 365 连接器卡片支持 Markdown 和有限的 HTML。</span><span class="sxs-lookup"><span data-stu-id="a7482-118">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>

# <a name="markdown-formatting-adaptive-cards"></a>[<span data-ttu-id="a7482-119">**Markdown 格式：自适应卡片**</span><span class="sxs-lookup"><span data-stu-id="a7482-119">**Markdown formatting: Adaptive Cards**</span></span>](#tab/adaptive-md)

 <span data-ttu-id="a7482-120">支持的`Fact.Title`和`Fact.Value`的`Textblock`样式如下：</span><span class="sxs-lookup"><span data-stu-id="a7482-120">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="a7482-121">Style</span><span class="sxs-lookup"><span data-stu-id="a7482-121">Style</span></span> | <span data-ttu-id="a7482-122">示例</span><span class="sxs-lookup"><span data-stu-id="a7482-122">Example</span></span> | <span data-ttu-id="a7482-123">Markdown</span><span class="sxs-lookup"><span data-stu-id="a7482-123">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7482-124">bold</span><span class="sxs-lookup"><span data-stu-id="a7482-124">bold</span></span> | <span data-ttu-id="a7482-125">**Bold**</span><span class="sxs-lookup"><span data-stu-id="a7482-125">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="a7482-126">italic</span><span class="sxs-lookup"><span data-stu-id="a7482-126">italic</span></span> | <span data-ttu-id="a7482-127">_Italic_</span><span class="sxs-lookup"><span data-stu-id="a7482-127">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="a7482-128">无序列表</span><span class="sxs-lookup"><span data-stu-id="a7482-128">unordered list</span></span> | <ul><li><span data-ttu-id="a7482-129">text</span><span class="sxs-lookup"><span data-stu-id="a7482-129">text</span></span></li><li><span data-ttu-id="a7482-130">text</span><span class="sxs-lookup"><span data-stu-id="a7482-130">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="a7482-131">排序列表</span><span class="sxs-lookup"><span data-stu-id="a7482-131">ordered list</span></span> | <ol><li><span data-ttu-id="a7482-132">text</span><span class="sxs-lookup"><span data-stu-id="a7482-132">text</span></span></li><li><span data-ttu-id="a7482-133">text</span><span class="sxs-lookup"><span data-stu-id="a7482-133">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="a7482-134">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="a7482-134">Hyperlinks</span></span> |[<span data-ttu-id="a7482-135">必应</span><span class="sxs-lookup"><span data-stu-id="a7482-135">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="a7482-136">以下 Markdown 标记不受支持：</span><span class="sxs-lookup"><span data-stu-id="a7482-136">The following Markdown tags are not supported:</span></span>

* <span data-ttu-id="a7482-137">标头</span><span class="sxs-lookup"><span data-stu-id="a7482-137">Headers</span></span>
* <span data-ttu-id="a7482-138">表格</span><span class="sxs-lookup"><span data-stu-id="a7482-138">Tables</span></span>
* <span data-ttu-id="a7482-139">图像</span><span class="sxs-lookup"><span data-stu-id="a7482-139">Images</span></span>
* <span data-ttu-id="a7482-140">预设格式文本</span><span class="sxs-lookup"><span data-stu-id="a7482-140">Preformatted text</span></span>
* <span data-ttu-id="a7482-141">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="a7482-141">Blockquotes</span></span>

> [!IMPORTANT]
> <span data-ttu-id="a7482-142">自适应卡片不支持任何 HTML 格式设置。</span><span class="sxs-lookup"><span data-stu-id="a7482-142">Adaptive cards do not support any HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="a7482-143">自适应卡片的换行符</span><span class="sxs-lookup"><span data-stu-id="a7482-143">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="a7482-144">在 "列表" `\r`中，可以`\n`对换行符使用或转义序列。</span><span class="sxs-lookup"><span data-stu-id="a7482-144">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="a7482-145">在`\n\n`列表中使用将导致缩进列表中的下一个元素。</span><span class="sxs-lookup"><span data-stu-id="a7482-145">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="a7482-146">如果需要在 textblock 中的其他位置使用换行符`\n\n`，请使用。</span><span class="sxs-lookup"><span data-stu-id="a7482-146">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="a7482-147">自适应卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="a7482-147">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="a7482-148">桌面和团队的移动版之间的格式略有不同。</span><span class="sxs-lookup"><span data-stu-id="a7482-148">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="a7482-149">在桌面上，自适应卡片 Markdown 格式在 web 浏览器和团队客户端应用程序中的显示格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="a7482-149">On the desktop, Adaptive Card Markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![自适应卡片 Markdown 桌面客户端中的格式设置](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="a7482-151">在 iOS 上，自适应卡片 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="a7482-151">On iOS, Adaptive Card Markdown formatting appears like this:</span></span>

![自适应卡片 Markdown 格式在 iOS 中](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="a7482-153">在 Android 上，自适应卡片 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="a7482-153">On Android, Adaptive Card Markdown formatting appears like this:</span></span>

![Android 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a><span data-ttu-id="a7482-155">有关自适应卡片的详细信息</span><span class="sxs-lookup"><span data-stu-id="a7482-155">More information on Adaptive Cards</span></span>

<span data-ttu-id="a7482-156">[自适应卡片中的文本功能](/adaptive-cards/create/textfeatures)团队不支持本主题中提及的日期和本地化功能。</span><span class="sxs-lookup"><span data-stu-id="a7482-156">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="a7482-157">自适应卡片的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="a7482-157">Formatting sample for Adaptive cards</span></span>

``` json
{
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
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
            "text": "Check out [Adaptive Cards](http://adaptivecards.io)"
        }
    ]
}
```

### <a name="mention-support-within-adaptive-cards"></a><span data-ttu-id="a7482-158">提及自适应卡片中的支持</span><span class="sxs-lookup"><span data-stu-id="a7482-158">Mention support within Adaptive cards</span></span>

> [!NOTE]
> <span data-ttu-id="a7482-159">在[开发人员预览版](../../resources/dev-preview/developer-preview-intro.md)中，目前仅支持对卡片中提及支持。</span><span class="sxs-lookup"><span data-stu-id="a7482-159">Mention support in cards is currently supported in [Developer Preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="a7482-160">Bot 和邮件扩展现在可以在文本块和 FactSet 元素中包括卡片内容中提及的内容。</span><span class="sxs-lookup"><span data-stu-id="a7482-160">Bots and Messaging extensions can now include mentions within the card content in Text Block and FactSet elements.</span></span>

### <a name="constructing-mentions"></a><span data-ttu-id="a7482-161">构建提及</span><span class="sxs-lookup"><span data-stu-id="a7482-161">Constructing mentions</span></span>

<span data-ttu-id="a7482-162">若要在自适应卡片中添加提及的内容，应用需要包含以下元素</span><span class="sxs-lookup"><span data-stu-id="a7482-162">To include a mention in an Adaptive Card your app needs to include the following elements</span></span>

* <span data-ttu-id="a7482-163">`<at>username</at>`在支持的自适应卡片元素中</span><span class="sxs-lookup"><span data-stu-id="a7482-163">`<at>username</at>` in the supported adaptive card elements</span></span>
* <span data-ttu-id="a7482-164">卡片`mention`内容中`msteams`属性内的对象，其中包括所提及用户的团队用户 id</span><span class="sxs-lookup"><span data-stu-id="a7482-164">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

<span data-ttu-id="a7482-165">请注意，目前移动客户端上不支持带有提及的卡片。</span><span class="sxs-lookup"><span data-stu-id="a7482-165">Note that cards with mentions aren't supported on mobile clients at the moment.</span></span>

### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="a7482-166">带提及的示例自适应卡片</span><span class="sxs-lookup"><span data-stu-id="a7482-166">Sample Adaptive card with a mention</span></span>

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
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
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

# <a name="markdown-formatting-o365-connector-cards"></a>[<span data-ttu-id="a7482-167">**Markdown 格式： O365 连接器卡**</span><span class="sxs-lookup"><span data-stu-id="a7482-167">**Markdown formatting: O365 Connector Cards**</span></span>](#tab/connector-md)

<span data-ttu-id="a7482-168">连接器卡支持有限的 Markdown 和 HTML 格式设置。</span><span class="sxs-lookup"><span data-stu-id="a7482-168">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="a7482-169">上一节中介绍了 HTML 支持。</span><span class="sxs-lookup"><span data-stu-id="a7482-169">HTML support is described in the last section.</span></span>

| <span data-ttu-id="a7482-170">Style</span><span class="sxs-lookup"><span data-stu-id="a7482-170">Style</span></span> | <span data-ttu-id="a7482-171">示例</span><span class="sxs-lookup"><span data-stu-id="a7482-171">Example</span></span> | <span data-ttu-id="a7482-172">Markdown</span><span class="sxs-lookup"><span data-stu-id="a7482-172">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7482-173">bold</span><span class="sxs-lookup"><span data-stu-id="a7482-173">bold</span></span> | <span data-ttu-id="a7482-174">**text**</span><span class="sxs-lookup"><span data-stu-id="a7482-174">**text**</span></span> | `**text**` |
| <span data-ttu-id="a7482-175">italic</span><span class="sxs-lookup"><span data-stu-id="a7482-175">italic</span></span> | <span data-ttu-id="a7482-176">*text*</span><span class="sxs-lookup"><span data-stu-id="a7482-176">*text*</span></span> | `*text*` |
| <span data-ttu-id="a7482-177">标头（级别&ndash;1 3）</span><span class="sxs-lookup"><span data-stu-id="a7482-177">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="a7482-178">**Text**</span><span class="sxs-lookup"><span data-stu-id="a7482-178">**Text**</span></span> | `### Text`|
| <span data-ttu-id="a7482-179">删除</span><span class="sxs-lookup"><span data-stu-id="a7482-179">strikethrough</span></span> | <span data-ttu-id="a7482-180">~~text~~</span><span class="sxs-lookup"><span data-stu-id="a7482-180">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="a7482-181">无序列表</span><span class="sxs-lookup"><span data-stu-id="a7482-181">unordered list</span></span> | <ul><li><span data-ttu-id="a7482-182">text</span><span class="sxs-lookup"><span data-stu-id="a7482-182">text</span></span></li><li><span data-ttu-id="a7482-183">text</span><span class="sxs-lookup"><span data-stu-id="a7482-183">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="a7482-184">排序列表</span><span class="sxs-lookup"><span data-stu-id="a7482-184">ordered list</span></span> | <ol><li><span data-ttu-id="a7482-185">text</span><span class="sxs-lookup"><span data-stu-id="a7482-185">text</span></span></li><li><span data-ttu-id="a7482-186">text</span><span class="sxs-lookup"><span data-stu-id="a7482-186">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="a7482-187">预设格式文本</span><span class="sxs-lookup"><span data-stu-id="a7482-187">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="a7482-188">blockquote</span><span class="sxs-lookup"><span data-stu-id="a7482-188">blockquote</span></span> | <span data-ttu-id="a7482-189">>blockquote 文本</span><span class="sxs-lookup"><span data-stu-id="a7482-189">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="a7482-190">超链接</span><span class="sxs-lookup"><span data-stu-id="a7482-190">hyperlink</span></span> | [<span data-ttu-id="a7482-191">必应</span><span class="sxs-lookup"><span data-stu-id="a7482-191">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="a7482-192">图像链接</span><span class="sxs-lookup"><span data-stu-id="a7482-192">image link</span></span> |![在摇滚上的工作](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="a7482-194">在连接器卡中，将为`\n\n`（而不是为`\n`或`\r`）呈现换行符。</span><span class="sxs-lookup"><span data-stu-id="a7482-194">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="a7482-195">使用 Markdown 的连接器卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="a7482-195">Mobile and desktop differences for connector cards using Markdown</span></span>

<span data-ttu-id="a7482-196">在桌面上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="a7482-196">On the desktop, Markdown formatting for connector cards looks like this:</span></span>

![桌面客户端中的连接器卡的 Markdown 格式](../../assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="a7482-198">在 iOS 上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="a7482-198">On iOS, Markdown formatting for connector cards looks like this:</span></span>

![IOS 客户端中的连接器卡的 Markdown 格式](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="a7482-200">问题：</span><span class="sxs-lookup"><span data-stu-id="a7482-200">Issues:</span></span>

* <span data-ttu-id="a7482-201">团队的 iOS 客户端不会在连接器卡片中呈现 Markdown 或 HTML 嵌入式图像。</span><span class="sxs-lookup"><span data-stu-id="a7482-201">The iOS client for Teams does not render Markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="a7482-202">Blockquotes 呈现为缩进但不带灰色背景。</span><span class="sxs-lookup"><span data-stu-id="a7482-202">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="a7482-203">在 Android 上，连接器卡的 Markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="a7482-203">On Android, Markdown formatting for connector cards looks like this:</span></span>

![Android 客户端中的连接器卡的 Markdown 格式](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="a7482-205">Markdown 连接器卡的格式示例</span><span class="sxs-lookup"><span data-stu-id="a7482-205">Formatting example for Markdown Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
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
            "text": "embedded image link: ![Duck on a rock](http://aka.ms/Fo983c)"
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

## <a name="formatting-cards-with-html"></a><span data-ttu-id="a7482-206">使用 HTML 格式化卡片</span><span class="sxs-lookup"><span data-stu-id="a7482-206">Formatting cards with HTML</span></span>

# <a name="html-formatting-o365-connector-cards"></a>[<span data-ttu-id="a7482-207">**HTML 格式： O365 连接器卡**</span><span class="sxs-lookup"><span data-stu-id="a7482-207">**HTML formatting: O365 Connector Cards**</span></span>](#tab/connector-html)

<span data-ttu-id="a7482-208">连接器卡支持有限的 Markdown 和 HTML 格式设置。</span><span class="sxs-lookup"><span data-stu-id="a7482-208">Connector cards support limited Markdown and HTML formatting.</span></span> <span data-ttu-id="a7482-209">Markdown 将在下一节中介绍。</span><span class="sxs-lookup"><span data-stu-id="a7482-209">Markdown is described in the next section.</span></span>

| <span data-ttu-id="a7482-210">Style</span><span class="sxs-lookup"><span data-stu-id="a7482-210">Style</span></span> | <span data-ttu-id="a7482-211">示例</span><span class="sxs-lookup"><span data-stu-id="a7482-211">Example</span></span> | <span data-ttu-id="a7482-212">HTML</span><span class="sxs-lookup"><span data-stu-id="a7482-212">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7482-213">bold</span><span class="sxs-lookup"><span data-stu-id="a7482-213">bold</span></span> | <span data-ttu-id="a7482-214">**text**</span><span class="sxs-lookup"><span data-stu-id="a7482-214">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="a7482-215">italic</span><span class="sxs-lookup"><span data-stu-id="a7482-215">italic</span></span> | <span data-ttu-id="a7482-216">*text*</span><span class="sxs-lookup"><span data-stu-id="a7482-216">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="a7482-217">标头（级别&ndash;1 3）</span><span class="sxs-lookup"><span data-stu-id="a7482-217">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="a7482-218">**Text**</span><span class="sxs-lookup"><span data-stu-id="a7482-218">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="a7482-219">删除</span><span class="sxs-lookup"><span data-stu-id="a7482-219">strikethrough</span></span> | <span data-ttu-id="a7482-220">~~text~~</span><span class="sxs-lookup"><span data-stu-id="a7482-220">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="a7482-221">无序列表</span><span class="sxs-lookup"><span data-stu-id="a7482-221">unordered list</span></span> | <ul><li><span data-ttu-id="a7482-222">text</span><span class="sxs-lookup"><span data-stu-id="a7482-222">text</span></span></li><li><span data-ttu-id="a7482-223">text</span><span class="sxs-lookup"><span data-stu-id="a7482-223">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="a7482-224">排序列表</span><span class="sxs-lookup"><span data-stu-id="a7482-224">ordered list</span></span> | <ol><li><span data-ttu-id="a7482-225">text</span><span class="sxs-lookup"><span data-stu-id="a7482-225">text</span></span></li><li><span data-ttu-id="a7482-226">text</span><span class="sxs-lookup"><span data-stu-id="a7482-226">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="a7482-227">预设格式文本</span><span class="sxs-lookup"><span data-stu-id="a7482-227">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="a7482-228">blockquote</span><span class="sxs-lookup"><span data-stu-id="a7482-228">blockquote</span></span> | <blockquote><span data-ttu-id="a7482-229">text</span><span class="sxs-lookup"><span data-stu-id="a7482-229">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="a7482-230">超链接</span><span class="sxs-lookup"><span data-stu-id="a7482-230">hyperlink</span></span> | [<span data-ttu-id="a7482-231">必应</span><span class="sxs-lookup"><span data-stu-id="a7482-231">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="a7482-232">图像链接</span><span class="sxs-lookup"><span data-stu-id="a7482-232">image link</span></span> | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="a7482-233">在连接器卡中，使用`<p>`标记在 HTML 中呈现的换行符。</span><span class="sxs-lookup"><span data-stu-id="a7482-233">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="a7482-234">使用 HTML 的连接器卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="a7482-234">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="a7482-235">在桌面上，连接器卡的 HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="a7482-235">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![桌面客户端中的连接器卡的 HTML 格式](../../assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="a7482-237">在 iOS 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="a7482-237">On iOS, HTML formatting looks like this:</span></span>

![IOS 客户端中的连接器卡的 HTML 格式](../../assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="a7482-239">问题：</span><span class="sxs-lookup"><span data-stu-id="a7482-239">Issues:</span></span>

* <span data-ttu-id="a7482-240">嵌入式图像不是使用 Markdown 或 HTML in 连接器卡片呈现在 iOS 上。</span><span class="sxs-lookup"><span data-stu-id="a7482-240">Inline images are not rendered on iOS using either Markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="a7482-241">预设格式的文本将呈现，但不具有灰色背景。</span><span class="sxs-lookup"><span data-stu-id="a7482-241">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="a7482-242">在 Android 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="a7482-242">On Android, HTML formatting looks like this:</span></span>

![Android 客户端中的连接器卡的 HTML 格式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="a7482-244">HTML 连接器卡的格式示例</span><span class="sxs-lookup"><span data-stu-id="a7482-244">Formatting sample for HTML Connector Cards</span></span>

``` json
{
  "contentType": "application/vnd.microsoft.teams.card.o365connector",
  "content": {
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
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
            "text": "embedded image <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img>"
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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[<span data-ttu-id="a7482-245">**HTML 格式：英雄和缩略图卡片**</span><span class="sxs-lookup"><span data-stu-id="a7482-245">**HTML Formatting: hero and thumbnail cards**</span></span>](#tab/simple-html)

<span data-ttu-id="a7482-246">简单卡片（如英雄和缩略图卡片）支持 HTML 标记。</span><span class="sxs-lookup"><span data-stu-id="a7482-246">HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="a7482-247">不支持 Markdown。</span><span class="sxs-lookup"><span data-stu-id="a7482-247">Markdown is not supported.</span></span>

| <span data-ttu-id="a7482-248">Style</span><span class="sxs-lookup"><span data-stu-id="a7482-248">Style</span></span> | <span data-ttu-id="a7482-249">示例</span><span class="sxs-lookup"><span data-stu-id="a7482-249">Example</span></span> | <span data-ttu-id="a7482-250">HTML</span><span class="sxs-lookup"><span data-stu-id="a7482-250">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a7482-251">bold</span><span class="sxs-lookup"><span data-stu-id="a7482-251">bold</span></span> | <span data-ttu-id="a7482-252">**text**</span><span class="sxs-lookup"><span data-stu-id="a7482-252">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="a7482-253">italic</span><span class="sxs-lookup"><span data-stu-id="a7482-253">italic</span></span> | <span data-ttu-id="a7482-254">*text*</span><span class="sxs-lookup"><span data-stu-id="a7482-254">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="a7482-255">标头（级别&ndash;1 3）</span><span class="sxs-lookup"><span data-stu-id="a7482-255">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="a7482-256">**Text**</span><span class="sxs-lookup"><span data-stu-id="a7482-256">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="a7482-257">删除</span><span class="sxs-lookup"><span data-stu-id="a7482-257">strikethrough</span></span> | <span data-ttu-id="a7482-258">~~text~~</span><span class="sxs-lookup"><span data-stu-id="a7482-258">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="a7482-259">无序列表</span><span class="sxs-lookup"><span data-stu-id="a7482-259">unordered list</span></span> | <ul><li><span data-ttu-id="a7482-260">text</span><span class="sxs-lookup"><span data-stu-id="a7482-260">text</span></span></li><li><span data-ttu-id="a7482-261">text</span><span class="sxs-lookup"><span data-stu-id="a7482-261">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="a7482-262">排序列表</span><span class="sxs-lookup"><span data-stu-id="a7482-262">ordered list</span></span> | <ol><li><span data-ttu-id="a7482-263">text</span><span class="sxs-lookup"><span data-stu-id="a7482-263">text</span></span></li><li><span data-ttu-id="a7482-264">text</span><span class="sxs-lookup"><span data-stu-id="a7482-264">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="a7482-265">预设格式文本</span><span class="sxs-lookup"><span data-stu-id="a7482-265">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="a7482-266">blockquote</span><span class="sxs-lookup"><span data-stu-id="a7482-266">blockquote</span></span> | <blockquote><span data-ttu-id="a7482-267">text</span><span class="sxs-lookup"><span data-stu-id="a7482-267">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="a7482-268">超链接</span><span class="sxs-lookup"><span data-stu-id="a7482-268">hyperlink</span></span> | [<span data-ttu-id="a7482-269">必应</span><span class="sxs-lookup"><span data-stu-id="a7482-269">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="a7482-270">图像链接</span><span class="sxs-lookup"><span data-stu-id="a7482-270">image link</span></span> |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="a7482-271">简单卡片的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="a7482-271">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="a7482-272">由于桌面和移动平台之间的分辨率不同，因此桌面和团队的移动版之间的格式不同。</span><span class="sxs-lookup"><span data-stu-id="a7482-272">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="a7482-273">在桌面上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="a7482-273">On the desktop, HTML formatting appears like this:</span></span>

![桌面客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="a7482-275">在 iOS 上，HTML 格式的外观如下所示：</span><span class="sxs-lookup"><span data-stu-id="a7482-275">On iOS, HTML formatting appears like this:</span></span>

![IOS 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="a7482-277">问题：</span><span class="sxs-lookup"><span data-stu-id="a7482-277">Issues:</span></span>

* <span data-ttu-id="a7482-278">在 iOS 上不呈现粗体和斜体等字符格式。</span><span class="sxs-lookup"><span data-stu-id="a7482-278">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="a7482-279">在 Android 上，HTML 格式的外观如下所示：</span><span class="sxs-lookup"><span data-stu-id="a7482-279">On Android, HTML formatting appears like this:</span></span>

![Android 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="a7482-281">Android 上正确显示的字符格式（如粗体和斜体）。</span><span class="sxs-lookup"><span data-stu-id="a7482-281">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="a7482-282">简单卡片中的 HTML 格式的格式示例</span><span class="sxs-lookup"><span data-stu-id="a7482-282">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="a7482-283">这些屏幕截图是使用团队 AppStudio 创建的，其中，将一个英雄卡片的 text 属性设置为以下字符串。</span><span class="sxs-lookup"><span data-stu-id="a7482-283">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="a7482-284">您可以通过修改此代码来测试自己的卡片中的格式设置。</span><span class="sxs-lookup"><span data-stu-id="a7482-284">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
