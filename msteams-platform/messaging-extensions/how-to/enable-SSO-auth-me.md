---
title: 对消息扩展的 SSO 支持
author: KirtiPereira
description: 了解如何使用代码示例为消息传递扩展启用 SSO 支持。
ms.localizationpriority: high
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 148e8c59acc520e7771ac23c38b4b17c43d4d74d
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111253"
---
# <a name="single-sign-on-support-for-message-extensions"></a>对消息扩展的单一登录支持

单一登录 (SSO) 支持现在可用于消息扩展和链接展开。 默认情况下，为消息扩展启用单一登录会刷新身份验证令牌，从而最大程度地减少需要输入 Microsoft Teams 登录凭据的次数。

本文档介绍如何在必要时启用 SSO 并存储身份验证令牌。

## <a name="prerequisites"></a>先决条件

为消息扩展和链接展开启用 SSO 的先决条件如下：

* 必须具有 [Azure](https://azure.microsoft.com/free/) 帐户。
* 必须通过 Azure AD 门户配置应用，并按照[通过 Azure AD 门户注册应用](../../bots/how-to/authentication/auth-aad-sso-bots.md#register-your-app-through-the-azure-ad-portal)中的定义更新 Teams 应用程序清单中的机器人。

> [!NOTE]
> 有关创建 Azure 帐户和更新应用清单的详细信息，请参阅[对机器人的单一登录 (SSO) 支持](../../bots/how-to/authentication/auth-aad-sso-bots.md)。

## <a name="enable-sso-for-message-extensions-and-link-unfurling"></a>为消息扩展和链接展开启用 SSO

完成先决条件后，可以为消息扩展和链接展开启用 SSO。

要启用 SSO：

1. 在 Microsoft Azure 门户中更新机器人 [OAuth 连接](../../bots/how-to/authentication/auth-aad-sso-bots.md#update-the-azure-portal-with-the-oauth-connection)详细信息。
2. 下载[消息扩展示例](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config)，并按照向导提供的设置说明操作。
   > [!NOTE]
   > 设置消息扩展时，请使用机器人 OAuth 连接。
3. 在 [TeamsMessagingExtensionsSearchAuthConfigBot.cs](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config/Bots/TeamsMessagingExtensionsSearchAuthConfigBot.cs) 文件中，在 `OnTeamsMessagingExtensionQueryAsync` 和/或 `OnTeamsAppBasedLinkQueryAsync` 中将值从 *auth* 更新为 *silentAuth*。  

    > [!NOTE]
    > 我们不支持其他处理程序 SSO，但 TeamsMessagingExtensionsSearchAuthConfigBot.cs 中的 `OnTeamsMessagingExtensionQueryAsync` 和 `OnTeamsAppBasedLinkQueryAsync` 文件除外。

4. 在 `turnContext.Activity.Value` 有效负载或 `OnTeamsAppBasedLinkQueryAsync` 的 `OnTeamsMessagingExtensionQueryAsync` 处理程序中接收令牌，具体取决于启用 SSO 的应用场景：

    ```json
    JObject valueObject=JObject.FromObject(turnContext.Activity.Value);
    if(valueObject["authentication"] !=null)
     {
        JObject authenticationObject=JObject.FromObject(valueObject["authentication"]);
        if(authenticationObject["token"] !=null)
     }
    
     ```
  
    如果使用 OAuth 连接，请将以下代码添加到 TeamsMessagingExtensionsSearchAuthConfigBot.cs 文件以更新或添加存储中的令牌：

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
                var userTokenClient = turnContext.TurnState.Get<UserTokenClient>();
                tokenExchangeResponse = await userTokenClient.ExchangeTokenAsync(
                                turnContext.Activity.From.Id,
                                 _connectionName,
                                 turnContext.Activity.ChannelId,
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

* [为消息扩展添加身份验证](add-authentication.md)
* [对机器人使用 SSO](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [链接展开](link-unfurling.md)
