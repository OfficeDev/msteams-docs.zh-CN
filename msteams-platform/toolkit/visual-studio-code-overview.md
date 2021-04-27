---
title: 使用 Microsoft Teams Toolkit 和 Visual Studio 代码生成应用
description: 开始使用 Microsoft Teams Visual Studio直接在 Visual Studio Code 中生成出色的自定义Toolkit
keywords: teams visual studio code toolkit
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 59f2943f37856c42346b2ffad4e01d88910679ae
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020259"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>使用 Teams 应用和Toolkit Visual Studio生成应用

借助 Microsoft Teams 工具包，可以直接在 Visual Studio Code 环境中创建自定义 Teams 应用程序。 此工具包将引导你完成整个过程，并提供构建、调试和启动 Teams 应用所需的一切资源。

## <a name="installing-the-teams-toolkit"></a>安装 Teams Toolkit

Microsoft Teams Toolkit for Visual Studio Code 可从 Visual Studio [Marketplace](https://aka.ms/teams-toolkit) 下载，或直接作为 Visual Studio Code 中的扩展。

> [!TIP]
> 安装后，你应该会看到 Teams Toolkit代码Visual Studio栏中。 如果没有，请在活动栏中右键单击并选择 Microsoft **Teams** 固定工具包，方便访问。

## <a name="using-the-toolkit"></a>使用工具包

- [设置新项目](#set-up-a-new-teams-project)
- [导入现有项目](#import-an-existing-teams-app-project)
- [配置应用程序](#configure-your-app)
- [打包应用](#package-your-app)
- [在本地或在 Teams 中运行应用](#run-your-app)

## <a name="set-up-a-new-teams-project"></a>设置新的 Teams 项目

1. 在本地环境中为项目创建工作区/文件夹。
1. 在Visual Studio代码"中，选择 Teams 图标 ![Teams 图标](../assets/icons/favicon-16x16.png) 从窗口左侧的活动栏中。
1. 从 **命令菜单中选择Toolkit** 打开 Microsoft Teams 选项。
1. 从 **命令菜单中选择创建新的 Teams** 应用。
1. 当系统提示时，输入工作区的名称。 这将同时用作项目将驻留的文件夹的名称以及应用的默认名称。
1. 按 **Enter，** 你将到达" **添加功能"** 屏幕，为新应用配置属性。
1. 选择" **完成** "按钮以完成配置过程。

## <a name="import-an-existing-teams-app-project"></a>导入现有 Teams 应用项目

1. 在Visual Studio代码"中，选择 Teams 图标 ![Teams 图标](../assets/icons/favicon-16x16.png) 从窗口左侧的活动栏中。
1. 从 **命令菜单中选择** 导入应用包。
1. 选择现有的 [Teams 应用包](../concepts/build-and-test/apps-package.md) zip 文件。
1. 选择" **选择发布程序包"** 按钮。 现在，应该使用应用的详细信息填充工具包的配置选项卡。
1. In Visual Studio Code， select **File**  ->  **Add Folder to Workspace** to add your source code directory to the Visual Studio Code workspace.

## <a name="configure-your-app"></a>配置应用程序

Teams 应用的核心包括三个组件：

  1. Microsoft Teams 客户端 (Web、桌面或移动) 用户与你的应用进行交互。
  1. 响应将在 Teams 中显示的内容请求的服务器，例如 HTML 选项卡内容或自动程序自适应卡片。
  1. 包含 [三个文件的](/concepts/build-and-test/apps-package.md) Teams 应用包：

  > [!div class="checklist"]
  >
  > - 打开manifest.js 
  > - [要显示在](../resources/schema/manifest-schema.md#icons)公共或组织应用程序目录中的应用的颜色图标
 > - 显示在 [Teams](../resources/schema/manifest-schema.md#icons) 活动栏上的大纲图标。

安装应用后，Teams 客户端将分析清单文件以确定所需信息，如应用名称和服务所在的 URL。

1. 若要配置你的应用，请导航到 Microsoft **Teams Toolkit** 代码Visual Studio选项卡。
1. 选择 **"编辑应用包** "以查看 **"应用详细信息"** 页。
1. 编辑"应用详细信息"页中的字段将更新manifest.js文件（最终作为应用包的一部分提供）上的内容。 *请参阅* [App Studio 清单编辑器](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>打包应用

修改 **应用的**.publish文件夹中的应用程序详细信息页面、清单或 **.env** 文件将自动生成 **Development.zip文件。** 你需要在同一文件夹中 [包含两](../concepts/build-and-test/apps-package.md#app-icons) 个图标。

## <a name="install-and-run-your-app-locally"></a>在本地安装和运行应用

## <a name="run-your-app"></a>运行应用

### <a name="install-and-run-your-app-locally"></a>在本地安装和运行应用

有关如何打包 *和测试应用的* 详细说明，请参阅项目主页中的 *生成和运行内容。 通常，你需要安装你的应用的服务器，使它运行，然后设置隧道解决方案，以便 Teams 可以访问从 localhost 运行的内容。

### <a name="enable-development-from-localhost"></a>从 localhost 启用开发

如果你想要使用 HTTPS 在 localhost 上调试基于选项卡的应用，则需要告诉浏览器信任从 中提供的应用 <https://localhost> 。 导航到 <https://localhost:3000/tab>。 如果您看到一条指示该网站不受信任的警告，请选择继续继续的选项。 现在，你的应用应可从 Teams 客户端访问。

### <a name="run-your-app-in-teams"></a>在 Teams 中运行应用

先决条件： [启用 Teams 开发人员预览模式](https://aka.ms/teams-toolkit-enable-devpreview)

1. 导航到"代码"窗口左侧的活动Visual Studio栏。
1. 选择" **运行** "图标以显示 **"运行和调试"** 视图。
1. 您还可以使用键盘快捷方式 `Ctrl+Shift+D` 。

> [!div class="nextstepaction"]
> [下一步：维护和支持已发布的应用](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
