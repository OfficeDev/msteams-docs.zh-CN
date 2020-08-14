---
title: 向连接器和 Webhook 发送邮件
description: 介绍如何使用 Microsoft Teams 中的 Office 365 连接器
localization_priority: Priority
keywords: Teams o365 连接器
ms.openlocfilehash: 16dbb99add82c26930baf22bfc2c5153fd47b2f1
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651647"
---
# <a name="sending-messages-to-connectors-and-webhooks"></a>向连接器和 Webhook 发送邮件

若要通过 Office 365 连接器或传入 Webhook 发送邮件，请将 JSON 有效负载发布到 Webhook URL。 通常，此有效负载将采用 [Office 365 连接器卡](~/task-modules-and-cards/cards/cards-reference.md#office-365-connector-card)的形式。

还可使用此 JSON 创建包含丰富输入内容（如文本输入、多重选择或选择日期和时间）的卡。 生成卡并将其发布到 Webhook URL 的代码可以在任何托管服务上运行。 这些卡片被定义为可操作邮件的一部分，在 Teams 机器人和邮件扩展中使用的[卡片](~/task-modules-and-cards/what-are-cards.md)受支持。

### <a name="example-connector-message"></a>示例连接器邮件

```json
{
    "@type": "MessageCard",
    "@context": "http://schema.org/extensions",
    "themeColor": "0076D7",
    "summary": "Larry Bryant created a new task",
    "sections": [{
        "activityTitle": "![TestImage](https://47a92947.ngrok.io/Content/Images/default.png)Larry Bryant created a new task",
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
            "target": "http://..."
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
            "target": "http://..."
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
            "target": "http://..."
        }]
    }]
}
```

此邮件在频道中生成以下卡片。

![连接器卡的屏幕截图](~/assets/images/connectors/connector_message.png)

## <a name="creating-actionable-messages"></a>创建可操作邮件

上一节中的示例包括卡上的三个可见按钮。 通过使用 `ActionCard` 操作在邮件的 `potentialAction` 属性中定义每个按钮，每个操作包含一个输入类型：文本字段、日期选取器或多选列表。 每个 `ActionCard` 操作都具有关联的操作，例如 `HttpPOST`。

连接器卡支持三种类型的操作：

- `ActionCard` 显示一个或多个输入类型和关联的操作
- `HttpPOST` 向 URL 发送 POST 请求
- `OpenUri` 在单独的浏览器或应用程序中打开 URI；根据操作系统，可选择性地针对不同的 URI

（第四个操作 `ViewAction` 仍受支持，但不再需要；改用 `OpenUri`。）

`ActionCard` 操作支持三种输入类型：

- `TextInput` 具有可选长度限制的单行或多行文本字段
- `DateInput` 具有可选时间选择器的日期选择器
- `MultichoiceInput` 提供单项选择或多重选择的选项枚举列表

`MultichoiceInput` 支持控制列表最初是否完全展开的 `style` 属性。 `style` 的默认值取决于 `isMultiSelect` 的值。

| `isMultiSelect` | `style` 默认值 |
| --- | --- |
| `false` 或未指定 | `compact` |
| `true` | `expanded` |

如果想要以精简样式初始显示多选列表，则必须同时指定 `"isMultiSelect": true` 和 `"style": true`。

> [!NOTE]
> 在 Microsoft Teams 中的指定 `style` 属性的 `compact` 与在 Microsoft Outlook 中指定 `style` 属性的 `normal` 相同。

有关连接器卡操作的所有其他详细信息，请参阅可操作的邮件卡参考中的**[“操作”](/outlook/actionable-messages/card-reference#actions)**。

## <a name="setting-up-a-custom-incoming-webhook"></a>设置自定义传入 Webhook

请按照以下步骤，了解如何向连接器发送简单卡。

1. 在 Microsoft Teams 中，选择频道名称旁边的 **“更多选项”**(**&#8943;**) ，然后选择 **“连接器”**。
2. 滚动浏览 **“传入 Webhook”** 的连接器列表，然后选择 **“添加”**。
3. 输入 Webhook 的名称，上传图像以与 Webhook 中的数据相关联，然后选择 **“创建”**。
4. 将 Webhook 复制到剪贴板并保存。 需要 Webhook URL 才能将信息发送到 Microsoft Teams。
5. 选择 **“完成”**。

### <a name="post-a-message-to-the-webhook-using-curl"></a>使用 cURL 将邮件发布到 Webhook

以下步骤使用 [cURL](https://curl.haxx.se/)。 假设你已安装，并熟悉其基本用法。

1. 在命令行中输入以下 cURL 命令：

   ```bash
   // on macOS or Linux
   curl -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

   ```bash
   // on Windows
   curl.exe -H 'Content-Type: application/json' -d '{"text": "Hello World"}' <YOUR WEBHOOK URL>
   ```

2. 如果 POST 成功，则可以看到 `curl` 简单输出 **1**。
3. 检查 Microsoft Team 客户端。 你应查看发布到团队的新卡片。

### <a name="post-a-message-to-the-webhook-using-powershell"></a>使用 PowerShell 将邮件发布到 Webhook

以下步骤使用 PowerShell。 假设你已安装，并熟悉其基本用法。

1. 在 PowerShell 提示符中，输入以下命令：

   ```powershell
   Invoke-RestMethod -Method post -ContentType 'Application/Json' -Body '{"text":"Hello World!"}' -Uri <YOUR WEBHOOK URL>
   ```

2. 如果 POST 成功，则可以看到 `Invoke-RestMethod` 简单输出 **1**。
3. 检查与 Webhook URL 相关联的 Microsoft Teams 频道。 你应查看发布到频道的新卡片。

- 包含两个图标，按照[“图标”](~/concepts/build-and-test/apps-package.md#icons)中的说明。
- 修改清单的 `icons` 部分，以便引用图标的文件名，而不是 URL。

以下 manifest.json 文件包含测试和提交应用程序所需的基本元素。

> [!NOTE]
> 将以下示例中的 `id` 和 `connectorId` 替换为连接器的 GUID。

#### <a name="example-manifestjson-with-connector"></a>带连接器的示例 manifest.json

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "id": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
  "version": "1.0",
  "packageName": "com.sampleapp",
  "developer": {
    "name": "Publisher",
    "websiteUrl": "https://www.microsoft.com",
    "privacyUrl": "https://www.microsoft.com",
    "termsOfUseUrl": "https://www.microsoft.com"
  },
  "description": {
    "full": "This is a small sample app we made for you! This app has samples of all capabilities Microsoft Teams supports.",
    "short": "This is a small sample app we made for you!"
  },
  "icons": {
    "outline": "sampleapp-outline.png",
    "color": "sampleapp-color.png"
  },
  "connectors": [
    {
      "connectorId": "e9343a03-0a5e-4c1f-95a8-263a565505a5",
      "scopes": [
        "team"
      ]
    }
  ],
  "name": {
    "short": "Sample App",
    "full": "Sample App"
  },
  "accentColor": "#FFFFFF",
  "needsIdentity": "true"
}
```

## <a name="send-adaptive-cards-using-an-incoming-webhook"></a>使用传入 webhook 发送自适应卡

> [!NOTE]
>
> ✔ 完全支持所有本地自适应卡架构元素（`Action.Submit` 除外）。
>
> ✔ 受支持的操作包括：[**Action.OpenURL**](https://adaptivecards.io/explorer/Action.OpenUrl.html)、[**Action.ShowCard**](https://adaptivecards.io/explorer/Action.ShowCard.html) 和 [**Action.ToggleVisibility**](https://adaptivecards.io/explorer/Action.ToggleVisibility.html)。

### <a name="the-flow-for-sending-adaptive-cards-via-an-incoming-webhook-is-as-follows"></a>通过传入 webhook 发送[自适应卡](../../task-modules-and-cards/cards/cards-reference.md#adaptive-card)的流程如下所示：

**1.** 在 Teams 中[设置自定义 webhook](#setting-up-a-custom-incoming-webhook)。</br></br>
**2.** 创建自适应卡 JSON 文件：

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
                  "For Samples and Templates, see":"https://adaptivecards.io/samples"
               }
            ]
         }
      }
   ]
}
```

> [!div class="checklist"]
>
> - `"type"` 字段必须为 `"message"`。
> - `"attachments"` 阵列包含一组卡对象。
> - `"contentType"` 字段必须设置为自适应卡类型。
> - `"content"` 对象为采用 JSON 格式的卡。

**3.** 使用 Postman 测试自适应卡

可以使用 [Postman](https://www.postman.com) 测试自适应卡，以发送 POST 请求至在设置传入 webhook 时创建的 URL。 将 JSON 文件粘贴至请求主体中，并在 Teams 中查看自适应卡。

>[!TIP]
> 你可以为测试 Post 请求主体使用自适应卡代码[示例和模板](https://adaptivecards.io/samples)。

## <a name="testing-your-connector"></a>测试连接器

若要测试连接器，请将其上传到团队中，就像使用任何其他应用程序一样。 可使用连接器开发人员仪表板中的清单文件（按照上一部分的说明进行修改）和两个图标文件来创建 .zip 包。

上传应用程序后，从任意频道打开连接器列表。 向下滚动到底部，查看 **“上传”** 部分中的应用程序。

![“连接器”对话框中上传部分的屏幕截图](~/assets/images/connectors/connector_dialog_uploaded.png)

现在可启动配置体验。 请注意，此流程是通过弹出窗口完全在 Microsoft Teams 中发生。 目前，这种行为与我们创建的连接器中的配置体验不同；我们正在努力统一体验。

若要验证 `HttpPOST` 操作是否正常工作，请使用[自定义传入 Webhook](#setting-up-a-custom-incoming-webhook)。

## <a name="rate-limiting-for-connectors"></a>连接器的速率限制

应用程序速率限制可以控制允许连接器或传入 Webhook 在频道上生成的流量。 Teams 通过固定速率窗口以及以秒为单位的增量计数器跟踪请求。  如果发出的请求过多，则会限制客户端连接，直至该窗口刷新（即在固定速率的持续时间内）。

### <a name="transactions-per-second-thresholds"></a>**每秒事务数阈值**

| 时间（秒）  | 允许的最大请求数  |
|---|---|
| 1   | 4  |  
| 30   | 60  |  
| 3600   | 100  |
| 7200 | 150  |
| 86400  | 1800  |

*另请参阅* [Office 365 连接器 - Microsoft Teams](https://docs.microsoft.com/connectors/teams/)

如下所示，[具有指数补偿的重试逻辑](/azure/architecture/patterns/retry)将减轻速率限制，以应对请求在一秒内超出限制的情况。 请按照[最佳做法](../../bots/how-to/rate-limit.md#best-practices)避免达到速率限制。

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
 
这些限制已就位，通过连接器减少频道垃圾邮件，并确保最终用户获得最佳体验。
