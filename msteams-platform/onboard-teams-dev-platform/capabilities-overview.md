---
title: 了解团队应用程序功能
author: heath-hamilton
description: 团队平台功能概述，这些功能是用于生成团队应用程序的扩展点。
ms.topic: overview
ms.author: lajanuar
ms.openlocfilehash: 9bb94d2cfd5c30b2245c5ccf580d374972315e72
ms.sourcegitcommit: d3bb4bbcdff9545c9869647dcdbe563a2db868be
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/18/2020
ms.locfileid: "47964562"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="972df-103">了解团队应用程序功能</span><span class="sxs-lookup"><span data-stu-id="972df-103">Understanding Teams app capabilities</span></span>

<span data-ttu-id="972df-104">*功能* 是在 Microsoft 团队平台上构建应用程序的扩展点。</span><span class="sxs-lookup"><span data-stu-id="972df-104">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="972df-105">有多种方法可以扩展团队客户端，因此每个应用程序都是唯一的：某些应用程序具有一项功能 (如 webhook) ，而另一些则可以提供用户选项。</span><span class="sxs-lookup"><span data-stu-id="972df-105">There are multiple ways to extend the Teams client, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="972df-106">例如，您的应用程序可以在中心位置 ("选项卡中显示数据) 并通过会话界面 (bot) 提供相同的信息。</span><span class="sxs-lookup"><span data-stu-id="972df-106">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="972df-107">你的团队应用可以具有以下核心功能中的一个或所有：</span><span class="sxs-lookup"><span data-stu-id="972df-107">Your Teams app can have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="972df-108">选项卡</span><span class="sxs-lookup"><span data-stu-id="972df-108">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="972df-109">消息扩展</span><span class="sxs-lookup"><span data-stu-id="972df-109">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="972df-110">Webhook 和连接器</span><span class="sxs-lookup"><span data-stu-id="972df-110">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)
* [<span data-ttu-id="972df-111">机器人</span><span class="sxs-lookup"><span data-stu-id="972df-111">Bots</span></span>](../bots/what-are-bots.md)

<span data-ttu-id="972df-112">您的应用程序还可以利用高级功能，例如 [Microsoft GRAPH REST API](../graph-api/rsc/resource-specific-consent.md)。</span><span class="sxs-lookup"><span data-stu-id="972df-112">Your app can also can take advantage of advanced capabilities, such as the [Microsoft Graph REST API](../graph-api/rsc/resource-specific-consent.md).</span></span>

<span data-ttu-id="972df-113">请参阅下图，了解哪些功能将在您的应用程序中提供所需的功能。</span><span class="sxs-lookup"><span data-stu-id="972df-113">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

![说明团队应用程序功能是什么的构思图](doc-links/images/capabilities-overview.png)

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="972df-115">执行最适合您的用户的操作</span><span class="sxs-lookup"><span data-stu-id="972df-115">Doing what's best for your users</span></span>

<span data-ttu-id="972df-116">在熟悉团队应用程序开发的过程中，您将开始了解其 subtleties。</span><span class="sxs-lookup"><span data-stu-id="972df-116">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="972df-117">有多种方法可以生成某些功能 (如收集用户输入) 。</span><span class="sxs-lookup"><span data-stu-id="972df-117">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="972df-118">例如，可以使用将基于 web 的窗体嵌入在选项卡中 `<iframe>` 。</span><span class="sxs-lookup"><span data-stu-id="972df-118">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="972df-119">此外，您还可以使用任务模块（团队 UI 约定）在选项卡中执行此操作，以获得用户可能喜欢的更真实的体验。</span><span class="sxs-lookup"><span data-stu-id="972df-119">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="972df-120">选择功能和 UI 约定、控件和元素的正确组合，可以先 [了解受众的用例](../concepts/design/understand-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="972df-120">Choosing the right combination of capabilities and UI conventions, controls, and elements comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>

## <a name="learn-more"></a><span data-ttu-id="972df-121">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="972df-121">Learn more</span></span>

* [<span data-ttu-id="972df-122">开始规划您的应用程序</span><span class="sxs-lookup"><span data-stu-id="972df-122">Start planning your app</span></span>](../concepts/extensibility-points.md)
