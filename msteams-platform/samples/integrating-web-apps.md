---
author: heath-hamilton
description: 将现有 Web 应用与应用程序集成的最佳Microsoft Teams
ms.author: v-heha
ms.date: 08/26/2020
localization_priority: Normal
ms.topic: conceptual
title: Web 应用
ms.openlocfilehash: b7f530198a8e1c240e3cf4b227d786af94f6c89e
ms.sourcegitcommit: e1fe46c574cec378319814f8213209ad3063b2c3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 05/24/2021
ms.locfileid: "52630430"
---
# <a name="web-apps"></a><span data-ttu-id="66102-103">Web 应用</span><span class="sxs-lookup"><span data-stu-id="66102-103">Web apps</span></span> 

<span data-ttu-id="66102-104">通过将 Web 应用与 Teams集成，你可以使 Web 应用适合其社交和协作Teams。</span><span class="sxs-lookup"><span data-stu-id="66102-104">You can make web apps suitable with Teams' social and collaborative features, by properly integrating them with Teams.</span></span>
  
<span data-ttu-id="66102-105">你可以与应用程序集成的不同应用Teams如下所示：</span><span class="sxs-lookup"><span data-stu-id="66102-105">The different types of apps which you can integrate with Teams are as follows:</span></span>
* <span data-ttu-id="66102-106">**独立应用**：独立应用是单页应用或大型复杂应用。</span><span class="sxs-lookup"><span data-stu-id="66102-106">**Standalone apps**: A stand alone app is a single-page or large, and complex app.</span></span> <span data-ttu-id="66102-107">用户可以在应用程序内使用它的某些Teams。</span><span class="sxs-lookup"><span data-stu-id="66102-107">The user can use some aspects of it in Teams.</span></span>
* <span data-ttu-id="66102-108">**协作应用**：已针对组织本身固有的社交和协作功能Teams。</span><span class="sxs-lookup"><span data-stu-id="66102-108">**Collaboration apps**: An app already built for the social and collaborative features inherent to Teams.</span></span>
* <span data-ttu-id="66102-109">**SharePoint：SharePoint** 中显示的页面Teams。</span><span class="sxs-lookup"><span data-stu-id="66102-109">**SharePoint**: A SharePoint page you want to surface in Teams.</span></span>

<span data-ttu-id="66102-110">你可以映射并按照适用于集成方案的适当准则执行。</span><span class="sxs-lookup"><span data-stu-id="66102-110">You can map and follow the appropriate guideline applicable to your integration scenario.</span></span>
<span data-ttu-id="66102-111">本文档概述了Teams功能、文件和数据存储的共享点要求、API 要求、身份验证以及应用与 Teams 的深层链接。</span><span class="sxs-lookup"><span data-stu-id="66102-111">This document gives an overview of Teams capabilities, share-point requirements for file and data storage, API requirements, authentication, and deep-linking of your app with Teams.</span></span>
 
## <a name="get-to-know-teams-platform-capabilities"></a><span data-ttu-id="66102-112">了解Teams功能</span><span class="sxs-lookup"><span data-stu-id="66102-112">Get to know Teams platform capabilities</span></span>

<span data-ttu-id="66102-113">\***集成方案**：独立应用、协作应用SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="66102-113">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="66102-114">你的Teams应用必须包含必需和预期的协作功能。</span><span class="sxs-lookup"><span data-stu-id="66102-114">Your Teams app must include required and expected collaborative features.</span></span> <span data-ttu-id="66102-115">若要使用应用集成，必须熟悉Teams术语。</span><span class="sxs-lookup"><span data-stu-id="66102-115">To work with app integration, it is important to familiarize with Teams development terminology.</span></span>

