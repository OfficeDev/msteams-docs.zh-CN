---
title: 在自适应卡片中键入提前搜索
author: Rajeshwari-v
description: 介绍自适应卡片中 Input.ChoiceSet 控件的 typeahead 搜索
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: surbhigupta
ms.openlocfilehash: 1e302a74ceffb88989989b42aa8a202d1e79fb36
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65103437"
---
# <a name="typeahead-search-in-adaptive-cards"></a>在自适应卡片中键入提前搜索

自适应卡片中的 Typeahead 搜索功能为组件提供了增强的搜索体验 `input.choiceset` 。 它提供了在搜索字段中输入文本的选项列表。 可以将 typeahead 搜索与自适应卡片结合在一起，以搜索和选择数据。

可以对以下搜索使用 typeahead 搜索：

* [静态搜索](#static-typeahead-search)
* [动态搜索](#dynamic-typeahead-search)

## <a name="static-typeahead-search"></a>静态 typeahead 搜索

静态 typeahead 搜索允许用户从自适应卡有效负载中指定 `input.choiceset` 的值进行搜索。 静态 typeahead 搜索可用于向用户显示多个选项。 静态搜索中的有效负载大小随有效负载中指定的选择数而增加。
当用户开始输入文本时，将筛选选项，这部分匹配输入。 下拉列表突出显示了与搜索匹配的输入字符。

下图演示了静态 typeahead 搜索：

![静态 typeahead 搜索](~/assets/images/Cards/static-typeahead-search.gif)

## <a name="dynamic-typeahead-search"></a>动态 typeahead 搜索

动态类型头搜索可用于搜索和选择大型数据集中的数据。 数据集是从卡片有效负载中指定的数据集动态加载的。 在用户键入时，超前类型功能有助于筛选出选项。

# <a name="desktop"></a>[桌面设备](#tab/desktop)

:::image type="content" source="../../assets/images/Cards/dynamic-typeahead-search-desktop.png" alt-text="动态 typeahead 搜索":::

:::image type="content" source="../../assets/images/Cards/dynamic-typeahead-search-desktop-2.png" alt-text="动态类型头搜索 2":::

# <a name="mobile"></a>[移动设备](#tab/mobile)

Android 和 iOS 移动客户端支持自适应卡片中的 typeahead 搜索。

**应用场景**

John 是一名在 Xbox 零售店工作的商店员工。 该商店使用机器人接收来自客户的新购买请求。 客户可以从可用的数千个游戏中进行搜索。 自适应卡片中的 Typeahead 搜索用于搜索和选择客户的选择。

**在自适应卡片中使用 typeahead 搜索**

1. 用户 A 打开存储机器人。
1. 用户 A 将命令发送到机器人以获取 **新客户请求**。 机器人使用具有 `Input.ChoiceSet` 组件的自适应卡片进行响应。
1. 用户 A 使用 typeahead 搜索根据客户的选择搜索和选择信息。

下图演示了 typeahead 搜索的移动体验：

![静态 typeahead 搜索](~/assets/images/Cards/static-typeahead-search.gif)

---

> [!NOTE]
> 无法通过动态搜索（例如基于查询的消息扩展）获得丰富的卡片体验。

## <a name="implement-typeahead-search"></a>实现 typeahead 搜索

`Input.ChoiceSet` 是自适应卡片中的重要输入组件之一。 可以将 typeahead 搜索控件添加到 `Input.ChoiceSet` 组件以实现 typeahead 搜索。 可以使用以下选择搜索和选择所需的信息：

* 下拉列表，例如展开的选择。
* 单选按钮，例如单选。
* 复选框，例如多个选择。

> [!NOTE]
> 控 `Input.ChoiceSet` 件基于样式和 `isMultiSelect` 属性。

### <a name="schema-properties"></a>架构属性

以下属性是架构中启用 typeahead 搜索的新新增内容 [`Input.ChoiceSet`](https://adaptivecards.io/explorer/Input.ChoiceSet.html) ：

| 属性| 类型 | 必需 | 说明 |
|-----------|------|----------|-------------|
| style | 精简版 <br/> Expanded <br/> Filtered | 否 | 将筛选的样式添加到静态类型预览支持的验证列表中。|
| choices.data | Data.Query | 否 | 通过从后端提取一组远程选项，在用户键入时启用动态超前类型。 |

### <a name="dataquery-definition"></a>Data.Query 定义

| 属性| 类型 | 必需 | 说明 |
|-----------|------|----------|-------------|
| 类型 | Data.Query | 可访问 | 指定它是 Data.Query 对象。|
| 数据 | 字符串 | 是 | 指定动态提取的数据类型。 |
| value | 字符串 | 否 | 使用用户 `ChoiceSet`提供给机器人的输入填充对机器人的调用请求。 |
| count | 数字 | 否 | 填充对机器人的调用请求，以指定必须返回的元素数。 如果用户想要发送其他数量，机器人会忽略它。 |
| skip | 数字 | 否 | 填充对机器人的调用请求，以指示用户希望在列表中分页并向前移动。 |

### <a name="example"></a>示例

包含具有单个&多选选项的静态和动态 typeahead 搜索的示例有效负载，如下所示：

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "columns": [
        {
          "width": "1",
          "items": [
            {
              "size": null,
              "url": "https://urlp.asm.skype.com/v1/url/content?url=https%3a%2f%2fi.imgur.com%2fhdOYxT8.png",
              "height": "auto",
              "type": "Image"
            }
          ],
          "type": "Column"
        },
        {
          "width": "2",
          "items": [
            {
              "size": "extraLarge",
              "text": "Game Purchase",
              "weight": "bolder",
              "wrap": true,
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "text": "Please fill out the below form to send a game purchase request.",
      "wrap": true,
      "type": "TextBlock"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Game: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "stretch",
          "items": [
            {
              "choices": [
                {
                  "title": "Call of Duty",
                  "value": "call_of_duty"
                },
                {
                  "title": "Death's Door",
                  "value": "deaths_door"
                },
                {
                  "title": "Grand Theft Auto V",
                  "value": "grand_theft"
                },
                {
                  "title": "Minecraft",
                  "value": "minecraft"
                }
              ],
              "style": "filtered",
              "placeholder": "Search for a game",
              "id": "choiceGameSingle",
              "type": "Input.ChoiceSet"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Multi-Game: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "stretch",
          "items": [
            {
              "choices": [
                {
                  "title": "Static Option 1",
                  "value": "static_option_1"
                },
                {
                  "title": "Static Option 2",
                  "value": "static_option_2"
                },
                {
                  "title": "Static Option 3",
                  "value": "static_option_3"
                }
              ],
              "isMultiSelect": true,
              "style": "filtered",
              "choices.data": {
                "type": "Data.Query",
                "dataset": "xbox"
              },
              "id": "choiceGameMulti",
              "type": "Input.ChoiceSet"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "columns": [
        {
          "width": "auto",
          "items": [
            {
              "text": "Needed by: ",
              "wrap": true,
              "height": "stretch",
              "type": "TextBlock"
            }
          ],
          "type": "Column"
        },
        {
          "width": "stretch",
          "items": [
            {
              "id": "choiceDate",
              "type": "Input.Date"
            }
          ],
          "type": "Column"
        }
      ],
      "type": "ColumnSet"
    },
    {
      "text": "Buy and download digital games and content directly from your Xbox console, Windows 10 PC, or at Xbox.com.",
      "wrap": true,
      "type": "TextBlock"
    },
    {
      "text": "Earn points for what you already do on Xbox, then redeem your points on real rewards. Play more, get rewarded. Start earning today.",
      "wrap": true,
      "type": "TextBlock"
    }
  ],
  "actions": [
    {
      "data": {
        "msteams": {
          "type": "invoke",
          "value": {
            "type": "task/submit"
          }
        }
      },
      "title": "Request Purchase",
      "type": "Action.Submit"
    }
  ],
  "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
  "version": "1.2"
}
```

## <a name="code-snippets-for-invoke-request-and-response"></a>用于调用请求和响应的代码片段

### <a name="invoke-request"></a>调用请求

```json
{
    "name": "application/search",
    "type": "invoke",
    "value": {
        "queryText": "fluentui",
        "queryOptions": {
            "skip": 0,
            "top": 15
        },
        "dataset": "npm"
    },
    "locale": "en-US",
    "localTimezone": "America/Los_Angeles",
    // …. other fields
}
```

### <a name="response"></a>响应

#### <a name="c"></a>[C#](#tab/csharp)

```csharp
protected override async Task<InvokeResponse> OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
{
    if (turnContext.Activity.Name == "application/search")
    {
 var packages = new[] {
   new { title = "A very extensive set of extension methods", value = "FluentAssertions" },
   new { title = "Fluent UI Library", value = "FluentUI" }};

 var searchResponseData = new
 {
     type = "application/vnd.microsoft.search.searchResponse",
     value = new
     {
  results = packages
     }
 };
 var jsonString = JsonConvert.SerializeObject(searchResponseData);
 JObject jsonData = JObject.Parse(jsonString);
 return new InvokeResponse()
 {
     Status = 200,
     Body = jsonData
 };
    }

    return null;
}
```

#### <a name="nodejs"></a>[Node.js](#tab/nodejs)

```nodejs
  async onInvokeActivity(context) {
    if (context._activity.name == 'application/search') {
      // let searchQuery = context._activity.value.queryText;  // This can be used to filter the results
      var successResult = {
        status: 200,
        body: {
          "type": "application/vnd.microsoft.search.searchResponse",
          "value": {
            "results": [
              {
                "value": "FluentAssertions",
                "title": "A very extensive set of extension methods"
              },
              {
                "value": "FluentUI",
                "title": "Fluent UI Library"
              }
            ]
          }
        }
      }

      return successResult;

    }
  }
```

#### <a name="json"></a>[JSON](#tab/json)

```json
{
    "status": 200,
    "body" : {
        "type": "application/vnd.microsoft.search.searchResponse",
        "value": {
           "results": [
                {
                    "value": "FluentAssertions",
                    "title": "A very extensive set of extension methods."
                },
                {
                    "value": "FluentUI",
                    "title": "Fluent UI Library"
                }
            ]
        }
    }
}
```

---

## <a name="code-sample"></a>代码示例

|**示例名称** | **说明** | **C#** | **Node.js** |
|----------------|-----------------|--------------|----------------|
| 自适应卡片上的 Typeahead 搜索控件 | 此示例显示自适应卡片中静态和动态 typeahead 搜索控件的功能。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-type-ahead-search-adaptive-cards/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-type-ahead-search-adaptive-cards/nodejs) |

## <a name="see-also"></a>另请参阅

* [自适应卡的通用操作](Universal-actions-for-adaptive-cards/Overview.md)
* [任务模块](../what-are-task-modules.md)
