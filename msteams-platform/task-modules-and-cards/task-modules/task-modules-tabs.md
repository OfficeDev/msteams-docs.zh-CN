---
title: 在选项卡中Microsoft Teams模块
description: 介绍如何使用 Teams 客户端 SDK 从Microsoft Teams调用任务模块
localization_priority: Normal
ms.topic: how-to
keywords: 任务模块团队选项卡客户端 sdk
ms.openlocfilehash: 5e85fd0662b8a15d6b98d9c2d2dfa5137b05fa39
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019522"
---
# <a name="using-task-modules-in-tabs"></a>在选项卡中使用任务模块

将任务模块添加到选项卡可以大大简化任何需要数据输入的工作流的用户体验。 任务模块允许你在可感知Teams中收集输入。 一个很好的示例是编辑 Planner 卡;可以使用任务模块来创建类似的体验。

为了支持任务模块功能，向 Microsoft Teams SDK 添加了两[个新函数](/javascript/api/overview/msteams-client)：

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

下面我们了解一下每个功能如何工作。

## <a name="invoking-a-task-module-from-a-tab"></a>从选项卡调用任务模块

若要从选项卡调用任务模块，请使用 `microsoftTeams.tasks.startTask()` 传递 [TaskInfo 对象](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) 和可选回调 `submitHandler` 函数。 如前面所述，有两种情况需要考虑：

1. 的值设置为 `TaskInfo.url` URL。 任务模块窗口将显示 `TaskModule.url` ，并作为一个内部 `<iframe>` 窗口加载。 该页面上的 JavaScript 应调用 `microsoftTeams.initialize()` 。 如果页面上有函数，并且调用 时出错，则调用 时将 设置为 指示错误的错误字符串， `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` [如下所述](#task-module-invocation-errors)。
1. 的值 `taskInfo.card` 是自适应卡片[的 JSON。](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment) 在这种情况下，明显没有任何 JavaScript 函数在用户关闭或按下自适应卡片上的按钮时调用;接收用户输入内容的唯一方法就是将结果传递给机器人 `submitHandler` 。 若要从选项卡使用自适应卡片任务模块，应用必须包含自动程序才能从用户获取任何信息。 下面对此进行了说明。

## <a name="example-invoking-a-task-module"></a>示例：调用任务模块

下面的代码改编自任务 [模块示例](~/task-modules-and-cards/what-are-task-modules.md#code-sample)。 任务模块如下所示：

![任务模块 - 自定义窗体](~/assets/images/task-module/task-module-custom-form.png)

非常简单;它只是将 的值回显到 `submitHandler` `err` 控制台 `result` ：

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

## <a name="submitting-the-result-of-a-task-module"></a>提交任务模块的结果

函数 `submitHandler` 与 一同使用 `TaskInfo.url` 。 `submitHandler`函数驻留在 `TaskInfo.url` 网页中。 如果在调用任务模块时出现错误，函数将立即调用，并包含指示发生了哪个 `submitHandler` `err` [错误的字符串](#task-module-invocation-errors)。 当用户按任务模块右上角的 X 时，也会使用字符串调用 `submitHandler` `err` 函数。

如果没有调用错误，并且用户不按 X 消除它，则用户完成后按下一个按钮。 根据它是任务模块中的 URL 还是自适应卡片，下面是发生的情况：

### <a name="htmljavascript-taskinfourl"></a>HTML/JavaScript `TaskInfo.url` () 

验证用户输入了哪些信息后，调用 SDK 函数 (以下称为" `microsoftTeams.tasks.submitTask()` `submitTask()` 可读性") 。 如果只想关闭任务模块，Teams调用不带任何参数，但大多数情况下，需要将对象或字符串传递到 `submitTask()` `submitHandler` 。

将结果作为第一个参数传递。 Teams调用 where `submitHandler` `err` will and will be `null` the `result` object/string you passed to `submitTask()` 。 如果使用 参数调用 ，则必须传递 或 字符串数组：这允许 Teams 验证发送结果的应用是否与调用任务模块的应用 `submitTask()` `result`  `appId` `appId` 相同。

### <a name="adaptive-card-taskinfocard"></a>自适应卡片 `TaskInfo.card` () 

如果使用 调用任务模块，当用户按下按钮时，卡片中的值将返回 `submitHandler` `Action.Submit` 为 的值 `result` 。 如果用户按下 Esc 按钮或按 X， `err` 将改为返回 。 或者，如果你的应用包含除选项卡外还包含自动程序，则只需在 对象中包含 自动程序 作为 `appId` `completionBotId` `TaskInfo` 的值。 用户 (填充的自适应卡片正文) 当用户按下按钮时，会通过一条消息发送给 `task/submit invoke` `Action.Submit` 自动程序。 您接收的对象的架构与针对任务/提取和任务/提交消息接收[的架构非常相似](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages);唯一的区别是 JSON 对象的架构是自适应卡片对象，而不是包含自适应卡片对象的对象，就像自适应卡片用于[机器人一样](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)。

## <a name="example-submitting-the-result-of-a-task-module"></a>示例：提交任务模块的结果

使用 HTML [窗体撤回](#example-invoking-a-task-module) 上述任务模块中的窗体。 下面是定义表单的地方：

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

此窗体上有五个字段，但我们仅对此示例中的三个字段的值感兴趣：、 `name` `email` 和 `favoriteBook` 。

下面是调用 `validateForm()` 的函数 `submitTask()` ：

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

## <a name="task-module-invocation-errors"></a>任务模块调用错误

下面是你的 `err` 可以接收的可能值 `submitHandler` ：

| 问题 | 错误消息 (值 `err`)  |
| ------- | ------------------------------ |
| 指定了 和 `TaskInfo.url` `TaskInfo.card` 的值。 | "已指定 card 和 url 的值。 允许一个或另一个，但不能同时使用这两者。" |
| 既不 `TaskInfo.url` 指定也不 `TaskInfo.card` 指定。 | "你必须为卡片或 url 指定值。" |
| 无效 `appId` 。 | "invalid appId." |
| 用户按下 X 按钮，关闭它。 | "用户已取消/关闭任务模块。" |
