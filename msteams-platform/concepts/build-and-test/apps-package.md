---
title: 打包应用程序
description: 了解如何打包应用程序以在 Microsoft 团队中进行测试、上载和发布
keywords: 团队应用程序打包
ms.topic: conceptual
ms.openlocfilehash: 66131f37f9f68c8fd54412d41068f6124da94453
ms.sourcegitcommit: 6c786434b56cc8c2765a14aa1f6149870245f309
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 06/06/2020
ms.locfileid: "44801165"
---
# <a name="create-an-app-package-for-your-microsoft-teams-app"></a><span data-ttu-id="169c0-104">为 Microsoft 团队应用程序创建应用程序包</span><span class="sxs-lookup"><span data-stu-id="169c0-104">Create an app package for your Microsoft Teams app</span></span>

<span data-ttu-id="169c0-105">团队中的应用程序由应用程序清单 JSON 文件定义，并捆绑到应用程序包及其图标中。</span><span class="sxs-lookup"><span data-stu-id="169c0-105">Apps in Teams are defined by an app manifest JSON file, and bundled in an app package with their icons.</span></span> <span data-ttu-id="169c0-106">您需要一个应用程序包来上载和安装团队中的应用程序，并发布到您的业务线应用程序目录或 AppSource。</span><span class="sxs-lookup"><span data-stu-id="169c0-106">You'll need an app package to upload and install your app in Teams, and to publish to either your Line of Business app catalog or to AppSource.</span></span>

<span data-ttu-id="169c0-107">团队应用程序包是一个 .zip 文件，其中包含以下内容：</span><span class="sxs-lookup"><span data-stu-id="169c0-107">A Teams app package is a .zip file containing the following:</span></span>

