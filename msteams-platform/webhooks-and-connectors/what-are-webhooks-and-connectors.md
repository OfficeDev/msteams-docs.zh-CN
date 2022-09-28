---
title: Webhook 和连接器
author: clearab
description: 了解 Webhook 和连接器如何帮助将 Web 服务连接到 Microsoft Teams 中的频道和团队。 了解传入、传出 Webhook 和Office 365连接器。
ms.localizationpriority: high
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 94c84b577dfb20cb823167d3af84f5460bb87554
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100446"
---
# <a name="webhooks-and-connectors"></a>Webhook 和连接器

Webhook 和连接器有助于将 Web 服务连接到 Microsoft Teams 中的频道和团队。 Webhook 是用户定义的 HTTP 回调，用于通知用户在 Teams 频道中发生的任何操作。 这是应用获取实时数据的一种方式。 连接器允许用户订阅以接收来自 Web 服务的通知和消息。 他们为你的服务公开了一个 HTTPS 端点，以卡片的形式发布消息。

> [!IMPORTANT]
> 可以选择生成通知机器人 Teams 应用，而不是传入 Webhook。 它们的性能类似，但通知机器人具有更多功能。 有关详细信息，请参阅 [使用 JavaScript](../sbs-gs-notificationbot.yml) 或 [传入 Webhook 通知示例生成通知](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/incoming-webhook-notification)机器人。 若要开始，请立即下载 [Teams 工具包](https://marketplace.visualstudio.com/items?itemName=TeamsDevApp.ms-teams-vscode-extension) 并浏览。 有关详细信息，请参阅 [Teams 工具包文档](../toolkit/teams-toolkit-fundamentals.md)。

## <a name="outgoing-webhooks"></a>传出 webhook

Webhook 可帮助 Teams 与外部应用集成。 使用传出 Webhook，可以将文本消息从频道发送到 Web 服务。 配置传出 Webhook 后，用户可以 @提及传出 Webhook 并向 Web 服务发送消息。 该服务在 10 秒内使用文本或卡片响应消息。

> [!NOTE]
> 传出 Webhook 是根据每个团队配置的，不能作为常规 Teams 应用的一部分包含在内。

## <a name="connectors"></a>连接器

连接器允许用户订阅以接收来自 Web 服务的通知和消息。 它们公开服务的 HTTPS 终结点，以便将消息发布到 Teams 频道，通常采用卡片形式。

### <a name="incoming-webhooks"></a>传入 webhook

传入的 Webhook 有助于将消息从应用发布到 Teams。 如果在任何频道中为团队启用了传入 Webhook，则会公开 HTTPS 终结点，该终结点接受格式正确的 JSON 并将消息插入到该通道中。 例如，可以在 DevOps 通道中创建传入 Webhook，配置生成，并同时部署和监视服务以发送警报。

#### <a name="notification-bot-or-incoming-webhook---choose-the-right-one"></a>通知机器人或传入 Webhook - 选择正确的

在开始了解如何生成传入 Webhook 之前，你可能还想知道可以使用 Teams 工具包生成通知机器人。 通知机器人可以启用更可自定义的体验，以满足不同的业务方案。

详细了解通知机器人和传入 Webhook 之间的差异，以便为方案选择正确的解决方案：

| &nbsp; | 通知机器人 |  传入 Webhook |
| --- | --- | --- |
| 这是什么？ | Teams 应用 | Teams 功能 |
| 需要安装 | 是 | 否 |
| 合适的方案 | • 定期接收定期通知和消息，例如，接收团队任务的每日通知。 <br>  • 根据真实事件接收通知和消息。 例如，一旦团队成员上传文件，就会收到通知。 | 与外部应用通信，并接收来自其他应用的通知和消息。 |
| 范围配置 | • Teams 频道 <br> • 群组聊天 <br> • 个人聊天 | Teams 频道 |
| 消息进程 | 通知机器人可用作 Teams 应用程序。 可以定义业务逻辑，以处理数据并以自定义格式显示数据。 | Webhook 是 Teams 功能，而不是 Teams 应用程序，因此它只接收和显示数据而不进行处理。 |
| 检索 Teams 上下文 | 通知机器人可以检索 Teams 上下文，例如频道或用户信息、消息等。 | 否 |
| 发送自适应卡片 | 是 | 是 |
| 发送欢迎消息 | 可以发送欢迎消息 | 无欢迎消息 |
| 支持触发器 | 支持的所有触发器。 如果使用 Teams 工具包，可以使用以下触发器快速获取模板项目： <br> • Azure 函数上托管的时间触发器。 <br> • 在 Azure 应用服务上托管的 Restify HTTP 触发器 <br> • 托管在Azure Functions上的 HTTP 触发器 | 支持的所有触发器 |
| 生成工具 | • [Teams 工具包概述Visual Studio Code](../toolkit/teams-toolkit-fundamentals.md) <br> • [Visual Studio 的 Teams 工具包概述](../toolkit/teams-toolkit-fundamentals.md) <br> • [TeamsFx 库](../toolkit/TeamsFx-CLI.md) <br> • [TeamsFx SDK](../toolkit/TeamsFx-SDK.md) | 不需要任何工具 |
| 所需的云资源 | Azure Bot Framework | 不需要资源 |
| 教程 | [使用 JavaScript 生成通知机器人](../sbs-gs-notificationbot.yml) | [传入 Webhook 通知示例](https://github.com/OfficeDev/TeamsFx-Samples/tree/dev/incoming-webhook-notification) |

### <a name="office-365-connectors"></a>Office 365 连接器

Office 365 连接器允许你为传入 Webhook 创建自定义配置页，并将其打包为 Teams 应用的一部分。 你主要使用 Office 365 连接器卡发送邮件，并且能够向其添加一组有限的卡片操作。 例如，一个天气连接器，允许用户选择一个位置和一天中的任何时间，以接收有关明天天气的更新。 它们是在频道级别配置的，但安装在团队级别。

> [!NOTE]
> 可以将 Office 365 连接器 Teams 应用分发到 AppStore。

## <a name="create-and-send-messages"></a>创建和发送邮件

可操作邮件允许用户在不离开其电子邮件客户端的情况下采取措施，从而增加用户参与度。 使用 Office 365 和传入 Webhook，可以通过将 JSON 有效负载发布到 Webhook URL 来发送消息。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建传出 Webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)

## <a name="see-also"></a>另请参阅

* [创建传入 Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [创建 Office 365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [创建和发送邮件](~/webhooks-and-connectors/how-to/connectors-using.md)
* [使用 JavaScript 生成通知机器人](../sbs-gs-notificationbot.yml)
* [使用 JavaScript 生成第一个机器人应用](../sbs-gs-bot.yml)
