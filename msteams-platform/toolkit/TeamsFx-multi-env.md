---
title: TeamsFX Teams Toolkit
author: MuyangAmigo
description: 关于 TeamsFX 多环境
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: 0e53d90dd6ead30200dd1f07ba9a100a3d1f4ca1
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227977"
---
# <a name="manage-multiple-environments-in-teams-toolkit"></a>在环境中管理Teams Toolkit

 Teams Toolkit开发人员提供了一种简单方法，用于创建和管理多个环境、预配项目以及将项目部署到 Teams App 的目标环境。

 对于多个环境，开发人员可以：

1. **生产前测试**：在新式应用开发生命周期中将 Teams 应用发布到生产环境之前，通常先设置多个环境 (开发、测试、暂存) 。

2. **管理不同环境中的应用行为**：开发人员可以设置不同环境的不同行为，例如开发人员可能想要在生产环境中启用遥测，但在开发环境中禁用遥测。

## <a name="prerequisite"></a>先决条件

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

>[!TIP]
> 你应该已经拥有一个Teams VS 代码打开的应用项目。

## <a name="create-a-new-environment"></a>创建新环境

创建新项目后，默认情况下Teams Toolkit创建：

- 一 `local` 个表示本地计算机环境配置的环境。
- 一 `dev` 个表示远程/云环境配置的环境。

> [!NOTE]
> 每个项目只能有一个 `local` 环境，但有多个远程环境。

若要添加另一个远程环境，请选择边栏中的"Teams"图标，单击"环境"部分下的"加号"按钮，然后按照要创建的问题操作，如下图所示：

![add-env](./images/create-env.png)

> [!NOTE]
> 如果您具有多个现有环境，则需要选择一个现有环境来创建环境。 该命令将所选现有环境的文件内容和文件内容复制到 `config.<newEnv>.json` `azure.parameters.<newEnv>.json` 要创建的新环境中。

## <a name="select-target-environment"></a>选择目标环境 

随着环境中引入Teams Toolkit，对于所有与环境相关的操作，您可以选择要针对其执行操作的目标环境。 当你具有多个远程环境时，工具包将提示并请求目标环境，如下图所示：

![选择 env](./images/select-env.png)

## <a name="project-folder-structure"></a>Project文件夹结构 

创建项目后，可以查看项目资源管理器区域中的项目文件夹和Visual Studio Code。 除了自定义代码之外，某些文件Teams Toolkit用于维护应用配置、状态和模板。 下面列出了这些文件并概述了它们与多个环境的关系。

- `.fx/configs`：用户可以为应用自定义的配置文件Teams配置文件。
  - `config.<envName>.json`：每个环境的配置文件。
  - `azure.parameters.<envName>.json`：Azure BICEP 预配的按环境参数文件。
  - `projectSettings.json`：全局项目设置，适用于所有环境。
  - `localSettings.json`：本地调试配置文件。
- `.fx/states`：设置由组生成Toolkit。
  - `state.<envName>.json`：按环境设置输出文件。
  - `<env>.userdata`：预配输出的针对每个环境的敏感用户数据。
- `templates`
  - `appPackage`：应用清单模板文件。
  - `azure`：BICEP 模板文件。

## <a name="customize-the-provision"></a>自定义预配 

Teams Toolkit可以更改配置文件和模板文件，以自定义每个环境中的资源设置。

下表列出了自定义预配支持的常见方案以及自定义位置：

