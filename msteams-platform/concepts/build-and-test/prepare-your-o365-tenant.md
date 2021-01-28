---
title: 准备 Microsoft 365 租户
description: 如何在 Microsoft 365 中开始使用 Teams
ms.topic: how-to
keywords: 配置 Microsoft 365 租户 Teams 上传
ms.openlocfilehash: bfeb1a5d39b8a6ad8d1dd4d631f984ecec4e26f1
ms.sourcegitcommit: 976e870cc925f61b76c3830ec04ba6e4bdfde32f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 01/27/2021
ms.locfileid: "50014451"
---
# <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="84452-104">准备 Microsoft 365 租户</span><span class="sxs-lookup"><span data-stu-id="84452-104">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="84452-105">如果你是 Microsoft 365 订阅者，可以使用以下计划之一为 Microsoft Teams 开发 [应用](https://products.office.com/business/compare-more-office-365-for-business-plans)：</span><span class="sxs-lookup"><span data-stu-id="84452-105">If you are a Microsoft 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="84452-106">基本</span><span class="sxs-lookup"><span data-stu-id="84452-106">Basic</span></span>
* <span data-ttu-id="84452-107">标准</span><span class="sxs-lookup"><span data-stu-id="84452-107">Standard</span></span>
* <span data-ttu-id="84452-108">企业版 E1、E3 和 E5</span><span class="sxs-lookup"><span data-stu-id="84452-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="84452-109">开发人员版</span><span class="sxs-lookup"><span data-stu-id="84452-109">Developer</span></span>
* <span data-ttu-id="84452-110">教育版、教育增强版和教育版 E5</span><span class="sxs-lookup"><span data-stu-id="84452-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="84452-111">Microsoft Teams 也将提供给在停用之前订阅 E4 [的客户](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)。</span><span class="sxs-lookup"><span data-stu-id="84452-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="84452-112">只需要开发环境？</span><span class="sxs-lookup"><span data-stu-id="84452-112">Just need a development environment?</span></span>

<span data-ttu-id="84452-113">如果当前没有 Microsoft 365 帐户，可以注册 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program) 订阅。</span><span class="sxs-lookup"><span data-stu-id="84452-113">If you don't currently have a Microsoft 365 account, you can sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="84452-114">它 *90* 天免费，并且将持续续订，只要使用它进行开发活动。</span><span class="sxs-lookup"><span data-stu-id="84452-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="84452-115">如果你有企业Visual Studio专业版订阅，这两个计划都包括免费的 Microsoft 365 开发人员[](https://aka.ms/MyVisualStudioBenefits)订阅，在订阅的生命周期内Visual Studio订阅。</span><span class="sxs-lookup"><span data-stu-id="84452-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="84452-116">*请参阅*[设置 Microsoft 365 开发人员订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="84452-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="84452-117">为组织启用 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="84452-117">Enable Microsoft Teams for your organization</span></span> 

<span data-ttu-id="84452-118">如果尚未为组织启用 Microsoft Teams，你将需要首先执行这一操作。</span><span class="sxs-lookup"><span data-stu-id="84452-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="84452-119">请看一下我们为组织 [启用 Teams 的详细指南](/microsoftteams/enable-features-office-365)。</span><span class="sxs-lookup"><span data-stu-id="84452-119">Take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="84452-120">启用自定义 Teams 应用并启用自定义应用上传</span><span class="sxs-lookup"><span data-stu-id="84452-120">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="84452-121">为开发人员租户启用自定义应用旁加载，如下所示：</span><span class="sxs-lookup"><span data-stu-id="84452-121">Turn on custom app sideloading for your developer tenant as follows:</span></span>

1. <span data-ttu-id="84452-122">使用管理员 [凭据登录到 Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) 管理中心。</span><span class="sxs-lookup"><span data-stu-id="84452-122">Login to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credential.</span></span> 

2. <span data-ttu-id="84452-123">选择 **"显示所有**  -->  **团队"。**</span><span class="sxs-lookup"><span data-stu-id="84452-123">Select **Show All** --> **Teams**.</span></span> 

![管理中心菜单的图像](~/assets/images/prepare-test-tenant/admin-center.png)

> [!Note] 
> <span data-ttu-id="84452-125">"Teams"选项最多可能需要 24 小时才能显示。</span><span class="sxs-lookup"><span data-stu-id="84452-125">It can take up to 24 hours for the "Teams" option to appear.</span></span> <span data-ttu-id="84452-126">在此期间，你可以将 [自定义应用上载到 Teams 环境](/microsoftteams/upload-custom-apps#validate) 以进行测试和验证。</span><span class="sxs-lookup"><span data-stu-id="84452-126">During interim, you can [Upload your custom app to a Teams environment](/microsoftteams/upload-custom-apps#validate) for testing and validation.</span></span>

3. <span data-ttu-id="84452-127">导航到 **Teams 应用**  -->  **设置策略**  -->  **全局 (组织范围内的默认)**</span><span class="sxs-lookup"><span data-stu-id="84452-127">Navigate to **Teams apps** --> **Setup Policies** --> **Global(Org-wide default)**</span></span>  

![打开旁加载视图](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="84452-129">将 **自定义应用切换** 至 **打开** 位置。</span><span class="sxs-lookup"><span data-stu-id="84452-129">Toggle **upload custom apps** to the **on** position.</span></span>

<span data-ttu-id="84452-130">就是这么简单。</span><span class="sxs-lookup"><span data-stu-id="84452-130">That's it!</span></span> <span data-ttu-id="84452-131">你的测试租户现在将允许自定义应用旁加载。</span><span class="sxs-lookup"><span data-stu-id="84452-131">Your test tenant will now allow custom app sideloading.</span></span>

> [!Note] 
> <span data-ttu-id="84452-132">启用旁加载最多可能需要 24 小时。</span><span class="sxs-lookup"><span data-stu-id="84452-132">It can take up to 24 hours before sideloading is enabled.</span></span> <span data-ttu-id="84452-133">在此期间，可以使用 **上传来 \<your tenant>** 测试你的应用。</span><span class="sxs-lookup"><span data-stu-id="84452-133">During interim, you can use **upload for \<your tenant>** to test your app.</span></span>

![updload 应用视图](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="84452-135">有关这些设置如何交互的完整信息，请参阅：在[Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)中管理自定义应用策略和设置，以及[管理 Microsoft Teams 中的应用设置策略](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)。</span><span class="sxs-lookup"><span data-stu-id="84452-135">For complete information on how these settings interact, *See*, [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>
