---
title: 新建 Teams 应用
author: zyxiaoyuer
description: 在本模块中，了解如何使用 Teams 工具包创建新的 Teams 应用
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/14/2022
ms.openlocfilehash: 8500f5ba1f54b28f68f9b56c0a42aedfff108e64
ms.sourcegitcommit: c806c5ffe277c740d0d7b8f62e72ade562029194
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2022
ms.locfileid: "67617794"
---
# <a name="create-a-new-teams-project"></a>创建新的 Teams 项目

可以通过在 Teams 工具包中选择 **“创建新的 Teams 应用** ”来生成新的 Teams 项目。 可以在 Teams 工具包中创建以下类型的应用：

| 应用类型 | 定义 |
| --- | --- |
| 基本 Teams 应用 | 基本 Teams 应用是选项卡、机器人或消息扩展应用，可以根据需要创建和自定义该应用。 |
| 基于方案的 Teams 应用 | 基于方案的 Teams 应用是通知机器人、命令机器人、已启用 SSO 的选项卡或 SPFx 选项卡应用，适用于一个特定方案。 例如，通知机器人仅适用于发送通知而不用于聊天。 |

## <a name="create-a-new-teams-app"></a>新建 Teams 应用

创建新 Teams 应用的步骤与所有类型的应用（SPFx 和通知机器人除外）类似。 以下步骤可帮助你构建新的 Tab 应用：

**创建应用**

1. 打开 Visual Studio Code。

1. 选择左侧导航栏中的 Teams 工具包 :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.png"::: 图标。

1. 选择 **创建新的 Teams 应用**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. 确保 **选项卡** 已选中为应用功能。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-capabilities-tabapp.png" alt-text="选择应用功能":::

1. 选择 **JavaScript** 作为编程语言。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-language-tab.png" alt-text="显示如何选择编程语言的屏幕截图。":::

1. 选择 **默认文件夹** 以将项目根文件夹存储在默认位置。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-default-location.png" alt-text="选择默认位置":::

   以下步骤指导你更改默认位置：

      1. 选择 **“浏览**”。

          :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/select-browse.png" alt-text="选择浏览以进行存储":::

      1. 选择项目工作区的位置。

      1. 选择 **“选择文件夹**”。

          :::image type="content" source="../assets/images/teams-toolkit-v2/select-folder.png" alt-text="用于存储的 select-folder":::

1. 输入 `helloworld` 为应用程序名称。 确保仅使用字母数字字符。 选择“**Enter**”。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/enter-name-tab1.png" alt-text="显示在何处输入应用名称的屏幕截图。":::

1. 默认情况下，项目将在 10 秒内在新窗口中打开。 如果要在当前窗口中打开，请 **在当前窗口中选择“打开**”。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/new-window-notification.png" alt-text="新窗口通知":::

   Teams 选项卡应用在几秒钟内创建。

    :::image type="content" source="../assets/images/teams-toolkit-v2/first-tab/tap-app-created1.png" alt-text="显示已创建应用的屏幕截图。":::


### <a name="directory-structure-for-different-app-types"></a>不同应用类型的目录结构

Teams 工具包提供用于生成应用的所有组件。 创建项目后，可以在 **资源管理器** 下查看项目文件夹和文件。

<br>
<details>
<summary><b>基本 Teams 应用的目录结构</b></summary>

你有三种不同类型的基本 Teams 应用，目录结构看起来与所有类型的应用类似。 以下示例演示基本的 Teams 选项卡应用目录结构：

| 文件夹名 | 目录 |
| --- | --- |
| `.fx/configs` | 用户可以为 Teams 应用自定义的配置文件。 |
| - `.fx/configs/config.<envName>.json` | 每个环境的配置文件。 |
| - `.fx/configs/azure.parameters.<envName>.json` | 适用于每个环境的 Azure BICEP 预配的参数文件。 |
| - `.fx/configs/projectSettings.json` | 适用于所有环境的全局项目设置。 |
| `tabs` | 运行时所需的 Tab 功能代码，例如隐私通知、使用条款和配置选项卡。 |
| - `tabs/src/index.jsx` | 前端应用的入口点，其中主应用组件随之呈现 `ReactDOM.render()` |
| - `tabs/src/components/App.jsx` | 用于处理应用中的 URL 路由的代码。 它调用了 [JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md) 应用和团队之间建立通信。 |
| - `tabs/src/components/Tab.jsx` | 用于实现应用 UI 的代码。 |
| - `tabs/src/components/TabConfig.jsx` | 用于实现配置应用的 UI 的代码。 |
| `templates/appPackage` | 应用清单模板文件和应用图标：color.png和outline.png。 |
| - `templates/appPackage/manifest.template.json` | 用于在本地或远程环境中运行应用的应用清单。  |
| `templates/azure` | BICEP 模板文件 |

