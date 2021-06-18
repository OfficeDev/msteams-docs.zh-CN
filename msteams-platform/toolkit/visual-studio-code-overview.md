---
title: 使用 Microsoft Teams Toolkit 和 Visual Studio 代码生成应用
description: 开始使用 Microsoft Teams Visual Studio直接在 Visual Studio Code 中生成出色的自定义Toolkit
keywords: teams visual studio code toolkit
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: b2cfab5cb2ea2d727608b6ea3bbfec3271b2b039
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994138"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>使用 Teams 应用和Toolkit Visual Studio生成应用

Teams Toolkit for Visual Studio Code 通过针对开发人员体验的"零配置"方法帮助开发人员创建和部署具有集成标识、访问云存储、Microsoft Graph 数据以及 Azure 和 M365 中其他服务的 Teams 应用。  

还可以将工具包与 Visual Studio一 (CLI `teamsfx`) 。

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a>安装 Teams Toolkit for Visual Studio Code

1. 打开 Visual Studio 代码。
1. Select the Extensions view (**Ctrl+Shift+X**  /  **⌘⇧-X** or **View > Extensions**) .
1. 在搜索框中，输入 _Teams Toolkit_。
1. 在 Teams 应用旁的绿色安装按钮上选择Toolkit。

还可以在"Toolkit代码Visual Studio [上找到 Teams 服务](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

以下工具由代码扩展Visual Studio安装。 如果已安装，则改为使用已安装的版本。 如果使用 Linux (WSL) ，则必须先安装这些工具，然后才能使用：

