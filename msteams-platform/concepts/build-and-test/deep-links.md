---
title: 创建深层链接
description: 介绍深层链接以及如何在应用程序中使用它们
keywords: 团队深层链接 deeplink
ms.openlocfilehash: 03580c4d15c82da70402d68d85b0d28f8afa670e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673360"
---
# <a name="create-deep-links-to-content-and-features-in-microsoft-teams"></a><span data-ttu-id="4dcb9-104">创建指向 Microsoft 团队中的内容和功能的深层链接</span><span class="sxs-lookup"><span data-stu-id="4dcb9-104">Create deep links to content and features in Microsoft Teams</span></span>

<span data-ttu-id="4dcb9-105">您可以创建指向团队客户端中的信息和功能的链接。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-105">You can create links to information and features within the Teams client.</span></span> <span data-ttu-id="4dcb9-106">这可能有用的示例：</span><span class="sxs-lookup"><span data-stu-id="4dcb9-106">Examples of where this may be useful:</span></span>

* <span data-ttu-id="4dcb9-107">将用户导航到某个应用程序的选项卡中的内容。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-107">Navigating the user to content within one of your app's tabs.</span></span> <span data-ttu-id="4dcb9-108">例如，您的应用程序可能有一个用于发送通知用户重要活动的邮件的 bot。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-108">For instance, your app may have a bot that sends messages notifying the user of an important activity.</span></span> <span data-ttu-id="4dcb9-109">当用户点击通知时，深层链接将导航到 "" 选项卡，以便用户可以查看有关活动的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-109">When the user taps on the notification, the deep link navigates to the tab so the user can view more details about the activity.</span></span>
* <span data-ttu-id="4dcb9-110">您的应用程序通过使用所需参数预填充深层链接来自动执行或简化某些用户任务，如创建聊天或安排会议。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-110">Your app automates or simplifies certain user tasks, such as creating a chat or scheduling a meeting, by pre-populating the deep links with required parameters.</span></span> <span data-ttu-id="4dcb9-111">这样，用户就无需手动输入信息。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-111">This avoids the need for users to manually enter information.</span></span>

## <a name="deep-linking-to-your-tab"></a><span data-ttu-id="4dcb9-112">深度链接到你的选项卡</span><span class="sxs-lookup"><span data-stu-id="4dcb9-112">Deep linking to your tab</span></span>

<span data-ttu-id="4dcb9-113">您可以创建指向团队中的实体的深层链接。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-113">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="4dcb9-114">通常，这用于创建导航到您的选项卡中的内容和信息的链接。例如，如果您的选项卡中包含任务列表工作组成员可以创建和共享单个任务的链接。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-114">Typically, this is used to create links that navigate to content and information within your tab. For example, if your tab contains a task list team members may create and share links to individual tasks.</span></span> <span data-ttu-id="4dcb9-115">单击时，链接将导航到重点关注特定项目的选项卡。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-115">When clicked, the link navigates to your tab which focuses on the specific item.</span></span> <span data-ttu-id="4dcb9-116">若要实现此目的，请为每个项目添加 "复制链接" 操作，采用最适合您的 UI 的任何方式。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-116">To implement this, you add a "copy link" action to each item, in whatever way best suits your UI.</span></span> <span data-ttu-id="4dcb9-117">当用户执行此操作时，将调用`shareDeepLink()`以显示一个对话框，其中包含用户可以复制到剪贴板的链接。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-117">When the user takes this action, you call `shareDeepLink()` to display a dialog box containing a link that the user can copy to the clipboard.</span></span> <span data-ttu-id="4dcb9-118">在进行此调用时，还会为您的项目传递一个 ID，在后续[链接时，](~/tabs/how-to/access-teams-context.md)将返回该 ID，并且重新加载您的选项卡。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-118">When you make this call, you also pass an ID for your item, which you get back in the [context](~/tabs/how-to/access-teams-context.md) when the link is followed and your tab is reloaded.</span></span>

<span data-ttu-id="4dcb9-119">或者，也可以使用本主题后面所指定的格式以编程方式生成深层链接。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-119">Alternatively, you can also generate deep links programmatically, using the format specified later in this topic.</span></span> <span data-ttu-id="4dcb9-120">您可能需要在[机器人](~/bots/what-are-bots.md)和[连接器](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md)消息中使用这些选项，以告知用户对您的选项卡或其中的项目所做的更改。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-120">You might want to use these in [bot](~/bots/what-are-bots.md) and [Connector](~/webhooks-and-connectors/what-are-webhooks-and-connectors.md) messages that inform users about changes to your tab, or to items within it.</span></span>

