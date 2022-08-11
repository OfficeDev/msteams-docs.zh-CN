---
author: surbhigupta
title: 调试适用于 Visual Studio 的 Teams 应用
description: 在本模块中，了解如何使用 Teams 工具包在 Visual Studio 本地调试 Teams 应用
ms.author: v-amprasad
ms.localizationpriority: high
ms.topic: overview
ms.date: 03/21/2022
ms.openlocfilehash: cff0b3e18f63bc7943a7fc16875294f41257a37c
ms.sourcegitcommit: 52a11f7614c43172bc2d57401a60d569db5310a9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/09/2022
ms.locfileid: "67291665"
---
# <a name="debug-your-teams-app-locally-using-visual-studio"></a>使用 Visual Studio 在本地调试 Teams 应用

Teams 工具包可帮助你在本地调试和预览 Microsoft Teams 应用。 调试是生成、检查、检测和更正应用中的问题或 bug 的过程。 调试可确保程序成功运行。 Visual Studio 允许调试选项卡、机器人和消息扩展。 Teams 工具包支持以下调试功能：

* 准备 Teams 应用依赖项
* 开始调试
* 切换断点
* 热重新加载
* 停止调试

在调试过程中，Teams 工具包会自动启动应用服务、启动调试和旁加载 Teams 应用。 调试后，可以在 Teams Web 客户端中预览 Teams 应用。 还可以自定义调试设置，以使用机器人终结点或环境变量加载已配置的应用。

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

## <a name="debug-your-app-locally"></a>在本地调试应用

可以通过执行以下操作，在 Visual Studio 中使用 Teams 工具包在本地调试应用：

### <a name="set-up-ngrok-only-for-bot-and-message-extension-app"></a>设置仅适用于机器人和消息扩展应用的 ngrok () 

使用命令提示符运行以下命令：

```
ngrok http 5130
```

### <a name="set-up-your-teams-toolkit"></a>设置 Teams 工具包

创建项目后，使用 Teams 工具包执行以下步骤来调试应用：

1. 右键单击 **项目**。
1. 选择 **Teams 工具包**。
1. 选择 **“准备 Teams 应用依赖项**”。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-teamsappdependencies.png" alt-text="用于本地调试的 Teams 应用依赖项":::

   > [!NOTE]
   > 在此方案中，项目名称为 MyTeamsApp1

   登录前，Microsoft 365 帐户需要具有旁加载权限。  请确保 Teams 应用可以上传到租户，否则 Teams 应用可能无法在 Teams 客户端中运行。

1. 登录到 **Microsoft 365 帐户**。
1. 选择 **“继续**
   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-signin-m365.png" alt-text="登录到 Microsoft 365 帐户":::”

   > [!Note]
   > 通过访问了解有关旁加载权限的详细信息 <https://aka.ms/teamsfx-sideloading-option>。

1. 选择 **“调试**”。
1. 选择 **“开始调试**”，或直接选择 **F5**。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-Startdebug.png" alt-text="开始调试":::

   Visual Studio 在浏览器中的 Microsoft Teams 客户端中启动 Teams 应用。

   > [!Note]
   > 通过访问了解详细信息 <https://aka.ms/teamsfx-vs-debug>。

1. 加载 Microsoft Teams 后，选择 **“添加** ”以在 Teams 中安装应用。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-add-loadapp.png" alt-text="选择“添加以加载应用”":::

   > [!TIP]
   > 还可以在调试期间使用 Visual Studio 的热重载函数。 通过访问了解详细信息 <https://aka.ms/teamsfx-vs-hotreload>。

   > [!NOTE]
   > 在调试通知机器人应用时，请确保将 HTTP 请求发布到“<http://localhost:5130/api/notification>”以触发通知。 如果在创建项目时选择了 HTTP 触发器，则可以使用任何 API 工具，例如 curl (Windows 命令提示符) 、Postman 等。

   > [!TIP]
   > 如果对 Teams 应用清单文件 (/templates/appPackage/manifest.template.json) 进行任何更改，请确保执行 Prepare Teams 应用依赖项命令。 在尝试在本地再次运行 Teams 应用之前。

## <a name="key-features-of-teams-toolkit"></a>Teams 工具包的主要功能

可以看到 Teams 工具包的以下主要功能，这些功能可自动执行 Teams 应用的本地调试过程：

### <a name="prepare-teams-app-dependencies"></a>准备 Teams 应用依赖项

Teams 工具包准备本地调试依赖项，并在帐户的租户中注册 Teams 应用。 对于机器人和消息扩展应用，Teams 工具包将注册和配置机器人。

### <a name="start-debugging"></a>开始调试

可以使用单个操作执行调试，按 **F5** 开始调试。 Teams 工具包在浏览器中生成代码、启动服务和启动应用。

### <a name="toggle-breakpoints"></a>切换断点

可以在选项卡、机器人、消息扩展和 Azure 函数的源代码中切换断点。 在 Web 浏览器中与 Teams 应用交互时，断点会执行。
下图显示了切换断点：

:::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-toggle-breakpoint.png" alt-text="本地调试切换断点":::

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

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-launch-teamsapp-webapp.png" alt-text="通过删除 launchurl 将团队作为 Web 应用启动":::

1. 右键单击 **“解决方案**”。
1. 选择“属性”。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-solution-properties.png" alt-text="右键单击解决方案并选择属性":::

1. 在对话中选择 **配置属性** > **配置** 。
1. 选择取消选中 **“部署** ”进程框。
1. 选择“**确定**”。

   :::image type="content" source="../assets/images/debug-teams-app/vs-localdebug-disable-deploy.png" alt-text="取消选中配置属性中的部署 ":::

## <a name="see-also"></a>另请参阅

* [使用 Visual Studio 预配云资源](provision-cloud-resources.md)
* [使用 Visual Studio 将 Teams 应用部署到云](deploy-teams-app.md)
* [使用 Visual Studio 编辑 Teams 应用清单](VS-TeamsFx-preview-and-customize-app-manifest.md)
