---
title: 教程 - 使用 C 创建第一个应用#
description: 了解如何开始使用 .NET 或 C#构建 Microsoft Teams 应用。
keywords: 入门 .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: ededd0800c7f789469e79e2a475c125b7fc37795
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449317"
---
# <a name="create-your-first-teams-app-using-c-or-net"></a>使用 .NET 或 C#创建你的第一个 Teams 应用

本教程帮助你使用 C# .NET 创建 Microsoft Teams 应用。 为此，你必须：

* 准备环境
* 获取先决条件
* 下载示例
* 生成和运行示例
* 托管示例应用
* 更新托管应用的凭据
* 配置应用选项卡

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>获取先决条件

若要完成本教程，需要安装以下工具：

- [安装 Git](https://git-scm.com/downloads)
- [安装 Visual Studio](https://www.visualstudio.com/downloads/)

你可以安装免费的社区版Visual Studio。 在安装过程中，如果有要添加到路径的选项 `git` ，请选择它。 在终端窗口中，运行以下命令来验证 `git` 您的安装：

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

你可以开始使用简单的 [Hello， World！](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/csharp) C# 示例。 在终端窗口中，运行以下命令将示例存储库克隆到您的计算机：

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> 你可以 [分叉](https://help.github.com/articles/fork-a-repo/) 此 [存储库以](https://github.com/OfficeDev/Microsoft-Teams-Samples) 修改所做的更改并将其保存到 GitHub。

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>生成和运行示例

克隆存储库后，使用 Visual Studio 从示例的 **Microsoft-Teams-Samples/samples/app-hello-world/csharp** 目录中打开解决方案文件 **Microsoft.Teams.Samples.HelloWorld.sln。** 然后，从 **"生成"菜单中** 选择"生成 **解决方案** "。 若要运行示例，请按 **F5** 或从 **"调试"菜单中选择"开始****调试**"。

当应用启动时，浏览器窗口将打开，并启动应用的根。 你可以转到以下 URL 来验证是否正在加载所有应用 URL：

- [https://localhost:44327/](https://localhost:44327/)
- [https://localhost:44327/hello](https://localhost:44327/hello)
- [https://localhost:44327/first](https://localhost:44327/first)
- [https://localhost:44327/second]https://localhost:44327/second)

<a name="HostSample"></a>

> [!Note]
> 如果收到错误 `Could not find a part of the path … bin\roslyn\csc.exe` ，则使用命令更新程序包 `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。 有关详细信息，请参阅 Stack [Overflow 上的此问题](https://stackoverflow.com/questions/32780315)。

## <a name="host-the-sample-app"></a>托管示例应用

Microsoft Teams 中的应用是提供一个或多个功能的 Web 应用程序。 若要让 Teams 平台加载你的应用，你的应用必须在 Internet 上可用。 为此，你需要托管应用。 你可以免费在 Microsoft Azure 中托管它，或者使用 创建到计算机上本地进程的隧道 `ngrok` 。 托管应用后，记下其根 URL，例如或 `https://yourteamsapp.ngrok.io` `https://yourteamsapp.azurewebsites.net` 。

### <a name="tunnel-using-ngrok"></a>使用 ngrok 的隧道

为了快速测试，可以在您的计算机上运行该应用，并通过 Web 终结点创建一个隧道。 [`ngrok`](https://ngrok.com) 是一个免费工具，可用于获取 Web 地址，例如 `https://d0ac14a5.ngrok.io` 。 可以 [下载并安装](https://ngrok.com/download) ngrok，并将其添加到您的位置 `PATH` 。

安装后 `ngrok` ，打开一个新的终端窗口并运行以下命令以创建隧道：

```bash
ngrok http 44327 -host-header=localhost:44327
```

`Ngrok` 侦听来自 Internet 的请求，将它们路由到在端口 44327 上运行的应用。 若要验证，请打开浏览器并转到 `https://d0ac14a5.ngrok.io/hello` 加载应用的 Hello 页面。 使用控制台会话中显示的转发地址，而不是 `ngrok` 此 URL。

> [!NOTE]
> 如果在生成和运行步骤中使用不同的端口，[](#build-and-run-the-sample)请确保使用相同的端口号来设置 `ngrok` 隧道。

> [!TIP]
> 建议在不同的终端窗口中 `ngrok` 运行。 这是为了阻止 `ngrok` 运行而不会影响应用。 必须停止、重新生成和重新运行应用。 会话 `ngrok` 在此窗口中提供有用的调试信息。

该应用仅在您计算机的当前会话期间可用。 如果计算机已关闭或进入睡眠状态，服务将不再可用。 在将应用共享给其他用户进行测试时，请记住这一点。 如果必须重新启动该服务，应用将返回一个新地址，并且必须更新使用该地址的每一个位置。 付费版 `ngrok` 没有此限制。

### <a name="host-in-azure"></a>Azure 中的主机

Microsoft Azure 使用共享基础结构在免费层托管 .NET 应用程序。 这足以运行 `Hello World` 示例。 有关详细信息，请参阅 [创建新的免费 Azure 帐户](https://azure.microsoft.com/free/)。

Visual Studio向不同提供程序（包括 Azure）部署应用提供内置支持。

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>更新托管应用的凭据

示例应用要求将环境变量设置为保存在文本文件 [中的值](~/includes/get-started/get-started-use-app-studio.md#bots)。

打开appsettings.js上的文件。 使用保存在文本文件中的自动程序 ID 更新 **MicrosoftAppId** 值。 使用保存的自动程序密码更新 **MicrosoftAppPassword。**

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

进行这些更改后，重新生成应用。 如果你使用的是 ngrok，请在本地运行应用，如果你正在 Azure 中托管，请重新部署该应用。

## <a name="configure-the-app-tab"></a>配置应用选项卡

将应用安装到团队后，必须将其配置为显示内容。 转到已安装示例应用的团队中的频道，然后选择 **"+"** 按钮以添加新选项卡。从 **"添加选项卡****"列表中选择** Hello World。 此时将显示一个配置对话框，允许您选择要在此通道中显示的选项卡。 选择选项卡并选择" **保存选项卡** `Hello World` "后，选项卡随选项卡一起加载。

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>在 Teams 中测试机器人

现在，你可以测试 Teams 中的自动程序。 选择你在团队中注册应用并键入的频道 `@your-bot-name` 。 这称为 **\@ 提及**。 自动程序将回复你发送的任何消息。

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>测试邮件扩展

若要测试邮件扩展，可以选择 **对话** 视图中输入框下方的...。 将显示包含 **"Hello World"应用的** 菜单。 选择它时，将显示一组随机文本。 可以选择其中一个随机文本并插入到对话中。

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

选择随机文本之一。 将显示格式化并准备好随您自己的邮件一起发送的卡片。

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
