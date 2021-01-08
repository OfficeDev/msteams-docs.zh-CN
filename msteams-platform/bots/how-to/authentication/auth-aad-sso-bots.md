---
title: 为机器人提供单一登录支持
description: 介绍如何获取用户令牌。 目前，机器人开发人员可以使用具有 OAuth 卡支持的登录卡或 azure 自动程序服务。
keywords: 令牌， 用户令牌， 自动程序 SSO 支持
ms.openlocfilehash: ee9dbee063acf90f5596fc95d002caf53f88a08a
ms.sourcegitcommit: 0a9e91c65d88512eda895c21371b3cd4051dca0d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/23/2020
ms.locfileid: "49729072"
---
# <a name="single-sign-on-sso-support-for-bots"></a>单一登录 (SSO) 自动程序支持

Azure AD (Azure Active Directory 中的单一登录身份验证) 通过静默刷新身份验证令牌来最大程度地减少用户输入其登录凭据的时间。 如果用户同意使用你的应用，则他们不需要在另一台设备上再次同意，并且将自动登录。 该流非常类似于 Teams [选项卡 SSO 支持]( ../../../tabs/how-to/authentication/auth-aad-sso.md)。 区别在于自动程序如何请求令牌和接收响应的协议。

OAuth 2.0 是 Azure Active Directory 和 Azure AD (和许多其他标识提供程序) 身份验证和授权的开放式标准。 基本了解 OAuth 2.0 是在 Teams 中处理身份验证的先决条件。

## <a name="bot-sso-at-runtime"></a>运行时自动程序 SSO

![运行时自动程序 SSO 图](../../../assets/images/bots/bots-sso-diagram.png)

1. 机器人使用包含该属性的 OAuthCard 发送邮件 `tokenExchangeResource` 。 它指示 Teams 获取自动程序应用程序的身份验证令牌。 用户在用户的所有活动终结点接收消息。

    > [!NOTE]
    >* 一个用户一次可以具有多个活动终结点。  
    >* 自动程序令牌从用户每个活动终结点接收。
    >* 单一登录支持当前需要在个人范围内安装应用。

2. 如果当前用户第一次使用自动程序应用程序， (如果需要同意) 或处理双重身份验证等 (身份验证请求) 。

3. Microsoft Teams 从 Azure AD 终结点为当前用户请求自动程序应用程序令牌。

4. Azure AD 将机器人应用程序令牌发送到 Teams 应用程序。

5. Microsoft Teams 将令牌作为调用活动返回的值对象的一部分（名称为登录/令牌Exchange）发送给机器人。
  
6. 令牌将在自动程序应用程序中进行分析，以提取所需信息，如用户的电子邮件地址。
  
## <a name="develop-a-single-sign-on-microsoft-teams-bot"></a>开发单一登录 Microsoft Teams 自动程序
  
开发 SSO Microsoft Teams 自动程序需要执行以下步骤：

