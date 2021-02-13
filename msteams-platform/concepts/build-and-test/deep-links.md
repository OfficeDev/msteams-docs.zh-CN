---
title: 创建指向内容的深层链接
description: 介绍深层链接以及如何在应用中使用它们
ms.topic: how-to
keywords: 团队深层链接深层链接
ms.openlocfilehash: d6efe7332035320d2114e0e834d1c971ccc7108c
ms.sourcegitcommit: e3b6bc31059ec77de5fbef9b15c17d358abbca0f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/12/2021
ms.locfileid: "50231559"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a><span data-ttu-id="37281-104">创建指向 Microsoft Teams 中内容和功能的深层链接</span><span class="sxs-lookup"><span data-stu-id="37281-104">Create deep links to content and features in Microsoft Teams</span></span>

<span data-ttu-id="37281-105">可以在 Teams 内创建指向信息和功能的链接。</span><span class="sxs-lookup"><span data-stu-id="37281-105">You can create links to information and features within Teams.</span></span> <span data-ttu-id="37281-106">创建深层链接很有用的示例如下所示：</span><span class="sxs-lookup"><span data-stu-id="37281-106">Examples where creating deep links are useful are as follows:</span></span>

* <span data-ttu-id="37281-107">将用户导航到应用选项卡之一中的内容。</span><span class="sxs-lookup"><span data-stu-id="37281-107">Navigating the user to content within one of your app's tabs.</span></span> <span data-ttu-id="37281-108">例如，你的应用可以有一个自动程序来发送消息，通知用户重要活动。</span><span class="sxs-lookup"><span data-stu-id="37281-108">For instance, your app can have a bot that sends messages notifying the user of an important activity.</span></span> <span data-ttu-id="37281-109">当用户点击通知时，深层链接将导航到选项卡，以便用户可以查看有关活动的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="37281-109">When the user taps on the notification, the deep link navigates to the tab so the user can view more details about the activity.</span></span>
* <span data-ttu-id="37281-110">你的应用通过预填充包含所需参数的深层链接，自动执行或简化某些用户任务，如创建聊天或安排会议。</span><span class="sxs-lookup"><span data-stu-id="37281-110">Your app automates or simplifies certain user tasks, such as creating a chat or scheduling a meeting, by pre-populating the deep links with required parameters.</span></span> <span data-ttu-id="37281-111">这无需用户手动输入信息。</span><span class="sxs-lookup"><span data-stu-id="37281-111">This avoids the need for users to manually enter information.</span></span>

> [!NOTE]
>
> <span data-ttu-id="37281-112">深层链接先启动浏览器，然后再导航到内容和信息，如下所示：</span><span class="sxs-lookup"><span data-stu-id="37281-112">A deeplink launches the browser first before navigating to content and information as follows:</span></span>
>
> <span data-ttu-id="37281-113">**Tab**：</span><span class="sxs-lookup"><span data-stu-id="37281-113">**Tab**:</span></span>  
> <span data-ttu-id="37281-114">✔直接导航到深层链接 URL。</span><span class="sxs-lookup"><span data-stu-id="37281-114">✔ Directly navigates to the deeplink url.</span></span>
>
> <span data-ttu-id="37281-115">**自动程序**：</span><span class="sxs-lookup"><span data-stu-id="37281-115">**Bot**:</span></span>  
> <span data-ttu-id="37281-116">✔正文中的深度链接 - 首先在浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="37281-116">✔ Deeplink in card body - Opens in browser first.</span></span>  
> <span data-ttu-id="37281-117">✔添加到自适应卡片中的 OpenURL 操作中的 Deeplink - 直接导航到深度链接 url。</span><span class="sxs-lookup"><span data-stu-id="37281-117">✔ Deeplink added to OpenURL action in Adaptive Card - Directly navigates to the deeplink url.</span></span>  
> <span data-ttu-id="37281-118">✔中的超链接标记文本 - 首先在浏览器中打开。</span><span class="sxs-lookup"><span data-stu-id="37281-118">✔ Hyperlink markdown text in the card - Opens in browser first.</span></span>  
>
> <span data-ttu-id="37281-119">**聊天**：</span><span class="sxs-lookup"><span data-stu-id="37281-119">**Chat**:</span></span>  
> <span data-ttu-id="37281-120">✔文本消息超链接标记：直接导航到深层链接 URL。</span><span class="sxs-lookup"><span data-stu-id="37281-120">✔ Text message hyperlink markdown : Directly navigates to deeplink url.</span></span>  
> <span data-ttu-id="37281-121">✔常规聊天对话中粘贴的链接 - 直接导航到深层链接 URL。</span><span class="sxs-lookup"><span data-stu-id="37281-121">✔ Link pasted in general chat conversation - Directly navigates to deeplink url.</span></span>

