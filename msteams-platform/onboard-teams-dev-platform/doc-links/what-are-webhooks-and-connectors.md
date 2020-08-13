---
title: 什么是 webhook 和连接器？
author: clearab
description: 了解 webhook 和连接器如何将您的 web 服务连接到团队客户端。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 740806e43af94d5a5da876affec2070a5a461b11
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651876"
---
# <a name="what-are-webhooks-and-connectors"></a>什么是 webhook 和连接器？

Webhook 和连接器是使用 Microsoft 团队频道和聊天连接外部系统和服务的简单方法。

例如，用户可以从其他应用订阅通知 (通常采用卡片) 形式。

## <a name="incoming-webhooks"></a>传入 webhook

传入 webhook 是最简单的连接器类型，以及将团队的通道连接到外部服务的快速而简单的方式。 对于为该团队) 启用的任何频道 (，您可以公开一个 HTTPS 终结点，该终结点接受正确格式化的 JSON 并在通道中插入邮件。

请参阅[创建传入 webhook](~/webhooks-and-connectors/how-to/add-incoming-webhook.md)。

### <a name="user-scenarios"></a>用户方案

传入 webhook 最适用于特定团队特有的方案。 例如，可以在 DevOps 通道中创建传入 webhook，并将生成、部署和监视服务配置为发送警报。

## <a name="office-365-connectors"></a>Office 365 连接器

Office 365 连接器允许您为传入的 webhook 创建自定义配置页，并将其打包为团队应用程序的一部分。 然后，可以将该应用更广泛地分发到应用商店。 您主要使用 Office 365 连接器卡发送邮件，这些卡也可以具有一组有限的卡片操作。 它们在频道级别上配置，但在团队级别安装。

请参阅[创建 Office 365 连接器](~/webhooks-and-connectors/how-to/connectors-creating.md)。

### <a name="user-scenarios"></a>用户方案

一个天气连接器，可让你选择一天的位置和时间接收有关明天的预测的更新。

## <a name="outgoing-webhooks"></a>传出 webhook

传出 webhook 允许用户向 web 服务发送来自频道的短信。 配置完成后，用户可以 @mention 您的应用程序并向外部服务发送邮件。 服务有5秒的时间向邮件发送响应，可能包含文本或卡。

传出 webhook 是基于每个团队配置的，不能作为普通团队应用程序的一部分包括在内。

请参阅[创建传出 webhook](~/webhooks-and-connectors/how-to/add-outgoing-webhook.md)。

### <a name="user-scenarios"></a>用户方案

传出 webhook 最适合用于完成不需要收集或交换大量信息的特定于团队的工作流。

## <a name="learn-more"></a>了解详细信息

* [规划应用程序](../../concepts/extensibility-points.md)
* [生成应用程序](../../concepts/building-an-app.md)
* [发布应用程序](../../concepts/deploy-and-publish/overview.md)