> [!NOTE]
> 如果有机器人或消息扩展应用，则将相关文件夹添加到目录结构。

若要详细了解不同类型的基本 Teams 应用的目录结构，请参阅下表：

| 应用类型 | 链接 |
| --- | --- |
| 对于选项卡应用 | [使用 JavaScript 生成第一个选项卡应用](../sbs-gs-javascript.yml) |
| 对于机器人应用 | [使用 JavaScript 生成第一个机器人应用](../sbs-gs-bot.yml) |
| 对于消息扩展应用 | [使用 JavaScript 生成第一个消息传递扩展应用](../sbs-gs-msgext.yml) |

</details>
<br>
<details>
<summary><b>基于方案的 Teams 应用的目录结构</b></summary>

你有四种不同类型的基于方案的 Teams 应用，目录结构看起来与所有类型的应用类似。 以下示例演示基于方案的通知机器人 Teams 应用目录结构：

新的项目文件夹包含以下内容：

| 文件夹名 | 目录 |
| --- | --- |
| `.fx` | 项目级别设置、配置和环境信息 |
| `.vscode` | 本地调试的 VS 代码文件 |
| `bot` | 机器人源代码 |
| `templates` | Teams 应用清单和相应 Azure 资源的模板 |

**机器人** 文件夹中的核心通知实现及其包含：

| 文件名 | 目录 |
| --- | --- |
| `src/adaptiveCards/` | 自适应卡片模板  |
| `src/internal/` | 为通知功能生成的初始化代码 |
| `src/index.*s` | 用于处理机器人消息和发送通知的入口点 |
| `.gitignore` | 要从机器人项目中排除本地文件的文件 |
| `package.json` | 机器人项目的 npm 包文件 |

> [!NOTE]
> 如果有命令机器人、启用 SSO 的选项卡或 SPFx 选项卡应用，则将相关文件夹添加到目录结构中。

若要详细了解不同类型的基于方案的 Teams 应用的目录结构，请参阅下表：

| 应用类型 | 链接 |
| --- | --- |
| 对于通知机器人应用 | [向 Teams 发送通知](../sbs-gs-notificationbot.yml) |
| 对于命令机器人应用 | [生成命令机器人](../sbs-gs-commandbot.yml) |
| 对于 SPFx 选项卡应用 | [使用 SPFx 构建 Teams 应用](../sbs-gs-spfx.yml) |

</details>
<br>
<details>
<summary><b>多功能应用的目录结构</b></summary>

可以使用添加功能将更多功能添加到现有 Teams 应用。 例如，如果将机器人应用添加到现有选项卡应用，Teams 工具包会添加包含相关文件和代码的机器人文件夹。

下图显示了 Tab 应用的目录结构：

   :::image type="content" source="../assets/images/teams-toolkit-v2/tabapp-directory.png" alt-text="Tab 应用目录结构":::

下图显示了具有机器人功能的 Tab 应用的目录结构：

   :::image type="content" source="../assets/images/teams-toolkit-v2/tab-app-with-bot-app.png" alt-text="具有机器人应用目录结构的 Tab 应用":::

</details>

## <a name="see-also"></a>另请参阅

* [使用 Blazor 构建 Teams 应用](../sbs-gs-blazorupdate.yml)
* [使用 C# 或 .NET 构建 Teams 应用](../sbs-gs-csharp.yml)
* [所有类型的环境和创建 Teams 应用的先决条件](tools-prerequisites.md)
* [准备使用 Microsoft Teams 工具包生成应用](build-environments.md)
