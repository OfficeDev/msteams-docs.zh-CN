---
title: 探索 Teams 工具包
author: zyxiaoyuer
description: 在本模块中，了解如何探索 Teams 工具包
ms.author: zhany
ms.localizationpriority: medium
ms.topic: overview
ms.date: 07/29/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 0fa31c52b206738cfb174519fc6d3c445b604a8e
ms.sourcegitcommit: c3601696cced9aadc764f1e734646ee7711f154c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2022
ms.locfileid: "68833126"
---
# <a name="explore-teams-toolkit"></a>探索 Teams 工具包

在此文档中，可以了解适用于 Visual Studio Code 和 Visual Studio 的 Teams 工具包中的不同 UI 元素以及说明和基本用法。

::: zone pivot="visual-studio-code"

## <a name="teams-toolkit-for-visual-studio-code-basic-ui-elements"></a>用于Visual Studio Code基本 UI 元素的 Teams 工具包

安装 Teams 工具包后，你将看到 Teams 工具包 UI，如下图所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/overview1.png" alt-text="Teams 工具包概述":::

| 序列号 | UI 元素 | 定义 |
| --- | --- |
| 1 | **入门** | 探索 Teams 工具包。 |
| &nbsp; | **教程** | 访问不同的教程。 |
| &nbsp; | **文档** | 访问 Microsoft Teams 开发人员文档。 |
| 2 | **创建新的 Teams 应用** | 根据要求创建新的 Teams 应用。 |
| 3 | **查看示例** | 基于现有示例生成不同类型的应用。 |
| 4 | **打开文件夹** | 打开现有 Teams 应用。 |
| 5 | **新建文件** | 创建新文件。 |
| &nbsp; | **打开文件** | 打开现有文件。 |
| &nbsp; | **打开文件夹** | 打开现有文件夹。 |
| 6 | **最近** | 查看最近的文件。 |

### <a name="exploring-the-teams-toolkit-task-pane"></a>浏览 Teams 工具包任务窗格

可以从 Teams 工具包的任务窗格中浏览更多 UI 元素。 只有在使用 Teams 工具包创建应用后，任务窗格才可见。 以下视频可帮助你了解创建新 Teams 应用的过程，完成此过程后，可以在 Teams 工具包中查看任务窗格。

   ![创建 Teams 应用](~/assets/videos/javascript-tab-app1.gif)

创建新的 Teams 应用后，可以在左侧面板中看到应用的目录结构，在右侧面板中看到自述文件。

:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/first-page.png" alt-text="Teams 工具包的第一页":::

让我们来了解一下 Teams 工具包 UI。

 在Visual Studio Code工具栏中，以下图标与 Teams 工具包相关：

| 图标 | 说明 |
| --- | --- |
| **资源管理器** :::image type="icon" source="../assets/images/teams-toolkit-v2/file-explorer-icon.PNG":::  | 查看应用的目录结构。 |
| **运行和调试** :::image type="icon" source="../assets/images/teams-toolkit-v2/run-debug-icon.PNG":::  | 启动本地或远程调试过程。 |
| **Teams 工具包** :::image type="icon" source="../assets/images/teams-toolkit-v2/teams-toolkit-sidebar-icon.PNG"::: | 在 Teams 工具包中查看任务窗格。 |

