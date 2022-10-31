---
title: 向 Teams 应用添加功能
author: surbhigupta
description: 在本模块中，了解如何添加 Teams 工具包的功能
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: a0bec3166228b53dd4a6da336b42632ba2475582
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791753"
---
# <a name="add-capabilities-to-teams-apps"></a>向 Teams 应用添加功能

使用 Teams 工具包添加功能有助于将其他功能添加到现有 Microsoft Teams 应用。 添加更多功能的优点是，可以使用 Teams 工具包自动添加源代码，从而向应用添加更多函数。 还可以根据在 Teams 应用中创建的项目选择不同的功能。 下表列出了 Teams 应用功能：

|功能|说明|其他支持的功能|
|--------|-------------|-----------------|
|**基本 Teams 应用**|              |
| Tab |  选项卡是引用应用清单中声明的域的简单 HTML 标记。 可以在团队、群组聊天或个人应用中为单个用户添加选项卡作为频道的一部分。|选项卡， 通知机器人， 命令机器人， 机器人， 消息扩展|
|SPFx 选项卡| SPFx 选项卡应用托管在 Microsoft 365 中，它支持开发和托管客户端 SPFx 解决方案|无|
|已启用 SSO 的选项卡|可以生成支持 SSO 的选项卡应用，以允许用户使用单一登录功能|已启用 SSO 的选项卡， 通知机器人， 命令机器人， 机器人， 消息扩展|
| Bot |  机器人通过文本、交互式卡片和任务模块帮助与 Web 服务进行交互。|消息扩展、已启用 SSO 的选项卡、选项卡|
| 消息扩展 | 消息扩展有助于通过 Microsoft Teams 客户端中的按钮和表单与 Web 服务进行交互。|机器人，启用 SSO 的选项卡，选项卡|
|**基于方案的 Teams 应用**|             |
| 通知机器人 | 通知机器人在 Teams 频道、群组聊天或个人聊天中主动发送消息。 可以使用 HTTP 请求（如卡片或文本）触发通知机器人。 |已启用 SSO 的选项卡、选项卡|
| 命令机器人 | 命令机器人允许使用命令机器人自动执行重复任务。 它使用自适应卡片响应聊天中发送的简单命令。 |已启用 SSO 的选项卡、选项卡|
| 工作流机器人| 工作流机器人允许用户与工作流机器人应用中的自适应卡片操作处理程序功能启用的自适应卡片进行交互。|已启用 SSO 的选项卡、选项卡|

> [!NOTE]
> 最多可以添加 16 个实例的选项卡。 至于机器人和消息扩展，可以一次为每个实例添加一个。

## <a name="add-capabilities"></a>添加功能

可以通过以下方法添加功能：

* [在 Microsoft Visual Studio Code 中使用 Teams 工具包](#using-teams-toolkit-in-microsoft-visual-studio-code)
* [使用命令面板](#using-the-command-palette)
* [使用 TeamsFx CLI](#using-teamsfx-cli)

### <a name="using-teams-toolkit-in-microsoft-visual-studio-code"></a>在 Microsoft Visual Studio Code 中使用 Teams 工具包

   1. 打开 **Visual Studio Code**。
   1. 从活动栏中选择 **“Teams 工具包** ”。
   1. 选择 **“开发**”下的“**添加功能**”。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/select-feature123.png" alt-text="从 Teams 工具包添加功能":::

      > [!NOTE]
      > 在 Teams 应用中成功添加功能后，需要为每个环境进行预配。

### <a name="using-the-command-palette"></a>使用命令面板

   1. 选择“ **查看** > **命令面板...”** 或 **Ctrl+Shift+P**。

      :::image type="content" source="../assets/images/teams-toolkit-v2/manual/add-capabilities-command-palette.png" alt-text="从命令 palatte 添加功能":::

   1. 输入 **Teams：添加功能**。
   1. 按 Enter。

      :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/teams-add-features.png" alt-text="使用命令面板添加功能。":::

   1. 从弹出窗口中，选择需要在项目中添加的功能。

       :::image type="content" source="~/assets/images/teams-toolkit-v2/manual/notification-add-capabilities.png" alt-text="通知":::

### <a name="using-teamsfx-cli"></a>使用 TeamsFx CLI

* 将目录更改为 **项目目录**。
* 下表列出了功能和所需的命令：

  |功能和方案| 命令|
  |-----------------------|----------|
  |添加通知机器人 |`teamsfx add notification`|
  |添加命令机器人 |`teamsfx add command-and-response`|
  |添加启用 SSO 的选项卡 |`teamsfx add sso-tab`|
  |添加选项卡 |`teamsfx add tab`|
  |添加机器人 |`teamsfx add bot`|
  |添加消息扩展 |`teamsfx add message extension`|

## <a name="changes-after-adding-capabilities"></a>添加功能后所做的更改

下表显示了添加功能时，应用文件中可以看到的更改：

|添加功能|说明| 更改|
|------------|------------------------|---------|
|机器人、消息扩展和选项卡|在项目中包括 **hello world**&nbsp;机器人或选项卡应用程序模板。|前端机器人或选项卡模板代码将分别添加到具有 路径 `yourProjectFolder/bot` 或 `yourProjectFolder/tab` 的子文件夹中。|
| 机器人、消息扩展和选项卡 |包括Visual Studio Code所需的脚本，在想要在本地调试应用程序时执行。 |文件 `launch.json` 及 `task.json` 文件夹下 `.vscode` 已更新。|
| 机器人和消息扩展|在清单文件中包括机器人或选项卡相关信息，该文件代表 Teams 平台中的应用程序。|文件夹下`templates/appPackage`的文件`manifest.template.json`已更新，其中包括清单文件中与选项卡相关的信息，该文件代表 Teams 平台中的应用程序。 更改显示在机器人的 ID、机器人的范围以及 hello world 机器人或选项卡应用程序可以响应的命令中。|
|Tab|在清单文件中包括机器人或选项卡相关信息，该文件代表 Teams 平台中的应用程序。|文件夹下`templates/appPackage`的文件`manifest.template.json`已更新，其中包括清单文件中与选项卡相关的信息，该文件代表 Teams 平台中的应用程序。 这些更改在可配置和静态选项卡以及选项卡的作用域中可见。|
|机器人、消息扩展和选项卡|在 teamsfx 中包含与机器人或选项卡相关的&nbsp;信息，以及用于集成 Azure 函数的预配文件。|将更新下面的 `templates/azure/teamsfx` 文件，并 `templates/azure/provision/xxx`重新生成 .bicep 文件。|
|机器人、消息扩展和选项卡|确保为新添加的功能设置了正确的项目配置。|将重新生成下面的 `.fx/config` 文件|

## <a name="step-by-step-guides"></a>分步指南

* 按照 [分步](../sbs-gs-commandbot.yml) 指南在 Microsoft Teams 中生成命令机器人。

* 按照 [分步](../sbs-gs-notificationbot.yml) 指南在 Microsoft Teams 中生成通知机器人。

* 按照 [分步](../sbs-gs-workflow-bot.yml) 指南在 Microsoft Teams 中生成工作流机器人。

## <a name="see-also"></a>另请参阅

* [预配云资源](provision.md)
* [创建新的 Teams 项目](create-new-project.md)
