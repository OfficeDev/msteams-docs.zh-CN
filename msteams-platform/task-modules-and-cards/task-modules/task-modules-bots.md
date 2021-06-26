---
title: 使用自动程序Microsoft Teams模块
description: 如何将任务模块与自动程序Microsoft Teams，包括 Bot Framework 卡、自适应卡片和深层链接。
localization_priority: Normal
ms.topic: how-to
keywords: 任务模块团队机器人
ms.openlocfilehash: 5d9aa2b651a4c99cee75aada62a4d1176a589d79
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140305"
---
# <a name="use-task-modules-from-bots"></a><span data-ttu-id="ef23a-104">使用自动程序中的任务模块</span><span class="sxs-lookup"><span data-stu-id="ef23a-104">Use task modules from bots</span></span>

<span data-ttu-id="ef23a-105">可以使用自适应卡片和自动程序框架Microsoft Teams、缩略图和自动程序连接器上的按钮从自动程序调用任务Office 365模块。</span><span class="sxs-lookup"><span data-stu-id="ef23a-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive Cards and Bot Framework cards that is hero, thumbnail, and Office 365 Connector.</span></span> <span data-ttu-id="ef23a-106">任务模块通常是比多个对话步骤更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="ef23a-106">Task modules are often a better user experience than multiple conversation steps.</span></span> <span data-ttu-id="ef23a-107">跟踪自动程序状态并允许用户中断或取消序列。</span><span class="sxs-lookup"><span data-stu-id="ef23a-107">Keep track of bot state and allow the user to interrupt or cancel the sequence.</span></span>

<span data-ttu-id="ef23a-108">有两种调用任务模块的方法：</span><span class="sxs-lookup"><span data-stu-id="ef23a-108">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="ef23a-109">一种新的调用消息：使用 Bot Framework 卡片的卡片操作或自适应卡片的卡片操作，以及 任务模块的 URL 或自适应卡片，从自动程序动态获取 `task/fetch` `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` 。</span><span class="sxs-lookup"><span data-stu-id="ef23a-109">A new kind of invoke message `task/fetch`: Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, task module either a URL or an Adaptive Card, is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="ef23a-110">深层链接 URL：使用任务[](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax)模块的深层链接语法，可以分别使用 Bot Framework 卡片的卡片操作或自适应卡片的卡片 `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)操作。</span><span class="sxs-lookup"><span data-stu-id="ef23a-110">Deep link URLs: Using the [deep link syntax for task modules](~/task-modules-and-cards/task-modules/invoking-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive Cards, respectively.</span></span> <span data-ttu-id="ef23a-111">使用深层链接 URL，任务模块 URL 或自适应卡片正文已知以避免相对于 的服务器往返 `task/fetch` 。</span><span class="sxs-lookup"><span data-stu-id="ef23a-111">With deep link URLs, the task module URL or Adaptive Card body is already known to avoid a server round-trip relative to `task/fetch`.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="ef23a-112">每个 `url` 和 `fallbackUrl` 都必须实现 HTTPS 加密协议。</span><span class="sxs-lookup"><span data-stu-id="ef23a-112">Each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

<span data-ttu-id="ef23a-113">下一节提供有关使用 调用任务模块的详细信息 `task/fetch` 。</span><span class="sxs-lookup"><span data-stu-id="ef23a-113">The next section provides details on invoking a task module using `task/fetch`.</span></span>

## <a name="invoke-a-task-module-using-taskfetch"></a><span data-ttu-id="ef23a-114">使用任务/提取调用任务模块</span><span class="sxs-lookup"><span data-stu-id="ef23a-114">Invoke a task module using task/fetch</span></span>

<span data-ttu-id="ef23a-115">当卡片的对象操作或初始化时，以及当用户选择该按钮时，会向自动 `value` `invoke` `Action.Submit` `invoke` 程序发送一条消息。</span><span class="sxs-lookup"><span data-stu-id="ef23a-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized and when a user selects the button, an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="ef23a-116">在消息的 HTTP 响应中，包装对象中嵌入了一个 `invoke` [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) Teams该对象用于显示任务模块。</span><span class="sxs-lookup"><span data-stu-id="ef23a-116">In the HTTP response to the `invoke` message, there is a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![任务/提取请求或响应](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="ef23a-118">以下步骤使用 task/fetch 提供调用任务模块：</span><span class="sxs-lookup"><span data-stu-id="ef23a-118">The following steps provides the invoke task module using task/fetch:</span></span>

1. <span data-ttu-id="ef23a-119">此图显示了具有购买卡片操作的 Bot  Framework `invoke` [hero 卡](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke)。</span><span class="sxs-lookup"><span data-stu-id="ef23a-119">This image shows a Bot Framework hero card with a **Buy** `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#action-type-invoke).</span></span> <span data-ttu-id="ef23a-120">属性的值 `type` 为 `task/fetch` ，对象的其余部分 `value` 可以是你的选择。</span><span class="sxs-lookup"><span data-stu-id="ef23a-120">The value of the `type` property is `task/fetch` and the rest of the `value` object can be of your choice.</span></span>
1. <span data-ttu-id="ef23a-121">机器人接收 HTTP `invoke` POST 消息。</span><span class="sxs-lookup"><span data-stu-id="ef23a-121">The bot receives the `invoke` HTTP POST message.</span></span>
1. <span data-ttu-id="ef23a-122">机器人创建响应对象，并返回 HTTP 200 响应代码的 POST 响应正文。</span><span class="sxs-lookup"><span data-stu-id="ef23a-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="ef23a-123">有关响应的架构详细信息，请参阅有关 [task/submit 的讨论](#the-flexibility-of-tasksubmit)。</span><span class="sxs-lookup"><span data-stu-id="ef23a-123">For more information on schema for responses, see [the discussion on task/submit](#the-flexibility-of-tasksubmit).</span></span> <span data-ttu-id="ef23a-124">以下代码提供了 HTTP 响应的正文示例，该响应包含嵌入包装对象中的 [TaskInfo](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) 对象：</span><span class="sxs-lookup"><span data-stu-id="ef23a-124">The following code provides an example of body of the HTTP response that contains a [TaskInfo object](~/task-modules-and-cards/task-modules/invoking-task-modules.md#the-taskinfo-object) embedded in a wrapper object:</span></span>

    ```json
    {
      "task": {
        "type": "continue",
        "value": {
          "title": "Task module title",
          "height": 500,
          "width": "medium",
          "url": "https://contoso.com/msteams/taskmodules/newcustomer",
          "fallbackUrl": "https://contoso.com/msteams/taskmodules/newcustomer"
        }
      }
    }
    ```

    <span data-ttu-id="ef23a-125">`task/fetch`事件及其对机器人的响应类似于客户端 SDK 中的 `microsoftTeams.tasks.startTask()` 函数。</span><span class="sxs-lookup"><span data-stu-id="ef23a-125">The `task/fetch` event and its response for bots is similar to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>

