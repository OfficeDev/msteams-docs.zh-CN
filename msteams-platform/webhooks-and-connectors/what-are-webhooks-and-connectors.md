---
title: 什么是 Webhook 和连接器？
author: surbhigupta
description: 了解 webhook 和连接器如何将 Web 服务连接到 Teams 客户端。
localization_priority: Normal
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 3e8105c9f069428bf93fb9bc2533895878f5ded1
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069043"
---
# <a name="what-are-webhooks-and-connectors"></a>什么是 Webhook 和连接器？

Webhook 和连接器是将 Web 服务连接到 Microsoft Teams 中的频道和团队的一种简单方法。 

## <a name="outgoing-webhooks"></a>传出 webhook

通过传出 webhook，用户可以将文本消息从频道发送到 Web 服务。 配置后，用户将能够@mention发送 Webhook，并发送消息到服务。 你的服务将在五秒钟内发送对邮件的响应，其中可能包含文本或卡片。

传出 Webhook 基于每个团队进行配置，不能作为常规 webhook 应用的一Teams一部分。 它们最适合完成不需要收集或交换大量信息的特定于团队的工作负荷。

有关详细信息，请参阅创建 [传出 Webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)。

## <a name="connectors"></a>连接器

连接器允许用户订阅以接收来自 Web 服务的通知和消息。 它们公开你的服务的 HTTPS 终结点，以将消息张贴到 - 通常采用卡片形式。

### <a name="incoming-webhooks"></a>传入 Webhook

传入 webhook 是最简单的连接器类型。 对于团队策略 (如果已启用该团队) 你可以选择公开接受正确格式的 JSON 的 HTTPS 终结点，并将消息插入到该通道中。 它们是将频道连接到服务的一种快速而简单的方式，并且最适用于特定团队所特有的方案。 例如，可以在客户端通道中创建传入 webhook DevOps配置生成、部署和监控服务以发送警报。

有关详细信息，请参阅创建[传入 Webhook。](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)

### <a name="office-365-connectors"></a>Office 365 连接器

Office 365连接器允许你为传入 Webhook 创建自定义配置页面，将它们打包为 Teams 应用的一部分。 然后，你可以更广泛地分发该应用，甚至分发到我们的应用商店。 你主要使用Office 365连接器卡发送邮件，并且还能够向它们添加一组有限的卡片操作。 例如，天气连接器允许用户选择一天中的位置和时间，以接收有关明天天气的更新。 它们在频道级别配置，但安装在团队级别。

有关详细信息，请参阅创建[Office 365连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)。
