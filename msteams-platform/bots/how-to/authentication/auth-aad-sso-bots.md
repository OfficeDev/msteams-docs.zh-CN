---
title: 为机器人提供单一登录支持
description: 介绍如何获取用户令牌。 目前，机器人开发人员可以使用登录卡或具有 OAuth 卡支持的 azure 自动程序服务。
keywords: 令牌， 用户令牌， 自动程序 SSO 支持
ms.localizationpriority: medium
ms.topic: conceptual
ms.openlocfilehash: a3b150ee27eeb387c71191e74b6765dd5a93b148
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155369"
---
# <a name="single-sign-on-sso-support-for-bots"></a>单一登录 (SSO) 自动程序支持

AAD Azure Active Directory (中的单一登录) 以静默方式刷新身份验证令牌，最大程度地减少用户输入登录凭据所需的次数。 如果用户同意使用你的应用，他们无需在另一台设备上再次提供同意，可自动登录。 流类似于选项卡[SSO](../../../tabs/how-to/authentication/auth-aad-sso.md)Microsoft Teams流，但是，区别在于自动程序如何请求令牌和[接收响应的协议](#receive-the-bot-token)。 [](#request-a-bot-token)

>[!NOTE]
> OAuth 2.0 是 AAD 和许多其他标识提供程序使用的身份验证和授权的开放式标准。 对 OAuth 2.0 有基本的了解是在 Teams 中进行身份验证的先决条件。

## <a name="bot-sso-at-runtime"></a>运行时自动程序 SSO

![运行时自动程序 SSO 图](../../../assets/images/bots/bots-sso-diagram.png)

完成以下步骤，获取身份验证和自动程序应用程序令牌：

1. 机器人使用包含 `tokenExchangeResource` 属性的 OAuthCard 发送消息。 它会Teams自动程序应用程序获取身份验证令牌。 用户在所有活动用户终结点接收消息。

    > [!NOTE]
    >* 一个用户一次可以有多个活动终结点。
    >* 机器人令牌接收自每个活动用户终结点。
    >* 应用必须安装在个人作用域内才能支持 SSO。

1. 如果当前用户第一次使用自动程序应用程序，将显示请求提示，请求用户执行下列操作之一：
    * 如果需要，请提供同意。
    * 处理逐步处理的身份验证，例如双因素身份验证。

1. Teams当前用户的 AAD 终结点请求自动程序应用程序令牌。

1. AAD 将自动程序应用程序令牌发送到Teams应用程序。

1. Teams名称为 **sign-in/tokenExchange** 的调用活动返回的值对象，将令牌发送到自动程序。
  
1. 机器人应用程序中分析的令牌提供用户的电子邮件地址等所需信息。
  
## <a name="develop-an-sso-teams-bot"></a>开发 SSO Teams bot
  
完成以下步骤以开发 SSO 自动Teams程序：

1. [通过 AAD 门户注册应用](#register-your-app-through-the-aad-portal)。
1. [更新自动Teams的应用程序清单](#update-your-teams-application-manifest-for-your-bot)。
1. [添加代码以请求和接收自动程序令牌](#add-the-code-to-request-and-receive-a-bot-token)。

### <a name="register-your-app-through-the-aad-portal"></a>通过 AAD 门户注册应用

通过 AAD 门户注册应用的步骤与选项卡 [SSO 流类似](../../../tabs/how-to/authentication/auth-aad-sso.md)。 完成以下步骤以注册应用：

1. 在应用注册门户Azure Active Directory[新](https://go.microsoft.com/fwlink/?linkid=2083908)应用程序。
2. 选择 **"新建注册"。** 将显示 **"注册应用程序"** 页。
3. 在 **"注册应用程序"** 页中，输入以下值：
    1. 为 **应用输入** 名称。
    2. 选择" **支持的帐户类型"，** 选择"单个租户"或"多租户帐户类型"。

        > [!NOTE]
        >
        > 如果用户在同一租户中注册了 AAD 应用，并且他们在同一租户中提出身份验证请求，则系统不会要求用户同意并Teams。 但是，如果用户在不同的租户中注册了 AAD 应用，则必须同意这些权限。

    3. 选择 **“注册”**。
4. 在概述页面上，复制并保存应用程序 (**客户端) ID。** 稍后在更新应用程序清单时Teams它。
5. 在“**管理**”下，选择“**公开 API**”。 

   > [!IMPORTANT]
    > * 如果要构建独立自动程序，请输入应用程序 ID URI 作为 `api://botid-{YourBotId}` 。 此处 **YourBotId** 是 AAD 应用程序 ID。
    > * 如果要使用自动程序和选项卡生成应用，请输入应用程序 ID URI 作为 `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。

5. 选择应用程序对 AAD 终结点和（可选）Microsoft Graph。
6. [授予桌面](/azure/active-directory/develop/v2-permissions-and-consent)Teams Web 和移动应用程序的权限。
7. 选择“**添加作用域**”。
8. 在打开的面板中，输入 作为范围名称 `access_as_user` 添加 **客户端应用**。

    >[!NOTE]
    > 用于access_as_user客户端应用的"管理员和用户"作用域。
    >
    > 您必须了解以下重要限制：
    >
    > * 仅支持用户级别的 Microsoft Graph API 权限，如电子邮件、配置文件、offline_access和 OpenId。 如果需要访问其他 Microsoft Graph作用域（如 或 ），请参阅获取具有 Graph `User.Read` `Mail.Read` [权限的访问令牌](../../../tabs/how-to/authentication/auth-aad-sso.md#get-an-access-token-with-graph-permissions)。
    > * 应用程序的域名必须与为 AAD 应用程序注册的域名相同。
    > * 当前不支持每个应用多个域。
    > * 使用域 `azurewebsites.net` 的应用程序不受支持，因为它很常见，并且可能是安全风险。

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a>使用 OAuth 连接更新 Azure 门户

完成以下步骤以使用 OAuth 连接更新 Azure 门户：

1. 在 Azure 门户中，导航到 **"应用注册"。**

2. 转到 **API 权限**。 选择 **"添加**  >  **Microsoft Graph** 委派权限"，然后从 Microsoft Graph API  >  添加以下权限：
    * User.Read (默认启用) 
    * 电子邮件
    * offline_access
    * OpenId
    * 个人资料

3. 在 Azure 门户中，导航到 **"自动程序通道注册"。**

4. 选择 **设置** 窗格上的"设置"，**然后选择****"OAuth** 连接"部分下的"添加设置设置"。

    ![SSOBotHandle2 视图](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. 执行以下步骤以完成"新建 **连接设置"** 表单：

    >[!NOTE]
    > **AAD** 应用程序中可能需要隐式授权。

    1. 在" **新建连接** 设置 **"页中输入名称** 。 这是在运行时自动程序 SSO 步骤 *5* 中的自动程序服务代码设置 [内引用的名称](#bot-sso-at-runtime)。
    2. 从"**服务提供程序"** 下拉列表中，选择 **"Azure Active Directory v2"。**
    3. 输入客户端凭据，例如 AAD 应用程序的 **客户端** **ID** 和客户端密码。
    4. 对于 **令牌Exchange URL，** 请使用在更新自动程序的应用程序Teams [中定义的作用域值](#update-your-teams-application-manifest-for-your-bot)。 令牌Exchange URL 向 SDK 指示此 AAD 应用程序已针对 SSO 进行配置。
    5. 在" **租户 ID"** 框中，输入 *常用*。
    6. 添加 **为** AAD 应用程序指定下游 API 的权限时配置的所有作用域。 提供客户端 ID 和客户端密码后，令牌存储将令牌交换为具有定义权限的图形令牌。
    7. 选择“**保存**”。

    ![VuSSOBotConnection 设置视图](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a>更新自动Teams应用程序清单

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

* **id** - 应用程序的客户端 ID。 这是在向 AAD 注册应用程序时获取的应用程序 ID。 不要与多个应用共享此应用程序 ID Teams应用。 为使用 的每个应用程序清单创建新的 AAD 应用 `webApplicationInfo` 。
* **resource** - 应用程序的域和子域。 这是相同的 URI，包括在通过 AAD 门户注册应用时注册 `api://` `scope` [的协议](#register-your-app-through-the-aad-portal)。 不得在资源 `access_as_user` 中包括路径。 此 URI 的域部分必须与应用程序清单的 URL 中使用的域和子Teams匹配。

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a>添加代码以请求和接收自动程序令牌

#### <a name="request-a-bot-token"></a>请求自动程序令牌

获取令牌的请求是使用现有邮件架构的普通 POST 邮件请求。 它包含在 OAuthCard 的附件中。 OAuthCard 类的架构在 Microsoft [Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) 中定义，它类似于登录卡。 Teams在卡片上填充属性时，将此请求视为 `TokenExchangeResource` 无提示令牌获取。 对于Teams通道，仅处理唯一标识令牌请求 `Id` 的属性。

>[!NOTE]
> SSO `OAuthPrompt` 身份验证支持 `MultiProviderAuthDialog` Microsoft Bot Framework 或 。

如果用户第一次使用该应用程序并且需要用户同意，则显示以下对话框以继续获得同意体验：

!["同意"对话框](../../../assets/images/bots/bots-consent-dialogbox.png)

当用户选择“**继续**”时，将发生以下事件：

* 如果机器人定义了登录按钮，则自动程序登录流程的触发方式类似于来自邮件流中 OAuth 卡按钮的登录流。 开发人员必须决定哪些权限需要用户同意。 如果需要权限超过 的令牌，建议采用此方法 `openId` 。 例如，如果要交换图形资源的令牌。

* 如果自动程序未在 OAuth 卡上提供登录按钮，需要用户同意才能获得最低权限集。 此令牌可用于基本身份验证和获取用户的电子邮件地址。

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

通过调用活动发送包含令牌的响应，该活动架构与机器人今天接收的其他调用活动架构相同。 唯一的区别是调用名称、 **登录/令牌Exchange** 和 **值** 字段。 **值** 字段包含 **Id（** 获取令牌的初始请求的字符串）和 **令牌** 字段，字符串值（包括令牌）。

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

`turnContext.activity.value`为[TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true)类型，包含自动程序可以进一步使用的令牌。 出于性能原因，必须存储令牌并刷新它们。

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
3. 客户端在向用户显示 OAuth 卡之前截获该卡片，并检查其是否包含 `TokenExchangeResource` 属性。
4. 如果该属性存在，客户端会向 `TokenExchangeInvokeRequest` 自动程序发送 。 客户端必须具有用户的可交换令牌，该令牌必须是 Azure AD v2 令牌，并且其受众必须与 `TokenExchangeResource.Uri` 属性相同。 客户端通过以下代码向机器人发送调用活动：

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

5. 自动程序处理 `TokenExchangeInvokeRequest` 并返回 `TokenExchangeInvokeResponse` 回客户端。 客户端必须等待，直到收到 `TokenExchangeInvokeResponse` 。

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

6. 如果 `TokenExchangeInvokeResponse` 具有 `status` `200` 的 ，则客户端不会显示 OAuth 卡。 请参阅 [正常流图像](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)。 对于任何其他 `status` 或如果未收到 `TokenExchangeInvokeResponse` ，客户端会向用户显示 OAuth 卡。 请参阅 [回退流图像](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)。 这可确保 SSO 流在出现任何错误或未满足依赖关系（如用户同意）时恢复为正常 OAuthCard 流。


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
  
2. 更新以包含 、密码和在使用 OAuth 连接更新 Azure 门户 `appsettings.json` `botId` [中定义的连接名称](#update-the-azure-portal-with-the-oauth-connection)。
3. 更新清单并确保 `token.botframework.com` 它位于有效的域列表中。 有关详细信息，请参阅Teams[身份验证示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)。
4. Zip the manifest with the profile images and install it in Teams.

## <a name="code-sample"></a>代码示例
|**示例名称** | **说明** |**.NET** | 
|----------------|-----------------|--------------|
|自动程序框架 SDK | 使用自动程序框架 SDK 的示例。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)|
