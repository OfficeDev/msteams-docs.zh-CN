---
title: 定义消息传递扩展操作命令
author: clearab
description: 邮件扩展操作命令概述
localization_priority: Normal
ms.topic: conceptual
ms.author: anclear
ms.openlocfilehash: f49e821ecb98659b4cfd68f93b37f1a8f611a9fb
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020714"
---
# <a name="define-messaging-extension-action-commands"></a><span data-ttu-id="3472a-103">定义消息传递扩展操作命令</span><span class="sxs-lookup"><span data-stu-id="3472a-103">Define messaging extension action commands</span></span>

[!include[v4-to-v3-SDK-pointer](~/includes/v4-to-v3-pointer-me.md)]

<span data-ttu-id="3472a-104">操作命令允许你向用户显示 Teams 中称为任务模块的模式弹出窗口。</span><span class="sxs-lookup"><span data-stu-id="3472a-104">Action commands allow you to present your users with a modal popup called a task module in Teams.</span></span> <span data-ttu-id="3472a-105">任务模块收集或显示信息、处理交互并将信息发送回 Teams。</span><span class="sxs-lookup"><span data-stu-id="3472a-105">The task module collects or displays information, processes the interaction and sends the information back to Teams.</span></span> <span data-ttu-id="3472a-106">本文档指导您如何选择操作命令调用位置、创建任务模块、发送最终消息或卡片、使用 app studio 创建操作命令或手动创建它。</span><span class="sxs-lookup"><span data-stu-id="3472a-106">This document guides you on how to select action command invoke locations, create your task module, send final message, or card, create action command using app studio, or create it manually.</span></span> 

<span data-ttu-id="3472a-107">在创建操作命令之前，必须确定以下因素：</span><span class="sxs-lookup"><span data-stu-id="3472a-107">Before creating the action command you must decide the following factors:</span></span>

