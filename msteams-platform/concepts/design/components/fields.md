---
title: 设计准则参考
description: 介绍在应用程序中使用字段和 flyouts 的准则
keywords: 团队设计准则引用组件字段和 flyouts
ms.openlocfilehash: 0f62d38bf961ae79b05c599638cefb3c76f46ed4
ms.sourcegitcommit: 4329a94918263c85d6c65ff401f571556b80307b
ms.translationtype: MT
ms.contentlocale: zh-CN
ms.lasthandoff: 02/01/2020
ms.locfileid: "41673425"
---
# <a name="fields-and-flyouts"></a><span data-ttu-id="b0da6-104">字段和 flyouts</span><span class="sxs-lookup"><span data-stu-id="b0da6-104">Fields and flyouts</span></span>

---

## <a name="fields"></a><span data-ttu-id="b0da6-105">Fields</span><span class="sxs-lookup"><span data-stu-id="b0da6-105">Fields</span></span>

<span data-ttu-id="b0da6-106">字段是用户可以在其中输入文本的区域。</span><span class="sxs-lookup"><span data-stu-id="b0da6-106">Fields are areas where users can input text.</span></span>

### <a name="padding-and-size"></a><span data-ttu-id="b0da6-107">填充和大小</span><span class="sxs-lookup"><span data-stu-id="b0da6-107">Padding and size</span></span>

<span data-ttu-id="b0da6-108">单行文本字段是32的固定高度，以匹配其他组件的高度。</span><span class="sxs-lookup"><span data-stu-id="b0da6-108">Single-line text fields are a fixed height of 32px to match the height of other components.</span></span> <span data-ttu-id="b0da6-109">一些文本字段（如 "说明" 字段）可能会垂直增加以允许更多的文本。</span><span class="sxs-lookup"><span data-stu-id="b0da6-109">Some text fields such as description fields may be taller vertically to allow more text.</span></span>
[!include[Padding and size](~/includes/design/fields-image-padding.html)]

### <a name="states"></a><span data-ttu-id="b0da6-110">市</span><span class="sxs-lookup"><span data-stu-id="b0da6-110">States</span></span>

<span data-ttu-id="b0da6-111">这些是文本字段的状态。</span><span class="sxs-lookup"><span data-stu-id="b0da6-111">These are the states of our text fields.</span></span> <span data-ttu-id="b0da6-112">文本字段存在于不同的状态中。</span><span class="sxs-lookup"><span data-stu-id="b0da6-112">Text fields exist in different states.</span></span> <span data-ttu-id="b0da6-113">我们有专用于九种可能的方案的特定设计，包括（从上到下）：静止文本字段、焦点上的键盘以及字段中的光标、在焦点内输入文本的键盘、错误处理已成功、错误处理已成功、明文字段（包括 X 图标）、搜索字段（包括搜索图标）、加载字段和禁用的字段。</span><span class="sxs-lookup"><span data-stu-id="b0da6-113">We have specific designs dedicated to nine possible scenarios, including (top to bottom): Resting text field, Keyboard in focus and cursor inside the field, Keyboard in focus with text entered, Error handling has succeeded, Error handling has failed, Clear text field (including an X icon), Search field (including a Search icon), Loading field, and a Disabled field.</span></span>
[!include[Field states](~/includes/design/fields-image-states.html)]

### <a name="formatting-help-text-and-labels"></a><span data-ttu-id="b0da6-114">设置帮助文本和标签的格式</span><span class="sxs-lookup"><span data-stu-id="b0da6-114">Formatting help text and labels</span></span>

<span data-ttu-id="b0da6-115">字段可以包含占位符文本，以提供所需的信息类型的示例。</span><span class="sxs-lookup"><span data-stu-id="b0da6-115">Fields can contain placeholder text to give an example of the kind of information that is required.</span></span> <span data-ttu-id="b0da6-116">他们还可以保留为用户提供更多上下文的标签。</span><span class="sxs-lookup"><span data-stu-id="b0da6-116">They can also hold labels that give the user more context.</span></span> <span data-ttu-id="b0da6-117">在字段中，文本应始终左对齐。</span><span class="sxs-lookup"><span data-stu-id="b0da6-117">Within a field, your text should always be justified left.</span></span> <span data-ttu-id="b0da6-118">我们也在这里使用句子大小写。</span><span class="sxs-lookup"><span data-stu-id="b0da6-118">We use sentence casing throughout here, as well.</span></span>

