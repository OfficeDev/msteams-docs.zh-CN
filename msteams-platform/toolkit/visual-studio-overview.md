---
title: 使用 Microsoft Teams 安全和Toolkit生成Visual Studio
description: 使用 Microsoft Teams 服务器直接在 Visual Studio内构建出色的自定义Toolkit
keywords: Teams Visual Studio 工具包
ms.topic: overview
ms.openlocfilehash: 79ea22cfd154313247132c22684d444c0813c66f
ms.sourcegitcommit: 9fd61042e8be513c2b2bd8a33ab5e9e6498d65c5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/20/2020
ms.locfileid: "46819201"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a>使用 Microsoft Teams 安全和 Toolkit构建Visual Studio

Microsoft Teams Toolkit允许你在开发人员的集成开发环境内直接 Visual Studio创建自定义 Teams 应用， (IDE) 。 Microsoft Teams 工具包将指导你完成该过程，并提供生成、调试和启动 Teams 应用所需的一切。

## <a name="prerequisites"></a>先决条件

1. [启用开发人员预览版](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. 确保已 **<span>ASP.NE</span>您的 Web 开发模块** 添加到您的 Visual Studio。 您可以通过添加或删除工作负载和 [组件文档来按照"修改Visual Studio中的步骤进行检查](/visualstudio/install/modify-visual-studio?view=vs-2019) 。

![Visual Studio asp.net模块](../assets/images/visual-studio-web-dev-module.png)

3. 如果希望通过从应用程序部署应用程序来测试 Visual Studio您的应用程序，则需要在 (Internet Information Services) 安装 IIS 应用程序。 Visual Studio不包含 IIS，并且未将其包含在默认的 Windows 10、Windows 8 或 Windows 7 配置中;但是，你可以从 Microsoft 下载中心 [下载最新版本](https://www.microsoft.com/download/details.aspx?id=48264)。

![IIS 下载页面视图](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>安装 Teams Toolkit

Microsoft Teams Toolkit for Visual Studio可从 [Visual Studio Marketplace 下载或](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) 直接从 Visual Studio 中的" **扩展"** 菜单下载。

## <a name="using-the-toolkit"></a>使用工具包

- [设置新项目](#set-up-a-new-teams-project)
- [配置应用程序](#configure-your-app)
- [打包应用](#package-your-app)
- [在 Teams 中运行应用](#install-and-run-your-app-locally)
- [验证你的应用](#validate-your-app)
- [发布应用](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>设置新的 Teams 项目

1. 选择 **"创建新项目"。**
1. 选择**Microsoft Teams 应用，然后选择**"下一**步"。**
1. 你将会到达"配置**您的新建项目**"屏幕，你可以在其中选择**项目名称、****位置和**解决方案**名称**。
1. 选中标有文件夹 **的框，并在相同目录中标记为"放置解决方案"和项目**。
1. 标记为"添加功能 **"的弹出** 窗口将允许你为项目设置选择一个或多个功能。
1. 选择" **下一** 步"按钮以完成配置过程。
1. 标记为"添加功能" **的弹出** 窗口将允许你为每个选定功能选择属性。
1. 选择 **"** 完成"，然后登录 **Microsoft Teams Toolkit** 登录页面。

## <a name="configure-your-app"></a>配置应用程序

Teams 应用从核心来托管三个组件：

  1. Microsoft Teams 客户端可 (应用交互的) 应用或移动版应用程序。
  1. 响应将要在 Teams 中显示的内容请求的服务器，例如 HTML 选项卡内容或自动程序自适应卡片。
  1. 一个 [包含三](/concepts/build-and-test/apps-package.md) 个文件的 Teams 应用包：

  > [!div class="checklist"]
  >
  > - 打开manifest.js打开
  > - 要 [在公共](../resources/schema/manifest-schema.md#icons) 或组织应用程序目录中显示的应用的颜色图标
 > - 显示在[outline icon](../resources/schema/manifest-schema.md#icons) Teams 活动栏上的大纲图标。

安装应用后，Teams 客户端将分析清单文件，以确定所需的信息，如应用的名称和服务所在的 URL。

> [!NOTE]
>如果你尚未执行此操作，将需要登录 Microsoft 365 或帐户才能继续进行开发过程。
>
> 如果没有 Microsoft 365 帐户，可注册 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program) 订阅。 可以免 *费提供* 90 天，将不续续订，只要你将其用于开发活动。 如果你有新的Visual Studio *企业版* 或 *专业版* 订阅，这两种计划均包括免费的 Microsoft 365 [开发人员订阅](https://aka.ms/MyVisualStudioBenefits)，在生命周期订阅的Visual Studio活动。 *请参阅*[设置 Microsoft 365 开发人员订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。
>

### <a name="configuration-steps"></a>配置步骤

1. 若要配置应用，请在**Microsoft Teams 硬件硬件Toolkit，** 选择"编辑**应用包"。**
1. 从"**我的环境"** 下拉菜单中，选择"**开发"。**
1. 你将在"应用 **详细信息"** 页上编辑应用的属性字段。
1. 编辑应用详细信息页中的字段会更新 manifest.json file 的内容，这些文件最终将作为应用包的一部分提供。 [了解更多](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>打包应用

修改应用**详细信息页面**或更新**清单，或**应用 **.publish**文件夹中的 **.env**文件将自动生成**Development.zip**文件。 该Development.zip文件包括三个必需的文件，**即manifest.js个**[和两个图标文件](../concepts/build-and-test/apps-package.md#icons)。

## <a name="install-and-run-your-app-locally"></a>在本地安装和运行应用程序

1. 从"**解决方案配置"下拉**菜单中，选择"**部署"。**

!["解决方案配置"菜单](../assets/images/solution-configurations.png)

2. 选择 **"ISS 快速 + Teams"** 按钮。

1. Teams 将启动，且应用安装对话框应出现在 Teams 客户端中。

## <a name="validate-your-app"></a>验证你的应用

" **验证** "页面允许你在将应用提交到 AppSource 前检查应用包。 只需上载清单包，验证工具即可针对所有与清单相关的测试用例检查您的应用程序。 对于每个失败的测试，说明会提供一个可帮助您修复错误的文档链接。 对于难以自动化的测试， **最常见的失败** 测试用例的初步检查表详细信息 7 以及指向完整提交清单的链接。

## <a name="publish-your-app-to-teams"></a>将应用发布到 Teams

✔在项目主页上，可将应用上传到团队、为公司用户将应用提交到公司自定义应用商店，也可以针对所有 Teams 用户将应用提交到 App Source。

✔ IT 管理员会查看这些提交。

✔可以返回到" **发布"** 页面检查提交状态，并了解应用是否由 IT 管理员批准或拒绝。这也是将向应用提交更新或取消任何当前活动提交的地点。

> [!div class="nextstepaction"]
> [下一步：维护和支持已发布的应用](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
