---
title: 什么是团队中的自定义选项卡？
author: laujan
description: 团队平台上的自定义选项卡概述
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: e89f07133f86b6c0700e6a71d8e53bf6d9831196
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576846"
---
# <a name="what-are-microsoft-teams-custom-tabs"></a><span data-ttu-id="f6e0e-103">什么是 Microsoft 团队自定义选项卡？</span><span class="sxs-lookup"><span data-stu-id="f6e0e-103">What are Microsoft Teams custom tabs?</span></span>

<span data-ttu-id="f6e0e-104">选项卡是嵌入在 Microsoft 团队中的团队感知网页。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-104">Tabs are Teams-aware webpages embedded in Microsoft Teams.</span></span> <span data-ttu-id="f6e0e-105">它们是简单的 HTML <iframe \> 标记，指向应用程序清单中声明的域，可以作为单个用户的团队、组聊天或个人应用程序内的频道的一部分添加。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-105">They are simple HTML <iframe\> tags that point to domains declared in the app manifest and can be added as part of a channel inside a team, group chat, or personal app for an individual user.</span></span> <span data-ttu-id="f6e0e-106">您可以将自定义选项卡包含在您的应用程序中，以在工作组中嵌入自己的 web 内容或向 web 内容添加特定于团队的功能。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-106">You can include custom tabs with your app to embed your own web content in Teams or add Teams-specific functionality to your web content.</span></span> <span data-ttu-id="f6e0e-107">*请参阅*[团队 JAVASCRIPT 客户端 SDK](/javascript/api/overview/msteams-client)。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-107">*See* [Teams JavaScript client SDK](/javascript/api/overview/msteams-client).</span></span>

> [!NOTE]
> <span data-ttu-id="f6e0e-108">Chrome 80，安排在早期2020中发布，默认引入新的 cookie 值并强加 cookie 策略。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-108">Chrome 80, scheduled for release in early 2020, introduces new cookie values and imposes cookie policies by default.</span></span> <span data-ttu-id="f6e0e-109">建议您为 cookie 设置预期用途，而不是依赖于默认浏览器行为。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-109">It's recommended that you set the intended use for your cookies rather than rely on default browser behavior.</span></span> <span data-ttu-id="f6e0e-110">*请参阅* [SameSite cookie 属性 (2020 update)](../resources/samesite-cookie-update.md)。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-110">*See* [SameSite cookie attribute (2020 update)](../resources/samesite-cookie-update.md).</span></span>

<span data-ttu-id="f6e0e-111">在团队中提供了两种类型的选项卡：渠道/组和个人。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-111">There are two types of tabs available in Teams — channel/group and personal.</span></span> <span data-ttu-id="f6e0e-112">频道/组选项卡可将内容传递到频道和组聊天，这是在专门的基于 web 的内容周围创建协作空间的绝佳方式。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-112">Channel/group tabs deliver content to channels and group chats, and are a great way to create collaborative spaces around dedicated web-based content.</span></span> <span data-ttu-id="f6e0e-113">个人选项卡和个人范围的 bot 是个人应用程序的一部分，且范围限定为单个用户。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-113">Personal tabs, along with personally-scoped bots, are part of personal apps and are scoped to a single user.</span></span> <span data-ttu-id="f6e0e-114">可以将它们固定到左侧导航栏以方便访问。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-114">They can be pinned to the left navigation bar for easy access.</span></span>

