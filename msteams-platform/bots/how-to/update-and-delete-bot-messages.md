---
title: 更新和删除从你的 bot 发送的邮件
author: WashingtonKayaker
description: 如何更新和删除从你的 Microsoft 团队 bot 发送的邮件
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 012a6edb77f75c43cff01c58fb94e03fd4f61a85
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673380"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a>更新和删除从你的 bot 发送的邮件

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a>更新邮件

你的 bot 可以在发送邮件后动态更新邮件，而不是让你的邮件成为数据的静态快照。 您可以对轮询更新、在按钮按下时修改可用操作或任何其他异步状态更改的方案使用动态邮件更新。

新邮件需要与类型中的原始邮件不匹配。 例如，如果原始邮件包含附件，则新邮件可以是简单的短信。

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

若要更新现有的邮件，请将`Activity`具有现有活动 ID 的新对象传递`UpdateActivityAsync`给`TurnContext`该类的方法。 *请参阅* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

若要更新现有的邮件，请将`Activity`具有现有活动 ID 的新对象传递`updateActivity`给该`TurnContext`对象的方法。 *请参阅* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="pythontabpython"></a>[Python](#tab/python)

若要更新现有的邮件，请将`Activity`具有现有活动 ID 的新对象传递`update_activity`给`TurnContext`该类的方法。 请参阅[TurnContextClass](link to Python API ref docs)。

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

---

## <a name="deleting-messages"></a>删除邮件

在 Bot 框架中，每封邮件都有其自己唯一的活动标识符。
可以使用 Bot 框架的`DeleteActivity`方法删除邮件，如下所示。

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

若要删除该消息，请将该活动的 ID `DeleteActivityAsync`传递给`TurnContext`该类的方法。 *请参阅* [DeleteActivityAsync 方法 TurnContext](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

若要删除该邮件，请将该活动的 ID `deleteActivity`传递给该`TurnContext`对象的方法。 *请参阅* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="pythontabpython"></a>[Python](#tab/python)

若要删除该邮件，请将该活动的 ID `delete_activity`传递给该`TurnContext`对象的方法。 请参阅[delete_activity](link to Python API ref docs)。

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

---

