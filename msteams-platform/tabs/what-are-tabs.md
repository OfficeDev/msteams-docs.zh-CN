---
title: Microsoft Teams 选项卡
author: surbhigupta
description: 自定义选项卡在 Teams 概述
localization_priority: Normal
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 1564d7410cd0ce18d27afbbb3729cc30cfcfc4f6
ms.sourcegitcommit: 4d9d1542e04abacfb252511c665a7229d8bb7162
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/25/2021
ms.locfileid: "53140158"
---
# <a name="microsoft-teams-tabs"></a><span data-ttu-id="db006-103">Microsoft Teams 选项卡</span><span class="sxs-lookup"><span data-stu-id="db006-103">Microsoft Teams tabs</span></span>

<span data-ttu-id="db006-104">选项卡是Teams网页中嵌入的可感知Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="db006-104">Tabs are Teams-aware webpages embedded in Microsoft Teams.</span></span> <span data-ttu-id="db006-105">它们是简单的 HTML <iframe 标记，这些标记指向在应用程序清单中声明的域，并可以添加为单个用户的团队、群聊或个人应用中的频道的一 \> 部分。</span><span class="sxs-lookup"><span data-stu-id="db006-105">They are simple HTML <iframe\> tags that point to domains declared in the app manifest and can be added as part of a channel inside a team, group chat, or personal app for an individual user.</span></span> <span data-ttu-id="db006-106">可以将自定义选项卡与你的应用一起，以将自己的 Web 内容嵌入Teams或Teams Web 内容添加特定于 Web 的功能。</span><span class="sxs-lookup"><span data-stu-id="db006-106">You can include custom tabs with your app to embed your own web content in Teams or add Teams-specific functionality to your web content.</span></span> <span data-ttu-id="db006-107">有关详细信息，请参阅[javaScript Teams SDK。](/javascript/api/overview/msteams-client)</span><span class="sxs-lookup"><span data-stu-id="db006-107">For more information, see [Teams JavaScript client SDK](/javascript/api/overview/msteams-client).</span></span>

<span data-ttu-id="db006-108">下图显示了 Contoso 频道选项卡：</span><span class="sxs-lookup"><span data-stu-id="db006-108">The following image shows Contoso channel tabs:</span></span>

![频道或组和个人选项卡](../assets/images/tabs/tabs.png)

