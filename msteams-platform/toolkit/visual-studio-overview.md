---
title: 使用 Teams Toolkit 和 Visual Studio
description: 开始使用自定义工具直接在Visual Studio生成出色的自定义Microsoft Teams Toolkit
keywords: teams visual studio 工具包
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 996037f5bb1caaa2493e1eebe51039724822fef9
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949697"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>使用 Teams Toolkit 和 Visual Studio

借助 Microsoft Teams 工具包，可以直接在 Visual Studio 集成开发环境（IDE）中创建自定义 Teams 应用程序。 Microsoft Teams 工具包将引导你完成整个过程，并提供构建、调试和启动 Teams 应用所需的一切资源。

## <a name="prerequisites"></a>先决条件

1. [启用开发人员预览](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)。

1. 确保已 ASP.NE **<span></span>T** 和 Web 开发模块添加到Visual Studio实例。 通过添加或删除工作负载和组件文档，可以按照Visual Studio中的[步骤进行](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)检查。

![Visual studio asp.net 模块](../assets/images/visual-studio-web-dev-module.png)

3. 如果要通过从应用程序部署应用来测试Visual Studio，则必须在Internet Information Services (环境中) ) IIS 应用程序。 Visual Studio IIS，并且它不包含在默认 Windows 10、Windows 8 或 Windows 7 配置中;但是，你可以从 Microsoft 下载中心[下载最新版本](https://www.microsoft.com/download/details.aspx?id=48264)。

![IIS 下载页面视图](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>安装Teams Toolkit

可以从 Microsoft Teams Toolkit Visual Studio 应用商店或直接从 Visual Studio[内的](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)"扩展"菜单中下载Visual Studio。  从 Visual Studio Marketplace 下载[Teams Toolkit for Visual Studio 2019。](https://marketplace.visualstudio.com/items?itemName=msft-vsteamstoolkit.vsteamstoolkit)

## <a name="using-the-toolkit"></a>使用工具包

- [设置新项目](#set-up-a-new-teams-project)
- [配置应用程序](#configure-your-app)
- [打包应用](#package-your-app)
- [在客户端安装并运行Teams](#install-and-run-your-app-locally)
- [验证你的应用](#validate-your-app)
- [发布应用程序](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>设置新的Teams项目

![Teams工具包](../assets/images/teamstoolkiticon.png)

1. 选择 **创建新项目**。

    ![新建项目](../assets/images/createnewproject.png)

1. 选择适用于应用的快速 **入门工具Microsoft Teams下** 一 **步"。**
1. 在"**配置新项目"** 页中，Project **名称、****位置** 和 **解决方案名称**。
1. 选中" **将解决方案和项目放置在同一目录中"** 复选框。
1. 在 **"添加功能** "弹出窗口中，为项目设置选择一个或多个功能。
1. 选择" **下一** 步"按钮以完成配置过程。
1. 在 **"添加功能** "弹出窗口中，选择每个选定功能的属性。
1. 选择 **“完成”**。 将显示 **Microsoft Teams Toolkit** 登录页面。

    ![Teams工具包登录页面](../assets/images/Teamstoolkitpage.png)

## <a name="configure-your-app"></a>配置应用程序

应用程序的核心是Teams三个组件：

  1. 用户Microsoft Teams应用的客户端（包括 Web、桌面或移动）。
  1. 响应对内容请求的服务器，Teams HTML 选项卡内容或自动程序自适应卡片。
  1. 应用Teams包包含三个文件：

      - 打开manifest.js
      - 要 [显示在](../resources/schema/manifest-schema.md#icons) 公共或组织应用程序目录中的应用的颜色图标。
      - 显示在[活动](../resources/schema/manifest-schema.md#icons)栏上的Teams图标。

安装应用后，Teams客户端将分析清单文件以确定所需信息，如应用名称和服务所在的 URL。

> [!NOTE]
>如果尚未登录，则必须登录到 Microsoft 365 帐户，以继续进行开发过程。
>
> 如果你没有帐户，Microsoft 365注册开发人员计划[Microsoft 365订阅。](https://developer.microsoft.com/microsoft-365/dev-program) 它是免费的 90 天，只要你使用它进行开发活动，它将续订。 如果你有一个 Visual Studio Enterprise 或 Professional 订阅，这两个计划均Microsoft 365[免费](https://aka.ms/MyVisualStudioBenefits)开发人员订阅，在订阅生命周期内Visual Studio有效。 有关详细信息，请参阅[设置开发人员Microsoft 365订阅](/office/developer-program/office-365-developer-program-get-started)。

### <a name="configuration-steps"></a>配置步骤

1. 若要配置你的应用，请在 **登录Microsoft Teams Toolkit，** 选择"编辑 **应用包"。**
1. 从"**我的环境"** 下拉菜单中，选择"开发 **"。**
1. 在 **"应用详细信息** "页中，编辑应用的属性字段。
    
    编辑"应用详细信息"页中的字段将更新应用程序manifest.js中将作为应用包的一部分提供的文件上的内容。 有关详细信息，请参阅Teams Toolkit[清单](https://aka.ms/teams-toolkit-manifest)。

## <a name="package-your-app"></a>打包应用

修改 **应用程序详细信息** 页面或更新清单或应用的.publish 文件夹中的 **.env** 文件 **将** 自动生成Development.zip文件。 the Development.zip file includes three required files， the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).

## <a name="install-and-run-your-app-locally"></a>在本地安装和运行应用

1. 从" **解决方案配置"** 下拉菜单中 **，选择"** 部署"，如下图所示：

    !["解决方案配置"菜单](../assets/images/solution-configurations.png)

1. 选择 **"IIS Express + Teams"** 按钮。

    应用程序安装对话框将显示在客户端Teams中。

## <a name="validate-your-app"></a>验证你的应用

" **验证** "页允许你在将应用提交到 AppSource 之前检查应用包。 只需上传清单包，验证工具将针对所有与清单相关的测试用例检查你的应用。 对于每个失败的测试，该说明都提供了一个文档链接，帮助您修复错误。 对于难以自动执行的测试，"初步检查表"详细介绍了最常见的失败测试用例 7，并链接到完整的提交清单。

## <a name="publish-your-app-to-teams"></a>将应用发布到 Teams

* 在项目主页上，你可以将应用上载到团队、将应用提交到公司自定义应用商店供你组织的用户使用，或将应用提交到所有 Teams 用户的应用源。

* IT 管理员将审阅这些提交。

* 你可以返回到发布 **页面** ，检查你的提交状态，并了解你的应用是否已被 IT 管理员批准或拒绝。这同样也是你可以向应用提交更新或取消任何当前处于活动状态的提交的地方。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [维护和支持已发布的应用](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
