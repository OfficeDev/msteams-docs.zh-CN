---
title: 设计准则参考
description: 介绍在应用程序中使用颜色的准则
keywords: 团队设计准则参考组件颜色
ms.openlocfilehash: dab223891e88615b52386d3692d4a98607d6d449
ms.sourcegitcommit: aca9990e1f84b07b9e77c08bfeca4440eb4e64f0
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 11/25/2020
ms.locfileid: "49409062"
---
# <a name="color"></a><span data-ttu-id="bac03-104">颜色</span><span class="sxs-lookup"><span data-stu-id="bac03-104">Color</span></span>

<span data-ttu-id="bac03-105">使用我们为背景、通知、文本和按钮提供的已批准中性调色板，可帮助你的应用程序在团队家庭中更好地感觉。</span><span class="sxs-lookup"><span data-stu-id="bac03-105">Using our approved neutral palette for backgrounds, notifications, text, and buttons will help your app feel more at home in Teams.</span></span> <span data-ttu-id="bac03-106">由于团队有两个颜色主题 (浅色和深色) ，因此最好确保您的应用程序在这两个主题中看起来非常出色。</span><span class="sxs-lookup"><span data-stu-id="bac03-106">Since Teams has two color themes (light and dark), it’s a good idea to make sure your app looks great in both themes.</span></span>

### <a name="app-black-252423"></a><span data-ttu-id="bac03-107">$app-黑色 ( # 252423) </span><span class="sxs-lookup"><span data-stu-id="bac03-107">$app-black (#252423)</span></span>

<span data-ttu-id="bac03-108">最常用的文本颜色。</span><span class="sxs-lookup"><span data-stu-id="bac03-108">Our most commonly-used text color.</span></span> <span data-ttu-id="bac03-109">我们将其用于文本的五个不透明度级别。</span><span class="sxs-lookup"><span data-stu-id="bac03-109">We use it at five levels of opacity for text.</span></span> <span data-ttu-id="bac03-110">文本应主要用于100%、74%、64% 不透明度，因为它是可访问的。</span><span class="sxs-lookup"><span data-stu-id="bac03-110">Text should mainly be used at 100%, 74%, 64% opacity since it is accessible.</span></span> <span data-ttu-id="bac03-111">52% 到36% 的文本应谨慎使用，因为它无法访问。</span><span class="sxs-lookup"><span data-stu-id="bac03-111">Text at 52% and 36% should be used sparingly since it is not accessible.</span></span>

[!include[Appblack color and text](~/includes/design/color-image-appblack-text.html)]

1. <span data-ttu-id="bac03-112">100%-标头和基准文本</span><span class="sxs-lookup"><span data-stu-id="bac03-112">100% - Headers and base text</span></span>
2. <span data-ttu-id="bac03-113">74%-标签、subheads、归属和图标按钮</span><span class="sxs-lookup"><span data-stu-id="bac03-113">74% - Labels, subheads, attributions, and icon buttons</span></span>
3. <span data-ttu-id="bac03-114">64%-邮件预览、帮助文本 (不显示) </span><span class="sxs-lookup"><span data-stu-id="bac03-114">64% - Message previews, help text (not shown)</span></span>
4. <span data-ttu-id="bac03-115">52%-时间戳</span><span class="sxs-lookup"><span data-stu-id="bac03-115">52% - Timestamps</span></span>
5. <span data-ttu-id="bac03-116">36%-禁用的文本</span><span class="sxs-lookup"><span data-stu-id="bac03-116">36% - Disabled text</span></span>

<span data-ttu-id="bac03-117">`$app-black`对于某些 UI 元素，我们还在其他 opacities 中使用：</span><span class="sxs-lookup"><span data-stu-id="bac03-117">We also use `$app-black` at other opacities for some UI elements:</span></span>

[!include[Appblack color and text](~/includes/design/color-image-appblack-ui.html)]

1. <span data-ttu-id="bac03-118">14%-横幅背景</span><span class="sxs-lookup"><span data-stu-id="bac03-118">14% - Banner backgrounds</span></span>
2. <span data-ttu-id="bac03-119">5%-禁用按钮和卡片边框</span><span class="sxs-lookup"><span data-stu-id="bac03-119">5% - Disabled button and card borders</span></span>

### <a name="default-theme-color-ramp"></a><span data-ttu-id="bac03-120">默认主题颜色渐变</span><span class="sxs-lookup"><span data-stu-id="bac03-120">Default theme color ramp</span></span>

