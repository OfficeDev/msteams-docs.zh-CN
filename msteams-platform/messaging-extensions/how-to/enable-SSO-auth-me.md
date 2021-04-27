---
title: 对邮件扩展的 SSO 支持
author: KirtiPereira
description: 如何为邮件扩展启用 SSO 支持
localization_priority: Normal
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: f7dc689da3f0e3e06b8f9c68836b6449c2ae9120
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020700"
---
# <a name="single-sign-on-sso-support-for-messaging-extensions"></a><span data-ttu-id="f75f2-103">单一登录 (SSO) 邮件扩展支持</span><span class="sxs-lookup"><span data-stu-id="f75f2-103">Single sign-on (SSO) support for messaging extensions</span></span>
 
<span data-ttu-id="f75f2-104">单一登录支持现在可用于邮件扩展和链接取消点击。</span><span class="sxs-lookup"><span data-stu-id="f75f2-104">Single sign-on support is now available for messaging extensions and link unfurling.</span></span> <span data-ttu-id="f75f2-105">为消息传递扩展启用单一登录 (SSO) 会以静默方式刷新身份验证令牌，从而最大限度地减少为 Microsoft Teams 输入登录凭据所需的次数。</span><span class="sxs-lookup"><span data-stu-id="f75f2-105">Enabling Single sign-on (SSO) for messaging extensions silently refreshes the authentication token, which minimizes the number of times you need to enter your sign in credentials for Microsoft Teams.</span></span>

<span data-ttu-id="f75f2-106">本文档指导您如何启用 SSO 和存储身份验证令牌（如果需要）。</span><span class="sxs-lookup"><span data-stu-id="f75f2-106">This document guides you on how to enable the SSO and store your authentication token, if required.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f75f2-107">必备条件</span><span class="sxs-lookup"><span data-stu-id="f75f2-107">Prerequisites</span></span>

