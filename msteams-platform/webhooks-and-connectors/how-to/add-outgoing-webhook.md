---
title: 使用传出 webhook Microsoft Teams自定义聊天机器人
description: 介绍如何添加传出 Webhook
ms.topic: conceptual
ms.author: lajanuar
localization_priority: Normal
keywords: teams 选项卡传出 Webhook 可操作邮件验证 webhook
ms.openlocfilehash: a5a0cdfc9080ac4567f438b6fb6fd0671df8c19f
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566528"
---
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a>向使用传出 webhook Teams自定义聊天机器人

## <a name="outgoing-webhooks-in-teams"></a>webhook 中的传出 webhook Teams

Webhook 是一种与外部Teams集成的方式。 webhook 实质上是发送到回调 URL 的 POST 请求。 传出 Webhook 允许用户向 Web 服务发送消息，而无需完成通过 Microsoft Bot Framework 创建[自动程序的完整过程](https://dev.botframework.com/)。

传出 webhook 将数据从 Teams发送到能够接受 JSON 有效负载的任何选定服务。 将传出 Webhook 添加到团队后，它充当机器人，使用 mention 在频道中查找 **\@ 消息**。 它将通知发送到外部 Web 服务，并响应丰富的消息，其中包括卡片和图像。

## <a name="outgoing-webhook-key-features"></a>传出 Webhook 关键功能

| 功能 | 说明 |
| ------- | ----------- |
| 作用域配置| Webhook 的范围在团队级别。 必须完成要添加传出 Webhook 的每个团队的安装过程。 |
| 反应消息| 用户必须使用 @mention webhook 接收消息。 目前，用户只能在公共频道（而不是个人或专用范围）中发送传出 Webhook 消息。 |
|标准 HTTP 邮件交换|响应显示在与原始请求消息相同的链中，并且可以包含任何自动程序框架消息内容，例如格式文本、图像、卡片和表情符号。 尽管传出 Webhook 可以使用卡片，但除了 以外，它们不能使用任何卡片操作 `openURL` 。|
| TeamsAPI 方法支持|传出 Webhook 将 HTTP POST 发送到 Web 服务并处理回响应。 他们无法访问任何其他 API，如检索团队中的名单或频道列表。|

## <a name="creating-actionable-messages"></a>创建可操作邮件

连接器卡包含卡片上的三个可见按钮。 每个按钮通过使用 `potentialAction` 操作在邮件的 属性 `ActionCard` 中定义。 每个 `ActionCard` 字段都包含一个输入类型;文本字段、日期选取器或多选项列表。 每个 `ActionCard` 操作都有一个关联的操作，例如， `HttpPOST` 。

连接器卡支持三种类型的操作：

| 操作 | 说明 |
| ------- | ----------- |
| `ActionCard` |显示一个或多个输入类型和关联的操作。|
| `HttpPOST` | 向 URL 发送 POST 请求。 |
| `OpenUri` |  在单独的浏览器或应用中打开 URI，并基于操作系统选择面向不同的 URI。|

`ActionCard` 操作支持三种输入类型：

| 输入类型 | 描述 |
| ------- | ----------- |
| `TextInput` | 具有可选长度限制的单行或多行文本字段。 |
| `DateInput` | 具有可选时间选择器的日期选择器。 |
| `MultichoiceInput` | 指定的选项列表，提供单个选择或多个选择。|

`MultichoiceInput` 支持 `style` 控制完全展开列表显示的属性。 的默认值 `style` 取决于 `isMultiSelect` 值。

| `isMultiSelect` value  | `style` 默认值  |
| --- | --- |
| `false` 或未指定 | 默认样式为 `compact`|
| `true` | 默认样式为 `expanded` |

> [!NOTE]
> * 如果要 `"isMultiSelect": true` 以紧凑样式显示多选列表，请输入 和 `"style": true` 。
> * 在 `compact` Microsoft `style` Teams中选择属性与在 Microsoft `normal` `style` Outlook。
> * Webhook 仅支持Office 365卡片和自适应卡片。

有关连接器卡操作的其他所有详细信息 **[，请参阅可](/outlook/actionable-messages/card-reference#actions)** 操作邮件卡参考中的操作。

## <a name="adding-outgoing-webhooks-to-your-app"></a>将传出 Webhook 添加到应用

**应用** 场景：将应用频道上的Teams状态数据库服务器推送到你的应用。  
**示例**：你拥有一个业务线应用，它通过跨租户的 TEAMS HR 用户跟踪对员工记录Office 365 CRUD 操作。

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a>1. 在应用服务器上创建 URL 以接受并处理具有 JSON 有效负载的 POST 请求

你的服务接收标准 Azure 自动程序服务消息架构中的邮件。 机器人框架连接器是一项 RESTful 服务，它使服务可以通过 HTTPS 协议处理 JSON 格式邮件的交换，如 [Azure Bot Service API 中记录](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)。 或者，你可以按照 [Microsoft Bot Framework SDK] 处理和分析消息。 另请参阅 [关于 Azure Bot 服务](/azure/bot-service/bot-service-overview-introduction)。


传出 Webhook 的范围为级别 `team` ，并且所有团队成员都可以看到。 就像机器人一样，用户需要 **\@ 提及** 传出 Webhook 的名称，以在频道中调用它。

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a>2. 创建用于验证传出 Webhook HMAC 令牌的方法

#### <a name="hmac-signature-for-testing-with-code-example"></a>用于测试的 HMAC 签名代码示例

使用入站邮件和 id 的示例：{"contoso"的 SigningKeyDictionary 的"contoso"，"vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }。

在请求标头的授权中，使用值"HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U="。

为了确保服务仅接收来自实际客户端Teams的呼叫，Teams HTTP 标头中提供 HMAC `hmac` 代码。 始终在身份验证协议中包含代码。

代码必须始终验证请求中包含的 HMAC 签名：

* 从邮件的请求正文生成 HMAC 令牌。 大多数平台上有要执行此操作的标准库， ([Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js或参阅 Teams [Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C \#) 。 Microsoft Teams使用标准 SHA256 HMAC 加密。 你需要在 UTF8 中将正文转换为字节数组。
* 在客户端中注册传出 webhook 时，计算由 Teams 提供的安全令牌的字节数组Teams哈希]。 请参阅 [创建传出 Webhook](#create-an-outgoing-webhook)。
* 使用 UTF-8 编码将哈希转换为字符串。
* 将生成的哈希的字符串值与 HTTP 请求中提供的值进行比较。

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a>3. 创建发送成功或失败响应的方法

来自传出 Webhook 的响应显示在与原始邮件相同的回复链中。 当用户执行查询时，Microsoft Teams向服务发出同步 HTTP 请求，您的代码将在连接中断和终止之前获取 5 秒钟来响应消息。

### <a name="example-response"></a>示例响应

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a>创建传出 Webhook

1. 选择相应的团队 **，然后从** " (&#8226;&#8226;&#8226;) "下拉菜单中选择"管理团队"。
1. 从导航 **栏中选择** "应用"选项卡。
1. 从窗口的右下角选择"**创建传出 Webhook"。**
1. 在生成的弹出窗口中，填写必填字段：

>* **名称**：Webhook 标题和@mention点击
>* **回调 URL：** 接受 JSON 有效负载并接收来自客户端的 POST 请求的 HTTPS Teams
>* **说明**：显示在配置文件卡片和团队级应用仪表板中的详细字符串
>* **个人资料图片**：Webhook 的可选应用图标
>* Select the **Create** button from the lower right corner of the pop-up window and the outgoing webhook are added to the current team's channels.
>* 下一个对话框窗口显示基于哈希的消息身份验证代码 ([HMAC](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301)) 安全令牌，该令牌用于对 Teams 和指定的外部服务之间的呼叫进行身份验证。
>* 仅在 URL 有效且服务器和客户端身份验证令牌相等（例如 HMAC 握手）时，传出 Webhook 才可供团队用户使用。

## <a name="code-sample"></a>代码示例
|**示例名称** | **说明** | **.NET** | **Node.js** |
|----------------|------------------|--------|----------------|
| 传出 webhook | 用于创建要 **用于自定义聊天** 机器人Microsoft Teams。| [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

