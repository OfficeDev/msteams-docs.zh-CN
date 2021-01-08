---
title: 自动程序基础知识
author: clearab
description: 了解 Teams 中机器人的基础知识。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 43dd351b30fdba3435d39aca43aae0f2de00ed24
ms.sourcegitcommit: d0e71ea63af2f67eba75ba283ec46cc7cdf87d75
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/24/2020
ms.locfileid: "49731956"
---
# <a name="bot-basics"></a>自动程序基础知识

这是基于核心 Bot Framework 文档中[](https://aka.ms/how-bots-work)自动程序如何工作的文章构建[的简介](https://aka.ms/azure-bot-service-docs)。 您可能会发现该文章以及"概念"部分的其他文章很有用。

为 Microsoft Teams 开发的自动程序的主要区别在于如何处理活动。 Microsoft Teams 活动处理程序派生自 Bot Framework 的活动处理程序，用于路由所有 Teams 活动，然后再允许处理任何特定于 Teams 的活动。

## <a name="teams-activity-handlers"></a>Teams 活动处理程序

当 Microsoft Teams 自动程序收到活动时，它会将活动传递给 *其活动处理程序*。 其中，有一个称为轮转处理程序的基本处理程序，所有活动都通过该处理程序进行路由。 轮 *转处理程序* 调用所需的活动处理程序以处理收到的任何类型的活动。 为 Microsoft Teams 设计的自动程序的不同是它派生自从 `TeamsActivityHandler` Bot Framework 的类派生 `ActivityHandler` 的类。

# <a name="c"></a>[C#](#tab/csharp)

与使用 Microsoft Bot Framework 创建的任何自动程序一样，如果机器人收到消息活动，轮转处理程序将看到传入活动并将其发送到 `OnMessageActivityAsync` 活动处理程序。 在 Teams 中，此功能保持不变。 如果机器人收到对话更新活动，轮机处理程序将看到传入活动并将其发送到 `OnConversationUpdateActivityAsync` 。 *Teams* 活动处理程序，将首先检查任何 Teams 特定事件，如果未找到任何事件，则传递到 Bot Framework 的活动处理程序。

在 Teams 活动处理程序类中，有两个主要的 Teams 活动处理程序，可路由所有对话更新活动，并路由 `OnConversationUpdateActivityAsync` `OnInvokeActivityAsync` 所有 Teams 调用活动。

若要为 Teams 特定活动处理程序实现逻辑，你将在自动程序中替代这些方法，如下面的自动程序逻辑 [部分所示](#bot-logic) 。 对于其中每个处理程序，没有基本实现，因此只需在替代中添加想要的逻辑。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

与使用 Microsoft Bot Framework 创建的任何自动程序一样，如果机器人收到消息活动，轮转处理程序将看到传入活动并将其发送到 `onMessage` 活动处理程序。 在 Teams 中，此功能保持不变。 如果机器人收到对话更新活动，轮机处理程序将看到传入活动并将其发送到 `dispatchConversationUpdateActivity` 。 *Teams* 活动处理程序，将首先检查任何 Teams 特定事件，如果未找到任何事件，则传递到自动程序框架活动处理程序。

在 Teams 活动处理程序类中，有两个主要的 Teams 活动处理程序，可路由所有对话更新 `dispatchConversationUpdateActivity` 活动，并路由所有 Teams `onInvokeActivity` 调用活动。

若要为 Teams 特定活动处理程序实现逻辑，你将在自动程序中替代这些方法，如"自动程序逻辑"[部分所述。](#bot-logic) 对于其中每个处理程序，请定义自动程序逻辑，然后 **确保在 `next()` 末尾进行调用**。 通过 `next()` 调用，可确保下一个处理程序运行。

# <a name="python"></a>[Python](#tab/python)

自动程序是使用 Microsoft Bot Framework 创建的，如果这些机器人收到消息活动，则轮转处理程序将收到该传入活动的通知。 然后，轮转处理程序将传入活动发送到 `on_message_activity` 活动处理程序。 在 Teams 中，此功能保持不变。 如果机器人收到对话更新活动，则轮转处理程序将收到该传入活动的通知，并将传入活动发送到 `on_conversation_update_activity` 。 Teams 活动处理程序将首先检查任何 Teams 特定事件。 如果未找到任何事件，它将将它们传递到 Bot Framework 的活动处理程序。

在 Teams 活动处理程序类中，有两个主要的 Teams 活动处理程序和 `on_conversation_update_activity` `on_invoke_activity` 。 `on_conversation_update_activity` 路由所有对话更新活动 `on_invoke_activity` ，并路由所有 Teams 调用活动。

若要为 Teams 特定活动处理程序实现逻辑，你需要在自动程序中替代这些方法，如"自动程序逻辑" [部分](#bot-logic) 所示。 这些处理程序没有基本实现，因此，你需要在替代中添加所需的逻辑。

---

## <a name="bot-logic"></a>自动程序逻辑

机器人逻辑处理来自一个或多个自动程序通道的传入活动，并生成传出活动作为响应。  从 Teams 活动处理程序类派生的机器人仍然如此，该类首先检查 Teams 活动，然后将所有其他活动传递给自动程序框架活动处理程序。

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

下面介绍的所有活动处理程序将继续像处理非 Teams 机器人一样工作，除了处理成员添加和成员删除活动外，这些处理程序在团队的上下文中将有所不同，其中新成员将添加到团队而不是消息线程。

下面概述了其中定义的 `ActivityHandler` 处理程序：

| 事件 | 处理程序 | 说明 |
| :-- | :-- | :-- |
| 接收的任何活动类型 | `OnTurnAsync` | 根据收到的活动类型调用其他处理程序之一。 |
| 接收的邮件活动 | `OnMessageActivityAsync` | 重写它以处理 `Message` 活动。 |
| 收到的对话更新活动 | `OnConversationUpdateActivityAsync` | 在活动中，如果除自动程序成员外的成员加入或 `ConversationUpdate` 离开对话，则调用处理程序。 |
| 非自动程序成员加入对话 | `OnMembersAddedAsync` | 重写此关系以处理加入对话的成员。 |
| 非机器人成员离开对话 | `OnMembersRemovedAsync` | 重写此关系以处理成员离开对话。 |
| 接收的事件活动 | `OnEventActivityAsync` | 在 `Event` 活动中，调用特定于事件类型的处理程序。 |
| 收到的令牌响应事件活动 | `OnTokenResponseEventAsync` | 重写它以处理令牌响应事件。 |
| 收到的非令牌响应事件活动 | `OnEventAsync` | 重写它以处理其他类型的事件。 |
| 收到的其他活动类型 | `OnUnrecognizedActivityTypeAsync` | 重写它以处理任何活动类型，否则未经处理。 |

#### <a name="teams-specific-handlers"></a>特定于 Teams 的处理程序

扩展 `TeamsActivityHandler` 了上述处理程序列表，以包括以下内容：

| 事件 | 处理程序 | 说明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | 重写此规则以处理正在创建的 Teams 频道。 有关详细信息，请参阅[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[中创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | 重写此规则以处理要删除的 Teams 频道。 有关详细信息，请参阅 [对话更新](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) 事件 [中删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | 重写它以处理正在重命名的 Teams 频道。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) 重命名 [的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` 重写它以处理正在重命名的 Teams 团队。 有关详细信息，请参阅 [对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 重命名 [的团队](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersAdded | `OnTeamsMembersAddedAsync` | 在 `OnMembersAddedAsync` 中调用方法 `ActivityHandler` 。 重写此规则以处理加入团队的成员。 有关详细信息，请参阅[在对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)[中添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | 在 `OnMembersRemovedAsync` 中调用方法 `ActivityHandler` 。 重写此规则以处理离开团队的成员。 有关详细信息，请参阅 [对话更新事件中删除](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) 的 [团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|

#### <a name="teams-invoke-activities"></a>Teams 调用活动

下面是从 Teams 活动处理程序调用的所有 `OnInvokeActivityAsync` _Teams_ 活动处理程序的列表：

| 调用类型                    | 处理程序                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | Teams 卡片操作调用。 |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | Teams 文件同意接受。 |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | Teams 文件许可。 |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | Teams 文件许可。 |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | Teams O365 连接器卡片操作。 |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | Teams 登录验证状态。 |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | Teams 任务模块提取。 |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | Teams 任务模块提交。 |

上面列出的调用活动适用于 Teams 中的对话机器人。 Bot Framework SDK 还支持特定于消息传递扩展的调用。 有关详细信息，请参阅 [什么是邮件扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)

# <a name="javascript"></a>[JavaScript](#tab/javascript)

下面描述的所有活动处理程序将继续像处理非 Teams 自动程序一样工作，除了处理添加的成员和成员删除的活动外，这些处理程序在团队的上下文中有所不同，其中新成员将添加到团队而不是消息线程。

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

下面概述了其中定义的 `ActivityHandler` 处理程序。

| 事件 | 处理程序 | 说明 |
| :-- | :-- | :-- |
| 接收的任何活动类型 | `onTurn` | 根据收到的活动类型调用其他处理程序之一。 |
| 接收的邮件活动 | `onMessage` | 为此提供一个函数以处理 `Message` 活动。 |
| 收到的对话更新活动 | `onConversationUpdate` | 在活动中，如果除自动程序成员外的成员加入或 `ConversationUpdate` 离开对话，则调用处理程序。 |
| 非自动程序成员加入对话 | `onMembersAdded` | 为此提供一个函数来处理加入对话的成员。 |
| 非机器人成员离开对话 | `onMembersRemoved` | 为此提供一个函数来处理离开对话的成员。 |
| 接收的事件活动 | `onEvent` | 在 `Event` 活动中，调用特定于事件类型的处理程序。 |
| 收到的令牌响应事件活动 | `onTokenResponseEvent` | 为此提供一个函数以处理令牌响应事件。 |
| 收到的其他活动类型 | `onUnrecognizedActivityType` | 为此提供一个函数来处理任何活动类型，否则未经处理。 |
| 活动处理程序已完成 | `onDialog` | 为此提供一个函数，以处理应在其余活动处理程序完成后在轮转结束时完成的任何处理。 |

#### <a name="teams-specific-handlers"></a>特定于 Teams 的处理程序

扩展 `TeamsActivityHandler` 了核心聊天机器人框架处理程序部分中的处理程序列表，以包括以下内容：

| 事件 | 处理程序 | 说明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | 重写此规则以处理正在创建的 Teams 频道。 有关详细信息，请参阅[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[中创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | 重写此规则以处理要删除的 Teams 频道。 有关详细信息，请参阅 [对话更新](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) 事件 [中删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | 重写它以处理正在重命名的 Teams 频道。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) 重命名 [的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` 重写它以处理正在重命名的 Teams 团队。 有关详细信息，请参阅 [对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 重命名 [的团队](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| MembersAdded | `OnTeamsMembersAddedAsync` | 在 `OnMembersAddedAsync` 中调用方法 `ActivityHandler` 。 重写此规则以处理加入团队的成员。 有关详细信息，请参阅[在对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)[中添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | 在 `OnMembersRemovedAsync` 中调用方法 `ActivityHandler` 。 重写此规则以处理离开团队的成员。 有关详细信息，请参阅 [对话更新事件中删除](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) 的 [团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |

#### <a name="teams-invoke-activities"></a>Teams 调用活动

下面是从 Teams 活动处理程序调用的所有 `onInvokeActivity` Teams 活动处理程序的列表：

| 调用类型                    | 处理程序                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | Teams 卡片操作调用。 |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | Teams 文件同意接受。 |
| fileConsent/invoke              | `handleTeamsFileConsent`            | Teams 文件许可。 |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | Teams 文件许可。 |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | Teams O365 连接器卡操作。 |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | Teams 登录验证状态。 |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | Teams 任务模块提取。 |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | Teams 任务模块提交。 |

Teams 调用活动部分中列出的调用活动适用于 Teams 中的对话机器人。 Bot Framework SDK 还支持调用特定于邮件扩展的活动。 有关详细信息，请参阅 [什么是邮件扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)。

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

>[!NOTE]
> 除了添加和删除的成员的活动之外，本节中所述的所有活动处理程序将继续像使用非 Teams 自动程序一样工作。

活动处理程序在团队上下文中有所不同，其中，将新成员添加到团队，而不是消息线程。

其中定义的处理程序列表 `ActivityHandler` 包括：

| 事件 | 处理程序 | 说明 |
| :-- | :-- | :-- |
| 接收的任何活动类型 | `on_turn` | 根据收到的活动类型调用其他处理程序之一。 |
| 接收的邮件活动 | `on_message_activity` | 重写它以处理 `Message` 活动。 |
| 收到的对话更新活动 | `on_conversation_update_activity` | 如果除机器人成员外的成员加入或离开对话，请调用处理程序。 |
| 非自动程序成员加入对话 | `on_members_added_activity` | 重写此关系以处理加入对话的成员。 |
| 非机器人成员离开对话 | `on_members_removed_activity` | 重写此关系以处理离开对话的成员。 |
| 接收的事件活动 | `on_event_activity` | 调用特定于事件类型的处理程序。 |
| 收到的令牌响应事件活动 | `on_token_response_event` | 重写它以处理令牌响应事件。 |
| 收到的非令牌响应事件活动 | `on_event` | 重写它以处理其他类型的事件。 |
| 收到的其他活动类型 | `on_unrecognized_activity_type` | 重写它以处理任何未处理的活动类型。 |

#### <a name="teams-specific-handlers"></a>特定于 Teams 的处理程序

扩展 `TeamsActivityHandler` 了核心聊天机器人框架处理程序部分中的处理程序列表，以包括以下内容：

| 事件 | 处理程序 | 说明 |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | 替代此设置以处理正在创建的 Teams 频道。 有关详细信息，请参阅对话[更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)[中创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。 |
| channelDeleted | `on_teams_channel_deleted` | 重写此规则以处理要删除的 Teams 频道。 有关详细信息，请参阅对话 [更新](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted) 事件 [中删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| channelRenamed | `on_teams_channel_renamed` | 替代它以处理正在重命名的 Teams 频道。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed) 重命名 [的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;` 替代它以处理正在重命名的 Teams 团队。 有关详细信息，请参阅对话 [更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed) 重命名 [的团队](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersAdded | `on_teams_members_added` | 在 `OnMembersAddedAsync` 中调用方法 `ActivityHandler` 。 重写此规则以处理加入团队的成员。 有关详细信息，请参阅["对话更新"事件中添加](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)[的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|
| MembersRemoved | `on_teams_members_removed` | 在 `OnMembersRemovedAsync` 中调用方法 `ActivityHandler` 。 重写此规则以处理离开团队的成员。 有关详细信息，请参阅 [对话更新事件中删除](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed) 的 [团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events)。|

#### <a name="teams-invoke-activities"></a>Teams 调用活动

从 Teams 活动处理程序调用的 `on_invoke_activity` Teams 活动处理程序列表包括：

| 调用类型                    | 处理程序                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | Teams 卡片操作调用。 |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | Teams 文件同意接受。 |
| fileConsent/invoke              | `on_teams_file_consent`            | Teams 文件许可。 |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | Teams 文件许可拒绝。 |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | Teams O365 连接器卡操作。 |
| signin/verifyState              | `on_teams_signin_verify_state`      | Teams 登录验证状态。 |
| task/fetch                      | `on_teams_task_module_fetch`        | Teams 任务模块提取。 |
| task/submit                     | `on_teams_task_module_submit`       | Teams 任务模块提交。 |

Teams 调用活动部分中列出的调用活动适用于 Teams 中的对话机器人。 Bot Framework SDK 还支持调用特定于邮件扩展的活动。 有关详细信息，请参阅 [什么是邮件扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)。

---
