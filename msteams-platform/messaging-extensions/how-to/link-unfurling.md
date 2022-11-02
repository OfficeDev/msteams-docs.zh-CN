---
title: 链接展开
author: surbhigupta
description: 使用应用清单或手动在 Microsoft Teams 应用中使用消息传递扩展添加链接展开。 使用开发人员门户添加链接展开。 如何更新 Web 服务代码以处理调用请求。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: c706bd4caf8ab7859fb0c8f9b5b9e8f337a3b269
ms.sourcegitcommit: 9ea9a70d2591bce6b8c980d22014e160f7b45f91
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/02/2022
ms.locfileid: "68820148"
---
# <a name="add-link-unfurling"></a>添加链接展开

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

本文档指导你如何使用开发人员门户或手动将链接展开添加到应用清单。 借助链接展开，当具有特定域的 URL 粘贴到撰写消息区域时，应用可以注册以接收 `invoke` 活动。 包含 `invoke` 粘贴到撰写消息区域的完整 URL。 可以使用卡片进行响应，用户可以展开该卡以获取其他信息或操作。 这用作搜索命令，URL 作为搜索词。

> [!NOTE]
>
> * 目前，移动客户端不支持链接展开。
> * 链接展开结果缓存 30 分钟。
> * 链接展开不需要消息传递扩展命令。 但是，清单中必须至少有一个命令，因为它是消息传递扩展中的必需属性。 有关详细信息，请参阅 [撰写扩展](/microsoftteams/platform/resources/schema/manifest-schema)

Azure DevOps 消息扩展使用链接展开查找粘贴到撰写消息区域(指向工作项)的 URL。 在下图中，用户粘贴了 Azure DevOps 中消息扩展已解析为卡片的项的 URL：

:::image type="content" source="~/assets/images/compose-extensions/messagingextensions_linkunfurling.png" alt-text="链接展开示例":::

若要详细了解链接展开，请参阅以下视频：
<br>
> [!VIDEO <https://www.microsoft.com/en-us/videoplayer/embed/RE4OFZG>]
<br>

## <a name="add-link-unfurling-to-your-app-manifest"></a>将链接展开添加到应用清单

要将链接展开添加到应用清单，请将新的 `messageHandlers` 数组添加到应用清单 JSON 的 `composeExtensions` 节。 可以通过开发人员门户或手动添加数组。 域列表可以包含通配符，例如 `*.example.com`。 这与域的某区段完全匹配；如果需要匹配 `a.b.example.com`，则使用 `*.*.example.com`。

> [!NOTE]
> 不要直接或通过通配符添加不在你的控制范围中的域。 例如，`yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。 顶级域是禁止的，例如 、 `*.com``*.org`。

### <a name="add-link-unfurling-using-developer-portal"></a>使用开发人员门户添加链接展开

1. 从 Microsoft Teams 客户端打开 **开发人员门户** ，然后选择“ **应用** ”选项卡。
1. 加载应用清单。
1. 在 **“应用功能”下的“消息传递扩展**”页上，选择现有机器人或创建新的机器人。
1. 选择“**保存**”。
1. 选择 **“预览链接**”部分下的“**添加域**”，然后输入有效域。
1. 选择“**添加**”。 下图说明了此流程:

   :::image type="content" source="../../assets/images/tdp/add-domain-button.PNG" alt-text="开发人员门户中消息处理程序部分的屏幕截图。" lightbox="../../assets/images/tdp/add-domain.PNG":::

### <a name="add-link-unfurling-manually"></a>手动添加链接展开

> [!NOTE]
> 如果身份验证是通过 Azure AD 添加的，请使用 [机器人在 Teams 中展开链接](/microsoftteams/platform/sbs-botbuilder-linkunfurling?tabs=vs&tutorial-step=4)。

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

* [消息扩展](../what-are-messaging-extensions.md)
* [自适应卡](../../task-modules-and-cards/what-are-cards.md#adaptive-cards)
* [选项卡链接展开和演示区域视图](../../tabs/tabs-link-unfurling.md)
* [composeExtensions](../../resources/schema/manifest-schema.md#composeextensions)
