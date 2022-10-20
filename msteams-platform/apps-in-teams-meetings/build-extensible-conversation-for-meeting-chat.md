---
title: 为会议聊天生成可扩展对话
author: v-sdhakshina
description: 本文介绍如何为 Microsoft Teams 与机器人、卡片和消息扩展的会议聊天构建可扩展对话。
ms.topic: conceptual
ms.author: v-sdhakshina
ms.localizationpriority: medium
ms.openlocfilehash: 65fc91d51cd4c740f28d5f33a2ad578f214c20a8
ms.sourcegitcommit: 40d4bde10b6820c62e49e2400b10ab3569c8c815
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/20/2022
ms.locfileid: "68615384"
---
# <a name="build-extensible-conversation-for-meeting-chat"></a>为会议聊天生成可扩展对话

可以在 Microsoft Teams 会议中扩展对话。 可以组合机器人、消息扩展、卡片和任务模块，以提供直观体验。

## <a name="bots"></a>机器人

机器人也称为聊天机器人或对话机器人。 它是一个应用，可由客户服务或支持人员等用户运行简单且重复的任务。 机器人的日常使用包括提供天气信息、预订餐食或提供旅行信息。 与机器人的交互可以是快速问答或复杂的对话。 需要在频道会议的范围和`groupchat`所有其他会议类型的范围中`team`启用机器人。 若要实现机器人，请从 [生成机器人](/microsoftteams/platform//sbs-gs-javascript?tabs=vscode%2Cvsc%2Cviscode)开始。

### <a name="bot-apis"></a>机器人 API

[Bot Framework](https://dev.botframework.com/) 是一个丰富的 SDK，用于使用 C#、Java、Python 和 JavaScript 创建机器人。 如果具有基于 Bot Framework 的机器人，则可以对其进行修改以在 Teams 中工作。 使用 C# 或 Node.js 来利用我们的 [SDK](/microsoftteams/platform/)。

### <a name="code-samples---bots"></a>代码示例 - 机器人

|示例名称 | Description | .NETCore | Node.js | Python |
|----------------|-----------------|--------------|----------------|
| Teams 对话自动程序 | 消息传送和聊天事件处理 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |
|机器人示例 | 机器人示例集  | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python) |

## <a name="message-extensions"></a>消息扩展

消息扩展允许用户通过 Teams 客户端中的按钮和窗体与 Web 服务交互。 用户可以从撰写消息区域、命令框或直接从消息搜索或启动外部系统中的操作。 可以以格式丰富的卡片的形式将该交互的结果发送回 Teams 客户端。 为会议聊天实现消息扩展与定期聊天没有什么不同。 若要实现消息扩展，请从 [消息扩展](/microsoftteams/platform/messaging-extensions/what-are-messaging-extensions?tabs=dotnet)开始。

## <a name="cards-and-task-modules"></a>卡片和任务模块

卡片为用户在对话流中提供各种视频、音频、可选消息以及帮助。 使用任务模块，可以在 Teams 中创建模式弹出体验。 对于启动和完成任务，或者显示视频或 Power 商业智能 (BI) 仪表板之类的丰富信息来说尤其有用。 有关详细信息，请参阅 [生成卡片和任务模块](/microsoftteams/platform/task-modules-and-cards/cards-and-task-modules)。

## <a name="feature-compatibility-by-user-types"></a>按用户类型设置的功能兼容性

下表提供了用户类型，并列出了每个用户可以在会议中访问的功能：

| 用户类型 | 机器人 | 消息扩展 | 自适应卡 | 任务模块 |
| :-- | :-- | :-- | :-- | :-- |
| 租户内用户 | 可用 | 可用 | 可用 | 可用 |
| 来宾，租户 Azure AD 的一部分 | 不可用 | 不可用 | 允许在会议聊天中进行交互。 | 允许从自适应卡片在会议聊天中进行交互。 |
| 联合用户，有关详细信息，请参阅 [非标准用户](/microsoftteams/non-standard-users)。 | 允许交互。 不允许获取、更新和删除。 | 不可用 | 允许在会议聊天中进行交互。 | 允许从自适应卡片在会议聊天中进行交互。 |
| 匿名用户 | 不可用 | 不可用 | 允许在会议聊天中进行交互。 | 不可用 |

## <a name="see-also"></a>另请参阅

* [设计 Microsoft Teams 邮件扩展](../messaging-extensions/design/messaging-extension-design.md)
* [为 Microsoft Teams 应用设计任务模块](../task-modules-and-cards/task-modules/design-teams-task-modules.md)
