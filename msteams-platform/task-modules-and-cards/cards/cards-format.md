---
title: 卡片中的文本格式
description: 介绍 Microsoft Teams 中的卡片文本格式
keywords: 团队机器人卡格式
ms.localizationpriority: high
ms.topic: reference
ms.date: 06/25/2021
ms.openlocfilehash: d660d58b00624b4d91ce4241829b204c66ba95df
ms.sourcegitcommit: 9e448dcdfd78f4278e9600808228e8158d830ef7
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/17/2022
ms.locfileid: "62059600"
---
# <a name="format-cards-in-microsoft-teams"></a>Microsoft Teams 中的格式卡

下面是向卡片添加富格式的两种方法:
* [Markdown](#format-cards-with-markdown)
* [HTML](#format-cards-with-html)

卡片仅支持文本属性中的格式设置，不支持在标题或副标题属性中进行格式设置。 可以使用 XML 或 HTML 格式的子集或 Markdown 指定格式，具体取决于卡类型。 对于当前和将来的自适应卡片开发，建议使用 Markdown 格式设置。

卡片类型之间的格式设置支持有所不同。 桌面和移动 Microsoft Teams 客户端以及桌面浏览器中的 Teams 之间的卡片呈现可能略有不同。

可以在任何 Teams 卡片中包含内联图像。 图像的格式可以为 `.png`、`.jpg` 或 `.gif` 文件，且不得超过 1024 x1024 px 或 1 MB。 不支持动态 GIF。 有关详细信息，请参阅 [类型的卡片](./cards-reference.md#inline-card-images)。

可以使用包含某些支持样式的 Markdown 格式化自适应卡片和 Office 365 连接器卡片。

## <a name="format-cards-with-markdown"></a>使用 Markdown 的格式卡片

以下卡片类型支持 Teams 中的 Markdown 格式设置:

* 自适应卡片: 在自适应卡片 `Textblock` 字段以及 `Fact.Title` 和 `Fact.Value` 中支持 Markdown。 自适应卡片不支持 HTML。
* Office 365 连接器卡: Office 365 连接器卡在文本字段支持 Markdown 和有限的 HTML 格式设置。

可以将换行符用于自适应卡片，使用 `\r` 或 `\n` 列表中新行的转义序列。 桌面和移动版适用于自适应卡的 Teams 的格式不同。 Web、桌面和移动客户端都支持基于卡片的提及。 可以使用信息掩码属性来屏蔽特定信息，例如自适应卡`Input.Text`输入元素中用户的密码或敏感信息。 你可以使用 `width` 对象扩展自适应卡的宽度。 可以自适应卡片内启用键盘缓冲支持，并在用户键入输入时筛选输入选项集。 可以使用 `msteams` 属性添加在阶段视图中选择地显示图像的功能。

桌面和移动版适用于自适应卡 和连接器卡片的 Teams 的格式不同。 在本部分中，可以通过 Markdown 格式示例了解自适应卡和连接器卡。

# <a name="markdown-format-for-adaptive-cards"></a>[自适应卡片的 Markdown 格式](#tab/adaptive-md)

 下表提供了 `Textblock`、`Fact.Title` 和 `Fact.Value` 支持的样式:

| 样式 | 示例 | Markdown |
| --- | --- | --- |
| 粗体 | **Bold** | ```**Bold**``` |
| 斜体 | _Italic_ | ```_Italic_``` |
| 未排序列表 | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 已排序列表 | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| Hyperlinks |[必应](https://www.bing.com/)| ```[Title](url)``` |

不支持以下 Markdown 标记:

* 标题
* 表格
* 图像
* 预设格式的文本
* 块引号

### <a name="newlines-for-adaptive-cards"></a>自适应卡片的换行符

可以在列表中使用 `\r` 或 `\n` 转义序列来换行。 在列表中使用 `\n\n` 会导致缩进列表中的下一个元素。 如果需要在 TextBlock 中其他位置换行，请使用 `\n\n`。

### <a name="mobile-and-desktop-differences-for-adaptive-cards"></a>自适应卡的移动和桌面差异

在桌面上，自适应卡片 Markdown 格式显示在 Web 浏览器和 Teams 客户端应用程序中，如下图所示:

![桌面客户端中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-desktop-client.png)

在 IOS 上，自适应卡片 Markdown 格式显示如下图所示:

![IOS 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-iOS-75.png)

在 Android 上，自适应卡片 Markdown 格式显示如下图所示:

![Android 中的自适应卡片 Markdown 格式](../../assets/images/cards/Adaptive-markdown-Android.png)

有关详细信息，请参阅 [自适应卡片中的文本功能](/adaptive-cards/create/textfeatures)。

> [!NOTE]
> Teams 不支持本节中提到的日期和本地化功能。

### <a name="adaptive-cards-format-sample"></a>自适应卡片格式示例

以下代码演示自适应卡片格式的示例:

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

### <a name="mention-support-within-adaptive-cards"></a>自适应卡片内提及的支持 

可以在自适应卡主体中为机器人和消息传递扩展响应添加@提及。 若要在卡片中添加@提及，请遵循[在频道和群组聊天对话中提及](../../bots/how-to/conversations/channel-and-group-conversations.md#work-with-mentions) 基于消息的相同通知逻辑和呈现。

机器人和消息传递扩展可以在 [TextBlock](https://adaptivecards.io/explorer/TextBlock.html) 和 [FactSet](https://adaptivecards.io/explorer/FactSet.html) 元素的卡片内容中包含提及。

> [!NOTE]
> * Teams 平台上的自适应卡片目前不支持 [媒体元素](https://adaptivecards.io/explorer/Media.html)。
> * 机器人消息不支持频道和团队提及。

若要在自适应卡片中包含提及，应用需要包含以下元素:

* `<at>username</at>` 在支持的自适应卡元素中。
* 卡片内容中 `msteams` 属性的 `mention` 对象包括所提及用户的 Teams 用户 ID。
* `userId` 对于机器人 ID 和特定用户是唯一的。 它可用于@提及特定用户。 `userId` 可以使用在 [获取用户 ID](/microsoftteams/platform/bots/how-to/conversations/send-proactive-messages?tabs=dotnet#get-the-user-id-team-id-or-channel-id) 中提到的一个选项来检索。

#### <a name="sample-adaptive-card-with-a-mention"></a>带提及的示例自适应卡片

下面的代码演示了具有提及的自适应卡片示例:

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

### <a name="aad-object-id-and-upn-in-user-mention"></a>在用户提及中的 AAD 对象 ID 和 UPN 

除了现有的提及 ID 外，Teams 平台还允许使用其 AAD 对象 ID 和用户原则名称 (UPN) 提及用户。 带有自适应卡的机器人和带有传入 Webhook 的连接器支持两个用户提及的 ID。 

下表描述了新支持的用户提及 ID:

|ID  | 支持功能 |   说明 | 示例 |
|----------|--------|---------------|---------|
| AAD 对象 ID | 机器人，连接器 |  AAD 用户的对象 ID |  49c4641c-ab91-4248-aebb-6a7de286397b |
| UPN | 机器人，连接器 | AAD 用户的 UPN | john.smith@microsoft.com |

#### <a name="user-mention-in-bots-with-adaptive-cards"></a>使用自适应卡片在机器人中提及用户 

除现有 ID 外，机器人还支持使用 AAD 对象 ID 和 UPN 提及用户。 对于短信、自适应卡片正文和消息传递扩展响应，机器人中提供了对两个新 ID 的支持。 机器人支持对话和 `invoke` 方案中的提及 ID。 使用 ID @提及时，用户将获取活动源通知。 

> [!NOTE]
> 在机器人中使用自适应卡片的用户提及不需要架构更新和 UI/UX 更改。

##### <a name="example"></a>示例 

使用自适应卡在机器人中提到的用户示例如下:

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

下图演示了在机器人中使用自适应卡片的用户提及:

![使用自适应卡片在机器人中提及用户](~/assets/images/authentication/user-mention-in-bot.png)

#### <a name="user-mention-in-incoming-webhook-with-adaptive-cards"></a>使用自适应卡片的传入 Webhook 中的用户提及 

传入 Webhook 开始支持使用 AAD 对象 ID 和 UPN 在自适应卡片中提及用户。

> [!NOTE]    
> * 在传入 Webhook 的架构中启用用户提及，以支持 AAD 对象 ID 和 UPN。 
> * 对于具有 AAD 对象 ID 和 UPN 的用户提及不需要进行 UI/UX 更改。      

##### <a name="example"></a>示例 

传入 Webhook 中的用户提及示例如下所示:

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

下图说明了在传入 Webhook 中的用户提及:

![传入 Webhook 中的用户提及](~/assets/images/authentication/user-mention-in-incoming-webhook.png)

### <a name="information-masking-in-adaptive-cards"></a>自适应卡片中的信息屏蔽

使用信息掩码属性来屏蔽特定信息，例如自适应卡[`Input.Text`](https://adaptivecards.io/explorer/Input.Text.html)输入元素中用户的密码或敏感信息。

> [!NOTE]
> 该功能仅支持客户端信息掩码。 掩码输入文本以明文形式发送到在 [机器人配置期间指定的 HTTPS 终结点地址](../../build-your-first-app/build-bot.md#4-register-your-bot-endpoint)。

若要屏蔽自适应卡片中的信息，请将 `style`属性添加到 **类型** `input.text`，然后将其值设置为 **密码**。

#### <a name="sample-adaptive-card-with-masking-property"></a>带掩码属性的示例自适应卡片

下面的代码演示了具有掩码属性的自适应卡片的示例:

```json
{
    "type": "Input.Text",
    "id": "secretThing",
    "style": "password",
},
```

下图是自适应卡片中屏蔽信息的示例:

![屏蔽信息图像](../../assets/images/cards/masking-information-view.png)

### <a name="full-width-adaptive-card"></a>全宽自适应卡片

可以使用 `msteams` 属性扩展自适应卡片的宽度并使用其他画布空间。 下一部分提供有关如何使用该属性的信息。

#### <a name="construct-full-width-cards"></a>构造全宽卡

若要制作全宽自适应卡，卡片内容中的 `width` 对象 `msteams` 属性必须设置为 `Full`。

#### <a name="sample-adaptive-card-with-full-width"></a>全宽自适应卡片示例

若要制作全宽自适应卡片，应用必须包含以下代码示例中的元素:

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

下图显示了全宽自适应卡片:

![全宽自适应卡片视图](../../assets/images/cards/full-width-adaptive-card.png)

下图显示了未将 `width` 属性设置为 **完全** 时自适应卡片的默认视图:

![小宽自适应卡片视图](../../assets/images/cards/small-width-adaptive-card.png)

### <a name="typeahead-support"></a>键盘缓冲支持

在[`Input.Choiceset`](https://adaptivecards.io/explorer/Input.ChoiceSet.html)架构元素中，要求用户筛选和选择大量选项可能会显著降低任务完成的速度。 自适应卡片内的键盘缓冲支持可以通过在用户键入输入时缩小或筛选输入选项集来简化输入选择。

若要在 `Input.Choiceset` 中启用键盘缓冲，请将 `style` 设置为 `filtered` 并确保 `isMultiSelect` 设置为 `false`。

#### <a name="sample-adaptive-card-with-typeahead-support"></a>具有键盘缓冲支持的示例自适应卡片

下面的代码演示了具有键盘缓冲支持的自适应卡片示例:

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

### <a name="stage-view-for-images-in-adaptive-cards"></a>自适应卡片中图像的阶段视图

在自适应卡片中，可以使用 `msteams` 属性添加在阶段视图中选择地显示图像的功能。 当用户将鼠标悬停在图像上时，可以看到 `allowExpand` 属性设置为 `true` 的展开图标。 有关如何使用该属性的信息，请参阅以下示例:

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

当用户将鼠标悬停在图像上时，展开图标将显示在右上角，如下图所示:

![具有可展开图像的自适应卡片](../../assets/images/cards/adaptivecard-hover-expand-icon.png)

当用户选择展开图标时，图像将显示在阶段视图中，如下图所示:

![图像扩大到阶段视图](../../assets/images/cards/adaptivecard-expand-image.png)

在阶段视图中，用户可以放大和缩小图像。 你可以在自适应卡片中选择必须具有此功能的图像。

> [!NOTE]
> * 放大和缩小功能仅适用于自适应卡片中图像类型的图像元素。
> * 对于 Teams 移动应用，自适应卡片中图像的阶段视图功能是默认可用的。 用户只需点击图像即可在阶段视图中查看自适应卡片图像，而不考虑是否存在 `allowExpand` 属性。

# <a name="markdown-format-for-office-365-connector-cards"></a>[用于 Office 365 连接器卡片的 Markdown 格式](#tab/connector-md)

连接器卡支持有限的 Markdown 和 HTML 格式设置。

| 样式 | 示例 | Markdown |
| --- | --- | --- |
| 粗体 | **text** | `**text**` |
| 斜体 | *text* | `*text*` |
| 标头 (级别 1&ndash;3) | **Text** | `### Text`|
| 删除线 | ~~text~~ | `~~text~~` |
| 未排序列表 | <ul><li>text</li><li>text</li></ul> | ```- Item 1\r- Item 2\r- Item 3``` |
| 已排序列表 | <ol><li>text</li><li>text</li></ol> | ```1. Green\r2. Orange\r3. Blue``` |
| 预设格式的文本 | `text` | ``preformatted text`` |
| Blockquote | >blockquote 文本 | `>blockquote text` |
| Hyperlink | [必应](https://www.bing.com/) | `[Bing](https://www.bing.com/)` |
| 图像链接 |![岩石上的鸭子](https://aka.ms/Fo983c) | `![Duck](https://aka.ms/Fo983c)` |

在连接器卡中，为 `\n\n` 呈现换行符，但不针对 `\n` 或 `\r` 呈现换行符。

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>连接器卡的移动和桌面差异

在桌面上，连接器卡片的 Markdown 格式显示如下图所示:

![桌面客户端中连接器卡片的 Markdown 格式](../../assets/images/cards/connector-desktop-markdown-combined.png)

在 IOS 上，连接器卡片的 Markdown 格式显示如下图所示:

![IOS 客户端中连接器卡片的 Markdown 格式](../../assets/images/cards/connector-iphone-markdown-combined-80.png)

使用 Markdown for iOS 的连接器卡包括以下问题:

* 适用于 Teams 的 iOS 客户端不会在连接器卡片中呈现 Markdown 或 HTML 内联图像。
* 块引号呈现为缩进，但没有灰色背景。

在 Android 上，连接器卡片的 Markdown 格式显示如下图所示:

![Android 客户端中连接器卡片的 Markdown 格式](../../assets/images/cards/connector-android-markdown-combined.png)

### <a name="format-example-for-markdown-connector-cards"></a>Markdown 连接器卡的格式示例

以下代码演示 Markdown 连接器卡的格式设置示例:

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

## <a name="format-cards-with-html"></a>使用 HTML 的格式卡片

以下卡片类型支持 Teams 中的 HTML 格式设置:

* Office 365 连接器卡: Office 365 连接器卡支持有限的 Markdown 和 HTML 格式设置。
* 主图和缩略图卡：简单卡片 (如主图和缩略图卡) 支持 HTML 标记。

桌面和移动版 Teams for Office 365 连接器卡和简单卡片的格式不同。 在本部分中，可以通过 HTML 格式示例了解连接器卡和简单卡。

# <a name="html-format-for-office-365-connector-cards"></a>[用于 Office 365 连接器卡片的 HTML 格式](#tab/connector-html)

连接器卡支持有限的 Markdown 和 HTML 格式设置。

| 样式 | 示例 | HTML |
| --- | --- | --- |
| 粗体 | **text** | `<strong>text</strong>` |
| 斜体 | *text* | `<em>text</em>` |
| 标头 (级别 1&ndash;3) | **Text** | `<h3>Text</h3>` |
| 删除线 | ~~text~~ | `<strike>text</strike>` |
| 未排序列表 | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 已排序列表 | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 预设格式的文本 | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| Hyperlink | [必应](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 图像链接 | <img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img> | `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

在连接器卡中，换行符是使用 `<p>` 标记在 HTML 中呈现的。

### <a name="mobile-and-desktop-differences-for-connector-cards"></a>连接器卡的移动和桌面差异

在桌面上，连接器卡片的 HTML 格式显示如下图所示:

![桌面客户端中连接器卡片的 HTML 格式](../../assets/images/cards/Connector-desktop-html-combined.png)

在 iOS 上，HTML 格式如下图所示:

![iOS 客户端中连接器卡的 HTML 格式设置](../../assets/images/cards/connector-iphone-html-combined-80.png)

使用 HTML for iOS 的连接器卡包括以下问题:

* 在 iOS 上使用连接器卡中的 Markdown 或 HTML 无法呈现内联图像。
* 呈现预先格式化的文本，但没有灰色背景。

在 Android 上，HTML 格式如下图所示:

![Android 客户端中连接器卡片的 HTML 格式](../../assets/images/cards/connector-android-html-combined.png)

### <a name="format-sample-for-html-connector-cards"></a>HTML 连接器卡的格式示例

以下代码演示 HTML 连接器卡的格式设置示例:

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

# <a name="html-format-for-hero-and-thumbnail-cards"></a>[主图和缩略图卡 HTML 格式](#tab/simple-html)

简单卡片 (如主图和缩略图卡) 支持 HTML 标记。 不支持 Markdown。

| 样式 | 示例 | HTML |
| --- | --- | --- |
| 粗体 | **text** | `<strong>text</strong>` |
| 斜体 | *text* | `<em>text</em>` |
| 标头 (级别 1&ndash;3) | **Text** | `<h3>Text</h3>` |
| 删除线 | ~~text~~ | `<strike>text</strike>` |
| 未排序列表 | <ul><li>text</li><li>text</li></ul> | `<ul><li>text</li><li>text</li></ul>` |
| 已排序列表 | <ol><li>text</li><li>text</li></ol> | `<ol><li>text</li><li>text</li></ol>` |
| 预设格式的文本 | `text` | `<pre>text</pre>` |
| Blockquote | <blockquote>text</blockquote> | `<blockquote>text</blockquote>` |
| Hyperlink | [必应](https://www.bing.com/) | `<a href="https://www.bing.com/">Bing</a>` |
| 图像链接 |<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>| `<img src="https://aka.ms/Fo983c" alt="Duck on a rock"></img>` |

### <a name="mobile-and-desktop-differences-for-simple-cards"></a>简单卡的移动和桌面差异

由于桌面和移动平台之间存在解析差异，因此 Teams 的桌面和移动版之间的格式不同。

在桌面上，HTML 格式如下图所示:

![桌面客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-desktop-v2.png)

在 iOS 上，HTML 格式如下图所示:

![iOS 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-mobile-v2.png)

字符格式 (如粗体和斜体) 不会在 iOS 上呈现。

在 Android 上，HTML 格式如下图所示:

![Android 客户端中的 HTML 格式](../../assets/images/cards/card-formatting-xml-android-60.png)

字符格式，如粗体和斜体在 Android 上正确显示。

### <a name="format-example-for-simple-cards"></a>简单卡片的格式示例

上一部分中的图像是使用 Teams **App Studio** 创建的，其中主图卡的文本属性设置为以下字符串:

`<p>bold: <strong>Bold Text</strong></p><p>italic: <em>Italic Text</em></p><p>strikethrough: <strike>Strikethrough text</strike></p><h1>Header 1</h1><h2>Header 2</h2><h3>Header 3</h3><p>bullet list: <ul><li>text</li><li>text</li></ul></p><p>ordered list: <ol><li>text</li><li>text</li></ol></p><pre>preformatted text</pre><blockquote>blockquote text</blockquote></p><p>hyperlink: <a href=\"https://www.bing.com/\">Bing</a></p><p>embedded image: <img src=\"https://aka.ms/Fo983c\" alt=\"Duck on a rock\"></img></p>`

可以通过修改此代码在自己的卡片中测试格式。

---

## <a name="see-also"></a>另请参阅

* [卡片操作](./cards-actions.md)
* [使用机器人的任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* [任务模块](~/task-modules-and-cards/cards/cards-format.md)
* [设置你的智能机器人邮件格式](~/bots/how-to/format-your-bot-messages.md)
