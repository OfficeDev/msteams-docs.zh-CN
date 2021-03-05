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
# <a name="add-custom-bots-to-teams-with-outgoing-webhooks"></a><span data-ttu-id="03a26-104">使用传出 Webhook 将自定义自动程序添加到 Teams</span><span class="sxs-lookup"><span data-stu-id="03a26-104">Add custom bots to Teams with outgoing webhooks</span></span>

## <a name="what-are-outgoing-webhooks-in-teams"></a><span data-ttu-id="03a26-105">Teams 中的传出 Webhook 是什么？</span><span class="sxs-lookup"><span data-stu-id="03a26-105">What are outgoing webhooks in Teams?</span></span>

<span data-ttu-id="03a26-106">Webhook 是 Teams 与外部应用集成的唯一方式。</span><span class="sxs-lookup"><span data-stu-id="03a26-106">Webhooks are an eminent way for Teams to integrate with external apps.</span></span> <span data-ttu-id="03a26-107">Webhook 实质上是发送到回调 URL 的 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="03a26-107">A webhook is essentially a POST request sent to a callback URL.</span></span> <span data-ttu-id="03a26-108">传出 Webhook 允许用户向 Web 服务发送消息，而无需完成通过 Microsoft Bot Framework 创建自动程序 [的完整过程](https://dev.botframework.com/)。</span><span class="sxs-lookup"><span data-stu-id="03a26-108">Outgoing webhooks allow users to send messages to your web service without going through the full process of creating bots via the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span>

<span data-ttu-id="03a26-109">传出 Webhook 将数据从 Teams 发送到能够接受 JSON 有效负载的任何选定服务。</span><span class="sxs-lookup"><span data-stu-id="03a26-109">Outgoing webhook sends data from Teams to any chosen service capable of accepting a JSON payload.</span></span> <span data-ttu-id="03a26-110">将传出 Webhook 添加到团队后，它充当机器人，使用提及在频道中查找 **\@ 消息**。</span><span class="sxs-lookup"><span data-stu-id="03a26-110">After adding the outgoing webhooks to a team, it acts as a bot and looks for messages in channels using **\@mention**.</span></span> <span data-ttu-id="03a26-111">它将通知发送到外部 Web 服务，并响应丰富的消息，其中包括卡片和图像。</span><span class="sxs-lookup"><span data-stu-id="03a26-111">It sends notifications to external web services and responds with rich messages, which include cards and images.</span></span>

## <a name="outgoing-webhook-key-features"></a><span data-ttu-id="03a26-112">传出 Webhook 关键功能</span><span class="sxs-lookup"><span data-stu-id="03a26-112">Outgoing webhook key features</span></span>

| <span data-ttu-id="03a26-113">功能</span><span class="sxs-lookup"><span data-stu-id="03a26-113">Feature</span></span> | <span data-ttu-id="03a26-114">说明</span><span class="sxs-lookup"><span data-stu-id="03a26-114">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="03a26-115">作用域配置</span><span class="sxs-lookup"><span data-stu-id="03a26-115">Scoped configuration</span></span>| <span data-ttu-id="03a26-116">Webhook 的范围在团队级别。</span><span class="sxs-lookup"><span data-stu-id="03a26-116">Webhooks are scoped at the team level.</span></span> <span data-ttu-id="03a26-117">必须完成要添加传出 Webhook 的每个团队的安装过程。</span><span class="sxs-lookup"><span data-stu-id="03a26-117">You must go through the setup process for each team where you want to add your outgoing webhook.</span></span> |
| <span data-ttu-id="03a26-118">反应消息</span><span class="sxs-lookup"><span data-stu-id="03a26-118">Reactive messaging</span></span>| <span data-ttu-id="03a26-119">用户必须使用 @mention webhook 接收邮件。</span><span class="sxs-lookup"><span data-stu-id="03a26-119">Users must use @mention for the webhook to receive messages.</span></span> <span data-ttu-id="03a26-120">目前，用户只能在公共频道（而不是个人或专用范围）中发送传出 Webhook 消息。</span><span class="sxs-lookup"><span data-stu-id="03a26-120">Currently, users can only message an outgoing webhook in public channels and not within the personal or private scope.</span></span> |
|<span data-ttu-id="03a26-121">标准 HTTP 邮件交换</span><span class="sxs-lookup"><span data-stu-id="03a26-121">Standard HTTP message exchange</span></span>|<span data-ttu-id="03a26-122">响应与原始请求消息在同一个链中，可以包括任何自动程序框架消息内容，例如格式文本、图像、卡片和表情符号。</span><span class="sxs-lookup"><span data-stu-id="03a26-122">Responses appear in the same chain as the original request message and can include any bot framework message content, for example, rich text, images, cards, and emojis.</span></span> <span data-ttu-id="03a26-123">尽管传出 Webhook 可以使用卡片，但除了 `openURL` .</span><span class="sxs-lookup"><span data-stu-id="03a26-123">Although outgoing webhooks can use cards, they cannot use any card actions except for `openURL`.</span></span>|
| <span data-ttu-id="03a26-124">Teams API 方法支持</span><span class="sxs-lookup"><span data-stu-id="03a26-124">Teams API method support</span></span>|<span data-ttu-id="03a26-125">传出 Webhook 将 HTTP POST 发送到 Web 服务并处理回响应。</span><span class="sxs-lookup"><span data-stu-id="03a26-125">Outgoing webhook sends an HTTP POST to a web service and process a response back.</span></span> <span data-ttu-id="03a26-126">他们无法访问任何其他 API，例如检索团队中的名单或频道列表。</span><span class="sxs-lookup"><span data-stu-id="03a26-126">They cannot access any other APIs like retrieve the roster or list of channels in a team.</span></span>|

## <a name="creating-actionable-messages"></a><span data-ttu-id="03a26-127">创建可操作邮件</span><span class="sxs-lookup"><span data-stu-id="03a26-127">Creating actionable messages</span></span>

<span data-ttu-id="03a26-128">连接器卡包含卡片上的三个可见按钮。</span><span class="sxs-lookup"><span data-stu-id="03a26-128">The connector cards include three visible buttons on the card.</span></span> <span data-ttu-id="03a26-129">每个按钮使用操作 `potentialAction` 在邮件属性中 `ActionCard` 定义。</span><span class="sxs-lookup"><span data-stu-id="03a26-129">Each button is defined in the `potentialAction` property of the message by using `ActionCard` actions.</span></span> <span data-ttu-id="03a26-130">每个 `ActionCard` 字段都包含一个输入类型;一个文本字段、一个日期选取器或一个多选项列表。</span><span class="sxs-lookup"><span data-stu-id="03a26-130">Each `ActionCard` contains an input type; a text field, a date picker, or a multi-choice list.</span></span> <span data-ttu-id="03a26-131">每个 `ActionCard` 操作都有一个关联的操作，例如 `HttpPOST` ，</span><span class="sxs-lookup"><span data-stu-id="03a26-131">Each `ActionCard` action has an associated action, for example, `HttpPOST`.</span></span>

<span data-ttu-id="03a26-132">连接器卡支持三种类型的操作：</span><span class="sxs-lookup"><span data-stu-id="03a26-132">Connector cards support three types of actions:</span></span>

| <span data-ttu-id="03a26-133">操作</span><span class="sxs-lookup"><span data-stu-id="03a26-133">Action</span></span> | <span data-ttu-id="03a26-134">说明</span><span class="sxs-lookup"><span data-stu-id="03a26-134">Description</span></span> |
| ------- | ----------- |
| `ActionCard` |<span data-ttu-id="03a26-135">显示一个或多个输入类型和关联的操作。</span><span class="sxs-lookup"><span data-stu-id="03a26-135">Presents one or more input types and associated actions.</span></span>|
| `HttpPOST` | <span data-ttu-id="03a26-136">向 URL 发送 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="03a26-136">Sends a POST request to a URL.</span></span> |
| `OpenUri` |  <span data-ttu-id="03a26-137">在单独的浏览器或应用中打开 URI，根据操作系统选择面向不同的 URI。</span><span class="sxs-lookup"><span data-stu-id="03a26-137">Opens a URI in a separate browser or app, optionally targets different URIs based on operating systems.</span></span>|

<span data-ttu-id="03a26-138">`ActionCard` 操作支持三种输入类型：</span><span class="sxs-lookup"><span data-stu-id="03a26-138">The `ActionCard` action supports three input types:</span></span>

| <span data-ttu-id="03a26-139">输入类型</span><span class="sxs-lookup"><span data-stu-id="03a26-139">Input type</span></span> | <span data-ttu-id="03a26-140">说明</span><span class="sxs-lookup"><span data-stu-id="03a26-140">Description</span></span> |
| ------- | ----------- |
| `TextInput` | <span data-ttu-id="03a26-141">具有可选长度限制的单行或多行文本字段。</span><span class="sxs-lookup"><span data-stu-id="03a26-141">A single-line or multiline text field with an optional length limit.</span></span> |
| `DateInput` | <span data-ttu-id="03a26-142">具有可选时间选择器的日期选择器。</span><span class="sxs-lookup"><span data-stu-id="03a26-142">A date selector with an optional time selector.</span></span> |
| `MultichoiceInput` | <span data-ttu-id="03a26-143">指定的选项列表，提供单个选择或多个选择。</span><span class="sxs-lookup"><span data-stu-id="03a26-143">A specified list of choices, offering either a single selection or multiple selections.</span></span>|

<span data-ttu-id="03a26-144">`MultichoiceInput` 支持 `style` 控制完全展开列表显示的属性。</span><span class="sxs-lookup"><span data-stu-id="03a26-144">`MultichoiceInput` supports a `style` property that controls the display of a fully expanded list.</span></span> <span data-ttu-id="03a26-145">默认值取决于 `style` `isMultiSelect` 值。</span><span class="sxs-lookup"><span data-stu-id="03a26-145">The default value of `style` depends on the `isMultiSelect` value.</span></span>

| <span data-ttu-id="03a26-146">`isMultiSelect` value</span><span class="sxs-lookup"><span data-stu-id="03a26-146">`isMultiSelect` value</span></span>  | <span data-ttu-id="03a26-147">`style` 默认值</span><span class="sxs-lookup"><span data-stu-id="03a26-147">`style` default value</span></span>  |
| --- | --- |
| <span data-ttu-id="03a26-148">`false` 或未指定</span><span class="sxs-lookup"><span data-stu-id="03a26-148">`false` or not specified</span></span> | <span data-ttu-id="03a26-149">默认样式为 `compact`</span><span class="sxs-lookup"><span data-stu-id="03a26-149">The default style is `compact`</span></span>|
| `true` | <span data-ttu-id="03a26-150">默认样式为 `expanded`</span><span class="sxs-lookup"><span data-stu-id="03a26-150">The default style is `expanded`</span></span> |

> [!NOTE]
> * <span data-ttu-id="03a26-151">如果希望多选列表以紧凑样式显示，请输入和 `"isMultiSelect": true` `"style": true` 。</span><span class="sxs-lookup"><span data-stu-id="03a26-151">Enter both `"isMultiSelect": true` and `"style": true`, if you want the multi-select list to be displayed in a compact style.</span></span>
> * <span data-ttu-id="03a26-152">在 Teams 中选择属性与选择 `compact` Microsoft `style` Outlook `normal` `style` 中的属性相同。</span><span class="sxs-lookup"><span data-stu-id="03a26-152">Selecting `compact` for the `style` property in Teams is the same as selecting `normal` for the `style` property in Microsoft Outlook.</span></span>
> * <span data-ttu-id="03a26-153">Webhook 仅支持 Office 365 邮件回卡和自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="03a26-153">Webhooks support only Office 365 message back cards and adaptive cards.</span></span>

<span data-ttu-id="03a26-154">有关连接器卡操作的其他所有详细信息 **[，请参阅可](/outlook/actionable-messages/card-reference#actions)** 操作邮件卡参考中的操作。</span><span class="sxs-lookup"><span data-stu-id="03a26-154">For all other details about connector card actions, see **[Actions](/outlook/actionable-messages/card-reference#actions)** in the actionable message card reference.</span></span>

## <a name="adding-outgoing-webhooks-to-your-app"></a><span data-ttu-id="03a26-155">向应用添加传出 Webhook</span><span class="sxs-lookup"><span data-stu-id="03a26-155">Adding outgoing webhooks to your app</span></span>

<span data-ttu-id="03a26-156">**应用** 场景：将 Teams 频道上的更改状态数据库服务器推送到你的应用。</span><span class="sxs-lookup"><span data-stu-id="03a26-156">**Scenario**: Push change status notifications on a Teams channel database server to your app.</span></span>  
<span data-ttu-id="03a26-157">**示例**：你有一个业务线应用，可跟踪 Teams 渠道 HR 用户在 Office 365 租赁中对员工记录执行的所有 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="03a26-157">**Example**: You have a line-of-business app that tracks all CRUD operations made to employee records by Teams channel HR users across an Office 365 tenancy.</span></span>

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a><span data-ttu-id="03a26-158">1. 在应用服务器上创建 URL 以接受并处理具有 JSON 负载的 POST 请求</span><span class="sxs-lookup"><span data-stu-id="03a26-158">1. Create a URL on your app's server to accept and process a POST request with a JSON payload</span></span>

<span data-ttu-id="03a26-159">服务接收标准 Azure 自动程序服务消息架构中的邮件。</span><span class="sxs-lookup"><span data-stu-id="03a26-159">Your service receives messages in a standard Azure bot service messaging schema.</span></span> <span data-ttu-id="03a26-160">自动程序框架连接器是一项 RESTful 服务，它使服务可以通过 HTTPS 协议处理 JSON 格式邮件的交换，如 [Azure Bot Service API 中记录](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="03a26-160">The bot framework connector is a RESTful service that empowers your service to process the interchange of JSON formatted messages via HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).</span></span> <span data-ttu-id="03a26-161">或者，你可以按照 [Microsoft Bot Framework SDK] 处理和分析消息。</span><span class="sxs-lookup"><span data-stu-id="03a26-161">Alternatively, you can follow the [Microsoft Bot Framework SDK] to process and parse messages.</span></span> <span data-ttu-id="03a26-162">另请参阅 [关于 Azure 自动程序服务](/azure/bot-service/bot-service-overview-introduction)。</span><span class="sxs-lookup"><span data-stu-id="03a26-162">See also [About Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).</span></span>


<span data-ttu-id="03a26-163">传出 Webhook 的范围是级别 `team` ，并且所有团队成员都可以看到。</span><span class="sxs-lookup"><span data-stu-id="03a26-163">Outgoing webhooks are scoped to the `team` level and are visible to all the team members.</span></span> <span data-ttu-id="03a26-164">与机器人一样，用户需要 **\@ 提及** 传出 Webhook 的名称，以在频道中调用它。</span><span class="sxs-lookup"><span data-stu-id="03a26-164">Just like a bot, users need to **\@mention** the name of the outgoing webhook to invoke it in the channel.</span></span>

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a><span data-ttu-id="03a26-165">2. 创建验证传出 Webhook HMAC 令牌的方法</span><span class="sxs-lookup"><span data-stu-id="03a26-165">2. Create a method to verify the outgoing webhook HMAC token</span></span>

#### <a name="hmac-signature-for-testing-with-code-example"></a><span data-ttu-id="03a26-166">用于测试代码示例的 HMAC 签名</span><span class="sxs-lookup"><span data-stu-id="03a26-166">HMAC signature for testing with code example</span></span>

<span data-ttu-id="03a26-167">使用入站邮件和 ID 的示例："contoso"的 SigningKeyDictionary 的"contoso"，"vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }。</span><span class="sxs-lookup"><span data-stu-id="03a26-167">Using example of inbound message and id: "contoso" of SigningKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.</span></span>

<span data-ttu-id="03a26-168">在请求标头的授权中，使用值"HMAC 03TCao0i55H1eVKUusZORjtvYTs+mO41mPL+R1e1U="。</span><span class="sxs-lookup"><span data-stu-id="03a26-168">Use the value "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" in the authorization of request header.</span></span>

<span data-ttu-id="03a26-169">为了确保你的服务仅接收来自实际 Teams 客户端的呼叫，Teams 在 HTTP 标头中提供了 HMAC `hmac` 代码。</span><span class="sxs-lookup"><span data-stu-id="03a26-169">To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC code in the HTTP `hmac` header.</span></span> <span data-ttu-id="03a26-170">始终在身份验证协议中包含代码。</span><span class="sxs-lookup"><span data-stu-id="03a26-170">Always included the code in your authentication protocol.</span></span>

<span data-ttu-id="03a26-171">您的代码必须始终验证请求中包含的 HMAC 签名：</span><span class="sxs-lookup"><span data-stu-id="03a26-171">Your code must always validate the HMAC signature included in the request:</span></span>

* <span data-ttu-id="03a26-172">从邮件的请求正文生成 HMAC 令牌。</span><span class="sxs-lookup"><span data-stu-id="03a26-172">Generate the HMAC token from the request body of the message.</span></span> <span data-ttu-id="03a26-173">在大部分平台上，有一些标准库可以 ([加密](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js或查看适用于 C) 的 [Teams Webhook](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) \# 示例。</span><span class="sxs-lookup"><span data-stu-id="03a26-173">There are standard libraries to do this on most platforms (see [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js or see [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#).</span></span> <span data-ttu-id="03a26-174">Microsoft Teams 使用标准 SHA256 HMAC 加密。</span><span class="sxs-lookup"><span data-stu-id="03a26-174">Microsoft Teams uses standard SHA256 HMAC cryptography.</span></span> <span data-ttu-id="03a26-175">你需要在 UTF8 中将正文转换为字节数组。</span><span class="sxs-lookup"><span data-stu-id="03a26-175">You need to convert the body to a byte array in UTF8.</span></span>
* <span data-ttu-id="03a26-176">从 Teams 在 **Teams** 客户端中注册传出 Webhook 时提供的安全令牌的字节数组计算哈希。</span><span class="sxs-lookup"><span data-stu-id="03a26-176">Compute the hash from the byte array of the security token **provided by Teams** when you registered the outgoing webhook in the Teams client].</span></span> <span data-ttu-id="03a26-177">请参阅["创建传出 Webhook"。](#create-an-outgoing-webhook)</span><span class="sxs-lookup"><span data-stu-id="03a26-177">See [Create an outgoing webhook](#create-an-outgoing-webhook).</span></span>
* <span data-ttu-id="03a26-178">使用 UTF-8 编码将哈希转换为字符串。</span><span class="sxs-lookup"><span data-stu-id="03a26-178">Convert the hash to a string using UTF-8 encoding.</span></span>
* <span data-ttu-id="03a26-179">将生成的哈希的字符串值与 HTTP 请求中提供的值进行比较。</span><span class="sxs-lookup"><span data-stu-id="03a26-179">Compare the string value of the generated hash with the value provided in the HTTP request.</span></span>

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a><span data-ttu-id="03a26-180">3. 创建发送成功或失败响应的方法</span><span class="sxs-lookup"><span data-stu-id="03a26-180">3. Create a method to send a success or failure response</span></span>

<span data-ttu-id="03a26-181">传出 Webhook 的响应与原始邮件显示在相同的回复链中。</span><span class="sxs-lookup"><span data-stu-id="03a26-181">Responses from your outgoing webhooks appear in the same reply chain as the original message.</span></span> <span data-ttu-id="03a26-182">当用户执行查询时，Microsoft Teams 会向你的服务发出同步 HTTP 请求，你的代码在连接停止和终止之前获取 5 秒钟来响应消息。</span><span class="sxs-lookup"><span data-stu-id="03a26-182">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code gets five seconds to respond to the message before the connection times out and terminates.</span></span>

### <a name="example-response"></a><span data-ttu-id="03a26-183">示例响应</span><span class="sxs-lookup"><span data-stu-id="03a26-183">Example response</span></span>

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a><span data-ttu-id="03a26-184">创建传出 Webhook</span><span class="sxs-lookup"><span data-stu-id="03a26-184">Create an outgoing webhook</span></span>

1. <span data-ttu-id="03a26-185">选择相应的团队 **，然后从** " (&#8226;&#8226;&#8226;) "下拉菜单中选择"管理团队"。</span><span class="sxs-lookup"><span data-stu-id="03a26-185">Select the appropriate team and choose **Manage team** from the (&#8226;&#8226;&#8226;) drop-down menu.</span></span>
1. <span data-ttu-id="03a26-186">从导航 **栏中** 选择"应用"选项卡。</span><span class="sxs-lookup"><span data-stu-id="03a26-186">Choose the **Apps** tab from the navigation bar.</span></span>
1. <span data-ttu-id="03a26-187">从窗口的右下角选择 **"创建传出 Webhook"。**</span><span class="sxs-lookup"><span data-stu-id="03a26-187">From the window's lower right corner select **Create an outgoing webhook**.</span></span>
1. <span data-ttu-id="03a26-188">在生成的弹出窗口中，填写必填字段：</span><span class="sxs-lookup"><span data-stu-id="03a26-188">In the resulting popup window complete the required fields:</span></span>

>* <span data-ttu-id="03a26-189">**名称** - webhook 标题和@mention点击。</span><span class="sxs-lookup"><span data-stu-id="03a26-189">**Name** - The webhook title and @mention tap.</span></span>
>* <span data-ttu-id="03a26-190">**回调 URL** - 接受 JSON 有效负载并接收来自 Teams 的 POST 请求的 HTTPS 终结点。</span><span class="sxs-lookup"><span data-stu-id="03a26-190">**Callback URL** - The HTTPS endpoint that accepts JSON payloads and receives POST requests from Teams.</span></span>
>* <span data-ttu-id="03a26-191">**说明** - 显示在配置文件卡片和团队级应用仪表板中的详细字符串。</span><span class="sxs-lookup"><span data-stu-id="03a26-191">**Description** - A detailed string that appear in the profile card and the team-level App dashboard.</span></span>
>* <span data-ttu-id="03a26-192">**配置文件图片** 是 Webhook 的可选应用图标。</span><span class="sxs-lookup"><span data-stu-id="03a26-192">**Profile Picture** an optional app icon for your webhook.</span></span>
>* <span data-ttu-id="03a26-193">Select the **Create** button from the lower right corner of the pop-up window and the outgoing webhook are added to the current team's channels.</span><span class="sxs-lookup"><span data-stu-id="03a26-193">Select the **Create** button from the lower right corner of the pop-up window and the outgoing webhook are added to the current team's channels.</span></span>
>* <span data-ttu-id="03a26-194">下一个对话框窗口显示基于哈希的消息身份验证代码 [ (HMAC ](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301)) 安全令牌，用于对 Teams 和指定的外部服务之间的调用进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="03a26-194">The next dialog window displays an [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) security token that is used to authenticate calls between Teams and the designated outside service.</span></span>
>* <span data-ttu-id="03a26-195">传出 Webhook 仅在 URL 有效且服务器和客户端身份验证令牌相等（例如 HMAC 握手）时，才可供团队用户使用。</span><span class="sxs-lookup"><span data-stu-id="03a26-195">The outgoing webhook is available to the team's users, only if the URL is valid and the server and client authentication tokens are equal for example, an HMAC handshake.</span></span>

## <a name="code-sample"></a><span data-ttu-id="03a26-196">代码示例</span><span class="sxs-lookup"><span data-stu-id="03a26-196">Code sample</span></span>
|<span data-ttu-id="03a26-197">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="03a26-197">**Sample name**</span></span> | <span data-ttu-id="03a26-198">**说明**</span><span class="sxs-lookup"><span data-stu-id="03a26-198">**Description**</span></span> | <span data-ttu-id="03a26-199">**.NET**</span><span class="sxs-lookup"><span data-stu-id="03a26-199">**.NET**</span></span> | <span data-ttu-id="03a26-200">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="03a26-200">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="03a26-201">传出 Webhook</span><span class="sxs-lookup"><span data-stu-id="03a26-201">Outgoing webhooks</span></span> | <span data-ttu-id="03a26-202">用于创建 Microsoft Teams **中使用的** 自定义自动程序的示例。</span><span class="sxs-lookup"><span data-stu-id="03a26-202">Samples to create **Custom Bots** to be used in Microsoft Teams.</span></span>| [<span data-ttu-id="03a26-203">View</span><span class="sxs-lookup"><span data-stu-id="03a26-203">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [<span data-ttu-id="03a26-204">View</span><span class="sxs-lookup"><span data-stu-id="03a26-204">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

