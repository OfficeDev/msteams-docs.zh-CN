---
title: 在 Teams 中启用资源特定许可
description: 本文介绍 Microsoft Teams 中特定于资源的许可以及如何利用它。
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: reference
ms.openlocfilehash: 7321c3dbf1f2a3493a1d457cfd80d7fc1efb01d6
ms.sourcegitcommit: 82c585d287d61924ce3a3bba3e9caeff35c9a27a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/02/2022
ms.locfileid: "67586705"
---
# <a name="resource-specific-consent"></a>资源特定许可

> [!NOTE]
> 针对聊天范围的资源特定许可仅适用于[公共开发人员预览版](../../resources/dev-preview/developer-preview-intro.md)。

资源特定许可 (RSC) 是 Microsoft Teams 和 Microsoft Graph API 的集成，允许你的应用使用 API 终结点来管理组织内的特定资源（团队或聊天对话）。 RSC 权限模型允许 *团队所有者* 和 *聊天对话所有者* 分别授权某个应用程序访问和修改团队数据和聊天数据。

**注意：** 如果某个聊天有与其关联的会议或通话，则相关 RSC 权限也适用于这些资源。

## <a name="resource-specific-permissions"></a>资源特定权限

特定于 Teams 的精细 RSC 权限定义了应用程序可以在特定资源中执行的操作。

### <a name="resource-specific-permissions-for-a-team"></a>团队的资源特定权限

|应用权限| Action |
| ----- | ----- |
|TeamSettings.Read.Group | 获取此团队的设置。|
|TeamSettings.ReadWrite.Group|更新此团队的设置。|
|ChannelSettings.Read.Group|获取此团队的频道名称、频道说明和频道设置。|
|ChannelSettings.ReadWrite.Group|更新此团队的频道名称、频道说明和频道设置。|
|Channel.Create.Group|在这个团队中创建频道。 |
|Channel.Delete.Group|删除此团队中的频道。 |
|ChannelMessage.Read.Group |获取此团队的频道消息。 |
|TeamsAppInstallation.Read.Group|获取此团队的已安装应用列表。|
|TeamsTab.Read.Group|获取此团队的选项卡列表。|
|TeamsTab.Create.Group|在此团队中创建选项卡。 |
|TeamsTab.ReadWrite.Group|更新此团队的选项卡。 |
|TeamsTab.Delete.Group|删除此团队的选项卡。 |
|TeamMember.Read.Group|获取此团队的成员。 |
|TeamsActivity.Send.Group|在此团队中用户的活动信息提要内创建新通知。 |

