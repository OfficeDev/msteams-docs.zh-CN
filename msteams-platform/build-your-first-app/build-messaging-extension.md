---
title: 入门 - 生成邮件扩展
author: girliemac
description: 使用 Microsoft Teams 快速创建邮件Microsoft Teams Toolkit。
ms.author: timura
ms.date: 03/25/2021
ms.topic: tutorial
ms.openlocfilehash: 91a5a15697163ee9103607511047a6411a5acf1a
ms.sourcegitcommit: 303fc214aa04757779a171337f31a6539f47fd03
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2021
ms.locfileid: "52068757"
---
# <a name="build-your-first-messaging-extension-for-microsoft-teams"></a>生成首个邮件扩展Microsoft Teams

邮件扩展有两Teams：[搜索命令](../messaging-extensions/how-to/search-commands/define-search-command.md)[和操作命令](../messaging-extensions/how-to/action-commands/define-action-command.md)。 

本教程指导你创建搜索命令 (也称为基于搜索的邮件扩展 *) ，* 它是查找外部内容并共享外部内容的快捷方式Teams。 用户可以从"撰写"或Teams访问搜索命令。

## <a name="what-youll-learn"></a>您将了解哪些功能

* 使用 Microsoft Teams Toolkit for Visual Studio Code 创建应用项目和消息传递扩展Visual Studio Code。
* 了解与邮件扩展相关的应用配置和基架。
* 在本地托管应用。
* 为邮件扩展配置自动程序。
* 旁加载和测试邮件扩展Teams。

## <a name="prerequisites"></a>先决条件

