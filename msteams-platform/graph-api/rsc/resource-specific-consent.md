---
title: Teams 中特定于资源的同意
description: 介绍 Teams 中特定于资源的同意以及如何利用它。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: teams 授权 OAuth SSO AAD rsc Graph
ms.openlocfilehash: cf57637dac91fae14473a831e76f868f458d8f27
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596215"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="8115f-104">RSC (资源特定的) </span><span class="sxs-lookup"><span data-stu-id="8115f-104">Resource-specific consent (RSC)</span></span>

<span data-ttu-id="8115f-105">RSC (特定于资源的) 是 Microsoft Teams 和 Microsoft Graph API 集成，使你的应用可以使用 API 终结点来管理组织内的特定团队。</span><span class="sxs-lookup"><span data-stu-id="8115f-105">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="8115f-106">使用 RSC (权限) 特定于资源的同意，团队所有者可以授予应用程序访问和/或修改团队数据的许可。</span><span class="sxs-lookup"><span data-stu-id="8115f-106">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="8115f-107">特定于 Teams 的精细 RSC 权限定义应用程序可以在特定团队中执行哪些操作：</span><span class="sxs-lookup"><span data-stu-id="8115f-107">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="8115f-108">特定于资源的权限</span><span class="sxs-lookup"><span data-stu-id="8115f-108">Resource-specific permissions</span></span>

|<span data-ttu-id="8115f-109">应用权限</span><span class="sxs-lookup"><span data-stu-id="8115f-109">Application permission</span></span>| <span data-ttu-id="8115f-110">操作</span><span class="sxs-lookup"><span data-stu-id="8115f-110">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="8115f-111">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="8115f-111">TeamSettings.Read.Group</span></span> | <span data-ttu-id="8115f-112">获取此团队的设置。</span><span class="sxs-lookup"><span data-stu-id="8115f-112">Get the settings for this team.</span></span>|
|<span data-ttu-id="8115f-113">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="8115f-113">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="8115f-114">更新此团队的设置。</span><span class="sxs-lookup"><span data-stu-id="8115f-114">Update the settings for this team.</span></span>|
|<span data-ttu-id="8115f-115">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="8115f-115">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="8115f-116">获取此团队的频道名称、频道说明和频道设置。</span><span class="sxs-lookup"><span data-stu-id="8115f-116">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="8115f-117">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="8115f-117">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="8115f-118">更新此团队的频道名称、频道说明和频道设置。</span><span class="sxs-lookup"><span data-stu-id="8115f-118">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="8115f-119">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="8115f-119">Channel.Create.Group</span></span>|<span data-ttu-id="8115f-120">在这个团队中创建频道。</span><span class="sxs-lookup"><span data-stu-id="8115f-120">Create channels in this team.</span></span>|
|<span data-ttu-id="8115f-121">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="8115f-121">Channel.Delete.Group</span></span>|<span data-ttu-id="8115f-122">删除此团队中的频道。</span><span class="sxs-lookup"><span data-stu-id="8115f-122">Delete channels in this team.</span></span>|
|<span data-ttu-id="8115f-123">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="8115f-123">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="8115f-124">获取此团队的频道消息。</span><span class="sxs-lookup"><span data-stu-id="8115f-124">Get this team's channel messages.</span></span>|
|<span data-ttu-id="8115f-125">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="8115f-125">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="8115f-126">获取此团队已安装应用的列表。</span><span class="sxs-lookup"><span data-stu-id="8115f-126">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="8115f-127">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="8115f-127">TeamsTab.Read.Group</span></span>|<span data-ttu-id="8115f-128">获取此团队的选项卡列表。</span><span class="sxs-lookup"><span data-stu-id="8115f-128">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="8115f-129">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="8115f-129">TeamsTab.Create.Group</span></span>|<span data-ttu-id="8115f-130">在此团队中创建选项卡。</span><span class="sxs-lookup"><span data-stu-id="8115f-130">Create tabs in this team.</span></span>|
|<span data-ttu-id="8115f-131">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="8115f-131">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="8115f-132">更新此团队的选项卡。</span><span class="sxs-lookup"><span data-stu-id="8115f-132">Update this team's tabs.</span></span>|
|<span data-ttu-id="8115f-133">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="8115f-133">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="8115f-134">删除此团队的选项卡。</span><span class="sxs-lookup"><span data-stu-id="8115f-134">Delete this team's tabs.</span></span>|
|<span data-ttu-id="8115f-135">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="8115f-135">TeamMember.Read.Group</span></span>|<span data-ttu-id="8115f-136">获取此团队的成员。</span><span class="sxs-lookup"><span data-stu-id="8115f-136">Get this team's members.</span></span>|

