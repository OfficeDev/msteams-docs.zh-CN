---
title: 移动设备上的选项卡
description: 介绍设计适用于移动设备的选项卡的指南。
ms.topic: conceptual
keywords: teams 设计指南参考框架个人应用移动选项卡
ms.openlocfilehash: 70ff46e446b146b134f34830e8867133cbeeca14
ms.sourcegitcommit: f74b74d5bed1df193e59f46121ada443fb57277b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/03/2021
ms.locfileid: "50093286"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="a8a97-104">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="a8a97-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="a8a97-105">如果你选择让频道/组选项卡显示在 Teams 移动客户端上，则配置必须具有属性值， (`setSettings()` `websiteUrl` 请参阅下面的) 。</span><span class="sxs-lookup"><span data-stu-id="a8a97-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="a8a97-106">自定义选项卡可以是包含静态选项卡和/或一对一自动程序 (应用的频道、群聊或个人应用的一) 。</span><span class="sxs-lookup"><span data-stu-id="a8a97-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="a8a97-107">个人应用在应用箱中的移动客户端上可用。</span><span class="sxs-lookup"><span data-stu-id="a8a97-107">Personal apps are available on mobile clients in the app drawer.</span></span> <span data-ttu-id="a8a97-108">该应用只能从桌面或 Web 客户端安装，最多可能需要 24 小时才能显示在移动客户端上。</span><span class="sxs-lookup"><span data-stu-id="a8a97-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="a8a97-109">还可在移动设备上使用频道选项卡。</span><span class="sxs-lookup"><span data-stu-id="a8a97-109">Channel tabs are also available on mobile.</span></span> <span data-ttu-id="a8a97-110">默认行为当前用于在浏览器窗口中启动 `websiteUrl` 选项卡。</span><span class="sxs-lookup"><span data-stu-id="a8a97-110">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="a8a97-111">但是，可以通过单击选项卡旁边的溢出菜单并选择"打开"（将使用你加载 Teams 移动客户端中的选项卡）在移动客户端上 `...`  `contentUrl` 加载它们。</span><span class="sxs-lookup"><span data-stu-id="a8a97-111">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="a8a97-112">访问个人选项卡</span><span class="sxs-lookup"><span data-stu-id="a8a97-112">Accessing personal tabs</span></span>

<span data-ttu-id="a8a97-113">下图显示了如何在移动设备上访问个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="a8a97-113">The following illustration shows how you access a personal tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="显示 Teams 移动应用箱的图示。" border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="a8a97-115">访问频道选项卡</span><span class="sxs-lookup"><span data-stu-id="a8a97-115">Accessing channel tabs</span></span>

<span data-ttu-id="a8a97-116">下图显示了如何在移动设备上访问频道选项卡。</span><span class="sxs-lookup"><span data-stu-id="a8a97-116">The following illustration shows how you access a channel tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="显示 Teams 移动选项卡的图示。" border="false":::

## <a name="design-considerations"></a><span data-ttu-id="a8a97-118">设计注意事项</span><span class="sxs-lookup"><span data-stu-id="a8a97-118">Design considerations</span></span>

<span data-ttu-id="a8a97-119">我们的移动平台允许应用成为一种沉浸式体验，应用内容将接管 Teams 主导航之外的所有屏幕。</span><span class="sxs-lookup"><span data-stu-id="a8a97-119">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="a8a97-120">若要创建适合 Teams 的沉浸式体验，请遵循以下指南。</span><span class="sxs-lookup"><span data-stu-id="a8a97-120">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="a8a97-121">响应式设计</span><span class="sxs-lookup"><span data-stu-id="a8a97-121">Responsive design</span></span>

