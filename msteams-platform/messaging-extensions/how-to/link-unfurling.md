---
title: 链接展开
author: surbhigupta
description: 了解如何使用应用清单在 Microsoft Teams 应用中添加带消息传递扩展的链接展开，或使用代码示例和示例手动添加。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: c5f89847e374f6e7e2e15409f4a9fe019701788d
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2022
ms.locfileid: "66032971"
---
# <a name="link-unfurling"></a>链接展开

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

本文档介绍如何使用 App Studio 或手动向应用清单添加链接。 借助链接展开，当具有特定域的 URL 粘贴到撰写消息区域时，应用可以注册以接收 `invoke` 活动。 包含 `invoke` 粘贴到撰写消息区域的完整 URL。 可以使用卡片进行响应，用户可以展开该卡片以获取其他信息或操作。 这可用作搜索命令，其中 URL 作为搜索词。

> [!NOTE]
>
> * 目前，移动客户端不支持链接展开。
> * 链接展开结果缓存 30 分钟。

Azure DevOps 消息扩展使用链接展开查找粘贴到撰写消息区域(指向工作项)的 URL。 在下图中，用户粘贴了消息扩展已解析为卡片的Azure DevOps项的 URL：

:::image type="content" source="~/assets/images/compose-extensions/messagingextensions_linkunfurling.png" alt-text="链接展开示例":::

## <a name="add-link-unfurling-to-your-app-manifest"></a>将链接展开添加到应用清单

要将链接展开添加到应用清单，请将新的 `messageHandlers` 数组添加到应用清单 JSON 的 `composeExtensions` 节。 可以借助 App Studio 或手动添加数组。 域列表可以包含通配符，例如 `*.example.com`。 这与域的某区段完全匹配；如果需要匹配 `a.b.example.com`，则使用 `*.*.example.com`。

> [!NOTE]
> 请勿直接或通过通配符添加不在控件中的域。 例如，`yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。 例如，`*.com``*.org`禁止使用顶级域。

### <a name="add-link-unfurling-using-app-studio"></a>使用 App Studio 添加链接展开

1. 从 Microsoft Teams 客户端打开 “**App Studio**”，并选择“**清单编辑器**”选项卡。
1. 加载应用清单。
1. 在“**消息扩展**”页面上，添加要在“**消息处理程序**”部分中查找的域。下图说明了此过程：

    :::image type="content" source="~/assets/images/link-unfurling.png" alt-text="App Studio 中的“消息处理程序”部分":::

### <a name="add-link-unfurling-manually"></a>手动添加链接展开

> [!NOTE]
> 如果通过 Azure AD 添加身份验证，请[使用机器人在Teams中展开链接](/microsoftteams/platform/sbs-botbuilder-linkunfurling?tabs=vs&tutorial-step=4)。

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
