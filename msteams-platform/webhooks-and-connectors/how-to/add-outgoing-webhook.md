---
title: 创建传出 Webhook
author: laujan
description: 介绍如何创建传出 Webhook
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
keywords: teams 选项卡传出 Webhook 可操作邮件验证 webhook
ms.openlocfilehash: c02ff5388e47ba40056afcc1fcf5e8d7ad4437e8
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140320"
---
# <a name="create-outgoing-webhook"></a><span data-ttu-id="36995-104">创建传出 Webhook</span><span class="sxs-lookup"><span data-stu-id="36995-104">Create Outgoing Webhook</span></span>

<span data-ttu-id="36995-105">传出 Webhook 充当自动程序，使用 @mention 在频道 **中搜索消息**。</span><span class="sxs-lookup"><span data-stu-id="36995-105">The Outgoing Webhook acts as a bot and search for messages in channels using **@mention**.</span></span> <span data-ttu-id="36995-106">它将通知发送到外部 Web 服务，并响应丰富的消息，其中包括卡片和图像。</span><span class="sxs-lookup"><span data-stu-id="36995-106">It sends notifications to external web services and responds with rich messages, which include cards and images.</span></span> <span data-ttu-id="36995-107">它有助于跳过通过以下过程创建[Microsoft Bot Framework。](https://dev.botframework.com/)</span><span class="sxs-lookup"><span data-stu-id="36995-107">It helps to skip the process of creating bots through the [Microsoft Bot Framework](https://dev.botframework.com/).</span></span>

## <a name="key-features-of-outgoing-webhook"></a><span data-ttu-id="36995-108">传出 Webhook 的主要功能</span><span class="sxs-lookup"><span data-stu-id="36995-108">Key features of Outgoing Webhook</span></span>

<span data-ttu-id="36995-109">下表提供了传出 Webhook 的功能和说明：</span><span class="sxs-lookup"><span data-stu-id="36995-109">The following table provides the features and description of Outgoing Webhooks:</span></span>

| <span data-ttu-id="36995-110">功能</span><span class="sxs-lookup"><span data-stu-id="36995-110">Features</span></span> | <span data-ttu-id="36995-111">说明</span><span class="sxs-lookup"><span data-stu-id="36995-111">Description</span></span> |
| ------- | ----------- |
| <span data-ttu-id="36995-112">作用域配置</span><span class="sxs-lookup"><span data-stu-id="36995-112">Scoped configuration</span></span>| <span data-ttu-id="36995-113">Webhook 的范围在团队级别。</span><span class="sxs-lookup"><span data-stu-id="36995-113">Webhooks are scoped at the team level.</span></span> <span data-ttu-id="36995-114">每个项的必需设置过程会添加一个传出 Webhook。</span><span class="sxs-lookup"><span data-stu-id="36995-114">Mandatory set up process for each adds an Outgoing Webhook.</span></span> |
| <span data-ttu-id="36995-115">反应消息</span><span class="sxs-lookup"><span data-stu-id="36995-115">Reactive messaging</span></span>| <span data-ttu-id="36995-116">用户必须使用 @mention webhook 接收消息。</span><span class="sxs-lookup"><span data-stu-id="36995-116">Users must use @mention for the webhook to receive messages.</span></span> <span data-ttu-id="36995-117">目前，用户只能在公共频道中发送传出 Webhook 消息，而不是在个人或专用范围内。</span><span class="sxs-lookup"><span data-stu-id="36995-117">Currently, users can only message an Outgoing Webhook in public channels and not within the personal or private scope.</span></span> |
|<span data-ttu-id="36995-118">标准 HTTP 邮件交换</span><span class="sxs-lookup"><span data-stu-id="36995-118">Standard HTTP message exchange</span></span>|<span data-ttu-id="36995-119">响应显示在与原始请求消息相同的链中，并且可以包含任何 Bot Framework 消息内容，例如格式文本、图像、卡片和表情符号。</span><span class="sxs-lookup"><span data-stu-id="36995-119">Responses appear in the same chain as the original request message and can include any Bot Framework message content, for example, rich text, images, cards, and emojis.</span></span> <span data-ttu-id="36995-120">尽管传出 Webhook 可以使用卡片，但除了 以外，它们不能使用任何卡片操作 `openURL` 。</span><span class="sxs-lookup"><span data-stu-id="36995-120">Although Outgoing Webhooks can use cards, they cannot use any card actions except for `openURL`.</span></span>|
| <span data-ttu-id="36995-121">TeamsAPI 方法支持</span><span class="sxs-lookup"><span data-stu-id="36995-121">Teams API method support</span></span>|<span data-ttu-id="36995-122">传出 Webhook 将 HTTP POST 发送到 Web 服务并获取响应。</span><span class="sxs-lookup"><span data-stu-id="36995-122">Outgoing Webhooks sends an HTTP POST to a web service and gets a response.</span></span> <span data-ttu-id="36995-123">他们无法访问任何其他 API，例如检索团队中名单或频道列表。</span><span class="sxs-lookup"><span data-stu-id="36995-123">They cannot access any other APIs, such as retrieve the roster or list of channels in a team.</span></span>|

## <a name="create-outgoing-webhooks"></a><span data-ttu-id="36995-124">创建传出 Webhook</span><span class="sxs-lookup"><span data-stu-id="36995-124">Create Outgoing Webhooks</span></span>

<span data-ttu-id="36995-125">创建传出 Webhook，并添加自定义聊天机器人Teams。</span><span class="sxs-lookup"><span data-stu-id="36995-125">Create Outgoing Webhooks and add custom bots to Teams.</span></span>

<span data-ttu-id="36995-126">**创建传出 Webhook**</span><span class="sxs-lookup"><span data-stu-id="36995-126">**To create an Outgoing Webhook**</span></span>

1. <span data-ttu-id="36995-127">Select **Teams** from the left pane.</span><span class="sxs-lookup"><span data-stu-id="36995-127">Select **Teams** from the left pane.</span></span> <span data-ttu-id="36995-128">将显示 **Teams** 页：</span><span class="sxs-lookup"><span data-stu-id="36995-128">The **Teams** page appears:</span></span>

    ![Teams 频道](~/assets/images/teamschannel.png)

1. <span data-ttu-id="36995-130">在 **"Teams"** 页中，选择创建传出 Webhook 所需的团队，然后选择 &#8226;&#8226;&#8226;。</span><span class="sxs-lookup"><span data-stu-id="36995-130">In the **Teams** page, select the required team to create an Outgoing Webhook and select the &#8226;&#8226;&#8226;.</span></span> <span data-ttu-id="36995-131">在下拉菜单中，选择"**管理团队"：**</span><span class="sxs-lookup"><span data-stu-id="36995-131">In the dropdown menu, select **Manage team**:</span></span>

    ![创建传出 Webhook](~/assets/images/outgoingwebhook1.png)

1. <span data-ttu-id="36995-133">选择频道 **页面上** 的"应用"选项卡：</span><span class="sxs-lookup"><span data-stu-id="36995-133">Select the **Apps** tab on the channel page:</span></span>

    ![创建传出 Webhook](~/assets/images/outgoingwebhook2.png)

1. <span data-ttu-id="36995-135">选择 **"创建传出 Webhook"：**</span><span class="sxs-lookup"><span data-stu-id="36995-135">Select **Create an Outgoing Webhook**:</span></span>

    ![创建传出 Webhook](~/assets/images/outgoingwebhook3.png)

1. <span data-ttu-id="36995-137">在"创建传出 **Webhook"页中键入以下** 详细信息：</span><span class="sxs-lookup"><span data-stu-id="36995-137">Type the following details in the **Create an Outgoing Webhook** page:</span></span>

    * <span data-ttu-id="36995-138">**名称**：Webhook 标题和@mention选项卡。</span><span class="sxs-lookup"><span data-stu-id="36995-138">**Name**: The webhook title and @mention tab.</span></span>
    * <span data-ttu-id="36995-139">**回调 URL：** 接受 JSON 有效负载并接收来自客户端的 POST 请求的 HTTPS Teams。</span><span class="sxs-lookup"><span data-stu-id="36995-139">**Callback URL**: The HTTPS endpoint that accepts JSON payloads and receives POST requests from Teams.</span></span>
    * <span data-ttu-id="36995-140">**说明**：显示在配置文件卡片和团队级应用仪表板中的详细字符串。</span><span class="sxs-lookup"><span data-stu-id="36995-140">**Description**: A detailed string that appears in the profile card and the team-level App dashboard.</span></span>
    * <span data-ttu-id="36995-141">**个人资料图片**：Webhook 的应用图标，可选。</span><span class="sxs-lookup"><span data-stu-id="36995-141">**Profile Picture**: An app icon for your webhook, which is optional.</span></span>

1. <span data-ttu-id="36995-142">选择“创建”。</span><span class="sxs-lookup"><span data-stu-id="36995-142">Select **Create**.</span></span> <span data-ttu-id="36995-143">传出 Webhook 将添加到当前团队的频道：</span><span class="sxs-lookup"><span data-stu-id="36995-143">The Outgoing Webhook is added to the current team's channel:</span></span>

    ![创建传出 Webhook](~/assets/images/outgoingwebhook.png)

<span data-ttu-id="36995-145">将显示 [基于哈希的消息身份验证代码 (HMAC) ](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) 对话框。</span><span class="sxs-lookup"><span data-stu-id="36995-145">A [Hash-based Message Authentication Code (HMAC)](https://security.stackexchange.com/questions/20129/how-and-when-do-i-use-hmac/20301) dialogue box appears.</span></span> <span data-ttu-id="36995-146">它是一个安全令牌，用于对 Teams 和指定的外部服务之间的调用进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="36995-146">It is a security token used to authenticate calls between Teams and the designated outside service.</span></span>

>[!NOTE]
> <span data-ttu-id="36995-147">仅在 URL 有效且服务器和客户端身份验证令牌相等时，传出 Webhook 才可供团队用户使用。</span><span class="sxs-lookup"><span data-stu-id="36995-147">The Outgoing Webhook is available to the team's users, only if the URL is valid and the server and client authentication tokens are equal.</span></span> <span data-ttu-id="36995-148">例如，HMAC 握手。</span><span class="sxs-lookup"><span data-stu-id="36995-148">For example, an HMAC handshake.</span></span>

<span data-ttu-id="36995-149">以下方案提供了添加传出 Webhook 的详细信息：</span><span class="sxs-lookup"><span data-stu-id="36995-149">The following scenario provides the details to add an Outgoing Webhook:</span></span>

* <span data-ttu-id="36995-150">应用场景：将更改状态通知推送到Teams通道数据库服务器应用。</span><span class="sxs-lookup"><span data-stu-id="36995-150">Scenario: Push change status notifications on a Teams channel database server to your app.</span></span>
* <span data-ttu-id="36995-151">示例：你有一个业务线应用，可跟踪所有 CRUD 操作，如创建、读取、更新和删除。</span><span class="sxs-lookup"><span data-stu-id="36995-151">Example: You have a line of business app that tracks all CRUD operations, such as create, read, update, and delete.</span></span> <span data-ttu-id="36995-152">这些操作通过跨租户的 Teams HR 用户对员工Office 365操作。</span><span class="sxs-lookup"><span data-stu-id="36995-152">These operations are made to the employee records by Teams channel HR users across an Office 365 tenancy.</span></span>

# <a name="url-json-payload"></a>[<span data-ttu-id="36995-153">URL JSON 有效负载</span><span class="sxs-lookup"><span data-stu-id="36995-153">URL JSON payload</span></span>](#tab/urljsonpayload)
<span data-ttu-id="36995-154">**在应用服务器上创建 URL 以接受并处理具有 JSON 有效负载的 POST 请求**</span><span class="sxs-lookup"><span data-stu-id="36995-154">**Create a URL on your app's server to accept and process a POST request with a JSON payload**</span></span>

<span data-ttu-id="36995-155">你的服务接收标准 Azure 自动程序服务消息架构中的邮件。</span><span class="sxs-lookup"><span data-stu-id="36995-155">Your service receives messages in a standard Azure bot service messaging schema.</span></span> <span data-ttu-id="36995-156">Bot Framework 连接器是一项 RESTful 服务，它支持通过 HTTPS 协议处理 JSON 格式邮件的交换，如 [Azure Bot Service API 中记录](/bot-framework/rest-api/bot-framework-rest-connector-api-reference)。</span><span class="sxs-lookup"><span data-stu-id="36995-156">The Bot Framework connector is a RESTful service that empowers to process the interchange of JSON formatted messages through HTTPS protocols as documented in the [Azure Bot Service API](/bot-framework/rest-api/bot-framework-rest-connector-api-reference).</span></span> <span data-ttu-id="36995-157">或者，你可以按照 Microsoft Bot Framework SDK 处理和分析消息。</span><span class="sxs-lookup"><span data-stu-id="36995-157">Alternatively, you can follow the Microsoft Bot Framework SDK to process and parse messages.</span></span> <span data-ttu-id="36995-158">有关详细信息，请参阅 [Azure Bot 服务概述](/azure/bot-service/bot-service-overview-introduction)。</span><span class="sxs-lookup"><span data-stu-id="36995-158">For more information, see [overview of Azure Bot Service](/azure/bot-service/bot-service-overview-introduction).</span></span>

<span data-ttu-id="36995-159">传出 Webhook 的范围为级别 `team` ，并且所有团队成员都可以看到。</span><span class="sxs-lookup"><span data-stu-id="36995-159">Outgoing Webhooks are scoped to the `team` level and are visible to all the team members.</span></span> <span data-ttu-id="36995-160">用户需要 **\@ 提及传出** Webhook 的名称，以在频道中调用它。</span><span class="sxs-lookup"><span data-stu-id="36995-160">Users need to **\@mention** the name of the Outgoing Webhook to invoke it in the channel.</span></span>

# <a name="verify-hmac-token"></a>[<span data-ttu-id="36995-161">验证 HMAC 令牌</span><span class="sxs-lookup"><span data-stu-id="36995-161">Verify HMAC token</span></span>](#tab/verifyhmactoken)
<span data-ttu-id="36995-162">**创建用于验证传出 Webhook HMAC 令牌的方法**</span><span class="sxs-lookup"><span data-stu-id="36995-162">**Create a method to verify the Outgoing Webhook HMAC token**</span></span>

<span data-ttu-id="36995-163">使用入站邮件和 ID 示例：{"contoso"的 SigningKeyDictionary 的"contoso"，"vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }。</span><span class="sxs-lookup"><span data-stu-id="36995-163">Using example of inbound message and ID: "contoso" of SigningKeyDictionary of {"contoso", "vqF0En+Z0ucuRTM/01o2GuhMH3hKKk/N2bOmlM31zaA=" }.</span></span>

<span data-ttu-id="36995-164">在请求标头的授权中，使用值"HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U="。</span><span class="sxs-lookup"><span data-stu-id="36995-164">Use the value "HMAC 03TCao0i55H1eVKUusZOTZRjtvYTs+mO41mPL+R1e1U=" in the authorization of request header.</span></span>

<span data-ttu-id="36995-165">为了确保服务仅接收来自实际客户端Teams的呼叫，Teams HTTP 授权标头中提供 HMAC `hmac` 代码。</span><span class="sxs-lookup"><span data-stu-id="36995-165">To ensure that your service is receiving calls only from actual Teams clients, Teams provides an HMAC code in the HTTP `hmac` authorization header.</span></span> <span data-ttu-id="36995-166">始终在身份验证协议中包括代码。</span><span class="sxs-lookup"><span data-stu-id="36995-166">Always include the code in your authentication protocol.</span></span>

<span data-ttu-id="36995-167">代码必须始终验证请求中包含的 HMAC 签名，如下所示：</span><span class="sxs-lookup"><span data-stu-id="36995-167">Your code must always validate the HMAC signature included in the request as follows:</span></span>

* <span data-ttu-id="36995-168">从邮件的请求正文生成 HMAC 令牌。</span><span class="sxs-lookup"><span data-stu-id="36995-168">Generate the HMAC token from the request body of the message.</span></span> <span data-ttu-id="36995-169">在大多数平台上，有一些标准库可以这样做，例如加密[for](https://nodejs.org/api/crypto.html#crypto_crypto) Node.js 和 Teams [webhook 示例](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) \#) 。</span><span class="sxs-lookup"><span data-stu-id="36995-169">There are standard libraries to do this on most platform, such as [Crypto](https://nodejs.org/api/crypto.html#crypto_crypto) for Node.js and [Teams webhook sample](https://github.com/OfficeDev/microsoft-teams-sample-outgoing-webhook/blob/23eb61da5a18634d51c5247944843da9abed01b6/WebhookSampleBot/Models/AuthProvider.cs) for C\#).</span></span> <span data-ttu-id="36995-170">Microsoft Teams使用标准 SHA256 HMAC 加密。</span><span class="sxs-lookup"><span data-stu-id="36995-170">Microsoft Teams uses standard SHA256 HMAC cryptography.</span></span> <span data-ttu-id="36995-171">你必须在 UTF8 中将正文转换为字节数组。</span><span class="sxs-lookup"><span data-stu-id="36995-171">You must convert the body to a byte array in UTF8.</span></span>
* <span data-ttu-id="36995-172">在客户端中注册传出 Webhook 时，计算由 Teams 提供的安全令牌的字节数组Teams哈希。</span><span class="sxs-lookup"><span data-stu-id="36995-172">Compute the hash from the byte array of the security token provided by Teams when you registered the Outgoing Webhook in the Teams client.</span></span> <span data-ttu-id="36995-173">请参阅 [创建传出 Webhook](#create-outgoing-webhook)。</span><span class="sxs-lookup"><span data-stu-id="36995-173">See [create an Outgoing Webhook](#create-outgoing-webhook).</span></span>
* <span data-ttu-id="36995-174">使用 UTF-8 编码将哈希转换为字符串。</span><span class="sxs-lookup"><span data-stu-id="36995-174">Convert the hash to a string using UTF-8 encoding.</span></span>
* <span data-ttu-id="36995-175">将生成的哈希的字符串值与 HTTP 请求中提供的值进行比较。</span><span class="sxs-lookup"><span data-stu-id="36995-175">Compare the string value of the generated hash with the value provided in the HTTP request.</span></span>

# <a name="method-to-respond"></a>[<span data-ttu-id="36995-176">响应方法</span><span class="sxs-lookup"><span data-stu-id="36995-176">Method to respond</span></span>](#tab/methodtorespond)
<span data-ttu-id="36995-177">**创建发送成功或失败响应的方法**</span><span class="sxs-lookup"><span data-stu-id="36995-177">**Create a method to send a success or failure response**</span></span>

<span data-ttu-id="36995-178">来自传出 Webhook 的响应显示在与原始邮件相同的回复链中。</span><span class="sxs-lookup"><span data-stu-id="36995-178">Responses from your Outgoing Webhooks appear in the same reply chain as the original message.</span></span> <span data-ttu-id="36995-179">当用户执行查询时，Microsoft Teams向服务发出同步 HTTP 请求，您的代码将在连接中断和终止之前获取 5 秒钟来响应消息。</span><span class="sxs-lookup"><span data-stu-id="36995-179">When the user performs a query, Microsoft Teams issues a synchronous HTTP request to your service and your code gets five seconds to respond to the message before the connection times out and terminates.</span></span>

### <a name="example-response"></a><span data-ttu-id="36995-180">示例响应</span><span class="sxs-lookup"><span data-stu-id="36995-180">Example response</span></span>

```json
{
    "type": "message",
    "text": "This is a reply!"
}
```
---

> [!NOTE]
> * <span data-ttu-id="36995-181">可以使用传出 Webhook 将自适应卡片、Hero 卡片和短信作为附件发送。</span><span class="sxs-lookup"><span data-stu-id="36995-181">You can send Adaptive Card, Hero card, and text messages as attachment with Outgoing Webhook.</span></span>
> * <span data-ttu-id="36995-182">卡片支持格式设置。</span><span class="sxs-lookup"><span data-stu-id="36995-182">Cards support formatting.</span></span> <span data-ttu-id="36995-183">有关详细信息，请参阅使用 [markdown 格式化卡片](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown)。</span><span class="sxs-lookup"><span data-stu-id="36995-183">For more information, see [format cards with markdown](~/task-modules-and-cards/cards/cards-format.md?tabs=adaptive-md%2Cconnector-html#format-cards-with-markdown).</span></span>

<span data-ttu-id="36995-184">以下代码是自适应卡片响应的示例：</span><span class="sxs-lookup"><span data-stu-id="36995-184">Following codes are examples of an Adaptive Card response:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="36995-185">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="36995-185">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="36995-186">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="36995-186">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="36995-187">JSON</span><span class="sxs-lookup"><span data-stu-id="36995-187">JSON</span></span>](#tab/json)

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

## <a name="code-sample"></a><span data-ttu-id="36995-188">代码示例</span><span class="sxs-lookup"><span data-stu-id="36995-188">Code sample</span></span>

|<span data-ttu-id="36995-189">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="36995-189">**Sample name**</span></span> | <span data-ttu-id="36995-190">**说明**</span><span class="sxs-lookup"><span data-stu-id="36995-190">**Description**</span></span> | <span data-ttu-id="36995-191">**.NET**</span><span class="sxs-lookup"><span data-stu-id="36995-191">**.NET**</span></span> | <span data-ttu-id="36995-192">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="36995-192">**Node.js**</span></span> |
|----------------|------------------|--------|----------------|
| <span data-ttu-id="36995-193">传出 Webhook</span><span class="sxs-lookup"><span data-stu-id="36995-193">Outgoing Webhooks</span></span> | <span data-ttu-id="36995-194">用于创建自定义聊天机器人的示例，以在 Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="36995-194">Samples to create custom bots to be used in Microsoft Teams.</span></span>| [<span data-ttu-id="36995-195">View</span><span class="sxs-lookup"><span data-stu-id="36995-195">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/csharp) | [<span data-ttu-id="36995-196">View</span><span class="sxs-lookup"><span data-stu-id="36995-196">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/outgoing-webhook/nodejs)|

## <a name="see-also"></a><span data-ttu-id="36995-197">另请参阅</span><span class="sxs-lookup"><span data-stu-id="36995-197">See also</span></span>
* [<span data-ttu-id="36995-198">创建传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="36995-198">Create an Incoming Webhook</span></span>](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [<span data-ttu-id="36995-199">创建 Office 365 连接器</span><span class="sxs-lookup"><span data-stu-id="36995-199">Create an Office 365 Connector</span></span>](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [<span data-ttu-id="36995-200">创建和发送邮件</span><span class="sxs-lookup"><span data-stu-id="36995-200">Create and send messages</span></span>](~/webhooks-and-connectors/how-to/connectors-using.md)
