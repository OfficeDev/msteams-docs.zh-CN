---
title: 使用消息扩展启动操作
description: 创建基于操作的消息扩展，以允许用户触发外部服务
ms.localizationpriority: medium
ms.topic: how-to
keywords: teams 消息扩展消息扩展搜索
ms.openlocfilehash: a29d1a5b49845d930ac4efbdd3967bd6b4446891
ms.sourcegitcommit: 0117c4e750a388a37cc189bba8fc0deafc3fd230
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65104364"
---
# <a name="initiate-actions-with-message-extensions"></a>使用消息扩展启动操作

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

基于操作的消息扩展允许用户在Teams时触发外部服务中的操作。

![消息扩展卡的示例](~/assets/images/compose-extensions/ceexample.png)

以下部分介绍如何执行此操作：

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

## <a name="action-type-message-extensions"></a>操作类型消息扩展

若要从消息扩展启动操作，请将 `type` 参数设置为 `action`。 下面是包含搜索和创建命令的清单示例。 单个消息扩展最多可以有 10 个不同的命令。 这可以包括多个搜索和多个基于操作的命令。

### <a name="complete-app-manifest-example"></a>完整的应用清单示例

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
          "fetchTask": false,
          "parameters": [
            {
              "name": "Name",
              "title": "Title"
              "inputType": "text"
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

### <a name="initiate-actions-from-messages"></a>从消息启动操作

除了从撰写消息区域启动操作外，还可以使用消息扩展从消息启动操作。 这将允许您将消息内容发送到机器人进行处理，并可选择性地使用“ [响应提交](#responding-to-submit)”中所述的方法使用响应回复该消息。 响应将作为对用户在提交前可以编辑的消息的答复进行插入。 用户可以从溢出 `...` 菜单访问消息扩展，然后选择 `Take action` 如下图所示：

![从消息启动操作的示例](~/assets/images/compose-extensions/messageextensions_messageaction.png)

若要使消息扩展能够从消息中工作，请在应用清单中将参数添加 `context` 到消息扩展的 `commands` 对象，如以下示例所示。 数组的`context`有效字符串包括`"message"`和 `"commandBox"``"compose"`。 默认值为 `["compose", "commandBox"]`。 有关参数的完整详细信息`context`，请参阅[“定义命令](#define-commands)”部分：

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

下面是包含将作为请求的一部分发送到机器人的消息详细信息的`composeExtension`对象的示例`value`。

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

可以通过上传应用来测试消息扩展。 有关详细信息，请参阅在 [团队中上传应用](~/concepts/deploy-and-publish/apps-upload.md)。

若要打开邮件扩展插件，请导航到任何聊天或频道。 在撰写框中选择“ **更多”选项** **(&#8943;**) 按钮，然后选择邮件扩展。

## <a name="collecting-input-from-users"></a>从用户收集输入

可通过三种方式从Teams中的最终用户收集信息。

### <a name="static-parameter-list"></a>静态参数列表

在此方法中，只需在清单中定义参数的静态列表，如上面的“创建微软待办”命令中所示。 若要使用此方法，请确保 `fetchTask` 设置为 `false` 并在清单中定义参数。

当用户选择具有静态参数的命令时，Teams将在任务模块中生成一个表单，其中包含清单中定义的参数。 点击“提交”时，将向机器人发送一个 `composeExtension/submitAction` 。 有关预期响应集的详细信息，请参阅 [“响应提交](#responding-to-submit)”。

### <a name="dynamic-input-using-an-adaptive-card"></a>使用自适应卡片的动态输入

在此方法中，服务可以定义自定义自适应卡来收集用户输入。 对于此方法，请将 `fetchTask` 参数设置为 `true` 清单中。 如果设置， `fetchTask` `true` 则将忽略为该命令定义的任何静态参数。

在此方法中，服务接收 `composeExtension/fetchTask` 事件并使用基于自适应卡 [的任务模块响应进行响应](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)。 下面是带有自适应卡片的示例响应：

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

如果用户需要在获取用户输入之前对扩展进行身份验证或配置，则机器人还可以使用身份验证/配置响应进行响应。

### <a name="dynamic-input-using-a-web-view"></a>使用 Web 视图的动态输入

在此方法中，服务可以显示基于 `<iframe>` 小组件以显示任何自定义 UI 并收集用户输入。 对于此方法，请将 `fetchTask` 参数设置为 `true` 清单中。

就像在自适应卡流中一 `fetchTask` 样，服务发送事件并使用基于 URL [的任务模块响应进行响应](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)。 下面是带有自适应卡片的示例响应：

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

### <a name="request-to-install-your-conversational-bot"></a>请求安装聊天机器人

如果应用包含会话机器人，请确保在加载任务模块之前将其安装在会话中。 在需要获取任务模块的其他上下文的情况下，这很有用。 例如，可能需要提取名册以填充人员选取器控件或团队中的频道列表。

为了便于此流，当消息扩展首次收到 `composeExtension/fetchTask` 调用检查以查看机器人是否安装在当前上下文中时。 你可以通过尝试获取名册呼叫来获取此数据。 例如，如果未安装机器人，则返回自适应卡片，其中包含请求用户安装机器人的操作。 用户需要有权在该位置安装应用。 如果无法安装，则消息会提示与管理员联系。

下面是响应的示例：

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

一旦用户完成安装，机器人将收到另一条调用 `name = composeExtension/submitAction`消息，其中包含和 `value.data.msteams.justInTimeInstall = true`。

下面是调用的示例：

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

如果机器人已安装，则使用相同的任务响应响应响应调用。

## <a name="responding-to-submit"></a>响应提交

用户完成输入后，机器人将收到命令 `composeExtension/submitAction` ID 和参数值设置的事件。

这些是预期对 a `submitAction`的不同反应。

### <a name="task-module-response"></a>任务模块响应

当扩展需要将对话链接在一起以获取详细信息时，将使用此功能。 响应与前面提到的完全相同 `fetchTask` 。

### <a name="compose-extension-authconfig-response"></a>撰写扩展身份验证/配置响应

当扩展需要进行身份验证或配置以继续时，将使用此功能。 有关详细信息，请参阅搜索 [部分中的身份验证部分](~/resources/messaging-extension-v3/search-extensions.md#authentication) 。

### <a name="compose-extension-result-response"></a>撰写扩展结果响应

这用于将卡片作为命令的结果插入撰写框中。 它与搜索命令中使用的响应相同，但它仅限于数组中的一张卡片或一个结果。

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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a>使用从机器人发送的自适应卡片消息进行响应

通过使用机器人将带有自适应卡片的消息插入通道来响应提交操作。 用户可以在提交邮件之前预览消息，也可以编辑/与之交互。 在创建自适应卡片响应之前需要从用户收集信息的方案中，这很有用。 以下方案演示如何使用此流在不包含频道消息中的配置步骤的情况下配置轮询。

1. 用户选择消息扩展以触发任务模块。
1. 用户使用任务模块来配置轮询。
1. 提交配置任务模块后，应用使用任务模块中提供的信息来制作自适应卡片，并将其作为 `botMessagePreview` 响应发送给客户端。
1. 然后，用户可以在机器人将其插入通道之前预览自适应卡片消息。 如果机器人不是通道的成员，单击 `Send` 将添加机器人。
1. 与自适应卡片交互会在发送消息之前更改消息。
1. 用户选择 `Send` 后，机器人会将消息发布到通道。

若要启用此流，任务模块应响应，如下面的示例所示，该示例将向用户显示预览消息。

>[!Note]
>该 `activityPreview` 活动必须包含完全包含 1 个 `message` 自适应卡片附件的活动。

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

你的消息扩展现在需要响应两种新类型的交互， `value.botMessagePreviewAction = "send"` 以及 `value.botMessagePreviewAction = "edit"`。 下面是需要处理的 `value` 对象的示例：

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

响应 `edit` 请求时，应使用包含用户已提交的信息填充的值的响应进行响应 `task` 。 响应 `send` 请求时，应向包含最终自适应卡片的通道发送一条消息。

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

此示例使用 [Microsoft.Bot.Connector.Teams 显示此流SDK (v3) ](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)。

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
