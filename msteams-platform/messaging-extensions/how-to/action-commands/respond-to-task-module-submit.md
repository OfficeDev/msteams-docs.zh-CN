---
title: 响应任务模块提交操作
author: clearab
description: 介绍如何从邮件扩展操作命令响应任务模块提交操作
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 1fb2f2dc51d7de1208a5a913abf2d38cb80c401a
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231643"
---
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="30749-103">响应任务模块提交操作</span><span class="sxs-lookup"><span data-stu-id="30749-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="30749-104">在用户提交任务模块后，Web 服务会收到一条调用消息，该消息包含 `composeExtension/submitAction` 命令 ID 和参数值。</span><span class="sxs-lookup"><span data-stu-id="30749-104">After a user submits the task module, your web service receives a `composeExtension/submitAction` invoke message with the command ID and parameter values.</span></span> <span data-ttu-id="30749-105">你的应用有五秒钟时间响应调用，否则用户会收到一条错误消息"无法访问应用"，并且Teams 客户端将忽略对调用的任何答复。</span><span class="sxs-lookup"><span data-stu-id="30749-105">Your app has five seconds to respond to the invoke, otherwise the user receives an error message *Unable to reach the app*, and any reply to the invoke is ignored by the Teams client.</span></span>

<span data-ttu-id="30749-106">有以下用于响应的选项：</span><span class="sxs-lookup"><span data-stu-id="30749-106">You have the following options for responding:</span></span>

