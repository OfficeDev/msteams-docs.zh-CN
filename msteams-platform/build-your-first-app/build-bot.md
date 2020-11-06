---
title: 入门-构建机器人
author: heath-hamilton
description: 使用 Microsoft 团队工具包快速创建 Microsoft 团队 bot。
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 1229064ac6b7aab73c50048f0764c6a2353ab54a
ms.sourcegitcommit: 99c35de7e2c604bd8bce392242c2c2fa709cd50b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/06/2020
ms.locfileid: "48931735"
---
# <a name="build-a-bot-for-microsoft-teams"></a>为 Microsoft 团队构建机器人

您将在本教程中构建基本 *机器人* 应用程序。 Bot 充当团队用户与 web 服务之间的媒介。 用户可以与机器人聊天以快速获取信息或启动服务执行的工作流和任务。

## <a name="your-assignment"></a>您的分配

你的工作区创建了一个使用 [选项卡](../build-your-first-app/build-personal-tab.md) 来呈现重要联系人信息的团队应用。 例如，同事可以快速访问技术支持电话号码。 而不是打电话，如果用户可以使用 chatbot 联系技术支持，该怎么办？ 你的老板要求你查看如何快速启动并在团队中运行基本的会话机器人。

## <a name="what-youll-learn"></a>你将了解的内容

> [!div class="checklist"]
>
> * 使用 Microsoft 团队工具包为 Visual Studio Code 创建一个应用程序项目和机器人
> * 确定与 bot 相关的一些应用配置和基架
> * 在本地托管应用程序
> * 为团队配置机器人
> * 旁加载和测试团队中的 bot

## <a name="before-you-begin"></a>准备工作

