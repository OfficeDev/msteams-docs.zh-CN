---
title: TeamsFx 命令行接口
author: MuyangAmigo
description: 介绍 TeamsFx 命令行接口
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 5fde7e94c198bfe76810a52ede78d0be7270ba0c
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104516"
---
# <a name="teamsfx-library"></a>TeamsFx 库

Microsoft Teams框架 (TeamsFx) 是一个库， (封装常见功能和集成模式，例如简化对 Microsoft Identity) 的访问。 可以使用零配置为Microsoft Teams生成应用。

下面是主要 TeamsFx 功能的列表：

* **TeamsFx 协作**：让开发人员和项目所有者邀请其他协作者加入 TeamsFx 项目。 可以协作调试和部署 TeamsFx 项目。

* **TeamsFx CLI**：它加速Teams应用程序开发。 它还启用 CI/CD 方案，可将 CLI 集成到用于自动化的脚本中。

* **TeamsFx SDK**：TeamsFx 软件开发工具包 (SDK) 是主要的 TeamsFx 代码库，用于封装为Teams开发人员定制的客户端和服务器端代码的简单身份验证。

## <a name="teamsfx-command-line-interface"></a>TeamsFx 命令行接口

TeamsFx CLI 是基于文本的命令行接口，可加速应用程序开发Teams。 它旨在提供以键盘为中心的体验，同时构建Teams应用程序。 它还启用 CI/CD 方案，可将 CLI 集成到用于自动化的脚本中。

有关详细信息，请参阅：

