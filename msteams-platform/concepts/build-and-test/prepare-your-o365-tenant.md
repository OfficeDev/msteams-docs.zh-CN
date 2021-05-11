---
title: 准备 Microsoft 365 租户
description: 如何开始使用Teams Microsoft 365
ms.topic: how-to
localization_priority: Normal
keywords: 配置Microsoft 365租户Teams上载
ms.openlocfilehash: 45d6dfb57fd2faa5bb303aac1dff86be142d0dc2
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019942"
---
# <a name="prepare-your-microsoft-365-tenant"></a><span data-ttu-id="ff05a-104">准备 Microsoft 365 租户</span><span class="sxs-lookup"><span data-stu-id="ff05a-104">Prepare your Microsoft 365 tenant</span></span>

<span data-ttu-id="ff05a-105">Microsoft 365订阅者可以使用以下Microsoft Teams之一开发适用于用户的应用程序：</span><span class="sxs-lookup"><span data-stu-id="ff05a-105">Microsoft 365 subscribers can develop apps for Microsoft Teams with one of the following plans:</span></span>

* <span data-ttu-id="ff05a-106">基本</span><span class="sxs-lookup"><span data-stu-id="ff05a-106">Basic</span></span>
* <span data-ttu-id="ff05a-107">标准</span><span class="sxs-lookup"><span data-stu-id="ff05a-107">Standard</span></span>
* <span data-ttu-id="ff05a-108">EnterpriseE1、E3 和 E5</span><span class="sxs-lookup"><span data-stu-id="ff05a-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="ff05a-109">Developer</span><span class="sxs-lookup"><span data-stu-id="ff05a-109">Developer</span></span>
* <span data-ttu-id="ff05a-110">教育版、教育增强版和教育版 E5</span><span class="sxs-lookup"><span data-stu-id="ff05a-110">Education, Education Plus, and Education E5</span></span>

