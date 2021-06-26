---
title: 调用和消除任务模块
description: 调用和消除任务模块。
author: surbhigupta12
ms.topic: conceptual
localization_priority: Normal
ms.openlocfilehash: a23d5cee3f13967772a4b58ed973bf08906e36a6
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140767"
---
# <a name="invoke-and-dismiss-task-modules"></a><span data-ttu-id="a9365-103">调用和消除任务模块</span><span class="sxs-lookup"><span data-stu-id="a9365-103">Invoke and dismiss task modules</span></span>

<span data-ttu-id="a9365-104">可以从选项卡、自动程序或深层链接调用任务模块。</span><span class="sxs-lookup"><span data-stu-id="a9365-104">Task modules can be invoked from tabs, bots, or deep links.</span></span> <span data-ttu-id="a9365-105">响应可以是 HTML、JavaScript 或自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="a9365-105">The response can be either in HTML, JavaScript, or as an Adaptive Card.</span></span> <span data-ttu-id="a9365-106">在如何调用任务模块以及如何处理用户交互的响应方面，存在很多灵活性。</span><span class="sxs-lookup"><span data-stu-id="a9365-106">There is a lot of flexibility in terms of how task modules are invoked and how to deal with the response of the user's interaction.</span></span> <span data-ttu-id="a9365-107">下表总结了此操作的工作原理：</span><span class="sxs-lookup"><span data-stu-id="a9365-107">The following table summarizes how this works:</span></span>

