---
title: 入门 - 使用应用生成Teams应用SPFx
author: zhenyasav
description: 了解如何使用自定义选项卡生成SharePoint 框架
ms.author: zhenyasa
ms.date: 05/19/2021
ms.topic: quickstart
ms.openlocfilehash: 23df721a28225a8c453274e6e77efa8f756e84f3
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994369"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-sharepoint-framework-spfx"></a>使用应用生成并运行Microsoft Teams应用SharePoint 框架 (SPFx) 

在本教程中，你将在Microsoft Teams应用SharePoint 框架 (SPFx) 一个简单的个人应用。  (个人应用包括一组作用域为供个人使用的选项卡。) 在本教程中，你将了解 Teams 应用的结构、如何在本地运行应用以及如何将应用部署到 SharePoint。

## <a name="before-you-begin"></a>准备工作

通过安装[先决条件](prerequisites.md)确保您的开发环境已设置

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)

## <a name="get-organized"></a>有序整理

除了先决条件之外，您还需要是网站集SharePoint管理员。  你将在此位置部署要托管的应用。  如果你使用的是 M365 开发人员计划租户，请使用注册该计划时设置的管理员帐户。  

## <a name="create-your-project"></a>创建项目

使用 Teams 工具包创建你的第一个项目:

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. 打开 Visual Studio Code。
1. 通过选择边栏中的 Teams 图标，打开 Teams 工具包:

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code 边栏中的 Teams 图标。":::

1. 选择 **创建新项目**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. 选择 **创建新的 Teams 应用**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="&quot;创建新项目&quot;的向导启动":::

1. 在 **选择功能** 步骤中， **选项卡** 功能已被选中。  按 **确定**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities.png" alt-text="显示如何向新应用添加功能的屏幕截图。":::

1. 在"**前端托管类型"步骤中**，选择 **"SharePoint 框架 (SPFx) "。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="显示如何选择新应用的托管的屏幕截图。":::

1. 在"**框架"** 步骤中，选择 **"React"。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-which-framework.png" alt-text="选择框架":::

1. 当系统询问 **Web 部件名称时**，按 **Enter** 接受默认值。

1. 当系统询问 **Web 部件说明时**，按 **Enter** 接受默认值。

1. 当系统要求 **使用编程语言时**，按 **Enter** 接受默认值。

1. 选择工作区文件夹。  将在工作区文件夹中为正在创建的项目创建一个文件夹。

1. 为应用输入合适的名称，如 `helloworld`。  应用的名称只能包含字母数字字符。  按 **Enter** 以继续。

将在数秒钟内创建你的 Teams 应用。

# <a name="command-line"></a>[命令行](#tab/cli)

使用 `teamsfx` CLI 创建你的第一个项目。  从要创建项目文件夹的文件夹开始。

``` bash
teamsfx new
```

CLI 会提出一些问题来引导创建项目。  每个问题将告诉你该如何回答（例如，使用箭头键选择一个选项）。  如果已回答问题，请通过按 **Enter** 确认。

1. 选择 **"创建新的 Teams 应用**。
1. 选择" **选项卡** 功能。
1. 选择 **SharePoint 框架 (SPFx)** 前端托管。
1. 选择 **React** 框架"。
1. 按 **Enter** 作为 **Web 部件名称**。
1. 按 **Enter** 键查看 **Web 部件说明**。
1. 按 **Enter** 键 **以使用编程语言**。
1. 按 **Enter** 选择默认工作区文件夹。
1. 为应用输入合适的名称，如 `helloworld`。  应用的名称只能包含字母数字字符。

回答所有问题后，将创建项目。

---

- [详细了解如何针对 SharePoint 框架](/sharepoint/dev/spfx/sharepoint-framework-overview)

## <a name="take-a-tour-of-the-source-code"></a>浏览源代码

