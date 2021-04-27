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
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="727c8-103">更新和删除从自动程序发送的消息</span><span class="sxs-lookup"><span data-stu-id="727c8-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

<span data-ttu-id="727c8-104">自动程序可以在发送邮件后动态更新消息，而不是将它们作为数据的静态快照。</span><span class="sxs-lookup"><span data-stu-id="727c8-104">Your bot can dynamically update messages after sending them instead of having them as static snapshots of data.</span></span> <span data-ttu-id="727c8-105">也可使用 Bot Framework 的方法删除 `DeleteActivity` 邮件。</span><span class="sxs-lookup"><span data-stu-id="727c8-105">Messages can also be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

## <a name="update-messages"></a><span data-ttu-id="727c8-106">更新邮件</span><span class="sxs-lookup"><span data-stu-id="727c8-106">Update messages</span></span>

<span data-ttu-id="727c8-107">你可以将动态消息更新用于各种方案，例如轮询更新、在按下按钮后修改可用操作，或者任何其他异步状态更改。</span><span class="sxs-lookup"><span data-stu-id="727c8-107">You can use dynamic message updates for scenarios, such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="727c8-108">新邮件不需要匹配原始类型。</span><span class="sxs-lookup"><span data-stu-id="727c8-108">It is not necessary for the new message to match the original in type.</span></span> <span data-ttu-id="727c8-109">例如，如果原始邮件包含附件，则新邮件可以是简单的短信。</span><span class="sxs-lookup"><span data-stu-id="727c8-109">For example, if the original message contains an attachment, the new message can be a simple text message.</span></span>

# <a name="c"></a>[<span data-ttu-id="727c8-110">C#</span><span class="sxs-lookup"><span data-stu-id="727c8-110">C#</span></span>](#tab/dotnet)

