---
title: 对话基础知识
description: 对话简介
ms.topic: overview
ms.author: anclear
localization_priority: Normal
keyword: conversations basics messages
ms.openlocfilehash: 886c2764c2d8dceecb0f6a0e960b3487d9360c3682e46c9a8098f6fb8a2876bf
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2021
ms.locfileid: "57705859"
---
# <a name="conversation-basics"></a>对话基础知识

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

对话是在自动程序与一Microsoft Teams用户之间发送的一系列消息。 下表提供了三种类型的对话，也称为Teams：

| 对话类型 | 说明 |
| ------- | ----------- |
| `channel` | 此对话类型对频道的所有成员可见。 |
| `personal` | 此对话类型包括机器人和单个用户之间的对话。 |
| `groupChat` | 此对话类型包括机器人与两个或多个用户之间的聊天。 它还可在会议聊天中启用机器人。 |

自动程序的行为方式有所不同，具体取决于它涉及的对话：

* 在频道和群聊对话中的机器人要求用户@提及机器人来在频道中调用它。

* 一对一对话中的聊天机器人不需要@mention。 用户发送的所有消息将路由到自动程序。

> [!NOTE]
> 自动程序可以接收团队中所有频道消息，而无需@mentioned RSC 权限 (特定) 消息。 此功能目前仅适用于公共 [开发人员预览](../../../resources/dev-preview/developer-preview-intro.md) 版。 有关详细信息，请参阅使用 [RSC 接收所有频道消息](channel-messages-with-rsc.md)。

若要使机器人能够处理特定对话或范围，在应用清单 中添加对此 [范围的支持](~/resources/schema/manifest-schema.md)。

自动程序对话中每条消息都是 `Activity` 一个类型 为 的对象 `messageType: message` 。 当用户发送消息时，Teams自动程序处理该邮件。 此外，若要定义自动程序响应的核心命令，可以添加命令菜单以及自动程序命令的下拉列表。 组或频道中的聊天机器人仅在被提及时接收@botname。 Teams在自动程序处于活动状态的范围中发生的对话事件向机器人发送通知。 可以在代码中捕获这些事件，然后对它们采取措施。

机器人还可以向用户发送主动消息。 主动消息是自动程序发送的任何不响应用户请求的消息。 你可以设置自动程序消息的格式，以包含包含交互式元素（如按钮、文本、图像、音频、视频等）的丰富卡片。 自动程序可以在发送邮件后动态更新消息，而不是将消息作为数据的静态快照。 也可使用 Bot Framework 的方法删除 `DeleteActivity` 邮件。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [智能机器人对话中的邮件](~/bots/how-to/conversations/conversation-messages.md)
