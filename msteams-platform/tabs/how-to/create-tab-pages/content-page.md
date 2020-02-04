---
title: 创建内容页
author: laujan
description: ''
keywords: 团队选项卡组频道配置静态
ms.topic: conceptual
ms.author: v-laujan
ms.openlocfilehash: ac85e000c9bdaebf28cb33143a7c82a348d3771e
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673246"
---
# <a name="create-a-content-page-for-your-tab"></a><span data-ttu-id="8d6de-103">创建选项卡的内容页</span><span class="sxs-lookup"><span data-stu-id="8d6de-103">Create a content page for your tab</span></span>

<span data-ttu-id="8d6de-104">内容页面是在团队客户端中呈现的网页。</span><span class="sxs-lookup"><span data-stu-id="8d6de-104">A content page is a webpage that is rendered within the Teams client.</span></span> <span data-ttu-id="8d6de-105">通常情况下，它们是以下部分：</span><span class="sxs-lookup"><span data-stu-id="8d6de-105">Typically these are part of:</span></span>

* <span data-ttu-id="8d6de-106">个人作用域的自定义选项卡-在此实例中，内容页面是用户遇到的第一页。</span><span class="sxs-lookup"><span data-stu-id="8d6de-106">A personal-scoped custom tab - In this instance the content page is the first page the user encounters.</span></span>
* <span data-ttu-id="8d6de-107">通道/组自定义选项卡-用户固定并在适当的上下文中配置选项卡后，将显示内容页。</span><span class="sxs-lookup"><span data-stu-id="8d6de-107">A channel/group custom tab - After the user pins and configures the tab in the appropriate context, the content page is displayed.</span></span>
* <span data-ttu-id="8d6de-108">[任务模块](~/task-modules-and-cards/what-are-task-modules.md)-您可以创建内容页并将其作为 web 视图嵌入任务模块中。</span><span class="sxs-lookup"><span data-stu-id="8d6de-108">A [task module](~/task-modules-and-cards/what-are-task-modules.md) - You can create a content page and embed it as a webview inside a task module.</span></span> <span data-ttu-id="8d6de-109">页面将在模式弹出窗口中呈现。</span><span class="sxs-lookup"><span data-stu-id="8d6de-109">The page will be rendered inside the modal popup.</span></span>

<span data-ttu-id="8d6de-110">本文特定于将内容页用作选项卡;但是，无论内容页面是如何呈现给最终用户的，此处的大部分指南都适用。</span><span class="sxs-lookup"><span data-stu-id="8d6de-110">This article is specific to using content pages as tabs; however the majority of the guidance here would apply regardless of how the content page is presented to the end-user.</span></span>

## <a name="tab-content-and-style-guidelines"></a><span data-ttu-id="8d6de-111">选项卡内容和样式准则</span><span class="sxs-lookup"><span data-stu-id="8d6de-111">Tab content and style guidelines</span></span>

<span data-ttu-id="8d6de-112">您的选项卡的总体目标应是提供对具有实际价值和明显用途的有意义和吸引人的内容的访问。</span><span class="sxs-lookup"><span data-stu-id="8d6de-112">Your tab's overall objective should be to provide access to meaningful and engaging content that has a practical value and an evident purpose.</span></span> <span data-ttu-id="8d6de-113">这并不意味着您应放弃令人满意的样式，但您应通过使您的选项卡设计整洁、导航直观和内容沉浸在最大限度地减少杂乱的注意力。</span><span class="sxs-lookup"><span data-stu-id="8d6de-113">That does not mean that you should forego a pleasing style, but you should focus on minimizing clutter by making your tab design clean, navigation intuitive, and content immersive.</span></span> <span data-ttu-id="8d6de-114">使用选项卡和[Microsoft 团队应用程序审批过程指南](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)查看[内容和对话](~/tabs/design/tabs.md)</span><span class="sxs-lookup"><span data-stu-id="8d6de-114">See [Content and conversations, all at once using tabs](~/tabs/design/tabs.md) and [Microsoft Teams app approval process guidance](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)</span></span>

## <a name="integrate-your-code-with-teams"></a><span data-ttu-id="8d6de-115">将您的代码与团队集成</span><span class="sxs-lookup"><span data-stu-id="8d6de-115">Integrate your code with Teams</span></span>

<span data-ttu-id="8d6de-116">若要在团队中显示您的页面，您必须包含[Microsoft 团队 JavaScript 客户端 SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) ，并在`microsoftTeams.initialize()`页面加载后包含一个调用。</span><span class="sxs-lookup"><span data-stu-id="8d6de-116">For your page to display in Teams, you must include the [Microsoft Teams JavaScript client SDK](/javascript/api/overview/msteams-client?view=msteams-client-js-latest) and include a call to `microsoftTeams.initialize()` after your page loads.</span></span> <span data-ttu-id="8d6de-117">这就是页面和团队客户端的通信方式：</span><span class="sxs-lookup"><span data-stu-id="8d6de-117">That is how your page and the Teams client communicate:</span></span>

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

