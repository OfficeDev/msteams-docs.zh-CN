---
title: 在自动程序Microsoft Teams模块
description: 如何将任务模块与自动程序Microsoft Teams，包括 Bot Framework 卡、自适应卡片和深层链接
localization_priority: Normal
ms.topic: how-to
keywords: 任务模块团队机器人
ms.openlocfilehash: bfaf3dfe791c1736aeb418e2689e513908f04534
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52566564"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a>使用自动程序Microsoft Teams模块

可以使用自适应卡片和自动程序框架Microsoft Teams上的按钮从自动程序调用任务模块 (Hero、Thumbnail 和 Office 365 Connector) 。 与开发人员必须跟踪机器人状态并允许用户中断/取消序列的多个对话步骤不同，任务模块通常是更好的用户体验。

有两种调用任务模块的方法：

* **一种新的调用消息 `task/fetch` 。** 使用自动程序框架卡片的卡片操作或自适应卡片的卡片操作和 ，任务模块 (URL 或自适应卡片) 从自动程序动态获取 `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` 。
* **深层链接 URL。** 使用[任务模块的](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)深层链接语法，你可以分别使用 Bot Framework 卡片的卡片操作或自适应卡片 `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)的卡片操作。 对于深层链接 URL，任务模块 URL 或自适应卡片正文明显提前已知，以避免相对于 的服务器往返 `task/fetch` 行程。

>[!IMPORTANT]
>为确保安全通信，每个和 `url` `fallbackUrl` 都必须实现 HTTPS 加密协议。

## <a name="invoking-a-task-module-through-taskfetch"></a>通过任务/提取调用任务模块

当卡片操作的对象或以正确的方式初始化时 () 下面进行了详细说明，当用户按下按钮时，会向自动程序 `value` `invoke` `Action.Submit` `invoke` 发送消息。 在消息的 HTTP 响应中，包装器对象中嵌入了一个 `invoke` [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)对象，Teams用于显示任务模块。

![task/fetch request/response](~/assets/images/task-module/task-module-invoke-request-response.png)

让我们更详细地了解一下每个步骤：

1. 本示例显示具有"Buy"卡片操作的 Bot Framework `invoke` [Hero 卡](~/task-modules-and-cards/cards/cards-actions.md#invoke)。 属性的值 `type` 为 `task/fetch` - 对象的其余部分 `value` 可以是您喜欢的任何对象。
1. 机器人接收 HTTP `invoke` POST 消息。
1. 机器人创建响应对象，并返回 HTTP 200 响应代码的 POST 响应正文。 有关任务 [/](#the-flexibility-of-tasksubmit)提交的讨论如下所述响应的架构，但现在要记住的重要一点就是 HTTP 响应的正文包含嵌入包装对象的 [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) 对象。 例如：

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

    从概念上说，事件及其对自动程序的响应与客户端 SDK 中的 `task/fetch` `microsoftTeams.tasks.startTask()` 函数类似。
1. Microsoft Teams任务模块。

## <a name="submitting-the-result-of-a-task-module"></a>提交任务模块的结果

当用户使用完任务模块后，将结果提交回自动程序与使用选项卡的方式类似，但[](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)存在一些差异，因此此处也进行了介绍。

* **HTML/JavaScript `TaskInfo.url` ()**。 验证用户输入的信息后，可调用 SDK 函数 (以下称为" `microsoftTeams.tasks.submitTask()` `submitTask()` 可读性") 。 如果只想关闭任务模块，Teams调用不带任何参数，但大多数情况下，需要将对象或字符串传递到 `submitTask()` `submitHandler` 。 只需传递它作为第一个参数， `result` 。 Teams `submitHandler` 将调用 `err` ：will `null` 和 `result` will be the object/string you passed to `submitTask()` 。 如果使用 参数调用 ，则必须传递 或 字符串数组：这允许 Teams 验证发送结果的应用是否与调用任务模块的应用 `submitTask()` `result`  `appId` `appId` 相同。 自动程序将收到 `task/submit` 一条消息， `result` 如下 [所述](#payload-of-taskfetch-and-tasksubmit-messages)。
* **自适应卡片 `TaskInfo.card` () 。** 自适应卡片正文 (用户填充) 当用户按下任何按钮时，会通过一条消息发送给 `task/submit` 自动 `Action.Submit` 程序。

## <a name="the-flexibility-of-tasksubmit"></a>任务/提交的灵活性

在上一部分中，你了解了当用户完成从自动程序调用的任务模块时，机器人始终会收到 `task/submit invoke` 一条消息。 作为开发人员，在回复消息 *时，有几个* `task/submit` 选项：

| HTTP 正文响应                      | 应用场景                                |
| --------------------------------------- | --------------------------------------- |
| 无 (忽略 `task/submit` 消息)  | 最简单的响应是没有任何响应。 用户完成任务模块后，自动程序无需响应。 |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams将在弹出消息 `value` 框中显示 的值。 |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | 允许你在向导/多步骤体验中将自适应卡片序列"链接"在一起。 _请注意，将自适应卡片链接至序列是一个高级方案，未在此处进行介绍。但是Node.js示例应用支持它，并且其工作方式记录在其 README.md [文件中](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)。_ |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>任务/提取和任务/提交消息的有效负载

本部分定义机器人接收或 Bot Framework 对象时接收的内容 `task/fetch` `task/submit` `Activity` 的架构。 重要的顶级如下所示：

| 属性 | 描述                          |
| -------- | ------------------------------------ |
| `type`   | 将始终为 `invoke`              |
| `name`   | 或 `task/fetch``task/submit` |
| `value`  | 开发人员定义的有效负载。 通常，对象 `value` 的结构反映从事件发送Teams。 但是，在这种情况下，这有所不同，因为我们希望同时支持从 Bot Framework () 和自适应卡片操作 () 获取动态提取 `task/fetch` `value` (`Action.Submit` `data`) ，并且 `context` `value` / `data` 我们需要一种方法来将 Teams 与自动程序进行通信，以及其中包括哪些内容。<br/><br/>我们通过将两者合并到父对象中来这样做：<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a>示例：接收和响应任务/提取和任务/提交调用消息 - Node.js

> [!NOTE]
> 下面的示例代码在 Technical Preview 和此功能的最终版本之间进行了修改：请求的架构更改为遵循上一节中 `task/fetch` [记录的内容](#payload-of-taskfetch-and-tasksubmit-messages)。 也就是说，文档正确，但实现不正确。 有关 `// for Technical Preview [...]` 更改内容，请参阅下面的注释。