1. <span data-ttu-id="ef23a-126">Microsoft Teams任务模块。</span><span class="sxs-lookup"><span data-stu-id="ef23a-126">Microsoft Teams displays the task module.</span></span>

<span data-ttu-id="ef23a-127">下一节提供有关提交任务模块结果的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ef23a-127">The next section provides details on submitting the result of a task module.</span></span>

## <a name="submit-the-result-of-a-task-module"></a><span data-ttu-id="ef23a-128">提交任务模块的结果</span><span class="sxs-lookup"><span data-stu-id="ef23a-128">Submit the result of a task module</span></span>

<span data-ttu-id="ef23a-129">当用户完成任务模块后，将结果提交回自动程序与使用选项卡的方式类似。</span><span class="sxs-lookup"><span data-stu-id="ef23a-129">When the user is finished with the task module, submitting the result back to the bot is similar to the way it works with tabs.</span></span> <span data-ttu-id="ef23a-130">有关详细信息，请参阅 [提交任务模块的结果的示例](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module)。</span><span class="sxs-lookup"><span data-stu-id="ef23a-130">For more information, see [example of submitting the result of a task module](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-of-submitting-the-result-of-a-task-module).</span></span> <span data-ttu-id="ef23a-131">存在以下一些区别：</span><span class="sxs-lookup"><span data-stu-id="ef23a-131">There are a few differences as follows:</span></span>

