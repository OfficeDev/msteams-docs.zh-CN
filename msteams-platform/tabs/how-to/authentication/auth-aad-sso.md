---
title: 选项卡的单一登录支持
description: '介绍 SSO (单一) '
ms.topic: how-to
localization_priority: Normal
keywords: teams 身份验证 SSO AAD 单一登录 api
ms.openlocfilehash: 65e8d5e5387ec727e9ce02967516d8672bf67931
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019606"
---
# <a name="single-sign-on-sso-support-for-tabs"></a><span data-ttu-id="27c96-104">单一登录 (SSO) 选项卡支持</span><span class="sxs-lookup"><span data-stu-id="27c96-104">Single sign-on (SSO) support for tabs</span></span>

<span data-ttu-id="27c96-105">用户通过Microsoft Teams、学校或 Microsoft 帐户（Office 365、Outlook等）登录登录。</span><span class="sxs-lookup"><span data-stu-id="27c96-105">Users sign in to Microsoft Teams through their work, school, or Microsoft accounts that is Office 365, Outlook, and so on.</span></span> <span data-ttu-id="27c96-106">通过允许单一登录在桌面或移动客户端上授权Teams选项卡或任务模块，可以充分利用这一点。</span><span class="sxs-lookup"><span data-stu-id="27c96-106">You can take advantage of this by allowing a single sign-on to authorize your Teams tab or task module on desktop or mobile clients.</span></span> <span data-ttu-id="27c96-107">如果用户同意使用你的应用，则当他们自动登录时，他们不需要在另一台设备上再次同意。</span><span class="sxs-lookup"><span data-stu-id="27c96-107">If a user consents to use your app, they do not have to consent again on another device as they are signed in automatically.</span></span> <span data-ttu-id="27c96-108">此外，会预取访问令牌，以改进性能和加载时间。</span><span class="sxs-lookup"><span data-stu-id="27c96-108">In addition, your access token is prefetched to improve performance and load times.</span></span>

> [!NOTE]
> <span data-ttu-id="27c96-109">**Teams SSO 的移动客户端版本**</span><span class="sxs-lookup"><span data-stu-id="27c96-109">**Teams mobile client versions supporting SSO**</span></span>  
>
> <span data-ttu-id="27c96-110">✔Teams Android (1416/1.0.0.2020073101 及更高版本) </span><span class="sxs-lookup"><span data-stu-id="27c96-110">✔Teams for Android (1416/1.0.0.2020073101 and later)</span></span>
>
> <span data-ttu-id="27c96-111">✔Teams iOS (_版本_：2.0.18 及更高版本) </span><span class="sxs-lookup"><span data-stu-id="27c96-111">✔Teams for iOS (_Version_: 2.0.18 and later)</span></span>  
>
> <span data-ttu-id="27c96-112">为了获得最佳体验Teams，请使用最新版本的 iOS 和 Android。</span><span class="sxs-lookup"><span data-stu-id="27c96-112">For the best experience with Teams, use the latest version of iOS and Android.</span></span>

> [!NOTE]
> <span data-ttu-id="27c96-113">**快速入门**</span><span class="sxs-lookup"><span data-stu-id="27c96-113">**Quickstart**</span></span>  
>
> <span data-ttu-id="27c96-114">开始使用选项卡 SSO 的最简单路径是使用适用于 Teams 的 Visual Studio Code。</span><span class="sxs-lookup"><span data-stu-id="27c96-114">The simplest path to getting started with tab SSO is with the Teams toolkit for Visual Studio Code.</span></span> <span data-ttu-id="27c96-115">有关详细信息，请参阅[SSO with Teams toolkit 和 Visual Studio Code for tabs](../../../toolkit/visual-studio-code-tab-sso.md)</span><span class="sxs-lookup"><span data-stu-id="27c96-115">For more information, see [SSO with Teams toolkit and Visual Studio Code for tabs](../../../toolkit/visual-studio-code-tab-sso.md)</span></span>

## <a name="how-sso-works-at-runtime"></a><span data-ttu-id="27c96-116">运行时 SSO 的工作方式</span><span class="sxs-lookup"><span data-stu-id="27c96-116">How SSO works at runtime</span></span>

<span data-ttu-id="27c96-117">下图显示了 SSO 进程的工作原理：</span><span class="sxs-lookup"><span data-stu-id="27c96-117">The following image shows how the SSO process works:</span></span>

<!-- markdownlint-disable MD033 -->
<img src="~/assets/images/tabs/tabs-sso-diagram.png" alt="Tab single sign-on SSO diagram" width="75%"/>