<span data-ttu-id="f75f2-108">为邮件扩展和链接展开启用 SSO 的先决条件如下所示：</span><span class="sxs-lookup"><span data-stu-id="f75f2-108">The prerequisite to enable SSO for messaging extensions and link unfurling are as follows:</span></span>
* <span data-ttu-id="f75f2-109">必须具有 [Azure](https://azure.microsoft.com/en-us/free/) 帐户。</span><span class="sxs-lookup"><span data-stu-id="f75f2-109">You must have an [Azure](https://azure.microsoft.com/en-us/free/) account.</span></span>
* <span data-ttu-id="f75f2-110">必须通过 AAD 门户配置应用，并更新机器人的 Teams 应用程序清单，如通过 AAD 门户注册应用 [所定义](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="f75f2-110">You must configure your app through the AAD portal, and update your Teams application manifest for your bot as defined in [register your app through the AAD portal](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal).</span></span>

> [!NOTE]
> <span data-ttu-id="f75f2-111">有关创建 Azure 帐户和更新应用清单的信息，请参阅单一登录 [ (SSO) 自动程序支持](../../bots/how-to/authentication/auth-aad-sso-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="f75f2-111">For more information on creating an Azure account and updating your app manifest, see [Single sign-on (SSO) support for bots](../../bots/how-to/authentication/auth-aad-sso-bots.md).</span></span>

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a><span data-ttu-id="f75f2-112">为消息传递扩展和链接取消展开启用 SSO</span><span class="sxs-lookup"><span data-stu-id="f75f2-112">Enable SSO for messaging extensions and link unfurling</span></span>

<span data-ttu-id="f75f2-113">完成先决条件后，您可以为消息传递扩展和链接取消点击启用 SSO。</span><span class="sxs-lookup"><span data-stu-id="f75f2-113">After the prerequisites are completed, you can enable SSO for messaging extensions and link unfurling.</span></span>

<span data-ttu-id="f75f2-114">**启用 SSO**</span><span class="sxs-lookup"><span data-stu-id="f75f2-114">**To enable SSO**</span></span>
1. <span data-ttu-id="f75f2-115">在 Azure 门户中更新机器人 [OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) 连接详细信息。</span><span class="sxs-lookup"><span data-stu-id="f75f2-115">Update your bots [OAuth connection](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) details in the Azure portal.</span></span>
2. <span data-ttu-id="f75f2-116">下载 [邮件扩展示例并按照](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) 向导提供的设置说明操作。</span><span class="sxs-lookup"><span data-stu-id="f75f2-116">Download the [messaging extensions sample](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) and follow the setup instructions provided by the wizard.</span></span>
   > [!NOTE]
   > <span data-ttu-id="f75f2-117">设置邮件扩展时，请使用自动程序 OAuth 连接。</span><span class="sxs-lookup"><span data-stu-id="f75f2-117">Use your bots OAuth connection when setting up your messaging extensions.</span></span>
3. <span data-ttu-id="f75f2-118">在 [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs)文件中，在 和 / 或 中将值从 *auth* 更新为 *silentAuth。* `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync`</span><span class="sxs-lookup"><span data-stu-id="f75f2-118">In the [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) file, update the value from *auth* to *silentAuth* in the `OnTeamsMessagingExtensionQueryAsync` and / or `OnTeamsAppBasedLinkQueryAsync`.</span></span>  

    > [!NOTE]
    > <span data-ttu-id="f75f2-119">我们不支持其他处理程序 `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` SSO，TeamsMessagingExtensionsSearchAuthConfigBot.cs 文件除外。</span><span class="sxs-lookup"><span data-stu-id="f75f2-119">We do not support other handlers SSO, except `OnTeamsMessagingExtensionQueryAsync` and `OnTeamsAppBasedLinkQueryAsync` from the TeamsMessagingExtensionsSearchAuthConfigBot.cs file.</span></span>
   
4. <span data-ttu-id="f75f2-120">在有效负载中的 处理程序中或在 中接收令牌，具体取决于你要为以下项启用 `OnTeamsMessagingExtensionQueryAsync` `turnContext.Activity.Value` `OnTeamsAppBasedLinkQueryAsync` SSO 的方案：</span><span class="sxs-lookup"><span data-stu-id="f75f2-120">You receive the token in `OnTeamsMessagingExtensionQueryAsync` handler in the `turnContext.Activity.Value` payload or in the `OnTeamsAppBasedLinkQueryAsync`, depending on which scenario you are enabling the SSO for:</span></span>

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    <span data-ttu-id="f75f2-121">如果使用的是 OAuth 连接，请向 TeamsMessagingExtensionsSearchAuthConfigBot.cs 文件添加以下代码，以更新或添加存储中的令牌：</span><span class="sxs-lookup"><span data-stu-id="f75f2-121">If you are using the OAuth connection, add the following code to the TeamsMessagingExtensionsSearchAuthConfigBot.cs file to update or add the token in the store:</span></span>
    
   ```C#
   protected override async Task<InvokeResponse> OnInvokeActivityAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
        {
            JObject valueObject = JObject.FromObject(turnContext.Activity.Value);
            if (valueObject["authentication"] != null)
            {
                JObject authenticationObject = JObject.FromObject(valueObject["authentication"]);
                if (authenticationObject["token"] != null)
                {
                    //If the token is NOT exchangeable, then return 412 to require user consent
                    if (await TokenIsExchangeable(turnContext, cancellationToken))
                    {
                        return await base.OnInvokeActivityAsync(turnContext, cancellationToken).ConfigureAwait(false);
                    }
                    else
                    {
                        var response = new InvokeResponse();
                        response.Status = 412;
                        return response;
                    }
                }
            }
            return await base.OnInvokeActivityAsync(turnContext, cancellationToken).ConfigureAwait(false);
        }
        private async Task<bool> TokenIsExchangeable(ITurnContext turnContext, CancellationToken cancellationToken)
        {
            TokenResponse tokenExchangeResponse = null;
            try
            {
                JObject valueObject = JObject.FromObject(turnContext.Activity.Value);
                var tokenExchangeRequest =
                ((JObject)valueObject["authentication"])?.ToObject<TokenExchangeInvokeRequest>();
                tokenExchangeResponse = await (turnContext.Adapter as IExtendedUserTokenProvider).ExchangeTokenAsync(
                 turnContext,
                 _connectionName,
                 turnContext.Activity.From.Id,
                 new TokenExchangeRequest
                 {
                     Token = tokenExchangeRequest.Token,
                 },
                 cancellationToken).ConfigureAwait(false);
            }
    #pragma warning disable CA1031 //Do not catch general exception types (ignoring, see comment below)
            catch
    #pragma warning restore CA1031 //Do not catch general exception types
            {
                //ignore exceptions
                //if token exchange failed for any reason, tokenExchangeResponse above remains null, and a failure invoke response is sent to the caller.
                //This ensures the caller knows that the invoke has failed.
            }
            if (tokenExchangeResponse == null || string.IsNullOrEmpty(tokenExchangeResponse.Token))
            {
                return false;
            }
            return true;
        }
    
    ```    

## <a name="see-also"></a><span data-ttu-id="f75f2-122">另请参阅</span><span class="sxs-lookup"><span data-stu-id="f75f2-122">See also</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f75f2-123">向邮件扩展添加身份验证</span><span class="sxs-lookup"><span data-stu-id="f75f2-123">Add authentication to your messaging extensions</span></span>](add-authentication.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f75f2-124">将 SSO 用于聊天机器人</span><span class="sxs-lookup"><span data-stu-id="f75f2-124">Use SSO for bots</span></span>](../../bots/how-to/authentication/auth-aad-sso-bots.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="f75f2-125">链接展开</span><span class="sxs-lookup"><span data-stu-id="f75f2-125">Link unfurling</span></span>](link-unfurling.md)