> [!VIDEO https://www.youtube-nocookie.com/embed/Jw6i7Mkt0dg]


> [!VIDEO https://www.youtube-nocookie.com/embed/T2a8yJC3VcQ]

<span data-ttu-id="db006-110">在选项卡上工作之前，必须完成一些先决条件。</span><span class="sxs-lookup"><span data-stu-id="db006-110">There are few prerequisites that you must go through before working on tabs.</span></span>

<span data-ttu-id="db006-111">有两种类型的选项卡可用于Teams个人选项卡和频道或组。</span><span class="sxs-lookup"><span data-stu-id="db006-111">There are two types of tabs available in Teams, personal and channel or group.</span></span> <span data-ttu-id="db006-112">[个人选项卡](~/tabs/how-to/create-personal-tab.md)和个人范围的自动程序是个人应用的一部分，并且范围为单个用户。</span><span class="sxs-lookup"><span data-stu-id="db006-112">[Personal tabs](~/tabs/how-to/create-personal-tab.md), along with personally-scoped bots, are part of personal apps and are scoped to a single user.</span></span> <span data-ttu-id="db006-113">它们可固定到左侧导航栏，便于访问。</span><span class="sxs-lookup"><span data-stu-id="db006-113">They can be pinned to the left navigation bar for easy access.</span></span> <span data-ttu-id="db006-114">[频道或组选项卡](~/tabs/how-to/create-channel-group-tab.md) 向频道和群聊提供内容，是围绕基于 Web 的专用内容创建协作空间的一种很好的方法。</span><span class="sxs-lookup"><span data-stu-id="db006-114">[Channel or group tabs](~/tabs/how-to/create-channel-group-tab.md) deliver content to channels and group chats, and are a great way to create collaborative spaces around dedicated web-based content.</span></span>

<span data-ttu-id="db006-115">您可以将 [内容页创建](~/tabs/how-to/create-tab-pages/content-page.md) 为个人选项卡、频道或组选项卡或任务模块的一部分。</span><span class="sxs-lookup"><span data-stu-id="db006-115">You can [create a content page](~/tabs/how-to/create-tab-pages/content-page.md) as part of a personal tab, channel or group tab, or task module.</span></span> <span data-ttu-id="db006-116">您可以创建[一个配置](~/tabs/how-to/create-tab-pages/configuration-page.md)页，使用户能够配置 Microsoft Teams 应用，并使用它配置频道或群聊选项卡、消息扩展或 Office 365 连接器。</span><span class="sxs-lookup"><span data-stu-id="db006-116">You can [create a configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) that enables users to configure Microsoft Teams app and use it to configure a channel or group chat tab, a messaging extension, or an Office 365 Connector.</span></span> <span data-ttu-id="db006-117">您可以允许用户在安装后重新配置选项卡， [并创建应用程序的选项卡](~/tabs/how-to/create-tab-pages/removal-page.md) 删除页。</span><span class="sxs-lookup"><span data-stu-id="db006-117">You can permit users to reconfigure your tab after installation and [create a tab removal page](~/tabs/how-to/create-tab-pages/removal-page.md) for your application.</span></span> <span data-ttu-id="db006-118">生成包含选项卡Teams应用时，必须测试选项卡在 Android 和 iOS 和[iOS Teams运行。](~/tabs/design/tabs-mobile.md)</span><span class="sxs-lookup"><span data-stu-id="db006-118">When you build a Teams app that includes a tab, you must test how your [tab functions on both the Android and iOS Teams clients](~/tabs/design/tabs-mobile.md).</span></span> <span data-ttu-id="db006-119">您的选项卡 [必须通过基本](~/tabs/how-to/access-teams-context.md) 信息、区域设置和主题信息获取上下文，或者确定 `entityId` `subEntityId` 选项卡中的内容。</span><span class="sxs-lookup"><span data-stu-id="db006-119">Your tab must [get context](~/tabs/how-to/access-teams-context.md) through basic information, locale and theme information, and `entityId` or `subEntityId` that identifies what is in the tab.</span></span>

<span data-ttu-id="db006-120">你可以生成带自适应卡片的选项卡，并集中Teams应用功能，无需为机器人和选项卡提供不同的后端。</span><span class="sxs-lookup"><span data-stu-id="db006-120">You can build tabs with Adaptive Cards and centralize all Teams app capabilities by eliminating the need for a different backend for your bots and tabs.</span></span> <span data-ttu-id="db006-121">[阶段视图](~/tabs/tabs-link-unfurling.md)是一个新的 UI 组件，允许你呈现在屏幕中全屏打开Teams固定为选项卡的内容。现有[链接取消点击](~/tabs/tabs-link-unfurling.md)服务已更新，以便它可用于使用自适应卡片和聊天服务将 URL 转换为选项卡。</span><span class="sxs-lookup"><span data-stu-id="db006-121">[Stage View](~/tabs/tabs-link-unfurling.md) is a new UI component that allows you to render the content opened in full screen in Teams and pinned as a tab. The existing [link unfurling](~/tabs/tabs-link-unfurling.md) service is updated so that it is used to turn URLs into a tab using an Adaptive Card and Chat Services.</span></span> <span data-ttu-id="db006-122">您可以使用对话[](~/tabs/how-to/conversational-tabs.md)子实体创建对话选项卡，这些子实体允许用户就选项卡中的子实体（如特定任务、患者和销售机会）展开对话，而不是讨论整个选项卡。你可以更改选项卡[边距](~/resources/removing-tab-margins.md)，以增强开发人员在构建应用时的体验。</span><span class="sxs-lookup"><span data-stu-id="db006-122">You can [create conversational tabs](~/tabs/how-to/conversational-tabs.md) using conversational sub-entities that allow users to have conversations about sub-entities in your tab, such as specific task, patient, and sales opportunity, instead of discussing the entire tab. You can make changes to [tab margins](~/resources/removing-tab-margins.md) to enhance the developer's experience when building apps.</span></span>

## <a name="tab-features"></a><span data-ttu-id="db006-123">选项卡功能</span><span class="sxs-lookup"><span data-stu-id="db006-123">Tab features</span></span>

<span data-ttu-id="db006-124">选项卡功能如下所示：</span><span class="sxs-lookup"><span data-stu-id="db006-124">The tab features are as follows:</span></span>

* <span data-ttu-id="db006-125">如果将选项卡添加到同样具有自动程序的应用，则机器人也会添加到团队中。</span><span class="sxs-lookup"><span data-stu-id="db006-125">If a tab is added to an app that also has a bot, the bot is also added to the team.</span></span>
* <span data-ttu-id="db006-126">感知Azure Active Directory (AAD) 当前用户的 ID。</span><span class="sxs-lookup"><span data-stu-id="db006-126">Awareness of Azure Active Directory (AAD) ID of the current user.</span></span>
* <span data-ttu-id="db006-127">用于指示语言（即 ）的用户区域设置感知 `en-us` 。</span><span class="sxs-lookup"><span data-stu-id="db006-127">Locale awareness for the user to indicate language that is `en-us`.</span></span>
* <span data-ttu-id="db006-128">单一登录 (SSO) 功能（如果受支持）。</span><span class="sxs-lookup"><span data-stu-id="db006-128">Single sign-on (SSO) capability, if supported.</span></span>
* <span data-ttu-id="db006-129">能够使用机器人或应用通知深层链接到选项卡或服务中的子实体，例如单个工作项。</span><span class="sxs-lookup"><span data-stu-id="db006-129">Ability to use bots or app notifications to deep link to the tab or to a sub-entity within the service, for example an individual work item.</span></span>
* <span data-ttu-id="db006-130">从选项卡内的链接打开任务模块的能力。</span><span class="sxs-lookup"><span data-stu-id="db006-130">The ability to open a task module from links within a tab.</span></span>
* <span data-ttu-id="db006-131">在选项卡SharePoint Web 部件重用。</span><span class="sxs-lookup"><span data-stu-id="db006-131">Reuse of SharePoint web parts within the tab.</span></span>

## <a name="tabs-user-scenarios"></a><span data-ttu-id="db006-132">选项卡用户方案</span><span class="sxs-lookup"><span data-stu-id="db006-132">Tabs user scenarios</span></span>

<span data-ttu-id="db006-133">**应用场景：** 将基于 Web 的现有资源引入Teams。</span><span class="sxs-lookup"><span data-stu-id="db006-133">**Scenario:** Bring an existing web-based resource inside Teams.</span></span> \
<span data-ttu-id="db006-134">**示例：** 在向用户显示信息Teams个人选项卡的应用中创建个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="db006-134">**Example:** You create a personal tab in your Teams app that presents an informational corporate website to users.</span></span>

<span data-ttu-id="db006-135">**应用场景：** 向自动程序或消息传递Teams添加支持页面。</span><span class="sxs-lookup"><span data-stu-id="db006-135">**Scenario:** Add support pages to a Teams bot or messaging extension.</span></span> \
<span data-ttu-id="db006-136">**示例：** 创建个人选项卡，为用户提供 **关于** 网页的内容和帮助网页内容。</span><span class="sxs-lookup"><span data-stu-id="db006-136">**Example:** You create personal tabs that provide **about** and **help** webpage content to users.</span></span>

<span data-ttu-id="db006-137">**应用场景：** 提供对用户定期与之交互的项目的访问权限，以便进行协作对话与协作。</span><span class="sxs-lookup"><span data-stu-id="db006-137">**Scenario:** Provide access to items that your users interact with regularly for cooperative dialogue and collaboration.</span></span> \
<span data-ttu-id="db006-138">**示例：** 创建一个通道或组选项卡，该选项卡具有到各个项目的深层链接。</span><span class="sxs-lookup"><span data-stu-id="db006-138">**Example:** You create a channel or group tab with deep linking to individual items.</span></span>

## <a name="understand-how-tabs-work"></a><span data-ttu-id="db006-139">了解选项卡如何工作</span><span class="sxs-lookup"><span data-stu-id="db006-139">Understand how tabs work</span></span>

<span data-ttu-id="db006-140">可以使用下列方法之一创建选项卡：</span><span class="sxs-lookup"><span data-stu-id="db006-140">You can use one of the following methods to create tabs:</span></span>

* [<span data-ttu-id="db006-141">在应用清单中声明自定义选项卡</span><span class="sxs-lookup"><span data-stu-id="db006-141">Declare custom tab in app manifest</span></span>](#declare-custom-tab-in-app-manifest)
* [<span data-ttu-id="db006-142">使用自适应卡片生成选项卡</span><span class="sxs-lookup"><span data-stu-id="db006-142">Use Adaptive Card to build tabs</span></span>](~/tabs/how-to/build-adaptive-card-tabs.md)

### <a name="declare-custom-tab-in-app-manifest"></a><span data-ttu-id="db006-143">在应用清单中声明自定义选项卡</span><span class="sxs-lookup"><span data-stu-id="db006-143">Declare custom tab in app manifest</span></span>

<span data-ttu-id="db006-144">自定义选项卡在应用包的应用清单中声明。</span><span class="sxs-lookup"><span data-stu-id="db006-144">A custom tab is declared in the app manifest of your app package.</span></span> <span data-ttu-id="db006-145">对于希望作为选项卡包含在应用中的每个网页，可定义 URL 和范围。</span><span class="sxs-lookup"><span data-stu-id="db006-145">For each webpage you want included as a tab in your app, you define a URL and a scope.</span></span> <span data-ttu-id="db006-146">此外，你可以将[Teams JavaScript 客户端 SDK](/javascript/api/overview/msteams-client)添加到页面，并加载 `microsoftTeams.initialize()` 页面后调用。</span><span class="sxs-lookup"><span data-stu-id="db006-146">Additionally, you can add the [Teams JavaScript client SDK](/javascript/api/overview/msteams-client) to your page, and call `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="db006-147">Teams显示页面并提供对Teams特定信息的访问权限，例如，Teams客户端正在运行深色主题。</span><span class="sxs-lookup"><span data-stu-id="db006-147">Teams displays your page and provides access to Teams-specific information, for example the Teams client is running the dark theme.</span></span>

<span data-ttu-id="db006-148">无论你选择在频道或组还是个人范围内公开选项卡，都必须在选项卡<显示一个 iframe \> HTML 内容页。 [](~/tabs/how-to/create-tab-pages/content-page.md)对于个人选项卡，内容 URL 直接在Teams清单中通过 `contentUrl` 数组中的 属性 `staticTabs` 进行设置。</span><span class="sxs-lookup"><span data-stu-id="db006-148">Whether you choose to expose your tab within the channel or group, or personal scope, you must present an <iframe\> HTML [content page](~/tabs/how-to/create-tab-pages/content-page.md) in your tab. For personal tabs, the content URL is set directly in your Teams app manifest by the `contentUrl` property in the `staticTabs` array.</span></span> <span data-ttu-id="db006-149">您的选项卡的内容对于所有用户都是相同的。</span><span class="sxs-lookup"><span data-stu-id="db006-149">Your tab's content is the same for all users.</span></span>

<span data-ttu-id="db006-150">对于频道或组选项卡，还可以创建其他配置页面。</span><span class="sxs-lookup"><span data-stu-id="db006-150">For channel or group tabs, you can also create an additional configuration page.</span></span> <span data-ttu-id="db006-151">此页面允许您配置内容页 URL，通常使用 URL 查询字符串参数加载该上下文的适当内容。</span><span class="sxs-lookup"><span data-stu-id="db006-151">This page allows you to configure content page URL, typically by using URL query string parameters to load the appropriate content for that context.</span></span> <span data-ttu-id="db006-152">这是因为频道或组选项卡可以添加到多个团队或群组聊天中。</span><span class="sxs-lookup"><span data-stu-id="db006-152">This is because your channel or group tab can be added to multiple teams or group chats.</span></span> <span data-ttu-id="db006-153">每次后续安装时，您的用户可以配置选项卡，从而允许您根据需要定制体验。</span><span class="sxs-lookup"><span data-stu-id="db006-153">On each subsequent install, your users can configure the tab, allowing you to tailor the experience as required.</span></span> <span data-ttu-id="db006-154">当用户添加或配置选项卡时，URL 与 UI Teams用户界面 (选项卡) 。</span><span class="sxs-lookup"><span data-stu-id="db006-154">When users add or configure a tab, a URL is associated with the tab that is presented in the Teams user interface (UI).</span></span> <span data-ttu-id="db006-155">配置选项卡只是向该 URL 添加其他参数。</span><span class="sxs-lookup"><span data-stu-id="db006-155">Configuring a tab simply adds additional parameters to that URL.</span></span> <span data-ttu-id="db006-156">例如，当您添加"Azure Boards"选项卡时，配置页允许您选择加载哪一个选项卡。</span><span class="sxs-lookup"><span data-stu-id="db006-156">For example, when you add the Azure Boards tab, the configuration page allows you to choose, which board the tab loads.</span></span> <span data-ttu-id="db006-157">配置页面 URL 由应用清单  `configurationUrl` 的 `configurableTabs` 数组中的 属性指定。</span><span class="sxs-lookup"><span data-stu-id="db006-157">The configuration page URL is specified by the  `configurationUrl` property in the `configurableTabs` array in your app manifest.</span></span>

<span data-ttu-id="db006-158">你可以有多个频道或组选项卡，每个应用最多有 16 个个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="db006-158">You can have multiple channels or group tabs, and up to 16 personal tabs per app.</span></span>

## <a name="see-also"></a><span data-ttu-id="db006-159">另请参阅</span><span class="sxs-lookup"><span data-stu-id="db006-159">See also</span></span>

* [<span data-ttu-id="db006-160">请求设备权限</span><span class="sxs-lookup"><span data-stu-id="db006-160">Request device permissions</span></span>](../concepts/device-capabilities/native-device-permissions.md)
* [<span data-ttu-id="db006-161">集成媒体功能</span><span class="sxs-lookup"><span data-stu-id="db006-161">Integrate media capabilities</span></span>](../concepts/device-capabilities/mobile-camera-image-permissions.md)
* [<span data-ttu-id="db006-162">集成 QR 或条形码扫描仪</span><span class="sxs-lookup"><span data-stu-id="db006-162">Integrate a QR or barcode scanner</span></span>](../concepts/device-capabilities/qr-barcode-scanner-capability.md)
* [<span data-ttu-id="db006-163">集成位置功能</span><span class="sxs-lookup"><span data-stu-id="db006-163">Integrate location capabilities</span></span>](../concepts/device-capabilities/location-capability.md)

## <a name="next-step"></a><span data-ttu-id="db006-164">后续步骤</span><span class="sxs-lookup"><span data-stu-id="db006-164">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="db006-165">先决条件</span><span class="sxs-lookup"><span data-stu-id="db006-165">Prerequisites</span></span>](~/tabs/how-to/tab-requirements.md)
