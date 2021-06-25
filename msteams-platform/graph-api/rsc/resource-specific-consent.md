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
# <a name="resource-specific-consent"></a>资源特定许可

> [!NOTE]
> 聊天范围的特定于资源的同意仅适用于 [公共开发人员预览](../../resources/dev-preview/developer-preview-intro.md) 版。

资源特定的同意 (RSC) 是一种 Microsoft Teams 和 Microsoft Graph API 集成，使你的应用可以使用 API 终结点来管理组织中特定的资源（团队或聊天）。 RSC 权限模型使团队所有者和聊天所有者可以分别授予应用程序访问和修改团队数据和聊天数据的许可。

## <a name="resource-specific-permissions"></a>特定于资源的权限

具体、Teams特定的 RSC 权限定义应用程序可以在特定资源中执行哪些操作。

### <a name="resource-specific-permissions-for-a-team"></a>团队的特定于资源的权限

|应用权限| 操作 |
| ----- | ----- |
|TeamSettings.Read.Group | 获取此团队的设置。|
|TeamSettings.ReadWrite.Group|更新此团队的设置。|
|ChannelSettings.Read.Group|获取此团队的频道名称、频道说明和频道设置。|
|ChannelSettings.ReadWrite.Group|更新此团队的频道名称、频道说明和频道设置。|
|Channel.Create.Group|在这个团队中创建频道。 |
|Channel.Delete.Group|删除此团队中的频道。 |
|ChannelMessage.Read.Group |获取此团队的频道消息。 |
|TeamsAppInstallation.Read.Group|获取此团队已安装应用的列表。|
|TeamsTab.Read.Group|获取此团队的选项卡列表。|
|TeamsTab.Create.Group|在此团队中创建选项卡。 |
|TeamsTab.ReadWrite.Group|更新此团队的选项卡。 |
|TeamsTab.Delete.Group|删除此团队的选项卡。 |
|TeamMember.Read.Group|获取此团队的成员。 |

