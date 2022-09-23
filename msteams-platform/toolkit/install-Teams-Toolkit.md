---
title: 安装 Teams 工具包
author: zyxiaoyuer
description: 在本模块中，了解 Teams 工具包的安装
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 9b6492efed353e2f3228a04da292141679401e66
ms.sourcegitcommit: ef545fac5c0dbe970d81f53b1631930e9196eba3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/23/2022
ms.locfileid: "67991654"
---
# <a name="install-teams-toolkit"></a>安装 Teams 工具包

Teams 工具包是 Visual Studio 和 Visual Studio Code 中的扩展。 在本文档中，可以了解如何安装 Teams 工具包。

::: zone pivot="visual-studio-code"

## <a name="install-teams-toolkit-for-visual-studio-code"></a>安装适用于 Visual Studio Code 的 Teams 工具包

在开始安装之前，需要安装Visual Studio Code和 Teams 客户端。

## <a name="steps-to-install-teams-toolkit"></a>安装 Teams 工具包的步骤

可以从Visual Studio Code中的扩展和Visual Studio Code市场安装 Teams 工具包。 以下步骤可帮助你安装 Teams 工具包：

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. 打开 **Visual Studio Code**。
1. 选择“扩展”视图 (**Ctrl+Shift+X** / ⌘⇧ **-X** 或 **视图>扩展)**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="安装":::

1. 在搜索框中输入 **Teams 工具包** 。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="工具包":::

1. 选择“安装”。
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="安装工具包 4.0.0":::

   在Visual Studio Code成功安装 Teams 工具包后，Teams 工具包图标将显示在Visual Studio Code工具栏中。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="安装后":::

# <a name="marketplace"></a>[市场](#tab/marketplace)

1. 打开[Visual Studio Code市场](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

   将显示以下页面。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-ttk-marketplace.png" alt-text="安装 TTK 市场":::

1. 选择“安装”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Install-ttk.png" alt-text="安装 TTK":::

1. 在弹出窗口中，选择 **“打开**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-open.png" alt-text="选择打开的":::

   将显示以下Visual Studio Code页。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ttk-in-vsc.png" alt-text="在 VSC 中选择 TTK":::

1. 选择“安装”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="选择在 VSC 中安装 TTK":::

   在Visual Studio Code成功安装 Teams 工具包后，Teams 工具包图标将显示在Visual Studio Code工具栏中。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="安装后":::

---

#### <a name="upgrade-teams-toolkit"></a>升级 Teams 工具包

默认情况下，Teams 工具包将升级到最新版本。 以下步骤可帮助你安装不同的版本：

* 选择“扩展” :::image type="icon" source="../assets/images/teams-toolkit-v2/extension icon.PNG"::: 图标。
* 在搜索框中输入 **Teams 工具包**  。
* 在 Teams 工具包扩展中，选择 :::image type="icon" source="../assets/images/teams-toolkit-v2/setting icon.PNG"::: 图标。
* 选择 **“安装另一个版本** ”以升级到最新版本的 Teams 工具包。

::: zone-end

::: zone pivot="visual-studio"

## <a name="install-teams-toolkit-for-visual-studio"></a>安装 Visual Studio 的 Teams 工具包

在开始安装之前，需要安装Visual Studio 安装程序。

可以从 [Visual Studio 下载页面](https://visualstudio.microsoft.com)下载最新Visual Studio 安装程序。

## <a name="steps-to-install-teams-toolkit"></a>安装 Teams 工具包的步骤

打开Visual Studio 安装程序后，在弹出的工作负荷窗口中：

1. 选择 **ASP.NET 和 Web 开发** 工作负载。
1. 在 **“安装详细信息**”面板中选择 **Microsoft Teams 开发工具**。
1. 选择“安装”。

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install_1.png" alt-text="Visual studio-installation":::

1. 选择 **“启动** ”以打开 Visual Studio。

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch_1.png" alt-text="启动 visual Studio":::

   > [!IMPORTANT]
   > 建议下载 Visual Studio 2022 版本 17.3.3，因为适用于 Visual Studio 的 Teams 工具包在此版本中为 GA。 本文适用于 Visual Studio 2022 版本 17.3.3。 Teams 工具包版本 17.3.* 或更高版本。

::: zone-end

## <a name="see-also"></a>另请参阅

* [浏览 Teams 工具包](explore-Teams-Toolkit.md)
* [使用 Teams 工具包创建新的 Teams 应用](create-new-project.md)
* [准备使用 Microsoft Teams 工具包生成应用](build-environments.md)
* [使用 Teams 工具包预配云资源](provision.md)
* [将 Teams 应用部署到云](deploy.md)
* [在 Visual Studio 中创建新的 Teams 应用](create-new-teams-app-for-Visual-Studio.md)
* [使用 Visual Studio 预配云资源](provision-cloud-resources.md)
* [使用 Visual Studio 将 Teams 应用部署到云](deploy-teams-app.md)
