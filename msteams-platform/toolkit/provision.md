---
title: 使用Teams Toolkit预配云资源
author: MuyangAmigo
description: 预配云资源
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: e11c66e7e818a090305e320ed21080c7ca897856
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227982"
---
# <a name="use-teams-toolkit-to-provision-cloud-resources"></a>使用Teams Toolkit预配云资源

TeamsFx 提供与 Azure 和 Microsoft 365 云的无缝集成，允许你使用单个命令将应用程序放置到 Azure 中。 TeamsFx 与 Azure 资源管理器集成，使你能够使用基础结构作为代码方法以声明方式预配应用程序所需的 Azure 资源。  

## <a name="prerequisites"></a>先决条件

* 帐户先决条件

    若要预配云资源，你必须具有以下具有适当权限的帐户。 有关详细信息，请参阅[准备帐户以生成Teams应用](accounts.md)。
    * Microsoft 365
    * 具有有效订阅的 Azure

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!TIP]
> 你应该已经拥有一个Teams VS 代码打开的应用项目。

## <a name="provision-using-teams-toolkit"></a>使用 Teams Toolkit

预配通过 Teams Toolkit 或 TeamsFx CLI Visual Studio Code单个命令执行，如下所示：

[预配基于 Azure 的应用](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8&branch)

## <a name="resource-creation"></a>资源创建

当你在 Teams Toolkit 或 TeamsFx CLI 中触发预配命令时，你可以获取以下资源：

* AAD租户下Microsoft 365应用程序
* Teams租户的 Microsoft 365 平台下注册Teams应用
* 所选 Azure 订阅下的 Azure 资源

创建新项目时，将获取要创建的所有 Azure 资源。 生成的ARM模板定义所有 Azure 资源，并帮助在预配期间创建所需的 Azure 资源。 向 [现有项目添加新功能/](./add-resource.md) 资源时，更新ARM模板反映了最新更改。

