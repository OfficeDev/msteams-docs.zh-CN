---
title: 使用 Microsoft Teams 选项卡中的任务模块
description: 介绍如何使用 Microsoft Teams 客户端 SDK 从 Teams 选项卡调用任务模块
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
# <a name="using-task-modules-in-tabs"></a><span data-ttu-id="90019-104">在选项卡中使用任务模块</span><span class="sxs-lookup"><span data-stu-id="90019-104">Using task modules in tabs</span></span>

<span data-ttu-id="90019-105">将任务模块添加到选项卡可以大大简化任何需要数据输入的工作流的用户体验。</span><span class="sxs-lookup"><span data-stu-id="90019-105">Adding a task module to your tab can greatly simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="90019-106">任务模块允许你在 Teams 感知弹出窗口中收集他们的输入。</span><span class="sxs-lookup"><span data-stu-id="90019-106">Task modules allow you to gather their input in a Teams-aware popup.</span></span> <span data-ttu-id="90019-107">一个很好的示例是编辑 Planner 卡;可以使用任务模块来创建类似的体验。</span><span class="sxs-lookup"><span data-stu-id="90019-107">A good example of this is editing Planner cards; you can use task modules to create a similar experience.</span></span>

<span data-ttu-id="90019-108">为了支持任务模块功能，向 Microsoft Teams 客户端 SDK 添加了两 [个新函数](/javascript/api/overview/msteams-client)：</span><span class="sxs-lookup"><span data-stu-id="90019-108">To support the task module feature, two new functions were added to the [Microsoft Teams client SDK](/javascript/api/overview/msteams-client):</span></span>

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

<span data-ttu-id="90019-109">下面我们了解一下每个功能如何工作。</span><span class="sxs-lookup"><span data-stu-id="90019-109">Let's see how each of them work.</span></span>

## <a name="invoking-a-task-module-from-a-tab"></a><span data-ttu-id="90019-110">从选项卡调用任务模块</span><span class="sxs-lookup"><span data-stu-id="90019-110">Invoking a task module from a tab</span></span>

<span data-ttu-id="90019-111">若要从选项卡调用任务模块，请使用 `microsoftTeams.tasks.startTask()` 传递 [TaskInfo 对象](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) 和可选回调 `submitHandler` 函数。</span><span class="sxs-lookup"><span data-stu-id="90019-111">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="90019-112">如前面所述，有两种情况需要考虑：</span><span class="sxs-lookup"><span data-stu-id="90019-112">As described earlier, there are two cases to consider:</span></span>

