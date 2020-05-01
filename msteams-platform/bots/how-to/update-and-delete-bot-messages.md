---
title: 更新和删除从你的 bot 发送的邮件
author: WashingtonKayaker
description: 如何更新和删除从你的 Microsoft 团队 bot 发送的邮件
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 46994c6810197002ef1c108af4f725426395b37f
ms.sourcegitcommit: 2b1fd50466d807869fd173371ba7dfd82a0064ac
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2020
ms.locfileid: "43957185"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a>更新和删除从你的 bot 发送的邮件

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a>更新邮件

你的 bot 可以在发送邮件后动态更新邮件，而不是让你的邮件成为数据的静态快照。 您可以对轮询更新、在按钮按下时修改可用操作或任何其他异步状态更改的方案使用动态邮件更新。

新邮件需要与类型中的原始邮件不匹配。 例如，如果原始邮件包含附件，则新邮件可以是简单的短信。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

若要更新现有的邮件，请将`Activity`具有现有活动 ID 的新对象传递`UpdateActivityAsync`给`TurnContext`该类的方法。 *请参阅* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

若要更新现有的邮件，请将`Activity`具有现有活动 ID 的新对象传递`updateActivity`给该`TurnContext`对象的方法。 *请参阅* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[Python](#tab/python)

若要更新现有的邮件，请将`Activity`具有现有活动 ID 的新对象传递`update_activity`给`TurnContext`该类的方法。 请参阅[TurnContextClass](link to Python API ref docs)。

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[REST API](#tab/rest)

>[!NOTE]
>您可以开发任何 web 编程技术中的团队应用程序，并直接调用[机器人连接器服务 REST api](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0)。 若要执行此操作，您需要使用 API 请求来实施[身份验证](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0)安全过程。

若要更新对话中的现有活动，请在`conversationId`请求`activityId`终结点中包含和。 若要完成此方案，您应缓存最初的 POST 呼叫返回的活动 ID。

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| **请求正文** | [活动](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object)对象 |
| **返回** | 一个[ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object)对象 |

---

## <a name="deleting-messages"></a>删除邮件

在 Bot 框架中，每封邮件都有其自己唯一的活动标识符。
可以使用 Bot 框架的`DeleteActivity`方法删除邮件，如下所示。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

若要删除该消息，请将该活动的 ID `DeleteActivityAsync`传递给`TurnContext`该类的方法。 *请参阅* [DeleteActivityAsync 方法 TurnContext](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

若要删除该邮件，请将该活动的 ID `deleteActivity`传递给该`TurnContext`对象的方法。 *请参阅* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[Python](#tab/python)

若要删除该邮件，请将该活动的 ID `delete_activity`传递给该`TurnContext`对象的方法。 请参阅[活动更新-和-删除](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)。

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[REST API](#tab/rest)

 若要删除对话中的现有活动，请在`conversationId`请求`activityId`终结点中包含和。

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| **请求正文** | 不适用 |
| **返回** | 指示操作结果的 HTTP 状态代码。 响应正文中未指定任何内容。 |

---
