---
title: 选项卡的设计准则
description: 介绍为内容和协作创建选项卡的准则
keywords: 团队设计指南参考框架选项卡配置
ms.openlocfilehash: c718dd897d314ecb5acfbb7cc537b8eead142b0c
ms.sourcegitcommit: 646a8224523be7db96f9686e22d420d62d55d4b4
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 03/02/2020
ms.locfileid: "42365260"
---
# <a name="content-and-conversations-all-at-once-using-tabs"></a><span data-ttu-id="b85aa-104">内容和对话，所有使用选项卡一次</span><span class="sxs-lookup"><span data-stu-id="b85aa-104">Content and conversations, all at once using tabs</span></span>

> [!Important]
> <span data-ttu-id="b85aa-105">**移动客户端上的选项卡**</span><span class="sxs-lookup"><span data-stu-id="b85aa-105">**Tabs on Mobile Clients**</span></span>
>
> <span data-ttu-id="b85aa-106">创建选项卡时，请遵循[移动电话上的选项卡指南](./tabs-mobile.md)。</span><span class="sxs-lookup"><span data-stu-id="b85aa-106">Follow the [guidance for tabs on mobile](./tabs-mobile.md) when creating your tabs.</span></span> <span data-ttu-id="b85aa-107">如果您的选项卡使用身份验证，则必须将团队 JavaScript SDK 升级到版本1.4.1 或更高版本，否则身份验证将失败。</span><span class="sxs-lookup"><span data-stu-id="b85aa-107">If your tab uses authentication, you must upgrade your Teams JavaScript SDK to version 1.4.1 or later, or authentication will fail.</span></span>
>
> <span data-ttu-id="b85aa-108">**移动设备上的个人（静态）选项卡：**</span><span class="sxs-lookup"><span data-stu-id="b85aa-108">**Personal (static) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="b85aa-109">在[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中，可以使用静态选项卡（个人应用）。</span><span class="sxs-lookup"><span data-stu-id="b85aa-109">Static tabs (personal app) are available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span>
> * <span data-ttu-id="b85aa-110">在构建静态选项卡时，请确保遵循[移动电话上的选项卡指南](~/tabs/design/tabs-mobile.md)</span><span class="sxs-lookup"><span data-stu-id="b85aa-110">While building your static tabs, ensure to follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md)</span></span>
>
> <span data-ttu-id="b85aa-111">**移动设备上的频道/组（可配置）选项卡：**</span><span class="sxs-lookup"><span data-stu-id="b85aa-111">**Channel/group (configurable) tabs on mobile:**</span></span>
>
> * <span data-ttu-id="b85aa-112">移动客户端仅显示具有值的`websiteUrl`选项卡。</span><span class="sxs-lookup"><span data-stu-id="b85aa-112">Mobile clients only show tabs that have a value for `websiteUrl`.</span></span> <span data-ttu-id="b85aa-113">如果希望您的选项卡显示在团队移动客户端上，则必须设置的`websiteUrl`值。</span><span class="sxs-lookup"><span data-stu-id="b85aa-113">If you want your tab to appear on the Teams mobile clients, you must set the value of `websiteUrl`.</span></span>
> * <span data-ttu-id="b85aa-114">移动上的默认打开行为是使用在浏览器中的`websiteUrl`外部打开。</span><span class="sxs-lookup"><span data-stu-id="b85aa-114">Default open behavior on mobile is to open outside in browser using the `websiteUrl`.</span></span> <span data-ttu-id="b85aa-115">对于发布到公用应用商店的应用程序，如果您希望频道选项卡在默认情况下在团队内打开，请遵循[移动电话上的选项卡指南](~/tabs/design/tabs-mobile.md)，并转到您的支持代表以请求列入白名单。</span><span class="sxs-lookup"><span data-stu-id="b85aa-115">For apps published to the public App Store, if you want your channel tab to open inside teams by default, follow the [guidance for tabs on mobile](~/tabs/design/tabs-mobile.md), and reach out to your support rep to request to be whitelisted.</span></span>

