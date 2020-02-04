---
title: 响应任务模块提交操作
author: clearab
description: 介绍如何从邮件扩展操作命令响应任务模块提交操作
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 33a9388ee84dcf03a5bda59c5a5139c6f49bde6c
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673310"
---
# <a name="respond-to-the-task-module-submit-action"></a>响应任务模块提交操作

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

用户提交任务模块后，web 服务将收到设置了命令 id `composeExtension/submitAction`和参数值的 invoke 消息。 您的应用程序将有5秒的时间来响应调用，否则，用户将收到 "无法访问应用" 错误消息，并且团队客户端将忽略对该调用的任何答复。

您有以下选项可供您进行响应。

* 无响应-你可以选择使用 "提交" 操作在外部系统中触发进程，而不向用户提供任何反馈。 这对于长时间运行的进程很有用，您可以选择以另一种方式提供反馈（例如，使用[主动消息](~/bots/how-to/conversations/send-proactive-messages.md)）。
* [另一个任务模块](#respond-with-another-task-module)-您可以作为多步骤交互的一部分，使用其他任务模块进行响应。
* [卡片响应](#respond-with-a-card-inserted-into-the-compose-message-area)-你可以使用用户可与之交互和/或插入邮件的卡片进行响应。
* [来自 bot 的自适应卡片](#bot-response-with-adaptive-card)-将自适应卡片直接插入对话中。
* [请求用户进行身份验证](~/messaging-extensions/how-to/add-authentication.md)
* [请求用户提供其他配置](~/messaging-extensions/how-to/add-configuration-page.md)

下表显示了哪些类型的响应可基于邮件扩展的调用位置（`commandContext`）。 对于身份验证或配置，一旦用户完成了流，原始调用将重新发送到您的 web 服务。

|响应类型 | 编撰 | 命令栏 | message |
|--------------|:-------------:|:-------------:|:---------:|
|卡片响应 | x | x | x |
|另一个任务模块 | x | x | x |
|带有自适应卡片的 Bot | x |  | x |
| 无响应 | x | x | x |

## <a name="the-submitaction-invoke-event"></a>SubmitAction 调用事件

下面是接收调用消息的示例。

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

这是您将收到的 JSON 对象的一个示例。 `commandContext`参数指示邮件扩展的触发位置。 `data`对象将窗体上的字段作为参数，并将用户提交的值包含在窗体中。 此处的 JSON 对象将被缩短，以突出显示最相关的字段。

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a>使用插入撰写邮件区域中的卡片进行响应

对`composeExtension/submitAction`请求做出响应的最常见方法是将卡片插入撰写邮件区域中。 然后，用户可以选择将该卡提交到对话中。 有关使用卡片的详细信息，请参阅[卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

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

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node.js](#tab/javascript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

## <a name="respond-with-another-task-module"></a>使用另一个任务模块进行响应

您可以选择使用其他任务模块`submitAction`响应事件。 这在以下情况中非常有用：

* 您需要收集大量信息。
* 如果您需要根据用户输入动态更改要收集的信息
* 如果需要验证用户提交的信息，并且可能会在出现错误时使用错误消息重新发送该表单。 

响应方法与[响应初始`fetchTask`事件](~/messaging-extensions/how-to/action-commands/create-task-module.md)相同。 如果您使用的是 Bot 框架 SDK，则相同的事件将触发这两个提交操作。 这意味着您需要确保添加确定正确响应的逻辑。

## <a name="bot-response-with-adaptive-card"></a>使用自适应卡片的 Bot 响应

>[!Note]
>此流要求您将`bot`对象添加到应用程序清单，并且您具有为 bot 定义的必要作用域。 使用与你的 bot 的邮件扩展相同的 Id。

您还可以通过将带有自适应卡片的邮件插入到使用 bot 的频道中来响应提交操作。 你的用户将能够在提交邮件之前预览邮件，并可能对其进行编辑/与之交互。 当您需要在创建自适应卡片响应之前从用户处收集信息，或者在某人与他人交互后需要更新卡片时，这可能非常有用。 以下方案显示了应用程序 Polly 如何使用此流配置轮询，而不在通道对话中包括配置步骤。

1. 用户单击邮件扩展可触发任务模块。
2. 用户使用任务 moudule 配置投票。
3. 提交任务模块后，应用使用提供的信息将轮询构建为自适应卡片，并将其作为`botMessagePreview`响应发送给客户端。
4. 然后，用户可以预览自适应卡片邮件，然后将其插入频道。 如果应用尚未成为频道的成员，则单击`Send` "" 将添加它。
   1. 用户还可以选择`Edit`将其返回到原始任务模块的邮件。
5. 与自适应卡片进行交互会在发送邮件之前对其进行更改。
6. 用户单击`Send`机器人后，会将邮件发送到频道。

### <a name="respond-to-initial-submit-action"></a>响应初始提交操作

若要启用此流，任务模块应使用 bot 将`composeExtension/submitAction`发送到频道的卡片的预览对初始邮件做出响应。 这使用户可以在发送之前验证卡，还会在对话中尝试安装你的 bot （如果尚未安装）。

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

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

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node.js](#tab/javascript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

>[!Note]
>`activityPreview`必须包含一个`message`只有1个自适应卡片附件的活动。 `<< Card Payload >>`值是要发送的卡片的占位符。

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

### <a name="the-botmessagepreview-send-and-edit-events"></a>BotMessagePreview 发送和编辑事件

现在，您的`composeExtension/submitAction`邮件扩展将需要对两种新的调用进行响应， `value.botMessagePreviewAction = "send"`其中`value.botMessagePreviewAction = "edit"`和。

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

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

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node.js](#tab/javascript)

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

# <a name="jsontabjson"></a>[JSON](#tab/json)

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

### <a name="respond-to-botmessagepreview-edit"></a>响应 botMessagePreview 编辑

如果用户通过单击 "**编辑**" 按钮决定在发送前编辑卡片，您将收到带有`composeExtension/submitAction` `value.botMessagePreviewAction = edit`的 invoke。 通常情况下，应通过返回发送的任务模块来响应开始交互的`composeExtension/fetchTask`初始调用，以做出响应。 这样一来，用户可以通过重新输入原始信息来开始此过程。 此外，您还应考虑使用现在可用于预填充任务模块的信息，以便用户无需从头开始填写所有信息。

请参阅[响应初始`fetchTask`事件](~/messaging-extensions/how-to/action-commands/create-task-module.md)。

### <a name="respond-to-botmessagepreview-send"></a>响应 botMessagePreview send

用户单击 "**发送**" 按钮后，您将收到带`composeExtension/submitAction`调用的`value.botMessagePreviewAction = send`invoke。 您的 web 服务将需要创建一个具有自适应卡片的主动消息，并将其发送到对话，同时还会回复调用。

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

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
  
  await turnContext.SendActivityAsync(responseActivity);

  return new MessagingExtensionActionResponse();
}
```

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node.js](#tab/javascript)

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
      const responseActivity = { type: 'message', attachments: [adaptiveCard] };
    
      await context.sendActivity(responseActivity);
    }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

你将收到一封`composeExtension/submitAction`类似下面的新邮件。

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

## <a name="next-steps"></a>后续步骤

添加搜索命令

* [定义搜索命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
