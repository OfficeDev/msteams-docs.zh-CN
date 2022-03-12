---
title: 使用应用和Teams Toolkit生成Visual Studio
description: 开始使用自定义工具直接在 Visual Studio 生成出色的Microsoft Teams Toolkit。 了解如何在开发人员门户Visual Studio应用、验证应用，以及从开发人员门户Visual Studio应用。
keywords: teams visual studio 工具包
ms.localizationpriority: medium
ms.topic: overview
ms.date: 1/13/2022
ms.author: johmil
ms.openlocfilehash: c34f1113cd4da5f1b416dba6bc950b3588accecf
ms.sourcegitcommit: 8a0ffd21c800eecfcd6d1b5c4abd8c107fcf3d33
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/12/2022
ms.locfileid: "63453420"
---
# <a name="teams-toolkit-for-visual-studio"></a>Visual Studio 的Teams工具包

构建、测试和开发 IDE Teams应用程序。

Teams Toolkit Visual Studio 的扩展，可轻松创建 Teams 的新项目、在 Teams 开发人员门户中自动设置应用、在 Teams 中运行和调试、配置云托管以及从 IDE 使用 [TeamsFx](https://github.com/OfficeDev/teamsfx)。

## <a name="install-teams-toolkit-for-visual-studio"></a>安装Teams Toolkit Visual Studio

>[!NOTE]
> 作为先决条件，请确保使用 Visual Studio 2022 17.1 Preview 2 或更高版本按照下面的说明进行操作。

1. 如果已安装 2022 17.1 Visual Studio 2，请跳到下一步。 否则，[请安装 Visual Studio 2022 Preview](https://visualstudio.microsoft.com/vs/preview/)。
2. 打开Visual Studio 安装程序。
3. 为 **现有的** VS 2022 Preview 安装选择"修改"。
4. 选择 ASP.NET **和 Web 开发** 工作负载。
5. 在右侧，展开"**ASP.NET 和 Web** 开发"部分，Microsoft Teams **可选组件列表中的"** 开发工具"。
6. 选择 **"****安装"** Visual Studio 安装程序"修改"以完成安装过程。

![选择Microsoft Teams安装程序.Visual Studio中的) 工具。](images/teams-development-tools-vs-installer.png)

## <a name="get-started-quickly-with-a-new-project"></a>快速开始使用新项目

Teams Toolkit模板提供开始使用应用项目所需的全部代码、文件和Teams配置。

通过Microsoft Teams应用项目模板，Microsoft 365自动注册和配置新应用所需的Teams帐户。

> [!NOTE]
> 如果你没有帐户，Microsoft 365注册开发人员计划Microsoft 365[订阅](https://developer.microsoft.com/microsoft-365/dev-program)。 它是免费的 90 天，只要你使用它进行开发活动，它将续订。 如果你有一个 Visual Studio Enterprise 或 Professional 订阅，这两个计划均Microsoft 365[免费](https://aka.ms/MyVisualStudioBenefits)开发人员订阅，在订阅生命周期内Visual Studio有效。 有关详细信息，请参阅[设置开发人员Microsoft 365订阅](/office/developer-program/office-365-developer-program-get-started)。

1. 启动 Visual Studio 2022。
1. 在"开始"窗口中， **选择"新建项目"**。
1. 在"**搜索模板"** 框中，输入"Microsoft Teams应用"。
1. 选择"**Microsoft Teams"模板**，然后选择"下一 **步"**。
1. 在"**配置新项目"窗口中**，在"新建项目名称"框中键入或Project **HelloTeams**。 然后，选择" **创建"**。
1. 在"**新建Teams应用程序**"窗口中，选择或Microsoft 365选择 **帐户选择器登录帐户**。 然后，选择" **创建"**。

![在 Microsoft Teams 中创建新的 Visual Studio 应用Visual Studio。](images/teams-toolkit-vs-new-project.png)

Visual Studio将打开新项目，Teams Toolkit开发人员门户中设置Teams新项目。 将为链接到上述步骤中Teams帐户的 Microsoft 365 组织添加项目，并创建新的Azure Active Directory注册。 这是应用在应用中运行Teams。

## <a name="run-and-debug-your-app-in-teams"></a>在应用程序中运行和调试Teams

你可以从本地启动本地运行的应用Visual Studio。

1. 打开或[创建Teams应用项目](#get-started-quickly-with-a-new-project)。
2. 按 **F5** 或选择"调试 **">"开始** 调试Visual Studio"。

Visual Studio将在浏览器中启动Teams应用项目并开始调试。

## <a name="host-your-teams-app-in-the-cloud-and-preview-it"></a>在Teams托管应用并预览

可以创建和自动配置云资源，以使用云资源在 Azure 中Teams Toolkit。

1. 选择"**Project > Teams Toolkit >云"菜单中的"预配**"。
2. 在"选择订阅"窗口中，选择要用于创建资源的 Azure 订阅。

Teams Toolkit将在此订阅中创建 Azure 资源，但此步骤中未部署任何代码。 若要将项目部署到这些新资源：

1. 选择"**Project > Teams Toolkit >云"菜单中的"部署**"。

## <a name="preview-your-app-running-from-cloud-resources"></a>预览从云资源运行的应用

可以使用远程资源在浏览器中运行应用，以验证一切是否正常工作。 在此方案中，无法进行调试。

1. 选择"**Project > Teams Toolkit >预览Teams应用"** 菜单。

你的应用将在浏览器中打开，并使用预配和部署步骤创建的资源。

## <a name="publish-your-app-to-teams"></a>将应用发布到 Teams

在 Teams [](https://dev.teams.microsoft.com/home)开发人员门户中，你可以将应用上载到团队、将应用提交到组织中用户的公司自定义应用商店，或将应用提交到所有 Teams 用户的应用源。

- IT 管理员将审阅这些提交。
- 你可以返回到发布 **页面** ，检查你的提交状态，并了解你的应用是否已被 IT 管理员批准或拒绝。这同样也是你可以向应用提交更新或取消任何当前处于活动状态的提交的地方。
