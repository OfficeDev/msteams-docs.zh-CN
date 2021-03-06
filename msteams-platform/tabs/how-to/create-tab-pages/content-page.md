---
title: 创建内容页
author: laujan
description: 如何创建内容页
keywords: teams 选项卡组通道可配置静态
ms.topic: conceptual
ms.author: lajanuar
ms.openlocfilehash: 619ca1079fcdb5a44eec2fa63d6687a0eb65cd4d
ms.sourcegitcommit: 9cfbc44912980a33d2d7c7c85739aeea6ccb41de
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/05/2021
ms.locfileid: "50479870"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="697f0-104">为选项卡创建内容页</span><span class="sxs-lookup"><span data-stu-id="697f0-104">Create a content page for your tab</span></span>

<span data-ttu-id="697f0-105">内容页是在 Teams 客户端中呈现的网页。</span><span class="sxs-lookup"><span data-stu-id="697f0-105">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="697f0-106">通常，这些是以下部分：</span><span class="sxs-lookup"><span data-stu-id="697f0-106">Typically these are part of:</span></span>

* <span data-ttu-id="697f0-107">个人范围的自定义选项卡 - 在此实例中，内容页是用户遇到的第一页。</span><span class="sxs-lookup"><span data-stu-id="697f0-107">A personal-scoped custom tab - In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="697f0-108">频道/组自定义选项卡 - 在用户固定并配置相应上下文中的选项卡后，将显示内容页。</span><span class="sxs-lookup"><span data-stu-id="697f0-108">A channel/group custom tab - After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="697f0-109">任务 [模块](~/task-modules-and-cards/what-are-task-modules.md) - 您可以创建内容页并将其作为 Web 视图嵌入任务模块中。</span><span class="sxs-lookup"><span data-stu-id="697f0-109">A [task module](~/task-modules-and-cards/what-are-task-modules.md) - You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="697f0-110">页面将在模式弹出窗口内呈现。</span><span class="sxs-lookup"><span data-stu-id="697f0-110">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="697f0-111">本文专门介绍将内容页用作选项卡;但是，无论内容页如何向最终用户显示，此处的大部分指南都将适用。</span><span class="sxs-lookup"><span data-stu-id="697f0-111">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-style-guidelines"></a><span data-ttu-id="697f0-112">选项卡内容和样式指南</span><span class="sxs-lookup"><span data-stu-id="697f0-112">Tab content and style guidelines</span></span>

