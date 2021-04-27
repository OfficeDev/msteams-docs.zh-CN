---
title: 更新和删除从自动程序发送的消息
author: WashingtonKayaker
description: 如何更新和删除从 Microsoft Teams 自动程序发送的消息
ms.topic: overview
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: f1e9c068f4ce89f0fd3aa4f5a174a3d3c4b67a77
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019984"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a>更新和删除从自动程序发送的消息

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

自动程序可以在发送邮件后动态更新消息，而不是将它们作为数据的静态快照。 也可使用 Bot Framework 的方法删除 `DeleteActivity` 邮件。

## <a name="update-messages"></a>更新邮件

你可以将动态消息更新用于各种方案，例如轮询更新、在按下按钮后修改可用操作，或者任何其他异步状态更改。

新邮件不需要匹配原始类型。 例如，如果原始邮件包含附件，则新邮件可以是简单的短信。

# <a name="c"></a>[C#](#tab/dotnet)

若要更新现有消息，请用现有活动 ID 将新对象 `Activity` 传递到 `UpdateActivityAsync` 类的 `TurnContext` 方法。 有关详细信息，请参阅 [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

若要更新现有邮件，请向 对象的 方法传递具有现有 `Activity` 活动 ID `updateActivity` 的新 `TurnContext` 对象。 有关详细信息，请参阅 [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

若要更新现有消息，请用现有活动 ID 将新对象 `Activity` 传递到 `update_activity` 类的 `TurnContext` 方法。 请参阅 [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true)。

```python
new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

> [!NOTE]

> 可以使用任何 Web 编程技术开发 Teams 应用，并直接调用[Bot Connector 服务 REST API。](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true) 为此，你需要使用 [API](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) 请求实现身份验证安全过程。

若要更新对话中的现有活动，请包含 `conversationId` 请求 `activityId` 终结点中的 和 。 若要完成此方案，您必须缓存原始 Post 调用返回的活动 ID。

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| **Request 和 Responce** | **描述** |
|----|----|
| 活动[对象](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) | [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)对象 |

---
* * *

现在你已更新邮件，请更新传入活动的按钮选择上的现有卡片。

## <a name="update-cards"></a>更新卡片

若要更新按钮选择上的现有卡片，可以使用 `ReplyToId` 传入活动。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

若要更新按钮选择上的现有卡片，请用更新的卡片将新对象作为活动 ID 传递给 类 `Activity` `ReplyToId` 的 `UpdateActivityAsync` `TurnContext` 方法。 请参阅 [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

若要更新按钮选择上的现有卡片，请用更新的卡片将新对象作为活动 ID 传递给 `Activity` `replyToId` 对象的 `updateActivity` `TurnContext` 方法。 请参阅 [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。

```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[Python](#tab/python)

若要在按钮单击时更新现有卡片，请用更新的卡片将新对象作为活动 ID 传递给 类 `Activity` `reply_to_id` 的 `update_activity` `TurnContext` 方法。 请参阅 [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true)。

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

> [!NOTE]
> 可以使用任何 Web 编程技术开发 Teams 应用，并直接调用[机器人连接器服务 REST API。](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true) 为此，必须使用 [API](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) 请求实现身份验证安全过程。

若要更新对话中的现有活动，请包含 `conversationId` 请求 `activityId` 终结点中的 和 。 若要完成此方案，您必须缓存原始 Post 调用返回的活动 ID。

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|请求 |响应 |
|----|----|
| 活动 [对象](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) 。 | 一 [个 ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) 对象。 |

* * *

现在，你已更新卡片，可以使用 Bot 框架删除消息。

## <a name="delete-messages"></a>删除邮件

在 Bot Framework 中，每条消息都有其唯一的活动标识符。 可以使用 Bot Framework 的方法删除 `DeleteActivity` 邮件。

# <a name="c"></a>[C#](#tab/dotnet)

若要删除邮件，请将其活动 ID 传递给 `DeleteActivityAsync` 类 `TurnContext` 的 方法。 有关详细信息，请参阅 [TurnContext.DeleteActivityAsync 方法](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)。

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

若要删除邮件，请向 对象的 方法传递该 `deleteActivity` 活动的 `TurnContext` ID。 有关详细信息，请参阅 [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true)。

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

若要删除该邮件，请向 对象的 方法传递该 `delete_activity` 活动的 `TurnContext` ID。 有关详细信息，请参阅 [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)。

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

若要删除对话中的现有活动，请包含 `conversationId` 请求 `activityId` 终结点中的 和 。

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| **Request 和 Responce** | **描述** |
|----|----|
| 不适用 | 指示操作结果的 HTTP 状态代码。 响应正文中未指定任何项。 |

---

## <a name="code-sample"></a>代码示例

以下代码示例演示了对话的基础知识：

| **示例名称** | **描述** | **.NET** | **Node.js** | **Python** |
|----------------------|-----------------|--------|-------------|--------|
| Teams 对话基础知识  | 演示 Teams 中对话的基础知识，包括消息更新和删除。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [获取 Teams 上下文](~/bots/how-to/get-teams-context.md)
