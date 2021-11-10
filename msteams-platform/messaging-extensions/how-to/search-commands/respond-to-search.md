---
title: 响应搜索命令
author: surbhigupta
description: 了解如何使用代码示例和示例从 Microsoft Teams应用中的消息扩展响应搜索命令
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: none
ms.openlocfilehash: 46c5d1ef47d9c31552efac00baef347baf3c7470
ms.sourcegitcommit: af1d0a4041ce215e7863ac12c71b6f1fa3e3ba81
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/10/2021
ms.locfileid: "60889375"
---
# <a name="respond-to-search-command"></a>响应搜索命令

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

在用户提交搜索命令后，Web 服务会收到一条调用消息，其中包含包含 `composeExtension/query` `value` 搜索参数的对象。 此调用将触发，并满足以下条件：

* 在搜索框中输入字符时。
* `initialRun` 在应用清单中设置为 true，一旦调用搜索命令，就会收到调用消息。 有关详细信息，请参阅默认 [查询](#default-query)。

本文档指导您如何以卡片和预览形式响应用户请求，以及用户Microsoft Teams默认查询的条件。

请求参数位于请求中的 对象中 `value` ，其中包括以下属性：

| 属性名称 | 用途 |
|---|---|
| `commandId` | 用户调用的命令的名称，与在应用清单中声明的命令之一匹配。 |
| `parameters` | 参数数组。 每个参数对象都包含参数名称以及用户提供的参数值。 |
| `queryOptions` | 分页参数： <br>`skip`：跳过此查询的计数 <br>`count`：要返回的元素数。 |

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

以下 JSON 已缩短，以突出显示最相关的部分。

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "searchKeywords",
        "value": "Toronto"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
...
}
```

* * *

## <a name="respond-to-user-requests"></a>响应用户请求

当用户执行查询时，Microsoft Teams向服务发送同步 HTTP 请求。 此时，代码有 `5` 几秒钟时间提供对请求的 HTTP 响应。 在此期间，你的服务可以执行其他查找，或执行为请求提供服务所需的任何其他业务逻辑。

服务必须使用与用户查询匹配的结果进行响应。 该响应必须指示 的 HTTP 状态代码以及具有以下属性的有效 `200 OK` 应用程序或 JSON 对象：

|属性名称|用途|
|---|---|
|`composeExtension`|顶级响应信封。|
|`composeExtension.type`|响应类型。 支持以下类型： <br>`result`：显示搜索结果列表 <br>`auth`：要求用户进行身份验证 <br>`config`：要求用户设置消息扩展 <br>`message`：显示纯文本消息 |
|`composeExtension.attachmentLayout`|指定附件的布局。 用于 类型 `result` 的响应。 <br>目前支持以下类型： <br>`list`：包含缩略图、标题和文本字段的卡片对象列表 <br>`grid`：缩略图图像的网格 |
|`composeExtension.attachments`|有效 attachment 对象的数组。 用于 类型 `result` 的响应。 <br>目前支持以下类型： <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|建议的操作。 用于 或 类型的 `auth` 响应 `config` 。 |
|`composeExtension.text`|要显示的消息。 用于 类型 `message` 的响应。 |

### <a name="response-card-types-and-previews"></a>响应卡类型和预览

Teams支持以下卡片类型：

* [缩略图卡片](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [Hero card](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

若要更好地了解卡片并概览卡片，请参阅 [什么是卡片](~/task-modules-and-cards/what-are-cards.md)。

若要了解如何使用缩略图和 Hero 卡片类型，请参阅 [添加卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。

有关连接器卡的其他Office 365，请参阅使用[Office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)。

结果列表显示在项目 UI 中Microsoft Teams每个项目的预览。 预览以以下两种方式之一生成：

* 在 `preview` 对象内使用 `attachment` 属性。 附件 `preview` 只能是 Hero 或 Thumbnail 卡片。
* 从附件的基本 `title` 、 `text` 和 `image` 属性中提取。 只有在属性未设置且这些属性可用 `preview` 时，才使用这些属性。
* 预览卡片不支持 Hero 或 Thumbnail 卡片按钮和点击操作（调用除外）。

可以使用自适应卡片或连接器Office 365预览属性在结果列表中显示该卡片的预览。 如果结果已是 Hero 或 Thumbnail 卡片，则不需要预览属性。 如果使用预览附件，它必须是 Hero 或 Thumbnail 卡片。 如果未指定任何预览属性，则卡片预览将失败，并且不显示任何内容。

### <a name="response-example"></a>响应示例

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken) 
{
  var text = query?.Parameters?[0]?.Value as string ?? string.Empty;

  //searches NuGet for a package
  var obj = JObject.Parse(await (new HttpClient()).GetStringAsync($"https://azuresearch-usnc.nuget.org/query?q=id:{text}&prerelease=true"));
  var packages = obj["data"].Select(item => (item["id"].ToString(), item["version"].ToString(), item["description"].ToString()));

  // We take every row of the results and wrap them in cards wrapped in in MessagingExtensionAttachment objects.
  // The Preview is optional, if it includes a Tap, that will trigger the OnTeamsMessagingExtensionSelectItemAsync event back on this bot.
  var attachments = packages.Select(package => new MessagingExtensionAttachment
      {
          ContentType = HeroCard.ContentType,
          Content = new HeroCard { Title = package.Item1 },
          Preview = new HeroCard { Title = package.Item1, Tap = new CardAction { Type = "invoke", Value = package } }.ToAttachment()
      })
      .ToList();

  // The list of MessagingExtensionAttachments must we wrapped in a MessagingExtensionResult wrapped in a MessagingExtensionResponse.
  return new MessagingExtensionResponse
  {
      ComposeExtension = new MessagingExtensionResult
      {
          Type = "result",
          AttachmentLayout = "list",
          Attachments = attachments
      }
  };
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearchBot extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
        const searchQuery = query.parameters[0].value;
        const response = await axios.get(`http://registry.npmjs.com/-/v1/search?${ querystring.stringify({ text: searchQuery, size: 8 }) }`);

        const attachments = [];
        response.data.objects.forEach(obj => {
            const heroCard = CardFactory.heroCard(obj.package.name);
            const preview = CardFactory.heroCard(obj.package.name);
            const attachment = { ...heroCard, preview };
            attachments.push(attachment);
        });

        return {
            composeExtension: {
                type: 'result',
                attachmentLayout: 'list',
                attachments: attachments
            }
        };
    }
}
```

# <a name="json"></a>[JSON](#tab/json)

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
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        }
      },
      {
        "contentType": "application/vnd.microsoft.card.adaptive",
        "content": {
          "type": "AdaptiveCard",
          "body": [
            {
              "type": "Container",
              "items": [
                {
                  "type": "TextBlock",
                  "text": "Microsoft Corp (NASDAQ: MSFT)",
                  "size": "medium",
                  "isSubtle": true
                },
                {
                  "type": "TextBlock",
                  "text": "September 19, 4:00 PM EST",
                  "isSubtle": true
                }
              ]
            },
            {
              "type": "Container",
              "spacing": "none",
              "items": [
                {
                  "type": "ColumnSet",
                  "columns": [
                    {
                      "type": "Column",
                      "width": "stretch",
                      "items": [
                        {
                          "type": "TextBlock",
                          "text": "75.30",
                          "size": "extraLarge"
                        },
                        {
                          "type": "TextBlock",
                          "text": "▼ 0.20 (0.32%)",
                          "size": "small",
                          "color": "attention",
                          "spacing": "none"
                        }
                      ]
                    },
                    {
                      "type": "Column",
                      "width": "auto",
                      "items": [
                        {
                          "type": "FactSet",
                          "facts": [
                            {
                              "title": "Open",
                              "value": "62.24"
                            },
                            {
                              "title": "High",
                              "value": "62.98"
                            },
                            {
                              "title": "Low",
                              "value": "62.20"
                            }
                          ]
                        }
                      ]
                    }
                  ]
                }
              ]
            }
          ],
          "version": "1.0"
        },
        "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "Microsoft Corp (NASDAQ: MSFT)",
            "text": "75.30 ▼ 0.20 (0.32%)"
          }
        }
      }
    ]
  }
}
```

