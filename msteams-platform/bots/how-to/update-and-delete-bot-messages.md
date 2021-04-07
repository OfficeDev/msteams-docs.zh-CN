---
title: 更新和删除从自动程序发送的消息
author: WashingtonKayaker
description: 如何更新和删除从 Microsoft Teams 自动程序发送的消息
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: 04a17914efd40173d761537773613b93563999aa
ms.sourcegitcommit: f5ee3fa5ef6126d9bf845948d27d9067b3bbb994
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/06/2021
ms.locfileid: "51596201"
---
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="b0fe5-103">更新和删除从自动程序发送的消息</span><span class="sxs-lookup"><span data-stu-id="b0fe5-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="update-messages"></a><span data-ttu-id="b0fe5-104">更新邮件</span><span class="sxs-lookup"><span data-stu-id="b0fe5-104">Update messages</span></span>

<span data-ttu-id="b0fe5-105">机器人可以在发送邮件后动态更新消息。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-105">Your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="b0fe5-106">你可以将动态消息更新用于轮询更新、在按下按钮后修改可用操作，或者任何其他异步状态更改。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="b0fe5-107">新邮件的类型不需要与原始邮件匹配。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-107">The new message need not match the original in type.</span></span> <span data-ttu-id="b0fe5-108">例如，如果原始邮件包含附件，则新邮件可以是简单的短信。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-108">For example, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="c"></a>[<span data-ttu-id="b0fe5-109">C#</span><span class="sxs-lookup"><span data-stu-id="b0fe5-109">C#</span></span>](#tab/dotnet)

