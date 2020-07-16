---
title: 移动设备上的选项卡
description: 介绍设计适用于移动设备的选项卡的指南。
keywords: 团队设计准则参考框架个人应用移动选项卡
ms.openlocfilehash: ac547e74fd56e4f1da6c731959d8bb59dbe48213
ms.sourcegitcommit: 26b7404142706290810064f8216abaa1c262d1e5
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 07/16/2020
ms.locfileid: "45145921"
---
# <a name="tabs-on-mobile"></a><span data-ttu-id="31cbd-104">移动设备上的选项卡</span><span class="sxs-lookup"><span data-stu-id="31cbd-104">Tabs on mobile</span></span>

> [!NOTE]
> <span data-ttu-id="31cbd-105">如果选择在工作组移动客户端上显示频道/组选项卡，则 `setSettings()` 配置必须具有 `websiteUrl` 属性值（请参阅下文）。</span><span class="sxs-lookup"><span data-stu-id="31cbd-105">If you choose to have your channel/group tab appear on Teams mobile clients, the `setSettings()` configuration must have a value for the `websiteUrl` property (see below).</span></span> <span data-ttu-id="31cbd-106">个人选项卡当前可在[开发人员预览版](~/resources/dev-preview/developer-preview-intro.md)中使用。</span><span class="sxs-lookup"><span data-stu-id="31cbd-106">Personal tabs are currently available in [developer preview](~/resources/dev-preview/developer-preview-intro.md).</span></span> <span data-ttu-id="31cbd-107">将很快发布对移动客户端上的选项卡的完全支持。</span><span class="sxs-lookup"><span data-stu-id="31cbd-107">Full support for tabs on mobile clients will be released soon.</span></span> <span data-ttu-id="31cbd-108">若要准备更新，请在创建选项卡时遵循此处介绍的内容。</span><span class="sxs-lookup"><span data-stu-id="31cbd-108">To prepare for the update, you should follow the presented here when creating your tabs.</span></span>

<span data-ttu-id="31cbd-109">自定义选项卡可以是频道、组聊天或个人应用（包含静态选项卡和/或一对一 bot 的应用程序）的一部分。</span><span class="sxs-lookup"><span data-stu-id="31cbd-109">Custom tabs can be part of a channel, group chat, or personal app (apps that contain static tabs and/or a one-to-one bot).</span></span>

<span data-ttu-id="31cbd-110">应用程序抽屉中的移动客户端提供了个人应用程序。</span><span class="sxs-lookup"><span data-stu-id="31cbd-110">Personal apps are available on mobile clients in the App Drawer.</span></span> <span data-ttu-id="31cbd-111">只能从桌面或 web 客户端安装应用程序，并且在移动客户端上可能需要长达24小时才能显示该应用程序。</span><span class="sxs-lookup"><span data-stu-id="31cbd-111">The app can only be installed from a desktop or web client, and can take up to 24 hours to appear on mobile clients.</span></span>

<span data-ttu-id="31cbd-112">组和频道选项卡也在移动客户端上可用。</span><span class="sxs-lookup"><span data-stu-id="31cbd-112">Group and channel tabs are available on mobile clients as well.</span></span> <span data-ttu-id="31cbd-113">默认行为是使用 `websiteUrl` ，在浏览器窗口中启动您的选项卡。</span><span class="sxs-lookup"><span data-stu-id="31cbd-113">The default behavior is currently to use your `websiteUrl` to launch your tab in a browser window.</span></span> <span data-ttu-id="31cbd-114">但是，可以通过单击选项卡旁边的 "溢出" 菜单，然后选择 "打开"，在移动客户端上加载这些用户 `...` ，这将使用您在**Open** `contentUrl` 团队移动客户端内加载该选项卡。</span><span class="sxs-lookup"><span data-stu-id="31cbd-114">However, they can be loaded on a mobile client by clicking the `...` overflow menu next to the tab and choosing **Open**, which will use your `contentUrl` to load the tab inside the Teams mobile client.</span></span>

![移动应用程序抽屉](../../assets/images/personal-app-mobile.png)

## <a name="developer-considerations-for-mobile-support"></a><span data-ttu-id="31cbd-116">移动支持的开发人员注意事项</span><span class="sxs-lookup"><span data-stu-id="31cbd-116">Developer considerations for mobile support</span></span>

<span data-ttu-id="31cbd-117">在构建包含选项卡的应用程序时，需要考虑（并测试）选项卡在 Android 和 iOS Microsoft 团队客户端上的工作方式。</span><span class="sxs-lookup"><span data-stu-id="31cbd-117">When you're building an app that includes a tab, you need to consider (and test) how your tab will function on both the Android and iOS Microsoft Teams clients.</span></span> <span data-ttu-id="31cbd-118">以下各节概述了您需要考虑的一些关键方案。</span><span class="sxs-lookup"><span data-stu-id="31cbd-118">The sections below outline some of the key scenarios you need to consider.</span></span>

