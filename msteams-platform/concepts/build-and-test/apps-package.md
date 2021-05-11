---
title: 打包应用
description: 了解如何打包应用Microsoft Teams测试、上传和应用商店发布。
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: e477539a9b8eaa0c869a2070fcd20b74aecfe490
ms.sourcegitcommit: 25c9ad27f99682caaa7347840578b118c63b8f69
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/30/2021
ms.locfileid: "52101700"
---
# <a name="create-a-microsoft-teams-app-package"></a><span data-ttu-id="dd255-103">创建Microsoft Teams应用包</span><span class="sxs-lookup"><span data-stu-id="dd255-103">Create a Microsoft Teams app package</span></span>

<span data-ttu-id="dd255-104">你需要应用包，但计划分配你的Microsoft Teams包。</span><span class="sxs-lookup"><span data-stu-id="dd255-104">You need an app package however you plan to distribute your Microsoft Teams app.</span></span> <span data-ttu-id="dd255-105">有效包是包含以下内容的 ZIP 文件：</span><span class="sxs-lookup"><span data-stu-id="dd255-105">A valid package is a ZIP file that contains the following:</span></span>

* <span data-ttu-id="dd255-106">**应用** 清单 ：描述如何配置应用，包括应用的功能、必需资源以及其他重要属性。</span><span class="sxs-lookup"><span data-stu-id="dd255-106">**App manifest**: Describes how your app is configured, including its capabilities, required resources, and other important attributes.</span></span>
* <span data-ttu-id="dd255-107">**应用图标**：每个程序包都需要应用的颜色和轮廓图标。</span><span class="sxs-lookup"><span data-stu-id="dd255-107">**App icons**: Each package requires a color and outline icon for your app.</span></span>

## <a name="app-manifest"></a><span data-ttu-id="dd255-108">应用部件清单</span><span class="sxs-lookup"><span data-stu-id="dd255-108">App manifest</span></span>

<span data-ttu-id="dd255-109">应用清单文件必须位于包的顶级，名称为 `manifest.json` 。</span><span class="sxs-lookup"><span data-stu-id="dd255-109">Your app manifest file must be at the top level of the package with the name `manifest.json`.</span></span> 