有关更多详细信息，请参阅[团队的资源特定许可权限](/graph/permissions-reference#team-resource-specific-consent-permissions)。

### <a name="resource-specific-permissions-for-a-chat"></a>聊天的资源特定权限

下表提供了聊天的资源特定权限：

|应用权限| Action |
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
| TeamsAppInstallation.Read.Chat | 查看此聊天中安装了哪些应用。                   |
| OnlineMeeting.ReadBasic.Chat   | 读取与此聊天关联的会议基本属性，例如名称、日程安排、组织者、加入链接和开始/结束通知。 |
| Calls.AccessMedia.Chat         | 访问与此聊天或会议关联的通话中的媒体流。                                    |
| Calls.JoinGroupCalls.Chat         | 加入与此聊天或会议关联的通话。                                    |
| TeamsActivity.Send.Chat         | 在此聊天中用户的活动信息提要内创建新通知。 |
| OnlineMeetingTranscript.Read.Chat | 阅读与此聊天关联的会议的脚本。 |

有关更多详细信息，请参阅[聊天的资源特定许可权限](/graph/permissions-reference#chat-resource-specific-consent-permissions)。

> [!NOTE]
> 资源特定权限仅适用于 Teams 客户端上安装的 Teams 应用，目前不属于 Azure Active Directory (AAD) 门户。

## <a name="enable-rsc-in-your-application"></a>在应用程序中启用 RSC

1. [配置同意设置](#configure-consent-settings)。
    1. [使用 Azure AD 门户在团队中为 RSC 配置组所有者同意设置](#configure-group-owner-consent-settings-for-rsc-in-a-team-using-the-azure-ad-portal)。
    1. [使用 Microsoft Graph API 在聊天中为 RSC 配置聊天所有者同意设置](#configure-chat-owner-consent-settings-for-rsc-in-a-chat-using-the-microsoft-graph-apis)。
1. [使用 Azure AD 门户向 Microsoft 标识平台注册应用](#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。
1. [在 Azure AD 门户中查看应用程序权限](#review-your-application-permissions-in-the-azure-ad-portal)。
1. [从标识平台获取访问令牌](#obtain-an-access-token-from-the-microsoft-identity-platform)。
1. [更新 Teams 应用清单](#update-your-teams-app-manifest)。
1. [直接在 Teams 中安装应用](#sideload-your-app-in-teams)。
1. [检查是否为应用添加了 RSC 权限](#check-your-app-for-added-rsc-permissions)。
    1. [在团队中检查是否为应用添加了 RSC 权限](#check-your-app-for-added-rsc-permissions-in-a-team)。
    1. [在聊天中检查是否为应用添加了 RSC 权限](#check-your-app-for-added-rsc-permissions-in-a-chat)。

## <a name="configure-consent-settings"></a>配置同意设置

### <a name="configure-group-owner-consent-settings-for-rsc-in-a-team-using-the-azure-ad-portal"></a>使用 Azure AD 门户在团队中为 RSC 配置组所有者同意设置

可以直接在 Microsoft Azure 门户中启用或禁用[组所有者许可](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-portal)：

1. 以[全局管理员或公司管理员](/azure/active-directory/roles/permissions-reference#global-administrator&preserve-view=true)身份登录 [Azure 门户](https://portal.azure.com)。
1. 选择“**Azure Active Directory**” > “**企业应用程序**” > “**许可和权限**” > “[**用户同意设置**](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ConsentPoliciesMenuBlade/UserSettings)”。
1. 使用标记为“**针对访问数据的应用的组所有者许可**”的控件启用、禁用或限制用户许可。 默认值为“**允许针对所有组所有者的组所有者许可**”。 对于使用 RSC 安装应用的团队所有者，必须为该用户启用组所有者许可。

    ![Azure RSC 团队配置](../../assets/images/azure-rsc-team-configuration.png)

此外，还可以使用 PowerShell 启用或禁用组所有者许可，按照[使用 PowerShell 配置组所有者许可](/azure/active-directory/manage-apps/configure-user-consent-groups?tabs=azure-powershell)中所述的步骤操作。

### <a name="configure-chat-owner-consent-settings-for-rsc-in-a-chat-using-the-microsoft-graph-apis"></a>使用 Microsoft Graph API 在聊天中为 RSC 配置聊天所有者同意设置

可以使用图形 API为聊天启用或禁用 RSC。 [**teamsAppSettings**](/graph/api/teamsappsettings-update#example-1-enable-installation-of-apps-that-require-resource-specific-consent-in-chats-meetings) 中的属性`isChatResourceSpecificConsentEnabled`控制是否在租户中启用聊天 RSC。

   ![图形 RSC 团队配置](../../assets/images/rsc/graph-rsc-chat-configuration.png)

> 属性的默认值 **是ChatResourceSpecificConsentEnabled** ，它基于首次使用 RSC 进行聊天时租户中是否打开或关闭 [用户同意设置](/azure/active-directory/manage-apps/configure-user-consent?tabs=azure-portal) 。 这可能是) 首次检索 [**teamsAppSettings**](/graph/api/teamsappsettings-get) 或 b) 在聊天/会议中安装具有资源特定权限的 Teams 应用。

## <a name="register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal"></a>使用 Azure AD 门户向 Microsoft 标识平台注册应用

Azure AD 门户提供了一个用于注册和配置应用的中央平台。 必须在 Azure AD 门户中注册应用，才能将其与标识平台集成并调用 Microsoft Graph API。 有关详细信息，请参阅[向标识平台注册应用程序](/graph/auth-register-app-v2)。

> [!WARNING]
> 不能在多个 Teams 应用之间共享 Azure AD 应用 ID。 Teams 应用和 Azure AD 应用之间必须存在 1:1 映射。 尝试安装与同一 Azure AD 应用 ID 关联的多个 Teams 应用将导致安装或运行时失败。

## <a name="review-your-application-permissions-in-the-azure-ad-portal"></a>在 Azure AD 门户中查看应用程序权限

1. 转到“**主页**” > “**应用注册**”页面，然后选择你的 RSC 应用。
1. 从左窗格中选择“**API 权限**”，然后浏览应用的“**已配置权限**”列表。 如果应用只进行 RSC Graph API 调用，请删除该页面上的所有权限。 如果应用也进行非 RSC 调用，请根据需要保留这些权限。

> [!IMPORTANT]
> Azure AD 门户不能用于请求 RSC 权限。 RSC 权限目前专属于 Teams 客户端中安装的 Teams 应用程序，并在 Teams 应用清单 (JSON) 文件中声明。

## <a name="obtain-an-access-token-from-the-microsoft-identity-platform"></a>从 Microsoft 标识平台获取访问令牌

若要进行 Graph API 调用，必须从标识平台获取应用的访问令牌。 必须先在 Azure AD 门户中注册应用，然后该应用才能从 Microsoft 标识平台获取令牌。 访问令牌包含你的应用的相关信息，还有它就可通过 Microsoft Graph 访问的资源和 API 所具备的权限。

必须具有 Azure AD 注册过程中的以下值，才能从标识平台检索访问令牌：

* 应用注册门户分配的 **应用程序 ID**。 如果应用支持单一登录 (SSO)，则必须对应用和 SSO 使用相同的应用程序 ID。
* **客户端机密/密码** 或作为 **证书** 的公钥或私钥对。 这不是本机应用的必需项。
* 可让应用接收来自 Azure AD 的响应的 **重定向 URI**（或回复 URL）。

有关详细信息，请参阅[代表用户获取访问权限](/graph/auth-v2-user?view=graph-rest-1.0#3-get-a-token&preserve-view=true)和[在没有用户的情况下获取访问权限](/graph/auth-v2-service)。

## <a name="update-your-teams-app-manifest"></a>更新 Teams 应用清单

RSC 权限在应用清单 JSON 文件中声明。

> [!IMPORTANT]
> 非 RSC 权限存储在 Azure 门户中。 请勿将它们添加到应用清单。

### <a name="manifest-changes-for-resource-specific-consent"></a>针对资源特定许可的清单更改

<br>

<details>

<summary><b>应用清单版本 1.12 的 RSC 权限</b></summary>

使用以下值将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到应用清单：

|名称| 类型 | 说明|
|---|---|---|
|`id` |字符串 |你的 Azure AD 应用 ID。 有关详细信息，请参阅[在 Azure AD 门户中注册应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。|
|`resource`|String| 此字段在 RSC 中没有操作，但必须添加并包含值以免出现错误响应；任何字符串都可以。|

指定应用所需的权限。

|名称| 类型 | 说明|
|---|---|---|
|`authorization`|Object|应用运行所需的权限列表。 有关详细信息，请参阅 [清单中的授权链接占位符]

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
> 如果应用旨在支持在团队和聊天范围内安装，则可以在 `authorization` 下的同一清单中指定团队和聊天权限。

<br>

</details>

<br>

<details>

<summary><b>应用清单版本 1.11 或更低版本的 RSC 权限</b></summary>

使用以下值将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到应用清单：

|名称| 类型 | 说明|
|---|---|---|
|`id` |字符串 |你的 Azure AD 应用 ID。 有关详细信息，请参阅[在 Azure AD 门户中注册应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。|
|`resource`|String| 此字段在 RSC 中没有操作，但必须添加并包含值以免出现错误响应；任何字符串都可以。|
|`applicationPermissions`|字符串数组|应用的 RSC 权限。 有关详细信息，请参阅[特定于资源的权限](resource-specific-consent.md#resource-specific-permissions)。|

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
> 如果应用旨在支持在团队和聊天范围内安装，则可以在 `applicationPermissions` 下的同一清单中指定团队和聊天权限。

<br>

</details>

## <a name="sideload-your-app-in-teams"></a>在 Teams 中旁加载应用

如果 Teams 管理员允许上传自定义应用，则可以直接将[应用旁加载](~/concepts/deploy-and-publish/apps-upload.md)到特定团队或聊天。

## <a name="check-your-app-for-added-rsc-permissions"></a>检查是否为应用添加了 RSC 权限

> [!IMPORTANT]
> RSC 权限不属于用户。 调用是使用应用权限进行的，而不是用户委派权限。 可以允许应用执行用户无法执行的操作，例如删除选项卡。在进行 RSC API 调用之前，必须先查看团队所有者或聊天所有者对你的用法的意向。 有关详细信息，请参阅 [Microsoft Teams API 概述](/graph/teams-concept-overview)。

将应用安装到资源后，可以使用 [Graph 浏览器](https://developer.microsoft.com/graph/graph-explorer)查看资源中已授予应用的权限。

### <a name="check-your-app-for-added-rsc-permissions-in-a-team"></a>在团队中检查是否为应用添加了 RSC 权限

1. 从 Teams 获取团队的 **groupId**。
1. 在 Teams 中，从最左侧窗格中选择“**Teams**”。
1. 选择要安装应用的团队。
1. 选择该团队对应的省略号 &#x25CF;&#x25CF;&#x25CF;。
1. 从团队下拉菜单中选择“**获取团队链接**”。
1. 从“**获取指向团队的链接**”弹出对话框中复制并保存 **groupId** 值。
1. 登录到 **Graph 浏览器**。
1. 对以下终结点进行 **GET** 调用：`https://graph.microsoft.com/beta/teams/{teamGroupId}/permissionGrants`。 响应中的 `clientAppId` 字段将映射到 Teams 应用清单中指定的 `webApplicationInfo.id`。

    ![Graph 浏览器对针对团队 RSC 权限的 GET 调用的响应](../../assets/images/team-graph-permissions.png)

若要详细了解如何获取特定团队中安装的应用的详细信息，请参阅[获取指定团队中安装的应用的名称和其他详细信息](/graph/api/team-list-installedapps#example-2-get-the-names-and-other-details-of-installed-apps)。

### <a name="check-your-app-for-added-rsc-permissions-in-a-chat"></a>在聊天中检查是否为应用添加了 RSC 权限

1. 从 Teams *Web* 客户端获取聊天线程 ID。
1. 在 Teams Web 客户端中，从最左侧窗格中选择“**聊天**”。
1. 从下拉菜单中选择安装了应用的聊天。
1. 从字符串中复制 Web URL 并保存聊天线程 ID。

    ![Web URL 中的聊天线程 ID](../../assets/images/chat-thread-id.png)

1. 登录到 **Graph 浏览器**。
1. 对以下终结点进行 **GET** 调用：`https://graph.microsoft.com/beta/chats/{chatId}/permissionGrants`。 响应中的 `clientAppId` 字段将映射到 Teams 应用清单中指定的 `webApplicationInfo.id`。

    ![Graph 浏览器对针对聊天 RSC 权限的 GET 调用的响应](../../assets/images/chat-graph-permissions.png)

若要详细了解如何获取特定聊天中安装的应用的详细信息，请参阅[获取指定聊天中安装的应用的名称和其他详细信息](/graph/api/chat-list-installedapps#example-2-get-the-names-and-other-details-of-apps-installed-in-the-specified-chat)。

## <a name="code-sample"></a>代码示例

| **示例名称** | **说明** | **.NET** |**Node.js** |
|-----------------|-----------------|----------------|----------------|
| 资源特定许可 (RSC) | 使用 RSC 调用 Graph API。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/graph-rsc/nodeJs)|

## <a name="see-also"></a>另请参阅

* [在 Teams 中测试资源特定许可权限](test-resource-specific-consent.md)
* [Microsoft Teams 中针对管理员的资源特定许可](/MicrosoftTeams/resource-specific-consent)
