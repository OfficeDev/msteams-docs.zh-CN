---
title: 准备 Office 365 租户
description: 如何开始使用 Office 365 中的团队
keywords: 配置 Office 365 租户团队上载
ms.openlocfilehash: 62cd640196631f50c72762253ff1bd75a143337d
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673359"
---
# <a name="prepare-your-office-365-tenant"></a><span data-ttu-id="a38e7-104">准备 Office 365 租户</span><span class="sxs-lookup"><span data-stu-id="a38e7-104">Prepare your Office 365 tenant</span></span>

<span data-ttu-id="a38e7-105">若要为 Microsoft 团队开发应用程序，您必须是[Office 365 客户，且具有以下计划之一](https://products.office.com/business/compare-more-office-365-for-business-plans)。</span><span class="sxs-lookup"><span data-stu-id="a38e7-105">To develop apps for Microsoft Teams, you need to be an [Office 365 customer with one of the following plans](https://products.office.com/business/compare-more-office-365-for-business-plans).</span></span>

* <span data-ttu-id="a38e7-106">商业协作版</span><span class="sxs-lookup"><span data-stu-id="a38e7-106">Business Essentials</span></span>
* <span data-ttu-id="a38e7-107">商业高级版</span><span class="sxs-lookup"><span data-stu-id="a38e7-107">Business Premium</span></span>
* <span data-ttu-id="a38e7-108">企业版 E1、E3 和 E5</span><span class="sxs-lookup"><span data-stu-id="a38e7-108">Enterprise E1, E3, and E5</span></span>
* <span data-ttu-id="a38e7-109">Developer</span><span class="sxs-lookup"><span data-stu-id="a38e7-109">Developer</span></span>
* <span data-ttu-id="a38e7-110">教育版、教育版和教育版 E5</span><span class="sxs-lookup"><span data-stu-id="a38e7-110">Education, Education Plus, and Education E5</span></span>

<span data-ttu-id="a38e7-111">Microsoft 团队还将对在其退休前购买了 E4 的客户提供。</span><span class="sxs-lookup"><span data-stu-id="a38e7-111">Microsoft Teams will also be available to customers who purchased E4 prior to its retirement.</span></span>

## <a name="just-need-a-development-environment"></a><span data-ttu-id="a38e7-112">只需要开发环境？</span><span class="sxs-lookup"><span data-stu-id="a38e7-112">Just need a development environment?</span></span>

<span data-ttu-id="a38e7-113">如果当前没有 Office 365 帐户，可以注册[office 365 开发人员计划](https://dev.office.com/devprogram)以获取*免费*的90天（只要你将其用于开发活动，就可以续订，只要你使用它进行开发活动） Office 365 开发人员租户。</span><span class="sxs-lookup"><span data-stu-id="a38e7-113">If you don't currently have an Office 365 account, you can sign up for the [Office 365 Developer program](https://dev.office.com/devprogram) to get a *free* 90 days (can be renewed for as long as you're using it for development activity) Office 365 Developer Tenant.</span></span> <span data-ttu-id="a38e7-114">此帐户仅可用于测试目的。</span><span class="sxs-lookup"><span data-stu-id="a38e7-114">This account can only be used for testing purposes.</span></span> <span data-ttu-id="a38e7-115">有关[设置测试帐户](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec?ui=en-US&rs=en-US&ad=US)的详细信息，请参阅。</span><span class="sxs-lookup"><span data-stu-id="a38e7-115">See more information on [setting up your test accounts](https://support.office.com/article/Add-users-individually-or-in-bulk-to-Office-365-Admin-Help-1970f7d6-03b5-442f-b385-5880b9c256ec?ui=en-US&rs=en-US&ad=US).</span></span>

## <a name="enable-microsoft-teams-for-your-organization"></a><span data-ttu-id="a38e7-116">为你的组织启用 Microsoft 团队</span><span class="sxs-lookup"><span data-stu-id="a38e7-116">Enable Microsoft Teams for your organization</span></span>

<span data-ttu-id="a38e7-117">如果尚未为你的组织启用 Microsoft 团队，你将需要先执行此操作。</span><span class="sxs-lookup"><span data-stu-id="a38e7-117">If Microsoft Teams is not yet enabled for your organization, you'll need to do that first.</span></span> <span data-ttu-id="a38e7-118">请参阅我们为[你的组织启用团队](/microsoftteams/how-to-roll-out-teams)的详细指南。</span><span class="sxs-lookup"><span data-stu-id="a38e7-118">Take a look at our detailed guidance for [enabling Teams for your organization](/microsoftteams/how-to-roll-out-teams).</span></span>

## <a name="enable-custom-teams-apps-and-turn-on-custom-app-uploading"></a><span data-ttu-id="a38e7-119">启用自定义团队应用并启用自定义应用上传</span><span class="sxs-lookup"><span data-stu-id="a38e7-119">Enable custom Teams apps and turn on custom app uploading</span></span>

> <span data-ttu-id="a38e7-120">注意：如果你正在使用 O365 开发人员组织生成应用，则应已将这些设置配置为允许你生成、上传和测试应用。</span><span class="sxs-lookup"><span data-stu-id="a38e7-120">Note: If you're using an O365 Developer Organization to build your app, these settings should already be configured to allow you to build, upload and test your app.</span></span>

<span data-ttu-id="a38e7-121">启用自定义应用程序和自定义应用程序上载涉及以下三个设置：</span><span class="sxs-lookup"><span data-stu-id="a38e7-121">There are three settings involved in enabling custom apps and custom app uploading:</span></span>

* <span data-ttu-id="a38e7-122">**组织范围内的自定义应用设置**-此设置可启用或禁用组织的自定义应用程序。</span><span class="sxs-lookup"><span data-stu-id="a38e7-122">**Org-wide custom app setting** - This setting either enables or disables custom apps for your organization.</span></span> <span data-ttu-id="a38e7-123">需要打开它。</span><span class="sxs-lookup"><span data-stu-id="a38e7-123">It needs to be on.</span></span> 
* <span data-ttu-id="a38e7-124">**团队自定义应用设置**-此设置适用于 Microsoft 团队中的每个团队。</span><span class="sxs-lookup"><span data-stu-id="a38e7-124">**Team custom app setting** - This setting is for each individual team inside Microsoft Teams.</span></span> <span data-ttu-id="a38e7-125">如果要为特定团队安装您的应用程序，则需要为该团队启用此项。</span><span class="sxs-lookup"><span data-stu-id="a38e7-125">If you want to install your app for a specific team, this will need to be on for that team.</span></span>
* <span data-ttu-id="a38e7-126">**用户自定义应用程序策略**-此设置可控制单个用户的权限。</span><span class="sxs-lookup"><span data-stu-id="a38e7-126">**User custom app policy** - This set of settings controls the permissions for an individual user.</span></span> <span data-ttu-id="a38e7-127">你需要为你想要上载自定义应用的个人启用此。</span><span class="sxs-lookup"><span data-stu-id="a38e7-127">You'll need to enable this for individuals you want to upload custom apps.</span></span>

<span data-ttu-id="a38e7-128">有关这些设置如何交互的完整信息，请参阅在[Microsoft 团队中管理自定义应用程序策略和设置](/MicrosoftTeams/teams-custom-app-policies-and-settings)。</span><span class="sxs-lookup"><span data-stu-id="a38e7-128">For complete information on how these settings interact see [Manage custom app policies and settings in Microsoft Teams](/MicrosoftTeams/teams-custom-app-policies-and-settings).</span></span>
