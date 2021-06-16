---
title: 创建深层链接
description: 介绍深层链接以及如何在应用中使用它们
ms.topic: how-to
localization_priority: Normal
keywords: 团队深层链接深度链接
ms.openlocfilehash: 07eb03f2e9686c26a917ab1f2d72fc0668e59107
ms.sourcegitcommit: 9f499908437655d6ebdc6c4b3c3603ee220315b7
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/15/2021
ms.locfileid: "52949677"
---
# <a name="create-deep-links"></a><span data-ttu-id="2ae9f-104">创建深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-104">Create deep links</span></span> 

<span data-ttu-id="2ae9f-105">您可以创建指向网站内的信息和功能Teams。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-105">You can create links to information and features within Teams.</span></span> <span data-ttu-id="2ae9f-106">创建深层链接很有用的方案如下所示：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-106">The scenarios where creating deep links are useful are as follows:</span></span>

* <span data-ttu-id="2ae9f-107">将用户导航到应用选项卡之一中的内容。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-107">Navigating the user to the content within one of your app's tabs.</span></span> <span data-ttu-id="2ae9f-108">例如，你的应用可以有一个自动程序，用于向用户发送重要活动通知消息。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-108">For instance, your app can have a bot that sends messages notifying the user of an important activity.</span></span> <span data-ttu-id="2ae9f-109">当用户点击通知时，深层链接将导航到选项卡，以便用户可以查看有关活动的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-109">When the user taps on the notification, the deep link navigates to the tab so that the user can view more details about the activity.</span></span>
* <span data-ttu-id="2ae9f-110">你的应用通过使用所需参数预先填充深层链接来自动执行或简化某些用户任务，例如创建聊天或安排会议。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-110">Your app automates or simplifies certain user tasks, such as creating a chat or scheduling a meeting, by pre populating the deep links with required parameters.</span></span> <span data-ttu-id="2ae9f-111">这样可以避免用户手动输入信息。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-111">This avoids the need for users to manually enter information.</span></span>

> [!NOTE]
>
> <span data-ttu-id="2ae9f-112">深层链接在导航到内容之前先启动浏览器。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-112">A deeplink launches the browser first before navigating to content.</span></span> <span data-ttu-id="2ae9f-113">深入链接对实体Teams行为如下：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-113">The behaviour of deep links on Teams entities are as follows:</span></span>
>
> <span data-ttu-id="2ae9f-114">**Tab**：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-114">**Tab**:</span></span>  
> <span data-ttu-id="2ae9f-115">✔直接导航到深度链接 URL。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-115">✔ Directly navigates to the deeplink url.</span></span>
>
> <span data-ttu-id="2ae9f-116">**Bot**：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-116">**Bot**:</span></span>  
> <span data-ttu-id="2ae9f-117">✔正文中打开 Deeplink：首先在浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-117">✔ Deeplink in card body: Opens in browser first.</span></span>  
> <span data-ttu-id="2ae9f-118">✔卡片中添加到 OpenURL 操作中的 Deeplink：直接导航到 deeplink url。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-118">✔ Deeplink added to OpenURL action in Adaptive Card: Directly navigates to the deeplink url.</span></span>  
> <span data-ttu-id="2ae9f-119">✔卡片中的超链接标记文本：首先在浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-119">✔ Hyperlink markdown text in the card: Opens in browser first.</span></span>  
>
> <span data-ttu-id="2ae9f-120">**聊天**：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-120">**Chat**:</span></span>  
> <span data-ttu-id="2ae9f-121">✔文本消息超链接标记：直接导航到深层链接 URL。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-121">✔ Text message hyperlink markdown: Directly navigates to deeplink url.</span></span>  
> <span data-ttu-id="2ae9f-122">✔常规聊天对话中粘贴的链接：直接导航到深度链接 URL。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-122">✔ Link pasted in general chat conversation: Directly navigates to deeplink url.</span></span>

## <a name="deep-linking-to-your-tab"></a><span data-ttu-id="2ae9f-123">到选项卡的深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-123">Deep linking to your tab</span></span>

<span data-ttu-id="2ae9f-124">可以创建指向网站中的实体的深层Teams。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-124">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="2ae9f-125">这用于创建导航到选项卡中的内容和信息的链接。例如，如果选项卡包含任务列表，工作组成员可以创建并共享指向单个任务的链接。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-125">This is used to create links that navigate to content and information within your tab. For example, if your tab contains a task list, team members can create and share links to individual tasks.</span></span> <span data-ttu-id="2ae9f-126">选择该链接时，它将导航到以特定项目为焦点的选项卡。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-126">When you select the link, it navigates to your tab which focuses on the specific item.</span></span> <span data-ttu-id="2ae9f-127">若要实现此目标，你可以以 **最适合** 你的 UI 的任何方式向每个项目添加一个复制链接操作。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-127">To implement this, you add a **copy link** action to each item, in whatever way best suits your UI.</span></span> <span data-ttu-id="2ae9f-128">当用户执行该操作时，调用 以显示一个对话框，其中包含用户可 `shareDeepLink()` 复制到剪贴板的链接。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-128">When the user takes this action, you call `shareDeepLink()` to display a dialog box containing a link that the user can copy to the clipboard.</span></span> <span data-ttu-id="2ae9f-129">进行此调用时，还会传递项目的 ID，在单击链接并重新加载选项卡时，会返回[](~/tabs/how-to/access-teams-context.md)上下文 ID。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-129">When you make this call, you also pass an ID for your item, which you get back in the [context](~/tabs/how-to/access-teams-context.md) when the link is followed and your tab is reloaded.</span></span>

