---
title: 单一登录
description: 描述 (SSO) 的单一登录
keywords: 团队身份验证 SSO AAD 单一登录 api
ms.openlocfilehash: cf3c33cf9721243936890140d5bcce641c443e2e
ms.sourcegitcommit: 7a2da3b65246a125d441a971e7e6a6418355adbe
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2020
ms.locfileid: "46587732"
---
# <a name="single-sign-on-sso"></a><span data-ttu-id="2beb6-104"> (SSO) 的单一登录</span><span class="sxs-lookup"><span data-stu-id="2beb6-104">Single Sign-On (SSO)</span></span>

<span data-ttu-id="2beb6-105">用户通过其工作、学校或 Microsoft 帐户登录 Microsoft 团队 (Office 365、Outlook 等) 。</span><span class="sxs-lookup"><span data-stu-id="2beb6-105">Users sign in to Microsoft Teams via their work, school, or Microsoft accounts (Office 365, Outlook, etc).</span></span> <span data-ttu-id="2beb6-106">通过允许单一登录对桌面或移动客户端上的 Microsoft "团队" 选项卡 (或任务模块) 进行授权，可以利用这一点。</span><span class="sxs-lookup"><span data-stu-id="2beb6-106">You can take advantage of this by allowing a single sign-on to authorize your Microsoft Teams tab (or task module) on desktop or mobile clients.</span></span> <span data-ttu-id="2beb6-107">因此，如果用户同意使用您的应用程序，则无需再次在其他设备上同意，它们将自动登录。</span><span class="sxs-lookup"><span data-stu-id="2beb6-107">Thus, if a user consents to use your app, they won’t have to consent again on another device — they will signed in be automatically.</span></span> <span data-ttu-id="2beb6-108">此外，我们还会预提取访问令牌，以提高性能和加载时间。</span><span class="sxs-lookup"><span data-stu-id="2beb6-108">In addition, we prefetch your access token to improve performance and load times.</span></span>

## <a name="how-sso-works-at-runtime"></a><span data-ttu-id="2beb6-109">运行时 SSO 的工作方式</span><span class="sxs-lookup"><span data-stu-id="2beb6-109">How SSO works at runtime</span></span>

<span data-ttu-id="2beb6-110">下图显示 SSO 进程的工作原理：</span><span class="sxs-lookup"><span data-stu-id="2beb6-110">The following diagram shows how the SSO process works:</span></span>

<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. <span data-ttu-id="2beb6-111">在 "" 选项卡中，对进行了 JavaScript 调用 `getAuthToken()` 。</span><span class="sxs-lookup"><span data-stu-id="2beb6-111">In the tab, a JavaScript call is made to `getAuthToken()`.</span></span> <span data-ttu-id="2beb6-112">这将告知团队获取选项卡应用程序的身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="2beb6-112">This tells Teams to obtain an authentication token for the tab application.</span></span>
2. <span data-ttu-id="2beb6-113">如果这是当前用户第一次使用您的选项卡应用程序，则在需要同意时，将会发出请求提示 () 或处理步骤验证 (如双重身份验证) ）。</span><span class="sxs-lookup"><span data-stu-id="2beb6-113">If this is the first time the current user has used your tab application, there will be a request prompt to consent (if consent is required) or to handle step-up authentication (such as two-factor authentication).</span></span>
3. <span data-ttu-id="2beb6-114">团队从当前用户的 Azure AD 终结点请求选项卡应用程序令牌。</span><span class="sxs-lookup"><span data-stu-id="2beb6-114">Teams requests the tab application token from the Azure AD endpoint for the current user.</span></span>
4. <span data-ttu-id="2beb6-115">Azure AD 将选项卡应用程序令牌发送给团队应用程序。</span><span class="sxs-lookup"><span data-stu-id="2beb6-115">Azure AD sends the tab application token to the Teams application.</span></span>
5. <span data-ttu-id="2beb6-116">团队将选项卡应用程序令牌作为调用返回的 result 对象的一部分发送到选项卡 `getAuthToken()` 。</span><span class="sxs-lookup"><span data-stu-id="2beb6-116">Teams sends the tab application token to the tab as part of the result object returned by the `getAuthToken()` call.</span></span>
6. <span data-ttu-id="2beb6-117">将通过 JavaScript 在选项卡应用程序中分析令牌，以提取所需的信息，如用户的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="2beb6-117">The token will be parsed in the tab application, via JavaScript, to extract the needed information, such as the user's email address.</span></span>

