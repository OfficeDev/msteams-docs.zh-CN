---
title: 使用 Microsoft 团队工具包和 Visual Studio Code 生成应用程序
description: 开始在 Visual Studio Code 中使用 Microsoft 团队工具包直接构建强大的自定义应用程序
keywords: 团队 visual studio code 工具包
ms.date: 06/30/2020
ms.openlocfilehash: 17f21d1656b32074318030b9df9e643200f58f80
ms.sourcegitcommit: ecf7ca8e77e77fe3f4cad1b13e3d31a825155555
ms.translationtype: Auto
ms.contentlocale: zh-CN
ms.lasthandoff: 07/07/2020
ms.locfileid: "45054250"
---
# <a name="build-apps-with-the-microsoft-teams-toolkit-and-visual-studio-code"></a>使用 Microsoft 团队工具包和 Visual Studio Code 生成应用程序

Microsoft 团队工具包使你能够在 Visual Studio Code 环境中直接创建自定义团队应用。 该工具包将引导您完成整个过程，并提供生成、调试和启动团队应用程序所需的所有内容。

## <a name="installing-the-teams-toolkit"></a>安装团队工具包

Visual studio Code 的 Microsoft 团队工具包可从[Visual Studio Marketplace](https://aka.ms/teams-toolkit)下载，也可直接作为 Visual studio code 中的扩展。

> [!TIP]
> 安装完成后，应在 Visual Studio Code 活动栏中看到 "团队" 工具包。 如果不是，请在活动栏中右键单击，然后选择 " **Microsoft 团队**" 以固定该工具包以方便访问。

## <a name="using-the-toolkit"></a>使用工具包

- [设置新项目](#set-up-a-new-teams-project)
- [导入现有项目](#import-an-existing-teams-app-project)
- [配置应用程序](#configure-your-app)
- [打包应用程序](#package-your-app)
- [在团队中运行应用程序](#run-your-app-in-teams)
- [验证您的应用程序](#validate-your-app)
- [发布应用程序](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>设置新的团队项目

1. 在本地环境中为项目创建一个工作区/文件夹。
1. 在 Visual Studio Code 中，选择 "团队" 图标 ![Teams 图标](../assets/icons/favicon-16x16.png) 从窗口左侧的活动栏中进行。
1. 从 "命令" 菜单中选择 **"打开 Microsoft 团队工具包"** 。
1. 从 "命令" 菜单中选择 "**创建新的团队应用**"。
1. 出现提示时，输入工作区的名称。 这将用作项目将驻留的文件夹的名称和应用程序的默认名称。
1. 按**enter** ，你将进入 "**添加功能**" 屏幕，为新应用配置属性。
1. 选择 "**完成**" 按钮完成配置过程。

## <a name="import-an-existing-teams-app-project"></a>导入现有团队应用程序项目

1. 在 Visual Studio Code 中，选择 "团队" 图标 ![Teams 图标](../assets/icons/favicon-16x16.png) 从窗口左侧的活动栏中进行。
1. 从 "命令" 菜单中选择 "**导入应用程序包**"。
1. 选择现有[团队应用程序包](../concepts/build-and-test/apps-package.md)zip 文件。
1. 选择 "**选择发布包**" 按钮。 此时，工具包的 "配置" 选项卡应包含您的应用程序的详细信息。
1. 在 visual studio code 中，选择 "**文件**" "  ->  **将文件夹添加到工作区**"，将源代码目录添加到 Visual studio code Workspace。

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

1. 若要配置您的应用程序，请导航到 Visual Studio Code 中的 " **Microsoft 团队工具包**" 选项卡。
1. 选择 "**编辑应用程序包**" 以查看**应用程序详细信息**页。
1. 编辑应用程序详细信息页中的字段将更新作为应用程序包一部分最终交付的文件上的 manifest.js的内容。 [了解更多](https://aka.ms/teams-toolkit-manifest)

## <a name="package-your-app"></a>打包应用程序

修改您的应用**程序详细信息**页面或更新**清单**，或应用程序的 **. publish**文件夹中的**env**文件将自动生成**Development.zip**文件。 您需要在同一文件夹中包含[两个图标](../concepts/build-and-test/apps-package.md#icons)。

## <a name="install-and-run-your-app-locally"></a>在本地安装和运行应用程序

有关打包和测试应用程序的详细说明，请参阅在项目主页中*构建和运行*内容。 通常情况下，您需要安装应用程序的服务器，使其运行，然后设置隧道解决方案，以便团队可以访问本地主机中运行的内容。

## <a name="add-a-trusted-certificate-for-localhost"></a>为本地主机添加受信任证书

如果您希望使用 https 在 localhost 上调试基于选项卡的应用程序，则需要将 localhost 的证书添加到 `Trusted Root Certification Authorities` 目录中。 每台计算机只需完成一次此步骤。</br></br>

**创建并安装受信任的证书：**
<details>
  <summary>在此处展开</summary>

* 构建并运行应用程序
  * 按照项目自述文件的 "**生成和运行**" 部分中的 instuctions 操作，以便从提供服务 https://localhost:3000/tab 。通常情况下，这将涉及执行， `npm install` 然后`npm start`
  * https://localhost:3000/tab从 Google Chrome 导航到

* 获取 SSL 证书：
  * 打开 "Chrome 开发人员工具" 窗口（ `ctrl + shift + i`  /  `cmd + option + i` ）。
  * 在 `Security` 选项卡上单击
  * 单击 "启用"， `View certificate` 可以选择下载证书，方法是在 OS X 中将其拖放到桌面，或者单击 `Details` Windows 中的选项卡，然后单击`Copy to File…`
  * 将该文件命名为 <*任何内容*> .cer，并将其保存到不需要管理员同意执行写入操作的文件夹中。
  
* 在**Windows**上安装证书
  * 选择 `DER encoded binary X.509 (.CER)` 选项（第一个选项）并保存它。
  * 双击证书并安装它。
  * 选取`Local Machine`
  * 选定`Place all certificates in the following store`
  * 选取`Trusted Root Certification Authorities`
  * 确认安装
  
* 安装证书**MAC OS X**
  * 在 OS X 上，打开密钥链 Access 实用工具，并 `System` 从左侧的菜单中选择。 单击锁定图标可启用更改。
  * 单击靠近底部的加号按钮以添加新证书，然后选择 `localhost.cer` 您拖到桌面的文件。 `Always Trust`在出现的对话框中单击。
  * 将证书添加到系统密钥链后，双击证书并展开 `Trust` 证书详细信息部分。 `Always Trust`为每个选项选择。

> [!IMPORTANT]
> 如果收到安全证书警告，请导航到 https://localhost:3000/tab 。如果网站仍不受信任，请重新启动您的计算机，并应接受为受信任的本地主机。
</details>

## <a name="run-your-app-in-teams"></a>在团队中运行应用程序
- 先决条件：
  - [启用团队开发人员预览模式](https://aka.ms/teams-toolkit-enable-devpreview)

1. 导航到 Visual Studio "代码" 窗口左侧的 "活动" 栏。
1. 选择 "**运行**" 图标以显示 "**运行" 和 "调试**" 视图。
1. 您还可以使用键盘快捷方式 `Ctrl+Shift+D` 。

## <a name="validate-your-app"></a>验证您的应用程序

通过 "**验证**" 页面，您可以在将应用程序提交到 AppSource 之前检查应用程序包。 只需上传清单包，验证工具就会检查应用程序是否符合所有与清单相关的测试用例。 对于每个失败的测试，说明提供的文档链接可帮助您修复错误。 对于难以自动化的测试，**初步清单**详细说明了最常见的失败测试事例的7，以及指向完整提交核对清单的链接。

## <a name="publish-your-app-to-teams"></a>将您的应用程序发布到团队

在您的项目主页上，您可以将应用程序上载到团队，将您的应用程序提交到贵组织中用户的公司自定义应用商店，或将您的应用程序提交到所有团队用户的应用程序源。 你的 IT 管理员将查看这些提交。 您可以返回到 "*发布*" 页面以查看您的提交状态，并了解您的应用程序是否已由 IT 管理员批准或拒绝。此外，您还可以将更新提交到您的应用程序或取消任何当前活动的提交。

> [!div class="nextstepaction"]
> [下一步：维护和支持发布的应用程序](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
