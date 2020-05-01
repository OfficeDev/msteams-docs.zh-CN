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
# <a name="update-and-delete-messages-sent-from-your-bot"></a><span data-ttu-id="7181a-103">更新和删除从你的 bot 发送的邮件</span><span class="sxs-lookup"><span data-stu-id="7181a-103">Update and delete messages sent from your bot</span></span>

[!INCLUDE [pre-release-label](~/includes/v4-to-v3-pointer-bots.md)]

## <a name="updating-messages"></a><span data-ttu-id="7181a-104">更新邮件</span><span class="sxs-lookup"><span data-stu-id="7181a-104">Updating messages</span></span>

<span data-ttu-id="7181a-105">你的 bot 可以在发送邮件后动态更新邮件，而不是让你的邮件成为数据的静态快照。</span><span class="sxs-lookup"><span data-stu-id="7181a-105">Rather than have your messages be static snapshots of data, your bot can dynamically update messages after sending them.</span></span> <span data-ttu-id="7181a-106">您可以对轮询更新、在按钮按下时修改可用操作或任何其他异步状态更改的方案使用动态邮件更新。</span><span class="sxs-lookup"><span data-stu-id="7181a-106">You can use dynamic message updates for scenarios such as poll updates, modifying available actions after a button press, or any other asynchronous state change.</span></span>

<span data-ttu-id="7181a-107">新邮件需要与类型中的原始邮件不匹配。</span><span class="sxs-lookup"><span data-stu-id="7181a-107">The new message need not match the original in type.</span></span> <span data-ttu-id="7181a-108">例如，如果原始邮件包含附件，则新邮件可以是简单的短信。</span><span class="sxs-lookup"><span data-stu-id="7181a-108">For instance, if the original message contained an attachment, the new message can be a simple text message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7181a-109">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7181a-109">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="7181a-110">若要更新现有的邮件，请将`Activity`具有现有活动 ID 的新对象传递`UpdateActivityAsync`给`TurnContext`该类的方法。</span><span class="sxs-lookup"><span data-stu-id="7181a-110">To update an existing message, pass a new `Activity` object with the existing activity ID to the `UpdateActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="7181a-111">*请参阅* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="7181a-111">*See* [TurnContextClass](/dotnet/api/microsoft.bot.builder.turncontext?view=botbuilder-dotnet-stable)</span></span>

```csharp
var newActivity = MessageFactory.Text("The new text for the activity");
newActivity.Id = activityId;
await turnContext.UpdateActivityAsync(newActivity, cancellationToken);
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7181a-112">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7181a-112">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="7181a-113">若要更新现有的邮件，请将`Activity`具有现有活动 ID 的新对象传递`updateActivity`给该`TurnContext`对象的方法。</span><span class="sxs-lookup"><span data-stu-id="7181a-113">To update an existing message, pass a new `Activity` object with the existing activity ID to the `updateActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="7181a-114">*请参阅* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span><span class="sxs-lookup"><span data-stu-id="7181a-114">*See* [updateActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#updateactivity-partial-activity--)</span></span>

```typescript
const newActivity = MessageFactory.text('The new text for the activity');
newActivity.id = activityId;
await turnContext.updateActivity(newActivity);
```

# <a name="python"></a>[<span data-ttu-id="7181a-115">Python</span><span class="sxs-lookup"><span data-stu-id="7181a-115">Python</span></span>](#tab/python)

<span data-ttu-id="7181a-116">若要更新现有的邮件，请将`Activity`具有现有活动 ID 的新对象传递`update_activity`给`TurnContext`该类的方法。</span><span class="sxs-lookup"><span data-stu-id="7181a-116">To update an existing message, pass a new `Activity` object with the existing activity ID to the `update_activity` method of the `TurnContext` class.</span></span> <span data-ttu-id="7181a-117">请参阅[TurnContextClass](link to Python API ref docs)。</span><span class="sxs-lookup"><span data-stu-id="7181a-117">See [TurnContextClass](link to Python API ref docs).</span></span>

```python

new_activity = MessageFactory.text("The new text for the activity")
new_activity.id = activity_id
update_result = await context.update_activity(new_activity)

