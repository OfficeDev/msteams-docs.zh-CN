---
title: 在自动程序中添加卡片操作
description: 描述自动Microsoft Teams中的卡片操作以及如何在机器人中使用它们
localization_priority: Normal
ms.topic: conceptual
keywords: teams 机器人卡片操作
ms.openlocfilehash: 1b20ca8003ab74c5dd2860e754024ae64ff94527
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140087"
---
# <a name="card-actions"></a><span data-ttu-id="1900b-104">卡片操作</span><span class="sxs-lookup"><span data-stu-id="1900b-104">Card actions</span></span>

<span data-ttu-id="1900b-105">聊天机器人和邮件扩展中使用的Teams支持以下活动 [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) 类型：</span><span class="sxs-lookup"><span data-stu-id="1900b-105">Cards used by bots and messaging extensions in Teams support the following activity [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) types:</span></span>

> [!NOTE]
> <span data-ttu-id="1900b-106">操作 `CardAction` 不同于从 `potentialActions` 连接器Office 365连接器卡的操作。</span><span class="sxs-lookup"><span data-stu-id="1900b-106">The `CardAction` actions differ from `potentialActions` for Office 365 Connector cards when used from connectors.</span></span>

| <span data-ttu-id="1900b-107">类型</span><span class="sxs-lookup"><span data-stu-id="1900b-107">Type</span></span> | <span data-ttu-id="1900b-108">操作</span><span class="sxs-lookup"><span data-stu-id="1900b-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="1900b-109">在默认浏览器中打开 URL。</span><span class="sxs-lookup"><span data-stu-id="1900b-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="1900b-110">从选择按钮或点击卡片的用户向机器人发送消息和有效负载。</span><span class="sxs-lookup"><span data-stu-id="1900b-110">Sends a message and payload to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="1900b-111">向聊天流发送单独的消息。</span><span class="sxs-lookup"><span data-stu-id="1900b-111">Sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="1900b-112">从选择按钮或点击该卡的用户向机器人发送消息。</span><span class="sxs-lookup"><span data-stu-id="1900b-112">Sends a message to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="1900b-113">所有对话参与者都可以看到从用户到机器人的消息。</span><span class="sxs-lookup"><span data-stu-id="1900b-113">This message from user to bot is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="1900b-114">从选择按钮或点击卡片的用户向机器人发送消息和有效负载。</span><span class="sxs-lookup"><span data-stu-id="1900b-114">Sends a message and payload to the bot from the user who selected the button or tapped the card.</span></span> <span data-ttu-id="1900b-115">此消息不可见。</span><span class="sxs-lookup"><span data-stu-id="1900b-115">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="1900b-116">启动 OAuth 流，允许机器人与安全服务连接。</span><span class="sxs-lookup"><span data-stu-id="1900b-116">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="1900b-117">Teams不支持 `CardAction` 上表中未列出的类型。</span><span class="sxs-lookup"><span data-stu-id="1900b-117">Teams does not support `CardAction` types not listed in the previous table.</span></span>
>* <span data-ttu-id="1900b-118">Teams不支持 `potentialActions` 属性。</span><span class="sxs-lookup"><span data-stu-id="1900b-118">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="1900b-119">卡片操作不同于 Bot [](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) Framework 或 Azure Bot 服务中的建议操作。</span><span class="sxs-lookup"><span data-stu-id="1900b-119">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework or Azure Bot Service.</span></span> <span data-ttu-id="1900b-120">建议的操作在活动Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="1900b-120">Suggested actions are not supported in Microsoft Teams.</span></span> <span data-ttu-id="1900b-121">如果希望按钮显示在自动程序Teams，请使用卡片。</span><span class="sxs-lookup"><span data-stu-id="1900b-121">If you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="1900b-122">如果使用卡片操作作为邮件扩展的一部分，则这些操作在将卡片提交到频道之前不起作用。</span><span class="sxs-lookup"><span data-stu-id="1900b-122">If you are using a card action as part of a messaging extension, the actions do not work until the card is submitted to the channel.</span></span> <span data-ttu-id="1900b-123">当卡片位于撰写消息框中时，操作不起作用。</span><span class="sxs-lookup"><span data-stu-id="1900b-123">The actions do not work while the card is in the compose message box.</span></span>

