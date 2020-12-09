---
title: 使用 Microsoft 团队工具包和 Visual Studio Code 生成应用程序
description: 开始在 Visual Studio Code 中使用 Microsoft 团队工具包直接构建强大的自定义应用程序
keywords: 团队 visual studio code 工具包
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 350da030d15e72e2cad51c5967afab9b6f29fe9e
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49604471"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>使用团队工具包和 Visual Studio Code 生成应用程序

Microsoft 团队工具包使你能够在 Visual Studio Code 环境中直接创建自定义团队应用。 该工具包将引导您完成整个过程，并提供生成、调试和启动团队应用程序所需的所有内容。

## <a name="installing-the-teams-toolkit"></a>安装团队工具包

Visual studio Code 的 Microsoft 团队工具包可从 [Visual Studio Marketplace](https://aka.ms/teams-toolkit) 下载，也可直接作为 Visual studio code 中的扩展。

> [!TIP]
> 安装完成后，应在 Visual Studio Code 活动栏中看到 "团队" 工具包。 如果不是，请在活动栏中右键单击，然后选择 " **Microsoft 团队** " 以固定该工具包以方便访问。

## <a name="using-the-toolkit"></a>使用工具包

- [设置新项目](#set-up-a-new-teams-project)
- [导入现有项目](#import-an-existing-teams-app-project)
- [配置应用程序](#configure-your-app)
- [打包应用程序](#package-your-app)
- [在本地或在团队中运行应用程序](#run-your-app)

## <a name="set-up-a-new-teams-project"></a>设置新的团队项目

1. 在本地环境中为项目创建一个工作区/文件夹。
1. 在 Visual Studio Code 中，选择 "团队" 图标 ![Teams 图标](../assets/icons/favicon-16x16.png) 从窗口左侧的活动栏中进行。
1. 从 "命令" 菜单中选择 **"打开 Microsoft 团队工具包"** 。
1. 从 "命令" 菜单中选择 " **创建新的团队应用** "。
1. 出现提示时，输入工作区的名称。 这将用作项目将驻留的文件夹的名称和应用程序的默认名称。
1. 按 **enter** ，你将进入 " **添加功能** " 屏幕，为新应用配置属性。
1. 选择 " **完成** " 按钮完成配置过程。

## <a name="import-an-existing-teams-app-project"></a>导入现有团队应用程序项目

1. 在 Visual Studio Code 中，选择 "团队" 图标 ![Teams 图标](../assets/icons/favicon-16x16.png) 从窗口左侧的活动栏中进行。
1. 从 "命令" 菜单中选择 " **导入应用程序包** "。
1. 选择现有 [团队应用程序包](../concepts/build-and-test/apps-package.md) zip 文件。
1. 选择 " **选择发布包** " 按钮。 此时，工具包的 "配置" 选项卡应包含您的应用程序的详细信息。
1. 在 visual studio code 中，选择 "**文件**" "  ->  **将文件夹添加到工作区**"，将源代码目录添加到 Visual studio code Workspace。

## <a name="configure-your-app"></a>配置应用程序

在其核心中，团队应用程序包含三个组件：

  1. Microsoft 团队客户端 (web、桌面或移动) ，用户与您的应用程序进行交互。
  1. 对将在团队中显示的内容请求做出响应的服务器，例如，HTML 选项卡内容或 bot 自适应卡。
  1. 由三个文件组成的团队 [应用程序包](/concepts/build-and-test/apps-package.md) ：

  > [!div class="checklist"]
  >
  > - 上的 manifest.js 
  > - 显示在公用或组织应用程序目录中的应用程序的[彩色图标](../resources/schema/manifest-schema.md#icons)
 > - "团队" 活动栏中显示的 [大纲图标](../resources/schema/manifest-schema.md#icons) 。

在安装应用程序时，团队客户端会分析清单文件以确定所需的信息，如应用程序的名称和服务所在的 URL。

1. 若要配置您的应用程序，请导航到 Visual Studio Code 中的 " **Microsoft 团队工具包** " 选项卡。
1. 选择 " **编辑应用程序包** " 以查看 **应用程序详细信息** 页。
1. 编辑应用程序详细信息页中的字段将更新作为应用程序包一部分最终交付的文件上的 manifest.js的内容。 *请参阅*[应用程序 Studio 清单编辑器](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>打包应用程序

在应用程序的 **. publish** 文件夹中修改 **应用程序详细信息** 页、**清单** 或 **env** 文件将自动生成 **Development.zip** 文件。 您需要在同一文件夹中包含 [两个图标](../concepts/build-and-test/apps-package.md#app-icons) 。

## <a name="install-and-run-your-app-locally"></a>在本地安装和运行应用程序

## <a name="run-your-app"></a>运行应用程序

### <a name="install-and-run-your-app-locally"></a>在本地安装和运行应用程序

有关如何打包和测试您的应用程序的详细说明，请参阅在项目主页中 *生成和运行* 内容。 通常情况下，您需要安装应用程序的服务器，使其运行，然后设置隧道解决方案，以便团队可以访问本地主机中运行的内容。

### <a name="enable-development-from-localhost"></a>启用从 localhost 开发

如果您希望使用 HTTPS 在 localhost 上调试基于选项卡的应用程序，您需要告诉浏览器信任正在提供的应用程序 <https://localhost> 。 导航到 <https://localhost:3000/tab>。 如果您看到一条警告消息，指示该网站不受信任，请选择 "继续" 选项。 现在应可以从团队客户端访问您的应用程序。

### <a name="run-your-app-in-teams"></a>在团队中运行应用程序

先决条件： [启用团队开发人员预览模式](https://aka.ms/teams-toolkit-enable-devpreview)

1. 导航到 Visual Studio "代码" 窗口左侧的 "活动" 栏。
1. 选择 " **运行** " 图标以显示 " **运行" 和 "调试** " 视图。
1. 您还可以使用键盘快捷方式 `Ctrl+Shift+D` 。

> [!div class="nextstepaction"]
> [下一步：维护和支持发布的应用程序](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
