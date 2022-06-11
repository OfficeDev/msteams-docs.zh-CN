---
title: 智能机器人活动处理程序
author: surbhigupta
description: 了解 Teams 中的机器人活动处理程序。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
keywords: 活动处理程序框架机器人卡同意通道事件
ms.openlocfilehash: 8bf1638274c8d83c8483df13556927d98b4d8cb5
ms.sourcegitcommit: 12510f34b00bfdd0b0e92d35c8dbe6ea1f6f0be2
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/11/2022
ms.locfileid: "66032919"
---
# <a name="bot-activity-handlers"></a>智能机器人活动处理程序

本文档基于[机器人如何在](https://aka.ms/how-bots-work)核心[Bot Framework 中运行文档](https://aka.ms/azure-bot-service-docs)中的文章生成。 为 Microsoft Teams 开发的机器人与核心 Bot Framework 之间的主要区别在于 Teams 中提供的功能。

若要为机器人组织聊天逻辑，请使用活动处理程序。 使用 Teams 活动处理程序和机器人逻辑以两种方式处理活动。 Teams 活动处理程序添加了对特定于 Microsoft Teams 事件和交互的支持。 机器人对象包含轮次的会话推理或逻辑，并公开轮次处理程序，该处理程序是可以接受来自机器人适配器的传入活动的方法。

## <a name="teams-activity-handlers"></a>Teams 活动处理程序

Teams 活动处理程序派生自 Microsoft Bot Framework 的活动处理程序。 它会先路由所有 Teams 活动，然后再允许处理任何非 Teams 特定的活动。

当机器人Teams收到活动时，它会路由到活动处理程序。 所有活动都通过一个称为轮次处理程序的基本处理程序进行路由。 轮次处理程序调用所需的活动处理程序来管理收到的任何活动。 Teams 机器人派生自 `TeamsActivityHandler` 类，此类派生自 Bot Framework 的 `ActivityHandler` 类。

> [!NOTE]
> 如果机器人活动需要超过 15 秒才能处理，Teams向机器人终结点发送重试请求。 因此，机器人中会看到重复的请求。

# <a name="c"></a>[C#](#tab/csharp)

机器人是使用 Bot Framework 创建的。 如果机器人收到消息活动，则轮次处理程序会收到此传入活动的通知。 然后，轮次处理程序将传入活动发送到 `OnMessageActivityAsync` 活动处理程序。 在 Teams 中，此功能保持不变。 如果机器人收到会话更新活动，轮次处理程序将收到该传入活动的通知，并将传入活动发送到 `OnConversationUpdateActivityAsync`。 Teams 活动处理程序首先检查任何 Teams 特定的事件。 如果未找到任何事件，则会将其传递到 Bot Framework 的活动处理程序。

在 Teams 活动处理程序类中，有两个主要的 Teams 活动处理程序， `OnConversationUpdateActivityAsync` 和 `OnInvokeActivityAsync`。 `OnConversationUpdateActivityAsync` 路由所有会话更新活动， `OnInvokeActivityAsync` 路由所有 Teams 调用活动。

如果要实现特定活动处理程序 Teams 逻辑，必须覆盖机器人中的方法，如[机器人逻辑](#bot-logic)部分所示。 这些处理程序没有基本实现，因此，必须在重写中添加所需的逻辑。

Teams 活动处理程序的代码片段：

`OnTeamsChannelCreatedAsync`

```csharp

protected override Task OnTeamsChannelCreatedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            // Code logic here
        }
```

`OnTeamsChannelDeletedAsync`

```csharp

protected override Task OnTeamsChannelDeletedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
        {
            // Code logic here
        }
```

`OnTeamsChannelRenamedAsync`

```csharp

protected override Task OnTeamsChannelRenamedAsync(ChannelInfo channelInfo, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
  {
   // Code logic here
  }
```

`OnTeamsTeamRenamedAsync`

```csharp

protected override Task OnTeamsTeamRenamedAsync(TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
  {
   // Code logic here
  }
```

`OnTeamsMembersAddedAsync`

```csharp

protected override Task OnTeamsMembersAddedAsync(IList<TeamsChannelAccount> teamsMembersAdded, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken)
  {
   // Code logic here
  }
```

`OnTeamsMembersRemovedAsync`

```csharp

protected override Task OnTeamsMembersRemovedAsync(IList<TeamsChannelAccount> teamsMembersRemoved, TeamInfo teamInfo, ITurnContext<IConversationUpdateActivity> turnContext, CancellationToken cancellationToken);
  {
   // Code logic here
  }
```

# <a name="javascript"></a>[JavaScript](#tab/javascript)

机器人是使用 Bot Framework 创建的。 如果机器人收到消息活动，则轮次处理程序会收到此传入活动的通知。 然后，轮次处理程序将传入活动发送到 `onMessage` 活动处理程序。 在 Teams 中，此功能保持不变。 如果机器人收到会话更新活动，轮次处理程序将收到该传入活动的通知，并将传入活动发送到 `dispatchConversationUpdateActivity`。 Teams 活动处理程序首先检查任何 Teams 特定的事件。 如果未找到任何事件，则会将其传递到 Bot Framework 的活动处理程序。

在 Teams 活动处理程序类中，有两个主要的 Teams 活动处理程序， `dispatchConversationUpdateActivity` 和 `onInvokeActivity`。 `dispatchConversationUpdateActivity` 路由所有会话更新活动， `onInvokeActivity` 路由所有 Teams 调用活动。

如果要实现特定活动处理程序 Teams 逻辑，必须覆盖机器人中的方法，如[机器人逻辑](#bot-logic)部分所示。 为这些处理程序定义机器人逻辑，然后确保在最后调用 `next()`。 通过调用 `next()`，可确保下一个处理程序运行。

Teams 活动处理程序的代码片段：

`OnTeamsChannelCreatedAsync`

```javascript

onTeamsChannelCreated(async (channelInfo, teamInfo, context, next) => {
       // code for handling
        await next()
    });
```

`OnTeamsChannelDeletedAsync`

```javascript

onTeamsChannelDeleted(async (channelInfo, teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsChannelRenamedAsync`

```javascript

onTeamsChannelRenamed(async (channelInfo, teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsTeamRenamedAsync`

```javascript

onTeamsTeamRenamedAsync(async (teamInfo, context, next) => {
       // code for handling
       await next()
    });
```

`OnTeamsMembersAddedAsync`

```javascript

onTeamsMembersAdded(async (membersAdded, teamInfo, context, next) => {
       // code for handling
    await next();
    });
```

`OnTeamsMembersRemovedAsync`

```javascript

onTeamsMembersRemoved(async (membersRemoved, teamInfo, context, next) => {
       // code for handling
    await next();
    });
```

# <a name="python"></a>[Python](#tab/python)

机器人是使用 Bot Framework 创建的。 如果机器人收到消息活动，则轮次处理程序会收到此传入活动的通知。 然后，轮次处理程序将传入活动发送到 `on_message_activity` 活动处理程序。 在 Teams 中，此功能保持不变。 如果机器人收到会话更新活动，轮次处理程序将收到该传入活动的通知，并将传入活动发送到 `on_conversation_update_activity`。 Teams 活动处理程序首先检查任何 Teams 特定的事件。 如果未找到任何事件，则会将其传递到 Bot Framework 的活动处理程序。

在 Teams 活动处理程序类中，有两个主要的 Teams 活动处理程序， `on_conversation_update_activity` 和 `on_invoke_activity`。 `on_conversation_update_activity` 路由所有会话更新活动， `on_invoke_activity` 路由所有 Teams 调用活动。

如果要实现特定活动处理程序 Teams 逻辑，必须覆盖机器人中的方法，如[机器人逻辑](#bot-logic)部分所示。 这些处理程序没有基本实现，因此，必须在重写中添加所需的逻辑。

---

## <a name="bot-logic"></a>机器人逻辑

机器人逻辑处理来自一个或多个机器人通道的传入活动，并在响应中生成传出活动。 派生自Teams活动处理程序类的机器人仍然如此，该类首先检查Teams活动。 检查 Teams 活动后，会将所有其他活动传递给 Bot Framework 的活动处理程序。

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

>[!NOTE]
>
>* 除 **已添加** 和 **已删除** 成员的活动外，本部分中介绍的所有活动处理程序继续与非 Teams 机器人一样运行。
>* `onInstallationUpdateActivityAsync()` 方法用于在将机器人添加到 Teams 时获取 Teams 区域设置。

活动处理程序在团队的上下文中有所不同，其中新成员将添加到团队而不是消息线程。

中 `ActivityHandler` 定义的处理程序列表包括以下内容：

| Event | 处理程序 | 说明 |
| :-- | :-- | :-- |
| 收到的任何活动类型 | `OnTurnAsync` | 此方法根据收到的活动类型调用其他处理程序之一。 |
| 收到的消息活动 | `OnMessageActivityAsync` | 可以重写此方法来处理 `Message` 活动。 |
| 收到的对话更新活动 | `OnConversationUpdateActivityAsync` | 如果机器人以外的成员已加入或离开对话，则此方法在活动上 `ConversationUpdate` 调用处理程序。 |
| 非机器人成员加入了对话 | `OnMembersAddedAsync` | 可以重写此方法来处理加入会话的成员。 |
| 非机器人成员离开了对话 | `OnMembersRemovedAsync` | 可以重写此方法来处理离开会话的成员。 |
| 收到的事件活动 | `OnEventActivityAsync` | 此方法在 `Event` 活动上调用特定于事件类型的处理程序。 |
| 收到的令牌响应事件活动 | `OnTokenResponseEventAsync` | 可以重写此方法来处理令牌响应事件。 |
| 收到的非令牌响应事件活动 | `OnEventAsync` | 可以重写此方法来处理其他类型的事件。 |
| 收到的其他活动类型 | `OnUnrecognizedActivityTypeAsync` | 可以重写此方法以处理任何未处理的活动类型。 |

#### <a name="teams-specific-activity-handlers"></a>Teams 特定的活动处理程序

`TeamsActivityHandler` 扩展了核心 Bot Framework 处理程序部分中的处理程序列表，以包括以下内容：

| Event | 处理程序 | 说明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | 可以重写此方法来处理正在创建的 Teams 频道。 有关详细信息，请参阅[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)。 |
| ChannelDeleted | `OnTeamsChannelDeletedAsync` | 可以重写此方法来处理要删除的 Teams 频道。 有关详细信息，请参阅[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | 可以重写此方法以处理要重命名的 Teams 频道。 有关详细信息，请参阅[聊天更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[重命名的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)。|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` 可以重写此方法来处理要重命名的 Teams 团队。 有关详细信息，请参阅 [对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[重命名团队](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)。|
| MembersAdded | `OnTeamsMembersAddedAsync` | 此方法调用 `ActivityHandler` 中的 `OnMembersAddedAsync` 方法。 可以重写此方法来处理加入团队的成员。 有关详细信息，请参阅[会话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)。|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | 此方法调用 `ActivityHandler` 中的 `OnMembersRemovedAsync` 方法。 可以重写该方法来处理离开团队的成员。 有关详细信息，请参阅[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[删除的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)。|

#### <a name="teams-invoke-activities"></a>Teams 调用活动

从`OnInvokeActivityAsync`Teams活动处理程序调用的Teams活动处理程序列表包括：

| 调用类型                    | 处理程序                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | 从连接器接收到卡操作调用活动时，将调用此方法。 |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | 用户接受文件同意卡时，将调用此方法。 |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | 从连接器接收文件同意卡活动时，将调用此方法。 |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | 用户拒绝文件同意卡时，将调用此方法。 |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | 从连接器接收Office 365连接器卡操作活动时，将调用此方法。 |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | 从连接器接收登录验证状态活动时，将调用此方法。 |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | 可在派生类中重写此方法，以便在提取任务模块时提供逻辑。 |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | 可在派生类中重写此方法，以便在提交任务模块时提供逻辑。 |

本部分中列出的 Invoke 活动适用于Teams中的聊天机器人。 Bot Framework SDK 还支持调用特定于消息扩展的活动。 有关详细信息，请参阅[什么是消息扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

>[!NOTE]
> 除 **已添加** 和 **已删除** 成员的活动外，本部分中介绍的所有活动处理程序继续与非 Teams 机器人一样运行。

活动处理程序在团队的上下文中有所不同，其中新成员将添加到团队而不是消息线程。

中 `ActivityHandler` 定义的处理程序列表包括以下内容：

| Event | 处理程序 | 说明 |
| :-- | :-- | :-- |
| 收到的任何活动类型 | `onTurn` | 此方法根据收到的活动类型调用其他处理程序之一。 |
| 收到的消息活动 | `onMessage` | 此方法有助于处理 `Message` 活动。 |
| 收到的对话更新活动 | `onConversationUpdate` | 如果机器人以外的成员已加入或离开对话，则此方法在活动上 `ConversationUpdate` 调用处理程序。 |
| 非机器人成员加入了对话 | `onMembersAdded` | 此方法有助于处理加入会话的成员。 |
| 非机器人成员离开了对话 | `onMembersRemoved` | 此方法有助于处理离开会话的成员。 |
| 收到的事件活动 | `onEvent` | 此方法在 `Event` 活动上调用特定于事件类型的处理程序。 |
| 收到的令牌响应事件活动 | `onTokenResponseEvent` | 此方法有助于处理令牌响应事件。 |
| 收到的其他活动类型 | `onUnrecognizedActivityType` | 此方法有助于处理任何未处理的活动类型。 |

#### <a name="teams-specific-activity-handlers"></a>Teams 特定的活动处理程序

`TeamsActivityHandler` 扩展了核心 Bot Framework 处理程序部分中的处理程序列表，以包括以下内容：

| Event | 处理程序 | 说明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | 可以重写此方法来处理正在创建的 Teams 频道。 有关详细信息，请参阅[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)。 |
| ChannelDeleted | `OnTeamsChannelDeletedAsync` | 可以重写此方法来处理要删除的 Teams 频道。 有关详细信息，请参阅[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | 可以重写此方法以处理要重命名的 Teams 频道。 有关详细信息，请参阅[聊天更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[重命名的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)。 |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;` 可以重写此方法来处理要重命名的 Teams 团队。 有关详细信息，请参阅 [对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[重命名团队](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)。 |
| MembersAdded | `OnTeamsMembersAddedAsync` | 此方法调用 `ActivityHandler` 中的 `OnMembersAddedAsync` 方法。 可以重写此方法来处理加入团队的成员。 有关详细信息，请参阅[会话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)。 |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | 此方法调用 `ActivityHandler` 中的 `OnMembersRemovedAsync` 方法。 可以重写该方法来处理离开团队的成员。 有关详细信息，请参阅[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[删除的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)。 |

#### <a name="teams-invoke-activities"></a>Teams 调用活动

从`onInvokeActivity`Teams活动处理程序调用的Teams活动处理程序列表包括：

| 调用类型                    | 处理程序                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | 从连接器接收到卡操作调用活动时，将调用此方法。 |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | 用户接受文件同意卡时，将调用此方法。 |
| fileConsent/invoke              | `handleTeamsFileConsent`            | 从连接器接收文件同意卡活动时，将调用此方法。 |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | 用户拒绝文件同意卡时，将调用此方法。 |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | 从连接器接收Office 365连接器卡操作活动时，将调用此方法。 |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | 从连接器接收登录验证状态活动时，将调用此方法。 |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | 可在派生类中重写此方法，以便在提取任务模块时提供逻辑。 |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | 可在派生类中重写此方法，以便在提交任务模块时提供逻辑。 |

本部分中列出的调用活动适用于 Teams 中的聊天机器人。 Bot Framework SDK 还支持调用特定于消息扩展的活动。 有关详细信息，请参阅[什么是消息扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)。

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

>[!NOTE]
> 除 **已添加** 和 **已删除** 成员的活动外，本部分中介绍的所有活动处理程序继续与非 Teams 机器人一样运行。

活动处理程序在团队的上下文中有所不同，其中新成员将添加到团队而不是消息线程。

中 `ActivityHandler` 定义的处理程序列表包括以下内容：

| Event | 处理程序 | 说明 |
| :-- | :-- | :-- |
| 收到的任何活动类型 | `on_turn` | 此方法根据收到的活动类型调用其他处理程序之一。 |
| 收到的消息活动 | `on_message_activity` | 可以重写此方法来处理 `Message` 活动。 |
| 收到的对话更新活动 | `on_conversation_update_activity` | 如果机器人以外的成员加入或离开会话，此方法将调用处理程序。 |
| 非机器人成员加入了对话 | `on_members_added_activity` | 可以重写此方法来处理加入会话的成员。 |
| 非机器人成员离开了对话 | `on_members_removed_activity` | 可以重写此方法来处理离开会话的成员。 |
| 收到的事件活动 | `on_event_activity` | 此方法调用特定于事件类型的处理程序。 |
| 收到的令牌响应事件活动 | `on_token_response_event` | 可以重写此方法来处理令牌响应事件。 |
| 收到的非令牌响应事件活动 | `on_event` | 可以重写此方法来处理其他类型的事件。 |
| 收到的其他活动类型 | `on_unrecognized_activity_type` | 可以重写此方法来处理任何未处理的活动类型。 |

#### <a name="teams-specific-activity-handlers"></a>Teams 特定的活动处理程序

`TeamsActivityHandler` 扩展了核心 Bot Framework 处理程序部分内的处理程序列表，以包括以下内容：

| Event | 处理程序 | 说明 |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | 可以重写此方法来处理正在创建的 Teams 频道。 有关详细信息，请参阅[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)。 |
| ChannelDeleted | `on_teams_channel_deleted` | 可以重写此方法来处理要删除的 Teams 频道。 有关详细信息，请参阅[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)。|
| channelRenamed | `on_teams_channel_renamed` | 可以重写此方法以处理要重命名的 Teams 频道。 有关详细信息，请参阅[聊天更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[重命名的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)。|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;` 可以重写此方法来处理要重命名的 Teams 团队。 有关详细信息，请参阅 [对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[重命名团队](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)。|
| MembersAdded | `on_teams_members_added` | 此方法调用 `ActivityHandler` 中的 `OnMembersAddedAsync` 方法。 可以重写此方法来处理加入团队的成员。 有关详细信息，请参阅[会话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)。|
| MembersRemoved | `on_teams_members_removed` | 此方法调用 `ActivityHandler` 中的 `OnMembersRemovedAsync` 方法。 可以重写该方法来处理离开团队的成员。 有关详细信息，请参阅[对话更新事件](https://aka.ms/azure-bot-subscribe-to-conversation-events)中[删除的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)。|

#### <a name="teams-invoke-activities"></a>Teams 调用活动

从`on_invoke_activity`Teams活动处理程序调用的Teams活动处理程序列表包括：

| 调用类型                    | 处理程序                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | 从连接器接收到卡操作调用活动时，将调用此方法。 |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | 用户接受文件同意卡时，将调用此方法。 |
| fileConsent/invoke              | `on_teams_file_consent`            | 从连接器接收文件同意卡活动时，将调用此方法。 |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | 用户拒绝文件同意卡时，将调用此方法。 |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | 从连接器接收Office 365连接器卡操作活动时，将调用此方法。 |
| signin/verifyState              | `on_teams_signin_verify_state`      | 从连接器接收登录验证状态活动时，将调用此方法。 |
| task/fetch                      | `on_teams_task_module_fetch`        | 可在派生类中重写此方法，以便在提取任务模块时提供逻辑。 |
| task/submit                     | `on_teams_task_module_submit`       | 可在派生类中重写此方法，以便在提交任务模块时提供逻辑。 |

本部分中列出的调用活动适用于 Teams 中的聊天机器人。 Bot Framework SDK 还支持调用特定于消息扩展的活动。 有关详细信息，请参阅[什么是消息扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)。

---

---

现在你已经熟悉了机器人活动处理程序，让我们看看机器人的行为方式如何根据聊天及其接收或发送的消息而有所不同。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [对话基础知识](~/bots/how-to/conversations/conversation-basics.md)
