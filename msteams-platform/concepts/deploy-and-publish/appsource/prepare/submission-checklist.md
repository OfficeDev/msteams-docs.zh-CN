---
title: 应用商店提交清单
description: 将 Microsoft Teams 应用发布到 AppSource 之前使用的清单
ms.topic: reference
keywords: teams 发布应用商店 Office 发布清单提交 Teams 应用 appsource 验证
ms.openlocfilehash: 7cb9192c159e7d65aad188c9746de3de7947a42b
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014213"
---
# <a name="prepare-for-appsource-submission"></a><span data-ttu-id="3f25b-104">准备 AppSource 提交</span><span class="sxs-lookup"><span data-stu-id="3f25b-104">Prepare for AppSource submission</span></span>  

<span data-ttu-id="3f25b-105">若要在 AppSource 上列出，应用必须完成审批过程。</span><span class="sxs-lookup"><span data-stu-id="3f25b-105">To be listed on AppSource, your app must go through an approval process.</span></span> <span data-ttu-id="3f25b-106">这是 Microsoft Teams 组提供的一项免费服务，可验证你的应用是否按所述工作，包含所有适当的元数据，并提供对最终用户有价值的内容。</span><span class="sxs-lookup"><span data-stu-id="3f25b-106">This is a free service provided by the Microsoft Teams group that verifies that your app works as described, contains all appropriate metadata, and provides content that would be valuable to an end user.</span></span> <span data-ttu-id="3f25b-107">为了帮助你快速获得批准，请确保你的应用满足以下要求和准则：</span><span class="sxs-lookup"><span data-stu-id="3f25b-107">To help you achieve rapid approval, ensure your app meets the following requirements and guidelines:</span></span>