1. [<span data-ttu-id="3472a-108">可以从何处触发操作命令？</span><span class="sxs-lookup"><span data-stu-id="3472a-108">Where can the action command be triggered from?</span></span>](#select-action-command-invoke-locations)
1. [<span data-ttu-id="3472a-109">如何创建任务模块？</span><span class="sxs-lookup"><span data-stu-id="3472a-109">How will the task module be created?</span></span>](#select-how-to-create-your-task-module)
1. [<span data-ttu-id="3472a-110">最终的邮件或卡片是从自动程序发送到频道，还是将邮件或卡片插入撰写邮件区域供用户提交？</span><span class="sxs-lookup"><span data-stu-id="3472a-110">Will the final message or card be sent to the channel from a bot, or will the message or card be inserted into the compose message area for the user to submit?</span></span>](#select-how-the-final-message-is-sent)

## <a name="select-action-command-invoke-locations"></a><span data-ttu-id="3472a-111">选择操作命令调用位置</span><span class="sxs-lookup"><span data-stu-id="3472a-111">Select action command invoke locations</span></span>

<span data-ttu-id="3472a-112">首先，必须决定必须调用操作命令的位置。</span><span class="sxs-lookup"><span data-stu-id="3472a-112">First, you must decide the location from where your action command must be invoked.</span></span> <span data-ttu-id="3472a-113">通过指定应用清单中的 ，可以从以下一个或多个位置调用 `context` 命令：</span><span class="sxs-lookup"><span data-stu-id="3472a-113">By specifying the `context` in your app manifest, your command can be invoked from one or more of the following locations:</span></span>

* <span data-ttu-id="3472a-114">撰写邮件区域：撰写邮件区域底部的按钮。</span><span class="sxs-lookup"><span data-stu-id="3472a-114">Compose message area: The buttons at the bottom of the compose message area.</span></span>
* <span data-ttu-id="3472a-115">命令框：@mentioning命令框中显示你的应用。</span><span class="sxs-lookup"><span data-stu-id="3472a-115">Command box: By @mentioning your app in the command box.</span></span> 
   > [!NOTE]
   > <span data-ttu-id="3472a-116">如果从命令框调用消息扩展，则不能使用直接插入对话中的自动程序消息进行响应。</span><span class="sxs-lookup"><span data-stu-id="3472a-116">If messaging extension is invoked from the command box, you cannot respond with a bot message inserted directly into the conversation.</span></span>

* <span data-ttu-id="3472a-117">消息：直接通过邮件上的溢出 `...` 菜单从现有邮件发送。</span><span class="sxs-lookup"><span data-stu-id="3472a-117">Message: Directly from an existing message through the `...` overflow menu on a message.</span></span> 
    > [!NOTE] 
    > <span data-ttu-id="3472a-118">对自动程序的初始调用包括一个 JSON 对象，其中包含从其中调用它的消息。</span><span class="sxs-lookup"><span data-stu-id="3472a-118">The initial invoke to your bot includes a JSON object containing the message from which it was invoked.</span></span> <span data-ttu-id="3472a-119">可以在向邮件显示任务模块之前处理邮件。</span><span class="sxs-lookup"><span data-stu-id="3472a-119">You can process the message before presenting them with a task module.</span></span>

<span data-ttu-id="3472a-120">下图显示了调用 action 命令的位置：</span><span class="sxs-lookup"><span data-stu-id="3472a-120">The following image displays the locations from where action command is invoked:</span></span>

![操作命令调用位置](~/assets/images/messaging-extension-invoke-locations.png)

## <a name="select-how-to-create-your-task-module"></a><span data-ttu-id="3472a-122">选择如何创建任务模块</span><span class="sxs-lookup"><span data-stu-id="3472a-122">Select how to create your task module</span></span>

<span data-ttu-id="3472a-123">除了选择命令的调用位置之外，还必须选择如何为用户填充任务模块中的窗体。</span><span class="sxs-lookup"><span data-stu-id="3472a-123">In addition to selecting where your command can be invoked from, you must also select how to populate the form in the task module for your users.</span></span> <span data-ttu-id="3472a-124">有以下三个选项用于创建在任务模块内呈现的窗体：</span><span class="sxs-lookup"><span data-stu-id="3472a-124">You have the following three options for creating the form that is rendered inside the task module:</span></span>   

* <span data-ttu-id="3472a-125">**参数的静态列表**：这是最简单的方法。</span><span class="sxs-lookup"><span data-stu-id="3472a-125">**Static list of parameters**: This is the simplest method.</span></span> <span data-ttu-id="3472a-126">可以在 Teams 客户端呈现的应用清单中定义参数列表，但在这种情况下无法控制格式。</span><span class="sxs-lookup"><span data-stu-id="3472a-126">You can define a list of parameters in your app manifest the Teams client renders, but cannot control the formatting in this case.</span></span>
* <span data-ttu-id="3472a-127">**自适应卡片**：可以选择使用自适应卡片，该卡片可以更好地控制 UI，但仍限制可用控件和格式设置选项。</span><span class="sxs-lookup"><span data-stu-id="3472a-127">**Adaptive Card**:  You can select to use an Adaptive Card, which provides greater control over the UI, but still limits you on the available controls and formatting options.</span></span>
* <span data-ttu-id="3472a-128">**嵌入式 Web 视图**：可以选择在任务模块中嵌入自定义 Web 视图，以便完全控制 UI 和控件。</span><span class="sxs-lookup"><span data-stu-id="3472a-128">**Embedded web view**: You can select to embed a custom web view in the task module to have a complete control over the UI and controls.</span></span> 

<span data-ttu-id="3472a-129">如果选择创建包含参数静态列表的任务模块，并且当用户提交任务模块时，将调用消息扩展。</span><span class="sxs-lookup"><span data-stu-id="3472a-129">If you select to create the task module with a static list of parameters and when the user submits the task module, the messaging extension is called.</span></span> <span data-ttu-id="3472a-130">使用嵌入式 Web 视图或自适应卡片时，邮件扩展必须处理来自用户的初始调用事件、创建任务模块，并返回到客户端。</span><span class="sxs-lookup"><span data-stu-id="3472a-130">When using an embedded web view or an Adaptive Card, your messaging extension must handle an initial invoke event from the user, create the task module, and return it back to the client.</span></span>

## <a name="select-how-the-final-message-is-sent"></a><span data-ttu-id="3472a-131">选择最终邮件的发送</span><span class="sxs-lookup"><span data-stu-id="3472a-131">Select how the final message is sent</span></span>

<span data-ttu-id="3472a-132">在大多数情况下，操作命令会导致在撰写消息框中插入一个卡片。</span><span class="sxs-lookup"><span data-stu-id="3472a-132">In most cases, the action command results in a card inserted into the compose message box.</span></span> <span data-ttu-id="3472a-133">用户可以将其发送到频道或聊天。</span><span class="sxs-lookup"><span data-stu-id="3472a-133">The user can send it into the channel or chat.</span></span> <span data-ttu-id="3472a-134">在这种情况下，邮件来自用户，机器人无法进一步编辑或更新卡片。</span><span class="sxs-lookup"><span data-stu-id="3472a-134">In this case, the message comes from the user, and the bot cannot edit or update the card further.</span></span>

<span data-ttu-id="3472a-135">如果消息扩展从撰写框或直接通过消息调用，则 Web 服务可以直接将最终响应插入频道或聊天中。</span><span class="sxs-lookup"><span data-stu-id="3472a-135">If the messaging extension is invoked from the compose box or directly from a message, your web service can insert the final response directly into the channel or chat.</span></span> <span data-ttu-id="3472a-136">在这种情况下，自适应卡片来自机器人，机器人会更新它，并根据需要回复到对话线程。</span><span class="sxs-lookup"><span data-stu-id="3472a-136">In this case, the Adaptive Card comes from the bot, the bot updates it, and replies to the conversation thread if needed.</span></span> <span data-ttu-id="3472a-137">你必须使用相同的 ID 并定义适当的作用域将对象添加到 `bot` 应用清单。</span><span class="sxs-lookup"><span data-stu-id="3472a-137">You must add the `bot` object to the app manifest using  the same ID and defining the appropriate scopes.</span></span>

## <a name="add-the-action-command-to-your-app-manifest"></a><span data-ttu-id="3472a-138">将操作命令添加到应用清单</span><span class="sxs-lookup"><span data-stu-id="3472a-138">Add the action command to your app manifest</span></span>

<span data-ttu-id="3472a-139">若要将操作命令添加到应用清单，必须将新对象添加到应用清单 `composeExtension` JSON 的顶层。</span><span class="sxs-lookup"><span data-stu-id="3472a-139">To add the action command to the app manifest, you must add a new `composeExtension` object to the top level of the app manifest JSON.</span></span> <span data-ttu-id="3472a-140">为此，可以使用下列方法之一：</span><span class="sxs-lookup"><span data-stu-id="3472a-140">You can use one of the following ways to do so:</span></span>

* [<span data-ttu-id="3472a-141">使用 App Studio 创建操作命令</span><span class="sxs-lookup"><span data-stu-id="3472a-141">Create an action command using App Studio</span></span>](#create-an-action-command-using-app-studio)
* [<span data-ttu-id="3472a-142">手动创建操作命令</span><span class="sxs-lookup"><span data-stu-id="3472a-142">Create an action command manually</span></span>](#create-an-action-command-manually)

### <a name="create-an-action-command-using-app-studio"></a><span data-ttu-id="3472a-143">使用 App Studio 创建操作命令</span><span class="sxs-lookup"><span data-stu-id="3472a-143">Create an action command using App Studio</span></span>

> [!NOTE]
> <span data-ttu-id="3472a-144">创建操作命令的先决条件是，已创建邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="3472a-144">The prerequisite to create an action command is that you have already created a messaging extension.</span></span> <span data-ttu-id="3472a-145">若要了解如何创建邮件扩展，请参阅创建 [邮件扩展](~/messaging-extensions/how-to/create-messaging-extension.md)。</span><span class="sxs-lookup"><span data-stu-id="3472a-145">For information on how to create a messaging extension, see [create a messaging extension](~/messaging-extensions/how-to/create-messaging-extension.md).</span></span>

<span data-ttu-id="3472a-146">**创建操作命令**</span><span class="sxs-lookup"><span data-stu-id="3472a-146">**To create an action command**</span></span>

1. <span data-ttu-id="3472a-147">从 Microsoft Teams 客户端打开 **App Studio，** 然后选择清单 **编辑器** 选项卡。</span><span class="sxs-lookup"><span data-stu-id="3472a-147">Open **App Studio** from the Microsoft Teams client and select the **Manifest editor** tab.</span></span>
1. <span data-ttu-id="3472a-148">如果你已在 **App Studio** 中创建应用包，请从列表中选择它。</span><span class="sxs-lookup"><span data-stu-id="3472a-148">If you already created your app package in **App Studio**, select it from the list.</span></span> <span data-ttu-id="3472a-149">如果尚未创建应用包，请导入现有应用包。</span><span class="sxs-lookup"><span data-stu-id="3472a-149">If you have not created an app package, import an existing one.</span></span>
1. <span data-ttu-id="3472a-150">导入应用包后，在"功能"下 **选择**"消息传递 **扩展"。**</span><span class="sxs-lookup"><span data-stu-id="3472a-150">After importing an app package, select **Messaging extensions** under **Capabilities**.</span></span> <span data-ttu-id="3472a-151">你获得一个弹出窗口来设置邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="3472a-151">You get a pop-up window to set up the messaging extension.</span></span>
1. <span data-ttu-id="3472a-152">选择 **窗口中** 的"设置"，将消息传递扩展包括在你的应用体验中。</span><span class="sxs-lookup"><span data-stu-id="3472a-152">Select **Set up** in the window to include the messaging extension in your app experience.</span></span> <span data-ttu-id="3472a-153">下图显示了消息扩展设置窗口：</span><span class="sxs-lookup"><span data-stu-id="3472a-153">The following image displays the messaging extension set up window:</span></span>

    <img src="~/assets/images/messaging-extension/messaging-extension-set-up.png" alt="messaging extension set up" width="500"/>
    
1. <span data-ttu-id="3472a-154">若要创建消息扩展，你需要一个 Microsoft 注册的自动程序。</span><span class="sxs-lookup"><span data-stu-id="3472a-154">To create a messaging extension, you need a Microsoft registered bot.</span></span> <span data-ttu-id="3472a-155">可以使用现有自动程序或创建新的自动程序。</span><span class="sxs-lookup"><span data-stu-id="3472a-155">You can either use an existing bot or create a new bot.</span></span> <span data-ttu-id="3472a-156">选择 **"创建新自动程序**"选项，为新的自动程序命名，然后选择"创建 **"。**</span><span class="sxs-lookup"><span data-stu-id="3472a-156">Select **Create new bot** option, give a name for the new bot, and select **Create**.</span></span> <span data-ttu-id="3472a-157">下图显示了邮件扩展的自动程序创建：</span><span class="sxs-lookup"><span data-stu-id="3472a-157">The following image displays bot creation for messaging extension:</span></span>

    <img src="~/assets/images/messaging-extension/create-bot-for-messaging-extension.png" alt="create bot for messaging extension" width="500"/>

1. <span data-ttu-id="3472a-158">选择 **"** 邮件扩展 **"** 页的"命令"部分中的"添加"，以包含决定邮件扩展行为的命令。</span><span class="sxs-lookup"><span data-stu-id="3472a-158">Select **Add** in the **Command section** of the messaging extensions page to include the commands which decides the behaviour of messaging extension.</span></span>   
<span data-ttu-id="3472a-159">下图显示了邮件扩展的命令添加：</span><span class="sxs-lookup"><span data-stu-id="3472a-159">The following image displays command addition for messaging extension:</span></span>

   <img src="~/assets/images/messaging-extension/include-command.png" alt="include command" width="500"/>

1. <span data-ttu-id="3472a-160">选择 **"允许用户在 Teams 内触发外部服务中的操作"。**</span><span class="sxs-lookup"><span data-stu-id="3472a-160">Select **Allow users to trigger actions in external services while inside of Teams**.</span></span> <span data-ttu-id="3472a-161">下图显示了操作命令选择：</span><span class="sxs-lookup"><span data-stu-id="3472a-161">The following image displays the action command selection:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-selection.png" alt="action command selection" width="500"/>
    
1. <span data-ttu-id="3472a-162">若要使用一组静态参数来创建任务模块，请选择"为命令定义一组 **静态参数"。**</span><span class="sxs-lookup"><span data-stu-id="3472a-162">To use a static set of parameters to create your task module, select **Define a set of static parameters for the command**.</span></span> 

    <span data-ttu-id="3472a-163">下图显示了操作命令静态参数选择：</span><span class="sxs-lookup"><span data-stu-id="3472a-163">The following image displays the action command static parameter selection:</span></span>

   <img src="~/assets/images/messaging-extension/action-command-static-parameter-selection.png" alt="action command static parameter selection" width="500"/> 
   
    <span data-ttu-id="3472a-164">下图显示了一个静态参数设置示例：</span><span class="sxs-lookup"><span data-stu-id="3472a-164">The following image displays an example static parameter set-up:</span></span> 

   <img src="~/assets/images/messaging-extension/setting-up-of-static-parameter.png" alt="action command static parameter set-up" width="500"/>

    <span data-ttu-id="3472a-165">下图显示了静态参数测试示例：</span><span class="sxs-lookup"><span data-stu-id="3472a-165">The following image displays an example static parameter testing:</span></span>

   <img src="~/assets/images/messaging-extension/static-parameter-testing.png" alt="action command static parameter testing" width="500"/>

1. <span data-ttu-id="3472a-166">若要使用动态参数，请选择"从自动程序提取动态 **参数集"。**</span><span class="sxs-lookup"><span data-stu-id="3472a-166">To use dynamic parameters, select to **Fetch a dynamic set of parameters from your bot**.</span></span> <span data-ttu-id="3472a-167">下图显示了操作命令参数选择：</span><span class="sxs-lookup"><span data-stu-id="3472a-167">The following image displays the action command parameter selection:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-dynamic-parameter-selection.png" alt="action command dynamic parameter selection" width="500"/>
    
1. <span data-ttu-id="3472a-168">添加命令 **ID** 和 **标题**。</span><span class="sxs-lookup"><span data-stu-id="3472a-168">Add a **Command Id** and a **Title**.</span></span>
1. <span data-ttu-id="3472a-169">选择要从其中调用操作命令的位置。</span><span class="sxs-lookup"><span data-stu-id="3472a-169">Select the location from where you want to invoke the action command.</span></span> <span data-ttu-id="3472a-170">下图显示了操作命令调用位置：</span><span class="sxs-lookup"><span data-stu-id="3472a-170">The following image displays the action command invoke location:</span></span>

    <img src="~/assets/images/messaging-extension/action-command-invoke-location.png" alt="action command invoke location" width="500"/>

1. <span data-ttu-id="3472a-171">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="3472a-171">Select **Save**.</span></span>
1. <span data-ttu-id="3472a-172">若要添加更多参数，请选择" **参数"部分** 中的" **添加"** 按钮。</span><span class="sxs-lookup"><span data-stu-id="3472a-172">To add more parameters, select the **Add** button in the **Parameters** section.</span></span>

### <a name="create-an-action-command-manually"></a><span data-ttu-id="3472a-173">手动创建操作命令</span><span class="sxs-lookup"><span data-stu-id="3472a-173">Create an action command manually</span></span>

<span data-ttu-id="3472a-174">若要手动将基于操作的消息扩展命令添加到应用清单，必须将以下参数添加到 `composeExtension.commands` 对象数组：</span><span class="sxs-lookup"><span data-stu-id="3472a-174">To manually add your action-based messaging extension command to your app manifest, you must add the following parameters to the `composeExtension.commands` array of objects:</span></span>

| <span data-ttu-id="3472a-175">属性名称</span><span class="sxs-lookup"><span data-stu-id="3472a-175">Property name</span></span> | <span data-ttu-id="3472a-176">用途</span><span class="sxs-lookup"><span data-stu-id="3472a-176">Purpose</span></span> | <span data-ttu-id="3472a-177">是否必需？</span><span class="sxs-lookup"><span data-stu-id="3472a-177">Required?</span></span> | <span data-ttu-id="3472a-178">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="3472a-178">Minimum manifest version</span></span> |
|---|---|---|---|
| `id` | <span data-ttu-id="3472a-179">此属性是分配给此命令的唯一 ID。</span><span class="sxs-lookup"><span data-stu-id="3472a-179">This property is an unique ID that you assign to this command.</span></span> <span data-ttu-id="3472a-180">用户请求包括此 ID。</span><span class="sxs-lookup"><span data-stu-id="3472a-180">The user request includes this ID.</span></span> | <span data-ttu-id="3472a-181">是</span><span class="sxs-lookup"><span data-stu-id="3472a-181">Yes</span></span> | <span data-ttu-id="3472a-182">1.0</span><span class="sxs-lookup"><span data-stu-id="3472a-182">1.0</span></span> |
| `title` | <span data-ttu-id="3472a-183">此属性是命令名称。</span><span class="sxs-lookup"><span data-stu-id="3472a-183">This property is a command name.</span></span> <span data-ttu-id="3472a-184">此值显示在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="3472a-184">This value appears in the UI.</span></span> | <span data-ttu-id="3472a-185">是</span><span class="sxs-lookup"><span data-stu-id="3472a-185">Yes</span></span> | <span data-ttu-id="3472a-186">1.0</span><span class="sxs-lookup"><span data-stu-id="3472a-186">1.0</span></span> |
| `type` | <span data-ttu-id="3472a-187">此属性必须是 `action` 。</span><span class="sxs-lookup"><span data-stu-id="3472a-187">This property must be an `action`.</span></span> | <span data-ttu-id="3472a-188">不支持</span><span class="sxs-lookup"><span data-stu-id="3472a-188">No</span></span> | <span data-ttu-id="3472a-189">1.4</span><span class="sxs-lookup"><span data-stu-id="3472a-189">1.4</span></span> |
| `fetchTask` | <span data-ttu-id="3472a-190">对于任务模块的自适应卡片或嵌入式 Web 视图，以及参数的静态列表或加载 Web 视图时，此属性 `true` `false` 设置为 `taskInfo` 。</span><span class="sxs-lookup"><span data-stu-id="3472a-190">This property is set to `true` for an adaptive card or embedded web view for your task module, and`false` for a static list of parameters or when loading the web view by a `taskInfo`.</span></span> | <span data-ttu-id="3472a-191">不支持</span><span class="sxs-lookup"><span data-stu-id="3472a-191">No</span></span> | <span data-ttu-id="3472a-192">1.4</span><span class="sxs-lookup"><span data-stu-id="3472a-192">1.4</span></span> |
| `context` | <span data-ttu-id="3472a-193">此属性是一个可选的值数组，用于定义从何处调用消息传递扩展。</span><span class="sxs-lookup"><span data-stu-id="3472a-193">This property is an optional array of values that defines where the messaging extension is invoked from.</span></span> <span data-ttu-id="3472a-194">可取值包括 `message`、`compose` 或 `commandBox`。</span><span class="sxs-lookup"><span data-stu-id="3472a-194">The possible values are `message`, `compose`, or `commandBox`.</span></span> <span data-ttu-id="3472a-195">默认值为 `["compose", "commandBox"]`。</span><span class="sxs-lookup"><span data-stu-id="3472a-195">The default value is `["compose", "commandBox"]`.</span></span> | <span data-ttu-id="3472a-196">不支持</span><span class="sxs-lookup"><span data-stu-id="3472a-196">No</span></span> | <span data-ttu-id="3472a-197">1.5</span><span class="sxs-lookup"><span data-stu-id="3472a-197">1.5</span></span> |

<span data-ttu-id="3472a-198">如果使用参数的静态列表，则还必须添加以下参数：</span><span class="sxs-lookup"><span data-stu-id="3472a-198">If you are using a static list of parameters, you must also add the following parameters:</span></span>

| <span data-ttu-id="3472a-199">属性名称</span><span class="sxs-lookup"><span data-stu-id="3472a-199">Property name</span></span> | <span data-ttu-id="3472a-200">用途</span><span class="sxs-lookup"><span data-stu-id="3472a-200">Purpose</span></span> | <span data-ttu-id="3472a-201">是否必需？</span><span class="sxs-lookup"><span data-stu-id="3472a-201">Is required?</span></span> | <span data-ttu-id="3472a-202">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="3472a-202">Minimum manifest version</span></span> |
|---|---|---|---|
| `parameters` | <span data-ttu-id="3472a-203">此属性描述命令的参数静态列表。</span><span class="sxs-lookup"><span data-stu-id="3472a-203">This property describes the static list of parameters for the command.</span></span> <span data-ttu-id="3472a-204">仅在 为 时 `fetchTask` 使用 `false` 。</span><span class="sxs-lookup"><span data-stu-id="3472a-204">Only use when `fetchTask` is `false`.</span></span> | <span data-ttu-id="3472a-205">不支持</span><span class="sxs-lookup"><span data-stu-id="3472a-205">No</span></span> | <span data-ttu-id="3472a-206">1.0</span><span class="sxs-lookup"><span data-stu-id="3472a-206">1.0</span></span> |
| `parameter.name` | <span data-ttu-id="3472a-207">此属性描述参数的名称。</span><span class="sxs-lookup"><span data-stu-id="3472a-207">This property describes the name of the parameter.</span></span> <span data-ttu-id="3472a-208">这将在用户请求中发送到你的服务。</span><span class="sxs-lookup"><span data-stu-id="3472a-208">This is sent to your service in the user request.</span></span> | <span data-ttu-id="3472a-209">是</span><span class="sxs-lookup"><span data-stu-id="3472a-209">Yes</span></span> | <span data-ttu-id="3472a-210">1.0</span><span class="sxs-lookup"><span data-stu-id="3472a-210">1.0</span></span> |
| `parameter.description` | <span data-ttu-id="3472a-211">此属性描述参数的用途或应提供的值示例。</span><span class="sxs-lookup"><span data-stu-id="3472a-211">This property describes the parameter’s purposes or example of the value that should be provided.</span></span> <span data-ttu-id="3472a-212">此值显示在 UI 中。</span><span class="sxs-lookup"><span data-stu-id="3472a-212">This value appears in the UI.</span></span> | <span data-ttu-id="3472a-213">是</span><span class="sxs-lookup"><span data-stu-id="3472a-213">Yes</span></span> | <span data-ttu-id="3472a-214">1.0</span><span class="sxs-lookup"><span data-stu-id="3472a-214">1.0</span></span> |
| `parameter.title` | <span data-ttu-id="3472a-215">此属性是一个简短的用户友好参数标题或标签。</span><span class="sxs-lookup"><span data-stu-id="3472a-215">This property is a short user-friendly parameter title or label.</span></span> | <span data-ttu-id="3472a-216">是</span><span class="sxs-lookup"><span data-stu-id="3472a-216">Yes</span></span> | <span data-ttu-id="3472a-217">1.0</span><span class="sxs-lookup"><span data-stu-id="3472a-217">1.0</span></span> |
| `parameter.inputType` | <span data-ttu-id="3472a-218">此属性设置为所需的输入类型。</span><span class="sxs-lookup"><span data-stu-id="3472a-218">This property is set to the type of input required.</span></span> <span data-ttu-id="3472a-219">可能的值包括 `text` `textarea` `number` `date` 、、、、、。 `time` `toggle`</span><span class="sxs-lookup"><span data-stu-id="3472a-219">The possible values include `text`, `textarea`, `number`, `date`, `time`, `toggle`.</span></span> <span data-ttu-id="3472a-220">默认值设置为 `text` 。</span><span class="sxs-lookup"><span data-stu-id="3472a-220">The default value is set to `text`.</span></span> | <span data-ttu-id="3472a-221">不支持</span><span class="sxs-lookup"><span data-stu-id="3472a-221">No</span></span> | <span data-ttu-id="3472a-222">1.4</span><span class="sxs-lookup"><span data-stu-id="3472a-222">1.4</span></span> |

<span data-ttu-id="3472a-223">如果你使用的是嵌入式 Web 视图，可以选择添加 对象来获取 Web 视图， `taskInfo` 而无需直接调用机器人。</span><span class="sxs-lookup"><span data-stu-id="3472a-223">If you are using an embedded web view, you can optionally add the `taskInfo` object to fetch your web view without calling your bot directly.</span></span> <span data-ttu-id="3472a-224">如果选择此选项，则其行为类似于使用静态参数列表的行为。</span><span class="sxs-lookup"><span data-stu-id="3472a-224">If you select this option, the behavior is similar to that of using a static list of parameters.</span></span> <span data-ttu-id="3472a-225">因此，与机器人的第一次 [交互是响应任务模块提交操作](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)。</span><span class="sxs-lookup"><span data-stu-id="3472a-225">In that the first interaction with your bot is [responding to the task module submit action](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md).</span></span> <span data-ttu-id="3472a-226">如果使用对象 `taskInfo` ，则必须将 参数 `fetchTask` 设置为 `false` 。</span><span class="sxs-lookup"><span data-stu-id="3472a-226">If you are using a `taskInfo` object, you must set the `fetchTask` parameter to `false`.</span></span>

| <span data-ttu-id="3472a-227">属性名称</span><span class="sxs-lookup"><span data-stu-id="3472a-227">Property name</span></span> | <span data-ttu-id="3472a-228">用途</span><span class="sxs-lookup"><span data-stu-id="3472a-228">Purpose</span></span> | <span data-ttu-id="3472a-229">是否必需？</span><span class="sxs-lookup"><span data-stu-id="3472a-229">Is required?</span></span> | <span data-ttu-id="3472a-230">最低清单版本</span><span class="sxs-lookup"><span data-stu-id="3472a-230">Minimum manifest version</span></span> |
|---|---|---|---|
|`taskInfo`|<span data-ttu-id="3472a-231">指定在使用消息传递扩展命令时要预加载的任务模块。</span><span class="sxs-lookup"><span data-stu-id="3472a-231">Specify the task module to preload when using a messaging extension command.</span></span> | <span data-ttu-id="3472a-232">不支持</span><span class="sxs-lookup"><span data-stu-id="3472a-232">No</span></span> | <span data-ttu-id="3472a-233">1.4</span><span class="sxs-lookup"><span data-stu-id="3472a-233">1.4</span></span> |
|`taskInfo.title`|<span data-ttu-id="3472a-234">初始任务模块标题。</span><span class="sxs-lookup"><span data-stu-id="3472a-234">Initial task module title.</span></span> |<span data-ttu-id="3472a-235">不支持</span><span class="sxs-lookup"><span data-stu-id="3472a-235">No</span></span> | <span data-ttu-id="3472a-236">1.4</span><span class="sxs-lookup"><span data-stu-id="3472a-236">1.4</span></span> |
|`taskInfo.width`|<span data-ttu-id="3472a-237">任务模块宽度，以像素为单位的一个数字或默认布局（如 `large` 、 `medium` 或 `small` ）。</span><span class="sxs-lookup"><span data-stu-id="3472a-237">Task module width, either a number in pixels or default layout such as `large`, `medium`, or `small`.</span></span> |<span data-ttu-id="3472a-238">不支持</span><span class="sxs-lookup"><span data-stu-id="3472a-238">No</span></span> | <span data-ttu-id="3472a-239">1.4</span><span class="sxs-lookup"><span data-stu-id="3472a-239">1.4</span></span> |
|`taskInfo.height`|<span data-ttu-id="3472a-240">任务模块高度，以像素为单位或默认布局（如 、 `large` `medium` 或 `small` ）。</span><span class="sxs-lookup"><span data-stu-id="3472a-240">Task module height, either a number in pixels or default layout such as `large`, `medium`, or `small`.</span></span>|<span data-ttu-id="3472a-241">不支持</span><span class="sxs-lookup"><span data-stu-id="3472a-241">No</span></span> | <span data-ttu-id="3472a-242">1.4</span><span class="sxs-lookup"><span data-stu-id="3472a-242">1.4</span></span> |
|`taskInfo.url`|<span data-ttu-id="3472a-243">初始 Web 视图 URL。</span><span class="sxs-lookup"><span data-stu-id="3472a-243">Initial web view URL.</span></span>|<span data-ttu-id="3472a-244">不支持</span><span class="sxs-lookup"><span data-stu-id="3472a-244">No</span></span> | <span data-ttu-id="3472a-245">1.4</span><span class="sxs-lookup"><span data-stu-id="3472a-245">1.4</span></span> | 

#### <a name="app-manifest-example"></a><span data-ttu-id="3472a-246">应用清单示例</span><span class="sxs-lookup"><span data-stu-id="3472a-246">App manifest example</span></span>

<span data-ttu-id="3472a-247">下一节是定义两个 `composeExtensions` 操作命令的对象的示例。</span><span class="sxs-lookup"><span data-stu-id="3472a-247">The following section is an example of a `composeExtensions` object defining two action commands.</span></span> <span data-ttu-id="3472a-248">这不是完整清单的示例。</span><span class="sxs-lookup"><span data-stu-id="3472a-248">It is not an example of the complete manifest.</span></span> <span data-ttu-id="3472a-249">有关完整的应用清单架构，请参阅 [应用清单架构](~/resources/schema/manifest-schema.md)：</span><span class="sxs-lookup"><span data-stu-id="3472a-249">For the complete app manifest schema, see [app manifest schema](~/resources/schema/manifest-schema.md):</span></span>

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

## <a name="code-sample"></a><span data-ttu-id="3472a-250">代码示例</span><span class="sxs-lookup"><span data-stu-id="3472a-250">Code sample</span></span>

| <span data-ttu-id="3472a-251">示例名称</span><span class="sxs-lookup"><span data-stu-id="3472a-251">Sample Name</span></span>           | <span data-ttu-id="3472a-252">说明</span><span class="sxs-lookup"><span data-stu-id="3472a-252">Description</span></span> | <span data-ttu-id="3472a-253">.NET</span><span class="sxs-lookup"><span data-stu-id="3472a-253">.NET</span></span>    | <span data-ttu-id="3472a-254">Node.js</span><span class="sxs-lookup"><span data-stu-id="3472a-254">Node.js</span></span>   |   
|:---------------------|:--------------|:---------|:--------|
|<span data-ttu-id="3472a-255">Teams 消息传递扩展操作</span><span class="sxs-lookup"><span data-stu-id="3472a-255">Teams messaging extension action</span></span>| <span data-ttu-id="3472a-256">介绍如何定义操作命令、创建任务模块和响应任务模块提交操作。</span><span class="sxs-lookup"><span data-stu-id="3472a-256">Describes how to define action commands, create task module, and  respond to task module submit action.</span></span> |[<span data-ttu-id="3472a-257">View</span><span class="sxs-lookup"><span data-stu-id="3472a-257">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/51.teams-messaging-extensions-action)|[<span data-ttu-id="3472a-258">View</span><span class="sxs-lookup"><span data-stu-id="3472a-258">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/51.teams-messaging-extensions-action) | 
|<span data-ttu-id="3472a-259">Teams 消息传递扩展搜索</span><span class="sxs-lookup"><span data-stu-id="3472a-259">Teams messaging extension search</span></span>   |  <span data-ttu-id="3472a-260">介绍如何定义搜索命令并响应搜索。</span><span class="sxs-lookup"><span data-stu-id="3472a-260">Describes how to define search commands and respond to searches.</span></span>        |[<span data-ttu-id="3472a-261">View</span><span class="sxs-lookup"><span data-stu-id="3472a-261">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/csharp_dotnetcore/50.teams-messaging-extensions-search)|[<span data-ttu-id="3472a-262">View</span><span class="sxs-lookup"><span data-stu-id="3472a-262">View</span></span>](https://github.com/microsoft/BotBuilder-Samples/tree/master/samples/javascript_nodejs/50.teams-messaging-extensions-search)|

## <a name="next-step"></a><span data-ttu-id="3472a-263">后续步骤</span><span class="sxs-lookup"><span data-stu-id="3472a-263">Next step</span></span>

<span data-ttu-id="3472a-264">如果你使用的是自适应卡片或没有对象的嵌入 Web 视图，下一 `taskInfo` 步是：</span><span class="sxs-lookup"><span data-stu-id="3472a-264">If you are using either an Adaptive Card or an embedded web view without a `taskInfo` object, the next step is to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3472a-265">使用任务模块创建和响应</span><span class="sxs-lookup"><span data-stu-id="3472a-265">Create and respond with a task module</span></span>](~/messaging-extensions/how-to/action-commands/create-task-module.md)

<span data-ttu-id="3472a-266">如果要将参数或嵌入的 Web 视图与对象一同使用，下一 `taskInfo` 步是：</span><span class="sxs-lookup"><span data-stu-id="3472a-266">If you are using the parameters or an embedded web view with a `taskInfo` object, the next step is to:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="3472a-267">响应任务模块提交</span><span class="sxs-lookup"><span data-stu-id="3472a-267">Respond to task module submit</span></span>](~/messaging-extensions/how-to/action-commands/respond-to-task-module-submit.md)

