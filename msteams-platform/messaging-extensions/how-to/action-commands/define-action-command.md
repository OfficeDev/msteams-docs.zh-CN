---
title: 定义邮件扩展操作命令
author: clearab
description: 邮件扩展操作命令概述
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: be2135477c4234187f374aef215f90e8329fb74e
ms.sourcegitcommit: 5739245903278d521ec920427248b6b48676e637
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/07/2021
ms.locfileid: "49778399"
---
# <a name="define-messaging-extension-action-commands"></a><span data-ttu-id="22221-103">定义邮件扩展操作命令</span><span class="sxs-lookup"><span data-stu-id="22221-103">Define messaging extension action commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="22221-104">使用操作命令 (，你可以向用户显示名为 Teams) 中任务模块的模式弹出窗口，以收集或显示信息，然后处理他们的交互并将信息发送回 Teams。</span><span class="sxs-lookup"><span data-stu-id="22221-104">Action commands allow you present your users with a modal popup (called a task module in Teams) to collect or display information, then process their interaction and send information back to Teams.</span></span> <span data-ttu-id="22221-105">在创建命令之前，你需要决定：</span><span class="sxs-lookup"><span data-stu-id="22221-105">Before creating your command you'll need to decide:</span></span>

1. <span data-ttu-id="22221-106">可以从何处触发操作命令？</span><span class="sxs-lookup"><span data-stu-id="22221-106">Where can the action command be triggered from?</span></span>
1. <span data-ttu-id="22221-107">如何创建任务模块？</span><span class="sxs-lookup"><span data-stu-id="22221-107">How will the task module be created?</span></span>
1. <span data-ttu-id="22221-108">最终的邮件或卡片是从自动程序发送到频道，还是将邮件或卡片插入撰写邮件区域供用户提交？</span><span class="sxs-lookup"><span data-stu-id="22221-108">Will the final message or card be sent to the channel from a bot, or will the message or card be inserted into the compose message area for the user to submit?</span></span>

## <a name="choose-action-command-invoke-locations"></a><span data-ttu-id="22221-109">选择操作命令调用位置</span><span class="sxs-lookup"><span data-stu-id="22221-109">Choose action command invoke locations</span></span>

<span data-ttu-id="22221-110">首先需要确定操作命令的触发位置，具体 (调用命令) 位置。 </span><span class="sxs-lookup"><span data-stu-id="22221-110">The first thing you need to decide is where your action command can be triggered (or more specifically, *invoked*) from.</span></span> <span data-ttu-id="22221-111">通过指定 `context` 应用清单中的命令，可以从以下一个或多个位置调用命令：</span><span class="sxs-lookup"><span data-stu-id="22221-111">By specifying the `context` in your app manifest, your command can be invoked from one or more of the following locations:</span></span>

* <span data-ttu-id="22221-112">撰写邮件区域底部的按钮。</span><span class="sxs-lookup"><span data-stu-id="22221-112">The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="22221-113">By @mentioning your app in the command box.</span><span class="sxs-lookup"><span data-stu-id="22221-113">By @mentioning your app in the command box.</span></span> <span data-ttu-id="22221-114">注意：如果从命令框调用消息扩展，则不能使用直接插入到对话中的自动程序消息进行响应。</span><span class="sxs-lookup"><span data-stu-id="22221-114">Note: You cannot respond with a bot message inserted directly into the conversation if your messaging extension is invoked from the command box.</span></span>
* <span data-ttu-id="22221-115">直接通过 ... 从现有邮件发送...消息上的溢出菜单。</span><span class="sxs-lookup"><span data-stu-id="22221-115">Directly from an existing message via the ... overflow menu on a message.</span></span> <span data-ttu-id="22221-116">注意：对自动程序的初始调用将包括一个 JSON 对象，该对象包含从其中调用它的消息，你可以先处理该对象，然后再向它们显示任务模块。</span><span class="sxs-lookup"><span data-stu-id="22221-116">Note: The initial invoke to your bot will include a JSON object containing the message from which it was invoked, which you can process before presenting them with a task module.</span></span>

## <a name="choose-how-to-build-your-task-module"></a><span data-ttu-id="22221-117">选择如何生成任务模块</span><span class="sxs-lookup"><span data-stu-id="22221-117">Choose how to build your task module</span></span>

