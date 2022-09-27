---
title: 使用 Teams 工具包使用 Teams Toolkit for Visual Studio 预配云资源
author: surbhigupta
description: 在本模块中，了解如何使用 Teams 工具包预配云资源。 此外，还要在 Visual Studio 中创建资源并自定义资源预配
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 00e021e3e42eed6eeb5881d258a9884a7e579377
ms.sourcegitcommit: 65ae3ccc2312ddc6cdaa05096e30bdf9dca10c3f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/27/2022
ms.locfileid: "68027444"
---
# <a name="provision-cloud-resources-using-visual-studio"></a>使用 Visual Studio 预配云资源

TeamsFx 与 Azure 和 Microsoft 365 云集成，可通过单个命令将应用程序放置在 Azure 中。 TeamsFx 与 Azure 资源管理器集成，使你能够预配 Azure 资源。 对于代码方法，应用程序需要云资源。

## <a name="prerequisites"></a>先决条件

下面是预配云资源所需的工具列表：

| &nbsp; | 安装 | 用于使用... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Visual Studio 2022 版本 17.3 | 可以安装 Visual Studio 的企业版，并安装“ASP.NET”工作负荷和 Microsoft Teams 开发工具。 |
| &nbsp; | [Microsoft 365 开发人员帐户](https://developer.microsoft.com/en-us/microsoft-365/dev-program) | 对具有相应安装应用权限的 Teams 帐户的访问权限。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | 通过聊天、会议、通话等应用与每一位同事进行协作的 Microsoft Teams - 一个地方完成所有操作。 |
| &nbsp; | Teams 工具包 | 一个 Visual Studio 扩展，用于为应用创建项目基架。 使用最新版本。 |
| &nbsp; | [Azure 帐户](https://portal.azure.com/) | 具有有效订阅的 Azure 帐户。 |

## <a name="steps-to-provision-cloud-resources"></a>预配云资源的步骤

以下步骤可帮助你使用 Visual Studio 预配云资源：

### <a name="sign-in-to-your-microsoft-365-account"></a>登录到 Microsoft 365 帐户

1. Visual Studio 2022。
2. 打开 Microsoft Teams 应用项目。
3. 选择 **“项目**”。
4. 选择 **Teams 工具包**。
5. 选择 **“准备 Teams 应用依赖项**”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare-app-dependencies.png" alt-text="准备团队应用依赖项":::

7. 选择 **“登录...** ”以登录到 Azure 帐户。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-prepare1.png" alt-text="登录 Microsoft 365":::

    > [!NOTE]
    > 如果已登录，则会显示用户名，或者可以选择相同的用户名来切换帐户。

8. 将打开默认 Web 浏览器， [以便登录到](https://developer.microsoft.com/en-us/microsoft-365/dev-program) 帐户。
9. 登录帐户后选择 **“继续** ”。

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-signin-M365.png" alt-text="通过选择“继续”进行确认":::

### <a name="sign-in-to-your-azure-account"></a>登录到 Azure 帐户

1. 打开 Visual Studio 2022。
2. 打开 Teams 应用项目。
3. 选择 **“项目**”。
4. 选择 **Teams 工具包**。
5. 在 **云中选择“预配**”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud.png" alt-text="登录到 Azure 帐户":::

6. 选择 **“登录...** ”以登录到 Azure 帐户。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-start.png" alt-text="登录到 Azure 帐户":::

   > [!NOTE]
   > 如果已登录，则会显示用户名，或者可以选择切换帐户。

7. 使用凭据登录到 Azure 帐户。 浏览器会自动关闭。

### <a name="to-provision-cloud-resources"></a>预配云资源

1. 在 Visual Studio 中打开项目后，选择 **“项目**”
2. 选择 **Teams 工具包**
3. 在 **云中选择“预配**”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-in-cloud1.png" alt-text="在云中预配":::

4. 在 **“预配** ”对话中，可以看到 Azure 帐户中所有订阅的列表。
5. 可以选择或创建新的 **资源组**。
6. 选择 **“预配**”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-select-subscription1.png" alt-text="选择资源组":::

7. 对话框警告可以根据 Azure 使用情况添加费用。 选择 **“预配**”。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-warning.png" alt-text="预配警告":::

   在 Azure 云中创建资源的预配过程可能需要一些时间。

8. 检查 Teams 工具包输出窗口以监视进度。
9. 预配完成后系统会提示你。 选择 **“查看预配的资源** ”以查看已预配的所有资源。

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/Provision-cloud-resources-in-TTK-VS/teams-toolkit-vs-provision-provision-success.png" alt-text="查看预配的资源":::

### <a name="create-resources"></a>创建资源

在 Teams 工具包或 TeamsFx CLI 中触发预配命令时，可以创建以下资源：

* Microsoft Azure Active Directory (Microsoft 365 租户下的 Azure AD) 应用程序。
* Microsoft 365 租户的 Teams 平台下的 Teams 应用注册。
* 所选 Azure 订阅下的 Azure 资源。

创建新项目时，还需要创建 Azure 资源。 Azure 资源管理器 (ARM) 模板定义了所有 Azure 资源，并可帮助你在预配期间创建所需的 Azure 资源。

### <a name="create-resource-for-teams-tab-application"></a>为 Teams 选项卡应用程序创建资源

| Resource | 用途 | 说明 |
| --- | --- | --- |
| 应用服务计划 | 托管选项卡的 Web 应用。 | 不适用 |
| 应用服务 | 托管 Blazor 选项卡应用和帮助获取其他服务访问权限的简单身份验证服务器。 | 添加用户分配的标识，以访问其他 Azure 资源。 |
| 管理标识 | 对 Azure 服务到服务请求进行身份验证。 | 跨不同功能和资源共享。 |

### <a name="create-resources-for-teams-message-extension-application"></a>为 Teams 消息扩展应用程序创建资源

| Resource | 用途 | 说明 |
| --- | --- | --- |
| Azure 机器人 | 将应用注册为机器人框架。 | 将机器人连接到 Teams。 |
| App 服务计划 | 托管 Web 机器人应用。 | 不适用 |
| App 服务 | 托管机器人应用。 | 添加用户分配的标识，以访问其他 Azure 资源。 |
| 管理标识 | 对 Azure 服务到服务请求进行身份验证。 | 跨不同功能和资源共享。 |

### <a name="create-resources-for-teams-command-bot-application"></a>为 Teams 命令机器人应用程序创建资源

| Resource | 用途 | 说明 |
| --- | --- | --- |
| Azure 机器人 | 将应用注册为机器人框架。 | 将机器人连接到 Teams。 |
| 应用服务计划 | 托管 Web 机器人应用。 | 不适用 |
| 应用服务 | 托管机器人应用。 | 添加用户分配的标识，以访问其他 Azure 资源。 |
| 管理标识 | 对 Azure 服务到服务请求进行身份验证。 | 跨不同功能和资源共享。 |

### <a name="create-resources-for-teams-notification-bot-with-http-trigger-web-api-server-application"></a>使用 HTTP 触发器 (Web API 服务器) 应用程序创建 Teams 通知机器人的资源

| Resource | 用途 | 说明 |
| --- | --- | --- |
| Azure 机器人 | 将应用注册为机器人框架。 | 将机器人连接到 Teams。 |
| 应用服务计划 | 托管 Web 机器人应用。 | 不适用 |
| 应用服务 | 托管机器人应用。 | 添加用户分配的标识，以访问其他 Azure 资源。 |
| 托管标识 | 对 Azure 服务到服务请求进行身份验证。 | 跨不同功能和资源共享。 |

### <a name="create-resource-for-teams-notification-bot-with-http-trigger-azure-function-application"></a>使用 HTTP 触发器为 Teams 通知机器人创建资源 (Azure 函数) 应用程序

| Resource | 用途 | 说明 |
| --- | --- | --- |
| Azure 机器人 | 将应用注册为机器人框架。 | 将机器人连接到 Teams。 |
| 管理标识 | 对 Azure 服务到服务请求进行身份验证。 | 在不同功能和资源之间共享。 |
| 存储帐户 | 帮助创建函数应用。 | 不适用 |
| 应用服务计划 | 托管函数机器人应用。 | 不适用 |
| 函数应用 | 托管机器人应用。 | -添加用户分配的标识以访问其他 Azure 资源。<br>-添加跨源资源共享 (CORS) 规则，以允许来自 Tab 应用的请求。<br>-添加仅允许来自 Teams 应用的请求的身份验证设置。<br>-添加 TeamsFx SDK 所需的应用设置。 |

### <a name="create-resource-for-teams-notification-bot-with-timer-trigger-azure-function-application"></a>使用计时器触发器为 Teams 通知机器人创建资源 (Azure 函数) 应用程序

| Resource | 用途 | 说明 |
| --- | --- | --- |
| Azure 机器人 | 将应用注册为机器人框架。 | 将机器人连接到 Teams。 |
| 管理标识 | 对 Azure 服务到服务请求进行身份验证。 | 跨不同功能和资源共享。 |
| 存储帐户 | 帮助创建函数应用。 | 不适用。 |
| 应用服务计划 | 托管函数机器人应用。 | 不适用 |
| 函数应用 | 托管机器人应用。 | -添加用户分配的标识以访问其他 Azure 资源。<br>-添加跨源资源共享 (CORS) 规则，以允许来自 Tab 应用的请求。<br>-添加仅允许来自 Teams 应用的请求的身份验证设置。<br>-添加 TeamsFx SDK 所需的应用设置。 |

### <a name="create-resources-for-teams-notification-bot-with-http-trigger--timer-trigger-azure-function-application"></a>使用 HTTP 触发器 + 计时器触发器 (Azure 函数) 应用程序为 Teams 通知机器人创建资源

| Resource | 用途 | 说明 |
| --- | --- | --- |
| Azure 机器人 | 将应用注册为机器人框架。 | 将机器人连接到 Teams。 |
| 管理标识 | 对 Azure 服务到服务请求进行身份验证。 | 跨不同功能和资源共享。 |
| 存储帐户 | 帮助创建函数应用。 | 不适用 |
| 应用服务计划 | 托管函数机器人应用。 | 不适用 |
| 函数应用 | 托管机器人应用。 | -添加用户分配的标识以访问其他 Azure 资源。<br>-添加跨源资源共享 (CORS) 规则，以允许来自 Tab 应用的请求。<br>-添加仅允许来自 Teams 应用的请求的身份验证设置。<br>-添加 TeamsFx SDK 所需的应用设置。 |

### <a name="manage-your-resources"></a>管理资源

可以登录[Azure 门户](https://portal.azure.com/)和管理 Teams 工具包创建的所有资源。

* 可以从现有列表或已创建的新资源组中选择资源组。
* 可以在内容表的概述部分中查看所选资源组的详细信息。

### <a name="customize-resource-provision"></a>自定义资源预配

使用 Teams 工具包，可以使用代码方法的基础结构来定义要预配的 Azure 资源。 可以根据要求更改 Teams 工具包中的配置。

Teams 工具包使用 ARM 模板来定义 Azure 资源。 ARM 模板是一组 bicep 文件，用于定义项目的基础结构和配置。 你可以通过修改 ARM 模板来自定义 Azure 资源。 有关详细信息，请参阅 [bicep 文档](/azure/azure-resource-manager/bicep)。

使用 ARM 进行预配涉及更改以下几套文件、参数和模板：

* ARM 参数文件 (`azure.parameters.{your_env_name}.json`) 位于文件夹中 `.fx/configs` ，用于将参数传递给模板。
* 位于文件夹中的 `templates/azure` ARM 模板文件包含以下文件：

| 文件 | 函数 | 允许自定义 |
| --- | --- | --- |
| main.bicep | 为 Azure 资源提供入口点。 提供 | 是 |
| provision.bicep | 创建和配置 Azure 资源。 | 是 |
| config.bicep | 将 TeamsFx 所需的配置添加到 Azure 资源。 | 是 |
| provision/xxx.bicep | 创建和配置所使用的 `provision.bicep`每个 Azure 资源。 | 可访问 |
| teamsfx/xxx.bicep | 将 TeamsFx 所需的配置添加到所使用的 `config.bicep`每个 Azure 资源。| 否 |

> [!NOTE]
> 将资源或功能添加到项目后， `teamsfx/xxx.bicep` 将重新生成。 若要修改 bicep 文件，可以使用 Git 跟踪对文件所做的 `teamsfx/xxx.bicep` 更改。 这不会使你在向项目添加资源或功能时丢失任何更改。

ARM 模板文件使用参数的占位符。 占位符的目的是确保可在新环境中创建新资源。 实际值是从文件解析的 `.fx/states/state.{env}.json` 。

### <a name="azure-ad-application-related-parameters"></a>Azure AD 应用程序相关参数

| 参数名称 | 默认值占位符 | 占位符的含义 | 如何自定义 |
| --- | --- | --- | --- |
| Microsoft 365 ClientId | {{state.fx-resource-aad-app-for-teams.clientId}} | 在预配期间创建的应用的 Azure AD 应用客户端 ID。 | [自定义该值](#use-an-existing-azure-ad-app-for-your-teams-app) |
| Microsoft 365 ClientSecret | {{state.fx-resource-aad-app-for-teams.clientSecret}} | 在预配期间创建的应用的 Azure AD 应用客户端机密。 | [自定义该值](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 TenantId | {{state.fx-resource-aad-app-for-teams.tenantId}} | 应用的 Azure AD 应用的租户 ID。 | [自定义该值](#use-an-existing-azure-ad-app-for-your-teams-app)  |
| Microsoft 365 OAuthAuthorityHost | {{state.fx-resource-aad-app-for-teams.oauthHost}} | 应用的 Azure AD 应用的 OAuth 颁发机构主机。 | [自定义该值](#use-an-existing-azure-ad-app-for-your-teams-app) |
| botAadAppClientId | {{state.fx-resource-bot.botId}} | 预配期间创建的机器人 Azure AD 应用客户端 ID。 | [自定义该值](#use-an-existing-azure-ad-app-for-your-bot) |
| botAadAppClientSecret | {{state.fx-resource-bot.botPassword}} | 在预配期间创建机器人的 Azure AD 应用客户端机密。 | [自定义该值](#use-an-existing-azure-ad-app-for-your-bot) |

### <a name="reference-environment-variables-in-parameter-files"></a>参数文件中的引用环境变量

当值为机密时，无需在参数文件中对其进行硬编码。 参数文件支持引用环境变量中的值。 可以在 Teams 工具包的参数值中使用此语 `{{$env.YOUR_ENV_VARIABLE_NAME}}` 法从当前环境变量解析。

以下示例将从环境变量 `DB_CONNECTION_STRING` 中读取参数 `mySelfHostedDbConnectionString` 的值：

```json
...
    "mySelfHostedDbConnectionString": "{{$env.DB_CONNECTION_STRING}}"
...
```

### <a name="customize-arm-template-files"></a>自定义 ARM 模板文件

如果预定义的模板不符合应用程序要求，则可以自定义文件夹下 `templates/azure` 的 ARM 模板。 例如，可以自定义 ARM 模板，为应用创建一些额外的 Azure 资源。 你需要具备有关 bicep 语言的基本知识，该语言用于创作 ARM 模板。

若要确保 TeamsFx 工具正常运行，请自定义符合以下要求的 ARM 模板：

* 确保文件夹结构和文件名保持不变。 向项目添加更多资源或功能时，该工具可能会将新内容追加到现有文件中。
* 确保自动生成的参数的名称及其属性名称保持未挂起。 向项目添加更多资源或功能时，可以使用自动生成的参数。
* 确保自动生成的 ARM 模板的输出也保持不变。 可以向 ARM 模板添加更多输出。 输出现在 `.fx/states/state.{env}.json` 和可以用于其他功能，例如部署和验证清单文件。

### <a name="customize-teams-app"></a>自定义 Teams 应用

可以通过添加配置片段来自定义机器人或 Teams 应用，以使用由你创建的 Azure AD 应用。 可以通过以下方式执行：

#### <a name="use-an-existing-azure-ad-app-for-your-bot"></a>为机器人使用现有的 Azure AD 应用

可以添加以下配置代码片段 `.fx/configs/config.{env}.json` ，以使用为 Teams 应用创建的 Azure AD 应用。 若要创建 Azure AD 应用，请按照链接操作 <https://aka.ms/teamsfx-existing-aad-doc>。

```json
"auth": {
    "clientId": "<your Azure AD app client id>",
    "clientSecret": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}",
    "objectId": "<your Azure AD app object id>",
    "accessAsUserScopeId": "<id of the access_as_user scope>"
}
```

添加代码段后，将客户端机密添加到相关环境变量，以便 Teams 工具包可以在预配期间解析实际的客户端机密。

> [!NOTE]
> 确保不要在多个环境中共享同一 Azure AD 应用。 如果没有更新 Azure AD 应用的权限，则会收到一条警告，其中包含手动更新 Azure AD 应用的说明。 按照以下说明在预配后更新 Azure AD 应用。

#### <a name="use-an-existing-azure-ad-app-for-your-teams-app"></a>为 Teams 应用使用现有的 Azure AD 应用

可以添加以下配置代码片段以 `.fx/configs/config.{env}.json` 使用为机器人创建的 Azure AD 应用：

```json
"bot": {
    "appId": "<your Azure AD app client id>",
    "appPassword": "{{$env.ENV_NAME_THAT_STORES_YOUR_SECRET}}"
}
```

添加代码段后，将客户端机密添加到 Teams 工具包的相关环境变量，以在预配期间解析实际的客户端机密。

#### <a name="skip-adding-user-for-sql-database"></a>跳过为 SQL 数据库添加用户的操作

如果 Teams 工具包尝试将用户添加到 SQL 数据库时出现权限不足错误，则可以添加以下配置代码片段以 `.fx/configs/config.{env}.json` 跳过添加 SQL 数据库用户：

```json
"skipAddingSqlUser": true
```

## <a name="see-also"></a>另请参阅

* [使用 Visual Studio 将 Teams 应用部署到云](deploy-teams-app.md)
* [使用 Visual Studio 编辑 Teams 应用清单](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [在本地为 Visual Studio 调试 Teams 应用](debug-teams-app-visual-studio.md)