> [!NOTE]
> * <span data-ttu-id="ff05a-111">有关订阅Microsoft 365，请参阅[计划](https://products.office.com/business/compare-more-office-365-for-business-plans)。</span><span class="sxs-lookup"><span data-stu-id="ff05a-111">For more information on Microsoft 365 subscriptions, see [plans](https://products.office.com/business/compare-more-office-365-for-business-plans).</span></span>
> * <span data-ttu-id="ff05a-112">Teams停用之前订阅 E4 的客户也[可用](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)。</span><span class="sxs-lookup"><span data-stu-id="ff05a-112">Teams is also available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="create-your-development-environment"></a><span data-ttu-id="ff05a-113">创建开发环境</span><span class="sxs-lookup"><span data-stu-id="ff05a-113">Create your development environment</span></span>

<span data-ttu-id="ff05a-114">如果你没有帐户，Microsoft 365注册开发人员计划Microsoft 365[订阅](https://developer.microsoft.com/microsoft-365/dev-program)。</span><span class="sxs-lookup"><span data-stu-id="ff05a-114">If you do not have a Microsoft 365 account, you must sign up for a [Microsoft 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="ff05a-115">订阅将免费 90 天，并持续续订，只要将订阅用于开发活动。</span><span class="sxs-lookup"><span data-stu-id="ff05a-115">The subscription is free for 90 days and continues to renew as long as you are using it for development activity.</span></span> <span data-ttu-id="ff05a-116">如果你有一个Visual Studio Enterprise或Professional订阅，这两个计划均包括免费Microsoft 365[开发人员订阅](https://aka.ms/MyVisualStudioBenefits)。</span><span class="sxs-lookup"><span data-stu-id="ff05a-116">If you have a Visual Studio Enterprise or Professional subscription, both programs include a free Microsoft 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits).</span></span> <span data-ttu-id="ff05a-117">只要你的订阅处于活动状态，Visual Studio就有效。</span><span class="sxs-lookup"><span data-stu-id="ff05a-117">It is active as long as your Visual Studio subscription is active.</span></span> <span data-ttu-id="ff05a-118">有关详细信息，请参阅[设置开发人员Microsoft 365订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="ff05a-118">For more information, see [set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-teams-for-your-organization"></a><span data-ttu-id="ff05a-119">为Teams启用管理</span><span class="sxs-lookup"><span data-stu-id="ff05a-119">Enable Teams for your organization</span></span>

<span data-ttu-id="ff05a-120">Enable Teams for your organization and for more information， see [enabling Teams for your organization](/microsoftteams/enable-features-office-365).</span><span class="sxs-lookup"><span data-stu-id="ff05a-120">Enable Teams for your organization and for more information, see [enabling Teams for your organization](/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="ff05a-121">启用自定义Teams应用并启用自定义应用上传</span><span class="sxs-lookup"><span data-stu-id="ff05a-121">Enable custom Teams apps and turn on custom app uploading</span></span>

<span data-ttu-id="ff05a-122">**为开发人员租户启用自定义应用上传或旁加载**</span><span class="sxs-lookup"><span data-stu-id="ff05a-122">**To turn on the custom app uploading or sideloading for your developer tenant**</span></span>

1. <span data-ttu-id="ff05a-123">使用管理员[Microsoft 365](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/)登录管理中心。</span><span class="sxs-lookup"><span data-stu-id="ff05a-123">Sign in to [Microsoft 365 admin center](https://admin.microsoft.com/Adminportal/Home?source=applauncher#/homepage#/) with your admin credentials.</span></span>

2. <span data-ttu-id="ff05a-124">选择 **"显示所有**  >  **Teams"。**</span><span class="sxs-lookup"><span data-stu-id="ff05a-124">Select **Show All** > **Teams**.</span></span>

    ![管理中心菜单](~/assets/images/prepare-test-tenant/admin-center.png)

    > [!Note]
    > <span data-ttu-id="ff05a-126">可能需要 24 小时才能显示 **Teams选项。**</span><span class="sxs-lookup"><span data-stu-id="ff05a-126">It can take up to 24 hours for the **Teams** option to appear.</span></span> <span data-ttu-id="ff05a-127">可以将[自定义应用上传到Teams环境中](/microsoftteams/upload-custom-apps#validate)进行测试和验证。</span><span class="sxs-lookup"><span data-stu-id="ff05a-127">You can [upload your custom app to a Teams environment](/microsoftteams/upload-custom-apps#validate) for testing and validation in that time.</span></span>

3. <span data-ttu-id="ff05a-128">导航到 **Teams**  >  **应用设置策略**  >  **全局 。**</span><span class="sxs-lookup"><span data-stu-id="ff05a-128">Navigate to **Teams apps** > **Setup Policies** > **Global**.</span></span>

   ![打开旁加载视图](~/assets/images/prepare-test-tenant/turn-on-sideload.png)

4. <span data-ttu-id="ff05a-130">将 **Upload应用切换到\*\*\*\*"打开"** 位置。</span><span class="sxs-lookup"><span data-stu-id="ff05a-130">Toggle **Upload custom apps** to the **On** position.</span></span>

5. <span data-ttu-id="ff05a-131">选择“**保存**”。</span><span class="sxs-lookup"><span data-stu-id="ff05a-131">Select **Save**.</span></span> <span data-ttu-id="ff05a-132">测试租户可以允许自定义应用旁加载。</span><span class="sxs-lookup"><span data-stu-id="ff05a-132">Your test tenant can permit custom app sideloading.</span></span>

    > [!Note]
    > <span data-ttu-id="ff05a-133">旁加载可能需要 24 小时才能处于活动状态。</span><span class="sxs-lookup"><span data-stu-id="ff05a-133">It can take up to 24 hours for the sideloading to be active.</span></span> <span data-ttu-id="ff05a-134">临时，可以使用 **upload for \<your tenant>** 测试应用。</span><span class="sxs-lookup"><span data-stu-id="ff05a-134">In the interim, you can use **upload for \<your tenant>** to test your app.</span></span> <span data-ttu-id="ff05a-135">若要上传.zip包文件，请参阅上传 [自定义应用](/microsoftteams/upload-custom-apps#upload)。</span><span class="sxs-lookup"><span data-stu-id="ff05a-135">To upload the .zip package file of the app, see [upload custom apps](/microsoftteams/upload-custom-apps#upload).</span></span>

    ![Upload应用视图](~/assets/images/prepare-test-tenant/upload-for-contoso.png)

<span data-ttu-id="ff05a-137">有关这些设置如何交互的完整信息，请参阅管理[](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)Teams 中的自定义应用策略和设置[Teams。](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)</span><span class="sxs-lookup"><span data-stu-id="ff05a-137">For complete information on how these settings interact, see [manage custom app policies and settings in Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [manage app setup policies in Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>

## <a name="next-step"></a><span data-ttu-id="ff05a-138">后续步骤</span><span class="sxs-lookup"><span data-stu-id="ff05a-138">Next step</span></span>

> [!div class="nextstepaction"] 
> [<span data-ttu-id="ff05a-139">选择测试设置</span><span class="sxs-lookup"><span data-stu-id="ff05a-139">Choose a test setup</span></span>](~/concepts/build-and-test/debug.md)

