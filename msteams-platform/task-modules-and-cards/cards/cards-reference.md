---
title: 卡片类型
description: 介绍自动程序可用的所有卡片和卡片Teams
ms.localizationpriority: medium
keywords: 机器人卡参考
ms.topic: reference
ms.openlocfilehash: 2768b1b156ecd86a6bcc2a7b8b42448db3eeeaae
ms.sourcegitcommit: 8feddafb51b2a1a85d04e37568b2861287f982d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2021
ms.locfileid: "59475592"
---
# <a name="types-of-cards"></a>卡片类型

自动程序支持自适应、Office 365、列表、Office 365 连接器、收据、登录以及缩略图卡和卡片Microsoft Teams。 它们基于 Bot Framework 定义的卡，Teams不支持所有 Bot Framework 卡，并且添加了一些自己的卡。

确定不同的卡片类型之前，请了解如何创建 Hero 卡片、缩略图卡片或自适应卡片。

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a>创建 Hero 卡片、缩略图卡或自适应卡片

**从 App Studio 创建 Hero 卡片、缩略图卡片或自适应卡片**

1. 从应用商店 **转到 App Studio** Teams。
1. 选择 **"卡片编辑器"。**
1. 选择 **创建新卡片**。
1. 从 **Hero Card、Thumbnail** **Card** 或 **Adaptive** Card 中选择其中一张卡片 **的"创建"。** 显示该卡片的元数据详细信息、按钮以及 json、csharp 和节点代码示例。

    ![Hero card details](~/assets/images/Cards/Herocarddetails.png)

1. 选择 **"将此卡发送给我"。** 该卡片作为聊天消息发送给您。

## <a name="card-examples"></a>卡片示例

有关如何使用卡的其他信息，请参阅 Bot Builder SDK v3 的文档。 代码示例也可在 **Microsoft/BotBuilder-Samples** 存储库上GitHub。 以下是一些卡片示例：

* .NET
  * [将卡片添加为邮件的附件](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)。
  * [卡片示例代码自动程序生成器 v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards)。

* Node.js
  * [将卡片添加为邮件的附件](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)。
  * [卡片示例代码自动程序生成器 v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards)。

## <a name="card-types"></a>卡片类型

你可以根据应用程序要求标识和使用不同类型的卡片。 下表显示了可供你使用卡片的类型：

