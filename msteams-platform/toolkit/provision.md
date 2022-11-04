---
title: 使用 Teams 工具包预配云资源
author: MuyangAmigo
description: 在本模块中，了解如何使用 Teams 工具包预配云资源、资源创建和自定义资源预配
ms.author: shenwe
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 6c3e44de4d63911dff5481ab859019aea37559d1
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833196"
---
# <a name="provision-cloud-resources"></a>预配云资源

TeamsFx 与 Azure 和 Microsoft 365 云进行了集成，因此你可以使用单个命令将应用程序放置在 Azure 中。 TeamsFx 与 Azure 资源管理器进行了集成，因此你能够预配应用程序在使用代码方法时所需的 Azure 资源。

::: zone pivot="visual-studio-code"

## <a name="provision-using-teams-toolkit-in-visual-studio-code"></a>在 Visual Studio Code 中使用 Teams 工具包进行预配

预配使用 Teams Toolkit for Visual Studio Code 或 TeamsFx CLI 中的单个命令执行。 有关详细信息，请参阅 [预配基于 Azure 的应用](/microsoftteams/platform/sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode%2Cvcode&tutorial-step=8)

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

ARM 模板文件使用占位符来表示参数。 这些占位符的用途是确保在新环境中为你创建新资源。 实际值将从 `.fx/states/state.{env}.json` 中解析得到。

有两种类型的参数，例如 Azure AD 应用程序相关参数和 Azure 资源相关参数。

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

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>为 Teams 应用使用现有的 Azure AD 应用

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

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>为机器人使用现有的 Azure AD 应用

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
2. 例如， `functionAppName` 在 节下 `provisionParameters` 添加新属性。
3. 输入值 `functionAppName`，例如 `contosoteamsappapi`。
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

想要将 Azure 存储添加到 Azure 函数后端以存储 Blob 数据。 不存在可以使用 Azure 存储支持来更新 bicep 模板的自动流。 但是，你可以编辑 bicep 文件并添加资源。 具体步骤如下：

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

::: zone-end

::: zone pivot="visual-studio"

## <a name="provision-using-teams-toolkit-in-visual-studio"></a>在 Visual Studio 中使用 Teams 工具包进行预配

以下步骤可帮助你使用 Visual Studio 预配云资源：

### <a name="sign-in-to-your-microsoft-365-account"></a>登录到 Microsoft 365 帐户

1. 打开 Visual Studio 2022。
1. 打开 Microsoft Teams 应用项目。
1. 选择 **“项目** > **Teams 工具包** > **准备 Teams 应用依赖项**”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare-app-dependencies1.png" alt-text="准备 Teams 应用依赖项":::

1. 选择“ **登录** ”以登录到 Azure 帐户。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare1.png" alt-text="登录到 Microsoft 365":::

    > [!NOTE]
    > 如果已登录，将显示用户名，也可以选择相同的来切换帐户。

