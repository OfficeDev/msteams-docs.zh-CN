---
title: 对 bot 的单一登录支持
description: 介绍如何获取用户令牌。 目前，bot 开发人员可以在支持 OAuth 卡时使用 "登录卡" 或 "azure bot 服务"。
keywords: 令牌，用户令牌，针对 bot 的 SSO 支持
ms.openlocfilehash: 0b896f7e13847f529075b5562a6c3eb2542482bf
ms.sourcegitcommit: df9448681d2a81f1029aad5a5e1989cd438d1ae0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2020
ms.locfileid: "48877842"
---
# <a name="single-sign-on-sso-support-for-bots"></a>单一登录 (SSO) 对 bot 的支持

Azure Active Directory 中的单一登录身份验证 (Azure AD) 最大限度地减少用户需要通过静默方式刷新身份验证令牌来输入其登录凭据的次数。 如果用户同意使用您的应用程序，则无需再次在其他设备上同意，并将自动登录。 流与 " [团队" 选项卡的 SSO 支持]( ../../../tabs/how-to/authentication/auth-aad-sso.md)非常相似。 不同之处在于，机器人如何请求令牌和接收响应的协议。

OAuth 2.0 是一种开放标准，用于 Azure Active Directory (Azure AD) 和许多其他标识提供程序使用的身份验证和授权。 对 OAuth 2.0 的基本了解是在团队中使用身份验证的先决条件。

## <a name="bot-sso-at-runtime"></a>运行时的 Bot SSO

![运行时关系图中的 Bot SSO](../../../assets/images/bots/bots-sso-diagram.png)

1. 机器人发送包含属性的 OAuthCard 的邮件 `tokenExchangeResource` 。 它告诉团队获取机器人应用程序的身份验证令牌。 用户在用户的所有活动终结点上接收邮件。

> [!NOTE]
> ✔用户一次可以有一个以上的活动终结点。  
> ✔从用户的每个活动终结点接收 bot 令牌。
> ✔单一登录支持目前要求在个人作用域中安装应用程序。

2. 如果是当前用户第一次使用你的 bot 应用程序，则在需要同意的情况下，将会发出请求提示 () 或处理步骤验证 (如双重身份验证) ）。

3. Microsoft 团队从当前用户的 Azure AD 终结点请求 bot 应用程序令牌。

4. Azure AD 将机器人应用程序令牌发送给团队应用程序。

5. Microsoft 团队将令牌以名称登录/tokenExchange 的 invoke 活动返回的 value 对象的一部分发送到 bot。
  
6. 令牌将在 bot 应用程序中进行分析，以提取所需的信息，如用户的电子邮件地址。
  
## <a name="develop-an-single-sign-on-microsoft-teams-bot"></a>开发单一登录 Microsoft 团队 bot
  
以下步骤是开发 SSO Microsoft 团队 bot 所必需的：

