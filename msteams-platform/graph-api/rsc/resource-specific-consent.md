---
title: Teams 中特定于资源的许可
description: 介绍 Teams 中特定于资源的许可以及如何利用它。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: Teams 授权 OAuth SSO AAD rsc Graph
ms.openlocfilehash: 7e3fc3faa111f4ba982c1c79e6b5b873b8773aef
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819180"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="633ee-104">特定于资源的 RSC (同) </span><span class="sxs-lookup"><span data-stu-id="633ee-104">Resource-specific consent (RSC)</span></span>

>[!IMPORTANT]
> <span data-ttu-id="633ee-105">这些 API 在终结点中 https://graph.microsoft.com/beta 可访问。</span><span class="sxs-lookup"><span data-stu-id="633ee-105">These APIs are accessible in the https://graph.microsoft.com/beta endpoint.</span></span>  <span data-ttu-id="633ee-106">[beta 版本](/graph/versioning-and-support#beta-version)终结点包括当前处于预览版且未正式发布的 API。</span><span class="sxs-lookup"><span data-stu-id="633ee-106">The [beta version](/graph/versioning-and-support#beta-version) endpoint includes APIs that are currently in preview and are not yet generally available.</span></span> <span data-ttu-id="633ee-107">beta 终结点中的 API 可能会发生更改，建议不要在生产应用中使用它们。</span><span class="sxs-lookup"><span data-stu-id="633ee-107">The APIs in the beta endpoint are subject to change and we don't recommend that you use them in your production apps.</span></span> 

<span data-ttu-id="633ee-108">特定于资源的 (RSC) Microsoft Teams 和 Graph API 集成，它使你的应用能够使用 API 终结点来管理组织内的特定团队。</span><span class="sxs-lookup"><span data-stu-id="633ee-108">Resource-specific consent (RSC) is a Microsoft Teams and Graph API integration that enables your app to use API endpoints to manage specific teams within an organization.</span></span> <span data-ttu-id="633ee-109">根据资源的 (同意) 模型， *工作组所有者* 可同意应用程序访问和/或修改团队的数据。</span><span class="sxs-lookup"><span data-stu-id="633ee-109">The resource-specific consent (RSC) permissions model enables *team owners* to grant consent for an application to access and/or modify a team's data.</span></span> <span data-ttu-id="633ee-110">精细的特定于 Teams 的 RSC 权限定义应用程序可在特定团队内执行的操作：</span><span class="sxs-lookup"><span data-stu-id="633ee-110">The granular, Teams-specific, RSC permissions define what an application can do within a specific team:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="633ee-111">特定于资源的权限</span><span class="sxs-lookup"><span data-stu-id="633ee-111">Resource-specific permissions</span></span>

