---
title: 创建内容页
author: surbhigupta
description: 如何创建内容页
keywords: teams 选项卡组通道可配置静态
localization_priority: Normal
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 1276fdac2d3a30836b574b8e51b99fcbd7a415d2
ms.sourcegitcommit: 85a52119df6c4cb4536572e6d2e7407f0e5e8a23
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/29/2021
ms.locfileid: "53179732"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="64414-104">为选项卡创建内容页</span><span class="sxs-lookup"><span data-stu-id="64414-104">Create a content page for your tab</span></span>

<span data-ttu-id="64414-105">内容页是在客户端中呈现Teams网页。</span><span class="sxs-lookup"><span data-stu-id="64414-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="64414-106">这些是以下部分：</span><span class="sxs-lookup"><span data-stu-id="64414-106">These are part of:</span></span>

* <span data-ttu-id="64414-107">个人范围的自定义选项卡：在这种情况下，内容页是用户遇到的第一个页面。</span><span class="sxs-lookup"><span data-stu-id="64414-107">A personal-scoped custom tab: In this case, the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="64414-108">频道或组自定义选项卡：内容页在用户固定并配置相应上下文中的选项卡后显示。</span><span class="sxs-lookup"><span data-stu-id="64414-108">A channel or group custom tab: The content page is displayed after the user pins and configures the tab in the appropriate context.</span></span>
* <span data-ttu-id="64414-109">任务 [模块](~/task-modules-and-cards/what-are-task-modules.md)：可以创建内容页，并将其作为 Web 视图嵌入任务模块中。</span><span class="sxs-lookup"><span data-stu-id="64414-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md): You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="64414-110">页面在模式弹出窗口内呈现。</span><span class="sxs-lookup"><span data-stu-id="64414-110">The page is rendered inside the modal pop-up.</span></span>

<span data-ttu-id="64414-111">本文专门介绍将内容页用作选项卡;但是，无论内容页如何呈现给用户，此处的大部分指南都适用。</span><span class="sxs-lookup"><span data-stu-id="64414-111">This article is specific to using content pages as tabs; however the majority of the guidance here applies regardless of how the content page is presented to the user.</span></span>

## <a name="tab-content-and-design-guidelines"></a><span data-ttu-id="64414-112">选项卡内容和设计指南</span><span class="sxs-lookup"><span data-stu-id="64414-112">Tab content and design guidelines</span></span>

<span data-ttu-id="64414-113">选项卡的总体目标是提供对具有实用价值且明确用途的有意义且吸引人的内容的访问。</span><span class="sxs-lookup"><span data-stu-id="64414-113">Your tab's overall objective is to provide access to meaningful and engaging content that has practical value and an evident purpose.</span></span> <span data-ttu-id="64414-114">您必须专注于使选项卡设计干净、导航直观且内容沉浸式。</span><span class="sxs-lookup"><span data-stu-id="64414-114">You must focus on making your tab design clean, navigation intuitive, and content immersive.</span></span>

<span data-ttu-id="64414-115">有关详细信息，请参阅选项卡[设计指南和](~/tabs/design/tabs.md)Microsoft Teams[应用商店验证指南](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)。</span><span class="sxs-lookup"><span data-stu-id="64414-115">For more information, see [tab design guidelines](~/tabs/design/tabs.md) and [Microsoft Teams store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md).</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="64414-116">将代码与Teams</span><span class="sxs-lookup"><span data-stu-id="64414-116">Integrate your code with Teams</span></span>

<span data-ttu-id="64414-117">若要在页面中显示Teams，必须包含[Microsoft Teams JavaScript](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true)客户端 SDK，并包括加载 `microsoftTeams.initialize()` 页面后对 的调用。</span><span class="sxs-lookup"><span data-stu-id="64414-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest&preserve-view=true) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> 

<span data-ttu-id="64414-118">以下代码提供了页面和客户端之间如何Teams的示例：</span><span class="sxs-lookup"><span data-stu-id="64414-118">The following code provides an example of how your page and the Teams client communicate:</span></span>

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

## <a name="access-additional-content"></a><span data-ttu-id="64414-119">访问其他内容</span><span class="sxs-lookup"><span data-stu-id="64414-119">Access additional content</span></span>

<span data-ttu-id="64414-120">您可以通过使用 SDK 与 Teams交互、创建深层链接、使用任务模块并验证 URL 域是否包含在数组中来访问 `validDomains` 其他内容。</span><span class="sxs-lookup"><span data-stu-id="64414-120">You can access additional content by using the SDK to interact with Teams, creating deep links, using task modules, and verifying if URL domains are included in the `validDomains` array.</span></span>