1. <span data-ttu-id="90019-113">的值设置为 `TaskInfo.url` URL。</span><span class="sxs-lookup"><span data-stu-id="90019-113">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="90019-114">任务模块窗口将显示 `TaskModule.url` ，并作为一个内部 `<iframe>` 窗口加载。</span><span class="sxs-lookup"><span data-stu-id="90019-114">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="90019-115">该页面上的 JavaScript 应调用 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="90019-115">JavaScript on that page should call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="90019-116">如果页面上有函数，并且调用 时出错，则调用 时将 设置为 指示错误的错误字符串， `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` [如下所述](#task-module-invocation-errors)。</span><span class="sxs-lookup"><span data-stu-id="90019-116">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the error as described [below](#task-module-invocation-errors).</span></span>
1. <span data-ttu-id="90019-117">的值 `taskInfo.card` 是自适应卡片[的 JSON。](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)</span><span class="sxs-lookup"><span data-stu-id="90019-117">The value of `taskInfo.card` is the [JSON for an Adaptive card](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="90019-118">在这种情况下，明显没有任何 JavaScript 函数在用户关闭或按下自适应卡片上的按钮时调用;接收用户输入内容的唯一方法就是将结果传递给机器人 `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="90019-118">In this case there's obviously not any JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive card; the only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="90019-119">若要从选项卡使用自适应卡片任务模块，应用必须包含自动程序才能从用户获取任何信息。</span><span class="sxs-lookup"><span data-stu-id="90019-119">To use an Adaptive card task module from a tab your app must include a bot to get any information back from the user.</span></span> <span data-ttu-id="90019-120">下面对此进行了说明。</span><span class="sxs-lookup"><span data-stu-id="90019-120">This is explained below.</span></span>

## <a name="example-invoking-a-task-module"></a><span data-ttu-id="90019-121">示例：调用任务模块</span><span class="sxs-lookup"><span data-stu-id="90019-121">Example: Invoking a task module</span></span>

<span data-ttu-id="90019-122">下面的代码改编自任务 [模块示例](~/task-modules-and-cards/what-are-task-modules.md#code-sample)。</span><span class="sxs-lookup"><span data-stu-id="90019-122">The code below is adapted from [the task module sample](~/task-modules-and-cards/what-are-task-modules.md#code-sample).</span></span> <span data-ttu-id="90019-123">任务模块如下所示：</span><span class="sxs-lookup"><span data-stu-id="90019-123">Here's what the task module looks like:</span></span>

![任务模块 - 自定义窗体](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="90019-125">非常简单;它只是将 的值回显到 `submitHandler` `err` 控制台 `result` ：</span><span class="sxs-lookup"><span data-stu-id="90019-125">The `submitHandler` is very simple; it just echoes the value of `err` or `result` to the console:</span></span>

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

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="90019-126">提交任务模块的结果</span><span class="sxs-lookup"><span data-stu-id="90019-126">Submitting the result of a task module</span></span>

<span data-ttu-id="90019-127">函数 `submitHandler` 与 一同使用 `TaskInfo.url` 。</span><span class="sxs-lookup"><span data-stu-id="90019-127">The `submitHandler` function is used with `TaskInfo.url`.</span></span> <span data-ttu-id="90019-128">`submitHandler`函数驻留在 `TaskInfo.url` 网页中。</span><span class="sxs-lookup"><span data-stu-id="90019-128">The `submitHandler` function resides in the `TaskInfo.url` web page.</span></span> <span data-ttu-id="90019-129">如果在调用任务模块时出现错误，函数将立即调用，并包含指示发生了哪个 `submitHandler` `err` [错误的字符串](#task-module-invocation-errors)。</span><span class="sxs-lookup"><span data-stu-id="90019-129">If there's an error when invoking the task module your `submitHandler` function will be immediately invoked with an `err` string indicating which [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="90019-130">当用户按任务模块右上角的 X 时，也会使用字符串调用 `submitHandler` `err` 函数。</span><span class="sxs-lookup"><span data-stu-id="90019-130">The `submitHandler` function is also called with an `err` string when the user presses the X at the upper right of task module.</span></span>

<span data-ttu-id="90019-131">如果没有调用错误，并且用户不按 X 消除它，则用户完成后按下一个按钮。</span><span class="sxs-lookup"><span data-stu-id="90019-131">If there's no invocation error and the user doesn't press X to dismiss it, the user presses a button when finished.</span></span> <span data-ttu-id="90019-132">根据它是任务模块中的 URL 还是自适应卡片，下面是发生的情况：</span><span class="sxs-lookup"><span data-stu-id="90019-132">Depending on whether it's a URL or an Adaptive card in the task module, here's what happens:</span></span>

### <a name="htmljavascript-taskinfourl"></a><span data-ttu-id="90019-133">HTML/JavaScript `TaskInfo.url` () </span><span class="sxs-lookup"><span data-stu-id="90019-133">HTML/JavaScript (`TaskInfo.url`)</span></span>

<span data-ttu-id="90019-134">验证用户输入了哪些信息后，调用 SDK 函数 (以下称为" `microsoftTeams.tasks.submitTask()` `submitTask()` 可读性") 。</span><span class="sxs-lookup"><span data-stu-id="90019-134">Once you've validated what the user has entered you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="90019-135">如果你仅希望 Teams 关闭任务模块，但大多数情况下你想要将对象或字符串传递到 你的 ，你可以调用不带任何 `submitTask()` 参数 `submitHandler` 的 。</span><span class="sxs-lookup"><span data-stu-id="90019-135">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="90019-136">将结果作为第一个参数传递。</span><span class="sxs-lookup"><span data-stu-id="90019-136">Pass your result as the first parameter.</span></span> <span data-ttu-id="90019-137">Teams 将 `submitHandler` 调用 `err` 位置， `null` `result` 并且将是你传递给 的对象/字符串 `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="90019-137">Teams will invoke `submitHandler` where `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="90019-138">如果使用 参数调用 ，则必须传递 或 字符串数组：这允许 Teams 验证发送结果的应用是否与调用任务模块的应用 `submitTask()` `result`  `appId` `appId` 相同。</span><span class="sxs-lookup"><span data-stu-id="90019-138">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="90019-139">自适应卡片 `TaskInfo.card` () </span><span class="sxs-lookup"><span data-stu-id="90019-139">Adaptive card (`TaskInfo.card`)</span></span>

<span data-ttu-id="90019-140">如果使用 调用任务模块，当用户按下按钮时，卡片中的值将返回 `submitHandler` `Action.Submit` 为 的值 `result` 。</span><span class="sxs-lookup"><span data-stu-id="90019-140">If you invoked the task module with a `submitHandler`, when the user presses an `Action.Submit` button the values in the card will be returned as the value of `result`.</span></span> <span data-ttu-id="90019-141">如果用户按下 Esc 按钮或按 X， `err` 将改为返回 。</span><span class="sxs-lookup"><span data-stu-id="90019-141">If the user presses the Esc button or presses the X, `err` will be returned instead.</span></span> <span data-ttu-id="90019-142">或者，如果你的应用包含除选项卡外还包含自动程序，则只需在 对象中包含 自动程序 作为 `appId` `completionBotId` `TaskInfo` 的值。</span><span class="sxs-lookup"><span data-stu-id="90019-142">Alternatively, if your app contains a bot in addition to a tab you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="90019-143">用户 (填充的自适应卡片正文) 当用户按下按钮时，会通过一条消息发送给 `task/submit invoke` `Action.Submit` 自动程序。</span><span class="sxs-lookup"><span data-stu-id="90019-143">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit invoke` message when the user presses an `Action.Submit` button.</span></span> <span data-ttu-id="90019-144">您接收的对象的架构与针对任务/提取和任务/提交消息接收[的架构非常相似](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages);唯一的区别是 JSON 对象的架构是自适应卡片对象，而不是包含自适应卡片对象的对象，就像自适应卡片用于[机器人一样](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)。</span><span class="sxs-lookup"><span data-stu-id="90019-144">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); the only difference is that the schema of the JSON object is an Adaptive card object as opposed to an object *containing* an Adaptive card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

## <a name="example-submitting-the-result-of-a-task-module"></a><span data-ttu-id="90019-145">示例：提交任务模块的结果</span><span class="sxs-lookup"><span data-stu-id="90019-145">Example: submitting the result of a task module</span></span>

<span data-ttu-id="90019-146">使用 HTML [窗体撤回](#example-invoking-a-task-module) 上述任务模块中的窗体。</span><span class="sxs-lookup"><span data-stu-id="90019-146">Recall the [form in the task module above](#example-invoking-a-task-module) with an HTML form.</span></span> <span data-ttu-id="90019-147">下面是定义表单的地方：</span><span class="sxs-lookup"><span data-stu-id="90019-147">Here's where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="90019-148">此窗体上有五个字段，但我们仅对此示例中的三个字段的值感兴趣：、 `name` `email` 和 `favoriteBook` 。</span><span class="sxs-lookup"><span data-stu-id="90019-148">There are five fields on this form but we're only interested in the values of three of them for this example: `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="90019-149">下面是调用 `validateForm()` 的函数 `submitTask()` ：</span><span class="sxs-lookup"><span data-stu-id="90019-149">Here's the `validateForm()` function that calls `submitTask()`:</span></span>

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

## <a name="task-module-invocation-errors"></a><span data-ttu-id="90019-150">任务模块调用错误</span><span class="sxs-lookup"><span data-stu-id="90019-150">Task module invocation errors</span></span>

<span data-ttu-id="90019-151">下面是你的 `err` 可以接收的可能值 `submitHandler` ：</span><span class="sxs-lookup"><span data-stu-id="90019-151">Here are the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="90019-152">问题</span><span class="sxs-lookup"><span data-stu-id="90019-152">Problem</span></span> | <span data-ttu-id="90019-153">错误消息 (值 `err`) </span><span class="sxs-lookup"><span data-stu-id="90019-153">Error message (value of `err`)</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="90019-154">指定了 和 `TaskInfo.url` `TaskInfo.card` 的值。</span><span class="sxs-lookup"><span data-stu-id="90019-154">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="90019-155">"已指定 card 和 url 的值。</span><span class="sxs-lookup"><span data-stu-id="90019-155">"Values for both card and url were specified.</span></span> <span data-ttu-id="90019-156">允许一个或另一个，但不能同时使用这两者。"</span><span class="sxs-lookup"><span data-stu-id="90019-156">One or the other, but not both, are allowed."</span></span> |
| <span data-ttu-id="90019-157">既不 `TaskInfo.url` 指定也不 `TaskInfo.card` 指定。</span><span class="sxs-lookup"><span data-stu-id="90019-157">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="90019-158">"你必须为卡片或 url 指定值。"</span><span class="sxs-lookup"><span data-stu-id="90019-158">"You must specify a value for either card or url."</span></span> |
| <span data-ttu-id="90019-159">无效 `appId` 。</span><span class="sxs-lookup"><span data-stu-id="90019-159">Invalid `appId`.</span></span> | <span data-ttu-id="90019-160">"invalid appId."</span><span class="sxs-lookup"><span data-stu-id="90019-160">"Invalid appId."</span></span> |
| <span data-ttu-id="90019-161">用户按下 X 按钮，关闭它。</span><span class="sxs-lookup"><span data-stu-id="90019-161">User pressed X button, closing it.</span></span> | <span data-ttu-id="90019-162">"用户已取消/关闭任务模块。"</span><span class="sxs-lookup"><span data-stu-id="90019-162">"User cancelled/closed the task module."</span></span> |
