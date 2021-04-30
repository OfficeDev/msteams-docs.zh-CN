---
title: 移动设备上的选项卡
description: 介绍设计适用于移动设备的选项卡的指南。
ms.topic: conceptual
localization_priority: Normal
keywords: teams 设计指南参考框架个人应用移动应用选项卡
ms.openlocfilehash: b9f09ce2603ee2617b8b93ba2132b900c61f2c31
ms.sourcegitcommit: 1256639fa424e3833b44207ce847a245824d48e6
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/29/2021
ms.locfileid: "52088757"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="e920a-104">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="e920a-104">Tabs on mobile</span></span>

<span data-ttu-id="e920a-105">你可以将选项卡包括在Teams、聊天和个人应用中。</span><span class="sxs-lookup"><span data-stu-id="e920a-105">You can include tabs in Teams mobile channels, chats, and personal apps.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="e920a-106">访问个人选项卡</span><span class="sxs-lookup"><span data-stu-id="e920a-106">Accessing personal tabs</span></span>

<span data-ttu-id="e920a-107">你可以访问应用箱中的个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="e920a-107">You can access personal tabs in the app drawer.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="插图显示Teams移动应用箱。" border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="e920a-109">访问频道选项卡</span><span class="sxs-lookup"><span data-stu-id="e920a-109">Accessing channel tabs</span></span>

<span data-ttu-id="e920a-110">可以通过选择频道或已添加这些选项卡的聊天中的"更多"按钮来访问频道和组选项卡。</span><span class="sxs-lookup"><span data-stu-id="e920a-110">You can access channel and group tabs by selecting the **More** button in the channel or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="显示移动Teams的图示。" border="false":::

## <a name="design-considerations"></a><span data-ttu-id="e920a-112">设计注意事项</span><span class="sxs-lookup"><span data-stu-id="e920a-112">Design considerations</span></span>

<span data-ttu-id="e920a-113">我们的移动平台允许应用成为沉浸式体验，其中应用内容从主导航导航Teams屏幕。</span><span class="sxs-lookup"><span data-stu-id="e920a-113">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="e920a-114">若要创建适合你的体验的沉浸Teams，请遵循以下指南。</span><span class="sxs-lookup"><span data-stu-id="e920a-114">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="e920a-115">响应式设计</span><span class="sxs-lookup"><span data-stu-id="e920a-115">Responsive design</span></span>