| <span data-ttu-id="a9365-108">使用 调用</span><span class="sxs-lookup"><span data-stu-id="a9365-108">Invoked using</span></span> | <span data-ttu-id="a9365-109">包含 HTML 或 JavaScript 的任务模块</span><span class="sxs-lookup"><span data-stu-id="a9365-109">Task module with HTML or JavaScript</span></span> | <span data-ttu-id="a9365-110">具有自适应卡片的任务模块</span><span class="sxs-lookup"><span data-stu-id="a9365-110">Task module with Adaptive Card</span></span> |
| --- | --- | --- |
| <span data-ttu-id="a9365-111">选项卡中的 JavaScript</span><span class="sxs-lookup"><span data-stu-id="a9365-111">JavaScript in a tab</span></span> | <span data-ttu-id="a9365-112">1. 将 Teams客户端 SDK 函数 `tasks.startTask()` 与可选回调 `submitHandler(err, result)` 函数一同使用。</span><span class="sxs-lookup"><span data-stu-id="a9365-112">1. Use the Teams client SDK function `tasks.startTask()` with an optional `submitHandler(err, result)` callback function.</span></span> <br/><br/> <span data-ttu-id="a9365-113">2. 在任务模块代码中，当用户已执行这些操作时，Teams对象作为参数调用 SDK `tasks.submitTask()` `result` 函数。</span><span class="sxs-lookup"><span data-stu-id="a9365-113">2. In the task module code, when the user has performed the actions, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="a9365-114">如果在 `submitHandler` 中指定了回调 `tasks.startTask()` ，Teams使用 作为 `result` 参数调用它。</span><span class="sxs-lookup"><span data-stu-id="a9365-114">If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with `result` as a parameter.</span></span> <span data-ttu-id="a9365-115">如果在调用 时出错，则 `tasks.startTask()` `submitHandler` 改为使用字符串调用 `err` 函数。</span><span class="sxs-lookup"><span data-stu-id="a9365-115">If there was an error when invoking `tasks.startTask()`, the `submitHandler` function is called with an `err` string instead.</span></span> <br/><br/> <span data-ttu-id="a9365-116">3.还可以在调用 时 `completionBotId` 指定 `teams.startTask()` 。</span><span class="sxs-lookup"><span data-stu-id="a9365-116">3. You can also specify a `completionBotId` when calling `teams.startTask()`.</span></span> <span data-ttu-id="a9365-117">然后 `result` ，将 改为发送到自动程序。</span><span class="sxs-lookup"><span data-stu-id="a9365-117">Then the `result` is sent to the bot instead.</span></span> | <span data-ttu-id="a9365-118">1. 使用 TaskInfo Teams包含要显示在任务模块弹出窗口中的自适应卡片的 JSON 来调用客户端 SDK `tasks.startTask()` [](#the-taskinfo-object) `TaskInfo.card` 函数。</span><span class="sxs-lookup"><span data-stu-id="a9365-118">1. Call the Teams client SDK function `tasks.startTask()` with a [TaskInfo object](#the-taskinfo-object) and `TaskInfo.card` containing the JSON for the Adaptive Card to show in the task module pop-up.</span></span> <br/><br/> <span data-ttu-id="a9365-119">2. 如果在 中指定了回调，Teams如果调用时出错或者用户关闭任务模块弹出窗口（使用右上角的 `submitHandler` `tasks.startTask()` `err` X）以字符串调用它 `tasks.startTask()` 。</span><span class="sxs-lookup"><span data-stu-id="a9365-119">2. If a `submitHandler` callback was specified in `tasks.startTask()`, Teams calls it with an `err` string, if there was an error when invoking `tasks.startTask()` or if the user closes the task module pop-up using the X at the upper right.</span></span> <br/><br/> <span data-ttu-id="a9365-120">3. 如果用户按下某个 `Action.Submit` 按钮，则其 `data` 对象将返回为 的值 `result` 。</span><span class="sxs-lookup"><span data-stu-id="a9365-120">3. If the user presses an `Action.Submit` button then its `data` object is returned as the value of `result`.</span></span> |
| <span data-ttu-id="a9365-121">自动程序卡按钮</span><span class="sxs-lookup"><span data-stu-id="a9365-121">Bot card button</span></span> | <span data-ttu-id="a9365-122">1. 自动程序卡片按钮可以通过两种方式（深度链接 URL 或发送消息）调用任务模块，具体取决于按钮 `task/fetch` 的类型。</span><span class="sxs-lookup"><span data-stu-id="a9365-122">1. Bot card buttons, depending on the type of button, can invoke task modules in two ways, a deep link URL or by sending a `task/fetch` message.</span></span> <br/><br/> <span data-ttu-id="a9365-123">2. 如果按钮的操作是自适应卡片的按钮类型，则 HTTP POST 事件 `type` `task/fetch` 将发送给 `Action.Submit` `task/fetch invoke` 机器人。</span><span class="sxs-lookup"><span data-stu-id="a9365-123">2. If the button's action `type` is `task/fetch` that is `Action.Submit` button type for Adaptive Cards, a `task/fetch invoke` event that is an HTTP POST is sent to the bot.</span></span> <span data-ttu-id="a9365-124">机器人使用 HTTP 200 响应 POST，响应正文包含 [TaskInfo 对象周围的包装](#the-taskinfo-object)器。</span><span class="sxs-lookup"><span data-stu-id="a9365-124">The bot responds to the POST with HTTP 200 and the response body containing a wrapper around the [TaskInfo object](#the-taskinfo-object).</span></span> <span data-ttu-id="a9365-125">有关详细信息，请参阅使用[调用任务模块 `task/fetch` ](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch)。</span><span class="sxs-lookup"><span data-stu-id="a9365-125">For more information, see [invoking a task module using `task/fetch`](~/task-modules-and-cards/task-modules/task-modules-bots.md#invoke-a-task-module-using-taskfetch).</span></span> <span data-ttu-id="a9365-126">Teams任务模块。</span><span class="sxs-lookup"><span data-stu-id="a9365-126">Teams displays the task module.</span></span> <br/><br/> <span data-ttu-id="a9365-127">3. 用户执行这些操作后，Teams对象作为参数调用 sdk `tasks.submitTask()` `result` 函数。</span><span class="sxs-lookup"><span data-stu-id="a9365-127">3. After the user has performed the actions, call the Teams SDK function `tasks.submitTask()` with a `result` object as a parameter.</span></span> <span data-ttu-id="a9365-128">机器人会收到 `task/submit invoke` 一条消息，其中包含 `result` 对象。</span><span class="sxs-lookup"><span data-stu-id="a9365-128">The bot receives a `task/submit invoke` message that contains the `result` object.</span></span> <br/><br/> <span data-ttu-id="a9365-129">4. 通过不执行任何操作（即任务成功完成、在弹出窗口中向用户显示消息或调用另一个任务模块窗口）来响应邮件，你有三种不同的方法。 `task/submit`</span><span class="sxs-lookup"><span data-stu-id="a9365-129">4. You have three different ways to respond to the `task/submit` message, by doing nothing that is the task completed successfully, by displaying a message to the user in a pop-up window, or by invoking another task module window.</span></span> <span data-ttu-id="a9365-130">有关详细信息，请参阅[上的详细说明 `task/submit` ](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。</span><span class="sxs-lookup"><span data-stu-id="a9365-130">For more information, see [detailed discussion on `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> | <ul><li> <span data-ttu-id="a9365-131">与 Bot Framework 卡上的按钮类似，自适应卡片上的按钮支持两种调用任务模块的方法、包含按钮的深层链接 URL `Action.openUrl` `task/fetch` 和使用 `Action.Submit` 按钮。</span><span class="sxs-lookup"><span data-stu-id="a9365-131">Like buttons on Bot Framework cards, buttons on Adaptive Cards support two ways of invoking task modules, deep link URLs with `Action.openUrl` buttons, and `task/fetch` using `Action.Submit` buttons.</span></span> </li></ul> <br/><br/> <ul><li> <span data-ttu-id="a9365-132">具有自适应卡片的任务模块与 HTML 或 JavaScript 的情况非常类似。</span><span class="sxs-lookup"><span data-stu-id="a9365-132">Task modules with Adaptive Cards work very similarly to the HTML or JavaScript case.</span></span> <span data-ttu-id="a9365-133">主要区别在于，由于在使用自适应卡片时没有 JavaScript，因此无法调用 `tasks.submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="a9365-133">The major difference is that since there is no JavaScript when you are using Adaptive Cards, there is no way to call `tasks.submitTask()`.</span></span> <span data-ttu-id="a9365-134">相反，Teams对象， `data` `Action.Submit` 并返回该对象作为事件 `task/submit` 的有效负载。</span><span class="sxs-lookup"><span data-stu-id="a9365-134">Instead, Teams takes the `data` object from `Action.Submit` and returns it as the payload of the `task/submit` event.</span></span> <span data-ttu-id="a9365-135">有关详细信息，请参阅[的灵活性 `task/submit` ](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit)。</span><span class="sxs-lookup"><span data-stu-id="a9365-135">For more information, see [flexibility of `task/submit`](~/task-modules-and-cards/task-modules/task-modules-bots.md#the-flexibility-of-tasksubmit).</span></span> </li></ul> |
| <span data-ttu-id="a9365-136">深层链接 URL</span><span class="sxs-lookup"><span data-stu-id="a9365-136">Deep link URL</span></span> <br/>[<span data-ttu-id="a9365-137">URL 语法</span><span class="sxs-lookup"><span data-stu-id="a9365-137">URL syntax</span></span>](#task-module-deep-link-syntax) | <span data-ttu-id="a9365-138">1. Teams调用任务模块，该模块是显示在深层链接的参数中指定的内的 `<iframe>` `url` URL。</span><span class="sxs-lookup"><span data-stu-id="a9365-138">1. Teams invokes the task module that is the URL that appears inside the `<iframe>` specified in the `url` parameter of the deep link.</span></span> <span data-ttu-id="a9365-139">没有 `submitHandler` 回调。</span><span class="sxs-lookup"><span data-stu-id="a9365-139">There is no `submitHandler` callback.</span></span> <br/><br/> <span data-ttu-id="a9365-140">2. 在任务模块中页面的 JavaScript 内，调用 以使用对象作为参数关闭它，就像从选项卡或自动程序卡按钮调用它一 `tasks.submitTask()` `result` 样。</span><span class="sxs-lookup"><span data-stu-id="a9365-140">2. Within the JavaScript of the page in the task module, call `tasks.submitTask()` to close it with a `result` object as a parameter, the same as when invoking it from a tab or a bot card button.</span></span> <span data-ttu-id="a9365-141">但是，完成逻辑略有不同。</span><span class="sxs-lookup"><span data-stu-id="a9365-141">However, completion logic is slightly different.</span></span> <span data-ttu-id="a9365-142">如果完成逻辑驻留在没有自动程序的客户端上，则没有回调，因此任何完成逻辑都必须位于 调用 之前 `submitHandler` 的代码 `tasks.submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="a9365-142">If your completion logic resides on the client that is if there is no bot, there is no `submitHandler` callback, so any completion logic must be in the code preceding the call to `tasks.submitTask()`.</span></span> <span data-ttu-id="a9365-143">调用错误仅通过控制台报告。</span><span class="sxs-lookup"><span data-stu-id="a9365-143">Invocation errors are only reported through the console.</span></span> <span data-ttu-id="a9365-144">如果你有自动程序，可以在深度链接中指定参数以 `completionBotId` 通过事件 `result` 发送 `task/submit` 对象。</span><span class="sxs-lookup"><span data-stu-id="a9365-144">If you have a bot, then you can specify a `completionBotId` parameter in the deep link to send the `result` object through a `task/submit` event.</span></span> | <span data-ttu-id="a9365-145">1. Teams调用任务模块，该任务模块是自适应卡片的 JSON 卡片正文，指定为深层链接参数的 URL 编码 `card` 值。</span><span class="sxs-lookup"><span data-stu-id="a9365-145">1. Teams invokes the task module that is the JSON card body of the Adaptive Card that is specified as a URL-encoded value of the `card` parameter of the deep link.</span></span> <br/><br/> <span data-ttu-id="a9365-146">2. 用户通过选择任务模块右上角的 X 或按卡片上的按钮来 `Action.Submit` 关闭任务模块。</span><span class="sxs-lookup"><span data-stu-id="a9365-146">2. The user closes the task module by selecting the X at the upper right of the task module or by pressing an `Action.Submit` button on the card.</span></span> <span data-ttu-id="a9365-147">由于没有要调用的项，因此用户必须具有自动程序来发送自适应卡片 `submitHandler` 字段的值。</span><span class="sxs-lookup"><span data-stu-id="a9365-147">Since there is no `submitHandler` to call, the user must have a bot to send the value of the Adaptive Card fields.</span></span> <span data-ttu-id="a9365-148">用户必须使用深层链接中的 参数指定使用事件 `completionBotId` 将数据发送到的 `task/submit invoke` 自动程序。</span><span class="sxs-lookup"><span data-stu-id="a9365-148">The user must use the `completionBotId` parameter in the deep link to specify the bot to send the data to using a `task/submit invoke` event.</span></span> |

> [!NOTE]
> <span data-ttu-id="a9365-149">移动版不支持从 JavaScript 调用任务模块。</span><span class="sxs-lookup"><span data-stu-id="a9365-149">Invoking a task module from JavaScript is not supported on mobile.</span></span>

<span data-ttu-id="a9365-150">下一节指定定义任务模块 `TaskInfo` 的某些属性的对象。</span><span class="sxs-lookup"><span data-stu-id="a9365-150">The next section specifies the `TaskInfo` object that defines certain attributes for a task module.</span></span>

## <a name="the-taskinfo-object"></a><span data-ttu-id="a9365-151">TaskInfo 对象</span><span class="sxs-lookup"><span data-stu-id="a9365-151">The TaskInfo object</span></span>

<span data-ttu-id="a9365-152">`TaskInfo`对象包含任务模块的元数据。</span><span class="sxs-lookup"><span data-stu-id="a9365-152">The `TaskInfo` object contains the metadata for a task module.</span></span> <span data-ttu-id="a9365-153">为 `url` 嵌入的 iFrame 或 `card` 自适应卡片定义 。</span><span class="sxs-lookup"><span data-stu-id="a9365-153">Define the `url` for an embedded iFrame or `card` for an Adaptive Card.</span></span> <span data-ttu-id="a9365-154">下表提供了对象定义：</span><span class="sxs-lookup"><span data-stu-id="a9365-154">The following table provides the object definition:</span></span>

| <span data-ttu-id="a9365-155">属性</span><span class="sxs-lookup"><span data-stu-id="a9365-155">Attribute</span></span> | <span data-ttu-id="a9365-156">类型</span><span class="sxs-lookup"><span data-stu-id="a9365-156">Type</span></span> | <span data-ttu-id="a9365-157">说明</span><span class="sxs-lookup"><span data-stu-id="a9365-157">Description</span></span> |
| --- | --- | --- |
| `title` | <span data-ttu-id="a9365-158">string</span><span class="sxs-lookup"><span data-stu-id="a9365-158">string</span></span> | <span data-ttu-id="a9365-159">此属性显示在应用名称下方和应用图标右侧。</span><span class="sxs-lookup"><span data-stu-id="a9365-159">This attribute appears below the app name and to the right of the app icon.</span></span> |
| `height` | <span data-ttu-id="a9365-160">number or string</span><span class="sxs-lookup"><span data-stu-id="a9365-160">number or string</span></span> | <span data-ttu-id="a9365-161">此属性可以是一个数字，表示任务模块的高度，以像素为单位，或 `small` 、 或 `medium` `large` 。</span><span class="sxs-lookup"><span data-stu-id="a9365-161">This attribute can be a number representing the task module's height in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="a9365-162">有关详细信息，请参阅任务 [模块大小调整](#task-module-sizing)。</span><span class="sxs-lookup"><span data-stu-id="a9365-162">For more information, see [task module sizing](#task-module-sizing).</span></span> |
| `width` | <span data-ttu-id="a9365-163">number or string</span><span class="sxs-lookup"><span data-stu-id="a9365-163">number or string</span></span> | <span data-ttu-id="a9365-164">此属性可以是一个数字，表示任务模块的宽度，以像素为单位，或 `small` 、 或 `medium` `large` 。</span><span class="sxs-lookup"><span data-stu-id="a9365-164">This attribute can be a number representing the task module's width in pixels, or `small`, `medium`, or `large`.</span></span> <span data-ttu-id="a9365-165">有关详细信息，请参阅任务 [模块大小调整](#task-module-sizing)。</span><span class="sxs-lookup"><span data-stu-id="a9365-165">For more information, see [task module sizing](#task-module-sizing).</span></span> |
| `url` | <span data-ttu-id="a9365-166">string</span><span class="sxs-lookup"><span data-stu-id="a9365-166">string</span></span> | <span data-ttu-id="a9365-167">此属性是作为任务模块内部加载的页面 `<iframe>` 的 URL。</span><span class="sxs-lookup"><span data-stu-id="a9365-167">This attribute is the URL of the page loaded as an `<iframe>` inside the task module.</span></span> <span data-ttu-id="a9365-168">URL 的域必须在你的应用清单中的 [应用的 validDomains](~/resources/schema/manifest-schema.md#validdomains) 数组中。</span><span class="sxs-lookup"><span data-stu-id="a9365-168">The URL's domain must be in the app's [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in your app's manifest.</span></span> |
| `card` | <span data-ttu-id="a9365-169">自适应卡片或自适应卡片自动程序卡附件</span><span class="sxs-lookup"><span data-stu-id="a9365-169">Adaptive Card or Adaptive Card bot card attachment</span></span> | <span data-ttu-id="a9365-170">此属性是要显示在任务模块中的自适应卡片的 JSON。</span><span class="sxs-lookup"><span data-stu-id="a9365-170">This attribute is the JSON for the Adaptive Card to appear in the task module.</span></span> <span data-ttu-id="a9365-171">如果用户从自动程序调用，请使用 Bot Framework 对象中的自适应卡片 `attachment` JSON。</span><span class="sxs-lookup"><span data-stu-id="a9365-171">If the user is invoking from a bot, use the Adaptive Card JSON in a Bot Framework `attachment` object.</span></span> <span data-ttu-id="a9365-172">在选项卡中，用户必须使用自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="a9365-172">From a tab, the user must use an Adaptive Card.</span></span> <span data-ttu-id="a9365-173">有关详细信息，请参阅自适应 [卡片或自适应卡片自动程序卡附件](#adaptive-card-or-adaptive-card-bot-card-attachment)</span><span class="sxs-lookup"><span data-stu-id="a9365-173">For more information, see [Adaptive Card or Adaptive Card bot card attachment](#adaptive-card-or-adaptive-card-bot-card-attachment)</span></span> |
| `fallbackUrl` | <span data-ttu-id="a9365-174">string</span><span class="sxs-lookup"><span data-stu-id="a9365-174">string</span></span> | <span data-ttu-id="a9365-175">如果客户端不支持任务模块功能，则此属性将在浏览器选项卡中打开 URL。</span><span class="sxs-lookup"><span data-stu-id="a9365-175">This attribute opens the URL in a browser tab, if a client does not support the task module feature.</span></span> |
| `completionBotId` | <span data-ttu-id="a9365-176">string</span><span class="sxs-lookup"><span data-stu-id="a9365-176">string</span></span> | <span data-ttu-id="a9365-177">此属性指定要发送用户与任务模块交互结果的自动程序应用 ID。</span><span class="sxs-lookup"><span data-stu-id="a9365-177">This attribute specifies a bot App ID to send the result of the user's interaction with the task module.</span></span> <span data-ttu-id="a9365-178">如果指定，机器人将接收事件负载 `task/submit invoke` 中具有 JSON 对象的事件。</span><span class="sxs-lookup"><span data-stu-id="a9365-178">If specified, the bot receives a `task/submit invoke` event with a JSON object in the event payload.</span></span> |

> [!NOTE]
> <span data-ttu-id="a9365-179">任务模块功能要求要加载的任何 URL 的域包含在应用清单的数组 `validDomains` 中。</span><span class="sxs-lookup"><span data-stu-id="a9365-179">The task module feature requires that the domains of any URLs you want to load are included in the `validDomains` array in your app's manifest.</span></span>

<span data-ttu-id="a9365-180">下一节指定允许用户设置任务模块的高度和宽度的任务模块大小。</span><span class="sxs-lookup"><span data-stu-id="a9365-180">The next section specifies task module sizing that enables the user to set the height and width of the task module.</span></span>

## <a name="task-module-sizing"></a><span data-ttu-id="a9365-181">任务模块大小调整</span><span class="sxs-lookup"><span data-stu-id="a9365-181">Task module sizing</span></span>

<span data-ttu-id="a9365-182">使用 和 的整数设置任务模块的高度和宽度 `TaskInfo.width` `TaskInfo.height` （以像素为单位）。</span><span class="sxs-lookup"><span data-stu-id="a9365-182">Using integers for `TaskInfo.width` and `TaskInfo.height`, sets the height and width of the task module in pixels.</span></span> <span data-ttu-id="a9365-183">但是，根据团队窗口的大小和屏幕分辨率，它们按比例减少，同时保持宽度或高度的纵横比。</span><span class="sxs-lookup"><span data-stu-id="a9365-183">However, depending on the size of the Team's window and screen resolution they are reduced proportionally while maintaining the aspect ratio that is width or height.</span></span>

<span data-ttu-id="a9365-184">如果 和 为 、 或 ，则以下图像中红色矩形的大小与可用空间的比例为 `TaskInfo.width` `TaskInfo.height` `"small"` `"medium"` `"large"` 20%、50% 和 60%，对于 `width` `height` ：</span><span class="sxs-lookup"><span data-stu-id="a9365-184">If `TaskInfo.width` and `TaskInfo.height` are `"small"`, `"medium"`, or `"large"`, the size of the red rectangle in the following image is a proportion of the available space, 20%, 50%, and 60% for `width` and 20%, 50%, and 66% for `height`:</span></span>

![任务模块示例](~/assets/images/task-module/task-module-example.png)

<span data-ttu-id="a9365-186">从选项卡调用的任务模块可以动态调整大小。</span><span class="sxs-lookup"><span data-stu-id="a9365-186">Task modules invoked from a tab can be dynamically resized.</span></span> <span data-ttu-id="a9365-187">调用后 `tasks.startTask()` ，可以调用 newSize 对象的高度和宽度属性符合 `tasks.updateTask(newSize)` TaskInfo 规范，例如 `{ height: 'medium', width: 'medium' }` 。</span><span class="sxs-lookup"><span data-stu-id="a9365-187">After calling `tasks.startTask()` you can call `tasks.updateTask(newSize)` where height and width properties on the newSize object conform to the TaskInfo specification, for example `{ height: 'medium', width: 'medium' }`.</span></span>

<span data-ttu-id="a9365-188">下一节提供了在 YouTube 视频和 PowerApp 中嵌入任务模块的示例。</span><span class="sxs-lookup"><span data-stu-id="a9365-188">The next section provides examples of embedding task modules in a YouTube video and a PowerApp.</span></span>

## <a name="task-module-css-for-html-or-javascript-task-modules"></a><span data-ttu-id="a9365-189">HTML 或 JavaScript 任务模块的任务模块 CSS</span><span class="sxs-lookup"><span data-stu-id="a9365-189">Task module CSS for HTML or JavaScript task modules</span></span>

<span data-ttu-id="a9365-190">基于 HTML 或 JavaScript 的任务模块可以访问标题下方的整个任务模块区域。</span><span class="sxs-lookup"><span data-stu-id="a9365-190">HTML or JavaScript-based task modules have access to the entire area of the task module below the header.</span></span> <span data-ttu-id="a9365-191">虽然这提供了极大的灵活性，但如果您希望边缘的填充与页眉元素对齐并避免不必要的滚动条，则用户必须提供正确的 CSS。</span><span class="sxs-lookup"><span data-stu-id="a9365-191">While that offers a great deal of flexibility, if you want padding around the edges to align with the header elements and avoid unnecessary scroll bars, the user must provide the right CSS.</span></span> <span data-ttu-id="a9365-192">以下各节提供了一些用例示例。</span><span class="sxs-lookup"><span data-stu-id="a9365-192">The next sections provide some examples for a few use cases.</span></span>

<span data-ttu-id="a9365-193">**示例 1：YouTube 视频**</span><span class="sxs-lookup"><span data-stu-id="a9365-193">**Example 1: YouTube video**</span></span>

<span data-ttu-id="a9365-194">YouTube 提供在网页上嵌入视频的能力。</span><span class="sxs-lookup"><span data-stu-id="a9365-194">YouTube offers the ability to embed videos on web pages.</span></span> <span data-ttu-id="a9365-195">使用简单的存根网页在任务模块中的网页上嵌入视频很简单。</span><span class="sxs-lookup"><span data-stu-id="a9365-195">It is easy to embed videos on web pages in a task module using a simple stub web page.</span></span>

![YouTube 视频](~/assets/images/task-module/youtube-example.png)

<span data-ttu-id="a9365-197">以下代码提供了没有 CSS 的网页的 HTML 示例：</span><span class="sxs-lookup"><span data-stu-id="a9365-197">The following code provides an example of the HTML for the web page without the CSS:</span></span>

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

<span data-ttu-id="a9365-198">以下代码提供了 CSS 的示例：</span><span class="sxs-lookup"><span data-stu-id="a9365-198">The following code provides an example of the CSS:</span></span>

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

<span data-ttu-id="a9365-199">**示例 2：PowerApp**</span><span class="sxs-lookup"><span data-stu-id="a9365-199">**Example 2: PowerApp**</span></span>

<span data-ttu-id="a9365-200">用户也可以使用相同的方法嵌入 PowerApp。</span><span class="sxs-lookup"><span data-stu-id="a9365-200">The user can use the same approach to embed a PowerApp as well.</span></span> <span data-ttu-id="a9365-201">由于任何单个 PowerApp 的高度或宽度都是可自定义的，因此用户可以调整高度和宽度以实现所需的演示文稿。</span><span class="sxs-lookup"><span data-stu-id="a9365-201">As the height or width of any individual PowerApp is customizable, the user can adjust the height and width to achieve the desired presentation.</span></span>

![资产管理 PowerApp](~/assets/images/task-module/powerapp-example.png)

<span data-ttu-id="a9365-203">以下代码提供了 PowerApp 的 HTML 示例：</span><span class="sxs-lookup"><span data-stu-id="a9365-203">The following code provides an example of the HTML for PowerApp:</span></span>

```html
<iframe width="720" height="520" src="https://web.powerapps.com/webplayer/iframeapp?source=iframe&screenColor=rgba(104,101,171,1)&appId=/providers/Microsoft.PowerApps/apps/xxxxxxxx-xxxx-xxxx-xxxx-xxxxxxxxxxxx"></iframe>
```

<span data-ttu-id="a9365-204">以下代码提供了 CSS 的示例：</span><span class="sxs-lookup"><span data-stu-id="a9365-204">The following code provides an example of the CSS:</span></span>

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

<span data-ttu-id="a9365-205">下一节提供有关使用自适应卡片或自适应卡片自动程序卡附件调用卡片的详细信息。</span><span class="sxs-lookup"><span data-stu-id="a9365-205">The next section provides details on invoking your card using Adaptive Card or Adaptive Card bot card attachment.</span></span>

## <a name="adaptive-card-or-adaptive-card-bot-card-attachment"></a><span data-ttu-id="a9365-206">自适应卡片或自适应卡片自动程序卡附件</span><span class="sxs-lookup"><span data-stu-id="a9365-206">Adaptive Card or Adaptive Card bot card attachment</span></span>

<span data-ttu-id="a9365-207">根据调用你的 方式，你必须使用自适应卡片或自适应卡片自动程序卡附件，它是一个封装在附件对象中的自适应 `card` 卡片。</span><span class="sxs-lookup"><span data-stu-id="a9365-207">Depending on how you are invoking your `card`, you must use either an Adaptive Card or an Adaptive Card bot card attachment, which is an Adaptive Card wrapped in an attachment object.</span></span>

<span data-ttu-id="a9365-208">当你从选项卡调用时，用户必须使用自适应卡片。</span><span class="sxs-lookup"><span data-stu-id="a9365-208">When you are invoking from a tab, the user must use an Adaptive Card.</span></span>

<span data-ttu-id="a9365-209">以下代码提供自适应卡片的示例：</span><span class="sxs-lookup"><span data-stu-id="a9365-209">The following code provides an example of an Adaptive Card:</span></span>

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

<span data-ttu-id="a9365-210">以下代码提供了从自动程序调用时自适应卡片自动程序卡附件的示例：</span><span class="sxs-lookup"><span data-stu-id="a9365-210">The following code provides an example of an Adaptive Card bot card attachment when you are invoking from a bot:</span></span>

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

<span data-ttu-id="a9365-211">下一节提供有关任务模块深层链接语法的详细信息，包括 `TaskInfo` 对象 和 `APP_ID` `BOT_APP_ID` 。</span><span class="sxs-lookup"><span data-stu-id="a9365-211">The next section provides details on task module deep link syntax including the `TaskInfo` object and `APP_ID` and `BOT_APP_ID`.</span></span>

## <a name="task-module-deep-link-syntax"></a><span data-ttu-id="a9365-212">任务模块深度链接语法</span><span class="sxs-lookup"><span data-stu-id="a9365-212">Task module deep link syntax</span></span>

<span data-ttu-id="a9365-213">任务模块深层链接是具有以下两个其他详细信息（可选）的 TaskInfo 对象的 `APP_ID` 序列化 `BOT_APP_ID` ：</span><span class="sxs-lookup"><span data-stu-id="a9365-213">A task module deep link is a serialization of the TaskInfo object with the following two other details, `APP_ID` and optionally the `BOT_APP_ID`:</span></span>

`https://teams.microsoft.com/l/task/APP_ID?url=<TaskInfo.url>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

`https://teams.microsoft.com/l/task/APP_ID?card=<TaskInfo.card>&height=<TaskInfo.height>&width=<TaskInfo.width>&title=<TaskInfo.title>&completionBotId=BOT_APP_ID`

<span data-ttu-id="a9365-214">有关 、 和 的数据类型和允许的值 `<TaskInfo.url>` `<TaskInfo.card>` `<TaskInfo.height>` `<TaskInfo.width>` `<TaskInfo.title>` ，请参阅 [TaskInfo 对象](#the-taskinfo-object)。</span><span class="sxs-lookup"><span data-stu-id="a9365-214">For the data types and allowable values for `<TaskInfo.url>`, `<TaskInfo.card>`, `<TaskInfo.height>`, `<TaskInfo.width>`, and `<TaskInfo.title>`, see [TaskInfo object](#the-taskinfo-object).</span></span>

> [!TIP]
> <span data-ttu-id="a9365-215">URL 在使用 参数时对深度链接进行 `card` 编码，例如 JavaScript[ `encodeURI()` ](https://www.w3schools.com/jsref/jsref_encodeURI.asp)的函数 。</span><span class="sxs-lookup"><span data-stu-id="a9365-215">URL encode the deep link when using the `card` parameter, for example, JavaScript's [`encodeURI()` function](https://www.w3schools.com/jsref/jsref_encodeURI.asp).</span></span>

<span data-ttu-id="a9365-216">下表提供了有关 和 `APP_ID` 的信息 `BOT_APP_ID` ：</span><span class="sxs-lookup"><span data-stu-id="a9365-216">The following table provides information on `APP_ID` and `BOT_APP_ID`:</span></span>

| <span data-ttu-id="a9365-217">值</span><span class="sxs-lookup"><span data-stu-id="a9365-217">Value</span></span> | <span data-ttu-id="a9365-218">类型</span><span class="sxs-lookup"><span data-stu-id="a9365-218">Type</span></span> | <span data-ttu-id="a9365-219">必需</span><span class="sxs-lookup"><span data-stu-id="a9365-219">Required</span></span> | <span data-ttu-id="a9365-220">说明</span><span class="sxs-lookup"><span data-stu-id="a9365-220">Description</span></span> |
| --- | --- | --- | --- |
| `APP_ID` | <span data-ttu-id="a9365-221">string</span><span class="sxs-lookup"><span data-stu-id="a9365-221">string</span></span> | <span data-ttu-id="a9365-222">是</span><span class="sxs-lookup"><span data-stu-id="a9365-222">Yes</span></span> | <span data-ttu-id="a9365-223">调用任务模块的应用的[ID。](~/resources/schema/manifest-schema.md#id)</span><span class="sxs-lookup"><span data-stu-id="a9365-223">The [ID](~/resources/schema/manifest-schema.md#id) of the app invoking the task module.</span></span> <span data-ttu-id="a9365-224">的 [清单中的 validDomains](~/resources/schema/manifest-schema.md#validdomains) `APP_ID` 数组必须包含 `url` 的域的 if 位于 URL `url` 中。</span><span class="sxs-lookup"><span data-stu-id="a9365-224">The [validDomains array](~/resources/schema/manifest-schema.md#validdomains) in the manifest for `APP_ID` must contain the domain for `url` if `url` is in the URL.</span></span> <span data-ttu-id="a9365-225">从选项卡或自动程序调用任务模块时，应用 ID 已已知，这就是它未包含在 中的原因 `TaskInfo` 。</span><span class="sxs-lookup"><span data-stu-id="a9365-225">The app ID is already known when a task module is invoked from a tab or a bot, which is why it is not included in `TaskInfo`.</span></span> |
| `BOT_APP_ID` | <span data-ttu-id="a9365-226">string</span><span class="sxs-lookup"><span data-stu-id="a9365-226">string</span></span> | <span data-ttu-id="a9365-227">否</span><span class="sxs-lookup"><span data-stu-id="a9365-227">No</span></span> | <span data-ttu-id="a9365-228">如果指定了 `completionBotId` 的值，则使用消息将对象 `result` `task/submit invoke` 发送到指定的自动程序。</span><span class="sxs-lookup"><span data-stu-id="a9365-228">If a value for `completionBotId` is specified, the `result` object is sent using a `task/submit invoke` message to the specified bot.</span></span> <span data-ttu-id="a9365-229">`BOT_APP_ID` 必须在应用清单中指定为自动程序，即不能将其发送到任何自动程序。</span><span class="sxs-lookup"><span data-stu-id="a9365-229">`BOT_APP_ID` must be specified as a bot in the app's manifest, that is you cannot send it to any bot.</span></span> |

> [!NOTE]
> <span data-ttu-id="a9365-230">`APP_ID` 如果应用有建议自动程序用作应用 ID（如果存在的话）。在许多情况下，和 可能 `BOT_APP_ID` 相同。</span><span class="sxs-lookup"><span data-stu-id="a9365-230">`APP_ID` and `BOT_APP_ID` can be the same in many cases, if an app has a recommended bot to use as an app's ID if there is one.</span></span>

<span data-ttu-id="a9365-231">下一节提供有关将键盘与应用的任务模块一同使用的详细信息。</span><span class="sxs-lookup"><span data-stu-id="a9365-231">The next section provides details on using a keyboard with your app's task module.</span></span>

## <a name="keyboard-and-accessibility-guidelines"></a><span data-ttu-id="a9365-232">键盘和辅助功能指南</span><span class="sxs-lookup"><span data-stu-id="a9365-232">Keyboard and accessibility guidelines</span></span>

<span data-ttu-id="a9365-233">对于基于 HTML 或 JavaScript 的任务模块，必须确保应用的任务模块可以与键盘一同使用。</span><span class="sxs-lookup"><span data-stu-id="a9365-233">With HTML or JavaScript-based task modules, you must ensure your app's task module can be used with a keyboard.</span></span> <span data-ttu-id="a9365-234">屏幕阅读器程序还取决于使用键盘进行导航的能力。</span><span class="sxs-lookup"><span data-stu-id="a9365-234">Screen reader programs also depend on the ability to navigate using the keyboard.</span></span> <span data-ttu-id="a9365-235">这包括以下两项：</span><span class="sxs-lookup"><span data-stu-id="a9365-235">This includes the following two things:</span></span>

* <span data-ttu-id="a9365-236">使用 [HTML 标记中的 tabindex](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) 属性控制可以聚焦的元素。</span><span class="sxs-lookup"><span data-stu-id="a9365-236">Using the [tabindex attribute](https://developer.mozilla.org/en-US/docs/Web/HTML/Global_attributes/tabindex) in your HTML tags to control which elements can be focused.</span></span> <span data-ttu-id="a9365-237">另外，使用 tabindex 属性确定它通常使用 <kbd>Tab</kbd> 键和 <kbd>Shift-Tab</kbd> 键参与顺序键盘导航的地方。</span><span class="sxs-lookup"><span data-stu-id="a9365-237">Also, use tabindex attribute to identify where it participates in sequential keyboard navigation usually with the <kbd>Tab</kbd> and <kbd>Shift-Tab</kbd> keys.</span></span>
* <span data-ttu-id="a9365-238">在 <kbd>JavaScript</kbd> 中为任务模块处理 Esc 键。</span><span class="sxs-lookup"><span data-stu-id="a9365-238">Handling the <kbd>Esc</kbd> key in the JavaScript for your task module.</span></span> <span data-ttu-id="a9365-239">以下代码提供了如何处理 <kbd>Esc</kbd> 键的示例：</span><span class="sxs-lookup"><span data-stu-id="a9365-239">The following code provides an example of how to handle the <kbd>Esc</kbd> key:</span></span>

    ```javascript
    // Handle the Esc key
    document.onkeyup = function(event) {
    if ((event.key === 27) || (event.key === "Escape")) {
      microsoftTeams.submitTask(null); // this will return an err object to the completionHandler()
      }
    }
    ```

<span data-ttu-id="a9365-240">Microsoft Teams确保键盘导航从任务模块标头正常进入 HTML，反之亦然。</span><span class="sxs-lookup"><span data-stu-id="a9365-240">Microsoft Teams ensures that keyboard navigation works properly from the task module header into your HTML and vice-versa.</span></span>

## <a name="code-sample"></a><span data-ttu-id="a9365-241">代码示例</span><span class="sxs-lookup"><span data-stu-id="a9365-241">Code sample</span></span>

|<span data-ttu-id="a9365-242">示例名称</span><span class="sxs-lookup"><span data-stu-id="a9365-242">Sample name</span></span> | <span data-ttu-id="a9365-243">说明</span><span class="sxs-lookup"><span data-stu-id="a9365-243">Description</span></span> | <span data-ttu-id="a9365-244">.NET</span><span class="sxs-lookup"><span data-stu-id="a9365-244">.NET</span></span> | <span data-ttu-id="a9365-245">Node.js</span><span class="sxs-lookup"><span data-stu-id="a9365-245">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="a9365-246">任务模块示例 bots-V4</span><span class="sxs-lookup"><span data-stu-id="a9365-246">Task module sample bots-V4</span></span> | <span data-ttu-id="a9365-247">用于创建任务模块的示例。</span><span class="sxs-lookup"><span data-stu-id="a9365-247">Samples for creating task modules.</span></span> |[<span data-ttu-id="a9365-248">View</span><span class="sxs-lookup"><span data-stu-id="a9365-248">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[<span data-ttu-id="a9365-249">View</span><span class="sxs-lookup"><span data-stu-id="a9365-249">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|
|<span data-ttu-id="a9365-250">任务模块示例选项卡和 bots-V3</span><span class="sxs-lookup"><span data-stu-id="a9365-250">Task module sample tabs and bots-V3</span></span> | <span data-ttu-id="a9365-251">用于创建任务模块的示例。</span><span class="sxs-lookup"><span data-stu-id="a9365-251">Samples for creating task modules.</span></span> |[<span data-ttu-id="a9365-252">View</span><span class="sxs-lookup"><span data-stu-id="a9365-252">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/csharp)|[<span data-ttu-id="a9365-253">View</span><span class="sxs-lookup"><span data-stu-id="a9365-253">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/app-task-module/nodejs)| 

## <a name="see-also"></a><span data-ttu-id="a9365-254">另请参阅</span><span class="sxs-lookup"><span data-stu-id="a9365-254">See also</span></span>

* [<span data-ttu-id="a9365-255">请求设备权限</span><span class="sxs-lookup"><span data-stu-id="a9365-255">Request device permissions</span></span>](~/concepts/device-capabilities/native-device-permissions.md)
* [<span data-ttu-id="a9365-256">集成媒体功能</span><span class="sxs-lookup"><span data-stu-id="a9365-256">Integrate media capabilities</span></span>](~/concepts/device-capabilities/mobile-camera-image-permissions.md)
* [<span data-ttu-id="a9365-257">将 QR 或条形码扫描仪功能集成到 Teams</span><span class="sxs-lookup"><span data-stu-id="a9365-257">Integrate QR or barcode scanner capability in Teams</span></span>](~/concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [<span data-ttu-id="a9365-258">在 Teams 中集成位置Teams</span><span class="sxs-lookup"><span data-stu-id="a9365-258">Integrate location capabilities in Teams</span></span>](~/concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a><span data-ttu-id="a9365-259">后续步骤</span><span class="sxs-lookup"><span data-stu-id="a9365-259">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="a9365-260">在选项卡中使用任务模块</span><span class="sxs-lookup"><span data-stu-id="a9365-260">Use task modules in tabs</span></span>](~/task-modules-and-cards/task-modules/task-modules-tabs.md)