* <span data-ttu-id="30749-107">无响应 - 你可以选择使用提交操作在外部系统中触发进程，并且不会向用户提供任何反馈。</span><span class="sxs-lookup"><span data-stu-id="30749-107">No response - You can choose to use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="30749-108">这对长时间运行的过程很有用，你可以选择以其他方式提供反馈 (例如，使用主动 [消息](~/bots/how-to/conversations/send-proactive-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="30749-108">This can be useful for long-running processes, and you may choose to provide feedback in another manner (for example, with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="30749-109">[另一个](#respond-with-another-task-module) 任务模块 - 作为多步骤交互的一部分，可以使用其他任务模块进行响应。</span><span class="sxs-lookup"><span data-stu-id="30749-109">[Another task module](#respond-with-another-task-module) - You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="30749-110">[卡片](#respond-with-a-card-inserted-into-the-compose-message-area) 响应 - 可以使用用户随后可以与之交互和/或插入邮件的卡片进行响应。</span><span class="sxs-lookup"><span data-stu-id="30749-110">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area) - You can respond with a card that the user can then interact with and/or insert into a message.</span></span>
* <span data-ttu-id="30749-111">[自动程序中的自适应卡片](#bot-response-with-adaptive-card) - 将自适应卡片直接插入对话中。</span><span class="sxs-lookup"><span data-stu-id="30749-111">[Adaptive Card from bot](#bot-response-with-adaptive-card) - Insert an Adaptive Card directly into the conversation.</span></span>
* [<span data-ttu-id="30749-112">请求用户身份验证</span><span class="sxs-lookup"><span data-stu-id="30749-112">Request the user authenticate</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="30749-113">请求用户输入其他配置</span><span class="sxs-lookup"><span data-stu-id="30749-113">Request the user provide additional configuration</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="30749-114">对于身份验证或配置，在用户完成流后，原始调用将重新发送到 Web 服务。</span><span class="sxs-lookup"><span data-stu-id="30749-114">For authentication or configuration, after the user completes the flow the original invoke is re-sent to your web service.</span></span> <span data-ttu-id="30749-115">下表根据消息扩展的调用位置显示哪些类型的 `commandContext` 响应可用：</span><span class="sxs-lookup"><span data-stu-id="30749-115">The following table shows which types of responses are available based on the invoke location `commandContext` of the messaging extension:</span></span> 

|<span data-ttu-id="30749-116">响应类型</span><span class="sxs-lookup"><span data-stu-id="30749-116">Response Type</span></span> | <span data-ttu-id="30749-117">compose</span><span class="sxs-lookup"><span data-stu-id="30749-117">compose</span></span> | <span data-ttu-id="30749-118">命令栏</span><span class="sxs-lookup"><span data-stu-id="30749-118">command bar</span></span> | <span data-ttu-id="30749-119">message</span><span class="sxs-lookup"><span data-stu-id="30749-119">message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="30749-120">卡片响应</span><span class="sxs-lookup"><span data-stu-id="30749-120">Card response</span></span> | <span data-ttu-id="30749-121">x</span><span class="sxs-lookup"><span data-stu-id="30749-121">x</span></span> | <span data-ttu-id="30749-122">x</span><span class="sxs-lookup"><span data-stu-id="30749-122">x</span></span> | <span data-ttu-id="30749-123">x</span><span class="sxs-lookup"><span data-stu-id="30749-123">x</span></span> |
|<span data-ttu-id="30749-124">另一个任务模块</span><span class="sxs-lookup"><span data-stu-id="30749-124">Another task module</span></span> | <span data-ttu-id="30749-125">x</span><span class="sxs-lookup"><span data-stu-id="30749-125">x</span></span> | <span data-ttu-id="30749-126">x</span><span class="sxs-lookup"><span data-stu-id="30749-126">x</span></span> | <span data-ttu-id="30749-127">x</span><span class="sxs-lookup"><span data-stu-id="30749-127">x</span></span> |
|<span data-ttu-id="30749-128">带自适应卡片的机器人</span><span class="sxs-lookup"><span data-stu-id="30749-128">Bot with Adaptive Card</span></span> | <span data-ttu-id="30749-129">x</span><span class="sxs-lookup"><span data-stu-id="30749-129">x</span></span> |  | <span data-ttu-id="30749-130">x</span><span class="sxs-lookup"><span data-stu-id="30749-130">x</span></span> |
| <span data-ttu-id="30749-131">无响应</span><span class="sxs-lookup"><span data-stu-id="30749-131">No response</span></span> | <span data-ttu-id="30749-132">x</span><span class="sxs-lookup"><span data-stu-id="30749-132">x</span></span> | <span data-ttu-id="30749-133">x</span><span class="sxs-lookup"><span data-stu-id="30749-133">x</span></span> | <span data-ttu-id="30749-134">x</span><span class="sxs-lookup"><span data-stu-id="30749-134">x</span></span> |

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="30749-135">submitAction 调用事件</span><span class="sxs-lookup"><span data-stu-id="30749-135">The submitAction invoke event</span></span>

<span data-ttu-id="30749-136">接收调用消息的示例如下所示：</span><span class="sxs-lookup"><span data-stu-id="30749-136">Examples of receiving the invoke message are as follows:</span></span>

# <a name="cnet"></a>[<span data-ttu-id="30749-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="30749-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="30749-138">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="30749-138">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="30749-139">JSON</span><span class="sxs-lookup"><span data-stu-id="30749-139">JSON</span></span>](#tab/json)

<span data-ttu-id="30749-140">这是您收到的 JSON 对象的示例。</span><span class="sxs-lookup"><span data-stu-id="30749-140">This is an example of the JSON object you receive.</span></span> <span data-ttu-id="30749-141">`commandContext`此参数指示从何处触发邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="30749-141">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="30749-142">`data`该对象包含表单上的字段作为参数以及用户提交的值。</span><span class="sxs-lookup"><span data-stu-id="30749-142">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="30749-143">此处的 JSON 对象已缩短，以突出显示最相关的字段。</span><span class="sxs-lookup"><span data-stu-id="30749-143">The JSON object here is shortened to highlight the most relevant fields.</span></span>

```json
{
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith",
  "serviceUrl": "https://smba.trafficmanager.net/amer/",
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "id": "submitButton",
      "formField1": "formField1_value",
      "formField2": "formField2_value",
      "formField3": "formField3_value"
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  }
}
```

* * *

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="30749-144">使用插入撰写邮件区域中的卡片进行响应</span><span class="sxs-lookup"><span data-stu-id="30749-144">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="30749-145">响应请求的最常见方法 `composeExtension/submitAction` 为插入撰写邮件区域中的卡片。</span><span class="sxs-lookup"><span data-stu-id="30749-145">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="30749-146">然后，用户可以选择将卡片提交到对话。</span><span class="sxs-lookup"><span data-stu-id="30749-146">The user can then choose to submit the card to the conversation.</span></span> <span data-ttu-id="30749-147">有关使用卡片的信息，请参阅 [卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="30749-147">For more information on using cards see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="30749-148">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="30749-148">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
    var response = new MessagingExtensionActionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            AttachmentLayout = "list",
            Type = "result",
        },
    };
    var createCardData = ((JObject)action.Data).ToObject<CreateCardData>();
var card = new HeroCard
{
     Title = createCardData.Title,
     Subtitle = createCardData.Subtitle,
     Text = createCardData.Text,
};
    var attachments = new List<MessagingExtensionAttachment>();
    attachments.Add(new MessagingExtensionAttachment
    {
        Content = card,
        ContentType = HeroCard.ContentType,
        Preview = card.ToAttachment(),
    });
    response.ComposeExtension.Attachments = attachments;
    return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="30749-149">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="30749-149">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
    const data = action.data;
    const heroCard = CardFactory.heroCard(data.title, data.text);
    heroCard.content.subtitle = data.subTitle;
    const attachment = { contentType: heroCard.contentType, content: heroCard.content, preview: heroCard };

    return {
      composeExtension: {
        type: 'result',
        attachmentLayout: 'list',
        attachments: [
          attachment
        ]
      }
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="30749-150">JSON</span><span class="sxs-lookup"><span data-stu-id="30749-150">JSON</span></span>](#tab/json)

```json
{
  "composeExtension": {
    "attachmentLayout": "list",
    "type": "result",
    "attachments": [
      {
        "preview": {
          "contentType": "application/vnd.microsoft.card.hero",
          "content": {
            "title": "formField1_value",
            "subtitle": "formField2_value",
            "text": "formField3_value"
          }
        },
        "contentType": "application/vnd.microsoft.card.hero",
        "content": {
          "title": "formField1_value",
          "subtitle": "formField2_value",
          "text": "formField3_value"
        }
      }
    ]
  }
}
```

* * *

## <a name="respond-with-another-task-module"></a><span data-ttu-id="30749-151">使用另一个任务模块进行响应</span><span class="sxs-lookup"><span data-stu-id="30749-151">Respond with another task module</span></span>

<span data-ttu-id="30749-152">可以选择使用其他任务 `submitAction` 模块响应事件。</span><span class="sxs-lookup"><span data-stu-id="30749-152">You can choose to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="30749-153">在：</span><span class="sxs-lookup"><span data-stu-id="30749-153">This can be useful when:</span></span>

* <span data-ttu-id="30749-154">您需要收集大量信息。</span><span class="sxs-lookup"><span data-stu-id="30749-154">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="30749-155">如果需要根据用户输入动态更改所收集的信息</span><span class="sxs-lookup"><span data-stu-id="30749-155">If you need to dynamically change what information you are collecting based on user input</span></span>
* <span data-ttu-id="30749-156">如果需要验证用户提交的信息，如果出现错误，可能会重新发送包含错误消息的表单。</span><span class="sxs-lookup"><span data-stu-id="30749-156">If you need to validate the information submitted by the user and potentially resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="30749-157">响应方法与响应初始事件 [ `fetchTask` 的方法相同](~/messaging-extensions/how-to/action-commands/create-task-module.md)。</span><span class="sxs-lookup"><span data-stu-id="30749-157">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="30749-158">如果你使用的是 Bot Framework SDK，则这两个提交操作具有相同的事件触发器。</span><span class="sxs-lookup"><span data-stu-id="30749-158">If you are using the Bot Framework SDK the same event triggers for both submit actions.</span></span> <span data-ttu-id="30749-159">这意味着您必须添加确定正确响应的逻辑。</span><span class="sxs-lookup"><span data-stu-id="30749-159">This means you must add logic which determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="30749-160">带自适应卡片的自动程序响应</span><span class="sxs-lookup"><span data-stu-id="30749-160">Bot response with Adaptive Card</span></span>

>[!Note]
><span data-ttu-id="30749-161">此流要求将对象添加到应用清单，并且你必须为自动程序 `bot` 定义必要的作用域。</span><span class="sxs-lookup"><span data-stu-id="30749-161">This flow requires that you add the `bot` object to your app manifest, and that you have the necessary scope defined for the bot.</span></span> <span data-ttu-id="30749-162">使用与自动程序的邮件扩展相同的 ID。</span><span class="sxs-lookup"><span data-stu-id="30749-162">Use the same ID as your messaging extension for your bot.</span></span>

<span data-ttu-id="30749-163">您还可以使用自动程序将带自适应卡片的邮件插入频道，以响应提交操作。</span><span class="sxs-lookup"><span data-stu-id="30749-163">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="30749-164">你的用户可以在提交邮件之前预览邮件，并可能编辑邮件或与之交互。</span><span class="sxs-lookup"><span data-stu-id="30749-164">Your user can preview the message before submitting it, and potentially edit or interact with it as well.</span></span> <span data-ttu-id="30749-165">当你在创建自适应卡片响应之前从用户收集信息，或者当你在某人与之交互后更新卡片时，这会非常有用。</span><span class="sxs-lookup"><span data-stu-id="30749-165">This can be very useful in scenarios where you gather information from your users before creating an adaptive card response, or when you update the card after someone interacts with it.</span></span> <span data-ttu-id="30749-166">以下方案显示应用 Polly 如何使用此流配置轮询，而不在频道对话中包括配置步骤：</span><span class="sxs-lookup"><span data-stu-id="30749-166">The following scenario shows how the app Polly uses this flow to configure a poll without including the configuration steps in the channel conversation:</span></span>

1. <span data-ttu-id="30749-167">用户选择消息扩展以触发任务模块。</span><span class="sxs-lookup"><span data-stu-id="30749-167">The user selects the messaging extension to trigger the task module.</span></span>
2. <span data-ttu-id="30749-168">用户使用任务模块配置轮询。</span><span class="sxs-lookup"><span data-stu-id="30749-168">The user configures the poll with the task module.</span></span>
3. <span data-ttu-id="30749-169">提交任务模块后，应用使用提供的信息将轮询生成为自适应卡片，并将其作为 `botMessagePreview` 响应发送给客户端。</span><span class="sxs-lookup"><span data-stu-id="30749-169">After submitting the task module the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
4. <span data-ttu-id="30749-170">然后，用户可以预览自适应卡片消息，然后自动程序将其插入通道。</span><span class="sxs-lookup"><span data-stu-id="30749-170">The user can then preview the adaptive card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="30749-171">如果应用尚未是频道的成员，则选择添加 `Send` 它。</span><span class="sxs-lookup"><span data-stu-id="30749-171">If the app is not already a member of the channel, selecting `Send` adds it.</span></span>
   1. <span data-ttu-id="30749-172">用户还可以选择邮件 `Edit` ，以将其返回到原始任务模块。</span><span class="sxs-lookup"><span data-stu-id="30749-172">The user can also choose to `Edit` the message, which returns them to the original task module.</span></span>
5. <span data-ttu-id="30749-173">与自适应卡片交互在发送邮件之前会更改邮件。</span><span class="sxs-lookup"><span data-stu-id="30749-173">Interacting with the adaptive card changes the message before sending it.</span></span>
6. <span data-ttu-id="30749-174">用户选择自动 `Send` 程序后，将消息发送到频道。</span><span class="sxs-lookup"><span data-stu-id="30749-174">After the user selects `Send` the bot posts the message to the channel.</span></span>

### <a name="respond-to-initial-submit-action"></a><span data-ttu-id="30749-175">响应初始提交操作</span><span class="sxs-lookup"><span data-stu-id="30749-175">Respond to initial submit action</span></span>

<span data-ttu-id="30749-176">若要启用此流，任务模块应响应初始消息，并预览机器人 `composeExtension/submitAction` 发送到频道的卡片。</span><span class="sxs-lookup"><span data-stu-id="30749-176">To enable this flow your task module should respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot send to the channel.</span></span> <span data-ttu-id="30749-177">这样，用户有机会在发送之前验证该卡，并尝试在对话中安装聊天机器人（如果尚未安装）。</span><span class="sxs-lookup"><span data-stu-id="30749-177">This gives the user the opportunity to verify the card before sending, and also attempt to install your bot in the conversation if it is not already installed.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="30749-178">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="30749-178">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  dynamic createCardData = ((JObject) action.Data).ToObject(typeof(JObject));
  var response = new MessagingExtensionActionResponse
  {
    ComposeExtension = new MessagingExtensionResult
    {
      Type = "botMessagePreview",
      ActivityPreview = MessageFactory.Attachment(new Attachment
      {
        Content = new AdaptiveCard("1.0")
        {
          Body = new List<AdaptiveElement>()
          {
            new AdaptiveTextBlock() { Text = "FormField1 value was:", Size = AdaptiveTextSize.Large },
            new AdaptiveTextBlock() { Text = Data["FormField1"] as string }
          },
          Height = AdaptiveHeight.Auto,
          Actions = new List<AdaptiveAction>()
          {
            new AdaptiveSubmitAction
            {
              Type = AdaptiveSubmitAction.TypeName,
              Title = "Submit",
              Data = new JObject { { "submitLocation", "messagingExtensionFetchTask" } },
            },
          }
        },
        ContentType = AdaptiveCard.ContentType
      }) as Activity
    }
  };

  return response;
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="30749-179">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="30749-179">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
    const submittedData = action.data;
    const adaptiveCard = CardFactory.adaptiveCard({
      actions: [
        { type: 'Action.Submit', title: 'Submit', data: { submitLocation: 'messagingExtensionSubmit' } }
      ],
      body: [
          { text: 'Adaptive Card from Task Module', type: 'TextBlock', weight: 'bolder' },
          { text: `${ submittedData.Question }`, type: 'TextBlock', id: 'Question' },
          { id: 'Answer', placeholder: 'Answer here...', type: 'Input.Text' },
        {
          choices: [
            { title: submittedData.Option1, value: submittedData.Option1 },
            { title: submittedData.Option2, value: submittedData.Option2 },
            { title: submittedData.Option3, value: submittedData.Option3 }
          ],
          id: 'Choices',
          isMultiSelect: submittedData.MultiSelect,
          style: 'expanded',
          type: 'Input.ChoiceSet'
        }
      ],
      type: 'AdaptiveCard',
      version: '1.0'
    });
    return {
      composeExtension: {
        activityPreview: MessageFactory.attachment(adaptiveCard, null, null, InputHints.ExpectingInput),
        type: 'botMessagePreview'
      }
    };
  }
}
```

# <a name="json"></a>[<span data-ttu-id="30749-180">JSON</span><span class="sxs-lookup"><span data-stu-id="30749-180">JSON</span></span>](#tab/json)

>[!Note]
><span data-ttu-id="30749-181">必须 `activityPreview` 包含正好包含 `message` 1 个自适应卡片附件的活动。</span><span class="sxs-lookup"><span data-stu-id="30749-181">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span> <span data-ttu-id="30749-182">该值 `<< Card Payload >>` 是想要发送的卡片的占位符。</span><span class="sxs-lookup"><span data-stu-id="30749-182">The `<< Card Payload >>` value is a placeholder for the card you wish to send.</span></span>

```json
{
  "composeExtension": {
    "type": "botMessagePreview",
    "activityPreview": {
      "type": "message",
      "attachments":  [
        {
          "contentType": "application/vnd.microsoft.card.adaptive",
          "content": << Card Payload >>
        }
      ]
    }
  }
}
```

* * *

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="30749-183">botMessagePreview 发送和编辑事件</span><span class="sxs-lookup"><span data-stu-id="30749-183">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="30749-184">您的邮件扩展现在必须响应调用的两个新 `composeExtension/submitAction` 种类，其中 `value.botMessagePreviewAction = "send"` 和 `value.botMessagePreviewAction = "edit"` 。</span><span class="sxs-lookup"><span data-stu-id="30749-184">Your message extension must respond now to two new varieties of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="30749-185">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="30749-185">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewEditAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle the event
}

protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewSendAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle the event
}

```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="30749-186">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="30749-186">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionBotMessagePreviewEdit(context, action) {

    //handle the event
  }
  
  handleTeamsMessagingExtensionBotMessagePreviewSend(context, action) {

    //handle the event
  }
}

```

# <a name="json"></a>[<span data-ttu-id="30749-187">JSON</span><span class="sxs-lookup"><span data-stu-id="30749-187">JSON</span></span>](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "edit | send",
    "botActivityPreview": [
      {
        "type": "message/card",
        "attachments": [
          {
            "content":
              {
                "type": "AdaptiveCard",
                "body": [{<<card payload>>}]
              },
            "contentType" : "application/vnd.microsoft.card.adaptive"
          }
        ],
        "context": { "theme": "default" }
      }
    ],
  }
}
```

* * *

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="30749-188">响应 botMessagePreview 编辑</span><span class="sxs-lookup"><span data-stu-id="30749-188">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="30749-189">如果用户通过选择"编辑"按钮在发送之前编辑卡片，则会收到 `composeExtension/submitAction` 一个调用 `value.botMessagePreviewAction = edit` 。</span><span class="sxs-lookup"><span data-stu-id="30749-189">If the user edits the card before sending by selecting the **Edit** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="30749-190">通常，应返回为响应启动交互的初始调用而发送的任务模块 `composeExtension/fetchTask` 进行响应。</span><span class="sxs-lookup"><span data-stu-id="30749-190">You should typically respond by returning the task module you sent in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="30749-191">这允许用户通过重新输入原始信息来重新开始此过程。</span><span class="sxs-lookup"><span data-stu-id="30749-191">This allows the user to start the process over by re-entering the original information.</span></span> <span data-ttu-id="30749-192">使用可用信息预填充任务模块，以便用户无需从头开始填写所有信息。</span><span class="sxs-lookup"><span data-stu-id="30749-192">Use the available information to pre-populate the task module so the user does not have to fill out all of the information from scratch.</span></span>

<span data-ttu-id="30749-193">请参阅 [响应初始 `fetchTask` 事件](~/messaging-extensions/how-to/action-commands/create-task-module.md)。</span><span class="sxs-lookup"><span data-stu-id="30749-193">See [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="30749-194">响应 botMessagePreview 发送</span><span class="sxs-lookup"><span data-stu-id="30749-194">Respond to botMessagePreview send</span></span>

<span data-ttu-id="30749-195">在用户选择"发送" **按钮后** ，您将收到 `composeExtension/submitAction` 一个调用 `value.botMessagePreviewAction = send` 。</span><span class="sxs-lookup"><span data-stu-id="30749-195">After the user selects the **Send** button, you receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="30749-196">Web 服务必须创建具有自适应卡片的主动消息并将其发送到对话，并回复调用。</span><span class="sxs-lookup"><span data-stu-id="30749-196">Your web service has to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="30749-197">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="30749-197">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionBotMessagePreviewSendAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var activityPreview = action.BotActivityPreview[0];
  var attachmentContent = activityPreview.Attachments[0].Content;
  var previewedCard = JsonConvert.DeserializeObject<AdaptiveCard>(attachmentContent.ToString(),
          new JsonSerializerSettings { NullValueHandling = NullValueHandling.Ignore });
  
  previewedCard.Version = "1.0";

  var responseActivity = Activity.CreateMessageActivity();
  Attachment attachment = new Attachment()
  {
    ContentType = AdaptiveCard.ContentType,
    Content = previewedCard
  };
  responseActivity.Attachments.Add(attachment);
  
  // Attribute the message to the user on whose behalf the bot is posting
  responseActivity.ChannelData = new {
    OnBehalfOf = new []
    {
      new
      {
        ItemId = 0,
        MentionType = "person",
        Mri = turnContext.Activity.From.Id,
        DisplayName = turnContext.Activity.From.Name
      }  
    }
  };
  
  await turnContext.SendActivityAsync(responseActivity);

  return new MessagingExtensionActionResponse();
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="30749-198">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="30749-198">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    async handleTeamsMessagingExtensionBotMessagePreviewSend(context, action) {
      // The data has been returned to the bot in the action structure.
      const activityPreview = action.botActivityPreview[0];
      const attachmentContent = activityPreview.attachments[0].content;
      const userText = attachmentContent.body[1].text;
      const choiceSet = attachmentContent.body[3];

      const submitData = {
        MultiSelect: choiceSet.isMultiSelect ? 'true' : 'false',
        Option1: choiceSet.choices[0].title,
        Option2: choiceSet.choices[1].title,
        Option3: choiceSet.choices[2].title,
        Question: userText
      };

      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [
          { type: 'Action.Submit', title: 'Submit', data: { submitLocation: 'messagingExtensionSubmit' } }
        ],
        body: [
          { text: 'Adaptive Card from Task Module', type: 'TextBlock', weight: 'bolder' },
          { text: `${ submitData.Question }`, type: 'TextBlock', id: 'Question' },
          { id: 'Answer', placeholder: 'Answer here...', type: 'Input.Text' },
          {
            choices: [
                { title: submitData.Option1, value: submitData.Option1 },
                { title: submitData.Option2, value: submitData.Option2 },
                { title: submitData.Option3, value: submitData.Option3 }
            ],
            id: 'Choices',
            isMultiSelect: submitData.MultiSelect,
            style: 'expanded',
            type: 'Input.ChoiceSet'
          }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });
      const responseActivity = { type: 'message', attachments: [adaptiveCard], channelData: {
          onBehalfOf: [
              { itemId: 0, mentionType: 'person', mri: context.activity.from.id, displayname: context.activity.from.name }
          ]
      }};

      await context.sendActivity(responseActivity);
    }
}
```

# <a name="json"></a>[<span data-ttu-id="30749-199">JSON</span><span class="sxs-lookup"><span data-stu-id="30749-199">JSON</span></span>](#tab/json)

<span data-ttu-id="30749-200">您将收到一 `composeExtension/submitAction` 条类似于以下内容的新邮件：</span><span class="sxs-lookup"><span data-stu-id="30749-200">You receive a new `composeExtension/submitAction` message similar to the following:</span></span>

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send",
    "botActivityPreview": [
      {
        "type": "message/card",
        "attachments": [
          {
            "content":
              {
                "type": "AdaptiveCard",
                "body": [{<<card payload>>}]
              },
            "contentType" : "application/vnd.microsoft.card.adaptive"
          }
        ],
        "context": { "theme": "default" }
      }
    ],
  }
}
```

* * *

### <a name="user-attribution-for-bots-messages"></a><span data-ttu-id="30749-201">自动程序消息的用户属性</span><span class="sxs-lookup"><span data-stu-id="30749-201">User attribution for bots messages</span></span> 

<span data-ttu-id="30749-202">在机器人代表用户发送邮件的情况下，将消息归为该用户有助于参与，并展示更自然的交互流。</span><span class="sxs-lookup"><span data-stu-id="30749-202">In scenarios where a bot sends messages on behalf of a user, attributing the message to that user can help with engagement and showcase a more natural interaction flow.</span></span> <span data-ttu-id="30749-203">此功能允许你将来自自动程序的邮件属性属性给代表其发送的用户。</span><span class="sxs-lookup"><span data-stu-id="30749-203">This feature allows you to attribute a message from your bot to a user on whose behalf it was sent.</span></span>

<span data-ttu-id="30749-204">在下图中，左侧是自动程序发送的无用户属性的卡片消息，右侧是自动程序发送的具有用户 *属性的卡片*。</span><span class="sxs-lookup"><span data-stu-id="30749-204">In the following image, on the left is a card message sent by a bot *without* user attribution and on the right is a card sent by a bot *with* user attribution.</span></span>

![屏幕截图](../../../assets/images/messaging-extension/user-attribution-bots.png)

<span data-ttu-id="30749-206">若要在团队中使用用户属性，必须将提及实体添加到发送到 Teams 的有效负载 `OnBehalfOf` `ChannelData` `Activity` 中。</span><span class="sxs-lookup"><span data-stu-id="30749-206">To use the user attribution in teams, you must  add the `OnBehalfOf` mention entity to `ChannelData` in your `Activity` payload that is sent to Teams.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="30749-207">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="30749-207">C#/.NET</span></span>](#tab/dotnet-1)

```csharp
    OnBehalfOf = new []
    {
      new
      {
        ItemId = 0,
        MentionType = "person",
        Mri = turnContext.Activity.From.Id,
        DisplayName = turnContext.Activity.From.Name
      }  
    }

```

# <a name="json"></a>[<span data-ttu-id="30749-208">JSON</span><span class="sxs-lookup"><span data-stu-id="30749-208">JSON</span></span>](#tab/json-1)

```json
{
    "text": "Hello World!",
    "ChannelData": {
        "OnBehalfOf": [{
            "itemid": 0,
            "mentionType": "person",
            "mri": "29:orgid:89e6508d-6c0f-4ffe-9f6a-b58416d965ae",
            "displayName": "Sowrabh N R S"
        }]
    }
}
```

* * *

<span data-ttu-id="30749-209">以下部分介绍了 Array 中的 `OnBehalfOf` 实体：</span><span class="sxs-lookup"><span data-stu-id="30749-209">The following section is a description of the entities in the `OnBehalfOf` of Array:</span></span>

#### <a name="details-of--onbehalfof-entity-schema"></a><span data-ttu-id="30749-210">实体  `OnBehalfOf` 架构的详细信息</span><span class="sxs-lookup"><span data-stu-id="30749-210">Details of  `OnBehalfOf` entity schema</span></span>

|<span data-ttu-id="30749-211">字段</span><span class="sxs-lookup"><span data-stu-id="30749-211">Field</span></span>|<span data-ttu-id="30749-212">类型</span><span class="sxs-lookup"><span data-stu-id="30749-212">Type</span></span>|<span data-ttu-id="30749-213">说明</span><span class="sxs-lookup"><span data-stu-id="30749-213">Description</span></span>|
|:---|:---|:---|
|`itemId`|<span data-ttu-id="30749-214">整数</span><span class="sxs-lookup"><span data-stu-id="30749-214">Integer</span></span>|<span data-ttu-id="30749-215">应为 0</span><span class="sxs-lookup"><span data-stu-id="30749-215">Should be 0</span></span>|
|`mentionType`|<span data-ttu-id="30749-216">String</span><span class="sxs-lookup"><span data-stu-id="30749-216">String</span></span>|<span data-ttu-id="30749-217">应为"person"</span><span class="sxs-lookup"><span data-stu-id="30749-217">Should be "person"</span></span>|
|`mri`|<span data-ttu-id="30749-218">String</span><span class="sxs-lookup"><span data-stu-id="30749-218">String</span></span>|<span data-ttu-id="30749-219">邮件资源标识符 (邮件) 邮件发送者的邮件的 MRI 标识符。</span><span class="sxs-lookup"><span data-stu-id="30749-219">Message resource identifier (MRI) of the person on whose behalf the message is sent.</span></span> <span data-ttu-id="30749-220">邮件发件人名称将显示为" \<user\> 通过 \<bot name\> "。</span><span class="sxs-lookup"><span data-stu-id="30749-220">Message sender name would appear as "\<user\> via \<bot name\>".</span></span>|
|`displayName`|<span data-ttu-id="30749-221">String</span><span class="sxs-lookup"><span data-stu-id="30749-221">String</span></span>|<span data-ttu-id="30749-222">人员的名称。</span><span class="sxs-lookup"><span data-stu-id="30749-222">Name of the person.</span></span> <span data-ttu-id="30749-223">在名称解析不可用时用作回退。</span><span class="sxs-lookup"><span data-stu-id="30749-223">Used as fallback in case name resolution is unavailable.</span></span>|
  
## <a name="next-steps"></a><span data-ttu-id="30749-224">后续步骤</span><span class="sxs-lookup"><span data-stu-id="30749-224">Next Steps</span></span>

<span data-ttu-id="30749-225">添加搜索命令</span><span class="sxs-lookup"><span data-stu-id="30749-225">Add a search command</span></span>

* [<span data-ttu-id="30749-226">定义搜索命令</span><span class="sxs-lookup"><span data-stu-id="30749-226">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
