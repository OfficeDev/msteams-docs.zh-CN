---
title: 了解团队应用程序功能
author: heath-hamilton
description: ''
ms.topic: overview
ms.author: heath-hamilton
ms.openlocfilehash: 580d75b648bde1caf0e85647c89635804c91fb70
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651909"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="0f6a1-102">了解团队应用程序功能</span><span class="sxs-lookup"><span data-stu-id="0f6a1-102">Understanding Teams app capabilities</span></span>

<span data-ttu-id="0f6a1-103">*功能*是在 Microsoft 团队平台上构建应用程序的扩展点。</span><span class="sxs-lookup"><span data-stu-id="0f6a1-103">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="0f6a1-104">有多种方法可以扩展团队客户端，因此每个应用程序都是唯一的：某些应用程序具有一项功能 (如 webhook) ，而另一些则可以提供用户选项。</span><span class="sxs-lookup"><span data-stu-id="0f6a1-104">There are multiple ways to extend the Teams client, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="0f6a1-105">例如，您的应用程序可以在中心位置 ("选项卡中显示数据) 并通过会话界面 (bot) 提供相同的信息。</span><span class="sxs-lookup"><span data-stu-id="0f6a1-105">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="0f6a1-106">你的团队应用可以具有以下核心功能中的一个或所有：</span><span class="sxs-lookup"><span data-stu-id="0f6a1-106">Your Teams app can have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="0f6a1-107">选项卡</span><span class="sxs-lookup"><span data-stu-id="0f6a1-107">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="0f6a1-108">消息扩展</span><span class="sxs-lookup"><span data-stu-id="0f6a1-108">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="0f6a1-109">Webhook 和连接器</span><span class="sxs-lookup"><span data-stu-id="0f6a1-109">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)
* [<span data-ttu-id="0f6a1-110">机器人</span><span class="sxs-lookup"><span data-stu-id="0f6a1-110">Bots</span></span>](../bots/what-are-bots.md)

<span data-ttu-id="0f6a1-111">您的应用程序还可以利用高级功能，例如[Microsoft GRAPH REST API](../graph-api/rsc/resource-specific-consent.md)。</span><span class="sxs-lookup"><span data-stu-id="0f6a1-111">Your app can also can take advantage of advanced capabilities, such as the [Microsoft Graph REST API](../graph-api/rsc/resource-specific-consent.md).</span></span>

<span data-ttu-id="0f6a1-112">请参阅下图，了解哪些功能将在您的应用程序中提供所需的功能。</span><span class="sxs-lookup"><span data-stu-id="0f6a1-112">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

![说明团队应用程序功能是什么的构思图](doc-links/images/capabilities-overview.png)

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="0f6a1-114">执行最适合您的用户的操作</span><span class="sxs-lookup"><span data-stu-id="0f6a1-114">Doing what's best for your users</span></span>

<span data-ttu-id="0f6a1-115">在熟悉团队应用程序开发的过程中，您将开始了解其 subtleties。</span><span class="sxs-lookup"><span data-stu-id="0f6a1-115">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="0f6a1-116">有多种方法可以生成某些功能 (如收集用户输入) 。</span><span class="sxs-lookup"><span data-stu-id="0f6a1-116">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="0f6a1-117">例如，可以使用将基于 web 的窗体嵌入在选项卡中 `<iframe>` 。</span><span class="sxs-lookup"><span data-stu-id="0f6a1-117">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="0f6a1-118">此外，您还可以使用任务模块（团队 UI 约定）在选项卡中执行此操作，以获得用户可能喜欢的更真实的体验。</span><span class="sxs-lookup"><span data-stu-id="0f6a1-118">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="0f6a1-119">选择功能和 UI 约定、控件和元素的正确组合，可以先[了解受众的用例](../concepts/design/understand-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="0f6a1-119">Choosing the right combination of capabilities and UI conventions, controls, and elements comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>

## <a name="learn-more"></a><span data-ttu-id="0f6a1-120">了解详细信息</span><span class="sxs-lookup"><span data-stu-id="0f6a1-120">Learn more</span></span>

* [<span data-ttu-id="0f6a1-121">开始规划您的应用程序</span><span class="sxs-lookup"><span data-stu-id="0f6a1-121">Start planning your app</span></span>](../concepts/extensibility-points.md)
