---
title: 准备 Microsoft 365 租户
description: 如何在 Microsoft 365 中开始使用 Teams
ms.topic: how-to
keywords: 配置 Microsoft 365 租户 Teams 上传
ms.openlocfilehash: aa7f994744f8b1c62aa32122a5006cfa0f22d391
ms.sourcegitcommit: 5b3ba227c2e5e6f7a2c629961993f168da6a504d
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/08/2021
ms.locfileid: "51634748"
---
# <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="0245e-104">准备 Microsoft 365 租户</span><span class="sxs-lookup"><span data-stu-id="0245e-104">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="0245e-105">Microsoft 365 订阅者可以使用以下计划之一为 Microsoft Teams 开发应用：</span><span class="sxs-lookup"><span data-stu-id="0245e-105">Microsoft 365 subscribers can develop apps for Microsoft Teams with one of the following plans:</span></span>

* <span data-ttu-id="0245e-106">基本</span><span class="sxs-lookup"><span data-stu-id="0245e-106">Basic</span></span>
* <span data-ttu-id="0245e-107">标准</span><span class="sxs-lookup"><span data-stu-id="0245e-107">Standard</span></span>
* <span data-ttu-id="0245e-108">企业版 E1、E3 和 E5</span><span class="sxs-lookup"><span data-stu-id="0245e-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="0245e-109">Developer</span><span class="sxs-lookup"><span data-stu-id="0245e-109">Developer</span></span>
* <span data-ttu-id="0245e-110">教育版、教育增强版和教育版 E5</span><span class="sxs-lookup"><span data-stu-id="0245e-110">Education, Education Plus, and Education E5</span></span>

> [!NOTE]
> <span data-ttu-id="0245e-111">有关 Microsoft 365 订阅详细信息，请参阅 [计划](https://products.office.com/business/compare-more-office-365-for-business-plans)。</span><span class="sxs-lookup"><span data-stu-id="0245e-111">For more information on Microsoft 365 subscriptions, see [plans](https://products.office.com/business/compare-more-office-365-for-business-plans).</span></span>
> 
> <span data-ttu-id="0245e-112">Microsoft Teams 还可供在停用前订阅 E4 [的客户使用](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)。</span><span class="sxs-lookup"><span data-stu-id="0245e-112">Microsoft Teams is also available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="create-your-development-environment"></a><span data-ttu-id="0245e-113">创建开发环境</span><span class="sxs-lookup"><span data-stu-id="0245e-113">Create your development environment</span></span>

<span data-ttu-id="0245e-114">如果你没有 Microsoft 365 帐户，则必须注册 [Microsoft 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program) 订阅。</span><span class="sxs-lookup"><span data-stu-id="0245e-114">If you do not have a Microsoft 365 account, you must sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="0245e-115">订阅将免费 90 天，并持续续订，只要将订阅用于开发活动。</span><span class="sxs-lookup"><span data-stu-id="0245e-115">The subscription is free for 90 days and continues to renew as long as you are using it for development activity.</span></span> <span data-ttu-id="0245e-116">如果你有企业版Visual Studio专业版订阅，这两个计划都包括免费的 Microsoft 365 [开发人员订阅](https://aka.ms/MyVisualStudioBenefits)。</span><span class="sxs-lookup"><span data-stu-id="0245e-116">If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits).</span></span> <span data-ttu-id="0245e-117">只要你的订阅处于活动状态，它Visual Studio有效。</span><span class="sxs-lookup"><span data-stu-id="0245e-117">It is active for as long as your Visual Studio subscription is active.</span></span> <span data-ttu-id="0245e-118">有关详细信息，请参阅设置 Microsoft [365 开发人员订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="0245e-118">For more inforamtion, see [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="0245e-119">为组织启用 Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="0245e-119">Enable Microsoft Teams for your organization</span></span>

<span data-ttu-id="0245e-120">为组织启用 Microsoft Teams，并查看为组织启用 [Teams 的详细指南](/microsoftteams/enable-features-office-365)。</span><span class="sxs-lookup"><span data-stu-id="0245e-120">Enable Microsoft Teams for your organization and take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="0245e-121">启用自定义 Teams 应用并启用自定义应用上传</span><span class="sxs-lookup"><span data-stu-id="0245e-121">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="0245e-122">**为开发人员租户启用自定义应用上传或旁加载**</span><span class="sxs-lookup"><span data-stu-id="0245e-122">**To turn on the custom app uploading or sideloading for your developer tenant**</span></span>

1. <span data-ttu-id="0245e-123">使用管理员凭据登录 [Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) 管理中心。</span><span class="sxs-lookup"><span data-stu-id="0245e-123">Sign in to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credentials.</span></span>

2. <span data-ttu-id="0245e-124">选择 **"显示所有**  >  **团队"。**</span><span class="sxs-lookup"><span data-stu-id="0245e-124">Select **Show All** > **Teams**.</span></span>

    ![管理中心菜单的图像](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > <span data-ttu-id="0245e-126">可能需要 24 小时才能 **显示 Teams** 选项。</span><span class="sxs-lookup"><span data-stu-id="0245e-126">It can take up to 24 hours for the **Teams** option to appear.</span></span> <span data-ttu-id="0245e-127">可以将 [自定义应用上传到 Teams 环境](/microsoftteams/upload-custom-apps#validate) ，以在当时进行测试和验证。</span><span class="sxs-lookup"><span data-stu-id="0245e-127">You can [upload your custom app to a Teams environment](/microsoftteams/upload-custom-apps#validate) for testing and validation in that time.</span></span>

3. <span data-ttu-id="0245e-128">导航到 **Teams 应用**  >  **设置策略**  >  **全局**。</span><span class="sxs-lookup"><span data-stu-id="0245e-128">Navigate to **Teams apps** > **Setup Policies** > **Global**.</span></span>

   ![打开旁加载视图](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="0245e-130">将 **上传自定义应用** 切换至 **打开** 位置。</span><span class="sxs-lookup"><span data-stu-id="0245e-130">Toggle **upload custom apps** to the **on** position.</span></span>

5. <span data-ttu-id="0245e-131">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="0245e-131">Select **Save**.</span></span>
   <span data-ttu-id="0245e-132">测试租户可以允许自定义应用旁加载。</span><span class="sxs-lookup"><span data-stu-id="0245e-132">Your test tenant can permit custom app sideloading.</span></span>

    > [!Note]
    > <span data-ttu-id="0245e-133">旁加载可能需要 24 小时才能处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="0245e-133">It can take up to 24 hours for the sideloading to be active.</span></span> <span data-ttu-id="0245e-134">在此期间，可以使用 upload **for \<your tenant>** 测试应用。</span><span class="sxs-lookup"><span data-stu-id="0245e-134">During interim, you can use **upload for \<your tenant>** to test your app.</span></span>

    ![updload 应用视图](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="0245e-136">有关这些设置如何交互的完整信息，请参阅在 [Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) 中管理自定义应用策略和设置和在 Microsoft Teams 中管理 [应用设置策略](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)。</span><span class="sxs-lookup"><span data-stu-id="0245e-136">For complete information on how these settings interact, see [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>

## <a name="next-step"></a><span data-ttu-id="0245e-137">后续步骤</span><span class="sxs-lookup"><span data-stu-id="0245e-137">Next step</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="0245e-138">选择测试设置</span><span class="sxs-lookup"><span data-stu-id="0245e-138">Choose a test setup</span></span>](~/concepts/build-and-test/debug.md)
> 


