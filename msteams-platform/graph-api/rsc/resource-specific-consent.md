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
# <a name="resource-specific-consent-rsc"></a>RSC (资源特定的) 

RSC (特定于资源的) 是 Microsoft Teams 和 Microsoft Graph API 集成，使你的应用可以使用 API 终结点来管理组织内的特定团队。 使用 RSC (权限) 特定于资源的同意，团队所有者可以授予应用程序访问和/或修改团队数据的许可。 特定于 Teams 的精细 RSC 权限定义应用程序可以在特定团队中执行哪些操作：

## <a name="resource-specific-permissions"></a>特定于资源的权限

|应用权限| 操作 |
| ----- | ----- |
|TeamSettings.Read.Group | 获取此团队的设置。|
|TeamSettings.ReadWrite.Group|更新此团队的设置。|
|ChannelSettings.Read.Group|获取此团队的频道名称、频道说明和频道设置。|
|ChannelSettings.ReadWrite.Group|更新此团队的频道名称、频道说明和频道设置。|
|Channel.Create.Group|在这个团队中创建频道。|
|Channel.Delete.Group|删除此团队中的频道。|
|ChannelMessage.Read.Group |获取此团队的频道消息。|
|TeamsAppInstallation.Read.Group|获取此团队已安装应用的列表。|
|TeamsTab.Read.Group|获取此团队的选项卡列表。|
|TeamsTab.Create.Group|在此团队中创建选项卡。|
|TeamsTab.ReadWrite.Group|更新此团队的选项卡。|
|TeamsTab.Delete.Group|删除此团队的选项卡。|
|TeamMember.Read.Group|获取此团队的成员。|

>[!NOTE]
>特定于资源的权限仅适用于安装在 Teams 客户端上的 Teams 应用，并且当前不是 Azure Active Directory 门户的一部分。

## <a name="enable-resource-specific-consent-in-your-application"></a>在应用程序中启用特定于资源的同意

在应用程序中启用 RSC 的步骤如下所示：