## <a name="action-type-openurl"></a><span data-ttu-id="1900b-124">操作类型 openUrl</span><span class="sxs-lookup"><span data-stu-id="1900b-124">Action type openUrl</span></span>

<span data-ttu-id="1900b-125">`openUrl` action 类型指定在默认浏览器中启动的 URL。</span><span class="sxs-lookup"><span data-stu-id="1900b-125">`openUrl` action type specifies a URL to launch in the default browser.</span></span>

> [!NOTE]
> <span data-ttu-id="1900b-126">自动程序不会收到有关已选择哪个按钮的任何通知。</span><span class="sxs-lookup"><span data-stu-id="1900b-126">Your bot does not receive any notice on which button was selected.</span></span>

<span data-ttu-id="1900b-127">使用 `openUrl` ，可以创建具有以下属性的操作：</span><span class="sxs-lookup"><span data-stu-id="1900b-127">With `openUrl`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="1900b-128">属性</span><span class="sxs-lookup"><span data-stu-id="1900b-128">Property</span></span> | <span data-ttu-id="1900b-129">说明</span><span class="sxs-lookup"><span data-stu-id="1900b-129">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="1900b-130">显示为按钮标签。</span><span class="sxs-lookup"><span data-stu-id="1900b-130">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="1900b-131">此字段必须包含格式正确的完整 URL。</span><span class="sxs-lookup"><span data-stu-id="1900b-131">This field must contain a full and properly formed URL.</span></span> |

# <a name="json"></a>[<span data-ttu-id="1900b-132">JSON</span><span class="sxs-lookup"><span data-stu-id="1900b-132">JSON</span></span>](#tab/json)

<span data-ttu-id="1900b-133">以下代码显示了 `openUrl` JSON 中的操作类型示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-133">The following code shows an example of `openUrl` action type in JSON:</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

# <a name="c"></a>[<span data-ttu-id="1900b-134">C#</span><span class="sxs-lookup"><span data-stu-id="1900b-134">C#</span></span>](#tab/csharp)