<span data-ttu-id="b0da6-119">我们将 Microsoft Yahei UI 常规的12磅（caption）和 $app-灰色-02 用于标签。</span><span class="sxs-lookup"><span data-stu-id="b0da6-119">We use Segoe UI Regular at 12 pt (caption) and $app-gray-02 for labels.</span></span> <span data-ttu-id="b0da6-120">对于 "帮助" 文本，我们使用的是 14 pt （base）和 $app-灰阶-02 的 Microsoft Yahei UI。</span><span class="sxs-lookup"><span data-stu-id="b0da6-120">For help text, we use Segoe UI Regular at 14 pt (base) and $app-gray-02.</span></span>
[!include[Fields typography](~/includes/design/fields-image-typography.html)]

---

## <a name="flyouts"></a><span data-ttu-id="b0da6-121">Flyouts</span><span class="sxs-lookup"><span data-stu-id="b0da6-121">Flyouts</span></span>

<span data-ttu-id="b0da6-122">Flyouts 比对话框更轻便，可以快速消除。</span><span class="sxs-lookup"><span data-stu-id="b0da6-122">Flyouts are more lightweight than dialogs and can be dismissed quickly.</span></span> <span data-ttu-id="b0da6-123">它们可以包含按钮、字段和其他组件。</span><span class="sxs-lookup"><span data-stu-id="b0da6-123">They can contain buttons, fields, and other components.</span></span>
[!include[Flyouts](~/includes/design/flyouts-image.html)]

### <a name="sizing-and-padding"></a><span data-ttu-id="b0da6-124">调整大小和填充</span><span class="sxs-lookup"><span data-stu-id="b0da6-124">Sizing and padding</span></span>

<span data-ttu-id="b0da6-125">我们建议将16px 填充到内容的左侧和右侧。</span><span class="sxs-lookup"><span data-stu-id="b0da6-125">We recommend a 16px padding to the left and right of the content.</span></span>
[!include[Flyouts size and padding](~/includes/design/flyouts-image-sizepadding.html)]

### <a name="placement"></a><span data-ttu-id="b0da6-126">Placement</span><span class="sxs-lookup"><span data-stu-id="b0da6-126">Placement</span></span>

<span data-ttu-id="b0da6-127">Flyouts 是上下文，应放置在触发它的元素的上方、下方或旁边。</span><span class="sxs-lookup"><span data-stu-id="b0da6-127">Flyouts are contextual and should be placed above, below, or beside the element that triggered it.</span></span>

### <a name="scrolling"></a><span data-ttu-id="b0da6-128">上下</span><span class="sxs-lookup"><span data-stu-id="b0da6-128">Scrolling</span></span>

<span data-ttu-id="b0da6-129">标头保留在位置，以便为要滚动的内容提供上下文。</span><span class="sxs-lookup"><span data-stu-id="b0da6-129">The header remains in place to give context to the content being scrolled.</span></span>
[!include[Flyouts scrolling](~/includes/design/flyouts-image-scrolling.html)]

## <a name="mobile"></a><span data-ttu-id="b0da6-130">移动设备</span><span class="sxs-lookup"><span data-stu-id="b0da6-130">Mobile</span></span>

<span data-ttu-id="b0da6-131">字段是接受用户输入的文本输入框。</span><span class="sxs-lookup"><span data-stu-id="b0da6-131">Fields are text-entry boxes that accept input from users.</span></span> <span data-ttu-id="b0da6-132">飞出菜单是显示在顶部窗格中的水平弹出窗口，可用于显示有关项目的更多详细信息。</span><span class="sxs-lookup"><span data-stu-id="b0da6-132">Flyout menus are horizontal pop-up windows that appear from the top pane and can be used to show more detail about an item.</span></span>

### <a name="field-controls"></a><span data-ttu-id="b0da6-133">字段控件</span><span class="sxs-lookup"><span data-stu-id="b0da6-133">Field Controls</span></span>

[!include[Mobile fields](~/includes/design/fields-mobile-image.html)]

### <a name="flyout-menu-list-controls"></a><span data-ttu-id="b0da6-134">浮出菜单列表控件</span><span class="sxs-lookup"><span data-stu-id="b0da6-134">Flyout menu list controls</span></span>

[!include[Mobile flyout menu controls](~/includes/design/flyout-menu-mobile-image.html)]
