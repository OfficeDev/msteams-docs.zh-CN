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
# <a name="cards-reference"></a>卡片参考

本部分中列出的卡片在团队的 bot 中受支持。 它们基于由 Bot 框架定义的卡，但团队不支持所有机器人框架卡，并已添加了其自己的部分。 下面的参考中称为不同之处。

## <a name="card-examples"></a>卡片示例

您可以在机器人生成器 SDK （v3）的文档中找到有关如何使用卡片的其他信息。 GitHub 上的 Microsoft/BotBuilder-示例存储库中也提供了代码示例。

* .NET
  * [将卡片添加为邮件附件](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [卡片示例代码（Bot 生成器 v3）](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* Node.js
  * [将卡片添加为邮件附件](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [卡片示例代码（Bot 生成器 v3）](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a>卡片类型

此表显示了可供您使用的卡片类型。

| 卡片类型 | 说明 |
| --- | --- |
| [自适应卡片](#adaptive-card) | 可包含文本、语音、图像、按钮和输入字段的任意组合的高度可自定义卡片。 |
| [英雄卡片](#hero-card) | 通常包含一个大图像、一个或多个按钮以及少量文本。 |
| [列出卡片](#list-card) | 项目的滚动列表。 |
| [Office 365 连接器卡](#office-365-connector-card) | 具有多个节、字段、图像和操作的灵活布局。 |
| [收据卡](#receipt-card) | 向用户提供收据。 |
| [登录卡片](#signin-card) | 启用机器人以请求用户登录。 |
| [缩略图卡片](#thumbnail-card) | 通常包含一个缩略图图像、一些短文本以及一个或多个按钮。 |
| [卡片集合](#card-collections) | 用于在单个响应中返回多个项目 |

## <a name="common-properties-for-all-cards"></a>所有卡片的通用属性

### <a name="inline-card-images"></a>内嵌卡片图像

您的卡片可以通过包含指向您的公开可用图像的链接来包含内嵌图像。 出于性能考虑，强烈建议您将映像托管在公共内容传递网络（CDN）上。

图像在大小上向上或向下放大，同时保持纵横比以覆盖图像区域，然后从中心裁剪以达到适合该卡片的纵横比。

图像必须最多为1024×1024和 1 MB （PNG、JPEG 或 GIF 格式）;不正式支持动画 GIF。

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| url | URL | 指向图像的 HTTPS URL |
| alt | String | 图像的可访问说明 |

### <a name="buttons"></a>按钮

按钮以堆叠方式显示在卡片底部。 按钮文本总是在单行上，如果文本超出按钮宽度，则将被截尾取整。 不会显示超出卡片支持的最大数量的任何其他按钮。

有关详细信息，请参阅[卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。

### <a name="card-formatting"></a>卡片格式

有关卡片中的文本格式的详细信息，请参阅[卡片格式](~/task-modules-and-cards/cards/cards-format.md)。

## <a name="adaptive-card"></a>自适应卡片

> [!NOTE]
> 对于所有用户，仅支持1.0 版自适应卡。 版本1.2 当前仅适用于开发人员预览版

一种可自定义的卡片，可包含文本、语音、图像、按钮和输入字段的任意组合。

### <a name="support-for-adaptive-cards"></a>对自适应卡片的支持

| 团队中的 bot | 邮件扩展  | 连接器 | Bot 框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="example-adaptive-card"></a>自适应卡片示例

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

#### <a name="for-more-information-on-adaptive-cards"></a>有关自适应卡片的详细信息

* [自适应卡片概述](/adaptive-cards/)
* [团队中的自适应卡片操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a>英雄卡片

通常包含一个大图像（一个或多个按钮和文本）的卡片。

### <a name="support-for-hero-cards"></a>对英雄卡片的支持

| 团队中的 bot | 邮件扩展  | 连接器 | Bot 框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="properties-of-a-hero-card"></a>一个英雄卡片的属性

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多2行;当前不支持的格式 |
| 字幕 | 格式文本  | 卡片的副标题。 最多2行;当前不支持的格式 |
| text | 格式文本  | 文本显示在副标题的正下方;请参阅[卡片格式](~/task-modules-and-cards/cards/cards-format.md)设置选项 |
| 图形 | 图像数组 | 显示在卡片顶部的图像。 纵横比16:9 |
| 按钮 | Action 对象的数组 | 适用于当前卡片的一组操作。 最大6 |
| 即可 | Action 对象 | 当用户点击卡片本身时，将激活此操作 |
|

### <a name="example-hero-card"></a>示例英雄卡片

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

### <a name="for-more-information-on-hero-cards"></a>有关英雄卡片的详细信息

Bot 框架参考：

* ["英雄卡片" 节点](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [英雄卡片 C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0)

## <a name="list-card"></a>列出卡片

团队添加了列表卡，以提供列表集合可以提供的功能之外的功能。 清单卡片提供了项的滚动列表。

### <a name="support-for-list-cards"></a>支持列表卡片

| 团队中的 bot | 邮件扩展  | 连接器 | Bot 框架 |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |
|

### <a name="properties-of-a-list-card"></a>列表卡的属性

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多2行;当前不支持的格式 |
| items | 列表项的数组  ||
| 按钮 | Action 对象的数组 | 适用于当前卡片的一组操作。 最大6。 不会在移动设备上呈现。 |
|

### <a name="example-list-card"></a>列表卡片示例

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

## <a name="office-365-connector-card"></a>Office 365 连接器卡

在团队中受支持，而不是在 Bot 框架中。

Office 365 连接器卡提供了具有多个节、字段、图像和操作的灵活布局。 此卡封装连接器卡，以便 bot 可以使用它。 有关连接器卡和 O365 卡之间的差异，请参阅 "注释" 部分。

### <a name="support-for-office-365-connector-cards"></a>支持 Office 365 连接器卡

| 团队中的 bot | 邮件扩展  | 连接器 | Bot 框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |
|

### <a name="properties-of-the-office-365-connector-card"></a>Office 365 连接器卡的属性

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多2行;当前不支持的格式 |
| 摘要 | 格式文本  | 卡片摘要。 最多2行;当前不支持的格式 |
| text | 格式文本  | 文本显示在副标题的正下方;请参阅[卡片格式](~/task-modules-and-cards/cards/cards-format.md)设置选项 |
| themeColor | 十六进制字符串 | 重写从应用程序清单提供的 accentColor 的颜色 |

### <a name="notes-on-the-office-365-connector-card"></a>Office 365 连接器卡上的备注

Office 365 连接器卡在 Microsoft 团队中正常工作，包括[ActionCard 操作](/outlook/actionable-messages/card-reference#actioncard-action)。

使用连接器中的连接器卡和在你的 bot 中使用连接器卡的一个重要区别是处理智能卡操作。

* 对于连接器，终结点通过 HTTP POST 接收卡有效负载。
* 对于 bot，该`HttpPOST`操作触发仅将`invoke`操作 ID 和正文发送到 bot 的活动。

每个连接器卡最多可以显示10个部分，每个部分最多可包含5个图像和5个操作。

> [!NOTE]
> 将不会显示邮件中的任何其他节、图像或操作。

所有文本字段都支持 Markdown 和 HTML。 您可以通过在邮件中设置`markdown`属性来控制哪些部分使用 MARKDOWN 或 HTML。 默认情况下`markdown` ，设置为`true`;如果要改为使用 HTML，则将`markdown`设置`false`为。

如果指定`themeColor`属性，它将替代应用程序`accentColor`清单中的属性。

若要指定的呈现样式`activityImage`，可以按如下`activityImageType`所示进行设置。

| 值 | 说明 |
| --- | --- |
| `avatar` | 设置`activityImage`将裁剪为圆形 |
| `article` | `activityImage`将显示为一个矩形，并保持其纵横比 |

有关连接器卡属性的所有其他详细信息，请参阅可[操作邮件卡参考](/outlook/actionable-messages/card-reference)。 Microsoft 团队目前不支持的连接器卡片属性如下所示：

* `heroImage`
* `hideOriginalBody`
* `startGroup`（始终按`true`团队处理）
* `originator`
* `correlationId`

### <a name="example-office-365-connector-card"></a>示例 Office 365 连接器卡

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

## <a name="receipt-card"></a>收据卡

在团队中受支持。

使 bot 能够向用户提供收据的卡片。 它通常包含要包含在收据、税和总计信息以及其他文本中的项的列表。

### <a name="support-for-receipts-cards"></a>对收据卡的支持

| 团队中的 bot | 邮件扩展  | 连接器 | Bot 框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="for-more-information-on-receipt-cards"></a>有关收据卡的详细信息

Bot 框架参考：

* ["收据卡" 节点](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest)
* [收据卡 C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0)

## <a name="signin-card"></a>登录卡片

使机器人能够请求用户登录的卡片。 在与 Bot 框架中相比，在不同表单中的团队中支持。 团队中的登录卡片与 bot 框架中的登录卡片类似，但在团队登录卡仅支持两个操作时除外： `signin`和。 `openUrl`

*登录操作*可用于团队中的任何卡片，而不仅仅是登录卡。 有关身份验证的详细信息，请参阅[Microsoft 团队身份验证流的](~/bots/how-to/authentication/auth-flow-bot.md)主题相关主题。

### <a name="support-for-signin-cards"></a>对登录卡的支持

| 团队中的 bot | 邮件扩展  | 连接器 | Bot 框架 |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

### <a name="for-more-information-on-signin-cards"></a>有关登录卡的详细信息

Bot 框架参考：

* [登录卡片节点](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest)
* [登录卡 C#](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0)

## <a name="thumbnail-card"></a>缩略图卡片

通常包含单个缩略图图像、一个或多个按钮以及文本的卡片。

### <a name="support-for-thumbnail-cards"></a>支持缩略图卡片

| 团队中的 bot | 邮件扩展  | 连接器 | Bot 框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

![缩略图示例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>缩略图卡的属性

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多2行;当前不支持的格式 |
| 字幕 | 格式文本  | 卡片的副标题。 最多2行;当前不支持的格式 |
| text | 格式文本  | 文本显示在副标题的正下方;请参阅[卡片格式](~/task-modules-and-cards/cards/cards-format.md)设置选项 |
| 图形 | 图像数组 | 显示在卡片顶部的图像。 纵横比1:1 （方形） |
| 按钮 | Action 对象的数组 | 适用于当前卡片的一组操作。 最大6 |
| 即可 | Action 对象 | 当用户点击卡片本身时，将激活此操作 |
|

### <a name="example-thumbnail-card"></a>缩略图示例卡片

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

### <a name="for-more-information"></a>更多详细信息

Bot 框架参考：

* [缩略图卡片节点](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest)
* [缩略图卡片 C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0)

## <a name="card-collections"></a>卡片集合

团队中支持卡片集合。

卡集合由 Bot 框架（ `builder.AttachmentLayout.carousel`和`builder.AttachmentLayout.list`）提供。 这些集合可以包含自适应、英雄或缩略图卡片。

## <a name="carousel-collection"></a>轮播集合

[轮播布局](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0)显示了卡片的轮播，也可以选择使用关联的动作按钮。

### <a name="support-for-carousel-collections"></a>对轮播集合的支持

| 团队中的 bot | 邮件扩展  | 连接器 | Bot 框架 |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

> [!NOTE]
> 每封邮件的轮播最多可显示10张卡片。

### <a name="example-carousel-collection"></a>示例轮播集合

![卡片轮播的示例](~/assets/images/cards/carousel.png)

属性与对英雄或缩略图卡片的属性相同。

### <a name="syntax-for-carousel-collections"></a>轮播集合的语法

`builder.AttachmentLayout.carousel`

## <a name="list-collection"></a>列表集合

### <a name="support-for-list-collections"></a>对列表集合的支持

列表布局显示垂直堆叠的卡片列表，可以选择使用关联的操作按钮。

| 团队中的 bot | 邮件扩展  | 连接器 | Bot 框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="example-list-collection"></a>示例列表集合

![卡片列表的示例](~/assets/images/cards/list.png)

属性与对英雄或缩略图卡片的属性相同。

列表最多可显示10个卡片（每封邮件）。

> [!NOTE]
> 清单卡的某些组合在 iOS 和 Android 上尚不受支持。

### <a name="syntax-for-list-collections"></a>列表集合的语法

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a>团队不支持的卡片

以下卡片由 Bot 框架实现，但团队不支持。

* 动画卡片
* 音频卡
* 视频卡
