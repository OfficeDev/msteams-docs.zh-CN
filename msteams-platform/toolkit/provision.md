---
title: 使用 Teams 工具包预配云资源
author: MuyangAmigo
description: 在本模块中，了解如何使用 Teams 工具包、资源创建和自定义资源预配来预配云资源
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 1c7ec89accf7173be07eea742576b920ab47ee4d
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616987"
---
# <a name="provision-cloud-resources"></a>预配云资源

TeamsFx 与 Azure 和 Microsoft 365 云进行了集成，因此你可以使用单个命令将应用程序放置在 Azure 中。 TeamsFx 与 Azure 资源管理器进行了集成，因此你能够预配应用程序在使用代码方法时所需的 Azure 资源。

## <a name="provision-using-teams-toolkit"></a>使用 Teams 工具包进行预配

预配是使用 Teams Toolkit 中用于 Visual Studio Code 或 TeamsFx CLI 的单个命令执行的。 有关详细信息，请参阅 [预配基于 Azure 的应用](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8)

## <a name="create-resources"></a>创建资源

在 Teams 工具包或 TeamsFx CLI 中触发预配命令时，可以获取以下资源：

* Microsoft Azure Active Directory (Microsoft 365 租户下的 Azure AD) 应用程序。
* Microsoft 365 租户的 Teams 平台下的 Teams 应用注册。
* 所选 Azure 订阅下的 Azure 资源。

创建新项目时，可以使用所有 Azure 资源。 ARM 模板可定义所有 Azure 资源，并有助于在预配期间创建所需的 Azure 资源。 向现有项目[添加新功能资源](./add-resource.md)时，更新的 ARM 模板将反映最新更改。

