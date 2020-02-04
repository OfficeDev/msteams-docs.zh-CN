---
title: 选项卡的设计准则
description: 介绍为内容和协作创建选项卡的准则
keywords: 团队设计指南参考框架选项卡配置
ms.openlocfilehash: adf86678a42e2267af00734e1ef85efced882488
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41672974"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="2b54c-104">内容和对话，所有使用选项卡一次</span><span class="sxs-lookup"><span data-stu-id="2b54c-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="2b54c-105">**移动客户端上的选项卡**</span><span class="sxs-lookup"><span data-stu-id="2b54c-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="2b54c-106">创建选项卡时，请遵循[移动电话上的选项卡指南](~/tabs/design/tabs-mobile.md)。</span><span class="sxs-lookup"><span data-stu-id="2b54c-106">Follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="2b54c-107">如果您的选项卡使用身份验证，则必须将团队 JavaScript SDK 升级到版本1.4.1 或更高版本，否则身份验证将失败。</span><span class="sxs-lookup"><span data-stu-id="2b54c-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="2b54c-108">**移动设备上的个人（静态）选项卡：**</span><span class="sxs-lookup"><span data-stu-id="2b54c-108">**Personal (static) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="2b54c-109">在[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中，可以使用静态选项卡（个人应用）。</span><span class="sxs-lookup"><span data-stu-id="2b54c-109">Static tabs (personal app) are available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
> * <span data-ttu-id="2b54c-110">在构建静态选项卡时，请确保遵循[移动电话上的选项卡指南](~/tabs/design/tabs-mobile.md)</span><span class="sxs-lookup"><span data-stu-id="2b54c-110">While building your static tabs, ensure to follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md)</span></span>
>
> <span data-ttu-id="2b54c-111">**移动设备上的频道/组（可配置）选项卡：**</span><span class="sxs-lookup"><span data-stu-id="2b54c-111">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="2b54c-112">移动客户端仅显示具有值的`websiteUrl`选项卡。</span><span class="sxs-lookup"><span data-stu-id="2b54c-112">Mobile clients only show tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="2b54c-113">如果希望您的选项卡显示在团队移动客户端上，则必须设置的`websiteUrl`值。</span><span class="sxs-lookup"><span data-stu-id="2b54c-113">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="2b54c-114">移动上的默认打开行为是使用在浏览器中的`websiteUrl`外部打开。</span><span class="sxs-lookup"><span data-stu-id="2b54c-114">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="2b54c-115">对于发布到公用应用商店的应用程序，如果您希望频道选项卡在默认情况下在团队内打开，请遵循[移动电话上的选项卡指南](~/tabs/design/tabs-mobile.md)，并转到您的支持代表以请求列入白名单。</span><span class="sxs-lookup"><span data-stu-id="2b54c-115">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="2b54c-116">选项卡是可用于在团队的随机工作流中共享内容、举行对话和托管第三方服务的画布。</span><span class="sxs-lookup"><span data-stu-id="2b54c-116">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="2b54c-117">当您在 Microsoft 团队中构建一个选项卡时，它会将 web 应用程序的前端和中心放置在易于从关键对话中访问的位置。</span><span class="sxs-lookup"><span data-stu-id="2b54c-117">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="2b54c-118">准则</span><span class="sxs-lookup"><span data-stu-id="2b54c-118">Guidelines</span></span>

<span data-ttu-id="2b54c-119">一个合适的选项卡应显示以下特征：</span><span class="sxs-lookup"><span data-stu-id="2b54c-119">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="2b54c-120">重点功能</span><span class="sxs-lookup"><span data-stu-id="2b54c-120">Focused functionality</span></span>

<span data-ttu-id="2b54c-121">当为满足特定需求而构建时，选项卡的工作效果最佳。</span><span class="sxs-lookup"><span data-stu-id="2b54c-121">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="2b54c-122">将重点放在一小部分任务或与选项卡所在通道相关的一组数据。</span><span class="sxs-lookup"><span data-stu-id="2b54c-122">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="2b54c-123">简化 chrome</span><span class="sxs-lookup"><span data-stu-id="2b54c-123">Reduced chrome</span></span>

<span data-ttu-id="2b54c-124">避免在选项卡中创建多个面板、添加导航层或要求用户在一个选项卡中垂直和水平滚动。换言之，请不要在选项卡中包含选项卡。</span><span class="sxs-lookup"><span data-stu-id="2b54c-124">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

