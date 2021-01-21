---
title: 入门 - 生成邮件扩展
author: heath-hamilton
description: 使用 Microsoft Teams Toolkit 快速创建 Microsoft Teams 消息传递Toolkit。
ms.author: lajanuar
ms.date: 11/04/2020
ms.topic: tutorial
ms.openlocfilehash: 86d44740feaa2cd33aff0e1dde14d757420d90d6
ms.sourcegitcommit: 00c657e3bf57d3b92aca7da941cde47a2eeff4d0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/20/2021
ms.locfileid: "49911917"
---
# <a name="build-a-messaging-extension-for-microsoft-teams"></a>为 Microsoft Teams 构建消息传递扩展

有两种类型的 Teams 应用 *消息传递扩展*：[搜索命令](../messaging-extensions/how-to/search-commands/define-search-command.md)[和操作命令](../messaging-extensions/how-to/action-commands/define-action-command.md)。

在此课程中，你将创建搜索命令 (*也称为* 基于搜索的邮件扩展) ，它是在 Teams 中查找和共享外部内容的快捷方式。 用户可以从 Teams 撰写或命令 [框访问搜索命令](../messaging-extensions/what-are-messaging-extensions.md)。

## <a name="your-assignment"></a>你的作业

组织的技术支持通过 Teams 与用户进行通信，但票证位于单独的系统中。 这意味着支持人员必须不断在应用之间来回切换。 你将调查如何通过为 Teams 创建简单的基于搜索的消息扩展来减少此上下文切换。

## <a name="what-youll-learn"></a>您将了解哪些知识

> [!div class="checklist"]
>
> * 使用 Microsoft Teams Toolkit for Visual Studio Code 创建应用项目和消息传递扩展机器人
> * 确定应用配置和一些与邮件扩展相关的基架
> * 在本地托管应用
> * 为邮件扩展配置自动程序
> * 在 Teams 中旁加载和测试消息传递扩展

## <a name="before-you-begin"></a>准备工作

