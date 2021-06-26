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
# <a name="use-task-modules-in-tabs"></a><span data-ttu-id="c2b80-104">在选项卡中使用任务模块</span><span class="sxs-lookup"><span data-stu-id="c2b80-104">Use task modules in tabs</span></span>

<span data-ttu-id="c2b80-105">向选项卡添加任务模块，以简化任何需要数据输入的工作流的用户体验。</span><span class="sxs-lookup"><span data-stu-id="c2b80-105">Add a task module to your tab to simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="c2b80-106">任务模块允许你在 Microsoft 弹出窗口中收集Teams-Aware输入。</span><span class="sxs-lookup"><span data-stu-id="c2b80-106">Task modules allow you to gather their input in a Microsoft Teams-Aware pop-up.</span></span> <span data-ttu-id="c2b80-107">编辑 Planner 卡就是一个很好的示例。</span><span class="sxs-lookup"><span data-stu-id="c2b80-107">A good example of this is editing Planner cards.</span></span> <span data-ttu-id="c2b80-108">可以使用任务模块来创建类似的体验。</span><span class="sxs-lookup"><span data-stu-id="c2b80-108">You can use task modules to create a similar experience.</span></span>

<span data-ttu-id="c2b80-109">为了支持任务模块功能，向 Teams SDK 添加了两[个新函数](/javascript/api/overview/msteams-client)。</span><span class="sxs-lookup"><span data-stu-id="c2b80-109">To support the task module feature, two new functions are added to the [Teams client SDK](/javascript/api/overview/msteams-client).</span></span> <span data-ttu-id="c2b80-110">以下代码显示了这两个函数的示例：</span><span class="sxs-lookup"><span data-stu-id="c2b80-110">The following code shows an example of these two functions:</span></span>

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

<span data-ttu-id="c2b80-111">你可以了解从选项卡调用任务模块和提交任务模块结果的工作原理。</span><span class="sxs-lookup"><span data-stu-id="c2b80-111">You can see how invoking a task module from a tab and submitting the result of a task module works.</span></span>

## <a name="invoke-a-task-module-from-a-tab"></a><span data-ttu-id="c2b80-112">从选项卡调用任务模块</span><span class="sxs-lookup"><span data-stu-id="c2b80-112">Invoke a task module from a tab</span></span>

<span data-ttu-id="c2b80-113">若要从选项卡调用任务模块，请使用 `microsoftTeams.tasks.startTask()` 传递 [TaskInfo 对象](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) 和可选回调 `submitHandler` 函数。</span><span class="sxs-lookup"><span data-stu-id="c2b80-113">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="c2b80-114">有两种情况需要考虑：</span><span class="sxs-lookup"><span data-stu-id="c2b80-114">There are two cases to consider:</span></span>

