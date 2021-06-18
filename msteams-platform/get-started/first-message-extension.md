---
title: 开始 - 构建第一个邮件扩展
author: adrianhall
description: 使用 Teams 工具包为 Microsoft Teams 创建邮件扩展。
ms.author: adhal
ms.date: 05/20/2021
ms.topic: quickstart
ms.openlocfilehash: bf00897beec92c64fe9dd68ca76e35751b3c7aed
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994201"
---
# <a name="build-and-run-your-first-messaging-extension-for-microsoft-teams"></a>构建并运行 Microsoft Teams 的第一个消息传递扩展

有两种类型的 Teams **消息扩展**：

- [搜索命令](../messaging-extensions/how-to/search-commands/define-search-command.md)允许您搜索外部系统并将搜索结果以卡片的形式插入到消息中。
- [动作命令](../messaging-extensions/how-to/action-commands/define-action-command.md)允许为用户提供一个模式弹出式窗口来收集或显示信息，然后处理他们的互动并将信息发送回 Teams。

在本教程中，您将创建一 *搜索命令* 搜索外部数据并将结果插入邮件。  

## <a name="before-you-begin"></a>准备工作

通过安装[先决条件](prerequisites.md)确保你的开发环境已设置

> [!div class="nextstepaction"]
> [安装先决条件](prerequisites.md)

## <a name="create-your-project"></a>创建项目

使用 Teams 工具包创建你的第一个项目:

# <a name="visual-studio-code"></a>[Visual Studio Code](#tab/vscode)

1. 打开 Visual Studio 代码。
1. 选择边栏中的"团队"图标打开 Teams 工具包：

    :::image type="content" source="../assets/images/teams-toolkit-v2/sidebar-icon.png" alt-text="Visual Studio Code 边栏中的 Teams 图标。":::

1. 选择 **创建新项目**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-project.png" alt-text="Teams 工具包边栏中&quot;创建新项目&quot;链接的位置。":::

1. 选择 **创建新的 Teams 应用**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-new-project-intro.png" alt-text="&quot;创建新项目&quot;的向导启动":::

1. 在" **选择功能"** 步骤 ， 选择 **邮件扩展** ，然后取消选择 **选项卡**。 按 **确定**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-create-project-capabilities.png" alt-text="显示如何向新应用添加功能的屏幕截图。":::

1. 在 **机器人注册** 步骤中，选择 **创建新的机器人注册**。

   :::image type="content" source="../assets/images/teams-toolkit-v2/create-bot-registration.png" alt-text="选择创建新的自动注册":::

   > [!NOTE]
   > 消息扩展依赖于自动程序，在用户和你的代码之间提供对话框。

1. 在" **编程语言** 步骤中， 选择 **JavaScript**。

    :::image type="content" source="../assets/images/teams-toolkit-v2/create-project-programming-languages.png" alt-text="显示如何选择编程语言的屏幕截图。":::

1. 选择工作区文件夹。  将在工作区文件夹中为正在创建的项目创建一个文件夹。

1. 为应用输入合适的名称，如 `helloworld`。  应用的名称只能包含字母数字字符。  按 **Enter** 以继续。

将在数秒钟内创建你的 Teams 应用。

# <a name="command-line"></a>[命令行](#tab/cli)

使用 `teamsfx` CLI 创建你的第一个项目。  从要创建项目文件夹的文件夹开始。

``` bash
teamsfx new
```

CLI 会提出一些问题来引导创建项目。  每个问题将告诉你该如何回答（例如，使用箭头键选择一个选项）。  如果已回答问题，请通过按 **Enter** 确认。

1. 选择 **"创建新的 Teams 应用**。
1. 选择 **邮件扩展** 功能，然后取消选择" **选项卡** 功能。
1. 选择 **创建新的自动注册**。
1. 选择 **JavaScript** 作为编程语言。
1. 按 **Enter** 选择默认工作区文件夹。
1. 为应用输入合适的名称，如 `helloworld`。  应用的名称只能包含字母数字字符。

回答所有问题后，将创建项目。

---

## <a name="take-a-tour-of-the-source-code"></a>浏览源代码