<span data-ttu-id="1900b-135">以下代码显示了一个操作 `openUrl` 类型示例C#：</span><span class="sxs-lookup"><span data-stu-id="1900b-135">The following code shows an example of `openUrl` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.OpenUrl,
    Title = "Tabs in Teams",
    Value = "https://docs.microsoft.com/en-us/microsoftteams/platform/"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="1900b-136">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="1900b-136">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="1900b-137">以下代码显示了 `openUrl` JavaScript 中的操作类型示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-137">The following code shows an example of `openUrl` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: 'openUrl',
    title: 'Tabs in Teams',
    value: 'https://docs.microsoft.com/en-us/microsoftteams/platform/'
}])
```

---

## <a name="action-type-messageback"></a><span data-ttu-id="1900b-138">操作类型 messageBack</span><span class="sxs-lookup"><span data-stu-id="1900b-138">Action type messageBack</span></span>

<span data-ttu-id="1900b-139">使用 `messageBack` ，可以创建具有以下属性的完全自定义操作：</span><span class="sxs-lookup"><span data-stu-id="1900b-139">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="1900b-140">属性</span><span class="sxs-lookup"><span data-stu-id="1900b-140">Property</span></span> | <span data-ttu-id="1900b-141">说明</span><span class="sxs-lookup"><span data-stu-id="1900b-141">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="1900b-142">显示为按钮标签。</span><span class="sxs-lookup"><span data-stu-id="1900b-142">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="1900b-143">可选。</span><span class="sxs-lookup"><span data-stu-id="1900b-143">Optional.</span></span> <span data-ttu-id="1900b-144">操作执行时由聊天流中的用户使用。</span><span class="sxs-lookup"><span data-stu-id="1900b-144">Used by the user in the chat stream when the action is performed.</span></span> <span data-ttu-id="1900b-145">此文本不会发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="1900b-145">This text is not sent to your bot.</span></span> |
| `value` | <span data-ttu-id="1900b-146">操作执行时发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="1900b-146">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="1900b-147">你可以为操作（如唯一标识符或 JSON 对象）对上下文进行编码。</span><span class="sxs-lookup"><span data-stu-id="1900b-147">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="1900b-148">操作执行时发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="1900b-148">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="1900b-149">使用此属性可简化机器人开发。</span><span class="sxs-lookup"><span data-stu-id="1900b-149">Use this property to simplify bot development.</span></span> <span data-ttu-id="1900b-150">代码可以检查单个顶级属性以调度自动程序逻辑。</span><span class="sxs-lookup"><span data-stu-id="1900b-150">Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="1900b-151">灵活性意味着代码无法直接使用 在历史记录中留下可见的 `messageBack` 用户消息 `displayText` 。</span><span class="sxs-lookup"><span data-stu-id="1900b-151">The flexibility of `messageBack` means that your code cannot leave a visible user message in the history simply by not using `displayText`.</span></span>

# <a name="json"></a>[<span data-ttu-id="1900b-152">JSON</span><span class="sxs-lookup"><span data-stu-id="1900b-152">JSON</span></span>](#tab/json)

<span data-ttu-id="1900b-153">以下代码显示了 `messageBack` JSON 中的操作类型示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-153">The following code shows an example of `messageBack` action type in JSON:</span></span>

```json
{
  "buttons": [
    {
    "type": "messageBack",
    "title": "My MessageBack button",
    "displayText": "I clicked this button",
    "text": "User just clicked the MessageBack button",
    "value": "{\"property\": \"propertyValue\" }"
    }
  ]
}
```

<span data-ttu-id="1900b-154">该属性 `value` 可以是序列化的 JSON 字符串或 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="1900b-154">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

# <a name="c"></a>[<span data-ttu-id="1900b-155">C#</span><span class="sxs-lookup"><span data-stu-id="1900b-155">C#</span></span>](#tab/csharp)

<span data-ttu-id="1900b-156">以下代码显示了一个操作 `messageBack` 类型示例C#：</span><span class="sxs-lookup"><span data-stu-id="1900b-156">The following code shows an example of `messageBack` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.MessageBack,
    Title = "My MessageBack button",
    DisplayText = "I clicked this button",
    Text = "User just clicked the MessageBack button",
    Value = "{\"property\": \"propertyValue\" }"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="1900b-157">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="1900b-157">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="1900b-158">以下代码显示了 `messageBack` JavaScript 中的操作类型示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-158">The following code shows an example of `messageBack` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: 'messageBack',
    title: "My MessageBack button",
    displayText: "I clicked this button",
    text: "User just clicked the MessageBack button",
    value: {property: "propertyValue" }
}])
```

---

### <a name="inbound-message-example"></a><span data-ttu-id="1900b-159">入站邮件示例</span><span class="sxs-lookup"><span data-stu-id="1900b-159">Inbound message example</span></span>

<span data-ttu-id="1900b-160">`replyToId` 包含卡片操作所来自的邮件的 ID。</span><span class="sxs-lookup"><span data-stu-id="1900b-160">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="1900b-161">如果要更新邮件，请使用它。</span><span class="sxs-lookup"><span data-stu-id="1900b-161">Use it if you want to update the message.</span></span>

<span data-ttu-id="1900b-162">以下代码显示了入站邮件的示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-162">The following code shows an example of inbound message:</span></span>

```json
{
   "text":"User just clicked the MessageBack button",
   "value":{
      "property":"propertyValue"
   },
   "type":"message",
   "timestamp":"2017-06-22T22:38:47.407Z",
   "id":"f:5261769396935243054",
   "channelId":"msteams",
   "serviceUrl":"https://smba.trafficmanager.net/amer-client-ss.msg/",
   "from":{
      "id":"29:102jd210jd010icsoaeclaejcoa9ue09u",
      "name":"John Smith"
   },
   "conversation":{
      "id":"19:malejcou081i20ojmlcau0@thread.skype;messageid=1498171086622"
   },
   "recipient":{
      "id":"28:76096e45-119f-4736-859c-6dfff54395f7",
      "name":"MyBot"
   },
   "entities":[
      {
        "locale": "en-US",
        "country": "US",
        "platform": "Windows",
        "timezone": "America/Los_Angeles",
        "type": "clientInfo" 
      }
   ],
   "channelData":{
      "channel":{
         "id":"19:malejcou081i20ojmlcau0@thread.skype"
      },
      "team":{
         "id":"19:12d021jdoijsaeoaue0u@thread.skype"
      },
      "tenant":{
         "id":"bec8e231-67ad-484e-87f4-3e5438390a77"
      }
   },
        "replyToId": "1575667808184",
}
```

