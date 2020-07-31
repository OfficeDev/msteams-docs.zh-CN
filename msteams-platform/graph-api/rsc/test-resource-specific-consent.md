---
title: 测试团队中特定于资源的同意
description: 详细信息在使用 Postman 的团队中测试特定于资源的同意
localization_priority: Normal
author: laujan
ms.author: lajanuar
ms.topic: How-to
keywords: 团队授权 OAuth SSO AAD rsc Postman Graph
ms.openlocfilehash: a7384222e5e4cba164f918186ce53b4c1b702016
ms.sourcegitcommit: 3e94edba28e9e1252b6a6ba35d4df32710dfc5d4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/31/2020
ms.locfileid: "46531264"
---
# <a name="test-resource-specific-consent-permissions--in-teams"></a>在团队中测试特定于资源的同意权限

特定于资源的同意（RSC）是 Microsoft 团队和图形 API 集成，使您的应用程序能够使用 API 终结点来管理组织中的特定团队。 请*参阅*  [特定于资源的同意（RSC）— MICROSOFT 团队 Graph API](resource-specific-consent.md)。

> [!NOTE]
>若要测试 RSC 权限，您的团队应用程序清单文件必须包含使用以下字段填充的**webApplicationInfo**项：
>
> - **id** -你的 azure ad 应用 id，*请参阅*[在 azure ad 门户中注册你的应用](resource-specific-consent.md#register-your-app-with-microsoft-identity-platform-via-the-azure-ad-portal)。
> - **resource** —任何字符串，*请参阅*[更新团队应用程序清单](resource-specific-consent.md#update-your-teams-app-manifest)中的注释
> - **应用程序权限**-您的应用程序的 RSC 权限，*请参阅*[特定于资源的权限](resource-specific-consent.md#resource-specific-permissions)。

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

>[!IMPORTANT]
>在您的应用程序清单中，仅包括您希望应用程序具有的 RSC 权限。

## <a name="test-added-rsc-permissions-using-the-postman-app"></a>测试添加了使用 Postman 应用程序的 RSC 权限

若要检查 API 请求负载是否符合 RSC 权限，需要将[RSC JSON 测试代码](test-rsc-json-file.md)复制到本地环境中并更新以下值：

1. `azureADAppId`-你的应用程序的 Azure AD 应用 id。
1. `azureADAppSecret`-你的 Azure AD 应用程序密钥（密码）
1. `token_scope`—获取令牌所需的作用域-将值设置为https://graph.microsoft.com/.default
1. `teamGroupId`—可以从团队客户端获取团队组 id，如下所示：

> [!div class="checklist"]
>
> * 在团队客户端中，从最左侧的导航栏中选择 "**团队**"。
> * 从下拉菜单中选择应用程序安装到的团队。
> * 选择 "**更多选项**" 图标（&#8943;）
> * 选择 "**获取到团队的链接**" 
> * 复制并保存字符串中的**groupId**值。

### <a name="using-postman"></a>使用 Postman

> [!div class="checklist"]
>
> * 打开[Postman](https://www.postman.com)应用程序。
> * 选择 "**文件**  =>  **导入**  =>  **导入文件**" 以从您的环境中上载更新的 JSON 文件。  
> * 选择 "**集合**" 选项卡。 
> * 选择**测试 RSC**旁边的 v 形（>）以展开详细信息视图，并查看 API 请求。

为每个 API 调用执行整个权限集。 在应用程序清单中指定的权限应成功，而未指定的权限应失败，并出现 HTTP 403 状态代码。 检查所有响应状态代码，以确认您的应用程序中的 RSC 权限行为满足预期。

>[!NOTE]
>若要测试特定的 DELETE and READ API 调用，请将这些实例方案添加到 JSON 文件中。

## <a name="test--revoked-rsc-permissions-using-postman"></a>使用[Postman](https://www.postman.com/)测试已吊销的 RSC 权限

> [!div class="checklist"]
>
> * 从特定团队中卸载应用程序。
> * 按照上述步骤[使用 Postman 添加的 RSC 权限进行测试](#test-added-rsc-permissions-using-the-postman-app)。
> * 检查所有响应状态代码，以确认成功使用 HTTP 403 状态代码的特定 API 调用失败。

> [!div class="nextstepaction"]
>
> [了解有关图形 API 和团队的详细信息](/graph/api/resources/teams-api-overview?view=graph-rest-1.0)
