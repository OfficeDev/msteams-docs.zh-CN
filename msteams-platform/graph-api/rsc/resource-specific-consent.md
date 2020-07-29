---
title: 团队中的特定于资源的同意
description: 介绍了团队中特定于资源的同意以及如何利用它。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: 团队授权 OAuth SSO AAD rsc Graph
ms.openlocfilehash: bf449b338e8c0f42dfef776e533fb6b5ff591529
ms.sourcegitcommit: 1b909fb9ccf6cdd84ed0d8f9ea0463243a802a23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/28/2020
ms.locfileid: "45434501"
---
# <a name="resource-specific-consent-rsc--developer-preview"></a><span data-ttu-id="24546-104">特定于资源的同意（RSC）-开发人员预览版</span><span class="sxs-lookup"><span data-stu-id="24546-104">Resource-specific consent (RSC) — Developer Preview</span></span>

>[!NOTE]

><span data-ttu-id="24546-105">启用开发人员预览后，会在桌面和 web 客户端中提供特定于资源的同意权限。</span><span class="sxs-lookup"><span data-stu-id="24546-105">The resource-specific consent permissions are available in desktop and web clients after Developer Preview has been enabled.</span></span> <span data-ttu-id="24546-106">有关详细信息，请参阅[如何启用开发人员预览](../../resources/dev-preview/developer-preview-intro.md)。</span><span class="sxs-lookup"><span data-stu-id="24546-106">See [How do I enable Developer Preview](../../resources/dev-preview/developer-preview-intro.md) for more information.</span></span>

<span data-ttu-id="24546-107">特定于资源的同意（RSC）是 Microsoft 团队和图形 API 集成，使您的应用程序能够使用 API 终结点来管理组织中的特定团队。</span><span class="sxs-lookup"><span data-stu-id="24546-107">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="24546-108">特定于资源的同意（RSC）权限模型使*团队所有者*能够授予应用程序访问和/或修改团队数据的同意。</span><span class="sxs-lookup"><span data-stu-id="24546-108">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="24546-109">具体的团队特定的 RSC 权限定义了应用程序可在特定团队中执行的操作：</span><span class="sxs-lookup"><span data-stu-id="24546-109">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="24546-110">特定于资源的权限</span><span class="sxs-lookup"><span data-stu-id="24546-110">Resource-specific permissions</span></span>

