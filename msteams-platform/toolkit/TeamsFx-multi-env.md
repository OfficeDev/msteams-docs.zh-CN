---
title: TeamsFX 中有多个Teams Toolkit
author: MuyangAmigo
description: 关于 TeamsFX 多环境
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: 1c0bb7eb75ee982e7c08d3039e59f03fc7f18146
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768460"
---
# <a name="manage-multiple-environments-in-teams-toolkit"></a>在环境中管理Teams Toolkit

 Teams Toolkit提供了一种简单方法，用于创建和管理多个环境、预配项目以及将项目部署到 Teams App 的目标环境。

 对于多个环境，可以执行下列操作：

1. **生产前测试**：在新式应用开发生命周期中将 Teams 应用发布到生产环境之前设置多个环境（如开发、测试和暂存）是常见做法。

2. **管理不同环境中的应用行为**：你可以为多个环境设置不同的行为，例如，在生产环境中启用遥测，但在开发环境中禁用它。

## <a name="prerequisite"></a>先决条件

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!TIP]
> 确保你已Teams VS 代码打开的应用项目。

## <a name="create-a-new-environment"></a>创建新环境

创建新项目后，默认情况下Teams Toolkit创建：

- 一 `local` 个表示本地计算机环境配置的环境。
- 一 `dev` 个表示远程或云环境配置的环境。

> [!NOTE]
> 每个项目只能有一个 `local` 环境，但有多个远程环境。

若要添加另一个远程环境，请选择边栏中的"Teams"图标，选择"环境"部分下的"创建新环境"，如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="创建":::

> [!NOTE]
> 如果您具有多个现有环境，则需要选择一个现有环境来创建相同的环境。 该命令将所选现有环境的文件内容和文件内容复制到 `config.<newEnv>.json` `azure.parameters.<newEnv>.json` 要创建的新环境中。

## <a name="select-target-environment"></a>选择目标环境 

您可以选择所有与环境相关的操作的目标环境。 当你具有多个远程环境时，工具包会提示并请求目标环境，如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="添加 env":::

## <a name="project-folder-structure"></a>Project文件夹结构 

创建项目后，可以查看项目资源管理器区域中的项目文件夹和Visual Studio Code。 除了自定义代码之外，某些Teams Toolkit还用于维护应用的配置、状态和模板。 以下列表提供了文件并概述了它们与多个环境的关系。

- `.fx/configs`：配置用户可为应用自定义Teams文件。
  - `config.<envName>.json`：每个环境的配置文件。
  - `azure.parameters.<envName>.json`：Azure bicep 预配的按环境参数文件。
  - `projectSettings.json`：全局项目设置，适用于所有环境。
  - `localSettings.json`：本地调试配置文件。
- `.fx/states`：设置由组生成Toolkit。
  - `state.<envName>.json`：按环境设置输出文件。
  - `<env>.userdata`：预配输出的针对每个环境的敏感用户数据。
- `templates`
  - `appPackage`：应用清单模板文件。
  - `azure`：Bicep 模板文件。

## <a name="customize-the-provision"></a>自定义预配 

Teams Toolkit可以更改配置文件和模板文件，以自定义每个环境中的资源设置。

下表列出了自定义设置支持的常见方案以及自定义位置：