```typescript
// Handle requests and responses for a "Custom Form" and an "Adaptive card" task module.
// Assumes request is coming from an Adaptive card Action.Submit button that has a "taskModule" property indicating what to invoke
private async onInvoke(event: builder.IEvent, cb: (err: Error, body: any, status?: number) => void): Promise<void> {
    let invokeType = (event as any).name;
    let invokeValue = (event as any).value;
    if (invokeType === undefined) {
        invokeType = null;
    }
    switch (invokeType) {
        case "task/fetch": {
            if (invokeValue !== undefined && invokeValue.data.taskModule === "customform") { // for Technical Preview, was invokeValue.taskModule
                // Return the specified task module response to the bot
                let fetchTemplate: any = {
                    "task": {
                        "type": "continue",
                        "value": {
                            "title": "Custom Form",
                            "height": 510,
                            "width": 430,
                            "fallbackUrl": "https://contoso.com/teamsapp/customform",
                            "url": "https://contoso.com/teamsapp/customform",
                        }
                    }
                };
                cb(null, fetchTemplate, 200);
            };
            if (invokeValue !== undefined && invokeValue.data.taskModule === "adaptivecard") { // for Technical Preview, was invokeValue.taskModule
                let adaptiveCard = {
                    "type": "AdaptiveCard",
                    "body": [
                        {
                            "type": "TextBlock",
                            "text": "Here is a ninja cat:"
                        },
                        {
                            "type": "Image",
                            "url": "http://adaptivecards.io/content/cats/1.png",
                            "size": "Medium"
                        }
                    ],
                    "version": "1.0"
                };
                // Return the specified task module response to the bot
                let fetchTemplate: any = {
                    "task": {
                        "type": "continue",
                        "value": {
                            "title": "Ninja Cat",
                            "height": "small",
                            "width": "small",
                            "card": {
                                contentType: "application/vnd.microsoft.card.adaptive",
                                content: adaptiveCard,
                            }
                        }
                    }
                };
                cb(null, fetchTemplate, 200);
            };
            break;
        }
        case "task/submit": {
            if (invokeValue.data !== undefined) {
                // It's a valid task module response
                let submitResponse: any = {
                    "task": {
                        "type": "message",
                        "value": "Task complete!",
                    }
                };
                cb(null, fetchTemplates.submitMessageResponse, 200)
            }
        }
    }
}
```

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a>示例：接收和响应任务/提取和任务/提交调用消息 - C#