> [!NOTE]
> Azure 服务在订阅中产生成本，你可以参考定价 [计算器](https://azure.microsoft.com/pricing/calculator/) 了解估计值。

### <a name="resource-creation-for-teams-tab-application"></a>为 Teams Tab 应用程序创建资源

|资源|此资源的用途| 注释 |
|----------|--------------------------------|-----|
| Azure 存储 | 托管选项卡应用 | 启用静态 Web 应用功能以承载选项卡应用 |
| 简单身份验证的应用服务计划 | 托管简单身份验证的 Web 应用 | |
| 用于简单身份验证的 Web 应用 | 托管简单的身份验证服务器，可帮助您访问单页应用程序中的其他服务 | 添加用户分配的标识，以轻松访问其他 Azure 资源 |
| 用户分配的身份 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

### <a name="resources-created-for-teams-bot-or-messaging-extension-application"></a>为自动程序Teams邮件扩展应用程序创建的资源

|资源|此资源的用途| 注释 |
|----------|--------------------------------|-----|
| Azure Bot 服务 | 使用 Bot Framework 将应用注册为自动程序 | 将机器人连接到Teams |
| 自动程序的应用服务计划 | 托管自动程序 Web 应用 | |
| 适用于自动程序的 Web 应用 | 托管机器人应用 | 添加用户分配的标识，以轻松访问其他 Azure 资源。 <br /> 添加 [TeamsFx SDK 所需的应用设置](https://www.npmjs.com/package/@microsoft/teamsfx) |
| 用户分配的身份 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

### <a name="resources-created-when-including-azure-functions-in-the-project"></a>在将 Azure 函数包括在项目中时创建的资源

|资源|此资源的用途| 注释 |
|----------|--------------------------------|-----|
| Function App 的应用服务计划 | 托管 Function App | |
| Function App | 托管 Azure 函数 API | 添加用户分配的标识，以轻松访问其他 Azure 资源。 <br /> 添加 CORS 规则以允许来自选项卡应用的请求 <br /> 添加仅允许来自你的应用程序请求的Teams设置。 <br /> 添加 [TeamsFx SDK 所需的应用设置](https://www.npmjs.com/package/@microsoft/teamsfx) |
| Azure 存储 Function App | 创建 Function App 时必需 | |
| 用户分配的身份 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

### <a name="resources-created-when-including-azure-sql-in-the-project"></a>在将 Azure SQL项目时创建的资源

|资源|此资源的用途| 注释 |
|----------|--------------------------------|-----|
| Azure SQL Server | 托管Azure SQL 数据库实例 | 允许所有 Azure 服务访问服务器 |
| Azure SQL 数据库 | 存储应用数据 | 向用户授予对数据库的读取/写入权限 |
| 用户分配的身份 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

### <a name="resources-created-when-including-azure-api-management-in-the-project"></a>在项目中包括 Azure API 管理时创建的资源

|资源|此资源的用途|
|----------|--------------------------------|
| Azure Active Directory API 管理服务的应用程序 | 允许由 API 管理服务管理的 Microsoft Power Platform 访问 API |
| API 管理服务 | 管理在 Function App 中托管的 API |
| API 管理产品 | 对 API 进行分组，定义使用条款和运行时策略 |
| API 管理 OAuth 服务器 | 允许 Microsoft Power Platform 访问在 Function App 中托管的 API |
| 用户分配的身份 | 对 Azure 服务到服务请求进行身份验证 |

## <a name="customize-resource-provision"></a>自定义资源预配 

Teams Toolkit使用基础结构作为代码方法来定义要预配的 Azure 资源以及如何配置这些资源。 该工具使用ARM模板定义 Azure 资源。 the ARM template is a set of bicep files that defines the infrastructure and configuration for your project. 你可以自定义通过修改模板创建的 Azure ARM。 有关详细信息，请参阅 [bicep 文档](/azure/azure-resource-manager/bicep.md)。 使用 ARM涉及更改以下两组文件、参数和模板：

* ARM参数 () 位于文件夹中，用于将 `azure.parameters.{your_env_name}.json` `.fx/configs` 参数传递到模板。
* ARM位于 的模板文件 `templates/azure` ，此文件夹包含以下文件：

| 文件 | 它有什么功能 | 允许自定义 |
| --- | --- | --- |
| main.bicep | 提供 Azure 资源预配的入口点 | 是 |
| provision.bicep | 创建和配置 Azure 资源 | 是 |
| config.bicep | 将 TeamsFx 所需配置添加到 Azure 资源 | 是 |
| provision/xxx.bicep | 创建并配置使用的每个 Azure 资源 `provision.bicep` | 是 |
| teamsfx/xxx.bicep | 将 TeamsFx 所需配置添加到使用的每个 Azure 资源 `config.bicep`| 否 |

> [!NOTE]
> 向项目添加资源或功能 `teamsfx/xxx.bicep` 时，将重新生成 。 这就是它标记为不可自定义的原因。 如果确实需要修改这些 bicep 文件，我们建议使用 Git 跟踪对文件所做的更改，以便你在添加资源或功能时不会 `teamsfx/xxx.bicep` 丢失更改。

### <a name="customize-arm-parameters-and-templates"></a>自定义ARM参数和模板

可以通过自定义参数文件和自定义 bicep 文件来自定义 Azure 资源。

#### <a name="customize-arm-template-parameter-files"></a>自定义ARM模板参数文件

工具包提供了一组预定义参数，用于自定义 Azure 资源。 参数文件位于 ， `.fx/configs/azure.parameters.{env}.json` 所有可用参数均在 属性中 `provisionParameters` 定义。 如果预定义参数满足你的要求，最好自定义参数文件。

以下是可用的预定义参数列表：

| 参数名 | 默认值 | 参数可以自定义哪些内容 | 值约束 |
| --- | --- | --- | --- |
| resourceBaseName | 针对每个环境自动生成 | 所有资源的默认名称 | 2-20 个小写字母和数字 |
| simpleAuthServerFarmsName | ${resourceBaseName}simpleAuth | 简单身份验证应用服务计划的名称 | 1-40 个字母数字和连字符 |
| simpleAuthWebAppName | ${resourceBaseName}simpleAuth | 简单身份验证 Web 应用的名称 | 2-60 个字母数字和连字符 <br /> 不能以连字符开始或结束 |
| simpleAuthSku | F1 | 简单身份验证应用服务计划的 SKU |  |
| frontendHostingStorageName | ${resourceBaseName}选项卡 | 前端托管帐户存储名称 | 3-24 个小写字母和数字 |
| frontendHostingStorageSku | Standard_LRS | 前端托管帐户的 SKU 存储帐户 | 请参阅此页面 [，查看](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep&branch) 可用的 SKUS |
| functionServerfarmsName | ${resourceBaseName}api | Function App 的应用服务计划的名称 | 1-40 个字母数字和连字符 |
| functionServerfarmsSku | Y1 | FUnction 应用的应用服务计划的 SKU |
| functionAppName | ${resourceBaseName}api | Function App 的名称 | 2-60 个字母数字和连字符 <br /> 不能以连字符开始或结束 |
| functionStorageName | ${resourceBaseName}api | Function App 的帐户存储名称 | 3-24 个小写字母和数字 |
| functionStorageSku | Standard_LRS | Function App 存储 帐户的 SKU | 请参阅此页面 [，查看](/azure/templates/microsoft.storage/storageaccounts?tabs=bicep&branch=pr-en-us-4713)可用的 SKUS |
| botServiceName | ${resourceBaseName} | Azure Bot 服务的名称 | 2-64 个字母数字、下划线、句点和连字符 <br /> 从字母数字开始 |
| botServiceSku | F0 | Azure Bot 服务的 SKU | 请参阅此页面 [，查看](/azure/templates/microsoft.botservice/2021-05-01-preview/botservices?tabs=bicep&branch) 可用的 SKUS |
| botDisplayName | ${resourceBaseName} | 自动程序显示名称 | 1-42 个字符 |
| botServerfarmsName | ${resourceBaseName}bot | 自动程序的应用服务计划的名称 | 1-40 个字母数字和连字符 |
| botWebAppName | ${resourceBaseName}bot | 自动程序 Web 应用的名称 | 2-60 个字母数字和连字符 <br /> 不能以连字符开始或结束 |
| botWebAppSKU | F1 | 自动程序应用服务计划的 SKU |  |
| userAssignedIdentityName | ${resourceBaseName} | 用户分配标识的名称 | 3-128 字母数字、连字符和下划线 <br /> 以字母或数字开头 |
| sqlServerName | ${resourceBaseName} | Azure 服务SQL Server | 1-63 个小写字母、数字和连字符 <br /> 不能以连字符开始或结束 |
| sqlDatabaseName | ${resourceBaseName} | 名称Azure SQL 数据库 | 1-128 个字符，不能用于 <>*%&：？ \/ 或控制字符 <br /> 不能以时间段或空格结尾 |
| sqlDatabaseSku | 基本 | SKU Azure SQL 数据库 |  |
| apimServiceName | ${resourceBaseName} | APIM 服务的名称 | 1-50 个字母数字和连字符 <br /> 从字母开始，以字母数字结尾 |
| apimServiceSku | 消耗 | APIM 服务的 SKU | 请参阅此页面 [，查看](/azure/templates/microsoft.apimanagement/service?tabs=bicep&branch)可用的 SKUS |
| apimProductName | ${resourceBaseName} | APIM 产品的名称 | 1-80 个字母数字和连字符 <br /> 从字母开始，以字母数字结尾 |
| apimOauthServerName | ${resourceBaseName} | APIM OAuth 服务器的名称 | 1-80 个字母数字和连字符 <br /> 从字母开始，以字母数字结尾 |

同时，以下参数可用于预配期间填充的值。 这些占位符的目的是确保在创建新环境时，我们可创建新的资源。 实际值从 解析 `.fx/states/state.{env}.json` 。

##### <a name="aad-application-related-parameters"></a>AAD应用程序相关的参数

| 参数名 | 默认值位置持有者 | 位置持有者的含义 | 如何自定义 |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | 预配期间AAD创建的应用客户端 ID | 请参阅 [此部分](#use-an-existing-aad-app-for-your-teams-app) 以自定义值 |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | 预配期间AAD创建的应用客户端密码 | 请参阅 [此部分](#use-an-existing-aad-app-for-your-teams-app) 以自定义值 |
| Microsoft 365TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | 应用的应用应用租户AAD ID | 请参阅 [此部分](#use-an-existing-aad-app-for-your-teams-app) 以自定义值 |
| Microsoft 365 OauthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | 应用的应用程序应用程序 OAuth AAD主机 | 请参阅 [此部分](#use-an-existing-aad-app-for-your-teams-app) 以自定义值 |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | 自动程序AAD预配期间创建的应用客户端 ID | 请参阅 [此部分](#use-an-existing-aad-app-for-your-bot) 以自定义值 |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | 自动程序AAD预配期间创建的应用客户端密码 | 请参阅 [此部分](#use-an-existing-aad-app-for-your-bot) 以自定义值 |
| apimClientId | {{state.fx-resource-apim.apimClientAADClientId}} | APIM AAD预配期间创建的应用客户端 ID | 删除占位符并填写实际值 |
| apimClientSecret | {{state.fx-resource-apim.apimClientAADClientSecret}} | APIM AAD预配期间创建的应用客户端密码 | 删除占位符并填写实际值 |

##### <a name="azure-resource-related-parameters"></a>Azure 资源相关参数

| 参数名称 | 默认值位置持有者 | 位置持有者的含义 | 如何自定义 |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | Azure SQL Server预配期间提供的管理员帐户 | 删除占位符并填写实际值 |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | Azure SQL Server预配期间提供的管理员密码 | 删除占位符并填写实际值 |
| apimPublisherEmail | {{state.fx-resource-apim.publisherEmail}} | APIM 的发布者电子邮件，默认值是 Azure 帐户 | 删除占位符并填写实际值 |
| apimPublisherName | {{state.fx-resource-apim.publisherName}} | APIM 的发布者名称，默认值是 Azure 帐户 | 删除占位符并填写实际值 |

#### <a name="referencing-environment-variables-in-parameter-files"></a>在参数文件中引用环境变量

有时你可能不希望对参数文件中的值进行硬编码。 例如，当值是密码时。 参数文件支持引用环境变量中的值。 可以使用参数值中的语法告诉工具需要从当前环境变量 `{{$env.YOUR_ENV_VARIABLE_NAME}}` 解析该值。

下面的示例将读取环境变量 `mySelfHostedDbConnectionString` 中的参数值 `DB_CONNECTION_STRING` ：

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

#### <a name="customize-arm-template-files"></a>自定义ARM模板文件

如果预定义模板不符合应用程序要求，可以自定义文件夹ARM模板 `templates/azure` 。 例如，你可以自定义ARM模板，为应用创建一些额外的 Azure 资源。 这是一个高级方案，需要你具备用于创作模板的 bicep ARM知识。 可以从 bicep 文档 开始使用[bicep。](/azure/azure-resource-manager/bicep/?branch)
> [!NOTE]
> 该ARM模板由所有环境共享。 如果环境 [之间的预配行为不同](/azure/azure-resource-manager/bicep/conditional-resource-deployment?branch) ，可以使用条件部署。

若要确保 TeamsFx 工具正常工作，请确保自定义ARM模板满足以下要求。 如果使用其他工具进行进一步开发，可以忽略这些要求。

* 保持文件夹结构和文件名不变。 当您向项目添加更多资源/功能时，该工具可能会向现有文件追加新内容。
* 保持自动生成的参数的名称及其属性名称不变。 向项目添加更多资源/功能时，可能会使用自动生成的参数。
* 保持自动生成的模板ARM不变。 可以将其他输出添加到模板ARM模板。 输出将保留并用于其他功能，如部署、 `.fx/states/state.{env}.json` 验证清单文件等。

### <a name="customization-scenarios"></a>自定义方案

这些是你可以自定义预配行为的一些常见方案。

#### <a name="use-an-existing-aad-app-for-your-teams-app"></a>为应用AAD现有 Teams 应用

你可以将以下配置代码段添加到文件，以使用AAD为你的应用创建 `.fx/configs/config.{env}.json` 的应用程序Teams应用。 若要创建AAD应用，请参阅 <https://aka.ms/teamsfx-existing-aad-doc> 。

```json
"auth": {
    "clientId": "<your AAD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your AAD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

添加上述代码段后，将你的密码添加到相关环境变量，以便工具可以在预配期间解析实际密码。

> [!NOTE]
> 不应在多个环境中共享AAD应用程序。 如果你没有更新 AAD 应用的权限，你将会收到一条警告，说明如何手动更新AAD应用。 请按照说明在预配后更新AAD应用。

#### <a name="use-an-existing-aad-app-for-your-bot"></a>将现有AAD应用用于自动程序

你可以将以下配置代码段添加到 `.fx/configs/config.{env}.json` 文件，以使用AAD自动程序创建的应用。

```json
"bot": {
    "appId": "<your AAD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

添加上述代码段后，将你的密码添加到相关环境变量，以便工具可以在预配期间解析实际密码。

> [!NOTE]
> 不应在多个环境中共享AAD应用程序。

#### <a name="skip-adding-user-for-sql-database"></a>跳过为数据库SQL用户

有时，当工具尝试向数据库中添加用户时，SQL错误。 您可以将以下配置代码段添加到 `.fx/configs/config.{env}.json` 文件以跳过添加SQL数据库用户。

```json
"skipAddingSqlUser": true
```

### <a name="specifying-the-name-of-function-app-instance"></a>指定 Function App 实例的名称

此示例中，我将为 Function App 实例指定另一 `contosoteamsappapi` 个名称，而不是使用默认名称。

> [!NOTE]
> 如果已预配环境，指定名称将创建一个新的 Function App 实例，而不是重命名之前创建的实例。

以下步骤如下：

1. 为 `.fx/configs/azure.parameters.{env}.json` 当前环境打开。
2. 向 参数 的值 `functionAppName` 添加新属性 `provisionParameters` 。
3. 将"contosoteamsappapi"作为 `functionAppName`
4. 最后的参数文件如下所示：

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

**将其他 Azure 资源 (Azure) 添加到应用程序**

考虑此方案，你想要将Azure 存储添加到 Azure 函数后端以存储一些 blob 数据。 没有自动流来更新 bicep 模板Azure 存储支持。 但是，您可以编辑 bicep 文件并添加资源。 步骤如下

1. 创建选项卡项目
2. 向项目添加函数。 你可以访问 ["添加资源](./add-resource.md) "，了解有关添加资源有关详细信息。
3. 在模板中存储新帐户ARM帐户。 为简化，我们将直接在 中声明 `templates/azure/provision/function.bicep` 资源。 你可以自由地在其他位置声明资源。

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

4. 使用 设置 中的 Azure 存储 连接字符串更新 Azure Function App 应用程序，这是步骤 `templates/azure/provision/function.bicep` 3 中的同一文件。 将以下代码 `functionApp` 段添加到资源的 `appSettings` 数组。

    ``````````````````bicep
    {
        name: 'MyAppStorageAccountConnectionString'
        value: 'DefaultEndpointsProtocol=https;AccountName=${applicationStorageAccount.name};AccountKey=${listKeys(applicationStorageAccount.id, '2021-06-01').keys[0].value}'
    }
    ```````````````````

5. 现在，可以使用输出绑定Azure 存储函数。

## <a name="faq"></a>常见问题

<br>

<details>

<summary><b>如何排除故障？</b></summary>

如果在错误通知中Teams Toolkit错误Visual Studio Code，可以单击错误通知上的按钮 `Get Help` 以导航到相关帮助文档。如果你使用的是 TeamsFx CLI，错误消息结尾处会显示一个指向帮助文档的超链接。还可以直接查看[预配帮助](https://aka.ms/teamsfx-arm-help)文档。

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

<summary><b>如何预配基于SharePoint的应用？</b></summary>

你可以按照[基于SharePoint预配应用预配基于](/microsoftteams/platform/sbs-gs-spfx?tabs=vscode%2Cviscode&tutorial-step=4&branch)SharePoint的应用。

> [!NOTE]
> 目前，Teams使用 SharePoint 框架 生成应用Teams Toolkit与 Azure 没有直接集成，本文档中的内容不适用于基于SPFx的应用。


<br>

</details>

## <a name="see-also"></a>另请参阅

> [!div class="nextstepaction"]
> [将 Teams 应用部署到云](deploy.md)

> [!div class="nextstepaction"]
> [管理多个环境](TeamsFx-multi-env.md)

> [!div class="nextstepaction"]
> [与其他开发人员协作处理Teams项目](TeamsFx-collaboration.md)
