---
title: 响应搜索命令
author: surbhigupta
description: 了解如何从 Microsoft Teams 应用中的消息扩展响应搜索命令。 了解如何响应用户请求。
ms.topic: conceptual
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: bc1034db9a5b63d861f1abbe98f22c73556710b2
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100558"
---
# <a name="respond-to-search-command"></a>响应搜索命令

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

用户提交搜索命令后，Web 服务将收到一条 `composeExtension/query` 包含具有 `value` 搜索参数的对象的调用消息。 使用以下条件触发的此调用：

* 当字符输入到搜索框中时。
* `initialRun` 在应用清单中设置为 true，一旦调用搜索命令，就会收到调用消息。 有关详细信息，请参阅 [默认查询](#default-query)。

本文档介绍如何以卡片和预览的形式响应用户请求，以及 Microsoft Teams 发出默认查询的条件。

请求参数在 `value` 请求中的对象中找到，其中包括以下属性：

| 属性名称 | 用途 |
|---|---|
| `commandId` | 用户调用的命令的名称，与应用清单中声明的命令之一匹配。 |
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

下面的 JSON 会缩短，以突出显示最相关的部分。

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

当用户执行查询时，Microsoft Teams 会向服务发出同步 HTTP 请求。 此时，代码有 `5` 几秒钟的时间向请求提供 HTTP 响应。 在此期间，服务可以执行其他查找或为请求提供服务所需的任何其他业务逻辑。

服务必须响应与用户查询匹配的结果。 响应必须指示具有以下属性的 `200 OK` HTTP 状态代码以及有效的应用程序或 JSON 对象：

|属性名称|用途|
|---|---|
|`composeExtension`|顶级响应信封。|
|`composeExtension.type`|响应类型。 支持以下类型： <br>`result`：显示搜索结果的列表 <br>`auth`：提示用户进行身份验证 <br>`config`：提示用户设置消息扩展插件 <br>`message`：显示纯文本消息 |
|`composeExtension.attachmentLayout`|指定附件的布局。 用于类型 `result`响应。 <br>目前支持以下类型： <br>`list`：包含缩略图、标题和文本字段的卡片对象列表 <br>`grid`：缩略图图像的网格 |
|`composeExtension.attachments`|有效附件对象的数组。 用于类型 `result`响应。 <br>目前支持以下类型： <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|建议的操作。 用于类型或 `config`. `auth` 的响应。 |
|`composeExtension.text`|要显示的消息。 用于类型 `message`响应。 |

### <a name="response-card-types-and-previews"></a>响应卡类型和预览

Teams 支持以下卡片类型：

* [缩略图卡](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [主图卡](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [自适应卡](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

若要更好地了解和概述卡片，请参阅[卡片。](~/task-modules-and-cards/what-are-cards.md)

若要了解如何使用缩略图和英雄卡片类型，请 [参阅添加卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。

有关Office 365连接器卡的其他信息，请参阅[“使用Office 365连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)”。

结果列表显示在 Microsoft Teams UI 中，其中包含每个项的预览。 预览版是通过以下两种方式之一生成的：

* `preview`使用对象中的`attachment`属性。 附 `preview` 件只能是 Hero 或缩略图卡。
* 从对象的基本`title``text`属性和`image`属性中`attachment`提取。 仅当未指定该属性时， `preview` 才使用基本属性。

对于 Hero 或缩略图卡，预览卡不支持调用操作其他操作，例如按钮和点击。

若要发送自适应卡片或Office 365连接器卡，必须包含预览版。 该 `preview` 属性必须是 Hero 或缩略图卡。 如果未在对象中 `attachment` 指定预览属性，则不会生成预览。

对于 Hero 和 Thumbnail 卡，无需指定预览属性，默认情况下会生成预览版。

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

### <a name="enable-and-handle-tap-actions"></a>启用和处理点击操作

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override Task<MessagingExtensionResponse> OnTeamsMessagingExtensionSelectItemAsync(ITurnContext<IInvokeActivity> turnContext, JObject query, CancellationToken cancellationToken)
{
    // The Preview card's Tap should have a Value property assigned, this will be returned to the bot in this event. 
    var (packageId, version, description, projectUrl, iconUrl) = query.ToObject<(string, string, string, string, string)>();

    var card = new ThumbnailCard
    {
        Title = "Card Select Item",
        Subtitle = description
    };

    var attachment = new MessagingExtensionAttachment
    {
        ContentType = ThumbnailCard.ContentType,
        Content = card,
    };

    return Task.FromResult(new MessagingExtensionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            Type = "result",
            AttachmentLayout = "list",
            Attachments = new List<MessagingExtensionAttachment> { attachment }
        }
    });
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
async handleTeamsMessagingExtensionSelectItem(context, obj) {
        return {
            composeExtension: {
                  type: 'result',
                  attachmentLayout: 'list',
                  attachments: [CardFactory.thumbnailCard(obj.Item3)]
            }
        };
    } 
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "name": "composeExtension/selectItem",
    "type": "invoke",
    "value": {
        "Item1": "Package_Name",
        "Item2": "Version",
        "Item3": "Package Description"
    },
    .
    .
    .
}
```

* * *

> [!NOTE]
> `OnTeamsMessagingExtensionSelectItemAsync` 不会在移动团队应用程序中触发。

## <a name="default-query"></a>默认查询

如果设置为`initialRun``true`在清单中，则当用户首次打开消息扩展时，Microsoft Teams 将发出 **默认** 查询。 服务可以使用一组预填充的结果来响应此查询。 当搜索命令需要身份验证或配置、显示最近查看的项目、收藏夹或不依赖于用户输入的任何其他信息时，这非常有用。

默认查询的结构与任何常规用户查询相同， `name` 字段设置为 `initialRun` 并 `value` 设置为 `true` 如下对象所示：

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

| 示例名称           | 说明 | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Teams 消息扩展操作| 介绍如何定义操作命令、创建任务模块和响应任务模块提交操作。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |
|Teams 消息扩展搜索   |  介绍如何定义搜索命令和响应搜索。        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [向消息扩展添加身份验证](~/messaging-extensions/how-to/add-authentication.md)

## <a name="see-also"></a>另请参阅

[将配置添加到消息扩展](~/get-started/first-message-extension.md)
