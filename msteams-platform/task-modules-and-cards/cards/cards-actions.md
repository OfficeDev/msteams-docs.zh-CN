---
title: 在 bot 中添加卡片操作
description: 介绍 Microsoft 团队中的卡片操作以及如何在你的 bot 中使用它们
keywords: 团队 bot 卡片操作
ms.openlocfilehash: e0b050cde9adf5bd811d5d95ce1c6f1bf60546a1
ms.sourcegitcommit: fdcd91b270d4c2e98ab2b2c1029c76c49bb807fa
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/13/2020
ms.locfileid: "44801027"
---
# <a name="card-actions"></a><span data-ttu-id="9be65-104">卡片操作</span><span class="sxs-lookup"><span data-stu-id="9be65-104">Card actions</span></span>

<span data-ttu-id="9be65-105">由团队中的 bot 和邮件分机使用的卡片支持以下活动（ [`CardAction`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards) ）类型。</span><span class="sxs-lookup"><span data-stu-id="9be65-105">Cards used by bots and messaging extensions in Teams support the following activity ([`CardAction`](https://docs.microsoft.com/bot-framework/dotnet/bot-builder-dotnet-add-rich-card-attachments#process-events-within-rich-cards)) types.</span></span> <span data-ttu-id="9be65-106">请注意， `potentialActions` 从连接器使用时，这些操作与 Office 365 连接器卡有所不同。</span><span class="sxs-lookup"><span data-stu-id="9be65-106">Note that these actions differ from `potentialActions` for Office 365 Connector cards when used from Connectors.</span></span>

| <span data-ttu-id="9be65-107">类型</span><span class="sxs-lookup"><span data-stu-id="9be65-107">Type</span></span> | <span data-ttu-id="9be65-108">Action</span><span class="sxs-lookup"><span data-stu-id="9be65-108">Action</span></span> |
| --- | --- |
| `openUrl` | <span data-ttu-id="9be65-109">在默认浏览器中打开 URL。</span><span class="sxs-lookup"><span data-stu-id="9be65-109">Opens a URL in the default browser.</span></span> |
| `messageBack` | <span data-ttu-id="9be65-110">将邮件和有效负载发送到 bot （从单击按钮或点击卡片的用户），并将单独的邮件发送到聊天流。</span><span class="sxs-lookup"><span data-stu-id="9be65-110">Sends a message and payload to the bot (from the user who clicked the button or tapped the card) and sends a separate message to the chat stream.</span></span> |
| `imBack`| <span data-ttu-id="9be65-111">将邮件发送到自动程序（从单击按钮的用户或通过点击卡片）。</span><span class="sxs-lookup"><span data-stu-id="9be65-111">Sends a message to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="9be65-112">此邮件（从用户到 bot）对所有对话参与者均可见。</span><span class="sxs-lookup"><span data-stu-id="9be65-112">This message (from user to bot) is visible to all conversation participants.</span></span> |
| `invoke` | <span data-ttu-id="9be65-113">将邮件和有效负载发送到机器人（从单击按钮的用户或通过点击卡片）。</span><span class="sxs-lookup"><span data-stu-id="9be65-113">Sends a message and payload to the bot (from the user who clicked the button or tapped the card).</span></span> <span data-ttu-id="9be65-114">此消息不可见。</span><span class="sxs-lookup"><span data-stu-id="9be65-114">This message is not visible.</span></span> |
| `signin` | <span data-ttu-id="9be65-115">启动 OAuth 流，允许 bot 与安全服务连接。</span><span class="sxs-lookup"><span data-stu-id="9be65-115">Initiates OAuth flow, allowing bots to connect with secure services.</span></span> |

> [!NOTE]
>* <span data-ttu-id="9be65-116">团队不支持 `CardAction` 上表中未列出的类型。</span><span class="sxs-lookup"><span data-stu-id="9be65-116">Teams does not support `CardAction` types not listed in the preceding table.</span></span>
>* <span data-ttu-id="9be65-117">团队不支持该 `potentialActions` 属性。</span><span class="sxs-lookup"><span data-stu-id="9be65-117">Teams does not support the `potentialActions` property.</span></span>
>* <span data-ttu-id="9be65-118">卡片操作与 Bot 框架/Azure Bot 服务中的[建议操作](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button)不同。</span><span class="sxs-lookup"><span data-stu-id="9be65-118">Card actions are different than [suggested actions](https://docs.microsoft.com/azure/bot-service/bot-builder-howto-add-suggested-actions?view=azure-bot-service-4.0&tabs=javascript#suggest-action-using-button) in Bot Framework/Azure Bot Service.</span></span> <span data-ttu-id="9be65-119">Microsoft 团队不支持建议的操作：如果希望按钮显示在 "团队" bot 邮件中，请使用卡片。</span><span class="sxs-lookup"><span data-stu-id="9be65-119">Suggested actions are not supported in Microsoft Teams: if you want buttons to appear on a Teams bot message, use a card.</span></span>
>* <span data-ttu-id="9be65-120">如果使用的是作为邮件扩展一部分的卡片操作，则在将该卡片提交到频道之前，操作将不起作用（当卡片在撰写消息框中时，这些操作将不起作用）。</span><span class="sxs-lookup"><span data-stu-id="9be65-120">If you're using a card action as part of a messaging extension, the actions will be not work until the card is submitted to the channel (they will not work while the card is in the compose message box).</span></span>

<span data-ttu-id="9be65-121">团队还支持[自适应卡片操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)，仅供自适应卡片使用。</span><span class="sxs-lookup"><span data-stu-id="9be65-121">Teams also supports [Adaptive Cards actions](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions), which are only used by Adaptive Cards.</span></span> <span data-ttu-id="9be65-122">这些操作在本参考结束时在各自的部分中列出。</span><span class="sxs-lookup"><span data-stu-id="9be65-122">These actions are listed in their own section at the end of this reference.</span></span>

## <a name="openurl"></a><span data-ttu-id="9be65-123">openUrl</span><span class="sxs-lookup"><span data-stu-id="9be65-123">openUrl</span></span>

<span data-ttu-id="9be65-124">此操作类型指定要在默认浏览器中启动的 URL。</span><span class="sxs-lookup"><span data-stu-id="9be65-124">This action type specifies a URL to launch in the default browser.</span></span> <span data-ttu-id="9be65-125">请注意，你的 bot 不会收到单击了哪个按钮的任何通知。</span><span class="sxs-lookup"><span data-stu-id="9be65-125">Note that your bot does not receive any notice on which button was clicked.</span></span>

<span data-ttu-id="9be65-126">`value`字段必须包含完整且格式正确的 URL。</span><span class="sxs-lookup"><span data-stu-id="9be65-126">The `value` field must contain a full and properly formed URL.</span></span>

```json
{
    "type": "openUrl",
    "title": "Tabs in Teams",
    "value": "https://msdn.microsoft.com/microsoft-teams/tabs"
}
```

## <a name="messageback"></a><span data-ttu-id="9be65-127">messageBack</span><span class="sxs-lookup"><span data-stu-id="9be65-127">messageBack</span></span>

<span data-ttu-id="9be65-128">使用 `messageBack` ，您可以创建具有以下属性的完全自定义操作：</span><span class="sxs-lookup"><span data-stu-id="9be65-128">With `messageBack`, you can create a fully customized action with the following properties:</span></span>

| <span data-ttu-id="9be65-129">属性</span><span class="sxs-lookup"><span data-stu-id="9be65-129">Property</span></span> | <span data-ttu-id="9be65-130">说明</span><span class="sxs-lookup"><span data-stu-id="9be65-130">Description</span></span> |
| --- | --- |
| `title` | <span data-ttu-id="9be65-131">显示为按钮标签。</span><span class="sxs-lookup"><span data-stu-id="9be65-131">Appears as the button label.</span></span> |
| `displayText` | <span data-ttu-id="9be65-132">可选。</span><span class="sxs-lookup"><span data-stu-id="9be65-132">Optional.</span></span> <span data-ttu-id="9be65-133">在执行操作时，用户在聊天流中回显。</span><span class="sxs-lookup"><span data-stu-id="9be65-133">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="9be65-134">此文本*不*会发送到你的机器人。</span><span class="sxs-lookup"><span data-stu-id="9be65-134">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="9be65-135">在执行操作时发送到你的 bot。</span><span class="sxs-lookup"><span data-stu-id="9be65-135">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="9be65-136">您可以对操作的上下文进行编码，例如唯一标识符或 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="9be65-136">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="9be65-137">在执行操作时发送到你的 bot。</span><span class="sxs-lookup"><span data-stu-id="9be65-137">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="9be65-138">使用此属性可简化 bot 的开发：您的代码可以检查单个顶级属性以调度 bot 逻辑。</span><span class="sxs-lookup"><span data-stu-id="9be65-138">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

<span data-ttu-id="9be65-139">这 `messageBack` 意味着您的代码可以选择不使用，而只是在历史记录中留下可见的用户消息 `displayText` 。</span><span class="sxs-lookup"><span data-stu-id="9be65-139">The flexibility of `messageBack` means that your code can choose not to leave a visible user message in the history simply by not using `displayText`.</span></span>

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

<span data-ttu-id="9be65-140">该 `value` 属性可以是序列化的 json 字符串，也可以是 json 对象。</span><span class="sxs-lookup"><span data-stu-id="9be65-140">The `value` property can be either a serialized JSON string or a JSON object.</span></span>

### <a name="inbound-message-example"></a><span data-ttu-id="9be65-141">入站邮件示例</span><span class="sxs-lookup"><span data-stu-id="9be65-141">Inbound message example</span></span>

<span data-ttu-id="9be65-142">`replyToId`包含卡操作来自的邮件的 ID。</span><span class="sxs-lookup"><span data-stu-id="9be65-142">`replyToId` contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="9be65-143">如果要更新邮件，请使用此方法。</span><span class="sxs-lookup"><span data-stu-id="9be65-143">Use it if you want to update the message.</span></span>

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

## <a name="imback"></a><span data-ttu-id="9be65-144">imBack</span><span class="sxs-lookup"><span data-stu-id="9be65-144">imBack</span></span>

<span data-ttu-id="9be65-145">此操作会触发到你的 bot 的返回邮件，就像用户在正常聊天消息中键入它一样。</span><span class="sxs-lookup"><span data-stu-id="9be65-145">This action triggers a return message to your bot, as if the user typed it in a normal chat message.</span></span> <span data-ttu-id="9be65-146">如果你的用户和所有其他用户在频道中，将会看到按钮响应。</span><span class="sxs-lookup"><span data-stu-id="9be65-146">Your user, and all other users if in a channel, will see that button response.</span></span>

<span data-ttu-id="9be65-147">该 `value` 字段应包含聊天中的文本字符串回显，从而发回机器人。</span><span class="sxs-lookup"><span data-stu-id="9be65-147">The `value` field should contain the text string echoed in the chat and therefore sent back to the bot.</span></span> <span data-ttu-id="9be65-148">这是将在你的 bot 中处理的邮件文本，以执行所需的逻辑。</span><span class="sxs-lookup"><span data-stu-id="9be65-148">This is the message text you will process in your bot to perform the desired logic.</span></span> <span data-ttu-id="9be65-149">注意：此字段是一个简单的字符串，不支持格式化或隐藏字符。</span><span class="sxs-lookup"><span data-stu-id="9be65-149">Note: this field is a simple string - there is no support for formatting or hidden characters.</span></span>

```json
{
    "type": "imBack",
    "title": "More",
    "value": "Show me more"
}
```

## <a name="invoke"></a><span data-ttu-id="9be65-150">调</span><span class="sxs-lookup"><span data-stu-id="9be65-150">invoke</span></span>

<span data-ttu-id="9be65-151">该 `invoke` 操作用于调用[任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)。</span><span class="sxs-lookup"><span data-stu-id="9be65-151">The `invoke` action is used for invoking [task modules](~/task-modules-and-cards/task-modules/task-modules-bots.md).</span></span>

<span data-ttu-id="9be65-152">`invoke`操作包含三个属性： `type` 、 `title` 和 `value` 。</span><span class="sxs-lookup"><span data-stu-id="9be65-152">The `invoke` action contains three properties: `type`, `title`, and `value`.</span></span> <span data-ttu-id="9be65-153">`value`属性可以包含字符串、字符串化 JSON 对象或 json 对象。</span><span class="sxs-lookup"><span data-stu-id="9be65-153">The `value` property can contain a string, a stringified JSON object, or a JSON object.</span></span>

```json
{
    "type": "invoke",
    "title": "Option 1",
    "value": {
        "option": "opt1"
    }
}
```

<span data-ttu-id="9be65-154">当用户单击此按钮时，你的 bot 将接收 `value` 具有一些其他信息的对象。</span><span class="sxs-lookup"><span data-stu-id="9be65-154">When a user clicks the button, your bot will receive the `value` object with some additional info.</span></span> <span data-ttu-id="9be65-155">请注意，活动类型将为 `invoke` 而不是 `message` （ `activity.Type == "invoke"` ）。</span><span class="sxs-lookup"><span data-stu-id="9be65-155">Please note that the activity type will be `invoke` instead of `message` (`activity.Type == "invoke"`).</span></span>

### <a name="example-invoke-button-definition-net"></a><span data-ttu-id="9be65-156">示例： Invoke button definition （.NET）</span><span class="sxs-lookup"><span data-stu-id="9be65-156">Example: Invoke button definition (.NET)</span></span>

```csharp
var button = new CardAction()
{
    Title = "Option 1",
    Type = "invoke",
    Value = "{\"option\": \"opt1\"}"
};
```

### <a name="example-incoming-invoke-message"></a><span data-ttu-id="9be65-157">示例：传入的 invoke 消息</span><span class="sxs-lookup"><span data-stu-id="9be65-157">Example: Incoming invoke message</span></span>

<span data-ttu-id="9be65-158">顶级 `replyToId` 属性包含卡片操作来自的邮件的 ID。</span><span class="sxs-lookup"><span data-stu-id="9be65-158">The top-level `replyToId` property contains the ID of the message that the card action came from.</span></span> <span data-ttu-id="9be65-159">如果要更新邮件，请使用此方法。</span><span class="sxs-lookup"><span data-stu-id="9be65-159">Use it if you want to update the message.</span></span>

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

## <a name="signin"></a><span data-ttu-id="9be65-160">登录</span><span class="sxs-lookup"><span data-stu-id="9be65-160">signin</span></span>

<span data-ttu-id="9be65-161">启动 OAuth 流，使 bot 能够与安全服务连接，如下文更详细地介绍： [bot 中的身份验证流](~/bots/how-to/authentication/auth-flow-bot.md)。</span><span class="sxs-lookup"><span data-stu-id="9be65-161">Initiates an OAuth flow, allowing bots to connect with secure services, as described in more detail here: [Authentication flow in bots](~/bots/how-to/authentication/auth-flow-bot.md).</span></span>

## <a name="adaptive-cards-actions"></a><span data-ttu-id="9be65-162">自适应卡片操作</span><span class="sxs-lookup"><span data-stu-id="9be65-162">Adaptive Cards actions</span></span>

<span data-ttu-id="9be65-163">自适应卡片支持三种操作类型：</span><span class="sxs-lookup"><span data-stu-id="9be65-163">Adaptive Cards support three action types:</span></span>

* [<span data-ttu-id="9be65-164">操作。 OpenUrl</span><span class="sxs-lookup"><span data-stu-id="9be65-164">Action.OpenUrl</span></span>](http://adaptivecards.io/explorer/Action.OpenUrl.html)
* [<span data-ttu-id="9be65-165">Action.Submit</span><span class="sxs-lookup"><span data-stu-id="9be65-165">Action.Submit</span></span>](http://adaptivecards.io/explorer/Action.Submit.html)
* [<span data-ttu-id="9be65-166">操作。 ShowCard</span><span class="sxs-lookup"><span data-stu-id="9be65-166">Action.ShowCard</span></span>](http://adaptivecards.io/explorer/Action.ShowCard.html)

<span data-ttu-id="9be65-167">除了上面提到的操作之外，还可以使用对象中的属性修改自适应卡 `Action.Submit` 有效负载，以支持现有机器人框架操作 `msteams` `data` `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="9be65-167">In addition to the actions mentioned above, you can modify the Adaptive Card `Action.Submit` payload to support existing Bot Framework actions using a `msteams` property in the `data` object of `Action.Submit`.</span></span> <span data-ttu-id="9be65-168">以下各节详细介绍了如何将现有的 Bot 框架操作用于自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="9be65-168">The below sections detail how to use existing Bot Framework actions with Adaptive Cards.</span></span>

### <a name="adaptive-cards-with-messageback-action"></a><span data-ttu-id="9be65-169">具有 messageBack 操作的自适应卡片</span><span class="sxs-lookup"><span data-stu-id="9be65-169">Adaptive Cards with messageBack action</span></span>

<span data-ttu-id="9be65-170">若要包含 `messageBack` 自适应卡片的操作，请在对象中包含以下详细信息 `msteams` 。</span><span class="sxs-lookup"><span data-stu-id="9be65-170">To include a `messageBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="9be65-171">请注意，如果需要，可以在对象中包含其他隐藏属性 `data` 。</span><span class="sxs-lookup"><span data-stu-id="9be65-171">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="9be65-172">属性</span><span class="sxs-lookup"><span data-stu-id="9be65-172">Property</span></span> | <span data-ttu-id="9be65-173">说明</span><span class="sxs-lookup"><span data-stu-id="9be65-173">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="9be65-174">设置为`messageBack`</span><span class="sxs-lookup"><span data-stu-id="9be65-174">Set to `messageBack`</span></span> |
| `displayText` | <span data-ttu-id="9be65-175">可选。</span><span class="sxs-lookup"><span data-stu-id="9be65-175">Optional.</span></span> <span data-ttu-id="9be65-176">在执行操作时，用户在聊天流中回显。</span><span class="sxs-lookup"><span data-stu-id="9be65-176">Echoed by the user into the chat stream when the action is performed.</span></span> <span data-ttu-id="9be65-177">此文本*不*会发送到你的机器人。</span><span class="sxs-lookup"><span data-stu-id="9be65-177">This text is *not* sent to your bot.</span></span> |
| `value` | <span data-ttu-id="9be65-178">在执行操作时发送到你的 bot。</span><span class="sxs-lookup"><span data-stu-id="9be65-178">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="9be65-179">您可以对操作的上下文进行编码，例如唯一标识符或 JSON 对象。</span><span class="sxs-lookup"><span data-stu-id="9be65-179">You can encode context for the action, such as unique identifiers or a JSON object.</span></span> |
| `text` | <span data-ttu-id="9be65-180">在执行操作时发送到你的 bot。</span><span class="sxs-lookup"><span data-stu-id="9be65-180">Sent to your bot when the action is performed.</span></span> <span data-ttu-id="9be65-181">使用此属性可简化 bot 的开发：您的代码可以检查单个顶级属性以调度 bot 逻辑。</span><span class="sxs-lookup"><span data-stu-id="9be65-181">Use this property to simplify bot development: Your code can check a single top-level property to dispatch bot logic.</span></span> |

#### <a name="example"></a><span data-ttu-id="9be65-182">示例</span><span class="sxs-lookup"><span data-stu-id="9be65-182">Example</span></span>

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

### <a name="adaptive-cards-with-imback-action"></a><span data-ttu-id="9be65-183">具有 imBack 操作的自适应卡片</span><span class="sxs-lookup"><span data-stu-id="9be65-183">Adaptive Cards with imBack action</span></span>

<span data-ttu-id="9be65-184">若要包含 `imBack` 自适应卡片的操作，请在对象中包含以下详细信息 `msteams` 。</span><span class="sxs-lookup"><span data-stu-id="9be65-184">To include a `imBack` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="9be65-185">请注意，如果需要，可以在对象中包含其他隐藏属性 `data` 。</span><span class="sxs-lookup"><span data-stu-id="9be65-185">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="9be65-186">属性</span><span class="sxs-lookup"><span data-stu-id="9be65-186">Property</span></span> | <span data-ttu-id="9be65-187">说明</span><span class="sxs-lookup"><span data-stu-id="9be65-187">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="9be65-188">设置为`imBack`</span><span class="sxs-lookup"><span data-stu-id="9be65-188">Set to `imBack`</span></span> |
| `value` | <span data-ttu-id="9be65-189">需要在聊天中回送的字符串</span><span class="sxs-lookup"><span data-stu-id="9be65-189">String that needs to be echoed back in the chat</span></span> |

#### <a name="example"></a><span data-ttu-id="9be65-190">示例</span><span class="sxs-lookup"><span data-stu-id="9be65-190">Example</span></span>

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

### <a name="adaptive-cards-with-signin-action"></a><span data-ttu-id="9be65-191">具有登录操作的自适应卡片</span><span class="sxs-lookup"><span data-stu-id="9be65-191">Adaptive Cards with signin action</span></span>

<span data-ttu-id="9be65-192">若要包含 `signin` 自适应卡片的操作，请在对象中包含以下详细信息 `msteams` 。</span><span class="sxs-lookup"><span data-stu-id="9be65-192">To include a `signin` action with an Adaptive Card include the following details in the `msteams` object.</span></span> <span data-ttu-id="9be65-193">请注意，如果需要，可以在对象中包含其他隐藏属性 `data` 。</span><span class="sxs-lookup"><span data-stu-id="9be65-193">Note that you can include additional hidden properties in the `data` object if needed.</span></span>

| <span data-ttu-id="9be65-194">属性</span><span class="sxs-lookup"><span data-stu-id="9be65-194">Property</span></span> | <span data-ttu-id="9be65-195">说明</span><span class="sxs-lookup"><span data-stu-id="9be65-195">Description</span></span> |
| --- | --- |
| `type` | <span data-ttu-id="9be65-196">设置为`signin`</span><span class="sxs-lookup"><span data-stu-id="9be65-196">Set to `signin`</span></span> |
| `value` | <span data-ttu-id="9be65-197">设置为要重定向到的 URL</span><span class="sxs-lookup"><span data-stu-id="9be65-197">Set to the URL that you want to redirect to</span></span>  |

#### <a name="example"></a><span data-ttu-id="9be65-198">示例</span><span class="sxs-lookup"><span data-stu-id="9be65-198">Example</span></span>

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
