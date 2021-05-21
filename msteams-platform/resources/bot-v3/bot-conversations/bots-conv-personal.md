---
title: 与机器人的一对一对话
description: 介绍与自动程序进行一对一对话的端到端Microsoft Teams
keywords: teams 方案 1on1 1to1 对话机器人
localization_priority: Normal
ms.topic: conceptual
ms.date: 05/20/2019
ms.openlocfilehash: dff65e919485eff0443032995b934b7ae93c64eb
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566500"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>与自动 (进行个人) 一对一Microsoft Teams对话

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams允许用户与基于系统构建的机器人进行直接[Microsoft Bot Framework。](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) 用户可以在发现应用库中找到自动程序，并将其添加到个人Teams体验。 团队所有者和具有适当权限的用户还可以将聊天机器人添加为团队成员。 有关详细信息，请参阅在团队频道 [中交互](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)) ，这样不仅可在该团队的频道中使用它们，还可用于所有这些用户的个人聊天。

个人聊天与频道中的聊天不同，即用户无需@mention聊天机器人。 如果在个人、群聊或频道等多个上下文中使用聊天机器人，则需要检测机器人是否位于群聊或频道中，并处理消息的方式稍微有些不同。 有关详细信息，请参阅 [在团队频道或群聊中交互](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。

## <a name="designing-a-great-personal-bot"></a>设计出色的个人机器人

这是一个Microsoft Teams机器人，可帮助用户获取所需的信息，所有这些信息均在 Teams 体验上下文中。 与机器人的私人对话是机器人及其用户之间的私人交换;它们是在个人上下文中提供特定于用户且与该用户相关的信息的一种很好的方法。 个人聊天中的聊天机器人真正是服务和个人之间的对话，其中群聊或频道中的机器人将一切广播给一组人。

根据你要创建的体验，机器人可能需要在多个范围工作 - 个人、群聊和团队。 支持多个作用域的工作最少。 Teams自动程序在所有范围内都运行，但应确保自动程序有意义，并提供你选择支持的任何作用域 (用户) 价值。

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>最佳做法：个人对话中的欢迎消息

第一 [次](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) 聊天时，自动程序应主动向个人聊天发送欢迎消息 (并且仅在用户首次) 聊天时发送欢迎消息。 此建议不适用于频道中的首次联系人。