- [Azure 函数核心工具](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools 用于在本地调试运行期间在本地运行任何后端组件，包括在 Azure 中运行服务时所需的身份验证帮助程序。 它使用 npm 安装在项目目录中 `devDependencies` 。

- [.NET SDK](/dotnet/core/install/)

    .NET SDK 用于安装用于本地调试和 Azure Functions 应用部署的自定义绑定。 如果尚未全局安装 .NET 3.1 或更高版本 SDK，则安装可移植版本。

- [ngrok](https://ngrok.com/download)

    一些 Teams 应用 (对话机器人、消息传递扩展和传入 webhook) 需要入站连接。  你需要通过隧道向 Teams 公开你的开发系统。 仅包含选项卡的应用不需要隧道。  此包安装在项目目录中， (npm `devDependencies`) 。

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a>使用 Teams Toolkit for Visual Studio Code

- [设置新项目](#set-up-a-new-teams-project)
- [配置应用程序](#configure-your-app)
- [在本地运行应用](#install-and-run-your-app-locally)
- [发布应用程序](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>设置新的 Teams 项目

Teams Toolkit可以创建在托管在 M365 SharePoint 环境的 Azure 或 SPFx Web 部件中的 React 应用。 若要创建在 Azure 上托管的新 React 应用：

1. 打开 Visual Studio Code。
1. 通过选择边栏中的 Teams 图标，打开 Teams 工具包:

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code 边栏中的 Teams 图标。":::

1. 选择 **创建新项目**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. 选择 **创建新的 Teams 应用**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="&quot;创建新项目&quot;的向导启动":::

1. 在 **"选择功能"** 步骤中， **已** 选择 Tab 功能。 还可以选择自动程序 **与****消息传递扩展**。  按 **确定**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="显示如何向新应用添加功能的屏幕截图。":::

1. 在 **前端托管类型** 步骤中， 选择 **Azure**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="显示如何选择新应用的托管的屏幕截图。":::

1. （可选）在"云 **资源"** 步骤中，选择应用程序使用的云资源。 可以选择 CRUD (、读取、更新和删除) 表或 API SQL访问：

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="显示如何为新应用添加云资源的屏幕截图。":::

1. 在 **"编程语言"** 步骤中，可以选择 **"JavaScript"或****"TypeScript"：**

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="显示如何选择编程语言的屏幕截图。":::

1. 选择工作区文件夹。 在工作区文件夹中为要创建的项目创建文件夹。

1. 为应用输入合适的名称，如 `helloworld`。 应用的名称只能包含字母数字字符。  按 **Enter** 以继续。

Teams 应用在几秒钟内创建。 基架应用包含用于处理 Azure Active Directory 单一登录和 Microsoft Graph 访问的代码。  如果你选择了 Azure 资源，则这些资源的代码也可用。

有关 SPFx 创建和发布过程的演练，请参阅 [SPFx 教程](../get-started/first-app-spfx.md)。

## <a name="configure-your-app"></a>配置应用程序

Teams 应用的核心包括三个组件：

  1. Microsoft Teams 客户端 (Web、桌面或移动) 用户与你的应用进行交互。
  1. 响应对在 Teams 中显示的内容的请求的服务器。 例如，HTML 选项卡内容或自动程序自适应卡片。
  1. Teams 应用包包含三个文件：

      > [!div class="checklist"]
      >
      > - 打开manifest.js。
      > - 要 [显示在](../resources/schema/manifest-schema.md#icons) 公共或组织应用程序目录中的应用的颜色图标。
      > - 显示在 [Teams](../resources/schema/manifest-schema.md#icons) 活动栏上的大纲图标。

清单和图标在上传到 Teams 之前 `.fx` 存储在项目的文件夹中。 安装应用后，Teams 客户端将分析清单文件以确定所需信息，如应用名称和服务所在的 URL。

1. 若要配置你的应用，请导航到"Toolkit代码 **"Visual Studio"** 选项卡。
1. 选择 **"项目"** 部分中的" **清单编辑器** "。

编辑"应用详细信息"页中的字段将更新manifest.js作为应用包的一部分交付的 on 文件的内容。

## <a name="install-and-run-your-app-locally"></a>在本地安装和运行应用

若要在本地构建并运行应用程序:

1. 在 Visual Studio Code 中，按 **F5** 以在调试模式下运行应用程序。

   > 首次运行该应用时，将下载所有依赖项并编译该应用。  编译完成后，将自动打开浏览器窗口。  这可能需要 3-5 分钟才能完成。

   工具包会提示你安装本地证书（如果需要）。 此证书允许 Teams 从 `https://localhost`。 出现下列对话框时，选择"是"：

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="显示如何安装 SSL 证书以便 Teams 从 localhost 加载应用程序提示的屏幕截图。":::

1. Web 浏览器开始运行应用程序。 如果系统提示打开 Microsoft Teams，请选择"取消"以留在浏览器中。 此外，系统还会提示你在其他时间切换到 Teams 应用程序。 发生这种情况时，选择 Web 应用。

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="显示启动后如何选择 Teams 的 Web 版本的屏幕截图":::

1. 系统可能会提示你登录。 如果是这样，则使用你的 M365 帐户登录。
1. 系统提示将应用安装到 Teams 时，按 **添加**。

后端和前端都挂钩到 Visual Studio 代码调试器。  这允许你在代码中的任意位置设置断点并检查状态。  还可以在浏览器中使用任何前端调试 (如 React 开发人员) 工具。  有关在代码中调试Visual Studio，请参阅 [文档](https://code.visualstudio.com/Docs/editor/debugging)。

## <a name="publish-your-app-to-teams"></a>将应用发布到 Teams

必须先将应用发布到 Teams 开发人员门户，然后才能供其他人使用。

1. 若要发布你的应用，请导航到"Toolkit代码 **"Visual Studio"** 选项卡。
1. 选择 **"发布Teams"****部分中的**"Project"。

如果使用 Azure 托管，则必须已预配并部署到云。 有关发布过程SPFx，请参阅 SPFx[教程](../get-started/first-app-spfx.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [维护和支持已发布的应用](../concepts/deploy-and-publish/appsource/post-publish/overview.md)