|<span data-ttu-id="24546-111">应用权限</span><span class="sxs-lookup"><span data-stu-id="24546-111">Application permission</span></span>| <span data-ttu-id="24546-112">操作</span><span class="sxs-lookup"><span data-stu-id="24546-112">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="24546-113">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="24546-113">TeamSettings.Read.Group</span></span> | <span data-ttu-id="24546-114">获取此团队的设置。</span><span class="sxs-lookup"><span data-stu-id="24546-114">Get the settings for this team.</span></span>|
|<span data-ttu-id="24546-115">TeamSettings。组</span><span class="sxs-lookup"><span data-stu-id="24546-115">TeamSettings.Edit.Group</span></span>|<span data-ttu-id="24546-116">更新此团队的设置。</span><span class="sxs-lookup"><span data-stu-id="24546-116">Update the settings for this team.</span></span>|
|<span data-ttu-id="24546-117">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="24546-117">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="24546-118">获取此团队的频道名称、频道说明和频道设置。</span><span class="sxs-lookup"><span data-stu-id="24546-118">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="24546-119">ChannelSettings.Edit.Group</span><span class="sxs-lookup"><span data-stu-id="24546-119">ChannelSettings.Edit.Group</span></span>|<span data-ttu-id="24546-120">更新此团队的频道名称、频道说明和频道设置。</span><span class="sxs-lookup"><span data-stu-id="24546-120">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="24546-121">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="24546-121">Channel.Create.Group</span></span>|<span data-ttu-id="24546-122">在这个团队中创建频道。</span><span class="sxs-lookup"><span data-stu-id="24546-122">Create channels in this team.</span></span>|
|<span data-ttu-id="24546-123">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="24546-123">Channel.Delete.Group</span></span>|<span data-ttu-id="24546-124">删除此团队中的频道。</span><span class="sxs-lookup"><span data-stu-id="24546-124">Delete channels in this team.</span></span>|
|<span data-ttu-id="24546-125">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="24546-125">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="24546-126">获取此团队的频道消息。</span><span class="sxs-lookup"><span data-stu-id="24546-126">Get this team's channel messages.</span></span>|
|<span data-ttu-id="24546-127">TeamsApp.Read.Group</span><span class="sxs-lookup"><span data-stu-id="24546-127">TeamsApp.Read.Group</span></span>|<span data-ttu-id="24546-128">获取此团队安装的应用程序的列表。</span><span class="sxs-lookup"><span data-stu-id="24546-128">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="24546-129">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="24546-129">TeamsTab.Read.Group</span></span>|<span data-ttu-id="24546-130">获取此团队的选项卡列表。</span><span class="sxs-lookup"><span data-stu-id="24546-130">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="24546-131">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="24546-131">TeamsTab.Create.Group</span></span>|<span data-ttu-id="24546-132">在此团队中创建选项卡。</span><span class="sxs-lookup"><span data-stu-id="24546-132">Create tabs in this team.</span></span>|
|<span data-ttu-id="24546-133">TeamsTab.Edit.Group</span><span class="sxs-lookup"><span data-stu-id="24546-133">TeamsTab.Edit.Group</span></span>|<span data-ttu-id="24546-134">更新此团队的选项卡。</span><span class="sxs-lookup"><span data-stu-id="24546-134">Update this team's tabs.</span></span>|
|<span data-ttu-id="24546-135">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="24546-135">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="24546-136">删除此团队的选项卡。</span><span class="sxs-lookup"><span data-stu-id="24546-136">Delete this team's tabs.</span></span>|
|<span data-ttu-id="24546-137">Member.Read.Group</span><span class="sxs-lookup"><span data-stu-id="24546-137">Member.Read.Group</span></span>|<span data-ttu-id="24546-138">获取此团队的成员。</span><span class="sxs-lookup"><span data-stu-id="24546-138">Get this team's members.</span></span>|
|<span data-ttu-id="24546-139">Owner.Read.Group</span><span class="sxs-lookup"><span data-stu-id="24546-139">Owner.Read.Group</span></span>|<span data-ttu-id="24546-140">获取此团队的所有者。</span><span class="sxs-lookup"><span data-stu-id="24546-140">Get this team's owners.</span></span>|

