---
title: 在 Microsoft Teams 选项卡中使用任务模块
description: 介绍如何从 Teams 选项卡调用任务模块，并使用 Microsoft Teams 客户端 SDK 提交其结果。 它包括代码示例。
ms.localizationpriority: high
ms.topic: how-to
keywords: 任务模块 Teams 选项卡客户端 sdk
ms.openlocfilehash: eb199842a60832e6eb77575a7438cc9f52db6e09
ms.sourcegitcommit: f15bd0e90eafb00e00cf11183b129038de8354af
ms.translationtype: HT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2022
ms.locfileid: "65111225"
---
# <a name="use-task-modules-in-tabs"></a>在选项卡中使用任务模块

将任务模块添加到选项卡，以简化用户对需要数据输入的任何工作流的体验。 使用任务模块可以在 Microsoft Teams-Aware 弹出窗口中收集其输入。 一个很好的示例是编辑 Planner 卡片。 可以使用任务模块创建类似的体验。

为了支持任务模块功能，将两个新函数添加到 [Teams 客户端 SDK](/javascript/api/overview/msteams-client)。 以下代码演示以下两个函数的示例：

```typescript
microsoftTeams.tasks.startTask(
    taskInfo: TaskInfo,
    submitHandler?: (err: string, result: string | any) => void
): void;

microsoftTeams.tasks.submitTask(
    result?: string | any,
    appIds?: string | string[]
): void;
```

可以查看如何从选项卡调用任务模块并提交任务模块的结果。

## <a name="invoke-a-task-module-from-a-tab"></a>从选项卡调用任务模块

若要从选项卡调用任务模块，请使用 `microsoftTeams.tasks.startTask()` 传递 [TaskInfo 对象](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) 和可选 `submitHandler` 回调函数。 请考虑下列两种情况：

