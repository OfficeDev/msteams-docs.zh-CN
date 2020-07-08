---
title: 使用 Microsoft 团队工具包和 Visual Studio 生成应用程序
description: 开始在 Visual Studio 中使用 Microsoft 团队工具包直接构建强大的自定义应用程序
keywords: 团队 visual studio 工具包
ms.date: 06/30/2020
ms.openlocfilehash: e5715cf23cfd221b65afe0e6258ce06ff98770aa
ms.sourcegitcommit: 694babb79d379360a20cf928a9d2b88dd6d3bdd0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "45051711"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio"></a>使用 Microsoft 团队工具包和 Visual Studio 生成应用程序

Microsoft 团队工具包使您能够在 Visual Studio 环境中直接创建自定义团队应用。 该工具包将引导您完成整个过程，并提供生成、调试和启动团队应用程序所需的所有内容。

## <a name="installing-the-teams-toolkit"></a>安装团队工具包

Visual studio 的 Microsoft 团队工具包可从[Visual Studio Marketplace](https://aka.ms/teams-toolkit)下载或直接作为 visual studio 中的扩展。

## <a name="using-the-toolkit"></a>使用工具包

- [设置新项目](#set-up-a-new-teams-project)
- [配置应用程序](#configure-your-app)
- [打包应用程序](#package-your-app)
- [在团队中运行应用程序](#install-and-run-your-app-locally)
- [验证您的应用程序](#validate-your-app)
- [发布应用程序](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>设置新的团队项目

1. 创建一个新项目并选择 "Microsoft Terams 工具包" 模板。
1. 你将进入 "**添加功能**" 屏幕，为新应用配置属性。
1. 选择 "**完成**" 按钮完成配置过程。

## <a name="configure-your-app"></a>配置应用程序

在其核心中，团队应用程序包含三个组件：

  1. Microsoft 团队客户端（web、桌面或移动版），用户与您的应用程序进行交互。
  1. 对将在团队中显示的内容请求做出响应的服务器，例如，HTML 选项卡内容或 bot 自适应卡。
  1. 由三个文件组成的团队[应用程序包](/concepts/build-and-test/apps-package.md)：

  > [!div class="checklist"]
  >
  > - 上的 manifest.js 
  > - 显示在公用或组织应用程序目录中的应用程序的[彩色图标](../resources/schema/manifest-schema.md#icons)
 > - "团队" 活动栏中显示的[大纲图标](../resources/schema/manifest-schema.md#icons)。

在安装应用程序时，团队客户端会分析清单文件以确定所需的信息，如应用程序的名称和服务所在的 URL。

1. 若要配置您的应用程序，请导航到**Microsoft 团队工具包**扩展窗口。
1. 选择 "**编辑应用程序包**" 以查看**应用程序详细信息**页。
1. 编辑应用程序详细信息页中的字段将更新作为应用程序包一部分最终交付的文件上的 manifest.js的内容。 [了解更多](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>打包应用程序

修改您的应用**程序详细信息**页面或更新**清单**，或应用程序的 **. publish**文件夹中的**env**文件将自动生成**Development.zip**文件。 您需要在同一文件夹中包含[两个图标](../concepts/build-and-test/apps-package.md#icons)。

## <a name="install-and-run-your-app-locally"></a>在本地安装和运行应用程序

从 "*解决方案配置*" 下拉菜单中，选择 "*部署*"。 按 " *ISS Express + 团队*" 按钮。 团队将启动，并且应用程序安装对话框应显示在团队客户端中。

## <a name="validate-your-app"></a>验证您的应用程序

通过 "**验证**" 页面，您可以在将应用程序提交到 AppSource 之前检查应用程序包。 只需上传清单包，验证工具就会检查应用程序是否符合所有与清单相关的测试用例。 对于每个失败的测试，说明提供的文档链接可帮助您修复错误。 对于难以自动化的测试，**初步清单**详细说明了最常见的失败测试事例的7，以及指向完整提交核对清单的链接。

## <a name="publish-your-app-to-teams"></a>将您的应用程序发布到团队

在您的项目主页上，您可以将应用程序上载到团队，将您的应用程序提交到贵组织中用户的公司自定义应用商店，或将您的应用程序提交到所有团队用户的应用程序源。 你的 IT 管理员将查看这些提交。 您可以返回到 "*发布*" 页面以查看您的提交状态，并了解您的应用程序是否已由 IT 管理员批准或拒绝。此外，您还可以将更新提交到您的应用程序或取消任何当前活动的提交。

> [!div class="nextstepaction"]
> [下一步：维护和支持发布的应用程序](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
