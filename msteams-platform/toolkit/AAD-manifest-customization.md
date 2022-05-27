---
title: 在Teams Toolkit中管理Azure Active Directory应用程序
author: zyxiaoyuer
description: 介绍在Teams Toolkit中管理Azure Active Directory应用程序
ms.author: surbhigupta
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/20/2022
ms.openlocfilehash: 9ffd4e4fd8f346f49d715f2537942d02cd4892d9
ms.sourcegitcommit: d9025e959dcdd011ed4feca820dae7c5d1251b27
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65755935"
---
# <a name="azure-ad-manifest"></a>Azure AD 清单

[Azure Active Directory (Azure AD) 清单](/azure/active-directory/develop/reference-app-manifest)包含Microsoft 标识平台中 Azure AD 应用程序对象的所有属性的定义。

Teams Toolkit现在在Teams应用程序开发生命周期内，使用清单文件作为事实来源管理 Azure AD 应用程序。

## <a name="customize-azure-ad-manifest-template"></a>自定义 Azure AD 清单模板

可以自定义 Azure AD 清单模板以更新 Azure AD 应用程序。

1. 在项目中打开 `aad.template.json` 。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add template.png" alt-text="template":::

2. 直接更新模板或 [从另一个文件引用值](https://github.com/OfficeDev/TeamsFx/wiki/Manage-AAD-application-in-Teams-Toolkit#Placeholders-in-AAD-manifest-template)。 可在此处看到多个自定义方案：
  
   * [添加应用程序权限](#customize-requiredresourceaccess)
   * [预授权客户端应用程序](#customize-preauthorizedapplications)
   * [更新身份验证响应的重定向 URL](#customize-redirect-urls)

3. [为本地环境部署 Azure AD 应用程序更改](#deploy-azure-ad-application-changes-for-local-environment)。
  
4. [为远程环境部署 Azure AD 应用程序更改](#deploy-azure-ad-application-changes-for-remote-environment)。

### <a name="customize-requiredresourceaccess"></a>自定义 requiredResourceAccess

如果Teams应用程序需要更多权限才能使用其他权限调用 API，则需要更新 `requiredResourceAccess` Azure AD 清单模板中的属性。 可以查看此属性的以下示例：

```JSON

   "requiredResourceAccess": [
    {
        "resourceAppId": "Microsoft Graph",
        "resourceAccess": [
            {
                "id": "User.Read", // For Microsoft Graph API, you can also use uuid for permission id
                "type": "Scope" // Scope is for delegated permission
            },
            {
                "id": "User.Export.All",
                "type": "Role" // Role is for application permission
            }
        ]
    },
    {
        "resourceAppId": "Office 365 SharePoint Online",
        "resourceAccess": [
            {
                "id": "AllSites.Read",
                "type": "Scope"
            }
        ]
    }
]
```

* `resourceAppId`属性适用于不同的 API，用于`Microsoft Graph`并`Office 365``SharePoint Online`直接输入名称而不是 UUID，对于其他 API，请使用 UUID。

* `resourceAccess.id` 属性适用于不同的权限，用于 `Microsoft Graph` 并 `Office 365 SharePoint Online`直接输入权限名称而不是 UUID，对于其他 API，请使用 UUID。

* `resourceAccess.type` 属性用于委派权限或应用程序权限。 `Scope` 表示委派权限，表示 `Role` 应用程序权限。

### <a name="customize-preauthorizedapplications"></a>自定义 preAuthorizedApplications

可以使用 `preAuthorizedApplications` 属性授权客户端应用程序，以指示 API 信任应用程序，并且用户在客户端调用公开 API 时不同意。 可以查看此属性的以下示例：

```JSON

    "preAuthorizedApplications": [
        {
            "appId": "1fec8e78-bce4-4aaf-ab1b-5451cc387264",
            "permissionIds": [
                "{{state.fx-resource-aad-app-for-teams.oauth2PermissionScopeId}}"
            ]
        }
        ...
    ]
```

`preAuthorizedApplications.appId` 属性用于要授权的应用程序。 如果你不知道应用程序 ID，但只知道应用程序名称，则可以转到Azure 门户并按照以下步骤搜索应用程序以查找 ID：

1. 转到[Azure 门户](https://portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)并打开应用程序注册。

1. 选择 **所有应用程序** 并搜索应用程序名称。

1. 选择应用程序名称，并从概述页获取应用程序 ID。

### <a name="customize-redirect-urls"></a>自定义重定向 URL

  重定向 URL 在成功身份验证后返回身份验证响应（例如令牌）时使用。 可以使用属性 `replyUrlsWithType`自定义重定向 URL，例如，若要添加 `https://www.examples.com/auth-end.html` 为重定向 URL，可以将其添加为以下示例：

``` JSON
"replyUrlsWithType": [
    ...
    {
        "url": "https://www.examples.com/auth-end.html",
        "type": "Spa"
    }
]
```

## <a name="azure-ad-manifest-template-placeholders"></a>Azure AD 清单模板占位符

Azure AD 清单文件包含具有 {{...}} 的占位符参数 在为不同环境生成期间替换它的语句。 可以使用占位符参数生成对配置文件、状态文件和环境变量的引用。

### <a name="reference-state-file-values-in-azure-ad-manifest-template"></a>Azure AD 清单模板中的引用状态文件值

状态文件位于 `.fx\states\state.xxx.json` xxx (表示不同的环境) 。 以下示例显示了典型的状态文件：

``` JSON
{
    "solution": {
        "teamsAppTenantId": "uuid",
        ...
    },
    "fx-resource-aad-app-for-teams": {
        "applicationIdUris": "api://xxx.com/uuid",
        ...
    }
    ...
}
```

可以在 Azure AD 清单中使用此占位符参数：`{{state.fx-resource-aad-app-for-teams.applicationIdUris}}`在属性中`fx-resource-aad-app-for-teams`引用`applicationIdUris`值。

### <a name="reference-config-file-values-in-azure-ad-manifest-template"></a>Azure AD 清单模板中的引用配置文件值

配置文件位于 `.fx\configs\config.xxx.json` xxx (表示不同的环境) 。 以下示例演示配置文件：

``` JSON
{
  "$schema": "https://aka.ms/teamsfx-env-config-schema",
  "description": "description.",
  "manifest": {
    "appName": {
      "short": "app",
      "full": "Full name for app"
    }
  }
}
```

可以使用 Azure AD 清单中的占位符参数来 `{{config.manifest.appName.short}}` 引用 `short` 值。

### <a name="reference-environment-variable-in-azure-ad-manifest-template"></a>Azure AD 清单模板中的引用环境变量

有时，你不想对 Azure AD 清单模板中的值进行硬编码。 例如，当值为机密时。 Azure AD 清单模板文件支持引用环境变量值。 可以使用参数值中的语 `{{env.YOUR_ENV_VARIABLE_NAME}}` 法告诉工具解析当前环境变量的值。

## <a name="author-and-preview-azure-ad-manifest-with-code-lens"></a>使用代码镜头创作和预览 Azure AD 清单

Azure AD 清单模板文件具有要查看和编辑的代码透镜。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/preview view.png" alt-text="previewview":::

### <a name="azure-ad-manifest-template-file"></a>Azure AD 清单模板文件

在 Azure AD 清单模板文件的开头，有一个预览代码镜头。 选择代码透镜，它根据所选环境生成 Azure AD 清单。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add codelens.png" alt-text="addcodelens":::

### <a name="placeholder-argument-code-lens"></a>占位符参数代码透视

占位符参数代码透镜可帮助快速查看本地调试和开发环境的值。 如果鼠标悬停在占位符参数上，则会显示所有环境值的工具提示框。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add arguments.png" alt-text="addarguments":::

### <a name="required-resource-access-code-lens"></a>所需的资源访问代码镜头

它不同于官方 [Azure AD 清单架构](/azure/active-directory/develop/reference-app-manifest)，而`resourceAppId``resourceAccess`属性中的 `requiredResourceAccess` ID 仅支持 UUID，Teams Toolkit中的 Azure AD 清单模板也支持用户可读字符串`Microsoft Graph`和`Office 365 SharePoint Online`权限。 如果输入 UUID，代码镜头会显示用户可读字符串，否则显示 UUID。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/add resource.png" alt-text="addresource":::

### <a name="pre-authorized-applications-code-lens"></a>预授权应用程序代码透镜

代码镜头显示该属性的每个授权应用程序 ID 的 `preAuthorizedApplications` 应用程序名称。

## <a name="deploy-azure-ad-application-changes-for-local-environment"></a>为本地环境部署 Azure AD 应用程序更改

1. 在其中`aad.template.json`选择`Preview`代码透镜。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy1.png" alt-text="deploy1":::

2. 选择 `local` 环境。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy2.png" alt-text="deploy2":::

3. 在其中`aad.local.json`选择`Deploy Azure AD Manifest`代码透镜。

     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy3.png" alt-text="deploy3":::

4. 部署本地环境中使用的 Azure AD 应用程序的更改。
  
## <a name="deploy-azure-ad-application-changes-for-remote-environment"></a>为远程环境部署 Azure AD 应用程序更改

1. 打开命令面板，然后选择： `Teams: Deploy Azure Active Directory application manifest`。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy4.png" alt-text="deploy4":::

2. 还可以右键单击上下 `aad.template.json` 文菜单并从中进行选择 `Deploy Azure Active Directory application manifest` 。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add deploy5.png" alt-text="deploy5":::

## <a name="view-azure-ad-application-on-the-azure-portal"></a>在Azure 门户上查看 Azure AD 应用程序

1. 从 `state.xxx.json` (xxx 复制 Azure AD 应用程序客户端 ID 是已在属性中 `fx-resource-aad-app-for-teams` 部署 Azure AD 应用程序) 文件的环境名称。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view1.png" alt-text="view1":::

2. 转到[Azure 门户](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)并登录到Microsoft 365帐户。
  
   > [!NOTE]
   > 确保Teams应用程序和 M365 帐户的登录凭据相同。

3. 打开 [应用注册页](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)，使用之前复制的客户端 ID 搜索 Azure AD 应用程序。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view2.png" alt-text="view2":::

4. 从搜索结果中选择 Azure AD 应用程序以查看详细信息。
  
5. 在 Azure AD 应用信息页中，选择 `Manifest` 菜单以查看此应用程序的清单。 清单的架构与文件中的 `aad.template.json` 架构相同。 有关清单的详细信息，请[参阅Azure Active Directory应用程序清单](/azure/active-directory/develop/reference-app-manifest)。
  
     :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add view3.png" alt-text="view3":::

6. 可以选择 **“其他菜单** ”，通过门户查看或配置 Azure AD 应用程序。
  
## <a name="use-an-existing-azure-ad-application"></a>使用现有的 Azure AD 应用程序

可以将现有的 Azure AD 应用程序用于Teams项目，有关详细信息，请参阅[为Teams应用程序使用现有的 Azure AD 应用程序](https://github.com/OfficeDev/TeamsFx/wiki/Customize-provision-behaviors#use-an-existing-aad-app-for-your-teams-app)。

## <a name="azure-ad-application-in-teams-application-development-lifecycle"></a>Teams应用程序开发生命周期中的 Azure AD 应用程序

需要在Teams应用程序开发生命周期的各个阶段与 Azure AD 应用程序交互。

1. **创建Project**

      默认情况下，可以使用 SSO 支持附带的Teams Toolkit创建项目，例如`SSO-enabled tab`。 有关创建新应用的详细信息，请参阅[使用Teams Toolkit创建新的Teams应用程序](create-new-project.md)。 系统会自动创建 Azure AD 清单文件： `templates\appPackage\aad.template.json` Teams Toolkit在本地开发期间或将应用程序移到云时创建或更新 Azure AD 应用程序。

2. **将 SSO 添加到机器人或选项卡**

      创建没有 SSO 内置的Teams应用程序后，Teams Toolkit以增量方式帮助你为项目添加 SSO。 因此，会自动为你创建 Azure AD 清单文件： `templates\appPackage\aad.template.json`

      Teams Toolkit在下次本地调试会话期间或将应用程序移到云时创建或更新 Azure AD 应用程序。

3. **在本地生成**

    Teams Toolkit在本地开发 (（称为 F5) ）期间执行以下功能：

    * 读取文件 `state.local.json` 以查找现有的 Azure AD 应用程序。 如果 Azure AD 应用程序已存在，Teams Toolkit重新使用现有的 Azure AD 应用程序，否则需要使用该`aad.template.json`文件创建新应用程序。

    * 最初忽略清单文件中需要其他上下文 (的某些属性，例如，在创建包含清单文件的新 Azure AD 应用程序期间需要本地调试终结点) 的 replyUrls 属性。

    * 本地开发环境成功启动后，Azure AD 应用程序的标识符Uris、replyUrls 和其他在创建阶段不可用的属性会相应地更新。

    * 在下一次本地调试会话期间，将加载对 Azure AD 应用程序所做的更改。 可以看到 [Azure AD 应用程序更改](https://github.com/OfficeDev/TeamsFx/wiki/) 以手动应用更改 Azure AD 应用程序更改。

4. **预配云资源**

      将应用程序移到云时，需要预配云资源并部署应用程序。 在本地开发等阶段，Teams Toolkit将：

      * 读取文件 `state.{env}.json` 以查找现有的 Azure AD 应用程序。 如果 Azure AD 应用程序已存在，Teams Toolkit重新使用现有的 Azure AD 应用程序，否则需要使用该`aad.template.json`文件创建新应用程序。

      * 最初忽略清单文件中需要其他上下文 (的某些属性，例如 replyUrls 属性需要在创建包含清单文件的新 Azure AD 应用程序期间) 前端或机器人终结点。

      * 其他资源预配完成后，Azure AD 应用程序的标识符Uris 和 replyUrls 会相应地更新到正确的终结点。

5. **生成应用程序**

    * 部署到云命令会将应用程序部署到预配的资源。 它不包括部署你所做的 Azure AD 应用程序更改。

    * 可以看到， [为远程环境部署 Azure AD 应用程序更改](#deploy-azure-ad-application-changes-for-remote-environment) ，以便为远程环境部署 Azure AD 应用程序更改。

    * Teams Toolkit根据 Azure AD 清单模板文件更新 Azure AD 应用程序。

## <a name="limitations"></a>限制

1. Teams Toolkit扩展不支持 Azure AD 清单架构中列出的所有属性。
  
      下表列出了Teams Toolkit扩展中不支持的属性：

      |**不支持的属性**|**原因**|
      |-----------|----------|
      |passwordCredentials|清单中不允许|
      |createdDateTime|只读且无法更改|
      |logoUrl|只读且无法更改|
      |publisherDomain|只读且无法更改|
      |oauth2RequirePostResponse|图形 API中不存在|
      |oauth2AllowUrlPathMatching|图形 API中不存在|
      |samlMetadataUrl|图形 API中不存在|
      |orgRestrictions|图形 API中不存在|
      |认证|图形 API中不存在|

2. 目前 `requiredResourceAccess` ，属性只能对 `Microsoft Graph` 和 `Office 365 SharePoint Online` API 使用用户可读资源应用程序名称或权限名称字符串。 对于其他 API，需要改用 UUID。 可以按照以下步骤从Azure 门户检索 ID：

    * 在[Azure 门户](https://ms.portal.azure.com/#blade/Microsoft_AAD_IAM/ActiveDirectoryMenuBlade/RegisteredApps)上注册新的 Azure AD 应用程序。
    * 从 Azure AD 应用程序页中选择 `API permissions` 。
    * 选择此选项 `add a permission` 可添加所需的权限。
    * 从属性中`requiredResourceAccess`选择`Manifest`可以找到 API 和权限的 ID。

## <a name="see-also"></a>另请参阅

* [在Toolkit中预览和自定义应用清单](TeamsFx-preview-and-customize-app-manifest.md)
