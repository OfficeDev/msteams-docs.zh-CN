---
title: 在 Teams 工具包中自定义 Teams 应用清单
author: zyxiaoyuer
description: 在本模块中，了解如何在不同环境中编辑、预览和自定义 Teams 应用清单。
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/13/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: e92e30cf30dd06dbbe3c513a79fe4b7ed7c4bc1a
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833098"
---
# <a name="customize-teams-app-manifest"></a>自定义 Teams 应用部件清单

Teams 应用清单介绍了你的应用如何集成到 Microsoft Teams 产品中。

::: zone pivot="visual-studio-code"

## <a name="customize-teams-app-manifest-for-visual-studio-code"></a>为Visual Studio Code自定义 Teams 应用清单

Teams 应用清单介绍了你的应用如何集成到 Microsoft Teams 产品中。 有关清单的详细信息，请参阅 [Teams 的应用清单架构](../resources/schema/manifest-schema.md)。 本节介绍：

* [在本地环境中预览清单文件](#preview-manifest-file-in-local-environment)
* [远程环境中的预览清单文件](#preview-manifest-file-in-remote-environment)
* [将本地更改同步到开发人员门户](#sync-local-changes-to-developer-portal)
* [自定义 Teams 应用清单](#customize-your-teams-app-manifest)
* [验证清单](#validate-manifest)

清单模板文件 `manifest.template.json` 位于 scaffolding 下的 `templates/appPackage` 文件夹下。 包含占位符和实际值的模板文件和实际值由 Teams 工具包在不同环境中使用 和 `.fx/configs` `.fx/states` 的文件进行解析。

为了预览包含实际内容的清单，Teams 工具包会在 文件夹下 `build/appPackage` 生成预览清单文件：

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote Teams app
        ├───appPackage.local.zip - Zipped app package of local Teams app
        ├───manifest.{env}.json  - Previewed manifest of remote Teams app
        └───manifest.local.json  - Previewed manifest of local Teams app
```

可以在本地和远程环境中预览清单文件。

* [在本地环境中预览清单文件](#preview-manifest-file-in-local-environment)
* [远程环境中的预览清单文件](#preview-manifest-file-in-remote-environment)

## <a name="preview-manifest-file-in-local-environment"></a>在本地环境中预览清单文件

若要在本地环境中预览清单文件，可以按 **F5** 运行本地调试。 它会为你生成默认的本地设置，然后在 `build/appPackage` 文件夹下生成应用包和预览清单。

还可以通过两种方法预览本地清单文件

* 通过在 codelens 中使用预览选项
* 使用 **Zip Teams 元数据包** 选项

以下步骤有助于使用 codelens 中的预览选项预览本地清单文件：

1. 在文件的 codelens `manifest.template.json` 中选择 **“预览**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="屏幕截图是一个示例，其中显示了清单文件的 codelens 中的预览。":::

1. 选择 **“本地**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="屏幕截图是显示环境中选择本地的示例。":::

以下步骤有助于使用 **Zip Teams 元数据包** 选项预览本地清单文件：

1. 选择 `manifest.template.json` 文件。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="屏幕截图是显示选择 manifest.template.json 的示例。":::

1. 选择Visual Studio Code工具栏中的 Teams 工具包:::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG":::图标。

1. 在“**部署**”下选择“**Zip Teams 元数据包**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="屏幕截图是显示 zip Teams 元数据包选择的示例。":::

1. 选择 **“本地**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-env1.png" alt-text="屏幕截图是显示环境中选择本地的示例。":::

预览本地如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="屏幕截图是显示本地预览的示例。":::

## <a name="preview-manifest-file-in-remote-environment"></a>远程环境中的预览清单文件

若要使用 Visual Studio Code 预览清单文件，请执行以下操作：

* 在 Teams 工具包扩展的 **“开发**”下，选择“**在云中预配**”
  
  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/provision.png" alt-text="屏幕截图是显示云资源中预配选择的示例。":::

若要使用命令面板预览清单文件，请执行以下操作：

* 触发 Teams：从命令面板 **在云中预配** 。

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/command palatte.png" alt-text="屏幕截图是显示使用命令面板预配云资源的示例。":::

它为远程 Teams 应用生成配置，并在文件夹下 `build/appPackage` 生成包和预览清单。

还可以在远程环境中通过两种方法预览清单文件

* 通过在 codelens 中使用预览选项
* 使用 **Zip Teams 元数据包** 选项

以下步骤有助于使用 codelens 中的预览选项预览清单文件：

1. 在文件的 codelens `manifest.template.json` 中选择 **“预览**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="屏幕截图是在清单文件的 codelens 中显示预览的示例。":::

1. 选择环境。

   > [!NOTE]
   > 如果有多个环境，则需要选择要预览的环境，如下图所示：

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="屏幕截图是显示环境添加的示例。":::

以下步骤有助于在远程环境中使用 **Zip Teams 元数据包** 选项预览清单文件：

1. 选择 `manifest.template.json` 文件。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-manifest-json.png" alt-text="屏幕截图是显示选择 manifest.template.json 的示例。":::

1. 选择Visual Studio Code工具栏中的 Teams 工具包:::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG":::图标。

1. 在“**部署**”下选择“**Zip Teams 元数据包**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-metadata-package.png" alt-text="屏幕截图是显示 zip Teams 元数据包选择的示例。":::

1. 选择环境。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="屏幕截图是显示环境添加的示例。":::

   > [!NOTE]
   > 如果有多个环境，则需要选择要预览的环境，如下图所示：

## <a name="sync-local-changes-to-developer-portal"></a>将本地更改同步到开发人员门户

预览清单文件后，可以通过以下方式将本地更改同步到开发人员门户：

> [!NOTE]
> 有关开发人员门户的详细信息，请参阅 [Teams 开发人员门户](../concepts/build-and-test/teams-developer-portal.md)。

1. 部署 Teams 应用清单。

   可以采用以下任一方式部署 Teams 应用清单：

   * 转到 `manifest.template.json` 文件，然后右键单击以 `Deploy Teams app manifest` 从上下文菜单中选择。

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-manifest.png" alt-text="屏幕截图是显示选择部署 Teams 应用清单的示例。":::

   * 从命令面板触发 `Teams: Deploy Teams app manifest` 。

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deploy-command.png" alt-text="屏幕截图是显示从命令面板部署的示例。":::

2. 更新到 Teams 平台。

   可以通过以下任一方式更新到 Teams 平台：

   * 选择 左上角的`manifest.{env}.json`“**更新到 Teams 平台**”。

   * 触发 Teams：在 菜单栏`manifest.{env}.json`上 **将清单更新到 Teams 平台**。

      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/update-to-teams.png" alt-text="屏幕截图是在清单的菜单栏上显示 Teams 平台更新的示例。":::

还可以触发 Teams：从命令面板 **将清单更新到 Teams 平台** ：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="屏幕截图是一个示例，显示了从命令面板选择 Teams：将清单更新到 Teams 平台。":::

> [!NOTE]
> 从编辑器 codelens 或菜单栏触发将当前清单文件更新到 Teams 平台。 从命令面板触发需要选择目标环境。

 CLI 命令：

``` bash
        teamsfx deploy manifest --include-app-manifest yes
```

---

> [!NOTE]
> 更改将更新到开发人员门户。 将覆盖开发门户中的任何手动更新。

如果清单文件因配置文件更改或模板更改而过时，请选择以下任一操作：

* **仅预览**：根据当前配置覆盖本地清单文件。
* **预览和更新**：根据当前配置覆盖本地清单文件，并更新为 Teams 平台。
* **取消**：不执行任何操作。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="屏幕截图是一个示例，显示用于选择“仅预览”的导航，以及当清单文件因配置或模板更改而过时时，预览和更新和取消选项。":::

## <a name="customize-your-teams-app-manifest"></a>自定义 Teams 应用清单

Teams 工具包包含跨本地和远程环境的 `manifest.template.json` 文件夹下的以下清单模板文件：

* `manifest.template.json`
* `templates/appPackage`

在本地调试或预配期间，Teams 工具包从 `manifest.template.json`加载清单，并使用 、 `state.{env}.json``config.{env}.json`中的配置，并在[开发门户中](https://dev.teams.microsoft.com/apps)创建 Teams 应用。

### <a name="supported-placeholders-in-manifesttemplatejson"></a>manifest.template.json 中支持的占位符

以下列表在 中 `manifest.template.json`提供了支持的占位符：

* `{{state.xx}}` 是预定义的占位符，其值由 Teams 工具包解析（在 `state.{env}.json` 中定义）。 确保不修改 中的值 `state.{env}.json`
* `{{config.manifest.xx}}` 是自定义占位符，其值解析自 `config.{env}.json`

**添加自定义参数**

1. 添加自定义参数，如下所示：</br>
   a. 使用模式 `{{config.manifest.xx}}`在 中添加`manifest.template.json`占位符。</br>
   b. 在 `config.{env}.json`中添加配置值。

     ```json
     {
         "manifest": {
          "KEY": "VALUE"
          }
     }
     ```

2. 可以通过选择任一配置占位符“**转到配置文件**”或“在 中`manifest.template.json`**查看状态文件**”来转到配置文件。

### <a name="validate-manifest"></a>验证清单

在 **Zip Teams 元数据包** 等操作期间，Teams 工具包会根据其架构验证清单。 以下列表提供了验证清单的不同方法：

* 在 VSC 中，从命令面板触发 `Teams: Validate manifest file` ：

  :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/validate.png" alt-text="屏幕截图是显示命令面板中的 Teams 验证清单文件的示例。":::

* 在 CLI 中，使用 命令：

     ``` bash
        teamsfx validate --env local
        teamsfx validate --env dev
        ```

---

## To preview values for local and dev environment

In `manifest.template.json`, you can go to codelens to preview the values for `local` and `dev` environment.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/codelens.png" alt-text="Screenshot is an example of showing preview values for local and dev environment.":::

> [!NOTE]
> Provision the environment or execute local debug to generate values for placeholders.

You can go to state file or configuration file by selecting the codelens, which provides a drop-down list with all the environment names. After selecting one environment, the corresponding state file or configuration file opens.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-environment.png" alt-text="Screenshot is an example of showing the selection of an environment.":::

To preview values for all the environments, you can hover over the placeholder. It shows a list with environment names and corresponding values. If you haven't provisioned the environment or executed the local debug, select `Trigger Teams: Provision in the cloud command to see placeholder value` or `Trigger local debug to see placeholder value`.

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/hover.png" alt-text="Screenshot is an example of showing the preview values for all environments.":::

::: zone-end

::: zone pivot="visual-studio"

## Edit Teams app manifest using Visual Studio

Teams Toolkit in Visual Studio loads manifest from `manifest.template.json` with configurations from `state.{env}.json` and `config.{env}.json` while provisioning and preparing app dependencies. You can also create Microsoft Teams app in [Developer Portal](https://dev.teams.microsoft.com/apps) with the manifest.

After scaffolding, in the manifest template file under `templates/appPackage` folder,
`manifest.template.json` is shared between local and remote environment.

In the manifest template, select **Project** > **Teams Toolkit** > **Open Manifest File**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png" alt-text="Screenshot is an example of showing the navigation to open manifest file." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-open-manifest.png":::

### Customize app manifest in Teams Toolkit

There are two types of placeholders in `manifest.template.json`:

* `{{state.xx}}` is pre-defined placeholder, whose value is resolved by Teams Toolkit, defined in `state.{env}.json`. It's recommended to not modify the values in `state.{env}.json`.
* `{{config.manifest.xx}}` is customized placeholder, whose value is resolved from `config.{env}.json`.

You can add a customized parameter by:

* Adding a placeholder in `manifest.template.json` with pattern: `{{config.manifest.xx}}`.
* Adding a config value in `config.{env}.json`.

    ```
        {
            "manifest": {
            "KEY": "VALUE"
            }
    }
    ```

### Preview app manifest in Teams Toolkit

You can preview values in app manifest in two ways:

* When you hover over the placeholder in `manifest.template.json`, then you can see the values for **dev** and **local** environment.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png" alt-text="Screenshot is an example showing when you hover over placeholder, can view the values for dev and local environment." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-placeholder1.png":::

* You can also hover over the key besides each placeholder in `manifest.template.json`, and you can see the same values for **dev** and **local** environment.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png" alt-text="Screenshot is an example showing when you hover over key beside placeholder can view the same values for dev and local environment." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-hover-key-placeholder.png":::

   > [!NOTE]
   > If the environment has not been provisioned, or the Teams app dependencies have not been prepared, it indicates that the values for placeholder have not been generated. Please follow the guidance inside hover to generate corresponding values.

### Preview manifest file

To preview the manifest file, you can sideload for local or deploy for Azure. You can preview the manifest file by performing the following step:

* Select **Project** > **Teams Toolkit** and trigger **Prepare Teams App Dependencies** or **Provision in the Cloud** that generates configuration for local or remote Teams app.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png" alt-text="Screenshot is an example of showing preview manifest file." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview-manifest1.png":::

There are two other ways to upload zip app package before you can preview manifest file:

1. From the list of menu select **Project** > **Teams Toolkit** > **Zip App Package**, and select **For Local** or **For Azure**.

    :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png" alt-text="Screenshot is an example of showing the navigation to zip app package for local and azure." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-zip1.png":::

1. You can also upload zip app package from Solution Explorer, if you right-click on **MyTeamsApp1** and then select **Teams Toolkit** > **Zip App Package** > **For Local** or **For Azure**.

  > [!NOTE]
  > In this scenario the project name is **MyTeamsApp1**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png" alt-text="Screenshot is an example of showing the list of Teams toolkit menus from solution explorer." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-solution-explorer1.png":::

Teams Toolkit generates the zip app package, and to preview manifest file content you can follow the step below:

* Right-click on **manifest.template.json** under **appPackage** folder, select **Preview Manifest File** > **For Local** or **For Azure**.

   :::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png" alt-text="Screenshot is an example of showing the preview manifest menu for local and azure." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-preview1.png":::

This displays the preview of the manifest file in Visual Studio.

### Sync local changes to Developer Portal

After you've previewed the manifest file in Visual Studio, you can now sync the local changes to the Developer Portal. Select **Project** > **Teams Toolkit** > **Update Manifest in Teams Developer Portal**, or context menu from Solution Explorer. You can now preview the manifest file in Developer Portal as a result of syncing the local changes.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png" alt-text="Screenshot is an example of showing the navigation to update manifest in Teams developer portal." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-update-manifest1.png":::

The changes are updated to Teams Developer Portal.

> [!NOTE]
>
> * Select **Overwrite and update** or **Cancel** from the **Warning** dialog box to make any manual updates that can be overwritten in the Developer Portal.
> * When you create a Teams command bot using Visual Studio, two app IDs are registered in Azure Active Directory. You can identify the app IDs in the Developer Portal as **Application client ID** under Basic information and existing **Bot ID** under **App features**.

:::image type="content" source="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png" alt-text="Screenshot is an example of showing the update warning." lightbox="../assets/images/Tools-and-SDK-revamp/edit-manifest-for-visual-studio/vs-overwrite.png":::

::: zone-end

## See also

* [Manage multiple environments](TeamsFx-multi-env.md)
* [Reference: Manifest schema for Microsoft Teams](../resources/schema/manifest-schema.md)
* [Public developer preview for Microsoft Teams](../resources/dev-preview/developer-preview-intro.md)
* [Provision cloud resources using Visual Studio](provision-cloud-resources.md)
* [Deploy Teams app to the cloud using Visual Studio](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)
