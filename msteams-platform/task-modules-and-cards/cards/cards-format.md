---
title: 卡片中的文本格式
description: 描述 Microsoft 团队中的卡片文本格式
keywords: 团队 bot 卡片格式
ms.date: 03/29/2018
ms.openlocfilehash: 4a467c5b0b21cc3c19977bf7caa25e6790904b10
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673437"
---
# <a name="card-formatting"></a>卡片格式

您可以使用 markdown 或 HTML 向卡片添加格式文本格式，具体取决于卡片类型。

卡片仅支持 text 属性中的格式设置，而不支持标题或副标题属性中的格式设置。 可以使用 XML （HTML）格式子集或 Markdown （具体取决于卡片类型）指定格式。 对于当前使用 markdown 格式的 amd 未来开发的自适应卡，建议使用该格式。

不同的卡片类型之间的格式支持不同，在桌面和移动团队客户端以及桌面浏览器中的团队之间，卡片的呈现可能略有不同。

## <a name="card-types"></a>卡片类型

有三种类型的卡片支持团队中的 Markdown：

* **自适应卡片**： Markdown 在自适应卡片`Textblock`字段以及`Fact.Title`和`Fact.Value`中受支持。 自适应卡片中不支持 HTML。
* **O365 连接器卡片**：文本字段中的 Office 365 连接器卡片支持 Markdown 和有限的 HTML。
* **简单卡片**：支持有限的 HTML，但在简单卡片中不支持 markdown。

## <a name="markdown-formatting-for-adaptive-cards"></a>自适应卡片的 Markdown 格式

 支持的`Fact.Title`和`Fact.Value`的`Textblock`样式如下：

