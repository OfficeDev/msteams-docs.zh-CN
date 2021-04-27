---
title: " Microsoft Teams 中的自动程序"
author: clearab
description: Microsoft Teams 中的聊天机器人概述。
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 70240b7396fc5e7a77749dc4e7326bfb30ea4415
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020889"
---
# <a name="bots-in-microsoft-teams"></a> Microsoft Teams 中的自动程序

聊天机器人也称为聊天机器人或对话机器人，它是运行由用户（如客户服务或支持人员）执行的简单且重复的自动化任务的应用。 日常使用中的机器人示例包括提供有关天气信息的机器人、预订预订或提供旅行信息。 机器人交互可以是一个快速的问题和答案，也可以是提供对服务的访问权限的复杂对话。

> [!VIDEO https://www.youtube-nocookie.com/embed/zSIysk0yL0Q]

会话机器人允许用户通过文本、交互卡和任务模块与 web 服务进行交互。

![使用文本调用自动程序](~/assets/images/invokebotwithtext.png)

![使用卡片调用机器人](~/assets/images/invokebotwithcard.png)

<img src="~/assets/images/task-module-example.png" alt="Invoke bot using task module" width="400"/>

对话机器人非常灵活，并且范围可以处理几个简单的命令，或复杂的、由人工智能支持且自然语言处理任务。 它们可以是较大应用程序的一个方面，也可以完全独立。

找到卡片、文本和任务模块的合适组合是创建有用的自动程序的关键。 下图显示了用户在一对一聊天中同时使用文本和交互式卡片与机器人进行对话：

:::image type="content" source="~/assets/images/FAQPlusEndUser.gif" alt-text="常见问题解答自动程序示例" border="true":::

用户和机器人之间的每次交互都表示为活动。 当机器人收到活动时，它会将活动传递给其活动处理程序。 有关详细信息，请参阅 [自动程序活动处理程序](~/bots/bot-basics.md)。 

此外，机器人是具有对话界面的应用。 可以使用文本、交互式卡片和语音与机器人交互。 根据对话是频道还是群聊对话，还是一对一对话，机器人的行为会有所不同。 对话通过 Bot Framework 连接器处理。 有关详细信息，请参阅 [对话基础知识](~/bots/how-to/conversations/conversation-basics.md)。

自动程序需要上下文信息（如用户配置文件详细信息）来访问相关内容并增强机器人体验。 有关详细信息，请参阅获取 [Teams 上下文](~/bots/how-to/get-teams-context.md)。 

还可使用 Graph API 或 Teams 自动程序 API 通过自动程序发送和接收文件。 有关详细信息，请参阅通过自动 [程序发送和接收文件](~/bots/how-to/bots-filesv4.md)。

此外，速率限制用于优化用于 Teams 应用程序的聊天机器人。 为了保护 Microsoft Teams 及其用户，机器人 API 提供了传入请求的速率限制。 有关详细信息，请参阅在 [Teams 中通过速率限制优化机器人](~/bots/how-to/rate-limit.md)。

借助用于通话和联机会议的 Microsoft Graph API，Microsoft Teams 应用现在可以使用语音和视频与用户进行交互。 有关详细信息，请参阅 [通话和会议机器人](~/bots/calls-and-meetings/calls-meetings-bots-overview.md)。 

可以使用 Teams 机器人 API 获取聊天或团队的一个或多个成员的信息。 有关详细信息，请参阅对 [Teams 自动程序 API 所做的更改，以提取团队或聊天成员](~/resources/team-chat-member-api-changes.md)。

## <a name="see-also"></a>另请参阅

> [!div class="nextstepaction"]
> [创建适合 Teams 的机器人](~/bots/how-to/create-a-bot-for-teams.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [智能机器人和 SDK](~/bots/bot-features.md)
