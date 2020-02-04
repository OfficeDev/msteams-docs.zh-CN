---
title: 有关处理传入呼叫通知的技术详细信息
description: 有关处理来自传入呼叫的通知的详细技术信息
keywords: 调用呼叫通知回调区域相关性
ms.date: 04/02/2019
ms.openlocfilehash: be8860ff70cd7dff4fd9599079ea7aab4f454174
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673415"
---
# <a name="incoming-call-notifications-technical-details"></a><span data-ttu-id="46601-104">传入呼叫通知：技术详细信息</span><span class="sxs-lookup"><span data-stu-id="46601-104">Incoming call notifications: technical details</span></span>

<span data-ttu-id="46601-105">在[为 Microsoft 团队注册呼叫和会议机器人](./registering-calling-bot.md#creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot)时，我们提到了用于所有传入呼叫的 webhook **（用于呼叫）** URL-你的 bot 的所有传入呼叫的 webhook 终结点。</span><span class="sxs-lookup"><span data-stu-id="46601-105">In [Registering a calling and meeting bot for Microsoft Teams](./registering-calling-bot.md#creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot), we mentioned the **Webhook (for calling)** URL — the webhook endpoint for all incoming calls to your bot.</span></span> <span data-ttu-id="46601-106">本主题讨论响应这些通知所需的技术详细信息。</span><span class="sxs-lookup"><span data-stu-id="46601-106">This topic discusses the technical details you'll need to respond to these notifications.</span></span>

## <a name="protocol-determination"></a><span data-ttu-id="46601-107">协议确定</span><span class="sxs-lookup"><span data-stu-id="46601-107">Protocol determination</span></span>

<span data-ttu-id="46601-108">传入通知以旧版格式提供，以与以前的[Skype 协议](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0)兼容。</span><span class="sxs-lookup"><span data-stu-id="46601-108">The incoming notification is provided in legacy format for compatibility with the previous [Skype protocol](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0).</span></span> <span data-ttu-id="46601-109">为了将呼叫转换为 Microsoft Graph 协议，你的 bot 必须确定通知是否为旧格式，并在以下情况下回复：</span><span class="sxs-lookup"><span data-stu-id="46601-109">In order to convert the call to the Microsoft Graph protocol, your bot must determine whether the notification is in legacy format and reply with:</span></span>

```http
HTTP/1.1 204 No Content
```

<span data-ttu-id="46601-110">你的 bot 将再次收到通知，但这次在 Microsoft Graph 协议中。</span><span class="sxs-lookup"><span data-stu-id="46601-110">Your bot will receive the notification again, but this time in the Microsoft Graph protocol.</span></span>

<span data-ttu-id="46601-111">在实时媒体平台的未来版本中，我们将允许您配置您的应用程序支持的协议，以避免以旧格式接收初始回调。</span><span class="sxs-lookup"><span data-stu-id="46601-111">In a future release of the Real-time Media Platform, we'll allow you to configure the protocol your application supports to avoid receiving the initial callback in the legacy format.</span></span>

## <a name="redirects-for-region-affinity"></a><span data-ttu-id="46601-112">区域关联的重定向</span><span class="sxs-lookup"><span data-stu-id="46601-112">Redirects for region affinity</span></span>

<span data-ttu-id="46601-113">你将从托管呼叫的数据中心呼叫你的 webhook。</span><span class="sxs-lookup"><span data-stu-id="46601-113">You'll call your webhook from the data-center hosting the call.</span></span> <span data-ttu-id="46601-114">呼叫可能会在任何数据中心开始，并且不会考虑区域相关性。</span><span class="sxs-lookup"><span data-stu-id="46601-114">The call may start in any data center and doesn't take into account region affinities.</span></span> <span data-ttu-id="46601-115">通知将发送到您的部署，具体取决于 GeoDNS 解决方案。</span><span class="sxs-lookup"><span data-stu-id="46601-115">The notification will be sent to your deployment depending on the GeoDNS resolution.</span></span> <span data-ttu-id="46601-116">如果您的应用程序通过检查初始通知负载或以其他方式（如果需要在不同的部署中运行）确定应用程序，则应用程序可能会通过以下方式回复：</span><span class="sxs-lookup"><span data-stu-id="46601-116">If your application determines, by inspecting the initial notification payload or otherwise, that it needs to run in a different deployment, the application may reply with:</span></span>

```http
HTTP/1.1 302 Found
Location: your-new-location
```

<span data-ttu-id="46601-117">使用 "[应答](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer)API" 使你的 bot 能够应答传入呼叫。</span><span class="sxs-lookup"><span data-stu-id="46601-117">Enable your bot to answer an incoming call using the [answer](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) API.</span></span> <span data-ttu-id="46601-118">您可以指定处理`callbackUri`此特定调用的。</span><span class="sxs-lookup"><span data-stu-id="46601-118">You can specify the `callbackUri` to handle this particular call.</span></span> <span data-ttu-id="46601-119">这对于您的__ 呼叫由特定分区进行处理且您希望将`callbackUri`此信息嵌入到右侧实例的有状态的实例很有用。</span><span class="sxs-lookup"><span data-stu-id="46601-119">This is useful for _stateful_ instances where your call is handled by a particular partition and you want to embed this information in the `callbackUri` for routing to the right instance.</span></span>

## <a name="authenticating-the-callback"></a><span data-ttu-id="46601-120">对回调进行身份验证</span><span class="sxs-lookup"><span data-stu-id="46601-120">Authenticating the callback</span></span>

<span data-ttu-id="46601-121">你的 bot 应检查发布到你的 webhook 的令牌以验证请求。</span><span class="sxs-lookup"><span data-stu-id="46601-121">Your bot should inspect the token posted to your webhook to validate the request.</span></span> <span data-ttu-id="46601-122">每当 API 发布到 webhook 时，HTTP POST 邮件都会在授权标头中包含一个 OAuth 令牌作为持有者作为应用程序的应用 ID 的持有者令牌。</span><span class="sxs-lookup"><span data-stu-id="46601-122">Whenever the API posts to the webhook, the HTTP POST message contains an OAuth token in the Authorization header as a Bearer token, with audience as your application's App ID.</span></span>

<span data-ttu-id="46601-123">您的应用程序应在接受回调请求之前验证此令牌。</span><span class="sxs-lookup"><span data-stu-id="46601-123">Your application should validate this token before accepting the callback request.</span></span>

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

<span data-ttu-id="46601-124">OAuth 令牌的值将如下所示，并将由 Skype 签署。</span><span class="sxs-lookup"><span data-stu-id="46601-124">The OAuth token will have values like the following, and will be signed by Skype.</span></span> <span data-ttu-id="46601-125">发布的 OpenID 配置<https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration>可用于验证令牌。</span><span class="sxs-lookup"><span data-stu-id="46601-125">The OpenID configuration published at <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> can be used to verify the token.</span></span>

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

* <span data-ttu-id="46601-126">**aud**受众是为应用程序指定的应用 ID URI。</span><span class="sxs-lookup"><span data-stu-id="46601-126">**aud** audience is the App ID URI specified for the application.</span></span>
* <span data-ttu-id="46601-127">**tid**是 Contoso.com 的租户 id。</span><span class="sxs-lookup"><span data-stu-id="46601-127">**tid** is the tenant id for Contoso.com.</span></span>
* <span data-ttu-id="46601-128">**iss**是令牌颁发者`https://api.botframework.com`。</span><span class="sxs-lookup"><span data-stu-id="46601-128">**iss** is the token issuer, `https://api.botframework.com`.</span></span>

<span data-ttu-id="46601-129">处理 webhook 的代码应验证令牌，确保其未过期，并检查是否已通过已发布的 OpenID 配置对其进行签名。</span><span class="sxs-lookup"><span data-stu-id="46601-129">Your code handling the webhook should validate the token, ensure it hasn't expired, and check whether it has been signed by our published OpenID configuration.</span></span> <span data-ttu-id="46601-130">您还应检查**aud**是否符合您的应用程序 ID，然后再接受回调请求。</span><span class="sxs-lookup"><span data-stu-id="46601-130">You should also check whether **aud** matches your App ID before accepting the callback request.</span></span>

<span data-ttu-id="46601-131">[示例](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs)演示如何验证入站请求。</span><span class="sxs-lookup"><span data-stu-id="46601-131">[Sample](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs) shows how to validate inbound requests.</span></span>
