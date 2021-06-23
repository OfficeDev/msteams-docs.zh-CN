---
title: 创建对话选项卡
author: surbhigupta
description: 为频道选项卡创建对话子实体聊天
keywords: Teams 选项卡频道可配置
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: 343cbe26ded2792489640ae3d86ec94c7c6db72b
ms.sourcegitcommit: 623d81eb079d1842813265746a5fe0fe6311b196
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/22/2021
ms.locfileid: "53069232"
---
# <a name="create-conversational-tabs"></a><span data-ttu-id="c1cc9-104">创建对话选项卡</span><span class="sxs-lookup"><span data-stu-id="c1cc9-104">Create conversational tabs</span></span>

<span data-ttu-id="c1cc9-105">会话子实体提供了一种方法，允许用户就选项卡中的子实体（如特定任务、患者和销售机会）展开对话，而不是讨论整个选项卡（也称为实体）。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-105">Conversational sub-entities provides a way to allow users to have conversations about sub-entities in your tab, such as specific task, patient, and sales opportunity, instead of discussing the entire tab, also known as entity.</span></span> <span data-ttu-id="c1cc9-106">传统的频道或可配置的选项卡允许用户就选项卡进行对话，但用户可能需要更集中的对话。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-106">A traditional channel or configurable tab allows the user to have a conversation about a tab, but the user may want a more focused conversation.</span></span> <span data-ttu-id="c1cc9-107">如果太多内容无法集中讨论或内容随着时间的推移而发生更改，则可能出现更集中的对话的要求，使对话与显示的内容无关。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-107">The requirement for a more focused conversation can arise either, if there is too much content to have a centralized discussion or the content changed over time, making the conversation irrelevant to the content being shown.</span></span> <span data-ttu-id="c1cc9-108">对话子实体为动态选项卡提供了更加集中的对话体验。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-108">Conversational sub-entities provides a much more focused conversation experience for dynamic tabs.</span></span>

<span data-ttu-id="c1cc9-109">对话子实体仅在频道中受支持。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-109">Conversational sub-entities are only supported in channels.</span></span> <span data-ttu-id="c1cc9-110">但是，它们可用于从个人选项卡或静态选项卡创建或继续已固定到频道的选项卡中的对话。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-110">However, they can be used from a personal or static tab to create or continue conversations in tabs that are *already* pinned to a channel.</span></span> <span data-ttu-id="c1cc9-111">如果你想要为用户提供一个位置来查看和访问跨多个渠道发生的对话，静态选项卡将非常有用。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-111">The static tab is useful if you wish to provide one location for a user to view and access conversations happening across multiple channels.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c1cc9-112">先决条件</span><span class="sxs-lookup"><span data-stu-id="c1cc9-112">Prerequisites</span></span>

<span data-ttu-id="c1cc9-113">为了支持对话子实体，您的选项卡 Web 应用程序必须能够在后端数据库中存储子实体与↔之间的映射。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-113">In order to support conversational sub-entities, your tab web application must have the ability to store a mapping between sub-entities ↔ conversations in a backend database.</span></span> <span data-ttu-id="c1cc9-114">我们将为您提供 ，但您有责任存储此内容，Teams以便用户 `conversationId` `conversationId` 继续对话。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-114">We will provide you with the `conversationId`, but it will be your responsibility to store that `conversationId` and return it to Teams in order for users to continue the conversation.</span></span>

## <a name="start-a-new-conversation"></a><span data-ttu-id="c1cc9-115">启动新对话</span><span class="sxs-lookup"><span data-stu-id="c1cc9-115">Start a new conversation</span></span>

<span data-ttu-id="c1cc9-116">若要启动新对话，请使用 `openConversation()` 函数。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-116">To start a new conversation, you use the `openConversation()` function.</span></span> <span data-ttu-id="c1cc9-117">启动和继续对话都由此方法处理，但是，对函数的输入将根据您要执行的操作而更改。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-117">Starting and continuing a conversation are all handled by this method, however, the inputs to the function change depending on which action you want to take.</span></span> <span data-ttu-id="c1cc9-118">从用户的角度来看，这将在屏幕右侧打开对话面板，以启动对话或继续对话。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-118">From the users perspective, this opens the conversation panel to the right of the screen, either to initiate a conversation or continue a conversation.</span></span>

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

<span data-ttu-id="c1cc9-119">**openConversation** 采用以下输入在频道中启动对话：</span><span class="sxs-lookup"><span data-stu-id="c1cc9-119">**openConversation** takes the following inputs to start a conversation in a channel:</span></span>

* <span data-ttu-id="c1cc9-120">**subEntityId**：这是特定子实体的 ID。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-120">**subEntityId**: This is the ID of your specific sub-entity.</span></span> <span data-ttu-id="c1cc9-121">例如，task-123。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-121">For example, task-123.</span></span>
* <span data-ttu-id="c1cc9-122">**entityId**：这是选项卡实例创建时 ID。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-122">**entityId**: This is the ID of the tab instance when it was created.</span></span> <span data-ttu-id="c1cc9-123">ID 必须引用回同一个选项卡实例。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-123">The ID is important to refer back to the same tab instance.</span></span>
* <span data-ttu-id="c1cc9-124">**channelId：** 这是选项卡实例所在的通道。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-124">**channelId**: This is the channel in which the tab instance resides.</span></span>
   > [!NOTE]
   > <span data-ttu-id="c1cc9-125">**channelId** 对于频道选项卡是可选的。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-125">The **channelId** is optional for channel tabs.</span></span> <span data-ttu-id="c1cc9-126">但是，如果你想要保持通道和静态选项卡的实现相同，则建议这样做。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-126">However, it is recommended if you wish to keep your implementation across channel and static tabs the same.</span></span>
