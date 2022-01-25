---
title: 在应用程序内测试特定于资源的许可Teams
description: 使用 Postman 和代码示例在 Teams中测试特定于资源的同意的详细信息
ms.localizationpriority: medium
author: akjo
ms.author: lajanuar
ms.topic: tutorial
keywords: teams 授权 OAuth SSO Azure AD rsc Postman Graph
ms.openlocfilehash: fe3819b0da9783a6cf3aacac08a6045337e27600
ms.sourcegitcommit: 7209e5af27e1ebe34f7e26ca1e6b17cb7290bc06
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/25/2022
ms.locfileid: "62212480"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>在应用程序内测试特定于资源的许可Teams

> [!NOTE]
> 聊天范围的特定于资源的同意仅适用于 [公共开发人员预览](../../resources/dev-preview/developer-preview-intro.md) 版。

特定于资源的同意 (RSC) 是一种 Microsoft Teams 和 Graph API 集成，使你的应用可以使用 API 终结点来管理组织内的特定资源（团队或聊天）。 有关详细信息，请参阅[RSC](resource-specific-consent.md) (资源特定的) — Microsoft Teams Graph API。

> [!NOTE]
> 若要测试 RSC 权限，Teams清单文件必须包含填充了以下字段的 **webApplicationInfo** 密钥：
>
> - **id：Azure AD** 应用 ID，请参阅在应用 [门户中Azure AD应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-using-the-azure-ad-portal)。
> - **resource**：任何字符串，请参阅更新你的Teams [清单中的注释](resource-specific-consent.md#update-your-teams-app-manifest)。
> - **应用程序权限**：应用的 RSC 权限，请参阅 [特定于资源的权限](resource-specific-consent.md#resource-specific-permissions)。

## <a name="example-for-a-team"></a>团队示例
```json
"webApplicationInfo":{
    "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource":"https://AnyString",
    "applicationPermissions":[
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

## <a name="example-for-a-chat"></a>聊天示例
```json
"webApplicationInfo":{
    "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
    "resource":"https://AnyString",
    "applicationPermissions":[
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

> [!IMPORTANT]
> 在应用清单中，仅包含希望应用具有的 RSC 权限。

>[!NOTE]
>如果应用旨在支持在团队和聊天范围内安装，可以在 下的同一清单中指定团队和聊天权限 `applicationPermissions` 。

>如果应用旨在访问呼叫/媒体 API，则 应该Azure AD `webApplicationInfo.Id` [Azure Bot](/graph/cloud-communications-get-started#register-a-bot)服务的应用 ID。

## <a name="test-added-rsc-permissions-to-a-team-using-the-postman-app"></a>使用 Postman 应用测试向团队添加的 RSC 权限

若要检查 API 请求有效负载是否接受 RSC 权限，需要将团队的 [RSC JSON](test-team-rsc-json-file.md) 测试代码复制到本地环境并更新以下值：

* `azureADAppId`：应用的应用Azure AD ID。
* `azureADAppSecret`：Azure AD应用密码。
* `token_scope`：获取令牌需要 范围。 将值设置为 https://graph.microsoft.com/.default 。
* `teamGroupId`：可以从客户端获取团队组 id，Teams如下所示：

    1. 在Teams客户端中，Teams **左侧导航** 栏中选择"导航栏"。
    2. 从下拉菜单中选择安装应用的团队。
    3. 选择" **更多选项"** 图标 (&#8943;) 。
    4. 选择 **获取团队链接**。 
    5. 复制并保存字符串中的 **groupId** 值。

## <a name="test-added-rsc-permissions-to-a-chat-using-the-postman-app"></a>使用 Postman 应用测试向聊天添加的 RSC 权限

若要检查 API 请求有效负载是否接受 RSC 权限，需要将聊天的 [RSC JSON](test-chat-rsc-json-file.md) 测试代码复制到本地环境并更新以下值：

* `azureADAppId`：应用的应用Azure AD ID。
* `azureADAppSecret`：Azure AD应用密码。
* `token_scope`：获取令牌需要 范围。 将值设置为 https://graph.microsoft.com/.default 。
* `tenantId`：租户的名称Azure AD对象 ID。
* `chatId`：可以从 Web 客户端获取聊天Teams *ID，* 如下所示：

    1. 在 Teams客户端中 **，从最** 左侧导航栏中选择"聊天"。
    2. 从下拉菜单中选择应用安装位置的聊天。
    3. 复制 Web URL，然后从字符串中保存聊天线程 ID。
![来自 Web URL 的聊天线程 ID。](../../assets/images/chat-thread-id.png)

### <a name="use-postman"></a>使用 Postman

1. 打开 [Postman](https://www.postman.com) 应用。
2. 选择 **"**  >  **文件**  >  **导入导入文件**"，从环境中上载更新的 JSON 文件。  
3. 选择" **集合"** 选项卡。 
4. 选择"测试 **>** **RSC"** 旁边的 V 形以展开详细信息视图并查看 API 请求。

针对每个 API 调用执行整个权限集合。 在应用程序清单中指定的权限必须成功，而未指定的权限必须使用 HTTP 403 状态代码失败。 检查所有响应状态代码，确认应用中 RSC 权限的行为符合预期。

> [!NOTE]
> 若要测试特定的 DELETE 和 READ API 调用，请向 JSON 文件添加这些实例方案。

## <a name="test-revoked-rsc-permissions-using-postman"></a>使用[Postman](https://www.postman.com/)测试吊销的 RSC 权限

1. 从特定资源卸载应用。
2. 按照聊天或团队的步骤操作： 
    1. [使用 Postman 测试向团队添加了 RSC 权限](#test-added-rsc-permissions-to-a-team-using-the-postman-app)。
    2. [使用 Postman 测试向聊天添加的 RSC 权限](#test-added-rsc-permissions-to-a-chat-using-the-postman-app)。
3. 检查所有响应状态代码，确认特定 API 调用失败，并 **包含 HTTP 403 状态代码**。

## <a name="see-also"></a>另请参阅

* [Microsoft Graph API 和 Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)
* [特定于资源的同意](~/graph-api/rsc/resource-specific-consent.md)
