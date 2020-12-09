---
title: 打包应用程序
description: 了解如何打包 Microsoft 团队应用程序以进行测试、上载和存储发布。
ms.topic: conceptual
ms.openlocfilehash: 6929375c8d6a1602f01d83d15bfa0dab7f02a664
ms.sourcegitcommit: c102da958759c13aa9e0f81bde1cffb34a8bef34
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/09/2020
ms.locfileid: "49605265"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="a9929-103">为 Microsoft 团队应用程序创建应用程序包</span><span class="sxs-lookup"><span data-stu-id="a9929-103">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="a9929-104">团队中的应用程序由应用程序清单 JSON 文件定义，并捆绑到应用程序包及其图标中。</span><span class="sxs-lookup"><span data-stu-id="a9929-104">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="a9929-105">您需要一个应用程序包来上载和安装团队中的应用程序，并发布到您的业务线应用程序目录或 AppSource。</span><span class="sxs-lookup"><span data-stu-id="a9929-105">You'll need an app package to upload and install your app in Teams and publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="a9929-106">团队应用程序包是一个 .zip 文件，其中包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="a9929-106">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="a9929-107">一个名为的清单文件 `manifest.json` ，它指定应用程序的属性，并指向您的体验所需的资源，如其选项卡配置页或其机器人的 Microsoft 应用 ID 的位置。</span><span class="sxs-lookup"><span data-stu-id="a9929-107">A manifest file named `manifest.json`, which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="a9929-108">[您的应用程序的颜色和边框图标](#app-icons)。</span><span class="sxs-lookup"><span data-stu-id="a9929-108">[Color and outline icons for your app](#app-icons).</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="a9929-109">创建指令清单</span><span class="sxs-lookup"><span data-stu-id="a9929-109">Creating a manifest</span></span>