## <a name="accessing-additional-content"></a><span data-ttu-id="8d6de-118">访问其他内容</span><span class="sxs-lookup"><span data-stu-id="8d6de-118">Accessing additional content</span></span>

### <a name="using-the-sdk-to-interact-with-teams"></a><span data-ttu-id="8d6de-119">使用 SDK 与团队进行交互</span><span class="sxs-lookup"><span data-stu-id="8d6de-119">Using the SDK to interact with Teams</span></span>

<span data-ttu-id="8d6de-120">[团队客户端 JAVASCRIPT SDK](~/tabs/how-to/using-teams-client-sdk.md)提供了许多其他功能，在开发人员的内容页时，您可能会发现有用的功能。</span><span class="sxs-lookup"><span data-stu-id="8d6de-120">The [Teams client JavaScript SDK](~/tabs/how-to/using-teams-client-sdk.md) provides many additional functions you may find useful while developer your content page.</span></span>

### <a name="deep-links"></a><span data-ttu-id="8d6de-121">Deep links</span><span class="sxs-lookup"><span data-stu-id="8d6de-121">Deep links</span></span>

<span data-ttu-id="8d6de-122">您可以创建指向团队中的实体的深层链接。</span><span class="sxs-lookup"><span data-stu-id="8d6de-122">You can create deep links to entities in Teams.</span></span> <span data-ttu-id="8d6de-123">通常，这些用于创建导航到您的选项卡中的内容和信息的链接。请参阅[创建指向 Microsoft 团队中的内容和功能的深层链接](~/concepts/build-and-test/deep-links.md)。</span><span class="sxs-lookup"><span data-stu-id="8d6de-123">Typically, these are used to create links that navigate to content and information within your tab. See [Create deep links to content and features in Microsoft Teams](~/concepts/build-and-test/deep-links.md).</span></span>

### <a name="task-modules"></a><span data-ttu-id="8d6de-124">任务模块</span><span class="sxs-lookup"><span data-stu-id="8d6de-124">Task Modules</span></span>

<span data-ttu-id="8d6de-125">任务模块是可以从选项卡触发的模式弹出窗口的体验。通常在内容页中，您不希望通过多个页面导航您的用户。</span><span class="sxs-lookup"><span data-stu-id="8d6de-125">A task module is a modal popup-like experience that you can trigger from your tab. Typically in a content page you do not want to navigate your user through multiple pages.</span></span> <span data-ttu-id="8d6de-126">相反，您将使用任务模块显示用于收集其他信息的表单，并显示列表中项目的详细信息，或任何其他需要向用户提供其他信息的时间。</span><span class="sxs-lookup"><span data-stu-id="8d6de-126">Instead, you will use task modules to present forms for gathering additional information, displaying the details of an item in a list, or any other time you need to present the user with additional information.</span></span> <span data-ttu-id="8d6de-127">任务模块本身可以是其他内容页，也可以完全使用自适应卡片创建。</span><span class="sxs-lookup"><span data-stu-id="8d6de-127">The task modules themselves can be additional content pages, or created completely using Adaptive Cards.</span></span> <span data-ttu-id="8d6de-128">有关完整信息，请参阅[在选项卡中使用任务模块](~/task-modules-and-cards/task-modules/task-modules-tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="8d6de-128">See [Using task modules in tabs](~/task-modules-and-cards/task-modules/task-modules-tabs.md) for complete information.</span></span>

### <a name="valid-domains"></a><span data-ttu-id="8d6de-129">有效的域</span><span class="sxs-lookup"><span data-stu-id="8d6de-129">Valid Domains</span></span>

<span data-ttu-id="8d6de-130">确保您的选项卡中使用的所有 URL 域都包含在`validDomains` [清单](~/concepts/build-and-test/apps-package.md)中的阵列中。</span><span class="sxs-lookup"><span data-stu-id="8d6de-130">Ensure that the all URL domains used in your tabs are included in the `validDomains` array in your [manifest](~/concepts/build-and-test/apps-package.md).</span></span> <span data-ttu-id="8d6de-131">有关详细信息，请参阅清单架构参考中的[validDomains](~/resources/schema/manifest-schema.md#validdomains) 。</span><span class="sxs-lookup"><span data-stu-id="8d6de-131">For more information, see [validDomains](~/resources/schema/manifest-schema.md#validdomains) in the manifest schema reference.</span></span> <span data-ttu-id="8d6de-132">但是，请注意，您的选项卡的核心功能在团队中，而不是在团队外部。</span><span class="sxs-lookup"><span data-stu-id="8d6de-132">However, be mindful that the core functionality of your tab exists within Teams and not outside of Teams.</span></span>
