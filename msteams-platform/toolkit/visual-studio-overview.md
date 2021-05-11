---
title: 使用 Microsoft Teams Toolkit 和 Visual Studio
description: 开始使用自定义工具直接在Visual Studio生成出色的自定义Microsoft Teams Toolkit
keywords: teams visual studio 工具包
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: bf8250e42bdf96073d729a19e921c400f242c67a
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020251"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio"></a>使用 Teams Toolkit 和 Visual Studio

借助 Microsoft Teams 工具包，可以直接在 Visual Studio 集成开发环境（IDE）中创建自定义 Teams 应用程序。 Microsoft Teams 工具包将引导你完成整个过程，并提供构建、调试和启动 Teams 应用所需的一切资源。

## <a name="prerequisites"></a>先决条件

1. [启用开发人员预览](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. 确保已 ASP.NE **<span></span>T** 和 Web 开发模块添加到Visual Studio实例。 通过添加或删除工作负载和组件[文档，可以按照修改Visual Studio中的步骤进行](/visualstudio/install/modify-visual-studio?view=vs-2019&preserve-view=true)检查。

![visual studio asp.net 模块](../assets/images/visual-studio-web-dev-module.png)

3. 如果你想要通过从应用程序部署应用来Visual Studio，则需要在开发环境中 (Internet Information Services) IIS 应用程序。 Visual Studio不包括 IIS，并且它不包含在默认 Windows 10、Windows 8 或 Windows 7 配置中;但是，你可以从 Microsoft 下载中心[下载最新版本](https://www.microsoft.com/download/details.aspx?id=48264)。

![IIS 下载页面视图](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>安装Teams Toolkit

可以从 Microsoft Teams Toolkit Visual Studio 应用商店或直接从 Visual Studio[内的](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate)"扩展"菜单中下载Visual Studio。 

## <a name="using-the-toolkit"></a>使用工具包

- [设置新项目](#set-up-a-new-teams-project)
- [配置应用程序](#configure-your-app)
- [打包应用](#package-your-app)
- [在应用商店中Teams](#install-and-run-your-app-locally)
- [验证你的应用](#validate-your-app)
- [发布应用程序](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>设置新的Teams项目

1. 选择 **创建新项目**。
1. 选择 **Microsoft Teams应用**"，然后选择"下一 **步"。**
1. 你将到达 **配置新项目屏幕**，可在其中选择Project **名称****、位置** 和 **解决方案名称**。
1. 选中标记为"将解决方案 **和项目放置在同一目录中"的框**。
1. 标记为"添加功能"的弹出窗口将允许你为项目设置选择一个或多个功能。
1. 选择" **下一** 步"按钮以完成配置过程。
1. 标记为"添加功能"的弹出窗口将允许你选择每个选定功能的属性。
1. 选择 **"完成**"，你将 **登录Microsoft Teams Toolkit登录** 页面。

## <a name="configure-your-app"></a>配置应用程序

应用程序的核心是Teams三个组件：

  1. The Microsoft Teams client (web， desktop or mobile) where users interact with your app.
  1. 响应将在应用程序中显示的内容请求的服务器，Teams HTML 选项卡内容或自动程序自适应卡片。
  1. 一Teams[文件](/concepts/build-and-test/apps-package.md)组成的应用包：

  > [!div class="checklist"]
  >
  > - 打开manifest.js
  > - [要显示在](../resources/schema/manifest-schema.md#icons)公共或组织应用程序目录中的应用的颜色图标
 > - 显示在[活动](../resources/schema/manifest-schema.md#icons)栏上的Teams图标。

安装应用后，Teams客户端将分析清单文件以确定所需信息，如应用名称和服务所在的 URL。

> [!NOTE]
>如果尚未登录，则需要登录帐户或帐户Microsoft 365继续开发过程。
>
> 如果你没有帐户，Microsoft 365注册开发人员计划[Microsoft 365订阅。](https://developer.microsoft.com/microsoft-365/dev-program) 它 *是免费的* 90 天，并且将持续续订，只要你使用它进行开发活动。 如果你有一个 Visual Studio *Enterprise* 或 *Professional* 订阅，这两个计划均包括免费 Microsoft 365 [开发人员](https://aka.ms/MyVisualStudioBenefits)订阅，在订阅生命周期内Visual Studio有效。 *请参阅*[设置开发人员Microsoft 365订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。
>

### <a name="configuration-steps"></a>配置步骤

1. 若要配置你的应用，请在 **登录Microsoft Teams Toolkit，** 选择"编辑 **应用包"。**
1. 从"**我的环境"** 下拉菜单中，选择"开发 **"。**
1. 你将登录" **应用详细信息** "页面，可在其中编辑应用的属性字段。
1. 编辑"应用详细信息"页中的字段将更新manifest.js文件（最终作为应用包的一部分提供）上的内容。 [了解更多](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>打包应用

修改 **应用程序详细信息** 页面或更新清单或应用的.publish 文件夹中的 **.env** 文件 **将** 自动生成Development.zip文件。 The Development.zip file includes three required files — the **manifest.json** and [two icons](../concepts/build-and-test/apps-package.md#app-icons).

## <a name="install-and-run-your-app-locally"></a>在本地安装和运行应用

1. 从"**解决方案配置"** 下拉菜单中，选择"部署 **"。**

!["解决方案配置"菜单](../assets/images/solution-configurations.png)

2. 选择 **"IIS Express + Teams"** 按钮。

1. Teams将启动，并且应用安装对话应显示在 Teams 客户端中。

## <a name="validate-your-app"></a>验证你的应用

" **验证** "页允许你在将应用提交到 AppSource 之前检查应用包。 只需上传清单包，验证工具将针对所有与清单相关的测试用例检查你的应用。 对于每个失败的测试，该说明都提供了一个文档链接，帮助您修复错误。 对于难以自动执行的测试，"初步检查表"详细介绍了最常见的失败测试用例 7，并链接到完整的提交清单。

## <a name="publish-your-app-to-teams"></a>将应用发布到 Teams

✔在项目主页上，可以将应用上传到团队，将应用提交到公司自定义应用商店供组织用户使用，或将应用提交到所有 Teams 用户的应用源。

✔ IT 管理员将查看这些提交。

✔你可以返回到"发布"页面，检查提交状态并了解你的应用是否已被 IT 管理员批准或拒绝。这也是你向应用提交更新或取消任何当前处于活动状态的提交的地方。

> [!div class="nextstepaction"]
> [下一步：维护和支持已发布的应用](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>
