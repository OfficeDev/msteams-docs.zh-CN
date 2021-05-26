---
title: 入门 - 先决条件
author: adrianhall
description: 了解如何开始使用应用Microsoft Teams并设置你的环境。
ms.author: adhal
ms.date: 05/24/2021
ms.topic: quickstart
ms.openlocfilehash: 73d99f2bbbc69bf13242110a56e13e662655283c
ms.sourcegitcommit: 9cabeaed9baf96c8caeb1497f0bc37abdb787d22
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/25/2021
ms.locfileid: "52646672"
---
# <a name="prerequisites-get-started-with-microsoft-teams-app-development"></a>先决条件：开始Microsoft Teams开发

创建第一个Teams应用之前，必须安装一些工具并设置开发环境。

## <a name="install-required-tools"></a>安装所需的工具

你需要的一些工具取决于你更希望如何生成Teams应用：

- [Node.js(](https://nodejs.org/en/download/) 使用最新的 v14 LTS 版本)  
- 具有开发人员工具的浏览器 -例如[Microsoft Edge (](https://www.microsoft.com/edge)推荐) [Google Chrome](https://www.google.com/chrome/)
- 如果你使用 JavaScript、TypeScript 或 SharePoint 框架 (SPFx) 进行开发，Visual Studio Code版本 1.55 或更高版本。 [](https://code.visualstudio.com/download)  
- 如果使用 .NET 进行开发，请安装[Visual Studio 2019。](https://visualstudio.com/download)  确保安装 ASP.NET **Web 开发** 或 **.NET Core 跨平台开发** 工作负载。

> [!WARNING]
> 存在与 打包在 Node `npm@7` v15 及更高版本中的已知问题。 如果在运行时遇到问题 `npm install` ，请确保使用节点 v14 (LTS) 

## <a name="install-the-teams-toolkit"></a>安装Teams Toolkit

该Teams Toolkit使用工具来为应用预配和部署云资源、发布到 Teams 应用商店等，帮助简化开发过程。 你可以将工具包与 Visual Studio Code、Visual Studio 或作为称为 (的 CLI `teamsfx`) 。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. 打开Visual Studio Code。
1. Select the Extensions view (**Ctrl+Shift+X**  /  **⌘⇧-X** or **View > Extensions**) .
1. 在搜索框中，输入 _"Teams Toolkit"。_
1. 在屏幕旁的绿色安装按钮上选择Teams Toolkit。

您还可以在 Teams Toolkit Marketplace 上找到Visual Studio Code[应用程序](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension)。

如果需要，Visual Studio Code安装以下工具。  如果已安装，将改为使用已安装的版本。  如果使用 Linux (WSL) ，则必须先安装这些工具，然后才能使用：

- [Azure 函数核心工具](/azure/azure-functions/functions-run-local)

    Azure Functions Core Tools 用于在本地调试运行期间在本地运行任何后端组件，包括在 Azure 中运行服务时所需的身份验证帮助程序。  它使用 npm (安装在项目目录中 `devDependencies`) 。

- [.NET SDK](/dotnet/core/install/)

    .NET SDK 用于安装用于本地调试和 Azure Functions 应用部署的自定义绑定。  如果尚未全局安装 .NET 3.1 (或更高版本) SDK，将安装可移植版本。

- [ngrok](https://ngrok.com/download)

    某些Teams应用功能 (对话机器人、消息传递扩展和传入 webhook) 需要入站连接。  你需要通过隧道公开开发Teams进行开发。  仅包含选项卡的应用不需要隧道。  此包安装在项目目录中， (npm `devDependencies`) 。

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

您可以使用 Visual Studio 2019 在 .NET Teams Blazor Server 开发应用程序。  如果不打算在 .NET 中Teams应用程序，请安装 Visual Studio Code 版本的 Teams Toolkit。

若要安装 Teams Toolkit 扩展：

1. 打开Visual Studio 2019。
1. 选择 **扩展**  >  **管理扩展**。
1. 在搜索框中，输入 _"Teams Toolkit"。_
1. 选择"Teams Toolkit扩展并选择"下载 **"。**

将下载扩展。  关闭 Visual Studio 2019 以安装扩展。

# <a name="command-line"></a>[命令行](#tab/cli)

若要安装 TeamsFx CLI，请使用 `npm` 程序包管理器：

``` bash
npm install -g @microsoft/teamsfx-cli
```

根据您的配置，您可能需要使用 安装 `sudo` CLI：

``` bash
sudo npm install -g --unsafe-perm @microsoft/teamsfx-cli
```

这更常见于 Linux 和 macOS 系统。

确保将 npm 全局缓存添加到 PATH。  这通常是作为安装程序的一Node.js一部分。  

可以将 CLI 与 命令 `teamsfx` 一同使用。  通过运行 验证命令是否正常工作 `teamsfx -h` 。

> [!CAUTION]
> 在 PowerShell 终端中运行 TeamsFx 之前，你需要为 PowerShell 启用"远程签名"执行策略。  有关详细信息，请参阅 [PowerShell 文档](/powershell/module/microsoft.powershell.core/about/about_signing)。

---

## <a name="install-optional-tools"></a>安装可选工具

安装用于应用开发的浏览器工具。 例如，如果你的应用是使用React编写的，可以使用React工具：

- [ReactChrome 开发人员工具](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi)

如果你想要访问 Azure 中存储的数据或在 Azure 中为 Teams 应用部署基于云的后端，请安装以下工具：

- [Azure Tools for Visual Studio Code](https://marketplace.visualstudio.com/items?itemName=ms-vscode.vscode-node-azure-pack)
- [Azure CLI](/cli/azure/install-azure-cli)

如果你使用 Microsoft Graph数据，你应该了解 Microsoft Graph浏览器并添加书签。 此基于浏览器的工具允许你在应用Graph查询 Microsoft 帐户。

- [Microsoft Graph 浏览器](https://developer.microsoft.com/graph/graph-explorer)

借助开发人员门户Teams，你可以配置、管理和分发 Teams 应用 (包括组织或 Teams 应用商店) 。

- [开发人员门户Teams](https://dev.teams.microsoft.com/)

## <a name="enable-sideloading"></a>启用旁加载

在开发期间，你需要在应用程序内加载Teams而不分发它。  这称为"旁加载"。

1. 如果你有一个Teams帐户，请验证你能否在应用中旁加载Teams：

    1. 在客户端Teams，选择"应用 **"。**
    1. 查找用于自定义 **Upload的选项**。

    :::image type="content" source="~/assets/images/teams-toolkit-v2/upload-custom-app-closeup.png" alt-text="插图显示可以在Teams上传自定义应用。":::

> [!NOTE]
> 如果仍无法旁加载应用，请与管理员Teams联系。 有关详细信息[，请参阅Teams应用和启用自定义应用](~/concepts/build-and-test/prepare-your-o365-tenant.md#enable-custom-teams-apps-and-turn-on-custom-app-uploading)上传。

## <a name="get-a-free-teams-developer-tenant-optional"></a>获取一个Teams开发人员租户 (可选) 

如果看不到旁加载选项，或者没有 Teams 帐户，可以通过加入 M365 开发人员计划获取免费的 Teams 开发人员帐户。  注册过程大约需要两分钟。

1. 转到开发人员[Microsoft 365计划](https://developer.microsoft.com/microsoft-365/dev-program)。
1. 选择 **立即加入** 并按照屏幕上的说明进行操作。
1. 当你进入欢迎屏幕时，选择 **"设置 E5 订阅"。**
1. 设置管理员帐户。 完成后，你应该会看到如下所示的屏幕。

    :::image type="content" source="~/assets/images/build-your-first-app/dev-program-subscription.png" alt-text="注册开发人员计划后看到Microsoft 365的示例。":::

1. 使用刚Teams的管理员帐户登录登录。
1. 验证你现在是否具有Upload **应用选项**。

## <a name="get-a-free-azure-account"></a>获取免费的 Azure 帐户

如果你想要在 Azure 中托管应用或访问资源，则需要 Azure 订阅。  可以在 [开始之前创建一](https://azure.microsoft.com/free/) 个免费帐户。

## <a name="sign-in-to-your-microsoft-365-and-azure-accounts"></a>登录到你的 Microsoft 365 和 Azure 帐户

你将需要访问两个帐户：

- 你的Microsoft 365帐户凭据。 这是用于登录帐户的帐户Teams。 如果你使用的是开发人员Microsoft 365租户，这是注册该计划时设置的管理员帐户。
- - 你的 Azure 凭据。 这是用于访问 Azure 门户和预配新的云资源以支持你的应用的帐户。

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. 打开Visual Studio Code
1. 选择Teams栏中的"设置"图标：

    :::image type="content" source="~/assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Teams边栏中的Visual Studio Code图标。":::

1. 选择 **"登录 M365"。**

    :::image type="content" source="~/assets/images/teams-toolkit-v2/account-commands.png" alt-text="用于登录的&quot;帐户&quot;部分的位置。":::

1. 登录过程将开始使用正常的 Web 浏览器。  完成 M365 帐户的登录过程。  当可以关闭浏览器并返回到浏览器时，系统将Visual Studio Code。
1. 返回到Teams Toolkit中的Visual Studio Code。
1. 选择 **"登录到 Azure"。**

    > [!TIP]
    > 如果已安装 Azure 帐户扩展并使用相同的帐户，可以跳过此步骤。  将自动使用与其他扩展中相同的帐户。

1. 登录过程将开始使用正常的 Web 浏览器。  完成 Azure 帐户的登录过程。  当可以关闭浏览器并返回到浏览器时，系统将Visual Studio Code。

完成后，边栏的 **"帐户** "部分将分别显示两个帐户以及可用的 Azure 订阅数。  确保至少有一个可用的 Azure 订阅可用。  如果没有，请注销并使用其他帐户。

# <a name="visual-studio-2019"></a>[Visual Studio 2019](#tab/vs)

Visual Studio 2019 将提示您根据需要登录到每个服务。  无需提前登录 M365 和 Azure 帐户。

# <a name="command-line"></a>[命令行](#tab/cli)

1. 登录以Microsoft 365 TeamsFx CLI：

    ``` bash
    teamsfx account login m365
    ```

    登录过程将开始使用正常的 Web 浏览器。  完成 M365 帐户的登录过程。  当可以关闭浏览器时，系统将提示你。

2. 使用 TeamsFx CLI 登录 Azure：

    ``` bash
    teamsfx account login azure
    ```

    登录过程将开始使用正常的 Web 浏览器。  完成 Azure 帐户的登录过程。  当可以关闭浏览器时，系统将提示你。

帐户登录名在 Visual Studio Code TeamsFx CLI 之间共享。

---

## <a name="next-steps"></a>后续步骤

现在，你的开发环境已配置，你可以创建、生成和部署你的第一个Teams应用。

- [使用 Teams 创建你的第一个React](first-app-react.md)
- [使用 Blazor 创建Teams应用程序](first-app-blazor.md)
- [使用 Teams 创建第一个SharePoint 框架 (SPFx) ](first-app-spfx.md)
- [创建对话机器人应用](first-app-bot.md)
- [创建邮件扩展](first-message-extension.md)