## <a name="deep-linking-to-your-tab"></a><span data-ttu-id="37281-122">到选项卡的深层链接</span><span class="sxs-lookup"><span data-stu-id="37281-122">Deep linking to your tab</span></span>

<span data-ttu-id="37281-123">你可以创建指向 Teams 中实体的深层链接。</span><span class="sxs-lookup"><span data-stu-id="37281-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="37281-124">通常，这用于创建导航到选项卡中内容和信息的链接。例如，如果选项卡包含任务列表，工作组成员可以创建并共享指向单个任务的链接。</span><span class="sxs-lookup"><span data-stu-id="37281-124">Typically, this is used to create links that navigate to content and information within your tab. For example, if your tab contains a task list team members can create and share links to individual tasks.</span></span> <span data-ttu-id="37281-125">选择链接时，它会导航到以特定项目为焦点的选项卡。</span><span class="sxs-lookup"><span data-stu-id="37281-125">When you select the link, it  navigates to your tab which focuses on the specific item.</span></span> <span data-ttu-id="37281-126">若要实现此目标，请以最适合你的 UI 的任何方式向每个项目添加"复制链接"操作。</span><span class="sxs-lookup"><span data-stu-id="37281-126">To implement this, you add a "copy link" action to each item, in whatever way best suits your UI.</span></span> <span data-ttu-id="37281-127">当用户采取此操作时，您调用以显示一个对话框，其中包含用户可复制到 `shareDeepLink()` 剪贴板的链接。</span><span class="sxs-lookup"><span data-stu-id="37281-127">When the user takes this action, you call `shareDeepLink()` to display a dialog box containing a link that the user can copy to the clipboard.</span></span> <span data-ttu-id="37281-128">进行此调用时，还会传递项的 ID，在单击链接并重新加载选项卡时，会[](~/tabs/how-to/access-teams-context.md)返回该 ID。</span><span class="sxs-lookup"><span data-stu-id="37281-128">When you make this call, you also pass an ID for your item, which you get back in the [context](~/tabs/how-to/access-teams-context.md) when the link is followed and your tab is reloaded.</span></span>

<span data-ttu-id="37281-129">或者，您也可以使用本主题稍后指定的格式以编程方式生成深层链接。</span><span class="sxs-lookup"><span data-stu-id="37281-129">Alternatively, you can also generate deep links programmatically, using the format specified later in this topic.</span></span> <span data-ttu-id="37281-130">可以在 [自动程序消息](~/bots/what-are-bots.md) 和连接器消息 [中](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) 使用这些消息，以通知用户选项卡或其中项目的更改。</span><span class="sxs-lookup"><span data-stu-id="37281-130">You can use these in [bot](~/bots/what-are-bots.md) and [connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) messages that inform users about changes to your tab, or to items within it.</span></span>

> [!NOTE]
> <span data-ttu-id="37281-131">此深层链接不同于指向选项卡菜单项的 **"** 复制"链接提供的链接，而该链接仅生成指向此选项卡的深层链接。</span><span class="sxs-lookup"><span data-stu-id="37281-131">This deep link is different from the links provided by the **Copy link to tab** menu item, which just generates a deep link that points to this tab.</span></span>

>[!NOTE]
> <span data-ttu-id="37281-132">目前，shareDeepLink 在移动平台上不起作用。</span><span class="sxs-lookup"><span data-stu-id="37281-132">Currently, shareDeepLink does not work on mobile platforms.</span></span>

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a><span data-ttu-id="37281-133">显示指向选项卡内项目的深层链接</span><span class="sxs-lookup"><span data-stu-id="37281-133">Showing a deep link to an item within your tab</span></span>

<span data-ttu-id="37281-134">若要显示包含指向选项卡中项目的深层链接的对话框，请调用 `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`</span><span class="sxs-lookup"><span data-stu-id="37281-134">To show a dialog box that contains a deep link to an item within your tab, call `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`</span></span>

