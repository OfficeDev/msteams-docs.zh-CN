---
title: 响应搜索命令
author: clearab
description: 如何在 Microsoft 团队应用中的邮件扩展中响应搜索命令。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: e8b40dd8f422ffbd2537e8fa76a38c15eb6208de
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673492"
---
# <a name="respond-to-the-search-command"></a>响应搜索命令

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

您的 web 服务将接收`composeExtension/query`包含具有搜索参数的`value`对象的调用消息。 触发此调用：

* 在搜索框中输入字符时。
* 如果`initialRun`在应用程序清单中将设置为 true，则会在调用搜索命令后立即收到调用消息。 请参阅[默认查询](#default-query)。

请求参数本身位于请求的`value`对象中，其中包括以下属性：

| 属性名称 | 用途 |
|---|---|
| `commandId` | 用户调用的命令的名称，与应用程序清单中声明的命令之一相匹配。 |
| `parameters` | 参数数组。 每个 parameter 对象包含参数名称，以及用户提供的参数值。 |
| `queryOptions` | 分页参数： <br>`skip`：跳过此查询的计数 <br>`count`：要返回的元素数 |

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionResponse> OnTeamsMessagingExtensionQueryAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionQuery query, CancellationToken cancellationToken)
{
  //code to handle the query
}
```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

```typescript
class TeamsMessagingExtensionsSearch extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionQuery(context, query) {
  //code to handle the query
    }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

下面的 JSON 将被缩短，以突出显示最相关的部分。

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

当用户执行查询时，Microsoft 团队会向您的服务发出同步 HTTP 请求。 在这种情况下，您的代码有5秒的时间来提供对请求的 HTTP 响应。 在这段时间内，您的服务可以执行其他查找，或提供服务请求所需的任何其他业务逻辑。

您的服务应使用与用户查询匹配的结果进行响应。 响应必须指示 HTTP 状态代码`200 OK` ，以及具有以下正文的有效 application/json 对象：

|属性名称|用途|
|---|---|
|`composeExtension`|顶级响应信封。|
|`composeExtension.type`|响应的类型。 支持以下类型： <br>`result`：显示搜索结果列表 <br>`auth`：要求用户进行身份验证 <br>`config`：要求用户设置邮件扩展 <br>`message`：显示纯文本消息 |
|`composeExtension.attachmentLayout`|指定附件的布局。 用于类型`result`的响应。 <br>目前支持以下类型： <br>`list`：包含缩略图、标题和文本字段的卡片对象的列表 <br>`grid`：缩略图图像的网格 |
|`composeExtension.attachments`|有效的附件对象的数组。 用于类型`result`的响应。 <br>目前支持以下类型： <br>`application/vnd.microsoft.card.thumbnail` <br>`application/vnd.microsoft.card.hero` <br>`application/vnd.microsoft.teams.card.o365connector` <br>`application/vnd.microsoft.card.adaptive`|
|`composeExtension.suggestedActions`|建议的操作。 用于类型`auth`或`config`的响应。 |
|`composeExtension.text`|要显示的消息。 用于类型`message`的响应。 |

### <a name="response-card-types-and-previews"></a>响应卡片类型和预览

我们支持以下附件类型：

* [缩略图卡片](~/task-modules-and-cards/cards/cards-reference.md#thumbnail-card)
* [英雄卡片](~/task-modules-and-cards/cards/cards-reference.md#hero-card)
* [Office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)
* [自适应卡片](~/task-modules-and-cards/cards/cards-reference.md#adaptive-card)

有关概述，请参阅[什么是卡片](~/task-modules-and-cards/what-are-cards.md)。

若要了解如何使用缩略图和英雄卡片类型，请参阅[添加卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。

有关 Office 365 连接器卡的其他文档，请参阅[使用 office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)。

结果列表显示在 Microsoft 团队 UI 中，每个项目都有一个预览。 将通过以下两种方式之一生成预览：

* 在`attachment`对象`preview`中使用属性。 该`preview`附件只能是一个英雄或缩略图卡片。
* 从附件的基本`title`、 `text`和`image`属性中提取。 仅当未设置该`preview`属性且这些属性可用时，才使用这些属性。

您可以仅通过其 preview 属性在结果列表中显示自适应卡片或 Office 365 连接器卡片的预览。 如果结果已经是英雄或缩略图卡片，则无需执行此步骤。 如果使用预览附件，则它必须是英雄或缩略图卡片。 如果未指定 preview 属性，卡片的预览将会失败，并且不会显示任何内容。

### <a name="response-example"></a>响应示例

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

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

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

如果在清单`initialRun`中`true`设置为，Microsoft 团队会在用户第一次打开邮件扩展时发出 "默认" 查询。 您的服务可以使用一组预填充的结果对此查询做出响应。 当您的搜索命令需要进行身份验证或配置、显示最近查看的项目、收藏夹或任何其他不依赖于用户输入的信息时，这可能很有用。

默认查询的结构与任何常规用户`name`查询相同，字段在下面的对象中设置`initialRun`为`value`和设置`true`为。

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

## <a name="next-steps"></a>后续步骤

添加身份验证和/或配置

* [向邮件扩展添加身份验证](~/messaging-extensions/how-to/add-authentication.md)
* [向邮件扩展添加配置](~/messaging-extensions/how-to/add-configuration-page.md)

部署配置

* [部署应用程序包](~/concepts/deploy-and-publish/apps-upload.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