<span data-ttu-id="bac03-121">有关 CodePen，请参阅 [Microsoft 团队设计指南-默认主题颜色渐变](https://codepen.io/msteams/pen/KyPmqL/) 。</span><span class="sxs-lookup"><span data-stu-id="bac03-121">See the Pen [Microsoft Teams design guidelines - default theme color ramp](https://codepen.io/msteams/pen/KyPmqL/) on CodePen.</span></span>

<iframe height='620' scrolling='no' title='<span data-ttu-id="bac03-122">Microsoft 团队设计指南-默认主题颜色渐变</span><span class="sxs-lookup"><span data-stu-id="bac03-122">Microsoft Teams design guidelines - default theme color ramp</span></span>' src='//codepen.io/msteams/embed/KyPmqL/?height=682&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="bac03-123">请参阅 microsoft 团队 (<a href='https://codepen.io/msteams'>@msteams</a>) 在<a href='https://codepen.io'>CodePen</a>上的<a href='https://codepen.io/msteams/pen/KyPmqL/'>microsoft 团队设计指南-默认主题颜色滑道</a>。</span><span class="sxs-lookup"><span data-stu-id="bac03-123">See the Pen <a href='https://codepen.io/msteams/pen/KyPmqL/'>Microsoft Teams design guidelines - default theme color ramp</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

### <a name="other-default-theme-colors"></a><span data-ttu-id="bac03-124">其他默认主题颜色</span><span class="sxs-lookup"><span data-stu-id="bac03-124">Other default theme colors</span></span>

<span data-ttu-id="bac03-125">有关 CodePen 的 [其他默认主题颜色，请参阅 Microsoft 团队的 Microsoft 团队设计指南](https://codepen.io/msteams/pen/zPOdYJ/) 。</span><span class="sxs-lookup"><span data-stu-id="bac03-125">See the Pen [Microsoft Teams design guidelines - other default theme colors](https://codepen.io/msteams/pen/zPOdYJ/) on CodePen.</span></span>

<iframe height='392' scrolling='no' title='<span data-ttu-id="bac03-126">Microsoft 团队设计指南-其他默认主题颜色</span><span class="sxs-lookup"><span data-stu-id="bac03-126">Microsoft Teams design guidelines - other default theme colors</span></span>' src='//codepen.io/msteams/embed/zPOdYJ/?height=442&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="bac03-127">请参阅 Microsoft 团队的 <a href='https://codepen.io/msteams/pen/zPOdYJ/'>Microsoft 团队设计指南-其他默认主题颜色</a> (<a href='https://codepen.io/msteams'>@msteams</a> 在 <a href='https://codepen.io'>CodePen</a>上) 。</span><span class="sxs-lookup"><span data-stu-id="bac03-127">See the Pen <a href='https://codepen.io/msteams/pen/zPOdYJ/'>Microsoft Teams design guidelines - other default theme colors</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

### <a name="dark-theme-color-ramp"></a><span data-ttu-id="bac03-128">深色主题颜色渐变</span><span class="sxs-lookup"><span data-stu-id="bac03-128">Dark theme color ramp</span></span>

<span data-ttu-id="bac03-129">请参阅 CodePen 上的 [Microsoft 团队设计指南-深色的主题颜色滑道](https://codepen.io/msteams/pen/BmBwjx/) 。</span><span class="sxs-lookup"><span data-stu-id="bac03-129">See the Pen [Microsoft Teams design guidelines - dark theme color ramp](https://codepen.io/msteams/pen/BmBwjx/) on CodePen.</span></span>

<iframe height='798' scrolling='no' title='<span data-ttu-id="bac03-130">Microsoft 团队设计指南-深色主题颜色渐变</span><span class="sxs-lookup"><span data-stu-id="bac03-130">Microsoft Teams design guidelines - dark theme color ramp</span></span>' src='//codepen.io/msteams/embed/BmBwjx/?height=846&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="bac03-131">请参阅 Microsoft 团队 (<a href='https://codepen.io/msteams'>@msteams</a>) 在<a href='https://codepen.io'>CodePen</a>上的<a href='https://codepen.io/msteams/pen/BmBwjx/'>microsoft 团队设计指南-深色主题颜色滑道</a>。</span><span class="sxs-lookup"><span data-stu-id="bac03-131">See the Pen <a href='https://codepen.io/msteams/pen/BmBwjx/'>Microsoft Teams design guidelines - dark theme color ramp</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>

> <span data-ttu-id="bac03-132">**注意：** Msteams-ui 样式-核心库的实际值被编码为变量。</span><span class="sxs-lookup"><span data-stu-id="bac03-132">**Note:** The msteams-ui-styles-core library has the actual values coded as variables.</span></span> <span data-ttu-id="bac03-133">如果颜色更新，这些变量将非常有用。</span><span class="sxs-lookup"><span data-stu-id="bac03-133">These variables will be helpful if the colors are ever updated.</span></span>


### <a name="other-dark-theme-colors"></a><span data-ttu-id="bac03-134">其他深色主题颜色</span><span class="sxs-lookup"><span data-stu-id="bac03-134">Other dark theme colors</span></span>

<span data-ttu-id="bac03-135">有关 CodePen，请参阅 [Microsoft 团队的 Microsoft 团队设计指南-其他深色主题颜色](https://codepen.io/msteams/pen/zPOEXN/) 。</span><span class="sxs-lookup"><span data-stu-id="bac03-135">See the Pen [Microsoft Teams design guidelines - other dark theme colors](https://codepen.io/msteams/pen/zPOEXN/) on CodePen.</span></span>

<iframe height='390' scrolling='no' title='<span data-ttu-id="bac03-136">Microsoft 团队设计指南-其他深色主题颜色</span><span class="sxs-lookup"><span data-stu-id="bac03-136">Microsoft Teams design guidelines - other dark theme colors</span></span>' src='//codepen.io/msteams/embed/zPOEXN/?height=442&theme-id=31655&default-tab=result&embed-version=2' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'><span data-ttu-id="bac03-137">请参阅 microsoft 团队 (<a href='https://codepen.io/msteams'>@msteams</a>) 在<a href='https://codepen.io'>CodePen</a>上的<a href='https://codepen.io/msteams/pen/zPOEXN/'>microsoft 团队设计指南-其他深色主题颜色</a>。</span><span class="sxs-lookup"><span data-stu-id="bac03-137">See the Pen <a href='https://codepen.io/msteams/pen/zPOEXN/'>Microsoft Teams design guidelines - other dark theme colors</a> by Microsoft Teams (<a href='https://codepen.io/msteams'>@msteams</a>) on <a href='https://codepen.io'>CodePen</a>.</span></span>
</iframe>
