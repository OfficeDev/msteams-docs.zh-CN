---
title: 卡片中的文本格式
description: 介绍 Microsoft Teams 中的卡片文本格式
keywords: teams 自动程序卡格式
ms.date: 03/29/2018
ms.openlocfilehash: d7016f8b954e885221c55bd6c29309fd90a1dcfc
ms.sourcegitcommit: d41da0b608327829b902aded6bc85c0d0016d068
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/31/2021
ms.locfileid: "51474997"
---
# <a name="format-cards-in-teams"></a>在 Teams 中设置卡片格式

可以使用 Markdown 或 HTML 将格式文本格式添加到卡片，具体取决于卡片类型。

卡片仅支持文本属性中的格式设置，不支持标题或副标题属性中的格式设置。 可以使用 XML 格式的子集或 HTML (格式) Markdown 来指定格式，具体取决于卡片类型。 对于当前和未来开发，建议使用 Markdown 格式的自适应卡片。

不同卡类型之间的格式支持不同，并且桌面版和移动版 Teams 客户端以及桌面浏览器中的 Teams 的卡片呈现可能略有不同。

你可以将内联图像与任意 Teams 卡一起包含。 格式设置为 、 或 文件的图像不能超过  `.png` `.jpg` `.gif` 1024 像素× 1024 像素或 1 MB。 动态 GIF 不受正式支持。 *请参阅*[卡片参考](./cards-reference.md#inline-card-images)

## <a name="formatting-cards-with-markdown"></a>使用 Markdown 格式化卡片

Teams 中支持 Markdown 的卡片类型有两种：

> [!div class="checklist"]
> * **自适应卡片**： Markdown 在自适应卡片字段中以及 和 `Textblock` `Fact.Title` 中受支持 `Fact.Value` 。 自适应卡片不支持 HTML。
> * **O365 连接器卡**：文本字段中的 Office 365 连接器卡支持 Markdown 和有限的 HTML。

# <a name="markdown-formatting-adaptive-cards"></a>[**Markdown 格式：自适应卡片**](#tab/adaptive-md)

 和 `Textblock` 支持的 `Fact.Title` `Fact.Value` 样式包括：

| 样式 | 示例 | Markdown |
| --- | --- | --- |
| bold | **Bold** | ```**Bold**``` |
| italic | _Italic_ | ```_Italic_``` |
| 无序列表 | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 排序列表 | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Hyperlinks |[必应](https://www.bing.com/)| ```[Title](url)``` |

不支持以下 Markdown 标记：

* 标头
* 表格
* 图像
* 预设格式的文本
* Blockquotes

> [!IMPORTANT]
> 自适应卡片不支持 HTML 格式。

### <a name="newlines-for-adaptive-cards"></a>自适应卡片的 Newlines

在列表中，可以将 `\r` 或 `\n` 转义序列用于新行。 在 `\n\n` 列表中使用 将导致列表中的下一个元素缩进。 如果你需要在 textblock 中的其他地方使用 newlines，请使用 `\n\n` 。

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>自适应卡片的移动和桌面差异

桌面版和移动版 Teams 的格式略有不同。

在桌面上，自适应卡片 Markdown 格式在 Web 浏览器和 Teams 客户端应用程序中如下所示：

![桌面客户端中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

在 iOS 上，自适应卡片 Markdown 格式如下所示：

![iOS 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

在 Android 上，自适应卡片 Markdown 格式如下所示：

![Android 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-Android.png)

### <a name="more-information-on-adaptive-cards"></a>自适应卡片详细信息

[自适应卡片中的文本功能](/adaptive-cards/create/textfeatures) 本主题中提到的日期和本地化功能在 Teams 中不受支持。

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

### <a name="mention-support-within-adaptive-cards-v12"></a>自适应卡片 v1.2 中的提及支持

Web、桌面和移动客户端支持基于卡片的提及。 你可以为机器人和消息传递扩展响应在自适应卡片正文中添加 @ 提及。  若要在卡片中添加 @ 提及，请遵循与频道和群聊对话中基于消息的提及相同的通知 [逻辑和呈现](../../bots/how-to/conversations/channel-and-group-conversations.md#working-with-mentions )。

聊天机器人和消息传递扩展可以在 [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 和 [FactSet](https://adaptivecards.io/explorer/FactSet.html) 元素的卡片内容中包括提及。

> [!NOTE]
> * [Teams 平台上](https://adaptivecards.io/explorer/Media.html) 的自适应卡片 v1.2 当前不支持媒体元素。
> * 频道&团队提及在机器人消息中不受支持。

#### <a name="constructing-mentions"></a>构造提及

若要在自适应卡片中包括提及，应用需要包括以下元素

* `<at>username</at>` 在支持的自适应卡片元素中
* `mention`卡片内容中属性内的对象，其中包括被提及用户的 `msteams` Teams 用户 ID

#### <a name="sample-adaptive-card-with-a-mention"></a>带提及功能的示例自适应卡片

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


### <a name="information-masking-in-adaptive-cards"></a>自适应卡片中的信息屏蔽
使用信息屏蔽属性可以屏蔽特定信息，如自适应卡片输入元素内用户的密码或 [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) 敏感信息。 

> [!NOTE]
> 该功能仅支持客户端信息屏蔽，将屏蔽的输入文本作为纯文本发送到在机器人配置期间指定的 https [终结点地址](../../build-your-first-app/build-bot.md#4-configure-your-bot)。 

> [!NOTE]
> 信息屏蔽属性当前仅在开发人员预览版中可用。

若要屏蔽自适应卡片中的信息，请添加 `isMasked` 属性以 **键入** `Input.Text` ，将其值设置为 *true*。

#### <a name="sample-adaptive-card-with-masking-property"></a>具有屏蔽属性的示例自适应卡片

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
    "isMasked": true
  },
```

下图是自适应卡片中屏蔽信息的示例：

![屏蔽信息图像](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>全宽自适应卡片
可以使用 属性扩展自适应卡片的宽度， `msteams` 并占用额外的画布空间。 有关如何使用 属性的信息，请参阅以下示例：

#### <a name="constructing-full-width-cards"></a>构造全宽卡片
若要制作全宽自适应卡片，必须将卡片内容 `width` `msteams` 中的 属性中的 对象设置为 `Full` 。
此外，你的应用必须包含以下元素：

#### <a name="sample-adaptive-card-with-full-width"></a>全宽自适应卡片示例

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

完整宽度自适应卡片如下所示： ![ 全宽自适应卡片视图](../../assets/images/cards/full-width-adaptive-card.png)

如果尚未将属性设置为 `width` *Full，* 则自适应卡片的默认视图如下所示： ![ 小宽度自适应卡片视图](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>Typeahead 支持

在架构元素中，要求用户通过大量选择进行筛选可能会显著降低 [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) 任务完成速度。 自适应卡片中的 Typeahead 支持可以在用户键入输入时缩小或筛选输入选项集，从而简化输入选择。 

#### <a name="enable-typeahead-in-adaptive-cards"></a>在自适应卡片中启用 typeahead

若要在 设置为 内启用 `Input.Choiceset` `style` typeahead， `filtered` 并确保 `isMultiSelect` 设置为 `false` 。 

#### <a name="sample-adaptive-card-with-typeahead-support"></a>具有 typeahead 支持的示例自适应卡片

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

### <a name="stage-view-for-images-in-adaptive-cards"></a>自适应卡片中的图像阶段视图

> [!NOTE]
> 此功能目前仅在开发人员预览版中可用。
 
在自适应卡片中，可以使用 属性添加选择性地在阶段 `msteams` 视图中显示图像的能力。 当用户将鼠标悬停在图像上时，他们将看到展开图标，其 `allowExpand` 属性设置为 `true` 。 有关如何使用 属性的信息，请参阅以下示例：

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

当用户将鼠标悬停在图像上方时，图像右上角将显示展开图标：带可展开图像的自适应 ![ 卡片](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

当用户选择展开按钮时，图像显示在阶段视图中：展开 ![ 到阶段视图的图像](../../assets/images/cards/adaptivecard-expand-image.png)

在阶段视图中，用户可以放大和缩小图像。 可以选择自适应卡片中的哪些图像需要具备此功能。

> [!NOTE]
> 放大和缩小功能仅适用于自适应卡片 (图像) 图像元素。

> [!NOTE]
> 对于 Teams 移动应用，自适应卡片中的图像阶段视图功能默认可用，用户只需点击图像即可在阶段视图中查看自适应卡片图像，而不管属性是否 `allowExpand` 存在。

# <a name="markdown-formatting-o365-connector-cards"></a>[**Markdown 格式：O365 连接器卡**](#tab/connector-md)

连接器卡支持有限的 Markdown 和 HTML 格式。 HTML 支持在上一节中介绍。

| 样式 | 示例 | Markdown |
| --- | --- | --- |
| bold | **text** | `**text**` |
| italic | *text* | `*text*` |
| 页眉 (级别 1 &ndash; 3)  | **Text** | `### Text`|
| strikethrough | ~~text~~ | `~~text~~` |
| 无序列表 | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 排序列表 | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| 预设格式的文本 | `text` | ``preformatted text`` |
| blockquote | >blockquote 文本 | `>blockquote text` |
| 超链接 | [必应](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| 图像链接 |![在一个地心上闪避](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

在连接器卡中，为 呈现新行 `\n\n` ，但不为 或 `\n` 呈现 `\r` 。

### <a name="mobile-and-desktop-differences-for-connector-cards-using-markdown"></a>使用 Markdown 的连接器卡的移动和桌面差异

在桌面上，连接器卡的 Markdown 格式如下所示：

![桌面客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-desktop-markdown-combined.png)

在 iOS 上，连接器卡的 Markdown 格式如下所示：

![iOS 客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

问题：

* 适用于 Teams 的 iOS 客户端不会在连接器卡中呈现 Markdown 或 HTML 内嵌图像。
* Blockquotes 呈现为缩进，但不带灰色背景。

在 Android 上，连接器卡的 Markdown 格式如下所示：

![Android 客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="formatting-example-for-markdown-connector-cards"></a>Markdown 连接器卡的格式设置示例

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

## <a name="formatting-cards-with-html"></a>使用 HTML 设置卡片格式

# <a name="html-formatting-o365-connector-cards"></a>[**HTML 格式：O365 连接器卡**](#tab/connector-html)

连接器卡支持有限的 Markdown 和 HTML 格式。 Markdown 将下一节介绍。

| 样式 | 示例 | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| 页眉 (级别 1 &ndash; 3)  | **Text** | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `<strike>text</strike>` |
| 无序列表 | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 排序列表 | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 预设格式的文本 | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| 超链接 | [必应](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 图像链接 | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

在连接器卡中，使用 标记以 HTML 格式呈现 `<p>` 新行。

### <a name="mobile-and-desktop-differences-for-connector-cards-using-html"></a>使用 HTML 的连接器卡的移动和桌面差异

在桌面上，连接器卡的 HTML 格式如下所示：

![桌面客户端中连接器卡的 HTML 格式](../../assets/images/cards/Connector-desktop-html-combined.png)

在 iOS 上，HTML 格式如下所示：

![iOS 客户端中连接器卡的 HTML 格式](../../assets/images/cards/connector-iphone-html-combined-80.png)

问题：

* 内联图像不会使用连接器卡中的 Markdown 或 HTML 呈现在 iOS 上。
* 呈现预设格式的文本，但没有灰色背景。

在 Android 上，HTML 格式如下所示：

![Android 客户端中连接器卡的 HTML 格式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="formatting-sample-for-html-connector-cards"></a>HTML 连接器卡的格式设置示例

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

# <a name="html-formatting-hero-and-thumbnail-cards"></a>[**HTML 格式：hero 和 thumbnail 卡片**](#tab/simple-html)

HTML 标记支持简单的卡片，如 hero 和 thumbnail 卡片。 不支持 Markdown。

| 样式 | 示例 | HTML |
| --- | --- | --- |
| bold | **text** | `<strong>text</strong>` |
| italic | *text* | `<em>text</em>` |
| 页眉 (级别 1 &ndash; 3)  | **Text** | `<h3>Text</h3>` |
| strikethrough | ~~text~~ | `<strike>text</strike>` |
| 无序列表 | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 排序列表 | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 预设格式的文本 | `text` | `<pre>text</pre>` |
| blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| 超链接 | [必应](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 图像链接 |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>简单卡片的移动和桌面差异

由于桌面平台和移动平台的分辨率差异，桌面版和移动版 Teams 的格式不同。

在桌面上，HTML 格式如下所示：

![桌面客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

在 iOS 上，HTML 格式如下所示：

![iOS 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

问题：

* 粗体和 italic 等字符格式不会呈现在 iOS 上。

在 Android 上，HTML 格式如下所示：

![Android 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-android-60.png)

在 Android 上正确显示粗体和 italic 等字符格式。

### <a name="formatting-sample-for-html-formatting-in-simple-cards"></a>简单卡片中 HTML 格式的格式设置示例

这些屏幕截图是使用 Teams AppStudio 创建的，其中 Hero 卡片的文本属性设置为以下字符串。 可以通过修改此代码在你自己的卡片中测试格式。

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

---
