---
title: 向Teams应用添加功能
author: MuyangAmigo
description: 介绍添加Teams Toolkit功能
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: a0ebea1fb05e3583c90c41596da98a25d89f9b4c
ms.sourcegitcommit: 74623035d7c18194e339f566c820e0653bc3d8b6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656759"
---
# <a name="add-capabilities-to-teams-apps"></a>向Teams应用添加功能

在Teams Toolkit中添加功能可帮助你向现有Teams应用添加其他功能。下表列出了Teams应用功能：

|**功能**|**说明**|
|--------|-------------|
| 选项卡 |  选项卡是引用应用清单中声明的域的简单 HTML 标记。 可以将选项卡添加为团队内部频道的一部分，为单个用户添加群组聊天或个人应用。|
| 机器人 |  机器人有助于通过文本、交互式卡片和任务模块与 Web 服务交互。|
| 消息扩展 | 消息扩展有助于通过Microsoft Teams客户端中的按钮和表单与 Web 服务交互。|

## <a name="advantages"></a>优点

以下列表提供了在 TeamsFx 中添加更多功能的优点：

* 提供便利
* 使用Teams Toolkit自动添加源代码，向应用添加更多函数

## <a name="limitations"></a>限制

以下列表提供了在 TeamsFx 中添加更多功能的限制：

* 最多可以添加 16 个实例的选项卡
* 可以为每个实例添加一个实例的机器人和消息扩展

## <a name="add-capabilities"></a>添加功能

**可以通过以下方法添加功能：**

* 若要在Visual Studio Code中使用Teams Toolkit来添加功能
* 使用命令面板添加功能

  > [!Note]
  > 在Teams应用中成功添加功能后，需要为每个环境进行预配。

* **若要在Visual Studio Code中使用Teams Toolkit来添加功能：**

   1. 打开 **Visual Studio Code**。
   1. 从左侧面板中选择 **Teams Toolkit**。
   1. 选择 **“开发**”下 **的“添加功能**”。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/select-feature123.png" alt-text="更新了一个" border="true":::

* **若要使用命令面板添加功能：**

   1. 打开 **命令面板**。
   1. 输入 **Teams：添加功能**。
   1. 按 Enter 键。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/Teams-add-features.png" alt-text="团队功能" border="true":::

   1. 在弹出窗口中，选择要在项目中添加的功能。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/notification-add-capabilities.png" alt-text="通知" border="true":::

## <a name="add-capabilities-using-teamsfx-cli"></a>使用 TeamsFx CLI 添加功能

* 将目录更改为 **项目目录**
* 下表列出了功能和所需的命令：

  |功能和方案| 命令|
  |-----------------------|----------|
  |添加通知机器人 |`teamsfx add notification `|
  |添加命令机器人 |`teamsfx add command-and-response `|
  |添加已启用 sso 的选项卡 |`teamsfx add sso-tab`|
  |添加选项卡 |`teamsfx add tab`|
  |添加机器人 |`teamsfx add bot`|
  |添加消息扩展插件 |`teamsfx add message extension`|

## <a name="available-capabilities-to-add-for-different-teams-project"></a>用于为不同Teams项目添加的可用功能

可以选择基于在Teams应用中创建的项目添加不同的功能。
下表列出了要在项目中添加的可用功能：

|现有功能|其他支持的功能|
|--------------------|--------------------|
|SPFx选项卡 |无|
|启用了 SSO 的选项卡 |已启用 SSO 的选项卡、通知机器人、命令机器人、机器人、消息扩展|
|通知机器人 |已启用 SSO 的选项卡、选项卡|
|命令机器人 |已启用 SSO 的选项卡、选项卡|
|Tab |Tab、通知机器人、命令机器人、机器人、消息扩展|
|Bot |消息扩展，启用了 SSO 的选项卡，选项卡|
|消息扩展 |机器人，已启用 SSO 的选项卡，选项卡 |

## <a name="add-bot-tab-and-message-extension"></a>添加机器人、选项卡和消息扩展

添加机器人和消息扩展后，项目中的更改如下所示：

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

## <a name="step-by-step-guide"></a>分步指南

* 按照[分步](../sbs-gs-commandbot.yml)指南在Microsoft Teams中生成命令机器人

* 按照[分步](../sbs-gs-notificationbot.yml)指南在Microsoft Teams中生成通知机器人。

## <a name="see-also"></a>另请参阅

* [预配云资源](provision.md)
* [新建Teams项目](create-new-project.md)