|<span data-ttu-id="66102-116">常见应用功能</span><span class="sxs-lookup"><span data-stu-id="66102-116">Common app features</span></span>   |<span data-ttu-id="66102-117">Teams平台功能</span><span class="sxs-lookup"><span data-stu-id="66102-117">Teams platform capabilities</span></span>   |
|----------|-----------|
|<span data-ttu-id="66102-118">嵌入式网页、主页或 Webview</span><span class="sxs-lookup"><span data-stu-id="66102-118">Embedded webpage, homepage, or webview</span></span>  |[<span data-ttu-id="66102-119">选项卡</span><span class="sxs-lookup"><span data-stu-id="66102-119">Tabs</span></span>](../tabs/what-are-tabs.md)  |
|<span data-ttu-id="66102-120">共享快捷方式和扩展</span><span class="sxs-lookup"><span data-stu-id="66102-120">Share shortcuts and extensions</span></span>  |[<span data-ttu-id="66102-121">消息扩展</span><span class="sxs-lookup"><span data-stu-id="66102-121">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="66102-122">操作快捷方式和扩展</span><span class="sxs-lookup"><span data-stu-id="66102-122">Action shortcuts and extensions</span></span>  |[<span data-ttu-id="66102-123">消息扩展</span><span class="sxs-lookup"><span data-stu-id="66102-123">Messaging extensions</span></span>](../messaging-extensions/what-are-messaging-extensions.md)  |
|<span data-ttu-id="66102-124">Chatbots</span><span class="sxs-lookup"><span data-stu-id="66102-124">Chatbots</span></span>  |[<span data-ttu-id="66102-125">机器人</span><span class="sxs-lookup"><span data-stu-id="66102-125">Bots</span></span>](../bots/what-are-bots.md) |
|<span data-ttu-id="66102-126">频道通知</span><span class="sxs-lookup"><span data-stu-id="66102-126">Channel notifications</span></span>  |[<span data-ttu-id="66102-127">机器人</span><span class="sxs-lookup"><span data-stu-id="66102-127">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="66102-128">传入 Webhook</span><span class="sxs-lookup"><span data-stu-id="66102-128">Incoming webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)<br/>[<span data-ttu-id="66102-129">Office 365 连接器</span><span class="sxs-lookup"><span data-stu-id="66102-129">Office 365 Connectors</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="66102-130">邮件外部服务</span><span class="sxs-lookup"><span data-stu-id="66102-130">Message external services</span></span>  |[<span data-ttu-id="66102-131">机器人</span><span class="sxs-lookup"><span data-stu-id="66102-131">Bots</span></span>](../bots/what-are-bots.md)<br/>[<span data-ttu-id="66102-132">传出 webhook</span><span class="sxs-lookup"><span data-stu-id="66102-132">Outgoing webhooks</span></span>](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)  |
|<span data-ttu-id="66102-133">Modals</span><span class="sxs-lookup"><span data-stu-id="66102-133">Modals</span></span>  |[<span data-ttu-id="66102-134">任务模块</span><span class="sxs-lookup"><span data-stu-id="66102-134">Task modules</span></span>](../task-modules-and-cards/what-are-task-modules.md)  |
|<span data-ttu-id="66102-135">内容丰富的卡片</span><span class="sxs-lookup"><span data-stu-id="66102-135">Content-rich cards</span></span>  |[<span data-ttu-id="66102-136">自适应卡</span><span class="sxs-lookup"><span data-stu-id="66102-136">Adaptive Cards</span></span>](../task-modules-and-cards/what-are-cards.md)  |

## <a name="determine-a-subset-of-functionality"></a><span data-ttu-id="66102-137">确定功能的子集</span><span class="sxs-lookup"><span data-stu-id="66102-137">Determine a subset of functionality</span></span>

<span data-ttu-id="66102-138">\***集成方案**：独立应用\*</span><span class="sxs-lookup"><span data-stu-id="66102-138">\***Integration scenarios**: Standalone apps\*</span></span>

<span data-ttu-id="66102-139">将现有应用程序的所有功能集成到Teams通常会导致强制的或不自然的用户体验，尤其是在较大的应用中。</span><span class="sxs-lookup"><span data-stu-id="66102-139">Integrating all features of an existing application into Teams often leads to a forced or unnatural user experience, particularly in larger apps.</span></span> <span data-ttu-id="66102-140">从影响最大的功能开始，以及那些与项目更自然地Teams。</span><span class="sxs-lookup"><span data-stu-id="66102-140">Start with the most impactful features and those that integrates more naturally with Teams.</span></span> <span data-ttu-id="66102-141">你可以允许用户启动主应用并访问其完整功能集。</span><span class="sxs-lookup"><span data-stu-id="66102-141">You can allow users to launch the main app and access its full set of features.</span></span>

<span data-ttu-id="66102-142">**将应用与应用集成的先决条件Teams** 以下是将应用与应用集成Teams。</span><span class="sxs-lookup"><span data-stu-id="66102-142">**Prerequisites to integrate your app with Teams** Following are the prerequisites to integrate your app with Teams.</span></span> 

1. <span data-ttu-id="66102-143">[将应用的用例映射到Teams功能](../concepts/design/map-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="66102-143">[Map your app's use cases to Teams platform capabilities](../concepts/design/map-use-cases.md).</span></span>
1. <span data-ttu-id="66102-144">[确定应用的入口点](../concepts/extensibility-points.md)。</span><span class="sxs-lookup"><span data-stu-id="66102-144">[Determine your app's entry points](../concepts/extensibility-points.md).</span></span> <span data-ttu-id="66102-145">它是用于个人用途、协作还是同时用于两者？</span><span class="sxs-lookup"><span data-stu-id="66102-145">Is it for personal use, collaboration, or both?</span></span>

## <a name="understand-sharepoint-requirements-and-options"></a><span data-ttu-id="66102-146">了解SharePoint要求和选项</span><span class="sxs-lookup"><span data-stu-id="66102-146">Understand SharePoint requirements and options</span></span>

<span data-ttu-id="66102-147">\***集成方案**： SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="66102-147">\***Integration scenarios**: SharePoint\*</span></span>

<span data-ttu-id="66102-148">若要将现有[SharePoint页](/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites)作为"Teams"选项卡集成，必须考虑以下事项：</span><span class="sxs-lookup"><span data-stu-id="66102-148">To integrate an existing [SharePoint page](/MicrosoftTeams/teams-standalone-static-tabs-using-spo-sites) as a Teams tab, you must consider the following:</span></span>

* <span data-ttu-id="66102-149">它必须是新式 *联机* SharePoint页面。</span><span class="sxs-lookup"><span data-stu-id="66102-149">It must be a *modern* SharePoint online page.</span></span>
* <span data-ttu-id="66102-150">仅支持个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="66102-150">Only personal tabs are supported.</span></span> <span data-ttu-id="66102-151">无法将页面作为通道选项卡进行集成。</span><span class="sxs-lookup"><span data-stu-id="66102-151">You cannot integrate your page as a channel tab.</span></span>

<span data-ttu-id="66102-152">或者，您也可以使用 Teams[生成一个SharePoint 框架](/sharepoint/dev/spfx/integrate-with-teams-introduction)选项卡。</span><span class="sxs-lookup"><span data-stu-id="66102-152">Alternatively, you can build a Teams tab [using the SharePoint Framework](/sharepoint/dev/spfx/integrate-with-teams-introduction).</span></span>

## <a name="aim-towards-multi-tenancy"></a><span data-ttu-id="66102-153">旨在实现多租户</span><span class="sxs-lookup"><span data-stu-id="66102-153">Aim towards multi-tenancy</span></span>

<span data-ttu-id="66102-154">\***集成方案**：独立应用、协作应用SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="66102-154">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="66102-155">如果你的应用由多个组织使用，请考虑多租户托管，它使产品可扩展并大大简化分发。</span><span class="sxs-lookup"><span data-stu-id="66102-155">If your app is used by multiple organizations, consider multi-tenant hosting that makes your product scalable and greatly simplify the distribution.</span></span>

## <a name="review-your-apis"></a><span data-ttu-id="66102-156">查看 API</span><span class="sxs-lookup"><span data-stu-id="66102-156">Review your APIs</span></span>

<span data-ttu-id="66102-157">\***集成方案**：独立应用、协作应用\*</span><span class="sxs-lookup"><span data-stu-id="66102-157">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="66102-158">与应用集成时，你必须使应用的现有 API 和数据结构支持Teams。</span><span class="sxs-lookup"><span data-stu-id="66102-158">You must make your app's existing APIs and data structures support the app when integrating with Teams.</span></span> <span data-ttu-id="66102-159">若要扩展支持，必须使用有关 Teams 的上下文信息扩充 API 和数据结构，以用于标识映射[](../concepts/authentication/configure-identity-provider.md)、深层链接[](../concepts/build-and-test/deep-links.md)支持以及合并 Microsoft [Graph。](/graph/teams-concept-overview)</span><span class="sxs-lookup"><span data-stu-id="66102-159">To extend the support, you must augment the APIs and data structures with contextual information about Teams for [identity mapping](../concepts/authentication/configure-identity-provider.md), [deep-link support](../concepts/build-and-test/deep-links.md), and [incorporating Microsoft Graph](/graph/teams-concept-overview).</span></span>

<span data-ttu-id="66102-160">了解有关获取应用选项卡或自动程序Teams[上下文](../tabs/how-to/access-teams-context.md)[。](../bots/how-to/get-teams-context.md)</span><span class="sxs-lookup"><span data-stu-id="66102-160">Learn more about getting context for your Teams [tab](../tabs/how-to/access-teams-context.md) or [bot](../bots/how-to/get-teams-context.md).</span></span>

## <a name="understand-authentication-options"></a><span data-ttu-id="66102-161">了解身份验证选项</span><span class="sxs-lookup"><span data-stu-id="66102-161">Understand authentication options</span></span>

<span data-ttu-id="66102-162">\***集成方案**：独立应用、协作应用SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="66102-162">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="66102-163">Azure Active Directory (AD) 是用户标识Teams。</span><span class="sxs-lookup"><span data-stu-id="66102-163">Azure Active Directory (AD) is the identity provider for Teams.</span></span> <span data-ttu-id="66102-164">如果你的应用使用不同的标识提供程序，则必须执行标识映射练习或与 Azure AD 结合使用。</span><span class="sxs-lookup"><span data-stu-id="66102-164">If your app uses a different identity provider, you must either do an identity mapping exercise or combine with Azure AD.</span></span>

<span data-ttu-id="66102-165">Teams Azure AD 为第三 (应用使用单一登录 (SSO) 机制。</span><span class="sxs-lookup"><span data-stu-id="66102-165">Teams has single sign-on (SSO) mechanisms with Azure AD for third-party apps.</span></span> <span data-ttu-id="66102-166">它还提供使用 OAuth 和开放 ID 身份验证等标准（称为 OIDC）将身份验证流连接其他标识提供程序。</span><span class="sxs-lookup"><span data-stu-id="66102-166">It also provides the guidance for authentication flows to other identity providers using standards such as OAuth and Open ID Connect, known as OIDC.</span></span>

<span data-ttu-id="66102-167">对于SharePoint，如果你希望 SSO 适用于另一个应用，则只能使用 SSO，并且不能添加另一个 Azure AD ID，因为 ID SharePoint应用。</span><span class="sxs-lookup"><span data-stu-id="66102-167">For SharePoint pages, you can only use SSO and cannot add another Azure AD ID if you want SSO to work for another app as the ID is the SharePoint app.</span></span>

<span data-ttu-id="66102-168">了解有关身份验证[在 Teams 中Teams。](../concepts/authentication/authentication.md)</span><span class="sxs-lookup"><span data-stu-id="66102-168">Learn more about [authentication in Teams](../concepts/authentication/authentication.md).</span></span>

## <a name="follow-teams-design-guidelines"></a><span data-ttu-id="66102-169">遵循Teams设计准则</span><span class="sxs-lookup"><span data-stu-id="66102-169">Follow Teams design guidelines</span></span>

<span data-ttu-id="66102-170">\***集成方案**：独立应用、协作应用\*</span><span class="sxs-lookup"><span data-stu-id="66102-170">\***Integration scenarios**: Standalone apps, collaboration apps\*</span></span>

<span data-ttu-id="66102-171">确保遵循[Teams准则](../concepts/design/understand-use-cases.md)，使应用成为本机应用Teams。</span><span class="sxs-lookup"><span data-stu-id="66102-171">Ensure to follow [Teams design guidelines](../concepts/design/understand-use-cases.md) to make your app native to Teams.</span></span> <span data-ttu-id="66102-172">无法将现有应用内容迁移到"Teams选项卡。有关应用设计详细信息，请参阅[Fluent Design System。](https://fluentsite.z22.web.core.windows.net/)</span><span class="sxs-lookup"><span data-stu-id="66102-172">You cannot migrate an existing app content to a Teams tab. For more information on app design, see [Fluent Design System](https://fluentsite.z22.web.core.windows.net/).</span></span>

## <a name="maximize-deep-linking"></a><span data-ttu-id="66102-173">最大化深层链接</span><span class="sxs-lookup"><span data-stu-id="66102-173">Maximize deep linking</span></span>

<span data-ttu-id="66102-174">\***集成方案**：独立应用、协作应用SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="66102-174">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="66102-175">您可以创建指向网站内的信息和功能Teams。</span><span class="sxs-lookup"><span data-stu-id="66102-175">You can create links to information and features within Teams.</span></span> <span data-ttu-id="66102-176">使用[深层链接](../concepts/build-and-test/deep-links.md)将你的应用与Teams，因为它们将应用的多个部分关联在一起，获得更本机的Teams体验。</span><span class="sxs-lookup"><span data-stu-id="66102-176">Use [deep links](../concepts/build-and-test/deep-links.md) to link your app with Teams as they tie together multiple pieces of an app for a more native Teams experience.</span></span>

## <a name="be-smart-when-messaging-users"></a><span data-ttu-id="66102-177">在消息传递用户时要智能</span><span class="sxs-lookup"><span data-stu-id="66102-177">Be smart when messaging users</span></span>

<span data-ttu-id="66102-178">\***集成方案**：独立应用、协作应用SharePoint\*</span><span class="sxs-lookup"><span data-stu-id="66102-178">\***Integration scenarios**: Standalone apps, collaboration apps, SharePoint\*</span></span>

<span data-ttu-id="66102-179">在多[线程](../bots/what-are-bots.md)Teams应用中使用自动程序，因为它提供比[webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md)更大的灵活性。</span><span class="sxs-lookup"><span data-stu-id="66102-179">Use a [bot](../bots/what-are-bots.md) in your Teams app for multi-threaded conversation, as it offers more flexibility than a [webhook](../webhooks-and-connectors/what-are-webhooks-and-connectors.md).</span></span>

<span data-ttu-id="66102-180">自动程序还允许你向单个 **用户** 或频道发送主动消息。</span><span class="sxs-lookup"><span data-stu-id="66102-180">Bots also allow you to send **proactive messages** to individual users or channels.</span></span> <span data-ttu-id="66102-181">主动邮件是由外部事件触发的未经提示的消息，而不是发送给自动程序的消息。</span><span class="sxs-lookup"><span data-stu-id="66102-181">The proactive messages are unprompted messages triggered by an outside event and not a message sent to a bot.</span></span> <span data-ttu-id="66102-182">例如，自动程序在安装或新用户加入频道时发送欢迎消息。</span><span class="sxs-lookup"><span data-stu-id="66102-182">For example, your bot sends a welcome message when it is installed or a new user joins a channel.</span></span> 

<span data-ttu-id="66102-183">发送主动邮件Teams特定标识符。</span><span class="sxs-lookup"><span data-stu-id="66102-183">Sending proactive messages requires Teams-specific identifiers.</span></span> <span data-ttu-id="66102-184">您可以通过提取[名单或用户配置文件](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile)数据、订阅对话事件，或者使用[](../bots/how-to/conversations/subscribe-to-conversation-events.md)Microsoft Graph[来捕获信息](/microsoftteams/platform/graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages?context=graph/context#proactive-messaging-in-teams)。</span><span class="sxs-lookup"><span data-stu-id="66102-184">You can capture the information by [fetching roster or user profile data](../bots/how-to/get-teams-context.md#fetch-the-roster-or-user-profile), [subscribing to conversation events](../bots/how-to/conversations/subscribe-to-conversation-events.md), or using [Microsoft Graph](/microsoftteams/platform/graph-api/proactive-bots-and-messages/graph-proactive-bots-and-messages?context=graph/context#proactive-messaging-in-teams).</span></span>

<span data-ttu-id="66102-185">不要向具有过多邮件的用户发送垃圾邮件。</span><span class="sxs-lookup"><span data-stu-id="66102-185">Do not spam users with excessive messages.</span></span> <span data-ttu-id="66102-186">如果Teams支持此功能，则用户可以为你的应用配置通知设置。</span><span class="sxs-lookup"><span data-stu-id="66102-186">If the Teams capability supports it, the users can configure notification settings for your app.</span></span>   
<span data-ttu-id="66102-187">下面是一条通知邮件的示例： **不要向我发送不通知的邮件**。</span><span class="sxs-lookup"><span data-stu-id="66102-187">Following is an example of a notification message: **Don't send me unprompted messages**.</span></span>

## <a name="use-sharepoint-for-file-and-data-storage"></a><span data-ttu-id="66102-188">将SharePoint用于文件和数据存储</span><span class="sxs-lookup"><span data-stu-id="66102-188">Use SharePoint for file and data storage</span></span>

<span data-ttu-id="66102-189">***集成方案：** 独立应用、协作应用SharePoint页面*</span><span class="sxs-lookup"><span data-stu-id="66102-189">***Integration scenarios:** Standalone apps, collaboration apps, SharePoint pages*</span></span>

<span data-ttu-id="66102-190">创建团队时，还会SharePoint[网站](/microsoftteams/sharepoint-onedrive-interact)集以支持该团队的文件和数据存储。</span><span class="sxs-lookup"><span data-stu-id="66102-190">When a team is created, a [SharePoint site collection](/microsoftteams/sharepoint-onedrive-interact) is also provisioned to support file and data storage for that team.</span></span> <span data-ttu-id="66102-191">如果应用与文件交互，则必须利用此功能。</span><span class="sxs-lookup"><span data-stu-id="66102-191">Your app must leverage this feature if it interacts with files.</span></span> <span data-ttu-id="66102-192">使用网站集将原始数据存储在SharePoint和Excel。</span><span class="sxs-lookup"><span data-stu-id="66102-192">Use the site collection to store raw data in SharePoint Lists and Excel.</span></span>

## <a name="see-also"></a><span data-ttu-id="66102-193">另请参阅</span><span class="sxs-lookup"><span data-stu-id="66102-193">See also</span></span>

[<span data-ttu-id="66102-194">集成 web 应用</span><span class="sxs-lookup"><span data-stu-id="66102-194">Integrate web apps</span></span>](~/samples/integrate-web-apps-overview.md)
