---
title: 在Teams中预览应用Teams Toolkit
author: zyxiaoyuer
description: 预览 Teams 应用清单
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
---

# <a name="preview-teams-app-manifest-in-teams-toolkit"></a>在Teams预览应用Teams Toolkit

搭建基架后，以下是文件夹下可用的清单模板 `templates/appPackage` 文件：

- `manifest.local.template.json` - 本地调试团队应用。
- `manifest.remote.template.json` - 在所有远程环境之间共享。

模板文件由占位符组成，并且来自 Teams Toolkit的实际值在 和 下的文件中`.fx/configs`解析`.fx/states`。

## <a name="prerequisite"></a>先决条件

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!TIP]
> 确保你已Teams代码打开Visual Studio项目。

## <a name="preview-manifest"></a>预览清单

若要预览包含真实内容的清单，Teams Toolkit文件夹下生成预览清单`build/appPackage`文件：

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote teams app
        ├───appPackage.local.zip - Zipped app package of local team app
        ├───manifest.{env}.json  - Previewed manifest of remote teams app
        └───manifest.local.json  - Previewed manifest of local teams app
```

### <a name="preview-local-manifest-file"></a>预览本地清单文件

若要预览本地团队应用的清单文件，你需要按 **F5** 运行本地调试。 它生成默认本地设置，然后应用包和预览清单生成在 **build/appPackage** 文件夹下。

您还可以按照以下步骤预览本地清单：

1. 在  **manifest.local.template.json** 文件的代码中选择预览。
2. 选择  **manifest.local.template.json 文件的菜单栏上的"预览清单** 文件"。
3. 选择 **树Teams压缩元数据包**，**然后选择本地。**
预览本地显示如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-1.png" alt-text="预览":::

### <a name="preview-manifest-in-remote-environment"></a>远程环境中预览清单

若要预览远程团队应用的清单文件，请在 Teams Toolkit  扩展树视图的开发面板中选择"在云中预配"，或从命令调色板触发Teams **：** 在云中预配"。 它生成远程团队应用的配置，并生成 build **/appPackage 文件夹下的程序包和预览** 清单。

还可以按照以下步骤在远程环境中预览清单：

1. 在  **manifest.remote.template.json** 文件的代码中选择预览。
2. 选择  **manifest.remote.template.json 文件的菜单栏上的"预览清单** 文件"。
3. 选择 **树Teams压缩元数据** 包。
4. 选择你的环境。

如果存在多个环境，则需要选择想要预览的环境，如图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="添加 env":::

## <a name="sync-local-changes-to-dev-portal"></a>将本地更改同步到开发人员门户

预览清单文件后，你可以按照以下步骤将本地更改同步到开发人员门户：

1.  选择 **"更新Teams** 左上角的"更新""更新平台"`manifest.{env}.json`
2. 选择 **Teams：将清单更新Teams菜单** 栏上的"更新到平台"`manifest.{env}.json`

 还可以从命令 **Teams，将Teams清单更新到** 平台

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="树视图":::

> [!NOTE]
> 从编辑器代码lens或 **标题触发**，将当前清单文件更新为Teams清单。 从命令调色板触发需要选择目标环境。

如果清单文件由于配置文件更改或模板更改而过期，请确保确认以下操作：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::

- **仅预览**：根据当前配置将覆盖本地清单文件
- **预览和更新**：本地清单文件将根据当前配置进行覆盖，并更新到Teams平台
- **取消**：不执行任何操作

> [!NOTE]
> 更改将更新到开发人员门户。 如果你在开发人员门户中拥有一些手动更新，它将被覆盖。

## <a name="see-also"></a>另请参阅

[在Teams中自定义应用Teams Toolkit](TeamsFx-manifest-customization.md)
