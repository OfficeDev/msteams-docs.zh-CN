---
title: '开始使用 c #/.NET'
description: '使用 c #/.NET 在 Microsoft 团队中开始构建出色的应用程序'
keywords: '入门 .net c # csharp'
ms.date: 11/09/2018
ms.openlocfilehash: de133894042baaba897a9f046d613cd5dbb94eee
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673187"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-cnet-and-app-studio"></a>使用 c #/.NET 和应用程序工作室在 Microsoft 团队平台上开始使用

[Microsoft 团队](/microsoftteams/)开发人员平台使您能够轻松扩展团队并将自己的应用程序和服务与团队工作区无缝集成。 然后，可以将这些应用分发到企业或世界各地的团队。

若要扩展 Microsoft 团队，你将需要创建 Microsoft 团队应用。 Microsoft 团队应用程序是您承载的 web 应用程序。 然后，可以将此应用集成到团队中的用户工作区中。

本教程将帮助您开始使用 .NET 中的 c # 创建 Microsoft 团队应用程序。 您可以通过将应用程序加载到您有权访问的团队，或使用 Office 开发人员程序创建的测试租户来测试应用程序。

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="GetPrerequisites"></a>

## <a name="get-prerequisites"></a>获取先决条件

若要完成本教程，您需要获取以下工具：