1. [在 Azure Active Directory 门户](#configure-group-owner-consent-settings-in-the-azure-ad-portal)中配置组所有者同意设置。
1. [通过 Azure AD 门户向 Microsoft 标识平台注册应用](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
1. [查看 Azure AD 门户中的应用程序权限](#review-your-application-permissions-in-the-azure-ad-portal)。
1. [从 Microsoft Identity 平台获取访问令牌](#obtain-an-access-token-from-the-microsoft-identity-platform)。
1. [更新 Teams 应用清单](#update-your-teams-app-manifest)。
1. [直接在 Teams 中安装应用](#install-your-app-directly-in-teams)。
1. [检查应用是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions)。

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>在 Azure AD 门户中配置组所有者同意设置

可以直接在 Azure 门户 [中启用](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) 或禁用组所有者同意：

> [!div class="checklist"]
>
>- 以全局管理员/公司管理员登录 [Azure](https://portal.azure.com) [门户](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)。  
 > - [选择](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)**"Azure Active Directory**  =>  **企业**  =>  **应用程序许可和权限**  =>  **用户同意设置"。**
> - 使用标记为组所有者同意的控件启用、禁用或限制用户同意访问数据 (默认值为允许组所有者同意所有组所有者) 。  对于使用 RSC 安装应用的团队所有者，必须为该用户启用组所有者同意。

![azure rsc 配置](../../assets/images/azure-rsc-configuration.png)

若要使用 PowerShell 启用或禁用组所有者同意，请按照使用 PowerShell 配置组所有者 [同意中概述的步骤操作](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>通过 Azure AD 门户向 Microsoft 标识平台注册应用

Azure Active Directory 门户提供了一个中央平台，用于注册和配置应用。 应用必须在 Azure AD 门户中注册，才能与 Microsoft 标识平台集成并调用 Microsoft Graph API。 *请参阅*[向 Microsoft 标识平台注册应用程序](/graph/auth-register-app-v2)。

>[!WARNING]
>不要向同一 Azure AD 应用 ID 注册多个 Teams 应用。应用 ID 对于每个应用必须是唯一的。 尝试将多个应用安装到同一应用 ID 将失败。

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>在 Azure AD 门户中查看应用程序权限

导航到 **"主页**  =>  **应用注册"** 页并选择 RSC 应用。 从 **左侧导航** 栏中选择 API 权限，并检查应用的已配置权限列表。 如果你的应用将仅进行 RSC Graph API 调用，请删除该页面上的所有权限。 如果你的应用还将进行非 RSC 调用，请根据需要保留这些权限。

>[!IMPORTANT]
>Azure AD 门户不能用于请求 RSC 权限。 RSC 权限当前专用于 Teams 客户端中安装的 (Teams 应用程序，并且使用 JSON) 文件在应用清单中声明。

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>从 Microsoft 标识平台获取访问令牌

若要进行 Graph API 调用，你必须从标识平台获取应用的访问令牌。 应用必须先在 Azure AD 门户中注册，然后才能从 Microsoft 标识平台获取令牌。 访问令牌包含你的应用的相关信息，还有它就可通过 Microsoft Graph 访问的资源和 API 所具备的权限。

你需要从 Azure AD 注册过程获取以下值，以从标识平台检索访问令牌：

- 应用注册门户分配的应用程序 **ID。** 如果你的应用支持单一登录 (SSO) 应用和 SSO 应使用相同的应用程序 ID。
- 客户端 **密码/密码** 或公钥/私钥对 (**证书) 。** 这不是本机应用的必需项。
- 重定向 **URI** (或回复 URL) 应用接收来自 Azure AD 的响应。

 *请参阅*[代表用户获取访问权限和](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true)[在没有用户的情况下获取访问权限](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>更新 Teams 应用清单

RSC 权限在应用清单 (JSON) 文件中声明。  将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：

> [!div class="checklist"]
>
> - **id**  — Azure AD 应用 ID。 *请参阅* 在 [Azure AD 门户中注册应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
> - **resource**  — 任何字符串。 此字段在 RSC 中没有任何操作，但必须添加该字段，并且必须具有值以避免错误响应;任何字符串将执行。
> - **应用程序权限** — 应用的 RSC 权限。 *请参阅*[特定于资源的权限](resource-specific-consent.md#resource-specific-permissions)。

>
>[!IMPORTANT]
> 非 RSC 权限存储在 Azure 门户中。 不要将它们添加到应用清单。
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

## <a name="install-your-app-directly-in-teams"></a>直接在 Teams 中安装应用

创建应用后，你可以 [将应用包直接](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) 上载到特定团队。  为此，必须将 **上载自定义应用** 策略设置作为自定义应用设置策略的一部分启用。 *请参阅*[自定义应用策略设置](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)。

## <a name="check-your-app-for-added-rsc-permissions"></a>检查应用是否添加了 RSC 权限

>[!IMPORTANT]
>RSC 权限不归为用户。 调用使用应用程序权限而不是用户委派权限进行。 因此，可以允许应用执行用户无法执行的操作，例如创建频道或删除选项卡。在调用 RSC API 之前，应查看团队所有者对用例的意图。 *请参阅* [Microsoft Teams API 概述](/graph/teams-concept-overview)。

将应用安装到团队后，可以使用 [Graph 浏览器](https://developer.microsoft.com/graph/graph-explorer)  查看已授予团队中应用的权限：

> [!div class="checklist"]
>
>- 从 Teams 客户端获取团队的 **groupId。**
> - 在 Teams 客户端中 **，从** 最左侧导航栏中选择 Teams。
> - 从下拉菜单中选择安装应用的团队。
> - 选择" **更多选项"** 图标 (&#8943;) 。
> - 选择 **获取团队链接**。
> - 复制并保存字符串中的 **groupId** 值。
> - 登录到 **Graph 浏览器**。
> - 对以下 **终结点** 进行 GET 调用 `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` ：。 响应中的 clientAppId 字段将映射到 Teams 应用清单中指定的 appId。
  ![GRAPH 浏览器对 GET 调用的响应。](../../assets/images/graph-permissions.png)

## <a name="code-sample"></a>代码示例
| **示例名称** | **Description** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| RSC (资源特定)  | 使用 RSC 调用 Graph API。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|



## <a name="test-resource-specific-consent"></a>测试特定于资源的同意
 
> [!div class="nextstepaction"]
> [**在 Teams 中测试特定于资源的同意权限**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>Teams 管理员相关主题

> [!div class="nextstepaction"]
> [**Microsoft Teams 中针对管理员的资源特定许可**](/MicrosoftTeams/resource-specific-consent)
> 

