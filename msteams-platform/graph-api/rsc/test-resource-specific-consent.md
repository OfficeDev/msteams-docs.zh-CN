---
title: 在 Teams 中测试特定于资源的同意权限
description: 有关使用 Postman 和代码示例在 Teams 中测试特定于资源的同意的详细信息
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: Teams 授权 OAuth SSO Microsoft Azure Active Directory (Azure AD) rsc Postman Graph
ms.openlocfilehash: ade66f40662140b86fcc9ae2e185fc10ea09d2f2
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791711"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>在 Teams 中测试特定于资源的同意权限

> [!NOTE]
> 针对聊天范围的特定于资源的同意仅适用于[公共开发人员预览版](../../resources/dev-preview/developer-preview-intro.md)。

特定于资源的同意 (RSC) 是 Microsoft Teams 和 Graph API 的集成，允许你的应用使用 API 终结点来管理组织内的特定资源（团队或聊天对话）。 有关详细信息，请参阅[特定于资源的同意 (RSC) — Microsoft Teams 图形 API](resource-specific-consent.md)。

## <a name="prerequisites"></a>先决条件

在测试之前，请确保验证以下应用清单更改以获得特定于资源的同意：

<br>

<details>

<summary><b>应用清单版本 1.12 及更高版本的 RSC 权限</b></summary>

使用以下值将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到应用清单：

|名称| 类型 | 说明|
|---|---|---|
|`id` |字符串 |你的 Azure AD 应用 ID。 有关详细信息，请参阅[在 Azure AD 门户中注册应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。|
|`resource`|String| 此字段在 RSC 中没有操作，但必须添加并包含值以免出现错误响应；任何字符串都可以。|

指定应用所需的权限。

|名称| 类型 | 说明|
|---|---|---|
|`authorization`|Object|应用运行所需的权限列表。 有关详细信息，请参阅[授权](../../resources/schema/manifest-schema.md#authorization)。|

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

</details>

<br>

<details>

<summary><b>应用清单版本 1.11 及更低版本的 RSC 权限</b></summary>

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

<br>

> [!NOTE]
> 如果应用旨在支持在团队和聊天范围内安装，则可以在 `applicationPermissions` 下的同一清单中指定团队和聊天权限。

</details>

> [!IMPORTANT]
> 在应用清单中，仅包含你希望应用拥有的 RSC 权限。

> [!NOTE]
> 如果应用用于访问调用/媒体 API，则 `webApplicationInfo.Id` 应为 [Azure 机器人服务](/graph/cloud-communications-get-started#register-a-bot)的 Azure AD 应用 ID。

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>测试使用 Postman 应用向团队添加的 RSC 权限

若要检查 API 请求有效负载是否遵循 RSC 权限，需要将[团队的 RSC JSON 测试代码](test-team-rsc-json-file.md)复制到本地环境中并更新以下值：

* `azureADAppId`：应用的 Azure AD 应用 ID。
* `azureADAppSecret`：Azure AD 应用密码。
* `token_scope`：获取令牌所需的范围。 将值设置为 `https://graph.microsoft.com/.default`。
* `teamGroupId`：可以从 Teams 客户端获取团队组 ID，如下所示：

    1. 在 Teams 客户端中，从最左侧导航栏中选择“**团队**”。
    2. 从下拉菜单中选择安装应用的团队。
    3. 选择“**更多选项**”图标 (&#8943;)。
    4. 选择“**获取团队链接**”。
    5. 从字符串复制并保存 **groupId** 值。

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>测试使用 Postman 应用向聊天添加的 RSC 权限

若要检查 API 请求有效负载是否遵循 RSC 权限，需要将[聊天的 RSC JSON 测试代码](test-chat-rsc-json-file.md)复制到本地环境中并更新以下值：

* `azureADAppId`：应用的 Azure AD 应用 ID。
* `azureADAppSecret`：Azure AD 应用密码。
* `token_scope`：获取令牌所需的范围。 将值设置为 `https://graph.microsoft.com/.default`。
* `tenantId`：租户的名称或 Azure AD 对象 ID。
* `chatId`：可以从 Teams *Web* 客户端获取聊天线程 ID，如下所示：

    1. 在 Teams Web 客户端中，从最左侧导航栏中选择“**聊天**”。
    2. 从下拉菜单中选择安装了应用的聊天。
    3. 从字符串中复制 Web URL 并保存聊天线程 ID。
![来自 Web URL 的聊天线程 ID。](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>使用 Postman

1. 打开 [Postman](https://www.postman.com) 应用。
2. 选择”**文件**“ > ”**导入**” > ”**导入文件**”，以从环境中上传更新的 JSON 文件。  
3. 单击“**集合**”选项卡。
4. 选择“**测试 RSC**”旁边的 V 形线 **>** 以展开详细信息视图并查看 API 请求。

为每个 API 调用执行整个权限集合。 在应用清单中指定的权限必须成功，而未指定的权限必须失败并带有 HTTP 403 状态代码。 检查所有响应状态代码，确认应用中 RSC 权限的行为是否符合预期。

> [!NOTE]
> 若要测试特定的 DELETE 和 READ API 调用，请将这些实例方案添加到 JSON 文件。

## <a name="test-revoked-rsc-permissions-using-postman"></a>使用 [Postman](https://www.postman.com/) 测试已撤销的 RSC 权限

1. 从特定资源中卸载应用。
2. 为聊天或团队执行以下步骤：
    1. [测试使用 Postman 向团队添加的 RSC 权限](#test-added-rsc-permissions-to-a-team-using-the-postman-app)。
    2. [测试使用 Postman 向聊天添加的 RSC 权限](#test-added-rsc-permissions-to-a-chat-using-the-postman-app)。
3. 检查所有响应状态代码，确认特定 API 调用 **是否已失败并带有 HTTP 403 状态代码**。

## <a name="see-also"></a>另请参阅

* [Microsoft Graph API 和 Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)
* [特定于资源的同意](~/graph-api/rsc/resource-specific-consent.md)
