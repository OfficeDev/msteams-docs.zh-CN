---
title: 创建和发送邮件
author: laujan
description: 介绍如何使用 Microsoft Teams 中的 Office 365 连接器
ms.topic: how-to
localization_priority: Normal
keywords: Teams o365 连接器
ms.openlocfilehash: 8835e43ed74a8da5ad3b3b4358b259d63068b469
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179893"
---
# <a name="create-and-send-messages"></a>创建和发送邮件

您可以创建可操作邮件，并通过传入 Webhook 或 Office 365 连接器发送。

## <a name="create-actionable-messages"></a>创建可操作邮件

可操作邮件包含卡片上的三个可见按钮。 每个按钮通过使用操作在邮件的 属性中定义，每个按钮都有一个输入类型、一个 `potentialAction` `ActionCard` 文本字段、一个日期选取器或一个多选项列表。 每个 `ActionCard` 都有一个关联的操作，例如 `HttpPOST` 。

连接器卡支持以下操作：

- `ActionCard`：显示一个或多个输入类型和关联的操作。
- `HttpPOST`：向 URL 发送 POST 请求。
- `OpenUri`：在单独的浏览器或应用中打开 URI，并基于操作系统选择面向不同的 URI。

`ActionCard` 操作支持三种输入类型：

- `TextInput`：具有可选长度限制的单行或多行文本字段。
- `DateInput`：具有可选时间选择器的日期选择器。
- `MultichoiceInput`：提供单选或多选选项的枚举列表。

`MultichoiceInput` 支持控制列表最初是否完全展开的 `style` 属性。 的默认值取决于 `style` 的值 `isMultiSelect` ，如下所示：

| `isMultiSelect` | `style` 默认值 |
| --- | --- |
| `false` 或未指定 | `compact` |
| `true` | `expanded` |

若要以紧凑样式显示多选项列表，必须同时指定 `"isMultiSelect": true` 和 `"style": true` 。