|<span data-ttu-id="633ee-112">应用权限</span><span class="sxs-lookup"><span data-stu-id="633ee-112">Application permission</span></span>| <span data-ttu-id="633ee-113">操作</span><span class="sxs-lookup"><span data-stu-id="633ee-113">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="633ee-114">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="633ee-114">TeamSettings.Read.Group</span></span> | <span data-ttu-id="633ee-115">获取此团队的设置。</span><span class="sxs-lookup"><span data-stu-id="633ee-115">Get the settings for this team.</span></span>|
|<span data-ttu-id="633ee-116">TeamSettings.Edit.Group</span><span class="sxs-lookup"><span data-stu-id="633ee-116">TeamSettings.Edit.Group</span></span>|<span data-ttu-id="633ee-117">更新此团队的设置。</span><span class="sxs-lookup"><span data-stu-id="633ee-117">Update the settings for this team.</span></span>|
|<span data-ttu-id="633ee-118">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="633ee-118">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="633ee-119">获取此团队的频道名称、渠道描述和频道设置。</span><span class="sxs-lookup"><span data-stu-id="633ee-119">Get the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="633ee-120">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="633ee-120">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="633ee-121">更新此团队的频道名称、频道描述和频道设置。</span><span class="sxs-lookup"><span data-stu-id="633ee-121">Update the channel names, channel descriptions, and channel settings for this team.</span></span>|
|<span data-ttu-id="633ee-122">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="633ee-122">Channel.Create.Group</span></span>|<span data-ttu-id="633ee-123">在这个团队中创建频道。</span><span class="sxs-lookup"><span data-stu-id="633ee-123">Create channels in this team.</span></span>|
|<span data-ttu-id="633ee-124">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="633ee-124">Channel.Delete.Group</span></span>|<span data-ttu-id="633ee-125">删除此团队中的频道。</span><span class="sxs-lookup"><span data-stu-id="633ee-125">Delete channels in this team.</span></span>|
|<span data-ttu-id="633ee-126">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="633ee-126">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="633ee-127">获取此团队的频道消息。</span><span class="sxs-lookup"><span data-stu-id="633ee-127">Get this team's channel messages.</span></span>|
|<span data-ttu-id="633ee-128">TeamsApp.Read.Group</span><span class="sxs-lookup"><span data-stu-id="633ee-128">TeamsApp.Read.Group</span></span>|<span data-ttu-id="633ee-129">获取此团队已安装应用的列表。</span><span class="sxs-lookup"><span data-stu-id="633ee-129">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="633ee-130">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="633ee-130">TeamsTab.Read.Group</span></span>|<span data-ttu-id="633ee-131">获取此团队的选项卡列表。</span><span class="sxs-lookup"><span data-stu-id="633ee-131">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="633ee-132">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="633ee-132">TeamsTab.Create.Group</span></span>|<span data-ttu-id="633ee-133">在此团队中创建选项卡。</span><span class="sxs-lookup"><span data-stu-id="633ee-133">Create tabs in this team.</span></span>|
|<span data-ttu-id="633ee-134">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="633ee-134">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="633ee-135">更新此团队的选项卡。</span><span class="sxs-lookup"><span data-stu-id="633ee-135">Update this team's tabs.</span></span>|
|<span data-ttu-id="633ee-136">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="633ee-136">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="633ee-137">删除此团队的选项卡。</span><span class="sxs-lookup"><span data-stu-id="633ee-137">Delete this team's tabs.</span></span>|
|<span data-ttu-id="633ee-138">Member.Read.Group</span><span class="sxs-lookup"><span data-stu-id="633ee-138">Member.Read.Group</span></span>|<span data-ttu-id="633ee-139">获取此团队的成员。</span><span class="sxs-lookup"><span data-stu-id="633ee-139">Get this team's members.</span></span>|
|<span data-ttu-id="633ee-140">Owner.Read.Group</span><span class="sxs-lookup"><span data-stu-id="633ee-140">Owner.Read.Group</span></span>|<span data-ttu-id="633ee-141">获取此团队的所有者。</span><span class="sxs-lookup"><span data-stu-id="633ee-141">Get this team's owners.</span></span>|