<span data-ttu-id="22221-118">除了选择命令的调用位置之外，还必须选择如何在任务模块中为用户填充表单。</span><span class="sxs-lookup"><span data-stu-id="22221-118">In addition to choosing where your command can be invoked from, you must also chose how to populate the form in the task module for your users.</span></span> <span data-ttu-id="22221-119">有三个选项用于创建在任务模块内呈现的表单：</span><span class="sxs-lookup"><span data-stu-id="22221-119">You have three options for creating the form that is rendered inside the task module:</span></span>

* <span data-ttu-id="22221-120">**参数的静态列表** - 这是最简单的选项。</span><span class="sxs-lookup"><span data-stu-id="22221-120">**Static list of parameters** - This is the simplest option.</span></span> <span data-ttu-id="22221-121">可以在 Teams 客户端将 (的应用清单) 输入字段定义参数列表。</span><span class="sxs-lookup"><span data-stu-id="22221-121">You can define a list of parameters (input fields) in your app manifest the Teams client will render.</span></span> <span data-ttu-id="22221-122">不能使用此选项控制格式。</span><span class="sxs-lookup"><span data-stu-id="22221-122">You cannot control the formatting with this option.</span></span>
* <span data-ttu-id="22221-123">**自适应卡片** - 你可以选择使用自适应卡片，它可更好地控制 UI，但仍限制你使用可用的控件和格式设置选项。</span><span class="sxs-lookup"><span data-stu-id="22221-123">**Adaptive card** - You can choose to use an adaptive card, which provides greater control over the UI, but still limits you on the available controls and formatting options.</span></span>
* <span data-ttu-id="22221-124">**嵌入式 Web 视图** - 如果需要完全控制 UI 和控件，可以选择在任务模块中嵌入自定义 Web 视图。</span><span class="sxs-lookup"><span data-stu-id="22221-124">**Embedded web view** - If you need complete control over the UI and controls, you can choose to embed a custom web view in the task module.</span></span>

<span data-ttu-id="22221-125">如果选择使用静态参数列表创建任务模块，则当用户提交任务模块时，将首次调用邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="22221-125">If you choose to create your task module with a static list of parameters, the first call to your messaging extension will be when a user submits the task module.</span></span> <span data-ttu-id="22221-126">使用嵌入式 Web 视图或自适应卡片时，邮件扩展将需要处理来自用户的初始调用事件、创建任务模块，然后返回给客户端。</span><span class="sxs-lookup"><span data-stu-id="22221-126">When using an embedded web view or an adaptive card, your messaging extension will need to handle an initial invoke event from the user, create the task module, and return it back to the client.</span></span>

## <a name="choose-how-the-final-message-will-be-sent"></a><span data-ttu-id="22221-127">选择最终邮件的发送</span><span class="sxs-lookup"><span data-stu-id="22221-127">Choose how the final message will be sent</span></span>

<span data-ttu-id="22221-128">在大多数情况下，您的操作命令将导致在撰写邮件框中插入卡片。</span><span class="sxs-lookup"><span data-stu-id="22221-128">In most cases, your action command will result in a card inserted into the compose message box.</span></span> <span data-ttu-id="22221-129">然后，你的用户可以决定将其发送到频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="22221-129">Your user can then decide to send it into the channel or chat.</span></span> <span data-ttu-id="22221-130">在这种情况下，消息来自用户，你的自动程序将无法进一步编辑或更新卡片。</span><span class="sxs-lookup"><span data-stu-id="22221-130">The message in this case comes from the user, and your bot will not be able to edit or update the card further.</span></span>

<span data-ttu-id="22221-131">如果消息扩展从撰写框或直接从消息中触发，则 Web 服务可以直接将最终响应插入频道或聊天中。</span><span class="sxs-lookup"><span data-stu-id="22221-131">If your messaging extension is triggered from the compose box or directly from a message, your web service can insert the final response directly into the channel or chat.</span></span> <span data-ttu-id="22221-132">在这种情况下，自适应卡片来自自动程序，自动程序将能够更新它，并且机器人还可以根据需要回复对话线程。</span><span class="sxs-lookup"><span data-stu-id="22221-132">In this case, the adaptive card comes from the bot, the bot will be able to update it, and the bot can also reply to the conversation thread if needed.</span></span> <span data-ttu-id="22221-133">你将需要使用相同的 ID 和定义适当的范围将对象添加到 `bot` 应用清单。</span><span class="sxs-lookup"><span data-stu-id="22221-133">You will need to add the `bot` object to your app manifest using the same Id and defining the appropriate scopes.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="22221-134">将命令添加到应用清单</span><span class="sxs-lookup"><span data-stu-id="22221-134">Add the command to your app manifest</span></span>

