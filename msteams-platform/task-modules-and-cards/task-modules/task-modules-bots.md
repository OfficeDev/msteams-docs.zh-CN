---
title: 使用自动程序Microsoft Teams模块
description: 如何将任务模块与自动程序Microsoft Teams，包括 Bot Framework 卡、自适应卡片和深层链接。
localization_priority: Normal
ms.topic: how-to
keywords: 任务模块团队机器人
ms.openlocfilehash: 7a4c5b0a3986f5a6a59064a05bcbc68587955effca0ea7fab80a7097a9732b6f
ms.sourcegitcommit: 3ab1cbec41b9783a7abba1e0870a67831282c3b5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/07/2021
ms.locfileid: "57701869"
---
# <a name="use-task-modules-from-bots"></a>使用机器人的任务模块

可以使用自适应卡片和自动程序框架Microsoft Teams、缩略图和自动程序连接器上的按钮从自动程序调用任务Office 365模块。 任务模块通常是比多个对话步骤更好的用户体验。 跟踪自动程序状态并允许用户中断或取消序列。

有两种调用任务模块的方法：

* 一种新的调用消息：使用 Bot Framework 卡片的卡片操作或自适应卡片的卡片操作，以及 任务模块的 URL 或自适应卡片，从自动程序动态获取 `task/fetch` `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` 。
* 深层链接 URL：使用任务[](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)模块的深层链接语法，可以分别使用 Bot Framework 卡片的卡片操作或自适应卡片的卡片 `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)操作。 使用深层链接 URL，任务模块 URL 或自适应卡片正文已知以避免相对于 的服务器往返 `task/fetch` 。

> [!IMPORTANT]
> 每个 `url` 和 `fallbackUrl` 都必须实现 HTTPS 加密协议。

下一节提供有关使用 调用任务模块的详细信息 `task/fetch` 。

## <a name="invoke-a-task-module-using-taskfetch"></a>使用任务/提取调用任务模块

当卡片的对象操作或初始化时，以及当用户选择该按钮时，会向自动 `value` `invoke` `Action.Submit` `invoke` 程序发送一条消息。 在消息的 HTTP 响应中，包装对象中嵌入了一个 `invoke` [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) Teams该对象用于显示任务模块。

![任务/提取请求或响应](~/assets/images/task-module/task-module-invoke-request-response.png)

以下步骤使用 task/fetch 提供调用任务模块：

1. 此图显示了具有购买卡片操作的 Bot  Framework `invoke` [hero 卡](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)。 属性的值 `type` 为 `task/fetch` ，对象的其余部分 `value` 可以是你的选择。
1. 机器人接收 HTTP `invoke` POST 消息。
1. 机器人创建响应对象，并返回 HTTP 200 响应代码的 POST 响应正文。 有关响应的架构详细信息，请参阅有关 [task/submit 的讨论](#the-flexibility-of-tasksubmit)。 以下代码提供了 HTTP 响应的正文示例，该响应包含嵌入包装对象中的 [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) 对象：

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

    `task/fetch`事件及其对机器人的响应类似于客户端 SDK 中的 `microsoftTeams.tasks.startTask()` 函数。

1. Microsoft Teams任务模块。

下一节提供有关提交任务模块结果的详细信息。

## <a name="submit-the-result-of-a-task-module"></a>提交任务模块的结果

当用户完成任务模块后，将结果提交回自动程序与使用选项卡的方式类似。 有关详细信息，请参阅 [提交任务模块的结果的示例](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)。 存在以下一些区别：

* HTML 或 JavaScript，即 ：在验证用户输入内容后，出于可读性目的，调用以下引用的 `TaskInfo.url` `microsoftTeams.tasks.submitTask()` SDK `submitTask()` 函数。 如果希望关闭任务模块Teams调用不带任何参数，但必须将对象或字符串传递给 `submitTask()` `submitHandler` 。 将它作为第一个参数传递 `result` 。 Teams调用 `submitHandler` 、 、 `err` 和 `null` `result` 是传递给 的对象或字符串 `submitTask()` 。 如果使用 参数 `submitTask()` 调用 `result` ，则必须传递 或 `appId` 字符串 `appId` 数组。 这Teams验证发送结果的应用是否与调用任务模块的应用相同。 自动程序会收到一 `task/submit` 条消息，其中包括 `result` 。 有关详细信息，请参阅 [和 `task/fetch` 邮件 `task/submit` 的有效负载](#payload-of-taskfetch-and-tasksubmit-messages)。
* 自适应卡片，即 ：当用户选择任何按钮时，用户填充的自适应卡片正文通过消息 `TaskInfo.card` `task/submit` 发送给 `Action.Submit` 机器人。

下一节提供有关 灵活性的详细信息 `task/submit` 。

## <a name="the-flexibility-of-tasksubmit"></a>任务/提交的灵活性

当用户完成从自动程序调用的任务模块时，机器人始终会收到 `task/submit invoke` 一条消息。 回复邮件时有几种选项 `task/submit` ，如下所示：

| HTTP 正文响应                      | 应用场景                                |
| --------------------------------------- | --------------------------------------- |
| None 将忽略 `task/submit` 该消息 | 最简单的响应是没有任何响应。 用户完成任务模块后，自动程序无需响应。 |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams在弹出 `value` 消息框中显示 的值。 |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | 允许你在向导或多步骤体验中将自适应卡片序列链接在一起。 |

> [!NOTE]
> 将自适应卡片链接至序列是一种高级方案。 示例Node.js支持它。 有关详细信息，请参阅任务[Microsoft Teams模块Node.js。 ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)

下一节提供有关 和 邮件的有效 `task/fetch` 负载 `task/submit` 的详细信息。

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>任务/提取和任务/提交消息的有效负载

本部分定义机器人接收或 Bot Framework 对象时接收的内容 `task/fetch` `task/submit` `Activity` 的架构。 下表提供了 和 消息的有效负载 `task/fetch` `task/submit` 的属性：

| 属性 | 说明                          |
| -------- | ------------------------------------ |
| `type`   | 始终 `invoke` 为 。           |
| `name`   | 是 `task/fetch` 或 `task/submit` 。 |
| `value`  | 是开发人员定义的有效负载。 对象的结构与从对象 `value` 发送Teams。 但在这种情况下，情况有所不同。 它需要对来自自动程序框架的动态提取（即 和 `task/fetch` `value` 自适应卡片操作） `Action.Submit` 的支持，即 `data` 。 除了 或 中Teams外，需要一种与自动程序 `context` 通信 `value` 的方法 `data` 。<br/><br/>将"value"和"data"合并到父对象中：<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

下一节提供了一个在邮件中接收、响应 `task/fetch` `task/submit` 和调用Node.js。

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a>任务/提取和任务/提交调用消息的示例Node.js和 C#

# <a name="nodejs"></a>[Node.js](#tab/nodejs)

```typescript
handleTeamsTaskModuleFetch(context, taskModuleRequest) {
    // Called when the user selects an options from the displayed HeroCard or
    // AdaptiveCard.  The result is the action to perform.

    const cardTaskFetchValue = taskModuleRequest.data.data;
    var taskInfo = {}; // TaskModuleTaskInfo

    if (cardTaskFetchValue === TaskModuleIds.YouTube) {
        // Display the YouTube.html page
        taskInfo.url = taskInfo.fallbackUrl = this.baseUrl + '/' + TaskModuleIds.YouTube + '.html';
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
    } else if (cardTaskFetchValue === TaskModuleIds.CustomForm) {
        // Display the CustomForm.html page, and post the form data back via
        // handleTeamsTaskModuleSubmit.
        taskInfo.url = taskInfo.fallbackUrl = this.baseUrl + '/' + TaskModuleIds.CustomForm + '.html';
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
    } else if (cardTaskFetchValue === TaskModuleIds.AdaptiveCard) {
        // Display an AdaptiveCard to prompt user for text, and post it back via
        // handleTeamsTaskModuleSubmit.
        taskInfo.card = this.createAdaptiveCardAttachment();
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
    }

    return TaskModuleResponseFactory.toTaskModuleResponse(taskInfo);
}

