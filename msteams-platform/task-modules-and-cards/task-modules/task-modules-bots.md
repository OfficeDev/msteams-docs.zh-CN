---
title: 在 Microsoft Teams 机器人中使用任务模块
description: 如何将任务模块与 Microsoft Teams 机器人配合使用，包括 Bot Framework 卡片、自适应卡片和深层链接。
ms.localizationpriority: high
ms.topic: how-to
keywords: 任务模块团队机器人深层链接自适应卡片
ms.openlocfilehash: 1074eee616ca7a5d78a071fb42c23d0010a8300d
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111330"
---
# <a name="use-task-modules-from-bots"></a>使用机器人的任务模块

可以使用自适应卡片和 Bot Framework 卡片（主图、缩略图和 Office 365 连接器）上的按钮从 Microsoft Teams 机器人调用任务模块。 任务模块通常是比多对话步骤更好的用户体验。 跟踪机器人状态，并允许用户中断或取消序列。

调用任务模块有两种方法：

* 一种新型的调用消息 `task/fetch`：使用 Bot Framework 卡片的 `invoke` [卡片操作](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)或自适应卡片的 `Action.Submit` [卡片操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)，通过 `task/fetch`，从机器人动态提取任务模块（URL 或自适应卡片）。
* 深层链接 URL：使用[任务模块的深层链接语法](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)，可以分别使用 Bot Framework 卡片的 `openUrl` [卡片操作](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl)或自适应卡片的 `Action.OpenUrl` [卡片操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)。 使用深层链接 URL 时，任务模块 URL 或自适应卡片正文已知，以避免服务器相对于 `task/fetch` 往返。

> [!IMPORTANT]
> 每个 `url` 和 `fallbackUrl` 都必须实现 HTTPS 加密协议。

下节提供有关使用 `task/fetch` 调用任务模块的详细信息。

## <a name="invoke-a-task-module-using-taskfetch"></a>使用任务/提取调用任务模块

当 `invoke` 卡片操作的 `value` 对象或 `Action.Submit` 已初始化，且当用户选择该按钮时，会向机器人发送一条 `invoke` 消息。 在 `invoke` 消息的 HTTP 答复中，包装器对象中嵌入了 [TaskInfo 对象](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)，Teams 用其显示任务模块。

:::image type="content" source="../../assets/images/task-module/task-module-invoke-request-response.png" alt-text="任务/提取请求或答复":::

以下步骤使用任务/提取提供调用任务模块：

