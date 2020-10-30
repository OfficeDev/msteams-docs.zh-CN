---
title: 团队中的特定于资源的同意
description: 介绍了团队中特定于资源的同意以及如何利用它。
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: Overview
keywords: 团队授权 OAuth SSO AAD rsc Graph
ms.openlocfilehash: e7a59497b77b303b6ef06582828f7c5cb36dbb58
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796189"
---
# <a name="resource-specific-consent-rsc"></a>特定于资源的同意 (RSC) 

>[!IMPORTANT]
> 这些 Api 在终结点中是可访问的 https://graph.microsoft.com/beta 。  [Beta 版本](/graph/versioning-and-support#beta-version)终结点包含当前处于预览阶段且尚不可用的 api。 Beta endpoint 中的 Api 可能会发生更改，我们建议您不要在生产应用程序中使用它们。 

特定于资源的同意 (RSC) 是 Microsoft 团队和图形 API 集成，使您的应用程序能够使用 API 终结点来管理组织中的特定团队。 特定于资源的同意 (RSC) 权限模型使 *团队所有者* 能够授予应用程序访问和/或修改团队数据的同意。 具体的团队特定的 RSC 权限定义了应用程序可在特定团队中执行的操作：

## <a name="resource-specific-permissions"></a>特定于资源的权限

|应用权限| 操作 |
| ----- | ----- |
|TeamSettings.Read.Group | 获取此团队的设置。|
|TeamSettings 的组|更新此团队的设置。|
|ChannelSettings.Read.Group|获取此团队的频道名称、频道说明和频道设置。|
|ChannelSettings 的组|更新此团队的频道名称、频道说明和频道设置。|
|Channel.Create.Group|在这个团队中创建频道。|
|Channel.Delete.Group|删除此团队中的频道。|
|ChannelMessage.Read.Group |获取此团队的频道消息。|
|TeamsAppInstallation。 Group|获取此团队安装的应用程序的列表。|
|TeamsTab.Read.Group|获取此团队的选项卡列表。|
|TeamsTab.Create.Group|在此团队中创建选项卡。|
|TeamsTab 的组|更新此团队的选项卡。|
|TeamsTab.Delete.Group|删除此团队的选项卡。|
|TeamMember。 Group|获取此团队的成员。|

>[!NOTE]
>特定于资源的权限仅对在团队客户端上安装的团队应用程序可用，并且当前不是 Azure Active Directory 门户的一部分。

## <a name="enable-resource-specific-consent-in-your-application"></a>在应用程序中启用特定于资源的同意

在应用程序中启用 RSC 的步骤如下所示：

