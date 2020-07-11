---
title: 响应任务模块提交操作
author: clearab
description: 介绍如何从邮件扩展操作命令响应任务模块提交操作
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: a876275f5f4f9c3a7c1fea275eecb9c26b780fd0
ms.sourcegitcommit: 3ba5a5a7d9d9d906abc3ee1df9c2177de0cfd767
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/11/2020
ms.locfileid: "45103011"
---
# <a name="respond-to-the-task-module-submit-action"></a><span data-ttu-id="7f62d-103">响应任务模块提交操作</span><span class="sxs-lookup"><span data-stu-id="7f62d-103">Respond to the task module submit action</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="7f62d-104">用户提交任务模块后，web 服务将收到 `composeExtension/submitAction` 设置了命令 id 和参数值的 invoke 消息。</span><span class="sxs-lookup"><span data-stu-id="7f62d-104">Once a user submits the task module, your web service will receive a `composeExtension/submitAction` invoke message with the command id and parameter values set.</span></span> <span data-ttu-id="7f62d-105">您的应用程序将有5秒的时间来响应调用，否则，用户将收到 "无法访问应用" 错误消息，并且团队客户端将忽略对该调用的任何答复。</span><span class="sxs-lookup"><span data-stu-id="7f62d-105">Your app will have five seconds to respond to the invoke, otherwise the user will receive an "Unable to reach the app" error message, and any reply to the invoke will be ignored by the Teams client.</span></span>

<span data-ttu-id="7f62d-106">您有以下选项可供您进行响应。</span><span class="sxs-lookup"><span data-stu-id="7f62d-106">You have the following options for responding.</span></span>