<span data-ttu-id="b0fe5-110">若要更新现有消息，请用现有活动 ID 将新对象 `Activity` 传递到 `UpdateActivityAsync` 类的 `TurnContext` 方法。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="b0fe5-111">请参阅 [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-111">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescript"></a>[<span data-ttu-id="b0fe5-112">TypeScript</span><span class="sxs-lookup"><span data-stu-id="b0fe5-112">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="b0fe5-113">若要更新现有邮件，请向 对象的 方法传递具有现有 `Activity` 活动 ID `updateActivity` 的新 `TurnContext` 对象。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="b0fe5-114">请参阅 [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-114">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="b0fe5-115">Python</span><span class="sxs-lookup"><span data-stu-id="b0fe5-115">Python</span></span>](#tab/python)

<span data-ttu-id="b0fe5-116">若要更新现有消息，请用现有活动 ID 将新对象 `Activity` 传递到 `update_activity` 类的 `TurnContext` 方法。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="b0fe5-117">请参阅 [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-117">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[<span data-ttu-id="b0fe5-118">REST API</span><span class="sxs-lookup"><span data-stu-id="b0fe5-118">REST API</span></span>](#tab/rest)

>[!NOTE]
><span data-ttu-id="b0fe5-119">可以使用任何 Web 编程技术开发 Teams 应用，并直接调用[Bot Connector 服务 REST API。](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true)</span><span class="sxs-lookup"><span data-stu-id="b0fe5-119">You can develop Teams apps in any web programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0&preserve-view=true).</span></span> <span data-ttu-id="b0fe5-120">为此，你需要使用 [API](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) 请求实现身份验证安全过程。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-120">To do so, you need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0&preserve-view=true) security procedures with your API requests.</span></span>

<span data-ttu-id="b0fe5-121">若要更新对话中的现有活动，请包含 `conversationId` 请求 `activityId` 终结点中的 和 。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-121">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="b0fe5-122">若要完成此方案，您必须缓存原始 POST 调用返回的活动 ID。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-122">To complete this scenario, you must cache the activity ID returned by the original POST call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|<span data-ttu-id="b0fe5-123">请求</span><span class="sxs-lookup"><span data-stu-id="b0fe5-123">Request</span></span> |<span data-ttu-id="b0fe5-124">响应</span><span class="sxs-lookup"><span data-stu-id="b0fe5-124">Response</span></span> |
|----|----|
|<span data-ttu-id="b0fe5-125">Activity [](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true)对象</span><span class="sxs-lookup"><span data-stu-id="b0fe5-125">An [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object</span></span> |<span data-ttu-id="b0fe5-126">[ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true)对象</span><span class="sxs-lookup"><span data-stu-id="b0fe5-126">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object</span></span>  |

---

## <a name="update-cards"></a><span data-ttu-id="b0fe5-127">更新卡片</span><span class="sxs-lookup"><span data-stu-id="b0fe5-127">Update cards</span></span>

<span data-ttu-id="b0fe5-128">若要更新按钮选择上的现有卡片，可以使用 `ReplyToId` 传入活动。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-128">To update the existing card on button selection, you can use `ReplyToId` of incoming activity.</span></span>

# <a name="c"></a>[<span data-ttu-id="b0fe5-129">C#</span><span class="sxs-lookup"><span data-stu-id="b0fe5-129">C#</span></span>](#tab/dotnet)

<span data-ttu-id="b0fe5-130">若要在按钮单击时更新现有卡片，请用更新的卡片将新对象作为活动 ID 传递给 类 `Activity` `ReplyToId` 的 `UpdateActivityAsync` `TurnContext` 方法。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-130">To update existing card on a button click, pass a new `Activity` object with updated card and `ReplyToId` as activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="b0fe5-131">请参阅 [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-131">See [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>
```csharp
var activity = MessageFactory.Attachment(card.ToAttachment());
activity.Id = turnContext.Activity.ReplyToId;
await turnContext.UpdateActivityAsync(activity, cancellationToken);
```

# <a name="typescript"></a>[<span data-ttu-id="b0fe5-132">TypeScript</span><span class="sxs-lookup"><span data-stu-id="b0fe5-132">TypeScript</span></span>](#tab/typescript)


<span data-ttu-id="b0fe5-133">若要在按钮单击时更新现有卡片，请用更新的卡片将新对象作为活动 ID 传递给 `Activity` `replyToId` 对象的 `updateActivity` `TurnContext` 方法。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-133">To update existing card on a button click, pass a new `Activity` object with updated card and `replyToId` as activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="b0fe5-134">请参阅 [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-134">See [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--&preserve-view=true).</span></span>
```typescript
const message = MessageFactory.attachment(card);
message.id = context.activity.replyToId;
await context.updateActivity(message);
```

# <a name="python"></a>[<span data-ttu-id="b0fe5-135">Python</span><span class="sxs-lookup"><span data-stu-id="b0fe5-135">Python</span></span>](#tab/python)

<span data-ttu-id="b0fe5-136">若要在按钮单击时更新现有卡片，请用更新的卡片将新对象作为活动 ID 传递给 类 `Activity` `reply_to_id` 的 `update_activity` `TurnContext` 方法。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-136">To update existing card on a button click, pass a new `Activity` object with updated card and `reply_to_id` as activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="b0fe5-137">请参阅 [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-137">See [TurnContextClass](/python/api/botbuilder-core/botbuilder.core.turncontext?view=botbuilder-py-latest&preserve-view=true).</span></span>

```python
updated_activity = MessageFactory.attachment(CardFactory.hero_card(card))
updated_activity.id = turn_context.activity.reply_to_id
await turn_context.update_activity(updated_activity)

```

# <a name="rest-api"></a>[<span data-ttu-id="b0fe5-138">REST API</span><span class="sxs-lookup"><span data-stu-id="b0fe5-138">REST API</span></span>](#tab/rest)

<span data-ttu-id="b0fe5-139">若要更新对话中的现有活动，请包含 `conversationId` 请求 `activityId` 终结点中的 和 。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-139">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="b0fe5-140">若要完成此方案，您必须缓存原始 Post 调用返回的活动 ID。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-140">To complete this scenario, you must cache the activity ID returned by the original post call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

|<span data-ttu-id="b0fe5-141">请求</span><span class="sxs-lookup"><span data-stu-id="b0fe5-141">Request</span></span> |<span data-ttu-id="b0fe5-142">响应</span><span class="sxs-lookup"><span data-stu-id="b0fe5-142">Response</span></span> |
|----|----|
| <span data-ttu-id="b0fe5-143">一 [个 Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) 对象。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-143">An [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object&preserve-view=true) object.</span></span> | <span data-ttu-id="b0fe5-144">一 [个 ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) 对象。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-144">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object&preserve-view=true) object.</span></span> |

---

## <a name="delete-messages"></a><span data-ttu-id="b0fe5-145">删除邮件</span><span class="sxs-lookup"><span data-stu-id="b0fe5-145">Delete messages</span></span>

<span data-ttu-id="b0fe5-146">在 Bot Framework 中，每条消息都有其自己的唯一活动标识符。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-146">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="b0fe5-147">可以使用 Bot Framework 的方法删除消息 `DeleteActivity` ，如下所示。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-147">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="c"></a>[<span data-ttu-id="b0fe5-148">C#</span><span class="sxs-lookup"><span data-stu-id="b0fe5-148">C#</span></span>](#tab/dotnet)

<span data-ttu-id="b0fe5-149">若要删除该邮件，请将其活动 ID 传递给 `DeleteActivityAsync` 类 `TurnContext` 的 方法。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-149">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="b0fe5-150">请参阅 [TurnContext.DeleteActivityAsync 方法](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-150">See [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable&preserve-view=true).</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescript"></a>[<span data-ttu-id="b0fe5-151">TypeScript</span><span class="sxs-lookup"><span data-stu-id="b0fe5-151">TypeScript</span></span>](#tab/typescript)

<span data-ttu-id="b0fe5-152">若要删除该邮件，请向 对象的 方法传递该 `deleteActivity` 活动的 `TurnContext` ID。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-152">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="b0fe5-153">请参阅 [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true)。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-153">See [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--&preserve-view=true).</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="b0fe5-154">Python</span><span class="sxs-lookup"><span data-stu-id="b0fe5-154">Python</span></span>](#tab/python)

<span data-ttu-id="b0fe5-155">若要删除该邮件，请向 对象的 方法传递该 `delete_activity` 活动的 `TurnContext` ID。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-155">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="b0fe5-156">请参阅 [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-156">See [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="b0fe5-157">REST API</span><span class="sxs-lookup"><span data-stu-id="b0fe5-157">REST API</span></span>](#tab/rest)

<span data-ttu-id="b0fe5-158">若要删除对话中的现有活动，请包含 `conversationId` 请求 `activityId` 终结点中的 和 。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-158">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

|<span data-ttu-id="b0fe5-159">请求</span><span class="sxs-lookup"><span data-stu-id="b0fe5-159">Request</span></span> |<span data-ttu-id="b0fe5-160">响应</span><span class="sxs-lookup"><span data-stu-id="b0fe5-160">Response</span></span> |
|----|----|
| <span data-ttu-id="b0fe5-161">不适用</span><span class="sxs-lookup"><span data-stu-id="b0fe5-161">N/A</span></span> | <span data-ttu-id="b0fe5-162">指示操作结果的 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-162">An HTTP status code that indicates the outcome of the operation.</span></span> <span data-ttu-id="b0fe5-163">响应正文中未指定任何项。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-163">Nothing is specified in the body of the response.</span></span> |

---

## <a name="code-samples"></a><span data-ttu-id="b0fe5-164">代码示例</span><span class="sxs-lookup"><span data-stu-id="b0fe5-164">Code samples</span></span>

<span data-ttu-id="b0fe5-165">官方对话的基础知识如下所示：</span><span class="sxs-lookup"><span data-stu-id="b0fe5-165">The official conversation basics are as follows:</span></span>

| <span data-ttu-id="b0fe5-166">示例名称</span><span class="sxs-lookup"><span data-stu-id="b0fe5-166">Sample name</span></span>           | <span data-ttu-id="b0fe5-167">Description</span><span class="sxs-lookup"><span data-stu-id="b0fe5-167">Description</span></span>                                                                      | <span data-ttu-id="b0fe5-168">.NET</span><span class="sxs-lookup"><span data-stu-id="b0fe5-168">.NET</span></span>    | <span data-ttu-id="b0fe5-169">Node.js</span><span class="sxs-lookup"><span data-stu-id="b0fe5-169">Node.js</span></span>   | <span data-ttu-id="b0fe5-170">Python</span><span class="sxs-lookup"><span data-stu-id="b0fe5-170">Python</span></span>  |
|:----------------------|:---------------------------------------------------------------------------------|:--------|:-------------|:--------|
|<span data-ttu-id="b0fe5-171">Teams 对话基础知识</span><span class="sxs-lookup"><span data-stu-id="b0fe5-171">Teams Conversation Basics</span></span>  | <span data-ttu-id="b0fe5-172">演示 Teams 中对话的基础知识，包括消息更新和删除。</span><span class="sxs-lookup"><span data-stu-id="b0fe5-172">Demonstrates basics of conversations in Teams, including message update and delete.</span></span>|[<span data-ttu-id="b0fe5-173">View</span><span class="sxs-lookup"><span data-stu-id="b0fe5-173">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/57.teams-conversation-bot)|[<span data-ttu-id="b0fe5-174">View</span><span class="sxs-lookup"><span data-stu-id="b0fe5-174">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/57.teams-conversation-bot) | [<span data-ttu-id="b0fe5-175">View</span><span class="sxs-lookup"><span data-stu-id="b0fe5-175">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/python/57.teams-conversation-bot)|
