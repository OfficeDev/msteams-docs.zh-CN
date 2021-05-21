---
title: 了解应用功能
author: heath-hamilton
description: Teams说明的应用功能
ms.topic: conceptual
localization_priority: Normal
ms.author: lajanuar
ms.date: 09/22/2020
ms.openlocfilehash: 209d187681b1370440931fcd40744965395b13e8
ms.sourcegitcommit: 51e4a1464ea58c254ad6bd0317aca03ebf6bf1f6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/19/2021
ms.locfileid: "52565149"
---
# <a name="understand-microsoft-teams-app-capabilities"></a><span data-ttu-id="c7a0b-103">了解Microsoft Teams应用功能</span><span class="sxs-lookup"><span data-stu-id="c7a0b-103">Understand Microsoft Teams app capabilities</span></span>

<span data-ttu-id="c7a0b-104">扩展性或入口点是应用向用户自我清单的不同方式。</span><span class="sxs-lookup"><span data-stu-id="c7a0b-104">Extensibility or entry points are different ways in which an app can manifest itself to a user.</span></span> <span data-ttu-id="c7a0b-105">例如，用户可以与画布选项卡上的应用交互以执行活动，或者可能会选择使用对话机器人执行相同的操作。</span><span class="sxs-lookup"><span data-stu-id="c7a0b-105">For example, a user can interact with an app on a canvas tab to do an activity or might choose to do the same using a conversational bot.</span></span> <span data-ttu-id="c7a0b-106">用于生成应用的各种Teams允许你增加其使用范围。</span><span class="sxs-lookup"><span data-stu-id="c7a0b-106">The various capabilities used to build your Teams app allow you to increase its usage scope.</span></span>

<span data-ttu-id="c7a0b-107">有多种方法可以扩展Teams，因此每个应用都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="c7a0b-107">There are multiple ways to extend Teams, so every app is unique.</span></span> <span data-ttu-id="c7a0b-108">有些仅具有一个功能，如 webhook，而其他功能则具有多个功能来为用户提供各种选项。</span><span class="sxs-lookup"><span data-stu-id="c7a0b-108">Some only have one capability, such as a webhook, while others have more than one feature to give users various options.</span></span> <span data-ttu-id="c7a0b-109">例如，你的应用可以在中心位置（即选项卡）中显示数据，并通过对话界面（即自动程序）显示相同的 **信息**。</span><span class="sxs-lookup"><span data-stu-id="c7a0b-109">For example, your app can display data in a central location, that is, the **tab** and present that same information through a conversational interface, that is, the **bot**.</span></span>

## <a name="app-capabilities"></a><span data-ttu-id="c7a0b-110">应用功能</span><span class="sxs-lookup"><span data-stu-id="c7a0b-110">App capabilities</span></span>

<span data-ttu-id="c7a0b-111">你的Teams应用具有以下一项或全部核心功能：</span><span class="sxs-lookup"><span data-stu-id="c7a0b-111">Your Teams app have one or all of the following core capabilities:</span></span>

* [<span data-ttu-id="c7a0b-112">选项卡</span><span class="sxs-lookup"><span data-stu-id="c7a0b-112">Tabs</span></span>](../tabs/what-are-tabs.md)
* [<span data-ttu-id="c7a0b-113">消息扩展</span><span class="sxs-lookup"><span data-stu-id="c7a0b-113">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)
* [<span data-ttu-id="c7a0b-114">机器人</span><span class="sxs-lookup"><span data-stu-id="c7a0b-114">Bots</span></span>](../bots/what-are-bots.md)
* [<span data-ttu-id="c7a0b-115">Webhook 和连接器</span><span class="sxs-lookup"><span data-stu-id="c7a0b-115">Webhooks and connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)

<span data-ttu-id="c7a0b-116">你的应用还可以利用高级功能，例如 Microsoft Graph API [for Teams。](/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="c7a0b-116">Your app can also take advantage of advanced capabilities, such as the [Microsoft Graph API for Teams](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="c7a0b-117">下图展示了哪些功能将为你提供你需要的应用功能：</span><span class="sxs-lookup"><span data-stu-id="c7a0b-117">The following illustration gives you an idea of which capabilities will provide the features you want in your app:</span></span>

:::image type="content" source="../assets/images/capabilities-overview.png" alt-text="&quot;心图&quot;Teams应用功能是什么。":::

## <a name="always-consider-your-user"></a><span data-ttu-id="c7a0b-119">始终考虑你的用户</span><span class="sxs-lookup"><span data-stu-id="c7a0b-119">Always consider your user</span></span>

<span data-ttu-id="c7a0b-120">在熟悉应用开发Teams，了解它的核心基础。</span><span class="sxs-lookup"><span data-stu-id="c7a0b-120">As you familiarize yourself with Teams app development, you understand its core fundamentals.</span></span> <span data-ttu-id="c7a0b-121">您了解到存在多个生成特定功能的方法。</span><span class="sxs-lookup"><span data-stu-id="c7a0b-121">You understand that there is more than one way to build certain features.</span></span> <span data-ttu-id="c7a0b-122">在这种情况下，请考虑如何为用户提供更本机的体验。</span><span class="sxs-lookup"><span data-stu-id="c7a0b-122">In such scenarios, consider how you can provide a more native experience to your user.</span></span>
<span data-ttu-id="c7a0b-123">例如，可以在作为应用程序中的选项卡构建的表单中收集用户输入。</span><span class="sxs-lookup"><span data-stu-id="c7a0b-123">For example, you can collect user input in a form built as a tab in the app.</span></span> <span data-ttu-id="c7a0b-124">您还可以使用任务模块完成此操作，而无需切换视图和中断用户的工作流程。</span><span class="sxs-lookup"><span data-stu-id="c7a0b-124">You can also do this using a task module without switching views and disrupting user's flow of work.</span></span> <span data-ttu-id="c7a0b-125">选择与用户常规工作流程的偏差最小的扩展点很重要。</span><span class="sxs-lookup"><span data-stu-id="c7a0b-125">It is important to choose extension points that provide least deviation from a user's regular flow of work.</span></span>

## <a name="see-also"></a><span data-ttu-id="c7a0b-126">另请参阅</span><span class="sxs-lookup"><span data-stu-id="c7a0b-126">See also</span></span>

[<span data-ttu-id="c7a0b-127">生成适用于Teams</span><span class="sxs-lookup"><span data-stu-id="c7a0b-127">Build apps for Teams</span></span>](../overview.md)

## <a name="next-step"></a><span data-ttu-id="c7a0b-128">后续步骤</span><span class="sxs-lookup"><span data-stu-id="c7a0b-128">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c7a0b-129">团队应用程序入口点</span><span class="sxs-lookup"><span data-stu-id="c7a0b-129">Teams app entry points</span></span>](../concepts/extensibility-points.md)
