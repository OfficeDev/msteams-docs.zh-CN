---
author: heath-hamilton
description: 将现有 Web 应用与 Microsoft Teams 集成的最佳方案
ms.author: v-heha
ms.date: 08/26/2020
ms.topic: conceptual
title: 将 Web 应用与 Microsoft Teams 集成
ms.openlocfilehash: 4671d2277d5eb7c035421c51b1714eccaac06a31
ms.sourcegitcommit: 79e6bccfb513d4c16a58ffc03521edcf134fa518
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/13/2021
ms.locfileid: "51696484"
---
# <a name="integrate-web-apps-with-teams"></a><span data-ttu-id="7eb7c-103">将 Web 应用与 Teams 集成</span><span class="sxs-lookup"><span data-stu-id="7eb7c-103">Integrate web apps with Teams</span></span>

<span data-ttu-id="7eb7c-104">你是否具有你认为适合 Teams 社交和协作功能的 Web 应用？</span><span class="sxs-lookup"><span data-stu-id="7eb7c-104">Do you have a web app you think would fit naturally with Teams' social and collaborative features?</span></span> <span data-ttu-id="7eb7c-105">这些指南可帮助你了解如何集成以下类型的应用：</span><span class="sxs-lookup"><span data-stu-id="7eb7c-105">These guidelines can help you understand how to integrate the following types of apps:</span></span>

* <span data-ttu-id="7eb7c-106">**独立应用**：可以是单页应用或希望用户使用 Teams 中某些方面的大型复杂应用。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-106">**Standalone apps**: Could be a single-page app or large, complex app you want people to use some aspects of in Teams.</span></span>
* <span data-ttu-id="7eb7c-107">**协作应用**：为 Teams 固有的社交和协作功能构建的应用。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-107">**Collaboration apps**: An app already built for the social and collaborative features inherent to Teams.</span></span>
* <span data-ttu-id="7eb7c-108">**SharePoint：** 想要在 Teams 中显示 SharePoint 页面。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-108">**SharePoint**: A SharePoint page you want to surface in Teams.</span></span>

<span data-ttu-id="7eb7c-109">对于每个指南，你可以查看它是否适用于你的集成方案。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-109">For each guideline, you can see if it's applicable to your integration scenario.</span></span>

## <a name="get-to-know-teams-platform-capabilities"></a><span data-ttu-id="7eb7c-110">了解 Teams 平台功能</span><span class="sxs-lookup"><span data-stu-id="7eb7c-110">Get to know Teams platform capabilities</span></span>

<span data-ttu-id="7eb7c-111">***集成方案：** 独立应用程序、协作应用程序、SharePoint*</span><span class="sxs-lookup"><span data-stu-id="7eb7c-111">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="7eb7c-112">Teams 应用可以包含用户在协作时需要和可能期望的功能，但你可能不熟悉 Teams 开发术语。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-112">Your Teams app can include features users want and might expect when collaborating, but you may be unfamiliar with Teams development terminology.</span></span>

