---
title: 来电通知
description: 有关处理来自传入呼叫的通知的详细技术信息
ms.topic: conceptual
localization_priority: Normal
keywords: 调用呼叫通知回调区域相关性
ms.date: 04/02/2019
ms.openlocfilehash: 06068c13d27598b9a7b5e70181c69f9efb2c0afb
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020174"
---
# <a name="incoming-call-notifications"></a><span data-ttu-id="63153-104">来电通知</span><span class="sxs-lookup"><span data-stu-id="63153-104">Incoming call notifications</span></span>

<span data-ttu-id="63153-105">在 [注册 Microsoft Teams 的](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities)通话和会议机器人时，提及用于呼叫 URL 的 Webhook。</span><span class="sxs-lookup"><span data-stu-id="63153-105">In [registering a calls and meetings bot for Microsoft Teams](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities), the Webhook for calling URL is mentioned.</span></span> <span data-ttu-id="63153-106">此 URL 是自动程序的所有传入呼叫的 webhook 终结点。</span><span class="sxs-lookup"><span data-stu-id="63153-106">This URL is the webhook endpoint for all incoming calls to your bot.</span></span>

## <a name="protocol-determination"></a><span data-ttu-id="63153-107">协议确定</span><span class="sxs-lookup"><span data-stu-id="63153-107">Protocol determination</span></span>

