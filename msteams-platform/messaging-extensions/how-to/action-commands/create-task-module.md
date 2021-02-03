---
title: 创建并发送任务模块
author: clearab
description: 如何处理初始调用操作以及从操作消息扩展命令使用任务模块进行响应
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 58fb7e1ff5690b33c2e23f68529f05869afa9016
ms.sourcegitcommit: ce74f821660b1258c72b3c3f71c1cf177e7e92ef
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/02/2021
ms.locfileid: "50072873"
---
# <a name="create-and-send-the-task-module"></a>创建并发送任务模块

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

如果未使用应用清单中定义的参数填充任务模块，则必须为用户创建任务模块。 使用自适应卡片或嵌入式 Web 视图。

## <a name="the-initial-invoke-request"></a>初始调用请求

使用此方法，你的服务将收到一个类型对象，并且必须使用包含自适应卡片或嵌入 Web 视图 `Activity` `composeExtension/fetchTask` 的 URL `task` 的对象进行响应。 除了标准自动程序活动属性外，初始调用负载还包含以下请求元数据：

|属性名称|用途|
|---|---|
|`type`| 请求的类型。 它必须是 `invoke` 。 |
|`name`| 向服务发出的命令类型。 它必须是 `composeExtension/fetchTask` 。 |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| 发送请求的用户的 Azure Active Directory 对象 ID。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.channel.id`| 如果在 (通道中提出请求，通道 ID 将) 。 |
|`channelData.team.id`| 如果 (频道中提出请求，团队 ID) 。 |
|`value.commandId` | 包含已调用的命令的 ID。 |
|`value.commandContext` | 触发事件的上下文。 它必须是 `compose` 。 |
|`value.context.theme` | 用户的客户端主题，可用于嵌入 Web 视图格式。 它必须是 `default` ， `contrast` 或 `dark` 。 |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-11-chat-are-listed-in-the-following-section"></a>以下部分列出了从 1：1 聊天调用任务模块时的有效负载活动属性：

|属性名称|用途|
|---|---|
|`type`| 请求的类型。 它必须是 `invoke` 。 |
|`name`| 向服务发出的命令类型。 它必须是 `composeExtension/fetchTask` 。 |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| 发送请求的用户的 Azure Active Directory 对象 ID。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.source.name`| 调用任务模块的源名称。 |
|`ChannelData.legacy. replyToId`| 获取或设置此邮件作为回复的邮件的 ID。 |
|`value.commandId` | 包含已调用的命令的 ID。 |
|`value.commandContext` | 触发事件的上下文。 它必须是 `compose` 。 |
|`value.context.theme` | 用户的客户端主题，可用于嵌入 Web 视图格式。 它必须是 `default` ， `contrast` 或 `dark` 。 |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-group-chat-are-listed-in-the-following-section"></a>以下部分列出了从群聊调用任务模块时的有效负载活动属性：

|属性名称|用途|
|---|---|
|`type`| 请求的类型。 它必须是 `invoke` 。 |
|`name`| 向服务发出的命令类型。 它必须是 `composeExtension/fetchTask` 。 |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| 发送请求的用户的 Azure Active Directory 对象 ID。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.source.name`| 调用任务模块的源名称。 |
|`ChannelData.legacy. replyToId`| 获取或设置此邮件作为回复的邮件的 ID。 |
|`value.commandId` | 包含已调用的命令的 ID。 |
|`value.commandContext` | 触发事件的上下文。 它必须是 `compose` 。 |
|`value.context.theme` | 用户的客户端主题，可用于嵌入 Web 视图格式。 它必须是 `default` ， `contrast` 或 `dark` 。 |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-new-post-are-listed-in-the-following-section"></a>从频道调用任务模块时， (新帖子) 下一节列出：

|属性名称|用途|
|---|---|
|`type`| 请求的类型。 它必须是 `invoke` 。 |
|`name`| 向服务发出的命令类型。 它必须是 `composeExtension/fetchTask` 。 |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| 发送请求的用户的 Azure Active Directory 对象 ID。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.channel.id`| 如果在 (通道中提出请求，通道 ID 将) 。 |
|`channelData.team.id`| 如果 (频道中提出请求，团队 ID) 。 |
|`channelData.source.name`| 调用任务模块的源名称。 |
|`ChannelData.legacy. replyToId`| 获取或设置此邮件作为回复的邮件的 ID。 |
|`value.commandId` | 包含已调用的命令的 ID。 |
|`value.commandContext` | 触发事件的上下文。 它必须是 `compose` 。 |
|`value.context.theme` | 用户的客户端主题，可用于嵌入 Web 视图格式。 它必须是 `default` ， `contrast` 或 `dark` 。 |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-channel-reply-to-thread-are-listed-in-the-following-section"></a>从频道调用任务模块时， (主题) 将列在以下部分中：

