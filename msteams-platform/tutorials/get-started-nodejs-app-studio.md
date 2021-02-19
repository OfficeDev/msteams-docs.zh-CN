---
title: 教程 - 使用工具创建第一Node.js
description: 了解如何开始构建 Microsoft Teams 应用Node.js。
keywords: nodejs app Studio node.js入门
ms.topic: tutorial
ms.custom: scenarios:getting-started; languages:JavaScript,Node.js
ms.openlocfilehash: 61be1056a07952c6cf166dbe183fa257ceaf7227
ms.sourcegitcommit: 6ff8d1244ac386641ebf9401804b8df3854b02dc
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/18/2021
ms.locfileid: "50294759"
---
# <a name="create-your-first-microsoft-teams-app-using-nodejs"></a>使用应用创建你的第一个 Microsoft Teams Node.js

本教程可帮助你开始使用 Node.js 创建 Microsoft Teams 应用。

[!include [prepare your environment](~/includes/prepare-environment.md)]

<a name="DownloadAndHost"></a>

## <a name="download-and-host-your-app"></a>下载和托管应用

按照以下步骤在 Teams 中下载并托管简单的"hello world"应用。

<a name="GetPrerequisites"></a>

### <a name="get-prerequisites"></a>获取先决条件

若要完成本教程，您需要以下工具。 如果尚未安装它们，可以从这些链接安装它们。