```

# <a name="rest-api"></a>[<span data-ttu-id="7181a-118">REST API</span><span class="sxs-lookup"><span data-stu-id="7181a-118">REST API</span></span>](#tab/rest)

>[!NOTE]
><span data-ttu-id="7181a-119">您可以开发任何 web 编程技术中的团队应用程序，并直接调用[机器人连接器服务 REST api](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0)。</span><span class="sxs-lookup"><span data-stu-id="7181a-119">You can develop Teams apps in any web-programming technology and directly call the [Bot Connector service REST APIs](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0).</span></span> <span data-ttu-id="7181a-120">若要执行此操作，您需要使用 API 请求来实施[身份验证](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0)安全过程。</span><span class="sxs-lookup"><span data-stu-id="7181a-120">To do so, you'll need to implement [Authentication](/azure/bot-service/rest-api/bot-framework-rest-connector-authentication?view=azure-bot-service-4.0) security procedures with your API requests.</span></span>

<span data-ttu-id="7181a-121">若要更新对话中的现有活动，请在`conversationId`请求`activityId`终结点中包含和。</span><span class="sxs-lookup"><span data-stu-id="7181a-121">To update an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span> <span data-ttu-id="7181a-122">若要完成此方案，您应缓存最初的 POST 呼叫返回的活动 ID。</span><span class="sxs-lookup"><span data-stu-id="7181a-122">To complete this scenario, you should cache the activity ID returned by the original POST call.</span></span>

```http
PUT /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="7181a-123">**请求正文**</span><span class="sxs-lookup"><span data-stu-id="7181a-123">**Request body**</span></span> | <span data-ttu-id="7181a-124">[活动](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object)对象</span><span class="sxs-lookup"><span data-stu-id="7181a-124">An [Activity](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#activity-object) object</span></span> |
| <span data-ttu-id="7181a-125">**返回**</span><span class="sxs-lookup"><span data-stu-id="7181a-125">**Returns**</span></span> | <span data-ttu-id="7181a-126">一个[ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object)对象</span><span class="sxs-lookup"><span data-stu-id="7181a-126">A [ResourceResponse](/azure/bot-service/rest-api/bot-framework-rest-connector-api-reference?view=azure-bot-service-4.0#resourceresponse-object) object</span></span> |

---

## <a name="deleting-messages"></a><span data-ttu-id="7181a-127">删除邮件</span><span class="sxs-lookup"><span data-stu-id="7181a-127">Deleting messages</span></span>

<span data-ttu-id="7181a-128">在 Bot 框架中，每封邮件都有其自己唯一的活动标识符。</span><span class="sxs-lookup"><span data-stu-id="7181a-128">In the Bot Framework, every message has its own unique activity identifier.</span></span>
<span data-ttu-id="7181a-129">可以使用 Bot 框架的`DeleteActivity`方法删除邮件，如下所示。</span><span class="sxs-lookup"><span data-stu-id="7181a-129">Messages can be deleted using the Bot Framework's `DeleteActivity` method as shown here.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7181a-130">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7181a-130">C#/.NET</span></span>](#tab/dotnet)

<span data-ttu-id="7181a-131">若要删除该消息，请将该活动的 ID `DeleteActivityAsync`传递给`TurnContext`该类的方法。</span><span class="sxs-lookup"><span data-stu-id="7181a-131">To delete that message, pass that activity's ID to the `DeleteActivityAsync` method of the `TurnContext` class.</span></span> <span data-ttu-id="7181a-132">*请参阅* [DeleteActivityAsync 方法 TurnContext](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span><span class="sxs-lookup"><span data-stu-id="7181a-132">*See* [TurnContext.DeleteActivityAsync Method](/dotnet/api/microsoft.bot.builder.turncontext.deleteactivityasync?view=botbuilder-dotnet-stable)</span></span>

```csharp
foreach (var activityId in _list)
{
    await turnContext.DeleteActivityAsync(activityId, cancellationToken);
}
```

# <a name="typescriptnodejs"></a>[<span data-ttu-id="7181a-133">TypeScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7181a-133">TypeScript/Node.js</span></span>](#tab/typescript)

<span data-ttu-id="7181a-134">若要删除该邮件，请将该活动的 ID `deleteActivity`传递给该`TurnContext`对象的方法。</span><span class="sxs-lookup"><span data-stu-id="7181a-134">To delete that message, pass that activity's ID to the `deleteActivity` method of the `TurnContext` object.</span></span> <span data-ttu-id="7181a-135">*请参阅* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span><span class="sxs-lookup"><span data-stu-id="7181a-135">*See* [deleteActivity](/javascript/api/botbuilder-core/turncontext?view=botbuilder-ts-latest#deleteactivity-string---partial-conversationreference--)</span></span>

```typescript
for (let i = 0; i < activityIds.length; i++) {
    await turnContext.deleteActivity(activityIds[i]);
}
```

# <a name="python"></a>[<span data-ttu-id="7181a-136">Python</span><span class="sxs-lookup"><span data-stu-id="7181a-136">Python</span></span>](#tab/python)

<span data-ttu-id="7181a-137">若要删除该邮件，请将该活动的 ID `delete_activity`传递给该`TurnContext`对象的方法。</span><span class="sxs-lookup"><span data-stu-id="7181a-137">To delete that message, pass that activity's ID to the `delete_activity` method of the `TurnContext` object.</span></span> <span data-ttu-id="7181a-138">请参阅[活动更新-和-删除](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py)。</span><span class="sxs-lookup"><span data-stu-id="7181a-138">See [activity-update-and-delete](https://github.com/microsoft/botbuilder-python/blob/c04ecacb22c1f4b43a671fe2f1e4782218391975/tests/teams/scenarios/activity-update-and-delete/bots/activity_update_and_delete_bot.py).</span></span>

```python
for each activity_id in _list:
    await TurnContext.delete_activity(activity_id)
```

# <a name="rest-api"></a>[<span data-ttu-id="7181a-139">REST API</span><span class="sxs-lookup"><span data-stu-id="7181a-139">REST API</span></span>](#tab/rest)

 <span data-ttu-id="7181a-140">若要删除对话中的现有活动，请在`conversationId`请求`activityId`终结点中包含和。</span><span class="sxs-lookup"><span data-stu-id="7181a-140">To delete an existing activity within a conversation, include the `conversationId` and `activityId` in the request endpoint.</span></span>

```http
DELETE /v3/conversations/{conversationId}/activities/{activityId}
```

| | |
|----|----|
| <span data-ttu-id="7181a-141">**请求正文**</span><span class="sxs-lookup"><span data-stu-id="7181a-141">**Request body**</span></span> | <span data-ttu-id="7181a-142">不适用</span><span class="sxs-lookup"><span data-stu-id="7181a-142">n/a</span></span> |
| <span data-ttu-id="7181a-143">**返回**</span><span class="sxs-lookup"><span data-stu-id="7181a-143">**Returns**</span></span> | <span data-ttu-id="7181a-144">指示操作结果的 HTTP 状态代码。</span><span class="sxs-lookup"><span data-stu-id="7181a-144">An HTTP Status code that indicates the outcome of the operation.</span></span> <span data-ttu-id="7181a-145">响应正文中未指定任何内容。</span><span class="sxs-lookup"><span data-stu-id="7181a-145">Nothing is specified in the body of the response.</span></span> |

---
