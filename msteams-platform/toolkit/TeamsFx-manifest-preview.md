---
title: 在 Teams 工具包中预览 Teams 应用清单
author: zyxiaoyuer
description: 预览 Teams 应用清单
ms.author: nliu
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 91bc070d30136ce1f004676172594f26ca37dea5
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111869"
---
# <a name="preview-app-manifest-in-toolkit"></a>工具包中的预览应用清单

清单模板文件 `manifest.template.json` 位于 scaffolding 下的 `templates/appPackage` 文件夹下。 具有占位符的模板文件和实际值由 Teams 工具包从不同环境的 `.fx/configs` 和 `.fx/states` 下的文件解析。

## <a name="prerequisite"></a>先决条件

* 安装 [最新版本的 Teams 工具包](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)

> [!TIP]
> 确保已在 Visual Studio 代码中打开 Teams 应用项目。

## <a name="preview-manifest"></a>预览清单

若要预览包含真实内容的清单，Teams 工具包将在 `build/appPackage` 文件夹下生成预览清单文件：

```text
└───build
    └───appPackage
        ├───appPackage.{env}.zip - Zipped app package of remote teams app
        ├───appPackage.local.zip - Zipped app package of local team app
        ├───manifest.{env}.json  - Previewed manifest of remote teams app
        └───manifest.local.json  - Previewed manifest of local teams app
```

### <a name="preview-local-manifest-file"></a>预览本地清单文件

若要预览本地 Teams 应用的清单文件，可以按 **F5** 运行本地调试。 它会为你生成默认的本地设置，然后在 `build/appPackage` 文件夹下生成应用包和预览清单。

还可以按照以下步骤预览本地清单：

1. 在 `manifest.template.json` 文件的代码管理器中选择 **预览**，然后选择 **本地**
2. 在 `manifest.template.json` 文件的菜单栏中选择 **预览清单文件**
3. 在 Treeview 中选择 **Zip Teams 元数据包** ，然后选择 **本地**

预览本地如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/preview-23.png" alt-text="预览":::

### <a name="preview-manifest-in-remote-environment"></a>远程环境中的预览清单

若要预览远程团队应用的清单文件，请在 Teams 工具包扩展 Treeview 的 **开发** 面板中选择 **在云中预配**，或从命令面板触发 **Teams：在云中预配**。 它为远程团队应用生成配置，并在 `build/appPackage` 文件夹下生成包和预览清单。

还可以按照以下步骤在远程环境中预览清单：

1. 在 `manifest.template.json` 文件的代码管理器中选择 **预览**
2. 在 `manifest.template.json` 文件的菜单栏中选择 **预览清单文件**
3. 在 Treeview 中选择 **Zip Teams 元数据包**
4. 选择你的环境

如果有多个环境，则需要选择要预览的环境，如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview-1.png" alt-text="添加 env":::

## <a name="sync-local-changes-to-developer-portal"></a>将本地更改同步到开发人员门户

预览清单文件后，可以按照以下步骤将本地更改同步到开发人员门户：

1. 选择 `manifest.{env}.json` 左上角的 **更新到 Teams 平台**
2. 在 `manifest.{env}.json` 的菜单栏中选择 **Teams：将清单更新到 Teams 平台**

 还可以从命令面板触发 **Teams：将清单更新到 Teams平台**：

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/pre.png" alt-text="树状视图":::

> [!NOTE]
> 从编辑器代码管理器或 **标题** 触发，将当前清单文件更新到 Teams 平台。 从命令面板中触发需要选择目标环境

  

如果清单文件由于配置文件更改或模板更改而过时，请选择以下任一操作：

* **仅预览**：根据当前配置覆盖本地清单文件
* **预览和更新**：根据当前配置覆盖本地清单文件，并更新到 Teams 平台
* **取消**：不执行任何操作

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/manifest preview -3.png" alt-text="pre":::



> [!NOTE]
> 更改会在开发人员门户中更新。 开发门户中的任何手动更新都会被覆盖。

## <a name="see-also"></a>另请参阅

[在 Teams 工具包中自定义 Teams 应用清单](TeamsFx-manifest-customization.md)
