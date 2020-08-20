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
# <a name="resource-specific-consent-rsc"></a>特定于资源的 RSC (同) 

>[!IMPORTANT]
> 这些 API 在终结点中 https://graph.microsoft.com/beta 可访问。  [beta 版本](/graph/versioning-and-support#beta-version)终结点包括当前处于预览版且未正式发布的 API。 beta 终结点中的 API 可能会发生更改，建议不要在生产应用中使用它们。 

特定于资源的 (RSC) Microsoft Teams 和 Graph API 集成，它使你的应用能够使用 API 终结点来管理组织内的特定团队。 根据资源的 (同意) 模型， *工作组所有者* 可同意应用程序访问和/或修改团队的数据。 精细的特定于 Teams 的 RSC 权限定义应用程序可在特定团队内执行的操作：

## <a name="resource-specific-permissions"></a>特定于资源的权限

|应用权限| 操作 |
| ----- | ----- |
|TeamSettings.Read.Group | 获取此团队的设置。|
|TeamSettings.Edit.Group|更新此团队的设置。|
|ChannelSettings.Read.Group|获取此团队的频道名称、渠道描述和频道设置。|
|ChannelSettings.ReadWrite.Group|更新此团队的频道名称、频道描述和频道设置。|
|Channel.Create.Group|在这个团队中创建频道。|
|Channel.Delete.Group|删除此团队中的频道。|
|ChannelMessage.Read.Group |获取此团队的频道消息。|
|TeamsApp.Read.Group|获取此团队已安装应用的列表。|
|TeamsTab.Read.Group|获取此团队的选项卡列表。|
|TeamsTab.Create.Group|在此团队中创建选项卡。|
|TeamsTab.ReadWrite.Group|更新此团队的选项卡。|
|TeamsTab.Delete.Group|删除此团队的选项卡。|
|Member.Read.Group|获取此团队的成员。|
|Owner.Read.Group|获取此团队的所有者。|

>[!NOTE]
>特定于资源的权限仅适用于安装在 Teams 客户端上的 Teams 应用，目前不属于 Azure Active Directory 门户。

## <a name="enable-resource-specific-consent-in-your-application"></a>在应用程序中启用特定于资源的许可

在应用程序中启用 RSC 的步骤如下：

