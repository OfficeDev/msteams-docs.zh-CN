---
title: 链接展开
author: surbhigupta
description: 了解如何使用应用清单或手动使用代码示例和示例，在Microsoft Teams应用中添加与消息扩展展开的链接。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 2dee02545a522b202e9cc695f7099848269e8944
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104404"
---
# <a name="link-unfurling"></a>链接展开

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

本文档介绍如何使用 App Studio 和手动向应用清单添加链接。 通过链接展开，应用可以在将具有特定域的 URL 粘贴到撰写消息区域时注册以接收 `invoke` 活动。 包含 `invoke` 粘贴到撰写消息区域的完整 URL，你可以使用用户可以展开的卡片进行响应，从而提供其他信息或操作。 这类似于搜索命令，其中 URL 充当搜索词。

> [!NOTE]
>
> * 目前，移动客户端不支持链接展开。
> * 链接展开结果缓存 30 分钟。

Azure DevOps消息扩展使用链接展开来查找粘贴到指向工作项的撰写消息区域中的 URL。 在下图中，用户粘贴了Azure DevOps中工作项的 URL，消息扩展已解析为卡片：

![链接展开示例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>将链接展开添加到应用清单

若要将链接展开添加到应用清单，请将新 `messageHandlers` 数组添加到 `composeExtensions` 应用清单 JSON 部分。 可以借助 App Studio 或手动添加数组。 例如 `*.example.com`，域列表可以包括通配符。 这完全匹配域的一个段;如果需要匹配 `a.b.example.com` ，请使用 `*.*.example.com`。

> [!NOTE]
> 不要直接或通过通配符添加不在你控制中的域。 例如， `yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。 此外，禁止使用顶级域。 例如， `*.com`. `*.org`

### <a name="add-link-unfurling-using-app-studio"></a>使用 App Studio 添加链接展开

1. 从Microsoft Teams客户端打开 **App Studio**，然后选择 **“清单编辑器**”选项卡。
1. 加载应用清单。
1. 在 **“消息扩展** ”页上，添加要在 **“消息处理程序** ”部分中查找的域。 下图说明了此过程：

    ![App Studio 中的消息处理程序部分](~/assets/images/link-unfurling.png)

### <a name="add-link-unfurling-manually"></a>手动添加链接展开

若要使消息扩展能够与链接交互，首先必须将数 `messageHandlers` 组添加到应用清单。 以下示例说明如何手动添加链接展开：

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

有关完整清单示例，请参阅 [清单参考](~/resources/schema/manifest-schema.md)。

## <a name="handle-the-composeextensionquerylink-invoke"></a>`composeExtension/queryLink`处理调用

将域添加到应用清单后，必须更新 Web 服务代码以处理调用请求。 使用收到的 URL 搜索服务并创建卡片响应。 如果使用多个卡片进行响应，则仅使用第一个卡片响应。

支持以下卡片类型：

* [缩略图卡](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [主图卡](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [自适应卡](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

有关详细信息，请参阅 [操作类型调用](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)。

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

下面是发送到机器人的 `invoke` 示例：

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

下面是响应的示例：

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

## <a name="step-by-step-guide"></a>分步指南

按照[分步指南](../../sbs-botbuilder-linkunfurling.yml)操作，使用机器人在Teams中展开链接。

## <a name="see-also"></a>另请参阅

* [卡片](~/task-modules-and-cards/what-are-cards.md)
* [选项卡链接展开和阶段视图](~/tabs/tabs-link-unfurling.md)