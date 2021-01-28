---
title: 自动程序基础知识
author: clearab
description: 了解 Teams 中机器人的基础知识。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 3c4e707fa4677c2441f348e8d09ecf4428ef1296
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014500"
---
# <a name="bot-basics"></a>自动程序基础知识

本文档介绍 Microsoft Teams 中的机器人，这些机器人基于核心 Bot [](https://aka.ms/how-bots-work) Framework 文档中的机器人工作[方式一文构建](https://aka.ms/azure-bot-service-docs)。 为 Microsoft Teams 开发的机器人和核心 Bot Framework 之间的主要区别在于 Teams 中提供的功能。

## <a name="teams-activity-handlers"></a>Teams 活动处理程序

Teams 活动处理程序派生自 Microsoft Bot Framework 的活动处理程序。 它先路由所有 Teams 活动，然后再允许处理任何特定于 Teams 的活动。

当 Teams 自动程序收到活动时，它被定向到 *活动处理程序*。 所有活动都通过一个称为轮转处理程序的基本 *处理程序进行路由*。 轮 *转处理程序* 调用所需的活动处理程序来管理收到的任何活动。 Teams 自动程序派生自 `TeamsActivityHandler` 类，该类派生自 Bot Framework 的 `ActivityHandler` 类。

# <a name="c"></a>[C#](#tab/csharp)

自动程序是使用 Bot Framework 创建的。 如果机器人收到消息活动，则轮转处理程序将收到该传入活动的通知。 然后，轮转处理程序将传入活动发送到 `OnMessageActivityAsync` 活动处理程序。 在 Teams 中，此功能保持不变。 如果机器人收到对话更新活动，则轮转处理程序将收到该传入活动的通知，并将传入活动发送到 `OnConversationUpdateActivityAsync` 。 Teams 活动处理程序首先检查任何 Teams 特定事件。 如果未找到任何事件，它会将它们传递给 Bot Framework 的活动处理程序。

在 Teams 活动处理程序类中，有两个主要的 Teams 活动处理程序和 `OnConversationUpdateActivityAsync` `OnInvokeActivityAsync` 。 `OnConversationUpdateActivityAsync` 路由所有对话更新活动 `OnInvokeActivityAsync` ，并路由所有 Teams 调用活动。

若要实现 Teams 特定活动处理程序的逻辑，必须替代自动程序中的方法，如"自动程序逻辑" [部分](#bot-logic) 所示。 这些处理程序没有基本实现，因此，必须在替代中添加想要的逻辑。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

自动程序是使用 Bot Framework 创建的。 如果机器人收到消息活动，则轮转处理程序将收到该传入活动的通知。 然后，轮转处理程序将传入活动发送到 `onMessage` 活动处理程序。 在 Teams 中，此功能保持不变。 如果机器人收到对话更新活动，则轮转处理程序将收到该传入活动的通知，并将传入活动发送到 `dispatchConversationUpdateActivity` 。 Teams 活动处理程序首先检查任何 Teams 特定事件。 如果未找到任何事件，它会将它们传递给 Bot Framework 的活动处理程序。

在 Teams 活动处理程序类中，有两个主要的 Teams 活动处理程序和 `dispatchConversationUpdateActivity` `onInvokeActivity` 。 `dispatchConversationUpdateActivity` 路由所有对话更新活动 `onInvokeActivity` ，并路由所有 Teams 调用活动。

若要实现 Teams 特定活动处理程序的逻辑，必须替代自动程序中的方法，如"自动程序逻辑" [部分](#bot-logic) 所示。 定义这些处理程序的自动程序逻辑， **然后确保在 `next()` 末尾进行调用**。 通过 `next()` 调用，可确保下一个处理程序运行。

# <a name="python"></a>[Python](#tab/python)

自动程序是使用 Bot Framework 创建的。 如果机器人收到消息活动，则轮转处理程序将收到该传入活动的通知。 然后，轮转处理程序将传入活动发送到 `on_message_activity` 活动处理程序。 在 Teams 中，此功能保持不变。 如果机器人收到对话更新活动，则轮转处理程序将收到该传入活动的通知，并将传入活动发送到 `on_conversation_update_activity` 。 Teams 活动处理程序首先检查任何 Teams 特定事件。 如果未找到任何事件，它会将它们传递给 Bot Framework 的活动处理程序。

在 Teams 活动处理程序类中，有两个主要的 Teams 活动处理程序和 `on_conversation_update_activity` `on_invoke_activity` 。 `on_conversation_update_activity` 路由所有对话更新活动 `on_invoke_activity` ，并路由所有 Teams 调用活动。

若要实现 Teams 特定活动处理程序的逻辑，必须替代自动程序中的方法，如"自动程序逻辑" [部分](#bot-logic) 所示。 这些处理程序没有基本实现，因此，必须在替代中添加想要的逻辑。

---

## <a name="bot-logic"></a>自动程序逻辑

机器人逻辑处理来自一个或多个自动程序通道的传入活动，并响应生成传出活动。 对于从 Teams 活动处理程序类派生的机器人，这一点仍然如此，此类将首先检查 Teams 活动。 检查 Teams 活动后，它会将所有其他活动传递给 Bot Framework 的活动处理程序。

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

>[!NOTE]
> 除了添加 *和**删除* 的成员的活动之外，本节中所述的所有活动处理程序将继续像使用非 Teams 自动程序一样工作。

活动处理程序在团队的上下文中有所不同，其中新成员将添加到团队，而不是消息线程。

其中定义的处理程序列表 `ActivityHandler` 包括：

| 事件 | 处理程序 | 说明 |
| :-- | :-- | :-- |
| 接收的任何活动类型 | `OnTurnAsync` | 此方法根据收到的活动类型调用其他处理程序之一。 |
| 接收的邮件活动 | `OnMessageActivityAsync` | 可以重写此方法以处理 `Message` 活动。 |
| 接收的对话更新活动 | `OnConversationUpdateActivityAsync` | 如果除自动程序成员外的其他成员在活动上加入或离开对话，此方法将调用 `ConversationUpdate` 处理程序。 |
| 非自动程序成员加入对话 | `OnMembersAddedAsync` | 可以重写此方法以处理加入对话的成员。 |
| 非机器人成员离开对话 | `OnMembersRemovedAsync` | 可以重写此方法以处理离开对话的成员。 |
| 接收的事件活动 | `OnEventActivityAsync` | 此方法在活动上调用特定于事件类型的 `Event` 处理程序。 |
| 收到的令牌响应事件活动 | `OnTokenResponseEventAsync` | 可以重写此方法以处理令牌响应事件。 |
| 收到的非令牌响应事件活动 | `OnEventAsync` | 可以重写此方法以处理其他类型的事件。 |
| 收到的其他活动类型 | `OnUnrecognizedActivityTypeAsync` | 可以重写此方法以处理任何活动类型，否则无法处理。 |

#### <a name="teams-specific-activity-handlers"></a>Teams 特定活动处理程序

扩展 `TeamsActivityHandler` 了核心聊天机器人框架处理程序部分中的处理程序列表，以包括以下内容：

| 事件 | 处理程序 | 说明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | 可以重写此方法以处理正在创建的 Teams 频道。 有关详细信息，请参阅对话[更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[中创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | 可以重写此方法以处理要删除的 Teams 频道。 有关详细信息，请参阅对话 [更新](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) 事件 [中删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | 可以重写此方法以处理要重命名的 Teams 频道。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) 重命名 [的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` 可以重写此方法以处理正在重命名的 Teams 团队。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 重命名 [的团队](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersAdded | `OnTeamsMembersAddedAsync` | 此方法在 中 `OnMembersAddedAsync` 调用该方法 `ActivityHandler` 。 可以重写此方法以处理加入团队的成员。 有关详细信息，请参阅[在对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)[中添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | 此方法在 中 `OnMembersRemovedAsync` 调用该方法 `ActivityHandler` 。 可以重写此方法以处理离开团队的成员。 有关详细信息，请参阅 [对话更新事件中删除](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) 的 [团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|

#### <a name="teams-invoke-activities"></a>Teams 调用活动

从 Teams 活动处理程序调用的 `OnInvokeActivityAsync` Teams 活动处理程序列表包括：

| 调用类型                    | 处理程序                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | 从连接器接收卡片操作调用活动时，将调用此方法。 |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | 当用户接受文件同意卡时，将调用此方法。 |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | 从连接器收到文件同意卡活动时，将调用此方法。 |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | 当用户拒绝文件同意卡时，将调用此方法。 |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | 从连接器接收 O365 连接器卡操作活动时，将调用此方法。 |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | 当从连接器收到 signIn 验证状态活动时，将调用此方法。 |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | 可以在派生类中重写此方法，以提供提取任务模块时的逻辑。 |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | 此方法可以在派生类中重写，以提供提交任务模块时的逻辑。 |

本部分中列出的调用活动适用于 Teams 中的对话机器人。 Bot Framework SDK 还支持调用特定于邮件扩展的活动。 有关详细信息，请参阅 [什么是邮件扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

>[!NOTE]
> 除了添加 *和**删除* 的成员的活动之外，本节中所述的所有活动处理程序将继续像使用非 Teams 自动程序一样工作。

活动处理程序在团队上下文中有所不同，其中，将新成员添加到团队，而不是消息线程。

其中定义的处理程序列表 `ActivityHandler` 包括：

| 事件 | 处理程序 | 说明 |
| :-- | :-- | :-- |
| 接收的任何活动类型 | `onTurn` | 此方法根据收到的活动类型调用其他处理程序之一。 |
| 接收的邮件活动 | `onMessage` | 此方法有助于处理 `Message` 活动。 |
| 接收的对话更新活动 | `onConversationUpdate` | 如果除自动程序成员外的其他成员在活动上加入或离开对话，此方法将调用 `ConversationUpdate` 处理程序。 |
| 非自动程序成员加入对话 | `onMembersAdded` | 此方法有助于处理加入对话的成员。 |
| 非机器人成员离开对话 | `onMembersRemoved` | 此方法有助于处理离开对话的成员。 |
| 接收的事件活动 | `onEvent` | 此方法在活动上调用特定于事件类型的 `Event` 处理程序。 |
| 收到的令牌响应事件活动 | `onTokenResponseEvent` | 此方法有助于处理令牌响应事件。 |
| 收到的其他活动类型 | `onUnrecognizedActivityType` | 此方法有助于处理任何活动类型，否则无法处理。 |

#### <a name="teams-specific-activity-handlers"></a>Teams 特定活动处理程序

扩展 `TeamsActivityHandler` 了核心聊天机器人框架处理程序部分中的处理程序列表，以包括以下内容：

| 事件 | 处理程序 | 说明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | 可以重写此方法以处理正在创建的 Teams 频道。 有关详细信息，请参阅对话[更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[中创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | 可以重写此方法以处理要删除的 Teams 频道。 有关详细信息，请参阅对话 [更新](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) 事件 [中删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | 可以重写此方法以处理要重命名的 Teams 频道。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) 重命名 [的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` 可以重写此方法以处理正在重命名的 Teams 团队。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 重命名 [的团队](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| MembersAdded | `OnTeamsMembersAddedAsync` | 此方法在 中 `OnMembersAddedAsync` 调用该方法 `ActivityHandler` 。 可以重写此方法以处理加入团队的成员。 有关详细信息，请参阅[在对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)[中添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | 此方法在 中 `OnMembersRemovedAsync` 调用该方法 `ActivityHandler` 。 可以重写此方法以处理离开团队的成员。 有关详细信息，请参阅 [对话更新事件中删除](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) 的 [团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |

#### <a name="teams-invoke-activities"></a>Teams 调用活动

从 Teams 活动处理程序调用的 `onInvokeActivity` Teams 活动处理程序列表包括：

| 调用类型                    | 处理程序                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | 从连接器接收卡片操作调用活动时，将调用此方法。 |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | 当用户接受文件同意卡时，将调用此方法。 |
| fileConsent/invoke              | `handleTeamsFileConsent`            | 从连接器收到文件同意卡活动时，将调用此方法。 |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | 当用户拒绝文件同意卡时，将调用此方法。 |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | 从连接器接收 O365 连接器卡操作活动时，将调用此方法。 |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | 当从连接器收到 signIn 验证状态活动时，将调用此方法。 |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | 可以在派生类中重写此方法，以提供提取任务模块时的逻辑。 |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | 此方法可以在派生类中重写，以提供提交任务模块时的逻辑。 |

本部分中列出的调用活动适用于 Teams 中的对话机器人。 Bot Framework SDK 还支持调用特定于邮件扩展的活动。 有关详细信息，请参阅 [什么是邮件扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)。

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

>[!NOTE]
> 除了添加 *和**删除* 的成员的活动之外，本节中所述的所有活动处理程序将继续像使用非 Teams 自动程序一样工作。

活动处理程序在团队上下文中有所不同，其中，将新成员添加到团队，而不是消息线程。

其中定义的处理程序列表 `ActivityHandler` 包括：

| 事件 | 处理程序 | 说明 |
| :-- | :-- | :-- |
| 接收的任何活动类型 | `on_turn` | 此方法根据收到的活动类型调用其他处理程序之一。 |
| 接收的邮件活动 | `on_message_activity` | 可以重写此方法以处理 `Message` 活动。 |
| 接收的对话更新活动 | `on_conversation_update_activity` | 如果除机器人成员外的成员加入或离开对话，此方法将调用处理程序。 |
| 非自动程序成员加入对话 | `on_members_added_activity` | 可以重写此方法以处理加入对话的成员。 |
| 非机器人成员离开对话 | `on_members_removed_activity` | 可以重写此方法以处理离开对话的成员。 |
| 接收的事件活动 | `on_event_activity` | 此方法调用特定于事件类型的处理程序。 |
| 收到的令牌响应事件活动 | `on_token_response_event` | 可以重写此方法以处理令牌响应事件。 |
| 收到的非令牌响应事件活动 | `on_event` | 可以重写此方法以处理其他类型的事件。 |
| 收到的其他活动类型 | `on_unrecognized_activity_type` | 可以重写此方法以处理任何未处理的活动类型。 |

#### <a name="teams-specific-activity-handlers"></a>Teams 特定活动处理程序

扩展 `TeamsActivityHandler` 了核心聊天机器人框架处理程序部分中的处理程序列表，以包括以下内容：

| 事件 | 处理程序 | 说明 |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | 可以重写此方法以处理正在创建的 Teams 频道。 有关详细信息，请参阅对话[更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[中创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `on_teams_channel_deleted` | 可以重写此方法以处理要删除的 Teams 频道。 有关详细信息，请参阅对话 [更新](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) 事件 [中删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `on_teams_channel_renamed` | 可以重写此方法以处理要重命名的 Teams 频道。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) 重命名 [的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;` 可以重写此方法以处理正在重命名的 Teams 团队。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 重命名 [的团队](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersAdded | `on_teams_members_added` | 此方法在 中 `OnMembersAddedAsync` 调用该方法 `ActivityHandler` 。 可以重写此方法以处理加入团队的成员。 有关详细信息，请参阅[在对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)[中添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersRemoved | `on_teams_members_removed` | 此方法在 中 `OnMembersRemovedAsync` 调用该方法 `ActivityHandler` 。 可以重写此方法以处理离开团队的成员。 有关详细信息，请参阅 [对话更新事件中删除](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) 的 [团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|

#### <a name="teams-invoke-activities"></a>Teams 调用活动

从 Teams 活动处理程序调用的 `on_invoke_activity` Teams 活动处理程序列表包括：

| 调用类型                    | 处理程序                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | 从连接器接收卡片操作调用活动时，将调用此方法。 |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | 当用户接受文件同意卡时，将调用此方法。 |
| fileConsent/invoke              | `on_teams_file_consent`            | 从连接器收到文件同意卡活动时，将调用此方法。 |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | 当用户拒绝文件同意卡时，将调用此方法。 |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | 从连接器接收 O365 连接器卡操作活动时，将调用此方法。 |
| signin/verifyState              | `on_teams_signin_verify_state`      | 当从连接器收到 signIn 验证状态活动时，将调用此方法。 |
| task/fetch                      | `on_teams_task_module_fetch`        | 可以在派生类中重写此方法，以提供提取任务模块时的逻辑。 |
| task/submit                     | `on_teams_task_module_submit`       | 此方法可以在派生类中重写，以提供提交任务模块时的逻辑。 |

本部分中列出的调用活动适用于 Teams 中的对话机器人。 Bot Framework SDK 还支持调用特定于邮件扩展的活动。 有关详细信息，请参阅 [什么是邮件扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)。

---
