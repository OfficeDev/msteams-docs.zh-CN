---
title: 对话基础知识
description: 在本模块中，了解频道中的机器人聊天类型、个人聊天和 Microsoft Teams 中的群组聊天范围。
ms.topic: overview
ms.author: anclear
ms.localizationpriority: medium
ms.openlocfilehash: ab27bc6000712cd046d92d9e020bfbe8fa65daa0
ms.sourcegitcommit: 84747a9e3c561c2ca046eda0b52ada18da04521d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/31/2022
ms.locfileid: "68791816"
---
# <a name="conversation-basics"></a>对话基础知识

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

对话是在 Microsoft Teams 机器人与一个或多个用户之间发送的一系列消息。 下表提供了三种类型的对话，在 Teams 中也称为范围：

| 对话类型 | 说明 |
| ------- | ----------- |
| `channel` | 此对话类型对频道的所有成员可见。 |
| `personal` | 此会话类型包括机器人与单个用户之间的对话。 |
| `groupChat` | 此对话类型包括机器人与两个或更多用户之间的聊天。 它还可在会议聊天中启用机器人。 |

机器人的行为方式不同，具体取决于它所涉及的对话：

* 在频道和群聊对话中的机器人要求用户@提及机器人来在频道中调用它。

* 一对一对话中的机器人不要求@提及。 用户发送的所有消息都路由到机器人。

> [!NOTE]
> 无需使用特定于资源的许可 (RSC) 权限来@mentioned机器人即可接收团队中的所有通道消息。 此功能目前仅适用于[公共开发人员预览版](../../../resources/dev-preview/developer-preview-intro.md)。 有关详细信息，请参阅[使用 RSC 接收所有频道消息](channel-messages-with-rsc.md)。

若要使机器人在特定会话或范围内工作，请在 [应用清单](~/resources/schema/manifest-schema.md)中添加对该范围的支持。

机器人对话中的每个消息都是 `Activity` 类型的 `messageType: message`对象。 当用户发送消息时，Teams 会将消息发布到机器人，机器人将处理该消息。 此外，若要定义机器人响应的核心命令，可以添加包含机器人命令下拉列表的命令菜单。 组或通道中的机器人仅在@botname提及时接收消息。 对于发生在机器人活动范围内的对话事件，Teams 会向机器人发送通知。 可以在代码中捕获这些事件并对其执行操作。

机器人还可以向用户发送主动消息。 主动消息是由机器人发送的、不响应用户请求的任何消息。 可以设置机器人消息的格式，使其包含包含交互式元素（如按钮、文本、图像、音频、视频等）的富卡。 机器人可以在发送消息后动态更新消息，而不是将消息作为数据的静态快照。 也可以使用 Bot Framework 的 `DeleteActivity` 方法删除消息。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [智能机器人对话中的邮件](~/bots/how-to/conversations/conversation-messages.md)