<span data-ttu-id="b85aa-116">选项卡是可用于在团队的随机工作流中共享内容、举行对话和托管第三方服务的画布。</span><span class="sxs-lookup"><span data-stu-id="b85aa-116">Tabs are canvases that you can use to share content, hold conversations, and host third-party services, all within a team’s organic workflow.</span></span> <span data-ttu-id="b85aa-117">当您在 Microsoft 团队中构建一个选项卡时，它会将 web 应用程序的前端和中心放置在易于从关键对话中访问的位置。</span><span class="sxs-lookup"><span data-stu-id="b85aa-117">When you build a tab in Microsoft Teams, it puts your web app front and center where it’s easily accessible from key conversations.</span></span>

## <a name="guidelines"></a><span data-ttu-id="b85aa-118">准则</span><span class="sxs-lookup"><span data-stu-id="b85aa-118">Guidelines</span></span>

<span data-ttu-id="b85aa-119">一个合适的选项卡应显示以下特征：</span><span class="sxs-lookup"><span data-stu-id="b85aa-119">A good tab should display the following characteristics:</span></span>

### <a name="focused-functionality"></a><span data-ttu-id="b85aa-120">重点功能</span><span class="sxs-lookup"><span data-stu-id="b85aa-120">Focused functionality</span></span>

<span data-ttu-id="b85aa-121">当为满足特定需求而构建时，选项卡的工作效果最佳。</span><span class="sxs-lookup"><span data-stu-id="b85aa-121">Tabs work best when they’re built to address a specific need.</span></span> <span data-ttu-id="b85aa-122">将重点放在一小部分任务或与选项卡所在通道相关的一组数据。</span><span class="sxs-lookup"><span data-stu-id="b85aa-122">Focus on a small set of tasks or a subset of data that’s relevant to the channel the tab is in.</span></span>

### <a name="reduced-chrome"></a><span data-ttu-id="b85aa-123">简化 chrome</span><span class="sxs-lookup"><span data-stu-id="b85aa-123">Reduced chrome</span></span>

<span data-ttu-id="b85aa-124">避免在选项卡中创建多个面板、添加导航层或要求用户在一个选项卡中垂直和水平滚动。换言之，请不要在选项卡中包含选项卡。</span><span class="sxs-lookup"><span data-stu-id="b85aa-124">Avoid creating multiple panels in a tab, adding layers of navigation, or requiring users to scroll both vertically and horizontally in one tab. In other words, try not to have tabs in your tab.</span></span>

### <a name="integration"></a><span data-ttu-id="b85aa-125">集中</span><span class="sxs-lookup"><span data-stu-id="b85aa-125">Integration</span></span>

<span data-ttu-id="b85aa-126">查找通过将卡发布到对话来通知用户选项卡活动的方法。</span><span class="sxs-lookup"><span data-stu-id="b85aa-126">Find ways to notify users about tab activity by posting cards to a conversation, for example.</span></span>

### <a name="conversational"></a><span data-ttu-id="b85aa-127">对话</span><span class="sxs-lookup"><span data-stu-id="b85aa-127">Conversational</span></span>

<span data-ttu-id="b85aa-128">寻找一种有助于围绕选项卡进行对话的方法。这样可确保在现有内容、数据或流程上进行对话中心。</span><span class="sxs-lookup"><span data-stu-id="b85aa-128">Find a way to facilitate conversation around a tab. This ensures that conversations center on the content, data, or process at hand.</span></span>

### <a name="streamlined-access"></a><span data-ttu-id="b85aa-129">精简访问</span><span class="sxs-lookup"><span data-stu-id="b85aa-129">Streamlined access</span></span>

<span data-ttu-id="b85aa-130">请确保在适当的时间授予对正确人员的访问权限。</span><span class="sxs-lookup"><span data-stu-id="b85aa-130">Make sure you’re granting access to the right people at the right time.</span></span> <span data-ttu-id="b85aa-131">保持您的登录过程很简单将避免为发布和协作创建障碍。</span><span class="sxs-lookup"><span data-stu-id="b85aa-131">Keeping your sign-in process simple will avoid creating barriers to contribution and collaboration.</span></span>