* <span data-ttu-id="7f62d-107">无响应-你可以选择使用 "提交" 操作在外部系统中触发进程，而不向用户提供任何反馈。</span><span class="sxs-lookup"><span data-stu-id="7f62d-107">No response - You can choose to use the submit action to trigger a process in an external system, and not provide any feedback to the user.</span></span> <span data-ttu-id="7f62d-108">这对于长时间运行的进程很有用，您可以选择以其他方式提供反馈 (例如，使用[主动消息](~/bots/how-to/conversations/send-proactive-messages.md)。</span><span class="sxs-lookup"><span data-stu-id="7f62d-108">This can be useful for long-running processes, and you may choose to provide feedback in another manner (for example, with a [proactive message](~/bots/how-to/conversations/send-proactive-messages.md).</span></span>
* <span data-ttu-id="7f62d-109">[另一个任务模块](#respond-with-another-task-module)-您可以作为多步骤交互的一部分，使用其他任务模块进行响应。</span><span class="sxs-lookup"><span data-stu-id="7f62d-109">[Another task module](#respond-with-another-task-module) - You can respond with an additional task module as part of a multi-step interaction.</span></span>
* <span data-ttu-id="7f62d-110">[卡片响应](#respond-with-a-card-inserted-into-the-compose-message-area)-你可以使用用户可与之交互和/或插入邮件的卡片进行响应。</span><span class="sxs-lookup"><span data-stu-id="7f62d-110">[Card response](#respond-with-a-card-inserted-into-the-compose-message-area) - You can respond with a card that the user can then interact with and/or insert into a message.</span></span>
* <span data-ttu-id="7f62d-111">[来自 bot 的自适应卡片](#bot-response-with-adaptive-card)-将自适应卡片直接插入对话中。</span><span class="sxs-lookup"><span data-stu-id="7f62d-111">[Adaptive Card from bot](#bot-response-with-adaptive-card) - Insert an Adaptive Card directly into the conversation.</span></span>
* [<span data-ttu-id="7f62d-112">请求用户进行身份验证</span><span class="sxs-lookup"><span data-stu-id="7f62d-112">Request the user authenticate</span></span>](~/messaging-extensions/how-to/add-authentication.md)
* [<span data-ttu-id="7f62d-113">请求用户提供其他配置</span><span class="sxs-lookup"><span data-stu-id="7f62d-113">Request the user provide additional configuration</span></span>](~/messaging-extensions/how-to/add-configuration-page.md)

<span data-ttu-id="7f62d-114">下表显示了哪些类型的响应可基于邮件扩展的调用位置 (`commandContext`) 。</span><span class="sxs-lookup"><span data-stu-id="7f62d-114">The table below shows which types of responses are available based on the invoke location (`commandContext`) of the messaging extension.</span></span> <span data-ttu-id="7f62d-115">对于身份验证或配置，一旦用户完成了流，原始调用将重新发送到您的 web 服务。</span><span class="sxs-lookup"><span data-stu-id="7f62d-115">For authentication or configuration, once the user completes the flow the original invoke will be re-sent to your web service.</span></span>

|<span data-ttu-id="7f62d-116">响应类型</span><span class="sxs-lookup"><span data-stu-id="7f62d-116">Response Type</span></span> | <span data-ttu-id="7f62d-117">编撰</span><span class="sxs-lookup"><span data-stu-id="7f62d-117">compose</span></span> | <span data-ttu-id="7f62d-118">命令栏</span><span class="sxs-lookup"><span data-stu-id="7f62d-118">command bar</span></span> | <span data-ttu-id="7f62d-119">message</span><span class="sxs-lookup"><span data-stu-id="7f62d-119">message</span></span> |
|--------------|:-------------:|:-------------:|:---------:|
|<span data-ttu-id="7f62d-120">卡片响应</span><span class="sxs-lookup"><span data-stu-id="7f62d-120">Card response</span></span> | <span data-ttu-id="7f62d-121">x</span><span class="sxs-lookup"><span data-stu-id="7f62d-121">x</span></span> | <span data-ttu-id="7f62d-122">x</span><span class="sxs-lookup"><span data-stu-id="7f62d-122">x</span></span> | <span data-ttu-id="7f62d-123">x</span><span class="sxs-lookup"><span data-stu-id="7f62d-123">x</span></span> |
|<span data-ttu-id="7f62d-124">另一个任务模块</span><span class="sxs-lookup"><span data-stu-id="7f62d-124">Another task module</span></span> | <span data-ttu-id="7f62d-125">x</span><span class="sxs-lookup"><span data-stu-id="7f62d-125">x</span></span> | <span data-ttu-id="7f62d-126">x</span><span class="sxs-lookup"><span data-stu-id="7f62d-126">x</span></span> | <span data-ttu-id="7f62d-127">x</span><span class="sxs-lookup"><span data-stu-id="7f62d-127">x</span></span> |
|<span data-ttu-id="7f62d-128">带有自适应卡片的 Bot</span><span class="sxs-lookup"><span data-stu-id="7f62d-128">Bot with Adaptive Card</span></span> | <span data-ttu-id="7f62d-129">x</span><span class="sxs-lookup"><span data-stu-id="7f62d-129">x</span></span> |  | <span data-ttu-id="7f62d-130">x</span><span class="sxs-lookup"><span data-stu-id="7f62d-130">x</span></span> |
| <span data-ttu-id="7f62d-131">无响应</span><span class="sxs-lookup"><span data-stu-id="7f62d-131">No response</span></span> | <span data-ttu-id="7f62d-132">x</span><span class="sxs-lookup"><span data-stu-id="7f62d-132">x</span></span> | <span data-ttu-id="7f62d-133">x</span><span class="sxs-lookup"><span data-stu-id="7f62d-133">x</span></span> | <span data-ttu-id="7f62d-134">x</span><span class="sxs-lookup"><span data-stu-id="7f62d-134">x</span></span> |

## <a name="the-submitaction-invoke-event"></a><span data-ttu-id="7f62d-135">SubmitAction 调用事件</span><span class="sxs-lookup"><span data-stu-id="7f62d-135">The submitAction invoke event</span></span>

<span data-ttu-id="7f62d-136">下面是接收调用消息的示例。</span><span class="sxs-lookup"><span data-stu-id="7f62d-136">Below are examples of receiving the invoke message.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7f62d-137">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7f62d-137">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[<span data-ttu-id="7f62d-138">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7f62d-138">JavaScript/Node.js</span></span>](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[<span data-ttu-id="7f62d-139">JSON</span><span class="sxs-lookup"><span data-stu-id="7f62d-139">JSON</span></span>](#tab/json)

<span data-ttu-id="7f62d-140">这是您将收到的 JSON 对象的一个示例。</span><span class="sxs-lookup"><span data-stu-id="7f62d-140">This is an example of the JSON object you will receive.</span></span> <span data-ttu-id="7f62d-141">`commandContext`参数指示邮件扩展的触发位置。</span><span class="sxs-lookup"><span data-stu-id="7f62d-141">The `commandContext` parameter indicates where your messaging extension was triggered from.</span></span> <span data-ttu-id="7f62d-142">`data`对象将窗体上的字段作为参数，并将用户提交的值包含在窗体中。</span><span class="sxs-lookup"><span data-stu-id="7f62d-142">The `data` object contains the fields on the form as parameters, and the values the user submitted.</span></span> <span data-ttu-id="7f62d-143">此处的 JSON 对象将被缩短，以突出显示最相关的字段。</span><span class="sxs-lookup"><span data-stu-id="7f62d-143">The JSON object here is shortened to highlight the most relevant fields.</span></span>

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a><span data-ttu-id="7f62d-144">使用插入撰写邮件区域中的卡片进行响应</span><span class="sxs-lookup"><span data-stu-id="7f62d-144">Respond with a card inserted into the compose message area</span></span>

<span data-ttu-id="7f62d-145">对请求做出响应的最常见方法 `composeExtension/submitAction` 是将卡片插入撰写邮件区域中。</span><span class="sxs-lookup"><span data-stu-id="7f62d-145">The most common way to respond to the `composeExtension/submitAction` request is with a card inserted into the compose message area.</span></span> <span data-ttu-id="7f62d-146">然后，用户可以选择将该卡提交到对话中。</span><span class="sxs-lookup"><span data-stu-id="7f62d-146">The user can then choose to submit the card to the conversation.</span></span> <span data-ttu-id="7f62d-147">有关使用卡片的详细信息，请参阅[卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="7f62d-147">For more information on using cards see [cards and card actions](~/task-modules-and-cards/cards/cards-actions.md).</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7f62d-148">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7f62d-148">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
    dynamic Data = JObject.Parse(action.Data.ToString());
    var response = new MessagingExtensionActionResponse
    {
        ComposeExtension = new MessagingExtensionResult
        {
            AttachmentLayout = "list",
            Type = "result",
        },
    };
    var card = new HeroCard
    {
        Title = Data["formField1"] as string,
        Subtitle = Data["formField2"]  as string,
        Text = Data["formField3"]  as string,
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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="7f62d-149">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7f62d-149">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="7f62d-150">JSON</span><span class="sxs-lookup"><span data-stu-id="7f62d-150">JSON</span></span>](#tab/json)

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

## <a name="respond-with-another-task-module"></a><span data-ttu-id="7f62d-151">使用另一个任务模块进行响应</span><span class="sxs-lookup"><span data-stu-id="7f62d-151">Respond with another task module</span></span>

<span data-ttu-id="7f62d-152">您可以选择 `submitAction` 使用其他任务模块响应事件。</span><span class="sxs-lookup"><span data-stu-id="7f62d-152">You can choose to respond to the `submitAction` event with an additional task module.</span></span> <span data-ttu-id="7f62d-153">这在以下情况中非常有用：</span><span class="sxs-lookup"><span data-stu-id="7f62d-153">This can be useful when:</span></span>

* <span data-ttu-id="7f62d-154">您需要收集大量信息。</span><span class="sxs-lookup"><span data-stu-id="7f62d-154">You need to collect large amounts of information.</span></span>
* <span data-ttu-id="7f62d-155">如果您需要根据用户输入动态更改要收集的信息</span><span class="sxs-lookup"><span data-stu-id="7f62d-155">If you need to dynamically change what information you're collecting based on user input</span></span>
* <span data-ttu-id="7f62d-156">如果需要验证用户提交的信息，并且可能会在出现错误时使用错误消息重新发送该表单。</span><span class="sxs-lookup"><span data-stu-id="7f62d-156">If you need to validate the information submitted by the user and potentially resend the form with an error message if something is wrong.</span></span> 

<span data-ttu-id="7f62d-157">响应方法与[响应初始 `fetchTask` 事件](~/messaging-extensions/how-to/action-commands/create-task-module.md)相同。</span><span class="sxs-lookup"><span data-stu-id="7f62d-157">The method for response is the same as [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span> <span data-ttu-id="7f62d-158">如果您使用的是 Bot 框架 SDK，则相同的事件将触发这两个提交操作。</span><span class="sxs-lookup"><span data-stu-id="7f62d-158">If you're using the Bot Framework SDK the same event will trigger for both submit actions.</span></span> <span data-ttu-id="7f62d-159">这意味着您需要确保添加确定正确响应的逻辑。</span><span class="sxs-lookup"><span data-stu-id="7f62d-159">This mean you need to be sure to add logic which determines the correct response.</span></span>

## <a name="bot-response-with-adaptive-card"></a><span data-ttu-id="7f62d-160">使用自适应卡片的 Bot 响应</span><span class="sxs-lookup"><span data-stu-id="7f62d-160">Bot response with Adaptive Card</span></span>

>[!Note]
><span data-ttu-id="7f62d-161">此流要求您将对象添加 `bot` 到应用程序清单，并且您具有为 bot 定义的必要作用域。</span><span class="sxs-lookup"><span data-stu-id="7f62d-161">This flow requires that you add the `bot` object to your app manifest, and that you have the necessary scope defined for the bot.</span></span> <span data-ttu-id="7f62d-162">使用与你的 bot 的邮件扩展相同的 Id。</span><span class="sxs-lookup"><span data-stu-id="7f62d-162">Use the same Id as your messaging extension for your bot.</span></span>

<span data-ttu-id="7f62d-163">您还可以通过将带有自适应卡片的邮件插入到使用 bot 的频道中来响应提交操作。</span><span class="sxs-lookup"><span data-stu-id="7f62d-163">You can also respond to the submit action by inserting a message with an Adaptive Card into the channel with a bot.</span></span> <span data-ttu-id="7f62d-164">你的用户将能够在提交邮件之前预览邮件，并可能对其进行编辑/与之交互。</span><span class="sxs-lookup"><span data-stu-id="7f62d-164">Your user will be able to preview the message before submitting it, and potentially edit/interact with it as well.</span></span> <span data-ttu-id="7f62d-165">当您需要在创建自适应卡片响应之前从用户处收集信息，或者在某人与他人交互后需要更新卡片时，这可能非常有用。</span><span class="sxs-lookup"><span data-stu-id="7f62d-165">This can be very useful in scenarios where you need to gather information from your users before creating an adaptive card response, or when you're going to need to update the card after someone interacts with it.</span></span> <span data-ttu-id="7f62d-166">以下方案显示了应用程序 Polly 如何使用此流配置轮询，而不在通道对话中包括配置步骤。</span><span class="sxs-lookup"><span data-stu-id="7f62d-166">The following scenario shows how the app Polly uses this flow to configure a poll without including the configuration steps in the channel conversation.</span></span>

1. <span data-ttu-id="7f62d-167">用户单击邮件扩展可触发任务模块。</span><span class="sxs-lookup"><span data-stu-id="7f62d-167">The user clicks the messaging extension to trigger the task module.</span></span>
2. <span data-ttu-id="7f62d-168">用户使用任务模块配置投票。</span><span class="sxs-lookup"><span data-stu-id="7f62d-168">The user configures the poll with the task module.</span></span>
3. <span data-ttu-id="7f62d-169">提交任务模块后，应用使用提供的信息将轮询构建为自适应卡片，并将其作为响应发送 `botMessagePreview` 给客户端。</span><span class="sxs-lookup"><span data-stu-id="7f62d-169">After submitting the task module the app uses the information provided to build the poll as an Adaptive Card and sends it as a `botMessagePreview` response to the client.</span></span>
4. <span data-ttu-id="7f62d-170">然后，用户可以预览自适应卡片邮件，然后将其插入频道。</span><span class="sxs-lookup"><span data-stu-id="7f62d-170">The user can then preview the adaptive card message before the bot inserts it into the channel.</span></span> <span data-ttu-id="7f62d-171">如果应用尚未成为频道的成员，则单击 `Send` "" 将添加它。</span><span class="sxs-lookup"><span data-stu-id="7f62d-171">If the app is not already a member of the channel, clicking `Send` will add the it.</span></span>
   1. <span data-ttu-id="7f62d-172">用户还可以选择将 `Edit` 其返回到原始任务模块的邮件。</span><span class="sxs-lookup"><span data-stu-id="7f62d-172">The user can also chose to `Edit` the message, which returns them to the original task module.</span></span>
5. <span data-ttu-id="7f62d-173">与自适应卡片进行交互会在发送邮件之前对其进行更改。</span><span class="sxs-lookup"><span data-stu-id="7f62d-173">Interacting with the adaptive card changes the message before sending it.</span></span>
6. <span data-ttu-id="7f62d-174">用户单击机器人后，会将 `Send` 邮件发送到频道。</span><span class="sxs-lookup"><span data-stu-id="7f62d-174">Once the user clicks `Send` the bot posts the message to the channel.</span></span>

### <a name="respond-to-initial-submit-action"></a><span data-ttu-id="7f62d-175">响应初始提交操作</span><span class="sxs-lookup"><span data-stu-id="7f62d-175">Respond to initial submit action</span></span>

<span data-ttu-id="7f62d-176">若要启用此流，任务模块应 `composeExtension/submitAction` 使用 bot 将发送到频道的卡片的预览对初始邮件做出响应。</span><span class="sxs-lookup"><span data-stu-id="7f62d-176">To enable this flow your task module should respond to the initial `composeExtension/submitAction` message with a preview of the card that the bot will send to the channel.</span></span> <span data-ttu-id="7f62d-177">这使用户可以在发送之前验证卡，还会在对话中尝试安装你的 bot （如果尚未安装）。</span><span class="sxs-lookup"><span data-stu-id="7f62d-177">This gives the user the opportunity to verify the card before sending, and also will attempt to install your bot in the conversation if it is not already installed.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7f62d-178">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7f62d-178">C#/.NET</span></span>](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  dynamic Data = JObject.Parse(action.Data.ToString());
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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="7f62d-179">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7f62d-179">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="7f62d-180">JSON</span><span class="sxs-lookup"><span data-stu-id="7f62d-180">JSON</span></span>](#tab/json)

>[!Note]
><span data-ttu-id="7f62d-181">`activityPreview`必须包含一个 `message` 只有1个自适应卡片附件的活动。</span><span class="sxs-lookup"><span data-stu-id="7f62d-181">The `activityPreview` must contain a `message` activity with exactly 1 adaptive card attachment.</span></span> <span data-ttu-id="7f62d-182">`<< Card Payload >>`值是要发送的卡片的占位符。</span><span class="sxs-lookup"><span data-stu-id="7f62d-182">The `<< Card Payload >>` value is a placeholder for the card you wish to send.</span></span>

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

### <a name="the-botmessagepreview-send-and-edit-events"></a><span data-ttu-id="7f62d-183">BotMessagePreview 发送和编辑事件</span><span class="sxs-lookup"><span data-stu-id="7f62d-183">The botMessagePreview send and edit events</span></span>

<span data-ttu-id="7f62d-184">现在，您的邮件扩展将需要对两种新的调用进行响应 `composeExtension/submitAction` ，其中 `value.botMessagePreviewAction = "send"` 和 `value.botMessagePreviewAction = "edit"` 。</span><span class="sxs-lookup"><span data-stu-id="7f62d-184">Your message extension will now need to respond to two new varieties of the `composeExtension/submitAction` invoke, where `value.botMessagePreviewAction = "send"`and `value.botMessagePreviewAction = "edit"`.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7f62d-185">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7f62d-185">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="7f62d-186">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7f62d-186">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="7f62d-187">JSON</span><span class="sxs-lookup"><span data-stu-id="7f62d-187">JSON</span></span>](#tab/json)

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

### <a name="respond-to-botmessagepreview-edit"></a><span data-ttu-id="7f62d-188">响应 botMessagePreview 编辑</span><span class="sxs-lookup"><span data-stu-id="7f62d-188">Respond to botMessagePreview edit</span></span>

<span data-ttu-id="7f62d-189">如果用户通过单击 "**编辑**" 按钮决定在发送前编辑卡片，您将收到带有的 `composeExtension/submitAction` invoke `value.botMessagePreviewAction = edit` 。</span><span class="sxs-lookup"><span data-stu-id="7f62d-189">If the user decides to edit the card before sending by clicking the **Edit** button, you will receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = edit`.</span></span> <span data-ttu-id="7f62d-190">通常情况下，应通过返回发送的任务模块来响应开始交互的初始调用，以做出响应 `composeExtension/fetchTask` 。</span><span class="sxs-lookup"><span data-stu-id="7f62d-190">You should typically respond by returning the task module you sent in response to the initial `composeExtension/fetchTask` invoke that began the interaction.</span></span> <span data-ttu-id="7f62d-191">这样一来，用户可以通过重新输入原始信息来开始此过程。</span><span class="sxs-lookup"><span data-stu-id="7f62d-191">This allows the user to start the process over by re-entering the original information.</span></span> <span data-ttu-id="7f62d-192">此外，您还应考虑使用现在可用于预填充任务模块的信息，以便用户无需从头开始填写所有信息。</span><span class="sxs-lookup"><span data-stu-id="7f62d-192">You should also consider using the information you now have available to pre-populate the task module so the user doesn't have fill out all of the information from scratch.</span></span>

<span data-ttu-id="7f62d-193">请参阅[响应初始 `fetchTask` 事件](~/messaging-extensions/how-to/action-commands/create-task-module.md)。</span><span class="sxs-lookup"><span data-stu-id="7f62d-193">See [responding to the initial `fetchTask` event](~/messaging-extensions/how-to/action-commands/create-task-module.md).</span></span>

### <a name="respond-to-botmessagepreview-send"></a><span data-ttu-id="7f62d-194">响应 botMessagePreview send</span><span class="sxs-lookup"><span data-stu-id="7f62d-194">Respond to botMessagePreview send</span></span>

<span data-ttu-id="7f62d-195">用户单击 "**发送**" 按钮后，您将收到 `composeExtension/submitAction` 带调用的 invoke `value.botMessagePreviewAction = send` 。</span><span class="sxs-lookup"><span data-stu-id="7f62d-195">Once the user clicks the **Send** button, you will receive a `composeExtension/submitAction` invoke with `value.botMessagePreviewAction = send`.</span></span> <span data-ttu-id="7f62d-196">您的 web 服务将需要创建一个具有自适应卡片的主动消息，并将其发送到对话，同时还会回复调用。</span><span class="sxs-lookup"><span data-stu-id="7f62d-196">Your web service will need to create and send a proactive message with the Adaptive Card to the conversation, and also reply to the invoke.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7f62d-197">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7f62d-197">C#/.NET</span></span>](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[<span data-ttu-id="7f62d-198">JavaScript/Node.js</span><span class="sxs-lookup"><span data-stu-id="7f62d-198">JavaScript/Node.js</span></span>](#tab/javascript)

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

# <a name="json"></a>[<span data-ttu-id="7f62d-199">JSON</span><span class="sxs-lookup"><span data-stu-id="7f62d-199">JSON</span></span>](#tab/json)

<span data-ttu-id="7f62d-200">你将收到一 `composeExtension/submitAction` 封类似下面的新邮件。</span><span class="sxs-lookup"><span data-stu-id="7f62d-200">You will receive a new `composeExtension/submitAction` message similar to the one below.</span></span>

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

### <a name="user-attribution-for-bots-messages"></a><span data-ttu-id="7f62d-201">Bot 消息的用户归属</span><span class="sxs-lookup"><span data-stu-id="7f62d-201">User attribution for bots messages</span></span> 

<span data-ttu-id="7f62d-202">在 bot 代表用户发送邮件的情况下，将邮件的特性化到该用户可以帮助接洽，并展示更自然的交互流程。</span><span class="sxs-lookup"><span data-stu-id="7f62d-202">In scenarios where a bot sends messages on behalf of a user, attributing the message to that user can help with engagement and showcase a more natural interaction flow.</span></span> <span data-ttu-id="7f62d-203">此功能允许您代表正在启动邮件的用户发送邮件。</span><span class="sxs-lookup"><span data-stu-id="7f62d-203">This feature allows you to send messages on behalf of the user who is initiating the message.</span></span>

<span data-ttu-id="7f62d-204">在下面的图像中，左侧是由*不带*用户归属的 bot 发送的卡片邮件，右侧是由*具有*用户归属的 bot 发送的卡片。</span><span class="sxs-lookup"><span data-stu-id="7f62d-204">In the image below, on the left is a card message sent by a bot *without* user attribution and on the right is a card sent by a bot *with* user attribution.</span></span>

![屏幕截图](../../../assets/images/messaging-extension/user-attribution-bots.png)

<span data-ttu-id="7f62d-206">若要在团队中使用用户归属，您需要将 `OnBehalfOf` 提及实体添加到 `ChannelData` `Activity` 发送给团队的有效负载中。</span><span class="sxs-lookup"><span data-stu-id="7f62d-206">To use user attribution in teams, you need to add the `OnBehalfOf` mention entity to `ChannelData` in your `Activity` payload that is sent to Teams.</span></span>

# <a name="cnet"></a>[<span data-ttu-id="7f62d-207">C#/.NET</span><span class="sxs-lookup"><span data-stu-id="7f62d-207">C#/.NET</span></span>](#tab/dotnet-1)

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

# <a name="json"></a>[<span data-ttu-id="7f62d-208">JSON</span><span class="sxs-lookup"><span data-stu-id="7f62d-208">JSON</span></span>](#tab/json-1)

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

<span data-ttu-id="7f62d-209">以下是对数组中的实体的说明 `OnBehalfOf` ：</span><span class="sxs-lookup"><span data-stu-id="7f62d-209">Below is a description of the entities in the `OnBehalfOf` of Array:</span></span>

#### <a name="details-of--onbehalfof-entity-schema"></a><span data-ttu-id="7f62d-210">实体架构的详细信息 `OnBehalfOf`</span><span class="sxs-lookup"><span data-stu-id="7f62d-210">Details of  `OnBehalfOf` entity schema</span></span>

|<span data-ttu-id="7f62d-211">字段</span><span class="sxs-lookup"><span data-stu-id="7f62d-211">Field</span></span>|<span data-ttu-id="7f62d-212">类型</span><span class="sxs-lookup"><span data-stu-id="7f62d-212">Type</span></span>|<span data-ttu-id="7f62d-213">说明</span><span class="sxs-lookup"><span data-stu-id="7f62d-213">Description</span></span>|
|:---|:---|:---|
|`itemId`|<span data-ttu-id="7f62d-214">Integer</span><span class="sxs-lookup"><span data-stu-id="7f62d-214">Integer</span></span>|<span data-ttu-id="7f62d-215">应为0</span><span class="sxs-lookup"><span data-stu-id="7f62d-215">Should be 0</span></span>|
|`mentionType`|<span data-ttu-id="7f62d-216">String</span><span class="sxs-lookup"><span data-stu-id="7f62d-216">String</span></span>|<span data-ttu-id="7f62d-217">应为 "person"</span><span class="sxs-lookup"><span data-stu-id="7f62d-217">Should be "person"</span></span>|
|`mri`|<span data-ttu-id="7f62d-218">String</span><span class="sxs-lookup"><span data-stu-id="7f62d-218">String</span></span>|<span data-ttu-id="7f62d-219">邮件资源标识符 (其代表其发送邮件的人员的 MRI) 。</span><span class="sxs-lookup"><span data-stu-id="7f62d-219">Message resource identifier (MRI) of the person on whose behalf the message is sent.</span></span> <span data-ttu-id="7f62d-220">邮件发件人名称将显示为 " \<user\> via \<bot name\> "。</span><span class="sxs-lookup"><span data-stu-id="7f62d-220">Message sender name would appear as "\<user\> via \<bot name\>".</span></span>|
|`displayName`|<span data-ttu-id="7f62d-221">String</span><span class="sxs-lookup"><span data-stu-id="7f62d-221">String</span></span>|<span data-ttu-id="7f62d-222">人员的姓名。</span><span class="sxs-lookup"><span data-stu-id="7f62d-222">Name of the person.</span></span> <span data-ttu-id="7f62d-223">在案例名称解析中不可用时用作回退。</span><span class="sxs-lookup"><span data-stu-id="7f62d-223">Used as fallback in case name resolution is unavailable.</span></span>|
  
## <a name="next-steps"></a><span data-ttu-id="7f62d-224">后续步骤</span><span class="sxs-lookup"><span data-stu-id="7f62d-224">Next Steps</span></span>

<span data-ttu-id="7f62d-225">添加搜索命令</span><span class="sxs-lookup"><span data-stu-id="7f62d-225">Add a search command</span></span>

* [<span data-ttu-id="7f62d-226">定义搜索命令</span><span class="sxs-lookup"><span data-stu-id="7f62d-226">Define search commands</span></span>](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
