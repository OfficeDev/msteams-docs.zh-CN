---
title: 在 Microsoft 团队选项卡中使用任务模块
description: 介绍如何使用 Microsoft 团队客户端 SDK 从团队选项卡调用任务模块。
keywords: 任务模块团队选项卡客户端 sdk
ms.openlocfilehash: e10958195713f338a9b5e0a0672d8b6a29da9264
ms.sourcegitcommit: 2a84a3c8b10771e37ce51bf603a967633947a3e4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/10/2020
ms.locfileid: "44801004"
---
# <a name="using-task-modules-in-tabs"></a>在选项卡中使用任务模块

将任务模块添加到选项卡后，可以大大简化用户对需要数据输入的任何工作流的体验。 任务模块允许您在工作组感知弹出窗口中收集其输入信息。 此示例的一个很有用的示例是编辑 Planner 卡片;您可以使用任务模块来创建类似的体验。

若要支持任务模块功能， [Microsoft 团队客户端 SDK](/javascript/api/overview/msteams-client)中添加了两个新函数：

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

我们来看看每个方法的工作方式。

## <a name="invoking-a-task-module-from-a-tab"></a>从选项卡调用任务模块

若要从选项卡调用任务模块，请使用 `microsoftTeams.tasks.startTask()` 传递[TaskInfo 对象](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)和可选的 `submitHandler` 回调函数。 如上文所述，有两种情况需要考虑：

1. 的值 `TaskInfo.url` 设置为 URL。 将显示 "任务模块" 窗口，并 `TaskModule.url` 将 `<iframe>` 其加载为内部。 该页面上的 JavaScript 应调用 `microsoftTeams.initialize()` 。 如果 `submitHandler` 页面上有一个函数，并且调用时出现错误 `microsoftTeams.tasks.startTask()` ，则会调用，并将其 `submitHandler` `err` 设置为错误字符串，以指示如下所述[below](#task-module-invocation-errors)的错误。
1. 的值 `taskInfo.card` 是[自适应卡片的 JSON](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)。 在这种情况下，在 `submitHandler` 用户关闭或按下自适应卡片上的按钮时，显然没有任何要调用的 JavaScript 函数; 通过将结果传递给 bot，接收用户输入的内容的唯一方法。 若要从选项卡中使用自适应卡片任务模块，您的应用程序必须包括用于从用户获取任何信息的 bot。 下面对此进行了说明。

## <a name="example-invoking-a-task-module"></a>示例：调用任务模块

下面的代码适用于[任务模块示例](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples)。 任务模块如下所示：

![任务模块-自定义窗体](~/assets/images/task-module/task-module-custom-form.png)

`submitHandler`这非常简单; 它只是回显控制台的值 `err` `result` ：

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

`submitHandler`函数与一起使用 `TaskInfo.url` 。 `submitHandler`函数驻留在网页中 `TaskInfo.url` 。 如果调用任务模块时出现错误 `submitHandler` ，将立即使用 `err` 指示发生了哪种[错误](#task-module-invocation-errors)的字符串来调用函数。 `submitHandler` `err` 当用户按下位于任务模块右上角的 X 时，也可以使用字符串调用函数。

如果没有调用错误，并且用户没有按 X 关闭它，则用户在完成时按下一个按钮。 根据任务模块中的 URL 或自适应卡片的不同，将发生以下情况：

### <a name="htmljavascript-taskinfourl"></a>HTML/JavaScript （ `TaskInfo.url` ）

验证用户输入的内容后，您就可以调用 `microsoftTeams.tasks.submitTask()` SDK 函数（在以后 `submitTask()` 出于可读性目的而引用）。 `submitTask()`如果只想要团队关闭任务模块，则可以不带任何参数调用，但大多数时候需要将一个对象或字符串传递给您的 `submitHandler` 。

将您的结果作为第一个参数传递。 团队将调用的 `submitHandler` 位置 `err` `null` ，并且 `result` 将为您传递到的对象/字符串 `submitTask()` 。 如果 `submitTask()` 使用参数进行调用 `result` ，则**必须**传递一个或多 `appId` 个 `appId` 字符串数组：这允许团队验证发送结果的应用程序是否与调用任务模块的应用程序相同。

### <a name="adaptive-card-taskinfocard"></a>自适应卡片（ `TaskInfo.card` ）

如果调用任务模块时使用的是 `submitHandler` ，当用户按下按钮时， `Action.Submit` 卡片中的值将作为的值返回 `result` 。 如果用户按 Esc 按钮或按 X， `err` 则将改为返回。 或者，如果您的应用程序包含一个 bot 以及一个选项卡，您只需在 `appId` 对象的值中包含 bot 的 `completionBotId` `TaskInfo` 。 自适应卡片正文（由用户填写）将在 `task/submit invoke` 用户按下按钮时通过消息发送到机器人 `Action.Submit` 。 您接收的对象的架构与[您收到的用于任务/提取和任务/提交邮件的架构](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)非常相似;唯一的区别在于，JSON 对象的架构是一个自适应卡片对象，而不是*包含*自适应卡片对象的对象，就像[在使用自适应卡片时使用 bot](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)一样。

## <a name="example-submitting-the-result-of-a-task-module"></a>示例：提交任务模块的结果

使用 HTML 表单撤回[上面的任务模块中的表单](#example-invoking-a-task-module)。 以下是定义表单的位置：

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

此窗体上有五个字段，但我们只对其中三个字段的值感兴趣，例如： `name` 、 `email` 和 `favoriteBook` 。

下面是 `validateForm()` 调用的函数 `submitTask()` ：

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

以下是 `err` 可由您接收到的可能值 `submitHandler` ：

| 问题 | 错误消息（值为 `err` ） |
| ------- | ------------------------------ |
| `TaskInfo.url`已指定和的值 `TaskInfo.card` 。 | "同时指定了卡片和 url 的值。 允许使用其中一个或另一个，但不是两者。 |
| 既 `TaskInfo.url` 不 `TaskInfo.card` 指定也不指定。 | "必须为卡片或 url 指定值。" |
| 无效 `appId` 。 | "AppId 无效。" |
| 用户已按 X 按钮，然后关闭它。 | "用户取消/关闭了任务模块"。 |
