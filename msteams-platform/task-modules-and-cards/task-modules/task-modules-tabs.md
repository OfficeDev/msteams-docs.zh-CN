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
# <a name="using-task-modules-in-tabs"></a><span data-ttu-id="b2f25-104">在选项卡中使用任务模块</span><span class="sxs-lookup"><span data-stu-id="b2f25-104">Using task modules in tabs</span></span>

<span data-ttu-id="b2f25-105">将任务模块添加到选项卡可以大大简化需要数据输入的任何工作流的用户体验。</span><span class="sxs-lookup"><span data-stu-id="b2f25-105">Adding a task module to your tab can greatly simplify your user's experience for any workflows that require data input.</span></span> <span data-ttu-id="b2f25-106">任务模块允许你在 Teams 感知弹出窗口中收集其输入。</span><span class="sxs-lookup"><span data-stu-id="b2f25-106">Task modules allow you to gather their input in a Teams-aware popup.</span></span> <span data-ttu-id="b2f25-107">一个很好的示例是编辑 Planner 卡;可以使用任务模块来创建类似的体验。</span><span class="sxs-lookup"><span data-stu-id="b2f25-107">A good example of this is editing Planner cards; you can use task modules to create a similar experience.</span></span>

<span data-ttu-id="b2f25-108">为了支持任务模块功能，向 Microsoft Teams 客户端 SDK 添加了两 [个新函数](/javascript/api/overview/msteams-client)：</span><span class="sxs-lookup"><span data-stu-id="b2f25-108">To support the task module feature, two new functions were added to the [Microsoft Teams client SDK](/javascript/api/overview/msteams-client):</span></span>

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

<span data-ttu-id="b2f25-109">让我们看一下每个功能如何工作。</span><span class="sxs-lookup"><span data-stu-id="b2f25-109">Let's see how each of them work.</span></span>

## <a name="invoking-a-task-module-from-a-tab"></a><span data-ttu-id="b2f25-110">从选项卡调用任务模块</span><span class="sxs-lookup"><span data-stu-id="b2f25-110">Invoking a task module from a tab</span></span>

<span data-ttu-id="b2f25-111">若要从选项卡调用任务模块，请使用 `microsoftTeams.tasks.startTask()` 传递 [TaskInfo 对象](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) 和可选 `submitHandler` 回调函数。</span><span class="sxs-lookup"><span data-stu-id="b2f25-111">To invoke a task module from a tab use `microsoftTeams.tasks.startTask()` passing a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) and an optional `submitHandler` callback function.</span></span> <span data-ttu-id="b2f25-112">如前面所述，有两种情况需要考虑：</span><span class="sxs-lookup"><span data-stu-id="b2f25-112">As described earlier, there are two cases to consider:</span></span>