有关详细信息，请参阅团队 [资源特定的许可权限](/graph/permissions-reference#teams-resource-specific-consent-permissions)。

### <a name="resource-specific-permissions-for-a-chat"></a>聊天的特定于资源的权限

下表提供了聊天的特定于资源的权限：

|应用权限| 操作 |
| ----- | ----- |
| ChatSettings.Read.Chat         | 获取此聊天的设置。                                    |
| ChatSettings.ReadWrite.Chat    | 更新此聊天的设置。                          |
| ChatMessage.Read.Chat          | 获取此聊天的消息。                                    |
| ChatMember.Read.Chat           | 获取此聊天的成员。                                     |
| Chat.Manage.Chat               | 管理此聊天。                                             |
| TeamsTab.Read.Chat             | 获取此聊天的选项卡。                                        |
| TeamsTab.Create.Chat           | 在此聊天中创建选项卡。                                     |
| TeamsTab.Delete.Chat           | 删除此聊天的选项卡。                                      |
| TeamsTab.ReadWrite.Chat        | 管理此聊天的选项卡。                                      |
| TeamsAppInstallation.Read.Chat | 获取此聊天中安装的应用。                   |
| OnlineMeeting.ReadBasic.Chat   | 获取与此聊天关联的会议的基本属性，如名称、日程安排、组织者和加入链接。 |

有关详细信息，请参阅 [聊天资源特定的许可权限](/graph/permissions-reference#chat-resource-specific-consent-permissions)。

> [!NOTE]
> 特定于资源的权限仅适用于安装在 Teams 客户端上的 Teams 应用，并且当前不是 Azure Active Directory (AAD) 的一部分。

## <a name="enable-rsc-in-your-application"></a>在应用程序中启用 RSC

1. [在 AAD 门户中配置同意设置](#configure-consent-settings-in-the-aad-portal)。
    1. [为团队中的 RSC 配置组所有者同意设置](#configure-group-owner-consent-settings-for-rsc-in-a-team)。
    1. [在聊天中为 RSC 配置用户同意设置](#configure-user-consent-settings-for-rsc-in-a-chat)。
1. [使用 AAD Microsoft 标识平台注册你的应用](#register-your-app-with-microsoft-identity-platform-using-the-aad-portal)。
1. [在 AAD 门户中查看应用程序权限](#review-your-application-permissions-in-the-aad-portal)。
1. [从标识平台 获取访问令牌](#obtain-an-access-token-from-the-microsoft-identity-platform)。
1. [更新应用Teams清单](#update-your-teams-app-manifest)。
1. [直接在 Teams 中安装应用](#sideload-your-app-in-teams)。
1. [检查应用是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions)。
    1. [检查你的应用在团队中是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions-in-a-team)。
    1. [检查你的应用在聊天中是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions-in-a-chat)。

## <a name="configure-consent-settings-in-the-aad-portal"></a>在 AAD 门户中配置许可设置

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a>为团队中的 RSC 配置组所有者同意设置

可以直接在 Azure 门户 [中启用](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal) 或禁用组所有者同意：

1. 以全局管理员或公司管理员登录 [Azure](https://portal.azure.com) [门户](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。
1. 选择 **Azure Active Directory Enterprise**  >    >  **同意和权限**  >  [**用户同意设置"。**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)
1. 使用标记为组所有者同意的控件启用、禁用或限制用户 **同意访问数据的应用**。 默认值为 **允许所有组所有者获得组所有者同意**。 对于使用 RSC 安装应用的团队所有者，必须为该用户启用组所有者同意。

    ![Azure RSC 团队配置](../../assets/images/azure-rsc-team-configuration.png)

此外，您可以使用 PowerShell 启用或禁用组所有者同意，按照使用 PowerShell 配置组所有者同意中概述 [的步骤操作](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a>在聊天中为 RSC 配置用户同意设置

可以直接在 Azure 门户 [中启用](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) 或禁用用户同意：

1. 以全局管理员或公司管理员登录 [Azure](https://portal.azure.com) [门户](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。
1. 选择 **Azure Active Directory Enterprise**  >    >  **同意和权限**  >  [**用户同意设置"。**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)
1. 使用标记为"应用程序的用户同意"的控件启用 **、禁用或限制用户同意**。 默认值为 **"允许用户同意应用"。** 若要聊天成员使用 RSC 安装应用，必须为该用户启用用户同意。

    ![Azure RSC 聊天配置](../../assets/images/azure-rsc-chat-configuration.png)

此外，您可以使用 PowerShell 启用或禁用用户同意，按照使用 PowerShell 配置用户同意中 [概述的步骤操作](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell)。

## <a name="register-your-app-with-microsoft-identity-platform-using-the-aad-portal"></a>使用 AAD Microsoft 标识平台注册应用

AAD 门户提供了一个中央平台，用于注册和配置应用。 你的应用必须在 AAD 门户中注册才能与标识平台集成，并调用 Microsoft Graph API。 有关详细信息，请参阅 [向标识平台注册应用程序](/graph/auth-register-app-v2)。

> [!WARNING]
> AAD 应用 ID 不能跨多个应用Teams共享。 在一个应用和一个 AAD 应用Teams一对一映射。 尝试安装多个与Teams AAD 应用 ID 关联的应用将导致安装或运行时失败。

## <a name="review-your-application-permissions-in-the-aad-portal"></a>在 AAD 门户中查看应用程序权限

1. 转到"**主页**  >  **应用注册"** 页并选择 RSC 应用。
1. 从 **左窗格中选择"API** 权限"，然后浏览应用的 **"已配置权限"** 列表。 如果你的应用仅进行 RSC Graph API 调用，请删除该页面上的所有权限。 如果你的应用还进行非 RSC 调用，请保留所需的权限。

> [!IMPORTANT]
> AAD 门户不能用于请求 RSC 权限。 RSC 权限当前专用于 Teams 客户端中安装的 Teams 应用程序，这些权限在 Teams 应用程序清单 (JSON) 文件中声明。

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>从应用程序获取访问Microsoft 标识平台

若要Graph API 调用，必须从标识平台获取应用的访问令牌。 应用必须先在 AAD 门户中注册，然后才能从标识平台获取令牌。 访问令牌包含你的应用的相关信息，还有它就可通过 Microsoft Graph 访问的资源和 API 所具备的权限。

您必须具有来自 AAD 注册过程的以下值，以从标识平台检索访问令牌：

- 应用注册门户分配的应用程序 **ID。** 如果你的应用支持单一登录 (SSO) 你必须对应用和 SSO 使用相同的应用程序 ID。
- 客户端 **密码/密码** 或公钥或私钥对，即 **证书**。 这不是本机应用的必需项。
- 应用接收来自 AAD 的响应的重定向 **URI** 或回复 URL。

有关详细信息，请参阅 [代表用户获取访问权限和](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true) 在没有 [用户的情况下获取访问权限](/graph/auth-v2-service)。

## <a name="update-your-teams-app-manifest"></a>更新Teams应用程序清单

RSC 权限在应用清单 JSON 文件中声明。 将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：

|名称| 类型 | 说明|
|---|---|---|
|`id` |String |AAD 应用 ID。 有关详细信息，请参阅在 [AAD 门户中注册应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-aad-portal)。|
|`resource`|String| 此字段在 RSC 中没有任何操作，但必须添加该字段，并且必须具有值以避免错误响应;任何字符串将执行。|
|`applicationPermissions`|字符串数组|应用的 RSC 权限。 有关详细信息，请参阅特定于 [资源的权限](resource-specific-consent.md#resource-specific-permissions)。|

>
> [!IMPORTANT]
> 非 RSC 权限存储在 Azure 门户中。 不要将它们添加到应用清单。
>

### <a name="example-for-rsc-in-a-team"></a>团队中的 RSC 示例

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

### <a name="example-for-rsc-in-a-chat"></a>聊天中的 RSC 示例

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
> 如果应用旨在支持在团队和聊天范围内安装，可以在 下的同一清单中指定团队和聊天权限 `applicationPermissions` 。

## <a name="sideload-your-app-in-teams"></a>在应用程序中旁加载Teams

如果你的Teams管理员允许自定义应用上传，你可以将应用直接旁加载[](~/concepts/deploy-and-publish/apps-upload.md)到特定团队或聊天。

## <a name="check-your-app-for-added-rsc-permissions"></a>检查应用是否添加了 RSC 权限

> [!IMPORTANT]
> RSC 权限不归为用户。 调用使用应用程序权限而不是用户委派权限进行。 可以允许应用执行用户无法执行的操作，例如删除选项卡。必须先查看团队所有者或聊天所有者的意图，然后才能进行 RSC API 调用。 有关详细信息，请参阅 Microsoft Teams [API 概述](/graph/teams-concept-overview)。

将应用安装到资源后，可以使用 Graph[资源管理器](https://developer.microsoft.com/graph/graph-explorer)查看已授予资源中应用程序的权限。

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a>检查你的应用在团队中是否添加了 RSC 权限

1. 从组获取 **团队的 groupId** Teams。
1. In Teams， select **Teams** from the leftmost pane.
1. 选择要安装应用的团队。
1. 选择该团队 &#x25CF;&#x25CF;&#x25CF; 省略号。
1. 从 **团队下拉菜单中选择** 获取团队链接。
1. 复制并保存"获取团队链接"弹出对话框中的 **groupId** 值。
1. 登录到 Graph **资源管理器**。
1. 对此终结点 **进行 GET** 调用 `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants` ：。 响应 `clientAppId` 中的字段将映射到应用程序清单 `webApplicationInfo.id` Teams中指定的。

    ![Graph对团队 RSC 权限的 GET 调用的浏览器响应](../../assets/images/team-graph-permissions.png)

若要详细了解如何获取特定团队中安装的应用的详细信息，请参阅获取指定团队中安装的应用 [的名称和其他详细信息](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)。

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a>检查你的应用在聊天中是否添加了 RSC 权限

1. 从 Web 客户端获取Teams *ID。*
1. 在 Teams 客户端中 **，从最** 左侧的窗格中选择"聊天"。
1. 从下拉菜单中选择应用安装位置的聊天。
1. 复制 Web URL，然后从字符串中保存聊天线程 ID。

    ![来自 Web URL 的聊天线程 ID](../../assets/images/chat-thread-id.png)

1. 登录到 Graph **资源管理器**。
1. 对以下 **终结点** 进行 GET 调用 `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants` ：。 响应 `clientAppId` 中的字段将映射到应用程序清单 `webApplicationInfo.id` Teams中指定的。

    ![Graph对聊天 RSC 权限的 GET 调用的浏览器响应](../../assets/images/chat-graph-permissions.png)

若要详细了解如何获取特定聊天中安装的应用的详细信息，请参阅获取指定聊天中安装的应用 [的名称和其他详细信息](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Resource-Specific RSC (同意)  | 使用 RSC 调用Graph API。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|

## <a name="see-also"></a>另请参阅
 
* [在应用程序内测试特定于资源的许可Teams](test-resource-specific-consent.md)
* [管理员许可中Microsoft Teams特定资源的同意](/MicrosoftTeams/resource-specific-consent)
