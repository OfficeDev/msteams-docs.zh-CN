---
title: 链接 unfurling
author: clearab
description: 如何在 Microsoft 团队应用中使用邮件扩展功能执行链接 unfurling。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 5b20ea303a2c3d085651a53b01af4bb449d386de
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673495"
---
# <a name="link-unfurling"></a>链接 unfurling

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

通过链接 unfurling 如果将特定域的 Url 粘贴`invoke`到撰写邮件区域中，应用可以注册接收活动。 `invoke`将包含粘贴到撰写邮件区域中的完整 URL，您可以使用用户可以*unfurl*的卡片进行响应，并提供其他信息或操作。 此操作的工作方式与[搜索命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)非常相似，URL 充当搜索词。

Azure DevOps 消息扩展使用 link unfurling 查找粘贴到指向工作项的撰写邮件区域中的 Url。 在下面的屏幕截图中，用户已将 Azure DevOps 中的工作项的 URL 粘贴到邮件扩展已解析为卡片。

![Link unfurling 的示例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>向您的应用程序清单添加链接 unfurling

为此，您需要将新`messageHandlers`的数组添加到`composeExtensions`应用程序清单 JSON 的部分。 您可以使用应用程序 Studio 的帮助或手动执行此操作。 例如`*.example.com`，域列表可以包含通配符。 这与域的一段完全匹配;如果需要匹配`a.b.example.com` ，请使用`*.*.example.com`。

### <a name="using-app-studio"></a>使用应用程序 Studio

1. 在应用程序 Studio 中，在 "清单编辑器" 选项卡上，加载您的应用程序清单。
1. 在 "**邮件扩展**" 页上，在 "**邮件处理程序**" 部分添加要查找的域，如下面的屏幕截图所示。

![应用程序 Studio 中的 "邮件处理程序" 部分](~/assets/images/link-unfurling.png)

### <a name="manually"></a>手动

若要使您的邮件扩展能够与链接进行交互，这种方法首先需要`messageHandlers`将该数组添加到应用程序清单中，如以下示例中所示。 本示例不是完整的清单，请参阅[清单参考](~/resources/schema/manifest-schema.md)，了解完整的清单示例。

```json
...
"composeExtensions": [
  {
    "botId": "abc123456-ab12-ab12-ab12-abcdef123456",
    "messageHandlers": [
      {
        "type": "link",
        "value": {
          "domains": [
            "*.trackeddomain.com"
          ]
        }
      }
    ]
  }
],
...
```

## <a name="handle-the-composeextensionquerylink-invoke"></a>处理`composeExtension/queryLink`调用

在添加了要侦听应用程序清单的域之后，您需要更新 web 服务代码以处理调用请求。 使用您收到的 URL 搜索您的服务并创建卡片响应。 如果使用多个卡进行响应，将仅使用第一个。

我们支持以下卡类型：

* [缩略图卡片](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [英雄卡片](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

有关概述，请参阅[什么是卡片](~/task-modules-and-cards/what-are-cards.md)。

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsAppBasedLinkQueryAsync(ITurnContext<IInvokeActivity> turnContext, AppBasedLinkQuery query, CancellationToken cancellationToken)
{
    //You'll use the query.link value to search your service and create a card response
    var heroCard = new ThumbnailCard
    {
        Title = "Thumbnail Card",
        Text = query.Url,
        Images = new List<CardImage> { new CardImage("https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png") },
    };

    var attachments = new MessagingExtensionAttachment(HeroCard.ContentType, null, heroCard);
    var result = new MessagingExtensionResult(AttachmentLayoutTypes.List, "result", new[] { attachments }, null, "test unfurl");

    return new MessagingExtensionResponse(result);
}
```

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node.js](#tab/javascript)

```javascript
class TeamsLinkUnfurlingBot extends TeamsActivityHandler {
  handleTeamsAppBasedLinkQuery(context, query) {
    const attachment = CardFactory.thumbnailCard('Thumbnail Card',
      query.url,
      ['https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png']);

    const result = {
      attachmentLayout: 'list',
      type: 'result',
      attachments: [attachment]
    };

    const response = {
      composeExtension: result
    };
    return response;
  }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

这是`invoke`发送到你的 bot 的一个示例。

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

响应的示例如下所示。

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "attachments": [
      {
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        }
      }
    ]
  }
}
```

* * *
