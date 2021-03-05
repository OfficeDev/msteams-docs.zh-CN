---
title: 在 Microsoft Teams 选项卡中使用任务模块
description: 介绍如何使用 Microsoft Teams 客户端 SDK 从 Teams 选项卡调用任务模块。
keywords: 任务模块团队选项卡客户端 sdk
ms.openlocfilehash: 3f1da4d5eec31638d69adc01a45831534d015f41
ms.sourcegitcommit: 5cb3453e918bec1173899e7591b48a48113cf8f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/04/2021
ms.locfileid: "50449554"
---
# <a name="using-task-modules-in-tabs"></a>在选项卡中使用任务模块

将任务模块添加到选项卡可以大大简化需要数据输入的任何工作流的用户体验。 任务模块允许你在 Teams 感知弹出窗口中收集其输入。 一个很好的示例是编辑 Planner 卡;可以使用任务模块来创建类似的体验。

为了支持任务模块功能，向 Microsoft Teams 客户端 SDK 添加了两 [个新函数](/javascript/api/overview/msteams-client)：

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

让我们看一下每个功能如何工作。

## <a name="invoking-a-task-module-from-a-tab"></a>从选项卡调用任务模块

若要从选项卡调用任务模块，请使用 `microsoftTeams.tasks.startTask()` 传递 [TaskInfo 对象](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) 和可选 `submitHandler` 回调函数。 如前面所述，有两种情况需要考虑：

1. 值设置为 `TaskInfo.url` URL。 任务模块窗口将显示 `TaskModule.url` 并作为内部 `<iframe>` 加载。 该页上的 JavaScript 应调用 `microsoftTeams.initialize()` 。 如果页面上有一个函数，并且调用时出错，则调用设置为指示错误的错误字符串， `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` 如下 [所述](#task-module-invocation-errors)。
1. 的值为 `taskInfo.card` 自适应[卡片的 JSON。](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment) 在这种情况下，在用户关闭或按下自适应卡片上的按钮时，明显没有任何 JavaScript 函数可调用;接收用户输入内容的唯一方法就是将结果传递给机器人。 `submitHandler` 若要从选项卡使用自适应卡片任务模块，应用必须包含自动程序才能从用户获取任何信息。 下面对此进行了说明。

## <a name="example-invoking-a-task-module"></a>示例：调用任务模块

下面的代码改编自任务 [模块示例](~/task-modules-and-cards/what-are-task-modules.md#code-sample)。 任务模块如下所示：

![任务模块 - 自定义窗体](~/assets/images/task-module/task-module-custom-form.png)

非常简单 `submitHandler` ;它只是将控制台的值 `err` 回显 `result` ：

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

该 `submitHandler` 函数与 `TaskInfo.url` 。 `submitHandler`该函数驻留在 `TaskInfo.url` 网页中。 如果在调用任务模块时出错，函数将立即调用，并包含一个指示发生了 `submitHandler` `err` 错误的 [字符串](#task-module-invocation-errors)。 当用户按任务模块右上角的 X 时，也会使用字符串调用 `submitHandler` `err` 该函数。

如果没有调用错误，并且用户不按 X 来消除它，则用户完成后按一个按钮。 根据它是任务模块中的 URL 还是自适应卡片，以下是发生的情况：

### <a name="htmljavascript-taskinfourl"></a>HTML/JavaScript `TaskInfo.url` () 

验证用户输入的信息后， (为了可读性目的调用 SDK 函数 `microsoftTeams.tasks.submitTask()` `submitTask()`) 。 如果你仅希望 Teams 关闭任务模块，但在大多数情况下，你想要将对象或字符串传递给你的 ，你可以调用不带任何 `submitTask()` 参数 `submitHandler` 。

将结果作为第一个参数传递。 Teams 将 `submitHandler` 调用 `err` 将在何处 `null` ， `result` 并且将是你传递给的对象/字符串 `submitTask()` 。 如果使用参数调用，则必须传递字符串数组或字符串数组：这允许 Teams 验证发送结果的应用是否与调用任务模块的应用 `submitTask()` `result`  `appId` `appId` 相同。

### <a name="adaptive-card-taskinfocard"></a>自适应卡片 `TaskInfo.card` () 

如果使用 a 调用任务模块，当用户按下按钮时，卡片中的值将返回 `submitHandler` `Action.Submit` 为 `result` 值 。 如果用户按下 Esc 按钮或按 X， `err` 将改为返回。 或者，如果你的应用除了包含选项卡外还包含自动程序，你只需将机器人的值包含在 `appId` `completionBotId` 对象 `TaskInfo` 中。 当用户按下 (时，自适应卡片正文) 会通过消息发送给自动 `task/submit invoke` `Action.Submit` 程序。 您接收的对象的架构与接收任务/提取和[任务/](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)提交消息的架构非常相似;唯一的区别是，JSON 对象的架构是自适应卡片对象，而不是包含自适应卡片对象的对象，就像自适应卡片与机器人一[样。](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)

## <a name="example-submitting-the-result-of-a-task-module"></a>示例：提交任务模块的结果

使用 [HTML 表单](#example-invoking-a-task-module) 调用上述任务模块中的表单。 下面是定义表单的地方：

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

此窗体上有五个字段，但我们仅对此示例中三个字段的值感兴趣：、 `name` `email` 和 `favoriteBook` 。

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

下面是以下可能 `err` 的值，可通过以下帐户接收 `submitHandler` ：

| 问题 | 错误消息 (`err` 值)  |
| ------- | ------------------------------ |
| 同时指定了 `TaskInfo.url` 这两 `TaskInfo.card` 个值。 | "已指定卡和 url 的值。 允许一个或另一个，但不能同时允许这两者。" |
| 既不 `TaskInfo.url` 指定也不 `TaskInfo.card` 指定。 | "必须为卡片或 url 指定值。" |
| 无效 `appId` 。 | "appId 无效。" |
| 用户按下 X 按钮，关闭它。 | "用户已取消/关闭任务模块。" |