* <span data-ttu-id="ef23a-132">HTML 或 JavaScript，即 ：在验证用户输入内容后，出于可读性目的，调用以下引用的 `TaskInfo.url` `microsoftTeams.tasks.submitTask()` SDK `submitTask()` 函数。</span><span class="sxs-lookup"><span data-stu-id="ef23a-132">HTML or JavaScript that is `TaskInfo.url`: Once you have validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function referred to hereafter as `submitTask()` for readability purposes.</span></span> <span data-ttu-id="ef23a-133">如果希望关闭任务模块Teams调用不带任何参数，但必须将对象或字符串传递给 `submitTask()` `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="ef23a-133">You can call `submitTask()` without any parameters if you want Teams to close the task module, but you must pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="ef23a-134">将它作为第一个参数传递 `result` 。</span><span class="sxs-lookup"><span data-stu-id="ef23a-134">Pass it as the first parameter, `result`.</span></span> <span data-ttu-id="ef23a-135">Teams调用 `submitHandler` 、 、 `err` 和 `null` `result` 是传递给 的对象或字符串 `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="ef23a-135">Teams invokes `submitHandler`, `err` is `null`, and `result` is the object or string you passed to `submitTask()`.</span></span> <span data-ttu-id="ef23a-136">如果使用 参数 `submitTask()` 调用 `result` ，则必须传递 或 `appId` 字符串 `appId` 数组。</span><span class="sxs-lookup"><span data-stu-id="ef23a-136">If you call `submitTask()` with a `result` parameter, you must pass an `appId` or an array of `appId` strings.</span></span> <span data-ttu-id="ef23a-137">这Teams验证发送结果的应用是否与调用任务模块的应用相同。</span><span class="sxs-lookup"><span data-stu-id="ef23a-137">This allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="ef23a-138">自动程序会收到一 `task/submit` 条消息，其中包括 `result` 。</span><span class="sxs-lookup"><span data-stu-id="ef23a-138">Your bot receives a `task/submit` message including `result`.</span></span> <span data-ttu-id="ef23a-139">有关详细信息，请参阅 [和 `task/fetch` 邮件 `task/submit` 的有效负载](#payload-of-taskfetch-and-tasksubmit-messages)。</span><span class="sxs-lookup"><span data-stu-id="ef23a-139">For more information, see [payload of `task/fetch` and `task/submit` messages](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="ef23a-140">自适应卡片，即 ：当用户选择任何按钮时，用户填充的自适应卡片正文通过消息 `TaskInfo.card` `task/submit` 发送给 `Action.Submit` 机器人。</span><span class="sxs-lookup"><span data-stu-id="ef23a-140">Adaptive Card that is `TaskInfo.card`: The Adaptive Card body as filled in by the user is sent to the bot through a `task/submit` message when the user selects any `Action.Submit` button.</span></span>

<span data-ttu-id="ef23a-141">下一节提供有关 灵活性的详细信息 `task/submit` 。</span><span class="sxs-lookup"><span data-stu-id="ef23a-141">The next section provides details on the flexibility of `task/submit`.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="ef23a-142">任务/提交的灵活性</span><span class="sxs-lookup"><span data-stu-id="ef23a-142">The flexibility of task/submit</span></span>

<span data-ttu-id="ef23a-143">当用户完成从自动程序调用的任务模块时，机器人始终会收到 `task/submit invoke` 一条消息。</span><span class="sxs-lookup"><span data-stu-id="ef23a-143">When the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="ef23a-144">回复邮件时有几种选项 `task/submit` ，如下所示：</span><span class="sxs-lookup"><span data-stu-id="ef23a-144">You have several options when responding to the `task/submit` message as follows:</span></span>

| <span data-ttu-id="ef23a-145">HTTP 正文响应</span><span class="sxs-lookup"><span data-stu-id="ef23a-145">HTTP body response</span></span>                      | <span data-ttu-id="ef23a-146">应用场景</span><span class="sxs-lookup"><span data-stu-id="ef23a-146">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="ef23a-147">None 将忽略 `task/submit` 该消息</span><span class="sxs-lookup"><span data-stu-id="ef23a-147">None ignore the `task/submit` message</span></span> | <span data-ttu-id="ef23a-148">最简单的响应是没有任何响应。</span><span class="sxs-lookup"><span data-stu-id="ef23a-148">The simplest response is no response at all.</span></span> <span data-ttu-id="ef23a-149">用户完成任务模块后，自动程序无需响应。</span><span class="sxs-lookup"><span data-stu-id="ef23a-149">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="ef23a-150">Teams在弹出 `value` 消息框中显示 的值。</span><span class="sxs-lookup"><span data-stu-id="ef23a-150">Teams displays the value of `value` in a pop-up message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="ef23a-151">允许你在向导或多步骤体验中将自适应卡片序列链接在一起。</span><span class="sxs-lookup"><span data-stu-id="ef23a-151">Allows you to chain sequences of Adaptive Cards together in a wizard or multi-step experience.</span></span> |

> [!NOTE]
> <span data-ttu-id="ef23a-152">将自适应卡片链接至序列是一种高级方案。</span><span class="sxs-lookup"><span data-stu-id="ef23a-152">Chaining Adaptive Cards into a sequence is an advanced scenario.</span></span> <span data-ttu-id="ef23a-153">示例Node.js支持它。</span><span class="sxs-lookup"><span data-stu-id="ef23a-153">The Node.js sample app supports it.</span></span> <span data-ttu-id="ef23a-154">有关详细信息，请参阅任务[Microsoft Teams模块Node.js。 ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)</span><span class="sxs-lookup"><span data-stu-id="ef23a-154">For more information, see [Microsoft Teams task module Node.js](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes).</span></span>

<span data-ttu-id="ef23a-155">下一节提供有关 和 邮件的有效 `task/fetch` 负载 `task/submit` 的详细信息。</span><span class="sxs-lookup"><span data-stu-id="ef23a-155">The next section provides details on payload of `task/fetch` and `task/submit` messages.</span></span>

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="ef23a-156">任务/提取和任务/提交消息的有效负载</span><span class="sxs-lookup"><span data-stu-id="ef23a-156">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="ef23a-157">本部分定义机器人接收或 Bot Framework 对象时接收的内容 `task/fetch` `task/submit` `Activity` 的架构。</span><span class="sxs-lookup"><span data-stu-id="ef23a-157">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="ef23a-158">下表提供了 和 消息的有效负载 `task/fetch` `task/submit` 的属性：</span><span class="sxs-lookup"><span data-stu-id="ef23a-158">The following table provides the properties of payload of `task/fetch` and `task/submit` messages:</span></span>

| <span data-ttu-id="ef23a-159">属性</span><span class="sxs-lookup"><span data-stu-id="ef23a-159">Property</span></span> | <span data-ttu-id="ef23a-160">说明</span><span class="sxs-lookup"><span data-stu-id="ef23a-160">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="ef23a-161">始终 `invoke` 为 。</span><span class="sxs-lookup"><span data-stu-id="ef23a-161">Is always `invoke`.</span></span>           |
| `name`   | <span data-ttu-id="ef23a-162">是 `task/fetch` 或 `task/submit` 。</span><span class="sxs-lookup"><span data-stu-id="ef23a-162">Is either `task/fetch` or `task/submit`.</span></span> |
| `value`  | <span data-ttu-id="ef23a-163">是开发人员定义的有效负载。</span><span class="sxs-lookup"><span data-stu-id="ef23a-163">Is the developer-defined payload.</span></span> <span data-ttu-id="ef23a-164">对象的结构与从对象 `value` 发送Teams。</span><span class="sxs-lookup"><span data-stu-id="ef23a-164">The structure of the `value` object is the same as what is sent from Teams.</span></span> <span data-ttu-id="ef23a-165">但在这种情况下，情况有所不同。</span><span class="sxs-lookup"><span data-stu-id="ef23a-165">In this case, however, it is different.</span></span> <span data-ttu-id="ef23a-166">它需要对来自自动程序框架的动态提取（即 和 `task/fetch` `value` 自适应卡片操作） `Action.Submit` 的支持，即 `data` 。</span><span class="sxs-lookup"><span data-stu-id="ef23a-166">It requires support for dynamic fetch that is `task/fetch` from both Bot Framework, which is `value` and Adaptive Card `Action.Submit` actions, which is `data`.</span></span> <span data-ttu-id="ef23a-167">除了 或 中Teams外，需要一种与自动程序 `context` 通信 `value` 的方法 `data` 。</span><span class="sxs-lookup"><span data-stu-id="ef23a-167">A way to communicate Teams `context` to the bot is required in addition to what is included in `value` or `data`.</span></span><br/><br/><span data-ttu-id="ef23a-168">将"value"和"data"合并到父对象中：</span><span class="sxs-lookup"><span data-stu-id="ef23a-168">Combine 'value' and 'data' into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

<span data-ttu-id="ef23a-169">下一节提供了一个在邮件中接收、响应 `task/fetch` `task/submit` 和调用Node.js。</span><span class="sxs-lookup"><span data-stu-id="ef23a-169">The next section provides an example of receiving and responding to `task/fetch` and `task/submit` invoke messages in Node.js.</span></span>

## <a name="example-of-taskfetch-and-tasksubmit-invoke-messages-in-nodejs-and-c"></a><span data-ttu-id="ef23a-170">任务/提取和任务/提交调用消息的示例Node.js和 C#</span><span class="sxs-lookup"><span data-stu-id="ef23a-170">Example of task/fetch and task/submit invoke messages in Node.js and C#</span></span>

# <a name="nodejs"></a>[<span data-ttu-id="ef23a-171">Node.js</span><span class="sxs-lookup"><span data-stu-id="ef23a-171">Node.js</span></span>](#tab/nodejs)

```typescript
handleTeamsTaskModuleFetch(context, taskModuleRequest) {
    // Called when the user selects an options from the displayed HeroCard or
    // AdaptiveCard.  The result is the action to perform.

    const cardTaskFetchValue = taskModuleRequest.data.data;
    var taskInfo = {}; // TaskModuleTaskInfo

    if (cardTaskFetchValue === TaskModuleIds.YouTube) {
        // Display the YouTube.html page
        taskInfo.url = taskInfo.fallbackUrl = this.baseUrl + '/' + TaskModuleIds.YouTube + '.html';
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
    } else if (cardTaskFetchValue === TaskModuleIds.CustomForm) {
        // Display the CustomForm.html page, and post the form data back via
        // handleTeamsTaskModuleSubmit.
        taskInfo.url = taskInfo.fallbackUrl = this.baseUrl + '/' + TaskModuleIds.CustomForm + '.html';
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
    } else if (cardTaskFetchValue === TaskModuleIds.AdaptiveCard) {
        // Display an AdaptiveCard to prompt user for text, and post it back via
        // handleTeamsTaskModuleSubmit.
        taskInfo.card = this.createAdaptiveCardAttachment();
        this.setTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
    }

    return TaskModuleResponseFactory.toTaskModuleResponse(taskInfo);
}

async handleTeamsTaskModuleSubmit(context, taskModuleRequest) {
    // Called when data is being returned from the selected option (see `handleTeamsTaskModuleFetch').

    // Echo the users input back.  In a production bot, this is where you'd add behavior in
    // response to the input.
    await context.sendActivity(MessageFactory.text('handleTeamsTaskModuleSubmit: ' + JSON.stringify(taskModuleRequest.data)));

    // Return TaskModuleResponse
    return {
        // TaskModuleMessageResponse
        task: {
            type: 'message',
            value: 'Thanks!'
        }
    };
}

