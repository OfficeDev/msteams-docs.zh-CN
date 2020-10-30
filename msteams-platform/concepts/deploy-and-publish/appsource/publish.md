---
title: Microsoft 团队应用程序审批提交过程指南
description: 介绍用于获取发布到 Microsoft 团队应用商店的应用程序的提交审批过程
keywords: 团队发布 microsoft store office 发布发布 AppSource 合作伙伴中心帐户验证应用帐户未发布资格
ms.openlocfilehash: 2879717aebd9d295cdf37cc0371b68f5f695b86b
ms.sourcegitcommit: 3fc7ad33e2693f07170c3cb1a0d396261fc5c619
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 10/29/2020
ms.locfileid: "48796307"
---
# <a name="submit-your-app-to-appsource"></a><span data-ttu-id="1c4bd-104">将您的应用程序提交到 AppSource</span><span class="sxs-lookup"><span data-stu-id="1c4bd-104">Submit your app to AppSource</span></span>

## <a name="teams-app-submission"></a><span data-ttu-id="1c4bd-105">团队应用程序提交</span><span class="sxs-lookup"><span data-stu-id="1c4bd-105">Teams app submission</span></span>

<span data-ttu-id="1c4bd-106">将应用程序发布到 [AppSource](https://appsource.microsoft.com) 使其在团队应用程序目录和 web 上可用。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-106">Publishing  your app to [AppSource](https://appsource.microsoft.com) makes it available in the Teams app catalog and on the web.</span></span> <span data-ttu-id="1c4bd-107">从较高的层次来看，将应用程序提交到 AppSource 的过程如下：</span><span class="sxs-lookup"><span data-stu-id="1c4bd-107">At a high level, the process for submitting your app to AppSource is:</span></span>

1. <span data-ttu-id="1c4bd-108">遵循我们的 [设计准则](~/concepts/design/understand-use-cases.md)来开发您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-108">Develop your app following our [design guidelines](~/concepts/design/understand-use-cases.md).</span></span> <span data-ttu-id="1c4bd-109">选项卡应遵循我们的 [选项卡设计准则](~/tabs/design/tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-109">Tabs should follow our [tab design guidelines](~/tabs/design/tabs.md).</span></span> <span data-ttu-id="1c4bd-110">Bot 应遵循 [bot 设计指南](~/bots/design/bots.md)。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-110">Bots should follow the [bot design guidelines](~/bots/design/bots.md).</span></span>
1. <span data-ttu-id="1c4bd-111">确保您的应用程序符合 Microsoft 团队的应用程序 [验证策略](/legal/marketplace/certification-policies) 。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-111">Ensure your app meets the app [validation policies](/legal/marketplace/certification-policies) for Microsoft Teams.</span></span> 
1. <span data-ttu-id="1c4bd-112">使用 [清单验证工具](https://docs.microsoft.com/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/submission-checklist#teams-app-validation-tool) 自我测试您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-112">Self test your app with the [Manifest validation tool](https://docs.microsoft.com/microsoftteams/platform/concepts/deploy-and-publish/appsource/prepare/submission-checklist#teams-app-validation-tool) .</span></span>
1. <span data-ttu-id="1c4bd-113">在 "[合作伙伴中心](https://support.microsoft.com/help/4499930/partner-center-overview)" 中[设置开发人员帐户](/office/dev/store/open-a-developer-account)。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-113">[Set up a developer account](/office/dev/store/open-a-developer-account) in [Partner Center](https://support.microsoft.com/help/4499930/partner-center-overview).</span></span> <span data-ttu-id="1c4bd-114">另 *请参阅* 下面的 FAQ 部分中的 [如何创建合作伙伴中心帐户](#how-do-i-create-a-partner-center-account)。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-114">*See also* [How do I create a Partner Center account](#how-do-i-create-a-partner-center-account) in the FAQ section, below.</span></span>
1. <span data-ttu-id="1c4bd-115">按照 [提交清单](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)，准备要提交的应用程序。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-115">Prepare your app for submission by following our [submission checklist](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).</span></span>
1. <span data-ttu-id="1c4bd-116">查看我们 [关于成功提交应用程序的提示](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-116">Review our [tips for a successful app submission](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md).</span></span>
1. <span data-ttu-id="1c4bd-117">[通过合作伙伴中心](/office/dev/store/use-partner-center-to-submit-to-appsource)将您的包提交到 AppSource。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-117">Submit your package to [AppSource through Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource).</span></span>
1. <span data-ttu-id="1c4bd-118">跟踪合作伙伴中心仪表板上的审批流程。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-118">Track the approval process on your Partner Center dashboard.</span></span> <span data-ttu-id="1c4bd-119">*请参阅*[合作伙伴中心概述](https://support.microsoft.com/help/4499930/partner-center-overview)。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-119">*See* [Partner Center Overview](https://support.microsoft.com/help/4499930/partner-center-overview).</span></span>
1. <span data-ttu-id="1c4bd-120">提交后提交—查看有关 [维护和支持您发布的应用程序](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)的指南。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-120">Post submission — review our guidance for [Maintaining and supporting your published app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md).</span></span>

>[!NOTE]
>
>- <span data-ttu-id="1c4bd-121">如果您的团队应用程序包含 bot，则必须遵守 Bot 开发人员框架 [行为准则](https://aka.ms/bf-conduct)。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-121">If your Teams app contains a bot, you must comply with the Bot Developer Framework [Code of Conduct](https://aka.ms/bf-conduct).</span></span>
>- <span data-ttu-id="1c4bd-122">如果您的应用程序包含 Office 365 连接器，可能会应用其他条款。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-122">If your app contains an Office 365 Connector, additional terms may apply.</span></span> <span data-ttu-id="1c4bd-123">*请参阅*[连接器开发人员仪表板](https://aka.ms/connectorsdashboard)和 [应用程序开发人员协议](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm)。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-123">*See* [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard) and [App Developer Agreement](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm).</span></span>
>- <span data-ttu-id="1c4bd-124">若要使您的应用程序可供 GCC 用户使用，并在存储中避免出现重复的应用程序列表，则身份验证进程/流应标识用户并将其传送到适用于 GCC 用户的指定/预期内容 URL。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-124">To make your app available for GCC users and avoid duplicate app listings in the store, the auth process/flow should identify and route the user to the specified/expected content URL for GCC users.</span></span>

## <a name="faqs--teams-apps-and-partner-account-verification-process-in-partner-center"></a><span data-ttu-id="1c4bd-125">Faq —合作伙伴中心的团队应用和合作伙伴帐户验证流程</span><span class="sxs-lookup"><span data-stu-id="1c4bd-125">FAQs — Teams apps and Partner account verification process in Partner Center</span></span>

## <a name="how-do-i-create-a-partner-center-account"></a><span data-ttu-id="1c4bd-126">如何创建合作伙伴中心帐户？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-126">How do I create a Partner Center account?</span></span>

<span data-ttu-id="1c4bd-127">有两种创建合作伙伴中心帐户的方法：</span><span class="sxs-lookup"><span data-stu-id="1c4bd-127">There are two ways to create a Partner Center account:</span></span>

- <span data-ttu-id="1c4bd-128">如果你不熟悉合作伙伴中心，并且在 Microsoft 网络中没有帐户，请 [使用 "合作伙伴中心注册" 页创建帐户](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-128">If you're new to Partner Center and don't have an account  within the Microsoft network, [create an account using the Partner Center enrollment page](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment).</span></span>
- <span data-ttu-id="1c4bd-129">如果你已在合作伙伴网络中注册，请 [使用现有注册直接在合作伙伴中心中创建帐户](/office/dev/store/)。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-129">If you're already enrolled in the Partner Network, [create an account directly in Partner Center using an existing enrollment](/office/dev/store/).</span></span>

## <a name="what-if-i-cannot-find-my-office-store-account-in-partner-center"></a><span data-ttu-id="1c4bd-130">如果我无法在合作伙伴中心找到我的 Office 应用商店帐户，该怎么办？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-130">What if I cannot find my Office Store account in Partner Center?</span></span>

<span data-ttu-id="1c4bd-131">请打开 [合作伙伴中心支持票证](https://partner.microsoft.com/support/v2/?stage=1) ，然后从下拉菜单中选择以下内容：</span><span class="sxs-lookup"><span data-stu-id="1c4bd-131">Please open a [Partner Center support ticket](https://partner.microsoft.com/support/v2/?stage=1) and select the following from the drop-down menus:</span></span>

| <span data-ttu-id="1c4bd-132">菜单</span><span class="sxs-lookup"><span data-stu-id="1c4bd-132">Menu</span></span> | <span data-ttu-id="1c4bd-133">选项</span><span class="sxs-lookup"><span data-stu-id="1c4bd-133">Option</span></span> |
| -------   | -------  |
|<span data-ttu-id="1c4bd-134">类别</span><span class="sxs-lookup"><span data-stu-id="1c4bd-134">Category</span></span>| <span data-ttu-id="1c4bd-135">商业市场</span><span class="sxs-lookup"><span data-stu-id="1c4bd-135">Commercial Marketplace</span></span>|
| <span data-ttu-id="1c4bd-136">主题</span><span class="sxs-lookup"><span data-stu-id="1c4bd-136">Topic</span></span> | <span data-ttu-id="1c4bd-137">常规市场帮助和操作方法问题</span><span class="sxs-lookup"><span data-stu-id="1c4bd-137">General Marketplace Help and How-to questions</span></span> |
| <span data-ttu-id="1c4bd-138">子</span><span class="sxs-lookup"><span data-stu-id="1c4bd-138">Subtopic</span></span>| <span data-ttu-id="1c4bd-139">Office 加载项</span><span class="sxs-lookup"><span data-stu-id="1c4bd-139">Office add-in</span></span> |

## <a name="where-can-i-get-support-for-my-partner-center-account-issues"></a><span data-ttu-id="1c4bd-140">在哪里可以获得对我的合作伙伴中心帐户问题的支持？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-140">Where can I get support for my Partner Center account issues?</span></span>

<span data-ttu-id="1c4bd-141">请访问我们的 [发布者支持页面](https://aka.ms/marketplacepublishersupport) 以搜索你的问题主题并查找指南。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-141">Please visit our [publishers support page](https://aka.ms/marketplacepublishersupport) to search for your issue topic and find guidance.</span></span> <span data-ttu-id="1c4bd-142">如果提供的指南不起作用，请 [打开合作伙伴中心支持票证](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-142">If the provided guidance is not helpful, [open a Partner Center support ticket](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket).</span></span>

## <a name="how-do-i-manage-my-office-store-account-in-partner-center"></a><span data-ttu-id="1c4bd-143">如何在合作伙伴中心管理我的 Office 应用商店帐户？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-143">How do I manage my Office Store account in Partner Center?</span></span>

<span data-ttu-id="1c4bd-144">若要了解如何通过合作伙伴中心管理 Office 应用商店帐户，请访问 "  [合作伙伴中心" 中的 "管理你的 Office 应用商店帐户](/office/dev/store/manage-account-settings-and-profile) "。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-144">Please visit our  [Manage your Office Store account in Partner Center](/office/dev/store/manage-account-settings-and-profile) for guidance on managing your Office Store account through Partner Center.</span></span>

## <a name="how-do-i-add-my-phone-number-to-the-partner-profile-contact-section"></a><span data-ttu-id="1c4bd-145">如何将我的电话号码添加到合作伙伴配置文件联系人部分？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-145">How do I add my phone number to the partner profile contact section?</span></span>

<span data-ttu-id="1c4bd-146">电话号码包含三个部分：国家/地区代码、区号和电话号码。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-146">The phone number has three parts — country code, area code, and the telephone number.</span></span> <span data-ttu-id="1c4bd-147">如果你的电话号码不包含区号，则将第二个框留空，然后完成第三个框。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-147">If your phone number doesn't include an area code, then leave the second box empty, and complete the third box.</span></span>

## <a name="how-do-i-manage-my-account-settings-and-partner-profile-in-partner-center"></a><span data-ttu-id="1c4bd-148">如何在合作伙伴中心管理我的帐户设置和合作伙伴配置文件？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-148">How do I manage my account settings and partner profile in Partner Center?</span></span>

<span data-ttu-id="1c4bd-149">有关管理合作伙伴中心帐户设置的指南，请访问我们的 " [管理帐户设置和配置文件信息](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) " 页面。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-149">Please visit our [Manage account settings and profile info](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) page for guidance on managing your Partner Center account settings.</span></span>

## <a name="why-do-i-receive-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a><span data-ttu-id="1c4bd-150">为什么我会收到邮件：当我尝试通过合作伙伴中心提交我的加载项时，"此帐户未发布合格"。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-150">Why do I receive the message, "This account is not publish eligible," when I try to submit my add-in through Partner Center?</span></span>

<span data-ttu-id="1c4bd-151">当您的 [帐户验证状态](/partner-center/verification-responses) 为 "挂起" 时，您将收到上述错误消息。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-151">You'll receive the above error message when your [account verification status](/partner-center/verification-responses) is pending.</span></span> <span data-ttu-id="1c4bd-152">您可以在 "合作伙伴中心" [仪表板](https://partner.microsoft.com/dashboard)中通过选择 " **设置** " 选项 ("齿轮" 图标) 在页面页眉命令行管理程序的右上角，然后选择 " **开发人员设置** " 帐户 "帐户  =>  **Account**   =>  **设置** " 来检查您的帐户验证状态。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-152">You can check your account verification status in the Partner Center [dashboard](https://partner.microsoft.com/dashboard) by selecting the **Settings** option (the gear icon) in the upper-right corner of the page header shell and choosing **Developer settings** => **Account**  => **Account settings** .</span></span>

![合作伙伴中心帐户设置页](../../../assets/images/partner-center-accts-page.png)

![合作伙伴中心验证状态](../../../assets/images/partner-center-verification-status.png)

<span data-ttu-id="1c4bd-155">在帐户验证过程中，将显示每个所需步骤的状态（电子邮件所有权、雇用验证和商业验证）。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-155">During the account verification process the status of each required step —  Email Ownership, Employment Verification, and Business Verification — will be displayed.</span></span> <span data-ttu-id="1c4bd-156">成功完成验证过程后，配置文件页上的注册的验证状态将从 "挂起" 更改为 "已授权"，并且不会再显示进程步骤。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-156">Once the verification process has been successfully completed, the verification status of your enrollment on the profile page will change from "pending" to "authorized," and the process steps will no longer be displayed.</span></span>

![合作伙伴中心验证错误](../../../assets/images/partner-center-acct-verification-error.png)

## <a name="what-is-verified-in-partner-center-account-verification-process-and-how-to-respond"></a><span data-ttu-id="1c4bd-158">合作伙伴中心帐户验证过程中验证了哪些内容以及如何进行响应？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-158">What is verified in Partner Center account verification process and how to respond?</span></span>
<span data-ttu-id="1c4bd-159">有三个验证区域-电子邮件所有权、雇用和业务。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-159">There are three verification areas - Email Ownership, Employment and Business.</span></span> <span data-ttu-id="1c4bd-160">如果你是主要联系人 (全局管理员 "或" 帐户管理员 ") ，请查看已验证内容的详细信息 [以及如何响应](/partner-center/verification-responses#what-is-verified-and-how-to-respond) 。我们建议你转到合作伙伴配置文件以监视验证状态并跟踪进度。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-160">Please see the details of [What is verified and how to respond](/partner-center/verification-responses#what-is-verified-and-how-to-respond) If you are the primary contact (Global admin or Account admin), we recommend that you go to your Partner Profile to monitor verification status and track progress.</span></span>

<span data-ttu-id="1c4bd-161">验证过程完成后，配置文件页面上的注册的验证状态将从 " *待定* " 更改为 "已 *授权* "，并且在该页面上显示的 "进程步骤" 状态将消失。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-161">Once the verification process is complete, the verification status of your enrollment on the profile page will change from *pending* to *authorized* and the process steps with status, displayed on that page, will disappear.</span></span> <span data-ttu-id="1c4bd-162">主要联系人会在验证完成后的几个工作日内收到来自 Microsoft 的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-162">The primary contact will receive an email from Microsoft within a few business days after the verification is completed.</span></span>

## <a name="my-account-verification-status-has-not-advanced-beyond-email-ownership-in-partner-center-how-should-i-proceed"></a><span data-ttu-id="1c4bd-163">我的帐户验证状态除了合作伙伴中心的电子邮件所有权之外，尚未提前。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-163">My account Verification status has not advanced beyond Email Ownership in Partner Center.</span></span> <span data-ttu-id="1c4bd-164">我应该如何继续？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-164">How should I proceed?</span></span>

<span data-ttu-id="1c4bd-165">在 **电子邮件所有权** 验证过程中，会将验证电子邮件发送到主要联系人电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-165">During the **Email Ownership** verification process, a verification email is sent to the primary contact email address.</span></span> <span data-ttu-id="1c4bd-166">请检查主要联系人收件箱中是否有需要主题行操作的电子邮件 **maccount@ <span>microsoft</span>.Com** *：使用 microsoft 验证您的电子邮件帐户* ，请求您完成电子邮件验证过程。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-166">Please check your primary contact inbox for an email  from **maccount@ <span>microsoft</span>.com** with the subject  line *Action needed: Verify your email account with Microsoft* , requesting that you complete the email verification process.</span></span> <span data-ttu-id="1c4bd-167">验证电子邮件将发送到合作伙伴中心的 "帐户设置" 页上列出的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-167">The verification email will be sent to the email address listed  in your account settings page in Partner Center.</span></span>

> [!NOTE]
 ><span data-ttu-id="1c4bd-168">电子邮件验证链接仅在7天内有效。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-168">The email verification link is only valid for 7 days.</span></span> <span data-ttu-id="1c4bd-169">你可以通过访问合作伙伴配置文件页面并选择 " **重新发送验证电子邮件** " 链接，请求重新向你发送电子邮件。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-169">You can request that we resend the email to you by visiting your partner profile page and selecting the **Resend verification email** link.</span></span> <span data-ttu-id="1c4bd-170">若要确保收到电子邮件，请将安全列表电子邮件从 microsoft.com 为安全域，并检查 "垃圾邮件" 文件夹。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-170">To ensure that the email is received, safelist email from microsoft.com as a secure domain, and check your junk email folders.</span></span>

## <a name="how-i-do-get-further-support-for-my-account-related-issues"></a><span data-ttu-id="1c4bd-171">如何获取对与我的帐户相关的问题的进一步支持？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-171">How I do get further support for my account related issues?</span></span>

<span data-ttu-id="1c4bd-172">若要了解如何创建支持票证，请访问 [合作伙伴中心计划中的商业市场计划的支持人员](/azure/marketplace/partner-center-portal/support) 和步骤。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-172">Please visit our [Support for the Commercial Marketplace program in Partner Center](/azure/marketplace/partner-center-portal/support) page for guidance and steps to create a support ticket.</span></span>

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what--should-i-do-next"></a><span data-ttu-id="1c4bd-173">我已检查我的邮件文件夹，但尚未收到验证电子邮件。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-173">I've checked my mail folders and haven't received the verification email.</span></span> <span data-ttu-id="1c4bd-174">接下来我该怎么办？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-174">What  should I do next?</span></span>

<span data-ttu-id="1c4bd-175">请尝试以下操作：</span><span class="sxs-lookup"><span data-stu-id="1c4bd-175">Please try the following:</span></span>

1. <span data-ttu-id="1c4bd-176">检查您的垃圾邮件文件夹。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-176">Check your junk/spam folder.</span></span>
1. <span data-ttu-id="1c4bd-177">清除浏览器缓存，转到合作伙伴中心帐户仪表板，然后选择 " **重新发送验证电子邮件** " 链接，将验证电子邮件发送到您的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-177">Clear the browser cache, go to your Partner Center account dashboard, and select  the **Resend verification email** link to have the verification email resent to your email address.</span></span>
1. <span data-ttu-id="1c4bd-178">尝试从其他浏览器访问  **重新发送验证电子邮件** 链接。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-178">Try accessing the  **Resend verification email** link  from a different browser.</span></span>
1. <span data-ttu-id="1c4bd-179">与 IT 部门合作，以确保电子邮件服务器不会阻止验证电子邮件。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-179">Work with your IT department to ensure that the verification emails are not blocked by the email server.</span></span>
1. <span data-ttu-id="1c4bd-180">调整您的服务器的垃圾邮件筛选器，以允许/通过 maccount@microsoft 的所有电子邮件进行安全列表 **。 <span></span>com** 。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-180">Adjust your server's spam filter to allow/safelist all emails from **maccount@microsoft.<span></span>com** .</span></span>

## <a name="how-long-does-the-employment-verification-process-usually-take"></a><span data-ttu-id="1c4bd-181">雇用验证过程通常需要多长时间？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-181">How long does the employment verification process usually take?</span></span>

<span data-ttu-id="1c4bd-182">如果所有提交的详细信息都是正确的，则雇用验证将在1到2小时内完成。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-182">If all the submitted details are correct, employment verification completes in 1 to 2 hours.</span></span>

## <a name="how-long-does-the-business-verification-process-usually-take"></a><span data-ttu-id="1c4bd-183">"业务验证" 过程通常需要多长时间？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-183">How long does the “Business Verification” process usually take?</span></span>

<span data-ttu-id="1c4bd-184">业务验证需要1到2个工作日才能完成，只要提交了所有必需的文档。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-184">Business Verification takes 1 to 2 business days to complete, provided that all required documents have been submitted.</span></span>

## <a name="if-i-reach-out-to-the-support-team-will-my-ticket-be-expedited"></a><span data-ttu-id="1c4bd-185">如果我转到支持团队，我的票证将会加快吗？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-185">If I reach out to the support team, will my ticket be expedited?</span></span>

<span data-ttu-id="1c4bd-186">支持票证将在一周内得到解决。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-186">Support tickets will be resolved within a week's time.</span></span> <span data-ttu-id="1c4bd-187">请查找将发送到在发出支持票证时提供的电子邮件的更新。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-187">Please look for the updates which will be sent to the email provided when the support ticket was raised.</span></span>

## <a name="my-issue-is-not-listed-here--are-there-other-pages-i-can-reference-for-partner-center-issues"></a><span data-ttu-id="1c4bd-188">我的问题未在此处列出。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-188">My issue is not listed here.</span></span>  <span data-ttu-id="1c4bd-189">是否有其他页面可供我参考以获取合作伙伴中心问题？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-189">Are there other pages I can reference for Partner Center issues?</span></span>

<span data-ttu-id="1c4bd-190">请参阅我们的 [商业市场文档](/azure/marketplace/) 以获取更多帮助。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-190">Please refer to our [commercial marketplace documentation](/azure/marketplace/) for more help.</span></span>

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a><span data-ttu-id="1c4bd-191">我已经创建了一个支持票证，它已有7个工作日，但尚未收到更新。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-191">I've created a support ticket, it has been 7 business days, and I haven't received an update.</span></span> <span data-ttu-id="1c4bd-192">在哪里可以获得更多帮助？</span><span class="sxs-lookup"><span data-stu-id="1c4bd-192">Where can I get additional help?</span></span>

<span data-ttu-id="1c4bd-193">请 **<teamsubm@microsoft.com>** 使用以下详细信息发送电子邮件：</span><span class="sxs-lookup"><span data-stu-id="1c4bd-193">Please send an email to **<teamsubm@microsoft.com>** with the following details:</span></span>

1. <span data-ttu-id="1c4bd-194">**主题行** 。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-194">**Subject Line** .</span></span> <span data-ttu-id="1c4bd-195">*<App_Name>的合作伙伴中心帐户问题* (指定您的应用程序) 的名称。</span><span class="sxs-lookup"><span data-stu-id="1c4bd-195">*Partner Center Account Issue for <App_Name>* (specify the name of your app).</span></span>
1. <span data-ttu-id="1c4bd-196">**电子邮件正文：**</span><span class="sxs-lookup"><span data-stu-id="1c4bd-196">**Email body:**</span></span>
    * <span data-ttu-id="1c4bd-197">支持票证号码：</span><span class="sxs-lookup"><span data-stu-id="1c4bd-197">Support ticket number:</span></span>
    * <span data-ttu-id="1c4bd-198">卖家 ID：</span><span class="sxs-lookup"><span data-stu-id="1c4bd-198">Your seller ID:</span></span>
    * <span data-ttu-id="1c4bd-199"> (的问题的屏幕截图（如果可能）) ：</span><span class="sxs-lookup"><span data-stu-id="1c4bd-199">A screen shot of the issue (if possible):</span></span>

>
> [!div class="nextstepaction"]
> [<span data-ttu-id="1c4bd-200">了解有关 Microsoft 团队的应用验证策略的详细信息</span><span class="sxs-lookup"><span data-stu-id="1c4bd-200">Learn more about app validation policies for Microsoft Teams</span></span>](/legal/marketplace/certification-policies)
