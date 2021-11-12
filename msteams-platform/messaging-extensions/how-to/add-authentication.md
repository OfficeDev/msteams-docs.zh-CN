---
title: 向邮件扩展添加身份验证
author: surbhigupta
description: 了解如何使用代码示例和示例向消息传递扩展添加身份验证
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 83c7ce4f7897014345fd071b28273ade5907a917
ms.sourcegitcommit: 1431dfe08d5a19a63dbf1542a2e6c661e4dd7fc1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/12/2021
ms.locfileid: "60949094"
---
# <a name="add-authentication-to-your-messaging-extension"></a>向邮件扩展添加身份验证

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>标识用户

每个对服务的请求都包括用户 ID、显示名称和Azure Active Directory ID。

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

和 `id` `aadObjectId` 值保证经过身份验证的用户Teams。 它们用作在服务中查找凭据或任何缓存状态的密钥。 此外，每个请求Azure Active Directory租户 ID，用于标识用户的组织。 如果适用，请求还包含发起请求的团队 ID 和频道 ID。

## <a name="authentication"></a>身份验证

如果服务需要用户身份验证，则用户必须先登录，然后才能使用消息传递扩展。 身份验证步骤类似于自动程序或选项卡的步骤。顺序如下所示：

1. 用户发出查询或默认查询将自动发送到您的服务。
1. 服务通过检查用户 ID 来检查用户Teams身份验证。
1. 如果用户未经过身份验证，请发送回包含建议操作（包括身份验证 `auth` `openUrl` URL）的响应。
1. 客户端Microsoft Teams给定身份验证 URL 启动托管网页的对话框。
1. 用户登录后，应关闭窗口，并将身份验证代码发送到 Teams客户端。
1. 然后Teams客户端向服务重新提供查询，其中包括步骤 5 中传递的身份验证代码。

服务应验证步骤 6 中收到的身份验证代码是否与步骤 5 中的身份验证代码匹配。 这可确保恶意用户不会尝试欺骗或破坏登录流。 这实际上"关闭循环"以完成安全身份验证序列。

### <a name="respond-with-a-sign-in-action"></a>通过登录操作响应

若要提示未经身份验证的用户登录，请通过包含身份验证 URL 的类型的建议操作 `openUrl` 进行响应。

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
> 若要在弹出窗口中托管登录Teams，URL 的域部分必须位于应用的有效域列表中。 有关详细信息，请参阅[清单架构中的 validDomains。](~/resources/schema/manifest-schema.md#validdomains)

### <a name="start-the-sign-in-flow"></a>启动登录流程

登录体验必须响应迅速且适合弹出窗口。 它应与使用消息传递[Microsoft Teams JavaScript](/javascript/api/overview/msteams-client)客户端 SDK 集成。

与在 Microsoft Teams 内运行的其他嵌入体验一样，窗口内的代码需要先调用 `microsoftTeams.initialize()` 。 如果你的代码执行 OAuth 流，你可以将Teams ID 传递到你的窗口中，然后将它传递到 OAuth 登录 URL。

### <a name="complete-the-sign-in-flow"></a>完成登录流程

当登录请求完成并重定向回你的页面时，它必须执行以下步骤：

1. 生成一个安全代码，一个随机数字。 您必须在服务上缓存此代码，以及通过登录流获取的凭据，如 OAuth 2.0 令牌。
1. 调用 `microsoftTeams.authentication.notifySuccess` 并传递安全代码。

此时，窗口关闭，控件将传递给Teams客户端。 客户端现在重新提供原始用户查询以及 属性中的安全 `state` 代码。 代码可以使用安全代码查找之前存储的凭据以完成身份验证序列，然后完成用户请求。

#### <a name="reissued-request-example"></a>重新请求示例

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
|邮件扩展 - 身份验证和配置 | 具有配置页面、接受搜索请求和在用户登录后返回结果的消息扩展。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[View](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)| 

## <a name="see-also"></a>另请参阅

[单一登录 (SSO) 邮件扩展支持](~/messaging-extensions/how-to/enable-sso-auth-me.md)
