---
title: 调试 Teams 应用
author: surbhigupta
description: 在本模块中，了解如何在 Teams 工具包中调试 Teams 应用以及 Teams 工具包的主要功能
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
zone_pivot_groups: teams-app-platform
ms.openlocfilehash: 624cad282e181ed56cbc3041f725b046ca061c72
ms.sourcegitcommit: 637b8f93b103297b1ff9f1af181680fca6f4499d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/07/2022
ms.locfileid: "68499158"
---
# <a name="debug-your-teams-app"></a>调试 Teams 应用

Teams 工具包可帮助你调试和预览 Microsoft Teams 应用。 调试是检查、检测和更正问题或 bug 以确保程序在 Teams 中成功运行的过程。

::: zone pivot="visual-studio-code"

## <a name="debug-your-teams-app-for-visual-studio-code"></a>调试 Teams 应用以Visual Studio Code

Microsoft 中的 Teams 工具包Visual Studio Code自动执行调试过程。 可以检测错误并修复这些错误，并预览 Teams 应用。 还可以自定义调试设置以创建选项卡或机器人。

## <a name="debug-your-microsoft-teams-app-for-visual-studio-code"></a>调试 Microsoft Teams 应用以进行Visual Studio Code

Visual Studio Code中的 Teams 工具包自动执行调试过程。 可以检测错误并修复这些错误，并预览 Teams 应用。 还可以自定义调试设置以创建选项卡或机器人。

在调试过程中：

* Teams 工具包会自动启动应用服务、启动调试器和旁加载 Teams 应用。
* Teams 工具包在调试后台过程中检查先决条件。
* 调试后，Teams 应用可在本地 Teams Web 客户端中预览。
* 还可以自定义调试设置，使用自动程序终结点、开发证书或调试部分组件来加载配置应用。
* Microsoft Visual Studio Code允许你调试选项卡、机器人、消息扩展和Azure Functions。

## <a name="key-debug-features-of-teams-toolkit"></a>Teams 工具包的关键调试功能

Teams 工具包支持以下调试功能：

