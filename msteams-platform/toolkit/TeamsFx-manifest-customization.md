---
title: 在Teams中自定义应用Teams Toolkit
author: zyxiaoyuer
description: 自定义Teams应用程序清单
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 34b454f63eb900fce2f38748838ce46558835ac5
ms.sourcegitcommit: f1e6f90fb6f7f5825e55a6d18ccf004d0091fb6d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/30/2021
ms.locfileid: "61227990"
---
# <a name="customize-teams-app-manifest-in-teams-toolkit"></a>在Teams中自定义应用Teams Toolkit

Teams Toolkit文件夹下的两个清单模板 `templates/appPackage` 文件：

- `manifest.local.template.json` - 本地调试团队应用
- `manifest.remote.template.json` - 在所有环境中共享

## <a name="prerequisite"></a>先决条件

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!TIP]
> 你应该已经拥有一个Teams VS 代码中打开的应用项目。

预配期间，Teams Toolkit中加载清单，并结合 和 `manifest.remote.template.json` `state.{env}.json` 的配置 `config.{env}.json` 。 然后，它在此清单 [的开发人员门户](https://dev.teams.microsoft.com/apps) 中创建团队应用。

在本地调试过程中，Teams Toolkit `manifest.local.template.json` 从 加载清单，并结合 中的配置 `localSettings.json` 。 然后，它在此清单 [的开发人员门户](https://dev.teams.microsoft.com/apps) 中创建团队应用。

## <a name="supported-placeholder-in-manifestremotetemplatejson"></a>manifest.remote.template.json 中支持的占位符

- `{{state.xx}}`是预定义的占位符，其值由 Teams Toolkit解析，在 中定义 `state.{env}.json` 。 不应修改状态中的值。{env}.json。
- `{{config.manifest.xx}}` 是自定义占位符，其值从 `config.{env}.json` 解析。
  - 可以通过以下方法添加自定义参数：
    - 使用模式在 manifest.remote.template.json 中添加占位符： `{{config.manifest.xx}}`
    - 在 config 中添加 config 值。{env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

    除了 中每个配置占位符 `manifest.remote.template.json` 之外，还有一个 `Go to config file` 按钮。 可以通过选择配置文件来导航到配置文件，如图所示：

    ![转到配置文件](./images/gotoconfigfile.png)

## <a name="supported-placeholder-in-manifestlocaltemplatejson"></a>manifest.local.template.json 中支持的占位符

`{{localSettings.xx}}`是预定义的占位符，其值由 Teams Toolkit解析，在 中定义 `localSettings.json` 。 不应修改 localSettings.json 中的值。

 > [!NOTE]
 > 建议不要自定义本地清单。

## <a name="see-also"></a>另请参阅

> [!div class="nextstepaction"]
> [在Teams中预览应用Teams Toolkit](TeamsFx-manifest-preview.md)