- [安装 Git](https://git-scm.com/downloads)
- [安装 Visual Studio 2017](https://www.visualstudio.com/downloads/)。 您可以安装免费社区版。

如果您在安装过程中看到`git`一个添加到路径的选项，请选择执行此操作。 这将很方便。

通过在`git`终端窗口中运行以下命令来验证您的安装：
> [!NOTE]
> 在你的平台上使用你最舒适的终端窗口。 这些示例使用 Bash，但将在大多数平台上运行。

```bash
$ git --version
git version 2.17.1.windows.2

```

请务必启动 Visual Studio 2017 并安装任何更新（如图所示）。

您可以继续使用此终端窗口运行本教程后面的命令。

<a name="DownloadSample"></a>

## <a name="download-the-sample"></a>下载示例

我们提供了一个简单的[Hello，World！](https://github.com/OfficeDev/msteams-samples-hello-world-csharp) 在 c # 中的示例可帮助您入门。 在终端窗口中，运行以下命令以将示例存储库克隆到本地计算机：

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-csharp.git
```

> [!TIP]
> 如果要将所做的更改修改并签入 GitHub 以供将来参考[，则可以](https://github.com/OfficeDev/msteams-samples-hello-world-csharp)[派生](https://help.github.com/articles/fork-a-repo/)此存储库。

<a name="BuildRun"></a>

## <a name="build-and-run-the-sample"></a>生成和运行示例

克隆存储库后，使用 Visual Studio 从示例的根目录中打开`Microsoft.Teams.Samples.HelloWorld.sln`解决方案文件，然后单击`Build Solution` `Build`菜单中的。 您可以通过按`F5`或从`Start Debugging` `Debug`菜单中选择来运行该示例。

当应用启动时，您将看到一个打开的浏览器窗口，其中启动了应用程序的根目录。 您可以导航到以下 Url，以验证是否已加载所有应用程序 Url：

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

> [!Note]
> 如果收到类似`Could not find a part of the path … bin\roslyn\csc.exe`的错误，请尝试使用命令`Update-Package Microsoft.CodeDom.Providers.DotNetCompilerPlatform -r`更新该包。 有关更多详细信息，请参阅[StackOverflow 上的此问题](https://stackoverflow.com/questions/32780315)。

## <a name="host-the-sample-app"></a>承载示例应用程序

请注意，Microsoft 团队中的应用是公开一个或多个功能的 web 应用程序。 若要使团队平台加载您的应用程序，您的应用程序必须可从 internet 访问。 若要使您的应用程序可从 internet 访问，您需要托管您的应用程序。 你可以在 Microsoft Azure 中将其托管为免费，或使用`ngrok`在开发计算机上的本地进程创建隧道。 当您完成应用程序的托管时，请记下其根 URL。 它的外观如下所示`https://yourteamsapp.ngrok.io` ： `https://yourteamsapp.azurewebsites.net`或。

### <a name="tunnel-using-ngrok"></a>使用 ngrok 的隧道

若要快速测试，可以在本地计算机上运行应用程序，并通过 web 终结点创建到它的隧道。 [ngrok](https://ngrok.com)是一个免费工具，可让你做到这一点。 通过 ngrok，您可以获取诸如`https://d0ac14a5.ngrok.io` （此 URL 只是一个示例）之类的 web 地址。 您可以为您的环境[下载并安装](https://ngrok.com/download)ngrok。 请确保将其添加到中的某个位置`PATH`。

安装后，可以打开一个新的终端窗口并运行以下命令来创建隧道。 此示例使用端口3333，因此请务必在此处指定它。

```bash
ngrok http 3333 -host-header=localhost:3333
```

Ngrok 将侦听来自 internet 的请求，并将其路由到在端口3333上运行的应用。 您可以通过打开浏览器并转到`https://d0ac14a5.ngrok.io/hello`加载应用程序的 hello 页面来进行验证。 请务必使用控制台会话中由 ngrok 显示的转发地址，而不是此 URL。

> [!NOTE]
> 如果您在上面的 "[内部版本" 和 "运行](#build-and-run-the-sample)" 步骤中使用了不同的端口，请确保使用相同的`ngrok`端口号设置隧道。
> [!TIP]
> 最好在不同的终端窗口中`ngrok`运行，以使其保持运行状态，而不影响您稍后可能需要停止、重新生成和重新运行的应用程序。 该`ngrok`会话将在此窗口中返回有用的调试信息。

应用将仅在开发计算机上的当前会话过程中可用。 如果计算机关闭或进入睡眠状态，服务将不再可用。 在共享应用程序以供其他用户测试时，请记住这一点。 如果必须重新启动服务，它将返回一个新地址，并且您必须更新使用该地址的每个位置。 付费版本的 Ngrok 没有此限制。

### <a name="host-in-azure"></a>Azure 中的主机

Microsoft Azure 允许你使用共享基础结构将 .NET 应用程序托管在免费的层上。 这就足够了运行此`Hello World`示例。 有关详细信息，请参阅[创建新的免费帐户](https://azure.microsoft.com/free/)。

Visual Studio 为对不同提供程序（包括 Azure）的应用程序部署提供内置支持。

<img width="530px" src="~/assets/images/get-started/publishtoazure1.png" title="Visual Studio"/>

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-the-credentials-for-your-hosted-app"></a>更新承载的应用程序的凭据

示例应用程序需要将以下环境变量设置为您在前面记下的值。

打开 web.config 文件，并找到 " *appSettings* " 部分。 使用之前保存的你的 Bot ID 更新*MicrosoftAppId*值。 使用之前保存的 Bot 密码更新*MicrosoftAppPassword* 。

<img width="560px" src="~/assets/images/get-started/get-started-net-azure-add-keys.png" title="设置键"/>

进行这些更改后，请重新生成应用程序。 如果您使用的是 ngrok，请在本地运行应用程序，如果您是在 Azure 中托管，请重新部署应用程序。

## <a name="configure-the-app-tab"></a>配置 "应用程序" 选项卡

将应用程序安装到团队后，需要将其配置为显示内容。 转到安装了示例应用程序的团队中的某个频道，然后单击 **"+"** 按钮以添加新的选项卡。然后，可以从`Hello World` "**添加选项卡**" 列表中进行选择。 随后将显示配置对话框。 此对话框将允许您选择要在此通道中显示的选项卡。 选择选项卡并单击 "打开`Save` " 后，即可看到使用`Hello World`所选的选项卡加载的选项卡。

<img width="530px" src="~/assets/images/samples-hello-world-tab-configure.png" title="配置的屏幕截图" />

### <a name="test-your-bot-in-teams"></a>在团队中测试你的 bot

现在可以与团队中的 bot 进行交互。 选择您在其中注册应用程序的团队中的频道，然后`@your-bot-name`键入。 这称为 " ** \@提及**"。 发送到 bot 的任何邮件都将作为答复发送回您。

<img width="450px" title="Bot 响应" src="~/assets/images/samples-hello-world-bot.png" />

### <a name="test-your-messaging-extension"></a>测试消息扩展

若要测试您的邮件扩展插件，可以单击对话视图中输入框下的三个点。 将弹出一个菜单，其中包含 **"Hello World"** 应用。 当您单击它时，您将看到一组随机文本显示。 您可以选择其中的任何一个，并将其插入到对话中。

<img width="530px" title="邮件扩展菜单" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="530px" title="邮件扩展结果" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

选择一种随机文本，您将看到一张卡片的格式并准备好在底部使用您自己的消息进行发送。

<img width="530px" title="邮件扩展发送" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