1. [创建 Azure 免费帐户](#create-an-azure-account)
2. [更新 Teams 应用清单](#update-your-app-manifest)
3. [添加代码以请求和接收自动程序令牌](#request-a-bot-token)

### <a name="create-an-azure-account"></a>创建 Azure 帐户

此步骤类似于选项卡 [SSO 流](../../../tabs/how-to/authentication/auth-aad-sso.md)：

1. 获取 Teams 桌面、Web 或移动客户端的 [Azure AD](/graph/concepts/auth-register-app-v2) 应用程序 ID。
2. 指定应用程序对 Azure AD 终结点和（可选）Microsoft Graph 所需的权限。
3. [授予 Teams](/azure/active-directory/develop/v2-permissions-and-consent) 桌面、Web 和移动应用程序的权限。
4. 选择 **"添加范围"。**
5. 在打开的面板中，通过输入作为范围名称 `access_as_user` 添加 **客户端应用**。

    >[!NOTE]
    > 用于添加access_as_user应用的"access_as_user"作用域适用于"管理员和用户"。

    > [!IMPORTANT]
    > * 如果要生成独立自动程序，将应用程序 ID URI 设置为 `api://botid-{YourBotId}` 此处 **，YourBotId** 将引用 Azure AD 应用程序 ID。
    > * 如果要使用自动程序和选项卡生成应用，将应用程序 ID URI 设置为 `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。

### <a name="update-your-app-manifest"></a>更新应用清单

将新属性添加到 Microsoft Teams 清单：

**WebApplicationInfo** - 以下元素的父元素：

> [!div class="checklist"]
>
> * **id** - 应用程序的客户端 ID。 这是在向 Azure AD 注册应用程序时获取的应用程序 ID。
>* **resource** - 应用程序的域和子域。 这是相同的 URI (，包括) 步骤 6 中创建时注册 `api://` `scope` 的协议。 不应在资源 `access_as_user` 中包括路径。 此 URI 的域部分应匹配 Teams 应用程序清单的 URL 中使用的域，包括任何子域。

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

### <a name="request-a-bot-token"></a>请求自动程序令牌

获取令牌的请求是使用现有邮件架构 (普通 POST 消息) 。 它包含在 OAuthCard 的附件中。 OAuthCard 类的架构在 Microsoft [Bot 架构 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) 中定义，它非常类似于登录卡。 如果卡片上填充了属性，Teams 将对此请求视为无提示 `TokenExchangeResource` 令牌获取。 对于 Teams 频道，我们仅遵守 `Id` 唯一标识令牌请求的属性。

>[!NOTE]
> 自动程序 `OAuthPrompt` 框架或支持单一登录 `MultiProviderAuthDialog` (SSO) 身份验证。

如果这是用户第一次使用你的应用程序，并且需要用户同意，将显示一个对话框，以继续获得与下面类似的同意体验。 当用户 **选择"继续**"时，将发生两个不同的情况，具体取决于是否已定义自动程序以及 OAuthCard 上的登录按钮。

!["同意"对话框](../../../assets/images/bots/bots-consent-dialogbox.png)

如果自动程序定义登录按钮，则自动程序登录流的触发方式与从邮件流中的卡片按钮的登录流类似。 由开发人员决定请求用户同意哪些权限。 如果需要权限超出权限的令牌（例如，如果要交换图形资源的令牌），则建议采用 `openId` 此方法。

如果自动程序未在卡上提供登录按钮，它将触发用户对最低权限集的同意。 此令牌对于基本身份验证和获取用户的电子邮件地址非常有用。

**没有登录按钮的 C# 令牌请求**：

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

包含令牌的响应通过调用活动发送，该调用活动架构与其他人调用机器人今天接收的活动相同。 唯一的区别是调用名称、登录 **/令牌Exchange** 和值字段，该字段将包含 **ID** (获取令牌的初始请求的字符串) ，令牌字段 (字符串值，包括令牌) 。  请注意，如果用户有多个活动终结点，您可能会收到针对给定请求的多个响应。 由你使用令牌删除响应的重复数据。

**用于响应处理调用活动的 C# 代码**：

```csharp
protected override async Task<InvokeResponse> OnInvokeActivityAsync
  (ITurnContext<IInvokeActivity> turnContext, CancellationToken cancellationToken)
        {
            try
            {
                if (turnContext.Activity.Name == SignInConstants.TokenExchangeOperationName && turnContext.Activity.ChannelId == Channels.Msteams)
                {
                    await OnTokenResponseEventAsync(turnContext, cancellationToken);
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

`turnContext.activity.value`其类型为[TokenExchangeInvokeRequest，](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true)其中包含自动程序可以进一步使用的令牌。 出于性能原因，请安全地存储令牌并刷新它们。

### <a name="update-the-azure-portal-with-the-oauth-connection"></a>使用 OAuth 连接更新 Azure 门户

1. 在 Azure 门户中，导航回 **自动程序通道注册**。

2. 切换到"**设置"****边栏选项卡**，然后选择"OAuth 连接设置"部分下的"添加设置"。

    ![SSOBotHandle2 视图](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

3. 完成 **"连接设置"** 表单：

    > [!div class="checklist"]
    >
    > * 输入新连接设置的名称。 这将是在步骤 **5** 中的自动程序服务代码设置内引用的名称。
    > * 在"服务提供程序"下拉列表中，**选择 Azure Active Directory V2。**
    >* 输入 AAD 应用程序的客户端凭据。

    >[!NOTE]
    > **AAD** 应用程序中可能需要隐式授予。

    >* 对于令牌 Exchange URL，请使用 AAD 应用程序上一步中定义的作用域值。 令牌 Exchange URL 的存在向 SDK 指示此 AAD 应用程序已针对 SSO 进行配置。
    >* 指定"common"作为 **租户 ID。**
    >* 为 AAD 应用程序指定对下游 API 的权限时配置的所有作用域。 提供客户端 ID 和客户端密码后，令牌存储将用已定义的权限交换令牌，获取图形令牌。
    >* 选择“**保存**”。

    ![BotSSOBotConnection 设置视图](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-the-auth-sample"></a>更新身份验证示例

从团队 [身份验证示例开始](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)。

1. 更新 TeamsBot 以包括以下内容。 若要处理传入请求的 deduping，请参阅以下内容：

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
  
2. 更新 `appsettings.json` 以包括 `botId` 上面定义的 、 密码和连接名称。
3. 更新清单并确保 `token.botframework.com` 该清单位于有效域部分。
4. Zip the manifest with the profile images and install it in Teams.

#### <a name="additional-code-samples"></a>其他代码示例

* [使用 Bot Framework SDK 的 C# 示例](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)。

* [使用 Bot Framework SDK 删除](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682)令牌请求的 C# 示例。

* [没有使用 Bot Framework SDK 令牌存储的 C# 示例](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)。
