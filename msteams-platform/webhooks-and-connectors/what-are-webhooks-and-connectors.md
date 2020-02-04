---
title: 什么是 webhook 和连接器？
author: clearab
description: 了解 webhook 和连接器如何将您的 web 服务连接到团队客户端。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 2be6f82bba0efe05a22a8da9da0acc1e0ad6fa00
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41672985"
---
# <a name="what-are-webhooks-and-connectors"></a>什么是 webhook 和连接器？

Webhook 和连接器是将 web 服务连接到 Microsoft 团队中的频道和团队的简单方法。 

## <a name="outgoing-webhooks"></a>传出 webhook

传出 webhook 允许用户向 web 服务发送来自频道的短信。 配置完成后，你的用户将能够 @mention 你的传出 webhook 并向你的服务发送一条消息。 您的服务将有五秒的时间向邮件发送响应，可能包含文本或卡。

传出 webhook 是按每个团队配置的，不能作为普通团队应用程序的一部分包括在内。 它们最适合于完成不需要收集或交换大量信息的特定于团队的工作负载。

请参阅[创建传出 webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)。

## <a name="connectors"></a>连接器

连接器允许用户订阅来自 web 服务的接收通知和消息。 它们公开服务的 HTTPS 终结点，通常以卡片形式发布邮件。

### <a name="incoming-webhooks"></a>传入 webhook

传入的 webhook 是最简单的连接器类型。 对于团队中的任何频道（如果为该工作组启用），可以选择公开 HTTPS 终结点，该终结点将接受正确格式化的 JSON 并将邮件插入到该通道中。 它们是将频道连接到服务的快速、简便的方法，最适用于特定团队特有的方案。 例如，可以在 DevOps 通道中创建一个传入 webhook，并将生成、部署和监控服务配置为发送通知。

请参阅[创建传入 webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)。

### <a name="office-365-connectors"></a>Office 365 连接器

Office 365 连接器允许您为传入的 webhook 创建自定义配置页，并将它们打包为团队应用程序的一部分。 然后，您可以更广泛地分发该应用程序，甚至可以分发到应用商店。 您主要使用 Office 365 连接器卡发送邮件，并且还能够将一组有限的卡片操作添加到其中。 这是一个可供用户选择接收有关明天天气的更新的位置和时间的天气连接器的有用示例。 它们在频道级别上配置，但在团队级别安装。

请参阅[创建 Office 365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)。