<span data-ttu-id="37281-135">提供以下字段：</span><span class="sxs-lookup"><span data-stu-id="37281-135">Provide these fields:</span></span>

* <span data-ttu-id="37281-136">`subEntityId`&emsp;要深入链接到的选项卡内项目的唯一标识符</span><span class="sxs-lookup"><span data-stu-id="37281-136">`subEntityId`&emsp;A unique identifier for the item within your tab to which you are deep linking</span></span>
* <span data-ttu-id="37281-137">`subEntityLabel`&emsp;用于显示深层链接的项目的标签</span><span class="sxs-lookup"><span data-stu-id="37281-137">`subEntityLabel`&emsp;A label for the item to use for displaying the deep link</span></span>
* <span data-ttu-id="37281-138">`subEntityWebUrl`&emsp;具有回退 URL 的可选字段，如果客户端不支持呈现选项卡</span><span class="sxs-lookup"><span data-stu-id="37281-138">`subEntityWebUrl`&emsp;An optional field with a fallback URL to use if the client does not support rendering the tab</span></span>

### <a name="generating-a-deep-link-to-your-tab"></a><span data-ttu-id="37281-139">生成到选项卡的深层链接</span><span class="sxs-lookup"><span data-stu-id="37281-139">Generating a deep link to your tab</span></span>

> [!NOTE]
> <span data-ttu-id="37281-140">个人选项卡具有 `personal` 范围，而频道和组选项卡使用 `team` 或 `group` 作用域。</span><span class="sxs-lookup"><span data-stu-id="37281-140">Personal tabs have a `personal` scope, while channel and group tabs use `team` or `group` scopes.</span></span> <span data-ttu-id="37281-141">这两个选项卡类型的语法略有不同，因为只有可配置的选项卡具有与其上下文 `channel` 对象关联的属性。</span><span class="sxs-lookup"><span data-stu-id="37281-141">The two tab types have a slightly different syntax since only the configurable tab has a `channel` property associated with its context object.</span></span> <span data-ttu-id="37281-142">有关 [选项卡](~/resources/schema/manifest-schema.md) 范围详细信息，请参阅清单参考。</span><span class="sxs-lookup"><span data-stu-id="37281-142">See the [manifest](~/resources/schema/manifest-schema.md) reference for more information on tab scopes.</span></span>

> [!NOTE]
> <span data-ttu-id="37281-143">只有在使用 v0.4 或更高版本库配置了选项卡并且由于该选项卡具有实体 ID 时，深度链接才能正常工作。</span><span class="sxs-lookup"><span data-stu-id="37281-143">Deep links work properly only if the tab was configured using the v0.4 or later library and because of that has an entity ID.</span></span> <span data-ttu-id="37281-144">指向没有实体 ID 的选项卡的深层链接仍导航到选项卡，但无法向选项卡提供子实体 ID。</span><span class="sxs-lookup"><span data-stu-id="37281-144">Deep links to tabs without entity IDs still navigate to the tab but can not provide the sub-entity ID to the tab.</span></span>

<span data-ttu-id="37281-145">对可以在自动程序、连接器或邮件扩展卡中使用的深层链接使用以下格式：</span><span class="sxs-lookup"><span data-stu-id="37281-145">Use the following format for a deep link that you can use in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

> [!NOTE]
> <span data-ttu-id="37281-146">如果自动程序发送包含深层链接的消息，则当用户选择链接时将打开一 `TextBlock` 个新的浏览器选项卡。</span><span class="sxs-lookup"><span data-stu-id="37281-146">If the bot sends a message containing a `TextBlock` with a deep link, then a new browser tab is opened when the user selects the link.</span></span> <span data-ttu-id="37281-147">这发生在 Chrome 和 Microsoft Teams 桌面应用中，两者均在 Linux 上运行。</span><span class="sxs-lookup"><span data-stu-id="37281-147">This happens in Chrome and in the Microsoft Teams desktop app, both running on Linux.</span></span>
> <span data-ttu-id="37281-148">如果机器人将相同的深层链接 URL 发送到一个，则当用户选择链接时，将在当前浏览器选项卡中打开 `Action.OpenUrl` Teams 选项卡。</span><span class="sxs-lookup"><span data-stu-id="37281-148">If the bot sends the same deep link URL into an `Action.OpenUrl`, then the Teams tab is opened in the current browser tab when the user selects the link.</span></span> <span data-ttu-id="37281-149">未打开新浏览器选项卡。</span><span class="sxs-lookup"><span data-stu-id="37281-149">No new browser tab is opened.</span></span>

