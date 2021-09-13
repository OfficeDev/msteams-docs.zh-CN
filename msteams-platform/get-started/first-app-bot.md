---
title: 入门 - 构建你的第一个对话机器人
author: adrianhall
description: 使用 Teams 工具包为 Microsoft Teams 创建对话机器人。
ms.author: adhal
ms.date: 05/27/2021
ms.topic: quickstart
ms.localizationpriority: none
ms.openlocfilehash: f9f35f5b4e639c6568ad3c1eccfc750d3bd9b853
ms.sourcegitcommit: fc9f906ea1316028d85b41959980b81f2c23ef2f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/12/2021
ms.locfileid: "59155799"
---
# <a name="build-your-first-conversational-bot-for-microsoft-teams"></a>构建你的第一个 Microsoft Teams 对话机器人

在本教程中，你将了解如何构建、运行和部署 Teams 机器人应用。 机器人是 Teams 用户和 Web 服务之间的中介。 用户可以与机器人聊天，以快速获取信息、启动工作流或启动 Web 服务能够执行的任何操作。 

> [!IMPORTANT]
> 目前，自动程序在 政府社区云 (GCC) 中可用，但在 doD GCC-High 和国防部 (中) 。

## <a name="before-you-begin"></a>开始之前

通过安装先决条件确保已设置开发环境。

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)

## <a name="create-your-project"></a>创建项目

使用 Teams 工具包创建你的第一个项目:

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. 打开 Visual Studio Code。
1. 选择边Teams图标以打开Teams Toolkit。

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code 边栏中的 Teams 图标。":::

1. 选择 **创建新项目**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. 选择 **创建新的 Teams 应用**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="&quot;创建新项目&quot;的向导启动":::

1. 在"**选择功能"** 部分，选择"**自动** 程序"，取消选择 **"选项卡**"，然后选择"确定 **"。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-capabilities-bot.png" alt-text="显示如何向新应用添加功能的屏幕截图。":::

1. 在"**自动程序注册"** 部分，**选择"创建新的自动程序注册"。**

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="选择创建新的机器人注册":::

1. 在"**编程语言"部分**，选择 **"JavaScript"。**

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="显示如何选择编程语言的屏幕截图。":::

1. 选择工作区文件夹。  将在工作区文件夹中为正在创建的项目创建一个文件夹。

1. 为应用输入合适的名称，如 `helloworld`。  应用的名称必须仅包含字母数字字符。  按 **Enter** 以继续。

将在数秒钟内创建你的 Teams 应用。

# <a name="command-line"></a>[命令行](#tab/cli)

使用 `teamsfx` CLI 创建你的第一个项目。  从要创建项目文件夹的文件夹开始。

``` bash
teamsfx new
```

CLI 会提出一些问题来引导创建项目。  每个问题将告诉你该如何回答（例如，使用箭头键选择一个选项）。  如果已回答问题，请通过按 **Enter** 确认。

1. 选择 **创建新的 Teams 应用**。
1. 选择 **自动程序** ，然后取消选择 **选项卡**。
1. 选择 **创建新的机器人注册**。
1. 选择 **JavaScript** 作为编程语言。
1. 按 **Enter** 选择默认工作区文件夹。
1. 为应用输入合适的名称，如 `helloworld`。  应用的名称只能包含字母数字字符。

在回答所有问题后，将创建项目。

---

## <a name="take-a-tour-of-the-source-code"></a>浏览源代码

