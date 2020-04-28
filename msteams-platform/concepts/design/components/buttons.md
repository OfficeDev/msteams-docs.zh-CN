---
title: 设计准则参考
description: 介绍在应用程序中使用按钮、链接和控件的准则
keywords: 团队设计准则参考组件按钮链接颜色
ms.openlocfilehash: b9325980c38048ee250ace6b00f1ed29c6cbea8d
ms.sourcegitcommit: 61edf47c9dd1dbc1df03d0d9fb83bfedca4c423b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 04/28/2020
ms.locfileid: "43914586"
---
# <a name="buttons-links-and-controls"></a><span data-ttu-id="bf01f-104">按钮、链接和控件</span><span class="sxs-lookup"><span data-stu-id="bf01f-104">Buttons, links, and controls</span></span>

---

## <a name="button-types"></a><span data-ttu-id="bf01f-105">按钮类型</span><span class="sxs-lookup"><span data-stu-id="bf01f-105">Button types</span></span>

<span data-ttu-id="bf01f-106">按钮的样式方式有助于传达它们触发的操作类型。</span><span class="sxs-lookup"><span data-stu-id="bf01f-106">The way buttons are styled helps communicate what kind of action they trigger.</span></span> <span data-ttu-id="bf01f-107">我们维护各种格式的按钮，以显示不同的强调级别。</span><span class="sxs-lookup"><span data-stu-id="bf01f-107">We maintain a wide range of buttons that are formatted to show different levels of emphasis.</span></span>

<span data-ttu-id="bf01f-108">按钮可以有文本、图标或文本和图标的组合。</span><span class="sxs-lookup"><span data-stu-id="bf01f-108">Buttons can have text, an icon, or a combination of text and an icon.</span></span> <span data-ttu-id="bf01f-109">为了在层次结构中传达不同的级别，我们为每个类别中的主要和辅助按钮设计。</span><span class="sxs-lookup"><span data-stu-id="bf01f-109">To communicate different levels in a hierarchy, we designed primary and secondary buttons within each category.</span></span>

### <a name="fluent-design-system"></a><span data-ttu-id="bf01f-110">熟知设计系统</span><span class="sxs-lookup"><span data-stu-id="bf01f-110">Fluent Design System</span></span>

