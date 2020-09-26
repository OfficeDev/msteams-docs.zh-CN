---
title: 移动设备上的选项卡
description: 介绍设计适用于移动设备的选项卡的指南。
keywords: 团队设计准则参考框架个人应用移动选项卡
ms.openlocfilehash: a1939465b04a1fe4b803efaf83402852ca536059
ms.sourcegitcommit: b51a4982842948336cfabedb63bdf8f72703585e
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 09/25/2020
ms.locfileid: "48279792"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="19a2c-104">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="19a2c-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="19a2c-105">如果选择在工作组移动客户端上显示 "频道/组" 选项卡，则该 `setSettings()` 配置必须具有该属性的值 `websiteUrl` (请参阅下) 。</span><span class="sxs-lookup"><span data-stu-id="19a2c-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span>

<span data-ttu-id="19a2c-106">自定义选项卡可以是频道、组聊天或个人应用 (包含静态选项卡和/或一对一机器人) 的应用程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="19a2c-106">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="19a2c-107">应用程序抽屉中的移动客户端提供了个人应用程序。</span><span class="sxs-lookup"><span data-stu-id="19a2c-107">Personal apps are available on mobile clients in the app drawer.</span></span> <span data-ttu-id="19a2c-108">只能从桌面或 web 客户端安装应用程序，并且在移动客户端上可能需要长达24小时才能显示该应用程序。</span><span class="sxs-lookup"><span data-stu-id="19a2c-108">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="19a2c-109">移动设备上也提供频道选项卡。</span><span class="sxs-lookup"><span data-stu-id="19a2c-109">Channel tabs are also available on mobile.</span></span> <span data-ttu-id="19a2c-110">默认行为是使用 `websiteUrl` ，在浏览器窗口中启动您的选项卡。</span><span class="sxs-lookup"><span data-stu-id="19a2c-110">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="19a2c-111">但是，可以通过单击选项卡旁边的 "溢出" 菜单，然后选择 "打开"，在移动客户端上加载这些用户 `...` ，这将使用您在**Open** `contentUrl` 团队移动客户端内加载该选项卡。</span><span class="sxs-lookup"><span data-stu-id="19a2c-111">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

## <a name="accessing-personal-tabs"></a><span data-ttu-id="19a2c-112">访问个人选项卡</span><span class="sxs-lookup"><span data-stu-id="19a2c-112">Accessing personal tabs</span></span>

<span data-ttu-id="19a2c-113">下图显示了如何在移动设备上访问个人选项卡。</span><span class="sxs-lookup"><span data-stu-id="19a2c-113">The following illustration shows how you access a personal tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-app-drawer.png" alt-text="显示团队移动应用程序抽屉的图示。" border="false":::

## <a name="accessing-channel-tabs"></a><span data-ttu-id="19a2c-115">访问频道选项卡</span><span class="sxs-lookup"><span data-stu-id="19a2c-115">Accessing channel tabs</span></span>

<span data-ttu-id="19a2c-116">下图显示了如何访问移动设备上的 "频道" 选项卡。</span><span class="sxs-lookup"><span data-stu-id="19a2c-116">The following illustration shows how you access a channel tab on mobile.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab.png" alt-text="显示 "工作组移动" 选项卡的图示。" border="false":::

## <a name="design-considerations"></a><span data-ttu-id="19a2c-118">设计注意事项</span><span class="sxs-lookup"><span data-stu-id="19a2c-118">Design considerations</span></span>

<span data-ttu-id="19a2c-119">通过我们的移动平台，应用可以成为一种沉浸式体验，其中的应用程序内容除了主要团队导航之外，其他所有屏幕都占据了整个屏幕。</span><span class="sxs-lookup"><span data-stu-id="19a2c-119">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="19a2c-120">若要创建适合团队的沉浸式体验，请遵循以下准则。</span><span class="sxs-lookup"><span data-stu-id="19a2c-120">To create an immersive experience that fits with Teams, follow these guidelines.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="19a2c-121">响应式设计</span><span class="sxs-lookup"><span data-stu-id="19a2c-121">Responsive design</span></span>

