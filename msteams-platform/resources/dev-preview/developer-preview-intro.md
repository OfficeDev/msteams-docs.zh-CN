---
title: 开发者预览版
description: 介绍公共服务开发者预览版中的Microsoft Teams
ms.topic: conceptual
localization_priority: Normal
keywords: teams 预览开发人员功能
ms.openlocfilehash: f19268afd81fe9fa7ae2116740e7b9d4ff8225cb
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52019718"
---
# <a name="public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="201f0-104">公共开发人员预览版Microsoft Teams</span><span class="sxs-lookup"><span data-stu-id="201f0-104">Public developer preview for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="201f0-105">预览版中包含的功能可能不完整，在公开发布之前可能会发生更改。</span><span class="sxs-lookup"><span data-stu-id="201f0-105">Features included in preview may not be complete, and may undergo changes before becoming available in the public release.</span></span> <span data-ttu-id="201f0-106">它们仅供测试和探索使用。</span><span class="sxs-lookup"><span data-stu-id="201f0-106">They are provided for testing and exploration purposes only.</span></span> <span data-ttu-id="201f0-107">它们不应在生产应用程序中使用。</span><span class="sxs-lookup"><span data-stu-id="201f0-107">They should not be used in production applications.</span></span>

<span data-ttu-id="201f0-108">开发者预览版是一个针对开发人员的公共计划，提供对开发人员中未Microsoft Teams。</span><span class="sxs-lookup"><span data-stu-id="201f0-108">Developer Preview is a public program for developers which provides early access to unreleased features in Microsoft Teams.</span></span> <span data-ttu-id="201f0-109">这允许你浏览和测试即将推出的功能，以潜在地包含在Microsoft Teams应用中。</span><span class="sxs-lookup"><span data-stu-id="201f0-109">This allows you to explore and test upcoming features for potential inclusion in your Microsoft Teams app.</span></span> <span data-ttu-id="201f0-110">我们还欢迎 [提供有关开发人员](~/feedback.md) 预览版中任何功能的反馈。</span><span class="sxs-lookup"><span data-stu-id="201f0-110">We also welcome [feedback](~/feedback.md) on any feature in developer preview.</span></span> <span data-ttu-id="201f0-111">开发人员预览Microsoft Teams客户端启用，因此无需担心影响整个组织。</span><span class="sxs-lookup"><span data-stu-id="201f0-111">Developer preview is enabled per Microsoft Teams client, so you don't need to worry about affecting your entire organization.</span></span>

## <a name="developer-preview-app-manifest"></a><span data-ttu-id="201f0-112">开发人员预览应用清单</span><span class="sxs-lookup"><span data-stu-id="201f0-112">Developer preview app manifest</span></span>

<span data-ttu-id="201f0-113">开发人员预览版中启用的许多功能都需要更改应用清单 JSON 文件。</span><span class="sxs-lookup"><span data-stu-id="201f0-113">Many features enabled in developer preview will require alterations to your app manifest JSON file.</span></span> <span data-ttu-id="201f0-114">为此，将需要使用开发人员预览清单架构 如果[](~/resources/schema/manifest-schema-dev-preview.md)使用此架构，你将不能使用[App Studio](~/concepts/build-and-test/app-studio-overview.md)进行这些更改，也不能使用它上载应用进行测试。</span><span class="sxs-lookup"><span data-stu-id="201f0-114">To do so you'll need to use the [developer preview manifest schema](~/resources/schema/manifest-schema-dev-preview.md) If you use this schema, you will not be able to use [App Studio](~/concepts/build-and-test/app-studio-overview.md) to make these changes, nor will you be able to use it to upload your app for testing.</span></span> <span data-ttu-id="201f0-115">若要上传应用，你需要单击应用栏上的 `More apps` 图标，然后选择 `Upload a custom app link` 。</span><span class="sxs-lookup"><span data-stu-id="201f0-115">To upload your app you'll need to click the `More apps` icon on the app bar, then select the `Upload a custom app link`.</span></span> <span data-ttu-id="201f0-116">使用此方法，你只能上传应用包的压缩版本。</span><span class="sxs-lookup"><span data-stu-id="201f0-116">Using this method you can only upload a zipped version of your app package.</span></span>

<span data-ttu-id="201f0-117">你可能会发现使用 App Studio 创建应用包的非开发人员预览部分非常有用，然后导出该包并手动编辑文件以添加想要使用的开发人员预览 `manifest.json` 功能。</span><span class="sxs-lookup"><span data-stu-id="201f0-117">You may find it useful to use App Studio to create the non-developer preview portions of your app package, then export that package and manually edit the `manifest.json` file to add the developer preview features you wish to use.</span></span> <span data-ttu-id="201f0-118">将开发人员预览功能添加到文件后，将无法将程序包重新导入 `manifest.json` App Studio。</span><span class="sxs-lookup"><span data-stu-id="201f0-118">Once you've added developer preview features to the `manifest.json` file you will not be able to re-import the package into App Studio.</span></span>

## <a name="enable-developer-preview"></a><span data-ttu-id="201f0-119">启用开发人员预览</span><span class="sxs-lookup"><span data-stu-id="201f0-119">Enable developer preview</span></span>