setTaskInfo(taskInfo, uiSettings) {
    taskInfo.height = uiSettings.height;
    taskInfo.width = uiSettings.width;
    taskInfo.title = uiSettings.title;
}
```

# <a name="c"></a>[<span data-ttu-id="ef23a-172">C#</span><span class="sxs-lookup"><span data-stu-id="ef23a-172">C#</span></span>](#tab/csharp)

```csharp
protected override Task<TaskModuleResponse> OnTeamsTaskModuleFetchAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
{
    var asJobject = JObject.FromObject(taskModuleRequest.Data);
    var value = asJobject.ToObject<CardTaskFetchValue<string>>()?.Data;

    var taskInfo = new TaskModuleTaskInfo();
    switch (value)
    {
        case TaskModuleIds.YouTube:
            taskInfo.Url = taskInfo.FallbackUrl = _baseUrl + "/" + TaskModuleIds.YouTube;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
            break;
        case TaskModuleIds.CustomForm:
            taskInfo.Url = taskInfo.FallbackUrl = _baseUrl + "/" + TaskModuleIds.CustomForm;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
            break;
        case TaskModuleIds.AdaptiveCard:
            taskInfo.Card = CreateAdaptiveCardAttachment();
            SetTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
            break;
        default:
            break;
    }

    return Task.FromResult(taskInfo.ToTaskModuleResponse());
}