## <a name="lesser-known-tab-features"></a><span data-ttu-id="f6e0e-115">较低的已知选项卡功能</span><span class="sxs-lookup"><span data-stu-id="f6e0e-115">Lesser known tab features</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="f6e0e-116">如果将某个选项卡添加到也具有 bot 的应用程序中，则也会将该 bot 添加到团队中。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-116">If a tab is added to an app that also has a bot, the bot is added to the team as well.</span></span>
> * <span data-ttu-id="f6e0e-117">感知 Azure Active Directory (Azure AD) 当前用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-117">Awareness of Azure Active Directory (Azure AD) ID of the current user.</span></span>
> * <span data-ttu-id="f6e0e-118">用户的区域设置感知以指示语言，即， `en-us` 。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-118">Locale awareness for the user to indicate language, i.e., `en-us`.</span></span> 
> * <span data-ttu-id="f6e0e-119">单一登录 (SSO) 功能（如果支持）。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-119">Single sign-on (SSO) capability, if supported.</span></span>
> * <span data-ttu-id="f6e0e-120">能够使用 bot 或应用程序通知深入链接到选项卡或服务内的子实体（例如，单个工作项）。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-120">Ability to use bots or app notifications to deep link to the tab or to a sub-entity within the service, e.g., an individual work item.</span></span>
> * <span data-ttu-id="f6e0e-121">通过选项卡中的链接打开任务模块的功能。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-121">The ability to open a task module from links within a tab.</span></span>
> * <span data-ttu-id="f6e0e-122">在选项卡中重用 SharePoint web 部件。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-122">Reuse of SharePoint web parts within the tab.</span></span>

## <a name="tabs-user-scenarios"></a><span data-ttu-id="f6e0e-123">选项卡用户方案</span><span class="sxs-lookup"><span data-stu-id="f6e0e-123">Tabs user scenarios</span></span>

<span data-ttu-id="f6e0e-124">**方案：** 将现有的基于 web 的资源引入团队中。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-124">**Scenario:** Bring an existing web-based resource inside Teams.</span></span> \
<span data-ttu-id="f6e0e-125">**示例：** 您在团队应用程序中创建了一个个人选项卡，用于向用户提供信息性企业网站。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-125">**Example:** You create a personal tab in your Teams app that presents an informational corporate website to users.</span></span>

<span data-ttu-id="f6e0e-126">**方案：** 将支持页面添加到团队 bot 或邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-126">**Scenario:** Add support pages to a Teams bot or messaging extension.</span></span> \
<span data-ttu-id="f6e0e-127">**示例：** 您可以为用户 *创建向用户提供 "* 帮助" 和 " *帮助* " 网页内容的个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-127">**Example:** You create personal tabs that provide *about* and *help* webpage content to users.</span></span>

<span data-ttu-id="f6e0e-128">**方案：** 提供对用户定期与协作对话和协作进行交互的项目的访问。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-128">**Scenario:** Provide access to items that your users interact with regularly for cooperative dialogue and collaboration.</span></span> \
<span data-ttu-id="f6e0e-129">**示例：** 您可以创建一个通道/组选项卡，其中包含对各个项目的深层链接。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-129">**Example:** You create a channel/group tab with deep linking to individual items.</span></span>

## <a name="how-do-tabs-work"></a><span data-ttu-id="f6e0e-130">选项卡如何工作？</span><span class="sxs-lookup"><span data-stu-id="f6e0e-130">How do tabs work?</span></span>

<span data-ttu-id="f6e0e-131">自定义选项卡在应用程序包的应用部件清单（manifest）中声明。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-131">A custom tab is declared in the app manifest of your app package.</span></span> <span data-ttu-id="f6e0e-132">对于您要在应用程序中包含为选项卡的每个网页，定义一个 URL 和一个作用域。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-132">For each webpage you want included as a tab in your app, you define a URL and a scope.</span></span> <span data-ttu-id="f6e0e-133">此外，还需要将 [团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client) 添加到页面，并在 `microsoftTeams.initialize()` 加载页面后调用。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-133">Additionally, you need to add the [Teams JavaScript client SDK](/javascript/api/overview/msteams-client) to your page, and call `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="f6e0e-134">如果这样做，将告知团队显示您的页面，使您可以访问特定于团队的信息 (例如，如果团队客户端运行的是 *深色主题*) ，并允许您根据结果执行操作。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-134">Doing so will tell Teams to display your page, give you access to Teams-specific information (for example if the Teams client is running the *dark theme*), and allow you to take action based on the results.</span></span>

