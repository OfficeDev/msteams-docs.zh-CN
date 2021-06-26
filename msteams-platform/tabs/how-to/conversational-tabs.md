---
title: 创建对话选项卡
author: surbhigupta
description: 为频道选项卡创建对话子实体聊天
keywords: Teams 选项卡频道可配置
ms.topic: conceptual
ms.author: lomeybur
ms.openlocfilehash: fbc5e90842c892cfb7e14f845563d7d2ffb397bb
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140262"
---
# <a name="create-conversational-tabs"></a><span data-ttu-id="11c87-104">创建对话选项卡</span><span class="sxs-lookup"><span data-stu-id="11c87-104">Create conversational tabs</span></span>

<span data-ttu-id="11c87-105">会话子实体提供了一种方法，允许用户就选项卡中的子实体（如特定任务、患者和销售机会）展开对话，而不是讨论整个选项卡（也称为实体）。</span><span class="sxs-lookup"><span data-stu-id="11c87-105">Conversational sub-entities provides a way to allow users to have conversations about sub-entities in your tab, such as specific task, patient, and sales opportunity, instead of discussing the entire tab, also known as entity.</span></span> <span data-ttu-id="11c87-106">传统的频道或可配置的选项卡允许用户就选项卡进行对话，但用户需要更集中的对话。</span><span class="sxs-lookup"><span data-stu-id="11c87-106">A traditional channel or configurable tab allows the user to have a conversation about a tab, but the user requires a more focused conversation.</span></span> <span data-ttu-id="11c87-107">如果内容太多，无法进行集中讨论，或者内容随着时间的推移而发生更改，使对话与显示的内容无关，则可能会出现更集中的对话的要求。</span><span class="sxs-lookup"><span data-stu-id="11c87-107">The requirement for a more focused conversation can arise either, if there is too much content to have a centralized discussion or because the content changed over time, making the conversation irrelevant to the content being shown.</span></span> <span data-ttu-id="11c87-108">对话子实体为动态选项卡提供了更加集中的对话体验。</span><span class="sxs-lookup"><span data-stu-id="11c87-108">Conversational sub-entities provides a much more focused conversation experience for dynamic tabs.</span></span>

<span data-ttu-id="11c87-109">对话子实体仅在频道中受支持。</span><span class="sxs-lookup"><span data-stu-id="11c87-109">Conversational sub-entities are only supported in channels.</span></span> <span data-ttu-id="11c87-110">它们可用于从个人选项卡或静态选项卡创建或继续已固定到频道的选项卡中的对话。</span><span class="sxs-lookup"><span data-stu-id="11c87-110">They can be used from a personal or static tab to create or continue conversations in tabs that are already pinned to a channel.</span></span> <span data-ttu-id="11c87-111">如果你想要为用户提供一个位置来查看和访问跨多个渠道发生的对话，静态选项卡非常有用。</span><span class="sxs-lookup"><span data-stu-id="11c87-111">The static tab is useful if you want to provide one location for a user to view and access conversations happening across multiple channels.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="11c87-112">先决条件</span><span class="sxs-lookup"><span data-stu-id="11c87-112">Prerequisites</span></span>

<span data-ttu-id="11c87-113">为了支持对话子实体，您的选项卡 Web 应用程序必须能够在后端数据库中存储子实体与↔之间的映射。</span><span class="sxs-lookup"><span data-stu-id="11c87-113">In order to support conversational sub-entities, your tab web application must have the ability to store a mapping between sub-entities ↔ conversations in a backend database.</span></span> <span data-ttu-id="11c87-114">`conversationId`提供了 ，但您必须存储此内容，Teams `conversationId` 以便用户继续对话。</span><span class="sxs-lookup"><span data-stu-id="11c87-114">The `conversationId` is provided, but you must store that `conversationId` and return it to Teams in order for users to continue the conversation.</span></span>

## <a name="start-a-new-conversation"></a><span data-ttu-id="11c87-115">启动新对话</span><span class="sxs-lookup"><span data-stu-id="11c87-115">Start a new conversation</span></span>