> [!NOTE]
> <span data-ttu-id="4dcb9-121">这不同于**复制指向选项卡**菜单项的链接提供的链接，它只生成指向此选项卡的深层链接。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-121">This is different from the links provided by the **Copy link to tab** menu item, which just generates a deep link that points to this tab.</span></span>

### <a name="showing-a-deep-link-to-an-item-within-your-tab"></a><span data-ttu-id="4dcb9-122">在选项卡中显示指向某个项目的深层链接</span><span class="sxs-lookup"><span data-stu-id="4dcb9-122">Showing a deep link to an item within your tab</span></span>

<span data-ttu-id="4dcb9-123">若要显示一个对话框，其中包含指向您的选项卡中的项的深层链接，请调用`microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`</span><span class="sxs-lookup"><span data-stu-id="4dcb9-123">To show a dialog box that contains a deep link to an item within your tab, call `microsoftTeams.shareDeepLink({ subEntityId: <subEntityId>, subEntityLabel: <subEntityLabel>, subEntityWebUrl: <subEntityWebUrl> })`</span></span>

<span data-ttu-id="4dcb9-124">提供以下字段：</span><span class="sxs-lookup"><span data-stu-id="4dcb9-124">Provide these fields:</span></span>

* <span data-ttu-id="4dcb9-125">`subEntityId`&emsp;选项卡中您要深度链接的项的唯一标识符</span><span class="sxs-lookup"><span data-stu-id="4dcb9-125">`subEntityId`&emsp;A unique identifier for the item within your tab to which you are deep linking</span></span>
* <span data-ttu-id="4dcb9-126">`subEntityLabel`&emsp;用于显示深层链接的项的标签</span><span class="sxs-lookup"><span data-stu-id="4dcb9-126">`subEntityLabel`&emsp;A label for the item to use for displaying the deep link</span></span>
* <span data-ttu-id="4dcb9-127">`subEntityWebUrl`&emsp;一个可选字段，如果客户端不支持呈现该选项卡，则为要使用的回退 URL</span><span class="sxs-lookup"><span data-stu-id="4dcb9-127">`subEntityWebUrl`&emsp;An optional field with a fallback URL to use if the client does not support rendering the tab</span></span>

### <a name="generating-a-deep-link-to-your-tab"></a><span data-ttu-id="4dcb9-128">生成指向您的选项卡的深层链接</span><span class="sxs-lookup"><span data-stu-id="4dcb9-128">Generating a deep link to your tab</span></span>

> [!NOTE]
> <span data-ttu-id="4dcb9-129">静态选项卡的作用域为 "个人"，且可配置的选项卡的作用域为 "team"。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-129">Static tabs have a scope of "personal" and configurable tabs have a scope of "team".</span></span> <span data-ttu-id="4dcb9-130">由于只有可配置的选项卡具有与其上下文对象相关联的`channel`属性，这两个选项卡类型的语法略有不同。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-130">The two tab types have a slightly different syntax since only the configurable tab has a `channel` property associated with its context object.</span></span> <span data-ttu-id="4dcb9-131">有关个人和团队作用域的详细信息，请参阅[清单](~/resources/schema/manifest-schema.md)参考。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-131">See the [Manifest](~/resources/schema/manifest-schema.md) reference for more information on personal and team scopes.</span></span>
> [!NOTE]
> <span data-ttu-id="4dcb9-132">仅当选项卡是使用 v 0.4 或更高版本库配置的，并且由于具有实体 ID 时，Deep 链接才会正常工作。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-132">Deep links work properly only if the tab was configured using the v0.4 or later library and because of that has an entity ID.</span></span> <span data-ttu-id="4dcb9-133">指向不含实体 Id 的选项卡的深层链接仍会导航到选项卡，但不能向该选项卡提供子实体 ID。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-133">Deep links to tabs without entity IDs still navigate to the tab but can't provide the sub-entity ID to the tab.</span></span>

