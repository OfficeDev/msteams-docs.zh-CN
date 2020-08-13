---
title: 准备团队开发环境
description: 如何将您的环境设置为 developi 团队应用程序
keywords: 配置 Office 365 租户团队上载环境开发
ms.openlocfilehash: 701c6c110026007cf1670e783348bbdbe1aff498
ms.sourcegitcommit: 9fbc701a9a039ecdc360aefbe86df52b9c3593f3
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 08/12/2020
ms.locfileid: "46651896"
---
# <a name="prepare-your-development-environment"></a><span data-ttu-id="5729a-104">准备开发环境</span><span class="sxs-lookup"><span data-stu-id="5729a-104">Prepare your development environment</span></span>

<span data-ttu-id="5729a-105">如果你是 Office 365 订阅者，则可以使用以下 [计划](https://products.office.com/business/compare-more-office-365-for-business-plans)之一为 Microsoft 团队开发应用程序：</span><span class="sxs-lookup"><span data-stu-id="5729a-105">If you are an Office 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="5729a-106">商业协作版</span><span class="sxs-lookup"><span data-stu-id="5729a-106">Business Essentials</span></span>
* <span data-ttu-id="5729a-107">商业高级版</span><span class="sxs-lookup"><span data-stu-id="5729a-107">Business Premium</span></span>
* <span data-ttu-id="5729a-108">企业版 E1、E3 和 E5</span><span class="sxs-lookup"><span data-stu-id="5729a-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="5729a-109">Developer</span><span class="sxs-lookup"><span data-stu-id="5729a-109">Developer</span></span>
* <span data-ttu-id="5729a-110">教育版、教育版和教育版 E5</span><span class="sxs-lookup"><span data-stu-id="5729a-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="5729a-111">Microsoft 团队还将对在其 [退休](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)前订阅 E4 的客户提供。</span><span class="sxs-lookup"><span data-stu-id="5729a-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="5729a-112">只需要开发环境？</span><span class="sxs-lookup"><span data-stu-id="5729a-112">Just need a development environment?</span></span>

<span data-ttu-id="5729a-113">如果当前没有 Office 365 帐户，则可以注册 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program) 订阅。</span><span class="sxs-lookup"><span data-stu-id="5729a-113">If you don't currently have an Office 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="5729a-114">它在90天内 *免费* 使用，并且将持续更新，只要你将其用于开发活动即可。</span><span class="sxs-lookup"><span data-stu-id="5729a-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="5729a-115">如果你有 Visual Studio *Enterprise* 或 *专业版* 订阅，这两个程序都包括一个免费的 Microsoft 365 [开发人员订阅](https://aka.ms/MyVisualStudioBenefits)，在 Visual Studio 订阅的生命周期内处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="5729a-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="5729a-116">*请参阅*[设置 Microsoft 365 开发人员订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="5729a-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="5729a-117">为你的组织启用 Microsoft 团队</span><span class="sxs-lookup"><span data-stu-id="5729a-117">Enable Microsoft Teams for your organization</span></span>

<span data-ttu-id="5729a-118">如果尚未为你的组织启用 Microsoft 团队，你将需要先执行此操作。</span><span class="sxs-lookup"><span data-stu-id="5729a-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="5729a-119">请参阅我们为 [你的组织启用团队](https://docs.microsoft.com/microsoftteams/enable-features-office-365)的详细指南。</span><span class="sxs-lookup"><span data-stu-id="5729a-119">Take a look at our detailed guidance for [enabling Teams for your organization](https://docs.microsoft.com/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="5729a-120">启用自定义团队应用并启用自定义应用上传</span><span class="sxs-lookup"><span data-stu-id="5729a-120">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="5729a-121">按如下方式为开发人员租户启用自定义应用旁加载：</span><span class="sxs-lookup"><span data-stu-id="5729a-121">Turn on custom app sideloading for your developer tenant as follows:</span></span>

1. <span data-ttu-id="5729a-122">使用管理员凭据登录到 [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) 。</span><span class="sxs-lookup"><span data-stu-id="5729a-122">Login to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credential.</span></span> 

2. <span data-ttu-id="5729a-123">选择 "**显示所有**  -->  **团队**"。</span><span class="sxs-lookup"><span data-stu-id="5729a-123">Select **Show All** --> **Teams**.</span></span> 

![应用程序溢出菜单的图像](~/assets/images/prepare-test-tenant/admin-center.png)

3. <span data-ttu-id="5729a-125">导航到**团队应用**  -->  **程序设置策略**  -->  \*\*全局 (组织范围默认) \*\*</span><span class="sxs-lookup"><span data-stu-id="5729a-125">Navigate to **Teams apps** --> **Setup Policies** --> **Global(Org-wide default)**</span></span>  

![应用程序溢出菜单的图像](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="5729a-127">将 " **上载自定义应用** " 切换到 " **开** " 位置。</span><span class="sxs-lookup"><span data-stu-id="5729a-127">Toggle **upload custom apps** to the **on** position.</span></span>

<span data-ttu-id="5729a-128">就是这么简单。</span><span class="sxs-lookup"><span data-stu-id="5729a-128">That's it!</span></span> <span data-ttu-id="5729a-129">你的测试租户现在将允许自定义应用旁加载。</span><span class="sxs-lookup"><span data-stu-id="5729a-129">Your test tenant will now allow custom app sideloading.</span></span>

> [!Note] 
> <span data-ttu-id="5729a-130">在启用旁加载之前，可能需要长达24小时。</span><span class="sxs-lookup"><span data-stu-id="5729a-130">It can take up to 24 hours before sideloading is enabled.</span></span> <span data-ttu-id="5729a-131">在临时期间，您可以使用**上 \<your tenant> 传**来测试您的应用程序。</span><span class="sxs-lookup"><span data-stu-id="5729a-131">During interim, you can use **upload for \<your tenant>** to test your app.</span></span>

![应用程序溢出菜单的图像](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="5729a-133">有关这些设置如何进行交互的完整信息， *请参阅*在 microsoft 团队中 [管理自定义应用策略和设置](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) 和 [管理 microsoft 团队中的应用程序安装策略](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)。</span><span class="sxs-lookup"><span data-stu-id="5729a-133">For complete information on how these settings interact, *See*, [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>