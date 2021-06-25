---
title: 在"管理"中启用特定于资源Teams
description: 介绍资源特定的Teams以及如何利用它。
localization_priority: Normal
author: akjo
ms.author: lajanuar
ms.topic: reference
keywords: teams 授权 OAuth SSO AAD rsc Graph
ms.openlocfilehash: 4573140e33bffb0daafbdc9f929b5afd49231af8
ms.sourcegitcommit: 6e4d2c8e99426125f7b72b9640ee4a4b4f374401
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/24/2021
ms.locfileid: "53114418"
---
# <a name="resource-specific-consent"></a><span data-ttu-id="efdae-104">资源特定许可</span><span class="sxs-lookup"><span data-stu-id="efdae-104">Resource-specific consent</span></span>

> [!NOTE]
> <span data-ttu-id="efdae-105">聊天范围的特定于资源的同意仅适用于 [公共开发人员预览](../../resources/dev-preview/developer-preview-intro.md) 版。</span><span class="sxs-lookup"><span data-stu-id="efdae-105">Resource-specific consent for chat scope is available in [public developer preview](../../resources/dev-preview/developer-preview-intro.md) only.</span></span>

<span data-ttu-id="efdae-106">资源特定的同意 (RSC) 是一种 Microsoft Teams 和 Microsoft Graph API 集成，使你的应用可以使用 API 终结点来管理组织中特定的资源（团队或聊天）。</span><span class="sxs-lookup"><span data-stu-id="efdae-106">Resource-specific consent (RSC) is a Microsoft Teams and Microsoft Graph API integration that enables your app to use API endpoints to manage specific resources, either teams or chats, within an organization.</span></span> <span data-ttu-id="efdae-107">RSC 权限模型使团队所有者和聊天所有者可以分别授予应用程序访问和修改团队数据和聊天数据的许可。</span><span class="sxs-lookup"><span data-stu-id="efdae-107">The RSC permissions model enables *team owners* and *chat owners* to grant consent for an application to access and modify a team's data and a chat's data, respectively.</span></span>

## <a name="resource-specific-permissions"></a><span data-ttu-id="efdae-108">特定于资源的权限</span><span class="sxs-lookup"><span data-stu-id="efdae-108">Resource-specific permissions</span></span>

<span data-ttu-id="efdae-109">具体、Teams特定的 RSC 权限定义应用程序可以在特定资源中执行哪些操作。</span><span class="sxs-lookup"><span data-stu-id="efdae-109">The granular, Teams-specific, RSC permissions define what an application can do within a specific resource.</span></span>

### <a name="resource-specific-permissions-for-a-team"></a><span data-ttu-id="efdae-110">团队的特定于资源的权限</span><span class="sxs-lookup"><span data-stu-id="efdae-110">Resource-specific permissions for a team</span></span>

|<span data-ttu-id="efdae-111">应用权限</span><span class="sxs-lookup"><span data-stu-id="efdae-111">Application permission</span></span>| <span data-ttu-id="efdae-112">操作</span><span class="sxs-lookup"><span data-stu-id="efdae-112">Action</span></span> |
| ----- | ----- |
|<span data-ttu-id="efdae-113">TeamSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="efdae-113">TeamSettings.Read.Group</span></span> | <span data-ttu-id="efdae-114">获取此团队的设置。</span><span class="sxs-lookup"><span data-stu-id="efdae-114">Get this team's settings.</span></span>|
|<span data-ttu-id="efdae-115">TeamSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="efdae-115">TeamSettings.ReadWrite.Group</span></span>|<span data-ttu-id="efdae-116">更新此团队的设置。</span><span class="sxs-lookup"><span data-stu-id="efdae-116">Update this team's settings.</span></span>|
|<span data-ttu-id="efdae-117">ChannelSettings.Read.Group</span><span class="sxs-lookup"><span data-stu-id="efdae-117">ChannelSettings.Read.Group</span></span>|<span data-ttu-id="efdae-118">获取此团队的频道名称、频道说明和频道设置。</span><span class="sxs-lookup"><span data-stu-id="efdae-118">Get this team's channel names, channel descriptions, and channel settings.</span></span>|
|<span data-ttu-id="efdae-119">ChannelSettings.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="efdae-119">ChannelSettings.ReadWrite.Group</span></span>|<span data-ttu-id="efdae-120">更新此团队的频道名称、频道说明和频道设置。</span><span class="sxs-lookup"><span data-stu-id="efdae-120">Update this team's channel names, channel descriptions, and channel settings.</span></span>|
|<span data-ttu-id="efdae-121">Channel.Create.Group</span><span class="sxs-lookup"><span data-stu-id="efdae-121">Channel.Create.Group</span></span>|<span data-ttu-id="efdae-122">在这个团队中创建频道。</span><span class="sxs-lookup"><span data-stu-id="efdae-122">Create channels in this team.</span></span> |
|<span data-ttu-id="efdae-123">Channel.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="efdae-123">Channel.Delete.Group</span></span>|<span data-ttu-id="efdae-124">删除此团队中的频道。</span><span class="sxs-lookup"><span data-stu-id="efdae-124">Delete channels in this team.</span></span> |
|<span data-ttu-id="efdae-125">ChannelMessage.Read.Group</span><span class="sxs-lookup"><span data-stu-id="efdae-125">ChannelMessage.Read.Group</span></span> |<span data-ttu-id="efdae-126">获取此团队的频道消息。</span><span class="sxs-lookup"><span data-stu-id="efdae-126">Get this team's channel messages.</span></span> |
|<span data-ttu-id="efdae-127">TeamsAppInstallation.Read.Group</span><span class="sxs-lookup"><span data-stu-id="efdae-127">TeamsAppInstallation.Read.Group</span></span>|<span data-ttu-id="efdae-128">获取此团队已安装应用的列表。</span><span class="sxs-lookup"><span data-stu-id="efdae-128">Get a list of this team's installed apps.</span></span>|
|<span data-ttu-id="efdae-129">TeamsTab.Read.Group</span><span class="sxs-lookup"><span data-stu-id="efdae-129">TeamsTab.Read.Group</span></span>|<span data-ttu-id="efdae-130">获取此团队的选项卡列表。</span><span class="sxs-lookup"><span data-stu-id="efdae-130">Get a list of this team's tabs.</span></span>|
|<span data-ttu-id="efdae-131">TeamsTab.Create.Group</span><span class="sxs-lookup"><span data-stu-id="efdae-131">TeamsTab.Create.Group</span></span>|<span data-ttu-id="efdae-132">在此团队中创建选项卡。</span><span class="sxs-lookup"><span data-stu-id="efdae-132">Create tabs in this team.</span></span> |
|<span data-ttu-id="efdae-133">TeamsTab.ReadWrite.Group</span><span class="sxs-lookup"><span data-stu-id="efdae-133">TeamsTab.ReadWrite.Group</span></span>|<span data-ttu-id="efdae-134">更新此团队的选项卡。</span><span class="sxs-lookup"><span data-stu-id="efdae-134">Update this team's tabs.</span></span> |
|<span data-ttu-id="efdae-135">TeamsTab.Delete.Group</span><span class="sxs-lookup"><span data-stu-id="efdae-135">TeamsTab.Delete.Group</span></span>|<span data-ttu-id="efdae-136">删除此团队的选项卡。</span><span class="sxs-lookup"><span data-stu-id="efdae-136">Delete this team's tabs.</span></span> |
|<span data-ttu-id="efdae-137">TeamMember.Read.Group</span><span class="sxs-lookup"><span data-stu-id="efdae-137">TeamMember.Read.Group</span></span>|<span data-ttu-id="efdae-138">获取此团队的成员。</span><span class="sxs-lookup"><span data-stu-id="efdae-138">Get this team's members.</span></span> |

