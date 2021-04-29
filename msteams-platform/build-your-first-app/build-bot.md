---
title: 入门 - 生成自动程序
author: girliemac
description: 使用 Microsoft Teams 工具快速创建 Microsoft Teams Toolkit。
ms.author: timura
ms.date: 04/14/2020
ms.topic: tutorial
ms.openlocfilehash: dbb6f0a2497a0914d8e14473f1dbd6b2b225fc96
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068605"
---
# <a name="create-your-first-bot-for-teams"></a>为 Teams 创建第一个自动程序

本教程指导你生成基本自动程序应用。 机器人充当 Teams 用户与 Web 应用或具有对话界面的服务之间的中介。 用户可以与机器人聊天，以快速获取信息或启动服务执行的工作流和任务。

## <a name="what-youll-learn"></a>您将了解哪些功能

* 使用 Microsoft Teams Toolkit for Visual Studio Code 创建应用项目和自动程序。
* 了解与机器人相关的 Teams 应用配置。
* 使用 localhost 隧道解决方案在本地托管和运行应用。
* 在 Teams 中旁加载和测试机器人。

## <a name="prerequisites"></a>先决条件

确保你了解如何设置和构建简单的 Teams 应用。 有关详细信息，请参阅创建 [你的第一个 Microsoft Teams"Hello， World！"应用](../build-your-first-app/build-and-run.md)。 

## <a name="1-create-your-app-project"></a>1. 创建应用项目

Microsoft Teams Toolkit可帮助你为应用设置以下组件： 

* **与机器人相关的应用** 配置和基架
* **自动** 注册到 Microsoft Azure 自动程序服务的自动程序

**创建应用项目**

1. 在Visual Studio代码"中，选择左侧活动栏上的 **"Microsoft Teams"，** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择"**创建新的 Teams 应用"。**

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="显示如何在 Teams 应用中创建应用的Toolkit。":::

1. 系统提示时，使用 Microsoft 365 开发帐户登录。 
1. 在"选择项目"屏幕上，选择"对话机器人"： 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="显示如何在 Teams Toolkit 中创建新机器人的屏幕截图。":::

1. 在" **配置项目"** 屏幕上，输入自动程序的名称。 这是应用的默认名称，也是本地计算机上应用项目目录的名称。
1. 选择 **"新建自动**  >  **程序创建自动** 程序注册"，如下图所示：

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Screenshot showing naming new bot in the Teams Toolkit.":::

    如果成功，你的新自动程序将具有 **"已注册"** 状态。 现在自动程序已注册到 Microsoft Azure 自动程序服务。 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Screenshot showing registering new bot in the Teams Toolkit.":::

1. 选择 **屏幕** 底部的"完成"，然后在你的计算机上保存项目。  

## <a name="2-understand-your-app-project-components"></a>2. 了解应用项目组件

当你使用 Teams 解决方案创建项目时，许多应用配置和基架会自动Toolkit。 让我们看一下构建自动程序的主要组件：

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="Screenshot showing a project scaffold in the Teams Toolkit.":::

