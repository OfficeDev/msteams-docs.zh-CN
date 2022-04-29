---
title: 在 Teams 工具包中自定义 Teams 应用清单
author: zyxiaoyuer
description: 自定义 Teams 应用清单
ms.author: nliu
ms.localizationpriority: high
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 28a06da170ee52e4340aa3d401d39ad08f58e2ba
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65110258"
---
# <a name="customize-app-manifest-in-toolkit"></a>在工具包中自定义应用清单

Teams 工具包包含跨本地和远程环境的 `manifest.template.json` 文件夹下的以下清单模板文件：

* `manifest.template.json`
* `templates/appPackage`


## <a name="prerequisite"></a>先决条件

* 安装 [最新版本的 Teams 工具包](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

> [!TIP]
> 确保已在 Visual Studio Code 中打开 Teams 应用项目。

在本地调试或预配期间，Teams 工具包将从 `manifest.template.json` 加载清单（其中包含来自 `state.{env}.json` 和 `config.{env}.json` 的配置），并在[开发人员门户](https://dev.teams.microsoft.com/apps)中创建 Teams 应用。


## <a name="placeholders-supported-in-manifesttemplatejson"></a>manifest.template.json 中支持的占位符

* `{{state.xx}}` 是预定义的占位符，其值由 Teams 工具包解析（在 `state.{env}.json` 中定义）。 确保不要修改 state.{env}.json 中的值
* `{{config.manifest.xx}}` 是自定义占位符，其值从 `config.{env}.json` 中解析

  1. 可以按如下方式添加自定义参数：
      1. 在 manifest.template.json 中添加具有以下模式的占位符：`{{config.manifest.xx}}`
      2. 在 config.{env}.json 中添加配置值

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

   2. 可以通过选择任何一个配置占位符来导航到配置文件：**转到配置文件** 或 **查看 `manifest.template.json` 中的状态文件**

## <a name="see-also"></a>另请参阅

[在 Teams 工具包中预览 Teams 应用清单](TeamsFx-manifest-preview.md)