<span data-ttu-id="37281-150">查询参数包括：</span><span class="sxs-lookup"><span data-stu-id="37281-150">The query parameters are:</span></span>

* <span data-ttu-id="37281-151">`appId`&emsp;清单中的 ID;例如，"fe4a8eba-2a31-4737-8e33-e5fae6fee194"</span><span class="sxs-lookup"><span data-stu-id="37281-151">`appId`&emsp;The ID from your manifest; for example, "fe4a8eba-2a31-4737-8e33-e5fae6fee194"</span></span>
* <span data-ttu-id="37281-152">`entityId`&emsp;选项卡中项的 ID，在配置选项卡 [时提供](~/tabs/how-to/create-tab-pages/configuration-page.md);例如，"tasklist123"</span><span class="sxs-lookup"><span data-stu-id="37281-152">`entityId`&emsp;The ID for the item in the tab, which you provided when [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md); for example, "tasklist123"</span></span>
* <span data-ttu-id="37281-153">`entityWebUrl`或具有回退 URL 的可选字段（如果客户端不支持呈现选项卡）;例如 `subEntityWebUrl` &emsp; ，" https://tasklist.example.com/123 " 或 https://tasklist.example.com/list123/task456 "</span><span class="sxs-lookup"><span data-stu-id="37281-153">`entityWebUrl` or `subEntityWebUrl`&emsp;An optional field with a fallback URL to use if the client does not support rendering the tab; for example, "https://tasklist.example.com/123" or "https://tasklist.example.com/list123/task456"</span></span>
* <span data-ttu-id="37281-154">`entityLabel`或选项卡中项的标签，用于显示深层链接;例如，" `subEntityLabel` &emsp; 任务列表 123"或"任务 456"</span><span class="sxs-lookup"><span data-stu-id="37281-154">`entityLabel` or `subEntityLabel`&emsp;A label for the item in your tab, to use when displaying the deep link; for example, "Task List 123" or "Task 456"</span></span>
* <span data-ttu-id="37281-155">`context`&emsp;包含以下字段的 JSON 对象：</span><span class="sxs-lookup"><span data-stu-id="37281-155">`context`&emsp;A JSON object containing the following fields:</span></span>
  * <span data-ttu-id="37281-156">`subEntityId`&emsp;选项卡内项 _的_ ID;例如，"task456"</span><span class="sxs-lookup"><span data-stu-id="37281-156">`subEntityId`&emsp;An ID for the item _within_ the tab; for example, "task456"</span></span>
  * <span data-ttu-id="37281-157">`channelId`&emsp;选项卡上下文中提供的 Microsoft Teams 频道 [ID;](~/tabs/how-to/access-teams-context.md)例如，"19：cbe3683f25094106b826c9cada3afbe0@thread.skype"。</span><span class="sxs-lookup"><span data-stu-id="37281-157">`channelId`&emsp;The Microsoft Teams channel ID that is available from the tab [context](~/tabs/how-to/access-teams-context.md); for example, "19:cbe3683f25094106b826c9cada3afbe0@thread.skype".</span></span> <span data-ttu-id="37281-158">此属性仅在作用域为"team"的可配置选项卡中可用。</span><span class="sxs-lookup"><span data-stu-id="37281-158">This property is only available in configurable tabs with a scope of "team".</span></span> <span data-ttu-id="37281-159">它在静态选项卡中不可用，这些选项卡的范围为"个人"。</span><span class="sxs-lookup"><span data-stu-id="37281-159">It is not available in static tabs, which have a scope of "personal".</span></span>

<span data-ttu-id="37281-160">示例：</span><span class="sxs-lookup"><span data-stu-id="37281-160">Examples:</span></span>

