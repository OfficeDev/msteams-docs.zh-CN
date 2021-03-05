---
title: 选项卡的单一登录支持
description: '描述 SSO (单一) '
ms.topic: how-to
keywords: teams 身份验证 SSO AAD 单一登录 api
ms.openlocfilehash: 7b8406473b8356b9c26948641b49f7e1239e697a
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449260"
---
# <a name="single-sign-on-sso-support-for-tabs"></a><span data-ttu-id="58a94-104">单一登录 (SSO) 选项卡支持</span><span class="sxs-lookup"><span data-stu-id="58a94-104">Single sign-on (SSO) support for tabs</span></span>

<span data-ttu-id="58a94-105">用户通过工作、学校或 Microsoft 帐户登录 Microsoft Teams (Office 365、Outlook 等) 。</span><span class="sxs-lookup"><span data-stu-id="58a94-105">Users sign in to Microsoft Teams via their work, school, or Microsoft accounts (Office 365, Outlook, etc).</span></span> <span data-ttu-id="58a94-106">你可以利用这一点，允许单一登录在桌面或移动客户端上 (Microsoft Teams 选项卡) 或任务模块。</span><span class="sxs-lookup"><span data-stu-id="58a94-106">You can take advantage of this by allowing a single sign-on to authorize your Microsoft Teams tab (or task module) on desktop or mobile clients.</span></span> <span data-ttu-id="58a94-107">因此，如果用户同意使用你的应用，则他们不需要在另一台设备上再次同意，他们将自动登录。</span><span class="sxs-lookup"><span data-stu-id="58a94-107">Thus, if a user consents to use your app, they won’t have to consent again on another device — they will be signed in automatically.</span></span> <span data-ttu-id="58a94-108">此外，我们会预取访问令牌以提高性能和加载时间。</span><span class="sxs-lookup"><span data-stu-id="58a94-108">In addition, we prefetch your access token to improve performance and load times.</span></span>

> [!NOTE]
> <span data-ttu-id="58a94-109">**支持 SSO 的 Teams 移动客户端版本**</span><span class="sxs-lookup"><span data-stu-id="58a94-109">**Teams mobile client versions supporting SSO**</span></span>  
>
> <span data-ttu-id="58a94-110">✔ Android (1416/1.0.0.2020073101 及更高版本) </span><span class="sxs-lookup"><span data-stu-id="58a94-110">✔Teams for Android (1416/1.0.0.2020073101 and later)</span></span>
>
> <span data-ttu-id="58a94-111">✔ iOS (_版本_：2.0.18 及更高版本) </span><span class="sxs-lookup"><span data-stu-id="58a94-111">✔Teams for iOS (_Version_: 2.0.18 and later)</span></span>  
>
> <span data-ttu-id="58a94-112">为了获得最佳 Teams 体验，请使用最新版本的 iOS 和 Android。</span><span class="sxs-lookup"><span data-stu-id="58a94-112">For the best experience with Teams, please use the latest version of iOS and Android.</span></span>

> [!NOTE]
> <span data-ttu-id="58a94-113">**快速入门**</span><span class="sxs-lookup"><span data-stu-id="58a94-113">**Quickstart**</span></span>  
>
> <span data-ttu-id="58a94-114">开始使用选项卡 SSO 的最简单路径是 Microsoft Teams Toolkit for Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="58a94-114">The simplest path to getting started with tab SSO is with the Microsoft Teams Toolkit for Visual Studio Code.</span></span> [<span data-ttu-id="58a94-115">了解更多</span><span class="sxs-lookup"><span data-stu-id="58a94-115">Learn more</span></span>](../../../toolkit/visual-studio-code-tab-sso.md)

## <a name="how-sso-works-at-runtime"></a><span data-ttu-id="58a94-116">运行时 SSO 的工作方式</span><span class="sxs-lookup"><span data-stu-id="58a94-116">How SSO works at runtime</span></span>