1. <span data-ttu-id="27c96-118">在选项卡中，对 进行 JavaScript 调用 `getAuthToken()` 。</span><span class="sxs-lookup"><span data-stu-id="27c96-118">In the tab, a JavaScript call is made to `getAuthToken()`.</span></span> <span data-ttu-id="27c96-119">这将Teams获取选项卡应用程序的身份验证令牌。</span><span class="sxs-lookup"><span data-stu-id="27c96-119">This tells Teams to obtain an authentication token for the tab application.</span></span>
2. <span data-ttu-id="27c96-120">如果这是当前用户第一次使用你的选项卡应用程序，则当需要同意或处理双重身份验证等逐步身份验证时，会提示你同意。</span><span class="sxs-lookup"><span data-stu-id="27c96-120">If this is the first time the current user has used your tab application, there is a request prompt to consent if consent is required or to handle step-up authentication such as two-factor authentication.</span></span>
3. <span data-ttu-id="27c96-121">Teams从当前用户的 AAD Azure Active Directory (终结点) 选项卡应用程序令牌。</span><span class="sxs-lookup"><span data-stu-id="27c96-121">Teams requests the tab application token from the Azure Active Directory (AAD) endpoint for the current user.</span></span>
4. <span data-ttu-id="27c96-122">AAD 将选项卡应用程序令牌发送到Teams应用程序。</span><span class="sxs-lookup"><span data-stu-id="27c96-122">AAD sends the tab application token to the Teams application.</span></span>
5. <span data-ttu-id="27c96-123">Teams将选项卡应用程序令牌作为调用返回的结果对象的一部分发送到 `getAuthToken()` 选项卡。</span><span class="sxs-lookup"><span data-stu-id="27c96-123">Teams sends the tab application token to the tab as part of the result object returned by the `getAuthToken()` call.</span></span>
6. <span data-ttu-id="27c96-124">令牌使用 JavaScript 在选项卡应用程序中进行分析，以提取所需信息，如用户的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="27c96-124">The token is parsed in the tab application using JavaScript, to extract required information, such as the user's email address.</span></span>

