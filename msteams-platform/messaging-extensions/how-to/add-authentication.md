---
title: 为消息扩展添加身份验证
author: surbhigupta
description: 了解如何使用代码示例向消息传递扩展添加身份验证
ms.localizationpriority: high
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 36a2aa269bfc43f4c07e97a5c214e3081a38ffeb
ms.sourcegitcommit: 591bab4c7e01ac9099b9a540f149b64e6e31e6e8
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2022
ms.locfileid: "65135708"
---
# <a name="add-authentication-to-your-message-extension"></a>为消息扩展添加身份验证

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>标识用户

对服务的每个请求都包含用户 ID、用户的显示名称和 Azure Active Directory 对象 ID。

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

对于经过身份验证的 Teams 用户，确保提供 `id` 和 `aadObjectId` 值。 它们用作密钥来查找服务中的凭据或任何缓存状态。 此外，每个请求都包含 Azure Active Directory 租户 ID，用于标识用户的组织。 如果适用，请求还包含发起请求的团队 ID 和通道 ID。

## <a name="authentication"></a>身份验证

如果服务需要用户身份验证，则用户必须先登录，然后才能使用消息扩展。 身份验证步骤类似于机器人或选项卡。身份验证序列如下所示：

1. 用户发出查询，或默认查询会自动发送到服务。
1. 服务通过检查 Teams 用户 ID 来检查用户是否经过身份验证。
1. 如果用户未经过身份验证，请使用 `openUrl` 建议的操作（包括身份验证 URL）发回 `auth` 响应。
1. Microsoft Teams 客户端使用给定的身份验证 URL 启动托管网页的对话框。
1. 用户登录后，应关闭窗口并将 **身份验证代码** 发送到 Teams 客户端。
1. 然后，Teams 客户端会重新向服务发出查询，其中包括步骤 5 中传递的身份验证代码。

服务应验证步骤 6 中收到的身份验证代码是否与步骤 5 中的身份验证代码一致。 这可确保恶意用户不会尝试欺骗或破坏登录流。 这可以有效地“关闭循环”以完成安全身份验证序列。

### <a name="respond-with-a-sign-in-action"></a>使用登录操作进行响应

若要提示未经身份验证的用户登录，请使用包含身份验证 URL 的类型为 `openUrl` 的建议操作进行响应。

#### <a name="response-example-for-a-sign-in-action"></a>登录操作的响应示例

```json
{
  "composeExtension":{
    "type":"auth",
    "suggestedActions":{
      "actions":[
        {
          "type": "openUrl",
          "value": "https://example.com/auth",
          "title": "Sign in to this app"
        }
      ]
    }
  }
}
```

> [!NOTE]
>
> * 若要在 Teams 弹出窗口中托管登录体验，URL 的域部分必须位于应用的有效域列表中。有关详细信息，请参阅清单架构中的 [validDomains](~/resources/schema/manifest-schema.md#validdomains)。
> * 可以通过包含宽度和高度的查询字符串参数 `Value = $"{_siteUrl}/searchSettings.html?height=600&width=600"` 来定义身份验证弹出窗口的大小。

### <a name="start-the-sign-in-flow"></a>启动登录流

登录体验必须具有响应能力，并且适合弹出窗口。 它应与使用消息传递的 [Microsoft Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 集成。

与 Microsoft Teams 内运行的其他嵌入式体验一样，窗口内的代码也需要先调用 `microsoftTeams.initialize()`。 如果代码执行 OAuth 流，则可以将 Teams 用户 ID 传递到窗口，然后将其传递到 OAuth 登录 URL。

### <a name="complete-the-sign-in-flow"></a>完成登录流

当登录请求完成并重定向回页面后，必须执行以下步骤：

1. 生成安全代码（一个随机数）。必须在服务上缓存此代码，以及通过登录流获取的凭据，例如 OAuth 2.0 令牌。
1. 调用 `microsoftTeams.authentication.notifySuccess` 并传递安全代码。

此时，窗口会关闭，并且控件将传递给 Teams 客户端。 客户端现在会重新发出原始用户查询，以及属性中 `state` 的安全代码。 你的代码可以使用安全代码来查找之前存储的凭据以完成身份验证序列，然后完成用户请求。

#### <a name="reissued-request-example"></a>重新发出的请求示例

```json
{
    "name": "composeExtension/query",
    "value": {
        "commandId": "insertWiki",
        "parameters": [{
            "name": "searchKeyword",
            "value": "lakers"
        }],
        "state": "12345",
        "queryOptions": {
            "skip": 0,
            "count": 25
        }
    },
    "type": "invoke",
    "timestamp": "2017-04-26T05:18:25.629Z",
    "localTimestamp": "2017-04-25T22:18:25.629-07:00",
    "entities": [{
        "locale": "en-US",
        "country": "US",
        "platform": "Web",
        "type": "clientInfo"
    }],
    "text": "",
    "attachments": [],
    "address": {
        "id": "f:7638210432489287768",
        "channelId": "msteams",
        "user": {
            "id": "29:1A5TJWHkbOwSyu_L9Ktk9QFI1d_kBOEPeNEeO1INscpKHzHTvWfiau5AX_6y3SuiOby-r73dzHJ17HipUWqGPgw",
            "aadObjectId": "fc8ca1c0-d043-4af6-b09f-141536207403"
        },
        "conversation": {
            "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
        },
        "bot": {
            "id": "28:c073afa8-7e77-4f92-b3e7-aa589e952a3e",
            "name": "maotestbot2"
        },
        "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
        "useAuth": true
    },
    "source": "msteams"
}
```

## <a name="code-sample"></a>代码示例

|**示例名称** | **说明** |**.NET** | **Node.js**|
|----------------|-----------------|--------------|----------------|
|消息扩展 - 身份验证和配置 | 具有配置页的消息扩展将接受搜索请求，并在用户登录后返回结果。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)|

## <a name="see-also"></a>另请参阅

[对消息扩展的单一登录 (SSO) 支持](~/messaging-extensions/how-to/enable-sso-auth-me.md)