<span data-ttu-id="2ae9f-130">或者，您也可以使用本主题稍后指定的格式以编程方式生成深层链接。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-130">Alternatively, you can also generate deep links programmatically, using the format specified later in this topic.</span></span> <span data-ttu-id="2ae9f-131">可以在机器人 [和连接器消息](~/bots/what-are-bots.md) 中 [使用](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) 深层链接，以通知用户选项卡或其中项目的更改。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-131">You can use deep links in [bot](~/bots/what-are-bots.md) and [connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) messages that inform users about changes to your tab, or to items within it.</span></span>

> [!NOTE]
> <span data-ttu-id="2ae9f-132">此深层链接不同于"复制到选项卡"菜单项所提供的链接，而"复制到选项卡"菜单项仅生成指向此选项卡的深层链接。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-132">This deep link is different from the links provided by the **Copy link to tab** menu item, which just generates a deep link that points to this tab.</span></span>

>[!NOTE]
> <span data-ttu-id="2ae9f-133">目前，shareDeepLink 在移动平台上不起作用。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-133">Currently, shareDeepLink does not work on mobile platforms.</span></span>

### <a name="show-a-deep-link-to-an-item-within-your-tab"></a><span data-ttu-id="2ae9f-134">显示指向选项卡内某个项目的深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-134">Show a deep link to an item within your tab</span></span>

<span data-ttu-id="2ae9f-135">若要显示包含指向选项卡内某个项目的深层链接的对话框，请调用 `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })` 。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-135">To show a dialog box that contains a deep link to an item within your tab, call `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`.</span></span>

<span data-ttu-id="2ae9f-136">提供以下字段：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-136">Provide the following fields:</span></span>

* <span data-ttu-id="2ae9f-137">`subEntityId`：要深入链接的选项卡内项目的唯一标识符。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-137">`subEntityId`: A unique identifier for the item within your tab to which you are deep linking.</span></span>
* <span data-ttu-id="2ae9f-138">`subEntityLabel`：用于显示深层链接的项的标签。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-138">`subEntityLabel`: A label for the item to use for displaying the deep link.</span></span>
* <span data-ttu-id="2ae9f-139">`subEntityWebUrl`：在客户端不支持呈现选项卡时，使用带回退 URL 的可选字段。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-139">`subEntityWebUrl`: An optional field with a fallback URL to use if the client does not support rendering the tab.</span></span>

### <a name="generate-a-deep-link-to-your-tab"></a><span data-ttu-id="2ae9f-140">生成指向选项卡的深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-140">Generate a deep link to your tab</span></span>

> [!NOTE]
> <span data-ttu-id="2ae9f-141">个人选项卡具有 `personal` 范围，而频道和组选项卡使用 `team` 或 `group` 作用域。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-141">Personal tabs have a `personal` scope, while channel and group tabs use `team` or `group` scopes.</span></span> <span data-ttu-id="2ae9f-142">这两个选项卡类型的语法略有不同，因为只有可配置的选项卡具有与其 `channel` 上下文对象关联的属性。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-142">The two tab types have a slightly different syntax since only the configurable tab has a `channel` property associated with its context object.</span></span> <span data-ttu-id="2ae9f-143">有关 [选项卡](~/resources/schema/manifest-schema.md) 作用域详细信息，请参阅清单参考。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-143">See the [manifest](~/resources/schema/manifest-schema.md) reference for more information on tab scopes.</span></span>

> [!NOTE]
> <span data-ttu-id="2ae9f-144">只有在使用 v0.4 或更高版本库配置了选项卡，并且具有实体 ID 时，深度链接才能正常工作。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-144">Deep links work properly only if the tab was configured using the v0.4 or later library and because of that has an entity ID.</span></span> <span data-ttu-id="2ae9f-145">指向没有实体 ID 的选项卡的深层链接仍导航到选项卡，但无法向选项卡提供子实体 ID。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-145">Deep links to tabs without entity IDs still navigate to the tab but cannot provide the sub entity ID to the tab.</span></span>

<span data-ttu-id="2ae9f-146">对可以在机器人、连接器或邮件扩展卡中使用的深层链接使用以下格式：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-146">Use the following format for a deep link that you can use in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> <span data-ttu-id="2ae9f-147">如果机器人发送包含深层链接的消息，则当用户选择链接时将打开 `TextBlock` 一个新的浏览器选项卡。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-147">If the bot sends a message containing a `TextBlock` with a deep link, then a new browser tab is opened when the user selects the link.</span></span> <span data-ttu-id="2ae9f-148">这发生在 Chrome 和 Microsoft Teams 桌面应用中，这两者均在 Linux 上运行。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-148">This happens in Chrome and in the Microsoft Teams desktop app, both running on Linux.</span></span>
> <span data-ttu-id="2ae9f-149">如果自动程序将同一深层链接 URL 发送到 ，则当用户选择链接时，Teams当前浏览器选项卡中将打开"自动 `Action.OpenUrl` 链接"选项卡。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-149">If the bot sends the same deep link URL into an `Action.OpenUrl`, then the Teams tab is opened in the current browser tab when the user selects the link.</span></span> <span data-ttu-id="2ae9f-150">未打开新的浏览器选项卡。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-150">A new browser tab is not opened.</span></span>

