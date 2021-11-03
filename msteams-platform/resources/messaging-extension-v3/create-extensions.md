---
title: 使用消息传递扩展启动操作
description: 创建基于操作的消息扩展以允许用户触发外部服务
ms.localizationpriority: medium
ms.topic: how-to
keywords: teams 邮件扩展邮件扩展搜索
ms.openlocfilehash: 56dcf316eb430b9745856469eaf837ffe7c0bc00
ms.sourcegitcommit: 22c9e44437720d30c992a4a3626a2a9f745983c1
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/03/2021
ms.locfileid: "60720377"
---
# <a name="initiate-actions-with-messaging-extensions"></a>使用消息传递扩展启动操作

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

基于操作的消息扩展允许你的用户在外部服务中Teams。

![邮件扩展卡示例](~/assets/images/compose-extensions/ceexample.png)

以下各节介绍如何执行下列操作：

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a>操作类型邮件扩展

若要从邮件扩展启动操作，将 `type` 参数设置为 `action` 。 下面是一个使用搜索和创建命令的清单示例。 单个邮件扩展最多可以有 10 个不同的命令。 这可包括多个搜索和多个基于操作的命令。

#### <a name="complete-app-manifest-example"></a>完整的应用清单示例

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",
  "manifestVersion": "1.5",
  "version": "1.0",
  "id": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
  "packageName": "com.microsoft.teams.samples.Todo",
  "developer": {
    "name": "John Developer",
    "websiteUrl": "http://todobotservice.azurewebsites.net/",
    "privacyUrl": "http://todobotservice.azurewebsites.net/privacy",
    "termsOfUseUrl": "http://todobotservice.azurewebsites.net/termsofuse"
  },
  "name": {
    "short": "To Do",
    "full": "To Do"
  },
  "description": {
    "short": "Find or create a new task in To Do",
    "full": "Find or create a new task in To Do"
  },
  "icons": {
    "outline": "todo-outline.jpg",
    "color": "todo-color.jpg"
  },
  "accentColor": "#ff6a00",
  "composeExtensions": [
    {
      "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
      "canUpdateConfiguration": true,
      "commands": [
        {
          "id": "searchCmd",
          "description": "Search you Todo's",
          "title": "Search",
          "initialRun": true,
          "context": ["commandBox", "compose"],
          "parameters": [
            {
              "name": "searchKeyword",
              "description": "Enter your search keywords",
              "title": "Keywords"
            }
          ]
        },
        {
          "id": "addTodo",
          "description": "Create a To Do item",
          "title": "Create To Do",
          "type": "action",
          "context": ["commandBox", "message", "compose"],
          "parameters": [
            {
              "name": "Name",
              "description": "To Do Title",
              "title": "Title",
              "inputType": "text"
            },
            {
              "name": "Description",
              "description": "Description of the task",
              "title": "Description",
              "inputType": "textarea"
            },
            {
              "name": "Date",
              "description": "Due date for the task",
              "title": "Date",
              "inputType": "date"
            }
          ]
        },
        {
          "id": "reassignTodo",
          "description": "Reassign a todo item",
          "title": "Reassign a todo item",
          "type": "action",
          "fetchTask": true,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
            }
          ]
        }
      ]
    }
  ],
  "permissions": [
    "identity",
    "messageTeamMembers"
  ],
  "validDomains": [
    "todobotservice.azurewebsites.net",
    "*.todobotservice.azurewebsites.net"
  ]
}
```

### <a name="initiate-actions-from-messages"></a>从邮件启动操作

除了从撰写邮件区域启动操作之外，您还可以使用邮件扩展从邮件启动操作。 这将允许你将邮件内容发送到自动程序进行处理，并可以选择使用 方法通过 响应回复消息，如响应以 [提交 中所述](#responding-to-submit)。 该响应将作为回复插入，您的用户可以在提交之前编辑该邮件。 你的用户可以从溢出菜单访问消息传递扩展 `...` ，然后选择 `Take action` 如下图所示：

![从邮件启动操作的示例](~/assets/images/compose-extensions/messageextensions_messageaction.png)

若要使邮件扩展从邮件中工作，请向应用清单中的邮件扩展对象添加 参数， `context` `commands` 如以下示例所示。 数组的有效 `context` 字符串是 `"message"` 、 `"commandBox"` 和 `"compose"` 。 默认值为 `["compose", "commandBox"]`。 有关 [参数的完整详细信息](#define-commands) ，请参阅定义命令 `context` 部分：

```json
"composeExtensions": [
  {
    "botId": "57a3c29f-1fc5-4d97-a142-35bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Create To Do",
        "type": "Action",
        "context": ["message"],
        "fetchTask": true
    }]
    ...