<span data-ttu-id="22221-135">现在，你已决定用户如何与操作命令交互，是时候将其添加到应用清单了。</span><span class="sxs-lookup"><span data-stu-id="22221-135">Now that you've decided how users will interact with your action command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="22221-136">为此，你需要将新对象添加到应用清单 `composeExtension` JSON 的顶层。</span><span class="sxs-lookup"><span data-stu-id="22221-136">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="22221-137">可以在 App Studio 的帮助下完成操作，也可以手动完成。</span><span class="sxs-lookup"><span data-stu-id="22221-137">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="22221-138">使用 App Studio 创建命令</span><span class="sxs-lookup"><span data-stu-id="22221-138">Create a command using App Studio</span></span>

<span data-ttu-id="22221-139">以下步骤假定你已 [创建邮件扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="22221-139">The following steps assume you've already [created a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

1. <span data-ttu-id="22221-140">从 Microsoft Teams 客户端中，打开 **App Studio** 并选择清单 **编辑器** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="22221-140">From the Microsoft Teams client, open **App Studio** and select the **Manifest Editor** tab.</span></span>
2. <span data-ttu-id="22221-141">如果你已在 App Studio 中创建应用包，请从列表中选择它。</span><span class="sxs-lookup"><span data-stu-id="22221-141">If you've already created your app package in App Studio, chose it from the list.</span></span> <span data-ttu-id="22221-142">如果没有，你可以导入现有应用包。</span><span class="sxs-lookup"><span data-stu-id="22221-142">If not, you can import an existing app package.</span></span>
3. <span data-ttu-id="22221-143">单击 **"命令** "部分中的"添加"按钮。</span><span class="sxs-lookup"><span data-stu-id="22221-143">Click the **Add** button in the Command section.</span></span>
4. <span data-ttu-id="22221-144">选择 **"允许用户在 Teams 内触发外部服务中的操作"。**</span><span class="sxs-lookup"><span data-stu-id="22221-144">Choose **Allow users to trigger actions in external services while inside of Teams**.</span></span>
5. <span data-ttu-id="22221-145">如果要使用一组静态参数来创建任务模块，请选择该选项。</span><span class="sxs-lookup"><span data-stu-id="22221-145">If you want to use a static set of parameters to create your task module, select that option.</span></span> <span data-ttu-id="22221-146">否则，请选择 **从自动程序获取一组动态参数**。</span><span class="sxs-lookup"><span data-stu-id="22221-146">Otherwise, choose to **Fetch a dynamic set of parameters from your bot**.</span></span>
6. <span data-ttu-id="22221-147">添加命令 **ID** 和 **标题**。</span><span class="sxs-lookup"><span data-stu-id="22221-147">Add a **Command Id** and a **Title**.</span></span>
7. <span data-ttu-id="22221-148">选择要从何处触发操作命令。</span><span class="sxs-lookup"><span data-stu-id="22221-148">Select where you want your action command to be triggered from.</span></span>
8. <span data-ttu-id="22221-149">如果对任务模块使用参数，请添加第一个参数。</span><span class="sxs-lookup"><span data-stu-id="22221-149">If you're using parameters for your task module, add the first one.</span></span>
9. <span data-ttu-id="22221-150">单击"保存"。</span><span class="sxs-lookup"><span data-stu-id="22221-150">Click Save</span></span>
10. <span data-ttu-id="22221-151">如果需要添加更多参数，请单击"参数"部分中的"添加"按钮以添加它们。</span><span class="sxs-lookup"><span data-stu-id="22221-151">If you need to add more parameters, click the **Add** button in the **Parameters** section to add them.</span></span>

### <a name="manually-create-a-command"></a><span data-ttu-id="22221-152">手动创建命令</span><span class="sxs-lookup"><span data-stu-id="22221-152">Manually create a command</span></span>

<span data-ttu-id="22221-153">若要将基于操作的消息扩展命令手动添加到应用清单，你需要将以下参数添加到对象 `composeExtension.commands` 数组。</span><span class="sxs-lookup"><span data-stu-id="22221-153">To manually add your action-based messaging extension command to your app manifest, you'll need to add the follow parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="22221-154">属性名称</span><span class="sxs-lookup"><span data-stu-id="22221-154">Property name</span></span> | <span data-ttu-id="22221-155">用途</span><span class="sxs-lookup"><span data-stu-id="22221-155">Purpose</span></span> | <span data-ttu-id="22221-156">是否必需？</span><span class="sxs-lookup"><span data-stu-id="22221-156">Required?</span></span> | <span data-ttu-id="22221-157">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="22221-157">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="22221-158">分配给此命令的唯一 ID。</span><span class="sxs-lookup"><span data-stu-id="22221-158">Unique ID that you assign to this command.</span></span> <span data-ttu-id="22221-159">用户请求将包含此 ID。</span><span class="sxs-lookup"><span data-stu-id="22221-159">The user request will include this ID.</span></span> | <span data-ttu-id="22221-160">是</span><span class="sxs-lookup"><span data-stu-id="22221-160">Yes</span></span> | <span data-ttu-id="22221-161">1.0</span><span class="sxs-lookup"><span data-stu-id="22221-161">1.0</span></span> |
| `title` | <span data-ttu-id="22221-162">命令名称。</span><span class="sxs-lookup"><span data-stu-id="22221-162">Command name.</span></span> <span data-ttu-id="22221-163">此值显示在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="22221-163">This value appears in the UI.</span></span> | <span data-ttu-id="22221-164">是</span><span class="sxs-lookup"><span data-stu-id="22221-164">Yes</span></span> | <span data-ttu-id="22221-165">1.0</span><span class="sxs-lookup"><span data-stu-id="22221-165">1.0</span></span> |
| `type` | <span data-ttu-id="22221-166">必须是 `action`</span><span class="sxs-lookup"><span data-stu-id="22221-166">Must be `action`</span></span> | <span data-ttu-id="22221-167">否</span><span class="sxs-lookup"><span data-stu-id="22221-167">No</span></span> | <span data-ttu-id="22221-168">1.4</span><span class="sxs-lookup"><span data-stu-id="22221-168">1.4</span></span> |
| `fetchTask` | <span data-ttu-id="22221-169">`true`对于任务模块的自适应卡片或嵌入式 Web 视图，对于静态参数列表，或者当通过 `false``taskInfo`</span><span class="sxs-lookup"><span data-stu-id="22221-169">`true` for an adaptive card or embedded web view for your task module, `false` for a static list of parameters or when loading the web view by a `taskInfo`</span></span> | <span data-ttu-id="22221-170">否</span><span class="sxs-lookup"><span data-stu-id="22221-170">No</span></span> | <span data-ttu-id="22221-171">1.4</span><span class="sxs-lookup"><span data-stu-id="22221-171">1.4</span></span> |
| `context` | <span data-ttu-id="22221-172">用于定义可以从何处调用邮件扩展的值的可选数组。</span><span class="sxs-lookup"><span data-stu-id="22221-172">Optional array of values that defines where the messaging extension can be invoked from.</span></span> <span data-ttu-id="22221-173">可能的值是 `message` ， `compose` 或 `commandBox` 。</span><span class="sxs-lookup"><span data-stu-id="22221-173">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="22221-174">默认值为 `["compose", "commandBox"]`。</span><span class="sxs-lookup"><span data-stu-id="22221-174">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="22221-175">否</span><span class="sxs-lookup"><span data-stu-id="22221-175">No</span></span> | <span data-ttu-id="22221-176">1.5</span><span class="sxs-lookup"><span data-stu-id="22221-176">1.5</span></span> |

<span data-ttu-id="22221-177">如果使用静态参数列表，则也会添加它们。</span><span class="sxs-lookup"><span data-stu-id="22221-177">If you are using a static list of parameters, you'll add them as well.</span></span>

| <span data-ttu-id="22221-178">属性名称</span><span class="sxs-lookup"><span data-stu-id="22221-178">Property name</span></span> | <span data-ttu-id="22221-179">用途</span><span class="sxs-lookup"><span data-stu-id="22221-179">Purpose</span></span> | <span data-ttu-id="22221-180">是否必需？</span><span class="sxs-lookup"><span data-stu-id="22221-180">Required?</span></span> | <span data-ttu-id="22221-181">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="22221-181">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="22221-182">命令的参数静态列表。</span><span class="sxs-lookup"><span data-stu-id="22221-182">Static list of parameters for the command.</span></span> <span data-ttu-id="22221-183">仅在为时 `fetchTask` 使用 `false`</span><span class="sxs-lookup"><span data-stu-id="22221-183">Only use when `fetchTask` is `false`</span></span> | <span data-ttu-id="22221-184">否</span><span class="sxs-lookup"><span data-stu-id="22221-184">No</span></span> | <span data-ttu-id="22221-185">1.0</span><span class="sxs-lookup"><span data-stu-id="22221-185">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="22221-186">参数的名称。</span><span class="sxs-lookup"><span data-stu-id="22221-186">The name of the parameter.</span></span> <span data-ttu-id="22221-187">这将在用户请求中发送到你的服务。</span><span class="sxs-lookup"><span data-stu-id="22221-187">This is sent to your service in the user request.</span></span> | <span data-ttu-id="22221-188">是</span><span class="sxs-lookup"><span data-stu-id="22221-188">Yes</span></span> | <span data-ttu-id="22221-189">1.0</span><span class="sxs-lookup"><span data-stu-id="22221-189">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="22221-190">描述此参数的目的或应提供的值示例。</span><span class="sxs-lookup"><span data-stu-id="22221-190">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="22221-191">此值显示在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="22221-191">This value appears in the UI.</span></span> | <span data-ttu-id="22221-192">是</span><span class="sxs-lookup"><span data-stu-id="22221-192">Yes</span></span> | <span data-ttu-id="22221-193">1.0</span><span class="sxs-lookup"><span data-stu-id="22221-193">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="22221-194">简短的用户友好参数标题或标签。</span><span class="sxs-lookup"><span data-stu-id="22221-194">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="22221-195">是</span><span class="sxs-lookup"><span data-stu-id="22221-195">Yes</span></span> | <span data-ttu-id="22221-196">1.0</span><span class="sxs-lookup"><span data-stu-id="22221-196">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="22221-197">设置为所需的输入类型。</span><span class="sxs-lookup"><span data-stu-id="22221-197">Set to the type of input required.</span></span> <span data-ttu-id="22221-198">可能的值包括 `text` `textarea` ， ， `number` `date` `time` `toggle` 。</span><span class="sxs-lookup"><span data-stu-id="22221-198">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="22221-199">默认值设置为 `text`</span><span class="sxs-lookup"><span data-stu-id="22221-199">Default is set to `text`</span></span> | <span data-ttu-id="22221-200">否</span><span class="sxs-lookup"><span data-stu-id="22221-200">No</span></span> | <span data-ttu-id="22221-201">1.4</span><span class="sxs-lookup"><span data-stu-id="22221-201">1.4</span></span> |

<span data-ttu-id="22221-202">如果使用的是嵌入式 Web 视图，可以选择添加对象以提取 Web 视图，而无需 `taskInfo` 直接调用机器人。</span><span class="sxs-lookup"><span data-stu-id="22221-202">If you are using an embedded web view, you can optionally add the `taskInfo` object to fetch your web view without calling your bot directly.</span></span> <span data-ttu-id="22221-203">如果选择使用此选项，则此行为类似于使用静态参数列表，这是因为与机器人的第一次交互将响应任务 [模块提交操作](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)。</span><span class="sxs-lookup"><span data-stu-id="22221-203">If you choose to use this option, the behavior is similar to using a static list of parameters in that the first interaction with your bot will be [responding to the task module submit action](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span></span> <span data-ttu-id="22221-204">如果使用的是对象 `taskInfo` ，请确保还要将参数 `fetchTask` 设置为 `false` 。</span><span class="sxs-lookup"><span data-stu-id="22221-204">If you are using a `taskInfo` object, be sure to also set the `fetchTask` parameter to `false`.</span></span>

| <span data-ttu-id="22221-205">属性名称</span><span class="sxs-lookup"><span data-stu-id="22221-205">Property name</span></span> | <span data-ttu-id="22221-206">用途</span><span class="sxs-lookup"><span data-stu-id="22221-206">Purpose</span></span> | <span data-ttu-id="22221-207">是否必需？</span><span class="sxs-lookup"><span data-stu-id="22221-207">Required?</span></span> | <span data-ttu-id="22221-208">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="22221-208">Minimum manifest version</span></span> |
|---|---|---|---|
|`taskInfo`|<span data-ttu-id="22221-209">指定使用消息传递扩展命令时要预加载的任务模块</span><span class="sxs-lookup"><span data-stu-id="22221-209">Specify the task module to preload when using a messaging extension command</span></span>| <span data-ttu-id="22221-210">否</span><span class="sxs-lookup"><span data-stu-id="22221-210">No</span></span> | <span data-ttu-id="22221-211">1.4</span><span class="sxs-lookup"><span data-stu-id="22221-211">1.4</span></span> |
|`taskInfo.title`|<span data-ttu-id="22221-212">初始任务模块标题</span><span class="sxs-lookup"><span data-stu-id="22221-212">Initial task module title</span></span>|<span data-ttu-id="22221-213">否</span><span class="sxs-lookup"><span data-stu-id="22221-213">No</span></span> | <span data-ttu-id="22221-214">1.4</span><span class="sxs-lookup"><span data-stu-id="22221-214">1.4</span></span> |
|`taskInfo.width`|<span data-ttu-id="22221-215">任务模块宽度 - 一个数字（以像素为单位）或默认布局，如"large"、"medium"或"small"</span><span class="sxs-lookup"><span data-stu-id="22221-215">Task module width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|<span data-ttu-id="22221-216">否</span><span class="sxs-lookup"><span data-stu-id="22221-216">No</span></span> | <span data-ttu-id="22221-217">1.4</span><span class="sxs-lookup"><span data-stu-id="22221-217">1.4</span></span> |
|`taskInfo.height`|<span data-ttu-id="22221-218">任务模块高度 - 一个数字（以像素为单位）或默认布局，如"large"、"medium"或"small"</span><span class="sxs-lookup"><span data-stu-id="22221-218">Task module height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|<span data-ttu-id="22221-219">否</span><span class="sxs-lookup"><span data-stu-id="22221-219">No</span></span> | <span data-ttu-id="22221-220">1.4</span><span class="sxs-lookup"><span data-stu-id="22221-220">1.4</span></span> |
|`taskInfo.url`|<span data-ttu-id="22221-221">初始 Web 视图 URL</span><span class="sxs-lookup"><span data-stu-id="22221-221">Initial web view URL</span></span>|<span data-ttu-id="22221-222">否</span><span class="sxs-lookup"><span data-stu-id="22221-222">No</span></span> | <span data-ttu-id="22221-223">1.4</span><span class="sxs-lookup"><span data-stu-id="22221-223">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="22221-224">应用清单示例</span><span class="sxs-lookup"><span data-stu-id="22221-224">App manifest example</span></span>

<span data-ttu-id="22221-225">下面是定义两个操作 `composeExtensions` 命令的对象示例。</span><span class="sxs-lookup"><span data-stu-id="22221-225">The below is an example of a `composeExtensions` object defining two action commands.</span></span> <span data-ttu-id="22221-226">这不是完整清单的示例，有关完整应用清单架构，请参阅： [应用清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="22221-226">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

```json
...
"composeExtensions": [
  {
    "botId": "12a3c29f-1fc5-4d97-a142-12bb662b7b23",
    "canUpdateConfiguration": true,
    "commands": [
      {
        "id": "addTodo",
        "description": "Create a To Do item",
        "title": "Create To Do",
        "type": "action",
        "context": ["commandBox", "message", "compose"],
        "fetchTask": true,
        "parameters": [
          {
            "name": "Name",
            "description": "To Do Title",
            "title": "Title",
            "inputType": "text"
          },
          {
            "name": "Description",
            "description": "Description of the task",
            "title": "Description",
            "inputType": "textarea"
          },
          {
            "name": "Date",
            "description": "Due date for the task",
            "title": "Date",
            "inputType": "date"
          }
        ]
      },
      {
        "id": "reassignTodo",
        "description": "Reassign a todo item",
        "title": "Reassign a todo item",
        "type": "action",
        "fetchTask": true,
      }
    ]
  }
]
...
```

## <a name="next-steps"></a><span data-ttu-id="22221-227">后续步骤</span><span class="sxs-lookup"><span data-stu-id="22221-227">Next steps</span></span>

<span data-ttu-id="22221-228">如果你使用的是自适应卡片或没有对象的嵌入 Web 视图， `taskInfo` 你将希望：</span><span class="sxs-lookup"><span data-stu-id="22221-228">If you are using either an adaptive card or an embedded web view without a `taskInfo` object, you'll want to:</span></span>

* [<span data-ttu-id="22221-229">使用任务模块创建和响应</span><span class="sxs-lookup"><span data-stu-id="22221-229">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/create-task-module.md)

<span data-ttu-id="22221-230">如果将参数或嵌入的 Web 视图与对象一同使用，下一步是 `taskInfo` ：</span><span class="sxs-lookup"><span data-stu-id="22221-230">If you are using parameters or an embedded web view with a `taskInfo` object, the next step for you is to:</span></span>

* [<span data-ttu-id="22221-231">响应任务模块提交</span><span class="sxs-lookup"><span data-stu-id="22221-231">Respond to task module submit</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
