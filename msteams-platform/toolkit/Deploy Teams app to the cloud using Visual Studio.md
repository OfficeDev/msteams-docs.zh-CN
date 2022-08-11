---
title: 使用 Visual Studio 将 Teams 应用部署到云
author: surbhigupta
description: 在本模块中，了解如何将应用部署到云、Azure 或 SharePoint，并在 Visual Studio 中使用 Teams 工具包部署 Teams 应用
ms.author: v-amprasad
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 4cf2267f4392289f14c3ec3438abd66cf9fb1769
ms.sourcegitcommit: 60484634f38642048e9a9a1465ac0c3322c8229a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2022
ms.locfileid: "67290118"
---
# <a name="deploy-teams-app-to-the-cloud-using-visual-studio"></a>使用 Visual Studio 将 Teams 应用部署到云

Teams 工具包可帮助你将应用程序的前端和后端代码部署或上传到 Azure 订阅中预配的云资源。 部署后，可以在 Teams 客户端或 Web 浏览器中预览应用，然后才能开始使用。 可在 Visual Studio 中部署以下应用：

* Tab 应用（如前端应用程序）部署到 Azure 存储，配置为静态 Web 托管。
* 可以将具有 Azure 函数触发器的通知机器人应用部署到 Azure 函数。
* 机器人应用或消息扩展可以部署到 Azure 应用服务。

## <a name="prerequisite"></a>先决条件

下面是生成和部署应用所需的工具列表。

| &nbsp; | 安装 | 用于使用... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Visual Studio 2022 版本 17.3 | 可以安装 Visual Studio 的企业版，并安装“ASP.NET”工作负荷和 Microsoft Teams 开发工具。 |
| &nbsp; | Teams 工具包 | 一个 Visual Studio 扩展，用于为应用创建项目基架。 使用最新版本。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | 通过聊天、会议、通话等应用与每一位同事进行协作的 Microsoft Teams - 一个地方完成所有操作。 |
| &nbsp; | Azure 工具和 [Microsoft Azure CLI](/cli/azure/install-azure-cli) | 用于访问存储数据或在 Azure 中为 Teams 应用部署基于云的后端的 Azure 工具。 |

  > [!NOTE]
  > 在将项目代码部署到云之前， [请为 TTK Visual Studio 预配云资源](provision VS.md)。

## <a name="deploy-teams-app-using-teams-toolkit"></a>使用 Teams 工具包部署 Teams 应用

1. 启动 Visual Studio。
1. 选择 **“创建新项目** ”或从列表中打开现有项目。
1. 右键单击项目 **MyTeamsApp1**。
1. 选择 **Teams 工具包**。
1. 选择 **“部署到云...”**

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-cloud.png" alt-text="部署到云":::

   > [!NOTE]
   > 在此方案中，项目名称为 MyTeamsApp1。

6. 在确认对话框中选择 **“部署** ”。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-confirmation.png" alt-text="“部署到云确认”对话框":::

7. 触发并完成部署过程后，可以看到一个弹出窗口，其中确认已成功部署。 还可以检查输出窗口中的状态。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/VS-deploy-popup.png" alt-text="部署到云弹出窗口":::

成功将项目部署到 Azure 后，可以通过不同的方式在 Teams 工具包中预览应用：

1. 选择 **Project** > **Teams 工具包** > **Zip 应用包** 以生成 Teams 应用包。
1. 选择 **“本地** ”或 **“适用于 Azure”** 选项并上传到 Teams 客户端。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-ZipApp-package.png" alt-text="生成 Teams 应用包":::

**在 Teams 客户端中预览应用**

1. 选择 **“项目”**
1. 选择 **Teams 工具包**。
1. **在 Teams 中选择预览** 版。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams1.png" alt-text="Teams 客户端中的预览 Teams 应用":::

预览应用的另一种方法：

1. 右键单击解决方案资源管理器面板下的项目 **MyTeamsApp1**。
1. 选择 **Teams 工具包**。
1. **在 Teams 中选择“预览**”以在 Web 浏览器中启动 Teams 应用。

   :::image type="content" source="../assets/images/deploy-teams-app-cloud-vs/vs-deploy-preview-teams.png" alt-text="Web 浏览器中的预览团队应用":::

   > [!NOTE]
   > “项目”菜单中提供了相同的菜单选项。

## <a name="see-also"></a>另请参阅

* [在 Visual Studio 中创建新的 Teams 应用](create-new-teams-app-for-Visual-Studio.md)
* [使用 Visual Studio 预配云资源](Provision%20cloud%20resources%20using%20Visual%20Studio.md)
* [使用 Visual Studio 编辑 Teams 应用清单](VS-TeamsFx-preview-and-customize-app-manifest.md)
* [使用 Visual Studio 在本地调试 Teams 应用](debug-teams-app-visual-studio.md)
