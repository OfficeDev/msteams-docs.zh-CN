---
title: 开始使用应用程序 Studio 和 node.js
description: 使用 node.js 和应用程序 Studio 开始在 Microsoft 团队中构建出色的应用程序
keywords: 入门 node.js nodejs 应用程序 Studio
ms.date: 11/09/2018
ms.topic: tutorial
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 92fbbdd30e9cdaf54644b42bf642ca5825bcec51
ms.sourcegitcommit: b13b38a104946c32cd5245a7af706070e534927d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/28/2020
ms.locfileid: "43034048"
---
# <a name="get-started-on-the-microsoft-teams-platform-with-nodejs-and-app-studio"></a>使用 node.js 和应用程序 Studio 在 Microsoft 团队平台上开始

[Microsoft 团队](/microsoftteams/)开发人员平台使您能够轻松扩展团队并将自己的应用程序和服务与团队工作区无缝集成。 然后，可以将这些应用分发到企业或世界各地的团队。

若要扩展 Microsoft 团队，您需要创建 Microsoft 团队应用程序。 Microsoft 团队应用程序是您承载的 web 应用程序。 然后，可以将此应用集成到团队中的用户工作区中。

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a>下载并托管你的应用程序

按照以下步骤在团队中下载并托管一个简单的 "hello world" 应用。

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a>获取先决条件

若要完成本教程，您需要以下工具。 如果尚不具备这些链接，可以从这些链接进行安装。

