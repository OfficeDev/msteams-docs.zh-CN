---
title: 卡片中的文本格式
description: 描述 Microsoft 团队中的卡片文本格式
keywords: 团队 bot 卡片格式
ms.date: 03/29/2018
ms.openlocfilehash: eb8aa13b9e75d08dadd5e615029a9d418c6c7892
ms.sourcegitcommit: 44ac886c0ca34a16222d3991a61606f8483b8481
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/05/2020
ms.locfileid: "41783967"
---
# <a name="card-formatting"></a><span data-ttu-id="521ad-104">卡片格式</span><span class="sxs-lookup"><span data-stu-id="521ad-104">Card formatting</span></span>

<span data-ttu-id="521ad-105">您可以使用 markdown 或 HTML 向卡片添加格式文本格式，具体取决于卡片类型。</span><span class="sxs-lookup"><span data-stu-id="521ad-105">You can add rich text formatting to your cards using either markdown or HTML, depending on the card type.</span></span>

<span data-ttu-id="521ad-106">卡片仅支持 text 属性中的格式设置，而不支持标题或副标题属性中的格式设置。</span><span class="sxs-lookup"><span data-stu-id="521ad-106">Cards support formatting in the text property only, not in the title or subtitle properties.</span></span> <span data-ttu-id="521ad-107">可以使用 XML （HTML）格式子集或 Markdown （具体取决于卡片类型）指定格式。</span><span class="sxs-lookup"><span data-stu-id="521ad-107">Formatting can be specified using a subset of XML (HTML) formatting, or Markdown depending on card type.</span></span> <span data-ttu-id="521ad-108">对于当前使用 markdown 格式的 amd 未来开发的自适应卡，建议使用该格式。</span><span class="sxs-lookup"><span data-stu-id="521ad-108">For current amd future development Adaptive cards using markdown formatting is recommended.</span></span>

<span data-ttu-id="521ad-109">不同的卡片类型之间的格式支持不同，在桌面和移动团队客户端以及桌面浏览器中的团队之间，卡片的呈现可能略有不同。</span><span class="sxs-lookup"><span data-stu-id="521ad-109">Formatting support differs between different card types, and rendering of the card can differ slightly between the desktop and the mobile Teams clients, as well as Teams in the desktop browser.</span></span>

## <a name="card-types"></a><span data-ttu-id="521ad-110">卡片类型</span><span class="sxs-lookup"><span data-stu-id="521ad-110">Card types</span></span>

<span data-ttu-id="521ad-111">有三种类型的卡片支持团队中的 Markdown：</span><span class="sxs-lookup"><span data-stu-id="521ad-111">There are three types of cards that support Markdown in Teams:</span></span>

* <span data-ttu-id="521ad-112">**自适应卡片**： Markdown 在自适应卡片`Textblock`字段以及`Fact.Title`和`Fact.Value`中受支持。</span><span class="sxs-lookup"><span data-stu-id="521ad-112">**Adaptive Cards**: Markdown is supported in Adaptive Card `Textblock` field, as well as `Fact.Title` and `Fact.Value`.</span></span> <span data-ttu-id="521ad-113">自适应卡片中不支持 HTML。</span><span class="sxs-lookup"><span data-stu-id="521ad-113">HTML is not supported in adaptive cards.</span></span>
* <span data-ttu-id="521ad-114">**O365 连接器卡片**：文本字段中的 Office 365 连接器卡片支持 Markdown 和有限的 HTML。</span><span class="sxs-lookup"><span data-stu-id="521ad-114">**O365 Connector Cards**: Markdown and limited HTML is supported in Office 365 Connector cards in the text fields.</span></span>
* <span data-ttu-id="521ad-115">**简单卡片**：支持有限的 HTML，但在简单卡片中不支持 markdown。</span><span class="sxs-lookup"><span data-stu-id="521ad-115">**Simple Cards**: Limited HTML is supported, but markdown is not supported in simple cards.</span></span>

