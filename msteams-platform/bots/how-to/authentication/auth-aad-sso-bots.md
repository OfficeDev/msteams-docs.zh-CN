---
title: 为机器人提供单一登录支持
description: 介绍如何获取用户令牌。 目前，机器人开发人员可以使用具有 OAuth 卡支持的登录卡或 azure 自动程序服务。
keywords: 令牌， 用户令牌， 自动程序 SSO 支持
ms.topic: conceptual
ms.openlocfilehash: 8537cf41cdd7218b9bf7618fccf0e1704ac6b815
ms.sourcegitcommit: 92fa912a51f295bb8a2dc1593a46ce103752dcdd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/21/2021
ms.locfileid: "49917582"
---
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="ce009-105">单一登录 (SSO) 自动程序支持</span><span class="sxs-lookup"><span data-stu-id="ce009-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="ce009-106">Azure Active Directory (AAD) 中的单一登录身份验证通过静默刷新身份验证令牌来最大程度地减少用户输入登录凭据所需的次数。</span><span class="sxs-lookup"><span data-stu-id="ce009-106">Single sign-on authentication in Azure Active Directory (AAD) minimizes the number of times users need to enter their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="ce009-107">如果用户同意使用你的应用，他们无需在另一台设备上再次提供同意，可以自动登录。</span><span class="sxs-lookup"><span data-stu-id="ce009-107">If users agree to use your app, they need not provide consent again on another device and can sign in automatically.</span></span> <span data-ttu-id="ce009-108">流程类似于 Microsoft Teams[选项卡 SSO](../../../tabs/how-to/authentication/auth-aad-sso.md)支持流，但是，区别在于机器人如何请求令牌和[](#request-a-bot-token)[接收响应的协议](#receive-the-bot-token)。</span><span class="sxs-lookup"><span data-stu-id="ce009-108">The flow is similar to that of [Microsoft Teams tab SSO support](../../../tabs/how-to/authentication/auth-aad-sso.md), however, the difference is in the protocol for how a bot [requests tokens](#request-a-bot-token) and [receives responses](#receive-the-bot-token).</span></span>

>[!NOTE]
> <span data-ttu-id="ce009-109">OAuth 2.0 是 AAD 和许多其他标识提供程序使用的身份验证和授权的开放标准。</span><span class="sxs-lookup"><span data-stu-id="ce009-109">OAuth 2.0 is an open standard for authentication and authorization used by AAD and many other identity providers.</span></span> <span data-ttu-id="ce009-110">基本了解 OAuth 2.0 是在 Teams 中处理身份验证的先决条件。</span><span class="sxs-lookup"><span data-stu-id="ce009-110">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="ce009-111">运行时自动程序 SSO</span><span class="sxs-lookup"><span data-stu-id="ce009-111">Bot SSO at runtime</span></span>

![运行时自动程序 SSO 图](../../../assets/images/bots/bots-sso-diagram.png)

<span data-ttu-id="ce009-113">完成以下步骤，获取身份验证和自动程序应用程序令牌：</span><span class="sxs-lookup"><span data-stu-id="ce009-113">Complete the following steps to get authentication and bot application tokens:</span></span>

1. <span data-ttu-id="ce009-114">机器人使用包含该属性的 OAuthCard 发送邮件 `tokenExchangeResource` 。</span><span class="sxs-lookup"><span data-stu-id="ce009-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="ce009-115">它指示 Teams 获取自动程序应用程序的身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="ce009-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="ce009-116">用户在所有活动用户终结点接收消息。</span><span class="sxs-lookup"><span data-stu-id="ce009-116">The user receives messages at all the active user endpoints.</span></span>

    > [!NOTE]
    >* <span data-ttu-id="ce009-117">一个用户一次可以拥有多个活动终结点。</span><span class="sxs-lookup"><span data-stu-id="ce009-117">A user can have more than one active endpoint at a time.</span></span>
    >* <span data-ttu-id="ce009-118">自动程序令牌从每个活动用户终结点接收。</span><span class="sxs-lookup"><span data-stu-id="ce009-118">The bot token is received from every active user endpoint.</span></span>
    >* <span data-ttu-id="ce009-119">应用必须安装在个人范围内，SSO 支持。</span><span class="sxs-lookup"><span data-stu-id="ce009-119">The app must be installed in personal scope for SSO support.</span></span>

