---
title: 向您的邮件扩展添加身份验证
author: clearab
description: 如何向邮件扩展添加身份验证
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f7ebbcd99b1ec35900de7ec2f54f93263918e945
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673059"
---
# <a name="add-authentication-to-your-messaging-extension"></a>向您的邮件扩展添加身份验证

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a>标识用户

对服务的每个请求都包括执行请求的用户的已模糊处理 ID，以及用户的显示名称和 Azure Active Directory 对象 ID。

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

`id`和`aadObjectId`值保证已通过身份验证的团队用户的。 它们可用作在您的服务中查找凭据或任何缓存状态时使用的键。 此外，每个请求都包含用户的 Azure Active Directory 租户 ID，可用于标识用户的组织。 如果适用，该请求还包含发出请求的团队和频道 Id。

## <a name="authentication"></a>身份验证

如果您的服务需要进行用户身份验证，则需要在用户登录后才能使用邮件扩展。 如果您已编写用于用户签名的 bot 或选项卡，则应熟悉此部分。

序列如下所示：

1. 用户发出查询，或将默认查询自动发送到您的服务。
2. 您的服务通过检查团队用户 ID 检查用户是否先进行身份验证。
3. 如果用户未通过身份验证，则发送回复`auth` ，并提供`openUrl`建议的操作，包括身份验证 URL。
4. Microsoft 团队客户端使用给定的身份验证 URL 启动承载你的网页的弹出窗口。
5. 用户登录后，应关闭窗口并向团队客户端发送 "身份验证代码"。
6. 然后，团队客户端将查询重新发出到您的服务，其中包括在步骤5中传递的身份验证代码。

您的服务应验证步骤6中收到的身份验证代码是否与步骤5中的验证代码相匹配。 这可确保恶意用户不会尝试欺骗或危害登录流。 这将有效地 "关闭循环" 以完成安全身份验证序列。

### <a name="respond-with-a-sign-in-action"></a>使用登录操作进行响应

若要提示未经过身份验证的用户登录，请使用包含身份验证`openUrl` URL 的 "类型" 建议操作进行响应。

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
> 若要在团队弹出窗口中承载登录体验，URL 的域部分必须位于您的应用程序的有效域的列表中。 （请参阅清单架构中的[validDomains](~/resources/schema/manifest-schema.md#validdomains) 。）

### <a name="start-the-sign-in-flow"></a>启动登录流

您的登录体验应响应且适合弹出窗口。 它应与使用邮件传递的[Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)集成。

与在 Microsoft 团队中运行的其他嵌入式体验一样，窗口中的代码需要先调用`microsoftTeams.initialize()`。 如果你的代码执行 OAuth 流，则可以将团队用户 ID 传递到你的窗口，然后可以将其传递到 OAuth 登录 URL。

### <a name="complete-the-sign-in-flow"></a>完成登录流

当登录请求完成并重定向回您的页面时，应执行以下步骤：

1. 生成安全代码。 （可以是一个随机数字。）您需要将此代码与您的服务进行缓存，以及通过登录流（例如 OAuth 2.0 令牌）获取的凭据。
2. 调用`microsoftTeams.authentication.notifySuccess`并传递安全代码。

此时，窗口将关闭，并将控制传递给团队客户端。 客户端现在可以重新发出原始用户查询，以及`state`属性中的安全代码。 您的代码可以使用安全代码查找之前存储的凭据以完成身份验证序列，然后完成用户请求。

#### <a name="reissued-request-example"></a>重新颁发的请求示例

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

