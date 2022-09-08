---
title: 在 Teams 工具包中自定义 Teams 应用清单
author: zyxiaoyuer
description: 在本模块中，了解如何在不同的环境中编辑、预览和自定义 Teams 应用清单。
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
ms.openlocfilehash: 3828c357307c5f7bfd94935a75dc9d6f5cedbc39
ms.sourcegitcommit: c806c5ffe277c740d0d7b8f62e72ade562029194
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617787"
---
# <a name="customize-teams-app-manifest"></a>自定义 Teams 应用部件清单

Teams 应用清单介绍应用如何集成到 Microsoft Teams 产品中。 有关清单的详细信息，请参阅 [Teams 的应用清单架构](../resources/schema/manifest-schema.md)。 本节介绍：

* [本地环境中的预览清单文件](#preview-manifest-file-in-local-environment)
* [远程环境中的预览清单文件](#preview-manifest-file-in-remote-environment)
* [将本地更改同步到开发人员门户](#sync-local-changes-to-dev-portal)
* [自定义 Teams 应用清单](#customize-your-teams-app-manifest)
* [验证清单](#validate-manifest)

清单模板文件 `manifest.template.json` 位于 scaffolding 下的 `templates/appPackage` 文件夹下。 具有占位符的模板文件以及实际值由 Teams 工具包使用不同环境下 `.fx/configs` 的文件解 `.fx/states` 析。

若要使用实际内容预览清单，Teams 工具包在文件夹下 `build/appPackage` 生成预览清单文件：

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote Teams app
        ├───appPackage.local.zip - Zipped app package of local Teams app
        ├───manifest.{env}.json  - Previewed manifest of remote Teams app
        └───manifest.local.json  - Previewed manifest of local Teams app
```

可以在本地和远程环境中预览清单文件。

* [本地环境中的预览清单文件](#preview-manifest-file-in-local-environment)
* [远程环境中的预览清单文件](#preview-manifest-file-in-remote-environment)

## <a name="preview-manifest-file-in-local-environment"></a>本地环境中的预览清单文件

若要在本地环境中预览清单文件，可以按 **F5** 运行本地调试。 它会为你生成默认的本地设置，然后在 `build/appPackage` 文件夹下生成应用包和预览清单。

还可以通过两种方法预览本地清单文件

* 在 codelens 中使用预览选项
* 使用 **Zip Teams 元数据包** 选项

以下步骤有助于在 codelens 中使用预览选项预览本地清单文件：

1. 在文件的代码段`manifest.template.json`中选择 **“预览**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="预览":::

1. 选择 **“本地**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="选择 environment1":::

以下步骤有助于使用 **Zip Teams 元数据包** 选项预览本地清单文件：

1. 选择 `manifest.template.json` 文件。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="选择“清单”":::

1. 在Visual Studio Code工具栏中选择 Teams 工具包:::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG":::图标。

1. 选择 **“部署**”下的 **Zip Teams 元数据包**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="选择 Teams 元数据包":::

1. 选择 **“本地**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="选择环境":::

预览本地如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="预览":::

## <a name="preview-manifest-file-in-remote-environment"></a>远程环境中的预览清单文件

使用Visual Studio Code预览清单文件：

* 在 Teams 工具包扩展的 **“开发**”下选择 **云中的“预配”**
  
  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/provision.png" alt-text="预配云资源":::

若要使用命令 palatte 预览清单文件，请执行以下操作：

* 触发 **器 Teams：从命令面板在云中预配** 。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/command palatte.png" alt-text="使用命令 palatte 预配云资源":::

它生成远程 Teams 应用的配置，并在文件夹下 `build/appPackage` 生成包和预览清单。

还可以通过远程环境中的两种方法预览清单文件

* 在 codelens 中使用预览选项
* 使用 **Zip Teams 元数据包** 选项

以下步骤有助于在 codelens 中使用预览选项预览清单文件：

1. 在文件的代码段`manifest.template.json`中选择 **“预览**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="预览":::

1. 选择环境。

   > [!NOTE]
   > 如果有多个环境，则需要选择要预览的环境，如下图所示：

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="添加 env":::

以下步骤有助于在远程环境中使用 **Zip Teams 元数据包** 选项预览清单文件：

1. 选择 `manifest.template.json` 文件。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="选择“清单”":::

1. 在Visual Studio Code工具栏中选择 Teams 工具包:::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG":::图标。

1. 选择 **“部署**”下的 **Zip Teams 元数据包**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="选择 Teams 元数据包":::

1. 选择环境。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="添加 env":::

   > [!NOTE]
   > 如果有多个环境，则需要选择要预览的环境，如下图所示：

## <a name="sync-local-changes-to-dev-portal"></a>将本地更改同步到开发人员门户

预览清单文件后，可以通过以下方式将本地更改同步到开发人员门户：

> [!NOTE]
> 有关开发人员门户的详细信息，请参阅 [Teams 开发人员门户](../concepts/build-and-test/teams-developer-portal.md)。

1. 部署 Teams 应用清单。

   可以通过以下任一方式部署 Teams 应用清单：

   * 转到 `manifest.template.json` 文件，然后右键单击以从上下文菜单中进行选择 `Deploy Teams app manifest` 。

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-manifest.png" alt-text="部署清单":::

   * 来自命令面板的触发器 `Teams: Deploy Teams app manifest` 。

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-command.png" alt-text="从命令面板部署":::

2. 更新到 Teams 平台。

   可以通过以下任一方式更新到 Teams 平台：

   * 选择左上角的 **“更新到 Teams** ” `manifest.{env}.json`平台。

   * 触发 **Teams：将清单更新到** 菜单栏 `manifest.{env}.json`上的 Teams 平台。

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png" alt-text="更新到团队":::

还可以从命令面板触发 **Teams：将清单更新到 Teams 平台** ：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="树状视图":::

> [!NOTE]
> 来自编辑器代码管理器或菜单栏的触发器将当前清单文件更新到 Teams 平台。 命令面板中的触发器需要选择目标环境。

 CLI 命令：

``` bash
        teamsfx deploy manifest --include-app-manifest yes
```

---

> [!NOTE]
> 开发人员门户的更改更新。 开发人员门户中的任何手动更新都被覆盖。

如果清单文件因配置文件更改或模板更改而过时，请选择以下任一操作：

* **仅预览**：根据当前配置覆盖本地清单文件。
* **预览和更新**：本地清单文件根据当前配置覆盖，并已更新到 Teams 平台。
* **取消**：不执行任何操作。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::

## <a name="customize-your-teams-app-manifest"></a>自定义 Teams 应用清单

Teams 工具包包含跨本地和远程环境的 `manifest.template.json` 文件夹下的以下清单模板文件：

* `manifest.template.json`
* `templates/appPackage`

在本地调试或预配期间，Teams 工具包从`manifest.template.json`开发人员[门户](https://dev.teams.microsoft.com/apps)中加载清单和配置`state.{env}.json``config.{env}.json`，并创建 Teams 应用。

### <a name="supported-placeholders-in-manifesttemplatejson"></a>manifest.template.json 中支持的占位符

以下列表提供以下内容中 `manifest.template.json`支持的占位符：

* `{{state.xx}}` 是预定义的占位符，其值由 Teams 工具包解析（在 `state.{env}.json` 中定义）。 确保不修改其中的值 `state.{env}.json`
* `{{config.manifest.xx}}` 是自定义占位符，其值已从中解析 `config.{env}.json`

**添加自定义参数**

1. 按如下所示添加自定义参数：</br>
   a. 使用模式`{{config.manifest.xx}}`添加占位符`manifest.template.json`。</br>
   b. 在中添加配置值 `config.{env}.json`。

     ```json
     {
         "manifest": {
          "KEY": "VALUE"
          }
     }
     ```

2. 可以通过选择任何一个配置占位符 **转到配置文件** 或 **查看状态文件** 来导航到配置文件 `manifest.template.json`。

### <a name="validate-manifest"></a>验证清单

在 **Zip Teams 元数据包** 等操作期间，Teams 工具包会根据其架构验证清单。 以下列表提供了验证清单的不同方法：

* 在 VSC 中，从命令面板触发 `Teams: Validate manifest file` ：

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/validate.png" alt-text="验证文件":::

* 在 CLI 中，使用命令：

     ``` bash
        teamsfx validate --env local
        teamsfx validate --env dev
        ```

---

## To preview values for local and dev environment

In `manifest.template.json`, you can navigate to codelens to preview the values for `local` and `dev` environment.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/codelens.png" alt-text="Preview values":::

> [!NOTE]
> Provision the environment or execute local debug to generate values for placeholders.

You can navigate to state file or configuration file by selecting the codelens, which provides a drop-down list with all the environment names. After selecting one environment, the corresponding state file or configuration file opens.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-environment.png" alt-text="Select your environment":::

To preview values for all the environments, you can hover over the placeholder. It shows a list with environment names and corresponding values. If you haven't provisioned the environment or executed the local debug, select `Trigger Teams: Provision in the cloud command to see placeholder value` or `Trigger local debug to see placeholder value`.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/hover.png" alt-text="Preview all values":::

## See also

* [Manage multiple environments](TeamsFx-multi-env.md)
* [Reference: Manifest schema for Microsoft Teams](../resources/schema/manifest-schema.md)
* [Public developer preview for Microsoft Teams](../resources/dev-preview/developer-preview-intro.md)
