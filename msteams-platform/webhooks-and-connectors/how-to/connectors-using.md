---
title: 创建和发送邮件
author: laujan
description: 在本模块中，了解如何使用 Office 365 连接器并在 Microsoft Teams 中创建和发送可操作邮件
ms.topic: how-to
ms.localizationpriority: high
ms.openlocfilehash: 6e50877f1afbebe1e132c6461fbae30445227f43
ms.sourcegitcommit: 5c12af6a379c7cace409fda94677ea0334d7a3dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/13/2022
ms.locfileid: "67337213"
---
# <a name="create-and-send-messages"></a>创建和发送邮件

可以创建可操作邮件并通过传入 Webhook 或 Office 365 连接器发送。

## <a name="create-actionable-messages"></a>创建可操作邮件

可操作邮件包括卡片上的六个可见按钮。 通过使用 `ActionCard` 操作在邮件的 `potentialAction` 属性中定义每个按钮，每个操作带有一个输入类型: 文本字段、日期选取器或多选列表。 每个 `ActionCard` 都具有关联的操作，例如 `HttpPOST`。

连接器卡支持以下操作:

* `ActionCard`: 显示一个或多个输入类型和关联的操作。
* `HttpPOST`: 向 URL 发送 POST 请求。
* `OpenUri`: 在单独的浏览器或应用程序中打开 URI，根据操作系统，可选择性地针对不同的 URI。

`ActionCard` 操作支持三种输入类型：

* `TextInput`: 具有可选长度限制的单行或多行文本字段。
* `DateInput`: 具有可选时间选择器的日期选择器。
* `MultichoiceInput`: 提供单项选择或多重选择的选项枚举列表。

`MultichoiceInput` 支持控制列表最初是否完全展开的 `style` 属性。 `style`: 的默认值取决于 `isMultiSelect` 的值，如下所示:

| `isMultiSelect` | `style` 默认值 |
| --- | --- |
| `false` 或未指定 | `compact` |
| `true` | `expanded` |

若要以紧凑样式显示多选列表，请指定 `"isMultiSelect": true` 和 `"style": true`。

