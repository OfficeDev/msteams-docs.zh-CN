---
title: 在 Teams 中测试特定于资源的同意权限
description: 使用 Postman 在 Teams 中测试特定于资源的同意的详细信息
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: tutorial
keywords: teams 授权 OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: 0d3d1c895c77bb417a9fdd84e319103485aa8944
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634705"
---
# <a name="test-resource-specific-consent-permissions-in-teams"></a>在 Teams 中测试特定于资源的同意权限

RSC (特定于资源的) 是 Microsoft Teams 和 Graph API 集成，使你的应用可以使用 API 终结点来管理组织内的特定团队。 有关详细信息，请参阅 [RSC](resource-specific-consent.md) (特定) — Microsoft Teams Graph API。

> [!NOTE]
> 若要测试 RSC 权限，Teams 应用清单文件必须包含填充了以下字段的 **webApplicationInfo** 密钥：
>
> - **id**：Azure AD 应用 ID，请参阅在 [Azure AD 门户中注册应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
> - **resource**：任何字符串，请参阅更新  [Teams 应用清单中的注释](resource-specific-consent.md#update-your-teams-app-manifest)
> - **应用程序权限**：应用的 RSC 权限，请参阅 [特定于资源的权限](resource-specific-consent.md#resource-specific-permissions)。

```json
"webApplicationInfo":{
      "id":"XXxxXXXXX-XxXX-xXXX-XXxx-XXXXXXXxxxXX",
      "resource":"https://AnyString",
      "applicationPermissions":[
         "Channel.Create.Group",
         "Channel.Delete.Group",
         "ChannelMessage.Read.Group",
         "ChannelSettings.Read.Group",
         "ChannelSettings.Edit.Group",
         "Member.Read.Group",
         "Owner.Read.Group",
         "TeamsApp.Read.Group",
         "TeamsTab.Read.Group",
         "TeamsTab.Create.Group",
         "TeamsTab.Edit.Group",
         "TeamsTab.Delete.Group",
         "TeamSettings.Read.Group",
         "TeamSettings.Edit.Group"
      ]
   }
```

> [!IMPORTANT]
> 在应用清单中，仅包含希望应用具有的 RSC 权限。

## <a name="test-added-rsc-permissions-using-the-postman-app"></a>使用 Postman 应用测试添加的 RSC 权限

若要检查 API 请求有效负载是否接受 RSC 权限，需要将 [RSC JSON](test-rsc-json-file.md) 测试代码复制到本地环境并更新以下值：

* `azureADAppId`：应用的 Azure AD 应用 ID
* `azureADAppSecret`：你的 Azure AD 应用密码 (密码) 
* `token_scope`：获取令牌需要范围 - 将值设置为 https://graph.microsoft.com/.default
* `teamGroupId`：可以从 Teams 客户端获取团队组 ID，如下所示：

  > [!div class="checklist"]
  >
  > * 在 Teams 客户端中 **，从** 最左侧导航栏中选择 Teams。
  > * 从下拉菜单中选择安装应用的团队。
  > * 选择" **更多选项"** 图标 (&#8943;) 
  > * 选择 **获取团队链接** 
  > * 复制并保存字符串中的 **groupId** 值。

### <a name="use-postman"></a>使用 Postman

1. 打开 [Postman](https://www.postman.com) 应用。
2. 选择 **"**  >  **文件**  >  **导入导入文件**"，从环境中上载更新的 JSON 文件。  
3. 选择" **集合"** 选项卡。 
4. 选择"测试 **>** **RSC"** 旁边的 V 形以展开详细信息视图并查看 API 请求。

针对每个 API 调用执行整个权限集合。 在应用程序清单中指定的权限必须成功，而未指定的权限必须使用 HTTP 403 状态代码失败。 检查所有响应状态代码，确认应用中 RSC 权限的行为符合预期。

> [!NOTE]
> 若要测试特定的 DELETE 和 READ API 调用，请向 JSON 文件添加这些实例方案。

## <a name="test-revoked-rsc-permissions-using-postman"></a>使用[Postman](https://www.postman.com/)测试吊销的 RSC 权限

1. 从特定团队卸载应用。
2. 按照使用 [Postman 测试添加的 RSC 权限的步骤操作](#test-added-rsc-permissions-using-the-postman-app)。
3. 检查所有响应状态代码，确认特定 API 调用已成功，但 **HTTP 403 状态代码失败**。

## <a name="see-also"></a>另请参阅

> [!div class="nextstepaction"]
> [Microsoft Graph API 和 Teams](/graph/api/resources/teams-api-overview?view=graph-rest-1.0&preserve-view=true)