* <span data-ttu-id="3f25b-108">**分发方法：** 确保你的应用适合在应用商店平台上发布。</span><span class="sxs-lookup"><span data-stu-id="3f25b-108">**Distribution method:** Make sure your app is meant for publication on a store platform.</span></span> <span data-ttu-id="3f25b-109">还有其他 [一些选项可用于](../../overview.md) 分发应用，而无需发布到 AppSource。</span><span class="sxs-lookup"><span data-stu-id="3f25b-109">There are [other options](../../overview.md) to distribute your app without publishing to AppSource.</span></span>
* <span data-ttu-id="3f25b-110">**验证策略：** 应用必须在提交之前通过所有 [当前 AppSource](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams) 验证策略。</span><span class="sxs-lookup"><span data-stu-id="3f25b-110">**Validation policies:** Your app must pass all current [AppSource validation policies](https://docs.microsoft.com/legal/marketplace/certification-policies#1140-teams) before submission.</span></span> 
  > [!NOTE] 
  > <span data-ttu-id="3f25b-111">Appsource 验证策略可能会更改。</span><span class="sxs-lookup"><span data-stu-id="3f25b-111">The Appsource validation policies are subject to change.</span></span>
* <span data-ttu-id="3f25b-112">**移动就绪情况：** 你的应用必须具有移动响应能力。</span><span class="sxs-lookup"><span data-stu-id="3f25b-112">**Mobile readiness:** Your app must be mobile responsive.</span></span> <span data-ttu-id="3f25b-113">如果你的应用包含选项卡，它们必须遵循移动设计指南[](~/tabs/design/tabs-mobile.md)，并且你的应用必须符合 iOS 和[](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment)Android (移动操作系统上的) 。</span><span class="sxs-lookup"><span data-stu-id="3f25b-113">If your app contains tabs, they must follow the [mobile design guidelines](~/tabs/design/tabs-mobile.md) and your app must comply with [no upsell requirements](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment) on mobile OS (iOS and Android).</span></span>
* <span data-ttu-id="3f25b-114">**自行测试应用：** 使用清单验证 [工具测试你的应用](#teams-app-validation-tool)。</span><span class="sxs-lookup"><span data-stu-id="3f25b-114">**Self test your app:** Test your app using the [Manifest validation tool](#teams-app-validation-tool).</span></span>
* <span data-ttu-id="3f25b-115">**应用详细信息页面：** 你的应用必须与应用详细信息  [页面清单一致](detail-page-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="3f25b-115">**App detail page:** Your app must align with the  [App detail page checklist](detail-page-checklist.md).</span></span>
* <span data-ttu-id="3f25b-116">**提示和经常失败的情况：** 请特别注意列出的 [提示和经常失败的情况](frequently-failed-cases.md)  ，以改进应用提交和审批时间。</span><span class="sxs-lookup"><span data-stu-id="3f25b-116">**Tips and frequently failed cases:** Pay extra attention to the listed [Tips and frequently failed cases](frequently-failed-cases.md)  to improve your app submission and approval time.</span></span>
* <span data-ttu-id="3f25b-117">**应用清单：** 根据应用清单清单 [检查应用清单](app-manifest-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="3f25b-117">**App manifest:** Check your app manifest against the [App manifest checklist](app-manifest-checklist.md).</span></span>
* <span data-ttu-id="3f25b-118">**测试和调试：** 确保你已 [完全测试和调试你的应用](../../../build-and-test/debug.md)。</span><span class="sxs-lookup"><span data-stu-id="3f25b-118">**Testing and debugging:** Make certain that you have fully [tested and debugged your app](../../../build-and-test/debug.md).</span></span>
* <span data-ttu-id="3f25b-119">**测试说明：** 包括 [测试说明进行验证](#test-notes-for-validation)</span><span class="sxs-lookup"><span data-stu-id="3f25b-119">**Testing notes:** Include your [test notes for validation](#test-notes-for-validation)</span></span>
* <span data-ttu-id="3f25b-120">**隐私策略：** 确保 [隐私策略、使用条款和支持 URL 遵循](#privacy-policy-terms-of-use-and-support-urls) 我们的指南。</span><span class="sxs-lookup"><span data-stu-id="3f25b-120">**Privacy policies:** Ensure your [privacy policy, terms of use and support URLs](#privacy-policy-terms-of-use-and-support-urls) follow our guidelines.</span></span>

<span data-ttu-id="3f25b-121">完成上述所有要求后，通过合作伙伴中心将程序包提交到[AppSource。](/office/dev/store/use-partner-center-to-submit-to-appsource)</span><span class="sxs-lookup"><span data-stu-id="3f25b-121">Once you have completed all of the above requirements, submit your package to AppSource through [Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource).</span></span>

## <a name="teams-app-validation-tool"></a><span data-ttu-id="3f25b-122">Teams 应用验证工具</span><span class="sxs-lookup"><span data-stu-id="3f25b-122">Teams App Validation Tool</span></span>

<span data-ttu-id="3f25b-123">应用程序验证工具由应用[验证器和](#teams-app-validator)[初步清单组成](#preliminary-checklist)。</span><span class="sxs-lookup"><span data-stu-id="3f25b-123">The app validation tool consists of an [app validator](#teams-app-validator) and a [preliminary checklist](#preliminary-checklist).</span></span> <span data-ttu-id="3f25b-124">该工具复制 [AppSource](/office/dev/store/submit-to-appsource-via-partner-center) 用于评估应用提交的相同测试用例。</span><span class="sxs-lookup"><span data-stu-id="3f25b-124">The tool replicates the same test cases used by [AppSource](/office/dev/store/submit-to-appsource-via-partner-center) to evaluate your app submission.</span></span> <span data-ttu-id="3f25b-125">因此，在将解决方案提交到 AppSource 进行审批之前，通过所有测试用例至关重要。该工具可在 Teams 平台内的多个区域找到：</span><span class="sxs-lookup"><span data-stu-id="3f25b-125">Therefore,  it's crucial to pass all the test cases prior to submitting your solution to AppSource for approval.The tool can be found in several areas within the Teams platform:</span></span>

> [!div class="checklist"]
>
> * [<span data-ttu-id="3f25b-126">**应用验证程序主页**</span><span class="sxs-lookup"><span data-stu-id="3f25b-126">**App Validator homepage**</span></span>](https://dev.teams.microsoft.com/appvalidation.html)
> * [<span data-ttu-id="3f25b-127">**Teams Visual Studio 代码工具包**</span><span class="sxs-lookup"><span data-stu-id="3f25b-127">**Teams Visual Studio Code toolkit**</span></span>](/toolkit/visual-studio-code-overview.md)
> * [<span data-ttu-id="3f25b-128">**应用程序 Studio**</span><span class="sxs-lookup"><span data-stu-id="3f25b-128">**App Studio**</span></span>](/concepts/build-and-test/app-studio-overview.md)

### <a name="teams-app-validator"></a><span data-ttu-id="3f25b-129">Teams 应用验证程序</span><span class="sxs-lookup"><span data-stu-id="3f25b-129">Teams app validator</span></span>

<span data-ttu-id="3f25b-130">" **验证** "页允许你在提交到 AppSource 之前检查应用包。</span><span class="sxs-lookup"><span data-stu-id="3f25b-130">The **Validate** page allows you to check your app package before submission to AppSource.</span></span> <span data-ttu-id="3f25b-131">只需上传应用包，验证工具将针对所有清单相关的测试用例检查应用。</span><span class="sxs-lookup"><span data-stu-id="3f25b-131">Simply upload your app package and the validation tool will check your app against all manifest-related test cases.</span></span> <span data-ttu-id="3f25b-132">对于每个失败的测试，该说明都提供了一个文档链接，以帮助您修复错误。</span><span class="sxs-lookup"><span data-stu-id="3f25b-132">For each failed test, the description provides a documentation link to help you fix the error.</span></span>

![验证工具](../../../../assets/images/validation-tool/validator.png)

### <a name="preliminary-checklist"></a><span data-ttu-id="3f25b-134">初步清单</span><span class="sxs-lookup"><span data-stu-id="3f25b-134">Preliminary checklist</span></span>

<span data-ttu-id="3f25b-135">对于难以自动化的测试方案，初步清单显示七个最常失败的测试用例。</span><span class="sxs-lookup"><span data-stu-id="3f25b-135">For test scenarios that are difficult to automate, the preliminary checklist surfaces seven of the most commonly failed test cases.</span></span>

![初步清单](../../../../assets/images/validation-tool/preliminary-checklist.png)

## <a name="privacy-policy-terms-of-use-and-support-urls"></a><span data-ttu-id="3f25b-137">隐私策略、使用条款和支持 URL</span><span class="sxs-lookup"><span data-stu-id="3f25b-137">Privacy policy, terms of use and support URLs</span></span>

### <a name="privacy-policy"></a><span data-ttu-id="3f25b-138">隐私策略</span><span class="sxs-lookup"><span data-stu-id="3f25b-138">Privacy policy</span></span>

<span data-ttu-id="3f25b-139">隐私策略指南：</span><span class="sxs-lookup"><span data-stu-id="3f25b-139">Privacy policy guidelines:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="3f25b-140">隐私策略可以特定于你的应用和/或所有服务的整体策略。</span><span class="sxs-lookup"><span data-stu-id="3f25b-140">The privacy policy can be specific to your app and/or an overall policy for all of your services.</span></span>
> * <span data-ttu-id="3f25b-141">如果使用通用隐私策略，则必须引用"服务"、"应用程序"和"平台"，以包括 Teams 应用和网站。</span><span class="sxs-lookup"><span data-stu-id="3f25b-141">If you use a generic privacy policy, it must reference "services", "applications", and "platforms" to include your Teams app as well as your website.</span></span>
> * <span data-ttu-id="3f25b-142">它必须包括如何处理用户数据存储、用户数据保留、删除和安全控制。</span><span class="sxs-lookup"><span data-stu-id="3f25b-142">It must include how you handle user data storage, user data retention, deletion, and security controls.</span></span>
> * <span data-ttu-id="3f25b-143">它必须包含您的联系信息。</span><span class="sxs-lookup"><span data-stu-id="3f25b-143">It must include your contact information.</span></span>
> * <span data-ttu-id="3f25b-144">它不应包含断开的链接、beta URL 或暂存 URL。</span><span class="sxs-lookup"><span data-stu-id="3f25b-144">It should not contain broken links, beta URLs, or staging URLs.</span></span>

### <a name="terms-of-use"></a><span data-ttu-id="3f25b-145">使用条款</span><span class="sxs-lookup"><span data-stu-id="3f25b-145">Terms of use</span></span>

<span data-ttu-id="3f25b-146">使用条款声明应特定于应用和/或外接程序产品/服务。</span><span class="sxs-lookup"><span data-stu-id="3f25b-146">Your terms of use statement should be specific and applicable to your app and/or add-in offering.</span></span>

### <a name="support-urls"></a><span data-ttu-id="3f25b-147">支持 URL</span><span class="sxs-lookup"><span data-stu-id="3f25b-147">Support URLs</span></span>

<span data-ttu-id="3f25b-148">支持 URL 不应要求身份验证或登录凭据来联系你，以发现应用的任何问题。</span><span class="sxs-lookup"><span data-stu-id="3f25b-148">Your support URLs should not require authentication or login credential to contact you for any issues with your app.</span></span>

## <a name="test-notes-for-validation"></a><span data-ttu-id="3f25b-149">用于验证的测试说明</span><span class="sxs-lookup"><span data-stu-id="3f25b-149">Test notes for validation</span></span>

<span data-ttu-id="3f25b-150">请包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="3f25b-150">Please include the following:</span></span>

* <span data-ttu-id="3f25b-151">您必须至少提供两个登录凭据，一个管理员和非管理员。</span><span class="sxs-lookup"><span data-stu-id="3f25b-151">You must provide at least two login credentials, one admin and one non-admin.</span></span>

* <span data-ttu-id="3f25b-152">出于验证目的，你提供的帐户应具有足够的预填充数据。</span><span class="sxs-lookup"><span data-stu-id="3f25b-152">For verification purposes, the accounts you provide should have sufficient pre-populated data.</span></span>

* <span data-ttu-id="3f25b-153">对于企业应用、需要订阅的应用或具有 Office 365 租户/域依赖项的应用，必须在未为你的应用预配置的同一域中提供第三个帐户，以便我们可以验证首次运行的用户体验。</span><span class="sxs-lookup"><span data-stu-id="3f25b-153">For enterprise apps, apps where a subscription is required, or apps where there is an Office 365 tenant/domain dependency, you must provide a third account in the same domain that is not pre-configured for your app so that we can validate the first-run user experience.</span></span>

* <span data-ttu-id="3f25b-154">如果你的应用具有高级/升级功能，则必须提供具有必要访问权限的帐户来测试该体验。</span><span class="sxs-lookup"><span data-stu-id="3f25b-154">If your app has premium/upgraded features, an account with the necessary access must be provided to test that experience.</span></span>

* <span data-ttu-id="3f25b-155">您可以选择将测试说明上载到 SharePoint。</span><span class="sxs-lookup"><span data-stu-id="3f25b-155">You may choose to upload your test notes to SharePoint.</span></span> <span data-ttu-id="3f25b-156">如果是这样，请提供文件的公共链接。</span><span class="sxs-lookup"><span data-stu-id="3f25b-156">If so, please provide a public link to the file.</span></span>

* <span data-ttu-id="3f25b-157">**测试帐户**。</span><span class="sxs-lookup"><span data-stu-id="3f25b-157">**Test Accounts**.</span></span> <span data-ttu-id="3f25b-158">如果你的应用仅允许来自后端的许可帐户或安全列表，则测试帐户是必需的。</span><span class="sxs-lookup"><span data-stu-id="3f25b-158">A test account is required if your app only allows licensed accounts or safelisting from the backend.</span></span> <span data-ttu-id="3f25b-159">此外，如果应用中允许团队/群聊范围，则同一租户中的两个测试帐户需要验证团队协作方案。</span><span class="sxs-lookup"><span data-stu-id="3f25b-159">Also, if there is a team/group chat scope allowed in your app,  two test accounts in the same tenant are required to validate the team collaboration scenario.</span></span>

* <span data-ttu-id="3f25b-160">**集成步骤**。</span><span class="sxs-lookup"><span data-stu-id="3f25b-160">**Integration steps**.</span></span> <span data-ttu-id="3f25b-161">如果需要租户管理员进行预配置才能使用该应用，请包含这些步骤和/或提供配置的管理员帐户和非管理员帐户进行验证。</span><span class="sxs-lookup"><span data-stu-id="3f25b-161">If pre-configuration by a tenant admin is required to use the app, include the steps and/or provide configured admin and non-admin accounts for validation.</span></span> <span data-ttu-id="3f25b-162">注意：你可以注册 [Office 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program) 订阅。</span><span class="sxs-lookup"><span data-stu-id="3f25b-162">Note: you can sign up for an [Office 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="3f25b-163">它 *90* 天免费，并且将持续续订，只要使用它进行开发活动。</span><span class="sxs-lookup"><span data-stu-id="3f25b-163">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span>

* <span data-ttu-id="3f25b-164">**有关 Teams 中的** 应用功能的注释：详细介绍了应用在 Teams 中提供的所有功能以及测试每个功能的步骤。</span><span class="sxs-lookup"><span data-stu-id="3f25b-164">**Notes regarding the app features in Teams**: Detail all of the capabilities the app offers within Teams and steps for testing each feature.</span></span>

* <span data-ttu-id="3f25b-165">**显示应用功能的视频 (可选**) ：你可以提供产品的视频录制，以便我们完全了解应用的功能。</span><span class="sxs-lookup"><span data-stu-id="3f25b-165">**Video showing the app functionality (Optional)**: You can provide a video recording of the product for us to fully understand the functionality of the app.</span></span>