<span data-ttu-id="697f0-113">您的选项卡的总体目标应该是提供对具有实用价值且具有明显用途的有意义且具有吸引力的内容的访问。</span><span class="sxs-lookup"><span data-stu-id="697f0-113">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="697f0-114">这并不意味着你应该放弃一种令人愉悦的样式，但应专注于通过使选项卡设计简洁、导航直观和内容沉浸式来最大程度地减少混乱。</span><span class="sxs-lookup"><span data-stu-id="697f0-114">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span> <span data-ttu-id="697f0-115">查看 [内容和对话，全部使用](~/tabs/design/tabs.md) 选项卡和 Microsoft [Teams 应用审批流程指南](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span><span class="sxs-lookup"><span data-stu-id="697f0-115">See [Content and conversations, all at once using tabs](~/tabs/design/tabs.md) and [Microsoft Teams app approval process guidance](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="697f0-116">将代码与 Teams 集成</span><span class="sxs-lookup"><span data-stu-id="697f0-116">Integrate your code with Teams</span></span>

<span data-ttu-id="697f0-117">若要在 Teams 中显示页面，必须包含 [Microsoft Teams JavaScript 客户端 SDK，](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) 并包括加载页面 `microsoftTeams.initialize()` 后对页面的调用。</span><span class="sxs-lookup"><span data-stu-id="697f0-117">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="697f0-118">这就是你的页面和 Teams 客户端进行通信的方式：</span><span class="sxs-lookup"><span data-stu-id="697f0-118">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="697f0-119">访问其他内容</span><span class="sxs-lookup"><span data-stu-id="697f0-119">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="697f0-120">使用 SDK 与 Teams 交互</span><span class="sxs-lookup"><span data-stu-id="697f0-120">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="697f0-121">[Teams 客户端 JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md)提供了许多在开发内容页时可能发现有用的其他功能。</span><span class="sxs-lookup"><span data-stu-id="697f0-121">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developing your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="697f0-122">深度链接</span><span class="sxs-lookup"><span data-stu-id="697f0-122">Deep links</span></span>

<span data-ttu-id="697f0-123">可以在 Teams 中创建指向实体的深层链接。</span><span class="sxs-lookup"><span data-stu-id="697f0-123">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="697f0-124">通常，这些链接用于创建导航到选项卡中内容和信息的链接。请参阅["创建指向 Microsoft Teams 中内容和功能的深层链接"。](~/concepts/build-and-test/deep-links.md)</span><span class="sxs-lookup"><span data-stu-id="697f0-124">Typically, these are used to create links that navigate to content and information within your tab. See [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="697f0-125">任务模块</span><span class="sxs-lookup"><span data-stu-id="697f0-125">Task Modules</span></span>

<span data-ttu-id="697f0-126">任务模块是一种模式式弹出式体验，可以从选项卡触发。通常，在内容页中，你不希望在多个页面中导航用户。</span><span class="sxs-lookup"><span data-stu-id="697f0-126">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="697f0-127">相反，您将使用任务模块来显示表单，以收集其他信息、显示列表中某个项目的详细信息，或者需要向用户显示其他信息的其他时间。</span><span class="sxs-lookup"><span data-stu-id="697f0-127">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="697f0-128">任务模块本身可以是其他内容页，或者完全使用自适应卡片创建。</span><span class="sxs-lookup"><span data-stu-id="697f0-128">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="697f0-129">有关 [完整信息，请参阅使用选项卡中](~/task-modules-and-cards/task-modules/task-modules-tabs.md) 的任务模块。</span><span class="sxs-lookup"><span data-stu-id="697f0-129">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="697f0-130">有效域</span><span class="sxs-lookup"><span data-stu-id="697f0-130">Valid Domains</span></span>

<span data-ttu-id="697f0-131">确保选项卡中使用的所有 URL 域都包含在 `validDomains` 清单中的 [数组中](~/concepts/build-and-test/apps-package.md)。</span><span class="sxs-lookup"><span data-stu-id="697f0-131">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="697f0-132">有关详细信息，请参阅清单架构参考中的[validDomains。](~/resources/schema/manifest-schema.md#validdomains)</span><span class="sxs-lookup"><span data-stu-id="697f0-132">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="697f0-133">但是，请注意，选项卡的核心功能存在于 Teams 中，而不是 Teams 外部。</span><span class="sxs-lookup"><span data-stu-id="697f0-133">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>

## <a name="reorder-static-personal-tabs"></a><span data-ttu-id="697f0-134">对静态个人选项卡重新排序</span><span class="sxs-lookup"><span data-stu-id="697f0-134">Reorder static personal tabs</span></span>

<span data-ttu-id="697f0-135">从清单版本 1.7 开始，开发人员可以重新排列其个人应用中的所有选项卡。</span><span class="sxs-lookup"><span data-stu-id="697f0-135">Starting with manifest version 1.7, developers can rearrange all tabs in their personal app.</span></span> <span data-ttu-id="697f0-136">特别是，开发人员可以移动自动程序聊天选项卡，该选项卡始终默认位于个人应用选项卡标题中的任意位置的第一个位置。</span><span class="sxs-lookup"><span data-stu-id="697f0-136">In particular, a developer can move the *bot chat* tab, which always defaults to the first position, anywhere in the personal app tab header.</span></span> <span data-ttu-id="697f0-137">我们已经声明了两个保留的选项卡 entityId 关键字、对话和 *关于*。</span><span class="sxs-lookup"><span data-stu-id="697f0-137">We’ve declared two reserved tab entityId keywords, *conversations* and *about*.</span></span>

<span data-ttu-id="697f0-138">如果你创建具有个人范围的自动程序，它将默认显示在个人应用的第一个选项卡位置。</span><span class="sxs-lookup"><span data-stu-id="697f0-138">If you create a bot with a *personal* scope, it will show up in the first tab position in a personal app by default.</span></span> <span data-ttu-id="697f0-139">如果要将其移动到其他位置，则必须使用保留的关键字对话将静态 Tab 对象添加到 *清单* 中。</span><span class="sxs-lookup"><span data-stu-id="697f0-139">If you wish to move it to another position, you must add a static tab object to your manifest with the reserved keyword, *conversations*.</span></span> <span data-ttu-id="697f0-140">会话 *选项卡* 将基于在数组中添加对话选项卡的什么位置显示在Web 或 `staticTabs` 桌面上。</span><span class="sxs-lookup"><span data-stu-id="697f0-140">The *conversation* tab appears on web or desktop based on where you add the *conversation* tab in the `staticTabs` array.</span></span> 

```json
{
   "staticTabs":[
      {
         
      },
      {
         "entityId":"conversations",
         "scopes":[
            "personal"
         ]
      }
   ]
}
```

## <a name="show-a-native-loading-indicator"></a><span data-ttu-id="697f0-141">显示本机加载指示器</span><span class="sxs-lookup"><span data-stu-id="697f0-141">Show a native loading indicator</span></span>

<span data-ttu-id="697f0-142">从[清单架构 v1.7](../../../resources/schema/manifest-schema.md)开始，可以在[](../../../resources/schema/manifest-schema.md#showloadingindicator)Teams 中加载 Web 内容时提供本机加载指示器，例如选项卡内容页、配置页、[](configuration-page.md)删除页和[](removal-page.md)选项卡中的任务[模块](../../../task-modules-and-cards/task-modules/task-modules-tabs.md)。 [](#integrate-your-code-with-teams)</span><span class="sxs-lookup"><span data-stu-id="697f0-142">Starting with [manifest schema v1.7](../../../resources/schema/manifest-schema.md), you can provide a [native loading indicator](../../../resources/schema/manifest-schema.md#showloadingindicator) wherever your web content is loaded in Teams, e.g., [tab content page](#integrate-your-code-with-teams), [configuration page](configuration-page.md), [removal page](removal-page.md) and [task modules in tabs](../../../task-modules-and-cards/task-modules/task-modules-tabs.md).</span></span>

> [!NOTE]
> 1. <span data-ttu-id="697f0-143">移动设备尚不支持本机加载指示器。</span><span class="sxs-lookup"><span data-stu-id="697f0-143">The native loading indicator is not yet supported on mobile devices.</span></span>
> 2. <span data-ttu-id="697f0-144">如果在应用清单中指示，则所有选项卡配置、内容和删除页面以及所有基于  `"showLoadingIndicator : true`  iframe 的任务模块必须遵循以下强制协议：</span><span class="sxs-lookup"><span data-stu-id="697f0-144">If you indicate  `"showLoadingIndicator : true`  in your app manifest, then all tab configuration, content, and removal pages and all iframe-based task modules must follow the mandatory protocol, below:</span></span>


1. <span data-ttu-id="697f0-145">若要显示加载指示器，请 `"showLoadingIndicator": true` 添加到清单。</span><span class="sxs-lookup"><span data-stu-id="697f0-145">To show the loading indicator, add `"showLoadingIndicator": true` to your manifest.</span></span> 
2. <span data-ttu-id="697f0-146">请记住调用 `microsoftTeams.initialize();` 。</span><span class="sxs-lookup"><span data-stu-id="697f0-146">Remember to call `microsoftTeams.initialize();`.</span></span>
3. <span data-ttu-id="697f0-147">**可选。**</span><span class="sxs-lookup"><span data-stu-id="697f0-147">**Optional**.</span></span> <span data-ttu-id="697f0-148">如果已准备好打印到屏幕，并且希望延迟加载应用程序内容的其余部分，可以通过调用手动隐藏加载指示器 `microsoftTeams.appInitialization.notifyAppLoaded();`</span><span class="sxs-lookup"><span data-stu-id="697f0-148">If you're ready to print to the screen and wish to lazy load the rest of your application's content, you can manually hide the loading indicator by calling `microsoftTeams.appInitialization.notifyAppLoaded();`</span></span>
4. <span data-ttu-id="697f0-149">**强制 。**</span><span class="sxs-lookup"><span data-stu-id="697f0-149">**Mandatory**.</span></span> <span data-ttu-id="697f0-150">最后，致电 `microsoftTeams.appInitialization.notifySuccess()` 通知 Teams 你的应用已成功加载。</span><span class="sxs-lookup"><span data-stu-id="697f0-150">Finally, call `microsoftTeams.appInitialization.notifySuccess()` to notify Teams that your app has successfully loaded.</span></span> <span data-ttu-id="697f0-151">团队随后将隐藏加载指示器（如果适用）。</span><span class="sxs-lookup"><span data-stu-id="697f0-151">Teams will then hide the loading indicator if applicable.</span></span> <span data-ttu-id="697f0-152">如果未在 30 秒内调用，则假定你的应用已退出，并且将显示一个显示重试选项  `notifySuccess`  的错误屏幕。</span><span class="sxs-lookup"><span data-stu-id="697f0-152">If  `notifySuccess`  is not called within 30 seconds, it will be assumed that your app timed out and an error screen with a retry option will appear.</span></span>
5. <span data-ttu-id="697f0-153">如果应用程序无法加载，可以调用以让 `microsoftTeams.appInitialization.notifyFailure(reason);` Teams 知道出现错误。</span><span class="sxs-lookup"><span data-stu-id="697f0-153">If your application fails to load, you can call `microsoftTeams.appInitialization.notifyFailure(reason);` to let Teams know there was an error.</span></span> <span data-ttu-id="697f0-154">然后，会向用户显示一个错误屏幕：</span><span class="sxs-lookup"><span data-stu-id="697f0-154">An error screen will then be shown to the user:</span></span>

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
