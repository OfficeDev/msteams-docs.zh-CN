---
title: 将租户 ID 和对话 ID 发送到机器人的请求标头
description: 介绍如何将租户 ID 和对话 ID 发送到机器人的请求标头。
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: b3938b3011e09016f8594b2b17ba627d4922947b
ms.sourcegitcommit: 35bc2a31b92f3f7c6524373108f095a870d9ad09
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/21/2021
ms.locfileid: "51922523"
---
# <a name="send-tenant-id-and-conversation-id-to-the-request-headers-of-the-bot"></a>将租户 ID 和对话 ID 发送到机器人的请求标头

当前向自动程序发出的传出请求在标头或 URL 中不包含任何有助于机器人在不解压缩整个负载的情况下路由流量的信息。 活动通过类似于 https：//<your_domain>/api/messages 的 URL 发送给机器人。 收到在标头中显示对话 ID 和租户 ID 的请求。

## <a name="request-header-fields"></a>请求头字段

对于异步流和同步流，两个非标准请求头字段将添加到发送到自动程序的所有请求中。 下表提供了请求标头字段及其值。

| 字段键 | 值 |
|----------------|-----------------|
| x-ms-conversation-id | 与请求活动对应的对话 ID（如果适用，经确认或验证）。 |
| x-ms-tenant-id | 与请求活动中的对话对应的租户 ID。 |

如果租户或对话 ID 不存在于活动中，或者未在服务端进行验证，则值为空。

![请求头字段](~/assets/images/bots/requestheaderfields.png)