## <a name="markdown-formatting-for-adaptive-cards"></a><span data-ttu-id="521ad-116">自适应卡片的 Markdown 格式</span><span class="sxs-lookup"><span data-stu-id="521ad-116">Markdown formatting for Adaptive Cards</span></span>

 <span data-ttu-id="521ad-117">支持的`Fact.Title`和`Fact.Value`的`Textblock`样式如下：</span><span class="sxs-lookup"><span data-stu-id="521ad-117">The supported styles for `Textblock`, `Fact.Title` and `Fact.Value` are:</span></span>

| <span data-ttu-id="521ad-118">Style</span><span class="sxs-lookup"><span data-stu-id="521ad-118">Style</span></span> | <span data-ttu-id="521ad-119">示例</span><span class="sxs-lookup"><span data-stu-id="521ad-119">Example</span></span> | <span data-ttu-id="521ad-120">Markdown</span><span class="sxs-lookup"><span data-stu-id="521ad-120">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="521ad-121">bold</span><span class="sxs-lookup"><span data-stu-id="521ad-121">bold</span></span> | <span data-ttu-id="521ad-122">**Bold**</span><span class="sxs-lookup"><span data-stu-id="521ad-122">**Bold**</span></span> | ```**Bold**``` |
| <span data-ttu-id="521ad-123">italic</span><span class="sxs-lookup"><span data-stu-id="521ad-123">italic</span></span> | <span data-ttu-id="521ad-124">_Italic_</span><span class="sxs-lookup"><span data-stu-id="521ad-124">_Italic_</span></span> | ```_Italic_``` |
| <span data-ttu-id="521ad-125">无序列表</span><span class="sxs-lookup"><span data-stu-id="521ad-125">unordered list</span></span> | <ul><li><span data-ttu-id="521ad-126">text</span><span class="sxs-lookup"><span data-stu-id="521ad-126">text</span></span></li><li><span data-ttu-id="521ad-127">text</span><span class="sxs-lookup"><span data-stu-id="521ad-127">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="521ad-128">排序列表</span><span class="sxs-lookup"><span data-stu-id="521ad-128">ordered list</span></span> | <ol><li><span data-ttu-id="521ad-129">text</span><span class="sxs-lookup"><span data-stu-id="521ad-129">text</span></span></li><li><span data-ttu-id="521ad-130">text</span><span class="sxs-lookup"><span data-stu-id="521ad-130">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="521ad-131">Hyperlinks</span><span class="sxs-lookup"><span data-stu-id="521ad-131">Hyperlinks</span></span> |[<span data-ttu-id="521ad-132">必应</span><span class="sxs-lookup"><span data-stu-id="521ad-132">Bing</span></span>](https://www.bing.com/)| ```[Title](url)``` |

<span data-ttu-id="521ad-133">以下 markdown 标记不受支持：</span><span class="sxs-lookup"><span data-stu-id="521ad-133">The following markdown tags are not supported:</span></span>

* <span data-ttu-id="521ad-134">标头</span><span class="sxs-lookup"><span data-stu-id="521ad-134">Headers</span></span>
* <span data-ttu-id="521ad-135">表格</span><span class="sxs-lookup"><span data-stu-id="521ad-135">Tables</span></span>
* <span data-ttu-id="521ad-136">图像</span><span class="sxs-lookup"><span data-stu-id="521ad-136">Images</span></span>
* <span data-ttu-id="521ad-137">预设格式文本</span><span class="sxs-lookup"><span data-stu-id="521ad-137">Preformatted text</span></span>
* <span data-ttu-id="521ad-138">Blockquotes</span><span class="sxs-lookup"><span data-stu-id="521ad-138">Blockquotes</span></span>

<span data-ttu-id="521ad-139">自适应卡片不支持任何 HTML 格式设置。</span><span class="sxs-lookup"><span data-stu-id="521ad-139">Adaptive cards do not support any HTML formatting.</span></span>

### <a name="newlines-for-adaptive-cards"></a><span data-ttu-id="521ad-140">自适应卡片的换行符</span><span class="sxs-lookup"><span data-stu-id="521ad-140">Newlines for Adaptive Cards</span></span>

<span data-ttu-id="521ad-141">在 "列表" `\r`中，可以`\n`对换行符使用或转义序列。</span><span class="sxs-lookup"><span data-stu-id="521ad-141">In lists you can use the `\r` or `\n` escape sequences for newlines.</span></span> <span data-ttu-id="521ad-142">在`\n\n`列表中使用将导致缩进列表中的下一个元素。</span><span class="sxs-lookup"><span data-stu-id="521ad-142">Using `\n\n` in a list will cause the next element in the list to be indented.</span></span> <span data-ttu-id="521ad-143">如果需要在 textblock 中的其他位置使用换行符`\n\n`，请使用。</span><span class="sxs-lookup"><span data-stu-id="521ad-143">If you need newlines elsewhere in the textblock, use `\n\n`.</span></span>

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a><span data-ttu-id="521ad-144">自适应卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="521ad-144">Mobile and desktop differences for Adaptive Cards</span></span>

<span data-ttu-id="521ad-145">桌面和团队的移动版之间的格式略有不同。</span><span class="sxs-lookup"><span data-stu-id="521ad-145">Formatting is slightly different between the desktop and the mobile versions of Teams.</span></span>

<span data-ttu-id="521ad-146">在桌面上，自适应卡片 markdown 格式在 web 浏览器和团队客户端应用程序中的显示格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="521ad-146">On the desktop, Adaptive Card markdown formatting appears like this in both web browsers and in the Teams client application:</span></span>

![自适应卡片 Markdown 桌面客户端中的格式设置](~/assets/images/cards/Adaptive-markdown-desktop-client.png)

<span data-ttu-id="521ad-148">在 iOS 上，自适应卡片 markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="521ad-148">On iOS, Adaptive Card markdown formatting appears like this:</span></span>

![自适应卡片 Markdown 格式在 iOS 中](~/assets/images/cards/Adaptive-markdown-iOS-75.png)

<span data-ttu-id="521ad-150">在 Android 上，自适应卡片 markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="521ad-150">On Android, Adaptive Card markdown formatting appears like this:</span></span>

![Android 中的自适应卡片 Markdown 格式](~/assets/images/cards/Adaptive-markdown-Android.png)

### <a name="for-more-information-on-adaptive-cards"></a><span data-ttu-id="521ad-152">有关自适应卡片的详细信息</span><span class="sxs-lookup"><span data-stu-id="521ad-152">For more information on Adaptive Cards</span></span>

<span data-ttu-id="521ad-153">[自适应卡片中的文本功能](/adaptive-cards/create/textfeatures)团队不支持本主题中提及的日期和本地化功能。</span><span class="sxs-lookup"><span data-stu-id="521ad-153">[Text features in Adaptive cards](/adaptive-cards/create/textfeatures) The date and localization features mentioned in this topic are not supported in Teams.</span></span>

### <a name="formatting-sample-for-adaptive-cards"></a><span data-ttu-id="521ad-154">自适应卡片的格式设置示例</span><span class="sxs-lookup"><span data-stu-id="521ad-154">Formatting sample for Adaptive cards</span></span>

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

## <a name="mention-support-within-adaptive-cards"></a><span data-ttu-id="521ad-155">提及自适应卡片中的支持</span><span class="sxs-lookup"><span data-stu-id="521ad-155">Mention support within Adaptive cards</span></span> 

> [!NOTE]
> <span data-ttu-id="521ad-156">在[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中，目前仅支持对卡片中提及支持。</span><span class="sxs-lookup"><span data-stu-id="521ad-156">Mention support in cards is currently supported in [Developer Preview](~/resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="521ad-157">Bot 和邮件扩展现在可以在文本块和 FactSet 元素中包括卡片内容中提及的内容。</span><span class="sxs-lookup"><span data-stu-id="521ad-157">Bots and Messaging extensions can now include mentions within the card content in Text Block and FactSet elements.</span></span> 

### <a name="constructing-mentions"></a><span data-ttu-id="521ad-158">构建提及</span><span class="sxs-lookup"><span data-stu-id="521ad-158">Constructing mentions</span></span>

<span data-ttu-id="521ad-159">若要在自适应卡片中添加提及的内容，应用需要包含以下元素</span><span class="sxs-lookup"><span data-stu-id="521ad-159">To include a mention in an Adaptive Card your app needs to include the following elements</span></span>

* <span data-ttu-id="521ad-160">`<at>username</at>`在支持的自适应卡片元素中</span><span class="sxs-lookup"><span data-stu-id="521ad-160">`<at>username</at>` in the supported adaptive card elements</span></span>
* <span data-ttu-id="521ad-161">卡片`mention`内容中`msteams`属性内的对象，其中包括所提及用户的团队用户 id</span><span class="sxs-lookup"><span data-stu-id="521ad-161">The `mention` object inside of an `msteams` property in the card content, which includes the Teams user id of the user being mentioned</span></span>

<span data-ttu-id="521ad-162">请注意，目前移动客户端上不支持带有提及的卡片。</span><span class="sxs-lookup"><span data-stu-id="521ad-162">Note that cards with mentions aren't supported on mobile clients at the moment.</span></span>

### <a name="sample-adaptive-card-with-a-mention"></a><span data-ttu-id="521ad-163">带提及的示例自适应卡片</span><span class="sxs-lookup"><span data-stu-id="521ad-163">Sample Adaptive card with a mention</span></span>

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

## <a name="html-formatting-for-connector-cards"></a><span data-ttu-id="521ad-164">连接器卡的 HTML 格式</span><span class="sxs-lookup"><span data-stu-id="521ad-164">HTML formatting for Connector Cards</span></span>

<span data-ttu-id="521ad-165">连接器卡支持有限的 markdown 和 HTML 格式设置。</span><span class="sxs-lookup"><span data-stu-id="521ad-165">Connector cards support limited markdown and HTML formatting.</span></span> <span data-ttu-id="521ad-166">Markdown 将在下一节中介绍。</span><span class="sxs-lookup"><span data-stu-id="521ad-166">Markdown is described in the next section.</span></span>

| <span data-ttu-id="521ad-167">Style</span><span class="sxs-lookup"><span data-stu-id="521ad-167">Style</span></span> | <span data-ttu-id="521ad-168">示例</span><span class="sxs-lookup"><span data-stu-id="521ad-168">Example</span></span> | <span data-ttu-id="521ad-169">HTML</span><span class="sxs-lookup"><span data-stu-id="521ad-169">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="521ad-170">bold</span><span class="sxs-lookup"><span data-stu-id="521ad-170">bold</span></span> | <span data-ttu-id="521ad-171">**text**</span><span class="sxs-lookup"><span data-stu-id="521ad-171">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="521ad-172">italic</span><span class="sxs-lookup"><span data-stu-id="521ad-172">italic</span></span> | <span data-ttu-id="521ad-173">*text*</span><span class="sxs-lookup"><span data-stu-id="521ad-173">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="521ad-174">标头（级别&ndash;1 3）</span><span class="sxs-lookup"><span data-stu-id="521ad-174">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="521ad-175">**Text**</span><span class="sxs-lookup"><span data-stu-id="521ad-175">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="521ad-176">删除</span><span class="sxs-lookup"><span data-stu-id="521ad-176">strikethrough</span></span> | <span data-ttu-id="521ad-177">~~text~~</span><span class="sxs-lookup"><span data-stu-id="521ad-177">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="521ad-178">无序列表</span><span class="sxs-lookup"><span data-stu-id="521ad-178">unordered list</span></span> | <ul><li><span data-ttu-id="521ad-179">text</span><span class="sxs-lookup"><span data-stu-id="521ad-179">text</span></span></li><li><span data-ttu-id="521ad-180">text</span><span class="sxs-lookup"><span data-stu-id="521ad-180">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="521ad-181">排序列表</span><span class="sxs-lookup"><span data-stu-id="521ad-181">ordered list</span></span> | <ol><li><span data-ttu-id="521ad-182">text</span><span class="sxs-lookup"><span data-stu-id="521ad-182">text</span></span></li><li><span data-ttu-id="521ad-183">text</span><span class="sxs-lookup"><span data-stu-id="521ad-183">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="521ad-184">预设格式文本</span><span class="sxs-lookup"><span data-stu-id="521ad-184">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="521ad-185">blockquote</span><span class="sxs-lookup"><span data-stu-id="521ad-185">blockquote</span></span> | <blockquote><span data-ttu-id="521ad-186">text</span><span class="sxs-lookup"><span data-stu-id="521ad-186">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="521ad-187">超链接</span><span class="sxs-lookup"><span data-stu-id="521ad-187">hyperlink</span></span> | [<span data-ttu-id="521ad-188">必应</span><span class="sxs-lookup"><span data-stu-id="521ad-188">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="521ad-189">图像链接</span><span class="sxs-lookup"><span data-stu-id="521ad-189">image link</span></span> | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

<span data-ttu-id="521ad-190">在连接器卡中，使用`<p>`标记在 HTML 中呈现的换行符。</span><span class="sxs-lookup"><span data-stu-id="521ad-190">In connector cards, newlines are rendered in HTML using the `<p>` tag.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a><span data-ttu-id="521ad-191">使用 HTML 的连接器卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="521ad-191">Mobile and desktop differences for connector cards using HTML</span></span>

<span data-ttu-id="521ad-192">在桌面上，连接器卡的 HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="521ad-192">On the desktop, HTML formatting for connector cards looks like this:</span></span>

![桌面客户端中的连接器卡的 HTML 格式](~/assets/images/cards/Connector-desktop-html-combined.png)

<span data-ttu-id="521ad-194">在 iOS 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="521ad-194">On iOS, HTML formatting looks like this:</span></span>

![IOS 客户端中的连接器卡的 HTML 格式](~/assets/images/cards/connector-iphone-html-combined-80.png)

<span data-ttu-id="521ad-196">问题：</span><span class="sxs-lookup"><span data-stu-id="521ad-196">Issues:</span></span>

* <span data-ttu-id="521ad-197">嵌入式图像不是使用 markdown 或 HTML in 连接器卡片呈现在 iOS 上。</span><span class="sxs-lookup"><span data-stu-id="521ad-197">Inline images are not rendered on iOS using either markdown or HTML in Connector Cards.</span></span>
* <span data-ttu-id="521ad-198">预设格式的文本将呈现，但不具有灰色背景。</span><span class="sxs-lookup"><span data-stu-id="521ad-198">Preformatted text is rendered but does not have a gray background.</span></span>

<span data-ttu-id="521ad-199">在 Android 上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="521ad-199">On Android, HTML formatting looks like this:</span></span>

![Android 客户端中的连接器卡的 HTML 格式](~/assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a><span data-ttu-id="521ad-201">HTML 连接器卡的格式示例</span><span class="sxs-lookup"><span data-stu-id="521ad-201">Formatting sample for HTML Connector Cards</span></span>

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

## <a name="markdown-formatting-for-connector-cards"></a><span data-ttu-id="521ad-202">连接器卡的 Markdown 格式</span><span class="sxs-lookup"><span data-stu-id="521ad-202">Markdown formatting for Connector Cards</span></span>

<span data-ttu-id="521ad-203">连接器卡支持有限的 markdown 和 HTML 格式设置。</span><span class="sxs-lookup"><span data-stu-id="521ad-203">Connector cards support limited markdown and HTML formatting.</span></span> <span data-ttu-id="521ad-204">上一节中介绍了 HTML。</span><span class="sxs-lookup"><span data-stu-id="521ad-204">HTML is described in the last section.</span></span>

| <span data-ttu-id="521ad-205">Style</span><span class="sxs-lookup"><span data-stu-id="521ad-205">Style</span></span> | <span data-ttu-id="521ad-206">示例</span><span class="sxs-lookup"><span data-stu-id="521ad-206">Example</span></span> | <span data-ttu-id="521ad-207">Markdown</span><span class="sxs-lookup"><span data-stu-id="521ad-207">Markdown</span></span> |
| --- | --- | --- |
| <span data-ttu-id="521ad-208">bold</span><span class="sxs-lookup"><span data-stu-id="521ad-208">bold</span></span> | <span data-ttu-id="521ad-209">**text**</span><span class="sxs-lookup"><span data-stu-id="521ad-209">**text**</span></span> | `**text**` |
| <span data-ttu-id="521ad-210">italic</span><span class="sxs-lookup"><span data-stu-id="521ad-210">italic</span></span> | <span data-ttu-id="521ad-211">*text*</span><span class="sxs-lookup"><span data-stu-id="521ad-211">*text*</span></span> | `*text*` |
| <span data-ttu-id="521ad-212">标头（级别&ndash;1 3）</span><span class="sxs-lookup"><span data-stu-id="521ad-212">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="521ad-213">**Text**</span><span class="sxs-lookup"><span data-stu-id="521ad-213">**Text**</span></span> | `### Text`|
| <span data-ttu-id="521ad-214">删除</span><span class="sxs-lookup"><span data-stu-id="521ad-214">strikethrough</span></span> | <span data-ttu-id="521ad-215">~~text~~</span><span class="sxs-lookup"><span data-stu-id="521ad-215">~~text~~</span></span> | `~~text~~` |
| <span data-ttu-id="521ad-216">无序列表</span><span class="sxs-lookup"><span data-stu-id="521ad-216">unordered list</span></span> | <ul><li><span data-ttu-id="521ad-217">text</span><span class="sxs-lookup"><span data-stu-id="521ad-217">text</span></span></li><li><span data-ttu-id="521ad-218">text</span><span class="sxs-lookup"><span data-stu-id="521ad-218">text</span></span></li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| <span data-ttu-id="521ad-219">排序列表</span><span class="sxs-lookup"><span data-stu-id="521ad-219">ordered list</span></span> | <ol><li><span data-ttu-id="521ad-220">text</span><span class="sxs-lookup"><span data-stu-id="521ad-220">text</span></span></li><li><span data-ttu-id="521ad-221">text</span><span class="sxs-lookup"><span data-stu-id="521ad-221">text</span></span></li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| <span data-ttu-id="521ad-222">预设格式文本</span><span class="sxs-lookup"><span data-stu-id="521ad-222">preformatted text</span></span> | `text` | ``preformatted text`` |
| <span data-ttu-id="521ad-223">blockquote</span><span class="sxs-lookup"><span data-stu-id="521ad-223">blockquote</span></span> | <span data-ttu-id="521ad-224">>blockquote 文本</span><span class="sxs-lookup"><span data-stu-id="521ad-224">>blockquote text</span></span> | `>blockquote text` |
| <span data-ttu-id="521ad-225">超链接</span><span class="sxs-lookup"><span data-stu-id="521ad-225">hyperlink</span></span> | [<span data-ttu-id="521ad-226">必应</span><span class="sxs-lookup"><span data-stu-id="521ad-226">Bing</span></span>](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| <span data-ttu-id="521ad-227">图像链接</span><span class="sxs-lookup"><span data-stu-id="521ad-227">image link</span></span> |![在摇滚上的工作](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

<span data-ttu-id="521ad-229">在连接器卡中，将为`\n\n`（而不是为`\n`或`\r`）呈现换行符。</span><span class="sxs-lookup"><span data-stu-id="521ad-229">In connector cards, newlines are rendered for `\n\n`, but not for `\n` or `\r`.</span></span>

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a><span data-ttu-id="521ad-230">使用 markdown 的连接器卡的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="521ad-230">Mobile and desktop differences for connector cards using markdown</span></span>

<span data-ttu-id="521ad-231">在桌面上，连接器卡的 markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="521ad-231">On the desktop, markdown formatting for connector cards looks like this:</span></span>

![桌面客户端中的连接器卡的 HTML 格式](~/assets/images/cards/connector-desktop-markdown-combined.png)

<span data-ttu-id="521ad-233">在 iOS 上，连接器卡的 markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="521ad-233">On iOS, markdown formatting for connector cards looks like this:</span></span>

![IOS 客户端中的连接器卡的 HTML 格式](~/assets/images/cards/connector-iphone-markdown-combined-80.png)

<span data-ttu-id="521ad-235">问题：</span><span class="sxs-lookup"><span data-stu-id="521ad-235">Issues:</span></span>

* <span data-ttu-id="521ad-236">团队的 iOS 客户端不会在连接器卡片中呈现 markdown 或 HTML 嵌入式图像。</span><span class="sxs-lookup"><span data-stu-id="521ad-236">The iOS client for Teams does not render markdown or HTML inline images in Connector Cards.</span></span>
* <span data-ttu-id="521ad-237">Blockquotes 呈现为缩进但不带灰色背景。</span><span class="sxs-lookup"><span data-stu-id="521ad-237">Blockquotes are rendered as indented but without a gray background.</span></span>

<span data-ttu-id="521ad-238">在 Android 上，连接器卡的 markdown 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="521ad-238">On Android, markdown formatting for connector cards looks like this:</span></span>

![Android 客户端中的连接器卡的 HTML 格式](~/assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a><span data-ttu-id="521ad-240">Markdown 连接器卡的格式示例</span><span class="sxs-lookup"><span data-stu-id="521ad-240">Formatting example for markdown Connector Cards</span></span>

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

## <a name="html-formatting-for-simple-cards"></a><span data-ttu-id="521ad-241">简单卡片的 HTML 格式</span><span class="sxs-lookup"><span data-stu-id="521ad-241">HTML Formatting for simple cards</span></span>

<span data-ttu-id="521ad-242">这些 HTML 标记对诸如英雄和缩略图卡片等简单卡都受支持。</span><span class="sxs-lookup"><span data-stu-id="521ad-242">These HTML tags are supported for simple cards such as the hero and thumbnail card.</span></span> <span data-ttu-id="521ad-243">不支持 Markdown。</span><span class="sxs-lookup"><span data-stu-id="521ad-243">Markdown is not supported.</span></span>

| <span data-ttu-id="521ad-244">Style</span><span class="sxs-lookup"><span data-stu-id="521ad-244">Style</span></span> | <span data-ttu-id="521ad-245">示例</span><span class="sxs-lookup"><span data-stu-id="521ad-245">Example</span></span> | <span data-ttu-id="521ad-246">HTML</span><span class="sxs-lookup"><span data-stu-id="521ad-246">HTML</span></span> |
| --- | --- | --- |
| <span data-ttu-id="521ad-247">bold</span><span class="sxs-lookup"><span data-stu-id="521ad-247">bold</span></span> | <span data-ttu-id="521ad-248">**text**</span><span class="sxs-lookup"><span data-stu-id="521ad-248">**text**</span></span> | `<strong>text</strong>` |
| <span data-ttu-id="521ad-249">italic</span><span class="sxs-lookup"><span data-stu-id="521ad-249">italic</span></span> | <span data-ttu-id="521ad-250">*text*</span><span class="sxs-lookup"><span data-stu-id="521ad-250">*text*</span></span> | `<em>text</em>` |
| <span data-ttu-id="521ad-251">标头（级别&ndash;1 3）</span><span class="sxs-lookup"><span data-stu-id="521ad-251">header (levels 1&ndash;3)</span></span> | <span data-ttu-id="521ad-252">**Text**</span><span class="sxs-lookup"><span data-stu-id="521ad-252">**Text**</span></span> | `<h3>Text</h3>` |
| <span data-ttu-id="521ad-253">删除</span><span class="sxs-lookup"><span data-stu-id="521ad-253">strikethrough</span></span> | <span data-ttu-id="521ad-254">~~text~~</span><span class="sxs-lookup"><span data-stu-id="521ad-254">~~text~~</span></span> | `<strike>text</strike>` |
| <span data-ttu-id="521ad-255">无序列表</span><span class="sxs-lookup"><span data-stu-id="521ad-255">unordered list</span></span> | <ul><li><span data-ttu-id="521ad-256">text</span><span class="sxs-lookup"><span data-stu-id="521ad-256">text</span></span></li><li><span data-ttu-id="521ad-257">text</span><span class="sxs-lookup"><span data-stu-id="521ad-257">text</span></span></li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| <span data-ttu-id="521ad-258">排序列表</span><span class="sxs-lookup"><span data-stu-id="521ad-258">ordered list</span></span> | <ol><li><span data-ttu-id="521ad-259">text</span><span class="sxs-lookup"><span data-stu-id="521ad-259">text</span></span></li><li><span data-ttu-id="521ad-260">text</span><span class="sxs-lookup"><span data-stu-id="521ad-260">text</span></span></li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| <span data-ttu-id="521ad-261">预设格式文本</span><span class="sxs-lookup"><span data-stu-id="521ad-261">preformatted text</span></span> | `text` | `<pre>text</pre>` |
| <span data-ttu-id="521ad-262">blockquote</span><span class="sxs-lookup"><span data-stu-id="521ad-262">blockquote</span></span> | <blockquote><span data-ttu-id="521ad-263">text</span><span class="sxs-lookup"><span data-stu-id="521ad-263">text</span></span></blockquote> | `<blockquote>text</blockquote>` |
| <span data-ttu-id="521ad-264">超链接</span><span class="sxs-lookup"><span data-stu-id="521ad-264">hyperlink</span></span> | [<span data-ttu-id="521ad-265">必应</span><span class="sxs-lookup"><span data-stu-id="521ad-265">Bing</span></span>](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| <span data-ttu-id="521ad-266">图像链接</span><span class="sxs-lookup"><span data-stu-id="521ad-266">image link</span></span> |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a><span data-ttu-id="521ad-267">简单卡片的移动和桌面差异</span><span class="sxs-lookup"><span data-stu-id="521ad-267">Mobile and desktop differences for simple cards</span></span>

<span data-ttu-id="521ad-268">由于桌面和移动平台之间的分辨率不同，因此桌面和团队的移动版之间的格式不同。</span><span class="sxs-lookup"><span data-stu-id="521ad-268">Because of resolution differences between the desktop and mobile platform, formatting is different between the desktop and the mobile version of Teams.</span></span>

<span data-ttu-id="521ad-269">在桌面上，HTML 格式如下所示：</span><span class="sxs-lookup"><span data-stu-id="521ad-269">On the desktop, HTML formatting appears like this:</span></span>

![桌面客户端中的 HTML 格式](~/assets/images/cards/card-formatting-xml-desktop-v2.png)

<span data-ttu-id="521ad-271">在 iOS 上，HTML 格式的外观如下所示：</span><span class="sxs-lookup"><span data-stu-id="521ad-271">On iOS, HTML formatting appears like this:</span></span>

![IOS 客户端中的 HTML 格式](~/assets/images/cards/card-formatting-xml-mobile-v2.png)

<span data-ttu-id="521ad-273">问题：</span><span class="sxs-lookup"><span data-stu-id="521ad-273">Issues:</span></span>

* <span data-ttu-id="521ad-274">在 iOS 上不呈现粗体和斜体等字符格式。</span><span class="sxs-lookup"><span data-stu-id="521ad-274">Character formatting like bold and italic are not rendered on iOS.</span></span>

<span data-ttu-id="521ad-275">在 Android 上，HTML 格式的外观如下所示：</span><span class="sxs-lookup"><span data-stu-id="521ad-275">On Android, HTML formatting appears like this:</span></span>

![Android 客户端中的 HTML 格式](~/assets/images/cards/card-formatting-xml-android-60.png)

<span data-ttu-id="521ad-277">Android 上正确显示的字符格式（如粗体和斜体）。</span><span class="sxs-lookup"><span data-stu-id="521ad-277">Character formatting like bold and italic display correctly on Android.</span></span>

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a><span data-ttu-id="521ad-278">简单卡片中的 HTML 格式的格式示例</span><span class="sxs-lookup"><span data-stu-id="521ad-278">Formatting sample for HTML formatting in simple cards</span></span>

<span data-ttu-id="521ad-279">这些屏幕截图是使用团队 AppStudio 创建的，其中，将一个英雄卡片的 text 属性设置为以下字符串。</span><span class="sxs-lookup"><span data-stu-id="521ad-279">These screenshots were created using Teams AppStudio, where the text property of a hero card was set to the following string.</span></span> <span data-ttu-id="521ad-280">您可以通过修改此代码来测试自己的卡片中的格式设置。</span><span class="sxs-lookup"><span data-stu-id="521ad-280">You can test formatting in your own cards by modifying this code.</span></span>

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`
