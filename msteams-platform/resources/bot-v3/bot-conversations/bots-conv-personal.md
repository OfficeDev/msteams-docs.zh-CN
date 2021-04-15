---
title: 与机器人的一对一对话
description: 介绍在 Microsoft Teams 中与机器人进行一对一对话的端到端方案
keywords: teams 方案 1on1 1to1 对话机器人
ms.topic: conceptual
ms.date: 05/20/2019
ms.openlocfilehash: 43b44d15b675db2fa6c38d6661858c4e0a595039
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696666"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>与 Microsoft Teams (进行个人) 一对一对话

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams 允许用户与基于 Microsoft Bot Framework 构建的机器人 [直接对话](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true)。 用户可以在发现应用库中找到聊天机器人，并将其添加到个人对话的 Teams 体验中。 团队所有者和具有适当权限的用户还可以将聊天机器人添加为 [团队成员 (请参阅](~/resources/bot-v3/bot-conversations/bots-conv-channel.md) 在团队频道) 中交互，这样不仅可以在团队频道中使用它们，还可用于所有这些用户的个人聊天。

个人聊天与频道中的聊天不同，即用户无需@mention聊天机器人。 如果在个人、 (、群聊或频道等多个上下文中使用自动程序) 则需要检测机器人是否位于群聊或频道中，并处理消息的方式稍为不同。 有关详细信息 [，请参阅在团队频道或群组聊天](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) 中交互。

## <a name="designing-a-great-personal-bot"></a>设计出色的个人机器人

Microsoft Teams 中出色的自动程序可帮助用户获取所需的信息，所有这些信息均在 Teams 体验的上下文中实现。 与机器人的私人对话是机器人及其用户之间的私人交换;它们是在个人上下文中提供特定于用户且与该用户相关的信息的一种很好的方法。 个人聊天中的聊天机器人真正是服务和个人之间的对话，其中群聊或频道中的机器人将一切广播给一组人。

根据你要创建的体验，机器人可能需要在多个范围工作 - 个人、groupChat 和/或团队。 支持多个作用域的工作最少。 在 Teams 中，机器人功能在所有范围内都没有任何预期，但你应确保自动程序有意义，并提供你选择支持的任何 (范围) 价值。

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>最佳做法：个人对话中的欢迎消息

第一 [次](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) 聊天时，自动程序应主动向个人聊天发送欢迎消息 (并且仅在用户首次) 聊天时发送欢迎消息。  (此建议不适用于频道中的第一次) 
