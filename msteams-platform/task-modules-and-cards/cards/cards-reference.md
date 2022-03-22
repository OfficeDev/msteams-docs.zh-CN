---
title: 卡片类型
description: 介绍 Teams 中机器人可用的所有卡片和卡片操作
ms.localizationpriority: high
keywords: 机器人卡参考
ms.topic: reference
ms.openlocfilehash: 4bd890268641de5c228f77c8b65e5e93fcf66094
ms.sourcegitcommit: f9dc32566e87ffc1b2d2bd45f1388aae8f5c9083
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/17/2022
ms.locfileid: "63558824"
---
# <a name="types-of-cards"></a>卡片类型

Microsoft Teams 机器人支持自适应、主图、列表、Office 365 连接器、收据、登录以及缩略图卡和卡片集合。 它们基于 Bot Framework 定义的卡片，但 Teams 不支持所有Bot Framework卡，而是添加了一些自己的卡。

在识别不同的卡片类型之前，请先了解如何创建主图卡、缩略图卡或自适应卡片。

## <a name="create-a-hero-card-thumbnail-card-or-adaptive-card"></a>创建主图卡、缩略图卡或自适应卡片

要从 App Studio 创建主图卡、缩略图卡或自适应卡片，请：

1. 从 Teams 转到 **App Studio**。
1. 选择 **Card 编辑器**。
1. 选择 **创建新卡**。
1. 选择 **创建** **主卡**、**缩略图卡** 或 **自适应卡片** 其中的一张卡。 显示该卡的元数据详细信息、按钮以及 json、csharp 和 node 代码示例。

    ![主卡详细信息](~/assets/images/Cards/Herocarddetails.png)

1. 选择 **向我发送此卡片**。 该卡片将作为聊天消息发送给你。

## <a name="card-examples"></a>卡片示例

可以在 Bot Builder SDK v3 的文档中找到有关如何使用卡的其他信息。 GitHub 上的 **Microsoft/BotBuilder-Samples** 存储库中也提供了代码示例。 下面是一些卡片示例:

* .NET
  * [添加卡作为邮件附件](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)。
  * [卡片示例代码 Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/06.using-cards)。

* Node.js
  * [添加卡作为邮件附件](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)。
  * [卡片示例代码 Bot Builder v4](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/06.using-cards)。

## <a name="card-types"></a>卡片类型

可以根据应用程序要求识别和使用不同类型的卡片。 下表显示了可用的卡片类型:

