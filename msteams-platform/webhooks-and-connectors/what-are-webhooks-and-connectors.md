---
title: Webhook 和连接器
author: clearab
description: 了解 webhook 和连接器如何将 Web 服务连接到 Teams 客户端。
ms.localizationpriority: medium
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 3b7dd6b907ec1af0467c40bda53422cc75e503bc
ms.sourcegitcommit: 8feddafb51b2a1a85d04e37568b2861287f982d3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2021
ms.locfileid: "59475754"
---
# <a name="webhooks-and-connectors"></a>Webhook 和连接器

Webhook 和连接器有助于将 Web 服务连接到 Microsoft Teams。 Webhook 是用户定义的 HTTP 回调，用于通知用户有关在 Microsoft Teams 通道中发生的任何操作。 它是应用获取实时数据的方法。 连接器允许用户订阅以接收来自 Web 服务的通知和消息。 它们公开你的服务的 HTTPS 终结点，以卡片形式发布消息。

## <a name="outgoing-webhooks"></a>传出 Webhook

Webhook 可帮助Teams外部应用集成。 使用传出 Webhook，您可以将短信从频道发送到 Web 服务。 配置传出 Webhook 后，用户可以@mention传出 Webhook 并将消息发送到 Web 服务。 该服务在十秒钟内使用文本或卡片对邮件做出响应。

> [!NOTE]
> 传出 Webhook 基于每个团队进行配置，不能作为常规 webhook 应用的一Teams一部分。

## <a name="connectors"></a>连接器

连接器允许用户订阅从 Web 服务接收通知和消息。 它们公开服务的 HTTPS 终结点，以将消息Teams通道，通常采用卡片形式。

### <a name="incoming-webhooks"></a>传入 Webhook

传入 Webhook 可帮助将邮件从应用发布到Teams。 如果在任何频道中为团队启用了传入 Webhook，它将公开 HTTPS 终结点，该终结点接受格式正确的 JSON 并将消息插入到该通道中。 例如，可以在客户端通道DevOps传入 Webhook，配置生成，并同时部署和监视服务以发送警报。

### <a name="office-365-connectors"></a>Office 365 连接器

Office 365连接器允许你为传入 Webhook 创建自定义配置页，并打包它们作为 Teams 应用的一部分。 你主要使用 Office 365 连接器卡发送邮件，并且能够向这些连接器卡添加一组有限的卡片操作。 例如，天气连接器允许用户选择一个位置和一天中的某个时间，以接收有关明天天气的更新。 它们在频道级别配置，但安装在团队级别。

> [!NOTE]
> 可以将 Office 365 连接器Teams应用程序分发到我们的 AppStore。

## <a name="create-and-send-messages"></a>创建和发送邮件

可操作邮件允许用户在不离开其电子邮件客户端的情况下采取措施，从而增加用户参与度。 使用 Office 365 和传入 Webhook，可以通过将 JSON 有效负载发布到 webhook URL 来发送消息。

## <a name="see-also"></a>另请参阅

* [创建传入 Webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)
* [创建 Office 365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)
* [创建和发送邮件](~/webhooks-and-connectors/how-to/connectors-using.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [创建传出 Webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)