* [源代码](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli)
* [ (NPM) 打包 ](https://www.npmjs.com/package/@microsoft/teamsfx-cli)

## <a name="get-started"></a>入门

安装`teamsfx-cli``npm`并运行`teamsfx -h`以检查所有可用命令：

```bash
  npm install -g @microsoft/teamsfx-cli
  teamsfx -h
```

## <a name="supported-commands"></a>支持的命令

| 命令 | 说明 |
|----------------|-------------|
| `teamsfx new`| 创建新的Teams应用程序。|
| `teamsfx account`| 管理云服务帐户。 支持的云服务为“Azure”和“Microsoft 365”。 |
| `teamsfx env` | 管理环境。 |
| `teamsfx capability`| 将新功能添加到当前应用程序。|
| `teamsfx resource`  | 管理当前应用程序中的资源。|
| `teamsfx provision` | 在当前应用程序中预配云资源。|
| `teamsfx deploy` | 部署当前应用程序。  |
| `teamsfx package` | 将Teams应用构建到用于发布的包中。|
| `teamsfx validate` | 验证当前应用程序。|
| `teamsfx publish` | 将应用发布到Teams。|
| `teamsfx preview` | 预览当前应用程序。 |
| `teamsfx config`  | 管理配置数据。 |
| `teamsfx permission`| 在同一项目中与其他开发人员协作。|

## `teamsfx new`

默认情况下，`teamsfx new`进入交互模式并指导你完成创建新Teams应用程序的过程。 也可以通过将标志设置为 `--interactive` 非交互模式来 `false`使用。

| `teamsFx new` 命令 | 说明 |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | 从现有模板创建应用 |
| `teamsfx new template list`     | 列出所有可用模板 |

### <a name="parameters-for-teamsfx-new"></a>参数 `teamsfx new`

| 参数 | 要求 | 说明 |
|:---------------- |:-------------|:-------------|
|`--app-name` | 是| Teams应用程序的名称。|
|`--interactive`| 否 | 以交互方式选择选项。 选项为 `true` ， `false` 默认值为 `true`。|
|`--capabilities`| 否| 选择Teams应用程序功能、多个选项和 `tab``messaging-extension` `bot``tab-spfx`。 默认值为 `tab`。|
|`--programming-language`| 否| 项目的编程语言。 选项为 `javascript` 或 `typescript` 默认值为 `javascript`。|
|`--folder`| 否 | Project目录。 在此目录下创建一个具有应用名称的子文件夹。 默认值为 `./`。|
|`--spfx-framework-type`| 否| 如果 `Tab(SPfx)` 选择了功能，则适用。 前端框架。 选项为 `none` 和 `react`，默认值为 `none`。|
|`--spfx-web part-name`| 否 | 如果 `Tab(SPfx)` 选择了功能，则适用。 默认值为“helloworld”。|
|`--spfx-web part-desp`| 否 | 如果 `Tab(SPfx)` 选择了功能，则适用。 默认值为“helloworld description”。 |
|`--azure-resources`| 否| 如果包含功能，则适用 `tab` 。 将 Azure 资源添加到项目。 多个选项 (Azure SQL 数据库) `sql` 和`function` (Azure Functions) 。 |

### <a name="scenarios-for-teamsfx-new"></a>方案 `teamsfx new`

可以使用交互模式创建Teams应用。用于控制所有参数`teamsfx new`的方案如下所示：

#### <a name="tab-app-hosted-on-spfx-using-react"></a>使用React托管在SPFx上的 Tab 应用

```bash
teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
```

#### <a name="teams-app-in-javascript-with-tab-bot-capabilities-and-azure-functions"></a>在 JavaScript 中Teams具有选项卡、机器人功能和Azure Functions的应用

```bash
teamsfx new --interactive false --app-name newtabbotapp --capabilities tab bot --programming-language javascript --azure-resources function
```

#### <a name="teams-tab-app-with-azure-functions-and-azure-sql"></a>Teams具有Azure Functions和Azure SQL的选项卡应用

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

### <a name="scenarios-for-teamsfx-env"></a>方案 `teamsfx env`

`teamsfx env`方案如下所示：

#### <a name="create-a-new-environment"></a>创建新环境

通过从现有开发环境复制来添加新环境：

```bash
teamsfx env add staging --env dev
```

## `teamsfx capability`

将新功能添加到当前应用程序。

| `teamsFx capability` 命令  | 说明 |
|:----------------  |:-------------|
| `teamsfx capability add tab` | 添加选项卡 |
| `teamsfx capability add bot` | 添加机器人 |
| `teamsfx capability add messaging-extension`| 添加 messagE 扩展 |

> [!NOTE]
> 如果项目包含机器人，则无法添加消息扩展，反之亦然。 创建新的Teams应用项目时，可以在项目中包括机器人和消息扩展。

## `teamsfx resource`

管理当前应用程序中的资源。 支持的 `<resource-type>` 有： `azure-sql`和 `azure-function` `azure-apim` .

| `teamsFx resource` 命令  | 说明 |
|:----------------  |:-------------|
| `teamsfx resource add <resource-type>`      | 将资源添加到当前应用程序。|
| `teamsfx resource show <resource-type>`      | 显示资源的配置详细信息。 |
| `teamsfx resource list`      | 列出当前应用程序中的所有资源。 |

### <a name="parameters-for-teamsfx-resource-add-azure-function"></a>参数 `teamsfx resource add azure-function`

| 参数  | 要求 | 说明 |
|----------------  |-------------|-------------|
|`--function-name`| 是 | 提供函数名称。 默认值为 `getuserprofile`。 |

### <a name="parameters-for-teamsfx-resource-add-azure-sql"></a>参数 `teamsfx resource add azure-sql`

#### `--function-name`

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--function-name`| 是 | 提供函数名称。 默认值为 `getuserprofile`。 |

> [!NOTE]
> 函数名称已验证为SQL，需要从服务器工作负荷进行访问。 如果项目不包含 `Azure Functions`，请为你创建一个。

### <a name="parameters-for-teamsfx-resource-add-azure-apim"></a>参数 `teamsfx resource add azure-apim`

> [!TIP]
> 尝试使用现有 `APIM` 实例时，这些选项会生效。 默认情况下，无需指定任何选项，并且会在步骤期间 `teamsfx provision` 创建新实例。

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--subscription`| 是 | 选择 Azure 订阅|
|`--apim-resource-group`| 是| 资源组的名称。 |
|`--apim-service-name`| 是 | API 管理服务实例的名称。 |
|`--function-name`| 是 | 提供函数名称。 默认值为 `getuserprofile`。 |

> [!NOTE]
> `Azure API Management` 需要使用 `Azure Functions`。 如果项目不包含 `Azure Functions`，可以创建一个。

## `teamsfx provision`

在当前应用程序中预配云资源。

### <a name="parameters-for-teamsfx-provision"></a>参数 `teamsfx provision`

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是| 为项目选择一个环境。 |
|`--subscription`| 否 | 指定 Azure 订阅 ID。 |
|`--resource-group`| 否 | 设置现有资源组的名称。 |
|`--sql-admin-name`| 否 | 当项目中有SQL资源时适用。 SQL的管理员名称。|
|`--sql-password`| 否| 当项目中有SQL资源时适用。 SQL的管理员密码。|

## `teamsfx deploy`

此命令用于部署当前应用程序。 默认情况下，它会部署整个项目，但也可以部分部署。 多个选项包括`frontend-hosting`：、`function`、`apim``teamsbot`和 `spfx`。

### <a name="parameters-for-teamsfx-deploy"></a>参数 `teamsfx deploy`

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是| 选择项目的现有环境。 |
|`--open-api-document`| 否 | 当项目中有 APIM 资源时适用。 打开的 API 文档文件路径。 |
|`--api-prefix`| 否 | 当项目中有 APIM 资源时适用。 API 名称前缀。 API 的默认唯一名称是 `{api-prefix}-{resource-suffix}-{api-version}`。 |
|`--api-version`| 否 | 当项目中有 APIM 资源时适用。 API 版本。 |

## `teamsfx validate`

验证当前应用程序。 此命令验证应用程序的清单文件。

### <a name="parameters-for-teamsfx-validate"></a>参数 `teamsfx validate`

`--env`：选择项目的现有环境。

## `teamsfx publish`

将应用发布到Teams。

### <a name="parameters-for-teamsfx-publish"></a>参数 `teamsfx publish`

`--env`：选择项目的现有环境。

## `teamsfx package`

将Teams应用构建到用于发布的包中。

## `teamsfx preview`

从本地或远程预览当前应用程序。

### <a name="parameters-for-teamsfx-preview"></a>参数 `teamsfx preview`

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--local`| 否 | 从本地预览应用程序。 `--local` 是独占与 `--remote`. |
|`--remote`| 否 | 从远程预览应用程序。 `--remote` 是独占与 `--local`. |
|`--env`| 否 | 追加参数 `--remote` 时，选择项目的现有环境。 |
|`--folder`| 否 | Project根目录。 默认值为 `./`。 |
|`--browser`| 否 | 要打开Teams Web 客户端的浏览器。 选项是 `chrome`， `edge` `default` 如系统默认浏览器，值为 `default`。 |
|`--browser-arg`| 否 | 要传递到浏览器的参数（需要 --browser）可以多次使用，例如--browser-args=“--guest” |
|`--sharepoint-site`| 否 | SharePoint站点 URL，例如`{your-tenant-name}.sharepoint.com`SPFx项目远程预览。 |

### <a name="scenarios-for-teamsfx-preview"></a>方案 `teamsfx preview`

#### <a name="local-preview"></a>本地预览版

依赖：

* Node.js
* .NET SDK
* Azure Functions核心工具

```bash
teamsfx preview --local
teamsfx preview --local --browser chrome
```

#### <a name="remote-preview"></a>远程预览版

```bash
teamsfx preview --remote
teamsfx preview --remote --browser edge
```

> [!NOTE]
> 后台服务的日志，如React保存在其中`~/.fx/cli-log/local-preview/`。

## `teamsfx config`

管理用户范围或项目范围内的配置数据。

| `teamsfx config` 命令  | 说明 |
|:----------------  |:-------------|
| `teamsfx config get [option]` | 查看选项的配置值 |
| `teamsfx config set <option> <value>` | 更新选项的配置值 |

### <a name="parameters-for-teamsfx-config"></a>参数 `teamsfx config`

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是 | 选择项目的现有环境。 |
|`--folder`| 否 | Project目录。 这用于获取或设置项目配置。 默认值为 `./`。 |
|`--global`| 否 | 配置的应对。 如果这是真的，则范围仅限于用户范围而不是项目范围。 默认值为 `false`。 目前，支持的全局配置包括`telemetry`： `validate-dotnet-sdk``validate-func-core-tools``validate-node` |

### <a name="scenerios-for-teamsfx-config"></a>Scenerios for `teamsfx config`

文件中的 `.userdata` 机密已加密， `teamsfx config` 可帮助你查看或更新值。

#### <a name="stop-sending-telemetry-data"></a>停止发送遥测数据

```bash
teamsfx config set telemetry off
```

#### <a name="disable-environment-checker"></a>禁用环境检查器

有三个配置需要打开或关闭Node.js、.NET SDK 和 Azure Functions Core Tools 验证，并且默认情况下启用所有这些配置。 如果不需要依赖项验证并想要自行安装依赖项，则可以将配置设置为“关闭”。 请查看以下指南：

* [Node.js安装指南](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
* [.NET SDK 安装指南](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk)
* [Azure Functions核心工具安装指南](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure-functions-core-tools)。

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
| `teamsfx permission grant --env --email` | 授予协作者对指定环境项目Microsoft 365帐户的权限。 |
| `teamsfx permission status` | 显示项目的权限状态 |

### <a name="parameters-for-teamsfx-permission-grant"></a>参数 `teamsfx permission grant`

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是 | 提供 env 名称。 |
|`--email`| 可访问 | 提供协作者Microsoft 365电子邮件地址。 确保协作者的帐户与创建者位于同一租户中。 |

### <a name="parameters-for-teamsfx-permission-status"></a>参数 `teamsfx permission status`

| 参数 | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是 | 提供 env 名称。 |
|`--list-all-collaborators` | 否 | 使用此标志，Teams Toolkit CLI 将打印此项目的所有协作者。 |

### <a name="scenarios-for-teamsfx-permission"></a>方案 `teamsfx permission`

项目的权 `TeamsFx` 限如下所示：

#### <a name="grant-permission"></a>授予权限

Project创建者和协作者可以使用`teamsfx permission grant`命令将新的协作者添加到项目中：

```bash
teamsfx permission grant --env dev --email user-email@user-tenant.com
```

获得所需的权限后，项目创建者和协作者可以通过GitHub与新协作者共享项目，并且新协作者可以拥有Microsoft 365帐户的所有权限。

#### <a name="show-permission-status"></a>显示权限状态

Project创建者和协作者可以使用`teamsfx permission status`命令查看特定 env 的Microsoft 365帐户权限：

```bash
teamsfx permission status --env dev
```

#### <a name="list-all-collaborators"></a>列出所有协作者

Project创建者和协作者可以使用`teamsfx permission status`命令查看特定 env 的所有协作者：

```bash
teamsfx permission status --env dev --list-all-collaborators
```

#### <a name="e2e-collaboration-work-flow-in-cli"></a>CLI 中的 E2E 协作工作流

作为项目创建者：

* 若要创建新的 TeamsFx 选项卡或机器人项目，并选择 Azure 作为主机类型：

  ```bash
  teamsfx new --interactive false --app-name newapp --host-type azure
  ```

* 登录到Microsoft 365帐户和 Azure 帐户：

  ```bash
  teamsfx account login azure
  teamsfx account login Microsoft 365
  ```

* 预配项目：

  ```bash
  teamsfx provision
  ```

* 若要查看协作者：

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-status-all-1.png" alt-text="permission-1":::

* 将另一个帐户添加为协作者。 确保添加的帐户位于同一租户下：

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-grant-1.png" alt-text="permission":::

* 将项目推送到GitHub

作为Project协作者：

* 从GitHub克隆项目。
* 登录到Microsoft 365帐户。 确保添加相同的Microsoft 365帐户：

  ```bash
  teamsfx account login Microsoft 365
  ```

* 使用所有 Azure 资源的参与者权限登录到 Azure 帐户。

  ```bash
  teamsfx account login azure
  ```

* 检查权限状态。 应发现自己拥有项目的所有者权限：

  ```bash
  teamsfx permission status --env dev
  ```

  ![权限状态](./images/permission-status.png)

* 更新 Tab 代码，并将项目部署到远程。
* 启动远程设备，项目应正常工作。

## <a name="see-also"></a>另请参阅

* [用于 TypeScript 或 JavaScript 的 TeamsFx SDK](TeamsFx-SDK.md)
* [在 Teams 工具包中管理多个环境](TeamsFx-multi-env.md)
* [使用Teams Toolkit协作处理Teams项目](TeamsFx-collaboration.md)
* [Teams 工具包概述](teams-toolkit-fundamentals.md)