### <a name="responsiveness-to-window-sizing"></a><span data-ttu-id="b85aa-132">对窗口大小的响应</span><span class="sxs-lookup"><span data-stu-id="b85aa-132">Responsiveness to window sizing</span></span>

<span data-ttu-id="b85aa-133">在窗口大小中，可以将团队用作720px，以确保在小窗口中可用的选项卡与极高分辨率的可用性同样重要。</span><span class="sxs-lookup"><span data-stu-id="b85aa-133">Teams can be used in window sizes as small as 720px, so making sure that a tab is usable in a small window is just as important as usability at very high resolutions.</span></span>

### <a name="flat-navigation"></a><span data-ttu-id="b85aa-134">平面导航</span><span class="sxs-lookup"><span data-stu-id="b85aa-134">Flat navigation</span></span>

<span data-ttu-id="b85aa-135">我们要求开发人员不要将其整个门户添加到选项卡。保持导航相对平整有助于保持更简单的会话模式。</span><span class="sxs-lookup"><span data-stu-id="b85aa-135">We ask developers not to add their entire portal to a tab. Keeping the navigation relatively flat helps maintain a simpler conversational model.</span></span> <span data-ttu-id="b85aa-136">换言之，对话是关于事情的列表（如已会审的工作项）或一个内容（如规范）。</span><span class="sxs-lookup"><span data-stu-id="b85aa-136">In other words, the conversation is about a list of things, such as triaged work items, or a single thing, like a spec.</span></span>

<span data-ttu-id="b85aa-137">深入导航层次结构中有一些固有的导航挑战，在线程对话中。</span><span class="sxs-lookup"><span data-stu-id="b85aa-137">There are inherent navigational challenges with deep navigation hierarchy, within threaded conversations.</span></span> <span data-ttu-id="b85aa-138">为获得最佳用户体验，应将选项卡导航保持在最少，并按如下方式设计：</span><span class="sxs-lookup"><span data-stu-id="b85aa-138">For the best user experience, your tab navigation should be kept to a minimum and be designed as follows:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="b85aa-139">**打开一个任务模块，如单个工作项或实体**。</span><span class="sxs-lookup"><span data-stu-id="b85aa-139">**Opens a task module such as an individual work item or entity**.</span></span> <span data-ttu-id="b85aa-140">这将完全阻止聊天，并且是最佳选择，它是专门了解选项卡的聊天，而不是子实体或编辑体验。</span><span class="sxs-lookup"><span data-stu-id="b85aa-140">This precludes chat entirely and is the best option to keep chat specifically about the tab and not the sub-entities or editing experiences.</span></span>
>* <span data-ttu-id="b85aa-141">**在 iframe 中打开伪对话框**。</span><span class="sxs-lookup"><span data-stu-id="b85aa-141">**Opens a pseudo dialog in an iframe**.</span></span> <span data-ttu-id="b85aa-142">如果与屏蔽背景一起使用，我们建议使用较亮的颜色，而不是黑色。</span><span class="sxs-lookup"><span data-stu-id="b85aa-142">If used with a screened background we recommend using the lighter color rather than the dark.</span></span> <span data-ttu-id="b85aa-143">`app-gray-10 at 30%`透明度工作良好。</span><span class="sxs-lookup"><span data-stu-id="b85aa-143">The `app-gray-10 at 30%` transparency works well.</span></span>
>* <span data-ttu-id="b85aa-144">**打开浏览器页面**。</span><span class="sxs-lookup"><span data-stu-id="b85aa-144">**Opens a browser page**.</span></span>

### <a name="personality"></a><span data-ttu-id="b85aa-145">特征</span><span class="sxs-lookup"><span data-stu-id="b85aa-145">Personality</span></span>