* * *

## <a name="default-query"></a>默认查询

如果在清单中设置为 ，则Microsoft Teams用户首次打开邮件扩展时，将发送 `initialRun` `true` 默认查询。  你的服务可以使用一组预填充的结果来响应此查询。 当搜索命令需要身份验证或配置、显示最近查看的项目、收藏夹或其他不依赖于用户输入的信息时，此功能非常有用。

默认查询的结构与任何常规用户查询相同，字段设置为 并设置为 `name` `initialRun` `value` `true` ，如以下对象所示：

```json
{
  "type": "invoke",
  "name": "composeExtension/query",
  "value": {
    "commandId": "searchCmd",
    "parameters": [
      {
        "name": "initialRun",
        "value": "true"
      }
    ],
    "queryOptions": {
      "skip": 0,
      "count": 25
    }
  },
  ⋮
}
```

## <a name="code-sample"></a>代码示例

| 示例名称           | 描述 | .NET    | Node.js   |   
|:---------------------|:--------------|:---------|:--------|
|Teams邮件扩展操作| 介绍如何定义操作命令、创建任务模块和响应任务模块提交操作。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|Teams邮件扩展搜索   |  介绍如何定义搜索命令并响应搜索。        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [向消息传递扩展添加身份验证](~/messaging-extensions/how-to/add-authentication.md)

## <a name="see-also"></a>另请参阅

[向消息传递扩展添加配置](~/get-started/first-message-extension.md)