- [Git](https://git-scm.com/downloads)
- [Node.js和 NPM](https://nodejs.org/)
- 获取任何文本编辑器或 IDE。 你可以免费安装和Visual Studio [代码](https://code.visualstudio.com/download) 。

如果在安装过程中看到用于添加 、、和 PATH 的选项， `git` `node` `npm` `code` 请选择这样做。 它很方便。

在终端窗口中运行以下代码，验证这些工具是否可用：

> [!NOTE]
> 使用你在平台上最习惯的终端窗口。 这些示例使用 Git (中包含的 Bash) ，但这些脚本将在大多数平台上运行。

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

这些应用程序可能具有不同的版本。 这应该不是问题，但 gulp 除外。 对于 gulp，你将需要使用版本 4.0.0 或更高版本。

如果未在终端窗口中安装 gulp (或安装了错误的) ，则现在通过运行终端 `npm install gulp` 窗口来这样做。

如果已安装Visual Studio代码，可以通过运行以下代码验证安装：

```bash
code --version
1.28.2
929bacba01ef658b873545e26034d1a8067445e9
```

你可以继续使用此终端窗口运行本教程中遵循的命令。

<a name="DownloadSample"></a>

### <a name="download-the-sample"></a>下载示例

我们提供了一个简单的 [Hello， World！](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-hello-world/nodejs) 示例，以开始使用。 在终端窗口中，运行以下命令将示例存储库克隆到本地计算机：

```bash
git clone https://github.com/OfficeDev/Microsoft-Teams-Samples.git
```

> [!TIP]
> 如果要[修改并](https://help.github.com/articles/fork-a-repo/)签入对[](https://github.com/OfficeDev/Microsoft-Teams-Samples)GitHub 存储库的更改，可以分叉此存储库，供将来参考。

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

当 hello-world 应用启动时，它会显示 `App started listening on port 3333` 在终端窗口中。

> [!NOTE]
> 如果看到上述消息中显示的端口号不同，这是因为您设置了一个 PORT 环境变量。 您可以继续使用该端口，也可以将环境变量更改为 3333。

此时，你可以打开浏览器窗口并导航到以下 URL 以验证所有应用 URL 是否正在加载：

- [http://localhost:3333](http://localhost:3333)
- [http://localhost:3333/hello](http://localhost:3333/hello)
- [http://localhost:3333/first](http://localhost:3333/first)
- [http://localhost:3333/second](http://localhost:3333/second)

<a name="HostSample"></a>

### <a name="host-the-sample-app"></a>托管示例应用

请记住，Microsoft Teams 中的应用是公开一个或多个功能的 Web 应用程序。 若要使 Teams 平台加载你的应用，必须从 Internet 访问你的应用。 若要使应用从 Internet 访问，你需要 *托管* 你的应用。

对于本地测试，可以在本地计算机上运行应用，并创建一个使用 Web 终结点的隧道。 [ngrok](https://ngrok.com) 是一款免费工具，允许你执行这一操作。 通过 *ngrok，* 您可以获取 Web 地址，例如 (`https://d0ac14a5.ngrok.io` 此 URL 只是一个) 。 您可以 [为环境下载](https://ngrok.com/download)*并安装 ngrok。* 请确保将其添加到您的位置 `PATH` 。

安装后，可以打开一个新的终端窗口并运行以下命令以创建隧道。 此示例使用端口 3333，因此请务必在此处指定它。

```bash
ngrok http 3333 -host-header=localhost:3333
```

*Ngrok* 将侦听来自 Internet 的请求，并路由到在端口 3333 上运行的应用。 可以通过打开浏览器并加载应用的 Hello 页面 `https://d0ac14a5.ngrok.io/hello` 进行验证。 请务必使用 *ngrok* 在控制台会话中显示的转发地址，而不是此 URL。

> [!NOTE]
> 如果在以上构建和运行步骤中使用不同的端口 [](#build-and-run-the-sample)，请确保使用相同的端口号来设置 *ngrok* 隧道。
> [!TIP]
> 建议在不同的终端窗口中运行 *ngrok* 以保持其运行，而不会干扰节点应用，稍后可能需要停止、重新生成和重新运行。 *ngrok* 会话将在此窗口中返回有用的调试信息。

存在允许永久名称 *的付费版本的 ngrok。* 如果你使用免费版本，你的应用将仅在开发计算机上当前会话期间可用。 如果计算机已关闭或进入睡眠状态，服务将不再可用。 在共享应用供其他用户进行测试时，请记住这一点。 如果必须重新启动服务，它将返回一个新地址，并且必须更新使用该地址的每个位置。

请记住，记下应用的 URL，因为稍后使用 App studio 向 Teams 注册应用时将需要此 URL。 记事本可以正常使用。

<a name="DeployToTeams"></a>

## <a name="deploy-your-app-to-microsoft-teams"></a>将应用部署到 Microsoft Teams

此时，你拥有一个在 Internet 上托管的应用，但尚无法告知 Teams 在哪里查找它，甚至无法告知你应用被叫什么。 为此，你现在必须创建应用包。 这不仅仅是一个文本文件，其中包含应用清单和一些 Teams 客户端用于正确显示和标记应用的图标。 你可以手动创建此应用包，或者可以使用 App Studio，这是在 Teams 中运行的工具，可简化注册应用的过程。 App Studio 是建议创建和更新应用包的方法。

对于任一方法，你都需要以下各项：

- 可在 Internet 上找到应用的 URL。
- Teams 用于打造应用品牌的图标。 该示例附带位于"src\static\images"中的占位符图标。 如果需要，App Studio 还将提供默认图标。

[!include[Use App Studio to configure the app package](~/includes/get-started/get-started-use-app-studio.md)]

## <a name="update-your-hosted-app"></a>更新托管的应用

示例应用需要将以下环境变量设置为之前记下的值。

```
MICROSOFT_APP_ID=<YOUR BOT'S APP ID>
MICROSOFT_APP_PASSWORD=<YOUR BOT'S PASSWORD>
WEBSITE_NODE_DEFAULT_VERSION=8.9.4
```

具体操作方式因应用托管方式不同而不同。 使用环境变量的一个重要内容是，这些值是环境的一部分，你的应用的代码可以访问这些值，但它们不会向可能检查网站文件的第三方公开。

如果使用 ngrok 运行应用，则需要设置一些本地环境变量。 执行此操作的方法有很多，但如果使用的是 Visual Studio 代码，最简单的方法是添加启动 [配置](https://code.visualstudio.com/Docs/editor/debugging#_launch-configurations)：

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

MICROSOFT_APP_ID自动MICROSOFT_APP_PASSWORD的 ID 和密码。
NODE_DEBUG代码调试控制台中的自动程序Visual Studio发生的情况。
NODE_CONFIG_DIR指向存储库 (根目录，当应用在本地运行时，它将在 src 文件夹的) 中查找它。

> [!Note]
> 如果你尚未从本教程的前面部分停止 npm，则需要运行Visual Studio代码正确拾取启动配置 `npm stop` 变量。

<a name="ConfigureTheAppTab"></a>

## <a name="configure-the-app-tab"></a>配置应用选项卡

将应用安装到团队后，你需要将其配置为显示内容。 转到团队中的频道，然后单击 **"+"** 按钮以添加新选项卡。然后，可以从 `Hello World` "添加选项卡 **"列表中选择** 。 然后，将显示配置对话框。 此对话框将让你选择要在此通道中显示哪个选项卡。 选择选项卡并单击后 `Save` ，可以看到选项卡已 `Hello World` 加载，且已选择选项卡。

<img width="430px" alt="Screenshot of configure" src="~/assets/images/samples-hello-world-tab-configure.png"/>

### <a name="test-your-bot-in-teams"></a>在 Teams 中测试机器人

你现在可以在 Teams 中与机器人交互。 选择你注册应用的团队中的频道，然后键入 `@your-bot-name` ，然后键入消息。 这称为 **\@ 提及**。 发送到自动程序的任何邮件都将作为回复发送回。

<img width="450px" alt="Bot responses" src="~/assets/images/samples-hello-world-bot.png"/>

<a name="ComposeRichMessages"></a>

### <a name="test-your-messaging-extension"></a>测试邮件扩展

若要测试消息扩展，可以单击对话视图中输入框下方的三个点。 菜单将弹出，并包含 **"Hello World"** 应用。 单击它时，你将看到大量随机文本。 你可以选择其中任何一个，并将其插入到对话中。

<img width="430px" alt="Messaging extension menu" src="~/assets/images/samples-hello-world-messaging-extensions-menu.png" />

<img width="430px" alt="Messaging extension result" src="~/assets/images/samples-hello-world-messaging-extensions-result.png" />

选择其中一个随机文本，你将在底部看到一张格式化卡片，并准备好随自己的邮件一起发送。

<img width="430px" alt="Messaging extension send" src="~/assets/images/samples-hello-world-messaging-extensions-send.png" />