## <a name="action-type-imback"></a><span data-ttu-id="1900b-163">操作类型 imBack</span><span class="sxs-lookup"><span data-stu-id="1900b-163">Action type imBack</span></span>

<span data-ttu-id="1900b-164">该操作会触发向自动程序发送的返回消息，就像用户在普通聊天消息中 `imBack` 键入一样。</span><span class="sxs-lookup"><span data-stu-id="1900b-164">The `imBack` action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="1900b-165">你的用户和频道中的所有其他用户可以看到按钮响应。</span><span class="sxs-lookup"><span data-stu-id="1900b-165">Your user and all other users in a channel can see the button response.</span></span>

<span data-ttu-id="1900b-166">使用 `imBack` ，可以创建具有以下属性的操作：</span><span class="sxs-lookup"><span data-stu-id="1900b-166">With `imBack`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="1900b-167">属性</span><span class="sxs-lookup"><span data-stu-id="1900b-167">Property</span></span> | <span data-ttu-id="1900b-168">说明</span><span class="sxs-lookup"><span data-stu-id="1900b-168">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="1900b-169">显示为按钮标签。</span><span class="sxs-lookup"><span data-stu-id="1900b-169">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="1900b-170">此字段必须包含聊天中使用的文本字符串，因此发送回聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="1900b-170">This field must contain the text string used in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="1900b-171">这是在自动程序中执行所需逻辑时处理的消息文本。</span><span class="sxs-lookup"><span data-stu-id="1900b-171">This is the message text you process in your bot to perform the desired logic.</span></span> |

> [!NOTE]
> <span data-ttu-id="1900b-172">字段 `value` 是一个简单字符串。</span><span class="sxs-lookup"><span data-stu-id="1900b-172">The `value` field is a simple string.</span></span> <span data-ttu-id="1900b-173">不支持设置格式或隐藏字符。</span><span class="sxs-lookup"><span data-stu-id="1900b-173">There is no support for formatting or hidden characters.</span></span>

# <a name="json"></a>[<span data-ttu-id="1900b-174">JSON</span><span class="sxs-lookup"><span data-stu-id="1900b-174">JSON</span></span>](#tab/json)

<span data-ttu-id="1900b-175">以下代码显示了 `imBack` JSON 中的操作类型示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-175">The following code shows an example of `imBack` action type in JSON:</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

# <a name="c"></a>[<span data-ttu-id="1900b-176">C#</span><span class="sxs-lookup"><span data-stu-id="1900b-176">C#</span></span>](#tab/csharp)