- [Git](https://git-scm.com/downloads)
- [Node.js 和 NPM](https://nodejs.org/)
- 获取任何文本编辑器或 IDE。 您可以免费安装和使用[Visual Studio Code](https://code.visualstudio.com/download) 。

如果您在安装过程中`git`看到`node`要`npm`向路径`code`添加、、和的选项，请选择执行此操作。 这将很方便。

在终端窗口中运行以下命令，验证这些工具是否可用：

> [!NOTE]
> 在你的平台上使用你最舒适的终端窗口。 这些示例使用 Bash （包含在 Git 中），但这些脚本将在大多数平台上运行。

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 4.0.2
```

您可能具有这些应用程序的不同版本。 这不应是问题，gulp 除外。 对于 gulp，你将需要使用版本4.0.0 或更高版本。

如果未安装 gulp （或安装了错误的版本），请立即通过在终端窗口中`npm install gulp`运行来执行此操作。

如果已安装 Visual Studio Code，可以通过运行以下命令来验证安装：

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

您可以继续使用此终端窗口运行本教程后面的命令。

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a>下载示例

我们提供了一个简单的[Hello，World！](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs) 入门示例。 在终端窗口中，运行以下命令以将示例存储库克隆到本地计算机：

```bash
git clone https://github.com/OfficeDev/msteams-samples-hello-world-nodejs.git
```

> [!TIP]
> [如果要](https://github.com/OfficeDev/msteams-samples-hello-world-nodejs)修改和签入 GitHub 存储库的更改，以供将来参考，可以[派生](https://help.github.com/articles/fork-a-repo/)此存储库。

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a>生成和运行示例

克隆存储库后，转到包含示例的目录：

```bash
cd msteams-samples-hello-world-nodejs
```

为了生成示例，您需要安装其所有依赖项。 运行以下命令来执行此操作：

```bash
npm install
```

您应该会看到一组已安装的依赖项。 完成后，您可以运行应用程序：

```bash
npm start
```

当 hello world 应用程序启动时，它将`App started listening on port 3333`显示在终端窗口中。

> [!NOTE]
> 如果您看到上面的消息中显示了不同的端口号，则是因为您有一个端口环境变量集。 您可以继续使用该端口或将环境变量更改为3333。

此时，您可以打开浏览器窗口并导航到以下 Url，以验证是否已加载所有应用程序 Url：

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a>承载示例应用程序

请注意，Microsoft 团队中的应用是公开一个或多个功能的 web 应用程序。 若要使团队平台加载您的应用程序，您的应用程序必须可从 internet 访问。 若要使您的应用程序可从 internet 访问，您需要*托管*您的应用程序。

对于本地测试，可以在本地计算机上运行应用程序，并使用 web 终结点创建与之的隧道。 [ngrok](https://ngrok.com)是一个免费工具，可让你做到这一点。 通过*ngrok* ，您可以获取诸如`https://d0ac14a5.ngrok.io` （此 URL 只是一个示例）之类的 web 地址。 您可以为您的环境[下载并安装](https://ngrok.com/download) *ngrok* 。 请确保将其添加到中的某个位置`PATH`。

安装后，可以打开一个新的终端窗口并运行以下命令来创建隧道。 此示例使用端口3333，因此请务必在此处指定它。

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok*将侦听来自 internet 的请求，并将其路由到在端口3333上运行的应用。 您可以通过打开浏览器并转到`https://d0ac14a5.ngrok.io/hello`加载应用程序的 hello 页面来进行验证。 请务必使用控制台会话中由*ngrok*显示的转发地址，而不是此 URL。

> [!NOTE]
> 如果您在上面的 "[内部版本" 和 "运行](#build-and-run-the-sample)" 步骤中使用了不同的端口，请确保使用相同的端口号设置*ngrok*隧道。
> [!TIP]
> 最好在不同的终端窗口中运行*ngrok* ，使其保持运行状态，而不会干扰您稍后可能需要停止、重新生成和重新运行的节点应用。 *Ngrok*会话将在此窗口中返回有用的调试信息。

有*ngrok*的付费版本允许使用永久名称。 如果您使用的是免费版本，应用程序将仅在开发计算机上的当前会话过程中可用。 如果计算机关闭或进入睡眠状态，服务将不再可用。 在共享应用程序以供其他用户测试时，请记住这一点。 如果必须重新启动服务，它将返回一个新地址，并且您必须更新使用该地址的每个位置。

请记住，请记下你的应用程序的 URL，因为你稍后在使用应用程序 studio 向团队注册应用时将需要这样做。 为了实现此目的，记事本工作正常。

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>将应用程序部署到 Microsoft 团队

此时，您有一个托管在 internet 上的应用程序，但您还没有办法告诉团队在哪里查找它，甚至您的应用程序已被调用。 若要执行此操作，您现在必须创建一个应用程序包。 这只是一个文本文件，其中包含应用程序清单和一些图标，团队客户端将使用这些图标来正确地显示应用程序并为其打造品牌。 您可以手动创建此应用程序包，也可以使用应用程序工作室（在将简化应用程序注册过程的团队中运行的工具）。 应用程序使用 Studio 是创建和更新应用程序包的推荐方法。

对于这两种方法，您都需要以下各项：

- 在 internet 上可以找到你的应用程序的 URL。
- 团队将用来为你的应用程序建立品牌的图标。 示例附带了位于 "src\static\images." 中的占位符图标。 如果需要，应用程序 Studio 还将提供默认图标。

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a>更新承载的应用程序

示例应用程序需要将以下环境变量设置为您在前面记下的值。

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

执行此操作的方式取决于您的应用程序的承载方式。 使用环境变量的重要一点是，这些值是环境的一部分-可以通过应用程序的代码来访问它们，但它们不会向可能检查构成网站的文件的第三方公开。

如果您正在使用 ngrok 运行应用程序，则需要设置一些本地环境变量。 有多种方法可以实现此目的，但如果您使用 Visual Studio Code，最简单的方法是添加[启动配置](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)：

``` 
{
    "type": "node",
    "request": "launch",
    "name": "Launch - Teams Debug",
    "program": "${workspaceRoot}/src/app.js",
    "cwd": "${workspaceFolder}/src",
    "env": {
        "BASE_URI": "https://yourNgrokURL.ngrok.io",
        "MICROSOFT_APP_ID": "00000000-0000-0000-0000-000000000000",
        "MICROSOFT_APP_PASSWORD": "yourBotAppPassword",
        "NODE_DEBUG": "botbuilder",
        "SUPPRESS_NO_CONFIG_WARNING": "y",
        "NODE_CONFIG_DIR": "../config"
    }
}
```

其中：

MICROSOFT_APP_ID 和 MICROSOFT_APP_PASSWORD 分别是您的 bot 的 ID 和密码。
NODE_DEBUG 将在 Visual Studio Code 调试控制台中显示你的 bot 中发生的情况。
NODE_CONFIG_DIR 指向存储库根目录处的目录（默认情况下，当应用程序在本地运行时，它会在 src 文件夹中查找它）。

> [!Note]
> 如果您在本教程的前面部分没有停止 npm，则需要运行`npm stop` Visual Studio 代码，以便正确地拾取您的启动配置变量。

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>配置 "应用程序" 选项卡

将应用程序安装到团队后，需要将其配置为显示内容。 转到团队中的频道并单击 **"+"** 按钮以添加新的选项卡。然后，可以从`Hello World` "**添加选项卡**" 列表中进行选择。 随后将显示配置对话框。 此对话框将允许您选择要在此通道中显示的选项卡。 选择选项卡并单击 "" `Save`时，可以看到在`Hello World`所选的选项卡上加载的选项卡。

<img width="430px" src="~/assets/images/samples-hello-world-tab-configure.png" title="配置的屏幕截图" />

### <a name="test-your-bot-in-teams"></a>在团队中测试你的 bot

现在可以与团队中的 bot 进行交互。 选择您在其中注册应用程序的团队中的频道，然后`@your-bot-name`键入，然后键入您的消息。 这称为 " ** \@提及**"。 发送到 bot 的任何邮件都将作为答复发送回您。

<img width="450px" title="Bot 响应" src="~/assets/images/samples-hello-world-bot.png" />

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>测试消息扩展

若要测试您的邮件扩展插件，可以单击对话视图中输入框下的三个点。 将弹出一个菜单，其中包含 **"Hello World"** 应用。 当您单击它时，您将看到大量随机文本。 您可以选择其中的任何一个，并将其插入到对话中。

<img width="430px" title="邮件扩展菜单" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" title="邮件扩展结果" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

选择一种随机文本，您将看到一张卡片的格式并准备好在底部使用您自己的消息进行发送。

<img width="430px" title="邮件扩展发送" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