| 卡片类型 | 说明 |
| --- | --- |
| [自适应卡片](#adaptive-card) | 此卡片可高度自定义，可以包含文本、语音、图像、按钮和输入字段的任意组合。 |
| [Hero card](#hero-card) | 此卡片通常包含一个大图像、一个或多个按钮和少量文本。 |
| [列表卡](#list-card) | 此卡片包含项目的滚动列表。 |
| [Office 365连接器卡](#office-365-connector-card) | 此卡片具有具有多个分区、字段、图像和操作的灵活性布局。 |
| [收据卡](#receipt-card) | 此卡为用户提供收据。 |
| [登录卡](#signin-card) | 此卡使机器人可以请求用户登录。 |
| [缩略图卡片](#thumbnail-card) | 此卡片通常包含一个缩略图图像、一些短文本以及一个或多个按钮。 |
| [卡片集合](#card-collections) | 此卡片集合用于在单个响应中返回多个项目。 |

## <a name="features-that-support-different-card-types"></a>支持不同卡片类型的功能

| 卡片类型 | 机器人 | 邮件扩展预览 | 邮件扩展结果 | 任务模块 | 传出 Webhook | 传入 Webhook | Office 365 连接器 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 自适应卡片 | ✔ | ✖ | ✔ | ✔ | ✔ | ✔ | ✖ |
| Office 365连接器卡 | ✔ | ✖ | ✔ | ✖ | ✔ | ✔ | ✔ |
| Hero card | ✔ | ✔ | ✔ | ✖ | ✔ | ✔ | ✖ |
| 缩略图卡片 | ✔ | ✔ | ✔ | ✖ | ✔ | ✔ | ✖ |
| 列表卡 | ✔ | ✖ | ✖ | ✖ | ✔ | ✔ | ✖ |
| 收据卡 | ✔ | ✖ | ✖ | ✖ | ✖ | ✔ | ✖ |
| 登录卡 | ✔ | ✖ | ✖ | ✖ | ✖ | ✖ | ✖ |

> [!NOTE]
> 对于传入 Webhook 中的自适应卡片，完全支持除 以外的所有本机自适应 `Action.Submit` 卡片架构元素。 支持的操作包括 Action.OpenURL、Action.ShowCard、Action.ToggleVisibility 和 [**Action.Execute。**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute) [](https://adaptivecards.io/explorer/Action.OpenUrl.html) [](https://adaptivecards.io/explorer/Action.ShowCard.html) [](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)

## <a name="common-properties-for-all-cards"></a>所有卡片的常见属性

你可以浏览一些适用于所有卡片的常见属性。

> [!NOTE]
> 具有多个操作的 Hero 和缩略图卡片会自动拆分为多个卡片，在一个木马布局中。

### <a name="inline-card-images"></a>内联卡片图像

卡片可以包含内联图像，包括指向公开可用图像的链接。 出于性能目的，强烈建议你将映像托管在公用内容分发网络 (CDN) 。

图像的大小会向上或向下扩展，以保持覆盖图像区的纵横比。 然后从中心裁剪图像，以实现卡片的适当纵横比。

图像必须最多为 1024×1024 和 PNG、JPEG 或 GIF 格式。 不支持动态 GIF。

下表提供了内联卡片图像的属性：

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| url | URL | 图像的 HTTPS URL。 |
| alt | String | 图像的辅助说明。 |

> [!NOTE]
> 如果卡片包含的图像 URL 在最终图像之前重定向，则不支持图像 URL 中的重定向。 对于在公有云上共享的图像，会出现此情况。

### <a name="buttons"></a>按钮

按钮显示在卡片底部堆叠。 按钮文本始终位于单行，如果文本超过按钮宽度，则将被截断。 不会显示超过卡支持的最大数目的其他任何按钮。

有关详细信息，请参阅 [卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。

### <a name="card-formatting"></a>卡片格式

有关卡片中的文本格式设置详细信息，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。

确定所有卡片的常见属性后，你现在可以使用自适应卡片，这可通过将可操作内容直接添加到你使用的应用来帮助你提高参与度和效率。

## <a name="adaptive-card"></a>自适应卡片

> [!VIDEO https://www.youtube-nocookie.com/embed/J12lKt717Ws]

自适应卡片是可自定义的卡片，可以包含文本、语音、图像、按钮和输入字段的任意组合。 有关详细信息，请参阅自适应 [卡片](https://github.com/microsoft/AdaptiveCards/releases/tag/2020.07)。

### <a name="support-for-adaptive-cards"></a>自适应卡片支持

下表提供支持自适应卡片的功能：

| 聊天机器人Teams | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

> [!NOTE]
> * Teams平台支持 v1.4 或更早的自适应卡片功能，适用于机器人发送的卡和基于操作的消息扩展。
> * Teams平台支持 v1.3 或更早的自适应卡片功能用于其他功能，例如用户 (基于搜索的消息扩展发送的卡片以及取消展开) 、选项卡和任务模块的链接。
> * 在游戏平台上的自适应卡片中不支持正面或破坏性Teams样式。
> * 媒体元素当前在应用平台上的自适应卡片Teams支持。

### <a name="example-of-adaptive-card"></a>自适应卡片示例

![自适应卡片示例](~/assets/images/cards/adaptivecard.png)

以下代码显示了自适应卡片的示例：

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

#### <a name="additional-information-on-adaptive-cards"></a>自适应卡片的其他信息

Bot Framework 参考：

* [自适应卡片节点](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [自适应卡片 C#](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

你现在可以使用一张 Hero 卡片，这是一种用于直观突出显示潜在用户选择的多用途卡片。

## <a name="hero-card"></a>Hero card

通常包含单个大图像、一个或多个按钮和文本的卡片。

### <a name="support-for-hero-cards"></a>支持人物卡片

下表提供了支持人物卡片的功能：

| 聊天机器人Teams | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="properties-of-a-hero-card"></a>Hero 卡片的属性

下表提供 Hero 卡片的属性：

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多两行。 |
| subtitle | 格式文本  | 卡片的副标题。 最多两行。|
| text | 格式文本  | 文本显示在副标题下。 有关格式设置选项，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。 |
| images | 图像数组 | 显示在卡片顶部的图像。 纵横比 16：9。 |
| 按钮 | 操作对象数组 | 适用于当前卡片的操作集。 最多六个。 |
| 点击 | Action 对象 | 当用户点击卡片本身时激活。 |

### <a name="example-of-a-hero-card"></a>Hero 卡片示例

![Hero 卡片示例](~/assets/images/cards/hero.png)

以下代码显示了一个展示卡片的示例：

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

### <a name="additional-information-on-hero-cards"></a>有关 hero cards 的其他信息

Bot Framework 参考：

* [Hero card Node.js](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [Hero card C#](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a>列表卡

列表卡片已由列表Teams，以提供列表集合可以提供的功能之外的功能。 列表卡片提供项的滚动列表。

### <a name="support-for-list-cards"></a>支持列表卡

下表提供了支持列表卡片的功能：

| 聊天机器人Teams | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |

### <a name="properties-of-a-list-card"></a>列表卡片的属性

下表提供列表卡片的属性：

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多 2 行。|
| items | 列表项数组 | 适用于卡片的项目集。|
| 按钮 | 操作对象数组 | 适用于当前卡片的操作集。 最大值 6。 |

### <a name="example-of-a-list-card"></a>列表卡片示例

以下代码显示了列表卡片的示例：

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

## <a name="office-365-connector-card"></a>Office 365连接器卡

可以使用一个Office 365连接器卡，该卡提供灵活的布局，是获取有用信息的一种很好的方法。 自动Office 365支持自动Teams，而不是 Bot 框架。 此卡片提供具有多个分区、字段、图像和操作的灵活性布局。 此卡包含连接器卡，以便机器人可以使用它。 有关连接器卡和 Office 365 连接器卡之间的差异，请参阅连接器Office 365[卡上的其他信息](#additional-information-on-the-office-365-connector-card)。

### <a name="support-for-office-365-connector-cards"></a>支持 Office 365 连接器卡

下表提供了支持连接器Office 365的功能：

| 聊天机器人Teams | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |

### <a name="properties-of-the-office-365-connector-card"></a>连接器Office 365的属性

下表提供了连接器卡Office 365属性：

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多两行。 |
| 摘要 | 格式文本  | 卡片摘要。 最多两行。 |
| text | 格式文本  | 文本显示在副标题下。 有关格式设置选项，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。 |
| themeColor | 十六进制字符串 | 替代应用程序清单 `accentColor` 中提供的颜色。 |

### <a name="additional-information-on-the-office-365-connector-card"></a>连接器卡上Office 365信息

Office 365连接器卡在连接器中Microsoft Teams，包括[ `ActionCard` 操作](/outlook/actionable-messages/card-reference#actioncard-action)。

在机器人中从连接器使用连接器卡和使用连接器卡之间的重要区别是处理卡操作。 下表列出了差异：

| Connector | Bot |
| --- | --- |
| 终结点通过 HTTP POST 接收卡有效负载。 | `HttpPOST`该操作将触发 `invoke` 仅向自动程序发送操作 ID 和正文的活动。|

每个连接器卡最多可以显示 10 个部分，每个部分最多可以包含 5 个图像和 5 个操作。

> [!NOTE]
> 邮件中不显示任何其他节、图像或操作。

所有文本字段都支持 Markdown 和 HTML。 您可以通过在邮件中设置 属性来控制哪些部分使用 Markdown `markdown` 或 HTML。 默认情况下， `markdown` 设置为 `true` 。 如果要改为使用 HTML，请设置为 `markdown` `false` 。

如果指定 `themeColor` 属性，它将替代 `accentColor` 应用清单中的 属性。

若要指定 的呈现样式 `activityImage` ，可以如下 `activityImageType` 表所示进行设置：

| 值 | 说明 |
| --- | --- |
| `avatar` | 默认值 `activityImage` ，裁剪为圆形。 |
| `article` | `activityImage` 显示为矩形并保留其纵横比。 |

有关连接器卡属性的所有其他详细信息，请参阅 [可操作邮件卡参考](/outlook/actionable-messages/card-reference)。 当前不支持的唯Teams连接器卡属性如下所示：

* `heroImage`
* `hideOriginalBody`
* `startGroup`始终视为 `true` 在Teams
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a>连接器Office 365示例

以下代码显示连接器Office 365示例：

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

Teams支持收据卡。 它是使机器人能够为用户提供收据的卡片。 它通常包含要包含在收据上的项目列表，如税务和总信息。

### <a name="support-for-receipt-cards"></a>支持收据卡

下表提供了支持收据卡的功能：

| 聊天机器人Teams | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-receipt-card"></a>收据卡示例

![收据卡示例](~/assets/images/cards/receipt.png)

以下代码显示收据卡的示例：

```json
{
  "contentType": "application/vnd.microsoft.card.receipt",
  "content": {
    "title": "John Doe",
    "facts": [
      {
        "key": "Order Number",
        "value": "1234"
      },
      {
        "key": "Payment Method",
        "value": "VISA 5555-****"
      }
    ],
    "items": [
      {
        "title": "Data Transfer",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/traffic-manager.png"
        },
        "price": "$ 38.45",
        "quantity": "368"
      },
      {
        "title": "App Service",
        "image": {
          "url": "https://github.com/amido/azure-vector-icons/raw/master/renders/cloud-service.png"
        },
        "price": "$ 45.00",
        "quantity": "720"
      }
    ],
    "total": "$ 90.95",
    "tax": "$ 7.50",
    "buttons": [
      {
        "type": "openUrl",
        "title": "More information",
        "image": "https://account.windowsazure.com/content/6.10.1.38-.8225.160809-1618/aux-pre/images/offer-icon-freetrial.png",
        "value": "https://azure.microsoft.com/en-us/pricing/"
      }
    ]
  }
}
```

### <a name="additional-information-on-receipt-cards"></a>收据卡上的其他信息

Bot Framework 参考：

* [收据卡Node.js](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [收据卡 C#](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a>登录卡

自动Teams中的登录卡类似于 Bot 框架中的登录卡，只不过 Teams 中的登录卡仅支持两个 `signin` 操作 `openUrl` 和 。

The signin action can be used from any card in Teams， not just the signin card. 有关详细信息，请参阅自动[Teams的身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)。

### <a name="support-for-signin-cards"></a>支持登录卡

下表提供了支持登录卡的功能：

| 聊天机器人Teams | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

### <a name="additional-information-on-signin-cards"></a>登录卡的其他信息

Bot Framework 参考：

* [登录卡Node.js](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [登录卡 C#](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a>缩略图卡片

可以使用用于发送简单的可操作邮件的缩略图卡。 通常包含单个缩略图图像、一个或多个按钮和文本的卡片。

### <a name="support-for-thumbnail-cards"></a>对缩略图卡的支持

下表提供了支持缩略图卡的功能：

| 聊天机器人Teams | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

![缩略图卡片示例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>缩略图卡片的属性

下表提供缩略图卡片的属性：

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多 2 行。|
| subtitle | 格式文本  | 卡片的副标题。 最多 2 行。|
| text | 格式文本  | 文本显示在副标题下。 有关格式设置选项，请参阅 [卡片格式](~/task-modules-and-cards/cards/cards-format.md)。 |
| images | 图像数组 | 显示在卡片顶部的图像。 纵横比 1：1 正方形。 |
| 按钮 | 操作对象数组 | 适用于当前卡片的操作集。 最大值 6。 |
| 点击 | Action 对象 | 当用户点击卡片本身时激活。 |

### <a name="example-of-a-thumbnail-card"></a>缩略图卡片示例

以下代码显示了缩略图卡片的示例：

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

### <a name="additional-information"></a>其他信息

Bot Framework 参考：

* [缩略图卡片Node.js](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [缩略图卡片 C#](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a>卡片集合

可以使用包括木马和列表集合的卡片集合。 Teams支持卡片集合。 卡片集合包括 `builder.AttachmentLayout.carousel` `builder.AttachmentLayout.list` 和 。 这些集合包含自适应、hero 或缩略图卡片。

### <a name="carousel-collection"></a>Carousel 集合

盘 [选布局](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) 显示卡片的盘选（可选）以及关联的操作按钮。

#### <a name="support-for-carousel-collections"></a>支持木马集合

下表提供了支持盘车集合的功能：

| 聊天机器人Teams | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

> [!NOTE]
> 一个盘式消息最多可显示每封邮件 10 张卡片。

#### <a name="properties-of-a-carousel-card"></a>单盘式卡片的属性

单盘式播放卡片的属性与 hero 和 thumbnail 卡片相同。

#### <a name="example-of-a-carousel-collection"></a>一个木马集合的示例

![卡片的盘点示例](~/assets/images/cards/carousel.png)

以下代码显示了一个可进行盘车操作的集合示例：

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

#### <a name="syntax-for-carousel-collections"></a>盘车集合的语法

`builder.AttachmentLayoutTypes.Carousel` 是木马集合的语法。

### <a name="list-collection"></a>列表集合

列表布局显示卡片的垂直堆叠列表（可选）以及关联的操作按钮。

#### <a name="support-for-list-collections"></a>支持列表集合

下表提供了支持列表集合的功能：

| 聊天机器人Teams | 消息扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

#### <a name="example-of-a-list-collection"></a>列表集合的示例

![卡片列表示例](~/assets/images/cards/list.png)

列表集合的属性与 hero 或 thumbnail 卡片相同。

列表最多可显示每封邮件 10 张卡片。

> [!NOTE]
> iOS 和 Android 上尚不支持列表卡的一些组合。

#### <a name="syntax-for-list-collections"></a>列表集合的语法

`builder.AttachmentLayout.list` 是列表集合的语法。

## <a name="cards-not-supported-in-teams"></a>不支持的Teams

以下卡片由 Bot Framework 实现，但不受自动程序Teams：

* 动画卡
* 音频卡
* 视频卡

## <a name="see-also"></a>另请参阅

* [任务模块](~/task-modules-and-cards/what-are-task-modules.md)
* [格式化卡片](~/task-modules-and-cards/cards/cards-format.md)