<span data-ttu-id="11c87-116">若要启动新对话，请使用 `openConversation()` 函数。</span><span class="sxs-lookup"><span data-stu-id="11c87-116">To start a new conversation, use the `openConversation()` function.</span></span> <span data-ttu-id="11c87-117">启动和继续对话都由此方法处理。</span><span class="sxs-lookup"><span data-stu-id="11c87-117">Starting and continuing a conversation are all handled by this method.</span></span> <span data-ttu-id="11c87-118">对函数的输入根据要执行的操作而更改。</span><span class="sxs-lookup"><span data-stu-id="11c87-118">The inputs to the function change depending on which action you want to take.</span></span> <span data-ttu-id="11c87-119">从用户的角度来看，这将在屏幕右侧打开对话面板，以启动对话或继续对话。</span><span class="sxs-lookup"><span data-stu-id="11c87-119">From the users perspective, this opens the conversation panel to the right of the screen, either to initiate a conversation or continue a conversation.</span></span>

``` javascript
microsoftTeams.conversations.openConversation(openConversationRequest);
```

<span data-ttu-id="11c87-120">**openConversation** 采用以下输入在频道中启动对话：</span><span class="sxs-lookup"><span data-stu-id="11c87-120">**openConversation** takes the following inputs to start a conversation in a channel:</span></span>

* <span data-ttu-id="11c87-121">**subEntityId**：这是特定子实体的 ID。</span><span class="sxs-lookup"><span data-stu-id="11c87-121">**subEntityId**: This is the ID of your specific sub-entity.</span></span> <span data-ttu-id="11c87-122">例如，task-123。</span><span class="sxs-lookup"><span data-stu-id="11c87-122">For example, task-123.</span></span>
* <span data-ttu-id="11c87-123">**entityId**：这是选项卡实例创建时 ID。</span><span class="sxs-lookup"><span data-stu-id="11c87-123">**entityId**: This is the ID of the tab instance when it was created.</span></span> <span data-ttu-id="11c87-124">ID 必须引用回同一个选项卡实例。</span><span class="sxs-lookup"><span data-stu-id="11c87-124">The ID is important to refer back to the same tab instance.</span></span>
* <span data-ttu-id="11c87-125">**channelId：** 这是选项卡实例所在的通道。</span><span class="sxs-lookup"><span data-stu-id="11c87-125">**channelId**: This is the channel in which the tab instance resides.</span></span>
   > [!NOTE]
   > <span data-ttu-id="11c87-126">**channelId** 对于频道选项卡是可选的。</span><span class="sxs-lookup"><span data-stu-id="11c87-126">The **channelId** is optional for channel tabs.</span></span> <span data-ttu-id="11c87-127">但是，如果你想要保持通道和静态选项卡的实现相同，则建议这样做。</span><span class="sxs-lookup"><span data-stu-id="11c87-127">However, it is recommended if you want to keep your implementation across channel and static tabs the same.</span></span>
* <span data-ttu-id="11c87-128">**title**：这是在聊天面板中向用户显示的标题。</span><span class="sxs-lookup"><span data-stu-id="11c87-128">**title**: This is the title that is shown to the user in the chat panel.</span></span>

<span data-ttu-id="11c87-129">大部分这些值也可从 `getContext` API 中检索。</span><span class="sxs-lookup"><span data-stu-id="11c87-129">Most of these values can also be retrieved from the `getContext` API.</span></span>

```javascript
microsoftTeams.conversations.openConversation({“subEntityId”:”task-1”, “entityId”: “tabInstanceId-1”, “channelId”: ”19:baa6e71f65b948d189bf5c892baa8e5a@thread.skype”, “title”: "Task Title”});
```

<span data-ttu-id="11c87-130">下图显示了对话面板：</span><span class="sxs-lookup"><span data-stu-id="11c87-130">The following image shows the conversation panel:</span></span>

![对话子实体 - 开始对话](~/assets/images/tabs/conversational-subentities/start-conversation.png)