<span data-ttu-id="19a2c-122">由于您的选项卡可以在屏幕大小范围很广的设备上打开，因此它需要遵循 [快速响应设计](https://www.w3schools.com/html/html_responsive.asp) 原则。</span><span class="sxs-lookup"><span data-stu-id="19a2c-122">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="19a2c-123">所有关键构造在移动设备上都应该是可访问的，并且这些视图不应失真。</span><span class="sxs-lookup"><span data-stu-id="19a2c-123">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="19a2c-124">确保在移动设备上加载选项卡时，可以使用基于手指的导航轻松访问所有按钮和链接。</span><span class="sxs-lookup"><span data-stu-id="19a2c-124">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="layouts"></a><span data-ttu-id="19a2c-125">布局</span><span class="sxs-lookup"><span data-stu-id="19a2c-125">Layouts</span></span>

<span data-ttu-id="19a2c-126">为选项卡选择正确的布局非常重要。</span><span class="sxs-lookup"><span data-stu-id="19a2c-126">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="19a2c-127">您应考虑正在呈现的信息的类型，并选择一个布局来组织它以方便使用。</span><span class="sxs-lookup"><span data-stu-id="19a2c-127">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="19a2c-128">下面概述了一些可能的选项。</span><span class="sxs-lookup"><span data-stu-id="19a2c-128">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="19a2c-129">单个画布</span><span class="sxs-lookup"><span data-stu-id="19a2c-129">Single canvas</span></span>

<span data-ttu-id="19a2c-130">这是工作完成的一个大型区域。</span><span class="sxs-lookup"><span data-stu-id="19a2c-130">This is one large area where work gets done.</span></span> <span data-ttu-id="19a2c-131">团队 Wiki 应用程序遵循此模式。</span><span class="sxs-lookup"><span data-stu-id="19a2c-131">The Teams Wiki app follows this pattern.</span></span> <span data-ttu-id="19a2c-132">如果您的应用程序不将内容分隔为较小的组件，这就是理想之地。</span><span class="sxs-lookup"><span data-stu-id="19a2c-132">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-single-canvas.png" alt-text="显示 "团队移动单个画布" 选项卡的图示。" border="false":::

#### <a name="list"></a><span data-ttu-id="19a2c-134">列表</span><span class="sxs-lookup"><span data-stu-id="19a2c-134">List</span></span>

<span data-ttu-id="19a2c-135">列表非常适合于对大量数据进行排序和筛选，并且非常适合在顶部保留最重要的内容。</span><span class="sxs-lookup"><span data-stu-id="19a2c-135">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="19a2c-136">使用可排序列非常有用。</span><span class="sxs-lookup"><span data-stu-id="19a2c-136">It is helpful to use sortable columns.</span></span> <span data-ttu-id="19a2c-137">可以将操作添加到省略号菜单下的每个列表项。</span><span class="sxs-lookup"><span data-stu-id="19a2c-137">Actions can be added to each list item under the ellipsis menu.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-list.png" alt-text="显示团队移动列表选项卡的图示。" border="false":::

#### <a name="grid"></a><span data-ttu-id="19a2c-139">窗格</span><span class="sxs-lookup"><span data-stu-id="19a2c-139">Grid</span></span>

<span data-ttu-id="19a2c-140">网格对于显示高度直观的元素很有用。</span><span class="sxs-lookup"><span data-stu-id="19a2c-140">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="19a2c-141">它有助于在顶部添加筛选器或搜索控件。</span><span class="sxs-lookup"><span data-stu-id="19a2c-141">It helps to include a filter or search control at the top.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-grid.png" alt-text="图示显示了具有网格布局的 "工作组移动" 选项卡。" border="false":::

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="19a2c-143">移动设备上带有 bot 的选项卡</span><span class="sxs-lookup"><span data-stu-id="19a2c-143">Tabs with bots on mobile</span></span>

<span data-ttu-id="19a2c-144">下面的示例是包含选项卡和机器人的个人应用程序。</span><span class="sxs-lookup"><span data-stu-id="19a2c-144">The following example is a personal app that has tabs and a bot.</span></span>

:::image type="content" source="../../assets/images/tabs/mobile-tab-with-bot.png" alt-text="展示了具有选项卡和 bot 的移动团队应用程序的图示。" border="false":::

## <a name="ui-components"></a><span data-ttu-id="19a2c-146">UI 组件</span><span class="sxs-lookup"><span data-stu-id="19a2c-146">UI components</span></span>

### <a name="color-palettes"></a><span data-ttu-id="19a2c-147">调色板</span><span class="sxs-lookup"><span data-stu-id="19a2c-147">Color palettes</span></span>

<span data-ttu-id="19a2c-148">使用我们为背景、通知、文本和按钮提供的已批准中性调色板，可帮助你的应用程序在团队家庭中更好地感觉。</span><span class="sxs-lookup"><span data-stu-id="19a2c-148">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="19a2c-149">由于团队 mobile 有两个颜色主题 (浅色和深色) ，因此最好确保您的应用程序在这两个方面看起来非常出色。</span><span class="sxs-lookup"><span data-stu-id="19a2c-149">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

#### <a name="light-color"></a><span data-ttu-id="19a2c-150">浅色</span><span class="sxs-lookup"><span data-stu-id="19a2c-150">Light color</span></span>

![浅色调色板](../../assets/images/light-color.png)

#### <a name="dark-color"></a><span data-ttu-id="19a2c-152">深颜色</span><span class="sxs-lookup"><span data-stu-id="19a2c-152">Dark color</span></span>

![深色调色板](../../assets/images/dark-color.png)

### <a name="buttons-and-controls"></a><span data-ttu-id="19a2c-154">按钮和控件</span><span class="sxs-lookup"><span data-stu-id="19a2c-154">Buttons and controls</span></span>

<span data-ttu-id="19a2c-155">按钮的样式方式有助于传达它们触发的操作类型。</span><span class="sxs-lookup"><span data-stu-id="19a2c-155">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="19a2c-156">我们维护各种格式的按钮，以显示不同的强调级别。</span><span class="sxs-lookup"><span data-stu-id="19a2c-156">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="19a2c-157">按钮可以有文本、图标或文本和图标的组合。</span><span class="sxs-lookup"><span data-stu-id="19a2c-157">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="19a2c-158">为了在层次结构中传达不同的级别，我们为每个类别中的主要和辅助按钮设计。</span><span class="sxs-lookup"><span data-stu-id="19a2c-158">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

#### <a name="buttons"></a><span data-ttu-id="19a2c-159">按钮</span><span class="sxs-lookup"><span data-stu-id="19a2c-159">Buttons</span></span>

<span data-ttu-id="19a2c-160">主要和次要按钮。</span><span class="sxs-lookup"><span data-stu-id="19a2c-160">Primary and secondary buttons.</span></span>

![按钮图像](../../assets/images/buttons.png)

#### <a name="selection-controls"></a><span data-ttu-id="19a2c-162">选择控件</span><span class="sxs-lookup"><span data-stu-id="19a2c-162">Selection controls</span></span>

<span data-ttu-id="19a2c-163">单选按钮、复选框和切换。</span><span class="sxs-lookup"><span data-stu-id="19a2c-163">Radio buttons, checkboxes, and toggles.</span></span>

![选择控件](../../assets/images/selection-controls.png)

#### <a name="chiclets-and-pills"></a><span data-ttu-id="19a2c-165">Chiclets 和 pills</span><span class="sxs-lookup"><span data-stu-id="19a2c-165">Chiclets and pills</span></span>

![chiclets 和 pills](../../assets/images/chiclets-and-pills.png)

### <a name="typography"></a><span data-ttu-id="19a2c-167">版式</span><span class="sxs-lookup"><span data-stu-id="19a2c-167">Typography</span></span>

<span data-ttu-id="19a2c-168">版式应清晰和故意。</span><span class="sxs-lookup"><span data-stu-id="19a2c-168">Typography should be clear and purposeful.</span></span> <span data-ttu-id="19a2c-169">强调重要信息并避免使用多种字体和大小，以减少混淆。</span><span class="sxs-lookup"><span data-stu-id="19a2c-169">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="19a2c-170">我们建议使用句子事例，避免使用所有大写字母以实现本地化和可读性。</span><span class="sxs-lookup"><span data-stu-id="19a2c-170">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![移动 typograph](../../assets/images/mobile-typography.png)

### <a name="fields-and-flyouts"></a><span data-ttu-id="19a2c-172">字段和 flyouts</span><span class="sxs-lookup"><span data-stu-id="19a2c-172">Fields and flyouts</span></span>

<span data-ttu-id="19a2c-173">字段是用户可以在其中输入文本的区域。</span><span class="sxs-lookup"><span data-stu-id="19a2c-173">Fields are areas where users can input text.</span></span> <span data-ttu-id="19a2c-174">Flyouts 比对话框更轻便，并显示在顶部窗格中。</span><span class="sxs-lookup"><span data-stu-id="19a2c-174">Flyouts are more lightweight than dialogs and appear from the top pane.</span></span>

#### <a name="list-controls"></a><span data-ttu-id="19a2c-175">列出控件</span><span class="sxs-lookup"><span data-stu-id="19a2c-175">List controls</span></span>

![移动列表控件](../../assets/images/mobile-list-controls.png)

#### <a name="field-controls"></a><span data-ttu-id="19a2c-177">字段控件</span><span class="sxs-lookup"><span data-stu-id="19a2c-177">Field controls</span></span>

![移动字段控件](../../assets/images/mobile-field-controls.png)

## <a name="developer-considerations"></a><span data-ttu-id="19a2c-179">开发人员注意事项</span><span class="sxs-lookup"><span data-stu-id="19a2c-179">Developer considerations</span></span>

<span data-ttu-id="19a2c-180">在构建包含选项卡的应用程序时，需要考虑 (并测试您的选项卡在 Android 和 iOS Microsoft 团队客户端上将如何运行的) 。</span><span class="sxs-lookup"><span data-stu-id="19a2c-180">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="19a2c-181">以下各节概述了您需要考虑的一些关键方案。</span><span class="sxs-lookup"><span data-stu-id="19a2c-181">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="19a2c-182">在移动客户端上进行测试</span><span class="sxs-lookup"><span data-stu-id="19a2c-182">Testing on mobile clients</span></span>

<span data-ttu-id="19a2c-183">您需要验证您的选项卡在各种大小和质量的移动设备上是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="19a2c-183">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="19a2c-184">对于 Android 设备，您可以使用 [DevTools](~/tabs/how-to/developer-tools.md) 在选项卡运行时对其进行调试。</span><span class="sxs-lookup"><span data-stu-id="19a2c-184">For Android devices, you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="19a2c-185">我们建议您在高性能和低性能的设备以及平板电脑上进行测试。</span><span class="sxs-lookup"><span data-stu-id="19a2c-185">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="authentication"></a><span data-ttu-id="19a2c-186">身份验证</span><span class="sxs-lookup"><span data-stu-id="19a2c-186">Authentication</span></span>

<span data-ttu-id="19a2c-187">若要使身份验证在移动客户端上运行，您必须将 JavaScript SDK 升级到至少1.4.1 版本。</span><span class="sxs-lookup"><span data-stu-id="19a2c-187">For authentication to work on mobile clients, you must upgrade you Teams JavaScript SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth-and-intermittent-connections"></a><span data-ttu-id="19a2c-188">低带宽和间歇性连接</span><span class="sxs-lookup"><span data-stu-id="19a2c-188">Low bandwidth and intermittent connections</span></span>

<span data-ttu-id="19a2c-189">移动客户端需要在低带宽和间歇性连接中正常运行。</span><span class="sxs-lookup"><span data-stu-id="19a2c-189">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="19a2c-190">您的应用程序应通过向用户提供上下文相关消息来适当地处理任何超时。</span><span class="sxs-lookup"><span data-stu-id="19a2c-190">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="19a2c-191">此外，还应为用户提供对任何长时间运行的进程的反馈的用户进度指示器。</span><span class="sxs-lookup"><span data-stu-id="19a2c-191">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>
