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
# <a name="add-authentication-to-your-messaging-extension"></a><span data-ttu-id="df9e6-103">向您的邮件扩展添加身份验证</span><span class="sxs-lookup"><span data-stu-id="df9e6-103">Add authentication to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a><span data-ttu-id="df9e6-104">标识用户</span><span class="sxs-lookup"><span data-stu-id="df9e6-104">Identify the user</span></span>

<span data-ttu-id="df9e6-105">对服务的每个请求都包括执行请求的用户的已模糊处理 ID，以及用户的显示名称和 Azure Active Directory 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="df9e6-105">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="df9e6-106">`id`和`aadObjectId`值保证已通过身份验证的团队用户的。</span><span class="sxs-lookup"><span data-stu-id="df9e6-106">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="df9e6-107">它们可用作在您的服务中查找凭据或任何缓存状态时使用的键。</span><span class="sxs-lookup"><span data-stu-id="df9e6-107">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="df9e6-108">此外，每个请求都包含用户的 Azure Active Directory 租户 ID，可用于标识用户的组织。</span><span class="sxs-lookup"><span data-stu-id="df9e6-108">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="df9e6-109">如果适用，该请求还包含发出请求的团队和频道 Id。</span><span class="sxs-lookup"><span data-stu-id="df9e6-109">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="df9e6-110">身份验证</span><span class="sxs-lookup"><span data-stu-id="df9e6-110">Authentication</span></span>

<span data-ttu-id="df9e6-111">如果您的服务需要进行用户身份验证，则需要在用户登录后才能使用邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="df9e6-111">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="df9e6-112">如果您已编写用于用户签名的 bot 或选项卡，则应熟悉此部分。</span><span class="sxs-lookup"><span data-stu-id="df9e6-112">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="df9e6-113">序列如下所示：</span><span class="sxs-lookup"><span data-stu-id="df9e6-113">The sequence is as follows:</span></span>

1. <span data-ttu-id="df9e6-114">用户发出查询，或将默认查询自动发送到您的服务。</span><span class="sxs-lookup"><span data-stu-id="df9e6-114">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="df9e6-115">您的服务通过检查团队用户 ID 检查用户是否先进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="df9e6-115">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="df9e6-116">如果用户未通过身份验证，则发送回复`auth` ，并提供`openUrl`建议的操作，包括身份验证 URL。</span><span class="sxs-lookup"><span data-stu-id="df9e6-116">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="df9e6-117">Microsoft 团队客户端使用给定的身份验证 URL 启动承载你的网页的弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="df9e6-117">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="df9e6-118">用户登录后，应关闭窗口并向团队客户端发送 "身份验证代码"。</span><span class="sxs-lookup"><span data-stu-id="df9e6-118">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="df9e6-119">然后，团队客户端将查询重新发出到您的服务，其中包括在步骤5中传递的身份验证代码。</span><span class="sxs-lookup"><span data-stu-id="df9e6-119">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="df9e6-120">您的服务应验证步骤6中收到的身份验证代码是否与步骤5中的验证代码相匹配。</span><span class="sxs-lookup"><span data-stu-id="df9e6-120">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="df9e6-121">这可确保恶意用户不会尝试欺骗或危害登录流。</span><span class="sxs-lookup"><span data-stu-id="df9e6-121">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="df9e6-122">这将有效地 "关闭循环" 以完成安全身份验证序列。</span><span class="sxs-lookup"><span data-stu-id="df9e6-122">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="df9e6-123">使用登录操作进行响应</span><span class="sxs-lookup"><span data-stu-id="df9e6-123">Respond with a sign-in action</span></span>

<span data-ttu-id="df9e6-124">若要提示未经过身份验证的用户登录，请使用包含身份验证`openUrl` URL 的 "类型" 建议操作进行响应。</span><span class="sxs-lookup"><span data-stu-id="df9e6-124">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="df9e6-125">登录操作的响应示例</span><span class="sxs-lookup"><span data-stu-id="df9e6-125">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="df9e6-126">若要在团队弹出窗口中承载登录体验，URL 的域部分必须位于您的应用程序的有效域的列表中。</span><span class="sxs-lookup"><span data-stu-id="df9e6-126">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="df9e6-127">（请参阅清单架构中的[validDomains](~/resources/schema/manifest-schema.md#validdomains) 。）</span><span class="sxs-lookup"><span data-stu-id="df9e6-127">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="df9e6-128">启动登录流</span><span class="sxs-lookup"><span data-stu-id="df9e6-128">Start the sign-in flow</span></span>

<span data-ttu-id="df9e6-129">您的登录体验应响应且适合弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="df9e6-129">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="df9e6-130">它应与使用邮件传递的[Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)集成。</span><span class="sxs-lookup"><span data-stu-id="df9e6-130">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="df9e6-131">与在 Microsoft 团队中运行的其他嵌入式体验一样，窗口中的代码需要先调用`microsoftTeams.initialize()`。</span><span class="sxs-lookup"><span data-stu-id="df9e6-131">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="df9e6-132">如果你的代码执行 OAuth 流，则可以将团队用户 ID 传递到你的窗口，然后可以将其传递到 OAuth 登录 URL。</span><span class="sxs-lookup"><span data-stu-id="df9e6-132">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="df9e6-133">完成登录流</span><span class="sxs-lookup"><span data-stu-id="df9e6-133">Complete the sign-in flow</span></span>

<span data-ttu-id="df9e6-134">当登录请求完成并重定向回您的页面时，应执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="df9e6-134">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="df9e6-135">生成安全代码。</span><span class="sxs-lookup"><span data-stu-id="df9e6-135">Generate a security code.</span></span> <span data-ttu-id="df9e6-136">（可以是一个随机数字。）您需要将此代码与您的服务进行缓存，以及通过登录流（例如 OAuth 2.0 令牌）获取的凭据。</span><span class="sxs-lookup"><span data-stu-id="df9e6-136">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="df9e6-137">调用`microsoftTeams.authentication.notifySuccess`并传递安全代码。</span><span class="sxs-lookup"><span data-stu-id="df9e6-137">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="df9e6-138">此时，窗口将关闭，并将控制传递给团队客户端。</span><span class="sxs-lookup"><span data-stu-id="df9e6-138">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="df9e6-139">客户端现在可以重新发出原始用户查询，以及`state`属性中的安全代码。</span><span class="sxs-lookup"><span data-stu-id="df9e6-139">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="df9e6-140">您的代码可以使用安全代码查找之前存储的凭据以完成身份验证序列，然后完成用户请求。</span><span class="sxs-lookup"><span data-stu-id="df9e6-140">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="df9e6-141">重新颁发的请求示例</span><span class="sxs-lookup"><span data-stu-id="df9e6-141">Reissued request example</span></span>

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