<span data-ttu-id="a9929-110">*团队应用程序 Studio* 可帮助配置你的清单。</span><span class="sxs-lookup"><span data-stu-id="a9929-110">*Teams App Studio* can help configure your manifest.</span></span> <span data-ttu-id="a9929-111">它还包含 React 控件库和卡的可配置示例。</span><span class="sxs-lookup"><span data-stu-id="a9929-111">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="a9929-112">请参阅 [App Studio 概述](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="a9929-112">See [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="a9929-113">您的清单文件必须命名为 "manifest.json"，并且必须是上载包的最高级别。</span><span class="sxs-lookup"><span data-stu-id="a9929-113">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="a9929-114">请注意，以前生成的清单和包可能支持较旧版本的架构。</span><span class="sxs-lookup"><span data-stu-id="a9929-114">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="a9929-115">对于团队应用程序，尤其是 AppSource (以前的 Office 应用商店) 提交，必须使用当前 [清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="a9929-115">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="a9929-116">指定清单开头的架构，以从代码编辑器中启用 IntelliSense 或类似支持：</span><span class="sxs-lookup"><span data-stu-id="a9929-116">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.8/MicrosoftTeams.schema.json",`

## <a name="app-icons"></a><span data-ttu-id="a9929-117">应用程序图标</span><span class="sxs-lookup"><span data-stu-id="a9929-117">App icons</span></span>

<span data-ttu-id="a9929-118">您的应用程序包必须包含应用程序图标的两个 PNG 版本（彩色图标和大纲图标）。</span><span class="sxs-lookup"><span data-stu-id="a9929-118">Your app package must include two PNG versions of your app icon—a color icon and an outline icon.</span></span> <span data-ttu-id="a9929-119">为了使您的应用程序通过 AppSource 审阅，这些图标必须满足以下大小要求。</span><span class="sxs-lookup"><span data-stu-id="a9929-119">For your app to pass the AppSource review, these icons must meet the following size requirements.</span></span>

> [!Note]
> <span data-ttu-id="a9929-120">如果你的应用程序具有机器人或邮件扩展，你的图标也将包含在 Microsoft Azure Bot 服务注册中。</span><span class="sxs-lookup"><span data-stu-id="a9929-120">If your app has a bot or messaging extension, your icons also will be included in your Microsoft Azure Bot Service registration.</span></span>

### <a name="color-icon"></a><span data-ttu-id="a9929-121">颜色图标</span><span class="sxs-lookup"><span data-stu-id="a9929-121">Color icon</span></span>

<span data-ttu-id="a9929-122">您的图标的颜色版本在大多数团队场景中显示，并且必须为192x192 像素。</span><span class="sxs-lookup"><span data-stu-id="a9929-122">The color version of your icon displays in most Teams scenarios and must be 192x192 pixels.</span></span> <span data-ttu-id="a9929-123">您的图标符号 (96x96 像素) 可以是任何颜色或颜色，但它必须位于一个纯或完全透明的方形背景上。</span><span class="sxs-lookup"><span data-stu-id="a9929-123">Your icon symbol (96x96 pixels) can be any color or colors, but it must sit on a solid or fully transparent square background.</span></span>

<span data-ttu-id="a9929-124">团队将自动裁剪图标，以在多个场景中显示带圆角的方形，在 bot 方案中显示一个六角形。</span><span class="sxs-lookup"><span data-stu-id="a9929-124">Teams automatically crops your icon to display a square with rounded corners in multiple scenarios and a hexagonal shape in bot scenarios.</span></span> <span data-ttu-id="a9929-125">在符号周围包含48像素的填充，以便可以进行这些裁剪，而不会丢失任何细节。</span><span class="sxs-lookup"><span data-stu-id="a9929-125">Include 48 pixels of padding around your symbol so these crops can be made without losing any detail.</span></span>

:::image type="content" source="../../assets/images/icons/design-color-icon.png" alt-text="团队颜色图标设计指南。" border="false":::

### <a name="outline-icon"></a><span data-ttu-id="a9929-127">大纲图标</span><span class="sxs-lookup"><span data-stu-id="a9929-127">Outline icon</span></span>

<span data-ttu-id="a9929-128">在以下两种情况下，大纲图标将显示：</span><span class="sxs-lookup"><span data-stu-id="a9929-128">An outline icon displays in two scenarios:</span></span>

* <span data-ttu-id="a9929-129">当您的应用程序在团队左侧的应用程序栏上使用并 "已提升"。</span><span class="sxs-lookup"><span data-stu-id="a9929-129">When your app is in use and “hoisted” on the app bar on the left of Teams.</span></span>
* <span data-ttu-id="a9929-130">当用户锁定您的应用程序的邮件扩展时。</span><span class="sxs-lookup"><span data-stu-id="a9929-130">when a user pins your app's messaging extension.</span></span>

<span data-ttu-id="a9929-131">图标必须是32x32 像素。</span><span class="sxs-lookup"><span data-stu-id="a9929-131">The icon must be 32x32 pixels.</span></span> <span data-ttu-id="a9929-132">它可以是白色的透明背景，也可以是透明的白色背景 (不允许任何其他颜色) 。</span><span class="sxs-lookup"><span data-stu-id="a9929-132">It can be white with a transparent background or transparent with a white background (no other colors are permitted).</span></span> <span data-ttu-id="a9929-133">大纲图标周围的符号不应包含任何额外的填充。</span><span class="sxs-lookup"><span data-stu-id="a9929-133">The outline icon should not have any extra padding around the symbol.</span></span>

:::image type="content" source="../../assets/images/icons/design-outline-icon.png" alt-text="团队颜色图标设计指南。" border="false":::

### <a name="best-practices"></a><span data-ttu-id="a9929-135">最佳做法</span><span class="sxs-lookup"><span data-stu-id="a9929-135">Best practices</span></span>

:::row:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-do.png" alt-text="演示如何设计应用图标。" border="false":::

#### <a name="do-follow-the-precise-outline-icon-guidelines"></a><span data-ttu-id="a9929-137">操作：遵循精确的大纲图标准则</span><span class="sxs-lookup"><span data-stu-id="a9929-137">Do: Follow the precise outline icon guidelines</span></span>

<span data-ttu-id="a9929-138">您的图标中使用的白色的 RGB 值必须为红色：255、绿色：255、蓝色：255。</span><span class="sxs-lookup"><span data-stu-id="a9929-138">The RGB values of white used in your icon must be Red: 255, Green: 255, Blue: 255.</span></span> <span data-ttu-id="a9929-139">大纲图标的所有其他部分必须完全透明，alpha 通道设置为0。</span><span class="sxs-lookup"><span data-stu-id="a9929-139">All other parts of the outline icon must be fully transparent, with the alpha channel set to 0.</span></span>

   :::column-end:::
   :::column span="":::
:::image type="content" source="../../assets/images/icons/design-icon-dont.png" alt-text="演示如何不设计应用图标。" border="false":::

#### <a name="dont-crop-in-a-circular-or-rounded-square-shape"></a><span data-ttu-id="a9929-141">不：在圆形或圆角方形形状中裁剪</span><span class="sxs-lookup"><span data-stu-id="a9929-141">Don't: Crop in a circular or rounded square shape</span></span>

<span data-ttu-id="a9929-142">您的应用程序包中提交的颜色图标必须是方形。</span><span class="sxs-lookup"><span data-stu-id="a9929-142">The color icon submitted in your app package must be square.</span></span> <span data-ttu-id="a9929-143">不四舍五入图标的角。</span><span class="sxs-lookup"><span data-stu-id="a9929-143">Don’t round the corners of your icon.</span></span> <span data-ttu-id="a9929-144">团队自动调整拐角的半径。</span><span class="sxs-lookup"><span data-stu-id="a9929-144">Teams automatically adjusts the corner radius.</span></span>

   :::column-end:::
:::row-end:::

### <a name="examples"></a><span data-ttu-id="a9929-145">示例</span><span class="sxs-lookup"><span data-stu-id="a9929-145">Examples</span></span>

<span data-ttu-id="a9929-146">下面介绍了应用程序图标在不同的团队功能和上下文中的显示方式。</span><span class="sxs-lookup"><span data-stu-id="a9929-146">Here's how app icons appear in different Teams capabilities and contexts.</span></span>

#### <a name="personal-app"></a><span data-ttu-id="a9929-147">个人应用程序</span><span class="sxs-lookup"><span data-stu-id="a9929-147">Personal app</span></span>

:::image type="content" source="../../assets/images/icons/personal-app-icon-example.png" alt-text="示例：显示应用程序图标在个人应用程序中的外观。" border="false":::

#### <a name="bot-channel"></a><span data-ttu-id="a9929-149">Bot (频道) </span><span class="sxs-lookup"><span data-stu-id="a9929-149">Bot (channel)</span></span>

:::image type="content" source="../../assets/images/icons/bot-icon-example.png" alt-text="示例：显示应用程序图标在频道内的机器人的外观。" border="false":::

#### <a name="messaging-extension"></a><span data-ttu-id="a9929-151">消息扩展</span><span class="sxs-lookup"><span data-stu-id="a9929-151">Messaging extension</span></span>

:::image type="content" source="../../assets/images/icons/messaging-extension-icon-example.png" alt-text="<alt 文本>" border="false":::
