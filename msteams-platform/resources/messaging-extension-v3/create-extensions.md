---
title: 使用邮件扩展启动操作
description: 创建基于操作的消息扩展以允许用户触发外部服务
keywords: 工作组邮件传递扩展邮件扩展搜索
ms.openlocfilehash: 9b7d3bd53ba45d55e80f858a3c89be265c13482b
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673285"
---
# <a name="initiate-actions-with-messaging-extensions"></a>使用邮件扩展启动操作

[!include[v3-to-v4-SDK-pointer](~/includes/v3-to-v4-pointer-me.md)]

基于操作的消息传递扩展使用户能够在团队内触发外部服务中的操作。

![邮件扩展卡的示例](~/assets/images/compose-extensions/ceexample.png)

以下各节介绍如何执行此操作。

[!include[Common content for creating extensions](~/includes/messaging-extensions/messaging-extensions-common.md)]

### <a name="action-type-message-extensions"></a>操作类型邮件扩展名

若要从邮件扩展启动操作，请`type`将参数`action`设置为。 下面是一个带有搜索和创建命令的清单示例。 单个邮件传递分机最长可包含10个不同的命令。 这可以包括多个搜索和多个基于操作的命令。

#### <a name="complete-app-manifest-example"></a>完整的应用程序清单示例