若要暂时跳过此部分，可以 [在本地运行应用](#run-your-app-locally)。

消息扩展使用 [Bot Framework](https://docs.botframework.com) 以允许用户通过对话与你的服务交互。  设置标点文件夹后，你的项目将如下所示:

:::image type="content" source="../assets/images/teams-toolkit-v2/bot-file-layout.png" alt-text="机器人项目的文件布局。":::

机器人程序代码存储在 `bot` 文件夹中。  `bot/teamsBot.js` 是机器人的主入口点，对话将存储在 `dialogs` 文件夹中。

> [!Tip]
> 在将第一个机器人集成到 Teams 中之前，请熟悉 Teams 以外的机器人。  可以通过查看 [Azure 机器人服务](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)教程找到有关机器人的更多信息。

## <a name="run-your-app-locally"></a>在本地运行应用

Teams 工具包允许你在本地托管应用。  为此，请执行以下操作:

- Azure Active Directory 应用程序是在 M365 租户中注册的。
- 向 Teams 开发人员中心提交应用清单。
- 在本地使用 Azure Functions Core Tools 运行 API，以支持你的应用。
- [ngrok](https://ngrok.io) 安装并用于在 Teams 和机器人代码之间提供一个隧道。

若要在本地构建并运行应用程序:

1. 在Visual Studio Code中，按 **F5** 键以在调试模式下运行应用程序。

   > 首次运行该应用时，将下载所有依赖项并编译该应用。  编译完成后，将自动打开浏览器窗口。  这可能需要 3-5 分钟才能完成。

1. Web 浏览器开始运行该应用。 如果系统提示打开Teams，请选择 **"取消**"以保留在浏览器中。 系统也可能提示你在其他时间切换到Teams桌面;选择Teams Web 应用。

   :::image type="content" source="../assets/images/teams-toolkit-v2/launch-web-browser-and-pick-webapp.png" alt-text="显示启动后如何选择 Teams 的 Web 版本的屏幕截图":::

1. 系统可能会提示你登录。  如果是这样，则使用你的 M365 帐户登录。
1. 当系统提示将应用安装到 Teams，选择"添加 **"。**

   加载应用后，你将直接进入与机器人的聊天会话。  你可以键入 `intro` 以显示简介卡，键入 `show` 以显示你在 Microsoft Graph 中的详细信息。  (这需要额外审批权限)。

   调试工作如你通常预期一样 - 自己试一试！ 打开 `bot/dialogs/rootDialog.js` 文件并找到 `triggerCommand(...)` 方法。  为默认情况设置断点。  然后键入一些文本。

<!-- markdownlint-disable MD033 -->
<details>
<summary>在本地调试器中运行应用时，了解会发生什么情况。</summary>

按 **F5 键** 时，Teams Toolkit：

1. 向应用程序注册Azure Active Directory。
1. 将应用程序注册为"旁加载"Microsoft Teams。
1. 使用 Azure 函数核心工具 启动本地 [运行的应用程序后端](/azure/azure-functions/functions-run-local?#start)。
1. 启动 ngrok 隧道，Teams应用进行通信。
1. 首先Microsoft Teams命令指示Teams旁加载应用程序。

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary>了解如何在本地运行应用时解决常见问题。</summary>

若要在 Teams 中成功运行应用，必须具有允许应用程序旁加载的 Microsoft 365 开发帐户。 有关开设帐户的详细信息，请参阅 [先决条件](prerequisites.md#enable-sideloading)。

> [!IMPORTANT]
> 目前，旁加载应用在 政府社区云 (GCC) 、GCC-High 和 DOD 中可用。

> [!TIP]
> 在旁加载应用之前，使用工具包中包含的 [应用验证工具](https://dev.teams.microsoft.com/appvalidation.html) 检查问题。 修复错误以成功旁加载应用。
</details>

[!INCLUDE [Provision and Deploy your app on Azure](~/includes/get-started/azure-provisioning-instructions.md)]

<!-- markdownlint-disable MD033 -->

<details>
<summary>了解将应用部署到 Azure 时会发生的情况</summary>

部署之前，应用程序已在本地运行:

1. 后端使用 _Azure Functions Core Tools_ 运行。
1. 应用程序 HTTP 终结点 (Microsoft Teams 在此加载应用程序) 在本地运行。

   部署涉及预配活动 Azure 订阅上的资源，以及将应用程序后端和前端代码部署（上传）到 Azure。 后端使用多种 Azure 服务，包括 Azure 应用服务 和 Azure 机器人服务。

</details>

## <a name="see-also"></a>另请参阅

* [教程概述](code-samples.md) 
* [使用应用程序创建React](first-app-react.md)
* [使用 Blazor 创建应用](first-app-blazor.md)
* [使用应用程序创建SPFx](first-app-spfx.md)
* [使用或 C# .NET 创建应用](get-started-dotnet-app-studio.md)
* [使用Node.js创建应用](get-started-nodejs-app-studio.md)
* [使用 Yeoman 生成器创建应用](get-started-yeoman.md)
* [创建邮件扩展](first-message-extension.md)
* [代码示例](https://github.com/OfficeDev/Microsoft-Teams-Samples)