在C#中， `invoke` 消息由处理邮件 `HttpResponseMessage()` 的控制器 `Activity` 处理。 和 `task/fetch` `task/submit` 请求和响应为 JSON。 在C#中，处理原始 JSON 并不方便，因为它在 Node.js 中，因此你需要包装类来处理与 JSON 之间的序列化。 尚未在 Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)中对此进行直接支持，但你可以查看这些简单包装类在 C#[应用中的外观示例](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)。

下面是用于处理C#和使用这些包装类的邮件的示例代码 `task/fetch` `task/submit` `TaskInfo` ， (、) 示例摘录 `TaskEnvelope` ： [](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)

```csharp
private HttpResponseMessage HandleInvokeMessages(Activity activity)
{
    var activityValue = activity.Value.ToString();
    if (activity.Name == "task/fetch")
    {
        var action = Newtonsoft.Json.JsonConvert.DeserializeObject<Models.BotFrameworkCardValue<string>>(activityValue);

        Models.TaskInfo taskInfo = GetTaskInfo(action.Data);
        Models.TaskEnvelope taskEnvelope = new Models.TaskEnvelope
        {
            Task = new Models.Task()
            {
                Type = Models.TaskType.Continue,
                TaskInfo = taskInfo
            }
        };
        return Request.CreateResponse(HttpStatusCode.OK, taskEnvelope);
    }
    else if (activity.Name == "task/submit")
    {
        ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
        Activity reply = activity.CreateReply("Received = " + activity.Value.ToString());
        connector.Conversations.ReplyToActivity(reply);
    }
    return new HttpResponseMessage(HttpStatusCode.Accepted);
}

// Helper function for building the TaskInfo object based on the incoming request
private static Models.TaskInfo GetTaskInfo(string actionInfo)
{
    Models.TaskInfo taskInfo = new Models.TaskInfo();
    switch (actionInfo)
    {
        case TaskModuleIds.YouTube:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.YouTube;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
            break;
        case TaskModuleIds.PowerApp:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.PowerApp;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.PowerApp);
            break;
        case TaskModuleIds.CustomForm:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.CustomForm;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
            break;
        case TaskModuleIds.AdaptiveCard:
            taskInfo.Card = AdaptiveCardHelper.GetAdaptiveCard();
            SetTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
            break;
        default:
            break;
    }
    return taskInfo;
}
```

以上示例中未显示 的是 函数，它设置每个大小写的对象的 、 `SetTaskInfo()` `height` 和 `width` `title` `TaskInfo` 属性。 下面是[SetTaskInfo () 。 ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>自动程序框架卡片操作与自适应卡片操作。提交操作

Bot Framework 卡操作架构与自适应卡片操作略有不同 `Action.Submit` 。 因此，调用任务模块的方式也略有不同：中的 对象包含 对象，因此不会干扰卡片中 `data` `Action.Submit` `msteams` 其他属性。 下表显示了每个示例：

| Bot Framework 卡操作                              | 自适应卡片 Action.Submit 操作                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="see-also"></a>另请参阅

* [Microsoft Teams模块示例代码 — nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。