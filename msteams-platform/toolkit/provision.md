---
title: 使用 Teams 工具包预配云资源
author: MuyangAmigo
description: 预配云资源
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 24b058957ab0db7ebd2ab9178ac95fe9473257e6
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104117"
---
# <a name="use-teams-toolkit-to-provision-cloud-resources"></a>使用 Teams 工具包预配云资源

TeamsFx 与 Azure 和Microsoft 365云集成，使你可以使用单个命令将应用程序放置在 Azure 中。 TeamsFx 与 Azure 资源管理器集成，使你能够预配 Azure 资源，而应用程序需要这些资源来使用代码方法。  

## <a name="prerequisites"></a>先决条件

* 帐户先决条件若要预配云资源，必须具有以下帐户：

  * Microsoft 365具有有效订阅的帐户
  * 具有有效订阅的 Azure 有关详细信息，请参阅[如何准备用于生成Teams应用的帐户](accounts.md)。

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!TIP]
> 确保已在 VS 代码中打开Teams应用项目。

## <a name="provision-using-teams-toolkit"></a>使用Teams Toolkit进行预配

在 Teams Toolkit 中为 Visual Studio Code 或 TeamsFx CLI 执行预配，如下所示：

[预配基于 Azure 的应用](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8)

## <a name="resource-creation"></a>资源创建

在 Teams Toolkit 或 TeamsFx CLI 中触发预配命令时，可以获取以下资源：

* Microsoft Azure Active Directory (Azure AD) Microsoft 365租户下的应用程序
* 在Microsoft 365租户的Teams平台下Teams应用注册
* 所选 Azure 订阅下的 Azure 资源

创建新项目时，可以使用所有 Azure 资源。 ARM 模板定义所有 Azure 资源，并有助于在预配期间创建所需的 Azure 资源。 将 [新功能资源添加](./add-resource.md) 到现有项目时，更新的 ARM 模板将反映最新更改。

