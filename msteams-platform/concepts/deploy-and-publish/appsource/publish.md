---
title: Microsoft Teams 应用审批提交流程指南
description: 介绍将应用发布到 Microsoft Teams 应用商店的提交审批过程
keywords: teams 发布应用商店 Office 发布发布 AppSource 合作伙伴中心帐户验证应用帐户未发布符合条件的
ms.openlocfilehash: 6268d408cc4c44633b9b3629c902044815639176
ms.sourcegitcommit: db19fee033b41152267bb524d67aee5b7f64b04a
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/12/2021
ms.locfileid: "49797480"
---
# <a name="submit-your-app-to-appsource"></a><span data-ttu-id="190ec-104">将应用提交到 AppSource</span><span class="sxs-lookup"><span data-stu-id="190ec-104">Submit your app to AppSource</span></span>

## <a name="teams-app-submission"></a><span data-ttu-id="190ec-105">Teams 应用提交</span><span class="sxs-lookup"><span data-stu-id="190ec-105">Teams app submission</span></span>

<span data-ttu-id="190ec-106">将应用发布到 [AppSource](https://appsource.microsoft.com) 使其在 Teams 应用目录和 Web 上可用。</span><span class="sxs-lookup"><span data-stu-id="190ec-106">Publishing  your app to [AppSource](https://appsource.microsoft.com) makes it available in the Teams app catalog and on the web.</span></span> <span data-ttu-id="190ec-107">在高级别上，将应用提交到 AppSource 的过程是：</span><span class="sxs-lookup"><span data-stu-id="190ec-107">At a high level, the process for submitting your app to AppSource is:</span></span>

1. <span data-ttu-id="190ec-108">按照设计指南开发 [应用](~/concepts/design/understand-use-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="190ec-108">Develop your app by following the [design guidelines](~/concepts/design/understand-use-cases.md).</span></span> <span data-ttu-id="190ec-109">选项卡必须遵循桌面、Web 和移动的选项卡[设计](~/tabs/design/tabs.md)[指南](~/tabs/design/tabs-mobile.md)。</span><span class="sxs-lookup"><span data-stu-id="190ec-109">Tabs must follow the tab design guidelines for both, [desktop and web](~/tabs/design/tabs.md) and [mobile](~/tabs/design/tabs-mobile.md).</span></span> <span data-ttu-id="190ec-110">机器人必须遵循机器人 [设计指南](~/bots/design/bots.md)。</span><span class="sxs-lookup"><span data-stu-id="190ec-110">Bots must follow the [bot design guidelines](~/bots/design/bots.md).</span></span>
1. <span data-ttu-id="190ec-111">确保你的应用符合 Microsoft Teams [的应用验证](/legal/marketplace/certification-policies) 策略。</span><span class="sxs-lookup"><span data-stu-id="190ec-111">Ensure your app meets the app [validation policies](/legal/marketplace/certification-policies) for Microsoft Teams.</span></span> 
1. <span data-ttu-id="190ec-112">使用清单验证工具 [自行测试你的应用](prepare/submission-checklist.md#teams-app-validation-tool) 。</span><span class="sxs-lookup"><span data-stu-id="190ec-112">Self test your app with the [Manifest validation tool](prepare/submission-checklist.md#teams-app-validation-tool) .</span></span>
1. <span data-ttu-id="190ec-113">[在合作伙伴中心中](/office/dev/store/open-a-developer-account) 设置 [开发人员帐户](https://support.microsoft.com/help/4499930/partner-center-overview)。</span><span class="sxs-lookup"><span data-stu-id="190ec-113">[Set up a developer account](/office/dev/store/open-a-developer-account) in [Partner Center](https://support.microsoft.com/help/4499930/partner-center-overview).</span></span> <span data-ttu-id="190ec-114">*另请参阅*[下面的常见问题部分中的](#how-do-i-create-a-partner-center-account)"如何创建合作伙伴中心帐户"。</span><span class="sxs-lookup"><span data-stu-id="190ec-114">*See also* [How do I create a Partner Center account](#how-do-i-create-a-partner-center-account) in the FAQ section, below.</span></span>
1. <span data-ttu-id="190ec-115">按照我们的提交清单准备应用 [进行提交](prepare/submission-checklist.md)。</span><span class="sxs-lookup"><span data-stu-id="190ec-115">Prepare your app for submission by following our [submission checklist](prepare/submission-checklist.md).</span></span>
1. <span data-ttu-id="190ec-116">查看 [失败最多的测试用例，以便更快地进行应用质量审批](prepare/frequently-failed-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="190ec-116">Review the [most failed test cases for a quicker app quality approval](prepare/frequently-failed-cases.md).</span></span>
1. <span data-ttu-id="190ec-117">通过合作伙伴中心将程序包[提交到 AppSource。](/office/dev/store/use-partner-center-to-submit-to-appsource)</span><span class="sxs-lookup"><span data-stu-id="190ec-117">Submit your package to [AppSource through Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource).</span></span>
1. <span data-ttu-id="190ec-118">在合作伙伴中心仪表板上跟踪审批流程。</span><span class="sxs-lookup"><span data-stu-id="190ec-118">Track the approval process on your Partner Center dashboard.</span></span> <span data-ttu-id="190ec-119">*请参阅*[合作伙伴中心概述](https://support.microsoft.com/help/4499930/partner-center-overview)。</span><span class="sxs-lookup"><span data-stu-id="190ec-119">*See* [Partner Center Overview](https://support.microsoft.com/help/4499930/partner-center-overview).</span></span>
1. <span data-ttu-id="190ec-120">提交后 — 查看有关 [维护和支持已发布应用的指南](post-publish/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="190ec-120">Post submission — review our guidance for [Maintaining and supporting your published app](post-publish/overview.md).</span></span>

>[!NOTE]
>
>- <span data-ttu-id="190ec-121">你的 Teams 应用必须是移动响应式应用，并且符合 [iOS](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment) 和 Android (移动操作系统上的) 。</span><span class="sxs-lookup"><span data-stu-id="190ec-121">Your Teams app must be mobile responsive and comply with [no upsell requirements](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md#-mobile-responsiveness-no-direct-upsell-or-payment) on mobile OS (iOS and Android).</span></span> 
>- <span data-ttu-id="190ec-122">如果你的 Teams 应用包含机器人，你必须遵守 Bot 开发人员框架 [行为准则](https://aka.ms/bf-conduct)。</span><span class="sxs-lookup"><span data-stu-id="190ec-122">If your Teams app contains a bot, you must comply with the Bot Developer Framework [Code of Conduct](https://aka.ms/bf-conduct).</span></span>
>- <span data-ttu-id="190ec-123">如果你的应用包含 Office 365 连接器，则其他条款可能适用。</span><span class="sxs-lookup"><span data-stu-id="190ec-123">If your app contains an Office 365 Connector, additional terms may apply.</span></span> <span data-ttu-id="190ec-124">*请参阅*[连接器开发人员仪表板](https://aka.ms/connectorsdashboard)[和应用开发人员协议](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm)。</span><span class="sxs-lookup"><span data-stu-id="190ec-124">*See* [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard) and [App Developer Agreement](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm).</span></span>
>- <span data-ttu-id="190ec-125">若要使应用可供 GCC 用户使用，并避免应用商店中出现重复的应用列表，身份验证过程/流应标识用户，并让用户路由到 GCC 用户的指定/预期内容 URL。</span><span class="sxs-lookup"><span data-stu-id="190ec-125">To make your app available for GCC users and avoid duplicate app listings in the store, the auth process/flow should identify and route the user to the specified/expected content URL for GCC users.</span></span>

## <a name="faqs--teams-apps-and-partner-account-verification-process-in-partner-center"></a><span data-ttu-id="190ec-126">常见问题解答 — 合作伙伴中心中的 Teams 应用和合作伙伴帐户验证过程</span><span class="sxs-lookup"><span data-stu-id="190ec-126">FAQs — Teams apps and Partner account verification process in Partner Center</span></span>

## <a name="how-do-i-create-a-partner-center-account"></a><span data-ttu-id="190ec-127">如何创建合作伙伴中心帐户？</span><span class="sxs-lookup"><span data-stu-id="190ec-127">How do I create a Partner Center account?</span></span>

<span data-ttu-id="190ec-128">创建合作伙伴中心帐户的方法有两种：</span><span class="sxs-lookup"><span data-stu-id="190ec-128">There are two ways to create a Partner Center account:</span></span>

- <span data-ttu-id="190ec-129">如果你是合作伙伴中心的新用户，并且 Microsoft 网络内没有帐户，则使用合作伙伴中心注册 [页面创建一个帐户](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)。</span><span class="sxs-lookup"><span data-stu-id="190ec-129">If you're new to Partner Center and don't have an account  within the Microsoft network, [create an account using the Partner Center enrollment page](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment).</span></span>
- <span data-ttu-id="190ec-130">如果你已在合作伙伴网络中注册，请直接使用现有注册在合作伙伴 [中心创建帐户](/office/dev/store/)。</span><span class="sxs-lookup"><span data-stu-id="190ec-130">If you're already enrolled in the Partner Network, [create an account directly in Partner Center using an existing enrollment](/office/dev/store/).</span></span>

## <a name="what-if-i-cannot-find-my-office-store-account-in-partner-center"></a><span data-ttu-id="190ec-131">如果我在合作伙伴中心中找不到我的 Office 应用商店帐户，如何？</span><span class="sxs-lookup"><span data-stu-id="190ec-131">What if I cannot find my Office Store account in Partner Center?</span></span>

<span data-ttu-id="190ec-132">请打开 [合作伙伴中心支持票证](https://partner.microsoft.com/support/v2/?stage=1) ，然后从下拉菜单中选择以下内容：</span><span class="sxs-lookup"><span data-stu-id="190ec-132">Please open a [Partner Center support ticket](https://partner.microsoft.com/support/v2/?stage=1) and select the following from the drop-down menus:</span></span>

| <span data-ttu-id="190ec-133">菜单</span><span class="sxs-lookup"><span data-stu-id="190ec-133">Menu</span></span> | <span data-ttu-id="190ec-134">选项</span><span class="sxs-lookup"><span data-stu-id="190ec-134">Option</span></span> |
| -------   | -------  |
|<span data-ttu-id="190ec-135">类别</span><span class="sxs-lookup"><span data-stu-id="190ec-135">Category</span></span>| <span data-ttu-id="190ec-136">商业市场</span><span class="sxs-lookup"><span data-stu-id="190ec-136">Commercial Marketplace</span></span>|
| <span data-ttu-id="190ec-137">主题</span><span class="sxs-lookup"><span data-stu-id="190ec-137">Topic</span></span> | <span data-ttu-id="190ec-138">一般市场帮助和帮助问题</span><span class="sxs-lookup"><span data-stu-id="190ec-138">General Marketplace Help and How-to questions</span></span> |
| <span data-ttu-id="190ec-139">子标题</span><span class="sxs-lookup"><span data-stu-id="190ec-139">Subtopic</span></span>| <span data-ttu-id="190ec-140">Office 加载项</span><span class="sxs-lookup"><span data-stu-id="190ec-140">Office add-in</span></span> |

## <a name="where-can-i-get-support-for-my-partner-center-account-issues"></a><span data-ttu-id="190ec-141">在哪里可以获取对合作伙伴中心帐户问题的支持？</span><span class="sxs-lookup"><span data-stu-id="190ec-141">Where can I get support for my Partner Center account issues?</span></span>

<span data-ttu-id="190ec-142">请访问我们的 [发布者支持页面](https://aka.ms/marketplacepublishersupport) ，搜索你的问题主题并查找指南。</span><span class="sxs-lookup"><span data-stu-id="190ec-142">Please visit our [publishers support page](https://aka.ms/marketplacepublishersupport) to search for your issue topic and find guidance.</span></span> <span data-ttu-id="190ec-143">如果提供的指南没有帮助， [请打开合作伙伴中心支持票证](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket)。</span><span class="sxs-lookup"><span data-stu-id="190ec-143">If the provided guidance is not helpful, [open a Partner Center support ticket](/azure/marketplace/partner-center-portal/support#how-to-open-a-support-ticket).</span></span>

## <a name="how-do-i-manage-my-office-store-account-in-partner-center"></a><span data-ttu-id="190ec-144">如何在合作伙伴中心管理我的 Office 应用商店帐户？</span><span class="sxs-lookup"><span data-stu-id="190ec-144">How do I manage my Office Store account in Partner Center?</span></span>

<span data-ttu-id="190ec-145">请访问合作伙伴  [中心中的](/office/dev/store/manage-account-settings-and-profile) 管理 Office 应用商店帐户，获得通过合作伙伴中心管理 Office 应用商店帐户的指南。</span><span class="sxs-lookup"><span data-stu-id="190ec-145">Please visit our  [Manage your Office Store account in Partner Center](/office/dev/store/manage-account-settings-and-profile) for guidance on managing your Office Store account through Partner Center.</span></span>

## <a name="how-do-i-add-my-phone-number-to-the-partner-profile-contact-section"></a><span data-ttu-id="190ec-146">如何将我的电话号码添加到合作伙伴配置文件联系人部分？</span><span class="sxs-lookup"><span data-stu-id="190ec-146">How do I add my phone number to the partner profile contact section?</span></span>

<span data-ttu-id="190ec-147">电话号码包含三个部分 — 国家/地区代码、区号和电话号码。</span><span class="sxs-lookup"><span data-stu-id="190ec-147">The phone number has three parts — country code, area code, and the telephone number.</span></span> <span data-ttu-id="190ec-148">如果电话号码不包含区号，则保留第二个框为空，并填写第三个框。</span><span class="sxs-lookup"><span data-stu-id="190ec-148">If your phone number doesn't include an area code, then leave the second box empty, and complete the third box.</span></span>

## <a name="how-do-i-manage-my-account-settings-and-partner-profile-in-partner-center"></a><span data-ttu-id="190ec-149">如何在合作伙伴中心管理我的帐户设置和合作伙伴配置文件？</span><span class="sxs-lookup"><span data-stu-id="190ec-149">How do I manage my account settings and partner profile in Partner Center?</span></span>

<span data-ttu-id="190ec-150">请访问我们的 ["管理帐户设置"和配置文件信息](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) 页，获取有关管理合作伙伴中心帐户设置的指南。</span><span class="sxs-lookup"><span data-stu-id="190ec-150">Please visit our [Manage account settings and profile info](/windows/uwp/publish/manage-account-settings-and-profile#additional-settings-and-info) page for guidance on managing your Partner Center account settings.</span></span>

## <a name="why-do-i-receive-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a><span data-ttu-id="190ec-151">当我尝试通过合作伙伴中心提交我的外接程序时，为什么会收到消息"此帐户不符合发布条件"？</span><span class="sxs-lookup"><span data-stu-id="190ec-151">Why do I receive the message, "This account is not publish eligible," when I try to submit my add-in through Partner Center?</span></span>

<span data-ttu-id="190ec-152">帐户验证状态挂起时，您将收到 [上述](/partner-center/verification-responses) 错误消息。</span><span class="sxs-lookup"><span data-stu-id="190ec-152">You'll receive the above error message when your [account verification status](/partner-center/verification-responses) is pending.</span></span> <span data-ttu-id="190ec-153">可以在合作伙伴中心仪表板中检查帐户验证状态，方法[](https://partner.microsoft.com/dashboard)为 (页面标题外壳右上角的齿轮图标) "设置"选项，然后选择"开发人员设置帐户帐户设置  =>     =>  "。</span><span class="sxs-lookup"><span data-stu-id="190ec-153">You can check your account verification status in the Partner Center [dashboard](https://partner.microsoft.com/dashboard) by selecting the **Settings** option (the gear icon) in the upper-right corner of the page header shell and choosing **Developer settings** => **Account**  => **Account settings** .</span></span>

![合作伙伴中心帐户设置页](../../../assets/images/partner-center-accts-page.png)

![合作伙伴中心验证状态](../../../assets/images/partner-center-verification-status.png)

<span data-ttu-id="190ec-156">在帐户验证过程中，将显示每个必需步骤（电子邮件所有权、雇佣验证和业务验证）的状态。</span><span class="sxs-lookup"><span data-stu-id="190ec-156">During the account verification process the status of each required step —  Email Ownership, Employment Verification, and Business Verification — will be displayed.</span></span> <span data-ttu-id="190ec-157">成功完成验证过程后，配置文件页上注册的验证状态会从"挂起"更改为"已授权"，并且将不再显示流程步骤。</span><span class="sxs-lookup"><span data-stu-id="190ec-157">Once the verification process has been successfully completed, the verification status of your enrollment on the profile page will change from "pending" to "authorized," and the process steps will no longer be displayed.</span></span>

![合作伙伴中心验证错误](../../../assets/images/partner-center-acct-verification-error.png)

## <a name="what-is-verified-in-partner-center-account-verification-process-and-how-to-respond"></a><span data-ttu-id="190ec-159">合作伙伴中心帐户验证过程中验证了哪些功能以及如何响应？</span><span class="sxs-lookup"><span data-stu-id="190ec-159">What is verified in Partner Center account verification process and how to respond?</span></span>
<span data-ttu-id="190ec-160">有三个验证区域 - 电子邮件所有权、雇佣和业务。</span><span class="sxs-lookup"><span data-stu-id="190ec-160">There are three verification areas - Email Ownership, Employment and Business.</span></span> <span data-ttu-id="190ec-161">请参阅"已验证内容[](/partner-center/verification-responses#what-is-verified-and-how-to-respond)"和"如何响应"的详细信息。如果你是 (全局管理员或帐户管理员) 的主要联系人，我们建议你转到合作伙伴配置文件以监视验证状态并跟踪进度。</span><span class="sxs-lookup"><span data-stu-id="190ec-161">Please see the details of [What is verified and how to respond](/partner-center/verification-responses#what-is-verified-and-how-to-respond) If you are the primary contact (Global admin or Account admin), we recommend that you go to your Partner Profile to monitor verification status and track progress.</span></span>

<span data-ttu-id="190ec-162">完成验证过程后，配置文件页上注册的验证状态将从挂起更改为已授权，并且该页面上显示的包含状态的进程步骤将消失。</span><span class="sxs-lookup"><span data-stu-id="190ec-162">Once the verification process is complete, the verification status of your enrollment on the profile page will change from *pending* to *authorized* and the process steps with status, displayed on that page, will disappear.</span></span> <span data-ttu-id="190ec-163">主联系人将在验证完成后的几天内收到来自 Microsoft 的电子邮件。</span><span class="sxs-lookup"><span data-stu-id="190ec-163">The primary contact will receive an email from Microsoft within a few business days after the verification is completed.</span></span>

## <a name="my-account-verification-status-has-not-advanced-beyond-email-ownership-in-partner-center-how-should-i-proceed"></a><span data-ttu-id="190ec-164">我的帐户验证状态未超出合作伙伴中心中的电子邮件所有权。</span><span class="sxs-lookup"><span data-stu-id="190ec-164">My account Verification status has not advanced beyond Email Ownership in Partner Center.</span></span> <span data-ttu-id="190ec-165">如何继续？</span><span class="sxs-lookup"><span data-stu-id="190ec-165">How should I proceed?</span></span>

<span data-ttu-id="190ec-166">在 **电子邮件所有权** 验证过程中，验证电子邮件将发送到主要联系人电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="190ec-166">During the **Email Ownership** verification process, a verification email is sent to the primary contact email address.</span></span> <span data-ttu-id="190ec-167">请检查主联系人收件箱，查看来自 maccount@ **<span>microsoft</span>.com** 的电子邮件，主题行为"需要操作：使用 *Microsoft* 验证你的电子邮件帐户，请求你完成电子邮件验证过程"。</span><span class="sxs-lookup"><span data-stu-id="190ec-167">Please check your primary contact inbox for an email  from **maccount@<span>microsoft</span>.com** with the subject  line *Action needed: Verify your email account with Microsoft*, requesting that you complete the email verification process.</span></span> <span data-ttu-id="190ec-168">验证电子邮件将发送到合作伙伴中心帐户设置页中列出的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="190ec-168">The verification email will be sent to the email address listed  in your account settings page in Partner Center.</span></span>

> [!NOTE]
 ><span data-ttu-id="190ec-169">电子邮件验证链接仅在 7 天内有效。</span><span class="sxs-lookup"><span data-stu-id="190ec-169">The email verification link is only valid for 7 days.</span></span> <span data-ttu-id="190ec-170">可以通过访问合作伙伴配置文件页面并选择"重新发送验证电子邮件"链接，请求我们将电子邮件 **重新发送** 给你。</span><span class="sxs-lookup"><span data-stu-id="190ec-170">You can request that we resend the email to you by visiting your partner profile page and selecting the **Resend verification email** link.</span></span> <span data-ttu-id="190ec-171">若要确保收到电子邮件，请安全microsoft.com安全域发送的电子邮件，并检查垃圾邮件文件夹。</span><span class="sxs-lookup"><span data-stu-id="190ec-171">To ensure that the email is received, safelist email from microsoft.com as a secure domain, and check your junk email folders.</span></span>

## <a name="how-i-do-get-further-support-for-my-account-related-issues"></a><span data-ttu-id="190ec-172">如何进一步支持我的帐户相关问题？</span><span class="sxs-lookup"><span data-stu-id="190ec-172">How I do get further support for my account related issues?</span></span>

<span data-ttu-id="190ec-173">请访问合作伙伴 [中心页中的](/azure/marketplace/partner-center-portal/support) 商业市场支持计划页面，了解创建支持票证的指导和步骤。</span><span class="sxs-lookup"><span data-stu-id="190ec-173">Please visit our [Support for the Commercial Marketplace program in Partner Center](/azure/marketplace/partner-center-portal/support) page for guidance and steps to create a support ticket.</span></span>

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what--should-i-do-next"></a><span data-ttu-id="190ec-174">我检查了邮件文件夹，但没有收到验证电子邮件。</span><span class="sxs-lookup"><span data-stu-id="190ec-174">I've checked my mail folders and haven't received the verification email.</span></span> <span data-ttu-id="190ec-175">接下来我应该做什么？</span><span class="sxs-lookup"><span data-stu-id="190ec-175">What  should I do next?</span></span>

<span data-ttu-id="190ec-176">请尝试以下操作：</span><span class="sxs-lookup"><span data-stu-id="190ec-176">Please try the following:</span></span>

1. <span data-ttu-id="190ec-177">检查垃圾邮件/垃圾邮件文件夹。</span><span class="sxs-lookup"><span data-stu-id="190ec-177">Check your junk/spam folder.</span></span>
1. <span data-ttu-id="190ec-178">清除浏览器缓存，转到合作伙伴中心帐户仪表板，然后选择"重新发送验证 **电子邮件** "链接，将验证电子邮件重新发送到你的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="190ec-178">Clear the browser cache, go to your Partner Center account dashboard, and select  the **Resend verification email** link to have the verification email resent to your email address.</span></span>
1. <span data-ttu-id="190ec-179">请尝试从不同  **浏览器访问** "重新发送验证电子邮件"链接。</span><span class="sxs-lookup"><span data-stu-id="190ec-179">Try accessing the  **Resend verification email** link  from a different browser.</span></span>
1. <span data-ttu-id="190ec-180">与 IT 部门合作，确保电子邮件服务器不会阻止验证电子邮件。</span><span class="sxs-lookup"><span data-stu-id="190ec-180">Work with your IT department to ensure that the verification emails are not blocked by the email server.</span></span>
1. <span data-ttu-id="190ec-181">调整服务器的垃圾邮件筛选器以允许/安全列出来自 **maccount@microsoft。 <span></span>com**。</span><span class="sxs-lookup"><span data-stu-id="190ec-181">Adjust your server's spam filter to allow/safelist all emails from **maccount@microsoft.<span></span>com**.</span></span>

## <a name="how-long-does-the-employment-verification-process-usually-take"></a><span data-ttu-id="190ec-182">雇佣验证过程通常需要多久？</span><span class="sxs-lookup"><span data-stu-id="190ec-182">How long does the employment verification process usually take?</span></span>

<span data-ttu-id="190ec-183">如果所有提交的详细信息都正确，则雇佣验证在 1 到 2 小时内完成。</span><span class="sxs-lookup"><span data-stu-id="190ec-183">If all the submitted details are correct, employment verification completes in 1 to 2 hours.</span></span>

## <a name="how-long-does-the-business-verification-process-usually-take"></a><span data-ttu-id="190ec-184">"业务验证"过程通常需要多久？</span><span class="sxs-lookup"><span data-stu-id="190ec-184">How long does the “Business Verification” process usually take?</span></span>

<span data-ttu-id="190ec-185">如果已提交所有必需的文档，则业务验证需要 1 到 2 个工作日才能完成。</span><span class="sxs-lookup"><span data-stu-id="190ec-185">Business Verification takes 1 to 2 business days to complete, provided that all required documents have been submitted.</span></span>

## <a name="if-i-reach-out-to-the-support-team-will-my-ticket-be-expedited"></a><span data-ttu-id="190ec-186">如果我联系支持团队，我的票证是否将被加速？</span><span class="sxs-lookup"><span data-stu-id="190ec-186">If I reach out to the support team, will my ticket be expedited?</span></span>

<span data-ttu-id="190ec-187">支持票证将在一周内解决。</span><span class="sxs-lookup"><span data-stu-id="190ec-187">Support tickets will be resolved within a week's time.</span></span> <span data-ttu-id="190ec-188">请查找将在引发支持票证时发送到提供的电子邮件的更新。</span><span class="sxs-lookup"><span data-stu-id="190ec-188">Please look for the updates which will be sent to the email provided when the support ticket was raised.</span></span>

## <a name="my-issue-is-not-listed-here--are-there-other-pages-i-can-reference-for-partner-center-issues"></a><span data-ttu-id="190ec-189">我的问题未在此处列出。</span><span class="sxs-lookup"><span data-stu-id="190ec-189">My issue is not listed here.</span></span>  <span data-ttu-id="190ec-190">我是否有其他页面可以参考合作伙伴中心问题？</span><span class="sxs-lookup"><span data-stu-id="190ec-190">Are there other pages I can reference for Partner Center issues?</span></span>

<span data-ttu-id="190ec-191">有关更多帮助，请参阅我们的 [商业](/azure/marketplace/) 市场文档。</span><span class="sxs-lookup"><span data-stu-id="190ec-191">Please refer to our [commercial marketplace documentation](/azure/marketplace/) for more help.</span></span>

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a><span data-ttu-id="190ec-192">我创建了一个支持票证，已经 7 个工作日，并且我没有收到更新。</span><span class="sxs-lookup"><span data-stu-id="190ec-192">I've created a support ticket, it has been 7 business days, and I haven't received an update.</span></span> <span data-ttu-id="190ec-193">在哪里可以获取其他帮助？</span><span class="sxs-lookup"><span data-stu-id="190ec-193">Where can I get additional help?</span></span>

<span data-ttu-id="190ec-194">请发送电子邮件至 **<teamsubm@microsoft.com>** 以下详细信息：</span><span class="sxs-lookup"><span data-stu-id="190ec-194">Please send an email to **<teamsubm@microsoft.com>** with the following details:</span></span>

1. <span data-ttu-id="190ec-195">**主题行**。</span><span class="sxs-lookup"><span data-stu-id="190ec-195">**Subject Line**.</span></span> <span data-ttu-id="190ec-196">*合作伙伴中心帐户问题<App_Name>(* 指定应用名称) 。</span><span class="sxs-lookup"><span data-stu-id="190ec-196">*Partner Center Account Issue for <App_Name>* (specify the name of your app).</span></span>
1. <span data-ttu-id="190ec-197">**电子邮件正文：**</span><span class="sxs-lookup"><span data-stu-id="190ec-197">**Email body:**</span></span>
    * <span data-ttu-id="190ec-198">支持票证编号：</span><span class="sxs-lookup"><span data-stu-id="190ec-198">Support ticket number:</span></span>
    * <span data-ttu-id="190ec-199">卖家 ID：</span><span class="sxs-lookup"><span data-stu-id="190ec-199">Your seller ID:</span></span>
    * <span data-ttu-id="190ec-200">如果可能，问题 (屏幕截图) ：</span><span class="sxs-lookup"><span data-stu-id="190ec-200">A screen shot of the issue (if possible):</span></span>
    
## <a name="app-category-mapping"></a><span data-ttu-id="190ec-201">应用类别映射</span><span class="sxs-lookup"><span data-stu-id="190ec-201">App category mapping</span></span>

| <span data-ttu-id="190ec-202">Teams 类别</span><span class="sxs-lookup"><span data-stu-id="190ec-202">Teams Category</span></span>       | <span data-ttu-id="190ec-203">电脑类别</span><span class="sxs-lookup"><span data-stu-id="190ec-203">PC Categories</span></span>  |
|:---------------------|:---------------|
| <span data-ttu-id="190ec-204">分析和 BI</span><span class="sxs-lookup"><span data-stu-id="190ec-204">Analytics and BI</span></span> | <span data-ttu-id="190ec-205">分析、数据可视化和 BI</span><span class="sxs-lookup"><span data-stu-id="190ec-205">Analytics, Data Visualization and BI</span></span> |
| <span data-ttu-id="190ec-206">开发人员和 IT</span><span class="sxs-lookup"><span data-stu-id="190ec-206">Developer and IT</span></span> | <span data-ttu-id="190ec-207">开发人员工具、IT 管理员</span><span class="sxs-lookup"><span data-stu-id="190ec-207">Developer Tools, IT Admin</span></span> |
| <span data-ttu-id="190ec-208">教育</span><span class="sxs-lookup"><span data-stu-id="190ec-208">Education</span></span> | <span data-ttu-id="190ec-209">教育</span><span class="sxs-lookup"><span data-stu-id="190ec-209">Education</span></span> |
| <span data-ttu-id="190ec-210">人力资源</span><span class="sxs-lookup"><span data-stu-id="190ec-210">Human resources</span></span> | <span data-ttu-id="190ec-211">人力资源和招聘</span><span class="sxs-lookup"><span data-stu-id="190ec-211">Human Resources and Recruiting</span></span> |
| <span data-ttu-id="190ec-212">工作效率</span><span class="sxs-lookup"><span data-stu-id="190ec-212">Productivity</span></span> | <span data-ttu-id="190ec-213">内容管理、文件和文档、生产力、培训和教程以及实用程序</span><span class="sxs-lookup"><span data-stu-id="190ec-213">Content Management, Files and documents, Productivity, Training and Tutorials, and Utilities</span></span> |
| <span data-ttu-id="190ec-214">项目管理</span><span class="sxs-lookup"><span data-stu-id="190ec-214">Project management</span></span> | <span data-ttu-id="190ec-215">通信、项目管理、工作流和业务管理</span><span class="sxs-lookup"><span data-stu-id="190ec-215">Communication, Project Management, Workflow and Business Management</span></span> |
| <span data-ttu-id="190ec-216">销售和支持</span><span class="sxs-lookup"><span data-stu-id="190ec-216">Sales and support</span></span> | <span data-ttu-id="190ec-217">客户和联系人管理、客户支持、财务管理、销售和市场营销</span><span class="sxs-lookup"><span data-stu-id="190ec-217">Customer and Contact Management, Customer Support, Financial Management, Sales and Marketing</span></span> |
| <span data-ttu-id="190ec-218">社交和有趣</span><span class="sxs-lookup"><span data-stu-id="190ec-218">Social and fun</span></span> | <span data-ttu-id="190ec-219">图像和视频库、生活方式、新闻和天气、社交、旅行和导航</span><span class="sxs-lookup"><span data-stu-id="190ec-219">Image and Video Galleries, Lifestyle, News and Weather, Social, Travel and Navigation</span></span> |

>
> [!div class="nextstepaction"]
> [<span data-ttu-id="190ec-220">详细了解 Microsoft Teams 的应用验证策略</span><span class="sxs-lookup"><span data-stu-id="190ec-220">Learn more about app validation policies for Microsoft Teams</span></span>](/legal/marketplace/certification-policies)