<span data-ttu-id="727c8-111">若要更新现有消息，请用现有活动 ID 将新对象 `Activity` 传递到 `UpdateActivityAsync` 类的 `TurnContext` 方法。</span><span class="sxs-lookup"><span data-stu-id="727c8-111">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="727c8-112">有关详细信息，请参阅 [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="727c8-112">For more information, see [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[<span data-ttu-id="727c8-113">TypeScript</span><span class="sxs-lookup"><span data-stu-id="727c8-113">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="727c8-114">若要更新现有邮件，请向 对象的 方法传递具有现有 `Activity` 活动 ID `updateActivity` 的新 `TurnContext` 对象。</span><span class="sxs-lookup"><span data-stu-id="727c8-114">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="727c8-115">有关详细信息，请参阅 [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="727c8-115">For more information, see [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="727c8-116">Python</span><span class="sxs-lookup"><span data-stu-id="727c8-116">Python</span></span>](#tab/python)

<span data-ttu-id="727c8-117">若要更新现有消息，请用现有活动 ID 将新对象 `Activity` 传递到 `update_activity` 类的 `TurnContext` 方法。</span><span class="sxs-lookup"><span data-stu-id="727c8-117">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="727c8-118">请参阅 [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="727c8-118">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span></span>

```python
new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)
```

# <a name="rest-api"></a>[<span data-ttu-id="727c8-119">REST API</span><span class="sxs-lookup"><span data-stu-id="727c8-119">REST API</span></span>](#tab/rest)

> [!NOTE]

> <span data-ttu-id="727c8-120">可以使用任何 Web 编程技术开发 Teams 应用，并直接调用[Bot Connector 服务 REST API。](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="727c8-120">You can develop Teams apps in any web-programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="727c8-121">为此，你需要使用 [API](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) 请求实现身份验证安全过程。</span><span class="sxs-lookup"><span data-stu-id="727c8-121">To do so, you need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="727c8-122">若要更新对话中的现有活动，请包含 `conversationId` 请求 `activityId` 终结点中的 和 。</span><span class="sxs-lookup"><span data-stu-id="727c8-122">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="727c8-123">若要完成此方案，您必须缓存原始 Post 调用返回的活动 ID。</span><span class="sxs-lookup"><span data-stu-id="727c8-123">To complete this scenario, you must cache the activity ID returned by the original post call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| <span data-ttu-id="727c8-124">**Request 和 Responce**</span><span class="sxs-lookup"><span data-stu-id="727c8-124">**Request and Responce**</span></span> | <span data-ttu-id="727c8-125">**描述**</span><span class="sxs-lookup"><span data-stu-id="727c8-125">**Description**</span></span> |
|----|----|
| <span data-ttu-id="727c8-126">活动[对象](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="727c8-126">An [activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object</span></span> | <span data-ttu-id="727c8-127">[ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)对象</span><span class="sxs-lookup"><span data-stu-id="727c8-127">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object</span></span> |

---
* * *

<span data-ttu-id="727c8-128">现在你已更新邮件，请更新传入活动的按钮选择上的现有卡片。</span><span class="sxs-lookup"><span data-stu-id="727c8-128">Now that you have updated messages, update the existing card on button selection for incoming activities.</span></span>

## <a name="update-cards"></a><span data-ttu-id="727c8-129">更新卡片</span><span class="sxs-lookup"><span data-stu-id="727c8-129">Update cards</span></span>

<span data-ttu-id="727c8-130">若要更新按钮选择上的现有卡片，可以使用 `ReplyToId` 传入活动。</span><span class="sxs-lookup"><span data-stu-id="727c8-130">To update the existing card on button selection, you can use `ReplyToId` of incoming activity.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="727c8-131">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="727c8-131">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="727c8-132">若要更新按钮选择上的现有卡片，请用更新的卡片将新对象作为活动 ID 传递给 类 `Activity` `ReplyToId` 的 `UpdateActivityAsync` `TurnContext` 方法。</span><span class="sxs-lookup"><span data-stu-id="727c8-132">To update existing card on a button selection, pass a new `Activity` object with updated card and `ReplyToId` as activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="727c8-133">请参阅 [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="727c8-133">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[<span data-ttu-id="727c8-134">TypeScript</span><span class="sxs-lookup"><span data-stu-id="727c8-134">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="727c8-135">若要更新按钮选择上的现有卡片，请用更新的卡片将新对象作为活动 ID 传递给 `Activity` `replyToId` 对象的 `updateActivity` `TurnContext` 方法。</span><span class="sxs-lookup"><span data-stu-id="727c8-135">To update existing card on a button selection, pass a new `Activity` object with updated card and `replyToId` as activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="727c8-136">请参阅 [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="727c8-136">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[<span data-ttu-id="727c8-137">Python</span><span class="sxs-lookup"><span data-stu-id="727c8-137">Python</span></span>](#tab/python)

<span data-ttu-id="727c8-138">若要在按钮单击时更新现有卡片，请用更新的卡片将新对象作为活动 ID 传递给 类 `Activity` `reply_to_id` 的 `update_activity` `TurnContext` 方法。</span><span class="sxs-lookup"><span data-stu-id="727c8-138">To update existing card on a button click, pass a new `Activity` object with updated card and `reply_to_id` as activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="727c8-139">请参阅 [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="727c8-139">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span></span>

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)
```

# <a name="rest-api"></a>[<span data-ttu-id="727c8-140">REST API</span><span class="sxs-lookup"><span data-stu-id="727c8-140">REST API</span></span>](#tab/rest)

> [!NOTE]
> <span data-ttu-id="727c8-141">可以使用任何 Web 编程技术开发 Teams 应用，并直接调用[机器人连接器服务 REST API。](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="727c8-141">You can develop Teams apps in any web programming technology and directly call the [bot connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="727c8-142">为此，必须使用 [API](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) 请求实现身份验证安全过程。</span><span class="sxs-lookup"><span data-stu-id="727c8-142">To do this, you must implement [authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="727c8-143">若要更新对话中的现有活动，请包含 `conversationId` 请求 `activityId` 终结点中的 和 。</span><span class="sxs-lookup"><span data-stu-id="727c8-143">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="727c8-144">若要完成此方案，您必须缓存原始 Post 调用返回的活动 ID。</span><span class="sxs-lookup"><span data-stu-id="727c8-144">To complete this scenario, you must cache the activity ID returned by the original post call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|<span data-ttu-id="727c8-145">请求</span><span class="sxs-lookup"><span data-stu-id="727c8-145">Request</span></span> |<span data-ttu-id="727c8-146">响应</span><span class="sxs-lookup"><span data-stu-id="727c8-146">Response</span></span> |
|----|----|
| <span data-ttu-id="727c8-147">活动 [对象](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) 。</span><span class="sxs-lookup"><span data-stu-id="727c8-147">An [activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object.</span></span> | <span data-ttu-id="727c8-148">一 [个 ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) 对象。</span><span class="sxs-lookup"><span data-stu-id="727c8-148">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object.</span></span> |

* * *

<span data-ttu-id="727c8-149">现在，你已更新卡片，可以使用 Bot 框架删除消息。</span><span class="sxs-lookup"><span data-stu-id="727c8-149">Now that you have updated cards, you can delete messages using the Bot Framework.</span></span>

## <a name="delete-messages"></a><span data-ttu-id="727c8-150">删除邮件</span><span class="sxs-lookup"><span data-stu-id="727c8-150">Delete messages</span></span>

<span data-ttu-id="727c8-151">在 Bot Framework 中，每条消息都有其唯一的活动标识符。</span><span class="sxs-lookup"><span data-stu-id="727c8-151">In the Bot Framework, every message has its unique activity identifier.</span></span> <span data-ttu-id="727c8-152">可以使用 Bot Framework 的方法删除 `DeleteActivity` 邮件。</span><span class="sxs-lookup"><span data-stu-id="727c8-152">Messages can be deleted using the Bot Framework's `DeleteActivity` method.</span></span>

# <a name="c"></a>[<span data-ttu-id="727c8-153">C#</span><span class="sxs-lookup"><span data-stu-id="727c8-153">C#</span></span>](#tab/dotnet)

<span data-ttu-id="727c8-154">若要删除邮件，请将其活动 ID 传递给 `DeleteActivityAsync` 类 `TurnContext` 的 方法。</span><span class="sxs-lookup"><span data-stu-id="727c8-154">To delete a message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="727c8-155">有关详细信息，请参阅 [TurnContext.DeleteActivityAsync 方法](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="727c8-155">For more information, see [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="727c8-156">TypeScript</span><span class="sxs-lookup"><span data-stu-id="727c8-156">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="727c8-157">若要删除邮件，请向 对象的 方法传递该 `deleteActivity` 活动的 `TurnContext` ID。</span><span class="sxs-lookup"><span data-stu-id="727c8-157">To delete a message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="727c8-158">有关详细信息，请参阅 [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="727c8-158">For more information, see [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="727c8-159">Python</span><span class="sxs-lookup"><span data-stu-id="727c8-159">Python</span></span>](#tab/python)

<span data-ttu-id="727c8-160">若要删除该邮件，请向 对象的 方法传递该 `delete_activity` 活动的 `TurnContext` ID。</span><span class="sxs-lookup"><span data-stu-id="727c8-160">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="727c8-161">有关详细信息，请参阅 [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)。</span><span class="sxs-lookup"><span data-stu-id="727c8-161">For more information, see [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="727c8-162">REST API</span><span class="sxs-lookup"><span data-stu-id="727c8-162">REST API</span></span>](#tab/rest)

<span data-ttu-id="727c8-163">若要删除对话中的现有活动，请包含 `conversationId` 请求 `activityId` 终结点中的 和 。</span><span class="sxs-lookup"><span data-stu-id="727c8-163">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| <span data-ttu-id="727c8-164">**Request 和 Responce**</span><span class="sxs-lookup"><span data-stu-id="727c8-164">**Request and Responce**</span></span> | <span data-ttu-id="727c8-165">**描述**</span><span class="sxs-lookup"><span data-stu-id="727c8-165">**Description**</span></span> |
|----|----|
| <span data-ttu-id="727c8-166">不适用</span><span class="sxs-lookup"><span data-stu-id="727c8-166">N/A</span></span> | <span data-ttu-id="727c8-167">指示操作结果的 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="727c8-167">An HTTP status code that indicates the outcome of the operation.</span></span> <span data-ttu-id="727c8-168">响应正文中未指定任何项。</span><span class="sxs-lookup"><span data-stu-id="727c8-168">Nothing is specified in the body of the response.</span></span> |

---

## <a name="code-sample"></a><span data-ttu-id="727c8-169">代码示例</span><span class="sxs-lookup"><span data-stu-id="727c8-169">Code sample</span></span>

<span data-ttu-id="727c8-170">以下代码示例演示了对话的基础知识：</span><span class="sxs-lookup"><span data-stu-id="727c8-170">The following code sample demonstrates basics of conversations:</span></span>

| <span data-ttu-id="727c8-171">**示例名称**</span><span class="sxs-lookup"><span data-stu-id="727c8-171">**Sample Name**</span></span> | <span data-ttu-id="727c8-172">**描述**</span><span class="sxs-lookup"><span data-stu-id="727c8-172">**Description**</span></span> | <span data-ttu-id="727c8-173">**.NET**</span><span class="sxs-lookup"><span data-stu-id="727c8-173">**.NET**</span></span> | <span data-ttu-id="727c8-174">**Node.js**</span><span class="sxs-lookup"><span data-stu-id="727c8-174">**Node.js**</span></span> | <span data-ttu-id="727c8-175">**Python**</span><span class="sxs-lookup"><span data-stu-id="727c8-175">**Python**</span></span> |
|----------------------|-----------------|--------|-------------|--------|
| <span data-ttu-id="727c8-176">Teams 对话基础知识</span><span class="sxs-lookup"><span data-stu-id="727c8-176">Teams Conversation Basics</span></span>  | <span data-ttu-id="727c8-177">演示 Teams 中对话的基础知识，包括消息更新和删除。</span><span class="sxs-lookup"><span data-stu-id="727c8-177">Demonstrates basics of conversations in Teams including message update and delete.</span></span> | [<span data-ttu-id="727c8-178">View</span><span class="sxs-lookup"><span data-stu-id="727c8-178">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot) | [<span data-ttu-id="727c8-179">View</span><span class="sxs-lookup"><span data-stu-id="727c8-179">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="727c8-180">View</span><span class="sxs-lookup"><span data-stu-id="727c8-180">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot) |

## <a name="next-step"></a><span data-ttu-id="727c8-181">后续步骤</span><span class="sxs-lookup"><span data-stu-id="727c8-181">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="727c8-182">获取 Teams 上下文</span><span class="sxs-lookup"><span data-stu-id="727c8-182">Get Teams context</span></span>](~/bots/how-to/get-teams-context.md)
