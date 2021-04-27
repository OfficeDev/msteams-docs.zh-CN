---
title: 使用 Microsoft Teams 机器人中的任务模块
description: 如何将任务模块与 Microsoft Teams 自动程序一同使用，包括 Bot Framework 卡、自适应卡片和深层链接
localization_priority: Normal
ms.topic: how-to
keywords: 任务模块团队机器人
ms.openlocfilehash: 948af0c71acb20f4d84fa25ba79618045dad9da7
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020273"
---
# <a name="using-task-modules-from-microsoft-teams-bots"></a><span data-ttu-id="11655-104">使用 Microsoft Teams 机器人中的任务模块</span><span class="sxs-lookup"><span data-stu-id="11655-104">Using task modules from Microsoft Teams bots</span></span>

<span data-ttu-id="11655-105">可以使用自适应卡片和自动程序框架卡上的按钮从 Microsoft Teams 自动程序调用任务模块 (Hero、Thumbnail 和 Office 365 Connector) 。</span><span class="sxs-lookup"><span data-stu-id="11655-105">Task modules can be invoked from Microsoft Teams bots using buttons on Adaptive cards and Bot Framework cards (Hero, Thumbnail, and Office 365 Connector).</span></span> <span data-ttu-id="11655-106">与开发人员必须跟踪机器人状态并允许用户中断/取消序列的多个对话步骤不同，任务模块通常是更好的用户体验。</span><span class="sxs-lookup"><span data-stu-id="11655-106">Task modules are often a better user experience than multiple conversation steps where you as a developer have to keep track of bot state and allow the user to interrupt/cancel the sequence.</span></span>

<span data-ttu-id="11655-107">有两种调用任务模块的方法：</span><span class="sxs-lookup"><span data-stu-id="11655-107">There are two ways of invoking task modules:</span></span>

