---
title: 使用 Microsoft Teams 工具包和Visual Studio Code 生成应用
description: 开始使用Microsoft Teams Toolkit直接在Visual Studio Code内生成出色的自定义应用。
keywords: teams Visual Studio 代码工具包
ms.localizationpriority: medium
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 4672c6be9629d70c50885ecd0d9d034c943a337a
ms.sourcegitcommit: 5070746e736edb4ae77cd3efcb2ab8bb2e5819a0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/16/2022
ms.locfileid: "66123074"
---
# <a name="build-apps-with-the-teams-toolkit-and-visual-studio-code"></a>使用Teams Toolkit和Visual Studio Code生成应用

Visual Studio Code的Teams Toolkit可帮助开发人员创建和部署具有集成标识、云存储访问权限、Microsoft Graph 数据以及 Azure 中的其他服务的Teams应用，并Microsoft 365开发人员体验的“零配置”方法。

还可以将工具包与Visual Studio一起使用，也可以用作名为`teamsfx`) 的 CLI (。

## <a name="install-the-teams-toolkit-for-visual-studio-code"></a>安装Visual Studio Code的Teams Toolkit

1. 打开 Visual Studio Code。
1. 选择“扩展”视图 (**Ctrl+Shift+X** / ⌘⇧ **-X** 或 **视图>扩展)**。
1. 在搜索框中，输入 _Teams Toolkit_。
1. 在Teams Toolkit旁边的绿色安装按钮上选择。

还可以在Visual Studio Code市场中找到[Teams Toolkit](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

需要时，Visual Studio Code扩展将安装以下工具。 如果已安装，则改用已安装的版本。 如果使用包括 WSL) 在内的 Linux (，则必须先安装这些工具，然后才能使用：

- [Azure Functions Core Tools](/azure/azure-functions/functions-run-local)

    Azure Functions核心工具用于在本地调试运行期间在本地运行任何后端组件，包括在 Azure 中运行服务时所需的身份验证帮助程序。 它使用npm`devDependencies`安装在项目目录中。

- [.NET SDK](/dotnet/core/install/)

    .NET SDK 用于安装用于本地调试和Azure Functions应用部署的自定义绑定。 如果尚未全局安装 .NET 3.1 或更高版本的 SDK，则会安装可移植版本。

- [ngrok](https://ngrok.com/download)

    一些Teams应用功能 (会话机器人、消息传递扩展和传入 Webhook) 需要入站连接。  需要公开开发系统以通过隧道Teams。 对于仅包含选项卡的应用，不需要隧道。  此包安装在项目目录中， (使用npm `devDependencies`) 。

## <a name="use-the-teams-toolkit-for-visual-studio-code"></a>将Teams Toolkit用于Visual Studio Code

- [设置新项目](#set-up-a-new-teams-project)
- [配置应用程序](#configure-your-app)
- [在本地运行应用](#install-and-run-your-app-locally)
- [发布应用程序](#publish-your-app-to-teams)

## <a name="set-up-a-new-teams-project"></a>设置新的Teams项目

Teams Toolkit可以创建托管在 Azure 中的React应用，或SPFx托管在Microsoft 365 SharePoint环境中的 Web 部件。 若要创建要在 Azure 上托管的新React应用：

1. 打开 Visual Studio Code。
1. 通过选择边栏中的 Teams 图标，打开 Teams 工具包:

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code 边栏中的 Teams 图标。":::

1. 选择 **创建新项目**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. 选择 **创建新的 Teams 应用**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="&quot;创建新项目&quot;的向导启动":::

1. 在 **“选择功能** ”步骤中，已选择 **Tab** 功能。 还可以选择 **机器人** 和 **消息传递扩展**。  按 **确定**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="显示如何向新应用添加功能的屏幕截图。":::

1. 在 **前端托管类型** 步骤中， 选择 **Azure**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="显示如何选择新应用的托管的屏幕截图。":::

1. （可选）在 **云资源** 步骤中，选择应用程序使用的云资源。 可以选择 CRUD (创建、读取、更新和删除) 对SQL表或 API 的访问：

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="显示如何为新应用添加云资源的屏幕截图。":::

1. 在 **“编程语言** ”步骤中，可以选择 **JavaScript** 或 **TypeScript**：

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="显示如何选择编程语言的屏幕截图。":::

1. 选择工作区文件夹。 在要创建的项目的工作区文件夹中创建一个文件夹。

1. 为应用输入合适的名称，如 `helloworld`。 应用的名称只能包含字母数字字符。 按 **Enter** 以继续。

Teams应用会在几秒钟内创建。 基架应用包含用于处理使用Azure Active Directory的单一登录和访问 Microsoft Graph 的代码。 如果选择了 Azure 资源，则这些资源的代码也可用。

有关SPFx创建和发布过程的演练，请参阅[SPFx教程](../get-started/first-app-spfx.md)。

## <a name="configure-your-app"></a>配置应用程序

Teams应用的核心包含三个组件：

  1. Microsoft Teams客户端 (Web、桌面或移动) ，用户可在其中与应用交互。
  1. 响应Teams中显示的内容请求的服务器。 例如，HTML 选项卡内容或机器人自适应卡片。
  1. Teams应用包包含三个文件：

      > [!div class="checklist"]
      >
      > - manifest.json。
      > - 要在公共或组织应用目录中显示的应用的 [颜色图标](../resources/schema/manifest-schema.md#icons) 。
      > - 要在Teams活动栏上显示[的大纲图标](../resources/schema/manifest-schema.md#icons)。

清单和图标在上传到Teams之前存储在`.fx`项目的文件夹中。 安装应用时，Teams客户端会分析清单文件，以确定所需的信息，例如应用的名称和服务所在的 URL。

1. 若要配置应用，请导航到 **Visual Studio Code中的“Teams Toolkit**”选项卡。
1. 在 **Project** 部分中选择 **清单编辑器**。

编辑“应用详细信息”页中的字段会更新最终作为应用包的一部分寄送的 manifest.json 文件的内容。

## <a name="install-and-run-your-app-locally"></a>在本地安装和运行应用

若要在本地构建并运行应用程序:

1. 在 Visual Studio Code 中，按 **F5** 以在调试模式下运行应用程序。

   > 首次运行该应用时，将下载所有依赖项并编译该应用。  编译完成后，将自动打开浏览器窗口。 这可能需要 3-5 分钟才能完成。

   如果需要，工具包会提示你安装本地证书。 此证书允许 Teams 从 `https://localhost`。 出现下列对话框时，选择"是"：

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="显示如何安装 SSL 证书以便 Teams 从 localhost 加载应用程序提示的屏幕截图。":::

1. Web 浏览器开始运行应用程序。 如果系统提示打开 Microsoft Teams，请选择"取消"以留在浏览器中。 可能还会提示你在其他时间切换到Teams应用程序。 发生这种情况时选择 Web 应用。

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="显示启动后如何选择 Teams 的 Web 版本的屏幕截图":::

1. 系统可能会提示你登录。 如果是，请使用Microsoft 365帐户登录。
1. 系统提示将应用安装到 Teams 时，按 **添加**。

后端和前端都连接到Visual Studio Code调试器中。 这允许在代码中的任何位置设置断点并检查状态。  还可以使用任何前端调试工具 (，例如浏览器中的React开发人员工具) 。  有关Visual Studio Code中调试的详细信息，请查看[文档](https://code.visualstudio.com/Docs/editor/debugging)。

## <a name="publish-your-app-to-teams"></a>将应用发布到 Teams

必须先将应用发布到开发人员门户以供其他人使用，然后才能将其发布到开发人员门户以供Teams。

1. 若要发布应用，请导航到 **Visual Studio Code中的“Teams Toolkit**”选项卡。
1. 在Project部分中选择 **“发布到****Teams**”。

如果使用 Azure 托管，则必须已预配并部署到云。 有关SPFx发布过程的演练，请参阅[SPFx教程](../get-started/first-app-spfx.md)。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [维护和支持已发布的应用](../concepts/deploy-and-publish/appsource/post-publish/overview.md)

## <a name="see-also"></a>另请参阅

- [使用 Teams 工具包和 Visual Studio 构建应用](~/toolkit/visual-studio-overview.md)
- [使用 Microsoft Teams JavaScript 客户端 SDK 生成选项卡和其他托管体验](~/tabs/how-to/using-teams-client-sdk.md)