1. <span data-ttu-id="b2f25-113">值设置为 `TaskInfo.url` URL。</span><span class="sxs-lookup"><span data-stu-id="b2f25-113">The value of `TaskInfo.url` is set to a URL.</span></span> <span data-ttu-id="b2f25-114">任务模块窗口将显示 `TaskModule.url` 并作为内部 `<iframe>` 加载。</span><span class="sxs-lookup"><span data-stu-id="b2f25-114">The task module window appears and `TaskModule.url` is loaded as an `<iframe>` inside it.</span></span> <span data-ttu-id="b2f25-115">该页上的 JavaScript 应调用 `microsoftTeams.initialize()` 。</span><span class="sxs-lookup"><span data-stu-id="b2f25-115">JavaScript on that page should call `microsoftTeams.initialize()`.</span></span> <span data-ttu-id="b2f25-116">如果页面上有一个函数，并且调用时出错，则调用设置为指示错误的错误字符串， `submitHandler` `microsoftTeams.tasks.startTask()` `submitHandler` `err` 如下 [所述](#task-module-invocation-errors)。</span><span class="sxs-lookup"><span data-stu-id="b2f25-116">If there is a `submitHandler` function on the page and there is an error when invoking `microsoftTeams.tasks.startTask()`, then `submitHandler` is invoked with `err` set to the error string indicating the error as described [below](#task-module-invocation-errors).</span></span>
1. <span data-ttu-id="b2f25-117">的值为 `taskInfo.card` 自适应[卡片的 JSON。](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment)</span><span class="sxs-lookup"><span data-stu-id="b2f25-117">The value of `taskInfo.card` is the [JSON for an Adaptive card](~/task-modules-and-cards/what-are-task-modules.md#adaptive-card-or-adaptive-card-bot-card-attachment).</span></span> <span data-ttu-id="b2f25-118">在这种情况下，在用户关闭或按下自适应卡片上的按钮时，明显没有任何 JavaScript 函数可调用;接收用户输入内容的唯一方法就是将结果传递给机器人。 `submitHandler`</span><span class="sxs-lookup"><span data-stu-id="b2f25-118">In this case there's obviously not any JavaScript `submitHandler` function to call when the user closes or presses a button on the Adaptive card; the only way to receive what the user entered is by passing the result to a bot.</span></span> <span data-ttu-id="b2f25-119">若要从选项卡使用自适应卡片任务模块，应用必须包含自动程序才能从用户获取任何信息。</span><span class="sxs-lookup"><span data-stu-id="b2f25-119">To use an Adaptive card task module from a tab your app must include a bot to get any information back from the user.</span></span> <span data-ttu-id="b2f25-120">下面对此进行了说明。</span><span class="sxs-lookup"><span data-stu-id="b2f25-120">This is explained below.</span></span>

## <a name="example-invoking-a-task-module"></a><span data-ttu-id="b2f25-121">示例：调用任务模块</span><span class="sxs-lookup"><span data-stu-id="b2f25-121">Example: Invoking a task module</span></span>

<span data-ttu-id="b2f25-122">下面的代码改编自任务 [模块示例](~/task-modules-and-cards/what-are-task-modules.md#code-sample)。</span><span class="sxs-lookup"><span data-stu-id="b2f25-122">The code below is adapted from [the task module sample](~/task-modules-and-cards/what-are-task-modules.md#code-sample).</span></span> <span data-ttu-id="b2f25-123">任务模块如下所示：</span><span class="sxs-lookup"><span data-stu-id="b2f25-123">Here's what the task module looks like:</span></span>

![任务模块 - 自定义窗体](~/assets/images/task-module/task-module-custom-form.png)

<span data-ttu-id="b2f25-125">非常简单 `submitHandler` ;它只是将控制台的值 `err` 回显 `result` ：</span><span class="sxs-lookup"><span data-stu-id="b2f25-125">The `submitHandler` is very simple; it just echoes the value of `err` or `result` to the console:</span></span>

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

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="b2f25-126">提交任务模块的结果</span><span class="sxs-lookup"><span data-stu-id="b2f25-126">Submitting the result of a task module</span></span>

<span data-ttu-id="b2f25-127">该 `submitHandler` 函数与 `TaskInfo.url` 。</span><span class="sxs-lookup"><span data-stu-id="b2f25-127">The `submitHandler` function is used with `TaskInfo.url`.</span></span> <span data-ttu-id="b2f25-128">`submitHandler`该函数驻留在 `TaskInfo.url` 网页中。</span><span class="sxs-lookup"><span data-stu-id="b2f25-128">The `submitHandler` function resides in the `TaskInfo.url` web page.</span></span> <span data-ttu-id="b2f25-129">如果在调用任务模块时出错，函数将立即调用，并包含一个指示发生了 `submitHandler` `err` 错误的 [字符串](#task-module-invocation-errors)。</span><span class="sxs-lookup"><span data-stu-id="b2f25-129">If there's an error when invoking the task module your `submitHandler` function will be immediately invoked with an `err` string indicating which [error occurred](#task-module-invocation-errors).</span></span> <span data-ttu-id="b2f25-130">当用户按任务模块右上角的 X 时，也会使用字符串调用 `submitHandler` `err` 该函数。</span><span class="sxs-lookup"><span data-stu-id="b2f25-130">The `submitHandler` function is also called with an `err` string when the user presses the X at the upper right of task module.</span></span>

<span data-ttu-id="b2f25-131">如果没有调用错误，并且用户不按 X 来消除它，则用户完成后按一个按钮。</span><span class="sxs-lookup"><span data-stu-id="b2f25-131">If there's no invocation error and the user doesn't press X to dismiss it, the user presses a button when finished.</span></span> <span data-ttu-id="b2f25-132">根据它是任务模块中的 URL 还是自适应卡片，以下是发生的情况：</span><span class="sxs-lookup"><span data-stu-id="b2f25-132">Depending on whether it's a URL or an Adaptive card in the task module, here's what happens:</span></span>

### <a name="htmljavascript-taskinfourl"></a><span data-ttu-id="b2f25-133">HTML/JavaScript `TaskInfo.url` () </span><span class="sxs-lookup"><span data-stu-id="b2f25-133">HTML/JavaScript (`TaskInfo.url`)</span></span>

<span data-ttu-id="b2f25-134">验证用户输入的信息后， (为了可读性目的调用 SDK 函数 `microsoftTeams.tasks.submitTask()` `submitTask()`) 。</span><span class="sxs-lookup"><span data-stu-id="b2f25-134">Once you've validated what the user has entered you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="b2f25-135">如果你仅希望 Teams 关闭任务模块，但在大多数情况下，你想要将对象或字符串传递给你的 ，你可以调用不带任何 `submitTask()` 参数 `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="b2f25-135">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span>

<span data-ttu-id="b2f25-136">将结果作为第一个参数传递。</span><span class="sxs-lookup"><span data-stu-id="b2f25-136">Pass your result as the first parameter.</span></span> <span data-ttu-id="b2f25-137">Teams 将 `submitHandler` 调用 `err` 将在何处 `null` ， `result` 并且将是你传递给的对象/字符串 `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="b2f25-137">Teams will invoke `submitHandler` where `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="b2f25-138">如果使用参数调用，则必须传递字符串数组或字符串数组：这允许 Teams 验证发送结果的应用是否与调用任务模块的应用 `submitTask()` `result`  `appId` `appId` 相同。</span><span class="sxs-lookup"><span data-stu-id="b2f25-138">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span>

### <a name="adaptive-card-taskinfocard"></a><span data-ttu-id="b2f25-139">自适应卡片 `TaskInfo.card` () </span><span class="sxs-lookup"><span data-stu-id="b2f25-139">Adaptive card (`TaskInfo.card`)</span></span>

<span data-ttu-id="b2f25-140">如果使用 a 调用任务模块，当用户按下按钮时，卡片中的值将返回 `submitHandler` `Action.Submit` 为 `result` 值 。</span><span class="sxs-lookup"><span data-stu-id="b2f25-140">If you invoked the task module with a `submitHandler`, when the user presses an `Action.Submit` button the values in the card will be returned as the value of `result`.</span></span> <span data-ttu-id="b2f25-141">如果用户按下 Esc 按钮或按 X， `err` 将改为返回。</span><span class="sxs-lookup"><span data-stu-id="b2f25-141">If the user presses the Esc button or presses the X, `err` will be returned instead.</span></span> <span data-ttu-id="b2f25-142">或者，如果你的应用除了包含选项卡外还包含自动程序，你只需将机器人的值包含在 `appId` `completionBotId` 对象 `TaskInfo` 中。</span><span class="sxs-lookup"><span data-stu-id="b2f25-142">Alternatively, if your app contains a bot in addition to a tab you can simply include the `appId` of the bot as the value of `completionBotId` in the `TaskInfo` object.</span></span> <span data-ttu-id="b2f25-143">当用户按下 (时，自适应卡片正文) 会通过消息发送给自动 `task/submit invoke` `Action.Submit` 程序。</span><span class="sxs-lookup"><span data-stu-id="b2f25-143">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit invoke` message when the user presses an `Action.Submit` button.</span></span> <span data-ttu-id="b2f25-144">您接收的对象的架构与接收任务/提取和[任务/](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)提交消息的架构非常相似;唯一的区别是，JSON 对象的架构是自适应卡片对象，而不是包含自适应卡片对象的对象，就像自适应卡片与机器人一[样。](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="b2f25-144">The schema for the object you receive is very similar to [the schema you receive for task/fetch and task/submit messages](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages); the only difference is that the schema of the JSON object is an Adaptive card object as opposed to an object *containing* an Adaptive card object as [when Adaptive cards are used with bots](~/task-modules-and-cards/task-modules/task-modules-bots.md#payload-of-taskfetch-and-tasksubmit-messages).</span></span>

## <a name="example-submitting-the-result-of-a-task-module"></a><span data-ttu-id="b2f25-145">示例：提交任务模块的结果</span><span class="sxs-lookup"><span data-stu-id="b2f25-145">Example: submitting the result of a task module</span></span>

<span data-ttu-id="b2f25-146">使用 [HTML 表单](#example-invoking-a-task-module) 调用上述任务模块中的表单。</span><span class="sxs-lookup"><span data-stu-id="b2f25-146">Recall the [form in the task module above](#example-invoking-a-task-module) with an HTML form.</span></span> <span data-ttu-id="b2f25-147">下面是定义表单的地方：</span><span class="sxs-lookup"><span data-stu-id="b2f25-147">Here's where the form is defined:</span></span>

```html
<form method="POST" id="customerForm" action="/register" onSubmit="return validateForm()">
```

<span data-ttu-id="b2f25-148">此窗体上有五个字段，但我们仅对此示例中三个字段的值感兴趣：、 `name` `email` 和 `favoriteBook` 。</span><span class="sxs-lookup"><span data-stu-id="b2f25-148">There are five fields on this form but we're only interested in the values of three of them for this example: `name`, `email`, and `favoriteBook`.</span></span>

<span data-ttu-id="b2f25-149">下面是调用 `validateForm()` 的函数 `submitTask()` ：</span><span class="sxs-lookup"><span data-stu-id="b2f25-149">Here's the `validateForm()` function that calls `submitTask()`:</span></span>

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

## <a name="task-module-invocation-errors"></a><span data-ttu-id="b2f25-150">任务模块调用错误</span><span class="sxs-lookup"><span data-stu-id="b2f25-150">Task module invocation errors</span></span>

<span data-ttu-id="b2f25-151">下面是以下可能 `err` 的值，可通过以下帐户接收 `submitHandler` ：</span><span class="sxs-lookup"><span data-stu-id="b2f25-151">Here are the possible values of `err` that can be received by your `submitHandler`:</span></span>

| <span data-ttu-id="b2f25-152">问题</span><span class="sxs-lookup"><span data-stu-id="b2f25-152">Problem</span></span> | <span data-ttu-id="b2f25-153">错误消息 (`err` 值) </span><span class="sxs-lookup"><span data-stu-id="b2f25-153">Error message (value of `err`)</span></span> |
| ------- | ------------------------------ |
| <span data-ttu-id="b2f25-154">同时指定了 `TaskInfo.url` 这两 `TaskInfo.card` 个值。</span><span class="sxs-lookup"><span data-stu-id="b2f25-154">Values for both `TaskInfo.url` and `TaskInfo.card` were specified.</span></span> | <span data-ttu-id="b2f25-155">"已指定卡和 url 的值。</span><span class="sxs-lookup"><span data-stu-id="b2f25-155">"Values for both card and url were specified.</span></span> <span data-ttu-id="b2f25-156">允许一个或另一个，但不能同时允许这两者。"</span><span class="sxs-lookup"><span data-stu-id="b2f25-156">One or the other, but not both, are allowed."</span></span> |
| <span data-ttu-id="b2f25-157">既不 `TaskInfo.url` 指定也不 `TaskInfo.card` 指定。</span><span class="sxs-lookup"><span data-stu-id="b2f25-157">Neither `TaskInfo.url` nor `TaskInfo.card` specified.</span></span> | <span data-ttu-id="b2f25-158">"必须为卡片或 url 指定值。"</span><span class="sxs-lookup"><span data-stu-id="b2f25-158">"You must specify a value for either card or url."</span></span> |
| <span data-ttu-id="b2f25-159">无效 `appId` 。</span><span class="sxs-lookup"><span data-stu-id="b2f25-159">Invalid `appId`.</span></span> | <span data-ttu-id="b2f25-160">"appId 无效。"</span><span class="sxs-lookup"><span data-stu-id="b2f25-160">"Invalid appId."</span></span> |
| <span data-ttu-id="b2f25-161">用户按下 X 按钮，关闭它。</span><span class="sxs-lookup"><span data-stu-id="b2f25-161">User pressed X button, closing it.</span></span> | <span data-ttu-id="b2f25-162">"用户已取消/关闭任务模块。"</span><span class="sxs-lookup"><span data-stu-id="b2f25-162">"User cancelled/closed the task module."</span></span> |
