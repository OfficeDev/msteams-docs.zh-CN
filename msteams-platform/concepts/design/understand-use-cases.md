---
title: 了解应用的用例
author: heath-hamilton
description: 在规划Microsoft Teams应用时，应首先了解应用尝试解决的问题。
ms.topic: conceptual
localization_priority: Normal
ms.author: anclear
ms.openlocfilehash: 918f9f906136d4acd466ce54922588ce34a7e4ef
ms.sourcegitcommit: 14409950307b135265c8582408be5277b35131dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/17/2021
ms.locfileid: "52994096"
---
# <a name="understand-your-use-cases"></a><span data-ttu-id="7fbf6-103">了解用例</span><span class="sxs-lookup"><span data-stu-id="7fbf6-103">Understand your use cases</span></span>

<span data-ttu-id="7fbf6-104">Microsoft Teams平台提供了应用可以利用的各种入口点和[UI](../../concepts/extensibility-points.md)元素。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-104">The Microsoft Teams platform offers a large variety of [entry points and UI elements](../../concepts/extensibility-points.md) your app can take advantage of.</span></span>
> [!NOTE]
> <span data-ttu-id="7fbf6-105">在开始构建用例之前，你必须深入了解Teams功能，以及使用这些功能的 Teams功能。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-105">Before you start building your use cases, you must have a good understanding of Teams capabilities and what is possible on the Teams platform using them.</span></span>

<span data-ttu-id="7fbf6-106">与用户交互的每个方法都有其优点和缺点。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-106">Each method of interacting with your users has its strengths and weaknesses.</span></span> <span data-ttu-id="7fbf6-107">在应用中Teams出色的功能与找到满足用户需求的正确组合有关。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-107">Building an awesome Teams app is all about finding the right combination to meet your user's needs.</span></span> <span data-ttu-id="7fbf6-108">如果要满足这些需求，首先需要了解这些需求。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-108">If you are going to meet those needs, you first need to understand them.</span></span>

## <a name="understand-the-problem"></a><span data-ttu-id="7fbf6-109">了解问题</span><span class="sxs-lookup"><span data-stu-id="7fbf6-109">Understand the problem</span></span>

<span data-ttu-id="7fbf6-110">每个良好的应用都有一个核心问题或需要它尝试解决。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-110">Every good app has a core problem or a need it is trying to solve.</span></span> <span data-ttu-id="7fbf6-111">在开始生成应用之前，你需要阐明该问题是什么。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-111">Before you start building an app, you need to articulate what that problem is.</span></span> <span data-ttu-id="7fbf6-112">其中心Teams是一个协作平台，因此，在实现有效协作方面架起桥梁的应用非常适合。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-112">At its heart, Teams is a collaboration platform, so apps that bridge gaps in achieving effective collaboration are a great fit.</span></span> <span data-ttu-id="7fbf6-113">它还是一个社交平台，本机跨平台，位于Office 365的核心，并提供个人画布，让你创建应用。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-113">It is also a social platform, is natively cross-platform, sits at the heart of Office 365, and offers a personal canvas for you to create apps.</span></span> <span data-ttu-id="7fbf6-114">在此社交平台中，可以通过一款应用满足各种Teams需求。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-114">In this social platform, there is a wide variety of needs that can be solved with a Teams app.</span></span> <span data-ttu-id="7fbf6-115">如果了解要尝试解决的问题，就可以解决各种各样的问题。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-115">You can solve wide variety of problems, provided you understand which one you are trying to solve.</span></span> <span data-ttu-id="7fbf6-116">在开始生成应用之前，请提出相关问题，例如：</span><span class="sxs-lookup"><span data-stu-id="7fbf6-116">Before you start building an app, ask relevant questions, such as:</span></span>

* <span data-ttu-id="7fbf6-117">用户当前使用的状态系统的优缺点是什么？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-117">What are the pros and cons of the current state system used by your users?</span></span>
* <span data-ttu-id="7fbf6-118">自今天起，你的用户要解决的难处是什么？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-118">What are the pain points your users face as of today that you wish to address?</span></span>
* <span data-ttu-id="7fbf6-119">用户在当前执行此过程的方式中喜欢和喜欢哪些功能？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-119">What features or capabilities your users like and love in their current way of doing the process?</span></span>

