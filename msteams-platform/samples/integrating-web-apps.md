---
author: heath-hamilton
description: 将现有 web 应用与 Microsoft 团队集成的最佳实践
ms.author: v-heha
ms.date: 08/26/2020
ms.topic: conceptual
title: 将 web 应用与 Microsoft 团队集成
ms.openlocfilehash: e7d4f74526f7a71fe33d5a70d9ed60be960adefc
ms.sourcegitcommit: 1aa0b172931d0f81db346452788c41dc4a6717b9
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/22/2020
ms.locfileid: "48210160"
---
# <a name="integrate-web-apps-with-teams"></a><span data-ttu-id="b1e71-103">将 web 应用与团队集成</span><span class="sxs-lookup"><span data-stu-id="b1e71-103">Integrate web apps with Teams</span></span>

<span data-ttu-id="b1e71-104">您是否有您认为可自然符合团队社会和协作功能的 web 应用程序？</span><span class="sxs-lookup"><span data-stu-id="b1e71-104">Do you have a web app you think would fit naturally with Teams' social and collaborative features?</span></span> <span data-ttu-id="b1e71-105">这些指南可帮助您了解如何集成以下类型的应用程序：</span><span class="sxs-lookup"><span data-stu-id="b1e71-105">These guidelines can help you understand how to integrate the following types of apps:</span></span>

* <span data-ttu-id="b1e71-106">**独立应用程序**：可以是单页应用或大型、复杂的应用程序，您希望用户使用团队中的某些方面。</span><span class="sxs-lookup"><span data-stu-id="b1e71-106">**Standalone apps**: Could be a single-page app or large, complex app you want people to use some aspects of in Teams.</span></span>
* <span data-ttu-id="b1e71-107">**协作应用**程序：已为团队固有的社会和协作功能构建的应用程序。</span><span class="sxs-lookup"><span data-stu-id="b1e71-107">**Collaboration apps**: An app already built for the social and collaborative features inherent to Teams.</span></span>
* <span data-ttu-id="b1e71-108">**Sharepoint**：要在团队中呈现的 sharepoint 页面。</span><span class="sxs-lookup"><span data-stu-id="b1e71-108">**SharePoint**: A SharePoint page you want to surface in Teams.</span></span>

<span data-ttu-id="b1e71-109">对于每个准则，您都可以查看它是否适用于您的集成方案。</span><span class="sxs-lookup"><span data-stu-id="b1e71-109">For each guideline, you can see if it's applicable to your integration scenario.</span></span>

## <a name="get-to-know-teams-platform-capabilities"></a><span data-ttu-id="b1e71-110">了解团队平台功能</span><span class="sxs-lookup"><span data-stu-id="b1e71-110">Get to know Teams platform capabilities</span></span>

<span data-ttu-id="b1e71-111">\***集成方案**：独立应用程序、协作应用程序、SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="b1e71-111">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="b1e71-112">您的团队应用程序可以包括用户所需的功能，并且可能会在协作时预期的功能，但您可能不熟悉团队开发术语。</span><span class="sxs-lookup"><span data-stu-id="b1e71-112">Your Teams app can include features users want and might expect when collaborating, but you may be unfamiliar with Teams development terminology.</span></span>

