---
title: 定义邮件扩展操作命令
author: clearab
description: Microsoft 团队平台上的邮件扩展概述
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: 7eb734258aa34c69fa34d1413b2d3dab88e0113a
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673055"
---
# <a name="define-messaging-extension-action-commands"></a><span data-ttu-id="603c9-103">定义邮件扩展操作命令</span><span class="sxs-lookup"><span data-stu-id="603c9-103">Define messaging extension action commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="603c9-104">操作命令使您能够向用户呈现模式弹出窗口（在团队中称为任务模块），以收集或显示信息，然后处理其交互并将信息发送回团队。</span><span class="sxs-lookup"><span data-stu-id="603c9-104">Action commands allow you present your users with a modal popup (called a task module in Teams) to collect or display information, then process their interaction and send information back to Teams.</span></span> <span data-ttu-id="603c9-105">在创建您的命令之前，您需要确定：</span><span class="sxs-lookup"><span data-stu-id="603c9-105">Before creating your command you'll need to decide:</span></span>

1. <span data-ttu-id="603c9-106">从哪里可以触发操作命令？</span><span class="sxs-lookup"><span data-stu-id="603c9-106">Where can the action command be triggered from?</span></span>
1. <span data-ttu-id="603c9-107">将如何创建任务模块？</span><span class="sxs-lookup"><span data-stu-id="603c9-107">How will the task module be created?</span></span>
1. <span data-ttu-id="603c9-108">是否将最终邮件或卡片从 bot 发送到频道，或者是否将邮件或智能卡插入到撰写邮件区域中以供用户提交？</span><span class="sxs-lookup"><span data-stu-id="603c9-108">Will the final message or card be sent to the channel from a bot, or will the message or card be inserted into the compose message area for the user to submit?</span></span>

## <a name="choose-action-command-invoke-locations"></a><span data-ttu-id="603c9-109">选择操作命令调用位置</span><span class="sxs-lookup"><span data-stu-id="603c9-109">Choose action command invoke locations</span></span>

<span data-ttu-id="603c9-110">你需要确定的第一件事是，可以从哪个位置触发 action 命令（或更具体地说，*调用*）。</span><span class="sxs-lookup"><span data-stu-id="603c9-110">The first thing you need to decide is where your action command can be triggered (or more specifically, *invoked*) from.</span></span> <span data-ttu-id="603c9-111">通过`context`在应用程序清单中指定，可以从以下一个或多个位置调用命令：</span><span class="sxs-lookup"><span data-stu-id="603c9-111">By specifying the `context` in your app manifest, your command can be invoked from one or more of the following locations:</span></span>

* <span data-ttu-id="603c9-112">"撰写邮件" 区域底部的按钮。</span><span class="sxs-lookup"><span data-stu-id="603c9-112">The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="603c9-113">通过在命令框中 @mentioning 您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="603c9-113">By @mentioning your app in the command box.</span></span> <span data-ttu-id="603c9-114">注意：如果您的邮件扩展是从命令框中调用的，则不能使用直接插入到对话中的 bot 消息进行响应。</span><span class="sxs-lookup"><span data-stu-id="603c9-114">Note: You cannot respond with a bot message inserted directly into the conversation if your messaging extension is invoked from the command box.</span></span>
* <span data-ttu-id="603c9-115">直接从现有邮件，通过 .。。邮件上的溢出菜单。</span><span class="sxs-lookup"><span data-stu-id="603c9-115">Directly from an existing message via the ... overflow menu on a message.</span></span> <span data-ttu-id="603c9-116">注意：对你的 bot 的初始调用将包含一个 JSON 对象，其中包含从中调用该对象的邮件，您可以在将其处理到任务模块之前对其进行处理。</span><span class="sxs-lookup"><span data-stu-id="603c9-116">Note: The initial invoke to your bot will include a JSON object containing the message from which it was invoked, which you can process before presenting them with a task module.</span></span>

