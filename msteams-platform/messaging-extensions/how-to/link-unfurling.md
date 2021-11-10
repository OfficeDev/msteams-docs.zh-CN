---
title: 链接展开
author: surbhigupta
description: 了解如何使用应用清单或手动使用代码示例和示例在 Microsoft Teams 应用中添加与消息传递扩展取消链接。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f702ac2600dbfb3c8fd2992c41cc1c72754252ca
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889396"
---
# <a name="link-unfurling"></a>链接展开

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

本文档指导你如何使用 App studio 和手动将链接取消点击添加到应用清单。 通过链接取消链接，当特定域的 URL 粘贴到撰写邮件区域中时，你的应用可以注册以接收 `invoke` 活动。 包含粘贴到撰写邮件区域中的完整 URL，您可以使用用户可取消展开的卡片进行响应，从而 `invoke` 提供其他信息或操作。 这类似于 URL 用作搜索词的搜索命令。

> [!NOTE]
> * 目前，移动客户端不支持链接取消展开。
> * 链接取消点击结果缓存 30 分钟。

邮件Azure DevOps扩展使用链接取消链接查找粘贴到指向工作项的撰写邮件区域中的 URL。 在下图中，用户粘贴了邮件扩展已解析为Azure DevOps中工作项的 URL：

![链接取消链接示例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>向应用清单添加链接取消链接

若要向应用清单添加链接取消链接，请向应用清单 JSON 的 部分 `messageHandlers` `composeExtensions` 添加新数组。 可以在 App Studio 的帮助下或手动添加数组。 域列表可以包含通配符，例如 `*.example.com` 。 这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。

> [!NOTE]
> 不要直接添加或通过通配符添加不在控件中的域。 例如， `yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。 此外，还禁止顶级域。 例如 `*.com` ，、 `*.org` 。

### <a name="add-link-unfurling-using-app-studio"></a>使用 App Studio 添加链接取消链接

1. 从 **客户端** 打开 App Studio Microsoft Teams，然后选择"**清单编辑器"** 选项卡。
1. 加载应用清单。
1. 在 **"消息扩展** "页上，在"邮件处理程序"部分添加 **要查找的** 域。 下图说明了此过程：

    ![App Studio 中的邮件处理程序部分](~/assets/images/link-unfurling.png)
    
### <a name="add-link-unfurling-manually"></a>手动添加链接取消链接

若要使邮件扩展能够与链接进行交互，首先必须将 `messageHandlers` 数组添加到应用清单。 以下示例说明如何手动添加链接取消链接： 


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

有关完整的清单示例，请参阅 [清单参考](~/resources/schema/manifest-schema.md)。

## <a name="handle-the-composeextensionquerylink-invoke"></a>处理 `composeExtension/queryLink` 调用

将域添加到应用程序清单后，必须更新 Web 服务代码以处理调用请求。 使用收到的 URL 搜索服务并创建卡片响应。 如果使用多张卡片进行响应，则仅使用第一个卡片响应。

支持以下卡片类型：

* [缩略图卡片](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Hero card](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

可以使用自适应卡片或连接器Office 365预览属性在结果列表中显示该卡片的预览。 如果结果已是 Hero 或 Thumbnail 卡片，则不需要预览属性。 如果使用预览附件，它必须是 Hero 或 Thumbnail 卡片。 如果未指定任何预览属性，则卡片预览将失败，并且不显示任何内容。

### <a name="example"></a>示例

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsAppBasedLinkQueryAsync(ITurnContext<IInvokeActivity> turnContext, AppBasedLinkQuery query, CancellationToken cancellationToken)
{
    //You'll use the query.link value to search your service and create a card response
    var card = new HeroCard
    {
        Title = "Hero Card",
        Text = query.Url,
        Images = new List<CardImage> { new CardImage("https://raw.githubusercontent.com/microsoft/botframework-sdk/master/icon.png") },
    };

    var attachments = new MessagingExtensionAttachment(HeroCard.ContentType, null, card);
    var result = new MessagingExtensionResult(AttachmentLayoutTypes.List, "result", new[] { attachments }, null, "test unfurl");

    return new MessagingExtensionResponse(result);
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

下面是发送到 `invoke` 自动程序的示例：

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

下面是一个响应示例：

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
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
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

## <a name="see-also"></a>另请参阅 

* [卡片](~/task-modules-and-cards/what-are-cards.md)
* [选项卡链接展开和阶段视图](~/tabs/tabs-link-unfurling.md)