> [!TIP]
> <span data-ttu-id="2b54c-125">避免在选项卡中创建多个面板、添加导航层或要求用户在一个选项卡中垂直和水平滚动。</span><span class="sxs-lookup"><span data-stu-id="2b54c-125">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab.</span></span>

### <a name="integration"></a><span data-ttu-id="2b54c-126">集中</span><span class="sxs-lookup"><span data-stu-id="2b54c-126">Integration</span></span>

<span data-ttu-id="2b54c-127">查找通过将卡发布到对话来通知用户选项卡活动的方法。</span><span class="sxs-lookup"><span data-stu-id="2b54c-127">Find ways to notify users about tab activity by posting cards to a conversation, for example.</span></span>

### <a name="conversational"></a><span data-ttu-id="2b54c-128">对话</span><span class="sxs-lookup"><span data-stu-id="2b54c-128">Conversational</span></span>

<span data-ttu-id="2b54c-129">寻找一种有助于围绕选项卡进行对话的方法。这样可确保在现有内容、数据或流程上进行对话中心。</span><span class="sxs-lookup"><span data-stu-id="2b54c-129">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="2b54c-130">精简访问</span><span class="sxs-lookup"><span data-stu-id="2b54c-130">Streamlined access</span></span>

<span data-ttu-id="2b54c-131">请确保在适当的时间授予对正确人员的访问权限。</span><span class="sxs-lookup"><span data-stu-id="2b54c-131">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="2b54c-132">保持您的登录过程很简单将避免为发布和协作创建障碍。</span><span class="sxs-lookup"><span data-stu-id="2b54c-132">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="personality"></a><span data-ttu-id="2b54c-133">特征</span><span class="sxs-lookup"><span data-stu-id="2b54c-133">Personality</span></span>

<span data-ttu-id="2b54c-134">您的选项卡画布为你的体验提供出色的品牌打造机会。</span><span class="sxs-lookup"><span data-stu-id="2b54c-134">Your tab canvas presents a good opportunity to brand your experience.</span></span> <span data-ttu-id="2b54c-135">合并自己的徽标、颜色和布局以传达个性。</span><span class="sxs-lookup"><span data-stu-id="2b54c-135">Incorporate your own logos, colors, and layouts to communicate personality.</span></span>

<span data-ttu-id="2b54c-136">你的徽标是你的身份以及与你的用户的连接的重要部分。</span><span class="sxs-lookup"><span data-stu-id="2b54c-136">Your logo is an important part of your identity and a connection with your users.</span></span> <span data-ttu-id="2b54c-137">因此，请务必将其包括在内。</span><span class="sxs-lookup"><span data-stu-id="2b54c-137">So be sure to include it.</span></span>

* <span data-ttu-id="2b54c-138">将徽标放置在左右角或沿下边缘</span><span class="sxs-lookup"><span data-stu-id="2b54c-138">Place your logo in the left or right corner or along the bottom edge</span></span>
* <span data-ttu-id="2b54c-139">保持您的徽标较小且不引人注目</span><span class="sxs-lookup"><span data-stu-id="2b54c-139">Keep your logo small and unobtrusive</span></span>

> [!TIP]
> <span data-ttu-id="2b54c-140">请使用我们的视觉样式，让你的服务感觉像团队的一部分。</span><span class="sxs-lookup"><span data-stu-id="2b54c-140">Please work with our visual style so your service feels like a part of Teams.</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="2b54c-141">选项卡布局</span><span class="sxs-lookup"><span data-stu-id="2b54c-141">Tab layouts</span></span>