> [!NOTE]
> <span data-ttu-id="2beb6-118">`getAuthToken()`仅适用于同意一组有限的用户级 api （电子邮件、配置文件、offline_access 和 OpenId），而不是对更多 Microsoft Graph 范围（例如或）有效 `User.Read` `Mail.Read` 。</span><span class="sxs-lookup"><span data-stu-id="2beb6-118">The `getAuthToken()` is only valid for consenting to a limited set of user-level APIs — email, profile, offline_access and OpenId — and not for further Microsoft Graph scopes such as `User.Read` or `Mail.Read`.</span></span> <span data-ttu-id="2beb6-119">如果你需要[其他 Graph 作用域](#apps-that-require-additional-microsoft-graph-scopes)，请参阅本文档末尾的部分，了解建议的解决方法。</span><span class="sxs-lookup"><span data-stu-id="2beb6-119">See our section at the end of this document for suggested workarounds if you require [additional Graph scopes](#apps-that-require-additional-microsoft-graph-scopes).</span></span>

<span data-ttu-id="2beb6-120">SSO API 也可在嵌入 web 内容的[任务模块](../../../task-modules-and-cards/what-are-task-modules.md)中运行。</span><span class="sxs-lookup"><span data-stu-id="2beb6-120">The SSO API will also work in [Task Modules](../../../task-modules-and-cards/what-are-task-modules.md) that embed web content.</span></span>

## <a name="develop-an-sso-microsoft-teams-tab"></a><span data-ttu-id="2beb6-121">开发 SSO Microsoft 团队选项卡</span><span class="sxs-lookup"><span data-stu-id="2beb6-121">Develop an SSO Microsoft Teams tab</span></span>

<span data-ttu-id="2beb6-122">本节介绍创建使用 SSO 的 "团队" 选项卡所涉及的任务。</span><span class="sxs-lookup"><span data-stu-id="2beb6-122">This section describes the tasks involved in creating a Teams tab that uses SSO.</span></span> <span data-ttu-id="2beb6-123">此处介绍了这些任务是语言和框架不可知的。</span><span class="sxs-lookup"><span data-stu-id="2beb6-123">These tasks are described here are language- and framework-agnostic.</span></span>

### <a name="1-create-your-azure-active-directory-azure-ad-application"></a><span data-ttu-id="2beb6-124">1. 在 Azure AD) 应用程序中创建 Azure Active Directory (</span><span class="sxs-lookup"><span data-stu-id="2beb6-124">1. Create your Azure Active Directory (Azure AD) application</span></span>

<span data-ttu-id="2beb6-125">在[AZURE AD 门户](https://azure.microsoft.com/features/azure-portal/)中注册应用程序。</span><span class="sxs-lookup"><span data-stu-id="2beb6-125">Register your application in the[Azure AD portal](https://azure.microsoft.com/features/azure-portal/).</span></span> <span data-ttu-id="2beb6-126">该流程用时 5-10 分钟，包括以下任务：</span><span class="sxs-lookup"><span data-stu-id="2beb6-126">This is a 5–10 minute process that includes the following tasks:</span></span>

1. <span data-ttu-id="2beb6-127">获取[AZURE AD 应用程序 ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)。</span><span class="sxs-lookup"><span data-stu-id="2beb6-127">Get your [Azure AD Application ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).</span></span>
2. <span data-ttu-id="2beb6-128">指定应用程序需要的 Azure AD 终结点和 Microsoft Graph （可选）的权限。</span><span class="sxs-lookup"><span data-stu-id="2beb6-128">Specify the permissions that your application needs for the Azure AD endpoint and, optionally, Microsoft Graph.</span></span>
3. <span data-ttu-id="2beb6-129">[授予](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources)对团队桌面、web 和移动应用程序的权限。</span><span class="sxs-lookup"><span data-stu-id="2beb6-129">[Grant permissions](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) for Teams desktop, web, and mobile applications.</span></span>
4. <span data-ttu-id="2beb6-130">预授权团队通过选择 "**添加范围**" 按钮，并在打开的面板中，输入 `access_as_user` 作为**作用域名称**。</span><span class="sxs-lookup"><span data-stu-id="2beb6-130">Pre-authorize Teams by selecting the **Add a scope** button and in the panel that opens, enter `access_as_user` as the **Scope name**.</span></span>

> [!NOTE]
> <span data-ttu-id="2beb6-131">您应注意一些重要限制：</span><span class="sxs-lookup"><span data-stu-id="2beb6-131">There are some important restrictions you should be aware of:</span></span>
>
> * <span data-ttu-id="2beb6-132">仅支持用户级别的 Microsoft Graph API 权限，即电子邮件、配置文件、offline_access、OpenId。</span><span class="sxs-lookup"><span data-stu-id="2beb6-132">We only support user-level Microsoft Graph API permissions, i.e., email, profile, offline_access, OpenId.</span></span> <span data-ttu-id="2beb6-133">如果需要访问其他 Microsoft Graph 作用域 (例如 `User.Read` 或 `Mail.Read`) ，请参阅本文档末尾的[建议解决方法](#apps-that-require-additional-microsoft-graph-scopes)。</span><span class="sxs-lookup"><span data-stu-id="2beb6-133">If you need access to other Microsoft Graph scopes (such as `User.Read` or `Mail.Read`), see our [recommended workaround](#apps-that-require-additional-microsoft-graph-scopes) at the end of this documentation.</span></span>
> * <span data-ttu-id="2beb6-134">您的应用程序的域名与您为 Azure AD 应用程序注册的域名称相同，这一点很重要。</span><span class="sxs-lookup"><span data-stu-id="2beb6-134">It's important that your application's domain name is the same as the domain name you've registering for your Azure AD application.</span></span>
> * <span data-ttu-id="2beb6-135">目前，我们不支持每个应用的多个域。</span><span class="sxs-lookup"><span data-stu-id="2beb6-135">We don't currently support multiple domains per app.</span></span>
> * <span data-ttu-id="2beb6-136">我们不支持使用域的应用程序， `azurewebsites.net` 因为它太常见，可能存在安全风险。</span><span class="sxs-lookup"><span data-stu-id="2beb6-136">We don't support applications that use the `azurewebsites.net` domain because it is too common and may be a security risk.</span></span> <span data-ttu-id="2beb6-137">但是，我们正在努力删除此限制。</span><span class="sxs-lookup"><span data-stu-id="2beb6-137">However, we're actively seeking to remove this restriction.</span></span>

#### <a name="steps"></a><span data-ttu-id="2beb6-138">步骤</span><span class="sxs-lookup"><span data-stu-id="2beb6-138">Steps</span></span>

1. <span data-ttu-id="2beb6-139">在[Azure Active Directory –应用程序注册](https://go.microsoft.com/fwlink/?linkid=2083908)门户中注册新的应用程序。</span><span class="sxs-lookup"><span data-stu-id="2beb6-139">Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
2. <span data-ttu-id="2beb6-140">选择 "**新建注册**"，并在 "*注册应用程序" 页*上，设置以下值：</span><span class="sxs-lookup"><span data-stu-id="2beb6-140">Select **New Registration** and on the *register an application page*, set following values:</span></span>
    * <span data-ttu-id="2beb6-141">将**名称**设置为您的应用程序名称。</span><span class="sxs-lookup"><span data-stu-id="2beb6-141">Set **name** to your app name.</span></span>
    * <span data-ttu-id="2beb6-142">选择**受支持的帐户类型** (任何帐户类型的工作) ¹</span><span class="sxs-lookup"><span data-stu-id="2beb6-142">Choose the **supported account types** (any account type will work) ¹</span></span>
    * <span data-ttu-id="2beb6-143">保留“重定向 URI”\*\*\*\* 为空。</span><span class="sxs-lookup"><span data-stu-id="2beb6-143">Leave **Redirect URI** empty.</span></span>
    * <span data-ttu-id="2beb6-144">选择“注册”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="2beb6-144">Choose **Register**.</span></span>
3. <span data-ttu-id="2beb6-145">在 "概述" 页上，将应用程序复制并保存\*\* (客户端) ID\*\*。</span><span class="sxs-lookup"><span data-stu-id="2beb6-145">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="2beb6-146">稍后在更新团队应用程序清单时，将需要它。</span><span class="sxs-lookup"><span data-stu-id="2beb6-146">You’ll need it later when updating your Teams application manifest.</span></span>
4. <span data-ttu-id="2beb6-147">在“**管理**”下，选择“**公开 API**”。</span><span class="sxs-lookup"><span data-stu-id="2beb6-147">Under **Manage**, select **Expose an API**.</span></span> 
5. <span data-ttu-id="2beb6-148">选择 "**设置**" 链接，以以的形式生成应用程序 ID URI `api://{AppID}` 。</span><span class="sxs-lookup"><span data-stu-id="2beb6-148">Select the **Set** link to generate the Application ID URI in the form of `api://{AppID}`.</span></span> <span data-ttu-id="2beb6-149">插入完全限定的域名 (，并追加一个正斜杠 "/"，并追加到双正斜杠和 GUID 之间的结束) 。</span><span class="sxs-lookup"><span data-stu-id="2beb6-149">Insert your fully qualified domain name (with a forward slash "/" appended to the end) between the double forward slashes and the GUID.</span></span> <span data-ttu-id="2beb6-150">整个 ID 的形式应为： `api://fully-qualified-domain-name.com/{AppID}` ²</span><span class="sxs-lookup"><span data-stu-id="2beb6-150">The entire ID should have the form of: `api://fully-qualified-domain-name.com/{AppID}` ²</span></span>
    * <span data-ttu-id="2beb6-151">例如： `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 。</span><span class="sxs-lookup"><span data-stu-id="2beb6-151">ex: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`.</span></span>
6. <span data-ttu-id="2beb6-152">选择“添加一个作用域”\*\*\*\* 按钮。</span><span class="sxs-lookup"><span data-stu-id="2beb6-152">Select the **Add a scope** button.</span></span> <span data-ttu-id="2beb6-153">在打开的面板中，输入 `access_as_user` 作为“作用域名称”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="2beb6-153">In the panel that opens, enter `access_as_user` as the **Scope name**.</span></span>
7. <span data-ttu-id="2beb6-154">设置**谁可以同意？** 若要`Admins and users`</span><span class="sxs-lookup"><span data-stu-id="2beb6-154">Set **Who can consent?** to `Admins and users`</span></span>
8. <span data-ttu-id="2beb6-155">填写用于配置管理员和用户同意提示的字段，其中包含适用于该范围的值 `access_as_user` ：</span><span class="sxs-lookup"><span data-stu-id="2beb6-155">Fill in the fields for configuring the admin and user consent prompts with values that are appropriate for the `access_as_user` scope:</span></span>
    * <span data-ttu-id="2beb6-156">**管理员同意职务：** 团队可以访问用户的配置文件。</span><span class="sxs-lookup"><span data-stu-id="2beb6-156">**Admin consent title:** Teams can access the user’s profile.</span></span>
    * <span data-ttu-id="2beb6-157">**管理员同意说明**：允许团队以当前用户的身份调用应用程序的 web api。</span><span class="sxs-lookup"><span data-stu-id="2beb6-157">**Admin consent description**: Allows Teams to call the app’s web APIs as the current user.</span></span>
    * <span data-ttu-id="2beb6-158">**用户同意标题**：团队可以访问用户配置文件，并代表用户发出请求。</span><span class="sxs-lookup"><span data-stu-id="2beb6-158">**User consent title**: Teams can access the user profile and make requests on the user's behalf.</span></span>
    * <span data-ttu-id="2beb6-159">**用户同意说明：** 使团队可以使用与用户相同的权限调用此应用的 Api。</span><span class="sxs-lookup"><span data-stu-id="2beb6-159">**User consent description:** Enable Teams to call this app’s APIs with the same rights as the user.</span></span>
9. <span data-ttu-id="2beb6-160">确保将 "**状态**" 设置为 "**已启用**"</span><span class="sxs-lookup"><span data-stu-id="2beb6-160">Ensure that **State** is set to **Enabled**</span></span>
10. <span data-ttu-id="2beb6-161">选择 "**添加范围**"</span><span class="sxs-lookup"><span data-stu-id="2beb6-161">Select **Add scope**</span></span>
    * <span data-ttu-id="2beb6-162">显示在文本字段正下方的**范围名称**的域部分应自动匹配上一步中设置的**应用程序 ID** URI，并 `/access_as_user` 追加到末尾：</span><span class="sxs-lookup"><span data-stu-id="2beb6-162">The domain part of the **Scope name** displayed just below the text field should automatically match the **Application ID** URI set in the previous step, with `/access_as_user` appended to the end:</span></span>
        * `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`
11. <span data-ttu-id="2beb6-163">在 "**授权客户端应用程序**" 部分中，确定要为您的应用程序的 web 应用程序授权的应用程序。</span><span class="sxs-lookup"><span data-stu-id="2beb6-163">In the **Authorized client applications** section, identify the applications that you want to authorize for your app’s web application.</span></span> <span data-ttu-id="2beb6-164">需要输入以下每个 Id：</span><span class="sxs-lookup"><span data-stu-id="2beb6-164">Each of the following IDs needs to be entered:</span></span>
    * <span data-ttu-id="2beb6-165">`1fec8e78-bce4-4aaf-ab1b-5451cc387264` (团队移动/桌面应用程序) </span><span class="sxs-lookup"><span data-stu-id="2beb6-165">`1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Teams mobile/desktop application)</span></span>
    * <span data-ttu-id="2beb6-166">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (团队 web 应用程序) </span><span class="sxs-lookup"><span data-stu-id="2beb6-166">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Teams web application)</span></span>
12. <span data-ttu-id="2beb6-167">导航到 " **API 权限**"，并确保添加 "关注" 权限：</span><span class="sxs-lookup"><span data-stu-id="2beb6-167">Navigate to **API Permissions**, and make sure to add the follow permissions:</span></span>
    * <span data-ttu-id="2beb6-168">默认情况下， (启用 Read) </span><span class="sxs-lookup"><span data-stu-id="2beb6-168">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="2beb6-169">email</span><span class="sxs-lookup"><span data-stu-id="2beb6-169">email</span></span>
    * <span data-ttu-id="2beb6-170">offline_access</span><span class="sxs-lookup"><span data-stu-id="2beb6-170">offline_access</span></span>
    * <span data-ttu-id="2beb6-171">OpenId</span><span class="sxs-lookup"><span data-stu-id="2beb6-171">OpenId</span></span>
    * <span data-ttu-id="2beb6-172">profile</span><span class="sxs-lookup"><span data-stu-id="2beb6-172">profile</span></span>

13. <span data-ttu-id="2beb6-173">导航到 "**身份验证**"</span><span class="sxs-lookup"><span data-stu-id="2beb6-173">Navigate to **Authentication**</span></span>

    <span data-ttu-id="2beb6-174">如果尚未向应用授予 IT 管理员同意，则用户在首次使用应用程序时必须提供许可。</span><span class="sxs-lookup"><span data-stu-id="2beb6-174">If an app hasn't been granted IT admin consent, users will have to provide consent the first time they use an app.</span></span>

    <span data-ttu-id="2beb6-175">设置重定向 URI：</span><span class="sxs-lookup"><span data-stu-id="2beb6-175">Set a redirect URI:</span></span>
    * <span data-ttu-id="2beb6-176">选择 "**添加平台**"。</span><span class="sxs-lookup"><span data-stu-id="2beb6-176">Select **Add a platform**.</span></span>
    * <span data-ttu-id="2beb6-177">选择 " **web**"。</span><span class="sxs-lookup"><span data-stu-id="2beb6-177">Select **web**.</span></span>
    * <span data-ttu-id="2beb6-178">输入您的应用程序的**重定向 URI** 。</span><span class="sxs-lookup"><span data-stu-id="2beb6-178">Enter the **redirect URI** for your app.</span></span> <span data-ttu-id="2beb6-179">这将是成功的隐式授予流将重定向到用户的页面。</span><span class="sxs-lookup"><span data-stu-id="2beb6-179">This will be the page where a successful implicit grant flow will redirect the user.</span></span>

    <span data-ttu-id="2beb6-180">通过选中以下框启用隐式授予：</span><span class="sxs-lookup"><span data-stu-id="2beb6-180">Enable implicit grant by checking the following boxes:</span></span>  
    <span data-ttu-id="2beb6-181">✔ ID 令牌</span><span class="sxs-lookup"><span data-stu-id="2beb6-181">✔ ID Token</span></span>  
    <span data-ttu-id="2beb6-182">✔访问令牌</span><span class="sxs-lookup"><span data-stu-id="2beb6-182">✔ Access Token</span></span>  
    
    

> [!NOTE]
>
> * <span data-ttu-id="2beb6-183">¹如果您的 Azure AD 应用注册到在团队中进行身份验证请求的_同一个_租户中，则不会要求用户同意并将立即被授予访问令牌。</span><span class="sxs-lookup"><span data-stu-id="2beb6-183">¹ If your Azure AD app is registered in the _same_ tenant where you're making an authentication request in Teams, the user won't be asked to consent and will be granted an access token right away.</span></span> <span data-ttu-id="2beb6-184">如果 Azure AD 应用在其他租户中注册，则用户只需同意这些权限。</span><span class="sxs-lookup"><span data-stu-id="2beb6-184">Users only need to consent to these permissions if the Azure AD app is registered in a different tenant.</span></span>
> * <span data-ttu-id="2beb6-185">²如果你收到一条错误，指出域已拥有且你是所有者，请按照[以下过程操作：将自定义域名添加到 Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain)以注册域，然后重复上面的步骤5。</span><span class="sxs-lookup"><span data-stu-id="2beb6-185">² If you get an error stating that the domain is already owned and you are the owner, follow the procedure at [Quickstart: Add a custom domain name to Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) to register the domain, and then repeat step 5, above.</span></span> <span data-ttu-id="2beb6-186"> (如果您未使用 Office 365 租赁) 中的管理员凭据登录，也会发生此错误。</span><span class="sxs-lookup"><span data-stu-id="2beb6-186">(This error can also occur if you aren't signed in with Admin credentials in the Office 365 tenancy).</span></span>
> * <span data-ttu-id="2beb6-187">如果未在返回的访问令牌中接收 UPN (用户主体名称) ，则可以将其作为 Azure AD 中的[可选声明](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims)进行添加。</span><span class="sxs-lookup"><span data-stu-id="2beb6-187">If you are not receiving the UPN (User Principal Name) in the returned access token, you can add it as an [optional claim](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) in Azure AD.</span></span>

### <a name="2-update-your-microsoft-teams-application-manifest"></a><span data-ttu-id="2beb6-188">2. 更新 Microsoft 团队应用程序清单</span><span class="sxs-lookup"><span data-stu-id="2beb6-188">2. Update your Microsoft Teams application manifest</span></span>

<span data-ttu-id="2beb6-189">将新属性添加到 Microsoft 团队清单：</span><span class="sxs-lookup"><span data-stu-id="2beb6-189">Add new properties to your Microsoft Teams manifest:</span></span>

* <span data-ttu-id="2beb6-190">**WebApplicationInfo** -以下元素的父元素：</span><span class="sxs-lookup"><span data-stu-id="2beb6-190">**WebApplicationInfo** - The parent of the following elements:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="2beb6-191">**id** -应用程序的客户端 id。</span><span class="sxs-lookup"><span data-stu-id="2beb6-191">**id** - The client ID of the application.</span></span> <span data-ttu-id="2beb6-192">这是您在向 Azure AD 注册应用程序的过程中获得的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="2beb6-192">This is the application ID that you obtained as part of registering the application with Azure AD.</span></span>
>* <span data-ttu-id="2beb6-193">**resource** -应用程序的域和子域。</span><span class="sxs-lookup"><span data-stu-id="2beb6-193">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="2beb6-194">此 URI (包括 `api://` 您在 `scope` 上面的步骤6中创建时注册的协议) 。</span><span class="sxs-lookup"><span data-stu-id="2beb6-194">This is the same URI (including the `api://` protocol) that you registered when creating your `scope` in step 6 above.</span></span> <span data-ttu-id="2beb6-195">您不应 `access_as_user` 在资源中包含该路径。</span><span class="sxs-lookup"><span data-stu-id="2beb6-195">You shouldn't include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="2beb6-196">此 URI 的域部分应与在团队应用程序清单的 Url 中使用的域（包括任何子域）相匹配。</span><span class="sxs-lookup"><span data-stu-id="2beb6-196">The domain part of this URI should match the domain, including any subdomains, used in the URLs of your Teams application manifest.</span></span>

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

> [!NOTE]
>
>* <span data-ttu-id="2beb6-197">AAD 应用的资源通常是其网站 URL 和 appID (（例如) ）的根 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` 。</span><span class="sxs-lookup"><span data-stu-id="2beb6-197">The resource for an AAD app will usually be the root of its site URL and the appID (e.g. `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`).</span></span> <span data-ttu-id="2beb6-198">我们还使用此值来确保你的请求来自同一个域。</span><span class="sxs-lookup"><span data-stu-id="2beb6-198">We also use this value to ensure your request is coming from the same domain.</span></span> <span data-ttu-id="2beb6-199">因此，请确保 `contentURL` 选项卡使用与资源属性相同的域。</span><span class="sxs-lookup"><span data-stu-id="2beb6-199">Therefore, make sure that the `contentURL` for your tab uses the same domains as your resource property.</span></span>
>* <span data-ttu-id="2beb6-200">您需要使用清单版本1.5 或更高版本来实现 `webApplicationInfo` 字段。</span><span class="sxs-lookup"><span data-stu-id="2beb6-200">You need to use manifest version 1.5 or higher to implement the `webApplicationInfo` field.</span></span>

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a><span data-ttu-id="2beb6-201">3. 从客户端代码中获取身份验证令牌</span><span class="sxs-lookup"><span data-stu-id="2beb6-201">3. Get an authentication token from your client-side code</span></span>

<span data-ttu-id="2beb6-202">身份验证 API 如下所示：</span><span class="sxs-lookup"><span data-stu-id="2beb6-202">Here's what the authentication API looks like:</span></span>

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); },
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

<span data-ttu-id="2beb6-203">当您 `getAuthToken` 需要拨打和额外的用户同意时 (对用户级权限) -我们将向用户显示一个对话框，让他们鼓励他们授予额外的同意。</span><span class="sxs-lookup"><span data-stu-id="2beb6-203">When you call `getAuthToken` - and additional user consent is required (for user-level permissions) - we will show a dialog to the user encouraging them to grant additional consent.</span></span> 

<span data-ttu-id="2beb6-204">收到成功回调中的访问令牌后，可以对访问令牌进行解码，以查看与该令牌关联的声明。</span><span class="sxs-lookup"><span data-stu-id="2beb6-204">Once you've received the access token in the success callback you can decode the access token to view the claims associated with that token.</span></span> <span data-ttu-id="2beb6-205"> (可以选择将访问令牌手动复制/粘贴到工具（如[JWT.io](https://jwt.io/) ），以检查其内容) 。</span><span class="sxs-lookup"><span data-stu-id="2beb6-205">(Optionally, you can manually copy/paste the access token into a tool such as [JWT.io](https://jwt.io/) to inspect its contents).</span></span> <span data-ttu-id="2beb6-206">如果未在返回的访问令牌中接收 UPN (用户主体名称) ，则可以将其作为 Azure AD 中的[可选声明](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims)进行添加。</span><span class="sxs-lookup"><span data-stu-id="2beb6-206">If you are not receiving the UPN (User Principal Name) in the returned access token, you can add it as an [optional claim](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) in Azure AD.</span></span>

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="sample-code"></a><span data-ttu-id="2beb6-207">示例代码</span><span class="sxs-lookup"><span data-stu-id="2beb6-207">Sample code</span></span>

<span data-ttu-id="2beb6-208">请访问我们的示例应用程序： [MSTeams 选项卡 SSO 示例-Nodejs](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs)</span><span class="sxs-lookup"><span data-stu-id="2beb6-208">Visit our sample application: [MSTeams Tabs SSO Sample - Nodejs](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs)</span></span>

<span data-ttu-id="2beb6-209">该自述文件介绍如何设置开发环境以及如何在 Azure AD 中配置应用程序。</span><span class="sxs-lookup"><span data-stu-id="2beb6-209">The README explains how to set up your development environment and how to configure your application in Azure AD.</span></span> <span data-ttu-id="2beb6-210">您还可以进一步了解如何在[应用程序结构部分](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs#app-structure)中对示例进行构造，以帮助熟悉基本代码。</span><span class="sxs-lookup"><span data-stu-id="2beb6-210">You can also find further information on how the sample is structured in the [app structure section](https://github.com/OfficeDev/msteams-tabs-sso-sample-nodejs#app-structure) to help familiarize yourself with the codebase.</span></span>

## <a name="known-limitations"></a><span data-ttu-id="2beb6-211">已知限制</span><span class="sxs-lookup"><span data-stu-id="2beb6-211">Known Limitations</span></span>

### <a name="apps-that-require-additional-microsoft-graph-scopes"></a><span data-ttu-id="2beb6-212">需要其他 Microsoft Graph 作用域的应用程序</span><span class="sxs-lookup"><span data-stu-id="2beb6-212">Apps that require additional Microsoft Graph Scopes</span></span>

<span data-ttu-id="2beb6-213">我们目前的 SSO 实施仅授予用户级权限（电子邮件、配置文件、offline_access、OpenId）的同意，而不是对其他 Api (（如 User. read) ）。</span><span class="sxs-lookup"><span data-stu-id="2beb6-213">Our current implementation for SSO only grants consent for user-level permissions — email, profile, offline_access, OpenId — not for other APIs (such as User.Read or Mail.Read).</span></span> <span data-ttu-id="2beb6-214">如果您的应用程序需要更多 Microsoft Graph 作用域，下面是一些启用解决方法：</span><span class="sxs-lookup"><span data-stu-id="2beb6-214">If your app needs further Microsoft Graph scopes, here are some enabling workarounds:</span></span>

#### <a name="tenant-admin-consent"></a><span data-ttu-id="2beb6-215">租户管理员同意</span><span class="sxs-lookup"><span data-stu-id="2beb6-215">Tenant Admin Consent</span></span>

<span data-ttu-id="2beb6-216">最简单的方法是让租户管理员代表组织进行预先同意。</span><span class="sxs-lookup"><span data-stu-id="2beb6-216">The simplest approach is to get a tenant admin to pre-consent on behalf of the organization.</span></span> <span data-ttu-id="2beb6-217">这意味着用户无需同意这些作用域，您就可以使用 Azure AD 的[代表流](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)来交换令牌服务器端。</span><span class="sxs-lookup"><span data-stu-id="2beb6-217">This means users won’t have to consent to these scopes and you can then be free to exchange the token server side using Azure AD’s [on-behalf-of flow](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow).</span></span> <span data-ttu-id="2beb6-218">这种解决方法对于内部业务线应用程序是可接受的，但对于可能无法依赖租户管理员批准的第三方开发人员来说可能不够。</span><span class="sxs-lookup"><span data-stu-id="2beb6-218">This workaround is acceptable for internal line-of-business applications but may not be enough for third-party developers who may not be able to rely on tenant admin approval.</span></span>

<span data-ttu-id="2beb6-219">同意代表组织 (作为租户管理员) 的简单方法是访问：</span><span class="sxs-lookup"><span data-stu-id="2beb6-219">A simple way of consenting on behalf of an organization (as a tenant admin) is to visit:</span></span>

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a><span data-ttu-id="2beb6-220">使用 Auth API 请求其他许可</span><span class="sxs-lookup"><span data-stu-id="2beb6-220">Asking for additional consent using the Auth API</span></span>

<span data-ttu-id="2beb6-221">获取其他 Microsoft Graph 作用域的另一种方法是，使用现有的[基于 web 的 AZURE ad 身份验证方法](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)呈现许可对话，这涉及弹出 Azure ad 同意对话框。</span><span class="sxs-lookup"><span data-stu-id="2beb6-221">Another approach for getting additional Microsoft Graph scopes is to present a consent dialog using our existing [web-based Azure AD authentication approach](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) which involves popping up an Azure AD consent dialog.</span></span> <span data-ttu-id="2beb6-222">有一些显著的添加：</span><span class="sxs-lookup"><span data-stu-id="2beb6-222">There are some notable additions:</span></span>

1. <span data-ttu-id="2beb6-223">`getAuthToken()`需要使用 AZURE AD[代表流](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)交换服务器端检索的令牌，以获取对这些额外 Microsoft Graph api 的访问权限。</span><span class="sxs-lookup"><span data-stu-id="2beb6-223">The token retrieved using `getAuthToken()` needs to be exchanged server-side using Azure AD [on-behalf-of flow](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) to get access to those additional Microsoft Graph APIs.</span></span>
    * <span data-ttu-id="2beb6-224">请务必将 v2 Microsoft Graph 终结点用于此 exchange</span><span class="sxs-lookup"><span data-stu-id="2beb6-224">Be sure to use the v2 Microsoft Graph endpoint for this exchange</span></span>
2. <span data-ttu-id="2beb6-225">如果 exchange 发生故障，Azure AD 将返回无效的授予异常。</span><span class="sxs-lookup"><span data-stu-id="2beb6-225">If the exchange fails, Azure AD will return an invalid grant exception.</span></span> <span data-ttu-id="2beb6-226">通常有以下两种错误消息 `invalid_grant` 之一：`interaction_required`</span><span class="sxs-lookup"><span data-stu-id="2beb6-226">There are usually one of two error messages: `invalid_grant` or `interaction_required`</span></span>
3. <span data-ttu-id="2beb6-227">当 exchange 发生故障时，您需要请求其他许可。</span><span class="sxs-lookup"><span data-stu-id="2beb6-227">When the exchange fails, then you need to ask for additional consent.</span></span> <span data-ttu-id="2beb6-228">建议显示一些 UI，要求用户授予更多许可。</span><span class="sxs-lookup"><span data-stu-id="2beb6-228">We recommend showing some UI asking the user to grant additional consent.</span></span> <span data-ttu-id="2beb6-229">此 UI 应包括使用我们的[AZURE ad 身份验证 API](~/concepts/authentication/auth-silent-aad.md)触发 azure ad 许可对话的按钮。</span><span class="sxs-lookup"><span data-stu-id="2beb6-229">This UI should include a button that triggers an Azure AD consent dialog using our [Azure AD authentication API](~/concepts/authentication/auth-silent-aad.md).</span></span>
4. <span data-ttu-id="2beb6-230">当询问 Azure AD 的其他许可时，您需要将 `prompt=consent` [查询字符串参数](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context)包括在 azure ad 中，否则 azure ad 将不会要求提供其他作用域。</span><span class="sxs-lookup"><span data-stu-id="2beb6-230">When asking for additional consent from Azure AD, you need to include `prompt=consent` in your [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) to Azure AD otherwise Azure AD will not ask for the additional scopes.</span></span>
    * <span data-ttu-id="2beb6-231">而不是：`?scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="2beb6-231">Instead of: `?scope={scopes}`</span></span>
    * <span data-ttu-id="2beb6-232">使用以下命令：`?prompt=consent&scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="2beb6-232">Use this: `?prompt=consent&scope={scopes}`</span></span>
    * <span data-ttu-id="2beb6-233">请确保 `{scopes}` 包含要提示用户的所有作用域 (例如： Mail. read) 。</span><span class="sxs-lookup"><span data-stu-id="2beb6-233">Be sure that `{scopes}` includes all the scopes you are prompting the user for (ex: Mail.Read or User.Read).</span></span>
5. <span data-ttu-id="2beb6-234">一旦用户授予了其他权限，则重试代表流，以获取对这些附加 Api 的访问权限。</span><span class="sxs-lookup"><span data-stu-id="2beb6-234">Once the user has granted additional permission, retry the on-behalf-of-flow to get access to these additional APIs.</span></span>

### <a name="non-azure-ad-authentication"></a><span data-ttu-id="2beb6-235">非 Azure AD 身份验证</span><span class="sxs-lookup"><span data-stu-id="2beb6-235">Non-Azure AD Authentication</span></span>

<span data-ttu-id="2beb6-236">以上所述的身份验证解决方案仅适用于支持 Azure AD 作为标识提供程序的应用程序和服务。</span><span class="sxs-lookup"><span data-stu-id="2beb6-236">The above-described authentication solution only works for apps and services that support Azure AD as an identity provider.</span></span> <span data-ttu-id="2beb6-237">要使用基于非 Azure AD 的服务进行身份验证的应用程序需要继续使用基于弹出窗口的[web 身份验证流](~/concepts/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="2beb6-237">Apps that want to authenticate using non-Azure AD based services need to continue using the pop-up-based [web authentication flow](~/concepts/authentication.md).</span></span>