有关连接器卡操作的详细信息，请参阅 [操作](/outlook/actionable-messages/card-reference#actions)。

> [!NOTE]
>
> * 在 Microsoft Teams 中指定 `style` 属性的 `compact` 与在 Microsoft Outlook 中指定 `style` 属性的 `normal` 相同。
> * 对于 HttpPOST 操作，请求中包括承载令牌。 此令牌包括执行此操作的 Office 365 用户的 Microsoft Azure Active Directory (Azure AD) 标识。

## <a name="send-a-message-through-incoming-webhook-or-office-365-connector"></a>通过传入 Webhook 或 Office 365 连接器发送消息

若要通过传入 Webhook 或 Office 365 连接器发送消息，请将 JSON 有效负载发布到 Webhook URL。 此有效负载必须采用 [Office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card) 的形式。

还可使用此 JSON 创建包含丰富输入内容 (如文本输入、多重选择或选择日期和时间) 的卡。 生成卡并将其发布到 Webhook URL 的代码可以在任何托管服务上运行。 这些卡片被定义为可操作邮件的一部分，在 Teams 机器人和消息扩展中使用的[卡片](~/task-modules-and-cards/what-are-cards.md)也受支持。

### <a name="example-of-connector-message"></a>连接器消息示例

连接器消息示例如下所示:

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

此邮件在频道中提供以下卡片:

![连接器卡的屏幕截图](~/assets/images/connectorcard.png)

## <a name="send-messages-using-curl-and-powershell"></a>使用 cURL 和 PowerShell 发送消息

# <a name="curl"></a>[cURL](#tab/cURL)

若要使用 cURL 在 Webhook 中发布消息，请按照以下步骤进行:

1. 从 [cURL 网站](https://curl.haxx.se/) 安装 cURL。

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
    > 如果 POST 成功，则必须看到 `curl` 简单输出 **1**。

1. 检查 Teams 客户端以查看已发布的新卡片。

# <a name="powershell"></a>[PowerShell](#tab/PowerShell)

 先决条件: 安装 PowerShell 并熟悉其基本用法。

若要使用 PowerShell 将消息发布到 Webhook，请按照以下步骤进行:

1. 在 PowerShell 提示符中，输入以下命令：

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

    > [!NOTE]
    > 如果 POST 成功，则必须看到 `Invoke-RestMethod` 简单输出 **1**。

1. 检查与 Webhook URL 相关联的 Teams 频道。 你应查看发布到频道的新卡片。 在使用连接器测试或发布应用之前，必须执行以下操作:

    * [包括两个图标](../../concepts/build-and-test/apps-package.md#app-icons)。
    * 将清单的 `icons` 部分修改为图标的文件名而不是 URL。

---

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a>使用传入 webhook 发送自适应卡

> [!NOTE]
>
> * 完全支持所有本机自适应卡片架构元素 (`Action.Submit`除外)。
> * 受支持的操作有 [**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html)、[**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html)，以及 [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)

若要使用传入 webhook 以发送自适应卡，请按照以下步骤进行:

1. 在 Teams 中 [设置自定义 webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)。
1. 使用以下代码创建自适应卡的 JSON 文件:

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

    自适应卡 JSON 文件的属性如下所示:

    * `"type"` 字段必须为 `"message"`。
    * `"attachments"` 阵列包含一组卡对象。
    * `"contentType"` 字段必须设置为自适应卡类型。
    * `"content"` 对象为采用 JSON 格式的卡。

1. 使用 Postman 测试自适应卡:

    * 使用 [Postman](https://www.postman.com) 测试自适应卡，向为设置传入 Webhook 而创建的 URL 发送 POST 请求。
    * 将 JSON 文件粘贴至请求主体中，并在 Teams 中查看自适应卡。

> [!TIP]
> 使用自适应卡 [代码示例和模板](https://adaptivecards.io/samples) 测试 POST 请求的主体。

## <a name="rate-limiting-for-connectors"></a>连接器的速率限制

应用程序速率限制可以控制允许连接器或传入 Webhook 在频道上生成的流量。 Teams 使用固定速率窗口以及以秒为单位的增量计数器跟踪请求。 如果在一秒内发出的请求超过四个，则客户端连接会受到限制，直到窗口刷新的持续时间为固定速率。

### <a name="transactions-per-second-thresholds"></a>每秒事务数阈值

下表提供了基于时间的事务详细信息:

| 时间 (秒)  | 允许的最大请求数  |
|---|---|
| 1   | 4  |  
| 30   | 60  |  
| 3600   | 100  |
| 7200 | 150  |
| 86400  | 1800  |

[具有指数补偿的重试逻辑](/azure/architecture/patterns/retry) 将减轻速率限制，以应对请求在一秒内超出限制的情况。请遵循 [最佳做法](../../bots/how-to/rate-limit.md) 以避免达到效率限制。

> [!NOTE]
> [具有指数补偿的重试逻辑](/azure/architecture/patterns/retry)将减轻速率限制，以应对请求在一秒内超出限制的情况。请参阅 [HTTP 429 响应](../../bots/how-to/rate-limit.md#handle-http-429-responses)以避免达到速率限制。

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

这些限制已就位，通过连接器减少频道垃圾邮件，并确保用户获得最佳体验。

## <a name="see-also"></a>另请参阅

* [适用于 Microsoft Teams 的 Office 365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [创建传入 Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [创建传出 Webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
* [Teams 机器人消息的速率限制](~/bots/how-to/rate-limit.md)
* [具有自适应卡片的生成选项卡](~/tabs/how-to/build-adaptive-card-tabs.md)
* [Microsoft Teams 中的格式卡](~/task-modules-and-cards/cards/cards-format.md)
* [使用 JavaScript 生成通知机器人](../../sbs-gs-notificationbot.yml)
* [使用 JavaScript 生成第一个机器人应用](../../sbs-gs-bot.yml)