<span data-ttu-id="a8a97-122">由于你的选项卡可以在具有各种屏幕大小的设备上打开，它需要遵循响应式 [设计](https://www.w3schools.com/html/html_responsive.asp) 原则。</span><span class="sxs-lookup"><span data-stu-id="a8a97-122">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="a8a97-123">所有关键构造都应可以在移动设备上访问，并且不应使视图失真。</span><span class="sxs-lookup"><span data-stu-id="a8a97-123">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="a8a97-124">确保在移动设备上加载选项卡时，所有按钮和链接都可以通过手指导航轻松访问。</span><span class="sxs-lookup"><span data-stu-id="a8a97-124">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="a8a97-125">布局</span><span class="sxs-lookup"><span data-stu-id="a8a97-125">Layouts</span></span>

<span data-ttu-id="a8a97-126">为选项卡选择正确的布局非常重要。</span><span class="sxs-lookup"><span data-stu-id="a8a97-126">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="a8a97-127">应考虑要呈现的信息类型，并选择一种布局来组织该信息，方便使用。</span><span class="sxs-lookup"><span data-stu-id="a8a97-127">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="a8a97-128">下面概述了一些潜在的选项。</span><span class="sxs-lookup"><span data-stu-id="a8a97-128">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="a8a97-129">单画布</span><span class="sxs-lookup"><span data-stu-id="a8a97-129">Single canvas</span></span>

<span data-ttu-id="a8a97-130">这是完成工作的一个大区域。</span><span class="sxs-lookup"><span data-stu-id="a8a97-130">This is one large area where work gets done.</span></span> <span data-ttu-id="a8a97-131">Teams Wiki 应用遵循此模式。</span><span class="sxs-lookup"><span data-stu-id="a8a97-131">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="a8a97-132">如果你的应用不将内容分为较小的组件，这非常适合。</span><span class="sxs-lookup"><span data-stu-id="a8a97-132">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="显示 Teams 移动单画布选项卡的图示。" border="false":::

#### <a name="list"></a><span data-ttu-id="a8a97-134">列出</span><span class="sxs-lookup"><span data-stu-id="a8a97-134">List</span></span>

<span data-ttu-id="a8a97-135">列表非常适用于对大量数据进行排序和筛选，并且非常能将最重要的内容放在最上面。</span><span class="sxs-lookup"><span data-stu-id="a8a97-135">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="a8a97-136">使用可排序列很有用。</span><span class="sxs-lookup"><span data-stu-id="a8a97-136">It is helpful to use sortable columns.</span></span> <span data-ttu-id="a8a97-137">可以将操作添加到省略号菜单下的每个列表项。</span><span class="sxs-lookup"><span data-stu-id="a8a97-137">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="显示 Teams 移动列表选项卡的图示。" border="false":::

#### <a name="grid"></a><span data-ttu-id="a8a97-139">网格</span><span class="sxs-lookup"><span data-stu-id="a8a97-139">Grid</span></span>

<span data-ttu-id="a8a97-140">网格对于显示高度可视的元素非常有用。</span><span class="sxs-lookup"><span data-stu-id="a8a97-140">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="a8a97-141">这有助于在顶部包含筛选器或搜索控件。</span><span class="sxs-lookup"><span data-stu-id="a8a97-141">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="插图显示具有网格布局的 Teams 移动选项卡。" border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="a8a97-143">使用移动设备上的机器人的选项卡</span><span class="sxs-lookup"><span data-stu-id="a8a97-143">Tabs with bots on mobile</span></span>

<span data-ttu-id="a8a97-144">以下示例是一个包含选项卡和自动程序的个人应用。</span><span class="sxs-lookup"><span data-stu-id="a8a97-144">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="插图显示具有选项卡和自动程序的移动 Teams 应用。" border="false":::

## <a name="ui-components"></a><span data-ttu-id="a8a97-146">UI 组件</span><span class="sxs-lookup"><span data-stu-id="a8a97-146">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="a8a97-147">调色板</span><span class="sxs-lookup"><span data-stu-id="a8a97-147">Color palettes</span></span>

<span data-ttu-id="a8a97-148">将已批准的中性调色板用于背景、通知、文本和按钮将帮助你的应用在 Teams 中感觉更加自在。</span><span class="sxs-lookup"><span data-stu-id="a8a97-148">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="a8a97-149">由于 Teams 移动版具有 (浅色和深色) 主题，因此，建议确保你的应用在两者中都外观良好。</span><span class="sxs-lookup"><span data-stu-id="a8a97-149">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="a8a97-150">浅色</span><span class="sxs-lookup"><span data-stu-id="a8a97-150">Light color</span></span>

![浅色调色板](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="a8a97-152">深色</span><span class="sxs-lookup"><span data-stu-id="a8a97-152">Dark color</span></span>

![深色调色板](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="a8a97-154">按钮和控件</span><span class="sxs-lookup"><span data-stu-id="a8a97-154">Buttons and controls</span></span>

<span data-ttu-id="a8a97-155">按钮的样式设置有助于传达它们触发的操作类型。</span><span class="sxs-lookup"><span data-stu-id="a8a97-155">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="a8a97-156">我们维护各种按钮，这些按钮经过格式化以显示不同的强调级别。</span><span class="sxs-lookup"><span data-stu-id="a8a97-156">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="a8a97-157">按钮可以有文本、图标或文本和图标的组合。</span><span class="sxs-lookup"><span data-stu-id="a8a97-157">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="a8a97-158">为了传达层次结构中的不同级别，我们设计了每个类别中的主按钮和辅助按钮。</span><span class="sxs-lookup"><span data-stu-id="a8a97-158">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="a8a97-159">按钮</span><span class="sxs-lookup"><span data-stu-id="a8a97-159">Buttons</span></span>

<span data-ttu-id="a8a97-160">主按钮和辅助按钮。</span><span class="sxs-lookup"><span data-stu-id="a8a97-160">Primary and secondary buttons.</span></span>

![按钮图像](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="a8a97-162">选择控件</span><span class="sxs-lookup"><span data-stu-id="a8a97-162">Selection controls</span></span>

<span data-ttu-id="a8a97-163">单选按钮、复选框和切换键。</span><span class="sxs-lookup"><span data-stu-id="a8a97-163">Radio buttons, checkboxes, and toggles.</span></span>

![选择控件](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="a8a97-165">小红和装饰</span><span class="sxs-lookup"><span data-stu-id="a8a97-165">Chiclets and pills</span></span>

![let 和分红](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="a8a97-167">版式</span><span class="sxs-lookup"><span data-stu-id="a8a97-167">Typography</span></span>

<span data-ttu-id="a8a97-168">版式应清晰且有目的。</span><span class="sxs-lookup"><span data-stu-id="a8a97-168">Typography should be clear and purposeful.</span></span> <span data-ttu-id="a8a97-169">强调重要信息并避免使用多个字体和大小以减少混淆。</span><span class="sxs-lookup"><span data-stu-id="a8a97-169">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="a8a97-170">我们建议使用句子大小写，并避免使用全部大写字母进行本地化和易读。</span><span class="sxs-lookup"><span data-stu-id="a8a97-170">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![移动版式](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="a8a97-172">字段和飞出</span><span class="sxs-lookup"><span data-stu-id="a8a97-172">Fields and flyouts</span></span>

<span data-ttu-id="a8a97-173">字段是用户可以输入文本的区域。</span><span class="sxs-lookup"><span data-stu-id="a8a97-173">Fields are areas where users can input text.</span></span> <span data-ttu-id="a8a97-174">弹出控件比对话框更轻量，并且从顶部窗格中显示。</span><span class="sxs-lookup"><span data-stu-id="a8a97-174">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="a8a97-175">列出控件</span><span class="sxs-lookup"><span data-stu-id="a8a97-175">List controls</span></span>

![移动列表控件](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="a8a97-177">字段控件</span><span class="sxs-lookup"><span data-stu-id="a8a97-177">Field controls</span></span>

![移动字段控件](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="a8a97-179">开发人员注意事项</span><span class="sxs-lookup"><span data-stu-id="a8a97-179">Developer considerations</span></span>

<span data-ttu-id="a8a97-180">生成包含选项卡的应用时，需要考虑 (并测试) 在 Android 和 iOS Microsoft Teams 客户端上的运行方式。</span><span class="sxs-lookup"><span data-stu-id="a8a97-180">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="a8a97-181">以下各节概述了需要考虑的一些关键方案。</span><span class="sxs-lookup"><span data-stu-id="a8a97-181">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="a8a97-182">在移动客户端上测试</span><span class="sxs-lookup"><span data-stu-id="a8a97-182">Testing on mobile clients</span></span>

<span data-ttu-id="a8a97-183">需要验证选项卡在各种大小和质量的移动设备上是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="a8a97-183">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="a8a97-184">对于 Android 设备，可以在选项卡运行时使用 [DevTools](~/tabs/how-to/developer-tools.md) 调试选项卡。</span><span class="sxs-lookup"><span data-stu-id="a8a97-184">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="a8a97-185">建议在高性能和低性能设备以及平板电脑上进行测试。</span><span class="sxs-lookup"><span data-stu-id="a8a97-185">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="authentication"></a><span data-ttu-id="a8a97-186">身份验证</span><span class="sxs-lookup"><span data-stu-id="a8a97-186">Authentication</span></span>

<span data-ttu-id="a8a97-187">若要在移动客户端上进行身份验证，必须将 Teams JavaScript SDK 至少升级到版本 1.4.1。</span><span class="sxs-lookup"><span data-stu-id="a8a97-187">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="a8a97-188">低带宽和间歇性连接</span><span class="sxs-lookup"><span data-stu-id="a8a97-188">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="a8a97-189">移动客户端经常需要在低带宽和间歇性连接下运行。</span><span class="sxs-lookup"><span data-stu-id="a8a97-189">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="a8a97-190">应用应该通过向用户提供上下文消息来适当地处理任何超时。</span><span class="sxs-lookup"><span data-stu-id="a8a97-190">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="a8a97-191">您还应使用用户进度指示器，以针对任何长时间运行的过程向用户提供反馈。</span><span class="sxs-lookup"><span data-stu-id="a8a97-191">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

> [!NOTE]
> <span data-ttu-id="a8a97-192">只有在根据审批团队的输入将应用程序添加到允许列表后，才能在移动设备上启用选项卡。</span><span class="sxs-lookup"><span data-stu-id="a8a97-192">Tabs are enabled on mobile only after the application is added to an allow list, based on the input of the approval team.</span></span> <span data-ttu-id="a8a97-193">若要检查移动响应，请与用户联系teamsubm@microsoft.com。</span><span class="sxs-lookup"><span data-stu-id="a8a97-193">To check mobile responsiveness, reach out to teamsubm@microsoft.com.</span></span> 