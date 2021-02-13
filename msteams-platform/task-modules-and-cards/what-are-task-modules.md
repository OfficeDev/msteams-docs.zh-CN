---
title: 什么是任务模块？
author: clearab
description: 添加模式弹出窗口体验，以收集 Microsoft Teams 应用中的信息或向用户显示信息。
ms.topic: overview
ms.author: anclear
ms.openlocfilehash: d92da7e6def6d66efd2f94600b7b8f8847553701
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231657"
---
# <a name="what-are-task-modules"></a><span data-ttu-id="3ff39-103">什么是任务模块？</span><span class="sxs-lookup"><span data-stu-id="3ff39-103">What are task modules?</span></span>

<span data-ttu-id="3ff39-104">任务模块允许你在 Teams 应用程序中创建模式弹出体验。</span><span class="sxs-lookup"><span data-stu-id="3ff39-104">Task modules allow you to create modal popup experiences in your Teams application.</span></span> <span data-ttu-id="3ff39-105">在弹出窗口中，你可以运行自己的自定义 HTML/JavaScript 代码，显示基于小部件（如 YouTube 或 Microsoft Stream 视频）或 `<iframe>` 显示 [自适应卡片](/adaptive-cards/)。</span><span class="sxs-lookup"><span data-stu-id="3ff39-105">Inside the popup you can run your own custom HTML/JavaScript code, show an `<iframe>`-based widget such as a YouTube or Microsoft Stream video or display an [Adaptive card](/adaptive-cards/).</span></span> <span data-ttu-id="3ff39-106">它们对于启动和完成任务或显示丰富的信息（如视频或 Power BI 仪表板）特别有用。</span><span class="sxs-lookup"><span data-stu-id="3ff39-106">They are especially useful for initiating and completing tasks or displaying rich information like videos or Power BI dashboards.</span></span> <span data-ttu-id="3ff39-107">与选项卡或基于对话的自动程序体验相比，弹出式体验对于用户启动和完成任务通常更自然。</span><span class="sxs-lookup"><span data-stu-id="3ff39-107">A popup experience is often more natural for users initiating and completing tasks compared to a tab or a conversation-based bot experience.</span></span>

<span data-ttu-id="3ff39-108">任务模块基于 Microsoft Teams 选项卡构建;它们实质上是弹出窗口中的一个选项卡。</span><span class="sxs-lookup"><span data-stu-id="3ff39-108">Task modules build on the foundation of Microsoft Teams tabs; they are essentially a tab inside a popup window.</span></span> <span data-ttu-id="3ff39-109">它们使用相同的 SDK，因此，如果你已生成选项卡，则 90% 已能够创建任务模块。</span><span class="sxs-lookup"><span data-stu-id="3ff39-109">They use the same SDK, so if you've built a tab you are already 90% of the way to being able to create a task module.</span></span>

<span data-ttu-id="3ff39-110">可以通过三种方式调用任务模块：</span><span class="sxs-lookup"><span data-stu-id="3ff39-110">Task modules can be invoked in three ways:</span></span>

