---
title: 打包应用
description: 了解如何打包 Microsoft Teams 应用以进行测试、上传和应用商店发布。
localization_priority: Normal
ms.topic: conceptual
ms.openlocfilehash: c8341f3d83b5e6610e44276d6732affa1d1c1e91
ms.sourcegitcommit: 825abed2f8784d2bab7407ba7a4455ae17bbd28f
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/26/2021
ms.locfileid: "52020138"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="c56ae-103">为 Microsoft Teams 应用创建应用包</span><span class="sxs-lookup"><span data-stu-id="c56ae-103">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="c56ae-104">Teams 中的应用由应用清单 JSON 文件定义，并捆绑在带图标的应用包中。</span><span class="sxs-lookup"><span data-stu-id="c56ae-104">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="c56ae-105">你需要一个应用包，以在 Teams 中上传和安装应用，并发布到业务线应用目录或 AppSource。</span><span class="sxs-lookup"><span data-stu-id="c56ae-105">You'll need an app package to upload and install your app in Teams and publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="c56ae-106">Teams 应用包是包含以下内容的 .zip 文件：</span><span class="sxs-lookup"><span data-stu-id="c56ae-106">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="c56ae-107">一个名为 的清单文件，它指定应用的属性，并指向体验所需的资源，例如选项卡配置页的位置或其自动 `manifest.json` 程序 Microsoft 应用 ID 的位置。</span><span class="sxs-lookup"><span data-stu-id="c56ae-107">A manifest file named `manifest.json`, which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="c56ae-108">[应用的颜色和大纲图标](#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="c56ae-108">[Color and outline icons for your app](#app-icons).</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="c56ae-109">创建指令清单</span><span class="sxs-lookup"><span data-stu-id="c56ae-109">Creating a manifest</span></span>