## <a name="choose-how-to-build-your-task-module"></a><span data-ttu-id="603c9-117">选择如何生成任务模块</span><span class="sxs-lookup"><span data-stu-id="603c9-117">Choose how to build your task module</span></span>

<span data-ttu-id="603c9-118">除了可以选择从中调用命令的位置之外，还必须选择如何在任务模块中为您的用户填充窗体。</span><span class="sxs-lookup"><span data-stu-id="603c9-118">In addition to choosing where your command can be invoked from, you must also chose how to populate the form in the task module for your users.</span></span> <span data-ttu-id="603c9-119">有三个选项可用于创建在任务模块中呈现的表单：</span><span class="sxs-lookup"><span data-stu-id="603c9-119">You have three options for creating the form that is rendered inside the task module:</span></span>

* <span data-ttu-id="603c9-120">**参数的静态列表**-这是最简单的选项。</span><span class="sxs-lookup"><span data-stu-id="603c9-120">**Static list of parameters** - This is the simplest option.</span></span> <span data-ttu-id="603c9-121">您可以定义应用程序清单中团队客户端将呈现的参数（输入字段）的列表。</span><span class="sxs-lookup"><span data-stu-id="603c9-121">You can define a list of parameters (input fields) in your app manifest the Teams client will render.</span></span> <span data-ttu-id="603c9-122">您无法使用此选项控制格式设置。</span><span class="sxs-lookup"><span data-stu-id="603c9-122">You cannot control the formatting with this option.</span></span>
* <span data-ttu-id="603c9-123">**自适应卡片**-您可以选择使用自适应卡片，它可以更好地控制 UI，但仍会限制可用控件和格式选项。</span><span class="sxs-lookup"><span data-stu-id="603c9-123">**Adaptive card** - You can choose to use an adaptive card, which provides greater control over the UI, but still limits you on the available controls and formatting options.</span></span>
* <span data-ttu-id="603c9-124">**嵌入的 web 视图**-如果需要对 UI 和控件进行完全控制，则可以选择在任务模块中嵌入自定义 web 视图。</span><span class="sxs-lookup"><span data-stu-id="603c9-124">**Embedded web view** - If you need complete control over the UI and controls, you can choose to embed a custom web view in the task module.</span></span>

<span data-ttu-id="603c9-125">如果选择使用静态的参数列表创建任务模块，则当用户提交任务模块时，对邮件扩展的第一次调用。</span><span class="sxs-lookup"><span data-stu-id="603c9-125">If you choose to create your task module with a static list of parameters, the first call to your messaging extension will be when a user submits the task module.</span></span> <span data-ttu-id="603c9-126">使用嵌入的 web 视图或自适应卡片时，邮件扩展将需要处理用户的初始调用事件，创建任务模块，并将其返回到客户端。</span><span class="sxs-lookup"><span data-stu-id="603c9-126">When using an embedded web view or an adaptive card, your messaging extension will need to handle an initial invoke event from the user, create the task module, and return it back to the client.</span></span>

## <a name="choose-how-the-final-message-will-be-sent"></a><span data-ttu-id="603c9-127">选择最终邮件的发送方式</span><span class="sxs-lookup"><span data-stu-id="603c9-127">Choose how the final message will be sent</span></span>

<span data-ttu-id="603c9-128">在大多数情况下，您的操作命令将导致卡片插入 "撰写" 消息框中。</span><span class="sxs-lookup"><span data-stu-id="603c9-128">In most cases, your action command will result in a card inserted into the compose message box.</span></span> <span data-ttu-id="603c9-129">然后，你的用户可以决定将其发送到频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="603c9-129">Your user can then decide to send it into the channel or chat.</span></span> <span data-ttu-id="603c9-130">在这种情况下，该消息来自用户，并且你的 bot 将无法进一步编辑或更新此卡。</span><span class="sxs-lookup"><span data-stu-id="603c9-130">The message in this case comes from the user, and your bot will not be able to edit or update the card further.</span></span>