| 卡类型 | Description |
| --- | --- |
| [自适应卡](#adaptive-card) | 此卡片高度可自定义，可以包含文本、语音、图像、按钮和输入字段的任意组合。 |
| [主图卡](#hero-card) | 此卡通常包含单个大图像、一个或多个按钮以及少量文本。 |
| [列表卡](#list-card) | 此卡包含项的滚动列表。 |
| [Office 365 连接器卡](#office-365-connector-card) | 此卡具有具有多个分区、字段、图像和操作的灵活布局。 |
| [收据卡](#receipt-card) | 此卡片向用户提供收据。 |
| [登录卡](#signin-card) | 此卡使机器人能够请求用户登录。 |
| [缩略图卡](#thumbnail-card) | 此卡通常包含单个缩略图、一些短文本和一个或多个按钮。 |
| [卡集合](#card-collections) | 此卡集合用于在单个响应中返回多个项。 |

## <a name="features-that-support-different-card-types"></a>支持不同卡类型的功能

| 卡类型 | 机器人 | 消息扩展预览 | 消息扩展结果 | 任务模块 | 传出 webhook | 传入 webhook | Office 365 连接器 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| 自适应卡片 | ✔ | ✖ | ✔ | ✔ | ✔ | ✔ | ✖ |
| Office 365 连接器卡 | ✔ | ✖ | ✔ | ✖ | ✔ | ✔ | ✔ |
| 主图卡片 | ✔ | ✔ | ✔ | ✖ | ✔ | ✔ | ✖ |
| 缩略图卡片 | ✔ | ✔ | ✔ | ✖ | ✔ | ✔ | ✖ |
| 列表卡 | ✔ | ✖ | ✖ | ✖ | ✔ | ✔ | ✖ |
| 收据卡 | ✔ | ✖ | ✖ | ✖ | ✖ | ✔ | ✖ |
| 登录卡 | ✔ | ✖ | ✖ | ✖ | ✖ | ✖ | ✖ |

> [!NOTE]
> 对于传入 Webhook 中的自适应卡片，完全支持所有本机自适应卡片架构元素 (`Action.Submit` 除外)。 受支持的操作包括 [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html)、[**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)、[**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)和 [**Action.Execute**](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)。

## <a name="common-properties-for-all-cards"></a>所有卡片的常用属性

可以浏览一些适用于所有卡片的常见属性。

> [!NOTE]
> 具有多个操作的主图和缩略图卡会自动拆分为一个轮播布局中的多个卡片。

### <a name="inline-card-images"></a>内联卡片图像

卡片可包含内联图像，包括公开的可用映像链接。 出于性能目的，强烈建议在公共内容分发网络 (CDN) 上托管映像。

图像的大小会增加或减小，以保持覆盖图像区域的纵横比。 然后从中心裁剪图像，以实现卡的适当纵横比。

图像必须最多为 1024x1024，并采用 PNG、JPEG 或 GIF 格式。不支持动态 GIF。

下表提供内联卡图像的属性:

| 属性 | 类型  | Description |
| --- | --- | --- |
| url | URL | 图片的 HTTPS URL。 |
| alt | String | 可访问的图像说明。 |

> [!NOTE]
> 如果卡片包含在最终图像之前重定向的图像 URL，则不支持图像 URL 中的重定向。在公有云上共享的映像会出现这种情况。

### <a name="buttons"></a>按钮

按钮显示在卡片底部堆叠。 按钮文本始终位于单行上，如果文本超出按钮宽度，则会将其截断。 不显示超出卡支持的最大数值的任何其他按钮。

有关详细信息，请参阅 [卡片](~/task-modules-and-cards/cards/cards-actions.md)。

### <a name="card-formatting"></a>卡片格式

有关卡片中文本格式的详细信息，请参阅 [卡格式](~/task-modules-and-cards/cards/cards-format.md)。

标识所有卡片的通用属性后，现在可以使用自适应卡片，这有助于通过将可操作内容直接添加到所使用的应用中来提高参与度和效率。

## <a name="adaptive-card"></a>自适应卡片

自适应卡片是一种可自定义的卡片，可以包含文本、语音、图像、按钮和输入字段的任意组合。要了解详细信息，请参阅 [自适应卡片](https://github.com/microsoft/AdaptiveCards/releases/tag/2020.07)。

### <a name="support-for-adaptive-cards"></a>支持自适应卡片

下表提供了支持自适应卡片的功能:

| Teams 中的机器人 | 消息传递扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

> [!NOTE]
>
> * Teams 平台支持 v1.4 或更早版本的自适应卡片功能，适用于机器人发送的卡片和基于操作的消息传递扩展。
> * Teams 平台支持 v1.3 或更早版本的自适应卡片功能，以实现其他功能，例如用户发送的卡片 (基于搜索的消息传递扩展和链接展开)、选项卡和任务模块。
> * Teams 平台上的自适应卡片不支持积极或破坏性的操作样式。
> * Teams 平台上的自适应卡片目前不支持媒体元素。

### <a name="example-of-adaptive-card"></a>自适应卡片示例

:::image type="content" source="~/assets/images/cards/adaptivecard.png" alt-text="自适应卡片示例" border="true":::

以下代码演示自适应卡片的示例:

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

#### <a name="additional-information-on-adaptive-cards"></a>有关自适应卡片的其他信息

Bot Framework 参考:

* [自适应卡片节点](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-an-adaptive-card&preserve-view=true)
* [自适应卡 C#](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-an-adaptive-card&preserve-view=true)

要详细了解自适应卡片，请参阅 [自适应卡片](/adaptive-cards/)。

现在可以使用主图卡，这是一种多用途卡，用于直观地突出显示潜在的用户选择。

## <a name="hero-card"></a>主图卡片

通常包含单个大图像、一个或多个按钮和文本的卡片。

### <a name="support-for-hero-cards"></a>支持主图卡

下表提供了支持主图卡的功能:

| Teams 中的机器人 | 消息传递扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="properties-of-a-hero-card"></a>主图卡的属性

下表提供了主图卡的属性:

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多两行。 |
| 副标题 | 格式文本  | 卡片的副标题。 最多两行。|
| text | 格式文本  | 文本显示在副标题下。 有关格式设置选项，请参阅 [卡格式](~/task-modules-and-cards/cards/cards-format.md)。 |
| 图像 | 图像数组 | 显示在卡片顶部的图像。 纵横比为 16:9。 |
| 按钮 | 操作对象数组 | 适用于当前卡片的操作集。最大值为 6。 |
| 点击 | Action 对象 | 当用户点击卡片本身时激活。 |

### <a name="example-of-a-hero-card"></a>主图卡的示例

![主图卡的示例](~/assets/images/cards/hero.png)

以下代码显示主图卡示例:

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

### <a name="additional-information-on-hero-cards"></a>有关主图卡的其他信息

Bot Framework 参考:

* [主图卡 Node.js](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=javascript#send-a-hero-card&preserve-view=true)
* [主图卡 C#](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-hero-card&preserve-view=true)

## <a name="list-card"></a>列表卡

Teams 已添加列表卡片，以提供超出列表集合可提供的功能。 列表卡提供项的滚动列表。

### <a name="support-for-list-cards"></a>支持列表卡

下表提供了支持列表卡的功能:

| Teams 中的机器人 | 消息传递扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ |✔ |

### <a name="properties-of-a-list-card"></a>列表卡的属性

下表提供了列表卡的属性:

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多 2 行。|
| items | 列表项的数组 | 适用于卡片的项集。|
| 按钮 | 操作对象数组 | 适用于当前卡片的操作集。最大值为 6。 |

### <a name="example-of-a-list-card"></a>列表卡的示例

以下代码显示列表卡示例:

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

可以使用 Office 365 连接器卡片来工作，该卡片提供灵活的布局，是获取有用信息的好方法。 Teams 中支持 Office 365 连接器卡，而不支持 Bot Framework。 此卡片提供具有多个分区、字段、图像和操作的灵活布局。 此卡包含连接器卡，以便机器人可以使用它。 有关连接器卡与 Office 365 连接器卡之间的区别，请参阅 [office 365 连接器卡上的其他信息](#additional-information-on-the-office-365-connector-card)。

### <a name="support-for-office-365-connector-cards"></a>对 Office 365 连接器卡的支持

下表提供了支持 Office 365 连接器卡的功能:

| Teams 中的机器人 | 消息传递扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✔ | ✖ |

### <a name="properties-of-the-office-365-connector-card"></a>Office 365 连接器卡的属性

下表提供了 Office 365 连接器卡的属性:

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多两行。 |
| 摘要 | 格式文本  | 卡片摘要。 最多两行。 |
| text | 格式文本  | 文本显示在副标题下。 有关格式设置选项，请参阅 [卡格式](~/task-modules-and-cards/cards/cards-format.md)。 |
| themeColor | HEX 字符串 | 替代应用程序清单中提供的 `accentColor` 颜色。 |

### <a name="additional-information-on-the-office-365-connector-card"></a>Office 365 连接器卡上的其他信息

Office 365 连接器卡在 Microsoft Teams 中正常工作，包括[`ActionCard`操作](/outlook/actionable-messages/card-reference#actioncard-action)。

从连接器使用连接器卡和在机器人中使用连接器卡之间的重要区别在于卡片操作的处理。下表列出了区别：

| Connector | Bot |
| --- | --- |
| 终结点通过 HTTP POST 接收卡有效负载。 | `HttpPOST` 操作触发仅向机器人发送操作 ID 和主体的 `invoke` 活动。|

每个连接器卡最多可以显示 10 个分区，每个部分最多可以包含五个图像和五个操作。

> [!NOTE]
> 消息中不会显示任何其他部分、图像或操作。

所有文本字段都支持 Markdown 和 HTML。 可以通过在消息中设置属性来控制哪些节使用 Markdown 或 `markdown` HTML。 默认情况下，`markdown` 设置为 `true`。 若要改用 HTML，请将 `markdown` 设置为 `false`。

如果指定 `themeColor` 属性，它将替代应用清单中的 `accentColor` 属性。

若要指定 `activityImage` 的呈现样式，可以如下表所示设置 `activityImageType`:

| 值 | Description |
| --- | --- |
| `avatar` | 默认情况下， 将将 `activityImage`裁剪为圆圈。 |
| `article` | `activityImage` 显示为矩形并保留其纵横比。 |

有关连接器卡属性的所有其他详细信息，请参阅 [可操作信息卡参考](/outlook/actionable-messages/card-reference)。 Teams 当前不支持的唯一连接器卡属性如下所示:

* `heroImage`
* `hideOriginalBody`
* `startGroup` 在 Teams 中总视为 `true`
* `originator`
* `correlationId`

### <a name="example-of-an-office-365-connector-card"></a>Office 365 连接器卡的示例

以下代码演示 Office 365 连接器卡片的示例:

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

Teams 支持收据卡。 它是使机器人能够向用户提供收据的卡片。 它通常包含收据上要包含的项目列表，例如税务和总信息。

### <a name="support-for-receipt-cards"></a>支持收据卡

下表提供了支持收据片的功能:

| Teams 中的机器人 | 消息传递扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

### <a name="example-of-a-receipt-card"></a>收据卡的示例

![收据卡的示例](~/assets/images/cards/receipt.png)

以下代码显示收据卡示例:

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

### <a name="additional-information-on-receipt-cards"></a>有关收据卡的其他信息

Bot Framework 参考:

* [收据卡 Node.js](/javascript/api/botframework-schema/receiptcard?view=botbuilder-ts-latest&preserve-view=true)
* [收据卡 C#](/dotnet/api/microsoft.bot.schema.receiptcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="signin-card"></a>登录卡

Teams 中的登录卡类似于 Bot Framework 中的登录卡，只不过 Teams 中的登录卡仅支持两个操作 `signin` 和 `openUrl`。

登录操作可以从 Teams 中的任何卡中使用，而不仅仅是登录卡。 有关详细信息，请参阅 [机器人的 Teams 身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)。

### <a name="support-for-signin-cards"></a>支持登录卡

下表提供了支持登录卡的功能:

| Teams 中的机器人 | 消息传递扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

### <a name="additional-information-on-signin-cards"></a>有关登录卡的其他信息

Bot Framework 参考:

* [登录卡 Node.js](/javascript/api/botframework-schema/signincard?view=botbuilder-ts-latest&preserve-view=true)
* [登录卡 C#](/dotnet/api/microsoft.bot.schema.signincard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="thumbnail-card"></a>缩略图卡片

可以使用用于发送简单可操作消息的缩略图卡。 通常包含单个缩略图、一个或多个按钮和文本的卡片。

### <a name="support-for-thumbnail-cards"></a>支持缩略图卡

下表提供了支持缩略卡的功能:

| Teams 中的机器人 | 消息传递扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

![缩略图卡示例](~/assets/images/cards/thumbnail.png)

### <a name="properties-of-a-thumbnail-card"></a>缩略图卡的属性

下表提供了缩略图卡的属性:

| 属性 | 类型  | 说明 |
| --- | --- | --- |
| title | 格式文本  | 卡片的标题。 最多 2 行。|
| 副标题 | 格式文本  | 卡片的副标题。 最多 2 行。|
| text | 格式文本  | 文本显示在副标题下。 有关格式设置选项，请参阅 [卡格式](~/task-modules-and-cards/cards/cards-format.md)。 |
| 图像 | 图像数组 | 显示在卡片顶部的图像。 纵横比 1:1 正方形。 |
| 按钮 | 操作对象数组 | 适用于当前卡片的操作集。最大值为 6。 |
| 点击 | Action 对象 | 当用户点击卡片本身时激活。 |

### <a name="example-of-a-thumbnail-card"></a>缩略图卡示例

以下代码演示缩略图卡片的示例:

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

Bot Framework 参考:

* [缩略图卡 Node.js](/javascript/api/botframework-schema/thumbnailcard?view=botbuilder-ts-latest&preserve-view=true)
* [缩略图卡 C#](/dotnet/api/microsoft.bot.schema.thumbnailcard?view=botbuilder-dotnet-stable&preserve-view=true)

## <a name="card-collections"></a>卡片集合

可以使用包含轮播和列表集合的卡片集合。 Teams 支持卡片集合。 卡片集合包括 `builder.AttachmentLayout.carousel` 和 `builder.AttachmentLayout.list`。 这些集合包含自适应卡、主图或缩略图卡。

### <a name="carousel-collection"></a>轮播集合

[轮播布局](/azure/bot-service/bot-builder-howto-add-media-attachments?view=azure-bot-service-4.0&tabs=csharp#send-a-carousel-of-cards&preserve-view=true) 显示卡片的轮播，可以选择有相关操作的按钮。

#### <a name="support-for-carousel-collections"></a>支持轮播集合

下表提供了支持轮播集合的功能:

| Teams 中的机器人 | 消息传递扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✖ | ✖ | ✔ |

> [!NOTE]
> 轮播每封邮件最多可显示十张卡片。

#### <a name="properties-of-a-carousel-card"></a>轮播卡的属性

轮播卡的属性与主图和缩略图卡相同。

#### <a name="example-of-a-carousel-collection"></a>轮播集合的示例

![卡片的轮播示例](~/assets/images/cards/carousel.png)

下面的代码演示轮播集合的示例:

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

#### <a name="syntax-for-carousel-collections"></a>轮播集合的语法

`builder.AttachmentLayoutTypes.Carousel` 是轮播集合的语法。

### <a name="list-collection"></a>列表集合

列表布局显示一个垂直堆积的卡片列表，可选择使用关联的操作按钮。

#### <a name="support-for-list-collections"></a>支持列表集合

下表提供了支持列表集合的功能:

| Teams 中的机器人 | 消息传递扩展  | 连接器 | 机器人框架 |
| --- | --- | --- | --- |
| ✔ | ✔ | ✖ | ✔ |

#### <a name="example-of-a-list-collection"></a>列表集合示例

![卡片列表示例](~/assets/images/cards/list.png)

列表集合的属性与主图或缩略图卡相同。

列表每封邮件最多可显示十张卡片。

> [!NOTE]
> iOS 和 Android 尚不支持列表卡的某些组合。

#### <a name="syntax-for-list-collections"></a>列表集合的语法

`builder.AttachmentLayout.list` 是列表集合的语法。

## <a name="cards-not-supported-in-teams"></a>Teams 中不支持卡片

以下卡由 Bot Framework 实现，但不受 Teams 支持:

* 动画卡片
* 音频卡片
* 视频卡片

## <a name="see-also"></a>另请参阅

* [任务模块](~/task-modules-and-cards/what-are-task-modules.md)
* [格式卡](~/task-modules-and-cards/cards/cards-format.md)
* [最新卡片](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/up-to-date-views.md)
* [使用自适应卡的通用操作](~/task-modules-and-cards/cards/universal-actions-for-adaptive-cards/work-with-universal-actions-for-adaptive-cards.md)
* [表单完成反馈](~/bots/how-to/conversations/conversation-messages.md#form-completion-feedback)
