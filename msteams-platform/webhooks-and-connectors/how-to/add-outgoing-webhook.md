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
# <a name="add-custom-bots-to-microsoft-teams-with-outgoing-webhooks"></a><span data-ttu-id="ebe45-103">向带有传出 webhook 的 Microsoft 团队添加自定义 bot</span><span class="sxs-lookup"><span data-stu-id="ebe45-103">Add custom bots to Microsoft Teams with outgoing webhooks</span></span>

## <a name="what-are-outgoing-webhooks-in-teams"></a><span data-ttu-id="ebe45-104">什么是团队中的传出 webhook？</span><span class="sxs-lookup"><span data-stu-id="ebe45-104">What are outgoing webhooks in Teams?</span></span>

<span data-ttu-id="ebe45-105">Webhook 是团队与外部应用程序集成的一种极好的方式。</span><span class="sxs-lookup"><span data-stu-id="ebe45-105">Webhooks are a great way for Teams to integrate with external apps.</span></span> <span data-ttu-id="ebe45-106">Webhook 实质上是发送给回调 URL 的 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="ebe45-106">A webhook is essentially a POST request sent to a callback URL.</span></span> <span data-ttu-id="ebe45-107">在团队中，传出 webhook 提供了一种简单的方法，允许用户向 web 服务发送邮件，而无需完成通过[Microsoft Bot 框架](https://dev.botframework.com/)创建 bot 的整个过程。</span><span class="sxs-lookup"><span data-stu-id="ebe45-107">In Teams, outgoing webhooks provide a simple way to allow users to send messages to your web service without having to go through the full process of creating bots via the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span> <span data-ttu-id="ebe45-108">传出 webhook 将数据从团队发布到任何能够接受 JSON 有效负载的选定服务。</span><span class="sxs-lookup"><span data-stu-id="ebe45-108">Outgoing webhooks post data from Teams to any chosen service capable of accepting a JSON payload.</span></span> <span data-ttu-id="ebe45-109">将传出 webhook 添加到团队后，它就像 bot 一样，使用\*\* \@ 提及\*\*的消息侦听通道，将通知发送到外部 web 服务，并响应可包含卡片和图像的丰富邮件。</span><span class="sxs-lookup"><span data-stu-id="ebe45-109">Once an outgoing webhook is added to a team, it acts like bot, listening in channels for messages using **\@mention**, sending notifications to external web services, and responding with rich messages that can include cards and images.</span></span>

## <a name="outgoing-webhook-key-features"></a><span data-ttu-id="ebe45-110">传出 webhook 密钥功能</span><span class="sxs-lookup"><span data-stu-id="ebe45-110">Outgoing webhook key features</span></span>

| <span data-ttu-id="ebe45-111">功能</span><span class="sxs-lookup"><span data-stu-id="ebe45-111">Feature</span></span> | <span data-ttu-id="ebe45-112">说明</span><span class="sxs-lookup"><span data-stu-id="ebe45-112">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="ebe45-113">作用域配置</span><span class="sxs-lookup"><span data-stu-id="ebe45-113">Scoped Configuration</span></span>| <span data-ttu-id="ebe45-114">Webhook 在团队级别范围内。</span><span class="sxs-lookup"><span data-stu-id="ebe45-114">Webhooks are scoped at the team level.</span></span> <span data-ttu-id="ebe45-115">您需要完成每个要向其添加传出 webhook 的团队的安装过程。</span><span class="sxs-lookup"><span data-stu-id="ebe45-115">You’ll need to go through the setup process for each team you want to add your outgoing webhook to.</span></span> |
| <span data-ttu-id="ebe45-116">响应消息</span><span class="sxs-lookup"><span data-stu-id="ebe45-116">Reactive Messaging</span></span>| <span data-ttu-id="ebe45-117">用户必须使用 webhook 的 @mention 来接收邮件。</span><span class="sxs-lookup"><span data-stu-id="ebe45-117">Users must use @mention for the webhook to receive messages.</span></span> <span data-ttu-id="ebe45-118">当前用户只能将公用通道中的传出 webhook （而不能在个人或专用范围内）发送邮件</span><span class="sxs-lookup"><span data-stu-id="ebe45-118">Currently users can only message an outgoing webhook in public channels and not within the personal or private scope</span></span> |
|<span data-ttu-id="ebe45-119">标准 HTTP 邮件交换</span><span class="sxs-lookup"><span data-stu-id="ebe45-119">Standard HTTP message exchange</span></span>|<span data-ttu-id="ebe45-120">响应将显示在原始请求邮件所在的同一链中，并且可以包括任何 Bot 框架邮件内容 (格式文本、图像、卡片和表情符号) 。</span><span class="sxs-lookup"><span data-stu-id="ebe45-120">Responses will appear in the same chain as the original request message and can include any Bot Framework message content (rich text, images, cards, and emojis).</span></span> <span data-ttu-id="ebe45-121">**注意**：虽然传出 webhook 可以使用卡片，但不能使用除之外的任何卡片操作 `openURL` 。</span><span class="sxs-lookup"><span data-stu-id="ebe45-121">**Note**: Although outgoing webhooks can use cards, they cannot use any card actions except for `openURL`.</span></span>|
| <span data-ttu-id="ebe45-122">团队 API 方法支持</span><span class="sxs-lookup"><span data-stu-id="ebe45-122">Teams API method support</span></span>|<span data-ttu-id="ebe45-123">在团队中，传出 webhook 向 web 服务发送 HTTP POST 并处理回复。</span><span class="sxs-lookup"><span data-stu-id="ebe45-123">In Teams, outgoing webhooks send an HTTP POST to a web service and process a response back.</span></span> <span data-ttu-id="ebe45-124">他们不能访问任何其他 Api，如检索团队中的名单或频道列表。</span><span class="sxs-lookup"><span data-stu-id="ebe45-124">They cannot access any other APIs like retrieve the roster or list of channels in a team.</span></span>|

## <a name="adding-outgoing-webhook-processing-to-your-app"></a><span data-ttu-id="ebe45-125">将传出 webhook 处理添加到您的应用程序</span><span class="sxs-lookup"><span data-stu-id="ebe45-125">Adding outgoing webhook processing to your app</span></span>

<span data-ttu-id="ebe45-126">**方案**：将团队频道数据库服务器上的更改状态通知推送到您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="ebe45-126">**Scenario**: Push change status notifications on a Teams channel database server to your app.</span></span>  
<span data-ttu-id="ebe45-127">**示例**：您具有一条业务线应用程序，用于跟踪团队频道用户在 Office 365 租赁中对雇员记录所做的所有 CRUD 操作。</span><span class="sxs-lookup"><span data-stu-id="ebe45-127">**Example**: You have a line-of-business app that tracks all CRUD operations made to employee records by Teams channel HR users across an Office 365 tenancy.</span></span>

### <a name="1-create-a-url-on-your-apps-server-to-accept-and-process-a-post-request-with-a-json-payload"></a><span data-ttu-id="ebe45-128">1. 在应用程序的服务器上创建 URL，以使用 JSON 有效负载接受和处理 POST 请求</span><span class="sxs-lookup"><span data-stu-id="ebe45-128">1. Create a URL on your app's server to accept and process a POST request with a JSON payload</span></span>

<span data-ttu-id="ebe45-129">你的服务将在标准 Azure bot 服务消息架构中接收邮件。</span><span class="sxs-lookup"><span data-stu-id="ebe45-129">Your service will receive messages in the standard Azure bot service messaging schema.</span></span> <span data-ttu-id="ebe45-130">Bot 框架连接器是一项 RESTful 服务，它使服务能够通过 HTTPS 协议（如[Azure Bot 服务 API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)中所述）处理 JSON 格式的邮件交换。</span><span class="sxs-lookup"><span data-stu-id="ebe45-130">The Bot Framework connector is a RESTful service that enables your service to process the interchange of JSON formatted messages via HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).</span></span> <span data-ttu-id="ebe45-131">或者，您可以按照 [Microsoft Bot 框架 SDK] 来处理和分析邮件。</span><span class="sxs-lookup"><span data-stu-id="ebe45-131">Alternatively, you can follow the [Microsoft Bot Framework SDK] to process and parse messages.</span></span> <span data-ttu-id="ebe45-132">*另请参阅*  [关于 Azure Bot 服务](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0)。</span><span class="sxs-lookup"><span data-stu-id="ebe45-132">*See also*  [About Azure Bot Service](/azure/bot-service/bot-service-overview-introduction?view=azure-bot-service-4.0).</span></span>

