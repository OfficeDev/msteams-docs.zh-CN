---
title: 入门 - 生成自动程序
author: heath-hamilton
description: 使用 Microsoft Teams 工具快速创建 Microsoft Teams Toolkit。
ms.author: lajanuar
localization_priority: Normal
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 5dfbfa05d2f1e36bbc14bd929cb2592303081522
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019998"
---
# <a name="build-a-bot-for-microsoft-teams"></a>构建适用于 Microsoft Teams 的自动程序

本教程中 *将生成基本* 机器人应用。 机器人充当 Teams 用户和 Web 服务之间的中介。 用户可以与机器人聊天，以快速获取信息或启动服务执行的工作流和任务。

## <a name="your-assignment"></a>您的工作分配

你的工作区创建了一个 Teams 应用，该应用 [使用选项卡](../build-your-first-app/build-personal-tab.md) 来显示重要的联系人信息。 例如，同事可以快速访问技术支持电话号码。 但是，如果人们能够使用 chatbot 联系技术支持，而不是呼叫，应该怎么做？ 你的领导要求你查看在 Teams 中快速启动和运行基本对话机器人。

## <a name="what-youll-learn"></a>您将了解哪些功能

> [!div class="checklist"]
>
> * 使用 Microsoft Teams Toolkit for Visual Studio Code 创建应用项目和自动程序
> * 确定一些与机器人相关的应用配置和基架
> * 在本地托管应用
> * 为 Teams 配置自动程序
> * 在 Teams 中旁加载和测试机器人

## <a name="before-you-begin"></a>开始之前

如果尚未了解，请确保 [了解并安装 Teams 开发先决条件](build-first-app-overview.md#get-prerequisites)。

## <a name="1-create-your-app-project"></a>1. 创建应用项目

Microsoft Teams Toolkit可帮助你为应用设置以下组件：

* **与机器人相关的应用** 配置和基架
* **自动** 注册到 Microsoft Azure 自动程序服务的自动程序

> [!TIP]
> 如果你之前尚未创建 Teams 应用项目，你可能会发现按照这些说明更详细地解释项目会[](../build-your-first-app/build-and-run.md)很有帮助。

1. 在Visual Studio代码"中，选择左侧活动栏上的 **"Microsoft Teams"，** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择"**创建新的 Teams 应用"。**
1. 系统提示时，使用 Microsoft 365 开发帐户登录。
1. 在"**添加功能"屏幕上**，选择"**自动程序"，** 然后选择"下一 **步"。**
1. 输入 Teams 应用的名称。  (这是应用的默认名称，也是本地计算机上应用项目目录的名称。) 
1. 转到配置 **自动程序** ，然后选择 **创建新** 自动程序，然后选择 **创建自动程序注册**。 如果成功，你的新自动程序将具有 **"已注册"** 状态。
1. 选择 **屏幕** 底部的"完成"，然后选择创建项目的位置。

## <a name="2-identify-relevant-app-project-components"></a>2. 确定相关的应用程序项目组件

当你使用 Teams 解决方案创建项目时，许多应用配置和基架会自动Toolkit。 让我们看一下生成自动程序的主要组件。

### <a name="app-configurations"></a>应用配置

若要查看或更新机器人的配置，请选择工具包中的 **App Studio，** 然后转到 **自动程序**。

### <a name="app-scaffolding"></a>应用基架

应用基架提供了一个文件，该文件位于项目的根目录中，用于处理机器人如何处理 Teams (中的活动，例如机器人如何响应特定消息，如 `botActivityHandler.js` "Hello") 。

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. 设置应用的安全隧道

出于测试目的，让我们在端口 3978 (本地 Web 服务器上承载) 。

1. 如果尚未安装，请安装 [ngrok](https://ngrok.com/download)。
1. 在终端中，运行 `ngrok http -host-header=rewrite 3978` 。
1. 复制输出链接中的 HTTPS URL，例如 (，) `https://468b9ab725e9.ngrok.io` Teams 需要 HTTPS 连接。

通过此 URL， (需要 HTTPS 连接的 Teams) 将能够隧道连接到你在 `localhost` 端口 3978 (托管应用) 。

## <a name="4-configure-your-bot"></a>4. 配置自动程序

若要在 Teams 中使用自动程序，你必须向 Azure Bot 服务注册它。 对于你来说，当你使用 Teams 应用设置应用时，这将自动Toolkit。

你仍然必须指定终结点地址，以接收并处理用户 (消息，即) 发送到自动程序的请求。 通常，URL 类似于 `https://HOST_URL/api/messages` 。 可以在工具包中快速进行配置。

1. 在Visual Studio代码"中，选择左侧活动栏上的 **"Microsoft Teams"，** 然后选择"打开 :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: Microsoft Teams **Toolkit"。**
1. 转到自动 **程序>现有自动程序注册并选择** 你在安装期间创建的自动程序。
1. 在 **"自动程序终结点** 地址"字段中，输入 ngrok URL (例如，) 托管自动程序并追加到其中 `https://468b9ab725e9.ngrok.io` `/api/messages` 。<br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="显示可以在 Teams 服务中配置自动程序终结点 URL 的Toolkit。":::

机器人将能够响应 Teams 中的消息。

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

1. 在Visual Studio代码"中，按 **F5** 键以启动 Teams Web 客户端。
1. 在应用安装对话框中，选择 **"为我添加"。**  (你可以将聊天机器人添加到频道或聊天中，但对其他人来说，在一对一聊天中测试聊天机器人的干扰性) 

## <a name="7-test-your-bot"></a>7. 测试机器人

现在，对于有趣的部分：让我们对机器人说"Hello"。

1. 在撰写框中，发送邮件 `Hello` 。

自动程序使用类似以下消息的回复。

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="显示用户对 Teams 机器人说&quot;Hello&quot;并收到响应的屏幕截图。":::

## <a name="well-done"></a>干的好

恭喜！ 你有一个基本的 Teams 机器人，可以一对一地与用户通信，或在组设置 (频道和聊天) 。

## <a name="troubleshooting"></a>疑难解答

如果你在完成本教程时有问题，以下信息可能会有所帮助。

### <a name="bot-isnt-connected-to-teams"></a>机器人未连接到 Teams

如果你安装了应用，但自动程序无法工作，请确保自动程序已连接到 Azure [Bot 服务的 Teams *频道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

了解这与 Teams 中的频道不同，了解这一点很重要。 在这种情况下，频道是 Azure 自动程序服务如何将机器人连接到 Teams 或其他受支持的 [Microsoft 或第三方通信应用](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="learn-more"></a>了解详细信息

* [查看 Teams 机器人可以使用我们的示例之一执行哪些其他功能](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [自动程序对话基础知识](../bots/how-to/conversations/conversation-basics.md)
* 遵循 [我们的设计指南](../bots/design/bots.md) ，使用生产就绪 [UI](../concepts/design/design-teams-app-ui-templates.md) 模板构建，以创建无缝体验。
* [Teams 中的自动程序身份验证](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [创建没有工具包的自动程序](../resources/bot-v3/bots-create.md)
