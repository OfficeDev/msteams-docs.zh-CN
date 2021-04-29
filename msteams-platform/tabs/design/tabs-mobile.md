---
title: 移动设备上的选项卡
description: 介绍设计适用于移动设备的选项卡的指南。
ms.topic: conceptual
localization_priority: Normal
keywords: teams 设计指南参考框架个人应用移动应用选项卡
ms.openlocfilehash: cdcaddf5ba0fb18537e87daa4b459c7377225f76
ms.sourcegitcommit: d90c5dafea09e2893dea8da46ee49516bbaa04b0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2021
ms.locfileid: "52075694"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="64683-104">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="64683-104">Tabs on mobile</span></span>

<span data-ttu-id="64683-105">可以在 Teams 移动频道、聊天和个人应用中包括选项卡。</span><span class="sxs-lookup"><span data-stu-id="64683-105">You can include tabs in Teams mobile channels, chats, and personal apps.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="64683-106">访问个人选项卡</span><span class="sxs-lookup"><span data-stu-id="64683-106">Accessing personal tabs</span></span>

<span data-ttu-id="64683-107">你可以访问应用箱中的个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="64683-107">You can access personal tabs in the app drawer.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="显示 Teams 移动应用箱的图示。" border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="64683-109">访问频道选项卡</span><span class="sxs-lookup"><span data-stu-id="64683-109">Accessing channel tabs</span></span>

<span data-ttu-id="64683-110">可以通过选择频道或已添加这些选项卡的聊天中的"更多"按钮来访问频道和组选项卡。</span><span class="sxs-lookup"><span data-stu-id="64683-110">You can access channel and group tabs by selecting the **More** button in the channel or chat in which they've been added.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="显示 Teams 移动选项卡的图示。" border="false":::

## <a name="design-considerations"></a><span data-ttu-id="64683-112">设计注意事项</span><span class="sxs-lookup"><span data-stu-id="64683-112">Design considerations</span></span>

<span data-ttu-id="64683-113">我们的移动平台允许应用成为沉浸式体验，其中应用内容接管了主 Teams 导航之外的所有屏幕。</span><span class="sxs-lookup"><span data-stu-id="64683-113">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="64683-114">若要创建适合 Teams 的沉浸式体验，请遵循以下指南。</span><span class="sxs-lookup"><span data-stu-id="64683-114">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="64683-115">响应式设计</span><span class="sxs-lookup"><span data-stu-id="64683-115">Responsive design</span></span>