|<span data-ttu-id="b1e71-113">常见应用程序功能</span><span class="sxs-lookup"><span data-stu-id="b1e71-113">Common app features</span></span>   |<span data-ttu-id="b1e71-114">团队平台功能</span><span class="sxs-lookup"><span data-stu-id="b1e71-114">Teams platform capabilities</span></span>   |
|----------|-----------|
|<span data-ttu-id="b1e71-115">嵌入的网页、主页或 web 视图</span><span class="sxs-lookup"><span data-stu-id="b1e71-115">Embedded webpage, homepage, or webview</span></span>  |[<span data-ttu-id="b1e71-116">选项卡</span><span class="sxs-lookup"><span data-stu-id="b1e71-116">Tabs</span></span>](../tabs/what-are-tabs.md)  |
|<span data-ttu-id="b1e71-117">共享快捷方式和扩展</span><span class="sxs-lookup"><span data-stu-id="b1e71-117">Share shortcuts and extensions</span></span>  |[<span data-ttu-id="b1e71-118">消息扩展</span><span class="sxs-lookup"><span data-stu-id="b1e71-118">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="b1e71-119">操作快捷方式和扩展</span><span class="sxs-lookup"><span data-stu-id="b1e71-119">Action shortcuts and extensions</span></span>  |[<span data-ttu-id="b1e71-120">消息扩展</span><span class="sxs-lookup"><span data-stu-id="b1e71-120">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="b1e71-121">Chatbots</span><span class="sxs-lookup"><span data-stu-id="b1e71-121">Chatbots</span></span>  |[<span data-ttu-id="b1e71-122">机器人</span><span class="sxs-lookup"><span data-stu-id="b1e71-122">Bots</span></span>](../bots/what-are-bots.md) |
|<span data-ttu-id="b1e71-123">频道通知</span><span class="sxs-lookup"><span data-stu-id="b1e71-123">Channel notifications</span></span>  |[<span data-ttu-id="b1e71-124">机器人</span><span class="sxs-lookup"><span data-stu-id="b1e71-124">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="b1e71-125">传入 webhook</span><span class="sxs-lookup"><span data-stu-id="b1e71-125">Incoming webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[<span data-ttu-id="b1e71-126">Office 365 连接器</span><span class="sxs-lookup"><span data-stu-id="b1e71-126">Office 365 Connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="b1e71-127">邮件外部服务</span><span class="sxs-lookup"><span data-stu-id="b1e71-127">Message external services</span></span>  |[<span data-ttu-id="b1e71-128">机器人</span><span class="sxs-lookup"><span data-stu-id="b1e71-128">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="b1e71-129">传出 webhook</span><span class="sxs-lookup"><span data-stu-id="b1e71-129">Outgoing webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="b1e71-130">模式</span><span class="sxs-lookup"><span data-stu-id="b1e71-130">Modals</span></span>  |[<span data-ttu-id="b1e71-131">任务模块</span><span class="sxs-lookup"><span data-stu-id="b1e71-131">Task modules</span></span>](../task-modules-and-cards/what-are-task-modules.md)  |
|<span data-ttu-id="b1e71-132">内容丰富的卡片</span><span class="sxs-lookup"><span data-stu-id="b1e71-132">Content-rich cards</span></span>  |[<span data-ttu-id="b1e71-133">自适应卡片</span><span class="sxs-lookup"><span data-stu-id="b1e71-133">Adaptive Cards</span></span>](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a><span data-ttu-id="b1e71-134">确定功能的子集</span><span class="sxs-lookup"><span data-stu-id="b1e71-134">Determine a subset of functionality</span></span>

<span data-ttu-id="b1e71-135">\***集成方案**：独立应用程序 \*</span><span class="sxs-lookup"><span data-stu-id="b1e71-135">\***Integration scenarios**: Standalone apps\*</span></span>

<span data-ttu-id="b1e71-136">将现有应用程序的所有功能集成到团队中通常会导致强制或 unnatural 的用户体验，尤其是在大型应用程序中。</span><span class="sxs-lookup"><span data-stu-id="b1e71-136">Integrating all features of an existing application into Teams often leads to a forced or unnatural user experience, particularly in larger apps.</span></span> <span data-ttu-id="b1e71-137">考虑从最 impactful 的功能开始，这些功能将更自然地与团队集成。</span><span class="sxs-lookup"><span data-stu-id="b1e71-137">Consider starting with the most impactful features and those that will integrate more naturally with Teams.</span></span> <span data-ttu-id="b1e71-138">请记住，始终允许用户启动主要应用程序，并访问其完整的功能集。</span><span class="sxs-lookup"><span data-stu-id="b1e71-138">Remember, you can always allow users to launch the main app and access its full set of features.</span></span>

<span data-ttu-id="b1e71-139">在开始任何技术工作之前，请为你的团队应用程序做一些规划：</span><span class="sxs-lookup"><span data-stu-id="b1e71-139">Before you begin any technical work, do some planning for your Teams app:</span></span>

1. <span data-ttu-id="b1e71-140">将[应用程序的用例映射到团队平台功能](../concepts/design/map-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="b1e71-140">[Map your app's use cases to Teams platform capabilities](../concepts/design/map-use-cases.md).</span></span>
1. <span data-ttu-id="b1e71-141">[确定您的应用程序的入口点](../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="b1e71-141">[Determine your app's entry points](../concepts/extensibility-points.md).</span></span> <span data-ttu-id="b1e71-142">是用于个人用途、协作还是同时使用这两者？</span><span class="sxs-lookup"><span data-stu-id="b1e71-142">Is it for personal use, collaboration, or both?</span></span>

## <a name="understand-sharepoint-requirements-and-options"></a><span data-ttu-id="b1e71-143">了解 SharePoint 要求和选项</span><span class="sxs-lookup"><span data-stu-id="b1e71-143">Understand SharePoint requirements and options</span></span>

<span data-ttu-id="b1e71-144">\***集成方案**： SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="b1e71-144">\***Integration scenarios**: SharePoint\*</span></span>

<span data-ttu-id="b1e71-145">您可以将现有 [SharePoint 页面](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) 集成为 "团队" 选项卡。请记住以下几点：</span><span class="sxs-lookup"><span data-stu-id="b1e71-145">You can integrate an existing [SharePoint page](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) as a Teams tab. Remember the following:</span></span>

* <span data-ttu-id="b1e71-146">它必须是 *新式* SharePoint Online 页面</span><span class="sxs-lookup"><span data-stu-id="b1e71-146">It must be a *modern* SharePoint Online page</span></span>
* <span data-ttu-id="b1e71-147">仅支持个人选项卡 (无法将您的页面集成为通道选项卡) </span><span class="sxs-lookup"><span data-stu-id="b1e71-147">Only personal tabs are supported (you can't integrate your page as a channel tab)</span></span>

<span data-ttu-id="b1e71-148">或者，您可以 [使用 SharePoint 框架](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction)生成 "团队" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="b1e71-148">Alternatively, you can build a Teams tab [using the SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction).</span></span>

## <a name="aim-towards-multi-tenancy"></a><span data-ttu-id="b1e71-149">朝着多租户为目的</span><span class="sxs-lookup"><span data-stu-id="b1e71-149">Aim towards multi-tenancy</span></span>

<span data-ttu-id="b1e71-150">\***集成方案**：独立应用程序、协作应用程序、SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="b1e71-150">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="b1e71-151">如果你的应用程序由多个组织使用，请考虑多租户托管，这将使你的产品可扩展并大大简化分发。</span><span class="sxs-lookup"><span data-stu-id="b1e71-151">If your app is used by multiple organizations, consider multi-tenant hosting that would make your product scalable and greatly simplify distribution.</span></span>

## <a name="review-your-apis"></a><span data-ttu-id="b1e71-152">查看你的 Api</span><span class="sxs-lookup"><span data-stu-id="b1e71-152">Review your APIs</span></span>

<span data-ttu-id="b1e71-153">\***集成方案**：独立应用程序、协作应用程序 \*</span><span class="sxs-lookup"><span data-stu-id="b1e71-153">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="b1e71-154">不要假设您的应用程序的现有 Api 和数据结构在与团队集成时完全支持该应用程序。</span><span class="sxs-lookup"><span data-stu-id="b1e71-154">Don't assume your app's existing APIs and data structures fully support the app when integrated with Teams.</span></span> <span data-ttu-id="b1e71-155">您可能需要扩充这些信息，其中包含有关 [标识映射](../concepts/authentication/configure-identity-provider.md)、 [深度链接支持](../concepts/build-and-test/deep-links.md)和 [包含 Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview)的团队的上下文信息。</span><span class="sxs-lookup"><span data-stu-id="b1e71-155">You might need to augment these with contextual information about Teams for [identity mapping](../concepts/authentication/configure-identity-provider.md), [deep-link support](../concepts/build-and-test/deep-links.md), and [incorporating Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="b1e71-156">了解有关获取 ["团队" 选项卡](../tabs/how-to/access-teams-context.md) 或 [bot](../bots/how-to/get-teams-context.md)的上下文的详细信息。</span><span class="sxs-lookup"><span data-stu-id="b1e71-156">Learn more about getting context for your Teams [tab](../tabs/how-to/access-teams-context.md) or [bot](../bots/how-to/get-teams-context.md).</span></span>

## <a name="understand-authentication-options"></a><span data-ttu-id="b1e71-157">了解身份验证选项</span><span class="sxs-lookup"><span data-stu-id="b1e71-157">Understand authentication options</span></span>

<span data-ttu-id="b1e71-158">\***集成方案**：独立应用程序、协作应用程序、SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="b1e71-158">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="b1e71-159">Azure Active Directory (AD) 是团队的标识提供者。</span><span class="sxs-lookup"><span data-stu-id="b1e71-159">Azure Active Directory (AD) is the identity provider for Teams.</span></span> <span data-ttu-id="b1e71-160">如果您的应用程序使用不同的标识提供程序，则必须执行 identity mapping 练习或与 Azure AD 联盟。</span><span class="sxs-lookup"><span data-stu-id="b1e71-160">If your app uses a different identity provider, you must either do an identity mapping exercise or federate with Azure AD.</span></span>

<span data-ttu-id="b1e71-161">团队具有单一登录 (SSO) 机制，其中包含适用于第三方应用程序的 Azure AD，以及使用诸如 OAuth 和 Open ID Connect (OIDC) 的其他标识提供程序进行身份验证流的指南。</span><span class="sxs-lookup"><span data-stu-id="b1e71-161">Teams has single sign-on (SSO) mechanisms with Azure AD for third-party apps and guidance for authentication flows to other identity providers using standards such as OAuth and Open ID Connect (OIDC).</span></span>

<span data-ttu-id="b1e71-162">对于 SharePoint 页面，如果您希望 SSO 在另一个应用程序中运行，则只能使用 SSO，并且无法添加其他 Azure AD ID，因为 ID 是 SharePoint 应用) 的 (。</span><span class="sxs-lookup"><span data-stu-id="b1e71-162">For SharePoint pages, you can only use SSO and can't add another Azure AD ID if you want SSO to work for another app (since the ID is the SharePoint app).</span></span>

<span data-ttu-id="b1e71-163">了解有关 [团队中的身份验证的](../concepts/authentication/authentication.md)详细信息。</span><span class="sxs-lookup"><span data-stu-id="b1e71-163">Learn more about [authentication in Teams](../concepts/authentication/authentication.md).</span></span>

## <a name="follow-teams-design-guidelines"></a><span data-ttu-id="b1e71-164">关注团队设计准则</span><span class="sxs-lookup"><span data-stu-id="b1e71-164">Follow Teams design guidelines</span></span>

<span data-ttu-id="b1e71-165">\***集成方案**：独立应用程序、协作应用程序 \*</span><span class="sxs-lookup"><span data-stu-id="b1e71-165">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="b1e71-166">通常情况下，您的应用程序应在团队中感觉自然。</span><span class="sxs-lookup"><span data-stu-id="b1e71-166">In general, your app should feel natural in Teams.</span></span> <span data-ttu-id="b1e71-167">您可能会认为将现有应用程序内容迁移到 "团队" 选项卡是足够的，但强烈建议您的应用遵循 [团队设计准则](../concepts/design/understand-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="b1e71-167">You might think migrating existing app content to a Teams tab is sufficient, but we strongly recommend your app follows [Teams design guidelines](../concepts/design/understand-use-cases.md).</span></span> <span data-ttu-id="b1e71-168">另请参阅： [熟知设计系统](https://fluentsite.z22.web.core.windows.net/)。</span><span class="sxs-lookup"><span data-stu-id="b1e71-168">See also: [Fluent Design System](https://fluentsite.z22.web.core.windows.net/).</span></span>

## <a name="maximize-deep-linking"></a><span data-ttu-id="b1e71-169">最大化深度链接</span><span class="sxs-lookup"><span data-stu-id="b1e71-169">Maximize deep linking</span></span>

<span data-ttu-id="b1e71-170">\***集成方案**：独立应用程序、协作应用程序、SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="b1e71-170">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="b1e71-171">团队中的几乎所有内容都可以直接链接到 [深层链接](../concepts/build-and-test/deep-links.md)。</span><span class="sxs-lookup"><span data-stu-id="b1e71-171">Almost everything in Teams can be linked to directly with a [deep link](../concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="b1e71-172">您的应用程序应最大限度地利用这些内容，包括与特定邮件和选项卡内容的链接。</span><span class="sxs-lookup"><span data-stu-id="b1e71-172">Your app should maximize use of these, including linking to and from specific messages and tab content.</span></span> <span data-ttu-id="b1e71-173">Deep links 可以真正将应用程序的多个部分结合在一起，以实现更多的本机团队体验。</span><span class="sxs-lookup"><span data-stu-id="b1e71-173">Deep links can really tie together multiple pieces of an app for a more native Teams experience.</span></span>

## <a name="be-smart-when-messaging-users"></a><span data-ttu-id="b1e71-174">在邮件用户进行智能化时进行智能化</span><span class="sxs-lookup"><span data-stu-id="b1e71-174">Be smart when messaging users</span></span>

<span data-ttu-id="b1e71-175">\***集成方案**：独立应用程序、协作应用程序、SharePoint \*</span><span class="sxs-lookup"><span data-stu-id="b1e71-175">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="b1e71-176">考虑团队应用程序现在可以发送的消息类型以及长期。</span><span class="sxs-lookup"><span data-stu-id="b1e71-176">Consider the types of messages your Teams app might send now and in the long term.</span></span> <span data-ttu-id="b1e71-177">如果您认为您的应用程序将有多线程对话，则 [bot](../bots/what-are-bots.md) 可能会比 [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)提供更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="b1e71-177">If you think your app will ever have a multi-threaded conversation, a [bot](../bots/what-are-bots.md) might offer more flexibility than a [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

<span data-ttu-id="b1e71-178">您还可以通过 bot 向单个用户或频道发送 *主动消息* 。</span><span class="sxs-lookup"><span data-stu-id="b1e71-178">Bots also allow you to send *proactive messages* to individual users or channels.</span></span> <span data-ttu-id="b1e71-179">这些是由外部事件触发的自发邮件，而不是发送到 bot 的邮件。</span><span class="sxs-lookup"><span data-stu-id="b1e71-179">These are unprompted messages triggered by an outside event and not a message sent to a bot.</span></span> <span data-ttu-id="b1e71-180"> (例如，你的 bot 可以在安装时发送欢迎消息，或者新用户加入频道。 ) </span><span class="sxs-lookup"><span data-stu-id="b1e71-180">(For example, your bot can send a welcome message when it's installed or a new user joins a channel.)</span></span> 

<span data-ttu-id="b1e71-181">发送前瞻性邮件需要特定于团队的标识符-您可以通过 [提取名单或用户配置文件数据](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile)、 [订阅会话事件](../bots/how-to/conversations/subscribe-to-conversation-events.md)或使用 [Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging)来捕获此信息。</span><span class="sxs-lookup"><span data-stu-id="b1e71-181">Sending proactive messages requires Teams-specific identifiers—you can capture this information by [fetching roster or user profile data](../bots/how-to/get-teams-context.md#fetching-the-roster-or-user-profile), [subscribing to conversation events](../bots/how-to/conversations/subscribe-to-conversation-events.md), or using [Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging).</span></span>

<span data-ttu-id="b1e71-182">注意不到邮件过多的垃圾邮件用户。</span><span class="sxs-lookup"><span data-stu-id="b1e71-182">Be careful not to spam users with excessive messages.</span></span> <span data-ttu-id="b1e71-183">如果团队功能支持，请考虑让用户为您的应用程序配置通知设置 (例如，"不向我发送自发消息。") 。</span><span class="sxs-lookup"><span data-stu-id="b1e71-183">If the Teams capability supports it, consider letting users configure notification settings for your app (for example, "Don't send me unprompted messages.").</span></span>

## <a name="use-sharepoint-for-file-and-data-storage"></a><span data-ttu-id="b1e71-184">将 SharePoint 用于文件和数据存储</span><span class="sxs-lookup"><span data-stu-id="b1e71-184">Use SharePoint for file and data storage</span></span>

<span data-ttu-id="b1e71-185">***集成方案：** 独立应用程序、协作应用程序、SharePoint 页面*</span><span class="sxs-lookup"><span data-stu-id="b1e71-185">***Integration scenarios:** Standalone apps, collaboration apps, SharePoint pages*</span></span>

<span data-ttu-id="b1e71-186">创建团队时，也会将 [SharePoint 网站集](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) 配置为支持该团队的文件和数据存储。</span><span class="sxs-lookup"><span data-stu-id="b1e71-186">When a team is created, a [SharePoint site collection](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) is also provisioned to support file and data storage for that team.</span></span> <span data-ttu-id="b1e71-187">如果您的应用程序与文件交互，则可以并应使用此功能。</span><span class="sxs-lookup"><span data-stu-id="b1e71-187">Your app can and should leverage this feature if it interacts with files.</span></span> <span data-ttu-id="b1e71-188">您还可以使用网站集将原始数据存储在 SharePoint 列表和 Excel 中。</span><span class="sxs-lookup"><span data-stu-id="b1e71-188">You can also use the site collection to store raw data in SharePoint Lists and Excel.</span></span>
