---
title: 在Microsoft Teams机器人中使用任务模块
description: 如何将任务模块与Microsoft Teams机器人配合使用，包括 Bot Framework 卡、自适应卡片和深层链接。
ms.localizationpriority: medium
ms.topic: how-to
keywords: 任务模块团队机器人深度链接自适应卡
ms.openlocfilehash: 7391f7e0d9da444831b98b4b6b69a97b35298800
ms.sourcegitcommit: 3bfd0d2c4d83f306023adb45c8a3f829f7150b1d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/27/2022
ms.locfileid: "65073767"
---
# <a name="use-task-modules-from-bots"></a>使用机器人的任务模块

可以使用自适应卡片和 Bot Framework 卡（主图、缩略图和Office 365连接器）上的按钮从Microsoft Teams机器人调用任务模块。 任务模块通常是比多个对话步骤更好的用户体验。 跟踪机器人状态，并允许用户中断或取消序列。

调用任务模块的方法有两种：

* 一种新型的调用消息 `task/fetch`：使用 `invoke` Bot Framework 卡的 [卡片操作](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) 或 `Action.Submit`自适应卡片的 [卡操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) ， `task/fetch`以及任务模块（URL 或自适应卡片）是从机器人动态提取的。
* 深层链接 URL：使用 [任务模块的深层链接语法](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)，可以分别使用 `openUrl` Bot Framework 卡的 [卡片操作](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) 或 `Action.OpenUrl`自适应卡片的 [卡片操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) 。 使用深层链接 URL 时，任务模块 URL 或自适应卡片正文已为已知，以避免服务器往返相对于 `task/fetch`。

> [!IMPORTANT]
> 每个 `url` 协议都必须 `fallbackUrl` 实现 HTTPS 加密协议。

下一部分提供有关使用任务模块调用 `task/fetch`的详细信息。

## <a name="invoke-a-task-module-using-taskfetch"></a>使用任务/提取调用任务模块

`value`当卡片操作的`invoke`对象或`Action.Submit`初始化时，当用户选择该按钮时，会向机器人发送一`invoke`条消息。 在消息的 HTTP 响应`invoke`中，包装器对象中嵌入了 [TaskInfo 对象](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)，Teams用于显示任务模块。

:::image type="content" source="../../assets/images/task-module/task-module-invoke-request-response.png" alt-text="任务/提取请求或响应":::

以下步骤使用任务/提取提供调用任务模块：

1. 此图显示了一张 Bot Framework hero 卡，其中包含 **“购买** `invoke` [卡”操作](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)。 属性的 `type` 值是 `task/fetch` ，对象的 `value` 其余部分可以是你选择的。
1. 机器人接收 `invoke` HTTP POST 消息。
1. 机器人创建一个响应对象，并使用 HTTP 200 响应代码在 POST 响应正文中返回它。 有关响应架构的详细信息，请参阅 [有关任务/提交的讨论](#the-flexibility-of-tasksubmit)。 以下代码提供了 HTTP 响应正文的示例，其中包含嵌入在包装 [器对象中的 TaskInfo 对象](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) ：

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

    事件 `task/fetch` 及其对机器人的响应类似于 `microsoftTeams.tasks.startTask()` 客户端 SDK 中的函数。

1. Microsoft Teams显示任务模块。

下一部分提供有关提交任务模块结果的详细信息。

## <a name="submit-the-result-of-a-task-module"></a>提交任务模块的结果

当用户完成任务模块后，将结果提交回机器人与使用选项卡的方式类似。 有关详细信息，请参阅 [提交任务模块结果的示例](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)。 有一些差异，如下所示：

* HTML 或 JavaScript，即 `TaskInfo.url`：验证用户输入的内容后，调用 `microsoftTeams.tasks.submitTask()` 后称为 `submitTask()` 可读性的 SDK 函数。 如果希望Teams关闭任务模块，则无需任何参数即可调用`submitTask()`，但必须将对象或字符串传递给你`submitHandler`。 将其作为第一个参数传递。 `result` Teams调用`submitHandler`，`err`即`null``result`传递给`submitTask()`的对象或字符串。 如果使用参数调 `submitTask()` 用 `result` ，则必须传递字符 `appId` 串或字符串数 `appId` 组。 这允许Teams验证发送结果的应用是否与调用任务模块的应用相同。 机器人收到一 `task/submit` 条消息，包括 `result`。 有关详细信息，请参阅 [有效负载 `task/fetch` 和 `task/submit` 消息](#payload-of-taskfetch-and-tasksubmit-messages)。
* 自适应卡片，即`TaskInfo.card`：当用户选择任何`Action.Submit`按钮时，用户填写的自适应卡片正文将通过`task/submit`消息发送到机器人。

下一部分提供有关灵活性的 `task/submit`详细信息。

## <a name="the-flexibility-of-tasksubmit"></a>任务/提交的灵活性

当用户完成从机器人调用的任务模块后，机器人始终会收到一 `task/submit invoke` 条消息。 响应消息时有多个选项， `task/submit` 如下所示：

| HTTP 正文响应                      | 应用场景                                |
| --------------------------------------- | --------------------------------------- |
| 无一人忽略 `task/submit` 消息 | 最简单的响应根本不是响应。 当用户完成任务模块时，无需机器人进行响应。 |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams显示弹出消息框中的值`value`。 |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | 允许在向导或多步骤体验中将自适应卡片序列链接在一起。 |

> [!NOTE]
> 将自适应卡片链接到序列中是一种高级方案。 Node.js示例应用支持它。 有关详细信息，请参阅[Microsoft Teams任务模块Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)。

下一部分提供有关有效负载和`task/submit`消息的`task/fetch`详细信息。

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>任务/提取和任务/提交消息的有效负载

本部分定义机器人收到或 `task/submit` Bot Framework `Activity` 对象时收到`task/fetch`的内容的架构。 下表提供了有效负载和`task/submit`消息的`task/fetch`属性：

| 属性 | 说明                          |
| -------- | ------------------------------------ |
| `type`   | 始终 `invoke`如此。           |
| `name`   | 是或 `task/fetch` `task/submit`. |
| `value`  | 开发人员定义的有效负载。 对象的`value`结构与从Teams发送的结构相同。 但在本例中，情况不同。 它需要支持动态提取，这是 `task/fetch` 从机器人框架，这是 `value` 和自适应卡 `Action.Submit` 片操作，即 `data`。 除了机器人中包含`value`的内容或`data`内容外，还需要一种与机器人通信 `context` Teams的方法。<br/><br/>将“value”和“data”组合到父对象中：<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

下一部分提供了在Node.js中接收和响应 `task/fetch` 和 `task/submit` 调用消息的示例。

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a>Node.js和 C 中的任务/提取和任务/提交调用消息的示例#

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

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Bot Framework 卡操作与自适应卡片操作.提交操作

Bot Framework 卡操作的架构不同于自适应卡片 `Action.Submit` 操作，调用任务模块的方式也不同。 其中的 `data` 对象 `Action.Submit` 包含一个 `msteams` 对象，因此它不会干扰卡片中的其他属性。 下表显示了每个卡片操作的示例：

| Bot Framework 卡操作                              | 自适应卡片操作.提交操作                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a>代码示例

|示例名称 | Description | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|任务模块示例 bots-V4 | 用于创建任务模块的示例。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="step-by-step-guide"></a>分步指南

按照分[步指南](../../sbs-botbuilder-taskmodule.yml)在Teams中创建和提取任务模块机器人。

## <a name="see-also"></a>另请参阅

* [Node.js中Microsoft Teams任务模块示例代码](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
