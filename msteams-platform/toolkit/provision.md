---
title: 使用Teams Toolkit预配云资源
author: MuyangAmigo
description: 预配云资源
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: ef087add6e69d8168a065bf52f4e265a55559755
ms.sourcegitcommit: a36760750ff4f510c374a4c956be57f7c1b4a0db
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/20/2022
ms.locfileid: "63674990"
---
# <a name="use-teams-toolkit-to-provision-cloud-resources"></a>使用Teams Toolkit预配云资源

TeamsFx 与 Azure 和 Microsoft 365 集成，这允许你使用单个命令将应用程序放置到 Azure 中。 TeamsFx 与 Azure 资源管理器集成，使你能够预配 Azure 资源，应用程序需要这些资源进行代码方法。  

## <a name="prerequisites"></a>必备条件

* 帐户先决条件 若要预配云资源，你必须具有以下帐户：

  * Microsoft 365有效订阅的帐户
  * 具有有效订阅的 Azure 有关详细信息，请参阅如何准备帐户[以生成Teams应用](accounts.md)。

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!TIP]
> 确保你已Teams VS 代码打开的应用项目。

## <a name="provision-using-teams-toolkit"></a>使用 Teams Toolkit

预配通过单个命令在 Teams Toolkit Visual Studio Code TeamsFx CLI 中执行，如下所示：

[预配基于 Azure 的应用](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8)

## <a name="resource-creation"></a>资源创建

当你在 Teams Toolkit 或 TeamsFx CLI 中触发预配命令时，你可以获取以下资源：

* Microsoft Azure Active Directory (Azure AD) 租户下Microsoft 365应用程序
* Teams租户的 Teams 平台下Microsoft 365应用注册
* 所选 Azure 订阅下的 Azure 资源

创建新项目时，可以使用所有 Azure 资源。 the ARM template defines all the Azure resources and helps to create required Azure resources during provision. 向 [现有项目添加新功能资源](./add-resource.md) 时，更新ARM模板反映了最新更改。