若要暂时跳过此部分，可以 [在本地运行应用](#run-your-app-locally)。

消息扩展使用 [Bot Framework](https://docs.botframework.com) 以允许用户通过对话与你的服务交互。  设置标点文件夹后，你的项目将如下所示:

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-file-layout.png" alt-text="机器人项目的文件布局。":::

自动程序代码存储在 `bot` 中。  `bots/messageExtensionBot.js` 是邮件扩展的主入口点。

> [!Tip]
> 在将第一个机器人集成到 Teams 中之前，请熟悉 Teams 以外的机器人。  可以通过查看 [Azure 机器人服务](/azure/bot-service/bot-builder-basics?view=azure-bot-service-4.0&preserve-view=true)教程找到有关机器人的更多信息。

## <a name="run-your-app-locally"></a>在本地运行应用

Teams 工具包允许你在本地托管应用。  为此，请执行以下操作:

- Azure Active Directory 应用程序是在 M365 租户中注册的。
- 向 Teams 开发人员门户提交应用清单。
- 在本地使用 Azure 函数核心工具运行 API，以支持你的应用。
- [ngrok](https://ngrok.io) 安装并用于在 Teams 和消息扩展之间提供一个隧道。

若要在本地构建和运行应用，请执行：

1. 在 Visual Studio Code 中，按 **F5** 以在调试模式下运行应用程序。

   > 首次运行该应用时，将下载所有依赖项并编译该应用。  编译完成后，将自动打开浏览器窗口。  这可能需要 3-5 分钟才能完成。

1. 将在 Web 浏览器中加载 Teams，并提示进行登录。 如果系统提示打开 Microsoft Teams，请选择"取消"以保留在浏览器中。 使用 M365 帐户登录。

1. 按 **添加** 将应用添加到你的帐户。

加载应用后，你将直接进入搜索对话框：

:::image type="content" source="../assets/images/teams-toolkit-v2/msgextn-completed-app.png" alt-text="操作中基于搜索的邮件扩展":::

在搜索框中键入文本，然后选择其中一个选项。  自适应卡片将添加到输入框中。

<!-- markdownlint-disable MD033 -->
<details>
<summary>在调试器中本地运行应用时，会发生什么情况。</summary>

按 F5 时，Teams 工具包:

1. 使用 Azure Active Directory 注册应用程序。
1. 在 Microsoft Teams 中将你的应用程序注册为“旁加载”。
1. 使用 [Azure Function Core Tools](/azure/azure-functions/functions-run-local?#start) 启动在本地运行的应用程序后端。
1. 启动 ngrok 隧道，以便 Teams 可以与你的应用通信。
1. 启动 Microsoft Teams，并用命令指示 Teams 旁加载该应用程序。

</details>

<!-- markdownlint-disable MD033 -->
<details>
<summary>了解如何在本地运行应用时解决常见问题。</summary>

若要在 Teams 中成功运行应用，必须具有允许应用程序旁加载的 Microsoft 365 开发帐户。 有关开设帐户的详细信息，请参阅 [先决条件](prerequisites.md#enable-sideloading)。

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

## <a name="add-a-configuration-page-to-your-messaging-extension"></a>向邮件扩展添加配置页面

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

## <a name="code-sample"></a>代码示例

The Teams Search Auth Config for sample projects on GitHub， demonstrate how to create messaging extensions that include a configuration page and [Bot Service authentication](https://github.com/microsoft/BotBuilder-Samples#teams-samples). 这些示例还演示如何创建接受搜索请求的邮件扩展，并返回用户登录后的结果。

| **示例名称** | **说明** | **.NET** | **Node.js** | **Python** |
|-----------------|-----------------|-------------|--------------|--------|
| 自动程序生成器 | 创建邮件扩展。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/52.teams-messaging-extensions-search-auth-config) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/52.teams-messaging-extensions-search-auth-config) | [View]( https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/50.teams-messaging-extension-search) |

## <a name="additional-code-sample"></a>其他代码示例

> [!div class="nextstepaction"]
> [查看更多 Bot Framework 示例GitHub](https://github.com/OfficeDev/microsoft-teams-samples#messaging-extensions-samples-using-the-v4-sdk)

## <a name="see-also"></a>另请参阅

- [使用 React 创建 Teams 应用](first-app-react.md)
- [使用 Blazor 创建 Teams 应用](first-app-blazor.md)
- [创建 Teams 应用作为 SharePoint Web 部件](first-app-spfx.md) （不需要 Azure）
- [创建对话机器人](first-app-bot.md)
