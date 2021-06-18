---
title: 资源特定许可Teams
description: 介绍资源特定的Teams以及如何利用它。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: reference
keywords: teams 授权 OAuth SSO AAD rsc Graph
ms.openlocfilehash: 215b528310137da331b0aef6ab004e0448dbfadf
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994312"
---
# <a name="resource-specific-consent-rsc"></a><span data-ttu-id="dcc4a-104">RSC (资源特定的) </span><span class="sxs-lookup"><span data-stu-id="dcc4a-104">Resource-specific consent (RSC)</span></span>

> [!NOTE]
> <span data-ttu-id="dcc4a-105">聊天范围的特定于资源的同意仅适用于 [公共开发人员预览](../../resources/dev-preview/developer-preview-intro.md) 版。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-105">Resource-specific consent for chat scope is available in [public developer preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="dcc4a-106">特定于资源的同意 (RSC) 是一种 Microsoft Teams 和 Microsoft Graph API 集成，使你的应用可以使用 API 终结点来管理组织内的特定资源（团队或聊天）。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-106">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific resources—either teams or chats—within an organization.</span></span> <span data-ttu-id="dcc4a-107">RSC) 权限模型的特定于资源的许可 (允许团队所有者和聊天所有者分别授予应用程序访问和/或修改团队数据和聊天数据的许可。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-107">The resource-specific consent (RSC) permissions model enables *team owners* and *chat owners* to grant consent for an application to access and/or modify a team's data and a chat's data, respectively.</span></span> <span data-ttu-id="dcc4a-108">具体、Teams特定的 RSC 权限定义应用程序可以在特定资源中执行哪些操作：</span><span class="sxs-lookup"><span data-stu-id="dcc4a-108">The granular, Teams-specific, RSC permissions define what an application can do within a specific resource:</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="dcc4a-109">特定于资源的权限</span><span class="sxs-lookup"><span data-stu-id="dcc4a-109">Resource-specific permissions</span></span>

### <a name="resource-specific-permissions-for-a-team"></a><span data-ttu-id="dcc4a-110">团队的特定于资源的权限</span><span class="sxs-lookup"><span data-stu-id="dcc4a-110">Resource-specific permissions for a team</span></span>
|<span data-ttu-id="dcc4a-111">应用权限</span><span class="sxs-lookup"><span data-stu-id="dcc4a-111">Application permission</span></span>| <span data-ttu-id="dcc4a-112">操作</span><span class="sxs-lookup"><span data-stu-id="dcc4a-112">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="dcc4a-113">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="dcc4a-113">TeamSettings.Read.Group</span></span> | <span data-ttu-id="dcc4a-114">获取此团队的设置。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-114">Get this team's settings.</span></span>|
|<span data-ttu-id="dcc4a-115">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="dcc4a-115">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="dcc4a-116">更新此团队的设置。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-116">Update this team's settings.</span></span>|
|<span data-ttu-id="dcc4a-117">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="dcc4a-117">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="dcc4a-118">获取此团队的频道名称、频道说明和频道设置。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-118">Get this team's channel names, channel descriptions, and channel settings.</span></span>|
|<span data-ttu-id="dcc4a-119">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="dcc4a-119">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="dcc4a-120">更新此团队的频道名称、频道说明和频道设置。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-120">Update this team's channel names, channel descriptions, and channel settings.</span></span>|
|<span data-ttu-id="dcc4a-121">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="dcc4a-121">Channel.Create.Group</span></span>|<span data-ttu-id="dcc4a-122">在这个团队中创建频道。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-122">Create channels in this team.</span></span>|
|<span data-ttu-id="dcc4a-123">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="dcc4a-123">Channel.Delete.Group</span></span>|<span data-ttu-id="dcc4a-124">删除此团队中的频道。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-124">Delete channels in this team.</span></span>|
|<span data-ttu-id="dcc4a-125">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="dcc4a-125">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="dcc4a-126">获取此团队的频道消息。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-126">Get this team's channel messages.</span></span>|
|<span data-ttu-id="dcc4a-127">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="dcc4a-127">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="dcc4a-128">获取此团队已安装应用的列表。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-128">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="dcc4a-129">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="dcc4a-129">TeamsTab.Read.Group</span></span>|<span data-ttu-id="dcc4a-130">获取此团队的选项卡列表。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-130">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="dcc4a-131">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="dcc4a-131">TeamsTab.Create.Group</span></span>|<span data-ttu-id="dcc4a-132">在此团队中创建选项卡。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-132">Create tabs in this team.</span></span>|
|<span data-ttu-id="dcc4a-133">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="dcc4a-133">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="dcc4a-134">更新此团队的选项卡。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-134">Update this team's tabs.</span></span>|
|<span data-ttu-id="dcc4a-135">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="dcc4a-135">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="dcc4a-136">删除此团队的选项卡。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-136">Delete this team's tabs.</span></span>|
|<span data-ttu-id="dcc4a-137">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="dcc4a-137">TeamMember.Read.Group</span></span>|<span data-ttu-id="dcc4a-138">获取此团队的成员。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-138">Get this team's members.</span></span>|

<span data-ttu-id="dcc4a-139">有关详细信息，请参阅Teams[特定资源的同意权限](/graph/permissions-reference#teams-resource-specific-consent-permissions)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-139">For more details, see [Teams resource-specific consent permissions](/graph/permissions-reference#teams-resource-specific-consent-permissions).</span></span>

### <a name="resource-specific-permissions-for-a-chat"></a><span data-ttu-id="dcc4a-140">聊天的特定于资源的权限</span><span class="sxs-lookup"><span data-stu-id="dcc4a-140">Resource-specific permissions for a chat</span></span>
|<span data-ttu-id="dcc4a-141">应用权限</span><span class="sxs-lookup"><span data-stu-id="dcc4a-141">Application permission</span></span>| <span data-ttu-id="dcc4a-142">操作</span><span class="sxs-lookup"><span data-stu-id="dcc4a-142">Action</span></span> |
| ----- | ----- |
| <span data-ttu-id="dcc4a-143">ChatSettings.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="dcc4a-143">ChatSettings.Read.Chat</span></span>         | <span data-ttu-id="dcc4a-144">获取此聊天的设置。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-144">Get this chat's settings.</span></span>                                    |
| <span data-ttu-id="dcc4a-145">ChatSettings.ReadWrite.Chat</span><span class="sxs-lookup"><span data-stu-id="dcc4a-145">ChatSettings.ReadWrite.Chat</span></span>    | <span data-ttu-id="dcc4a-146">更新此聊天的设置。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-146">Update this chat's settings.</span></span>                          |
| <span data-ttu-id="dcc4a-147">ChatMessage.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="dcc4a-147">ChatMessage.Read.Chat</span></span>          | <span data-ttu-id="dcc4a-148">获取此聊天的消息。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-148">Get this chat's messages.</span></span>                                    |
| <span data-ttu-id="dcc4a-149">ChatMember.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="dcc4a-149">ChatMember.Read.Chat</span></span>           | <span data-ttu-id="dcc4a-150">获取此聊天的成员。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-150">Get this chat's members.</span></span>                                     |
| <span data-ttu-id="dcc4a-151">Chat.Manage.Chat</span><span class="sxs-lookup"><span data-stu-id="dcc4a-151">Chat.Manage.Chat</span></span>               | <span data-ttu-id="dcc4a-152">管理此聊天。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-152">Manage this chat.</span></span>                                             |
| <span data-ttu-id="dcc4a-153">TeamsTab.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="dcc4a-153">TeamsTab.Read.Chat</span></span>             | <span data-ttu-id="dcc4a-154">获取此聊天的选项卡。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-154">Get this chat's tabs.</span></span>                                        |
| <span data-ttu-id="dcc4a-155">TeamsTab.Create.Chat</span><span class="sxs-lookup"><span data-stu-id="dcc4a-155">TeamsTab.Create.Chat</span></span>           | <span data-ttu-id="dcc4a-156">在此聊天中创建选项卡。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-156">Create tabs in this chat.</span></span>                                     |
| <span data-ttu-id="dcc4a-157">TeamsTab.Delete.Chat</span><span class="sxs-lookup"><span data-stu-id="dcc4a-157">TeamsTab.Delete.Chat</span></span>           | <span data-ttu-id="dcc4a-158">删除此聊天的选项卡。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-158">Delete this chat's tabs.</span></span>                                      |
| <span data-ttu-id="dcc4a-159">TeamsTab.ReadWrite.Chat</span><span class="sxs-lookup"><span data-stu-id="dcc4a-159">TeamsTab.ReadWrite.Chat</span></span>        | <span data-ttu-id="dcc4a-160">管理此聊天的选项卡。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-160">Manage this chat's tabs.</span></span>                                      |
| <span data-ttu-id="dcc4a-161">TeamsAppInstallation.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="dcc4a-161">TeamsAppInstallation.Read.Chat</span></span> | <span data-ttu-id="dcc4a-162">获取此聊天中安装的应用。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-162">Get which apps are installed in this chat.</span></span>                   |
| <span data-ttu-id="dcc4a-163">OnlineMeeting.ReadBasic.Chat</span><span class="sxs-lookup"><span data-stu-id="dcc4a-163">OnlineMeeting.ReadBasic.Chat</span></span>   | <span data-ttu-id="dcc4a-164">获取与此聊天关联的会议的基本属性，如名称、日程安排、组织者和加入链接。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-164">Get basic properties—such as name, schedule, organizer, and join link—of a meeting associated with this chat.</span></span> |

<span data-ttu-id="dcc4a-165">有关详细信息，请参阅聊天 [资源特定的许可权限](/graph/permissions-reference#chat-resource-specific-consent-permissions)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-165">For more details, see [Chat resource-specific consent permissions](/graph/permissions-reference#chat-resource-specific-consent-permissions).</span></span>

>[!NOTE]
><span data-ttu-id="dcc4a-166">特定于资源的权限仅适用于安装在 Teams 客户端上的Teams应用，并且当前不是 Azure Active Directory 门户的一部分。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-166">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory portal.</span></span>

## <a name="enable-resource-specific-consent-in-your-application"></a><span data-ttu-id="dcc4a-167">在应用程序中启用特定于资源的同意</span><span class="sxs-lookup"><span data-stu-id="dcc4a-167">Enable resource-specific consent in your application</span></span>

<span data-ttu-id="dcc4a-168">在应用程序中启用 RSC 的步骤如下所示：</span><span class="sxs-lookup"><span data-stu-id="dcc4a-168">The steps for enabling RSC in your application are as follows:</span></span>

1. <span data-ttu-id="dcc4a-169">[配置许可门户中的Azure Active Directory设置](#configure-consent-settings-in-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-169">[Configure consent settings in the Azure Active Directory portal](#configure-consent-settings-in-the-azure-ad-portal).</span></span>
    1. <span data-ttu-id="dcc4a-170">[为团队中的 RSC 配置组所有者同意设置](#configure-group-owner-consent-settings-for-rsc-in-a-team)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-170">[Configure group owner consent settings for RSC in a team](#configure-group-owner-consent-settings-for-rsc-in-a-team).</span></span>
    1. <span data-ttu-id="dcc4a-171">[在聊天中为 RSC 配置用户同意设置](#configure-user-consent-settings-for-rsc-in-a-chat)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-171">[Configure user consent settings for RSC in a chat](#configure-user-consent-settings-for-rsc-in-a-chat).</span></span>
1. <span data-ttu-id="dcc4a-172">[通过 Azure AD Microsoft 标识平台注册应用](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-172">[Register your app with Microsoft identity platform via the Azure AD portal](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="dcc4a-173">[查看 Azure AD 门户中的应用程序权限](#review-your-application-permissions-in-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-173">[Review your application permissions in the Azure AD portal](#review-your-application-permissions-in-the-azure-ad-portal).</span></span>
1. <span data-ttu-id="dcc4a-174">[从 Microsoft Identity 平台获取访问令牌](#obtain-an-access-token-from-the-microsoft-identity-platform)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-174">[Obtain an access token from the Microsoft Identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="dcc4a-175">[更新应用Teams清单](#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-175">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="dcc4a-176">[直接在 Teams 中安装应用](#sideload-your-app-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-176">[Install your app directly in Teams](#sideload-your-app-in-teams).</span></span>
1. <span data-ttu-id="dcc4a-177">[检查应用是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-177">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>
    1. <span data-ttu-id="dcc4a-178">[检查你的应用在团队中是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions-in-a-team)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-178">[Check your app for added RSC permissions in a team](#check-your-app-for-added-rsc-permissions-in-a-team).</span></span>
    1. <span data-ttu-id="dcc4a-179">[检查你的应用在聊天中是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions-in-a-chat)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-179">[Check your app for added RSC permissions in a chat](#check-your-app-for-added-rsc-permissions-in-a-chat).</span></span>

## <a name="configure-consent-settings-in-the-azure-ad-portal"></a><span data-ttu-id="dcc4a-180">在 Azure AD 门户中配置许可设置</span><span class="sxs-lookup"><span data-stu-id="dcc4a-180">Configure consent settings in the Azure AD portal</span></span>

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a><span data-ttu-id="dcc4a-181">为团队中的 RSC 配置组所有者同意设置</span><span class="sxs-lookup"><span data-stu-id="dcc4a-181">Configure group owner consent settings for RSC in a team</span></span>

<span data-ttu-id="dcc4a-182">可以直接在 Azure 门户 [中启用](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) 或禁用组所有者同意：</span><span class="sxs-lookup"><span data-stu-id="dcc4a-182">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="dcc4a-183">以全局管理员/公司管理员登录 [Azure](https://portal.azure.com) [门户](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-183">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).</span></span>  
 > - <span data-ttu-id="dcc4a-184">[选择](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)**Azure Active Directory Enterprise**  =>    =>  **同意和权限**  =>  **用户同意设置"。**</span><span class="sxs-lookup"><span data-stu-id="dcc4a-184">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="dcc4a-185">使用标记为组所有者同意的控件启用、禁用或限制用户同意访问数据 (默认值为允许组所有者同意所有组所有者) 。 </span><span class="sxs-lookup"><span data-stu-id="dcc4a-185">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data** (The default is **Allow group owner consent for all group owners**).</span></span> <span data-ttu-id="dcc4a-186">对于使用 RSC 安装应用的团队所有者，必须为该用户启用组所有者同意。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-186">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

![azure rsc 团队配置](../../assets/images/azure-rsc-team-configuration.png)

<span data-ttu-id="dcc4a-188">若要使用 PowerShell 启用或禁用组所有者同意，请按照使用 PowerShell 配置组所有者 [同意中概述的步骤操作](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-188">To enable or disable group owner consent using PowerShell, follow the steps outlined in [Configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a><span data-ttu-id="dcc4a-189">在聊天中为 RSC 配置用户同意设置</span><span class="sxs-lookup"><span data-stu-id="dcc4a-189">Configure user consent settings for RSC in a chat</span></span>

<span data-ttu-id="dcc4a-190">可以直接在 Azure 门户 [中启用](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) 或禁用用户同意：</span><span class="sxs-lookup"><span data-stu-id="dcc4a-190">You can enable or disable [user consent](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) directly within the Azure portal:</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="dcc4a-191">以全局管理员/公司管理员登录 [Azure](https://portal.azure.com) [门户](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-191">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator/Company Administrator](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).</span></span>  
 > - <span data-ttu-id="dcc4a-192">[选择](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)**Azure Active Directory Enterprise**  =>    =>  **同意和权限**  =>  **用户同意设置"。**</span><span class="sxs-lookup"><span data-stu-id="dcc4a-192">[Select](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings) **Azure Active Directory** => **Enterprise applications** => **Consent and permissions** => **User consent settings**.</span></span>
> - <span data-ttu-id="dcc4a-193">启用、禁用或限制用户同意，但标有"应用程序用户同意 (默认为"允许用户同意应用 **或**) "。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-193">Enable, disable, or limit user consent with the control labeled **User consent for applications** (The default is **Allow user consent for apps**).</span></span> <span data-ttu-id="dcc4a-194">若要聊天成员使用 RSC 安装应用，必须为该用户启用用户同意。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-194">For a chat member to install an app using RSC, user consent must be enabled for that user.</span></span>

![azure rsc 聊天配置](../../assets/images/azure-rsc-chat-configuration.png)

<span data-ttu-id="dcc4a-196">若要使用 PowerShell 启用或禁用用户同意，请按照使用 PowerShell 配置用户同意中 [概述的步骤操作](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-196">To enable or disable user consent using PowerShell, follow the steps outlined in [Configure user consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell).</span></span>


## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a><span data-ttu-id="dcc4a-197">通过 Azure AD Microsoft 标识平台注册应用</span><span class="sxs-lookup"><span data-stu-id="dcc4a-197">Register your app with Microsoft identity platform via the Azure AD portal</span></span>

<span data-ttu-id="dcc4a-198">Azure Active Directory门户提供了一个中央平台，用于注册和配置应用。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-198">The Azure Active Directory portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="dcc4a-199">应用必须在 Azure AD 门户中注册，才能与 Microsoft 标识平台 并调用 Microsoft Graph API。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-199">Your app must be registered in the Azure AD portal to integrate with the Microsoft identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="dcc4a-200">有关详细信息，请参阅向应用程序[注册Microsoft 标识平台。](/graph/auth-register-app-v2)</span><span class="sxs-lookup"><span data-stu-id="dcc4a-200">For more information, see [Register an application with the Microsoft identity platform](/graph/auth-register-app-v2).</span></span>

>[!WARNING]
><span data-ttu-id="dcc4a-201">Azure AD 应用 ID 不应在多个应用之间Teams共享。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-201">An Azure AD app ID should not be shared across multiple Teams apps.</span></span> <span data-ttu-id="dcc4a-202">应用和 Azure AD 应用之间应该Teams一对一映射。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-202">There should be a 1:1 mapping between a Teams App and an Azure AD app.</span></span> <span data-ttu-id="dcc4a-203">尝试安装多个与Teams Azure AD 应用 ID 关联的应用将导致安装/运行时失败。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-203">Attempts to install multiple Teams apps which are associated with the same Azure AD app ID will cause installation/runtime failures.</span></span>

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a><span data-ttu-id="dcc4a-204">在 Azure AD 门户中查看应用程序权限</span><span class="sxs-lookup"><span data-stu-id="dcc4a-204">Review your application permissions in the Azure AD portal</span></span>

<span data-ttu-id="dcc4a-205">导航到 **"主页**  =>  **应用注册"** 页并选择 RSC 应用。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-205">Navigate to the **Home** => **App registrations** page and select your RSC app.</span></span> <span data-ttu-id="dcc4a-206">从 **左侧导航** 栏中选择 API 权限，并检查应用的已配置权限列表。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-206">Choose **API permissions** from the left nav bar and examine the list of configured permissions for your app.</span></span> <span data-ttu-id="dcc4a-207">如果你的应用将仅执行 RSC Graph API 调用，请删除该页面上的所有权限。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-207">If your app will only make RSC Graph API calls, delete all the permission on that page.</span></span> <span data-ttu-id="dcc4a-208">如果你的应用还将进行非 RSC 调用，请根据需要保留这些权限。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-208">If your app will also make non-RSC calls, keep those permissions as needed.</span></span>

>[!IMPORTANT]
><span data-ttu-id="dcc4a-209">Azure AD 门户不能用于请求 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-209">The Azure AD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="dcc4a-210">RSC 权限当前专用于 Teams 客户端中安装的 Teams 应用程序，这些权限在 Teams 应用程序清单 (JSON) 文件中声明。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-210">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the Teams app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="dcc4a-211">从应用程序获取访问Microsoft 标识平台</span><span class="sxs-lookup"><span data-stu-id="dcc4a-211">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="dcc4a-212">若要Graph API 调用，必须从标识平台获取应用的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-212">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="dcc4a-213">应用必须先在 Azure AD 门户Microsoft 标识平台令牌，然后才能从应用获取令牌。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-213">Before your app can get a token from the Microsoft identity platform, it must be registered in the Azure AD portal.</span></span> <span data-ttu-id="dcc4a-214">访问令牌包含你的应用的相关信息，还有它就可通过 Microsoft Graph 访问的资源和 API 所具备的权限。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-214">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="dcc4a-215">你需要从 Azure AD 注册过程获取以下值，以从标识平台检索访问令牌：</span><span class="sxs-lookup"><span data-stu-id="dcc4a-215">You'll need to have the following values from the Azure AD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="dcc4a-216">应用注册门户分配的应用程序 **ID。**</span><span class="sxs-lookup"><span data-stu-id="dcc4a-216">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="dcc4a-217">如果你的应用支持单一登录 (SSO) 应用和 SSO 应使用相同的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-217">If your app supports single sign-on (SSO) you should use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="dcc4a-218">客户端 **密码/密码** 或公钥/私钥对 (**证书) 。**</span><span class="sxs-lookup"><span data-stu-id="dcc4a-218">The  **Client secret/password** or a public/private key pair (**Certificate**).</span></span> <span data-ttu-id="dcc4a-219">这不是本机应用的必需项。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-219">This is not required for native apps.</span></span>
- <span data-ttu-id="dcc4a-220">重定向 **URI** (或回复 URL) 应用接收来自 Azure AD 的响应。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-220">A **Redirect URI** (or reply URL) for your app to receive responses from Azure AD.</span></span>

 <span data-ttu-id="dcc4a-221">*请参阅*[代表用户获取访问权限和](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true)[在没有用户的情况下获取访问权限](/graph/auth-v2-service)</span><span class="sxs-lookup"><span data-stu-id="dcc4a-221">*See* [Get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [Get access without a user](/graph/auth-v2-service)</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="dcc4a-222">更新Teams应用程序清单</span><span class="sxs-lookup"><span data-stu-id="dcc4a-222">Update your Teams app manifest</span></span>

<span data-ttu-id="dcc4a-223">RSC 权限在应用清单 (JSON) 文件中声明。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-223">The RSC permissions are declared in your app manifest (JSON) file.</span></span>  <span data-ttu-id="dcc4a-224">将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：</span><span class="sxs-lookup"><span data-stu-id="dcc4a-224">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

> [!div class="checklist"]
>
> - <span data-ttu-id="dcc4a-225">**id**  — 你的 Azure AD 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-225">**id**  — your Azure AD app ID.</span></span> <span data-ttu-id="dcc4a-226">有关详细信息，请参阅在 [Azure AD 门户中注册应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-226">For more information, see [Register your app in the Azure AD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal).</span></span>
> - <span data-ttu-id="dcc4a-227">**resource**  — 任何字符串。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-227">**resource**  — any string.</span></span> <span data-ttu-id="dcc4a-228">此字段在 RSC 中没有任何操作，但必须添加该字段，并且必须具有值以避免错误响应;任何字符串将执行。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-228">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>
> - <span data-ttu-id="dcc4a-229">**应用程序权限** — 应用的 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-229">**application permissions** — RSC permissions for  your app.</span></span> <span data-ttu-id="dcc4a-230">有关详细信息，请参阅资源 [特定的权限](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-230">For more information, see [Resource-specific Permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>

>
>[!IMPORTANT]
> <span data-ttu-id="dcc4a-231">非 RSC 权限存储在 Azure 门户中。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-231">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="dcc4a-232">不要将它们添加到应用清单。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-232">Do not add them to the app manifest.</span></span>
>

### <a name="example-for-rsc-in-a-team"></a><span data-ttu-id="dcc4a-233">团队中的 RSC 示例</span><span class="sxs-lookup"><span data-stu-id="dcc4a-233">Example for RSC in a team</span></span>
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

### <a name="example-for-rsc-in-a-chat"></a><span data-ttu-id="dcc4a-234">聊天中的 RSC 示例</span><span class="sxs-lookup"><span data-stu-id="dcc4a-234">Example for RSC in a chat</span></span>
```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
      "ChatSettings.Read.Chat",
      "ChatSettings.ReadWrite.Chat",
      "ChatMessage.Read.Chat",
      "ChatMember.Read.Chat",
      "Chat.Manage.Chat",
      "TeamsTab.Read.Chat",
      "TeamsTab.Create.Chat",
      "TeamsTab.Delete.Chat",
      "TeamsTab.ReadWrite.Chat",
      "TeamsAppInstallation.Read.Chat",
      "OnlineMeeting.ReadBasic.Chat"
    ]
  }
```

>[!NOTE]
><span data-ttu-id="dcc4a-235">如果应用旨在支持在团队和聊天范围内安装，可以在 下的同一清单中指定团队和聊天权限 `applicationPermissions` 。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-235">If the app is meant to support installation in both team and chat scopes, then both team and chat permissions can be specified in the same manifest under `applicationPermissions`.</span></span>

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="dcc4a-236">在应用程序中旁加载Teams</span><span class="sxs-lookup"><span data-stu-id="dcc4a-236">Sideload your app in Teams</span></span>

<span data-ttu-id="dcc4a-237">如果你的Teams管理员允许自定义应用上传，你可以将应用直接旁加载[](~/concepts/deploy-and-publish/apps-upload.md)到特定团队或聊天。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-237">If your Teams admin allows custom app uploads, you can [sideload your app](~/concepts/deploy-and-publish/apps-upload.md) directly to a specific team or chat.</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="dcc4a-238">检查应用是否添加了 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="dcc4a-238">Check your app for added RSC permissions</span></span>

>[!IMPORTANT]
><span data-ttu-id="dcc4a-239">RSC 权限不归为用户。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-239">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="dcc4a-240">调用使用应用程序权限而不是用户委派权限进行。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-240">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="dcc4a-241">因此，可以允许应用执行用户无法执行的操作，例如删除选项卡。在调用 RSC API 之前，应查看团队所有者或聊天所有者对用例的意图。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-241">Thus, the app may be allowed to perform actions that the user cannot, such as deleting a tab. You should review the team owner's or chat owner's intent for your use case prior to making RSC API calls.</span></span> <span data-ttu-id="dcc4a-242">有关详细信息，请参阅 Microsoft Teams [API 概述](/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-242">For more information, see [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="dcc4a-243">将应用安装到资源后，可以使用Graph[资源管理器](https://developer.microsoft.com/graph/graph-explorer)查看已授予资源中应用程序的权限：</span><span class="sxs-lookup"><span data-stu-id="dcc4a-243">Once the app has been installed to a resource, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer)  to view the permissions that have been granted to the app in the resource:</span></span>

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a><span data-ttu-id="dcc4a-244">检查你的应用在团队中是否添加了 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="dcc4a-244">Check your app for added RSC permissions in a team</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="dcc4a-245">从客户端获取团队的 **groupId** Teams Id。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-245">Get the team's **groupId** from the Teams client.</span></span>
> - <span data-ttu-id="dcc4a-246">在Teams客户端中，Teams **左侧导航** 栏选择"导航"。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-246">In the Teams client, select **Teams** from the far left nav bar.</span></span>
> - <span data-ttu-id="dcc4a-247">从下拉菜单中选择安装应用的团队。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-247">Select the team where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="dcc4a-248">选择" **更多选项"** 图标 (&#8943;) 。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-248">Select the **More options** icon (&#8943;).</span></span>
> - <span data-ttu-id="dcc4a-249">选择 **获取团队链接**。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-249">Select **Get link to team**.</span></span>
> - <span data-ttu-id="dcc4a-250">复制并保存字符串中的 **groupId** 值。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-250">Copy and save the **groupId** value from the string.</span></span>
> - <span data-ttu-id="dcc4a-251">登录到 **Graph 资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-251">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="dcc4a-252">对以下 **终结点** 进行 GET 调用 `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants` ：。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-252">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="dcc4a-253">响应 `clientAppId` 中的字段将映射到应用程序清单 `webApplicationInfo.id` Teams中指定的。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-253">The `clientAppId` field in the response will map to the `webApplicationInfo.id` specified in the Teams app manifest.</span></span>
  <span data-ttu-id="dcc4a-254">![Graph对获取团队 RSC 权限的 GET 调用的浏览器响应。](../../assets/images/team-graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="dcc4a-254">![Graph explorer response to GET call for team RSC permissions.](../../assets/images/team-graph-permissions.png)</span></span>

<span data-ttu-id="dcc4a-255">若要了解如何获取有关特定团队中安装的应用的详细信息，请参阅获取指定团队中安装的应用的名称 [和其他详细信息](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-255">For information about how to get details about apps installed in a specific team, see [Get the names and other details of apps installed in the specified team](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps).</span></span>

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a><span data-ttu-id="dcc4a-256">检查你的应用在聊天中是否添加了 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="dcc4a-256">Check your app for added RSC permissions in a chat</span></span>

> [!div class="checklist"]
>
>- <span data-ttu-id="dcc4a-257">从 Web 客户端获取Teams *ID。*</span><span class="sxs-lookup"><span data-stu-id="dcc4a-257">Get the chat thread ID from the Teams *web* client.</span></span>
> - <span data-ttu-id="dcc4a-258">在 web Teams中 **，从最** 左侧导航栏中选择"聊天"。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-258">In the Teams web client, select **Chat** from the far left nav bar.</span></span>
> - <span data-ttu-id="dcc4a-259">从下拉菜单中选择应用安装位置的聊天。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-259">Select the chat where the app is installed from the drop-down menu.</span></span>
> - <span data-ttu-id="dcc4a-260">复制 Web URL，然后从字符串中保存聊天线程 ID。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-260">Copy the web URL and save the chat thread ID from the string.</span></span>
<span data-ttu-id="dcc4a-261">![来自 Web URL 的聊天线程 ID。](../../assets/images/chat-thread-id.png)</span><span class="sxs-lookup"><span data-stu-id="dcc4a-261">![Chat thread id from web URL.](../../assets/images/chat-thread-id.png)</span></span>
> - <span data-ttu-id="dcc4a-262">登录到 **Graph 资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-262">Log into **Graph Explorer**.</span></span>
> - <span data-ttu-id="dcc4a-263">对以下 **终结点** 进行 GET 调用 `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants` ：。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-263">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants`.</span></span> <span data-ttu-id="dcc4a-264">响应 `clientAppId` 中的字段将映射到应用程序清单 `webApplicationInfo.id` Teams中指定的。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-264">The `clientAppId` field in the response will map to the `webApplicationInfo.id` specified in the Teams app manifest.</span></span>
  <span data-ttu-id="dcc4a-265">![Graph对聊天 RSC 权限的 GET 调用的浏览器响应。](../../assets/images/chat-graph-permissions.png)</span><span class="sxs-lookup"><span data-stu-id="dcc4a-265">![Graph explorer response to GET call for chat RSC permissions.](../../assets/images/chat-graph-permissions.png)</span></span>

<span data-ttu-id="dcc4a-266">若要了解如何获取有关特定聊天中安装的应用的详细信息，请参阅获取指定聊天中安装的应用的名称 [和其他详细信息](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-266">For information about how to get details about apps installed in a specific chat, see [Get the names and other details of apps installed in the specified chat](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat).</span></span>

## <a name="code-sample"></a><span data-ttu-id="dcc4a-267">代码示例</span><span class="sxs-lookup"><span data-stu-id="dcc4a-267">Code sample</span></span>
| <span data-ttu-id="dcc4a-268">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="dcc4a-268">**Sample name**</span></span> | <span data-ttu-id="dcc4a-269">**说明**</span><span class="sxs-lookup"><span data-stu-id="dcc4a-269">**Description**</span></span> | <span data-ttu-id="dcc4a-270">**.NET**</span><span class="sxs-lookup"><span data-stu-id="dcc4a-270">**.NET**</span></span> |<span data-ttu-id="dcc4a-271">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="dcc4a-271">**Node.js**</span></span> |
|-----------------|-----------------|----------------|----------------|
| <span data-ttu-id="dcc4a-272">RSC (资源特定) </span><span class="sxs-lookup"><span data-stu-id="dcc4a-272">Resource Specific Consent (RSC)</span></span> | <span data-ttu-id="dcc4a-273">使用 RSC 调用Graph API。</span><span class="sxs-lookup"><span data-stu-id="dcc4a-273">Use RSC to call Graph APIs.</span></span> | [<span data-ttu-id="dcc4a-274">View</span><span class="sxs-lookup"><span data-stu-id="dcc4a-274">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[<span data-ttu-id="dcc4a-275">View</span><span class="sxs-lookup"><span data-stu-id="dcc4a-275">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="see-also"></a><span data-ttu-id="dcc4a-276">另请参阅</span><span class="sxs-lookup"><span data-stu-id="dcc4a-276">See also</span></span>
 
* [<span data-ttu-id="dcc4a-277">在应用程序内测试特定于资源的许可Teams</span><span class="sxs-lookup"><span data-stu-id="dcc4a-277">Test resource-specific consent permissions in Teams</span></span>](test-resource-specific-consent.md)
* [<span data-ttu-id="dcc4a-278">管理员许可中Microsoft Teams特定资源的同意</span><span class="sxs-lookup"><span data-stu-id="dcc4a-278">Resource-specific consent in Microsoft Teams for admins</span></span>](/MicrosoftTeams/resource-specific-consent)


