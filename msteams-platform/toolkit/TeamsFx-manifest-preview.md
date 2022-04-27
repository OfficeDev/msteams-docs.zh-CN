---
title: Teams Toolkit中的预览Teams应用清单
author: zyxiaoyuer
description: 预览 Teams 应用清单
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 57dc719f872d502beded14c30a09d72c27ee74c3
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073278"
---
# <a name="preview-app-manifest-in-toolkit"></a>Toolkit中的预览应用清单

在基架之后，清单模板文件 `manifest.template.json` 在文件夹下 `templates/appPackage` 可用。 包含占位符的模板文件和实际值通过Teams Toolkit来自不同环境下`.fx/configs`的文件解`.fx/states`析。

## <a name="prerequisite"></a>先决条件

* 安装[最新版本的Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> 确保已在Visual Studio代码中打开Teams应用项目。

## <a name="preview-manifest"></a>预览清单

若要使用实际内容预览清单，Teams Toolkit在文件夹下`build/appPackage`生成预览清单文件：

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote teams app
        ├───appPackage.local.zip - Zipped app package of local team app
        ├───manifest.{env}.json  - Previewed manifest of remote teams app
        └───manifest.local.json  - Previewed manifest of local teams app
```

### <a name="preview-local-manifest-file"></a>预览本地清单文件

若要预览本地 Teams 应用的清单文件，可以按 **F5** 运行本地调试。 它会为你生成默认的本地设置，然后在文件夹下 `build/appPackage` 生成应用包和预览清单。

还可以按照以下步骤预览本地清单：

1. 在文件的代码管理`manifest.template.json`器中选择 **“预览**”，然后选择 **本地**
2. 在文件的菜单栏`manifest.template.json`上选择 **预览清单文件**
3. 在 Treeview **中选择 Zip Teams 元数据包**，然后选择 **本地**

本地预览显示，如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="预览":::

### <a name="preview-manifest-in-remote-environment"></a>远程环境中的预览清单

若要预览远程团队应用的清单文件，请在Teams Toolkit扩展 Treeview 的 **开发** 面板中选择“预 **配**”，或触发Teams：从命令面板 **在云中预配**。 它为远程团队应用生成配置，并在文件夹下 `build/appPackage` 生成包和预览清单。

还可以按照以下步骤预览远程环境中的清单：

1. 在文件的代码管理器`manifest.template.json`中选择 **“预览**”
2. 在文件的菜单栏`manifest.template.json`上选择 **预览清单文件**
3. 在 Treeview **中选择 Zip Teams 元数据包**
4. 选择环境

如果有多个环境，则需要选择要预览的环境，如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="添加 env":::

## <a name="sync-local-changes-to-developer-portal"></a>将本地更改同步到开发人员门户

预览清单文件后，可以按照以下步骤将本地更改同步到开发人员门户：

1. 选择 **“更新”到** 左上角的Teams平台`manifest.{env}.json`
2. 选择 **Teams：将清单更新到** 菜单栏上的Teams平台`manifest.{env}.json`

 还可以触发Teams：从命令面板 **将清单更新到Teams平台**：

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="树视图":::

> [!NOTE]
> 从编辑器代码管理器或 **游戏** 触发器将当前清单文件更新到Teams平台。 命令面板中的触发器需要选择目标环境

  

如果清单文件因配置文件更改或模板更改而过时，请选择以下任一操作：

* **仅预览**：根据当前配置覆盖本地清单文件
* **预览和更新**：本地清单文件根据当前配置被覆盖，并已更新到Teams平台
* **取消**：未执行任何操作

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::



> [!NOTE]
> 更改会在开发人员门户中更新。 开发门户中的任何手动更新都被覆盖。

## <a name="see-also"></a>另请参阅

[在Teams Toolkit中自定义Teams应用清单](TeamsFx-manifest-customization.md)
