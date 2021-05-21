---
title: 教程 - 使用工具创建第一Node.js
description: 了解如何开始使用 Microsoft Teams 生成Node.js。
keywords: nodejs app Studio node.js入门
ms.topic: tutorial
localization_priority: Normal
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 46272671443e07432513b667af424b5c5be05f2e
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566536"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a>使用 Microsoft Teams 创建你的第一个Node.js

本教程帮助你开始使用 Microsoft Teams 创建Node.js。

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a>下载和托管应用

按照以下步骤在应用程序下载并托管简单的"hello world"Teams。

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a>获取先决条件

若要完成本教程，你需要以下工具。 如果尚未安装，可以通过这些链接进行安装。

- [Git](https://git-scm.com/downloads)
- [Node.js 和 NPM](https://nodejs.org/)
- 获取任何文本编辑器或 IDE。 你可以免费安装和[Visual Studio Code](https://code.visualstudio.com/download)应用程序。

如果在安装过程中看到向 `git` PATH 添加 、、 和 `node` `npm` `code` 的选项，请选择这样做。 它很方便。

在终端窗口中运行以下代码，验证这些工具是否可用：

> [!NOTE]
> 使用你最熟悉平台的终端窗口。 这些示例使用 Git (中包含的 Bash) ，但这些脚本将在大多数平台上运行。

```bash
$ git --version
git version 2.19.0.windows.1

$ node -v
v8.9.3

$ npm -v
5.5.1

$ gulp -v
CLI version 2.3.0
Local version 4.0.2
```

这些应用程序可能具有不同的版本。 这应该不是问题，但 gulp 除外。 对于 gulp，你需要使用版本 4.0.0 或更高版本。

如果没有在终端窗口中安装 gulp (或安装的版本) ，现在在终端窗口中 `npm install gulp` 运行。

如果已安装Visual Studio Code，可以运行以下代码验证安装：

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

你可以继续使用此终端窗口运行本教程中遵循的命令。

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a>下载示例

我们提供了简单的 [Hello， World！](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs) 示例，以开始。 在终端窗口中，运行以下命令将示例存储库克隆到本地计算机：

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> 如果要[修改和](https://help.github.com/articles/fork-a-repo/)[签入对](https://github.com/OfficeDev/Microsoft-Teams-Samples)存储库所做的更改，可以分叉此存储库GitHub供将来参考。

<a name="BuildRun"></a>

### <a name="build-and-run-the-sample"></a>生成和运行示例

克隆存储库后，请更改为包含示例的目录：

```bash
cd Microsoft-Teams-Samples/samples/app-hello-world/nodejs/
```

为了生成示例，需要安装其所有依赖项。 为此，运行以下命令：

```bash
npm install
```

你应该会看到一组依赖项正在安装。 完成后，你可以运行应用：

```bash
npm start
```

当 Hello-world 应用启动时，它显示在 `App started listening on port 3333` 终端窗口中。

> [!NOTE]
> 如果看到上述消息中显示的端口号不同，这是因为您设置了一个 PORT 环境变量。 您可以继续使用该端口，也可以将环境变量更改为 3333。

此时，你可以打开浏览器窗口并导航到以下 URL 以验证所有应用 URL 是否正在加载：

- `http://localhost:3333`
- `http://localhost:3333/hello`
- `http://localhost:3333/first`
- `http://localhost:3333/second`

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a>托管示例应用

请记住，Microsoft Teams应用程序是公开一个或多个功能的 Web 应用程序。 若要Teams加载应用，应用必须从 Internet 访问。 若要使你的应用从 Internet 上访问，你需要 *托管* 你的应用。

对于本地测试，可以在本地计算机上运行应用，并创建一个使用 Web 终结点的隧道。 [ngrok](https://ngrok.com) 是一款免费工具，允许你这样做。 使用 *ngrok，* 你可以获取 Web 地址 `https://d0ac14a5.ngrok.io` ， (此 URL 只是一个) 。 你可以 [为环境下载](https://ngrok.com/download)*并安装 ngrok。* 请确保将其添加到 中的位置 `PATH` 。

安装后，可以打开一个新的终端窗口并运行以下命令以创建隧道。 此示例使用端口 3333，因此请务必在此处指定它：

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok* 将侦听来自 Internet 的请求，并将它们路由到在端口 3333 上运行的应用。 你可以打开浏览器并加载应用的 Hello 页面 `https://d0ac14a5.ngrok.io/hello` 来进行验证。 请务必使用 *ngrok* 在控制台会话中显示的转发地址，而不是此 URL。

> [!NOTE]
> 如果在以上构建和运行步骤中使用不同的端口 [](#build-and-run-the-sample)，请确保使用相同的端口号来设置 *ngrok* 隧道。
> [!TIP]
> 建议在不同的终端窗口中运行 *ngrok* 以保持其运行，而不会影响节点应用，稍后您可能必须停止、重新生成和重新运行节点应用。 *ngrok* 会话将在此窗口中返回有用的调试信息。

存在允许永久名称的 *ngrok* 付费版本。 如果你使用免费版本，你的应用将仅在开发计算机上当前会话期间可用。 如果计算机关闭或进入睡眠状态，服务将不再可用。 在共享应用供其他用户进行测试时，请记住这一点。 如果必须重新启动服务，它将返回一个新地址，并且必须更新使用该地址的每一处地址。

请记住，记下应用的 URL，因为稍后在使用 App studio 向应用注册Teams时将需要此 URL。 记事本适合此目的。

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>将应用部署到Microsoft Teams

此时，你拥有一个在 Internet 上托管的应用，但你尚无法告知Teams在哪里查找它，甚至告诉用户你的应用被调用了什么。 为此，现在必须创建应用包。 这不仅仅是一个包含应用清单和一些图标的文本文件，Teams客户端将使用这些图标来正确显示你的应用并打造你的应用品牌。 你可以手动创建此应用包，或者可以使用 App Studio，这是一个在 Teams 中运行的工具，可简化注册应用的过程。 App Studio 是建议创建和更新应用包的方法。

对于任一方法，你都需要：

- 可以在 Internet 上找到应用的 URL。
- 用于Teams应用品牌的图标。 此示例附带位于"src\static\images"中的占位符图标。 App Studio 还会根据需要提供默认图标。

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a>更新托管的应用

示例应用需要将以下环境变量设置为之前记下的值：

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

具体操作方式因应用托管方式不同而不同。 使用环境变量的一个重要内容是，这些值是环境的一部分，可通过应用的代码访问它们，但它们不会向可能检查网站文件的第三方公开。

如果使用 ngrok 运行应用，则需要设置一些本地环境变量。 执行此操作的方法有很多，但如果使用的是Visual Studio Code，最简单的方法是添加启动[配置](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)：

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

MICROSOFT_APP_ID和MICROSOFT_APP_PASSWORD是自动程序 ID 和密码。
NODE_DEBUG将在调试控制台中显示自动程序Visual Studio Code发生了什么。
NODE_CONFIG_DIR指向存储库根目录（默认情况下 (，当本地运行应用时，它将在 src 文件夹的) 。

> [!Note]
> 如果你尚未从本教程的前面部分停止 npm，则需要运行 ，以便Visual Studio Code正确拾取启动配置 `npm stop` 变量。

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>配置"应用"选项卡

将应用安装到团队后，你需要将其配置为显示内容。 转到团队中的频道，然后单击 **"+"** 按钮以添加新选项卡。然后，可以从 `Hello World` "添加 **选项卡"列表中选择** 。 然后，你将看到配置对话框。 此对话框将让你选择要在此通道中显示哪个选项卡。 选择该选项卡并单击后，可以看到已加载选项卡 `Save` `Hello World` 的选项卡已选择：

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a>在设备中测试Teams

现在，你可以与自动程序在 Teams。 选择你注册应用的团队中的频道，然后键入 `@your-bot-name` ，然后键入消息。 这称为 **\@ 提及**。 发送到自动程序的任何消息都将作为回复发送回：

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>测试邮件扩展

若要测试消息扩展，可以单击对话视图中输入框下方的三个点。 菜单将弹出，并包含 **"Hello World"** 应用。 单击它时，你将看到大量随机文本。 可以选择其中任何一个，并将其插入到对话中：

<img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

选择随机文本之一，你将在底部看到格式化的卡片，并准备好发送自己的邮件：

<img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
