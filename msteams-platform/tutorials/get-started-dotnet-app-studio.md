---
title: 教程 - 使用 C 创建第一个应用#
description: 了解如何开始使用 C#/.NET 生成 Microsoft Teams 应用。
keywords: 入门 .net c# csharp
ms.custom: scenarios:getting-started; languages:ASP.NET,C#
ms.topic: tutorial
ms.date: 11/09/2018
ms.openlocfilehash: c28c4d00c375b8e37f82c343eec2c5405ae0c1c8
ms.sourcegitcommit: fa64b83c0b534bf7a89f256880d5b5ca193e4b04
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/28/2021
ms.locfileid: "50037037"
---
# <a name="create-your-first-microsoft-teams-app-using-c"></a>使用 C 创建你的第一个 Microsoft Teams 应用#

本教程可帮助你开始使用 .NET 上的 C# 创建 Microsoft Teams 应用。

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>获取先决条件

若要完成本教程，你需要获取以下工具：

- [安装 Git](https://git-scm.com/downloads)
- [安装Visual Studio](https://www.visualstudio.com/downloads/)。 你可以安装免费的社区版。

如果在安装过程中看到要添加到 PATH 的选项， `git` 请选择这样做。 它很方便。

在 `git` 终端窗口中运行以下代码，验证安装：
> [!NOTE]
> 使用你最熟悉平台的终端窗口。 这些示例使用 Bash，但将在大多数平台上运行。

```bash
$ git --version
git version 2.17.1.windows.2

```

请确保启动最新版本的 Visual Studio并安装任何更新（如果显示）。

你可以继续使用此终端窗口运行本教程中遵循的命令。

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>下载示例

我们提供了简单的 [Hello， World！](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) 示例。 在终端窗口中，运行以下命令将示例存储库克隆到本地计算机：

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> 如果要[修改并](https://help.github.com/articles/fork-a-repo/)[签入对](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)GitHub 所做的更改，可分叉此存储库供将来参考。

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>生成和运行示例

克隆存储库后，使用Visual Studio从示例的根目录打开解决方案文件，然后 `Microsoft.Teams.Samples.HelloWorld.sln` `Build Solution` 从菜单中 `Build` 单击。 可以通过按或从菜单中 `F5` 选择来 `Start Debugging` 运行 `Debug` 示例。

当应用启动时，你将看到浏览器窗口打开，并且应用的根已启动。 你可以导航到以下 URL 以验证是否正在加载所有应用 URL：

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> 如果收到类似错误 `Could not find a part of the path … bin\roslyn\csc.exe` ，请尝试使用命令更新程序包 `Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r` 。 有关 [其他详细信息，请参阅 StackOverflow](https://stackoverflow.com/questions/32780315) 上的此问题。

## <a name="host-the-sample-app"></a>托管示例应用

请记住，Microsoft Teams 中的应用是公开一个或多个功能的 Web 应用程序。 若要让 Teams 平台加载你的应用，必须从 Internet 访问你的应用。 若要使应用从 Internet 访问，你需要托管你的应用。 你可以免费在 Microsoft Azure 中托管它，或者使用创建到开发计算机上本地进程的隧道 `ngrok` 。 托管完应用后，记下其根 URL。 它的外观如下所示：或 `https://yourteamsapp.ngrok.io` `https://yourteamsapp.azurewebsites.net` 。

### <a name="tunnel-using-ngrok"></a>使用 ngrok 的隧道

为了快速测试，可以在本地计算机上运行应用，并通过 Web 终结点创建一个隧道。 [ngrok](https://ngrok.com) 是一款免费工具，允许你执行这一操作。 通过 ngrok，您可以获取 Web 地址 `https://d0ac14a5.ngrok.io` ， (此 URL 只是一个) 。 您可以 [为环境](https://ngrok.com/download) 下载并安装 ngrok。 请确保将其添加到您的位置 `PATH` 。

安装后，可以打开一个新的终端窗口并运行以下命令以创建隧道。 此示例使用端口 3333，因此请务必在此处指定它。

```bash
ngrok http 3333 -host-header=localhost:3333
```

Ngrok 将侦听来自 Internet 的请求，并路由到在端口 3333 上运行的应用。 可以通过打开浏览器并加载 `https://d0ac14a5.ngrok.io/hello` 应用的 Hello 页面进行验证。 请确保使用 ngrok 在控制台会话中显示的转发地址，而不是此 URL。

> [!NOTE]
> 如果在以上构建和运行步骤中使用不同的端口[](#build-and-run-the-sample)，请确保使用相同的端口号来设置 `ngrok` 隧道。
> [!TIP]
> 建议在不同的终端窗口中运行，以保持其运行，而不会影响应用，稍后可能需要停止、重新生成 `ngrok` 和重新运行。 会话 `ngrok` 将在此窗口中返回有用的调试信息。

该应用仅在开发计算机上当前会话期间可用。 如果计算机关闭或进入睡眠状态，服务将不再可用。 在共享应用供其他用户进行测试时，请记住这一点。 如果必须重新启动服务，它将返回一个新地址，并且必须更新使用该地址的每一位置。 Ngrok 的付费版本没有此限制。

### <a name="host-in-azure"></a>Azure 中的主机

Microsoft Azure 允许你使用共享基础结构在免费层托管 .NET 应用程序。 这将足以运行 `Hello World` 此示例。 有关详细信息 [，请参阅创建新的免费](https://azure.microsoft.com/free/) 帐户。

Visual Studio对应用部署到不同提供程序（包括 Azure）的内置支持。

<img width="530px" alt="Visual Studio" src="~/assets/images/get-started/publishtoazure1.png"/>

[!include [Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>更新托管应用的凭据

示例应用要求将以下环境变量设置为之前记录的值。

打开文件appsettings.js文件。 使用之前保存的自动程序 ID 更新 *MicrosoftAppId* 值。 使用之前保存的自动程序密码更新 *MicrosoftAppPassword。*

<img width="560px" alt="Setting the keys" src="~/assets/images/get-started/get-started-net-azure-add-keys.png"/>

进行这些更改后，重新生成应用。 如果你使用的是 ngrok，请在本地运行应用，如果你托管在 Azure 中，请重新部署该应用。

## <a name="configure-the-app-tab"></a>配置应用选项卡

将应用安装到团队后，你需要将其配置为显示内容。 转到你安装示例应用的团队中的频道，然后单击 **"+"** 按钮以添加新选项卡。然后，可以从 `Hello World` "添加选项卡 **"列表中选择** 。 然后，将显示配置对话框。 此对话框将让你选择要在此通道中显示的选项卡。 选择该选项卡并单击后，即可看到已加载的 `Save` `Hello World` 选项卡以及您选择的选项卡。

<img width="530px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png" />

### <a name="test-your-bot-in-teams"></a>在 Teams 中测试机器人

现在，你可以与 Teams 中的机器人进行交互。 选择你注册应用的团队中的频道，然后键入 `@your-bot-name` 。 这称为 **\@ 提及**。 向自动程序发送的任何消息都将作为回复发送回。

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>测试邮件扩展

若要测试消息扩展，可以单击对话视图中输入框下方的三个点。 菜单将弹出，并 **包含"Hello World"** 应用。 单击它时，你将看到一组随机文本显示。 可以选择其中任何一个，并将其插入到对话中。

<img width="530px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

选择随机文本之一，你将在底部看到一张格式化卡片，并准备好随自己的邮件一起发送。

<img width="530px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