## <a name="understand-your-user"></a><span data-ttu-id="7fbf6-120">了解用户</span><span class="sxs-lookup"><span data-stu-id="7fbf6-120">Understand your user</span></span>

<span data-ttu-id="7fbf6-121">了解你的用户是谁，并且你可以确定正确的分发模型，但更重要的是，它可以帮助你确定用户如何使用Teams。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-121">Understand who your user is and you can identify the right distribution model but more importantly, it helps you to identify how users use Teams.</span></span> <span data-ttu-id="7fbf6-122">提出相关问题，例如：</span><span class="sxs-lookup"><span data-stu-id="7fbf6-122">Ask relevant questions, such as:</span></span>

* <span data-ttu-id="7fbf6-123">用户主要是移动客户端上的一线工作人员吗？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-123">Are the users primarily front-line workers on mobile clients?</span></span>
* <span data-ttu-id="7fbf6-124">你是否希望大量来宾用户需要访问你的应用？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-124">Do you expect a lot of guest users to need access to your app?</span></span>
* <span data-ttu-id="7fbf6-125">他们使用团队和频道还是主要使用群聊？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-125">Do they use teams and channels or primarily group chats?</span></span>
* <span data-ttu-id="7fbf6-126">主要用户的技术有多复杂？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-126">How technically sophisticated are your primary users?</span></span>
* <span data-ttu-id="7fbf6-127">是否需要全面的载入体验或一些指针？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-127">Do you need a thorough onboarding experience or a few pointers might do?</span></span>

