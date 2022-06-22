---
title: Webhook 和连接器
author: clearab
description: 在此模块中，了解 Webhook 和连接器如何将 Web 服务连接到 Teams 客户端。
ms.localizationpriority: high
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: fc65046c0bcbecb6ed4c0f15ea81beac77195256
ms.sourcegitcommit: 7bbb7caf729a00b267ceb8af7defffc91903d945
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/21/2022
ms.locfileid: "66190036"
---
# <a name="webhooks-and-connectors"></a>Webhook 和连接器

Webhook 和连接器有助于将 Web 服务连接到 Microsoft Teams 中的频道和团队。 Webhook 是用户定义的 HTTP 回调，用于通知用户在 Teams 频道中发生的任何操作。 这是应用获取实时数据的一种方法。 连接器允许用户订阅以接收来自 Web 服务的通知和消息。 他们为你的服务公开了一个 HTTPS 端点，以卡片的形式发布消息。

## <a name="outgoing-webhooks"></a>传出 webhook

Webhook 可帮助 Teams 与外部应用集成。 使用传出 Webhook，可以将文本消息从频道发送到 Web 服务。 配置传出 Webhook 后，用户可以 @提及传出 Webhook 并向 Web 服务发送消息。 该服务在十秒内使用文本或卡片的方式响应消息。

> [!NOTE]
> 传出 Webhook 是根据每个团队配置的，不能作为常规 Teams 应用的一部分包含在内。

## <a name="connectors"></a>连接器

连接器允许用户订阅以接收来自 Web 服务的通知和消息。 它们公开服务的 HTTPS 终结点，以便将消息发布到 Teams 频道，通常采用卡片形式。

### <a name="incoming-webhooks"></a>传入 webhook

传入的 Webhook 有助于将消息从应用发布到 Teams。 如果在任何频道中为团队启用了传入 Webhook，则会公开 HTTPS 终结点，该终结点接受格式正确的 JSON 并将消息插入到该通道中。 例如，可以在 DevOps 通道中创建传入 Webhook，配置生成，并同时部署和监视服务以发送警报。

### <a name="office-365-connectors"></a>Office 365 连接器

Office 365 连接器允许你为传入 Webhook 创建自定义配置页，并将其打包为 Teams 应用的一部分。 你主要使用 Office 365 连接器卡发送邮件，并且能够向其添加一组有限的卡片操作。 例如，一个天气连接器，允许用户选择一个位置和一天中的某个时间，以接收有关明天天气的更新。 它们是在频道级别配置的，但安装在团队级别。

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