<span data-ttu-id="bf01f-111">熟知的 UI 为 web 和桌面组件状态、样式和可访问性提供指导。</span><span class="sxs-lookup"><span data-stu-id="bf01f-111">Fluent UI provides guidance for web and desktop component states, styling, and accessibility.</span></span> <span data-ttu-id="bf01f-112">可以对团队平台上的按钮设置格式以显示不同级别的强调。</span><span class="sxs-lookup"><span data-stu-id="bf01f-112">Buttons on the Teams platform can be formatted to show different levels of emphasis.</span></span> <span data-ttu-id="bf01f-113">有关 HTML 和 CSS 十六进制颜色值，*请参阅*[熟知 UI 按钮的颜色](https://fluentsite.z22.web.core.windows.net/components/button/definition?showCode=false&showRtl=false&showTransparent=false&showVariables=true#types-emphasis)。  </span><span class="sxs-lookup"><span data-stu-id="bf01f-113">*See*  [Fluent UI button colors](https://fluentsite.z22.web.core.windows.net/components/button/definition?showCode=false&showRtl=false&showTransparent=false&showVariables=true#types-emphasis) for HTML and CSS hexadecimal color values.</span></span>

### <a name="text-buttons"></a><span data-ttu-id="bf01f-114">文本按钮</span><span class="sxs-lookup"><span data-stu-id="bf01f-114">Text buttons</span></span>

<span data-ttu-id="bf01f-115">在对话框中，应将按钮右对齐，从最右边的主要操作开始。</span><span class="sxs-lookup"><span data-stu-id="bf01f-115">In dialogs, you should align buttons to the right, starting with the primary action farthest to the right.</span></span> <span data-ttu-id="bf01f-116">在卡片中，按钮是左对齐的。</span><span class="sxs-lookup"><span data-stu-id="bf01f-116">In cards, buttons are left-aligned.</span></span>

<span data-ttu-id="bf01f-117">团队中的按钮样式</span><span class="sxs-lookup"><span data-stu-id="bf01f-117">Button styles in Teams</span></span>

<span data-ttu-id="bf01f-118">桌面客户端[!include[Button states](~/includes/design/buttons-image-states.html)]</span><span class="sxs-lookup"><span data-stu-id="bf01f-118">Desktop Client [!include[Button states](~/includes/design/buttons-image-states.html)]</span></span>

<span data-ttu-id="bf01f-119">移动客户端[!include[Mobile button states](~/includes/design/buttons-mobile-image-states.html)]</span><span class="sxs-lookup"><span data-stu-id="bf01f-119">Mobile Client [!include[Mobile button states](~/includes/design/buttons-mobile-image-states.html)]</span></span>

<span data-ttu-id="bf01f-120">对话框按钮[!include[Dialog buttons](~/includes/design/buttons-image-dialog.html)]</span><span class="sxs-lookup"><span data-stu-id="bf01f-120">Dialog buttons [!include[Dialog buttons](~/includes/design/buttons-image-dialog.html)]</span></span>

<span data-ttu-id="bf01f-121">卡片按钮状态[!include[Card button states](~/includes/design/buttons-image-cardstates.html)]</span><span class="sxs-lookup"><span data-stu-id="bf01f-121">Card button states [!include[Card button states](~/includes/design/buttons-image-cardstates.html)]</span></span>

<span data-ttu-id="bf01f-122">卡片按钮[!include[Card buttons](~/includes/design/buttons-image-card.html)]</span><span class="sxs-lookup"><span data-stu-id="bf01f-122">Card buttons [!include[Card buttons](~/includes/design/buttons-image-card.html)]</span></span>

### <a name="icon-buttons"></a><span data-ttu-id="bf01f-123">图标按钮</span><span class="sxs-lookup"><span data-stu-id="bf01f-123">Icon buttons</span></span>

<span data-ttu-id="bf01f-124">图标按钮可以调用操作，也可以在打开和关闭时进行切换。</span><span class="sxs-lookup"><span data-stu-id="bf01f-124">Icon buttons can invoke an action and can also be toggled on and off.</span></span>
[!include[Icon buttons](~/includes/design/buttons-image-icon.html)]

<span data-ttu-id="bf01f-125">在某些情况下，您可以对图标和文本进行配对以提高强调效果。</span><span class="sxs-lookup"><span data-stu-id="bf01f-125">In some cases, you can pair an icon and text to increase emphasis.</span></span>
[!include[Icon text buttons](~/includes/design/buttons-image-icontext.html)]

### <a name="miscellaneous-buttons"></a><span data-ttu-id="bf01f-126">杂项按钮</span><span class="sxs-lookup"><span data-stu-id="bf01f-126">Miscellaneous buttons</span></span>

#### <a name="desktop-clients"></a><span data-ttu-id="bf01f-127">桌面客户端</span><span class="sxs-lookup"><span data-stu-id="bf01f-127">Desktop Clients</span></span>
<span data-ttu-id="bf01f-128">放射状按钮、复选框和切换开关。</span><span class="sxs-lookup"><span data-stu-id="bf01f-128">Radial buttons, checkboxes, and toggle switches.</span></span><br/>
[!include[Other buttons](~/includes/design/buttons-image-others.html)]

#### <a name="mobile-clients"></a><span data-ttu-id="bf01f-129">移动客户端</span><span class="sxs-lookup"><span data-stu-id="bf01f-129">Mobile Clients</span></span>
<span data-ttu-id="bf01f-130">放射状按钮、复选框和切换开关。</span><span class="sxs-lookup"><span data-stu-id="bf01f-130">Radial buttons, checkboxes, and toggle switches.</span></span><br/>
[!include[Other buttons](~/includes/design/buttons-image-mobile-others.html)]

---

## <a name="links"></a><span data-ttu-id="bf01f-131">链接</span><span class="sxs-lookup"><span data-stu-id="bf01f-131">Links</span></span>

<span data-ttu-id="bf01f-132">下面是我们对内嵌文本链接的已批准样式。</span><span class="sxs-lookup"><span data-stu-id="bf01f-132">Here are our approved styles for inline text links.</span></span>
[!include[Approved link styles](~/includes/design/links-image-text.html)]

---

## <a name="style"></a><span data-ttu-id="bf01f-133">Style</span><span class="sxs-lookup"><span data-stu-id="bf01f-133">Style</span></span>

## <a name="size-and-padding"></a><span data-ttu-id="bf01f-134">大小和填充</span><span class="sxs-lookup"><span data-stu-id="bf01f-134">Size and padding</span></span>

<span data-ttu-id="bf01f-135">文本按钮、图标和控件包含在32高容器中，以确保所有控件在视觉上对齐和一致。</span><span class="sxs-lookup"><span data-stu-id="bf01f-135">Text buttons, icons, and controls are contained within a 32px high container to ensure all controls are visually aligned and consistent.</span></span>
[!include[Size and padding](~/includes/design/style-image-size.html)]

### <a name="rounded-corners"></a><span data-ttu-id="bf01f-136">圆角</span><span class="sxs-lookup"><span data-stu-id="bf01f-136">Rounded corners</span></span>

<span data-ttu-id="bf01f-137">文本按钮的拐角半径为3px。</span><span class="sxs-lookup"><span data-stu-id="bf01f-137">Text buttons have a corner radius of 3px.</span></span>
[!include[Rounded corners](~/includes/design/style-image-corners.html)]

### <a name="button-text"></a><span data-ttu-id="bf01f-138">按钮文本</span><span class="sxs-lookup"><span data-stu-id="bf01f-138">Button text</span></span>

<span data-ttu-id="bf01f-139">在文本中使用句首字母以帮助本地化和可读性。</span><span class="sxs-lookup"><span data-stu-id="bf01f-139">Use sentence case in text for buttons to help with localization and legibility.</span></span> <span data-ttu-id="bf01f-140">（换言之，仅将短语或句子中的第一个单词的首字母大写。</span><span class="sxs-lookup"><span data-stu-id="bf01f-140">(In other words, only capitalize the first letter of the first word in a phrase or sentence.)</span></span>
