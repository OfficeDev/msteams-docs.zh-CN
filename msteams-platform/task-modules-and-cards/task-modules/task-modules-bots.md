---
title: 在 Microsoft 团队 bot 中使用任务模块
description: 如何在 Microsoft 团队 bot 中使用任务模块，包括机器人框架卡、自适应卡片和深层链接。
keywords: 任务模块团队 bot
ms.openlocfilehash: 32fb6a4aa0a8bf2297a4f60331dc5c6c6aceb4e2
ms.sourcegitcommit: 214eccbadb7f3a67236b79a041ef487b7bf6dfbd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/07/2020
ms.locfileid: "44801137"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="52e57-104">使用 Microsoft 团队 bot 中的任务模块</span><span class="sxs-lookup"><span data-stu-id="52e57-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="52e57-105">可以使用自适应卡片和机器人框架卡（英雄、缩略图和 Office 365 连接器）上的按钮从 Microsoft 工作组 bot 调用任务模块。</span><span class="sxs-lookup"><span data-stu-id="52e57-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="52e57-106">作为开发人员必须跟踪 bot 状态并允许用户中断/取消序列的多个对话步骤相比，任务模块通常是更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="52e57-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="52e57-107">有两种方法可以调用任务模块：</span><span class="sxs-lookup"><span data-stu-id="52e57-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="52e57-108">**一种新的调用消息 `task/fetch` 。**</span><span class="sxs-lookup"><span data-stu-id="52e57-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="52e57-109">使用 `invoke` Bot 框架卡的[卡操作](~/task-modules-and-cards/cards/cards-actions.md#invoke)或 `Action.Submit` 自适应卡片的[卡操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)， `task/fetch` 任务模块（URL 或自适应卡片）是从你的 Bot 动态获取的。</span><span class="sxs-lookup"><span data-stu-id="52e57-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="52e57-110">**深层链接 Url。**</span><span class="sxs-lookup"><span data-stu-id="52e57-110">**Deep link URLs.**</span></span> <span data-ttu-id="52e57-111">通过使用[任务模块的深层链接语法](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)，可以 `openUrl` 分别对 Bot 框架卡或卡片操作使用 "[智能卡" 操作](~/task-modules-and-cards/cards/cards-actions.md#openurl) `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) 。</span><span class="sxs-lookup"><span data-stu-id="52e57-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="52e57-112">使用深层链接 Url 时，任务模块 URL 或自适应卡片正文会提前知道，从而避免相对于服务器的往返行程 `task/fetch` 。</span><span class="sxs-lookup"><span data-stu-id="52e57-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

>[!IMPORTANT]
><span data-ttu-id="52e57-113">为确保安全通信，每个 `url` 和 `fallbackUrl` 必须实现 HTTPS 加密协议。</span><span class="sxs-lookup"><span data-stu-id="52e57-113">To ensure secure communications, each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

## <a name="invoking-a-task-module-via-taskfetch"></a><span data-ttu-id="52e57-114">通过任务/提取调用任务模块</span><span class="sxs-lookup"><span data-stu-id="52e57-114">Invoking a task module via task/fetch</span></span>

<span data-ttu-id="52e57-115">当 `value` 卡片操作的对象 `invoke` 或 `Action.Submit` 以正确的方式进行初始化时（下面将详细介绍），当用户按下按钮时，会将 `invoke` 邮件发送到 bot。</span><span class="sxs-lookup"><span data-stu-id="52e57-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="52e57-116">在对邮件的 HTTP 响应中 `invoke` ，有一个嵌入在包装对象中的[TaskInfo 对象](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)，团队使用该对象来显示任务模块。</span><span class="sxs-lookup"><span data-stu-id="52e57-116">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![任务/回迁请求/响应](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="52e57-118">让我们更详细地了解一下每个步骤：</span><span class="sxs-lookup"><span data-stu-id="52e57-118">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="52e57-119">本示例显示了带有 "购买" `invoke` [卡片操作](~/task-modules-and-cards/cards/cards-actions.md#invoke)的 Bot 框架英雄卡片。</span><span class="sxs-lookup"><span data-stu-id="52e57-119">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="52e57-120">属性的值 `type` 为 `task/fetch` -对象的其余部分 `value` 可以是您喜欢的任何内容。</span><span class="sxs-lookup"><span data-stu-id="52e57-120">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
2. <span data-ttu-id="52e57-121">机器人将接收 `invoke` HTTP POST 消息。</span><span class="sxs-lookup"><span data-stu-id="52e57-121">The bot receives the `invoke` HTTP POST message.</span></span>
3. <span data-ttu-id="52e57-122">Bot 将创建响应对象，并使用 HTTP 200 响应代码在 POST 响应的正文中返回该对象。</span><span class="sxs-lookup"><span data-stu-id="52e57-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="52e57-123">有关响应的架构[在有关任务/提交的讨论中](#the-flexibility-of-tasksubmit)进行了说明，但现在要记住的重要一点是，HTTP 响应的正文包含嵌入在包装对象中的[TaskInfo 对象](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)，例如：</span><span class="sxs-lookup"><span data-stu-id="52e57-123">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, e.g.:</span></span>

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

    <span data-ttu-id="52e57-124">`task/fetch`Bot 的事件及其响应在概念上类似于 `microsoftTeams.tasks.startTask()` 客户端 SDK 中的功能。</span><span class="sxs-lookup"><span data-stu-id="52e57-124">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
4. <span data-ttu-id="52e57-125">Microsoft 团队显示任务模块。</span><span class="sxs-lookup"><span data-stu-id="52e57-125">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="52e57-126">提交任务模块的结果</span><span class="sxs-lookup"><span data-stu-id="52e57-126">Submitting the result of a task module</span></span>

<span data-ttu-id="52e57-127">当用户使用任务模块完成后，将结果提交回 bot 与[使用选项卡的方式](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)类似，但存在一些不同之处，因此也会在此处进行说明。</span><span class="sxs-lookup"><span data-stu-id="52e57-127">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="52e57-128">**HTML/JavaScript （ `TaskInfo.url` ）**。</span><span class="sxs-lookup"><span data-stu-id="52e57-128">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="52e57-129">验证用户输入的内容后，调用 `microsoftTeams.tasks.submitTask()` SDK 函数（在以后 `submitTask()` 出于可读性目的而引用）。</span><span class="sxs-lookup"><span data-stu-id="52e57-129">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="52e57-130">`submitTask()`如果只想要团队关闭任务模块，则可以不带任何参数调用，但大多数时候需要将一个对象或字符串传递给您的 `submitHandler` 。</span><span class="sxs-lookup"><span data-stu-id="52e57-130">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="52e57-131">只需将其作为第一个参数传递即可 `result` 。</span><span class="sxs-lookup"><span data-stu-id="52e57-131">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="52e57-132">团队将调用 `submitHandler` ： `err` 将为 `null` ，并 `result` 将成为您传递给的对象/字符串 `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="52e57-132">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="52e57-133">如果 `submitTask()` 使用参数进行调用 `result` ，则**必须**传递一个或多 `appId` 个 `appId` 字符串数组：这允许团队验证发送结果的应用程序是否与调用任务模块的应用程序相同。</span><span class="sxs-lookup"><span data-stu-id="52e57-133">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="52e57-134">你的 bot 将收到一 `task/submit` 条消息，其中包括如下 `result` 所述的消息。 [below](#payload-of-taskfetch-and-tasksubmit-messages)</span><span class="sxs-lookup"><span data-stu-id="52e57-134">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="52e57-135">**自适应卡片（ `TaskInfo.card` ）**。</span><span class="sxs-lookup"><span data-stu-id="52e57-135">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="52e57-136">自适应卡片正文（由用户填写）将在 `task/submit` 用户按下任意按钮时通过消息发送到机器人 `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="52e57-136">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="52e57-137">任务/提交的灵活性</span><span class="sxs-lookup"><span data-stu-id="52e57-137">The flexibility of task/submit</span></span>

<span data-ttu-id="52e57-138">在上一节中，您了解到当用户完成从 bot 中调用的任务模块后，bot 将始终收到一 `task/submit invoke` 条消息。</span><span class="sxs-lookup"><span data-stu-id="52e57-138">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="52e57-139">作为开发人员，您可以在*响应*邮件时使用以下几个选项 `task/submit` ：</span><span class="sxs-lookup"><span data-stu-id="52e57-139">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="52e57-140">HTTP 正文响应</span><span class="sxs-lookup"><span data-stu-id="52e57-140">HTTP Body Response</span></span>                      | <span data-ttu-id="52e57-141">应用场景</span><span class="sxs-lookup"><span data-stu-id="52e57-141">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="52e57-142">无（忽略该 `task/submit` 消息）</span><span class="sxs-lookup"><span data-stu-id="52e57-142">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="52e57-143">最简单的响应是无响应。</span><span class="sxs-lookup"><span data-stu-id="52e57-143">The simplest response is no response at all.</span></span> <span data-ttu-id="52e57-144">当用户使用任务模块完成时，你的 bot 不需要进行响应。</span><span class="sxs-lookup"><span data-stu-id="52e57-144">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="52e57-145">团队将 `value` 在弹出消息框中显示值。</span><span class="sxs-lookup"><span data-stu-id="52e57-145">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="52e57-146">允许您在向导/多步骤体验中将自适应卡片的序列 "链" 在一起。</span><span class="sxs-lookup"><span data-stu-id="52e57-146">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="52e57-147">_请注意，将自适应卡片链接到一个序列是一个高级方案，此处未对其进行介绍。但是，Node.js 示例应用程序支持它，并且它的工作方式在[其 README.md 文件](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)中进行了记录。_</span><span class="sxs-lookup"><span data-stu-id="52e57-147">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="52e57-148">任务/提取和任务/提交邮件的有效负载</span><span class="sxs-lookup"><span data-stu-id="52e57-148">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="52e57-149">此部分定义了你的 bot 在接收 `task/fetch` 或 `task/submit` bot 框架对象时接收的内容的架构 `Activity` 。</span><span class="sxs-lookup"><span data-stu-id="52e57-149">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="52e57-150">下面显示了重要的顶级：</span><span class="sxs-lookup"><span data-stu-id="52e57-150">The important top-level appear below:</span></span>

| <span data-ttu-id="52e57-151">属性</span><span class="sxs-lookup"><span data-stu-id="52e57-151">Property</span></span> | <span data-ttu-id="52e57-152">说明</span><span class="sxs-lookup"><span data-stu-id="52e57-152">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="52e57-153">将始终为`invoke`</span><span class="sxs-lookup"><span data-stu-id="52e57-153">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="52e57-154">`task/fetch`或者`task/submit`</span><span class="sxs-lookup"><span data-stu-id="52e57-154">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="52e57-155">开发人员定义的有效负载。</span><span class="sxs-lookup"><span data-stu-id="52e57-155">The developer-defined payload.</span></span> <span data-ttu-id="52e57-156">通常，对象的结构会 `value` 反映从团队发送的内容。</span><span class="sxs-lookup"><span data-stu-id="52e57-156">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="52e57-157">但是，在这种情况下，由于我们要支持 `task/fetch` 来自 Bot 框架（ `value` ）和自适应卡片操作（）的动态提取（） `Action.Submit` `data` ，并且 `context` 除了中包含的内容之外，我们还需要一种方法来将团队与 bot 进行通信 `value` / `data` 。</span><span class="sxs-lookup"><span data-stu-id="52e57-157">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="52e57-158">为此，我们将两者组合成一个父对象：</span><span class="sxs-lookup"><span data-stu-id="52e57-158">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="52e57-159">示例：接收和响应任务/提取和任务/提交调用邮件-Node.js</span><span class="sxs-lookup"><span data-stu-id="52e57-159">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

> [!NOTE]
> <span data-ttu-id="52e57-160">下面的示例代码在此功能的技术预览和最终版本中进行了修改：请求的架构 `task/fetch` 已更改，以遵循[上一节中所述](#payload-of-taskfetch-and-tasksubmit-messages)内容。</span><span class="sxs-lookup"><span data-stu-id="52e57-160">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="52e57-161">也就是说，文档是正确的，但实现不正确。</span><span class="sxs-lookup"><span data-stu-id="52e57-161">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="52e57-162">请参阅 `// for Technical Preview [...]` 下面的注释以了解所做的更改。</span><span class="sxs-lookup"><span data-stu-id="52e57-162">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

```typescript
// Handle requests and responses for a "Custom Form" and an "Adaptive card" task module.
// Assumes request is coming from an Adaptive card Action.Submit button that has a "taskModule" property indicating what to invoke
private async onInvoke(event: builder.IEvent, cb: (err: Error, body: any, status?: number) => void): Promise<void> {
    let invokeType = (event as any).name;
    let invokeValue = (event as any).value;
    if (invokeType === undefined) {
        invokeType = null;
    }
    switch (invokeType) {
        case "task/fetch": {
            if (invokeValue !== undefined && invokeValue.data.taskModule === "customform") { // for Technical Preview, was invokeValue.taskModule
                // Return the specified task module response to the bot
                let fetchTemplate: any = {
                    "task": {
                        "type": "continue",
                        "value": {
                            "title": "Custom Form",
                            "height": 510,
                            "width": 430,
                            "fallbackUrl": "https://contoso.com/teamsapp/customform",
                            "url": "https://contoso.com/teamsapp/customform",
                        }
                    }
                };
                cb(null, fetchTemplate, 200);
            };
            if (invokeValue !== undefined && invokeValue.data.taskModule === "adaptivecard") { // for Technical Preview, was invokeValue.taskModule
                let adaptiveCard = {
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
                };
                // Return the specified task module response to the bot
                let fetchTemplate: any = {
                    "task": {
                        "type": "continue",
                        "value": {
                            "title": "Ninja Cat",
                            "height": "small",
                            "width": "small",
                            "card": {
                                contentType: "application/vnd.microsoft.card.adaptive",
                                content: adaptiveCard,
                            }
                        }
                    }
                };
                cb(null, fetchTemplate, 200);
            };
            break;
        }
        case "task/submit": {
            if (invokeValue.data !== undefined) {
                // It's a valid task module response
                let submitResponse: any = {
                    "task": {
                        "type": "message",
                        "value": "Task complete!",
                    }
                };
                cb(null, fetchTemplates.submitMessageResponse, 200)
            }
        }
    }
}
```

<span data-ttu-id="52e57-163">*另*请参阅[Microsoft 团队任务模块示例代码-Nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts)和[Bot 框架示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="52e57-163">*See also*, [Microsoft Teams task module sample code — nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) and  [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="52e57-164">示例：接收和响应任务/提取和任务/提交调用消息-C#</span><span class="sxs-lookup"><span data-stu-id="52e57-164">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="52e57-165">在 c # bot 中， `invoke` 处理邮件的控制器会处理邮件 `HttpResponseMessage()` `Activity` 。</span><span class="sxs-lookup"><span data-stu-id="52e57-165">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="52e57-166">`task/fetch`和 `task/submit` 请求和响应为 JSON。</span><span class="sxs-lookup"><span data-stu-id="52e57-166">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="52e57-167">在 c # 中，不像处理 Node.js 中的原始 JSON 那样方便，因此，您需要使用包装类来处理 JSON 和 JSON 的序列化。</span><span class="sxs-lookup"><span data-stu-id="52e57-167">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="52e57-168">在 Microsoft 团队[c # SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)中，尚无直接支持此功能，但您可以在[c # 示例应用](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)中看到这些简单包装类的外观示例。</span><span class="sxs-lookup"><span data-stu-id="52e57-168">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="52e57-169">下面的示例代码是 `task/fetch` `task/submit` 使用这些包装类（，）的 c # 中的示例代码和消息 `TaskInfo` `TaskEnvelope` ，[示例](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)中的 excerpted：</span><span class="sxs-lookup"><span data-stu-id="52e57-169">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

```csharp
private HttpResponseMessage HandleInvokeMessages(Activity activity)
{
    var activityValue = activity.Value.ToString();
    if (activity.Name == "task/fetch")
    {
        var action = Newtonsoft.Json.JsonConvert.DeserializeObject<Models.BotFrameworkCardValue<string>>(activityValue);

        Models.TaskInfo taskInfo = GetTaskInfo(action.Data);
        Models.TaskEnvelope taskEnvelope = new Models.TaskEnvelope
        {
            Task = new Models.Task()
            {
                Type = Models.TaskType.Continue,
                TaskInfo = taskInfo
            }
        };
        return Request.CreateResponse(HttpStatusCode.OK, taskEnvelope);
    }
    else if (activity.Name == "task/submit")
    {
        ConnectorClient connector = new ConnectorClient(new Uri(activity.ServiceUrl));
        Activity reply = activity.CreateReply("Received = " + activity.Value.ToString());
        connector.Conversations.ReplyToActivity(reply);
    }
    return new HttpResponseMessage(HttpStatusCode.Accepted);
}

// Helper function for building the TaskInfo object based on the incoming request
private static Models.TaskInfo GetTaskInfo(string actionInfo)
{
    Models.TaskInfo taskInfo = new Models.TaskInfo();
    switch (actionInfo)
    {
        case TaskModuleIds.YouTube:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.YouTube;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.YouTube);
            break;
        case TaskModuleIds.PowerApp:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.PowerApp;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.PowerApp);
            break;
        case TaskModuleIds.CustomForm:
            taskInfo.Url = taskInfo.FallbackUrl = ApplicationSettings.BaseUrl + "/" + TaskModuleIds.CustomForm;
            SetTaskInfo(taskInfo, TaskModuleUIConstants.CustomForm);
            break;
        case TaskModuleIds.AdaptiveCard:
            taskInfo.Card = AdaptiveCardHelper.GetAdaptiveCard();
            SetTaskInfo(taskInfo, TaskModuleUIConstants.AdaptiveCard);
            break;
        default:
            break;
    }
    return taskInfo;
}
```

<span data-ttu-id="52e57-170">上面的示例中未显示 `SetTaskInfo()` 函数，用于设置 `height` `width` `title` `TaskInfo` 每种情况下对象的、和属性。</span><span class="sxs-lookup"><span data-stu-id="52e57-170">Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case.</span></span> <span data-ttu-id="52e57-171">以下是[SetTaskInfo （）的源代码](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)。</span><span class="sxs-lookup"><span data-stu-id="52e57-171">Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span></span>

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="52e57-172">Bot 框架卡片操作与自适应卡片操作。提交操作</span><span class="sxs-lookup"><span data-stu-id="52e57-172">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="52e57-173">机器人框架卡片操作的架构与自适应卡片操作略有不同 `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="52e57-173">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="52e57-174">因此，调用任务模块的方法也稍有不同： `data` 对象 `Action.Submit` 包含一个 `msteams` 对象，因此它不会干扰卡片中的其他属性。</span><span class="sxs-lookup"><span data-stu-id="52e57-174">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="52e57-175">下表显示了每个示例：</span><span class="sxs-lookup"><span data-stu-id="52e57-175">The following table shows an example of each:</span></span>

| <span data-ttu-id="52e57-176">机器人框架卡操作</span><span class="sxs-lookup"><span data-stu-id="52e57-176">Bot Framework card action</span></span>                              | <span data-ttu-id="52e57-177">自适应卡片操作。提交操作</span><span class="sxs-lookup"><span data-stu-id="52e57-177">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