<span data-ttu-id="c56ae-110">**Teams App Studio** 可帮助配置清单。</span><span class="sxs-lookup"><span data-stu-id="c56ae-110">**Teams App Studio** can help configure your manifest.</span></span> <span data-ttu-id="c56ae-111">它还包含 React 控件库和卡的可配置示例。</span><span class="sxs-lookup"><span data-stu-id="c56ae-111">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="c56ae-112">有关详细信息，请参阅 [App Studio 概述](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="c56ae-112">For more information, see [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="c56ae-113">清单文件必须命名为"manifest.js打开"，并且位于上传程序包的顶层。</span><span class="sxs-lookup"><span data-stu-id="c56ae-113">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="c56ae-114">请注意，之前构建的清单和包可能支持较旧版本的架构。</span><span class="sxs-lookup"><span data-stu-id="c56ae-114">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="c56ae-115">对于 Teams 应用，尤其是 AppSource (Office 应用商店) 提交，必须使用当前的 [清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="c56ae-115">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="c56ae-116">在清单的开头指定架构，以IntelliSense代码编辑器提供类似支持：</span><span class="sxs-lookup"><span data-stu-id="c56ae-116">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/en-us/json-schemas/teams/v1.9/MicrosoftTeams.schema.json",`
 
## <a name="app-icons"></a><span data-ttu-id="c56ae-117">应用图标</span><span class="sxs-lookup"><span data-stu-id="c56ae-117">App icons</span></span>

<span data-ttu-id="c56ae-118">应用包必须包含应用图标的两个 PNG 版本，即颜色图标和大纲图标。</span><span class="sxs-lookup"><span data-stu-id="c56ae-118">Your app package must include two PNG versions of your app icon—a color icon and an outline icon.</span></span> <span data-ttu-id="c56ae-119">若要使应用通过 AppSource 评价，这些图标必须满足以下大小要求。</span><span class="sxs-lookup"><span data-stu-id="c56ae-119">For your app to pass the AppSource review, these icons must meet the following size requirements.</span></span>

> [!Note]
> <span data-ttu-id="c56ae-120">如果你的应用具有自动程序或消息传递扩展，则你的图标也将包含在 Microsoft Azure 自动程序服务注册中。</span><span class="sxs-lookup"><span data-stu-id="c56ae-120">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

### <a name="color-icon"></a><span data-ttu-id="c56ae-121">颜色图标</span><span class="sxs-lookup"><span data-stu-id="c56ae-121">Color icon</span></span>

<span data-ttu-id="c56ae-122">图标的颜色版本在大多数 Teams 方案中显示，并且必须为 192x192 像素。</span><span class="sxs-lookup"><span data-stu-id="c56ae-122">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="c56ae-123">图标符号 (96x96 像素) 可以是任何颜色，但它必须位于纯色或完全透明的方形背景上。</span><span class="sxs-lookup"><span data-stu-id="c56ae-123">Your icon symbol (96x96 pixels) can be any color or colors, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="c56ae-124">Teams 自动将图标进行缩小，以在多个方案中显示圆角的正方形，以及自动程序方案中的六边形。</span><span class="sxs-lookup"><span data-stu-id="c56ae-124">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="c56ae-125">在符号周围包含 48 像素的填充，以便进行这些种种时不会丢失任何详细信息。</span><span class="sxs-lookup"><span data-stu-id="c56ae-125">Include 48 pixels of padding around your symbol so these crops can be made without losing any detail.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="Teams 颜色图标和设计指南。" border="false":::

### <a name="outline-icon"></a><span data-ttu-id="c56ae-127">大纲图标</span><span class="sxs-lookup"><span data-stu-id="c56ae-127">Outline icon</span></span>

<span data-ttu-id="c56ae-128">大纲图标在两种方案中显示：</span><span class="sxs-lookup"><span data-stu-id="c56ae-128">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="c56ae-129">当你的应用在使用中并且 Teams 左侧的应用栏上"已打开"时。</span><span class="sxs-lookup"><span data-stu-id="c56ae-129">When your app is in use and “hoisted” on the app bar on the left of Teams.</span></span>
* <span data-ttu-id="c56ae-130">当用户固定你的应用的消息扩展时。</span><span class="sxs-lookup"><span data-stu-id="c56ae-130">when a user pins your app's messaging extension.</span></span>

<span data-ttu-id="c56ae-131">图标必须为 32x32 像素。</span><span class="sxs-lookup"><span data-stu-id="c56ae-131">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="c56ae-132">它可以是白色且具有透明背景，或者使用白色背景 (不允许使用任何其他颜色) 。</span><span class="sxs-lookup"><span data-stu-id="c56ae-132">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="c56ae-133">大纲图标不应在符号周围有任何额外的填充。</span><span class="sxs-lookup"><span data-stu-id="c56ae-133">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="Teams 大纲图标设计指南。" border="false":::

### <a name="best-practices"></a><span data-ttu-id="c56ae-135">最佳做法</span><span class="sxs-lookup"><span data-stu-id="c56ae-135">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="显示如何设计应用图标的图示。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="c56ae-137">应做：遵循精确的大纲图标指南</span><span class="sxs-lookup"><span data-stu-id="c56ae-137">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="c56ae-138">图标中使用的白色 RGB 值必须为红色：255、绿色：255、蓝色：255。</span><span class="sxs-lookup"><span data-stu-id="c56ae-138">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="c56ae-139">大纲图标的所有其他部分必须完全透明，alpha 通道设置为 0。</span><span class="sxs-lookup"><span data-stu-id="c56ae-139">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="显示如何不设计应用图标的图示。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="c56ae-141">不：以圆形或圆角正方形形状裁剪</span><span class="sxs-lookup"><span data-stu-id="c56ae-141">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="c56ae-142">在应用包中提交的颜色图标必须为正方形。</span><span class="sxs-lookup"><span data-stu-id="c56ae-142">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="c56ae-143">不要四角舍入图标。</span><span class="sxs-lookup"><span data-stu-id="c56ae-143">Don’t round the corners of your icon.</span></span> <span data-ttu-id="c56ae-144">Teams 自动调整角半径。</span><span class="sxs-lookup"><span data-stu-id="c56ae-144">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

### <a name="examples"></a><span data-ttu-id="c56ae-145">示例</span><span class="sxs-lookup"><span data-stu-id="c56ae-145">Examples</span></span>

<span data-ttu-id="c56ae-146">下面将说明应用图标在不同的 Teams 功能和上下文中的显示方式。</span><span class="sxs-lookup"><span data-stu-id="c56ae-146">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="c56ae-147">个人应用</span><span class="sxs-lookup"><span data-stu-id="c56ae-147">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="显示应用图标在个人应用中的外观的示例。" border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="c56ae-149">自动 (频道) </span><span class="sxs-lookup"><span data-stu-id="c56ae-149">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="显示应用图标在频道内的自动程序上的外观的示例。" border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="c56ae-151">消息传递扩展</span><span class="sxs-lookup"><span data-stu-id="c56ae-151">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<替换文字>" border="false":::