<span data-ttu-id="efdae-139">有关详细信息，请参阅团队 [资源特定的许可权限](/graph/permissions-reference#teams-resource-specific-consent-permissions)。</span><span class="sxs-lookup"><span data-stu-id="efdae-139">For more details, see [team resource-specific consent permissions](/graph/permissions-reference#teams-resource-specific-consent-permissions).</span></span>

### <a name="resource-specific-permissions-for-a-chat"></a><span data-ttu-id="efdae-140">聊天的特定于资源的权限</span><span class="sxs-lookup"><span data-stu-id="efdae-140">Resource-specific permissions for a chat</span></span>

<span data-ttu-id="efdae-141">下表提供了聊天的特定于资源的权限：</span><span class="sxs-lookup"><span data-stu-id="efdae-141">The following table provides resource-specific permissions for a chat:</span></span>

|<span data-ttu-id="efdae-142">应用权限</span><span class="sxs-lookup"><span data-stu-id="efdae-142">Application permission</span></span>| <span data-ttu-id="efdae-143">操作</span><span class="sxs-lookup"><span data-stu-id="efdae-143">Action</span></span> |
| ----- | ----- |
| <span data-ttu-id="efdae-144">ChatSettings.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="efdae-144">ChatSettings.Read.Chat</span></span>         | <span data-ttu-id="efdae-145">获取此聊天的设置。</span><span class="sxs-lookup"><span data-stu-id="efdae-145">Get this chat's settings.</span></span>                                    |
| <span data-ttu-id="efdae-146">ChatSettings.ReadWrite.Chat</span><span class="sxs-lookup"><span data-stu-id="efdae-146">ChatSettings.ReadWrite.Chat</span></span>    | <span data-ttu-id="efdae-147">更新此聊天的设置。</span><span class="sxs-lookup"><span data-stu-id="efdae-147">Update this chat's settings.</span></span>                          |
| <span data-ttu-id="efdae-148">ChatMessage.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="efdae-148">ChatMessage.Read.Chat</span></span>          | <span data-ttu-id="efdae-149">获取此聊天的消息。</span><span class="sxs-lookup"><span data-stu-id="efdae-149">Get this chat's messages.</span></span>                                    |
| <span data-ttu-id="efdae-150">ChatMember.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="efdae-150">ChatMember.Read.Chat</span></span>           | <span data-ttu-id="efdae-151">获取此聊天的成员。</span><span class="sxs-lookup"><span data-stu-id="efdae-151">Get this chat's members.</span></span>                                     |
| <span data-ttu-id="efdae-152">Chat.Manage.Chat</span><span class="sxs-lookup"><span data-stu-id="efdae-152">Chat.Manage.Chat</span></span>               | <span data-ttu-id="efdae-153">管理此聊天。</span><span class="sxs-lookup"><span data-stu-id="efdae-153">Manage this chat.</span></span>                                             |
| <span data-ttu-id="efdae-154">TeamsTab.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="efdae-154">TeamsTab.Read.Chat</span></span>             | <span data-ttu-id="efdae-155">获取此聊天的选项卡。</span><span class="sxs-lookup"><span data-stu-id="efdae-155">Get this chat's tabs.</span></span>                                        |
| <span data-ttu-id="efdae-156">TeamsTab.Create.Chat</span><span class="sxs-lookup"><span data-stu-id="efdae-156">TeamsTab.Create.Chat</span></span>           | <span data-ttu-id="efdae-157">在此聊天中创建选项卡。</span><span class="sxs-lookup"><span data-stu-id="efdae-157">Create tabs in this chat.</span></span>                                     |
| <span data-ttu-id="efdae-158">TeamsTab.Delete.Chat</span><span class="sxs-lookup"><span data-stu-id="efdae-158">TeamsTab.Delete.Chat</span></span>           | <span data-ttu-id="efdae-159">删除此聊天的选项卡。</span><span class="sxs-lookup"><span data-stu-id="efdae-159">Delete this chat's tabs.</span></span>                                      |
| <span data-ttu-id="efdae-160">TeamsTab.ReadWrite.Chat</span><span class="sxs-lookup"><span data-stu-id="efdae-160">TeamsTab.ReadWrite.Chat</span></span>        | <span data-ttu-id="efdae-161">管理此聊天的选项卡。</span><span class="sxs-lookup"><span data-stu-id="efdae-161">Manage this chat's tabs.</span></span>                                      |
| <span data-ttu-id="efdae-162">TeamsAppInstallation.Read.Chat</span><span class="sxs-lookup"><span data-stu-id="efdae-162">TeamsAppInstallation.Read.Chat</span></span> | <span data-ttu-id="efdae-163">获取此聊天中安装的应用。</span><span class="sxs-lookup"><span data-stu-id="efdae-163">Get which apps are installed in this chat.</span></span>                   |
| <span data-ttu-id="efdae-164">OnlineMeeting.ReadBasic.Chat</span><span class="sxs-lookup"><span data-stu-id="efdae-164">OnlineMeeting.ReadBasic.Chat</span></span>   | <span data-ttu-id="efdae-165">获取与此聊天关联的会议的基本属性，如名称、日程安排、组织者和加入链接。</span><span class="sxs-lookup"><span data-stu-id="efdae-165">Get basic properties, such as name, schedule, organizer, and join link of a meeting associated with this chat.</span></span> |

<span data-ttu-id="efdae-166">有关详细信息，请参阅 [聊天资源特定的许可权限](/graph/permissions-reference#chat-resource-specific-consent-permissions)。</span><span class="sxs-lookup"><span data-stu-id="efdae-166">For more details, see [chat resource-specific consent permissions](/graph/permissions-reference#chat-resource-specific-consent-permissions).</span></span>

> [!NOTE]
> <span data-ttu-id="efdae-167">特定于资源的权限仅适用于安装在 Teams 客户端上的 Teams 应用，并且当前不是 Azure Active Directory (AAD) 的一部分。</span><span class="sxs-lookup"><span data-stu-id="efdae-167">Resource-specific permissions are only available to Teams apps installed on the Teams client and are currently not part of the Azure Active Directory (AAD) portal.</span></span>

## <a name="enable-rsc-in-your-application"></a><span data-ttu-id="efdae-168">在应用程序中启用 RSC</span><span class="sxs-lookup"><span data-stu-id="efdae-168">Enable RSC in your application</span></span>

1. <span data-ttu-id="efdae-169">[在 AAD 门户中配置同意设置](#configure-consent-settings-in-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="efdae-169">[Configure consent settings in the AAD portal](#configure-consent-settings-in-the-aad-portal).</span></span>
    1. <span data-ttu-id="efdae-170">[为团队中的 RSC 配置组所有者同意设置](#configure-group-owner-consent-settings-for-rsc-in-a-team)。</span><span class="sxs-lookup"><span data-stu-id="efdae-170">[Configure group owner consent settings for RSC in a team](#configure-group-owner-consent-settings-for-rsc-in-a-team).</span></span>
    1. <span data-ttu-id="efdae-171">[在聊天中为 RSC 配置用户同意设置](#configure-user-consent-settings-for-rsc-in-a-chat)。</span><span class="sxs-lookup"><span data-stu-id="efdae-171">[Configure user consent settings for RSC in a chat](#configure-user-consent-settings-for-rsc-in-a-chat).</span></span>
1. <span data-ttu-id="efdae-172">[使用 AAD Microsoft 标识平台注册你的应用](#register-your-app-with-microsoft-identity-platform-using-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="efdae-172">[Register your app with Microsoft identity platform using the AAD portal](#register-your-app-with-microsoft-identity-platform-using-the-aad-portal).</span></span>
1. <span data-ttu-id="efdae-173">[在 AAD 门户中查看应用程序权限](#review-your-application-permissions-in-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="efdae-173">[Review your application permissions in the AAD portal](#review-your-application-permissions-in-the-aad-portal).</span></span>
1. <span data-ttu-id="efdae-174">[从标识平台 获取访问令牌](#obtain-an-access-token-from-the-microsoft-identity-platform)。</span><span class="sxs-lookup"><span data-stu-id="efdae-174">[Obtain an access token from the identity platform](#obtain-an-access-token-from-the-microsoft-identity-platform).</span></span>
1. <span data-ttu-id="efdae-175">[更新应用Teams清单](#update-your-teams-app-manifest)。</span><span class="sxs-lookup"><span data-stu-id="efdae-175">[Update your Teams app manifest](#update-your-teams-app-manifest).</span></span>
1. <span data-ttu-id="efdae-176">[直接在 Teams 中安装应用](#sideload-your-app-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="efdae-176">[Install your app directly in Teams](#sideload-your-app-in-teams).</span></span>
1. <span data-ttu-id="efdae-177">[检查应用是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions)。</span><span class="sxs-lookup"><span data-stu-id="efdae-177">[Check your app for added RSC permissions](#check-your-app-for-added-rsc-permissions).</span></span>
    1. <span data-ttu-id="efdae-178">[检查你的应用在团队中是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions-in-a-team)。</span><span class="sxs-lookup"><span data-stu-id="efdae-178">[Check your app for added RSC permissions in a team](#check-your-app-for-added-rsc-permissions-in-a-team).</span></span>
    1. <span data-ttu-id="efdae-179">[检查你的应用在聊天中是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions-in-a-chat)。</span><span class="sxs-lookup"><span data-stu-id="efdae-179">[Check your app for added RSC permissions in a chat](#check-your-app-for-added-rsc-permissions-in-a-chat).</span></span>

## <a name="configure-consent-settings-in-the-aad-portal"></a><span data-ttu-id="efdae-180">在 AAD 门户中配置许可设置</span><span class="sxs-lookup"><span data-stu-id="efdae-180">Configure consent settings in the AAD portal</span></span>

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a><span data-ttu-id="efdae-181">为团队中的 RSC 配置组所有者同意设置</span><span class="sxs-lookup"><span data-stu-id="efdae-181">Configure group owner consent settings for RSC in a team</span></span>

<span data-ttu-id="efdae-182">可以直接在 Azure 门户 [中启用](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) 或禁用组所有者同意：</span><span class="sxs-lookup"><span data-stu-id="efdae-182">You can enable or disable [group owner consent](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) directly within the Azure portal:</span></span>

1. <span data-ttu-id="efdae-183">以全局管理员或公司管理员登录 [Azure](https://portal.azure.com) [门户](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="efdae-183">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator or Company Administrator](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).</span></span>
1. <span data-ttu-id="efdae-184">选择 **Azure Active Directory Enterprise**  >    >  **同意和权限**  >  [**用户同意设置"。**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)</span><span class="sxs-lookup"><span data-stu-id="efdae-184">Select **Azure Active Directory** > **Enterprise applications** > **Consent and permissions** > [**User consent settings**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings).</span></span>
1. <span data-ttu-id="efdae-185">使用标记为组所有者同意的控件启用、禁用或限制用户 **同意访问数据的应用**。</span><span class="sxs-lookup"><span data-stu-id="efdae-185">Enable, disable, or limit user consent with the control labeled **Group owner consent for apps accessing data**.</span></span> <span data-ttu-id="efdae-186">默认值为 **允许所有组所有者获得组所有者同意**。</span><span class="sxs-lookup"><span data-stu-id="efdae-186">The default is **Allow group owner consent for all group owners**.</span></span> <span data-ttu-id="efdae-187">对于使用 RSC 安装应用的团队所有者，必须为该用户启用组所有者同意。</span><span class="sxs-lookup"><span data-stu-id="efdae-187">For a team owner to install an app using RSC, group owner consent must be enabled for that user.</span></span>

    ![Azure RSC 团队配置](../../assets/images/azure-rsc-team-configuration.png)

<span data-ttu-id="efdae-189">此外，您可以使用 PowerShell 启用或禁用组所有者同意，按照使用 PowerShell 配置组所有者同意中概述 [的步骤操作](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="efdae-189">In addition, you can enable or disable group owner consent using PowerShell, follow the steps outlined in [configure group owner consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell).</span></span>

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a><span data-ttu-id="efdae-190">在聊天中为 RSC 配置用户同意设置</span><span class="sxs-lookup"><span data-stu-id="efdae-190">Configure user consent settings for RSC in a chat</span></span>

<span data-ttu-id="efdae-191">可以直接在 Azure 门户 [中启用](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) 或禁用用户同意：</span><span class="sxs-lookup"><span data-stu-id="efdae-191">You can enable or disable [user consent](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) directly within the Azure portal:</span></span>

1. <span data-ttu-id="efdae-192">以全局管理员或公司管理员登录 [Azure](https://portal.azure.com) [门户](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="efdae-192">Sign in to the [Azure portal](https://portal.azure.com) as a [Global Administrator or Company Administrator](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true).</span></span>
1. <span data-ttu-id="efdae-193">选择 **Azure Active Directory Enterprise**  >    >  **同意和权限**  >  [**用户同意设置"。**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)</span><span class="sxs-lookup"><span data-stu-id="efdae-193">Select **Azure Active Directory** > **Enterprise applications** > **Consent and permissions** > [**User consent settings**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings).</span></span>
1. <span data-ttu-id="efdae-194">使用标记为"应用程序的用户同意"的控件启用 **、禁用或限制用户同意**。</span><span class="sxs-lookup"><span data-stu-id="efdae-194">Enable, disable, or limit user consent with the control labeled **User consent for applications**.</span></span> <span data-ttu-id="efdae-195">默认值为 **"允许用户同意应用"。**</span><span class="sxs-lookup"><span data-stu-id="efdae-195">The default is **Allow user consent for apps**.</span></span> <span data-ttu-id="efdae-196">若要聊天成员使用 RSC 安装应用，必须为该用户启用用户同意。</span><span class="sxs-lookup"><span data-stu-id="efdae-196">For a chat member to install an app using RSC, user consent must be enabled for that user.</span></span>

    ![Azure RSC 聊天配置](../../assets/images/azure-rsc-chat-configuration.png)

<span data-ttu-id="efdae-198">此外，您可以使用 PowerShell 启用或禁用用户同意，按照使用 PowerShell 配置用户同意中 [概述的步骤操作](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell)。</span><span class="sxs-lookup"><span data-stu-id="efdae-198">In addition, you can enable or disable user consent using PowerShell, follow the steps outlined in [configure user consent using PowerShell](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell).</span></span>

## <a name="register-your-app-with-microsoft-identity-platform-using-the-aad-portal"></a><span data-ttu-id="efdae-199">使用 AAD Microsoft 标识平台注册应用</span><span class="sxs-lookup"><span data-stu-id="efdae-199">Register your app with Microsoft identity platform using the AAD portal</span></span>

<span data-ttu-id="efdae-200">AAD 门户提供了一个中央平台，用于注册和配置应用。</span><span class="sxs-lookup"><span data-stu-id="efdae-200">The AAD portal provides a central platform for you to register and configure your apps.</span></span> <span data-ttu-id="efdae-201">你的应用必须在 AAD 门户中注册才能与标识平台集成，并调用 Microsoft Graph API。</span><span class="sxs-lookup"><span data-stu-id="efdae-201">Your app must be registered in the AAD portal to integrate with the identity platform and call Microsoft Graph APIs.</span></span> <span data-ttu-id="efdae-202">有关详细信息，请参阅 [向标识平台注册应用程序](/graph/auth-register-app-v2)。</span><span class="sxs-lookup"><span data-stu-id="efdae-202">For more information, see [register an application with the identity platform](/graph/auth-register-app-v2).</span></span>

> [!WARNING]
> <span data-ttu-id="efdae-203">AAD 应用 ID 不能跨多个应用Teams共享。</span><span class="sxs-lookup"><span data-stu-id="efdae-203">An AAD app ID must not be shared across multiple Teams apps.</span></span> <span data-ttu-id="efdae-204">在一个应用和一个 AAD 应用Teams一对一映射。</span><span class="sxs-lookup"><span data-stu-id="efdae-204">There must be a 1:1 mapping between a Teams app and an AAD app.</span></span> <span data-ttu-id="efdae-205">尝试安装多个与Teams AAD 应用 ID 关联的应用将导致安装或运行时失败。</span><span class="sxs-lookup"><span data-stu-id="efdae-205">Attempts to install multiple Teams apps which are associated with the same AAD app ID will cause installation or runtime failures.</span></span>

## <a name="review-your-application-permissions-in-the-aad-portal"></a><span data-ttu-id="efdae-206">在 AAD 门户中查看应用程序权限</span><span class="sxs-lookup"><span data-stu-id="efdae-206">Review your application permissions in the AAD portal</span></span>

1. <span data-ttu-id="efdae-207">转到"**主页**  >  **应用注册"** 页并选择 RSC 应用。</span><span class="sxs-lookup"><span data-stu-id="efdae-207">Go to the **Home** > **App registrations** page and select your RSC app.</span></span>
1. <span data-ttu-id="efdae-208">从 **左窗格中选择"API** 权限"，然后浏览应用的 **"已配置权限"** 列表。</span><span class="sxs-lookup"><span data-stu-id="efdae-208">Choose **API permissions** from the left pane and go through the list of **Configured permissions** for your app.</span></span> <span data-ttu-id="efdae-209">如果你的应用仅进行 RSC Graph API 调用，请删除该页面上的所有权限。</span><span class="sxs-lookup"><span data-stu-id="efdae-209">If your app only makes RSC Graph API calls, delete all the permissions on that page.</span></span> <span data-ttu-id="efdae-210">如果你的应用还进行非 RSC 调用，请保留所需的权限。</span><span class="sxs-lookup"><span data-stu-id="efdae-210">If your app also makes non-RSC calls, keep those permissions as required.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efdae-211">AAD 门户不能用于请求 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="efdae-211">The AAD portal cannot be used to request RSC permissions.</span></span> <span data-ttu-id="efdae-212">RSC 权限当前专用于 Teams 客户端中安装的 Teams 应用程序，这些权限在 Teams 应用程序清单 (JSON) 文件中声明。</span><span class="sxs-lookup"><span data-stu-id="efdae-212">RSC permissions are currently exclusive to Teams applications installed in the Teams client and are declared in the Teams app manifest (JSON) file.</span></span>

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a><span data-ttu-id="efdae-213">从应用程序获取访问Microsoft 标识平台</span><span class="sxs-lookup"><span data-stu-id="efdae-213">Obtain an access token from the Microsoft identity platform</span></span>

<span data-ttu-id="efdae-214">若要Graph API 调用，必须从标识平台获取应用的访问令牌。</span><span class="sxs-lookup"><span data-stu-id="efdae-214">To make Graph API calls, you must obtain an access token for your app from the identity platform.</span></span> <span data-ttu-id="efdae-215">应用必须先在 AAD 门户中注册，然后才能从标识平台获取令牌。</span><span class="sxs-lookup"><span data-stu-id="efdae-215">Before your app can get a token from the identity platform, it must be registered in the AAD portal.</span></span> <span data-ttu-id="efdae-216">访问令牌包含你的应用的相关信息，还有它就可通过 Microsoft Graph 访问的资源和 API 所具备的权限。</span><span class="sxs-lookup"><span data-stu-id="efdae-216">The access token contains information about your app and the permissions it has for the resources and APIs available through Microsoft Graph.</span></span>

<span data-ttu-id="efdae-217">您必须具有来自 AAD 注册过程的以下值，以从标识平台检索访问令牌：</span><span class="sxs-lookup"><span data-stu-id="efdae-217">You must have the following values from the AAD registration process to retrieve an access token from the identity platform:</span></span>

- <span data-ttu-id="efdae-218">应用注册门户分配的应用程序 **ID。**</span><span class="sxs-lookup"><span data-stu-id="efdae-218">The **Application ID** assigned by the app registration portal.</span></span> <span data-ttu-id="efdae-219">如果你的应用支持单一登录 (SSO) 你必须对应用和 SSO 使用相同的应用程序 ID。</span><span class="sxs-lookup"><span data-stu-id="efdae-219">If your app supports single sign-on (SSO) you must use the same Application ID for your app and SSO.</span></span>
- <span data-ttu-id="efdae-220">客户端 **密码/密码** 或公钥或私钥对，即 **证书**。</span><span class="sxs-lookup"><span data-stu-id="efdae-220">The **Client secret/password** or a public or private key pair that is **Certificate**.</span></span> <span data-ttu-id="efdae-221">这不是本机应用的必需项。</span><span class="sxs-lookup"><span data-stu-id="efdae-221">This is not required for native apps.</span></span>
- <span data-ttu-id="efdae-222">应用接收来自 AAD 的响应的重定向 **URI** 或回复 URL。</span><span class="sxs-lookup"><span data-stu-id="efdae-222">A **Redirect URI** or reply URL for your app to receive responses from AAD.</span></span>

<span data-ttu-id="efdae-223">有关详细信息，请参阅 [代表用户获取访问权限和](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) 在没有 [用户的情况下获取访问权限](/graph/auth-v2-service)。</span><span class="sxs-lookup"><span data-stu-id="efdae-223">For more information, see [get access on behalf of a user](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) and [get access without a user](/graph/auth-v2-service).</span></span>

## <a name="update-your-teams-app-manifest"></a><span data-ttu-id="efdae-224">更新Teams应用程序清单</span><span class="sxs-lookup"><span data-stu-id="efdae-224">Update your Teams app manifest</span></span>

<span data-ttu-id="efdae-225">RSC 权限在应用清单 JSON 文件中声明。</span><span class="sxs-lookup"><span data-stu-id="efdae-225">The RSC permissions are declared in your app manifest JSON file.</span></span> <span data-ttu-id="efdae-226">将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：</span><span class="sxs-lookup"><span data-stu-id="efdae-226">Add a [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) key to your app manifest with the following values:</span></span>

|<span data-ttu-id="efdae-227">名称</span><span class="sxs-lookup"><span data-stu-id="efdae-227">Name</span></span>| <span data-ttu-id="efdae-228">类型</span><span class="sxs-lookup"><span data-stu-id="efdae-228">Type</span></span> | <span data-ttu-id="efdae-229">说明</span><span class="sxs-lookup"><span data-stu-id="efdae-229">Description</span></span>|
|---|---|---|
|`id` |<span data-ttu-id="efdae-230">String</span><span class="sxs-lookup"><span data-stu-id="efdae-230">String</span></span> |<span data-ttu-id="efdae-231">AAD 应用 ID。</span><span class="sxs-lookup"><span data-stu-id="efdae-231">Your AAD app ID.</span></span> <span data-ttu-id="efdae-232">有关详细信息，请参阅在 [AAD 门户中注册应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal)。</span><span class="sxs-lookup"><span data-stu-id="efdae-232">For more information, see [register your app in the AAD portal](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal).</span></span>|
|`resource`|<span data-ttu-id="efdae-233">String</span><span class="sxs-lookup"><span data-stu-id="efdae-233">String</span></span>| <span data-ttu-id="efdae-234">此字段在 RSC 中没有任何操作，但必须添加该字段，并且必须具有值以避免错误响应;任何字符串将执行。</span><span class="sxs-lookup"><span data-stu-id="efdae-234">This field has no operation in RSC, but must be added and have a value to avoid an error response; any string will do.</span></span>|
|`applicationPermissions`|<span data-ttu-id="efdae-235">字符串数组</span><span class="sxs-lookup"><span data-stu-id="efdae-235">Array of strings</span></span>|<span data-ttu-id="efdae-236">应用的 RSC 权限。</span><span class="sxs-lookup"><span data-stu-id="efdae-236">RSC permissions for  your app.</span></span> <span data-ttu-id="efdae-237">有关详细信息，请参阅特定于 [资源的权限](resource-specific-consent.md#resource-specific-permissions)。</span><span class="sxs-lookup"><span data-stu-id="efdae-237">For more information, see [resource-specific permissions](resource-specific-consent.md#resource-specific-permissions).</span></span>|

>
> [!IMPORTANT]
> <span data-ttu-id="efdae-238">非 RSC 权限存储在 Azure 门户中。</span><span class="sxs-lookup"><span data-stu-id="efdae-238">Non-RSC permissions are stored in the Azure portal.</span></span> <span data-ttu-id="efdae-239">不要将它们添加到应用清单。</span><span class="sxs-lookup"><span data-stu-id="efdae-239">Do not add them to the app manifest.</span></span>
>

### <a name="example-for-rsc-in-a-team"></a><span data-ttu-id="efdae-240">团队中的 RSC 示例</span><span class="sxs-lookup"><span data-stu-id="efdae-240">Example for RSC in a team</span></span>

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

### <a name="example-for-rsc-in-a-chat"></a><span data-ttu-id="efdae-241">聊天中的 RSC 示例</span><span class="sxs-lookup"><span data-stu-id="efdae-241">Example for RSC in a chat</span></span>

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

> [!NOTE]
> <span data-ttu-id="efdae-242">如果应用旨在支持在团队和聊天范围内安装，可以在 下的同一清单中指定团队和聊天权限 `applicationPermissions` 。</span><span class="sxs-lookup"><span data-stu-id="efdae-242">If the app is meant to support installation in both team and chat scopes, then both team and chat permissions can be specified in the same manifest under `applicationPermissions`.</span></span>

## <a name="sideload-your-app-in-teams"></a><span data-ttu-id="efdae-243">在应用程序中旁加载Teams</span><span class="sxs-lookup"><span data-stu-id="efdae-243">Sideload your app in Teams</span></span>

<span data-ttu-id="efdae-244">如果你的Teams管理员允许自定义应用上传，你可以将应用直接旁加载[](~/concepts/deploy-and-publish/apps-upload.md)到特定团队或聊天。</span><span class="sxs-lookup"><span data-stu-id="efdae-244">If your Teams admin allows custom app uploads, you can [sideload your app](~/concepts/deploy-and-publish/apps-upload.md) directly to a specific team or chat.</span></span>

## <a name="check-your-app-for-added-rsc-permissions"></a><span data-ttu-id="efdae-245">检查应用是否添加了 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="efdae-245">Check your app for added RSC permissions</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efdae-246">RSC 权限不归为用户。</span><span class="sxs-lookup"><span data-stu-id="efdae-246">The RSC permissions are not attributed to a user.</span></span> <span data-ttu-id="efdae-247">调用使用应用程序权限而不是用户委派权限进行。</span><span class="sxs-lookup"><span data-stu-id="efdae-247">Calls are made with app permissions, not user delegated permissions.</span></span> <span data-ttu-id="efdae-248">可以允许应用执行用户无法执行的操作，例如删除选项卡。必须先查看团队所有者或聊天所有者的意图，然后才能进行 RSC API 调用。</span><span class="sxs-lookup"><span data-stu-id="efdae-248">The app can be allowed to perform actions that the user cannot, such as deleting a tab. You must review the team owner's or chat owner's intent for your use before making RSC API calls.</span></span> <span data-ttu-id="efdae-249">有关详细信息，请参阅 Microsoft Teams [API 概述](/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="efdae-249">For more information, see [Microsoft Teams API overview](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="efdae-250">将应用安装到资源后，可以使用 Graph[资源管理器](https://developer.microsoft.com/graph/graph-explorer)查看已授予资源中应用程序的权限。</span><span class="sxs-lookup"><span data-stu-id="efdae-250">After the app has been installed to a resource, you can use [Graph Explorer](https://developer.microsoft.com/graph/graph-explorer) to view the permissions that have been granted to the app in the resource.</span></span>

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a><span data-ttu-id="efdae-251">检查你的应用在团队中是否添加了 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="efdae-251">Check your app for added RSC permissions in a team</span></span>

1. <span data-ttu-id="efdae-252">从组获取 **团队的 groupId** Teams。</span><span class="sxs-lookup"><span data-stu-id="efdae-252">Get the team's **groupId** from Teams.</span></span>
1. <span data-ttu-id="efdae-253">In Teams， select **Teams** from the leftmost pane.</span><span class="sxs-lookup"><span data-stu-id="efdae-253">In Teams, select **Teams** from the leftmost pane.</span></span>
1. <span data-ttu-id="efdae-254">选择要安装应用的团队。</span><span class="sxs-lookup"><span data-stu-id="efdae-254">Select the team where the app is to be installed.</span></span>
1. <span data-ttu-id="efdae-255">选择该团队 &#x25CF;&#x25CF;&#x25CF; 省略号。</span><span class="sxs-lookup"><span data-stu-id="efdae-255">Select the ellipses &#x25CF;&#x25CF;&#x25CF; for that team.</span></span>
1. <span data-ttu-id="efdae-256">从 **团队下拉菜单中选择** 获取团队链接。</span><span class="sxs-lookup"><span data-stu-id="efdae-256">Select **Get link to team** from the team drop-down menu.</span></span>
1. <span data-ttu-id="efdae-257">复制并保存"获取团队链接"弹出对话框中的 **groupId** 值。</span><span class="sxs-lookup"><span data-stu-id="efdae-257">Copy and save the **groupId** value from the **Get a link to the team** pop-up dialog box.</span></span>
1. <span data-ttu-id="efdae-258">登录到 Graph **资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="efdae-258">Sign in to **Graph Explorer**.</span></span>
1. <span data-ttu-id="efdae-259">对此终结点 **进行 GET** 调用 `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants` ：。</span><span class="sxs-lookup"><span data-stu-id="efdae-259">Make a **GET** call to this endpoint: `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants`.</span></span> <span data-ttu-id="efdae-260">响应 `clientAppId` 中的字段将映射到应用程序清单 `webApplicationInfo.id` Teams中指定的。</span><span class="sxs-lookup"><span data-stu-id="efdae-260">The `clientAppId` field in the response will map to the `webApplicationInfo.id` specified in the Teams app manifest.</span></span>

    ![Graph对团队 RSC 权限的 GET 调用的浏览器响应](../../assets/images/team-graph-permissions.png)

<span data-ttu-id="efdae-262">若要详细了解如何获取特定团队中安装的应用的详细信息，请参阅获取指定团队中安装的应用 [的名称和其他详细信息](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)。</span><span class="sxs-lookup"><span data-stu-id="efdae-262">For more information on how to get details of the apps installed in a specific team, see [get the names and other details of apps installed in the specified team](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps).</span></span>

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a><span data-ttu-id="efdae-263">检查你的应用在聊天中是否添加了 RSC 权限</span><span class="sxs-lookup"><span data-stu-id="efdae-263">Check your app for added RSC permissions in a chat</span></span>

1. <span data-ttu-id="efdae-264">从 Web 客户端获取Teams *ID。*</span><span class="sxs-lookup"><span data-stu-id="efdae-264">Get the chat thread ID from the Teams *web* client.</span></span>
1. <span data-ttu-id="efdae-265">在 Teams 客户端中 **，从最** 左侧的窗格中选择"聊天"。</span><span class="sxs-lookup"><span data-stu-id="efdae-265">In the Teams web client, select **Chat** from the leftmost pane.</span></span>
1. <span data-ttu-id="efdae-266">从下拉菜单中选择应用安装位置的聊天。</span><span class="sxs-lookup"><span data-stu-id="efdae-266">Select the chat where the app is installed from the drop-down menu.</span></span>
1. <span data-ttu-id="efdae-267">复制 Web URL，然后从字符串中保存聊天线程 ID。</span><span class="sxs-lookup"><span data-stu-id="efdae-267">Copy the web URL and save the chat thread ID from the string.</span></span>

    ![来自 Web URL 的聊天线程 ID](../../assets/images/chat-thread-id.png)

1. <span data-ttu-id="efdae-269">登录到 Graph **资源管理器**。</span><span class="sxs-lookup"><span data-stu-id="efdae-269">Sign in to **Graph Explorer**.</span></span>
1. <span data-ttu-id="efdae-270">对以下 **终结点** 进行 GET 调用 `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants` ：。</span><span class="sxs-lookup"><span data-stu-id="efdae-270">Make a **GET** call to the following endpoint: `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants`.</span></span> <span data-ttu-id="efdae-271">响应 `clientAppId` 中的字段将映射到应用程序清单 `webApplicationInfo.id` Teams中指定的。</span><span class="sxs-lookup"><span data-stu-id="efdae-271">The `clientAppId` field in the response will map to the `webApplicationInfo.id` specified in the Teams app manifest.</span></span>

    ![Graph对聊天 RSC 权限的 GET 调用的浏览器响应](../../assets/images/chat-graph-permissions.png)

<span data-ttu-id="efdae-273">若要详细了解如何获取特定聊天中安装的应用的详细信息，请参阅获取指定聊天中安装的应用 [的名称和其他详细信息](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)。</span><span class="sxs-lookup"><span data-stu-id="efdae-273">For more information on how to get details of apps installed in a specific chat, see [get the names and other details of apps installed in the specified chat](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat).</span></span>

## <a name="code-sample"></a><span data-ttu-id="efdae-274">代码示例</span><span class="sxs-lookup"><span data-stu-id="efdae-274">Code sample</span></span>

| <span data-ttu-id="efdae-275">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="efdae-275">**Sample name**</span></span> | <span data-ttu-id="efdae-276">**说明**</span><span class="sxs-lookup"><span data-stu-id="efdae-276">**Description**</span></span> | <span data-ttu-id="efdae-277">**.NET**</span><span class="sxs-lookup"><span data-stu-id="efdae-277">**.NET**</span></span> |<span data-ttu-id="efdae-278">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="efdae-278">**Node.js**</span></span> |
|-----------------|-----------------|----------------|----------------|
| <span data-ttu-id="efdae-279">Resource-Specific RSC (同意) </span><span class="sxs-lookup"><span data-stu-id="efdae-279">Resource-Specific Consent (RSC)</span></span> | <span data-ttu-id="efdae-280">使用 RSC 调用Graph API。</span><span class="sxs-lookup"><span data-stu-id="efdae-280">Use RSC to call Graph APIs.</span></span> | [<span data-ttu-id="efdae-281">View</span><span class="sxs-lookup"><span data-stu-id="efdae-281">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[<span data-ttu-id="efdae-282">View</span><span class="sxs-lookup"><span data-stu-id="efdae-282">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|

## <a name="see-also"></a><span data-ttu-id="efdae-283">另请参阅</span><span class="sxs-lookup"><span data-stu-id="efdae-283">See also</span></span>
 
* [<span data-ttu-id="efdae-284">在应用程序内测试特定于资源的许可Teams</span><span class="sxs-lookup"><span data-stu-id="efdae-284">Test resource-specific consent permissions in Teams</span></span>](test-resource-specific-consent.md)
* [<span data-ttu-id="efdae-285">管理员许可中Microsoft Teams特定资源的同意</span><span class="sxs-lookup"><span data-stu-id="efdae-285">Resource-specific consent in Microsoft Teams for admins</span></span>](/MicrosoftTeams/resource-specific-consent)
