---
title: 准备应用商店提交
description: 介绍提交要列在应用商店Microsoft Teams应用之前的最后步骤。
ms.topic: how-to
localization_priority: Normal
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: d46d21c3d984b5688c00857e485210b0f0fcf2c7
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101679"
---
# <a name="prepare-your-microsoft-teams-store-submission"></a><span data-ttu-id="4e36a-103">准备Microsoft Teams应用商店提交</span><span class="sxs-lookup"><span data-stu-id="4e36a-103">Prepare your Microsoft Teams store submission</span></span>

<span data-ttu-id="4e36a-104">你已设计、生成和测试Microsoft Teams应用。</span><span class="sxs-lookup"><span data-stu-id="4e36a-104">You've designed, built, and tested your Microsoft Teams app.</span></span> <span data-ttu-id="4e36a-105">现在，你已准备好列出它，以便用户可以发现并开始使用你的应用。</span><span class="sxs-lookup"><span data-stu-id="4e36a-105">Now you're ready to list it so people can discover and start using your app.</span></span>

<span data-ttu-id="4e36a-106">在将应用提交到 [合作伙伴中心](/office/dev/store/use-partner-center-to-submit-to-appsource)之前，请确保你已完成以下操作。</span><span class="sxs-lookup"><span data-stu-id="4e36a-106">Before you submit your app to [Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource), make sure you've done the following.</span></span>

## <a name="validate-your-app-package"></a><span data-ttu-id="4e36a-107">验证应用包</span><span class="sxs-lookup"><span data-stu-id="4e36a-107">Validate your app package</span></span>

<span data-ttu-id="4e36a-108">当你的应用可能在测试环境中运行时，你应该检查你的应用包，以避免在提交过程中出现问题。</span><span class="sxs-lookup"><span data-stu-id="4e36a-108">While your app may be working in a test environment, you should check your app package to avoid running into issues during the submission process.</span></span>

<span data-ttu-id="4e36a-109">应用Microsoft Teams工具可帮助你在提交到合作伙伴中心之前识别和修复问题。</span><span class="sxs-lookup"><span data-stu-id="4e36a-109">The Microsoft Teams app validation tool helps you identify and fix issues before submitting to Partner Center.</span></span> <span data-ttu-id="4e36a-110">该工具根据应用商店验证期间使用的相同测试用例自动检查应用的配置。</span><span class="sxs-lookup"><span data-stu-id="4e36a-110">The tool automatically checks your app's configurations against the same test cases used during store validation.</span></span>