* 其值 `TaskInfo.url` 设置为 URL。 将显示任务模块窗口，并 `TaskModule.url` 将其加载为其中的窗口 `<iframe>`。 该页上的 JavaScript 调用 `microsoftTeams.initialize()`。 如果页面上有一个 `submitHandler` 函数，并且调用 `microsoftTeams.tasks.startTask()` 时出错，则 `submitHandler` 调用 `err` 时设置为表示相同的错误字符串。 有关详细信息，请参阅 [任务模块调用错误](#task-module-invocation-errors)。
* 其 `taskInfo.card` 值 [ 为自适应卡片的 JSON](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)。 当用户关闭或按下自适应卡片上的按钮时，没有要调用的 JavaScript `submitHandler` 函数。 接收用户输入的内容的唯一方法是将结果传递给机器人。 若要从选项卡使用自适应卡片任务模块，应用必须包含机器人才能从用户获取任何响应。

下一部分提供了调用任务模块的示例。

## <a name="example-of-invoking-a-task-module"></a>调用任务模块的示例

下图显示了任务模块：

:::image type="content" source="../../assets/images/task-module/task-module-custom-form.png" alt-text="任务模块自定义窗体":::

以下代码改编自 [任务模块示例](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample)：

```javascript
let taskInfo = {
    title: null,
    height: null,
    width: null,
    url: null,
    card: null,
    fallbackUrl: null,
    completionBotId: null,
};

taskInfo.url = "https://contoso.com/teamsapp/customform";
taskInfo.title = "Custom Form";
taskInfo.height = 510;
taskInfo.width = 430;
submitHandler = (err, result) => {
    console.log(`Submit handler - err: ${err}`);
    console.log(`Submit handler - result\rName: ${result.name}\rEmail: ${result.email}\rFavorite book: ${result.favoriteBook}`);
};
microsoftTeams.tasks.startTask(taskInfo, submitHandler);
```

`submitHandler` 非常简单，它将 `err` 或 `result` 的值回显到控制台。

## <a name="submit-the-result-of-a-task-module"></a>提交任务模块的结果

该 `submitHandler` 函数驻留在 `TaskInfo.url` 网页中，并与`TaskInfo.url` 一起使用。 如果调用任务模块时出错，则会立即调用`submitHandler` 函数，其中包含一个 `err` 字符串，指示 [发生错误](#task-module-invocation-errors)。 当用户选择任务模块右上角的 X 以关闭`submitHandler` 函数时，还会使用 `err` 字符串调用该函数。

如果没有调用错误，并且用户未选择 X 将其关闭，则用户会在完成后选择一个按钮。 确定任务模块中的 URL 或自适应卡片，下一部分提供有关具体情况的详细信息。

### <a name="html-or-javascript-taskinfourl"></a>HTML 或 JavaScript `TaskInfo.url`

验证用户的输入后，调用名为 `submitTask()` 的 `microsoftTeams.tasks.submitTask()` SDK 函数。 如果只想让 Teams 关闭任务模块，请在没有任何参数的情况下调用 `submitTask()`。 可以将对象或字符串传递给你的 `submitHandler`。

将结果作为第一个参数传递。 Teams 调用`submitHandler`传递到`submitTask()`的对象或字符串的位置`err``null`和`result`位置。 如果调用带 `result` 参数的 `submitTask()`，则必须传递 `appId` 或 `appId` 字符串的数组。 这允许 Teams 验证发送结果的应用是否与调用的任务模块相同。

### <a name="adaptive-card-taskinfocard"></a>自适应卡片`TaskInfo.card`

使用某个任务模块调用 `submitHandler` 任务模块，用户选择一个 `Action.Submit` 按钮时，卡片中的值将作为值 `result` 返回。 如果用户选择右上角的 Esc 键或 X，则 返回 `err`。 如果应用除了选项卡外还包含机器人，则只需将机器人的值`completionBotId`包含`appId`在对象中`TaskInfo`。 用户填写的自适应卡片正文会在用户选择`Action.Submit`按钮时使用`task/submit invoke`消息发送到机器人。 收到的对象架构与 [ 收到的任务/提取和任务/提交消息的架构 ](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages) 非常相似。 唯一区别是，JSON 对象的架构是自适应卡片对象，而不是包含自适应卡片对象的对象，[就像使用自适应卡片和机器人一样](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)。

下一部分提供了提交任务模块结果的示例。

## <a name="example-of-submitting-the-result-of-a-task-module"></a>提交任务模块结果的示例

有关详细信息，请参阅 [任务模块中的 HTML 窗体](#example-of-invoking-a-task-module)。 下面的代码提供了一个表单定义位置的示例：

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

此窗体上有五个字段，但对于本示例，只需要三个值，`name`、`email`以及 `favoriteBook`。

以下代码提供了调用`submitTask()`以下函数的`validateForm()`示例：

```javascript
function validateForm() {
    var customerInfo = {
        name: document.forms["customerForm"]["name"].value,
        email: document.forms["customerForm"]["email"].value,
        favoriteBook: document.forms["customerForm"]["favoriteBook"].value
    }
    microsoftTeams.tasks.submitTask(customerInfo, "xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx");
    return true;
}
```

下一部分提供任务模块调用问题及其错误消息。

## <a name="task-module-invocation-errors"></a>任务模块调用错误

下表提供了`submitHandler`接收`err`的可能值：

| 问题 | 值为 `err` 的错误消息 |
| ------- | ------------------------------ |
| 指定了 `TaskInfo.url` 和 `TaskInfo.card` 的值。 | 已指定卡片值和 URL 值。允许两者之一，但不能两者都允许。 |
| 既未指定 `TaskInfo.url`，也未指定 `TaskInfo.card`。 | 必须为卡片或 URL 指定值。 |
| 无效 `appId`。 | 无效的应用 ID。 |
| 用户选择的 X 按钮，将其关闭。 | 用户已取消或关闭任务模块。 |

## <a name="code-sample"></a>代码示例

|示例名称 | Description | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|任务模块示例选项卡和 bots-V3 | 用于创建任务模块的示例。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)|

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [使用机器人的任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)

## <a name="see-also"></a>另请参阅

[调用和关闭任务模块](~/task-modules-and-cards/task-modules/invoking-task-modules.md)
