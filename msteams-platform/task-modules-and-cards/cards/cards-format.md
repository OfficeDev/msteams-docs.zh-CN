---
title: 卡片中的文本格式
description: 描述 Microsoft 团队中的卡片文本格式
keywords: 团队 bot 卡片格式
ms.date: 03/29/2018
ms.openlocfilehash: fcf0692fe033cd3c30ea1e3ac7bda8ddd06297ca
ms.sourcegitcommit: 64acd30eee8af5fe151e9866c13226ed3f337c72
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/18/2020
ms.locfileid: "49346705"
---
# <a name="format-cards-in-teams"></a>设置团队中卡片的格式

您可以使用 Markdown 或 HTML 向卡片添加格式文本格式，具体取决于卡片类型。

卡片仅支持 text 属性中的格式设置，而不支持标题或副标题属性中的格式设置。 可以使用 XML (HTML) 格式或 Markdown 的子集指定格式，具体取决于卡片类型。 对于当前和将来使用 Markdown 格式的开发自适应卡片，建议使用格式设置。

不同的卡片类型之间的格式支持不同，在桌面和移动团队客户端以及桌面浏览器中的团队之间，卡片的呈现可能略有不同。

可以在任何团队卡片中添加内嵌图像。 图像的格式为  `.png` 、 `.jpg` 或文件， `.gif` 不得超过1024× 1024 PX 或 1 MB。 不正式支持动画 GIF。 *请参阅*[卡片参考](./cards-reference.md#inline-card-images)

## <a name="formatting-cards-with-markdown"></a>使用 Markdown 设置卡片格式

有两种卡类型支持团队中的 Markdown：

> [!div class="checklist"]
> * **自适应卡片**： Markdown 在自适应卡片 `Textblock` 字段以及和中受 `Fact.Title` 支持 `Fact.Value` 。 自适应卡片中不支持 HTML。
> * **O365 连接器卡片**：文本字段中的 Office 365 连接器卡片支持 Markdown 和有限的 HTML。

# <a name="markdown-formatting-adaptive-cards"></a>[**Markdown 格式：自适应卡片**](#tab/adaptive-md)

 支持的和的 `Textblock` 样式 `Fact.Title` `Fact.Value` 如下：

| 样式 | 示例 | Markdown |
| --- | --- | --- |
| bold | **Bold** | ```**Bold**``` |
| italic | _Italic_ | ```_Italic_``` |
| 无序列表 | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 排序列表 | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Hyperlinks |[必应](https://www.bing.com/)| ```[Title](url)``` |

以下 Markdown 标记不受支持：

* 标头
* 表格
* 图像
* 预设格式文本
* Blockquotes

> [!IMPORTANT]
> 自适应卡片不支持 HTML 格式。

### <a name="newlines-for-adaptive-cards"></a>自适应卡片的换行符

在 "列表" 中，可以对 `\r` 换行符使用或 `\n` 转义序列。 `\n\n`在列表中使用将导致缩进列表中的下一个元素。 如果需要在 textblock 中的其他位置使用换行符，请使用 `\n\n` 。

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>自适应卡的移动和桌面差异

桌面和团队的移动版之间的格式略有不同。

在桌面上，自适应卡片 Markdown 格式在 web 浏览器和团队客户端应用程序中的显示格式如下所示：

![自适应卡片 Markdown 桌面客户端中的格式设置](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

在 iOS 上，自适应卡片 Markdown 格式如下所示：

![自适应卡片 Markdown 格式在 iOS 中](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

在 Android 上，自适应卡片 Markdown 格式如下所示：

![Android 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a>有关自适应卡片的详细信息

[自适应卡片中的文本功能](/adaptive-cards/create/textfeatures) 团队不支持本主题中提及的日期和本地化功能。

### <a name="formatting-sample-for-adaptive-cards"></a>自适应卡片的格式设置示例

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

### <a name="mention-support-within-adaptive-cards-v12"></a>提及自适应卡片中的支持 1.2 1。2

基于卡片的提及在 Web、桌面和移动客户端中受支持。 您可以在自适应卡片正文中添加用于 bot 和邮件扩展响应的 @ 提及。  若要在卡片中添加 @ 提及，请在 [通道和组聊天对话中](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions )遵循与基于邮件的提及相同的通知逻辑和呈现。

Bot 和邮件扩展可以在 [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 和 [FactSet](https://adaptivecards.io/explorer/FactSet.html) 元素的卡片内容中包括提及。

> [!NOTE]
> * 目前，工作组平台上的自适应卡版1.2 中不支持[媒体元素](https://adaptivecards.io/explorer/Media.html)。
> * 在 bot 消息中不支持频道 & 的团队提及。

### <a name="constructing-mentions"></a>构建提及

若要在自适应卡片中添加提及的内容，应用需要包含以下元素

* `<at>username</at>` 在支持的自适应卡片元素中
* `mention` `msteams` 卡片内容中属性内的对象，其中包括所提及用户的团队用户 id

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

# <a name="markdown-formatting-o365-connector-cards"></a>[**Markdown 格式： O365 连接器卡**](#tab/connector-md)

连接器卡支持有限的 Markdown 和 HTML 格式设置。 上一节中介绍了 HTML 支持。

| 样式 | 示例 | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| 标头 (级别 1 &ndash; 3)  | **Text** | `### Text`|
| 删除 | ~~text~~ | `~~text~~` |
| 无序列表 | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 排序列表 | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| 预设格式文本 | `text` | ``preformatted text`` |
| blockquote | >blockquote 文本 | `>blockquote text` |
| 超链接 | [必应](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| 图像链接 |![在摇滚上的工作](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

在连接器卡中，将为 `\n\n` （而不是为或）呈现换行符 `\n` `\r` 。

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>使用 Markdown 的连接器卡的移动和桌面差异

在桌面上，连接器卡的 Markdown 格式如下所示：

![桌面客户端中的连接器卡的 Markdown 格式](../../assets/images/cards/connector-desktop-markdown-combined.png)

在 iOS 上，连接器卡的 Markdown 格式如下所示：

![IOS 客户端中的连接器卡的 Markdown 格式](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

问题：

* 团队的 iOS 客户端不会在连接器卡片中呈现 Markdown 或 HTML 嵌入式图像。
* Blockquotes 呈现为缩进但不带灰色背景。

在 Android 上，连接器卡的 Markdown 格式如下所示：

![Android 客户端中的连接器卡的 Markdown 格式](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>Markdown 连接器卡的格式示例

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

## <a name="formatting-cards-with-html"></a>使用 HTML 格式化卡片

# <a name="html-formatting-o365-connector-cards"></a>[**HTML 格式： O365 连接器卡**](#tab/connector-html)

连接器卡支持有限的 Markdown 和 HTML 格式设置。 Markdown 将在下一节中介绍。

| 样式 | 示例 | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| 标头 (级别 1 &ndash; 3)  | **Text** | `<h3>Text</h3>` |
| 删除 | ~~text~~ | `<strike>text</strike>` |
| 无序列表 | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 排序列表 | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 预设格式文本 | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| 超链接 | [必应](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 图像链接 | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

在连接器卡中，使用标记在 HTML 中呈现的换行符 `<p>` 。

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>使用 HTML 的连接器卡的移动和桌面差异

在桌面上，连接器卡的 HTML 格式如下所示：

![桌面客户端中的连接器卡的 HTML 格式](../../assets/images/cards/Connector-desktop-html-combined.png)

在 iOS 上，HTML 格式如下所示：

![IOS 客户端中的连接器卡的 HTML 格式](../../assets/images/cards/connector-iphone-html-combined-80.png)

问题：

* 嵌入式图像不是使用 Markdown 或 HTML in 连接器卡片呈现在 iOS 上。
* 预设格式的文本将呈现，但不具有灰色背景。

在 Android 上，HTML 格式如下所示：

![Android 客户端中的连接器卡的 HTML 格式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a>HTML 连接器卡的格式示例

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[**HTML 格式：英雄和缩略图卡片**](#tab/simple-html)

简单卡片（如英雄和缩略图卡片）支持 HTML 标记。 不支持 Markdown。

| 样式 | 示例 | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| 标头 (级别 1 &ndash; 3)  | **Text** | `<h3>Text</h3>` |
| 删除 | ~~text~~ | `<strike>text</strike>` |
| 无序列表 | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 排序列表 | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 预设格式文本 | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| 超链接 | [必应](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 图像链接 |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>简单卡片的移动和桌面差异

由于桌面和移动平台之间的分辨率不同，因此桌面和团队的移动版之间的格式不同。

在桌面上，HTML 格式如下所示：

![桌面客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

在 iOS 上，HTML 格式的外观如下所示：

![IOS 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

问题：

* 在 iOS 上不呈现粗体和斜体等字符格式。

在 Android 上，HTML 格式的外观如下所示：

![Android 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-android-60.png)

Android 上正确显示的字符格式（如粗体和斜体）。

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>简单卡片中的 HTML 格式的格式示例

这些屏幕截图是使用团队 AppStudio 创建的，其中，将一个英雄卡片的 text 属性设置为以下字符串。 您可以通过修改此代码来测试自己的卡片中的格式设置。

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