如果尚未安装，请确保了解并 [安装 Teams 开发先决条件](build-first-app-overview.md#get-prerequisites)。

## <a name="1-create-your-app-project"></a>1. 创建应用项目

Microsoft Teams Toolkit可帮助你为邮件扩展设置以下组件：

* **与邮件扩展相关的** 应用配置和基架
* **自动** 注册到 Microsoft Azure 自动程序服务的邮件扩展的自动程序

> [!TIP]
> 如果你之前尚未创建 Teams 应用项目，你可能会发现按照这些说明更详细地解释项目会[](../build-your-first-app/build-and-run.md)很有帮助。

1. 在Visual Studio代码中，选择左侧活动栏上的 **Microsoft Teams，** :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 然后选择 **"创建新的 Teams 应用"。**
1. 当系统提示时，使用 Microsoft 365 开发帐户登录。
1. 在"**添加功能"** 屏幕上，选择 **"消息扩展**"，然后选择"**下一步"。**
1. 输入 Teams 应用的名称。  (这是应用的默认名称，也是本地计算机上应用项目目录的名称。) 
1. 在 **"配置邮件扩展** "屏幕上，执行以下操作：
    1. 仅选择 **邮件扩展类型的** 基于搜索的选项。
    1. 选择 **"新建自动程序**，**然后创建自动程序注册"。** 如果成功，你的新自动 **程序将具有** 注册状态。
    1. 现在 **，为链接** 取消链接选项选择"否"。
1. 选择 **屏幕** 底部的"完成"以配置项目。

## <a name="2-identify-relevant-app-project-components"></a>2. 确定相关应用程序项目组件

使用 Teams 解决方案创建项目时，会自动设置大部分应用配置和基架Toolkit。

### <a name="app-configurations"></a>应用配置

若要查看或更新邮件扩展的配置，请在工具包中选择 App **Studio，** 然后转到 **邮件扩展**。

### <a name="app-scaffolding"></a>应用基架

应用基架提供了一个文件，该文件位于项目的根目录中，用于处理邮件扩展 (或技术上，邮件扩展的自动程序) 如何响应 Teams 中的搜索查询。 `botActivityHandler.js` [](#4-configure-the-bot-for-your-messaging-extension)

## <a name="3-set-up-a-secure-tunnel-to-your-app"></a>3. 为应用设置安全隧道

出于测试目的，让我们在本地 Web 服务器上托管邮件扩展， (端口 3978) 。

1. 如果尚未安装，请安装 [ngrok](https://ngrok.com/download)。
1. 在终端中，运行 `ngrok http -host-header=rewrite 3978` 。
1. 例如，复制输出 URL (，) `https://468b9ab725e9.ngrok.io` Teams 需要 HTTPS 连接。

通过此 URL， (需要 HTTPS 连接的 Teams) 将能够通过隧道连接到在端口 `localhost` 3978 (托管应用) 。

## <a name="4-configure-the-bot-for-your-messaging-extension"></a>4. 为邮件扩展配置自动程序

消息传递扩展依赖机器人将用户请求从 Teams 发送到托管服务并处理。 必须在 Azure 自动程序服务中注册自动程序，该服务是在使用 Teams 应用设置应用时Toolkit。

您仍必须指定自动程序终结点 URL，以接收并处理邮件扩展中的搜索查询。 通常，URL 如下所示 `https://HOST_URL/api/messages` 。 可以在工具包中快速配置此功能。

1. 在Visual Studio代码中，选择左侧活动栏上的 **Microsoft Teams，** 然后选择" :::image type="icon" source="../assets/icons/vsc-toolkit.png"::: 打开 Microsoft **Teams** Toolkit。
1. 转到 **"自动>现有自动程序注册** "，然后选择在安装期间创建的自动程序。
1. 在 **Bot 终结点地址** 字段中，输入 ngrok URL (例如，) 自动程序并追加 `https://468b9ab725e9.ngrok.io` `/api/messages` 到其中。

机器人将能够处理邮件扩展中的查询。

## <a name="5-build-and-run-your-app"></a>5. 生成并运行应用

你已设置 URL 来托管邮件扩展，并配置它以处理搜索。 是时候让应用启动并运行了。

1. 在终端中，转到应用项目的根目录并运行 `npm install` 。
1. 运行 `npm start`。

如果成功，你将看到以下消息，指示你的邮件扩展服务正在侦听你的活动 `localhost` ：

`Bot/ME service listening at http://localhost:3978`

## <a name="6-sideload-your-messaging-extension-in-teams"></a>6. 在 Teams 中旁加载邮件扩展

运行消息扩展后，可以在 Teams 中安装它。

> [!TIP]
> 如果你之前没有旁加载 Teams 应用并遇到问题，请按照以下 [说明操作](../build-your-first-app/build-and-run.md#4-sideload-your-app-in-teams)。

1. 在Visual Studio代码中，按 **F5** 键启动 Teams Web 客户端。
1. 在应用安装对话框中，选择 **"为我添加"。**

## <a name="7-test-your-messaging-extension"></a>7. 测试邮件扩展

了解消息扩展在 Teams 聊天中如何工作。

1. 启动新聊天。 在撰写框中 **，选择"** 更多"并选择你刚刚旁加载的邮件 :::image type="icon" source="../assets/icons/teams-client-more.png"::: 扩展应用。
1. 尝试搜索一些 (例如， **票证**) 。 如果你的应用正常工作，你将看到示例搜索结果 (你可以稍后添加自己的) 。<br/>
   :::image type="content" source="../assets/images/build-your-first-app/me-teams-test.png" alt-text="显示如何在 Teams 撰写框中使用基于搜索的消息扩展的屏幕截图。":::

## <a name="well-done"></a>干的好

恭喜！ 你拥有一个基本的 Teams 消息传递扩展，该扩展设置为在撰写或命令框中搜索外部内容。

## <a name="next-steps"></a>后续步骤

请参阅以下页面以继续构建功能齐全的邮件扩展：

1. [定义与](../messaging-extensions/how-to/search-commands/define-search-command.md) 服务相关的搜索命令。
1. 配置服务 [以响应用户的搜索](../messaging-extensions/how-to/search-commands/respond-to-search.md)。

## <a name="troubleshooting"></a>疑难解答

如果你在完成本教程时出问题，以下信息可能会有所帮助。

### <a name="bot-isnt-connected-to-teams"></a>自动程序未连接到 Teams

如果你安装了应用，但它无法工作，请确保消息扩展的机器人已连接到 Azure Bot 服务的 [Teams *频道*](https://docs.microsoft.com/azure/bot-service/channel-connect-teams?view=azure-bot-service-4.0&preserve-view=true)。

了解这与 Teams 中的频道不同，了解这一点很重要。 在这种情况下，频道是 Azure 自动程序服务如何将机器人连接到 Teams 或其他受支持的 [Microsoft 或第三方通信应用](https://docs.microsoft.com/azure/bot-service/bot-service-channels-reference?view=azure-bot-service-4.0&preserve-view=true)。

## <a name="learn-more"></a>了解详细信息

* [包含链接取消链接功能](../messaging-extensions/how-to/link-unfurling.md)
* 遵循 [我们的设计准则，](../messaging-extensions/design/messaging-extension-design.md) 使用 [生产就绪 UI](../concepts/design/design-teams-app-ui-templates.md) 模板生成，以创建无缝体验。
* [添加身份验证](../messaging-extensions/how-to/add-authentication.md)
* [创建基于操作的邮件扩展](../messaging-extensions/how-to/action-commands/define-action-command.md)
* [Microsoft Bot Framework](https://dev.botframework.com/)
