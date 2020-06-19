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
# <a name="using-task-modules-in-tabs"></a><span data-ttu-id="6b418-104">在选项卡中使用任务模块</span><span class="sxs-lookup"><span data-stu-id="6b418-104">Using task modules in tabs</span></span>

<span data-ttu-id="6b418-105">将任务模块添加到选项卡后，可以大大简化用户对需要数据输入的任何工作流的体验。</span><span class="sxs-lookup"><span data-stu-id="6b418-105">Adding a task module to your tab can greatly simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="6b418-106">任务模块允许您在工作组感知弹出窗口中收集其输入信息。</span><span class="sxs-lookup"><span data-stu-id="6b418-106">Task modules allow you to gather their input in a Teams-aware popup.</span></span> <span data-ttu-id="6b418-107">此示例的一个很有用的示例是编辑 Planner 卡片;您可以使用任务模块来创建类似的体验。</span><span class="sxs-lookup"><span data-stu-id="6b418-107">A good example of this is editing Planner cards; you can use task modules to create a similar experience.</span></span>

<span data-ttu-id="6b418-108">若要支持任务模块功能， [Microsoft 团队客户端 SDK](/javascript/api/overview/msteams-client)中添加了两个新函数：</span><span class="sxs-lookup"><span data-stu-id="6b418-108">To support the task module feature, two new functions were added to the [Microsoft Teams client SDK](/javascript/api/overview/msteams-client):</span></span>

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

<span data-ttu-id="6b418-109">我们来看看每个方法的工作方式。</span><span class="sxs-lookup"><span data-stu-id="6b418-109">Let's see how each of them work.</span></span>

## <a name="invoking-a-task-module-from-a-tab"></a><span data-ttu-id="6b418-110">从选项卡调用任务模块</span><span class="sxs-lookup"><span data-stu-id="6b418-110">Invoking a task module from a tab</span></span>

<span data-ttu-id="6b418-111">若要从选项卡调用任务模块，请使用 `microsoftTeams.tasks.startTask()` 传递[TaskInfo 对象](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)和可选的 `submitHandler` 回调函数。</span><span class="sxs-lookup"><span data-stu-id="6b418-111">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="6b418-112">如上文所述，有两种情况需要考虑：</span><span class="sxs-lookup"><span data-stu-id="6b418-112">As described earlier, there are two cases to consider:</span></span>