### <a name="testing-on-mobile-clients"></a><span data-ttu-id="31cbd-119">在移动客户端上进行测试</span><span class="sxs-lookup"><span data-stu-id="31cbd-119">Testing on mobile clients</span></span>

<span data-ttu-id="31cbd-120">您需要验证您的选项卡在各种大小和质量的移动设备上是否正常工作。</span><span class="sxs-lookup"><span data-stu-id="31cbd-120">You need to validate that your tab functions properly on mobile devices of various sizes and qualities.</span></span> <span data-ttu-id="31cbd-121">对于 Android 设备，您可以使用[DevTools](~/tabs/how-to/developer-tools.md)在选项卡运行时对其进行调试。</span><span class="sxs-lookup"><span data-stu-id="31cbd-121">For Android devices you can use the [DevTools](~/tabs/how-to/developer-tools.md) to debug your tab while it is running.</span></span> <span data-ttu-id="31cbd-122">我们建议您在高性能和低性能的设备以及平板电脑上进行测试。</span><span class="sxs-lookup"><span data-stu-id="31cbd-122">We recommend that you test on both high and low performing devices, as well as on a tablet.</span></span>

### <a name="responsive-design"></a><span data-ttu-id="31cbd-123">响应式设计</span><span class="sxs-lookup"><span data-stu-id="31cbd-123">Responsive design</span></span>