2. <span data-ttu-id="ce009-120">如果当前用户第一次使用机器人应用程序，将显示请求提示，请求用户执行下列操作之一：</span><span class="sxs-lookup"><span data-stu-id="ce009-120">If the current user is using your bot application for the first time, a request prompt appears requesting the user to do one of the following:</span></span>
    * <span data-ttu-id="ce009-121">如果需要，请提供同意。</span><span class="sxs-lookup"><span data-stu-id="ce009-121">Provide consent, if required.</span></span>
    * <span data-ttu-id="ce009-122">处理上一步身份验证，如双重身份验证。</span><span class="sxs-lookup"><span data-stu-id="ce009-122">Handle step-up authentication, such as two-factor authentication.</span></span>

3. <span data-ttu-id="ce009-123">Teams 从 AAD 终结点为当前用户请求自动程序应用程序令牌。</span><span class="sxs-lookup"><span data-stu-id="ce009-123">Teams requests the bot application token from the AAD endpoint for the current user.</span></span>

4. <span data-ttu-id="ce009-124">AAD 将机器人应用程序令牌发送到 Teams 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ce009-124">AAD sends the bot application token to the Teams application.</span></span>

5. <span data-ttu-id="ce009-125">Teams 使用名称登录 **/tokenExchange** 将令牌作为调用活动返回的值对象的一部分发送到机器人。</span><span class="sxs-lookup"><span data-stu-id="ce009-125">Teams sends the token to the bot as part of the value object returned by the invoke activity with the name **sign-in/tokenExchange**.</span></span>
  
6. <span data-ttu-id="ce009-126">自动程序应用程序中的已分析令牌提供所需信息，如用户的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="ce009-126">The parsed token in the bot application provides the required information, such as the user's email address.</span></span>
  
## <a name="develop-an-sso-teams-bot"></a><span data-ttu-id="ce009-127">开发 SSO Teams 机器人</span><span class="sxs-lookup"><span data-stu-id="ce009-127">Develop an SSO Teams bot</span></span>
  
<span data-ttu-id="ce009-128">完成以下步骤以开发 SSO Teams 自动程序：</span><span class="sxs-lookup"><span data-stu-id="ce009-128">Complete the following steps to develop an SSO Teams bot:</span></span>