1. [在 Azure Active Directory 门户中配置组所有者同意设置](#configure-group-owner-consent-settings-in-the-azure-ad-portal)。
1. [通过 Azure AD 门户将应用注册到 Microsoft 标识平台](#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
1. [在 Azure AD 门户中查看应用程序权限](#review-your-application-permissions-in-the-azure-ad-portal)
1. [从 Microsoft 标识平台获取访问令牌](#obtain-an-access-token-from-the-microsoft-identity-platform)。
1. [更新 Teams 应用清单](#update-your-teams-app-manifest)。
1. [直接在 Teams 中安装你的应用](#install-your-app-directly-in-teams)。
1. [检查应用，查看添加的 RSC 权限](#check-your-app-for-added-rsc-permissions)。

## <a name="configure-group-owner-consent-settings-in-the-azure-ad-portal"></a>在 Azure AD 门户中配置组所有者同意设置

你可以直接在  [Azure 门户中启用或禁用](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-to-apps-accessing-group-data) 组所有者许可：

> [!div class="checklist"]
>
>- 以全局管理员 [/](https://portal.azure.com) 公司管理员 [身份登录到 Azure 门户](/azure/active-directory/users-groups-roles/directory-assign-admin-roles.md#global-administrator--company-administrator)。  
 > - 选择 **"Azure Active Directory**  => **企业应用程序**  => **用户设置"。**
> - 启用、禁用或限制用户同意，并允许用户同意访问标签用户的 **控制者 (** 默认情况下启用此功能) 。

![azure rsc 配置](../../assets/images/azure-rsc-configuration.svg)

| 值 | 说明|
|--- | --- |
|是 | 为所有组所有者启用特定于组的许可。|
|否 |对所有用户禁用特定于组的许可。| 
|Limited | 为所选组的成员启用特定于组的许可。|

若要使用 PowerShell 在 Azure 门户内启用或禁用组所有者同意，请按照使用 [PowerShell 配置组所有者同意中概述的步骤操作](/azure/active-directory/manage-apps/configure-user-consent#configure-group-owner-consent-using-powershell)。

## <a name="register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal"></a>通过 Azure AD 门户向 Microsoft 标识平台注册应用

Azure Active Directory 门户提供了一个中心平台，可注册和配置应用。 必须在 Azure AD 门户中注册应用，才能与 Microsoft 标识平台集成并调用 Graph API。 *请参阅*[向 Microsoft 标识平台注册应用程序](/graph/auth-register-app-v2)。

>[!WARNING]
>请勿将多个 Teams 应用注册到同一个 Azure AD 应用 ID。应用 ID 对于每个应用都必须是唯一的。 尝试将多个应用安装到同一应用 ID 时失败。

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>在 Azure AD 门户中查看应用程序权限

导航到"**家庭**  =>  **应用注册"** 页面并选择 RSC 应用。 从 **左侧** 导航栏中选择 API 权限，并检查应用已配置权限的列表。 如果你的应用仅调用 RSC Graph，请删除该页面上的所有权限。 如果你的应用还将发出非 RSC 调用，请根据需要保留这些权限。

>[!IMPORTANT]
>Azure AD 门户无法用于请求 RSC 权限。 RSC 权限目前仅为安装在 Teams 客户端中的 Teams 应用程序) ，并在 JSON 格式文件的应用清单 (中声明。

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>从 Microsoft 标识平台获取访问令牌

若要进行 Graph API 调用，必须从标识平台为应用获取访问令牌。 必须在 Azure AD 门户中注册你的应用，然后它才能从 Microsoft 标识平台获取令牌。 访问令牌包含你的应用的相关信息，还有它就可通过 Microsoft Graph 访问的资源和 API 所具备的权限。

将需要从 Azure AD 注册进程中拥有以下值，从标识平台检索访问令牌：

- 应用注册门户分配的应用程序**ID。** 如果应用在 SSO 身份验证选项 (单) 则应该为应用和 SSO 使用相同的应用 ID。
- 客户端**密码/密码或公钥**/私钥对 (钥对 (**) 。** 这不是本机应用的必需项。
- 可以 **让 (** AZURE AD) 或回复 URL 链接或回复 URL 文件。

 *在*[没有用户的情况下代表用户查看](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token)[访问权限并获取访问权限](/graph/auth-v2-service)

## <a name="update-your-teams-app-manifest"></a>更新 Teams 应用部件清单 （manifest）

RSC 权限在 JSON 设备的应用程序清单或 (应用程序) 中。  使用以下 [值将 webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到应用部件清单：

> [!div class="checklist"]
>
> - **id** — 你的 Azure AD 应用 ID。*请参阅*["在 Azure AD 门户注册你的应用"。](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)
> - **资源**  — 任何字符串。 此字段在 RSC 中没有操作，但必须添加并具有值以避免响应;可对任何字符串执行操作。
> - **应用程序权限** — 您的应用程序的 RSC 权限。 *参*[见特定于资源的权限](resource-specific-consent.md#resource-specific-permissions)。

>
>[!IMPORTANT]
> 非 RSC 权限存储在 Azure 门户中。 不要将其添加到应用部件清单 （manifest）。
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

创建应用后，你可以将 [应用包直接](../../concepts/deploy-and-publish/apps-upload.md#upload-your-package-into-a-team-using-the-apps-tab) 上传到特定团队。  为此，必须在 **自定义应用程序设置策略** 中启用"上载自定义应用程序"策略设置。 *请参阅*[自定义应用策略设置](/microsoftteams/teams-custom-app-policies-and-settings#custom-app-policy-and-settings)。

## <a name="check-your-app-for-added-rsc-permissions"></a>检查你的应用的添加 RSC 权限

>[!IMPORTANT]
>RSC 权限不会分配给用户。 调用使用应用权限，而非用户委派的权限。 因此，应用可能可以执行用户无法执行的操作，例如创建通道或删除选项卡。应在调用 RSC API 之前审查团队所有者有关用例的意图。 *请参阅* [Microsoft Teams API 概述](/graph/teams-concept-overview)。

将应用安装到团队后，可以使用 [Graph 浏览器](https://developer.microsoft.com/graph/graph-explorer)  查看该团队中已授予应用的权限：

> [!div class="checklist"]
>
>- 从 Teams 客户端**获取团队的 groupId。**
> - 在 Teams 客户端中，从最左侧导航栏选择**Teams。**
> - 从下拉菜单中选择安装应用的团队。
> - 选择" **更多"选项** (&#8943;) 。
> - 选择 **"获取团队链接"。**
> - 复制并保存字符串 **中的 groupId** 值。
> - 登录到 **Graph 浏览器**。
> - 对以下 **端** 点执行 GET 调用 `https://graph.microsoft.com/beta/groups/{teamGroupId}/permissionGrants` ： 响应中的 clientAppId 字段将映射到 Teams 应用部件清单 （manifest） 中指定的 appId。
  ![GET 调用的图形浏览器响应。](../../assets/images/graph-permissions.png)
 
## <a name="test-resource-specific-consent"></a>测试特定于资源的许可
 
> [!div class="nextstepaction"]
> [**测试 Teams 中特定于资源的许可权限**](test-resource-specific-consent.md)
 
## <a name="related-topic-for-teams-administrators"></a>Teams 管理员相关主题

> [!div class="nextstepaction"]
> [**Microsoft Teams 中面向管理员的特定于资源的同意**](/MicrosoftTeams/resource-specific-consent)
> 