* <span data-ttu-id="37281-161">指向可配置选项卡本身的链接： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="37281-161">Link to a configurable tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="37281-162">指向可配置选项卡中的任务项的链接： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="37281-162">Link to a task item within the configurable tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="37281-163">指向静态选项卡本身的链接： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span><span class="sxs-lookup"><span data-stu-id="37281-163">Link to a static tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span></span>
* <span data-ttu-id="37281-164">指向静态选项卡中的任务项的链接： `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span><span class="sxs-lookup"><span data-stu-id="37281-164">Link to a task item within the static tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="37281-165">确保所有查询参数都正确编码了 URI。</span><span class="sxs-lookup"><span data-stu-id="37281-165">Ensure that all query parameters are properly URI encoded.</span></span> <span data-ttu-id="37281-166">您必须使用上一个示例遵循之前的示例：</span><span class="sxs-lookup"><span data-stu-id="37281-166">You must follow the preceeding examples using the last example:</span></span>
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a><span data-ttu-id="37281-167">从选项卡使用深层链接</span><span class="sxs-lookup"><span data-stu-id="37281-167">Consuming a deep link from a tab</span></span>

<span data-ttu-id="37281-168">导航到深层链接时，Microsoft Teams 只需导航到选项卡，并通过 Microsoft Teams JavaScript 库提供一种机制，以检索子实体 ID（如果存在）。</span><span class="sxs-lookup"><span data-stu-id="37281-168">When navigating to a deep link, Microsoft Teams simply navigates to the tab and provides a mechanism through the Microsoft Teams JavaScript library to retrieve the sub-entity ID if it exists.</span></span>

<span data-ttu-id="37281-169">如果 [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) 选项卡通过深层链接导航，调用将返回包含 `subEntityId` 字段的上下文。</span><span class="sxs-lookup"><span data-stu-id="37281-169">The [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) call returns a context that includes the `subEntityId` field if the tab is navigated through a deep link.</span></span>

## <a name="deep-linking-from-your-tab"></a><span data-ttu-id="37281-170">从选项卡进行深层链接</span><span class="sxs-lookup"><span data-stu-id="37281-170">Deep linking from your tab</span></span>

<span data-ttu-id="37281-171">你可以从选项卡深入链接到 Teams 中的内容。如果你的选项卡需要链接到 Teams 中的其他内容（如频道、消息、其他选项卡，或者甚至打开计划对话框，这非常有用。</span><span class="sxs-lookup"><span data-stu-id="37281-171">You can deeplink to content in Teams from your tab. This is useful if your tab needs to link to other content in Teams, such as to a channel, message, another tab or even to open a scheduling dialog.</span></span> <span data-ttu-id="37281-172">若要从选项卡触发深层链接，应调用：</span><span class="sxs-lookup"><span data-stu-id="37281-172">To trigger a deeplink from your tab you should call:</span></span>

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

<span data-ttu-id="37281-173">此调用将你导航到正确的 URL，或触发客户端操作，例如打开计划或应用安装对话框。</span><span class="sxs-lookup"><span data-stu-id="37281-173">This call navigates you to the correct URL, or trigger a client action, such as opening a scheduling or app install dialog.</span></span> <span data-ttu-id="37281-174">请参阅以下示例：</span><span class="sxs-lookup"><span data-stu-id="37281-174">See the following example:</span></span>

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a><span data-ttu-id="37281-175">到聊天的深层链接</span><span class="sxs-lookup"><span data-stu-id="37281-175">Deep linking to a chat</span></span>

<span data-ttu-id="37281-176">通过指定参与者集，可以创建指向用户之间的私人聊天的深层链接。</span><span class="sxs-lookup"><span data-stu-id="37281-176">You can create deep links to private chats between users by specifying the set of participants.</span></span> <span data-ttu-id="37281-177">如果指定参与者不存在聊天，则链接将用户导航到空的新聊天。</span><span class="sxs-lookup"><span data-stu-id="37281-177">If a chat does not exist with the specified participants, the link navigates the user to an empty new chat.</span></span> <span data-ttu-id="37281-178">在用户发送第一条消息之前，会以草稿状态新建聊天。</span><span class="sxs-lookup"><span data-stu-id="37281-178">New chats are  created in draft state until the user sends the first message.</span></span> <span data-ttu-id="37281-179">否则，您可以指定聊天的名称（如果它不存在）以及应插入到用户的撰写框中的文本。</span><span class="sxs-lookup"><span data-stu-id="37281-179">Otherwise, you can specify the name of the chat if it does not already exist, along with text that should be inserted into the user's compose box.</span></span> <span data-ttu-id="37281-180">你可以将此功能视为用户执行手动操作以导航到或创建聊天，然后键入消息的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="37281-180">You can think of this feature as a shortcut for the user taking the manual action of navigating to or creating the chat, and then typing out the message.</span></span>

<span data-ttu-id="37281-181">例如，如果你将 Office 365 用户配置文件作为卡片从自动程序返回，此深层链接可让用户轻松与该用户聊天。</span><span class="sxs-lookup"><span data-stu-id="37281-181">As an example use case, if you are returning an Office 365 user profile from your bot as a card, this deep link can allow the user to easily chat with that person.</span></span>

### <a name="generating-a-deep-link-to-a-chat"></a><span data-ttu-id="37281-182">生成到聊天的深层链接</span><span class="sxs-lookup"><span data-stu-id="37281-182">Generating a deep link to a chat</span></span>

<span data-ttu-id="37281-183">对于可以在自动程序、连接器或邮件扩展卡中使用的深层链接，请使用此格式：</span><span class="sxs-lookup"><span data-stu-id="37281-183">Use this format for a deep link that you can use in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

<span data-ttu-id="37281-184">示例：`https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span><span class="sxs-lookup"><span data-stu-id="37281-184">Example: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span></span>

