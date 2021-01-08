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
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="7630e-105">单一登录 (SSO) 自动程序支持</span><span class="sxs-lookup"><span data-stu-id="7630e-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="7630e-106">Azure AD (Azure Active Directory 中的单一登录身份验证) 通过静默刷新身份验证令牌来最大程度地减少用户输入其登录凭据的时间。</span><span class="sxs-lookup"><span data-stu-id="7630e-106">Single sign-on authentication in Azure Active Directory (Azure AD) minimizes the number of times users need to enter their login credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="7630e-107">如果用户同意使用你的应用，则他们不需要在另一台设备上再次同意，并且将自动登录。</span><span class="sxs-lookup"><span data-stu-id="7630e-107">If users agree to use your app, they will not have to consent again on another device and will be signed in automatically.</span></span> <span data-ttu-id="7630e-108">该流非常类似于 Teams [选项卡 SSO 支持]( ../../../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="7630e-108">The flow is very similar to the [Teams tab SSO support]( ../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="7630e-109">区别在于自动程序如何请求令牌和接收响应的协议。</span><span class="sxs-lookup"><span data-stu-id="7630e-109">The difference is the protocol for how a bot requests tokens and receives responses.</span></span>

<span data-ttu-id="7630e-110">OAuth 2.0 是 Azure Active Directory 和 Azure AD (和许多其他标识提供程序) 身份验证和授权的开放式标准。</span><span class="sxs-lookup"><span data-stu-id="7630e-110">OAuth 2.0 is an open standard for authentication and authorization used by Azure Active Directory (Azure AD) and many other identity providers.</span></span> <span data-ttu-id="7630e-111">基本了解 OAuth 2.0 是在 Teams 中处理身份验证的先决条件。</span><span class="sxs-lookup"><span data-stu-id="7630e-111">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="7630e-112">运行时自动程序 SSO</span><span class="sxs-lookup"><span data-stu-id="7630e-112">Bot SSO at runtime</span></span>

![运行时自动程序 SSO 图](../../../assets/images/bots/bots-sso-diagram.png)

1. <span data-ttu-id="7630e-114">机器人使用包含该属性的 OAuthCard 发送邮件 `tokenExchangeResource` 。</span><span class="sxs-lookup"><span data-stu-id="7630e-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="7630e-115">它指示 Teams 获取自动程序应用程序的身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="7630e-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="7630e-116">用户在用户的所有活动终结点接收消息。</span><span class="sxs-lookup"><span data-stu-id="7630e-116">The user receives messages at all the active endpoints of the user.</span></span>

    > [!NOTE]
    >* <span data-ttu-id="7630e-117">一个用户一次可以具有多个活动终结点。</span><span class="sxs-lookup"><span data-stu-id="7630e-117">A user can have more than one active endpoint at a time.</span></span>  
    >* <span data-ttu-id="7630e-118">自动程序令牌从用户每个活动终结点接收。</span><span class="sxs-lookup"><span data-stu-id="7630e-118">The bot token is received from every active endpoint of the user.</span></span>
    >* <span data-ttu-id="7630e-119">单一登录支持当前需要在个人范围内安装应用。</span><span class="sxs-lookup"><span data-stu-id="7630e-119">Single sign-on support currently requires the app to be installed in personal scope.</span></span>

2. <span data-ttu-id="7630e-120">如果当前用户第一次使用自动程序应用程序， (如果需要同意) 或处理双重身份验证等 (身份验证请求) 。</span><span class="sxs-lookup"><span data-stu-id="7630e-120">If it is the first time the current user has used your bot application, there will be a request prompt to consent (if consent is required) or to handle step-up authentication (such as two-factor authentication).</span></span>

3. <span data-ttu-id="7630e-121">Microsoft Teams 从 Azure AD 终结点为当前用户请求自动程序应用程序令牌。</span><span class="sxs-lookup"><span data-stu-id="7630e-121">Microsoft Teams requests the bot application token from the Azure AD endpoint for the current user.</span></span>