1. [在 Azure Active Directory 门户中配置组所有者同意设置](#configure-group-owner-consent-settings-in-the-azure-ad-portal)。
1. [通过 AZURE AD 门户将您的应用程序注册到 Microsoft identity platform](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
1. [在 Azure AD 门户中查看你的应用程序权限](#review-your-application-permissions-in-the-azure-ad-portal)
1. [从 Microsoft Identity Platform 获取访问令牌](#obtain-an-access-token-from-the-microsoft-identity-platform)。
1. [更新团队应用程序清单](#update-your-teams-app-manifest)。
1. [直接在团队中安装您的应用程序](#install-your-app-directly-in-teams)。
1. [检查您的应用程序是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions)。

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>在 Azure AD 门户中配置组所有者同意设置

您可以在 Azure 门户中直接启用或禁用 [组所有者同意](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) ：

> [!div class="checklist"]
>
>- 以[全局管理员/公司管理员身份](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)登录到[Azure 门户](https://portal.azure.com)。  
 > - [选择](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)" **Azure Active Directory**  =>  **企业应用程序**  =>  **同意和权限** "  =>  **用户同意设置** 。
> - 启用、禁用或将用户同意限制为对 **访问数据的应用程序进行 "组所有者同意** " (默认为 " **允许所有组所有者的组所有者同意** ") 。 若要让团队所有者使用 RSC 安装应用程序，必须为该用户启用组所有者许可。

![azure rsc 配置](../../assets/images/azure-rsc-configuration.png)

若要在 Azure 门户中使用 PowerShell 启用或禁用组所有者同意，请按照 [使用 Powershell 配置组所有者许可](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell)中所述的步骤操作。

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>通过 Azure AD 门户将您的应用程序注册到 Microsoft identity platform

Azure Active Directory 门户为您提供了一个用于注册和配置应用程序的中央平台。 您的应用程序必须在 Azure AD 门户中注册，才能与 Microsoft identity platform 和调用 Graph Api 集成。 *请参阅*[在 Microsoft identity platform 中注册应用程序](/graph/auth-register-app-v2)。

>[!WARNING]
>不要将多个团队应用注册到同一个 Azure AD 应用 id。应用程序 id 对于每个应用程序必须是唯一的。 尝试将多个应用程序安装到相同的应用 id 将会失败。

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>在 Azure AD 门户中查看你的应用程序权限

导航到 " **家庭**  =>  **应用注册** " 页，并选择您的 RSC 应用程序。 从左侧导航栏中选择 " **API 权限** "，然后检查您的应用程序的已配置权限列表。 如果您的应用程序将仅进行 RSC Graph 呼叫，则删除该页面上的所有权限。 如果你的应用程序还将进行非 RSC 呼叫，请根据需要保留这些权限。

>[!IMPORTANT]
>Azure AD 门户不能用于请求 RSC 权限。 RSC 权限当前对于安装在团队客户端中的团队应用程序是独占的，在应用程序清单 (JSON) 文件中声明。

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>从 Microsoft identity platform 获取访问令牌

若要进行 Graph API 调用，必须从标识平台获取应用程序的访问令牌。 在您的应用程序可以从 Microsoft identity platform 获取令牌之前，它必须在 Azure AD 门户中进行注册。 访问令牌包含你的应用的相关信息，还有它就可通过 Microsoft Graph 访问的资源和 API 所具备的权限。

您需要使用 Azure AD 注册过程中的以下值从标识平台检索访问令牌：

- 应用注册门户分配的 **应用程序 ID** 。 如果您的应用程序支持单一登录 (SSO) 则您的应用程序和 SSO 应使用相同的应用程序 ID。
- **客户端密钥/密码** 或公钥/私钥对)  ( **证书** 。 这不是本机应用的必需项。
- **重定向 URI** (或用于从 Azure AD 接收响应的应用程序) 回复 URL。

 *请参阅*[代表用户获取访问权限](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token)并在 [没有用户的情况下获取访问权限](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>更新团队应用程序清单

RSC 权限是在应用程序清单 (JSON) 文件中声明的。  使用以下值将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 项添加到应用程序清单中：

> [!div class="checklist"]
>
> - **id** -你的 azure ad 应用 Id。 *请参阅*[在 azure ad 门户中注册你的应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
> - **resource**  —任何字符串。 此字段在 RSC 中没有任何操作，但必须添加它并具有值以避免错误响应;任何字符串都将执行。
> - **应用程序权限** -您的应用程序的 RSC 权限。 *请参阅*[特定于资源的权限](resource-specific-consent.md#resource-specific-permissions)。

>
>[!IMPORTANT]
> 非 RSC 权限存储在 Azure 门户中。 请勿将其添加到应用程序清单。
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

## <a name="install-your-app-directly-in-teams"></a>直接在团队中安装您的应用程序

创建您的应用程序后，您可以将 [应用程序包直接上载](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) 到特定团队。  若要执行此操作，必须将 " **上载自定义应用** " 策略设置作为自定义应用程序安装策略的一部分启用。 *请参阅*[自定义应用策略设置](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)。

## <a name="check-your-app-for-added-rsc-permissions"></a>检查您的应用程序是否添加了 RSC 权限

>[!IMPORTANT]
>RSC 权限不是用户的属性。 调用通过应用权限而不是用户委派权限进行。 因此，可能允许应用程序执行用户无法执行的操作，例如创建频道或删除选项卡。在进行 RSC API 调用之前，应查看团队所有者对用例的意图。 *请参阅* [Microsoft 团队 API 概述](/graph/teams-concept-overview)。

将应用程序安装到团队后，可以使用 [Graph 浏览器](https://developer.microsoft.com/graph/graph-explorer)  查看已授予给团队中的应用程序的权限：

> [!div class="checklist"]
>
>- 从团队客户端获取团队的 **groupId** 。
> - 在团队客户端中，从最左侧的导航栏中选择 " **团队** "。
> - 从下拉菜单中选择应用程序安装到的团队。
> - 选择 " **更多选项** " 图标 ( # A0) 。
> - 选择 " **获取到团队的链接** "。
> - 复制并保存字符串中的 **groupId** 值。
> - 登录到 **Graph 浏览器** 。
> - 对以下终结点进行 **GET** 调用： `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` 。 响应中的 clientAppId 字段将映射到在团队应用程序清单中指定的 appId。
  ![Graph 资源管理器响应 GET call。](../../assets/images/graph-permissions.png)
 
## <a name="test-resource-specific-consent"></a>测试特定于资源的同意
 
> [!div class="nextstepaction"]
> [**在团队中测试特定于资源的同意权限**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>团队管理员的相关主题

> [!div class="nextstepaction"]
> [**Microsoft 团队中针对管理员的特定于资源的同意**](/MicrosoftTeams/resource-specific-consent)
> 