<span data-ttu-id="dd255-110">发布到应用商店Teams，请确保清单引用最新的[架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="dd255-110">When publishing to the Teams store, make sure your manifest references the latest [schema](~/resources/schema/manifest-schema.md).</span></span>

## <a name="app-icons"></a><span data-ttu-id="dd255-111">应用图标</span><span class="sxs-lookup"><span data-stu-id="dd255-111">App icons</span></span>

<span data-ttu-id="dd255-112">应用包必须包含应用图标的两个 PNG 版本：颜色和大纲版本。</span><span class="sxs-lookup"><span data-stu-id="dd255-112">Your app package must include two PNG versions of your app icon: A color and outline version.</span></span>

> [!Note]
> <span data-ttu-id="dd255-113">如果你的应用具有自动程序或消息传递扩展，你的图标也将包含在你的自动Microsoft Azure注册中。</span><span class="sxs-lookup"><span data-stu-id="dd255-113">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

<span data-ttu-id="dd255-114">若要使应用通过Teams评价，这些图标必须满足以下大小要求。</span><span class="sxs-lookup"><span data-stu-id="dd255-114">For your app to pass Teams store review, these icons must meet the following size requirements.</span></span>

### <a name="color-icon"></a><span data-ttu-id="dd255-115">颜色图标</span><span class="sxs-lookup"><span data-stu-id="dd255-115">Color icon</span></span>

<span data-ttu-id="dd255-116">图标的颜色版本在大多数应用场景中Teams必须为 192x192 像素。</span><span class="sxs-lookup"><span data-stu-id="dd255-116">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="dd255-117">图标符号 (96x96 像素) 可以是任何颜色，但它必须位于纯色或完全透明的方形背景上。</span><span class="sxs-lookup"><span data-stu-id="dd255-117">Your icon symbol (96x96 pixels) can be any color, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="dd255-118">Teams自动种图标，以在多个方案中显示圆角的正方形，在机器人方案中显示六边形形状。</span><span class="sxs-lookup"><span data-stu-id="dd255-118">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="dd255-119">若要裁剪符号而不丢失任何细节，请在你的符号周围包含 48 像素的填充。</span><span class="sxs-lookup"><span data-stu-id="dd255-119">To crop the symbol without losing any detail, include 48 pixels of padding around your symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams颜色图标和设计指南。" border="false":::

### <a name="outline-icon"></a><span data-ttu-id="dd255-121">大纲图标</span><span class="sxs-lookup"><span data-stu-id="dd255-121">Outline icon</span></span>

<span data-ttu-id="dd255-122">大纲图标在两种方案中显示：</span><span class="sxs-lookup"><span data-stu-id="dd255-122">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="dd255-123">当你的应用在使用中时，在应用栏的左侧应用栏上Teams。</span><span class="sxs-lookup"><span data-stu-id="dd255-123">When your app is in use and “hoisted” on the app bar on the left side of Teams.</span></span>
* <span data-ttu-id="dd255-124">当用户固定你的应用的消息扩展时。</span><span class="sxs-lookup"><span data-stu-id="dd255-124">When a user pins your app's messaging extension.</span></span>

<span data-ttu-id="dd255-125">图标必须为 32x32 像素。</span><span class="sxs-lookup"><span data-stu-id="dd255-125">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="dd255-126">它可以是白色且具有透明背景，或者使用白色背景 (不允许使用任何其他颜色) 。</span><span class="sxs-lookup"><span data-stu-id="dd255-126">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="dd255-127">大纲图标不应在符号周围有任何额外的填充。</span><span class="sxs-lookup"><span data-stu-id="dd255-127">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams大纲图标设计指南。" border="false":::

### <a name="best-practices"></a><span data-ttu-id="dd255-129">最佳做法</span><span class="sxs-lookup"><span data-stu-id="dd255-129">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="显示如何设计应用图标的图示。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="dd255-131">应做：遵循精确的大纲图标指南</span><span class="sxs-lookup"><span data-stu-id="dd255-131">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="dd255-132">图标中使用的白色 RGB 值必须为红色：255、绿色：255、蓝色：255。</span><span class="sxs-lookup"><span data-stu-id="dd255-132">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="dd255-133">大纲图标的所有其他部分必须完全透明，alpha 通道设置为 0。</span><span class="sxs-lookup"><span data-stu-id="dd255-133">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="显示如何不设计应用图标的图示。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="dd255-135">不：以圆形或圆角正方形形状裁剪</span><span class="sxs-lookup"><span data-stu-id="dd255-135">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="dd255-136">在应用包中提交的颜色图标必须为正方形。</span><span class="sxs-lookup"><span data-stu-id="dd255-136">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="dd255-137">不要四角舍入图标。</span><span class="sxs-lookup"><span data-stu-id="dd255-137">Don’t round the corners of your icon.</span></span> <span data-ttu-id="dd255-138">Teams自动调整角半径。</span><span class="sxs-lookup"><span data-stu-id="dd255-138">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

#### <a name="dont-copy-other-brands"></a><span data-ttu-id="dd255-139">不要：复制其他品牌</span><span class="sxs-lookup"><span data-stu-id="dd255-139">Don't: Copy other brands</span></span>

<span data-ttu-id="dd255-140">图标不得模仿你未拥有的任何受版权保护 (例如，类似于 Microsoft 产品或品牌) 。</span><span class="sxs-lookup"><span data-stu-id="dd255-140">Your icons must not mimic any copyrighted products that you don't own (for example, a design similar to a Microsoft product or brand).</span></span>

### <a name="examples"></a><span data-ttu-id="dd255-141">示例</span><span class="sxs-lookup"><span data-stu-id="dd255-141">Examples</span></span>

<span data-ttu-id="dd255-142">下面是应用图标在不同功能和上下文中Teams的方式。</span><span class="sxs-lookup"><span data-stu-id="dd255-142">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="dd255-143">个人应用</span><span class="sxs-lookup"><span data-stu-id="dd255-143">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="显示应用图标在个人应用中的外观的示例。" border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="dd255-145">自动 (频道) </span><span class="sxs-lookup"><span data-stu-id="dd255-145">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="显示应用图标在频道内的自动程序上的外观的示例。" border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="dd255-147">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="dd255-147">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<替换文字>" border="false":::

## <a name="next-step"></a><span data-ttu-id="dd255-149">后续步骤</span><span class="sxs-lookup"><span data-stu-id="dd255-149">Next step</span></span>

<span data-ttu-id="dd255-150">选择计划如何分配应用：</span><span class="sxs-lookup"><span data-stu-id="dd255-150">Choose how you plan to distribute your app:</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="dd255-151">在应用程序中旁加载Teams</span><span class="sxs-lookup"><span data-stu-id="dd255-151">Sideload your app in Teams</span></span>](~/concepts/deploy-and-publish/apps-upload.md)
> [!div class="nextstepaction"]
> [<span data-ttu-id="dd255-152">将应用发布到组织</span><span class="sxs-lookup"><span data-stu-id="dd255-152">Publish your app to your org</span></span>](/MicrosoftTeams/tenant-apps-catalog-teams?toc=/microsoftteams/platform/toc.json&bc=/MicrosoftTeams/breadcrumb/toc.json)
> [!div class="nextstepaction"]
> [<span data-ttu-id="dd255-153">将应用发布到应用商店</span><span class="sxs-lookup"><span data-stu-id="dd255-153">Publish your app to the store</span></span>](~/concepts/deploy-and-publish/appsource/publish.md)