```json
{
  "$schema": "https://developer.microsoft.com/json-schemas/teams/v1.5/MicrosoftTeams.schema.json",
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

### <a name="initiate-actions-from-messages"></a>从邮件中启动操作

除了从撰写邮件区域中启动操作之外，还可以使用邮件扩展从邮件中启动操作。 这将允许您将邮件的内容发送到你的 bot 以进行处理，还可以选择使用响应[提交](#responding-to-submit)中所述的方法，使用响应答复该邮件。 响应将作为回复插入到您的用户可以在提交前编辑的邮件。 您的用户可以从 "溢出`...` " 菜单访问您的邮件扩展`Take action` ，然后选择下面的图像中的 "as"。

![从邮件中启动操作的示例](~/assets/images/compose-extensions/messageextensions_messageaction.png)

若要使邮件扩展能够从邮件中运行，您需要将`context`参数添加到应用程序清单中的`commands`邮件扩展的对象，如下例所示。 `context`数组的有效字符串为`"message"`、 `"commandBox"`和`"compose"`。 默认值为 `["compose", "commandBox"]`。 有关`context`参数的完整详细信息，请参阅 "[定义命令](#define-commands)" 部分。

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

下面是一个`value`对象的示例，其中包含将作为`composeExtension`请求的一部分发送到你的 bot 的邮件详细信息。

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

您可以通过上载您的应用程序来测试您的邮件扩展。 有关详细信息，请参阅[在团队中上传你的应用](~/concepts/deploy-and-publish/apps-upload.md)。

若要打开邮件扩展插件，请导航到任何聊天或频道。 选择 "撰写" 框中的 "**更多选项**（**&#8943;**）" 按钮，然后选择您的邮件扩展。

## <a name="collecting-input-from-users"></a>收集用户的输入

有三种方法可以从工作组中的最终用户处收集信息。

### <a name="static-parameter-list"></a>静态参数列表

在此方法中，您只需定义清单中的参数的静态列表，如上面的 "创建任务" 命令中所示。 若要使用此方法`fetchTask` ，请确保`false`设置为，并在清单中定义参数。

当用户选择带有静态参数的命令时，团队将在任务模块中使用清单中定义的参数生成窗体。 在 "命中提交`composeExtension/submitAction` a" 发送到机器人。 有关预期响应集的详细信息，请参阅主题[响应提交](#responding-to-submit)。

### <a name="dynamic-input-using-an-adaptive-card"></a>使用自适应卡片的动态输入

在此方法中，服务可以定义自定义的自适应卡片以收集最终用户输入。 对于此方法，请在`fetchTask`清单中`true`将参数设置为。 请注意，如果您`fetchTask`设置`true`为将忽略为命令定义的任何静态参数。

在此方法中，服务将接收`composeExtension/fetchTask`事件，并需要使用基于自适应卡的[任务模块响应](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)进行响应。 以下是使用自适应卡片的示例响应：

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

如果用户需要在获取用户输入之前对扩展进行身份验证或配置，则 bot 还可以通过身份验证/配置响应进行响应。

### <a name="dynamic-input-using-a-web-view"></a>使用 web 视图的动态输入

在此方法中，您的服务`<iframe>`可以显示一个基于的小部件，以显示任何自定义 UI 并收集用户输入。 对于此方法，请在`fetchTask`清单中`true`将参数设置为。

就像在自适应卡流中，您的服务将`fetchTask`发送事件并需要使用基于 URL 的[任务模块响应](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)进行响应。 以下是使用自适应卡片的示例响应：

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

如果您的应用程序还包含一个对话机器人，则可能需要确保在加载任务模块之前在对话中安装你的 bot。 在需要获取任务模块的其他上下文的情况下，这可能很有用。 例如，您可能需要提取名单以填充 "人员选取器" 控件或团队中的频道列表。

若要简化此流程，当邮件扩展程序首次`composeExtension/fetchTask`收到调用检查以查看您的 bot 是否已安装在当前上下文中时（例如，您可以通过尝试 get 名单调用来实现此目的）。 如果未安装你的 bot，请返回一个自适应卡片，其中包含一个请求用户安装你的 bot 的操作。请参阅下面的示例。 请注意，这要求用户具有在该位置安装应用程序的权限;如果不能，他们将看到一条消息，询问用户是否与管理员联系。

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

一旦用户完成安装，你的 bot 将收到另一条带`name = composeExtension/submitAction`和`value.data.msteams.justInTimeInstall = true`的 invoke 消息。

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

您应使用与您进行响应的相同任务响应来响应此调用（如果已经安装了 bot）。

## <a name="responding-to-submit"></a>响应提交

用户完成输入后，你的 bot 将接收到设置`composeExtension/submitAction`了命令 id 和参数值的事件。

这些是对的`submitAction`预期的不同响应。

### <a name="task-module-response"></a>任务模块响应

当您的扩展需要将对话框链接在一起以获取详细信息时，将使用此信息。 响应与前面`fetchTask`提到的完全相同。

### <a name="compose-extension-authconfig-response"></a>撰写扩展身份验证/配置响应

当扩展需要进行身份验证或配置以便继续时，使用此方法。 有关详细信息，请参阅 "搜索" 部分中的 "[身份验证" 部分](~/resources/messaging-extension-v3/search-extensions.md#authentication)。

### <a name="compose-extension-result-response"></a>撰写扩展结果响应

这用于将一个卡片作为命令插入到撰写框中。 它与搜索命令中使用的响应相同，但仅限于一个卡片或阵列中的一个结果。

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
              "activityImage": "https://placekitten.com/200/200"
            },
            {
              "title": "Details",
              "facts": [
                {
                  "name": "Assigned to:",
                  "value": "[Larry Brown](mailto:larryb@example.com)"
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

### <a name="respond-with-an-adaptive-card-message-sent-from-a-bot"></a>使用从 bot 发送的自适应卡片邮件进行响应

您还可以通过将带有自适应卡片的邮件插入到使用 bot 的频道中来响应提交操作。 你的用户将能够在提交邮件之前预览邮件，并可能对其进行编辑/与之交互。 这在您需要在创建自适应卡片响应之前从用户处收集信息的情况下可能非常有用。 下面的方案演示如何使用此流配置轮询，而不在通道消息中包括配置步骤。

1. 用户单击邮件扩展可触发任务模块。
1. 用户使用任务模块配置轮询。
1. 提交配置任务模块后，应用使用任务模块中提供的信息来创建自适应卡片，并将其作为对客户`botMessagePreview`端的响应发送。
1. 然后，用户可以预览自适应卡片邮件，然后 bot 将其插入频道中。 如果 bot 尚不是频道的成员，则单击`Send` "" 将添加机器人。
1. 与自适应卡片进行交互将会在发送邮件之前对其进行更改。
1. 用户单击`Send` bot 后，会将邮件发送到频道。

若要启用此流，您的任务模块应如下面的示例所示进行响应，这将向用户显示预览邮件。

>[!Note]
>`activityPreview`必须包含一个`message`只有1个自适应卡片附件的活动。

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

您的邮件扩展现在需要对两种新类型的交互`value.botMessagePreviewAction = "send"`和`value.botMessagePreviewAction = "edit"`进行响应。 下面是需要处理的`value`对象的示例：

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

响应`edit`请求时，应`task`响应，其中包含以用户已提交的信息填充的值。 响应`send`请求时，应向包含最终的自适应卡的频道发送一封邮件。

# <a name="typescriptnodejstabtypescript"></a>[TypeScript/node.js](#tab/typescript)

下面的示例展示了如何使用[Node.js 团队 Bot 生成器 SDK](https://www.npmjs.com/package/botbuilder-teams)执行此操作。

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

# <a name="cnettabdotnet"></a>[C #/.NET](#tab/dotnet)

此示例演示如何使用[Microsoft Bot. 团队 SDK （v3）](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)进行传输。

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
