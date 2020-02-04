---
title: 在 Microsoft 团队 bot 中使用任务模块
description: 如何在 Microsoft 团队 bot 中使用任务模块，包括机器人框架卡、自适应卡片和深层链接。
keywords: 任务模块团队 bot
ms.openlocfilehash: 3a0e4591dbb26ff4afa8cc06edc0a03365da0eca
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673196"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="0c10b-104">使用 Microsoft 团队 bot 中的任务模块</span><span class="sxs-lookup"><span data-stu-id="0c10b-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="0c10b-105">可以使用自适应卡片和机器人框架卡（英雄、缩略图和 Office 365 连接器）上的按钮从 Microsoft 工作组 bot 调用任务模块。</span><span class="sxs-lookup"><span data-stu-id="0c10b-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="0c10b-106">作为开发人员必须跟踪 bot 状态并允许用户中断/取消序列的多个对话步骤相比，任务模块通常是更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="0c10b-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="0c10b-107">有两种方法可以调用任务模块：</span><span class="sxs-lookup"><span data-stu-id="0c10b-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="0c10b-108">**一种新的调用消息`task/fetch`。**</span><span class="sxs-lookup"><span data-stu-id="0c10b-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="0c10b-109">使用 bot `invoke`框架卡的[卡操作](~/task-modules-and-cards/cards/cards-actions.md#invoke)或`Action.Submit`自适应卡片`task/fetch`的[卡操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)，任务模块（URL 或自适应卡片）是从你的 Bot 动态获取的。</span><span class="sxs-lookup"><span data-stu-id="0c10b-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="0c10b-110">**深层链接 Url。**</span><span class="sxs-lookup"><span data-stu-id="0c10b-110">**Deep link URLs.**</span></span> <span data-ttu-id="0c10b-111">通过使用[任务模块的深层链接语法](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)，可以分别对 Bot `openUrl`框架卡或`Action.OpenUrl` [卡片操作](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)使用 "[智能卡" 操作](~/task-modules-and-cards/cards/cards-actions.md#openurl)。</span><span class="sxs-lookup"><span data-stu-id="0c10b-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="0c10b-112">使用深层链接 Url 时，任务模块 URL 或自适应卡片正文会提前知道，从而避免相对于服务器的往返行程`task/fetch`。</span><span class="sxs-lookup"><span data-stu-id="0c10b-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

## <a name="invoking-a-task-module-via-taskfetch"></a><span data-ttu-id="0c10b-113">通过任务/提取调用任务模块</span><span class="sxs-lookup"><span data-stu-id="0c10b-113">Invoking a task module via task/fetch</span></span>

<span data-ttu-id="0c10b-114">当`value` `invoke`卡片操作的对象或`Action.Submit`以正确的方式进行初始化时（下面将详细介绍），当用户按下按钮时，会将`invoke`邮件发送到 bot。</span><span class="sxs-lookup"><span data-stu-id="0c10b-114">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="0c10b-115">在对`invoke`邮件的 HTTP 响应中，有一个嵌入在包装对象中的[TaskInfo 对象](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)，团队使用该对象来显示任务模块。</span><span class="sxs-lookup"><span data-stu-id="0c10b-115">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![任务/回迁请求/响应](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="0c10b-117">让我们更详细地了解一下每个步骤：</span><span class="sxs-lookup"><span data-stu-id="0c10b-117">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="0c10b-118">本示例显示了带有 "购买" `invoke` [卡片操作](~/task-modules-and-cards/cards/cards-actions.md#invoke)的 Bot 框架英雄卡片。</span><span class="sxs-lookup"><span data-stu-id="0c10b-118">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="0c10b-119">`type`属性的值为`task/fetch` - `value`对象的其余部分可以是您喜欢的任何内容。</span><span class="sxs-lookup"><span data-stu-id="0c10b-119">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
2. <span data-ttu-id="0c10b-120">机器人将接收`invoke` HTTP POST 消息。</span><span class="sxs-lookup"><span data-stu-id="0c10b-120">The bot receives the `invoke` HTTP POST message.</span></span>
3. <span data-ttu-id="0c10b-121">Bot 将创建响应对象，并使用 HTTP 200 响应代码在 POST 响应的正文中返回该对象。</span><span class="sxs-lookup"><span data-stu-id="0c10b-121">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="0c10b-122">有关响应的架构[在有关任务/提交的讨论中](#the-flexibility-of-tasksubmit)进行了说明，但现在要记住的重要一点是，HTTP 响应的正文包含嵌入在包装对象中的[TaskInfo 对象](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object)，例如：</span><span class="sxs-lookup"><span data-stu-id="0c10b-122">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, e.g.:</span></span>

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
    
    <span data-ttu-id="0c10b-123">Bot `task/fetch`的事件及其响应在概念上类似于客户端 SDK 中`microsoftTeams.tasks.startTask()`的功能。</span><span class="sxs-lookup"><span data-stu-id="0c10b-123">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
4. <span data-ttu-id="0c10b-124">Microsoft 团队显示任务模块。</span><span class="sxs-lookup"><span data-stu-id="0c10b-124">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="0c10b-125">提交任务模块的结果</span><span class="sxs-lookup"><span data-stu-id="0c10b-125">Submitting the result of a task module</span></span>

<span data-ttu-id="0c10b-126">当用户使用任务模块完成后，将结果提交回 bot 与[使用选项卡的方式](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)类似，但存在一些不同之处，因此也会在此处进行说明。</span><span class="sxs-lookup"><span data-stu-id="0c10b-126">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="0c10b-127">**HTML/JavaScript （`TaskInfo.url`）**。</span><span class="sxs-lookup"><span data-stu-id="0c10b-127">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="0c10b-128">验证用户输入的内容后，调用`microsoftTeams.tasks.submitTask()` SDK 函数（在以后`submitTask()`出于可读性目的而引用）。</span><span class="sxs-lookup"><span data-stu-id="0c10b-128">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="0c10b-129">如果只想`submitTask()`要团队关闭任务模块，则可以不带任何参数调用，但大多数时候需要将一个对象或字符串传递给您`submitHandler`的。</span><span class="sxs-lookup"><span data-stu-id="0c10b-129">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="0c10b-130">只需将其作为第一个参数`result`传递即可。</span><span class="sxs-lookup"><span data-stu-id="0c10b-130">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="0c10b-131">团队将调用`submitHandler`： `err`将为`null` ， `result`并将成为您传递给的对象/ `submitTask()`字符串。</span><span class="sxs-lookup"><span data-stu-id="0c10b-131">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="0c10b-132">如果`result`使用参数进行`submitTask()`调用，则**必须**传递一个`appId`或多个`appId`字符串数组：这允许团队验证发送结果的应用程序是否与调用任务模块的应用程序相同。</span><span class="sxs-lookup"><span data-stu-id="0c10b-132">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="0c10b-133">你的 bot 将收到`task/submit`一条`result`消息，其中[包括如下所](#payload-of-taskfetch-and-tasksubmit-messages)述的消息。</span><span class="sxs-lookup"><span data-stu-id="0c10b-133">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="0c10b-134">**自适应卡片`TaskInfo.card`（）**。</span><span class="sxs-lookup"><span data-stu-id="0c10b-134">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="0c10b-135">自适应卡片正文（由用户填写）将在用户按下任意`task/submit` `Action.Submit`按钮时通过消息发送到机器人。</span><span class="sxs-lookup"><span data-stu-id="0c10b-135">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="0c10b-136">任务/提交的灵活性</span><span class="sxs-lookup"><span data-stu-id="0c10b-136">The flexibility of task/submit</span></span>

<span data-ttu-id="0c10b-137">在上一节中，您了解到当用户完成从 bot 中调用的任务模块后，bot 将始终收到一`task/submit invoke`条消息。</span><span class="sxs-lookup"><span data-stu-id="0c10b-137">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="0c10b-138">作为开发人员，您可以在*响应* `task/submit`邮件时使用以下几个选项：</span><span class="sxs-lookup"><span data-stu-id="0c10b-138">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="0c10b-139">HTTP 正文响应</span><span class="sxs-lookup"><span data-stu-id="0c10b-139">HTTP Body Response</span></span>                      | <span data-ttu-id="0c10b-140">方案</span><span class="sxs-lookup"><span data-stu-id="0c10b-140">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="0c10b-141">无（忽略该`task/submit`消息）</span><span class="sxs-lookup"><span data-stu-id="0c10b-141">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="0c10b-142">最简单的响应是无响应。</span><span class="sxs-lookup"><span data-stu-id="0c10b-142">The simplest response is no response at all.</span></span> <span data-ttu-id="0c10b-143">当用户使用任务模块完成时，你的 bot 不需要进行响应。</span><span class="sxs-lookup"><span data-stu-id="0c10b-143">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="0c10b-144">团队将`value`在弹出消息框中显示值。</span><span class="sxs-lookup"><span data-stu-id="0c10b-144">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="0c10b-145">允许您在向导/多步骤体验中将自适应卡片的序列 "链" 在一起。</span><span class="sxs-lookup"><span data-stu-id="0c10b-145">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="0c10b-146">_请注意，将自适应卡片链接到一个序列是一个高级方案，此处未对其进行介绍。然而，node.js 示例应用支持它，但它的工作方式在[其 README.md 文件](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)中进行了记录。_</span><span class="sxs-lookup"><span data-stu-id="0c10b-146">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="0c10b-147">任务/提取和任务/提交邮件的有效负载</span><span class="sxs-lookup"><span data-stu-id="0c10b-147">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="0c10b-148">此部分定义了你的 bot 在接收`task/fetch`或`task/submit` bot 框架`Activity`对象时接收的内容的架构。</span><span class="sxs-lookup"><span data-stu-id="0c10b-148">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="0c10b-149">下面显示了重要的顶级：</span><span class="sxs-lookup"><span data-stu-id="0c10b-149">The important top-level appear below:</span></span>

| <span data-ttu-id="0c10b-150">属性</span><span class="sxs-lookup"><span data-stu-id="0c10b-150">Property</span></span> | <span data-ttu-id="0c10b-151">说明</span><span class="sxs-lookup"><span data-stu-id="0c10b-151">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="0c10b-152">将始终为`invoke`</span><span class="sxs-lookup"><span data-stu-id="0c10b-152">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="0c10b-153">`task/fetch`或者`task/submit`</span><span class="sxs-lookup"><span data-stu-id="0c10b-153">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="0c10b-154">开发人员定义的有效负载。</span><span class="sxs-lookup"><span data-stu-id="0c10b-154">The developer-defined payload.</span></span> <span data-ttu-id="0c10b-155">通常， `value`对象的结构会反映从团队发送的内容。</span><span class="sxs-lookup"><span data-stu-id="0c10b-155">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="0c10b-156">但是，在这种情况下，由于我们要支持来自 Bot 框架（`task/fetch``value`）和自适应卡片`Action.Submit`操作（`data`）的动态提取（），并且除了中`context` `value` / `data`包含的内容之外，我们还需要一种方法来将团队与 bot 进行通信。</span><span class="sxs-lookup"><span data-stu-id="0c10b-156">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="0c10b-157">为此，我们将两者组合成一个父对象：</span><span class="sxs-lookup"><span data-stu-id="0c10b-157">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="0c10b-158">示例：接收和响应任务/提取和任务/提交调用消息-node.js</span><span class="sxs-lookup"><span data-stu-id="0c10b-158">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

<span data-ttu-id="0c10b-159">在 Bot `invoke`框架中处理邮件可能有点麻烦，因为在 BOT 框架 SDK 中不提供对它们的正式支持。</span><span class="sxs-lookup"><span data-stu-id="0c10b-159">Dealing with `invoke` messages in Bot Framework can be a little tricky because there's no formal support for them in the Bot Framework SDK.</span></span> <span data-ttu-id="0c10b-160">为了简化此过程，团队已在`onInvoke()` [botbuilder-团队 npm 包](https://www.npmjs.com/package/botbuilder-teams)中创建了 helper 函数（对于 node.js）。</span><span class="sxs-lookup"><span data-stu-id="0c10b-160">To make it easier, Teams has created `onInvoke()` helper functions in the [botbuilder-teams npm package (for Node.js)](https://www.npmjs.com/package/botbuilder-teams).</span></span> <span data-ttu-id="0c10b-161">下面的示例展示了如何执行此操作：</span><span class="sxs-lookup"><span data-stu-id="0c10b-161">This example below shows how to do it:</span></span>

> [!NOTE]
> <span data-ttu-id="0c10b-162">下面的示例代码在此功能的技术预览和最终版本中进行了修改： `task/fetch`请求的架构已更改，以遵循[上一节中所述](#payload-of-taskfetch-and-tasksubmit-messages)内容。</span><span class="sxs-lookup"><span data-stu-id="0c10b-162">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="0c10b-163">也就是说，文档是正确的，但实现不正确。</span><span class="sxs-lookup"><span data-stu-id="0c10b-163">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="0c10b-164">请参阅`// for Technical Preview [...]`下面的注释以了解所做的更改。</span><span class="sxs-lookup"><span data-stu-id="0c10b-164">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

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

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="0c10b-165">示例：接收和响应任务/提取和任务/提交调用消息-C#</span><span class="sxs-lookup"><span data-stu-id="0c10b-165">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="0c10b-166">在 c # bot `invoke`中，处理`Activity`邮件的`HttpResponseMessage()`控制器会处理邮件。</span><span class="sxs-lookup"><span data-stu-id="0c10b-166">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="0c10b-167">`task/fetch`和`task/submit`请求和响应为 JSON。</span><span class="sxs-lookup"><span data-stu-id="0c10b-167">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="0c10b-168">在 c # 中，像在 node.js 中那样处理原始 JSON 并不是很方便，因此，您需要使用包装类来处理 JSON 和从 JSON 的序列化。</span><span class="sxs-lookup"><span data-stu-id="0c10b-168">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="0c10b-169">在 Microsoft 团队[c # SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams)中，尚无直接支持此功能，但您可以在[c # 示例应用](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)中看到这些简单包装类的外观示例。</span><span class="sxs-lookup"><span data-stu-id="0c10b-169">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="0c10b-170">下面的示例代码是使用这些包装`task/fetch`类`task/submit` （`TaskInfo`， `TaskEnvelope`）的 c # 中的示例代码和消息，[示例](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)中的 excerpted：</span><span class="sxs-lookup"><span data-stu-id="0c10b-170">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

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

<span data-ttu-id="0c10b-171">上面的示例中未显示`SetTaskInfo()`函数，用于设置每种情况`height`下`width` `TaskInfo`对象的`title` 、和属性。</span><span class="sxs-lookup"><span data-stu-id="0c10b-171">Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case.</span></span> <span data-ttu-id="0c10b-172">以下是[SetTaskInfo （）的源代码](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)。</span><span class="sxs-lookup"><span data-stu-id="0c10b-172">Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span></span>

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="0c10b-173">Bot 框架卡片操作与自适应卡片操作。提交操作</span><span class="sxs-lookup"><span data-stu-id="0c10b-173">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="0c10b-174">机器人框架卡片操作的架构与自适应卡片`Action.Submit`操作略有不同。</span><span class="sxs-lookup"><span data-stu-id="0c10b-174">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="0c10b-175">因此，调用任务模块的方法也稍有不同： `data`对象`Action.Submit`包含一个`msteams`对象，因此它不会干扰卡片中的其他属性。</span><span class="sxs-lookup"><span data-stu-id="0c10b-175">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="0c10b-176">下表显示了每个示例：</span><span class="sxs-lookup"><span data-stu-id="0c10b-176">The following table shows an example of each:</span></span>

| <span data-ttu-id="0c10b-177">机器人框架卡操作</span><span class="sxs-lookup"><span data-stu-id="0c10b-177">Bot Framework card action</span></span>                              | <span data-ttu-id="0c10b-178">自适应卡片操作。提交操作</span><span class="sxs-lookup"><span data-stu-id="0c10b-178">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
