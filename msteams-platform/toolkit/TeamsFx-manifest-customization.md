---
title: 在Teams中自定义应用Teams Toolkit
author: zyxiaoyuer
description: 自定义 Teams 应用清单
ms.author: nliu
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: d9f2ea49ece8728101a738129e45dd8155887ebc
ms.sourcegitcommit: 2d5bdda6c52693ed682bbd543b0aa66e1feb3392
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2022
ms.locfileid: "61768075"
---
# <a name="customize-app-manifest-in-teams-toolkit"></a>在应用程序中自定义Teams Toolkit

Teams Toolkit文件夹下的以下清单模板 `templates/appPackage` 文件：

- `manifest.local.template.json` - 本地调试团队应用
- `manifest.remote.template.json` - 在所有环境中共享

## <a name="prerequisite"></a>先决条件

* [安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!TIP]
> 确保你已Teams中打开的应用VS Code。

预配期间，Teams Toolkit 加载 清单，并结合 和 的配置，在开发人员门户 `manifest.remote.template.json` `state.{env}.json` `config.{env}.json` 中创建[团队应用](https://dev.teams.microsoft.com/apps)。

在本地调试过程中，Teams Toolkit 加载 清单，并结合 中的配置，在开发人员 `manifest.local.template.json` `localSettings.json` 门户 中创建[团队应用](https://dev.teams.microsoft.com/apps)。

## <a name="supported-placeholder-in-manifestremotetemplatejson"></a>manifest.remote.template.json 中支持的占位符

- `{{state.xx}}`是预定义的占位符，其值由 Teams Toolkit解析，在 中定义 `state.{env}.json` 。 确保不修改状态中的值。{env}.json。
- `{{config.manifest.xx}}` 是自定义占位符，其值从 `config.{env}.json` 解析。
  - 您可以按如下方式添加自定义参数：
    - 使用模式在 manifest.remote.template.json 中添加占位符： `{{config.manifest.xx}}`
    - 在 config 中添加 config 值。{env}.json

        ```json
        {
            "manifest": {
                "KEY": "VALUE"
            }
        }
        ```

    除了 中每个配置占位符 `manifest.remote.template.json` 之外，还有 `Go to config file` 一个 。 可以通过选择配置文件来导航到配置文件。

## <a name="supported-placeholder-in-manifestlocaltemplatejson"></a>manifest.local.template.json 中支持的占位符

`{{localSettings.xx}}`是预定义的占位符，其值由 Teams Toolkit解析，在 中定义 `localSettings.json` 。 确保不修改 localSettings.json 中的值。

 > [!NOTE]
 > 确保不自定义本地清单。

## <a name="see-also"></a>另请参阅

[在Teams中预览应用Teams Toolkit](TeamsFx-manifest-preview.md)
