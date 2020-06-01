---
title: 单一登录
description: 介绍单一登录（SSO）
keywords: 团队身份验证 SSO AAD
ms.openlocfilehash: 8f9d94346aad7c096e4310f80b6cda73856afc8c
ms.sourcegitcommit: 61c93b22490526b1de87c0b14a3c7eb6e046caf6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/31/2020
ms.locfileid: "44455511"
---
# <a name="single-sign-on"></a><span data-ttu-id="d61aa-104">单一登录</span><span class="sxs-lookup"><span data-stu-id="d61aa-104">Single Sign-On</span></span>

> [!NOTE]
> <span data-ttu-id="d61aa-105">"单一登录" API 目前仅在_开发人员预览版_中受支持。</span><span class="sxs-lookup"><span data-stu-id="d61aa-105">The "single sign-on" API is currently supported in _Developer Preview_ only.</span></span>

<span data-ttu-id="d61aa-106">用户使用其工作或学校（Office 365）帐户登录 Microsoft 团队，您可以使用单一登录（SSO）对 Microsoft "团队" 选项卡上的用户进行授权，以利用这一点。这意味着，如果用户同意在桌面上使用您的应用程序，则无需再次在手机上同意，并且将自动登录。</span><span class="sxs-lookup"><span data-stu-id="d61aa-106">Users sign-in to Microsoft Teams using their work or school (Office 365) account and you can take advantage of this by using single sign-on (SSO) to authorize the user to your Microsoft Teams tab. That means if a user consents to use your app on desktop, they won’t have to consent again on mobile and will be automatically logged in.</span></span> 

## <a name="how-sso-works-at-runtime"></a><span data-ttu-id="d61aa-107">运行时 SSO 的工作方式</span><span class="sxs-lookup"><span data-stu-id="d61aa-107">How SSO works at runtime</span></span>

<span data-ttu-id="d61aa-108">下图显示 SSO 进程的工作原理：</span><span class="sxs-lookup"><span data-stu-id="d61aa-108">The following diagram shows how the SSO process works:</span></span>

<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. <span data-ttu-id="d61aa-109">在 "" 选项卡中，JavaScript 调用 getAuthToken （）。</span><span class="sxs-lookup"><span data-stu-id="d61aa-109">In the tab, JavaScript calls getAuthToken().</span></span> <span data-ttu-id="d61aa-110">这将告知团队应用程序获取对选项卡应用程序的身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="d61aa-110">This tells the Teams application to obtain an authentication token to the tab application.</span></span>
2. <span data-ttu-id="d61aa-111">如果这是当前用户第一次使用您的选项卡应用程序，则系统会提示他们同意（如果需要同意）或要求他们处理分步身份验证（如双重身份验证）。</span><span class="sxs-lookup"><span data-stu-id="d61aa-111">If this is the first time the current user has used your tab application, they will be prompted to consent (if consent is required) or asked to handle step-up authentication (such as two-factor authentication).</span></span>
3. <span data-ttu-id="d61aa-112">Microsoft 团队应用程序从 Azure AD v1.0 终结点请求当前用户的选项卡应用程序令牌。</span><span class="sxs-lookup"><span data-stu-id="d61aa-112">The Microsoft Teams application requests the tab application token from the Azure AD v1.0 endpoint for the current user.</span></span>
4. <span data-ttu-id="d61aa-113">Azure AD 将选项卡应用程序令牌发送给团队应用程序。</span><span class="sxs-lookup"><span data-stu-id="d61aa-113">Azure AD sends the tab application token to the Teams application.</span></span>
5. <span data-ttu-id="d61aa-114">Microsoft 团队应用程序将选项卡应用程序令牌作为 getAuthToken （）调用返回的 result 对象的一部分发送到选项卡。</span><span class="sxs-lookup"><span data-stu-id="d61aa-114">The Microsoft Teams application sends the tab application token to the tab as part of the result object returned by the getAuthToken() call.</span></span>
6. <span data-ttu-id="d61aa-115">选项卡应用程序中的 JavaScript 可以分析令牌，并提取所需的信息，如用户的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="d61aa-115">JavaScript in the tab application can parse the token and extract the information it needs, such as the user's email address.</span></span>
    * <span data-ttu-id="d61aa-116">注意：此令牌仅适用于同意一组有限的用户级 Api （ex：电子邮件、配置文件等），而不是对进一步的图表范围（如 Mail）有效。</span><span class="sxs-lookup"><span data-stu-id="d61aa-116">Note: this token is only valid for consenting to a limited set of user-level APIs (ex: email, profile, etc)  and not for further Graph scopes (such as Mail.Read).</span></span> <span data-ttu-id="d61aa-117">如果你需要其他 Graph 作用域，请参阅本文档末尾的部分，了解建议的解决方法。</span><span class="sxs-lookup"><span data-stu-id="d61aa-117">See our section at the end of this document for suggested workarounds if you require additional Graph scopes.</span></span>

