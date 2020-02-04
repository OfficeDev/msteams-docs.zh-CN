---
title: 开发人员预览版
description: 介绍 Microsoft 团队的公共开发人员预览版中的功能
keywords: 团队预览开发人员功能
ms.openlocfilehash: a09e715e4e2d4aba72726cc96c4d248c550a3ab1
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673288"
---
# <a name="public-developer-preview-for-microsoft-teams"></a><span data-ttu-id="9d4b6-104">Microsoft 团队的公共开发人员预览版</span><span class="sxs-lookup"><span data-stu-id="9d4b6-104">Public developer preview for Microsoft Teams</span></span>

>[!NOTE]
><span data-ttu-id="9d4b6-105">预览中包含的功能可能不完整，并且可能会在公开发布之前获得更改。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-105">Features included in preview may not be complete, and may undergo changes before becoming available in the public release.</span></span> <span data-ttu-id="9d4b6-106">仅提供它们用于测试和研究目的。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-106">They are provided for testing and exploration purposes only.</span></span> <span data-ttu-id="9d4b6-107">不应在生产应用程序中使用它们。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-107">They should not be used in production applications.</span></span>

<span data-ttu-id="9d4b6-108">开发人员预览版是为开发人员提供对 Microsoft 团队中的 unreleased 功能的早期访问的公共计划。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-108">Developer Preview is a public program for developers which provides early access to unreleased features in Microsoft Teams.</span></span> <span data-ttu-id="9d4b6-109">这使您可以探索和测试即将推出的功能，以便在 Microsoft 团队应用中可能包含这些功能。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-109">This allows you to explore and test upcoming features for potential inclusion in your Microsoft Teams app.</span></span> <span data-ttu-id="9d4b6-110">我们还欢迎对开发人员预览版中的任何功能提供[反馈](~/feedback.md)。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-110">We also welcome [feedback](~/feedback.md) on any feature in developer preview.</span></span> <span data-ttu-id="9d4b6-111">根据 Microsoft 团队客户端启用开发人员预览，因此无需担心会影响整个组织。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-111">Developer preview is enabled per Microsoft Teams client, so you don't need to worry about affecting your entire organization.</span></span>

## <a name="developer-preview-app-manifest"></a><span data-ttu-id="9d4b6-112">开发人员预览版应用程序清单</span><span class="sxs-lookup"><span data-stu-id="9d4b6-112">Developer preview app manifest</span></span>

<span data-ttu-id="9d4b6-113">在开发人员预览中启用的许多功能都需要对应用程序清单 JSON 文件进行变更。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-113">Many features enabled in developer preview will require alterations to your app manifest JSON file.</span></span> <span data-ttu-id="9d4b6-114">若要执行此操作，您需要使用[开发人员预览版清单架构](~/resources/schema/manifest-schema-dev-preview.md)。如果使用此架构，将无法使用[应用程序 Studio](~/concepts/build-and-test/app-studio-overview.md)进行这些更改，也不能使用它上传您的应用程序进行测试。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-114">To do so you'll need to use the [developer preview manifest schema](~/resources/schema/manifest-schema-dev-preview.md) If you use this schema, you will not be able to use [App Studio](~/concepts/build-and-test/app-studio-overview.md) to make these changes, nor will you be able to use it to upload your app for testing.</span></span> <span data-ttu-id="9d4b6-115">若要上传您的应用程序，您`More apps`需要单击应用栏上的图标，然后`Upload a custom app link`选择。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-115">To upload your app you'll need to click the `More apps` icon on the app bar, then select the `Upload a custom app link`.</span></span> <span data-ttu-id="9d4b6-116">使用此方法，您只能上载应用程序包的压缩版本。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-116">Using this method you can only upload a zipped version of your app package.</span></span>

<span data-ttu-id="9d4b6-117">您可能会发现，使用应用程序 Studio 创建应用程序包的非开发人员预览部分会非常有用，然后导出该程序包并手动编辑该`manifest.json`文件，以添加您想要使用的开发人员预览功能。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-117">You may find it useful to use App Studio to create the non-developer preview portions of your app package, then export that package and manually edit the `manifest.json` file to add the developer preview features you wish to use.</span></span> <span data-ttu-id="9d4b6-118">将开发人员预览功能添加到`manifest.json`文件后，将无法将包重新导入到应用程序 Studio 中。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-118">Once you've added developer preview features to the `manifest.json` file you will not be able to re-import the package into App Studio.</span></span>

## <a name="enable-developer-preview"></a><span data-ttu-id="9d4b6-119">启用开发人员预览</span><span class="sxs-lookup"><span data-stu-id="9d4b6-119">Enable developer preview</span></span>

