---
title: 使用传出 Webhook 将自定义自动程序添加到 Microsoft Teams
description: 介绍如何添加传出 Webhook
ms.topic: conceptual
ms.author: lajanuar
keywords: Teams 选项卡传出 Webhook 可操作邮件验证 webhook
ms.openlocfilehash: b7c587816a32e650009cdbfcd4dcf9028fb87392
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449540"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a>使用传出 Webhook 将自定义自动程序添加到 Teams

## <a name="what-are-outgoing-webhooks-in-teams"></a>Teams 中的传出 Webhook 是什么？

Webhook 是 Teams 与外部应用集成的唯一方式。 Webhook 实质上是发送到回调 URL 的 POST 请求。 传出 Webhook 允许用户向 Web 服务发送消息，而无需完成通过 Microsoft Bot Framework 创建自动程序 [的完整过程](https://dev.botframework.com/)。

传出 Webhook 将数据从 Teams 发送到能够接受 JSON 有效负载的任何选定服务。 将传出 Webhook 添加到团队后，它充当机器人，使用提及在频道中查找 **\@ 消息**。 它将通知发送到外部 Web 服务，并响应丰富的消息，其中包括卡片和图像。

## <a name="outgoing-webhook-key-features"></a>传出 Webhook 关键功能

| 功能 | 说明 |
| ------- | ----------- |
| 作用域配置| Webhook 的范围在团队级别。 必须完成要添加传出 Webhook 的每个团队的安装过程。 |
| 反应消息| 用户必须使用 @mention webhook 接收邮件。 目前，用户只能在公共频道（而不是个人或专用范围）中发送传出 Webhook 消息。 |
|标准 HTTP 邮件交换|响应与原始请求消息在同一个链中，可以包括任何自动程序框架消息内容，例如格式文本、图像、卡片和表情符号。 尽管传出 Webhook 可以使用卡片，但除了 `openURL` .|
| Teams API 方法支持|传出 Webhook 将 HTTP POST 发送到 Web 服务并处理回响应。 他们无法访问任何其他 API，例如检索团队中的名单或频道列表。|

## <a name="creating-actionable-messages"></a>创建可操作邮件

连接器卡包含卡片上的三个可见按钮。 每个按钮使用操作 `potentialAction` 在邮件属性中 `ActionCard` 定义。 每个 `ActionCard` 字段都包含一个输入类型;一个文本字段、一个日期选取器或一个多选项列表。 每个 `ActionCard` 操作都有一个关联的操作，例如 `HttpPOST` ，

连接器卡支持三种类型的操作：

| 操作 | 说明 |
| ------- | ----------- |
| `ActionCard` |显示一个或多个输入类型和关联的操作。|
| `HttpPOST` | 向 URL 发送 POST 请求。 |
| `OpenUri` |  在单独的浏览器或应用中打开 URI，根据操作系统选择面向不同的 URI。|

`ActionCard` 操作支持三种输入类型：

| 输入类型 | 说明 |
| ------- | ----------- |
| `TextInput` | 具有可选长度限制的单行或多行文本字段。 |
| `DateInput` | 具有可选时间选择器的日期选择器。 |
| `MultichoiceInput` | 指定的选项列表，提供单个选择或多个选择。|

`MultichoiceInput` 支持 `style` 控制完全展开列表显示的属性。 默认值取决于 `style` `isMultiSelect` 值。

| `isMultiSelect` value  | `style` 默认值  |
| --- | --- |
| `false` 或未指定 | 默认样式为 `compact`|
| `true` | 默认样式为 `expanded` |

> [!NOTE]
> * 如果希望多选列表以紧凑样式显示，请输入和 `"isMultiSelect": true` `"style": true` 。
> * 在 Teams 中选择属性与选择 `compact` Microsoft `style` Outlook `normal` `style` 中的属性相同。
> * Webhook 仅支持 Office 365 邮件回卡和自适应卡片。

有关连接器卡操作的其他所有详细信息 **[，请参阅可](/outlook/actionable-messages/card-reference#actions)** 操作邮件卡参考中的操作。

## <a name="adding-outgoing-webhooks-to-your-app"></a>向应用添加传出 Webhook

**应用** 场景：将 Teams 频道上的更改状态数据库服务器推送到你的应用。  
**示例**：你有一个业务线应用，可跟踪 Teams 渠道 HR 用户在 Office 365 租赁中对员工记录执行的所有 CRUD 操作。

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. 在应用服务器上创建 URL 以接受并处理具有 JSON 负载的 POST 请求

服务接收标准 Azure 自动程序服务消息架构中的邮件。 自动程序框架连接器是一项 RESTful 服务，它使服务可以通过 HTTPS 协议处理 JSON 格式邮件的交换，如 [Azure Bot Service API 中记录](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)。 或者，你可以按照 [Microsoft Bot Framework SDK] 处理和分析消息。 另请参阅 [关于 Azure 自动程序服务](/azure/bot-service/bot-service-overview-introduction)。


传出 Webhook 的范围是级别 `team` ，并且所有团队成员都可以看到。 与机器人一样，用户需要 **\@ 提及** 传出 Webhook 的名称，以在频道中调用它。

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. 创建验证传出 Webhook HMAC 令牌的方法

#### <a name="hmac-signature-for-testing-with-code-example"></a>用于测试代码示例的 HMAC 签名

使用入站邮件和 ID 的示例："contoso"的 SigningKeyDictionary 的"contoso"，"vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }。

在请求标头的授权中，使用值"HMAC 03TCao0i55H1eVKUusZORjtvYTs+mO41mPL+R1e1U="。

为了确保你的服务仅接收来自实际 Teams 客户端的呼叫，Teams 在 HTTP 标头中提供了 HMAC `hmac` 代码。 始终在身份验证协议中包含代码。

您的代码必须始终验证请求中包含的 HMAC 签名：

* 从邮件的请求正文生成 HMAC 令牌。 在大部分平台上，有一些标准库可以 ([加密](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js或查看适用于 C) 的 [Teams Webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) \# 示例。 Microsoft Teams 使用标准 SHA256 HMAC 加密。 你需要在 UTF8 中将正文转换为字节数组。
* 从 Teams 在 **Teams** 客户端中注册传出 Webhook 时提供的安全令牌的字节数组计算哈希。 请参阅["创建传出 Webhook"。](#create-an-outgoing-webhook)
* 使用 UTF-8 编码将哈希转换为字符串。
* 将生成的哈希的字符串值与 HTTP 请求中提供的值进行比较。

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. 创建发送成功或失败响应的方法

传出 Webhook 的响应与原始邮件显示在相同的回复链中。 当用户执行查询时，Microsoft Teams 会向你的服务发出同步 HTTP 请求，你的代码在连接停止和终止之前获取 5 秒钟来响应消息。

### <a name="example-response"></a>示例响应

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a>创建传出 Webhook

1. 选择相应的团队 **，然后从** " (&#8226;&#8226;&#8226;) "下拉菜单中选择"管理团队"。
1. 从导航 **栏中** 选择"应用"选项卡。
1. 从窗口的右下角选择 **"创建传出 Webhook"。**
1. 在生成的弹出窗口中，填写必填字段：

>* **名称** - webhook 标题和@mention点击。
>* **回调 URL** - 接受 JSON 有效负载并接收来自 Teams 的 POST 请求的 HTTPS 终结点。
>* **说明** - 显示在配置文件卡片和团队级应用仪表板中的详细字符串。
>* **配置文件图片** 是 Webhook 的可选应用图标。
>* Select the **Create** button from the lower right corner of the pop-up window and the outgoing webhook are added to the current team's channels.
>* 下一个对话框窗口显示基于哈希的消息身份验证代码 [ (HMAC ](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301)) 安全令牌，用于对 Teams 和指定的外部服务之间的调用进行身份验证。
>* 传出 Webhook 仅在 URL 有效且服务器和客户端身份验证令牌相等（例如 HMAC 握手）时，才可供团队用户使用。

## <a name="code-sample"></a>代码示例
|**示例名称** | **说明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| 传出 Webhook | 用于创建 Microsoft Teams **中使用的** 自定义自动程序的示例。| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