有关连接器卡操作详细信息，请参阅 [操作](/outlook/actionable-messages/card-reference#actions)。

> [!NOTE]
> * 在 Microsoft Teams 中指定 `style` 属性的 `compact` 与在 Microsoft Outlook 中指定 `style` 属性的 `normal` 相同。
> * 对于 HttpPOST 操作，请求中包括承载令牌。 此令牌包括已执行该操作的 Office 365 用户的 Azure AD 标识。

## <a name="send-a-message-through-incoming-webhook-or-office-365-connector"></a>通过传入 Webhook 或 Office 365 连接器发送邮件

若要通过传入 Webhook 或 Office 365 连接器发送邮件，请将 JSON 有效负载张贴到 webhook URL。 此有效负载必须以连接器Office 365[的形式。](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)

您还可以使用此 JSON 创建包含丰富输入（如文本输入、多选或选择日期和时间）的卡片。 生成卡片并张贴到 webhook URL 的代码可以在任何托管服务中运行。 这些卡片定义为可操作邮件的一部分，在卡片中也受[](~/task-modules-and-cards/what-are-cards.md)支持，用于Teams聊天机器人和消息传递扩展。

### <a name="example-of-connector-message"></a>连接器邮件示例

连接器邮件的示例如下所示：

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "Larry Bryant created a new task",
        "activitySubtitle": "On Project Tango",
        "activityImage": "https://teamsnodesample.azurewebsites.net/static/img/image5.png",
        "facts": [{
            "name": "Assigned to",
            "value": "Unassigned"
        }, {
            "name": "Due date",
            "value": "Mon May 01 2017 17:07:18 GMT-0700 (Pacific Daylight Time)"
        }, {
            "name": "Status",
            "value": "Not started"
        }],
        "markdown": true
    }],
    "potentialAction": [{
        "@type": "ActionCard",
        "name": "Add a comment",
        "inputs": [{
            "@type": "TextInput",
            "id": "comment",
            "isMultiline": false,
            "title": "Add a comment here for this task"
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Add comment",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "ActionCard",
        "name": "Set due date",
        "inputs": [{
            "@type": "DateInput",
            "id": "dueDate",
            "title": "Enter a due date for this task"
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Save",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "OpenUri",
        "name": "Learn More",
        "targets": [{
            "os": "default",
            "uri": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }, {
        "@type": "ActionCard",
        "name": "Change status",
        "inputs": [{
            "@type": "MultichoiceInput",
            "id": "list",
            "title": "Select a status",
            "isMultiSelect": "false",
            "choices": [{
                "display": "In Progress",
                "value": "1"
            }, {
                "display": "Active",
                "value": "2"
            }, {
                "display": "Closed",
                "value": "3"
            }]
        }],
        "actions": [{
            "@type": "HttpPOST",
            "name": "Save",
            "target": "https://docs.microsoft.com/outlook/actionable-messages"
        }]
    }]
}
```

此消息在频道中提供以下卡片：

![连接器卡的屏幕截图](~/assets/images/connectorcard.png)

## <a name="send-messages-using-curl-and-powershell"></a>使用 cURL 和 PowerShell 发送邮件

# <a name="curl"></a>[cURL](#tab/cURL)

**使用 cURL 在 Webhook 中发布消息**

1. 使用 安装 https://curl.haxx.se/ cURL：。

1. 在命令行中输入以下 cURL 命令：

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H "Content-Type:application/json" -d "{'text':'Hello World'}" <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > 如果 POST 成功，则必须看到 一个简单的 **1** 输出 `curl` 。

1. 检查Microsoft Teams新卡片的客户端。

# <a name="powershell"></a>[PowerShell](#tab/PowerShell)

 先决条件：安装 PowerShell 并熟悉其基本用法。

**使用 PowerShell 向 Webhook 发布消息**

1. 在 PowerShell 提示符中，输入以下命令：

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > 如果 POST 成功，则必须看到 一个简单的 **1** 输出 `Invoke-RestMethod` 。

1. 检查与 Webhook URL 相关联的 Microsoft Teams 频道。 你可以看到已张贴到频道的新卡片。 使用连接器测试或发布应用之前，必须执行以下操作：

    - [包括两个图标](../../concepts/build-and-test/apps-package.md#app-icons)。
    - 将 `icons` 清单部分修改为图标（而不是 URL）的文件名。

---

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a>使用传入 Webhook 发送自适应卡片

> [!NOTE]
> * 完全支持所有本机自适应卡片架构元素（除外 `Action.Submit` ）。
> * 支持的操作包括 [**Action.OpenURL、Action.ShowCard**](https://adaptivecards.io/explorer/Action.OpenUrl.html)和 [**Action.ToggleVisibility。**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html) [](https://adaptivecards.io/explorer/Action.ShowCard.html)

**通过传入 Webhook 发送自适应卡片**

1. 在 Teams 中设置自定义[webhook。](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
1. 使用下面的代码创建自适应卡片 JSON 文件：

    ```json
    {
       "type":"message",
       "attachments":[
          {
             "contentType":"application/vnd.microsoft.card.adaptive",
             "contentUrl":null,
             "content":{
                "$schema":"http://adaptivecards.io/schemas/adaptive-card.json",
                "type":"AdaptiveCard",
                "version":"1.2",
                "body":[
                    {
                    "type": "TextBlock",
                    "text": "For Samples and Templates, see [https://adaptivecards.io/samples](https://adaptivecards.io/samples)"
                    }
                ]
             }
          }
       ]
    }
    ```

    自适应卡片 JSON 文件的属性如下所示：

    * `"type"` 字段必须为 `"message"`。
    * `"attachments"` 阵列包含一组卡对象。
    * 该字段 `"contentType"` 必须设置为自适应卡片类型。
    * `"content"` 对象为采用 JSON 格式的卡。

1. 使用 Postman 测试自适应卡片：

    * 使用 [Postman](https://www.postman.com) 测试自适应卡片以向 URL 发送 POST 请求，该请求创建用于设置传入 Webhook。
    * 将 JSON 文件粘贴到请求正文中，并查看"自适应卡片"Teams。

> [!TIP]
> 使用自适应卡片 [代码示例和模板](https://adaptivecards.io/samples) 测试 POST 请求的正文。

## <a name="rate-limiting-for-connectors"></a>连接器的速率限制

应用程序速率限制控制允许连接器或传入 Webhook 在通道上生成的流量。 Teams固定速率窗口和增量计数器（以秒为单位）跟踪请求。 如果一秒钟提出四次以上请求，则客户端连接将受到限制，直到窗口在固定速率期间刷新。

### <a name="transactions-per-second-thresholds"></a>每秒事务数阈值

下表提供了基于时间的交易详细信息：

| 时间（以秒表示）  | 允许的最大请求数  |
|---|---|
| 1    | 4   |  
| 30   | 60  |  
| 3600   | 100  |
| 7200 | 150  |
| 86400  | 1800  |

对于 [请求在](/azure/architecture/patterns/retry) 一秒钟内超出限制的情况，具有指数退信的重试逻辑可以缓解速率限制。 请 [遵循最佳做法](../../bots/how-to/rate-limit.md) 以避免达到速率限制。

> [!NOTE]
> 对于 [请求在](/azure/architecture/patterns/retry) 一秒钟内超出限制的情况，具有指数退信的重试逻辑可以缓解速率限制。 请参阅 [HTTP 429 响应](../../bots/how-to/rate-limit.md#handle-http-429-responses)以避免达到速率限制。

```csharp
// Please note that response body needs to be extracted and read 
// as Connectors do not throw 429s
try
{
    // Perform Connector POST operation     
    var httpResponseMessage = await _client.PostAsync(IncomingWebhookUrl, new StringContent(content));
    // Read response content
    var responseContent = await httpResponseMessage.Content.ReadAsStringAsync();
    if (responseContent.Contains("Microsoft Teams endpoint returned HTTP error 429")) 
    {
        // initiate retry logic
    }
}
```

这些限制用于减少连接器发送的频道垃圾邮件，并确保为用户提供最佳体验。

## <a name="see-also"></a>另请参阅

* [Office 365连接器Microsoft Teams](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [创建传入 Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [创建传出 Webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