| 应用场景 | 位置| 说明 |
| --- | --- | --- |
| 自定义 Azure 资源 | <ul> <li>下的 Bicep 文件 `templates/azure` 。</li> <li>`.fx/azure.parameters.<envName>.json`.</li></ul> | [自定义ARM和模板](provision.md#customize-arm-parameters-and-templates)。 |
| 为应用AAD现有Teams应用程序 | <ul> <li>`auth` 中的 部分 `.fx/config.<envName>.json` 。</li> </ul> |  [为应用AAD现有Teams应用](provision.md#use-an-existing-aad-app-for-your-teams-app)。 |
| 重用现有AAD自动程序应用 | <ul> <li>`bot` 中的 部分 `.fx/config.<envName>.json` 。</li> </ul> | [为自动AAD现有应用](provision.md#use-an-existing-aad-app-for-your-bot)。 |
| 预配用户时跳过添加SQL | <ul> <li>`skipAddingSqlUser` 中的 属性 `.fx/config.<envName>.json` 。</li> </ul> | [跳过为数据库 SQL用户](provision.md#skip-adding-user-for-sql-database)。 |
| 自定义应用清单 | <ul> <li>`templates/manifest.remote.template.json`.</li> <li>`manifest` 中的 部分 `.fx/config.<envName>.json` 。</li>  </ul> | [在 Teams 中自定义应用Teams Toolkit。](TeamsFx-manifest-customization.md) |

## <a name="scenarios"></a>应用场景

### <a name="scenario-1-customize-teams-app-name-for-different-environment"></a>方案 1：Teams不同的环境自定义应用名称

你可以为默认Teams和暂存环境将应用 `myapp(dev)` `dev` `myapp(staging)` 名称设置为 `staging` 。

执行以下步骤进行自定义：

- 1. 打开配置文件 `.fx/configs/config.dev.json` 。
- 2. 将 manifest 属性 *更新为 > appName > short*`myapp(dev)`

  更新 `.fx/configs/config.dev.json` 如下所示：

  ```json
  {
      "$schema": "https://aka.ms/teamsfx-env-config-schema",
      "description": "You can customize the TeamsFx config for different environments.   Visit https://aka.ms/teamsfx-env-config to learn more about this.",
      "manifest": {
          "appName": {
              "short": "myapp(dev)"
              ...
          }
      }
      ...
  }
  ```

- 3. 创建新环境，如果 `staging` 不存在，则命名它。
- 4. 打开配置文件 `.fx/configs/config.staging.json` 。
- 5. 更新同一属性 `myapp(staging)` 。
- 6. 在 和 环境中运行 `dev` `staging` 预配命令以更新远程环境中的应用名称。 若要使用命令运行预配Teams Toolkit，请参阅[provision](provision.md#provision-using-teams-toolkit)。

### <a name="scenario-2-customize-teams-app-description-for-different-environment"></a>方案 2：为Teams自定义应用说明

在此方案中，你将了解如何为不同的环境Teams不同的应用说明：

- 对于默认环境 `dev` ，说明将为 `my app description for dev` ;
- 对于暂存 `staging` 环境，描述将为 `my app description for staging` ;

执行以下步骤进行自定义：

- 1. 打开配置文件 `.fx/configs/config.dev.json` 。
- 2. 将清单的新 *属性> description > short* with value `my app description for dev` 。

  更新 `.fx/configs/config.dev.json` 如下所示：

  ```json
  {
      "$schema": "https://aka.ms/teamsfx-env-config-schema",
      "description": "You can customize the TeamsFx config for different environments.   Visit https://aka.ms/teamsfx-env-config to learn more about this.",
      "manifest": {
          ...
          "description": {
              "short": "`my app description for dev"
              ...
          }
      }
      ...
  }
  ```

- 3. 创建一个新环境，如果 `staging` 不存在，则命名它。
- 4. 打开配置文件 `.fx/configs/config.staging.json` 。
- 5. 将同一属性添加到 `my app description for staging` 。
- 6. 打开Teams应用程序清单模板 `templates/appPackage/manifest.remote.template.json` 。
- 7. 更新 属性 `description > short` 以使用 **在** 配置文件时定义的变量和 mustache 语法 `{{config.manifest.description.short}}` 。
  
  更新 `manifest.remote.template.json` 如下所示：

  ```json
  {
    "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    ...
    "description": {
      "short": "{{config.manifest.description.short}}", 
      ...
    },
    ...
  }
  ```
- 8. 针对 和环境运行 `dev` 预配 `staging` 命令以更新远程环境中的应用名称。 若要使用命令运行预配Teams Toolkit，请参阅[provision](provision.md#provision-using-teams-toolkit)。

### <a name="scenario-3-customize-teams-app-description-for-all-environments"></a>方案 3：自定义Teams环境的应用说明

在此方案中，你将了解如何针对所有环境Teams `my app description` 应用的说明。

当Teams清单模板在所有环境中共享时，我们可以针对目标更新它的说明值：

- 1. 打开Teams应用程序清单模板 `templates/appPackage/manifest.remote.template.json` 。
- 2. 使用硬 `description > short` 编码 **字符串 更新 属性** `my app description` 。
  
  更新 `manifest.remote.template.json` 如下所示：

  ```json
  {
    "$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.11/MicrosoftTeams.schema.json",
    "manifestVersion": "1.11",
    "version": "1.0.0",
    ...
    "description": {
      "short": "my app description",
      ...
    },
    ...
  }

- 3. Run provision command against **all** environment to update the app name in remote environments. To run provision command with Teams Toolkit, see [provision](provision.md#provision-using-teams-toolkit).

### Scenario 4: customize Azure resources for different environment

You can customize Azure resources for each environment, for example specify Azure Function name, by editing the environment corresponding to `.fx/configs/azure.parameters.{env}.json` file.

For more information on Bicep template and parameter files, see [provision cloud resources](provision.md)

## See also

* [Provision cloud resources](provision.md)
* [Add more cloud resources](add-resource.md)
* [Collaborate with other developers on Teams project](TeamsFx-collaboration.md)
