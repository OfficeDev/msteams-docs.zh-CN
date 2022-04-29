---
title: TeamsFx 命令行接口
author: MuyangAmigo
description: 介绍 TeamsFx 命令行接口
ms.author: zhany
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: ab9bad973d337d783c1de70c2ad8575a67d6cb6e
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111435"
---
# <a name="teamsfx-library"></a>TeamsFx 库

Microsoft Teams Framework (TeamsFx) 是一种封装常见功能和集成模式（如简化对 Microsoft 标识的访问）的库。 可以使用零配置为 Microsoft Teams 构建应用。

下面是主要 TeamsFx 功能的列表：

* **TeamsFx 协作**：让开发人员和项目所有者能邀请其他协作者加入 TeamsFx 项目。 可以协作调试和部署 TeamsFx 项目。

* **TeamsFx CLI**：它可加速 Teams 应用程序开发。 它还启用 CI/CD 方案，可在脚本中集成 CLI 来实现自动化。

* **TeamsFx SDK**：TeamsFx 软件开发工具包 (SDK) 是主要的 TeamsFx 代码库，其中封装了为 Teams 开发人员量身定制的客户端和服务器端代码的简单身份验证。

## <a name="teamsfx-command-line-interface"></a>TeamsFx 命令行接口

TeamsFx CLI 是基于文本的命令行接口，可加速 Teams 应用程序开发。 它旨在在构建 Teams 应用程序时提供以键盘为中心的体验。 它还启用 CI/CD 方案，可在脚本中集成 CLI 来实现自动化。

有关详细信息，请参阅：

