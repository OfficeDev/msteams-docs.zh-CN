---
title: 智能机器人活动处理程序
author: surbhigupta
description: 了解Teams中的机器人活动处理程序。
ms.topic: conceptual
ms.localizationpriority: medium
ms.author: anclear
keywords: 活动处理程序框架机器人卡同意通道事件
ms.openlocfilehash: 34dd5e8042b71f4e7cc78df7e7c543c86a53f58e
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104033"
---
# <a name="bot-activity-handlers"></a>智能机器人活动处理程序

本文档基于有关机器人在核心 [Bot Framework 文档](https://aka.ms/azure-bot-service-docs)中[的工作原理](https://aka.ms/how-bots-work)的文章。 为Microsoft Teams开发的机器人与核心 Bot Framework 的主要区别在于Teams中提供的功能。

若要为机器人组织聊天逻辑，请使用活动处理程序。 使用Teams活动处理程序和机器人逻辑以两种方式处理活动。 Teams活动处理程序添加了对特定于Microsoft Teams的事件和交互的支持。 机器人对象包含轮次的会话推理或逻辑，并公开轮次处理程序，即可以接受来自机器人适配器的传入活动的方法。

## <a name="teams-activity-handlers"></a>Teams活动处理程序

Teams活动处理程序派生自Microsoft Bot Framework的活动处理程序。 在允许处理任何非Teams特定活动之前，它会路由所有Teams活动。

当机器人Teams收到活动时，它会路由到活动处理程序。 所有活动都通过一个称为轮次处理程序的基本处理程序路由。 轮次处理程序调用所需的活动处理程序来管理收到的任何活动。 Teams机器人派`TeamsActivityHandler`生自类，类派生自 Bot Framework 的`ActivityHandler`类。

# <a name="c"></a>[C#](#tab/csharp)

机器人是使用 Bot Framework 创建的。 如果机器人收到消息活动，则轮次处理程序将收到该传入活动的通知。 然后，轮次处理程序将传入活动发送到 `OnMessageActivityAsync` 活动处理程序。 在Teams中，此功能保持不变。 如果机器人收到会话更新活动，则轮次处理程序将接收该传入活动的通知，并将传入活动发送到 `OnConversationUpdateActivityAsync`。 Teams活动处理程序首先检查任何Teams特定事件。 如果未找到任何事件，则会将其传递给 Bot Framework 的活动处理程序。

在Teams活动处理程序类中，有两个主要Teams活动处理程序，`OnConversationUpdateActivityAsync`以及 `OnInvokeActivityAsync`。 `OnConversationUpdateActivityAsync`路由所有会话更新活动，并`OnInvokeActivityAsync`路由所有Teams调用活动。

若要实现特定活动处理程序Teams逻辑，必须覆盖机器人中的方法，如[机器人逻辑](#bot-logic)部分所示。 这些处理程序没有基本实现，因此，必须在替代中添加所需的逻辑。

Teams活动处理程序的代码片段：

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

机器人是使用 Bot Framework 创建的。 如果机器人收到消息活动，则轮次处理程序将收到该传入活动的通知。 然后，轮次处理程序将传入活动发送到 `onMessage` 活动处理程序。 在Teams中，此功能保持不变。 如果机器人收到会话更新活动，则轮次处理程序将接收该传入活动的通知，并将传入活动发送到 `dispatchConversationUpdateActivity`。 Teams活动处理程序首先检查任何Teams特定事件。 如果未找到任何事件，则会将其传递给 Bot Framework 的活动处理程序。

在Teams活动处理程序类中，有两个主要Teams活动处理程序，`dispatchConversationUpdateActivity`以及 `onInvokeActivity`。 `dispatchConversationUpdateActivity`路由所有会话更新活动，并`onInvokeActivity`路由所有Teams调用活动。

若要实现特定活动处理程序Teams逻辑，必须覆盖机器人中的方法，如[机器人逻辑](#bot-logic)部分所示。 为这些处理程序定义机器人逻辑，然后确保在末尾调用 `next()` 。 通过调用 `next()` ，可确保下一个处理程序运行。

Teams活动处理程序的代码片段：

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

机器人是使用 Bot Framework 创建的。 如果机器人收到消息活动，则轮次处理程序将收到该传入活动的通知。 然后，轮次处理程序将传入活动发送到 `on_message_activity` 活动处理程序。 在Teams中，此功能保持不变。 如果机器人收到会话更新活动，则轮次处理程序将接收该传入活动的通知，并将传入活动发送到 `on_conversation_update_activity`。 Teams活动处理程序首先检查任何Teams特定事件。 如果未找到任何事件，则会将其传递给 Bot Framework 的活动处理程序。

在Teams活动处理程序类中，有两个主要Teams活动处理程序，`on_conversation_update_activity`以及 `on_invoke_activity`。 `on_conversation_update_activity`路由所有会话更新活动，并`on_invoke_activity`路由所有Teams调用活动。

若要实现特定活动处理程序Teams逻辑，必须覆盖机器人中的方法，如[机器人逻辑](#bot-logic)部分所示。 这些处理程序没有基本实现，因此，必须在替代中添加所需的逻辑。

---

## <a name="bot-logic"></a>机器人逻辑

机器人逻辑处理来自一个或多个机器人通道的传入活动，并在响应中生成传出活动。 从Teams活动处理程序类派生的机器人仍然如此，该类首先检查Teams活动。 检查Teams活动后，它会将所有其他活动传递给 Bot Framework 的活动处理程序。

# <a name="c"></a>[C#](#tab/csharp)

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

>[!NOTE]
>
>* 除 **添加** 和 **删除** 成员的活动外，本部分中描述的所有活动处理程序继续与非Teams机器人一样工作。
>* `onInstallationUpdateActivityAsync()`方法用于在将机器人添加到Teams时获取Teams区域设置。

活动处理程序在团队的上下文中有所不同，其中新成员将添加到团队，而不是消息线程。

中 `ActivityHandler` 定义的处理程序列表包括以下内容：

| Event | 处理器 | 说明 |
| :-- | :-- | :-- |
| 收到的任何活动类型 | `OnTurnAsync` | 此方法根据收到的活动类型调用其他处理程序之一。 |
| 收到的消息活动 | `OnMessageActivityAsync` | 可以重写此方法来处理 `Message` 活动。 |
| 收到的对话更新活动 | `OnConversationUpdateActivityAsync` | 如果机器人以外的成员已加入或离开对话，则此方法在活动上 `ConversationUpdate` 调用处理程序。 |
| 非机器人成员加入了对话 | `OnMembersAddedAsync` | 可以重写此方法来处理加入会话的成员。 |
| 非机器人成员离开对话 | `OnMembersRemovedAsync` | 可以重写此方法来处理离开会话的成员。 |
| 收到的事件活动 | `OnEventActivityAsync` | 此方法对活动调用特定于事件类型的 `Event` 处理程序。 |
| 收到的令牌响应事件活动 | `OnTokenResponseEventAsync` | 可以重写此方法来处理令牌响应事件。 |
| 收到的非令牌响应事件活动 | `OnEventAsync` | 可以重写此方法来处理其他类型的事件。 |
| 收到的其他活动类型 | `OnUnrecognizedActivityTypeAsync` | 可以重写此方法来处理任何活动类型（否则未经处理）。 |

#### <a name="teams-specific-activity-handlers"></a>Teams特定的活动处理程序

扩展 `TeamsActivityHandler` 了核心 Bot Framework 处理程序部分中的处理程序列表，以包括以下内容：

| Event | 处理器 | 说明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | 可以重写此方法来处理正在创建的Teams通道。 有关详细信息，请参阅[在对话更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | 可以重写此方法来处理要删除的Teams通道。 有关详细信息，请参阅[对话更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | 可以重写此方法来处理要重命名的Teams通道。 有关详细信息，请参阅[在聊天更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[重命名的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)。|
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`可以重写此方法来处理要重命名的Teams团队。 有关详细信息，请参阅[在聊天更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[重命名的团队](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)。|
| MembersAdded | `OnTeamsMembersAddedAsync` | 此方法调用该 `OnMembersAddedAsync` 方法 `ActivityHandler`。 可以重写此方法来处理加入团队的成员。 有关详细信息，请参阅[会话更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)。|
| MembersRemoved | `OnTeamsMembersRemovedAsync` | 此方法调用该 `OnMembersRemovedAsync` 方法 `ActivityHandler`。 可以重写该方法来处理离开团队的成员。 有关详细信息，请参阅[对话更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[删除的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)。|

#### <a name="teams-invoke-activities"></a>Teams调用活动

从`OnInvokeActivityAsync`Teams活动处理程序调用的Teams活动处理程序列表包括：

| 调用类型                    | 处理器                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `OnTeamsCardActionInvokeAsync`       | 从连接器接收卡片操作调用活动时，将调用此方法。 |
| fileConsent/invoke              | `OnTeamsFileConsentAcceptAsync`      | 当用户接受文件同意卡时，将调用此方法。 |
| fileConsent/invoke              | `OnTeamsFileConsentAsync`            | 从连接器接收文件同意卡活动时，将调用此方法。 |
| fileConsent/invoke              | `OnTeamsFileConsentDeclineAsync`     | 当用户拒绝文件同意卡时，将调用此方法。 |
| actionableMessage/executeAction | `OnTeamsO365ConnectorCardActionAsync` | 从连接器接收Office 365连接器卡操作活动时，将调用此方法。 |
| signin/verifyState              | `OnTeamsSigninVerifyStateAsync`      | 当从连接器接收 signIn 验证状态活动时，将调用此方法。 |
| task/fetch                      | `OnTeamsTaskModuleFetchAsync`        | 可在派生类中重写此方法，以便在提取任务模块时提供逻辑。 |
| task/submit                     | `OnTeamsTaskModuleSubmitAsync`       | 可在派生类中重写此方法，以便在提交任务模块时提供逻辑。 |

本部分中列出的调用活动适用于Teams中的聊天机器人。 Bot Framework SDK 还支持调用特定于消息扩展的活动。 有关详细信息，请参阅 [什么是消息扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)。

# <a name="javascript"></a>[JavaScript](#tab/javascript)

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

>[!NOTE]
> 除 **添加** 和 **删除** 成员的活动外，本部分中描述的所有活动处理程序继续与非Teams机器人一样工作。

活动处理程序在团队的上下文中有所不同，其中新成员将添加到团队而不是消息线程。

中 `ActivityHandler` 定义的处理程序列表包括以下内容：

| Event | 处理器 | 说明 |
| :-- | :-- | :-- |
| 收到的任何活动类型 | `onTurn` | 此方法根据收到的活动类型调用其他处理程序之一。 |
| 收到的消息活动 | `onMessage` | 此方法有助于处理 `Message` 活动。 |
| 收到的对话更新活动 | `onConversationUpdate` | 如果机器人以外的成员已加入或离开对话，则此方法在活动上 `ConversationUpdate` 调用处理程序。 |
| 非机器人成员加入了对话 | `onMembersAdded` | 此方法有助于处理加入会话的成员。 |
| 非机器人成员离开对话 | `onMembersRemoved` | 此方法有助于处理离开会话的成员。 |
| 收到的事件活动 | `onEvent` | 此方法对活动调用特定于事件类型的 `Event` 处理程序。 |
| 收到的令牌响应事件活动 | `onTokenResponseEvent` | 此方法有助于处理令牌响应事件。 |
| 收到的其他活动类型 | `onUnrecognizedActivityType` | 此方法有助于处理任何活动类型（否则未处理）。 |

#### <a name="teams-specific-activity-handlers"></a>Teams特定的活动处理程序

扩展 `TeamsActivityHandler` 了核心 Bot Framework 处理程序部分中的处理程序列表，以包括以下内容：

| Event | 处理器 | 说明 |
| :-- | :-- | :-- |
| channelCreated | `OnTeamsChannelCreatedAsync` | 可以重写此方法来处理正在创建的Teams通道。 有关详细信息，请参阅[在对话更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)。 |
| channelDeleted | `OnTeamsChannelDeletedAsync` | 可以重写此方法来处理要删除的Teams通道。 有关详细信息，请参阅[对话更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)。|
| channelRenamed | `OnTeamsChannelRenamedAsync` | 可以重写此方法来处理要重命名的Teams通道。 有关详细信息，请参阅[在聊天更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[重命名的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)。 |
| teamRenamed | `OnTeamsTeamRenamedAsync` | `return Task.CompletedTask;`可以重写此方法来处理要重命名的Teams团队。 有关详细信息，请参阅[在聊天更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[重命名的团队](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)。 |
| MembersAdded | `OnTeamsMembersAddedAsync` | 此方法调用该 `OnMembersAddedAsync` 方法 `ActivityHandler`。 可以重写此方法来处理加入团队的成员。 有关详细信息，请参阅[会话更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)。 |
| MembersRemoved | `OnTeamsMembersRemovedAsync` | 此方法调用该 `OnMembersRemovedAsync` 方法 `ActivityHandler`。 可以重写该方法来处理离开团队的成员。 有关详细信息，请参阅[对话更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[删除的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)。 |

#### <a name="teams-invoke-activities"></a>Teams调用活动

从`onInvokeActivity`Teams活动处理程序调用的Teams活动处理程序列表包括：

| 调用类型                    | 处理器                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `handleTeamsCardActionInvoke`       | 从连接器接收卡片操作调用活动时，将调用此方法。 |
| fileConsent/invoke              | `handleTeamsFileConsentAccept`      | 当用户接受文件同意卡时，将调用此方法。 |
| fileConsent/invoke              | `handleTeamsFileConsent`            | 从连接器接收文件同意卡活动时，将调用此方法。 |
| fileConsent/invoke              | `handleTeamsFileConsentDecline`     | 当用户拒绝文件同意卡时，将调用此方法。 |
| actionableMessage/executeAction | `handleTeamsO365ConnectorCardAction` | 从连接器接收Office 365连接器卡操作活动时，将调用此方法。 |
| signin/verifyState              | `handleTeamsSigninVerifyState`      | 当从连接器接收 signIn 验证状态活动时，将调用此方法。 |
| task/fetch                      | `handleTeamsTaskModuleFetch`        | 可在派生类中重写此方法，以便在提取任务模块时提供逻辑。 |
| task/submit                     | `handleTeamsTaskModuleSubmit`       | 可在派生类中重写此方法，以便在提交任务模块时提供逻辑。 |

本部分中列出的调用活动适用于Teams中的聊天机器人。 Bot Framework SDK 还支持调用特定于消息扩展的活动。 有关详细信息，请参阅 [什么是消息扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)。

# <a name="python"></a>[Python](#tab/python)

#### <a name="core-bot-framework-handlers"></a>核心 Bot Framework 处理程序

>[!NOTE]
> 除 **添加** 和 **删除** 成员的活动外，本部分中描述的所有活动处理程序继续与非Teams机器人一样工作。

活动处理程序在团队的上下文中有所不同，其中新成员将添加到团队而不是消息线程。

中 `ActivityHandler` 定义的处理程序列表包括以下内容：

| Event | 处理器 | 说明 |
| :-- | :-- | :-- |
| 收到的任何活动类型 | `on_turn` | 此方法根据收到的活动类型调用其他处理程序之一。 |
| 收到的消息活动 | `on_message_activity` | 可以重写此方法来处理 `Message` 活动。 |
| 收到的对话更新活动 | `on_conversation_update_activity` | 如果机器人以外的成员加入或退出会话，此方法将调用处理程序。 |
| 非机器人成员加入了对话 | `on_members_added_activity` | 可以重写此方法来处理加入会话的成员。 |
| 非机器人成员离开对话 | `on_members_removed_activity` | 可以重写此方法来处理离开会话的成员。 |
| 收到的事件活动 | `on_event_activity` | 此方法调用特定于事件类型的处理程序。 |
| 收到的令牌响应事件活动 | `on_token_response_event` | 可以重写此方法来处理令牌响应事件。 |
| 收到的非令牌响应事件活动 | `on_event` | 可以重写此方法来处理其他类型的事件。 |
| 收到的其他活动类型 | `on_unrecognized_activity_type` | 可以重写此方法来处理任何未处理的活动类型。 |

#### <a name="teams-specific-activity-handlers"></a>Teams特定的活动处理程序

扩展 `TeamsActivityHandler` 了核心 Bot Framework 处理程序部分中的处理程序列表，以包括以下内容：

| Event | 处理器 | 说明 |
| :-- | :-- | :-- |
| channelCreated | `on_teams_channel_created` | 可以重写此方法来处理正在创建的Teams通道。 有关详细信息，请参阅[在对话更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[创建的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-created)。 |
| channelDeleted | `on_teams_channel_deleted` | 可以重写此方法来处理要删除的Teams通道。 有关详细信息，请参阅[对话更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[删除的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-deleted)。|
| channelRenamed | `on_teams_channel_renamed` | 可以重写此方法来处理要重命名的Teams通道。 有关详细信息，请参阅[在聊天更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[重命名的频道](https://aka.ms/azure-bot-subscribe-to-conversation-events#channel-renamed)。|
| teamRenamed | `on_teams_team_renamed` | `return Task.CompletedTask;`可以重写此方法来处理要重命名的Teams团队。 有关详细信息，请参阅[在聊天更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[重命名的团队](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-renamed)。|
| MembersAdded | `on_teams_members_added` | 此方法调用该 `OnMembersAddedAsync` 方法 `ActivityHandler`。 可以重写此方法来处理加入团队的成员。 有关详细信息，请参阅[会话更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[添加的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-added)。|
| MembersRemoved | `on_teams_members_removed` | 此方法调用该 `OnMembersRemovedAsync` 方法 `ActivityHandler`。 可以重写该方法来处理离开团队的成员。 有关详细信息，请参阅[对话更新事件中](https://aka.ms/azure-bot-subscribe-to-conversation-events)[删除的团队成员](https://aka.ms/azure-bot-subscribe-to-conversation-events#team-members-removed)。|

#### <a name="teams-invoke-activities"></a>Teams调用活动

从`on_invoke_activity`Teams活动处理程序调用的Teams活动处理程序列表包括：

| 调用类型                    | 处理器                              | 说明                                                  |
| :-----------------------------  | :----------------------------------- | :----------------------------------------------------------- |
| CardAction.Invoke               | `on_teams_card_action_invoke`       | 从连接器接收卡片操作调用活动时，将调用此方法。 |
| fileConsent/invoke              | `on_teams_file_consent_accept`      | 当用户接受文件同意卡时，将调用此方法。 |
| fileConsent/invoke              | `on_teams_file_consent`            | 从连接器接收文件同意卡活动时，将调用此方法。 |
| fileConsent/invoke              | `on_teams_file_consent_decline`     | 当用户拒绝文件同意卡时，将调用此方法。 |
| actionableMessage/executeAction | `on_teams_o365_connector_card_action` | 从连接器接收Office 365连接器卡操作活动时，将调用此方法。 |
| signin/verifyState              | `on_teams_signin_verify_state`      | 当从连接器接收 signIn 验证状态活动时，将调用此方法。 |
| task/fetch                      | `on_teams_task_module_fetch`        | 可在派生类中重写此方法，以便在提取任务模块时提供逻辑。 |
| task/submit                     | `on_teams_task_module_submit`       | 可在派生类中重写此方法，以便在提交任务模块时提供逻辑。 |

本部分中列出的调用活动适用于Teams中的聊天机器人。 Bot Framework SDK 还支持调用特定于消息扩展的活动。 有关详细信息，请参阅 [什么是消息扩展](https://aka.ms/azure-bot-what-are-messaging-extensions)。

---

---

现在你已经熟悉了机器人活动处理程序，让我们看看机器人的行为方式如何根据聊天及其接收或发送的消息而有所不同。

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [对话基础知识](~/bots/how-to/conversations/conversation-basics.md)
