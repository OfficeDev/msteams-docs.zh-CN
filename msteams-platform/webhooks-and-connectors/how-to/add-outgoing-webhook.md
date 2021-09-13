---
title: 创建传出 Webhook
author: laujan
description: 介绍如何创建传出 Webhook
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: lajanuar
keywords: teams 选项卡传出 Webhook 可操作邮件验证 webhook
ms.openlocfilehash: 2039ffdbc307b266e7bc0f93c1638450a8be9037
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155688"
---
# <a name="create-outgoing-webhook"></a>创建传出 Webhook

传出 Webhook 充当自动程序，使用 @mention 在 **频道中搜索消息**。 它将通知发送到外部 Web 服务，并响应丰富的消息，其中包括卡片和图像。 它有助于跳过通过以下过程创建[Microsoft Bot Framework。](https://dev.botframework.com/)

## <a name="key-features-of-outgoing-webhook"></a>传出 Webhook 的主要功能

下表提供了传出 Webhook 的功能和说明：

| 功能 | 说明 |
| ------- | ----------- |
| 作用域配置| Webhook 的范围在团队级别。 每个项的必需设置过程会添加一个传出 Webhook。 |
| 反应消息| 用户必须使用 @mention webhook 接收消息。 目前，用户只能在公共频道中发送传出 Webhook 消息，而不是在个人或专用范围内。 |
|标准 HTTP 邮件交换|响应显示在与原始请求消息相同的链中，并且可以包含任何 Bot Framework 消息内容，例如格式文本、图像、卡片和表情符号。 尽管传出 Webhook 可以使用卡片，但除了 以外，它们不能使用任何卡片操作 `openURL` 。|
| TeamsAPI 方法支持|传出 Webhook 将 HTTP POST 发送到 Web 服务并获取响应。 他们无法访问任何其他 API，例如检索团队中名单或频道列表。|

## <a name="create-outgoing-webhooks"></a>创建传出 Webhook

创建传出 Webhook，并添加自定义聊天机器人Teams。

**创建传出 Webhook**

1. 从 **Teams** 窗格中选择"下一个"。 将显示 **Teams** 页：

    ![Teams 频道](~/assets/images/teamschannel.png)

1. 在 **"Teams"** 页中，选择创建传出 Webhook 所需的团队，然后选择 &#8226;&#8226;&#8226;。 在下拉菜单中，选择"**管理团队"：**

    ![创建传出 Webhook](~/assets/images/outgoingwebhook1.png)

1. 选择频道 **页面上** 的"应用"选项卡：

    ![创建传出 Webhook](~/assets/images/outgoingwebhook2.png)

1. 选择 **"创建传出 Webhook"：**

    ![创建传出 Webhook](~/assets/images/outgoingwebhook3.png)

1. 在"创建传出 **Webhook"页中键入以下** 详细信息：

    * **名称**：Webhook 标题和@mention选项卡。
    * **回调 URL：** 接受 JSON 有效负载并接收来自客户端的 POST 请求的 HTTPS Teams。
    * **说明**：显示在配置文件卡片和团队级应用仪表板中的详细字符串。
    * **个人资料图片**：Webhook 的应用图标，可选。

1. 选择“**创建**”。 传出 Webhook 将添加到当前团队的频道：

    ![创建传出 Webhook](~/assets/images/outgoingwebhook.png)

将显示 [基于哈希的消息身份验证代码 (HMAC) ](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) 对话框。 它是一个安全令牌，用于对 Teams 和指定的外部服务之间的调用进行身份验证。

>[!NOTE]
> 仅在 URL 有效且服务器和客户端身份验证令牌相等时，传出 Webhook 才可供团队用户使用。 例如，HMAC 握手。

以下方案提供了添加传出 Webhook 的详细信息：

* 应用场景：将更改状态通知推送到Teams通道数据库服务器应用。
* 示例：你有一个业务线应用，可跟踪所有 CRUD 操作，如创建、读取、更新和删除。 这些操作通过跨租户的 Teams HR 用户对员工Office 365操作。

# <a name="url-json-payload"></a>[URL JSON 有效负载](#tab/urljsonpayload)
**在应用服务器上创建 URL 以接受并处理具有 JSON 有效负载的 POST 请求**

你的服务接收标准 Azure 自动程序服务消息架构中的邮件。 Bot Framework 连接器是一项 RESTful 服务，它支持通过 HTTPS 协议处理 JSON 格式邮件的交换，如 [Azure Bot Service API 中记录](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)。 或者，也可以按照 Microsoft Bot Framework SDK 处理和分析消息。 有关详细信息，请参阅 [Azure Bot 服务概述](/azure/bot-service/bot-service-overview-introduction)。

传出 Webhook 的范围为级别 `team` ，并且所有团队成员都可以看到。 用户需要 **\@ 提及传出** Webhook 的名称，以在频道中调用它。

# <a name="verify-hmac-token"></a>[验证 HMAC 令牌](#tab/verifyhmactoken)
**创建用于验证传出 Webhook HMAC 令牌的方法**

使用入站邮件和 ID 的示例：{"contoso"的 SigningKeyDictionary 的"contoso"，"vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }。

在请求标头的授权中，使用值"HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U="。

为了确保服务仅接收来自实际客户端Teams的呼叫，Teams HTTP 授权标头中提供 HMAC `hmac` 代码。 始终在身份验证协议中包括代码。

代码必须始终验证请求中包含的 HMAC 签名，如下所示：

* 从邮件的请求正文生成 HMAC 令牌。 在大多数平台上，有一些标准库可以这样做，例如加密[for](https://nodejs.org/api/crypto.html#crypto_crypto) Node.js 和 Teams [webhook 示例](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) \#) 。 Microsoft Teams使用标准 SHA256 HMAC 加密。 你必须在 UTF8 中将正文转换为字节数组。
* 在客户端中注册传出 Webhook 时，计算由 Teams 提供的安全令牌的字节数组Teams哈希。 请参阅 [创建传出 Webhook](#create-outgoing-webhook)。
* 使用 UTF-8 编码将哈希转换为字符串。
* 将生成的哈希的字符串值与 HTTP 请求中提供的值进行比较。

# <a name="method-to-respond"></a>[响应方法](#tab/methodtorespond)
**创建发送成功或失败响应的方法**

来自传出 Webhook 的响应显示在与原始邮件相同的回复链中。 当用户执行查询时，Microsoft Teams向服务发出同步 HTTP 请求，您的代码将在连接中断和终止之前获取 5 秒钟来响应消息。

### <a name="example-response"></a>示例响应

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```
---

> [!NOTE]
> * 可以使用传出 Webhook 将自适应卡片、Hero 卡片和短信作为附件发送。
> * 卡片支持格式设置。 有关详细信息，请参阅使用 [markdown 格式化卡片](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown)。

以下代码是自适应卡片响应的示例：

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
string content = await this.Request.Content.ReadAsStringAsync();
Activity incomingActivity = JsonConvert.DeserializeObject<Activity>(content);

var Card = new AdaptiveCard(new AdaptiveSchemaVersion("1.4"))
{
    Body = new List<AdaptiveElement>()
    {
        new AdaptiveTextBlock(){Text= $"Request sent by: {incomingActivity.From.Name}"},
        new AdaptiveImage(){Url=new Uri("https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6")},
        new AdaptiveTextBlock(){Text="Sample image for Adaptive Card.."}
    }
};

var attachment = new Attachment()
{
    ContentType = AdaptiveCard.ContentType,
    Content = Card
};

var sampleResponseActivity = new Activity
{
    Attachments = new [] { attachment }
};

return sampleResponseActivity;
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
var receivedMsg = JSON.parse(payload);
var responseMsg = JSON.stringify({
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "contentUrl": null,
            "content": {
                "type": "AdaptiveCard",
                "version": "1.4",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Request sent by: " + receivedMsg.from.name
                    },
                    {
                        "type": "Image",
                        "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
                    },
                    {
                        "type": "TextBlock",
                        "text": "Sample image for Adaptive Card."
                    }
                ]
            },
            "name": null,
            "thumbnailUrl": null
        }
    ]
});
```

# <a name="json"></a>[JSON](#tab/json)

```json
{
    "type": "message",
    "attachments": [
        {
            "contentType": "application/vnd.microsoft.card.adaptive",
            "content": {
                "type": "AdaptiveCard",
                "version": "1.4",
                "body": [
                    {
                        "type": "TextBlock",
                        "text": "Request sent by: Megan"
                    },
                    {
                        "type": "Image",
                        "url": "https://c.s-microsoft.com/en-us/CMSImages/DesktopContent-04_UPDATED.png?version=43c80870-99dd-7fb1-48c0-59aced085ab6"
                    },
                    {
                        "type": "TextBlock",
                        "text": "Sample image for Adaptive Card.."
                    }
                ]
            }
        }
    ]
}
```

* * *

## <a name="code-sample"></a>代码示例

|**示例名称** | **说明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| 传出 Webhook | 用于创建自定义聊天机器人的示例，以在 Microsoft Teams。| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## <a name="see-also"></a>另请参阅
* [创建传入 Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [创建 Office 365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [创建和发送邮件](~/webhooks-and-connectors/how-to/connectors-using.md)
