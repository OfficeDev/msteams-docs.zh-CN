---
title: 向Teams应用添加功能
author: MuyangAmigo
description: 介绍添加Teams Toolkit功能
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 9d2e3d559bd9d561e3afae8b0db9544ab2ad86cc
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073529"
---
# <a name="add-capabilities-to-your-teams-apps"></a>将功能添加到 Teams 应用

在应用开发过程中，可以创建具有Teams应用功能的新Teams应用。 下表列出了Teams应用功能：

|**功能**|**说明**|
|--------|-------------|
| 选项卡 |  选项卡是指向应用清单中声明的域的简单 HTML 标记。 可以添加选项卡作为团队内部频道的一部分，为单个用户添加群组聊天或个人应用|
| 机器人 |  机器人帮助通过文本、交互式卡片和任务模块与 Web 服务交互|
| 消息传递扩展 | 消息传递扩展有助于通过Microsoft Teams客户端中的按钮和表单与 Web 服务交互|

## <a name="prerequisite"></a>先决条件

* 安装 [最新版本的 Teams 工具包](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

> [!TIP]
> 确保已在 VS 代码中打开Teams应用项目。

## <a name="limitations"></a>限制

添加更多功能时对 TeamsFx 的限制如下所示：

* 最多可以添加 16 个实例的选项卡
* 可以为每个实例添加一个实例的机器人和消息传递扩展
## <a name="add-capabilities"></a>添加功能

> [!Note]
> 成功将功能添加到Teams应用后，需要为每个环境执行预配。
* 可以在Visual Studio Code中使用Teams Toolkit添加功能
    1. 打开 **Microsoft Visual Studio代码**
    1. 从左侧面板中选择 **Teams Toolkit**
    1. 选择 **“添加功能”**

        :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add capabilities.png" alt-text="capabilities":::

*   还可以打开命令面板并输入Teams：添加功能：

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/tree view capabilities.png" alt-text="备用功能":::


    1. 在弹出窗口中，选择要包含在项目中的功能：

    :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select capabilities.png" alt-text="select":::

    2. 选择 **“确定”**

所选功能已成功添加到项目中。 Teams Toolkit为新添加的功能生成源代码

## <a name="add-capabilities-using-teamsfx-cli-in-command-window"></a>在命令窗口中使用 TeamsFx CLI 添加功能

1. 将目录更改为 **项目目录**
1. 执行以下命令，向项目添加不同的功能：

   |功能和方案| 命令|
   |-----------------------|----------|
   |添加选项卡|`teamsfx capability add tab`|
   |添加机器人|`teamsfx capability add bot`|
   |添加消息传递扩展插件|`teamsfx capability add messaging-extension`|

## <a name="supported-capabilities"></a>支持的功能

除了Teams应用已有的功能外，还可以选择向Teams应用添加不同的功能。 下表提供了不同的Teams应用功能：

|现有功能|其他支持的功能|
|--------------------|--------------------|
|带有SPFx的选项卡|无|
|带有 Azure 的选项卡|机器人和消息传递扩展|
|Bot|选项卡|
|消息传递扩展|选项卡和机器人|
|选项卡和机器人|选项卡和消息扩展|
|选项卡和消息传递扩展插件|选项卡和机器人|
|选项卡、机器人和消息传递扩展|选项卡|
|选项卡 |机器人和消息扩展|

## <a name="add-bot-tab-and-messaging-extension"></a>添加机器人、选项卡和消息传递扩展

添加机器人和消息传递扩展后，项目中的更改如下所示：

* 机器人模板代码将添加到包含路径 `yourProjectFolder/bot`的子文件夹中。 这包括项目中的 **hello world** 机器人应用程序模板
* `launch.json`文件夹和`task.json`文件夹下`.vscode`更新，其中包括Visual Studio Code必需的脚本，并在要在本地调试应用程序时执行
* `manifest.template.json`文件夹下`templates/appPackage`的文件已更新，其中包括清单文件中表示Teams平台中的应用程序的机器人相关信息。 相关更改如下所示：
  * 机器人的 ID
  * 机器人的范围
  * hello world 机器人应用程序可以响应的命令
* 将更新下面 `templates/azure/teamsfx` 的文件，并 `templates/azure/provision/xxx`重新生成 .bicep 文件
* 下面的文件 `.fx/config` 已重新生成，这可确保使用新添加的功能的正确配置来设置项目

添加选项卡后，项目中的更改如下所示：

* 前端选项卡模板代码将添加到包含路径 `yourProjectFolder/tab`的子文件夹中，其中包括项目中的 **hello world** 选项卡应用程序模板
* `launch.json`文件夹和`task.json`文件夹下`.vscode`更新，其中包括Visual Studio Code必需的脚本，并在要在本地调试应用程序时执行
* `manifest.template.json`文件夹下`templates/appPackage`的文件已更新，其中包括清单文件中代表Teams平台中的应用程序的选项卡相关信息。 更改包括：
  * 可配置和静态选项卡
  * 选项卡的范围
* 将更新下面 `templates/azure/teamsfx` 的文件，并 `templates/azure/provision/xxx`重新生成 .bicep 文件
* 下面的文件 `.fx/config` 已重新生成，这可确保使用新添加的功能的正确配置来设置项目



## <a name="see-also"></a>另请参阅

* [预配云资源](provision.md)
* [新建Teams项目](create-new-project.md)
