---
title: 创建并发送任务模块
author: clearab
description: 如何处理初始调用操作并从操作消息扩展命令中的任务模块进行响应
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f5f96e71517d45f52d17d2d70c583ec1eec3babd
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673312"
---
# <a name="create-and-send-the-task-module"></a>创建并发送任务模块

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

如果您不使用应用程序清单中定义的参数填充任务模块，则需要创建向用户显示的任务模块。 您可以使用自适应卡片或嵌入的 web 视图。

## <a name="the-initial-invoke-request"></a>初始调用请求

使用此方法，您的服务将`Activity`接收类型`composeExtension/fetchTask`的对象，您需要使用包含自适应卡片`task`的对象或嵌入的 web 视图的 URL 来进行响应。 除了标准 bot 活动属性，初始调用负载还包含以下请求元数据：

|属性名称|用途|
|---|---|
|`type`| 请求类型;必须为`invoke`。 |
|`name`| 向您的服务发出的命令的类型。 将为`composeExtension/fetchTask`。 |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| 发送请求的用户的 Azure Active Directory 对象 id。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.channel.id`| 通道 ID （如果请求是在通道中发出的）。 |
|`channelData.team.id`| "工作组 ID" （如果请求是在通道中进行的）。 |
|`value.commandId` | 包含调用的命令的 Id。 |
|`value.commandContext` | 触发事件的上下文。 将为`compose`。 |
|`value.context.theme` | 用户的客户端主题，对于嵌入的 web 视图格式很有用。 将为`default` `contrast`或`dark`。 |

### <a name="example-fetchtask-request"></a>示例 fetchTask 请求

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/fetchTask",
  "type": "invoke",
  "timestamp": "2019-07-01T22:57:22.175Z",
  "localTimestamp": "2019-07-01T15:57:22.175-07:00",
  "id": "f:0123456878990178955",
  "channelId": "msteams",
  "serviceURL": "https://smba.trafficmanager.net/amer/",
  "from": {
    "id": "29:1test2GgHIa0DXzDT_OGwL5vSMZdAxDlGR7hYxZ6_JBVqHz2Zq9Nm44FUNWqHCdGBwHg8WrlFRsYrd0cCAS7dig",
    "name": "John Smith",
    "aadObjectId": "1234567d-1234-462a-8952-35b75f16f1e1"
  },
  "conversation": {
    "isGroup": true,
    "conversationType": "channel",
    "tenantId": "1234abcd-1234-12ab-12ab-35b75f16f1e1",
    "id": "19:83ed1d507cb5427c93495cf914326310@thread.skype"
  },
  "recipient": {
    "id": "28:049566e0-4401-4bcf-86a1-ce22082ce03a",
    "name": "mess"
  },
  "entities": [
    {
      "locale": "en-US",
      "country": "US",
      "platform": "Windows",
      "type": "clientInfo"
    }
  ],
  "channelData": {
    "channel": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "team": {
      "id": "19:83ab1d507cb5427c93495cf912345678@thread.skype"
    },
    "tenant": {
      "id": "1234abcd-1234-12ab-12ab-35b75f16f1e1"
    },
    "source": {
      "name": "compose"
    }
  },
  "value": {
    "commandId": "hello",
    "commandContext": "compose",
    "context": {
      "theme": "dark"
    }
  },
  "locale": "en-US"
}
```

* * *

## <a name="initial-invoke-request-from-a-message"></a>来自邮件的初始调用请求

从邮件（而不是撰写区域或命令栏）调用 bot 时，初始请求中`value`的对象将包含从其调用邮件扩展的邮件的详细信息。 下面是此对象的一个示例。 和`reactions` `mentions`数组是可选的，如果原始邮件中没有反应或提及，则不会显示。

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
...
  "value": {
    "commandId": "setReminder",
    "commandContext": "message",
    "messagePayload": {
      "id": "1111111111",
      "replyToId": null,
      "createdDateTime": "2019-02-25T21:29:36.065Z",
      "lastModifiedDateTime": null,
      "deleted": false,
      "subject": "Message subject",
      "summary": null,
      "importance": "normal",
      "locale": "en-us",
      "body": {
        "contentType": "html",
        "content": "This is the message the messaging extension was invoked from."
    },
      "from": {
        "device": null,
        "conversation": null,
        "user": {
          "userIdentityType": "aadUser",
          "id": "wxyz12ab8-ab12-cd34-ef56-098abc123876",
          "displayName": "Jamie Smythe"
        },
        "application": null
      },
      "reactions": [
        {
          "reactionType": "like",
          "createdDateTime": "2019-02-25T22:40:40.806Z",
          "user": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "qrst12346-ab12-cd34-ef56-098abc123876",
              "displayName": "Jim Brown"
            },
            "application": null
          }
        }
      ],
      "mentions": [
        {
          "id": 0,
          "mentionText": "Sarah",
          "mentioned": {
            "device": null,
            "conversation": null,
            "user": {
              "userIdentityType": "aadUser",
              "id": "ab12345678-ab12-cd34-ef56-098abc123876",
              "displayName": "Sarah"
            },
            "application": null
          }
        }
      ]
    }
  ...