<span data-ttu-id="4dcb9-134">此格式适用于您可以在机器人、连接器或邮件扩充卡中使用的深层链接：</span><span class="sxs-lookup"><span data-stu-id="4dcb9-134">Use this format for a deep link that you can use in a bot, Connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/entity/<appId>/<entityId>?webUrl=<entityWebUrl>&label=<entityLabel>&context=<context>`

<span data-ttu-id="4dcb9-135">查询参数为：</span><span class="sxs-lookup"><span data-stu-id="4dcb9-135">The query parameters are:</span></span>

* <span data-ttu-id="4dcb9-136">`appId`&emsp;清单中的 ID;例如，"fe4a8eba-2a31-4737-8e33-e5fae6fee194"</span><span class="sxs-lookup"><span data-stu-id="4dcb9-136">`appId`&emsp;The ID from your manifest; for example, "fe4a8eba-2a31-4737-8e33-e5fae6fee194"</span></span>
* <span data-ttu-id="4dcb9-137">`entityId`&emsp;选项卡中的项的 ID，在[配置选项卡](~/tabs/how-to/create-tab-pages/configuration-page.md)时提供;例如，"tasklist123"</span><span class="sxs-lookup"><span data-stu-id="4dcb9-137">`entityId`&emsp;The ID for the item in the tab, which you provided when [configuring the tab](~/tabs/how-to/create-tab-pages/configuration-page.md); for example, "tasklist123"</span></span>
* <span data-ttu-id="4dcb9-138">`entityWebUrl`或者`subEntityWebUrl` &emsp;一个可选字段，如果客户端不支持呈现该选项卡，则为要使用的回退 URL;例如，"https://tasklist.example.com/123" 或 "https://tasklist.example.com/list123/task456"</span><span class="sxs-lookup"><span data-stu-id="4dcb9-138">`entityWebUrl` or `subEntityWebUrl`&emsp;An optional field with a fallback URL to use if the client does not support rendering the tab; for example, "https://tasklist.example.com/123" or "https://tasklist.example.com/list123/task456"</span></span>
* <span data-ttu-id="4dcb9-139">`entityLabel`或`subEntityLabel` &emsp;选项卡中项的标签，以在显示深层链接时使用;例如，"任务列表 123" 或 "任务 456"</span><span class="sxs-lookup"><span data-stu-id="4dcb9-139">`entityLabel` or `subEntityLabel`&emsp;A label for the item in your tab, to use when displaying the deep link; for example, "Task List 123" or "Task 456"</span></span>
* <span data-ttu-id="4dcb9-140">`context`&emsp;一个包含以下字段的 JSON 对象：</span><span class="sxs-lookup"><span data-stu-id="4dcb9-140">`context`&emsp;A JSON object containing the following fields:</span></span>
  * <span data-ttu-id="4dcb9-141">`subEntityId`&emsp;选项卡_中_项的 ID;例如，"task456"</span><span class="sxs-lookup"><span data-stu-id="4dcb9-141">`subEntityId`&emsp;An ID for the item _within_ the tab; for example, "task456"</span></span>
  * <span data-ttu-id="4dcb9-142">`channelId`&emsp;Microsoft 团队频道 ID （可从选项卡[上下文](~/tabs/how-to/access-teams-context.md)中查看; 例如，"19： cbe3683f25094106b826c9cada3afbe0@thread skype"。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-142">`channelId`&emsp;The Microsoft Teams channel ID (available from the tab [context](~/tabs/how-to/access-teams-context.md); for example, "19:cbe3683f25094106b826c9cada3afbe0@thread.skype".</span></span> <span data-ttu-id="4dcb9-143">此属性仅在作用域为 "team" 的可配置选项卡中可用。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-143">This property is only available in configurable tabs with a scope of "team".</span></span> <span data-ttu-id="4dcb9-144">它在具有 "个人" 范围的静态选项卡中不可用。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-144">It is not available in static tabs, which have a scope of "personal".</span></span>

<span data-ttu-id="4dcb9-145">示例：</span><span class="sxs-lookup"><span data-stu-id="4dcb9-145">Examples:</span></span>

* <span data-ttu-id="4dcb9-146">链接到可配置的选项卡本身：`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="4dcb9-146">Link to a configurable tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123&context={"channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="4dcb9-147">链接到 "可配置" 选项卡中的任务项：`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span><span class="sxs-lookup"><span data-stu-id="4dcb9-147">Link to a task item within the configurable tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456","channelId": "19:cbe3683f25094106b826c9cada3afbe0@thread.skype"}`</span></span>
* <span data-ttu-id="4dcb9-148">指向静态选项卡本身的链接：`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span><span class="sxs-lookup"><span data-stu-id="4dcb9-148">Link to a static tab itself: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123&label=Task List 123`</span></span>
* <span data-ttu-id="4dcb9-149">链接到静态选项卡中的任务项：`https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span><span class="sxs-lookup"><span data-stu-id="4dcb9-149">Link to a task item within the static tab: `https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=https://tasklist.example.com/123/456&label=Task 456&context={"subEntityId": "task456"}`</span></span>