1. 此时会打开默认 Web 浏览器 [，以便登录](https://developer.microsoft.com/en-us/microsoft-365/dev-program) 帐户。

1. 登录帐户后，选择“ **继续** ”。

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-signin-M365.png" alt-text="通过选择“继续”进行确认":::

### <a name="sign-in-to-your-azure-account"></a>登录到 Azure 帐户

1. 打开 Visual Studio 2022。
1. 打开 Teams 应用项目。
1. 选择 **“云中的****项目** > **Teams 工具包** > 预配”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud2.png" alt-text="登录到 Azure 帐户":::

1. 选择“ **登录...”** 以登录到 Azure 帐户。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-start.png" alt-text="登录到 Azure 帐户":::

   > [!NOTE]
   > 如果已登录，将显示用户名，或者可以选择切换帐户。

   使用凭据登录到 Azure 帐户后，浏览器会自动关闭。

### <a name="to-provision-cloud-resources"></a>预配云资源

在 Visual Studio 中打开项目后：

1. 选择 **“云中的****项目** > **Teams 工具包** > 预配”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud2.png" alt-text="在云中预配":::

   此时会显示 **“预配** ”窗口。

1. 输入以下详细信息以预配资源。

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-select-subscription1.png" alt-text="选择资源组":::

   1. 从下拉列表中选择 **订阅名称** 。
   1. 从下拉列表中选择 **资源组** 。
   1. 从下拉列表中选择“ **区域** ”。

      > [!NOTE]
      > 可以通过选择“ **新建**”创建新的资源组。

   1. 选择“ **预配**”。

1. 此时会显示一个对话框，指出可能会根据 Azure 使用情况添加费用。 选择“ **预配**”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-warning.png" alt-text="预配警告":::

   预配过程在 Azure 云中创建资源。 可以通过观察 Teams 工具包输出窗口来监视进度。

1. 预配完成后，系统会提示你。 选择“ **查看预配的资源”** ，查看所有预配的资源。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-provision-success.png" alt-text="查看预配的资源":::

## <a name="create-resources"></a>创建资源

在 Teams 工具包或 TeamsFx CLI 中触发预配命令时，可以创建以下资源：

* Microsoft Azure Active Directory (Microsoft 365 租户下的 Azure AD) 应用程序。
* Microsoft 365 租户的 Teams 平台下的 Teams 应用注册。
* 所选 Azure 订阅下的 Azure 资源。

创建新项目时，还需要创建 Azure 资源。 Azure 资源管理器 (ARM) 模板定义所有 Azure 资源，并帮助你在预配期间创建所需的 Azure 资源。

以下列表显示了为不同类型的应用和 Azure 资源创建资源：
<br>

<details>
<summary><b>为 Teams 选项卡应用程序创建资源</b></summary>

| Resource | 用途 | 说明 |
| --- | --- | --- |
| 应用服务计划 | 托管选项卡的 Web 应用。 | 不适用 |
| 应用服务 | 托管 Blazor 选项卡应用和有助于访问其他服务的简单身份验证服务器。 | 添加用户分配的标识，以访问其他 Azure 资源。 |
| 管理标识 | 对 Azure 服务到服务请求进行身份验证。 | 跨不同的功能和资源共享。 |

</details>
<br>

<details>
<summary><b>Teams 消息扩展应用程序的资源创建</b></summary>

| Resource | 用途 | 说明 |
| --- | --- | --- |
| Azure 机器人 | 使用机器人框架将应用注册为机器人。 | 将机器人连接到 Teams。 |
| App 服务计划 | 托管 Web 机器人应用。 | 不适用 |
| App 服务 | 托管机器人应用。 | 添加用户分配的标识，以访问其他 Azure 资源。 |
| 管理标识 | 对 Azure 服务到服务请求进行身份验证。 | 跨不同的功能和资源共享。 |

</details>
<br>

<details>
<summary><b>Teams 命令机器人应用程序的资源创建</b></summary>

| Resource | 用途 | 说明 |
| --- | --- | --- |
| Azure 机器人 | 使用机器人框架将应用注册为机器人。 | 将机器人连接到 Teams。 |
| 应用服务计划 | 托管 Web 机器人应用。 | 不适用 |
| 应用服务 | 托管机器人应用。 | 添加用户分配的标识，以访问其他 Azure 资源。 |
| 管理标识 | 对 Azure 服务到服务请求进行身份验证。 | 跨不同的功能和资源共享。 |

</details>
<br>

<details>
<summary><b>使用 HTTP 触发器为 Teams 通知机器人创建资源 (Web API 服务器) 应用程序</b></summary>

| Resource | 用途 | 说明 |
| --- | --- | --- |
| Azure 机器人 | 使用机器人框架将应用注册为机器人。 | 将机器人连接到 Teams。 |
| 应用服务计划 | 托管 Web 机器人应用。 | 不适用 |
| 应用服务 | 托管机器人应用。 | 添加用户分配的标识，以访问其他 Azure 资源。 |
| 托管标识 | 对 Azure 服务到服务请求进行身份验证。 | 跨不同的功能和资源共享。 |

</details>
<br>

<details>
<summary><b>使用 HTTP 触发器为 Teams 通知机器人创建资源 (Azure 函数) 应用程序</b></summary>

| Resource | 用途 | 说明 |
| --- | --- | --- |
| Azure 机器人 | 使用机器人框架将应用注册为机器人。 | 将机器人连接到 Teams。 |
| 管理标识 | 对 Azure 服务到服务请求进行身份验证。 | 跨不同的功能和资源共享。 |
| 存储帐户 | 帮助创建函数应用。 | 不适用 |
| 应用服务计划 | 托管函数机器人应用。 | 不适用 |
| 函数应用 | 托管机器人应用。 | -添加用户分配的标识以访问其他 Azure 资源。<br>-添加跨域资源共享 (CORS) 规则，以允许来自选项卡应用的请求。<br>-添加了仅允许来自 Teams 应用的请求的身份验证设置。<br>-添加 TeamsFx SDK 所需的应用设置。 |

</details>
<br>

<details>
<summary><b>使用计时器触发器为 Teams 通知机器人创建资源 (Azure 函数) 应用程序</b></summary>

| Resource | 用途 | 说明 |
| --- | --- | --- |
| Azure 机器人 | 使用机器人框架将应用注册为机器人。 | 将机器人连接到 Teams。 |
| 管理标识 | 对 Azure 服务到服务请求进行身份验证。 | 跨不同的功能和资源共享。 |
| 存储帐户 | 帮助创建函数应用。 | 不适用。 |
| 应用服务计划 | 托管函数机器人应用。 | 不适用 |
| 函数应用 | 托管机器人应用。 | -添加用户分配的标识以访问其他 Azure 资源。<br>-添加跨域资源共享 (CORS) 规则，以允许来自选项卡应用的请求。<br>-添加了仅允许来自 Teams 应用的请求的身份验证设置。<br>-添加 TeamsFx SDK 所需的应用设置。 |

</details>
<br>

<details>
<summary><b>使用 HTTP 触发器 + 计时器触发器为 Teams 通知机器人创建资源 (Azure 函数) 应用程序</b></summary>

| Resource | 用途 | 说明 |
| --- | --- | --- |
| Azure 机器人 | 使用机器人框架将应用注册为机器人。 | 将机器人连接到 Teams。 |
| 管理标识 | 对 Azure 服务到服务请求进行身份验证。 | 跨不同的功能和资源共享。 |
| 存储帐户 | 帮助创建函数应用。 | 不适用 |
| 应用服务计划 | 托管函数机器人应用。 | 不适用 |
| 函数应用 | 托管机器人应用。 | -添加用户分配的标识以访问其他 Azure 资源。<br>-添加跨域资源共享 (CORS) 规则，以允许来自选项卡应用的请求。<br>-添加了仅允许来自 Teams 应用的请求的身份验证设置。<br>-添加 TeamsFx SDK 所需的应用设置。 |

</details>
<br>

### <a name="manage-your-resources"></a>管理资源

可以登录[Azure 门户](https://portal.azure.com/)并管理 Teams 工具包创建的所有资源。

* 可以从现有列表或已创建的新资源组中选择资源组。
* 可以在目录的“概述”部分查看所选资源组的详细信息。

## <a name="customize-resource-provision"></a>自定义资源预配

使用 Teams 工具包，可以使用代码方法的基础结构来定义要预配的 Azure 资源。 可以根据要求在 Teams 工具包中更改配置。

Teams 工具包使用 ARM 模板来定义 Azure 资源。 ARM 模板是一组 bicep 文件，用于定义项目的基础结构和配置。 你可以通过修改 ARM 模板来自定义 Azure 资源。 有关详细信息，请参阅 [bicep 文档](/azure/azure-resource-manager/bicep)。

使用 ARM 进行预配涉及更改以下几套文件、参数和模板：

* arm 参数文件 (`azure.parameters.{your_env_name}.json`) 位于 `.fx/configs` 文件夹中，用于将参数传递给模板。
* 位于 文件夹中的 `templates/azure` ARM 模板文件包含以下文件：

| 文件 | 函数 | 允许自定义 |
| --- | --- | --- |
| main.bicep | 提供 Azure 资源的入口点。 提供 | 是 |
| provision.bicep | 创建和配置 Azure 资源。 | 是 |
| config.bicep | 将 TeamsFx 所需的配置添加到 Azure 资源。 | 是 |
| provision/xxx.bicep | 创建并配置 使用 `provision.bicep`的每个 Azure 资源。 | 可访问 |
| teamsfx/xxx.bicep | 将 TeamsFx 所需的配置添加到 消耗 `config.bicep`的每个 Azure 资源。| 否 |

> [!NOTE]
> 将资源或功能添加到项目后， `teamsfx/xxx.bicep` 将重新生成。 若要修改 bicep 文件，可以使用 Git 跟踪对 `teamsfx/xxx.bicep` 文件的更改。 这不会在向项目添加资源或功能时丢失任何更改。

ARM 模板文件使用占位符来表示参数。 占位符的用途是确保可以在新环境中创建新资源。 实际值是从 `.fx/states/state.{env}.json` 文件中解析的。

### <a name="azure-ad-application-related-parameters"></a>Azure AD 应用程序相关参数

| 参数名称 | 默认值占位符 | 占位符的含义 | 如何自定义 |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | 预配期间创建的应用的 Azure AD 应用客户端 ID。 | [为 Teams 应用使用现有的 Azure AD 应用](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | 预配期间创建的应用的 Azure AD 应用客户端密码。 | [为 Teams 应用使用现有的 Azure AD 应用](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | 应用的 Azure AD 应用的租户 ID。 | [为 Teams 应用使用现有的 Azure AD 应用](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | 应用的 Azure AD 应用的 OAuth 授权主机。 | [为 Teams 应用使用现有的 Azure AD 应用](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | 在预配期间创建的机器人的 Azure AD 应用客户端 ID。 | [为机器人使用现有的 Azure AD 应用](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | 在预配期间创建的机器人的 Azure AD 应用客户端密码。 | [为机器人使用现有的 Azure AD 应用](#use-an-existing-azure-ad-app-for-your-bot) |

### <a name="reference-environment-variables-in-parameter-files"></a>在参数文件中引用环境变量

如果值为机密，则无需在参数文件中对其进行硬编码。 参数文件支持引用环境变量中的值。 可以在 Teams 工具包的参数值中使用此语法 `{{$env.YOUR_ENV_VARIABLE_NAME}}` ，以便从当前环境变量解析。

以下示例将从环境变量 `DB_CONNECTION_STRING` 中读取参数 `mySelfHostedDbConnectionString` 的值：

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

### <a name="customize-arm-template-files"></a>自定义 ARM 模板文件

如果预定义模板不符合应用程序要求，则可以自定义文件夹下的 `templates/azure` ARM 模板。 例如，可以自定义 ARM 模板，为应用创建一些额外的 Azure 资源。 你需要具备有关 bicep 语言的基本知识，该语言用于创作 ARM 模板。

若要确保 TeamsFx 工具正常运行，请自定义满足以下要求的 ARM 模板：

* 确保文件夹结构和文件名保持不变。 向项目添加更多资源或功能时，该工具可能会向现有文件追加新内容。
* 确保自动生成的参数的名称及其属性名称保持未挂起状态。 向项目添加更多资源或功能时，可以使用自动生成的参数。
* 确保自动生成的 ARM 模板的输出也保持不变。 可以将更多输出添加到 ARM 模板。 输出是 `.fx/states/state.{env}.json` 并且可用于其他功能，例如部署和验证清单文件。

### <a name="customize-teams-app"></a>自定义 Teams 应用

可以通过添加配置代码片段以使用你创建的 Azure AD 应用来自定义机器人或 Teams 应用。 可以采用以下方式执行操作：

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>为 Teams 应用使用现有的 Azure AD 应用

可以添加以下配置代码段 `.fx/configs/config.{env}.json` ，以使用为 Teams 应用创建的 Azure AD 应用。 若要创建 Azure AD 应用，请按照链接 <https://aka.ms/teamsfx-existing-aad-doc>操作。

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

添加代码段后，将客户端密码添加到相关环境变量，以便 Teams 工具包可以在预配期间解析实际的客户端密码。

> [!NOTE]
> 确保不要在多个环境中共享同一 Azure AD 应用。 如果无权更新 Azure AD 应用，则会收到一条警告，其中包含手动更新 Azure AD 应用的说明。 按照这些说明在预配后更新 Azure AD 应用。

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>为机器人使用现有的 Azure AD 应用

可以将以下配置代码片段添加到 ， `.fx/configs/config.{env}.json` 以使用为机器人创建的 Azure AD 应用：

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

添加代码段后，将客户端密码添加到 Teams 工具包的相关环境变量，以便在预配期间解析实际的客户端密码。

#### <a name="skip-adding-user-for-sql-database"></a>跳过为 SQL 数据库添加用户的操作

如果在 Teams 工具包尝试将用户添加到 SQL 数据库时收到权限不足错误，则可以将以下配置代码段添加到 `.fx/configs/config.{env}.json` 以跳过添加 SQL 数据库用户：

```json
"skipAddingSqlUser": true
```

::: zone-end

## <a name="see-also"></a>另请参阅

* [将 Teams 应用部署到云](deploy.md)
* [管理多个环境](TeamsFx-multi-env.md)
* [在 Teams 项目中与其他开发人员协作](TeamsFx-collaboration.md)
* [使用 Visual Studio 将 Teams 应用部署到云](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)
* [使用 Visual Studio 编辑 Teams 应用清单](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [在本地调试 Visual Studio 的 Teams 应用](debug-local.md#debug-your-teams-app-locally-using-visual-studio)