```

* * *

## <a name="respond-to-the-fetchtask"></a>响应 fetchTask

使用包含自适应卡片或 web `task` URL 的`taskInfo`对象的对象或简单的字符串消息来响应调用请求。

|属性名称|用途|
|---|---|
|`type`| 可以是`continue`显示窗体，也`message`可以是一个简单的弹出窗口。 |
|`value`| 或者是`taskInfo`窗体的对象，或者是`string`邮件的。 |

TaskInfo 对象的架构为：

|属性名称|用途|
|---|---|
|`title`| 任务模块的标题。|
|`height`| 可以是整数（以像素为单位），也`small`可以`medium`是`large`，或。|
|`width`| 可以是整数（以像素为单位），也`small`可以`medium`是`large`，或。|
|`card`| 自适应卡片，用于定义表单（如果使用一个）。
|`url`| 要作为嵌入 web 视图在任务模块内打开的 URL。|
|`fallbackUrl`| 如果客户端不支持任务模块功能，则在浏览器选项卡中打开此 URL。 |

### <a name="with-an-adaptive-card"></a>使用自适应卡片

使用自适应卡片时，需要使用包含自适应卡片的`task` `value`对象进行响应。

#### <a name="example-fetchtask-response-with-an-adaptive-card"></a>使用自适应卡片的 fetchTask 响应示例

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

除了 Bot 框架 SDK 之外，本示例还使用[AdaptiveCards NuGet 包](https://www.nuget.org/packages/AdaptiveCards)。

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Card = new Attachment()
        {
          ContentType = AdaptiveCard.ContentType,
          Content = new AdaptiveCard("1.0")
          {
            Body = new List<AdaptiveElement>()
            {
              new AdaptiveTextInput() { Id = "FormField1", Placeholder = placeholder},
              new AdaptiveTextInput() { Id = "FormField2", Placeholder = "FormField2"},
              new AdaptiveTextInput() { Id = "FormField3", Placeholder = "FormField3"},
            },
            Actions = new List<AdaptiveAction>()
            {
              new AdaptiveSubmitAction()
              {
                Type = AdaptiveSubmitAction.TypeName,
                Title = "Submit",
              },
            },
          },
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
    handleTeamsMessagingExtensionFetchTask(context, action) {
      const adaptiveCard = CardFactory.adaptiveCard({
        actions: [{
          data: { submitLocation: 'messagingExtensionFetchTask'},
          title: 'Submit',
          type: 'Action.Submit'
        }],
        body: [
          { text: 'Task Module', type: 'TextBlock', weight: 'bolder'},
          { type: 'TextBlock', text: 'Enter text for Question:' },
          { id: 'Question', placeholder: 'Question text here', type: 'Input.Text', value: userText },
          { type: 'TextBlock', text: 'Options for Question:' },
          { type: 'TextBlock', text: 'Is Multi-Select:' },
          {
            choices: [{ title: 'True', value: 'true' }, { title: 'False', value: 'false' }],
            id: 'MultiSelect',
            isMultiSelect: false,
            style: 'expanded',
            type: 'Input.ChoiceSet',
            value: isMultiSelect ? 'true' : 'false'
          },
          { id: 'Option1', placeholder: 'Option 1 here', type: 'Input.Text', value: option1 },
          { id: 'Option2', placeholder: 'Option 2 here', type: 'Input.Text', value: option2 }
        ],
        type: 'AdaptiveCard',
        version: '1.0'
      });

      return {
        task: {
          type: 'continue',
          value: {
            card: adaptiveCard,
            height: 450,
            title: 'Task Module Fetch Example',
            url: null,
            width: 500
          }
        }
      };
    }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "card":
      {
        "type": "AdaptiveCard",
        "version": "1.0",
        "body": [
          {
            "type": "Input.Text",
            "placeholder": "FormField1",
            "id": "FormField1"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField2",
            "id": "FormField2"
          },
          {
            "type": "Input.Text",
            "placeholder": "FormField3",
            "id": "FormField3"
          },
          {
            "type": "ActionSet",
            "actions": [
              {
                "type": "Action.Submit",
                "title": "Action.Submit",
                "id": "submitAction"
              }
            ]
          }
        ],
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json"
      }
    }
  }
}
```

* * *

### <a name="with-an-embedded-web-view"></a>嵌入的 web 视图

使用嵌入的 web 视图时，需要使用包含要加载的 web `task`表单 URL 的`value`对象的对象进行响应。 您要加载的任何 URL 的域必须包含在应用程序清单`validDomains`中的阵列中。 有关生成嵌入的 web 视图的完整信息，请参阅[任务模块文档](~/task-modules-and-cards/what-are-task-modules.md)。

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  string placeholder = "Not invoked from message";

  if (action.MessagePayload != null)
  {
      var messageText = action.MessagePayload.Body.Content;
      var fromId = action.MessagePayload.From.User.Id;
      placeholder = "Invoked from message";
  }

  var response = new MessagingExtensionActionResponse()
  {
    Task = new TaskModuleContinueResponse()
    {
      Value = new TaskModuleTaskInfo()
      {
        Height = "small",
        Width = "small",
        Title = "Example task module",
        Url = "https://contoso.com/msteams/taskmodules/newcustomer",
        },
      },
    },
  };
  return response;
}
```

# <a name="javascriptnodejstabjavascript"></a>[JavaScript/node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    return {
      task: {
        type: 'continue',
        value: {
          width: 500,
          height: 450,
          title: 'Task Module Fetch Example',
          url: 'https://contoso.com/msteams/taskmodules/newcustomer',
          fallbackUrl: 'https://contoso.com/msteams/taskmodules/newcustomer'
        }
      }
    };
  }
}
```

# <a name="jsontabjson"></a>[JSON](#tab/json)

```json
{
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "url": "https://contoso.com/msteams/taskmodules/newcustomer",
      "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
    }
  }
}
```

* * *

## <a name="next-steps"></a>后续步骤

如果您允许用户从任务模块中向后发送响应，则需要处理提交操作。

* [使用任务模块创建和响应](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