async handleTeamsTaskModuleSubmit(context, taskModuleRequest) {
    // Called when data is being returned from the selected option (see `handleTeamsTaskModuleFetch').

    // Echo the users input back.  In a production bot, this is where you'd add behavior in
    // response to the input.
    await context.sendActivity(MessageFactory.text('handleTeamsTaskModuleSubmit: ' + JSON.stringify(taskModuleRequest.data)));

    // Return TaskModuleResponse
    return {
        // TaskModuleMessageResponse
        task: {
            type: 'message',
            value: 'Thanks!'
        }
    };
}

setTaskInfo(taskInfo, uiSettings) {
    taskInfo.height = uiSettings.height;
    taskInfo.width = uiSettings.width;
    taskInfo.title = uiSettings.title;
}
```

# <a name="c"></a>[C#](#tab/csharp)

```csharp
protected override Task<TaskModuleResponse> OnTeamsTaskModuleFetchAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
{
    var asJobject = JObject.FromObject(taskModuleRequest.Data);
    var value = asJobject.ToObject<CardTaskFetchValue<string>>()?.Data;

    var taskInfo = new TaskModuleTaskInfo();
    switch (value)
    {
        case TaskModuleIds.YouTube:
            taskInfo.Url = taskInfo.FallbackUrl = _baseUrl + "/" + TaskModuleIds.YouTube;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
            break;
        case TaskModuleIds.CustomForm:
            taskInfo.Url = taskInfo.FallbackUrl = _baseUrl + "/" + TaskModuleIds.CustomForm;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
            break;
        case TaskModuleIds.AdaptiveCard:
            taskInfo.Card = CreateAdaptiveCardAttachment();
            SetTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
            break;
        default:
            break;
    }

    return Task.FromResult(taskInfo.ToTaskModuleResponse());
}

protected override async Task<TaskModuleResponse> OnTeamsTaskModuleSubmitAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
{
    var reply = MessageFactory.Text("OnTeamsTaskModuleSubmitAsync Value: " + JsonConvert.SerializeObject(taskModuleRequest));
    await turnContext.SendActivityAsync(reply, cancellationToken);

    return TaskModuleResponseFactory.CreateResponse("Thanks!");
}

private static void SetTaskInfo(TaskModuleTaskInfo taskInfo, UISettings uIConstants)
{
    taskInfo.Height = uIConstants.Height;
    taskInfo.Width = uIConstants.Width;
    taskInfo.Title = uIConstants.Title.ToString();
}
```

---

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>自动程序框架卡片操作与自适应卡片操作。提交操作

Bot Framework 卡片操作架构不同于自适应卡片操作，调用任务模块的方式 `Action.Submit` 也不同。 `data`中的 `Action.Submit` 对象包含 `msteams` 对象，因此不会干扰卡片中其他属性。 下表显示了每个卡片操作的示例：

| Bot Framework 卡操作                              | 自适应卡片操作.Submit 操作                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a>代码示例

|示例名称 | 说明 | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|任务模块示例 bots-V4 | 用于创建任务模块的示例。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a>另请参阅

* [Microsoft Teams任务模块示例代码Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