>[!NOTE]
><span data-ttu-id="24546-141">特定于资源的权限仅对在团队客户端上安装的团队应用程序可用，并且当前不是 Azure Active Directory 门户的一部分。</span><span class="sxs-lookup"><span data-stu-id="24546-141">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="24546-142">在应用程序中启用特定于资源的同意</span><span class="sxs-lookup"><span data-stu-id="24546-142">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="24546-143">在应用程序中启用 RSC 的步骤如下所示：</span><span class="sxs-lookup"><span data-stu-id="24546-143">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="24546-144">[在 Azure Active Directory 门户中配置组所有者同意设置](#configure-group-owner-consent-settings-in-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="24546-144">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="24546-145">[通过 AZURE AD 门户将您的应用程序注册到 Microsoft identity platform](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="24546-145">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. [<span data-ttu-id="24546-146">在 Azure AD 门户中查看你的应用程序权限</span><span class="sxs-lookup"><span data-stu-id="24546-146">Review your application permissions in the Azure AD portal</span></span>](#review-your-application-permissions-in-the-azure-ad-portal)
1. <span data-ttu-id="24546-147">[从 Microsoft Identity Platform 获取访问令牌](#obtain-an-access-token-from-the-microsoft-identity-platform)。</span><span class="sxs-lookup"><span data-stu-id="24546-147">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="24546-148">[更新团队应用程序清单](#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="24546-148">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="24546-149">[直接在团队中安装您的应用程序](#install-your-app-directly-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="24546-149">[Install your app directly in Teams](#install-your-app-directly-in-teams).</span></span>
1. <span data-ttu-id="24546-150">[检查您的应用程序是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions)。</span><span class="sxs-lookup"><span data-stu-id="24546-150">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="24546-151">在 Azure AD 门户中配置组所有者同意设置</span><span class="sxs-lookup"><span data-stu-id="24546-151">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="24546-152">您可以在 Azure 门户中直接启用或禁用[组所有者同意](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data)：</span><span class="sxs-lookup"><span data-stu-id="24546-152">You can enable or disable  [group owner consent](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="24546-153">以[全局管理员/公司管理员身份](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)登录到[Azure 门户](https://portal.azure.com)。</span><span class="sxs-lookup"><span data-stu-id="24546-153">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="24546-154">选择 " **Azure Active Directory**  => **企业应用程序**"  => **用户设置**。</span><span class="sxs-lookup"><span data-stu-id="24546-154">Select **Azure Active Directory** =>**Enterprise applications** =>**User settings**.</span></span>
> - <span data-ttu-id="24546-155">启用、禁用或限制用户使用标记为用户的用户**可以同意访问其拥有的组的公司数据的应用程序**（默认情况下启用此功能）。</span><span class="sxs-lookup"><span data-stu-id="24546-155">Enable, disable, or limit user consent with the control labeled **Users can consent to apps accessing company data for the groups they own** (This capability is enabled by default).</span></span>

![azure rsc 配置](../../assets/images/azure-rsc-configuration.svg)

| <span data-ttu-id="24546-157">值</span><span class="sxs-lookup"><span data-stu-id="24546-157">Value</span></span> | <span data-ttu-id="24546-158">说明</span><span class="sxs-lookup"><span data-stu-id="24546-158">Description</span></span>|
|--- | --- |
|<span data-ttu-id="24546-159">是</span><span class="sxs-lookup"><span data-stu-id="24546-159">Yes</span></span> | <span data-ttu-id="24546-160">对所有组所有者启用组特定的同意。</span><span class="sxs-lookup"><span data-stu-id="24546-160">Enable group-specific consent for all group owners.</span></span>|
|<span data-ttu-id="24546-161">否</span><span class="sxs-lookup"><span data-stu-id="24546-161">No</span></span> |<span data-ttu-id="24546-162">对所有用户禁用组特定的同意。</span><span class="sxs-lookup"><span data-stu-id="24546-162">Disable group-specific consent for all users.</span></span>| 
|<span data-ttu-id="24546-163">范围</span><span class="sxs-lookup"><span data-stu-id="24546-163">Limited</span></span> | <span data-ttu-id="24546-164">对所选组的成员启用组特定的同意。</span><span class="sxs-lookup"><span data-stu-id="24546-164">Enable group-specific consent for members of a selected group.</span></span>|

<span data-ttu-id="24546-165">若要在 Azure 门户中使用 PowerShell 启用或禁用组所有者同意，请按照[使用 Powershell 配置组所有者许可](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell)中所述的步骤操作。</span><span class="sxs-lookup"><span data-stu-id="24546-165">To enable or disable group owner consent within the Azure portal using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="24546-166">通过 Azure AD 门户将您的应用程序注册到 Microsoft identity platform</span><span class="sxs-lookup"><span data-stu-id="24546-166">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="24546-167">Azure Active Directory 门户为您提供了一个用于注册和配置应用程序的中央平台。</span><span class="sxs-lookup"><span data-stu-id="24546-167">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="24546-168">您的应用程序必须在 Azure AD 门户中注册，才能与 Microsoft identity platform 和调用 Graph Api 集成。</span><span class="sxs-lookup"><span data-stu-id="24546-168">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Graph APIs.</span></span> <span data-ttu-id="24546-169">*请参阅*[在 Microsoft identity platform 中注册应用程序](/graph/auth-register-app-v2)。</span><span class="sxs-lookup"><span data-stu-id="24546-169">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="24546-170">不要将多个团队应用注册到同一个 Azure AD 应用 id。应用程序 id 对于每个应用程序必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="24546-170">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="24546-171">尝试将多个应用程序安装到相同的应用 id 将会失败。</span><span class="sxs-lookup"><span data-stu-id="24546-171">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="24546-172">在 Azure AD 门户中查看你的应用程序权限</span><span class="sxs-lookup"><span data-stu-id="24546-172">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="24546-173">导航到 "**家庭**  =>  **应用注册**" 页，并选择您的 RSC 应用程序。</span><span class="sxs-lookup"><span data-stu-id="24546-173">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="24546-174">从左侧导航栏中选择 " **API 权限**"，然后检查您的应用程序的已配置权限列表。</span><span class="sxs-lookup"><span data-stu-id="24546-174">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="24546-175">如果您的应用程序将仅进行 RSC Graph 呼叫，则删除该页面上的所有权限。</span><span class="sxs-lookup"><span data-stu-id="24546-175">If your app will only make RSC Graph calls, delete all the permission on that page.</span></span> <span data-ttu-id="24546-176">如果你的应用程序还将进行非 RSC 呼叫，请根据需要保留这些权限。</span><span class="sxs-lookup"><span data-stu-id="24546-176">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="24546-177">Azure AD 门户不能用于请求 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="24546-177">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="24546-178">RSC 权限当前对于安装在团队客户端中并在应用程序清单（JSON）文件中声明的团队应用程序是独占的。</span><span class="sxs-lookup"><span data-stu-id="24546-178">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="24546-179">从 Microsoft identity platform 获取访问令牌</span><span class="sxs-lookup"><span data-stu-id="24546-179">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="24546-180">若要进行 Graph API 调用，必须从标识平台获取应用程序的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="24546-180">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="24546-181">在您的应用程序可以从 Microsoft identity platform 获取令牌之前，它必须在 Azure AD 门户中进行注册。</span><span class="sxs-lookup"><span data-stu-id="24546-181">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="24546-182">访问令牌包含你的应用的相关信息，还有它就可通过 Microsoft Graph 访问的资源和 API 所具备的权限。</span><span class="sxs-lookup"><span data-stu-id="24546-182">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="24546-183">您需要使用 Azure AD 注册过程中的以下值从标识平台检索访问令牌：</span><span class="sxs-lookup"><span data-stu-id="24546-183">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="24546-184">应用注册门户分配的**应用程序 ID** 。</span><span class="sxs-lookup"><span data-stu-id="24546-184">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="24546-185">如果您的应用程序支持单一登录（SSO），则您的应用程序和 SSO 应使用相同的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="24546-185">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="24546-186">**客户端密码/密码**或公钥/私钥对（**证书**）。</span><span class="sxs-lookup"><span data-stu-id="24546-186">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="24546-187">这不是本机应用的必需项。</span><span class="sxs-lookup"><span data-stu-id="24546-187">This is not required for native apps.</span></span>
- <span data-ttu-id="24546-188">您的应用程序从 Azure AD 接收响应的**重定向 URI** （或回复 URL）。</span><span class="sxs-lookup"><span data-stu-id="24546-188">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="24546-189">*请参阅*[代表用户获取访问权限](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token)并在[没有用户的情况下获取访问权限](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="24546-189">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="24546-190">更新团队应用程序清单</span><span class="sxs-lookup"><span data-stu-id="24546-190">Update your Teams app manifest</span></span>

<span data-ttu-id="24546-191">RSC 权限是在您的应用程序清单（JSON）文件中声明的。</span><span class="sxs-lookup"><span data-stu-id="24546-191">The RSC permissions are declared in you app manifest (JSON) file.</span></span>  <span data-ttu-id="24546-192">使用以下值将[webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo)项添加到应用程序清单中：</span><span class="sxs-lookup"><span data-stu-id="24546-192">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="24546-193">**id** —您的 Azure AD 应用程序 id。*请参阅*[在 Azure AD 门户中注册你的应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="24546-193">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="24546-194">**resource** —任何字符串。</span><span class="sxs-lookup"><span data-stu-id="24546-194">**resource**  — any string.</span></span> <span data-ttu-id="24546-195">此字段在 RSC 中没有任何操作，但必须添加它并具有值以避免错误响应;任何字符串都将执行。</span><span class="sxs-lookup"><span data-stu-id="24546-195">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="24546-196">**应用程序权限**-您的应用程序的 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="24546-196">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="24546-197">*请参阅*[特定于资源的权限](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="24546-197">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="24546-198">非 RSC 权限存储在 Azure 门户中。</span><span class="sxs-lookup"><span data-stu-id="24546-198">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="24546-199">请勿将其添加到应用程序清单。</span><span class="sxs-lookup"><span data-stu-id="24546-199">Do not add them to the app manifest.</span></span>
>

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "TeamSettings.Read.Group",
      "ChannelMessage.Read.Group",
      "TeamSettings.Edit.Group",
      "ChannelSettings.Edit.Group",
      "Channel.Create.Group",
      "Channel.Delete.Group",
      "TeamsApp.Read.Group",
      "TeamsTab.Read.Group",
      "TeamsTab.Create.Group",
      "TeamsTab.Edit.Group",
      "TeamsTab.Delete.Group",
      "Member.Read.Group",
      "Owner.Read.Group"
    ]
  }
```

## <a name="install-your-app-directly-in-teams"></a><span data-ttu-id="24546-200">直接在团队中安装您的应用程序</span><span class="sxs-lookup"><span data-stu-id="24546-200">Install your app directly in Teams</span></span>

<span data-ttu-id="24546-201">创建您的应用程序后，您可以将[应用程序包直接上载](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab)到特定团队。</span><span class="sxs-lookup"><span data-stu-id="24546-201">Once you've created your app you can [upload your app package](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) directly to a specific team.</span></span>  <span data-ttu-id="24546-202">若要执行此操作，必须将 "**上载自定义应用**" 策略设置作为自定义应用程序安装策略的一部分启用。</span><span class="sxs-lookup"><span data-stu-id="24546-202">To do so, the **Upload custom apps** policy setting must be enabled as part of the custom app setup policies.</span></span> <span data-ttu-id="24546-203">*请参阅*[自定义应用策略设置](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)。</span><span class="sxs-lookup"><span data-stu-id="24546-203">*See* [Custom app policy settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="24546-204">检查您的应用程序是否添加了 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="24546-204">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="24546-205">RSC 权限不是用户的属性。</span><span class="sxs-lookup"><span data-stu-id="24546-205">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="24546-206">调用通过应用权限而不是用户委派权限进行。</span><span class="sxs-lookup"><span data-stu-id="24546-206">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="24546-207">因此，可能允许应用程序执行用户无法执行的操作，例如创建频道或删除选项卡。在进行 RSC API 调用之前，应查看团队所有者对用例的意图。</span><span class="sxs-lookup"><span data-stu-id="24546-207">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="24546-208">*请参阅* [Microsoft 团队 API 概述](/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="24546-208">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="24546-209">将应用程序安装到团队后，可以使用[Graph 浏览器](https://developer.microsoft.com/graph/graph-explorer)查看已授予给团队中的应用程序的权限：</span><span class="sxs-lookup"><span data-stu-id="24546-209">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="24546-210">从团队客户端获取团队的**groupId** 。</span><span class="sxs-lookup"><span data-stu-id="24546-210">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="24546-211">在团队客户端中，从最左侧的导航栏中选择 "**团队**"。</span><span class="sxs-lookup"><span data-stu-id="24546-211">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="24546-212">从下拉菜单中选择应用程序安装到的团队。</span><span class="sxs-lookup"><span data-stu-id="24546-212">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="24546-213">选择 "**更多选项**" 图标（&#8943;）。</span><span class="sxs-lookup"><span data-stu-id="24546-213">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="24546-214">选择 "**获取到团队的链接**"。</span><span class="sxs-lookup"><span data-stu-id="24546-214">Select **Get link to team**.</span></span>
> - <span data-ttu-id="24546-215">复制并保存字符串中的**groupId**值。</span><span class="sxs-lookup"><span data-stu-id="24546-215">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="24546-216">登录到**Graph 浏览器**。</span><span class="sxs-lookup"><span data-stu-id="24546-216">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="24546-217">对以下终结点进行**GET**调用： `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` 。</span><span class="sxs-lookup"><span data-stu-id="24546-217">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="24546-218">响应中的 clientAppId 字段将映射到在团队应用程序清单中指定的 appId。</span><span class="sxs-lookup"><span data-stu-id="24546-218">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>

 ![Graph 资源管理器响应 GET call。](../../assets/images/graph-permissions.png)
 
## <a name="test-resource-specific-consent"></a><span data-ttu-id="24546-220">测试特定于资源的同意</span><span class="sxs-lookup"><span data-stu-id="24546-220">Test resource-specific consent</span></span>
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="24546-221">**在团队中测试特定于资源的同意权限**</span><span class="sxs-lookup"><span data-stu-id="24546-221">**Test resource-specific consent permissions in Teams**</span></span>](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="24546-222">团队管理员的相关主题</span><span class="sxs-lookup"><span data-stu-id="24546-222">Related topic for Teams administrators</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="24546-223">**Microsoft 团队中针对管理员的特定于资源的同意**</span><span class="sxs-lookup"><span data-stu-id="24546-223">**Resource-specific consent in Microsoft Teams for admins**</span></span>](/MicrosoftTeams/resource-specific-consent)
> 
