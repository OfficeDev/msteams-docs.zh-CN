---
title: Teams Toolkit概述
author: zyxiaoyuer
description: Teams Toolkit、Teams Toolkit和教程Toolkit概述
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 11/29/2021
ms.openlocfilehash: 0a048e12167847c1cc34560531cba13da9d74f8f
ms.sourcegitcommit: 58a24422bb04a529b6629a56803ed2efabc17cb1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2022
ms.locfileid: "62323161"
---
# <a name="teams-toolkit-overview"></a>Teams Toolkit概述

> [!NOTE]
> 目前，此功能仅适用于公共 **开发人员预览** 版。

Teams Toolkit允许你立即创建、调试和部署Teams应用Visual Studio Code。 使用工具包进行应用开发具有以下优点：

- 集成标识
- 访问云存储
- 来自 Microsoft Graph
- Azure 和 Microsoft 365零配置方法提供服务

Teams Toolkit将生成应用所需的全部工具Teams一个地方。

对于Teams应用开发，Teams Toolkit Visual Studio Code，可以使用 [CLI](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md) 工具，该工具由 `teamsfx`Toolkit 。

## <a name="user-journey-of-teams-toolkit"></a>用户旅程Teams Toolkit

Teams Toolkit自动执行手动工作，并提供与 Teams 和 Azure 资源的很好的集成。 下图显示了Teams Toolkit旅程：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey.png" alt-text="Teams Toolkit用户旅程" border="true":::

此旅程的主要里程碑是：

1. 首先创建新项目或尝试一个Teams应用程序。
1. 根据需要添加功能或编辑清单文件。
1. 使用 Microsoft 365 帐户生成和调试Teams应用。
1. 使用 Azure 帐户预配应用并部署到云。
1. 将应用发布到Teams。

## <a name="install-teams-toolkit-for-visual-studio-code"></a>安装Teams Toolkit Visual Studio Code

1. 打开 **Visual Studio Code。**
1. Select the Extensions view (**Ctrl+Shift+X** / **⌘⇧-X** or **View > Extensions)** ：

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="install":::

1. 在 **Teams Toolkit** 框中输入以下项：

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-2.png" alt-text="工具包":::

1. 选择 **安装**：
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install.png" alt-text="install toolkit":::

> [!TIP]
> 可以从应用商店Teams Toolkit Visual Studio Code[应用商店](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

## <a name="take-a-tour-of-teams-toolkit"></a>浏览Teams Toolkit

安装Toolkit后，你将看到Teams Toolkit UI，如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teams toolkit.png" alt-text="微型函数":::

可以选择"**快速入门**"浏览Teams Toolkit，也可以选择"新建 Teams **应用**"以创建一Teams项目。 在边栏中创建或打开Toolkit，可以查看所有现有功能Visual Studio Code列表。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/toolkit functions.png" alt-text="函数":::

让我们了解一下Teams Toolkit功能。

| Teams Toolkit功能 | 包括... | 可执行的操作 |
| --- | --- | --- |
| **Accounts** | &nbsp; | &nbsp; |
| &nbsp; | Microsoft 365帐户 | 将Microsoft 365帐户与有效的 E5 订阅一起用于生成应用。 |
| &nbsp; | Azure 帐户 | 使用 Azure 帐户在 Azure 上部署应用。 |
| **环境** | &nbsp; | &nbsp; |
| &nbsp; | local | 使用本地计算机环境配置在默认本地环境中部署应用。 |
| &nbsp; | dev | 使用远程或云环境配置在默认开发环境中部署应用。 你可创建更多环境（如需要）。 |
| **开发** | &nbsp; | &nbsp; |
| &nbsp; | 创建新的 Teams 应用 | 使用工具包向导为应用开发准备项目基架。 |
| &nbsp; | 查看示例 | 选择其中Teams Toolkit 12 个示例应用。 该工具包从 GitHub下载应用代码，你可以生成示例应用。 |
| &nbsp; | 添加功能 | 在开发过程中Teams应用Teams所需的其他功能。 |
| &nbsp; | 添加云资源 | 添加适合你的应用的可选云资源。 |
| &nbsp; | 编辑清单文件 | 编辑Teams客户端的应用Teams集成。 |
| **部署** | &nbsp; | &nbsp; |
| &nbsp; | 在云中预配 | 为应用程序分配 Azure 资源。 Teams Toolkit Azure 资源管理器集成。 |
| &nbsp; | Zip Teams元数据包 | 创建可上载到开发人员门户或开发人员Teams应用包。 它包含应用清单和应用图标。  |
| &nbsp; | 部署到云 | 将源代码部署到 Azure。 |
| &nbsp; | 发布到Teams | 发布开发的应用并将其分发到范围，例如个人、团队、频道或组织。 |
| &nbsp; | Teams 开发人员门户 | 使用开发人员门户配置和管理Teams应用程序。 |
| &nbsp; | CI/CD 指南 | 在构建应用程序的同时自动化Teams工作流。 |
| **帮助和反馈** | &nbsp; | &nbsp; |
| &nbsp; | 快速入门 | 查看Teams Toolkit中的"快速启动"Visual Studio Code。  |
| &nbsp; | 文档 | 选择访问开发人员Microsoft Teams文档。 |
| &nbsp; | 报告有关GitHub | 选择以访问GitHub页并引发任何问题。 |
|

> [!TIP]
> 在创建新问题之前浏览现有问题，或访问 [StackOverflow 标记 `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) 提交反馈。

## <a name="see-also"></a>另请参阅

* [使用新建项目Teams Toolkit](create-new-project.md)
* [准备帐户以生成Teams应用程序](accounts.md)
* [使用 Teams 工具包发布 Teams 应用](publish.md)
* [使用Teams Toolkit预配云资源](provision.md)
* [部署到云](deploy.md)