<span data-ttu-id="e920a-116">由于你的选项卡可以在具有各种屏幕大小的设备上打开，它需要遵循 [响应式设计](https://www.w3schools.com/html/html_responsive.asp) 原则。</span><span class="sxs-lookup"><span data-stu-id="e920a-116">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="e920a-117">所有关键构造都应可在移动设备上访问，并且不应使视图失真。</span><span class="sxs-lookup"><span data-stu-id="e920a-117">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="e920a-118">确保在移动设备上加载选项卡时，所有按钮和链接都可以通过基于手指的导航轻松访问。</span><span class="sxs-lookup"><span data-stu-id="e920a-118">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="e920a-119">布局</span><span class="sxs-lookup"><span data-stu-id="e920a-119">Layouts</span></span>

<span data-ttu-id="e920a-120">为选项卡选择正确的布局非常重要。</span><span class="sxs-lookup"><span data-stu-id="e920a-120">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="e920a-121">你应该考虑你呈现的信息类型，并选择一个布局来组织这些信息以方便使用。</span><span class="sxs-lookup"><span data-stu-id="e920a-121">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="e920a-122">下面概述了一些潜在的选项。</span><span class="sxs-lookup"><span data-stu-id="e920a-122">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="e920a-123">单画布</span><span class="sxs-lookup"><span data-stu-id="e920a-123">Single canvas</span></span>

<span data-ttu-id="e920a-124">这是完成工作的一个大区域。</span><span class="sxs-lookup"><span data-stu-id="e920a-124">This is one large area where work gets done.</span></span> <span data-ttu-id="e920a-125">Wiki Teams应用遵循此模式。</span><span class="sxs-lookup"><span data-stu-id="e920a-125">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="e920a-126">如果你的应用不将内容分为较小的组件，这非常适合。</span><span class="sxs-lookup"><span data-stu-id="e920a-126">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="显示移动Teams画布选项卡的图示。" border="false":::

#### <a name="list"></a><span data-ttu-id="e920a-128">列表</span><span class="sxs-lookup"><span data-stu-id="e920a-128">List</span></span>

<span data-ttu-id="e920a-129">列表对于对大量的数据进行排序和筛选都十分重要，并且非常能将最重要的内容放在最上面。</span><span class="sxs-lookup"><span data-stu-id="e920a-129">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="e920a-130">使用可排序列非常有用。</span><span class="sxs-lookup"><span data-stu-id="e920a-130">It is helpful to use sortable columns.</span></span> <span data-ttu-id="e920a-131">可以将操作添加到省略号菜单下的每个列表项。</span><span class="sxs-lookup"><span data-stu-id="e920a-131">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="显示&quot;移动Teams选项卡的图示。" border="false":::

#### <a name="grid"></a><span data-ttu-id="e920a-133">网格</span><span class="sxs-lookup"><span data-stu-id="e920a-133">Grid</span></span>

<span data-ttu-id="e920a-134">网格对于显示高度可视的元素非常有用。</span><span class="sxs-lookup"><span data-stu-id="e920a-134">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="e920a-135">这有助于在顶部包含筛选器或搜索控件。</span><span class="sxs-lookup"><span data-stu-id="e920a-135">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="插图显示一Teams网格布局的移动设备选项卡。" border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="e920a-137">在移动设备上使用机器人的选项卡</span><span class="sxs-lookup"><span data-stu-id="e920a-137">Tabs with bots on mobile</span></span>

<span data-ttu-id="e920a-138">以下示例是包含选项卡和自动程序的个人应用。</span><span class="sxs-lookup"><span data-stu-id="e920a-138">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="插图显示移动设备Teams选项卡和自动程序的应用。" border="false":::

## <a name="ui-components"></a><span data-ttu-id="e920a-140">UI 组件</span><span class="sxs-lookup"><span data-stu-id="e920a-140">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="e920a-141">调色板</span><span class="sxs-lookup"><span data-stu-id="e920a-141">Color palettes</span></span>

<span data-ttu-id="e920a-142">将已批准的中性调色板用于背景、通知、文本和按钮将有助于你的应用在Teams。</span><span class="sxs-lookup"><span data-stu-id="e920a-142">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="e920a-143">由于Teams手机具有 (浅色和深色) 主题，因此，建议确保你的应用在两者中都外观良好。</span><span class="sxs-lookup"><span data-stu-id="e920a-143">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="e920a-144">浅色</span><span class="sxs-lookup"><span data-stu-id="e920a-144">Light color</span></span>

![浅色调色板](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="e920a-146">深色</span><span class="sxs-lookup"><span data-stu-id="e920a-146">Dark color</span></span>

![深色调色板](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="e920a-148">按钮和控件</span><span class="sxs-lookup"><span data-stu-id="e920a-148">Buttons and controls</span></span>

<span data-ttu-id="e920a-149">设置按钮样式的方式有助于传达它们触发的操作类型。</span><span class="sxs-lookup"><span data-stu-id="e920a-149">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="e920a-150">我们保留各种按钮，这些按钮经过格式化以显示不同级别的强调。</span><span class="sxs-lookup"><span data-stu-id="e920a-150">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="e920a-151">按钮可以有文本、图标或文本和图标的组合。</span><span class="sxs-lookup"><span data-stu-id="e920a-151">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="e920a-152">为了传达层次结构中的不同级别，我们设计了每个类别中的主按钮和辅助按钮。</span><span class="sxs-lookup"><span data-stu-id="e920a-152">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="e920a-153">按钮</span><span class="sxs-lookup"><span data-stu-id="e920a-153">Buttons</span></span>

<span data-ttu-id="e920a-154">主按钮和辅助按钮。</span><span class="sxs-lookup"><span data-stu-id="e920a-154">Primary and secondary buttons.</span></span>

![按钮图像](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="e920a-156">选择控件</span><span class="sxs-lookup"><span data-stu-id="e920a-156">Selection controls</span></span>

<span data-ttu-id="e920a-157">单选按钮、复选框和切换。</span><span class="sxs-lookup"><span data-stu-id="e920a-157">Radio buttons, checkboxes, and toggles.</span></span>

![选择控件](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="e920a-159">小红包和装饰</span><span class="sxs-lookup"><span data-stu-id="e920a-159">Chiclets and pills</span></span>

![一些子项目](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="e920a-161">版式</span><span class="sxs-lookup"><span data-stu-id="e920a-161">Typography</span></span>

<span data-ttu-id="e920a-162">版式应清晰且有目的。</span><span class="sxs-lookup"><span data-stu-id="e920a-162">Typography should be clear and purposeful.</span></span> <span data-ttu-id="e920a-163">强调重要信息并避免使用多个字体和大小以减少混淆。</span><span class="sxs-lookup"><span data-stu-id="e920a-163">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="e920a-164">我们建议使用句大小写，并避免使用全部大写字母进行本地化和易读。</span><span class="sxs-lookup"><span data-stu-id="e920a-164">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![移动版式](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="e920a-166">字段和飞出</span><span class="sxs-lookup"><span data-stu-id="e920a-166">Fields and flyouts</span></span>

<span data-ttu-id="e920a-167">字段是用户可以输入文本的区域。</span><span class="sxs-lookup"><span data-stu-id="e920a-167">Fields are areas where users can input text.</span></span> <span data-ttu-id="e920a-168">弹出框比对话框更轻量，并且从顶部窗格中显示。</span><span class="sxs-lookup"><span data-stu-id="e920a-168">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="e920a-169">列出控件</span><span class="sxs-lookup"><span data-stu-id="e920a-169">List controls</span></span>

![移动列表控件](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="e920a-171">字段控件</span><span class="sxs-lookup"><span data-stu-id="e920a-171">Field controls</span></span>

![移动字段控件](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="e920a-173">开发人员注意事项</span><span class="sxs-lookup"><span data-stu-id="e920a-173">Developer considerations</span></span>

<span data-ttu-id="e920a-174">生成包含选项卡的应用时，需要考虑 (和测试) 在 Android 和 iOS Microsoft Teams上如何工作。</span><span class="sxs-lookup"><span data-stu-id="e920a-174">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="e920a-175">以下各节概述了需要考虑的一些关键方案。</span><span class="sxs-lookup"><span data-stu-id="e920a-175">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="authentication"></a><span data-ttu-id="e920a-176">身份验证</span><span class="sxs-lookup"><span data-stu-id="e920a-176">Authentication</span></span>

<span data-ttu-id="e920a-177">若要在移动客户端上进行身份验证，必须将 JavaScript SDK Teams至少升级到版本 1.4.1。</span><span class="sxs-lookup"><span data-stu-id="e920a-177">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="e920a-178">低带宽和间歇性连接</span><span class="sxs-lookup"><span data-stu-id="e920a-178">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="e920a-179">移动客户端经常需要在低带宽和间歇性连接下运行。</span><span class="sxs-lookup"><span data-stu-id="e920a-179">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="e920a-180">应用应该通过向用户提供上下文消息来适当地处理任何超时。</span><span class="sxs-lookup"><span data-stu-id="e920a-180">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="e920a-181">您还应使用用户进度指示器，以针对任何长时间运行的过程向用户提供反馈。</span><span class="sxs-lookup"><span data-stu-id="e920a-181">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="e920a-182">只有在根据审批团队的输入将应用程序添加到允许列表后，才能在移动设备上启用选项卡。</span><span class="sxs-lookup"><span data-stu-id="e920a-182">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="e920a-183">要检查移动响应，请联系 teamsubm@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="e920a-183">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="e920a-184">在移动客户端上测试</span><span class="sxs-lookup"><span data-stu-id="e920a-184">Testing on mobile clients</span></span>

<span data-ttu-id="e920a-185">需要验证选项卡在各种大小和质量的移动设备上是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="e920a-185">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="e920a-186">对于 Android 设备，可以在选项卡运行时使用 [DevTools](~/tabs/how-to/developer-tools.md) 调试选项卡。</span><span class="sxs-lookup"><span data-stu-id="e920a-186">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="e920a-187">建议在高性能和低性能设备（包括平板电脑）上进行测试。</span><span class="sxs-lookup"><span data-stu-id="e920a-187">We recommend that you test on both high- and low-performance devices, including a tablet.</span></span>

### <a name="distribution"></a><span data-ttu-id="e920a-188">分发</span><span class="sxs-lookup"><span data-stu-id="e920a-188">Distribution</span></span>

<span data-ttu-id="e920a-189">应用商店中列出的Teams必须经过批准，供移动使用，以在移动Teams正常运行。</span><span class="sxs-lookup"><span data-stu-id="e920a-189">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="e920a-190">选项卡可用性和行为取决于你的应用是否已获得批准。</span><span class="sxs-lookup"><span data-stu-id="e920a-190">Tab availability and behavior depends on whether your app is approved.</span></span>

#### <a name="apps-on-teams-store-approved-for-mobile"></a><span data-ttu-id="e920a-191">经批准Teams移动的应用商店上的应用</span><span class="sxs-lookup"><span data-stu-id="e920a-191">Apps on Teams store approved for mobile</span></span>

<span data-ttu-id="e920a-192">下表介绍了当应用在应用商店中列出并批准Teams时选项卡的可用性和行为。</span><span class="sxs-lookup"><span data-stu-id="e920a-192">The following table describes tab availability and behavior when the app is listed on the Teams store and approved for mobile use.</span></span>

|<span data-ttu-id="e920a-193">功能</span><span class="sxs-lookup"><span data-stu-id="e920a-193">Capability</span></span>   |<span data-ttu-id="e920a-194">移动可用性？</span><span class="sxs-lookup"><span data-stu-id="e920a-194">Mobile availability?</span></span>   |<span data-ttu-id="e920a-195">移动行为</span><span class="sxs-lookup"><span data-stu-id="e920a-195">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="e920a-196">频道</span><span class="sxs-lookup"><span data-stu-id="e920a-196">Channel</span></span> <br /> <span data-ttu-id="e920a-197">和组选项卡</span><span class="sxs-lookup"><span data-stu-id="e920a-197">and group tab</span></span>|<span data-ttu-id="e920a-198">是</span><span class="sxs-lookup"><span data-stu-id="e920a-198">Yes</span></span>|<span data-ttu-id="e920a-199">选项卡使用Teams在移动客户端中 `contentUrl` 打开。</span><span class="sxs-lookup"><span data-stu-id="e920a-199">Tab opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>|
|<span data-ttu-id="e920a-200">个人应用</span><span class="sxs-lookup"><span data-stu-id="e920a-200">Personal app</span></span>|<span data-ttu-id="e920a-201">是</span><span class="sxs-lookup"><span data-stu-id="e920a-201">Yes</span></span>|<span data-ttu-id="e920a-202">"个人应用"选项卡中的每个选项卡使用各自的Teams在移动客户端中 `contentUrl` 打开。</span><span class="sxs-lookup"><span data-stu-id="e920a-202">Each tab in the personal app tab opens in the Teams mobile client using its respective `contentUrl` configuration.</span></span>|

#### <a name="apps-on-teams-store-not-approved-for-mobile"></a><span data-ttu-id="e920a-203">未批准Teams移动的应用商店上的应用</span><span class="sxs-lookup"><span data-stu-id="e920a-203">Apps on Teams store not approved for mobile</span></span>

<span data-ttu-id="e920a-204">下表介绍了当应用在应用商店中列出但Teams批准的移动用途时选项卡可用性和行为。</span><span class="sxs-lookup"><span data-stu-id="e920a-204">The following table describes tab availability and behavior when the app is listed on the Teams store but not approved for mobile use.</span></span>

|<span data-ttu-id="e920a-205">功能</span><span class="sxs-lookup"><span data-stu-id="e920a-205">Capability</span></span>   |<span data-ttu-id="e920a-206">移动可用性？</span><span class="sxs-lookup"><span data-stu-id="e920a-206">Mobile availability?</span></span>|<span data-ttu-id="e920a-207">移动行为</span><span class="sxs-lookup"><span data-stu-id="e920a-207">Mobile behavior</span></span>|
|----------|-----------|------------|
|<span data-ttu-id="e920a-208">"频道和组"选项卡</span><span class="sxs-lookup"><span data-stu-id="e920a-208">Channel and group tab</span></span>|<span data-ttu-id="e920a-209">是</span><span class="sxs-lookup"><span data-stu-id="e920a-209">Yes</span></span>|<span data-ttu-id="e920a-210">选项卡将在设备的默认浏览器中打开，而不是使用应用的配置 (而 Teams 移动客户端也必须包含在源代码的函数 `websiteUrl` `setSettings()` [](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions)) 。</span><span class="sxs-lookup"><span data-stu-id="e920a-210">Tab opens in the device's default browser instead of the Teams mobile client using your app's `websiteUrl` configuration (which also must be included in your source code's `setSettings()` [function](https://docs.microsoft.com/javascript/api/@microsoft/teams-js/settings?view=msteams-client-js-latest#functions)).</span></span> <span data-ttu-id="e920a-211">但是，用户仍可在移动客户端Teams选项卡，方法为选择应用旁边的"更多"并选择"打开"，这将触发应用的 `contentUrl` 配置。</span><span class="sxs-lookup"><span data-stu-id="e920a-211">However, users can still view the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>|
|<span data-ttu-id="e920a-212">个人应用</span><span class="sxs-lookup"><span data-stu-id="e920a-212">Personal app</span></span>|<span data-ttu-id="e920a-213">不支持</span><span class="sxs-lookup"><span data-stu-id="e920a-213">No</span></span>|<span data-ttu-id="e920a-214">不适用</span><span class="sxs-lookup"><span data-stu-id="e920a-214">Not applicable</span></span>|

#### <a name="apps-not-on-teams-store"></a><span data-ttu-id="e920a-215">不在应用商店Teams应用</span><span class="sxs-lookup"><span data-stu-id="e920a-215">Apps not on Teams store</span></span>

<span data-ttu-id="e920a-216">如果要将应用旁加载或发布到组织的应用程序目录，选项卡行为将Teams Microsoft 批准的移动应用商店应用的行为相同。</span><span class="sxs-lookup"><span data-stu-id="e920a-216">If you're sideloading your app or publishing to an org's app catalog, tab behavior will be the same as Teams store apps approved by Microsoft for mobile.</span></span>
