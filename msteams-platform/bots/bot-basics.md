---
title: 智能机器人活动处理程序
author: clearab
description: 了解聊天机器人活动处理程序Teams。
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: da770d930ca6d00503c0102f1e683a60161636fd
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020188"
---
# <a name="bot-activity-handlers"></a>智能机器人活动处理程序

本文档基于核心 Bot Framework 文档中 [有关](https://aka.ms/how-bots-work) 机器人 [如何工作的文章](https://aka.ms/azure-bot-service-docs)。 为自动程序开发Microsoft Teams核心 Bot Framework 之间的主要区别在于Teams。

若要组织机器人的对话逻辑，则使用活动处理程序。 使用活动处理程序和自动程序逻辑Teams两种方式处理活动。 活动Teams处理程序添加了对特定于Microsoft Teams事件和交互的支持。 机器人对象包含轮次的对话逻辑或逻辑，并公开一个轮次处理程序，这是可接受来自机器人适配器的传入活动的方法。

## <a name="teams-activity-handlers"></a>Teams活动处理程序

Teams活动处理程序派生自Microsoft Bot Framework的活动处理程序。 它先Teams所有活动，然后再Teams处理任何非活动。

当聊天机器人Teams活动时，它会路由到活动处理程序。 所有活动都通过一个称为轮转处理程序的基本处理程序进行路由。 轮次处理程序调用所需的活动处理程序来管理收到的任何活动。 the Teams bot is derived from `TeamsActivityHandler` class， which is derived from the Bot Framework's `ActivityHandler` class.

# <a name="c"></a>[C#](#tab/csharp)

自动程序是使用 Bot Framework 创建的。 如果机器人收到消息活动，轮机处理程序将接收该传入活动的通知。 然后轮次处理程序将传入活动发送到 `OnMessageActivityAsync` 活动处理程序。 在Teams中，此功能保持不变。 如果机器人收到对话更新活动，则轮机处理程序将接收该传入活动的通知，并将传入活动发送到 `OnConversationUpdateActivityAsync` 。 活动Teams处理程序首先检查特定Teams事件。 如果未找到任何事件，它会将它们传递给 Bot Framework 的活动处理程序。

在Teams处理程序类中，有两个主要Teams活动处理程序和 `OnConversationUpdateActivityAsync` `OnInvokeActivityAsync` 。 `OnConversationUpdateActivityAsync`路由所有对话更新活动 `OnInvokeActivityAsync` ，并路由Teams活动。

若要实现特定活动Teams的逻辑，必须替代自动程序中的方法，如自动程序逻辑[部分](#bot-logic)所示。 这些处理程序没有基本实现，因此，必须在替代中添加想要的逻辑。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

自动程序是使用 Bot Framework 创建的。 如果机器人收到消息活动，轮机处理程序将接收该传入活动的通知。 然后轮次处理程序将传入活动发送到 `onMessage` 活动处理程序。 在Teams中，此功能保持不变。 如果机器人收到对话更新活动，则轮机处理程序将接收该传入活动的通知，并将传入活动发送到 `dispatchConversationUpdateActivity` 。 活动Teams处理程序首先检查特定Teams事件。 如果未找到任何事件，它会将它们传递给 Bot Framework 的活动处理程序。

在Teams处理程序类中，有两个主要Teams活动处理程序和 `dispatchConversationUpdateActivity` `onInvokeActivity` 。 `dispatchConversationUpdateActivity`路由所有对话更新活动 `onInvokeActivity` ，并路由Teams活动。

若要实现特定活动Teams的逻辑，必须替代自动程序中的方法，如自动程序逻辑[部分](#bot-logic)所示。 为这些处理程序定义自动程序逻辑，然后确保在末尾 `next()` 调用。 通过 `next()` 调用 ，可确保下一个处理程序运行。

# <a name="python"></a>[Python](#tab/python)

自动程序是使用 Bot Framework 创建的。 如果机器人收到消息活动，轮机处理程序将接收该传入活动的通知。 然后轮次处理程序将传入活动发送到 `on_message_activity` 活动处理程序。 在Teams中，此功能保持不变。 如果机器人收到对话更新活动，则轮机处理程序将接收该传入活动的通知，并将传入活动发送到 `on_conversation_update_activity` 。 活动Teams处理程序首先检查特定Teams事件。 如果未找到任何事件，它会将它们传递给 Bot Framework 的活动处理程序。

在Teams处理程序类中，有两个主要Teams活动处理程序和 `on_conversation_update_activity` `on_invoke_activity` 。 `on_conversation_update_activity`路由所有对话更新活动 `on_invoke_activity` ，并路由Teams活动。

若要实现特定活动Teams的逻辑，必须替代自动程序中的方法，如自动程序逻辑[部分](#bot-logic)所示。 这些处理程序没有基本实现，因此，必须在替代中添加想要的逻辑。

---

## <a name="bot-logic"></a>自动程序逻辑

机器人逻辑处理来自一个或多个自动程序通道的传入活动，并响应生成传出活动。 对于从活动处理程序类派生的自动程序Teams，它首先检查活动Teams情况。 检查活动Teams，它会将所有其他活动传递给 Bot Framework 的活动处理程序。

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

>[!NOTE]
> 除了添加 **和****删除** 的成员的活动之外，本节中所述的所有活动处理程序将继续像处理非自动程序一样Teams工作。

活动处理程序在团队的上下文中有所不同，其中将新成员添加到团队，而不是消息线程。

中定义的处理程序列表 `ActivityHandler` 包括：

| 事件 | Handler | 说明 |
| :-- | :-- | :-- |
| 接收的任何活动类型 | `OnTurnAsync` | 此方法根据收到的活动类型调用其他处理程序之一。 |
| 收到的邮件活动 | `OnMessageActivityAsync` | 可以重写此方法以处理 `Message` 活动。 |
| 收到的对话更新活动 | `OnConversationUpdateActivityAsync` | 如果活动上除机器人加入或离开对话的成员外，此方法将调用 `ConversationUpdate` 处理程序。 |
| 非自动程序成员已加入对话 | `OnMembersAddedAsync` | 可以重写此方法以处理加入对话的成员。 |
| 非自动程序成员离开对话 | `OnMembersRemovedAsync` | 可以重写此方法以处理离开对话的成员。 |
| 收到的事件活动 | `OnEventActivityAsync` | 此方法在活动上调用特定于事件类型的 `Event` 处理程序。 |
| 收到的令牌响应事件活动 | `OnTokenResponseEventAsync` | 可以重写此方法以处理令牌响应事件。 |
| 收到的非令牌响应事件活动 | `OnEventAsync` | 可以重写此方法以处理其他类型的事件。 |
| 收到的其他活动类型 | `OnUnrecognizedActivityTypeAsync` | 可以重写此方法以处理任何活动类型，否则无法处理。 |

#### <a name="teams-specific-activity-handlers"></a>Teams特定活动处理程序

`TeamsActivityHandler`扩展核心 Bot Framework 处理程序部分中的处理程序列表，以包括以下内容：

| 事件 | Handler | 说明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | 可以重写此方法以处理正在Teams的通道。 有关详细信息，请参阅对话[更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[中创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | 可以重写此方法以处理要Teams的通道。 有关详细信息，请参阅对话[更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)[中删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | 可以重写此方法以处理正在Teams的通道。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) 中 [重命名的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`可以重写此方法以处理正在Teams团队。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 中 [重命名的团队](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersAdded | `OnTeamsMembersAddedAsync` | 此方法在 `OnMembersAddedAsync` 中调用 方法 `ActivityHandler` 。 可以重写 方法以处理加入团队的成员。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)[中添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | 此方法在 `OnMembersRemovedAsync` 中调用 方法 `ActivityHandler` 。 可以重写 方法以处理离开团队的成员。 有关详细信息，请参阅对话[更新事件中删除](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)[的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|

#### <a name="teams-invoke-activities"></a>Teams调用活动

从Teams活动处理程序调用的Teams `OnInvokeActivityAsync` 活动处理程序的列表包括：

| 调用类型                    | Handler                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | 从连接器接收卡片操作调用活动时，将调用此方法。 |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | 当用户接受文件同意卡时，将调用此方法。 |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | 从连接器收到文件同意卡活动时，将调用此方法。 |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | 当用户拒绝文件同意卡时，将调用此方法。 |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | 从连接器接收 O365 连接器卡操作活动时，将调用此方法。 |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | 当 signIn 验证从连接器收到状态活动时，将调用此方法。 |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | 此方法可以在派生类中重写，以提供提取任务模块时的逻辑。 |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | 此方法可以在派生类中重写，以提供提交任务模块时的逻辑。 |

本节中列出的调用活动适用于远程聊天机器人Teams。 Bot Framework SDK 还支持调用特定于消息传递扩展的活动。 有关详细信息，请参阅 [什么是邮件扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

>[!NOTE]
> 除了添加 **和****删除** 的成员的活动之外，本节中所述的所有活动处理程序将继续像处理非自动程序一样Teams工作。

活动处理程序在团队的上下文中有所不同，其中，将新成员添加到团队，而不是消息线程。

中定义的处理程序列表 `ActivityHandler` 包括：

| 事件 | Handler | 说明 |
| :-- | :-- | :-- |
| 接收的任何活动类型 | `onTurn` | 此方法根据收到的活动类型调用其他处理程序之一。 |
| 收到的邮件活动 | `onMessage` | 此方法有助于处理 `Message` 活动。 |
| 收到的对话更新活动 | `onConversationUpdate` | 如果活动上除机器人加入或离开对话的成员外，此方法将调用 `ConversationUpdate` 处理程序。 |
| 非自动程序成员已加入对话 | `onMembersAdded` | 此方法有助于处理加入对话的成员。 |
| 非自动程序成员离开对话 | `onMembersRemoved` | 此方法有助于处理离开对话的成员。 |
| 收到的事件活动 | `onEvent` | 此方法在活动上调用特定于事件类型的 `Event` 处理程序。 |
| 收到的令牌响应事件活动 | `onTokenResponseEvent` | 此方法有助于处理令牌响应事件。 |
| 收到的其他活动类型 | `onUnrecognizedActivityType` | 此方法有助于处理未经处理的任何活动类型。 |

#### <a name="teams-specific-activity-handlers"></a>Teams特定活动处理程序

`TeamsActivityHandler`扩展核心 Bot Framework 处理程序部分中的处理程序列表，以包括以下内容：

| 事件 | Handler | 说明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | 可以重写此方法以处理正在Teams的通道。 有关详细信息，请参阅对话[更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[中创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | 可以重写此方法以处理要Teams的通道。 有关详细信息，请参阅对话[更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)[中删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | 可以重写此方法以处理正在Teams的通道。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) 中 [重命名的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`可以重写此方法以处理正在Teams团队。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 中 [重命名的团队](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| MembersAdded | `OnTeamsMembersAddedAsync` | 此方法在 `OnMembersAddedAsync` 中调用 方法 `ActivityHandler` 。 可以重写 方法以处理加入团队的成员。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)[中添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | 此方法在 `OnMembersRemovedAsync` 中调用 方法 `ActivityHandler` 。 可以重写 方法以处理离开团队的成员。 有关详细信息，请参阅对话[更新事件中删除](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)[的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |

#### <a name="teams-invoke-activities"></a>Teams调用活动

从Teams活动处理程序调用的Teams `onInvokeActivity` 活动处理程序的列表包括：

| 调用类型                    | Handler                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | 从连接器接收卡片操作调用活动时，将调用此方法。 |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | 当用户接受文件同意卡时，将调用此方法。 |
| fileConsent/invoke              | `handleTeamsFileConsent`            | 从连接器收到文件同意卡活动时，将调用此方法。 |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | 当用户拒绝文件同意卡时，将调用此方法。 |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | 从连接器接收 O365 连接器卡操作活动时，将调用此方法。 |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | 当 signIn 验证从连接器收到状态活动时，将调用此方法。 |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | 此方法可以在派生类中重写，以提供提取任务模块时的逻辑。 |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | 此方法可以在派生类中重写，以提供提交任务模块时的逻辑。 |

本节中列出的调用活动适用于远程聊天机器人Teams。 Bot Framework SDK 还支持调用特定于消息传递扩展的活动。 有关详细信息，请参阅 [什么是邮件扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)。

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

>[!NOTE]
> 除了添加 **和****删除** 的成员的活动之外，本节中所述的所有活动处理程序将继续像处理非自动程序一样Teams工作。

活动处理程序在团队的上下文中有所不同，其中，将新成员添加到团队，而不是消息线程。

中定义的处理程序列表 `ActivityHandler` 包括：

| 事件 | Handler | 说明 |
| :-- | :-- | :-- |
| 接收的任何活动类型 | `on_turn` | 此方法根据收到的活动类型调用其他处理程序之一。 |
| 收到的邮件活动 | `on_message_activity` | 可以重写此方法以处理 `Message` 活动。 |
| 收到的对话更新活动 | `on_conversation_update_activity` | 如果除机器人成员外的成员加入或离开对话，此方法将调用处理程序。 |
| 非自动程序成员已加入对话 | `on_members_added_activity` | 可以重写此方法以处理加入对话的成员。 |
| 非自动程序成员离开对话 | `on_members_removed_activity` | 可以重写此方法以处理离开对话的成员。 |
| 收到的事件活动 | `on_event_activity` | 此方法调用特定于事件类型的处理程序。 |
| 收到的令牌响应事件活动 | `on_token_response_event` | 可以重写此方法以处理令牌响应事件。 |
| 收到的非令牌响应事件活动 | `on_event` | 可以重写此方法以处理其他类型的事件。 |
| 收到的其他活动类型 | `on_unrecognized_activity_type` | 可以重写此方法以处理任何未处理的活动类型。 |

#### <a name="teams-specific-activity-handlers"></a>Teams特定活动处理程序

扩展核心 Bot Framework 处理程序部分中的处理程序 `TeamsActivityHandler` 列表，以包括以下内容：

| 事件 | Handler | 说明 |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | 可以重写此方法以处理正在Teams的通道。 有关详细信息，请参阅对话[更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[中创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `on_teams_channel_deleted` | 可以重写此方法以处理要Teams的通道。 有关详细信息，请参阅对话[更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)[中删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `on_teams_channel_renamed` | 可以重写此方法以处理正在Teams的通道。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) 中 [重命名的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;`可以重写此方法以处理正在Teams团队。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 中 [重命名的团队](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersAdded | `on_teams_members_added` | 此方法在 `OnMembersAddedAsync` 中调用 方法 `ActivityHandler` 。 可以重写 方法以处理加入团队的成员。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)[中添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersRemoved | `on_teams_members_removed` | 此方法在 `OnMembersRemovedAsync` 中调用 方法 `ActivityHandler` 。 可以重写 方法以处理离开团队的成员。 有关详细信息，请参阅对话[更新事件中删除](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)[的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|

#### <a name="teams-invoke-activities"></a>Teams调用活动

从Teams活动处理程序调用的Teams `on_invoke_activity` 活动处理程序的列表包括：

| 调用类型                    | Handler                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | 从连接器接收卡片操作调用活动时，将调用此方法。 |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | 当用户接受文件同意卡时，将调用此方法。 |
| fileConsent/invoke              | `on_teams_file_consent`            | 从连接器收到文件同意卡活动时，将调用此方法。 |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | 当用户拒绝文件同意卡时，将调用此方法。 |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | 从连接器接收 O365 连接器卡操作活动时，将调用此方法。 |
| signin/verifyState              | `on_teams_signin_verify_state`      | 当 signIn 验证从连接器收到状态活动时，将调用此方法。 |
| task/fetch                      | `on_teams_task_module_fetch`        | 此方法可以在派生类中重写，以提供提取任务模块时的逻辑。 |
| task/submit                     | `on_teams_task_module_submit`       | 此方法可以在派生类中重写，以提供提交任务模块时的逻辑。 |

本节中列出的调用活动适用于远程聊天机器人Teams。 Bot Framework SDK 还支持调用特定于消息传递扩展的活动。 有关详细信息，请参阅 [什么是邮件扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)。

---

* * *

现在，你已经熟悉自动程序活动处理程序，让我们了解聊天机器人的行为方式，具体取决于对话以及它接收或发送的消息。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [对话基础知识](~/bots/how-to/conversations/conversation-basics.md)