|属性名称|用途|
|---|---|
|`type`| 请求的类型。 它必须是 `invoke` 。 |
|`name`| 向服务发出的命令类型。 它必须是 `composeExtension/fetchTask` 。 |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| 发送请求的用户的 Azure Active Directory 对象 ID。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.channel.id`| 如果在 (通道中提出请求，通道 ID 将) 。 |
|`channelData.team.id`| 如果 (频道中提出请求，团队 ID) 。 |
|`channelData.source.name`| 调用任务模块的源名称。 |
|`ChannelData.legacy. replyToId`| 获取或设置此邮件作为回复的邮件的 ID。 |
|`value.commandId` | 包含已调用的命令的 ID。 |
|`value.commandContext` | 触发事件的上下文。 它必须是 `compose` 。 |
|`value.context.theme` | 用户的客户端主题，可用于嵌入 Web 视图格式。 它必须是 `default` ， `contrast` 或 `dark` 。 |

### <a name="payload-activity-properties-when-invoked-a-task-module-from-a-command-box-are-listed-in-the-following-section"></a>以下部分列出了从命令框调用任务模块时的有效负载活动属性：

|属性名称|用途|
|---|---|
|`type`| 请求的类型。 它必须是 `invoke` 。 |
|`name`| 向服务发出的命令类型。 它必须是 `composeExtension/fetchTask` 。 |
|`from.id`| 发送请求的用户的 ID。 |
|`from.name`| 发送请求的用户的名称。 |
|`from.aadObjectId`| 发送请求的用户的 Azure Active Directory 对象 ID。 |
|`channelData.tenant.id`| Azure Active Directory 租户 ID。 |
|`channelData.source.name`| 调用任务模块的源名称。 |
|`value.commandId` | 包含已调用的命令的 ID。 |
|`value.commandContext` | 触发事件的上下文。 它必须是 `compose` 。 |
|`value.context.theme` | 用户的客户端主题，可用于嵌入 Web 视图格式。 它必须是 `default` ， `contrast` 或 `dark` 。 |

### <a name="example-fetchtask-request"></a>fetchTask 请求示例

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  //handle fetch task
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreviewBot extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    //hand fetch task
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

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

When your bot is invoked from a message rather than the compose area or the command bar， the object in the initial request must contain the details `value` of the message of the message extension is invoked from. 有关此对象的示例，请参阅以下部分。 和数组是可选的，如果原始邮件中没有任何反应或提及，则它们 `reactions` `mentions` 不存在。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

```csharp
protected override async Task<MessagingExtensionActionResponse> OnTeamsMessagingExtensionFetchTaskAsync(ITurnContext<IInvokeActivity> turnContext, MessagingExtensionAction action, CancellationToken cancellationToken)
{
  var messageText = action.MessagePayload.Body.Content;
  var fromId = action.MessagePayload.From.User.Id;

  //finish handling the fetchTask
}
```

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

```javascript
class TeamsMessagingExtensionsActionPreview extends TeamsActivityHandler {
  handleTeamsMessagingExtensionFetchTask(context, action) {
    const messageText = action.messagePayload.body.content;

    //finish handling the fetchTask
  }
}
```

# <a name="json"></a>[JSON](#tab/json)

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

使用包含具有自适应卡片或 Web URL 的对象或简单的字符串消息的对象响应 `task` `taskInfo` 调用请求。

|属性名称|用途|
|---|---|
|`type`| 可以是呈现 `continue` 窗体，也可以 `message` 用于简单的弹出式窗体。 |
|`value`| 窗体 `taskInfo` 的对象或邮件 `string` 的对象。 |

taskInfo 对象的架构为：

|属性名称|用途|
|---|---|
|`title`| 任务模块的标题。|
|`height`| 它必须是一个整数 (以像素为单位) 或 `small` ， `medium` `large` 。|
|`width`| 它必须是一个整数 (以像素为单位) 或 `small` ， `medium` `large` 。|
|`card`| 定义表单的自适应卡片 (使用一个) 。
|`url`| 作为嵌入式 Web 视图在任务模块内打开的 URL。|
|`fallbackUrl`| 如果客户端不支持任务模块功能，则此 URL 在浏览器选项卡中打开。 |

### <a name="with-an-adaptive-card"></a>使用自适应卡片

使用自适应卡片时，必须使用包含自适应卡片的对象响应 `task` `value` 对象。

#### <a name="example-fetchtask-response-with-an-adaptive-card"></a>带自适应卡片的 fetchTask 响应示例

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

此示例除使用 Bot Framework SDK 外，还使用 [AdaptiveCards NuGet](https://www.nuget.org/packages/AdaptiveCards) 程序包。

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

```json
 {
  "task": {
    "type": "continue",
    "value": {
      "title": "Task module title",
      "height": 500,
      "width": "medium",
      "card": {
        "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
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
        ]
      }
    }
  }
}
```

* * *

### <a name="with-an-embedded-web-view"></a>使用嵌入式 Web 视图

使用嵌入式 Web 视图时，必须使用包含要加载的 Web 表单 URL 的对象响应 `task` `value` 对象。 要加载的任何 URL 的域必须包含在应用 `validDomains` 清单的数组中。 有关 [生成嵌入式 Web](~/task-modules-and-cards/what-are-task-modules.md) 视图的完整信息，请参阅任务模块文档。

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

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

# <a name="javascriptnodejs"></a>[JavaScript/Node.js](#tab/javascript)

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

# <a name="json"></a>[JSON](#tab/json)

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

### <a name="request-to-install-your-conversational-bot"></a>请求安装对话机器人

如果应用包含对话机器人，则先在对话中安装自动程序，然后再加载任务模块。 获取任务模块的其他上下文很有用。 此方案的典型示例是提取名单以填充人员选取器控件或团队中的频道列表。

当消息扩展收到调用时，请检查机器人是否安装在当前上下文中以便于 `composeExtension/fetchTask` 流。 例如，使用获取名单呼叫检查流程。 如果未安装自动程序，请返回自适应卡片，并返回一个请求用户安装自动程序的操作。 请参阅以下示例中的操作。 用户必须有权将应用安装在该位置进行检查。 如果应用安装不成功，用户将收到一条消息，联系管理员。

#### <a name="example-of-the-response"></a>响应示例：

```json
{
  "type": "AdaptiveCard",
  "body": [
    {
      "type": "TextBlock",
      "text": "Looks like you haven't used Disco in this team/chat"
    }
  ],
  "actions": [
    {
      "type": "Action.Submit",
      "title": "Continue",
      "data": {
        "msteams": {
          "justInTimeInstall": true
        }
      }
    }
  ],
  "version": "1.0"
}
```

安装后，自动程序会收到另一条调用消息，消息包含 `name = composeExtension/submitAction` 和 `value.data.msteams.justInTimeInstall = true` 。

#### <a name="example-of-the-invoke"></a>调用示例：

```json
{
  "value": {
    "commandId": "giveKudos",
    "commandContext": "compose",
    "context": {
      "theme": "default"
    },
    "data": {
      "msteams": {
        "justInTimeInstall": true
      }
    }
  },
  "conversation": {
    "id": "19:7705841b240044b297123ad7f9c99217@thread.skype"
  },
  "name": "composeExtension/submitAction",
  "imdisplayname": "Bob Smith"
}
```

对调用的任务响应必须类似于已安装的自动程序。

#### <a name="example-of-just-in-time-installation-of-app-with-adaptive-card"></a>使用自适应卡片实时安装应用的示例： 

```csharp
private static Attachment GetAdaptiveCardAttachmentFromFile(string fileName)
  {
      //Read the card json and create attachment.
         string[] paths = { ".", "Resources", fileName };
         var adaptiveCardJson = File.ReadAllText(Path.Combine(paths));
         var adaptiveCardAttachment = new Attachment()
            {
                ContentType = "application/vnd.microsoft.card.adaptive",
                Content = JsonConvert.DeserializeObject(adaptiveCardJson),
            };
            return adaptiveCardAttachment;
        }
```

* * *

## <a name="next-steps"></a>后续步骤

如果允许用户从任务模块发送回响应，则必须处理提交操作。

* [使用任务模块创建和响应](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
