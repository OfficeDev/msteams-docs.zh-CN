---
title: 向带有传出 webhook 的 Microsoft 团队添加自定义 bot
author: laujan
description: ''
keywords: 团队选项卡传出 webhook *
ms.topic: conceptual
ms.author: laujan
ms.openlocfilehash: 4881dc8768c7c51947f6a80a55affe78c28874d3
ms.sourcegitcommit: 3ba5a5a7d9d9d906abc3ee1df9c2177de0cfd767
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2020
ms.locfileid: "45102996"
---
# <a name="add-custom-bots-to-microsoft-teams-with-outgoing-webhooks"></a>向带有传出 webhook 的 Microsoft 团队添加自定义 bot

## <a name="what-are-outgoing-webhooks-in-teams"></a>什么是团队中的传出 webhook？

Webhook 是团队与外部应用程序集成的一种极好的方式。 Webhook 实质上是发送给回调 URL 的 POST 请求。 在团队中，传出 webhook 提供了一种简单的方法，允许用户向 web 服务发送邮件，而无需完成通过[Microsoft Bot 框架](https://dev.botframework.com/)创建 bot 的整个过程。 传出 webhook 将数据从团队发布到任何能够接受 JSON 有效负载的选定服务。 将传出 webhook 添加到团队后，它就像 bot 一样，使用** \@ 提及**的消息侦听通道，将通知发送到外部 web 服务，并响应可包含卡片和图像的丰富邮件。

## <a name="outgoing-webhook-key-features"></a>传出 webhook 密钥功能

| 功能 | 说明 |
| ------- | ----------- |
| 作用域配置| Webhook 在团队级别范围内。 您需要完成每个要向其添加传出 webhook 的团队的安装过程。 |
| 响应消息| 用户必须使用 webhook 的 @mention 来接收邮件。 当前用户只能将公用通道中的传出 webhook （而不能在个人或专用范围内）发送邮件 |
|标准 HTTP 邮件交换|响应将显示在原始请求邮件所在的同一链中，并且可以包括任何 Bot 框架邮件内容 (格式文本、图像、卡片和表情符号) 。 **注意**：虽然传出 webhook 可以使用卡片，但不能使用除之外的任何卡片操作 `openURL` 。|
| 团队 API 方法支持|在团队中，传出 webhook 向 web 服务发送 HTTP POST 并处理回复。 他们不能访问任何其他 Api，如检索团队中的名单或频道列表。|

## <a name="adding-outgoing-webhook-processing-to-your-app"></a>将传出 webhook 处理添加到您的应用程序

**方案**：将团队频道数据库服务器上的更改状态通知推送到您的应用程序。  
**示例**：您具有一条业务线应用程序，用于跟踪团队频道用户在 Office 365 租赁中对雇员记录所做的所有 CRUD 操作。

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. 在应用程序的服务器上创建 URL，以使用 JSON 有效负载接受和处理 POST 请求

你的服务将在标准 Azure bot 服务消息架构中接收邮件。 Bot 框架连接器是一项 RESTful 服务，它使服务能够通过 HTTPS 协议（如[Azure Bot 服务 API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)中所述）处理 JSON 格式的邮件交换。 或者，您可以按照 [Microsoft Bot 框架 SDK] 来处理和分析邮件。 *另请参阅*  [关于 Azure Bot 服务](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0)。

传出 webhook 的范围限定为 `team` 级别，并且对团队的所有成员都可见。 就像 bot 一样，用户需要在通道中** \@ 提及**传出 webhook 的名称来调用它。

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. 创建用于验证传出 webhook HMAC 令牌的方法

为了确保服务仅接收来自实际团队客户端的呼叫，团队在 HTTP 头中提供了一个在 `hmac` 您的身份验证协议中应始终包含的 HMAC 代码。

您的代码应始终验证请求中包含的 HMAC 签名：

* 从邮件的请求正文*生成*HMAC 令牌。 在大多数平台上，有一些标准库可执行此操作 (*请参阅*Node.js 的[加密](https://nodejs.org/api/crypto.html#crypto_crypto)或*参阅*适用于 C 的[团队 Webhook 示例](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) \#) 。 Microsoft 团队使用标准 SHA256 HMAC 加密。 您需要将正文转换为 UTF8 形式的字节数组。
* 当您在团队客户端中注册了传出 webhook 时，从**团队提供**的安全令牌的字节数组中*计算*哈希值。 *请参阅*下面的[创建传出 webhook](#create-an-outgoing-webhook)。
* 使用 UTF-8 编码将哈希值*转换*为字符串。
* 将生成的哈希的字符串值与 HTTP 请求中提供的值*进行比较*。

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. 创建用于发送成功或失败响应的方法

来自你的传出 webhook 的响应将显示在与原始邮件相同的答复链中。 当用户执行查询时，Microsoft 团队会向您的服务发出同步 HTTP 请求，并且您的代码将有5秒的时间来响应邮件，然后连接超时并终止。

### <a name="example-response"></a>示例响应

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a>创建传出 Webhook

1. 选择适当的团队，然后从 ( # A3) 下拉菜单中选择 "**管理团队**"。
1. 从导航栏中选择 "**应用**" 选项卡。
1. 从窗口的右下角选择 "**创建传出 webhook**"。
1. 在随后出现的弹出窗口中，完成必需的字段：

>* **Name** -webhook 标题和 @mention 点击。
>* **回调 URL** -将接受 JSON 有效负载的 HTTPS 终结点，并将接收来自团队的 POST 请求。
>* **Description** -将显示在配置文件卡片和团队级应用仪表板中的详细字符串。
>*  (可选) webhook 的应用程序图标的**个人资料图片**。
>* 从弹出窗口的右下角选择 "**创建**" 按钮，并将传出 webhook 添加到当前团队的通道中。
>* 下一个对话框窗口将显示[基于哈希的邮件身份验证代码 (HMAC) ](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301)安全令牌，该代码将用于在团队和指定的外部服务之间进行身份验证调用。
>* 如果 URL 有效且服务器和客户端身份验证令牌相等 (即 HMAC 握手) ，则会向团队用户提供传出 webhook。

## <a name="code-samples"></a>代码示例

您可以查看 GitHub 上的传出 webhook 代码示例：

### <a name="nodejs"></a>Node.js

[OfficeDev/msteams-示例-传出-webhook-nodejs](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs)

### <a name="c"></a>Lc\#

[OfficeDev/microsoft-团队-示例-传出-webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook)
