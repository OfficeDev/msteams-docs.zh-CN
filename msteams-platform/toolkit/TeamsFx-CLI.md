---
title: TeamsFx 命令行接口
author: MuyangAmigo
description: 描述 TeamsFx 命令行接口
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 33c67cc3ddd41d3c32ef95fe3b3360a0ad7f04fa
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768538"
---
# <a name="teamsfx-command-line-interface"></a>TeamsFx 命令行界面

TeamsFx CLI 是基于文本的命令行接口，可加速Teams开发。 它旨在提供以键盘为中心的体验，同时构建Teams应用程序。 它还支持 CI/CD 方案，可在其中将 CLI 集成到脚本中实现自动化。

有关更多信息，请参阅：
* [源代码](https://github.com/OfficeDev/TeamsFx/tree/dev/packages/cli) 
* [包 (NPM) ](https://www.npmjs.com/package/@microsoft/teamsfx-cli)

## <a name="get-started"></a>入门

安装 `teamsfx-cli` 并 `npm` 运行 `teamsfx -h` 以检查所有可用命令：

```bash
  npm install -g @microsoft/teamsfx-cli
  teamsfx -h
```

## <a name="supported-commands"></a>支持的命令

| 命令 | 说明 |
|----------------|-------------|
| `teamsfx new`| 创建新的 Teams 应用程序。|
| `teamsfx account`| 管理云服务帐户。 支持的云服务为"Azure"和"Microsoft 365"。 |
| `teamsfx env` | 管理环境。 |
| `teamsfx capability`| 向当前应用程序添加新功能。|
| `teamsfx resource`  | 管理当前应用程序中的资源。|
| `teamsfx provision` | 在当前应用程序中预配云资源。|
| `teamsfx deploy` | 部署当前应用程序。  |
| `teamsfx package` | 将你的Teams生成到要发布包中。|
| `teamsfx validate` | 验证当前应用程序。|
| `teamsfx publish` | 将应用发布到Teams。|
| `teamsfx preview` | 预览当前应用程序。 |
| `teamsfx config`  | 管理配置数据。 |
| `teamsfx permission`| 与同一项目中的其他开发人员协作。|

## `teamsfx new`

默认情况下， `teamsfx new` 将进入交互式模式，并指导你完成创建新应用程序Teams过程。 您也可以将标志设置为 ，以使用非交互 `--interactive` 模式 `false` 。

| `teamsFx new` 命令 | 说明 |
|:----------------  |:-------------|
| `teamsfx new template <template-name>`     | 从现有模板创建应用 |
| `teamsfx new template list`     | 列出所有可用模板 |

### <a name="parameters-for-teamsfx-new"></a>参数 `teamsfx new`

| 参数 | 要求 | 说明 |
|:---------------- |:-------------|:-------------|
|`--app-name` | 是| 应用程序的名称Teams应用程序。|
|`--interactive`| 不支持 | 以交互方式选择选项。 选项为 `true` 和 `false` ，默认值为 `true` 。|
|`--capabilities`| 不支持| Choose Teams application capabilities， the multiple options are `tab` ， `bot` ， and `messaging-extension` `tab-spfx` . 默认值为 `tab`。|
|`--programming-language`| 不支持| 项目的编程语言。 选项为 `javascript` 或 `typescript` ，默认值为 `javascript` 。|
|`--folder`| 不支持 | Project目录。 在此目录下创建具有应用名称的子文件夹。 默认值为 `./`。|
|`--spfx-framework-type`| 不支持| 如果选择了 `Tab(SPfx)` 功能，则适用。 前端框架。 选项为 `none` 和 `react` ，默认值为 `none` 。|
|`--spfx-web part-name`| 不支持 | 如果选择了 `Tab(SPfx)` 功能，则适用。 默认值为"helloworld"。|
|`--spfx-web part-desp`| 不支持 | 如果选择了 `Tab(SPfx)` 功能，则适用。 默认值为"helloworld description"。 |
|`--azure-resources`| 不支持| 如果包含功能， `tab` 适用。 将 Azure 资源添加到你的项目。 Azure Functions (Azure SQL 数据库) `sql` (`function` 多个) 。 |

### <a name="scenarios-for-teamsfx-new"></a>应用场景 `teamsfx new`

可以使用交互模式创建Teams应用。用于控制所有参数的方案 `teamsfx new` 如下所示：

#### <a name="tab-app-hosted-on-spfx-using-react"></a>使用选项卡托管在 SPFx 上的选项卡React

```bash
teamsfx new --interactive false --app-name newspfxapp --capabilities tab-spfx --spfx-framework-type react
```

#### <a name="teams-app-in-javascript-with-tab-bot-capabilities-and-azure-functions"></a>Teams JavaScript 中提供选项卡、自动程序功能和 Azure 函数的应用

```bash
teamsfx new --interactive false --app-name newtabbotapp --capabilities tab bot --programming-language javascript --azure-resources function
```

#### <a name="teams-tab-app-with-azure-functions-and-azure-sql"></a>Teams Azure Functions 和 Azure SQL 选项卡应用

```bash
teamsfx new --interactive false app-name newapp --azure-resources sql function --programming-language typescript
```

## `teamsfx account`

管理云服务帐户。 支持的云服务是 `Azure` 和 `Microsoft 365` 。

| `teamsFx account` 命令 | 说明 |
|:----------------  |:-------------|
| `teamsfx account login <service>`  | 登录到所选的云服务。 |
| `teamsfx account logout <service>`  | 注销所选云服务。 |
| `teamsfx account set --subscription` | 更新帐户设置以设置订阅 ID。 |

## `teamsfx env`

管理环境。

| `teamsfx env` 命令  | 说明 |
|:----------------  |:-------------|
| `teamsfx env add <new_env_name> --env <existing_env_name>` | 通过从指定环境复制来添加新环境。 |
| `teamsfx env list` | 列出所有环境。 |

### <a name="scenarios-for-teamsfx-env"></a>应用场景 `teamsfx env`

方案 `teamsfx env` 如下：

#### <a name="create-a-new-environment"></a>创建新环境

通过从现有开发环境中复制来添加新环境：

```bash
teamsfx env add staging --env dev
```

## `teamsfx capability`

向当前应用程序添加新功能。

| `teamsFx capability` 命令  | 说明 |
|:----------------  |:-------------|
| `teamsfx capability add tab` | 添加选项卡 |
| `teamsfx capability add bot` | 添加自动程序 |
| `teamsfx capability add messaging-extension`| 添加消息传递扩展 |

> [!NOTE]
> 如果项目包含自动程序，则不能添加消息扩展，反之亦然。 在创建新应用项目时，可以在项目中包括自动程序扩展Teams消息扩展。

## `teamsfx resource`

管理当前应用程序中的资源。 支持 `<resource-type>` 包括： `azure-sql` 和 `azure-function` `azure-apim` 。

| `teamsFx resource` 命令  | 说明 |
|:----------------  |:-------------|
| `teamsfx resource add <resource-type>`      | 将资源添加到当前应用程序中。|
| `teamsfx resource show <resource-type>`      | 显示资源的配置详细信息。 |
| `teamsfx resource list`      | 列出当前应用程序的所有资源。 |

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
> 函数名称被验证为SQL需要从服务器工作负载访问。 如果项目不包含 ，请 `Azure Functions` 创建一个。

### <a name="parameters-for-teamsfx-resource-add-azure-apim"></a>参数 `teamsfx resource add azure-apim`

> [!TIP]
> 这些选项在您尝试使用现有实例时 `APIM` 生效。 默认情况下，不必指定任何选项，并且它会在步骤期间创建新 `teamsfx provision` 实例。

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--subscription`| 是 | 选择 Azure 订阅|
|`--apim-resource-group`| 是| 资源组的名称。 |
|`--apim-service-name`| 是 | API 管理服务实例的名称。 |
|`--function-name`| 是 | 提供函数名称。 默认值为 `getuserprofile`。 |

> [!NOTE]
> `Azure API Management` 需要与 一起 `Azure Functions` 工作。 如果项目不包含 ， `Azure Functions` 可以创建一个。

## `teamsfx provision`

在当前应用程序中预配云资源。

### <a name="parameters-for-teamsfx-provision"></a>参数 `teamsfx provision`

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是| 选择项目的环境。 |
|`--subscription`| 不支持 | 指定 Azure 订阅 ID。 |
|`--resource-group`| 不支持 | 设置现有资源组的名称。 |
|`--sql-admin-name`| 不支持 | 当项目中存在SQL资源时适用。 管理员的管理员SQL。|
|`--sql-password`| 不支持| 当项目中存在SQL资源时适用。 管理员密码SQL。|

## `teamsfx deploy`

此命令用于部署当前应用程序。 默认情况下，它部署整个项目，但也可以部分部署。 多个选项包括 `frontend-hosting` `function` `apim` 、、、 `teamsbot` 和 `spfx` 。

### <a name="parameters-for-teamsfx-deploy"></a>参数 `teamsfx deploy`

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是| 为项目选择现有环境。 |
|`--open-api-document`| 不支持 | 在项目中存在 APIM 资源时适用。 打开的 API 文档文件路径。 |
|`--api-prefix`| 不支持 | 在项目中存在 APIM 资源时适用。 API 名称前缀。 API 的默认唯一名称是 `{api-prefix}-{resource-suffix}-{api-version}` 。 |
|`--api-version`| 不支持 | 在项目中存在 APIM 资源时适用。 API 版本。 |

## `teamsfx validate`

验证当前应用程序。 此命令验证应用程序的清单文件。

### <a name="parameters-for-teamsfx-validate"></a>参数 `teamsfx validate`

`--env`：为项目选择现有环境。

## `teamsfx publish`

将应用发布到Teams。

### <a name="parameters-for-teamsfx-publish"></a>参数 `teamsfx publish`

`--env`：为项目选择现有环境。

## `teamsfx package`

将你的Teams应用构建到一个包中以用于发布。

## `teamsfx preview`

从本地或远程预览当前应用程序。

### <a name="parameters-for-teamsfx-preview"></a>参数 `teamsfx preview`

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--local`| 否 | 从本地预览应用程序。 `--local` 与 独占 `--remote` 。 |
|`--remote`| 不支持 | 从远程预览应用程序。 `--remote` 与 独占 `--local` 。 |
|`--env`| 不支持 | 追加参数时，选择 `--remote` 项目的现有环境。 |
|`--folder`| 不支持 | Project根目录。 默认值为 `./`。 |
|`--browser`| 不支持 | 要打开 Web Teams的浏览器。 选项为 `chrome` ， `edge` 如 `default` 系统默认浏览器，值为 `default` 。 |
|`--browser-arg`| 不支持 | 要传递到浏览器的参数需要 --browser，可以多次使用，例如，--browser-args="--guest" |
|`--sharepoint-site`| 不支持 | SharePoint网站 URL，例如 `{your-tenant-name}.sharepoint.com` SPFx项目远程预览。 |

### <a name="scenarios-for-teamsfx-preview"></a>应用场景 `teamsfx preview`

#### <a name="local-preview"></a>本地预览

依赖项：

- Node.js
- .NET SDK
- Azure 函数核心工具

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
> 后台服务的日志（如 React 保存在 中 `~/.fx/cli-log/local-preview/` 。

## `teamsfx config`

在用户范围或项目范围内管理配置数据。

| `teamsfx config` 命令  | 说明 |
|:----------------  |:-------------|
| `teamsfx config get [option]` | 查看选项的配置值 |
| `teamsfx config set <option> <value>` | 更新选项的配置值 |

### <a name="parameters-for-teamsfx-config"></a>参数 `teamsfx config`

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是 | 为项目选择现有环境。 |
|`--folder`| 不支持 | Project目录。 这用于获取或设置项目配置。 默认值为 `./`。 |
|`--global`| 不支持 | 配置处理。 如果为 true，则范围限制为用户范围，而不是项目范围。 默认值为 `false`。 目前，受支持的全局配置包括 `telemetry` `validate-dotnet-sdk` `validate-func-core-tools` 、、、。 `validate-node` |

### <a name="scenerios-for-teamsfx-config"></a>的场景子 `teamsfx config`

文件中 `.userdata` 的密码已加密 `teamsfx config` ，可帮助你查看或更新值。

#### <a name="stop-sending-telemetry-data"></a>停止发送遥测数据

```bash
teamsfx config set telemetry off
```

#### <a name="disable-environment-checker"></a>禁用环境检查器

有三种配置可以打开或关闭Node.js.NET SDK 和 Azure Functions 核心工具验证，默认情况下，所有这些配置都已启用。 如果不需要依赖关系验证并且想要自行安装依赖项，可以将配置设置为"关闭"。 查看以下指南：
* [Node.js安装指南](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-nodejs)
* [.NET SDK 安装指南](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-net-sdk) 
* [Azure Functions 核心工具安装指南](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/vscode-extension/envchecker-help.md#how-to-install-azure-functions-core-tools)。

若要禁用 .NET SDK 验证，可以使用以下命令：

```bash
teamsfx config set validate-dotnet-sdk off
```

若要启用 .NET SDK 验证，可以使用以下命令：

```bash
teamsfx config set validate-dotnet-sdk on
```

#### <a name="view-all-the-user-scope-configuration"></a>查看所有用户作用域配置

```bash
teamsfx config get -g
```

#### <a name="view-all-the-configuration-in-project"></a>查看项目中的所有配置

密码将自动解密：

```bash
teamsfx config get --env dev
```

#### <a name="update-the-secret-configuration-in-project"></a>更新项目中的机密配置

```bash
teamsfx config set fx-resource-aad-app-for-teams.clientSecret xxx --env dev
```

## `teamsfx permission`

TeamsFx CLI 提供 `teamsFx permission` 协作方案的命令。

| `teamsFx permission` command | 说明 |
|:------------------------------|-------------|
| `teamsfx permission grant --env --email` | 为协作者的Microsoft 365指定环境的项目授予权限。 |
| `teamsfx permission status` | 显示项目的权限状态 |

### <a name="parameters-for-teamsfx-permission-grant"></a>参数 `teamsfx permission grant`

| 参数  | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是 | 提供 env 名称。 |
|`--email`| 是 | 提供协作者的Microsoft 365电子邮件地址。 确保协作者的帐户与创建者位于同一租户中。 |

### <a name="parameters-for-teamsfx-permission-status"></a>参数 `teamsfx permission status`

| 参数 | 要求 | 说明 |
|:----------------  |:-------------|:-------------|
|`--env`| 是 | 提供 env 名称。 |
|`--list-all-collaborators` | 不支持 | 通过此标志，Teams Toolkit CLI 打印此项目的所有协作者。 |

### <a name="scenarios-for-teamsfx-permission"></a>应用场景 `teamsfx permission`

项目的权限 `TeamsFx` 如下所示：

#### <a name="grant-permission"></a>授予权限

Project创建者和协作者可以使用命令 `teamsfx permission grant` 将新的协作者添加到项目中：

```bash
teamsfx permission grant --env dev --email user-email@user-tenant.com
```

收到所需权限后，项目创建者和协作者可以通过 GitHub 与新协作者共享项目，并且新协作者可以拥有 Microsoft 365 帐户的所有权限。

#### <a name="show-permission-status"></a>显示权限状态

Project创建者和协作者可以使用命令查看他的Microsoft 365 `teamsfx permission status` 特定 env 的帐户权限：

```bash
teamsfx permission status --env dev
```

#### <a name="list-all-collaborators"></a>列出所有协作者

Project创建者和协作者可以使用 `teamsfx permission status` 命令查看特定 env 的所有协作者：

```bash
teamsfx permission status --env dev --list-all-collaborators
```

#### <a name="e2e-collaboration-work-flow-in-cli"></a>CLI 中的 E2E 协作工作流程

作为项目创建者：

- 若要创建新的 TeamsFx 选项卡或自动程序项目，然后选择 Azure 作为主机类型：

  ```bash
  teamsfx new --interactive false --app-name newapp --host-type azure
  ```

- 若要登录到 Microsoft 365 帐户和 Azure 帐户：

  ```bash
  teamsfx account login azure
  teamsfx account login Microsoft 365
  ```

- 设置项目：

  ```bash
  teamsfx provision
  ```

- 查看协作者：

  ```bash
  teamsfx permission status --env dev --list-all-collaborators
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-status-all-1.png" alt-text="permission-1":::

- 添加另一个帐户作为协作者。 确保添加的帐户位于同一租户下：

  ```bash
  teamsfx permission grant --env dev --email user-email@user-tenant.com
  ```

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/permission-grant-1.png" alt-text="权限":::

- 将项目推送到GitHub

作为协作Project者：

- 从项目复制GitHub。
- 登录到 Microsoft 365 帐户。 确保添加相同的Microsoft 365帐户：

  ```bash
  teamsfx account login Microsoft 365
  ```

- 使用所有 Azure 资源的参与者权限登录到 Azure 帐户。

  ```bash
  teamsfx account login azure
  ```

- 检查权限状态。 你应该会发现自己拥有项目的所有者权限：

  ```bash
  teamsfx permission status --env dev
  ```
  ![权限状态](./images/permission-status.png)

- 更新选项卡代码，将项目部署到远程。
- 启动远程，项目应该可以正常工作。

## <a name="see-also"></a>另请参阅

* [适用于 TypeScript 或 JavaScript 的 TeamsFx SDK](TeamsFx-SDK.md)
* [在环境中管理Teams Toolkit](TeamsFx-multi-env.md)
* [使用Teams协作处理Teams Toolkit](TeamsFx-collaboration.md)
 