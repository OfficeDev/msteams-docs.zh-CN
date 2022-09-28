---
title: 链接展开
author: surbhigupta
description: 使用应用清单或手动在 Microsoft Teams 应用中添加与消息传递扩展展开的链接。 使用开发人员门户添加链接展开。 如何更新 Web 服务代码以处理调用请求。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 57d3ed45bebfc221f376bf7e08aef73a5b4c40ae
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100628"
---
# <a name="add-link-unfurling"></a>添加链接展开

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

本文档介绍如何使用开发人员门户或手动向应用清单添加链接。 借助链接展开，当具有特定域的 URL 粘贴到撰写消息区域时，应用可以注册以接收 `invoke` 活动。 包含 `invoke` 粘贴到撰写消息区域的完整 URL。 可以使用卡片进行响应，用户可以展开该卡片以获取其他信息或操作。 这可用作搜索命令，其中 URL 作为搜索词。

> [!NOTE]
>
> * 目前，移动客户端不支持链接展开。
> * 链接展开结果缓存 30 分钟。
> * 链接展开不需要消息传递扩展命令。 但是，清单中必须至少有一个命令，因为它是消息传递扩展中的必需属性。 有关详细信息，请参阅 [撰写扩展](/microsoftteams/platform/resources/schema/manifest-schema)

Azure DevOps 消息扩展使用链接展开查找粘贴到撰写消息区域(指向工作项)的 URL。 在下图中，用户粘贴了 Azure DevOps 中邮件扩展已解析为卡片中的项的 URL：

:::image type="content" source="~/assets/images/compose-extensions/messagingextensions_linkunfurling.png" alt-text="链接展开示例":::

请参阅以下视频，了解有关链接展开的详细信息：
<br>
> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OFZG]
<br>

## <a name="add-link-unfurling-to-your-app-manifest"></a>将链接展开添加到应用清单

要将链接展开添加到应用清单，请将新的 `messageHandlers` 数组添加到应用清单 JSON 的 `composeExtensions` 节。 可以借助开发人员门户或手动添加数组。 域列表可以包含通配符，例如 `*.example.com`。 这与域的某区段完全匹配；如果需要匹配 `a.b.example.com`，则使用 `*.*.example.com`。

> [!NOTE]
> 请勿直接或通过通配符添加不在控件中的域。 例如，`yourapp.onmicrosoft.com` 有效，但 `*.onmicrosoft.com` 无效。 例如，`*.com``*.org`禁止使用顶级域。

### <a name="add-link-unfurling-using-developer-portal"></a>使用开发人员门户添加链接展开

1. 从 Microsoft Teams 客户 **端打开开发人员门户** ，然后选择“ **应用** ”选项卡。
1. 加载应用清单。
1. 在 **“应用功能**”下 **的“消息传递扩展**”页上，选择现有机器人或创建新机器人。
1. 选择“**保存**”。
1. 选择 **“预览链接**”部分下 **的“添加域**”，然后输入有效域。
1. 选择“**添加**”。 下图说明了此流程:

   :::image type="content" source="../../assets/images/tdp/add-domain-button.PNG" alt-text="开发人员门户中消息处理程序部分的屏幕截图。" lightbox="../../assets/images/tdp/add-domain.PNG":::

### <a name="add-link-unfurling-manually"></a>手动添加链接展开

> [!NOTE]
> 如果通过 Azure AD 添加身份验证，请 [使用机器人在 Teams 中展开链接](/microsoftteams/platform/sbs-botbuilder-linkunfurling?tabs=vs&tutorial-step=4)。

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