<span data-ttu-id="b85aa-146">您的选项卡画布极有机会为你的体验提供品牌。</span><span class="sxs-lookup"><span data-stu-id="b85aa-146">Your tab canvas presents a great opportunity to brand your experience.</span></span> <span data-ttu-id="b85aa-147">您的徽标是标识的重要部分，与您的用户的连接。，因此请务必包含它：</span><span class="sxs-lookup"><span data-stu-id="b85aa-147">Your logo is an important part of your identity and connection with your users., so be sure to include it:</span></span>

> [!div class="checklist"]
>
>* <span data-ttu-id="b85aa-148">将徽标放置在左右角或沿下边缘</span><span class="sxs-lookup"><span data-stu-id="b85aa-148">Place your logo in the left or right corner or along the bottom edge</span></span>
> * <span data-ttu-id="b85aa-149">保持您的徽标较小且不引人注目</span><span class="sxs-lookup"><span data-stu-id="b85aa-149">Keep your logo small and unobtrusive</span></span>

<span data-ttu-id="b85aa-150">合并自己的颜色和布局 twill 也有助于传达个性。</span><span class="sxs-lookup"><span data-stu-id="b85aa-150">Incorporating your own colors and layouts twill also aid in communicating personality.</span></span>

> [!TIP]
> <span data-ttu-id="b85aa-151">请使用我们的视觉样式，让你的服务感觉像团队的一部分。</span><span class="sxs-lookup"><span data-stu-id="b85aa-151">Please work with our visual style so your service feels like a part of Teams.</span></span> <span data-ttu-id="b85aa-152">*请参阅*（例如 [团队颜色] （/concepts/design/components/typography.md</span><span class="sxs-lookup"><span data-stu-id="b85aa-152">*See*, for example [Teams Colors](/concepts/design/components/typography.md</span></span>

---

## <a name="tab-layouts"></a><span data-ttu-id="b85aa-153">选项卡布局</span><span class="sxs-lookup"><span data-stu-id="b85aa-153">Tab layouts</span></span>

[!INCLUDE [Tab layouts](../../includes/design/tab-layouts.html)]

---

## <a name="types-of-tabs"></a><span data-ttu-id="b85aa-154">选项卡的类型</span><span class="sxs-lookup"><span data-stu-id="b85aa-154">Types of tabs</span></span>

[!INCLUDE [Tab types](../../includes/design/tab-types.html)]

---

## <a name="configuration-page-height"></a><span data-ttu-id="b85aa-155">配置页高度</span><span class="sxs-lookup"><span data-stu-id="b85aa-155">Configuration page height</span></span>

>[!IMPORTANT]
><span data-ttu-id="b85aa-156">在9月2018中，选项卡[配置页面](~/tabs/how-to/create-tab-pages/configuration-page.md)的高度增加，而宽度保持不变。</span><span class="sxs-lookup"><span data-stu-id="b85aa-156">In September 2018, the height for the tab [configuration page](~/tabs/how-to/create-tab-pages/configuration-page.md) was increased while the width remained unchanged.</span></span> <span data-ttu-id="b85aa-157">如果您的应用程序是为较旧的大小设计的，则选项卡配置页将具有大量的垂直空白。</span><span class="sxs-lookup"><span data-stu-id="b85aa-157">If your app is designed for the older size your tab configuration page will have a great deal of vertical whitespace.</span></span> <span data-ttu-id="b85aa-158">从此更改中免除的旧版应用程序将需要在更新后与 Microsoft 联系，以适应新的维度。</span><span class="sxs-lookup"><span data-stu-id="b85aa-158">Legacy store apps exempted from this change will need to contact Microsoft after updating to accommodate the new dimensions.</span></span>

<span data-ttu-id="b85aa-159">选项卡配置页的尺寸：</span><span class="sxs-lookup"><span data-stu-id="b85aa-159">The dimensions of the tab configuration page:</span></span>

<img width="450px" title="配置选项卡的大小" src="~/assets/images/tabs/config-dialog-Contoso2.png" />

### <a name="guidelines-for-tab-configuration-page-format"></a><span data-ttu-id="b85aa-161">选项卡配置页面格式的准则</span><span class="sxs-lookup"><span data-stu-id="b85aa-161">Guidelines for tab configuration page format</span></span>

* <span data-ttu-id="b85aa-162">使固定高度图形元素上的选项卡配置页的内容区域的最小高度为基准。</span><span class="sxs-lookup"><span data-stu-id="b85aa-162">Base the minimum height of your content area of your tab configuration page on fixed-height graphic elements.</span></span>
* <span data-ttu-id="b85aa-163">使用`window.innerHeight`计算可用的垂直间距（配置页中的内容区域的高度）。</span><span class="sxs-lookup"><span data-stu-id="b85aa-163">Calculate available vertical space (the height of the content area in the configuration page) using `window.innerHeight`.</span></span> <span data-ttu-id="b85aa-164">这将返回配置页面所`<iframe>`驻留的大小，在将来的版本中可能会发生更改。</span><span class="sxs-lookup"><span data-stu-id="b85aa-164">This returns the size of the `<iframe>` in which your configuration page resides, which may change in future releases.</span></span> <span data-ttu-id="b85aa-165">通过使用此值，你的内容将自动调整为将来的更改。</span><span class="sxs-lookup"><span data-stu-id="b85aa-165">By using this value your content will adjust automatically to future changes.</span></span>
* <span data-ttu-id="b85aa-166">将垂直空间分配给可变高度元素减去固定高度元素所需的值。</span><span class="sxs-lookup"><span data-stu-id="b85aa-166">Allocate vertical space to the variable-height elements minus what's needed for the fixed-height elements.</span></span>
* <span data-ttu-id="b85aa-167">对于 "*登录*状态"，将内容垂直和水平居中。</span><span class="sxs-lookup"><span data-stu-id="b85aa-167">For the *login* state, vertically and horizontally center the content.</span></span>
* <span data-ttu-id="b85aa-168">如果需要背景图像，您需要一个新图像，调整大小以适合该区域（首选），或者您可以保留相同的图像并在其中进行选择：</span><span class="sxs-lookup"><span data-stu-id="b85aa-168">If you want a background image, you need either a new image, sized to fit the area (preferred), or you can keep the same image and choose between:</span></span>
  * <span data-ttu-id="b85aa-169">与左上角对齐。</span><span class="sxs-lookup"><span data-stu-id="b85aa-169">aligning to the upper left hand corner.</span></span>
  * <span data-ttu-id="b85aa-170">将图像缩放到合适大小。</span><span class="sxs-lookup"><span data-stu-id="b85aa-170">scaling the image to fit.</span></span>

<span data-ttu-id="b85aa-171">如果调整了适当的大小，您的选项卡配置页面应如下所示：</span><span class="sxs-lookup"><span data-stu-id="b85aa-171">When properly sized, your tab configuration page should look similar to this:</span></span>

<img width="450px" title=""新建配置" 选项卡" src="~/assets/images/tabs/config-dialog-Contoso.png" />

## <a name="best-practices"></a><span data-ttu-id="b85aa-173">最佳做法</span><span class="sxs-lookup"><span data-stu-id="b85aa-173">Best practices</span></span>

### <a name="always-include-a-default-state"></a><span data-ttu-id="b85aa-174">始终包含默认状态</span><span class="sxs-lookup"><span data-stu-id="b85aa-174">Always include a default state</span></span>

<span data-ttu-id="b85aa-175">如果您的选项卡是可配置的，则包括默认状态以使选项卡易于设置。</span><span class="sxs-lookup"><span data-stu-id="b85aa-175">Include a default state to make tabs easy to set up even if your tab is configurable.</span></span>

### <a name="deep-linking"></a><span data-ttu-id="b85aa-176">深度链接</span><span class="sxs-lookup"><span data-stu-id="b85aa-176">Deep linking</span></span>

<span data-ttu-id="b85aa-177">只要有可能，卡片和 bot 应在承载的选项卡中深入链接到丰富的数据。例如，卡片可能会显示错误数据的摘要，但单击它可以在选项卡中显示整个 bug。</span><span class="sxs-lookup"><span data-stu-id="b85aa-177">Whenever possible, cards and bots should deep link to richer data in a hosted tab. For example, a card may show a summary of bug data, but clicking it can shows the entire bug in a tab.</span></span>

### <a name="naming"></a><span data-ttu-id="b85aa-178">名称</span><span class="sxs-lookup"><span data-stu-id="b85aa-178">Naming</span></span>

<span data-ttu-id="b85aa-179">在很多情况下，您的应用程序的名称将产生很好的选项卡名称。</span><span class="sxs-lookup"><span data-stu-id="b85aa-179">In many cases, the name of your app will make a great tab name.</span></span> <span data-ttu-id="b85aa-180">此外，还应考虑根据它们提供的功能命名选项卡。</span><span class="sxs-lookup"><span data-stu-id="b85aa-180">But, also consider naming your tabs according to the functionality they provide.</span></span>

## <a name="notifications-for-tabs"></a><span data-ttu-id="b85aa-181">选项卡通知</span><span class="sxs-lookup"><span data-stu-id="b85aa-181">Notifications for tabs</span></span>

<span data-ttu-id="b85aa-182">对于选项卡内容更改，有两种通知模式：</span><span class="sxs-lookup"><span data-stu-id="b85aa-182">There are two modes of notification for tab content changes:</span></span>

> [!div class="checklist"]
>
> * <span data-ttu-id="b85aa-183">**使用应用程序 api 将更改通知用户**。</span><span class="sxs-lookup"><span data-stu-id="b85aa-183">**Use the app api to notify users of changes**.</span></span> <span data-ttu-id="b85aa-184">此消息将显示在用户的活动源和指向该选项卡的深层链接中。*请参阅*  [创建指向 Microsoft 团队中的内容和功能的深层链接](/concepts/build-and-test/deep-links?view=msteams-client-js-latest)</span><span class="sxs-lookup"><span data-stu-id="b85aa-184">This message will show up in the user’s activity feed and deep link to the tab. *See*  [Create deep links to content and features in Microsoft Teams](/concepts/build-and-test/deep-links?view=msteams-client-js-latest)</span></span>
> * <span data-ttu-id="b85aa-185">**使用 bot**。</span><span class="sxs-lookup"><span data-stu-id="b85aa-185">**Use a bot**.</span></span> <span data-ttu-id="b85aa-186">如果为 Tab 线程的目标，则此方法是首选方法。</span><span class="sxs-lookup"><span data-stu-id="b85aa-186">This method is preferred especially if the Tab thread is targeted.</span></span> <span data-ttu-id="b85aa-187">结果将是，选项卡的线程对话将作为最近活动的视图移动到视图中。</span><span class="sxs-lookup"><span data-stu-id="b85aa-187">The result will be that the tab’s threaded conversation will be moved into view as recently active.</span></span> <span data-ttu-id="b85aa-188">此方法还允许在通知的发送方式方面有一些复杂之处。</span><span class="sxs-lookup"><span data-stu-id="b85aa-188">This method also allows for some sophistication in how the notification is sent.</span></span>

  <span data-ttu-id="b85aa-189">将邮件发送到选项卡线程可将对所有用户的活动的感知提高到所有用户，而无需明确通知每个人。</span><span class="sxs-lookup"><span data-stu-id="b85aa-189">Sending a message to a tab thread increases the awareness of activity to all users without explicitly notifying everyone.</span></span> <span data-ttu-id="b85aa-190">这是不带噪音的感知。</span><span class="sxs-lookup"><span data-stu-id="b85aa-190">This is awareness without noise.</span></span> <span data-ttu-id="b85aa-191">此外，当您`@mention`将特定用户的通知放在其源中时，会将它们直接链接到 tab 线程。</span><span class="sxs-lookup"><span data-stu-id="b85aa-191">In addition, when you `@mention`  specific users the same notification will be placed in their feed, deep linking them to the tab thread directly.</span></span>