<span data-ttu-id="58a94-117">下图显示了 SSO 过程的工作原理：</span><span class="sxs-lookup"><span data-stu-id="58a94-117">The following diagram shows how the SSO process works:</span></span>

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. <span data-ttu-id="58a94-118">在选项卡中，对进行 JavaScript 调用 `getAuthToken()` 。</span><span class="sxs-lookup"><span data-stu-id="58a94-118">In the tab, a JavaScript call is made to `getAuthToken()`.</span></span> <span data-ttu-id="58a94-119">这将告知 Teams 获取选项卡应用程序的身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="58a94-119">This tells Teams to obtain an authentication token for the tab application.</span></span>
2. <span data-ttu-id="58a94-120">如果这是当前用户第一次使用选项卡应用程序，则当需要) 同意或处理双重身份验证 (如双重身份验证) 时，系统将会提示同意 (。</span><span class="sxs-lookup"><span data-stu-id="58a94-120">If this is the first time the current user has used your tab application, there will be a request prompt to consent (if consent is required) or to handle step-up authentication (such as two-factor authentication).</span></span>
3. <span data-ttu-id="58a94-121">Teams 从 Azure AD 终结点为当前用户请求选项卡应用程序令牌。</span><span class="sxs-lookup"><span data-stu-id="58a94-121">Teams requests the tab application token from the Azure AD endpoint for the current user.</span></span>
4. <span data-ttu-id="58a94-122">Azure AD 将选项卡应用程序令牌发送到 Teams 应用程序。</span><span class="sxs-lookup"><span data-stu-id="58a94-122">Azure AD sends the tab application token to the Teams application.</span></span>
5. <span data-ttu-id="58a94-123">Teams 将选项卡应用程序令牌作为调用返回的结果对象的一 `getAuthToken()` 部分发送到选项卡。</span><span class="sxs-lookup"><span data-stu-id="58a94-123">Teams sends the tab application token to the tab as part of the result object returned by the `getAuthToken()` call.</span></span>
6. <span data-ttu-id="58a94-124">令牌将在选项卡应用程序中通过 JavaScript 进行分析，以提取所需信息，如用户的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="58a94-124">The token will be parsed in the tab application, via JavaScript, to extract the needed information, such as the user's email address.</span></span>

> [!NOTE]
> <span data-ttu-id="58a94-125">仅对同意一组有限的用户级 API（电子邮件、配置文件、offline_access 和 OpenId）有效，对进一步 Microsoft Graph 范围（如 `getAuthToken()` `User.Read` 或）无效 `Mail.Read` 。</span><span class="sxs-lookup"><span data-stu-id="58a94-125">The `getAuthToken()` is only valid for consenting to a limited set of user-level APIs — email, profile, offline_access and OpenId — and not for further Microsoft Graph scopes such as `User.Read` or `Mail.Read`.</span></span> <span data-ttu-id="58a94-126">如果需要其他 Graph 范围，请参阅本文档末尾的部分，了解建议的 [解决方法](#apps-that-require-additional-microsoft-graph-scopes)。</span><span class="sxs-lookup"><span data-stu-id="58a94-126">See our section at the end of this document for suggested workarounds if you require [additional Graph scopes](#apps-that-require-additional-microsoft-graph-scopes).</span></span>

<span data-ttu-id="58a94-127">SSO API 还将 [在嵌入](../../../task-modules-and-cards/what-are-task-modules.md) Web 内容的任务模块中工作。</span><span class="sxs-lookup"><span data-stu-id="58a94-127">The SSO API will also work in [Task Modules](../../../task-modules-and-cards/what-are-task-modules.md) that embed web content.</span></span>

## <a name="develop-an-sso-microsoft-teams-tab"></a><span data-ttu-id="58a94-128">开发 SSO Microsoft Teams 选项卡</span><span class="sxs-lookup"><span data-stu-id="58a94-128">Develop an SSO Microsoft Teams tab</span></span>

<span data-ttu-id="58a94-129">本节介绍创建使用 SSO 的 Teams 选项卡所涉及的任务。</span><span class="sxs-lookup"><span data-stu-id="58a94-129">This section describes the tasks involved in creating a Teams tab that uses SSO.</span></span> <span data-ttu-id="58a94-130">此处介绍的这些任务与语言和框架无关。</span><span class="sxs-lookup"><span data-stu-id="58a94-130">These tasks are described here are language- and framework-agnostic.</span></span>

### <a name="1-create-your-azure-active-directory-azure-ad-application"></a><span data-ttu-id="58a94-131">1. 创建 Azure Active Directory (Azure AD) 应用程序</span><span class="sxs-lookup"><span data-stu-id="58a94-131">1. Create your Azure Active Directory (Azure AD) application</span></span>

#### <a name="registering-your-application-in-theazure-ad-portal-overview"></a><span data-ttu-id="58a94-132">在[Azure AD](https://azure.microsoft.com/features/azure-portal/) 门户中注册应用程序概述：</span><span class="sxs-lookup"><span data-stu-id="58a94-132">Registering your application in the[Azure AD portal](https://azure.microsoft.com/features/azure-portal/) overview:</span></span>

1. <span data-ttu-id="58a94-133">获取[Azure AD 应用程序 ID。](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)</span><span class="sxs-lookup"><span data-stu-id="58a94-133">Get your [Azure AD Application ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).</span></span>
2. <span data-ttu-id="58a94-134">指定应用程序对 Azure AD 终结点和（可选）Microsoft Graph 所需的权限。</span><span class="sxs-lookup"><span data-stu-id="58a94-134">Specify the permissions that your application needs for the Azure AD endpoint and, optionally, Microsoft Graph.</span></span>
3. <span data-ttu-id="58a94-135">[授予 Teams](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) 桌面、Web 和移动应用程序的权限。</span><span class="sxs-lookup"><span data-stu-id="58a94-135">[Grant permissions](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) for Teams desktop, web, and mobile applications.</span></span>
4. <span data-ttu-id="58a94-136">通过选择"添加范围 **"** 按钮预授权 Teams，在打开的面板中输入 `access_as_user` 为范围 **名称**。</span><span class="sxs-lookup"><span data-stu-id="58a94-136">Pre-authorize Teams by selecting the **Add a scope** button and in the panel that opens, enter `access_as_user` as the **Scope name**.</span></span>

> [!NOTE]
> <span data-ttu-id="58a94-137">应注意一些重要限制：</span><span class="sxs-lookup"><span data-stu-id="58a94-137">There are some important restrictions you should be aware of:</span></span>
>
> * <span data-ttu-id="58a94-138">我们仅支持用户级别的 Microsoft Graph API 权限，例如电子邮件、配置文件、offline_access、OpenId。</span><span class="sxs-lookup"><span data-stu-id="58a94-138">We only support user-level Microsoft Graph API permissions, i.e., email, profile, offline_access, OpenId.</span></span> <span data-ttu-id="58a94-139">如果需要访问其他 Microsoft Graph 作用域 (或) ，请参阅本文档末尾 `User.Read` `Mail.Read` 的推荐解决方法。 [](#apps-that-require-additional-microsoft-graph-scopes)</span><span class="sxs-lookup"><span data-stu-id="58a94-139">If you need access to other Microsoft Graph scopes (such as `User.Read` or `Mail.Read`), see our [recommended workaround](#apps-that-require-additional-microsoft-graph-scopes) at the end of this documentation.</span></span>
> * <span data-ttu-id="58a94-140">应用程序的域名与为 Azure AD 应用程序注册的域名相同，这一点很重要。</span><span class="sxs-lookup"><span data-stu-id="58a94-140">It's important that your application's domain name is the same as the domain name you've registering for your Azure AD application.</span></span>
> * <span data-ttu-id="58a94-141">我们当前不支持每个应用多个域。</span><span class="sxs-lookup"><span data-stu-id="58a94-141">We don't currently support multiple domains per app.</span></span>
> * <span data-ttu-id="58a94-142">我们不支持使用该域的应用程序，因为它太常见， `azurewebsites.net` 并且可能是一种安全风险。</span><span class="sxs-lookup"><span data-stu-id="58a94-142">We don't support applications that use the `azurewebsites.net` domain because it is too common and may be a security risk.</span></span> <span data-ttu-id="58a94-143">但是，我们正在积极寻求删除此限制。</span><span class="sxs-lookup"><span data-stu-id="58a94-143">However, we're actively seeking to remove this restriction.</span></span>

#### <a name="registering-your-app-through-the-azure-active-directory-portal-in-depth"></a><span data-ttu-id="58a94-144">通过 Azure Active Directory 门户进行深入注册应用：</span><span class="sxs-lookup"><span data-stu-id="58a94-144">Registering your app through the Azure Active Directory portal in-depth:</span></span>

1. <span data-ttu-id="58a94-145">在 Azure Active [Directory – 应用注册门户中注册新](https://go.microsoft.com/fwlink/?linkid=2083908) 应用程序。</span><span class="sxs-lookup"><span data-stu-id="58a94-145">Register a new application in the [Azure Active Directory – App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
2. <span data-ttu-id="58a94-146">选择 **"新建注册** "，在 *注册应用程序页上*，设置以下值：</span><span class="sxs-lookup"><span data-stu-id="58a94-146">Select **New Registration** and on the *register an application page*, set following values:</span></span>
    * <span data-ttu-id="58a94-147">将 **名称** 设置为应用名称。</span><span class="sxs-lookup"><span data-stu-id="58a94-147">Set **name** to your app name.</span></span>
    * <span data-ttu-id="58a94-148">选择 **支持的帐户类型 (** 任何帐户类型都将在) 中工作</span><span class="sxs-lookup"><span data-stu-id="58a94-148">Choose the **supported account types** (any account type will work) ¹</span></span>
    * <span data-ttu-id="58a94-149">保留“重定向 URI”为空。</span><span class="sxs-lookup"><span data-stu-id="58a94-149">Leave **Redirect URI** empty.</span></span>
    * <span data-ttu-id="58a94-150">选择“注册”。</span><span class="sxs-lookup"><span data-stu-id="58a94-150">Choose **Register**.</span></span>
3. <span data-ttu-id="58a94-151">在概述页上，复制并保存应用程序 (**客户端) ID。**</span><span class="sxs-lookup"><span data-stu-id="58a94-151">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="58a94-152">稍后更新 Teams 应用程序清单时将需要它。</span><span class="sxs-lookup"><span data-stu-id="58a94-152">You’ll need it later when updating your Teams application manifest.</span></span>
4. <span data-ttu-id="58a94-153">在“**管理**”下，选择“**公开 API**”。</span><span class="sxs-lookup"><span data-stu-id="58a94-153">Under **Manage**, select **Expose an API**.</span></span> 
5. <span data-ttu-id="58a94-154">选择 **"设置** "链接以生成应用程序 ID URI，格式为 `api://{AppID}` 。</span><span class="sxs-lookup"><span data-stu-id="58a94-154">Select the **Set** link to generate the Application ID URI in the form of `api://{AppID}`.</span></span> <span data-ttu-id="58a94-155">插入完全限定域名 (双正斜杠和 GUID 之间的) 后斜杠"/"。</span><span class="sxs-lookup"><span data-stu-id="58a94-155">Insert your fully qualified domain name (with a forward slash "/" appended to the end) between the double forward slashes and the GUID.</span></span> <span data-ttu-id="58a94-156">整个 ID 的形式 `api://fully-qualified-domain-name.com/{AppID}` 应为：</span><span class="sxs-lookup"><span data-stu-id="58a94-156">The entire ID should have the form of: `api://fully-qualified-domain-name.com/{AppID}` ²</span></span>
    * <span data-ttu-id="58a94-157">例如： `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` .</span><span class="sxs-lookup"><span data-stu-id="58a94-157">ex: `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`.</span></span>
    
    <span data-ttu-id="58a94-158">完全限定的域名是提供你的应用的人工可读域名。</span><span class="sxs-lookup"><span data-stu-id="58a94-158">The fully qualified domain name is the human readable domain name from which your app is served.</span></span> <span data-ttu-id="58a94-159">如果使用的是隧道服务（如 ngrok），则需要在 ngrok 子域发生更改时更新此值。</span><span class="sxs-lookup"><span data-stu-id="58a94-159">If you are using a tunneling service such as ngrok, you will need to update     this value whenever your ngrok subdomain changes.</span></span> 
6. <span data-ttu-id="58a94-160">选择“添加一个作用域”按钮。</span><span class="sxs-lookup"><span data-stu-id="58a94-160">Select the **Add a scope** button.</span></span> <span data-ttu-id="58a94-161">在打开的面板中，输入 `access_as_user` 作为“作用域名称”。</span><span class="sxs-lookup"><span data-stu-id="58a94-161">In the panel that opens, enter `access_as_user` as the **Scope name**.</span></span>
7. <span data-ttu-id="58a94-162">设置 **谁可以同意？**`Admins and users`</span><span class="sxs-lookup"><span data-stu-id="58a94-162">Set **Who can consent?** to `Admins and users`</span></span>
8. <span data-ttu-id="58a94-163">使用适用于作用域的值填写用于配置管理员和用户同意提示的 `access_as_user` 字段：</span><span class="sxs-lookup"><span data-stu-id="58a94-163">Fill in the fields for configuring the admin and user consent prompts with values that are appropriate for the `access_as_user` scope:</span></span>
    * <span data-ttu-id="58a94-164">**管理员同意标题：** Teams 可以访问用户配置文件。</span><span class="sxs-lookup"><span data-stu-id="58a94-164">**Admin consent title:** Teams can access the user’s profile.</span></span>
    * <span data-ttu-id="58a94-165">**管理员同意说明**：允许 Teams 以当前用户模式调用应用的 Web API。</span><span class="sxs-lookup"><span data-stu-id="58a94-165">**Admin consent description**: Allows Teams to call the app’s web APIs as the current user.</span></span>
    * <span data-ttu-id="58a94-166">**用户同意标题**：Teams 可以访问用户配置文件并代表用户提出请求。</span><span class="sxs-lookup"><span data-stu-id="58a94-166">**User consent title**: Teams can access the user profile and make requests on the user's behalf.</span></span>
    * <span data-ttu-id="58a94-167">**用户同意说明：** 允许 Teams 使用与用户相同的权限调用此应用的 API。</span><span class="sxs-lookup"><span data-stu-id="58a94-167">**User consent description:** Enable Teams to call this app’s APIs with the same rights as the user.</span></span>
9. <span data-ttu-id="58a94-168">确保 **状态** 设置为 **"已启用"**</span><span class="sxs-lookup"><span data-stu-id="58a94-168">Ensure that **State** is set to **Enabled**</span></span>
10. <span data-ttu-id="58a94-169">选择要 **保存的"添加范围** "按钮</span><span class="sxs-lookup"><span data-stu-id="58a94-169">Select the **Add scope** button to save</span></span> 
    * <span data-ttu-id="58a94-170">文本字段正下方显示的作用域名称的域部分应自动匹配上一步中设置的应用程序 **ID** URI，并追加 `/access_as_user` 到末尾：</span><span class="sxs-lookup"><span data-stu-id="58a94-170">The domain part of the **Scope name** displayed just below the text field should automatically match the **Application ID** URI set in the previous step, with `/access_as_user` appended to the end:</span></span>
        * `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`
11. <span data-ttu-id="58a94-171">在 **"授权客户端应用程序** "部分中，标识要针对应用的 Web 应用程序授权的应用程序。</span><span class="sxs-lookup"><span data-stu-id="58a94-171">In the **Authorized client applications** section, identify the applications that you want to authorize for your app’s web application.</span></span> <span data-ttu-id="58a94-172">选择 *"添加客户端应用程序"。*</span><span class="sxs-lookup"><span data-stu-id="58a94-172">Select *Add a client application*.</span></span> <span data-ttu-id="58a94-173">输入以下每个客户端 ID，然后选择在上一步中创建的授权作用域：</span><span class="sxs-lookup"><span data-stu-id="58a94-173">Enter each of the following client IDs and select the authorized scope you created in the previous step:</span></span>
    * <span data-ttu-id="58a94-174">`1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Teams 移动/桌面应用程序) </span><span class="sxs-lookup"><span data-stu-id="58a94-174">`1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Teams mobile/desktop application)</span></span>
    * <span data-ttu-id="58a94-175">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Teams Web 应用程序) </span><span class="sxs-lookup"><span data-stu-id="58a94-175">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Teams web application)</span></span>
12. <span data-ttu-id="58a94-176">导航到 **API 权限**。</span><span class="sxs-lookup"><span data-stu-id="58a94-176">Navigate to **API Permissions**.</span></span> <span data-ttu-id="58a94-177">选择 *"添加* Microsoft Graph 委派权限"权限，然后从 Microsoft Graph API 添加  >    >  以下权限：</span><span class="sxs-lookup"><span data-stu-id="58a94-177">Select *Add a permission* > *Microsoft Graph* > *Delegated permissions*, then add the following permissions from Microsoft Graph API:</span></span>
    * <span data-ttu-id="58a94-178">默认情况下， (User.Read) </span><span class="sxs-lookup"><span data-stu-id="58a94-178">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="58a94-179">电子邮件</span><span class="sxs-lookup"><span data-stu-id="58a94-179">email</span></span>
    * <span data-ttu-id="58a94-180">offline_access</span><span class="sxs-lookup"><span data-stu-id="58a94-180">offline_access</span></span>
    * <span data-ttu-id="58a94-181">OpenId</span><span class="sxs-lookup"><span data-stu-id="58a94-181">OpenId</span></span>
    * <span data-ttu-id="58a94-182">个人资料</span><span class="sxs-lookup"><span data-stu-id="58a94-182">profile</span></span>

13. <span data-ttu-id="58a94-183">导航到 **身份验证**</span><span class="sxs-lookup"><span data-stu-id="58a94-183">Navigate to **Authentication**</span></span>

    <span data-ttu-id="58a94-184">如果应用尚未获得 IT 管理员同意，则用户第一次使用应用时必须给予同意。</span><span class="sxs-lookup"><span data-stu-id="58a94-184">If an app hasn't been granted IT admin consent, users will have to provide consent the first time they use an app.</span></span>

    <span data-ttu-id="58a94-185">设置重定向 URI：</span><span class="sxs-lookup"><span data-stu-id="58a94-185">Set a redirect URI:</span></span>
    * <span data-ttu-id="58a94-186">选择 **"添加平台"。**</span><span class="sxs-lookup"><span data-stu-id="58a94-186">Select **Add a platform**.</span></span>
    * <span data-ttu-id="58a94-187">选择 **Web**。</span><span class="sxs-lookup"><span data-stu-id="58a94-187">Select **web**.</span></span>
    * <span data-ttu-id="58a94-188">输入 **应用的重定向 URI。**</span><span class="sxs-lookup"><span data-stu-id="58a94-188">Enter the **redirect URI** for your app.</span></span> <span data-ttu-id="58a94-189">这是一个页面，其中成功的隐式授予流将重定向用户。</span><span class="sxs-lookup"><span data-stu-id="58a94-189">This will be the page where a successful implicit grant flow will redirect the user.</span></span> <span data-ttu-id="58a94-190">这将是在步骤 5 中输入的完全限定域名，后跟应发送身份验证响应的 API 路由。</span><span class="sxs-lookup"><span data-stu-id="58a94-190">This will be same fully qualified domain name that you entered in step 5 followed by the API route where a authentication response should be sent.</span></span> <span data-ttu-id="58a94-191">如果你正在遵循任何 Teams 示例，这将是： `https://subdomain.example.com/auth-end`</span><span class="sxs-lookup"><span data-stu-id="58a94-191">If you are following any of the Teams samples, this will be: `https://subdomain.example.com/auth-end`</span></span>

    <span data-ttu-id="58a94-192">接下来，通过选中以下框启用隐式授予：</span><span class="sxs-lookup"><span data-stu-id="58a94-192">Next, enable implicit grant by checking the following boxes:</span></span>  
    <span data-ttu-id="58a94-193">✔ ID 令牌</span><span class="sxs-lookup"><span data-stu-id="58a94-193">✔ ID Token</span></span>  
    <span data-ttu-id="58a94-194">✔访问令牌</span><span class="sxs-lookup"><span data-stu-id="58a94-194">✔ Access Token</span></span>  
    
<span data-ttu-id="58a94-195">恭喜！</span><span class="sxs-lookup"><span data-stu-id="58a94-195">Congratulations!</span></span> <span data-ttu-id="58a94-196">你已完成应用注册先决条件以继续你的选项卡 SSO 应用。</span><span class="sxs-lookup"><span data-stu-id="58a94-196">You have completed the app registration prerequisites to proceed with your tab SSO app.</span></span>     

> [!NOTE]
>
> * <span data-ttu-id="58a94-197">1 如果你的 Azure AD 应用在 Teams 中进行身份验证请求的同一租户中注册，将不会要求用户同意，并且会马上获得访问令牌。</span><span class="sxs-lookup"><span data-stu-id="58a94-197">¹ If your Azure AD app is registered in the _same_ tenant where you're making an authentication request in Teams, the user won't be asked to consent and will be granted an access token right away.</span></span> <span data-ttu-id="58a94-198">如果用户在不同的租户中注册 Azure AD 应用，则只需同意这些权限。</span><span class="sxs-lookup"><span data-stu-id="58a94-198">Users only need to consent to these permissions if the Azure AD app is registered in a different tenant.</span></span>
> * <span data-ttu-id="58a94-199">1 如果收到错误，指出域已拥有并且你是所有者，请按照快速入门中的过程操作：将自定义域名添加到 [Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) 以注册域，然后重复上述步骤 5。</span><span class="sxs-lookup"><span data-stu-id="58a94-199">² If you get an error stating that the domain is already owned and you are the owner, follow the procedure at [Quickstart: Add a custom domain name to Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) to register the domain, and then repeat step 5, above.</span></span> <span data-ttu-id="58a94-200"> (如果未使用 Office 365 租户租户中的管理员凭据登录，也会) 。</span><span class="sxs-lookup"><span data-stu-id="58a94-200">(This error can also occur if you aren't signed in with Admin credentials in the Office 365 tenancy).</span></span>
> * <span data-ttu-id="58a94-201">如果未在返回的访问令牌 (UPN) 用户主体名称，可以在 Azure AD 中将其添加为可选声明。 [](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims)</span><span class="sxs-lookup"><span data-stu-id="58a94-201">If you are not receiving the UPN (User Principal Name) in the returned access token, you can add it as an [optional claim](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) in Azure AD.</span></span>

### <a name="2-update-your-microsoft-teams-application-manifest"></a><span data-ttu-id="58a94-202">2. 更新 Microsoft Teams 应用程序清单</span><span class="sxs-lookup"><span data-stu-id="58a94-202">2. Update your Microsoft Teams application manifest</span></span>

<span data-ttu-id="58a94-203">将新属性添加到 Microsoft Teams 清单：</span><span class="sxs-lookup"><span data-stu-id="58a94-203">Add new properties to your Microsoft Teams manifest:</span></span>

* <span data-ttu-id="58a94-204">**WebApplicationInfo** - 以下元素的父元素：</span><span class="sxs-lookup"><span data-stu-id="58a94-204">**WebApplicationInfo** - The parent of the following elements:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="58a94-205">**id** - 应用程序的客户端 ID。</span><span class="sxs-lookup"><span data-stu-id="58a94-205">**id** - The client ID of the application.</span></span> <span data-ttu-id="58a94-206">这是在向 Azure AD 注册应用程序时获取的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="58a94-206">This is the application ID that you obtained as part of registering the application with Azure AD.</span></span>
>* <span data-ttu-id="58a94-207">**resource** - 应用程序的域和子域。</span><span class="sxs-lookup"><span data-stu-id="58a94-207">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="58a94-208">这是相同的 URI (，包括) 步骤 6 中创建时注册 `api://` `scope` 的协议。</span><span class="sxs-lookup"><span data-stu-id="58a94-208">This is the same URI (including the `api://` protocol) that you registered when creating your `scope` in step 6 above.</span></span> <span data-ttu-id="58a94-209">不应在资源 `access_as_user` 中包括路径。</span><span class="sxs-lookup"><span data-stu-id="58a94-209">You shouldn't include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="58a94-210">此 URI 的域部分应匹配 Teams 应用程序清单的 URL 中使用的域（包括任何子域）。</span><span class="sxs-lookup"><span data-stu-id="58a94-210">The domain part of this URI should match the domain, including any subdomains, used in the URLs of your Teams application manifest.</span></span>

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

> [!NOTE]
>
>* <span data-ttu-id="58a94-211">AAD 应用的资源通常是其网站 URL 和 appID (的根，例如 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`) 。</span><span class="sxs-lookup"><span data-stu-id="58a94-211">The resource for an AAD app will usually be the root of its site URL and the appID (e.g. `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`).</span></span> <span data-ttu-id="58a94-212">我们还使用此值来确保你的请求来自同一个域。</span><span class="sxs-lookup"><span data-stu-id="58a94-212">We also use this value to ensure your request is coming from the same domain.</span></span> <span data-ttu-id="58a94-213">因此，请确保选项卡的域 `contentURL` 与资源属性使用相同的域。</span><span class="sxs-lookup"><span data-stu-id="58a94-213">Therefore, make sure that the `contentURL` for your tab uses the same domains as your resource property.</span></span>
>* <span data-ttu-id="58a94-214">您需要使用清单版本 1.5 或更高版本来实现 `webApplicationInfo` 该字段。</span><span class="sxs-lookup"><span data-stu-id="58a94-214">You need to use manifest version 1.5 or higher to implement the `webApplicationInfo` field.</span></span>

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a><span data-ttu-id="58a94-215">3. 从客户端代码获取身份验证令牌</span><span class="sxs-lookup"><span data-stu-id="58a94-215">3. Get an authentication token from your client-side code</span></span>

<span data-ttu-id="58a94-216">下面是身份验证 API 的外观：</span><span class="sxs-lookup"><span data-stu-id="58a94-216">Here's what the authentication API looks like:</span></span>

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

<span data-ttu-id="58a94-217">当你呼叫用户级别权限 (需要其他用户同意时) 我们将向用户显示一个对话框，鼓励他们授予 `getAuthToken` 其他同意。</span><span class="sxs-lookup"><span data-stu-id="58a94-217">When you call `getAuthToken` - and additional user consent is required (for user-level permissions) - we will show a dialog to the user encouraging them to grant additional consent.</span></span> 

<span data-ttu-id="58a94-218">在成功回调中收到访问令牌后，可以解码访问令牌以查看与该令牌关联的声明。</span><span class="sxs-lookup"><span data-stu-id="58a94-218">After you receive the access token in the success callback, you can decode the access token to view the claims associated with that token.</span></span> <span data-ttu-id="58a94-219">（可选）你可以手动将访问令牌复制并粘贴到工具中，jwt.ms检查其内容。 [](https://jwt.ms/)</span><span class="sxs-lookup"><span data-stu-id="58a94-219">Optionally, you can manually copy and paste the access token into a tool, such as [jwt.ms](https://jwt.ms/) to inspect its contents.</span></span> <span data-ttu-id="58a94-220">如果未在返回的访问令牌中 (UPN) 用户主体名称，可以在 Azure AD 中将其添加为可选声明。 [](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims)</span><span class="sxs-lookup"><span data-stu-id="58a94-220">If you are not receiving the User Principal Name (UPN) in the returned access token, you can add it as an [optional claim](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) in Azure AD.</span></span>

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-sample"></a><span data-ttu-id="58a94-221">代码示例</span><span class="sxs-lookup"><span data-stu-id="58a94-221">Code sample</span></span>

|<span data-ttu-id="58a94-222">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="58a94-222">**Sample name**</span></span>|<span data-ttu-id="58a94-223">**说明**</span><span class="sxs-lookup"><span data-stu-id="58a94-223">**Description**</span></span>|<span data-ttu-id="58a94-224">**C#**</span><span class="sxs-lookup"><span data-stu-id="58a94-224">**C#**</span></span>|<span data-ttu-id="58a94-225">**TypeScript**</span><span class="sxs-lookup"><span data-stu-id="58a94-225">**TypeScript**</span></span>|
|---------------|---------------|------|--------------|
| <span data-ttu-id="58a94-226">Tab SSO</span><span class="sxs-lookup"><span data-stu-id="58a94-226">Tab SSO</span></span> |<span data-ttu-id="58a94-227">适用于选项卡 Azure AD SSO 的 Microsoft Teams 示例应用</span><span class="sxs-lookup"><span data-stu-id="58a94-227">Microsoft Teams sample app for tabs Azure AD SSO</span></span>| [<span data-ttu-id="58a94-228">View</span><span class="sxs-lookup"><span data-stu-id="58a94-228">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|<span data-ttu-id="58a94-229">[视图](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs)，</span><span class="sxs-lookup"><span data-stu-id="58a94-229">[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs),</span></span> </br>[<span data-ttu-id="58a94-230">Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="58a94-230">Teams Toolkit</span></span>](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a><span data-ttu-id="58a94-231">已知限制</span><span class="sxs-lookup"><span data-stu-id="58a94-231">Known Limitations</span></span>

### <a name="apps-that-require-additional-microsoft-graph-scopes"></a><span data-ttu-id="58a94-232">需要其他 Microsoft Graph 作用域的应用</span><span class="sxs-lookup"><span data-stu-id="58a94-232">Apps that require additional Microsoft Graph Scopes</span></span>

<span data-ttu-id="58a94-233">我们当前针对 SSO 的实现仅授予用户级权限（电子邮件、配置文件、offline_access、OpenId）的许可，而不是针对其他 API (如 User.Read 或 Mail.Read) 。</span><span class="sxs-lookup"><span data-stu-id="58a94-233">Our current implementation for SSO only grants consent for user-level permissions — email, profile, offline_access, OpenId — not for other APIs (such as User.Read or Mail.Read).</span></span> <span data-ttu-id="58a94-234">如果你的应用需要进一步 Microsoft Graph 范围，下面是一些启用的解决方法：</span><span class="sxs-lookup"><span data-stu-id="58a94-234">If your app needs further Microsoft Graph scopes, here are some enabling workarounds:</span></span>

#### <a name="tenant-admin-consent"></a><span data-ttu-id="58a94-235">租户管理员同意</span><span class="sxs-lookup"><span data-stu-id="58a94-235">Tenant Admin Consent</span></span>

<span data-ttu-id="58a94-236">最简单的方法是让租户管理员代表组织预先同意。</span><span class="sxs-lookup"><span data-stu-id="58a94-236">The simplest approach is to get a tenant admin to pre-consent on behalf of the organization.</span></span> <span data-ttu-id="58a94-237">这意味着用户不需要同意这些范围，然后可以使用 Azure AD 的代表流自由交换令牌 [服务器端](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)。</span><span class="sxs-lookup"><span data-stu-id="58a94-237">This means users won’t have to consent to these scopes and you can then be free to exchange the token server side using Azure AD’s [on-behalf-of flow](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow).</span></span> <span data-ttu-id="58a94-238">此解决方法对于内部业务线应用程序是可接受的，但可能不足以供可能无法依赖租户管理员审批的第三方开发人员使用。</span><span class="sxs-lookup"><span data-stu-id="58a94-238">This workaround is acceptable for internal line-of-business applications but may not be enough for third-party developers who may not be able to rely on tenant admin approval.</span></span>

<span data-ttu-id="58a94-239">代表组织以租户管理员 (的一种) 方式是访问：</span><span class="sxs-lookup"><span data-stu-id="58a94-239">A simple way of consenting on behalf of an organization (as a tenant admin) is to visit:</span></span>

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a><span data-ttu-id="58a94-240">使用身份验证 API 请求其他同意</span><span class="sxs-lookup"><span data-stu-id="58a94-240">Asking for additional consent using the Auth API</span></span>

<span data-ttu-id="58a94-241">获取其他 Microsoft Graph 作用域的另一个方法是使用我们现有的基于 Web 的 [Azure AD](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) 身份验证方法显示同意对话框，该方法涉及弹出 Azure AD 同意对话框。</span><span class="sxs-lookup"><span data-stu-id="58a94-241">Another approach for getting additional Microsoft Graph scopes is to present a consent dialog using our existing [web-based Azure AD authentication approach](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) which involves popping up an Azure AD consent dialog.</span></span> <span data-ttu-id="58a94-242">有一些值得注意的新增功能：</span><span class="sxs-lookup"><span data-stu-id="58a94-242">There are some notable additions:</span></span>

1. <span data-ttu-id="58a94-243">使用检索到的令牌需要使用 Azure AD 代表流在服务器端交换，才能访问 `getAuthToken()` 这些额外的 Microsoft Graph API。 [](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)</span><span class="sxs-lookup"><span data-stu-id="58a94-243">The token retrieved using `getAuthToken()` needs to be exchanged server-side using Azure AD [on-behalf-of flow](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) to get access to those additional Microsoft Graph APIs.</span></span>
    * <span data-ttu-id="58a94-244">请务必对此交换使用 v2 Microsoft Graph 终结点</span><span class="sxs-lookup"><span data-stu-id="58a94-244">Be sure to use the v2 Microsoft Graph endpoint for this exchange</span></span>
2. <span data-ttu-id="58a94-245">如果交换失败，Azure AD 将返回无效的授予异常。</span><span class="sxs-lookup"><span data-stu-id="58a94-245">If the exchange fails, Azure AD will return an invalid grant exception.</span></span> <span data-ttu-id="58a94-246">通常有两条错误消息之 `invalid_grant` 一： `interaction_required`</span><span class="sxs-lookup"><span data-stu-id="58a94-246">There are usually one of two error messages: `invalid_grant` or `interaction_required`</span></span>
3. <span data-ttu-id="58a94-247">当交换失败时，需要请求其他同意。</span><span class="sxs-lookup"><span data-stu-id="58a94-247">When the exchange fails, then you need to ask for additional consent.</span></span> <span data-ttu-id="58a94-248">我们建议显示一些要求用户授予其他同意的 UI。</span><span class="sxs-lookup"><span data-stu-id="58a94-248">We recommend showing some UI asking the user to grant additional consent.</span></span> <span data-ttu-id="58a94-249">此 UI 应包括使用 Azure AD 身份验证 API 触发 [Azure AD 同意对话框的按钮](~/concepts/authentication/auth-silent-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="58a94-249">This UI should include a button that triggers an Azure AD consent dialog using our [Azure AD authentication API](~/concepts/authentication/auth-silent-aad.md).</span></span>
4. <span data-ttu-id="58a94-250">当请求 Azure AD 的其他同意时，你需要将查询字符串参数包括在 Azure AD 中，否则 Azure AD 不会要求其他 `prompt=consent` 范围。 [](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context)</span><span class="sxs-lookup"><span data-stu-id="58a94-250">When asking for additional consent from Azure AD, you need to include `prompt=consent` in your [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) to Azure AD otherwise Azure AD will not ask for the additional scopes.</span></span>
    * <span data-ttu-id="58a94-251">而不是： `?scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="58a94-251">Instead of: `?scope={scopes}`</span></span>
    * <span data-ttu-id="58a94-252">使用以下方法： `?prompt=consent&scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="58a94-252">Use this: `?prompt=consent&scope={scopes}`</span></span>
    * <span data-ttu-id="58a94-253">请确保包括提示用户输入 (的所有作用域，例如 `{scopes}` Mail.Read 或 User.Read) 。</span><span class="sxs-lookup"><span data-stu-id="58a94-253">Be sure that `{scopes}` includes all the scopes you are prompting the user for (ex: Mail.Read or User.Read).</span></span>
5. <span data-ttu-id="58a94-254">在用户授予其他权限后，重试代表流获取这些附加 API 的访问权限。</span><span class="sxs-lookup"><span data-stu-id="58a94-254">Once the user has granted additional permission, retry the on-behalf-of-flow to get access to these additional APIs.</span></span>

### <a name="non-azure-ad-authentication"></a><span data-ttu-id="58a94-255">非 Azure AD 身份验证</span><span class="sxs-lookup"><span data-stu-id="58a94-255">Non-Azure AD Authentication</span></span>

<span data-ttu-id="58a94-256">上述身份验证解决方案仅适用于支持 Azure AD 作为标识提供程序的应用和服务。</span><span class="sxs-lookup"><span data-stu-id="58a94-256">The above-described authentication solution only works for apps and services that support Azure AD as an identity provider.</span></span> <span data-ttu-id="58a94-257">想要使用基于非 Azure AD 的服务进行身份验证的应用需要继续使用基于弹出窗口的 [Web 身份验证流](~/concepts/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="58a94-257">Apps that want to authenticate using non-Azure AD based services need to continue using the pop-up-based [web authentication flow](~/concepts/authentication.md).</span></span>

> [!NOTE] 
> <span data-ttu-id="58a94-258">SSO 受 Azure AD B2C 租户内客户拥有的应用支持。</span><span class="sxs-lookup"><span data-stu-id="58a94-258">SSO is supported for customer owned apps within the Azure AD B2C tenants.</span></span>