* [开始调试](#start-debugging)
* [多目标调试](#multi-target-debugging)
* [切换断点](#toggle-breakpoints)
* [热重新加载](#hot-reload)
* [停止调试](#stop-debugging)

Teams 工具包在调试过程中执行后台函数，其中包括验证调试所需的先决条件。 可以在 Teams 工具包的输出通道中查看验证过程的进度。 在安装过程中，可以注册和配置 Teams 应用。

### <a name="start-debugging"></a>开始调试

可以按 **F5** 作为单个操作开始调试。 Teams 工具包开始检查先决条件、注册 Azure AD 应用、Teams 应用以及注册机器人、启动服务和启动浏览器。

### <a name="multi-target-debugging"></a>多目标调试

Teams 工具包利用多目标调试功能同时调试选项卡、自动程序、邮件扩展和 Azure 函数。

### <a name="toggle-breakpoints"></a>切换断点

可以在选项卡、自动程序、邮件扩展和 Azure 函数的源代码上切换断点。 在 Web 浏览器中与 Teams 应用交互时，将执行断点。 下图显示了切换断点：

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/toggle-points.png" alt-text="切换断点" lightbox="../assets/images/teams-toolkit-v2/debug/toggle-points.png":::

### <a name="hot-reload"></a>热重新加载

在调试 Teams 应用时，可以同时更新和保存选项卡、机器人、消息扩展和Azure Functions的源代码。 应用将重新加载，调试器将重新连接到编程语言。

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/hot-reload.png" alt-text="源代码的热重新加载" lightbox="../assets/images/teams-toolkit-v2/debug/hot-reload.png":::

### <a name="stop-debugging"></a>停止调试

完成本地调试后，可以选择 **“停止 (Shift+F5)** 或[Alt] 从浮动调试工具栏 **(Shift+F5) 断开连接** ，停止所有调试会话并终止任务。 下图显示了停止调试操作：

   :::image type="content" source="../assets/images/teams-toolkit-v2/debug/stop-debug.png" alt-text="停止调试":::

## <a name="prepare-for-debug"></a>准备调试

以下步骤可帮助你准备调试：

### <a name="sign-in-to-microsoft-365"></a>登录 Microsoft 365

如果已注册 Microsoft 365，请登录到 Microsoft 365。 有关详细信息，请参阅 [Microsoft 365 开发人员计划](tools-prerequisites.md#microsoft-365-developer-program)

### <a name="toggle-breakpoints"></a>切换断点

有关详细信息，请参阅[“切换断点](#toggle-breakpoints)”，确保可以在选项卡、机器人、消息扩展和Azure Functions的源代码上切换断点

## <a name="customize-debug-settings"></a>自定义调试设置

Teams 工具包取消选中某些先决条件，并允许你自定义调试设置以创建选项卡或机器人:

<br>

<details>
<summary><b>使用自动程序终结点</b></summary>

1. 在Visual Studio Code设置中，需要取消选中 **“确保 Ngrok 已安装并启动 (ngrok)**。

1. 可以将配置`.fx/configs/config.local.json`设置`siteEndpoint`为终结点。

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

1. 在Visual Studio Code设置中，需要取消选中 **“确保开发证书受信任 (devCert)**。

1. 可以将证书文件路径和密钥文件路径设置 `sslCertFile` 和 `sslKeyFile` 配置 `.fx/configs/config.local.json` 到其中。

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

1. 对于选项卡，需要在其中更新 `dev:teamsfx` 脚本 `tabs/package.json`。

1. 对于机器人或消息扩展，需要在其中更新 `dev:teamsfx` 脚本 `bot/package.json`。

1. 对于Azure Functions，需要更新 `dev:teamsfx` TypeScript 更新脚本`api/package.json`和 TypeScript 更新`watch:teamsfx`脚本。

   > [!NOTE]
   > 当前不支持自定义选项卡、自动程序、邮件扩展应用和 Azure 函数端口。

</details>

<details>
<summary><b>添加环境变量</b></summary>

你可以将环境变量添加到选项卡、自动程序、邮件扩展和 Azure 函数的 `.env.teamsfx.local` 文件。 Teams 工具包加载添加的环境变量，以在本地调试期间启动服务。

 > [!NOTE]
 > 请确保在添加新环境变量后启动新的本地调试，因为环境变量不支持热重新加载。

</details>

<details>
<summary><b>调试部分组件</b></summary>

Teams 工具包利用 Visual Studio Code 多目标调试功能，同时调试选项卡、自动程序、邮件扩展和 Azure 函数。 可以更新 `.vscode/launch.json` 和 `.vscode/tasks.json` 来调试部分组件。 如果只想在 Azure 函数项目中调试选项卡和自动程序，请使用以下步骤：

1. 注释 **`Attach to Bot`** 和 **`Attach to Backend`** 从调试复合在 `.vscode/launch.json`。

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

2. 在 .vscode/tasks.json 中从“开始所有”任务中注释 **`Start Backend`** 和启动机器人。

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

## <a name="next"></a>Next

> [!div class="nextstepaction"]
> [在本地调试应用](debug-local.md)

::: zone-end

::: zone pivot="visual-studio"

## <a name="debug-your-teams-app-using-visual-studio"></a>使用 Visual Studio 调试 Teams 应用

Teams 工具包自动执行应用启动服务、启动调试和旁加载 Teams 应用。 调试后，可以在 Teams Web 客户端中预览 Teams 应用。 还可以自定义调试设置，以使用机器人终结点或环境变量加载已配置的应用。 Visual Studio 允许调试选项卡、机器人和消息扩展。 在调试过程中，Teams 工具包支持以下调试功能：

* 准备 Teams 应用依赖项
* 开始调试
* 切换断点
* 热重新加载
* 停止调试

## <a name="prerequisites"></a>先决条件

| &nbsp; | 安装 | 用于使用... |
| --- | --- | --- |
| &nbsp; | **Required** | &nbsp; |
| &nbsp; | Visual Studio 2022 版本 17.3 | 可以安装 Visual Studio 的企业版，并安装“ASP.NET”工作负荷和 Microsoft Teams 开发工具。 |
| &nbsp; | Teams 工具包 | 一个 Visual Studio 扩展，用于为应用创建项目基架。 使用最新版本。 |
| &nbsp; | [Microsoft Teams](https://www.microsoft.com/microsoft-teams/download-app) | 通过聊天、会议、通话等应用与每一位同事进行协作的 Microsoft Teams - 一个地方完成所有操作。 |
| &nbsp; | [准备 Microsoft 365 租户](../concepts/build-and-test/prepare-your-o365-tenant.md) | 对具有相应安装应用权限的 Teams 帐户的访问权限。 |
| &nbsp; | [Microsoft 365 开发人员帐户](/../concepts/build-and-test/prepare-your-o365-tenant) | 对具有相应安装应用权限的 Teams 帐户的访问权限。 |
| &nbsp; | Azure 工具和 [Microsoft Azure CLI](/cli/azure/install-azure-cli) | 用于访问存储数据或在 Azure 中为 Teams 应用部署基于云的后端的 Azure 工具。 |
|&nbsp;  | **可选** | &nbsp; |
|&nbsp; |[Ngrok](https://ngrok.com/) | Ngrok 用于将外部消息从 Azure Bot Framework 转发到本地计算机。|

## <a name="key-features-of-teams-toolkit"></a>Teams 工具包的主要功能

可以看到 Teams 工具包的以下主要功能，这些功能可自动执行 Teams 应用的本地调试过程：

### <a name="prepare-teams-app-dependencies"></a>准备 Teams 应用依赖项

Teams 工具包准备本地调试依赖项，并在帐户的租户中注册 Teams 应用。 对于机器人和消息扩展应用，Teams 工具包将注册和配置机器人。

### <a name="start-debugging"></a>开始调试

可以使用单个操作执行调试，按 **F5** 开始调试。 Teams 工具包在浏览器中生成代码、启动服务和启动应用。

### <a name="toggle-breakpoints"></a>切换断点

可以在选项卡、机器人、消息扩展和 Azure 函数的源代码中切换断点。 在 Web 浏览器中与 Teams 应用交互时，断点会执行。
下图显示了切换断点：

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png" alt-text="本地调试切换断点" lightbox="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png":::

### <a name="hot-reload"></a>热重新加载

选择 **热重载** 在调试期间同时更新和保存源代码时，在 Teams 应用中应用更改。

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload.png" alt-text="选择热重载图标":::

从下拉列表 **中选择“文件保存”热重载** 选项以启用自动热重载。

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-hot-reload-filesave.png" alt-text="在文件保存时选择热重载":::
  
   > [!Tip]
   > 若要详细了解在调试期间 visual Studio 的热重载函数，可以访问<https://aka.ms/teamsfx-vs-hotreload>。

### <a name="stop-debugging"></a>停止调试

本地调试完成后，选择 **“停止** 调试”。

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Stopdebug.png" alt-text="选择“停止调试”图标":::

## <a name="customize-debug-settings"></a>自定义调试设置

可以自定义 Teams 应用的调试设置，以使用机器人终结点并添加环境变量：

### <a name="use-your-bot-endpoint"></a>使用自动程序终结点

可以将 **.fx/configs/config.local.json** 中的 siteEndpoint 配置设置为终结点。

```
"bot": {
    "siteEndpoint": "https://baidu.com"
}
```

### <a name="add-environment-variables"></a>添加环境变量

可以将 **environmentVariables** 添加到 **launchSettings.json** 文件。

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-environment-variables.png" alt-text="添加自定义环境变量":::

### <a name="launch-teams-app-as-a-web-app"></a>将 Teams 应用作为 Web 应用启动

可以将 Teams 应用作为 Web 应用启动，而不是在 Teams 客户端中运行。

1. 在项目下的解决方案资源管理器面板中选择 **“属性** > **”launchSettings.json**。
1. 从文件中删除 **“launchUrl”。**

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png" alt-text="通过删除 launchurl 将团队作为 Web 应用启动" lightbox="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png":::

1. 右键单击 **“解决方案** ”，然后选择 **“属性**”。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png" alt-text="右键单击解决方案并选择属性" lightbox="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png":::

1. 在对话框中选择 **“配置属性** > **配置** ”。
1. 清除 **“部署”** 复选框。
1. 选择“**确定**”。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png" alt-text="取消选中配置属性中的部署" lightbox="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png":::

::: zone-end

## <a name="see-also"></a>另请参阅

* [调试后台进程](debug-background-process.md)
* [使用 Teams 工具包预配云资源](provision.md)
* [部署到云](deploy.md)
* [预览和自定义 Teams 应用清单](TeamsFx-preview-and-customize-app-manifest.md)
