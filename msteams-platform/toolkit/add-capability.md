---
title: 向应用添加Teams功能
author: MuyangAmigo
description: 描述添加Teams Toolkit
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
---

# <a name="add-capabilities-to-your-teams-apps"></a>将功能添加到 Teams 应用

可以使用一种Teams应用功能创建新的 Teams 应用。 在应用开发过程中，Teams Toolkit向应用添加Teams功能。 下表列出了Teams应用程序功能：

|**功能**|**说明**|
|--------|-------------|
| 选项卡 |  选项卡是指向应用程序清单中声明的域的简单 HTML 标记。 你可以将选项卡添加为单个用户的团队、群聊或个人应用中频道的一部分。|
| 机器人 |  机器人通过文本、交互式卡片和任务模块帮助与 Web 服务交互。|
| 消息扩展 | 邮件扩展通过客户端中的按钮和表单帮助与 web Microsoft Teams交互。|

## <a name="prerequisite"></a>先决条件

[安装Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)版本 v3.0.0+。

> [!TIP]
> 确保你已Teams VS 代码中打开的应用项目。

## <a name="add-capabilities-using-teams-toolkit"></a>使用自定义设置添加Teams Toolkit

> [!IMPORTANT]
> 在将功能成功添加到你的应用后，你需要针对每个环境Teams预配。

1. 打开 **Visual Studio Code**。
1. Select **Teams Toolkit** from left panel.
1. 选择 **"添加功能"**：

    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add capabilities.png" alt-text="capabilities":::

   还可以打开命令调色板，然后输入Teams **：添加功能**： 
      
    :::image type="content" source="../assets/images/teams-toolkit-v2/manual/tree view capabilities.png" alt-text="备用功能":::

1. 从弹出窗口中，选择要包括在项目中的功能：

    :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select capabilities.png" alt-text="select":::

1. 选择“确定”。

所选功能成功添加到项目中。 应用程序Teams Toolkit新添加的功能生成源代码。

## <a name="add-capabilities-using-teamsfx-cli-in-command-window"></a>在命令窗口中使用 TeamsFx CLI 添加功能

1. 将目录更改为 **项目目录**。
1. 执行以下命令，向项目添加不同的功能：

   |功能与方案| 命令|
   |-----------------------|----------|
   |添加选项卡|`teamsfx capability add tab`|
   |添加自动程序|`teamsfx capability add bot`|
   |添加消息传递扩展|`teamsfx capability add messaging-extension`|

## <a name="supported-capabilities-matrix"></a>支持的功能矩阵

除了应用已有Teams功能外，还可以选择向应用添加Teams功能。 下表提供了不同的应用Teams功能： 

|现有功能|可以添加其他支持的功能|
|--------------------|--------------------|
|带选项卡SPFx|无|
|使用 Azure 的选项卡|机器人和消息传递扩展|
|Bot|选项卡|
|消息传递扩展|选项卡和自动程序|
|选项卡和自动程序|选项卡和邮件扩展|
|选项卡和消息传递扩展|选项卡和自动程序|
|选项卡、机器人和消息传递扩展|选项卡|
|选项卡 |机器人和邮件扩展|

## <a name="add-capabilities"></a>添加功能

添加机器人和消息传递扩展后，项目中的更改如下所示：

- 自动程序模板代码将添加到具有路径 的子文件夹 `yourProjectFolder/bot`。 这包括 hello **world bot** 应用程序模板到项目中。
- `launch.json`文件夹`task.json``.vscode`下的 和 将更新，其中包含用于Visual Studio Code脚本，并且当你要在本地调试应用程序时执行。 
- `manifest.remote.template.json`更新`manifest.local.template.json`文件夹下的 `templates/appPackage` 和 文件，其中包括清单文件中表示应用程序在 Teams 文件中的信息。 相关更改如下所示：
  - 自动程序 ID。
  - 自动程序的范围。
  - Hello world 自动程序应用程序可以响应的命令。
- 将更新 `templates/azure/teamsfx` 下的文件，并 `templates/azure/provision/xxx`重新生成 .bicep 文件。
- 下的文件 `.fx/config` 将重新生成，这可确保使用新添加功能正确的配置设置项目。

添加选项卡后，项目中的更改如下所示：

- 前端选项卡模板代码将添加到具有 path `yourProjectFolder/tab`的子文件夹，其中包含 **hello world** 选项卡应用程序模板到项目中。
- `launch.json`文件夹`task.json``.vscode`下的 和 将更新，其中包含用于Visual Studio Code脚本，并且当你要在本地调试应用程序时执行。 
- `manifest.remote.template.json``manifest.local.template.json`更新文件夹下的 `templates/appPackage` 和 文件，其中包括清单文件中与选项卡相关的信息，该清单文件表示 Teams 平台中的应用程序，更改如下所示：
  - 可配置选项卡和静态选项卡。
  - 选项卡的范围。
- 将更新 `templates/azure/teamsfx` 下的文件，并 `templates/azure/provision/xxx`重新生成 .bicep 文件。
- 下的文件 `.fx/config` 将重新生成，这可确保使用新添加功能正确的配置设置项目。

## <a name="limitations"></a>限制

在添加更多功能时对 TeamsFx 的限制如下所示：

* 可以添加最多 16 个实例的选项卡。
* 你可以为每个实例添加一个机器人和消息扩展。

## <a name="see-also"></a>另请参阅

* [预配云资源](provision.md)
* [新建Teams项目](create-new-project.md)