[!include[Tab layouts](~/includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="2b54c-142">选项卡的类型</span><span class="sxs-lookup"><span data-stu-id="2b54c-142">Types of tabs</span></span>

[!include[Tab types](~/includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="2b54c-143">配置页高度</span><span class="sxs-lookup"><span data-stu-id="2b54c-143">Configuration page height</span></span>

>[!NOTE]
><span data-ttu-id="2b54c-144">在9月2018中，选项卡[配置页面](~/tabs/how-to/create-tab-pages/configuration-page.md)的高度增加，而宽度保持不变。</span><span class="sxs-lookup"><span data-stu-id="2b54c-144">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="2b54c-145">如果您的应用程序是为较旧的大小设计的，则选项卡配置页将具有大量的垂直空白。</span><span class="sxs-lookup"><span data-stu-id="2b54c-145">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="2b54c-146">从此更改中免除的旧版应用程序将需要在更新后与 Microsoft 联系，以适应新的维度。</span><span class="sxs-lookup"><span data-stu-id="2b54c-146">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="2b54c-147">选项卡配置页的尺寸：</span><span class="sxs-lookup"><span data-stu-id="2b54c-147">The dimensions of the tab configuration page:</span></span>

<img width="450px" title="配置选项卡的大小" src="~/assets/images/tabs/config-dialog-Contoso2.png" />

### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="2b54c-149">选项卡配置页面格式的准则</span><span class="sxs-lookup"><span data-stu-id="2b54c-149">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="2b54c-150">使固定高度图形元素上的选项卡配置页的内容区域的最小高度为基准。</span><span class="sxs-lookup"><span data-stu-id="2b54c-150">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="2b54c-151">使用`window.innerHeight`计算可用的垂直间距（配置页中的内容区域的高度）。</span><span class="sxs-lookup"><span data-stu-id="2b54c-151">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="2b54c-152">这将返回配置页面所`<iframe>`驻留的大小，在将来的版本中可能会发生更改。</span><span class="sxs-lookup"><span data-stu-id="2b54c-152">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="2b54c-153">通过使用此值，你的内容将自动调整为将来的更改。</span><span class="sxs-lookup"><span data-stu-id="2b54c-153">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="2b54c-154">将垂直空间分配给可变高度元素减去固定高度元素所需的值。</span><span class="sxs-lookup"><span data-stu-id="2b54c-154">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="2b54c-155">对于 "*登录*状态"，将内容垂直和水平居中。</span><span class="sxs-lookup"><span data-stu-id="2b54c-155">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="2b54c-156">如果需要背景图像，您需要一个新图像，调整大小以适合该区域（首选），或者您可以保留相同的图像并在其中进行选择：</span><span class="sxs-lookup"><span data-stu-id="2b54c-156">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="2b54c-157">与左上角对齐。</span><span class="sxs-lookup"><span data-stu-id="2b54c-157">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="2b54c-158">将图像缩放到合适大小。</span><span class="sxs-lookup"><span data-stu-id="2b54c-158">scaling the image to fit.</span></span>

<span data-ttu-id="2b54c-159">如果调整了适当的大小，您的选项卡配置页面应如下所示：</span><span class="sxs-lookup"><span data-stu-id="2b54c-159">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title=""新建配置" 选项卡" src="~/assets/images/tabs/config-dialog-Contoso.png" />

## <a name="best-practices"></a><span data-ttu-id="2b54c-161">最佳做法</span><span class="sxs-lookup"><span data-stu-id="2b54c-161">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="2b54c-162">始终包含默认状态</span><span class="sxs-lookup"><span data-stu-id="2b54c-162">Always include a default state</span></span>

<span data-ttu-id="2b54c-163">如果您的选项卡是可配置的，则包括默认状态以使选项卡易于设置。</span><span class="sxs-lookup"><span data-stu-id="2b54c-163">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="2b54c-164">深度链接</span><span class="sxs-lookup"><span data-stu-id="2b54c-164">Deep linking</span></span>

<span data-ttu-id="2b54c-165">只要有可能，卡片和 bot 应在承载的选项卡中深入链接到丰富的数据。例如，卡片可能会显示错误数据的摘要，但单击它可以在选项卡中显示整个 bug。</span><span class="sxs-lookup"><span data-stu-id="2b54c-165">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="2b54c-166">名称</span><span class="sxs-lookup"><span data-stu-id="2b54c-166">Naming</span></span>

<span data-ttu-id="2b54c-167">在很多情况下，您的应用程序的名称可能会产生很好的选项卡名称。</span><span class="sxs-lookup"><span data-stu-id="2b54c-167">In many cases, the name of your app may make a great tab name.</span></span> <span data-ttu-id="2b54c-168">但请考虑根据它们提供的功能命名选项卡。</span><span class="sxs-lookup"><span data-stu-id="2b54c-168">But consider naming your tabs according to the functionality they provide.</span></span>
