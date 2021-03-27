---
title: 对邮件扩展的 SSO 支持
author: KirtiPereira
description: 如何为邮件扩展启用 SSO 支持
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: a5f75ef59a3d6fa3fe190b4dba4a1e5736a87562
ms.sourcegitcommit: 0206ed48c6a287d14aec3739540194a91766f0a3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/26/2021
ms.locfileid: "51378342"
---
# <a name="single-sign-on-sso-support-for-messaging-extensions"></a>单一登录 (SSO) 邮件扩展支持
 
单一登录支持现在可用于邮件扩展和链接取消点击。 为消息传递扩展启用单一登录 (SSO) 会以静默方式刷新身份验证令牌，从而最大限度地减少为 Microsoft Teams 输入登录凭据所需的次数。

本文档指导您如何启用 SSO 和存储身份验证令牌（如果需要）。

## <a name="prerequisites"></a>先决条件

为邮件扩展和链接展开启用 SSO 的先决条件如下所示：
* 必须具有 [Azure](https://azure.microsoft.com/en-us/free/) 帐户。
* 必须通过 AAD 门户配置应用，并更新机器人的 Teams 应用程序清单，如通过 AAD 门户注册应用 [所定义](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-aad-portal)。

> [!NOTE]
> 有关创建 Azure 帐户和更新应用清单的信息，请参阅单一登录 [ (SSO) 自动程序支持](../../bots/how-to/authentication/auth-aad-sso-bots.md)。

## <a name="enable-sso-for-messaging-extensions-and-link-unfurling"></a>为消息传递扩展和链接取消展开启用 SSO

完成先决条件后，您可以为消息传递扩展和链接取消点击启用 SSO。

**启用 SSO**
1. 在 Azure 门户中更新机器人 [OAuth](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection) 连接详细信息。
2. 下载 [邮件扩展示例并按照](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) 向导提供的设置说明操作。
   > [!NOTE]
   > 设置邮件扩展时，请使用自动程序 OAuth 连接。
3. 在 [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs)文件中，在 和 / 或 中将值从 *auth* 更新为 *silentAuth。* `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync`  

    > [!NOTE]
    > 我们不支持其他处理程序 `OnTeamsMessagingExtensionQueryAsync` `OnTeamsAppBasedLinkQueryAsync` SSO，TeamsMessagingExtensionsSearchAuthConfigBot.cs 文件除外。
   
4. 在有效负载中的 处理程序中或在 中接收令牌，具体取决于你要为以下项启用 `OnTeamsMessagingExtensionQueryAsync` `turnContext.Activity.Value` `OnTeamsAppBasedLinkQueryAsync` SSO 的方案：

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    如果使用的是 OAuth 连接，请向 TeamsMessagingExtensionsSearchAuthConfigBot.cs 文件添加以下代码，以更新或添加存储中的令牌：
    
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

## <a name="see-also"></a>另请参阅

> [!div class="nextstepaction"]
> [向邮件扩展添加身份验证](add-authentication.md)

> [!div class="nextstepaction"]
> [将 SSO 用于聊天机器人](../../bots/how-to/authentication/auth-aad-sso-bots.md)

> [!div class="nextstepaction"]
> [链接展开](link-unfurling.md)