1. <span data-ttu-id="ce009-129">[通过 AAD 门户注册应用](#register-your-app-through-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="ce009-129">[Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span>
2. <span data-ttu-id="ce009-130">[更新机器人的 Teams 应用程序清单](#update-your-teams-application-manifest-for-your-bot)。</span><span class="sxs-lookup"><span data-stu-id="ce009-130">[Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span>
3. <span data-ttu-id="ce009-131">[添加代码以请求和接收自动程序令牌](#add-the-code-to-request-and-receive-a-bot-token)。</span><span class="sxs-lookup"><span data-stu-id="ce009-131">[Add the code to request and receive a bot token](#add-the-code-to-request-and-receive-a-bot-token).</span></span>

### <a name="register-your-app-through-the-aad-portal"></a><span data-ttu-id="ce009-132">通过 AAD 门户注册应用</span><span class="sxs-lookup"><span data-stu-id="ce009-132">Register your app through the AAD portal</span></span>

<span data-ttu-id="ce009-133">通过 AAD 门户注册应用的步骤类似于选项卡 [SSO 流](../../../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="ce009-133">The steps to register your app through the AAD portal are similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="ce009-134">完成以下步骤以注册应用：</span><span class="sxs-lookup"><span data-stu-id="ce009-134">Complete the following steps to register your app:</span></span>

1. <span data-ttu-id="ce009-135">在 Azure Active [Directory - 应用注册门户中注册新](https://go.microsoft.com/fwlink/?linkid=2083908) 应用程序。</span><span class="sxs-lookup"><span data-stu-id="ce009-135">Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
2. <span data-ttu-id="ce009-136">选择 **"新建注册"。**</span><span class="sxs-lookup"><span data-stu-id="ce009-136">Select **New Registration**.</span></span> <span data-ttu-id="ce009-137">将显示 **"注册应用程序** "页。</span><span class="sxs-lookup"><span data-stu-id="ce009-137">The **Register an application** page appears.</span></span>
3. <span data-ttu-id="ce009-138">在 **"注册应用程序"** 页中，输入以下值：</span><span class="sxs-lookup"><span data-stu-id="ce009-138">In the **Register an application** page, enter the following values:</span></span>
    1. <span data-ttu-id="ce009-139">输入 **应用** 的名称。</span><span class="sxs-lookup"><span data-stu-id="ce009-139">Enter a **Name** for your app.</span></span>
    2. <span data-ttu-id="ce009-140">选择" **支持的帐户类型"，** 选择单个租户或多租户帐户类型。</span><span class="sxs-lookup"><span data-stu-id="ce009-140">Choose the **Supported account types**, select single tenant or multitenant account type.</span></span>

        > [!NOTE]
        >
        > <span data-ttu-id="ce009-141">如果用户在 Teams 中提出身份验证请求的同一租户中注册了 AAD 应用，则系统不会要求用户同意并授予访问令牌。</span><span class="sxs-lookup"><span data-stu-id="ce009-141">The users are not asked for consent and are granted access tokens right away, if the AAD app is registered in the same tenant where they are making an authentication request in Teams.</span></span> <span data-ttu-id="ce009-142">但是，如果 AAD 应用注册在不同的租户中，则用户必须同意这些权限。</span><span class="sxs-lookup"><span data-stu-id="ce009-142">However, the users must provide consent to the permissions, if the AAD app is registered in a different tenant.</span></span>

    3. <span data-ttu-id="ce009-143">选择 **“注册”**。</span><span class="sxs-lookup"><span data-stu-id="ce009-143">Choose **Register**.</span></span>
4. <span data-ttu-id="ce009-144">在概述页上，复制并保存应用程序 (**客户端) ID。**</span><span class="sxs-lookup"><span data-stu-id="ce009-144">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="ce009-145">稍后在更新 Teams 应用程序清单时需要它。</span><span class="sxs-lookup"><span data-stu-id="ce009-145">You need it later when updating your Teams application manifest.</span></span>
5. <span data-ttu-id="ce009-146">在“**管理**”下，选择“**公开 API**”。</span><span class="sxs-lookup"><span data-stu-id="ce009-146">Under **Manage**, select **Expose an API**.</span></span> 

   > [!IMPORTANT]
    > * <span data-ttu-id="ce009-147">如果要生成独立自动程序，请输入应用程序 ID URI 作为 `api://botid-{YourBotId}` 。</span><span class="sxs-lookup"><span data-stu-id="ce009-147">If you are building a standalone bot, enter the Application ID URI as `api://botid-{YourBotId}`.</span></span> <span data-ttu-id="ce009-148">此处 **，YourBotId** 是 AAD 应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="ce009-148">Here **YourBotId** is your AAD application ID.</span></span>
    > * <span data-ttu-id="ce009-149">如果要使用机器人和选项卡生成应用，请输入应用程序 ID URI `api://fully-qualified-domain-name.com/botid-{YourBotId}` 作为 。</span><span class="sxs-lookup"><span data-stu-id="ce009-149">If you are building an app with a bot and a tab, enter the Application ID URI as `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

5. <span data-ttu-id="ce009-150">选择应用程序对 AAD 终结点和 Microsoft Graph 所需的权限（可选）。</span><span class="sxs-lookup"><span data-stu-id="ce009-150">Select the permissions that your application needs for the AAD endpoint and, optionally, for Microsoft Graph.</span></span>
6. <span data-ttu-id="ce009-151">[授予 Teams](/azure/active-directory/develop/v2-permissions-and-consent) 桌面、Web 和移动应用程序的权限。</span><span class="sxs-lookup"><span data-stu-id="ce009-151">[Grant permissions](/azure/active-directory/develop/v2-permissions-and-consent) for Teams desktop, web, and mobile applications.</span></span>
7. <span data-ttu-id="ce009-152">选择 **"添加范围"。**</span><span class="sxs-lookup"><span data-stu-id="ce009-152">Select **Add a scope**.</span></span>
8. <span data-ttu-id="ce009-153">在打开的面板中，通过输入作为范围名称 `access_as_user` 添加 **客户端应用**。</span><span class="sxs-lookup"><span data-stu-id="ce009-153">In the panel that opens, add a client app by entering `access_as_user` as the **Scope name**.</span></span>

    >[!NOTE]
    > <span data-ttu-id="ce009-154">用于添加access_as_user应用的"access_as_user"作用域适用于"管理员和用户"。</span><span class="sxs-lookup"><span data-stu-id="ce009-154">The "access_as_user" scope used to add a client app is for "Administrators and users".</span></span>
    >
    > <span data-ttu-id="ce009-155">您必须了解以下重要限制：</span><span class="sxs-lookup"><span data-stu-id="ce009-155">You must be aware of the following important restrictions:</span></span>
    >
    > * <span data-ttu-id="ce009-156">仅支持用户级别的 Microsoft Graph API 权限，如电子邮件、配置文件、offline_access和 OpenId。</span><span class="sxs-lookup"><span data-stu-id="ce009-156">Only user-level Microsoft Graph API permissions, such as email, profile, offline_access, and OpenId are supported.</span></span> <span data-ttu-id="ce009-157">如果你需要访问其他 Microsoft Graph 范围，例如 `User.Read` 或 `Mail.Read` ，请参阅 [建议的解决方法](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-microsoft-graph-scopes)。</span><span class="sxs-lookup"><span data-stu-id="ce009-157">If you need access to other Microsoft Graph scopes, such as `User.Read` or `Mail.Read`, see [recommended workaround](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-microsoft-graph-scopes).</span></span>
    > * <span data-ttu-id="ce009-158">应用程序的域名必须与为 AAD 应用程序注册的域名相同。</span><span class="sxs-lookup"><span data-stu-id="ce009-158">Your application's domain name must be same as the domain name that you have registered for your AAD application.</span></span>
    > * <span data-ttu-id="ce009-159">当前不支持每个应用多个域。</span><span class="sxs-lookup"><span data-stu-id="ce009-159">Multiple domains per app are currently not supported.</span></span>
    > * <span data-ttu-id="ce009-160">使用域 `azurewebsites.net` 的应用程序不受支持，因为它很常见，并且可能是一种安全风险。</span><span class="sxs-lookup"><span data-stu-id="ce009-160">Applications that use the `azurewebsites.net` domain are not supported because it is common and may be a security risk.</span></span>

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="ce009-161">使用 OAuth 连接更新 Azure 门户</span><span class="sxs-lookup"><span data-stu-id="ce009-161">Update the Azure portal with the OAuth connection</span></span>

<span data-ttu-id="ce009-162">完成以下步骤以使用 OAuth 连接更新 Azure 门户：</span><span class="sxs-lookup"><span data-stu-id="ce009-162">Complete the following steps to update the Azure portal with the OAuth connection:</span></span>

1. <span data-ttu-id="ce009-163">在 Azure 门户中，导航到 **自动程序通道注册**。</span><span class="sxs-lookup"><span data-stu-id="ce009-163">In the Azure Portal, navigate to **Bot Channels Registration**.</span></span>

2. <span data-ttu-id="ce009-164">转到 **API 权限**。</span><span class="sxs-lookup"><span data-stu-id="ce009-164">Go to **API Permissions**.</span></span> <span data-ttu-id="ce009-165">选择 **"添加** Microsoft Graph 委派权限"权限，然后从 Microsoft Graph API 添加  >    >  以下权限：</span><span class="sxs-lookup"><span data-stu-id="ce009-165">Select **Add a permission** > **Microsoft Graph** > **Delegated permissions**, then add the following permissions from Microsoft Graph API:</span></span>
    * <span data-ttu-id="ce009-166">User.Read (默认启用) </span><span class="sxs-lookup"><span data-stu-id="ce009-166">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="ce009-167">email</span><span class="sxs-lookup"><span data-stu-id="ce009-167">email</span></span>
    * <span data-ttu-id="ce009-168">offline_access</span><span class="sxs-lookup"><span data-stu-id="ce009-168">offline_access</span></span>
    * <span data-ttu-id="ce009-169">OpenId</span><span class="sxs-lookup"><span data-stu-id="ce009-169">OpenId</span></span>
    * <span data-ttu-id="ce009-170">个人资料</span><span class="sxs-lookup"><span data-stu-id="ce009-170">profile</span></span>

3. <span data-ttu-id="ce009-171">选择 **左** 窗格上的"设置 **"，然后选择** "OAuth 连接设置"部分 **下的"添加** 设置"。</span><span class="sxs-lookup"><span data-stu-id="ce009-171">Select **Settings** on the left pane and choose **Add Setting** under the **OAuth Connection Settings** section.</span></span>

    ![SSOBotHandle2 视图](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

4. <span data-ttu-id="ce009-173">执行以下步骤以完成"新建 **连接设置"** 表单：</span><span class="sxs-lookup"><span data-stu-id="ce009-173">Perform the following steps to complete the **New Connection Setting** form:</span></span>

    >[!NOTE]
    > <span data-ttu-id="ce009-174">**AAD** 应用程序中可能需要隐式授予。</span><span class="sxs-lookup"><span data-stu-id="ce009-174">**Implicit grant** may be required in the AAD application.</span></span>

    1. <span data-ttu-id="ce009-175">在" **新建** 连接设置 **"页中输入名称** 。</span><span class="sxs-lookup"><span data-stu-id="ce009-175">Enter a **Name** in the **New Connection Setting** page.</span></span> <span data-ttu-id="ce009-176">这是在运行时自动程序 [SSO](#bot-sso-at-runtime)步骤 *5* 中的自动程序服务代码设置中引用的名称。</span><span class="sxs-lookup"><span data-stu-id="ce009-176">This is the name that is referred to inside the settings of your bot service code in *step 5* of [Bot SSO at runtime](#bot-sso-at-runtime).</span></span>
    2. <span data-ttu-id="ce009-177">从 **"服务提供商"** 下拉列表中，选择 **Azure Active Directory v2。**</span><span class="sxs-lookup"><span data-stu-id="ce009-177">From the **Service Provider** drop-down, select **Azure Active Directory v2**.</span></span>
    3. <span data-ttu-id="ce009-178">输入客户端凭据，如 AAD 应用程序的客户端 **ID** 和客户端密码。</span><span class="sxs-lookup"><span data-stu-id="ce009-178">Enter the client credentials, such as **Client id** and **Client secret** for the AAD application.</span></span>
    4. <span data-ttu-id="ce009-179">对于 **令牌 Exchange URL，** 请使用在更新机器人的 [Teams 应用程序清单中定义的作用域值](#update-your-teams-application-manifest-for-your-bot)。</span><span class="sxs-lookup"><span data-stu-id="ce009-179">For the **Token Exchange URL**, use the scope value defined in [Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span> <span data-ttu-id="ce009-180">令牌 Exchange URL 向 SDK 指示此 AAD 应用程序已针对 SSO 进行配置。</span><span class="sxs-lookup"><span data-stu-id="ce009-180">The Token Exchange URL indicates to the SDK that this AAD application is configured for SSO.</span></span>
    5. <span data-ttu-id="ce009-181">在" **租户 ID"** 框中，输入 *common*。</span><span class="sxs-lookup"><span data-stu-id="ce009-181">In the **Tenant ID** box, enter *common*.</span></span>
    6. <span data-ttu-id="ce009-182">为 AAD **应用程序** 指定对下游 API 的权限时配置的所有作用域。</span><span class="sxs-lookup"><span data-stu-id="ce009-182">Add all the **Scopes** configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="ce009-183">提供客户端 ID 和客户端密码后，令牌存储将令牌交换为具有定义权限的图形令牌。</span><span class="sxs-lookup"><span data-stu-id="ce009-183">With the Client id and Client secret provided, the token store exchanges the token for a graph token with defined permissions.</span></span>
    7. <span data-ttu-id="ce009-184">选择 **“保存”**。</span><span class="sxs-lookup"><span data-stu-id="ce009-184">Select **Save**.</span></span>

    ![BotSSOBotConnection 设置视图](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a><span data-ttu-id="ce009-186">更新机器人的 Teams 应用程序清单</span><span class="sxs-lookup"><span data-stu-id="ce009-186">Update your Teams application manifest for your bot</span></span>

<span data-ttu-id="ce009-187">如果应用程序包含独立自动程序，请使用以下代码将新属性添加到 Teams 应用程序清单：</span><span class="sxs-lookup"><span data-stu-id="ce009-187">If the application contains a standalone bot, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
<span data-ttu-id="ce009-188">如果应用程序包含自动程序和选项卡，则使用以下代码将新属性添加到 Teams 应用程序清单：</span><span class="sxs-lookup"><span data-stu-id="ce009-188">If the application contains a bot and a tab, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

<span data-ttu-id="ce009-189">**webApplicationInfo** 是以下元素的父元素：</span><span class="sxs-lookup"><span data-stu-id="ce009-189">**webApplicationInfo** is the parent of the following elements:</span></span>

* <span data-ttu-id="ce009-190">**id** - 应用程序的客户端 ID。</span><span class="sxs-lookup"><span data-stu-id="ce009-190">**id** - The client ID of the application.</span></span> <span data-ttu-id="ce009-191">这是在向 AAD 注册应用程序时获取的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="ce009-191">This is the application ID that you obtained as part of registering the application with AAD.</span></span>
* <span data-ttu-id="ce009-192">**resource** - 应用程序的域和子域。</span><span class="sxs-lookup"><span data-stu-id="ce009-192">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="ce009-193">这是相同的 URI，包括在通过 AAD 门户注册应用时注册 `api://` `scope` [的协议](#register-your-app-through-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="ce009-193">This is the same URI, including the `api://` protocol that you registered when creating your `scope` in [Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span> <span data-ttu-id="ce009-194">不得在资源 `access_as_user` 中包括路径。</span><span class="sxs-lookup"><span data-stu-id="ce009-194">You must not include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="ce009-195">此 URI 的域部分必须与 Teams 应用程序清单的 URL 中使用的域和子域匹配。</span><span class="sxs-lookup"><span data-stu-id="ce009-195">The domain part of this URI must match the domain and subdomains used in the URLs of your Teams application manifest.</span></span>

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a><span data-ttu-id="ce009-196">添加代码以请求和接收自动程序令牌</span><span class="sxs-lookup"><span data-stu-id="ce009-196">Add the code to request and receive a bot token</span></span>

#### <a name="request-a-bot-token"></a><span data-ttu-id="ce009-197">请求自动程序令牌</span><span class="sxs-lookup"><span data-stu-id="ce009-197">Request a bot token</span></span>

<span data-ttu-id="ce009-198">获取令牌的请求是使用现有邮件架构的普通 POST 消息请求。</span><span class="sxs-lookup"><span data-stu-id="ce009-198">The request to get the token is a normal POST message request using the existing message schema.</span></span> <span data-ttu-id="ce009-199">它包含在 OAuthCard 的附件中。</span><span class="sxs-lookup"><span data-stu-id="ce009-199">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="ce009-200">OAuthCard 类的架构在 Microsoft [Bot 架构 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) 中定义，它类似于登录卡。</span><span class="sxs-lookup"><span data-stu-id="ce009-200">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is similar to a sign-in card.</span></span> <span data-ttu-id="ce009-201">如果卡片上填充了属性，Teams 将此请求视为 `TokenExchangeResource` 无提示令牌获取。</span><span class="sxs-lookup"><span data-stu-id="ce009-201">Teams treats this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="ce009-202">对于 Teams 频道，仅会采用唯一 `Id` 标识令牌请求的属性。</span><span class="sxs-lookup"><span data-stu-id="ce009-202">For the Teams channel, only the `Id` property, which uniquely identifies a token request, is honored.</span></span>

>[!NOTE]
> <span data-ttu-id="ce009-203">Microsoft Bot Framework `OAuthPrompt` 或 `MultiProviderAuthDialog` 支持 SSO 身份验证。</span><span class="sxs-lookup"><span data-stu-id="ce009-203">The Microsoft Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for SSO authentication.</span></span>

<span data-ttu-id="ce009-204">如果用户第一次使用该应用程序并且需要用户同意，则显示以下对话框以继续获得同意体验：</span><span class="sxs-lookup"><span data-stu-id="ce009-204">If the user is using the application for the first time and user consent is required, the following dialog box appears to continue with the consent experience:</span></span>

!["同意"对话框](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="ce009-206">当用户选择"继续 **"时**，将发生以下事件：</span><span class="sxs-lookup"><span data-stu-id="ce009-206">When the user selects **Continue**, the following events occur:</span></span>

* <span data-ttu-id="ce009-207">如果自动程序定义登录按钮，则自动程序登录流程的触发方式类似于消息流中的 OAuth 卡按钮的登录流。</span><span class="sxs-lookup"><span data-stu-id="ce009-207">If the bot defines a sign-in button, the sign in flow for bots is triggered similar to the sign in flow from an OAuth card button in a message stream.</span></span> <span data-ttu-id="ce009-208">开发人员必须决定需要征得用户同意的权限。</span><span class="sxs-lookup"><span data-stu-id="ce009-208">The developer must decide which permissions require user's consent.</span></span> <span data-ttu-id="ce009-209">如果需要具有超出权限的令牌，建议采用此方法 `openId` 。</span><span class="sxs-lookup"><span data-stu-id="ce009-209">This approach is recommended if you require a token with permissions beyond `openId`.</span></span> <span data-ttu-id="ce009-210">例如，如果你想要交换图形资源的令牌。</span><span class="sxs-lookup"><span data-stu-id="ce009-210">For example, if you want to exchange the token for graph resources.</span></span>

* <span data-ttu-id="ce009-211">如果自动程序未在 OAuth 卡上提供登录按钮，需要用户同意，才能获得最低权限集。</span><span class="sxs-lookup"><span data-stu-id="ce009-211">If the bot is not providing a sign-in button on the OAuth card, user consent is required for a minimal set of permissions.</span></span> <span data-ttu-id="ce009-212">此令牌对于基本身份验证和获取用户的电子邮件地址非常有用。</span><span class="sxs-lookup"><span data-stu-id="ce009-212">This token is useful for basic authentication and to get the user's email address.</span></span>

##### <a name="c-token-request-without-a-sign-in-button"></a><span data-ttu-id="ce009-213">没有登录按钮的 C# 令牌请求</span><span class="sxs-lookup"><span data-stu-id="ce009-213">C# token request without a sign-in button</span></span>

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

#### <a name="receive-the-bot-token"></a><span data-ttu-id="ce009-214">接收机器人令牌</span><span class="sxs-lookup"><span data-stu-id="ce009-214">Receive the bot token</span></span>

<span data-ttu-id="ce009-215">通过调用活动发送包含令牌的响应，该调用活动与机器人当前接收的其他调用活动架构相同。</span><span class="sxs-lookup"><span data-stu-id="ce009-215">The response with the token is sent through an invoke activity with the same schema as other invoke activities that the bots receive today.</span></span> <span data-ttu-id="ce009-216">唯一的区别是调用名称、 **登录/tokenExchange** 和 **值** 字段。</span><span class="sxs-lookup"><span data-stu-id="ce009-216">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field.</span></span> <span data-ttu-id="ce009-217">值 **字段** 包含 **ID（** 获取令牌的初始请求的字符串）和 **令牌字段，** 一个包含令牌的字符串值。</span><span class="sxs-lookup"><span data-stu-id="ce009-217">The **value** field contains the **Id**, a string of the initial request to get the token and the **token** field, a string value including the token.</span></span>

>[!NOTE]
> <span data-ttu-id="ce009-218">如果用户有多个活动终结点，您可能会收到给定请求的多个响应。</span><span class="sxs-lookup"><span data-stu-id="ce009-218">You might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="ce009-219">必须使用令牌删除响应。</span><span class="sxs-lookup"><span data-stu-id="ce009-219">You must deduplicate the responses with the token.</span></span>

##### <a name="c-code-to-handle-the-invoke-activity"></a><span data-ttu-id="ce009-220">用于处理调用活动的 C# 代码</span><span class="sxs-lookup"><span data-stu-id="ce009-220">C# code to handle the invoke activity</span></span>

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

<span data-ttu-id="ce009-221">`turnContext.activity.value`其类型为[TokenExchangeInvokeRequest，](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true)其中包含自动程序可以进一步使用的令牌。</span><span class="sxs-lookup"><span data-stu-id="ce009-221">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="ce009-222">出于性能原因，必须存储令牌并刷新它们。</span><span class="sxs-lookup"><span data-stu-id="ce009-222">You must store the tokens for performance reasons and refresh them.</span></span>

### <a name="update-the-auth-sample"></a><span data-ttu-id="ce009-223">更新身份验证示例</span><span class="sxs-lookup"><span data-stu-id="ce009-223">Update the auth sample</span></span>

<span data-ttu-id="ce009-224">打开 [Teams 身份验证示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) ，然后完成以下步骤以更新它：</span><span class="sxs-lookup"><span data-stu-id="ce009-224">Open [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) and then complete the following steps to update it:</span></span>

1. <span data-ttu-id="ce009-225">通过添加以下代码，更新 TeamsBot 以处理传入请求的 deduping：</span><span class="sxs-lookup"><span data-stu-id="ce009-225">Update the TeamsBot to handle the deduping of the incoming request by including the following code:</span></span>

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
  
2. <span data-ttu-id="ce009-226">更新 `appsettings.json` 以包含 `botId` ，密码，以及使用 OAuth 连接更新 Azure 门户 [中定义的连接名称](#update-the-azure-portal-with-the-oauth-connection)。</span><span class="sxs-lookup"><span data-stu-id="ce009-226">Update `appsettings.json` to include the `botId`, password, and the connection name defined in [Update the Azure portal with the OAuth connection](#update-the-azure-portal-with-the-oauth-connection).</span></span>
3. <span data-ttu-id="ce009-227">更新清单并确保 `token.botframework.com` 该清单位于有效的域列表中。</span><span class="sxs-lookup"><span data-stu-id="ce009-227">Update the manifest and ensure that `token.botframework.com` is in the valid domains list.</span></span> <span data-ttu-id="ce009-228">有关详细信息，请参阅 [Teams 身份验证示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)。</span><span class="sxs-lookup"><span data-stu-id="ce009-228">For more information, see [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>
4. <span data-ttu-id="ce009-229">Zip the manifest with the profile images and install it in Teams.</span><span class="sxs-lookup"><span data-stu-id="ce009-229">Zip the manifest with the profile images and install it in Teams.</span></span>

#### <a name="additional-code-samples"></a><span data-ttu-id="ce009-230">其他代码示例</span><span class="sxs-lookup"><span data-stu-id="ce009-230">Additional code samples</span></span>

* <span data-ttu-id="ce009-231">[使用 Bot Framework SDK 的 C# 示例](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)。</span><span class="sxs-lookup"><span data-stu-id="ce009-231">[C# sample using the Bot Framework SDK](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore).</span></span>

* <span data-ttu-id="ce009-232">[使用 Bot Framework SDK 删除](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682)令牌请求的 C# 示例。</span><span class="sxs-lookup"><span data-stu-id="ce009-232">[C# sample using the Bot Framework SDK to deduplicate the token request](https://microsoft.sharepoint.com/:u:/t/ExtensibilityandFundamentals/Ea36rUGiN1BGt1RiLOb-mY8BGMF8NwPtronYGym0sCGOTw?e=4bB682).</span></span>

* <span data-ttu-id="ce009-233">[没有使用 Bot Framework SDK 令牌存储的 C# 示例](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw)。</span><span class="sxs-lookup"><span data-stu-id="ce009-233">[C# sample without using the Bot Framework SDK token store](https://microsoft-my.sharepoint-df.com/:u:/p/tac/EceKDXrkMn5AuGbh6iGid8ABKEVQ6hkxArxK1y7-M8OVPw).</span></span>