1. 此图显示了 Bot Framework 主图卡片，其中包含 **购买** `invoke` [卡片操作](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)。 `type` 属性的值是 `task/fetch`，`value` 对象的其余部分可自行选择。
1. 机器人接收 `invoke` HTTP POST 消息。
1. 机器人将创建答复对象，并使用 HTTP 200 答复代码在 POST 答复正文中将其返回。 有关答复架构的详细信息，请参阅[有关任务/提交的讨论](#the-flexibility-of-tasksubmit)。 以下代码提供了 HTTP 答复正文的示例，其中包含嵌入到包装器对象中的 [TaskInfo 对象](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object)：

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

    `task/fetch` 事件及其对机器人的答复类似于客户端 SDK 中的 `microsoftTeams.tasks.startTask()` 函数。

1. Microsoft Teams 显示任务模块。

下节提供有关提交任务模块结果的详细信息。

## <a name="submit-the-result-of-a-task-module"></a>提交任务模块的结果

当用户完成任务模块后，将结果提交回机器人时与使用选项卡的方式类似。 有关详细信息，请参阅[提交任务模块的结果示例](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)。 存在一些差异，见如下所示：

* HTML 或 JavaScript，即 `TaskInfo.url`：验证用户输入的内容后，为实现可读性目标，可调用 `microsoftTeams.tasks.submitTask()`（以下简称为 `submitTask()`）的 SDK 函数。 如果希望 Teams 关闭任务模块，可以调用不带任何参数的 `submitTask()`，但必须将对象或字符串传递给 `submitHandler`。 将其作为第一个参数 `result` 传递。 Teams 调用 `submitHandler`，`err` 是 `null`，`result` 是传递给 `submitTask()` 的对象或字符串。 如果调用带 `result` 参数的 `submitTask()`，则必须传递 `appId` 或 `appId` 字符串的数组。 这允许 Teams 验证发送结果的应用是否与调用任务模块的应用是同一个。 机器人收到一条 `task/submit` 消息，包括 `result`。 有关详细信息，请参阅 [`task/fetch` 和 `task/submit` 消息的有效负载](#payload-of-taskfetch-and-tasksubmit-messages)。
* 自适应卡片是 `TaskInfo.card`：当用户选择任何 `Action.Submit` 按钮时，用户填写的自适应卡片正文将通过 `task/submit` 消息发送到机器人。

下节提供有关 `task/submit` 灵活性的详细信息。

## <a name="the-flexibility-of-tasksubmit"></a>任务/提交的灵活性

当用户完成从机器人调用的任务模块后，机器人始终会收到一条 `task/submit invoke` 消息。 答复 `task/submit` 消息时有多个选项，见如下所示：

| HTTP 正文答复                      | 应用场景                                |
| --------------------------------------- | --------------------------------------- |
| 无人忽略 `task/submit` 消息 | 最简单的答复根本不是答复。 当用户完成任务模块时，无需机器人进行答复。 |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | Teams 显示弹出消息框中的 `value` 值。 |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | 允许在向导或多步骤体验中将自适应卡片序列链接到一起。 |

> [!NOTE]
> 将自适应卡片链接到序列中是一种高级应用场景。 Node.js 示例应用支持此操作。 有关详细信息，请参阅 [Microsoft Teams 任务模块 Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)。

下节提供有关 `task/fetch` 和 `task/submit` 消息有效负载的详细信息。

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a>任务/提取和任务/提交消息的有效负载

本节定义机器人收到 `task/fetch` 或 `task/submit` Bot Framework `Activity` 对象时收到的内容架构。 下表提供了 `task/fetch` 和 `task/submit` 消息有效负载的属性：

| 属性 | 说明                          |
| -------- | ------------------------------------ |
| `type`   | 始终为 `invoke`。           |
| `name`   | 是 `task/fetch` 或 `task/submit`。 |
| `value`  | 是开发人员定义的有效负载。 `value` 对象的结构与从 Teams 发送的结构相同。 但在此案例中，情况不同。 它需要支持动态提取，即从机器人框架 `task/fetch`，也就是 `value` 和自适应卡片 `Action.Submit` 操作，即 `data`。 除了 `value` 或 `data` 中包含的内容外，还需要一种 Teams `context` 与机器人通信的方法。<br/><br/>将“值”和“数据”组合到父对象中：<br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

下节提供在 Node.js 中接收和答复 `task/fetch` 和 `task/submit` 调用消息的示例。

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a>Node.js 和 C# 中的任务/提取和任务/提交调用消息的示例

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

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a>Bot Framework 卡片操作与自适应卡片操作。提交操作

Bot Framework 卡片操作的架构不同于自适应卡片 `Action.Submit` 操作，调用任务模块的方式也不同。 `Action.Submit` 中的 `data` 对象包含一个 `msteams` 对象，因此它不会干扰卡片中的其他属性。 下表显示了每个卡片操作的示例：

| Bot Framework 卡片操作                              | 自适应卡片 Action.Submit 操作                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a>代码示例

|示例名称 | Description | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|任务模块示例机器人-V4 | 用于创建任务模块的示例。 |[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[View](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="step-by-step-guide"></a>分步指南

按照[分步指南](../../sbs-botbuilder-taskmodule.yml)在 Teams 中创建和提取任务模块机器人。

## <a name="see-also"></a>另请参阅

* [Node.js 中的 Microsoft Teams 任务模块示例代码](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
