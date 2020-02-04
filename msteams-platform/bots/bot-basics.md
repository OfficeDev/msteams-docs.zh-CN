---
title: 机器人基础知识
author: clearab
description: 了解团队中的 bot 的基础知识。
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: e1b0c79b73ae89c8ab76ba0a1ff045603ab0b932
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673161"
---
# <a name="bot-basics"></a>机器人基础知识

这篇文章介绍了如何在核心[Bot 框架文档](https://aka.ms/azure-bot-service-docs)中[使用 bot 工作](https://aka.ms/how-bots-work)的文章。 您可能会发现，这篇文章以及*概念*部分中的其他文章非常有用。

为 Microsoft 团队开发的 bot 的主要区别在于活动的处理方式。 Microsoft 团队活动处理程序从 Bot 框架的活动处理程序派生，以在允许处理任何非团队特定活动之前路由所有团队活动。

## <a name="teams-activity-handlers"></a>团队活动处理程序

当 Microsoft 团队的 bot 收到活动时，它会将其传递到其*活动处理程序*。 在封面下，有一个称为*turn 处理程序*的基本处理程序，所有活动都通过路由。 *Turn 处理程序*将调用所需的活动处理程序以处理收到的任何类型的活动。 为 Microsoft 团队设计的 bot 的不同之处在于，它是`TeamsActivityHandler`从来自 bot 框架的`ActivityHandler`类派生的类派生而来。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)

与使用 Microsoft Bot 框架创建的任何 bot 一样，如果 bot 收到一条消息活动，则 turn 处理程序会看到传入的活动并将其`OnMessageActivityAsync`发送到活动处理程序。 在团队中，此功能保持不变。 如果 bot 收到对话更新活动，则 turn 处理程序会发现传入的活动并将其发送到`OnConversationUpdateActivityAsync` *团队*活动处理程序，该处理程序将首先检查任何团队特定事件，如果没有找到，则将其传递给 bot 框架的活动处理程序。

在团队活动处理程序类中，有两个主要的团队活动`OnConversationUpdateActivityAsync`处理程序，它们路由所有对话更新`OnInvokeActivityAsync`活动，并路由所有团队调用活动。

