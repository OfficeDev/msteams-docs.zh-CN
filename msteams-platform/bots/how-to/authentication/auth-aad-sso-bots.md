---
title: 为机器人提供单一登录支持
description: 介绍如何获取用户令牌。 目前，机器人开发人员可以将登录卡或 Azure 自动程序服务与 OAuth 卡支持一同使用。
keywords: 令牌， 用户令牌， 自动程序 SSO 支持， 权限， Microsoft Graph， Azure AD
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: 760c9f964298e120dfaf5cfadd199f5a7d02454f
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821596"
---
# <a name="single-sign-on-sso-support-for-bots"></a>单一登录 (SSO) 自动程序支持

Azure Active Directory中的单一登录身份验证以静默方式刷新身份验证令牌，以最大限度地减少用户输入登录凭据所需的次数。 如果用户同意使用你的应用，则当他们自动登录时，他们不必在另一台设备上再次提供同意。 选项卡和自动程序具有类似的 SSO 支持流。 但是[，机器人会请求令牌](#request-a-bot-token)[，并使用不同的](#receive-the-bot-token)协议接收响应。

>[!NOTE]
> OAuth 2.0 是一个开放标准，用于身份验证和授权，Azure AD和许多其他标识提供程序。 对 OAuth 2.0 有基本的了解是在 Teams 中进行身份验证的先决条件。

## <a name="bot-sso-at-runtime"></a>运行时自动程序 SSO

下图演示了自动程序中的 SSO 流：

![运行时自动程序 SSO 图](../../../assets/images/bots/bots-sso-diagram.png)

以下步骤可帮助你使用身份验证和自动程序应用程序令牌：

1. 自动程序向用户Teams包含获取自动程序应用程序的身份验证令牌的 OAuthCard`tokenExchangeResource`。 用户在所有活动用户终结点接收消息。

   > [!NOTE]
   >
   > * 一个用户一次可以有多个活动终结点。
   > * 机器人令牌接收自每个活动用户终结点。
   > * 应用必须安装在个人作用域内才能支持 SSO。


1. 如果当前用户第一次使用自动程序应用程序，则用户将显示请求提示以执行以下操作之一：
    * 请在必要时提供同意。
    * 处理逐步处理的身份验证，例如双因素身份验证。

1. Teams从当前用户的 Azure AD 终结点请求自动程序应用程序令牌。

1. Azure AD自动程序应用程序令牌发送到Teams应用程序。

1. Teams使用登录 **/令牌Exchange** 调用返回的值对象，将令牌发送到自动程序。
  
1. 机器人应用程序中分析的令牌提供用户的电子邮件地址等所需信息。
  
## <a name="develop-an-sso-teams-bot"></a>开发 SSO Teams自动程序
  
以下步骤将指导你开发 SSO Teams聊天机器人：

1. [通过应用门户Azure AD应用](#register-your-app-through-the-azure-ad-portal)。
1. [为自动Teams更新你的应用程序清单](#update-your-teams-application-manifest-for-your-bot)。
1. [添加代码以请求和接收自动程序令牌](#add-the-code-to-request-and-receive-a-bot-token)。

### <a name="register-your-app-through-the-azure-ad-portal"></a>通过应用门户Azure AD应用

通过应用门户注册Azure AD的步骤与选项卡 [SSO 流类似](../../../tabs/how-to/authentication/auth-aad-sso.md)。 以下步骤将指导你注册应用：

1. 在应用注册门户Azure Active Directory[注册新](https://go.microsoft.com/fwlink/?linkid=2083908)应用程序。

1. 选择“**新注册**”。 将显示 **注册应用程序** 页。

    ![新注册](~/assets/images/authentication/SSO-bots-auth/app-registration.png)

1. 在 **"注册应用程序"** 中，执行以下步骤：

   > [!NOTE]
   >
   > 如果用户在同一租户中注册 Azure AD 应用，并且他们在 Teams 中提出身份验证请求，则系统不会要求用户同意并授予访问Teams。 但是，如果用户在不同的租户中注册 Azure AD，用户必须同意这些权限。

    * 输入 **应用** 的名称。
    * 选择 **支持的帐户类型**，例如单个租户或多租户。
    * 选择“**注册**”。

    ![注册应用程序](~/assets/images/authentication/SSO-bots-auth/register-application.png)

1. 转到概述页面。
1. 复制应用程序客户端 **(ID) 值**。
1. 在 **"管理**"下，转到 **"公开 API"**

   > [!TIP]
   > 若要稍后更新应用清单，请保存 **应用程序 (客户端) ID** 值。

   > [!IMPORTANT]
   > * 如果要构建独立自动程序，请输入应用程序 ID URI 作为 `api://botid-{YourBotId}`。 此处 *YourBotId* 是Azure AD应用程序 ID。
   > * 如果要使用机器人和选项卡生成应用，请输入应用程序 ID URI 作为 `api://fully-qualified-domain-name.com/botid-{YourBotId}`。

1. 选择应用程序对 Azure AD 终结点和 Microsoft Graph 所需的权限。
1. [授予桌面](/azure/active-directory/develop/v2-permissions-and-consent)Teams Web 和移动应用程序的权限。
1. 选择“**添加作用域**”。
1. 在提示的面板中，输入 作为`access_as_user`**范围名称**。

   >[!NOTE]
   > 用于access_as_user客户端应用的"安全作用域"适用于"管理员和用户"。
   >
   > 您必须了解以下重要限制：
   >
   > * 仅支持用户级别的 Microsoft Graph API 权限，如电子邮件、配置文件、offline_access和 OpenId。 如果需要访问其他 Microsoft `User.Read` Graph作用域（如 或 `Mail.Read`），请参阅获取具有 Graph [权限的访问令牌](../../../tabs/how-to/authentication/auth-aad-sso.md#get-an-access-token-with-graph-permissions)。
   > * 应用程序的域名必须与为应用程序注册的域名Azure AD相同。
   > * 当前不支持每个应用多个域。
   > * 使用域的应用程序 `azurewebsites.net` 不受支持，因为它很常见，并且可能是安全风险。

1. In the **Who can consent？**， enter **Admins and users**.
1. 输入以下详细信息以使用适用于作用域的值配置管理员和用户同意 `access_as_user`提示。
    * **管理员显示名称**：Teams可以访问用户配置文件。
    * **管理员同意说明**：Teams 可以作为当前用户调用应用程序的 web API。
    * **用户显示名称**：Teams访问你的配置文件并代表你提出请求。
    * **用户同意** 描述：Teams你拥有相同权限调用此应用的 API。

    ![管理员和用户](~/assets/images/authentication/SSO-bots-auth/add-a-scope.png)

1. 确保状态设置为"已启用 **"**。

    ![State](~/assets/images/authentication/SSO-bots-auth/enabled-state.png)

1. 选择 **添加作用域** 保存详细信息。 显示的作用域名称的域 **部分** 必须自动匹配上一步中设置的应用程序 **ID** URI `/access_as_user` ，并追加到末尾 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`。

1. 在 **授权客户端应用程序中**，标识要针对应用的 Web 应用程序授权的应用程序。
1. 选择 **添加客户端应用程序**。

    ![客户端应用程序](~/assets/images/authentication/SSO-bots-auth/add-client-application.png)

1. 输入以下每个客户端 ID，然后选择在上一步中创建的授权范围：
    * 对于 Teams 移动或桌面应用程序，`1fec8e78-bce4-4aaf-ab1b-5451cc387264`。
    * 对于 Teams Web 应用程序，`5e3ce6c0-2b1f-4285-8d4b-75ee78787346`。

    ![客户端 ID](~/assets/images/authentication/SSO-bots-auth/add-client-id.png)

1. 转到" **身份验证"**。
1. 在 **"平台配置"** 中， **选择"添加平台"**。

    ![平台](~/assets/images/authentication/SSO-bots-auth/platform-configuration.png)

1. 选择“Web”

    ![配置平台](~/assets/images/authentication/SSO-bots-auth/configure-platform.png)

1. 输入 **应用的重定向 URI** 。

   >[!NOTE]
   > 此 URI 应为完全限定的域名。 它后跟发送身份验证响应的 API 路由。 如果正在关注任何 Teams 示例，则 URI 为 `https://token.botframework.com/.auth/web/redirect`。 有关详细信息，请参阅 [OAuth 2.0 授权代码流](/azure/active-directory/develop/v2-oauth2-auth-code-flow)。

    ![重定向 uris](~/assets/images/authentication/SSO-bots-auth/configure-web.png)

1. 添加必要的 **API 权限**。
    * 从 **左侧平面选择 API** 权限。
    * 选择 **"添加平台** "以添加你的应用在下游 API 中所需的任何用户委派权限，例如 User.Read。

1. 以下步骤将帮助您启用隐式授予：
    * 从 **左窗格中** 选择"身份验证"。
    * 选中 **"访问令牌** 和 **ID 令牌"** 复选框。
    
    ![授予流](~/assets/images/authentication/SSO-bots-auth/grant-flow.png)
    
    * 选择 **"保存** "保存更改。

#### <a name="update-manifest-in-microsoft-azure-portal"></a>更新门户中的Microsoft Azure清单

以下步骤将指导你在 Azure 门户中更新自动程序清单：

1. 从 **左窗格中** 选择清单。
1. 确保配置项设置为" **accessTokenAcceptedVersion"：2**。 如果不是，请更改其值到 **2**。

    ![更新清单](~/assets/images/bots/update-manifest.png)


   >[!NOTE]
   > 如果你已在应用中测试自动程序Teams，则必须从此应用注销，然后从 Teams。 然后再次登录以查看此更改。

1. 选择“**保存**”。

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>使用 OAuth 连接更新 Azure 门户

以下步骤将指导你使用 OAuth 连接更新 Azure 门户：

1. 在 Azure 门户中，转到 [**AzureBot**](https://ms.portal.azure.com/#create/Microsoft.AzureBot)
1. 转到左 **窗格** 上的"配置"。
1. 选择 **"添加 OAuth 连接设置**"。

    ![配置设置](~/assets/images/authentication/SSO-bots-auth/auth-setting2.png)

1. 以下步骤将指导您完成"新建 **连接设置"** 表单：

   >[!NOTE]
   > **在应用程序** 内可能需要隐式Azure AD授权。

    * 在 **"新建** 连接 **设置"页中输入"名称** "。

    >[!NOTE]
    > **"名称**"是指在运行时自动程序 SSO 的步骤 *5* 中 [自动程序服务代码的设置](#bot-sso-at-runtime)。

    * 从"**服务提供程序"** 下拉列表中，选择"Azure Active Directory **v2"**。
    * 输入客户端凭据，如客户端 **ID** 和客户端 **密码，Azure AD** 应用程序。
    * 对于 **令牌Exchange URL**，请使用更新自动程序Teams [应用程序清单中定义的作用域值](#update-your-teams-application-manifest-for-your-bot)。 令牌Exchange URL 向 SDK 指示Azure AD为 SSO 配置此令牌应用程序。
    * 在租户 **ID 中，** 输入 *common*。
    * 添加 **为应用程序** 指定下游 API 的权限时配置Azure AD范围。 提供客户端 ID 和客户端密码后，令牌存储将令牌交换为具有定义权限的图形令牌。
    * 选择“**保存**”。
    * 选择“**应用**”。
   
    ![连接设置](~/assets/images/authentication/Bot-connection-setting.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>为自动Teams更新你的应用程序清单

如果应用程序包含独立自动程序，则使用以下代码将新属性添加到Teams清单：

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
如果应用程序包含自动程序和选项卡，则使用以下代码将新属性添加到Teams清单：

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

**webApplicationInfo** 是以下元素的父元素：

* **id** - 应用程序的客户端 ID。 它是在向应用程序注册应用程序时获取的应用程序 ID Azure AD。 不要与多个应用共享此应用程序 ID Teams应用。 为使用 的每个Azure AD创建一个新的应用程序清单`webApplicationInfo`应用程序。
* **resource** - 应用程序的域和子域。 它是相同的 URI `api://` `scope`，包括在通过应用门户注册应用时注册Azure AD[协议](#register-your-app-through-the-azure-ad-portal)。 请勿在资源 `access_as_user` 中包括路径。 此 URI 的域部分必须与应用程序清单的 URL 中使用的域和子Teams匹配。

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>添加代码以请求和接收自动程序令牌

#### <a name="request-a-bot-token"></a>请求自动程序令牌

获取令牌的请求是使用现有邮件架构的普通 POST 邮件请求。 它包含在 OAuthCard 的附件中。 OAuthCard 类的架构在 [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) 中定义，它类似于登录卡。 Teams在卡片上`TokenExchangeResource`填充属性时，将此请求视为无提示令牌获取。 对于Teams通道`Id`，仅处理唯一标识令牌请求的属性。

>[!NOTE]
> `OAuthPrompt` SSO 身份验证支持 `MultiProviderAuthDialog` Microsoft Bot Framework 或 。

如果用户第一次使用该应用程序并且需要用户同意，则显示以下对话框以继续获得同意体验：

!["同意"对话框](~/assets/images/authentication/SSO-bots-auth/bot-consent-box.png)

当用户选择“**继续**”时，将发生以下事件：

* 如果机器人定义了登录按钮，则自动程序登录流将被激活，这类似于来自邮件流中 OAuth 卡按钮的登录流。 开发人员必须决定哪些权限需要用户同意。 如果需要权限超过 的令牌，建议采用此方法 `openId`。 例如，如果要交换图形资源的令牌。

* 如果机器人没有在 OAuth 卡片上提供登录按钮，则需要获得用户同意才能获得最小的权限集。 此令牌可用于基本身份验证和获取用户的电子邮件地址。

##### <a name="c-token-request-without-a-sign-in-button"></a>C#登录按钮创建令牌请求

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

通过调用活动发送包含令牌的响应，该活动架构与机器人今天接收的其他调用活动架构相同。 唯一的区别是调用名称、 **登录/令牌Exchange** 和 **值** 字段。 **值** 字段包含 **Id**、获取令牌的初始请求的字符串和 **令牌** 字段，包括令牌的字符串值。

>[!NOTE]
> 如果用户有多个活动终结点，您可能会收到对给定请求的多个响应。 必须使用令牌删除响应。

##### <a name="c-code-to-handle-the-invoke-activity"></a>C#代码来处理调用活动

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

`turnContext.activity.value`为 [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) 类型，包含自动程序可以进一步使用的令牌。 出于性能原因，必须存储令牌并刷新它们。

### <a name="token-exchange-failure"></a>令牌交换失败

如果令牌交换失败，请使用以下代码：

```json
{ 
    "status": "<response code>", 
    "body": 
    { 
        "id":"<unique Id>", 
        "connectionName": "<connection Name on the bot (from the OAuth card)>", 
        "failureDetail": "<failure reason if status code is not 200, null otherwise>" 
    } 
}
```

若要了解当令牌交换无法触发同意提示时自动程序执行哪些操作，请参阅以下步骤：

>[!NOTE]
> 当令牌交换失败时，自动程序无需执行任何用户操作。

1. 客户端与触发 OAuth 方案的机器人开始对话。
2. 机器人将 OAuth 卡发送回客户端。
3. 客户端在向用户显示 OAuth 卡之前截获该卡片，并检查其是否包含属性 `TokenExchangeResource` 。
4. 如果该属性存在，客户端会向 `TokenExchangeInvokeRequest` 自动程序发送 。 客户端必须具有用户的可交换令牌，该令牌必须是 Azure AD v2 令牌，并且其访问群体必须与 属性`TokenExchangeResource.Uri`相同。 客户端通过以下代码向机器人发送调用活动：

    ```json
    {
        "type": "Invoke",
        "name": "signin/tokenExchange",
        "value": 
        {
            "id": "<any unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "token": "<exchangeable token>"
        }
    }
    ```

5. 自动程序处理 `TokenExchangeInvokeRequest` 并返回 `TokenExchangeInvokeResponse` 回客户端。 客户端必须等待，直到收到 `TokenExchangeInvokeResponse`。

    ```json
    {
        "status": "<response code>",
        "body": 
        {
            "id":"<unique Id>",
            "connectionName": "<connection Name on the skill bot (from the OAuth card)>",
            "failureDetail": "<failure reason if status code is not 200, null otherwise>"
        }
    }
    ```

6. `TokenExchangeInvokeResponse`如果 具有 `status` `200`的 ，则客户端不会显示 OAuth 卡。 查看 [正常流图像](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)。 对于任何其他 `status` 或如果未 `TokenExchangeInvokeResponse` 收到 ，则客户端会向用户显示 OAuth 卡。 请参阅 [回退流图像](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)。 如果存在任何错误或未满足的依赖项（如用户同意），此活动可确保 SSO 流恢复为正常的 OAuthCard 流。


### <a name="update-the-auth-sample"></a>更新身份验证示例

打开[Teams身份验证示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)，然后完成以下步骤以更新它：

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
  
2. 更新 `appsettings.json` 以包含 `botId`、密码和在使用 [OAuth 连接更新 Azure 门户中定义的连接名称](#update-the-azure-portal-with-the-oauth-connection)。
3. 更新清单并确保它 `token.botframework.com` 位于有效的域列表中。 有关详细信息，请参阅Teams[身份验证示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)。
4. Zip the manifest with the profile images and install it in Teams.

## <a name="code-sample"></a>代码示例
|**示例名称** | **说明** |**.NET** | 
|----------------|-----------------|--------------|
|自动程序框架 SDK | 使用自动程序框架 SDK 的示例。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/46.teams-auth)|

## <a name="step-by-step-guide"></a>分步指南

按照 [分步指南](../../../sbs-bots-with-sso.yml)操作，该指南可帮助你创建启用了 SSO 身份验证的自动程序。