### <a name="use-the-sdk-to-interact-with-teams"></a><span data-ttu-id="64414-121">使用 SDK 与 Teams</span><span class="sxs-lookup"><span data-stu-id="64414-121">Use the SDK to interact with Teams</span></span>

<span data-ttu-id="64414-122">客户端[Teams JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md)提供了许多其他函数，您可以在开发内容页时发现这些函数很有用。</span><span class="sxs-lookup"><span data-stu-id="64414-122">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions that you can find useful while developing your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="64414-123">深度链接</span><span class="sxs-lookup"><span data-stu-id="64414-123">Deep links</span></span>

<span data-ttu-id="64414-124">可以创建指向网站中的实体的深层Teams。</span><span class="sxs-lookup"><span data-stu-id="64414-124">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="64414-125">这些链接用于创建导航到选项卡中的内容和信息的链接。有关详细信息，请参阅 create [deep links to content and features in Teams](~/concepts/build-and-test/deep-links.md)。</span><span class="sxs-lookup"><span data-stu-id="64414-125">These are used to create links that navigate to content and information within your tab. For more information, see [create deep links to content and features in Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="64414-126">任务模块</span><span class="sxs-lookup"><span data-stu-id="64414-126">Task modules</span></span>

<span data-ttu-id="64414-127">任务模块是一种模式弹出体验，可以从选项卡触发。在内容页中，可以使用任务模块来显示表单，以收集其他信息、显示列表中项目的详细信息或向用户显示其他信息。</span><span class="sxs-lookup"><span data-stu-id="64414-127">A task module is a modal pop-up experience that you can trigger from your tab. In a content page, you can use task modules to present forms for gathering additional information, displaying the details of an item in a list, or presenting the user with additional information.</span></span> <span data-ttu-id="64414-128">任务模块本身可以是其他内容页，或者完全使用自适应卡片创建。</span><span class="sxs-lookup"><span data-stu-id="64414-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="64414-129">有关详细信息，请参阅在 [选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="64414-129">For more information, see [using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

### <a name="valid-domains"></a><span data-ttu-id="64414-130">有效域</span><span class="sxs-lookup"><span data-stu-id="64414-130">Valid domains</span></span>

<span data-ttu-id="64414-131">确保选项卡中使用的所有 URL 域都包含在清单 `validDomains` 的 [数组中](~/concepts/build-and-test/apps-package.md)。</span><span class="sxs-lookup"><span data-stu-id="64414-131">Ensure that all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="64414-132">有关详细信息，请参阅清单架构参考中的[validDomains。](~/resources/schema/manifest-schema.md#validdomains)</span><span class="sxs-lookup"><span data-stu-id="64414-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span>

> [!NOTE]
> <span data-ttu-id="64414-133">选项卡的核心功能存在于Teams中，而不是位于Teams。</span><span class="sxs-lookup"><span data-stu-id="64414-133">The core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="64414-134">显示本机加载指示器</span><span class="sxs-lookup"><span data-stu-id="64414-134">Show a native loading indicator</span></span>

<span data-ttu-id="64414-135">从清单 [架构 v1.7](../../../resources/schema/manifest-schema.md)开始，你可以提供 [本机加载指示器](../../../resources/schema/manifest-schema.md#showloadingindicator)。</span><span class="sxs-lookup"><span data-stu-id="64414-135">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator).</span></span> <span data-ttu-id="64414-136">例如， [选项卡内容页](#integrate-your-code-with-teams)、 [配置页](configuration-page.md)、 [删除页](removal-page.md)和 [选项卡中的任务模块](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="64414-136">For example, [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md), and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> * <span data-ttu-id="64414-137">无法通过本机加载指示器属性配置移动客户端上的行为。</span><span class="sxs-lookup"><span data-stu-id="64414-137">The behavior on mobile clients is not configurable through the native loading indicator property.</span></span> <span data-ttu-id="64414-138">默认情况下，移动客户端在内容页和基于 iframe 的任务模块中显示此指示器。</span><span class="sxs-lookup"><span data-stu-id="64414-138">Mobile clients show this indicator by default across content pages and iframe-based task modules.</span></span> <span data-ttu-id="64414-139">当提出提取内容的请求时，会显示移动设备上的此指示器，请求完成后立即消除。</span><span class="sxs-lookup"><span data-stu-id="64414-139">This indicator on mobile is shown when a request is made to fetch content and gets dismissed as soon as the request gets completed.</span></span>

<span data-ttu-id="64414-140">如果你在应用清单中指示，则所有选项卡配置、内容和删除页面以及所有基于 `showLoadingIndicator : true`  iframe 的任务模块都必须执行以下步骤：</span><span class="sxs-lookup"><span data-stu-id="64414-140">If you indicate `showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow these steps:</span></span>

<span data-ttu-id="64414-141">**显示加载指示器**</span><span class="sxs-lookup"><span data-stu-id="64414-141">**To show the loading indicator**</span></span>

1. <span data-ttu-id="64414-142">添加到 `"showLoadingIndicator": true` 清单。</span><span class="sxs-lookup"><span data-stu-id="64414-142">Add `"showLoadingIndicator": true` to your manifest.</span></span>
1. <span data-ttu-id="64414-143">调用 `microsoftTeams.initialize();`。</span><span class="sxs-lookup"><span data-stu-id="64414-143">Call `microsoftTeams.initialize();`.</span></span>
1. <span data-ttu-id="64414-144">作为 **强制性步骤**，调用 以Teams `microsoftTeams.appInitialization.notifySuccess()` 应用已成功加载。</span><span class="sxs-lookup"><span data-stu-id="64414-144">As a **mandatory** step, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="64414-145">Teams，则隐藏加载指示器（如果适用）。</span><span class="sxs-lookup"><span data-stu-id="64414-145">Teams then hides the loading indicator, if applicable.</span></span> <span data-ttu-id="64414-146">如果未在 30 秒内调用，则假定你的应用已退出，并且将显示一个显示 `notifySuccess`  重试选项的错误屏幕。</span><span class="sxs-lookup"><span data-stu-id="64414-146">If `notifySuccess`  is not called within 30 seconds, it is assumed that your app timed out and an error screen with a retry option appears.</span></span>
1. <span data-ttu-id="64414-147">**（可选**）如果你已准备好打印到屏幕，并且希望延迟加载应用程序内容的其余部分，可以通过调用 手动隐藏加载指示器 `microsoftTeams.appInitialization.notifyAppLoaded();` 。</span><span class="sxs-lookup"><span data-stu-id="64414-147">**Optionally**, if you are ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`.</span></span>
1. <span data-ttu-id="64414-148">如果应用程序无法加载，可以调用 以Teams `microsoftTeams.appInitialization.notifyFailure(reason);` 出现错误。</span><span class="sxs-lookup"><span data-stu-id="64414-148">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="64414-149">向用户显示一个错误屏幕。</span><span class="sxs-lookup"><span data-stu-id="64414-149">An error screen is shown to the user.</span></span> <span data-ttu-id="64414-150">以下代码提供了应用程序失败原因的示例：</span><span class="sxs-lookup"><span data-stu-id="64414-150">The following code provides an example of application failure reasons:</span></span>

    ```typescript
    /* List of failure reasons */
    export const enum FailedReason {
        AuthFailed = "AuthFailed",
        Timeout = "Timeout",
        Other = "Other"
    }
    ```

## <a name="see-also"></a><span data-ttu-id="64414-151">另请参阅</span><span class="sxs-lookup"><span data-stu-id="64414-151">See also</span></span>

* [<span data-ttu-id="64414-152">Teams选项卡</span><span class="sxs-lookup"><span data-stu-id="64414-152">Teams tabs</span></span>](~/tabs/what-are-tabs.md)
* [<span data-ttu-id="64414-153">创建个人选项卡</span><span class="sxs-lookup"><span data-stu-id="64414-153">Create a personal tab</span></span>](~/tabs/how-to/create-personal-tab.md)
* [<span data-ttu-id="64414-154">创建频道或组选项卡</span><span class="sxs-lookup"><span data-stu-id="64414-154">Create a channel or group tab</span></span>](~/tabs/how-to/create-channel-group-tab.md)
* [<span data-ttu-id="64414-155">创建内容页</span><span class="sxs-lookup"><span data-stu-id="64414-155">Create a content page</span></span>](~/tabs/how-to/create-tab-pages/content-page.md)

## <a name="next-step"></a><span data-ttu-id="64414-156">后续步骤</span><span class="sxs-lookup"><span data-stu-id="64414-156">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="64414-157">创建配置页</span><span class="sxs-lookup"><span data-stu-id="64414-157">Create a configuration page</span></span>](~/tabs/how-to/create-tab-pages/configuration-page.md)
