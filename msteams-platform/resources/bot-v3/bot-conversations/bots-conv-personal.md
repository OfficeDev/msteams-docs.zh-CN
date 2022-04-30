---
title: 与机器人的一对一对话
description: 介绍在 Microsoft Teams 中与机器人进行一对一对话的端到端方案
keywords: Teams 方案 1on1 1to1 对话机器人
ms.localizationpriority: high
ms.topic: conceptual
ms.date: 05/20/2019
ms.openlocfilehash: d38285c212416d81a2108524946f0f9732a8dae9
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111939"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>与 Microsoft Teams 机器人进行个人（一对一）对话

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft Teams 允许用户与基于 [Microsoft Bot Framework](/azure/bot-service/?view=azure-bot-service-3.0&preserve-view=true) 构建的机器人进行直接对话。 用户可以在“发现应用”库中查找机器人，并将其添加到 Teams 体验以进行个人对话。 具有相应权限的团队所有者和用户还可以将机器人添加为团队成员。 有关详细信息，请参阅 [团队频道中的交互](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)，这不仅使他们在该团队的频道中可用，而且还可用于个人聊天用户。

个人聊天不同于频道中的聊天，因为用户无需 @提及机器人。 如果在多个上下文中使用机器人，如以下范围中：
* 个人
* 群组聊天
* 频道

你需要检测机器人是否位于群组聊天或频道中，并且处理消息的方式稍有不同。 有关详细信息，请参阅 [在团队频道或群组聊天中交互](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。

## <a name="designing-a-great-personal-bot"></a>设计出色的个人机器人

Microsoft Teams 中出色的机器人可帮助用户获取所需信息，所有这些都位于 Teams 体验的上下文中。 与机器人的个人对话是机器人与其用户之间的私人交流；这是一种在个人上下文中提供用户特定信息和与该用户相关信息的好方法。 个人聊天中的机器人是服务与个人之间的对话框，其中群组聊天或频道中的机器人会将所有内容广播给一组人。

根据要创建的体验，机器人可能需要在多个范围（个人、群组聊天和团队）中工作。 支持多个范围的工作是最少的。 Teams 并不期望机器人可在所有范围中发挥作用，但应确保机器人有意义，并在你选择支持的任何范围内提供用户价值。

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>最佳做法：个人对话中的欢迎消息

在用户首次（并且仅限首次）发起与机器人的个人聊天时，机器人应向个人聊天 [主动发送](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md) 欢迎消息。 此建议不适用于在频道中进行首次联系的情况。
