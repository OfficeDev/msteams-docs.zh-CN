---
title: Teams 工具包中的 TeamsFX 多环境
author: surbhigupta
description: 在本模块中，了解 TeamsFX 多环境，例如，创建新环境、选择目标环境等
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: conceptual
ms.date: 11/29/2021
ms.openlocfilehash: 4a4b67399b2ec7c78fa536b06ee7faa9bb352468
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616940"
---
# <a name="manage-multiple-environments"></a>管理多个环境

 Microsoft Teams 工具包提供了一种简单的方法，可用于创建和管理多个环境、预配项目以及将项目部署到 Microsoft Teams 应用的目标环境。

 可以使用多个环境执行以下操作：

1. **生产前测试**：可以在现代应用开发生命周期中将 Teams 应用发布到生产环境之前设置多个环境，例如开发、测试和暂存。

2. **管理不同环境中的应用行为**：可以为多个环境设置不同的应用行为，例如在生产环境中启用遥测。

   > [!NOTE]
   > 确保在开发环境中禁用遥测。

   > [!TIP]
   > 确保已在 Visual Studio 代码中打开 Teams 应用项目。

## <a name="create-new-environment"></a>创建新环境

创建项目后，Teams 工具包默认配置：

* 一个 `local` 表示本地计算机环境配置的环境。
* 表示远程或云环境配置的一个 `dev` 环境。

> [!NOTE]
> 每个项目只能有一个 `local` 环境，但可以有多个远程环境。

**添加远程环境**：

1. :::image type="content" source="~/assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png" alt-text="从活动栏的活动栏":::中选择 **Teams 工具包**。
2. 选择 **“+Teams：在环境**”部分下创建新环境，如下图所示：

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/create new env.png" alt-text="创建新环境":::

> [!Note]
> 如果有多个环境，则需要选择一个现有环境来创建相同的环境。 该命令将所选现有环境的文件内容 `config.<newEnv>.json` 复制 `azure.parameters.<newEnv>.json` 到创建的新环境。

## <a name="target-environment"></a>目标环境

可以选择目标环境，Teams 工具包会提示你在具有多个远程环境时选择目标环境：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="添加环境":::

## <a name="project-folder-structure"></a>项目文件夹结构

创建项目后，可以在Visual Studio Code中查看 **资源管理器** 下的项目文件夹和文件。 除了自定义代码，Teams 工具包还使用一些文件来维护`configs``states`应用和`templates`应用。 以下列表提供了文件，并概述了它们与多个环境的关系。

* `.fx/configs`：配置用户可以为 Teams 应用自定义的文件。
  * `config.<envName>.json`：按环境配置文件。
  * `azure.parameters.<envName>.json`：每个环境的 Azure bicep 预配参数文件。
  * `projectSettings.json`：适用于所有环境的全局项目设置。
* `.fx/states`：由 Teams 工具包生成的预配结果。
  * `state.<envName>.json`：按环境预配输出文件。
  * `<env>.userdata`：每个环境预配输出的用户数据。
* `templates`
  * `appPackage`：应用清单模板文件。
  * `azure`：Bicep 模板文件。

## <a name="customize-resource-provision"></a>自定义资源预配

Teams 工具包允许更改配置文件和模板文件，以自定义每个环境中的资源预配。

下表列出了自定义资源预配的常见方案：

