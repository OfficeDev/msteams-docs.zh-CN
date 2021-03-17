---
title: 响应任务模块提交操作
author: clearab
description: 介绍如何从消息传递扩展操作命令响应任务模块提交操作
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: fecc0ace5f767da3764529a9e8a590b37e547bb0
ms.sourcegitcommit: 1ce74ed167bb81bf09f7f6f8d518093efafb549e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/16/2021
ms.locfileid: "50827940"
---
# <a name="respond-to-the-task-module-submit-action"></a>响应任务模块提交操作

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

在用户提交任务模块后，Web 服务会收到一条调用消息，该消息包含 `composeExtension/submitAction` 命令 ID 和参数值。 你的应用有五秒钟时间响应调用，否则用户会收到错误消息"无法访问应用"，并且 Teams客户端将忽略对调用的任何回复。

有以下响应选项：

* 无响应 - 你可以选择使用提交操作在外部系统中触发进程，而不要向用户提供任何反馈。 这对长时间运行的过程很有用，你可以选择以其他方式提供反馈 (例如，使用主动 [消息](~/bots/how-to/conversations/send-proactive-messages.md)。
* [另一个](#respond-with-another-task-module) 任务模块 - 作为多步骤交互的一部分，可以使用其他任务模块进行响应。
* [卡片](#respond-with-a-card-inserted-into-the-compose-message-area) 响应 - 可以使用卡片进行响应，然后用户可以与之交互和/或插入到邮件中。
* [自动程序中的自适应卡片](#bot-response-with-adaptive-card) - 将自适应卡片直接插入对话中。
* [请求用户进行身份验证](~/messaging-extensions/how-to/add-authentication.md)
* [请求用户提供其他配置](~/messaging-extensions/how-to/add-configuration-page.md)

对于身份验证或配置，在用户完成流后，原始调用将重新发送到 Web 服务。 下表根据消息扩展的调用位置显示哪些类型的响应 `commandContext` 可用： 

|响应类型 | compose | 命令栏 | message |
|--------------|:-------------:|:-------------:|:---------:|
|卡片响应 | x | x | x |
|另一个任务模块 | x | x | x |
|带自适应卡片的自动程序 | x |  | x |
| 无响应 | x | x | x |

> [!NOTE]
> * 当你选择 **"Action.Submit** through ME cards"时，它会发送名称为 **composeExtension** 的 invoke 活动，其中值等于常规有效负载。
> * 选择 **"Action.Submit** through conversation"时，将收到名称为 **onCardButtonClicked** 的邮件活动，其中值等于常规有效负载。

## <a name="the-submitaction-invoke-event"></a>submitAction 调用事件

接收调用消息的示例如下所示：

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionSubmitActionAsync(
  ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken) {
  //code to handle the submit action
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  constructor() {
  handleTeamsMessagingExtensionSubmitAction(context, action) {
  
  //code to handle the submit action
    }
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

这是您收到的 JSON 对象的示例。 `commandContext`参数指示从何处触发邮件扩展。 `data`对象包含作为参数的表单上的字段以及用户提交的值。 此处的 JSON 对象已缩短，以突出显示最相关的字段。

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a>在撰写邮件区域中插入卡片进行响应

响应请求的最常见方法 `composeExtension/submitAction` 为将卡片插入撰写邮件区域。 然后，用户可以选择将卡片提交到对话。 有关使用卡片的信息，请参阅 [卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

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

## <a name="respond-with-another-task-module"></a>使用另一个任务模块响应

可以选择使用附加任务 `submitAction` 模块来响应事件。 当：

* 您需要收集大量信息。
* 如果需要根据用户输入动态更改所收集的信息
* 如果需要验证用户提交的信息，并可能重新发送包含错误消息的表单（如果出现错误）。 

响应 方法与响应初始事件 [ `fetchTask` 相同](~/messaging-extensions/how-to/action-commands/create-task-module.md)。 如果你使用的是 Bot Framework SDK，则针对这两个提交操作使用相同的事件触发器。 这意味着您必须添加确定正确响应的逻辑。

## <a name="bot-response-with-adaptive-card"></a>使用自适应卡片的自动程序响应

>[!Note]
>此流要求将对象添加到应用清单，并且为自动 `bot` 程序定义必要的作用域。 使用与自动程序的邮件扩展相同的 ID。

还可以响应提交操作，方法为使用自动程序将带自适应卡片的消息插入频道。 你的用户可以在提交邮件之前预览它，并可能编辑邮件或与之交互。 当你在创建自适应卡片响应之前从用户收集信息时，或者当你在某人与之交互后更新卡片时，这会非常有用。 以下方案显示应用 Polly 如何使用此流配置轮询，而不在频道对话中包括配置步骤：

1. 用户选择消息扩展以触发任务模块。
2. 用户使用任务模块配置轮询。
3. 提交任务模块后，应用使用提供的信息将轮询生成为自适应卡片，并将其作为 `botMessagePreview` 响应发送给客户端。
4. 然后，用户可以预览自适应卡片消息，然后机器人将其插入频道。 如果应用不是频道成员，选择添加 `Send` 它。
   1. 用户还可以选择将邮件返回到原始任务 `Edit` 模块的邮件。
5. 与自适应卡片交互在发送邮件之前会更改消息。
6. 用户选择自动 `Send` 程序后，将消息发送到频道。

### <a name="respond-to-initial-submit-action"></a>响应初始提交操作

若要启用此流，任务模块应该使用自动程序发送到频道的卡片预览来响应 `composeExtension/submitAction` 初始消息。 这样一来，用户有机会在发送之前验证该卡，并尝试在对话中安装聊天机器人（如果尚未安装）。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

>[!Note]
>必须 `activityPreview` 包含正好包含 `message` 1 个自适应卡片附件的活动。 `<< Card Payload >>`该值是你希望发送的卡片的占位符。

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

### <a name="the-botmessagepreview-send-and-edit-events"></a>botMessagePreview 发送和编辑事件

现在，你的邮件扩展必须响应调用的两个新 `composeExtension/submitAction` 类，其中 `value.botMessagePreviewAction = "send"` 和 `value.botMessagePreviewAction = "edit"` 。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

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

如果用户通过选择"编辑"按钮在发送前编辑卡片，将收到 `composeExtension/submitAction` 一个调用 `value.botMessagePreviewAction = edit` 。 通常，应该通过返回为响应启动交互的初始调用而发送的任务 `composeExtension/fetchTask` 模块来做出响应。 这允许用户通过重新输入原始信息来重新开始此过程。 使用可用信息预填充任务模块，以便用户无需从头开始填写所有信息。

请参阅 [响应初始 `fetchTask` 事件](~/messaging-extensions/how-to/action-commands/create-task-module.md)。

### <a name="respond-to-botmessagepreview-send"></a>响应 botMessagePreview 发送

在用户选择"发送 **"** 按钮后，您将收到 `composeExtension/submitAction` 一个调用 `value.botMessagePreviewAction = send` 。 Web 服务必须创建一条带自适应卡片的主动消息并将其发送到对话，并回复调用。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

您收到类似于 `composeExtension/submitAction` 以下的新邮件：

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

### <a name="user-attribution-for-bots-messages"></a>自动程序消息的用户属性 

在机器人代表用户发送邮件的情况下，将消息归为该用户有助于参与，并展示更自然的交互流。 此功能允许你将来自自动程序的邮件属性属性给代表其发送该邮件的用户。

在下图的左侧是自动程序发送的无用户属性的卡片消息，右侧是自动程序发送的具有用户 *属性* 的卡片。

![屏幕截图](../../../assets/images/messaging-extension/user-attribution-bots.png)

若要在团队中使用用户属性，必须在发送到 Teams 的有效负载中添加 `OnBehalfOf` mention `ChannelData` `Activity` 实体。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet-1)

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

# <a name="json"></a>[JSON](#tab/json-1)

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

以下部分介绍了 Array 中的 `OnBehalfOf` 实体：

#### <a name="details-of--onbehalfof-entity-schema"></a>实体  `OnBehalfOf` 架构的详细信息

|字段|类型|说明|
|:---|:---|:---|
|`itemId`|整数|应为 0|
|`mentionType`|String|应为"人"|
|`mri`|String|邮件资源 (MRI) 代表其发送邮件的人的 MRI 标识符。 通过""，邮件发件人 \<user\> 名称将显示为 \<bot name\> ""。|
|`displayName`|String|人员的姓名。 在名称解析不可用时用作回退。|
  
## <a name="next-steps"></a>后续步骤

添加搜索命令

* [定义搜索命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