<span data-ttu-id="2ae9f-151">查询参数包括：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-151">The query parameters are:</span></span>

| <span data-ttu-id="2ae9f-152">参数名称</span><span class="sxs-lookup"><span data-stu-id="2ae9f-152">Parameter name</span></span> | <span data-ttu-id="2ae9f-153">说明</span><span class="sxs-lookup"><span data-stu-id="2ae9f-153">Description</span></span> | <span data-ttu-id="2ae9f-154">示例</span><span class="sxs-lookup"><span data-stu-id="2ae9f-154">Example</span></span> |
|:------------|:--------------|:---------------------|
| `appId`&emsp; | <span data-ttu-id="2ae9f-155">清单中的 ID。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-155">The ID from your manifest.</span></span> |<span data-ttu-id="2ae9f-156">fe4a8eba-2a31-4737-8e33-e5fae6fee194</span><span class="sxs-lookup"><span data-stu-id="2ae9f-156">fe4a8eba-2a31-4737-8e33-e5fae6fee194</span></span>|
| `entityId`&emsp; | <span data-ttu-id="2ae9f-157">选项卡中项的 ID，在配置选项卡 [时提供](~/tabs/how-to/create-tab-pages/configuration-page.md)。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-157">The ID for the item in the tab, which you provided when [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md).</span></span>|<span data-ttu-id="2ae9f-158">Tasklist123</span><span class="sxs-lookup"><span data-stu-id="2ae9f-158">Tasklist123</span></span>|
| <span data-ttu-id="2ae9f-159">`entityWebUrl` 或 `subEntityWebUrl`&emsp;</span><span class="sxs-lookup"><span data-stu-id="2ae9f-159">`entityWebUrl` or `subEntityWebUrl`&emsp;</span></span> | <span data-ttu-id="2ae9f-160">在客户端不支持呈现选项卡时，使用带回退 URL 的可选字段。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-160">An optional field with a fallback URL to use if the client does not support rendering the tab.</span></span> | <span data-ttu-id="2ae9f-161">`https://tasklist.example.com/123` 或 `https://tasklist.example.com/list123/task456`</span><span class="sxs-lookup"><span data-stu-id="2ae9f-161">`https://tasklist.example.com/123` or `https://tasklist.example.com/list123/task456`</span></span> |
| <span data-ttu-id="2ae9f-162">`entityLabel` 或 `subEntityLabel`&emsp;</span><span class="sxs-lookup"><span data-stu-id="2ae9f-162">`entityLabel` or `subEntityLabel`&emsp;</span></span> | <span data-ttu-id="2ae9f-163">选项卡中项的标签，用于显示深层链接时。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-163">A label for the item in your tab, to use when displaying the deep link.</span></span> | <span data-ttu-id="2ae9f-164">任务列表 123 或"任务 456</span><span class="sxs-lookup"><span data-stu-id="2ae9f-164">Task List 123 or "Task 456</span></span> |
| <span data-ttu-id="2ae9f-165">`context`&emsp;</span><span class="sxs-lookup"><span data-stu-id="2ae9f-165">`context`&emsp;</span></span> </br></br>* `subEntityId`&emsp;</br></br> * `channelId`&emsp;| <span data-ttu-id="2ae9f-166">包含以下字段的 JSON 对象：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-166">A JSON object containing the following fields:</span></span></br></br> <span data-ttu-id="2ae9f-167">\* 选项卡内项的 ID。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-167">\* An ID for the item within the tab.</span></span> </br></br> <span data-ttu-id="2ae9f-168">\* Microsoft Teams上下文提供的信息通道[ID。](~/tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="2ae9f-168">\*  The Microsoft Teams channel ID that is available from the tab [context](~/tabs/how-to/access-teams-context.md).</span></span> | 
| `subEntityId`&emsp; | <span data-ttu-id="2ae9f-169">选项卡内项的 ID。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-169">An ID for the item within the tab.</span></span> |<span data-ttu-id="2ae9f-170">Task456</span><span class="sxs-lookup"><span data-stu-id="2ae9f-170">Task456</span></span> |
| `channelId`&emsp; | <span data-ttu-id="2ae9f-171">选项卡Microsoft Teams中提供的信息通道[ID。](~/tabs/how-to/access-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="2ae9f-171">The Microsoft Teams channel ID that is available from the tab [context](~/tabs/how-to/access-teams-context.md).</span></span> <span data-ttu-id="2ae9f-172">此属性仅在具有团队作用域的可配置选项卡 **中可用**。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-172">This property is only available in configurable tabs with a scope of **team**.</span></span> <span data-ttu-id="2ae9f-173">它在静态选项卡中不可用，静态选项卡具有个人 **作用域**。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-173">It is not available in static tabs, which have a scope of **personal**.</span></span>| <span data-ttu-id="2ae9f-174">19：cbe3683f25094106b826c9cada3afbe0@thread.skype</span><span class="sxs-lookup"><span data-stu-id="2ae9f-174">19:cbe3683f25094106b826c9cada3afbe0@thread.skype</span></span> |

<span data-ttu-id="2ae9f-175">示例：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-175">Examples:</span></span>

* <span data-ttu-id="2ae9f-176">链接到可配置的选项卡本身： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="2ae9f-176">Link to a configurable tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="2ae9f-177">链接到"可配置"选项卡内的任务项： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="2ae9f-177">Link to a task item within the configurable tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="2ae9f-178">链接到静态选项卡本身： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span><span class="sxs-lookup"><span data-stu-id="2ae9f-178">Link to a static tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span></span>
* <span data-ttu-id="2ae9f-179">链接到静态选项卡内的任务项： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span><span class="sxs-lookup"><span data-stu-id="2ae9f-179">Link to a task item within the static tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="2ae9f-180">确保所有查询参数都经过正确 URI 编码。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-180">Ensure that all query parameters are properly URI encoded.</span></span> <span data-ttu-id="2ae9f-181">您必须使用上一个示例遵循之前的示例：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-181">You must follow the preceeding examples using the last example:</span></span>

> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consume-a-deep-link-from-a-tab"></a><span data-ttu-id="2ae9f-182">从选项卡使用深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-182">Consume a deep link from a tab</span></span>

<span data-ttu-id="2ae9f-183">导航到深层链接时，Microsoft Teams导航到选项卡，并通过 Microsoft Teams JavaScript 库提供一种机制，以检索子实体 ID（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-183">When navigating to a deep link, Microsoft Teams simply navigates to the tab and provides a mechanism through the Microsoft Teams JavaScript library to retrieve the sub-entity ID if it exists.</span></span>

<span data-ttu-id="2ae9f-184">如果 [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) 选项卡通过深层链接导航，则调用将返回包含 `subEntityId` 字段的上下文。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-184">The [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) call returns a context that includes the `subEntityId` field if the tab is navigated through a deep link.</span></span>

## <a name="deep-linking-from-your-tab"></a><span data-ttu-id="2ae9f-185">选项卡中的深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-185">Deep linking from your tab</span></span>

<span data-ttu-id="2ae9f-186">可以从选项卡深入链接到Teams中的内容。如果你的选项卡需要链接到其他内容（如Teams、消息、其他选项卡或者甚至打开计划对话框，这将非常有用。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-186">You can deeplink to content in Teams from your tab. This is useful if your tab needs to link to other content in Teams, such as to a channel, message, another tab or even to open a scheduling dialog.</span></span> <span data-ttu-id="2ae9f-187">若要从选项卡触发深层链接，应调用：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-187">To trigger a deeplink from your tab you should call:</span></span>

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

<span data-ttu-id="2ae9f-188">此调用将你导航到正确的 URL，或触发客户端操作，例如打开计划或应用安装对话框。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-188">This call navigates you to the correct URL, or trigger a client action, such as opening a scheduling or app install dialog.</span></span> <span data-ttu-id="2ae9f-189">请参阅以下示例：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-189">See the following example:</span></span>

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a><span data-ttu-id="2ae9f-190">到聊天的深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-190">Deep linking to a chat</span></span>

<span data-ttu-id="2ae9f-191">通过指定一组参与者，可以创建指向用户之间的私人聊天的深层链接。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-191">You can create deep links to private chats between users by specifying the set of participants.</span></span> <span data-ttu-id="2ae9f-192">如果指定参与者不存在聊天，则链接将用户导航到空的新聊天。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-192">If a chat does not exist with the specified participants, the link navigates the user to an empty new chat.</span></span> <span data-ttu-id="2ae9f-193">在用户发送第一条消息之前，会以草稿状态创建新聊天。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-193">New chats are  created in draft state until the user sends the first message.</span></span> <span data-ttu-id="2ae9f-194">否则，您可以指定聊天的名称（如果它不存在）以及应插入到用户的撰写框中的文本。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-194">Otherwise, you can specify the name of the chat if it does not already exist, along with text that should be inserted into the user's compose box.</span></span> <span data-ttu-id="2ae9f-195">你可以将此功能视为用户执行手动操作以导航到或创建聊天，然后键入消息的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-195">You can think of this feature as a shortcut for the user taking the manual action of navigating to or creating the chat, and then typing out the message.</span></span>

<span data-ttu-id="2ae9f-196">例如，如果你将一个Office 365作为卡片从自动程序返回一个用户配置文件，则此深层链接可以让用户轻松地与此人聊天。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-196">As an example use case, if you are returning an Office 365 user profile from your bot as a card, this deep link can allow the user to easily chat with that person.</span></span>

### <a name="generate-a-deep-link-to-a-chat"></a><span data-ttu-id="2ae9f-197">生成聊天的深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-197">Generate a deep link to a chat</span></span>

<span data-ttu-id="2ae9f-198">对于可以在自动程序、连接器或邮件扩展卡中使用的深层链接，请使用此格式：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-198">Use this format for a deep link that you can use in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

<span data-ttu-id="2ae9f-199">示例：`https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span><span class="sxs-lookup"><span data-stu-id="2ae9f-199">Example: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span></span>

<span data-ttu-id="2ae9f-200">查询参数包括：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-200">The query parameters are:</span></span>

* <span data-ttu-id="2ae9f-201">`users`：表示聊天参与者的用户 ID 的逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-201">`users`: The comma-separated list of user IDs representing the participants of the chat.</span></span> <span data-ttu-id="2ae9f-202">执行该操作的用户始终作为参与者包含在内。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-202">The user that performs the action is always included as a participant.</span></span> <span data-ttu-id="2ae9f-203">目前，用户 ID 字段支持 Azure AD UserPrincipalName，例如仅电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-203">Currently, the User ID field supports the Azure AD UserPrincipalName, such as an email address only.</span></span>
* <span data-ttu-id="2ae9f-204">`topicName`：聊天的可选字段显示名称（如果与 3 个或多个用户聊天）。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-204">`topicName`: An optional field for chat's display name, in the case of a chat with 3 or more users.</span></span> <span data-ttu-id="2ae9f-205">如果未指定此字段，则聊天显示名称基于参与者的名称。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-205">If this field is not specified, the chat's display name is based on the names of the participants.</span></span>
* <span data-ttu-id="2ae9f-206">`message`：当聊天状态为草稿时，要插入到当前用户的撰写框中的消息文本的可选字段。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-206">`message`: An optional field for the message text that you want to insert into the current user's compose box while the chat is in a draft state.</span></span>

<span data-ttu-id="2ae9f-207">若要将此深层链接与自动程序一同使用，请在卡片按钮中指定此链接作为 URL 目标，或点击操作类型 `openUrl` 中的操作。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-207">To use this deep link with your bot, specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>

## <a name="generate-deep-links-to-file-in-channel"></a><span data-ttu-id="2ae9f-208">在通道中生成文件深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-208">Generate deep links to file in channel</span></span>

<span data-ttu-id="2ae9f-209">以下深层链接格式可用于自动程序、连接器或邮件扩展卡：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-209">The following deep link format can be used in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80?tenantId=<tenantid>&fileType=<filetype>&objectURL=<objectURL>&baseUrl=<baseURL>&serviceName=<Name>&threadId=<threadid>&groupId=<groupId>`

<span data-ttu-id="2ae9f-210">查询参数包括：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-210">The query parameters are:</span></span>

* <span data-ttu-id="2ae9f-211">`tenantId`：租户 ID 示例，0d9b645f-597b-41f0-a2a3-ef103fbd91bb</span><span class="sxs-lookup"><span data-stu-id="2ae9f-211">`tenantId`: Tenant ID example, 0d9b645f-597b-41f0-a2a3-ef103fbd91bb</span></span>
* <span data-ttu-id="2ae9f-212">`fileType`：受支持的文件类型，例如 docx、pptx、xlsx 和 pdf</span><span class="sxs-lookup"><span data-stu-id="2ae9f-212">`fileType`: Supported file type, such as docx, pptx, xlsx, and pdf</span></span>
* <span data-ttu-id="2ae9f-213">`objectUrl`：文件的对象 URL， `https://microsoft.sharepoint.com/teams/(filepath)`</span><span class="sxs-lookup"><span data-stu-id="2ae9f-213">`objectUrl`: Object URL of the file, `https://microsoft.sharepoint.com/teams/(filepath)`</span></span>
* <span data-ttu-id="2ae9f-214">`baseUrl`：文件的基本 URL， `https://microsoft.sharepoint.com/teams`</span><span class="sxs-lookup"><span data-stu-id="2ae9f-214">`baseUrl`: Base URL of the file, `https://microsoft.sharepoint.com/teams`</span></span>
* <span data-ttu-id="2ae9f-215">`serviceName`：服务名称、应用 ID</span><span class="sxs-lookup"><span data-stu-id="2ae9f-215">`serviceName`: Name of the service, app ID</span></span>
* <span data-ttu-id="2ae9f-216">`threadId`：threadId 是存储文件的团队的团队 ID。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-216">`threadId`: The threadId is the team ID of the team where the file is stored.</span></span> <span data-ttu-id="2ae9f-217">它是可选的，并且不能为存储在用户的"文件夹"文件夹中OneDrive设置。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-217">It is optional and cannot be set for files stored in a user's OneDrive folder.</span></span> <span data-ttu-id="2ae9f-218">threadId - 19：f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype</span><span class="sxs-lookup"><span data-stu-id="2ae9f-218">threadId - 19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype</span></span>
* <span data-ttu-id="2ae9f-219">`groupId`：文件组 ID ae063b79-5315-4ddb-ba70-27328ba6c31e</span><span class="sxs-lookup"><span data-stu-id="2ae9f-219">`groupId`: Group ID of the file, ae063b79-5315-4ddb-ba70-27328ba6c31e</span></span>

<span data-ttu-id="2ae9f-220">以下是指向文件的深层链接的示例格式：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-220">Following is the sample format of deeplink to files:</span></span>

`https://teams.microsoft.com/l/file/5E0154FC-F2B4-4DA5-8CDA-F096E72C0A80 ?tenantId=0d9b645f-597b-41f0-a2a3-ef103fbd91bb&fileType=pptx&objectUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform%2FShared%20Documents%2FFC7-%20Bot%20and%20Action%20Infra%2FKaizala%20Actions%20in%20Adaptive%20Cards%20-%20Deck.pptx&baseUrl=https%3A%2F%2Fmicrosoft.sharepoint.com%2Fteams%2FActionPlatform&serviceName=teams&threadId=19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype&groupId=ae063b79-5315-4ddb-ba70-27328ba6c31e`

### <a name="serialization-of-this-object"></a><span data-ttu-id="2ae9f-221">此对象的序列化：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-221">Serialization of this object:</span></span>
```
{
tenantId: "0d9b645f-597b-41f0-a2a3-ef103fbd91bb",
filetype: = "pptx",
objectUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform/Shared Documents/FC7- Bot and Action Infra/Kaizala Actions in Adaptive Cards - Deck.pptx",
baseUrl: "https://microsoft.sharepoint.com/teams/ActionPlatform",
serviceName: "teams",
threadId: = "19:f8fbfc4d89e24ef5b3b8692538cebeb7@thread.skype",
groupId: "ae063b79-5315-4ddb-ba70-27328ba6c31e"
}
```

## <a name="deep-linking-to-an-app"></a><span data-ttu-id="2ae9f-222">到应用的深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-222">Deep linking to an app</span></span>

<span data-ttu-id="2ae9f-223">在应用在应用商店中列出应用后，为应用Teams链接。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-223">Create deeplinks for the app after the app is listed in the Teams store.</span></span> <span data-ttu-id="2ae9f-224">若要创建链接以启动Teams，将以下 URL 附加到应用 `https://teams.microsoft.com/l/app/<your-app-id>` ID：。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-224">To create a link to launch Teams, append the following URL to your app ID: `https://teams.microsoft.com/l/app/<your-app-id>`.</span></span> <span data-ttu-id="2ae9f-225">将显示一个对话框来安装该应用。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-225">A dialog box appears to install the app.</span></span> 
  
## <a name="deep-linking-for-sharepoint-framework-tabs"></a><span data-ttu-id="2ae9f-226">选项卡的深层SharePoint 框架链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-226">Deep linking for SharePoint Framework tabs</span></span>

<span data-ttu-id="2ae9f-227">以下深层链接格式可用于机器人、连接器或邮件扩展卡： `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`</span><span class="sxs-lookup"><span data-stu-id="2ae9f-227">The following deep link format can be used in a bot, connector or messaging extension card: `https://teams.microsoft.com/l/entity/<AppId>/<EntityId>?webUrl=<entityWebUrl>/<EntityName>`</span></span>

> [!NOTE]
> <span data-ttu-id="2ae9f-228">当机器人发送带深层链接的 TextBlock 消息时，当用户选择该链接时，将打开一个新的浏览器选项卡。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-228">When a bot sends a TextBlock message with a deep link, a new browser tab opens when users select the link.</span></span> <span data-ttu-id="2ae9f-229">这发生在 Chrome 和Microsoft Teams Linux 上运行的桌面应用中。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-229">This happens in Chrome and Microsoft Teams desktop app running on Linux.</span></span>
> <span data-ttu-id="2ae9f-230">如果自动程序将同一深层链接 URL 发送到 ，Teams当用户选择链接时，将在当前浏览器中打开"自动 `Action.OpenUrl` 链接"选项卡。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-230">If the bot sends the same deep link URL into an `Action.OpenUrl`, the Teams tab opens in the current browser when the user selects the link.</span></span> <span data-ttu-id="2ae9f-231">未打开新的浏览器选项卡。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-231">No new browser tab is opened.</span></span>

<span data-ttu-id="2ae9f-232">查询参数包括：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-232">The query parameters are:</span></span>

* <span data-ttu-id="2ae9f-233">`appID`：清单 ID **fe4a8eba-2a31-4737-8e33-e5fae6fee194**。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-233">`appID`: Your manifest ID **fe4a8eba-2a31-4737-8e33-e5fae6fee194**.</span></span>

* <span data-ttu-id="2ae9f-234">`entityID`：配置选项卡时 [提供的项目 ID。](~/tabs/how-to/create-tab-pages/configuration-page.md)例如 **，tasklist123**。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-234">`entityID`: The item ID that you provided when [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md). For example, **tasklist123**.</span></span>
* <span data-ttu-id="2ae9f-235">`entityWebUrl`：如果客户端不支持呈现选项卡或 ，则使用带回退 URL 的可选 `https://tasklist.example.com/123` 字段 `https://tasklist.example.com/list123/task456` 。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-235">`entityWebUrl`: An optional field with a fallback URL to use if the client does not support rendering of the tab - `https://tasklist.example.com/123` or `https://tasklist.example.com/list123/task456`.</span></span>
* <span data-ttu-id="2ae9f-236">`entityName`：选项卡中项的标签，用于显示深层链接（任务列表 123 或任务 456）。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-236">`entityName`: A label for the item in your tab, to use when displaying the deep link, Task List 123 or Task 456.</span></span>

<span data-ttu-id="2ae9f-237">示例：https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList</span><span class="sxs-lookup"><span data-stu-id="2ae9f-237">Example: https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&TaskList</span></span>

## <a name="deep-linking-to-the-scheduling-dialog"></a><span data-ttu-id="2ae9f-238">到计划对话框的深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-238">Deep linking to the scheduling dialog</span></span>

> [!NOTE]
> <span data-ttu-id="2ae9f-239">此功能目前处于开发人员预览阶段。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-239">This feature is currently in developer preview.</span></span>

<span data-ttu-id="2ae9f-240">可以创建指向内置计划Teams的深层链接。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-240">You can create deep links to the Teams built-in scheduling dialog.</span></span> <span data-ttu-id="2ae9f-241">如果你的应用可帮助用户完成日历或计划相关任务，这将特别有用。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-241">This is especially useful if your app helps the user complete calendar or scheduling related tasks.</span></span>

### <a name="generate-a-deep-link-to-the-scheduling-dialog"></a><span data-ttu-id="2ae9f-242">生成到计划对话框的深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-242">Generate a deep link to the scheduling dialog</span></span>

<span data-ttu-id="2ae9f-243">对可以在自动程序、连接器或邮件扩展卡中使用的深层链接使用以下格式： `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span><span class="sxs-lookup"><span data-stu-id="2ae9f-243">Use the following format for a deep link that you can use in a bot, Connector, or messaging extension card: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span></span>

<span data-ttu-id="2ae9f-244">示例：`https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span><span class="sxs-lookup"><span data-stu-id="2ae9f-244">Example: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span></span>

<span data-ttu-id="2ae9f-245">查询参数包括：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-245">The query parameters are:</span></span>

* <span data-ttu-id="2ae9f-246">`attendees`：可选的以逗号分隔的用户 ID 列表，表示会议与会者。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-246">`attendees`: The optional comma-separated list of user IDs representing the attendees of the meeting.</span></span> <span data-ttu-id="2ae9f-247">执行该操作的用户是会议组织者。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-247">The user performing the action is the meeting organizer.</span></span> <span data-ttu-id="2ae9f-248">用户 ID 字段当前仅支持 Azure AD UserPrincipalName，通常为电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-248">The User ID field currently only supports the Azure AD UserPrincipalName, typically an email address.</span></span>
* <span data-ttu-id="2ae9f-249">`startTime`：事件的可选开始时间。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-249">`startTime`: The optional start time of the event.</span></span> <span data-ttu-id="2ae9f-250">这应该采用 [长 ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)格式，例如 *2018-03-12T23：55：25+02：00。*</span><span class="sxs-lookup"><span data-stu-id="2ae9f-250">This should be in [long ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601), for example *2018-03-12T23:55:25+02:00*.</span></span>
* <span data-ttu-id="2ae9f-251">`endTime`：事件的可选结束时间，也采用 ISO 8601 格式。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-251">`endTime`: The optional end time of the event, also in ISO 8601 format.</span></span>
* <span data-ttu-id="2ae9f-252">`subject`：会议主题的可选字段。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-252">`subject`: An optional field for the meeting subject.</span></span>
* <span data-ttu-id="2ae9f-253">`content`：会议详细信息字段的可选字段。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-253">`content`: An optional field for the meeting details field.</span></span>

> [!NOTE]
> <span data-ttu-id="2ae9f-254">目前不支持指定位置。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-254">Currently, specifying the location is not supported.</span></span> <span data-ttu-id="2ae9f-255">你必须指定 UTC 偏移量，它表示生成开始时间和结束时间时时区。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-255">You must specify the UTC offset, it means time zones when generating your start and end times.</span></span>

<span data-ttu-id="2ae9f-256">若要将此深层链接与自动程序一同使用，可以在卡片按钮中指定此链接作为 URL 目标，或点击操作类型 `openUrl` 中的操作。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-256">To use this deep link with your bot, you can specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>

## <a name="deep-linking-to-an-audio-or-audio-video-call"></a><span data-ttu-id="2ae9f-257">到音频或音频视频呼叫的深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-257">Deep linking to an audio or audio-video call</span></span>

<span data-ttu-id="2ae9f-258">可以通过将呼叫类型指定为 *audio* 或 *av* 以及参与者来创建深层链接，以调用单个用户或一组用户的仅音频或音频视频呼叫。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-258">You can create deep links to invoke audio only or audio-video calls to a single user or a group of users, by specifying the call type, as *audio* or *av*, and the participants.</span></span> <span data-ttu-id="2ae9f-259">调用深层链接之后和发出呼叫之前，Teams客户端会提示确认进行呼叫。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-259">After the deep link is invoked and before placing the call, Teams desktop client prompts a confirmation to make the call.</span></span> <span data-ttu-id="2ae9f-260">对于组呼叫，可以在相同的深度链接调用中调用一组 VoIP 用户和一组 PSTN 用户。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-260">In case of group call, you can call a set of VoIP users and a set of PSTN users in the same deeplink invocation.</span></span> 

<span data-ttu-id="2ae9f-261">对于视频呼叫，客户端将要求确认，并打开呼叫者的视频。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-261">In case of a video call, the client will ask for confirmation and turn on the caller's video for the call.</span></span> <span data-ttu-id="2ae9f-262">呼叫接收者可以选择仅通过音频或音频和视频，通过呼叫通知Teams进行响应。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-262">The receiver of the call has a choice to respond through audio only or audio and video, through the Teams call notification window.</span></span>

> [!NOTE]
> <span data-ttu-id="2ae9f-263">此深度链接不能用于调用会议。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-263">This deeplink cannot be used for invoking a meeting.</span></span>

### <a name="generate-a-deep-link-to-a-call"></a><span data-ttu-id="2ae9f-264">生成到呼叫的深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-264">Generate a deep link to a call</span></span>

| <span data-ttu-id="2ae9f-265">深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-265">Deep link</span></span> | <span data-ttu-id="2ae9f-266">格式</span><span class="sxs-lookup"><span data-stu-id="2ae9f-266">Format</span></span> | <span data-ttu-id="2ae9f-267">示例</span><span class="sxs-lookup"><span data-stu-id="2ae9f-267">Example</span></span> |
|-----------|--------|---------|
| <span data-ttu-id="2ae9f-268">进行音频呼叫</span><span class="sxs-lookup"><span data-stu-id="2ae9f-268">Make an audio call</span></span> | <span data-ttu-id="2ae9f-269"> https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; &lt; 、user2&gt;</span><span class="sxs-lookup"><span data-stu-id="2ae9f-269">https://teams.microsoft.com/l/call/0/0?users=&lt;user1&gt;,&lt;user2&gt;</span></span> | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com |
| <span data-ttu-id="2ae9f-270">进行音频和视频呼叫</span><span class="sxs-lookup"><span data-stu-id="2ae9f-270">Make an audio and video call</span></span> | <span data-ttu-id="2ae9f-271"> https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; &lt; ，user2 &gt;&video=true</span><span class="sxs-lookup"><span data-stu-id="2ae9f-271">https://teams.microsoft.com/l/call/0/0?users=&lt;user1&gt;,&lt;user2&gt;&withvideo=true</span></span> | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true |
|<span data-ttu-id="2ae9f-272">使用可选参数源进行音频和视频呼叫</span><span class="sxs-lookup"><span data-stu-id="2ae9f-272">Make an audio and video call with an optional parameter source</span></span> | <span data-ttu-id="2ae9f-273"> https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; ， &lt; user2&&gt; withvideo=true&source=demoApp</span><span class="sxs-lookup"><span data-stu-id="2ae9f-273">https://teams.microsoft.com/l/call/0/0?users=&lt;user1&gt;,&lt;user2&gt;&withvideo=true&source=demoApp</span></span> | https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com&withvideo=true&source=demoApp |  
| <span data-ttu-id="2ae9f-274">对 VoIP 和 PSTN 用户的组合进行音频和视频呼叫</span><span class="sxs-lookup"><span data-stu-id="2ae9f-274">Make an audio and video call to a combination of VoIP and PSTN users</span></span> | <span data-ttu-id="2ae9f-275"> https://teams.microsoft.com/l/call/0/0?users=&lt;user1 &gt; ，4： &lt; phonenumber&gt;</span><span class="sxs-lookup"><span data-stu-id="2ae9f-275">https://teams.microsoft.com/l/call/0/0?users=&lt;user1&gt;,4:&lt;phonenumber&gt;</span></span> | <span data-ttu-id="2ae9f-276"> https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210</span><span class="sxs-lookup"><span data-stu-id="2ae9f-276">https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,4:9876543210</span></span> |
  
<span data-ttu-id="2ae9f-277">以下是查询参数：</span><span class="sxs-lookup"><span data-stu-id="2ae9f-277">Following are the query parameters:</span></span>
* <span data-ttu-id="2ae9f-278">`users`：表示呼叫参与者的用户 ID 的逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-278">`users`: The comma-separated list of user IDs representing the participants of the call.</span></span> <span data-ttu-id="2ae9f-279">目前，用户 ID 字段支持 Azure AD UserPrincipalName（通常为电子邮件地址）或 PSTN 呼叫时，支持 pstn mri &lt; 4：phonenumber &gt; 。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-279">Currently, the User ID field supports the Azure AD UserPrincipalName, typically an email address, or in case of a PSTN call, it supports a pstn mri 4:&lt;phonenumber&gt;.</span></span>
* <span data-ttu-id="2ae9f-280">`Withvideo`：这是可选参数，可用于进行视频呼叫。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-280">`Withvideo`: This is an optional parameter, which you can use to make a video call.</span></span> <span data-ttu-id="2ae9f-281">设置此参数将仅打开呼叫者的相机。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-281">Setting this parameter will only turn on the caller's camera.</span></span> <span data-ttu-id="2ae9f-282">呼叫接收者可以选择通过音频或音频和视频呼叫通过呼叫通知窗口Teams进行应答。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-282">The receiver of the call has a choice to answer through audio or audio and video call through the Teams call notification window.</span></span> 
* <span data-ttu-id="2ae9f-283">`Source`：这是一个可选参数，用于通知深层链接的来源。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-283">`Source`: This is an optional parameter, which informs about the source of the deeplink.</span></span>

## <a name="code-sample"></a><span data-ttu-id="2ae9f-284">代码示例</span><span class="sxs-lookup"><span data-stu-id="2ae9f-284">Code sample</span></span>

| <span data-ttu-id="2ae9f-285">示例名称</span><span class="sxs-lookup"><span data-stu-id="2ae9f-285">Sample name</span></span> | <span data-ttu-id="2ae9f-286">说明</span><span class="sxs-lookup"><span data-stu-id="2ae9f-286">Description</span></span> | <span data-ttu-id="2ae9f-287">C#</span><span class="sxs-lookup"><span data-stu-id="2ae9f-287">C#</span></span> |<span data-ttu-id="2ae9f-288">Node.js</span><span class="sxs-lookup"><span data-stu-id="2ae9f-288">Node.js</span></span>|
|-------------|-------------|------|----|
|<span data-ttu-id="2ae9f-289">使用下级 ID 的深层链接</span><span class="sxs-lookup"><span data-stu-id="2ae9f-289">Deep Link consuming Subentity ID</span></span>  |<span data-ttu-id="2ae9f-290">Microsoft Teams聊天到选项卡使用子企业 ID 的深层链接的示例应用。</span><span class="sxs-lookup"><span data-stu-id="2ae9f-290">Microsoft Teams sample app for demonstrating deeplink from bot chat to tab consuming Subentity ID.</span></span>|[<span data-ttu-id="2ae9f-291">View</span><span class="sxs-lookup"><span data-stu-id="2ae9f-291">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/csharp)|[<span data-ttu-id="2ae9f-292">View</span><span class="sxs-lookup"><span data-stu-id="2ae9f-292">View</span></span>](https://github.com/OfficeDev/Microsoft-Teams-Samples/tree/main/samples/tab-deeplink/nodejs)|

## <a name="see-also"></a><span data-ttu-id="2ae9f-293">另请参阅</span><span class="sxs-lookup"><span data-stu-id="2ae9f-293">See also</span></span>

[<span data-ttu-id="2ae9f-294">集成 web 应用</span><span class="sxs-lookup"><span data-stu-id="2ae9f-294">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)