1. [创建 Azure 免费帐户](#create-an-azure-account)
2. [更新团队应用程序清单](#update-your-app-manifest)
3. [添加代码以请求和接收 bot 令牌](#request-a-bot-token)

### <a name="create-an-azure-account"></a>创建 Azure 帐户

此步骤类似于 [选项卡 SSO 流](../../../tabs/how-to/authentication/auth-aad-sso.md) 流：

1. 获取 [AZURE AD 应用程序 ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)。
2. 指定应用程序需要的 Azure AD 终结点和 Microsoft Graph （可选）的权限。
3. [授予](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) 对团队桌面、web 和移动应用程序的权限。
4. 预授权团队通过选择 " **添加范围** " 按钮，并在打开的面板中，输入 `access_as_user` 作为 **作用域名称** 。

> [!IMPORTANT]
> * 如果要构建独立的 bot，请将应用程序 ID URI 设置为 `api://botid-{YourBotId}` 。
> * 如果要使用 bot 和选项卡生成应用程序，请将应用程序 ID URI 设置为 `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。

### <a name="update-your-app-manifest"></a>更新应用程序清单

将新属性添加到 Microsoft 团队清单：

**WebApplicationInfo** -以下元素的父元素：

> [!div class="checklist"]
>
> * **id** -应用程序的客户端 id。 这是您在向 Azure AD 注册应用程序的过程中获得的应用程序 ID。
>* **resource** -应用程序的域和子域。 此 URI (包括 `api://` 您在 `scope` 上面的步骤6中创建时注册的协议) 。 您不应 `access_as_user` 在资源中包含该路径。 此 URI 的域部分应与在团队应用程序清单的 Url 中使用的域（包括任何子域）相匹配。

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

### <a name="request-a-bot-token"></a>请求 bot 令牌

获取令牌的请求是使用现有邮件架构)  (正常的 POST 邮件请求。 它包含在 OAuthCard 的附件中。 OAuthCard 类的架构在 [Microsoft Bot 架构 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) 中定义，与登录卡非常相似。 如果在卡片上填充了该属性，则团队会将此请求视为无提示令牌获取 `TokenExchangeResource` 。 对于 "团队渠道"，我们仅接受 `Id` 唯一标识令牌请求的属性。

如果这是用户第一次使用您的应用程序，并且需要用户同意，则将显示一个对话框，以继续使用与下面类似的同意体验。 当用户选择 " **继续** " 时，将根据是否定义了 Bot 以及 OAuthCard 上的登录按钮，将发生两个不同的情况。

!["同意" 对话框](../../../assets/images/bots/bots-consent-dialogbox.png)

如果机器人定义了登录按钮，则 bot 的登录流将以类似于邮件流中的卡按钮的登录流的方式触发。 由开发人员决定要求用户同意哪些权限。 如果需要具有权限的令牌 `openId` （例如，如果要交换 graph 资源的令牌），则建议使用此方法。

如果 bot 未在卡片上提供登录按钮，则会触发用户对最少一组权限的同意。 此令牌对基本身份验证和获取用户电子邮件地址非常有用。

**不带登录按钮的 c # 令牌请求** ：

```csharp
var attachment = new Attachment
            {
                Content = new OAuthCard
                {
                    TokenExchangeResource = new TokenExchangeResource
                    {
                        Id = requestId
                    }
                },
                ContentType = OAuthCard.ContentType,
            };
            var activity = MessageFactory.Attachment(attachment);

            // NOTE: This activity needs to be sent in the 1:1 conversation between the bot and the user. 
            // If the bot supports group and channel scope, this code should be updated to send the request to the 1:1 chat. 

   await turnContext.SendActivityAsync(activity, cancellationToken);
```

#### <a name="receiving-the-token"></a>接收令牌

令牌的响应是通过具有相同架构的调用活动发送的，而是由其他人调用，因为它会立即接收到这些活动。 唯一的区别是调用名称、 **登录/tokenExchange** 和 **值** 字段，其中包含的 **Id** (最初请求获取令牌的字符串) 和 **令牌** 字段 (包含令牌) 的字符串值。 请注意，如果用户有多个活动终结点，则可能会收到针对给定请求的多个响应。 您可以使用令牌 deduplicate 响应。

**用于响应处理调用活动的 c # 代码** ：

```csharp
protected override async Task<InvokeResponse> OnInvokeActivity
  (ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
        {
            try
            {
                if (turnContext.Activity.Name == SignInConstants.TokenExchangeOperationName && turnContext.Activity.ChannelId == Channels.Msteams)
                {
                    await OnTokenResponse(turnContext, cancellationToken);
                    return new InvokeResponse() { Status = 200 };
                }
                else
                {
                    return await base.OnInvokeActivityAsync(turnContext, cancellationToken);
                }
            }
            catch (InvokeResponseException e)
            {
                return e.CreateInvokeResponse();
            }
        }
```

的 `turnContext.activity.value` 类型为 [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) ，包含可供你的 bot 继续使用的令牌。 出于性能原因，安全地存储标记并刷新它们。

### <a name="update-the-azure-portal-with-the-oauth-connection"></a>使用 OAuth 连接更新 Azure 门户

1. 在 Azure 门户中，导航回 **机器人通道注册** 。

2. 切换到 " **设置** " 边栏选项卡，然后选择 "OAuth 连接设置" 部分下的 " **添加设置** "。

![SSOBotHandle2 视图](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

3. 完成 " **连接设置** " 窗体：

> [!div class="checklist"]
>
> * 为新的连接设置输入一个名称。 这将是在 **步骤 5** 中的 bot 服务代码的设置中引用的名称。
> * 在 "服务提供商" 下拉列表中，选择 " **Azure Active Directory V2** "。
>* 输入 AAD 应用程序的客户端凭据。
>* 对于令牌交换 URL，请使用在 AAD 应用程序的上一步骤中定义的范围值。 令牌交换 URL 的存在指示为 SDK 配置此 AAD 应用程序的 SSO。
>* 将 "公用" 指定为 **租户 ID** 。
>* 在为 AAD 应用程序指定对下游 Api 的权限时，添加所有配置的作用域。 使用提供的客户端 id 和客户端密码，令牌存储将为您交换带有定义的权限的图形令牌的令牌。
>* 选择“ **保存** ”。

![VuSSOBotConnection 设置视图](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-the-auth-sample"></a>更新身份验证示例

从 " [团队" auth 示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)开始。

1. 更新 TeamsBot 以包含以下项。 若要处理传入请求的 deduping，请参阅以下内容：

```csharp
 protected override async Task OnSignInInvokeAsync(ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
        {
            await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
        }
    protected override async Task OnTokenResponseEventAsync(ITurnContext<IEventActivity> turnContext, CancellationToken cancellationToken)
        {
            await Dialog.RunAsync(turnContext, ConversationState.CreateProperty<DialogState>(nameof(DialogState)), cancellationToken);
        }
```
  
2. 更新 `appsettings.json` 以包含 `botId` 上面定义的、密码和连接名称。
3. 更新清单，并确保 `token.botframework.com` 在 "有效域" 部分中。
4. 使用配置文件图像对清单进行压缩，并将其安装在团队中。

#### <a name="additional-code-samples"></a>其他代码示例

* [使用 Bot 框架 SDK 的 c # 示例](https://microsoft-my.sharepoint-df.com/:u:/p/vul/ETZQfeTViDlCv-frjgTIincB7dvk2HOnma1TLvcoeGGIxg?e=uPq62c)。

* [C # 示例使用 Bot 框架 SDK deduplicate 令牌请求](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682)。

* [不使用 Bot 框架 SDK 令牌存储的 c # 示例](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)