<span data-ttu-id="1900b-177">以下代码显示了一个操作 `imBack` 类型示例C#：</span><span class="sxs-lookup"><span data-stu-id="1900b-177">The following code shows an example of `imBack` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.ImBack,
    Title = "More",
    Value = "Show me more"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="1900b-178">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="1900b-178">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="1900b-179">以下代码显示了 `imBack` JavaScript 中的操作类型示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-179">The following code shows an example of `imBack` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: "imBack",
    title: "More",
    value: "Show me more"
}])
```

---

## <a name="action-type-invoke"></a><span data-ttu-id="1900b-180">操作类型调用</span><span class="sxs-lookup"><span data-stu-id="1900b-180">Action type invoke</span></span>

<span data-ttu-id="1900b-181">`invoke`操作用于调用任务[模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="1900b-181">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="1900b-182">操作 `invoke` 包含三个属性： `type` 、 `title` 和 `value` 。</span><span class="sxs-lookup"><span data-stu-id="1900b-182">The `invoke` action contains three properties, `type`, `title`, and `value`.</span></span>

<span data-ttu-id="1900b-183">使用 `invoke` ，可以创建具有以下属性的操作：</span><span class="sxs-lookup"><span data-stu-id="1900b-183">With `invoke`, you can create an action with the following properties:</span></span>

| <span data-ttu-id="1900b-184">属性</span><span class="sxs-lookup"><span data-stu-id="1900b-184">Property</span></span> | <span data-ttu-id="1900b-185">说明</span><span class="sxs-lookup"><span data-stu-id="1900b-185">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="1900b-186">显示为按钮标签。</span><span class="sxs-lookup"><span data-stu-id="1900b-186">Appears as the button label.</span></span> |
| `value` | <span data-ttu-id="1900b-187">此属性可以包含字符串、字符串化 JSON 对象或 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="1900b-187">This property can contain a string, a stringified JSON object, or a JSON object.</span></span> |

# <a name="json"></a>[<span data-ttu-id="1900b-188">JSON</span><span class="sxs-lookup"><span data-stu-id="1900b-188">JSON</span></span>](#tab/json)

<span data-ttu-id="1900b-189">以下代码显示了 `invoke` JSON 中的操作类型示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-189">The following code shows an example of `invoke` action type in JSON:</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="1900b-190">当用户选择该按钮时，机器人会收到 `value` 包含其他一些信息的对象。</span><span class="sxs-lookup"><span data-stu-id="1900b-190">When a user selects the button, your bot receives the `value` object with some additional information.</span></span>

> [!NOTE]
> <span data-ttu-id="1900b-191">活动类型不是 。 `invoke` `message` `activity.Type == "invoke"`</span><span class="sxs-lookup"><span data-stu-id="1900b-191">The activity type is `invoke` instead of `message` that is `activity.Type == "invoke"`.</span></span>

# <a name="c"></a>[<span data-ttu-id="1900b-192">C#</span><span class="sxs-lookup"><span data-stu-id="1900b-192">C#</span></span>](#tab/csharp)

<span data-ttu-id="1900b-193">以下代码显示了一个操作 `invoke` 类型示例C#：</span><span class="sxs-lookup"><span data-stu-id="1900b-193">The following code shows an example of `invoke` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="1900b-194">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="1900b-194">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="1900b-195">以下代码显示了一个 `invoke` 操作类型示例Node.js：</span><span class="sxs-lookup"><span data-stu-id="1900b-195">The following code shows an example of `invoke` action type in Node.js:</span></span>

```javascript
CardFactory.actions([
{
    type: "invoke",
    title: "Option 1",
    value: {
        option: "opt1"
    }
}])
```

---

### <a name="example-of-incoming-invoke-message"></a><span data-ttu-id="1900b-196">传入调用消息的示例</span><span class="sxs-lookup"><span data-stu-id="1900b-196">Example of incoming invoke message</span></span>

<span data-ttu-id="1900b-197">顶级属性包含卡片 `replyToId` 操作所来自的邮件的 ID。</span><span class="sxs-lookup"><span data-stu-id="1900b-197">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="1900b-198">如果要更新邮件，请使用它。</span><span class="sxs-lookup"><span data-stu-id="1900b-198">Use it if you want to update the message.</span></span>

<span data-ttu-id="1900b-199">以下代码显示了传入调用消息的示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-199">The following code shows an example of incoming invoke message:</span></span>

```json
{
    "type": "invoke",
    "value": {
        "option": "opt1"
    },
    "timestamp": "2017-02-10T04:11:19.614Z",
    "localTimestamp": "2017-02-09T21:11:19.614-07:00",
    "id": "f:6894910862892785420",
    "channelId": "msteams",
    "serviceUrl": "https://smba.trafficmanager.net/amer-client-ss.msg/",
    "from": {
        "id": "29:1Eniglq0-uVL83xNB9GU6w_G5a4SZF0gcJLprZzhtEbel21G_5h-
    NgoprRw45mP0AXUIZVeqrsIHSYV4ntgfVJQ",
        "name": "John Doe"
    },
    "conversation": {
        "id": "19:97b1ec61-45bf-453c-9059-6e8984e0cef4_8d88f59b-ae61-4300-bec0-caace7d28446@unq.gbl.spaces"
    },
    "recipient": {
        "id": "28:8d88f59b-ae61-4300-bec0-caace7d28446",
        "name": "MyBot"
    },
    "entities": [
        {
            "locale": "en-US",
            "country": "US",
            "platform": "Web",
            "type": "clientInfo"
        }
    ],
    "channelData": {
        "channel": {
            "id": "19:dc5ba12695be4eb7bf457cad6b4709eb@thread.skype"
        },
        "team": {
            "id": "19:712c61d0ef384e5fa681ba90ca943398@thread.skype"
        },
        "tenant": {
            "id": "72f988bf-86f1-41af-91ab-2d7cd011db47"
        }
    },
    "replyToId": "1575667808184"
}
```

## <a name="action-type-signin"></a><span data-ttu-id="1900b-200">操作类型登录</span><span class="sxs-lookup"><span data-stu-id="1900b-200">Action type signin</span></span>

<span data-ttu-id="1900b-201">`signin` 操作类型启动 OAuth 流，该流允许机器人与安全服务连接。</span><span class="sxs-lookup"><span data-stu-id="1900b-201">`signin` action type initiates an OAuth flow that permits bots to connect with secure services.</span></span> <span data-ttu-id="1900b-202">有关详细信息，请参阅自动 [程序中的身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="1900b-202">For more information, see [authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

<span data-ttu-id="1900b-203">Teams还支持[仅](#adaptive-cards-actions)由自适应卡片使用的自适应卡片操作。</span><span class="sxs-lookup"><span data-stu-id="1900b-203">Teams also supports [Adaptive Cards actions](#adaptive-cards-actions) that are only used by Adaptive Cards.</span></span>

# <a name="json"></a>[<span data-ttu-id="1900b-204">JSON</span><span class="sxs-lookup"><span data-stu-id="1900b-204">JSON</span></span>](#tab/json)

<span data-ttu-id="1900b-205">以下代码显示了 `signin` JSON 中的操作类型示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-205">The following code shows an example of `signin` action type in JSON:</span></span>

```json
{
"type": "signin",
"title": "Click me for signin",
"value": "https://signin.com"
}
```

# <a name="c"></a>[<span data-ttu-id="1900b-206">C#</span><span class="sxs-lookup"><span data-stu-id="1900b-206">C#</span></span>](#tab/csharp)

<span data-ttu-id="1900b-207">以下代码显示了一个操作 `signin` 类型示例C#：</span><span class="sxs-lookup"><span data-stu-id="1900b-207">The following code shows an example of `signin` action type in C#:</span></span>

```csharp
var button = new CardAction()
{
    Type = ActionTypes.Signin,
    Title = "Click me for signin",
    Value = "https://signin.com"
};
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="1900b-208">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="1900b-208">JavaScript/Node.js</span></span>](#tab/javascript)

<span data-ttu-id="1900b-209">以下代码显示了 `signin` JavaScript 中的操作类型示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-209">The following code shows an example of `signin` action type in JavaScript:</span></span>

```javascript
CardFactory.actions([
{
    type: "signin",
    title: "Click me for signin",
    value: "https://signin.com"
}])
```

---

## <a name="adaptive-cards-actions"></a><span data-ttu-id="1900b-210">自适应卡片操作</span><span class="sxs-lookup"><span data-stu-id="1900b-210">Adaptive Cards actions</span></span>

<span data-ttu-id="1900b-211">自适应卡片支持四种操作类型：</span><span class="sxs-lookup"><span data-stu-id="1900b-211">Adaptive Cards support four action types:</span></span>

* [<span data-ttu-id="1900b-212">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="1900b-212">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="1900b-213">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="1900b-213">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="1900b-214">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="1900b-214">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)
* [<span data-ttu-id="1900b-215">Action.Execute</span><span class="sxs-lookup"><span data-stu-id="1900b-215">Action.Execute</span></span>](/adaptive-cards/authoring-cards/universal-action-model#actionexecute)

<span data-ttu-id="1900b-216">还可以修改自适应卡片有效负载，以支持使用 对象中的 属性执行现有 `Action.Submit` Bot Framework `msteams` `data` 操作 `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="1900b-216">You can also modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using an `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="1900b-217">下一部分详细介绍了如何将现有 Bot Framework 操作与自适应卡片一同使用。</span><span class="sxs-lookup"><span data-stu-id="1900b-217">The next section provide details on how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="1900b-218">使用 `msteams` Bot Framework 操作向数据添加操作不能用于自适应卡片任务模块。</span><span class="sxs-lookup"><span data-stu-id="1900b-218">Adding `msteams` to data with a Bot Framework action does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="1900b-219">具有 messageBack 操作自适应卡片</span><span class="sxs-lookup"><span data-stu-id="1900b-219">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="1900b-220">若要在 `messageBack` 自适应卡片中包括操作，请包含对象中的以下 `msteams` 详细信息：</span><span class="sxs-lookup"><span data-stu-id="1900b-220">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="1900b-221">如果需要，可以在对象中包括其他 `data` 隐藏属性。</span><span class="sxs-lookup"><span data-stu-id="1900b-221">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="1900b-222">属性</span><span class="sxs-lookup"><span data-stu-id="1900b-222">Property</span></span> | <span data-ttu-id="1900b-223">说明</span><span class="sxs-lookup"><span data-stu-id="1900b-223">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="1900b-224">设置为 `messageBack` 。</span><span class="sxs-lookup"><span data-stu-id="1900b-224">Set to `messageBack`.</span></span> |
| `displayText` | <span data-ttu-id="1900b-225">可选。</span><span class="sxs-lookup"><span data-stu-id="1900b-225">Optional.</span></span> <span data-ttu-id="1900b-226">操作执行时由聊天流中的用户使用。</span><span class="sxs-lookup"><span data-stu-id="1900b-226">Used by the user in the chat stream when the action is performed.</span></span> <span data-ttu-id="1900b-227">此文本不会发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="1900b-227">This text is not sent to your bot.</span></span> |
| `value` | <span data-ttu-id="1900b-228">操作执行时发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="1900b-228">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="1900b-229">你可以为操作（如唯一标识符或 JSON 对象）对上下文进行编码。</span><span class="sxs-lookup"><span data-stu-id="1900b-229">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="1900b-230">操作执行时发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="1900b-230">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="1900b-231">使用此属性可简化机器人开发。</span><span class="sxs-lookup"><span data-stu-id="1900b-231">Use this property to simplify bot development.</span></span> <span data-ttu-id="1900b-232">代码可以检查单个顶级属性以调度自动程序逻辑。</span><span class="sxs-lookup"><span data-stu-id="1900b-232">Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="1900b-233">以下代码显示了操作自适应卡片 `messageBack` 的示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-233">The following code shows an example of Adaptive Cards with `messageBack` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for messageBack",
  "data": {
    "msteams": {
        "type": "messageBack",
        "displayText": "I clicked this button",
        "text": "text to bots",
        "value": "{\"bfKey\": \"bfVal\", \"conflictKey\": \"from value\"}"
    }
  }
}
```

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="1900b-234">使用 imBack 操作自适应卡片</span><span class="sxs-lookup"><span data-stu-id="1900b-234">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="1900b-235">若要在 `imBack` 自适应卡片中包括操作，请包含 对象中的以下 `msteams` 详细信息：</span><span class="sxs-lookup"><span data-stu-id="1900b-235">To include an `imBack` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="1900b-236">如果需要，可以在对象中包括其他 `data` 隐藏属性。</span><span class="sxs-lookup"><span data-stu-id="1900b-236">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="1900b-237">属性</span><span class="sxs-lookup"><span data-stu-id="1900b-237">Property</span></span> | <span data-ttu-id="1900b-238">说明</span><span class="sxs-lookup"><span data-stu-id="1900b-238">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="1900b-239">设置为 `imBack` 。</span><span class="sxs-lookup"><span data-stu-id="1900b-239">Set to `imBack`.</span></span> |
| `value` | <span data-ttu-id="1900b-240">需要在聊天中回显的字符串。</span><span class="sxs-lookup"><span data-stu-id="1900b-240">String that needs to be echoed back in the chat.</span></span> |

<span data-ttu-id="1900b-241">以下代码显示了操作自适应卡片 `imBack` 的示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-241">The following code shows an example of Adaptive Cards with `imBack` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for imBack",
  "data": {
    "msteams": {
        "type": "imBack",
        "value": "Text to reply in chat"
    }
  }
}
```

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="1900b-242">带登录操作自适应卡片</span><span class="sxs-lookup"><span data-stu-id="1900b-242">Adaptive Cards with signin action</span></span>

<span data-ttu-id="1900b-243">若要在 `signin` 自适应卡片中包括操作，请包含对象中的以下 `msteams` 详细信息：</span><span class="sxs-lookup"><span data-stu-id="1900b-243">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="1900b-244">如果需要，可以在对象中包括其他 `data` 隐藏属性。</span><span class="sxs-lookup"><span data-stu-id="1900b-244">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="1900b-245">属性</span><span class="sxs-lookup"><span data-stu-id="1900b-245">Property</span></span> | <span data-ttu-id="1900b-246">说明</span><span class="sxs-lookup"><span data-stu-id="1900b-246">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="1900b-247">设置为 `signin` 。</span><span class="sxs-lookup"><span data-stu-id="1900b-247">Set to `signin`.</span></span> |
| `value` | <span data-ttu-id="1900b-248">设置为要重定向的 URL。</span><span class="sxs-lookup"><span data-stu-id="1900b-248">Set to the URL where you want to redirect.</span></span>  |

<span data-ttu-id="1900b-249">以下代码显示了操作自适应卡片 `signin` 的示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-249">The following code shows an example of Adaptive Cards with `signin` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "Click me for signin",
  "data": {
    "msteams": {
        "type": "signin",
        "value": "https://signin.com"
    }
  }
}
```

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="1900b-250">具有调用操作的自适应卡片</span><span class="sxs-lookup"><span data-stu-id="1900b-250">Adaptive Cards with invoke action</span></span>

<span data-ttu-id="1900b-251">若要在 `invoke` 自适应卡片中包括操作，请包含 对象中的以下 `msteams` 详细信息：</span><span class="sxs-lookup"><span data-stu-id="1900b-251">To include an `invoke` action with an Adaptive Card include the following details in the `msteams` object:</span></span>

> [!NOTE]
> <span data-ttu-id="1900b-252">如果需要，可以在对象中包括其他 `data` 隐藏属性。</span><span class="sxs-lookup"><span data-stu-id="1900b-252">You can include additional hidden properties in the `data` object, if required.</span></span>

| <span data-ttu-id="1900b-253">属性</span><span class="sxs-lookup"><span data-stu-id="1900b-253">Property</span></span> | <span data-ttu-id="1900b-254">说明</span><span class="sxs-lookup"><span data-stu-id="1900b-254">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="1900b-255">设置为 `task/fetch` 。</span><span class="sxs-lookup"><span data-stu-id="1900b-255">Set to `task/fetch`.</span></span> |
| `data` | <span data-ttu-id="1900b-256">设置值。</span><span class="sxs-lookup"><span data-stu-id="1900b-256">Set the value.</span></span>  |

<span data-ttu-id="1900b-257">以下代码显示了操作自适应卡片 `invoke` 的示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-257">The following code shows an example of Adaptive Cards with `invoke` action:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    }
  }
}
```

<span data-ttu-id="1900b-258">以下代码显示了具有其他有效负载数据的自适应卡片 `invoke` 示例：</span><span class="sxs-lookup"><span data-stu-id="1900b-258">The following code shows an example of Adaptive Cards with `invoke` action with additional payload data:</span></span>

```json
{
  "type": "Action.Submit",
  "title": "submit"
  "data": {
    "msteams": {
        "type": "task/fetch"
    },
    "Value1": "some value"
  }
}
```

## <a name="see-also"></a><span data-ttu-id="1900b-259">另请参阅</span><span class="sxs-lookup"><span data-stu-id="1900b-259">See also</span></span>

[<span data-ttu-id="1900b-260">卡参考</span><span class="sxs-lookup"><span data-stu-id="1900b-260">Cards reference</span></span>](./cards-reference.md)

## <a name="next-step"></a><span data-ttu-id="1900b-261">后续步骤</span><span class="sxs-lookup"><span data-stu-id="1900b-261">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="1900b-262">自适应卡的通用操作</span><span class="sxs-lookup"><span data-stu-id="1900b-262">Universal Actions for Adaptive Cards</span></span>](../cards/Universal-actions-for-adaptive-cards/Overview.md)
