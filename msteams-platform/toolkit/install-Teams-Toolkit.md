---
title: 安装 Teams 工具包
author: zyxiaoyuer
description: 在本模块中，了解 Teams 工具包的安装
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: e079f023d931af48d5c06151c585a059c3f7f803
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833077"
---
# <a name="install-teams-toolkit"></a>安装 Teams 工具包

本文介绍如何安装 Teams 工具包扩展。

## <a name="prerequisites"></a>先决条件

::: zone pivot="visual-studio-code"

安装适用于 Visual Studio Code 的 Teams 工具包之前，需要[下载并安装 Visual Studio Code](https://code.visualstudio.com/Download)。

::: zone-end

::: zone pivot="visual-studio"

在安装 Teams Toolkit for Visual Studio 之前，需要使用 Visual Studio 安装程序[下载并安装 Visual Studio 2022](https://aka.ms/VSDownload)。

::: zone-end

::: zone pivot="visual-studio-code"

## <a name="install-teams-toolkit-for-visual-studio-code"></a>安装适用于 Visual Studio Code 的 Teams 工具包

可以使用 Visual Studio Code 中的“扩展”窗口安装 Teams 工具包，也可以从 Visual Studio 市场安装它。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. 启动 **Visual Studio Code**。
1.  (**Ctrl+Shift+X** / **⌘⇧-X** 或 **查看>扩展) 打开“扩展”** 窗口。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="屏幕截图显示如何安装。":::

1. 在搜索框中输入 **Teams 工具包** 。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="显示工具包的屏幕截图。":::

1. 选择“安装”。
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="显示安装工具包 4.0.0 的屏幕截图。":::

   在 Visual Studio Code 中成功安装 Teams 工具包后，Teams 工具包图标将显示在Visual Studio Code工具栏中。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="显示安装后的屏幕截图视图。":::

# <a name="marketplace"></a>[市场](#tab/marketplace)

1. 在 Web 浏览器中转到[Visual Studio Code市场](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-ttk-marketplace.png" alt-text="屏幕截图显示 TTK 市场的安装。":::

1. 选择“安装”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/Install-ttk.png" alt-text="显示如何安装 TTK 的屏幕截图。":::

1. 在弹出窗口中，选择“**打开**”以启动Visual Studio Code。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-open.png" alt-text="显示选择打开的屏幕截图。":::

   Teams 工具包扩展页显示在Visual Studio Code：

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ttk-in-vsc.png" alt-text="显示如何在 VSC 中选择 TTK 的屏幕截图。":::

1. 选择“安装”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/select-install-ttk.png" alt-text="屏幕截图显示如何选择“在 VSC 中安装 TTK”。":::

   在 Visual Studio Code 中成功安装 Teams 工具包后，Teams 工具包图标将显示在Visual Studio Code工具栏中。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/after-install.png" alt-text="显示安装后视图的屏幕截图。":::

---

## <a name="installing-a-different-release-version"></a>安装其他发布版本

默认情况下，Visual Studio Code会自动使 Teams 工具包保持最新状态。 如果要安装其他版本，请执行以下步骤：

* 从Visual Studio Code :::image type="icon" source="../assets/images/teams-toolkit-v2/extension icon.PNG"::: 工具栏中选择“扩展 () ”图标。
* 在搜索框中输入 **Teams 工具包**  。
* 在“Teams 工具包”页上，选择“ **卸载** ”按钮旁边的下拉箭头。
* 从菜单中选择 **“安装其他版本...”** ，然后选择要安装的版本。

## <a name="installing-a-pre-release-version"></a>安装预发布版本

GitHub 上还提供了适用于 Visual Studio Code 的 Teams 工具包扩展。 若要下载预发布，请转到 [GitHub 上的“发布”页](https://github.com/OfficeDev/TeamsFx/releases) ，并查找标记为预发行的扩展下载。

::: zone-end

::: zone pivot="visual-studio"

## <a name="install-teams-toolkit-for-visual-studio"></a>安装 Visual Studio 的 Teams 工具包

   > [!IMPORTANT]
   > 建议对 Teams 工具包使用 Visual Studio 2022 版本 17.3.3 或更高版本，这是最新版，用于修复 Visual Studio 早期版本中的多个已知问题。

1. [下载 Visual Studio 安装程序](https://aka.ms/VSDownload)，或打开它（如果已安装）。
2. 如果已安装 Visual Studio，请选择“ **安装**”或“ **修改** ”。
3. 选择“ **工作负载** ”选项卡，然后选择 **“ASP.NET 和 Web 开发** ”工作负载。
4. 在右侧的“**安装详细信息**”面板的“**可选**”部分选择 **Microsoft Teams 开发工具**。
5. 选择 **“修改** ”或“ **安装”** 以完成安装。

   :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-install_1.png" alt-text="屏幕截图显示如何安装 Visual Studio。":::

6. 安装完成后，选择“ **启动** ”以打开 Visual Studio。

    :::image type="content" source="../assets/images/teams-toolkit-overview/visual-studio-launch_1.png" alt-text="显示如何启动 Visual Studio 的屏幕截图。":::

::: zone-end

## <a name="next-steps"></a>后续步骤

安装 Teams 工具包后，请访问 [创建新的 Teams 项目](create-new-project.md) 以开始使用。

## <a name="see-also"></a>另请参阅

* [探索 Teams 工具包](explore-Teams-Toolkit.md)
* [使用 Teams 工具包创建新的 Teams 应用](create-new-project.md)
* [准备使用 Microsoft Teams 工具包生成应用](build-environments.md)
* [使用 Teams 工具包预配云资源](provision.md)
* [将 Teams 应用部署到云](deploy.md)
* [在 Visual Studio 中创建新的 Teams 应用](create-new-project.md#create-new-teams-app-in-visual-studio)
* [使用 Visual Studio 预配云资源](provision-cloud-resources.md)
* [使用 Visual Studio 将 Teams 应用部署到云](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)
