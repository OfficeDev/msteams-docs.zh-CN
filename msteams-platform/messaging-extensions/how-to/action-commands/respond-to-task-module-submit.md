---
title: 响应任务模块提交操作
author: surbhigupta
description: 了解如何使用主动消息从消息扩展操作命令响应任务模块提交操作。 定义搜索命令并响应搜索。
ms.localizationpriority: medium
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 827c939080aa2eff182115966351356b0d71e3a9
ms.sourcegitcommit: 75d0072c021609af33ce584d671f610d78b3aaef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/28/2022
ms.locfileid: "68100481"
---
# <a name="respond-to-the-task-module-submit-action"></a>响应任务模块提交操作

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

本文档将介绍应用如何响应操作命令，例如用户的任务模块提交操作。
在用户提交任务模块后，Web 服务会收到一条 `composeExtension/submitAction` 调用消息，其中包含命令 ID 和参数值。 应用有五秒钟的时间响应调用，否则用户会收到错误消息“**无法访问应用**”，Teams 客户端将忽略任何调用回复。

有以下响应选项：

* 无响应：使用提交操作在外部系统中触发进程，而不向用户提供任何反馈。 它对于长时间运行的进程以及交替提供反馈非常有用。 例如，可以使用[主动消息](~/bots/how-to/conversations/send-proactive-messages.md)提供反馈。
* [另一个任务模块](#respond-with-another-task-module)：可以在多步骤交互过程中使用其他任务模块进行响应。
* [卡片响应](#respond-with-a-card-inserted-into-the-compose-message-area)：可以使用用户能与之交互或插入到消息中的卡片进行响应。
* [来自机器人的自适应卡片](#bot-response-with-adaptive-card)：将自适应卡片直接插入对话中。
* [请求用户进行身份验证](~/messaging-extensions/how-to/add-authentication.md)。
* [请求用户提供其他配置](~/get-started/first-message-extension.md)。

对于身份验证或配置，在用户完成该过程后，原始调用将重新发送到 Web 服务。 下表根据消息扩展插件的调用位置 `commandContext` 显示哪些类型的响应可用：

|响应类型 | 撰写 | 命令栏 | 邮件 |
|--------------|:-------------:|:-------------:|:---------:|
|卡片响应 | ✔️ | ✔️ | ✔️ |
|另一个任务模块 | ✔️ | ✔️ | ✔️ |
|带自适应卡片的机器人 | ✔️ | ❌ | ✔️ |
| 无响应 | ✔️ | ✔️ | ✔️ |

> [!NOTE]
>
> * 当通过 ME 卡片选择 **Action.Submit** 时，它会发送名为 **composeExtension** 的调用活动，其中值等于常用有效负载。
> * 当通过对话选择 **Action.Submit** 时，将收到名为 **onCardButtonClicked** 的消息活动，其中值等于常用有效负载。

如果应用包含对话机器人，请在对话中安装机器人，然后加载任务模块。 机器人可用于获取任务模块的其他上下文。 若要安装对话机器人，请参阅[请求安装对话机器人](create-task-module.md#request-to-install-your-conversational-bot)。

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

这是收到的 JSON 对象的示例。 `commandContext` 参数指示从何处触发消息扩展。 `data` 对象包含表单上的字段作为参数，以及用户提交的值。 JSON 对象突出显示最相关的字段。

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

## <a name="respond-with-a-card-inserted-into-the-compose-message-area"></a>使用插入到撰写消息区域的卡片进行响应

响应 `composeExtension/submitAction` 请求的最常见方式是将卡片插入到撰写消息区域。 用户将卡片提交到对话。 有关使用卡片的详细信息，请参阅[卡片和卡片操作](~/task-modules-and-cards/cards/cards-actions.md)。

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

## <a name="respond-with-another-task-module"></a>使用另一个任务模块进行响应

可以选择使用其他任务模块响应 `submitAction` 事件。 当需要完成以下任务时，这非常有用：

* 收集大量信息。
* 根据用户输入动态更改信息集合。
* 验证用户提交的信息，并在出现错误时重新发送带有错误消息的表单。

响应方法与[响应初始 `fetchTask` 事件](~/messaging-extensions/how-to/action-commands/create-task-module.md)相同。 如果使用的是 Bot Framework SDK，则两个提交操作都会触发相同的事件。 若要使此操作正常工作，必须添加确定正确响应的逻辑。

## <a name="bot-response-with-adaptive-card"></a>使用自适应卡片获取机器人响应

> [!NOTE]
> The prerequisite to get the bot response with an Adaptive card is that you must add the `bot` object to your app manifest, and define the required scope for the bot. Use the same ID as your message extension for your bot.

你还可以通过使用机器人将带有自适应卡片的消息插入频道来响应 `submitAction`。 用户可以在提交消息之前预览它。 如果要在创建自适应卡片响应之前从用户那里收集信息，或者在有人与卡片交互后更新卡片时，这非常有用。

以下方案演示了应用 Polly 如何在包含频道对话中的配置步骤的情况下配置轮询：

若要配置轮询，请执行以下操作：

1. 用户选择消息扩展以调用任务模块。
1. 用户使用任务模块配置轮询。
1. 提交任务模块后，应用使用提供的信息将轮询生成为自适应卡片，并将其作为 `botMessagePreview` 响应发送给客户端。
1. 然后，用户可以在机器人将自适应卡片消息插入频道之前预览它。 如果应用不是通道的成员，请选择 `Send` 添加它。

    > [!NOTE]
    >
    > * 用户还可以选择 `Edit` 消息，这样会将其返回到原始任务模块。
    > * 与自适应卡片的交互会在发送消息之前更改消息。
    >
1. 用户选择 `Send`后，机器人会将消息发布到通道。

## <a name="respond-to-initial-submit-action"></a>响应初始提交操作

任务模块必须使用机器人发送到频道的卡片预览来响应初始 `composeExtension/submitAction` 消息。 用户可以在发送之前验证卡片，如果已安装机器人，则尝试在会话中安装机器人。

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

> [!NOTE]
>
> * `activityPreview` 必须包含仅具有一个自适应卡片附件的 `message` 活动。 `<< Card Payload >>` 值是要发送的卡片的占位符。

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

消息扩展必须响应两种新类型的 `composeExtension/submitAction` 调用，其中 `value.botMessagePreviewAction = "send"` 和 `value.botMessagePreviewAction = "edit"`。

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

如果用户在发送前编辑卡片，则通过选择“**编辑**”，你将收到一个带有 `value.botMessagePreviewAction = edit` 的 `composeExtension/submitAction` 调用。 通过返回你发送的任务模块进行响应，以响应开始交互的初始 `composeExtension/fetchTask` 调用。 这允许用户通过重新输入原始信息来启动进程。 使用可用信息更新任务模块，以便用户无需从头填写所有信息。
有关响应初始 `fetchTask` 事件的详细信息，请参阅[响应初始 `fetchTask` 事件](~/messaging-extensions/how-to/action-commands/create-task-module.md)。

### <a name="respond-to-botmessagepreview-send"></a>响应 botMessagePreview 发送

在用户选择“**发送**”后，你将收到带有 `value.botMessagePreviewAction = send` 的 `composeExtension/submitAction` 调用。 Web 服务必须使用自适应卡片创建主动消息并将其发送到对话，并回复调用。

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

你将收到类似于以下内容的新 `composeExtension/submitAction` 消息：

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

### <a name="user-attribution-for-bots-messages"></a>机器人消息的用户归属

如果机器人代表用户发送消息，则将消息归属于该用户有助于参与并展示更自然的交互流程。 使用此功能，可以将来自机器人的消息归属为代表其发送消息的用户。

在下图中，左侧是机器人在没有用户归属的情况下发送的卡片消息，右侧是机器人在有用户归属的情况下发送的卡片。

:::image type="content" source="../../../assets/images/messaging-extension/user-attribution-bots.png" alt-text="用户归属机器人":::

若要在团队中使用用户归属，必须将 `OnBehalfOf` 提及实体添加到发送到团队的 `Activity` 有效负载中的 `ChannelData`。

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

#### <a name="details-of--onbehalfof-entity-schema"></a>`OnBehalfOf` 实体架构的详细信息

以下部分介绍了 `OnBehalfOf` 数组中的实体：

|字段|类型|说明|
|:---|:---|:---|
|`itemId`|整数|介绍项目的标识。 其值必须是 `0`。|
|`mentionType`|字符串|介绍“人员”的提及。|
|`mri`|String|代表其发送消息的人员的消息资源标识符 (MRI)。 消息发件人名称将显示为“\<user\> - \<bot name\>”。|
|`displayName`|String|Name of the person. Used as fallback in case name resolution is unavailable.|
  
## <a name="code-sample"></a>代码示例

| 示例名称           | 说明 | .NET    | Node.js   |
|:---------------------|:--------------|:---------|:--------|
|Teams 消息扩展操作| 介绍如何定义操作命令、创建任务模块和响应任务模块提交操作。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) |
|Teams 消息扩展搜索   |  介绍如何定义搜索命令和响应搜索。        |[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [定义搜索命令](~/messaging-extensions/how-to/search-commands/define-search-command.md)

## <a name="see-also"></a>另请参阅

[响应搜索命令](~/messaging-extensions/how-to/search-commands/respond-to-search.md)