>[!NOTE]
><span data-ttu-id="8115f-137">特定于资源的权限仅适用于安装在 Teams 客户端上的 Teams 应用，并且当前不是 Azure Active Directory 门户的一部分。</span><span class="sxs-lookup"><span data-stu-id="8115f-137">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="8115f-138">在应用程序中启用特定于资源的同意</span><span class="sxs-lookup"><span data-stu-id="8115f-138">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="8115f-139">在应用程序中启用 RSC 的步骤如下所示：</span><span class="sxs-lookup"><span data-stu-id="8115f-139">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="8115f-140">[在 Azure Active Directory 门户](#configure-group-owner-consent-settings-in-the-azure-ad-portal)中配置组所有者同意设置。</span><span class="sxs-lookup"><span data-stu-id="8115f-140">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="8115f-141">[通过 Azure AD 门户向 Microsoft 标识平台注册应用](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="8115f-141">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="8115f-142">[查看 Azure AD 门户中的应用程序权限](#review-your-application-permissions-in-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="8115f-142">[Review your application permissions in the Azure AD portal](#review-your-application-permissions-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="8115f-143">[从 Microsoft Identity 平台获取访问令牌](#obtain-an-access-token-from-the-microsoft-identity-platform)。</span><span class="sxs-lookup"><span data-stu-id="8115f-143">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="8115f-144">[更新 Teams 应用清单](#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="8115f-144">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="8115f-145">[直接在 Teams 中安装应用](#install-your-app-directly-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="8115f-145">[Install your app directly in Teams](#install-your-app-directly-in-teams).</span></span>
1. <span data-ttu-id="8115f-146">[检查应用是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions)。</span><span class="sxs-lookup"><span data-stu-id="8115f-146">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="8115f-147">在 Azure AD 门户中配置组所有者同意设置</span><span class="sxs-lookup"><span data-stu-id="8115f-147">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="8115f-148">可以直接在 Azure 门户 [中启用](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) 或禁用组所有者同意：</span><span class="sxs-lookup"><span data-stu-id="8115f-148">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="8115f-149">以全局管理员/公司管理员登录 [Azure](https://portal.azure.com) [门户](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)。</span><span class="sxs-lookup"><span data-stu-id="8115f-149">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="8115f-150">[选择](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)**"Azure Active Directory**  =>  **企业**  =>  **应用程序许可和权限**  =>  **用户同意设置"。**</span><span class="sxs-lookup"><span data-stu-id="8115f-150">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="8115f-151">使用标记为组所有者同意的控件启用、禁用或限制用户同意访问数据 (默认值为允许组所有者同意所有组所有者) 。 </span><span class="sxs-lookup"><span data-stu-id="8115f-151">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data** (The default is **Allow group owner consent for all group owners**).</span></span> <span data-ttu-id="8115f-152">对于使用 RSC 安装应用的团队所有者，必须为该用户启用组所有者同意。</span><span class="sxs-lookup"><span data-stu-id="8115f-152">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

![azure rsc 配置](../../assets/images/azure-rsc-configuration.png)

<span data-ttu-id="8115f-154">若要使用 PowerShell 启用或禁用组所有者同意，请按照使用 PowerShell 配置组所有者 [同意中概述的步骤操作](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="8115f-154">To enable or disable group owner consent using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="8115f-155">通过 Azure AD 门户向 Microsoft 标识平台注册应用</span><span class="sxs-lookup"><span data-stu-id="8115f-155">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="8115f-156">Azure Active Directory 门户提供了一个中央平台，用于注册和配置应用。</span><span class="sxs-lookup"><span data-stu-id="8115f-156">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="8115f-157">应用必须在 Azure AD 门户中注册，才能与 Microsoft 标识平台集成并调用 Microsoft Graph API。</span><span class="sxs-lookup"><span data-stu-id="8115f-157">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="8115f-158">*请参阅*[向 Microsoft 标识平台注册应用程序](/graph/auth-register-app-v2)。</span><span class="sxs-lookup"><span data-stu-id="8115f-158">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="8115f-159">不要向同一 Azure AD 应用 ID 注册多个 Teams 应用。应用 ID 对于每个应用必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="8115f-159">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="8115f-160">尝试将多个应用安装到同一应用 ID 将失败。</span><span class="sxs-lookup"><span data-stu-id="8115f-160">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="8115f-161">在 Azure AD 门户中查看应用程序权限</span><span class="sxs-lookup"><span data-stu-id="8115f-161">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="8115f-162">导航到 **"主页**  =>  **应用注册"** 页并选择 RSC 应用。</span><span class="sxs-lookup"><span data-stu-id="8115f-162">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="8115f-163">从 **左侧导航** 栏中选择 API 权限，并检查应用的已配置权限列表。</span><span class="sxs-lookup"><span data-stu-id="8115f-163">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="8115f-164">如果你的应用将仅进行 RSC Graph API 调用，请删除该页面上的所有权限。</span><span class="sxs-lookup"><span data-stu-id="8115f-164">If your app will only make RSC Graph API calls, delete all the permission on that page.</span></span> <span data-ttu-id="8115f-165">如果你的应用还将进行非 RSC 调用，请根据需要保留这些权限。</span><span class="sxs-lookup"><span data-stu-id="8115f-165">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="8115f-166">Azure AD 门户不能用于请求 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="8115f-166">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="8115f-167">RSC 权限当前专用于 Teams 客户端中安装的 (Teams 应用程序，并且使用 JSON) 文件在应用清单中声明。</span><span class="sxs-lookup"><span data-stu-id="8115f-167">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="8115f-168">从 Microsoft 标识平台获取访问令牌</span><span class="sxs-lookup"><span data-stu-id="8115f-168">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="8115f-169">若要进行 Graph API 调用，你必须从标识平台获取应用的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="8115f-169">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="8115f-170">应用必须先在 Azure AD 门户中注册，然后才能从 Microsoft 标识平台获取令牌。</span><span class="sxs-lookup"><span data-stu-id="8115f-170">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="8115f-171">访问令牌包含你的应用的相关信息，还有它就可通过 Microsoft Graph 访问的资源和 API 所具备的权限。</span><span class="sxs-lookup"><span data-stu-id="8115f-171">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="8115f-172">你需要从 Azure AD 注册过程获取以下值，以从标识平台检索访问令牌：</span><span class="sxs-lookup"><span data-stu-id="8115f-172">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="8115f-173">应用注册门户分配的应用程序 **ID。**</span><span class="sxs-lookup"><span data-stu-id="8115f-173">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="8115f-174">如果你的应用支持单一登录 (SSO) 应用和 SSO 应使用相同的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="8115f-174">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="8115f-175">客户端 **密码/密码** 或公钥/私钥对 (**证书) 。**</span><span class="sxs-lookup"><span data-stu-id="8115f-175">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="8115f-176">这不是本机应用的必需项。</span><span class="sxs-lookup"><span data-stu-id="8115f-176">This is not required for native apps.</span></span>
- <span data-ttu-id="8115f-177">重定向 **URI** (或回复 URL) 应用接收来自 Azure AD 的响应。</span><span class="sxs-lookup"><span data-stu-id="8115f-177">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="8115f-178">*请参阅*[代表用户获取访问权限和](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true)[在没有用户的情况下获取访问权限](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="8115f-178">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="8115f-179">更新 Teams 应用清单</span><span class="sxs-lookup"><span data-stu-id="8115f-179">Update your Teams app manifest</span></span>

<span data-ttu-id="8115f-180">RSC 权限在应用清单 (JSON) 文件中声明。</span><span class="sxs-lookup"><span data-stu-id="8115f-180">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="8115f-181">将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：</span><span class="sxs-lookup"><span data-stu-id="8115f-181">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="8115f-182">**id**  — Azure AD 应用 ID。 *请参阅* 在 [Azure AD 门户中注册应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="8115f-182">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="8115f-183">**resource**  — 任何字符串。</span><span class="sxs-lookup"><span data-stu-id="8115f-183">**resource**  — any string.</span></span> <span data-ttu-id="8115f-184">此字段在 RSC 中没有任何操作，但必须添加该字段，并且必须具有值以避免错误响应;任何字符串将执行。</span><span class="sxs-lookup"><span data-stu-id="8115f-184">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="8115f-185">**应用程序权限** — 应用的 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="8115f-185">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="8115f-186">*请参阅*[特定于资源的权限](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="8115f-186">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="8115f-187">非 RSC 权限存储在 Azure 门户中。</span><span class="sxs-lookup"><span data-stu-id="8115f-187">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="8115f-188">不要将它们添加到应用清单。</span><span class="sxs-lookup"><span data-stu-id="8115f-188">Do not add them to the app manifest.</span></span>
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

## <a name="install-your-app-directly-in-teams"></a><span data-ttu-id="8115f-189">直接在 Teams 中安装应用</span><span class="sxs-lookup"><span data-stu-id="8115f-189">Install your app directly in Teams</span></span>

<span data-ttu-id="8115f-190">创建应用后，你可以 [将应用包直接](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) 上载到特定团队。</span><span class="sxs-lookup"><span data-stu-id="8115f-190">Once you've created your app you can [upload your app package](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) directly to a specific team.</span></span>  <span data-ttu-id="8115f-191">为此，必须将 **上载自定义应用** 策略设置作为自定义应用设置策略的一部分启用。</span><span class="sxs-lookup"><span data-stu-id="8115f-191">To do so, the **Upload custom apps** policy setting must be enabled as part of the custom app setup policies.</span></span> <span data-ttu-id="8115f-192">*请参阅*[自定义应用策略设置](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)。</span><span class="sxs-lookup"><span data-stu-id="8115f-192">*See* [Custom app policy settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="8115f-193">检查应用是否添加了 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="8115f-193">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="8115f-194">RSC 权限不归为用户。</span><span class="sxs-lookup"><span data-stu-id="8115f-194">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="8115f-195">调用使用应用程序权限而不是用户委派权限进行。</span><span class="sxs-lookup"><span data-stu-id="8115f-195">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="8115f-196">因此，可以允许应用执行用户无法执行的操作，例如创建频道或删除选项卡。在调用 RSC API 之前，应查看团队所有者对用例的意图。</span><span class="sxs-lookup"><span data-stu-id="8115f-196">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="8115f-197">*请参阅* [Microsoft Teams API 概述](/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="8115f-197">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="8115f-198">将应用安装到团队后，可以使用 [Graph 浏览器](https://developer.microsoft.com/graph/graph-explorer)  查看已授予团队中应用的权限：</span><span class="sxs-lookup"><span data-stu-id="8115f-198">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="8115f-199">从 Teams 客户端获取团队的 **groupId。**</span><span class="sxs-lookup"><span data-stu-id="8115f-199">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="8115f-200">在 Teams 客户端中 **，从** 最左侧导航栏中选择 Teams。</span><span class="sxs-lookup"><span data-stu-id="8115f-200">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="8115f-201">从下拉菜单中选择安装应用的团队。</span><span class="sxs-lookup"><span data-stu-id="8115f-201">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="8115f-202">选择" **更多选项"** 图标 (&#8943;) 。</span><span class="sxs-lookup"><span data-stu-id="8115f-202">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="8115f-203">选择 **获取团队链接**。</span><span class="sxs-lookup"><span data-stu-id="8115f-203">Select **Get link to team**.</span></span>
> - <span data-ttu-id="8115f-204">复制并保存字符串中的 **groupId** 值。</span><span class="sxs-lookup"><span data-stu-id="8115f-204">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="8115f-205">登录到 **Graph 浏览器**。</span><span class="sxs-lookup"><span data-stu-id="8115f-205">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="8115f-206">对以下 **终结点** 进行 GET 调用 `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` ：。</span><span class="sxs-lookup"><span data-stu-id="8115f-206">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="8115f-207">响应中的 clientAppId 字段将映射到 Teams 应用清单中指定的 appId。</span><span class="sxs-lookup"><span data-stu-id="8115f-207">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>
  <span data-ttu-id="8115f-208">![GRAPH 浏览器对 GET 调用的响应。](../../assets/images/graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="8115f-208">![Graph explorer response to GET call.](../../assets/images/graph-permissions.png)</span></span>

## <a name="code-sample"></a><span data-ttu-id="8115f-209">代码示例</span><span class="sxs-lookup"><span data-stu-id="8115f-209">Code sample</span></span>
| <span data-ttu-id="8115f-210">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="8115f-210">**Sample name**</span></span> | <span data-ttu-id="8115f-211">**Description**</span><span class="sxs-lookup"><span data-stu-id="8115f-211">**Description**</span></span> | <span data-ttu-id="8115f-212">**.NET**</span><span class="sxs-lookup"><span data-stu-id="8115f-212">**.NET**</span></span> |<span data-ttu-id="8115f-213">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="8115f-213">**Node.js**</span></span> |
|-----------------|-----------------|----------------|----------------|
| <span data-ttu-id="8115f-214">RSC (资源特定) </span><span class="sxs-lookup"><span data-stu-id="8115f-214">Resource Specific Consent (RSC)</span></span> | <span data-ttu-id="8115f-215">使用 RSC 调用 Graph API。</span><span class="sxs-lookup"><span data-stu-id="8115f-215">Use RSC to call Graph APIs.</span></span> | [<span data-ttu-id="8115f-216">View</span><span class="sxs-lookup"><span data-stu-id="8115f-216">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[<span data-ttu-id="8115f-217">View</span><span class="sxs-lookup"><span data-stu-id="8115f-217">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="test-resource-specific-consent"></a><span data-ttu-id="8115f-218">测试特定于资源的同意</span><span class="sxs-lookup"><span data-stu-id="8115f-218">Test resource-specific consent</span></span>
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="8115f-219">**在 Teams 中测试特定于资源的同意权限**</span><span class="sxs-lookup"><span data-stu-id="8115f-219">**Test resource-specific consent permissions in Teams**</span></span>](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="8115f-220">Teams 管理员相关主题</span><span class="sxs-lookup"><span data-stu-id="8115f-220">Related topic for Teams administrators</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="8115f-221">**Microsoft Teams 中针对管理员的资源特定许可**</span><span class="sxs-lookup"><span data-stu-id="8115f-221">**Resource-specific consent in Microsoft Teams for admins**</span></span>](/MicrosoftTeams/resource-specific-consent)
> 