> [!NOTE]
> <span data-ttu-id="27c96-125">仅在同意一组有限的用户级 API（即电子邮件、配置文件、offline_access `getAuthToken()` OpenId）时有效。</span><span class="sxs-lookup"><span data-stu-id="27c96-125">The `getAuthToken()` is only valid for consenting to a limited set of user-level APIs that is email, profile, offline_access and OpenId.</span></span> <span data-ttu-id="27c96-126">它不能用于进一步Graph范围，如 `User.Read` 或 `Mail.Read` 。</span><span class="sxs-lookup"><span data-stu-id="27c96-126">It is not used for further Graph scopes such as `User.Read` or `Mail.Read`.</span></span> <span data-ttu-id="27c96-127">有关建议的解决方法，请参阅[其他Graph范围](#apps-that-require-additional-graph-scopes)。</span><span class="sxs-lookup"><span data-stu-id="27c96-127">For suggested workarounds, see [additional Graph scopes](#apps-that-require-additional-graph-scopes).</span></span>

<span data-ttu-id="27c96-128">SSO API 还适用于 [嵌入](../../../task-modules-and-cards/what-are-task-modules.md) Web 内容的任务模块。</span><span class="sxs-lookup"><span data-stu-id="27c96-128">The SSO API also works in [task modules](../../../task-modules-and-cards/what-are-task-modules.md) that embed web content.</span></span>

## <a name="develop-an-sso-microsoft-teams-tab"></a><span data-ttu-id="27c96-129">"开发 SSO Microsoft Teams"选项卡</span><span class="sxs-lookup"><span data-stu-id="27c96-129">Develop an SSO Microsoft Teams tab</span></span>

<span data-ttu-id="27c96-130">本节介绍创建使用 SSO 的 Teams 选项卡所涉及的任务。</span><span class="sxs-lookup"><span data-stu-id="27c96-130">This section describes the tasks involved in creating a Teams tab that uses SSO.</span></span> <span data-ttu-id="27c96-131">这些任务与语言和框架无关。</span><span class="sxs-lookup"><span data-stu-id="27c96-131">These tasks are language- and framework-agnostic.</span></span>

### <a name="1-create-your-aad-application"></a><span data-ttu-id="27c96-132">1. 创建 AAD 应用程序</span><span class="sxs-lookup"><span data-stu-id="27c96-132">1. Create your AAD application</span></span>

<span data-ttu-id="27c96-133">**在 AAD 门户概述 [中注册](https://azure.microsoft.com/features/azure-portal/) 应用程序**</span><span class="sxs-lookup"><span data-stu-id="27c96-133">**To register your application in the [AAD portal](https://azure.microsoft.com/features/azure-portal/) overview**</span></span>

1. <span data-ttu-id="27c96-134">获取[AAD 应用程序 ID。](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in)</span><span class="sxs-lookup"><span data-stu-id="27c96-134">Get your [AAD Application ID](/azure/active-directory/develop/howto-create-service-principal-portal#get-values-for-signing-in).</span></span>
2. <span data-ttu-id="27c96-135">指定应用程序所需的 AAD 终结点和（可选）Graph。</span><span class="sxs-lookup"><span data-stu-id="27c96-135">Specify the permissions that your application needs for the AAD endpoint and, optionally, Graph.</span></span>
3. <span data-ttu-id="27c96-136">[授予对](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources)桌面Teams Web 和移动应用程序的权限。</span><span class="sxs-lookup"><span data-stu-id="27c96-136">[Grant permissions](/azure/active-directory/develop/howto-create-service-principal-portal#configure-access-policies-on-resources) for Teams desktop, web, and mobile applications.</span></span>
4. <span data-ttu-id="27c96-137">通过选择Teams"范围"按钮预授权用户，在打开的面板中，输入"access_as_user"作为 **"范围名称"。**</span><span class="sxs-lookup"><span data-stu-id="27c96-137">Pre-authorize Teams by selecting the **Add a scope** button and in the panel that opens, enter **access_as_user** as the **Scope name**.</span></span>

> [!NOTE]
> <span data-ttu-id="27c96-138">您必须了解一些重要的限制：</span><span class="sxs-lookup"><span data-stu-id="27c96-138">There are some important restrictions that you must know:</span></span>
>
> * <span data-ttu-id="27c96-139">仅支持用户Graph API 权限，即电子邮件、配置文件、offline_access、OpenId。</span><span class="sxs-lookup"><span data-stu-id="27c96-139">Only user-level Graph API permissions are supported that is, email, profile, offline_access, OpenId.</span></span> <span data-ttu-id="27c96-140">如果必须有权访问其他作用域，Graph作用域，请参阅 `User.Read` `Mail.Read` 建议的[解决方法](#apps-that-require-additional-graph-scopes)。</span><span class="sxs-lookup"><span data-stu-id="27c96-140">If you must have access to other Graph scopes such as `User.Read` or `Mail.Read`, see [recommended workaround](#apps-that-require-additional-graph-scopes).</span></span>
> * <span data-ttu-id="27c96-141">应用程序的域名与为 AAD 应用程序注册的域名相同，这一点很重要。</span><span class="sxs-lookup"><span data-stu-id="27c96-141">It is important that your application's domain name is the same as the domain name you have registered for your AAD application.</span></span>
> * <span data-ttu-id="27c96-142">目前不支持每个应用多个域。</span><span class="sxs-lookup"><span data-stu-id="27c96-142">Currently multiple domains per app are not supported.</span></span>

<span data-ttu-id="27c96-143">**通过 AAD 门户注册应用**</span><span class="sxs-lookup"><span data-stu-id="27c96-143">**To register your app through the AAD portal**</span></span>

1. <span data-ttu-id="27c96-144">在 AAD 应用注册门户 [中注册新](https://go.microsoft.com/fwlink/?linkid=2083908) 应用程序。</span><span class="sxs-lookup"><span data-stu-id="27c96-144">Register a new application in the [AAD App Registrations](https://go.microsoft.com/fwlink/?linkid=2083908) portal.</span></span>
2. <span data-ttu-id="27c96-145">选择 **"新建注册"。**</span><span class="sxs-lookup"><span data-stu-id="27c96-145">Select **New Registration**.</span></span> <span data-ttu-id="27c96-146">将显示 **"注册应用程序"** 页。</span><span class="sxs-lookup"><span data-stu-id="27c96-146">The **Register an application** page appears.</span></span>
3. <span data-ttu-id="27c96-147">在 **"注册应用程序"** 页中，输入以下值：</span><span class="sxs-lookup"><span data-stu-id="27c96-147">In the **Register an application** page, enter the following values:</span></span>
    1. <span data-ttu-id="27c96-148">为 **应用输入** 名称。</span><span class="sxs-lookup"><span data-stu-id="27c96-148">Enter a **Name** for your app.</span></span>
    2. <span data-ttu-id="27c96-149">选择" **支持的帐户类型"，** 选择"单个租户"或"多租户帐户类型"。</span><span class="sxs-lookup"><span data-stu-id="27c96-149">Choose the **Supported account types**, select single tenant or multitenant account type.</span></span> <span data-ttu-id="27c96-150">¹</span><span class="sxs-lookup"><span data-stu-id="27c96-150">¹</span></span>
    * <span data-ttu-id="27c96-151">保留“重定向 URI”为空。</span><span class="sxs-lookup"><span data-stu-id="27c96-151">Leave **Redirect URI** empty.</span></span>
    3. <span data-ttu-id="27c96-152">选择“注册”。</span><span class="sxs-lookup"><span data-stu-id="27c96-152">Choose **Register**.</span></span>
4. <span data-ttu-id="27c96-153">在概述页上，复制并保存应用程序 (**客户端) ID**。</span><span class="sxs-lookup"><span data-stu-id="27c96-153">On the overview page, copy and save the **Application (client) ID**.</span></span> <span data-ttu-id="27c96-154">更新应用程序清单时，稍后必须Teams该清单。</span><span class="sxs-lookup"><span data-stu-id="27c96-154">You must have it later when updating your Teams application manifest.</span></span>
5. <span data-ttu-id="27c96-155">在“**管理**”下，选择“**公开 API**”。</span><span class="sxs-lookup"><span data-stu-id="27c96-155">Under **Manage**, select **Expose an API**.</span></span>
6. <span data-ttu-id="27c96-156">选择 **"设置**"链接以生成格式为 的应用程序 ID URI。 `api://{AppID}`</span><span class="sxs-lookup"><span data-stu-id="27c96-156">Select the **Set** link to generate the Application ID URI in the form of `api://{AppID}`.</span></span> <span data-ttu-id="27c96-157">在双正斜杠和 GUID 之间插入完全限定域名，末尾附加一个正斜杠"/"。</span><span class="sxs-lookup"><span data-stu-id="27c96-157">Insert your fully qualified domain name with a forward slash "/" appended to the end, between the double forward slashes and the GUID.</span></span> <span data-ttu-id="27c96-158">整个 ID 的形式必须为 `api://fully-qualified-domain-name.com/{AppID}` 。</span><span class="sxs-lookup"><span data-stu-id="27c96-158">The entire ID must have the form of `api://fully-qualified-domain-name.com/{AppID}`.</span></span> <span data-ttu-id="27c96-159">1。例如 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000` ， 。</span><span class="sxs-lookup"><span data-stu-id="27c96-159">² For example, `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`.</span></span> <span data-ttu-id="27c96-160">完全限定的域名是提供应用时可读的域名。</span><span class="sxs-lookup"><span data-stu-id="27c96-160">The fully qualified domain name is the human readable domain name from which your app is served.</span></span> <span data-ttu-id="27c96-161">如果使用的是隧道服务（如 ngrok），则必须在 ngrok 子域发生更改时更新此值。</span><span class="sxs-lookup"><span data-stu-id="27c96-161">If you are using a tunneling service such as ngrok, you must update this value whenever your ngrok subdomain changes.</span></span>
7. <span data-ttu-id="27c96-162">选择 **"添加范围"。**</span><span class="sxs-lookup"><span data-stu-id="27c96-162">Select **Add a scope**.</span></span> <span data-ttu-id="27c96-163">在打开的面板中，输入 **access_as_user** 作为范围 **名称**。</span><span class="sxs-lookup"><span data-stu-id="27c96-163">In the panel that opens, enter **access_as_user** as the **Scope name**.</span></span>
8. <span data-ttu-id="27c96-164">在 **"Who同意？"** 框中，输入 **"管理员和用户"。**</span><span class="sxs-lookup"><span data-stu-id="27c96-164">In the **Who can consent?** box, enter **Admins and users**.</span></span>
9. <span data-ttu-id="27c96-165">在框中输入详细信息，以使用适用于作用域的值配置管理员和用户同意 `access_as_user` 提示：</span><span class="sxs-lookup"><span data-stu-id="27c96-165">Enter the details in the boxes for configuring the admin and user consent prompts with values that are appropriate for the `access_as_user` scope:</span></span>
    * <span data-ttu-id="27c96-166">**管理员同意标题** Teams用户可以访问用户配置文件。</span><span class="sxs-lookup"><span data-stu-id="27c96-166">**Admin consent title:** Teams can access the user’s profile.</span></span>
    * <span data-ttu-id="27c96-167">**管理员同意** 说明：Teams当前用户调用应用的 Web API。</span><span class="sxs-lookup"><span data-stu-id="27c96-167">**Admin consent description**: Teams can call the app’s web APIs as the current user.</span></span>
    * <span data-ttu-id="27c96-168">**用户同意标题**：Teams可以访问你的个人资料并代表你提出请求。</span><span class="sxs-lookup"><span data-stu-id="27c96-168">**User consent title**: Teams can access your profile and make requests on your behalf.</span></span>
    * <span data-ttu-id="27c96-169">**用户同意Teams：** 用户可以使用你拥有的相同权限调用此应用的 API。</span><span class="sxs-lookup"><span data-stu-id="27c96-169">**User consent description:** Teams can call this app’s APIs with the same rights as you have.</span></span>
10. <span data-ttu-id="27c96-170">确保将“状态”设置为“已启用”。</span><span class="sxs-lookup"><span data-stu-id="27c96-170">Ensure that **State** is set to **Enabled**.</span></span>
11. <span data-ttu-id="27c96-171">选择 **"添加范围** "以保存详细信息。</span><span class="sxs-lookup"><span data-stu-id="27c96-171">Select **Add scope** to save the details.</span></span> <span data-ttu-id="27c96-172">文本字段下方显示的 **作用域** 名称的域部分必须自动匹配上一步中设置的应用程序 **ID** URI，并 `/access_as_user` 追加到末尾 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user` 。</span><span class="sxs-lookup"><span data-stu-id="27c96-172">The domain part of the **Scope name** displayed below the text field must automatically match the **Application ID** URI set in the previous step, with `/access_as_user` appended to the end `api://subdomain.example.com/00000000-0000-0000-0000-000000000000/access_as_user`.</span></span>
12. <span data-ttu-id="27c96-173">在 **"授权客户端应用程序** "部分，确定要针对应用程序的 Web 应用程序授权的应用程序。</span><span class="sxs-lookup"><span data-stu-id="27c96-173">In the **Authorized client applications** section, identify the applications that you want to authorize for your app’s web application.</span></span> <span data-ttu-id="27c96-174">选择 **"添加客户端应用程序"。**</span><span class="sxs-lookup"><span data-stu-id="27c96-174">Select **Add a client application**.</span></span> <span data-ttu-id="27c96-175">输入以下每个客户端 ID，然后选择在上一步中创建的授权作用域：</span><span class="sxs-lookup"><span data-stu-id="27c96-175">Enter each of the following client IDs and select the authorized scope you created in the previous step:</span></span>
    * <span data-ttu-id="27c96-176">`1fec8e78-bce4-4aaf-ab1b-5451cc387264`用于Teams或桌面应用程序。</span><span class="sxs-lookup"><span data-stu-id="27c96-176">`1fec8e78-bce4-4aaf-ab1b-5451cc387264` for Teams mobile or desktop application.</span></span>
    * <span data-ttu-id="27c96-177">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346`Teams Web 应用程序。</span><span class="sxs-lookup"><span data-stu-id="27c96-177">`5e3ce6c0-2b1f-4285-8d4b-75ee78787346` for Teams web application.</span></span>
13. <span data-ttu-id="27c96-178">导航到 **"API 权限"。**</span><span class="sxs-lookup"><span data-stu-id="27c96-178">Navigate to **API Permissions**.</span></span> <span data-ttu-id="27c96-179">选择 **"添加**  >  **Microsoft Graph** 委派权限"，然后从 API 添加以下  >  Graph权限：</span><span class="sxs-lookup"><span data-stu-id="27c96-179">Select **Add a permission** > **Microsoft Graph** > **Delegated permissions**, then add the following permissions from Graph API:</span></span>
    * <span data-ttu-id="27c96-180">默认情况下启用 User.Read</span><span class="sxs-lookup"><span data-stu-id="27c96-180">User.Read enabled by default</span></span>
    * <span data-ttu-id="27c96-181">email</span><span class="sxs-lookup"><span data-stu-id="27c96-181">email</span></span>
    * <span data-ttu-id="27c96-182">offline_access</span><span class="sxs-lookup"><span data-stu-id="27c96-182">offline_access</span></span>
    * <span data-ttu-id="27c96-183">OpenId</span><span class="sxs-lookup"><span data-stu-id="27c96-183">OpenId</span></span>
    * <span data-ttu-id="27c96-184">个人资料</span><span class="sxs-lookup"><span data-stu-id="27c96-184">profile</span></span>

14. <span data-ttu-id="27c96-185">导航到 **身份验证**。</span><span class="sxs-lookup"><span data-stu-id="27c96-185">Navigate to **Authentication**.</span></span>

    <span data-ttu-id="27c96-186">如果应用尚未获得 IT 管理员同意，用户第一次使用应用时必须同意。</span><span class="sxs-lookup"><span data-stu-id="27c96-186">If an app has not been granted IT admin consent, users have to provide consent the first time they use an app.</span></span>

    <span data-ttu-id="27c96-187">若要输入重定向 URI：</span><span class="sxs-lookup"><span data-stu-id="27c96-187">To enter a redirect URI:</span></span>
    * <span data-ttu-id="27c96-188">选择 **"添加平台"。**</span><span class="sxs-lookup"><span data-stu-id="27c96-188">Select **Add a platform**.</span></span>
    * <span data-ttu-id="27c96-189">选择 **"Web"。**</span><span class="sxs-lookup"><span data-stu-id="27c96-189">Select **web**.</span></span>
    * <span data-ttu-id="27c96-190">输入 **应用的重定向 URI。**</span><span class="sxs-lookup"><span data-stu-id="27c96-190">Enter the **redirect URI** for your app.</span></span> <span data-ttu-id="27c96-191">这是一个页面，其中成功的隐式授予流将重定向用户。</span><span class="sxs-lookup"><span data-stu-id="27c96-191">This is the page where a successful implicit grant flow redirects the user.</span></span> <span data-ttu-id="27c96-192">这是在步骤 5 中输入的完全限定域名，后跟发送身份验证响应的 API 路由。</span><span class="sxs-lookup"><span data-stu-id="27c96-192">This is the same fully qualified domain name that you entered in step 5 followed by the API route where an authentication response is sent.</span></span> <span data-ttu-id="27c96-193">如果您遵循任何示例Teams，则此为 `https://subdomain.example.com/auth-end` 。</span><span class="sxs-lookup"><span data-stu-id="27c96-193">If you are following any of the Teams samples, this is `https://subdomain.example.com/auth-end`.</span></span>

    <span data-ttu-id="27c96-194">通过选中以下框启用隐式授予：✔ ID 令牌✔访问令牌</span><span class="sxs-lookup"><span data-stu-id="27c96-194">Enable implicit grant by checking the following boxes: ✔ ID Token ✔ Access Token</span></span>

<span data-ttu-id="27c96-195">恭喜！</span><span class="sxs-lookup"><span data-stu-id="27c96-195">Congratulations!</span></span> <span data-ttu-id="27c96-196">已完成应用注册先决条件，可以继续选项卡 SSO 应用。</span><span class="sxs-lookup"><span data-stu-id="27c96-196">You have completed the app registration prerequisites to proceed with your tab SSO app.</span></span>

> [!NOTE]
>
> * <span data-ttu-id="27c96-197">¹ 如果你的 AAD 应用在 Teams 中进行身份验证请求的同一租户中注册，则不能要求用户同意并获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="27c96-197">¹ If your AAD app is registered in the same tenant where you are making an authentication request in Teams, the user cannot be asked to consent and is granted an access token right away.</span></span> <span data-ttu-id="27c96-198">只有在 AAD 应用注册到其他租户时，用户才同意这些权限。</span><span class="sxs-lookup"><span data-stu-id="27c96-198">Users only consent to these permissions if the AAD app is registered in a different tenant.</span></span>
> * <span data-ttu-id="27c96-199">你已经收到一个错误，指出主机名不得基于已拥有域。</span><span class="sxs-lookup"><span data-stu-id="27c96-199">² If the custom domain is not added to AAD, you get an error stating that the host name must not be based on an already owned domain.</span></span> <span data-ttu-id="27c96-200">若要将自定义域添加到 AAD 并注册它，请按照向 [AAD](/azure/active-directory/fundamentals/add-custom-domain) 添加自定义域名过程操作，然后重复步骤 5。</span><span class="sxs-lookup"><span data-stu-id="27c96-200">To add custom domain to AAD and register it, follow the [add a custom domain name to AAD](/azure/active-directory/fundamentals/add-custom-domain) procedure, and then repeat step 5.</span></span> <span data-ttu-id="27c96-201">如果未使用租户租户中的管理员凭据登录，Office 365此错误。</span><span class="sxs-lookup"><span data-stu-id="27c96-201">You can also get this error if you are not signed in with Admin credentials in the Office 365 tenancy.</span></span>
> * <span data-ttu-id="27c96-202">如果未在返回的访问令牌 (UPN) ) 用户主体名称，可以在 AAD 中将其添加为可选声明。 [](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims)</span><span class="sxs-lookup"><span data-stu-id="27c96-202">If you are not receiving the user principal name (UPN)) in the returned access token, you can add it as an [optional claim](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) in AAD.</span></span>

### <a name="2-update-your-teams-application-manifest"></a><span data-ttu-id="27c96-203">2. 更新Teams应用程序清单</span><span class="sxs-lookup"><span data-stu-id="27c96-203">2. Update your Teams application manifest</span></span>

<span data-ttu-id="27c96-204">使用以下代码将新属性添加到Teams清单：</span><span class="sxs-lookup"><span data-stu-id="27c96-204">Use the following code to add new properties to your Teams manifest:</span></span>

```json
"webApplicationInfo": {
  "id": "00000000-0000-0000-0000-000000000000",
  "resource": "api://subdomain.example.com/00000000-0000-0000-0000-000000000000"
}
```

* <span data-ttu-id="27c96-205">**WebApplicationInfo** 是以下元素的父元素：</span><span class="sxs-lookup"><span data-stu-id="27c96-205">**WebApplicationInfo** is the parent of the following elements:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="27c96-206">**id** - 应用程序的客户端 ID。</span><span class="sxs-lookup"><span data-stu-id="27c96-206">**id** - The client ID of the application.</span></span> <span data-ttu-id="27c96-207">这是在向 Azure AD 注册应用程序时获取的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="27c96-207">This is the application ID that you obtained as part of registering the application with Azure AD.</span></span>
>* <span data-ttu-id="27c96-208">**resource** - 应用程序的域和子域。</span><span class="sxs-lookup"><span data-stu-id="27c96-208">**resource** - The domain and subdomain of your application.</span></span> <span data-ttu-id="27c96-209">这是相同的 URI (包括你在步骤 `api://` 6) 注册的协议 `scope` 和协议。</span><span class="sxs-lookup"><span data-stu-id="27c96-209">This is the same URI (including the `api://` protocol) that you registered when creating your `scope` in step 6.</span></span> <span data-ttu-id="27c96-210">不得在资源 `access_as_user` 中包括路径。</span><span class="sxs-lookup"><span data-stu-id="27c96-210">You must not include the `access_as_user` path in your resource.</span></span> <span data-ttu-id="27c96-211">此 URI 的域部分必须与在应用程序清单的 URL 中使用的域（包括任何子Teams匹配。</span><span class="sxs-lookup"><span data-stu-id="27c96-211">The domain part of this URI must match the domain, including any subdomains, used in the URLs of your Teams application manifest.</span></span>

> [!NOTE]
>
>* <span data-ttu-id="27c96-212">AAD 应用的资源通常是其网站 URL 和 appID (根，例如 `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`) 。</span><span class="sxs-lookup"><span data-stu-id="27c96-212">The resource for an AAD app is usually the root of its site URL and the appID (e.g. `api://subdomain.example.com/00000000-0000-0000-0000-000000000000`).</span></span> <span data-ttu-id="27c96-213">此值还用于确保你的请求来自同一个域。</span><span class="sxs-lookup"><span data-stu-id="27c96-213">This value is also used to ensure your request is coming from the same domain.</span></span> <span data-ttu-id="27c96-214">确保选项卡 `contentURL` 的 使用与资源属性相同的域。</span><span class="sxs-lookup"><span data-stu-id="27c96-214">Ensure that the `contentURL` for your tab uses the same domains as your resource property.</span></span>
>* <span data-ttu-id="27c96-215">必须使用清单版本 1.5 或更高版本来实现 `webApplicationInfo` 字段。</span><span class="sxs-lookup"><span data-stu-id="27c96-215">You must use manifest version 1.5 or higher to implement the `webApplicationInfo` field.</span></span>

### <a name="3-get-an-authentication-token-from-your-client-side-code"></a><span data-ttu-id="27c96-216">3. 从客户端代码获取身份验证令牌</span><span class="sxs-lookup"><span data-stu-id="27c96-216">3. Get an authentication token from your client-side code</span></span>

<span data-ttu-id="27c96-217">使用以下身份验证 API：</span><span class="sxs-lookup"><span data-stu-id="27c96-217">Use the following authentication API:</span></span>

```javascript
var authTokenRequest = {
  successCallback: function(result) { console.log("Success: " + result); },
  failureCallback: function(error) { console.log("Failure: " + error); }
};
microsoftTeams.authentication.getAuthToken(authTokenRequest);
```

<span data-ttu-id="27c96-218">调用 时，用户级别权限需要其他用户同意，将显示一个对话框，以向用户授予 `getAuthToken` 其他同意。</span><span class="sxs-lookup"><span data-stu-id="27c96-218">When you call `getAuthToken` - and additional user consent is required for user-level permissions, a dialog is shown to the user to grant additional consent.</span></span>

<span data-ttu-id="27c96-219">在成功回调中收到访问令牌后，可以解码访问令牌以查看与该令牌关联的声明。</span><span class="sxs-lookup"><span data-stu-id="27c96-219">After you receive the access token in the success callback, you can decode the access token to view the claims associated with that token.</span></span> <span data-ttu-id="27c96-220">（可选）你可以手动将访问令牌复制并粘贴到工具中，jwt.ms 检查其内容[](https://jwt.ms/)。</span><span class="sxs-lookup"><span data-stu-id="27c96-220">Optionally, you can manually copy and paste the access token into a tool, such as [jwt.ms](https://jwt.ms/) to inspect its contents.</span></span> <span data-ttu-id="27c96-221">如果未在返回的访问令牌中接收 UPN，可以在 AAD 中将其添加为[](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims)可选声明。</span><span class="sxs-lookup"><span data-stu-id="27c96-221">If you are not receiving the UPN in the returned access token, you can add it as an [optional claim](https://docs.microsoft.com/azure/active-directory/develop/active-directory-optional-claims) in AAD.</span></span>

<p>
    <img src="~/assets/images/tabs/tabs-sso-prompt.png" alt="Tab single sign-on SSO dialog prompt" width="75%"/>
</p>

## <a name="code-sample"></a><span data-ttu-id="27c96-222">代码示例</span><span class="sxs-lookup"><span data-stu-id="27c96-222">Code sample</span></span>

|<span data-ttu-id="27c96-223">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="27c96-223">**Sample name**</span></span>|<span data-ttu-id="27c96-224">**说明**</span><span class="sxs-lookup"><span data-stu-id="27c96-224">**Description**</span></span>|<span data-ttu-id="27c96-225">**C#**</span><span class="sxs-lookup"><span data-stu-id="27c96-225">**C#**</span></span>|<span data-ttu-id="27c96-226">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="27c96-226">**Node.js**</span></span>|
|---------------|---------------|------|--------------|
| <span data-ttu-id="27c96-227">选项卡 SSO</span><span class="sxs-lookup"><span data-stu-id="27c96-227">Tab SSO</span></span> |<span data-ttu-id="27c96-228">Microsoft Teams Azure AD SSO 的选项卡示例应用</span><span class="sxs-lookup"><span data-stu-id="27c96-228">Microsoft Teams sample app for tabs Azure AD SSO</span></span>| [<span data-ttu-id="27c96-229">View</span><span class="sxs-lookup"><span data-stu-id="27c96-229">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-sso/csharp)|<span data-ttu-id="27c96-230">[查看](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs)、</span><span class="sxs-lookup"><span data-stu-id="27c96-230">[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/blob/main/samples/tab-sso/nodejs),</span></span> </br>[<span data-ttu-id="27c96-231">Teams Toolkit</span><span class="sxs-lookup"><span data-stu-id="27c96-231">Teams Toolkit</span></span>](../../../toolkit/visual-studio-code-tab-sso.md)|

## <a name="known-limitations"></a><span data-ttu-id="27c96-232">已知限制</span><span class="sxs-lookup"><span data-stu-id="27c96-232">Known limitations</span></span>

### <a name="apps-that-require-additional-graph-scopes"></a><span data-ttu-id="27c96-233">需要其他作用域Graph应用</span><span class="sxs-lookup"><span data-stu-id="27c96-233">Apps that require additional Graph scopes</span></span>

<span data-ttu-id="27c96-234">我们的 SSO 当前实现仅授予用户级别权限（即电子邮件、配置文件、offline_access、OpenId）的许可，而不允许授予其他 API（如 User.Read 或 Mail.Read）的许可。</span><span class="sxs-lookup"><span data-stu-id="27c96-234">Our current implementation for SSO only grants consent for user-level permissions that is email, profile, offline_access, OpenId and not for other APIs such as User.Read or Mail.Read.</span></span> <span data-ttu-id="27c96-235">如果你的应用需要进一步Graph范围，下一部分将提供一些启用的解决方法。</span><span class="sxs-lookup"><span data-stu-id="27c96-235">If your app needs further Graph scopes, the next section provides some enabling workarounds.</span></span>

#### <a name="tenant-admin-consent"></a><span data-ttu-id="27c96-236">租户管理员同意</span><span class="sxs-lookup"><span data-stu-id="27c96-236">Tenant Admin Consent</span></span>

<span data-ttu-id="27c96-237">最简单的方法是让租户管理员代表组织预先同意。</span><span class="sxs-lookup"><span data-stu-id="27c96-237">The simplest approach is to get a tenant admin to pre-consent on behalf of the organization.</span></span> <span data-ttu-id="27c96-238">这意味着用户不需要同意这些作用域，然后可以使用 AAD 的代表流自由交换令牌 [服务器端](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow)。</span><span class="sxs-lookup"><span data-stu-id="27c96-238">This means users do not have to consent to these scopes and you can then be free to exchange the token server side using AAD’s [on-behalf-of flow](/azure/active-directory/develop/v1-oauth2-on-behalf-of-flow).</span></span> <span data-ttu-id="27c96-239">此解决方法对于内部业务线应用程序是可接受的，但不足以供无法依赖租户管理员审批的第三方开发人员使用。</span><span class="sxs-lookup"><span data-stu-id="27c96-239">This workaround is acceptable for internal line-of-business applications but is not enough for third-party developers who are not able to rely on tenant admin approval.</span></span>

<span data-ttu-id="27c96-240">代表组织作为租户管理员同意的一种简单方法就是引用 `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>` 。</span><span class="sxs-lookup"><span data-stu-id="27c96-240">A simple way of consenting on behalf of an organization as a tenant admin is to refer to `https://login.microsoftonline.com/common/adminconsent?client_id=<AAD_App_ID>`.</span></span>

#### <a name="ask-for-additional-consent-using-the-auth-api"></a><span data-ttu-id="27c96-241">使用身份验证 API 请求其他同意</span><span class="sxs-lookup"><span data-stu-id="27c96-241">Ask for additional consent using the Auth API</span></span>

<span data-ttu-id="27c96-242">获取其他Graph范围的另一个方法是使用我们现有的基于 Web 的[Azure AD](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page)身份验证方法显示同意对话框，该方法涉及弹出 Azure AD 同意对话框。</span><span class="sxs-lookup"><span data-stu-id="27c96-242">Another approach for getting additional Graph scopes is to present a consent dialog using our existing [web-based Azure AD authentication approach](~/tabs/how-to/authentication/auth-tab-aad.md#navigate-to-the-authorization-page-from-your-popup-page) which involves popping up an Azure AD consent dialog box.</span></span> 

<span data-ttu-id="27c96-243">**使用身份验证 API 请求其他同意**</span><span class="sxs-lookup"><span data-stu-id="27c96-243">**To ask for additional consent using the Auth API**</span></span>

1. <span data-ttu-id="27c96-244">使用 检索到的令牌需要使用 AAD 代表流在服务器端进行交换，才能访问这些附加 Graph `getAuthToken()` API。 [](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow)</span><span class="sxs-lookup"><span data-stu-id="27c96-244">The token retrieved using `getAuthToken()` needs to be exchanged server-side using AAD [on-behalf-of flow](/azure/active-directory/develop/v2-oauth2-on-behalf-of-flow) to get access to those additional Graph APIs.</span></span> <span data-ttu-id="27c96-245">确保对此 exchange 使用 v2 Graph终结点。</span><span class="sxs-lookup"><span data-stu-id="27c96-245">Ensure you use the v2 Graph endpoint for this exchange.</span></span>
2. <span data-ttu-id="27c96-246">如果交换失败，AAD 将返回无效的授予异常。</span><span class="sxs-lookup"><span data-stu-id="27c96-246">If the exchange fails, AAD returns an invalid grant exception.</span></span> <span data-ttu-id="27c96-247">通常有两条错误消息中的一条或 `invalid_grant` `interaction_required` 。</span><span class="sxs-lookup"><span data-stu-id="27c96-247">There are usually one of two error messages, `invalid_grant` or `interaction_required`.</span></span>
3. <span data-ttu-id="27c96-248">当交换失败时，必须请求其他同意。</span><span class="sxs-lookup"><span data-stu-id="27c96-248">When the exchange fails, you must ask for additional consent.</span></span> <span data-ttu-id="27c96-249">在 UI (显示) 要求用户授予其他同意。</span><span class="sxs-lookup"><span data-stu-id="27c96-249">Show some user interface (UI) asking the user to grant additional consent.</span></span> <span data-ttu-id="27c96-250">此 UI 必须包含使用 AAD 身份验证 API 触发 [AAD 同意对话框的按钮](~/concepts/authentication/auth-silent-aad.md)。</span><span class="sxs-lookup"><span data-stu-id="27c96-250">This UI must include a button that triggers an AAD consent dialog box using our [AAD authentication API](~/concepts/authentication/auth-silent-aad.md).</span></span>
4. <span data-ttu-id="27c96-251">请求 AAD 的其他同意时，必须在 `prompt=consent` 查询 [字符串参数](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) 中包括 AAD，否则 AAD 不要求其他范围。</span><span class="sxs-lookup"><span data-stu-id="27c96-251">When asking for additional consent from AAD, you must include `prompt=consent` in your [query-string-parameter](~/tabs/how-to/authentication/auth-silent-aad.md#get-the-user-context) to AAD, otherwise AAD does not ask for the additional scopes.</span></span>
    * <span data-ttu-id="27c96-252">而不是 `?scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="27c96-252">Instead of `?scope={scopes}`</span></span>
    * <span data-ttu-id="27c96-253">使用此 `?prompt=consent&scope={scopes}`</span><span class="sxs-lookup"><span data-stu-id="27c96-253">Use this `?prompt=consent&scope={scopes}`</span></span>
    * <span data-ttu-id="27c96-254">确保 `{scopes}` 包括提示用户的所有范围，例如 Mail.Read 或 User.Read。</span><span class="sxs-lookup"><span data-stu-id="27c96-254">Ensure that `{scopes}` includes all the scopes you are prompting the user for, for example, Mail.Read or User.Read.</span></span>
5. <span data-ttu-id="27c96-255">在用户授予其他权限后，重试代表流获取这些附加 API 的访问权限。</span><span class="sxs-lookup"><span data-stu-id="27c96-255">Once the user has granted additional permission, retry the on-behalf-of-flow to get access to these additional APIs.</span></span>

### <a name="non-aad-authentication"></a><span data-ttu-id="27c96-256">非 AAD 身份验证</span><span class="sxs-lookup"><span data-stu-id="27c96-256">Non-AAD authentication</span></span>

<span data-ttu-id="27c96-257">上述身份验证解决方案仅适用于支持 AAD 作为标识提供程序的应用和服务。</span><span class="sxs-lookup"><span data-stu-id="27c96-257">The above-described authentication solution only works for apps and services that support AAD as an identity provider.</span></span> <span data-ttu-id="27c96-258">想要使用基于非 AAD 的服务进行身份验证的应用必须继续使用基于弹出窗口的 [Web 身份验证流](~/concepts/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="27c96-258">Apps that want to authenticate using non-AAD based services must continue using the pop-up-based [web authentication flow](~/concepts/authentication.md).</span></span>

> [!NOTE]
> <span data-ttu-id="27c96-259">AAD B2C 租户内的客户拥有的应用支持 SSO。</span><span class="sxs-lookup"><span data-stu-id="27c96-259">SSO is supported for customer owned apps within the AAD B2C tenants.</span></span>
