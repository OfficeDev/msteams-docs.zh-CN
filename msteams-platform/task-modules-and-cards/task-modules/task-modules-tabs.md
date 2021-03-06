---
title: 使用选项卡中的任务Microsoft Teams模块
description: 介绍如何使用客户端 SDK 从Teams调用任务Microsoft Teams模块。
localization_priority: Normal
ms.topic: how-to
keywords: 任务模块团队选项卡客户端 sdk
ms.openlocfilehash: 8afd2c93261f28aa7ced4c98d29be27dca35f8b1
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140550"
---
# <a name="use-task-modules-in-tabs"></a>在选项卡中使用任务模块

向选项卡添加任务模块，以简化任何需要数据输入的工作流的用户体验。 任务模块允许你在 Microsoft 弹出窗口中收集Teams-Aware输入。 编辑 Planner 卡就是一个很好的示例。 可以使用任务模块来创建类似的体验。

为了支持任务模块功能，向 Teams SDK 添加了两[个新函数](/javascript/api/overview/msteams-client)。 以下代码显示了这两个函数的示例：

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

你可以了解从选项卡调用任务模块和提交任务模块结果的工作原理。

## <a name="invoke-a-task-module-from-a-tab"></a>从选项卡调用任务模块

若要从选项卡调用任务模块，请使用 `microsoftTeams.tasks.startTask()` 传递 [TaskInfo 对象](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) 和可选回调 `submitHandler` 函数。 有两种情况需要考虑：

* 的值设置为 `TaskInfo.url` URL。 任务模块窗口将显示 `TaskModule.url` ，并作为一个内部 `<iframe>` 窗口加载。 该页面上的 JavaScript 调用 `microsoftTeams.initialize()` 。 如果页面上有函数，并且调用 时出错，则调用 时将 设置为指示相同错误 `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` 字符串。 有关详细信息，请参阅任务 [模块调用错误](#task-module-invocation-errors)。
* 的值 `taskInfo.card` 是自适应[卡片的 JSON。](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment) 当用户关闭或按下自适应卡片上的按钮时，没有要调用的 JavaScript `submitHandler` 函数。 接收用户输入信息的唯一方法就是将结果传递给机器人。 若要从选项卡使用自适应卡片任务模块，你的应用必须包含自动程序才能从用户获取任何响应。

下一节提供了调用任务模块的示例。

## <a name="example-of-invoking-a-task-module"></a>调用任务模块的示例

下图显示了任务模块：

![任务模块 - 自定义窗体](~/assets/images/task-module/task-module-custom-form.png)

以下代码改编自任务 [模块示例](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample)：

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

`submitHandler`非常简单，它会将 的值回显到 控制台或 `err` `result` 。

## <a name="submit-the-result-of-a-task-module"></a>提交任务模块的结果

`submitHandler`函数驻留在 `TaskInfo.url` 网页中，与 一起使用 `TaskInfo.url` 。 如果在调用任务模块时出现错误，将立即调用函数，并包含一个字符串，指示 `submitHandler` `err` [发生了什么错误](#task-module-invocation-errors)。 当用户选择任务模块右上角的 X 以关闭该函数时，也会使用字符串调用 `submitHandler` `err` 该函数。

如果没有调用错误，并且用户未选择 X 将其消除，则用户在完成后选择一个按钮。 根据它是任务模块中的 URL 还是自适应卡片，接下来的部分将提供有关发生的情况的详细信息。

### <a name="html-or-javascript-taskinfourl"></a>HTML 或 JavaScript `TaskInfo.url`

验证用户输入后，调用 `microsoftTeams.tasks.submitTask()` 称为 的 SDK 函数 `submitTask()` 。 如果 `submitTask()` 只想关闭任务模块，Teams调用不带任何参数。 可以将对象或字符串传递到 `submitHandler` 。

将结果作为第一个参数传递。 Teams调用 `submitHandler` where is `err` 和 `null` `result` 是传递给 的对象或字符串 `submitTask()` 。 如果使用 参数 `submitTask()` 调用 `result` ，则必须传递 或 `appId` 字符串 `appId` 数组。 这允许Teams验证发送结果的应用是否与调用的任务模块相同。

### <a name="adaptive-card-taskinfocard"></a>自适应卡片 `TaskInfo.card`

当你使用 调用任务模块且用户选择一个按钮时，卡片中的值将返回 `submitHandler` `Action.Submit` 为 的值 `result` 。 如果用户选择 Esc 键或右上方的 X，则 `err` 改为返回 。 如果你的应用包含除选项卡外还包含自动程序，则只需在 对象中包含 自动程序 作为 `appId` `completionBotId` `TaskInfo` 的值。 当用户选择按钮时，使用消息将用户填充的自适应卡片 `task/submit invoke` 正文发送给 `Action.Submit` 自动程序。 你接收的对象的架构非常类似于你针对任务/提取和任务/提交消息收到的 [架构](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)。 唯一的区别是 JSON 对象的架构是自适应卡片对象，而不是包含自适应卡片对象的对象，就像自适应卡片用于机器人 [一样](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)。

下一节提供了一个提交任务模块结果的示例。

## <a name="example-of-submitting-the-result-of-a-task-module"></a>提交任务模块结果的示例

有关详细信息，请参阅任务 [模块中的 HTML 窗体](#example-of-invoking-a-task-module)。 以下代码提供了表单定义位置的示例：

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

此窗体上有五个字段，但对于此示例，只需要三个值，即 `name` 、 `email` 和 `favoriteBook` 。

以下代码提供了调用 `validateForm()` 的函数的示例 `submitTask()` ：

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

下一节提供任务模块调用问题及其错误消息。

## <a name="task-module-invocation-errors"></a>任务模块调用错误

下表提供了 你的 可以 `err` 接收的可能值 `submitHandler` ：

| 问题 | 值为 的错误消息 `err` |
| ------- | ------------------------------ |
| 指定了 和 `TaskInfo.url` `TaskInfo.card` 的值。 | 已指定卡和 URL 的值。 允许使用其中一个，但不能同时使用这两者。 |
| 既不 `TaskInfo.url` 指定也不 `TaskInfo.card` 指定。 | 必须为卡片或 URL 指定值。 |
| 无效 `appId` 。 | 无效的应用 ID。 |
| 用户选择 X 按钮，关闭它。 | 用户已取消或关闭任务模块。 |

## <a name="code-sample"></a>代码示例

|示例名称 | 说明 | .NET | Node.js|
|----------------|-----------------|--------------|----------------|
|任务模块示例选项卡和 bots-V3 | 用于创建任务模块的示例。 |[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[View](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a>另请参阅

[调用和消除任务模块](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

## <a name="next-step"></a>后续步骤

> [!div class="nextstepaction"]
> [使用自动程序中的任务模块](~/task-modules-and-cards/task-modules/task-modules-bots.md)
