---
title: 在应用程序内测试特定于资源的许可Teams
description: 使用 Postman 和代码示例Teams中测试特定于资源的同意的详细信息
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: teams 授权 OAuth SSO Microsoft Azure Active Directory (Azure AD) rsc Postman Graph
ms.openlocfilehash: 15a2a80a8f1ce280b462ed6e6e99242fb30f0dc3
ms.sourcegitcommit: 90587b1ec04bf20d716ed6feb8ccca4313e87f8c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/10/2022
ms.locfileid: "62518119"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>在应用程序内测试特定于资源的许可Teams

> [!NOTE]
> 聊天范围的特定于资源的同意仅适用于 [公共开发人员预览](../../resources/dev-preview/developer-preview-intro.md) 版。

资源特定的同意 (RSC) 是一种 Microsoft Teams 和 Graph API 集成，使你的应用可以使用 API 终结点来管理组织中特定的资源（团队或聊天）。 有关详细信息，请参阅 [RSC (特定) — Microsoft Teams Graph API](resource-specific-consent.md)。

## <a name="prerequisites"></a>先决条件

在测试之前，请确保验证以下应用清单更改是否获得特定于资源的同意：

<br>

<details>

<summary><b>应用清单版本 1.12 的 RSC 权限</b></summary>

将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：

|名称| 类型 | 说明|
|---|---|---|
|`id` |String |你的Microsoft Azure Active Directory (Azure AD) 应用 ID。 有关详细信息，请参阅在[应用门户中Microsoft Azure Active Directory (Azure AD) 应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。|
|`resource`|String| 此字段在 RSC 中没有任何操作，但必须添加该字段，并且必须具有值以避免错误响应;任何字符串将执行。|

指定应用程序所需的权限。

|名称| 类型 | 说明|
|---|---|---|
|`authorization`|Object|应用运行所需的权限列表。 有关详细信息，请参阅 [授权](../../resources/schema/manifest-schema.md#authorization)。|

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

</details>

<br>

<details>

<summary><b>应用清单版本 1.11 或更早版本的 RSC 权限</b></summary>

将 [webApplicationInfo](../../resources/schema/manifest-schema.md#webapplicationinfo) 密钥添加到具有以下值的应用清单：

|名称| 类型 | 说明|
|---|---|---|
|`id` |String |你的Microsoft Azure Active Directory (Azure AD) 应用 ID。 有关详细信息，请参阅在[应用门户中Microsoft Azure Active Directory (Azure AD) 应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。|
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

<br>

> [!NOTE]
> 如果应用旨在支持在团队和聊天范围内安装，可以在 下的同一清单中指定团队和聊天权限 `applicationPermissions`。
    
</details>

> [!IMPORTANT]
> 在应用清单中，仅包含希望应用具有的 RSC 权限。

> [!NOTE]
> 如果应用旨在访问呼叫/媒体 API，则 应该`webApplicationInfo.Id`Microsoft Azure Active Directory (Azure AD) Azure Bot 服务[的应用 ID](/graph/cloud-communications-get-started#register-a-bot)。

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>使用 Postman 应用测试向团队添加的 RSC 权限

若要检查 API 请求有效负载是否接受 RSC 权限，需要将团队的 [RSC JSON](test-team-rsc-json-file.md) 测试代码复制到本地环境并更新以下值：

* `azureADAppId`：应用的应用Microsoft Azure Active Directory (Azure AD) ID。
* `azureADAppSecret`：Microsoft Azure Active Directory (Azure AD) 应用密码。
* `token_scope`：获取令牌需要 范围。 将值设置为 https://graph.microsoft.com/.default。
* `teamGroupId`：可以从客户端获取团队Teams ID，如下所示：

    1. 在Teams客户端 **中，Teams** 左侧导航栏中选择"导航"。
    2. 从下拉菜单中选择安装应用的团队。
    3. 选择" **更多选项"** 图标 (&#8943;) 。
    4. 选择 **"获取团队链接"**。 
    5. 复制并保存 **字符串中的 groupId** 值。

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>使用 Postman 应用测试向聊天添加的 RSC 权限

若要检查 API 请求有效负载是否接受 RSC 权限，需要将 [聊天的 RSC JSON](test-chat-rsc-json-file.md) 测试代码复制到本地环境并更新以下值：

* `azureADAppId`：应用的应用Microsoft Azure Active Directory (Azure AD) ID。
* `azureADAppSecret`：Microsoft Azure Active Directory (Azure AD) 应用密码。
* `token_scope`：获取令牌需要 范围。 将值设置为 https://graph.microsoft.com/.default。
* `tenantId`：租户的名称Microsoft Azure Active Directory (Azure AD) 对象 ID。
* `chatId`：可以从 Web 客户端获取聊天Teams *ID*，如下所示：

    1. 在 Teams Web 客户端中 **，从最** 左侧导航栏中选择"聊天"。
    2. 从下拉菜单中选择应用安装位置的聊天。
    3. 复制 Web URL，然后从字符串中保存聊天线程 ID。
![来自 Web URL 的聊天线程 ID。](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>使用 Postman

1. 打开 [Postman](https://www.postman.com) 应用。
2. 选择 **"文件** > **"** > **"导入导入** 文件"以从环境中上载更新的 JSON 文件。  
3. 选择" **集合"** 选项卡。 
4. 选择"测试 **>** **RSC** "旁边的 V 形以展开详细信息视图并查看 API 请求。

针对每个 API 调用执行整个权限集合。 在应用程序清单中指定的权限必须成功，而未指定的权限必须使用 HTTP 403 状态代码失败。 检查所有响应状态代码，确认应用中 RSC 权限的行为符合预期。

> [!NOTE]
> 若要测试特定的 DELETE 和 READ API 调用，请向 JSON 文件添加这些实例方案。

## <a name="test-revoked-rsc-permissions-using-postman"></a>使用 [Postman](https://www.postman.com/) 测试吊销的 RSC 权限

1. 从特定资源卸载应用。
2. 按照聊天或团队的步骤操作： 
    1. [使用 Postman 测试向团队添加的 RSC 权限](#test-added-rsc-permissions-to-a-team-using-the-postman-app)。
    2. [使用 Postman 测试向聊天添加的 RSC 权限](#test-added-rsc-permissions-to-a-chat-using-the-postman-app)。
3. 检查所有响应状态代码，确认特定 API 调用已失败，并 **包含 HTTP 403 状态代码**。

## <a name="see-also"></a>另请参阅

* [Microsoft Graph API 和 Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)
* [特定于资源的同意](~/graph-api/rsc/resource-specific-consent.md)
