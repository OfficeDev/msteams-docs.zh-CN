---
title: 了解团队应用程序功能
author: heath-hamilton
description: 团队应用程序功能说明
ms.topic: conceptual
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: e7a6fe61fa5c74547ce20cc895afdd044f35e512
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210161"
---
# <a name="understanding-teams-app-capabilities"></a><span data-ttu-id="d0dce-103">了解团队应用程序功能</span><span class="sxs-lookup"><span data-stu-id="d0dce-103">Understanding Teams app capabilities</span></span>

<span data-ttu-id="d0dce-104">*功能* 是在 Microsoft 团队平台上构建应用程序的扩展点。</span><span class="sxs-lookup"><span data-stu-id="d0dce-104">*Capabilities* are the extension points for building apps on the Microsoft Teams platform.</span></span>

<span data-ttu-id="d0dce-105">有多种方法可以扩展团队，因此每个应用程序都是唯一的：某些应用程序具有一项功能 (如 webhook) ，而另一些则提供用户选项。</span><span class="sxs-lookup"><span data-stu-id="d0dce-105">There are multiple ways to extend Teams, so every app is unique: Some only have one capability (such as a webhook), while others have a few to give users options.</span></span> <span data-ttu-id="d0dce-106">例如，您的应用程序可以在中心位置 ("选项卡中显示数据) 并通过会话界面 (bot) 提供相同的信息。</span><span class="sxs-lookup"><span data-stu-id="d0dce-106">For instance, your app could display data in a central location (tab) and present that same information through a conversational interface (bot).</span></span>

<span data-ttu-id="d0dce-107">你的团队应用可以具有以下核心功能中的一个或所有：</span><span class="sxs-lookup"><span data-stu-id="d0dce-107">Your Teams app can have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="d0dce-108">选项卡</span><span class="sxs-lookup"><span data-stu-id="d0dce-108">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="d0dce-109">消息扩展</span><span class="sxs-lookup"><span data-stu-id="d0dce-109">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="d0dce-110">机器人</span><span class="sxs-lookup"><span data-stu-id="d0dce-110">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="d0dce-111">Webhook 和连接器</span><span class="sxs-lookup"><span data-stu-id="d0dce-111">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="d0dce-112">您的应用程序还可以利用高级功能，例如 [Microsoft GRAPH API For 团队](https://docs.microsoft.com/graph/teams-concept-overview)。</span><span class="sxs-lookup"><span data-stu-id="d0dce-112">Your app can also can take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="d0dce-113">请参阅下图，了解哪些功能将在您的应用程序中提供所需的功能。</span><span class="sxs-lookup"><span data-stu-id="d0dce-113">See the following illustration to get an idea which capabilities would provide the features you want in your app.</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="阐明了团队应用功能的构思图。":::

## <a name="doing-whats-best-for-your-users"></a><span data-ttu-id="d0dce-115">执行最适合您的用户的操作</span><span class="sxs-lookup"><span data-stu-id="d0dce-115">Doing what's best for your users</span></span>

<span data-ttu-id="d0dce-116">在熟悉团队应用程序开发的过程中，您将开始了解其 subtleties。</span><span class="sxs-lookup"><span data-stu-id="d0dce-116">As you familiarize yourself with Teams app development, you'll begin to understand its subtleties.</span></span> <span data-ttu-id="d0dce-117">有多种方法可以生成某些功能 (如收集用户输入) 。</span><span class="sxs-lookup"><span data-stu-id="d0dce-117">There's more than one way to build certain features (such as collecting user input).</span></span> <span data-ttu-id="d0dce-118">例如，可以使用将基于 web 的窗体嵌入在选项卡中 `<iframe>` 。</span><span class="sxs-lookup"><span data-stu-id="d0dce-118">For example, you could embed a web-based form in a tab using an `<iframe>`.</span></span> <span data-ttu-id="d0dce-119">此外，您还可以使用任务模块（团队 UI 约定）在选项卡中执行此操作，以获得用户可能喜欢的更真实的体验。</span><span class="sxs-lookup"><span data-stu-id="d0dce-119">You could also do this in a tab using a task module, a Teams UI convention, for a more native experience your users may prefer.</span></span>

<span data-ttu-id="d0dce-120">选择适当的功能和设计可先 [了解观众的用例](../concepts/design/understand-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="d0dce-120">Choosing the right capabilities and design comes down to first [understanding your audience's use cases](../concepts/design/understand-use-cases.md).</span></span>
