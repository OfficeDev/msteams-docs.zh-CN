---
title: 创建内容页
author: laujan
description: 如何创建内容页
keywords: 团队选项卡组频道配置静态
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 91a7d643d3a631610989e31eae14265cd725dbd0
ms.sourcegitcommit: e8dfcb167274e996395b77d65999991a18f2051a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/15/2020
ms.locfileid: "47818904"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="c0d89-104">创建选项卡的内容页</span><span class="sxs-lookup"><span data-stu-id="c0d89-104">Create a content page for your tab</span></span>

<span data-ttu-id="c0d89-105">内容页面是在团队客户端中呈现的网页。</span><span class="sxs-lookup"><span data-stu-id="c0d89-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="c0d89-106">通常情况下，它们是以下部分：</span><span class="sxs-lookup"><span data-stu-id="c0d89-106">Typically these are part of:</span></span>

* <span data-ttu-id="c0d89-107">个人作用域的自定义选项卡-在此实例中，内容页面是用户遇到的第一页。</span><span class="sxs-lookup"><span data-stu-id="c0d89-107">A personal-scoped custom tab - In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="c0d89-108">通道/组自定义选项卡-用户固定并在适当的上下文中配置选项卡后，将显示内容页。</span><span class="sxs-lookup"><span data-stu-id="c0d89-108">A channel/group custom tab - After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="c0d89-109">[任务模块](~/task-modules-and-cards/what-are-task-modules.md)-您可以创建内容页并将其作为 web 视图嵌入任务模块中。</span><span class="sxs-lookup"><span data-stu-id="c0d89-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md) - You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="c0d89-110">页面将在模式弹出窗口中呈现。</span><span class="sxs-lookup"><span data-stu-id="c0d89-110">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="c0d89-111">本文特定于将内容页用作选项卡;但是，无论内容页面是如何呈现给最终用户的，此处的大部分指南都适用。</span><span class="sxs-lookup"><span data-stu-id="c0d89-111">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-style-guidelines"></a><span data-ttu-id="c0d89-112">选项卡内容和样式准则</span><span class="sxs-lookup"><span data-stu-id="c0d89-112">Tab content and style guidelines</span></span>

