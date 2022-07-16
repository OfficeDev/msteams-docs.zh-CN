---
title: 向 Teams 应用添加功能
author: MuyangAmigo
description: 在本模块中，了解如何添加 Teams 工具包的功能、优势、限制和功能
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 90a1e28f4c7bb3d0bc9530fc1af8ad4d4e373c9b
ms.sourcegitcommit: 0c734a5809ad6eb36255c97f38589c67d0971741
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2022
ms.locfileid: "66830790"
---
# <a name="add-capabilities-to-teams-apps"></a>向 Teams 应用添加功能

在 Teams 工具包中添加功能可帮助你向现有 Teams 应用添加其他功能。下表列出了 Teams 应用功能：

|**功能**|**说明**|
|--------|-------------|
| 选项卡 |  选项卡是引用应用清单中声明的域的简单 HTML 标记。 可以将选项卡添加为团队内部频道的一部分，为单个用户添加群组聊天或个人应用。|
| 机器人 |  机器人有助于通过文本、交互式卡片和任务模块与 Web 服务交互。|
| 消息扩展 | 消息扩展有助于通过 Microsoft Teams 客户端中的按钮和表单与 Web 服务交互。|

## <a name="advantages"></a>优点

以下列表提供了在 TeamsFx 中添加更多功能的优点：

* 提供便利。
* 通过使用 Teams 工具包自动添加源代码，向应用添加更多函数。

## <a name="limitations"></a>限制

以下列表提供了在 TeamsFx 中添加更多功能的限制：

* 最多可以添加 16 个实例的选项卡。
* 可以为每个实例添加一个机器人和消息扩展。

## <a name="add-capabilities"></a>添加功能

**可以通过以下方法添加功能：**

* 在 Visual Studio Code 中使用 Teams 工具包添加功能。
* 使用命令面板添加功能。

  > [!Note]
  > 在 Teams 应用中成功添加功能后，需要为每个环境进行预配。

* **若要在Visual Studio Code中使用 Teams 工具包来添加功能：**

   1. 打开 **Visual Studio Code**。
   1. 从左侧面板中选择 **Teams 工具包** 。
   1. 选择 **“开发**”下 **的“添加功能**”。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/select-feature123.png" alt-text="更新了一个":::

* **若要使用命令面板添加功能：**

   1. 打开 **命令面板**。
   1. 输入 **Teams：添加功能**。
   1. 按 Enter 键。

      :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/teams-add-features.png" alt-text="使用命令面板添加功能。":::

   1. 在弹出窗口中，选择要在项目中添加的功能。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/notification-add-capabilities.png" alt-text="通知":::

## <a name="add-capabilities-using-teamsfx-cli"></a>使用 TeamsFx CLI 添加功能

* 将目录更改为 **项目目录**。
* 下表列出了功能和所需的命令：

  |功能和方案| 命令|
  |-----------------------|----------|
  |添加通知机器人 |`teamsfx add notification`|
  |添加命令机器人 |`teamsfx add command-and-response`|
  |添加已启用 sso 的选项卡 |`teamsfx add sso-tab`|
  |添加选项卡 |`teamsfx add tab`|
  |添加机器人 |`teamsfx add bot`|
  |添加消息扩展插件 |`teamsfx add message extension`|

## <a name="available-capabilities-to-add-for-different-teams-project"></a>用于为不同 Teams 项目添加的可用功能

可以选择基于在 Teams 应用中创建的项目添加不同的功能。
下表列出了要在项目中添加的可用功能：

|现有功能|其他支持的功能|
|--------------------|--------------------|
|SPFx 选项卡 |无|
|启用了 SSO 的选项卡 |已启用 SSO 的选项卡、通知机器人、命令机器人、机器人、消息扩展|
|通知机器人 |已启用 SSO 的选项卡、选项卡|
|命令机器人 |已启用 SSO 的选项卡、选项卡|
|Tab |Tab、通知机器人、命令机器人、机器人、消息扩展|
|Bot |消息扩展，启用了 SSO 的选项卡，选项卡|
|消息扩展 |机器人，已启用 SSO 的选项卡，选项卡 |

## <a name="add-bot-tab-and-message-extension"></a>添加机器人、选项卡和消息扩展

添加机器人和消息扩展后，项目中的更改如下所示：

* 机器人模板代码将添加到包含路径 `yourProjectFolder/bot`的子文件夹中。 这包括项目中的 **hello world** 机器人应用程序模板。
* `launch.json`文件夹和`task.json`文件夹下`.vscode`会更新，其中包括Visual Studio Code所需的脚本，并在要在本地调试应用程序时执行。
* `manifest.template.json` 文件夹下 `templates/appPackage` 的文件已更新，其中包括在 Teams 平台中表示应用程序的清单文件中的机器人相关信息。 相关更改如下所示：
  * 机器人的 ID
  * 机器人的范围
  * hello world 机器人应用程序可以响应的命令
* 将更新下面 `templates/azure/teamsfx` 的文件，并 `templates/azure/provision/xxx`重新生成 .bicep 文件。
* 下面的文件 `.fx/config` 会重新生成，这可确保为项目设置新添加功能的正确配置。

添加选项卡后，项目中的更改如下所示：

* 前端选项卡模板代码将添加到包含路径 `yourProjectFolder/tab`的子文件夹中，其中包括项目中的 **hello world** 选项卡应用程序模板。
* `launch.json`文件夹和`task.json`文件夹下`.vscode`会更新，其中包括Visual Studio Code所需的脚本，并在要在本地调试应用程序时执行。
* `manifest.template.json` 文件夹下 `templates/appPackage` 的文件已更新，其中包括在 Teams 平台中表示应用程序的清单文件中与选项卡相关的信息。 更改包括：
  * 可配置和静态选项卡
  * 选项卡的范围
* 将更新下面 `templates/azure/teamsfx` 的文件，并 `templates/azure/provision/xxx`重新生成 .bicep 文件。
* 下面的文件 `.fx/config` 已重新生成，这可确保为项目设置新添加功能的正确配置。

## <a name="step-by-step-guide"></a>分步指南

* 按照分 [步](../sbs-gs-commandbot.yml) 指南在 Microsoft Teams 中生成命令机器人

* 按照分 [步](../sbs-gs-notificationbot.yml) 指南在 Microsoft Teams 中生成通知机器人。

## <a name="see-also"></a>另请参阅

* [预配云资源](provision.md)
* [创建新的 Teams 项目](create-new-project.md)