> [!NOTE]
> Azure 服务会在你的订阅中产生成本，有关成本估计的详细信息，请参阅 [定价计算器](https://azure.microsoft.com/pricing/calculator/)。

### <a name="resource-creation-for-teams-tab-application"></a>为 Teams Tab 应用程序创建资源

|资源|用途|说明 |
|----------|--------------------------------|-----|
| Azure 存储 | 托管选项卡应用 | 启用静态 Web 应用功能以承载选项卡应用 |
| 简单身份验证的应用服务计划 | 托管简单身份验证的 Web 应用 |不适用 |
| 用于简单身份验证的 Web 应用 | 托管简单身份验证服务器，以访问单页应用程序中的其他服务 | 添加用户分配的标识以访问其他 Azure 资源 |
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

### <a name="resource-creation-for-teams-bot-or-messaging-extension-application"></a>为自动程序Teams邮件扩展应用程序创建资源

|资源|用途| 说明 |
|----------|--------------------------------|-----|
| Azure 自动程序服务 | 使用自动程序框架将应用注册为自动程序 | 将机器人连接到Teams |
| 自动程序的应用服务计划 | 托管自动程序 Web 应用 |不适用 |
| 适用于机器人的 Web 应用 | 托管机器人应用 | 添加用户分配的标识以访问其他 Azure 资源。 <br /> 添加 [TeamsFx SDK 所需的应用设置](https://www.npmjs.com/package/@microsoft/teamsfx) |
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

### <a name="resource-creation-for-azure-functions-in-the-project"></a>项目中 Azure 函数的资源创建

|资源|用途| 说明|
|----------|--------------------------------|-----|
| 函数应用的应用服务计划 | 托管函数应用 |不适用 |
| 函数应用 | 托管 Azure 函数 API | 添加用户分配的标识以访问其他 Azure 资源。 <br /> 将跨源资源共享 (CORS) 规则以允许来自选项卡应用的请求 <br /> 添加仅允许来自你的应用程序请求的Teams设置。 <br /> 添加 [TeamsFx SDK 所需的应用设置](https://www.npmjs.com/package/@microsoft/teamsfx) |
| 函数应用的 Azure 存储 | 创建函数应用所必需 |不适用|
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

### <a name="resource-creation-for-azure-sql-in-the-project"></a>在项目中为 Azure SQL创建资源

|资源|用途 | 说明 |
|----------|--------------------------------|-----|
| Azure SQL 服务器 | 托管 Azure SQL数据库实例 | 允许所有 Azure 服务访问服务器 |
| Azure SQL 数据库 | 存储应用数据 | 授予用户分配的对数据库的标识、读取或写入权限 |
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

### <a name="resource-creation-for-azure-api-management-in-the-project"></a>项目中 Azure API 管理的资源创建

|资源|用途|
|----------|--------------------------------|
| Azure AD API 管理服务的应用程序 | 允许由 API 管理服务管理的 Microsoft Power Platform 访问 API |
| API 管理服务 | 管理函数应用中托管的 API |
| API 管理产品 | 对 API 进行分组，定义使用条款和运行时策略 |
| API 管理 OAuth 服务器 | 允许 Microsoft Power Platform 访问函数应用中托管的 API |
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 |

### <a name="resources-created-when-including-azure-key-vault-in-the-project"></a>在项目中包括 Azure Key Vault 时创建的资源

|资源|此资源的用途|
|----------|--------------------------------|
| Azure 密钥保管库服务 | 管理 (密码，例如Azure AD Azure 服务) 应用程序客户端密码 |
| 用户分配的身份 | 对 Azure 服务到服务请求进行身份验证 |

## <a name="customize-resource-provision"></a>自定义资源预配

Teams Toolkit使用基础结构作为代码方法，以定义要预配的 Azure 资源以及配置方式。 该工具使用ARM模板定义 Azure 资源。 the ARM template is a set of bicep files that defines the infrastructure and configuration for your project. 可以通过修改自定义模板来自定义 azure ARM。 有关详细信息，请参阅 [bicep 文档](/azure/azure-resource-manager/bicep.md)。

使用 ARM涉及更改以下文件、参数和模板集：

* ARM位于文件夹中 (`azure.parameters.{your_env_name}.json` `.fx/configs`) 参数文件，以将参数传递到模板。
* ARM位于 `templates/azure`的模板文件，此文件夹包含以下文件：

| 文件 | 函数 | 允许自定义 |
| --- | --- | --- |
| main.bicep | 提供 Azure 资源预配的入口点 | 是 |
| provision.bicep | 创建和配置 Azure 资源 | 是 |
| config.bicep | 将 TeamsFx 所需配置添加到 Azure 资源 | 是 |
| provision/xxx.bicep | 创建和配置使用的每个 Azure 资源 `provision.bicep` | 是 |
| teamsfx/xxx.bicep | 将 TeamsFx 所需配置添加到使用的每个 Azure 资源 `config.bicep`| 否 |

> [!NOTE]
> 向项目添加资源或功能 `teamsfx/xxx.bicep` 时，将重新生成，不能自定义相同。 若要修改 bicep 文件，可以使用 Git `teamsfx/xxx.bicep` 跟踪对文件所做的更改，这有助于你在添加资源或功能时不会丢失更改。

### <a name="customize-arm-parameters-and-templates"></a>自定义ARM参数和模板

可以通过自定义参数文件和自定义 bicep 文件来自定义 Azure 资源。

#### <a name="customize-arm-template-parameter-files"></a>自定义ARM模板参数文件

工具包提供了一组预定义参数，用于自定义 Azure 资源。 参数文件位于 ， `.fx/configs/azure.parameters.{env}.json` 所有可用参数均在 属性中 `provisionParameters` 定义。 建议在预定义参数满足你的要求时自定义参数文件。

下表提供了可用预定义参数的列表：

| 参数名称 | 默认值 | 参数可以自定义哪些内容 | 值约束 |
| --- | --- | --- | --- |
| resourceBaseName | 针对每个环境自动生成 | 所有资源的默认名称 | 2-20 个小写字母和数字 |
| simpleAuthServerFarmsName | ${resourceBaseName}simpleAuth | 简单身份验证应用服务计划的名称 | 1-40 个字母数字和连字符 |
| simpleAuthWebAppName | ${resourceBaseName}simpleAuth | 简单身份验证 Web 应用的名称 | 2-60 个字母数字和连字符 <br /> 不能以连字符开始或结束 |
| simpleAuthSku | F1 | 简单身份验证应用服务计划的 SKU | 不适用 |
| frontendHostingStorageName | ${resourceBaseName}选项卡 | 前端托管存储帐户的名称 | 3-24 个小写字母和数字 |
| frontendHostingStorageSku | Standard_LRS | 前端托管存储帐户的 SKU |[可用的 SKUS](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep)|
| functionServerfarmsName | ${resourceBaseName}api | 函数应用服务计划的名称 | 1-40 个字母数字和连字符 |
| functionServerfarmsSku | Y1 | 函数应用服务计划的 SKU | 不适用|
| functionAppName | ${resourceBaseName}api | 函数应用的名称 | 2-60 个字母数字和连字符 <br /> 不能以连字符开始或结束 |
| functionStorageName | ${resourceBaseName}api | 函数应用的存储帐户的名称 | 3-24 个小写字母和数字 |
| functionStorageSku | Standard_LRS | 函数应用存储帐户的 SKU | [可用的 SKUS](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep) |
| botServiceName | ${resourceBaseName} | Azure 自动程序服务的名称 | 2-64 个字母数字、下划线、句点和连字符 <br /> 从字母数字开始 |
| botServiceSku | F0 | Azure 自动程序服务的 SKU | [可用的 SKUS](/azure/templates/microsoft.botservice/2021-05-01-preview/botservices?tabs=bicep) |
| botDisplayName | ${resourceBaseName} | 自动程序显示名称 | 1-42 个字符 |
| botServerfarmsName | ${resourceBaseName}bot | 机器人的应用服务计划的名称 | 1-40 个字母数字和连字符 |
| botWebAppName | ${resourceBaseName}bot | 机器人 Web 应用的名称 | 2-60 个字母数字和连字符 <br /> 不能以连字符开始或结束 |
| botWebAppSKU | F1 | 自动程序应用服务计划的 SKU | 不适用 |
| userAssignedIdentityName | ${resourceBaseName} | 用户分配标识的名称 | 3-128 字母数字、连字符和下划线 <br /> 以字母或数字开头 |
| sqlServerName | ${resourceBaseName} | Azure SQL 服务器的名称 | 1-63 个小写字母、数字和连字符 <br /> 无法以连字符开始或结束 |
| sqlDatabaseName | ${resourceBaseName} | Azure SQL数据库的名称 | 1-128 个字符，不能用于 <>*%&：\/？ 或控制字符 <br /> 不能以时间段或空格结尾 |
| sqlDatabaseSku | 基本 | Azure SQL 数据库的 SKU | 不适用  |
| apimServiceName | ${resourceBaseName} | APIM 服务的名称 | 1-50 个字母数字和连字符 <br /> 从字母开始，以字母数字结尾 |
| apimServiceSku | 消耗 | APIM 服务的 SKU | [可用的 SKUS](/azure/templates/microsoft.apimanagement/service?tabs=bicep) |
| apimProductName | ${resourceBaseName} | APIM 产品的名称 | 1-80 个字母数字和连字符 <br /> 从字母开始，以字母数字结尾 |
| apimOauthServerName | ${resourceBaseName} | APIM OAuth 服务器的名称 | 1-80 个字母数字和连字符 <br /> 从字母开始，以字母数字结尾 |
| keyVaultSkuName | standard | Azure 密钥保管库服务的 SKU 名称| |

同时，以下参数可用于预配期间填充的值。 这些占位符的目的是确保我们可以在新环境中创建新的资源。 实际值从 解析。`.fx/states/state.{env}.json`

##### <a name="azure-ad-application-related-parameters"></a>Azure AD应用程序相关的参数

| 参数名称 | 默认值位置持有者 | 位置持有者的含义 | 如何自定义 |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | 预配期间Azure AD创建的应用客户端 ID | [自定义值](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | 预配期间Azure AD创建的应用客户端密码 | [自定义值](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | 应用的应用应用租户Azure AD ID | [自定义值](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | 应用的 OAuth 授权主机Azure AD应用程序 | [自定义值](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | 自动程序Azure AD预配期间创建的应用客户端 ID | [自定义值](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | 自动程序Azure AD预配期间创建的应用客户端密码 | [自定义值](#use-an-existing-azure-ad-app-for-your-bot) |
| apimClientId | {{state.fx-resource-apim.apimClientAADClientId}} | APIM Azure AD预配期间创建的应用客户端 ID | 删除占位符并填写实际值 |
| apimClientSecret | {{state.fx-resource-apim.apimClientAADClientSecret}} | APIM Azure AD预配期间创建的应用客户端密码 | 删除占位符并填写实际值 |

##### <a name="azure-resource-related-parameters"></a>Azure 资源相关参数

| 参数名称 | 默认值位置持有者 | 位置持有者的含义 | 如何自定义 |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | Azure SQL Server预配期间提供的管理员帐户 | 删除占位符并填写实际值 |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | Azure SQL Server预配期间提供的管理员密码 | 删除占位符并填写实际值 |
| apimPublisherEmail | {{state.fx-resource-apim.publisherEmail}} | APIM 的发布者电子邮件，默认值是 Azure 帐户 | 删除占位符并填写实际值 |
| apimPublisherName | {{state.fx-resource-apim.publisherName}} | APIM 的发布者名称，默认值是 Azure 帐户 | 删除占位符并填写实际值 |

#### <a name="referencing-environment-variables-in-parameter-files"></a>在参数文件中引用环境变量

如果您不想硬编码参数文件（例如，当值是机密时）中的值。 参数文件支持引用环境变量中的值。 可以使用工具的参数 `{{$env.YOUR_ENV_VARIABLE_NAME}}` 值中的语法从当前环境变量进行解析。

下面的示例从环境变量中 `mySelfHostedDbConnectionString` 读取参数的值 `DB_CONNECTION_STRING`：

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

#### <a name="customize-arm-template-files"></a>自定义ARM模板文件

如果预定义模板不符合应用程序要求，可以自定义文件夹ARM模板 `templates/azure` 。 例如，你可以自定义ARM模板，为你的应用创建一些额外的 Azure 资源。 你需要具有 bicep 语言的基本知识，该语言用于创作ARM模板。 你可以从 bicep 文档[开始。](/azure/azure-resource-manager/bicep/)

> [!NOTE]
> 该ARM模板由所有环境共享。 如果预配 [行为因](/azure/azure-resource-manager/bicep/conditional-resource-deployment) 环境而异，可以使用条件部署。

若要确保 TeamsFx 工具正常工作，请确保自定义ARM模板，这满足以下要求。 如果使用其他工具进行进一步开发，可以忽略这些要求。

* 保持文件夹结构和文件名不变。 当您向项目添加更多资源或功能时，该工具可能会向现有文件追加新内容。
* 保持自动生成的参数的名称及其属性名称不变。 向项目添加更多资源或功能时，可能会使用自动生成的参数。
* 保持自动生成的模板ARM不变。 可以将其他输出添加到模板ARM模板。 输出是 `.fx/states/state.{env}.json` 并可用于其他功能，如部署、验证清单文件。

### <a name="customization-scenarios"></a>自定义方案

您可以自定义以下方案：

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>为自动程序Azure AD现有应用

你可以将以下配置`.fx/configs/config.{env}.json`代码段添加到文件，以使用Azure AD为你的应用创建的应用Teams应用。 若要创建Azure AD应用，请参阅 <https://aka.ms/teamsfx-existing-aad-doc>。

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

添加代码段后，将你的密码添加到相关环境变量，以便该工具可以在预配期间解析实际密码。

> [!NOTE]
> 确保不要在多个环境中共享Azure AD应用程序。 如果你无权更新 Azure AD 应用，你可以收到一条警告，说明如何手动更新Azure AD应用。 按照说明在预配后更新Azure AD应用。

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>为应用Azure AD现有 Teams 应用

你可以将以下配置代码`.fx/configs/config.{env}.json`段添加到文件，以使用Azure AD自动程序创建的应用：

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

添加上述代码段后，将你的密码添加到工具的相关环境变量，以在预配期间解析实际密码。

#### <a name="skip-adding-user-for-sql-database"></a>跳过为数据库SQL用户

如果工具尝试向数据库添加用户时SQL`.fx/configs/config.{env}.json`权限错误，可以将以下配置代码段添加到文件以跳过SQL数据库用户：

```json
"skipAddingSqlUser": true
```

### <a name="specifying-the-name-of-function-app-instance"></a>指定 Function App 实例的名称

你可以将 `contosoteamsappapi` 用于函数应用实例，而不是使用默认名称。

> [!NOTE]
> 如果已预配环境，指定名称可创建新的函数应用实例，而不是重命名之前创建的实例。

以下步骤如下：

1. 为 `.fx/configs/azure.parameters.{env}.json` 当前环境打开。
2. 向 参数 的值 `functionAppName` 添加新属性 `provisionParameters`。
3. 输入 `contosoteamsappapi` 作为 `functionAppName`
4. 下面的代码片段显示了最终的参数文件：

    ```json
    {
        "$schema": "https://schema.management.azure.com/schemas/2019-04-01/deploymentParameters.json#",
        "contentVersion": "1.0.0.0",
        "parameters": {
            "provisionParameters": {
            "value": {
                "functionAppName": "contosoteamsappapi"
                ...
                }
            }
        }
    }
    ```

### <a name="scenerio"></a>Scenerio

若要将其他 Azure 资源或存储添加到应用程序：

请考虑此方案，你想要将 Azure 存储添加到 Azure 函数后端以存储 blob 数据。 没有自动流来使用 Azure 存储支持更新 bicep 模板。 但是，您可以编辑 bicep 文件并添加资源。 具体步骤如下：

1. 创建选项卡项目。
2. 向项目添加函数。 有关详细信息，请参阅 [添加资源](./add-resource.md)。
3. 在模板中声明ARM帐户。 可以直接在 中声明 `templates/azure/provision/function.bicep` 资源。 你可以自由地在其他位置声明资源。

    `````````bicep
    var applicationStorageAccountName = 'myapp${uniqueString(resourceGroup().id)}'
    resource applicationStorageAccount 'Microsoft.Storage/storageAccounts@2021-06-01' = {
        name: applicationStorageAccountName
        location: resourceGroup().location
        kind: 'Storage'
        sku: {
            name: 'Standard_LRS'
        }
    }
    `````````

4. 使用 中的 Azure 存储连接字符串更新 Azure 函数应用设置 `templates/azure/provision/function.bicep`。 将以下代码段添加到 `functionApp` 资源的 `appSettings` 数组：

    ``````````````````bicep
    {
        name: 'MyAppStorageAccountConnectionString'
        value: 'DefaultEndpointsProtocol=https;AccountName=${applicationStorageAccount.name};AccountKey=${listKeys(applicationStorageAccount.id, '2021-06-01').keys[0].value}'
    }
    ```````````````````

5. 可以使用 Azure 存储输出绑定更新函数。

## <a name="faq"></a>常见问题

<br>

<details>

<summary><b>如何排除故障？</b></summary>

如果在错误通知Teams Toolkit时Visual Studio Code错误，获取帮助选择错误通知上的"选项"以导航到相关文档。 如果你使用的是 TeamsFx CLI，错误消息末尾会显示指向帮助文档的超链接。还可以直接查看 [预配帮助](https://aka.ms/teamsfx-arm-help) 文档。

<br>

</details>

<details>

<summary><b>如何在预配时切换到其他 Azure 订阅？</b></summary>

1. 切换当前帐户中的订阅或注销并选择新订阅。
2. 如果已预配当前环境，则需要创建新环境并执行预配，因为ARM不支持移动资源。
3. 如果未预配当前环境，可以直接触发预配。

<br>

</details>

<details>

<summary><b>如何在预配时更改资源组？</b></summary>

预配之前，该工具会询问你是要创建新资源组还是使用现有资源组。 可以在此步骤中提供一个新的资源组名称或选择现有的资源组名称。

<br>

</details>

<details>

<summary><b>如何预配基于 sharepoint 的应用程序？</b></summary>

你可以遵循[基于SharePoint应用的预配](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4)。

> [!NOTE]
> 目前，Teams sharepoint 框架和 Teams Toolkit 构建的应用程序没有与 Azure 的直接集成，文档内容不适用于基于 SPFx 的应用。

<br>

</details>

## <a name="see-also"></a>另请参阅

* [将 Teams 应用部署到云](deploy.md)
* [管理多个环境](TeamsFx-multi-env.md)
* [在 Teams 项目中与其他开发人员协作](TeamsFx-collaboration.md)
