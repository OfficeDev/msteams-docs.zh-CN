---
title: 向邮件扩展添加身份验证
author: clearab
description: 如何向邮件扩展添加身份验证
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: d673f52e63ba845675f6631470af68d65c7297ad
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449568"
---
# <a name="add-authentication-to-your-messaging-extension"></a><span data-ttu-id="e8e0d-103">向邮件扩展添加身份验证</span><span class="sxs-lookup"><span data-stu-id="e8e0d-103">Add authentication to your messaging extension</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="identify-the-user"></a><span data-ttu-id="e8e0d-104">标识用户</span><span class="sxs-lookup"><span data-stu-id="e8e0d-104">Identify the user</span></span>

<span data-ttu-id="e8e0d-105">对服务的每个请求包括执行请求的用户的模糊 ID，以及用户的 显示名称 和 Azure Active Directory 对象 ID。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-105">Every request to your services includes the obfuscated ID of the user that performed the request, as well as the user's display name and Azure Active Directory object ID.</span></span>

```json
"from": {
  "id": "29:1C7dbRrC_5yzN1RGtZIrcWT0xz88KPGP9sxdpVpV8sODlgPHeQE9RqQ02hnpuKzy6zZ-AaZx6swUOMj_Dsdse3TQ4sIaeebbFBF-VgjJy_nY",
  "name": "Larry Jin",
  "aadObjectId": "cd723fa0-0591-416a-9290-e93ecf3a9b92"
},
```

<span data-ttu-id="e8e0d-106">和 `id` `aadObjectId` 值保证为经过身份验证的 Teams 用户的值。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-106">The `id` and `aadObjectId` values are guaranteed to be that of the authenticated Teams user.</span></span> <span data-ttu-id="e8e0d-107">它们可以用作在服务中查找凭据或任何缓存状态的密钥。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-107">They can be used as keys to look up credentials or any cached state in your service.</span></span> <span data-ttu-id="e8e0d-108">此外，每个请求都包含用户的 Azure Active Directory 租户 ID，可用于标识用户的组织。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-108">In addition, each request contains the Azure Active Directory tenant ID of the user, which can be used to identify the user’s organization.</span></span> <span data-ttu-id="e8e0d-109">如果适用，请求还包含源自请求的团队和频道的 ID。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-109">If applicable, the request also contains the team and channel IDs from which the request originated.</span></span>

## <a name="authentication"></a><span data-ttu-id="e8e0d-110">身份验证</span><span class="sxs-lookup"><span data-stu-id="e8e0d-110">Authentication</span></span>

<span data-ttu-id="e8e0d-111">如果服务需要用户身份验证，则需要先登录用户，然后才能使用消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-111">If your service requires user authentication, you need to sign in the user before he or she can use the messaging extension.</span></span> <span data-ttu-id="e8e0d-112">如果已编写登录用户的自动程序或选项卡，则本节应该很熟悉。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-112">If you have written a bot or a tab that signs in the user, this section should be familiar.</span></span>

<span data-ttu-id="e8e0d-113">顺序如下所示：</span><span class="sxs-lookup"><span data-stu-id="e8e0d-113">The sequence is as follows:</span></span>

1. <span data-ttu-id="e8e0d-114">用户发出查询，或者默认查询会自动发送到你的服务。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-114">User issues a query, or the default query is automatically sent to your service.</span></span>
2. <span data-ttu-id="e8e0d-115">你的服务会检查用户是否已首先通过检查 Teams 用户 ID 进行身份验证。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-115">Your service checks whether the user has first authenticated by inspecting the Teams user ID.</span></span>
3. <span data-ttu-id="e8e0d-116">如果用户尚未进行身份验证，请发送回包含建议操作（包括身份验证 `auth` `openUrl` URL）的响应。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-116">If the user has not authenticated, send back an `auth` response with an `openUrl` suggested action including the authentication URL.</span></span>
4. <span data-ttu-id="e8e0d-117">Microsoft Teams 客户端使用给定的身份验证 URL 启动托管网页的弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-117">The Microsoft Teams client launches a pop-up window hosting your webpage using the given authentication URL.</span></span>
5. <span data-ttu-id="e8e0d-118">用户登录后，应关闭窗口，并将"身份验证代码"发送到 Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-118">After the user signs in, you should close your window and send an "authentication code" to the Teams client.</span></span>
6. <span data-ttu-id="e8e0d-119">然后，Teams 客户端重新向服务提供查询，其中包括步骤 5 中传递的身份验证代码。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-119">The Teams client then reissues the query to your service, which includes the authentication code passed in step 5.</span></span>

<span data-ttu-id="e8e0d-120">服务应验证步骤 6 中收到的身份验证代码是否与步骤 5 中的身份验证代码匹配。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-120">Your service should verify that the authentication code received in step 6 matches the one from step 5.</span></span> <span data-ttu-id="e8e0d-121">这可确保恶意用户不会尝试欺骗或破坏登录流。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-121">This ensures that a malicious user does not try to spoof or compromise the sign-in flow.</span></span> <span data-ttu-id="e8e0d-122">这实际上"关闭循环"以完成安全身份验证序列。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-122">This effectively "closes the loop" to finish the secure authentication sequence.</span></span>

### <a name="respond-with-a-sign-in-action"></a><span data-ttu-id="e8e0d-123">使用登录操作响应</span><span class="sxs-lookup"><span data-stu-id="e8e0d-123">Respond with a sign-in action</span></span>

<span data-ttu-id="e8e0d-124">若要提示未经身份验证的用户登录，请响应包含身份验证 URL 的推荐操作 `openUrl` 类型。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-124">To prompt an unauthenticated user to sign in, respond with a suggested action of type `openUrl` that includes the authentication URL.</span></span>