若要暂时跳过此部分，可以 [在本地运行应用](#run-your-app-locally)。

配置Teams Toolkit后，你具有组件来构建托管在项目Teams应用程序内的基本个人SharePoint 框架。  项目目录和文件显示在 Visual Studio 代码的资源管理器区域中。

:::image type="content" source="../assets/images/teams-toolkit-v2/app-project-files-spfx.png" alt-text="显示 Visual Studio Code 中个人应用的应用项目文件的屏幕截图。":::

工具包根据你在设置过程中添加的功能，自动在项目目录中创建标点文件夹。 Teams 工具包将保持其对于新目录中 `.fx` 的状态。  此目录中的其他项：

- 应用图标在 `color.png` 和 `outline.png`中存储为 PNG 文件。
- 发布到开发人员门户 for Teams的应用程序清单存储在 中 `manifest.source.json` 。
- 创建项目时选择的设置存储在 `settings.json`。

由于你选择了SPFx Web 部件项目，因此以下文件与 UI 相关：

- 该文件夹 `SPFx/src/webparts/{webpart}` 包含你的SPFx Web 部件。
- 该文件 `.vscode/launch.json` 描述了调试调色板中提供的调试配置。

有关 Web 部件SharePoint有关详细信息，Teams请参阅[SharePoint文档](/sharepoint/dev/spfx/build-for-teams-overview)。

## <a name="run-your-app-locally"></a>在本地运行应用

Teams Toolkit允许你在本地托管应用，并通过工作台SharePoint 框架[它](/sharepoint/dev/spfx/debug-in-vscode)。

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a>在 Visual Studio Code 本地生成和运行应用

若要在本地构建和运行应用，请执行：

1. 从Visual Studio Code，按 **F5。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-debug-local.png" alt-text="显示如何在本地工作台SPFx应用屏幕截图。":::

   > [!NOTE]
   > 首次运行该应用时，将下载所有依赖项并编译该应用。  生成完成后，浏览器窗口将自动打开并SharePoint工作台。  这可能需要 3-5 分钟才能完成。

   加载SharePoint工作台后。

   >[!NOTE]
   > 如有必要，工具包会提示你安装本地证书。 此证书允许 Teams 从 `https://localhost`。 出现下列对话框时，选择"是"：

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="显示如何安装 SSL 证书以便 Teams 从 localhost 加载应用程序提示的屏幕截图。":::

1. 按"添加 **Web 部件** " (+) 图标之一添加 Web 部件。

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart.png" alt-text="Screenshot showing the SPFx workbench running with the popup to add a webpart showing.":::

1. 从菜单中选择 Web 部件。

   :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-workbench-addpart2.png" alt-text="Screenshot showing the SPFx workbench running with the popup to add a webpart selection.":::

你的应用现在应该正在运行。  你可以执行正常的调试活动，就像在 Web 部件SPFx一样 (例如设置断点) 。

> [!TIP]
> 请尝试在 的 render 方法中放置断点 `SPFx/src/webparts/{webpart}/{webpart}.ts` 并重新加载浏览器窗口。 VS Code断点处停止。

## <a name="deploy-your-app-to-sharepoint"></a>将应用部署到SharePoint

确保SharePoint中存在应用程序目录。  如果其中一个不存在， [请创建一个](/sharepoint/use-app-catalog)。  可能需要 15 分钟才能完全创建应用程序目录。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. 打开 Visual Studio 代码。
1. 选择Teams Toolkit图标，从边栏Teams图标。
1. 选择 **"在云中预配"。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/provisioning-commands.png" alt-text="显示设置命令的屏幕截图":::

1. 可以通过查看右下角的对话框来监视进度。  几秒钟后，你将看到以下通知：

   :::image type="content" source="../assets/images/teams-toolkit-v2/provision-complete.png" alt-text="显示预配完成对话框的屏幕截图。":::

1. 预配完成后，选择"**部署到云"。**

1. 目前，自动化部署不可用。  将弹出一个对话框，提示你手动生成和部署。 按 **生成SharePoint包**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/build-sharepoint-package.png" alt-text="&quot;生成 Sharepoint 包&quot;对话框的屏幕截图":::

# <a name="command-line"></a>[命令行](#tab/cli)

在终端窗口中：

1. 运行 `teamsfx provision`。

   ``` bash
   teamsfx provision
   ```

   系统可能会提示你登录到 Azure 订阅。  如果需要，系统将提示你选择要用于 Azure 资源的 Azure 订阅。

   > [!NOTE]
   > 始终有一些用于托管应用的 Azure 资源。

1. 运行 `teamsfx deploy`。

   ``` bash
   teamsfx deploy
   ```

1. 当系统提示时，选择生成 **SharePoint包"。**

---

the SharePoint package is located `SPFx/sharepoint/solution` in within your project.  Upload程序包以SharePoint：

1. 登录到 M365 管理控制台，然后导航到SharePoint应用程序目录。

   - 打开 `https://admin.microsoft.com/AdminPortal/Home` 。
   - 在 **"管理中心**"下 **，SharePoint管理** 中心"。
   - 从 **边栏菜单中** 选择"更多功能"。
   - 按 **"应用"** 下的"**打开"。**
   - 选择 **"应用程序目录"。**

1. 选择 **"为用户分配SharePoint"。**

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-distribute-apps.png" alt-text="分配适用于SharePoint。":::

1. 选择 **"Upload"。**

1. 按 **"选择文件"。**

1. 找到 `{project}.sppkg` 位于项目内的 `SPFx/sharepoint/solution` 文件夹中的文件。  按 **"打开"。**

1. 按 **确定**。

1. 将自动SharePoint部署过程。  确保 **选中"使此解决方案对组织的所有网站** 都可用"，然后按"部署 **"。**

1. 选择" **文件"** 选项卡。

    :::image type="content" source="../assets/images/teams-toolkit-v2/spfx-appcatalog-filestab.png" alt-text="选择应用程序目录中的文件SharePoint选项卡。":::

1. 选择已部署的程序包，然后按"同步 **"Teams** 功能区中的"同步"。

    > [!Note]
    > 同步到Teams可能需要几分钟。  你将在浏览器的右侧看到一条消息，指示应用已成功同步到Teams。

打开Teams应用程序 (或登录 `https://teams.microsoft.com`) 。  按边栏上的三点，然后选择"所有 **应用"。**  该应用将放置在为 **组织类别构建的应用** 中。  你可以从该添加应用。

:::image type="content" source="../assets/images/teams-toolkit-v2/spfx-app-in-teams.png" alt-text="显示应用程序内应用的Teams":::

## <a name="see-also"></a>另请参阅

- [使用 React 创建 Teams 应用](first-app-react.md)
- [使用 Blazor 创建 Teams 应用](first-app-blazor.md)
- [创建邮件扩展](first-message-extension.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建对话机器人应用](first-app-bot.md)