> [!NOTE]
> Azure 服务会在订阅中产生成本，有关成本估算的详细信息，请参阅 [定价计算器](https://azure.microsoft.com/pricing/calculator/)。

### <a name="resource-creation-for-teams-tab-application"></a>为 Teams Tab 应用程序创建资源

|Resource|用途|说明 |
|----------|--------------------------------|-----|
| Azure 存储 | 托管选项卡应用 | 启用静态 Web 应用功能来托管选项卡应用 |
| 简单身份验证的应用服务计划 | 托管简单身份验证的 Web 应用 |不适用 |
| 用于简单身份验证的 Web 应用 | 托管简单身份验证服务器以访问单页应用程序中的其他服务 | 添加用户分配的标识以访问其他 Azure 资源 |
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

### <a name="resource-creation-for-teams-bot-or-message-extension-application"></a>为Teams机器人或消息扩展应用程序创建资源

|Resource|用途| 说明 |
|----------|--------------------------------|-----|
| Azure 机器人服务 | 将应用注册为机器人框架 | 将机器人连接到Teams |
| 机器人的应用服务计划 | 托管机器人的 Web 应用 |不适用 |
| 机器人的 Web 应用 | 托管机器人应用 | 添加用户分配的标识以访问其他 Azure 资源。 <br /> 添加 [TeamsFx SDK](https://www.npmjs.com/package/@microsoft/teamsfx) 所需的应用设置 |
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

### <a name="resource-creation-for-azure-functions-in-the-project"></a>为项目中的Azure Functions创建资源

|Resource|用途| 说明|
|----------|--------------------------------|-----|
| 函数应用的应用服务计划 | 托管函数应用 |不适用 |
| 函数应用 | 托管 Azure 函数 API | 添加用户分配的标识以访问其他 Azure 资源。 <br /> 添加跨源资源共享 (CORS) 规则以允许来自选项卡应用的请求 <br /> 添加仅允许来自Teams应用的请求的身份验证设置。 <br /> 添加 [TeamsFx SDK](https://www.npmjs.com/package/@microsoft/teamsfx) 所需的应用设置 |
| 用于函数应用的 Azure 存储 | 创建函数应用所需的 |不适用|
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

### <a name="resource-creation-for-azure-sql-in-the-project"></a>为项目中Azure SQL创建资源

|Resource|用途 | 说明 |
|----------|--------------------------------|-----|
| Azure SQL服务器 | 托管Azure SQL数据库实例 | 允许所有 Azure 服务访问服务器 |
| Azure SQL 数据库 | 存储应用的数据 | 向用户授予对数据库的标识、读取或写入权限 |
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

### <a name="resource-creation-for-azure-api-management-in-the-project"></a>在项目中为 Azure API 管理创建资源

|Resource|用途|
|----------|--------------------------------|
| Azure AD API 管理服务的应用程序 | 允许 Microsoft Power Platform 访问 API 管理服务管理的 API |
| API 管理服务 | 管理函数应用中托管的 API |
| API 管理产品 | 对 API 进行分组，定义使用条款和运行时策略 |
| API 管理 OAuth 服务器 | 使 Microsoft Power Platform 能够访问函数应用中托管的 API |
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 |

### <a name="resources-created-when-including-azure-key-vault-in-the-project"></a>在项目中包括 Azure 密钥保管库时创建的资源

|资源|此资源的用途|
|----------|--------------------------------|
| Azure 密钥保管库服务 | 管理机密 (，Azure AD其他 Azure 服务使用的应用客户端机密)  |
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 |

## <a name="customize-resource-provision"></a>自定义资源预配

Teams Toolkit使你能够使用基础结构作为代码方法来定义要预配的 Azure 资源以及要配置的方式。 该工具使用 ARM 模板来定义 Azure 资源。 ARM 模板是一组 bicep 文件，用于定义项目的基础结构和配置。 可以通过修改 ARM 模板来自定义 Azure 资源。 有关详细信息，请参阅 [bicep 文档](/azure/azure-resource-manager/bicep)。

使用 ARM 进行预配涉及更改以下文件、参数和模板集：

* ARM 参数文件 (`azure.parameters.{your_env_name}.json` 位于文件夹) `.fx/configs` ，用于将参数传递给模板。
* ARM 模板文件位于此文件夹中 `templates/azure`，其中包含以下文件：

| 文件 | 函数 | 允许自定义 |
| --- | --- | --- |
| main.bicep | 为 Azure 资源预配提供入口点 | 是 |
| provision.bicep | 创建和配置 Azure 资源 | 是 |
| config.bicep | 将 TeamsFx 所需的配置添加到 Azure 资源 | 是 |
| provision/xxx.bicep | 创建和配置所使用的每个 Azure 资源 `provision.bicep` | 可访问 |
| teamsfx/xxx.bicep | 将 TeamsFx 所需的配置添加到所使用的每个 Azure 资源 `config.bicep`| 否 |

> [!NOTE]
> 将资源或功能添加到项目时， `teamsfx/xxx.bicep` 将重新生成，不能自定义相同的资源或功能。 若要修改 bicep 文件，可以使用 Git 跟踪对文件所做的更改 `teamsfx/xxx.bicep` ，这有助于在添加资源或功能时不丢失更改。

### <a name="customize-arm-parameters-and-templates"></a>自定义 ARM 参数和模板

可以通过自定义参数文件并自定义 bicep 文件来自定义 Azure 资源。

#### <a name="customize-arm-template-parameter-files"></a>自定义 ARM 模板参数文件

该工具包提供一组预定义参数，供你自定义 Azure 资源。 参数文件位于 `.fx/configs/azure.parameters.{env}.json` 该位置，并且在属性中 `provisionParameters` 定义了所有可用参数。 如果预定义的参数满足你的要求，建议自定义参数文件。

下表提供了可用预定义参数的列表：

| 参数名称 | 默认值 | 参数可以自定义的内容 | 值约束 |
| --- | --- | --- | --- |
| resourceBaseName | 为每个环境自动生成 | 所有资源的默认名称 | 2-20 个小写字母和数字 |
| simpleAuthServerFarmsName | ${resourceBaseName}simpleAuth | 简单身份验证应用服务计划的名称 | 1-40 字母数字和连字符 |
| simpleAuthWebAppName | ${resourceBaseName}simpleAuth | 简单身份验证 Web 应用的名称 | 2-60 字母数字和连字符 <br /> 无法以连字符开头或结尾 |
| simpleAuthSku | F1 | 简单身份验证应用服务计划的 SKU | 不适用 |
| frontendHostingStorageName | ${resourceBaseName}选项卡 | 前端托管存储帐户的名称 | 3-24 小写字母和数字 |
| frontendHostingStorageSku | Standard_LRS | 前端托管存储帐户的 SKU |[可用 SKU](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep)|
| functionServerfarmsName | ${resourceBaseName}api | 函数应用服务计划的名称 | 1-40 字母数字和连字符 |
| functionServerfarmsSku | Y1 | 函数应用服务计划的 SKU | 不适用|
| functionAppName | ${resourceBaseName}api | 函数应用的名称 | 2-60 字母数字和连字符 <br /> 无法以连字符开头或结尾 |
| functionStorageName | ${resourceBaseName}api | 函数应用的存储帐户的名称 | 3-24 小写字母和数字 |
| functionStorageSku | Standard_LRS | 函数应用存储帐户的 SKU | [可用 SKU](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep) |
| botServiceName | ${resourceBaseName} | Azure 机器人服务的名称 | 2-64 字母数字、下划线、句点和连字符 <br /> 以字母数字开头 |
| botServiceSku | F0 | Azure 机器人服务的 SKU | [可用 SKU](/azure/templates/microsoft.botservice/2021-05-01-preview/botservices?tabs=bicep) |
| botDisplayName | ${resourceBaseName} | 机器人的显示名称 | 1-42 个字符 |
| botServerfarmsName | ${resourceBaseName}机器人 | 机器人应用服务计划的名称 | 1-40 字母数字和连字符 |
| botWebAppName | ${resourceBaseName}机器人 | 机器人 Web 应用的名称 | 2-60 字母数字和连字符 <br /> 无法以连字符开头或结尾 |
| botWebAppSKU | F1 | 机器人App 服务计划的 SKU | 不适用 |
| userAssignedIdentityName | ${resourceBaseName} | 用户分配标识的名称 | 3-128 字母数字、连字符和下划线 <br /> 以字母或数字开头 |
| sqlServerName | ${resourceBaseName} | Azure SQL服务器的名称 | 1-63 个小写字母、数字和连字符 <br /> 无法以连字符开头或结尾 |
| sqlDatabaseName | ${resourceBaseName} | Azure SQL数据库的名称 | 1-128 个字符，不能使用 <>*%&：\/？ 或控制字符 <br /> 不能以句点或空间结束 |
| sqlDatabaseSku | 基本 | Azure SQL数据库的 SKU | 不适用  |
| apimServiceName | ${resourceBaseName} | APIM 服务的名称 | 1-50 字母数字和连字符 <br /> 以字母开头，以字母数字结尾 |
| apimServiceSku | 消费 | APIM 服务的 SKU | [可用 SKU](/azure/templates/microsoft.apimanagement/service?tabs=bicep) |
| apimProductName | ${resourceBaseName} | APIM 产品的名称 | 1-80 字母数字和连字符 <br /> 以字母开头，以字母数字结尾 |
| apimOauthServerName | ${resourceBaseName} | APIM OAuth 服务器的名称 | 1-80 字母数字和连字符 <br /> 以字母开头，以字母数字结尾 |
| keyVaultSkuName | 标准 | Azure 密钥保管库服务的 SKU 名称| |

同时，以下参数在预配期间填充了值。 这些占位符的目的是确保我们可以在新环境中为你创建新资源。 实际值已从 `.fx/states/state.{env}.json`中解析。

##### <a name="azure-ad-application-related-parameters"></a>Azure AD应用程序相关的参数

| 参数名称 | 默认值放置者 | 位置持有人的含义 | 如何自定义 |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | 在预配期间创建的应用Azure AD应用客户端 ID | [自定义值](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | 在预配期间创建的应用Azure AD应用客户端机密 | [自定义值](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | 应用Azure AD应用的租户 ID | [自定义值](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | 应用Azure AD应用的 OAuth 颁发机构主机 | [自定义值](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | 预配期间创建的机器人Azure AD应用客户端 ID | [自定义值](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | 在预配期间创建的机器人Azure AD应用客户端机密 | [自定义值](#use-an-existing-azure-ad-app-for-your-bot) |
| apimClientId | {{state.fx-resource-apim.apimClientAADClientId}} | 在预配期间创建的 APIM Azure AD应用客户端 ID | 删除占位符并填写实际值 |
| apimClientSecret | {{state.fx-resource-apim.apimClientAADClientSecret}} | 在预配期间创建的 APIM Azure AD应用客户端机密 | 删除占位符并填写实际值 |

##### <a name="azure-resource-related-parameters"></a>与 Azure 资源相关的参数

| 参数名称 | 默认值放置者 | 位置持有人的含义 | 如何自定义 |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | Azure SQL预配期间提供的服务器管理员帐户 | 删除占位符并填写实际值 |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | Azure SQL预配期间提供的服务器管理员密码 | 删除占位符并填写实际值 |
| apimPublisherEmail | {{state.fx-resource-apim.publisherEmail}} | APIM 的发布者电子邮件，默认值为 Azure 帐户 | 删除占位符并填写实际值 |
| apimPublisherName | {{state.fx-resource-apim.publisherName}} | APIM 的发布者名称，默认值为 Azure 帐户 | 删除占位符并填写实际值 |

#### <a name="referencing-environment-variables-in-parameter-files"></a>引用参数文件中的环境变量

如果不想对参数文件中的值进行硬编码，例如，当值为机密时。 参数文件支持引用环境变量中的值。 可以对工具使用参数值中的语 `{{$env.YOUR_ENV_VARIABLE_NAME}}` 法从当前环境变量解析。

以下示例从环境变量`DB_CONNECTION_STRING`中读取参数的`mySelfHostedDbConnectionString`值：

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

#### <a name="customize-arm-template-files"></a>自定义 ARM 模板文件

如果预定义的模板不符合应用程序要求，则可以自定义文件夹下 `templates/azure` 的 ARM 模板。 例如，可以自定义 ARM 模板，为应用创建一些额外的 Azure 资源。 你需要具备 bicep 语言的基本知识，该语言用于创作 ARM 模板。 可以在 bicep 文档中开始使用 [bicep](/azure/azure-resource-manager/bicep/)。

> [!NOTE]
> ARM 模板由所有环境共享。 如果预配行为在环境之间有所不同，则可以使用 [条件部署](/azure/azure-resource-manager/bicep/conditional-resource-deployment) 。

若要确保 TeamsFx 工具正常运行，请确保自定义符合以下要求的 ARM 模板。 如果使用其他工具进行进一步开发，则可以忽略这些要求。

* 保持文件夹结构和文件名不变。 向项目添加更多资源或功能时，该工具可能会将新内容追加到现有文件。
* 保持自动生成参数的名称及其属性名称不变。 向项目添加更多资源或功能时，可以使用自动生成的参数。
* 保持自动生成的 ARM 模板的输出保持不变。 可以将其他输出添加到 ARM 模板。 输出现在 `.fx/states/state.{env}.json` 和可以用于其他功能，例如部署、验证清单文件。

### <a name="customization-scenarios"></a>自定义方案

可以自定义以下方案：

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>为机器人使用现有的Azure AD应用

可以将以下配置代码片段添加到`.fx/configs/config.{env}.json`文件中，以使用自己为Teams应用创建的Azure AD应用。 若要创建Azure AD应用，请参阅<https://aka.ms/teamsfx-existing-aad-doc>。

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

添加代码段后，将机密添加到相关环境变量，以便该工具可以在预配期间解析实际机密。

> [!NOTE]
> 确保不要在多个环境中共享同一Azure AD应用。 如果没有权限更新Azure AD应用，则可以收到有关如何手动更新Azure AD应用的说明的警告。 按照说明在预配后更新Azure AD应用。

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>对Teams应用使用现有的Azure AD应用

可以将以下配置代码片段添加到`.fx/configs/config.{env}.json`文件中，以使用自己为机器人创建的Azure AD应用：

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

添加上述代码片段后，将机密添加到相关环境变量，以便在预配期间解析实际机密。

#### <a name="skip-adding-user-for-sql-database"></a>跳过为SQL数据库添加用户

如果在工具尝试将用户添加到SQL数据库时权限不足，可以将以下配置代码片段添加到`.fx/configs/config.{env}.json`文件，以跳过添加SQL数据库用户：

```json
"skipAddingSqlUser": true
```

### <a name="specifying-the-name-of-function-app-instance"></a>指定 Function App 实例的名称

可以用于 `contosoteamsappapi` 函数应用实例，而不是使用默认名称。

> [!NOTE]
> 如果已预配环境，则指定名称可以为你创建新的函数应用实例，而不是重命名之前创建的实例。

以下步骤包括：

1. 打开 `.fx/configs/azure.parameters.{env}.json` 当前环境。
2. 向参数`provisionParameters`值添加新属性`functionAppName`。
3. 输入 `contosoteamsappapi` 为值 `functionAppName`
4. 最终参数文件显示在以下代码片段中：

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

若要将其他 Azure 资源或存储添加到应用程序，请执行以下操作：

考虑这种情况，需要将 Azure 存储添加到 Azure 函数后端以存储 Blob 数据。 没有自动流来使用 Azure 存储支持来更新 bicep 模板。 但是，可以编辑 bicep 文件并添加资源。 具体步骤如下：

1. 创建选项卡项目。
2. 向项目添加函数。 有关详细信息，请参阅 [添加资源](./add-resource.md)。
3. 在 ARM 模板中声明新的存储帐户。 可以直接声明 `templates/azure/provision/function.bicep` 资源。 你可以在其他位置自由声明资源。

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

4. 使用 Azure 存储连接字符串 `templates/azure/provision/function.bicep`更新 Azure 函数应用设置。 将以下代码片段添加到 `functionApp` 资源的 `appSettings` 数组：

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

<summary><b>如何进行故障排除？</b></summary>

如果在Visual Studio Code中出现Teams Toolkit错误，则可以在错误通知中选择 **获取帮助** 以导航到相关文档。 如果使用的是 TeamsFx CLI，则错误消息末尾会有一个指向帮助文档的超链接。还可以直接查看 [预配帮助文档](https://aka.ms/teamsfx-arm-help) 。

<br>

</details>

<details>

<summary><b>如何在预配时切换到另一个 Azure 订阅？</b></summary>

1. 在当前帐户中切换订阅或注销并选择新订阅。
2. 如果已预配当前环境，则需要创建新环境并执行预配，因为 ARM 不支持移动资源。
3. 如果未预配当前环境，可以直接触发预配。

<br>

</details>

<details>

<summary><b>如何在预配时更改资源组？</b></summary>

在预配之前，该工具会询问是要创建新的资源组还是使用现有资源组。 可在此步骤中提供新的资源组名称或选择现有资源组名称。

<br>

</details>

<details>

<summary><b>如何预配基于 sharepoint 的应用？</b></summary>

可以遵循[基于SharePoint的应用的预配](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4)。

> [!NOTE]
> 目前，使用 sharepoint 框架构建Teams应用与Teams Toolkit没有与 Azure 的直接集成，文档中的内容不适用于基于SPFx的应用。

<br>

</details>

## <a name="see-also"></a>另请参阅

* [将 Teams 应用部署到云](deploy.md)
* [管理多个环境](TeamsFx-multi-env.md)
* [在 Teams 项目中与其他开发人员协作](TeamsFx-collaboration.md)