* <span data-ttu-id="3ff39-111">**频道或个人选项卡。**</span><span class="sxs-lookup"><span data-stu-id="3ff39-111">**Channel or personal tabs.**</span></span> <span data-ttu-id="3ff39-112">使用 Microsoft Teams 选项卡 SDK，可以从选项卡上的按钮、链接或菜单调用任务模块。此处详细介绍 [了这一点。](~/task-modules-and-cards/task-modules/task-modules-tabs.md)</span><span class="sxs-lookup"><span data-stu-id="3ff39-112">Using the Microsoft Teams Tabs SDK you can invoke task modules from buttons, links or menus on your tab. [This is covered in detail here.](~/task-modules-and-cards/task-modules/task-modules-tabs.md)</span></span>
* <span data-ttu-id="3ff39-113">**机器人。**</span><span class="sxs-lookup"><span data-stu-id="3ff39-113">**Bots.**</span></span> <span data-ttu-id="3ff39-114">从自动程序 [发送的](~/task-modules-and-cards/cards/cards-reference.md) 卡片上的按钮。</span><span class="sxs-lookup"><span data-stu-id="3ff39-114">Buttons on [cards](~/task-modules-and-cards/cards/cards-reference.md) sent from your bot.</span></span> <span data-ttu-id="3ff39-115">当你不需要频道中的每个人查看你使用机器人执行什么时，这尤其有用。</span><span class="sxs-lookup"><span data-stu-id="3ff39-115">This is particularly useful when you don't need everyone in a channel to see what you are doing with a bot.</span></span> <span data-ttu-id="3ff39-116">例如，当用户在频道中回复轮询时，查看所创建的轮询记录并不实用。</span><span class="sxs-lookup"><span data-stu-id="3ff39-116">For example, when having users respond to a poll in a channel it's not terribly useful to see a record of that poll being created.</span></span> [<span data-ttu-id="3ff39-117">此处详细介绍了这一点。</span><span class="sxs-lookup"><span data-stu-id="3ff39-117">This is covered in detail here.</span></span>](~/task-modules-and-cards/task-modules/task-modules-bots.md)
* <span data-ttu-id="3ff39-118">**来自深层链接的 Teams 外部。**</span><span class="sxs-lookup"><span data-stu-id="3ff39-118">**Outside of Teams from a deep link.**</span></span> <span data-ttu-id="3ff39-119">还可以创建 URL 以从任何位置调用任务模块。</span><span class="sxs-lookup"><span data-stu-id="3ff39-119">You can also create URLs to invoke a task module from anywhere.</span></span> [<span data-ttu-id="3ff39-120">此处详细介绍了这一点。</span><span class="sxs-lookup"><span data-stu-id="3ff39-120">This is covered in detail here.</span></span>](#task-module-deep-link-syntax)

## <a name="what-a-task-module-looks-like"></a><span data-ttu-id="3ff39-121">任务模块的外观</span><span class="sxs-lookup"><span data-stu-id="3ff39-121">What a task module looks like</span></span>

<span data-ttu-id="3ff39-122">下面是从没有彩色矩形和编号的圆圈的自动程序 (调用任务模块时的外观，当然) ：</span><span class="sxs-lookup"><span data-stu-id="3ff39-122">Here's what a task module looks like when invoked from a bot (without the colored rectangles and numbered circles, of course):</span></span>

![任务模块示例](~/assets/images/task-module/task-module-example.png)

<span data-ttu-id="3ff39-124">让我们演练一下：</span><span class="sxs-lookup"><span data-stu-id="3ff39-124">Let's walk through it:</span></span>

1. <span data-ttu-id="3ff39-125">应用的[ `color` 图标](~/resources/schema/manifest-schema.md#icons)。</span><span class="sxs-lookup"><span data-stu-id="3ff39-125">Your app's [`color` icon](~/resources/schema/manifest-schema.md#icons).</span></span>
2. <span data-ttu-id="3ff39-126">应用[ `short` 的名称](~/resources/schema/manifest-schema.md#name)。</span><span class="sxs-lookup"><span data-stu-id="3ff39-126">Your app's [`short` name](~/resources/schema/manifest-schema.md#name).</span></span>
3. <span data-ttu-id="3ff39-127">任务模块的标题在 `title` [TaskInfo 对象的属性中指定](#the-taskinfo-object)。</span><span class="sxs-lookup"><span data-stu-id="3ff39-127">The task module's title specified in the `title` property of the [TaskInfo object](#the-taskinfo-object).</span></span>
4. <span data-ttu-id="3ff39-128">任务模块的关闭/取消按钮。</span><span class="sxs-lookup"><span data-stu-id="3ff39-128">The task module's close/cancel button.</span></span> <span data-ttu-id="3ff39-129">如果用户按此键，你的应用将收到 `err` 一个事件，如下 [所述](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)。</span><span class="sxs-lookup"><span data-stu-id="3ff39-129">If the user presses this, your app will receive an `err` event as described [here](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module).</span></span> <span data-ttu-id="3ff39-130"> (**注意：** 当前无法从 bot.) </span><span class="sxs-lookup"><span data-stu-id="3ff39-130">(**Note:** It is currently not possible to detect this event when a task module is invoked from a bot.)</span></span>
5. <span data-ttu-id="3ff39-131">如果使用 TaskInfo 对象的属性加载自己的网页，则蓝色矩形是网页的 `url` [显示位置](#the-taskinfo-object)。</span><span class="sxs-lookup"><span data-stu-id="3ff39-131">The blue rectangle is the where your web page appears if you are loading your own web page using the `url` property of the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="3ff39-132">下面的任务模块 [大小调整部分中提供了更多详细信息](#task-module-sizing) 。</span><span class="sxs-lookup"><span data-stu-id="3ff39-132">More detail is in the [task module sizing](#task-module-sizing) section below.</span></span>
6. <span data-ttu-id="3ff39-133">如果通过 TaskInfo 对象的属性显示自适应卡片，则添加填充，否则需要自己 `card` [处理。](#task-module-css-for-htmljavascript-task-modules) [](#the-taskinfo-object)</span><span class="sxs-lookup"><span data-stu-id="3ff39-133">If you are displaying an Adaptive card via the `card` property of the [TaskInfo object](#the-taskinfo-object) the padding is added for you, otherwise you'll need to [handle this yourself](#task-module-css-for-htmljavascript-task-modules).</span></span>
7. <span data-ttu-id="3ff39-134">自适应卡片按钮将在此处呈现。</span><span class="sxs-lookup"><span data-stu-id="3ff39-134">Adaptive card buttons will render here.</span></span> <span data-ttu-id="3ff39-135">如果你使用的是自己的页面，则必须创建自己的按钮。</span><span class="sxs-lookup"><span data-stu-id="3ff39-135">If you're using your own page you must create your own buttons.</span></span>

## <a name="overview-of-invoking-and-dismissing-task-modules"></a><span data-ttu-id="3ff39-136">调用和消除任务模块概述</span><span class="sxs-lookup"><span data-stu-id="3ff39-136">Overview of invoking and dismissing task modules</span></span>

<span data-ttu-id="3ff39-137">可以从选项卡、自动程序或深层链接调用任务模块，其中显示的内容可以是 HTML 或自适应卡片，因此在如何调用任务模块以及如何处理用户交互的结果方面有很多灵活性。</span><span class="sxs-lookup"><span data-stu-id="3ff39-137">Task modules can be invoked from tabs, bots or deep links and what appears in one can be either HTML or an Adaptive card, so there's a lot of flexibility in terms of how they are invoked and how to deal with the result of a user's interaction.</span></span> <span data-ttu-id="3ff39-138">下表总结了此操作的工作原理：</span><span class="sxs-lookup"><span data-stu-id="3ff39-138">The table below summarizes how this works:</span></span>

| <span data-ttu-id="3ff39-139">**通过...**</span><span class="sxs-lookup"><span data-stu-id="3ff39-139">**Invoked via...**</span></span> | <span data-ttu-id="3ff39-140">**任务模块为 HTML/JavaScript**</span><span class="sxs-lookup"><span data-stu-id="3ff39-140">**Task module is HTML/JavaScript**</span></span> | <span data-ttu-id="3ff39-141">**任务模块为自适应卡片**</span><span class="sxs-lookup"><span data-stu-id="3ff39-141">**Task module is Adaptive card**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3ff39-142">**选项卡中的 JavaScript**</span><span class="sxs-lookup"><span data-stu-id="3ff39-142">**JavaScript in a tab**</span></span> | <span data-ttu-id="3ff39-143">1. 将 Teams 客户端 SDK 函数与 `tasks.startTask()` 可选回调 `submitHandler(err, result)` 函数一同使用</span><span class="sxs-lookup"><span data-stu-id="3ff39-143">1. Use the Teams client SDK function `tasks.startTask()` with an optional `submitHandler(err, result)` callback function</span></span> <br/><br/> <span data-ttu-id="3ff39-144">2. 在任务模块代码中，当用户完成时，使用对象作为参数调用 Teams SDK `tasks.submitTask()` `result` 函数。</span><span class="sxs-lookup"><span data-stu-id="3ff39-144">2. In the task module code, when the user is finished, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="3ff39-145">如果在 `submitHandler` 中指定了回调 `tasks.startTask()` ，Teams 会使用参数 `result` 调用它。</span><span class="sxs-lookup"><span data-stu-id="3ff39-145">If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with `result` as a parameter.</span></span><br/><br/> <span data-ttu-id="3ff39-146">3. 如果在调用时出错，则改为 `tasks.startTask()` `submitHandler` 使用字符串 `err` 调用函数。</span><span class="sxs-lookup"><span data-stu-id="3ff39-146">3. If there was an error when invoking `tasks.startTask()`, the `submitHandler` function is called with an `err` string instead.</span></span> <br/><br/> <span data-ttu-id="3ff39-147">4. 还可以指定呼叫 `completionBotId` 时 - 在这种情况下，改为发送到 `teams.startTask()` `result` 自动程序。</span><span class="sxs-lookup"><span data-stu-id="3ff39-147">4. You can also specify a `completionBotId` when calling `teams.startTask()` - in that case `result` is sent to the bot instead.</span></span> | <span data-ttu-id="3ff39-148">1. 使用 TaskInfo 对象并包含要显示在任务模块弹出窗口中的自适应卡片的 JSON 调用 Teams 客户端 SDK `tasks.startTask()` [](#the-taskinfo-object) `TaskInfo.card` 函数。</span><span class="sxs-lookup"><span data-stu-id="3ff39-148">1. Call the Teams client SDK function `tasks.startTask()` with a [TaskInfo object](#the-taskinfo-object) and `TaskInfo.card` containing the JSON for the Adaptive card to show in the task module popup.</span></span> <br/><br/> <span data-ttu-id="3ff39-149">2. 如果在调用时出现错误，或者用户使用右上角的 X 关闭任务模块弹出窗口，则 Teams 会使用字符串调用 `submitHandler` `tasks.startTask()` `err` `tasks.startTask()` 它。</span><span class="sxs-lookup"><span data-stu-id="3ff39-149">2. If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with an `err` string if there was an error when invoking `tasks.startTask()` or if the user closes the task module popup using the X at the upper right.</span></span> <br/><br/> <span data-ttu-id="3ff39-150">3. 如果用户按下 Action.Submit 按钮，则其对象作为 `data` `result` 值返回。</span><span class="sxs-lookup"><span data-stu-id="3ff39-150">3. If the user presses an Action.Submit button then its `data` object is returned as the value of `result`.</span></span> |
| <span data-ttu-id="3ff39-151">**自动程序卡片按钮**</span><span class="sxs-lookup"><span data-stu-id="3ff39-151">**Bot card button**</span></span> | <span data-ttu-id="3ff39-152">1. 自动程序卡片按钮（具体取决于按钮类型）可以通过两种方式调用任务模块：深层链接 URL 或 `task/fetch` 发送消息。</span><span class="sxs-lookup"><span data-stu-id="3ff39-152">1. Bot card buttons, depending on the type of button, can invoke task modules in two ways: a deep link URL or by sending a `task/fetch` message.</span></span> <span data-ttu-id="3ff39-153">请参阅下文，了解链接 URL 的深入工作。</span><span class="sxs-lookup"><span data-stu-id="3ff39-153">See below for how deep link URLs work.</span></span> <br/><br/> <span data-ttu-id="3ff39-154">2. 如果按钮的操作是自适应卡片) 的 (按钮类型，则 (会向自动程序发送一个事件) 下的 HTTP POST，机器人使用 `type` `task/fetch` HTTP `Action.Submit` 200 响应 POST，响应正文包含 `task/fetch invoke` [TaskInfo](#the-taskinfo-object)对象周围的包装器。</span><span class="sxs-lookup"><span data-stu-id="3ff39-154">2. If the button's action `type` is `task/fetch` (`Action.Submit` button type for Adaptive cards), a `task/fetch invoke` event (an HTTP POST under the covers) is sent to the bot, and the bot responds to the POST with HTTP 200 and the response body containing a wrapper around the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="3ff39-155">这将详细介绍通过任务/提取[调用任务模块。](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch)</span><span class="sxs-lookup"><span data-stu-id="3ff39-155">This is explained in detail in [invoking a task module via task/fetch](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoking-a-task-module-via-taskfetch).</span></span><br/><br/> <span data-ttu-id="3ff39-156">3. Teams 显示任务模块;用户完成后，使用对象作为参数调用 Teams SDK `tasks.submitTask()` `result` 函数。</span><span class="sxs-lookup"><span data-stu-id="3ff39-156">3. Teams displays the task module; when the user is finished, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <br/><br/> <span data-ttu-id="3ff39-157">4. 自动程序收到 `task/submit invoke` 包含该对象 `result` 的消息。</span><span class="sxs-lookup"><span data-stu-id="3ff39-157">4. The bot receives a `task/submit invoke` message that contains the `result` object.</span></span> <span data-ttu-id="3ff39-158">有三种不同的方法来响应消息：不执行任何操作 (任务成功完成) ，在弹出窗口中向用户显示消息，或调用另一个任务模块窗口 (例如创建类似向导的体验 `task/submit`) 。</span><span class="sxs-lookup"><span data-stu-id="3ff39-158">You have three different ways to respond to the `task/submit` message: by doing nothing (the task completed successfully), by displaying a message to the user in a popup window, or by invoking another task module window (i.e. creating a wizard-like experience).</span></span> <span data-ttu-id="3ff39-159">在有关任务 [/提交的详细讨论中，将详细讨论这三个选项](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。</span><span class="sxs-lookup"><span data-stu-id="3ff39-159">These three options are discussed more [in the detailed discussion on task/submit](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> | <span data-ttu-id="3ff39-160">1. 与 Bot Framework 卡上的按钮类似，自适应卡片上的按钮支持两种调用任务模块的方法：包含按钮的深层链接 URL 以及 `Action.openUrl` `task/fetch` 通过使用 `Action.Submit` 按钮。</span><span class="sxs-lookup"><span data-stu-id="3ff39-160">1. Like buttons on Bot Framework cards, buttons on Adaptive cards support two ways of invoking task modules: deep link URLs with `Action.openUrl` buttons, and via `task/fetch` using `Action.Submit` buttons.</span></span> <br/><br/> <span data-ttu-id="3ff39-161">2. 具有自适应卡片的任务模块的运行方式与 HTML/JavaScript 用例 (左) 。</span><span class="sxs-lookup"><span data-stu-id="3ff39-161">2. Task modules with Adaptive cards work very similarly to the HTML/JavaScript case (see left).</span></span> <span data-ttu-id="3ff39-162">主要区别在于，由于在使用自适应卡片时没有 JavaScript，因此无法调用 `tasks.submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="3ff39-162">The major difference is that since there's no JavaScript when you're using Adaptive cards, there's no way to call `tasks.submitTask()`.</span></span> <span data-ttu-id="3ff39-163">相反，Teams 会从对象中取值，并返回该对象作为事件的有效负载， `data` `Action.Submit` `task/submit` 如此处 [所述](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。</span><span class="sxs-lookup"><span data-stu-id="3ff39-163">Instead, Teams takes the `data` object from `Action.Submit` and returns it as the payload of in the `task/submit` event, as described [here](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> |
| <span data-ttu-id="3ff39-164">**深层链接 URL**</span><span class="sxs-lookup"><span data-stu-id="3ff39-164">**Deep link URL**</span></span> <br/>[<span data-ttu-id="3ff39-165">URL 语法</span><span class="sxs-lookup"><span data-stu-id="3ff39-165">URL syntax</span></span>](#task-module-deep-link-syntax) | <span data-ttu-id="3ff39-166">1. Teams 调用任务模块;在深层链接的参数 `<iframe>` 中指定的内部出现的 `url` URL。</span><span class="sxs-lookup"><span data-stu-id="3ff39-166">1. Teams invokes the task module; the URL that appears inside the `<iframe>` specified in the `url` parameter of the deep link.</span></span> <span data-ttu-id="3ff39-167">没有 `submitHandler` 回调。</span><span class="sxs-lookup"><span data-stu-id="3ff39-167">There is no `submitHandler` callback.</span></span> <br/><br/> <span data-ttu-id="3ff39-168">2. 在任务模块中页面的 JavaScript 中，调用以将对象作为参数关闭它，与从选项卡或自动程序卡按钮调用对象 `tasks.submitTask()` `result` 时相同。</span><span class="sxs-lookup"><span data-stu-id="3ff39-168">2. Within the JavaScript of the page in the task module, call `tasks.submitTask()` to close it with a `result` object as a parameter, the same as when invoking it from a tab or a bot card button.</span></span> <span data-ttu-id="3ff39-169">但是，完成逻辑略有不同。</span><span class="sxs-lookup"><span data-stu-id="3ff39-169">Completion logic is slightly different, however.</span></span> <span data-ttu-id="3ff39-170">如果完成逻辑驻留在客户端 (即如果没有自动程序) 则没有回调，因此任何完成逻辑都必须位于调用 `submitHandler` 之前的代码。 `tasks.submitTask()`</span><span class="sxs-lookup"><span data-stu-id="3ff39-170">If your completion logic resides on the client (i.e. if there is no bot) there is no `submitHandler` callback, so any completion logic must be in the code preceding the call to `tasks.submitTask()`.</span></span> <span data-ttu-id="3ff39-171">仅通过控制台报告调用错误。</span><span class="sxs-lookup"><span data-stu-id="3ff39-171">Invocation errors are only reported via the console.</span></span> <span data-ttu-id="3ff39-172">如果你有自动程序，可以在深层链接中指定参数以 `completionBotId` 通过事件 `result` 发送 `task/submit` 对象。</span><span class="sxs-lookup"><span data-stu-id="3ff39-172">If you have a bot, then you can specify a `completionBotId` parameter in the deep link to send the `result` object via a `task/submit` event.</span></span> | <span data-ttu-id="3ff39-173">1. Teams 调用任务模块;自适应卡片的 JSON 卡正文指定为深层链接参数的 URL `card` 编码值。</span><span class="sxs-lookup"><span data-stu-id="3ff39-173">1. Teams invokes the task module; the JSON card body of the Adaptive card is specified as a URL-encoded value of the `card` parameter of the deep link.</span></span> <br/><br/> <span data-ttu-id="3ff39-174">2. 用户通过单击任务模块右上角的 X 或按卡片上的按钮来关闭任务 `Action.Submit` 模块。</span><span class="sxs-lookup"><span data-stu-id="3ff39-174">2. The user closes the task module by clicking on the X at the upper right of the task module or by pressing an `Action.Submit` button on the card.</span></span> <span data-ttu-id="3ff39-175">由于没有要调用的字段，因此你必须有一个自动程序将自适应 `submitHandler` 卡片字段的值发送到。</span><span class="sxs-lookup"><span data-stu-id="3ff39-175">Since there is no `submitHandler` to call, you must have a bot to send the value of the Adaptive card fields to.</span></span> <span data-ttu-id="3ff39-176">使用深层链接中的参数指定通过事件将数据 `completionBotId` 发送到的 `task/submit invoke` 自动程序。</span><span class="sxs-lookup"><span data-stu-id="3ff39-176">You use the `completionBotId` parameter in the deep link to specify the bot to send the data to via a `task/submit invoke` event.</span></span> |

> [!NOTE]
> <span data-ttu-id="3ff39-177">移动版不支持从 JavaScript 调用任务模块。</span><span class="sxs-lookup"><span data-stu-id="3ff39-177">Invoking a task module from JavaScript is not supported on mobile.</span></span>

## <a name="the-taskinfo-object"></a><span data-ttu-id="3ff39-178">TaskInfo 对象</span><span class="sxs-lookup"><span data-stu-id="3ff39-178">The TaskInfo object</span></span>

<span data-ttu-id="3ff39-179">该对象 `TaskInfo` 包含任务模块的元数据。</span><span class="sxs-lookup"><span data-stu-id="3ff39-179">The `TaskInfo` object contains the metadata for a task module.</span></span> <span data-ttu-id="3ff39-180">对象定义如下所示。</span><span class="sxs-lookup"><span data-stu-id="3ff39-180">The object definition is below.</span></span> <span data-ttu-id="3ff39-181">你必须 **为** 嵌入 `url` 的 iFrame (定义) ， (为自适应卡片 `card`) 。</span><span class="sxs-lookup"><span data-stu-id="3ff39-181">You **must** define either `url` (for an embedded iFrame) or `card` (for an Adaptive Card).</span></span>

| <span data-ttu-id="3ff39-182">属性</span><span class="sxs-lookup"><span data-stu-id="3ff39-182">Attribute</span></span> | <span data-ttu-id="3ff39-183">类型</span><span class="sxs-lookup"><span data-stu-id="3ff39-183">Type</span></span> | <span data-ttu-id="3ff39-184">说明</span><span class="sxs-lookup"><span data-stu-id="3ff39-184">Description</span></span> |
| --- | --- | --- |
| `title` | <span data-ttu-id="3ff39-185">string</span><span class="sxs-lookup"><span data-stu-id="3ff39-185">string</span></span> | <span data-ttu-id="3ff39-186">显示在应用名称下方，并出现在应用图标的右侧</span><span class="sxs-lookup"><span data-stu-id="3ff39-186">Appears below the app name and to the right of the app icon</span></span> |
| `height` | <span data-ttu-id="3ff39-187">number or string</span><span class="sxs-lookup"><span data-stu-id="3ff39-187">number or string</span></span> | <span data-ttu-id="3ff39-188">它可以是表示任务模块的高度（以像素为单位）或 `small` ， `medium` 或 `large` 。</span><span class="sxs-lookup"><span data-stu-id="3ff39-188">This can be a number representing the task module's height in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="3ff39-189">[请参阅下文，了解如何处理高度和宽度](#task-module-sizing)。</span><span class="sxs-lookup"><span data-stu-id="3ff39-189">[See below for how height and width are handled](#task-module-sizing).</span></span> |
| `width` | <span data-ttu-id="3ff39-190">number or string</span><span class="sxs-lookup"><span data-stu-id="3ff39-190">number or string</span></span> | <span data-ttu-id="3ff39-191">它可以是表示任务模块的宽度（以像素为单位）或 `small` ， `medium` 或 `large` 。</span><span class="sxs-lookup"><span data-stu-id="3ff39-191">This can be a number representing the task module's width in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="3ff39-192">[请参阅下文，了解如何处理高度和宽度](#task-module-sizing)。</span><span class="sxs-lookup"><span data-stu-id="3ff39-192">[See below for how height and width are handled](#task-module-sizing).</span></span> |
| `url` | <span data-ttu-id="3ff39-193">string</span><span class="sxs-lookup"><span data-stu-id="3ff39-193">string</span></span> | <span data-ttu-id="3ff39-194">作为任务模块内部加载 `<iframe>` 的页面的 URL。</span><span class="sxs-lookup"><span data-stu-id="3ff39-194">The URL of the page loaded as an `<iframe>` inside the task module.</span></span> <span data-ttu-id="3ff39-195">URL 的域必须在你的应用清单 [中的应用的 validDomains](~/resources/schema/manifest-schema.md#validdomains) 数组中。</span><span class="sxs-lookup"><span data-stu-id="3ff39-195">The URL's domain must be in the app's [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in your app's manifest.</span></span> |
| `card` | <span data-ttu-id="3ff39-196">自适应卡片或自适应卡片自动程序卡附件</span><span class="sxs-lookup"><span data-stu-id="3ff39-196">Adaptive card or an Adaptive card bot card attachment</span></span> | <span data-ttu-id="3ff39-197">要显示在任务模块中的自适应卡片的 JSON。</span><span class="sxs-lookup"><span data-stu-id="3ff39-197">The JSON for the Adaptive card to appear in the task module.</span></span> <span data-ttu-id="3ff39-198">如果从机器人调用，则需要在 Bot Framework 对象中使用自适应卡片 `attachment` JSON。</span><span class="sxs-lookup"><span data-stu-id="3ff39-198">If you're invoking from a bot, you'll need to use the Adaptive card JSON in a Bot Framework `attachment` object.</span></span> <span data-ttu-id="3ff39-199">从选项卡中，你只需使用自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="3ff39-199">From a tab you'll use just an Adaptive Card.</span></span> [<span data-ttu-id="3ff39-200">下面是一个示例。</span><span class="sxs-lookup"><span data-stu-id="3ff39-200">Here's an example.</span></span>](#adaptive-card-or-adaptive-card-bot-card-attachment) |
| `fallbackUrl` | <span data-ttu-id="3ff39-201">string</span><span class="sxs-lookup"><span data-stu-id="3ff39-201">string</span></span> | <span data-ttu-id="3ff39-202">如果客户端不支持任务模块功能，则此 URL 在浏览器选项卡中打开。</span><span class="sxs-lookup"><span data-stu-id="3ff39-202">If a client does not support the task module feature, this URL is opened in a browser tab.</span></span> |
| `completionBotId` | <span data-ttu-id="3ff39-203">string</span><span class="sxs-lookup"><span data-stu-id="3ff39-203">string</span></span> | <span data-ttu-id="3ff39-204">指定要发送用户与任务模块交互结果的自动程序应用 ID。</span><span class="sxs-lookup"><span data-stu-id="3ff39-204">Specifies a bot App ID to send the result of the user's interaction with the task module to.</span></span> <span data-ttu-id="3ff39-205">如果指定，机器人将在事件有效负载中接收 `task/submit invoke` 包含 JSON 对象的事件。</span><span class="sxs-lookup"><span data-stu-id="3ff39-205">If specified, the bot will receive a `task/submit invoke` event with a JSON object in the event payload.</span></span> |

> [!NOTE]
> <span data-ttu-id="3ff39-206">任务模块功能要求要加载的任何 URL 的域包含在应用清单的数组 `validDomains` 中。</span><span class="sxs-lookup"><span data-stu-id="3ff39-206">The task module feature requires that the domains of any URLs you want to load are included in the `validDomains` array in your app's manifest.</span></span>

## <a name="task-module-sizing"></a><span data-ttu-id="3ff39-207">任务模块大小调整</span><span class="sxs-lookup"><span data-stu-id="3ff39-207">Task module sizing</span></span>

<span data-ttu-id="3ff39-208">使用整数 `TaskInfo.width` 和 `TaskInfo.height` 将设置高度和宽度（以像素为单位）。</span><span class="sxs-lookup"><span data-stu-id="3ff39-208">Using integers for `TaskInfo.width` and `TaskInfo.height` will set the height and width in pixels.</span></span> <span data-ttu-id="3ff39-209">但是，根据团队窗口的大小和屏幕分辨率，它们将会按比例减少，同时保持纵横比 (宽度/高度) 。</span><span class="sxs-lookup"><span data-stu-id="3ff39-209">However, depending on the size of the Team's window and screen resolution they will be reduced proportionally while maintaining the aspect ratio (width/height).</span></span>

<span data-ttu-id="3ff39-210">If and are ， or the size of the red rectangle in the above is a proportion of the available `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` space： 20%， 50%， 60% for `width` and 20%， 50%， 66% for `height` .</span><span class="sxs-lookup"><span data-stu-id="3ff39-210">If `TaskInfo.width` and `TaskInfo.height` are `"small"`, `"medium"` or `"large"` the size of the red rectangle in the picture above is a proportion of the available space: 20%, 50%, 60% for `width` and 20%, 50%, 66% for `height`.</span></span>

<span data-ttu-id="3ff39-211">从选项卡调用的任务模块可以动态调整大小。</span><span class="sxs-lookup"><span data-stu-id="3ff39-211">Task modules invoked from a tab can be dynamically resized.</span></span> <span data-ttu-id="3ff39-212">调用后 `tasks.startTask()` ，可以调用 newSize 对象的高度和宽度属性符合 `tasks.updateTask(newSize)` TaskInfo 规范 (位置。</span><span class="sxs-lookup"><span data-stu-id="3ff39-212">After calling `tasks.startTask()` you can call `tasks.updateTask(newSize)` where height and width properties on the newSize object conform to the TaskInfo spec (ex.</span></span> <span data-ttu-id="3ff39-213">`{ height: 'medium', width: 'medium' }`).</span><span class="sxs-lookup"><span data-stu-id="3ff39-213">`{ height: 'medium', width: 'medium' }`).</span></span>

## <a name="task-module-css-for-htmljavascript-task-modules"></a><span data-ttu-id="3ff39-214">HTML/JavaScript 任务模块的任务模块 CSS</span><span class="sxs-lookup"><span data-stu-id="3ff39-214">Task module CSS for HTML/JavaScript task modules</span></span>

<span data-ttu-id="3ff39-215">基于 HTML/JavaScript 的任务模块可以访问标题下的任务模块的整个区域。</span><span class="sxs-lookup"><span data-stu-id="3ff39-215">HTML/JavaScript-based task modules have access to the entire area of the task module below the header.</span></span> <span data-ttu-id="3ff39-216">虽然这提供了极大的灵活性，但如果希望边缘周围的填充与页眉元素对齐，并避免不必要的滚动条，则需要提供正确的 CSS。</span><span class="sxs-lookup"><span data-stu-id="3ff39-216">While that offers a great deal of flexibility, if you want padding around the edges to align with the header elements and avoid unnecessary scrollbars you'll need to provide the right CSS.</span></span> <span data-ttu-id="3ff39-217">下面是几个用例的一些示例。</span><span class="sxs-lookup"><span data-stu-id="3ff39-217">Here are some examples for a few use cases.</span></span>

### <a name="example-1---youtube-video"></a><span data-ttu-id="3ff39-218">示例 1 - YouTube 视频</span><span class="sxs-lookup"><span data-stu-id="3ff39-218">Example 1 - YouTube video</span></span>

<span data-ttu-id="3ff39-219">YouTube 提供在网页上嵌入视频的能力。</span><span class="sxs-lookup"><span data-stu-id="3ff39-219">YouTube offers the ability to embed videos on web pages.</span></span> <span data-ttu-id="3ff39-220">使用简单的存根网页很容易在任务模块中显示：</span><span class="sxs-lookup"><span data-stu-id="3ff39-220">Using a simple stub web page it's easy to show this in a task module:</span></span>

![YouTube 视频](~/assets/images/task-module/youtube-example.png)

<span data-ttu-id="3ff39-222">下面是此页面的 HTML，不含 CSS：</span><span class="sxs-lookup"><span data-stu-id="3ff39-222">Here's the HTML for this page, without the CSS:</span></span>

```html
<!DOCTYPE html>
<html lang="en">
<head>
  ⋮
</head>
<body>
  <div id="embed-container">
    <iframe width="1000" height="700" src="https://www.youtube.com/embed/rd0Rd8w3FZ0" frameborder="0" allow="autoplay; encrypted-media" allowfullscreen=""></iframe>
  </div>
</body>
</html>
```

<span data-ttu-id="3ff39-223">CSS 如下所示：</span><span class="sxs-lookup"><span data-stu-id="3ff39-223">The CSS looks like this:</span></span>

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 95%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

### <a name="example-2---powerapp"></a><span data-ttu-id="3ff39-224">示例 2 - PowerApp</span><span class="sxs-lookup"><span data-stu-id="3ff39-224">Example 2 - PowerApp</span></span>

<span data-ttu-id="3ff39-225">您也可以使用相同的方法嵌入 PowerApp。</span><span class="sxs-lookup"><span data-stu-id="3ff39-225">You can use the same approach to embed a PowerApp as well.</span></span> <span data-ttu-id="3ff39-226">由于任何单个 PowerApp 的高度/宽度都是可自定义的，因此可能需要调整高度和宽度才能实现所需的演示文稿。</span><span class="sxs-lookup"><span data-stu-id="3ff39-226">As the height/width of any individual PowerApp is customizable, you may need to adjust the height and width to achieve your desired presentation.</span></span>

![资产管理 PowerApp](~/assets/images/task-module/powerapp-example.png)

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

<span data-ttu-id="3ff39-228">CSS 为：</span><span class="sxs-lookup"><span data-stu-id="3ff39-228">And the CSS is:</span></span>

```css
#embed-container iframe {
    position: absolute;
    top: 0;
    left: 0;
    width: 94%;
    height: 95%;
    padding-left: 20px;
    padding-right: 20px;
    padding-top: 10px;
    padding-bottom: 10px;
    border-style: none;
}
```

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a><span data-ttu-id="3ff39-229">自适应卡或自适应卡片自动程序卡附件</span><span class="sxs-lookup"><span data-stu-id="3ff39-229">Adaptive card or Adaptive card bot card attachment</span></span>

<span data-ttu-id="3ff39-230">如上所述，根据调用方式，你将需要使用自适应卡片或自适应卡片自动程序卡附件 (该附件只是包装在附件对象) 中的自适应卡片。 `card`</span><span class="sxs-lookup"><span data-stu-id="3ff39-230">As we noted above, depending on how you're invoking your `card` you'll need to use either an Adaptive card, or an Adaptive card bot card attachment (which is just an Adaptive card wrapped in an attachment object).</span></span>

<span data-ttu-id="3ff39-231">从选项卡调用时，将需要使用自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="3ff39-231">When you're invoking from a tab, you'll need to use an adaptive card.</span></span> <span data-ttu-id="3ff39-232">下面是一个非常简单的示例：</span><span class="sxs-lookup"><span data-stu-id="3ff39-232">Here's a very simple example:</span></span>

```json
{
    "type": "AdaptiveCard",
    "body": [
        {
            "type": "TextBlock",
            "text": "Here is a ninja cat:"
        },
        {
            "type": "Image",
            "url": "http://adaptivecards.io/content/cats/1.png",
            "size": "Medium"
        }
    ],
    "version": "1.0"
}
```

<span data-ttu-id="3ff39-233">当你从机器人调用时，你将需要使用自适应卡片自动程序卡附件，如以下示例所示：</span><span class="sxs-lookup"><span data-stu-id="3ff39-233">When you're invoking from a bot you'll need to use an Adaptive card bot card attachment as in the example below:</span></span>

```json
{
    "contentType": "application/vnd.microsoft.card.adaptive",
    "content": {
        "type": "AdaptiveCard",
        "body": [
            {
                "type": "TextBlock",
                "text": "Here is a ninja cat:"
            },
            {
                "type": "Image",
                "url": "http://adaptivecards.io/content/cats/1.png",
                "size": "Medium"
            }
        ],
        "version": "1.0"
    }
}
```

<span data-ttu-id="3ff39-234">你将需要记住是调用包含自动程序或选项卡中的自适应卡片的任务模块。</span><span class="sxs-lookup"><span data-stu-id="3ff39-234">You'll need to remember whether you are invoking a task module containing an Adaptive card from a bot or a tab.</span></span>

## <a name="task-module-deep-link-syntax"></a><span data-ttu-id="3ff39-235">任务模块深层链接语法</span><span class="sxs-lookup"><span data-stu-id="3ff39-235">Task module deep link syntax</span></span>

<span data-ttu-id="3ff39-236">任务模块深层链接只是包含其他两条信息的[TaskInfo](#the-taskinfo-object)对象的序列化，并且 `APP_ID` 可选： `BOT_APP_ID`</span><span class="sxs-lookup"><span data-stu-id="3ff39-236">A task module deep link is just a serialization of the [TaskInfo object](#the-taskinfo-object) with two other pieces of information, `APP_ID` and optionally the `BOT_APP_ID`:</span></span>

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

<span data-ttu-id="3ff39-237">有关[数据类型和允许](#the-taskinfo-object)的值，请参阅 TaskInfo 对象，以及 `<TaskInfo.url>` 。 `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>`</span><span class="sxs-lookup"><span data-stu-id="3ff39-237">See [TaskInfo object](#the-taskinfo-object) for the data types and allowable values for `<TaskInfo.url>`, `<TaskInfo.card>`, `<TaskInfo.height>`, `<TaskInfo.width>`, and `<TaskInfo.title>`.</span></span>

> [!TIP]
> <span data-ttu-id="3ff39-238">请确保 URL 对深层链接进行编码，尤其是在使用参数 (`card` 例如，JavaScript[ `encodeURI()` 的函数) 。](https://www.w3schools.com/jsref/jsref_encodeURI.asp)</span><span class="sxs-lookup"><span data-stu-id="3ff39-238">Be sure to URL encode the deep link, especially when using the `card` parameter (for example, JavaScript's [`encodeURI()` function](https://www.w3schools.com/jsref/jsref_encodeURI.asp)).</span></span>

<span data-ttu-id="3ff39-239">以下是有关和 `APP_ID` `BOT_APP_ID` 的信息：</span><span class="sxs-lookup"><span data-stu-id="3ff39-239">Here's the information on `APP_ID` and `BOT_APP_ID`:</span></span>

| <span data-ttu-id="3ff39-240">值</span><span class="sxs-lookup"><span data-stu-id="3ff39-240">Value</span></span> | <span data-ttu-id="3ff39-241">类型</span><span class="sxs-lookup"><span data-stu-id="3ff39-241">Type</span></span> | <span data-ttu-id="3ff39-242">是否必需？</span><span class="sxs-lookup"><span data-stu-id="3ff39-242">Required?</span></span> | <span data-ttu-id="3ff39-243">说明</span><span class="sxs-lookup"><span data-stu-id="3ff39-243">Description</span></span> |
| --- | --- | --- | --- |
| `APP_ID` | <span data-ttu-id="3ff39-244">string</span><span class="sxs-lookup"><span data-stu-id="3ff39-244">string</span></span> | <span data-ttu-id="3ff39-245">是</span><span class="sxs-lookup"><span data-stu-id="3ff39-245">Yes</span></span> | <span data-ttu-id="3ff39-246">[调用](~/resources/schema/manifest-schema.md#id)任务模块的应用的 ID。</span><span class="sxs-lookup"><span data-stu-id="3ff39-246">The [id](~/resources/schema/manifest-schema.md#id) of the app invoking the task module.</span></span> <span data-ttu-id="3ff39-247">[清单中的 validDomains](~/resources/schema/manifest-schema.md#validdomains)数组 `APP_ID` 必须包含 if `url` `url` 的域。</span><span class="sxs-lookup"><span data-stu-id="3ff39-247">The [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in the manifest for `APP_ID` must contain the domain for `url` if `url` is in the URL.</span></span> <span data-ttu-id="3ff39-248"> (从选项卡或自动程序调用任务模块时，应用 ID 已已知，这就是它未包含在 `TaskInfo` .) </span><span class="sxs-lookup"><span data-stu-id="3ff39-248">(The app ID is already known when a task module is invoked from a tab or a bot, which is why it's not included in `TaskInfo`.)</span></span> |
| `BOT_APP_ID` | <span data-ttu-id="3ff39-249">string</span><span class="sxs-lookup"><span data-stu-id="3ff39-249">string</span></span> | <span data-ttu-id="3ff39-250">否</span><span class="sxs-lookup"><span data-stu-id="3ff39-250">No</span></span> | <span data-ttu-id="3ff39-251">如果指定了值 `completionBotId` ，则对象通过消息发送给 `result` `task/submit invoke` 指定的自动程序。</span><span class="sxs-lookup"><span data-stu-id="3ff39-251">If a value for `completionBotId` is specified, the `result` object is sent via a a `task/submit invoke` message to the specified bot.</span></span> <span data-ttu-id="3ff39-252">`BOT_APP_ID` 必须指定为应用清单中的自动程序，即不能只将其发送到任何自动程序。</span><span class="sxs-lookup"><span data-stu-id="3ff39-252">`BOT_APP_ID` must be specified as a bot in the app's manifest, i.e. you can't just send it to any bot.</span></span> |

<span data-ttu-id="3ff39-253">请注意，它有效且相同，并且在许多情况下，如果应用具有自动程序，因为建议在有自动程序时将该应用用作 `APP_ID` `BOT_APP_ID` 应用的 ID。</span><span class="sxs-lookup"><span data-stu-id="3ff39-253">Note that it's valid for `APP_ID` and `BOT_APP_ID` to be the same, and in many cases will be if an app has a bot since it's recommended to use that as an app's ID if there is one.</span></span>

## <a name="keyboard-and-accessibility-guidelines"></a><span data-ttu-id="3ff39-254">键盘和辅助功能指南</span><span class="sxs-lookup"><span data-stu-id="3ff39-254">Keyboard and accessibility guidelines</span></span>

<span data-ttu-id="3ff39-255">对于基于 HTML/JavaScript 的任务模块，你有责任确保应用的任务模块可以与键盘一同使用。</span><span class="sxs-lookup"><span data-stu-id="3ff39-255">With HTML/JavaScript-based task modules it is your responsibility to ensure your app's task module can be used with a keyboard.</span></span> <span data-ttu-id="3ff39-256">屏幕阅读器程序还取决于使用键盘导航的能力。</span><span class="sxs-lookup"><span data-stu-id="3ff39-256">Screen reader programs also depend on the ability to navigate using the keyboard.</span></span> <span data-ttu-id="3ff39-257">从实践上说，这意味着两点：</span><span class="sxs-lookup"><span data-stu-id="3ff39-257">As a practical matter this means two things:</span></span>

1. <span data-ttu-id="3ff39-258">使用 HTML 标记中的[tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex)属性控制哪些元素可以聚焦以及是否/在何处参与顺序键盘导航 (通常使用 Tab 键和<kbd>Shift-Tab</kbd>键) 。 <kbd></kbd></span><span class="sxs-lookup"><span data-stu-id="3ff39-258">Using the [tabindex attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) in your HTML tags to control which elements can be focused and if/where it participates in sequential keyboard navigation (usually with the <kbd>Tab</kbd> and <kbd>Shift-Tab</kbd> keys).</span></span>
2. <span data-ttu-id="3ff39-259">处理任务模块的 JavaScript 中的 <kbd>Esc</kbd> 键。</span><span class="sxs-lookup"><span data-stu-id="3ff39-259">Handling the <kbd>Esc</kbd> key in the JavaScript for your task module.</span></span> <span data-ttu-id="3ff39-260">下面是显示如何执行此操作的代码示例：</span><span class="sxs-lookup"><span data-stu-id="3ff39-260">Here's a code sample showing how to do this:</span></span>

  ```javascript
  // Handle the Esc key
  document.onkeyup = function(event) {
  if ((event.key === 27) || (event.key === "Escape")) {
    microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
    }
  }
  ```

<span data-ttu-id="3ff39-261">Microsoft Teams 将确保键盘导航从任务模块标头正常转换为 HTML，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="3ff39-261">Microsoft Teams will ensure that keyboard navigation works properly from the task module header into your HTML and vice-versa.</span></span>

## <a name="task-module-samples"></a><span data-ttu-id="3ff39-262">任务模块示例</span><span class="sxs-lookup"><span data-stu-id="3ff39-262">Task module samples</span></span>

* [<span data-ttu-id="3ff39-263">Node.js/TypeScript 示例</span><span class="sxs-lookup"><span data-stu-id="3ff39-263">Node.js/TypeScript sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs)
* [<span data-ttu-id="3ff39-264">C#/.NET 示例</span><span class="sxs-lookup"><span data-stu-id="3ff39-264">C#/.NET sample</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp)

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ff39-265">了解更多信息：请求设备权限</span><span class="sxs-lookup"><span data-stu-id="3ff39-265">Learn  more: Request device permissions</span></span>](../concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="3ff39-266">了解更多信息：集成媒体功能</span><span class="sxs-lookup"><span data-stu-id="3ff39-266">Learn more: Integrate media capabilities</span></span>](../concepts/device-capabilities/mobile-camera-image-permissions.md)
