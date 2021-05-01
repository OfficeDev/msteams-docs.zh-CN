---
title: 资源特定许可Teams
description: 介绍资源特定的Teams以及如何利用它。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: teams 授权 OAuth SSO AAD rsc Graph
ms.openlocfilehash: 39e5c1bb8375fb5b5a3bd3900cb6ad870a3ff677
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101791"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="19a72-104">RSC (资源特定的) </span><span class="sxs-lookup"><span data-stu-id="19a72-104">Resource-specific consent (RSC)</span></span>

<span data-ttu-id="19a72-105">RSC) 是一种 Microsoft Teams 和 Microsoft Graph API 集成，它使你的应用可以使用 API 终结点来管理组织中特定的团队 (。</span><span class="sxs-lookup"><span data-stu-id="19a72-105">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="19a72-106">使用 RSC (权限) 特定于资源的同意，团队所有者可以授予应用程序访问和/或修改团队数据的许可。</span><span class="sxs-lookup"><span data-stu-id="19a72-106">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="19a72-107">具体、Teams特定的 RSC 权限定义应用程序可以在特定团队中执行哪些操作：</span><span class="sxs-lookup"><span data-stu-id="19a72-107">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="19a72-108">特定于资源的权限</span><span class="sxs-lookup"><span data-stu-id="19a72-108">Resource-specific permissions</span></span>

|<span data-ttu-id="19a72-109">应用权限</span><span class="sxs-lookup"><span data-stu-id="19a72-109">Application permission</span></span>| <span data-ttu-id="19a72-110">Action</span><span class="sxs-lookup"><span data-stu-id="19a72-110">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="19a72-111">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="19a72-111">TeamSettings.Read.Group</span></span> | <span data-ttu-id="19a72-112">获取此团队的设置。</span><span class="sxs-lookup"><span data-stu-id="19a72-112">Get the settings for this team.</span></span>|
|<span data-ttu-id="19a72-113">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="19a72-113">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="19a72-114">更新此团队的设置。</span><span class="sxs-lookup"><span data-stu-id="19a72-114">Update the settings for this team.</span></span>|
|<span data-ttu-id="19a72-115">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="19a72-115">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="19a72-116">获取此团队的频道名称、频道说明和频道设置。</span><span class="sxs-lookup"><span data-stu-id="19a72-116">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="19a72-117">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="19a72-117">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="19a72-118">更新此团队的频道名称、频道说明和频道设置。</span><span class="sxs-lookup"><span data-stu-id="19a72-118">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="19a72-119">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="19a72-119">Channel.Create.Group</span></span>|<span data-ttu-id="19a72-120">在这个团队中创建频道。</span><span class="sxs-lookup"><span data-stu-id="19a72-120">Create channels in this team.</span></span>|
|<span data-ttu-id="19a72-121">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="19a72-121">Channel.Delete.Group</span></span>|<span data-ttu-id="19a72-122">删除此团队中的频道。</span><span class="sxs-lookup"><span data-stu-id="19a72-122">Delete channels in this team.</span></span>|
|<span data-ttu-id="19a72-123">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="19a72-123">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="19a72-124">获取此团队的频道消息。</span><span class="sxs-lookup"><span data-stu-id="19a72-124">Get this team's channel messages.</span></span>|
|<span data-ttu-id="19a72-125">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="19a72-125">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="19a72-126">获取此团队已安装应用的列表。</span><span class="sxs-lookup"><span data-stu-id="19a72-126">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="19a72-127">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="19a72-127">TeamsTab.Read.Group</span></span>|<span data-ttu-id="19a72-128">获取此团队的选项卡列表。</span><span class="sxs-lookup"><span data-stu-id="19a72-128">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="19a72-129">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="19a72-129">TeamsTab.Create.Group</span></span>|<span data-ttu-id="19a72-130">在此团队中创建选项卡。</span><span class="sxs-lookup"><span data-stu-id="19a72-130">Create tabs in this team.</span></span>|
|<span data-ttu-id="19a72-131">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="19a72-131">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="19a72-132">更新此团队的选项卡。</span><span class="sxs-lookup"><span data-stu-id="19a72-132">Update this team's tabs.</span></span>|
|<span data-ttu-id="19a72-133">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="19a72-133">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="19a72-134">删除此团队的选项卡。</span><span class="sxs-lookup"><span data-stu-id="19a72-134">Delete this team's tabs.</span></span>|
|<span data-ttu-id="19a72-135">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="19a72-135">TeamMember.Read.Group</span></span>|<span data-ttu-id="19a72-136">获取此团队的成员。</span><span class="sxs-lookup"><span data-stu-id="19a72-136">Get this team's members.</span></span>|

>[!NOTE]
><span data-ttu-id="19a72-137">特定于资源的权限仅适用于安装在 Teams 客户端上的Teams应用，并且当前不是 Azure Active Directory 门户的一部分。</span><span class="sxs-lookup"><span data-stu-id="19a72-137">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="19a72-138">在应用程序中启用特定于资源的同意</span><span class="sxs-lookup"><span data-stu-id="19a72-138">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="19a72-139">在应用程序中启用 RSC 的步骤如下所示：</span><span class="sxs-lookup"><span data-stu-id="19a72-139">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="19a72-140">[在组门户 中配置组所有者Azure Active Directory设置](#configure-group-owner-consent-settings-in-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="19a72-140">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="19a72-141">[通过 Azure AD Microsoft 标识平台注册应用](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="19a72-141">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="19a72-142">[查看 Azure AD 门户中的应用程序权限](#review-your-application-permissions-in-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="19a72-142">[Review your application permissions in the Azure AD portal](#review-your-application-permissions-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="19a72-143">[从 Microsoft Identity 平台获取访问令牌](#obtain-an-access-token-from-the-microsoft-identity-platform)。</span><span class="sxs-lookup"><span data-stu-id="19a72-143">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="19a72-144">[更新应用Teams清单](#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="19a72-144">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="19a72-145">[直接在 Teams 中安装应用](#sideload-your-app-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="19a72-145">[Install your app directly in Teams](#sideload-your-app-in-teams).</span></span>
1. <span data-ttu-id="19a72-146">[检查应用是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions)。</span><span class="sxs-lookup"><span data-stu-id="19a72-146">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="19a72-147">在 Azure AD 门户中配置组所有者同意设置</span><span class="sxs-lookup"><span data-stu-id="19a72-147">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="19a72-148">可以直接在 Azure 门户 [中启用](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) 或禁用组所有者同意：</span><span class="sxs-lookup"><span data-stu-id="19a72-148">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="19a72-149">以全局管理员/公司管理员登录 [Azure](https://portal.azure.com) [门户](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)。</span><span class="sxs-lookup"><span data-stu-id="19a72-149">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="19a72-150">[选择](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)**Azure Active Directory Enterprise**  =>    =>  **同意和权限**  =>  **用户同意设置"。**</span><span class="sxs-lookup"><span data-stu-id="19a72-150">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="19a72-151">使用标记为组所有者同意的控件启用、禁用或限制用户同意访问数据 (默认值为允许组所有者同意所有组所有者) 。 </span><span class="sxs-lookup"><span data-stu-id="19a72-151">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data** (The default is **Allow group owner consent for all group owners**).</span></span> <span data-ttu-id="19a72-152">对于使用 RSC 安装应用的团队所有者，必须为该用户启用组所有者同意。</span><span class="sxs-lookup"><span data-stu-id="19a72-152">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

![azure rsc 配置](../../assets/images/azure-rsc-configuration.png)

<span data-ttu-id="19a72-154">若要使用 PowerShell 启用或禁用组所有者同意，请按照使用 PowerShell 配置组所有者 [同意中概述的步骤操作](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="19a72-154">To enable or disable group owner consent using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="19a72-155">通过 Azure AD Microsoft 标识平台注册应用</span><span class="sxs-lookup"><span data-stu-id="19a72-155">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="19a72-156">Azure Active Directory门户提供了一个中央平台，用于注册和配置应用。</span><span class="sxs-lookup"><span data-stu-id="19a72-156">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="19a72-157">应用必须在 Azure AD 门户中注册，才能与 Microsoft 标识平台 并调用 Microsoft Graph API。</span><span class="sxs-lookup"><span data-stu-id="19a72-157">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="19a72-158">*请参阅*[向应用程序注册Microsoft 标识平台。](/graph/auth-register-app-v2)</span><span class="sxs-lookup"><span data-stu-id="19a72-158">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="19a72-159">不要将多个Teams应用注册到同一 Azure AD 应用 ID。应用 ID 对于每个应用必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="19a72-159">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="19a72-160">尝试将多个应用安装到同一应用 ID 将失败。</span><span class="sxs-lookup"><span data-stu-id="19a72-160">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="19a72-161">在 Azure AD 门户中查看应用程序权限</span><span class="sxs-lookup"><span data-stu-id="19a72-161">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="19a72-162">导航到 **"主页**  =>  **应用注册"** 页并选择 RSC 应用。</span><span class="sxs-lookup"><span data-stu-id="19a72-162">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="19a72-163">从 **左侧导航** 栏中选择 API 权限，并检查应用的已配置权限列表。</span><span class="sxs-lookup"><span data-stu-id="19a72-163">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="19a72-164">如果你的应用将仅执行 RSC Graph API 调用，请删除该页面上的所有权限。</span><span class="sxs-lookup"><span data-stu-id="19a72-164">If your app will only make RSC Graph API calls, delete all the permission on that page.</span></span> <span data-ttu-id="19a72-165">如果你的应用还将进行非 RSC 调用，请根据需要保留这些权限。</span><span class="sxs-lookup"><span data-stu-id="19a72-165">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="19a72-166">Azure AD 门户不能用于请求 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="19a72-166">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="19a72-167">RSC 权限当前专用于安装在 Teams 客户端中的 Teams 应用程序，并且这些权限在应用程序清单 (JSON) 文件中声明。</span><span class="sxs-lookup"><span data-stu-id="19a72-167">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="19a72-168">从应用程序获取访问Microsoft 标识平台</span><span class="sxs-lookup"><span data-stu-id="19a72-168">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="19a72-169">若要Graph API 调用，必须从标识平台获取应用的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="19a72-169">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="19a72-170">应用必须先在 Azure AD 门户Microsoft 标识平台令牌，然后才能从应用获取令牌。</span><span class="sxs-lookup"><span data-stu-id="19a72-170">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="19a72-171">访问令牌包含你的应用的相关信息，还有它就可通过 Microsoft Graph 访问的资源和 API 所具备的权限。</span><span class="sxs-lookup"><span data-stu-id="19a72-171">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="19a72-172">你需要从 Azure AD 注册过程获取以下值，以从标识平台检索访问令牌：</span><span class="sxs-lookup"><span data-stu-id="19a72-172">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="19a72-173">应用注册门户分配的应用程序 **ID。**</span><span class="sxs-lookup"><span data-stu-id="19a72-173">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="19a72-174">如果你的应用支持单一登录 (SSO) 应用和 SSO 应使用相同的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="19a72-174">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="19a72-175">客户端 **密码/密码** 或公钥/私钥对 (**证书) 。**</span><span class="sxs-lookup"><span data-stu-id="19a72-175">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="19a72-176">这不是本机应用的必需项。</span><span class="sxs-lookup"><span data-stu-id="19a72-176">This is not required for native apps.</span></span>
- <span data-ttu-id="19a72-177">重定向 **URI** (或回复 URL) 应用接收来自 Azure AD 的响应。</span><span class="sxs-lookup"><span data-stu-id="19a72-177">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="19a72-178">*请参阅*[代表用户获取访问权限和](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true)[在没有用户的情况下获取访问权限](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="19a72-178">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="19a72-179">更新Teams应用程序清单</span><span class="sxs-lookup"><span data-stu-id="19a72-179">Update your Teams app manifest</span></span>

<span data-ttu-id="19a72-180">RSC 权限在应用清单 (JSON) 文件中声明。</span><span class="sxs-lookup"><span data-stu-id="19a72-180">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="19a72-181">将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：</span><span class="sxs-lookup"><span data-stu-id="19a72-181">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="19a72-182">**id**  — Azure AD 应用 ID。 *请参阅* 在 [Azure AD 门户中注册应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="19a72-182">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="19a72-183">**resource**  — 任何字符串。</span><span class="sxs-lookup"><span data-stu-id="19a72-183">**resource**  — any string.</span></span> <span data-ttu-id="19a72-184">此字段在 RSC 中没有任何操作，但必须添加该字段，并且必须具有值以避免错误响应;任何字符串将执行。</span><span class="sxs-lookup"><span data-stu-id="19a72-184">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="19a72-185">**应用程序权限** — 应用的 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="19a72-185">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="19a72-186">*请参阅*[特定于资源的权限](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="19a72-186">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="19a72-187">非 RSC 权限存储在 Azure 门户中。</span><span class="sxs-lookup"><span data-stu-id="19a72-187">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="19a72-188">不要将它们添加到应用清单。</span><span class="sxs-lookup"><span data-stu-id="19a72-188">Do not add them to the app manifest.</span></span>
>

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelMessage.Read.Group",
      "TeamSettings.Edit.Group",
      "ChannelSettings.ReadWrite.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.ReadWrite.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group"
    ]
  }
```

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="19a72-189">在应用程序中旁加载Teams</span><span class="sxs-lookup"><span data-stu-id="19a72-189">Sideload your app in Teams</span></span>

<span data-ttu-id="19a72-190">如果你Teams允许自定义应用上传，你可以将应用直接旁加载到特定[](~/concepts/deploy-and-publish/apps-upload.md)团队。</span><span class="sxs-lookup"><span data-stu-id="19a72-190">If your Teams admin allows custom app uploads, you can [sideload your app](~/concepts/deploy-and-publish/apps-upload.md) directly to a specific team.</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="19a72-191">检查应用是否添加了 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="19a72-191">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="19a72-192">RSC 权限不归为用户。</span><span class="sxs-lookup"><span data-stu-id="19a72-192">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="19a72-193">调用使用应用程序权限而不是用户委派权限进行。</span><span class="sxs-lookup"><span data-stu-id="19a72-193">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="19a72-194">因此，可以允许应用执行用户无法执行的操作，例如创建频道或删除选项卡。在调用 RSC API 之前，应查看团队所有者对用例的意图。</span><span class="sxs-lookup"><span data-stu-id="19a72-194">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="19a72-195">*请参阅* [Microsoft Teams API 概述](/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="19a72-195">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="19a72-196">将应用安装到团队后，可以使用Graph[资源管理器](https://developer.microsoft.com/graph/graph-explorer)查看已授予团队中应用的权限：</span><span class="sxs-lookup"><span data-stu-id="19a72-196">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="19a72-197">从客户端获取团队的 **groupId** Teams Id。</span><span class="sxs-lookup"><span data-stu-id="19a72-197">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="19a72-198">在Teams客户端中，Teams **左侧导航** 栏选择"导航"。</span><span class="sxs-lookup"><span data-stu-id="19a72-198">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="19a72-199">从下拉菜单中选择安装应用的团队。</span><span class="sxs-lookup"><span data-stu-id="19a72-199">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="19a72-200">选择" **更多选项"** 图标 (&#8943;) 。</span><span class="sxs-lookup"><span data-stu-id="19a72-200">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="19a72-201">选择 **获取团队链接**。</span><span class="sxs-lookup"><span data-stu-id="19a72-201">Select **Get link to team**.</span></span>
> - <span data-ttu-id="19a72-202">复制并保存字符串中的 **groupId** 值。</span><span class="sxs-lookup"><span data-stu-id="19a72-202">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="19a72-203">登录到 **Graph 资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="19a72-203">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="19a72-204">对以下 **终结点** 进行 GET 调用 `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` ：。</span><span class="sxs-lookup"><span data-stu-id="19a72-204">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="19a72-205">响应中的 clientAppId 字段将映射到在应用程序清单Teams appId。</span><span class="sxs-lookup"><span data-stu-id="19a72-205">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>
  <span data-ttu-id="19a72-206">![Graph GET 调用的浏览器响应。](../../assets/images/graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="19a72-206">![Graph explorer response to GET call.](../../assets/images/graph-permissions.png)</span></span>

## <a name="code-sample"></a><span data-ttu-id="19a72-207">代码示例</span><span class="sxs-lookup"><span data-stu-id="19a72-207">Code sample</span></span>
| <span data-ttu-id="19a72-208">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="19a72-208">**Sample name**</span></span> | <span data-ttu-id="19a72-209">**说明**</span><span class="sxs-lookup"><span data-stu-id="19a72-209">**Description**</span></span> | <span data-ttu-id="19a72-210">**.NET**</span><span class="sxs-lookup"><span data-stu-id="19a72-210">**.NET**</span></span> |<span data-ttu-id="19a72-211">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="19a72-211">**Node.js**</span></span> |
|-----------------|-----------------|----------------|----------------|
| <span data-ttu-id="19a72-212">RSC (资源特定) </span><span class="sxs-lookup"><span data-stu-id="19a72-212">Resource Specific Consent (RSC)</span></span> | <span data-ttu-id="19a72-213">使用 RSC 调用Graph API。</span><span class="sxs-lookup"><span data-stu-id="19a72-213">Use RSC to call Graph APIs.</span></span> | [<span data-ttu-id="19a72-214">View</span><span class="sxs-lookup"><span data-stu-id="19a72-214">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[<span data-ttu-id="19a72-215">View</span><span class="sxs-lookup"><span data-stu-id="19a72-215">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="test-resource-specific-consent"></a><span data-ttu-id="19a72-216">测试特定于资源的同意</span><span class="sxs-lookup"><span data-stu-id="19a72-216">Test resource-specific consent</span></span>
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="19a72-217">**在应用程序内测试特定于资源的许可Teams**</span><span class="sxs-lookup"><span data-stu-id="19a72-217">**Test resource-specific consent permissions in Teams**</span></span>](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="19a72-218">有关管理员Teams主题</span><span class="sxs-lookup"><span data-stu-id="19a72-218">Related topic for Teams administrators</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="19a72-219">**管理员许可中Microsoft Teams特定资源的同意**</span><span class="sxs-lookup"><span data-stu-id="19a72-219">**Resource-specific consent in Microsoft Teams for admins**</span></span>](/MicrosoftTeams/resource-specific-consent)
> 