如果还没有，请确保 [了解并安装团队开发先决条件](build-first-app-overview.md#get-prerequisites)。

## <a name="1-create-your-app-project"></a>1. 创建您的应用程序项目

Microsoft 团队工具包可帮助您为您的应用程序设置以下组件：

* 与 bot 相关的 **应用程序配置和基架**
* 自动注册到 Microsoft Azure Bot 服务的 **Bot**

> [!TIP]
> 如果之前尚未创建团队应用程序项目，您可能会发现，请按照 [以下说明](../build-your-first-app/build-and-run.md) 更详细地说明项目。

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队** "， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **创建新的团队应用** "。
1. 出现提示时，使用 Microsoft 365 开发帐户登录。
1. 在 " **添加功能** " 屏幕上，依次选择 **Bot** 和 " **下一步** "。
1. 为你的团队应用输入名称。  (这是您的应用程序的默认名称，也是本地计算机上的应用程序项目目录的名称。 ) 
1. 转到 " **配置 bot** "，选择 " **创建新的 bot** "，然后 **创建 bot 注册** 。 如果成功，新的 bot 将具有 **已注册** 状态。
1. 选择屏幕底部的 " **完成** "，然后选择要创建项目的位置。

## <a name="2-identify-relevant-app-project-components"></a>2. 确定相关的应用程序项目组件

大部分应用配置和基架是在使用团队工具包创建项目时自动设置的。 我们来看看构建机器人的主要组件。

### <a name="app-configurations"></a>应用配置

若要查看或更新你的 bot 的配置，请在工具包中选择 **应用程序 Studio** 并转到 " **bot** "。

### <a name="app-scaffolding"></a>应用程序基架

应用程序基架提供一个 `botActivityHandler.js` 文件，该文件位于项目的根目录中，用于处理你的 bot 如何处理团队中的活动 (例如，bot 如何对特定邮件（如 "Hello" ) ）进行响应。

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. 设置应用程序的安全隧道

出于测试目的，让您在本地 web 服务器上托管您的应用程序， (端口 3978) 。

1. 如果还未安装，请安装 [ngrok](https://ngrok.com/download)。
1. 在终端中，运行 `ngrok http -host-header=rewrite 3978` 。
1. 在输出中复制 HTTPS URL (例如， `https://468b9ab725e9.ngrok.io`) 自团队需要 HTTPS 连接。

使用此 URL 时，需要 HTTPS 连接) 的团队 (可以通过 `localhost` 端口 3978) 上的 (承载应用程序的位置进行隧道连接。

## <a name="4-configure-your-bot"></a>4. 配置你的 bot

若要在团队中使用 bot，必须将其注册到 Azure Bot 服务。 幸运的是，当您使用团队工具包设置应用程序时，将自动完成此操作。

您仍必须指定接收和处理用户邮件的终结点地址 (例如，发送到 bot 的请求) 。 通常，URL 如下所示 `https://HOST_URL/api/messages` 。 您可以在工具包中快速配置此设置。

1. 在 Visual Studio Code 中，选择左侧活动栏上的 " **Microsoft 团队** "， :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 " **打开 Microsoft 团队工具包** "。
1. 转到 " **bot" > 现有的 bot 注册** ，并选择您在安装过程中创建的 bot。
1. 在 " **Bot 终结点地址** " 字段中，输入 ngrok URL (例如， `https://468b9ab725e9.ngrok.io`) 您在其中承载机器人并追加 `/api/messages` 到它的位置。<br/>
    :::image type="content" source="../assets/images/build-your-first-app/bot-config-endpoint-url.png" alt-text="图中显示可在团队工具包中配置 bot 终结点 URL 的位置。":::

你的 bot 将能够响应团队中的邮件。

## <a name="5-build-and-run-your-app"></a>5. 生成并运行应用程序

您已经设置了承载你的 bot 并将其配置为处理邮件的 URL。 现在就可以启动并运行您的应用程序了。

1. 在终端中，转到您的应用程序项目的根目录并运行该目录 `npm install` 。
1. 运行 `npm start` 。

如果成功，你将看到以下消息，指示你的 bot 正在侦听你的活动 `localhost` ：

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-bot-in-teams"></a>6. 在团队中旁加载你的机器人

在运行机器人的情况下，可以将其安装在团队中。

> [!TIP]
> 如果您在之前未旁加载团队应用程序并遇到问题，请按照这些 [说明](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)进行操作。

1. 在 Visual Studio Code 中，按 **F5** 键以启动团队 web 客户端。
1. 在 "应用程序安装" 对话框中，选择 " **为我添加** "。  (你可以将机器人添加到频道或聊天，但对其他人来说，在一对一聊天中测试 bot 的干扰较差。 ) 

## <a name="7-test-your-bot"></a>7. 测试你的 bot

现在，为有趣部分：让我们将 "Hello" 告诉你的机器人。

1. 在 "撰写" 框中，发送一 `Hello` 封邮件。

你的 bot 将回复如下邮件等内容。

:::image type="content" source="../assets/images/build-your-first-app/contoso-chatbot.png" alt-text="显示用户将 &quot;Hello&quot; 告诉团队 bot 并收到响应的屏幕截图。":::

## <a name="well-done"></a>干的好

祝贺你！ 您有一个基本的团队 bot，可以与用户一次或在组设置 (频道和聊天) 通信。

## <a name="troubleshooting"></a>故障排除

如果你在完成本教程时遇到问题，以下信息可能会有所帮助。

### <a name="bot-isnt-connected-to-teams"></a>机器人未连接到团队

如果您安装了应用程序，但机器人无法正常运行，请确保将 bot [连接到 Azure Bot 服务的团队 *频道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

请务必了解，这与团队中的频道不相同。 在这种情况下，通道是 Azure Bot 服务将你的 Bot 连接到团队或其他 [受支持的 Microsoft 或第三方通信应用程序](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)的方式。

## <a name="learn-more"></a>了解更多

* [请参阅使用我们的示例之一可以执行的其他团队 bot](https://github.com/microsoft/BotBuilder-Samples#teams-samples)
* [自动程序对话基础知识](../bots/how-to/conversations/conversation-basics.md)
* [团队中的 Bot 身份验证](../bots/how-to/authentication/auth-flow-bot.md)
* [Microsoft Bot 框架](https://dev.botframework.com/)
* [在不使用工具包的情况下创建机器人](../bots/how-to/create-a-bot-for-teams.md)
