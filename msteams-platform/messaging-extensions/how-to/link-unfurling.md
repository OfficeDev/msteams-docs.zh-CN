---
title: 链接展开
author: clearab
description: 如何在 Microsoft Teams 应用中使用消息传递扩展执行链接取消链接。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 0d488638e63b8ec78bfa5bed8cf6f4f037883fb1
ms.sourcegitcommit: bf61ae5ad2afa4efdb0311158184d0cbb9c40174
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2021
ms.locfileid: "49845635"
---
# <a name="link-unfurling"></a>链接展开

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

> [!NOTE]
> 目前，移动客户端不支持链接取消链接。

通过取消链接，应用可以注册以在将特定域的 URL 粘贴到撰写邮件区域中时 `invoke` 接收活动。 将包含粘贴到撰写邮件区域中的完整 URL，您可以使用用户可以取消展开的卡片进行响应，从而 `invoke` 提供其他信息或操作。 这非常类似于搜索 [命令，URL](~/messaging-extensions/how-to/search-commands/define-search-command.md)充当搜索词。

Azure DevOps 邮件扩展使用链接取消链接查找粘贴到指向工作项的撰写邮件区域中的 URL。 在下面屏幕截图中，用户已粘贴 Azure DevOps 中某个工作项的 URL，邮件扩展已解析为卡片。

![链接取消链接示例](~/assets/images/compose-extensions/messagingextensions_linkunfurling.png)

## <a name="add-link-unfurling-to-your-app-manifest"></a>向应用清单添加链接取消链接

 若要向应用清单添加链接，请向应用清单 `messageHandlers` `composeExtensions` JSON 部分添加新数组。 可以在 App Studio 的帮助下或手动添加数组。 域列表可以包括通配符，例如 `*.example.com` 。 这完全匹配域的一个段;如果需要匹配，请使用 `a.b.example.com` `*.*.example.com` 。

> [!NOTE]
> 不要直接添加或通过通配符添加超出控件的域。 例如，yourapp.onmicrosoft.com有效，但 *.onmicrosoft.com 为 无效。 此外，还禁止顶级域。 例如*.com、*.org。

### <a name="using-app-studio"></a>使用 App Studio

1. 在 App Studio 的清单编辑器选项卡上，加载应用清单。
1. 在 **"消息扩展**"页上，在"邮件处理程序"部分添加要查找的域，如下面的屏幕截图所示。

![App Studio 中的邮件处理程序部分](~/assets/images/link-unfurling.png)

### <a name="manually"></a>手动

若要使邮件扩展可以这样与链接进行交互，你首先需要将数组添加到应用清单， `messageHandlers` 如以下示例所示。 此示例不是完整的清单 [，请参阅完整](~/resources/schema/manifest-schema.md) 清单示例的清单参考。

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

## <a name="handle-the-composeextensionquerylink-invoke"></a>处理 `composeExtension/queryLink` 调用

添加域以侦听应用程序清单后，需要更新 Web 服务代码以处理调用请求。 使用收到的 URL 搜索服务并创建卡片响应。 如果使用多张卡片进行响应，则仅使用第一张。

我们支持以下卡片类型：

* [缩略图卡片](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Hero 卡片](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

有关 [概述，请参阅什么是](~/task-modules-and-cards/what-are-cards.md) 卡片。

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

这是发送到机器人 `invoke` 的示例。

```json
{
  "type": "invoke",
  "name": "composeExtension/queryLink",
  "value": {
    "url": "https://theurlsubmittedbyyouruser.trackeddomain.com/id/1234"
  }
}
```

下面显示了一个响应示例。

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