## <a name="develop-an-sso-microsoft-teams-tab"></a><span data-ttu-id="d61aa-118">开发 SSO Microsoft 团队选项卡</span><span class="sxs-lookup"><span data-stu-id="d61aa-118">Develop an SSO Microsoft Teams tab</span></span>

<span data-ttu-id="d61aa-119">本节介绍创建使用 SSO 的 Microsoft "团队" 选项卡所涉及的任务。</span><span class="sxs-lookup"><span data-stu-id="d61aa-119">This section describes the tasks involved in creating an Microsoft Teams tab that use SSO.</span></span> <span data-ttu-id="d61aa-120">其中介绍的这些任务与语言和框架无关。</span><span class="sxs-lookup"><span data-stu-id="d61aa-120">These tasks are described here in a language- and framework-agnostic way.</span></span>

### <a name="1-create-your-aad-application-in-azure"></a><span data-ttu-id="d61aa-121">1. 在 Azure 中创建 AAD 应用程序</span><span class="sxs-lookup"><span data-stu-id="d61aa-121">1. Create your AAD application in Azure</span></span>

<span data-ttu-id="d61aa-122">在 Azure AD v1.0 终结点的注册门户中注册应用程序。</span><span class="sxs-lookup"><span data-stu-id="d61aa-122">Register you application at the registration portal for the Azure AD v1.0 endpoint.</span></span> <span data-ttu-id="d61aa-123">该流程用时 5-10 分钟，包括以下任务：</span><span class="sxs-lookup"><span data-stu-id="d61aa-123">This is a 5–10 minute process that includes the following tasks:</span></span>

* <span data-ttu-id="d61aa-124">获取 AAD 应用程序 ID</span><span class="sxs-lookup"><span data-stu-id="d61aa-124">Getting your AAD application ID</span></span>
* <span data-ttu-id="d61aa-125">指定应用程序对 AAD 终结点（也可以选择向 Microsoft Graph）所需的权限。</span><span class="sxs-lookup"><span data-stu-id="d61aa-125">Specify the permissions that your application needs for the AAD endpoint (and optionally to Microsoft Graph).</span></span> 
* <span data-ttu-id="d61aa-126">向 Microsoft 团队桌面、web 和移动应用程序授予对应用程序的信任</span><span class="sxs-lookup"><span data-stu-id="d61aa-126">Grant the Microsoft Teams desktop, web and mobile application to trust to your application</span></span>
* <span data-ttu-id="d61aa-127">预授权将 Microsoft 团队应用程序与默认作用域名称为的应用程序结合使用 `access_as_user` 。</span><span class="sxs-lookup"><span data-stu-id="d61aa-127">Preauthorize the Microsoft Teams application to your app with the default scope name of `access_as_user`.</span></span>

