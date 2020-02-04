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
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="4b323-103">更新和删除从你的 bot 发送的邮件</span><span class="sxs-lookup"><span data-stu-id="4b323-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a><span data-ttu-id="4b323-104">更新邮件</span><span class="sxs-lookup"><span data-stu-id="4b323-104">Updating messages</span></span>

<span data-ttu-id="4b323-105">你的 bot 可以在发送邮件后动态更新邮件，而不是让你的邮件成为数据的静态快照。</span><span class="sxs-lookup"><span data-stu-id="4b323-105">Rather than have your messages be static snapshots of data, your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="4b323-106">您可以对轮询更新、在按钮按下时修改可用操作或任何其他异步状态更改的方案使用动态邮件更新。</span><span class="sxs-lookup"><span data-stu-id="4b323-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="4b323-107">新邮件需要与类型中的原始邮件不匹配。</span><span class="sxs-lookup"><span data-stu-id="4b323-107">The new message need not match the original in type.</span></span> <span data-ttu-id="4b323-108">例如，如果原始邮件包含附件，则新邮件可以是简单的短信。</span><span class="sxs-lookup"><span data-stu-id="4b323-108">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="4b323-109">C #/.NET</span><span class="sxs-lookup"><span data-stu-id="4b323-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="4b323-110">若要更新现有的邮件，请将`Activity`具有现有活动 ID 的新对象传递`UpdateActivityAsync`给`TurnContext`该类的方法。</span><span class="sxs-lookup"><span data-stu-id="4b323-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="4b323-111">*请参阅* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="4b323-111">*See* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="4b323-112">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="4b323-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="4b323-113">若要更新现有的邮件，请将`Activity`具有现有活动 ID 的新对象传递`updateActivity`给该`TurnContext`对象的方法。</span><span class="sxs-lookup"><span data-stu-id="4b323-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="4b323-114">*请参阅* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span><span class="sxs-lookup"><span data-stu-id="4b323-114">*See* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="pythontabpython"></a>[<span data-ttu-id="4b323-115">Python</span><span class="sxs-lookup"><span data-stu-id="4b323-115">Python</span></span>](#tab/python)

<span data-ttu-id="4b323-116">若要更新现有的邮件，请将`Activity`具有现有活动 ID 的新对象传递`update_activity`给`TurnContext`该类的方法。</span><span class="sxs-lookup"><span data-stu-id="4b323-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="4b323-117">请参阅[TurnContextClass](link to Python API ref docs)。</span><span class="sxs-lookup"><span data-stu-id="4b323-117">See [TurnContextClass](link to Python API ref docs).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

---

## <a name="deleting-messages"></a><span data-ttu-id="4b323-118">删除邮件</span><span class="sxs-lookup"><span data-stu-id="4b323-118">Deleting messages</span></span>

<span data-ttu-id="4b323-119">在 Bot 框架中，每封邮件都有其自己唯一的活动标识符。</span><span class="sxs-lookup"><span data-stu-id="4b323-119">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="4b323-120">可以使用 Bot 框架的`DeleteActivity`方法删除邮件，如下所示。</span><span class="sxs-lookup"><span data-stu-id="4b323-120">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnettabdotnet"></a>[<span data-ttu-id="4b323-121">C #/.NET</span><span class="sxs-lookup"><span data-stu-id="4b323-121">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="4b323-122">若要删除该消息，请将该活动的 ID `DeleteActivityAsync`传递给`TurnContext`该类的方法。</span><span class="sxs-lookup"><span data-stu-id="4b323-122">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="4b323-123">*请参阅* [DeleteActivityAsync 方法 TurnContext](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="4b323-123">*See* [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejstabtypescript"></a>[<span data-ttu-id="4b323-124">TypeScript/node.js</span><span class="sxs-lookup"><span data-stu-id="4b323-124">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="4b323-125">若要删除该邮件，请将该活动的 ID `deleteActivity`传递给该`TurnContext`对象的方法。</span><span class="sxs-lookup"><span data-stu-id="4b323-125">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="4b323-126">*请参阅* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span><span class="sxs-lookup"><span data-stu-id="4b323-126">*See* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="pythontabpython"></a>[<span data-ttu-id="4b323-127">Python</span><span class="sxs-lookup"><span data-stu-id="4b323-127">Python</span></span>](#tab/python)

<span data-ttu-id="4b323-128">若要删除该邮件，请将该活动的 ID `delete_activity`传递给该`TurnContext`对象的方法。</span><span class="sxs-lookup"><span data-stu-id="4b323-128">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="4b323-129">请参阅[delete_activity](link to Python API ref docs)。</span><span class="sxs-lookup"><span data-stu-id="4b323-129">See [delete_activity](link to Python API ref docs).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

---

