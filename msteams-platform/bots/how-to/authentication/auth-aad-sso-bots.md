---
title: 为机器人提供单一登录支持
description: 介绍如何获取用户令牌。 目前，机器人开发人员可以使用登录卡或具有 OAuth 卡支持的 azure 自动程序服务。
keywords: 令牌， 用户令牌， 自动程序 SSO 支持
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: 8da2591c3685b5bd3dffd272abd77babe94ab04c
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020047"
---
# <a name="single-sign-on-sso-support-for-bots"></a><span data-ttu-id="98cb4-105">单一登录 (SSO) 自动程序支持</span><span class="sxs-lookup"><span data-stu-id="98cb4-105">Single sign-on (SSO) support for bots</span></span>

<span data-ttu-id="98cb4-106">AAD Azure Active Directory (中的单一登录身份验证) 以静默方式刷新身份验证令牌，从而最大程度地减少用户输入登录凭据所需的次数。</span><span class="sxs-lookup"><span data-stu-id="98cb4-106">Single sign-on authentication in Azure Active Directory (AAD) minimizes the number of times users need to enter their sign in credentials by silently refreshing the authentication token.</span></span> <span data-ttu-id="98cb4-107">如果用户同意使用你的应用，他们无需在另一台设备上再次提供同意，可自动登录。</span><span class="sxs-lookup"><span data-stu-id="98cb4-107">If users agree to use your app, they need not provide consent again on another device and can sign in automatically.</span></span> <span data-ttu-id="98cb4-108">该流类似于选项卡[SSO](../../../tabs/how-to/authentication/auth-aad-sso.md)Microsoft Teams流，但是，区别在于自动程序如何请求令牌和[接收响应的协议](#receive-the-bot-token)。 [](#request-a-bot-token)</span><span class="sxs-lookup"><span data-stu-id="98cb4-108">The flow is similar to that of [Microsoft Teams tab SSO support](../../../tabs/how-to/authentication/auth-aad-sso.md), however, the difference is in the protocol for how a bot [requests tokens](#request-a-bot-token) and [receives responses](#receive-the-bot-token).</span></span>

>[!NOTE]
> <span data-ttu-id="98cb4-109">OAuth 2.0 是 AAD 和许多其他标识提供程序使用的身份验证和授权的开放式标准。</span><span class="sxs-lookup"><span data-stu-id="98cb4-109">OAuth 2.0 is an open standard for authentication and authorization used by AAD and many other identity providers.</span></span> <span data-ttu-id="98cb4-110">对 OAuth 2.0 有基本的了解是在 Teams 中进行身份验证的先决条件。</span><span class="sxs-lookup"><span data-stu-id="98cb4-110">A basic understanding of OAuth 2.0 is a prerequisite for working with authentication in Teams.</span></span>

## <a name="bot-sso-at-runtime"></a><span data-ttu-id="98cb4-111">运行时自动程序 SSO</span><span class="sxs-lookup"><span data-stu-id="98cb4-111">Bot SSO at runtime</span></span>

![运行时自动程序 SSO 图](../../../assets/images/bots/bots-sso-diagram.png)

<span data-ttu-id="98cb4-113">完成以下步骤，获取身份验证和自动程序应用程序令牌：</span><span class="sxs-lookup"><span data-stu-id="98cb4-113">Complete the following steps to get authentication and bot application tokens:</span></span>

1. <span data-ttu-id="98cb4-114">机器人使用包含 属性的 OAuthCard 发送邮件 `tokenExchangeResource` 。</span><span class="sxs-lookup"><span data-stu-id="98cb4-114">The bot sends a message with an OAuthCard that contains the `tokenExchangeResource` property.</span></span> <span data-ttu-id="98cb4-115">它Teams自动程序应用程序获取身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="98cb4-115">It tells Teams to obtain an authentication token for the bot application.</span></span> <span data-ttu-id="98cb4-116">用户在所有活动用户终结点接收消息。</span><span class="sxs-lookup"><span data-stu-id="98cb4-116">The user receives messages at all the active user endpoints.</span></span>

    > [!NOTE]
    >* <span data-ttu-id="98cb4-117">一个用户一次可以具有多个活动终结点。</span><span class="sxs-lookup"><span data-stu-id="98cb4-117">A user can have more than one active endpoint at a time.</span></span>
    >* <span data-ttu-id="98cb4-118">自动程序令牌从每个活动用户终结点接收。</span><span class="sxs-lookup"><span data-stu-id="98cb4-118">The bot token is received from every active user endpoint.</span></span>
    >* <span data-ttu-id="98cb4-119">应用必须安装在个人范围内，SSO 支持。</span><span class="sxs-lookup"><span data-stu-id="98cb4-119">The app must be installed in personal scope for SSO support.</span></span>

2. <span data-ttu-id="98cb4-120">如果当前用户第一次使用自动程序应用程序，将显示请求提示，请求用户执行下列操作之一：</span><span class="sxs-lookup"><span data-stu-id="98cb4-120">If the current user is using your bot application for the first time, a request prompt appears requesting the user to do one of the following:</span></span>
    * <span data-ttu-id="98cb4-121">如果需要，请提供同意。</span><span class="sxs-lookup"><span data-stu-id="98cb4-121">Provide consent, if required.</span></span>
    * <span data-ttu-id="98cb4-122">处理逐步身份验证，如双重身份验证。</span><span class="sxs-lookup"><span data-stu-id="98cb4-122">Handle step-up authentication, such as two-factor authentication.</span></span>

3. <span data-ttu-id="98cb4-123">Teams当前用户的 AAD 终结点请求自动程序应用程序令牌。</span><span class="sxs-lookup"><span data-stu-id="98cb4-123">Teams requests the bot application token from the AAD endpoint for the current user.</span></span>

4. <span data-ttu-id="98cb4-124">AAD 将自动程序应用程序令牌发送到Teams应用程序。</span><span class="sxs-lookup"><span data-stu-id="98cb4-124">AAD sends the bot application token to the Teams application.</span></span>

5. <span data-ttu-id="98cb4-125">Teams名称为 **sign-in/tokenExchange** 的调用活动返回的值对象，将令牌发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="98cb4-125">Teams sends the token to the bot as part of the value object returned by the invoke activity with the name **sign-in/tokenExchange**.</span></span>
  
6. <span data-ttu-id="98cb4-126">自动程序应用程序中的已分析令牌提供所需信息，如用户的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="98cb4-126">The parsed token in the bot application provides the required information, such as the user's email address.</span></span>
  
## <a name="develop-an-sso-teams-bot"></a><span data-ttu-id="98cb4-127">开发 SSO Teams自动程序</span><span class="sxs-lookup"><span data-stu-id="98cb4-127">Develop an SSO Teams bot</span></span>
  
<span data-ttu-id="98cb4-128">完成以下步骤以开发 SSO 自动Teams程序：</span><span class="sxs-lookup"><span data-stu-id="98cb4-128">Complete the following steps to develop an SSO Teams bot:</span></span>

1. <span data-ttu-id="98cb4-129">[通过 AAD 门户注册应用](#register-your-app-through-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="98cb4-129">[Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span>
2. <span data-ttu-id="98cb4-130">[更新自动Teams应用程序清单](#update-your-teams-application-manifest-for-your-bot)。</span><span class="sxs-lookup"><span data-stu-id="98cb4-130">[Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span>
3. <span data-ttu-id="98cb4-131">[添加代码以请求和接收自动程序令牌](#add-the-code-to-request-and-receive-a-bot-token)。</span><span class="sxs-lookup"><span data-stu-id="98cb4-131">[Add the code to request and receive a bot token](#add-the-code-to-request-and-receive-a-bot-token).</span></span>

### <a name="register-your-app-through-the-aad-portal"></a><span data-ttu-id="98cb4-132">通过 AAD 门户注册应用</span><span class="sxs-lookup"><span data-stu-id="98cb4-132">Register your app through the AAD portal</span></span>

<span data-ttu-id="98cb4-133">通过 AAD 门户注册应用的步骤与选项卡 [SSO 流类似](../../../tabs/how-to/authentication/auth-aad-sso.md)。</span><span class="sxs-lookup"><span data-stu-id="98cb4-133">The steps to register your app through the AAD portal are similar to the [tab SSO flow](../../../tabs/how-to/authentication/auth-aad-sso.md).</span></span> <span data-ttu-id="98cb4-134">完成以下步骤以注册应用：</span><span class="sxs-lookup"><span data-stu-id="98cb4-134">Complete the following steps to register your app:</span></span>

1. <span data-ttu-id="98cb4-135">在应用注册门户Azure Active Directory[注册新](https://go.microsoft.com/fwlink/?linkid=2083908)应用程序。</span><span class="sxs-lookup"><span data-stu-id="98cb4-135">Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
2. <span data-ttu-id="98cb4-136">选择 **"新建注册"。**</span><span class="sxs-lookup"><span data-stu-id="98cb4-136">Select **New Registration**.</span></span> <span data-ttu-id="98cb4-137">将显示 **"注册应用程序"** 页。</span><span class="sxs-lookup"><span data-stu-id="98cb4-137">The **Register an application** page appears.</span></span>
3. <span data-ttu-id="98cb4-138">在 **"注册应用程序"** 页中，输入以下值：</span><span class="sxs-lookup"><span data-stu-id="98cb4-138">In the **Register an application** page, enter the following values:</span></span>
    1. <span data-ttu-id="98cb4-139">为 **应用输入** 名称。</span><span class="sxs-lookup"><span data-stu-id="98cb4-139">Enter a **Name** for your app.</span></span>
    2. <span data-ttu-id="98cb4-140">选择" **支持的帐户类型"，** 选择"单个租户"或"多租户帐户类型"。</span><span class="sxs-lookup"><span data-stu-id="98cb4-140">Choose the **Supported account types**, select single tenant or multitenant account type.</span></span>

        > [!NOTE]
        >
        > <span data-ttu-id="98cb4-141">如果用户在同一租户中注册了 AAD 应用，并且他们在 Teams 中提出身份验证请求，则系统不会要求用户同意并授予访问Teams。</span><span class="sxs-lookup"><span data-stu-id="98cb4-141">The users are not asked for consent and are granted access tokens right away, if the AAD app is registered in the same tenant where they are making an authentication request in Teams.</span></span> <span data-ttu-id="98cb4-142">但是，如果用户在不同的租户中注册了 AAD 应用，则用户必须同意这些权限。</span><span class="sxs-lookup"><span data-stu-id="98cb4-142">However, the users must provide consent to the permissions, if the AAD app is registered in a different tenant.</span></span>

    3. <span data-ttu-id="98cb4-143">选择 **“注册”**。</span><span class="sxs-lookup"><span data-stu-id="98cb4-143">Choose **Register**.</span></span>
4. <span data-ttu-id="98cb4-144">在概述页上，复制并保存应用程序 (**客户端) ID**。</span><span class="sxs-lookup"><span data-stu-id="98cb4-144">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="98cb4-145">稍后在更新应用程序清单时Teams它。</span><span class="sxs-lookup"><span data-stu-id="98cb4-145">You need it later when updating your Teams application manifest.</span></span>
5. <span data-ttu-id="98cb4-146">在“**管理**”下，选择“**公开 API**”。</span><span class="sxs-lookup"><span data-stu-id="98cb4-146">Under **Manage**, select **Expose an API**.</span></span> 

   > [!IMPORTANT]
    > * <span data-ttu-id="98cb4-147">如果要构建独立自动程序，请输入应用程序 ID URI 作为 `api://botid-{YourBotId}` 。</span><span class="sxs-lookup"><span data-stu-id="98cb4-147">If you are building a standalone bot, enter the Application ID URI as `api://botid-{YourBotId}`.</span></span> <span data-ttu-id="98cb4-148">此处 **YourBotId** 是 AAD 应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="98cb4-148">Here **YourBotId** is your AAD application ID.</span></span>
    > * <span data-ttu-id="98cb4-149">如果要使用自动程序和选项卡生成应用，请输入"应用程序 ID URI"作为 `api://fully-qualified-domain-name.com/botid-{YourBotId}` 。</span><span class="sxs-lookup"><span data-stu-id="98cb4-149">If you are building an app with a bot and a tab, enter the Application ID URI as `api://fully-qualified-domain-name.com/botid-{YourBotId}`.</span></span>

5. <span data-ttu-id="98cb4-150">选择应用程序对 AAD 终结点和 Microsoft Graph（可选）所需的权限。</span><span class="sxs-lookup"><span data-stu-id="98cb4-150">Select the permissions that your application needs for the AAD endpoint and, optionally, for Microsoft Graph.</span></span>
6. <span data-ttu-id="98cb4-151">[授予对](/azure/active-directory/develop/v2-permissions-and-consent)桌面Teams Web 和移动应用程序的权限。</span><span class="sxs-lookup"><span data-stu-id="98cb4-151">[Grant permissions](/azure/active-directory/develop/v2-permissions-and-consent) for Teams desktop, web, and mobile applications.</span></span>
7. <span data-ttu-id="98cb4-152">选择 **"添加范围"。**</span><span class="sxs-lookup"><span data-stu-id="98cb4-152">Select **Add a scope**.</span></span>
8. <span data-ttu-id="98cb4-153">在打开的面板中，输入 作为范围名称 `access_as_user` 添加 **客户端应用**。</span><span class="sxs-lookup"><span data-stu-id="98cb4-153">In the panel that opens, add a client app by entering `access_as_user` as the **Scope name**.</span></span>

    >[!NOTE]
    > <span data-ttu-id="98cb4-154">用于access_as_user客户端应用的"安全作用域"适用于"管理员和用户"。</span><span class="sxs-lookup"><span data-stu-id="98cb4-154">The "access_as_user" scope used to add a client app is for "Administrators and users".</span></span>
    >
    > <span data-ttu-id="98cb4-155">您必须了解以下重要限制：</span><span class="sxs-lookup"><span data-stu-id="98cb4-155">You must be aware of the following important restrictions:</span></span>
    >
    > * <span data-ttu-id="98cb4-156">仅支持用户级别的 Microsoft Graph API 权限，如电子邮件、配置文件、offline_access和 OpenId。</span><span class="sxs-lookup"><span data-stu-id="98cb4-156">Only user-level Microsoft Graph API permissions, such as email, profile, offline_access, and OpenId are supported.</span></span> <span data-ttu-id="98cb4-157">如果需要访问其他 Microsoft Graph作用域，例如 `User.Read` 或 `Mail.Read` ，请参阅[建议的解决方法](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes)。</span><span class="sxs-lookup"><span data-stu-id="98cb4-157">If you need access to other Microsoft Graph scopes, such as `User.Read` or `Mail.Read`, see [recommended workaround](../../../tabs/how-to/authentication/auth-aad-sso.md#apps-that-require-additional-graph-scopes).</span></span>
    > * <span data-ttu-id="98cb4-158">应用程序的域名必须与为 AAD 应用程序注册的域名相同。</span><span class="sxs-lookup"><span data-stu-id="98cb4-158">Your application's domain name must be same as the domain name that you have registered for your AAD application.</span></span>
    > * <span data-ttu-id="98cb4-159">当前不支持每个应用程序的多个域。</span><span class="sxs-lookup"><span data-stu-id="98cb4-159">Multiple domains per app are currently not supported.</span></span>
    > * <span data-ttu-id="98cb4-160">使用域 `azurewebsites.net` 的应用程序不受支持，因为它很常见，并且可能是安全风险。</span><span class="sxs-lookup"><span data-stu-id="98cb4-160">Applications that use the `azurewebsites.net` domain are not supported because it is common and may be a security risk.</span></span>

#### <a name="update-the-azure-portal-with-the-oauth-connection"></a><span data-ttu-id="98cb4-161">使用 OAuth 连接更新 Azure 门户</span><span class="sxs-lookup"><span data-stu-id="98cb4-161">Update the Azure portal with the OAuth connection</span></span>

<span data-ttu-id="98cb4-162">完成以下步骤以使用 OAuth 连接更新 Azure 门户：</span><span class="sxs-lookup"><span data-stu-id="98cb4-162">Complete the following steps to update the Azure portal with the OAuth connection:</span></span>

1. <span data-ttu-id="98cb4-163">在 Azure 门户中，导航到 **"应用注册"。**</span><span class="sxs-lookup"><span data-stu-id="98cb4-163">In the Azure Portal, navigate to **App registrations**.</span></span>

2. <span data-ttu-id="98cb4-164">转到 **API 权限**。</span><span class="sxs-lookup"><span data-stu-id="98cb4-164">Go to **API Permissions**.</span></span> <span data-ttu-id="98cb4-165">选择 **"添加**  >  **Microsoft Graph** 委派权限"，然后从 Microsoft Graph API  >  添加以下权限：</span><span class="sxs-lookup"><span data-stu-id="98cb4-165">Select **Add a permission** > **Microsoft Graph** > **Delegated permissions**, then add the following permissions from Microsoft Graph API:</span></span>
    * <span data-ttu-id="98cb4-166">User.Read (默认启用) </span><span class="sxs-lookup"><span data-stu-id="98cb4-166">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="98cb4-167">email</span><span class="sxs-lookup"><span data-stu-id="98cb4-167">email</span></span>
    * <span data-ttu-id="98cb4-168">offline_access</span><span class="sxs-lookup"><span data-stu-id="98cb4-168">offline_access</span></span>
    * <span data-ttu-id="98cb4-169">OpenId</span><span class="sxs-lookup"><span data-stu-id="98cb4-169">OpenId</span></span>
    * <span data-ttu-id="98cb4-170">个人资料</span><span class="sxs-lookup"><span data-stu-id="98cb4-170">profile</span></span>

3. <span data-ttu-id="98cb4-171">在 Azure 门户中，导航到 **"自动程序通道注册"。**</span><span class="sxs-lookup"><span data-stu-id="98cb4-171">In the Azure Portal, navigate to **Bot Channels Registration**.</span></span>

4. <span data-ttu-id="98cb4-172">选择 **设置** 窗格上的"设置"，**然后选择\*\*\*\*"OAuth** 连接"部分下的"添加设置设置"。</span><span class="sxs-lookup"><span data-stu-id="98cb4-172">Select **Settings** on the left pane and choose **Add Setting** under the **OAuth Connection Settings** section.</span></span>

    ![SSOBotHandle2 视图](../../../assets/images/bots/bots-vuSSOBotHandle2-settings.png)

5. <span data-ttu-id="98cb4-174">执行以下步骤以完成"新建 **连接设置"** 表单：</span><span class="sxs-lookup"><span data-stu-id="98cb4-174">Perform the following steps to complete the **New Connection Setting** form:</span></span>

    >[!NOTE]
    > <span data-ttu-id="98cb4-175">**AAD** 应用程序中可能需要隐式授权。</span><span class="sxs-lookup"><span data-stu-id="98cb4-175">**Implicit grant** may be required in the AAD application.</span></span>

    1. <span data-ttu-id="98cb4-176">在" **新建连接** 设置 **"页中输入名称** 。</span><span class="sxs-lookup"><span data-stu-id="98cb4-176">Enter a **Name** in the **New Connection Setting** page.</span></span> <span data-ttu-id="98cb4-177">这是在运行时自动程序 SSO 步骤 *5* 中的自动程序服务代码设置 [内引用的名称](#bot-sso-at-runtime)。</span><span class="sxs-lookup"><span data-stu-id="98cb4-177">This is the name that is referred to inside the settings of your bot service code in *step 5* of [Bot SSO at runtime](#bot-sso-at-runtime).</span></span>
    2. <span data-ttu-id="98cb4-178">从"**服务提供商"** 下拉列表中，选择 **"Azure Active Directory v2"。**</span><span class="sxs-lookup"><span data-stu-id="98cb4-178">From the **Service Provider** drop-down, select **Azure Active Directory v2**.</span></span>
    3. <span data-ttu-id="98cb4-179">输入客户端凭据，例如 AAD 应用程序的 **客户端** **ID** 和客户端密码。</span><span class="sxs-lookup"><span data-stu-id="98cb4-179">Enter the client credentials, such as **Client id** and **Client secret** for the AAD application.</span></span>
    4. <span data-ttu-id="98cb4-180">对于 **令牌Exchange URL，** 请使用更新自动程序Teams应用程序清单中 [定义的作用域值](#update-your-teams-application-manifest-for-your-bot)。</span><span class="sxs-lookup"><span data-stu-id="98cb4-180">For the **Token Exchange URL**, use the scope value defined in [Update your Teams application manifest for your bot](#update-your-teams-application-manifest-for-your-bot).</span></span> <span data-ttu-id="98cb4-181">令牌Exchange URL 向 SDK 指示此 AAD 应用程序已针对 SSO 进行配置。</span><span class="sxs-lookup"><span data-stu-id="98cb4-181">The Token Exchange URL indicates to the SDK that this AAD application is configured for SSO.</span></span>
    5. <span data-ttu-id="98cb4-182">在" **租户 ID"** 框中，输入 *常用*。</span><span class="sxs-lookup"><span data-stu-id="98cb4-182">In the **Tenant ID** box, enter *common*.</span></span>
    6. <span data-ttu-id="98cb4-183">添加 **为** AAD 应用程序指定下游 API 的权限时配置的所有作用域。</span><span class="sxs-lookup"><span data-stu-id="98cb4-183">Add all the **Scopes** configured when specifying permissions to downstream APIs for your AAD application.</span></span> <span data-ttu-id="98cb4-184">提供客户端 ID 和客户端密码后，令牌存储将令牌交换为具有定义权限的图形令牌。</span><span class="sxs-lookup"><span data-stu-id="98cb4-184">With the Client id and Client secret provided, the token store exchanges the token for a graph token with defined permissions.</span></span>
    7. <span data-ttu-id="98cb4-185">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="98cb4-185">Select **Save**.</span></span>

    ![VuSSOBotConnection 设置视图](../../../assets/images/bots/bots-vuSSOBotConnection-settings.png)

### <a name="update-your-teams-application-manifest-for-your-bot"></a><span data-ttu-id="98cb4-187">更新自动Teams应用程序清单</span><span class="sxs-lookup"><span data-stu-id="98cb4-187">Update your Teams application manifest for your bot</span></span>

<span data-ttu-id="98cb4-188">如果应用程序包含独立自动程序，则使用以下代码将新属性添加到Teams清单：</span><span class="sxs-lookup"><span data-stu-id="98cb4-188">If the application contains a standalone bot, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://botid-00000000-0000-0000-0000-000000000000"
        }
```
<span data-ttu-id="98cb4-189">如果应用程序包含自动程序和选项卡，则使用以下代码将新属性添加到Teams清单：</span><span class="sxs-lookup"><span data-stu-id="98cb4-189">If the application contains a bot and a tab, then use the following code to add new properties to the Teams application manifest:</span></span>

```json
    "webApplicationInfo": 
        {
            "id": "00000000-0000-0000-0000-000000000000",
            "resource": "api://subdomain.example.com/botid-00000000-0000-0000-0000-000000000000"
        }
```

<span data-ttu-id="98cb4-190">**webApplicationInfo** 是以下元素的父元素：</span><span class="sxs-lookup"><span data-stu-id="98cb4-190">**webApplicationInfo** is the parent of the following elements:</span></span>

* <span data-ttu-id="98cb4-191">**id** - 应用程序的客户端 ID。</span><span class="sxs-lookup"><span data-stu-id="98cb4-191">**id** - The client ID of the application.</span></span> <span data-ttu-id="98cb4-192">这是在向 AAD 注册应用程序时获取的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="98cb4-192">This is the application ID that you obtained as part of registering the application with AAD.</span></span>
* <span data-ttu-id="98cb4-193">**resource** - 应用程序的域和子域。</span><span class="sxs-lookup"><span data-stu-id="98cb4-193">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="98cb4-194">这是相同的 URI，包括在通过 AAD 门户注册应用时注册 `api://` `scope` [的协议](#register-your-app-through-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="98cb4-194">This is the same URI, including the `api://` protocol that you registered when creating your `scope` in [Register your app through the AAD portal](#register-your-app-through-the-aad-portal).</span></span> <span data-ttu-id="98cb4-195">不得在资源 `access_as_user` 中包括路径。</span><span class="sxs-lookup"><span data-stu-id="98cb4-195">You must not include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="98cb4-196">此 URI 的域部分必须与应用程序清单的 URL 中使用的域和子Teams匹配。</span><span class="sxs-lookup"><span data-stu-id="98cb4-196">The domain part of this URI must match the domain and subdomains used in the URLs of your Teams application manifest.</span></span>

### <a name="add-the-code-to-request-and-receive-a-bot-token"></a><span data-ttu-id="98cb4-197">添加代码以请求和接收自动程序令牌</span><span class="sxs-lookup"><span data-stu-id="98cb4-197">Add the code to request and receive a bot token</span></span>

#### <a name="request-a-bot-token"></a><span data-ttu-id="98cb4-198">请求自动程序令牌</span><span class="sxs-lookup"><span data-stu-id="98cb4-198">Request a bot token</span></span>

<span data-ttu-id="98cb4-199">获取令牌的请求是使用现有邮件架构的普通 POST 邮件请求。</span><span class="sxs-lookup"><span data-stu-id="98cb4-199">The request to get the token is a normal POST message request using the existing message schema.</span></span> <span data-ttu-id="98cb4-200">它包含在 OAuthCard 的附件中。</span><span class="sxs-lookup"><span data-stu-id="98cb4-200">It is included in the attachments of an OAuthCard.</span></span> <span data-ttu-id="98cb4-201">OAuthCard 类的架构在 Microsoft [Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) 中定义，它类似于登录卡。</span><span class="sxs-lookup"><span data-stu-id="98cb4-201">The schema for the OAuthCard class is defined in [Microsoft Bot Schema 4.0](/dotnet/api/microsoft.bot.schema.oauthcard?view=botbuilder-dotnet-stable&preserve-view=true) and it is similar to a sign-in card.</span></span> <span data-ttu-id="98cb4-202">Teams在卡片上填充属性时，将此请求视为 `TokenExchangeResource` 无提示令牌获取。</span><span class="sxs-lookup"><span data-stu-id="98cb4-202">Teams treats this request as a silent token acquisition if the `TokenExchangeResource` property is populated on the card.</span></span> <span data-ttu-id="98cb4-203">对于Teams通道，仅处理唯一标识 `Id` 令牌请求的属性。</span><span class="sxs-lookup"><span data-stu-id="98cb4-203">For the Teams channel, only the `Id` property, which uniquely identifies a token request, is honored.</span></span>

>[!NOTE]
> <span data-ttu-id="98cb4-204">SSO 身份验证支持 Microsoft Bot Framework `OAuthPrompt` `MultiProviderAuthDialog` 或 。</span><span class="sxs-lookup"><span data-stu-id="98cb4-204">The Microsoft Bot Framework `OAuthPrompt` or the `MultiProviderAuthDialog` is supported for SSO authentication.</span></span>

<span data-ttu-id="98cb4-205">如果用户第一次使用该应用程序并且需要用户同意，则显示以下对话框以继续获得同意体验：</span><span class="sxs-lookup"><span data-stu-id="98cb4-205">If the user is using the application for the first time and user consent is required, the following dialog box appears to continue with the consent experience:</span></span>

!["同意"对话框](../../../assets/images/bots/bots-consent-dialogbox.png)

<span data-ttu-id="98cb4-207">当用户选择"继续 **"时**，将发生以下事件：</span><span class="sxs-lookup"><span data-stu-id="98cb4-207">When the user selects **Continue**, the following events occur:</span></span>

* <span data-ttu-id="98cb4-208">如果机器人定义了登录按钮，则自动程序登录流程的触发方式类似于来自邮件流中 OAuth 卡按钮的登录流。</span><span class="sxs-lookup"><span data-stu-id="98cb4-208">If the bot defines a sign-in button, the sign in flow for bots is triggered similar to the sign in flow from an OAuth card button in a message stream.</span></span> <span data-ttu-id="98cb4-209">开发人员必须决定需要征得用户同意的权限。</span><span class="sxs-lookup"><span data-stu-id="98cb4-209">The developer must decide which permissions require user's consent.</span></span> <span data-ttu-id="98cb4-210">如果需要权限超过 的令牌，建议采用此方法 `openId` 。</span><span class="sxs-lookup"><span data-stu-id="98cb4-210">This approach is recommended if you require a token with permissions beyond `openId`.</span></span> <span data-ttu-id="98cb4-211">例如，如果要交换图形资源的令牌。</span><span class="sxs-lookup"><span data-stu-id="98cb4-211">For example, if you want to exchange the token for graph resources.</span></span>

* <span data-ttu-id="98cb4-212">如果自动程序未在 OAuth 卡上提供登录按钮，需要用户同意才能获得最低权限集。</span><span class="sxs-lookup"><span data-stu-id="98cb4-212">If the bot is not providing a sign-in button on the OAuth card, user consent is required for a minimal set of permissions.</span></span> <span data-ttu-id="98cb4-213">此令牌可用于基本身份验证和获取用户的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="98cb4-213">This token is useful for basic authentication and to get the user's email address.</span></span>

##### <a name="c-token-request-without-a-sign-in-button"></a><span data-ttu-id="98cb4-214">C#登录按钮创建令牌请求</span><span class="sxs-lookup"><span data-stu-id="98cb4-214">C# token request without a sign-in button</span></span>

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

#### <a name="receive-the-bot-token"></a><span data-ttu-id="98cb4-215">接收自动程序令牌</span><span class="sxs-lookup"><span data-stu-id="98cb4-215">Receive the bot token</span></span>

<span data-ttu-id="98cb4-216">通过调用活动发送包含令牌的响应，该活动架构与机器人今天接收的其他调用活动相同。</span><span class="sxs-lookup"><span data-stu-id="98cb4-216">The response with the token is sent through an invoke activity with the same schema as other invoke activities that the bots receive today.</span></span> <span data-ttu-id="98cb4-217">唯一的区别是调用名称、 **登录/令牌Exchange** 和 **值** 字段。</span><span class="sxs-lookup"><span data-stu-id="98cb4-217">The only difference is the invoke name, **sign-in/tokenExchange** and the **value** field.</span></span> <span data-ttu-id="98cb4-218">**值** 字段包含 **Id（** 获取令牌的初始请求的字符串）和 **令牌** 字段，字符串值（包括令牌）。</span><span class="sxs-lookup"><span data-stu-id="98cb4-218">The **value** field contains the **Id**, a string of the initial request to get the token and the **token** field, a string value including the token.</span></span>

>[!NOTE]
> <span data-ttu-id="98cb4-219">如果用户有多个活动终结点，您可能会收到针对给定请求的多个响应。</span><span class="sxs-lookup"><span data-stu-id="98cb4-219">You might receive multiple responses for a given request if the user has multiple active endpoints.</span></span> <span data-ttu-id="98cb4-220">必须使用令牌删除响应。</span><span class="sxs-lookup"><span data-stu-id="98cb4-220">You must deduplicate the responses with the token.</span></span>

##### <a name="c-code-to-handle-the-invoke-activity"></a><span data-ttu-id="98cb4-221">C#调用活动的代码</span><span class="sxs-lookup"><span data-stu-id="98cb4-221">C# code to handle the invoke activity</span></span>

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

<span data-ttu-id="98cb4-222">`turnContext.activity.value`为[TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true)类型，包含自动程序可以进一步使用的令牌。</span><span class="sxs-lookup"><span data-stu-id="98cb4-222">The `turnContext.activity.value` is of type [TokenExchangeInvokeRequest](/dotnet/api/microsoft.bot.schema.tokenexchangeinvokerequest?view=botbuilder-dotnet-stable&preserve-view=true) and contains the token that can be further used by your bot.</span></span> <span data-ttu-id="98cb4-223">出于性能原因，必须存储令牌并刷新它们。</span><span class="sxs-lookup"><span data-stu-id="98cb4-223">You must store the tokens for performance reasons and refresh them.</span></span>

### <a name="token-exchange-failure"></a><span data-ttu-id="98cb4-224">令牌交换失败</span><span class="sxs-lookup"><span data-stu-id="98cb4-224">Token exchange failure</span></span>

<span data-ttu-id="98cb4-225">如果令牌交换失败，请使用以下代码：</span><span class="sxs-lookup"><span data-stu-id="98cb4-225">In case of token exchange failure, use the following code:</span></span>

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

<span data-ttu-id="98cb4-226">若要了解当令牌交换无法触发同意提示时自动程序执行哪些操作，请参阅以下步骤：</span><span class="sxs-lookup"><span data-stu-id="98cb4-226">To understand what the bot does when the token exchange fails to trigger a consent prompt, see the following steps:</span></span>

>[!NOTE]
> <span data-ttu-id="98cb4-227">当令牌交换失败时，自动程序无需执行任何用户操作。</span><span class="sxs-lookup"><span data-stu-id="98cb4-227">No user action is required to be taken as the bot takes the actions when the token exchange fails.</span></span>

1. <span data-ttu-id="98cb4-228">客户端与触发 OAuth 方案的机器人开始对话。</span><span class="sxs-lookup"><span data-stu-id="98cb4-228">The client starts a conversation with the bot triggering an OAuth scenario.</span></span>
2. <span data-ttu-id="98cb4-229">机器人将 OAuth 卡发送回客户端。</span><span class="sxs-lookup"><span data-stu-id="98cb4-229">The bot sends back an OAuth card to the client.</span></span>
3. <span data-ttu-id="98cb4-230">客户端在向用户显示 OAuth 卡之前截获该卡片，并检查其是否包含 `TokenExchangeResource` 属性。</span><span class="sxs-lookup"><span data-stu-id="98cb4-230">The client intercepts the OAuth card before displaying it to the user and checks if it contains a `TokenExchangeResource` property.</span></span>
4. <span data-ttu-id="98cb4-231">如果该属性存在，客户端会向 `TokenExchangeInvokeRequest` 自动程序发送 。</span><span class="sxs-lookup"><span data-stu-id="98cb4-231">If the property exists, the client sends a `TokenExchangeInvokeRequest` to the bot.</span></span> <span data-ttu-id="98cb4-232">客户端必须具有用户的可交换令牌，该令牌必须是 Azure AD v2 令牌，并且其访问群体必须与 `TokenExchangeResource.Uri` 属性相同。</span><span class="sxs-lookup"><span data-stu-id="98cb4-232">The client must have an exchangeable token for the user, which must be an Azure AD v2 token and whose audience must be the same as `TokenExchangeResource.Uri` property.</span></span> <span data-ttu-id="98cb4-233">客户端通过以下代码向机器人发送调用活动：</span><span class="sxs-lookup"><span data-stu-id="98cb4-233">The client sends an invoke activity to the bot with the following code:</span></span>

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

5. <span data-ttu-id="98cb4-234">自动程序处理 `TokenExchangeInvokeRequest` 并返回 `TokenExchangeInvokeResponse` 回客户端。</span><span class="sxs-lookup"><span data-stu-id="98cb4-234">The bot processes the `TokenExchangeInvokeRequest` and returns a `TokenExchangeInvokeResponse` back to the client.</span></span> <span data-ttu-id="98cb4-235">客户端必须等待，直到收到 `TokenExchangeInvokeResponse` 。</span><span class="sxs-lookup"><span data-stu-id="98cb4-235">The client must wait till it receives the `TokenExchangeInvokeResponse`.</span></span>

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

6. <span data-ttu-id="98cb4-236">如果 `TokenExchangeInvokeResponse` 具有 `status` `200` 的 ，则客户端不会显示 OAuth 卡。</span><span class="sxs-lookup"><span data-stu-id="98cb4-236">If the `TokenExchangeInvokeResponse` has a `status` of `200`, then the client does not show the OAuth card.</span></span> <span data-ttu-id="98cb4-237">请参阅 [正常流图像](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="98cb4-237">See the [normal flow image](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true).</span></span> <span data-ttu-id="98cb4-238">对于任何其他 `status` 或如果未收到 `TokenExchangeInvokeResponse` ，客户端会向用户显示 OAuth 卡。</span><span class="sxs-lookup"><span data-stu-id="98cb4-238">For any other `status` or if the `TokenExchangeInvokeResponse` is not received, then the client shows the OAuth card to the user.</span></span> <span data-ttu-id="98cb4-239">请参阅 [回退流图像](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="98cb4-239">See the [fallback flow image](/azure/bot-service/bot-builder-concept-sso?view=azure-bot-service-4.0#sso-components-interaction&preserve-view=true).</span></span> <span data-ttu-id="98cb4-240">这可确保 SSO 流在出现任何错误或未满足依赖关系（如用户同意）时恢复为正常 OAuthCard 流。</span><span class="sxs-lookup"><span data-stu-id="98cb4-240">This ensures that the SSO flow falls back to normal OAuthCard flow in case of any errors or unmet dependencies like user consent.</span></span>


### <a name="update-the-auth-sample"></a><span data-ttu-id="98cb4-241">更新身份验证示例</span><span class="sxs-lookup"><span data-stu-id="98cb4-241">Update the auth sample</span></span>

<span data-ttu-id="98cb4-242">打开[Teams身份验证示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)，然后完成以下步骤以更新它：</span><span class="sxs-lookup"><span data-stu-id="98cb4-242">Open [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth) and then complete the following steps to update it:</span></span>

1. <span data-ttu-id="98cb4-243">通过添加以下代码，更新 TeamsBot 以处理传入请求的 deduping：</span><span class="sxs-lookup"><span data-stu-id="98cb4-243">Update the TeamsBot to handle the deduping of the incoming request by including the following code:</span></span>

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
  
2. <span data-ttu-id="98cb4-244">更新以包含 、密码和在使用 OAuth 连接更新 Azure 门户 `appsettings.json` `botId` [中定义的连接名称](#update-the-azure-portal-with-the-oauth-connection)。</span><span class="sxs-lookup"><span data-stu-id="98cb4-244">Update `appsettings.json` to include the `botId`, password, and the connection name defined in [Update the Azure portal with the OAuth connection](#update-the-azure-portal-with-the-oauth-connection).</span></span>
3. <span data-ttu-id="98cb4-245">更新清单并确保 `token.botframework.com` 它位于有效的域列表中。</span><span class="sxs-lookup"><span data-stu-id="98cb4-245">Update the manifest and ensure that `token.botframework.com` is in the valid domains list.</span></span> <span data-ttu-id="98cb4-246">有关详细信息，请参阅Teams[身份验证示例](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth)。</span><span class="sxs-lookup"><span data-stu-id="98cb4-246">For more information, see [Teams auth sample](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/46.teams-auth).</span></span>
4. <span data-ttu-id="98cb4-247">Zip the manifest with the profile images and install it in Teams.</span><span class="sxs-lookup"><span data-stu-id="98cb4-247">Zip the manifest with the profile images and install it in Teams.</span></span>

## <a name="code-sample"></a><span data-ttu-id="98cb4-248">代码示例</span><span class="sxs-lookup"><span data-stu-id="98cb4-248">Code sample</span></span>
|<span data-ttu-id="98cb4-249">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="98cb4-249">**Sample name**</span></span> | <span data-ttu-id="98cb4-250">**说明**</span><span class="sxs-lookup"><span data-stu-id="98cb4-250">**Description**</span></span> |<span data-ttu-id="98cb4-251">**.NET**</span><span class="sxs-lookup"><span data-stu-id="98cb4-251">**.NET**</span></span> | 
|----------------|-----------------|--------------|
|<span data-ttu-id="98cb4-252">自动程序框架 SDK</span><span class="sxs-lookup"><span data-stu-id="98cb4-252">Bot framework SDK</span></span> | <span data-ttu-id="98cb4-253">使用自动程序框架 SDK 的示例。</span><span class="sxs-lookup"><span data-stu-id="98cb4-253">Sample for using the bot framework SDK.</span></span> |[<span data-ttu-id="98cb4-254">View</span><span class="sxs-lookup"><span data-stu-id="98cb4-254">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/experimental/teams-sso/csharp_dotnetcore)|
