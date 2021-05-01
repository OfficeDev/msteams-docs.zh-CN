---
title: 解决应用商店提交问题
description: 了解如何排查并更正你的应用商店Microsoft Teams问题。
ms.topic: how-to
author: heath-hamilton
ms.author: surbhigupta
ms.openlocfilehash: 847534c68d013566e4bfbe0e5a1bbbe92e36e63e
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101883"
---
# <a name="resolve-issues-if-your-microsoft-teams-store-submission-fails"></a><span data-ttu-id="7f25f-103">解决应用商店提交Microsoft Teams时的问题</span><span class="sxs-lookup"><span data-stu-id="7f25f-103">Resolve issues if your Microsoft Teams store submission fails</span></span>

<span data-ttu-id="7f25f-104">发布到应用商店Microsoft Teams应用必须满足Teams[验证](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md)准则和商业市场[策略](https://docs.microsoft.com/legal/marketplace/certification-policies)。</span><span class="sxs-lookup"><span data-stu-id="7f25f-104">Apps published to the Microsoft Teams store must meet the [Teams store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) and [commercial marketplace policies](https://docs.microsoft.com/legal/marketplace/certification-policies).</span></span>

<span data-ttu-id="7f25f-105">如果你的应用商店提交失败，Microsoft 将提供一个验证验证服务，以帮助使你的应用合规并发布。</span><span class="sxs-lookup"><span data-stu-id="7f25f-105">If your store submission fails, Microsoft provides a concierge validation service to help get your app compliant and published.</span></span>

## <a name="get-help-directly-from-microsoft"></a><span data-ttu-id="7f25f-106">直接从 Microsoft 获取帮助</span><span class="sxs-lookup"><span data-stu-id="7f25f-106">Get help directly from Microsoft</span></span>

<span data-ttu-id="7f25f-107">Microsoft 提供的验证服务可帮助开发人员将应用发布到应用商店Teams商店。</span><span class="sxs-lookup"><span data-stu-id="7f25f-107">The concierge validation service provided by Microsoft helps developers get their apps published to the Teams store.</span></span> <span data-ttu-id="7f25f-108">作为此服务的一部分，Microsoft 会验证你的应用是否正常工作，是否包含所有适当的元数据，并为用户提供价值。</span><span class="sxs-lookup"><span data-stu-id="7f25f-108">As part of this service, Microsoft verifies if your app works as described, contains all appropriate metadata, and provides value to users.</span></span>

<span data-ttu-id="7f25f-109">如果应用提交失败，Microsoft 在提交后 24 小时内会向您发送评价报告和建议。</span><span class="sxs-lookup"><span data-stu-id="7f25f-109">If your app submission fails, Microsoft sends you a review report with recommendations within 24 hours of submission.</span></span>

## <a name="resolve-issues-and-resubmit-your-app"></a><span data-ttu-id="7f25f-110">解决问题并重新提交应用</span><span class="sxs-lookup"><span data-stu-id="7f25f-110">Resolve issues and resubmit your app</span></span>

<span data-ttu-id="7f25f-111">必须先修复 Microsoft 验证团队报告的所有问题，然后才能在合作伙伴中心重新提交应用。</span><span class="sxs-lookup"><span data-stu-id="7f25f-111">You must fix all issues reported by the Microsoft concierge validation team before resubmitting your app on Partner Center.</span></span> <span data-ttu-id="7f25f-112">Microsoft 报告包含以下信息：</span><span class="sxs-lookup"><span data-stu-id="7f25f-112">The Microsoft report includes the following information:</span></span>

* <span data-ttu-id="7f25f-113">针对 [每个问题](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) 的相应验证准则</span><span class="sxs-lookup"><span data-stu-id="7f25f-113">A corresponding [validation guideline](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) for each issue</span></span>
* <span data-ttu-id="7f25f-114">有关如何重现每个问题的说明</span><span class="sxs-lookup"><span data-stu-id="7f25f-114">Instructions on how to reproduce each issue</span></span>
* <span data-ttu-id="7f25f-115">推荐公开提供的开发人员文档解决每个问题</span><span class="sxs-lookup"><span data-stu-id="7f25f-115">Recommendations for resolving each issue based on publicly available developer documentation</span></span>

<span data-ttu-id="7f25f-116">解决问题并重新提交应用的过程通常如下所示：</span><span class="sxs-lookup"><span data-stu-id="7f25f-116">The process for resolving issues and resubmitting an app typically goes like this:</span></span>

1. <span data-ttu-id="7f25f-117">解决报告中的所有问题。</span><span class="sxs-lookup"><span data-stu-id="7f25f-117">You fix all issues in the report.</span></span>
1. <span data-ttu-id="7f25f-118">你可以将以下内容发送到 Microsoft 验证团队<a href="mailto:teamsubm@microsoft.com">，teamsubm@microsoft.com：</a></span><span class="sxs-lookup"><span data-stu-id="7f25f-118">You send the following to the Microsoft concierge validation team at <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>:</span></span>
   * <span data-ttu-id="7f25f-119">更新的应用包</span><span class="sxs-lookup"><span data-stu-id="7f25f-119">An updated app package</span></span>
   * <span data-ttu-id="7f25f-120">如果你未在原始提交 (，则应用测试说明) ：</span><span class="sxs-lookup"><span data-stu-id="7f25f-120">Test notes for your app (if you didn't include these in your original submission):</span></span>
      * <span data-ttu-id="7f25f-121">至少两个帐户的凭据 (一个管理员和非管理员帐户) </span><span class="sxs-lookup"><span data-stu-id="7f25f-121">Credentials for at least two accounts (one admin and one non-admin)</span></span>
      * <span data-ttu-id="7f25f-122">配置应用并测试其功能的说明</span><span class="sxs-lookup"><span data-stu-id="7f25f-122">Instructions to configure the app and test its functionality</span></span>
      * <span data-ttu-id="7f25f-123">显示应用程序中使用的应用Teams</span><span class="sxs-lookup"><span data-stu-id="7f25f-123">A video showing your app used in Teams</span></span>
1. <span data-ttu-id="7f25f-124">Microsoft 验证团队会全面测试更新后的应用。</span><span class="sxs-lookup"><span data-stu-id="7f25f-124">Microsoft concierge validation team fully tests your updated app.</span></span>
1. <span data-ttu-id="7f25f-125">执行下列操作之一：</span><span class="sxs-lookup"><span data-stu-id="7f25f-125">You do one of the following:</span></span>
   * <span data-ttu-id="7f25f-126">如果你的应用没有问题，请重新提交合作伙伴中心上的应用。</span><span class="sxs-lookup"><span data-stu-id="7f25f-126">If your app is free of issues, resubmit your app on Partner Center.</span></span>
   * <span data-ttu-id="7f25f-127">如果问题未解决或 Microsoft 发现新问题，您将收到另一个有关要修复问题的报告。</span><span class="sxs-lookup"><span data-stu-id="7f25f-127">If issues aren't resolved or Microsoft finds new issues, you receive another report on what to fix.</span></span> <span data-ttu-id="7f25f-128">解决这些问题，并将应用的更新版本发送到 teamsubm@microsoft.com <a href="mailto:teamsubm@microsoft.com">。</a></span><span class="sxs-lookup"><span data-stu-id="7f25f-128">Resolve those issues and send an updated version of the app to <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>.</span></span>

> [!CAUTION]
> <span data-ttu-id="7f25f-129">若要避免多个提交失败，请不要在 Microsoft 验证团队批准你的应用之前，在合作伙伴中心重新提交你的应用。</span><span class="sxs-lookup"><span data-stu-id="7f25f-129">To avoid multiple submission failures, do not resubmit your app on Partner Center until the Microsoft concierge validation team approves your app.</span></span>

## <a name="faq"></a><span data-ttu-id="7f25f-130">常见问题</span><span class="sxs-lookup"><span data-stu-id="7f25f-130">FAQ</span></span>

<span data-ttu-id="7f25f-131">在解决应用提交问题时，获取一些常见问题的解答。</span><span class="sxs-lookup"><span data-stu-id="7f25f-131">Get answers to some common questions when resolving app submission issues.</span></span>

<br>

<details>

<summary><span data-ttu-id="7f25f-132"><b>发布我的应用程序需要多久？</b></span><span class="sxs-lookup"><span data-stu-id="7f25f-132"><b>How long will it take to publish my app?</b></span></span></summary>

<span data-ttu-id="7f25f-133">如果你的应用商店提交没有问题，你的应用将在 1-2 个工作日内发布。</span><span class="sxs-lookup"><span data-stu-id="7f25f-133">If your store submission has no issues, your app will publish within 1-2 business days.</span></span> <span data-ttu-id="7f25f-134">如果应用失败，Microsoft 团队会提供修复问题的建议。</span><span class="sxs-lookup"><span data-stu-id="7f25f-134">If your app fails, a team from Microsoft provides you with recommendations to fix the issues.</span></span> <span data-ttu-id="7f25f-135">一旦进行这些修复，然后向该团队重新发送更新后的应用，如果应用已准备好发布或仍然需要更多工作，将在 24 小时内收到通知。</span><span class="sxs-lookup"><span data-stu-id="7f25f-135">Once you make those fixes and resend an updated app to that team, you will be notified in 24 hours if your app is ready to publish or still needs more work.</span></span>

<br>

</details>

<details>

<summary><span data-ttu-id="7f25f-136"><b>如何提高我的应用通过提交的可能性？</b></span><span class="sxs-lookup"><span data-stu-id="7f25f-136"><b>How do I increase the likelihood my app will pass submission?</b></span></span></summary>

<span data-ttu-id="7f25f-137">执行以下操作可能会导致成功提交：</span><span class="sxs-lookup"><span data-stu-id="7f25f-137">Doing the following can lead to a successful submission:</span></span>

1. <span data-ttu-id="7f25f-138">根据应用设计Teams[开发应用](~/concepts/design/design-teams-app-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="7f25f-138">Develop your app based on the [Teams design guidelines](~/concepts/design/design-teams-app-overview.md).</span></span>
1. <span data-ttu-id="7f25f-139">确保你的应用遵守应用商店验证[Teams](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) [Microsoft 商业市场认证策略](https://docs.microsoft.com/legal/marketplace/certification-policies)。</span><span class="sxs-lookup"><span data-stu-id="7f25f-139">Make sure your app adheres to the [Teams store validation guidelines](~/concepts/deploy-and-publish/appsource/prepare/teams-store-validation-guidelines.md) and [Microsoft commercial marketplace certification policies](https://docs.microsoft.com/legal/marketplace/certification-policies).</span></span>
1. <span data-ttu-id="7f25f-140">使用应用验证Microsoft Teams[测试应用包](https://dev.teams.microsoft.com/appvalidation.html)。</span><span class="sxs-lookup"><span data-stu-id="7f25f-140">Test your app package with the [Microsoft Teams app validation tool](https://dev.teams.microsoft.com/appvalidation.html).</span></span>
1. <span data-ttu-id="7f25f-141">[准备你的Teams提交](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="7f25f-141">[Prepare your Teams store submission](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).</span></span>

<br>

</details>

<details>

<summary><span data-ttu-id="7f25f-142"><b>我的应用已进行 beta 测试。我能否提交我的应用以节省发布过程的时间？</b></span><span class="sxs-lookup"><span data-stu-id="7f25f-142"><b>My app is in beta testing. Can I submit my app anyway to save time on the publishing process?</b></span></span></summary>

<span data-ttu-id="7f25f-143">否。</span><span class="sxs-lookup"><span data-stu-id="7f25f-143">No.</span></span> <span data-ttu-id="7f25f-144">Microsoft 仅验证生产就绪型应用。</span><span class="sxs-lookup"><span data-stu-id="7f25f-144">Microsoft only validates production-ready apps.</span></span>

<br>

</details>

<details>

<summary><span data-ttu-id="7f25f-145"><b>在合作伙伴中心 teamsubm@microsoft.com 提交我的应用之前，我可能需要联系客户吗？</b></span><span class="sxs-lookup"><span data-stu-id="7f25f-145"><b>May I contact the teamsubm@microsoft.com email before submitting my app for the first time on Partner Center?</b></span></span></summary>

<span data-ttu-id="7f25f-146">否。</span><span class="sxs-lookup"><span data-stu-id="7f25f-146">No.</span></span> <span data-ttu-id="7f25f-147">在合作伙伴中心首次提交应用之前，Microsoft 不会开始验证你的应用。</span><span class="sxs-lookup"><span data-stu-id="7f25f-147">Microsoft doesn't start validating your app until you submit your app for the first time on Partner Center.</span></span>

<br>

</details>

<details>

<summary><span data-ttu-id="7f25f-148"><b>我收到了一封来自合作伙伴中心的电子邮件，指出我的应用已批准发布。为什么我的应用不在应用商店Teams？</b></span><span class="sxs-lookup"><span data-stu-id="7f25f-148"><b>I received an email from Partner Center saying my app was approved to publish. Why isn't my app in the Teams store?</b></span></span></summary>

<span data-ttu-id="7f25f-149">应用获得批准后，发布通常需要 1-2 个工作日，具体取决于应用的功能。</span><span class="sxs-lookup"><span data-stu-id="7f25f-149">Once your app is approved, publishing usually takes 1-2 business days depending on the app's capabilities.</span></span><span data-ttu-id="7f25f-150">如果你的应用在两个工作日后尚未发布 <a href="mailto:teamsubm@microsoft.com">，请联系</a>teamsubm@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="7f25f-150"> If your app hasn't published after two business days, contact <a href="mailto:teamsubm@microsoft.com">teamsubm@microsoft.com</a>.</span></span>

<br>

</details>
