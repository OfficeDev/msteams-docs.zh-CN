---
title: 来电通知
description: 有关处理来自传入呼叫的通知的详细技术信息
ms.topic: conceptual
ms.localizationpriority: medium
keywords: 调用呼叫通知回调区域相关性
ms.date: 04/02/2019
ms.openlocfilehash: eb05499b32a0e62b9aa5b073770632c081b8526a
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155303"
---
# <a name="incoming-call-notifications"></a>来电通知

在[注册呼叫和会议机器人以使用 Microsoft Teams](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities)时，会提到用于呼叫 URL 的 Webhook。 此 URL 是自动程序的所有传入呼叫的 webhook 终结点。

## <a name="protocol-determination"></a>协议确定

传入通知以旧格式提供，用于与以前的 Skype[协议兼容](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true)。 为了将呼叫转换为 Microsoft Graph 协议，机器人必须确定通知是否采用旧格式并提供以下响应：

```http
HTTP/1.1 204 No Content
```

自动程序将再次接收通知，但这次在 Microsoft Graph协议。

在实时媒体平台的未来版本中，你可以配置应用程序支持的协议，以避免接收旧格式的初始回调。

下一节提供有关针对区域相关性重定向到部署的传入呼叫通知的详细信息。

## <a name="redirects-for-region-affinity"></a>区域相关性重定向

从托管呼叫的数据中心调用 webhook。 呼叫从任何数据中心开始，不会考虑区域关系。 通知将发送到你的部署，具体取决于 GeoDNS 分辨率。 如果应用程序通过检查初始通知有效负载或其他方式确定需要在不同的部署中运行，则应用程序将提供以下响应：

```http
HTTP/1.1 302 Found
Location: your-new-location
```

使机器人能够使用应答 API 应答 [传入](https://developer.microsoft.com/graph/docs/api-reference/beta/api/call_answer) 呼叫。 可以指定 以处理 `callbackUri` 此特定调用。 这适用于特定分区处理呼叫且您希望在 中嵌入此信息以路由到正确实例的有状态 `callbackUri` 实例。

下一节将提供有关通过检查张贴到 Webhook 的令牌对回调进行身份验证的详细信息。

## <a name="authenticate-the-callback"></a>对回调进行身份验证

自动程序必须检查张贴到 Webhook 的令牌以验证请求。 每次 API 发送到 webhook 时，HTTP POST 消息都会在授权标头中包含一个 OAuth 令牌作为一个 bearer 令牌，访问群体作为应用程序的应用程序 ID。

您的应用程序在接受回调请求之前必须验证此令牌。

以下示例代码用于对回调进行身份验证：

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

OAuth 令牌具有以下值，由 Skype：

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

发布的 OpenID <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> 配置可用于验证令牌。 每个 OAuth 令牌值使用如下：

* `aud` 其中 audience 为为应用程序指定的应用 ID URI。
* `tid` 是租户的租户 id Contoso.com。
* `iss` 是令牌颁发者 `https://api.botframework.com` 。

对于代码处理，webhook 必须验证令牌，确保令牌尚未过期，并检查它是否已由发布的 OpenID 配置签名。 在接受回调请求之前，还必须检查 aud 是否与应用 ID 匹配。

有关详细信息，请参阅验证 [入站请求](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [应用程序托管的媒体机器人的要求和注意事项](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)