* <span data-ttu-id="c2b80-115">的值设置为 `TaskInfo.url` URL。</span><span class="sxs-lookup"><span data-stu-id="c2b80-115">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="c2b80-116">任务模块窗口将显示 `TaskModule.url` ，并作为一个内部 `<iframe>` 窗口加载。</span><span class="sxs-lookup"><span data-stu-id="c2b80-116">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="c2b80-117">该页面上的 JavaScript 调用 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="c2b80-117">JavaScript on that page calls `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="c2b80-118">如果页面上有函数，并且调用 时出错，则调用 时将 设置为指示相同错误 `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` 字符串。</span><span class="sxs-lookup"><span data-stu-id="c2b80-118">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the same.</span></span> <span data-ttu-id="c2b80-119">有关详细信息，请参阅任务 [模块调用错误](#task-module-invocation-errors)。</span><span class="sxs-lookup"><span data-stu-id="c2b80-119">For more information, see [task module invocation errors](#task-module-invocation-errors).</span></span>
* <span data-ttu-id="c2b80-120">的值 `taskInfo.card` 是自适应[卡片的 JSON。](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)</span><span class="sxs-lookup"><span data-stu-id="c2b80-120">The value of `taskInfo.card` is the [JSON for an Adaptive Card](~/task-modules-and-cards/task-modules/invoking-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="c2b80-121">当用户关闭或按下自适应卡片上的按钮时，没有要调用的 JavaScript `submitHandler` 函数。</span><span class="sxs-lookup"><span data-stu-id="c2b80-121">There is no JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive Card.</span></span> <span data-ttu-id="c2b80-122">接收用户输入信息的唯一方法就是将结果传递给机器人。</span><span class="sxs-lookup"><span data-stu-id="c2b80-122">The only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="c2b80-123">若要从选项卡使用自适应卡片任务模块，你的应用必须包含自动程序才能从用户获取任何响应。</span><span class="sxs-lookup"><span data-stu-id="c2b80-123">To use an Adaptive Card task module from a tab, your app must include a bot to get any response from the user.</span></span>

<span data-ttu-id="c2b80-124">下一节提供了调用任务模块的示例。</span><span class="sxs-lookup"><span data-stu-id="c2b80-124">The next section gives an example of invoking a task module.</span></span>

## <a name="example-of-invoking-a-task-module"></a><span data-ttu-id="c2b80-125">调用任务模块的示例</span><span class="sxs-lookup"><span data-stu-id="c2b80-125">Example of invoking a task module</span></span>

<span data-ttu-id="c2b80-126">下图显示了任务模块：</span><span class="sxs-lookup"><span data-stu-id="c2b80-126">The following image displays the task module:</span></span>

![任务模块 - 自定义窗体](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="c2b80-128">以下代码改编自任务 [模块示例](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample)：</span><span class="sxs-lookup"><span data-stu-id="c2b80-128">The following code is adapted from [the task module sample](~/task-modules-and-cards/task-modules/invoking-task-modules.md#code-sample):</span></span>

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

<span data-ttu-id="c2b80-129">`submitHandler`非常简单，它会将 的值回显到 控制台或 `err` `result` 。</span><span class="sxs-lookup"><span data-stu-id="c2b80-129">The `submitHandler` is very simple and it echoes the value of `err` or `result` to the console.</span></span>

## <a name="submit-the-result-of-a-task-module"></a><span data-ttu-id="c2b80-130">提交任务模块的结果</span><span class="sxs-lookup"><span data-stu-id="c2b80-130">Submit the result of a task module</span></span>

<span data-ttu-id="c2b80-131">`submitHandler`函数驻留在 `TaskInfo.url` 网页中，与 一起使用 `TaskInfo.url` 。</span><span class="sxs-lookup"><span data-stu-id="c2b80-131">The `submitHandler` function resides in the `TaskInfo.url` web page and is used with `TaskInfo.url`.</span></span> <span data-ttu-id="c2b80-132">如果在调用任务模块时出现错误，将立即调用函数，并包含一个字符串，指示 `submitHandler` `err` [发生了什么错误](#task-module-invocation-errors)。</span><span class="sxs-lookup"><span data-stu-id="c2b80-132">If there is an error when invoking the task module, your `submitHandler` function is immediately invoked with an `err` string indicating what [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="c2b80-133">当用户选择任务模块右上角的 X 以关闭该函数时，也会使用字符串调用 `submitHandler` `err` 该函数。</span><span class="sxs-lookup"><span data-stu-id="c2b80-133">The `submitHandler` function is also called with an `err` string when the user selects X at the upper right of the task module to close it.</span></span>

<span data-ttu-id="c2b80-134">如果没有调用错误，并且用户未选择 X 将其消除，则用户在完成后选择一个按钮。</span><span class="sxs-lookup"><span data-stu-id="c2b80-134">If there is no invocation error and the user does not select X to dismiss it, the user chooses a button when finished.</span></span> <span data-ttu-id="c2b80-135">根据它是任务模块中的 URL 还是自适应卡片，接下来的部分将提供有关发生的情况的详细信息。</span><span class="sxs-lookup"><span data-stu-id="c2b80-135">Depending on whether it is a URL or an Adaptive Card in the task module, the next sections provide details on what occurs.</span></span>

### <a name="html-or-javascript-taskinfourl"></a><span data-ttu-id="c2b80-136">HTML 或 JavaScript `TaskInfo.url`</span><span class="sxs-lookup"><span data-stu-id="c2b80-136">HTML or JavaScript `TaskInfo.url`</span></span>

<span data-ttu-id="c2b80-137">验证用户输入后，调用 `microsoftTeams.tasks.submitTask()` 称为 的 SDK 函数 `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="c2b80-137">After validating the user's inputs, call the `microsoftTeams.tasks.submitTask()` SDK function referred to as `submitTask()`.</span></span> <span data-ttu-id="c2b80-138">如果 `submitTask()` 只想关闭任务模块，Teams调用不带任何参数。</span><span class="sxs-lookup"><span data-stu-id="c2b80-138">Call `submitTask()` without any parameters if you just want Teams to close the task module.</span></span> <span data-ttu-id="c2b80-139">可以将对象或字符串传递到 `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="c2b80-139">You can pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="c2b80-140">将结果作为第一个参数传递。</span><span class="sxs-lookup"><span data-stu-id="c2b80-140">Pass your result as the first parameter.</span></span> <span data-ttu-id="c2b80-141">Teams调用 `submitHandler` where is `err` 和 `null` `result` 是传递给 的对象或字符串 `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="c2b80-141">Teams invokes `submitHandler` where `err` is `null` and `result` is the object or string you passed to `submitTask()`.</span></span> <span data-ttu-id="c2b80-142">如果使用 参数 `submitTask()` 调用 `result` ，则必须传递 或 `appId` 字符串 `appId` 数组。</span><span class="sxs-lookup"><span data-stu-id="c2b80-142">If you call `submitTask()` with a `result` parameter, you must pass an `appId` or an array of `appId` strings.</span></span> <span data-ttu-id="c2b80-143">这允许Teams验证发送结果的应用是否与调用的任务模块相同。</span><span class="sxs-lookup"><span data-stu-id="c2b80-143">This permits Teams to validate that the app sending the result is same as the invoked task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="c2b80-144">自适应卡片 `TaskInfo.card`</span><span class="sxs-lookup"><span data-stu-id="c2b80-144">Adaptive Card `TaskInfo.card`</span></span>

