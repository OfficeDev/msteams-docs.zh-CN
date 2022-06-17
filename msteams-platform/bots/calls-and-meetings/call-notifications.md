---
title: 来电通知
description: 在本模块中，了解有关使用代码示例处理来自传入呼叫的通知、重定向和身份验证呼叫的详细技术信息
ms.topic: conceptual
ms.localizationpriority: medium
ms.date: 04/02/2019
ms.openlocfilehash: fd68b85a3c6f5f4682a728461d792093bcd8cac0
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143828"
---
# <a name="incoming-call-notifications"></a>来电通知

在[为 Microsoft Teams 注册呼叫和会议机器人](./registering-calling-bot.md#create-new-bot-or-add-calling-capabilities)时，系统会提到用于调用 URL 的 Webhook。 此 URL 是对机器人的所有传入呼叫的 Webhook 终结点。

## <a name="protocol-determination"></a>协议确定

传入通知以旧格式提供，以便与以前的 [Skype 协议](/azure/bot-service/dotnet/bot-builder-dotnet-real-time-media-concepts?view=azure-bot-service-3.0&preserve-view=true)兼容。 为了将调用转换为 Microsoft Graph 协议，机器人必须确定通知是否采用旧格式，并提供以下响应：

```http
HTTP/1.1 204 No Content
```

机器人会再次收到通知，但这次是采用 Microsoft Graph 协议的格式。

在将来发布的实时媒体平台中，你可以配置应用程序支持的协议，以避免以旧格式接收初始回拨。

下一节提供有关针对部署的区域相关性重定向来电通知的详细信息。

## <a name="redirects-for-region-affinity"></a>针对区域相关性的重定向

可从托管呼叫的数据中心调用 Webhook。 调用从任何数据中心开始，不考虑区域相关性。 通知将发送到部署，具体取决于 GeoDNS 解析。 如果应用程序通过检查初始通知负载或其他方式确定它需要在其他部署中运行，则该应用程序会提供以下响应：

```http
HTTP/1.1 302 Found
Location: your-new-location
```

允许机器人使用[应答](/graph/api/call-answer?view=graph-rest-1.0&tabs=http&preserve-view=true) API 接听来电。 可以指定 `callbackUri` 处理此特定呼叫。 这对于有状态实例非常有用，在这些实例中，你的呼叫由特定分区处理，并且你希望将此信息嵌入到 `callbackUri` 中，以便路由到正确的实例。

下一节提供有关通过检查发布到 Webhook 的令牌对回拨进行身份验证的详细信息。

## <a name="authenticate-the-callback"></a>对回拨进行身份验证

机器人必须检查发布到 Webhook 的令牌才能验证请求。 每当 API 发布到 Webhook 时，HTTP POST 消息都会在身份验证标头中包含一个 OAuth 令牌作为持有者令牌，并将受众作为应用程序的应用 ID。

你的应用程序必须先验证此令牌，然后才能接受回拨请求。

以下示例代码用于对回拨进行身份验证：

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

OAuth 令牌具有以下值，并由 Skype 签名：

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

在 <https://api.aps.skype.com/v1/.well-known/OpenIdConfiguration> 上发布的 OpenID 配置可用于验证令牌。 每个 OAuth 令牌值均按以下方式使用：

* `aud`，其中受众是为应用程序指定的应用 ID URI。
* `tid` 是 Contoso.com 的租户 ID。
* `iss` 是令牌颁发者，即 `https://api.botframework.com`

对于代码处理，Webhook 必须验证令牌，确保令牌尚未过期，并检查它是否已由已发布的 OpenID 配置进行签名。 在接受回拨请求之前，你还必须检查 aud 是否与应用 ID 匹配。

有关详细信息，请参阅[验证入站请求](https://github.com/microsoftgraph/microsoft-graph-comms-samples/blob/master/Samples/Common/Sample.Common/Authentication/AuthenticationProvider.cs)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [应用程序托管的媒体机器人的要求和注意事项](~/bots/calls-and-meetings/requirements-considerations-application-hosted-media-bots.md)

## <a name="see-also"></a>另请参阅

* [设置自动助理](/microsoftteams/create-a-phone-system-auto-attendant)
* [在 Android 和 Teams 视频电话设备上为 Microsoft Teams 会议室设置自动应答](/microsoftteams/set-up-auto-answer-on-teams-android)