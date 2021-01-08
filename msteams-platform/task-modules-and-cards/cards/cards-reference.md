---
title: 卡片参考
description: 介绍 Teams 中自动程序可用的所有卡片和卡片操作
keywords: 机器人卡参考
ms.openlocfilehash: 22a4faa932173387cbefe900e30106d063c49e50
ms.sourcegitcommit: 5739245903278d521ec920427248b6b48676e637
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/07/2021
ms.locfileid: "49778392"
---
# <a name="cards-reference"></a>卡片参考

本部分中列出的卡片在 Teams 自动程序中受支持。 它们基于 Bot Framework 定义的卡，但 Teams 不支持所有 Bot Framework 卡，并且已添加一些自己的卡。 下面引用中列出了差异。

## <a name="card-examples"></a>卡片示例

有关如何使用自动程序生成器 SDK (v3) 文档中的其他信息。 GitHub 上的 Microsoft/BotBuilder 示例存储库中也提供了一些代码示例。

* .NET
  * [将卡片添加为邮件附件](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments)
  * [自动程序生成器 v3 (的卡片示例) ](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/CSharp/cards-RichCards)
* Node.js
  * [将卡片添加为邮件附件](/bot-framework/nodejs/bot-builder-nodejs-send-rich-cards)
  * [自动程序生成器 v3 (的卡片示例) ](https://github.com/Microsoft/BotBuilder-Samples/tree/v3-sdk-samples/Node/cards-RichCards)

## <a name="types-of-cards"></a>卡片类型

此表显示可用的卡片类型。

| 卡片类型 | 说明 |
| --- | --- |
| [自适应卡片](#adaptive-card) | 可包含文本、语音、图像、按钮和输入字段的任意组合的高度可自定义卡片。 |
| [Hero Card](#hero-card) | 通常包含单个大图像、一个或多个按钮和少量文本。 |
| [列表卡片](#list-card) | 项的滚动列表。 |
| [Office 365 连接器卡](#office-365-connector-card) | 具有多个分区、字段、图像和操作的灵活性布局。 |
| [收据卡](#receipt-card) | 向用户提供收据。 |
| [登录卡](#signin-card) | 使机器人能够请求用户登录。 |
| [缩略图卡片](#thumbnail-card) | 通常包含单个缩略图图像、一些短文本和一个或多个按钮。 |
| [卡片集合](#card-collections) | 用于在单个响应中返回多个项目 |

## <a name="common-properties-for-all-cards"></a>所有卡片的常见属性

### <a name="inline-card-images"></a>内联卡片图像

你的卡片可以通过包含指向公开可用图像的链接来包含内嵌图像。 出于性能目的，我们强烈建议你将图像托管在 CDN 服务的公共内容交付 (CDN) 。

在保持纵横比以覆盖图像区域的同时，图像会放大或缩小大小，然后从中心裁剪以实现卡片的适当纵横比。

图像必须最多为 1024×1024 PNG、JPEG 或 GIF 格式;动态 GIF 不受正式支持。

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| url | URL | 图像的 HTTPS URL |
| alt | String | 图像的辅助说明 |

### <a name="buttons"></a>按钮

按钮显示在卡片底部堆叠。 按钮文本始终在一行上，如果文本超过按钮宽度，按钮文本将被截断。 不会显示超出卡支持的最大数目的其他任何按钮。

有关详细信息 [，](~/task-modules-and-cards/cards/cards-actions.md) 请参阅卡片操作。

### <a name="card-formatting"></a>卡片格式

有关 [卡片中的](~/task-modules-and-cards/cards/cards-format.md) 文本格式设置详细信息，请参阅卡片格式。

## <a name="adaptive-card"></a>自适应卡片

可自定义的卡片，可包含文本、语音、图像、按钮和输入字段的任意组合。 *请参阅*[自适应卡片 v1.2.0](https://github.com/microsoft/AdaptiveCards/releases/tag/v1.2.0)。

### <a name="support-for-adaptive-cards"></a>支持自适应卡片

| Teams 中的聊天机器人 | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

> [!NOTE]
> * Teams 平台支持 v1.2 或更早的自适应卡片功能。
> * Teams 平台上的自适应卡片 v1.2 当前不支持媒体元素。
### <a name="example-adaptive-card"></a>自适应卡片示例

![自适应卡片示例](~/assets/images/cards/adaptivecard.png)

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

#### <a name="for-more-information-on-adaptive-cards"></a>有关自适应卡片详细信息

* [自适应卡片概述](/adaptive-cards/)
* [Teams 中的自适应卡片操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)

## <a name="hero-card"></a>Hero 卡片

通常包含单个大图像、一个或多个按钮和文本的卡片。

### <a name="support-for-hero-cards"></a>支持 Hero 卡片

| Teams 中的聊天机器人 | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="properties-of-a-hero-card"></a>Hero 卡片的属性

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多 2 行。 |
| subtitle | 格式文本  | 卡片的副标题。 最多 2 行。|
| text | 格式文本  | 文本显示在副标题正下方;请参阅 [格式选项](~/task-modules-and-cards/cards/cards-format.md) 的卡片格式 |
| images | 图像数组 | 显示在卡片顶部的图像。 纵横比 16：9 |
| buttons | 操作对象数组 | 适用于当前卡片的操作集。 最大值 6 |
| 点击 | Action 对象 | 当用户点击卡片本身时，将激活此操作 |
|

### <a name="example-hero-card"></a>示例 Hero 卡片

![Hero 卡片示例](~/assets/images/cards/hero.png)

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

### <a name="for-more-information-on-hero-cards"></a>有关 Hero 卡片详细信息

Bot Framework 参考：

* [主卡节点](https://docs.microsoft.com/javascript/api/botframework-schema/herocard)
* [Hero card C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.herocard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="list-card"></a>列表卡

Teams 已添加列表卡片，以提供列表集合无法提供的功能。 列表卡提供项的滚动列表。

### <a name="support-for-list-cards"></a>支持列表卡

| Teams 中的聊天机器人 | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |
|

### <a name="properties-of-a-list-card"></a>列表卡片的属性

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多 2 行。|
| items | 列表项数组  ||
| buttons | 操作对象数组 | 适用于当前卡片的操作集。 最大值 6。 |

### <a name="example-list-card"></a>示例列表卡片

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

在 Teams 中受支持，在 Bot Framework 中不受支持。

Office 365 连接器卡提供具有多个分区、字段、图像和操作的灵活性布局。 此卡封装连接器卡，以便机器人可以使用它。 有关连接器卡和 O365 卡之间的差异，请参阅"备注"部分。

### <a name="support-for-office-365-connector-cards"></a>支持 Office 365 连接器卡

| Teams 中的聊天机器人 | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |
|

### <a name="properties-of-the-office-365-connector-card"></a>Office 365 连接器卡的属性

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多 2 行。 |
| 摘要 | 格式文本  | 卡片摘要。 最多 2 行。 |
| text | 格式文本  | 文本显示在副标题正下方;请参阅 [格式选项](~/task-modules-and-cards/cards/cards-format.md) 的卡片格式 |
| themeColor | 十六进制字符串 | 替代应用程序清单中提供的 accentColor 的颜色 |

### <a name="notes-on-the-office-365-connector-card"></a>Office 365 连接器卡上的备注

Office 365 连接器卡在 Microsoft Teams 上正常工作，包括 [ActionCard 操作](/outlook/actionable-messages/card-reference#actioncard-action)。

从连接器使用连接器卡和在机器人中使用连接器卡之间的一个重要区别是卡片操作的处理。

* 对于连接器，终结点通过 HTTP POST 接收卡有效负载。
* 对于自动程序，该操作将触发仅向自动程序发送操作 `HttpPOST` `invoke` ID 和正文的活动。

每个连接器卡最多可以显示 10 个部分，每个部分最多可以包含 5 个图像和 5 个操作。

> [!NOTE]
> 邮件中其他任何部分、图像或操作将不会显示。

所有文本字段都支持 Markdown 和 HTML。 您可以通过在邮件中设置属性来控制使用 Markdown 或 HTML `markdown` 的部分。 默认情况下， `markdown` 设置为;如果要改为使用 `true` HTML，则设置为 `markdown` `false` 。

如果指定 `themeColor` 该属性，它将覆盖 `accentColor` 应用清单中的属性。

若要指定其呈现样式 `activityImage` ，可以按 `activityImageType` 如下方式设置。

| 值 | 说明 |
| --- | --- |
| `avatar` | 默认值; `activityImage` 将裁剪为圆形 |
| `article` | `activityImage` 将显示为矩形并保留其纵横比 |

有关连接器卡属性的所有其他详细信息，请参阅 [可操作邮件卡参考](/outlook/actionable-messages/card-reference)。 Microsoft Teams 当前不支持的唯一连接器卡属性如下所示：

* `heroImage`
* `hideOriginalBody`
* `startGroup` (Teams `true`) 
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

在 Teams 中受支持。

使机器人能够向用户提供收据的卡。 它通常包含要包含在收据、税务和总额信息以及其他文本中的项目列表。

### <a name="support-for-receipts-cards"></a>对收据卡的支持

| Teams 中的聊天机器人 | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="for-more-information-on-receipt-cards"></a>有关收据卡详细信息

Bot Framework 参考：

* [收据卡节点](https://docs.microsoft.com/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [收据卡 C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.receiptcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="signin-card"></a>登录卡

使机器人能够请求用户登录的卡。 在 Teams 中受支持的形式与在 Bot Framework 中稍有不同。 Teams 中的登录卡类似于自动程序框架中的登录卡，但 Teams 中的登录卡仅支持两项操作： `signin` 和 `openUrl` 。

登录 *操作可以从* Teams 中的任意卡使用，而不只是从登录卡使用。 有关身份验证 [的详细信息，请参阅机器人](~/bots/how-to/authentication/auth-flow-bot.md) 的 Microsoft Teams 身份验证流主题。

### <a name="support-for-signin-cards"></a>支持登录卡

| Teams 中的聊天机器人 | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

### <a name="for-more-information-on-signin-cards"></a>有关登录卡详细信息

Bot Framework 参考：

* [登录卡节点](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [登录卡 C#](/dotnet/api/microsoft.bot.connector.signincard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="thumbnail-card"></a>缩略图卡片

通常包含单个缩略图图像、一个或多个按钮和文本的卡片。

### <a name="support-for-thumbnail-cards"></a>支持缩略图卡片

| Teams 中的聊天机器人 | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

![缩略图卡片示例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>缩略图卡片的属性

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多 2 行。|
| subtitle | 格式文本  | 卡片的副标题。 最多 2 行。|
| text | 格式文本  | 文本显示在副标题正下方;请参阅 [格式选项](~/task-modules-and-cards/cards/cards-format.md) 的卡片格式 |
| images | 图像数组 | 显示在卡片顶部的图像。 纵横比 1：1 (平方)  |
| buttons | 操作对象数组 | 适用于当前卡片的操作集。 最大值 6 |
| 点击 | Action 对象 | 当用户点击卡片本身时，将激活此操作 |
|

### <a name="example-thumbnail-card"></a>示例缩略图卡片

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

### <a name="for-more-information"></a>详细信息

Bot Framework 参考：

* [缩略图卡片节点](https://docs.microsoft.com/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [缩略图卡片 C#](https://docs.microsoft.com/dotnet/api/microsoft.bot.connector.thumbnailcard?view=botbuilder-dotnet-3.0&preserve-view=true)

## <a name="card-collections"></a>卡片集合

Teams 中支持卡片集合。

卡片集合： `builder.AttachmentLayout.carousel` `builder.AttachmentLayout.list` 和 。 这些集合包含自适应、Hero 或缩略图卡片。

## <a name="carousel-collection"></a>Carousel 集合

盘 [盘布局显示](/azure/bot-service/dotnet/bot-builder-dotnet-add-rich-card-attachments?view=azure-bot-service-3.0&preserve-view=true) 卡片的盘选（可选）和关联的操作按钮。

### <a name="support-for-carousel-collections"></a>对 Carousel 集合的支持

| Teams 中的聊天机器人 | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |
|

> [!NOTE]
> 一个木马可以显示每封邮件最多 10 张卡片。

### <a name="properties-of-a-carousel-card"></a>Carousel 卡的属性

木马卡片的属性与"Hero"和"Thumbnail"卡片的属性相同。

### <a name="example-carousel-collection"></a>示例 Carousel 集合

![卡片的盘盘示例](~/assets/images/cards/carousel.png)

```json
{
 "attachmentLayout": "carousel",
 "attachments":[
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "extraLarge",
                "weight": "bolder",
                "text": "Welcome to Employee Connect",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "size": "medium",
                "weight": "bolder",
                "text": "Add events to your calendar",
                "height": "stretch"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "The bot can send \r\rnotification to remind \r\ryou about the latest \r\revents and trainings.",
                "wrap": true,
                "height": "stretch"
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.2",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee connect"
              },
              {
                "type": "TextBlock",
                "text": "The bot can send notifications \r\rto remind you about the latest \r\r events and trainings",
                "wrap": true,
                "maxWidth": 2
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              },
              {
                "type": "ColumnSet",
                "columns": [
                  {
                    "type": "Column",
                    "items": [],
                    "height": "stretch"
                  }
                ]
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    },
    {
      "contentType": "application/vnd.microsoft.card.adaptive",
      "content": {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Container",
            "items": [
              {
                "type": "TextBlock",
                "size": "large",
                "weight": "bolder",
                "text": "Employee Connect final"
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Create and manage your tasks",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "text": "The app identifies all your pending tasks \r\r and helps you manage everything at \r\r one place.",
                "wrap": true
              },
              {
                "type": "TextBlock",
                "weight": "bolder",
                "text": "Try these commands \r\r- Pending Submissions \r\r- Pending Approvals- My Tools",
                "wrap": true,
                "height": "stretch"
              }
            ]
          }
        ],
        "actions": [
          {
            "type": "Action.Submit",
            "title": "Let's get started"
          }
        ]
      }
    }
  ]
}
```

### <a name="syntax-for-carousel-collections"></a>Carousel 集合的语法

`builder.AttachmentLayoutTypes.Carousel`

## <a name="list-collection"></a>列表集合

### <a name="support-for-list-collections"></a>支持列表集合

列表布局显示垂直堆叠的卡片列表（可选）以及关联的操作按钮。

| Teams 中的聊天机器人 | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |
|

### <a name="example-list-collection"></a>示例列表集合

![卡片列表示例](~/assets/images/cards/list.png)

属性与 Hero 或缩略图卡片的属性相同。

一个列表最多可显示每封邮件 10 张卡片。

> [!NOTE]
> iOS 和 Android 上尚不支持列表卡的一些组合。

### <a name="syntax-for-list-collections"></a>List 集合的语法

`builder.AttachmentLayout.list`

## <a name="cards-not-supported-in-teams"></a>Teams 中不支持的卡片

以下卡片由 Bot Framework 实现，但不受 Teams 支持。

* 动画卡
* 音频卡
* 视频卡