>[!NOTE]
><span data-ttu-id="633ee-142">特定于资源的权限仅适用于安装在 Teams 客户端上的 Teams 应用，目前不属于 Azure Active Directory 门户。</span><span class="sxs-lookup"><span data-stu-id="633ee-142">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="633ee-143">在应用程序中启用特定于资源的许可</span><span class="sxs-lookup"><span data-stu-id="633ee-143">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="633ee-144">在应用程序中启用 RSC 的步骤如下：</span><span class="sxs-lookup"><span data-stu-id="633ee-144">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="633ee-145">[在 Azure Active Directory 门户中配置组所有者同意设置](#configure-group-owner-consent-settings-in-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="633ee-145">[Configure group owner consent settings in the Azure Active Directory portal](#configure-group-owner-consent-settings-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="633ee-146">[通过 Azure AD 门户将应用注册到 Microsoft 标识平台](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="633ee-146">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. [<span data-ttu-id="633ee-147">在 Azure AD 门户中查看应用程序权限</span><span class="sxs-lookup"><span data-stu-id="633ee-147">Review your application permissions in the Azure AD portal</span></span>](#review-your-application-permissions-in-the-azure-ad-portal)
1. <span data-ttu-id="633ee-148">[从 Microsoft 标识平台获取访问令牌](#obtain-an-access-token-from-the-microsoft-identity-platform)。</span><span class="sxs-lookup"><span data-stu-id="633ee-148">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="633ee-149">[更新 Teams 应用清单](#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="633ee-149">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="633ee-150">[直接在 Teams 中安装你的应用](#install-your-app-directly-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="633ee-150">[Install your app directly in Teams](#install-your-app-directly-in-teams).</span></span>
1. <span data-ttu-id="633ee-151">[检查应用，查看添加的 RSC 权限](#check-your-app-for-added-rsc-permissions)。</span><span class="sxs-lookup"><span data-stu-id="633ee-151">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="633ee-152">在 Azure AD 门户中配置组所有者同意设置</span><span class="sxs-lookup"><span data-stu-id="633ee-152">Configure group owner consent settings in the Azure AD portal</span></span>

<span data-ttu-id="633ee-153">你可以直接在  [Azure 门户中启用或禁用](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) 组所有者许可：</span><span class="sxs-lookup"><span data-stu-id="633ee-153">You can enable or disable  [group owner consent](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="633ee-154">以全局管理员 [/](https://portal.azure.com) 公司管理员 [身份登录到 Azure 门户](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)。</span><span class="sxs-lookup"><span data-stu-id="633ee-154">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator).</span></span>  
 > - <span data-ttu-id="633ee-155">选择 **"Azure Active Directory**  => **企业应用程序**  => **用户设置"。**</span><span class="sxs-lookup"><span data-stu-id="633ee-155">Select **Azure Active Directory** =>**Enterprise applications** =>**User settings**.</span></span>
> - <span data-ttu-id="633ee-156">启用、禁用或限制用户同意，并允许用户同意访问标签用户的 **控制者 (** 默认情况下启用此功能) 。</span><span class="sxs-lookup"><span data-stu-id="633ee-156">Enable, disable, or limit user consent with the control labeled **Users can consent to apps accessing company data for the groups they own** (This capability is enabled by default).</span></span>

![azure rsc 配置](../../assets/images/azure-rsc-configuration.svg)

| <span data-ttu-id="633ee-158">值</span><span class="sxs-lookup"><span data-stu-id="633ee-158">Value</span></span> | <span data-ttu-id="633ee-159">说明</span><span class="sxs-lookup"><span data-stu-id="633ee-159">Description</span></span>|
|--- | --- |
|<span data-ttu-id="633ee-160">是</span><span class="sxs-lookup"><span data-stu-id="633ee-160">Yes</span></span> | <span data-ttu-id="633ee-161">为所有组所有者启用特定于组的许可。</span><span class="sxs-lookup"><span data-stu-id="633ee-161">Enable group-specific consent for all group owners.</span></span>|
|<span data-ttu-id="633ee-162">否</span><span class="sxs-lookup"><span data-stu-id="633ee-162">No</span></span> |<span data-ttu-id="633ee-163">对所有用户禁用特定于组的许可。</span><span class="sxs-lookup"><span data-stu-id="633ee-163">Disable group-specific consent for all users.</span></span>| 
|<span data-ttu-id="633ee-164">Limited</span><span class="sxs-lookup"><span data-stu-id="633ee-164">Limited</span></span> | <span data-ttu-id="633ee-165">为所选组的成员启用特定于组的许可。</span><span class="sxs-lookup"><span data-stu-id="633ee-165">Enable group-specific consent for members of a selected group.</span></span>|

<span data-ttu-id="633ee-166">若要使用 PowerShell 在 Azure 门户内启用或禁用组所有者同意，请按照使用 [PowerShell 配置组所有者同意中概述的步骤操作](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell)。</span><span class="sxs-lookup"><span data-stu-id="633ee-166">To enable or disable group owner consent within the Azure portal using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="633ee-167">通过 Azure AD 门户向 Microsoft 标识平台注册应用</span><span class="sxs-lookup"><span data-stu-id="633ee-167">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="633ee-168">Azure Active Directory 门户提供了一个中心平台，可注册和配置应用。</span><span class="sxs-lookup"><span data-stu-id="633ee-168">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="633ee-169">必须在 Azure AD 门户中注册应用，才能与 Microsoft 标识平台集成并调用 Graph API。</span><span class="sxs-lookup"><span data-stu-id="633ee-169">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Graph APIs.</span></span> <span data-ttu-id="633ee-170">*请参阅*[向 Microsoft 标识平台注册应用程序](/graph/auth-register-app-v2)。</span><span class="sxs-lookup"><span data-stu-id="633ee-170">*See* [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="633ee-171">请勿将多个 Teams 应用注册到同一个 Azure AD 应用 ID。应用 ID 对于每个应用都必须是唯一的。</span><span class="sxs-lookup"><span data-stu-id="633ee-171">Do not register multiple Teams apps to the same Azure AD app id. The app id must be unique for each app.</span></span> <span data-ttu-id="633ee-172">尝试将多个应用安装到同一应用 ID 时失败。</span><span class="sxs-lookup"><span data-stu-id="633ee-172">Attempts to install multiple apps to the same app id will fail.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="633ee-173">在 Azure AD 门户中查看应用程序权限</span><span class="sxs-lookup"><span data-stu-id="633ee-173">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="633ee-174">导航到"**家庭**  =>  **应用注册"** 页面并选择 RSC 应用。</span><span class="sxs-lookup"><span data-stu-id="633ee-174">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="633ee-175">从 **左侧** 导航栏中选择 API 权限，并检查应用已配置权限的列表。</span><span class="sxs-lookup"><span data-stu-id="633ee-175">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="633ee-176">如果你的应用仅调用 RSC Graph，请删除该页面上的所有权限。</span><span class="sxs-lookup"><span data-stu-id="633ee-176">If your app will only make RSC Graph calls, delete all the permission on that page.</span></span> <span data-ttu-id="633ee-177">如果你的应用还将发出非 RSC 调用，请根据需要保留这些权限。</span><span class="sxs-lookup"><span data-stu-id="633ee-177">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="633ee-178">Azure AD 门户无法用于请求 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="633ee-178">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="633ee-179">RSC 权限目前仅为安装在 Teams 客户端中的 Teams 应用程序) ，并在 JSON 格式文件的应用清单 (中声明。</span><span class="sxs-lookup"><span data-stu-id="633ee-179">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="633ee-180">从 Microsoft 标识平台获取访问令牌</span><span class="sxs-lookup"><span data-stu-id="633ee-180">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="633ee-181">若要进行 Graph API 调用，必须从标识平台为应用获取访问令牌。</span><span class="sxs-lookup"><span data-stu-id="633ee-181">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="633ee-182">必须在 Azure AD 门户中注册你的应用，然后它才能从 Microsoft 标识平台获取令牌。</span><span class="sxs-lookup"><span data-stu-id="633ee-182">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="633ee-183">访问令牌包含你的应用的相关信息，还有它就可通过 Microsoft Graph 访问的资源和 API 所具备的权限。</span><span class="sxs-lookup"><span data-stu-id="633ee-183">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="633ee-184">将需要从 Azure AD 注册进程中拥有以下值，从标识平台检索访问令牌：</span><span class="sxs-lookup"><span data-stu-id="633ee-184">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="633ee-185">应用注册门户分配的应用程序**ID。**</span><span class="sxs-lookup"><span data-stu-id="633ee-185">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="633ee-186">如果应用在 SSO 身份验证选项 (单) 则应该为应用和 SSO 使用相同的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="633ee-186">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="633ee-187">客户端**密码/密码或公钥**/私钥对 (钥对 (**) 。**</span><span class="sxs-lookup"><span data-stu-id="633ee-187">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="633ee-188">这不是本机应用的必需项。</span><span class="sxs-lookup"><span data-stu-id="633ee-188">This is not required for native apps.</span></span>
- <span data-ttu-id="633ee-189">可以 **让 (** AZURE AD) 或回复 URL 链接或回复 URL 文件。</span><span class="sxs-lookup"><span data-stu-id="633ee-189">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="633ee-190">*在*[没有用户的情况下代表用户查看](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token)[访问权限并获取访问权限](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="633ee-190">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="633ee-191">更新 Teams 应用部件清单 （manifest）</span><span class="sxs-lookup"><span data-stu-id="633ee-191">Update your Teams app manifest</span></span>

<span data-ttu-id="633ee-192">RSC 权限在 JSON 设备的应用程序清单或 (应用程序) 中。</span><span class="sxs-lookup"><span data-stu-id="633ee-192">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="633ee-193">使用以下 [值将 webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到应用部件清单：</span><span class="sxs-lookup"><span data-stu-id="633ee-193">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="633ee-194">**id** — 你的 Azure AD 应用 ID。*请参阅*["在 Azure AD 门户注册你的应用"。](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)</span><span class="sxs-lookup"><span data-stu-id="633ee-194">**id**  — your Azure AD app id. *See* [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="633ee-195">**资源**  — 任何字符串。</span><span class="sxs-lookup"><span data-stu-id="633ee-195">**resource**  — any string.</span></span> <span data-ttu-id="633ee-196">此字段在 RSC 中没有操作，但必须添加并具有值以避免响应;可对任何字符串执行操作。</span><span class="sxs-lookup"><span data-stu-id="633ee-196">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="633ee-197">**应用程序权限** — 您的应用程序的 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="633ee-197">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="633ee-198">*参*[见特定于资源的权限](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="633ee-198">*See* [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="633ee-199">非 RSC 权限存储在 Azure 门户中。</span><span class="sxs-lookup"><span data-stu-id="633ee-199">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="633ee-200">不要将其添加到应用部件清单 （manifest）。</span><span class="sxs-lookup"><span data-stu-id="633ee-200">Do not add them to the app manifest.</span></span>
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

## <a name="install-your-app-directly-in-teams"></a><span data-ttu-id="633ee-201">直接在 Teams 中安装应用</span><span class="sxs-lookup"><span data-stu-id="633ee-201">Install your app directly in Teams</span></span>

<span data-ttu-id="633ee-202">创建应用后，你可以将 [应用包直接](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) 上传到特定团队。</span><span class="sxs-lookup"><span data-stu-id="633ee-202">Once you've created your app you can [upload your app package](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) directly to a specific team.</span></span>  <span data-ttu-id="633ee-203">为此，必须在 **自定义应用程序设置策略** 中启用"上载自定义应用程序"策略设置。</span><span class="sxs-lookup"><span data-stu-id="633ee-203">To do so, the **Upload custom apps** policy setting must be enabled as part of the custom app setup policies.</span></span> <span data-ttu-id="633ee-204">*请参阅*[自定义应用策略设置](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)。</span><span class="sxs-lookup"><span data-stu-id="633ee-204">*See* [Custom app policy settings](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings).</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="633ee-205">检查你的应用的添加 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="633ee-205">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="633ee-206">RSC 权限不会分配给用户。</span><span class="sxs-lookup"><span data-stu-id="633ee-206">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="633ee-207">调用使用应用权限，而非用户委派的权限。</span><span class="sxs-lookup"><span data-stu-id="633ee-207">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="633ee-208">因此，应用可能可以执行用户无法执行的操作，例如创建通道或删除选项卡。应在调用 RSC API 之前审查团队所有者有关用例的意图。</span><span class="sxs-lookup"><span data-stu-id="633ee-208">Thus, the app may be allowed to perform actions that the user cannot, such as creating a channel or deleting a tab. You should review the team owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="633ee-209">*请参阅* [Microsoft Teams API 概述](/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="633ee-209">*See* [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="633ee-210">将应用安装到团队后，可以使用 [Graph 浏览器](https://developer.microsoft.com/graph/graph-explorer)  查看该团队中已授予应用的权限：</span><span class="sxs-lookup"><span data-stu-id="633ee-210">Once the app has been installed to a team, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in a team:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="633ee-211">从 Teams 客户端**获取团队的 groupId。**</span><span class="sxs-lookup"><span data-stu-id="633ee-211">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="633ee-212">在 Teams 客户端中，从最左侧导航栏选择**Teams。**</span><span class="sxs-lookup"><span data-stu-id="633ee-212">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="633ee-213">从下拉菜单中选择安装应用的团队。</span><span class="sxs-lookup"><span data-stu-id="633ee-213">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="633ee-214">选择" **更多"选项** (&#8943;) 。</span><span class="sxs-lookup"><span data-stu-id="633ee-214">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="633ee-215">选择 **"获取团队链接"。**</span><span class="sxs-lookup"><span data-stu-id="633ee-215">Select **Get link to team**.</span></span>
> - <span data-ttu-id="633ee-216">复制并保存字符串 **中的 groupId** 值。</span><span class="sxs-lookup"><span data-stu-id="633ee-216">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="633ee-217">登录到 **Graph 浏览器**。</span><span class="sxs-lookup"><span data-stu-id="633ee-217">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="633ee-218">对以下 **端** 点执行 GET 调用 `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` ：</span><span class="sxs-lookup"><span data-stu-id="633ee-218">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="633ee-219">响应中的 clientAppId 字段将映射到 Teams 应用部件清单 （manifest） 中指定的 appId。</span><span class="sxs-lookup"><span data-stu-id="633ee-219">The clientAppId field in the response will map to the appId specified in the Teams app manifest.</span></span>
  <span data-ttu-id="633ee-220">![GET 调用的图形浏览器响应。](../../assets/images/graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="633ee-220">![Graph explorer response to GET call.](../../assets/images/graph-permissions.png)</span></span>
 
## <a name="test-resource-specific-consent"></a><span data-ttu-id="633ee-221">测试特定于资源的许可</span><span class="sxs-lookup"><span data-stu-id="633ee-221">Test resource-specific consent</span></span>
 
> [!div class="nextstepaction"]
> [<span data-ttu-id="633ee-222">**测试 Teams 中特定于资源的许可权限**</span><span class="sxs-lookup"><span data-stu-id="633ee-222">**Test resource-specific consent permissions in Teams**</span></span>](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a><span data-ttu-id="633ee-223">Teams 管理员相关主题</span><span class="sxs-lookup"><span data-stu-id="633ee-223">Related topic for Teams administrators</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="633ee-224">**Microsoft Teams 中面向管理员的特定于资源的同意**</span><span class="sxs-lookup"><span data-stu-id="633ee-224">**Resource-specific consent in Microsoft Teams for admins**</span></span>](/MicrosoftTeams/resource-specific-consent)
> 