* <span data-ttu-id="c1cc9-127">**title**：这是在聊天面板中向用户显示的标题。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-127">**title**: This is the title that is shown to the user in the chat panel.</span></span>

<span data-ttu-id="c1cc9-128">大部分这些值也可从 `getContext` API 中检索。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-128">Most of these values can also be retrieved from the `getContext` API.</span></span>

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

<span data-ttu-id="c1cc9-129">这将打开对话面板。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-129">This will open the conversation panel.</span></span>

![Conversationl 子实体 - 开始对话](~/assets/images/tabs/conversational-subentities/start-conversation.png)

<span data-ttu-id="c1cc9-131">如果用户启动对话，则侦听该事件的回调以检索和保存 **conversationId 很重要**：</span><span class="sxs-lookup"><span data-stu-id="c1cc9-131">If the user starts a conversation, it’s important to listen for the callback of that event in order to retrieve and save the **conversationId**:</span></span>

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

<span data-ttu-id="c1cc9-132">`conversationReponse`对象包含与刚刚开始的对话有关的信息。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-132">The `conversationReponse` object contains information related to the conversation that was just started.</span></span> <span data-ttu-id="c1cc9-133">我们建议您保存此响应对象的所有属性，以便稍后重复使用。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-133">We recommend you save all the properties of this response object for reuse later.</span></span>

## <a name="continue-a-conversation"></a><span data-ttu-id="c1cc9-134">继续对话</span><span class="sxs-lookup"><span data-stu-id="c1cc9-134">Continue a conversation</span></span>

<span data-ttu-id="c1cc9-135">开始对话后，后续调用要求你提供与启动新频道选项卡对话中相同的输入，但 `openConversation()` 还包括 **conversationId** [](#Starting a new channel tab conversation)。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-135">After a conversation starts, subsequent calls to `openConversation()` requires that you also provide the same inputs as in [Starting a new channel tab conversation](#Starting a new channel tab conversation), but also include the **conversationId**.</span></span> <span data-ttu-id="c1cc9-136">将在视图中为具有相应对话的用户打开对话面板。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-136">The conversation panel opens for the user with the appropriate conversation in view.</span></span> <span data-ttu-id="c1cc9-137">用户能够实时查看新邮件或传入邮件。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-137">Users are able to see new or incoming messages in real-time.</span></span>

![Conversationl 子实体 - 继续对话](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a><span data-ttu-id="c1cc9-139">增强对话</span><span class="sxs-lookup"><span data-stu-id="c1cc9-139">Enhance a conversation</span></span>

<span data-ttu-id="c1cc9-140">最后，你的选项卡使用到子实体的深层链接 [，这一点很重要](~/concepts/build-and-test/deep-links.md)。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-140">Finally, it’s important that your tab consumes [deeplinks to your sub-entity](~/concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="c1cc9-141">例如，用户单击频道对话中的选项卡链接深度链接。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-141">For example, user clicking the tab chiclet deeplink from the channel conversation.</span></span> <span data-ttu-id="c1cc9-142">预期行为是接收深度链接，打开该子实体，然后打开该特定子实体的对话面板。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-142">The expected behavior is for you to receive the deeplink, open that sub-entity, and then open the conversation panel for that specific sub-entity.</span></span>

<span data-ttu-id="c1cc9-143">若要从个人选项卡或静态选项卡支持对话子实体，则不需要更改有关实现的任何内容。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-143">To support conversational sub-entities from your personal or static tab, you do not have to change anything about your implementation.</span></span> <span data-ttu-id="c1cc9-144">我们仅支持从已固定的频道选项卡开始或继续对话。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-144">We only support starting or continuing conversations from channel tabs that are already pinned.</span></span> <span data-ttu-id="c1cc9-145">通过支持静态选项卡，您可以为用户提供一个位置来与您的所有子实体进行交互。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-145">Supporting static tabs allow you to provide a single location for your users to interact with all your sub-entities.</span></span> <span data-ttu-id="c1cc9-146">但是，在最初在频道中创建选项卡时，保存 、和 非常重要，这样，在静态选项卡中打开对话视图时，您才能拥有 `subEntityId` `entityId` `channelId` 正确的属性。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-146">It is, however, important that you save the `subEntityId`, `entityId`, and `channelId` when your tab is originally created in a channel in order for you to have the right properties when opening the conversation view in a static tab.</span></span>

## <a name="close-a-conversation"></a><span data-ttu-id="c1cc9-147">关闭对话</span><span class="sxs-lookup"><span data-stu-id="c1cc9-147">Close a conversation</span></span>

<span data-ttu-id="c1cc9-148">可以通过调用 函数手动关闭对话 `closeConversation()` 视图。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-148">You can manually close the conversation view by calling the `closeConversation()` function.</span></span>

```javascript
microsoftTeams.conversations.closeConversation();
```

<span data-ttu-id="c1cc9-149">还可以在对话视图被用户关闭时侦听事件。</span><span class="sxs-lookup"><span data-stu-id="c1cc9-149">You can also listen for an event when the conversation view is closed by a user.</span></span>

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```