若要为工作组特定的活动处理程序实现您的逻辑，您将在您的 bot 中覆盖这些方法，如下面的[bot 逻辑](#bot-logic)部分中所示。 对于上述每个处理程序，都没有基实现，因此只需在替代中添加所需的逻辑即可。

# <a name="javascripttabjavascript"></a>[JavaScript](#tab/javascript)

与使用 Microsoft Bot 框架创建的任何 bot 一样，如果 bot 收到一条消息活动，则 turn 处理程序会看到传入的活动并将其`onMessage`发送到活动处理程序。 在团队中，此功能保持不变。 如果 bot 收到对话更新活动，则 turn 处理程序将看到传入的活动并将其发送到`dispatchConversationUpdateActivity` *团队*活动处理程序，该处理程序将首先检查是否有任何工作组特定事件，如果未找到，则将其传递给 bot 框架活动处理程序。

在团队活动处理程序类中，有两个主要的团队活动`dispatchConversationUpdateActivity`处理程序，它们路由所有对话更新`onInvokeActivity`活动，并路由所有团队调用活动。

若要为工作组特定的活动处理程序实现你的逻辑，你将在你的 bot 中覆盖这些方法，如下面的[bot 逻辑](#bot-logic)部分中所示。 对于每个处理程序，定义您的 bot 逻辑，然后**务必在结尾`next()`处呼叫**。 通过调用`next()` ，可以确保下一个处理程序运行。

---

## <a name="bot-logic"></a>Bot 逻辑

Bot 逻辑处理来自一个或多个机器人频道的传入活动并生成响应中的传出活动。  这仍适用于从团队活动处理程序类派生的 bot，它首先检查团队活动，然后将所有其他活动传递到 bot 框架活动处理程序。

# <a name="ctabcsharp"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>核心 Bot 框架处理程序

以下所述的所有活动处理程序将继续工作，就像处理*添加*的成员和*删除*了活动的成员例外，在团队的上下文中，将新成员添加到团队中，而不是将新成员添加到团队中，而非邮件线程。

中`ActivityHandler`定义的处理程序如下所示。

| 事件 | Handler | 说明 |
| :-- | :-- | :-- |
| 收到的任何活动类型 | `OnTurnAsync` | 根据收到的活动类型调用其他处理程序之一。 |
| 接收的邮件活动 | `OnMessageActivityAsync` | 重写此参数以`Message`处理活动。 |
| 收到对话更新活动 | `OnConversationUpdateActivityAsync` | 在`ConversationUpdate`活动中，如果加入或离开对话之外的其他成员，则调用处理程序。 |
| 加入对话的非 bot 成员 | `OnMembersAddedAsync` | 重写此参数以处理加入对话的成员。 |
| 非机器人成员离开对话 | `OnMembersRemovedAsync` | 重写此参数可处理离开对话的成员。 |
| 接收的事件活动 | `OnEventActivityAsync` | 在`Event`活动中，调用特定于事件类型的处理程序。 |
| 接收的令牌响应事件活动 | `OnTokenResponseEventAsync` | 重写此参数以处理令牌响应事件。 |
| 收到的非令牌响应事件活动 | `OnEventAsync` | 重写此参数可处理其他类型的事件。 |
| 收到的其他活动类型 | `OnUnrecognizedActivityTypeAsync` | 重写此参数以处理未处理的任何活动类型。 |

#### <a name="teams-specific-handlers"></a>特定于团队的处理程序

`TeamsActivityHandler`扩展了上面的处理程序列表，以包含以下内容：

| 事件 | Handler | 说明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | 重写此参数以处理正在创建的团队频道。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | 重写此参数可处理要删除的团队频道。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | 重写此参数可处理要重命名的团队频道。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[重命名的通道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)。|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`重写此参数可处理要重命名的团队团队。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[重命名的团队](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)。|
| MembersAdded | `OnTeamsMembersAddedAsync` | 调用中`OnMembersAddedAsync` `ActivityHandler`的方法。 重写此参数以处理加入团队的成员。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#Team-Member-Added)。|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | 调用中`OnMembersRemovedAsync` `ActivityHandler`的方法。 重写此参数可处理离开团队的成员。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[删除了工作组成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#Team-Member-Removed)。|

#### <a name="teams-invoke--activities"></a>团队调用活动

下面列出了从`OnInvokeActivityAsync` _团队_活动处理程序中调用的所有团队活动处理程序：

| 调用类型                    | Handler                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction               | `OnTeamsCardActionInvokeAsync`       | 团队卡片操作调用。 |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | 团队文件同意接受。 |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | 团队文件许可。 |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | 团队文件许可。 |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | 团队 O365 连接器卡片操作。 |
| 登录/verifyState              | `OnTeamsSigninVerifyStateAsync`      | 团队登录验证状态。 |
| 任务/提取                      | `OnTeamsTaskModuleFetchAsync`        | 团队任务模块提取。 |
| 任务/提交                     | `OnTeamsTaskModuleSubmitAsync`       | 团队任务模块提交。 |

上面列出的调用活动适用于团队中的对话 bot。 Bot 框架 SDK 还支持特定于邮件扩展的调用。 有关详细信息，请参阅[什么是邮件扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)

# <a name="javascripttabjavascript"></a>[JavaScript](#tab/javascript)

以下所述的所有活动处理程序将继续工作，如同处理*添加*的成员和*删除*了成员的活动除外，它们在团队的上下文中是不同的，在这种情况下，新成员将添加到团队中，而不是将新成员添加到团队中，而非邮件线程。

#### <a name="core-bot-framework-handlers"></a>核心 Bot 框架处理程序

中`ActivityHandler`定义的处理程序如下所示。

| 事件 | Handler | 说明 |
| :-- | :-- | :-- |
| 收到的任何活动类型 | `onTurn` | 根据收到的活动类型调用其他处理程序之一。 |
| 接收的邮件活动 | `onMessage` | 为此提供用于处理`Message`活动的函数。 |
| 收到对话更新活动 | `onConversationUpdate` | 在`ConversationUpdate`活动中，如果加入或离开对话之外的其他成员，则调用处理程序。 |
| 加入对话的非 bot 成员 | `onMembersAdded` | 为此提供一个函数来处理加入对话的成员。 |
| 非机器人成员离开对话 | `onMembersRemoved` | 为此提供一个函数来处理离开对话的成员。 |
| 接收的事件活动 | `onEvent` | 在`Event`活动中，调用特定于事件类型的处理程序。 |
| 接收的令牌响应事件活动 | `onTokenResponseEvent` | 为此提供用于处理令牌响应事件的函数。 |
| 收到的其他活动类型 | `onUnrecognizedActivityType` | 为此提供一个函数以处理任何未处理的活动类型。 |
| 活动处理程序已完成 | `onDialog` | 为此提供了一个函数，用于处理在结束时应完成的任何处理，在其余的活动处理程序完成之后。 |

#### <a name="teams-specific-handlers"></a>特定于团队的处理程序

`TeamsActivityHandler`扩展了上面的处理程序列表，以包含以下内容：

| 事件 | Handler | 说明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | 重写此参数以处理正在创建的团队频道。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | 重写此参数可处理要删除的团队频道。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | 重写此参数可处理要重命名的团队频道。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[重命名的通道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)。 |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`重写此参数可处理要重命名的团队团队。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[重命名的团队](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)。 |
| MembersAdded | `OnTeamsMembersAddedAsync` | 调用中`OnMembersAddedAsync` `ActivityHandler`的方法。 重写此参数以处理加入团队的成员。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#Team-Member-Added)。 |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | 调用中`OnMembersRemovedAsync` `ActivityHandler`的方法。 重写此参数可处理离开团队的成员。 有关详细信息，请参阅在[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[删除了工作组成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#Team-Member-Removed)。 |

#### <a name="teams-invoke-activities"></a>团队调用活动

下面列出了从`onInvokeActivity` _团队_活动处理程序中调用的所有团队活动处理程序：

| 调用类型                    | Handler                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction               | `handleTeamsCardActionInvoke`       | 团队卡片操作调用。 |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | 团队文件同意接受。 |
| fileConsent/invoke              | `handleTeamsFileConsent`            | 团队文件许可。 |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | 团队文件许可。 |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | 团队 O365 连接器卡片操作。 |
| 登录/verifyState              | `handleTeamsSigninVerifyState`      | 团队登录验证状态。 |
| 任务/提取                      | `handleTeamsTaskModuleFetch`        | 团队任务模块提取。 |
| 任务/提交                     | `handleTeamsTaskModuleSubmit`       | 团队任务模块提交。 |

上面列出的调用活动适用于团队中的对话 bot。 Bot 框架 SDK 还支持特定于邮件扩展的调用。 有关详细信息，请参阅[什么是邮件扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)

---