protected override async Task<TaskModuleResponse> OnTeamsTaskModuleSubmitAsync(ITurnContext<IInvokeActivity> turnContext, TaskModuleRequest taskModuleRequest, CancellationToken cancellationToken)
{
    var reply = MessageFactory.Text("OnTeamsTaskModuleSubmitAsync Value: " + JsonConvert.SerializeObject(taskModuleRequest));
    await turnContext.SendActivityAsync(reply, cancellationToken);

    return TaskModuleResponseFactory.CreateResponse("Thanks!");
}

private static void SetTaskInfo(TaskModuleTaskInfo taskInfo, UISettings uIConstants)
{
    taskInfo.Height = uIConstants.Height;
    taskInfo.Width = uIConstants.Width;
    taskInfo.Title = uIConstants.Title.ToString();
}
```

---

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="ef23a-173">自动程序框架卡片操作与自适应卡片操作。提交操作</span><span class="sxs-lookup"><span data-stu-id="ef23a-173">Bot Framework card actions vs. Adaptive Card Action.Submit actions</span></span>

<span data-ttu-id="ef23a-174">Bot Framework 卡片操作架构不同于自适应卡片操作，调用任务模块的方式 `Action.Submit` 也不同。</span><span class="sxs-lookup"><span data-stu-id="ef23a-174">The schema for Bot Framework card actions is different from Adaptive Card `Action.Submit` actions and the way to invoke task modules is also different.</span></span> <span data-ttu-id="ef23a-175">`data`中的 `Action.Submit` 对象包含 `msteams` 对象，因此不会干扰卡片中其他属性。</span><span class="sxs-lookup"><span data-stu-id="ef23a-175">The `data` object in `Action.Submit` contains an `msteams` object so it does not interfere with other properties in the card.</span></span> <span data-ttu-id="ef23a-176">下表显示了每个卡片操作的示例：</span><span class="sxs-lookup"><span data-stu-id="ef23a-176">The following table shows an example of each card action:</span></span>

| <span data-ttu-id="ef23a-177">Bot Framework 卡操作</span><span class="sxs-lookup"><span data-stu-id="ef23a-177">Bot Framework card action</span></span>                              | <span data-ttu-id="ef23a-178">自适应卡片操作.Submit 操作</span><span class="sxs-lookup"><span data-stu-id="ef23a-178">Adaptive Card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |

## <a name="code-sample"></a><span data-ttu-id="ef23a-179">代码示例</span><span class="sxs-lookup"><span data-stu-id="ef23a-179">Code sample</span></span>

|<span data-ttu-id="ef23a-180">示例名称</span><span class="sxs-lookup"><span data-stu-id="ef23a-180">Sample name</span></span> | <span data-ttu-id="ef23a-181">说明</span><span class="sxs-lookup"><span data-stu-id="ef23a-181">Description</span></span> | <span data-ttu-id="ef23a-182">.NET</span><span class="sxs-lookup"><span data-stu-id="ef23a-182">.NET</span></span> | <span data-ttu-id="ef23a-183">Node.js</span><span class="sxs-lookup"><span data-stu-id="ef23a-183">Node.js</span></span>|
|----------------|-----------------|--------------|----------------|
|<span data-ttu-id="ef23a-184">任务模块示例 bots-V4</span><span class="sxs-lookup"><span data-stu-id="ef23a-184">Task module sample bots-V4</span></span> | <span data-ttu-id="ef23a-185">用于创建任务模块的示例。</span><span class="sxs-lookup"><span data-stu-id="ef23a-185">Samples for creating task modules.</span></span> |[<span data-ttu-id="ef23a-186">View</span><span class="sxs-lookup"><span data-stu-id="ef23a-186">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/csharp_dotnetcore/54.teams-task-module)|[<span data-ttu-id="ef23a-187">View</span><span class="sxs-lookup"><span data-stu-id="ef23a-187">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/main/samples/javascript_nodejs/54.teams-task-module)|

## <a name="see-also"></a><span data-ttu-id="ef23a-188">另请参阅</span><span class="sxs-lookup"><span data-stu-id="ef23a-188">See also</span></span>

* [<span data-ttu-id="ef23a-189">Microsoft Teams任务模块示例代码Node.js</span><span class="sxs-lookup"><span data-stu-id="ef23a-189">Microsoft Teams task module sample code in Node.js</span></span>](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)
* [<span data-ttu-id="ef23a-190">Bot Framework 示例</span><span class="sxs-lookup"><span data-stu-id="ef23a-190">Bot Framework samples</span></span>](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)