> [!NOTE]
> <span data-ttu-id="d61aa-128">您应注意一些重要限制：</span><span class="sxs-lookup"><span data-stu-id="d61aa-128">There are some important restrictions you should be aware of:</span></span>
>
> * <span data-ttu-id="d61aa-129">仅支持用户级图形 API 权限，例如，电子邮件、配置文件、offline_access、openid。</span><span class="sxs-lookup"><span data-stu-id="d61aa-129">We only support user-level Graph API permissions, e.g., email, profile, offline_access, openid.</span></span> <span data-ttu-id="d61aa-130">如果需要访问其他图表范围，请阅读本文档末尾的建议解决方法。</span><span class="sxs-lookup"><span data-stu-id="d61aa-130">If you need access to other Graph scopes, read our recommended workaround at the end of this documentation.</span></span>
> * <span data-ttu-id="d61aa-131">您的应用程序的域名应注册到 Azure AD 应用程序，这一点很重要。</span><span class="sxs-lookup"><span data-stu-id="d61aa-131">It's important that your application's domain name be registered with your Azure AD application.</span></span> <span data-ttu-id="d61aa-132">当在团队中请求身份验证令牌时，以及在团队清单中指定资源属性（下一节中的详细信息）时，此名称必须与应用程序运行的域名相同。</span><span class="sxs-lookup"><span data-stu-id="d61aa-132">This must be the same domain name that your application runs on when requesting an authentication token in Teams and also when specifying the resource property in your Teams manifest (more details in the next section).</span></span>
> * <span data-ttu-id="d61aa-133">目前，每个应用程序不支持多个域</span><span class="sxs-lookup"><span data-stu-id="d61aa-133">We do not currently support multiple domains per app</span></span>
> * <span data-ttu-id="d61aa-134">我们还不支持使用域的应用程序， `azurewebsites.net` 因为此域太常见，可能存在安全风险</span><span class="sxs-lookup"><span data-stu-id="d61aa-134">We also do not support applications that use the `azurewebsites.net` domain since this domain is too common and may be a security risk</span></span>

#### <a name="steps"></a><span data-ttu-id="d61aa-135">步骤</span><span class="sxs-lookup"><span data-stu-id="d61aa-135">Steps</span></span>