<span data-ttu-id="7fbf6-128">有时答案是，我们希望为任何地方的所有Teams *解决此问题。*</span><span class="sxs-lookup"><span data-stu-id="7fbf6-128">Sometimes the answer is, *We want to solve this problem for all Teams users everywhere.*</span></span> <span data-ttu-id="7fbf6-129">如果是这种情况，请花些时间了解发布到 [AppSource 需要哪些时间](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-129">If that is the case for you, spend some time understanding [what it takes to get published to AppSource](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).</span></span>

## <a name="understand-the-limitations-of-the-app"></a><span data-ttu-id="7fbf6-130">了解应用程序的限制</span><span class="sxs-lookup"><span data-stu-id="7fbf6-130">Understand the limitations of the app</span></span>

<span data-ttu-id="7fbf6-131">了解应用在数据辅助功能和数据驻留要求方面的限制将有助于你设计更好的应用。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-131">Knowing the limitations of the apps in terms of data accessibility and data residency requirement will help you design better apps.</span></span> <span data-ttu-id="7fbf6-132">这一点很重要，因为了解谁拥有 API 的数据和可用性会影响解决方案体系结构。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-132">This is important, as having information on who owns the data and availability of APIs impacts the solution architecture.</span></span> <span data-ttu-id="7fbf6-133">同样，请提出相关问题，例如：</span><span class="sxs-lookup"><span data-stu-id="7fbf6-133">Again, ask relevant questions, such as:</span></span>

* <span data-ttu-id="7fbf6-134">当前应用的后端集成面临的难题是什么？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-134">What are the challenges with back end integration of the current app?</span></span>
* <span data-ttu-id="7fbf6-135">Who拥有后端数据？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-135">Who owns the back end data?</span></span> <span data-ttu-id="7fbf6-136">内部或第三方。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-136">In-house or third-party.</span></span>
* <span data-ttu-id="7fbf6-137">是否有影响应用正常运行的防火墙？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-137">Are there firewalls that impact the functioning of the app?</span></span>
* <span data-ttu-id="7fbf6-138">是否有 API 可以访问运行应用所需的数据？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-138">Are there APIs to access the data you need for functioning of your app?</span></span> 

## <a name="provide-authentication"></a><span data-ttu-id="7fbf6-139">提供身份验证</span><span class="sxs-lookup"><span data-stu-id="7fbf6-139">Provide authentication</span></span>

<span data-ttu-id="7fbf6-140">您必须提前确定是否需要保护要公开的服务以及处于什么级别。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-140">You must identify early on if you need to protect the services you are exposing and at what level.</span></span> <span data-ttu-id="7fbf6-141">请记住，Teams应用程序中公开的 Web 服务通过 Internet 公开提供。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-141">Remember, the web services exposed in your Teams app are publicly available over the internet.</span></span> <span data-ttu-id="7fbf6-142">因此，如果你需要保护他们，立即开始思考它。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-142">So, if you need to secure them start thinking about it now.</span></span> <span data-ttu-id="7fbf6-143">如果需要一个解决方案，要求您为租户之外的用户提供来宾访问，则需要设置访问限制和权限来保护机密信息。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-143">If you need a solution that requires you to provide guest access for users outside the tenant, access restrictions and permissions need to be placed to protect confidential information.</span></span> <span data-ttu-id="7fbf6-144">需要考虑来宾用户访问的限制，需要设计应用。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-144">You will need to design apps considering the limitations that come with guest user access.</span></span> <span data-ttu-id="7fbf6-145">因此，请提问，例如：</span><span class="sxs-lookup"><span data-stu-id="7fbf6-145">Therefore, ask questions, such as:</span></span> 

* <span data-ttu-id="7fbf6-146">用户将基于其角色访问不同的数据视图吗？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-146">Will the users access different views of data based on their roles?</span></span>
* <span data-ttu-id="7fbf6-147">是否涉及 PII？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-147">Is there PII involved?</span></span>
* <span data-ttu-id="7fbf6-148">交互还会基于用户角色吗？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-148">Will the interactions also be based on the user roles?</span></span>
* <span data-ttu-id="7fbf6-149">外部用户将访问该应用吗？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-149">Will external users access the app?</span></span>

## <a name="decide-what-goes-in-teams"></a><span data-ttu-id="7fbf6-150">确定要Teams</span><span class="sxs-lookup"><span data-stu-id="7fbf6-150">Decide what goes in Teams</span></span>

<span data-ttu-id="7fbf6-151">无论是构建新的解决方案还是将现有解决方案引入Teams，决定整个应用是否将位于 Teams 客户端中非常重要。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-151">Whether you are building something new or bringing an existing solution into Teams, it is important to decide if the entire app is going to be inside the Teams client.</span></span> <span data-ttu-id="7fbf6-152">检查仅引入部分体验是否有意义。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-152">Check if it makes sense to only bring in a portion of the experience.</span></span> <span data-ttu-id="7fbf6-153">通过选项卡、消息传递扩展、任务模块、自适应卡片和对话机器人的组合，你可以完全在 Teams。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-153">With a combination of tabs, messaging extensions, task modules, Adaptive Cards, and conversational bots you can build complex apps completely in Teams.</span></span>
<span data-ttu-id="7fbf6-154">请记住您的用户是谁以及您尝试解决的问题。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-154">Remember who your users are and the problem you are trying to solve.</span></span> <span data-ttu-id="7fbf6-155">他们已有一个系统来解决大多数问题，或者你只需将功能的一个子集扩展到Teams？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-155">Do they already have a system for solving most of the problem or you just need to extend a sub-set of the functionality into Teams?</span></span> <span data-ttu-id="7fbf6-156">通常，如果要引入解决方案的一部分，则必须专注于共享、协作、启动和监视工作流。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-156">Typically, if you are going to bring in a portion of your solution, you must focus on sharing, collaborating, initiating, and monitoring workflows.</span></span>

## <a name="plan-the-onboarding-experience"></a><span data-ttu-id="7fbf6-157">规划载入体验</span><span class="sxs-lookup"><span data-stu-id="7fbf6-157">Plan the onboarding experience</span></span>

<span data-ttu-id="7fbf6-158">应用的载入体验可能是成功还是失败的区别。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-158">Your onboarding experience can be the difference between success or failure for your app.</span></span> <span data-ttu-id="7fbf6-159">对于应用的每个功能以及可以安装该功能的每个上下文，你必须制定一个计划，了解如何进行自我介绍。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-159">For each capability of your app and each context that capability can be installed in, you must have a plan for how you are going to introduce yourself.</span></span> <span data-ttu-id="7fbf6-160">在一对一聊天中安装对话机器人时，在一对一聊天中安装聊天机器人时，其介绍方式有所不同。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-160">How you introduce your conversational bot when it is installed in a channel with a thousand people, is different when it is installed in a one-to-one chat.</span></span> <span data-ttu-id="7fbf6-161">当用户首次在频道中配置选项卡时会发生什么情况？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-161">What happens when a user first configures your tab in a channel?</span></span> <span data-ttu-id="7fbf6-162">如果你使用消息传递扩展共享卡片，向"了解更多"页面添加一个小链接以帮助向用户介绍你的应用还可以执行哪些操作是否有意义？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-162">If you are sharing cards with a messaging extension, does it make sense to add a small link to a **learn more** page to help introduce users to what else your app can do?</span></span>

<span data-ttu-id="7fbf6-163">了解用户是谁有助于打造正确的体验。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-163">Knowing who your users are helps you to craft the right experience.</span></span> <span data-ttu-id="7fbf6-164">你是否希望大多数用户已经拥有你的应用所针对的一些上下文，或者已经在另一个上下文中使用了你的服务？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-164">Do you expect most people to already have some context of what your app is for, or to have already used your services in another context?</span></span> <span data-ttu-id="7fbf6-165">他们之前是否没有任何知识进入你的应用？</span><span class="sxs-lookup"><span data-stu-id="7fbf6-165">Are they coming to your app with no prior knowledge?</span></span> <span data-ttu-id="7fbf6-166">请牢记关键用户的载入体验。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-166">Craft your onboarding experience with your key users in mind.</span></span>

<span data-ttu-id="7fbf6-167">请记住，用户可以以多种方式发现你的应用。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-167">Remember, users can discover your app in a variety of ways.</span></span> <span data-ttu-id="7fbf6-168">他们可能是安装应用的用户，或者当另一个用户使用它来共享内容时，可能会将其引入你的应用。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-168">They might be the ones installing it or they might be introduced to your app when another user uses it to share content.</span></span> <span data-ttu-id="7fbf6-169">如果你希望更多用户使用你的应用，则必须寻找向每个人介绍自己的方法。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-169">If you want more users to use your app, you must look for ways to introduce yourself to everyone.</span></span>

<span data-ttu-id="7fbf6-170">最重要的是，请记住没有人喜欢垃圾邮件。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-170">Above all, remember that nobody likes spam.</span></span> <span data-ttu-id="7fbf6-171">使用个人和频道消息进行爆炸是快速取消安装的良好方法！</span><span class="sxs-lookup"><span data-stu-id="7fbf6-171">Blasting away with personal and channel messages is a good way to get un-installed quickly!</span></span>

## <a name="plan-for-the-future"></a><span data-ttu-id="7fbf6-172">规划未来</span><span class="sxs-lookup"><span data-stu-id="7fbf6-172">Plan for the future</span></span>

<span data-ttu-id="7fbf6-173">确定用户希望在当前解决方案中具有的新功能。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-173">Identify which new features the user will prefer to have in the current solution.</span></span> <span data-ttu-id="7fbf6-174">如果你有要添加到应用的新功能的路线图，则设计和体系结构将受到影响。</span><span class="sxs-lookup"><span data-stu-id="7fbf6-174">If you have a roadmap for new features to add to the app, the design and architecture will be impacted.</span></span>

## <a name="see-also"></a><span data-ttu-id="7fbf6-175">另请参阅</span><span class="sxs-lookup"><span data-stu-id="7fbf6-175">See also</span></span>

* [<span data-ttu-id="7fbf6-176">选择如何发布应用程序</span><span class="sxs-lookup"><span data-stu-id="7fbf6-176">Choose how to distribute your app</span></span>](../deploy-and-publish/apps-publish-overview.md)
* [<span data-ttu-id="7fbf6-177">设计选项卡</span><span class="sxs-lookup"><span data-stu-id="7fbf6-177">Design tabs</span></span>](../../tabs/design/tabs.md)
* [<span data-ttu-id="7fbf6-178">设计机器人</span><span class="sxs-lookup"><span data-stu-id="7fbf6-178">Design bots</span></span>](../../bots/design/bots.md)

## <a name="next-step"></a><span data-ttu-id="7fbf6-179">后续步骤</span><span class="sxs-lookup"><span data-stu-id="7fbf6-179">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7fbf6-180">映射用例</span><span class="sxs-lookup"><span data-stu-id="7fbf6-180">Map your use cases</span></span>](../../concepts/design/map-use-cases.md)