* <span data-ttu-id="11655-108">**一种新的调用消息 `task/fetch` 。**</span><span class="sxs-lookup"><span data-stu-id="11655-108">**A new kind of invoke message `task/fetch`.**</span></span> <span data-ttu-id="11655-109">使用自动程序框架卡片的卡片操作或自适应卡片的卡片操作和 ，任务模块 (URL 或自适应卡片) 从自动程序动态获取 `invoke` [](~/task-modules-and-cards/cards/cards-actions.md#invoke) `Action.Submit` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) `task/fetch` 。</span><span class="sxs-lookup"><span data-stu-id="11655-109">Using the `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke) for Bot Framework cards, or the `Action.Submit` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, with `task/fetch`, the task module (either a URL or an Adaptive card) is fetched dynamically from your bot.</span></span>
* <span data-ttu-id="11655-110">**深层链接 URL。**</span><span class="sxs-lookup"><span data-stu-id="11655-110">**Deep link URLs.**</span></span> <span data-ttu-id="11655-111">使用[任务模块的](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax)深层链接语法，你可以分别使用 Bot Framework 卡片的卡片操作或自适应卡片 `openUrl` [](~/task-modules-and-cards/cards/cards-actions.md#openurl) `Action.OpenUrl` [](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions)的卡片操作。</span><span class="sxs-lookup"><span data-stu-id="11655-111">Using the [deep link syntax for task modules](~/task-modules-and-cards/what-are-task-modules.md#task-module-deep-link-syntax), you can use the `openUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#openurl) for Bot Framework cards or the `Action.OpenUrl` [card action](~/task-modules-and-cards/cards/cards-actions.md#adaptive-cards-actions) for Adaptive cards, respectively.</span></span> <span data-ttu-id="11655-112">对于深层链接 URL，任务模块 URL 或自适应卡片正文明显提前已知，以避免相对于 的服务器往返 `task/fetch` 行程。</span><span class="sxs-lookup"><span data-stu-id="11655-112">With deep link URLs, the task module URL or Adaptive card body is obviously known in advance, avoiding a server round-trip relative to `task/fetch`.</span></span>

>[!IMPORTANT]
><span data-ttu-id="11655-113">为确保安全通信，每个和 `url` `fallbackUrl` 都必须实现 HTTPS 加密协议。</span><span class="sxs-lookup"><span data-stu-id="11655-113">To ensure secure communications, each `url` and `fallbackUrl` must implement the HTTPS encryption protocol.</span></span>

## <a name="invoking-a-task-module-via-taskfetch"></a><span data-ttu-id="11655-114">通过任务/提取调用任务模块</span><span class="sxs-lookup"><span data-stu-id="11655-114">Invoking a task module via task/fetch</span></span>

<span data-ttu-id="11655-115">当卡片操作的对象或以正确的方式初始化时 () 下面进行了详细说明，当用户按下按钮时，会向自动程序 `value` `invoke` `Action.Submit` `invoke` 发送消息。</span><span class="sxs-lookup"><span data-stu-id="11655-115">When the `value` object of the `invoke` card action or `Action.Submit` is initialized in the proper way (explained in more detail below), when a user presses the button an `invoke` message is sent to the bot.</span></span> <span data-ttu-id="11655-116">在消息的 HTTP 响应中，有一个嵌入包装器对象中的 `invoke` [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) 对象，Teams 使用该对象显示任务模块。</span><span class="sxs-lookup"><span data-stu-id="11655-116">In the HTTP response to the `invoke` message, there's a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, which Teams uses to display the task module.</span></span>

![task/fetch request/response](~/assets/images/task-module/task-module-invoke-request-response.png)

<span data-ttu-id="11655-118">让我们更详细地了解一下每个步骤：</span><span class="sxs-lookup"><span data-stu-id="11655-118">Let's look at each step in a bit more detail:</span></span>

1. <span data-ttu-id="11655-119">本示例显示具有"Buy"卡片操作的 Bot Framework `invoke` [Hero 卡](~/task-modules-and-cards/cards/cards-actions.md#invoke)。</span><span class="sxs-lookup"><span data-stu-id="11655-119">This example shows a Bot Framework Hero card with a "Buy" `invoke` [card action](~/task-modules-and-cards/cards/cards-actions.md#invoke).</span></span> <span data-ttu-id="11655-120">属性的值 `type` 为 `task/fetch` - 对象的其余部分 `value` 可以是您喜欢的任何对象。</span><span class="sxs-lookup"><span data-stu-id="11655-120">The value of the `type` property is `task/fetch` - the rest of the `value` object can be whatever you like.</span></span>
2. <span data-ttu-id="11655-121">机器人接收 HTTP `invoke` POST 消息。</span><span class="sxs-lookup"><span data-stu-id="11655-121">The bot receives the `invoke` HTTP POST message.</span></span>
3. <span data-ttu-id="11655-122">机器人创建响应对象，并返回 HTTP 200 响应代码的 POST 响应正文。</span><span class="sxs-lookup"><span data-stu-id="11655-122">The bot creates a response object and returns it in the body of the POST response with an HTTP 200 response code.</span></span> <span data-ttu-id="11655-123">有关任务 [/](#the-flexibility-of-tasksubmit)提交的讨论如下所述响应的架构，但现在需要记住的重要一点就是 HTTP 响应的正文包含嵌入包装对象中的 [TaskInfo](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) 对象，例如：</span><span class="sxs-lookup"><span data-stu-id="11655-123">The schema for responses is described [below in the discussion on task/submit](#the-flexibility-of-tasksubmit), but the important thing to remember now is that the body of the HTTP response contains a [TaskInfo object](~/task-modules-and-cards/what-are-task-modules.md#the-taskinfo-object) embedded in a wrapper object, e.g.:</span></span>

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

    <span data-ttu-id="11655-124">从概念上说，事件及其对自动程序的响应与客户端 SDK 中的 `task/fetch` `microsoftTeams.tasks.startTask()` 函数类似。</span><span class="sxs-lookup"><span data-stu-id="11655-124">The `task/fetch` event and its response for bots is similar, conceptually, to the `microsoftTeams.tasks.startTask()` function in the client SDK.</span></span>
4. <span data-ttu-id="11655-125">Microsoft Teams 显示任务模块。</span><span class="sxs-lookup"><span data-stu-id="11655-125">Microsoft Teams displays the task module.</span></span>

## <a name="submitting-the-result-of-a-task-module"></a><span data-ttu-id="11655-126">提交任务模块的结果</span><span class="sxs-lookup"><span data-stu-id="11655-126">Submitting the result of a task module</span></span>

<span data-ttu-id="11655-127">当用户使用完任务模块后，将结果提交回自动程序与使用选项卡的方式类似，但[](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module)存在一些差异，因此此处也进行了介绍。</span><span class="sxs-lookup"><span data-stu-id="11655-127">When the user is finished with the task module, submitting the result back to the bot is similar [to the way it works with tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md#example-submitting-the-result-of-a-task-module), but there are a few differences, so it's described here too.</span></span>

* <span data-ttu-id="11655-128">**HTML/JavaScript `TaskInfo.url` ()**。</span><span class="sxs-lookup"><span data-stu-id="11655-128">**HTML/JavaScript (`TaskInfo.url`)**.</span></span> <span data-ttu-id="11655-129">验证用户输入的信息后，可调用 SDK 函数 (以下称为" `microsoftTeams.tasks.submitTask()` `submitTask()` 可读性") 。</span><span class="sxs-lookup"><span data-stu-id="11655-129">Once you've validated what the user has entered, you call the `microsoftTeams.tasks.submitTask()` SDK function (referred to hereafter as `submitTask()` for readability purposes).</span></span> <span data-ttu-id="11655-130">如果你仅希望 Teams 关闭任务模块，但大多数情况下你想要将对象或字符串传递到 你的 ，你可以调用不带任何 `submitTask()` 参数 `submitHandler` 的 。</span><span class="sxs-lookup"><span data-stu-id="11655-130">You can call `submitTask()` without any parameters if you just want Teams to close the task module, but most of the time you'll want to pass an object or a string to your `submitHandler`.</span></span> <span data-ttu-id="11655-131">只需传递它作为第一个参数， `result` 。</span><span class="sxs-lookup"><span data-stu-id="11655-131">Simply pass it as the first parameter, `result`.</span></span> <span data-ttu-id="11655-132">Teams 将 `submitHandler` 调用 `err` ：will `null` 和 will be `result` the object/string you passed to `submitTask()` 。</span><span class="sxs-lookup"><span data-stu-id="11655-132">Teams will invoke `submitHandler`: `err` will be `null` and `result` will be the object/string you passed to `submitTask()`.</span></span> <span data-ttu-id="11655-133">如果使用 参数调用 ，则必须传递 或 字符串数组：这允许 Teams 验证发送结果的应用是否与调用任务模块的应用 `submitTask()` `result`  `appId` `appId` 相同。</span><span class="sxs-lookup"><span data-stu-id="11655-133">If you do call `submitTask()` with a `result` parameter, you **must** pass an `appId` or an array of `appId` strings: this allows Teams to validate that the app sending the result is the same one which invoked the task module.</span></span> <span data-ttu-id="11655-134">自动程序将收到 `task/submit` 一条消息， `result` 如下 [所述](#payload-of-taskfetch-and-tasksubmit-messages)。</span><span class="sxs-lookup"><span data-stu-id="11655-134">Your bot will receive a `task/submit` message including `result` as described [below](#payload-of-taskfetch-and-tasksubmit-messages).</span></span>
* <span data-ttu-id="11655-135">**自适应卡片 `TaskInfo.card` () 。**</span><span class="sxs-lookup"><span data-stu-id="11655-135">**Adaptive card (`TaskInfo.card`)**.</span></span> <span data-ttu-id="11655-136">自适应卡片正文 (用户填充) 当用户按下任何按钮时，会通过一条消息发送给 `task/submit` 自动 `Action.Submit` 程序。</span><span class="sxs-lookup"><span data-stu-id="11655-136">The Adaptive card body (as filled in by the user) will be sent to the bot via a `task/submit` message when the user presses any `Action.Submit` button.</span></span>

## <a name="the-flexibility-of-tasksubmit"></a><span data-ttu-id="11655-137">任务/提交的灵活性</span><span class="sxs-lookup"><span data-stu-id="11655-137">The flexibility of task/submit</span></span>

<span data-ttu-id="11655-138">在上一部分中，你了解了当用户完成从自动程序调用的任务模块时，机器人始终会收到 `task/submit invoke` 一条消息。</span><span class="sxs-lookup"><span data-stu-id="11655-138">In the previous section, you learned that when the user finishes with a task module invoked from a bot, the bot always receives a `task/submit invoke` message.</span></span> <span data-ttu-id="11655-139">作为开发人员，在回复消息 *时，有几个* `task/submit` 选项：</span><span class="sxs-lookup"><span data-stu-id="11655-139">As a developer, you have several options when *responding* to the `task/submit` message:</span></span>

| <span data-ttu-id="11655-140">HTTP 正文响应</span><span class="sxs-lookup"><span data-stu-id="11655-140">HTTP Body Response</span></span>                      | <span data-ttu-id="11655-141">方案</span><span class="sxs-lookup"><span data-stu-id="11655-141">Scenario</span></span>                                |
| --------------------------------------- | --------------------------------------- |
| <span data-ttu-id="11655-142">无 (忽略 `task/submit` 消息) </span><span class="sxs-lookup"><span data-stu-id="11655-142">None (ignore the `task/submit` message)</span></span> | <span data-ttu-id="11655-143">最简单的响应是没有任何响应。</span><span class="sxs-lookup"><span data-stu-id="11655-143">The simplest response is no response at all.</span></span> <span data-ttu-id="11655-144">用户完成任务模块后，自动程序无需响应。</span><span class="sxs-lookup"><span data-stu-id="11655-144">Your bot is not required to respond when the user is finished with the task module.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "message",<br/>    "value": "Message text"<br/>  }<br/>}</pre> | <span data-ttu-id="11655-145">Teams 将在弹出消息 `value` 框中显示 的值。</span><span class="sxs-lookup"><span data-stu-id="11655-145">Teams will display the value of `value` in a popup message box.</span></span> |
| <pre>{<br/>  "task": {<br/>    "type": "continue",<br/>    "value": &lt;TaskInfo object&gt;<br/>  }<br/>}</pre> | <span data-ttu-id="11655-146">允许你在向导/多步骤体验中将自适应卡片序列"链接"在一起。</span><span class="sxs-lookup"><span data-stu-id="11655-146">Allows you to "chain" sequences of Adaptive cards together in a wizard/multi-step experience.</span></span> <span data-ttu-id="11655-147">_请注意，将自适应卡片链接至序列是一个高级方案，未在此处进行介绍。但是Node.js示例应用支持它，并且其工作方式记录在其 README.md [文件中](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)。_</span><span class="sxs-lookup"><span data-stu-id="11655-147">_Note that chaining Adaptive cards into a sequence is an advanced scenario and not documented here. The Node.js sample app supports it, however, and how it works is documented in [its README.md file](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs#implementation-notes)._</span></span> |

## <a name="payload-of-taskfetch-and-tasksubmit-messages"></a><span data-ttu-id="11655-148">任务/提取和任务/提交消息的有效负载</span><span class="sxs-lookup"><span data-stu-id="11655-148">Payload of task/fetch and task/submit messages</span></span>

<span data-ttu-id="11655-149">本部分定义机器人接收或 Bot Framework 对象时接收的内容 `task/fetch` `task/submit` `Activity` 的架构。</span><span class="sxs-lookup"><span data-stu-id="11655-149">This section defines the schema of what your bot receives when it receives a `task/fetch` or `task/submit` Bot Framework `Activity` object.</span></span> <span data-ttu-id="11655-150">重要的顶级如下所示：</span><span class="sxs-lookup"><span data-stu-id="11655-150">The important top-level appear below:</span></span>

| <span data-ttu-id="11655-151">属性</span><span class="sxs-lookup"><span data-stu-id="11655-151">Property</span></span> | <span data-ttu-id="11655-152">说明</span><span class="sxs-lookup"><span data-stu-id="11655-152">Description</span></span>                          |
| -------- | ------------------------------------ |
| `type`   | <span data-ttu-id="11655-153">将始终为 `invoke`</span><span class="sxs-lookup"><span data-stu-id="11655-153">Will always be `invoke`</span></span>              |
| `name`   | <span data-ttu-id="11655-154">或 `task/fetch``task/submit`</span><span class="sxs-lookup"><span data-stu-id="11655-154">Either `task/fetch` or `task/submit`</span></span> |
| `value`  | <span data-ttu-id="11655-155">开发人员定义的有效负载。</span><span class="sxs-lookup"><span data-stu-id="11655-155">The developer-defined payload.</span></span> <span data-ttu-id="11655-156">通常，对象 `value` 的结构反映从 Teams 发送的对象。</span><span class="sxs-lookup"><span data-stu-id="11655-156">Normally the structure of the `value` object mirrors what was sent from Teams.</span></span> <span data-ttu-id="11655-157">但是，在这种情况下，这有所不同，因为我们希望同时支持从 Bot Framework () 和自适应卡片操作 () 获取动态提取 `task/fetch` `value` (`Action.Submit` `data`) ， `context` `value` / `data` 并且我们需要一种方法来将 Teams 与自动程序通信，除了 包含哪些内容。</span><span class="sxs-lookup"><span data-stu-id="11655-157">In this case, however, it's different because we want to support dynamic fetch (`task/fetch`) from both Bot Framework (`value`) and Adaptive card `Action.Submit` actions (`data`), and we need a way to communicate Teams `context` to the bot in addition to what was included in `value`/`data`.</span></span><br/><br/><span data-ttu-id="11655-158">我们通过将两者合并到父对象中来这样做：</span><span class="sxs-lookup"><span data-stu-id="11655-158">We do this by combining the two into a parent object:</span></span><br/><br/><pre>{<br/>  "context": {<br/>    "theme": "default" &vert; "dark" &vert; "contrast",<br/>  },<br/>  "data": [value field from Bot Framework card] &vert; [data field from Adaptive Card] <br/>}</pre>  |

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---nodejs"></a><span data-ttu-id="11655-159">示例：接收和响应任务/提取和任务/提交调用消息 - Node.js</span><span class="sxs-lookup"><span data-stu-id="11655-159">Example: Receiving and responding to task/fetch and task/submit invoke messages - Node.js</span></span>

> [!NOTE]
> <span data-ttu-id="11655-160">下面的示例代码在 Technical Preview 和此功能的最终版本之间进行了修改：请求的架构更改为遵循上一节中 `task/fetch` [记录的内容](#payload-of-taskfetch-and-tasksubmit-messages)。</span><span class="sxs-lookup"><span data-stu-id="11655-160">The sample code below was modified between Technical Preview and final release of this feature: the schema of the `task/fetch` request changed to follow what was [documented in the previous section](#payload-of-taskfetch-and-tasksubmit-messages).</span></span> <span data-ttu-id="11655-161">也就是说，文档正确，但实现不正确。</span><span class="sxs-lookup"><span data-stu-id="11655-161">That is, the documentation was correct but the implementation was not.</span></span> <span data-ttu-id="11655-162">有关 `// for Technical Preview [...]` 更改内容，请参阅下面的注释。</span><span class="sxs-lookup"><span data-stu-id="11655-162">See the `// for Technical Preview [...]` comments below for what changed.</span></span>

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

<span data-ttu-id="11655-163">*另请参阅* Microsoft [Teams 任务模块示例代码 nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) 和  [Bot Framework 示例](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md)。</span><span class="sxs-lookup"><span data-stu-id="11655-163">*See also*, [Microsoft Teams task module sample code — nodejs](https://github.com/OfficeDev/microsoft-teams-sample-task-module-nodejs/blob/master/src/TeamsBot.ts) and  [Bot Framework samples](https://github.com/Microsoft/BotBuilder-Samples/blob/master/README.md).</span></span>

## <a name="example-receiving-and-responding-to-taskfetch-and-tasksubmit-invoke-messages---c"></a><span data-ttu-id="11655-164">示例：接收和响应任务/提取和任务/提交调用消息 - C#</span><span class="sxs-lookup"><span data-stu-id="11655-164">Example: Receiving and responding to task/fetch and task/submit invoke messages - C#</span></span>

<span data-ttu-id="11655-165">在C#中， `invoke` 消息由处理邮件 `HttpResponseMessage()` 的控制器 `Activity` 处理。</span><span class="sxs-lookup"><span data-stu-id="11655-165">In C# bots, `invoke` messages are processed by an `HttpResponseMessage()` controller processing an `Activity` message.</span></span> <span data-ttu-id="11655-166">和 `task/fetch` `task/submit` 请求和响应为 JSON。</span><span class="sxs-lookup"><span data-stu-id="11655-166">The `task/fetch` and `task/submit` requests and responses are JSON.</span></span> <span data-ttu-id="11655-167">在C#中，处理原始 JSON 并不方便，因为它在 Node.js 中，因此你需要包装类来处理与 JSON 之间的序列化。</span><span class="sxs-lookup"><span data-stu-id="11655-167">In C#, it's not as convenient to deal with raw JSON as it is in Node.js, so you need wrapper classes to handle the serialization to and from JSON.</span></span> <span data-ttu-id="11655-168">尚未在 Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) 中直接支持此功能，但你可以查看这些简单包装类在 C# [示例中的外观示例](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs)。</span><span class="sxs-lookup"><span data-stu-id="11655-168">There's no direct support for this in the Microsoft Teams [C# SDK](https://www.nuget.org/packages/Microsoft.Bot.Connector.Teams) yet, but you can see an example of what these simple wrapper classes would look like in the [C# sample app](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Models/TaskModel.cs).</span></span>

<span data-ttu-id="11655-169">下面是用于处理C#和使用这些包装类的邮件的示例代码 `task/fetch` `task/submit` `TaskInfo` ， (、) 示例摘录 `TaskEnvelope` ： [](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)</span><span class="sxs-lookup"><span data-stu-id="11655-169">Below is example code in C# for handling `task/fetch` and `task/submit` messages using these wrapper classes (`TaskInfo`, `TaskEnvelope`), excerpted from the [sample](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs):</span></span>

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

<span data-ttu-id="11655-170">以上示例中未显示 的是 函数，它设置每个大小写的对象的 、 `SetTaskInfo()` `height` 和 `width` `title` `TaskInfo` 属性。</span><span class="sxs-lookup"><span data-stu-id="11655-170">Not shown in the above example is the `SetTaskInfo()` function, which sets the `height`, `width`, and `title` properties of the `TaskInfo` object for each case.</span></span> <span data-ttu-id="11655-171">下面是[SetTaskInfo () 。 ](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs)</span><span class="sxs-lookup"><span data-stu-id="11655-171">Here's the [source code for SetTaskInfo()](https://github.com/OfficeDev/microsoft-teams-sample-task-module-csharp/blob/master/Microsoft.Teams.Samples.TaskModule.Web/Controllers/MessagesController.cs).</span></span>

### <a name="bot-framework-card-actions-vs-adaptive-card-actionsubmit-actions"></a><span data-ttu-id="11655-172">自动程序框架卡片操作与自适应卡片操作。提交操作</span><span class="sxs-lookup"><span data-stu-id="11655-172">Bot Framework card actions vs. Adaptive card Action.Submit actions</span></span>

<span data-ttu-id="11655-173">Bot Framework 卡操作架构与自适应卡片操作略有不同 `Action.Submit` 。</span><span class="sxs-lookup"><span data-stu-id="11655-173">The schema for Bot Framework card actions is slightly different from Adaptive card `Action.Submit` actions.</span></span> <span data-ttu-id="11655-174">因此，调用任务模块的方式也略有不同：中的 对象包含 对象，因此不会干扰卡片中 `data` `Action.Submit` `msteams` 其他属性。</span><span class="sxs-lookup"><span data-stu-id="11655-174">As a result, the way to invoke task modules is slightly different too: the `data` object in `Action.Submit` contains an `msteams` object so it won't interfere with other properties in the card.</span></span> <span data-ttu-id="11655-175">下表显示了每个示例：</span><span class="sxs-lookup"><span data-stu-id="11655-175">The following table shows an example of each:</span></span>

| <span data-ttu-id="11655-176">Bot Framework 卡操作</span><span class="sxs-lookup"><span data-stu-id="11655-176">Bot Framework card action</span></span>                              | <span data-ttu-id="11655-177">自适应卡片 Action.Submit 操作</span><span class="sxs-lookup"><span data-stu-id="11655-177">Adaptive card Action.Submit action</span></span>                     |
| ------------------------------------------------------ | ------------------------------------------------------ |
| <pre>{<br/>  "type": "invoke",<br/>  "title": "Buy",<br/>  "value": {<br/>    "type": "task/fetch",<br/>    &lt;...&gt;<br/>  }<br/>}</pre> | <pre>{<br/>  "type": "Action.Submit",<br/>  "id": "btnBuy",<br/>  "title": "Buy",<br/>  "data": {<br/>    &lt;...&gt;,<br/>    "msteams": {<br/>      "type": "task/fetch"<br/>    }<br/>  }<br/>}</pre>  |