> [!NOTE]
> Azure 服务会在订阅中产生费用，有关费用估算的详细信息，请参阅[定价计算器](https://azure.microsoft.com/pricing/calculator/)。

以下列表显示了为不同类型的应用和 Azure 资源创建资源：
<br>

<details>
<summary><b>为 Teams 选项卡应用程序创建资源</b></summary>

|Resource|用途|说明 |
|----------|--------------------------------|-----|
| Azure 存储 | 托管选项卡应用 | 启用静态 Web 应用功能来托管选项卡应用 |
| 用于支持简单身份验证的应用服务计划 | 托管简单身份验证的 Web 应用 |不适用 |
| 用于支持简单身份验证的 Web 应用 | 托管简单身份验证服务器，以获得对单页应用程序中的其他服务的访问权限 | 添加用户分配的标识，以访问其他 Azure 资源 |
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

</details>
<br>

<details>
<summary><b>为 Teams 机器人或消息扩展应用程序创建资源</b></summary>

|Resource|用途| 说明 |
|----------|--------------------------------|-----|
| Azure 机器人服务 | 将应用注册为采用机器人框架的机器人 | 将机器人连接到 Teams |
| 针对机器人的应用服务计划 | 托管机器人的 Web 应用 |不适用 |
| 针对机器人的 Web 应用 | 托管机器人应用 | 添加用户分配的标识，以访问其他 Azure 资源。 <br /> 添加 [TeamsFx SDK](https://www.npmjs.com/package/@microsoft/teamsfx) 所需的应用设置 |
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

</details>
<br>

<details>
<summary><b>为项目中的 Azure Functions 创建资源</b></summary>

|Resource|用途| 说明|
|----------|--------------------------------|-----|
| 针对函数应用的应用服务计划 | 托管函数应用 |不适用 |
| 函数应用 | 托管 Azure Functions API | 添加用户分配的标识，以访问其他 Azure 资源。 <br /> 添加跨源资源共享 (CORS) 规则，以允许来自选项卡应用的请求 <br /> 添加仅允许来自 Teams 应用的请求的身份验证设置。 <br /> 添加 [TeamsFx SDK](https://www.npmjs.com/package/@microsoft/teamsfx) 所需的应用设置 |
| 用于函数应用的 Azure 存储 | 创建函数应用时需要用到 |不适用|
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

</details>
<br>

<details>
<summary><b>为项目中的 Azure SQL 创建资源</b></summary>

|Resource|用途 | 说明 |
|----------|--------------------------------|-----|
| Azure SQL 服务器 | 托管 Azure SQL 数据库实例 | 允许所有 Azure 服务访问服务器 |
| Azure SQL 数据库 | 存储应用的数据 | 授予对数据库的用户分配的标识、读取或写入权限 |
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 | 跨不同功能和资源共享 |

</details>
<br>

<details>
<summary><b>为项目中的 Azure API 管理创建资源</b></summary>

|Resource|用途|
|----------|--------------------------------|
| 适用于 API 管理服务的 Azure AD 应用程序 | 允许 Microsoft Power Platform 访问由 API 管理服务管理的 API |
| API 管理服务 | 管理函数应用中托管的 API |
| API 管理产品 | 对 API 进行分组，定义使用条款和运行时策略 |
| API 管理 OAuth 服务器 | 使 Microsoft Power Platform 能够访问函数应用中托管的 API |
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 |

</details>
<br>

<details>
<summary><b>在项目中包括 Azure 密钥保管库时创建的资源</b></summary>

|资源|此资源的用途|
|----------|--------------------------------|
| Azure 密钥保管库服务 | 管理其他 Azure 服务使用的密码（例如 Azure AD 应用客户端密码） |
| 用户分配的标识 | 对 Azure 服务到服务请求进行身份验证 |

</details>
<br>

## <a name="customize-resource-provision"></a>自定义资源预配

使用 Teams 工具包，可以使用基础结构即代码方法来定义要预配的 Azure 资源以及要配置的方式。 该工具使用 ARM 模板来定义 Azure 资源。 ARM 模板是一组 bicep 文件，用于定义项目的基础结构和配置。 你可以通过修改 ARM 模板来自定义 Azure 资源。 有关详细信息，请参阅 [bicep 文档](/azure/azure-resource-manager/bicep)。

使用 ARM 进行预配涉及更改以下几套文件、参数和模板：

* ARM 参数文件 (`azure.parameters.{your_env_name}.json`)，位于文件夹 `.fx/configs` 内，用于将参数传递给模板。
* ARM 模板文件，位于 `templates/azure` 中，此文件夹中包含以下文件：

| 文件 | 函数 | 允许自定义 |
| --- | --- | --- |
| main.bicep | 为 Azure 资源预配提供入口点 | 是 |
| provision.bicep | 创建和配置 Azure 资源 | 是 |
| config.bicep | 将 TeamsFx 所需的配置添加到 Azure 资源 | 是 |
| provision/xxx.bicep | 创建和配置 `provision.bicep` 所使用的每个 Azure 资源 | 可访问 |
| teamsfx/xxx.bicep | 将 TeamsFx 所需的配置添加到 `config.bicep` 所使用的每个 Azure 资源| 否 |

> [!NOTE]
> 将资源或功能添加到项目时，`teamsfx/xxx.bicep` 将重新生成，请勿自定义相同的内容。 若要修改 bicep 文件，可以使用 Git 跟踪对 `teamsfx/xxx.bicep` 文件所做的更改，这有助于在添加资源或功能时不丢失更改。

### <a name="azure-ad-parameters"></a>Azure AD 参数

ARM 模板文件使用参数的占位符。 这些占位符的目的是确保在新环境中为你创建新资源。 实际值将从 `.fx/states/state.{env}.json` 中解析得到。

有两种类型的参数，例如与 Azure AD 应用程序相关的参数和与 Azure 资源相关的参数。

##### <a name="azure-ad-application-related-parameters"></a>Azure AD 应用程序相关的参数

| 参数名称 | 默认值占位符 | 占位符的含义 | 如何自定义 |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | 在预配期间为你的应用的 Azure AD 应用创建的客户端 ID | [为机器人使用现有的 Azure AD 应用](#use-an-existing-azure-ad-app-for-your-bot) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | 在预配期间为你的应用的 Azure AD 应用创建的客户端密码 | [为 Teams 应用使用现有的 Azure AD 应用](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | 你的应用的 Azure AD 应用的租户 ID | [为 Teams 应用使用现有的 Azure AD 应用](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | 你的应用的 Azure AD 应用的 OAuth 颁发机构主机 | [为 Teams 应用使用现有的 Azure AD 应用](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | 在预配期间创建的机器人 Azure AD 应用客户端 ID | [为机器人使用现有的 Azure AD 应用](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | 在预配期间创建的机器人 Azure AD 应用客户端密码 | [为机器人使用现有的 Azure AD 应用](#use-an-existing-azure-ad-app-for-your-bot) |

##### <a name="azure-resource-related-parameters"></a>与 Azure 资源相关的参数

| 参数名称 | 默认值占位符 | 占位符的含义 | 如何自定义 |
| --- | --- | --- | --- |
| azureSqlAdmin | {{state.fx-resource-azure-sql.admin}} | 你在预配期间提供的 Azure SQL 服务器管理员帐户 | 删除占位符并填写实际值 |
| azureSqlAdminPassword | {{state.fx-resource-azure-sql.adminPassword}} | 你在预配期间提供的 Azure SQL 服务器管理员密码 | 删除占位符并填写实际值 |

#### <a name="referencing-environment-variables-in-parameter-files"></a>在参数文件中引用环境变量

如果不想对参数文件中的值进行硬编码（例如，当值是密码时）， 参数文件支持引用环境变量中的值。 你可以在参数值中使用语法 `{{$env.YOUR_ENV_VARIABLE_NAME}}`，以便工具从当前环境变量进行解析。

以下示例将从环境变量 `DB_CONNECTION_STRING` 中读取参数 `mySelfHostedDbConnectionString` 的值：

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

#### <a name="customize-arm-template-files"></a>自定义 ARM 模板文件

如果预定义的模板不符合应用程序要求，你可以自定义文件夹 `templates/azure` 下的 ARM 模板。 例如，可以自定义 ARM 模板，为应用创建一些额外的 Azure 资源。 你需要具备有关 bicep 语言的基本知识，该语言用于创作 ARM 模板。 你可以参阅 [bicep 文档](/azure/azure-resource-manager/bicep/)，开始使用 bicep。

> [!NOTE]
> ARM 模板由所有环境共享。 如果预配行为在环境之间有所不同，则可以使用[条件部署](/azure/azure-resource-manager/bicep/conditional-resource-deployment)。

若要确保 TeamsFx 工具正常运行，请确保自定义符合以下要求的 ARM 模板。 如果是使用其他工具进行进一步开发，则可以忽略这些要求。

* 保持文件夹结构和文件名不变。 向项目添加更多资源或功能时，该工具可能会将新内容追加到现有文件。
* 保持自动生成参数的名称及其属性名称不变。 向项目添加更多资源或功能时，可以使用自动生成的参数。
* 保持自动生成的 ARM 模板的输出不变。 你可以向 ARM 模板添加其他输出。 输出为 `.fx/states/state.{env}.json`，且可用于其他功能，例如部署、验证清单文件。

### <a name="customization-scenarios"></a>自定义方案

你可以自定义以下方案：

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>为机器人使用现有的 Azure AD 应用

可以将以下配置代码片段添加到 `.fx/configs/config.{env}.json` 文件，以便使用自己为 Teams 应用创建的 Azure AD 应用。 若要创建 Azure AD 应用，请参阅 <https://aka.ms/teamsfx-existing-aad-doc>。

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

添加代码片段后，将密码添加到相关环境变量，以便工具可以在预配期间解析实际密码。

> [!NOTE]
> 确保不要在多个环境中共享同一 Azure AD 应用。 如果你没有更新 Azure AD 应用的权限，则可以收到一条警告，其中包含有关如何手动更新 Azure AD 应用的说明。 请按照说明在预配后更新 Azure AD 应用。

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>为 Teams 应用使用现有的 Azure AD 应用

可以将以下配置代码片段添加到 `.fx/configs/config.{env}.json` 文件，以便使用自己为机器人创建的 Azure AD 应用：

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

添加前面的代码片段后，将密码添加到相关环境变量，以便工具在预配期间解析实际密码。

#### <a name="skip-adding-user-for-sql-database"></a>跳过为 SQL 数据库添加用户的操作

如果在工具尝试为 SQL 数据库添加用户时出现权限不足错误，可以将以下配置代码片段添加到 `.fx/configs/config.{env}.json` 文件以跳过添加 SQL 数据库用户的操作：

```json
"skipAddingSqlUser": true
```

### <a name="specifying-the-name-of-function-app-instance"></a>指定函数应用实例的名称

可以将 `contosoteamsappapi` 用于函数应用实例，而不是使用默认名称。

> [!NOTE]
> 如果已预配环境，则指定名称可以为你创建新的函数应用实例，而不是重命名之前创建的实例。

以下步骤包括：

1. 针对当前环境打开 `.fx/configs/azure.parameters.{env}.json`。
2. 例如 `functionAppName` ，在节下 `provisionParameters` 添加新属性。
3. 输入一个值 `functionAppName`，例如 `contosoteamsappapi`。
4. 最终参数文件如以下代码片段所示：

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

向应用程序添加其他 Azure 资源或存储：

请考虑以下情况：

要将 Azure 存储添加到 Azure 函数后端以存储 Blob 数据。 不存在可以使用 Azure 存储支持来更新 bicep 模板的自动流。 但是，你可以编辑 bicep 文件并添加资源。 具体步骤如下：

1. 创建选项卡项目。
2. 向该项目添加函数。 有关详细信息，请参阅[添加资源](./add-resource.md)。
3. 在 ARM 模板中声明新的存储帐户。 你可以直接在 `templates/azure/provision/function.bicep` 声明该资源， 也可以在其他位置声明资源。

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

4. 使用 `templates/azure/provision/function.bicep` 中的 Azure 存储连接字符串更新 Azure 函数应用设置。 将以下代码片段添加到 `functionApp` 资源的 `appSettings` 数组：

    ``````````````````bicep
    {
        name: 'MyAppStorageAccountConnectionString'
        value: 'DefaultEndpointsProtocol=https;AccountName=${applicationStorageAccount.name};AccountKey=${listKeys(applicationStorageAccount.id, '2021-06-01').keys[0].value}'
    }
    ```````````````````

5. 你可以使用 Azure 存储输出绑定来更新函数。

## <a name="see-also"></a>另请参阅

* [将 Teams 应用部署到云](deploy.md)
* [管理多个环境](TeamsFx-multi-env.md)
* [在 Teams 项目中与其他开发人员协作](TeamsFx-collaboration.md)
