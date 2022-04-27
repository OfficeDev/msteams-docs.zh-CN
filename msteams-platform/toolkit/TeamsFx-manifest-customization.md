---
title: 在Teams Toolkit中自定义Teams应用清单
author: zyxiaoyuer
description: 自定义 Teams 应用清单
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: de85674891a53c1e87b43ae1d472daf35716c348
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073538"
---
# <a name="customize-app-manifest-in-toolkit"></a>在Toolkit中自定义应用清单

Teams Toolkit包含在本地和远程环境中的文件夹下`manifest.template.json`的以下清单模板文件：

* `manifest.template.json`
* `templates/appPackage`


## <a name="prerequisite"></a>先决条件

* 安装 [最新版本的 Teams 工具包](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

> [!TIP]
> 确保已在Visual Studio Code中打开Teams应用项目。

在本地调试或预配期间，Teams Toolkit从`manifest.template.json`开发人员[门户](https://dev.teams.microsoft.com/apps)加载清单、`config.{env}.json`从`state.{env}.json`中加载配置，并创建 Teams 应用。


## <a name="placeholders-supported-in-manifesttemplatejson"></a>manifest.template.json 中支持的占位符

* `{{state.xx}}`是预定义的占位符，其值由Teams Toolkit解析，在其中`state.{env}.json`定义。 确保不修改状态下的值。{env}.json
* `{{config.manifest.xx}}` 是自定义占位符，其值已从中解析 `config.{env}.json`

  1. 可以按如下所示添加自定义参数：
      1. 在 manifest.template.json 中添加具有模式的占位符： `{{config.manifest.xx}}`
      2. 在配置中添加配置值。{env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

   2. 可以通过选择任何一个配置占位符 **转到配置文件** 或 **在其中查看状态文件** 来导航到配置文件 `manifest.template.json`

## <a name="see-also"></a>另请参阅

[Teams Toolkit中的预览Teams应用清单](TeamsFx-manifest-preview.md)