<span data-ttu-id="c2b80-145">当你使用 调用任务模块且用户选择一个按钮时，卡片中的值将返回 `submitHandler` `Action.Submit` 为 的值 `result` 。</span><span class="sxs-lookup"><span data-stu-id="c2b80-145">When you invoke the task module with a `submitHandler` and the user selects an `Action.Submit` button, the values in the card are returned as the value of `result`.</span></span> <span data-ttu-id="c2b80-146">如果用户选择 Esc 键或右上方的 X，则 `err` 改为返回 。</span><span class="sxs-lookup"><span data-stu-id="c2b80-146">If the user selects the Esc key or X at the top right, `err` is returned instead.</span></span> <span data-ttu-id="c2b80-147">如果你的应用包含除选项卡外还包含自动程序，则只需在 对象中包含 自动程序 作为 `appId` `completionBotId` `TaskInfo` 的值。</span><span class="sxs-lookup"><span data-stu-id="c2b80-147">If your app contains a bot in addition to a tab, you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="c2b80-148">当用户选择按钮时，使用消息将用户填充的自适应卡片 `task/submit invoke` 正文发送给 `Action.Submit` 自动程序。</span><span class="sxs-lookup"><span data-stu-id="c2b80-148">The Adaptive Card body as filled in by the user is sent to the bot using a `task/submit invoke` message when the user selects an `Action.Submit` button.</span></span> <span data-ttu-id="c2b80-149">你接收的对象的架构非常类似于你针对任务/提取和任务/提交消息收到的 [架构](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)。</span><span class="sxs-lookup"><span data-stu-id="c2b80-149">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="c2b80-150">唯一的区别是 JSON 对象的架构是自适应卡片对象，而不是包含自适应卡片对象的对象，就像自适应卡片用于机器人 [一样](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)。</span><span class="sxs-lookup"><span data-stu-id="c2b80-150">The only difference is that the schema of the JSON object is an Adaptive Card object as opposed to an object containing an Adaptive Card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

<span data-ttu-id="c2b80-151">下一节提供了一个提交任务模块结果的示例。</span><span class="sxs-lookup"><span data-stu-id="c2b80-151">The next section gives an example of submitting the result of a task module.</span></span>

## <a name="example-of-submitting-the-result-of-a-task-module"></a><span data-ttu-id="c2b80-152">提交任务模块结果的示例</span><span class="sxs-lookup"><span data-stu-id="c2b80-152">Example of submitting the result of a task module</span></span>