* <span data-ttu-id="169c0-108">一个名为 "manifest.json" 的清单文件，它指定您的应用程序的属性，并指向您的体验所需的资源，如其选项卡配置页或其机器人的 Microsoft 应用 ID 的位置。</span><span class="sxs-lookup"><span data-stu-id="169c0-108">A manifest file named "manifest.json", which specifies attributes of your app and points to required resources for your experience, such the location of its tab configuration page or the Microsoft app ID for its bot.</span></span>
* <span data-ttu-id="169c0-109">透明的 "大纲" 图标和完整的 "颜色" 图标。</span><span class="sxs-lookup"><span data-stu-id="169c0-109">A transparent "outline" icon and a full "color" icon.</span></span> <span data-ttu-id="169c0-110">有关详细信息，请参阅本主题后面的[图标](#icons)。</span><span class="sxs-lookup"><span data-stu-id="169c0-110">See [Icons](#icons) later in this topic for more information.</span></span>

## <a name="creating-a-manifest"></a><span data-ttu-id="169c0-111">创建指令清单</span><span class="sxs-lookup"><span data-stu-id="169c0-111">Creating a manifest</span></span>

<span data-ttu-id="169c0-112">*团队应用程序 Studio*可帮助配置你的清单。</span><span class="sxs-lookup"><span data-stu-id="169c0-112">*Teams App Studio* can help configure your manifest.</span></span> <span data-ttu-id="169c0-113">它还包含 React 控件库和卡的可配置示例。</span><span class="sxs-lookup"><span data-stu-id="169c0-113">It also contains a React control library and configurable samples for cards.</span></span> <span data-ttu-id="169c0-114">请参阅[App Studio 概述](~/concepts/build-and-test/app-studio-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="169c0-114">See [App Studio Overview](~/concepts/build-and-test/app-studio-overview.md).</span></span>

<span data-ttu-id="169c0-115">您的清单文件必须命名为 "manifest.json"，并且必须是上载包的最高级别。</span><span class="sxs-lookup"><span data-stu-id="169c0-115">Your manifest file must be named "manifest.json" and be at the top level of the upload package.</span></span> <span data-ttu-id="169c0-116">请注意，以前生成的清单和包可能支持较旧版本的架构。</span><span class="sxs-lookup"><span data-stu-id="169c0-116">Note that manifests and packages built previously might support an older version of the schema.</span></span> <span data-ttu-id="169c0-117">对于团队应用程序，尤其是 AppSource （以前称为 Office 应用商店）提交，必须使用当前[清单架构](~/resources/schema/manifest-schema.md)。</span><span class="sxs-lookup"><span data-stu-id="169c0-117">For Teams apps and especially AppSource (formerly Office Store) submission, you must use the current [manifest schema](~/resources/schema/manifest-schema.md).</span></span>

> [!TIP]
> <span data-ttu-id="169c0-118">指定清单开头的架构，以从代码编辑器中启用 IntelliSense 或类似支持：</span><span class="sxs-lookup"><span data-stu-id="169c0-118">Specify the schema at the beginning of your manifest to enable IntelliSense or similar support from your code editor:</span></span>
>
> `"$schema": "https://developer.microsoft.com/json-schemas/teams/v1.7/MicrosoftTeams.schema.json",`

## <a name="icons"></a><span data-ttu-id="169c0-119">图标</span><span class="sxs-lookup"><span data-stu-id="169c0-119">Icons</span></span>

> [!Note]
> <span data-ttu-id="169c0-120">如果您的应用程序包含机器人或邮件扩展，则使用的图标将是上载到 bot 框架中的 bot 注册的图标。</span><span class="sxs-lookup"><span data-stu-id="169c0-120">If your app contains a bot or messaging extension, the icons used will be the icons uploaded to your bot registration in the Bot Framework.</span></span>

<span data-ttu-id="169c0-121">Microsoft 团队需要两个图标来满足你的应用程序体验，才能在产品中使用。</span><span class="sxs-lookup"><span data-stu-id="169c0-121">Microsoft Teams requires two icons for your app experience, to be used within the product.</span></span> <span data-ttu-id="169c0-122">图标必须包含在包中，并通过清单中的相对路径引用。</span><span class="sxs-lookup"><span data-stu-id="169c0-122">Icons must be included in the package and referenced via relative paths in the manifest.</span></span> <span data-ttu-id="169c0-123">每个路径的最大长度为2048个字节，图标的格式为 .png。</span><span class="sxs-lookup"><span data-stu-id="169c0-123">The maximum length of each path is 2048 bytes, and the format of the icon is .png.</span></span>

### <a name="color"></a><span data-ttu-id="169c0-124">颜色</span><span class="sxs-lookup"><span data-stu-id="169c0-124">color</span></span>

<span data-ttu-id="169c0-125">该 `color` 图标在 Microsoft 团队（在应用程序和选项卡库、bot、flyouts 等）中使用。</span><span class="sxs-lookup"><span data-stu-id="169c0-125">The `color` icon is used throughout Microsoft Teams (in app and tab galleries, bots, flyouts, and so on).</span></span> <span data-ttu-id="169c0-126">此图标应为192x192 像素。</span><span class="sxs-lookup"><span data-stu-id="169c0-126">This icon should be 192x192 pixels.</span></span> <span data-ttu-id="169c0-127">您的图标可以是任何颜色（或颜色），但背景应为您的品牌化强调文字颜色。</span><span class="sxs-lookup"><span data-stu-id="169c0-127">Your icon can be any color (or colors), but the background should be your branded accent color.</span></span> <span data-ttu-id="169c0-128">它还应在图标周围具有少量的填充，以适应图标的 bot 版本的六角裁剪。</span><span class="sxs-lookup"><span data-stu-id="169c0-128">It should also have a small amount of padding surrounding the icon to accommodate the hexagonal cropping for the bot version of the icon.</span></span>

### <a name="outline"></a><span data-ttu-id="169c0-129">outline</span><span class="sxs-lookup"><span data-stu-id="169c0-129">outline</span></span>

<span data-ttu-id="169c0-130">`outline`在以下位置使用图标：用户已将其标记为 "收藏夹" 的应用栏和邮件扩展。</span><span class="sxs-lookup"><span data-stu-id="169c0-130">The `outline` icon is used in these places: the app bar and messaging extensions the user has marked as a "favorite."</span></span> <span data-ttu-id="169c0-131">此图标必须为32x32 像素。</span><span class="sxs-lookup"><span data-stu-id="169c0-131">This icon must be 32x32 pixels.</span></span> <span data-ttu-id="169c0-132">大纲图标必须仅包含白色和透明度（无其他颜色）。</span><span class="sxs-lookup"><span data-stu-id="169c0-132">Your outline icon must contain only white and transparency (no other colors).</span></span> <span data-ttu-id="169c0-133">图标可以是白色背景，也可以是透明背景。</span><span class="sxs-lookup"><span data-stu-id="169c0-133">The icon can be white with transparent background or transparent with a white background.</span></span> <span data-ttu-id="169c0-134">大纲图标周围的图标周围不应有额外的填充，应尽可能紧密地裁剪，同时仍保持32x32 尺寸。</span><span class="sxs-lookup"><span data-stu-id="169c0-134">The outline icon should not have extra padding surrounding the icon and should be as tightly cropped as possible while still maintaining the 32x32 dimensions.</span></span> <span data-ttu-id="169c0-135">以下是几个很棒的示例：</span><span class="sxs-lookup"><span data-stu-id="169c0-135">Here are a few good examples:</span></span>

![示例大纲图标](~/assets/images/icons/sample20x20s.png)

<span data-ttu-id="169c0-137">例如，假设您的公司是 Contoso。</span><span class="sxs-lookup"><span data-stu-id="169c0-137">For example, say your company is Contoso.</span></span> <span data-ttu-id="169c0-138">您可以提交两个图标：</span><span class="sxs-lookup"><span data-stu-id="169c0-138">You'd submit two icons:</span></span>

![图标展示](~/assets/images/framework/framework_submit_icon.png)

<span data-ttu-id="169c0-140">以下是图标在 UI 中的显示方式：</span><span class="sxs-lookup"><span data-stu-id="169c0-140">Here's how the icons would appear in the UI:</span></span>

#### <a name="bot-and-chiclet-in-channel-view"></a><span data-ttu-id="169c0-141">通道视图中的 Bot 和 chiclet</span><span class="sxs-lookup"><span data-stu-id="169c0-141">Bot and chiclet in Channel view</span></span>

![Bot 和 chiclet UX](~/assets/images/icons/botandchiclet.png)

#### <a name="flyout"></a><span data-ttu-id="169c0-143">弹出</span><span class="sxs-lookup"><span data-stu-id="169c0-143">Flyout</span></span>

![示例 Contoso 图标](~/assets/images/icons/flyout.png)

#### <a name="app-bar-and-home-screen"></a><span data-ttu-id="169c0-145">应用栏和主屏幕</span><span class="sxs-lookup"><span data-stu-id="169c0-145">App bar and home screen</span></span>

![示例 Contoso 图标](~/assets/images/icons/appbarhomescreen.png)
