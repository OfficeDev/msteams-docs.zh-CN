---
title: 更新和删除从机器人发送的消息
author: WashingtonKayaker
description: 了解如何使用代码示例更新和删除从 Microsoft Teams 机器人在不同环境中和借助 REST API 发送的消息。
ms.topic: overview
ms.localizationpriority: high
ms.author: anclear
ms.openlocfilehash: 76befe46bab8d6cc0aa3d5c0c1e2c8c0f15bf579
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111407"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a>更新和删除从机器人发送的消息

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

机器人可以在发送消息后动态更新消息，而不是将其用作数据的静态快照。 也可以使用 Bot Framework 的 `DeleteActivity` 方法删除消息。

## <a name="update-messages"></a>更新邮件

可以针对轮询更新、按下按钮后修改可用操作或任何其他异步状态更改等方案使用动态消息更新。

新消息不需要匹配类型中的原始消息。 例如，如果原始消息包含附件，则新消息可以是简单的文本消息。

# <a name="c"></a>[C#](#tab/dotnet)

若要更新现有消息，请将具有现有活动 ID 的新 `Activity` 对象传递给 `TurnContext` 类的方法 `UpdateActivityAsync`。 有关详细信息，请参阅 [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

若要更新现有消息，请将具有现有活动 ID 的新 `Activity` 对象传递给 `TurnContext` 对象的方法 `updateActivity`。 有关详细信息，请参阅 [updataActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

若要更新现有消息，请将具有现有活动 ID 的新 `Activity` 对象传递给 `TurnContext` 类的方法 `update_activity`。 请参阅 [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true)。

```python
new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

> [!NOTE]
> 可以在任何 Web 编程技术中开发 Teams 应用，并直接调用[机器人连接器服务 REST API](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)。 为此，需要使用 API 请求实施[身份验证](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true)安全过程。

若要更新对话中的现有活动，请在请求端点中包含 `conversationId` 和 `activityId`。 若要完成此方案，必须缓存原始 post 调用返回的活动 ID。

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|请求 |响应 |
|----|----|
| [活动](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)对象。 | [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) 对象。 |

---
---

现在，你已更新消息，请为传入活动更新按钮选择的现有卡片。

## <a name="update-cards"></a>更新卡片

若要更新按钮选择的现有卡片，可以使用传入活动的 `ReplyToId`。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

若要更新按钮选择的现有卡片，请将具有更新卡片和 `ReplyToId` 活动 ID 的新 `Activity` 对象传递给 `TurnContext` 类的方法 `UpdateActivityAsync`。 请参阅 [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

若要更新的按钮选择的现有卡片，请将具有更新卡片和 `replyToId` 活动 ID 的新 `Activity` 对象传递给 `TurnContext` 对象的方法 `updateActivity`。 请参阅 [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。

```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[Python](#tab/python)

若要更新按钮点击的现有卡片，请将具有更新卡片和 `reply_to_id` 活动 ID 的新 `Activity` 对象传递给 `TurnContext` 类的方法 `update_activity`。 请参阅 [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true)。

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

> [!NOTE]
> 可以在任何 Web 编程技术中开发 Teams 应用，并直接调用[机器人连接器服务 REST API](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)。 为此，必须使用 API 请求实施[身份验证](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true)安全过程。

若要更新对话中的现有活动，请在请求端点中包含 `conversationId` 和 `activityId`。 若要完成此方案，必须缓存原始 post 调用返回的活动 ID。

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|请求 |响应 |
|----|----|
| [活动](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)对象。 | [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) 对象。 |

---

现在，你已更新卡片，可以使用 Bot Framework 删除消息。

## <a name="delete-messages"></a>删除邮件

在 Bot Framework 中，每个消息都有其唯一的活动标识符。 可以使用 Bot Framework 的 `DeleteActivity` 方法删除消息。

# <a name="c"></a>[C#](#tab/dotnet)

若要删除消息，请将该活动的 ID 传递给 `TurnContext` 类的方法 `DeleteActivityAsync`。 有关详细信息，请参阅 [TurnContext.DeleteActivityAsync 方法](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)。

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[TypeScript](#tab/typescript)

若要删除消息，请将该活动的 ID 传递给 `TurnContext` 对象的方法 `deleteActivity`。 有关详细信息，请参阅 [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true)。

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

若要删除该消息，请将该活动的 ID 传递给 `TurnContext` 对象的方法 `delete_activity`。 有关详细信息，请参阅 [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)。

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

若要删除对话中的现有活动，请在请求端点中包含 `conversationId` 和 `activityId`。

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| **请求和响应** | **说明** |
|----|----|
| 不适用 | 指示操作结果的 HTTP 状态代码。 响应正文中未指定任何内容。 |

---

## <a name="code-sample"></a>代码示例

以下代码示例演示了对话的基础知识：

| **示例名称** | **说明** | **.NET** | **Node.js** | **Python** |
|----------------------|-----------------|--------|-------------|--------|
| Teams 对话基础知识  | 演示 Teams 中对话的基础知识，包括消息更新和删除。 | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [获取 Teams 上下文](~/bots/how-to/get-teams-context.md)
