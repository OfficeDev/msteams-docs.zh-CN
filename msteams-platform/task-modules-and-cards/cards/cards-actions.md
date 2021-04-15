---
title: 在自动程序中添加卡片操作
description: 介绍 Microsoft Teams 中的卡片操作以及如何在机器人中使用它们
ms.topic: conceptual
keywords: teams 机器人卡片操作
ms.openlocfilehash: f02e195f619fdfa2ebbc4b2ef00669a1cb5b38f6
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696022"
---
# <a name="card-actions"></a><span data-ttu-id="5f6c8-104">卡片操作</span><span class="sxs-lookup"><span data-stu-id="5f6c8-104">Card actions</span></span>

<span data-ttu-id="5f6c8-105">Teams 中的机器人和消息传递扩展使用的卡片支持以下 () [`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) 类型。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-105">Cards used by bots and messaging extensions in Teams support the following activity ([`CardAction`](/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)) types.</span></span> <span data-ttu-id="5f6c8-106">请注意，在使用连接器时， `potentialActions` 这些操作不同于 Office 365 连接器卡。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-106">Note that these actions differ from `potentialActions` for Office 365 Connector cards when used from Connectors.</span></span>

| <span data-ttu-id="5f6c8-107">类型</span><span class="sxs-lookup"><span data-stu-id="5f6c8-107">Type</span></span> | <span data-ttu-id="5f6c8-108">Action</span><span class="sxs-lookup"><span data-stu-id="5f6c8-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="5f6c8-109">在默认浏览器中打开 URL。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="5f6c8-110">从单击按钮或点击卡片 (用户向聊天机器人发送消息和负载) 并将单独的消息发送到聊天流。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-110">Sends a message and payload to the bot (from the user who clicked the button or tapped the card) and sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="5f6c8-111">从单击该按钮 (点击卡片的用户向自动程序发送) 。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-111">Sends a message to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="5f6c8-112">此消息 (对话参与者) 自动程序"消息。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-112">This message (from user to bot) is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="5f6c8-113">从单击按钮或点击卡片 (用户向自动程序发送一条消息和负载) 。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-113">Sends a message and payload to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="5f6c8-114">此消息不可见。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-114">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="5f6c8-115">启动 OAuth 流，允许机器人与安全服务连接。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-115">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="5f6c8-116">Teams 不支持 `CardAction` 上表中未列出的类型。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-116">Teams does not support `CardAction` types not listed in the preceding table.</span></span>
>* <span data-ttu-id="5f6c8-117">Teams 不支持 `potentialActions` 属性。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-117">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="5f6c8-118">卡片操作不同于 Bot [](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) Framework/Azure Bot Service 中的建议操作。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-118">Card actions are different than [suggested actions](/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button&preserve-view=true) in Bot Framework/Azure Bot Service.</span></span> <span data-ttu-id="5f6c8-119">建议的操作在 Microsoft Teams 中不受支持：如果你希望按钮出现在 Teams 自动程序消息中，请使用卡片。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-119">Suggested actions are not supported in Microsoft Teams: if you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="5f6c8-120">如果你使用卡片操作作为邮件扩展的一部分，那么在将卡片提交到频道之前，这些操作将不起作用 (当卡片位于撰写消息框中时) 。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-120">If you're using a card action as part of a messaging extension, the actions will be not work until the card is submitted to the channel (they will not work while the card is in the compose message box).</span></span>

<span data-ttu-id="5f6c8-121">Teams 还 [支持自适应卡片操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)，这些操作仅由自适应卡片使用。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-121">Teams also supports [Adaptive Cards actions](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), which are only used by Adaptive Cards.</span></span> <span data-ttu-id="5f6c8-122">这些操作将在此参考末尾的其自己的部分中列出。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-122">These actions are listed in their own section at the end of this reference.</span></span>

## <a name="openurl"></a><span data-ttu-id="5f6c8-123">openUrl</span><span class="sxs-lookup"><span data-stu-id="5f6c8-123">openUrl</span></span>

<span data-ttu-id="5f6c8-124">此操作类型指定在默认浏览器中启动的 URL。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-124">This action type specifies a URL to launch in the default browser.</span></span> <span data-ttu-id="5f6c8-125">请注意，自动程序不会收到有关单击哪个按钮的任何通知。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-125">Note that your bot does not receive any notice on which button was clicked.</span></span>

<span data-ttu-id="5f6c8-126">字段 `value` 必须包含格式正确的完整 URL。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-126">The `value` field must contain a full and properly formed URL.</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a><span data-ttu-id="5f6c8-127">messageBack</span><span class="sxs-lookup"><span data-stu-id="5f6c8-127">messageBack</span></span>

<span data-ttu-id="5f6c8-128">使用 `messageBack` ，可以创建具有以下属性的完全自定义操作：</span><span class="sxs-lookup"><span data-stu-id="5f6c8-128">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="5f6c8-129">属性</span><span class="sxs-lookup"><span data-stu-id="5f6c8-129">Property</span></span> | <span data-ttu-id="5f6c8-130">说明</span><span class="sxs-lookup"><span data-stu-id="5f6c8-130">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="5f6c8-131">显示为按钮标签。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-131">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="5f6c8-132">可选。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-132">Optional.</span></span> <span data-ttu-id="5f6c8-133">用户执行该操作时回显到聊天流中。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-133">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="5f6c8-134">此文本 *不会* 发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-134">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="5f6c8-135">操作执行时发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-135">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="5f6c8-136">你可以为操作（如唯一标识符或 JSON 对象）对上下文进行编码。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-136">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="5f6c8-137">操作执行时发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-137">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="5f6c8-138">使用此属性可简化机器人开发：代码可以检查单个顶级属性以调度自动程序逻辑。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-138">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="5f6c8-139">灵活性意味着代码只需使用 ，就可以选择不在历史记录中留下 `messageBack` 可见的用户消息 `displayText` 。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-139">The flexibility of `messageBack` means that your code can choose not to leave a visible user message in the history simply by not using `displayText`.</span></span>

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

<span data-ttu-id="5f6c8-140">该属性 `value` 可以是序列化的 JSON 字符串或 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-140">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

### <a name="inbound-message-example"></a><span data-ttu-id="5f6c8-141">入站邮件示例</span><span class="sxs-lookup"><span data-stu-id="5f6c8-141">Inbound message example</span></span>

<span data-ttu-id="5f6c8-142">`replyToId` 包含卡片操作所来自的邮件的 ID。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-142">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="5f6c8-143">如果要更新邮件，请使用它。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-143">Use it if you want to update the message.</span></span>

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

## <a name="imback"></a><span data-ttu-id="5f6c8-144">imBack</span><span class="sxs-lookup"><span data-stu-id="5f6c8-144">imBack</span></span>

<span data-ttu-id="5f6c8-145">此操作会触发向自动程序发送的返回消息，就像用户在普通聊天消息中键入一样。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-145">This action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="5f6c8-146">你的用户和所有其他用户在频道中都将看到该按钮响应。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-146">Your user, and all other users if in a channel, will see that button response.</span></span>

<span data-ttu-id="5f6c8-147">字段 `value` 应包含聊天中回显的文本字符串，因此发送回聊天机器人。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-147">The `value` field should contain the text string echoed in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="5f6c8-148">这是将在自动程序中处理的消息文本，以执行所需的逻辑。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-148">This is the message text you will process in your bot to perform the desired logic.</span></span> <span data-ttu-id="5f6c8-149">注意：此字段是一个简单的字符串 - 不支持格式设置或隐藏字符。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-149">Note: this field is a simple string - there is no support for formatting or hidden characters.</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a><span data-ttu-id="5f6c8-150">invoke</span><span class="sxs-lookup"><span data-stu-id="5f6c8-150">invoke</span></span>

<span data-ttu-id="5f6c8-151">`invoke`操作用于调用任务[模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-151">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="5f6c8-152">操作 `invoke` 包含三个属性 `type` ：、 `title` 和 `value` 。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-152">The `invoke` action contains three properties: `type`, `title`, and `value`.</span></span> <span data-ttu-id="5f6c8-153">该属性 `value` 可以包含字符串、字符串化 JSON 对象或 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-153">The `value` property can contain a string, a stringified JSON object, or a JSON object.</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="5f6c8-154">当用户单击该按钮时，机器人将收到 `value` 包含其他一些信息的对象。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-154">When a user clicks the button, your bot will receive the `value` object with some additional info.</span></span> <span data-ttu-id="5f6c8-155">请注意，活动类型将 `invoke` 改为 (`message` `activity.Type == "invoke"`) 。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-155">Please note that the activity type will be `invoke` instead of `message` (`activity.Type == "invoke"`).</span></span>

### <a name="example-invoke-button-definition-net"></a><span data-ttu-id="5f6c8-156">示例：调用按钮定义 (.NET) </span><span class="sxs-lookup"><span data-stu-id="5f6c8-156">Example: Invoke button definition (.NET)</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a><span data-ttu-id="5f6c8-157">示例：传入调用消息</span><span class="sxs-lookup"><span data-stu-id="5f6c8-157">Example: Incoming invoke message</span></span>

<span data-ttu-id="5f6c8-158">顶级属性包含卡片 `replyToId` 操作所来自的邮件的 ID。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-158">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="5f6c8-159">如果要更新邮件，请使用它。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-159">Use it if you want to update the message.</span></span>

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

## <a name="signin"></a><span data-ttu-id="5f6c8-160">signin</span><span class="sxs-lookup"><span data-stu-id="5f6c8-160">signin</span></span>

<span data-ttu-id="5f6c8-161">启动 OAuth 流，允许机器人与安全服务连接，如以下更加详细地介绍：自动 [程序中的身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-161">Initiates an OAuth flow, allowing bots to connect with secure services, as described in more detail here: [Authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

## <a name="adaptive-cards-actions"></a><span data-ttu-id="5f6c8-162">自适应卡片操作</span><span class="sxs-lookup"><span data-stu-id="5f6c8-162">Adaptive Cards actions</span></span>

<span data-ttu-id="5f6c8-163">自适应卡片支持三种操作类型：</span><span class="sxs-lookup"><span data-stu-id="5f6c8-163">Adaptive Cards support three action types:</span></span>

* [<span data-ttu-id="5f6c8-164">Action.OpenUrl</span><span class="sxs-lookup"><span data-stu-id="5f6c8-164">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="5f6c8-165">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="5f6c8-165">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="5f6c8-166">Action.ShowCard</span><span class="sxs-lookup"><span data-stu-id="5f6c8-166">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)

<span data-ttu-id="5f6c8-167">除了上述操作之外，还可以修改自适应卡片有效负载，以支持使用 对象中的 属性执行现有 `Action.Submit` Bot Framework `msteams` `data` 操作 `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-167">In addition to the actions mentioned above, you can modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using a `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="5f6c8-168">以下各节详细介绍了如何将现有 Bot Framework 操作与自适应卡片一同使用。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-168">The below sections detail how to use existing Bot Framework actions with Adaptive Cards.</span></span>

> [!NOTE]
> <span data-ttu-id="5f6c8-169">使用 Bot Framework 操作向数据 `msteams` 添加内容不能用于自适应卡片任务模块。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-169">Adding `msteams` to data, with a Bot Framework action, does not work with an Adaptive Card task module.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="5f6c8-170">具有 messageBack 操作自适应卡片</span><span class="sxs-lookup"><span data-stu-id="5f6c8-170">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="5f6c8-171">若要在 `messageBack` 自适应卡片中包括操作，请包含 对象中的以下 `msteams` 详细信息。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-171">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="5f6c8-172">请注意，如果需要，可以在 对象中包括其他 `data` 隐藏属性。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-172">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="5f6c8-173">属性</span><span class="sxs-lookup"><span data-stu-id="5f6c8-173">Property</span></span> | <span data-ttu-id="5f6c8-174">说明</span><span class="sxs-lookup"><span data-stu-id="5f6c8-174">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="5f6c8-175">设置为 `messageBack`</span><span class="sxs-lookup"><span data-stu-id="5f6c8-175">Set to `messageBack`</span></span> |
| `displayText` | <span data-ttu-id="5f6c8-176">可选。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-176">Optional.</span></span> <span data-ttu-id="5f6c8-177">用户执行该操作时回显到聊天流中。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-177">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="5f6c8-178">此文本 *不会* 发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-178">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="5f6c8-179">操作执行时发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-179">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="5f6c8-180">你可以为操作（如唯一标识符或 JSON 对象）对上下文进行编码。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-180">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="5f6c8-181">操作执行时发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-181">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="5f6c8-182">使用此属性可简化机器人开发：代码可以检查单个顶级属性以调度自动程序逻辑。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-182">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

#### <a name="example"></a><span data-ttu-id="5f6c8-183">示例</span><span class="sxs-lookup"><span data-stu-id="5f6c8-183">Example</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="5f6c8-184">使用 imBack 操作自适应卡片</span><span class="sxs-lookup"><span data-stu-id="5f6c8-184">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="5f6c8-185">若要在 `imBack` 自适应卡片中包括操作，请包含 对象中的以下 `msteams` 详细信息。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-185">To include a `imBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="5f6c8-186">请注意，如果需要，可以在 对象中包括其他 `data` 隐藏属性。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-186">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="5f6c8-187">属性</span><span class="sxs-lookup"><span data-stu-id="5f6c8-187">Property</span></span> | <span data-ttu-id="5f6c8-188">说明</span><span class="sxs-lookup"><span data-stu-id="5f6c8-188">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="5f6c8-189">设置为 `imBack`</span><span class="sxs-lookup"><span data-stu-id="5f6c8-189">Set to `imBack`</span></span> |
| `value` | <span data-ttu-id="5f6c8-190">需要在聊天中回显的字符串</span><span class="sxs-lookup"><span data-stu-id="5f6c8-190">String that needs to be echoed back in the chat</span></span> |

#### <a name="example"></a><span data-ttu-id="5f6c8-191">示例</span><span class="sxs-lookup"><span data-stu-id="5f6c8-191">Example</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="5f6c8-192">带登录操作自适应卡片</span><span class="sxs-lookup"><span data-stu-id="5f6c8-192">Adaptive Cards with signin action</span></span>

<span data-ttu-id="5f6c8-193">若要在 `signin` 自适应卡片中包括操作，请包含 对象中的以下 `msteams` 详细信息。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-193">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="5f6c8-194">请注意，如果需要，可以在 对象中包括其他 `data` 隐藏属性。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-194">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="5f6c8-195">属性</span><span class="sxs-lookup"><span data-stu-id="5f6c8-195">Property</span></span> | <span data-ttu-id="5f6c8-196">说明</span><span class="sxs-lookup"><span data-stu-id="5f6c8-196">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="5f6c8-197">设置为 `signin`</span><span class="sxs-lookup"><span data-stu-id="5f6c8-197">Set to `signin`</span></span> |
| `value` | <span data-ttu-id="5f6c8-198">设置为要重定向到的 URL</span><span class="sxs-lookup"><span data-stu-id="5f6c8-198">Set to the URL that you want to redirect to</span></span>  |

#### <a name="example"></a><span data-ttu-id="5f6c8-199">示例</span><span class="sxs-lookup"><span data-stu-id="5f6c8-199">Example</span></span>

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

### <a name="adaptive-cards-with-invoke-action"></a><span data-ttu-id="5f6c8-200">具有调用操作的自适应卡片</span><span class="sxs-lookup"><span data-stu-id="5f6c8-200">Adaptive Cards with invoke action</span></span>
 
<span data-ttu-id="5f6c8-201">若要在 `invoke` 自适应卡片中包括操作，请包含 对象中的以下 `msteams` 详细信息。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-201">To include a `invoke` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="5f6c8-202">请注意，如果需要，可以在 对象中包括其他 `data` 隐藏属性。</span><span class="sxs-lookup"><span data-stu-id="5f6c8-202">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="5f6c8-203">属性</span><span class="sxs-lookup"><span data-stu-id="5f6c8-203">Property</span></span> | <span data-ttu-id="5f6c8-204">说明</span><span class="sxs-lookup"><span data-stu-id="5f6c8-204">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="5f6c8-205">设置为 `task/fetch`</span><span class="sxs-lookup"><span data-stu-id="5f6c8-205">Set to `task/fetch`</span></span> |
| `data` | <span data-ttu-id="5f6c8-206">设置值</span><span class="sxs-lookup"><span data-stu-id="5f6c8-206">Set the value</span></span>  |

#### <a name="example"></a><span data-ttu-id="5f6c8-207">示例</span><span class="sxs-lookup"><span data-stu-id="5f6c8-207">Example</span></span>

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

#### <a name="example-2-with-additional-payload-data"></a><span data-ttu-id="5f6c8-208">示例 2 (附加有效负载数据) </span><span class="sxs-lookup"><span data-stu-id="5f6c8-208">Example 2 (with additional payload data)</span></span>

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
