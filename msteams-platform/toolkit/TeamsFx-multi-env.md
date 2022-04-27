---
title: Teams Toolkit中的 TeamsFX 多个环境
author: MuyangAmigo
description: 关于 TeamsFX 多环境
ms.author: nintan
ms.localizationpriority: medium
ms.topic: overview of multiple environment
ms.date: 11/29/2021
ms.openlocfilehash: 194c31d02424d08080dca981bb9fe6d963d0a416
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073081"
---
# <a name="manage-multiple-environments"></a>管理多个环境

 Teams Toolkit提供了一种简单的方法，用于创建和管理多个环境、预配项目并将其部署到Teams应用的目标环境。

 可以使用多个环境执行以下操作：

1. **生产前测试**：在将Teams应用发布到现代应用开发生命周期中的生产环境之前，可以设置多个环境，例如开发、测试和暂存

2. **管理不同环境中的应用行为**：可以为多个环境设置不同的行为，例如在生产环境中启用遥测，但在开发环境中禁用遥测

## <a name="prerequisite"></a>先决条件

* 安装 [最新版本的 Teams 工具包](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

> [!TIP]
> 请确保已在Microsoft Visual Studio代码中打开Teams应用项目。

## <a name="create-a-new-environment"></a>创建新环境

创建新项目后，默认情况下Teams Toolkit创建：

* 表示本地计算机环境配置的一个 `local` 环境
* 表示远程或云环境配置的一个 `dev` 环境

> [!NOTE]
> 每个项目只能有一个 `local` 环境，但可以有多个远程环境。

**若要添加另一个远程环境，请执行以下操作**：

1. 在边栏中选择 **Teams** 图标
2. 选择 **“+Teams：在”环境“部分下创建新环境**，如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="创建":::

如果有多个环境，则需要选择一个现有环境来创建相同的环境。 该命令将所选现有环境的文件内容 `config.<newEnv>.json` 复制 `azure.parameters.<newEnv>.json` 到创建的新环境。

## <a name="select-target-environment"></a>选择目标环境

可以为所有与环境相关的操作选择目标环境。 当有多个远程环境时，Toolkit会提示并请求目标环境，如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="add env":::

## <a name="project-folder-structure"></a>Project文件夹结构

创建项目后，可以在Visual Studio Code的资源管理器区域中查看项目文件夹和文件。 除了自定义代码，Teams Toolkit还使用一些文件来维护应用的配置、状态和模板。 以下列表提供文件，并概述了它们与多个环境的关系。

* `.fx/configs`：配置用户可以为Teams应用自定义的文件
  * `config.<envName>.json`：每个环境的配置文件 
  * `azure.parameters.<envName>.json`：Azure bicep 预配的每个环境参数文件
  * `projectSettings.json`：适用于所有环境的全局项目设置
* `.fx/states`：由Toolkit生成的预配结果
  * `state.<envName>.json`：按环境预配输出文件
  * `<env>.userdata`：预配输出的每个环境敏感用户数据
* `templates`
  * `appPackage`：应用清单模板文件
  * `azure`：Bicep 模板文件

## <a name="customize-resource-provision"></a>自定义资源预配

Teams Toolkit允许更改配置文件和模板文件，以自定义每个环境中的资源预配。

下表列出了自定义资源预配的常见方案：

| 应用场景 | 位置| 说明 |
| --- | --- | --- |
| 自定义 Azure 资源 | <ul> <li>Bicep 文件下 `templates/azure`</li> <li>`.fx/azure.parameters.<envName>.json`</li></ul> | [自定义 ARM 参数和模板](provision.md#customize-arm-parameters-and-templates) |
| 为Teams应用重复使用现有Azure AD应用 | <ul> <li>`auth` section in`.fx/config.<envName>.json`</li> </ul> |  [对Teams应用使用现有的Azure AD应用](provision.md#use-an-existing-azure-ad-app-for-your-teams-app) |
| 重复使用机器人的现有Azure AD应用 | <ul> <li>`bot` section in`.fx/config.<envName>.json`</li> </ul> | [为机器人使用现有的Azure AD应用](provision.md#use-an-existing-azure-ad-app-for-your-bot) |
| 在预配SQL时跳过添加用户 | <ul> <li>`skipAddingSqlUser` property in`.fx/config.<envName>.json`</li> </ul> | [跳过为SQL数据库添加用户](provision.md#skip-adding-user-for-sql-database) |
| 自定义应用清单 | <ul> <li>`templates/manifest.template.json`</li> <li>`manifest` section in `.fx/config.<envName>.json`</li>  </ul> | [在Teams Toolkit中自定义Teams应用清单](TeamsFx-manifest-customization.md) |

## <a name="scenarios"></a>应用场景

有四种方案用于自定义不同环境中的资源预配。
<br>

<br><details>
<summary><b>方案 1：为不同环境自定义Teams应用名称</b></summary>

可以将Teams应用名称`myapp(dev)`设置为默认环境`dev`和`myapp(staging)`过渡环境`staging`。

执行以下自定义步骤：

1. 打开配置文件 `.fx/configs/config.dev.json`
2. 将 *清单> appName 的属性>简短* 更新为 `myapp(dev)`

  `.fx/configs/config.dev.json`更新如下所示：

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

3. 创建新环境并将其命名（如果不存在）`staging`
4. 打开配置文件 `.fx/configs/config.staging.json`
5. 更新同一属性 `myapp(staging)`
6. 在 `dev` 和 `staging` 环境中运行预配命令以更新远程环境中的应用名称。 若要使用Teams Toolkit运行预配命令，请参阅[预配](provision.md#provision-using-teams-toolkit)
</details>
<br>


<details>
<summary><b>方案 2：为不同环境自定义Teams应用说明</b></summary>

在此方案中，你将了解如何为不同的环境设置不同的Teams应用说明：

* 对于默认环境 `dev`，说明为 `my app description for dev`
* 对于过渡环境 `staging`，说明是 `my app description for staging`

执行以下自定义步骤：

1. 打开配置文件 `.fx/configs/config.dev.json`
2. 添加 *清单>说明的新属性>用值短*`my app description for dev`

  `.fx/configs/config.dev.json`更新如下所示：

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

3. 创建新环境并将其命名（如果不存在）`staging`
4. 打开配置文件 `.fx/configs/config.staging.json`
5. 将同一属性添加到 `my app description for staging`
6. 打开Teams应用清单模板`templates/appPackage/manifest.template.json`
7. 更新属性`description > short`以使用在配置具有胡子语法的文件中定义的 **变量**`{{config.manifest.description.short}}`
  
  `manifest.template.json`更新如下所示：

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

8. 针对 `dev` 环境 `staging` 运行预配命令，以更新远程环境中的应用名称。 若要使用Teams Toolkit运行预配命令，请参阅[预配](provision.md#provision-using-teams-toolkit)

</details>
<br>

<details>
<summary><b>方案 3：自定义所有环境的Teams应用说明</b></summary>

在此方案中，你将了解如何为所有环境设置Teams应用`my app description`的说明。

由于Teams应用清单模板在所有环境中共享，因此我们可以为目标更新其中的说明值：

1. 打开Teams应用清单模板`templates/appPackage/manifest.template.json`
2. 使用 **硬编码字符串** 更新属性`description > short` `my app description`
  
  `manifest.template.json`更新如下所示：

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
3. 针对 **所有** 环境运行预配命令，以更新远程环境中的应用名称。 若要使用Teams Toolkit运行预配命令，请参阅[预配](provision.md#provision-using-teams-toolkit)
<br></details>
<br>
<details>
<br><summary><b>方案 4：为不同的环境自定义 Azure 资源</b></summary>
可以通过编辑与 fx/configs/azure.parameters 对应的环境，为每个环境自定义 Azure 资源，例如指定 Azure 函数名称。{env}.json。 文件。

有关 Bicep 模板和参数文件的详细信息，请参阅 <br [预配云资源](provision.md)
</details>



## <a name="see-also"></a>另请参阅

* [预配云资源](provision.md)
* [添加更多云资源](add-resource.md)
* [在 Teams 项目中与其他开发人员协作](TeamsFx-collaboration.md)