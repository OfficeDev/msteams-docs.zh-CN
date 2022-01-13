---
title: " Microsoft Teams 中的自动程序"
author: surbhigupta
description: 自动程序在Microsoft Teams。
ms.topic: overview
ms.localizationpriority: medium
ms.author: anclear
ms.openlocfilehash: a9f53654ba3240b973b77c05cd64a22c80237350
ms.sourcegitcommit: a6c39106ccc002d02a65e11627659e0c48981d8a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/13/2022
ms.locfileid: "62014561"
---
# <a name="bots-in-microsoft-teams"></a> Microsoft Teams 中的自动程序

聊天机器人也称为聊天机器人或对话机器人。 该应用由客户服务或支持人员等用户运行简单而重复的任务。 自动程序的日常使用包括提供有关天气信息的机器人、预订预订或提供旅行信息。 与机器人的交互可以快速提出疑问和回答，也可以是一个复杂的对话。

> [!IMPORTANT]
> 目前，自动程序在 政府社区云 (GCC) 中可用，GCC-High DOD (中不可用) 。

对话机器人允许用户使用文本、交互式卡片和任务模块与 Web 服务交互。

![使用文本调用自动程序](~/assets/images/invokebotwithtext.png)

![使用卡片调用机器人](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

对话机器人非常灵活。 机器人可以处理几个涉及人工智能和自然语言处理的基本命令或复杂任务。 自动程序可以是较大应用程序的一部分，也可以独立。

使用卡片、文本和任务模块的合适组合来创建有用的自动程序。 下图显示了用户在一对一聊天中用文本和交互式卡片与机器人进行对话。

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="常见问题解答自动程序示例" border="true":::

用户和机器人之间的每次交互都表示为活动。 当机器人收到活动时，它会将活动传递给其活动处理程序。 请参阅 [自动程序活动处理程序](~/bots/bot-basics.md)。

机器人是具有对话界面的应用。 可以使用文本、交互式卡片和语音与机器人交互。 机器人在频道或群聊对话以及一对一对话中的行为有所不同。 对话通过 Bot Framework 连接器处理。 请参阅 [对话基础知识](~/bots/how-to/conversations/conversation-basics.md)。

自动程序需要上下文信息（如用户配置文件详细信息）来访问相关内容并增强机器人体验。 请参阅[获取Teams上下文](~/bots/how-to/get-teams-context.md)。

可以使用自动程序 API 或自动程序 API Graph发送和接收Teams文件。 请参阅 [通过自动程序发送和接收文件](~/bots/how-to/bots-filesv4.md)。

速率限制用于优化用于应用程序应用程序的Teams程序。 为了保护Microsoft Teams用户，自动程序 API 为传入请求提供了速率限制。 请参阅[在"配置"中通过速率限制Teams。](~/bots/how-to/rate-limit.md)

借助 Microsoft Graph API 进行呼叫和联机会议，Microsoft Teams应用现在可以使用语音和视频与用户进行交互。 请参阅 [通话和会议机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。

可以使用聊天Teams API 获取聊天或团队成员的信息。 请参阅[对Teams聊天机器人 API 所做的更改，以提取团队或聊天成员](~/resources/team-chat-member-api-changes.md)。

<!--- TBD: For quick scanning, see if the above information can be itemized as a list.
--->

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [智能机器人和 SDK](~/bots/bot-features.md)

## <a name="code-sample"></a>代码示例

|示例名称 | 说明 | C# | Node.js |
|----------------|-----------------|--------------|--------------|
| 自动程序日常任务提醒| 演示如何安排定期任务，以及如何在计划的时间获取提醒。 | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/csharp) | [View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/bot-daily-task-reminder/nodejs) |

## <a name="see-also"></a>另请参阅

* [创建适合 Teams 的机器人](~/bots/how-to/create-a-bot-for-teams.md)
* [为会议注册呼叫和会议Microsoft Teams](~/bots/calls-and-meetings/registering-calling-bot.md)
* [向自动程序Teams身份验证](~/bots/how-to/authentication/add-authentication.md)
* [智能机器人活动处理程序](~/bots/bot-basics.md)
* [Teams 智能机器人中的对话活动](~/bots/how-to/conversations/subscribe-to-conversation-events.md)