<span data-ttu-id="c2b80-153">有关详细信息，请参阅任务 [模块中的 HTML 窗体](#example-of-invoking-a-task-module)。</span><span class="sxs-lookup"><span data-stu-id="c2b80-153">For more information, see the [HTML form in the task module](#example-of-invoking-a-task-module).</span></span> <span data-ttu-id="c2b80-154">以下代码提供了表单定义位置的示例：</span><span class="sxs-lookup"><span data-stu-id="c2b80-154">The following code gives an example of where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="c2b80-155">此窗体上有五个字段，但对于此示例，只需要三个值，即 `name` 、 `email` 和 `favoriteBook` 。</span><span class="sxs-lookup"><span data-stu-id="c2b80-155">There are five fields on this form but for this example only three values are required, `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="c2b80-156">以下代码提供了调用 `validateForm()` 的函数的示例 `submitTask()` ：</span><span class="sxs-lookup"><span data-stu-id="c2b80-156">The following code gives an example of the `validateForm()` function that calls `submitTask()`:</span></span>

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

<span data-ttu-id="c2b80-157">下一节提供任务模块调用问题及其错误消息。</span><span class="sxs-lookup"><span data-stu-id="c2b80-157">The next section provides task module invocation problems and their error messages.</span></span>

## <a name="task-module-invocation-errors"></a><span data-ttu-id="c2b80-158">任务模块调用错误</span><span class="sxs-lookup"><span data-stu-id="c2b80-158">Task module invocation errors</span></span>

<span data-ttu-id="c2b80-159">下表提供了 你的 可以 `err` 接收的可能值 `submitHandler` ：</span><span class="sxs-lookup"><span data-stu-id="c2b80-159">The following table provides the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="c2b80-160">问题</span><span class="sxs-lookup"><span data-stu-id="c2b80-160">Problem</span></span> | <span data-ttu-id="c2b80-161">值为 的错误消息 `err`</span><span class="sxs-lookup"><span data-stu-id="c2b80-161">Error message that is value of `err`</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="c2b80-162">指定了 和 `TaskInfo.url` `TaskInfo.card` 的值。</span><span class="sxs-lookup"><span data-stu-id="c2b80-162">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="c2b80-163">已指定卡和 URL 的值。</span><span class="sxs-lookup"><span data-stu-id="c2b80-163">Values for both card and URL were specified.</span></span> <span data-ttu-id="c2b80-164">允许使用其中一个，但不能同时使用这两者。</span><span class="sxs-lookup"><span data-stu-id="c2b80-164">One or the other, but not both, are allowed.</span></span> |
| <span data-ttu-id="c2b80-165">既不 `TaskInfo.url` 指定也不 `TaskInfo.card` 指定。</span><span class="sxs-lookup"><span data-stu-id="c2b80-165">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="c2b80-166">必须为卡片或 URL 指定值。</span><span class="sxs-lookup"><span data-stu-id="c2b80-166">You must specify a value for either card or URL.</span></span> |
| <span data-ttu-id="c2b80-167">无效 `appId` 。</span><span class="sxs-lookup"><span data-stu-id="c2b80-167">Invalid `appId`.</span></span> | <span data-ttu-id="c2b80-168">无效的应用 ID。</span><span class="sxs-lookup"><span data-stu-id="c2b80-168">Invalid app ID.</span></span> |
| <span data-ttu-id="c2b80-169">用户选择 X 按钮，关闭它。</span><span class="sxs-lookup"><span data-stu-id="c2b80-169">User selected X button, closing it.</span></span> | <span data-ttu-id="c2b80-170">用户已取消或关闭任务模块。</span><span class="sxs-lookup"><span data-stu-id="c2b80-170">User cancelled or closed the task module.</span></span> |

## <a name="code-sample"></a><span data-ttu-id="c2b80-171">代码示例</span><span class="sxs-lookup"><span data-stu-id="c2b80-171">Code sample</span></span>

|<span data-ttu-id="c2b80-172">示例名称</span><span class="sxs-lookup"><span data-stu-id="c2b80-172">Sample name</span></span> | <span data-ttu-id="c2b80-173">说明</span><span class="sxs-lookup"><span data-stu-id="c2b80-173">Description</span></span> | <span data-ttu-id="c2b80-174">.NET</span><span class="sxs-lookup"><span data-stu-id="c2b80-174">.NET</span></span> | <span data-ttu-id="c2b80-175">Node.js</span><span class="sxs-lookup"><span data-stu-id="c2b80-175">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="c2b80-176">任务模块示例选项卡和 bots-V3</span><span class="sxs-lookup"><span data-stu-id="c2b80-176">Task module sample tabs and bots-V3</span></span> | <span data-ttu-id="c2b80-177">用于创建任务模块的示例。</span><span class="sxs-lookup"><span data-stu-id="c2b80-177">Samples for creating task modules.</span></span> |[<span data-ttu-id="c2b80-178">View</span><span class="sxs-lookup"><span data-stu-id="c2b80-178">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[<span data-ttu-id="c2b80-179">View</span><span class="sxs-lookup"><span data-stu-id="c2b80-179">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a><span data-ttu-id="c2b80-180">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c2b80-180">See also</span></span>

[<span data-ttu-id="c2b80-181">调用和消除任务模块</span><span class="sxs-lookup"><span data-stu-id="c2b80-181">Invoke and dismiss task modules</span></span>](~/task-modules-and-cards/task-modules/invoking-task-modules.md)

## <a name="next-step"></a><span data-ttu-id="c2b80-182">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c2b80-182">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c2b80-183">使用自动程序中的任务模块</span><span class="sxs-lookup"><span data-stu-id="c2b80-183">Using task modules from bots</span></span>](~/task-modules-and-cards/task-modules/task-modules-bots.md)
