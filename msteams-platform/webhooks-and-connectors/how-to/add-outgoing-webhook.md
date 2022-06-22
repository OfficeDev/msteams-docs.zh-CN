---
title: 创建传出 Webhook
author: laujan
description: 在本模块中，了解如何在 Microsoft Teams 中创建传出 Webhook 及其主要功能和代码示例
ms.topic: conceptual
ms.localizationpriority: high
ms.author: lajanuar
ms.openlocfilehash: a290d7197c842c3920bd536fa71774fd82e47d84
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2022
ms.locfileid: "66189892"
---
# <a name="create-outgoing-webhook"></a>创建传出 Webhook

传出 Webhook 充当机器人并使用 **@提及** 功能在频道中搜索邮件。 它向外部 Web 服务发送通知并以丰富的消息（包括卡片和图像）进行响应。 它有助于跳过通过 [Microsoft Bot Framework](https://dev.botframework.com/) 创建机器人的过程。

<!--- TBD: Edit this article.
* Admonitions/alerts may be overused in this article. Check once.
* An important alert at the end of this table does not make sense. Also, it has a code snippet inside it.
* Some screenshots like teamschannel.png may be redundant. Check once.
* Some headings use title case. We use sentence case for titles.
* Check for markdownlint errors. 
* Try using &nbsp; to add spaces in codeblocks for indentation and remove the hard tabs.
* Table with just a row is not really needed. Provide the content without tabulating it.
--->

请参阅以下视频，了解如何创建传出 Webhook：
<br>

> [!VIDEO https://www.microsoft.com/en-us/videoplayer/embed/RE4OIzu]
<br>

## <a name="key-features-of-outgoing-webhook"></a>传出 Webhook 的主要功能

下表提供了传出 Webhook 的功能和说明：

| 功能 | Description |
| ------- | ----------- |
| 作用域配置| Webhook 的作用域在团队级别。 每个强制设置过程都会添加一个传出 Webhook。 |
| 重新激活消息传递| 用户必须为 Webhook 使用 @提及功能才能接收消息。 目前，用户只能在公共频道中向传出 Webhook 发送消息，而不能在个人或私有作用域内发送消息。 |
|标准 HTTP 消息交换|响应与原始请求消息显示在同一链中，并且可以包含任何 Bot Framework 消息内容。 例如，格式文本、图像、卡片和表情符号。 尽管传出 Webhook 可以使用卡片，但它们不能使用除 `openURL` 以外的任何卡片操作。|
| Teams API 方法支持|传出 Webhook 会将 HTTP POST 发送到 Web 服务并获取响应。 它们无法访问任何其他 API，例如检索团队中的花名册或频道列表。|

## <a name="create-outgoing-webhooks"></a>创建传出 Webhook

创建传出 Webhook 并向 Teams 添加机器人。

若要创建传出 Webhook，请按照以下步骤操作：

1. 从左窗格中选择“**Teams**”。 此时将显示“**Teams**”页面：

    ![Teams 频道](~/assets/images/teamschannel.png)

1. 在“**Teams**”页面中，选择所需的团队以创建传出 Webhook，然后选择 &#8226;&#8226;&#8226;。在下拉菜单中，选择“**管理团队**”：

    ![创建传出 Webhook](~/assets/images/outgoingwebhook1.png)

1. 选择频道页面上的“**应用**”选项卡：

    ![创建传出 Webhook](~/assets/images/outgoingwebhook2.png)

1. 选择“**创建传出 Webhook**”：

    ![创建传出 Webhook](~/assets/images/outgoingwebhook3.png)

1. 在“**创建传出 Webhook**”页面中键入以下详细信息：

    * **名称**：Webhook 标题和“@提及”选项卡。
    * **回叫 URL**：接受 JSON 有效负载并接收来自 Teams 的 POST 请求的 HTTPS 终结点。
    * **说明**：显示在个人资料卡片和团队级应用仪表板中的详细字符串。
    * **个人资料图片**：Webhook 的应用图标，它为可选。

1. 选择“**创建**”。传出 Webhook 将添加到当前团队的频道中：

    ![创建传出 Webhook](~/assets/images/outgoingwebhook.png)

此时将显示“[基于哈希的消息身份验证代码 (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301)”对话框。 它是一个安全令牌，用于验证 Teams 与指定的外部服务之间的调用。 HMAC 安全令牌不会过期，并且对于每个配置都是唯一的。

>[!NOTE]
> 仅当 URL 有效并且服务器和客户端身份验证令牌相同时，团队的用户才可以使用传出 Webhook。例如，HMAC 握手。

以下方案提供了添加传出 Webhook 的详细信息：

* 方案：将 Teams 频道数据库服务器上的更改状态通知推送到你的应用。
* 示例: 你有一个业务线应用，它可以跟踪所有 CRUD (创建、读取、更新和删除) 操作。 Office 365 租户中的 Teams 频道 HR 用户可对员工记录执行这些操作。

# <a name="url-json-payload"></a>[URL JSON 有效负载](#tab/urljsonpayload)

**在应用服务器上创建 URL 以接受并处理具有 JSON 有效负载的 POST 请求**

你的服务将在标准 Azure 机器人服务消息传递架构中接收消息。 Bot Framework 连接器是一项 RESTful 服务，它支持通过 [Azure 机器人服务 API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference) 中所述的 HTTPS 协议来处理 JSON 格式消息的交换。 或者，你也可以通过 Microsoft Bot Framework SDK 来处理和解析消息。 有关详细信息，请参阅 [Azure 机器人服务概述](/azure/bot-service/bot-service-overview-introduction)。

传出 Webhook 的作用域为 `team` 级别，并且所有团队成员都可以看到。 用户需要 **\@提及** 传出 Webhook 的名称才能在频道中调用它。

# <a name="verify-hmac-token"></a>[验证 HMAC 令牌](#tab/verifyhmactoken)

**创建用于验证传出 Webhook HMAC 令牌的方法**

使用入站消息和 ID 的示例：SigningKeyDictionary 的“contoso”，{"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }。

在请求标头的授权中，使用值“HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=”。

为确保你的服务仅接收来自实际 Teams 客户端的调用，Teams 在 HTTP `hmac` 授权标头中提供了 HMAC 代码。始终在身份验证协议中包含 HMAC 代码。

你的代码必须始终验证请求中包含的 HMAC 签名，如下所示：

* 从邮件的请求正文生成 HMAC 令牌。 在大多数平台上都有执行此操作的标准库，例如 Node.js 的 [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) 和 C\# 的 [Teams Webhook 示例](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs)。 Microsoft Teams 使用标准 SHA256 HMAC 加密。 你必须将正文转换为采用 UTF8 格式的字节数组。
* 在客户端中注册传出 Webhook 时，将从 Teams 提供的安全令牌的字节数组计算哈希值。请参阅[创建传出 Webhook](#create-outgoing-webhook)。
* 将哈希值转换为使用 UTF-8 编码的字符串。
* 将生成的哈希字符串值与 HTTP 请求中提供的值进行比较。

# <a name="method-to-respond"></a>[回复方法](#tab/methodtorespond)

**创建发送成功或失败回复的方法**

来自传出 Webhook 的回复显示在与原始消息相同的回复链中。 当用户执行查询时，Teams 将向服务发出同步 HTTP 请求，并且你的代码在连接超时和终止之前有 5 秒时间回复消息。

### <a name="example-response"></a>示例响应

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

---

> [!NOTE]
>
> * 你可以使用传出 Webhook 将自适应卡片、主图卡片和短信作为附件发送。
> * 卡片支持设置格式。有关详细信息，请参阅[使用 Markdown 设置卡片格式](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown)。
> * 传出 Webhook 中的自适应卡片仅支持 `openURL` 卡片操作。

以下代码是自适应卡片答复的示例：

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

---

## <a name="code-sample"></a>代码示例

|**示例名称** | **说明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| 传出 webhook | 创建将在 Teams 中使用的自定义机器人的示例。| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## <a name="step-by-step-guide"></a>分步指南

按照[分步指南](../../sbs-outgoing-webhooks.yml)，在 Teams 中创建传出 Webhook。

## <a name="see-also"></a>另请参阅

* [创建传入 Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [创建 Office 365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [创建和发送邮件](~/webhooks-and-connectors/how-to/connectors-using.md)
