---
title: 卡片中的文本格式
description: 介绍卡片文本格式Microsoft Teams
keywords: teams 自动程序卡格式
ms.localizationpriority: medium
ms.topic: reference
ms.date: 06/25/2021
ms.openlocfilehash: 409ba9c0d96712ff3f5cfc40b64b406ce57818b8
ms.sourcegitcommit: 85d0584877db21e2d3e49d3ee940d22675617582
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/29/2021
ms.locfileid: "61216228"
---
# <a name="format-cards-in-microsoft-teams"></a>Microsoft Teams 中的格式卡

以下是向卡片添加格式文本格式的两种方法：
* [Markdown](#format-cards-with-markdown)
* [HTML](#format-cards-with-html)

卡片仅支持文本属性中的格式设置，不支持标题或副标题属性中的格式设置。 可以使用 XML 或 HTML 格式的子集或 Markdown 指定格式，具体取决于卡片类型。 对于自适应卡片的当前和未来开发，建议使用 Markdown 格式。

卡片类型之间的格式支持不同。 桌面版和移动版客户端之间以及桌面浏览器中Microsoft Teams卡Teams可能会略有不同。

你可以将内联图像与任意卡片Teams内。 图像的格式可以设置为 、 或 文件，并且不能超过 `.png` `.jpg` `.gif` 1024 像素× 1024 像素或 1 MB。 不支持动态 GIF。 有关详细信息，请参阅 [卡片类型](./cards-reference.md#inline-card-images)。

可以使用 Markdown 设置自适应卡片和Office 365连接器卡的格式，其中包括某些受支持的样式。

## <a name="format-cards-with-markdown"></a>使用 Markdown 格式化卡片

以下卡片类型支持 Markdown 格式Teams：

* 自适应卡片：自适应卡片字段以及 和 中都支持 `Textblock` `Fact.Title` `Fact.Value` Markdown。 自适应卡片不支持 HTML。
* Office 365连接器卡：文本字段中的 Office 365 连接器卡中支持 Markdown 和有限的 HTML。

你可以将新行用于自适应卡片，或者对列表中新行使用转 `\r` `\n` 义序列。 适用于自适应卡片的桌面版和移动版Teams不同。 Web、桌面和移动客户端支持基于卡片的提及。 可以使用信息屏蔽属性来屏蔽特定信息，如自适应卡片输入元素内用户的密码或 `Input.Text` 敏感信息。 可以使用 对象扩展自适应卡片 `width` 的宽度。 可以在自适应卡片中启用 typeahead 支持，在用户键入输入时筛选输入选项集。 可以使用 属性 `msteams` 添加选择性地在阶段视图中显示图像的能力。

对于自适应卡片和连接器卡，桌面版和移动版Teams不同。 在此部分中，你可以浏览自适应卡片和连接器卡的 Markdown 格式示例。

# <a name="markdown-format-for-adaptive-cards"></a>[自适应卡片的 Markdown 格式](#tab/adaptive-md)

 下表提供了 、 和 `Textblock` 支持的 `Fact.Title` 样式 `Fact.Value` ：

| 样式 | 示例 | Markdown |
| --- | --- | --- |
| 粗体 | **Bold** | ```**Bold**``` |
| 斜体 | _Italic_ | ```_Italic_``` |
| 未排序列表 | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 已排序列表 | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Hyperlinks |[必应](https://www.bing.com/)| ```[Title](url)``` |

不支持以下 Markdown 标记：

* 标题
* 表格
* 图像
* 预设格式的文本
* Blockquotes

### <a name="newlines-for-adaptive-cards"></a>自适应卡片的新行

可以将 或 `\r` `\n` 转义序列用于列表中新行。 在 `\n\n` 列表中使用 会导致列表中的下一个元素缩进。 如果需要 TextBlock 中其他位置的 newlines，请使用 `\n\n` 。

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>自适应卡片的移动和桌面差异

在桌面上，自适应卡片 Markdown 格式显示如下图所示，在 Web 浏览器和 Teams 应用程序中：

![桌面客户端中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

在 iOS 上，自适应卡片 Markdown 格式显示如下图所示：

![iOS 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

在 Android 上，自适应卡片 Markdown 格式显示如下图所示：

![Android 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-Android.png)

有关详细信息，请参阅自适应 [卡片中的文本功能](/adaptive-cards/create/textfeatures)。

> [!NOTE]
> 本节中提到的日期和本地化功能在 Teams。

### <a name="adaptive-cards-format-sample"></a>自适应卡片格式示例

以下代码显示了自适应卡片格式设置的示例：

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

### <a name="mention-support-within-adaptive-cards"></a>自适应卡片中的提及支持 

可以在自动@mentions消息扩展响应的自适应卡片正文中添加邮件。 若要在@mentions，请遵循与频道和群聊对话中基于消息的提及相同的通知逻辑和 [呈现](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions)。

聊天机器人和消息传递扩展可以在 [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 和 [FactSet](https://adaptivecards.io/explorer/FactSet.html) 元素的卡片内容中包括提及。

> [!NOTE]
> * [媒体元素](https://adaptivecards.io/explorer/Media.html)当前在应用程序平台上的自适应卡片Teams支持。
> * 机器人消息不支持频道和团队提及。

若要在自适应卡片中包括提及，你的应用需要包括以下元素：

* `<at>username</at>` 在支持的自适应卡片元素中。
* `mention`卡片内容 `msteams` 中属性内的对象包括Teams的用户 ID。
* `userId`是自动程序 ID 和特定用户所特有的。 它可用于@mention用户。 `userId`可以使用获取用户 ID 中提到的选项之[一来检索](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id)。

#### <a name="sample-adaptive-card-with-a-mention"></a>带提及功能的示例自适应卡片

以下代码显示了带提及功能自适应卡片的示例：

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

### <a name="aad-object-id-and-upn-in-user-mention"></a>AAD用户提及中的对象 ID 和 UPN 

Teams平台除了现有提及 ID 外，还允许使用 AAD 对象 ID 和用户原则名称 (UPN) 提及用户。 具有自适应卡片的机器人和具有传入 Webhook 的连接器支持两个用户提及的 ID。 

下表介绍了新支持的用户提及 ID：

|ID  | 支持功能 |   说明 | 示例 |
|----------|--------|---------------|---------|
| AAD对象 ID | 机器人，连接器 |  AAD用户的对象 ID |  49c4641c-ab91-4248-aebb-6a7de286397b |
| UPN | 机器人，连接器 | AAD用户的 UPN | john.smith@microsoft.com |

#### <a name="user-mention-in-bots-with-adaptive-cards"></a>使用自适应卡片的机器人中的用户提及 

除现有 ID 外，机器人还支持AAD对象 ID 和 UPN 的用户提及。 在短信、自适应卡片正文和消息传递扩展响应的机器人中提供对两个新 ID 的支持。 机器人支持会话和方案中的提及 `invoke` 设备。 当用户与 ID 一起@mentioned活动源通知。 

> [!NOTE]
> 对于自动程序中的自适应卡片，用户无需提及架构更新和 UI/UX 更改。

##### <a name="example"></a>示例 

使用自适应卡片的机器人中的用户提及示例，如下所示：

```json 
{
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.0",
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Hi <at>Adele UPN</at>, <at>Adele AAD</at>"
    }
  ],
  "msteams": {
    "entities": [
      {
        "type": "mention",
        "text": "<at>Adele UPN</at>",
        "mentioned": {
          "id": "AdeleV@contoso.onmicrosoft.com",
          "name": "Adele Vance"
        }
      },
      {
        "type": "mention",
        "text": "<at>Adele AAD</at>",
        "mentioned": {
          "id": "87d349ed-44d7-43e1-9a83-5f2406dee5bd",
          "name": "Adele Vance"
        }
      }
    ]
  }
}
```

下图展示了用户在 Bot 中通过自适应卡片提及的功能：

![使用自适应卡片在机器人中提及的用户](~/assets/images/authentication/user-mention-in-bot.png)

#### <a name="user-mention-in-incoming-webhook-with-adaptive-cards"></a>使用自适应卡片传入 Webhook 中的用户提及 

传入 Webhook 开始支持自适应卡片中的用户提及，AAD对象 ID 和 UPN。

> [!NOTE]    
> * 在架构中为传入 Webhook 启用用户提及功能，以支持AAD ID 和 UPN。 
> * 对于使用对象 ID 和 UPN 的用户提及，AAD UI/UX 更改。      
> * 传入 Webhook 的活动源通知以及用户提及的通知将在将来的版本中提供。

##### <a name="example"></a>示例 

传入 Webhook 中的用户提及示例，如下所示：

```json
{
    "type": "message",
    "attachments": [
        {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
            "type": "AdaptiveCard",
            "body": [
                {
                    "type": "TextBlock",
                    "size": "Medium",
                    "weight": "Bolder",
                    "text": "Sample Adaptive Card with User Mention"
                },
                {
                    "type": "TextBlock",
                    "text": "Hi <at>Adele UPN</at>, <at>Adele AAD</at>"
                }
            ],
            "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
            "version": "1.0",
            "msteams": {
                "entities": [
                    {
                        "type": "mention",
                        "text": "<at>Adele UPN</at>",
                        "mentioned": {
                          "id": "AdeleV@contoso.onmicrosoft.com",
                          "name": "Adele Vance"
                        }
                      },
                      {
                        "type": "mention",
                        "text": "<at>Adele AAD</at>",
                        "mentioned": {
                          "id": "87d349ed-44d7-43e1-9a83-5f2406dee5bd",
                          "name": "Adele Vance"
                        }
                      }
                ]
            }
        }
    }]
}
```

下图展示了传入 Webhook 中的用户提及：

![传入 Webhook 中的用户提及](~/assets/images/authentication/user-mention-in-incoming-webhook.png)

### <a name="information-masking-in-adaptive-cards"></a>自适应卡片中的信息屏蔽

使用信息屏蔽属性可以屏蔽特定信息，如自适应卡片输入元素内用户的密码或 [`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html) 敏感信息。

> [!NOTE]
> 该功能仅支持客户端信息屏蔽。 将屏蔽的输入文本作为纯文本发送到在机器人配置期间指定的 HTTPS [终结点地址](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint)。

若要屏蔽自适应卡片中的信息，请 `isMasked` 添加属性以 **键入** `Input.Text` ，将其值设置为 **true**。

#### <a name="sample-adaptive-card-with-masking-property"></a>带屏蔽属性的示例自适应卡片

以下代码显示了具有屏蔽属性的自适应卡片的示例：

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

下图是自适应卡片中屏蔽信息的示例：

![屏蔽信息图像](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>全宽自适应卡片

可以使用 属性扩展自适应卡片的宽度， `msteams` 并充分利用额外的画布空间。 下一节将提供有关如何使用 属性的信息。

#### <a name="construct-full-width-cards"></a>构造全宽卡片

若要制作全宽自适应卡片，卡片内容 `width` 中的 `msteams` 属性中的 对象必须设置为 `Full` 。

#### <a name="sample-adaptive-card-with-full-width"></a>全宽自适应卡片示例

若要制作全宽自适应卡片，你的应用必须包含以下代码示例中的元素：

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

下图显示了全宽自适应卡片：

![全宽自适应卡片视图](../../assets/images/cards/full-width-adaptive-card.png)

下图显示自适应卡片的默认视图，当你未将 属性设置为 `width` **Full 时**：

![小宽度自适应卡片视图](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>Typeahead 支持

在 schema 元素中，要求用户筛选和选择大量选项会显著降低 [`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) 任务完成速度。 自适应卡片中的 Typeahead 支持可以在用户键入输入时缩小或筛选输入选项集，从而简化输入选择。

若要在 中启用 `Input.Choiceset` typeahead，请设置为 `style` `filtered` ，并确保 `isMultiSelect` 设置为 `false` 。

#### <a name="sample-adaptive-card-with-typeahead-support"></a>具有字头支持的示例自适应卡片

以下代码演示了具有 typeahead 支持的自适应卡片的示例：

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

在自适应卡片中，可以使用 属性添加选择性地在阶段 `msteams` 视图中显示图像的能力。 当用户将鼠标悬停在图像上时，他们可以看到展开图标，其 `allowExpand` 属性设置为 `true` 。 有关如何使用 属性的信息，请参阅以下示例：

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
          }
     ],
    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
    "version": "1.2"
}
```

当用户将鼠标悬停在图像上方时，右上角将显示展开图标，如下图所示：

![带可展开图像的自适应卡片](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

当用户选择展开图标时，图像将显示在阶段视图中，如下图所示：

![展开到阶段视图的图像](../../assets/images/cards/adaptivecard-expand-image.png)

在阶段视图中，用户可以放大和缩小图像。 可以在自适应卡片中选择必须具有此功能的图像。

> [!NOTE]
> * 放大和缩小功能仅适用于自适应卡片中的图像类型图像元素。
> * 对于Teams应用，自适应卡片中的图像阶段视图功能默认可用。 用户只需点击图像即可在阶段视图中查看自适应卡片图像，无论属性 `allowExpand` 是否存在。

# <a name="markdown-format-for-office-365-connector-cards"></a>[Office 365 连接器卡的 Markdown 格式](#tab/connector-md)

连接器卡支持有限的 Markdown 和 HTML 格式。

| 样式 | 示例 | Markdown |
| --- | --- | --- |
| 粗体 | **text** | `**text**` |
| 斜体 | *text* | `*text*` |
| 标题 (级别 1 &ndash; 3)  | **Text** | `### Text`|
| 删除线 | ~~text~~ | `~~text~~` |
| 未排序列表 | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 已排序列表 | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| 预设格式的文本 | `text` | ``preformatted text`` |
| Blockquote | >blockquote 文本 | `>blockquote text` |
| 超链接 | [必应](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| 图像链接 |![在一个地心上闪避](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

在连接器卡中，为 呈现新行 `\n\n` ，但不为 或 `\n` 呈现 `\r` 。

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>连接器卡的移动和桌面差异

在桌面上，连接器卡的 Markdown 格式显示如下图所示：

![桌面客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-desktop-markdown-combined.png)

在 iOS 上，连接器卡的 Markdown 格式将显示，如下图所示：

![iOS 客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

使用 Markdown for iOS 的连接器卡包括以下问题：

* iOS 客户端用于Teams连接器卡中呈现 Markdown 或 HTML 内嵌图像。
* Blockquotes 呈现为缩进，但不带灰色背景。

在 Android 上，连接器卡的 Markdown 格式显示如下图所示：

![Android 客户端中连接器卡的 Markdown 格式](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="format-example-for-markdown-connector-cards"></a>Markdown 连接器卡的格式示例

以下代码显示了 Markdown 连接器卡的格式设置示例：

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

## <a name="format-cards-with-html"></a>使用 HTML 格式化卡片

以下卡片类型支持 HTML 格式Teams：

* Office 365连接器卡：连接器卡支持有限的 Markdown 和 HTML Office 365格式。
* Hero 和 thumbnail cards：简单卡片支持 HTML 标记，例如 hero 和 thumbnail 卡片。

对于连接器卡和简单卡，桌面版和移动版Teams Office 365不同。 在此部分中，您可以浏览连接器卡和简单卡片的 HTML 格式示例。

# <a name="html-format-for-office-365-connector-cards"></a>[连接器卡Office 365 HTML 格式](#tab/connector-html)

连接器卡支持有限的 Markdown 和 HTML 格式。

| 样式 | 示例 | HTML |
| --- | --- | --- |
| 粗体 | **text** | `<strong>text</strong>` |
| 斜体 | *text* | `<em>text</em>` |
| 标题 (级别 1 &ndash; 3)  | **Text** | `<h3>Text</h3>` |
| 删除线 | ~~text~~ | `<strike>text</strike>` |
| 未排序列表 | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 已排序列表 | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 预设格式的文本 | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| 超链接 | [必应](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 图像链接 | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

在连接器卡中，使用 标记以 HTML 格式呈现 `<p>` 新行。

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>连接器卡的移动和桌面差异

在桌面上，连接器卡的 HTML 格式将显示，如下图所示：

![桌面客户端中连接器卡的 HTML 格式](../../assets/images/cards/Connector-desktop-html-combined.png)

在 iOS 上，HTML 格式显示如下图所示：

![iOS 客户端中连接器卡的 HTML 格式](../../assets/images/cards/connector-iphone-html-combined-80.png)

使用 HTML for iOS 的连接器卡包括以下问题：

* 内联图像不会在 iOS 上使用 Markdown 或 HTML 在连接器卡上呈现。
* 呈现预设格式的文本，但没有灰色背景。

在 Android 上，HTML 格式显示如下图所示：

![Android 客户端中连接器卡的 HTML 格式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="format-sample-for-html-connector-cards"></a>HTML 连接器卡的格式示例

以下代码显示了 HTML 连接器卡的格式设置示例：

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

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[Hero 和缩略图卡片的 HTML 格式](#tab/simple-html)

简单卡片支持 HTML 标记，例如 hero 和 thumbnail 卡片。 不支持 Markdown。

| 样式 | 示例 | HTML |
| --- | --- | --- |
| 粗体 | **text** | `<strong>text</strong>` |
| 斜体 | *text* | `<em>text</em>` |
| 标题 (级别 1 &ndash; 3)  | **Text** | `<h3>Text</h3>` |
| 删除线 | ~~text~~ | `<strike>text</strike>` |
| 未排序列表 | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 已排序列表 | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 预设格式的文本 | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| 超链接 | [必应](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 图像链接 |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>简单卡片的移动和桌面差异

由于桌面平台和移动平台之间存在解决方案差异，因此桌面和移动设备版本之间的格式Teams。

在桌面上，HTML 格式显示如下图所示：

![桌面客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

在 iOS 上，HTML 格式显示如下图所示：

![iOS 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

字符格式（如粗体和 italic）不会呈现在 iOS 上。

在 Android 上，HTML 格式显示如下图所示：

![Android 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-android-60.png)

字符格式，如在 Android 上正确显示粗体和 italic。

### <a name="format-example-for-simple-cards"></a>简单卡片的格式示例

上一部分中的图像是使用 app **Studio** Teams创建的，其中 Hero 卡片的文本属性设置为以下字符串：

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

可以通过修改此代码在你自己的卡片中测试格式。

---

## <a name="see-also"></a>另请参阅

* [卡片操作](./cards-actions.md)
* [使用机器人的任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* [任务模块](~/task-modules-and-cards/cards/cards-format.md)
* [设置你的智能机器人邮件格式](~/bots/how-to/format-your-bot-messages.md)