* [源代码](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli)
* [包 (NPM)](https://www.npmjs.com/package/@microsoft/teamsfx-cli)

## <a name="get-started"></a>入门

从 `npm` 安装 `teamsfx-cli`，并运行 `teamsfx -h` 以检查所有可用命令：

```bash
  npm install -g @microsoft/teamsfx-cli
  teamsfx -h
```

## <a name="supported-commands"></a>支持的命令

| 命令 | 说明 |
|----------------|-------------|
| `teamsfx new`| 创建新的 Teams 应用程序。|
| `teamsfx account`| 管理云服务帐户。 支持的云服务为“Azure”和“Microsoft 365”。 |
| `teamsfx env` | 管理环境。 |
| `teamsfx capability`| 向当前应用程序添加新功能。|
| `teamsfx resource`  | 管理当前应用程序中的资源。|
| `teamsfx provision` | 在当前应用程序中预配云资源。|
| `teamsfx deploy` | 部署当前应用程序。  |
| `teamsfx package` | 将 Teams 应用构建到包中以进行发布。|
| `teamsfx validate` | 验证当前应用程序。|
| `teamsfx publish` | 将应用发布到 Teams。|
| `teamsfx preview` | 预览当前应用程序。 |
| `teamsfx config`  | 管理配置数据。 |
| `teamsfx permission`| 在同一项目中与其他开发人员协作。|

## `teamsfx new`

默认情况下，`teamsfx new` 会进入交互模式，并指导你完成创建新的 Teams 应用程序的过程。 还可以通过将 `--interactive` 标志设置为 `false` 来使用非交互模式。

| `teamsFx new` 命令 | 说明 |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | 从现有模板创建应用 |
| `teamsfx new template list`     | 列出所有可用模板 |

### <a name="parameters-for-teamsfx-new"></a>`teamsfx new` 的参数

| 参数 | 要求 | 说明 |
|:---------------- |:-------------|:-------------|
|`--app-name` | 是| Teams 应用程序的名称。|
|`--interactive`| 否 | 以交互方式选择选项。 选项为 `true` 和 `false`，默认值为 `true`。|
|`--capabilities`| 否| 选择 Teams 应用程序功能，多个选项为 `tab`、`bot`、`messaging-extension` 和 `tab-spfx`。 默认值为 `tab`。|
|`--programming-language`| 否| 项目的编程语言。 选项为 `javascript` 或 `typescript`，默认值为 `javascript`。|
|`--folder`| 否 | 项目目录。 将在此目录下创建具有应用名称的子文件夹。 默认值为 `./`。|
|`--spfx-framework-type`| 否| 如果选择了 `Tab(SPfx)` 功能，则适用。 前端框架。 选项为 `none` 和 `react`，默认值为 `none`。|
|`--spfx-web part-name`| 否 | 如果选择了 `Tab(SPfx)` 功能，则适用。 默认值为“helloworld”。|
|`--spfx-web part-desp`| 否 | 如果选择了 `Tab(SPfx)` 功能，则适用。 默认值为“helloworld description”。 |
|`--azure-resources`| 否| 如果包含 `tab` 功能，则适用。 将 Azure 资源添加到项目。 多个选项为 `sql`（Azure SQL 数据库）和 `function` (Azure Functions)。 |

### <a name="scenarios-for-teamsfx-new"></a>`teamsfx new` 的方案

可以使用交互模式创建 Teams 应用。使用 `teamsfx new` 控制所有参数的方案如下所示：

#### <a name="tab-app-hosted-on-spfx-using-react"></a>使用 React 托管在 SPFx 上的选项卡应用

```bash
teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
```

#### <a name="teams-app-in-javascript-with-tab-bot-capabilities-and-azure-functions"></a>JavaScript 中具有选项卡、机器人功能和 Azure Functions 的 Teams 应用

```bash
teamsfx new --interactive false --app-name newtabbotapp --capabilities tab bot --programming-language javascript --azure-resources function
```

#### <a name="teams-tab-app-with-azure-functions-and-azure-sql"></a>具有 Azure Functions 和 Azure SQL 的 Teams 选项卡应用

```bash
teamsfx new --interactive false app-name newapp --azure-resources sql function --programming-language typescript
```

## `teamsfx account`

管理云服务帐户。 支持的云服务是 `Azure` 和 `Microsoft 365`。

| `teamsFx account` 命令 | 说明 |
|:----------------  |:-------------|
| `teamsfx account login <service>`  | 登录到所选云服务。 |
| `teamsfx account logout <service>`  | 注销所选云服务。 |
| `teamsfx account set --subscription` | 更新帐户设置以设置订阅 ID。 |

## `teamsfx env`

管理环境。

| `teamsfx env` 命令  | 说明 |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | 通过从指定的环境复制来添加新环境。 |
| `teamsfx env list` | 列出所有环境。 |

### <a name="scenarios-for-teamsfx-env"></a>`teamsfx env` 的方案

`teamsfx env` 的方案如下所示：

#### <a name="create-a-new-environment"></a>创建新环境

通过从现有开发环境复制来添加新环境：

```bash
teamsfx env add staging --env dev
```

## `teamsfx capability`

向当前应用程序添加新功能。

| `teamsFx capability` 命令  | 说明 |
|:----------------  |:-------------|
| `teamsfx capability add tab` | 添加选项卡 |
| `teamsfx capability add bot` | 添加机器人 |
| `teamsfx capability add messaging-extension`| 添加消息扩展 |

> [!NOTE]
> 如果项目包含机器人，则无法添加消息扩展，反之亦然。 创建新的 Teams 应用项目时，可以在项目中同时包括机器人和消息扩展。

## `teamsfx resource`

管理当前应用程序中的资源。 支持的 `<resource-type>` 包括：`azure-sql`、`azure-function` 和 `azure-apim`。

| `teamsFx resource` 命令  | 说明 |
|:----------------  |:-------------|
| `teamsfx resource add <resource-type>`      | 将资源添加到当前应用程序。|
| `teamsfx resource show <resource-type>`      | 显示资源的配置详细信息。 |
| `teamsfx resource list`      | 列出当前应用程序中的所有资源。 |

### <a name="parameters-for-teamsfx-resource-add-azure-function"></a>`teamsfx resource add azure-function` 的参数

| 参数  | 要求 | 说明 |
|----------------  |-------------|-------------|
|`--function-name`| 是 | 提供函数名称。 默认值为 `getuserprofile`。 |

### <a name="parameters-for-teamsfx-resource-add-azure-sql"></a>`teamsfx resource add azure-sql` 的参数

#### `--function-name`

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--function-name`| 是 | 提供函数名称。 默认值为 `getuserprofile`。 |

> [!NOTE]
> 函数名称已验证为 SQL，需要从服务器工作负载进行访问。 如果项目不包含 `Azure Functions`，请创建一个。

### <a name="parameters-for-teamsfx-resource-add-azure-apim"></a>`teamsfx resource add azure-apim` 的参数

> [!TIP]
> 尝试使用现有 `APIM` 实例时，这些选项会生效。 默认情况下，无需指定任何选项，它会在 `teamsfx provision` 步骤期间创建新实例。

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--subscription`| 是 | 选择 Azure 订阅|
|`--apim-resource-group`| 是| 资源组的名称。 |
|`--apim-service-name`| 是 | API 管理服务实例的名称。 |
|`--function-name`| 是 | 提供函数名称。 默认值为 `getuserprofile`。 |

> [!NOTE]
> `Azure API Management` 需要使用 `Azure Functions`。 如果项目不包含 `Azure Functions`，则可以创建一个。

## `teamsfx provision`

在当前应用程序中预配云资源。

### <a name="parameters-for-teamsfx-provision"></a>`teamsfx provision` 的参数

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是| 为项目选择环境。 |
|`--subscription`| 否 | 指定 Azure 订阅 ID。 |
|`--resource-group`| 否 | 设置现有资源组的名称。 |
|`--sql-admin-name`| 否 | 当项目中存在 SQL 资源时适用。 SQL 的管理员名称。|
|`--sql-password`| 否| 当项目中有 SQL 资源时适用。 SQL 的管理员密码。|

## `teamsfx deploy`

此命令用于部署当前应用程序。 默认情况下，它会部署整个项目，但也可以部分部署。 多个选项是 `frontend-hosting`、`function`、`apim`、`teamsbot` 和 `spfx`。

### <a name="parameters-for-teamsfx-deploy"></a>`teamsfx deploy` 的参数

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是| 选择项目的现有环境。 |
|`--open-api-document`| 否 | 当项目中有 APIM 资源时适用。 打开的 API 文档文件路径。 |
|`--api-prefix`| 否 | 当项目中有 APIM 资源时适用。 API 名称前缀。 API 的默认唯一名称是 `{api-prefix}-{resource-suffix}-{api-version}`。 |
|`--api-version`| 否 | 当项目中有 APIM 资源时适用。 API 版本。 |

## `teamsfx validate`

验证当前应用程序。 此命令验证应用程序的清单文件。

### <a name="parameters-for-teamsfx-validate"></a>`teamsfx validate` 的参数

`--env`：选择项目的现有环境。

## `teamsfx publish`

将应用发布到 Teams。

### <a name="parameters-for-teamsfx-publish"></a>`teamsfx publish` 的参数

`--env`：选择项目的现有环境。

## `teamsfx package`

将 Teams 应用构建到包中以进行发布。

## `teamsfx preview`

从本地或远程预览当前应用程序。

### <a name="parameters-for-teamsfx-preview"></a>`teamsfx preview` 的参数

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--local`| 否 | 从本地预览应用程序。 `--local` 与 `--remote` 互斥。 |
|`--remote`| 否 | 从远程预览应用程序。 `--remote` 与 `--local` 互斥。 |
|`--env`| 否 | 追加参数 `--remote` 时，请选择项目的现有环境。 |
|`--folder`| 否 | 项目根目录。 默认值为 `./`。 |
|`--browser`| 否 | 用于打开 Teams Web 客户端的浏览器。 选项有 `chrome`、`edge` 和 `default`，如系统默认浏览器，值为 `default`。 |
|`--browser-arg`| 否 | 要传递到浏览器的参数需要 --browser，可以多次使用，例如 --browser-args="--guest" |
|`--sharepoint-site`| 否 | SharePoint 网站 URL，例如用于 SPFx 项目远程预览的 `{your-tenant-name}.sharepoint.com`。 |

### <a name="scenarios-for-teamsfx-preview"></a>`teamsfx preview` 的方案

#### <a name="local-preview"></a>本地预览

依赖项:

* Node.js
* .NET SDK
* Azure Functions Core Tools

```bash
teamsfx preview --local
teamsfx preview --local --browser chrome
```

#### <a name="remote-preview"></a>远程预览

```bash
teamsfx preview --remote
teamsfx preview --remote --browser edge
```

> [!NOTE]
> React 等后台服务的日志保存在 `~/.fx/cli-log/local-preview/` 中。

## `teamsfx config`

管理用户范围或项目范围内的配置数据。

| `teamsfx config` 命令  | 说明 |
|:----------------  |:-------------|
| `teamsfx config get [option]` | 查看选项的配置值 |
| `teamsfx config set <option> <value>` | 更新选项的配置值 |

### <a name="parameters-for-teamsfx-config"></a>`teamsfx config` 的参数

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是 | 选择项目的现有环境。 |
|`--folder`| 否 | 项目目录。 这用于获取或设置项目配置。 默认值为 `./`。 |
|`--global`| 否 | 配置的应对。 如果为 true，则范围仅限于用户范围而不是项目范围。 默认值为 `false`。 目前，支持的全局配置包括 `telemetry`、`validate-dotnet-sdk`、`validate-func-core-tools`、`validate-node`。 |

### <a name="scenerios-for-teamsfx-config"></a>`teamsfx config` 的方案

`.userdata` 文件中的 `teamsfx config` 机密已加密，可帮助查看或更新值。

#### <a name="stop-sending-telemetry-data"></a>停止发送遥测数据

```bash
teamsfx config set telemetry off
```

#### <a name="disable-environment-checker"></a>禁用环境检查器

有三种配置可以打开或关闭 Node.js、.NET SDK 和 Azure Functions Core Tools 验证，并且默认情况下启用所有这些配置。 如果不需要依赖项验证并想要自行安装依赖项，则可以将配置设置为“关闭”。 请查看以下指南：

* [Node.js 安装指南](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
* [.NET SDK 安装指南](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk)
* [Azure Functions Core Tools 安装指南](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure-functions-core-tools)。

若要禁用 .NET SDK 验证，可以使用以下命令：

```bash
teamsfx config set validate-dotnet-sdk off
```

若要启用 .NET SDK 验证，可以使用以下命令：

```bash
teamsfx config set validate-dotnet-sdk on
```

#### <a name="view-all-the-user-scope-configuration"></a>查看所有用户范围配置

```bash
teamsfx config get -g
```

#### <a name="view-all-the-configuration-in-project"></a>查看项目中的所有配置

机密会自动解密：

```bash
teamsfx config get --env dev
```

#### <a name="update-the-secret-configuration-in-project"></a>更新项目中的机密配置

```bash
teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
```

## `teamsfx permission`

TeamsFx CLI 为协作方案提供 `teamsFx permission` 命令。

| `teamsFx permission` 命令 | 说明 |
|:------------------------------|-------------|
| `teamsfx permission grant --env --email` | 为协作者的 Microsoft 365 帐户授予指定环境项目的权限。 |
| `teamsfx permission status` | 显示项目的权限状态 |

### <a name="parameters-for-teamsfx-permission-grant"></a>`teamsfx permission grant` 的参数

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是 | 提供环境名称。 |
|`--email`| 是 | 提供协作者的 Microsoft 365 电子邮件地址。 确保协作者的帐户与创建者位于同一租户中。 |

### <a name="parameters-for-teamsfx-permission-status"></a>`teamsfx permission status` 的参数

| 参数 | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是 | 提供环境名称。 |
|`--list-all-collaborators` | 否 | 使用此标志，Teams 工具包 CLI 将打印此项目的所有协作者。 |

### <a name="scenarios-for-teamsfx-permission"></a>`teamsfx permission` 的方案

`TeamsFx` 项目的权限如下所示：

#### <a name="grant-permission"></a>授予权限

项目创建者和协作者可以使用 `teamsfx permission grant` 命令将新的协作者添加到项目中：

```bash
teamsfx permission grant --env dev --email user-email@user-tenant.com
```

在获得所需权限后，项目创建者和协作者可以通过 GitHub 与新协作者共享项目，新协作者可以拥有 Microsoft 365 帐户的所有权限。

#### <a name="show-permission-status"></a>显示权限状态

项目创建者和协作者可以使用 `teamsfx permission status` 命令查看其 Microsoft 365 帐户对特定环境的权限：

```bash
teamsfx permission status --env dev
```

#### <a name="list-all-collaborators"></a>列出所有协作者

项目创建者和协作者可以使用 `teamsfx permission status` 命令查看特定环境的所有协作者：

```bash
teamsfx permission status --env dev --list-all-collaborators
```

#### <a name="e2e-collaboration-work-flow-in-cli"></a>CLI 中的 E2E 协作工作流

作为项目创建者：

* 创建新的 TeamsFx 选项卡或机器人项目，并选择 Azure 作为主机类型：

  ```bash
  teamsfx new --interactive false --app-name newapp --host-type azure
  ```

* 登录到 Microsoft 36 5帐户和 Azure 帐户：

  ```bash
  teamsfx account login azure
  teamsfx account login Microsoft 365
  ```

* 预配项目：

  ```bash
  teamsfx provision
  ```

* 查看协作者：

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-status-all-1.png" alt-text="permission-1":::

* 将另一个帐户添加为协作者。 确保添加的帐户位于同一租户下：

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-grant-1.png" alt-text="permission":::

* 将项目推送到 GitHub

作为项目协作者：

* 从 GitHub 克隆项目。
* 登录到 Microsoft 365 帐户。 确保添加相同的 Microsoft 365 帐户：

  ```bash
  teamsfx account login Microsoft 365
  ```

* 使用所有 Azure 资源的参与者权限登录到 Azure 帐户。

  ```bash
  teamsfx account login azure
  ```

* 检查权限状态。 应该发现自己拥有项目的所有者权限：

  ```bash
  teamsfx permission status --env dev
  ```

  ![权限状态](./images/permission-status.png)

* 更新选项卡代码，并将项目部署到远程。
* 启动远程，项目应该可以正常工作。

## <a name="see-also"></a>另请参阅

* [用于 TypeScript 或 JavaScript 的 TeamsFx SDK](TeamsFx-SDK.md)
* [在 Teams 工具包中管理多个环境](TeamsFx-multi-env.md)
* [使用 Teams 工具包协作处理 Teams 项目](TeamsFx-collaboration.md)
* [Teams 工具包概述](teams-toolkit-fundamentals.md)