在任务窗格中，可以看到以下部分：

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/accounts1.png" alt-text="accounts 部分":::
   :::column-end:::
   :::column span="":::

        若要开发 Teams 应用，需要以下帐户：
        
        * **登录到 M365**：使用具有有效 E5 订阅的 Microsoft 365 帐户生成应用。

        * **登录到 Azure**：使用 Azure 帐户在 Azure 上部署应用。 可以在开始之前[创建免费的 Azure 帐户](https://azure.microsoft.com/free/)。
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/environment1.png" alt-text="“环境”部分":::
   :::column-end:::
   :::column span="":::

        若要部署 Teams 应用，需要以下环境：
        
       * **local**：使用本地计算机环境配置在默认本地环境中部署应用。

        * **dev**：使用远程或云环境配置在默认开发环境中部署应用。 可以根据需要创建更多环境。
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/development.png" alt-text="开发部分":::
   :::column-end:::
   :::column span="":::

        若要创建和自定义 Teams 应用，需要以下功能：
        
       * **创建新的 Teams 应用**：使用工具包向导为应用开发准备项目基架。

        * **查看示例**：选择 Teams 工具包的任何示例应用。 该工具包会从 GitHub 下载应用代码，你可以构建示例应用。
        
        * **添加功能**：在开发过程中向 Teams 应用添加其他必需的 Teams 功能，并添加适合你的应用的可选云资源。
       
        * **编辑清单文件**：编辑 Teams 应用与 Teams 客户端的集成。
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/deployment1.png" alt-text="部署部分":::
   :::column-end:::
   :::column span="":::

        若要预配、部署和发布 Teams 应用，需要以下功能：
        
        * **在云中预配**：为应用程序分配 Azure 资源。 Teams 工具包与 Azure 资源管理器集成。

        * **Zip Teams 元数据包**：创建可上传到 Teams 或开发人员门户的应用包。 它包含应用清单和应用图标。
        
        * **部署到云**：将源代码部署到 Azure。
       
        * **发布到 Teams**：发布开发的应用并将其分发到个人、团队、频道或组织等范围。
        
        * **Teams 开发人员门户**：使用开发人员门户配置和管理 Teams 应用。 
   :::column-end:::
:::row-end:::

:::row:::
   :::column span="":::
      :::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/help-and-feedback1.png" alt-text="帮助和反馈部分":::
   :::column-end:::
   :::column span="":::

        访问有关 Teams 工具包的详细信息。 需要以下文档和资源。
        
        * **入门**：查看Visual Studio Code中的 Teams 工具包入门帮助。

        * **教程**：选择 以访问不同的教程。
        
        * **文档**：选择以访问 Microsoft Teams 开发人员文档。
       
        * **在 GitHub 上报告问题**：选择以访问 GitHub 页面并引发任何问题。
   :::column-end:::
:::row-end:::

::: zone-end

::: zone pivot="visual-studio"

## <a name="explore-teams-toolkit-for-visual-studio"></a>探索适用于 Visual Studio 的 Teams 工具包

安装 Teams 工具包后，可以通过两种不同的方法查看 Teams 工具包选项：

# <a name="project"></a>[项目](#tab/prj)

可以在 **“项目**”下访问 Teams 工具包。

1. 选择 **“项目** > **Teams 工具包**”。
1. 现在可以访问不同的 Teams 工具包选项。

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu_1.png" alt-text="Teams 工具包操作菜单":::

# <a name="solution-explorer"></a>[解决方案资源管理器](#tab/solutionexplorer)

   可以在 **解决方案资源管理器** 下访问 Teams 工具包。

1. 选择“**视图** > **解决方案资源管理器**”可查看解决方案资源管理器面板。
1. 右键单击 **“项目**”。
1. 选择 **“Teams 工具包”** 以访问不同的 Teams 工具包选项。

   :::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-operations-menu1_1.png" alt-text="Project 的 Teams 工具包操作":::

   > [!NOTE]
   > 在此方案中，项目名称为 **MyTeamsApp1**。

---

创建 Teams 项目后，可以在 Teams Toolkit for Visual Studio 上执行以下函数：

:::image type="content" source="../assets/images/teams-toolkit-overview/teams-toolkit-menu-options.png"alt-text="“项目”菜单中的 Teams 工具包操作":::

|功能  |说明  |
|---------|---------|
|准备 Teams 应用依赖项     |执行本地调试之前，执行此步骤有助于设置本地调试依赖项并在 Teams 平台中注册 Teams 应用。 你需要一个 Microsoft 365 帐户。 有关详细信息，请参阅 [使用 Visual Studio 在本地调试 Teams 应用](debug-local.md)         |
|打开清单文件     |若要打开 Teams 清单文件，可以将鼠标悬停在参数上以预览值。 有关详细信息，请参阅 [使用 Visual Studio 编辑 Teams 应用清单](VS-TeamsFx-preview-and-customize-app-manifest.md)         |
|在 Teams 开发人员门户中更新清单     |更新清单文件时，只有这样，才能将清单文件重新部署到 Azure，而无需再次部署整个项目。 使用此命令将更改更新到远程。 有关详细信息，请参阅 [使用 Visual Studio 编辑 Teams 应用清单](VS-TeamsFx-preview-and-customize-app-manifest.md)       |
|预配到云     |此选项可帮助你创建托管 Teams 应用的 Azure 资源。 有关详细信息，请参阅 [使用 Visual Studio 预配云资源](provision-cloud-resources.md)        |
|部署到云     |此选项可帮助你将代码复制到“预配到云”时创建的 Azure 资源。 有关详细信息，请参阅 [使用 Visual Studio 将 Teams 应用部署到云](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)        |
|Teams 中的预览版     |此选项启动 Teams Web 客户端，并允许在浏览器中预览 Teams 应用。         |
|Zip 应用包     |此选项在项目下的 文件夹中生成 Teams 应用包 `Build` 。 可以将包上传到 Teams 客户端并运行 Teams 应用。         |

::: zone-end

## <a name="see-also"></a>另请参阅

* [安装 Teams 工具包](install-Teams-Toolkit.md)
* [使用 Teams 工具包创建新的 Teams 应用](create-new-project.md)
* [准备使用 Microsoft Teams 工具包生成应用](build-environments.md)
* [使用 Teams 工具包预配云资源](provision.md)
* [在 Visual Studio 中创建新的 Teams 应用](create-new-project.md#create-new-teams-app-in-visual-studio)
* [使用 Visual Studio 预配云资源](provision-cloud-resources.md)
* [使用 Visual Studio 将 Teams 应用部署到云](deploy.md#deploy-teams-app-to-the-cloud-using-visual-studio)

<!--  
:::image type="content" source="../assets/images/teams-toolkit-v2/teams toolkit fundamentals/ui-elements.png" alt-text="UI Elements":::

|Section|Features|Details
|---------|---------|--------|
| **1. ACCOUNTS** | &nbsp; | &nbsp; |
| &nbsp; |Microsoft 365 account|  Use your Microsoft 365 account with a valid E5 subscription for building your app.|
| &nbsp; | Azure Account |  Use your Azure account for deploying app on Azure. You can [create a free Azure account](https://azure.microsoft.com/free/) before you start.|
|**2.ENVIRONMENT** |  &nbsp; | &nbsp;|
| &nbsp; |Local |Deploy your app in the default local environment with local machine environment configurations.|
| &nbsp; | Dev |Deploy your app in the default dev environment with remote or cloud environment configurations. You can create more environments, as you need.|
| **3.DEVELOPMENT** | &nbsp; | &nbsp; |
| &nbsp; | Create a new Teams app | Teams Toolkit helps you to create and customize your Teams app project that makes the Teams app development work simpler. Create a new Teams app helps you to start with Teams app development by creating new Teams project using Teams Toolkit either by using **Create new project**|
| &nbsp; | View Samples | Select any of Teams Toolkit's sample apps. The toolkit downloads the app code from GitHub, and you can build the sample app.|
| &nbsp; | Add Features | It helps you to add additional Teams capabilities such as **Tab** or **Bot** or **Message extension** or **Command bot** or **Notification bot**, or **SSO enabled tab** optionally add Azure resources such as **Azure SQL Database** or **Azure Key Vault**, or **Azure function** or **Azure API Management** which fits your development needs to your current Teams app. You can also add **API connection** or **Single Sign-on** or **CI/CD workflows** for your Teams app.
| &nbsp; | Edit Manifest file | It helps you customize manifest file based on the app requirements |
| **4.DEPLOYMENT** | &nbsp; | &nbsp; |
| &nbsp;| Provision in the cloud | Allocate Azure resources for your application. Teams Toolkit is integrated with Azure Resource Manager.|
| &nbsp; | Zip Teams metadata package| Create the app package that can be uploaded to Teams or Developer Portal. It contains the app manifest and app icons. |
| &nbsp; | Deploy to the cloud| Deploy the source code to Azure.|
| &nbsp; | Publish to Teams| Publish your developed app and distribute it to scopes, such as personal, team, channel, or organization.|
| &nbsp; | Developer Portal for Teams| It is the primary tool for configuring, distributing, and managing your Microsoft Teams apps. You can collaborate with colleagues on your app, set up runtime environments, and much more. |
| **5.HELP AND FEEDBACK** | &nbsp; | &nbsp; |
| &nbsp; | Get Started |  View the Teams Toolkit Get started help within Visual Studio Code.|
| &nbsp; | Tutorials| Select to access different tutorials.|
| &nbsp; | Documentation| Select to access the Microsoft Teams Developer Documentation.|
| &nbsp; | Report issues on GitHub| It helps to get **Quick support** from product expert. Browse the existing issues before you create a new one, or visit [StackOverflow tag `teams-toolkit`](https://stackoverflow.com/questions/tagged/teams-toolkit) to submit feedback.|
| **6.Explorer** | &nbsp; | &nbsp; |
 &nbsp; | &nbsp; | It helps to view the directory structure of your app.|
| **7.Run and Debug** | &nbsp; | &nbsp; |
 &nbsp; | &nbsp; | To start the local or remote debug process.|
-->