<span data-ttu-id="64683-116">由于你的选项卡可以在具有各种屏幕大小的设备上打开，它需要遵循 [响应式设计](https://www.w3schools.com/html/html_responsive.asp) 原则。</span><span class="sxs-lookup"><span data-stu-id="64683-116">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="64683-117">所有关键构造都应可在移动设备上访问，并且不应使视图失真。</span><span class="sxs-lookup"><span data-stu-id="64683-117">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="64683-118">确保在移动设备上加载选项卡时，所有按钮和链接都可以通过基于手指的导航轻松访问。</span><span class="sxs-lookup"><span data-stu-id="64683-118">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="64683-119">布局</span><span class="sxs-lookup"><span data-stu-id="64683-119">Layouts</span></span>

<span data-ttu-id="64683-120">为选项卡选择正确的布局非常重要。</span><span class="sxs-lookup"><span data-stu-id="64683-120">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="64683-121">你应该考虑你呈现的信息类型，并选择一个布局来组织这些信息以方便使用。</span><span class="sxs-lookup"><span data-stu-id="64683-121">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="64683-122">下面概述了一些潜在的选项。</span><span class="sxs-lookup"><span data-stu-id="64683-122">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="64683-123">单画布</span><span class="sxs-lookup"><span data-stu-id="64683-123">Single canvas</span></span>

<span data-ttu-id="64683-124">这是完成工作的一个大区域。</span><span class="sxs-lookup"><span data-stu-id="64683-124">This is one large area where work gets done.</span></span> <span data-ttu-id="64683-125">Teams Wiki 应用遵循此模式。</span><span class="sxs-lookup"><span data-stu-id="64683-125">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="64683-126">如果你的应用不将内容分为较小的组件，这非常适合。</span><span class="sxs-lookup"><span data-stu-id="64683-126">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="显示 Teams 移动单画布选项卡的图示。" border="false":::

#### <a name="list"></a><span data-ttu-id="64683-128">列表</span><span class="sxs-lookup"><span data-stu-id="64683-128">List</span></span>

<span data-ttu-id="64683-129">列表对于对大量的数据进行排序和筛选都十分重要，并且非常能将最重要的内容放在最上面。</span><span class="sxs-lookup"><span data-stu-id="64683-129">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="64683-130">使用可排序列非常有用。</span><span class="sxs-lookup"><span data-stu-id="64683-130">It is helpful to use sortable columns.</span></span> <span data-ttu-id="64683-131">可以将操作添加到省略号菜单下的每个列表项。</span><span class="sxs-lookup"><span data-stu-id="64683-131">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="显示 Teams 移动列表选项卡的图示。" border="false":::

#### <a name="grid"></a><span data-ttu-id="64683-133">网格</span><span class="sxs-lookup"><span data-stu-id="64683-133">Grid</span></span>

<span data-ttu-id="64683-134">网格对于显示高度可视的元素非常有用。</span><span class="sxs-lookup"><span data-stu-id="64683-134">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="64683-135">这有助于在顶部包含筛选器或搜索控件。</span><span class="sxs-lookup"><span data-stu-id="64683-135">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="显示具有网格布局的 Teams 移动选项卡的图示。" border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="64683-137">在移动设备上使用机器人的选项卡</span><span class="sxs-lookup"><span data-stu-id="64683-137">Tabs with bots on mobile</span></span>

<span data-ttu-id="64683-138">以下示例是包含选项卡和自动程序的个人应用。</span><span class="sxs-lookup"><span data-stu-id="64683-138">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="插图显示具有选项卡和自动程序的移动 Teams 应用。" border="false":::

## <a name="ui-components"></a><span data-ttu-id="64683-140">UI 组件</span><span class="sxs-lookup"><span data-stu-id="64683-140">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="64683-141">调色板</span><span class="sxs-lookup"><span data-stu-id="64683-141">Color palettes</span></span>

<span data-ttu-id="64683-142">将已批准的中性调色板用于背景、通知、文本和按钮将有助于你的应用在 Teams 中感觉更加自在。</span><span class="sxs-lookup"><span data-stu-id="64683-142">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="64683-143">由于 Teams 移动版具有 (浅色和深色) 主题，因此建议确保你的应用在两者中都外观良好。</span><span class="sxs-lookup"><span data-stu-id="64683-143">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="64683-144">浅色</span><span class="sxs-lookup"><span data-stu-id="64683-144">Light color</span></span>

![浅色调色板](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="64683-146">深色</span><span class="sxs-lookup"><span data-stu-id="64683-146">Dark color</span></span>

![深色调色板](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="64683-148">按钮和控件</span><span class="sxs-lookup"><span data-stu-id="64683-148">Buttons and controls</span></span>

<span data-ttu-id="64683-149">设置按钮样式的方式有助于传达它们触发的操作类型。</span><span class="sxs-lookup"><span data-stu-id="64683-149">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="64683-150">我们保留各种按钮，这些按钮经过格式化以显示不同级别的强调。</span><span class="sxs-lookup"><span data-stu-id="64683-150">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="64683-151">按钮可以有文本、图标或文本和图标的组合。</span><span class="sxs-lookup"><span data-stu-id="64683-151">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="64683-152">为了传达层次结构中的不同级别，我们设计了每个类别中的主按钮和辅助按钮。</span><span class="sxs-lookup"><span data-stu-id="64683-152">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="64683-153">按钮</span><span class="sxs-lookup"><span data-stu-id="64683-153">Buttons</span></span>

<span data-ttu-id="64683-154">主按钮和辅助按钮。</span><span class="sxs-lookup"><span data-stu-id="64683-154">Primary and secondary buttons.</span></span>

![按钮图像](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="64683-156">选择控件</span><span class="sxs-lookup"><span data-stu-id="64683-156">Selection controls</span></span>

<span data-ttu-id="64683-157">单选按钮、复选框和切换。</span><span class="sxs-lookup"><span data-stu-id="64683-157">Radio buttons, checkboxes, and toggles.</span></span>

![选择控件](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="64683-159">小红包和装饰</span><span class="sxs-lookup"><span data-stu-id="64683-159">Chiclets and pills</span></span>

![一些子项目](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="64683-161">版式</span><span class="sxs-lookup"><span data-stu-id="64683-161">Typography</span></span>

<span data-ttu-id="64683-162">版式应清晰且有目的。</span><span class="sxs-lookup"><span data-stu-id="64683-162">Typography should be clear and purposeful.</span></span> <span data-ttu-id="64683-163">强调重要信息并避免使用多个字体和大小以减少混淆。</span><span class="sxs-lookup"><span data-stu-id="64683-163">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="64683-164">我们建议使用句大小写，并避免使用全部大写字母进行本地化和易读。</span><span class="sxs-lookup"><span data-stu-id="64683-164">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![移动版式](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="64683-166">字段和飞出</span><span class="sxs-lookup"><span data-stu-id="64683-166">Fields and flyouts</span></span>

<span data-ttu-id="64683-167">字段是用户可以输入文本的区域。</span><span class="sxs-lookup"><span data-stu-id="64683-167">Fields are areas where users can input text.</span></span> <span data-ttu-id="64683-168">弹出框比对话框更轻量，并且从顶部窗格中显示。</span><span class="sxs-lookup"><span data-stu-id="64683-168">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="64683-169">列出控件</span><span class="sxs-lookup"><span data-stu-id="64683-169">List controls</span></span>

![移动列表控件](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="64683-171">字段控件</span><span class="sxs-lookup"><span data-stu-id="64683-171">Field controls</span></span>

![移动字段控件](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="64683-173">开发人员注意事项</span><span class="sxs-lookup"><span data-stu-id="64683-173">Developer considerations</span></span>

<span data-ttu-id="64683-174">生成包含选项卡的应用时，需要考虑 (和测试) 在 Android 和 iOS Microsoft Teams 客户端上如何运行。</span><span class="sxs-lookup"><span data-stu-id="64683-174">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="64683-175">以下各节概述了需要考虑的一些关键方案。</span><span class="sxs-lookup"><span data-stu-id="64683-175">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="authentication"></a><span data-ttu-id="64683-176">身份验证</span><span class="sxs-lookup"><span data-stu-id="64683-176">Authentication</span></span>

<span data-ttu-id="64683-177">若要在移动客户端上进行身份验证，必须将 Teams JavaScript SDK 至少升级到版本 1.4.1。</span><span class="sxs-lookup"><span data-stu-id="64683-177">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="64683-178">低带宽和间歇性连接</span><span class="sxs-lookup"><span data-stu-id="64683-178">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="64683-179">移动客户端经常需要在低带宽和间歇性连接下运行。</span><span class="sxs-lookup"><span data-stu-id="64683-179">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="64683-180">应用应该通过向用户提供上下文消息来适当地处理任何超时。</span><span class="sxs-lookup"><span data-stu-id="64683-180">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="64683-181">您还应使用用户进度指示器，以针对任何长时间运行的过程向用户提供反馈。</span><span class="sxs-lookup"><span data-stu-id="64683-181">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="64683-182">只有在根据审批团队的输入将应用程序添加到允许列表后，才能在移动设备上启用选项卡。</span><span class="sxs-lookup"><span data-stu-id="64683-182">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="64683-183">要检查移动响应，请联系 teamsubm@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="64683-183">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="64683-184">在移动客户端上测试</span><span class="sxs-lookup"><span data-stu-id="64683-184">Testing on mobile clients</span></span>

<span data-ttu-id="64683-185">需要验证选项卡在各种大小和质量的移动设备上是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="64683-185">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="64683-186">对于 Android 设备，可以在选项卡运行时使用 [DevTools](~/tabs/how-to/developer-tools.md) 调试选项卡。</span><span class="sxs-lookup"><span data-stu-id="64683-186">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="64683-187">建议在高性能和低性能设备以及平板电脑上进行测试。</span><span class="sxs-lookup"><span data-stu-id="64683-187">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="distribution"></a><span data-ttu-id="64683-188">分发</span><span class="sxs-lookup"><span data-stu-id="64683-188">Distribution</span></span>

<span data-ttu-id="64683-189">必须批准 Teams 应用商店中列出的应用进行移动使用，以在 Teams 移动客户端中正常运行。</span><span class="sxs-lookup"><span data-stu-id="64683-189">Apps listed on the Teams store must be approved for mobile use to function properly in the Teams mobile client.</span></span> <span data-ttu-id="64683-190">选项卡的行为方式取决于你的应用是否得到批准。</span><span class="sxs-lookup"><span data-stu-id="64683-190">How tabs behave depends on whether your app is approved.</span></span>

#### <a name="channel-and-group-tab-behavior"></a><span data-ttu-id="64683-191">通道和组选项卡行为</span><span class="sxs-lookup"><span data-stu-id="64683-191">Channel and group tab behavior</span></span>

* <span data-ttu-id="64683-192">**批准后的行为**：使用应用配置在 Teams 移动客户端 `contentUrl` 中打开。</span><span class="sxs-lookup"><span data-stu-id="64683-192">**Behavior when approved**: Opens in the Teams mobile client using your app's `contentUrl` configuration.</span></span>
* <span data-ttu-id="64683-193">**未批准时的行为**：使用应用配置选项在设备的默认浏览器中打开 (此配置还必须包含在源代码的功能 `websiteUrl` `setSettings()`) 。</span><span class="sxs-lookup"><span data-stu-id="64683-193">**Behavior when not approved**: Opens in the device’s default browser using your app's `websiteUrl` configuration (which also must be included in your source code's `setSettings()` function).</span></span> <span data-ttu-id="64683-194">但是，用户仍可在 Teams 移动客户端中加载该选项卡，方法为选择应用旁边的"更多"并选择"打开"，这将触发应用的 `contentUrl` 配置。</span><span class="sxs-lookup"><span data-stu-id="64683-194">However, users can still load the tab in the Teams mobile client by selecting **More** next to the app and choosing **Open**, which triggers your app’s `contentUrl` configuration.</span></span>

#### <a name="personal-app-behavior"></a><span data-ttu-id="64683-195">个人应用行为</span><span class="sxs-lookup"><span data-stu-id="64683-195">Personal app behavior</span></span>

* <span data-ttu-id="64683-196">**批准后的行为**：个人应用的每个选项卡使用各自的配置显示在 Teams 移动 `contentUrl` 客户端中。</span><span class="sxs-lookup"><span data-stu-id="64683-196">**Behavior when approved**: Each tab in the personal app displays in the Teams mobile client using their respective `contentUrl` configuration.</span></span>
* <span data-ttu-id="64683-197">**未批准时的行为**：个人应用在 Teams 移动客户端中不可用。</span><span class="sxs-lookup"><span data-stu-id="64683-197">**Behavior when not approved**: The personal app is unavailable in the Teams mobile client.</span></span>

#### <a name="non-teams-store-app-behavior"></a><span data-ttu-id="64683-198">非 Teams 应用商店应用行为</span><span class="sxs-lookup"><span data-stu-id="64683-198">Non-Teams store app behavior</span></span>

<span data-ttu-id="64683-199">如果要将应用旁加载或发布到组织的应用程序目录，选项卡行为将与 Microsoft 批准的适用于移动的 Teams 应用商店应用相同。</span><span class="sxs-lookup"><span data-stu-id="64683-199">If you're sideloading your app or publishing to an org's app catalog, tab behavior will be the same as Teams store apps approved by Microsoft for mobile.</span></span>
