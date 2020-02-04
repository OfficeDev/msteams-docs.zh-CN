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
# <a name="incoming-call-notifications-technical-details"></a>传入呼叫通知：技术详细信息

在[为 Microsoft 团队注册呼叫和会议机器人](./registering-calling-bot.md#creating-a-new-bot-or-adding-calling-capabilities-to-an-existing-bot)时，我们提到了用于所有传入呼叫的 webhook **（用于呼叫）** URL-你的 bot 的所有传入呼叫的 webhook 终结点。 本主题讨论响应这些通知所需的技术详细信息。

## <a name="protocol-determination"></a>协议确定

传入通知以旧版格式提供，以与以前的[Skype 协议](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0)兼容。 为了将呼叫转换为 Microsoft Graph 协议，你的 bot 必须确定通知是否为旧格式，并在以下情况下回复：

```http
HTTP/1.1 204 No Content
```

你的 bot 将再次收到通知，但这次在 Microsoft Graph 协议中。

在实时媒体平台的未来版本中，我们将允许您配置您的应用程序支持的协议，以避免以旧格式接收初始回调。

## <a name="redirects-for-region-affinity"></a>区域关联的重定向

你将从托管呼叫的数据中心呼叫你的 webhook。 呼叫可能会在任何数据中心开始，并且不会考虑区域相关性。 通知将发送到您的部署，具体取决于 GeoDNS 解决方案。 如果您的应用程序通过检查初始通知负载或以其他方式（如果需要在不同的部署中运行）确定应用程序，则应用程序可能会通过以下方式回复：

```http
HTTP/1.1 302 Found
Location: your-new-location
```

使用 "[应答](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer)API" 使你的 bot 能够应答传入呼叫。 您可以指定处理`callbackUri`此特定调用的。 这对于您的__ 呼叫由特定分区进行处理且您希望将`callbackUri`此信息嵌入到右侧实例的有状态的实例很有用。

## <a name="authenticating-the-callback"></a>对回调进行身份验证

你的 bot 应检查发布到你的 webhook 的令牌以验证请求。 每当 API 发布到 webhook 时，HTTP POST 邮件都会在授权标头中包含一个 OAuth 令牌作为持有者作为应用程序的应用 ID 的持有者令牌。

您的应用程序应在接受回调请求之前验证此令牌。

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

OAuth 令牌的值将如下所示，并将由 Skype 签署。 发布的 OpenID 配置<https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration>可用于验证令牌。

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

* **aud**受众是为应用程序指定的应用 ID URI。
* **tid**是 Contoso.com 的租户 id。
* **iss**是令牌颁发者`https://api.botframework.com`。

处理 webhook 的代码应验证令牌，确保其未过期，并检查是否已通过已发布的 OpenID 配置对其进行签名。 您还应检查**aud**是否符合您的应用程序 ID，然后再接受回调请求。

[示例](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs)演示如何验证入站请求。