| Style | 示例 | Markdown |
| --- | --- | --- |
| bold | **Bold** | ```**Bold**``` |
| italic | _Italic_ | ```_Italic_``` |
| 无序列表 | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 排序列表 | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Hyperlinks |[必应](https://www.bing.com/)| ```[Title](url)``` |

以下 markdown 标记不受支持：

* 标头
* 表格
* 图像
* 预设格式文本
* Blockquotes

自适应卡片不支持任何 HTML 格式设置。

### <a name="newlines-for-adaptive-cards"></a>自适应卡片的换行符

在 "列表" `\r`中，可以`\n`对换行符使用或转义序列。 在`\n\n`列表中使用将导致缩进列表中的下一个元素。 如果需要在 textblock 中的其他位置使用换行符`\n\n`，请使用。

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>自适应卡的移动和桌面差异

桌面和团队的移动版之间的格式略有不同。

在桌面上，自适应卡片 markdown 格式在 web 浏览器和团队客户端应用程序中的显示格式如下所示：

![自适应卡片 Markdown 桌面客户端中的格式设置](~/assets/images/cards/Adaptive-markdown-desktop-client.png)

在 iOS 上，自适应卡片 markdown 格式如下所示：

![自适应卡片 Markdown 格式在 iOS 中](~/assets/images/cards/Adaptive-markdown-iOS-75.png)

在 Android 上，自适应卡片 markdown 格式如下所示：

![Android 中的自适应卡片 Markdown 格式](~/assets/images/cards/Adaptive-markdown-Android.png)

### <a name="for-more-information-on-adaptive-cards"></a>有关自适应卡片的详细信息

[自适应卡片中的文本功能](/adaptive-cards/create/textfeatures)团队不支持本主题中提及的日期和本地化功能。

### <a name="formatting-sample-for-adaptive-cards"></a>自适应卡片的格式设置示例

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
## <a name="mention-support-within-adaptive-cards"></a>提及自适应卡片中的支持 

> [!NOTE]
> 在[开发人员预览版](~/resources/dev-preview/developer-preview-intro)中，目前仅支持对卡片中提及支持。

Bot 和邮件扩展现在可以在文本块和 FactSet 元素中包括卡片内容中提及的内容。 

### <a name="constructing-mentions"></a>构建提及
若要在自适应卡片中添加提及的内容，应用需要包含以下元素

* `<at>username</at>`在支持的自适应卡片元素中
* 卡片`mention`内容中`msteams`属性内的对象，其中包括所提及用户的团队用户 id

请注意，目前移动客户端上不支持带有提及的卡片。

### <a name="sample-adaptive-card-with-a-mention"></a>带提及的示例自适应卡片
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

## <a name="html-formatting-for-connector-cards"></a>连接器卡的 HTML 格式

连接器卡支持有限的 markdown 和 HTML 格式设置。 Markdown 将在下一节中介绍。

| Style | 示例 | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| 标头（级别&ndash;1 3） | **Text** | `<h3>Text</h3>` |
| 删除 | ~~text~~ | `<strike>text</strike>` |
| 无序列表 | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 排序列表 | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 预设格式文本 | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| 超链接 | [必应](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 图像链接 | <img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

在连接器卡中，使用`<p>`标记在 HTML 中呈现的换行符。

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>使用 HTML 的连接器卡的移动和桌面差异

在桌面上，连接器卡的 HTML 格式如下所示：

![桌面客户端中的连接器卡的 HTML 格式](~/assets/images/cards/Connector-desktop-html-combined.png)

在 iOS 上，HTML 格式如下所示：

![IOS 客户端中的连接器卡的 HTML 格式](~/assets/images/cards/connector-iphone-html-combined-80.png)

问题：

* 嵌入式图像不是使用 markdown 或 HTML in 连接器卡片呈现在 iOS 上。
* 预设格式的文本将呈现，但不具有灰色背景。

在 Android 上，HTML 格式如下所示：

![Android 客户端中的连接器卡的 HTML 格式](~/assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a>HTML 连接器卡的格式示例

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

## <a name="markdown-formatting-for-connector-cards"></a>连接器卡的 Markdown 格式

连接器卡支持有限的 markdown 和 HTML 格式设置。 上一节中介绍了 HTML。

| Style | 示例 | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| 标头（级别&ndash;1 3） | **Text** | `### Text`|
| 删除 | ~~text~~ | `~~text~~` |
| 无序列表 | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 排序列表 | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| 预设格式文本 | `text` | ``preformatted text`` |
| blockquote | >blockquote 文本 | `>blockquote text` |
| 超链接 | [必应](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| 图像链接 |![在摇滚上的工作](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

在连接器卡中，将为`\n\n`（而不是为`\n`或`\r`）呈现换行符。

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>使用 markdown 的连接器卡的移动和桌面差异

在桌面上，连接器卡的 markdown 格式如下所示：

![桌面客户端中的连接器卡的 HTML 格式](~/assets/images/cards/connector-desktop-markdown-combined.png)

在 iOS 上，连接器卡的 markdown 格式如下所示：

![IOS 客户端中的连接器卡的 HTML 格式](~/assets/images/cards/connector-iphone-markdown-combined-80.png)

问题：

* 团队的 iOS 客户端不会在连接器卡片中呈现 markdown 或 HTML 嵌入式图像。
* Blockquotes 呈现为缩进但不带灰色背景。

在 Android 上，连接器卡的 markdown 格式如下所示：

![Android 客户端中的连接器卡的 HTML 格式](~/assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>Markdown 连接器卡的格式示例

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

## <a name="html-formatting-for-simple-cards"></a>简单卡片的 HTML 格式

这些 HTML 标记对诸如英雄和缩略图卡片等简单卡都受支持。 不支持 Markdown。

| Style | 示例 | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| 标头（级别&ndash;1 3） | **Text** | `<h3>Text</h3>` |
| 删除 | ~~text~~ | `<strike>text</strike>` |
| 无序列表 | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 排序列表 | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 预设格式文本 | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| 超链接 | [必应](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 图像链接 |<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="http://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>简单卡片的移动和桌面差异

由于桌面和移动平台之间的分辨率不同，因此桌面和团队的移动版之间的格式不同。

在桌面上，HTML 格式如下所示：

![桌面客户端中的 HTML 格式](~/assets/images/cards/card-formatting-xml-desktop-v2.png)

在 iOS 上，HTML 格式的外观如下所示：

![IOS 客户端中的 HTML 格式](~/assets/images/cards/card-formatting-xml-mobile-v2.png)

问题：

* 在 iOS 上不呈现粗体和斜体等字符格式。

在 Android 上，HTML 格式的外观如下所示：

![Android 客户端中的 HTML 格式](~/assets/images/cards/card-formatting-xml-android-60.png)

Android 上正确显示的字符格式（如粗体和斜体）。

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>简单卡片中的 HTML 格式的格式示例

这些屏幕截图是使用团队 AppStudio 创建的，其中，将一个英雄卡片的 text 属性设置为以下字符串。 您可以通过修改此代码来测试自己的卡片中的格式设置。

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"http://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`
