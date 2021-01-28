---
title: 为机器人提供单一登录支持
description: 介绍如何获取用户令牌。 目前，机器人开发人员可以使用具有 OAuth 卡支持的登录卡或 azure 自动程序服务。
keywords: 令牌， 用户令牌， 自动程序 SSO 支持
ms.topic: conceptual
ms.openlocfilehash: 8669e00fcfcfb69844c4d63c9e7aa06b47567705
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014493"
---
# <a name="single-sign-on-sso-support-for-bots"></a>单一登录 (SSO) 自动程序支持

Azure Active Directory (AAD) 中的单一登录身份验证通过静默刷新身份验证令牌来最大程度地减少用户输入登录凭据所需的次数。 如果用户同意使用你的应用，他们无需在另一台设备上再次提供同意，可以自动登录。 流程类似于 Microsoft Teams[选项卡 SSO](../../../tabs/how-to/authentication/auth-aad-sso.md)支持流，但是，区别在于机器人如何请求令牌和[](#request-a-bot-token)[接收响应的协议](#receive-the-bot-token)。

>[!NOTE]
> OAuth 2.0 是 AAD 和许多其他标识提供程序使用的身份验证和授权的开放标准。 基本了解 OAuth 2.0 是在 Teams 中处理身份验证的先决条件。

## <a name="bot-sso-at-runtime"></a>运行时自动程序 SSO

![运行时自动程序 SSO 图](../../../assets/images/bots/bots-sso-diagram.png)

完成以下步骤，获取身份验证和自动程序应用程序令牌：

1. 机器人使用包含该属性的 OAuthCard 发送邮件 `tokenExchangeResource` 。 它指示 Teams 获取自动程序应用程序的身份验证令牌。 用户在所有活动用户终结点接收消息。

    > [!NOTE]
    >* 一个用户一次可以拥有多个活动终结点。
    >* 自动程序令牌从每个活动用户终结点接收。
    >* 应用必须安装在个人范围内，SSO 支持。

2. 如果当前用户第一次使用机器人应用程序，将显示请求提示，请求用户执行下列操作之一：
    * 如果需要，请提供同意。
    * 处理上一步身份验证，如双重身份验证。

3. Teams 从 AAD 终结点为当前用户请求自动程序应用程序令牌。

4. AAD 将机器人应用程序令牌发送到 Teams 应用程序。

5. Teams 使用名称登录 **/tokenExchange** 将令牌作为调用活动返回的值对象的一部分发送到机器人。
  
6. 自动程序应用程序中的已分析令牌提供所需信息，如用户的电子邮件地址。
  
## <a name="develop-an-sso-teams-bot"></a>开发 SSO Teams 机器人
  
完成以下步骤以开发 SSO Teams 自动程序：

1. [通过 AAD 门户注册应用](#register-your-app-through-the-aad-portal)。
2. [更新机器人的 Teams 应用程序清单](#update-your-teams-application-manifest-for-your-bot)。
3. [添加代码以请求和接收自动程序令牌](#add-the-code-to-request-and-receive-a-bot-token)。

### <a name="register-your-app-through-the-aad-portal"></a>通过 AAD 门户注册应用

通过 AAD 门户注册应用的步骤与选项卡 [SSO 流类似](../../../tabs/how-to/authentication/auth-aad-sso.md)。 完成以下步骤以注册应用：

1. 在 Azure Active [Directory - 应用注册门户中注册新](https://go.microsoft.com/fwlink/?linkid=2083908) 应用程序。
2. 选择 **"新建注册"。** 将显示 **"注册应用程序** "页。
3. 在 **"注册应用程序"** 页中，输入以下值：
    1. 输入 **应用** 的名称。
    2. 选择" **支持的帐户类型"，** 选择单个租户或多租户帐户类型。

        > [!NOTE]
        >
        > 如果用户在 Teams 中提出身份验证请求的同一租户中注册了 AAD 应用，则系统不会要求用户同意并授予访问令牌。 但是，如果 AAD 应用注册在不同的租户中，则用户必须同意这些权限。

    3. 选择 **“注册”**。
4. 在概述页上，复制并保存应用程序 (**客户端) ID。** 稍后在更新 Teams 应用程序清单时需要它。
5. 在“**管理**”下，选择“**公开 API**”。 

   > [!IMPORTANT]
    > * 如果要生成独立自动程序，请输入应用程序 ID URI 作为 `api://botid-{YourBotId}` 。 此处 **，YourBotId** 是 AAD 应用程序 ID。
    > * 如果要使用机器人和选项卡生成应用，请输入应用程序 ID URI `api://fully-qualified-domain-name.com/botid-{YourBotId}` 作为 。

5. 选择应用程序对 AAD 终结点和 Microsoft Graph 所需的权限（可选）。
6. [为](/azure/active-directory/develop/v2-permissions-and-consent) Teams 桌面、Web 和移动应用程序授予权限。
7. 选择 **"添加范围"。**
8. 在打开的面板中，通过输入作为范围名称 `access_as_user` 添加 **客户端应用**。

    >[!NOTE]
    > 用于添加access_as_user应用的"access_as_user"作用域适用于"管理员和用户"。
    >
    > 您必须了解以下重要限制：
    >
    > * 仅支持用户级别的 Microsoft Graph API 权限，如电子邮件、配置文件、offline_access和 OpenId。 如果你需要访问其他 Microsoft Graph 范围，例如 `User.Read` 或 `Mail.Read` ，请参阅 [建议的解决方法](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-microsoft-graph-scopes)。
    > * 应用程序的域名必须与为 AAD 应用程序注册的域名相同。
    > * 当前不支持每个应用多个域。
    > * 使用域 `azurewebsites.net` 的应用程序不受支持，因为它很常见，并且可能是一种安全风险。

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>使用 OAuth 连接更新 Azure 门户

完成以下步骤以使用 OAuth 连接更新 Azure 门户：

1. 在 Azure 门户中，导航到 **应用注册**。

2. 转到 **API 权限**。 选择 **"添加** Microsoft Graph 委派权限"权限，然后从 Microsoft Graph API 添加  >    >  以下权限：
    * User.Read (默认启用) 
    * email
    * offline_access
    * OpenId
    * 个人资料

3. 在 Azure 门户中，导航到 **自动程序通道注册**。

4. 选择 **左** 窗格上的"设置 **"，然后选择** "OAuth 连接设置"部分 **下的"添加** 设置"。

    ![SSOBotHandle2 视图](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. 执行以下步骤以完成"新建 **连接设置"** 表单：

    >[!NOTE]
    > **AAD** 应用程序中可能需要隐式授予。

    1. 在" **新建** 连接设置 **"页中输入名称** 。 这是在运行时自动程序 [SSO](#bot-sso-at-runtime)步骤 *5* 中的自动程序服务代码设置中引用的名称。
    2. 从 **"服务提供商"** 下拉列表中，选择 **Azure Active Directory v2。**
    3. 输入客户端凭据，如 AAD 应用程序的客户端 **ID** 和客户端密码。
    4. 对于 **令牌 Exchange URL，** 请使用在更新机器人的 [Teams 应用程序清单中定义的作用域值](#update-your-teams-application-manifest-for-your-bot)。 令牌 Exchange URL 向 SDK 指示此 AAD 应用程序已针对 SSO 进行配置。
    5. 在" **租户 ID"** 框中，输入 *common*。
    6. 为 AAD **应用程序** 指定对下游 API 的权限时配置的所有作用域。 提供客户端 ID 和客户端密码后，令牌存储将令牌交换为具有定义权限的图形令牌。
    7. 选择“**保存**”。

    ![BotSSOBotConnection 设置视图](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>更新机器人的 Teams 应用程序清单

如果应用程序包含独立自动程序，请使用以下代码将新属性添加到 Teams 应用程序清单：

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
如果应用程序包含自动程序和选项卡，则使用以下代码将新属性添加到 Teams 应用程序清单：

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** 是以下元素的父元素：

* **id** - 应用程序的客户端 ID。 这是在向 AAD 注册应用程序时获取的应用程序 ID。
* **resource** - 应用程序的域和子域。 这是相同的 URI，包括在通过 AAD 门户注册应用时注册 `api://` `scope` [的协议](#register-your-app-through-the-aad-portal)。 不得在资源 `access_as_user` 中包括路径。 此 URI 的域部分必须与 Teams 应用程序清单的 URL 中使用的域和子域匹配。

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>添加代码以请求和接收自动程序令牌

#### <a name="request-a-bot-token"></a>请求自动程序令牌

获取令牌的请求是使用现有邮件架构的普通 POST 消息请求。 它包含在 OAuthCard 的附件中。 OAuthCard 类的架构在 Microsoft [Bot 架构 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) 中定义，它类似于登录卡。 如果卡片上填充了属性，Teams 将此请求视为 `TokenExchangeResource` 无提示令牌获取。 对于 Teams 频道，仅 `Id` 处理唯一标识令牌请求的属性。

>[!NOTE]
> Microsoft Bot Framework `OAuthPrompt` 或 `MultiProviderAuthDialog` 支持 SSO 身份验证。

如果用户第一次使用该应用程序并且需要用户同意，则显示以下对话框以继续获得同意体验：

!["同意"对话框](../../../assets/images/bots/bots-consent-dialogbox.png)

当用户选择"继续 **"时**，将发生以下事件：

* 如果自动程序定义登录按钮，则自动程序登录流程的触发方式类似于消息流中的 OAuth 卡按钮的登录流。 开发人员必须决定需要征得用户同意的权限。 如果需要具有超出权限的令牌，建议采用此方法 `openId` 。 例如，如果要交换图形资源的令牌。

* 如果自动程序未在 OAuth 卡上提供登录按钮，需要用户同意，才能获得最低权限集。 此令牌对于基本身份验证和获取用户的电子邮件地址非常有用。

##### <a name="c-token-request-without-a-sign-in-button"></a>没有登录按钮的 C# 令牌请求

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

#### <a name="receive-the-bot-token"></a>接收自动程序令牌

包含令牌的响应通过调用活动发送，其架构与机器人当前接收的其他调用活动架构相同。 唯一的区别是调用名称、 **登录/tokenExchange** 和 **值** 字段。 值 **字段** 包含 **ID（** 获取令牌的初始请求的字符串）和 **令牌字段，** 一个包含令牌的字符串值。

>[!NOTE]
> 如果用户有多个活动终结点，您可能会收到给定请求的多个响应。 必须使用令牌删除响应。

##### <a name="c-code-to-handle-the-invoke-activity"></a>用于处理调用活动的 C# 代码

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

`turnContext.activity.value`其类型为[TokenExchangeInvokeRequest，](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true)其中包含自动程序可以进一步使用的令牌。 出于性能原因，必须存储令牌并刷新它们。

### <a name="update-the-auth-sample"></a>更新身份验证示例

打开 [Teams 身份验证示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) ，然后完成以下步骤以更新它：

1. 通过添加以下代码，更新 TeamsBot 以处理传入请求的 deduping：

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
  
2. 更新 `appsettings.json` 以包含 `botId` ，密码，以及使用 OAuth 连接更新 Azure 门户 [中定义的连接名称](#update-the-azure-portal-with-the-oauth-connection)。
3. 更新清单并确保 `token.botframework.com` 该清单位于有效的域列表中。 有关详细信息，请参阅 [Teams 身份验证示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)。
4. Zip the manifest with the profile images and install it in Teams.

#### <a name="additional-code-samples"></a>其他代码示例

* [使用 Bot Framework SDK 的 C# 示例](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)。