<span data-ttu-id="f6e0e-135">无论您是否选择在频道/组或个人作用域中公开您的选项卡，您都需要 \> 在您的选项卡中提供 <iframe HTML [内容页](~/tabs/how-to/create-tab-pages/content-page.md) 。对于个人选项卡，通过数组中的属性直接在团队应用程序清单中设置内容 URL `contentUrl` `staticTabs` 。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-135">Whether you choose to expose your tab within the channel/group or personal scope, you'll need to present an <iframe\> HTML [content page](~/tabs/how-to/create-tab-pages/content-page.md) in your tab. For personal tabs, the content URL is set directly in your Teams app manifest by the `contentUrl` property in the `staticTabs` array.</span></span> <span data-ttu-id="f6e0e-136">您的选项卡的内容将对所有用户都相同。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-136">Your tab's content will be the same for all users.</span></span>

<span data-ttu-id="f6e0e-137">对于频道/组选项卡，还需要创建其他配置页面，以允许用户配置内容页面 URL，通常是使用 URL 查询字符串参数为该上下文加载相应的内容。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-137">For channel/group tabs, you also need to create an additional configuration page that allows users to configure your content page URL, typically by using URL query string parameters to load the appropriate content for that context.</span></span> <span data-ttu-id="f6e0e-138">这是因为您的频道/组选项卡可以添加到多个不同的团队或组聊天。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-138">This is because your channel/group tab can be added to multiple different teams or group chats.</span></span> <span data-ttu-id="f6e0e-139">在每次后续安装中，用户都可以配置选项卡，使您可以根据需要调整体验。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-139">On each subsequent install, your users will be able to configure the tab, allowing you to tailor the experience as needed.</span></span> <span data-ttu-id="f6e0e-140">当用户添加或配置选项卡时，会将 URL 与团队 UI 中显示的选项卡相关联。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-140">When users add or configure a tab, a URL is being associated with the tab that is presented in the Teams UI.</span></span> <span data-ttu-id="f6e0e-141">配置选项卡只是将其他参数添加到该 URL。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-141">Configuring a tab is simply adding additional parameters to that URL.</span></span> <span data-ttu-id="f6e0e-142">例如，在添加 "Azure 主板" 选项卡时，"配置" 页允许您选择选项卡将加载的板。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-142">For example, when you add the Azure Boards tab, the configuration page allows you to choose which board the tab will load.</span></span> <span data-ttu-id="f6e0e-143">配置页面 URL 由  `configurationUrl` `configurableTabs` 应用程序清单中的数组中的属性指定。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-143">The configuration page URL is specified by the  `configurationUrl` property in the `configurableTabs` array in your app manifest.</span></span>

<span data-ttu-id="f6e0e-144">最多可以有一个 (1) 频道/组选项卡，每个应用最多可以有十六个 (16) 个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-144">You can have a maximum of one (1) channel/group tab and up to sixteen (16) personal tabs per app.</span></span>

## <a name="mobile-clients"></a><span data-ttu-id="f6e0e-145">移动客户端</span><span class="sxs-lookup"><span data-stu-id="f6e0e-145">Mobile clients</span></span>

<span data-ttu-id="f6e0e-146">如果选择在工作组移动客户端上显示 "频道/组" 选项卡，则 `setSettings()` 配置必须具有该属性的值 `websiteUrl` 。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-146">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property.</span></span> <span data-ttu-id="f6e0e-147">为了确保获得最佳用户体验，在创建选项卡时，应遵循 [移动电话上的选项卡指南](~/tabs/design/tabs-mobile.md) 。</span><span class="sxs-lookup"><span data-stu-id="f6e0e-147">To ensure optimal user experience, you should follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f6e0e-148">了解详细信息：请求设备权限</span><span class="sxs-lookup"><span data-stu-id="f6e0e-148">Learn  more: Request device permissions</span></span>](/concepts/device-capabilities/native-device-permissions.md)

> [!div class="nextstepaction"]
>[<span data-ttu-id="f6e0e-149">了解详细信息：照相机和图像库权限</span><span class="sxs-lookup"><span data-stu-id="f6e0e-149">Learn more: Camera and image gallery permissions</span></span>](/concepts/device-capabilities/mobile-camera-image-permissions.md)