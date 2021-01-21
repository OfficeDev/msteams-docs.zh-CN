---
title: 入门 - 生成自动程序
author: heath-hamilton
description: 使用 Microsoft Teams 工具快速创建 Microsoft Teams Toolkit。
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: fbabd5130f0b7eb648a980f5f143792cc4c17933
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911945"
---
# <a name="build-a-bot-for-microsoft-teams"></a>为 Microsoft Teams 生成自动程序

本教程中将 *生成基本机器人* 应用。 机器人充当 Teams 用户和 Web 服务之间的中介。 用户可以与机器人聊天，以快速获取信息或启动由你的服务执行的工作流和任务。

## <a name="your-assignment"></a>你的作业

你的工作场所创建了一个 Teams 应用，该应用 [使用选项卡](../build-your-first-app/build-personal-tab.md) 来显示重要的联系信息。 例如，同事可以快速访问技术支持电话号码。 但是，如果人们可以通过聊天机器人联系技术支持，而不是通话呢？ 你的领导要求你查看在 Teams 中快速启动和运行基本对话机器人。

## <a name="what-youll-learn"></a>您将了解哪些知识

> [!div class="checklist"]
>
> * 使用 Microsoft Teams Toolkit for Visual Studio Code 创建应用项目和自动程序
> * 确定一些与机器人相关的应用配置和基架
> * 在本地托管应用
> * 为 Teams 配置自动程序
> * 在 Teams 中旁加载和测试机器人

## <a name="before-you-begin"></a>准备工作

如果尚未安装，请确保了解并 [安装 Teams 开发先决条件](build-first-app-overview.md#get-prerequisites)。

## <a name="1-create-your-app-project"></a>1. 创建应用项目

Microsoft Teams Toolkit可帮助你为应用设置以下组件：

* **与机器人相关的** 应用配置和基架
* **自动** 注册到 Microsoft Azure 自动程序服务的自动程序

> [!TIP]
> 如果你之前尚未创建 Teams 应用项目，你可能会发现按照这些说明更详细地解释项目非常有用[](../build-your-first-app/build-and-run.md)。

1. 在Visual Studio代码中，选择左侧活动栏上的 **Microsoft Teams，** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 **"创建新的 Teams 应用"。**
1. 当系统提示时，使用 Microsoft 365 开发帐户登录。
1. 在"**添加功能"屏幕上**，选择 **"自动程序**"，然后选择"**下一步"。**
1. 输入 Teams 应用的名称。  (这是应用的默认名称，也是本地计算机上应用项目目录的名称。) 
1. 转到"**配置自动程序**"，然后选择 **"新建自动程序**，**然后创建自动程序注册"。** 如果成功，你的新自动 **程序将具有** 注册状态。
1. 选择 **屏幕** 底部的"完成"，然后选择创建项目的位置。

## <a name="2-identify-relevant-app-project-components"></a>2. 确定相关应用程序项目组件

使用 Teams 解决方案创建项目时，会自动设置大部分应用配置和基架Toolkit。 让我们看一下生成自动程序的主要组件。

### <a name="app-configurations"></a>应用配置

若要查看或更新机器人的配置，请在工具包中选择 **App Studio** 并转到 **Bots。**

### <a name="app-scaffolding"></a>应用基架

应用基架提供了一个文件，该文件位于项目的根目录中，用于处理机器人如何处理 Teams (中的活动，例如机器人如何响应特定消息，如 `botActivityHandler.js` "Hello") 。

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. 为应用设置安全隧道

出于测试目的，让我们在本地 Web 服务器上托管应用， (端口 3978) 。

1. 如果尚未安装，请安装 [ngrok](https://ngrok.com/download)。
1. 在终端中，运行 `ngrok http -host-header=rewrite 3978` 。
1. 例如，复制输出 URL (，) `https://468b9ab725e9.ngrok.io` Teams 需要 HTTPS 连接。

通过此 URL， (需要 HTTPS 连接的 Teams) 将能够隧道连接到在 `localhost` 端口 3978 (托管应用) 。

## <a name="4-configure-your-bot"></a>4. 配置机器人

若要在 Teams 中使用自动程序，你必须向 Azure Bot 服务注册它。 如果你使用 Teams 服务设置应用，这将自动Toolkit。

您仍必须指定终结点地址，以接收并处理 (消息，即发送到自动) 的请求。 通常，URL 如下所示 `https://HOST_URL/api/messages` 。 可以在工具包中快速配置此功能。

1. 在Visual Studio代码中，选择左侧活动栏上的 **Microsoft Teams，** 然后选择" :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 打开 Microsoft **Teams** Toolkit"。
1. 转到 **"自动>现有自动程序注册** "，然后选择在安装期间创建的自动程序。
1. 在 **Bot 终结点地址** 字段中，输入 ngrok URL (例如，) 自动程序并追加 `https://468b9ab725e9.ngrok.io` `/api/messages` 到其中。<br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="显示可在 Teams 服务中配置自动程序终结点 URL 的Toolkit。":::

机器人将能够响应 Teams 中的消息。

## <a name="5-build-and-run-your-app"></a>5. 生成并运行应用

你已设置 URL 来托管自动程序，并配置它以处理消息。 是时候让应用启动并运行了。

1. 在终端中，转到应用项目的根目录并运行 `npm install` 。
1. 运行 `npm start`。

如果成功，你将看到以下消息，指示机器人正在侦听你的活动 `localhost` ：

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. 在 Teams 中旁加载机器人

运行自动程序后，可以在 Teams 中安装它。

> [!TIP]
> 如果你之前没有旁加载 Teams 应用并遇到问题，请按照以下 [说明操作](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。

1. 在Visual Studio中，按 **F5** 键启动 Teams Web 客户端。
1. 在应用安装对话框中，选择 **"为我添加"。**  (你可以将聊天机器人添加到频道或聊天中，但对其他人来说，在一对一聊天中测试机器人的干扰性) 

## <a name="7-test-your-bot"></a>7. 测试机器人

现在，对于有趣的部分：让我们对机器人说"Hello"。

1. 在撰写框中，发送邮件 `Hello` 。

机器人使用如下消息进行回复。

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="显示用户向 Teams 机器人说&quot;Hello&quot;并收到响应的屏幕截图。":::

## <a name="well-done"></a>干的好

恭喜！ 你拥有一个基本的 Teams 机器人，可以一对一地与用户通信，或在频道和聊天 (组设置中) 。

## <a name="troubleshooting"></a>疑难解答

如果你在完成本教程时出问题，以下信息可能会有所帮助。

### <a name="bot-isnt-connected-to-teams"></a>自动程序未连接到 Teams

如果已安装应用，但自动程序无法工作，请确保自动程序已连接到 Azure [Bot 服务的 Teams *频道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

了解这与 Teams 中的频道不同，了解这一点很重要。 在这种情况下，频道是 Azure 自动程序服务如何将机器人连接到 Teams 或其他受支持的 [Microsoft 或第三方通信应用](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="learn-more"></a>了解详细信息

* [了解 Teams 机器人可以使用我们的一个示例执行哪些其他功能](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [自动程序对话基础知识](../bots/how-to/conversations/conversation-basics.md)
* 遵循 [我们的设计准则，](../bots/design/bots.md) 使用 [生产就绪 UI](../concepts/design/design-teams-app-ui-templates.md) 模板生成，以创建无缝体验。
* [Teams 中的自动程序身份验证](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
* [创建没有工具包的机器人](../bots/how-to/create-a-bot-for-teams.md)