1. <span data-ttu-id="d61aa-136">在 Azure Active Directory 中注册新应用程序[–应用注册](https://go.microsoft.com/fwlink/?linkid=2083908)门户</span><span class="sxs-lookup"><span data-stu-id="d61aa-136">Register a new application in the [Azure Active Directory – App Registration](https://go.microsoft.com/fwlink/?linkid=2083908) portal</span></span>
2. <span data-ttu-id="d61aa-137">选择 "新注册"。</span><span class="sxs-lookup"><span data-stu-id="d61aa-137">Select “New Registration”.</span></span> <span data-ttu-id="d61aa-138">在 "注册应用程序" 页上，按如下所示设置值：</span><span class="sxs-lookup"><span data-stu-id="d61aa-138">On the register an application page, set the values as follows:</span></span>
    * <span data-ttu-id="d61aa-139">将**名称**设置为您的应用程序名称</span><span class="sxs-lookup"><span data-stu-id="d61aa-139">Set **name** to your app name</span></span>
    * <span data-ttu-id="d61aa-140">将**支持的帐户类型**设置为**任何组织目录和个人 Microsoft 帐户中的帐户**</span><span class="sxs-lookup"><span data-stu-id="d61aa-140">Set **supported account types** to **Accounts in any organizational directory and personal Microsoft accounts**</span></span>
    * <span data-ttu-id="d61aa-141">将**重定向 URI**留空</span><span class="sxs-lookup"><span data-stu-id="d61aa-141">Leave **Redirect URI** empty</span></span>
    * <span data-ttu-id="d61aa-142">选择 "**注册**"</span><span class="sxs-lookup"><span data-stu-id="d61aa-142">Choose **Register**</span></span>
3. <span data-ttu-id="d61aa-143">在 "概述" 页上，复制并保存**应用程序（客户端） ID**。</span><span class="sxs-lookup"><span data-stu-id="d61aa-143">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="d61aa-144">稍后在更新团队应用程序清单时，将需要它。</span><span class="sxs-lookup"><span data-stu-id="d61aa-144">You’ll need it later when updating your Teams application manifest.</span></span>
4. <span data-ttu-id="d61aa-145">在“管理”\*\*\*\* 下选择“公开 API”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="d61aa-145">Select **Expose an API** under **Manage**.</span></span> <span data-ttu-id="d61aa-146">选择 "**设置**" 链接，以以的形式生成应用程序 ID URI `api://{AppID}` 。</span><span class="sxs-lookup"><span data-stu-id="d61aa-146">Select the **Set** link to generate the Application ID URI in the form of `api://{AppID}`.</span></span> <span data-ttu-id="d61aa-147">在双正斜杠和 GUID 之间插入完全限定的域名（在末尾追加一个正斜杠 "/"）。</span><span class="sxs-lookup"><span data-stu-id="d61aa-147">Insert your fully qualified domain name (with a forward slash "/" appended to the end) between the double forward slashes and the GUID.</span></span> <span data-ttu-id="d61aa-148">整个 ID 的形式应为：`api://fully-qualified-domain-name.com/{AppID}`</span><span class="sxs-lookup"><span data-stu-id="d61aa-148">The entire ID should have the form of: `api://fully-qualified-domain-name.com/{AppID}`</span></span>
    * <span data-ttu-id="d61aa-149">例如： `api://subdomain.example.com:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7` 。</span><span class="sxs-lookup"><span data-stu-id="d61aa-149">ex: `api://subdomain.example.com:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7`.</span></span>

> [!NOTE]
> <span data-ttu-id="d61aa-150">如果收到一条错误，指出域已有所有者，但你拥有该域，请按照[快速入门： 将自定义域名添加到 Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) 中的步骤进行操作来注册该域，然后重复此步骤。</span><span class="sxs-lookup"><span data-stu-id="d61aa-150">If you get an error saying that the domain is already owned but you own it, follow the procedure at [Quickstart: Add a custom domain name to Azure Active Directory](/azure/active-directory/fundamentals/add-custom-domain) to register it, and then repeat this step.</span></span> <span data-ttu-id="d61aa-151">（如果您未使用 Office 365 租赁中的管理员的凭据登录，也会发生此错误。</span><span class="sxs-lookup"><span data-stu-id="d61aa-151">(This error can also occur if you are not signed in with credentials of an admin in the Office 365 tenancy).</span></span>

5. <span data-ttu-id="d61aa-152">选择“添加一个作用域”\*\*\*\* 按钮。</span><span class="sxs-lookup"><span data-stu-id="d61aa-152">Select the **Add a scope** button.</span></span> <span data-ttu-id="d61aa-153">在打开的面板中，输入 `access_as_user` 作为“作用域名称”\*\*\*\*。</span><span class="sxs-lookup"><span data-stu-id="d61aa-153">In the panel that opens, enter `access_as_user` as the **Scope name**.</span></span>
6. <span data-ttu-id="d61aa-154">设置谁可以同意？为管理员和用户</span><span class="sxs-lookup"><span data-stu-id="d61aa-154">Set Who can consent? to Admins and users</span></span>
7. <span data-ttu-id="d61aa-155">填写用于配置管理员和用户同意提示的字段，其中包含适用于该范围的值 `access_as_user` 。</span><span class="sxs-lookup"><span data-stu-id="d61aa-155">Fill in the fields for configuring the admin and user consent prompts with values that are appropriate for the `access_as_user` scope.</span></span> <span data-ttu-id="d61aa-156">建议：</span><span class="sxs-lookup"><span data-stu-id="d61aa-156">Suggestions:</span></span>
    * <span data-ttu-id="d61aa-157">**管理员同意职务：** 团队可以访问用户的配置文件</span><span class="sxs-lookup"><span data-stu-id="d61aa-157">**Admin consent title:** Teams can access the user’s profile</span></span>
    * <span data-ttu-id="d61aa-158">**管理员同意说明**：允许团队以当前用户的身份调用应用程序的 web api。</span><span class="sxs-lookup"><span data-stu-id="d61aa-158">**Admin consent description**: Allows Teams to call the app’s web APIs as the current user.</span></span>
    * <span data-ttu-id="d61aa-159">**用户同意标题**：团队可以访问您的用户配置文件并代表你发出请求</span><span class="sxs-lookup"><span data-stu-id="d61aa-159">**User consent title**: Teams can access your user profile and make requests on your behalf</span></span>
    * <span data-ttu-id="d61aa-160">**用户同意说明：** 使团队可以使用你拥有的相同权限调用此应用的 Api</span><span class="sxs-lookup"><span data-stu-id="d61aa-160">**User consent description:** Enable Teams to call this app’s APIs with the same rights that you have</span></span>
8. <span data-ttu-id="d61aa-161">确保将 "**状态**" 设置为 "**已启用**"</span><span class="sxs-lookup"><span data-stu-id="d61aa-161">Ensure that **State** is set to **Enabled**</span></span>
9. <span data-ttu-id="d61aa-162">选择 "**添加范围**"</span><span class="sxs-lookup"><span data-stu-id="d61aa-162">Select **Add scope**</span></span>
    * <span data-ttu-id="d61aa-163">注意：在文本字段正下方显示的**范围名称**的域部分应自动与上一步中设置的**应用程序 ID** URI 进行匹配，并 `/access_as_user` 追加到结尾处; 例如：</span><span class="sxs-lookup"><span data-stu-id="d61aa-163">Note: The domain part of the **Scope name** displayed just below the text field should automatically match the **Application ID** URI set in the previous step, with `/access_as_user` appended to the end; for example:</span></span> 
        * `api://subdomain.example.com:6789/c6c1f32b-5e55-4997-881a-753cc1d563b7/access_as_user`
10. <span data-ttu-id="d61aa-164">在 "**授权客户端应用程序**" 部分中，确定要授权给应用程序的 web 应用程序的应用程序。</span><span class="sxs-lookup"><span data-stu-id="d61aa-164">In the **Authorized client applications** section, you identify the applications that you want to authorize to your app’s web application.</span></span> <span data-ttu-id="d61aa-165">需要输入以下每个 Id：</span><span class="sxs-lookup"><span data-stu-id="d61aa-165">Each of the following IDs needs to be entered:</span></span>
    * <span data-ttu-id="d61aa-166">`1fec8e78-bce4-4aaf-ab1b-5451cc387264`（团队移动/桌面应用程序）</span><span class="sxs-lookup"><span data-stu-id="d61aa-166">`1fec8e78-bce4-4aaf-ab1b-5451cc387264` (Teams mobile/desktop application)</span></span>
    * <span data-ttu-id="d61aa-167">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346`（团队 web 应用程序）</span><span class="sxs-lookup"><span data-stu-id="d61aa-167">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346` (Teams web application)</span></span>
11. <span data-ttu-id="d61aa-168">导航到 " **API 权限**"，并确保添加 "关注" 权限：</span><span class="sxs-lookup"><span data-stu-id="d61aa-168">Navigate to **API Permissions**, and make sure to add the follow permissions:</span></span>
    * <span data-ttu-id="d61aa-169">User。 Read （默认情况下已启用）</span><span class="sxs-lookup"><span data-stu-id="d61aa-169">User.Read (enabled by default)</span></span>
    * <span data-ttu-id="d61aa-170">email</span><span class="sxs-lookup"><span data-stu-id="d61aa-170">email</span></span>
    * <span data-ttu-id="d61aa-171">offline_access</span><span class="sxs-lookup"><span data-stu-id="d61aa-171">offline_access</span></span>
    * <span data-ttu-id="d61aa-172">openid</span><span class="sxs-lookup"><span data-stu-id="d61aa-172">openid</span></span>
    * <span data-ttu-id="d61aa-173">profile</span><span class="sxs-lookup"><span data-stu-id="d61aa-173">profile</span></span>

### <a name="2-update-your-microsoft-teams-application-manifest"></a><span data-ttu-id="d61aa-174">2. 更新 Microsoft 团队应用程序清单</span><span class="sxs-lookup"><span data-stu-id="d61aa-174">2. Update your Microsoft Teams application manifest</span></span>

<span data-ttu-id="d61aa-175">将新属性添加到 Microsoft 团队清单：</span><span class="sxs-lookup"><span data-stu-id="d61aa-175">Add new properties to your Microsoft Teams manifest:</span></span>

* <span data-ttu-id="d61aa-176">**WebApplicationInfo** - 下列元素的父元素。</span><span class="sxs-lookup"><span data-stu-id="d61aa-176">**WebApplicationInfo** - The parent of the following elements.</span></span>
* <span data-ttu-id="d61aa-177">**Id** -应用程序的客户端 Id。</span><span class="sxs-lookup"><span data-stu-id="d61aa-177">**Id** - The client ID of the application.</span></span> <span data-ttu-id="d61aa-178">这是在使用 Azure AD 1.0 终结点注册应用程序的过程中获得的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="d61aa-178">This is an application ID that you obtain as part of registering the application with Azure AD 1.0 endpoint.</span></span>
* <span data-ttu-id="d61aa-179">**Resource** -应用程序的域和子域。</span><span class="sxs-lookup"><span data-stu-id="d61aa-179">**Resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="d61aa-180">这是在 `api://` AAD 中注册应用时使用的 URI （包括协议）。</span><span class="sxs-lookup"><span data-stu-id="d61aa-180">This is the same URI (including the `api://` protocol) that you used when registering the app in AAD.</span></span> <span data-ttu-id="d61aa-181">此 URI 的域部分应与在团队应用程序清单的部分的 Url 中使用的域（包括任何子域）相匹配。</span><span class="sxs-lookup"><span data-stu-id="d61aa-181">The domain part of this URI should match the domain, including any subdomains, used in the URLs in the section of your Teams application manifest.</span></span>

```json
"webApplicationInfo": {
  "id": "<application_GUID here>",
  "resource": "<web_API resource here>"
}
```

<span data-ttu-id="d61aa-182">注意：</span><span class="sxs-lookup"><span data-stu-id="d61aa-182">Notes:</span></span>

* <span data-ttu-id="d61aa-183">AAD 应用的资源通常只是其网站 URL 和 appID 的根（例如 `api://subdomain.example.com/6789/c6c1f32b-5e55-4997-881a-753cc1d563b7` ）。</span><span class="sxs-lookup"><span data-stu-id="d61aa-183">The resource for an AAD app will usually just be the root of its site URL and the appID (e.g. `api://subdomain.example.com/6789/c6c1f32b-5e55-4997-881a-753cc1d563b7`).</span></span> <span data-ttu-id="d61aa-184">我们还使用此值来确保你的请求来自同一个域。</span><span class="sxs-lookup"><span data-stu-id="d61aa-184">We also use this value to ensure your request is coming from the same domain.</span></span> <span data-ttu-id="d61aa-185">Therefor 确保您 `contentURL` 的选项卡使用与您的资源属性相同的域。</span><span class="sxs-lookup"><span data-stu-id="d61aa-185">Therefor make sure that your `contentURL` for your tab uses the same domains as your resource property.</span></span>
* <span data-ttu-id="d61aa-186">您需要使用清单版本1.5 或更高版本，才能使用这些字段。</span><span class="sxs-lookup"><span data-stu-id="d61aa-186">You need to be using manifest version 1.5 or higher for these fields to be used.</span></span>
* <span data-ttu-id="d61aa-187">清单在清单中不受支持，而是应在 Azure 门户中的 API 权限部分中指定。</span><span class="sxs-lookup"><span data-stu-id="d61aa-187">Scopes aren’t supported in the manifest and instead should be specified in the API Permissions section in the Azure portal</span></span>

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a><span data-ttu-id="d61aa-188">3. 从客户端代码中获取身份验证令牌</span><span class="sxs-lookup"><span data-stu-id="d61aa-188">3. Get an authentication token from your client-side code</span></span>

<span data-ttu-id="d61aa-189">身份验证 API 如下所示：</span><span class="sxs-lookup"><span data-stu-id="d61aa-189">Here's what the authentication API looks like:</span></span>

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); },
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

