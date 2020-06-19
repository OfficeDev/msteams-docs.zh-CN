---
title: 具有 bot 的1开1对话
description: 介绍与 Microsoft 团队中的 bot 进行1开/1 开对话的端到端方案
keywords: 团队方案 1on1 1to1 对话机器人
ms.date: 05/20/2019
ms.openlocfilehash: e23bb98160125d7fdbb4521467e2f522d6b6ce40
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801018"
---
# <a name="have-a-personal-one-on-one-conversation-with-a-microsoft-teams-bot"></a>与 Microsoft 团队 bot 进行一次个人（一对一）对话

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-bots.md)]

Microsoft 团队允许用户与在[Microsoft Bot 框架](/azure/bot-service/?view=azure-bot-service-3.0)上构建的 bot 进行直接对话。 用户可以在发现应用程序库中找到 bot，并将其添加到他们的团队体验个人对话中。 具有相应权限的团队所有者和用户也可以添加作为团队成员的 bot （请参阅[在团队频道中进行交互](~/resources/bot-v3/bot-conversations/bots-conv-channel.md)），这不仅会使它们在团队的频道中可用，还适用于所有用户的个人聊天。

个人聊天与频道中的聊天不同，因为用户无需 @mention 机器人。 如果在多个上下文（个人、groupChat 或通道）中使用 bot，则需要检测 bot 是否在组聊天或频道中，并以略有不同的方式处理邮件。 有关更多详细信息，请参阅[在团队频道或组聊天中进行交互](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)。

## <a name="designing-a-great-personal-bot"></a>设计极大的个人 bot

Microsoft 团队中的一个很棒的 bot 可帮助用户获取他们所需的信息，所有这些都在团队体验的上下文中。 与 bot 的个人对话是 bot 与其用户之间的专用交换;它们是在个人上下文中提供有关该用户的特定信息和相关信息的好方法。 个人聊天中的 bot 实际上是服务和个人之间的一个对话框，其中群中的 bot 可将所有内容广播给一组用户。

根据您想要创建的体验，自动程序可能需要在多个范围内工作-个人、groupChat 和/或团队。 支持多个作用域的工作最少。 由于你的 bot 在所有作用域中都无法正常运行，团队没有任何预期，但应确保你的 bot 有意义，并在你选择支持的任何范围内提供用户值。

## <a name="best-practice-welcome-messages-in-personal-conversations"></a>最佳实践：个人对话中的欢迎邮件

你的 bot 应在首次（且仅在第一次）用户使用你的 bot 启动个人聊天时主动向个人聊天[发送](~/resources/bot-v3/bot-conversations/bots-conv-proactive.md)欢迎消息。 （此推荐不适用于频道中的首次联系人。）