<span data-ttu-id="37281-185">查询参数包括：</span><span class="sxs-lookup"><span data-stu-id="37281-185">The query parameters are:</span></span>

* <span data-ttu-id="37281-186">`users`：表示聊天参与者的用户 ID 的逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="37281-186">`users`: The comma-separated list of user IDs representing the participants of the chat.</span></span> <span data-ttu-id="37281-187">执行该操作的用户始终作为参与者包含在内。</span><span class="sxs-lookup"><span data-stu-id="37281-187">The user that performs the action is always included as a participant.</span></span> <span data-ttu-id="37281-188">目前，用户 ID 字段支持 Azure AD UserPrincipalName，通常仅支持电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="37281-188">Currently, the User ID field supports the Azure AD UserPrincipalName, typically an email address only.</span></span>
* <span data-ttu-id="37281-189">`topicName`：一个可选字段，用于显示名称（如果与 3 个或多个用户进行聊天）。</span><span class="sxs-lookup"><span data-stu-id="37281-189">`topicName`: An optional field for chat's display name, in the case of a chat with 3 or more users.</span></span> <span data-ttu-id="37281-190">如果未指定此字段，则聊天显示名称基于参与者的名称。</span><span class="sxs-lookup"><span data-stu-id="37281-190">If this field is not specified, the chat's display name is based on the names of the participants.</span></span>
* <span data-ttu-id="37281-191">`message`：在聊天状态为草稿时要插入到当前用户的撰写框中的消息文本的可选字段。</span><span class="sxs-lookup"><span data-stu-id="37281-191">`message`: An optional field for the message text that you want to insert into the current user's compose box while the chat is in a draft state.</span></span>

<span data-ttu-id="37281-192">若要将此深层链接与自动程序一同使用，可以在卡片按钮中指定此链接作为 URL 目标，或点击操作类型的 `openUrl` 操作。</span><span class="sxs-lookup"><span data-stu-id="37281-192">To use this deep link with your bot, you can specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>

### <a name="generating-a-deep-link-to-a-call"></a><span data-ttu-id="37281-193">生成与呼叫的深层链接</span><span class="sxs-lookup"><span data-stu-id="37281-193">Generating a deep link to a call</span></span>