<span data-ttu-id="603c9-131">如果您的邮件扩展是通过撰写框或直接从邮件中触发的，则您的 web 服务可以直接在频道或聊天中插入最终响应。</span><span class="sxs-lookup"><span data-stu-id="603c9-131">If your messaging extension is triggered from the compose box or directly from a message, your web service can insert the final response directly into the channel or chat.</span></span> <span data-ttu-id="603c9-132">在这种情况下，自适应卡片来自机器人，bot 将能够更新它，并且 bot 也可以在需要时回复到会话线程。</span><span class="sxs-lookup"><span data-stu-id="603c9-132">In this case, the adaptive card comes from the bot, the bot will be able to update it, and can the bot can also reply to the conversation thread if needed.</span></span> <span data-ttu-id="603c9-133">您需要使用相同的 Id `bot`将对象添加到应用程序清单，并定义相应的作用域。</span><span class="sxs-lookup"><span data-stu-id="603c9-133">You will need to add the `bot` object to your app manifest using the same Id and defining the appropriate scopes.</span></span>

## <a name="add-the-command-to-your-app-manifest"></a><span data-ttu-id="603c9-134">将命令添加到应用程序清单</span><span class="sxs-lookup"><span data-stu-id="603c9-134">Add the command to your app manifest</span></span>

<span data-ttu-id="603c9-135">现在，您已经决定了用户将如何与您的操作命令进行交互，现在是将其添加到应用程序清单中的时候了。</span><span class="sxs-lookup"><span data-stu-id="603c9-135">Now that you've decided how users will interact with your action command, it is time to add it to your app manifest.</span></span> <span data-ttu-id="603c9-136">若要执行此操作，请将`composeExtension`新对象添加到应用程序清单 JSON 的最高级别。</span><span class="sxs-lookup"><span data-stu-id="603c9-136">To do this you'll add a new `composeExtension` object to the top level of your app manifest JSON.</span></span> <span data-ttu-id="603c9-137">您可以使用应用程序 Studio 的帮助或手动执行此操作。</span><span class="sxs-lookup"><span data-stu-id="603c9-137">You can either do so with the help of App Studio, or manually.</span></span>

### <a name="create-a-command-using-app-studio"></a><span data-ttu-id="603c9-138">使用应用程序 Studio 创建命令</span><span class="sxs-lookup"><span data-stu-id="603c9-138">Create a command using App Studio</span></span>