1. <span data-ttu-id="6b418-113">的值 `TaskInfo.url` 设置为 URL。</span><span class="sxs-lookup"><span data-stu-id="6b418-113">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="6b418-114">将显示 "任务模块" 窗口，并 `TaskModule.url` 将 `<iframe>` 其加载为内部。</span><span class="sxs-lookup"><span data-stu-id="6b418-114">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="6b418-115">该页面上的 JavaScript 应调用 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="6b418-115">JavaScript on that page should call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="6b418-116">如果 `submitHandler` 页面上有一个函数，并且调用时出现错误 `microsoftTeams.tasks.startTask()` ，则会调用，并将其 `submitHandler` `err` 设置为错误字符串，以指示如下所述[below](#task-module-invocation-errors)的错误。</span><span class="sxs-lookup"><span data-stu-id="6b418-116">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the error as described [below](#task-module-invocation-errors).</span></span>
1. <span data-ttu-id="6b418-117">的值 `taskInfo.card` 是[自适应卡片的 JSON](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)。</span><span class="sxs-lookup"><span data-stu-id="6b418-117">The value of `taskInfo.card` is the [JSON for an Adaptive card](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="6b418-118">在这种情况下，在 `submitHandler` 用户关闭或按下自适应卡片上的按钮时，显然没有任何要调用的 JavaScript 函数; 通过将结果传递给 bot，接收用户输入的内容的唯一方法。</span><span class="sxs-lookup"><span data-stu-id="6b418-118">In this case there's obviously not any JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive card; the only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="6b418-119">若要从选项卡中使用自适应卡片任务模块，您的应用程序必须包括用于从用户获取任何信息的 bot。</span><span class="sxs-lookup"><span data-stu-id="6b418-119">To use an Adaptive card task module from a tab your app must include a bot to get any information back from the user.</span></span> <span data-ttu-id="6b418-120">下面对此进行了说明。</span><span class="sxs-lookup"><span data-stu-id="6b418-120">This is explained below.</span></span>

## <a name="example-invoking-a-task-module"></a><span data-ttu-id="6b418-121">示例：调用任务模块</span><span class="sxs-lookup"><span data-stu-id="6b418-121">Example: Invoking a task module</span></span>

<span data-ttu-id="6b418-122">下面的代码适用于[任务模块示例](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples)。</span><span class="sxs-lookup"><span data-stu-id="6b418-122">The code below is adapted from [the task module sample](~/task-modules-and-cards/what-are-task-modules.md#task-module-samples).</span></span> <span data-ttu-id="6b418-123">任务模块如下所示：</span><span class="sxs-lookup"><span data-stu-id="6b418-123">Here's what the task module looks like:</span></span>

![任务模块-自定义窗体](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="6b418-125">`submitHandler`这非常简单; 它只是回显控制台的值 `err` `result` ：</span><span class="sxs-lookup"><span data-stu-id="6b418-125">The `submitHandler` is very simple; it just echoes the value of `err` or `result` to the console:</span></span>

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

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="6b418-126">提交任务模块的结果</span><span class="sxs-lookup"><span data-stu-id="6b418-126">Submitting the result of a task module</span></span>

<span data-ttu-id="6b418-127">`submitHandler`函数与一起使用 `TaskInfo.url` 。</span><span class="sxs-lookup"><span data-stu-id="6b418-127">The `submitHandler` function is used with `TaskInfo.url`.</span></span> <span data-ttu-id="6b418-128">`submitHandler`函数驻留在网页中 `TaskInfo.url` 。</span><span class="sxs-lookup"><span data-stu-id="6b418-128">The `submitHandler` function resides in the `TaskInfo.url` web page.</span></span> <span data-ttu-id="6b418-129">如果调用任务模块时出现错误 `submitHandler` ，将立即使用 `err` 指示发生了哪种[错误](#task-module-invocation-errors)的字符串来调用函数。</span><span class="sxs-lookup"><span data-stu-id="6b418-129">If there's an error when invoking the task module your `submitHandler` function will be immediately invoked with an `err` string indicating which [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="6b418-130">`submitHandler` `err` 当用户按下位于任务模块右上角的 X 时，也可以使用字符串调用函数。</span><span class="sxs-lookup"><span data-stu-id="6b418-130">The `submitHandler` function is also called with an `err` string when the user presses the X at the upper right of task module.</span></span>

<span data-ttu-id="6b418-131">如果没有调用错误，并且用户没有按 X 关闭它，则用户在完成时按下一个按钮。</span><span class="sxs-lookup"><span data-stu-id="6b418-131">If there's no invocation error and the user doesn't press X to dismiss it, the user presses a button when finished.</span></span> <span data-ttu-id="6b418-132">根据任务模块中的 URL 或自适应卡片的不同，将发生以下情况：</span><span class="sxs-lookup"><span data-stu-id="6b418-132">Depending on whether it's a URL or an Adaptive card in the task module, here's what happens:</span></span>

### <a name="htmljavascript-taskinfourl"></a><span data-ttu-id="6b418-133">HTML/JavaScript （ `TaskInfo.url` ）</span><span class="sxs-lookup"><span data-stu-id="6b418-133">HTML/JavaScript (`TaskInfo.url`)</span></span>

<span data-ttu-id="6b418-134">验证用户输入的内容后，您就可以调用 `microsoftTeams.tasks.submitTask()` SDK 函数（在以后 `submitTask()` 出于可读性目的而引用）。</span><span class="sxs-lookup"><span data-stu-id="6b418-134">Once you've validated what the user has entered you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="6b418-135">`submitTask()`如果只想要团队关闭任务模块，则可以不带任何参数调用，但大多数时候需要将一个对象或字符串传递给您的 `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="6b418-135">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="6b418-136">将您的结果作为第一个参数传递。</span><span class="sxs-lookup"><span data-stu-id="6b418-136">Pass your result as the first parameter.</span></span> <span data-ttu-id="6b418-137">团队将调用的 `submitHandler` 位置 `err` `null` ，并且 `result` 将为您传递到的对象/字符串 `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="6b418-137">Teams will invoke `submitHandler` where `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="6b418-138">如果 `submitTask()` 使用参数进行调用 `result` ，则**必须**传递一个或多 `appId` 个 `appId` 字符串数组：这允许团队验证发送结果的应用程序是否与调用任务模块的应用程序相同。</span><span class="sxs-lookup"><span data-stu-id="6b418-138">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="6b418-139">自适应卡片（ `TaskInfo.card` ）</span><span class="sxs-lookup"><span data-stu-id="6b418-139">Adaptive card (`TaskInfo.card`)</span></span>

<span data-ttu-id="6b418-140">如果调用任务模块时使用的是 `submitHandler` ，当用户按下按钮时， `Action.Submit` 卡片中的值将作为的值返回 `result` 。</span><span class="sxs-lookup"><span data-stu-id="6b418-140">If you invoked the task module with a `submitHandler`, when the user presses an `Action.Submit` button the values in the card will be returned as the value of `result`.</span></span> <span data-ttu-id="6b418-141">如果用户按 Esc 按钮或按 X， `err` 则将改为返回。</span><span class="sxs-lookup"><span data-stu-id="6b418-141">If the user presses the Esc button or presses the X, `err` will be returned instead.</span></span> <span data-ttu-id="6b418-142">或者，如果您的应用程序包含一个 bot 以及一个选项卡，您只需在 `appId` 对象的值中包含 bot 的 `completionBotId` `TaskInfo` 。</span><span class="sxs-lookup"><span data-stu-id="6b418-142">Alternatively, if your app contains a bot in addition to a tab you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="6b418-143">自适应卡片正文（由用户填写）将在 `task/submit invoke` 用户按下按钮时通过消息发送到机器人 `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="6b418-143">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit invoke` message when the user presses an `Action.Submit` button.</span></span> <span data-ttu-id="6b418-144">您接收的对象的架构与[您收到的用于任务/提取和任务/提交邮件的架构](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)非常相似;唯一的区别在于，JSON 对象的架构是一个自适应卡片对象，而不是*包含*自适应卡片对象的对象，就像[在使用自适应卡片时使用 bot](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)一样。</span><span class="sxs-lookup"><span data-stu-id="6b418-144">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); the only difference is that the schema of the JSON object is an Adaptive card object as opposed to an object *containing* an Adaptive card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

## <a name="example-submitting-the-result-of-a-task-module"></a><span data-ttu-id="6b418-145">示例：提交任务模块的结果</span><span class="sxs-lookup"><span data-stu-id="6b418-145">Example: submitting the result of a task module</span></span>

<span data-ttu-id="6b418-146">使用 HTML 表单撤回[上面的任务模块中的表单](#example-invoking-a-task-module)。</span><span class="sxs-lookup"><span data-stu-id="6b418-146">Recall the [form in the task module above](#example-invoking-a-task-module) with an HTML form.</span></span> <span data-ttu-id="6b418-147">以下是定义表单的位置：</span><span class="sxs-lookup"><span data-stu-id="6b418-147">Here's where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="6b418-148">此窗体上有五个字段，但我们只对其中三个字段的值感兴趣，例如： `name` 、 `email` 和 `favoriteBook` 。</span><span class="sxs-lookup"><span data-stu-id="6b418-148">There are five fields on this form but we're only interested in the values of three of them for this example: `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="6b418-149">下面是 `validateForm()` 调用的函数 `submitTask()` ：</span><span class="sxs-lookup"><span data-stu-id="6b418-149">Here's the `validateForm()` function that calls `submitTask()`:</span></span>

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

## <a name="task-module-invocation-errors"></a><span data-ttu-id="6b418-150">任务模块调用错误</span><span class="sxs-lookup"><span data-stu-id="6b418-150">Task module invocation errors</span></span>

<span data-ttu-id="6b418-151">以下是 `err` 可由您接收到的可能值 `submitHandler` ：</span><span class="sxs-lookup"><span data-stu-id="6b418-151">Here are the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="6b418-152">问题</span><span class="sxs-lookup"><span data-stu-id="6b418-152">Problem</span></span> | <span data-ttu-id="6b418-153">错误消息（值为 `err` ）</span><span class="sxs-lookup"><span data-stu-id="6b418-153">Error message (value of `err`)</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="6b418-154">`TaskInfo.url`已指定和的值 `TaskInfo.card` 。</span><span class="sxs-lookup"><span data-stu-id="6b418-154">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="6b418-155">"同时指定了卡片和 url 的值。</span><span class="sxs-lookup"><span data-stu-id="6b418-155">"Values for both card and url were specified.</span></span> <span data-ttu-id="6b418-156">允许使用其中一个或另一个，但不是两者。</span><span class="sxs-lookup"><span data-stu-id="6b418-156">One or the other, but not both, are allowed."</span></span> |
| <span data-ttu-id="6b418-157">既 `TaskInfo.url` 不 `TaskInfo.card` 指定也不指定。</span><span class="sxs-lookup"><span data-stu-id="6b418-157">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="6b418-158">"必须为卡片或 url 指定值。"</span><span class="sxs-lookup"><span data-stu-id="6b418-158">"You must specify a value for either card or url."</span></span> |
| <span data-ttu-id="6b418-159">无效 `appId` 。</span><span class="sxs-lookup"><span data-stu-id="6b418-159">Invalid `appId`.</span></span> | <span data-ttu-id="6b418-160">"AppId 无效。"</span><span class="sxs-lookup"><span data-stu-id="6b418-160">"Invalid appId."</span></span> |
| <span data-ttu-id="6b418-161">用户已按 X 按钮，然后关闭它。</span><span class="sxs-lookup"><span data-stu-id="6b418-161">User pressed X button, closing it.</span></span> | <span data-ttu-id="6b418-162">"用户取消/关闭了任务模块"。</span><span class="sxs-lookup"><span data-stu-id="6b418-162">"User cancelled/closed the task module."</span></span> |
