---
title: Teams 工具包中的 TeamsFX 多环境
author: MuyangAmigo
description: 在本模块中，了解 TeamsFX 多环境，例如，创建新环境、选择目标环境等
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: 6256c620d62233da2420b3dfa7cd53101bf92978
ms.sourcegitcommit: ca84b5fe5d3b97f377ce5cca41c48afa95496e28
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2022
ms.locfileid: "66143569"
---
# <a name="manage-multiple-environments"></a>管理多个环境

 Teams 工具包提供了一种简单方法来创建和管理多个环境、预配项目并将其部署到 Teams 应用的目标环境。

 可以对多个环境执行以下操作：

1. **生产前测试**：在将Teams应用发布到现代应用开发生命周期中的生产环境之前，可以设置多个环境，例如开发、测试和暂存。

2. **管理不同环境中的应用行为**：可以为多个环境设置不同的行为，例如在生产环境中启用遥测，但在开发环境中禁用遥测。

## <a name="prerequisite"></a>先决条件

* 安装 [最新版本的 Teams 工具包](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

> [!TIP]
> 确保已在 Visual Studio 代码中打开 Teams 应用项目。

## <a name="create-a-new-environment"></a>创建新环境

创建新项目后，默认情况下 Teams 工具包将创建：

* 一个 `local` 环境，用于表示本地计算机环境配置
* 一个 `dev` 环境，用于表示远程或云环境配置

> [!NOTE]
> 每个项目只能有一个 `local` 环境，但可以有多个远程环境。

若要 **添加另一个远程环境**，请执行以下操作：

1. 从左侧导航栏中选择 **Teams** :::image type="content" source="../assets/images/teams-toolkit-v2/add-sso/teams-toolkit-sidebar-icon.png" alt-text="sso 添加边栏":::。
2. 选择 **“+Teams：在”环境****“** 部分下创建新环境，如下图所示：

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="创建":::

   如果有多个环境，则需要选择一个现有环境来创建相同的环境。 该命令会将 `config.<newEnv>.json` 和 `azure.parameters.<newEnv>.json` 的文件内容从所选的现有环境复制到所创建的新环境。

## <a name="select-target-environment"></a>选择目标环境

可以为所有与环境相关的操作选择目标环境。 如果有多个远程环境，则工具包会提示并请求目标环境，如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="添加环境":::

## <a name="project-folder-structure"></a>项目文件夹结构

创建项目后，可以在VS Code中查看 **资源管理器** 下的项目文件夹和文件。 除了自定义代码，Teams Toolkit使用一些文件来维护应用的配置、状态和模板。 以下列表提供了文件，并概述了它们与多个环境的关系。

* `.fx/configs`：配置用户可以为Teams应用自定义的文件
  * `config.<envName>.json`：按环境配置文件
  * `azure.parameters.<envName>.json`：每个环境的 Azure bicep 预配参数文件
  * `projectSettings.json`：适用于所有环境的全局项目设置
* `.fx/states`：预配由Toolkit生成的结果
  * `state.<envName>.json`：按环境预配输出文件
  * `<env>.userdata`：每个环境预配输出的用户数据
* `templates`
  * `appPackage`：应用清单模板文件
  * `azure`：Bicep 模板文件

## <a name="customize-resource-provision"></a>自定义资源预配

Teams 工具包允许更改配置文件和模板文件，以自定义每个环境中的资源预配。

下表列出了自定义资源预配的常见方案：

| 应用场景 | 位置| 说明 |
| --- | --- | --- |
| 自定义 Azure 资源 | <ul> <li>`templates/azure` 下的 Bicep 文件</li> <li>`.fx/azure.parameters.<envName>.json`</li></ul> | [自定义 ARM 参数和模板](provision.md#customize-arm-parameters-and-templates) |
| 为 Teams 应用重复使用现有的 Azure AD 应用 | <ul> <li>`.fx/config.<envName>.json` 中的 `auth` 部分</li> </ul> |  [为 Teams 应用使用现有的 Azure AD 应用](provision.md#use-an-existing-azure-ad-app-for-your-teams-app) |
| 为机器人重复使用现有的 Azure AD 应用 | <ul> <li>`.fx/config.<envName>.json` 中的 `bot` 部分</li> </ul> | [为机器人使用现有的 Azure AD 应用](provision.md#use-an-existing-azure-ad-app-for-your-bot) |
| 在预配 SQL 时跳过添加用户 | <ul> <li>`.fx/config.<envName>.json` 中的 `skipAddingSqlUser` 属性</li> </ul> | [跳过为 SQL 数据库添加用户](provision.md#skip-adding-user-for-sql-database) |
| 自定义应用清单 | <ul> <li>`templates/manifest.template.json`</li> <li>`.fx/config.<envName>.json` 中的 `manifest` 部分</li>  </ul> | [工具包中的预览应用清单](TeamsFx-preview-and-customize-app-manifest.md)|

## <a name="scenarios"></a>应用场景

可以看到以下方案，用于自定义不同环境中的资源预配。
<br>

<br><details>
<summary><b>方案 1：为不同环境自定义Teams应用名称</b></summary>

可以将Teams应用名称`myapp(dev)`设置为默认环境`dev`和`myapp(staging)`过渡环境`staging`。

请按照以下步骤进行自定义：

1. 打开配置文件 `.fx/configs/config.dev.json`。
2. 将 *清单> appName 的属性>简短* 更新为 `myapp(dev)`。

  `.fx/configs/config.dev.json` 的更新如下所示：

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

3. 创建新环境，并在不存在时将其 `staging` 命名。
4. 打开配置文件 `.fx/configs/config.staging.json`。
5. 更新同一属性 `myapp(staging)`。
6. 在 `dev` 和 `staging` 环境中运行预配命令，以更新远程环境中的应用名称。 若要使用Teams Toolkit运行预配命令，请参阅[预配](provision.md#provision-using-teams-toolkit)。

</details>

<details>
<summary><b>方案 2：为不同环境自定义 Teams 应用说明</b></summary>

可以为不同的环境设置不同的Teams应用说明：

* 对于默认环境 `dev`，说明为 `my app description for dev`
* 对于暂存环境 `staging`，说明为 `my app description for staging`

请按照以下步骤进行自定义：

1. 打开配置文件 `.fx/configs/config.dev.json`。
2. 添加 *清单>说明的新属性>用* 值 `my app description for dev`短。

  `.fx/configs/config.dev.json` 的更新如下所示：

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

3. 创建新环境，并在不存在时将其 `staging` 命名。
4. 打开配置文件 `.fx/configs/config.staging.json`。
5. 将同一属性添加到 `my app description for staging`.
6. 打开Teams应用清单模板`templates/appPackage/manifest.template.json`。
7. 更新属性`description > short`以使用在配置具有胡子语法`{{config.manifest.description.short}}`的文件中定义的 **变量**。
  
  `manifest.template.json` 的更新如下所示：

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

8. 针对 `dev` 和 `staging` 环境运行预配命令，以更新远程环境中的应用名称。

</details>

<details>
<summary><b>方案 3：为所有环境自定义 Teams 应用说明</b></summary>

可以将Teams应用`my app description`的说明设置为所有环境。

由于 Teams 应用清单模板是在所有环境中共享的，因此我们可以为目标更新其中的说明值：

1. 打开Teams应用清单模板`templates/appPackage/manifest.template.json`。
2. 使用 **硬编码字符串**`my app description`更新属性`description > short`。
  
  `manifest.template.json` 的更新如下所示：

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

  ```

3. 针对 **所有** 环境运行预配命令，以更新远程环境中的应用名称。

</details>

<details>
<br><summary><b>方案 4：为不同的环境自定义 Azure 资源</b></summary>
可以为每个环境自定义 Azure 资源，例如编辑与 fx/configs/azure.parameters 对应的环境。{env}.json 文件，用于指定 Azure 函数名称。

有关 Bicep 模板和参数文件的详细信息，请参阅 [预配云资源](provision.md)
</details>
</br>

## <a name="see-also"></a>另请参阅

* [预配云资源](provision.md)
* [添加更多云资源](add-resource.md)
* [在 Teams 项目中与其他开发人员协作](TeamsFx-collaboration.md)
