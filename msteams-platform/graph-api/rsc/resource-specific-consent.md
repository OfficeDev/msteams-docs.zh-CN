---
title: 启用资源特定许可Teams
description: 介绍资源特定的Teams以及如何利用它。
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: reference
keywords: teams 授权 OAuth SSO Azure AD rsc Graph
ms.openlocfilehash: 613416c7363de8a9351e56f5cdb2a6a339b74392
ms.sourcegitcommit: b9af51e24c9befcf46945400789e750c34723e56
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/15/2022
ms.locfileid: "62821687"
---
# <a name="resource-specific-consent"></a>资源特定许可

> [!NOTE]
> 聊天范围的特定于资源的同意仅适用于 [公共开发人员预览](../../resources/dev-preview/developer-preview-intro.md) 版。

特定于资源 (RSC) 是一种 Microsoft Teams 和 Microsoft Graph API 集成，使你的应用可以使用 API 终结点来管理组织内的特定资源（团队或聊天）。 RSC 权限模型使团队所有者和聊天所有者可以分别授予应用程序访问和修改团队数据和聊天数据的许可。 

**注意：** 如果聊天具有与之关联的会议或呼叫，则相关的 RSC 权限也适用于这些资源。

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
|TeamsActivity.Send.Group|在此团队中用户的活动源中创建新通知。 |

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
| OnlineMeeting.ReadBasic.Chat   | 读取与此聊天关联的会议的基本属性，如姓名、日程安排、组织者、加入链接和开始/结束通知。 |
| Calls.AccessMedia.Chat         | 访问与此聊天或会议关联的通话中的媒体流。                                    |
| Calls.JoinGroupCalls.Chat         | 加入与此聊天或会议关联的通话。                                    |
| TeamsActivity.Send.Chat         | 在此聊天中用户的活动源中创建新通知。 |