> [!IMPORTANT]
> <span data-ttu-id="4dcb9-150">确保所有查询参数都经过了正确的 URI 编码。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-150">Ensure that all query parameters are properly URI encoded.</span></span> <span data-ttu-id="4dcb9-151">为了提高可读性，以上示例不是，但您应该这样做。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-151">For the sake of readability, the above examples are not, but you should.</span></span> <span data-ttu-id="4dcb9-152">使用最后一个示例：</span><span class="sxs-lookup"><span data-stu-id="4dcb9-152">Using the last example:</span></span>
> ```javascript
> var encodedWebUrl = encodeURI('https://tasklist.example.com/123/456&label=Task 456');
> var encodedContext = encodeURI('{"subEntityId": "task456"}');
> var taskItemUrl = 'https://teams.microsoft.com/l/entity/fe4a8eba-2a31-4737-8e33-e5fae6fee194/tasklist123?webUrl=' + encodedWebUrl + '&context=' + encodedContext;
> ```

### <a name="consuming-a-deep-link-from-a-tab"></a><span data-ttu-id="4dcb9-153">从选项卡中使用深层链接</span><span class="sxs-lookup"><span data-stu-id="4dcb9-153">Consuming a deep link from a tab</span></span>

<span data-ttu-id="4dcb9-154">导航到深层链接时，Microsoft 团队只需导航到该选项卡，并通过 Microsoft 团队 JavaScript 库提供一种方法来检索子实体 ID （如果存在）。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-154">When navigating to a deep link, Microsoft Teams simply navigates to the tab and provides a mechanism via the Microsoft Teams JavaScript library to retrieve the sub-entity ID (if it exists).</span></span>

