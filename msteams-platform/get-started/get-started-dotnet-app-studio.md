---
title: 教程 - 使用 C 创建第一个应用#
description: 了解如何开始使用 Microsoft Teams 或 .NET C#应用程序。
keywords: 入门 .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
localization_priority: Normal
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: f63e729400fa74f1675faddbe0b5f8fa101c8824
ms.sourcegitcommit: 9d63611974ba8a7e7f19ceea35e50189a2e90434
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/02/2021
ms.locfileid: "53254333"
---
# <a name="build-your-first-teams-app-using-c"></a>使用 C 生成Teams应用#

本教程介绍如何使用 .NET 或 Microsoft Teams 生成首个 C#。 它还将引导你完成以下步骤：

1. [准备环境](#prepare-your-environment)
1. [获取先决条件](#GetPrerequisites)
1. [下载示例](#DownloadSample)
1. [生成和运行示例](#BuildRun)
1. [托管示例应用](#hostsample)
1. [更新托管应用的凭据](#updatecredentials)
1. [配置"应用"选项卡](#configureapptab)

<a name="prepare-your-environment"></a>
[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>获取先决条件

若要完成本教程，需要安装以下工具：

- [安装 Git](https://git-scm.com/downloads)
- [安装 Visual Studio](https://www.visualstudio.com/downloads/)

你可以安装免费社区版本的 Visual Studio。 在安装过程中，如果有要添加到路径的选项 `git` ，请选择它。 在终端窗口中，运行以下命令来验证 `git` 安装：

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> 在平台上使用合适的终端窗口。 这些示例使用 Git Bash，但可在大多数平台上运行。

打开最新版本的 Visual Studio并安装任何更新。

可以使用同一终端窗口运行本教程中的命令。

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>下载示例

你可以开始使用简单的 [Hello， World！](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp) C# 示例。 在终端窗口中，运行以下命令将示例存储库克隆到计算机：

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> 可以[分叉此](https://help.github.com/articles/fork-a-repo/)[存储库以](https://github.com/OfficeDev/Microsoft-Teams-Samples)修改所做的更改并将其保存到GitHub。

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>生成和运行示例

可以在克隆 smaple 后生成并运行它。 

**生成并运行克隆的示例**

1. 打开解决方案文件 **Microsoft.Teams。示例的** **Microsoft-Teams-Samples/samples/app-hello-world/csharp** 目录中的 Samples.HelloWorld.sln。
1. 从 **"生成"菜单中** 选择" **生成解决方案** "。
1. 选择 **F5** 键，或者从"调试 **"** 菜单中选择"开始调试"以运行示例。

    当应用启动时，浏览器窗口将打开，并启动应用的根。 你可以转到以下 URL 以验证是否正在加载所有应用 URL：

    - `https://localhost:44327/`
    - `https://localhost:44327/hello`
    - `https://localhost:44327/first`
    - `https://localhost:44327/second`

    > [!Note]
    > 如果收到错误 `Could not find a part of the path … bin\roslyn\csc.exe` ，则使用 命令 更新程序包 `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。 有关详细信息，请参阅 Stack [Overflow 上的此问题](https://stackoverflow.com/questions/32780315)。

    <a name="hostsample"></a>
    ## <a name="deploy-your-sample-app"></a>部署示例应用

    应用程序中Microsoft Teams是提供一个或多个功能的 Web 应用程序。 若要Teams加载应用，应用必须在 Internet 上可用。 为此，你需要托管应用。 你可以免费在 Microsoft Azure中托管它，或者使用 创建到计算机上本地进程的隧道 `ngrok` 。 托管应用后，记下其根 URL，如 `https://yourteamsapp.ngrok.io` 或 `https://yourteamsapp.azurewebsites.net` 。

### <a name="tunnel-using-ngrok"></a>Tunnel ngrok

为了快速测试，可以在计算机上运行应用，并通过 Web 终结点创建一个隧道。 [`ngrok`](https://ngrok.com) 是一款免费工具，可用于获取 Web 地址，例如 `https://d0ac14a5.ngrok.io` 。 你可以 [下载并安装](https://ngrok.com/download) ngrok，并将其添加到 中的位置 `PATH` 。

安装后 `ngrok` ，打开一个新的终端窗口并运行以下命令以创建隧道：

```bash
ngrok http 44327 -host-header=localhost:44327
```

`Ngrok` 响应来自 Internet 的请求，将它们路由到在端口 44327 上运行的应用。 

**验证响应**

1. 打开浏览器并转到 `https://d0ac14a5.ngrok.io/hello` 。 这将加载应用的 Hello 页面。
1. 使用控制台会话中显示的转发地址，而不是步骤 1 中提到的 `ngrok` URL。
    > [!NOTE]
    > 如果在生成和运行步骤中使用不同的 [端口，请确保](#build-and-run-the-sample) 使用相同的端口号来设置 `ngrok` 隧道。
    > [!TIP]
    > 建议在不同的终端 `ngrok` 窗口中运行。 这是为了在不 `ngrok` 干扰应用的情况下阻止运行。 必须停止、重新生成和重新运行应用。 会话 `ngrok` 在此窗口中提供有用的调试信息。

    该应用仅在您的计算机上的当前会话期间可用。 如果计算机关闭或进入睡眠状态，服务将不再可用。 在将应用共享给其他用户进行测试时，请记住这一点。 如果必须重新启动该服务，应用将返回一个新地址，并且必须更新使用该地址的每一个位置。 的付费 `ngrok` 版本没有此限制。

### <a name="host-in-azure"></a>Azure 中的主机

Microsoft Azure共享基础结构在免费层托管 .NET 应用程序。 这足以运行 `Hello World` 示例。 有关详细信息，请参阅 [创建新的免费 Azure 帐户](https://azure.microsoft.com/free/)。

Visual Studio对将应用部署到不同提供程序（包括 Azure）提供内置支持：

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

**更新应用包**

# <a name="app-studio"></a>[应用程序 Studio](#tab/AS)

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

# <a name="developer-portal"></a>[开发人员门户](#tab/DP)

**安装开发人员门户 (预览) 中Teams**


1. 选择 **左侧** 栏底部的"应用"图标，然后搜索"开发人员 **门户"。**

    <img width="430px" alt="Screenshot of TDP" src="~/assets/images/Screen1.png"/>

1. 选择 **"开发人员门户"，** 然后选择"打开 **"。**

    <img width="430px" alt="Screenshot of TDP Open" src="~/assets/images/screen2.png"/>

1. 选择"应用"选项卡，然后选择 **"导入现有应用"。**

    <img width="430px" alt="Screenshot of import app in tdp" src="~/assets/images/screen3.png"/>

1. 选择 **Hello World，****然后选择导入**。 Hello **World** 应用在开发人员门户中导入。 

    可以使用开发人员门户配置Teams应用。 清单位于"分发"下。 可以使用清单为应用配置功能、必需资源和重要的属性。 有关如何使用开发人员门户配置应用的更多详细信息，请参阅开发人员Teams[门户](../concepts/build-and-test/teams-developer-portal.md)。

    <img width="430px" alt="Screenshot of configure tdp" src="~/assets/images/Screen4.png"/>
---

<a name="updatecredentials"></a>
## <a name="update-the-credentials-for-your-hosted-app"></a>更新托管应用的凭据

示例应用要求将环境变量设置为文本文件中保存的值。

**更新托管应用的凭据**

1. 打开 `appsettings.json`文件。 
1. 使用保存在文本文件中的自动程序 ID 更新 **MicrosoftAppId** 值。 
1. 使用保存的自动程序密码更新 **MicrosoftAppPassword。**

    <img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

    进行这些更改后，重新生成应用。 如果你使用的是 ngrok，请在本地运行应用，如果你要托管在 Azure 中，请重新部署该应用。

<a name="configureapptab"></a>
## <a name="configure-the-app-tab"></a>配置"应用"选项卡

将应用安装到团队后，必须将其配置为显示内容。 

**配置"应用"选项卡**

1. 转到你安装了示例应用的团队中的频道，然后选择 **"+"** 按钮以添加新选项卡。
1. 从 **添加选项卡** 列表中选择Hello World。 将显示一个配置对话框，允许您选择要在此通道中显示的选项卡。 
1. 选择“**保存**”。 选项卡 `Hello World` 随选项卡一起加载。

    <img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>在设备中测试Teams

现在可以在 Teams 中测试自动程序。 

**测试机器人**

* 选择你注册应用的团队中的频道并键入 `@your-bot-name` 。 这称为 **\@ 提及**。 机器人将回复你发送的任何消息。

    <img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>测试邮件扩展

**测试邮件扩展**
1. 选择 **对话** 视图中输入框下方的...。 将显示包含 **"Hello World"应用的** 菜单。 
1. 选择菜单，将显示一组随机文本。 可以选择其中一个随机文本，该文本将插入到对话中。

    <img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu1.png" />

    <img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result1.png" />

1. 选择随机文本之一。 将显示格式化的卡片，并准备随自己的邮件一起发送。

    <img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />

## <a name="see-also"></a>另请参阅

* [教程概述](code-samples.md)
* [创建对话机器人应用](first-app-bot.md)
* [创建邮件扩展](first-message-extension.md)
* [代码示例](https://github.com/OfficeDev/Microsoft-Teams-Samples)