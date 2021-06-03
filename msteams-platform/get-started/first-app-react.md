---
title: 开始 - 使用回车功能生成第一个 Teams 应用
author: adrianhall
description: 快速创建显示"Hello，World！"的 Microsoft Teams 应用。 使用 Microsoft Teams 工具包并响应的消息。
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.openlocfilehash: 8c6a957dc01cfaac0f8463166a6647d6b18babed
ms.sourcegitcommit: 33a43c61f27ae750776616b2cf90159455d8ba6c
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/02/2021
ms.locfileid: "52721834"
---
# <a name="build-and-run-your-first-microsoft-teams-app-with-react"></a>使用 React 构建和运行第一个 Microsoft Teams 应用

在本教程中，将在回车应用中创建新的 Microsoft Teams 应用，该应用实施简单的个人应用，从 Microsoft Graph 提取信息。 （ *个人应用* 包括一组适用于个人使用的选项卡。）在本教程中，你将了解 Teams 应用的结构、在本地运行应用以及如何将应用部署到 Azure。

构建的应用将显示当前用户的基本用户信息。  授予权限后，应用会作为当前用户连接到 Microsoft Graph 以获取完整配置文件。

## <a name="before-you-begin"></a>准备工作

通过安装[先决条件](prerequisites.md)确保您的开发环境已设置

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)

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

1. 在 **前端托管类型** 步骤中， 选择 **Azure**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-hosting.png" alt-text="显示如何选择新应用的托管的屏幕截图。":::

1. 在 **云资源** 步骤中， 选择 **确定**。  本教程不需要其他云资源。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-cloud-resources.png" alt-text="显示如何为新应用添加云资源的屏幕截图。":::

1. 在" **编程语言** 步骤中， 选择 **JavaScript**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="显示如何选择编程语言的屏幕截图。":::

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
1. 选择 **Azure** 前端托管。
1. 请勿选择任何云资源。
1. 选择 **JavaScript** 作为编程语言。
1. 按 **Enter** 选择默认工作区文件夹。
1. 为应用输入合适的名称，如 `helloworld`。  应用的名称只能包含字母数字字符。

回答所有问题后，将创建项目。

---

## <a name="take-a-tour-of-the-source-code"></a>浏览源代码