<span data-ttu-id="37281-194">对于可以在自动程序、连接器或邮件扩展卡中使用的深层链接，请使用此格式：</span><span class="sxs-lookup"><span data-stu-id="37281-194">Use this format for a deep link that you can use in a bot, connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/call/0/0?users=<user1>,<user2>`

<span data-ttu-id="37281-195">示例：`https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span><span class="sxs-lookup"><span data-stu-id="37281-195">Example: `https://teams.microsoft.com/l/call/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span></span>

<span data-ttu-id="37281-196">查询参数包括：</span><span class="sxs-lookup"><span data-stu-id="37281-196">The query parameters are:</span></span>

* <span data-ttu-id="37281-197">`users`：表示呼叫参与者的用户 ID 的逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="37281-197">`users`: The comma-separated list of user IDs representing the participants of the call.</span></span> <span data-ttu-id="37281-198">执行该操作的用户始终作为参与者包含在内。</span><span class="sxs-lookup"><span data-stu-id="37281-198">The user that performs the action is always included as a participant.</span></span> <span data-ttu-id="37281-199">目前，用户 ID 字段支持 Azure AD UserPrincipalName，通常仅支持电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="37281-199">Currently, the User ID field supports the Azure AD UserPrincipalName, typically an email address only.</span></span>

## <a name="linking-to-the-scheduling-dialog"></a><span data-ttu-id="37281-200">链接到计划对话框</span><span class="sxs-lookup"><span data-stu-id="37281-200">Linking to the scheduling dialog</span></span>

> [!Note]
> <span data-ttu-id="37281-201">此功能目前处于开发人员预览阶段。</span><span class="sxs-lookup"><span data-stu-id="37281-201">This feature is currently in developer preview.</span></span>

<span data-ttu-id="37281-202">可以创建指向 Teams 内置计划对话框的深层链接。</span><span class="sxs-lookup"><span data-stu-id="37281-202">You can create deep links to the Teams built-in scheduling dialog.</span></span> <span data-ttu-id="37281-203">如果你的应用可帮助用户完成日历或计划相关任务，这尤其有用。</span><span class="sxs-lookup"><span data-stu-id="37281-203">This is especially useful if your app helps the user complete calendar or scheduling-related tasks.</span></span>

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a><span data-ttu-id="37281-204">生成到计划对话框的深层链接</span><span class="sxs-lookup"><span data-stu-id="37281-204">Generating a deep link to the scheduling dialog</span></span>

<span data-ttu-id="37281-205">对可以在自动程序、连接器或邮件扩展卡中使用的深层链接使用以下格式： `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span><span class="sxs-lookup"><span data-stu-id="37281-205">Use the following format for a deep link that you can use in a bot, Connector, or messaging extension card: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span></span>

<span data-ttu-id="37281-206">示例：`https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span><span class="sxs-lookup"><span data-stu-id="37281-206">Example: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span></span>

<span data-ttu-id="37281-207">查询参数包括：</span><span class="sxs-lookup"><span data-stu-id="37281-207">The query parameters are:</span></span>

* <span data-ttu-id="37281-208">`attendees`：表示会议与会者的用户 ID 的可选逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="37281-208">`attendees`: The optional comma-separated list of user IDs representing the attendees of the meeting.</span></span> <span data-ttu-id="37281-209">执行该操作的用户是会议组织者。</span><span class="sxs-lookup"><span data-stu-id="37281-209">The user performing the action is the meeting organizer.</span></span> <span data-ttu-id="37281-210">用户 ID 字段当前仅支持 Azure AD UserPrincipalName，通常为电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="37281-210">The User ID field currently only supports the Azure AD UserPrincipalName, typically an email address.</span></span>
* <span data-ttu-id="37281-211">`startTime`：事件的可选开始时间。</span><span class="sxs-lookup"><span data-stu-id="37281-211">`startTime`: The optional start time of the event.</span></span> <span data-ttu-id="37281-212">这应该采用长 [ISO 8601](https://en.wikipedia.org/wiki/ISO_8601)格式，例如"2018-03-12T23：55：25+02：00"。</span><span class="sxs-lookup"><span data-stu-id="37281-212">This should be in [long ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601), for example “2018-03-12T23:55:25+02:00”.</span></span>
* <span data-ttu-id="37281-213">`endTime`：事件的可选结束时间，也采用 ISO 8601 格式。</span><span class="sxs-lookup"><span data-stu-id="37281-213">`endTime`: The optional end time of the event, also in ISO 8601 format.</span></span>
* <span data-ttu-id="37281-214">`subject`：会议主题的可选字段。</span><span class="sxs-lookup"><span data-stu-id="37281-214">`subject`: An optional field for the meeting subject.</span></span>
* <span data-ttu-id="37281-215">`content`：会议详细信息字段的可选字段。</span><span class="sxs-lookup"><span data-stu-id="37281-215">`content`: An optional field for the meeting details field.</span></span>

<span data-ttu-id="37281-216">目前不支持指定位置。</span><span class="sxs-lookup"><span data-stu-id="37281-216">Currently, specifying the location is not supported.</span></span> <span data-ttu-id="37281-217">你必须指定 UTC 偏移量，这意味着生成开始时间和结束时间时时区。</span><span class="sxs-lookup"><span data-stu-id="37281-217">You must specify the UTC offset, it means time zones when generating your start and end times.</span></span>

<span data-ttu-id="37281-218">若要将此深层链接与自动程序一同使用，可以在卡片按钮中指定此链接作为 URL 目标，或点击操作类型的 `openUrl` 操作。</span><span class="sxs-lookup"><span data-stu-id="37281-218">To use this deep link with your bot, you can specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>