| 应用场景 | 自定义位置 | 如何自定义 |
| --- | --- | --- |
| 自定义 Azure 资源 | <ul> <li>下的 BICEP 文件 `templates/azure` 。</li> <li>`.fx/azure.parameters.<envName>.json`.</li></ul> | 有关 [更多详细信息ARM请参阅自定义自定义参数](provision.md#customize-arm-parameters-and-templates) 和模板。 |
| 为 AAD 应用Teams现有应用程序 | <ul> <li>`auth` 中的 部分 `.fx/config.<envName>.json` 。</li> </ul> | 有关[更多详细信息，请参阅AAD现有 Teams 应用](provision.md#use-an-existing-aad-app-for-your-teams-app)。 |
| 重新使用现有AAD自动程序应用 | <ul> <li>`bot` 中的 部分 `.fx/config.<envName>.json` 。</li> </ul> | 有关[更多详细信息，请参阅AAD自动程序使用](provision.md#use-an-existing-aad-app-for-your-bot)现有应用。 |
| 预配用户时跳过添加SQL | <ul> <li>`skipAddingSqlUser` 中的 属性 `.fx/config.<envName>.json` 。</li> </ul> | 有关更多详细信息[，请参阅SQL添加](provision.md#skip-adding-user-for-sql-database)用户。 |
| 自定义应用清单 | <ul> <li>`templates/manifest.remote.template.json`.</li> <li>`manifest` 中的 部分 `.fx/config.<envName>.json` 。</li>  </ul> | 有关更多详细信息[，Teams自定义 Teams Toolkit](TeamsFx-manifest-customization.md)中的应用程序清单。 |

## <a name="scenarios"></a>应用场景

### <a name="scenario-1-customize-teams-app-name-for-different-environment"></a>方案 1：为Teams自定义应用名称

此示例将了解如何为默认环境和暂存Teams将应用名称 `myapp(dev)` `dev` 设置为 `myapp(staging)` `staging` 。

请按照自定义步骤操作：

- 步骤 1：打开 `.fx/configs/config.dev.json` 配置文件。
- 步骤 2：将 manifest > *appName >更新为*`myapp(dev)`

  更新 `.fx/configs/config.dev.json` 到 ：

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

- 步骤 3：创建名为 `staging` 的新环境（如果不存在）。
- 步骤 4：打开 `.fx/configs/config.staging.json` 配置文件。
- 步骤 5：将步骤 2 的相同属性更新为 `myapp(staging)` 。
- 步骤 6：针对 和环境运行预配 `dev` `staging` 命令以更新远程环境中的应用名称。 了解如何使用命令运行预配Teams Toolkit。 有关详细信息，请参阅 [此文档](provision.md#provision-using-teams-toolkit)。

### <a name="scenario-2-customize-teams-app-description-for-different-environment"></a>方案 2：为Teams自定义应用说明

在此方案中，你将了解如何为不同的Teams设置不同的应用描述：

- 对于默认环境 `dev` ，说明将为 `my app description for dev` ;
- 对于暂存 `staging` 环境，描述将为 `my app description for staging` ;

执行自定义的步骤：

- 步骤 1：打开 `.fx/configs/config.dev.json` 配置文件。
- 步骤 2：将清单的新属性> description > *值为 的* `my app description for dev` short。

  更新到 `.fx/configs/config.dev.json`

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

- 步骤 3：创建一个名为 `staging` 的新环境（如果不存在）。
- 步骤 4：打开 `.fx/configs/config.staging.json` 配置文件。
- 步骤 5：将步骤 2 的相同属性添加到 `my app description for staging` 。
- 步骤 6：打开Teams应用程序清单模板 `templates/appPackage/manifest.remote.template.json` 。
- 步骤 7：更新 属性， `description > short` 以使用配置文件中定义的变量和 mustache 语法 `{{config.manifest.description.short}}` 。
  
  更新 `manifest.remote.template.json` 到 ：

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
- 步骤 8：针对 和环境运行预配 `dev` `staging` 命令以更新远程环境中的应用名称。 有关如何使用命令运行预配Teams Toolkit，请参阅[本文档了解](provision.md#provision-using-teams-toolkit)更多详细信息。

### <a name="scenario-3-customize-teams-app-description-for-all-environments"></a>方案 3：Teams所有环境自定义应用说明

在此方案中，你将了解如何针对所有环境Teams `my app description` 应用的说明。

当Teams清单模板在所有环境中共享时，我们可以针对目标更新它的说明值：

- 步骤 1：打开Teams应用程序清单模板 `templates/appPackage/manifest.remote.template.json` 。
- 步骤 2：使用硬 `description > short` 编码 **字符串 更新 属性** `my app description` 。
  
  更新 `manifest.remote.template.json` 到 ：

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

- Step 3: run provision command against **all** environment to update the app name in remote environments. For how to run provision command with Teams Toolkit, you can refer to [this document](provision.md#provision-using-teams-toolkit) for more details.

### Scenario 4: customize Azure resources for different environment

You can customize Azure resources for each environment, for example specifying Azure Function name, by editing the environment corresponding `.fx/configs/azure.parameters.{env}.json` file.

For more information on BICEP template and parameter files, see [provision cloud resources](provision.md)

## See also

> [!div class="nextstepaction"]
> [Provision cloud resources](provision.md)

> [!div class="nextstepaction"]
> [Add more cloud resources](add-resource.md)

> [!div class="nextstepaction"]
> [Collaborate with other developers on Teams project](TeamsFx-collaboration.md)