<span data-ttu-id="4dcb9-155">如果[`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-)通过深层链接将选项卡导航`subEntityId`到该字段，则调用将返回一个包含该字段的上下文。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-155">The [`microsoftTeams.getContext`](/javascript/api/@microsoft/teams-js#getcontext--context--context-----void-) call returns a context that includes the `subEntityId` field if the tab was navigated to via a deep link.</span></span>

## <a name="deep-linking-from-your-tab"></a><span data-ttu-id="4dcb9-156">从你的选项卡深层链接</span><span class="sxs-lookup"><span data-stu-id="4dcb9-156">Deep linking from your tab</span></span>

<span data-ttu-id="4dcb9-157">您可以从选项卡中 deeplink 到工作组中的内容。如果您的选项卡需要链接到团队中的其他内容（如频道、邮件、另一个选项卡或甚至打开日程安排对话框），这将非常有用。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-157">You can deeplink to content in Teams from your tab. This is useful if your tab needs to link to other content in Teams such as to a channel, message, another tab or even to open a scheduling dialog.</span></span> <span data-ttu-id="4dcb9-158">若要从您的选项卡触发 deeplink，应调用：</span><span class="sxs-lookup"><span data-stu-id="4dcb9-158">To trigger a deeplink from your tab you should call:</span></span>

```Javascript
microsoftTeams.executeDeepLink(/*deepLink*/);
```

<span data-ttu-id="4dcb9-159">此操作将导航到正确的 URL，或触发客户端操作，如打开计划或应用程序安装对话框。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-159">This will navigate you to the correct URL, or trigger a client action such as opening a scheduling or app install dialog.</span></span> <span data-ttu-id="4dcb9-160">示例：</span><span class="sxs-lookup"><span data-stu-id="4dcb9-160">Example:</span></span>

```Javascript
// Open a scheduling dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent");

// Open an app install dialog from your tab
microsoftTeams.executeDeepLink("https://teams.microsoft.com/l/app/f46ad259-0fe5-4f12-872d-c737b174bcb4");
```

## <a name="deep-linking-to-a-chat"></a><span data-ttu-id="4dcb9-161">深层链接到聊天</span><span class="sxs-lookup"><span data-stu-id="4dcb9-161">Deep linking to a chat</span></span>

<span data-ttu-id="4dcb9-162">您可以通过指定一组参与者来创建到用户之间的私人聊天的深层链接。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-162">You can create deep links to private chats between users by specifying the set of participants.</span></span> <span data-ttu-id="4dcb9-163">如果不存在与指定参与者的聊天，该链接将导航用户到空的新聊天。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-163">If a chat doesn't exist with the specified participants, the link will navigate the user to an empty new chat.</span></span> <span data-ttu-id="4dcb9-164">新聊天将在草稿状态中创建，直到用户发送第一封邮件。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-164">New chats will be created in draft state until the user sends the first message.</span></span> <span data-ttu-id="4dcb9-165">（可选）您可以指定聊天的名称（如果尚不存在）以及应插入到用户的 "撰写" 框中的文本。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-165">Optionally, you can specify the name of the chat (if it doesn't already exist), along with text that should be inserted into the user's compose box.</span></span> <span data-ttu-id="4dcb9-166">您可以将此功能视为用户执行导航或创建聊天的手动操作，然后键入邮件的快捷方式。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-166">You can think of this feature as a shortcut for the user taking the manual action of navigating to or creating the chat, and then typing out the message.</span></span>

<span data-ttu-id="4dcb9-167">例如，如果您以卡片形式返回来自 bot 的 Office 365 用户配置文件，此深层链接可以让用户轻松地与此人聊天。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-167">As an example use case, if you are returning an Office 365 user profile from your bot as a card, this deep link can allow the user to easily chat with that person.</span></span>

### <a name="generating-a-deep-link-to-a-chat"></a><span data-ttu-id="4dcb9-168">生成指向聊天的深层链接</span><span class="sxs-lookup"><span data-stu-id="4dcb9-168">Generating a deep link to a chat</span></span>

<span data-ttu-id="4dcb9-169">此格式适用于您可以在机器人、连接器或邮件扩充卡中使用的深层链接：</span><span class="sxs-lookup"><span data-stu-id="4dcb9-169">Use this format for a deep link that you can use in a bot, Connector, or messaging extension card:</span></span>

`https://teams.microsoft.com/l/chat/0/0?users=<user1>,<user2>,...&topicName=<chat name>&message=<precanned text>`

<span data-ttu-id="4dcb9-170">示例：`https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span><span class="sxs-lookup"><span data-stu-id="4dcb9-170">Example: `https://teams.microsoft.com/l/chat/0/0?users=joe@contoso.com,bob@contoso.com&topicName=Prep%20For%20Meeting%20Tomorrow&message=Hi%20folks%2C%20kicking%20off%20a%20chat%20about%20our%20meeting%20tomorrow`</span></span>

<span data-ttu-id="4dcb9-171">查询参数为：</span><span class="sxs-lookup"><span data-stu-id="4dcb9-171">The query parameters are:</span></span>

* <span data-ttu-id="4dcb9-172">`users`&emsp;代表聊天参与者的用户 Id 的逗号分隔列表。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-172">`users`&emsp;The comma-separated list of user IDs representing the participants of the chat.</span></span> <span data-ttu-id="4dcb9-173">执行操作的用户始终作为参与者加入。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-173">The user performing the action is always included as a participant.</span></span> <span data-ttu-id="4dcb9-174">"User ID" 字段当前仅支持 Azure AD UserPrincipalName （通常为电子邮件地址）。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-174">The User ID field currently only supports the Azure AD UserPrincipalName (typically an email address).</span></span>
* <span data-ttu-id="4dcb9-175">`topicName`&emsp;用于聊天的显示名称的可选字段，在与3个或更多用户聊天的情况下。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-175">`topicName`&emsp;An optional field for chat's display name, in the case of a chat with 3 or more users.</span></span> <span data-ttu-id="4dcb9-176">如果未指定此字段，则聊天的显示名称将基于参与者的名称。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-176">If this field is not specified, the chat's display name will be based on the names of the participants.</span></span>
* <span data-ttu-id="4dcb9-177">`message`&emsp;在聊天处于草稿状态时要插入到当前用户的撰写框中的邮件文本的可选字段。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-177">`message`&emsp;An optional field for the message text that you want to insert into the current user's compose box while the chat is in a draft state.</span></span>

<span data-ttu-id="4dcb9-178">若要使用与你的 bot 的深层链接，你可以将其指定为你的卡片按钮中的 URL 目标，或`openUrl`通过操作类型点击操作。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-178">To use this deep link with your bot, you can specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>

## <a name="linking-to-the-scheduling-dialog"></a><span data-ttu-id="4dcb9-179">链接到计划对话框</span><span class="sxs-lookup"><span data-stu-id="4dcb9-179">Linking to the scheduling dialog</span></span>

> [!Note]
> <span data-ttu-id="4dcb9-180">此功能当前处于开发人员预览版中。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-180">This feature is currently in developer preview.</span></span>

<span data-ttu-id="4dcb9-181">您可以创建指向团队客户端的内置日程安排对话框的深层链接。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-181">You can create deep links to the Teams client's built-in scheduling dialog.</span></span> <span data-ttu-id="4dcb9-182">如果您的应用程序可帮助用户完成日历或与日程排定相关的任务，这将非常有用。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-182">This is especially useful if your app helps the user complete calendar or scheduling-related tasks.</span></span>

### <a name="generating-a-deep-link-to-the-scheduling-dialog"></a><span data-ttu-id="4dcb9-183">生成指向日程安排对话框的深层链接</span><span class="sxs-lookup"><span data-stu-id="4dcb9-183">Generating a deep link to the scheduling dialog</span></span>

<span data-ttu-id="4dcb9-184">此格式适用于您可以在机器人、连接器或邮件扩充卡中使用的深层链接：`https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span><span class="sxs-lookup"><span data-stu-id="4dcb9-184">Use this format for a deep link that you can use in a bot, Connector, or messaging extension card: `https://teams.microsoft.com/l/meeting/new?subject=<meeting subject>&startTime=<date>&endTime=<date>&content=<content>&attendees=<user1>,<user2>,<user3>,...`</span></span>

<span data-ttu-id="4dcb9-185">示例：`https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span><span class="sxs-lookup"><span data-stu-id="4dcb9-185">Example: `https://teams.microsoft.com/l/meeting/new?subject=test%20subject&attendees=joe@contoso.com,bob@contoso.com&startTime=10%2F24%2F2018%2010%3A30%3A00&endTime=10%2F24%2F2018%2010%3A30%3A00&content=test%3Acontent`</span></span>

<span data-ttu-id="4dcb9-186">查询参数为：</span><span class="sxs-lookup"><span data-stu-id="4dcb9-186">The query parameters are:</span></span>

* <span data-ttu-id="4dcb9-187">`attendees`&emsp;可选的以逗号分隔的用户 Id 列表，表示会议的与会者。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-187">`attendees`&emsp;The optional comma-separated list of user IDs representing the attendees of the meeting.</span></span> <span data-ttu-id="4dcb9-188">执行操作的用户是会议组织者。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-188">The user performing the action is the meeting organizer.</span></span> <span data-ttu-id="4dcb9-189">"User ID" 字段当前仅支持 Azure AD UserPrincipalName （通常为电子邮件地址）。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-189">The User ID field currently only supports the Azure AD UserPrincipalName (typically an email address).</span></span>
* <span data-ttu-id="4dcb9-190">`startTime`&emsp;事件的可选开始时间。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-190">`startTime`&emsp;The optional start time of the event.</span></span> <span data-ttu-id="4dcb9-191">这应采用[ISO 8601 的长格式](https://en.wikipedia.org/wiki/ISO_8601)，例如 "2018-03-12T23：55： 25 + 02： 00"。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-191">This should be in [long ISO 8601 format](https://en.wikipedia.org/wiki/ISO_8601), for example “2018-03-12T23:55:25+02:00”.</span></span>
* <span data-ttu-id="4dcb9-192">`endTime`&emsp;事件的可选结束时间，也是 ISO 8601 格式。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-192">`endTime`&emsp;The optional end time of the event, also in ISO 8601 format.</span></span>
* <span data-ttu-id="4dcb9-193">`subject`&emsp;会议主题的可选字段。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-193">`subject`&emsp;An optional field for the meeting subject.</span></span>
* <span data-ttu-id="4dcb9-194">`content`&emsp;"会议详细信息" 域的可选字段。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-194">`content`&emsp;An optional field for the meeting details field.</span></span>

<span data-ttu-id="4dcb9-195">目前，不支持指定位置。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-195">Currently, specifying the location is not supported.</span></span> <span data-ttu-id="4dcb9-196">在生成开始和结束时间时，请务必指定 UTC 偏移量（时区）。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-196">When generating your start and end times be sure to specify the UTC offset (time zones).</span></span>

<span data-ttu-id="4dcb9-197">若要使用与你的 bot 的深层链接，你可以将其指定为你的卡片按钮中的 URL 目标，或`openUrl`通过操作类型点击操作。</span><span class="sxs-lookup"><span data-stu-id="4dcb9-197">To use this deep link with your bot, you can specify this as the URL target in your card's button or tap action through the `openUrl` action type.</span></span>