<span data-ttu-id="9d4b6-120">以每个客户端为基础启用开发人员预览，但在组织级别控制启用开发人员预览的选项。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-120">Developer preview is enabled on a per-client basis, but the option to turn on developer preview is controlled at the organization level.</span></span> <span data-ttu-id="9d4b6-121">若要启用选项以启用个人的开发人员预览版，必须确保能够上载自定义应用程序。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-121">To enable the option to turn on developer preview for an individual, you must ensure that they have the ability to upload custom apps.</span></span> <span data-ttu-id="9d4b6-122">有关详细信息，请参阅[设置你的租户](~/concepts/build-and-test/prepare-your-o365-tenant.md)。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-122">See [setting up your tenant](~/concepts/build-and-test/prepare-your-o365-tenant.md) for additional information.</span></span>

<span data-ttu-id="9d4b6-123">使用包含开发人员预览功能的应用可能会导致未启用开发人员预览的客户端出现意外行为。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-123">Using an app that contains developer preview features may cause clients that have not enabled developer preview to behave unexpectedly.</span></span> <span data-ttu-id="9d4b6-124">如果看不到 "开发人员预览" 条目，最可能的原因是您的组织未配置为应用上载。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-124">If you do not see an entry for developer preview the most likely reason is your organization is not configured for app uploading.</span></span>

### <a name="on-a-desktop-or-web-client"></a><span data-ttu-id="9d4b6-125">在桌面或 web 客户端上</span><span class="sxs-lookup"><span data-stu-id="9d4b6-125">On a desktop or web client</span></span>

<span data-ttu-id="9d4b6-126">若要在桌面或 web 客户端上启用公共开发人员预览，您需要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="9d4b6-126">To enable the public developer preview on a desktop or web client, you need to do the following:</span></span>

1. <span data-ttu-id="9d4b6-127">在租户的管理员控制台中启用上传应用程序[，如下所述。](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="9d4b6-127">Enabling uploading of apps in the admin console of your tenant as described [here](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>
1. <span data-ttu-id="9d4b6-128">单击您的配置文件（位于团队界面的右上角或左下方）以显示 "团队" 菜单。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-128">Click on your profile (either in the upper right or lower left of the Teams interface) to display the Teams menu.</span></span>
1. <span data-ttu-id="9d4b6-129">选择 "关于→开发人员预览"。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-129">Select About → Developer preview.</span></span>
1. <span data-ttu-id="9d4b6-130">选择 "**切换到开发人员预览**"。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-130">Select **Switch to Developer preview**.</span></span>

### <a name="on-a-mobile-client"></a><span data-ttu-id="9d4b6-131">在移动客户端上</span><span class="sxs-lookup"><span data-stu-id="9d4b6-131">On a mobile client</span></span>

<span data-ttu-id="9d4b6-132">若要在移动客户端上启用公共开发人员预览，您需要执行以下操作：</span><span class="sxs-lookup"><span data-stu-id="9d4b6-132">To enable the public developer preview on a mobile client, you need to do the following:</span></span>

1. <span data-ttu-id="9d4b6-133">在租户的管理员控制台中启用上传应用程序[，如下所述。](~/concepts/build-and-test/prepare-your-o365-tenant.md)</span><span class="sxs-lookup"><span data-stu-id="9d4b6-133">Enabling uploading of apps in the admin console of your tenant as described [here](~/concepts/build-and-test/prepare-your-o365-tenant.md).</span></span>
1. <span data-ttu-id="9d4b6-134">打开左上角的 "汉堡" 菜单，然后选择 "**设置**"。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-134">Open the hamburger menu on the top left, then select **Settings**.</span></span>
1. <span data-ttu-id="9d4b6-135">选择 "**关于**"。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-135">Select **About**.</span></span>
1. <span data-ttu-id="9d4b6-136">单击 "开发人员预览" 切换。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-136">Click the Developer preview toggle.</span></span>

## <a name="disable-developer-preview"></a><span data-ttu-id="9d4b6-137">禁用开发人员预览</span><span class="sxs-lookup"><span data-stu-id="9d4b6-137">Disable developer preview</span></span>

<span data-ttu-id="9d4b6-138">使用 "关于→开发人员预览" 下的相同菜单项，并单击它以将其关闭。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-138">Use the same menu item under About → Developer preview, and click on it to turn it off.</span></span>

## <a name="features-available-in-developer-preview"></a><span data-ttu-id="9d4b6-139">在开发人员预览版中可用的功能</span><span class="sxs-lookup"><span data-stu-id="9d4b6-139">Features available in developer preview</span></span>

<span data-ttu-id="9d4b6-140">有关当前在开发者预览版中启用的功能的完整列表，请参阅：[公共开发人员预览版中的功能](../../resources/dev-preview/developer-preview-features.md)。</span><span class="sxs-lookup"><span data-stu-id="9d4b6-140">For a full list of the features currently enabled in developer preview see: [Features in the public developer preview](../../resources/dev-preview/developer-preview-features.md).</span></span>
