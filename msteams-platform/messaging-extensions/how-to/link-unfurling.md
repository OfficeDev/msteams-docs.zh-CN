---
title: 链接展开
author: surbhigupta
description: 了解如何使用应用清单在 Microsoft Teams 应用中添加带消息传递扩展的链接展开，或使用代码示例和示例手动添加。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: b172320f6f116026fe5ea4b45c9c74da6ff82f07
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111246"
---
# <a name="link-unfurling"></a>链接展开

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

本文档会带你了解如何使用 App Studio 手动将链接展开添加到应用清单。 借助链接展开，当具有特定域的 URL 粘贴到撰写消息区域时，应用可以注册以接收 `invoke` 活动。 `invoke` 包含粘贴到撰写消息区域的完整 URL，你可以使用用户可展开的卡片进行响应，从而提供其他信息或操作。 其工作原理类似于搜索命令，其中 URL 充当搜索词。

> [!NOTE]
>
> * 目前，移动客户端不支持链接展开。
> * 链接展开结果缓存 30 分钟。

Azure DevOps 消息扩展使用链接展开查找粘贴到撰写消息区域(指向工作项)的 URL。 在下图中，用户已在 Azure DevOps 中粘贴工作项的 URL，消息扩展已将其解析为卡片:

![链接展开示例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>将链接展开添加到应用清单

要将链接展开添加到应用清单，请将新的 `messageHandlers` 数组添加到应用清单 JSON 的 `composeExtensions` 节。 可以借助 App Studio 或手动添加数组。 域列表可以包含通配符，例如 `*.example.com`。 这与域的某区段完全匹配；如果需要匹配 `a.b.example.com`，则使用 `*.*.example.com`。

> [!NOTE]
> 不要直接或通过通配符添加不受控的域。 例如，`yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。 此外，禁止使用顶级域。 例如，`*.com`、`*.org`。

### <a name="add-link-unfurling-using-app-studio"></a>使用 App Studio 添加链接展开

1. 从 Microsoft Teams 客户端打开 “**App Studio**”，并选择“**清单编辑器**”选项卡。
1. 加载应用清单。
1. 在“**消息扩展**”页面上，添加要在“**消息处理程序**”节中查找的域。 下图说明了此流程:

    ![App Studio 中的消息处理程序节](~/assets/images/link-unfurling.png)

### <a name="add-link-unfurling-manually"></a>手动添加链接展开

要使消息扩展能够与链接交互，首先必须将 `messageHandlers` 数组添加到应用清单。 以下示例说明了如何手动添加链接展开:

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

将域添加到应用清单后，必须更新 Web 服务代码以处理调用请求。 使用收到的 URL 以搜索服务并创建卡片响应。 如果使用多个卡片进行响应，则仅使用第一个卡片响应。

支持以下卡片类型:

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

以下是发送到机器人的 `invoke` 示例:

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

以下为响应示例:

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

按照 [分步指南](../../sbs-botbuilder-linkunfurling.yml) 使用机器人在 Teams 中展开链接。

## <a name="see-also"></a>另请参阅

* [卡片](~/task-modules-and-cards/what-are-cards.md)
* [选项卡链接展开和演示区域视图](~/tabs/tabs-link-unfurling.md)