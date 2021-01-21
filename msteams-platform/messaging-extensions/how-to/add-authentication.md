---
title: 向邮件扩展添加身份验证
author: clearab
description: 如何向邮件扩展添加身份验证
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 4ebe65af06240d13ceb99fe3b7640ab402d716c5
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911868"
---
# <a name="add-authentication-to-your-messaging-extension"></a>向邮件扩展添加身份验证

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>标识用户

每个对服务的请求都包括执行请求的用户的模糊 ID，以及用户的 显示名称 和 Azure Active Directory 对象 ID。

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

和 `id` `aadObjectId` 值保证为经过身份验证的 Teams 用户的值。 它们可用于在服务中查找凭据或任何缓存状态。 此外，每个请求都包含用户的 Azure Active Directory 租户 ID，可用于标识用户的组织。 如果适用，请求还包含发起请求的团队和频道的 ID。

## <a name="authentication"></a>身份验证

如果服务需要用户身份验证，则需要先登录用户，然后才能使用消息传递扩展。 如果你已编写用于登录用户的自动程序或选项卡，则本节应该很熟悉。

顺序如下所示：

1. 用户发出查询，或者默认查询会自动发送到服务。
2. 你的服务通过检查 Teams 用户 ID 来检查用户是否已首先进行身份验证。
3. 如果用户尚未进行身份验证，请发送回包含建议操作（包括身份验证 `auth` `openUrl` URL）的响应。
4. Microsoft Teams 客户端使用给定的身份验证 URL 启动承载网页的弹出窗口。
5. 用户登录后，应关闭窗口，并将"身份验证代码"发送到 Teams 客户端。
6. 然后，Teams 客户端重新向服务提供查询，其中包括步骤 5 中传递的身份验证代码。

服务应验证步骤 6 中收到的身份验证代码是否与步骤 5 中的身份验证代码匹配。 这可确保恶意用户不会尝试欺骗或破坏登录流。 这实际上"关闭循环"以完成安全身份验证序列。

### <a name="respond-with-a-sign-in-action"></a>使用登录操作响应

若要提示未经身份验证的用户登录，请响应包含身份验证 URL 的推荐操作 `openUrl` 类型。

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
> 若要在 Teams 弹出窗口中托管登录体验，URL 的域部分必须位于应用的有效域列表中。  (清单[架构中查看 validDomains。) ](~/resources/schema/manifest-schema.md#validdomains)

### <a name="start-the-sign-in-flow"></a>启动登录流

你的登录体验应该具有响应性，并且适合弹出窗口。 它应与使用消息传递 [的 Microsoft Teams JavaScript](/javascript/api/overview/msteams-client)客户端 SDK 集成。

与其他在 Microsoft Teams 内运行的嵌入体验一样，窗口内的代码需要先调用 `microsoftTeams.initialize()` 。 如果你的代码执行 OAuth 流，你可以将 Teams 用户 ID 传递到你的窗口中，然后可以将它传递到 OAuth 登录 URL。

### <a name="complete-the-sign-in-flow"></a>完成登录流程

当登录请求完成并重定向回你的页面时，它应执行以下步骤：

1. 生成安全代码。  (可以是随机数字。) 您需要在服务上缓存此代码，以及通过登录流获取的凭据 (如 OAuth 2.0 令牌) 。
2. 调用 `microsoftTeams.authentication.notifySuccess` 并传递安全代码。

此时，窗口关闭，控制权将传递给 Teams 客户端。 客户端现在可以重新发送原始用户查询以及属性中的安全 `state` 代码。 代码可以使用安全代码查找之前存储的凭据，以完成身份验证序列，然后完成用户请求。

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

## <a name="samples"></a>示例
有关显示邮件扩展身份验证过程的示例代码，请参阅：

[Microsoft Teams 消息传递扩展身份验证示例](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)

 