1. <span data-ttu-id="4e36a-111">转到应用[Microsoft Teams工具](https://dev.teams.microsoft.com/appvalidation.html)。</span><span class="sxs-lookup"><span data-stu-id="4e36a-111">Go to the [Microsoft Teams app validation tool](https://dev.teams.microsoft.com/appvalidation.html).</span></span> <span data-ttu-id="4e36a-112"> (注意：该工具在 [App Studio](../../../build-and-test/app-studio-overview.md).) </span><span class="sxs-lookup"><span data-stu-id="4e36a-112">(Note: The tool is also available in [App Studio](../../../build-and-test/app-studio-overview.md).)</span></span>
1. <span data-ttu-id="4e36a-113">Upload应用包运行自动测试。</span><span class="sxs-lookup"><span data-stu-id="4e36a-113">Upload your app package to run the automated tests.</span></span>
1. <span data-ttu-id="4e36a-114">转到" **初步检查表** "并查看难以自动化的测试用例。</span><span class="sxs-lookup"><span data-stu-id="4e36a-114">Go to the **Preliminary checklist** and review the test cases that are difficult to automate.</span></span>
1. <span data-ttu-id="4e36a-115">[修复了当自动测试](~/resources/schema/manifest-schema.md) 出错或未满足检查表中所有条件时的配置或应用的问题。</span><span class="sxs-lookup"><span data-stu-id="4e36a-115">[Fix issues with your configurations](~/resources/schema/manifest-schema.md) or app in general if the automated tests give you errors or you haven't met all the criteria in the checklist.</span></span>

## <a name="compile-testing-instructions"></a><span data-ttu-id="4e36a-116">编译测试说明</span><span class="sxs-lookup"><span data-stu-id="4e36a-116">Compile testing instructions</span></span>

<span data-ttu-id="4e36a-117">提供说明和资源来帮助审阅者测试你的应用，包括测试帐户、凭据和许可证密钥。</span><span class="sxs-lookup"><span data-stu-id="4e36a-117">Provide instructions and resources to help the reviewers test your app, including test accounts, credentials, and license keys.</span></span> <span data-ttu-id="4e36a-118">你可以添加合作伙伴中心中的说明，或将它们上载到 SharePoint 上的公开位置。</span><span class="sxs-lookup"><span data-stu-id="4e36a-118">You can add instructions in Partner Center or upload them to a publicly available location on SharePoint.</span></span>

### <a name="feature-list"></a><span data-ttu-id="4e36a-119">功能列表</span><span class="sxs-lookup"><span data-stu-id="4e36a-119">Feature list</span></span>

<span data-ttu-id="4e36a-120">提供有关应用功能的详细信息，Teams测试每个功能的步骤。</span><span class="sxs-lookup"><span data-stu-id="4e36a-120">Provide details about your app's capabilities in Teams and steps for testing each one.</span></span>

### <a name="accounts"></a><span data-ttu-id="4e36a-121">帐户</span><span class="sxs-lookup"><span data-stu-id="4e36a-121">Accounts</span></span>

<span data-ttu-id="4e36a-122">如果你的应用需要许可证或后端安全列表，则必须提供测试帐户。</span><span class="sxs-lookup"><span data-stu-id="4e36a-122">You must provide test accounts if your app requires a license or backend safelisting.</span></span> <span data-ttu-id="4e36a-123">你提供的所有帐户都必须包含预填充的数据，以便于测试。</span><span class="sxs-lookup"><span data-stu-id="4e36a-123">All accounts you provide must include pre-populated data to facilitate testing.</span></span>

<span data-ttu-id="4e36a-124">根据应用的功能，可能需要提供以下所有功能：</span><span class="sxs-lookup"><span data-stu-id="4e36a-124">Depending on your app's features, you may need to provide all of the following:</span></span>

* <span data-ttu-id="4e36a-125">管理员帐户 (管理员) </span><span class="sxs-lookup"><span data-stu-id="4e36a-125">Admin account (required)</span></span>
* <span data-ttu-id="4e36a-126">非管理员帐户 (必需) </span><span class="sxs-lookup"><span data-stu-id="4e36a-126">Non-admin account (required)</span></span>
* <span data-ttu-id="4e36a-127">为了正确测试首次运行登录体验而未预配置的帐户 (要求) </span><span class="sxs-lookup"><span data-stu-id="4e36a-127">An account that isn't pre-configured in order to properly test the first-run sign-in experience (required)</span></span>
* <span data-ttu-id="4e36a-128">有权访问高级或升级功能的帐户 (如果适用) </span><span class="sxs-lookup"><span data-stu-id="4e36a-128">An account with access to premium or upgraded features (if applicable)</span></span>
* <span data-ttu-id="4e36a-129">同一租户中的两个帐户，用于测试在共享上下文中工作的应用的 (体验（如果适用) </span><span class="sxs-lookup"><span data-stu-id="4e36a-129">Two accounts in the same tenant to test the collaboration experience for apps that work in shared contexts (if applicable)</span></span>

### <a name="tenant-configurations"></a><span data-ttu-id="4e36a-130">租户配置</span><span class="sxs-lookup"><span data-stu-id="4e36a-130">Tenant configurations</span></span>

<span data-ttu-id="4e36a-131">如果必须配置Teams租户才能使用你的应用，请包含这些说明以及管理员和非管理员帐户进行验证。</span><span class="sxs-lookup"><span data-stu-id="4e36a-131">If you must configure a Teams tenant to use your app, include those instructions and admin and non-admin accounts for validation.</span></span>

### <a name="video-optional"></a><span data-ttu-id="4e36a-132">视频 (可选) </span><span class="sxs-lookup"><span data-stu-id="4e36a-132">Video (optional)</span></span>

<span data-ttu-id="4e36a-133">提供你的应用的录制，以便 Microsoft 可以完全了解其功能。</span><span class="sxs-lookup"><span data-stu-id="4e36a-133">Provide a recording of your app so that Microsoft can fully understand its functionality.</span></span>

## <a name="create-your-store-listing-details"></a><span data-ttu-id="4e36a-134">创建应用商店一览详细信息</span><span class="sxs-lookup"><span data-stu-id="4e36a-134">Create your store listing details</span></span>

<span data-ttu-id="4e36a-135">你提交到合作伙伴[中心&#8212;包括](https://partner.microsoft.com)你的姓名、说明、图标和图像&#8212;成为应用的 Teams 应用商店和 Microsoft AppSource 一览。</span><span class="sxs-lookup"><span data-stu-id="4e36a-135">The information that you submit to [Partner Center](https://partner.microsoft.com)&#8212;including your name, descriptions, icons, and images&#8212;becomes the Teams store and Microsoft AppSource listing for your app.</span></span>

<span data-ttu-id="4e36a-136">应用商店一览可能是某人对你的应用的第一印象。</span><span class="sxs-lookup"><span data-stu-id="4e36a-136">A store listing may be someone's first impression of your app.</span></span> <span data-ttu-id="4e36a-137">通过可有效传达应用优势、功能和品牌一览增加安装量。</span><span class="sxs-lookup"><span data-stu-id="4e36a-137">Increase installations with a listing that effectively conveys your app's benefits, functionality, and brand.</span></span>

### <a name="specify-a-short-name"></a><span data-ttu-id="4e36a-138">指定短名称</span><span class="sxs-lookup"><span data-stu-id="4e36a-138">Specify a short name</span></span>

<span data-ttu-id="4e36a-139">特别是，你的应用 (，它的短) 在用户如何在应用商店[](~/resources/schema/manifest-schema.md#name)中发现它方面起到重要作用。</span><span class="sxs-lookup"><span data-stu-id="4e36a-139">Your app's name (specifically, its [*short name*](~/resources/schema/manifest-schema.md#name)) plays a crucial role in how users discover it in the store.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="../../../../assets/images/store-detail-page/AppName-02.png" alt-text="示例屏幕截图突出显示了在应用商店一览中显示应用的短名称的位置。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="4e36a-141">确保你的短名称符合应用商店 [验证准则](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name)。</span><span class="sxs-lookup"><span data-stu-id="4e36a-141">Make sure your short name adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#11-app-name).</span></span>

### <a name="write-descriptions"></a><span data-ttu-id="4e36a-142">编写说明</span><span class="sxs-lookup"><span data-stu-id="4e36a-142">Write descriptions</span></span>

<span data-ttu-id="4e36a-143">必须对你的应用进行简短而详细的说明。</span><span class="sxs-lookup"><span data-stu-id="4e36a-143">You must have a short and long description of your app.</span></span>

#### <a name="short-description"></a><span data-ttu-id="4e36a-144">简短说明</span><span class="sxs-lookup"><span data-stu-id="4e36a-144">Short description</span></span>

<span data-ttu-id="4e36a-145">应用简洁摘要，应原始、具有吸引力，并面向目标受众。</span><span class="sxs-lookup"><span data-stu-id="4e36a-145">A concise summary of your app that should be original, engaging, and directed at your target audience.</span></span> <span data-ttu-id="4e36a-146">将简短说明保留为一个句子。</span><span class="sxs-lookup"><span data-stu-id="4e36a-146">Keep the short description to one sentence.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/ShortDescription-02.png" alt-text="示例屏幕截图突出显示了在应用商店一览中显示应用的简短说明的位置。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="4e36a-148">请确保简短说明符合应用商店 [验证准则](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description)。</span><span class="sxs-lookup"><span data-stu-id="4e36a-148">Make sure your short description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#431-short-description).</span></span>

#### <a name="long-description"></a><span data-ttu-id="4e36a-149">较长说明</span><span class="sxs-lookup"><span data-stu-id="4e36a-149">Long description</span></span>

<span data-ttu-id="4e36a-150">长描述可以提供一个叙述性内容，其中突出显示了应用的主要功能、它所解决的问题及其目标受众。</span><span class="sxs-lookup"><span data-stu-id="4e36a-150">The long description can provide a narrative that highlights your app's main features, the problems it solves, and its target audience.</span></span> <span data-ttu-id="4e36a-151">虽然此说明可以有 4，000 个字符，但大多数用户只能阅读 300 到 500 个单词。</span><span class="sxs-lookup"><span data-stu-id="4e36a-151">While this description can be as long as 4,000 characters, most users will only read between 300-500 words.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/LongDescription-02.png" alt-text="示例屏幕截图突出显示了在应用商店一览中显示应用长说明的位置。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="4e36a-153">请确保你的详细说明符合应用商店 [验证准则](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description)。</span><span class="sxs-lookup"><span data-stu-id="4e36a-153">Make sure your long description adheres to the [store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#432-long-description).</span></span>

### <a name="adhere-to-icon-design-guidelines"></a><span data-ttu-id="4e36a-154">遵守图标设计指南</span><span class="sxs-lookup"><span data-stu-id="4e36a-154">Adhere to icon design guidelines</span></span>

<span data-ttu-id="4e36a-155">图标是用户在浏览应用商店时看到的主要元素之一。</span><span class="sxs-lookup"><span data-stu-id="4e36a-155">Icons are one of the main elements users see when browsing the store.</span></span> <span data-ttu-id="4e36a-156">图标应传达应用的品牌和用途，同时遵循Teams要求。</span><span class="sxs-lookup"><span data-stu-id="4e36a-156">Your icons should communicate your app's brand and purpose while also adhering to Teams requirements.</span></span>

<span data-ttu-id="4e36a-157">有关详细信息，请参阅[有关创建应用图标Teams指南](~/concepts/build-and-test/apps-package.md#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="4e36a-157">For more information, see [guidance on creating Teams app icons](~/concepts/build-and-test/apps-package.md#app-icons).</span></span>

### <a name="capture-screenshots"></a><span data-ttu-id="4e36a-158">捕获屏幕截图</span><span class="sxs-lookup"><span data-stu-id="4e36a-158">Capture screenshots</span></span>

<span data-ttu-id="4e36a-159">Screenshots provide a prominent visual preview of your app to complement your app name， icon， and descriptions.</span><span class="sxs-lookup"><span data-stu-id="4e36a-159">Screenshots provide a prominent visual preview of your app to complement your app name, icon, and descriptions.</span></span>

:::row:::

   :::column span="3":::
      :::image type="content" source="~/assets/images/store-detail-page/Screenshot-01.png" alt-text="示例屏幕截图突出显示了应用屏幕截图在应用商店一览中的显示位置。":::
   :::column-end:::
   :::column span="1":::
   :::column-end:::

:::row-end:::

<span data-ttu-id="4e36a-161">请记住以下有关屏幕截图：</span><span class="sxs-lookup"><span data-stu-id="4e36a-161">Remember the following about screenshots:</span></span>

* <span data-ttu-id="4e36a-162">每个列表最多可以有五张屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="4e36a-162">You can have up to five screenshots per listing.</span></span>
* <span data-ttu-id="4e36a-163">受支持的文件类型包括 PNG、JPEG 和 GIF。</span><span class="sxs-lookup"><span data-stu-id="4e36a-163">Supported file types include PNG, JPEG, and GIF.</span></span>
* <span data-ttu-id="4e36a-164">尺寸应为 1366x768 像素。</span><span class="sxs-lookup"><span data-stu-id="4e36a-164">Dimensions should be 1366x768 pixels.</span></span>
* <span data-ttu-id="4e36a-165">最大大小为 1，024 KB。</span><span class="sxs-lookup"><span data-stu-id="4e36a-165">Maximum size of 1,024 KB.</span></span>

<span data-ttu-id="4e36a-166">有关最佳做法，请参阅以下资源：</span><span class="sxs-lookup"><span data-stu-id="4e36a-166">For best practices, see the following resources:</span></span>

* [<span data-ttu-id="4e36a-167">Teams应用商店验证指南</span><span class="sxs-lookup"><span data-stu-id="4e36a-167">Teams store validation guidelines</span></span>](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md#44-screenshots)
* [<span data-ttu-id="4e36a-168">为 Microsoft 应用商店精心制作有效图像</span><span class="sxs-lookup"><span data-stu-id="4e36a-168">Craft effective images for Microsoft app stores</span></span>](/office/dev/store/craft-effective-appsource-store-images)

### <a name="create-a-video"></a><span data-ttu-id="4e36a-169">创建视频</span><span class="sxs-lookup"><span data-stu-id="4e36a-169">Create a video</span></span>

<span data-ttu-id="4e36a-170">一览中的视频可能是传达人们为什么应该使用你的应用的最有效方式。</span><span class="sxs-lookup"><span data-stu-id="4e36a-170">A video in your listing can be the most effective way to communicate why people should use your app.</span></span> <span data-ttu-id="4e36a-171">你应该在视频中回答以下问题：</span><span class="sxs-lookup"><span data-stu-id="4e36a-171">You should address the following questions in a video:</span></span>

* <span data-ttu-id="4e36a-172">Who应用是否适用于？</span><span class="sxs-lookup"><span data-stu-id="4e36a-172">Who is your app for?</span></span>
* <span data-ttu-id="4e36a-173">你的应用可以解决哪些问题？</span><span class="sxs-lookup"><span data-stu-id="4e36a-173">What problems can your app solve?</span></span>
* <span data-ttu-id="4e36a-174">你的应用如何工作？</span><span class="sxs-lookup"><span data-stu-id="4e36a-174">How does your app work?</span></span>
* <span data-ttu-id="4e36a-175">使用你的应用还有其他哪些好处？</span><span class="sxs-lookup"><span data-stu-id="4e36a-175">What other benefits do you get from using your app?</span></span>

#### <a name="best-practices-for-videos"></a><span data-ttu-id="4e36a-176">视频最佳做法</span><span class="sxs-lookup"><span data-stu-id="4e36a-176">Best practices for videos</span></span>

* <span data-ttu-id="4e36a-177">将视频保留 30-90 秒。</span><span class="sxs-lookup"><span data-stu-id="4e36a-177">Keep your video between 30-90 seconds.</span></span>
* <span data-ttu-id="4e36a-178">以质量为目标。</span><span class="sxs-lookup"><span data-stu-id="4e36a-178">Aim for quality.</span></span> <span data-ttu-id="4e36a-179">在列表中，用户将在屏幕截图前看到视频。</span><span class="sxs-lookup"><span data-stu-id="4e36a-179">In a listing, users will see your video before screenshots.</span></span>

### <a name="select-a-category-for-your-app"></a><span data-ttu-id="4e36a-180">为应用选择类别</span><span class="sxs-lookup"><span data-stu-id="4e36a-180">Select a category for your app</span></span>

<span data-ttu-id="4e36a-181">在提交过程中，将要求你对应用进行分类。</span><span class="sxs-lookup"><span data-stu-id="4e36a-181">During submission, you're asked to categorize your app.</span></span> <span data-ttu-id="4e36a-182">下表将Teams应用商店类别映射到合作伙伴中心[中列出的类别](https://aka.ms/PartnerCenterHomePage)。</span><span class="sxs-lookup"><span data-stu-id="4e36a-182">The following table maps Teams store categories to the categories listed in [Partner Center](https://aka.ms/PartnerCenterHomePage).</span></span>

| <span data-ttu-id="4e36a-183">Teams类别</span><span class="sxs-lookup"><span data-stu-id="4e36a-183">Teams categories</span></span>       | <span data-ttu-id="4e36a-184">合作伙伴中心类别</span><span class="sxs-lookup"><span data-stu-id="4e36a-184">Partner Center categories</span></span>  |
|:---------------------|:---------------|
| <span data-ttu-id="4e36a-185">分析和 BI</span><span class="sxs-lookup"><span data-stu-id="4e36a-185">Analytics and BI</span></span> | <span data-ttu-id="4e36a-186">分析、数据可视化和 BI</span><span class="sxs-lookup"><span data-stu-id="4e36a-186">Analytics, Data Visualization and BI</span></span> |
| <span data-ttu-id="4e36a-187">开发人员和 IT</span><span class="sxs-lookup"><span data-stu-id="4e36a-187">Developer and IT</span></span> | <span data-ttu-id="4e36a-188">开发人员工具、IT 管理员</span><span class="sxs-lookup"><span data-stu-id="4e36a-188">Developer Tools, IT Admin</span></span> |
| <span data-ttu-id="4e36a-189">教育</span><span class="sxs-lookup"><span data-stu-id="4e36a-189">Education</span></span> | <span data-ttu-id="4e36a-190">教育</span><span class="sxs-lookup"><span data-stu-id="4e36a-190">Education</span></span> |
| <span data-ttu-id="4e36a-191">人力资源</span><span class="sxs-lookup"><span data-stu-id="4e36a-191">Human resources</span></span> | <span data-ttu-id="4e36a-192">人力资源和招聘</span><span class="sxs-lookup"><span data-stu-id="4e36a-192">Human Resources and Recruiting</span></span> |
| <span data-ttu-id="4e36a-193">工作效率</span><span class="sxs-lookup"><span data-stu-id="4e36a-193">Productivity</span></span> | <span data-ttu-id="4e36a-194">内容管理、文件和文档、生产力、培训和教程以及实用程序</span><span class="sxs-lookup"><span data-stu-id="4e36a-194">Content Management, Files and documents, Productivity, Training and Tutorials, and Utilities</span></span> |
| <span data-ttu-id="4e36a-195">项目管理</span><span class="sxs-lookup"><span data-stu-id="4e36a-195">Project management</span></span> | <span data-ttu-id="4e36a-196">通信、Project、工作流和业务管理</span><span class="sxs-lookup"><span data-stu-id="4e36a-196">Communication, Project Management, Workflow, and Business Management</span></span> |
| <span data-ttu-id="4e36a-197">销售和支持</span><span class="sxs-lookup"><span data-stu-id="4e36a-197">Sales and support</span></span> | <span data-ttu-id="4e36a-198">客户和联系人管理、客户支持、金融服务、销售和市场营销</span><span class="sxs-lookup"><span data-stu-id="4e36a-198">Customer and Contact Management, Customer Support, Financial Management, Sales and Marketing</span></span> |
| <span data-ttu-id="4e36a-199">社交和有趣</span><span class="sxs-lookup"><span data-stu-id="4e36a-199">Social and fun</span></span> | <span data-ttu-id="4e36a-200">图像和视频库、生活方式、新闻和天气、社交、旅行和导航</span><span class="sxs-lookup"><span data-stu-id="4e36a-200">Image and Video Galleries, Lifestyle, News and Weather, Social, Travel, and Navigation</span></span> |

### <a name="localize-your-store-listing"></a><span data-ttu-id="4e36a-201">本地化应用商店一览</span><span class="sxs-lookup"><span data-stu-id="4e36a-201">Localize your store listing</span></span>

<span data-ttu-id="4e36a-202">合作伙伴中心 [支持本地化的应用商店一览](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions)。</span><span class="sxs-lookup"><span data-stu-id="4e36a-202">Partner Center supports [localized store listings](https://docs.microsoft.com/office/dev/store/prepare-localized-solutions).</span></span> <span data-ttu-id="4e36a-203">有关详细信息，请参阅[如何本地化你的Teams应用一览](../../../../concepts/build-and-test/apps-localization.md)。</span><span class="sxs-lookup"><span data-stu-id="4e36a-203">For more information, see [how to localize your Teams app listing](../../../../concepts/build-and-test/apps-localization.md).</span></span>

## <a name="complete-publisher-verification"></a><span data-ttu-id="4e36a-204">完成Publisher验证</span><span class="sxs-lookup"><span data-stu-id="4e36a-204">Complete Publisher Verification</span></span>

<span data-ttu-id="4e36a-205">[Publisher应用商店](/azure/active-directory/develop/publisher-verification-overview)中列出的Teams应用需要验证。有关详细信息，请参阅[常见问题](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions)、[如何将](/azure/active-directory/develop/mark-app-as-publisher-verified)应用标记为发布者验证和发布者[验证疑难解答](/azure/active-directory/develop/troubleshoot-publisher-verification)。</span><span class="sxs-lookup"><span data-stu-id="4e36a-205">[Publisher Verification](/azure/active-directory/develop/publisher-verification-overview) is required for Teams apps listed in the store.For more information, see [frequently asked questions](/azure/active-directory/develop/publisher-verification-overview#frequently-asked-questions), [how to mark your app as publisher verified](/azure/active-directory/develop/mark-app-as-publisher-verified), and [troubleshoot publisher verification](/azure/active-directory/develop/troubleshoot-publisher-verification).</span></span>

## <a name="complete-publisher-attestation"></a><span data-ttu-id="4e36a-206">完整Publisher证明</span><span class="sxs-lookup"><span data-stu-id="4e36a-206">Complete Publisher Attestation</span></span>

<span data-ttu-id="4e36a-207">[Publisher应用商店](/microsoft-365-app-certification/docs/attestation)中列出的应用Teams证明也是必需的。</span><span class="sxs-lookup"><span data-stu-id="4e36a-207">[Publisher Attestation](/microsoft-365-app-certification/docs/attestation) is also required for Teams apps listed in the store.</span></span> <span data-ttu-id="4e36a-208">此过程包括完成对应用的安全性、数据处理和合规性做法的自我评估，从而有助于潜在客户做出有关使用应用的明智决定。</span><span class="sxs-lookup"><span data-stu-id="4e36a-208">The process includes completing a self-assessment of your app's security, data handling, and compliance practices that can help potential customers make informed decisions about using your app.</span></span>

> [!NOTE]
> <span data-ttu-id="4e36a-209">如果你要提交新应用，则你无法正式完成Publisher证明，直到你的应用在应用商店Teams列出。</span><span class="sxs-lookup"><span data-stu-id="4e36a-209">If you're submitting a new app, you can't officially complete Publisher Attestation until your app is listed on the Teams store.</span></span> <span data-ttu-id="4e36a-210">如果要更新列出的应用，请完成Publisher证明，然后再提交应用的最新版本进行验证。</span><span class="sxs-lookup"><span data-stu-id="4e36a-210">If you're updating a listed app, complete Publisher Attestation before you submit the latest version of the app for validation.</span></span>

## <a name="next-step"></a><span data-ttu-id="4e36a-211">后续步骤</span><span class="sxs-lookup"><span data-stu-id="4e36a-211">Next step</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4e36a-212">提交应用</span><span class="sxs-lookup"><span data-stu-id="4e36a-212">Submit your app</span></span>](https://docs.microsoft.com/office/dev/store/add-in-submission-guide)