|<span data-ttu-id="7eb7c-113">常见应用功能</span><span class="sxs-lookup"><span data-stu-id="7eb7c-113">Common app features</span></span>   |<span data-ttu-id="7eb7c-114">Teams 平台功能</span><span class="sxs-lookup"><span data-stu-id="7eb7c-114">Teams platform capabilities</span></span>   |
|----------|-----------|
|<span data-ttu-id="7eb7c-115">嵌入式网页、主页或 Webview</span><span class="sxs-lookup"><span data-stu-id="7eb7c-115">Embedded webpage, homepage, or webview</span></span>  |[<span data-ttu-id="7eb7c-116">选项卡</span><span class="sxs-lookup"><span data-stu-id="7eb7c-116">Tabs</span></span>](../tabs/what-are-tabs.md)  |
|<span data-ttu-id="7eb7c-117">共享快捷方式和扩展</span><span class="sxs-lookup"><span data-stu-id="7eb7c-117">Share shortcuts and extensions</span></span>  |[<span data-ttu-id="7eb7c-118">消息扩展</span><span class="sxs-lookup"><span data-stu-id="7eb7c-118">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="7eb7c-119">操作快捷方式和扩展</span><span class="sxs-lookup"><span data-stu-id="7eb7c-119">Action shortcuts and extensions</span></span>  |[<span data-ttu-id="7eb7c-120">消息扩展</span><span class="sxs-lookup"><span data-stu-id="7eb7c-120">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="7eb7c-121">Chatbots</span><span class="sxs-lookup"><span data-stu-id="7eb7c-121">Chatbots</span></span>  |[<span data-ttu-id="7eb7c-122">机器人</span><span class="sxs-lookup"><span data-stu-id="7eb7c-122">Bots</span></span>](../bots/what-are-bots.md) |
|<span data-ttu-id="7eb7c-123">频道通知</span><span class="sxs-lookup"><span data-stu-id="7eb7c-123">Channel notifications</span></span>  |[<span data-ttu-id="7eb7c-124">机器人</span><span class="sxs-lookup"><span data-stu-id="7eb7c-124">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="7eb7c-125">传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="7eb7c-125">Incoming webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[<span data-ttu-id="7eb7c-126">Office 365 连接器</span><span class="sxs-lookup"><span data-stu-id="7eb7c-126">Office 365 Connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="7eb7c-127">邮件外部服务</span><span class="sxs-lookup"><span data-stu-id="7eb7c-127">Message external services</span></span>  |[<span data-ttu-id="7eb7c-128">机器人</span><span class="sxs-lookup"><span data-stu-id="7eb7c-128">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="7eb7c-129">传出 webhook</span><span class="sxs-lookup"><span data-stu-id="7eb7c-129">Outgoing webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="7eb7c-130">Modals</span><span class="sxs-lookup"><span data-stu-id="7eb7c-130">Modals</span></span>  |[<span data-ttu-id="7eb7c-131">任务模块</span><span class="sxs-lookup"><span data-stu-id="7eb7c-131">Task modules</span></span>](../task-modules-and-cards/what-are-task-modules.md)  |
|<span data-ttu-id="7eb7c-132">内容丰富的卡片</span><span class="sxs-lookup"><span data-stu-id="7eb7c-132">Content-rich cards</span></span>  |[<span data-ttu-id="7eb7c-133">自适应卡</span><span class="sxs-lookup"><span data-stu-id="7eb7c-133">Adaptive Cards</span></span>](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a><span data-ttu-id="7eb7c-134">确定功能的子集</span><span class="sxs-lookup"><span data-stu-id="7eb7c-134">Determine a subset of functionality</span></span>

<span data-ttu-id="7eb7c-135">\***集成方案**：独立应用\*</span><span class="sxs-lookup"><span data-stu-id="7eb7c-135">\***Integration scenarios**: Standalone apps\*</span></span>

<span data-ttu-id="7eb7c-136">将现有应用程序的所有功能集成到 Teams 中通常会导致强制的或不自然的用户体验，尤其是在大型应用中。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-136">Integrating all features of an existing application into Teams often leads to a forced or unnatural user experience, particularly in larger apps.</span></span> <span data-ttu-id="7eb7c-137">请考虑从影响最大的功能和与 Teams 更自然地集成的功能开始。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-137">Consider starting with the most impactful features and those that will integrate more naturally with Teams.</span></span> <span data-ttu-id="7eb7c-138">请记住，你始终可以允许用户启动主应用并访问其完整功能集。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-138">Remember, you can always allow users to launch the main app and access its full set of features.</span></span>

<span data-ttu-id="7eb7c-139">在开始任何技术工作之前，请对 Teams 应用进行一些规划：</span><span class="sxs-lookup"><span data-stu-id="7eb7c-139">Before you begin any technical work, do some planning for your Teams app:</span></span>

1. <span data-ttu-id="7eb7c-140">[将应用的用例映射到 Teams 平台功能](../concepts/design/map-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-140">[Map your app's use cases to Teams platform capabilities](../concepts/design/map-use-cases.md).</span></span>
1. <span data-ttu-id="7eb7c-141">[确定应用的入口点](../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-141">[Determine your app's entry points](../concepts/extensibility-points.md).</span></span> <span data-ttu-id="7eb7c-142">它是用于个人用途、协作还是同时用于两者？</span><span class="sxs-lookup"><span data-stu-id="7eb7c-142">Is it for personal use, collaboration, or both?</span></span>

## <a name="understand-sharepoint-requirements-and-options"></a><span data-ttu-id="7eb7c-143">了解 SharePoint 要求和选项</span><span class="sxs-lookup"><span data-stu-id="7eb7c-143">Understand SharePoint requirements and options</span></span>

<span data-ttu-id="7eb7c-144">\***集成方案**： SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="7eb7c-144">\***Integration scenarios**: SharePoint\*</span></span>

<span data-ttu-id="7eb7c-145">可以将现有 [SharePoint 页面集成为](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) Teams 选项卡。请记住以下事项：</span><span class="sxs-lookup"><span data-stu-id="7eb7c-145">You can integrate an existing [SharePoint page](https://docs.microsoft.com/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) as a Teams tab. Remember the following:</span></span>

* <span data-ttu-id="7eb7c-146">它必须 *是新式* SharePoint Online 页面</span><span class="sxs-lookup"><span data-stu-id="7eb7c-146">It must be a *modern* SharePoint Online page</span></span>
* <span data-ttu-id="7eb7c-147">只有个人选项卡 (无法将页面集成为频道选项卡) </span><span class="sxs-lookup"><span data-stu-id="7eb7c-147">Only personal tabs are supported (you can't integrate your page as a channel tab)</span></span>

<span data-ttu-id="7eb7c-148">或者，可以使用 [SharePoint](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction)框架生成 Teams 选项卡。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-148">Alternatively, you can build a Teams tab [using the SharePoint Framework](https://docs.microsoft.com/sharepoint/dev/spfx/integrate-with-teams-introduction).</span></span>

## <a name="aim-towards-multi-tenancy"></a><span data-ttu-id="7eb7c-149">旨在实现多租户</span><span class="sxs-lookup"><span data-stu-id="7eb7c-149">Aim towards multi-tenancy</span></span>

<span data-ttu-id="7eb7c-150">***集成方案：** 独立应用程序、协作应用程序、SharePoint*</span><span class="sxs-lookup"><span data-stu-id="7eb7c-150">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="7eb7c-151">如果你的应用由多个组织使用，请考虑多租户托管，这将提高产品可扩展性并极大地简化分发。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-151">If your app is used by multiple organizations, consider multi-tenant hosting that would make your product scalable and greatly simplify distribution.</span></span>

## <a name="review-your-apis"></a><span data-ttu-id="7eb7c-152">查看 API</span><span class="sxs-lookup"><span data-stu-id="7eb7c-152">Review your APIs</span></span>

<span data-ttu-id="7eb7c-153">\***集成方案**：独立应用、协作应用\*</span><span class="sxs-lookup"><span data-stu-id="7eb7c-153">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="7eb7c-154">与 Teams 集成时，请勿假定应用的现有 API 和数据结构完全支持该应用。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-154">Don't assume your app's existing APIs and data structures fully support the app when integrated with Teams.</span></span> <span data-ttu-id="7eb7c-155">你可能需要使用有关 Teams 的上下文信息来扩充[](../concepts/authentication/configure-identity-provider.md)这些信息，以用于标识映射、[深层链接支持](../concepts/build-and-test/deep-links.md)以及合并[Microsoft Graph。](https://docs.microsoft.com/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="7eb7c-155">You might need to augment these with contextual information about Teams for [identity mapping](../concepts/authentication/configure-identity-provider.md), [deep-link support](../concepts/build-and-test/deep-links.md), and [incorporating Microsoft Graph](https://docs.microsoft.com/graph/teams-concept-overview).</span></span>

<span data-ttu-id="7eb7c-156">详细了解如何获取 Teams 选项卡或[自动程序](../tabs/how-to/access-teams-context.md)[的上下文](../bots/how-to/get-teams-context.md)。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-156">Learn more about getting context for your Teams [tab](../tabs/how-to/access-teams-context.md) or [bot](../bots/how-to/get-teams-context.md).</span></span>

## <a name="understand-authentication-options"></a><span data-ttu-id="7eb7c-157">了解身份验证选项</span><span class="sxs-lookup"><span data-stu-id="7eb7c-157">Understand authentication options</span></span>

<span data-ttu-id="7eb7c-158">***集成方案：** 独立应用程序、协作应用程序、SharePoint*</span><span class="sxs-lookup"><span data-stu-id="7eb7c-158">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="7eb7c-159">Azure Active Directory (AD) 是 Teams 的标识提供程序。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-159">Azure Active Directory (AD) is the identity provider for Teams.</span></span> <span data-ttu-id="7eb7c-160">如果你的应用使用不同的标识提供程序，你必须执行标识映射练习或与 Azure AD 联合。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-160">If your app uses a different identity provider, you must either do an identity mapping exercise or federate with Azure AD.</span></span>

<span data-ttu-id="7eb7c-161">Teams 具有适用于第三方应用的 Azure AD 的单一登录 (SSO) 机制，以及使用 OAuth 和开放 ID Connect (OIDC) 等标准将身份验证流到其他标识提供商的指南。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-161">Teams has single sign-on (SSO) mechanisms with Azure AD for third-party apps and guidance for authentication flows to other identity providers using standards such as OAuth and Open ID Connect (OIDC).</span></span>

<span data-ttu-id="7eb7c-162">对于 SharePoint 页面，如果你希望 SSO 适用于另一个应用程序页面，则只能使用 SSO，并且不能添加其他 Azure AD ID (因为 ID 是 SharePoint 应用程序) 。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-162">For SharePoint pages, you can only use SSO and can't add another Azure AD ID if you want SSO to work for another app (since the ID is the SharePoint app).</span></span>

<span data-ttu-id="7eb7c-163">详细了解 Teams [中的身份验证](../concepts/authentication/authentication.md)。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-163">Learn more about [authentication in Teams](../concepts/authentication/authentication.md).</span></span>

## <a name="follow-teams-design-guidelines"></a><span data-ttu-id="7eb7c-164">遵循 Teams 设计指南</span><span class="sxs-lookup"><span data-stu-id="7eb7c-164">Follow Teams design guidelines</span></span>

<span data-ttu-id="7eb7c-165">\***集成方案**：独立应用、协作应用\*</span><span class="sxs-lookup"><span data-stu-id="7eb7c-165">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="7eb7c-166">通常，你的应用在 Teams 中应该感觉自然。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-166">In general, your app should feel natural in Teams.</span></span> <span data-ttu-id="7eb7c-167">你可能认为将现有应用内容迁移到 Teams 选项卡就足够了，但我们强烈建议你的应用遵循 [Teams 设计指南](../concepts/design/understand-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-167">You might think migrating existing app content to a Teams tab is sufficient, but we strongly recommend your app follows [Teams design guidelines](../concepts/design/understand-use-cases.md).</span></span> <span data-ttu-id="7eb7c-168">另请参阅 [：Fluent Design System](https://fluentsite.z22.web.core.windows.net/)。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-168">See also: [Fluent Design System](https://fluentsite.z22.web.core.windows.net/).</span></span>

## <a name="maximize-deep-linking"></a><span data-ttu-id="7eb7c-169">最大化深层链接</span><span class="sxs-lookup"><span data-stu-id="7eb7c-169">Maximize deep linking</span></span>

<span data-ttu-id="7eb7c-170">***集成方案：** 独立应用程序、协作应用程序、SharePoint*</span><span class="sxs-lookup"><span data-stu-id="7eb7c-170">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="7eb7c-171">Teams 中几乎所有内容都可以直接链接到深层 [链接](../concepts/build-and-test/deep-links.md)。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-171">Almost everything in Teams can be linked to directly with a [deep link](../concepts/build-and-test/deep-links.md).</span></span> <span data-ttu-id="7eb7c-172">你的应用应最大限度地利用这些信息，包括链接到特定消息和选项卡内容以及从这些邮件和选项卡内容进行链接。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-172">Your app should maximize use of these, including linking to and from specific messages and tab content.</span></span> <span data-ttu-id="7eb7c-173">深度链接可以真正将应用的多个部分连接在一起，以获得更本机的 Teams 体验。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-173">Deep links can really tie together multiple pieces of an app for a more native Teams experience.</span></span>

## <a name="be-smart-when-messaging-users"></a><span data-ttu-id="7eb7c-174">在消息传递用户时要智能</span><span class="sxs-lookup"><span data-stu-id="7eb7c-174">Be smart when messaging users</span></span>

<span data-ttu-id="7eb7c-175">***集成方案：** 独立应用程序、协作应用程序、SharePoint*</span><span class="sxs-lookup"><span data-stu-id="7eb7c-175">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="7eb7c-176">考虑 Teams 应用现在和长期可能发送的消息类型。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-176">Consider the types of messages your Teams app might send now and in the long term.</span></span> <span data-ttu-id="7eb7c-177">如果你认为你的应用将拥有多线程对话，机器人可能会提供比[webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)更大的灵活性。 [](../bots/what-are-bots.md)</span><span class="sxs-lookup"><span data-stu-id="7eb7c-177">If you think your app will ever have a multi-threaded conversation, a [bot](../bots/what-are-bots.md) might offer more flexibility than a [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

<span data-ttu-id="7eb7c-178">自动程序还允许你向单个 *用户* 或频道发送主动消息。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-178">Bots also allow you to send *proactive messages* to individual users or channels.</span></span> <span data-ttu-id="7eb7c-179">这些是外部事件触发的未经提示的消息，而不是发送给自动程序的消息。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-179">These are unprompted messages triggered by an outside event and not a message sent to a bot.</span></span> <span data-ttu-id="7eb7c-180"> (例如，自动程序可以在安装后或新用户加入频道时发送欢迎消息) </span><span class="sxs-lookup"><span data-stu-id="7eb7c-180">(For example, your bot can send a welcome message when it's installed or a new user joins a channel.)</span></span>

<span data-ttu-id="7eb7c-181">发送主动邮件需要特定于 Teams 的标识符 ，可以通过提取名单或[](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)用户配置文件数据、订阅对话事件，或者[](../bots/how-to/conversations/subscribe-to-conversation-events.md)使用 Microsoft Graph 来[捕获此信息](https://docs.microsoft.com/graph/teams-proactive-messaging)。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-181">Sending proactive messages requires Teams-specific identifiers—you can capture this information by [fetching roster or user profile data](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile), [subscribing to conversation events](../bots/how-to/conversations/subscribe-to-conversation-events.md), or using [Microsoft Graph](https://docs.microsoft.com/graph/teams-proactive-messaging).</span></span>

<span data-ttu-id="7eb7c-182">请注意不要向邮件过多的用户发送过多邮件。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-182">Be careful not to spam users with excessive messages.</span></span> <span data-ttu-id="7eb7c-183">如果 Teams 功能支持此功能，请考虑让用户为你的应用配置通知设置 (例如，"不要向我发送不拒绝的消息"。) 。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-183">If the Teams capability supports it, consider letting users configure notification settings for your app (for example, "Don't send me unprompted messages.").</span></span>

## <a name="use-sharepoint-for-file-and-data-storage"></a><span data-ttu-id="7eb7c-184">将 SharePoint 用于文件和数据存储</span><span class="sxs-lookup"><span data-stu-id="7eb7c-184">Use SharePoint for file and data storage</span></span>

<span data-ttu-id="7eb7c-185">***集成方案：** 独立应用程序、协作应用程序、SharePoint 页面*</span><span class="sxs-lookup"><span data-stu-id="7eb7c-185">***Integration scenarios:** Standalone apps, collaboration apps, SharePoint pages*</span></span>

<span data-ttu-id="7eb7c-186">创建团队时，还会设置 [SharePoint](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) 网站集以支持该团队的文件和数据存储。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-186">When a team is created, a [SharePoint site collection](https://docs.microsoft.com/microsoftteams/sharepoint-onedrive-interact) is also provisioned to support file and data storage for that team.</span></span> <span data-ttu-id="7eb7c-187">如果应用与文件交互，应用可以并且应该利用此功能。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-187">Your app can and should leverage this feature if it interacts with files.</span></span> <span data-ttu-id="7eb7c-188">您还可以使用网站集在 SharePoint 列表和 Excel 中存储原始数据。</span><span class="sxs-lookup"><span data-stu-id="7eb7c-188">You can also use the site collection to store raw data in SharePoint Lists and Excel.</span></span>
