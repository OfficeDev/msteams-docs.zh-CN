---
title: 入门 - 生成自动程序
author: girliemac
description: 使用Microsoft Teams快速创建自动程序Microsoft Teams Toolkit。
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
# <a name="create-your-first-bot-for-teams"></a>创建第一个自动程序Teams

本教程指导你生成基本自动程序应用。 自动程序充当用户Teams会话界面的 Web 应用或服务之间的中介。 用户可以与机器人聊天，以快速获取信息或启动服务执行的工作流和任务。

## <a name="what-youll-learn"></a>您将了解哪些功能

* 使用 Microsoft Teams Toolkit 创建应用项目和Visual Studio Code。
* 了解Teams自动程序相关的应用配置。
* 使用 localhost 隧道解决方案在本地托管和运行应用。
* 旁加载和测试自动程序Teams。

## <a name="prerequisites"></a>先决条件

确保你了解如何设置和构建简单的 Teams 应用。 有关详细信息，请参阅创建[你的第一个Microsoft Teams Hello， World！"应用](../build-your-first-app/build-and-run.md)。 

## <a name="1-create-your-app-project"></a>1. 创建应用项目

以下Microsoft Teams Toolkit可帮助你为应用设置以下组件： 

* **与机器人相关的应用** 配置和基架
* **自动** 注册到自动程序服务的Microsoft Azure自动程序

**创建应用项目**

1. In Visual Studio Code， select **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: on the left Activity Bar and choose Create a new **Teams app**.

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-01.png" alt-text="显示如何在应用商店中创建应用的Teams Toolkit。":::

1. 当系统提示时，使用你的 Microsoft 365帐户登录。 
1. 在"选择项目"屏幕上，选择"对话机器人"： 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-02.png" alt-text="Screenshot showing how to create a new bot in the Teams Toolkit.":::

1. 在" **配置项目"** 屏幕上，输入自动程序的名称。 这是应用的默认名称，也是本地计算机上应用项目目录的名称。
1. 选择 **"新建自动**  >  **程序创建自动** 程序注册"，如下图所示：

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-03.png" alt-text="Screenshot showing naming new bot in the Teams Toolkit.":::

    如果成功，你的新自动程序将具有 **"已注册"** 状态。 现在，自动程序将自动注册到 Microsoft Azure Bot Service。 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-04.png" alt-text="Screenshot showing registering new bot in the Teams Toolkit.":::

1. 选择 **屏幕** 底部的"完成"，然后在你的计算机上保存项目。  

## <a name="2-understand-your-app-project-components"></a>2. 了解应用项目组件

使用应用程序配置和基架创建项目时，许多应用配置和基架Teams Toolkit。 让我们看一下构建自动程序的主要组件：

:::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-05.png" alt-text="显示项目基架的屏幕截图Teams Toolkit。":::

如果你在另一个教程中创建选项卡，则机器人的应用基架将有所不同。 与选项卡不同，机器人开发不需要你生成任何前端 Web 组件或使用 JavaScript Teams SDK。  相反，基架使用[Microsoft Bot Framework](https://dev.botframework.com/)，这是一个开源 SDK，用于构建可在 Web、移动以及当然Teams！ 

该文件位于项目的根目录中，是Teams聊天机器人活动（如机器人如何响应特定消息）的 `botActivityHandler.js` 特定于 Teams 处理程序。 应用基架提供位于项目根目录中的文件是 Teams 特定处理程序，用于处理机器人活动，如机器人如何响应特定 `botActivityHandler.js` 消息。

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

    现在 ngrok 提供了一个在端口 3978 上转发到 localhost 的公共安全 URL，因此请复制 HTTPS URL，如下面的屏幕截图所示，因为 `https://287a4f4223bc.ngrok.io` Teams 需要 HTTPS 连接： 

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-ngrok-06.png" alt-text="显示具有 ngrok 的 localhost 隧道的屏幕截图。":::

1. 在应用清单中注册 URL。 

## <a name="4-register-your-bot-endpoint"></a>4. 注册自动程序终结点

若要在 Azure Teams自动程序，必须使用 Azure Bot 服务注册它。 当你使用应用设置应用时，这会自动Teams Toolkit。

仍必须指定终结点地址，以接收并处理发送给机器人的用户消息或请求。 通常，URL 类似于 `https://HOST_URL/api/messages` 。 可以在工具包中快速进行配置。

1. 在Visual Studio Code中，打开 **"Microsoft Teams Toolkit"。**
1. 选择 **"自动**  >  **程序""** 现有自动程序注册"，然后选择在安装期间创建的自动程序。 
1. 在 **"Bot 终结点地址** "字段中，输入 ngrok URL，例如 ，您将托管机器人并 `https://287a4f4223bc.ngrok.io` 附加到 `/api/messages` 其中：

    :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-bots-07.png" alt-text="显示如何使用 ngrok 隧道 localhost 的屏幕截图。":::

    正确设置终结点后，自动程序Teams响应邮件。 

## <a name="5-build-and-run-your-app"></a>5. 生成并运行应用

你已设置 URL 以托管自动程序，并配置为处理消息。 可以启动并运行应用了。

1. 在终端中，转到应用项目的根目录并运行 `npm install` 。
1. 运行 `npm start`。

   如果成功，你将看到以下消息，指示机器人正在侦听你的活动 `localhost` ：

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. 将自动程序旁加载Teams

运行自动程序后，你可以将其安装在Teams。

> [!TIP]
> 如果你之前未旁加载Teams并遇到问题，请按照以下[说明操作](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。

1. 在Visual Studio Code中，选择 **F5** 键以启动 Teams Web 客户端。
1. 在应用安装对话框中，选择 **"为我添加"。** 

   > [!Note]
   > 默认情况下，应用将添加到你的一对一直接聊天消息中，但是你可以选择将其安装到团队或聊天，方法是单击"为我添加"旁边的小 **箭头**。 在本教程中，我们只需单击"添加"。

   :::image type="content" source="../assets/images/build-your-first-app/vscode-teams-toolkit-install-08.png" alt-text="显示使用 ngrok 的隧道 localhost 的屏幕截图。":::

## <a name="7-test-your-bot"></a>7. 测试机器人

让我们对机器人说"Hello"。

* 在撰写框中，发送邮件 `Hello` 。
    自动程序使用类似以下消息的回复：

    :::image type="content" source="../assets/images/build-your-first-app/teams-client-bot.png" alt-text="显示用户向自动程序Teams&quot;Hello&quot;并收到响应的屏幕截图。":::

    现在，你已创建一Teams聊天机器人，该聊天机器人可以一对一地与用户通信，或在组设置中 (频道和聊天) 🎉

## <a name="troubleshoot-your-bot"></a>自动程序疑难解答

如果你在完成本教程时有问题，以下信息可能会有所帮助。

### <a name="bot-isnt-connected-to-teams"></a>自动程序未连接到Teams


如果你安装了应用，但自动程序无法工作，请确保自动程序已连接到 Azure 自动程序服务Teams [*频道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

了解这一点与 Teams 中的频道Teams。 在这种情况下，通道是 Azure 自动程序服务如何将机器人连接到Teams受支持的 Microsoft 或第三方[通信应用](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="see-also"></a>另请参阅

* [Bot 基础知识](../bots/bot-basics.md)
* [为用户生成个人Microsoft Teams](../build-your-first-app/build-personal-tab.md)
* [查看其他Teams机器人可以使用我们的示例之一执行哪些功能](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [自动程序对话基础知识](../bots/how-to/conversations/conversation-basics.md)
* [设计准则](../bots/design/bots.md) 
* [生产就绪 UI 模板](../concepts/design/design-teams-app-ui-templates.md)
* [自动程序身份验证Teams](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [创建没有工具包的自动程序](../resources/bot-v3/bots-create.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建邮件扩展](../build-your-first-app/build-messaging-extension.md)