```

下面是包含将在请求中发送的消息详细信息的对象示例，这些详细信息将 `value` `composeExtension` 发送给自动程序。

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
        "content": "this is the message"
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

### <a name="test-via-uploading"></a>通过上传进行测试

可以通过上传应用来测试邮件扩展。 有关详细信息，请参阅在团队 [中上传应用](~/concepts/deploy-and-publish/apps-upload.md)。

若要打开消息扩展，请导航到任何聊天或频道。 在撰写 **框中** 选择" (&#8943;) "按钮，然后选择邮件扩展。 

## <a name="collecting-input-from-users"></a>收集用户输入

有三种方法可以收集最终用户在 Teams。

### <a name="static-parameter-list"></a>静态参数列表

在此方法中，只需在清单中定义一个静态参数列表，如"Create 微软待办"命令所示。 若要使用此方法， `fetchTask` 请确保设置为 `false` ，并确保在清单中定义参数。

当用户选择具有静态参数的命令时，Teams将在任务模块中生成一个包含清单中定义的参数的窗体。 点击提交时 `composeExtension/submitAction` ，会向自动程序发送 。 有关预期响应集详细信息，请参阅 [响应以提交](#responding-to-submit)。

### <a name="dynamic-input-using-an-adaptive-card"></a>使用自适应卡片的动态输入

在此方法中，你的服务可以定义一个自定义自适应卡片来收集用户输入。 对于此方法，在 `fetchTask` 清单中将 `true` 参数设置为 。 如果设置为 `fetchTask` ， `true` 将忽略为命令定义的任何静态参数。

在此方法中，你的服务接收事件， `composeExtension/fetchTask` 并响应基于自适应卡片 [的任务模块响应](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)。 下面是包含自适应卡片的示例响应：

```json
{
    "task": {
        "type": "continue",
        "value": {
            "card": {
                "contentType": "application/vnd.microsoft.card.adaptive",
                "content": {
                    "body": [
                        {
                            "type": "TextBlock",
                            "text": "Please enter the following information:"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Name"
                        },
                        {
                            "type": "Input.Text",
                            "spacing": "None",
                            "title": "New Input.Toggle",
                            "placeholder": "Placeholder text"
                        },
                        {
                            "type": "TextBlock",
                            "text": "Date of birth"
                        },
                        {
                            "type": "Input.Date",
                            "spacing": "None",
                            "title": "New Input.Toggle"
                        }
                    ],
                    "type": "AdaptiveCard",
                    "$schema": "http://adaptivecards.io/schemas/adaptive-card.json",
                    "version": "1.0"
                }
            }
        }
    }
}
```

如果用户在获取用户输入之前需要验证或配置扩展，机器人也可以响应身份验证/配置响应。

### <a name="dynamic-input-using-a-web-view"></a>使用 Web 视图的动态输入

在此方法中，你的服务可以显示一 `<iframe>` 个基于小部件以显示任何自定义 UI 并收集用户输入。 对于此方法，在 `fetchTask` 清单中将 `true` 参数设置为 。

就像在自适应卡片流中一样，你的服务发送 `fetchTask` 事件，并响应基于 URL [的任务模块响应](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)。 下面是包含自适应卡片的示例响应：

```json
{
    "task": {
        "value": {
            "url": "http://mywebapp.com/input"
        },
        "type": "continue"
    }
}
```

### <a name="request-to-install-your-conversational-bot"></a>请求安装对话机器人

如果你的应用包含对话机器人，请确保它在加载任务模块之前安装在对话中。 在需要获取任务模块的其他上下文的情况下，这非常有用。 例如，您可能需要获取名单以填充人员选取器控件或团队中的频道列表。

为便于此流，当消息扩展首先收到调用检查以查看当前上下文中是否 `composeExtension/fetchTask` 安装了自动程序时。 您可以通过尝试获取名单呼叫获得此要求。 例如，如果未安装自动程序，则返回自适应卡片以及请求用户安装自动程序的操作。 用户需要有权在位置安装应用。 如果无法安装，邮件会提示与管理员联系。

下面是一个响应示例：

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

用户完成安装后，机器人将收到另一条使用 和 的调用 `name = composeExtension/submitAction` 消息 `value.data.msteams.justInTimeInstall = true` 。

下面是一个调用示例：

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

使用与已安装自动程序时响应的相同任务响应响应调用。

## <a name="responding-to-submit"></a>响应提交

用户完成输入后，机器人将收到一个包含命令 ID 和参数值 `composeExtension/submitAction` 设置的事件。

这些是对 的不同预期响应 `submitAction` 。

### <a name="task-module-response"></a>任务模块响应

当扩展需要将对话框链接在一起以了解更多信息时，会使用此功能。 该响应与前面提到的 `fetchTask` 完全相同。

### <a name="compose-extension-authconfig-response"></a>撰写扩展身份验证/配置响应

当扩展需要进行身份验证或配置为继续时，会使用此功能。 有关详细信息，请参阅搜索 [部分](~/resources/messaging-extension-v3/search-extensions.md#authentication) 中的身份验证部分。

### <a name="compose-extension-result-response"></a>撰写扩展结果响应

此命令用于将卡片作为命令的结果插入到撰写框中。 该响应与搜索命令中使用的响应相同，但仅限于数组中的一个卡片或一个结果。

```json
{
  "composeExtension": {
    "type": "result",
    "attachmentLayout": "list",
    "preview": {
          "contentType": "application/vnd.microsoft.card.thumbnail",
          "content": {
            "title": "85069: Create a cool app",
            "images": [
              {
                "url": "https://placekitten.com/200/200"
              }
            ]
          }
        },
    "attachments": [
      {  
        "contentType": "application/vnd.microsoft.teams.card.o365connector",
        "content": {
          "sections": [
            {
              "activityTitle": "[85069]: Create a cool app",
              "activityImage&quot;: &quot;https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value&quot;: &quot;[Larry Brown](mailto:larryb@example.com)"
                },
                {
                  "name": "State:",
                  "value": "Active"
                }
              ]
            }
          ]
        }
      }
    ]
  }
}
```

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a>使用从自动程序发送的自适应卡片消息进行响应

使用自动程序将带自适应卡片的消息插入频道，以响应提交操作。 你的用户可以在提交邮件之前预览它，并可能编辑/与之交互。 在需要先从用户收集信息，然后再创建自适应卡片响应的情况下，这非常有用。 以下方案演示如何使用此流配置轮询，而无需在频道消息中包括配置步骤。

1. 用户选择消息扩展以触发任务模块。
1. 用户使用任务模块配置轮询。
1. 提交配置任务模块后，应用将使用任务模块中提供的信息制作自适应卡片并将其作为 `botMessagePreview` 响应发送给客户端。
1. 然后，用户可以预览自适应卡片消息，然后机器人将其插入频道。 如果机器人不是频道成员，单击 `Send` 将添加机器人。
1. 与自适应卡片交互将更改消息，然后再发送它。
1. 用户选择后 `Send` ，机器人会向频道发布消息。

若要启用此流，任务模块应做出响应，如以下示例所示，这会向用户显示预览消息。

>[!Note]
>必须 `activityPreview` 包含正好包含 `message` 1 个自适应卡片附件的活动。

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

现在，邮件扩展需要响应两种新类型的交互， `value.botMessagePreviewAction = "send"` `value.botMessagePreviewAction = "edit"` 和 。 下面是需要 `value` 处理的对象的示例：

```json
{
  "name": "composeExtension/submitAction",
  "type": "invoke",
  "conversation": { "id": "19:c366b75791784100b6e8b515fd55b063@thread.skype" },
  "imdisplayname": "Pranav Smith",
  ...
  "value": {
    "botMessagePreviewAction": "send" | "edit",
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

响应请求时，应该使用填充了用户已提交信息的值 `edit` `task` 的响应进行响应。 响应请求时，应该向包含最终自适应卡片的频道 `send` 发送消息。

# <a name="typescriptnodejs"></a>[TypeScript/Node.js](#tab/typescript)

```typescript
teamChatConnector.onComposeExtensionSubmitAction((
    event: builder.IEvent,
    request: teamBuilder.IComposeExtensionActionCommandRequest,
    callback: (err: Error, result: any, statusCode: number) => void) => {
        let invokeValue = (<any> event).value;

        if (invokeValue.botMessagePreviewAction ) {
            let attachment = invokeValue.botActivityPreview[0].attachments[0];

            if (invokeValue.botMessagePreviewAction === 'send') {
                let msg = new builder.Message()
                    .address(event.address)
                    .addAttachment(attachment);
                teamChatConnector.send([msg.toMessage()],
                    (error) => {
                        if(error){
                            //TODO: Handle error and callback
                        }
                        else {
                            callback(null, null, 200);
                        }
                    }
                );
            }

            else if (invokeValue.botMessagePreviewAction === 'edit') {
              // Create the card and populate with user-inputted information
              let card = { ... }

              let taskResponse = {
                task: {
                  type: "continue",
                  value: {
                    title: "Card Preview",
                    card: {
                      contentType: 'application/vnd.microsoft.card.adaptive',
                      content: card
                    }
                  }
                }
              }
              callback(null, taskResponse, 200);
            }

        else {
            let attachment = {
                  //create adaptive card
                };
            let activity = new builder.Message().addAttachment(attachment).toMessage();
            let response = teamBuilder.ComposeExtensionResponse.messagePreview()
                .preview(activity)
                .toResponse();
            callback(null, response, 200);
        }
    });
```

# <a name="cnet"></a>[C#/.NET](#tab/dotnet)

此示例使用[Microsoft.Bot.Connector.Teams SDK (v3) 。 ](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)

```csharp
public class MessagesController : ApiController
{

    [BotAuthentication]
    public async Task<HttpResponseMessage> Post([FromBody]Activity activity)
    {
        MicrosoftAppCredentials.TrustServiceUrl(activity.ServiceUrl, DateTime.MaxValue);
        ConnectorClient connectorClient = new ConnectorClient(
            new Uri(activity.ServiceUrl),
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppIdKey],
            ConfigurationManager.AppSettings[MicrosoftAppCredentials.MicrosoftAppPasswordKey]);

        if (activity.Type == ActivityTypes.Invoke)
        {
            // Initial task module presented to the user
            if (activity.Name == "composeExtension/fetchTask")
            {
                string task = GetTaskModule();

                return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
            }
            else if (activity.Name == "composeExtension/submitAction")
            {
                dynamic activityValue = JObject.FromObject(activity.Value);
                string botMessagePreviewAction = activityValue["botMessagePreviewAction"];

                //This is the initial card response sent after the task module is submitted
                if (botMessagePreviewAction is null)
                {
                    string text = activityValue.data.cardMessage;

                    AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "This card will be inserted into the conversation by the bot.",
                        Size = AdaptiveTextSize.Large,
                        Wrap = true
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = "The text below is what you provided."
                    });
                    card.Body.Add(new AdaptiveTextBlock()
                    {
                        Text = text,
                    });

                    string cardJson = card.ToJson();

                    string cardMessage = $@"{{
                        'composeExtension': {{
                        'type': 'botMessagePreview',
                        'activityPreview': {{
                            'type': 'message',
                            'attachments': [{{
                                'contentType': 'application/vnd.microsoft.card.adaptive',
                                'content': {cardJson}
                            }}]
                        }}
                        }}
                    }}";

                    JObject res = JObject.Parse(cardMessage);
                    return Request.CreateResponse(HttpStatusCode.OK, res);

                }
                else
                {
                    //This is the "send the card to the channel" event
                    if (botMessagePreviewAction.Equals("send"))
                    {
                        string cardJson = JsonConvert.SerializeObject(activityValue.botActivityPreview[0].attachments[0].content);

                        AdaptiveCardParseResult cardResult = AdaptiveCard.FromJson(cardJson);
                        AdaptiveCard card = cardResult.Card;
                        Attachment cardAttachment = new Attachment
                        {
                            ContentType = AdaptiveCard.ContentType,
                            Content = card
                        };


                        Activity response = activity.CreateReply();
                        response.Attachments.Add(cardAttachment);

                        var result = await connectorClient.Conversations.SendToConversationAsync(response);
                    }
                    //This is fired if the user edits the card before sending it
                    else if (botMessagePreviewAction.Equals("edit"))
                    {
                        string task = GetTaskModule();

                        return Request.CreateResponse(HttpStatusCode.OK, JObject.Parse(task));
                    }
                    else
                    {
                        return Request.CreateResponse(HttpStatusCode.NotImplemented);
                    }
                }
            }
        }

        return Request.CreateResponse(HttpStatusCode.NotImplemented);

    }

    private static string GetTaskModule()
    {
        AdaptiveCard card = new AdaptiveCard(new AdaptiveSchemaVersion("1.0"));
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Please enter the following information:",
            Size = AdaptiveTextSize.Large
        });
        card.Body.Add(new AdaptiveTextBlock()
        {
            Text = "Card Message:"
        });
        card.Body.Add(new AdaptiveTextInput()
        {
            Id = "cardMessage",
            Spacing = AdaptiveSpacing.None,
            Placeholder = "Card message goes here."
        });
        card.Actions.Add(new AdaptiveSubmitAction()
        {
            Title = "Submit"
        });

        string cardJson = card.ToJson();

        //Create the task module response
        string task = $@"{{
                            'task': {{
                                'type': 'continue',
                                'value': {{
                                    'card': {{
                                        'contentType': 'application/vnd.microsoft.card.adaptive',
                                        'content': {cardJson}
                                        }}
                                    }}
                                }}
                            }}";
        return task;
    }

}
```

## <a name="see-also"></a>另请参阅

[Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