<span data-ttu-id="ebe45-133">传出 webhook 的范围限定为 `team` 级别，并且对团队的所有成员都可见。</span><span class="sxs-lookup"><span data-stu-id="ebe45-133">Outgoing webhooks are scoped to the `team` level and are visible to all members of the team.</span></span> <span data-ttu-id="ebe45-134">就像 bot 一样，用户需要在通道中\*\* \@ 提及\*\*传出 webhook 的名称来调用它。</span><span class="sxs-lookup"><span data-stu-id="ebe45-134">Just like a bot, users are required to **\@mention** the name of the outgoing webhook to invoke it in the channel.</span></span>

### <a name="2-create-a-method-to-verify-the-outgoing-webhook-hmac-token"></a><span data-ttu-id="ebe45-135">2. 创建用于验证传出 webhook HMAC 令牌的方法</span><span class="sxs-lookup"><span data-stu-id="ebe45-135">2. Create a method to verify the outgoing webhook HMAC token</span></span>

<span data-ttu-id="ebe45-136">为了确保服务仅接收来自实际团队客户端的呼叫，团队在 HTTP 头中提供了一个在 `hmac` 您的身份验证协议中应始终包含的 HMAC 代码。</span><span class="sxs-lookup"><span data-stu-id="ebe45-136">To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC Code in the HTTP `hmac` header that should always be  included in your authentication protocol.</span></span>