4. <span data-ttu-id="7630e-122">Azure AD 将机器人应用程序令牌发送到 Teams 应用程序。</span><span class="sxs-lookup"><span data-stu-id="7630e-122">Azure AD sends the bot application token to the Teams application.</span></span>

5. <span data-ttu-id="7630e-123">Microsoft Teams 将令牌作为调用活动返回的值对象的一部分（名称为登录/令牌Exchange）发送给机器人。</span><span class="sxs-lookup"><span data-stu-id="7630e-123">Microsoft Teams sends the token to the bot as part of the value object returned by the invoke activity with the name sign-in/tokenExchange.</span></span>
  
6. <span data-ttu-id="7630e-124">令牌将在自动程序应用程序中进行分析，以提取所需信息，如用户的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="7630e-124">The token will be parsed in the bot application to extract the needed information, such as the user's email address.</span></span>
  
## <a name="develop-a-single-sign-on-microsoft-teams-bot"></a><span data-ttu-id="7630e-125">开发单一登录 Microsoft Teams 自动程序</span><span class="sxs-lookup"><span data-stu-id="7630e-125">Develop a Single sign-on Microsoft Teams bot</span></span>
  
<span data-ttu-id="7630e-126">开发 SSO Microsoft Teams 自动程序需要执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="7630e-126">The following steps are required to develop an SSO Microsoft Teams bot:</span></span>