有关详细信息，请参阅 [聊天资源特定的许可权限](/graph/permissions-reference#chat-resource-specific-consent-permissions)。

> [!NOTE]
> 特定于资源的权限仅适用于安装在 Teams 客户端上的Teams应用，并且当前不是 Azure Active Directory (AAD) 门户的一部分。

## <a name="enable-rsc-in-your-application"></a>在应用程序中启用 RSC

1. [在门户中配置Azure AD设置](#configure-consent-settings-in-the-azure-ad-portal)。
    1. [为团队中的 RSC 配置组所有者同意设置](#configure-group-owner-consent-settings-for-rsc-in-a-team)。
    1. [在聊天中为 RSC 配置用户同意设置](#configure-user-consent-settings-for-rsc-in-a-chat)。
1. [使用应用门户Microsoft 标识平台应用Azure AD应用](#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。
1. [在应用程序门户中查看Azure AD权限](#review-your-application-permissions-in-the-azure-ad-portal)。
1. [从标识平台获取访问令牌](#obtain-an-access-token-from-the-microsoft-identity-platform)。
1. [更新你的Teams清单](#update-your-teams-app-manifest)。
1. [直接在应用中安装Teams](#sideload-your-app-in-teams)。
1. [检查应用是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions)。
    1. [检查你的应用在团队中是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions-in-a-team)。
    1. [检查你的应用在聊天中是否添加了 RSC 权限](#check-your-app-for-added-rsc-permissions-in-a-chat)。

## <a name="configure-consent-settings-in-the-azure-ad-portal"></a>在门户中配置Azure AD设置

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team"></a>为团队中的 RSC 配置组所有者同意设置

可以直接在应用门户[中启用](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal)或禁用Microsoft Azure许可：

1. 以全局管理员 [或](https://portal.azure.com) 公司管理员登录 Azure [门户](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。
1. 选择 **Azure Active Directory** >  **Enterprise应用程序** > **""用户同意设置"和"权限** > [**"**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)。
1. 使用标记为组所有者同意的控件启用、禁用或限制用户 **同意访问数据的应用**。 默认值为 **"允许所有组所有者获得组所有者同意"**。 对于使用 RSC 安装应用的团队所有者，必须为该用户启用组所有者同意。

    ![Azure RSC 团队配置](../../assets/images/azure-rsc-team-configuration.png)

此外，您可以使用 PowerShell 启用或禁用组所有者同意，按照使用 PowerShell 配置组所有者 [同意中概述的步骤操作](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)。

### <a name="configure-user-consent-settings-for-rsc-in-a-chat"></a>在聊天中为 RSC 配置用户同意设置

可以直接在 Azure 门户 [中启用](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) 或禁用用户同意：

1. 以全局管理员 [或](https://portal.azure.com) 公司管理员登录 Azure [门户](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)。
1. 选择 **Azure Active Directory** >  **Enterprise应用程序** > **""用户同意** 设置"和"权限 > [**"**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)。
1. 使用标记为"应用程序的用户同意"的控件启用 **、禁用或限制用户同意**。 默认值为 **"允许用户同意应用"**。 若要聊天成员使用 RSC 安装应用，必须为该用户启用用户同意。

    ![Azure RSC 聊天配置](../../assets/images/azure-rsc-chat-configuration.png)

此外，您可以使用 PowerShell 启用或禁用用户同意，按照使用 PowerShell 配置用户同意 [中概述的步骤操作](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-powershell)。

## <a name="register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal"></a>使用应用门户Microsoft 标识平台应用Azure AD应用

Azure AD门户提供了一个中央平台，用于注册和配置应用。 必须在应用门户中注册Azure AD与标识平台集成，并调用 Microsoft Graph API。 有关详细信息，请参阅 [向标识平台注册应用程序](/graph/auth-register-app-v2)。

> [!WARNING]
> 一Azure AD应用 ID 不能跨多个应用Teams共享。 一个应用和一个应用Teams 1：1 Azure AD映射。 尝试安装多个与Teams ID 关联的应用Azure AD安装或运行时失败。

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>在应用程序门户中查看Azure AD权限

1. 转到 **HomeApp**  >  注册页面并选择 RSC 应用。
1. 从 **左窗格中选择"API** 权限"，然后浏览应用的 **"已配置权限"** 列表。 如果你的应用仅进行 RSC Graph API 调用，请删除该页面上的所有权限。 如果你的应用还进行非 RSC 调用，请保留所需的权限。

> [!IMPORTANT]
> Azure AD门户不能用于请求 RSC 权限。 RSC 权限当前专用于 Teams 客户端中安装的 Teams 应用程序，这些权限在 Teams 应用清单 (JSON) 文件中声明。

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>从应用程序获取访问Microsoft 标识平台

若要Graph API 调用，必须从标识平台获取应用的访问令牌。 在你的应用可以从标识平台获取令牌之前，必须在 Azure AD 门户中注册。 访问令牌包含你的应用的相关信息，还有它就可通过 Microsoft Graph 访问的资源和 API 所具备的权限。

必须在注册过程中具有以下Azure AD从标识平台检索访问令牌：

- **应用注册** 门户分配的应用程序 ID。 如果你的应用支持单一登录 (SSO) 你必须对应用和 SSO 使用相同的应用程序 ID。
- 客户端 **密码/密码** 或作为证书的公钥或私钥 **对**。 这不是本机应用的必需项。
- **应用的重定向 URI** 或回复 URL，用于接收来自Azure AD。

有关详细信息，请参阅[代表用户获取访问权限和](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true)[在没有用户的情况下获取访问权限](/graph/auth-v2-service)。

## <a name="update-your-teams-app-manifest"></a>更新Teams应用程序清单

RSC 权限在应用清单 JSON 文件中声明。 

> [!IMPORTANT]
> 非 RSC 权限存储在 Azure 门户中。 不要将它们添加到应用清单。

### <a name="manifest-changes-for-resource-specific-consent"></a>特定于资源的同意的清单更改

<br>

<details>

<summary><b>应用清单版本 1.12 的 RSC 权限</b></summary>

将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：

|姓名| 类型 | 说明|
|---|---|---|
|`id` |String |你的Azure AD ID。 有关详细信息，请参阅在[应用门户中Azure AD应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。|
|`resource`|String| 此字段在 RSC 中没有任何操作，但必须添加该字段，并且必须具有值以避免错误响应;任何字符串将执行。|

指定应用程序所需的权限。

|姓名| 类型 | 说明|
|---|---|---|
|`authorization`|Object|应用运行所需的权限列表。 有关详细信息，请参阅 [清单中 link- 授权的占位符]

团队中的 RSC 示例

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp"
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "TeamSettings.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamSettings.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "ChannelSettings.Read.Group",
                "type": "Application"
            },
            {
                "name": "ChannelSettings.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "Channel.Create.Group",
                "type": "Application"
            },
            {
                "name": "Channel.Delete.Group",
                "type": "Application"
            },
            {
                "name": "ChannelMessage.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsAppInstallation.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Create.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.ReadWrite.Group",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Delete.Group",
                "type": "Application"
            },
            {
                "name": "TeamMember.Read.Group",
                "type": "Application"
            },
            {
                "name": "TeamsActivity.Send.Group",
                "type": "Application"
            }
        ]    
    }
}
```

聊天中的 RSC 示例

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp"
    },
"authorization": {
    "permissions": {
        "resourceSpecific": [
            {
                "name": "ChatSettings.Read.Chat",
                "type": "Application"
            },
            {
                "name": "ChatSettings.ReadWrite.Chat",
                "type": "Application"
            },
            {
                "name": "ChatMessage.Read.Chat",
                "type": "Application"
            },
            {
                "name": "ChatMember.Read.Chat",
                "type": "Application"
            },
            {
                "name": "Chat.Manage.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Read.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Create.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.Delete.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsTab.ReadWrite.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsAppInstallation.Read.Chat",
                "type": "Application"
            },
            {
                "name": "OnlineMeeting.ReadBasic.Chat",
                "type": "Application"
            },
            {
                "name": "Calls.AccessMedia.Chat",
                "type": "Application"
            },
            {
                "name": "Calls.JoinGroupCalls.Chat",
                "type": "Application"
            },
            {
                "name": "TeamsActivity.Send.Chat",
                "type": "Application"
            }
        ]    
    }
}
```

> [!NOTE]
> 如果应用旨在支持在团队和聊天范围内安装，可以在 下的同一清单中指定团队和聊天权限 `authorization`。
    
<br>

</details>

<br>

<details>

<summary><b>应用清单版本 1.11 或更早版本的 RSC 权限</b></summary>

将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：

|姓名| 类型 | 说明|
|---|---|---|
|`id` |String |你的Azure AD ID。 有关详细信息，请参阅在[应用门户中Azure AD应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。|
|`resource`|String| 此字段在 RSC 中没有任何操作，但必须添加该字段，并且必须具有值以避免错误响应;任何字符串将执行。|
|`applicationPermissions`|字符串数组|应用的 RSC 权限。 有关详细信息，请参阅特定于 [资源的权限](resource-specific-consent.md#resource-specific-permissions)。|

团队中的 RSC 示例

```json
"webApplicationInfo": {
    "id": "XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource": "https://RscBasedStoreApp",
    "applicationPermissions": [
        "TeamSettings.Read.Group",
        "TeamSettings.ReadWrite.Group",
        "ChannelSettings.Read.Group",
        "ChannelSettings.ReadWrite.Group",
        "Channel.Create.Group",
        "Channel.Delete.Group",
        "ChannelMessage.Read.Group",
        "TeamsAppInstallation.Read.Group",
        "TeamsTab.Read.Group",
        "TeamsTab.Create.Group",
        "TeamsTab.ReadWrite.Group",
        "TeamsTab.Delete.Group",
        "TeamMember.Read.Group",
        "TeamsActivity.Send.Group"
    ]
  }
```

聊天中的 RSC 示例

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
        "OnlineMeeting.ReadBasic.Chat",
        "Calls.AccessMedia.Chat",
        "Calls.JoinGroupCalls.Chat",
        "TeamsActivity.Send.Chat"
    ]
  }
```

> [!NOTE]
> 如果应用旨在支持在团队和聊天范围内安装，可以在 下的同一清单中指定团队和聊天权限 `applicationPermissions`。
    
<br>

</details>

## <a name="sideload-your-app-in-teams"></a>在 Teams 中旁加载应用

如果你Teams管理员允许自定义应用上传，你可以将应用直接旁加载[](~/concepts/deploy-and-publish/apps-upload.md)到特定团队或聊天。

## <a name="check-your-app-for-added-rsc-permissions"></a>检查应用是否添加了 RSC 权限

> [!IMPORTANT]
> RSC 权限不归为用户。 调用使用应用程序权限而不是用户委派权限进行。 可以允许应用执行用户无法执行的操作，例如删除选项卡。必须先查看团队所有者或聊天所有者的意图，然后才能进行 RSC API 调用。 有关详细信息，请参阅 Microsoft Teams [API 概述](/graph/teams-concept-overview)。

将应用安装到资源后，可以使用 Graph [资源管理器](https://developer.microsoft.com/graph/graph-explorer)查看已授予资源中应用程序的权限。

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a>检查你的应用在团队中是否添加了 RSC 权限

1. 从组获取 **团队的 groupId** Teams。
1. In Teams， select **Teams** from the leftmost pane.
1. 选择要安装应用的团队。
1. 选择该团队 &#x25CF;&#x25CF;&#x25CF; 省略号。
1. 从 **团队下拉菜单中选择** 获取团队链接。
1. 复制并保存"获取团队链接"弹出对话框中的 **groupId** 值。
1. 登录到"Graph **资源管理器"**。
1. 对此终结点 **进行 GET** 调用： `https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants`。 响应`clientAppId`中的字段将映射到`webApplicationInfo.id`在应用程序清单Teams中指定。

    ![Graph对获取团队 RSC 权限的 GET 调用的浏览器响应](../../assets/images/team-graph-permissions.png)

若要详细了解如何获取特定团队中安装的应用的详细信息，请参阅获取指定团队中安装的应用 [的名称和其他详细信息](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)。

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a>检查你的应用在聊天中是否添加了 RSC 权限

1. 从 Web 客户端获取Teams *ID*。
1. 在 Teams客户端中 **，从最** 左侧的窗格中选择"聊天"。
1. 从下拉菜单中选择应用安装位置的聊天。
1. 复制 Web URL，然后从字符串中保存聊天线程 ID。

    ![来自 Web URL 的聊天线程 ID](../../assets/images/chat-thread-id.png)

1. 登录到"Graph **资源管理器"**。
1. 对以下 **终结点进行 GET** 调用： `https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants`。 响应`clientAppId`中的字段将映射到`webApplicationInfo.id`在应用程序清单Teams中指定。

    ![Graph对聊天 RSC 权限的 GET 调用的浏览器响应](../../assets/images/chat-graph-permissions.png)

若要详细了解如何获取特定聊天中安装的应用的详细信息，请参阅获取指定聊天中安装的应用 [的名称和其他详细信息](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| Resource-Specific RSC (同意)  | 使用 RSC 调用Graph API。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|

## <a name="see-also"></a>另请参阅
 
* [在应用程序内测试特定于资源的许可Teams](test-resource-specific-consent.md)
* [管理员许可Microsoft Teams资源特定许可](/MicrosoftTeams/resource-specific-consent)
