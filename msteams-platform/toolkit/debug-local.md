---
title: 在本地调试 Teams 应用
author: surbhigupta
description: 在本模块中，了解如何在 Teams 工具包中本地调试 Teams 应用以及 Teams 工具包的主要功能
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: 68999351232deb60015259840147d2a1ab55681a
ms.sourcegitcommit: ed7488415f814d0f60faa15ee8ec3d64ee336380
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/07/2022
ms.locfileid: "67616550"
---
# <a name="debug-your-microsoft-teams-app-locally"></a>在本地调试 Microsoft Teams 应用

Microsoft Teams 工具包可帮助你在本地调试和预览 Teams 应用。 在调试过程中，Teams 工具包会自动启动应用服务、启动调试器和旁加载 Teams 应用。 调试后，可以在 Teams Web 客户端本地预览 Teams 应用。 在调试应用之前，需要设置 Teams 工具包。

## <a name="set-up-your-teams-toolkit-for-debugging"></a>设置用于调试的 Teams 工具包

以下步骤可帮助你在启动调试过程之前设置 Teams 工具包：

# <a name="windows"></a>[Windows](#tab/Windows)

1. 从 **“运行和调** 试”下拉列表中选择“调 **试 (边缘**) 或 **调试 (Chrome)**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="浏览器选项":::

1. 选择 **“运行** > **开始调试” (F5)**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="开始调试":::

3. 选择“**登录**”到 Microsoft 365 帐户。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="登录":::

   > [!TIP]
   > 可以选择“**阅读更多**”，以了解Microsoft 365 开发人员计划。 将打开默认 Web 浏览器，以便使用凭据登录到 Microsoft 365 帐户。

4. 选择“**安装**”，以安装本地主机的开发证书。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="证书":::

   > [!TIP]
   > 可以选择“**了解**”有关开发证书的详细。

5. 显示在 **“安全警告**”对话框中选择 **“是**”：

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate.png" alt-text="证书颁发机构":::：

工具包根据所选内容启动新的 Edge 或 Chrome 浏览器实例，并打开网页以加载 Teams 客户端。  

# <a name="macos"></a>[macOS](#tab/macOS)

1. 从 **“运行和调** 试”▷下拉列表中选择 **“调试 Edge**”或“**调试 Chrome**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="浏览器列表":::

1. 选择“**开始调试(F5)**”或“**运行**”，以在调试模式下运行 Teams 应用。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="调试应用":::

3. 选择“**登录**”到 Microsoft 365 帐户。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="登录到 Microsoft 365 帐户":::

   > [!TIP]
   > 可以选择“**阅读更多**”，以了解Microsoft 365 开发人员计划。 打开默认 Web 浏览器，使用凭据登录到 Microsoft 365 帐户。

4. 选择“**安装**”，以安装本地主机的开发证书。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="证书":::

   > [!TIP]
   > 可以选择“**了解**”有关开发证书的详细。

5. 输入 **用户名** 和 **密码**，然后选择 **“更新设置**”。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/mac-settings.png" alt-text="mac 登录":::

Teams 工具包启动浏览器实例并打开网页以加载 Teams 客户端。

---

## <a name="debug-your-app"></a>调试应用

在初始设置过程之后，Teams 工具包将启动以下过程：

* [启动应用服务](#starts-app-services)
* [启动调试配置](#launches-debug-configurations)
* [旁加载 Teams 应用程序](#sideloads-the-teams-app)

### <a name="starts-app-services"></a>启动应用服务

运行在其中 `.vscode/tasks.json`定义的任务。

|  组件 |  任务名称  | Folder |
| --- | --- | --- |
|  Tab |  **启动前端** |  选项卡 |
|  自动程序或邮件扩展 |  **启动自动程序** |  自动程序 |
|  Azure Functions |  **启动后端** |  API |

下图在运行选项卡、机器人或消息扩展以及Azure Functions时，在Visual Studio Code的 **“输出**”和 **“终端**”选项卡中显示任务名称。

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/Terminal.png" alt-text="启动应用服务":::

### <a name="launches-debug-configurations"></a>启动调试配置

启动在其中定义 `.vscode/launch.json`的调试配置。

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/launch-debuggers.png" alt-text="启动调试程序":::

下表列出了具有选项卡、机器人或消息扩展应用的项目调试配置名称和类型，并Azure Functions：

|  组件 |  调试配置名称  | 调试配置类型 |
| --- | --- | --- |
|  Tab |  **连接到前端 (Edge)** 或  **连接到前端 (Chrome)**  |  pwa-msedge 或 pwa-chrome  |
|  自动程序或邮件扩展 |   **连接到自动程序** |  pwa 节点 |
| Azure Functions |   **连接到后端** |  pwa 节点 |

下表列出了使用机器人应用、Azure Functions和不使用选项卡应用的项目调试配置名称和类型：

|  组件 |  调试配置名称  | 调试配置类型  |
| --- | --- | --- |
|  自动程序或邮件扩展  | **启动自动程序 (Edge)** 或 **启动自动程序 (Chrome)**  |   pwa-msedge 或 pwa-chrome  |
|  自动程序或邮件扩展  |   **连接到自动程序** |  pwa 节点  |
|  Azure Functions |  **连接到后端** |  pwa 节点 |

### <a name="sideloads-the-teams-app"></a>旁加载 Teams 应用

**配置附加到前端** 或 **启动机器人** 会启动 Edge 或 Chrome 浏览器实例，以在网页中加载 Teams 客户端。 加载 Teams 客户端后，Teams 会旁加载由启动配置 [Microsoft Teams](https://teams.microsoft.com/l/app/>${localTeamsAppId}?installAppPackage=true&webjoin=true&${account-hint}) 中定义的旁加载 URL 控制的 Teams 应用。 当 Teams 客户端在 Web 浏览器中加载时，根据要求从下拉列表中选择 **“添加** ”或选择一个选项。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png" alt-text="添加本地调试" lightbox="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png":::

   你的应用已添加到 Teams！

## <a name="next"></a>Next

> [!div class="nextstepaction"]
> [调试后台进程](debug-background-process.md)

## <a name="see-also"></a>另请参阅

* [使用 Teams 工具包预配云资源](provision.md)
* [将功能添加到 Teams 应用](add-capability.md)
* [部署到云](deploy.md)
* [在 Teams 工具包中管理多个环境](TeamsFx-multi-env.md)
