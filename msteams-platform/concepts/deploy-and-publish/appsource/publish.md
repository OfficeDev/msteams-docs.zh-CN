---
title: Microsoft 团队应用程序审批过程指南
description: 介绍了如何将应用发布到 Microsoft 团队应用商店的审批过程
keywords: 团队发布 microsoft store office 发布 AppSource
ms.openlocfilehash: 70f81f40ff424ab28e7129da7b947be0b1fcf469
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914544"
---
# <a name="submit-your-app-to-appsource"></a><span data-ttu-id="c3873-104">将您的应用程序提交到 AppSource</span><span class="sxs-lookup"><span data-stu-id="c3873-104">Submit your app to AppSource</span></span>

## <a name="teams-app-submission"></a><span data-ttu-id="c3873-105">团队应用程序提交</span><span class="sxs-lookup"><span data-stu-id="c3873-105">Teams app submission</span></span>

<span data-ttu-id="c3873-106">将应用程序发布到[AppSource](https://appsource.microsoft.com)使其在团队应用程序目录和 web 上可用。</span><span class="sxs-lookup"><span data-stu-id="c3873-106">Publishing  your app to [AppSource](https://appsource.microsoft.com) makes it available in the Teams app catalog and on the web.</span></span> <span data-ttu-id="c3873-107">从较高的层次来看，将应用程序提交到 AppSource 的过程如下：</span><span class="sxs-lookup"><span data-stu-id="c3873-107">At a high level, the process for submitting your app to AppSource is:</span></span>

1. <span data-ttu-id="c3873-108">遵循我们的[设计准则](~/concepts/design/understand-use-cases.md)来开发您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c3873-108">Develop your app following our [design guidelines](~/concepts/design/understand-use-cases.md).</span></span> <span data-ttu-id="c3873-109">选项卡应遵循我们的[选项卡设计准则](~/tabs/design/tabs.md)。</span><span class="sxs-lookup"><span data-stu-id="c3873-109">Tabs should follow our [tab design guidelines](~/tabs/design/tabs.md).</span></span> <span data-ttu-id="c3873-110">Bot 应遵循[bot 设计指南](~/bots/design/bots.md)。</span><span class="sxs-lookup"><span data-stu-id="c3873-110">Bots should follow the [bot design guidelines](~/bots/design/bots.md).</span></span>
1. <span data-ttu-id="c3873-111">在 "[合作伙伴中心](https://support.microsoft.com/help/4499930/partner-center-overview)" 中[设置开发人员帐户](/office/dev/store/open-a-developer-account)。</span><span class="sxs-lookup"><span data-stu-id="c3873-111">[Set up a developer account](/office/dev/store/open-a-developer-account) in [Partner Center](https://support.microsoft.com/help/4499930/partner-center-overview).</span></span>
1. <span data-ttu-id="c3873-112">按照[提交清单](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md)，准备要提交的应用程序。</span><span class="sxs-lookup"><span data-stu-id="c3873-112">Prepare your app for submission by following our [submission checklist](~/concepts/deploy-and-publish/appsource/prepare/submission-checklist.md).</span></span>
1. <span data-ttu-id="c3873-113">查看我们[关于成功提交应用程序的提示](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md)。</span><span class="sxs-lookup"><span data-stu-id="c3873-113">Review our [tips for a successful app submission](~/concepts/deploy-and-publish/appsource/prepare/frequently-failed-cases.md).</span></span>
1. <span data-ttu-id="c3873-114">[通过合作伙伴中心](/office/dev/store/use-partner-center-to-submit-to-appsource)将您的包提交到 AppSource。</span><span class="sxs-lookup"><span data-stu-id="c3873-114">Submit your package to [AppSource through Partner Center](/office/dev/store/use-partner-center-to-submit-to-appsource).</span></span>
1. <span data-ttu-id="c3873-115">跟踪合作伙伴中心仪表板上的审批流程。</span><span class="sxs-lookup"><span data-stu-id="c3873-115">Track the approval process on your Partner Center dashboard.</span></span> <span data-ttu-id="c3873-116">*请参阅*[合作伙伴中心概述](https://support.microsoft.com/help/4499930/partner-center-overview)。</span><span class="sxs-lookup"><span data-stu-id="c3873-116">*See* [Partner Center Overview](https://support.microsoft.com/help/4499930/partner-center-overview).</span></span>
1. <span data-ttu-id="c3873-117">提交后提交—查看有关[维护和支持您发布的应用程序](~/concepts/deploy-and-publish/appsource/post-publish/overview.md)的指南。</span><span class="sxs-lookup"><span data-stu-id="c3873-117">Post submission — review our guidance for [Maintaining and supporting your published app](~/concepts/deploy-and-publish/appsource/post-publish/overview.md).</span></span>

>[!NOTE]
>
> * <span data-ttu-id="c3873-118">如果您的团队应用程序包含 bot，则必须遵守 Bot 开发人员框架[行为准则](https://aka.ms/bf-conduct)。</span><span class="sxs-lookup"><span data-stu-id="c3873-118">If your Teams app contains a bot, you must comply with the Bot Developer Framework [Code of Conduct](https://aka.ms/bf-conduct).</span></span>
> * <span data-ttu-id="c3873-119">如果您的应用程序包含 Office 365 连接器，可能会应用其他条款。</span><span class="sxs-lookup"><span data-stu-id="c3873-119">If your app contains an Office 365 Connector, additional terms may apply.</span></span> <span data-ttu-id="c3873-120">*请参阅*[连接器开发人员仪表板](https://aka.ms/connectorsdashboard)和[应用程序开发人员协议](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm)。</span><span class="sxs-lookup"><span data-stu-id="c3873-120">*See* [Connectors Developer Dashboard](https://aka.ms/connectorsdashboard) and [App Developer Agreement](https://sellerdashboard.microsoft.com/Assets/Content/Agreements/Office_Store_Seller_Agreement_20120927.htm).</span></span>

## <a name="faqs--teams-apps-and-partner-accounts"></a><span data-ttu-id="c3873-121">Faq —团队应用和合作伙伴帐户</span><span class="sxs-lookup"><span data-stu-id="c3873-121">FAQs — Teams apps and Partner accounts</span></span>

## <a name="how-do-i-create-a-partner-center-account"></a><span data-ttu-id="c3873-122">如何创建合作伙伴中心帐户？</span><span class="sxs-lookup"><span data-stu-id="c3873-122">How do I create a Partner Center account?</span></span>

<span data-ttu-id="c3873-123">有两种创建合作伙伴中心帐户的方法：</span><span class="sxs-lookup"><span data-stu-id="c3873-123">There are two ways to create a Partner Center account:</span></span>

* <span data-ttu-id="c3873-124">如果你不熟悉合作伙伴中心，并且在 Microsoft 网络中没有帐户，请[使用 "合作伙伴中心注册" 页创建帐户](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment)。</span><span class="sxs-lookup"><span data-stu-id="c3873-124">If you're new to Partner center and don't have an account  within the Microsoft network, [create an account using the Partner Center enrollment page](/office/dev/store/open-a-developer-account#create-an-account-using-an-existing-partner-center-enrollment).</span></span>
* <span data-ttu-id="c3873-125">如果你已在合作伙伴网络中注册，请[使用现有注册直接在合作伙伴中心中创建帐户](/office/dev/store/)。</span><span class="sxs-lookup"><span data-stu-id="c3873-125">If you're already enrolled in the Partner Network, [create an account directly in Partner Center using an existing enrollment](/office/dev/store/).</span></span>

## <a name="how-do-i-add-my-phone-number-to-the-contact-info-section"></a><span data-ttu-id="c3873-126">如何将我的电话号码添加到 "联系人信息" 部分？</span><span class="sxs-lookup"><span data-stu-id="c3873-126">How do I add my phone number to the contact info section?</span></span>

<span data-ttu-id="c3873-127">电话号码包含三个部分：国家/地区代码、区号和电话号码。</span><span class="sxs-lookup"><span data-stu-id="c3873-127">The phone number has three parts — country code, area code, and the telephone number.</span></span> <span data-ttu-id="c3873-128">如果任何部分不适用，请输入数字`0`。</span><span class="sxs-lookup"><span data-stu-id="c3873-128">If any section is not applicable, please enter the number `0`.</span></span>

## <a name="why-do-i-get-the-message-this-account-is-not-publish-eligible-when-i-try-to-submit-my-add-in-through-partner-center"></a><span data-ttu-id="c3873-129">如果我尝试通过合作伙伴中心提交我的加载项，为什么我会收到 "此帐户未发布资格" 消息？</span><span class="sxs-lookup"><span data-stu-id="c3873-129">Why do I get the message, "This account is not publish eligible," when I try to submit my add-in through Partner Center?</span></span>

<span data-ttu-id="c3873-130">当您的[帐户验证状态](/partner-center/verification-responses)为 "挂起" 时，您将收到上述错误消息。</span><span class="sxs-lookup"><span data-stu-id="c3873-130">You will receive the above error message when your [account verification status](/partner-center/verification-responses) is pending.</span></span> <span data-ttu-id="c3873-131">您可以通过在页面页眉命令行管理程序的右上角选择 "**设置**" 选项（齿轮图标），然后选择 "**开发人员设置** => **帐户**  => **帐户设置**"，在 "合作伙伴中心"[仪表板](https://partner.microsoft.com/dashboard)中检查您的帐户验证状态。</span><span class="sxs-lookup"><span data-stu-id="c3873-131">You can check your account verification status in the Partner Center [dashboard](https://partner.microsoft.com/dashboard) by selecting the **Settings** option (the gear icon) in the upper-right corner of the page header shell and choosing **Developer settings** => **Account**  => **Account settings** .</span></span>

![合作伙伴中心帐户设置页](../../../assets/images/partner-center-accts-page.png)

![合作伙伴中心验证状态](../../../assets/images/partner-center-verification-status.png)

<span data-ttu-id="c3873-134">在帐户验证过程中，将显示每个所需步骤的状态（电子邮件所有权、雇用验证和商业验证）。</span><span class="sxs-lookup"><span data-stu-id="c3873-134">During the account verification process the status of each required step —  email ownership, employment verification, and business verification — will be displayed.</span></span> <span data-ttu-id="c3873-135">成功完成验证过程后，配置文件页上的注册的验证状态将从 "挂起" 更改为 "已授权"，并且不会再显示进程步骤。</span><span class="sxs-lookup"><span data-stu-id="c3873-135">Once the verification process has been successfully completed, the verification status of your enrollment on the profile page will change from "pending" to "authorized," and the process steps will no longer be displayed.</span></span>

![合作伙伴中心验证错误](../../../assets/images/partner-center-acct-verification-error.png)

## <a name="how-i-do-get-further-support-for-my-account-related-issues"></a><span data-ttu-id="c3873-137">如何获取对与我的帐户相关的问题的进一步支持？</span><span class="sxs-lookup"><span data-stu-id="c3873-137">How I do get further support for my account related issues?</span></span>

<span data-ttu-id="c3873-138">访问[合作伙伴帮助和支持页面](https://aka.ms/marketplacepublishersupport)，并搜索与你的问题相关的文档的有用解决方案。</span><span class="sxs-lookup"><span data-stu-id="c3873-138">Visit the [Partner help and support page](https://aka.ms/marketplacepublishersupport) and search for helpful solutions for documentation related to your issue.</span></span> <span data-ttu-id="c3873-139">如果提供的自助服务解决方案或文档对解决你的问题没有帮助，请通过选择 "**下一步**" 部分下的 "**提供问题详细信息**" 来将支持票证文件存档。</span><span class="sxs-lookup"><span data-stu-id="c3873-139">If the provided self-serve solutions or documents are not helpful in resolving your issue, please file a support ticket by selecting **Provide issue details** under the **Next step** section.</span></span> <span data-ttu-id="c3873-140">您可以在 "搜索" 框中搜索问题主题，或选择 "搜索" 框下方的 "**浏览主题**" 进一步向下钻取。</span><span class="sxs-lookup"><span data-stu-id="c3873-140">You can search for your issue topic in the search box or select **Browse Topics**, below the search box, to drill down further.</span></span>

> [!TIP]
> <span data-ttu-id="c3873-141">如果你要查找有关**帐户验证**问题的帮助：</span><span class="sxs-lookup"><span data-stu-id="c3873-141">If you're looking for help with an **account verification**  Issue:</span></span>
>
>1. <span data-ttu-id="c3873-142">在**搜索框**下方，选择 "**浏览主题**"。</span><span class="sxs-lookup"><span data-stu-id="c3873-142">Below the **Search box**, select **Browse Topics**.</span></span>
>1. <span data-ttu-id="c3873-143">从 "**类别**" 下拉菜单中选择 "**所有程序**"。</span><span class="sxs-lookup"><span data-stu-id="c3873-143">Select **All programs** from the **Category** drop-down menu.</span></span>
> 1. <span data-ttu-id="c3873-144">从 "**主题**" 下拉菜单中选择 "**帐户"、"加入" 和 "访问**"。</span><span class="sxs-lookup"><span data-stu-id="c3873-144">Select **Account, Onboarding, Access** from the **Topic** drop-down menu.</span></span>
>1. <span data-ttu-id="c3873-145">从 "**副标题**" 下拉菜单中**选择一个选项**。</span><span class="sxs-lookup"><span data-stu-id="c3873-145">**Select an option** from the **Subtopic** drop-down menu.</span></span>
>1. <span data-ttu-id="c3873-146">获取更多帮助。</span><span class="sxs-lookup"><span data-stu-id="c3873-146">For further assistance.</span></span> <span data-ttu-id="c3873-147">在 "**下一步**" 部分下选择 "**提供问题详细信息**"。</span><span class="sxs-lookup"><span data-stu-id="c3873-147">select **Provide issue details** under  the **Next Step** section.</span></span>
>

## <a name="ive-checked-my-mail-folders-and-havent-received-the-verification-email-what--should-i-do-next"></a><span data-ttu-id="c3873-148">我已检查我的邮件文件夹，但尚未收到验证电子邮件。</span><span class="sxs-lookup"><span data-stu-id="c3873-148">I've checked my mail folders and haven't received the verification email.</span></span> <span data-ttu-id="c3873-149">接下来我该怎么办？</span><span class="sxs-lookup"><span data-stu-id="c3873-149">What  should I do next?</span></span>

<span data-ttu-id="c3873-150">请尝试以下操作：</span><span class="sxs-lookup"><span data-stu-id="c3873-150">Please try the following:</span></span>

1. <span data-ttu-id="c3873-151">检查您的垃圾邮件文件夹。</span><span class="sxs-lookup"><span data-stu-id="c3873-151">Check your junk/spam folder.</span></span>
1. <span data-ttu-id="c3873-152">清除浏览器缓存，转到合作伙伴中心帐户仪表板，然后选择 "**重新发送验证电子邮件**" 链接，将验证电子邮件发送到您的电子邮件地址。</span><span class="sxs-lookup"><span data-stu-id="c3873-152">Clear the browser cache, go to your Partner Center account dashboard, and select  the **Resend verification email** link to have the verification email resent to your email address.</span></span>
1. <span data-ttu-id="c3873-153">尝试从其他浏览器访问**重新发送验证电子邮件**链接。</span><span class="sxs-lookup"><span data-stu-id="c3873-153">Try accessing the  **Resend verification email** link  from a different browser.</span></span>
1. <span data-ttu-id="c3873-154">与 IT 部门合作，以确保电子邮件服务器不会阻止验证电子邮件。</span><span class="sxs-lookup"><span data-stu-id="c3873-154">Work with your IT department to ensure that the verification emails are not blocked by the email server.</span></span>
1. <span data-ttu-id="c3873-155">调整您的服务器的垃圾邮件筛选器以允许/白名单中的所有电子邮件**maccount@microsoft。<span> </span>com**。</span><span class="sxs-lookup"><span data-stu-id="c3873-155">Adjust your server's spam filter to allow/whitelist all emails from **maccount@microsoft.<span></span>com**.</span></span>

## <a name="how-long-does-the-employment-verification-process-usually-take"></a><span data-ttu-id="c3873-156">雇用验证过程通常需要多长时间？</span><span class="sxs-lookup"><span data-stu-id="c3873-156">How long does the employment verification process usually take?</span></span>

<span data-ttu-id="c3873-157">如果正确提供了所有详细信息，则雇佣验证将在1到2小时内完成。</span><span class="sxs-lookup"><span data-stu-id="c3873-157">If all the details are provided correctly, employment verification completes in 1 to 2 hours.</span></span>

## <a name="ive-already-reached-out-to-support-is-there-a-way-to-expedite-my-case"></a><span data-ttu-id="c3873-158">我已经接通了支持，有没有办法可以加快我的案件？</span><span class="sxs-lookup"><span data-stu-id="c3873-158">I've already reached out to Support, is there a way to expedite my case?</span></span>

<span data-ttu-id="c3873-159">支持票证将在一周内得到解决。</span><span class="sxs-lookup"><span data-stu-id="c3873-159">Support tickets will be resolved within a week's time.</span></span> <span data-ttu-id="c3873-160">请查找将发送到在发出支持票证时提供的电子邮件的更新。</span><span class="sxs-lookup"><span data-stu-id="c3873-160">Please look for the updates which will be sent to the email provided when the support ticket was raised.</span></span>

## <a name="ive-created-a-support-ticket-it-has-been-7-business-days-and-i-havent-received-an-update-where-can-i-get-additional-help"></a><span data-ttu-id="c3873-161">我已经创建了一个支持票证，它已有7个工作日，但尚未收到更新。</span><span class="sxs-lookup"><span data-stu-id="c3873-161">I've created a support ticket, it has been 7 business days, and I haven't received an update.</span></span> <span data-ttu-id="c3873-162">在哪里可以获得更多帮助？</span><span class="sxs-lookup"><span data-stu-id="c3873-162">Where can I get additional help?</span></span>

<span data-ttu-id="c3873-163">请**<teamsubm@microsoft.com>** 使用以下详细信息发送电子邮件：</span><span class="sxs-lookup"><span data-stu-id="c3873-163">Please send an email to **<teamsubm@microsoft.com>** with the following details:</span></span>

1. <span data-ttu-id="c3873-164">**主题行**。</span><span class="sxs-lookup"><span data-stu-id="c3873-164">**Subject Line**.</span></span> <span data-ttu-id="c3873-165">*<App_Name>的合作伙伴中心帐户问题*（指定您的应用程序的名称）。</span><span class="sxs-lookup"><span data-stu-id="c3873-165">*Partner Center Account Issue for <App_Name>* (specify the name of your app).</span></span>
2. <span data-ttu-id="c3873-166">**电子邮件正文：**</span><span class="sxs-lookup"><span data-stu-id="c3873-166">**Email body:**</span></span>
    * <span data-ttu-id="c3873-167">支持票证号码：</span><span class="sxs-lookup"><span data-stu-id="c3873-167">Support ticket number:</span></span>
    * <span data-ttu-id="c3873-168">卖家 ID：</span><span class="sxs-lookup"><span data-stu-id="c3873-168">Your seller ID:</span></span>
    * <span data-ttu-id="c3873-169">问题的屏幕截图。</span><span class="sxs-lookup"><span data-stu-id="c3873-169">A screen shot of the issue.</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c3873-170">了解有关 Microsoft 团队的应用验证策略的详细信息</span><span class="sxs-lookup"><span data-stu-id="c3873-170">Learn more about app validation policies for Microsoft Teams</span></span>](https://docs.microsoft.com/legal/marketplace/certification-policies)
