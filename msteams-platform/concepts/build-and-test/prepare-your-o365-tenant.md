---
title: 准备 Office 365 租户
description: 如何开始使用 Office 365 中的团队
keywords: 配置 Office 365 租户团队上载
ms.openlocfilehash: 35f102223a5f8e6a8e12268e22aedca07a61b1fa
ms.sourcegitcommit: 058b7bbd817af5f513e0e018f2ef562dc3086a84
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/03/2020
ms.locfileid: "43120267"
---
# <a name="prepare-your-office-365-tenant"></a><span data-ttu-id="3ab50-104">准备 Office 365 租户</span><span class="sxs-lookup"><span data-stu-id="3ab50-104">Prepare your Office 365 tenant</span></span>

<span data-ttu-id="3ab50-105">如果你是 Office 365 订阅者，则可以使用以下[计划](https://products.office.com/business/compare-more-office-365-for-business-plans)之一为 Microsoft 团队开发应用程序：</span><span class="sxs-lookup"><span data-stu-id="3ab50-105">If you are an Office 365 subscriber, you can develop apps for Microsoft Teams with one of the following [plans](https://products.office.com/business/compare-more-office-365-for-business-plans):</span></span>

* <span data-ttu-id="3ab50-106">商业协作版</span><span class="sxs-lookup"><span data-stu-id="3ab50-106">Business Essentials</span></span>
* <span data-ttu-id="3ab50-107">商业高级版</span><span class="sxs-lookup"><span data-stu-id="3ab50-107">Business Premium</span></span>
* <span data-ttu-id="3ab50-108">企业版 E1、E3 和 E5</span><span class="sxs-lookup"><span data-stu-id="3ab50-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="3ab50-109">Developer</span><span class="sxs-lookup"><span data-stu-id="3ab50-109">Developer</span></span>
* <span data-ttu-id="3ab50-110">教育版、教育版和教育版 E5</span><span class="sxs-lookup"><span data-stu-id="3ab50-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="3ab50-111">Microsoft 团队还将对在其[退休](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147)前订阅 E4 的客户提供。</span><span class="sxs-lookup"><span data-stu-id="3ab50-111">Microsoft Teams will also be available to customers who subscribed to E4 prior to its [retirement](https://support.office.com//article/important-information-for-office-365-enterprise-e4-customers-f9572348-43a2-43fa-a3d8-3b6c9c042147).</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="3ab50-112">只需要开发环境？</span><span class="sxs-lookup"><span data-stu-id="3ab50-112">Just need a development environment?</span></span>

<span data-ttu-id="3ab50-113">如果当前没有 Office 365 帐户，可以注册[office 365 开发人员计划](https://developer.microsoft.com/microsoft-365/dev-program)订阅。</span><span class="sxs-lookup"><span data-stu-id="3ab50-113">If you don't currently have an Office 365 account, you can sign up for an [Office 365 Developer Program](https://developer.microsoft.com/microsoft-365/dev-program) subscription.</span></span> <span data-ttu-id="3ab50-114">它在90天内*免费*使用，并且将持续更新，只要你将其用于开发活动即可。</span><span class="sxs-lookup"><span data-stu-id="3ab50-114">It's *free* for 90 days and will continually renew as long as you're using it for development activity.</span></span> <span data-ttu-id="3ab50-115">如果您有 Visual Studio *Enterprise*或*专业*订阅，这两个程序都包括免费的 Office 365[开发人员订阅](https://aka.ms/MyVisualStudioBenefits)（在 visual Studio 订阅的生命周期内处于活动状态）。</span><span class="sxs-lookup"><span data-stu-id="3ab50-115">If you have a Visual Studio *Enterprise* or *Professional* subscription, both programs include a free Office 365 [developer subscription](https://aka.ms/MyVisualStudioBenefits), active for the life of your Visual Studio subscription.</span></span> <span data-ttu-id="3ab50-116">*请参阅*[设置 Microsoft 365 开发人员订阅](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started)。</span><span class="sxs-lookup"><span data-stu-id="3ab50-116">*See* [Set up a Microsoft 365 developer subscription](https://docs.microsoft.com/office/developer-program/office-365-developer-program-get-started).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="3ab50-117">为你的组织启用 Microsoft 团队</span><span class="sxs-lookup"><span data-stu-id="3ab50-117">Enable Microsoft Teams for your organization</span></span>

<span data-ttu-id="3ab50-118">如果尚未为你的组织启用 Microsoft 团队，你将需要先执行此操作。</span><span class="sxs-lookup"><span data-stu-id="3ab50-118">If Microsoft Teams has not been enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="3ab50-119">请参阅我们为[你的组织启用团队](https://docs.microsoft.com/microsoftteams/enable-features-office-365)的详细指南。</span><span class="sxs-lookup"><span data-stu-id="3ab50-119">Take a look at our detailed guidance for [enabling Teams for your organization](https://docs.microsoft.com/microsoftteams/enable-features-office-365).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="3ab50-120">启用自定义团队应用并启用自定义应用上传</span><span class="sxs-lookup"><span data-stu-id="3ab50-120">Enable custom Teams apps and turn on custom app uploading</span></span>

> [!Note] 
> <span data-ttu-id="3ab50-121">如果使用的是 Office 365 开发人员平台来构建应用程序，则应已将这些设置配置为允许您生成、上载和测试应用程序。</span><span class="sxs-lookup"><span data-stu-id="3ab50-121">If you're using the Office 365 developer platform to build your app, these settings should already be configured to allow you to build, upload, and test your app.</span></span>

<span data-ttu-id="3ab50-122">有三个与启用自定义应用程序和自定义应用程序上载相关的设置：</span><span class="sxs-lookup"><span data-stu-id="3ab50-122">There are three settings relevant to enabling custom apps and custom app uploading:</span></span>

* <span data-ttu-id="3ab50-123">**组织范围的自定义应用设置** => **允许与中的自定义应用** => **On**程序进行交互—此设置可启用或禁用组织的自定义应用程序。</span><span class="sxs-lookup"><span data-stu-id="3ab50-123">**Org-wide custom app setting** => **Allow interaction with custom apps** => **On** — This setting enables or disables custom apps for your organization.</span></span> <span data-ttu-id="3ab50-124">需要打开它。</span><span class="sxs-lookup"><span data-stu-id="3ab50-124">It needs to be on.</span></span> 
* <span data-ttu-id="3ab50-125">**团队自定义应用设置** => **允许成员上载自定义应用程序** => **打开/关闭**—此设置适用于 Microsoft 团队中的每个单独团队。</span><span class="sxs-lookup"><span data-stu-id="3ab50-125">**Team custom app setting** => **Allow members to upload custom apps** => **On/Off** — This setting applies to each individual team inside Microsoft Teams.</span></span> <span data-ttu-id="3ab50-126">如果要为特定团队安装您的应用程序，则需要为该团队启用此项。</span><span class="sxs-lookup"><span data-stu-id="3ab50-126">If you want to install your app for a specific team, this will need to be on for that team.</span></span>
* <span data-ttu-id="3ab50-127">**用户自定义应用程序策略** => **用户可以上传自定义应用程序** => **On/Off** ，此设置控制单个用户的权限。</span><span class="sxs-lookup"><span data-stu-id="3ab50-127">**User custom app policy** => **User can upload custom apps** => **On/Off** — This setting controls the permissions for an individual user.</span></span> <span data-ttu-id="3ab50-128">你需要为允许上传自定义应用的个人启用此。</span><span class="sxs-lookup"><span data-stu-id="3ab50-128">You'll need to enable this for individuals that are allowed to upload custom apps.</span></span>

<span data-ttu-id="3ab50-129">有关这些设置如何交互的完整信息，*请参阅*在 microsoft 团队中[管理自定义应用策略和设置](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings)和[管理 microsoft 团队中的应用程序设置策略](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies)。</span><span class="sxs-lookup"><span data-stu-id="3ab50-129">For complete information on how these settings interact, *see* [Manage custom app policies and settings in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-custom-app-policies-and-settings) and [Manage app setup policies in Microsoft Teams](https://docs.microsoft.com/microsoftteams/teams-app-setup-policies).</span></span>