<span data-ttu-id="201f0-120">基于每个客户端启用开发人员预览，但启用开发人员预览的选项在组织级别控制。</span><span class="sxs-lookup"><span data-stu-id="201f0-120">Developer preview is enabled on a per-client basis, but the option to turn on developer preview is controlled at the organization level.</span></span> <span data-ttu-id="201f0-121">若要启用为个人启用开发人员预览的选项，必须确保他们能够上传自定义应用。</span><span class="sxs-lookup"><span data-stu-id="201f0-121">To enable the option to turn on developer preview for an individual, you must ensure that they have the ability to upload custom apps.</span></span> <span data-ttu-id="201f0-122">有关 [其他信息，](~/concepts/build-and-test/prepare-your-o365-tenant.md) 请参阅设置租户。</span><span class="sxs-lookup"><span data-stu-id="201f0-122">See [setting up your tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md) for additional information.</span></span>

<span data-ttu-id="201f0-123">使用包含开发人员预览功能的应用可能会导致未启用开发人员预览的客户端发生意外行为。</span><span class="sxs-lookup"><span data-stu-id="201f0-123">Using an app that contains developer preview features may cause clients that have not enabled developer preview to behave unexpectedly.</span></span> <span data-ttu-id="201f0-124">如果未看到开发人员预览条目，最可能的原因是您的组织未配置应用上载。</span><span class="sxs-lookup"><span data-stu-id="201f0-124">If you do not see an entry for developer preview the most likely reason is your organization is not configured for app uploading.</span></span>

### <a name="on-a-desktop-or-web-client"></a><span data-ttu-id="201f0-125">在桌面或 Web 客户端上</span><span class="sxs-lookup"><span data-stu-id="201f0-125">On a desktop or web client</span></span>

<span data-ttu-id="201f0-126">若要在桌面或 Web 客户端上启用公共开发人员预览，需要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="201f0-126">To enable the public developer preview on a desktop or web client, you need to do the following:</span></span>

1. <span data-ttu-id="201f0-127">在租户的管理控制台中启用应用上传，如下 [所述](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="201f0-127">Enabling uploading of apps in the admin console of your tenant as described [here](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>
1. <span data-ttu-id="201f0-128">单击你的配置文件 (右上方或左下角Teams显示) 菜单Teams菜单。</span><span class="sxs-lookup"><span data-stu-id="201f0-128">Click on your profile (either in the upper right or lower left of the Teams interface) to display the Teams menu.</span></span>
1. <span data-ttu-id="201f0-129">选择"关于→开发人员预览"。</span><span class="sxs-lookup"><span data-stu-id="201f0-129">Select About → Developer preview.</span></span>
1. <span data-ttu-id="201f0-130">选择 **切换到开发人员预览**。</span><span class="sxs-lookup"><span data-stu-id="201f0-130">Select **Switch to Developer preview**.</span></span>

### <a name="on-a-mobile-client"></a><span data-ttu-id="201f0-131">在移动客户端上</span><span class="sxs-lookup"><span data-stu-id="201f0-131">On a mobile client</span></span>

<span data-ttu-id="201f0-132">若要在移动客户端上启用公共开发人员预览版，需要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="201f0-132">To enable the public developer preview on a mobile client, you need to do the following:</span></span>

1. <span data-ttu-id="201f0-133">在租户的管理控制台中启用应用上传，如下 [所述](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="201f0-133">Enabling uploading of apps in the admin console of your tenant as described [here](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>
1. <span data-ttu-id="201f0-134">打开左上方的汉堡包菜单，然后选择 **"设置"。**</span><span class="sxs-lookup"><span data-stu-id="201f0-134">Open the hamburger menu on the top left, then select **Settings**.</span></span>
1. <span data-ttu-id="201f0-135">选择 **"关于"。**</span><span class="sxs-lookup"><span data-stu-id="201f0-135">Select **About**.</span></span>
1. <span data-ttu-id="201f0-136">单击"开发人员预览"切换。</span><span class="sxs-lookup"><span data-stu-id="201f0-136">Click the Developer preview toggle.</span></span>

## <a name="disable-developer-preview"></a><span data-ttu-id="201f0-137">禁用开发人员预览</span><span class="sxs-lookup"><span data-stu-id="201f0-137">Disable developer preview</span></span>

<span data-ttu-id="201f0-138">使用"关于开发人员预览→"下的同一菜单项，然后单击它将其关闭。</span><span class="sxs-lookup"><span data-stu-id="201f0-138">Use the same menu item under About → Developer preview, and click on it to turn it off.</span></span>

## <a name="features-available-in-developer-preview"></a><span data-ttu-id="201f0-139">开发人员预览版中提供的功能</span><span class="sxs-lookup"><span data-stu-id="201f0-139">Features available in developer preview</span></span>

<span data-ttu-id="201f0-140">有关当前在开发人员预览版中启用的功能的完整列表，请参阅： [公共开发人员预览版中的功能](../../resources/dev-preview/developer-preview-features.md)。</span><span class="sxs-lookup"><span data-stu-id="201f0-140">For a full list of the features currently enabled in developer preview see: [Features in the public developer preview](../../resources/dev-preview/developer-preview-features.md).</span></span>