<span data-ttu-id="c0d89-113">您的选项卡的总体目标应是提供对具有实际价值和明显用途的有意义和吸引人的内容的访问。</span><span class="sxs-lookup"><span data-stu-id="c0d89-113">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="c0d89-114">这并不意味着您应放弃令人满意的样式，但您应通过使您的选项卡设计整洁、导航直观和内容沉浸在最大限度地减少杂乱的注意力。</span><span class="sxs-lookup"><span data-stu-id="c0d89-114">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span> <span data-ttu-id="c0d89-115">使用选项卡和[Microsoft 团队应用程序审批过程指南](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)查看[内容和对话](~/tabs/design/tabs.md)</span><span class="sxs-lookup"><span data-stu-id="c0d89-115">See [Content and conversations, all at once using tabs](~/tabs/design/tabs.md) and [Microsoft Teams app approval process guidance](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="c0d89-116">将您的代码与团队集成</span><span class="sxs-lookup"><span data-stu-id="c0d89-116">Integrate your code with Teams</span></span>

<span data-ttu-id="c0d89-117">若要在团队中显示您的页面，您必须包含 [Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) ，并在 `microsoftTeams.initialize()` 页面加载后包含一个调用。</span><span class="sxs-lookup"><span data-stu-id="c0d89-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="c0d89-118">这就是页面和团队客户端的通信方式：</span><span class="sxs-lookup"><span data-stu-id="c0d89-118">That is how your page and the Teams client communicate:</span></span>

```html
<!DOCTYPE html>
<html>
<head>
...
    <script src= 'https://statics.teams.cdn.office.net/sdk/v1.6.0/js/MicrosoftTeams.min.js'></script>
...
</head>

<body>
...
    <script>
    microsoftTeams.initialize();
    </script>
...
</body>
```

## <a name="accessing-additional-content"></a><span data-ttu-id="c0d89-119">访问其他内容</span><span class="sxs-lookup"><span data-stu-id="c0d89-119">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="c0d89-120">使用 SDK 与团队进行交互</span><span class="sxs-lookup"><span data-stu-id="c0d89-120">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="c0d89-121">[团队客户端 JAVASCRIPT SDK](~/tabs/how-to/using-teams-client-sdk.md)提供了许多其他功能，在开发人员的内容页时，您可能会发现有用的功能。</span><span class="sxs-lookup"><span data-stu-id="c0d89-121">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developer your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="c0d89-122">深度链接</span><span class="sxs-lookup"><span data-stu-id="c0d89-122">Deep links</span></span>

<span data-ttu-id="c0d89-123">您可以创建指向团队中的实体的深层链接。</span><span class="sxs-lookup"><span data-stu-id="c0d89-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="c0d89-124">通常，这些用于创建导航到您的选项卡中的内容和信息的链接。请参阅 [创建指向 Microsoft 团队中的内容和功能的深层链接](~/concepts/build-and-test/deep-links.md)。</span><span class="sxs-lookup"><span data-stu-id="c0d89-124">Typically, these are used to create links that navigate to content and information within your tab. See [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="c0d89-125">任务模块</span><span class="sxs-lookup"><span data-stu-id="c0d89-125">Task Modules</span></span>

<span data-ttu-id="c0d89-126">任务模块是可以从选项卡触发的模式弹出窗口的体验。通常在内容页中，您不希望通过多个页面导航您的用户。</span><span class="sxs-lookup"><span data-stu-id="c0d89-126">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="c0d89-127">相反，您将使用任务模块显示用于收集其他信息的表单，并显示列表中项目的详细信息，或任何其他需要向用户提供其他信息的时间。</span><span class="sxs-lookup"><span data-stu-id="c0d89-127">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="c0d89-128">任务模块本身可以是其他内容页，也可以完全使用自适应卡片创建。</span><span class="sxs-lookup"><span data-stu-id="c0d89-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="c0d89-129">有关完整信息，请参阅 [在选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md) 。</span><span class="sxs-lookup"><span data-stu-id="c0d89-129">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="c0d89-130">有效的域</span><span class="sxs-lookup"><span data-stu-id="c0d89-130">Valid Domains</span></span>

<span data-ttu-id="c0d89-131">确保您的选项卡中使用的所有 URL 域都包含在 `validDomains` [清单](~/concepts/build-and-test/apps-package.md)中的阵列中。</span><span class="sxs-lookup"><span data-stu-id="c0d89-131">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="c0d89-132">有关详细信息，请参阅清单架构参考中的 [validDomains](~/resources/schema/manifest-schema.md#validdomains) 。</span><span class="sxs-lookup"><span data-stu-id="c0d89-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="c0d89-133">但是，请注意，您的选项卡的核心功能在团队中，而不是在团队外部。</span><span class="sxs-lookup"><span data-stu-id="c0d89-133">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="c0d89-134">显示本机加载指示器</span><span class="sxs-lookup"><span data-stu-id="c0d89-134">Show a native loading indicator</span></span>

<span data-ttu-id="c0d89-135">从 [清单架构](../../../resources/schema/manifest-schema.md)v1.1，您可以在团队中加载 web 内容的任何位置提供 [本机加载指示器](../../../resources/schema/manifest-schema.md#showloadingindicator) ，例如， [选项卡内容页](#integrate-your-code-with-teams)、 [配置页](configuration-page.md)、 [删除页](removal-page.md) 和 [选项卡中的任务模块](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="c0d89-135">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator) wherever your web content is loaded in Teams, e.g., [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md) and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> <span data-ttu-id="c0d89-136">如果  `"showLoadingIndicator : true`  在应用程序清单中指明，则所有选项卡配置、内容和删除页以及所有基于 iframe 的任务模块必须遵循以下强制协议：</span><span class="sxs-lookup"><span data-stu-id="c0d89-136">If you indicate  `"showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow the mandatory protocol, below:</span></span>

1. <span data-ttu-id="c0d89-137">若要显示加载指示器，请将添加 `"showLoadingIndicator": true` 到你的清单中。</span><span class="sxs-lookup"><span data-stu-id="c0d89-137">To show the loading indicator, add `"showLoadingIndicator": true` to your manifest.</span></span> 
2. <span data-ttu-id="c0d89-138">请记住调用 `microsoftTeams.initialize();` 。</span><span class="sxs-lookup"><span data-stu-id="c0d89-138">Remember to call `microsoftTeams.initialize();`.</span></span>
3. <span data-ttu-id="c0d89-139">**可选**。</span><span class="sxs-lookup"><span data-stu-id="c0d89-139">**Optional**.</span></span> <span data-ttu-id="c0d89-140">如果您已准备好打印到屏幕，并希望延迟加载应用程序内容的其余部分，则可以通过调用来手动隐藏加载指示器 `microsoftTeams.appInitialization.notifyAppLoaded();`</span><span class="sxs-lookup"><span data-stu-id="c0d89-140">If you're ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`</span></span>
4. <span data-ttu-id="c0d89-141">**强制性**。</span><span class="sxs-lookup"><span data-stu-id="c0d89-141">**Mandatory**.</span></span> <span data-ttu-id="c0d89-142">最后，调用 `microsoftTeams.appInitialization.notifySuccess()` 以通知团队您的应用程序已成功加载。</span><span class="sxs-lookup"><span data-stu-id="c0d89-142">Finally, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="c0d89-143">如果适用，团队将隐藏加载指示器。</span><span class="sxs-lookup"><span data-stu-id="c0d89-143">Teams will then hide the loading indicator if applicable.</span></span> <span data-ttu-id="c0d89-144">如果  `notifySuccess`  在30秒内未调用，则系统将假定您的应用程序超时，并将出现一个带有重试选项的错误屏幕。</span><span class="sxs-lookup"><span data-stu-id="c0d89-144">If  `notifySuccess`  is not called within 30 seconds, it will be assumed that your app timed out and an error screen with a retry option will appear.</span></span>
5. <span data-ttu-id="c0d89-145">如果您的应用程序无法加载，则可以通过调用 `microsoftTeams.appInitialization.notifyFailure(reason);` 来让团队知道出现了错误。</span><span class="sxs-lookup"><span data-stu-id="c0d89-145">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="c0d89-146">随后将向用户显示一个错误屏幕：</span><span class="sxs-lookup"><span data-stu-id="c0d89-146">An error screen will then be shown to the user:</span></span>

```typescript
``
/* List of failure reasons */
export const enum FailedReason {
    AuthFailed = "AuthFailed",
    Timeout = "Timeout",
    Other = "Other"
}
```
>