<span data-ttu-id="ebe45-137">您的代码应始终验证请求中包含的 HMAC 签名：</span><span class="sxs-lookup"><span data-stu-id="ebe45-137">Your code should always validate the HMAC signature included in the request:</span></span>

* <span data-ttu-id="ebe45-138">从邮件的请求正文*生成*HMAC 令牌。</span><span class="sxs-lookup"><span data-stu-id="ebe45-138">*Generate* the HMAC token from the request body of the message.</span></span> <span data-ttu-id="ebe45-139">在大多数平台上，有一些标准库可执行此操作 (*请参阅*Node.js 的[加密](https://nodejs.org/api/crypto.html#crypto_crypto)或*参阅*适用于 C 的[团队 Webhook 示例](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) \#) 。</span><span class="sxs-lookup"><span data-stu-id="ebe45-139">There are standard libraries to do this on most platforms (*see* [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js or  *see* [Teams Webhook Sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#).</span></span> <span data-ttu-id="ebe45-140">Microsoft 团队使用标准 SHA256 HMAC 加密。</span><span class="sxs-lookup"><span data-stu-id="ebe45-140">Microsoft Teams uses standard SHA256 HMAC cryptography .</span></span> <span data-ttu-id="ebe45-141">您需要将正文转换为 UTF8 形式的字节数组。</span><span class="sxs-lookup"><span data-stu-id="ebe45-141">You will need to convert the body to a byte array in UTF8.</span></span>
* <span data-ttu-id="ebe45-142">当您在团队客户端中注册了传出 webhook 时，从**团队提供**的安全令牌的字节数组中*计算*哈希值。</span><span class="sxs-lookup"><span data-stu-id="ebe45-142">*Compute* the hash from the byte array of the security token **provided by Teams** when you registered the outgoing webhook in the Teams client].</span></span> <span data-ttu-id="ebe45-143">*请参阅*下面的[创建传出 webhook](#create-an-outgoing-webhook)。</span><span class="sxs-lookup"><span data-stu-id="ebe45-143">*See* [Create an outgoing webhook](#create-an-outgoing-webhook), below.</span></span>
* <span data-ttu-id="ebe45-144">使用 UTF-8 编码将哈希值*转换*为字符串。</span><span class="sxs-lookup"><span data-stu-id="ebe45-144">*Convert* the hash to a string using UTF-8 encoding.</span></span>
* <span data-ttu-id="ebe45-145">将生成的哈希的字符串值与 HTTP 请求中提供的值*进行比较*。</span><span class="sxs-lookup"><span data-stu-id="ebe45-145">*Compare* the string value of the generated hash with the value provided in the HTTP request.</span></span>

### <a name="3-create-a-method-to-send-a-success-or-failure-response"></a><span data-ttu-id="ebe45-146">3. 创建用于发送成功或失败响应的方法</span><span class="sxs-lookup"><span data-stu-id="ebe45-146">3. Create a method to send a success or failure response</span></span>

<span data-ttu-id="ebe45-147">来自你的传出 webhook 的响应将显示在与原始邮件相同的答复链中。</span><span class="sxs-lookup"><span data-stu-id="ebe45-147">Responses from your outgoing webhook will appear in the same reply chain as the original message.</span></span> <span data-ttu-id="ebe45-148">当用户执行查询时，Microsoft 团队会向您的服务发出同步 HTTP 请求，并且您的代码将有5秒的时间来响应邮件，然后连接超时并终止。</span><span class="sxs-lookup"><span data-stu-id="ebe45-148">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code will have 5 seconds to respond to the message before the connection times out and terminates.</span></span>

### <a name="example-response"></a><span data-ttu-id="ebe45-149">示例响应</span><span class="sxs-lookup"><span data-stu-id="ebe45-149">Example response</span></span>

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```

## <a name="create-an-outgoing-webhook"></a><span data-ttu-id="ebe45-150">创建传出 Webhook</span><span class="sxs-lookup"><span data-stu-id="ebe45-150">Create an outgoing webhook</span></span>

1. <span data-ttu-id="ebe45-151">选择适当的团队，然后从 ( # A3) 下拉菜单中选择 "**管理团队**"。</span><span class="sxs-lookup"><span data-stu-id="ebe45-151">Select the appropriate team and select **Manage team** from the (&#8226;&#8226;&#8226;) drop-down menu.</span></span>
1. <span data-ttu-id="ebe45-152">从导航栏中选择 "**应用**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="ebe45-152">Choose the **Apps** tab from the navigation bar.</span></span>
1. <span data-ttu-id="ebe45-153">从窗口的右下角选择 "**创建传出 webhook**"。</span><span class="sxs-lookup"><span data-stu-id="ebe45-153">From the window's lower right corner select **Create an outgoing webhook**.</span></span>
1. <span data-ttu-id="ebe45-154">在随后出现的弹出窗口中，完成必需的字段：</span><span class="sxs-lookup"><span data-stu-id="ebe45-154">In the resulting popup window complete the required fields:</span></span>

>* <span data-ttu-id="ebe45-155">**Name** -webhook 标题和 @mention 点击。</span><span class="sxs-lookup"><span data-stu-id="ebe45-155">**Name** - The webhook title and @mention tap.</span></span>
>* <span data-ttu-id="ebe45-156">**回调 URL** -将接受 JSON 有效负载的 HTTPS 终结点，并将接收来自团队的 POST 请求。</span><span class="sxs-lookup"><span data-stu-id="ebe45-156">**Callback URL** - The HTTPS endpoint that accepts JSON payloads and will receive POST requests from Teams.</span></span>
>* <span data-ttu-id="ebe45-157">**Description** -将显示在配置文件卡片和团队级应用仪表板中的详细字符串。</span><span class="sxs-lookup"><span data-stu-id="ebe45-157">**Description** - A detailed string that will appear in the profile card and the team-level App dashboard.</span></span>
>* <span data-ttu-id="ebe45-158"> (可选) webhook 的应用程序图标的**个人资料图片**。</span><span class="sxs-lookup"><span data-stu-id="ebe45-158">**Profile Picture** (optional) an app icon for your webhook.</span></span>
>* <span data-ttu-id="ebe45-159">从弹出窗口的右下角选择 "**创建**" 按钮，并将传出 webhook 添加到当前团队的通道中。</span><span class="sxs-lookup"><span data-stu-id="ebe45-159">Select the **Create** button from lower right corner of the pop-up window and the outgoing webhook will be added to the current team's channels.</span></span>
>* <span data-ttu-id="ebe45-160">下一个对话框窗口将显示[基于哈希的邮件身份验证代码 (HMAC) ](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301)安全令牌，该代码将用于在团队和指定的外部服务之间进行身份验证调用。</span><span class="sxs-lookup"><span data-stu-id="ebe45-160">The next dialog window will display an [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) security token that will be used to authenticate calls between Teams and the designated outside service.</span></span>
>* <span data-ttu-id="ebe45-161">如果 URL 有效且服务器和客户端身份验证令牌相等 (即 HMAC 握手) ，则会向团队用户提供传出 webhook。</span><span class="sxs-lookup"><span data-stu-id="ebe45-161">If the URL is valid and the server and client authentication tokens are equal (i.e., an HMAC handshake), the outgoing webhook will be available to the team's users.</span></span>

## <a name="code-samples"></a><span data-ttu-id="ebe45-162">代码示例</span><span class="sxs-lookup"><span data-stu-id="ebe45-162">Code samples</span></span>

<span data-ttu-id="ebe45-163">您可以查看 GitHub 上的传出 webhook 代码示例：</span><span class="sxs-lookup"><span data-stu-id="ebe45-163">You can view outgoing webhook code samples on GitHub:</span></span>

### <a name="nodejs"></a><span data-ttu-id="ebe45-164">Node.js</span><span class="sxs-lookup"><span data-stu-id="ebe45-164">Node.js</span></span>

[<span data-ttu-id="ebe45-165">OfficeDev/msteams-示例-传出-webhook-nodejs</span><span class="sxs-lookup"><span data-stu-id="ebe45-165">OfficeDev/msteams-samples-outgoing-webhook-nodejs</span></span>](https://github.com/OfficeDev/msteams-samples-outgoing-webhook-nodejs)

### <a name="c"></a><span data-ttu-id="ebe45-166">Lc\#</span><span class="sxs-lookup"><span data-stu-id="ebe45-166">C\#</span></span>

[<span data-ttu-id="ebe45-167">OfficeDev/microsoft-团队-示例-传出-webhook</span><span class="sxs-lookup"><span data-stu-id="ebe45-167">OfficeDev/microsoft-teams-sample-outgoing-webhook</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook)