若要暂时跳过此部分， 你可以[运行本地应用](#run-your-app-locally)。

在 Teams 工具包配置你的项目后，你只需这些组件就可以使用这些组件为 Teams 构建基本的个人应用。 项目目录和文件显示在 Visual Studio 代码的资源管理器区域中。

:::image type="content" source="../assets/images/teams-toolkit-v2/react-app-project.png" alt-text="显示 Visual Studio Code 中个人应用的应用项目文件的屏幕截图。":::

工具包根据你在设置过程中添加的功能，自动在项目目录中创建标点文件夹。 Teams 工具包将保持其对于新目录中 `.fx` 的状态。  此目录中的其他项：

- 应用图标在 `color.png` 和 `outline.png`中存储为 PNG 文件。
- 发布到 Developer Portal for Teams 的应用清单存储在 `manifest.source.json`。
- 创建项目时选择的设置存储在 `settings.json`。

由于在设置过程中选择了选项卡功能，因此 Teams 工具包会为网站目录中的基本选项卡 `tabs` 代码。 此目录中有几个重要文件：

- `tabs/src/index.jsx` 是前端应用的入口点，其中主应用程序组件 `App` 呈现为 `ReactDOM.render()`。
- `tabs/src/components/App.jsx` 处理应用中的 URL 路由。 它调用了 [JavaScript 客户端 SDK](../tabs/how-to/using-teams-client-sdk.md) 应用和团队之间建立通信。
- `tabs/src/components/Tab.jsx` 包含用于实现应用 UI 的代码。
- `tabs/src/components/TabConfig.jsx` 包含用于实施配置应用的 UI 的代码。

Teams 运行时需要几个选项卡，包括隐私声明、使用条款和配置选项卡。  隐私声明和使用条款的代码位于同一目录中。

添加云功能时，会向项目添加其他目录。  最为明显的是， `api` 目录将代码存储到所编写的任何 Azure 函数中。

## <a name="run-your-app-locally"></a>在本地运行应用

使用 Teams 工具包，你可以在本地运行应用。  这包含几个部分，是提供 Teams 所需的正确基础结构所必需的：

- 应用程序已注册 Azure Active Directory。  此应用程序具有与从加载应用的位置及其访问的任何后端资源相关联的权限。
- 托管 Web API 以辅助身份验证任务，作为应用和 Azure Active Directory 之间的代理。  这由 Azure 函数核心工具运行。  可以在 URL 位置访问 `https://localhost:5000`。
- 位于应用程序前端的 HTML、CSS 和 JavaScript 资源托管在本地服务中。 可通过访问文件 `https://localhost:3000`。
- 生成应用清单，存在于 Teams 开发人员门户中。  Teams 使用应用清单告诉已连接客户端从何处加载应用。

完成后，可在 Teams 客户端中加载该应用。  我们使用 Teams Web 客户端，以便可以在标准 Web 开发环境中查看 HTML、CSS 和 JavaScript 代码。

### <a name="build-and-run-your-app-locally-in-visual-studio-code"></a>在 Visual Studio Code 本地生成和运行应用

若要在本地构建和运行应用，请执行：

1. 在 Visual Studio Code 中，按 **F5** 以在调试模式下运行应用程序。

   > 首次运行该应用时，将下载所有依赖项并编译该应用。  编译完成后，将自动打开浏览器窗口。  这可能需要 3-5 分钟才能完成。

   如有必要，工具包会提示你安装本地证书。 此证书允许 Teams 从 `https://localhost`。 出现下列对话框时，选择"是"：

   :::image type="content" source="../assets/images/teams-toolkit-v2/ssl-prompt.png" alt-text="显示如何安装 SSL 证书以便 Teams 从 localhost 加载应用程序提示的屏幕截图。":::

1. Web 浏览器开始运行该应用。 如果系统提示打开Teams，请选择 **"取消**"以保留在浏览器中。 系统有时还可能会提示你切换到Teams桌面;选择Teams Web 应用。

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="显示启动后如何选择 Teams 的 Web 版本的屏幕截图":::

1. 系统可能会提示你登录。  如果是这样，则使用你的 M365 帐户登录。
1. 系统提示将应用安装到 Teams 时，按 **添加**。

此时将显示应用：

:::image type="content" source="../assets/images/teams-toolkit-v2/react-finished-app.png" alt-text="已完成应用的屏幕截图":::

你可以像调试任何其他 Web 应用程序一样执行正常调试活动（例如设置断点）。 该应用支持热重新加载。  如果更改了项目内的任何文件，将重新加载页面。

<!-- markdownlint-disable MD033 -->
<details>
<summary>在调试器中本地运行应用时，会发生什么情况。</summary>

按 F5 时，Teams 工具包:

1. 使用 Azure Active Directory 注册应用程序。
1. *已并行* Teams 中的应用。
1. 使用 Azure 函数核心工具中心 [本地运行的应用程序后端](/azure/azure-functions/functions-run-local?#start)。
1. 启动应用程序本地托管的前端。
1. 在 Web 浏览器中启动 Microsoft Teams，命令命令 Teams 从 `https://localhost:3000/tab` （URL 在应用程序清单中注册） 并排加载应用程序。

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary>了解如何在本地运行应用时解决常见问题。</summary>

若要在 Teams 中成功运行应用，必须具有允许应用旁加载的 Teams 帐户。 有关打开帐户详细信息，请参阅 [先决条件](prerequisites.md#enable-sideloading)。

</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->
<details>
<summary>了解将应用部署到 Azure 时会发生的情况</summary>

部署之前，应用程序已在本地运行:

1. 后端使用 _Azure Functions Core Tools_ 运行。
1. 应用程序 HTTP 终结点 (Microsoft Teams 在此加载应用程序) 在本地运行。

部署涉及预配活动 Azure 订阅上的资源，以及将应用程序后端和前端代码部署（上传）到 Azure。

1. 后端（如果已配置）使用多种 Azure 服务，包括 Azure 应用服务和 Azure 存储。
1. 将前端应用程序部署到配置用于静态 Web 托管的 Azure 存储帐户。

</details>

## <a name="next-steps"></a>后续步骤

了解创建 Teams 应用的其他方法：

- [使用 Blazor 创建 Teams 应用](first-app-blazor.md)
- [创建 Teams 应用作为 SharePoint Web 部件](first-app-spfx.md) （不需要 Azure）
- [创建对话机器人应用](first-app-bot.md)
- [创建邮件扩展](first-message-extension.md)
