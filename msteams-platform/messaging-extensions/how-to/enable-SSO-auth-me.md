---
title: 对消息扩展的 SSO 支持
author: KirtiPereira
description: 使用 Azure AD 和代码示例在 Teams 消息扩展应用中启用单一登录 (SSO) 。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: surbhigupta
ms.openlocfilehash: 999094e1649008e6d0528c8ac44c21a3f5f2f7a4
ms.sourcegitcommit: 82c585d287d61924ce3a3bba3e9caeff35c9a27a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2022
ms.locfileid: "67586845"
---
# <a name="enable-sso-for-message-extensions"></a>为消息扩展启用 SSO

单一登录 (SSO) 支持现在可用于消息扩展和链接展开。默认情况下，为消息扩展启用单一登录会刷新身份验证令牌，从而最大程度地减少输入 Microsoft Teams 登录凭据所需的次数。

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

4. 在有效负载中或在处理程序中`turnContext.Activity.Value``OnTeamsAppBasedLinkQueryAsync`接收令牌`OnTeamsMessagingExtensionQueryAsync`，具体取决于要为以下情况启用 SSO 的方案：

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

## <a name="code-sample"></a>代码示例

本部分提供机器人身份验证 v3 SDK 示例。

| **示例名称** | **说明** | **.NET** | **Node.js** | **Python** |
|---------------|------------|------------|-------------|---------------|
| 机器人身份验证 | 此示例演示如何开始在适用于 Teams 的机器人中进行身份验证。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/46.teams-auth) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/46.teams-auth) |
| 选项卡、机器人和消息扩展 (ME) SSO | 此示例显示用于 Tab、Bot 和 ME 的 SSO - 搜索、操作、链接展开。 |  [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-sso/nodejs) | 不适用 |
|Tab、Bot 和 Message 扩展| 此示例演示如何使用 SSO 检查 Bot、Tab 和消息扩展中的身份验证 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-auth/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-complete-auth/nodejs) | NA |

## <a name="see-also"></a>另请参阅

* [为消息扩展添加身份验证](add-authentication.md)
* [对机器人使用 SSO](../../bots/how-to/authentication/auth-aad-sso-bots.md)
* [链接展开](link-unfurling.md)
