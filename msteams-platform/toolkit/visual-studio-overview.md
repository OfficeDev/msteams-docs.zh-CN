---
title: 使用 Microsoft 团队工具包和 Visual Studio 生成应用程序
description: 开始在 Visual Studio 中使用 Microsoft 团队工具包直接构建强大的自定义应用程序
keywords: 团队 visual studio 工具包
ms.topic: overview
ms.openlocfilehash: 33005174dc1e12e6473522e7d7ee09920a989689
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651874"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a>使用 Microsoft 团队工具包和 Visual Studio 生成应用程序

Microsoft 团队工具包使您能够在 Visual Studio 集成开发环境 (IDE) 中直接创建自定义团队应用。 Microsoft 团队工具包将引导您完成此过程，并提供生成、调试和启动团队应用所需的所有内容。

## <a name="prerequisites"></a>先决条件

1. [启用开发人员预览](../resources/dev-preview/developer-preview-intro.md#enable-developer-preview)

1. 请确保已将** <span>ASP.NE</span>T 和 web 开发模块**添加到 Visual Studio 实例中。 您可以通过 [添加或删除工作负荷和组件文档，按照 Modify Visual Studio](/visualstudio/install/modify-visual-studio?view=vs-2019) 中的步骤进行检查。

![visual studio asp.net 模块](../assets/images/visual-studio-web-dev-module.png)

3. 如果您想要通过从 Visual Studio 部署应用程序来测试您的应用程序，您需要在开发环境中安装 IIS (Internet 信息服务) 。 Visual Studio 不包含 IIS，它不包含在默认的 Windows 10、Windows 8 或 Windows 7 配置中;但是，您可以从[Microsoft 下载中心](https://www.microsoft.com/download/details.aspx?id=48264.)下载最新版本。

![IIS 下载页面视图](../assets/images/iis.png)

## <a name="install-the-teams-toolkit"></a>安装团队工具包

Visual studio 的 Microsoft 团队工具包可从 [Visual Studio Marketplace](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.vsteamstemplate) 下载，也可直接从 visual studio 中的 " **扩展** " 菜单下载。

## <a name="using-the-toolkit"></a>使用工具包

- [设置新项目](#set-up-a-new-teams-project)
- [配置应用程序](#configure-your-app)
- [打包应用程序](#package-your-app)
- [在团队中运行应用程序](#install-and-run-your-app-locally)
- [验证您的应用程序](#validate-your-app)
- [发布应用程序](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>设置新的团队项目

1. 选择 " **新建项目**"。
1. 选择 " **Microsoft 团队应用** "，然后选择 " **下一步**"。
1. 您将收到 " **配置新项目** " 屏幕，您可在其中选择 **项目名称**、 **位置**和 **解决方案名称**。
1. 选中标记 " **将解决方案和项目放在同一目录中**" 的框。
1. 标有 " **添加功能** " 的弹出窗口将允许您为项目设置选择一个或多个功能。
1. 选择 " **下一步** " 按钮完成配置过程。
1. 标有 " **添加功能** " 的弹出窗口将允许您为每个选定的功能选择属性。
1. 选择 " **完成** "，你将在 **Microsoft 团队工具包** 登录页上进行土地。

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

> [!NOTE]
>如果尚未执行此操作，则需要登录到 Microsoft 365 或帐户，才能继续执行开发过程。
>
> 如果你没有 Microsoft 365 帐户，你可以注册 [microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program) 订阅。 它在90天内 *免费* 使用，并且将持续更新，只要你将其用于开发活动即可。 如果你有 Visual Studio *Enterprise* 或 *专业版* 订阅，这两个程序都包括一个免费的 Microsoft 365 [开发人员订阅](https://aka.ms/MyVisualStudioBenefits)，在 Visual Studio 订阅的生命周期内处于活动状态。 *请参阅*[设置 Microsoft 365 开发人员订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。
>

### <a name="configuration-steps"></a>配置步骤

1. 若要配置应用程序，请在 " **Microsoft 团队工具包** " 登录页上，选择 " **编辑应用程序包** "。
1. 从 " **我的环境** " 下拉菜单中，选择 " **开发**"。
1. 您将在 " **应用程序详细信息** " 页上放置，您可以在其中编辑应用程序的属性字段。
1. 编辑应用程序详细信息页中的字段将更新作为应用程序包一部分最终交付的文件上的 manifest.js的内容。 [了解详细信息](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>打包应用程序

修改**应用程序详细信息**页或更新**清单**，或应用程序的 **. publish**文件夹中的**env**文件将自动生成**Development.zip**文件。 Development.zip 文件包括三个所需的文件，即 **manifest.js打开** 和 [两个图标文件](../concepts/build-and-test/apps-package.md#icons)。

## <a name="install-and-run-your-app-locally"></a>在本地安装和运行应用程序

1. 从 " **解决方案配置** " 下拉菜单中选择 " **部署**"。

![解决方案配置菜单](../assets/images/solution-configurations.png)

2. 选择 " **ISS Express + 团队** " 按钮。

1. 团队将启动，并且应用程序安装对话框应显示在团队客户端中。

## <a name="validate-your-app"></a>验证您的应用程序

通过 " **验证** " 页面，您可以在将应用程序提交到 AppSource 之前检查应用程序包。 只需上传清单包，验证工具就会检查应用程序是否符合所有与清单相关的测试用例。 对于每个失败的测试，说明提供的文档链接可帮助您修复错误。 对于难以自动化的测试， **初步清单** 详细说明了最常见的失败测试事例的7，以及指向完整提交核对清单的链接。

## <a name="publish-your-app-to-teams"></a>将您的应用程序发布到团队

✔在项目主页上，您可以将应用程序上载到团队，将您的应用程序提交到贵组织中用户的公司自定义应用商店，或将应用程序提交到所有团队用户的应用程序源。

✔你的 IT 管理员将查看这些提交。

✔您可以返回到 " **发布** " 页面以检查提交状态，并了解您的应用程序是否已由 IT 管理员批准或拒绝。此外，您还可以将更新提交到您的应用程序或取消任何当前活动的提交。

> [!div class="nextstepaction"]
> [下一步：维护和支持发布的应用程序](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
>