如果你在另一个教程中创建选项卡，则机器人的应用基架将有所不同。 与选项卡不同，机器人开发不需要你生成任何前端 Web 组件或使用 Teams JavaScript 客户端 SDK。  相反，基架使用 [Microsoft Bot Framework，](https://dev.botframework.com/)它是一个开源 SDK，用于构建可在 Web、移动以及当然 Teams 上工作的智能企业级机器人！ 

该文件位于项目的根目录中，是特定于 Teams 的处理程序，可处理机器人活动，例如机器人如何 `botActivityHandler.js` 响应特定消息。 应用基架提供的文件位于项目的根目录中，是处理机器人活动（如机器人如何响应特定消息）的 `botActivityHandler.js` Teams 特定处理程序。

## <a name="3-securely-expose-your-localhost-to-the-internet"></a>3. 安全地将 localhost 公开到 Internet

查看文件，该文件将创建 HTTP 服务器并处理路由，以侦听对机器人 `index.js` 的传入请求。 `/api/messages`是应用用于响应客户端请求的终结点 URL： 

```JavaScript
server.post('/api/messages', (req, res) => { 
  adapter.processActivity(req, res, async (context) => { 
    await botActivityHandler.run(context); 
  }); 
}); 
```

若要将请求转发到机器人的逻辑，必须设置一个可公开访问的 URL，例如 `https://example.com/api/messages` ，而不是 `https://localhost` 。 由于你的应用当前正在从 localhost 运行，因此你必须 *对网络进行* 隧道传输。

隧道是一种协议，允许你跨网络传输数据。 localhost 隧道提供本地计算机和远程连接之间的连接。 若要安全地将 localhost 公开到 Internet，建议使用名为 **ngrok** 的第三方工具。 这将为您提供一个安全 URL。 

1. 转到 ["ngrok.com](https://ngrok.com/download) 网站，并按照说明在您的环境中安装和设置 ngrok。 
    
    将已安装的 ngrok.exe 文件的完整路径添加到系统 PATH 环境变量。 具体步骤特定于您使用的命令行管理程序。

1.  完成设置后，打开终端并运行 `ngrok http -host-header=rewrite 3978` 。 

    现在 ngrok 提供了一个在端口 3978 转发到 localhost 的公共安全 URL，因此请复制 HTTPS URL，如下面的屏幕截图所示， `https://287a4f4223bc.ngrok.io` 因为 Teams 需要 HTTPS 连接： 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="显示具有 ngrok 的 localhost 隧道的屏幕截图。":::

1. 在应用清单中注册 URL。 

## <a name="4-register-your-bot-endpoint"></a>4. 注册自动程序终结点

若要在 Teams 中使用自动程序，你必须向 Azure Bot 服务注册它。 使用 Teams 应用设置应用时，会自动Toolkit。

仍必须指定终结点地址，以接收并处理发送给机器人的用户消息或请求。 通常，URL 类似于 `https://HOST_URL/api/messages` 。 可以在工具包中快速进行配置。

1. 在Visual Studio代码"中，打开 **"Microsoft Teams Toolkit"。**
1. 选择 **"自动**  >  **程序""** 现有自动程序注册"，然后选择在安装期间创建的自动程序。 
1. 在 **"Bot 终结点地址** "字段中，输入 ngrok URL，例如 ，您将托管机器人并 `https://287a4f4223bc.ngrok.io` 附加到 `/api/messages` 其中：

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="显示如何使用 ngrok 隧道 localhost 的屏幕截图。":::

    正确设置终结点后，机器人将能够响应 Teams 中的消息。 

## <a name="5-build-and-run-your-app"></a>5. 生成并运行应用

你已设置 URL 以托管自动程序，并配置为处理消息。 可以启动并运行应用了。

1. 在终端中，转到应用项目的根目录并运行 `npm install` 。
1. 运行 `npm start`。

   如果成功，你将看到以下消息，指示机器人正在侦听你的活动 `localhost` ：

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. 在 Teams 中旁加载机器人

运行自动程序后，可以在 Teams 中安装它。

> [!TIP]
> 如果你之前未旁加载 Teams 应用并遇到问题，请按照以下 [说明操作](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。

1. 在Visual Studio代码"中，选择 **F5** 键以启动 Teams Web 客户端。
1. 在应用安装对话框中，选择 **"为我添加"。** 

   > [!Note]
   > 默认情况下，应用将添加到你的一对一直接聊天消息中，但是你可以选择将其安装到团队或聊天，方法是单击"为我添加"旁边的小 **箭头**。 在本教程中，我们只需单击"添加"。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="显示使用 ngrok 的隧道 localhost 的屏幕截图。":::

## <a name="7-test-your-bot"></a>7. 测试机器人

让我们对机器人说"Hello"。

* 在撰写框中，发送邮件 `Hello` 。
    自动程序使用类似以下消息的回复：

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="显示用户对 Teams 机器人说&quot;Hello&quot;并收到响应的屏幕截图。":::

    现在，你已创建一个基本的 Teams 机器人，可以一对一地与用户通信，或在组设置中通过 (和聊天功能) 🎉

## <a name="troubleshoot-your-bot"></a>自动程序疑难解答

如果你在完成本教程时有问题，以下信息可能会有所帮助。

### <a name="bot-isnt-connected-to-teams"></a>机器人未连接到 Teams


如果你安装了应用，但自动程序无法工作，请确保自动程序已连接到 Azure [Bot 服务的 Teams *频道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

了解这与 Teams 中的频道不同，了解这一点很重要。 在这种情况下，频道是 Azure 自动程序服务如何将机器人连接到 Teams 或其他受支持的 [Microsoft 或第三方通信应用](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="see-also"></a>另请参阅

* [Bot 基础知识](../bots/bot-basics.md)
* [为 Microsoft Teams 生成个人选项卡](../build-your-first-app/build-personal-tab.md)
* [查看 Teams 机器人可以使用我们的示例之一执行哪些其他功能](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [自动程序对话基础知识](../bots/how-to/conversations/conversation-basics.md)
* [设计准则](../bots/design/bots.md) 
* [生产就绪 UI 模板](../concepts/design/design-teams-app-ui-templates.md)
* [Teams 中的自动程序身份验证](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [创建没有工具包的自动程序](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建邮件扩展](../build-your-first-app/build-messaging-extension.md)