#### <a name="response-example-for-a-sign-in-action"></a><span data-ttu-id="e8e0d-125">登录操作的响应示例</span><span class="sxs-lookup"><span data-stu-id="e8e0d-125">Response example for a sign-in action</span></span>

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
> <span data-ttu-id="e8e0d-126">若要在 Teams 弹出窗口中托管登录体验，URL 的域部分必须位于你的应用的有效域列表中。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-126">For the sign-in experience to be hosted in a Teams pop-up, the domain portion of the URL must be in your app’s list of valid domains.</span></span> <span data-ttu-id="e8e0d-127"> (清单架构中查看[validDomains。) ](~/resources/schema/manifest-schema.md#validdomains)</span><span class="sxs-lookup"><span data-stu-id="e8e0d-127">(See [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema.)</span></span>

### <a name="start-the-sign-in-flow"></a><span data-ttu-id="e8e0d-128">启动登录流</span><span class="sxs-lookup"><span data-stu-id="e8e0d-128">Start the sign-in flow</span></span>

<span data-ttu-id="e8e0d-129">你的登录体验应该具有响应性，并且适合弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-129">Your sign-in experience should be responsive and fit within a popup window.</span></span> <span data-ttu-id="e8e0d-130">它应与 [使用消息传递的 Microsoft Teams JavaScript](/javascript/api/overview/msteams-client)客户端 SDK 集成。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-130">It should integrate with the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client), which uses message passing.</span></span>

<span data-ttu-id="e8e0d-131">与其他在 Microsoft Teams 内运行的嵌入体验一样，窗口内的代码需要先调用 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-131">As with other embedded experiences running inside Microsoft Teams, your code inside the window needs to first call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="e8e0d-132">如果你的代码执行 OAuth 流，你可以将 Teams 用户 ID 传递到你的窗口，然后可以将它传递到 OAuth 登录 URL。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-132">If your code performs an OAuth flow, you can pass the Teams user ID into your window, which then can pass it to the OAuth sign-in URL.</span></span>

### <a name="complete-the-sign-in-flow"></a><span data-ttu-id="e8e0d-133">完成登录流程</span><span class="sxs-lookup"><span data-stu-id="e8e0d-133">Complete the sign-in flow</span></span>

<span data-ttu-id="e8e0d-134">当登录请求完成并重定向回页面时，它应执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="e8e0d-134">When the sign-in request completes and redirects back to your page, it should perform the following steps:</span></span>

1. <span data-ttu-id="e8e0d-135">生成安全代码。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-135">Generate a security code.</span></span> <span data-ttu-id="e8e0d-136"> (可以是随机数字。) 您需要在服务上缓存此代码，以及通过登录流获取的凭据 (如 OAuth 2.0 令牌) 。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-136">(This can be a random number.) You need to cache this code on your service, along with the credentials obtained through the sign-in flow (such as OAuth 2.0 tokens).</span></span>
2. <span data-ttu-id="e8e0d-137">调用 `microsoftTeams.authentication.notifySuccess` 并传递安全代码。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-137">Call `microsoftTeams.authentication.notifySuccess` and pass the security code.</span></span>

<span data-ttu-id="e8e0d-138">此时，窗口关闭，控件将传递给 Teams 客户端。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-138">At this point, the window closes and control is passed to the Teams client.</span></span> <span data-ttu-id="e8e0d-139">客户端现在可以重新发送原始用户查询以及属性中的安全 `state` 代码。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-139">The client now can reissue the original user query, along with the security code in the `state` property.</span></span> <span data-ttu-id="e8e0d-140">代码可以使用安全代码查找之前存储的凭据，以完成身份验证序列，然后完成用户请求。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-140">Your code can use the security code to look up the credentials stored earlier to complete the authentication sequence and then complete the user request.</span></span>

#### <a name="reissued-request-example"></a><span data-ttu-id="e8e0d-141">重新发送的请求示例</span><span class="sxs-lookup"><span data-stu-id="e8e0d-141">Reissued request example</span></span>

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

## <a name="code-sample"></a><span data-ttu-id="e8e0d-142">代码示例</span><span class="sxs-lookup"><span data-stu-id="e8e0d-142">Code sample</span></span>
|<span data-ttu-id="e8e0d-143">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="e8e0d-143">**Sample name**</span></span> | <span data-ttu-id="e8e0d-144">**说明**</span><span class="sxs-lookup"><span data-stu-id="e8e0d-144">**Description**</span></span> |<span data-ttu-id="e8e0d-145">**.NET**</span><span class="sxs-lookup"><span data-stu-id="e8e0d-145">**.NET**</span></span> | <span data-ttu-id="e8e0d-146">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="e8e0d-146">**Node.js**</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="e8e0d-147">邮件扩展 - 身份验证和配置</span><span class="sxs-lookup"><span data-stu-id="e8e0d-147">Messaging extensions - auth and config</span></span> | <span data-ttu-id="e8e0d-148">具有配置页面、接受搜索请求和在用户登录后返回结果的消息扩展。</span><span class="sxs-lookup"><span data-stu-id="e8e0d-148">A Messaging Extension that has a configuration page, accepts search requests, and returns results after the user has signed in.</span></span> |[<span data-ttu-id="e8e0d-149">View</span><span class="sxs-lookup"><span data-stu-id="e8e0d-149">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)|[<span data-ttu-id="e8e0d-150">View</span><span class="sxs-lookup"><span data-stu-id="e8e0d-150">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/blob/main/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config)| 

 