<span data-ttu-id="d61aa-190">当你拨打 `getAuthToken` 并需要其他用户同意时（对于用户级权限），我们将向用户显示一个对话框，让他们鼓励他们授予额外的许可。</span><span class="sxs-lookup"><span data-stu-id="d61aa-190">When you call `getAuthToken` - and additional user consent is required (for user-level permissions) - we will show a dialog to the user encouraging them to grant additional consent.</span></span> 

<img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>

## <a name="demo-code"></a><span data-ttu-id="d61aa-191">演示代码</span><span class="sxs-lookup"><span data-stu-id="d61aa-191">Demo code</span></span>

<span data-ttu-id="d61aa-192">现在，您可以访问我们的测试应用程序[任务 Meow](https://github.com/ydogandjiev/taskmeow) ，并使用 SSO 清单并签出 `teams.auth.service.js` 和 `sso.auth.service.js` 文件，以查看如何处理身份验证工作流。</span><span class="sxs-lookup"><span data-stu-id="d61aa-192">For now you can visit our test application [Task Meow](https://github.com/ydogandjiev/taskmeow) and use the SSO manifest and checkout the `teams.auth.service.js` and `sso.auth.service.js` file to see how we handle the authentication workflow.</span></span>

## <a name="known-limitations"></a><span data-ttu-id="d61aa-193">已知限制</span><span class="sxs-lookup"><span data-stu-id="d61aa-193">Known Limitations</span></span>

### <a name="apps-that-require-additional-graph-scopes"></a><span data-ttu-id="d61aa-194">需要其他图表范围的应用程序</span><span class="sxs-lookup"><span data-stu-id="d61aa-194">Apps that require additional Graph Scopes</span></span>

<span data-ttu-id="d61aa-195">我们目前的 SSO 实施仅授予用户级权限（电子邮件、配置文件、offline_access、openid）的同意，而不授予对其他 Api （如 Mail）的同意。</span><span class="sxs-lookup"><span data-stu-id="d61aa-195">Our current implementation for SSO only grants consent for user-level permissions (email, profile, offline_access, openid) but not for other APIs (such as Mail.Read).</span></span> <span data-ttu-id="d61aa-196">如果您的应用程序需要更多图形范围，则有一些解决办法可实现此工作。</span><span class="sxs-lookup"><span data-stu-id="d61aa-196">If your app needs further Graph scopes, there are some workarounds to enable this.</span></span>

#### <a name="tenant-admin-consent"></a><span data-ttu-id="d61aa-197">租户管理员同意</span><span class="sxs-lookup"><span data-stu-id="d61aa-197">Tenant Admin Consent</span></span>

<span data-ttu-id="d61aa-198">最简单的方法是，让租户管理员代表组织进行预先同意。</span><span class="sxs-lookup"><span data-stu-id="d61aa-198">The simplest approach would be to get a tenant admin to pre-consent on behalf of the organization.</span></span> <span data-ttu-id="d61aa-199">这意味着用户无需同意这些作用域，然后可以使用 AAD 的[代表流](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)来免费交换令牌服务器端。</span><span class="sxs-lookup"><span data-stu-id="d61aa-199">This means users won’t have to consent to these scopes and you can then be free to exchange the token server side using AAD’s [on-behalf-of flow](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow).</span></span> <span data-ttu-id="d61aa-200">这种解决方法对于内部业务线应用程序是可接受的，但对于可能无法依赖租户管理员批准的 Isv 来说可能不够。</span><span class="sxs-lookup"><span data-stu-id="d61aa-200">This workaround is acceptable for internal line-of-business applications but may not be enough for ISVs who may not be able to rely on tenant admin approval.</span></span>

<span data-ttu-id="d61aa-201">同意代表组织（作为租户管理员）的一种简单方法是访问：</span><span class="sxs-lookup"><span data-stu-id="d61aa-201">A simple way of consenting on behalf of an organization (as a tenant admin) is to visit:</span></span>

* `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`

#### <a name="asking-for-additional-consent-using-the-auth-api"></a><span data-ttu-id="d61aa-202">使用 Auth API 请求其他许可</span><span class="sxs-lookup"><span data-stu-id="d61aa-202">Asking for additional consent using the Auth API</span></span>

<span data-ttu-id="d61aa-203">获取其他图表范围的另一种方法是，使用现有的[基于 web 的 aad 身份验证方法](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)呈现许可对话，这涉及弹出 AAD 同意对话框。</span><span class="sxs-lookup"><span data-stu-id="d61aa-203">Another approach for getting additional Graph scopes would be to present a consent dialog using our existing [web-based AAD authentication approach](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) which involves popping up an AAD consent dialog.</span></span> <span data-ttu-id="d61aa-204">有一些显著的添加：</span><span class="sxs-lookup"><span data-stu-id="d61aa-204">There are some notable additions:</span></span>

1. <span data-ttu-id="d61aa-205">使用 getAuthToken 检索到的令牌需要使用 AADs[代表流](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)进行交换，以获取对这些其他图形 api 的访问权限。</span><span class="sxs-lookup"><span data-stu-id="d61aa-205">The token retrieved using getAuthToken would need to be exchanged server side using AADs [on-behalf-of flow](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow) to get access to those additional Graph APIs.</span></span>
    * <span data-ttu-id="d61aa-206">请务必将 v2 Graph 终结点用于此 exchange</span><span class="sxs-lookup"><span data-stu-id="d61aa-206">Be sure to use the v2 Graph endpoint for this exchange</span></span>
2. <span data-ttu-id="d61aa-207">如果 exchange 失败，AAD 将返回无效的授予异常。</span><span class="sxs-lookup"><span data-stu-id="d61aa-207">If the exchange fails, AAD will return an invalid grant exception.</span></span> <span data-ttu-id="d61aa-208">通常有以下两种错误消息 `ConsentRequired` 之一：`InteractionRequired`</span><span class="sxs-lookup"><span data-stu-id="d61aa-208">There are usually one of two error messages: `ConsentRequired` or `InteractionRequired`</span></span>
3. <span data-ttu-id="d61aa-209">当 exchange 发生故障时，您需要请求其他许可。</span><span class="sxs-lookup"><span data-stu-id="d61aa-209">When the exchange fails, then you need to ask for additional consent.</span></span> <span data-ttu-id="d61aa-210">建议显示一些 UI，要求用户授予更多许可。</span><span class="sxs-lookup"><span data-stu-id="d61aa-210">We recommend showing some UI asking the user to grant additional consent.</span></span> <span data-ttu-id="d61aa-211">此 UI 应包含使用我们的[AAD 身份验证 API](~/concepts/authentication/auth-silent-aad.md)触发 aad 同意对话的按钮。</span><span class="sxs-lookup"><span data-stu-id="d61aa-211">This UI should include a button that triggers an AAD consent dialog using our [AAD authentication API](~/concepts/authentication/auth-silent-aad.md).</span></span>
4. <span data-ttu-id="d61aa-212">当询问来自 AAD 的其他许可时，您需要将 `prompt=consent` [查询字符串参数](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context)包括在您的 aad 中，否则 aad 将不会询问其他作用域。</span><span class="sxs-lookup"><span data-stu-id="d61aa-212">When asking for additional consent from AAD, you need to include `prompt=consent` in your [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) to AAD otherwise AAD will not ask for the additional scopes.</span></span>
    * <span data-ttu-id="d61aa-213">而不是：`?scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="d61aa-213">Instead of: `?scope={scopes}`</span></span>
    * <span data-ttu-id="d61aa-214">使用以下命令：`?prompt=consent&scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="d61aa-214">Use this: `?prompt=consent&scope={scopes}`</span></span>
    * <span data-ttu-id="d61aa-215">确保 `{scopes}` 包含要提示用户的所有作用域（例如： Mail. read 或 user. read）。</span><span class="sxs-lookup"><span data-stu-id="d61aa-215">Be sure that `{scopes}` includes all the scopes you are prompting the user for (ex: Mail.Read or User.Read).</span></span>
5. <span data-ttu-id="d61aa-216">一旦用户授予了其他权限，则重试代表流，以获取对这些附加 Api 的访问权限。</span><span class="sxs-lookup"><span data-stu-id="d61aa-216">Once the user has granted additional permission, retry the on-behalf-of-flow to get access to these additional APIs.</span></span>

### <a name="non-aad-authentication"></a><span data-ttu-id="d61aa-217">非 AAD 身份验证</span><span class="sxs-lookup"><span data-stu-id="d61aa-217">Non-AAD Authentication</span></span>

<span data-ttu-id="d61aa-218">以上所述的身份验证解决方案仅适用于支持 Azure AD 作为标识提供程序的应用程序和服务。</span><span class="sxs-lookup"><span data-stu-id="d61aa-218">The above-described authentication solution only works for apps and services that support Azure AD as an identity provider.</span></span> <span data-ttu-id="d61aa-219">若要使用基于非 AAD 的服务进行身份验证的应用程序，需要继续使用基于弹出窗口的[web 身份验证流](~/concepts/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="d61aa-219">Apps that want to authenticate using non-AAD based services need to continue using the popup-based [web authentication flow](~/concepts/authentication.md).</span></span>
