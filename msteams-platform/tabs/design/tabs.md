---
title: 选项卡的设计准则
description: 介绍为内容和协作创建选项卡的准则
keywords: 团队设计指南参考框架选项卡配置通道选项卡静态选项卡 "简单选项卡设计工作组" 选项卡
ms.openlocfilehash: 2d4e809e3ac11a5742113bf65125848a922c0207
ms.sourcegitcommit: 50571f5c6afc86177c4fe1032fe13366a7b706dd
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 12/04/2020
ms.locfileid: "49576860"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="1155d-104">内容和对话，所有使用选项卡一次</span><span class="sxs-lookup"><span data-stu-id="1155d-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="1155d-105">**移动客户端上的选项卡**</span><span class="sxs-lookup"><span data-stu-id="1155d-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="1155d-106">创建选项卡时，请遵循 [移动电话上的选项卡指南](./tabs-mobile.md) 。</span><span class="sxs-lookup"><span data-stu-id="1155d-106">Follow the [guidance for tabs on mobile](./tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="1155d-107">如果您的选项卡使用身份验证，则必须将团队 JavaScript SDK 升级到版本1.4.1 或更高版本，否则身份验证将失败。</span><span class="sxs-lookup"><span data-stu-id="1155d-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="1155d-108">**移动设备上的频道/组 (可配置) 选项卡：**</span><span class="sxs-lookup"><span data-stu-id="1155d-108">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="1155d-109">移动客户端仅显示具有值的可配置选项卡 `websiteUrl` 。</span><span class="sxs-lookup"><span data-stu-id="1155d-109">Mobile clients only show configurable tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="1155d-110">如果希望您的选项卡显示在团队移动客户端上，则必须设置的值 `websiteUrl` 。</span><span class="sxs-lookup"><span data-stu-id="1155d-110">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="1155d-111">移动上的默认打开行为是使用在浏览器中的外部打开 `websiteUrl` 。</span><span class="sxs-lookup"><span data-stu-id="1155d-111">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="1155d-112">对于发布到公用应用商店的应用程序，如果您希望频道选项卡在默认情况下在团队内打开，请遵循 [移动电话上的选项卡指南](~/tabs/design/tabs-mobile.md)，并转到您的支持代表以请求列入白名单。</span><span class="sxs-lookup"><span data-stu-id="1155d-112">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="1155d-113">选项卡是可用于在团队的随机工作流中共享内容、举行对话和托管第三方服务的画布。</span><span class="sxs-lookup"><span data-stu-id="1155d-113">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="1155d-114">当您在 Microsoft 团队中构建一个选项卡时，它会将 web 应用程序的前端和中心放置在易于从关键对话中访问的位置。</span><span class="sxs-lookup"><span data-stu-id="1155d-114">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="1155d-115">准则</span><span class="sxs-lookup"><span data-stu-id="1155d-115">Guidelines</span></span>

<span data-ttu-id="1155d-116">一个合适的选项卡应显示以下特征：</span><span class="sxs-lookup"><span data-stu-id="1155d-116">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="1155d-117">重点功能</span><span class="sxs-lookup"><span data-stu-id="1155d-117">Focused functionality</span></span>

<span data-ttu-id="1155d-118">当为满足特定需求而构建时，选项卡的工作效果最佳。</span><span class="sxs-lookup"><span data-stu-id="1155d-118">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="1155d-119">将重点放在一小部分任务或与选项卡所在通道相关的一组数据。</span><span class="sxs-lookup"><span data-stu-id="1155d-119">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="1155d-120">简化 chrome</span><span class="sxs-lookup"><span data-stu-id="1155d-120">Reduced chrome</span></span>

<span data-ttu-id="1155d-121">避免在选项卡中创建多个面板、添加导航层或要求用户在一个选项卡中垂直和水平滚动。换言之，请不要在选项卡中包含选项卡。</span><span class="sxs-lookup"><span data-stu-id="1155d-121">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

### <a name="integration"></a><span data-ttu-id="1155d-122">集成</span><span class="sxs-lookup"><span data-stu-id="1155d-122">Integration</span></span>

<span data-ttu-id="1155d-123">通过将 [自适应卡](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) 发布到对话中，查找通知用户有关选项卡活动的方法。</span><span class="sxs-lookup"><span data-stu-id="1155d-123">Find ways to notify users about tab activity by posting [adaptive cards](../../task-modules-and-cards/what-are-cards.md#adaptive-cards) to a conversation.</span></span>

### <a name="conversational"></a><span data-ttu-id="1155d-124">对话</span><span class="sxs-lookup"><span data-stu-id="1155d-124">Conversational</span></span>

<span data-ttu-id="1155d-125">寻找一种有助于围绕选项卡进行对话的方法。这样可确保在现有内容、数据或流程上进行对话中心。</span><span class="sxs-lookup"><span data-stu-id="1155d-125">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="1155d-126">精简访问</span><span class="sxs-lookup"><span data-stu-id="1155d-126">Streamlined access</span></span>

<span data-ttu-id="1155d-127">请确保在适当的时间授予对正确人员的访问权限。</span><span class="sxs-lookup"><span data-stu-id="1155d-127">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="1155d-128">保持您的登录过程很简单将避免为发布和协作创建障碍。</span><span class="sxs-lookup"><span data-stu-id="1155d-128">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="responsiveness-to-window-sizing"></a><span data-ttu-id="1155d-129">对窗口大小的响应</span><span class="sxs-lookup"><span data-stu-id="1155d-129">Responsiveness to window sizing</span></span>

<span data-ttu-id="1155d-130">在窗口大小中，可以将团队用作720px，以确保在小窗口中可用的选项卡与极高分辨率的可用性同样重要。</span><span class="sxs-lookup"><span data-stu-id="1155d-130">Teams can be used in window sizes as small as 720px, so making sure that a tab is usable in a small window is just as important as usability at very high resolutions.</span></span>

### <a name="flat-navigation"></a><span data-ttu-id="1155d-131">平面导航</span><span class="sxs-lookup"><span data-stu-id="1155d-131">Flat navigation</span></span>

<span data-ttu-id="1155d-132">我们要求开发人员不要将其整个门户添加到选项卡中。保持导航相对平整有助于保持更简单的会话模式。</span><span class="sxs-lookup"><span data-stu-id="1155d-132">We ask developers not to add their entire portal to a tab. Keeping the navigation relatively flat helps maintain a simpler conversational model.</span></span> <span data-ttu-id="1155d-133">换言之，对话是关于事情的列表（如已会审的工作项）或一个内容（如规范）。</span><span class="sxs-lookup"><span data-stu-id="1155d-133">In other words, the conversation is about a list of things, such as triaged work items, or a single thing, like a spec.</span></span>

<span data-ttu-id="1155d-134">深入导航层次结构中有一些固有的导航挑战，在线程对话中。</span><span class="sxs-lookup"><span data-stu-id="1155d-134">There are inherent navigational challenges with deep navigation hierarchy, within threaded conversations.</span></span> <span data-ttu-id="1155d-135">为获得最佳用户体验，应将选项卡导航保持在最少，并按如下方式设计：</span><span class="sxs-lookup"><span data-stu-id="1155d-135">For the best user experience, your tab navigation should be kept to a minimum and be designed as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="1155d-136">**打开一个任务模块，如单个工作项或实体**。</span><span class="sxs-lookup"><span data-stu-id="1155d-136">**Opens a task module such as an individual work item or entity**.</span></span> <span data-ttu-id="1155d-137">这将完全阻止聊天，并且是最佳选择，它是专门了解选项卡的聊天，而不是子实体或编辑体验。</span><span class="sxs-lookup"><span data-stu-id="1155d-137">This precludes chat entirely and is the best option to keep chat specifically about the tab and not the sub-entities or editing experiences.</span></span>
>* <span data-ttu-id="1155d-138">**在 iframe 中打开伪对话框**。</span><span class="sxs-lookup"><span data-stu-id="1155d-138">**Opens a pseudo dialog in an iframe**.</span></span> <span data-ttu-id="1155d-139">如果与屏蔽背景一起使用，我们建议使用较亮的颜色，而不是黑色。</span><span class="sxs-lookup"><span data-stu-id="1155d-139">If used with a screened background we recommend using the lighter color rather than the dark.</span></span> <span data-ttu-id="1155d-140">`app-gray-10 at 30%`透明度工作良好。</span><span class="sxs-lookup"><span data-stu-id="1155d-140">The `app-gray-10 at 30%` transparency works well.</span></span>
>* <span data-ttu-id="1155d-141">**打开浏览器页面**。</span><span class="sxs-lookup"><span data-stu-id="1155d-141">**Opens a browser page**.</span></span>

### <a name="personality"></a><span data-ttu-id="1155d-142">特征</span><span class="sxs-lookup"><span data-stu-id="1155d-142">Personality</span></span>

<span data-ttu-id="1155d-143">您的选项卡画布极有机会为你的体验提供品牌。</span><span class="sxs-lookup"><span data-stu-id="1155d-143">Your tab canvas presents a great opportunity to brand your experience.</span></span> <span data-ttu-id="1155d-144">您的徽标是标识的重要部分，与您的用户的连接。，因此请务必包含它：</span><span class="sxs-lookup"><span data-stu-id="1155d-144">Your logo is an important part of your identity and connection with your users., so be sure to include it:</span></span>

> [!div class="checklist"]
>
>* <span data-ttu-id="1155d-145">将徽标放置在左右角或沿下边缘</span><span class="sxs-lookup"><span data-stu-id="1155d-145">Place your logo in the left or right corner or along the bottom edge</span></span>
> * <span data-ttu-id="1155d-146">保持您的徽标较小且不引人注目</span><span class="sxs-lookup"><span data-stu-id="1155d-146">Keep your logo small and unobtrusive</span></span>

<span data-ttu-id="1155d-147">合并自己的颜色和布局 twill 也有助于传达个性。</span><span class="sxs-lookup"><span data-stu-id="1155d-147">Incorporating your own colors and layouts twill also aid in communicating personality.</span></span>

> [!TIP]
> <span data-ttu-id="1155d-148">请使用我们的视觉样式，让你的服务感觉像团队的一部分。</span><span class="sxs-lookup"><span data-stu-id="1155d-148">Please work with our visual style so your service feels like a part of Teams.</span></span> <span data-ttu-id="1155d-149">*请参阅* 示例 [团队颜色](../../concepts/design/components/color.md)</span><span class="sxs-lookup"><span data-stu-id="1155d-149">*See*, for example [Teams Colors](../../concepts/design/components/color.md)</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="1155d-150">选项卡布局</span><span class="sxs-lookup"><span data-stu-id="1155d-150">Tab layouts</span></span>

[!INCLUDE [Tab layouts](../../includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="1155d-151">选项卡的类型</span><span class="sxs-lookup"><span data-stu-id="1155d-151">Types of tabs</span></span>

[!INCLUDE [Tab types](../../includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="1155d-152">配置页高度</span><span class="sxs-lookup"><span data-stu-id="1155d-152">Configuration page height</span></span>

>[!IMPORTANT]
><span data-ttu-id="1155d-153">在9月2018中，选项卡 [配置页面](~/tabs/how-to/create-tab-pages/configuration-page.md) 的高度增加，而宽度保持不变。</span><span class="sxs-lookup"><span data-stu-id="1155d-153">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="1155d-154">如果您的应用程序是为较旧的大小设计的，则选项卡配置页将具有大量的垂直空白。</span><span class="sxs-lookup"><span data-stu-id="1155d-154">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="1155d-155">从此更改中免除的旧版应用程序将需要在更新后与 Microsoft 联系，以适应新的维度。</span><span class="sxs-lookup"><span data-stu-id="1155d-155">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="1155d-156">选项卡配置页的尺寸：</span><span class="sxs-lookup"><span data-stu-id="1155d-156">The dimensions of the tab configuration page:</span></span>


<img width="450px" title="配置选项卡的大小" src="~/assets/images/tabs/config-dialog-Contoso2.png" alt="sizes for config tabs" />


### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="1155d-158">选项卡配置页面格式的准则</span><span class="sxs-lookup"><span data-stu-id="1155d-158">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="1155d-159">使固定高度图形元素上的选项卡配置页的内容区域的最小高度为基准。</span><span class="sxs-lookup"><span data-stu-id="1155d-159">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="1155d-160">使用) 的配置页面中的内容区域的高度计算可用的垂直空间 (`window.innerHeight` 。</span><span class="sxs-lookup"><span data-stu-id="1155d-160">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="1155d-161">这将返回 `<iframe>` 配置页面所驻留的大小，在将来的版本中可能会发生更改。</span><span class="sxs-lookup"><span data-stu-id="1155d-161">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="1155d-162">通过使用此值，你的内容将自动调整为将来的更改。</span><span class="sxs-lookup"><span data-stu-id="1155d-162">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="1155d-163">将垂直空间分配给可变高度元素减去固定高度元素所需的值。</span><span class="sxs-lookup"><span data-stu-id="1155d-163">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="1155d-164">对于 " *登录* 状态"，将内容垂直和水平居中。</span><span class="sxs-lookup"><span data-stu-id="1155d-164">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="1155d-165">如果您需要背景图像，则需要一个新图像，调整大小以适合 (首选) 的区域，也可以保留相同的图像并在其中进行选择：</span><span class="sxs-lookup"><span data-stu-id="1155d-165">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="1155d-166">与左上角对齐。</span><span class="sxs-lookup"><span data-stu-id="1155d-166">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="1155d-167">将图像缩放到合适大小。</span><span class="sxs-lookup"><span data-stu-id="1155d-167">scaling the image to fit.</span></span>

<span data-ttu-id="1155d-168">如果调整了适当的大小，您的选项卡配置页面应如下所示：</span><span class="sxs-lookup"><span data-stu-id="1155d-168">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title=""新建配置" 选项卡" src="~/assets/images/tabs/config-dialog-Contoso.png" alt="new config tab"/>

## <a name="best-practices"></a><span data-ttu-id="1155d-170">最佳做法</span><span class="sxs-lookup"><span data-stu-id="1155d-170">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="1155d-171">始终包含默认状态</span><span class="sxs-lookup"><span data-stu-id="1155d-171">Always include a default state</span></span>

<span data-ttu-id="1155d-172">如果您的选项卡是可配置的，则包括默认状态以使选项卡易于设置。</span><span class="sxs-lookup"><span data-stu-id="1155d-172">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="1155d-173">深度链接</span><span class="sxs-lookup"><span data-stu-id="1155d-173">Deep linking</span></span>

<span data-ttu-id="1155d-174">只要有可能，卡片和 bot 应在承载的选项卡中深入链接到丰富的数据。例如，卡片可能会显示错误数据的摘要，但单击它可以在选项卡中显示整个 bug。</span><span class="sxs-lookup"><span data-stu-id="1155d-174">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="1155d-175">名称</span><span class="sxs-lookup"><span data-stu-id="1155d-175">Naming</span></span>

<span data-ttu-id="1155d-176">在很多情况下，您的应用程序的名称将产生很好的选项卡名称。</span><span class="sxs-lookup"><span data-stu-id="1155d-176">In many cases, the name of your app will make a great tab name.</span></span> <span data-ttu-id="1155d-177">此外，还应考虑根据它们提供的功能命名选项卡。</span><span class="sxs-lookup"><span data-stu-id="1155d-177">But, also consider naming your tabs according to the functionality they provide.</span></span>

### <a name="multi-window"></a><span data-ttu-id="1155d-178">多窗口</span><span class="sxs-lookup"><span data-stu-id="1155d-178">Multi-window</span></span>

<span data-ttu-id="1155d-179">具有复杂编辑功能的频道选项卡必须在多窗口中打开编辑器视图，而不是在选项卡中打开。</span><span class="sxs-lookup"><span data-stu-id="1155d-179">Channel tabs that have complex editing capabilities must open the editor view in multi-window rather than a tab.</span></span>

### <a name="no-horizontal-scrolling"></a><span data-ttu-id="1155d-180">无水平滚动</span><span class="sxs-lookup"><span data-stu-id="1155d-180">No horizontal scrolling</span></span>

<span data-ttu-id="1155d-181">制表位不应具有水平滚动。</span><span class="sxs-lookup"><span data-stu-id="1155d-181">Tab should not have horizontal scrolling.</span></span>

### <a name="easy-navigation"></a><span data-ttu-id="1155d-182">轻松导航</span><span class="sxs-lookup"><span data-stu-id="1155d-182">Easy navigation</span></span>

<span data-ttu-id="1155d-183">在选项卡应用程序中导航必须易于遵循，例如，在必要/适用的地方，页面具有以下内容：</span><span class="sxs-lookup"><span data-stu-id="1155d-183">Navigation inside a tab app must be easy to follow i.e. pages have the following where necessary/applicable:</span></span>
* <span data-ttu-id="1155d-184">后退按钮</span><span class="sxs-lookup"><span data-stu-id="1155d-184">Back buttons</span></span>
* <span data-ttu-id="1155d-185">页面页眉</span><span class="sxs-lookup"><span data-stu-id="1155d-185">Page headers</span></span>
* <span data-ttu-id="1155d-186">导航</span><span class="sxs-lookup"><span data-stu-id="1155d-186">Breadcrumbs</span></span>
* <span data-ttu-id="1155d-187">汉堡菜单</span><span class="sxs-lookup"><span data-stu-id="1155d-187">Hamburger menus</span></span>

### <a name="undo-last-action"></a><span data-ttu-id="1155d-188">撤消上一步操作</span><span class="sxs-lookup"><span data-stu-id="1155d-188">Undo last action</span></span>

<span data-ttu-id="1155d-189">用户必须能够撤消其在应用中的最后一项操作。</span><span class="sxs-lookup"><span data-stu-id="1155d-189">User must be able to undo their last action in the app.</span></span>

### <a name="share-content"></a><span data-ttu-id="1155d-190">共享内容</span><span class="sxs-lookup"><span data-stu-id="1155d-190">Share content</span></span>

<span data-ttu-id="1155d-191">个人应用应允许用户与其他团队成员共享个人应用程序体验中的内容。</span><span class="sxs-lookup"><span data-stu-id="1155d-191">Personal apps should enable users to share content from a personal app experience with other team members.</span></span> <span data-ttu-id="1155d-192">频道选项卡必须提供与主要团队导航相补充的导航，而不是与之冲突 (如左滑轨导航栏) 。</span><span class="sxs-lookup"><span data-stu-id="1155d-192">Channel tab must provide navigation that complements the main Teams navigation, rather than conflicting with it (such as left rail nav-bars).</span></span>

### <a name="single-view"></a><span data-ttu-id="1155d-193">单一视图</span><span class="sxs-lookup"><span data-stu-id="1155d-193">Single view</span></span>

<span data-ttu-id="1155d-194">个人应用应在单个视图中显示该应用程序的团队或组聊天范围实例的内容，例如，Trello 用户应能够在其个人应用程序的团队级别查看他们参与的所有 Trello 板实例。</span><span class="sxs-lookup"><span data-stu-id="1155d-194">Personal apps should present content from team or group chat scoped instances of that app in a single view, e.g., a Trello user should be able to see all instances of Trello boards they participate in at a team level in their personal app.</span></span>

### <a name="no-app-bar"></a><span data-ttu-id="1155d-195">无应用程序栏</span><span class="sxs-lookup"><span data-stu-id="1155d-195">No app bar</span></span>

<span data-ttu-id="1155d-196">选项卡不应提供带有与主团队导航相冲突的左侧导轨图标的应用程序栏。</span><span class="sxs-lookup"><span data-stu-id="1155d-196">Tabs should not provide an app bar with icons in the left rail that conflicts with the main Teams navigation.</span></span>

### <a name="navigation"></a><span data-ttu-id="1155d-197">导航</span><span class="sxs-lookup"><span data-stu-id="1155d-197">Navigation</span></span>

<span data-ttu-id="1155d-198">在应用程序中，选项卡的导航级别不应超过3个。</span><span class="sxs-lookup"><span data-stu-id="1155d-198">Tabs should not have more than 3 levels of navigation within the app.</span></span>

### <a name="l2l3-view"></a><span data-ttu-id="1155d-199">L2/L3 视图</span><span class="sxs-lookup"><span data-stu-id="1155d-199">L2/L3 view</span></span>

<span data-ttu-id="1155d-200">选项卡中的第二页和第三页应在主选项卡区域中的 L2/L3 视图中打开，这是通过痕迹导航导航的。</span><span class="sxs-lookup"><span data-stu-id="1155d-200">Secondary and tertiary pages in a tab should be opened in an L2/L3 view in the main tab area that is navigated via the breadcrumb.</span></span>

### <a name="no-link-to-external-browser"></a><span data-ttu-id="1155d-201">无指向外部浏览器的链接</span><span class="sxs-lookup"><span data-stu-id="1155d-201">No link to external browser</span></span>

<span data-ttu-id="1155d-202">选项卡中的链接目标不应链接到外部浏览器，但应链接到包含在团队中的 div 元素。</span><span class="sxs-lookup"><span data-stu-id="1155d-202">Link targets in tabs should not link to an external browser but should link to div elements contained within Teams.</span></span> <span data-ttu-id="1155d-203">例如，在任务模块、选项卡等中。</span><span class="sxs-lookup"><span data-stu-id="1155d-203">For example, inside task Modules, tabs, etc.</span></span>

## <a name="notifications-for-tabs"></a><span data-ttu-id="1155d-204">选项卡通知</span><span class="sxs-lookup"><span data-stu-id="1155d-204">Notifications for tabs</span></span>

<span data-ttu-id="1155d-205">对于选项卡内容更改，有两种通知模式：</span><span class="sxs-lookup"><span data-stu-id="1155d-205">There are two modes of notification for tab content changes:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="1155d-206">**使用应用程序 API 将更改通知用户**。</span><span class="sxs-lookup"><span data-stu-id="1155d-206">**Use the app API to notify users of changes**.</span></span> <span data-ttu-id="1155d-207">此消息将显示在用户的活动源和指向该选项卡的深层链接中。 *请参阅*  [创建指向 Microsoft 团队中的内容和功能的深层链接](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true )</span><span class="sxs-lookup"><span data-stu-id="1155d-207">This message will show up in the user’s activity feed and deep link to the tab. *See*  [Create deep links to content and features in Microsoft Teams](../../concepts/build-and-test/deep-links.md?view=msteams-client-js-latest&preserve-view=true )</span></span>

> * <span data-ttu-id="1155d-208">**使用 bot**。</span><span class="sxs-lookup"><span data-stu-id="1155d-208">**Use a bot**.</span></span> <span data-ttu-id="1155d-209">如果为 Tab 线程的目标，则此方法是首选方法。</span><span class="sxs-lookup"><span data-stu-id="1155d-209">This method is preferred especially if the Tab thread is targeted.</span></span> <span data-ttu-id="1155d-210">结果将是，选项卡的线程对话将作为最近活动的视图移动到视图中。</span><span class="sxs-lookup"><span data-stu-id="1155d-210">The result will be that the tab’s threaded conversation will be moved into view as recently active.</span></span> <span data-ttu-id="1155d-211">此方法还允许在通知的发送方式方面有一些复杂之处。</span><span class="sxs-lookup"><span data-stu-id="1155d-211">This method also allows for some sophistication in how the notification is sent.</span></span>

<span data-ttu-id="1155d-212">将邮件发送到选项卡线程可将对所有用户的活动的感知提高到所有用户，而无需明确通知每个人。</span><span class="sxs-lookup"><span data-stu-id="1155d-212">Sending a message to a tab thread increases the awareness of activity to all users without explicitly notifying everyone.</span></span> <span data-ttu-id="1155d-213">这是不带噪音的感知。</span><span class="sxs-lookup"><span data-stu-id="1155d-213">This is awareness without noise.</span></span> <span data-ttu-id="1155d-214">此外，当您 `@mention`  将特定用户的通知放在其源中时，会将它们直接链接到 tab 线程。</span><span class="sxs-lookup"><span data-stu-id="1155d-214">In addition, when you `@mention`  specific users the same notification will be placed in their feed, deep linking them to the tab thread directly.</span></span>

### <a name="tab-design-best-practices"></a><span data-ttu-id="1155d-215">选项卡设计最佳实践</span><span class="sxs-lookup"><span data-stu-id="1155d-215">Tab design best practices</span></span>

* <span data-ttu-id="1155d-216">个人/静态选项卡应使用户能够与其他团队成员共享个人应用程序体验中的内容。</span><span class="sxs-lookup"><span data-stu-id="1155d-216">Personal/Static tabs should enable users to share content from a personal app experience with another team members.</span></span>
* <span data-ttu-id="1155d-217">"个人/静态" 选项卡可以在单个视图中显示来自 team 或 group chat 的应用程序范围实例的内容。</span><span class="sxs-lookup"><span data-stu-id="1155d-217">Personal/Static tabs may present content from team or group chat scoped instances of that app in a single view.</span></span>
* <span data-ttu-id="1155d-218">选项卡中的链接目标不应链接到外部浏览器，但应链接到包含在团队中的 div 元素 (例如，内部、任务模块、选项卡等) 。</span><span class="sxs-lookup"><span data-stu-id="1155d-218">Link targets in tabs should not link to an external browser but should link to div elements contained within Teams (example-inside, task modules, tabs, etc).</span></span>
* <span data-ttu-id="1155d-219">选项卡应响应团队主题。</span><span class="sxs-lookup"><span data-stu-id="1155d-219">Tabs should be responsive to Team’s themes.</span></span> <span data-ttu-id="1155d-220">当 "团队" 主题发生更改时，应用程序中的主题也应更改以反映该主题。</span><span class="sxs-lookup"><span data-stu-id="1155d-220">When the Teams theme is changed, the theme within the app should also change to reflect that theme.</span></span>
* <span data-ttu-id="1155d-221">在可能的情况下，选项卡应使用团队样式的组件。</span><span class="sxs-lookup"><span data-stu-id="1155d-221">Tabs should use Teams-styled components where possible.</span></span> <span data-ttu-id="1155d-222">这意味着采用团队字体，键入斜坡、调色板、网格系统、动作、语音音频等。</span><span class="sxs-lookup"><span data-stu-id="1155d-222">It means adopting Teams fonts, type ramps, color palettes, grid system, motion, tone of voice, etc.</span></span>
* <span data-ttu-id="1155d-223">选项卡应将团队交互行为用于对话、信息层次结构等的页面内导航、定位和使用。</span><span class="sxs-lookup"><span data-stu-id="1155d-223">Tabs should use Teams interaction behaviors for in-page navigation, position, and use of dialogs, information hierarchies, etc.</span></span>
* <span data-ttu-id="1155d-224">在应用程序内导航时，选项卡应使用标准团队汉堡菜单和/或痕迹。</span><span class="sxs-lookup"><span data-stu-id="1155d-224">Tabs should use the standard Teams hamburger menu and/or breadcrumb for in-app navigation.</span></span> <span data-ttu-id="1155d-225">选项卡不应提供带有与主团队导航相冲突的左侧导轨图标的应用程序栏。</span><span class="sxs-lookup"><span data-stu-id="1155d-225">Tabs should not provide an app bar with icons in the left rail that conflicts with the main Teams navigation.</span></span>
* <span data-ttu-id="1155d-226">在应用程序中，选项卡的导航级别不应超过三个。</span><span class="sxs-lookup"><span data-stu-id="1155d-226">Tabs should not have more than three levels of navigation within the app.</span></span>
* <span data-ttu-id="1155d-227">选项卡中的第二页和第三页应在主选项卡区域中的 L2/L3 视图中打开，这是通过痕迹导航导航的。</span><span class="sxs-lookup"><span data-stu-id="1155d-227">Secondary and tertiary pages in a tab should be opened in an L2/L3 view in the main tab area that is navigated via the breadcrumb.</span></span>
* <span data-ttu-id="1155d-228">应用程序中具有复杂编辑功能的选项卡应在多窗口中打开编辑器视图，而不是在选项卡中打开桌面和 web) 的 (的选项卡。</span><span class="sxs-lookup"><span data-stu-id="1155d-228">Tabs that have complex editing capabilities within the app should open the editor view in multi-window rather than a tab (for desktop and web).</span></span>
* <span data-ttu-id="1155d-229">若要改进用户体验，请在首次运行时向用户发送欢迎消息，并响应 " **hi**"、" **帮助**" 和 " **hello** " 命令，并提供个人 bot。</span><span class="sxs-lookup"><span data-stu-id="1155d-229">For improved user experience include a personal bot that sends a welcome message to the user on the first run and responds to the **hi**, **help**, and **hello** commands.</span></span> <span data-ttu-id="1155d-230">您可以参阅有关 [对话 bot](../../bots/what-are-bots.md#in-a-one-to-one-chat) 的文档以获取进一步帮助。</span><span class="sxs-lookup"><span data-stu-id="1155d-230">You can refer to the documentation on [conversational bots](../../bots/what-are-bots.md#in-a-one-to-one-chat) for further assistance.</span></span>
