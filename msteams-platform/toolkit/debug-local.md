---
title: 调试 Teams 应用
description: 在 Teams 工具包中本地调试 Teams 应用
ms.author: surbhigupta
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: 04c88e840ba1edbeb657428bb76ecea86acf895a
ms.sourcegitcommit: eeaa8cbb10b9dfa97e9c8e169e9940ddfe683a7b
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/27/2022
ms.locfileid: "65756630"
---
# <a name="debug-your-teams-app-locally"></a>在本地调试 Teams 应用

Teams 工具包有助于本地调试和预览 Teams 应用。 调试是检查、检测和更正问题或错误，以确保程序正常运行的过程。 Visual Studio Code 可以调试选项卡、自动程序、邮件扩展和 Azure 函数。 Teams 工具包支持以下调试功能：

* [开始调试](#start-debugging)
* [多目标调试](#multi-target-debugging)
* [切换断点](#toggle-breakpoints)
* [热重新加载](#hot-reload)
* [停止调试](#stop-debugging)  


在调试过程中，Teams 工具包自动启动应用服务、调试程序，以及旁加载 Teams 应用。 调试后，Teams 应用可在 Teams Web 客户端本地预览。 还可以自定义调试设置，使用自动程序终结点、开发证书或调试部分组件来加载配置应用。

## <a name="prerequisite"></a>先决条件

安装 [最新版本的 Teams 工具包](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

## <a name="key-features-of-teams-toolkit"></a>Teams 工具包的主要功能

#### <a name="start-debugging"></a>开始调试

可以执行单个操作，选择 **F5** 开始调试。 Teams 工具包开始检查先决条件、注册Azure Active Directory 应用、注册 Teams 应用、注册机器人、启动服务和启动浏览器。

#### <a name="multi-target-debugging"></a>多目标调试

Teams 工具包利用多目标调试功能同时调试选项卡、自动程序、邮件扩展和 Azure 函数。

#### <a name="toggle-breakpoints"></a>切换断点

可以在选项卡、自动程序、邮件扩展和 Azure 函数的源代码上切换断点。 在 Web 浏览器中与 Teams 应用交互时，将执行断点。 下图显示了切换断点：

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/toggle-points.png" alt-text="切换断点":::

#### <a name="hot-reload"></a>热重新加载

调试 Teams 应用时，可以同时更新和保存选项卡、自动程序、邮件扩展和 Azure 函数的源代码。 应用将重新加载，调试器将重新连接到编程语言。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hot-reload.png" alt-text="源代码的热重新加载":::

#### <a name="stop-debugging"></a>停止调试

完成本地调试后，可以选择“**停止**”或从浮动调试工具栏“**断开连接**”，以停止所有调试会话并终止任务。下图显示了停止调试操作：

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/stop-debug.png" alt-text="停止调试":::

## <a name="debug-your-teams-app-locally"></a>在本地调试 Teams 应用

#### <a name="1-set-up-your-teams-toolkit"></a>1.设置 Teams 工具包

使用 Teams 工具包创建新应用后，完成以下步骤来调试应用：

<br>

<details>
<summary><b>Windows</b></summary>

1. 在活动栏的“**运行和调试**”中，选择“**调试 Edge**”或“**调试 Chrome**”

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="浏览器选项" border="false":::

1. 选择“**开始调试 (F5)**”或“**运行**”，以在调试模式下运行 Teams 应用

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="开始调试" border="false":::

3. 选择“**登录**”到 Microsoft 365 帐户

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="登录" border="true":::


   > [!TIP]
   > 可以选择“**阅读更多**”，以了解Microsoft 365 开发人员计划。 打开默认 Web 浏览器，使用凭据登录到 Microsoft 365 帐户。

4. 选择“**安装**”，以安装本地主机的开发证书

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="证书" border="true":::

   > [!TIP]
   > 可以选择“**了解**”有关开发证书的详细。

5. 如果出现以下对话框，请选择“**是**”：

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate.png" alt-text="证书颁发机构" border="true":::：

工具包根据所选内容启动新的 Edge 或 Chrome 浏览器实例，并打开网页以加载 Teams 客户端。  

</details>

<details>
<summary><b>macOS</b></summary>

1. 在活动栏的“**运行和调试**”中，选择“**调试 Edge**”或“**调试 Chrome**”。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/debug-run.png" alt-text="浏览器列表" border="false":::

1. 选择“**开始调试(F5)**”或“**运行**”，以在调试模式下运行 Teams 应用。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/start-debugging.png" alt-text="调试应用" border="false":::

3. 选择“**登录**”到 Microsoft 365 帐户。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/microsoft365-signin.png" alt-text="登录到 Microsoft 365 帐户" border="true":::

   > [!TIP]
   > 可以选择“**阅读更多**”，以了解Microsoft 365 开发人员计划。 打开默认 Web 浏览器，使用凭据登录到 Microsoft 365 帐户。

4. 选择“**安装**”，以安装本地主机的开发证书。

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/install-certificate.png" alt-text="证书" border="true":::

   > [!TIP]
   > 可以选择“**了解**”有关开发证书的详细。

5. 输入“**用户名**”和“**密码**”，然后在以下对话框中选择“**更新设置**”：

    :::image type="content" source="../assets/images/teams-toolkit-v2/debug/mac-settings.png" alt-text="mac 登录" border="true":::

工具包根据所选内容启动新的 Edge 或 Chrome 浏览器实例，并打开网页以加载 Teams 客户端。

</details>

#### <a name="2-debug-your-app"></a>2. 调试应用

初始设置过程完成后，Teams 工具包将启动以下进程：

a. [启动应用服务](#starts-app-services) </br>
b. [启动调试程序](#launches-debuggers)   </br>c.[旁加载 Teams 应用](#sideloads-the-teams-app)
        
#### <a name="starts-app-services"></a>启动应用服务

运行 `.vscode/tasks.json` 中定义的任务，如下所示：

|  组件 |  任务名称  | Folder |
| --- | --- | --- |
|  Tab |  **启动前端** |  选项卡 |
|  自动程序或邮件扩展 |  **启动自动程序** |  自动程序 |
|  Azure Functions |  **启动后端** |  API |

下图显示了运行选项卡、自动程序或邮件扩展和 Azure 函数时，Visual Studio Code 上的“**输出****终端**”选项卡上的任务名称。

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/Terminal.png" alt-text="启动应用服务":::

#### <a name="launches-debuggers"></a>启动调试程序

启动在 `.vscode/launch.json` 中定义的调试配置，如下所示：

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/launch-debuggers.png" alt-text="启动调试程序":::

下表列出了具有选项卡应用和自动程序应用项目的调试配置名称和类型：

|  组件 |  调试配置名称  | 调试配置类型 |
| --- | --- | --- |
|  Tab |  **连接到前端 (Edge)** 或  **连接到前端 (Chrome)**  |  pwa-msedge 或 pwa-chrome  |
|  自动程序或邮件扩展 |   **连接到自动程序** |  pwa 节点 |
| Azure Functions |   **连接到后端** |  pwa 节点 |

下表列出了具有自动程序应用（不含选项卡应用）项目的调试配置名称和类型：

|  组件 |  调试配置名称  | 调试配置类型  |
| --- | --- | --- |
|  自动程序或邮件扩展  | **启动自动程序 (Edge)** 或 **启动自动程序 (Chrome)**  |   pwa-msedge 或 pwa-chrome  |
|  自动程序或邮件扩展  |   **连接到自动程序** |  pwa 节点  |
|  Azure Functions |  **连接到后端** |  pwa 节点 |

#### <a name="sideloads-the-teams-app"></a>旁加载 Teams 应用

配置“**连接到前端**”或“**启动自动程序**”，启动新的 Edge 或 Chrome 浏览器实例，并打开网页以加载 Teams 客户端。 加载 Teams 客户端后，Teams 会旁加载由Teams 应用，此应用由 [Microsoft Teams](https://teams.microsoft.com/l/app/>${localTeamsAppId}?installAppPackage=true&webjoin=true&${account-hint}) 启动配置中定义的旁加载 URL 控制。  当 Teams 客户端在 Web 浏览器中加载时，请选择“**添加**”或根据要求从下拉列表中选择一项。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hello-local-debug.png" alt-text="本地调试" border="true":::

   你的应用已添加到 Teams！

## <a name="customize-debug-settings"></a>自定义调试设置

Teams 工具包通过取消选中某些先决条件，自定义调试设置以创建选项卡或自动程序：

<br>

<details>
<summary><b>使用自动程序终结点</b></summary>

1. 在 Visual Studio Code 设置中，清除 **确保 Ngrok 已安装并启动(ngrok)**。

1. 将 `.fx/configs/config.local.json` 中的 siteEndpoint 配置设置为终结点。

```json
{
    "bot": {
        "siteEndpoint": "https://your-bot-tunneling-url"
    }
}

```

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/bot-endpoint.png" alt-text="自定义自动程序终结点":::

</details>

<details>
<summary><b>使用开发证书</b></summary>

1. 在 Visual Studio Code 设置中，清除 **确保开发证书受信任(devCert)**。

1. 将 `.fx/configs/config.local.json` 中的 `sslCertFile` 和 `sslKeyFile` 配置设置为证书文件路径和密钥文件路径。

```json
{
    "frontend": {
        "sslCertFile": "",
        "sslKeyFile": ""
    }
}
```

:::image type="content" source="../assets/images/teams-toolkit-v2/debug/development-certificate-customize.png" alt-text="自定义证书":::

</details>

<details>
<summary><b>使用启动脚本以启动应用服务</b></summary>

1. 对于选项卡，请在 `tabs/package.json`中更新 `dev:teamsfx` 脚本。

1. 对于自动程序或邮件扩展，请在 `bot/package.json` 中更新 `dev:teamsfx` 脚本。

1. 对于 Azure 函数，请在 `api/package.json` 中更新 `dev:teamsfx` 脚本，并为 TypeScript 更新 `watch:teamsfx` 脚本。

   > [!NOTE]
   > 当前不支持自定义选项卡、自动程序、邮件扩展应用和 Azure 函数端口。

</details>

<details>
<summary><b>添加环境变量</b></summary>

你可以将环境变量添加到选项卡、自动程序、邮件扩展和 Azure 函数的 `.env.teamsfx.local` 文件。 Teams 工具包加载添加的环境变量，以在本地调试期间启动服务。

 > [!NOTE]
 > 确保在添加新环境变量后启动新的本地调试，因为环境变量不支持热重新加载。

</details>

<details>
<summary><b>调试部分组件</b></summary>


Teams 工具包利用 Visual Studio Code 多目标调试功能，同时调试选项卡、自动程序、邮件扩展和 Azure 函数。 可以更新 `.vscode/launch.json` 和 `.vscode/tasks.json` 来调试部分组件。 如果只想在 Azure 函数项目中调试选项卡和自动程序，请使用以下步骤：

1. 注释 **连接到自动程序**，**从 `.vscode/launch.json` 中的调试组件连接到后端**。

   ```json
   {
       "name": "Debug (Edge)",
        "configurations": [
           "Attach to Frontend (Edge)",
           // "Attach to Bot",
           // "Attach to Backend""
           ],
           "preLaunchTask": "Pre Debug Check & Start All",
           "presentation": {
               "group": "all",
               "order": 1
           },
           "stopAll": true

   }
   ```

2. 注释在 .vscode/tasks.json 中的“启动所有任务”中“**启动后端**”和“启动自动程序”。

   ```json
   {
                                           
       "label": "Start All",
       "dependsOn": [
           "Start Frontend",
             // "Start Backend",
             // "Start Bot"

         ]
              
   }
   ```

</details>

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [调试后台进程](debug-background-process.md)。

## <a name="see-also"></a>另请参阅

* [使用 Teams 工具包预配云资源](provision.md)
* [将功能添加到 Teams 应用](add-capability.md)
* [部署到云](deploy.md)
* [在 Teams 工具包中管理多个环境](TeamsFx-multi-env.md)