<span data-ttu-id="31cbd-124">由于您的选项卡可以在屏幕大小范围很广的设备上打开，因此它需要遵循[快速响应设计](https://www.w3schools.com/html/html_responsive.asp)原则。</span><span class="sxs-lookup"><span data-stu-id="31cbd-124">Because your tab can be opened on devices with a wide range of screen sizes, it needs to follow [responsive design](https://www.w3schools.com/html/html_responsive.asp) principles.</span></span> <span data-ttu-id="31cbd-125">所有关键构造在移动设备上都应该是可访问的，并且这些视图不应失真。</span><span class="sxs-lookup"><span data-stu-id="31cbd-125">All of the key constructs should be accessible on mobile devices, and the views should not be distorted.</span></span> <span data-ttu-id="31cbd-126">确保在移动设备上加载选项卡时，可以使用基于手指的导航轻松访问所有按钮和链接。</span><span class="sxs-lookup"><span data-stu-id="31cbd-126">Ensure that when your tab is loaded on a mobile device, all buttons and links are easily accessible using finger-based navigation.</span></span>

### <a name="authentication"></a><span data-ttu-id="31cbd-127">身份验证</span><span class="sxs-lookup"><span data-stu-id="31cbd-127">Authentication</span></span>

<span data-ttu-id="31cbd-128">若要使身份验证在移动客户端上运行，您必须将团队 JS SDK 升级到至少版本1.4.1。</span><span class="sxs-lookup"><span data-stu-id="31cbd-128">For authentication to work on mobile clients, you must upgrade you Teams JS SDK to at least version 1.4.1.</span></span>

### <a name="low-bandwidth--intermittent-connections"></a><span data-ttu-id="31cbd-129">低带宽 & 间歇连接</span><span class="sxs-lookup"><span data-stu-id="31cbd-129">Low bandwidth & intermittent connections</span></span>

<span data-ttu-id="31cbd-130">移动客户端需要在低带宽和间歇性连接中正常运行。</span><span class="sxs-lookup"><span data-stu-id="31cbd-130">Mobile clients regularly need to function with low bandwidth and intermittent connections.</span></span> <span data-ttu-id="31cbd-131">您的应用程序应通过向用户提供上下文相关消息来适当地处理任何超时。</span><span class="sxs-lookup"><span data-stu-id="31cbd-131">Your app should handle any timeouts appropriately by providing a contextual message to the user.</span></span> <span data-ttu-id="31cbd-132">此外，还应为用户提供对任何长时间运行的进程的反馈的用户进度指示器。</span><span class="sxs-lookup"><span data-stu-id="31cbd-132">You should also user progress indicators to provide feedback to your users for any long-running processes.</span></span>

## <a name="design-considerations-for-mobile"></a><span data-ttu-id="31cbd-133">移动的设计注意事项</span><span class="sxs-lookup"><span data-stu-id="31cbd-133">Design considerations for mobile</span></span>

<span data-ttu-id="31cbd-134">通过我们的移动平台，应用可以成为一种沉浸式体验，其中的应用程序内容除了主要团队导航之外，其他所有屏幕都占据了整个屏幕。</span><span class="sxs-lookup"><span data-stu-id="31cbd-134">Our mobile platform allows apps to be an immersive experience with the app content taking up all of the screen apart from main Teams navigation.</span></span> <span data-ttu-id="31cbd-135">若要创建在 Microsoft 团队客户端无缝适应的沉浸式体验，请遵循以下准则。</span><span class="sxs-lookup"><span data-stu-id="31cbd-135">To create an immersive experience that fits seamlessly within the Microsoft Teams client, follow the guidelines below.</span></span>

### <a name="layouts"></a><span data-ttu-id="31cbd-136">布局</span><span class="sxs-lookup"><span data-stu-id="31cbd-136">Layouts</span></span>

<span data-ttu-id="31cbd-137">为选项卡选择正确的布局非常重要。</span><span class="sxs-lookup"><span data-stu-id="31cbd-137">Choosing the correct layout for your tab is important.</span></span> <span data-ttu-id="31cbd-138">您应考虑正在呈现的信息的类型，并选择一个布局来组织它以方便使用。</span><span class="sxs-lookup"><span data-stu-id="31cbd-138">You should consider the kind of information you're presenting, and choose a layout that organizes it for easy consumption.</span></span> <span data-ttu-id="31cbd-139">下面概述了一些可能的选项。</span><span class="sxs-lookup"><span data-stu-id="31cbd-139">Some potential options are outlined below.</span></span>

#### <a name="single-canvas"></a><span data-ttu-id="31cbd-140">单个画布</span><span class="sxs-lookup"><span data-stu-id="31cbd-140">Single canvas</span></span>

<span data-ttu-id="31cbd-141">这是工作完成的一个大型区域。</span><span class="sxs-lookup"><span data-stu-id="31cbd-141">This is one large area where work gets done.</span></span> <span data-ttu-id="31cbd-142">Wiki 应用遵循此模式。</span><span class="sxs-lookup"><span data-stu-id="31cbd-142">The Wiki app follows this pattern.</span></span> <span data-ttu-id="31cbd-143">如果您的应用程序不将内容分隔为较小的组件，这就是理想之地。</span><span class="sxs-lookup"><span data-stu-id="31cbd-143">If you have an app that doesn’t separate content into smaller components this would be a good fit.</span></span>

![单个画布布局](~/assets/images/mobile-single-canvas.png)

#### <a name="list"></a><span data-ttu-id="31cbd-145">列表</span><span class="sxs-lookup"><span data-stu-id="31cbd-145">List</span></span>

<span data-ttu-id="31cbd-146">列表非常适合于对大量数据进行排序和筛选，并且非常适合在顶部保留最重要的内容。</span><span class="sxs-lookup"><span data-stu-id="31cbd-146">Lists are great for sorting and filtering large quantities of data and are great at keeping the most important things at the top.</span></span> <span data-ttu-id="31cbd-147">使用可排序列非常有用。</span><span class="sxs-lookup"><span data-stu-id="31cbd-147">It is helpful to use sortable columns.</span></span> <span data-ttu-id="31cbd-148">可以将操作添加到省略号菜单下的每个列表项。</span><span class="sxs-lookup"><span data-stu-id="31cbd-148">Actions can be added to each list item under the ellipsis menu.</span></span>

![列表布局](~/assets/images/mobile-list.png)

#### <a name="grid"></a><span data-ttu-id="31cbd-150">窗格</span><span class="sxs-lookup"><span data-stu-id="31cbd-150">Grid</span></span>

<span data-ttu-id="31cbd-151">网格对于显示高度直观的元素很有用。</span><span class="sxs-lookup"><span data-stu-id="31cbd-151">Grids are useful for showing elements which are highly visual.</span></span> <span data-ttu-id="31cbd-152">它有助于在顶部添加筛选器或搜索控件。</span><span class="sxs-lookup"><span data-stu-id="31cbd-152">It helps to include a filter or search control at the top.</span></span>

![网格布局](~/assets/images/mobile-grid.png)

### <a name="tabs-with-bots-on-mobile"></a><span data-ttu-id="31cbd-154">移动设备上带有 bot 的选项卡</span><span class="sxs-lookup"><span data-stu-id="31cbd-154">Tabs with bots on mobile</span></span>

<span data-ttu-id="31cbd-155">下面是一个包含两个静态选项卡和一个 bot 的个人应用示例。</span><span class="sxs-lookup"><span data-stu-id="31cbd-155">The below is an example personal app that contains two static tabs and a bot.</span></span>

![移动设备上的选项卡和 bot](~/assets/images/mobile-tab-with-bot.png)

### <a name="ui-components"></a><span data-ttu-id="31cbd-157">UI 组件</span><span class="sxs-lookup"><span data-stu-id="31cbd-157">UI Components</span></span>

#### <a name="color-palettes"></a><span data-ttu-id="31cbd-158">调色板</span><span class="sxs-lookup"><span data-stu-id="31cbd-158">Color palettes</span></span>

<span data-ttu-id="31cbd-159">使用我们为背景、通知、文本和按钮提供的已批准中性调色板，可帮助你的应用程序在团队家庭中更好地感觉。</span><span class="sxs-lookup"><span data-stu-id="31cbd-159">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="31cbd-160">由于团队 mobile 具有两种颜色主题（浅色和深色），因此最好确保您的应用程序在这两个方面看起来非常出色。</span><span class="sxs-lookup"><span data-stu-id="31cbd-160">Since Teams mobile has two colour themes (light and dark), it’s a good idea to make sure your app looks great in both.</span></span>

##### <a name="light-color"></a><span data-ttu-id="31cbd-161">浅色</span><span class="sxs-lookup"><span data-stu-id="31cbd-161">Light color</span></span>

![浅色调色板](~/assets/images/light-color.png)

##### <a name="dark-color"></a><span data-ttu-id="31cbd-163">深颜色</span><span class="sxs-lookup"><span data-stu-id="31cbd-163">Dark color</span></span>

![深色调色板](~/assets/images/dark-color.png)

#### <a name="buttons-and-controls"></a><span data-ttu-id="31cbd-165">按钮和控件</span><span class="sxs-lookup"><span data-stu-id="31cbd-165">Buttons and controls</span></span>

<span data-ttu-id="31cbd-166">按钮的样式方式有助于传达它们触发的操作类型。</span><span class="sxs-lookup"><span data-stu-id="31cbd-166">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="31cbd-167">我们维护各种格式的按钮，以显示不同的强调级别。</span><span class="sxs-lookup"><span data-stu-id="31cbd-167">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span> <span data-ttu-id="31cbd-168">按钮可以有文本、图标或文本和图标的组合。</span><span class="sxs-lookup"><span data-stu-id="31cbd-168">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="31cbd-169">为了在层次结构中传达不同的级别，我们为每个类别中的主要和辅助按钮设计。</span><span class="sxs-lookup"><span data-stu-id="31cbd-169">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

![按钮](~/assets/images/buttons.png)

![选择控件](~/assets/images/selection-controls.png)

![chiclets 和 pills](~/assets/images/chiclets-and-pills.png)

#### <a name="typography"></a><span data-ttu-id="31cbd-173">版式</span><span class="sxs-lookup"><span data-stu-id="31cbd-173">Typography</span></span>

<span data-ttu-id="31cbd-174">版式应清晰和故意。</span><span class="sxs-lookup"><span data-stu-id="31cbd-174">Typography should be clear and purposeful.</span></span> <span data-ttu-id="31cbd-175">强调重要信息并避免使用多种字体和大小，以减少混淆。</span><span class="sxs-lookup"><span data-stu-id="31cbd-175">Emphasize important information and avoid using multiple fonts and sizes to reduce confusion.</span></span> <span data-ttu-id="31cbd-176">我们建议使用句子事例，避免使用所有大写字母以实现本地化和可读性。</span><span class="sxs-lookup"><span data-stu-id="31cbd-176">We recommend using sentence case and avoiding the usage of all caps for localization and legibility.</span></span>

![移动 typograph](~/assets/images/mobile-typography.png)

#### <a name="fields-and-flyouts"></a><span data-ttu-id="31cbd-178">字段和浮出控件</span><span class="sxs-lookup"><span data-stu-id="31cbd-178">Fields and Flyouts</span></span>

<span data-ttu-id="31cbd-179">字段是用户可以在其中输入文本的区域。</span><span class="sxs-lookup"><span data-stu-id="31cbd-179">Fields are areas where users can input text.</span></span> <span data-ttu-id="31cbd-180">Flyouts 比对话框更轻便，显示在顶部窗格中。</span><span class="sxs-lookup"><span data-stu-id="31cbd-180">Flyouts are more lightweight than dialogs, and appear from the top pane.</span></span>

##### <a name="list-controls"></a><span data-ttu-id="31cbd-181">列出控件</span><span class="sxs-lookup"><span data-stu-id="31cbd-181">List controls</span></span>

![移动列表控件](~/assets/images/mobile-list-controls.png)

##### <a name="field-controls"></a><span data-ttu-id="31cbd-183">字段控件</span><span class="sxs-lookup"><span data-stu-id="31cbd-183">Field controls</span></span>

![移动字段控件](~/assets/images/mobile-field-controls.png)