确保你了解如何设置和构建简单的Teams应用程序。 有关详细信息，请参阅创建[你的第一个Microsoft Teams Hello， World！"应用](../build-your-first-app/build-and-run.md)。

## <a name="1-create-your-app-project"></a>1. 创建应用项目

下表Microsoft Teams Toolkit设置邮件扩展的以下组件：

* **与邮件扩展相关的** 应用配置和基架
* **自动** 程序用于自动注册到自动聊天机器人服务Microsoft Azure聊天扩展

**创建应用项目**

1. In Visual Studio Code， select **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: on the left Activity Bar and choose Create a new **Teams app**.
1. 当系统提示时，使用你的 Microsoft 365帐户登录。
1. 在"**选择项目"屏幕上的**"**消息传递扩展搜索**"  >  **中**，单击 **"JS (JavaScript) "。** 
1. 输入你的应用Teams名称。 这是应用的默认名称，也是本地计算机上应用项目目录的名称。
1. 选择 **"创建新自动程序"，** 然后单击 **"创建自动程序注册"** 按钮。 如果成功，你的新自动程序将具有 *"已注册"* 状态。 现在，自动程序将自动注册到 Microsoft Azure Bot Service。 
1. 选择 **屏幕** 底部的"完成"以配置项目，并在本地计算机上保存项目。

## <a name="2-understand-your-app-project-components"></a>2. 了解应用项目组件

使用应用程序配置和基架创建项目时，许多应用配置和基架Teams Toolkit。

* 应用配置：若要查看或更新邮件扩展的配置，请在工具包中选择 App **Studio，** 然后转到消息传递 **扩展**。
* 应用基架：应用基架提供位于项目根目录中的文件，用于处理邮件扩展 (或技术上邮件扩展的自动程序) 如何响应 Teams 中的搜索 `botActivityHandler.js` 查询[](#4-configure-the-bot-for-your-messaging-extension)。

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. 设置应用的安全隧道

出于测试目的，让我们在端口 3978 (本地 Web 服务器上托管邮件) 。 您将使用 [ngrok](https://ngrok.com/download) 设置到 localhost 的安全隧道。 有关详细信息[，请参阅生成第一Microsoft Teams](../build-your-first-app/build-bot.md#3-securely-expose-your-localhost-to-the-internet)聊天机器人。 

1. 如果尚未安装，请安装 [ngrok](https://ngrok.com/download)。
1. 在终端中，运行 `ngrok http -host-header=rewrite 3978` 。
1. 复制输出链接中的 HTTPS URL，例如 (，) `https://468b9ab725e9.ngrok.io` HTTPS Teams HTTPS 连接。

   通过此 URL，Teams (需要 HTTPS) 的应用程序将能够隧道连接到你在 `localhost` 端口 3978 (托管应用) 。

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. 为邮件扩展配置自动程序

邮件扩展依赖机器人将用户请求从 Teams发送到托管服务。 自动程序必须在 Azure Bot 服务中注册，该服务是在使用 Azure 自动程序服务设置应用Teams Toolkit。

您仍必须指定自动程序终结点 URL 以接收并处理邮件扩展中的搜索查询。 通常，URL 类似于 `https://HOST_URL/api/messages` 。 可以在工具包中快速进行配置。

1. In Visual Studio Code， select **Microsoft Teams** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: on the left Activity Bar and choose Open **Microsoft Teams Toolkit**.
1. 转到自动 **程序>现有自动程序注册并选择** 你在安装期间创建的自动程序。
1. 在 **"自动程序终结点** 地址"字段中，输入 ngrok URL (例如，) 托管自动程序并追加到其中 `https://468b9ab725e9.ngrok.io` `/api/messages` 。

   自动程序将能够处理邮件扩展中的查询。

## <a name="5-build-and-run-your-app"></a>5. 生成并运行应用

你已设置用于托管邮件扩展的 URL，并配置为处理搜索。 可以启动并运行应用了。

1. 打开终端并转到应用项目的根目录
1. 运行 `npm install`。
1. 运行 `npm start`。

   如果成功，你将看到以下消息，指示邮件扩展服务正在侦听你的活动 `localhost` ：

   `Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. 在客户端中旁加载Teams

在邮件扩展运行时，你可以将其安装在Teams。

> [!TIP]
> 如果你之前未旁加载Teams并遇到问题，请按照以下[说明操作](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。

1. 在Visual Studio Code中，选择 **F5** 键以启动 Teams Web 客户端。
1. 在应用安装对话框中，选择 **"为我添加"。**

## <a name="7-test-your-messaging-extension"></a>7. 测试邮件扩展

了解消息传递扩展在聊天Teams工作。

1. 启动新聊天。 在撰写框中，选择 **"更多** :::image type="icon" source="../assets/icons/teams-client-more.png"::: "并选择你刚刚旁加载的邮件扩展应用。
1. 尝试搜索某些内容 (例如 **，Tickets**) 。 如果你的应用正常工作，你将看到示例搜索结果 (你可以稍后添加自己的) 。

   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="Screenshot showing how a search-based messaging extension is used in the Teams compose box.":::

## <a name="troubleshooting"></a>疑难解答

如果你在完成本教程时有问题，以下信息可能会有所帮助。

**自动程序未连接到Teams**

如果你安装了应用，但它无法工作，请确保消息扩展的自动程序已连接到 Azure 自动程序服务的 Teams [*通道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

了解这一点与 Teams 中的频道Teams。 在这种情况下，通道是 Azure 自动程序服务如何将机器人连接到Teams受支持的 Microsoft 或第三方[通信应用](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="see-also"></a>另请参阅

* [Teams撰写或命令框](../messaging-extensions/what-are-messaging-extensions.md) 
* [包含链接展开功能](../messaging-extensions/how-to/link-unfurling.md)
* [设计准则](../messaging-extensions/design/messaging-extension-design.md) 
* [生产就绪 UI 模板](../concepts/design/design-teams-app-ui-templates.md) 
* [添加身份验证](../messaging-extensions/how-to/add-authentication.md)
* [创建基于操作的邮件扩展](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)

## <a name="next-steps"></a>后续步骤

> [!div class="nextstepaction"]
> [定义搜索命令](../messaging-extensions/how-to/search-commands/define-search-command.md)

> [!div class="nextstepaction"]
> [响应用户的搜索](../messaging-extensions/how-to/search-commands/respond-to-search.md)