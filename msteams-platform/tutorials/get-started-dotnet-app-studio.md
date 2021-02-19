---
title: 教程 - 使用 C 创建第一个应用#
description: 了解如何开始使用 C# 或 .NET 生成 Microsoft Teams 应用。
keywords: 入门 .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: 29cc4e0f434bf9ece9c6073af84627acc048b628
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294752"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a>使用 C# 或 .NET 创建你的第一个 Teams 应用

本教程帮助你使用 C# 或 .NET 创建 Microsoft Teams 应用。

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>获取先决条件

若要完成本教程，你需要获取以下工具：

- [安装 Git](https://git-scm.com/downloads)
- [安装Visual Studio](https://www.visualstudio.com/downloads/)。 你可以安装免费的社区版。

在安装过程中，如果有要添加到 PATH 的选项， `git` 请选择它。

在终端窗口中，运行以下命令来验证 `git` 您的安装：

```bash
$ git --version
git version 2.17.1.windows.2

```

> [!NOTE]
> 在平台上使用合适的终端窗口。 这些示例使用 Bash，但在大多数平台上运行。

请确保启动最新版本的 Visual Studio并安装任何更新。

可以使用同一终端窗口运行本教程中的命令。

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>下载示例

你可以开始使用简单的 [Hello， World！](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp) C# 中的示例。 在终端窗口中，运行以下命令将示例存储库克隆到本地计算机：

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> 你可以 [分叉](https://help.github.com/articles/fork-a-repo/) 此 [存储库以](https://github.com/OfficeDev/Microsoft-Teams-Samples) 修改所做的更改并将其保存到 GitHub 以参考。

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>生成和运行示例

克隆存储库后，使用 Visual Studio 从 `Microsoft.Teams.Samples.HelloWorld.sln` **示例的 Microsoft-Teams-Samples/samples/app-hello-world/csharp** 目录中打开解决方案文件，然后从菜单中选择。 `Build Solution` `Build` 若要运行示例， `F5` 请按或 `Start Debugging` 从菜单中 `Debug` 选择。

当应用启动时，浏览器窗口将打开，并启动应用的根。 你可以导航到以下 URL 以验证是否正在加载所有应用 URL：

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- [https://localhost:44327/second]https://localhost:44327/second)

<a name="HostSample"></a>

> [!Note]
> 如果收到错误 `Could not find a part of the path … bin\roslyn\csc.exe` ，则使用命令更新程序包 `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。 有关详细信息，请参阅 [StackOverflow 上的此问题](https://stackoverflow.com/questions/32780315)。

## <a name="host-the-sample-app"></a>托管示例应用

Microsoft Teams 中的应用是提供一个或多个功能的 Web 应用程序。 若要使 Teams 平台加载你的应用，必须从 Internet 访问你的应用。 若要使应用从 Internet 访问，你需要托管你的应用。 你可以免费在 Microsoft Azure 中托管它，或者使用 创建到开发计算机上本地进程的隧道 `ngrok` 。 托管完应用后，请记下其根 URL。 例如， `https://yourteamsapp.ngrok.io` 或 `https://yourteamsapp.azurewebsites.net` 。

### <a name="tunnel-using-ngrok"></a>使用 ngrok 的隧道

为了快速测试，可以在本地计算机上运行应用，并通过 Web 终结点创建一个隧道。 [ngrok](https://ngrok.com) 是一款免费工具，您可以使用该工具获取 Web 地址，如 `https://d0ac14a5.ngrok.io` 。 您可以 [下载并安装](https://ngrok.com/download) ngrok。 请确保将其添加到您的位置 `PATH` 。

安装 ngrok 后，打开一个新的终端窗口并运行以下命令以创建隧道：

```bash
ngrok http 44327 -host-header=localhost:44327
```

此示例使用端口 44327，请务必指定它。

Ngrok 侦听来自 Internet 的请求，将它们路由到在端口 44327 上运行的应用。 若要验证，请打开浏览器并转到 `https://d0ac14a5.ngrok.io/hello` 加载应用的 Hello 页面。 请使用控制台会话中 ngrok 显示的转发地址，而不是此 URL。

> [!NOTE]
> 如果在生成和运行步骤中使用不同的端口，[](#build-and-run-the-sample)请确保使用相同的端口号来设置 `ngrok` 隧道。

> [!TIP]
> 建议在不同的终端窗口中 `ngrok` 运行。 这是为了阻止 ngrok 在不会影响应用的情况下运行，你必须停止、重新生成和重新运行应用。 会话 `ngrok` 在此窗口中提供有用的调试信息。

该应用仅在开发计算机上当前会话期间可用。 如果计算机已关闭或进入睡眠状态，服务将不再可用。 在将应用共享给其他用户进行测试时，请记住这一点。 如果必须重新启动该服务，应用将返回一个新地址，并且必须更新使用该地址的每一个位置。 ngrok 的付费版本没有此限制。

### <a name="host-in-azure"></a>Azure 中的主机

Microsoft Azure 使用共享基础结构在免费层托管 .NET 应用程序。 这足以运行 `Hello World` 示例。 有关详细信息，请参阅 [创建新的免费帐户](https://azure.microsoft.com/free/)。

Visual Studio向不同提供程序（包括 Azure）部署应用提供内置支持。

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>更新托管应用的凭据

示例应用需要将以下环境变量设置为之前记下的值。

打开文件appsettings.js文件。 使用之前保存的自动程序 ID 更新 *MicrosoftAppId* 值。 使用之前保存的自动程序密码更新 *MicrosoftAppPassword。*

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

进行这些更改后，重新生成应用。 如果你使用的是 ngrok，请在本地运行应用，如果你正在 Azure 中托管，请重新部署该应用。

## <a name="configure-the-app-tab"></a>配置应用选项卡

将应用安装到团队后，你需要将其配置为显示内容。 转到已安装示例应用的团队中的频道，然后单击 **"+"** 按钮以添加新选项卡。然后，可以从 `Hello World` "添加选项卡 **"列表中选择** 。 然后，将显示配置对话框。 此对话框将让你选择要在此通道中显示哪个选项卡。 选择该选项卡并单击后，即可看到已加载的 `Save` `Hello World` 选项卡以及您选择的选项卡。

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>在 Teams 中测试机器人

你现在可以在 Teams 中与机器人交互。 选择你在团队中注册应用并键入的频道 `@your-bot-name` 。 这称为 **\@ 提及**。 发送到自动程序的任何邮件都将作为回复发送回。

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>测试邮件扩展

若要测试消息扩展，可以单击对话视图中输入框下方的三个点。 菜单将弹出，并包含 **"Hello World"** 应用。 单击它时，你将看到一组随机文本显示。 你可以选择其中任何一个，并将其插入到对话中。

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

选择其中一个随机文本，你将在底部看到一张格式化卡片，并准备好随自己的邮件一起发送。

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