1. [<span data-ttu-id="7630e-127">创建 Azure 免费帐户</span><span class="sxs-lookup"><span data-stu-id="7630e-127">Create an Azure free account</span></span>](#create-an-azure-account)
2. [<span data-ttu-id="7630e-128">更新 Teams 应用清单</span><span class="sxs-lookup"><span data-stu-id="7630e-128">Update your Teams app manifest</span></span>](#update-your-app-manifest)
3. [<span data-ttu-id="7630e-129">添加代码以请求和接收自动程序令牌</span><span class="sxs-lookup"><span data-stu-id="7630e-129">Add the code to request and receive the bot token</span></span>](#request-a-bot-token)

### <a name="create-an-azure-account"></a><span data-ttu-id="7630e-130">创建 Azure 帐户</span><span class="sxs-lookup"><span data-stu-id="7630e-130">Create an Azure account</span></span>

<span data-ttu-id="7630e-131">此步骤类似于选项卡 [SSO 流](../../../tabs/how-to/authentication/auth-aad-sso.md)：</span><span class="sxs-lookup"><span data-stu-id="7630e-131">This step is similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md):</span></span>

1. <span data-ttu-id="7630e-132">获取 Teams 桌面、Web 或移动客户端的 [Azure AD](/graph/concepts/auth-register-app-v2) 应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="7630e-132">Get your [Azure AD Application ID](/graph/concepts/auth-register-app-v2) for Teams desktop, web, or mobile client.</span></span>
2. <span data-ttu-id="7630e-133">指定应用程序对 Azure AD 终结点和（可选）Microsoft Graph 所需的权限。</span><span class="sxs-lookup"><span data-stu-id="7630e-133">Specify the permissions that your application needs for the Azure AD endpoint and, optionally, Microsoft Graph.</span></span>
3. <span data-ttu-id="7630e-134">[授予 Teams](/azure/active-directory/develop/v2-permissions-and-consent) 桌面、Web 和移动应用程序的权限。</span><span class="sxs-lookup"><span data-stu-id="7630e-134">[Grant permissions](/azure/active-directory/develop/v2-permissions-and-consent) for Teams desktop, web, and mobile applications.</span></span>
4. <span data-ttu-id="7630e-135">选择 **"添加范围"。**</span><span class="sxs-lookup"><span data-stu-id="7630e-135">Select **Add a scope**.</span></span>
5. <span data-ttu-id="7630e-136">在打开的面板中，通过输入作为范围名称 `access_as_user` 添加 **客户端应用**。</span><span class="sxs-lookup"><span data-stu-id="7630e-136">In the panel that opens, add a client app by entering `access_as_user` as the **Scope name**.</span></span>

    >[!NOTE]
    > <span data-ttu-id="7630e-137">用于添加access_as_user应用的"access_as_user"作用域适用于"管理员和用户"。</span><span class="sxs-lookup"><span data-stu-id="7630e-137">The "access_as_user" scope used to add a client app is for "Administrators and users".</span></span>

    > [!IMPORTANT]
    > * <span data-ttu-id="7630e-138">如果要生成独立自动程序，将应用程序 ID URI 设置为 `api://botid-{YourBotId}` 此处 **，YourBotId** 将引用 Azure AD 应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="7630e-138">If you are building a standalone bot, set the Application ID URI to `api://botid-{YourBotId}` Here, **YourBotId** refers to your Azure AD application ID.</span></span>
    > * <span data-ttu-id="7630e-139">如果要使用自动程序和选项卡生成应用，将应用程序 ID URI 设置为 `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。</span><span class="sxs-lookup"><span data-stu-id="7630e-139">If you are building an app with a bot and a tab, set the Application ID URI to `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

### <a name="update-your-app-manifest"></a><span data-ttu-id="7630e-140">更新应用清单</span><span class="sxs-lookup"><span data-stu-id="7630e-140">Update your app manifest</span></span>

<span data-ttu-id="7630e-141">将新属性添加到 Microsoft Teams 清单：</span><span class="sxs-lookup"><span data-stu-id="7630e-141">Add new properties to your Microsoft Teams manifest:</span></span>

<span data-ttu-id="7630e-142">**WebApplicationInfo** - 以下元素的父元素：</span><span class="sxs-lookup"><span data-stu-id="7630e-142">**WebApplicationInfo** - The parent of the following elements:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="7630e-143">**id** - 应用程序的客户端 ID。</span><span class="sxs-lookup"><span data-stu-id="7630e-143">**id** - The client ID of the application.</span></span> <span data-ttu-id="7630e-144">这是在向 Azure AD 注册应用程序时获取的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="7630e-144">This is the application ID that you obtained as part of registering the application with Azure AD.</span></span>
>* <span data-ttu-id="7630e-145">**resource** - 应用程序的域和子域。</span><span class="sxs-lookup"><span data-stu-id="7630e-145">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="7630e-146">这是相同的 URI (，包括) 步骤 6 中创建时注册 `api://` `scope` 的协议。</span><span class="sxs-lookup"><span data-stu-id="7630e-146">This is the same URI (including the `api://` protocol) that you registered when creating your `scope` in step 6 above.</span></span> <span data-ttu-id="7630e-147">不应在资源 `access_as_user` 中包括路径。</span><span class="sxs-lookup"><span data-stu-id="7630e-147">You shouldn't include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="7630e-148">此 URI 的域部分应匹配 Teams 应用程序清单的 URL 中使用的域，包括任何子域。</span><span class="sxs-lookup"><span data-stu-id="7630e-148">The domain part of this URI should match the domain, including any subdomains, used in the URLs of your Teams application manifest.</span></span>

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

### <a name="request-a-bot-token"></a><span data-ttu-id="7630e-149">请求自动程序令牌</span><span class="sxs-lookup"><span data-stu-id="7630e-149">Request a bot token</span></span>

<span data-ttu-id="7630e-150">获取令牌的请求是使用现有邮件架构 (普通 POST 消息) 。</span><span class="sxs-lookup"><span data-stu-id="7630e-150">The request to get the token is a normal POST message request (using the existing message schema).</span></span> <span data-ttu-id="7630e-151">它包含在 OAuthCard 的附件中。</span><span class="sxs-lookup"><span data-stu-id="7630e-151">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="7630e-152">OAuthCard 类的架构在 Microsoft [Bot 架构 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) 中定义，它非常类似于登录卡。</span><span class="sxs-lookup"><span data-stu-id="7630e-152">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is very similar to a sign-in card.</span></span> <span data-ttu-id="7630e-153">如果卡片上填充了属性，Teams 将对此请求视为无提示 `TokenExchangeResource` 令牌获取。</span><span class="sxs-lookup"><span data-stu-id="7630e-153">Teams will treat this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="7630e-154">对于 Teams 频道，我们仅遵守 `Id` 唯一标识令牌请求的属性。</span><span class="sxs-lookup"><span data-stu-id="7630e-154">For the Teams channel, we honor only the `Id` property, which uniquely identifies a token request.</span></span>

>[!NOTE]
> <span data-ttu-id="7630e-155">自动程序 `OAuthPrompt` 框架或支持单一登录 `MultiProviderAuthDialog` (SSO) 身份验证。</span><span class="sxs-lookup"><span data-stu-id="7630e-155">The Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for single sign-on (SSO) authentication.</span></span>

<span data-ttu-id="7630e-156">如果这是用户第一次使用你的应用程序，并且需要用户同意，将显示一个对话框，以继续获得与下面类似的同意体验。</span><span class="sxs-lookup"><span data-stu-id="7630e-156">If this is the first time the user is using your application and the user consent is required, the user will be shown a dialog to continue with the consent experience similar to the one below.</span></span> <span data-ttu-id="7630e-157">当用户 **选择"继续**"时，将发生两个不同的情况，具体取决于是否已定义自动程序以及 OAuthCard 上的登录按钮。</span><span class="sxs-lookup"><span data-stu-id="7630e-157">When the user selects **Continue**, two different things occur depending on whether the bot is defined or not and a sign-in button on the OAuthCard.</span></span>

!["同意"对话框](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="7630e-159">如果自动程序定义登录按钮，则自动程序登录流的触发方式与从邮件流中的卡片按钮的登录流类似。</span><span class="sxs-lookup"><span data-stu-id="7630e-159">If the bot defines a sign-in button, the sign-in flow for bots will be triggered similarly to the sign-in flow from a card button in a message stream.</span></span> <span data-ttu-id="7630e-160">由开发人员决定请求用户同意哪些权限。</span><span class="sxs-lookup"><span data-stu-id="7630e-160">It is up to the developer to decide which permissions to ask for the user to consent.</span></span> <span data-ttu-id="7630e-161">如果需要权限超出权限的令牌（例如，如果要交换图形资源的令牌），则建议采用 `openId` 此方法。</span><span class="sxs-lookup"><span data-stu-id="7630e-161">This approach is recommended if you need a token with permissions beyond `openId`, for example, if you want to exchange the token for graph resources.</span></span>

<span data-ttu-id="7630e-162">如果自动程序未在卡上提供登录按钮，它将触发用户对最低权限集的同意。</span><span class="sxs-lookup"><span data-stu-id="7630e-162">If the bot is not providing a sign-in button on the card, it triggers user consent for a minimal set of permissions.</span></span> <span data-ttu-id="7630e-163">此令牌对于基本身份验证和获取用户的电子邮件地址非常有用。</span><span class="sxs-lookup"><span data-stu-id="7630e-163">This token is useful for basic authentication and getting the user's email address.</span></span>

<span data-ttu-id="7630e-164">**没有登录按钮的 C# 令牌请求**：</span><span class="sxs-lookup"><span data-stu-id="7630e-164">**C# token request without a sign-in button**:</span></span>

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

#### <a name="receiving-the-token"></a><span data-ttu-id="7630e-165">接收令牌</span><span class="sxs-lookup"><span data-stu-id="7630e-165">Receiving the token</span></span>

<span data-ttu-id="7630e-166">包含令牌的响应通过调用活动发送，该调用活动架构与其他人调用机器人今天接收的活动相同。</span><span class="sxs-lookup"><span data-stu-id="7630e-166">The response with the token is sent through an invoke activity with the same schema as others invoke activities the bots receive today.</span></span> <span data-ttu-id="7630e-167">唯一的区别是调用名称、登录 **/令牌Exchange** 和值字段，该字段将包含 **ID** (获取令牌的初始请求的字符串) ，令牌字段 (字符串值，包括令牌) 。 </span><span class="sxs-lookup"><span data-stu-id="7630e-167">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field which will contain the **Id** (a string) of the initial request to get the token and the **token** field (a string value including the token).</span></span> <span data-ttu-id="7630e-168">请注意，如果用户有多个活动终结点，您可能会收到针对给定请求的多个响应。</span><span class="sxs-lookup"><span data-stu-id="7630e-168">Please note that you might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="7630e-169">由你使用令牌删除响应的重复数据。</span><span class="sxs-lookup"><span data-stu-id="7630e-169">It is up to you to deduplicate the responses with the token.</span></span>

<span data-ttu-id="7630e-170">**用于响应处理调用活动的 C# 代码**：</span><span class="sxs-lookup"><span data-stu-id="7630e-170">**C# code to respond to handle the invoke activity**:</span></span>

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

<span data-ttu-id="7630e-171">`turnContext.activity.value`其类型为[TokenExchangeInvokeRequest，](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true)其中包含自动程序可以进一步使用的令牌。</span><span class="sxs-lookup"><span data-stu-id="7630e-171">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="7630e-172">出于性能原因，请安全地存储令牌并刷新它们。</span><span class="sxs-lookup"><span data-stu-id="7630e-172">Store the tokens securely for performance reasons and refresh them.</span></span>

### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="7630e-173">使用 OAuth 连接更新 Azure 门户</span><span class="sxs-lookup"><span data-stu-id="7630e-173">Update the Azure portal with the OAuth connection</span></span>

1. <span data-ttu-id="7630e-174">在 Azure 门户中，导航回 **自动程序通道注册**。</span><span class="sxs-lookup"><span data-stu-id="7630e-174">In the Azure Portal, navigate back to the **Bot Channels Registration**.</span></span>

2. <span data-ttu-id="7630e-175">切换到"**设置"\*\*\*\*边栏选项卡**，然后选择"OAuth 连接设置"部分下的"添加设置"。</span><span class="sxs-lookup"><span data-stu-id="7630e-175">Switch to the **Settings** blade and choose **Add Setting** under the OAuth Connection Settings section.</span></span>

    ![SSOBotHandle2 视图](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

3. <span data-ttu-id="7630e-177">完成 **"连接设置"** 表单：</span><span class="sxs-lookup"><span data-stu-id="7630e-177">Complete the **Connection Setting** form:</span></span>

    > [!div class="checklist"]
    >
    > * <span data-ttu-id="7630e-178">输入新连接设置的名称。</span><span class="sxs-lookup"><span data-stu-id="7630e-178">Enter a name for your new Connection Setting.</span></span> <span data-ttu-id="7630e-179">这将是在步骤 **5** 中的自动程序服务代码设置内引用的名称。</span><span class="sxs-lookup"><span data-stu-id="7630e-179">This will be the name that gets referenced inside the settings of your bot service code in **step 5**.</span></span>
    > * <span data-ttu-id="7630e-180">在"服务提供程序"下拉列表中，**选择 Azure Active Directory V2。**</span><span class="sxs-lookup"><span data-stu-id="7630e-180">In the Service Provider dropdown, select **Azure Active Directory V2**.</span></span>
    >* <span data-ttu-id="7630e-181">输入 AAD 应用程序的客户端凭据。</span><span class="sxs-lookup"><span data-stu-id="7630e-181">Enter the client credentials for the AAD application.</span></span>

    >[!NOTE]
    > <span data-ttu-id="7630e-182">**AAD** 应用程序中可能需要隐式授予。</span><span class="sxs-lookup"><span data-stu-id="7630e-182">**Implicit grant** may be required in the AAD application.</span></span>

    >* <span data-ttu-id="7630e-183">对于令牌 Exchange URL，请使用 AAD 应用程序上一步中定义的作用域值。</span><span class="sxs-lookup"><span data-stu-id="7630e-183">For the Token Exchange URL, use the scope value defined in the previous step of your AAD application.</span></span> <span data-ttu-id="7630e-184">令牌 Exchange URL 的存在向 SDK 指示此 AAD 应用程序已针对 SSO 进行配置。</span><span class="sxs-lookup"><span data-stu-id="7630e-184">The presence of the Token Exchange URL is indicating to the SDK that this AAD application is configured for SSO.</span></span>
    >* <span data-ttu-id="7630e-185">指定"common"作为 **租户 ID。**</span><span class="sxs-lookup"><span data-stu-id="7630e-185">Specify "common" as the **Tenant ID**.</span></span>
    >* <span data-ttu-id="7630e-186">为 AAD 应用程序指定对下游 API 的权限时配置的所有作用域。</span><span class="sxs-lookup"><span data-stu-id="7630e-186">Add all the scopes configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="7630e-187">提供客户端 ID 和客户端密码后，令牌存储将用已定义的权限交换令牌，获取图形令牌。</span><span class="sxs-lookup"><span data-stu-id="7630e-187">With the client id and client secret provided, the token store will exchange the token for a graph token with defined permissions for you.</span></span>
    >* <span data-ttu-id="7630e-188">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="7630e-188">Select **Save**.</span></span>

    ![BotSSOBotConnection 设置视图](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-the-auth-sample"></a><span data-ttu-id="7630e-190">更新身份验证示例</span><span class="sxs-lookup"><span data-stu-id="7630e-190">Update the auth sample</span></span>

<span data-ttu-id="7630e-191">从团队 [身份验证示例开始](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)。</span><span class="sxs-lookup"><span data-stu-id="7630e-191">Start with the [teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>

1. <span data-ttu-id="7630e-192">更新 TeamsBot 以包括以下内容。</span><span class="sxs-lookup"><span data-stu-id="7630e-192">Update the TeamsBot to include the following.</span></span> <span data-ttu-id="7630e-193">若要处理传入请求的 deduping，请参阅以下内容：</span><span class="sxs-lookup"><span data-stu-id="7630e-193">To handle the deduping of the incoming request, see below:</span></span>

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
  
2. <span data-ttu-id="7630e-194">更新 `appsettings.json` 以包括 `botId` 上面定义的 、 密码和连接名称。</span><span class="sxs-lookup"><span data-stu-id="7630e-194">Update the `appsettings.json` to include the `botId`, password, and the connection name defined above.</span></span>
3. <span data-ttu-id="7630e-195">更新清单并确保 `token.botframework.com` 该清单位于有效域部分。</span><span class="sxs-lookup"><span data-stu-id="7630e-195">Update the manifest and ensure that `token.botframework.com` is in the valid domains section.</span></span>
4. <span data-ttu-id="7630e-196">Zip the manifest with the profile images and install it in Teams.</span><span class="sxs-lookup"><span data-stu-id="7630e-196">Zip the manifest with the profile images and install it in Teams.</span></span>

#### <a name="additional-code-samples"></a><span data-ttu-id="7630e-197">其他代码示例</span><span class="sxs-lookup"><span data-stu-id="7630e-197">Additional code samples</span></span>

* <span data-ttu-id="7630e-198">[使用 Bot Framework SDK 的 C# 示例](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)。</span><span class="sxs-lookup"><span data-stu-id="7630e-198">[C# sample using the Bot Framework SDK](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore).</span></span>

* <span data-ttu-id="7630e-199">[使用 Bot Framework SDK 删除](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682)令牌请求的 C# 示例。</span><span class="sxs-lookup"><span data-stu-id="7630e-199">[C# sample using the Bot Framework SDK to deduplicate the token request](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).</span></span>

* <span data-ttu-id="7630e-200">[没有使用 Bot Framework SDK 令牌存储的 C# 示例](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)。</span><span class="sxs-lookup"><span data-stu-id="7630e-200">[C# sample without using the Bot Framework SDK token store](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw).</span></span>
