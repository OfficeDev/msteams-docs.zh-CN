---
title: 将租户 ID 和对话 ID 发送到机器人的请求标头
description: 在本模块中，了解如何将租户 ID 和会话 ID 发送到 Teams 中机器人的请求标头。
ms.topic: conceptual
ms.localizationpriority: medium
ms.openlocfilehash: b292db11ced764bbe235bee0f6f8f4829ba7b6c9
ms.sourcegitcommit: ffc57e128f0ae21ad2144ced93db7c78a5ae25c4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2022
ms.locfileid: "66503772"
---
# <a name="request-headers-of-the-bot"></a>请求自动程序的标题

当前对机器人的传出请求在标头或 URL 中不包含任何有助于机器人在不解压缩整个有效负载的情况下路由流量的信息。 活动通过类似于 https://<your_domain>/api/messages 的 URL 发送到机器人。 接收请求以在标头中显示对话 ID 和租户 ID。

## <a name="request-header-fields"></a>请求标头字段

对于异步流和同步流，两个非标准请求标头字段将添加到向机器人发送的所有请求。 下表提供了请求标头字段及其值：

| 字段键 | 值 |
|----------------|-----------------|
| x-ms-conversation-id | 与请求活动相对应的对话 ID（如果适用且已确认或已验证）。 |
| x-ms-tenant-id | 与请求活动中的对话相对应的租户 ID。 |

如果活动中不存在租户或会话 ID 或未在服务端进行验证，则该值为空。

![请求标头字段](~/assets/images/bots/requestheaderfields.png)