<span data-ttu-id="63153-108">传入通知以旧格式提供，以与以前的 Skype 协议 [兼容](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="63153-108">The incoming notification is provided in a legacy format for compatibility with the previous [Skype protocol](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true).</span></span> <span data-ttu-id="63153-109">为了将调用转换为 Microsoft Graph 协议，机器人必须确定通知是否采用旧格式并提供以下响应：</span><span class="sxs-lookup"><span data-stu-id="63153-109">In order to convert the call to the Microsoft Graph protocol, your bot must determine whether the notification is in a legacy format and provide the following response:</span></span>

```http
HTTP/1.1 204 No Content
```

<span data-ttu-id="63153-110">自动程序会再次收到通知，但这次在 Microsoft Graph 协议中。</span><span class="sxs-lookup"><span data-stu-id="63153-110">Your bot receives the notification again, but this time in the Microsoft Graph protocol.</span></span>

<span data-ttu-id="63153-111">在实时媒体平台的未来版本中，你可以配置应用程序支持的协议，以避免接收旧格式的初始回调。</span><span class="sxs-lookup"><span data-stu-id="63153-111">In a future release of the Real-time Media Platform, you can configure the protocol your application supports to avoid receiving the initial callback in the legacy format.</span></span>

<span data-ttu-id="63153-112">下一节提供有关针对区域相关性重定向到部署的传入呼叫通知的详细信息。</span><span class="sxs-lookup"><span data-stu-id="63153-112">The next section provides details on incoming call notifications redirected for region affinity to your deployment.</span></span>

## <a name="redirects-for-region-affinity"></a><span data-ttu-id="63153-113">区域相关性重定向</span><span class="sxs-lookup"><span data-stu-id="63153-113">Redirects for region affinity</span></span>

<span data-ttu-id="63153-114">从托管呼叫的数据中心调用 webhook。</span><span class="sxs-lookup"><span data-stu-id="63153-114">You call your webhook from the data-center hosting the call.</span></span> <span data-ttu-id="63153-115">呼叫从任何数据中心开始，不会考虑区域关系。</span><span class="sxs-lookup"><span data-stu-id="63153-115">The call starts in any data center and does not take into account region affinities.</span></span> <span data-ttu-id="63153-116">通知将发送到你的部署，具体取决于 GeoDNS 分辨率。</span><span class="sxs-lookup"><span data-stu-id="63153-116">The notification is sent to your deployment depending on the GeoDNS resolution.</span></span> <span data-ttu-id="63153-117">如果应用程序通过检查初始通知有效负载或其他方式确定需要在不同的部署中运行，则应用程序将提供以下响应：</span><span class="sxs-lookup"><span data-stu-id="63153-117">If your application determines, by inspecting the initial notification payload or otherwise, that it needs to run in a different deployment, the application provides the following response:</span></span>

```http
HTTP/1.1 302 Found
Location: your-new-location
```

<span data-ttu-id="63153-118">使机器人能够使用应答 API 应答 [传入](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) 呼叫。</span><span class="sxs-lookup"><span data-stu-id="63153-118">Enable your bot to answer an incoming call using the [answer](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) API.</span></span> <span data-ttu-id="63153-119">可以指定 以处理 `callbackUri` 此特定调用。</span><span class="sxs-lookup"><span data-stu-id="63153-119">You can specify the `callbackUri` to handle this particular call.</span></span> <span data-ttu-id="63153-120">这适用于特定分区处理呼叫且您希望在 中嵌入此信息以路由到正确实例的有状态 `callbackUri` 实例。</span><span class="sxs-lookup"><span data-stu-id="63153-120">This is useful for stateful instances where your call is handled by a particular partition, and you want to embed this information in the `callbackUri` for routing to the right instance.</span></span>

<span data-ttu-id="63153-121">下一节将提供有关通过检查张贴到 Webhook 的令牌来验证回调的详细信息。</span><span class="sxs-lookup"><span data-stu-id="63153-121">The next section provides details on authenticating the callback by inspecting the token posted to your webhook.</span></span>

## <a name="authenticate-the-callback"></a><span data-ttu-id="63153-122">对回调进行身份验证</span><span class="sxs-lookup"><span data-stu-id="63153-122">Authenticate the callback</span></span>

<span data-ttu-id="63153-123">自动程序必须检查张贴到 Webhook 的令牌以验证请求。</span><span class="sxs-lookup"><span data-stu-id="63153-123">Your bot must inspect the token posted to your webhook to validate the request.</span></span> <span data-ttu-id="63153-124">每次 API 发送到 webhook 时，HTTP POST 消息都会在授权标头中包含一个 OAuth 令牌作为一个 bearer 令牌，访问群体作为应用程序的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="63153-124">Every time the API posts to the webhook, the HTTP POST message contains an OAuth token in the Authorization header as a bearer token, with the audience as your application's App ID.</span></span>

<span data-ttu-id="63153-125">您的应用程序在接受回调请求之前必须验证此令牌。</span><span class="sxs-lookup"><span data-stu-id="63153-125">Your application must validate this token before accepting the callback request.</span></span>

<span data-ttu-id="63153-126">以下示例代码用于对回调进行身份验证：</span><span class="sxs-lookup"><span data-stu-id="63153-126">The following sample code is used to authenticate the callback:</span></span>

```http
POST https://bot.contoso.com/api/calls
Content-Type: application/json
Authentication: Bearer <TOKEN>

"value": [
    "subscriptionId": "2887CEE8344B47C291F1AF628599A93C",
    "subscriptionExpirationDateTime": "2016-11-20T18:23:45.9356913Z",
    "changeType": "updated",
    "resource": "/app/calls/8A934F51F25B4EE19613D4049491857B",
    "resourceData": {
        "@odata.type": "#microsoft.graph.call",
        "state": "Established"
    }
]
```

<span data-ttu-id="63153-127">OAuth 令牌具有以下值，由 Skype 签名：</span><span class="sxs-lookup"><span data-stu-id="63153-127">The OAuth token has the following values, and is signed by Skype:</span></span>

```json
{
    "aud": "0efc74f7-41c3-47a4-8775-7259bfef4241",
    "iss": "https://api.botframework.com",
    "iat": 1466741440,
    "nbf": 1466741440,
    "exp": 1466745340,
    "tid": "1fdd12d0-4620-44ed-baec-459b611f84b2"
}
```

<span data-ttu-id="63153-128">发布的 OpenID <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> 配置可用于验证令牌。</span><span class="sxs-lookup"><span data-stu-id="63153-128">The OpenID configuration published at <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> can be used to verify the token.</span></span> <span data-ttu-id="63153-129">每个 OAuth 令牌值使用如下：</span><span class="sxs-lookup"><span data-stu-id="63153-129">Each OAuth token value is used as follows:</span></span>

* <span data-ttu-id="63153-130">`aud` 其中 audience 为为应用程序指定的应用 ID URI。</span><span class="sxs-lookup"><span data-stu-id="63153-130">`aud` where audience is the App ID URI specified for the application.</span></span>
* <span data-ttu-id="63153-131">`tid` 是租户的租户 id Contoso.com。</span><span class="sxs-lookup"><span data-stu-id="63153-131">`tid` is the tenant id for Contoso.com.</span></span>
* <span data-ttu-id="63153-132">`iss` 是令牌颁发者 `https://api.botframework.com` 。</span><span class="sxs-lookup"><span data-stu-id="63153-132">`iss` is the token issuer, `https://api.botframework.com`.</span></span>

<span data-ttu-id="63153-133">对于代码处理，Webhook 必须验证令牌，确保令牌尚未过期，并检查它是否已由发布的 OpenID 配置签名。</span><span class="sxs-lookup"><span data-stu-id="63153-133">For your code handling, the webhook must validate the token, ensure it has not expired, and check whether it has been signed by the published OpenID configuration.</span></span> <span data-ttu-id="63153-134">在接受回调请求之前，还必须检查 aud 是否与应用 ID 匹配。</span><span class="sxs-lookup"><span data-stu-id="63153-134">You must also check whether aud matches your App ID before accepting the callback request.</span></span>

<span data-ttu-id="63153-135">有关详细信息，请参阅验证 [入站请求](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs)。</span><span class="sxs-lookup"><span data-stu-id="63153-135">For more information, see [validate inbound requests](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs).</span></span>

## <a name="next-step"></a><span data-ttu-id="63153-136">后续步骤</span><span class="sxs-lookup"><span data-stu-id="63153-136">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="63153-137">应用程序托管的媒体机器人的要求和注意事项</span><span class="sxs-lookup"><span data-stu-id="63153-137">Requirements and considerations for application-hosted media bots</span></span>](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