<span data-ttu-id="603c9-139">以下步骤假定您已经[创建了邮件扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="603c9-139">The following steps assume you've already [created a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

1. <span data-ttu-id="603c9-140">在 Microsoft 团队客户端中，打开**应用程序 Studio**并选择 "**清单编辑器**" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="603c9-140">From the Microsoft Teams client, open **App Studio** and select the **Manifest Editor** tab.</span></span>
2. <span data-ttu-id="603c9-141">如果您已经在应用程序 Studio 中创建了应用程序包，请从列表中选择它。</span><span class="sxs-lookup"><span data-stu-id="603c9-141">If you've already created your app package in App Studio, chose it from the list.</span></span> <span data-ttu-id="603c9-142">如果不是，则可以导入现有的应用程序包。</span><span class="sxs-lookup"><span data-stu-id="603c9-142">If not, you can import an existing app package.</span></span>
3. <span data-ttu-id="603c9-143">单击 "命令" 部分的 "**添加**" 按钮。</span><span class="sxs-lookup"><span data-stu-id="603c9-143">Click the **Add** button in the Command section.</span></span>
4. <span data-ttu-id="603c9-144">选择 **"允许用户在团队内部触发外部服务中的操作"**。</span><span class="sxs-lookup"><span data-stu-id="603c9-144">Choose **Allow users to trigger actions in external services while inside of Teams**.</span></span>
5. <span data-ttu-id="603c9-145">如果要使用一组静态参数来创建任务模块，请选择该选项。</span><span class="sxs-lookup"><span data-stu-id="603c9-145">If you want to use a static set of parameters to create your task module, select that option.</span></span> <span data-ttu-id="603c9-146">否则，请选择**从你的 bot 中提取一组动态参数**。</span><span class="sxs-lookup"><span data-stu-id="603c9-146">Otherwise, choose to **Fetch a dynamic set of parameters from your bot**.</span></span>
6. <span data-ttu-id="603c9-147">添加**命令 Id**和**标题**。</span><span class="sxs-lookup"><span data-stu-id="603c9-147">Add a **Command Id** and a **Title**.</span></span>
7. <span data-ttu-id="603c9-148">选择要触发操作命令触发的位置。</span><span class="sxs-lookup"><span data-stu-id="603c9-148">Select where you want your action command to be triggered from.</span></span>
8. <span data-ttu-id="603c9-149">如果您使用的是任务模块的参数，请添加第一个。</span><span class="sxs-lookup"><span data-stu-id="603c9-149">If you're using parameters for your task module, add the first one.</span></span>
9. <span data-ttu-id="603c9-150">单击"保存"。</span><span class="sxs-lookup"><span data-stu-id="603c9-150">Click Save</span></span>
10. <span data-ttu-id="603c9-151">如果需要添加更多参数，请单击 "**参数**" 部分中的 "**添加**" 按钮以添加它们。</span><span class="sxs-lookup"><span data-stu-id="603c9-151">If you need to add more parameters, click the **Add** button in the **Parameters** section to add them.</span></span>

### <a name="manually-create-a-command"></a><span data-ttu-id="603c9-152">手动创建命令</span><span class="sxs-lookup"><span data-stu-id="603c9-152">Manually create a command</span></span>

<span data-ttu-id="603c9-153">若要将基于操作的消息扩展命令手动添加到应用程序清单中，需要将以下参数添加到您`composeExtension.commands`的对象数组中。</span><span class="sxs-lookup"><span data-stu-id="603c9-153">To manually add your action-based messaging extension command to your app manifest, you'll need to add the follow parameters to your `composeExtension.commands` array of objects.</span></span>

| <span data-ttu-id="603c9-154">属性名称</span><span class="sxs-lookup"><span data-stu-id="603c9-154">Property name</span></span> | <span data-ttu-id="603c9-155">用途</span><span class="sxs-lookup"><span data-stu-id="603c9-155">Purpose</span></span> | <span data-ttu-id="603c9-156">是否必需？</span><span class="sxs-lookup"><span data-stu-id="603c9-156">Required?</span></span> | <span data-ttu-id="603c9-157">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="603c9-157">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="603c9-158">您分配给此命令的唯一 ID。</span><span class="sxs-lookup"><span data-stu-id="603c9-158">Unique ID that you assign to this command.</span></span> <span data-ttu-id="603c9-159">用户请求将包括此 ID。</span><span class="sxs-lookup"><span data-stu-id="603c9-159">The user request will include this ID.</span></span> | <span data-ttu-id="603c9-160">是</span><span class="sxs-lookup"><span data-stu-id="603c9-160">Yes</span></span> | <span data-ttu-id="603c9-161">1.0</span><span class="sxs-lookup"><span data-stu-id="603c9-161">1.0</span></span> |
| `title` | <span data-ttu-id="603c9-162">命令名称。</span><span class="sxs-lookup"><span data-stu-id="603c9-162">Command name.</span></span> <span data-ttu-id="603c9-163">此值显示在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="603c9-163">This value appears in the UI.</span></span> | <span data-ttu-id="603c9-164">是</span><span class="sxs-lookup"><span data-stu-id="603c9-164">Yes</span></span> | <span data-ttu-id="603c9-165">1.0</span><span class="sxs-lookup"><span data-stu-id="603c9-165">1.0</span></span> |
| `type` | <span data-ttu-id="603c9-166">必须是 `action`</span><span class="sxs-lookup"><span data-stu-id="603c9-166">Must be `action`</span></span> | <span data-ttu-id="603c9-167">否</span><span class="sxs-lookup"><span data-stu-id="603c9-167">No</span></span> | <span data-ttu-id="603c9-168">1.4</span><span class="sxs-lookup"><span data-stu-id="603c9-168">1.4</span></span> |
| `fetchTask` | <span data-ttu-id="603c9-169">`true`对于任务模块的自适应卡片或嵌入的 web 视图， `false`对于参数的静态列表或在加载 web 视图时`taskInfo`</span><span class="sxs-lookup"><span data-stu-id="603c9-169">`true` for an adaptive card or embedded web view for your task module, `false` for a static list of parameters or when loading the web view by a `taskInfo`</span></span> | <span data-ttu-id="603c9-170">否</span><span class="sxs-lookup"><span data-stu-id="603c9-170">No</span></span> | <span data-ttu-id="603c9-171">1.4</span><span class="sxs-lookup"><span data-stu-id="603c9-171">1.4</span></span> |
| `context` | <span data-ttu-id="603c9-172">值的可选数组，用于定义可以从中调用邮件扩展的位置。</span><span class="sxs-lookup"><span data-stu-id="603c9-172">Optional array of values that defines where the messaging extension can be invoked from.</span></span> <span data-ttu-id="603c9-173">可能的值`message`为`compose`、或`commandBox`。</span><span class="sxs-lookup"><span data-stu-id="603c9-173">Possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="603c9-174">默认值为 `["compose", "commandBox"]`。</span><span class="sxs-lookup"><span data-stu-id="603c9-174">Default is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="603c9-175">否</span><span class="sxs-lookup"><span data-stu-id="603c9-175">No</span></span> | <span data-ttu-id="603c9-176">1.5</span><span class="sxs-lookup"><span data-stu-id="603c9-176">1.5</span></span> |

<span data-ttu-id="603c9-177">如果使用的是静态参数列表，则也将添加它们。</span><span class="sxs-lookup"><span data-stu-id="603c9-177">If you are using a static list of parameters, you'll add them as well.</span></span>

| <span data-ttu-id="603c9-178">属性名称</span><span class="sxs-lookup"><span data-stu-id="603c9-178">Property name</span></span> | <span data-ttu-id="603c9-179">用途</span><span class="sxs-lookup"><span data-stu-id="603c9-179">Purpose</span></span> | <span data-ttu-id="603c9-180">是否必需？</span><span class="sxs-lookup"><span data-stu-id="603c9-180">Required?</span></span> | <span data-ttu-id="603c9-181">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="603c9-181">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="603c9-182">命令的参数的静态列表。</span><span class="sxs-lookup"><span data-stu-id="603c9-182">Static list of parameters for the command.</span></span> <span data-ttu-id="603c9-183">仅在何时`fetchTask`使用`false`</span><span class="sxs-lookup"><span data-stu-id="603c9-183">Only use when `fetchTask` is `false`</span></span> | <span data-ttu-id="603c9-184">否</span><span class="sxs-lookup"><span data-stu-id="603c9-184">No</span></span> | <span data-ttu-id="603c9-185">1.0</span><span class="sxs-lookup"><span data-stu-id="603c9-185">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="603c9-186">参数的名称。</span><span class="sxs-lookup"><span data-stu-id="603c9-186">The name of the parameter.</span></span> <span data-ttu-id="603c9-187">此项将发送到用户请求中的服务。</span><span class="sxs-lookup"><span data-stu-id="603c9-187">This is sent to your service in the user request.</span></span> | <span data-ttu-id="603c9-188">是</span><span class="sxs-lookup"><span data-stu-id="603c9-188">Yes</span></span> | <span data-ttu-id="603c9-189">1.0</span><span class="sxs-lookup"><span data-stu-id="603c9-189">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="603c9-190">描述了此参数的用途或应提供的值的示例。</span><span class="sxs-lookup"><span data-stu-id="603c9-190">Describes this parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="603c9-191">此值显示在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="603c9-191">This value appears in the UI.</span></span> | <span data-ttu-id="603c9-192">是</span><span class="sxs-lookup"><span data-stu-id="603c9-192">Yes</span></span> | <span data-ttu-id="603c9-193">1.0</span><span class="sxs-lookup"><span data-stu-id="603c9-193">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="603c9-194">短用户友好参数标题或标签。</span><span class="sxs-lookup"><span data-stu-id="603c9-194">Short user-friendly parameter title or label.</span></span> | <span data-ttu-id="603c9-195">是</span><span class="sxs-lookup"><span data-stu-id="603c9-195">Yes</span></span> | <span data-ttu-id="603c9-196">1.0</span><span class="sxs-lookup"><span data-stu-id="603c9-196">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="603c9-197">设置为所需的输入类型。</span><span class="sxs-lookup"><span data-stu-id="603c9-197">Set to the type of input required.</span></span> <span data-ttu-id="603c9-198">可能的值`text`包括`textarea`、 `number`、 `date`、 `time`、 `toggle`、。</span><span class="sxs-lookup"><span data-stu-id="603c9-198">Possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="603c9-199">默认值设置为`text`</span><span class="sxs-lookup"><span data-stu-id="603c9-199">Default is set to `text`</span></span> | <span data-ttu-id="603c9-200">否</span><span class="sxs-lookup"><span data-stu-id="603c9-200">No</span></span> | <span data-ttu-id="603c9-201">1.4</span><span class="sxs-lookup"><span data-stu-id="603c9-201">1.4</span></span> |

<span data-ttu-id="603c9-202">如果使用的是嵌入的 web 视图，则可以选择添加`taskInfo`对象以获取您的 web 视图，而无需直接调用你的 bot。</span><span class="sxs-lookup"><span data-stu-id="603c9-202">If you are using an embedded web view, you can optionally add the `taskInfo` object to fetch your web view without calling your bot directly.</span></span> <span data-ttu-id="603c9-203">如果选择使用此选项，则行为类似于在中使用静态参数列表，因为与你的 bot 的第一次交互将[响应任务模块提交操作](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)。</span><span class="sxs-lookup"><span data-stu-id="603c9-203">If you choose to use this option, the behavior is similar to using a static list of parameters in that the first interaction with your bot will be [responding to the task module submit action](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span></span> <span data-ttu-id="603c9-204">如果使用的`taskInfo`是对象，请确保同时将`fetchTask`参数设置为。 `false`</span><span class="sxs-lookup"><span data-stu-id="603c9-204">If you are using a `taskInfo` object, be sure to also set the `fetchTask` parameter to `false`.</span></span>

| <span data-ttu-id="603c9-205">属性名称</span><span class="sxs-lookup"><span data-stu-id="603c9-205">Property name</span></span> | <span data-ttu-id="603c9-206">用途</span><span class="sxs-lookup"><span data-stu-id="603c9-206">Purpose</span></span> | <span data-ttu-id="603c9-207">是否必需？</span><span class="sxs-lookup"><span data-stu-id="603c9-207">Required?</span></span> | <span data-ttu-id="603c9-208">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="603c9-208">Minimum manifest version</span></span> |
|---|---|---|---|
|`taskInfo`|<span data-ttu-id="603c9-209">指定在使用消息扩展命令时要预加载的任务模块</span><span class="sxs-lookup"><span data-stu-id="603c9-209">Specify the task module to preload when using a messaging extension command</span></span>| <span data-ttu-id="603c9-210">否</span><span class="sxs-lookup"><span data-stu-id="603c9-210">No</span></span> | <span data-ttu-id="603c9-211">1.4</span><span class="sxs-lookup"><span data-stu-id="603c9-211">1.4</span></span> |
|`taskInfo.title`|<span data-ttu-id="603c9-212">初始任务模块标题</span><span class="sxs-lookup"><span data-stu-id="603c9-212">Initial task module title</span></span>|<span data-ttu-id="603c9-213">否</span><span class="sxs-lookup"><span data-stu-id="603c9-213">No</span></span> | <span data-ttu-id="603c9-214">1.4</span><span class="sxs-lookup"><span data-stu-id="603c9-214">1.4</span></span> |
|`taskInfo.width`|<span data-ttu-id="603c9-215">任务模块宽度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"</span><span class="sxs-lookup"><span data-stu-id="603c9-215">Task module width - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|<span data-ttu-id="603c9-216">否</span><span class="sxs-lookup"><span data-stu-id="603c9-216">No</span></span> | <span data-ttu-id="603c9-217">1.4</span><span class="sxs-lookup"><span data-stu-id="603c9-217">1.4</span></span> |
|`taskInfo.height`|<span data-ttu-id="603c9-218">任务模块高度-以像素为单位的数字或默认布局，如 "大"、"中" 或 "small"</span><span class="sxs-lookup"><span data-stu-id="603c9-218">Task module height - either a number in pixels or default layout such as 'large', 'medium', or 'small'</span></span>|<span data-ttu-id="603c9-219">否</span><span class="sxs-lookup"><span data-stu-id="603c9-219">No</span></span> | <span data-ttu-id="603c9-220">1.4</span><span class="sxs-lookup"><span data-stu-id="603c9-220">1.4</span></span> |
|`taskInfo.url`|<span data-ttu-id="603c9-221">初始 web 视图 URL</span><span class="sxs-lookup"><span data-stu-id="603c9-221">Initial web view URL</span></span>|<span data-ttu-id="603c9-222">否</span><span class="sxs-lookup"><span data-stu-id="603c9-222">No</span></span> | <span data-ttu-id="603c9-223">1.4</span><span class="sxs-lookup"><span data-stu-id="603c9-223">1.4</span></span> |

#### <a name="app-manifest-example"></a><span data-ttu-id="603c9-224">应用部件清单示例</span><span class="sxs-lookup"><span data-stu-id="603c9-224">App manifest example</span></span>

<span data-ttu-id="603c9-225">下面是定义两个动作命令`composeExtensions`的对象的一个示例。</span><span class="sxs-lookup"><span data-stu-id="603c9-225">The below is an example of a `composeExtensions` object defining two action commands.</span></span> <span data-ttu-id="603c9-226">这不是完整清单的完整清单示例，请参阅：[应用程序清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="603c9-226">It is not an example of the complete manifest, for the full app manifest schema see: [App manifest schema](~/resources/schema/manifest-schema.md).</span></span>

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
        "fetchTask": false,
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

## <a name="next-steps"></a><span data-ttu-id="603c9-227">后续步骤</span><span class="sxs-lookup"><span data-stu-id="603c9-227">Next steps</span></span>

<span data-ttu-id="603c9-228">如果您使用的是自适应卡片或不带`taskInfo`对象的嵌入式 web 视图，则需要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="603c9-228">If you are using either an adaptive card or an embedded web view without a `taskInfo` object, you'll want to:</span></span>

* [<span data-ttu-id="603c9-229">使用任务模块创建和响应</span><span class="sxs-lookup"><span data-stu-id="603c9-229">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/create-task-module.md)

<span data-ttu-id="603c9-230">如果使用的是带`taskInfo`对象的参数或嵌入的 web 视图，则下一步是：</span><span class="sxs-lookup"><span data-stu-id="603c9-230">If you are using parameters or an embedded web view with a `taskInfo` object, the next step for you is to:</span></span>

* [<span data-ttu-id="603c9-231">响应任务模块提交</span><span class="sxs-lookup"><span data-stu-id="603c9-231">Respond to task module submit</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

[!include[messaging-extension-learn-more](~/includes/messaging-extensions/learn-more.md)]