| 应用场景 | 位置| 说明 |
| --- | --- | --- |
| 自定义 Azure 资源 |`templates/azure` `.fx/azure.parameters.<envName>.json` 下的 Bicep 文件 | [自定义 ARM 参数和模板](provision.md#customize-arm-template-files) |
| 为 Teams 应用重复使用现有的 Azure AD 应用 | `.fx/config.<envName>.json` 中的 `auth` 部分|  [为 Teams 应用使用现有的 Azure AD 应用](provision.md#use-an-existing-azure-ad-app-for-your-teams-app) |
| 为机器人重复使用现有的 Azure AD 应用 |`.fx/config.<envName>.json` 中的 `bot` 部分| [为机器人使用现有的 Azure AD 应用](provision.md#use-an-existing-azure-ad-app-for-your-bot) |
| 在预配 SQL 时跳过添加用户 |`.fx/config.<envName>.json` 中的 `skipAddingSqlUser` 属性| [跳过为 SQL 数据库添加用户](provision.md#skip-adding-user-for-sql-database) |
| 自定义应用清单 |`templates/manifest.template.json` 文件下 `manifest` 部分在 `.fx/config.<envName>.json`| [工具包中的预览应用清单](TeamsFx-preview-and-customize-app-manifest.md)|

## <a name="scenarios"></a>应用场景

可以看到以下方案，用于自定义不同环境中的资源预配。
<br>

<br><details>
<summary><b>方案 1：为不同环境自定义 Teams 应用名称 </b></summary>

可以将 Teams 应用名称 `myapp(dev)` 设置为默认环境 `dev` 和 `myapp(staging)` 过渡环境 `staging`。

自定义步骤：

1. 打开配置文件 `.fx/configs/config.dev.json`。
2. 更新 **short** to **`myapp(dev)`** 的 **`manifest`** > **`appName`** > 属性。

  更新内容 `.fx/configs/config.dev.json` 如下：

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

3. 可以创建一个新环境，并在它不存在时将其 `staging` 命名。
4. 打开配置文件 `.fx/configs/config.staging.json`。
5. 更新同一属性 `myapp(staging)`。
6. 现在，可以在远程环境中运行预配命令 `dev` 和 `staging` 环境来更新应用名称。 若要使用 Teams 工具包运行预配命令，请参阅 [预配](provision.md#provision-using-teams-toolkit)。

</details>

<details>
<summary><b>方案 2：为不同环境自定义 Teams 应用说明</b></summary>

可以为不同的环境设置不同的 Teams 应用说明：

* 对于默认环境 `dev`，说明为 `my app description for dev`。
* 对于过渡环境 `staging`，说明是 `my app description for staging`。

自定义步骤：

1. 打开配置文件 `.fx/configs/config.dev.json`。
2. 添加具有值的新属性 **`manifest`****`short`** > **`description`** > 。**`my app description for dev`**

  更新内容 `.fx/configs/config.dev.json` 如下：

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
6. 打开 Teams 应用清单模板 `templates/appPackage/manifest.template.json`。
7. 更新属性 **`description`** > **`short`** 以使用在配置具有胡子语法 **`{{config.manifest.description.short}}`** 的文件中定义的 **变量**。
  
  更新内容 `manifest.template.json` 如下：

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

8. 现在可以针对 `dev` 环境 `staging` 运行预配命令，以更新远程环境中的应用名称。

</details>

<details>
<summary><b>方案 3：为所有环境自定义 Teams 应用说明</b></summary>

可以将 Teams 应用 `my app description` 的说明设置为所有环境。

由于 Teams 应用清单模板是在所有环境中共享的，因此我们可以为目标更新其中的说明值：

1. 打开 Teams 应用清单模板 `templates/appPackage/manifest.template.json`。
2. 使用硬编码字符串更新属性 **`description`****`short`** > 。**`my app description`**
  
  更新内容 `manifest.template.json` 如下：

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

3. 现在可以针对 **所有** 环境运行预配命令，以更新远程环境中的应用名称。

</details>

<details>
<br><summary><b>方案 4：为不同环境自定义 Azure 资源</b></summary>

可以为每个环境自定义 Azure 资源，例如编辑与 fx/configs/azure.parameters 对应的环境。{env}.json 文件，用于指定 Azure 函数名称。

有关 Bicep 模板和参数文件的详细信息，请参阅 [预配云资源](provision.md)。
</details>
</br>

## <a name="see-also"></a>另请参阅

* [预配云资源](provision.md)
* [添加更多云资源](add-resource.md)
* [在 Teams 项目中与其他开发人员协作](TeamsFx-collaboration.md)
* [在不同的环境中测试应用行为](test-app-behavior.md)
