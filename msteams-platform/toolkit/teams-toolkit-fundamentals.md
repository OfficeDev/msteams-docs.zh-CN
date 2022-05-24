---
title: Teams 工具包概述
author: zyxiaoyuer
description: Teams 工具包概述、Teams 工具包安装和工具包功能概览
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/17/2022
ms.openlocfilehash: 36436b5cc2cf7edec784ab653b12d8cf44172b8b
ms.sourcegitcommit: 80edf3c964bb47a2ee13f9eda4334ad19e21f331
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2022
ms.locfileid: "65654600"
---
# <a name="teams-toolkit-overview"></a>Teams 工具包概述


适用于 Microsoft Visual Studio Code 的 Teams 工具包可帮助创建和部署具有集成标识、云存储访问、来自 Microsoft Graph 的数据以及采用零配置方法的其他 Azure 和 Microsoft 365 服务的 Teams 应用。 对于 Teams 应用开发，类似于适用于 Visual Studio 的 Teams 工具包，可以使用 [CLI 工具](https://github.com/OfficeDev/TeamsFx/blob/dev/docs/cli/user-manual.md)，其中包括工具包 `teamsfx`。
Teams 工具包允许直接从 Visual Studio Code 创建、调试和部署 Teams 应用。 使用工具包进行应用开发具有以下优点：

* 集成标识
* 对云存储的访问权限
* 来自 Microsoft Graph 的数据
* 采用零配置方法的 Azure 和 Microsoft 365 服务

Teams 工具包将构建 Teams 应用所需的所有工具集中在一处。

## <a name="user-journey-of-teams-toolkit"></a>Teams 工具包的用户旅程

Teams 工具包可自动执行手动工作，并提供 Teams 和 Azure 资源的强大集成。 下图显示了 Teams 工具包用户旅程：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/teams-toolkit-user-journey.png" alt-text="Teams 工具包用户旅程" border="true":::

此旅程的主要里程碑包括：

1. 首先创建新项目或尝试示例 Teams 应用。
1. 根据需要添加功能或编辑清单文件。
1. 使用 Microsoft 365 帐户构建和调试 Teams 应用。
1. 使用 Azure 帐户预配应用并将其部署到云。
1. 将应用发布到 Teams。

## <a name="install-teams-toolkit-for-visual-studio-code"></a>安装适用于 Visual Studio Code 的 Teams 工具包

1. 打开 **Visual Studio Code**。
1. 选择“扩展”视图 (**Ctrl+Shift+X** / ⌘⇧ **-X** 或 **视图>扩展)**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install toolkit-1.png" alt-text="安装":::

1. 在搜索框中输入 **Teams Toolkit**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit2.png" alt-text="工具包":::

1. 选择“**安装**”。
  
   :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/install-toolkit.png" alt-text="安装工具包 4.0.0":::

> [!TIP]
> 可以从 [Visual Studio Code 商城](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)安装 Teams 工具包。

## <a name="take-a-tour-of-teams-toolkit"></a>了解 Teams 工具包

安装工具包后，将看到 Teams 工具包 UI，如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/Teams-toolkit.png" alt-text="迷你功能":::

可以选择 **入门** 来浏览Teams Toolkit，或选择 **“新建Teams应用**”以创建一个Teams项目。 如果Visual Studio Code Teams Toolkit创建了Teams项目，则会看到具有所有功能的Teams Toolkit UI，如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teamstookit1.png" alt-text="teams 工具包的屏幕截图":::

让我们来看看本文档中介绍的主题。

## <a name="accounts"></a>帐户

若要开发 Teams 应用，至少需要一个具有有效订阅的 Microsoft 365 帐户。 如果要在 Azure 上托管后端资源，还需要 Azure 帐户。 Teams Toolkit支持用于登录、预配和部署 Azure 资源的集成体验。 可以在开始之前[创建免费的 Azure 帐户](https://azure.microsoft.com/free/)。

## <a name="environment"></a>环境

Teams 工具包可帮助创建和管理多个环境、预配项目并将其部署到 Teams 应用的目标环境。

### <a name="teamsfx-collaboration"></a>TeamsFx 协作

它允许开发人员和项目所有者邀请其他协作者加入 TeamsFx 项目，以调试、预配和部署相同的 TeamsFx 项目。

:::image type="content" source="../assets/images/teams-toolkit-v2/manual/teamsfx.png" alt-text="Teamsfx 项目":::

## <a name="development"></a>开发

Teams 工具包可帮助创建和自定义 Teams 应用项目，使 Teams 应用开发更简单。

### <a name="create-a-new-teams-app"></a>新建 Teams 应用

它通过使用Teams Toolkit创建新项目或 **从示例**"开始"菜单创建新的Teams **项目**，帮助你从Teams应用开发入门。

### <a name="add-features"></a>添加功能

它可帮助你以增量方式添加其他Teams功能，如 **Tab** 或 **Bot**，或者选择性地添加 Azure 资源（如 **Azure SQL 数据库** 或 **Azure 密钥保管库**，以满足当前Teams应用的开发需求。 还可以为Teams应用添加 **单一登录** 或 **CI/CD 工作流**。 

### <a name="edit-manifest-file"></a>编辑清单文件

它可帮助你编辑 Teams 应用与 Teams 客户端的集成。

## <a name="deployment"></a>部署

在开发期间或之后，请确保预配、部署和发布 Teams 应用，然后用户才能访问它。

### <a name="provision-in-the-cloud"></a>在云中预配

它与 Azure 资源管理器集成，使你能够预配应用程序需要用于代码方法的 Azure 资源。

### <a name="deploy-to-the-cloud"></a>部署到云

 它有助于将源代码部署到 Azure。

### <a name="publish-to-teams"></a>发布到 Teams

创建应用后，可以将应用分发到不同的范围，例如个人、团队、组织或任何人。 发布到 Teams 有助于发布开发的应用。

#### <a name="teamsfx-cli"></a>TeamsFx CLI

它是一个基于文本的命令行接口，可加速 Teams 应用程序开发，并启用 CI/CD 方案，以便在脚本中集成 CLI 来实现自动化。

#### <a name="teamsfx-sdk"></a>TeamsFx SDK

它可帮助将实施标识和云资源访问的任务减少到采用零配置的单行语句。

## <a name="help-and-feedback"></a>帮助和反馈

在本部分中，可以找到所需的文档和资源。 可以在 Teams 工具包中选择“**在 GitHub 上报告问题**”，以获得产品专家的 **快速支持**。 请在创建新问题之前先浏览问题，或访问 [StackOverflow 标记 `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) 提交反馈。

让我们来了解 Teams 工具包功能。

| Teams 工具包功能 | 包括... | 可执行的操作 |
| --- | --- | --- |
| **Accounts** | &nbsp; | &nbsp; |
| &nbsp; | Microsoft 365 账户 | 将 Microsoft 365 帐户与用于构建应用的有效 E5 订阅配合使用。 |
| &nbsp; | Azure 帐户 | 使用 Azure 帐户在 Azure 上部署应用。 |
| **环境** | &nbsp; | &nbsp; |
| &nbsp; | 本地 | 使用本地计算机环境配置在默认本地环境中部署应用。 |
| &nbsp; | 开发 | 使用远程或云环境配置在默认开发环境中部署应用。 可以根据需要创建更多环境。 |
| **开发** | &nbsp; | &nbsp; |
| &nbsp; | 新建 Teams 应用 | 使用工具包向导为应用开发准备项目基架。 |
| &nbsp; | 查看示例 | 选择 Teams 工具包的 12 个示例应用中的任何一个。 该工具包会从 GitHub 下载应用代码，你可以构建示例应用。 |
| &nbsp; | 添加功能 | - 在开发过程中将其他所需的Teams功能添加到Teams应用。 </br> - 添加适合应用的可选云资源。 |
| &nbsp; | 编辑清单文件 | 编辑 Teams 应用与 Teams 客户端的集成。 |
| **部署** | &nbsp; | &nbsp; |
| &nbsp; | 在云中预配 | 为应用程序分配 Azure 资源。 Teams 工具包与 Azure 资源管理器集成。 |
| &nbsp; | 压缩 Teams 元数据包 | 创建可上传到 Teams 或开发人员门户的应用包。 它包含应用清单和应用图标。  |
| &nbsp; | 部署到云 | 将源代码部署到 Azure。 |
| &nbsp; | 发布到 Teams | 发布开发的应用并将其分发到范围，例如个人、团队、频道或组织。 |
| &nbsp; | Teams 开发人员门户 | 使用开发人员门户配置和管理 Teams 应用。 |
| **帮助和反馈** | &nbsp; | &nbsp; |
| &nbsp; | 快速启动 | 在Visual Studio Code中查看Teams Toolkit快速入门帮助。  |
| &nbsp; | 教程 | 选择此选项可访问不同的教程。 |
| &nbsp; | 文档 | 选择此选项可访问 Microsoft Teams 开发人员文档。 |
| &nbsp; | 在 GitHub 上报告问题 | 选择此选项可访问 GitHub 页面并提出任何问题。 |


> [!TIP]
> 请在创建新问题之前先浏览现有问题，或访问 [StackOverflow 标记 `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) 提交反馈。

## <a name="see-also"></a>另请参阅

* [使用 Teams 工具包创建新项目](create-new-project.md)
* [准备帐户以生成 Teams 应用](accounts.md)
* [使用 Teams 工具包发布 Teams 应用](publish.md)
* [使用 Teams 工具包预配云资源](provision.md)
* [部署到云](deploy.md)