<span data-ttu-id="11c87-132">如果用户启动对话，则侦听该事件的回调以检索和保存 **conversationId 很重要**：</span><span class="sxs-lookup"><span data-stu-id="11c87-132">If the user starts a conversation, it is important to listen for the callback of that event in order to retrieve and save the **conversationId**:</span></span>

```javascript
microsoftTeams.conversations.onStartConversation = (conversationResponse) => {
    // console.log(conversationReponse.conversationId)
};
```

<span data-ttu-id="11c87-133">`conversationResponse`对象包含与已启动的对话有关的信息。</span><span class="sxs-lookup"><span data-stu-id="11c87-133">The `conversationResponse` object contains information related to the conversation that was started.</span></span> <span data-ttu-id="11c87-134">建议您保存此响应对象的所有属性，供以后使用。</span><span class="sxs-lookup"><span data-stu-id="11c87-134">It is recommended that you save all the properties of this response object for later use.</span></span>

## <a name="continue-a-conversation"></a><span data-ttu-id="11c87-135">继续对话</span><span class="sxs-lookup"><span data-stu-id="11c87-135">Continue a conversation</span></span>

<span data-ttu-id="11c87-136">开始对话后，后续调用要求你提供与开始新对话中相同的输入， `openConversation()` 但还包括 [](#start-a-new-conversation) **conversationId**。</span><span class="sxs-lookup"><span data-stu-id="11c87-136">After a conversation starts, subsequent calls to `openConversation()` requires that you also provide the same inputs as in [start a new conversation](#start-a-new-conversation), but also include the **conversationId**.</span></span> <span data-ttu-id="11c87-137">将在视图中为具有相应对话的用户打开对话面板。</span><span class="sxs-lookup"><span data-stu-id="11c87-137">The conversation panel opens for the user with the appropriate conversation in view.</span></span> <span data-ttu-id="11c87-138">用户能够实时查看新邮件或传入邮件。</span><span class="sxs-lookup"><span data-stu-id="11c87-138">Users are able to see new or incoming messages in real-time.</span></span>

<span data-ttu-id="11c87-139">下图显示了包含相应对话的对话面板：</span><span class="sxs-lookup"><span data-stu-id="11c87-139">The following image shows the conversation panel with the appropriate conversation:</span></span>

![对话子实体 - 继续对话](~/assets/images/tabs/conversational-subentities/continue-conversation.png)

## <a name="enhance-a-conversation"></a><span data-ttu-id="11c87-141">增强对话</span><span class="sxs-lookup"><span data-stu-id="11c87-141">Enhance a conversation</span></span>

<span data-ttu-id="11c87-142">您的选项卡包含到子实体的深层链接 [，这一点很重要](~/concepts/build-and-test/deep-links.md)。</span><span class="sxs-lookup"><span data-stu-id="11c87-142">It is important that your tab includes [deeplinks to your sub-entity](~/concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="11c87-143">例如，用户从频道对话中选择选项卡深度链接。</span><span class="sxs-lookup"><span data-stu-id="11c87-143">For example, user selecting the tab chiclet deeplink from the channel conversation.</span></span> <span data-ttu-id="11c87-144">预期行为是接收深度链接，打开该子实体，然后打开该子实体的对话面板。</span><span class="sxs-lookup"><span data-stu-id="11c87-144">The expected behavior is to receive the deeplink, open that sub-entity, and then open the conversation panel for that sub-entity.</span></span>

<span data-ttu-id="11c87-145">若要从个人选项卡或静态选项卡支持对话子实体，则不需要在实现中更改任何内容。</span><span class="sxs-lookup"><span data-stu-id="11c87-145">To support conversational sub-entities from your personal or static tab, you do not have to change anything in your implementation.</span></span> <span data-ttu-id="11c87-146">我们仅支持从已固定的频道选项卡开始或继续对话。</span><span class="sxs-lookup"><span data-stu-id="11c87-146">We only support starting or continuing conversations from channel tabs that are already pinned.</span></span> <span data-ttu-id="11c87-147">通过支持静态选项卡，您可以为用户提供一个位置来与您的所有子实体进行交互。</span><span class="sxs-lookup"><span data-stu-id="11c87-147">Supporting static tabs allows you to provide a single location for your users to interact with all your sub-entities.</span></span> <span data-ttu-id="11c87-148">在静态选项卡中打开对话视图时，在最初在频道中创建选项卡时，保存 、 和 具有正确的属性，这一点 `subEntityId` `entityId` `channelId` 很重要。</span><span class="sxs-lookup"><span data-stu-id="11c87-148">It is important that you save the `subEntityId`, `entityId`, and `channelId` when your tab is originally created in a channel to have the right properties when opening the conversation view in a static tab.</span></span>

## <a name="close-a-conversation"></a><span data-ttu-id="11c87-149">关闭对话</span><span class="sxs-lookup"><span data-stu-id="11c87-149">Close a conversation</span></span>

<span data-ttu-id="11c87-150">可以通过调用 函数手动关闭对话 `closeConversation()` 视图。</span><span class="sxs-lookup"><span data-stu-id="11c87-150">You can manually close the conversation view by calling the `closeConversation()` function.</span></span>

```javascript
microsoftTeams.conversations.closeConversation();
```

<span data-ttu-id="11c87-151">还可以在对话视图被用户关闭时侦听事件。</span><span class="sxs-lookup"><span data-stu-id="11c87-151">You can also listen for an event when the conversation view is closed by a user.</span></span>

```javascript
microsoftTeams.conversations.onCloseConversation = (conversationResponse) => {
    // console.log(conversationResponse)
};
```

## <a name="see-also"></a><span data-ttu-id="11c87-152">另请参阅</span><span class="sxs-lookup"><span data-stu-id="11c87-152">See also</span></span>

* [<span data-ttu-id="11c87-153">Teams选项卡</span><span class="sxs-lookup"><span data-stu-id="11c87-153">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="11c87-154">先决条件</span><span class="sxs-lookup"><span data-stu-id="11c87-154">Prerequisites</span></span>](~/tabs/how-to/tab-requirements.md)
* [<span data-ttu-id="11c87-155">创建个人选项卡</span><span class="sxs-lookup"><span data-stu-id="11c87-155">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="11c87-156">创建频道或组选项卡</span><span class="sxs-lookup"><span data-stu-id="11c87-156">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="11c87-157">创建内容页</span><span class="sxs-lookup"><span data-stu-id="11c87-157">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)
* [<span data-ttu-id="11c87-158">创建配置页</span><span class="sxs-lookup"><span data-stu-id="11c87-158">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
* [<span data-ttu-id="11c87-159">为选项卡创建删除页</span><span class="sxs-lookup"><span data-stu-id="11c87-159">Create a removal page for your tab</span></span>](~/tabs/how-to/create-tab-pages/removal-page.md)
* [<span data-ttu-id="11c87-160">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="11c87-160">Tabs on mobile</span></span>](~/tabs/design/tabs-mobile.md)
* [<span data-ttu-id="11c87-161">获取选项卡的上下文</span><span class="sxs-lookup"><span data-stu-id="11c87-161">Get context for your tab</span></span>](~/tabs/how-to/access-teams-context.md)
* [<span data-ttu-id="11c87-162">具有自适应卡片的生成选项卡</span><span class="sxs-lookup"><span data-stu-id="11c87-162">Build tabs with Adaptive Cards</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)
* [<span data-ttu-id="11c87-163">选项卡链接展开和阶段视图</span><span class="sxs-lookup"><span data-stu-id="11c87-163">Tabs link unfurling and Stage View</span></span>](~/tabs/tabs-link-unfurling.md)

## <a name="next-step"></a><span data-ttu-id="11c87-164">后续步骤</span><span class="sxs-lookup"><span data-stu-id="11c87-164">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="11c87-165">选项卡边距更改</span><span class="sxs-lookup"><span data-stu-id="11c87-165">Tab margin changes</span></span>](~/resources/removing-tab-margins.md)