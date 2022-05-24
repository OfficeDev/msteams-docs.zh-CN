---
title: Teams 工具包概述
author: zyxiaoyuer
description: Teams 工具包概述、Teams 工具包安装和工具包功能概览
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 05/17/2022
ms.openlocfilehash: 12ac74f64c4be69ff9b73ca2de1ee7c91917b259
ms.sourcegitcommit: 74623035d7c18194e339f566c820e0653bc3d8b6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2022
ms.locfileid: "65656857"
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
<!--  
Let's explore Teams Toolkit features.

| Teams Toolkit Features | Includes | What you can do |
| --- | --- | --- |
| **Accounts** | &nbsp; | &nbsp; |
| &nbsp; | Microsoft 365 account | Use your Microsoft 365 account with a valid E5 subscription for building your app. |
| &nbsp; | Azure account | Use your Azure account for deploying app on Azure. |
| **Environment** | &nbsp; | &nbsp; |
| &nbsp; | local | Deploy your app in the default local environment with local machine environment configurations. |
| &nbsp; | dev | Deploy your app in the default dev environment with remote or cloud environment configurations. You can create more environments, as you need. |
| **Development** | &nbsp; | &nbsp; |
| &nbsp; | Create a new Teams app | Use the toolkit wizard to prepare project scaffolding for app development. |
| &nbsp; | View samples | Select any of Teams Toolkit's 12 sample apps. The toolkit downloads the app code from GitHub, and you can build the sample app. |
| &nbsp; | Add Features | - Add other required Teams capabilities to Teams app during development process. </br> - Add optional cloud resources suitable for your app. |
| &nbsp; | Edit manifest file | Edit the Teams app integration with Teams client. |
| **Deployment** | &nbsp; | &nbsp; |
| &nbsp; | Provision in the cloud | Allocate Azure resources for your application. Teams Toolkit is integrated with Azure Resource Manager. |
| &nbsp; | Zip Teams metadata package | Create the app package that can be uploaded to Teams or Developer Portal. It contains the app manifest and app icons.  |
| &nbsp; | Deploy to the cloud | Deploy the source code to Azure. |
| &nbsp; | Publish to Teams | Publish your developed app and distribute it to scopes, such as personal, team, channel, or organization. |
| &nbsp; | Developer Portal for Teams | Use Developer Portal to configure and manage your Teams app. |
| **Help and Feedback** | &nbsp; | &nbsp; |
| &nbsp; | Quick start | View the Teams Toolkit Quick start help within Visual Studio Code.  |
| &nbsp; | Tutorial | Select to access different tutorials. |
| &nbsp; | Documentation | Select to access the Microsoft Teams Developer Documentation. |
| &nbsp; | Report issues on GitHub | Select to access GitHub page and raise any issues. |

-->
> [!TIP]
> 请在创建新问题之前先浏览现有问题，或访问 [StackOverflow 标记 `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) 提交反馈。

## <a name="see-also"></a>另请参阅

* [使用 Teams 工具包创建新项目](create-new-project.md)
* [准备帐户以生成 Teams 应用](accounts.md)
* [使用 Teams 工具包发布 Teams 应用](publish.md)
* [使用 Teams 工具包预配云资源](provision.md)
* [部署到云](deploy.md)
